# Pitstop engineering workshop
This document describes an engineering workshop that can be used for training .NET engineers and getting them up to speed on several cloud-native software-architecture aspects and how to develop and run software using containerization technologies like Docker and Kubernetes.

In most workshops you start from scratch, but in this workshop you will actually start with a complete working solution called Pitstop. You will learn by executing several labs in which you will be adding functionality to the solution.

Pitstop is an open-source .NET Core sample application that demonstrates the following software-architecture aspects:

- Microservices
- Event-driven architecture
- Domain Driven Design
- Onion architecture
- CQRS
- Event-sourcing

Also, Pitstop demonstrates how to develop and deploy applications using several deployment technologies:

- Docker
- Docker-compose
- Kubernetes
- Service-mesh (Istio & Linkerd)

# Labs
In order to complete the labs, make sure you read (at least) the following sections of the [Pitstop wiki on Github](https://github.com/EdwinVW/pitstop/wiki):

- [Start page](https://github.com/EdwinVW/pitstop/wiki/Home)
- [Application functionality](https://github.com/EdwinVW/pitstop/wiki/Application%20functionality)
- [Domain description](https://github.com/EdwinVW/pitstop/wiki/Domain%20description)
- [Solution architecture](https://github.com/EdwinVW/pitstop/wiki/Solution%20Architecture)
- [Technology used](https://github.com/EdwinVW/pitstop/wiki/Technology%20used)

By now, you should have some understanding of what the Pitstop solution contains and what functionality it offers. Next you will execute several lab assignments in which you will add stuff to the Pitstop solution.

## Lab 0: Preparation
There are some prerequisites for this workshop. First you need an active Internet connection. Additionally you will need to install the following software on your laptop:

- Docker Community Edition (CE)
- Visual Studio Code
- .NET Core SDK
- (optional) Git client

>If you already have satisfied these prerequisites, you can skip Lab 0 and go directly to Lab 1. 

### Step 0.1: Install prerequisites
Install the following software (if not already installed) on your laptop: 

#### Docker CE
Download link: <a href="https://docs.docker.com/install" target="_blank">Docker Community Edition (CE)</a>. 

On Windows, you need Hyper-V to be enabled on your machine in order to install Docker for Windows CE. If you have not enabled Hyper-V, do so now. <a href="https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v" target="_blank">Here</a> you find a description of how to enable Hyper-V on Windows. Make sure to double-check the prerequisites.

For downloading Docker CE, you need to login with your Docker Id. Create one if you don't already have a Docker Id. 

During the installation of Docker CE, do not switch to Windows containers. We will only use Linux containers. After the installation you need to log out and login again (sometimes reboot your machine).

After the installation, start the Docker engine by double clicking the Docker for Windows icon. 

#### Visual Studio Code
This workshop assumes you are working with Visual Studio Code. 

Download link: <a href="https://visualstudio.microsoft.com/downloads" target="_blank">Visual Studio Code</a>

#### .NET Core SDK
Install the .NET Core SDK version 3.0. 

Download link: <a href="https://www.microsoft.com/net/download" target="_blank">.NET Core SDK</a>

#### Git client
Install the Git client for your OS to interact with the Pitstop repo on Github. 

Download link: <a href="https://git-scm.com/downloads" target="_blank">Git</a> 

### Step 0.2: Access Github
If you do not already have a Github account, create one by going to the <a href="https://www.github.com" target="_blank">Github website</a> and click on the *Sign up* link in the top right corner. Make sure you are logged into Github with your account. 

## Lab 1: Run the applicaton
In this lab we'll make sure you can run Pitstop on your machine. 

### Step 1.1: Get the sources
Get the sources from Github onto your machine.

For this to work, you must have installed the Git client (see Step 0.1). 
1. Open your browser and navigate to the Pitstop repo on Github: <a href="https://github.com/edwinvw/pitstop" target="_blank">https://github.com/edwinvw/pitstop</a>. 
2. Click the *Fork* button.
3. The repo is forked to your Github account. If you have multiple accounts, Github will ask which account to fork to.
4. Click the green *Clone or download* button on the forked repo. A dialog is shown.
5. Copy the repo URL to the clipboard. 
6. Open Visual Studio Code on your machine.
7. Give the clone repo command by pressing `CTRL-Shift-P`, typing `Git Clone` and pressing `enter` to confirm. You will be asked to specify a repo URL.
8. Paste the copied repo URL in the text-box and press `enter` to confirm.
9. You will be asked to specify a folder for cloning the repo into. Select a folder and confirm. The repo will be cloned in this folder.
10. When VS Code asks you to open the cloned repo, do that. Now you can start working with the repo.

This would be a good time to walk through the solution and see what's in there. In the <a href="https://github.com/EdwinVW/pitstop/wiki" target="_blank">Wiki</a> of the repo, you can find an overview of the solution structure. 

### Step 1.2: Build the Docker images
In order to build the Docker images, follow the instructions in the <a href="https://github.com/EdwinVW/pitstop/wiki/Building%20the%20Docker%20images" target="_blank">'Building the Docker images' section</a> in the repo's Wiki.

### Step 1.3: Run the application
In order to run the application, follow the instructions in the <a href="https://github.com/EdwinVW/pitstop/wiki/Run%20the%20application%20using%20using%20Docker%20Compose" target="_blank">'Starting the application' section</a> in the repo's Wiki.

### Step 1.4: Get to know the solution
In order to get to know the functionality of the application, make sure you have read the introduction of the solution in the repo's README file up to the *Technology* section. After that, follow the <a href="https://github.com/EdwinVW/pitstop/wiki/Testing%20the%20application" target="_blank">'Testing the application' section</a> in the repo's Wiki. 

## Lab 2: ATDD with Specflow and Augurk
The Pitstop solution does not contain any specifications or scenario-tests. It's up to you to add this to the solution. We will primarily focus on the *WorkshopManagement* domain because this is the domain with the most interesting business-logic.

1. Add [specflow](https://specflow.org/) to the *WorkshopManagementAPI*.
2. Write specflow feature files for the functionality in this domain.
3. Write scenario-tests based on the feature-files that test the domain's functionality.
4. Setup [Augurk](https://github.com/Augurk/Augurk) for the project so that you are able to see living documentation for the *WorkshopManagement* domain based on the feature files.

## Lab 3: Add an event-handler for customer events
When something happens within the Pitstop application that could be interesting for other parts of the system, an event is published to the message-broker. For instance: when a new customer is registered, a *CustomerRegistered* event is published. 

In this lab you will add a service to the solution that will react to customer events. What we will do when the event is received is up to your imagination. For the workshop, we will keep it simple and just dump a message on the console. 

The service we will build offers no API and can therefore be a simple console application (just as the existing *NotificationService* for instance). 

### Step 3.1: Create the .NET Core application
First we will add a new service to the solution. 

1. Open a command-prompt or Powershell window.
2. Make sure you are in the `src` folder within the Pitstop repository.
3. Use the `dotnet new` command to create a new .NET Core console application named *CustomerEventHandler*:
   ```
   dotnet new console -o CustomerEventHandler
   ```
   The output should look something like this:

   ![](img/dotnet-new-customereventhandler.png)

A new *CustomerEventHandler* folder will be created which contains a .NET Core project. Because the created project-type is a console application, the folder will only contain a project file (*CustomerEventHandler.csproj*) and a main program file (*Program.cs*). The default implementation generated by `dotnet new` is printing *'Hello World!'* to the console.

You can test the application by running it:

```
cd CustomerEventHandler
dotnet run
```

The output should look like this:

![](img/dotnet-run-customereventhandler.png)

### Step 3.2: Create event-handler
Now that you've added a new .NET Core project to the solution, you can start implementing the business logic of the service. As stated, the 'business logic' will be fairly simple for this workshop.

**Open the project in VS Code**
Let's open Visual Studio Code to start coding:

1. Start Visual Studio Code.
2. Select *File*, *Open Folder* and select the *CustomerEventHandler* folder you created in step 3.1. 
   >Visual Studio Code might show you some dialogs about plugins that you can install. For now, just install all plugins that it suggests. It will also asks you to add some 'assets' it needs for building and debugging the project. Acknowledge this with 'Yes'. This will create a '.vscode' folder. You can ignore that folder for now.
   
3. Open the file *CustomerEventHandler.csproj* by double-clicking on it. This is the file that describes the project. It is pretty straightforward and clean.
4. Start the application by pressing `F5`. The project will be built and started. You can see the output in the 'DEBUG CONSOLE' window that was automatically opened.

**Add reference to the infrastructure package**
The CustomerEventHandler service will need to receive messages from the message-broker. I have created a nuget package (*Pitstop.Infrastructure*) that contains a library that will make it easy to implement this without any specific knowledge about RabbitMQ (the broker that is used in the solution). 

You need to add a reference to the *Pitstop.Infrastructure.Messaging* nuget package. Execute the following steps to add a reference to the package: 

1. Open the terminal window in Visual Studio Code using the *Terminal* menu.
2. Type the following command in this window: `dotnet add package PitStop.Infrastructure.Messaging`. 
3. Visual Studio Code will detect changes in the references and automatically restore the references.

**Add event definition**
Now you can start adding some business logic. First you need to add the definition of the events you want to handle. All messages that are sent over the message-broker are plain JSON. The *CustomerRegistered* event is defined as follows:

```json
{
	"messageId": "guid",
	"messageType": "string",
	"customerId" : "string",
	"name": "string",
	"address": "string",
	"postalCode": "string",
	"city": "string",
	"telephoneNumber": "string",
	"emailAddress": "string"
}
```

You need to define a C# class to hold this information. We will only use the *customer id* and *name* properties in our code, so in your event-definition you can skip the other customer properties.

The infrastructure package you referenced in the previous step contains an *Event* base-class for events. This class inherits from the *Message* base-class which contains the *MessageId* and *MessageType* properties (the message-type is inferred from the name of the class).

1. Add a new *CustomerRegistered* class to your project.
2. Derive this class from the Event base-class in the *Pitstop.Infrastructure.Messaging* library.
2. Add the implementation of the event-class that only contains the *customerId* and *name* property of the customer.

**Add a *CustomerManager* class that handles events**
Now that you have a definition of the event, you will add a *CustomerManager* class that will get the events from the message-broker and handles them. The polling for messages and the handling of a message when it's available are abstracted in two separate interfaces: *IMessageHandler* and *IMessageHandlerCallback*. They are both defined in the infrastructure package.  

The *IMessageHandler* interface abstracts the polling for messages on a message-broker. An implementation of this interface will be passed into your *CustomerManager*'s constructor. The infrastructure package also contains an implementation of this interface that works with RabbitMQ. 

When you want to start listening for messages, you have to call the *Start()* method on this interface and pass in an implementation of the *IMessageHhandlerCallback* interface. The *HandleMessageAync()* method is called on the callback implementation when a message is available on the message-broker. The *CustomerManager* will implement this interface and handle the events.

This is a class diagram of this pattern:
![](img/messaging-cd.png)
 
1. Add a new *CustomerManager* class to your project.
2. Add the implementation that handles *CustomerRegistered* messages. You can reference other event-handlers (e.g. *AuditlogService*) for inspiration.

**Start the customermanager**
Now that you created a *CustomerManager* that can handle *CustomerRegistered* events, you need to start this manager form the main program. You will use the *RabbitMQMessageHandler* class from the infrastructure package to pass into the *CustomerManager*. 

1. Open the *Program.cs* file in the project.
2. Replace the existing code with the necessary code to setup and start the event-handler. You can reference other event-handlers (e.g. *AuditlogService*) for inspiration.

**Build the code**
In order to check whether or not you made any mistakes until now, build the code. Do this by pressing `Ctrl-Shift-B` in Visual Studio Code and choosing the task *Build*. The output window should look like this:

![](img/vscode-build.png) 

### Step 3.3: Run the service
We can start the *CustomerEventHandler* to test whether or not it works. 

1. Make sure you have the Pitstop application running on your machine (as described in Step 1.3: Run the application).
2. Open a command prompt or Powershell window and go to the *CustomerEventHandler* folder.
3. Start the application by giving the following command: `dotnet run`.
4. Open the browser and go to http://localhost:7000 to open the Pitstop web-app.
5. Go to the *Customer Management* tab and register a new customer.

Watch the output window of your *CustomerEventHandler*. You should see that a message is printed to the console, something like this:

![](img/dotnet-run-customereventhandler-broker.png) 

That's it! You have now created a new service that can react on events emitted by the services in the Pitstop solution. Pretty sweet!

### Step 3.4: Create Docker image
Now that you have created a functional service, let's run it in a Docker container.

1. Add a new file to the project named *Dockerfile*.
2. Copy the contents of the dockerfile of the *AuditlogService* and make sure it starts the CustomerEventHandler (in the ENTRYPOINT statement).

> Please take some time to go over the Dockerfile now. You see an example of the Docker multi-stage build mechanism. 
> - First it starts in a container that is based on an image that contains the full .NET Core SDK (*mcr.microsoft.com/dotnet/core/sdk:3.0*). We call this *build-env* for later reference.
> - After that it sets the folder */app* as the current working-folder for the build. It copies the *.csproj* file of your project into to the working-folder. 
> - Then it restores all the dependencies by running `dotnet restore`. 
> - After the restore, it copies the rest of the files to the working-folder and publishes the application by running `dotnet publish -c Release -o out`. It builds the *Release* configuration and outputs the result in the folder *out* within the working-folder.
> - Now it starts the second phase which runs in a container based on the .NET Core run-time container (*mcr.microsoft.com/dotnet/core/runtime:3.0*). This container does not contain the entire .NET Core SDK - so it's much smaller.
> - It then copies the output from the other build phase (that was called *build-env*) to the local folder within the container.
> - Finally it specifies the entry-point - the command to execute when the container starts. In this case it specifies the command `dotnet` and as argument the assembly that was created during the build. This will start the *CustomerEventHandler* console application you've created.

Now you are going to build a Docker image using the Dockerfile.

1. Open a command prompt or Powershell window and go to the *CustomerEventHandler* folder.
2. Build a Docker image by entering the following command: 

	`docker build --rm -t pitstop/customereventhandler:1.0 .`

   > You specify the name of the image using the *Tag* option (`-t`).
3. Check whether the image is created by entering the following command: `docker images`:

   ![](img/docker-images.png)

### Step 3.5: Run the service in a Docker container
Now that you have the Docker image, you can start a container based on this image. 

1. Run a Docker container based on the image by entering the following command:

	`docker run -it --rm --network src_default --name customereventhandler pitstop/customereventhandler:1.0`

   >In this command you specify the virtual network to connect with. In this case we specify the name of the default network that was created by docker-compose when we started the solution (*src_default*). By doing this, the container can find and access the RabbitMQ server that is running in a separate Docker container on the virtual network.
2. Open the browser and go to http://localhost:7000 to open the Pitstop web-app.
3. Go to the *Customer Management* tab and register a new customer.

Watch the output of your running container. You should see that message again that indicates that a customer was registered:

![](img/docker-run.png)

**Before you continue, stop the running container by pressing `Ctrl-C`.**

### Step 3.6: Run the service using docker-compose
The last step in this lab is to extend the docker-compose file to include your service. 

1. Open the *docker-compose* file in the *src* folder of the Pitstop repo in Visual Studio Code.
2. Add this snippet to the *docker-compose* file just before the webapp part:
 
   ```
     customereventhandler:
       image: pitstop/customereventhandler:1.0
       build: CustomerEventHandler
       container_name: CustomerEventHandler
       depends_on:
         - rabbitmq
       environment:
         - DOTNET_ENVIRONMENT=Production    
   ```
3. Save the file.
4. Open the Powershell window where you started the solution using `docker-compose up`.
5. Stop the running solution by pressing `Ctrl-C` and wait until all the containers are stopped.
6. Restart the solution by giving the command: `docker-compose up`. The *CustomerEventHandler* will be started together with all the other services.
2. Open the browser and go to http://localhost:7000 to open the Pitstop web-app.
3. Go to the *Customer Management* tab and register a new customer.

Watch the docker-compose logging in the console. You should see that message again that indicates that a customer was registered:

![](img/docker-compose-output.png)

>The following labs are more advanced labs you can do on your own if you're done with the first two labs. There's no extensive description on how to complete these labs, only a description of the required outcome. It's up to you to figure out the best way to implement these requirements. 

## Lab 3 - Add update functionality to Pitstop
The current version of Pitstop only supports adding customers, vehicles and maintenance jobs. There is no way to update these. In this lab you have to add support for updating the data of customers, vehicles and maintenance jobs.

1. Add Specflow features for this new functionality.
2. Write the unit- and specflow-tests for testing this new functionality.
2. Add the requested functionality.
4. Extend the UI-tests with this new functionality.

## Lab 4 - Add Inventory management
During a maintenance job, a mechanic often uses products like: tires, windscreen-wipers, oil, oil-filters, etcetera. There is currently no way to support this in Pitstop. In this lab you have to add the ability for a mechanic to add products that he or she uses during the execution of a maintenance-job. For every product used, the inventory must be updated and the price of the products must be added to the bill that is sent to the customer. 

In the context-map shown in the <a href="https://github.com/EdwinVW/pitstop/wiki/Domain%20description" target="_blank">domain description</a> on the Wiki, Inventory Management is shown (grayed out). Use this information in this assignment. 

1. Add Specflow features for this new functionality.
2. Add an *InventoryManagement* service to the solution that can be used to manage the products in stock. 
3. Write the unit- and specflow-tests for testing this new functionality.
4. Add the requested functionality.
5. Extend the UI-tests with this new functionality.

## Lab 5 - Deploy Pitstop to Azure
Until now, you've ran Pitstop in containers on your local machine. In this lab you will learn how to deploy a microservices application that consists of multiple parts (Pitstop) in Microsoft Azure. In a production scenario, using containers for running the app would be a fine solution. But in order to get you up-to-speed with different Azure services, you're not allowed to host the app in containers (using ACI or AKS).

- Follow the following courses in the Pluralsight library:
	- [AZ-103 - Azure Administrator](https://app.pluralsight.com/paths/certificate/microsoft-azure-administrator-az-103)
	- [AZ-203 - Developing Solutions for Microsoft Azure](https://app.pluralsight.com/paths/certificate/developing-solutions-for-microsoft-azure-az-203)
- Request access to an Azure Subscription by asking approval from your business-unit manager and sending an email to [support@infosupport.com](mailto:support@infosupport.com).
- Make a deployment diagram for deploying Pitstop as-is in Azure. A requirement is that you use Azure PAAS / SAAS services and do not use container-hosting services like ACI or AKS.
- Send the deployment diagram to your suprevisor for review.
- Deploy Pitstop to Azure (and make sure the web-app is publicly available).
- Share a link  to the web-app with your supervisor. 

## Lab 6 - Setup a CI/CD pipeline
Modern applications are built using an automated CI pipeline and deployed using an automated CD pipeline. Azure DevOps is a tool to implement fully automated CI/CD pipelines. There an on-premises version and a cloud version. In this assignment you will setup a CI/CD pipeline for building and deploying Pitstop.  

- Build a CI/CD pipeline in Azure DevOps to do a fully automated deployment of the necessary infrastructure (according to your diagram) for hosting Pitstop in Azure. Hint: use ARM templates. 
- Build a CI/CD pipeline in Azure DevOps to do a fully automated deployment of the Pitstop application on the provisioned infrastructure.

