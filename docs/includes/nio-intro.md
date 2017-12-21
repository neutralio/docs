Hello to a new world of connected intelligence using nio!

This tutorial introduces you to the System Designer and the fundamental concepts of building a nio [project](https://docs.n.io/glossary#project) including how to create
[systems](https://docs.n.io/glossary#system),
[instances](https://docs.n.io/glossary#instance),
[services](https://docs.n.io/glossary#service), and
[blocks](https://docs.n.io/glossary#block).

## Before You Begin

The [**System Designer**](https://docs.n.io/system-designer/) is the graphical user interface used to build your nio system. This video provides you with a quick tour of the System Designer including the navigation, work areas, and toolbars.

{% video %}https://www.youtube.com/watch?v=GFs5EK6zao8{% endvideo %}

## Create a System

The very first time you open the System Designer, you are literally starting with a blank canvas. The canvas is where you will build systems containing instances, services, and blocks. To begin, create a system named `workshops` that will contain the projects you create as you learn to use nio.

1. Open the **System Designer** in a new tab in your browser.

  https://designer.n.io/

1. You can create a new system in two ways.
  * If this is your first time opening nio, the **create new system** window displays.

    %accordion%**Click arrow to collapse/expand**%accordion%

    ![](/img/cloud/Hello-CreateNewSystem.png)

    %/accordion%

  * If you have already been working in nio, in the lower-left corner, click the **`+`** button.

    %accordion%**Click arrow to collapse/expand**%accordion%

    ![](/img/cloud/Hello-BlankCanvas.png)

    %/accordion%

1. Complete the **create new system** window:
  1. In the **system name** box, enter `workshops`.
  1. Click **accept**.

Way to go! You just created a [system](https://docs.n.io/glossary#system) to hold the projects you will build in these tutorials. Your canvas has expanded to include the contextual toolbar and you are currently in the system context. The next step is to create a cloud [instance](https://docs.n.io/glossary#instance) within your newly created system.

## Create an Instance
An [instance](https://docs.n.io/glossary#instance) is an installation of nio that you are running. It is possible to have multiple instances  (both cloud and local) running in a system and multiple services in an instance.

A cloud instance runs a version of nio that is installed in the cloud and managed by niolabs. You will create a cloud instance named `Tutorials` to hold the services that you will create in these tutorials.

1. Click **create cloud instance**.

  %accordion%**Click arrow to collapse/expand**%accordion%

  ![](/img/cloud/Hello-Create-Cloud-Instance.png)

  %/accordion%

1. Complete the **create cloud instance** window.

  %accordion%**Click arrow to collapse/expand**%accordion%

  ![](/img/cloud/Hello-CreateCloudInstance.png)

  %/accordion%

  1. In the **instance name** box, enter `Tutorials`.
  1. Click **accept**.

Alright! You just created a cloud [instance](https://docs.n.io/glossary#instance) of nio. Your contextual toolbar now shows you the instance context where you can view and edit your instance. You can create all of your [services](https://docs.n.io/glossary#service) for the tutorials within this cloud instance. In the next step you will learn how to make your first service.

## Create a Service
A service is a real-time process that runs on an instance. It is a collection of blocks that perform a service. Now you can create a simple `simulate-and-log` service that will generate a signal and log it to the logger panel.

1. Click **create new service**.

  %accordion%**Click arrow to collapse/expand**%accordion%

  ![](/img/cloud/Hello-Create-New-Service.png)

  %/accordion%

1. Complete the **create new service** window.

  %accordion%**Click arrow to collapse/expand**%accordion%

  ![](/img/cloud/Hello-CreateNewService.png)

  %/accordion%
  1. In the **service name** box, enter `simulate-and-log`.
  1. Click **accept**.

You’re cruising now! You just created your first [service](https://docs.n.io/glossary#service). Notice that the block library appeared on the right side of your canvas and your contextual toolbar now has you in the service context where you can edit, save, and start and stop your service. The service will hold the logic created by a workflow of [blocks](https://docs.n.io/glossary#block). In the next step, you will use the block library to add blocks to your service.

## Add Blocks

The blocks are the units that do the work inside a service.

The basic `simulate-and-log` service needs two blocks:
  The _CounterIntervalSimulator_ block to simulate and emit a [signal](https://docs.n.io/glossary/#signal) at a specified interval, and the _Logger_ block to log each incoming signal to the logger panel.

| Block Type           | Block Name                |
|----------------------|---------------------------|
| [CounterIntervalSimulator](https://blocks.n.io/CounterIntervalSimulator) | Simulate |
| [Logger](https://blocks.n.io/Logger) | Log       |

1. In the **block library** search box, enter `CounterIntervalSimulator`.

  %accordion%**Click arrow to collapse/expand**%accordion%

  ![](/img/cloud/Hello-SearchCISBlock.png)

  %/accordion%

1. Drag the *CounterIntervalSimulator* block type to the canvas.
1. In the **block name** box, enter `Simulate` and click **accept**.

  %accordion%**Click arrow to collapse/expand**%accordion%

  ![](/img/cloud/Hello-CreateBlockSimulate.png)

  %/accordion%
1. In the **block library** search box, enter `Logger`.
1. Drag the *Logger* block type to the canvas.
1. In the **block name** box, enter `Log` and click **accept**.

  %accordion%**Click arrow to collapse/expand**%accordion%

  ![](/img/cloud/Hello-Blockname-Log.png)

  %/accordion%

To learn about all the blocks nio has to offer, visit [https://blocks.n.io](https://blocks.n.io).

Way to go! You are now familiar with how to add blocks to your nio service! The first block simulates data and the second block logs that data to the logger panel.

## Connect the Blocks
To do their work, the two blocks on your canvas need to communicate. In nio, signals are is passed between blocks via their terminals. A terminal is shown as a blue circle on the top or bottom of a block. Signals are emitted from an output terminal on the bottom of a block and received by an input terminal on top of a block. The lines connecting the terminals configure the route the signal will take. Once a signal is emitted from one block, the next block(s) in the route will receive it.

1. Click and drag the output terminal of the **Simulate** block and release the connector on the input terminal of the **Log**  block.

  %accordion%**Click arrow to collapse/expand**%accordion%

  ![](/img/cloud/Hello-ConnectAndSaveBlocks.png)

  %/accordion%
1. Click anywhere on the canvas to ensure you have deselected the blocks and returned to the service context.
1. Click **save** on the contextual toolbar to save your service with its new block connections.

>**[info] Disconnecting Blocks**
>
>To disconnect two blocks, click the input terminal of the receiving block, then drag and release the connector anywhere on the canvas.

Now that you connected the two blocks, your service is fully functional.

## Run Service
Start your service to see the simulated signals log to the logger panel.

1. Click **start** (![](/img/cloud/Start.png)) on the contextual toolbar.
1. Click **open logger panel** to view the logs of the signal created by the counter interval simulator.

  %accordion%**Click arrow to collapse/expand**%accordion%

  ![](/img/cloud/Hello-SimLogger.png)

  %/accordion%

Congratulations! You just learned the basics of using the nio Platform with the **System Designer**.

You created a signal in one block and sent it to another block to be logged and visualized.

To nio, all data is a signal whether it is received from a simulator, an API, a hardware sensor, or a database. You just need to select the appropriate block to access your particular data source. Integrating a new data source is as simple as dragging a new block to your canvas.

Similarly, the logger screen is just one easy way to visualize the output of a service, but signals can be visualized in many other ways by using different blocks. For example, if you want to see outputs in a tweet, add and configure the Twitter block, or if you wanted to receive outputs in a text message, add and configure a Twilio block.

If the output doesn’t need to be visualized, the signals can be sent to other services by way of a publisher block, or to a database with a database block.

You can browse all of the available blocks at http://blocks.n.io. Feel free to make more services by connecting blocks to perform various tasks on your own.

If you would like to explore configuring blocks and sharing signals across services and instances, be sure to check out the nio 101 [tutorials](/nio-101/restful-api/README.md) that expand in complexity. As a next step, we recommend exploring the [Distributed Demo](https://workshops.n.io/plant) to better understand the value of distributed computing and how nio can be applied to a real-world application.