---
id: ubuntu
title: Ubuntu
---

:::warning
The following guide is intended for contributors to set-up ToolJet locally. If you're interested in **self-hosting** ToolJet, please refer to the **[Setup](/docs/setup/)** section.
:::

Follow these steps to setup and run ToolJet on Ubuntu. Open terminal and run the commands below.

## Setting up

1. Set up the environment

    1.1 Install NVM
    ```bash
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
    ```

    Use the command to load NVM:
    ```bash
    source ~/.nvm/nvm.sh
    ```

    Close and reopen your terminal to start using nvm
    ```bash
    nvm install 18.18.2
    ```

    Ensure you have the correct version of npm, or it will cause an error about fsevents.
    ```bash
    npm i -g npm@9.8.1
    ```

    1.2 Install Postgres
    ```bash
    sudo apt install postgresql postgresql-contrib
    sudo apt-get install libpq-dev
    ```
    
    1.3 Install PostgREST

    :::info
    Please use PostgREST version 12.2.0
    :::

    Please follow the installation [PostgREST](https://postgrest.org/en/stable/install.html) guide

2. Setup the repository:

    2.1 Fork the repository:

    Go to the [ToolJet GitHub repository](https://github.com/ToolJet/Tooljet), click on the **Fork** button to create a copy of the repository under your own GitHub account.

    2.2 Clone your forked repository:

    After forking, clone the forked repository to your local machine using the URL of your forked repo.

    ```bash
    git clone https://github.com/<your-username>/ToolJet.git
    ```
    
3. Set up environment variables

    Create a `.env` file by copying `.env.example`. More information on the variables that can be set is given in the [environment variables reference](/docs/setup/env-vars)
    ```bash
    cp .env.example .env
    ```

4. Populate the keys in the env file
   :::info
   `SECRET_KEY_BASE` requires a 64 byte key. (If you have `openssl` installed, run `openssl rand -hex 64` to create a 64 byte secure   random key)

   `LOCKBOX_MASTER_KEY` requires a 32 byte key. (Run `openssl rand -hex 32` to create a 32 byte secure random key)
   :::

   Example:
   ```bash
   cat .env
   TOOLJET_HOST=http://localhost:8082
   LOCKBOX_MASTER_KEY= <generate using 'openssl rand -hex 32'>
   SECRET_KEY_BASE= <generate using 'openssl rand -hex 64'>
   NODE_ENV=development
   # DATABASE CONFIG
   PG_HOST=localhost
   PG_PORT=5432
   PG_USER=postgres
   PG_PASS=postgres
   PG_DB=tooljet_development
   TOOLJET_DB=tooljet_db
   TOOLJET_DB_USER=postgres
   TOOLJET_DB_HOST=localhost
   TOOLJET_DB_PASS=postgres
   ```

5. Install and build dependencies
    ```bash
    npm install
    npm install --prefix server
    npm install --prefix frontend
    npm run build:plugins
    ```
   > **_NOTE:_**
   > If the `npm run build:plugins` command fails due to some packages are missing, try running the following command to install the necessary packages:
   `sudo apt install build-essential`
   > then proceed to `npm run build:plugins` step again
    

6. Set up database
    ```bash
    npm run --prefix server db:create
    npm run --prefix server db:reset
    ```
    :::info
    If at any point you need to reset the database, use this command `npm run --prefix server db:reset`
    :::

7. Run plugins compilation in watch mode
    ```bash
    cd ./plugins && npm start
    ```

8. Run the server
    ```bash
    cd ./server && npm run start:dev
    ```

9. Run the client
    ```bash
    cd ./frontend && npm start
    ```


    The client will start running on the port 8082, you can access the client by visiting:  [http://localhost:8082](http://localhost:8082)

10. Create login credentials

    Visiting https://localhost:8082 should redirect you to the login page, click on the signup link and enter your email. The emails sent by the server in development environment are captured and are opened in your default browser. Click the invitation link in the email preview to setup the account.


## Running tests

Test config requires the presence of `.env.test` file at the root of the project.

To run the unit tests
```bash
npm run --prefix server test
```

To run e2e tests
```bash
npm run --prefix server test:e2e
```

To run a specific unit test
```bash
npm run --prefix server test <path-to-file>
```
