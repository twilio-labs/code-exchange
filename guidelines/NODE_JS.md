# Node.js Coding Guidelines

## Background

These guidelines have been authored with the following things in mind:

**consistency**
All code should be formatted and written the same way

**maintainability**
Having automated tests to check the main functionality of the application allows us to keep apps up-to-date

**pluggability**
By keeping a consistent application format and a minimum consistent set of dependencies means developer can more easily combine different applications

**contribution-friendliness**
Every template/application should be friendly to new contirbutors to allow to fix bugs or add missing features.

## Guidelines

With these criteria in mind we came up with the following guidelines. To make it easy for people to get started, we are also maintaining an example repository that you can use as a template for your application:
==> github.com/twilio-labs/sample-template-nodejs

**If possible use the [provided template to start your application](https://github.com/twilio-labs/sample-template-nodejs).**

### 1. Be familiar

Any of our applications should feel familiar to the developer. While for a general Node.js application that might mean we can start with a blank slate application, for some applications like a React app this means starting with the standard bootstrapped project. For example using `create-react-app` for React, `ng init` for Angular, etc.

After that see how the remaining guidelines fit into this.

### 2. Use a linter

Linting allows us to keep the code consistent. The preferred linter for us is a combination of [`eslint`](https://npm.im/eslint) and [`prettier`](https://npm.im/prettier).

The preferred configurations for these tools are:

- [`.eslintrc.json`](https://github.com/twilio-labs/sample-template-nodejs/blob/master/.eslintrc.json)
- [`.prettierrc`](https://github.com/twilio-labs/sample-template-nodejs/blob/master/.prettierrc)

### 3. Testing

Our code should be reliable and maintainable and testing plays a big part in this. The more tests you can author for your application, the better. However, at the very least you should have some general tests covering the core functionality of your application. This will allow us to keep applications easier up-to-date with automated dependency updates.

Our preferred testing frameworks are:

- [`jest`](https://jestjs.io/) as a general testing framework (backend & frontend)
- [`cypress`](https://www.cypress.io/) for E2E UI tests
- [`mocha`](https://npm.im/mocha) and [`chai`](https://npm.im/chai) if already available in the project
- [`supertest`](https://npm.im/supertest) for testing HTTP APIs
- [`nock`](https://npm.im/nock) for mocking external APIs like Twilio

When in doubt you should cover tests for template applications in the following order:

1. Test the endpoints/webhooks your app is exposing (for example using `supertest`)
2. Create E2E tests for your user interface to check for the basic functionality
3. Write additional unit tests starting with the mosts complex/critical functions

### 4. Frameworks & libraries

In general you should use as many or little libraries as it makes sense for the respective target audience. Less libraries and dependencies makes it easier for people to adopt it. But if that means the codebase increases significantly because of code that is seemingly unrelated to the use-case, use a library/dependency instead.

If an application can be written in a serverless & stateless fashion like using [Twilio Functions](https://twilio.com/functions), you should prefer that, write your template as a Function Template and submit it to github.com/twilio-labs/function-templates.

If you'll require a more complex webserver, use [`express`](https://npm.im/express) as for scaffolding your webserver.

Some other common libraries and tools that can be used in your template:

- [`nodemon`](https://npm.im/nodemon) for restarting development servers
- [`got`](https://npm.im/got) for HTTP requests in Node.js
- [`parcel-bundler`](https://parceljs.org/getting_started.html) for a general purpose bundler unless [`webpack`] is already part of the project. `parcel` supports a wide variety of functionality without any configuration necessary
- [`node-env-run`](https://npm.im/node-env-run) and [`configure-env`](https://npm.im/configure-env) as libraries for loading and setting environment variables (see next section). Alternatively [`dotenv`](https://npm.im/dotenv) or [`dotenv-safe`](https://npm.im/dotenv-safe)

### 5. Using Environment Variables

Credentials for Twilio and other external services as well as things like service SIDs should be stored as environment variables. In order to make it easy for people to get started, every project should use `.env` files for this.

The actual `.env` file should never be included in a template and should be part of the `.gitignore` file. However, a project should have an `.env.example` file that specifies every environment variable necessary, including default values where applicable and a comment line (prefixed with `#`) above it specifying what this value is and how to retrieve the value (for example sign up at twilio.com).

The tool [`configure-env`](https://npm.im/configure-env) can be used in a setup script or in the setup instructions and will use the `.env.example` file as a fundation to prompt the user for these values

Libraries to load environment variables are:

- [`node-env-run`](https://npm.im/node-env-run) to run Node with values from a `.env` file without having to modify code
- [`dotenv-safe`](https://npm.im/dotenv-safe) to load env variables and check if everything in `.env.example` is also set in `.env`
- [`dotenv`](https://npm.im/dotenv) to just load `.env` files

### 6. Databases

We want to make the project setup for people as easy as possible. In order to avoid them having to wrestle with databases, whenever possible, you should use a filesystem based one. For basic use cases [`lowdb`](https://npm.im/lowdb) is a good library. For more advanced use cases [`sqlite3`](https://github.com/mapbox/node-sqlite3) can come handy.

If possible you should also pre-populate the database with some basic data.

### 7. Continous Integration

GitHub introduced GitHub Actions as a way to run continous integration tests directly on their platform allowing to test apps on Windows, Linux and macOS. This is our preferred way of running tests and other automation. You can find some basic templates in the sample repository: https://github.com/twilio-labs/sample-template-nodejs/tree/master/.github/workflows

### 8. General Files & Structure

Every project should have the following files to improve the experience for developers:

- `README.md` with a [structure following the template project](https://github.com/twilio-labs/sample-template-nodejs/blob/master/README.md)
- `CONTRIBUTING.md` explaining how to contribute to this project for example to fix bugs. This can be included in the `README.md`

As for the overall structure of your project, follow what's the best practice for the target audience. For a general Node.js application, take the basic template as a reference: https://github.com/twilio-labs/sample-template-nodejs
