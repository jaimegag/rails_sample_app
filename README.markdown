# Ruby on Rails Tutorial: sample application

This is the sample application for [*Ruby on Rails Tutorial: Learn Rails by Example*](http://railstutorial.org/) by [Michael Hartl](http://michaelhartl.com/).

This sample has been modified to run on Cloud Foundry. The `cf-autoconfig` gem was added to enable auto-configuration of database connections as described in the [Cloud Foundry documentation](https://docs.pivotal.io/pivotalcf/buildpacks/ruby/ruby-service-bindings.html). The `mysql2` and `activerecord-mysql2-adapter` gems were also added to support connection to MySQL database through ActiveRecord. 

## Running the application on Cloud Foundry

After installing in the 'cf' [command-line interface for Cloud Foundry](http://docs.pivotal.io/pivotalcf/cf-cli/install-go-cli.html),
targeting a Cloud Foundry instance, and logging in, the application can be pushed using these commands:

First, view a list of services and plans available in your Cloud Foundry instance: 

~~~
$ cf marketplace
Getting services from marketplace
OK

service          plans          description
app-autoscaler   bronze, gold   Scales bound applications in response to load
p-mysql          100mb-dev      MySQL service for application development and testing
p-rabbitmq       standard       RabbitMQ is a robust and scalable high-performance multi-protocol messaging broker.
~~~

Choose a MySQL service from the list and create a service instance named `rails-mysql` using a MySQL service and plan: 

~~~
$ cf create-service 100mb-dev rails-mysql
Creating service rails-mysql
OK
~~~

Now push the application: 

~~~
$ cf push APP-NAME
Using manifest file manifest.yml

Updating app rails-sample
OK

Creating route rails-sample.cfapps.io...
OK

Binding rails-sample.cfapps.io to rails-sample...
OK

Uploading rails-sample...
Uploading app files from: rails_sample_app
Uploading 444.2K, 217 files
Done uploading
OK
Binding service rails-mysql to app rails-sample
OK

Starting app rails-sample
...

0 of 1 instances running, 1 starting
1 of 1 instances running

App started

Showing health and status for app rails-sample
OK

requested state: started
instances: 1/1
usage: 256M x 1 instances
urls: rails-sample.cfapps.io
last uploaded: Fri Mar 11 18:29:50 UTC 2016
stack: cflinuxfs2
buildpack: ruby

     state     since                    cpu    memory          disk
#0   running   2014-05-29 03:34:22 PM   0.0%   50.3M of 256M   80.2M of 1G
~~~

The application will be pushed using settings in the provided `manifest.yml` file. The output of the
`cf push` command shows the URL that was assigned. Using the provided URL you can browse to the running application.
