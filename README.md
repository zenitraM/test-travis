# Travis issue with postgresql 9.4 addon

[![Build Status](https://travis-ci.org/rochoa/test-travis.svg?branch=master)](https://travis-ci.org/rochoa/test-travis)

Having a `.travis.yml` config file like:

```yml
sudo: false

addons:
  postgresql: "9.4"
  apt:
    packages:
    - postgresql-plpython-9.4

before_install:
  - createdb template_postgis
  - psql -c "CREATE EXTENSION postgis" template_postgis

script: echo 1
```

[It fails to install and start postgresql](https://travis-ci.org/rochoa/test-travis/builds/113432117#L150-L171) with an error like:
```
...

Setting up postgresql-9.4 (9.4.6-1.pgdg12.4+1) ...
Refused to start PostgreSQL 9.4, because PostgreSQL 9.1 is currently running! You should first stop 9.1 instance...
invoke-rc.d: initscript postgresql, action "start" failed.
dpkg: error processing postgresql-9.4 (--configure):
 subprocess installed post-installation script returned error exit status 13
dpkg: dependency problems prevent configuration of postgresql-contrib-9.4:
 postgresql-contrib-9.4 depends on postgresql-9.4 (= 9.4.6-1.pgdg12.4+1); however:
  Package postgresql-9.4 is not configured yet.
dpkg: error processing postgresql-contrib-9.4 (--configure):
 dependency problems - leaving unconfigured
dpkg: dependency problems prevent configuration of postgresql-plpython-9.4:
 postgresql-plpython-9.4 depends on postgresql-9.4 (= 9.4.6-1.pgdg12.4+1); however:
  Package postgresql-9.4 is not configured yet.
dpkg: error processing postgresql-plpython-9.4 (--configure):
 dependency problems - leaving unconfigured
No apport report written because the error message indicates its a followup error from a previous failure.
No apport report written because the error message indicates its a followup error from a previous failure.
Errors were encountered while processing:
 postgresql-9.4
 postgresql-contrib-9.4
 postgresql-plpython-9.4
E: Sub-process /usr/bin/dpkg returned an error code (1)
...
```
