# file structure #
```
app/
venv/
app/
__init__.py
functions.p
main.py
config.py
```

# software carpentry #

# modularization #

Circular imports.

# google style guide #
<https://github.com/google/styleguide/blob/gh-pages/pyguide.md>

Consistent variable naming, function naming, class naming, separation of modules, class versus function, modularization, nested function definitions.

# asynchronous vs parallel vs concurrent vs coroutine #
- parallel distributes tasks to multiple processors that actively work simultaneously
- concurrent handle tasks that are in progress at same time, but only necessary to work briefly and separately on each task, so work can be interleaved on whatever order the tasks require
- Asynch dispatches tasks to devices that take care of themselves, so the program can do other things until it receives a signal that the results are finished

# share global variable between files #
Not suggested unless annoying to have it as function argument in everything.

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

# dry principals #

# logging #

Logging at module level. Multiple loggers. Different logging levels. Notifying administrator on exceptions and logging exceptions on program failure.

# nested function definitions #

# ci/cd #
Build test cases into program, add docker executable build to part of pipeline, commit to remote repository triggers an image build that runs tests, notifies administrator upon failure or deploys image and pushes image to docker hub.

# change log #

# responding to issues on github and making changes #

# proper versioning - something at work on this #

# licensing #

# version control #
Proper branching and tagging.

# documentation #
Using a documentation generator like Sphinx for auto-generating documentation.

# linting #

# code coverage #

# unit testing #

# checkpoint programs with log files? #
