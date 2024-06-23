

project creation in Django
--------------------------

    >   $ mkdir <PROJ_NAME> && cd <PROJ_NAME>
    >   $ python3 -m venv venv

if it doesn't work:

    sudo apt-get update
    sudo apt-get upgrade
    sudo apt install ppython3 pip
    sudo apt install python3-venv

project activation
------------------

    >   $ source venv/bin/activate                               #   source env/Scripts/activate [ for Windows ]

    >   (env) $ pip install django                              #   (env) $ python.exe -m pip install --upgrade pip [ if requested ]
    >   (env) $ pip install djangorestframework
    >   (env) $ django-admin startproject <PROJ_NAME> .
    >   (env) $ django-admin startapp <APP_NAME>

    >   (env) $ python3 manage.py migrate

    >   (env) $ python3 manage.py createsuperuser --username <USERNAME> --email <EMAIL_ADDRESS>

    >   (env) $ python3 manage.py runserver
