# folder structure #

```
top level package_name
package_name/
tests/
venv/
data/
.travis/
.gitignore
.dockerignore
Dockerfile
.travis.yml
Procfile
README.md
...
```


# Send Email #

Unfortunately requires the use of password in plain text, but so long as used internally this is fine. Can also use environment variables here for safety.

```
import smtplib
smtp_server = smtplib.SMTP('smtp.gmail.com', 587)
smtp_server.ehlo()
smtp_server.starttls()
smtp_server.login('email', 'password')
smtp_server.sendmail('from', ['to'], 'message')
smtp_server.quit()
```

# Parallelism In Almost One Line #

For a function taking a single argument:

```
from multiprocessing import cpu_count, Pool

def f(x):
return x*x

pool = Pool(cpu_count())
results = pool.map(f, [1, 2, 3])
pool.close()
pool.join()
del pool
```

For a function taking multiple arguments:

```
from multiprocessing import cpu_count, Pool

def f(a, b):
return a + b

pool = Pool(cpu_count())
data = [(1, 2), (3, 4)]
results = pool.starmap(f, data)
pool.close()
pool.join()
del pool
```

For use with pandas DataFrames, create a wrapper for your function:

```
import pandas as pd
import numpy as np
from multiprocessing import cpu_count, Pool

df = pd.DataFrame({'a': ['chop', 'me', 'up'],
'b': ['3', '6', 'mafia']})

def join_rows(df):
df['joined_column'] = df.apply(lambda x: ' '.join(x), axis = 1)
return df

def join_rows_parallel(df, num_cores):
df_split = np.array_split(df, num_cores)
pool = Pool(num_cores)
df = pd.concat(pool.map(join_rows, df_split))
pool.close()
pool.join()
del pool
return df
```

# Logging Output #

Instead of including lots of print statements to be excluded later, logging to the console or a file can be useful for debugging.

```
import logging

logging.basicConfig(filename = 'mylogfile.log',
level = logging.DEBUG,
format = '%(asctime)s:%(levelname)s:%(message)s')

def foo(x):
logging.debug('calling foo {}'.format(x))
# do stuff

def bar(x):
logging.debug('calling bar {}'.format(x))
if x > y:
logging.warning('x > y')
# do stuff

if __name__ == '__main__':
data = foo(x)
logging.info('foo is still working')
transform = bar(x)
logging.shutdown()
```

# improved logging #
This snippet adds email on exception support and fixes log file size, so when log files are 10MB, a new log file will be created and the old one will have end in .log.#. Here we set 2 backups, so we will have a .log, and .log.1, and .log.2 with .log.2 being the oldest. Would want to empty the logs directory on application startup. Using the process id in log file names allows logging of multiple processes. We can also then use regular expressions for particular expressions we want to find too. There's also an SMTPHandler for emailing logs more seamlessly than our ad-hoc way.
```
import os
import sys
import re
import traceback
import logging
from logging.handlers import RotatingFileHandler

def log_except_hook(*exc_info):
exception = "".join(traceback.format_exception(*exc_info))
app_log.error("Unhandled exception:\n%s", exception)
send_email(exception) # uses existing email construct

log_format = logging.Formatter('%(asctime)s:%(levelname)s:%(message)s')
log_file = './logs/process_' + str(os.getpid()) + '.log'
handler = RotatingFileHandler(log_file, mode = 'a', maxBytes = 10 * 1024 * 1024, backupCount = 2, encoding = None, delay = 0)
handler.setFormatter(log_formatter)
handler.setLevel(logging.DEBUG) # or logging.info
app_log = logging.getLogger('root') # not sure if value should be given to getLogger or not
app_log.setLevel(logging.DEBUG)
app_log.addHandler(handler)

sys.excepthook = log_except_hook

regex = "log expression we are looking for"
logs = os.listdir('./logs/')
for log in logs:
if log.endswith('.log'):
with open('./logs/' + log) as infile:
log = infile.read()
print(re.findall(regex, log))

```

# Try-Except-Else-Finally #
For more complicated try-except blocks, there's the `else` and `finally` additions. `else` will be executed if there are __no__ exceptions, interrupted by a `return`, `continue`, or `break` statement. `finally` is executed no matter the result, so this construct can be useful for logging information and returning purposes.

```
def foo(x):
try:
f = open(x, 'r')
except IOError:
logging.debug('file x not found')
# do something after error with package to return
else:
print(x, 'has', len(f.readlines()), 'lines')
# continue processing with package to return
finally:
logging.debug('we finished this function')
return package
```


# Break During Function Execution #
Sometimes it can be useful to break out of a function that takes too long to execute.

