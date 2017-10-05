---
title: Aan de slag met Azure queue storage- en Visual Studio verbonden Services (ASP.NET) | Microsoft Docs
description: Hoe u aan de slag met Azure queue storage in een ASP.NET-project in Visual Studio nadat u een opslagaccount met behulp van Visual Studio verbonden Services
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94ca3413-5497-433f-abbe-836f83a9de72
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/23/2016
ms.author: kraigb
ms.openlocfilehash: 4687e5dfce72583728068c176d86d100313badf6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="ffda8-103">Aan de slag met Azure queue storage- en Visual Studio verbonden Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="ffda8-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="ffda8-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ffda8-104">Overview</span></span>

<span data-ttu-id="ffda8-105">Azure queue storage biedt cloud messaging tussen toepassingsonderdelen.</span><span class="sxs-lookup"><span data-stu-id="ffda8-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="ffda8-106">Bij het ontwerpen van schaalbare toepassingen worden toepassingsonderdelen vaak ontkoppeld, zodat ze onafhankelijk van elkaar kunnen worden geschaald.</span><span class="sxs-lookup"><span data-stu-id="ffda8-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="ffda8-107">Queue Storage biedt asynchrone uitwisseling van berichten voor communicatie tussen toepassingsonderdelen, of deze nu worden uitgevoerd in de cloud, op een desktopcomputer, op een on-premises server of op een mobiel apparaat.</span><span class="sxs-lookup"><span data-stu-id="ffda8-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="ffda8-108">Queue Storage biedt daarnaast ondersteuning voor het beheren van asynchrone taken en het samenstellen van proceswerkstromen.</span><span class="sxs-lookup"><span data-stu-id="ffda8-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="ffda8-109">Deze zelfstudie laat zien hoe ASP.NET code schrijven voor enkele algemene scenario's met Azure queue storage entiteiten.</span><span class="sxs-lookup"><span data-stu-id="ffda8-109">This tutorial shows how to write ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="ffda8-110">Deze scenario's omvatten algemene taken, zoals het maken van een Azure-wachtrij en toevoegen, wijzigen, lezen en verwijderen van Wachtrijberichten.</span><span class="sxs-lookup"><span data-stu-id="ffda8-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="ffda8-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ffda8-111">Prerequisites</span></span>

