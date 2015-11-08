Developing
==========

Tabs on Tallahassee (ToT) is a Django application powered by the `Open Civic Data <https://opencivicdata.org>`_ specification.

Development requires:
    * Python 3.4 or 3.5 (w/ virtualenv/pip)
    * PostgreSQL 9.4 w/ PostGIS
    * git
    * a relatively recent version of poppler utils for ``pdftotext``
        * on OSX: ``brew install poppler``
        * on Ubuntu: ``apt-get install poppler-utils``

Getting Started
---------------

1) Create a new virtualenv::

    $ pyvenv tot -p `which python3`

2) Within this virtualenv install the requirements::

    (tot)$ pip install -r requirements.txt

3) Create a Postgres DB (default name is "opencivicdata" w/ a user named "pupa" w/ password "pupa", this is fine for development but be sure to change these settings for deployment.

4) Initialize the database::

    (tot)$ pupa dbinit us               # loads OCD / pupa setup for United States jurisdictions
    (tot)$ ./manage.py migrate          # run remainder of database migrations
    (tot)$ ./manage.py loadshapefiles   # load shapefiles from shapefiles/ directory
    (tot)$ ./manage.py loadmappings us  # create mappings from FL districts to shapefiles

5) At this point it should be possible to run the scraper::

    (tot)$ pupa update fl people bills session=2016

You can also run other sessions too::

    (tot)$ pupa update fl bills session=2015A

6) At this point you're good to go, you can run the Django dev server in the typical way::

    (tot)$ ./manage.py runserver

A Functional Database
---------------------

Setting up a full database w/ all of the data is time-consuming and in theory only needs to be done once.

A "clean" database has been created w/ the following steps::

    (tot)$ pupa dbinit us
    (tot)$ ./manage.py migrate
    (tot)$ ./manage.py loadshapefiles
    (tot)$ ./manage.py loadmappings us
    (tot)$ ./manage.py loaddata fixtures/*.json
    (tot)$ pupa update fl people
    (tot)$ pupa update fl bills session=2015
    (tot)$ pupa update fl bills session=2015A
    (tot)$ pupa update fl bills session=2015B
    (tot)$ pupa update fl bills session=2016

    # TODO: 204, 2015C, 2016

Directory Layout
----------------

The ToT source code consists of:

ansible/
    `Ansible <https://ansible.com>`_ deployment playbook
docs/
    The sphinx source for these docs.
fixtures/
    Django fixtures used to initialize an empty database.
shapefiles/
    Florida district shapefiles from Census.gov, current as of 2015.
static/
    Static assets (css, javascript)
templates/
    All Django templates for the website.
fl/
    A Pupa 0.5 compatible scraper for Florida's legislature.
api/
    Django application powering the API.
bills/
    Django application powering the bill list/detail views.
glossary/
    Django application powering the glossary functionality.
legislators/
    Django application powering the legislators list/detail views.
preferences/
    Django application for ToT user preferences.
tot/
    Project settings/wsgi app/etc.

Additional Notes
----------------

This project was developed against:

* opencivicdata-django 0.7.4
* opencivicdata-divisions-2015.4.21
* pupa 0.5.0
* represent-boundaries 0.7.4
* Django 1.9b1
* djangorestframework 3.2.4
* django-cors-headers 1.1.0
* whitenoise 2.0.4
* lxml 3.4.4
* Markdown 2.6.2
* rest_framework_json_api @ d22cc0a
* waterfall @ 974beb
* django-registration @ f1dfbd


Many of these libraries were bleeding edge at the time of writing and significant changes may have occurred.
Before upgrading any libraries be very careful to ensure that they don't introduce breaking changes.