```
import signal
import time

class TimeoutException(Exception):
pass

def timeout_handler(signum, frame):
raise TimeoutException

if __name__ == '__main__':
signal.signal(signal.SIGALRM, timeout_handler)

# raise TimeoutException after 5 seconds
signal.alarm(5)
try:
time.sleep(10)
# possibly long function
except TimeoutException:
print('function took too long, moving to a shorter function')
# some shorter function
# logging.info('...')
# except TimeoutException:
# continue
else:
# reset alarm
signal.alarm(0)
# continue processing long function
finally:
return result
```

# *args, **kwargs #

`*args` unpacks all arguments into a function and can be used for shorthand function calls or variable length function calls, eg,

```
def f(z, *args):
for num in args:
z *= num
return z
```

```
def f(...param = None...):
....
if param:
...
...
```

# retrying module #

Useful module for handling 'unreliable' functions, like connecting to SQL servers for instance. Instead of throwing an exception, `retrying` will keep retrying to connect.

```
from retrying import retry

def retry_if_result_none(result):
"""
Return True if we should retry
"""
return result is None

@retry(wait_fixed = , stop_max_attempt_number = , wait_random_min = , wait_random_max =, retry_on_result = retry_if_result_none)
def unreliable_function_might_return_none():
print('retry if result is None, throw exception otherwise')
```

This snippet will continue to retry the function so long as the `retry_on_result` function is true.

# Suppress Warnings #

For cases when we want to suppress warnings

```
import warnings
...
def warn(*arg, **kwargs):
pass
...
if __name__ == '__main__':
warnings.warn = warn
...
```

# flatten variably nested lists #
```
def flatten(l):
"""flatten multilevel nested lists whereas itertools.chain.from_iterable only works for singly nested lists"""
for el in l:
if isinstance(el, collections.Iterable) and not isinstance(el, (str, bytes)):
yield from flatten(el)
else:
yield el
```

# find parents of children that may also be children #
```
def traverse_parents(child_dict, obj):
"""for when we have objects that are children of parents that also might be children
recursively find the parents after only computing the (parent, child) relationships once
assumes that child_dict is of form child:[parents]
works well in combination with the flatten function above"""
if not obj in child_dict:
return [obj]
else:
parents = child_dict[obj]
out = []
for p in parents:
result = traverse_parents(child_dict, p)
# appends a list of lists possibly
out.append(result)
return out
```

# flatten dataframe with list element column #
```
def split_df_list(frame, target_column):
"""Unpacks dataframe list column into multiple rows"""
tmp = pd.DataFrame({
col:np.repeat(frame[col].values, frame[target_column].str.len())
for col in frame.columns.difference([target_column])
}).assign(**{target_column:np.concatenate(frame[target_column].values)})[frame.columns.tolist()]
return tmp
```

# monitoring script when email on fail support isnt great #

//Does not work exactly as expected currently.//

```
import os
import psutil
import smtplib
import datetime
import time

def send_email(fproc):
sender = 'email@example.com'
receivers = ['email@example.com']
message = """
From: First Last <email@example.com>
To: First Last <email@example.com>
Subject: Your Program crashed

This message is to notify the current administrator that {} has failed.
This message was triggered at {:%Y-%m-%d %H:%M:%S}.
"""
smtpObj = smtplib.SMTP('smtp.example.com', 25)
smtpObj.sendmail(sender, receivers, message.format(fproc, datetime.datetime.now()))

if __name__ == '__main__':
with open('run.sh', encoding = 'utf-8') as infile:
progs = infile.read().split('\n')
progs.pop(0)
progs = [p.split()[1] for p in progs]
os.system('./run.sh &')
procs = [p for p in psutil.process_iter() if p.name() == 'python' and p.cmdline()[1] in progs]
calls = [p.cmdline() for p in procs]
while True:
for i in range(len(procs)):
if not procs[i].is_running():
send_email(calls[i])
time.sleep(120)
```

# sharing global variables between modules #

```
# settings.py
def init():
global myvar
myvar = []

# subfile.py
import settings

def stuff():
settings.myvar.append('hey')

# main.py
import settings
import subfile
settings.init() # initialize global variable
subfile.stuff() # do stuff with global variable
```

# Moving window of all possible substrings #
```
import itertools
def substrings(x):
for i, j in itertools.combinations(range(len(x) + 1), 2):
yield x[i:j]
if __name__ == '__main__':
x = ['alex', 'allison', 'maple', 'cheyenne', 'claire']
result = substrings(x)
for r in result:
print(' '.join(r))
```
