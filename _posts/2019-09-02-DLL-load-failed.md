---
layout: post
title:  "from . import _mklinit \n ImportError: DLL load failed"
---

# How to solve ImportError: DLL load failed when using conda environment

## Environment: 
- OS info: Windows 10 Pro 64 bit Build 17763
- Conda environment was installed from within Visual Studio 2019

<details><summary>Steps I took to create conda env in VS2019 (included for the sake of reproducibility) </summary>

1. Launch Visual Studio 2019 Professional
2. Click "Continue without code" at the bottom right of the launch window
3. Click "Add Environment" in "Python Environments" panel
4. Click "Conda environment"
5. Name it as _conda-64_ instead of the default name _env_
6. Select radio button "One or more Anaconda package names" 
7. Enter _python numpy pandas scipy matplotlib sympy pytest_  into the text box below
8. Click "Create"

</details>


## IDE: Visual Studio Code with Python extension installed.

## Code:

```
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 20, 100)  # Create a list of evenly-spaced numbers over the range
plt.plot(x, np.sin(x))       # Plot the sine of each x point
plt.show()                   # Display the plot
```

Error message:

```
Traceback (most recent call last):
  File "c:\Users\me\.vscode\extensions\ms-python.python-2019.8.30787\pythonFiles\ptvsd_launcher.py", line 43, in <module>
    main(ptvsdArgs)
  File "c:\Users\me\.vscode\extensions\ms-python.python-2019.8.30787\pythonFiles\lib\python\ptvsd\__main__.py", line 432, in main
    run()
  File "c:\Users\me\.vscode\extensions\ms-python.python-2019.8.30787\pythonFiles\lib\python\ptvsd\__main__.py", line 316, in run_file
    runpy.run_path(target, run_name='__main__')
  File "C:\Users\me\.conda\envs\conda-64\lib\runpy.py", line 263, in run_path
    pkg_name=pkg_name, script_name=fname)
  File "C:\Users\me\.conda\envs\conda-64\lib\runpy.py", line 96, in _run_module_code
    mod_name, mod_spec, pkg_name, script_name)
  File "C:\Users\me\.conda\envs\conda-64\lib\runpy.py", line 85, in _run_code
    exec(code, run_globals)
  File "d:\ppark\source\hello\standardplot.py", line 1, in <module>
    import matplotlib.pyplot as plt
  File "C:\Users\me\.conda\envs\conda-64\lib\site-packages\matplotlib\__init__.py", line 138, in <module>
    from . import cbook, rcsetup
  File "C:\Users\me\.conda\envs\conda-64\lib\site-packages\matplotlib\cbook\__init__.py",
line 31, in <module>
    import numpy as np
  File "C:\Users\me\.conda\envs\conda-64\lib\site-packages\numpy\__init__.py", line 140, in <module>
    from . import _distributor_init
  File "C:\Users\me\.conda\envs\conda-64\lib\site-packages\numpy\_distributor_init.py", line 34, in <module>
    from . import _mklinit
ImportError: DLL load failed: The specified module could not be found.
```

## How I tackled the problem

- Context: I wanted to share the environment with vscode (visual studio code) in order to save the disk space. 
- Situation: Although vscode recognized the conda environment, it was not able to import matplotlib and numpy. 
- Observation: It was a PATH issue, and the solution was to add to PATH the following:
_c:\Users\me\\.conda\envs\conda-64\Library\bin_
The exact path may vary, but it would be something like this: _your\conda\path\\..\Library\bin_.

And now it works. Hope it helps anyone who might be struggling with the import problem. 