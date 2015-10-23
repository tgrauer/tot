Tabs on Tallahassee
===================

[![Build Status](https://travis-ci.org/jamesturk/tot.svg)](https://travis-ci.org/jamesturk/tot)

Getting Started
---------------

0) Before getting started it is necessary to have a few things installed:

    * Python 3.4+
    * PostgreSQL 9.4
    * git

1) Create a new virtualenv:
    $ pyvenv tot -p `which python3`

2) Install Python requirements within this virtualenv:

    (tot)$ pip install -r requirements.txt

3) Initialize the database:

    (tot)$ pupa dbinit us

4) Load Shapefiles & Mappings

    (tot)$ ./manage.py loadshapefiles
    (tot)$ ./manage.py loadmappings


Running the Scraper
-------------------

From within the tot virtualenv:

    $ pupa update fl people bills session=2016

Project Layout
--------------

    api
        django app for API
    bills
        django app for bill views
    fl
        pupa 0.5 compatible scraper for FL legislature
    glossary
        django app for legislative term glossary
    preferences
        django app for user preferences & API key application
    shapefiles
        Florida shapefiles
    templates
        HTML templates for website
    tot
        core django project