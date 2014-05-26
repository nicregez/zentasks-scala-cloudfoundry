Zentasks Sample Application
===========================

This is a slight rework of the
[Play framework 2.1.1](http://www.playframework.com/documentation/2.1.1/Home)
Scala-language sample application - `zentasks` - to run on Cloud Foundry v2.
The application uses PostgreSQL instead of the in-built H2 in-memory database. 

PostgreSQL barked on the use of `user` as a table name because `user` is a reserved word.
The queries used in the application have been updated accordingly to use `users` instead. 

Deploying to Cloud Foundry v2
-----------------------------

To deploy the application to Cloud Foundry, create a PostgreSQL service instance in
Cloud Foundry, build the dist and push the application to Cloud Foundry using the
provided `manifest.yml` file. 

The provided `manifest.yml` has to be edited prior to deploying the application
as the route using the default host name is likely to be already taken the Cloud Foundry
environment. The output of the `cf app zentasks` command shows the route (URL) that was used.
Using the provided URL in the `urls` field displayed, you can browse to the running application.

The name of the service instance created by the command `cf create-service` has to
match the name of the service in the `manifest.yml` file.

```bash
$ cf create-service postgresql default tasks-db
$ play dist
$ cf push
```

Re-initialising the PostgreSQL database
---------------------------------------

If you would like to re-init the database, the easiest way is to delete and re-create
the database completely.

```bash
$ cf unbind-service zentasks tasks-db
$ cf delete-service tasks-db
$ cf create-service postgresql default tasks-db
$ cf push
```

Feedback
--------

Most welcome. Create pull-requests or contact me via email.
