---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-11"
---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Deploying apps by using the cf command

When you deploy your applications to {{site.data.keyword.Bluemix_notm}} from the command line interface, a buildpack must be provided as the runtime environment according to your application language and framework. You can also use the Delivery Pipeline service to deploy applications to {{site.data.keyword.Bluemix_notm}}.

{{site.data.keyword.Bluemix_notm}} provides built-in buildpacks that support Java and Node.js. If you are using these languages and frameworks, you don't need to specify the buildpack when you deploy your application by using the command line interface. Because {{site.data.keyword.Bluemix_notm}} is built on Cloud Foundry, the command defaults to these buildpacks.

If you use an external buildpack, you must specify the URL of the buildpack by using the **-b** option when you deploy your application to {{site.data.keyword.Bluemix_notm}} from the command prompt.

  * To deploy Liberty server packages to {{site.data.keyword.Bluemix_notm}}, use the following command from your source directory:

  ```
  cf push
  ```

  For more information about Liberty Buildpack, see [Liberty for Java](/docs/runtimes/liberty/index.html).

  * To deploy Java Tomcat applications to {{site.data.keyword.Bluemix_notm}}, use the following command:

  ```
  cf push appname -b https://github.com/cloudfoundry/java-buildpack.git -p app_path
  ```

  * To deploy WAR packages to {{site.data.keyword.Bluemix_notm}}, use the following command:

  ```
  cf push appname -p app.war
  ```
  Or, you can specify a directory that contains your application files by using the following command:

  ```
  cf push appname -p "./app"
  ```

  * To deploy Node.js applications to {{site.data.keyword.Bluemix_notm}}, use the following command:

  ```
  cf push appname -p app_path
  ```

A `package.json` file must be in your Node.js application for the application to be recognized by the Node.js buildpack. The `app.js` file is the entry script for the application, and can be specified in the `package.json` file. The following example shows a simple `package.json` file:

  ```
  {
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": ">=3.4.7 <4",
                "jade": ">=1.1.4"
        },
        "scripts": {
                "start": "node app.js"
        },
        "engines": {
                "node": ">=0.10.0"
        },
        "repository": {}
  }
  ```

  For more information about the `package.json` file, see [package.json](https://www.npmjs.org/doc/files/package.json.html){:new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").

  * To deploy PHP, Ruby, or Python applications to {{site.data.keyword.Bluemix_notm}}, use the following command from the directory that contains your application source:

  ```
  cf push appname
  ```

### Deploying an app in multiple spaces

An app is specific to the space where it is deployed. You can't move or copy an app from one space to another in {{site.data.keyword.Bluemix_notm}}. To deploy an app in multiple spaces, you must deploy your app in each space where you want to use the app by the following steps:

  1. Switch to the space where you want to deploy your app by using the **cf target** command with the **-s** option:

  ```
  cf target -s <space_name>
  ```

  2. Go to your app directory and deploy your app by using the **cf push** command, where appname must be unique within your domain.

  ```
  cf push appname
  ```
