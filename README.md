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

In this example our code runs the [`main`
method](https://github.com/phanikumarmss/sparkJava/blob/master/src/main/java/com/google/appengine/sparkdemo/Main.java) 

In the main method, we have a sample java `staticFiles.location("/public");` which specifies the location of the static content. 

get("/", (req, res) -> {
            res.redirect("index.html"); return null;
        });
        
The above method will serve the request on http://URL/ by redirecting the response to `index.html`

 get("/hello", (req, res) -> "Hello World");
 
From the above code, we can directly serve the request on `http://URL/hello` with a simple string.

# App.yaml
This file in the application is responsible for specifying the type of environment onto which the Google App Engine should deploy the application onto. As well as some other configurations like autoscaling, service name and many more.

# Dockerfile

As our application belongs to flexible environment, we can specify the list of operations that should be performed on the container to start our application on Google App Engine.

FROM gcr.io/google_appengine/openjdk #The container that should be used to deploy our application
VOLUME /tmp #The volume that should be attached to the container from the underlying infrastructure
ADD spark-1.0-jar-with-dependencies.jar app.jar #In general, [`ADD`](https://docs.docker.com/engine/reference/builder/#add) ` source destination` copies the source file to the destination in the container. Here we will be copying `spark-1.0-jar-with-dependencies.jar` to destination with app.jar name.
[`CMD`](https://docs.docker.com/engine/reference/run/#cmd-default-command-or-options) [ "java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"] executes the command to run our application on Google App Engine Flexible environment.

