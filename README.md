# bluemix-remote-debugging

Detailed introduction to remote debugging Java EE applications in Bluemix.

## Requirements

Before we can start, make sure the following preconditions are fulfilled:

* You have already installed the latest "Oxygen" release of Eclipse IDE for Java EE (if not, get it <a href="https://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/oxygenr">here</a>)

* You have a valid IBM Bluemix account (if not, create your test account <a href="https://www.ibm.com/cloud-computing/bluemix/">here</a>)

* You have installed the Cloud Foundry CLI (if not, download from <a href="https://github.com/cloudfoundry/cli">here</a>)


## Boosting Eclipse for Bluemix development

For being able to connect with Bluemix from within Eclipse, we need to install a corresponding plugin at first. To search for plugins in Eclipse, go to _Help_ in the menu bar and navigate to _Eclipse Marketplace_. You should then see a window where you can search for available plugins. Typing "bluemix" and start searching should offer you the _IBM Eclipse Tools for Bluemix for Oxygen_ plugin. 

<img src="https://github.com/dev4cloud/bluemix-remote-debugging/blob/master/graphics/bluemix-plugin.png">

Click _Install_, accept the license terms as well as the pre-selected packages and finally restart Eclipse after a successful installation process.


4. Server view > "New server"; Navigate to IBM > Bluemix; Click on "next"
5. Type in credentials (valid Bluemix account required); Select region; "Validate account" to check input
