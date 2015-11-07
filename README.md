Welcome to the OBP API Explorer
===============================

# ABOUT

This application is used to explore the OBP API and interact with the data and services in the context of the logged in user.



# LICENSE

This project is licensed under the AGPL V3 (see NOTICE) and a commercial license from TESOBE.

# SETUP

The project is using sbt or Maven 3 as a build tool.
See build.scala or pom.xml respectively for the dependencies.

----

To compile and run jetty, cd into the root directory (where this file is) and run:

$ sbt
...
> compile
> ~;container:start; container:reload /

(Note that you first have to start sbt and then on its console start jetty with the container:start task, otherwise it will exit immediately. More here: https://github.com/siasia/xsbt-web-plugin/wiki)

In OS X, sbt can be installed with $ sudo port install sbt

----


Alternatively, maven can also be used:

mvn jetty:run


Note: You may need to add the pluginGroup to the $HOME/.m2/settings.xml

<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                      http://maven.apache.org/xsd/settings-1.0.0.xsd">
  ...
  <pluginGroups>
    <pluginGroup>org.mortbay.jetty</pluginGroup>
  </pluginGroups>
  ...
</settings>

---

## Ubuntu

If you use Ubuntu (or a derivate) and encrypted home directories (e.g. you have ~/.Private), you might run into the following error when the project is built:

    uncaught exception during compilation: java.io.IOException
    [ERROR] File name too long
    [ERROR] two errors found
    [DEBUG] Compilation failed (CompilerInterface)

The current workaround is to move the project directory onto a different partition, e.g. under /opt/ .

# PROPS FILE

There is a props file template provided at src/main/resources/props/sample.props.template. It needs to be renamed and modified in order for
the application to work.

1. Renaming:

The sample.props.template file must be renamed for Lift to find it (https://www.assembla.com/wiki/show/liftweb/Properties). Renaming it to default.props
should be the easiest way to get started.


*base_url*

The base_url is used to calculate the callback url to give to the Open Bank Project API server. This should just be the
base url used to access the API Explorer. So if you're running a copy of the API Explorer at
api-explorer.example.com over https, on the standard port, it would be "https://api-explorer.example.com".
An example value for local development could be: http://127.0.0.1:8082 (8080 is the default Lift development port)

*api_hostname*

The api_hostname should be the base url of the Open Bank Project API. For example, https://api.openbankproject.com/api

*obp_consumer_key*
*obp_secret_key*

The keys are obtained by registering as a developer on the Open Bank Project API server located at "api_hostname".


All in all, a props file could look something like:

api_hostname=https://api.openbankproject.com/api
obp_consumer_key=uodsifnodsfifdsliufdsliufdsfdsfsdfsx
obp_secret_key=iuesbfiyvglxzgifg7eisgei7fglesfi
base_url=http://localhost:8082
