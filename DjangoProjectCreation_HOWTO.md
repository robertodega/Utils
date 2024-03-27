
--------------------------
project creation in Django
--------------------------

$ mkdir <PROJ_NAME> && cd <PROJ_NAME>
$ python3 -m venv venv

    -   if it doesn't work:
        -   sudo apt-get update
        -   sudo apt-get upgrade
        -   sudo apt install ppython3 pip
        -   sudo apt install python3-venv

$ source venv/bin/activate                               #   source env/Scripts/activate [ for Windows ]

(venv) $ pip install django                              #   (venv) $ python.exe -m pip install --upgrade pip [ if requested ]
(venv) $ pip install djangorestframework
(venv) $ django-admin startproject <PROJ_NAME> .

(venv) $ django-admin startapp <APP_NAME>

(venv) $ python3 manage.py migrate

(venv) $ python3 manage.py createsuperuser --username <USERNAME> --email <EMAIL_ADDRESS>

(venv) $ python3 manage.py runserver
