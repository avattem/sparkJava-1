# SparkJava on App Engine Flexible Environment

This repository demonstrates a sample Spark Java application to deploy it into Google App Engine.

# Running locally
Run the application on your local machine by typing the following into your command line from the sparkjava directory: mvn clean package exec:java. Navigate to localhost:8080 to view and interact with the application.

Setup
-----

1.  Create a Google Cloud project with the App Engine API enabled.
    [Follow these
    instructions](https://cloud.google.com/docs/authentication#preparation) to
    get your project set up. If you wish to deploy this application, you will
    also need to [enable
    billing](https://support.google.com/cloud/?rd=2#topic=6288636).

2. Set up the local development environment by [installing the Google Cloud
   SDK](https://cloud.google.com/sdk/) and running the following commands in
   command line: `gcloud auth application-default login` and `gcloud config set project [YOUR
   PROJECT ID]`.

3. Ensure that you have Maven installed and configured to use Java 8. See
   installation instructions [here](https://maven.apache.org/install.html).
   
   
Deploying
---------

If you've enabled billing (step 1 in [Setup](#Setup)), you can deploy the
application to the web by running `mvn appengine:deploy` from your command line
(from the `sparkjava` directory).

How does it work?
-----------------

You'll notice that the source code is split into three folders: `appengine`,
`java/com/google/appengine/sparkdemo`, and `resource/public`. The `appengine`
folder contains a `Dockerfile` and an `app.yaml`, necessary files to [configure
the VM
environment](https://cloud.google.com/appengine/docs/managed-vms/config). 

In this example we have a [main class file] (https://github.com/phanikumarmss/sparkJava/blob/master/src/main/java/com/google/appengine/sparkdemo/Main.java)

