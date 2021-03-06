privacyIDEA
===========

[![Build Status](https://travis-ci.org/privacyidea/privacyidea.svg?branch=master)](https://travis-ci.org/privacyidea/privacyidea)
[![CircleCI](https://circleci.com/gh/privacyidea/privacyidea/tree/master.svg?style=shield&circle-token=:circle-token)](https://circleci.com/gh/privacyidea/privacyidea)
[![Coverage Status](https://img.shields.io/coveralls/privacyidea/privacyidea.svg)](https://coveralls.io/r/privacyidea/privacyidea)
[![Downloads](https://img.shields.io/pypi/dm/privacyidea.svg)](https://pypi.python.org/pypi/privacyidea/)
[![Latest Version](https://img.shields.io/pypi/v/privacyidea.svg)](https://pypi.python.org/pypi/privacyidea/)
[![License](https://img.shields.io/github/license/privacyidea/privacyidea.svg)](https://pypi.python.org/pypi/privacyidea/)
[![Documentation Status](https://readthedocs.org/projects/privacyidea/badge/?version=latest)](http://privacyidea.readthedocs.org/en/latest/)
[![Code Climate](https://codeclimate.com/github/privacyidea/privacyidea/badges/gpa.svg)](https://codeclimate.com/github/privacyidea/privacyidea)

privacyIDEA is an open solution for strong two-factor authentication like 
OTP tokens, SMS, Smartphones or SSH keys.
Using privacyIDEA you can enhance your existing applications like local login 
(PAM, Windows Credential Provider), 
VPN, remote access, SSH connections, access to web sites or web portals with 
a second factor during authentication. Thus boosting the security of your 
existing applications.

privacyIDEA does not bind you to any decision of the authentication
protocol or it does not dictate you where your user information should be
stored. This is achieved by its totally modular architecture.
privacyIDEA is not only open as far as its modular architecture is
concerned. But privacyIDEA is completely licensed under the AGPLv3.

It supports a wide variety of authentication devices like OTP tokens 
(HMAC, HOTP, TOTP, OCRA, mOTP), Yubikey (HOTP, TOTP, AES), Smartphone
Apps like Google Authenticator, SMS, Email, SSH keys, x509 certificates.

Since version 2 privacyIDEA is based on flask and sqlalchemy as the python backend. The
web UI is based on angularJS and bootstrap.
A MachineToken design lets you assign tokens to machnies. Thus you can use
your Yubikey to unlock LUKS, assign SSH keys to SSH servers or use Offline OTP with PAM.

With version 2 the code was cleaned up and it was emphasized to keep a good
code coverage. The design separates the database layer from the library layer
and from the REST API layer. Thus allowing easy unit testing in each layer.

You are also welcome to take a look at the hopefully tidy code and contribute.

I try to keep up a good test coverage. So run tests!

Setup
=====

You can setup the system in a virtual environment:
    
    git checkout https://github.com/privacyidea/privacyidea.git
    cd privacyidea
    virtualenv venv
    source venv/bin/activate
    pip install -r requirements.txt

Read the install instructions at http://privacyidea.readthedocs.org.

Running it
==========

Create the database:

    ./pi-manage.py createdb

Create the first administrator:

    ./pi-manage.py admin add <username> <email>

Run it:

    ./pi-manage.py runserver

Now you can connect to http://localhost:5000 with your browser and login as administrator.

Run in virtualenv
=================

For running the server in a virtual env see documentation at
http://privacyidea.readthedocs.org/en/latest/installation/index.html#python-package-index.

Run tests
=========

    nosetests -v --with-coverage --cover-package=privacyidea --cover-html

Code structure
==============

The database models are defined in ``models.py`` and tested in tests/test_db_model.py.

Based on the database models there are the libraries ``lib/config.py`` which is
responsible for basic configuration in the database table ``config``.
And the library ``lib/resolver.py`` which provides functions for the database
table ``resolver``. This is tested in tests/test_lib_resolver.py.

Based on the resolver there is the library ``lib/realm.py`` which provides functions
for the database table ``realm``. Several resolvers are combined into a realm.

Based on the realm there is the library ``lib/user.py`` which provides functions 
for users. There is no database table user, since users are dynamically read from
the user sources like SQL, LDAP, SCIM or flat files.

Upgrading
=========
In certain cases the database structure has changed (1.5->2.0).
Read http://privacyidea.readthedocs.org/en/latest/installation/upgrade.html 
for upgrade instructions.
