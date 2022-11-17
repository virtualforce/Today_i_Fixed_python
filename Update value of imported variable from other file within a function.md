# Problem
Usually variables and functions from other files are imported at the top and during deployment of that project, these imports happen only at the start.
How to get their latest/original value after we modify them in current file as it doesn't refresh despite revoking multiple times.

# Environment
* IDE Version : pyCharm Community Edition 2022.2.3
* Python Version: 3.8
* Flask Version: 2.2.2

# How you fix it

In order to get updated/refresh values of imported variables or functions in current function/file, we need to revoke/reload their values again irrespective where we imported them i.e. either within current function or on top of file. 

# Solution
### File where the variable exist variable.py
```
some_variable = {'name': 'Danish', 'city': 'Lahore'}
```

### File where variable is imported/required app.py

Import the some_variable from variable.py file at the top with reload function
```
from variable import some_variable  
from importlib import reload 
```

To refresh the value of some_variable within a function and use it for required purpose.
```
def some_function():
    reload(some_variable)
    random_dict = {}
    random_dict.update(somevariable)
    ...
```
