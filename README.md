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
Git is installed from https://git-scm.com/install/
No Git global hook paths are setup yet, check "core.hooksPath" property value with
```shell
git config --global core.hooksPath
# or
git config --global --list
```

## Install global hooks
Note, that downloaded repository will be registered in the Git global configuration, 
so pay attention it should be quite static folder, i.e. if moved/renamed - then configuration must be reset.

```shell
# set name of the folder to download repository into
FOLDER_NAME=git-global-hooks

# do repository cloning
git clone https://github.com/exadmin/qubership-pre-commit-proto.git "$FOLDER_NAME"

# Setup global path to hooks
cd "$FOLDER_NAME"
git config --global core.hooksPath "$(pwd)/hooks-global"
```

## Uninstall
Just unset Git global property to hooks
```shell
git config --global --unset core.hooksPath
```