# Employee Management system - challenge.
<!-- [![Maintainability](https://api.codeclimate.com/v1/badges/e4f2f989e61455bf391a/maintainability)](https://codeclimate.com/github/Stackup-Rwanda/stackup2-barefoot-backend/maintainability)   [![Build Status](https://travis-ci.org/Stackup-Rwanda/stackup2-barefoot-backend.svg?branch=develop)](https://travis-ci.org/Stackup-Rwanda/stackup2-barefoot-backend)
[![Coverage Status](https://coveralls.io/repos/github/Stackup-Rwanda/stackup2-barefoot-backend/badge.svg?branch=develop)](https://coveralls.io/github/Stackup-Rwanda/stackup2-barefoot-backend?branch=develop)
[![Reviewed by Hound](https://img.shields.io/badge/Reviewed_by-Hound-8E64B0.svg)](https://houndci.com) -->

## Testing

For testing follow below steps:

* First clone it by running `$ git clone https://github.com/muchristian/employeems-challenge.git`
* Run `$ npm install` to install packages
* Choose between two environment variable `$ NODE_ENV=development | test`
* For `$ NODE_ENV=development` start server by running `$ npm run dev` 
* For `$ NODE_ENV=test` start server by running `$ npm test`


## Sequelize and Sequelize-cli

This API uses Sequelize as its ORM. To get you started, we will configure sequelize using .sequelizerc file.

The .sequelizerc file will in turn be used by sequelize-cli to setup the the sequelize folder structure.

### 1. Configure environment variables

The following are example environment variables needed:

#### Database

* DEV_DB_USERNAME
* DEV_DB_PASSWORD
* DEV_DB_NAME
* DEV_DB_HOSTNAME
* DEV_DB_PORT

#### General

* NODE_ENV=development

According to [the docs](https://sequelize.org/v5/manual/migrations.html), sequelize will only use Model files, it's the table representation. On the other hand, the migration file is a change in that model or more specifically that table, used by CLI. Treat migrations like a commit or a log for some change in database.
### 1. Create or Drop DB
If you may want to create a database, you'll have to run `$npm run db:create` that represent `$ npx sequelize-cli db:create`

And for if you may want to drop a database, you'll have to run `$npm run db:drop` that represent `$ npx sequelize-cli db:drop`

### 2. Running Migrations

Until this step, we haven't inserted anything into the database. We have just created required model and migration files for our first model User. Now to actually create that table in database you need to run `db:migrate` command.

`$ npx sequelize-cli db:migrate`

This command will execute these steps:

* Will ensure a table called SequelizeMeta in database. This table is used to record which migrations have run on the current database
* Start looking for any migration files which haven't run yet. This is possible by checking `SequelizeMeta table`. In this case it will run `XXXXXXXXXXXXXX-create-user.js` migration, which we created in last step.
* Creates a table called `Users` with all columns as specified in its migration file.

### 4. Undoing Migrations

Now our table has been created and saved in database. With migration you can revert to old state by just running a command.

You can use `db:migrate:undo`, this command will revert most recent migration.

`$ npx sequelize-cli db:migrate:undo`

You can revert back to initial state by undoing all migrations with `db:migrate:undo:all` command. You can also revert back to a specific migration by passing its name in `--to` option.

`$ npx sequelize-cli db:migrate:undo:all --to XXXXXXXXXXXXXX-create-user.js`

Refer to the [sequelize](https://sequelize.org/v5/) and [sequelize-cli](https://github.com/sequelize/cli/tree/master/docs) docs for more information.

## Endpoints Specifications

| Endpoint | Request | Status | Description |
| --- | --- | --- | --- |
| / | GET | 200 OK | Helps users to access to the parent api for the whole application|
| /api/auth/signup | POST | 201 CREATED | Makes a post request to signup a new user and return access token |
| /api/auth/login | POST | 200 OK | Makes a post request to login an existing user and return an access token |
| /api/auth/resetpassword | POST | 200 OK | Makes a post request, for for requesting to reset a password by sending the user's email and it returns a token to send with the next route of resetting password |
| /api/auth/resetpassord/:token | POST | 200 OK | Makes a POST request reset user's password |
| /api/profile | GET | 200 OK | Makes a GET request, to help a logged-in user to see his profile after successful login |
| /api/profile/:username | GET | 200 OK | Makes a GET request to help a user to see other users' profiles by adding their usernames in URL |
| /api/profile | PATCH | 200 OK | Makes a PATCH request when a user wants to update his profile |
| /api/profile/password | PATCH | 200 OK | Makes a PATCH request to help password changes, whenever a user needs to change his/her password directly from his/her profile|
| /api/auth/verify?token=eyWWWSDHFGC | GET | 200 OK | Makes a GET request when a user clicks on the link that is sent to him/her via Email to verify his/her email |
| /api/trips/inapp/notification | GET | 200 OK | It shows the inApp notifications to manager and requester |
| api/auth/disable?mode=inapp | PATCH | 200 OK | It enables/disables inApp notifications |
| api/auth/disable?mode=email | PATCH | 200 OK | It enables/disables email notifications |
| ||More Details about all of the above endpoints, their responses form, and when there is an error how they respond, please click here for further documentation [Documentation](https://stackup2-barefoot-backend-stag.herokuapp.com/public/api-docs/#/) ||
