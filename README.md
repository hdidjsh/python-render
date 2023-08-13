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

We also need to create a requirements.txt file so that Render will know what packages to install or if we want to share
our project with other people in the future.

Test Flask app on local:

```shell
$ flask run
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

Important: To save time having to stop and start the server every time you want to make a change to your backend code,
we can add this one line environment variable to a .env file:

```shell
# .env
FLASK_DEBUG=True
```

## Deploy your Flask app to Render

```shell
pip freeze > requirements.txt
```

Go to [Create a new Web Service](https://dashboard.render.com/select-repo?type=web) and connect your GitHub repo.

Make sure the Build Command is:

```shell
pip install -r requirements.txt
```

And the Start Command is:

```shell
gunicorn app:app
```

Lastly click on the “Advanced” button and add three environment variables:

```shell
PYTHON_VERSION = 3.10.12
PROD_APP_SETTINGS = config.ProductionConfig
```

The PYTHON_VERSION variable tells Render to use Python version 3.10.12 — exactly the same version we specified at the
very beginning of our project with pyenv.

The second PROD_APP_SETTINGS variable instructs Render to use the Flask production config options we set in our
config.py file.

With our web service configuration done, now all we have left to do is click “Create Web Service” and watch the project
get deployed

This will take a bit of time since we are on the free plan. At the end of the process if everything went smoothly we
should see the output saying "Build successful" and "Starting service with gunicorn app: app".

From here we can click on the link Render has provided for us and see our “Hello World!” message live on the Internet.