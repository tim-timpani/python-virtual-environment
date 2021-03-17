# Python Virtual Environment
Python virtual environments are used to keep a version of the python interpreter, installed
packages, and other binaries (such as pip) in a separate work environment.  This is
very useful when switching versions of python or avoiding conflicting packages/versions.
There are software packages available to help manage virtual environments,
such as Anaconda (or Conda).  Conda is now charging a subscription for commercial use and will 
block access from corporations unless a paid subscription is used.  These instructions show 
how to manage python virtual environments using the built-in features of Python with a little 
help from bash/zsh.


## Instructions for MacOS
Although MacOS comes with Python (as of Big Sur: both 2.7 and 3.7) which is used by the
OS.  It's best practice to use virtual environments rather than install packages or modify
 the interpreters used by the OS.

#### Choose A Folder
Each virtual environment, keeps symlinks and files in a directory structure.
It's a good idea to decide at the start where to put the virtual environment directories.
They can be stored anywhere on the filesystem. One option is to use a common directory. For
the purposes of these instructions, we will use a commmon directory called **envs** under the home
directory. Create the folder with the following command:
* mkdir ~/envs

#### Install Python
Install the desired version of Python by going to python.org. Download and install
one or more versions of python. The installer package will install each one into a
separate directory on the system to support multiple versions. At the time of this writing
they are installed into /Library/Frameworks/Python.framework/Versions/X.X  where X.X is the
version.  This path may be needed when creating a virtual environment through an IDE.

#### Install The Virtual Environment Package
This only needs to be done **once for each version of Python** that will be used in virtual
environments.  Use the command below, replacing X.X with the version installed above.
* sudo pipX.X install virtualenv

#### Create a Virtual Environment
Create a virtual environment by running **pythonX.X -m virtualenv _path-to-env_**
Here's an example using Python 3.9 and creating a virtual environment called
test_39
* python3.9 -m virtualenv ~/envs/test_39
    
### Activate a Virtual Environment
The active environment will dictate where pip installs packages and
which python interpreter and other binaries will run. By default, the shell prompt will have the
name of the currently active environment in parentheses.  Activate the environment by sourcing
the respective activate file into the current shell replacing _name_ with the name of the desired
environment: 
* source ~/envs/_name_/bin/activate

### Default Virtual Environement
Place the source command for the desired environment in ~/.zshrc for zsh or ~/.bashrc for bash.
Older MacOS (and those user accounts upgraded from older OS) will have your user set to bash. 
Newer accounts default to zsh.  Check your user settings if you are unsure.

### Deactivate Virtual Environment
To revert back to the sysetem default python, enter the command: **deactiavate**

### Deleting Virtual Environment
Simply delete the directory with the name of the virtual environment
you wish to delete. It's advised to use Finder to delete the folder rather than
shell commands. This will help reduce undesired results if a command is typed in wrong.

### Command Shortcut For Activating Virtual Environements
The source command (above) used to activate a virtual environment is a bit cumbersome.  One way
to improve this, is to place a function in the shell rc file that will
list and change the environment. Place the below lines in ~/.zshrc (or ~/.bashrc if using bash).
Restart the terminal session or source the rc file for it to take affect. Enter **e** to list the
environment names and **e _name_** to activate it (replacing **_name_** with the environement name).
```
e() {
  if [ -z "$1" ]
  then
    ls -1 ~/envs
  else
    source ~/envs/$1/bin/activate
  fi
}
```
