# About
Contains Git-hook-based scripts to be registered as a global hooks - such approach may be useful for teams who work 
with a lot of repositories with similar rules to perform checks on commit.

The logic of solution is following:
1. Global hooks are registered once for the Git application
2. Each time user commits - Global Hooks are triggered:
   1. First of all online updates are checked for the Global Hooks
   2. If working repository contains "./qubership/global-pre-commit-config.yaml" file then "pre-commit" framework 
   will be started using this configuration.
   3. In case no errors happened on the previous step (or no configuration file is found) then local hook ".git/pre-commit" will be called if exists.

# How to install
## Prerequisites
### Git
Git to be installed from https://git-scm.com/install/
No Git global hook paths are setup yet, check "core.hooksPath" property value with
```shell
git config --global core.hooksPath
# or
git config --global --list
```

### Python
Python to be installed from https://www.python.org/downloads/, currently tested version is 3.14.2.
Solution is based on using [pre-commit framework](https://pre-commit.com/) which is python-based.

### Pre-commit
Pre-commit framework to be installed from using instructions from https://pre-commit.com/
```shell
pip install pre-commit
```

After installation check pre-commit version by
```shell
pre-commit --version
```
Currently tested with 4.5.1


## Install global hooks
Note, that downloaded repository will be registered in the Git global configuration, 
so pay attention it should be quite static folder, i.e. if moved/renamed - then configuration must be reset.


### Windows
Navigate to the folder where new subfolder will be created by git clone, then run following script
```shell
REM set name of the folder to download repository into
set FOLDER_NAME=git-global-hooks

REM do repository cloning
git clone https://github.com/exadmin/qubership-pre-commit-proto.git "%FOLDER_NAME%"

REM Setup global path to hooks
cd "%FOLDER_NAME%"
git config --global core.hooksPath "%cd%\hooks-global"
```

### Linux
Navigate to the folder where new subfolder will be created by git clone, then run following script
```shell
# set name of the folder to download repository into
FOLDER_NAME=git-global-hooks

# do repository cloning
git clone https://github.com/exadmin/qubership-pre-commit-proto.git "$FOLDER_NAME"

# Setup global path to hooks
cd "$FOLDER_NAME"

# Linux variant
git config --global core.hooksPath "$(pwd)/hooks-global"
```

Check that property is set correctly
```shell
git config --global core.hooksPath
```

Now, each time you are doing
```shell
git commit -m "Commit description"
```
a Global Hooks will be called with mentioned logic as described at the beginning of README.md file.



## Uninstall or disable
Just unset Git global property to hooks
```shell
git config --global --unset core.hooksPath
```