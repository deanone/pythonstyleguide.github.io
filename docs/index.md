This document presents a set of guidelines for developing applications using Python. These guidelines aim to enhance readability and consistency of the code, enabling also its effective reuse and extension for new applications. 

## Imports

All imports should be on the top of the script file and should be on separate lines. 

```python
# good
import os
import sys

# bad
import os, sys
```
Sub-package imports should also be included along with the rest of the imports.

```python
# good
from package1 import subpackage1, subpackage2
a = subpackage1.do_something()

# bad
import package1
a = package1.subpackage1.do_something()
```
When importing a module, all code at the top level will be executed. It is very important, even for files that are meant to be executables only, to include the main functionality within one or more functions and always perform the check ```if __name__ == '__main__'``` before executing the main program. 

```python
def fun1():
    pass # do something
  
if __name__ == "__main__": 
    results = fun1() 
```

This way, ```fun1()``` from the example script above can also be imported in another script if needed.

```python

from abc import fun1

def fun2(results):
    pass # do something
  
if __name__ == "__main__":
    results = fun1()
    fun2(results) 
```

## Naming

Guidelines derived from Guido’s Recommendations (PEP 8 Style Guide):

Type | Format
------------ | -------------
Packages | ```lower_with_under``` 
Modules | ```lower_with_under``` 
Classes | ```CapWords``` 
Exceptions | ```CapWords``` 
Functions | ```lower_with_under()``` 
Global/Class Constants | ```CAPS_WITH_UNDER``` 
Global/Class Variables | ```lower_with_under``` 
Instance Variables | ```lower_with_under``` 
Method Names | ```lower_with_under()``` 
Function/Method Parameters | ```lower_with_under``` 
Local Variables | ```lower_with_under```

Function names, variable names, and filenames should be descriptive and they should start with a lowercase character. Class names should normally use the CapWords convention. Always use a .py filename extension.

```python
# good
def multiply_by_4(x):
    return x * 4

multiplication_result =  multiply_by_4(3)

# bad
def fun(x):
    return x * 4   

a = fun(5)
```

Python is dynamically typed and a single variable can be set to many different values. Therefore, you should avoid using the same variable name for different declarations within your code.  

```python
# bad
result = [1, 2, 3]
result = 'this is a string' 
result = result_from_a_function() 
result = result_from_another_function() 
```

## Declaring List and Dictionary variables

When declaring a list variable it is convenient to use the following format: 

```python
my_list = [
    "element1",
    "element2",
    "element3"
]
```

Furthermore, using a comma after the last list element can be helpful when adding new elements or when a version control system is used to review code changes that include modifications in the list. 

If you use this pattern, each value must be placed on a line by itself and the close parenthesis/bracket/brace on the next line.

```python
# good
my_list = [
    "element1",
    "element2",
    "element3", 
]

# bad
my_list = ["element1", "element2",]
```

Use similar format when declaring a dictionary variable:

```python
my_dict = {
    "key1": {
        "subkey1": "value1"
    },
    "key2": "value2",
    "key3": "value3"
}
```

## Indentation

Indent your code blocks with 4 spaces.


In case of long function names, align the arguments on the next line after the open parenthesis or bracket on the first line.

```python
# good
def long_function_with_lots_of_arguments(argument1, argument2, argument3,
                                         argument4, argument5, argument6):
    ...

# bad
def long_function_with_lots_of_arguments(argument1, argument2, argument3,
         argument4, argument5, argument6):
    ...

```

## Whitespace

Do not use whitespace before a comma, semicolon, or colon. Avoid trailing whitespace anywhere.

