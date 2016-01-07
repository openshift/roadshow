#** Lab 9: Using Templates**

Running all these individual commands can be tedious and error prone.
Fortunately for you, all of this configuration can be put together into a single
*Template* which can then be processed to create a full set of resources. A
*Template* may define parameters for certain values, such as DB username or
password, and they can be automatically generated by OpenShift at processing
time.

Administrators can load *Templates* into OpenShift and make them available to
all users, even via the web console. Users can create *Templates* and load them
into their own *Projects* for other users (with access) to share and use.

The great thing about *Templates* is that they can speed up the deployment
workflow for application development by providing a "recipe" of sorts that can
be deployed with a single command.  Not only that, they can be loaded into
OpenShift from an external URL, which will allow you to keep your templates in a
version control system.

Let's combine all of the exercises we have performed in the last three labs into
a single *Template* that we can then instantiate with a single command.  I bet
you are probably hating us now for having you go through all of that work when
you could have issued a single command! Just remember that it is important for
you to understand how to create, deploy, and wire resources together.  In order
for the magic to happen, first create a new project and add the template to the
project:

	$ oc new-project userXX-template
	$ oc create -f https://raw.githubusercontent.com/gshipley/openshift3mlbparks/master/mlbparks-template.json

Now we have access to the application template in our project.  As a side note, administrators have the capability to add templates to the general *openshift* project which will in turn provide an application template to any user on the system.

Are you ready for the magic command?  Here it is:

	$ oc new-app mlbparks

You will see the following output:

    --> Deploying template mlbparks for "mlbparks"
         With parameters:
          APPLICATION_NAME=mlbparks
          APPLICATION_DOMAIN=
          SOURCE_REPOSITORY_URL=https://github.com/gshipley/openshift3mlbparks
          SOURCE_REPOSITORY_REF=master
          CONTEXT_DIR=
          HORNETQ_QUEUES=
          HORNETQ_TOPICS=
          HORNETQ_CLUSTER_PASSWORD=BlflcWjX # generated
          GITHUB_WEBHOOK_SECRET=FdhVeba3 # generated
          GENERIC_WEBHOOK_SECRET=pbp4lDMM # generated
          IMAGE_STREAM_NAMESPACE=openshift
          DATABASE_SERVICE_NAME=mongodb
          MONGODB_USER=user7TI # generated
          MONGODB_PASSWORD=4IucG7FYvPeXWKqQ # generated
          MONGODB_DATABASE=sampledb
          MONGODB_ADMIN_PASSWORD=7DlSvtYyAscfL2fC # generated
    --> Creating resources with label app=mlbparks ...
        Service "mlbparks" created
        Route "mlbparks" created
        ImageStream "mlbparks" created
        BuildConfig "mlbparks" created
        DeploymentConfig "mlbparks" created
        Service "mongodb" created
        DeploymentConfig "mongodb" created
    --> Success
        Build scheduled for "mlbparks" - use the logs command to track its progress.
        Run 'oc status' to view your app.

OpenShift will automatically start a build for you. When it is complete, visit
your app. Does it work? Think about how this could be used in your environment.
For example, a template could define a large set of resources that make up a
"reference application", complete with several app servers, databases, and more.
You could deploy the entire set of resources with one command, and then hack on
them to develop new features, microservices, fix bugs, and more.

As a final exercise, look at the template that was used to create the
resources for our *mlbparks* application.

    https://raw.githubusercontent.com/gshipley/openshift3mlbparks/master/mlbparks-template.json

**End of Lab 9**