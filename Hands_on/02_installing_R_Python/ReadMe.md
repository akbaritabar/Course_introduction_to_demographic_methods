# Required software for Hands-on sessions using R and/or Python
For the hands-on part of the following weeks, we will use R and Python. 

It is necessary to have these two software installed and check if they are functioning e.g., by importing a package or checking their installed versions.

In Python, we will use [virtual environments](https://realpython.com/python-virtual-environments-a-primer/) to isolate our projects and their required packages. This helps with reproducibility practices and making sure your code could be taken by someone else to re-run on their machine to recreate the results you have shown.

In R, if you are familiar with [Renv](https://rstudio.github.io/renv/index.html), feel free to use it to isolate your projects and R package requirements. The concepts are the same, but there are small differences in the details and syntax. If you do not use Renv, I recommend having a `requirements.txt` file where you keep track of R packages that are installed for your current project.

# Install R and RStudio

The IT should already have installed R and RStudio on the lab computers.

If you are using R on Ubuntu Linux, I recommend using [R2U](https://github.com/eddelbuettel/r2u) to enable installing packages from binary instead of source that takes much less time.

To install it on your own, please follow these links:
- **For Windows**: [https://cran.r-project.org/bin/windows/base/](https://cran.r-project.org/bin/windows/base/)
- **For Mac**: [https://cran.r-project.org/bin/macosx/](https://cran.r-project.org/bin/macosx/)
- **For Linux**: [https://cran.r-project.org/](https://cran.r-project.org/) Click on the button for Linux, then select your distribution, i.e., "Ubuntu" and follow the steps outlined to add it to Linux sources list and install using `sudo apt-get`

And once you installed R, visit this link to download and install RStudio: [https://posit.co/download/rstudio-desktop/](https://posit.co/download/rstudio-desktop/) or Poistron [https://positron.posit.co/](https://positron.posit.co/)

# UV for Python installation, project management and virtual environments
## Steps to create a project using UV
0. install uv, see `https://docs.astral.sh/uv/getting-started/installation/`
1. to create a project folder and use a specific version of Python `uv init projectName --python 3.13`
2. then go to project `cd projectName`
3. to add all packages listed in requirements `uv add -r requirements.txt`
4. now, to run code using `snakemake` use `uvx` (or `uv tool run`) as in `uvx snakemake --version`
5. or to use VS Code that already inherits the environment created by uv do `code .`
6. or for Jupyter lab do `uv run --with jupyter jupyter lab`
7. to see requirements and project's dependencies `uv tree` and to record all those that are installed so far with `requirements.txt` or by `uv add packageName` (and removed by `uv remove packageName`) `uv sync`
8. A good practice then is to create a folder with project name to keep code, data, etc there i.e., `mkdir projectName`


# ALTERNATIVE 1: using Pyenv for Linux and Mac: Use Pyenv with vanilla, or conda, miniforge, etc Python versions on Linux or Mac "without" affecting the system installation of python
1. This is a good introduction: https://realpython.com/intro-to-pyenv/
2. Follow installation steps from this link (available for Mac and Linux, for Windows refer to a different repository, discussed in next section): https://github.com/pyenv/pyenv
3. After the step on adding it to .bashrc, .bash_profile, and .profile, if you had an issue with bash not seeing it right i.e., if `pyenv --version` was giving an error like `/usr/bin/env: ‘bash\r’: No such file or directory`. You have to remove pyenv (go to the folder where it is installed i.e., `~/.pyenv` or something similar, and delete that folder), then edit `git` configuration and set this from true to false i.e., `git config --global core.autocrlf false` and then reinstall pyenv and add it to bash as outlined above
4. Next, confirm that installation was successful with `pyenv --version`. Here are a list of pyenv commands: https://github.com/pyenv/pyenv/blob/master/COMMANDS.md
5. After the installation, it is now possible to write `pyenv install --list` to see which Python distributions are available to install e.g., it can also install miniforge and conda ones, similar to vanilla Python using `pyenv install PYTHON-VERSION-NUMBER` (or conda/miniforge name from the list). I suggest installing the latest Python 3 vanilla version i.e., "3.13" and later 
   - **Note**: please check if the libraries you are going to install support the Python version, I would recommend not to install the latest version, since some libraries will not be up-to-date enough to work with it.
6. Next, change the **local** python from the system one to the one installed with pyenv to prevent messing up the system one i.e., activate it with `pyenv local PYTHON-VERSION-NUMBER` and check it with `pyenv versions` (star shows the Python in use)
7. **NOTE**: do NOT use `pyenv global` for instance on Ubuntu as some apps rely on system's installation of python and this changes the python in use by the system and causes those apps to fail working. Instead, open a project folder and set the pyenv local only for that project and then do 'pyenv activate' as below
8. It also installs a plugin called `pyenv-virtualenv` (https://github.com/pyenv/pyenv-virtualenv) which works to create virtual environments.
9. To start a new project and its own virtual environment, I would recommend creating a folder for this project, then `cd project-folder` and inside the folder, doing `pyenv virtualenv env`. This will create a subfolder inside the project folder, which is called `env` and include all environment related files there. Once you are sharing your project with someone, you can skip sharing this folder as the person receiving the requirements file can recreate the environment on their own.
10. Activate it with `pyenv activate env`
11. Seeing `python -m pip --version` or `python --version` should confirm and `python -m pip list` will give only pip in this folder/project
12. Install packages with pip i.e., `python -m pip install -r requirements.txt` and at the end `pyenv deactivate` to exit this environment.

# Pyenv for Windows
0. This is a good introduction to Pyenv: https://realpython.com/intro-to-pyenv/
1. Open `Powershell` in Windows (by opening the start menu and typing Powershell) and then put these and enter which asks Powershell to run scripts "only" for your user: `Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`
2. Close and reopen Powershell. Follow the steps in this link for installation: https://github.com/pyenv-win/pyenv-win (which asks you to run one command to download and install it)
3. Next, confirm that installation was successful with `pyenv --version`. Running `pyenv commands` lists available commands and what they do.
4. After the installation, it is now possible to write `pyenv install --list` to see which Python distributions are available to install e.g., it can also install miniforge and conda ones, similar to vanilla Python using `pyenv install PYTHON-VERSION-NUMBER` (or conda/miniforge name from the list). I suggest installing the latest Python 3 vanilla version i.e., "3.13" and later.
   - **Note**: please check if the libraries you are going to install support the Python version, I would recommend not to install the latest version, since some libraries will not be up-to-date enough to work with it.
5. Next, change the **local** python from the system one to the one installed with pyenv to prevent messing up the system one i.e., activate it with `pyenv local PYTHON-VERSION-NUMBER` and check it with `pyenv versions` (star shows the Python in use)
6. Afterwards, `pyenv local PY-VERSION` allows setting it locally in a project folder which could be checked with `pyenv versions` and also `pyenv which python` or `pyenv which pip` and `python -m pip list`
7. You can then use `pip install virtualenv` for `virtualenv` to create virtual environments. A safer way would be to use `python -m virtualenv` (which asks the Python in use, as you set it above by Pyenv, to run the module virtualenv)
8. Check its correct installation with `python -m virtualenv --version` (which also prints where it is installed which should be under your newly installed vanilla Python)
9. Now `python -m pip list` should only show python, pip, and virtualenv, and a few things that are their requirements
10. To start a new project and its own virtual environment, I would recommend creating a folder for this project, then `cd project-folder` and inside the folder, doing `python -m virtualenv env`. This will create a subfolder inside the project folder, which is called `env` and include all environment related files there. Once you are sharing your project with someone, you can skip sharing this folder as the person receiving the requirements file can recreate the environment on their own.
11. After environment is created, if you are using Windows Command Prompt do  `.\env\Scripts\activate.bat` which activates the environment. Instead, if you are using Windows Powershell terminal, you can do `.\env\Scripts\activate.ps1` (Thanks to Sina for this hint). Now, if you do `python -m pip list` it should only list pip itself as the installed package and nothing else. This in addition to the name of virtual environment printed in parenthesis at the start of command line i.e., "(env)" means you have successfully created the environment and activated it.
12. Then copy the "requirements.txt" file into this project folder and do `python -m pip install -r requirements.txt` to use this environment and install the required packages.
13. **Please note**: On Windows, it can often happen that creating a new virtual environment in a subfolder lead to "file path name too long" error. The reason is your folder path should not exceed 256 characters (including spaces) and the solution is to create your project in another folder with shorter folder name(s).

## Uninstalling pyenv from Windows
0. See this link for guidelines: [https://github.com/pyenv-win/pyenv-win/issues/597](https://github.com/pyenv-win/pyenv-win/issues/597)
1. Open Windows Powershell in a directory that is not Pyenv installation directory and run `Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/pyenv-win/pyenv-win/master/pyenv-win/install-pyenv-win.ps1" -OutFile "./install-pyenv-win.ps1"; &"./install-pyenv-win.ps1" -UNINSTALL`

# ALTERNATIVE 2: another (less preferred) option is to install and use the Miniforge or the Anaconda distribution of Python
- I prioritize this lower as this distribution is larger in size to download and install. But it comes with `conda` package and environment manager which is very helpful for the beginner level.
- Here is a step by step guide from a previous course of mine: [https://github.com/akbaritabar/BiblioDemography_IMPRS_PHDS_2022_IDEM187/blob/main/0_code/01_Required_installation_setup_python.md](https://github.com/akbaritabar/BiblioDemography_IMPRS_PHDS_2022_IDEM187/blob/main/0_code/01_Required_installation_setup_python.md)

# List current environment's requirements
1. Activate the environment by following steps outlined above or "cd project-env-name" and `source ./bin/activate` or for Windows `.\Scripts\activate.bat`
2. Run `python -m pip freeze --local > requirements.txt` which will export all installed requirements in this environment and their exact versions into a requirements text file
3. Deactivate this environment with "deactivate"
4. Go back to the folder where you want to create a replication folder for this project and test reproducibility and follow steps above with `python -m virtualenv project-env-name` but use a different name for replication environment

# If you messed up the virtual environment
- Most importantly **Stay calm!** 
    - The goal of installing a light-weight vanilla Python and using virtual environments was to keep things clean and isolated from each other or the system not to cause any problems.
- Create a new environment following steps outlined above and install the required packages.


# Where to learn basics of R and Python?
## To start with Python

Check this website first:

[https://www.w3schools.com/python/python_intro.asp](https://www.w3schools.com/python/python_intro.asp)


Check this repository by Vincent Traag and others, for an introductory course and code:

[https://github.com/vtraag/intro-python](https://github.com/vtraag/intro-python)


Or this one by Data Carpentry:

[https://datacarpentry.org/python-ecology-lesson/](https://datacarpentry.org/python-ecology-lesson/)

## To start with R
Check this website first:

[https://www.w3schools.com/r/default.asp](https://www.w3schools.com/r/default.asp)
      

This "very short introduction to R" is a good start: 

[https://cran.r-project.org/doc/contrib/Torfs+Brauer-Short-R-Intro.pdf](https://cran.r-project.org/doc/contrib/Torfs+Brauer-Short-R-Intro.pdf)


Or this course by Data Carpentry:

[https://datacarpentry.org/R-genomics/index.html](https://datacarpentry.org/R-genomics/index.html)
