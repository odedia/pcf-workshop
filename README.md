# PCF Workshop
An introduction to PCF and its capabilities

## Your first `cf push`

Let's start with a simple NodeJS application.
1. Download the `cf cli` from https://github.com/cloudfoundry/cli#downloads
2. Make sure cli is properly install by running `cf version`
3. Login to the environment:
```
CF_API_URL=<provided by instructor>
cf login -a $CF_API_URL
```
4. Select the space that matches your team as provided by instructor
5. Clone the NodeJS application from the following URL: https://github.com/odedia/cf-sample-app-nodejs
6. Review the `package.json` file.
7. Review the `manifest.yml` file.
8. Push your application to the Pivotal Cloud Foundry by running `cf push`.
