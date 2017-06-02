---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-11"
---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Migrating apps to Diego

Diego is the default Cloud Foundry architecture for {{site.data.keyword.Bluemix_notm}}, and support for DEAs will be removed, so you must migrate all of your existing applications by updating each app. 
{:shortdesc}

Start migrating your apps to Diego by updating the application with the Diego flag. The application immediately attempts to start running on Diego and stops running on the DEAs.

As your application is updated from DEA architecture to Diego, you might experience a short downtime, or a prolonged downtime, if the application is not compatible with Diego. To limit downtime, perform a [blue-green deploy](/docs/manageapps/updapps.html#blue_green) by deploying a copy of your application to Diego, and then swapping routes and scaling down the DEA application.

Complete the following steps to migrate your app to Diego:

 1.  Install both the [cf CLI ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/cloudfoundry/cli/releases){: new_window} and the [Diego-Enabler CLI Plugin ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/cloudfoundry-incubator/Diego-Enabler){:new_window}.
 2. Review the [known issues list](depapps.html#knownissues).
 3. Set the Diego flag to change your app to running on Diego:
  ```
  $ cf enable-diego APPLICATION_NAME
  ```

After you update your app, verify that your app started and is working as expected. If you cannot access your app right away, you might need to try again later. If your migrated app fails to start, it will remain offline until you identify and resolve the issue, and then restart the app.

IBM will alert you of the upcoming mandatory migration period when DEA architecture support will be removed, and if you have not migrated your apps, the operations team will migrate all apps for you.

To validate which backend the application is running on, use the following command:

  ```
  $ cf has-diego-enabled APPLICATION_NAME
  ```

## Diego migration known issues
{: #knownissues}

There are the following known issues that you might need to address when migrating your apps to Diego:

  * Worker applications deployed with the `--no-route` option do not report as healthy. To prevent this, disable the port-based health check with the `cf set-health-check APP_NAME none` command.
  * The **cf files** command is no longer supported. The replacement is the **cf ssh** command. For more details on the **cf ssh** command, see [cf ssh](/docs/cli/reference/cfcommands/index.html#cf_ssh).
  * Some apps might use a high number of file descriptors (inodes). If you encounter this issue, you must increase disk quota for your app with the `cf scale APP_NAME [-k DISK]` command.

For the comprehensive list of known issues, see the Cloud Foundry documentation page for [Migrating to Diego ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/cloudfoundry/diego-design-notes/blob/master/migrating-to-diego.md){: new_window}.

## Rolling back to DEAs
{: #rollbackdea}

Until support for the older DEA architecture is removed, you can run the following command to transition back to DEAs: `cf disable-diego APPLICATION_NAME`. You can also still deploy apps to the DEA architecture until support is removed.

**Note**: You must have both the [cf CLI ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/cloudfoundry/cli/releases){: new_window} and the [Diego-Enabler CLI Plugin ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/cloudfoundry-incubator/Diego-Enabler){:new_window} installed to use the `disable-diego` command.

1. Deploy the application without starting it:
```
$ cf push APPLICATION_NAME --no-start
```
2. Run the disable-diego command:
```
$ cf disable-diego APPLICATION_NAME
```
3. Start the application:
```
$ cf start APPLICATION_NAME
```
