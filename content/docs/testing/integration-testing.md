---
title: "Integration Testing"
draft: false
weight: 10
---

Ourchive leverages integration testing to test end-to-end flows for activities such as searching or loading a user's works. We have a separate Cypress repo to accomplish this goal, as well as settings that allow you to run the app against a database specifically for integration testing.

## Data Setup

Integration tests should use `ourchive_app.settings.integration`, which uses a different database and includes information on test data for the app. 

Create a database, e.g. `ourchive_db_integration`, on the same database server with the same user as your local dev environment. Set the appropriate value in your .env file:

```bash {title=".env"}
OURCHIVE_INTEGRATION_DB_NAME=ourchive_db_integration
``` 

Then, in the terminal, activate your venv, cd to `ourchive/ourchive_app`, and run the data population script:

```bash
./generate-test-data.sh
```

This script does three things:
1. Applies migrations to the database configured in `ourchive_app.settings.integration`
2. Runs the `loadourchivedata` management command to load necessary data (settings and notification types)
3. Runs the `createintegrationtestdata` management command to load test data for integration testing.

`createintegrationtestdata` uses <a href="https://faker.readthedocs.io/en/master/index.html" target="_blank" title="Faker Docs">Faker</a> to generate fake data to populate a site. This includes:

* Basic data: users, tag types, work types, attribute types, languages
* Chives: works, bookmarks, collections, series, anthologies, with associated tags, languages, attributes, and other FK data
* Admin data: news, announcements

This is done leveraging `ourchive_app.util.ourchive_fakes`. The `ourchive_app` module's `tests.py` has a test suite for these functions, which you can run to observe their behavior. Note that under test, `generate_everything` is flaky - so the test is skipped, but you can run it to debug if need be. (The flakiness is largely a function of duplicate data concerns that are handled when the script is run by the management console.)

Once you've run the bash script, you should be able to start the site:

```bash
python manage.py runserver --settings=ourchive_app.settings.integration
```

And view the generated data.

{{< callout context="note" title="Note" >}} 
You can generate more data by running the `createintegrationtestdata` command yourself:

```bash
python manage.py createintegrationtestdata --settings=ourchive_app.settings.integration
```

The `-s` flag tells the command to skip creating unique data like users and tag types, but will create more chives, admin info, etc. This can be useful if you're testing something like search pagination. Use 
```bash
python manage.py createintegrationtestdata --help
```
for more information on this command.
{{</ callout >}}

## Cypress Setup

### Prerequisites

To ensure Cypress works on your machine prior to installing our tests, please follow their [guide](https://docs.cypress.io/guides/getting-started/installing-cypress). We test using their npm instructions.

### Setup

In your projects directory, clone the repo.

```bash
git clone https://github.com/OurchiveIO/ourchive-e2e-tests
```

Navigate to the directory and install requirements.

```bash
cd ourchive-e2e-tests
npm install
```

{{< callout context="note" title="Note" >}} 
Current config assumes you're using the default Django `runserver` URL, `http://127.0.0.1:8000/`. If you're not, just update `cypress.config.js` with your URL.
{{</ callout >}}

In your root `ourchive-e2e-tests` directory, copy the environment variables:

```bash
cp cypress.env.EXAMPLE.json cypress.env.json
```

Open `cypress.env.json` and update the variables if you want. 


**searchTerm**: Used for search smoke testing, the term that is typed in the search box. Default is a word we are sure Faker will seed for us: "the".

**facetFilter**: The checkbox filter used to test faceted filtering. Default is one of our generated data's work types: "Fic".


Run Cypress:

```bash
npm run cy:open
```

You should see Cypress open up. Click 'E2E Testing' - you will likely see an error:

{{< img loading="eager" fetchpriority="high" src="cypress-config-issue-screenshot.png" alt="Screenshot of Cypress running locally with a 'cannot connect base URL' warning." >}}

<br/>
To fix that you just need to ensure the app is running (against the integration settings, so you get all the data we just loaded). In a separate terminal window or tab, with your venv activated, in the `ourchive/ourchive_app` directory:

```bash
python manage.py runserver --settings=ourchive_app.settings.integration
```

You should now be able to run the integration tests. 

## Contributing

We welcome contributions to the E2E repo. As of 2024, we are targeting smoke testing and form functionality (CRUD operations on chives, users, etc).