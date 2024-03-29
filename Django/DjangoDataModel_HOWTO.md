__________________________________________________________________________________________________________

 The un-normalized data is provided as both a spreadsheet and a CSV file:

        PROJECTS/Django/EXERCISES/dataModelBuilder/whc-sites-2018-clean.csv

 The columns in the data are as follows:

        name,description,justification,year,longitude,latitude,area_hectares,category,state,region,iso

__________________________________________________________________________________________________________

$ mkdir dataModelBuilder && cd dataModelBuilder

                                                -------------------
                                                Virtual Environment
                                                -------------------

$ python3 -m venv env
source env/Scripts/activate
(env) $ pip install django

                                                ---------------
                                                Getting Started
                                                ---------------

(env) django-admin startproject batch
(env) cd batch
(env) django-admin startapp unesco
(env) cd unesco
(env) wget https://www.dj4e.com/assn/dj4e_load/whc-sites-2018-clean.csv [ if wget installed ]
(env) mkdir scripts
(env) touch scripts/__init__.py
(env) nano scripts/many_load.py

-   Copy content from https://github.com/csev/dj4e-samples/tree/main/scripts/many_load.py

(env) cd ~/PROJECTS/Django/TESTS/dataModelBuilder/batch
(env) pip install django_extensions

(env) python3 manage.py check

-   in batch/batch/settings.py add to INSTALLED_APPS

        'django_extensions',
        'unesco.apps.UnescoConfig',

(env) python3 manage.py check

                                                -------------------
                                                Design a Data Model
                                                -------------------

 batch/unesco/models.py:

------------------------------------------------------------------------------------------
from django.db import models

class Category(models.Model):
    name = models.CharField(max_length=128, default="")
    def __str__(self) :
        return self.name

class State(models.Model):
    name = models.CharField(max_length=128, default="")
    def __str__(self) :
        return self.name

class Iso(models.Model):
    name = models.CharField(max_length=128, default="")
    def __str__(self) :
        return self.name

class Region(models.Model):
    name = models.CharField(max_length=128, default="")
    def __str__(self) :
        return self.name

class Site(models.Model):
    name = models.CharField(max_length=300)
    year = models.IntegerField(null=True)
    latitude = models.FloatField(null=True)
    longitude = models.FloatField(null=True)
    description = models.TextField(null=True)
    justification = models.TextField(null=True)
    area_hectares = models.FloatField(null=True)
    category = models.ForeignKey("Category", on_delete=models.CASCADE, null=True)
    region = models.ForeignKey("Region", on_delete=models.CASCADE, null=True)
    iso = models.ForeignKey("Iso", on_delete=models.CASCADE, null=True)
    state = models.ForeignKey("State", on_delete=models.CASCADE, null=True)

    def __str__(self) :
        return self.name

------------------------------------------------------------------------------------------

(env) python3 manage.py makemigrations
(env) python3 manage.py migrate

-   in dataModelBuilder/batch/unesco/scripts/many_load.py do changes:

------------------------------------------------------------------------------
#   from many.models import Person, Course, Membership
from unesco.models import Category, State, Iso, Region, Site

#   fhand = open('many/load.csv')
fhand = open('unesco/whc-sites-2018-clean.csv')

#   Person.objects.all().delete()
#   Course.objects.all().delete()
#   Membership.objects.all().delete()
Category.objects.all().delete()

------------------------------------------------------------------------------

    -   Create the "lookup" entries in each table (Category, Iso, State, and Region) [ indexes read from CSV file positions ] 

------------------------------------------------------------------------------

#   p, created = Person.objects.get_or_create(email=row[0])
#   c, created = Course.objects.get_or_create(title=row[2])
cat, created = Category.objects.get_or_create(name=row[7])
iso, created = Iso.objects.get_or_create(name=row[10])
state, created = State.objects.get_or_create(name=row[8])
region, created = Region.objects.get_or_create(name=row[9])

------------------------------------------------------------------------------

    -   In current CSV file, somwtimes the year column will be empty. 
    -   Do a try / except for each of the numeric fields that might be missing or have invalid data.
    -   Create the Site object from the lookup objects, cleaned up column data and the string data that goes into the Site table.

------------------------------------------------------------------------------

#   r = Membership.LEARNER
#   if row[1] == 'I':
#       r = Membership.INSTRUCTOR
#   m = Membership(role=r, person=p, course=c)
#   m.save()
try:
    y = int(row[3])
except:
    y = None

try:
    long = float(row[4])
except:
    long = None

try:
    lat = float(row[5])
except:
    lat = None

try:
    aect = float(row[6])
except:
    aect = None

site = Site(name=row[0], description=row[1], justification=row[2], year=y, longitude=long, latitude=lat, area_hectares=aect, category=cat, state=state, region=region, iso=iso)
site.save()

------------------------------------------------------------------------------

                                                ------------------
                                                Running the Script
                                                ------------------

(env) cd ~/PROJECTS/Django/TESTS/dataModelBuilder/batch
(env) python3 manage.py runscript many_load

