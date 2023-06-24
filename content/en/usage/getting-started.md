---
title: Getting Started
weight: -20
---

This page describes installing and running Ourchive locally for the purposes of development.

If you are planning to install Ourchive as a website, please refer to the [admin docs](https://changeme).

<!--more-->

{{< toc >}}

## Prerequisites

- Python 3.x+
- Postgres 15+ [docs](https://www.postgresql.org/docs/15/index.html)
- Python 3.x+ dev tools

### Install prerequisites

{{< hint type=note >}}
**Info**\
The below instructions assume you are installing on an Ubuntu machine. Similar comments should work for any Unix-based machine but are beyond the scope of this documentation.
{{< /hint >}}

{{< hint type=important >}}
**Warning**\
There's more than one way to climb a tree and there's more than one way to get a working Python development environment going. The below relies heavily upon best practices described in [Python's documentation](https://docs.python.org/3/library/venv.html).
{{< /hint >}}


```shell
# install python 
sudo apt-get update && sudo apt-get upgrade
sudo apt-get install python3.11

# install python dev tools
sudo apt-get install python3.11-dev

# install postgres
sudo apt install postgresql postgresql-contrib
sudo systemctl start postgresql.service

# log into postgres
sudo -u postgres psql

# create database and user. NOTE: the below assumes you are in
# a development environment and that you are using Postgres version 15
# or higher.
CREATE DATABASE ourchive_db;
CREATE USER ourchive WITH PASSWORD 'ourchive';
GRANT ALL PRIVILEGES ON DATABASE ourchive_db TO ourchive;
\c ourchive_db postgres
GRANT ALL ON SCHEMA public TO ourchive;
```

### Set up virtual environment

The below instructions assume you installed python3.11 following the instructions above. You can check to see what version of python your default 'python' installation points to:

```shell
python --version
```

If it outputs "Python 3.11.2" or any version higher than 3.11, the below instructions can look like `python -m venv venv`.

If you have not created a virtual environment before, we strongly recommend reviewing (Python's docs)[https://docs.python.org/3/library/venv.html].

1. Create & activate the virtual environment

```shell
# clone the repo
git clone https://github.com/c-e-p/ourchive

# enter repo & create virtual environment
cd ourchive
python3.11 -m venv venv

# activate the virtual environment
source venv/bin/activate
```

2. Install requirements

```shell
cd ourchive_app
pip install -r requirements.txt
```

#### Troubleshooting

You are pretty likely to get errors related to `psygopg2`. Never fear, this is a common error and there are many resources on the internet to help you fix it.

If you get an install error for `psycopg2` that references `libpq-fe.h`:
```shell
         ./psycopg/psycopg.h:36:10: fatal error: libpq-fe.h: No such file or directory
         36 | #include <libpq-fe.h>
```

Refer to the solve [here](https://askubuntu.com/questions/1372562/how-to-install-libpq-dev-14-0-1-on-ubuntu-21-10).

If you have a different error, we strongly recommend searching for the error and seeing how others have solved it, as it is likely specific to your machine/version/distro/etc. 

### Load fixture data

### Update settings

### Run migrations

### Run server

## Using the theme