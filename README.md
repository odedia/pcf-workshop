# PCF Workshop
An introduction to PCF and its capabilities

## 1. Your first `cf push`

Let's start with a simple NodeJS application.
1. Download the `cf cli` from https://github.com/cloudfoundry/cli#downloads
2. Make sure cli is properly install by running `cf version`
3. Login to the environment:
```
CF_API_URL=<provided by instructor>
cf login -a $CF_API_URL
```
4. Select the org and space that matches your team as provided by the instructor.
5. Clone the NodeJS application from the following URL: https://github.com/odedia/cf-sample-app-nodejs
6. Review the `package.json` file.
7. Review the `manifest.yml` file.
8. Push your application to the Pivotal Cloud Foundry by running `cf push`.


## 1. Exploring the application from the command line

The apps manager is a great place to view information about your application, but everything can also be done from the command line or through REST api calls.
1. Run `cf app cf-nodejs` to see an overview about your application
2. Run `cf scale -i 2 cf-nodejs` to scale your application to two instances.
3. Run `cf logs --recent cf-nodejs` to view the latest aggregated logs from all instances of your application.
4. Run `cf logs cf-nodejs` to get a constant stream of the current logs from your application. Refresh the app on a browser and see the results in the logs. Notice how some logs are emitted from the platform, such as [RTR/0].
5. Run `cf restart cf-nodejs` to perform a simple restart of the node process in each container.
6. Run `cf restage cf-nodejs` to perform a full container rebuild from the last push.
6. Run `cf events cf-nodejs` to view the latest events that occured in your application.
7. Sometimes it makes sense to see exactly what goes on inside a container. Run `cf ssh cf-nodejs` to ssh into one of the running containers of your application. Remember, all containers are stateless and created from the same image, so they are all pretty much the same. Explore the contents of the `app` directory. `exit` the container when done.
8. The `cf cli` is extensible. View the available extensions by running `cf repo-plugins`.
9. Install the `top` cf plugin by running `cf install-plugin top`.
10. Run `cf top` to view a unix-like `top`  of the orgs you can work on.
11. You can review all available commands by running `cf help`.

## 2. Pushing a python application
1. Download the python example from https://github.com/odedia/python-cf-example
2. Review the manifest.yml
3. Push your app with `cf push`.
4. Check the app in Apps Manager. What has changed from the previous deployment?

## 3. .NET Framework and Windows Containers
1. Clone the .NET Framework application from https://github.com/odedia/pcf-dotnet-environment-viewer.
2. Inspect the code. This is a standard .NET Framework application.
3. Under the ViewEnvironment directory, create a manifest.yml with the following data (replace <Your Name>:
```
---
applications:
- name: dotnet-app
  host: dotnet-<Your Name>
  memory: 1024m
  stack: windows2016
  buildpack: hwc_buildpack
```
4. `cf push` the app.
5. View the application in your browser. Inspect the app in Apps Manager.
5. Run `cf ssh dotnet-app`. You are now inside the Windows container. You can see the code under the `app` diretory.

### 4. Service Brokers
1. Inspect the options in the marketplace from the UI. Each service has a few plans available as defined by the operator.
2. Run `cf marketplace` from the command line. You should see the same services.
3. Create a MySQL service from the command line: `cf create-service p.mysql db-small mysql`.
4. Run `cf service mysql` to monitor the progress of the service creation. The platform now creates a virtual machine at the BOSH layer to host your database.
5. Bind the application to your dotnet-app: `cf bind-service mysql dotnet-app`.
6. Restage your application: `cf restage dotnet-app`
7. Inspect the app in Apps Manager. Under services, you will see the bounded service.
8. Inspect the running application. You will now see an "Attendees" section in the UI. You can restart the app and the data will remain.
