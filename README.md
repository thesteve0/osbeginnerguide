About
=====

A Django 1.4.5 example project for deployment on "Do It Yourself" application type of http://openshift.redhat.com

Example deployment: http://petstore-zemanel.rhcloud.com

Setting up Openshift
--------------------

Create the Openshift application

    $ rhc app create djangoexample diy-0.1

Add Postgres cartridge

    $ rhc cartridge add postgresql-8.4 --app djangoexample

Merge this example source with the Openshift repo barebones source code

    $ git remote add djangoexample -m master https://github.com/zemanel/openshift-diy-django-example.git

    $ git pull -s recursive -X theirs djangoexample master

Deploy app to openshift

    $ git push origin

Pre deploy stage
----------------

On every deployment, the 'deploy' hook script performs the following actions:

* [re-]creates a python virtual environment on $OPENSHIFT_DATA_DIR/venv and activates it
* installs a pip requirements file named 'requirements.txt' which is located on the root of the repo.
The virtualenv is versioned based on the requirements.txt MD5, to speed up deployments
* runs the 'syncdb', 'migrate' and 'collectstatic' django commands
* Pip downloads are cached on the '${OPENSHIFT_TMP_DIR}.pip/cache' folder
* the 'start' hook script runs gunicorn as a daemon, binded on $OPENSHIFT_INTERNAL_IP:$OPENSHIFT_INTERNAL_PORT,
with a pid file written to '${OPENSHIFT_DATA_DIR}gunicorn.pid', which is then used by the 'stop' hook to terminate the gunicorn process
* there are separated stdout and access logs, outputted to $OPENSHIFT_LOG_DIR  
    

Developing locally
------------------

A *settings_localdev.py* module has *out of the box* defaults for using local folders and an Sqlite database.

It can easily be used this way:

    $ export DJANGO_SETTINGS_MODULE=settings_localdev

    $ dj syncdb

    $ dj migrate

The *settings_localdev.py* module approach can be duplicated into another module not checked into source control and
further customized, for example.



<<<<<<< HEAD
=======
An impatient beginner's guide to OpenShift. Based off the workshops the evanglists usually give. 
It assumes you know how to program in your language but may not know GIT or SSH or server configuration.

To see how all the pages are put together please look at index.txt
These docs are written in ASCIIDOC.

The documents in this repository are licensed Creative Commons 0 (CC0).
>>>>>>> 504873f382ec4685cb584b3e8cf5aa37045cf3c3
