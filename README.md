# How to debug Java EE applications running in Bluemix from Eclipse IDE 

<br/>

## Requirements

Before we can start, make sure the following preconditions are fulfilled:

* You have already installed the latest "Oxygen" release of Eclipse IDE for Java EE (if not, get it <a href="https://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/oxygenr">here</a>)

* You have a valid IBM Bluemix account (if not, create your test account <a href="https://www.ibm.com/cloud-computing/bluemix/">here</a>)

* You have installed the Cloud Foundry CLI (if not, download from <a href="https://github.com/cloudfoundry/cli">here</a>)

<br/>

## Boosting Eclipse for Bluemix development

For being able to connect with Bluemix from within Eclipse, we need to install a corresponding plugin at first. To search for plugins in Eclipse, go to _Help_ in the menu bar and navigate to _Eclipse Marketplace_. You should then see a window where you can search for available plugins. Typing "bluemix" and start searching should offer you the _IBM Eclipse Tools for Bluemix for Oxygen_ plugin. 

<br/>
<p align="center">
  <img src="https://github.com/dev4cloud/bluemix-remote-debugging/blob/master/graphics/bluemix-plugin.png" width=454 height=586>
</p>

<br/>

Click _Install_, accept the license terms as well as the pre-selected packages and finally restart Eclipse after a successful installation process.

<br/>

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

Given that your login has been successful, a new "IBM Bluemix" entry should appear in the _Servers_ tab of Eclipse. You can expand the entry and see all the services you have currently deployed in Bluemix.

<br/>

<p align="center">
  <img src="https://github.com/dev4cloud/bluemix-remote-debugging/blob/master/graphics/eclipse-bluemix-4.png" width=600 height=200>
</p>

<br/>


## Import demo application into Eclipse IDE

Next, we need a demo application that we can ship to Bluemix in order to test remote debugging. If you haven't done this yet, move over to the _dev4cloud/hangman-app_ repository and clone it to your local machine. You can either use the Git CLI or clone the repository directly from within Eclipse. 
Let's assume you directly used the Git CLI to get a copy of the hangman app. As the next step, the project must be imported into Eclipse. To do so, navigate to _File > Import_ and select _Existing Projects into Workspace_. 

<br/>

<p align="center">
  <img src="https://github.com/dev4cloud/bluemix-remote-debugging/blob/master/graphics/eclipse-project-import-1.png" width=525 height=550>
</p>

<br/>

Then, hit _Next_ and browse to the root directory of your recently cloned hangman app repo. Keep the defaults of the remaining settings and press the _Finish_ button. The hangman app should now appear in the Eclipse project explorer. 
In order to check if your Eclipse project setup is correct, right-click the "IBM Bluemix" entry in the _Servers_ tab in Eclipse and select _Add and Remove..._ from the context menu. This will give you a window showing which applications are currently deployed to Bluemix or rather which projects in your workspace are ready to get deployed. If your hangman app is listed under the _Available_ section, then everything is fine and you can skip the next section. 

<br/>

<p align="center">
  <img src="https://github.com/dev4cloud/bluemix-remote-debugging/blob/master/graphics/eclipse-bluemix-deployment-1.png" width=525 height=550>
</p>

<br/>


## <a name="fix"></a>Fixing the Eclipse project preferences

In case the freshly imported hangman app project does not appear in the list, this is due to a misconfiguration of the project preferences in Eclipse. However, this can be fixed by slightly tweaking these settings. 
Make sure that the app is selected and navigate to _Project > Properties_ from the menu bar. In the popup, search for the _Project Facets_ entry and click it. You should see that the checkbox for _Dynamic Web Module_ is deselected, which is the reason why the project is not considered "available" by the Bluemix plugin. 

<br/>

<p align="center">
  <img src="https://github.com/dev4cloud/bluemix-remote-debugging/blob/master/graphics/eclipse-project-import-4.png" width=500 height=340>
</p>

<br/>

Activate the checkbox and make also sure that the _Java_ facet is also selected and its version is 1.7 (this is also marked as "required" by the _Dynamic Web Module_ facet). Otherwise, Eclipse will start throwing weird exceptions and error messages. As soon as you're finished, the hangman app should now be recognized correctly by the Bluemix plugin.       

<br/>

## Ant build configuration

The hangman app relies on the _Ant_ tool for build configuration. Since Eclipse for Java EE IDE comes with Ant support by default, setting up the Ant build is fairly simple. Just click on the arrow  to the right of the _External Tools_ button and move on to _External Tool Configurations_. This should give you a pre-configured Ant run configuration based on the hangman project's _build.xml_ file. This configuration was created by Eclipse, which recognized the project as an Ant project due to the _build.xml_ file in the root directory. Selecting the _Targets_ tab shows a list of all Ant targets defined in the _build.xml_ file. 

<br/>

<p align="center">
  <img src="https://github.com/dev4cloud/bluemix-remote-debugging/blob/master/graphics/eclipse-project-import-2.png" width=500 height=350>
</p>

<br/>


The _build_ target should already be checked, which is perfectly ok for us. This target compiles the code and packages up the application within a WAR archive, which can be deployed on an application server. Click _Run_ and watch the output of the build process in the _Console_ tab. The following screenshot shows the output messages of a successful build.  

<br/>

<p align="center">
  <img src="https://github.com/dev4cloud/bluemix-remote-debugging/blob/master/graphics/eclipse-project-import-3.png">
</p>

<br/>


## Deploying the hangman app to Bluemix

The final step before we can start a remote debugging session is transferring the hangman application to Bluemix and launch it there. It is assumed that at this point, the configured Bluemix server has recognized your hangman Eclipse project as ready for being deployed to Bluemix (if not, go back to [this](#fix) section). 
Right-click the Bluemix server in the Eclipse _Servers_ tab and go to _Add and Remove..._ as you did before. The hangman app, which is now listed on the left side as available for deployment to Bluemix, can easily be transferred to Bluemix by highlighting it and clicking on _Add >_ afterwards. You can track the deployment process by watching the console output.

<br/>

<p align="center">
  <img src="https://github.com/dev4cloud/bluemix-remote-debugging/blob/master/graphics/eclipse-bluemix-deployment-2.png" width=525 height=550>
</p>

<br/>


The current state of your deployment is also visible in your Bluemix console. You should see that a new application appears under _Cloud Foundry Apps_ whose state should finally go to green and "Running" once the deployment has finished and the hangman app is ready.

<br/>

<p align="center">
  <img src="https://github.com/dev4cloud/bluemix-remote-debugging/blob/master/graphics/eclipse-bluemix-deployment-4.png" width=930 height=180>
</p>

<br/>


## Starting a remote debugging session

We're now all set to finally give remote debugging with Eclipse and Bluemix a try. 


