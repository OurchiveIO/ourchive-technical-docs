---
title: "Getting Started"
draft: false
weight: 1
toc: true
---

This page describes installing and running Ourchive locally for the purposes of development.

If you are planning to install Ourchive as a website, please refer to the [admin docs](https://docs.getourchive.io).

<!--more-->

# Local Development with Docker

If you would like to do development with Docker containers, this is currently supported. Please visit [Developing with Docker]({{<ref "docker-development.md">}}).


# Local Development Native

## Prerequisites

{{< callout context="caution" title="Heads Up" icon="alert-triangle" >}} 

The below instructions assume you are installing on an Ubuntu machine. Similar commands should work for any Unix-based machine but are beyond the scope of this documentation.
{{</ callout >}}

- Python 3.x+
- Postgres 15+ [docs](https://www.postgresql.org/docs/15/index.html)
- Python 3.x+ dev tools

{{< callout context="caution" title="Regarding Virtual Environments" icon="alert-triangle" >}} 
****

There's more than one way to climb a tree and there's more than one way to get a working Python development environment going. The below relies heavily upon best practices described in [Python's documentation](https://docs.python.org/3/library/venv.html).

{{< /callout >}}


### Python & Postgres

```bash
# install python 
sudo apt-get update && sudo apt-get upgrade && sudo apt-get install python3.11

# install python dev tools
sudo apt-get install python3.11-dev

# install postgres
sudo apt install postgresql postgresql-contrib

# start the service
sudo systemctl start postgresql.service

# log into postgres
sudo -u postgres psql

# create database and user. NOTE: the below assumes you are in
# a development environment and that you are using Postgres version 15
# or higher.

# create the database
CREATE DATABASE ourchive_db;

# create the Ourchive user. This should match the information in settings.py.
CREATE USER ourchive WITH PASSWORD 'ourchive';

# grant privileges to the ourchive user
GRANT ALL PRIVILEGES ON DATABASE ourchive_db TO ourchive;

# connect to the db
\c ourchive_db postgres

# grant schema permissions
GRANT ALL ON SCHEMA public TO ourchive;

# exit from the database
\q

# this tells the system to create the trigram extension when a new database is created. this allows search
# integration tests to pass.
psql -d template1 -c "CREATE EXTENSION pg_trgm;" -U ourchive
```

### Set up virtual environment

The below instructions assume you installed python3.11 following the instructions above. You can check to see what version of python your default 'python' installation points to:

```bash
python --version
```

If it outputs "Python 3.11.2" or any version higher than 3.11, the below instructions can look like `python -m venv venv`.

If you have not created a virtual environment before, we strongly recommend reviewing (Python's docs)[https://docs.python.org/3/library/venv.html].

1. Create & activate the virtual environment

```bash
# clone the repo
git clone https://github.com/OurchiveIO/ourchive

# enter repo & create virtual environment
cd ourchive && python3.11 -m venv venv

# activate the virtual environment
source venv/bin/activate
```

2. Install requirements

```bash
cd ourchive_app && pip install -r requirements.txt
```

#### Troubleshooting

You are pretty likely to get errors related to `psygopg2`. Never fear, this is a common error and there are many resources on the internet to help you fix it.

If you get an install error for `psycopg2` that references `libpq-fe.h`:
```bash
./psycopg/psycopg.h:36:10: fatal error: libpq-fe.h: No such file or directory
36 | #include <libpq-fe.h>
```

Refer to the solve [here](https://askubuntu.com/questions/1372562/how-to-install-libpq-dev-14-0-1-on-ubuntu-21-10).

If you have a different error, we strongly recommend searching for the error and seeing how others have solved it, as it is likely specific to your machine/version/distro/etc. 

## Run migrations

```bash
# run migrations
python manage.py migrate
```

## Load fixture data

{{< callout context="caution" title="Caution" icon="alert-triangle" >}} 
**Do not skip this step!**

Ourchive is a configurable app. You need to load settings data or the app will not function properly!
{{</ callout >}}

Ourchive ships with fixture data for some necessary configurations and for convenience of development. You **must** load settings. You can load works, bookmarks, etc for the convenience of starting with a pre-loaded environment.

```bash
# load the fixture data
./load-fixtures.sh
```

## Run server
```bash
# run migrations
python manage.py runserver
```

## That's it

You should now have a working installation of Ourchive. 

## Troubleshooting

"But I don't", you cry. Not to worry, it happens to the best of us. Here are some basic troubleshooting tips:

1. Follow the error: Google the console and/or site output. Common issues include database connectivity, pip versioning issues, or python devtools problems.
2. Delete everything and start over: Ourchive is a fairly simple app right now with minimal external dependencies. Sometimes a clean reinstall can help.
3. [Open an issue](https://github.com/OurchiveIO/ourchive/issues/new/choose) with the Ourchive team. We want to help!

{{< img loading="eager" fetchpriority="high" src="dr_manhattan.jpg" alt="Dr Manhattan meme with the text 'just keep deleting your venv and reinstalling, it'll work this time for sure'" >}}