# bluemix-remote-debugging

Detailed introduction to remote debugging Java EE applications in Bluemix.

## Requirements

Before we can start, make sure the following preconditions are fulfilled:

* You have already installed the latest "Oxygen" release of Eclipse IDE for Java EE (if not, get it <a href="https://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/oxygenr">here</a>)

* You have a valid IBM Bluemix account (if not, create your test account <a href="https://www.ibm.com/cloud-computing/bluemix/">here</a>)

* You have installed the Cloud Foundry CLI (if not, download from <a href="https://github.com/cloudfoundry/cli">here</a>)


## Boosting Eclipse for Bluemix development

For being able to connect with Bluemix from within Eclipse, we need to install a corresponding plugin at first. To search for plugins in Eclipse, go to _Help_ in the menu bar and navigate to _Eclipse Marketplace_. You should then see a window where you can search for available plugins. Typing "bluemix" and start searching should offer you the _IBM Eclipse Tools for Bluemix for Oxygen_ plugin. 

<br/>
<p align="center">
  <img src="https://github.com/dev4cloud/bluemix-remote-debugging/blob/master/graphics/bluemix-plugin.png" width=454 height=586>
</p>

Click _Install_, accept the license terms as well as the pre-selected packages and finally restart Eclipse after a successful installation process.


## Connecting Eclipse to your Bluemix account

Now that we have Bluemix support enabled in Eclipse, the next step is to login into your Bluemix account. From the menu bar, go to _File >  New > Other_ and search for server in the window that shows up. Select the _Server_ entry and hit _Next_. That should give you another window where you can choose the type of server you want to create. Open up the _IBM_ folder that should be present and you should see an entry labeled with _IBM Bluemix_. Because this is what we want, select the entry and click _Next_.

<br/>
<p align="center">
  <img src="https://github.com/dev4cloud/bluemix-remote-debugging/blob/master/graphics/eclipse-bluemix-1.png" width=454 height=586>
</p>
<br/>

Now you're prompted to provide your Bluemix credentials. Besides, make sure you select the correct Bluemix region before you continue. Otherwise your login might fail. As soon as you're done, press _Finish_.

<br/>
<p align="center">
  <img src="https://github.com/dev4cloud/bluemix-remote-debugging/blob/master/graphics/eclipse-bluemix-2.png" width=454 height=586>
</p>
<br/>