* [<span data-ttu-id="ffda8-112">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ffda8-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="ffda8-113">Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="ffda8-113">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="ffda8-114">Maken van een MVC-controller</span><span class="sxs-lookup"><span data-stu-id="ffda8-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="ffda8-115">In de **Solution Explorer**, met de rechtermuisknop op **domeincontrollers**, en selecteer in het contextmenu **toevoegen -> Controller**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-115">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![Een domeincontroller toevoegen aan een ASP.NET MVC-app](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="ffda8-117">Op de **Add Scaffold** dialoogvenster Selecteer **MVC 5 Controller - leeg**, en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-117">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Geef een MVC-controller](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="ffda8-119">Op de **Controller toevoegen** dialoogvenster, de naam van de controller *QueuesController*, en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-119">On the **Add Controller** dialog, name the controller *QueuesController*, and select **Add**.</span></span>

    ![De naam van de MVC-controller](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="ffda8-121">Voeg de volgende *met* richtlijnen voor de `QueuesController.cs` bestand:</span><span class="sxs-lookup"><span data-stu-id="ffda8-121">Add the following *using* directives to the `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="ffda8-122">Een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="ffda8-122">Create a queue</span></span>

<span data-ttu-id="ffda8-123">De volgende stappen laten zien hoe een wachtrij maken:</span><span class="sxs-lookup"><span data-stu-id="ffda8-123">The following steps illustrate how to create a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="ffda8-124">Deze sectie wordt ervan uitgegaan dat u de stappen hebt voltooid [de ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="ffda8-124">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="ffda8-125">Open het `QueuesController.cs`-bestand.</span><span class="sxs-lookup"><span data-stu-id="ffda8-125">Open the `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="ffda8-126">Toevoegen van een methode aangeroepen **CreateQueue** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="ffda8-127">Binnen de **CreateQueue** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="ffda8-127">Within the **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ffda8-128">Gebruik de volgende code de verbindingsreeks voor opslag en storage-account-gegevens ophalen uit de configuratie van Azure service: (wijziging  *&lt;storage-account-name >* op de naam van de Azure storage-account u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="ffda8-128">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="ffda8-129">Ophalen van een **CloudQueueClient** object vertegenwoordigt een queue-serviceclient.</span><span class="sxs-lookup"><span data-stu-id="ffda8-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="ffda8-130">Ophalen van een **CloudQueue** -object met een verwijzing naar de naam van de gewenste wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ffda8-130">Get a **CloudQueue** object that represents a reference to the desired queue name.</span></span> <span data-ttu-id="ffda8-131">De **CloudQueueClient.GetQueueReference** methode heeft een aanvraag in voor wachtrijopslag moet fungeren niet maken.</span><span class="sxs-lookup"><span data-stu-id="ffda8-131">The **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="ffda8-132">De verwijzing wordt geretourneerd of de wachtrij bestaat of niet.</span><span class="sxs-lookup"><span data-stu-id="ffda8-132">The reference is returned whether or not the queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="ffda8-133">Roep de **CloudQueue.CreateIfNotExists** methode voor het maken van de wachtrij als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="ffda8-133">Call the **CloudQueue.CreateIfNotExists** method to create the queue if it does not yet exist.</span></span> <span data-ttu-id="ffda8-134">De **CloudQueue.CreateIfNotExists** methode retourneert **true** als de wachtrij niet bestaat en is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ffda8-134">The **CloudQueue.CreateIfNotExists** method returns **true** if the queue does not exist, and is successfully created.</span></span> <span data-ttu-id="ffda8-135">Anders **false** wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ffda8-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="ffda8-136">Update de **ViewBag** met de naam van de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ffda8-136">Update the **ViewBag** with the name of the queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="ffda8-137">In de **Solution Explorer**, vouw de **weergaven** map met de rechtermuisknop op **wachtrijen**, en selecteer in het contextmenu **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-137">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="ffda8-138">Op de **weergave toevoegen** dialoogvenster Voer **CreateQueue** voor de weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-138">On the **Add View** dialog, enter **CreateQueue** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="ffda8-139">Open `CreateQueue.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment:</span><span class="sxs-lookup"><span data-stu-id="ffda8-139">Open `CreateQueue.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="ffda8-140">In de **Solution Explorer**, vouw de **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="ffda8-140">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="ffda8-141">Nadat de laatste **Html.ActionLink**, voeg de volgende **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="ffda8-141">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="ffda8-142">Voer de toepassing en selecteer **wachtrij maken** om vergelijkbaar met de volgende schermopname resultaten te bekijken:</span><span class="sxs-lookup"><span data-stu-id="ffda8-142">Run the application, and select **Create queue** to see results similar to the following screen shot:</span></span>
  
    ![Wachtrij maken](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="ffda8-144">Zoals eerder vermeld de **CloudQueue.CreateIfNotExists** methode retourneert **true** alleen wanneer de wachtrij bestaat niet en is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ffda8-144">As mentioned previously, the **CloudQueue.CreateIfNotExists** method returns **true** only when the queue doesn't exist and is created.</span></span> <span data-ttu-id="ffda8-145">Dus als u de app wordt uitgevoerd wanneer de wachtrij bestaat, de methode retourneert **false**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-145">Therefore, if you run the app when the queue exists, the method returns **false**.</span></span> <span data-ttu-id="ffda8-146">Als u wilt de app meerdere keren uitvoert, moet u de wachtrij verwijderen voordat u de app opnieuw uitvoert.</span><span class="sxs-lookup"><span data-stu-id="ffda8-146">To run the app multiple times, you must delete the queue before running the app again.</span></span> <span data-ttu-id="ffda8-147">Kan het verwijderen van de wachtrij worden uitgevoerd via de **CloudQueue.Delete** methode.</span><span class="sxs-lookup"><span data-stu-id="ffda8-147">Deleting the queue can be done via the **CloudQueue.Delete** method.</span></span> <span data-ttu-id="ffda8-148">U kunt ook verwijderen voor de wachtrij met behulp van de [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) of de [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="ffda8-148">You can also delete the queue using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="ffda8-149">Een bericht toevoegen aan een wachtrij</span><span class="sxs-lookup"><span data-stu-id="ffda8-149">Add a message to a queue</span></span>

<span data-ttu-id="ffda8-150">Zodra u hebt [wachtrij](#create-a-queue), kunt u berichten naar die wachtrij toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ffda8-150">Once you've [created a queue](#create-a-queue), you can add messages to that queue.</span></span> <span data-ttu-id="ffda8-151">Deze sectie helpt u bij het toevoegen van een bericht naar een wachtrij *test wachtrij*.</span><span class="sxs-lookup"><span data-stu-id="ffda8-151">This section walks you through adding a message to a queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="ffda8-152">Deze sectie wordt ervan uitgegaan dat u de stappen hebt voltooid [de ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="ffda8-152">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="ffda8-153">Open het `QueuesController.cs`-bestand.</span><span class="sxs-lookup"><span data-stu-id="ffda8-153">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="ffda8-154">Toevoegen van een methode aangeroepen **AddMessage** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="ffda8-155">Binnen de **AddMessage** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="ffda8-155">Within the **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ffda8-156">Gebruik de volgende code de verbindingsreeks voor opslag en storage-account-gegevens ophalen uit de configuratie van Azure service: (wijziging  *&lt;storage-account-name >* op de naam van de Azure storage-account u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="ffda8-156">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="ffda8-157">Ophalen van een **CloudQueueClient** object vertegenwoordigt een queue-serviceclient.</span><span class="sxs-lookup"><span data-stu-id="ffda8-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="ffda8-158">Ophalen van een **CloudQueueContainer** -object met een verwijzing naar de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ffda8-158">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="ffda8-159">Maak de **CloudQueueMessage** -object dat het bericht dat u wilt toevoegen aan de wachtrij aangeeft.</span><span class="sxs-lookup"><span data-stu-id="ffda8-159">Create the **CloudQueueMessage** object representing the message you want to add to the queue.</span></span> <span data-ttu-id="ffda8-160">Een **CloudQueueMessage** object kan worden gemaakt vanuit een tekenreeks (in UTF-8-indeling) of een byte-matrix.</span><span class="sxs-lookup"><span data-stu-id="ffda8-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="ffda8-161">Roep de **CloudQueue.AddMessage** methode de messaged toevoegen aan de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ffda8-161">Call the **CloudQueue.AddMessage** method to add the messaged to the queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="ffda8-162">Maken en een aantal **ViewBag** eigenschappen voor weergave in de weergave.</span><span class="sxs-lookup"><span data-stu-id="ffda8-162">Create and set a couple of **ViewBag** properties for display in the view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="ffda8-163">In de **Solution Explorer**, vouw de **weergaven** map met de rechtermuisknop op **wachtrijen**, en selecteer in het contextmenu **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-163">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="ffda8-164">Op de **weergave toevoegen** dialoogvenster Voer **AddMessage** voor de weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-164">On the **Add View** dialog, enter **AddMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="ffda8-165">Open `AddMessage.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment:</span><span class="sxs-lookup"><span data-stu-id="ffda8-165">Open `AddMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    The message '@ViewBag.Message' was added to the queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="ffda8-166">In de **Solution Explorer**, vouw de **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="ffda8-166">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="ffda8-167">Nadat de laatste **Html.ActionLink**, voeg de volgende **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="ffda8-167">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="ffda8-168">Voer de toepassing en selecteer **toevoegen bericht** om vergelijkbaar met de volgende schermopname resultaten te bekijken:</span><span class="sxs-lookup"><span data-stu-id="ffda8-168">Run the application, and select **Add message** to see results similar to the following screen shot:</span></span>
  
    ![Bericht toevoegen](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="ffda8-170">De twee secties - [een bericht in een wachtrij lezen zonder het te verwijderen](#read-a-message-from-a-queue-without-removing-it) en [lezen en verwijderen van een bericht van een wachtrij](#read-and-remove-a-message-from-a-queue) -te laten zien hoe u berichten in een wachtrij lezen.</span><span class="sxs-lookup"><span data-stu-id="ffda8-170">The two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how to read messages from a queue.</span></span>    

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="ffda8-171">Een bericht in een wachtrij lezen zonder het te verwijderen</span><span class="sxs-lookup"><span data-stu-id="ffda8-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="ffda8-172">Deze sectie ziet u hoe bekijken van een wachtrij bericht (het eerste bericht gelezen zonder het te verwijderen).</span><span class="sxs-lookup"><span data-stu-id="ffda8-172">This section illustrates how to peek at a queued message (read the first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="ffda8-173">Deze sectie wordt ervan uitgegaan dat u de stappen hebt voltooid [de ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="ffda8-173">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="ffda8-174">Open het `QueuesController.cs`-bestand.</span><span class="sxs-lookup"><span data-stu-id="ffda8-174">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="ffda8-175">Toevoegen van een methode aangeroepen **PeekMessage** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="ffda8-176">Binnen de **PeekMessage** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="ffda8-176">Within the **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ffda8-177">Gebruik de volgende code de verbindingsreeks voor opslag en storage-account-gegevens ophalen uit de configuratie van Azure service: (wijziging  *&lt;storage-account-name >* op de naam van de Azure storage-account u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="ffda8-177">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="ffda8-178">Ophalen van een **CloudQueueClient** object vertegenwoordigt een queue-serviceclient.</span><span class="sxs-lookup"><span data-stu-id="ffda8-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="ffda8-179">Ophalen van een **CloudQueueContainer** -object met een verwijzing naar de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ffda8-179">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="ffda8-180">Roep de **CloudQueue.PeekMessage** methode om te lezen van het eerste bericht in de wachtrij zonder het te verwijderen uit de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ffda8-180">Call the **CloudQueue.PeekMessage** method to read the first message in the queue without removing it from the queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="ffda8-181">Update de **ViewBag** met twee waarden: naam van de wachtrij en het bericht dat is gelezen.</span><span class="sxs-lookup"><span data-stu-id="ffda8-181">Update the **ViewBag** with two values: the queue name and the message that was read.</span></span> <span data-ttu-id="ffda8-182">De **CloudQueueMessage** object beschrijft de twee eigenschappen voor het ophalen van de waarde van het object: **CloudQueueMessage.AsBytes** en **CloudQueueMessage.AsString**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-182">The **CloudQueueMessage** object exposes two properties for getting the object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="ffda8-183">**AsString** (gebruikt in dit voorbeeld) retourneert een tekenreeks, terwijl **AsBytes** retourneert een bytematrix.</span><span class="sxs-lookup"><span data-stu-id="ffda8-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="ffda8-184">In de **Solution Explorer**, vouw de **weergaven** map met de rechtermuisknop op **wachtrijen**, en selecteer in het contextmenu **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-184">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="ffda8-185">Op de **weergave toevoegen** dialoogvenster Voer **PeekMessage** voor de weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-185">On the **Add View** dialog, enter **PeekMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="ffda8-186">Open `PeekMessage.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment:</span><span class="sxs-lookup"><span data-stu-id="ffda8-186">Open `PeekMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "PeekMessage";
    }
    
    <h2>Peek Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Peeked Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>    
    ```

1. <span data-ttu-id="ffda8-187">In de **Solution Explorer**, vouw de **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="ffda8-187">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="ffda8-188">Nadat de laatste **Html.ActionLink**, voeg de volgende **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="ffda8-188">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="ffda8-189">Voer de toepassing en selecteer **Peek bericht** om vergelijkbaar met de volgende schermopname resultaten te bekijken:</span><span class="sxs-lookup"><span data-stu-id="ffda8-189">Run the application, and select **Peek message** to see results similar to the following screen shot:</span></span>
  
    ![Bericht](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="ffda8-191">Lezen en verwijderen van een bericht van een wachtrij</span><span class="sxs-lookup"><span data-stu-id="ffda8-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="ffda8-192">Informatie over het lezen en verwijderen van een bericht van een wachtrij in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="ffda8-192">In this section, you learn how to read and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="ffda8-193">Deze sectie wordt ervan uitgegaan dat u de stappen hebt voltooid [de ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="ffda8-193">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="ffda8-194">Open het `QueuesController.cs`-bestand.</span><span class="sxs-lookup"><span data-stu-id="ffda8-194">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="ffda8-195">Toevoegen van een methode aangeroepen **gelezenBericht** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="ffda8-196">Binnen de **gelezenBericht** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="ffda8-196">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ffda8-197">Gebruik de volgende code de verbindingsreeks voor opslag en storage-account-gegevens ophalen uit de configuratie van Azure service: (wijziging  *&lt;storage-account-name >* op de naam van de Azure storage-account u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="ffda8-197">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="ffda8-198">Ophalen van een **CloudQueueClient** object vertegenwoordigt een queue-serviceclient.</span><span class="sxs-lookup"><span data-stu-id="ffda8-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="ffda8-199">Ophalen van een **CloudQueueContainer** -object met een verwijzing naar de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ffda8-199">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="ffda8-200">Roep de **CloudQueue.GetMessage** methode het eerste bericht in de wachtrij te lezen.</span><span class="sxs-lookup"><span data-stu-id="ffda8-200">Call the **CloudQueue.GetMessage** method to read the first message in the queue.</span></span> <span data-ttu-id="ffda8-201">De **CloudQueue.GetMessage** methode kunt u het bericht onzichtbaar gedurende 30 seconden (standaard) om te lezen van berichten, zodat er geen andere code kunt wijzigen of verwijderen van bericht tijdens de verwerking van deze code.</span><span class="sxs-lookup"><span data-stu-id="ffda8-201">The **CloudQueue.GetMessage** method makes the message invisible for 30 seconds (by default) to any other code reading messages so that no other code can modify or delete the message while your processing it.</span></span> <span data-ttu-id="ffda8-202">Als u wilt wijzigen van de hoeveelheid tijd die het bericht onzichtbaar is, wijzigt u de **visibilityTimeout** parameter worden doorgegeven aan de **CloudQueue.GetMessage** methode.</span><span class="sxs-lookup"><span data-stu-id="ffda8-202">To change the amount of time the message is invisible, modify the **visibilityTimeout** parameter being passed to the **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible to other code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="ffda8-203">Roep de **CloudQueueMessage.Delete** methode om te verwijderen van het bericht uit de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ffda8-203">Call the **CloudQueueMessage.Delete** method to delete the message from the queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="ffda8-204">Update de **ViewBag** met het bericht is verwijderd en de naam van de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ffda8-204">Update the **ViewBag** with the message deleted, and the name of the queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="ffda8-205">In de **Solution Explorer**, vouw de **weergaven** map met de rechtermuisknop op **wachtrijen**, en selecteer in het contextmenu **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-205">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="ffda8-206">Op de **weergave toevoegen** dialoogvenster Voer **gelezenBericht** voor de weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-206">On the **Add View** dialog, enter **ReadMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="ffda8-207">Open `ReadMessage.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment:</span><span class="sxs-lookup"><span data-stu-id="ffda8-207">Open `ReadMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "ReadMessage";
    }
    
    <h2>Read Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Read (and Deleted) Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>
    ```

1. <span data-ttu-id="ffda8-208">In de **Solution Explorer**, vouw de **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="ffda8-208">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="ffda8-209">Nadat de laatste **Html.ActionLink**, voeg de volgende **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="ffda8-209">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="ffda8-210">Voer de toepassing en selecteer **Lees-/ verwijderingsbericht** om vergelijkbaar met de volgende schermopname resultaten te bekijken:</span><span class="sxs-lookup"><span data-stu-id="ffda8-210">Run the application, and select **Read/Delete message** to see results similar to the following screen shot:</span></span>
  
    ![Lezen en verwijderen van bericht](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-the-queue-length"></a><span data-ttu-id="ffda8-212">Lengte van de wachtrij ophalen</span><span class="sxs-lookup"><span data-stu-id="ffda8-212">Get the queue length</span></span>

<span data-ttu-id="ffda8-213">Deze sectie ziet u hoe u de lengte van de wachtrij (het aantal berichten).</span><span class="sxs-lookup"><span data-stu-id="ffda8-213">This section illustrates how to get the queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="ffda8-214">Deze sectie wordt ervan uitgegaan dat u de stappen hebt voltooid [de ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="ffda8-214">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="ffda8-215">Open het `QueuesController.cs`-bestand.</span><span class="sxs-lookup"><span data-stu-id="ffda8-215">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="ffda8-216">Toevoegen van een methode aangeroepen **GetQueueLength** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="ffda8-217">Binnen de **gelezenBericht** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="ffda8-217">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ffda8-218">Gebruik de volgende code de verbindingsreeks voor opslag en storage-account-gegevens ophalen uit de configuratie van Azure service: (wijziging  *&lt;storage-account-name >* op de naam van de Azure storage-account u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="ffda8-218">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="ffda8-219">Ophalen van een **CloudQueueClient** object vertegenwoordigt een queue-serviceclient.</span><span class="sxs-lookup"><span data-stu-id="ffda8-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="ffda8-220">Ophalen van een **CloudQueueContainer** -object met een verwijzing naar de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ffda8-220">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="ffda8-221">Roep de **CloudQueue.FetchAttributes** methode voor het ophalen van de wachtrij-kenmerken (met inbegrip van de lengte).</span><span class="sxs-lookup"><span data-stu-id="ffda8-221">Call the **CloudQueue.FetchAttributes** method to retrieve the queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="ffda8-222">Toegang tot de **CloudQueue.ApproximateMessageCount** eigenschap ophalen van de lengte van de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ffda8-222">Access the **CloudQueue.ApproximateMessageCount** property to get the queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="ffda8-223">Update de **ViewBag** met de naam van de wachtrij en de lengte.</span><span class="sxs-lookup"><span data-stu-id="ffda8-223">Update the **ViewBag** with the name of the queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="ffda8-224">In de **Solution Explorer**, vouw de **weergaven** map met de rechtermuisknop op **wachtrijen**, en selecteer in het contextmenu **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-224">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="ffda8-225">Op de **weergave toevoegen** dialoogvenster Voer **GetQueueLength** voor de weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-225">On the **Add View** dialog, enter **GetQueueLength** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="ffda8-226">Open `GetQueueLengthMessage.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment:</span><span class="sxs-lookup"><span data-stu-id="ffda8-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    The queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="ffda8-227">In de **Solution Explorer**, vouw de **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="ffda8-227">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="ffda8-228">Nadat de laatste **Html.ActionLink**, voeg de volgende **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="ffda8-228">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="ffda8-229">Voer de toepassing en selecteer **ophalen wachtrijlengte** om vergelijkbaar met de volgende schermopname resultaten te bekijken:</span><span class="sxs-lookup"><span data-stu-id="ffda8-229">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span></span>
  
    ![Wachtrijlengte ophalen](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="ffda8-231">Een wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="ffda8-231">Delete a queue</span></span>
<span data-ttu-id="ffda8-232">Deze sectie ziet u hoe een wachtrij verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ffda8-232">This section illustrates how to delete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="ffda8-233">Deze sectie wordt ervan uitgegaan dat u de stappen hebt voltooid [de ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="ffda8-233">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="ffda8-234">Open het `QueuesController.cs`-bestand.</span><span class="sxs-lookup"><span data-stu-id="ffda8-234">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="ffda8-235">Toevoegen van een methode aangeroepen **DeleteQueue** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="ffda8-236">Binnen de **DeleteQueue** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="ffda8-236">Within the **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ffda8-237">Gebruik de volgende code de verbindingsreeks voor opslag en storage-account-gegevens ophalen uit de configuratie van Azure service: (wijziging  *&lt;storage-account-name >* op de naam van de Azure storage-account u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="ffda8-237">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="ffda8-238">Ophalen van een **CloudQueueClient** object vertegenwoordigt een queue-serviceclient.</span><span class="sxs-lookup"><span data-stu-id="ffda8-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="ffda8-239">Ophalen van een **CloudQueueContainer** -object met een verwijzing naar de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ffda8-239">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="ffda8-240">Roep de **CloudQueue.Delete** methode om te verwijderen van de wachtrij dat wordt vertegenwoordigd door de **CloudQueue** object.</span><span class="sxs-lookup"><span data-stu-id="ffda8-240">Call the **CloudQueue.Delete** method to delete the queue represented by the **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="ffda8-241">Update de **ViewBag** met de naam van de wachtrij en de lengte.</span><span class="sxs-lookup"><span data-stu-id="ffda8-241">Update the **ViewBag** with the name of the queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="ffda8-242">In de **Solution Explorer**, vouw de **weergaven** map met de rechtermuisknop op **wachtrijen**, en selecteer in het contextmenu **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-242">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="ffda8-243">Op de **weergave toevoegen** dialoogvenster Voer **DeleteQueue** voor de weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ffda8-243">On the **Add View** dialog, enter **DeleteQueue** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="ffda8-244">Open `DeleteQueue.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment:</span><span class="sxs-lookup"><span data-stu-id="ffda8-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="ffda8-245">In de **Solution Explorer**, vouw de **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="ffda8-245">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="ffda8-246">Nadat de laatste **Html.ActionLink**, voeg de volgende **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="ffda8-246">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="ffda8-247">Voer de toepassing en selecteer **ophalen wachtrijlengte** om vergelijkbaar met de volgende schermopname resultaten te bekijken:</span><span class="sxs-lookup"><span data-stu-id="ffda8-247">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span></span>
  
    ![Wachtrij verwijderen](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="ffda8-249">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ffda8-249">Next steps</span></span>
<span data-ttu-id="ffda8-250">Bekijk meer functiehandleidingen voor informatie over aanvullende mogelijkheden voor het opslaan van gegevens in Azure.</span><span class="sxs-lookup"><span data-stu-id="ffda8-250">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="ffda8-251">Aan de slag met Azure blob storage en Visual Studio verbonden Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="ffda8-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="ffda8-252">Aan de slag met Azure-tabelopslag en Visual Studio verbonden Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="ffda8-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
