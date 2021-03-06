[![Build Status](https://travis-ci.org/autoconstruccion/autoconstruccion.svg?branch=master)](https://travis-ci.org/autoconstruccion/autoconstruccion)

# Autoconstruccion

Autoconstruccion project at H4ckademy

by Creepy Coconuts

## Requirements:

* Python 3.4
* See requirements.txt & requirements-dev.txt



KWOWN ISSUES

* On Gnu/Debian jessie it's need to do a workarround to install the virtual environment,
    because pip it's not included with python3 package.

    Further information at
    http://askubuntu.com/questions/488529/pyvenv-3-4-error-returned-non-zero-exit-status-1

    python3 -m venv --without-pip ./venv
    source ven/bin/activate
    curl https://bootstrap.pypa.io/get-pip.py | python
    pip3.5 install -r requirements.txt
    deactivate



##HOW TO RUN

    First activate your virtual environment or create it init-dev-end.sh and then launch the server

    source ./venv/bin/activate
    python server_app/run.py

    By default the server is running at localhost on port 5000
    http://127.0.0.1:5000

## REQUIREMENTS

    Python3.4 its required, all installation is done at virtual environment venv
    Postgresql required

## HOWTO CONTRIBUTE

    Use your github account to fork this proyect
    https://github.com/autoconstruccion/autoconstruccion#fork-destination-box

    Once you have a fork download it into your box
    ```
# download your code using git 
    git clone https://github.com/<youruser>/autoconsturccion src
# add upstream aka oficial repo 
    cd src
    git remote add upstream http://github.com/autoconstruccion/autoconstruccion
# update your code with the upstream
    git pull upstream master
    ```
    when you want to do contributing do it using a new branch
    ```
    git checkout -b fix_this_feature
    git add .
    git commit -m"this fix that"
    ...
# upload your branch to your github repo
    git push origin fix_this_feature
    ```
    and then use the github panel to do a pull request.
    Use you branch to do the pull request against autoconstruccion master branch

    we'll reicibe your pull request and will be reviewed for adding to the main code



## CONFIGURE NOTIFIER
    Notifier is the layer that provides a way to comunicate with the users, could be a mail service, or a instant messenger service like telegram, jabber, etc...
    At this moment only mailgun service it's implemented. 

    In order to configure mailgun service, firstly you need a Mailgun account. Register your account here: https://mailgun.com/signup

    Once you have your new account you need to configure the notifier transport.
    Edit the `instance/config.py` file and add or edit this config:


```
NOTIFIER_MAILGUN = {
    "transport": "Mailgun",
    "api-key": "key-XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
    "host": "https://api.mailgun.net/v3/sandboxceXXXXXXXXXXXXXXX.mailgun.org/messages",
    "from": "from@email.com" 
}

NOTIFIER_DEFAULT = 'NOTIFIER_MAILGUN'

```

Stop and start the application in order to reload notifier configuration, it's readed only at startup process.

## HOWTO DATABASE MIGRATION
    Firstly define your new data structe at models.py, alembic will check this file

    then sure your database it's to date
    ```
    alembic upgrade head
    ``` 
    and then add a new revision with a descriptive message
    ```
    alembic revision -m "descriptive message" --autogenerate
    ```
