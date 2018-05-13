### Send Email 

Unfortunately requires the use of password in plain text, but so long as used internally this is fine. 

```
import smtplib
smtp_server = smtplib.SMTP('smtp.gmail.com', 587)
smtp_server.ehlo()
smtp_server.starttls()
smtp_server.login('email', 'password')
smtp_server.sendmail('from', ['to'], 'message')
smtp_server.quit()
```

### Parallelism In Almost One Line 

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
from multiprocessing import cpu_count,  Pool

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

### Logging Output 

Instead of including lots of print statements to be excluded later, logging to the console or a  file can be useful for debugging.

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

### Try-Except-Else-Finally 
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


### Break During Function Execution 
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

### *args, **kwargs 

`*args` unpacks all arguments into a function and can be used for shorthand function calls or variable length function calls, eg,

```
def f(z, *args):
    for num in args:
        z *= num
    return z
```

`**kwargs` is a dictionary of optional parameters for a function, it is an alternative to having 
```
def f(...param = None...): 
    ....
    if param:
        ...
    ...
```

### retrying module 

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

### Suppress Warnings 

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