* text tags
* sorting algorithms/techniques
* setup tools
* map, filter
* sorted(zip()) for sort one list byanother list
* collections.Counter
* global vars
* next
* iter
* itertools
* combinations
* maybe put repeat in second argument during starmap calls, problem at work not parallelizing this
* continuously write to log files,temporary files for progress, grid search iterations completed, loop progress, etc.
* yaml, pyqt, pathlib
* docstrings for auto documentation using sphinx
* tornado web server, gunicorn
* setuptools for making setup.py files
* smooth plots with exponential moving average
* set(list) to get unique list elements
* use tox (integrate with testing in jenkins, travis-ci)
* use threading within class (like Ryan's automodeler)
* flask + gunicorn(maybe tornado) for asynchronous application
* flask gui with api
* only learn flask enough for api development after the two tutorials
* jupyter notebook magic commands
* pprint has stream to file option
* Flask application database storage, populate once at startup?
* flask test coverage page for unit tests
* lots of flask tutorials on digital ocean
* gunicorn/celery/tornado/pyramid web servers for flask/django
* reverse proxy flask applications
* sort one list by another
* function within function definitions
* f strings for better formatting instead of `%` or `.format` calls
* warnings.filterwarnings(action=...,cat=...,module=...)
* checkpointing long running programs
* sqlite3 databases
* numba for offloading calculations on gpu
* map/filter
* multiprocessing shared objects
* importing packages and modules correctly?
* checkpoint programs using logging
* cython?
* <https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-vii-error-handling> the debugging section fake email server is pretty cool, easy directions on using your gmail too.
* linting/coverage
* class static methods are just class methods that dont require the self arguments
* logging smtphandler for sending emails
* pandas iterrows for times where we want to iterate over df instead of apply/map
* pandas reset_index for getting single index df after groupby
* <https://stackoverflow.com/questions/15268953/how-to-install-python-package-from-github>
* filter/map/reduce
* <https://stackoverflow.com/questions/5442910/python-multiprocessing-pool-map-for-multiple-arguments>
* <http://www.racketracer.com/2016/07/06/pandas-in-parallel/>
* <http://blog.adeel.io/2016/11/06/parallelize-pandas-map-or-apply/>
* <https://stackoverflow.com/questions/5442910/python-multiprocessing-pool-map-for-multiple-arguments/5443941#5443941>
* <https://github.com/mkleehammer/pyodbc/wiki/Getting-started>
* <https://stackoverflow.com/questions/35905335/aggregation-over-partition-pandas-dataframe> - pandas transform method for doing a groupby and then say wanting column means
* f strings
* inline if statements without colons
* circular imports when modules depend on another for objects
* __init__.py imports like flask tutorial versus blank file
* never for loop and change values in a dictionary. it becomes immutable, always make a copy in the for loop to set the values needed.
* super() for class inheritance <https://stackoverflow.com/questions/222877/what-does-super-do-in-python>
* <https://medium.freecodecamp.org/a-guide-to-asynchronous-programming-in-python-with-asyncio-232e2afa44f6>
* smtphandler in logging for email
* python has internal webserver for testing things, probably want one on the network for little email support or get google api key and some alternative to the plain text.
* proper use of __init__.py, either blank or module imports like flask app
* dataclasses for simpler class constructs
* <https://rise.cs.berkeley.edu/blog/pandas-on-ray-early-lessons/> parallel pandas
* <http://takluyver.github.io/posts/so-you-want-to-write-a-desktop-app-in-python.html>
* pandas.series.isin for testing multiple equalities
* np.where for conditional column settings
* lambda x: x if condition else not x
* pandas pivot tables for making categorical tables
* pandas cross tab for making categorical count tables