Do use a whitespace after a comma, semicolon or colon. In order to enhance readability, use a whitespace before and after equality sign (=) and number sign (#) in case of comments.

```python
# good
get_order_info(orders[0], {id: "1234"})
my_list = []
i = i + 1

# bad
get_order_info( orders[ 0 ], { id: "1234" } )
my_list=[]
i=i+1
```

## Comments and Docstrings

Write docstrings for all public modules, functions, classes, and methods. Docstrings should provide a brief description of the general functionality, along with the description and type of the input and return values.  

Always use the three double-quote """ format for docstrings (PEP 257).

Docstrings should follow the Sphinx docstring format in order be able to automatically generate Sphinx documentation (https://www.sphinx-doc.org/en/master/) for the module.

```python
def sample_function(ParamName):
    """
    [Summary]

    :param [ParamName]: [ParamDescription], defaults to [DefaultParamVal]
    :type [ParamName]: [ParamType](, optional)
    ...
    :raises [ErrorType]: [ErrorDescription]
    ...
    :return: [ReturnDescription]
    :rtype: [ReturnType]
    """
    
    ...
```

Comments should be complete sentences that have a clear and easily understandable explanation. It is important to include a few lines of comments before complicated operations. 

In case inline comments are used, they should start at least 2 spaces away from the code with the comment character #, followed by at least one space before the text of the comment itself. 

```python
l = [1, 2, 3, 4]
l = l[::-1]  # Reverse the order of the elements in the list
```
In general, you should avoid using inline comments too often. You should also avoid using redundant comments: 
```python
# bad
compute_RMSE() # compute RMSE
```

## Line length

Maximum line length is 79 characters. 

Regarding docstrings or comments, the line length should be limited to 72 characters. 

```python
# good
sample_fun(parm1, param2, param3="test", param4=None,
           param5=None, param6=0)

if (param1 == 0 and param2 == 0 and
    param3 == 2 and param4 == 5):
    
    ...
```
Exceptions to this rule include long URLs or pathnames (if it is possible put them in a separate line).

```python
# you can find the documentation here:
# https://example.com/api/documentation/v2.0/swagger.html
```

Use parenthesis when separating a long string in multiple lines.  

```python
s = ("this is my really, really, really, "  
     "really long string that I'd like to split.")
```

Surround top-level function and class definitions with two blank lines. 
Method definitions inside a class are surrounded by a single blank line.

## Statements

Do not use multiple statements on the same line. 

```python
# good
if condition:
    do_something()

for order in orders:
    process_orders()

# bad
if condition: do_something
for order in orders: process_order(order)
do_something(); do_another_thing();
```

## Project Structure

Project structure is very important and identifies the way modules are organized within a project. As the code repository is getting larger, a proper folder and module structure will enhance code maintenance and development. An example project repository is presented below: 

```python
docs/
myexampleproject/
    __init__.py
    app.py
    helpers.py
    tests/
        __init__.py
        test_helpers.py
    ..
    ..
requirements.txt
.gitignore
readme.md
```
The *docs* directory should contain the documentation of the project's modules, classes and functions. You can use Sphinx (https://www.sphinx-doc.org/en/master/) for automatically creating the documentation. A *requirements.txt* file containing required pip packages and versions should be placed at the root of the repository. It should specify the dependencies required to run the project. A *readme* file should be included in each project, containing basic instructions on executing the project.

Core module functions, used to execute a main process, should be included in the main project file (e.g., app.py, service.py, etc.). Helper functions, used to perform helper operations (e.g., calculations, database queries etc.), should be included in a seperate file (e.g., helpers.py, utils.py, etc.). This way, code readability and maintainability is enhanced, business logic is included in a single file and the corresponding functions can be imported into different modules if needed. You should use a similar structure for your Jupyter notebooks - define your helper functions in a seperate *.py* file and import it in the top of the notebook.

## Unit Testing 
Testing your code is very important. Unit tests are code-level tests, written to verify small units of functionality. They should be designed to provide a broad testing coverage and their goal is to detect possible bugs, along with ensuring that code changes do not cause other modules to fail. One of the unit testing frameworks you can use in Python is *unittest* (https://docs.python.org/3/library/unittest.html#module-unittest). It supports test automation, sharing of setup and shutdown code for tests, aggregation of tests into collections and tests independence. A simple example based on the aforementioned project structure is presented below:

First, let's define a helper function (helpers.py):
```python
def multiply_number_by_four(x):
    return x * 4
```

Now, lets create a test in order to verify our function is working correctly (tests/test_helpers.py)
```python
import unittest
from helpers import multiply_number_by_four

class TestHelpers(unittest.TestCase):
    def test_multiply_number_by_four(self):
        self.assertEqual(multiply_number_by_four(3), 12) 

if __name__ == '__main__':
    unittest.main()
```
In that case, init file can be an empty python file, used to to mark tests/ directory as Python package directory. Now, tests can be executed from the parent directory using the following command:
```python
cd myexampleproject
python -m unittest tests.test_helpers
```
Alternatively, unit tests can be automatically discovered from unittest using the command (still inside the project directory):
```python
python -m unittest discover
```
or you can set up a test suite, which is a collection of test cases used to aggregate tests that should be executed together.

## Decorators

Decorators can be used to specify a transformation on a method. They are functions that extend the behavior of other functions without explicitly modifying them.A few usage examples include adding logging, verifying permissions etc. and can be used in order to eliminate repetitive code. Consider the example below:

```python
from datetime import datetime
from functools import wraps
import logging 

def log_datetime(func):
    """
    Log the execution date and time of a function
    """
    @wraps(func)
    def wrapper():
        logging.basicConfig(level=logging.DEBUG, format='%(message)s')
        logging.debug('Function: {} executed on: {}'.format(
                func.__name__, 
                datetime.today().strftime("%Y-%m-%d %H:%M:%S")
            ))
        func()

    return wrapper

@log_datetime
def perform_API_request():
    """
    Perform an API request
    """
    pass

if __name__ == '__main__': 
    perform_API_request()
```

By defining the decorator log_datetime we are able to decorate various functions in order to perform logging operations. Another good example of functionality handled with decoration is memoization or caching. In this case, we can store the results of an expensive function and use them directly instead of recomputing them. More information about decorators can be found here: https://wiki.python.org/moin/PythonDecoratorLibrary

## Context Managers

Context managers allow you to effectively allocate and release resources. The most widely used example of context managers is the *with* statement: 

```python
with open('my_file.txt', 'w') as file_to_update:
    file_to_update.write('File Updated!')
```

In the example above, we open the file, write data to it and then close it. We could have used a *try/finally* block to execute the same operation, but using *with* statement we make the code cleaner and easier to read. 

There are two ways of implementing context managers. The first way is to implement them as a class: 

```python

class MyFileHandler(object):
    def __init__(self, filename, method):
        self.file_obj = open(filename, method)
    def __enter__(self):
        return self.file_obj
    def __exit__(self, exc_type, exc_value, exc_traceback):
        if self.file_obj:
            self.file_obj.close()
        if exc_value:
            print("An exception occurred: ", exc_type)
            print("Exception message: ", exc_value)
            # Handle exception here...
            
        return True

with MyFileHandler('my_file.txt', 'w') as file_to_update:
    file_to_update.write('File Updated!')

```
MyFileHandler is first instantiated and then *enter* method is called, opens the file object and returns it. Within the *with* block we write to the file and when this operation is finished, the *exit* method is called to close the file. Exception handling is performed within the *exit* method. Based on the example above, we could have executed the following:

```python
with MyFileHandler('my_file.txt', 'w') as file_to_update:
    file_to_update.undefined_function()
```
In that case we would receive the following output:

```python
An exception occurred:  <class 'AttributeError'>
Exception message:  '_io.TextIOWrapper' object has no attribute 'undefined_function'
```

Another way of implementing context managers is by using generators:

```python
from contextlib import contextmanager
     
@contextmanager
def my_custom_open_file_func(filename):
    filename_opened = open(filename, 'r')
    try:
        yield filename_opened
    except Exception as e:
        print("Handling Exception: ", e)
        # Handle exception here...
    finally:
        filename_opened.close()

with my_custom_open_file_func('my_file.txt') as file_to_read:
    contents = file_to_read.read()
```

The *my_custom_open_file_func* function executes until it reaches the yield statement. Due to this, it creates a generator and returns to the *with* statement, which then assigns the value to *file_to_read*. The *except* clause handles exceptions that may occur and the *finally* clause closes the file when the operation is finished. 

In case we need to perform a simple action, it is better to use the generators implementation. 

## Loops and Vectorization

You should avoid using too many loops and if-statements, as it may result in complicated code, hard to extend and debug. Considering performance, it is better to use vectorized operations instead of *for loops*. Vectorization is the implementation of array operations without using *for loops*. It is used widely in mathematical models because it provides faster execution and less code size. Packages *NumPy* and *pandas* offer such capabilities. For example, using the pandas *apply()* function (https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.apply.html), a function can be applied to an entire DataFrame. In the following example, NumPy *sum()* function can be used to sum the elements of an array: 

```python
import numpy as np
my_test_array = np.arange(10000)

# Good
my_test_array_sum = np.sum(my_test_array)

# Bad
my_test_array_sum = 0
for i in my_test_array:
    my_test_array_sum += i
```

Another example using pandas:

```python
import pandas as pd
import numpy as np

grades_df = pd.DataFrame(np.random.randint(1,10, size=100), columns=['grade'])
grades_df['status'] = ''

# Naive Python looping
for i in range(0, len(grades_df)):
    if grades_df['grade'][i] >= 5:
        grades_df.at[i, 'status'] = 'Passed'
    else:
        grades_df.at[i, 'status'] = 'Failed'

# Using apply() function
def compute_status(x):
    if x['grade'] >= 5:
        return 'Passed'
    else:
        return 'Failed'

grades_df['status'] = grades_df.apply(lambda x: compute_status(x), axis=1)

# Using vectorization
def grades_vector(grade):
    grades_df.loc[(grade >= 5), 'status'] = 'Passed'
    grades_df.loc[(grade < 5), 'status'] = 'Failed'

grades_vector(grades_df['grade'])
```

## Comprehensions

Comprehensions provide a way to map a list (or a dictionary) into another list (or dictionary) by applying a function to each one of the elements. Any Python expression can be used in a comprehension. Moreover, comprehensions can be used for mapping and filtering:

```python
my_list_of_integers = [1, 2, 3, 4, 5]

# Good
my_list_of_integers_filtered = [i for i in my_list_of_integers if i > 3]

# Bad
my_list_of_integers_filtered = []
for i in range(0, len(my_list_of_integers)):
    if my_list_of_integers[i] > 3:
        my_list_of_integers_filtered.append(my_list_of_integers[i])

```

List comprehensions are more declarative than loops and they can be used to make your code easy to read and debug. However, they should not be used in all circumstances (i.e., when you need to include too much into a single statement).

## Modules, Functions and Classes

Organize your code into modules. Each module may contain multiple classes and functions. Functions should be small and perform a single operation (e.g., set an object, query database and return information, etc.). You should split large functions into smaller ones and always use descriptive names (e.g., get_all_orders(), get_single_order(), generate_report(), etc.). 

Classes can be useful in large projects, as they favor code organization and reusability. They can be used to encapsulate the implementation details or state of an object. You should use classes if you need to keep state and logically group together methods and function that perform operations on data. 

When defining a class, you need to be careful with declaring mutable variables (e.g., lists, dictionaries) as class variables. Consider the following example: 

```python
class Shirt:
    
    # mistaken use of a class variable
    colours = []             

    def __init__(self, name):
        self.name = name

    def add_colour(self, colour):
        self.colours.append(colour)

>>> s1 = Shirt('shirt-091123')
>>> s2 = Shirt('shirt-1231sf')
>>> s1.add_colour('red')
>>> s2.add_colour('blue')

# unexpectedly colours are shared by all shirts
>>> s1.colours                      
['red', 'blue']
```
In the example above, we wanted to add different colours to each one of the class instances s1 and s2 but, since we are using a mutable class variable, colours are shared by all class instances. Correct design of the class should use an instance variable instead:

```python
class Shirt:

    def __init__(self, name):
        self.name = name
        self.colours = [] # creates a new empty list for each shirt
        
    def add_colour(self, colour):
        self.colours.append(colour)

>>> s1 = Shirt('shirt-091123')
>>> s2 = Shirt('shirt-1231sf')
>>> s1.add_colour('red')
>>> s2.add_colour('blue')
```
List *colours* in the example above, is initiated for each instance and therefore each colour will be added to the specific instance variable. You should use instance variables for data unique to each instance and class variables for data that are shared by all instances of a class.

## Environment Variables

Sensitive information or configuration options for different development environments should be set as environment variables. Environment variables consist of key/value pairs that can be set at a local scope using .env files. Some variable examples are presented below: 
* API keys
* Hosts, URLs
* Database credentials


You should __never hard-code this data in your code__. You should generally avoid using hard-coded variables (e.g., file names, full paths, etc.) or global variables that can be modified by any function during runtime. This may lead to unpredictable behavior, especially in multi-threaded environments. 

A useful package that can be used to set and retrieve such environment variables is python-dotenv (https://github.com/theskumar/python-dotenv).

## Data Validation

Data validation is very important, especially in web applications and applications that require client interaction (API requests) or user input. Validation schemas contain the rules for validating client or user input. You should define and group these schemas in a seperate file (e.g., models.py).

In addition, it would be better to use existing libraries for performing data validation. They provide validation functionality out of the box and you can easily reuse or extend the defined validation schemas. Some of the most popular libraries that can be used for this purpose:

* *Cerberus* (https://docs.python-cerberus.org/en/stable/index.html) - lightweight and extensible
* *marshmallow* (https://marshmallow.readthedocs.io/en/stable/) - can also be used for data serialization and deserialization
