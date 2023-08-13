## Deploy a production ready Flask app on Render for free

Guide on how to deploy your Python code with Flask using Render cloud hosting

## Setup your local Python project and environment

```shell
curl https://pyenv.run | bash
```

## Add to ~/.bashrc for Ubuntu 22.04

```shell
WARNING: seems you still have not added 'pyenv' to the load path.

# Load pyenv automatically by appending
# the following to 
~/.bash_profile if it exists, otherwise ~/.profile (for login shells)
and ~/.bashrc (for interactive shells) :

export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"

# Restart your shell for the changes to take effect.

# Load pyenv-virtualenv automatically by adding
# the following to ~/.bashrc:

eval "$(pyenv virtualenv-init -)"
```

## Install specific Python version

```shell
pyenv install 3.10.12
```

## Configure and create a (very) simple Flask app

```shell
pyenv local 3.10.12
```

## Create the virtual environment for our packages 

This can be called anything but to keep things simple I just name it .venv for all my projects. (It can’t conflict with
anything as this environment is locally-scoped to the project):

```shell
python -m venv .venv
```

Activate the environment:

```shell
source .venv/bin/activate
```

With our local virtual environment created and activated we can now install some packages. Let’s start with Flask and
python-dotenv, which we can install in one command:

```shell
pip install --upgrade pip
pip install Flask python-dotenv
```

## Deploy your Flask app to Render

```shell

```
