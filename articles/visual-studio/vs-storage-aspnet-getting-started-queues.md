---
title: aaaGet de slag met Azure queue storage- en Visual Studio verbonden Services (ASP.NET) | Microsoft Docs
description: Hoe tooget gestart met behulp van Azure queue storage nadat u hebt aangesloten tooa storage-account met behulp van Visual Studio verbonden Services in een ASP.NET-project in Visual Studio
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
ms.openlocfilehash: 415a437c4ce60b1e2e328f8e937c73b0d5c50e78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="b994c-103">Aan de slag met Azure queue storage- en Visual Studio verbonden Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="b994c-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="b994c-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b994c-104">Overview</span></span>

<span data-ttu-id="b994c-105">Azure queue storage biedt cloud messaging tussen toepassingsonderdelen.</span><span class="sxs-lookup"><span data-stu-id="b994c-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="b994c-106">Bij het ontwerpen van schaalbare toepassingen worden toepassingsonderdelen vaak ontkoppeld, zodat ze onafhankelijk van elkaar kunnen worden geschaald.</span><span class="sxs-lookup"><span data-stu-id="b994c-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="b994c-107">Queue storage biedt asynchrone messaging voor communicatie tussen toepassingsonderdelen, of ze worden uitgevoerd in Hallo cloud, op Hallo bureaublad, op een on-premises server of op een mobiel apparaat.</span><span class="sxs-lookup"><span data-stu-id="b994c-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="b994c-108">Queue Storage biedt daarnaast ondersteuning voor het beheren van asynchrone taken en het samenstellen van proceswerkstromen.</span><span class="sxs-lookup"><span data-stu-id="b994c-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="b994c-109">Deze zelfstudie laat zien hoe toowrite ASP.NET-code voor enkele algemene scenario's met Azure queue storage entiteiten.</span><span class="sxs-lookup"><span data-stu-id="b994c-109">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="b994c-110">Deze scenario's omvatten algemene taken, zoals het maken van een Azure-wachtrij en toevoegen, wijzigen, lezen en verwijderen van Wachtrijberichten.</span><span class="sxs-lookup"><span data-stu-id="b994c-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="b994c-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b994c-111">Prerequisites</span></span>

* [<span data-ttu-id="b994c-112">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b994c-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="b994c-113">Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="b994c-113">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="b994c-114">Maken van een MVC-controller</span><span class="sxs-lookup"><span data-stu-id="b994c-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="b994c-115">In Hallo **Solution Explorer**, met de rechtermuisknop op **domeincontrollers**, en selecteer in het contextmenu hello, **toevoegen -> Controller**.</span><span class="sxs-lookup"><span data-stu-id="b994c-115">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Een controller tooan ASP.NET MVC-app toevoegen](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="b994c-117">Op Hallo **Add Scaffold** dialoogvenster Selecteer **MVC 5 Controller - leeg**, en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b994c-117">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Geef een MVC-controller](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="b994c-119">Op Hallo **Controller toevoegen** dialoogvenster, naam Hallo controller *QueuesController*, en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b994c-119">On hello **Add Controller** dialog, name hello controller *QueuesController*, and select **Add**.</span></span>

    ![Naam Hallo MVC-controller](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="b994c-121">Voeg de volgende Hallo *met* richtlijnen toohello `QueuesController.cs` bestand:</span><span class="sxs-lookup"><span data-stu-id="b994c-121">Add hello following *using* directives toohello `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="b994c-122">Een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="b994c-122">Create a queue</span></span>

<span data-ttu-id="b994c-123">Hallo volgende stappen laten zien hoe een wachtrij toocreate:</span><span class="sxs-lookup"><span data-stu-id="b994c-123">hello following steps illustrate how toocreate a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="b994c-124">Deze sectie wordt ervan uitgegaan dat u Hallo stappen hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="b994c-124">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="b994c-125">Open Hallo `QueuesController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="b994c-125">Open hello `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="b994c-126">Toevoegen van een methode aangeroepen **CreateQueue** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="b994c-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="b994c-127">Binnen Hallo **CreateQueue** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="b994c-127">Within hello **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b994c-128">Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="b994c-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="b994c-129">Ophalen van een **CloudQueueClient** object vertegenwoordigt een queue-serviceclient.</span><span class="sxs-lookup"><span data-stu-id="b994c-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="b994c-130">Ophalen van een **CloudQueue** -object met de naam van een verwijzing toohello gewenste wachtrij.</span><span class="sxs-lookup"><span data-stu-id="b994c-130">Get a **CloudQueue** object that represents a reference toohello desired queue name.</span></span> <span data-ttu-id="b994c-131">Hallo **CloudQueueClient.GetQueueReference** methode heeft een aanvraag in voor wachtrijopslag moet fungeren niet maken.</span><span class="sxs-lookup"><span data-stu-id="b994c-131">hello **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="b994c-132">Hallo verwijzing wordt geretourneerd of Hallo wachtrij bestaat of niet.</span><span class="sxs-lookup"><span data-stu-id="b994c-132">hello reference is returned whether or not hello queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="b994c-133">Hallo aanroepen **CloudQueue.CreateIfNotExists** methode toocreate Hallo wachtrij als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="b994c-133">Call hello **CloudQueue.CreateIfNotExists** method toocreate hello queue if it does not yet exist.</span></span> <span data-ttu-id="b994c-134">Hallo **CloudQueue.CreateIfNotExists** methode retourneert **true** als Hallo wachtrij niet bestaat en is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b994c-134">hello **CloudQueue.CreateIfNotExists** method returns **true** if hello queue does not exist, and is successfully created.</span></span> <span data-ttu-id="b994c-135">Anders **false** wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b994c-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="b994c-136">Update Hallo **ViewBag** met de naam van de wachtrij Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b994c-136">Update hello **ViewBag** with hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="b994c-137">In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **wachtrijen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="b994c-137">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b994c-138">Op Hallo **weergave toevoegen** dialoogvenster Voer **CreateQueue** voor Hallo weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b994c-138">On hello **Add View** dialog, enter **CreateQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="b994c-139">Open `CreateQueue.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="b994c-139">Open `CreateQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="b994c-140">In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="b994c-140">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b994c-141">Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="b994c-141">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="b994c-142">Voer Hallo toepassing uit en selecteer **wachtrij maken** toosee resulteert vergelijkbare toohello schermopname te volgen:</span><span class="sxs-lookup"><span data-stu-id="b994c-142">Run hello application, and select **Create queue** toosee results similar toohello following screen shot:</span></span>
  
    ![Wachtrij maken](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="b994c-144">Zoals eerder vermeld, Hallo **CloudQueue.CreateIfNotExists** methode retourneert **true** alleen wanneer Hallo wachtrij bestaat niet en is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b994c-144">As mentioned previously, hello **CloudQueue.CreateIfNotExists** method returns **true** only when hello queue doesn't exist and is created.</span></span> <span data-ttu-id="b994c-145">Dus als u Hallo app uitvoeren wanneer de wachtrij Hallo bestaat, Hallo methode retourneert **false**.</span><span class="sxs-lookup"><span data-stu-id="b994c-145">Therefore, if you run hello app when hello queue exists, hello method returns **false**.</span></span> <span data-ttu-id="b994c-146">toorun hello app meerdere keren moet u Hallo wachtrij verwijderen voordat u Hallo app opnieuw uitvoert.</span><span class="sxs-lookup"><span data-stu-id="b994c-146">toorun hello app multiple times, you must delete hello queue before running hello app again.</span></span> <span data-ttu-id="b994c-147">Verwijderen Hallo wachtrij kan worden uitgevoerd via Hallo **CloudQueue.Delete** methode.</span><span class="sxs-lookup"><span data-stu-id="b994c-147">Deleting hello queue can be done via hello **CloudQueue.Delete** method.</span></span> <span data-ttu-id="b994c-148">U kunt ook Hallo wachtrij met Hallo verwijderen [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) of Hallo [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="b994c-148">You can also delete hello queue using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="b994c-149">Een berichtenwachtrij tooa toevoegen</span><span class="sxs-lookup"><span data-stu-id="b994c-149">Add a message tooa queue</span></span>

<span data-ttu-id="b994c-150">Zodra u hebt [wachtrij](#create-a-queue), kunt u berichten toothat wachtrij toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b994c-150">Once you've [created a queue](#create-a-queue), you can add messages toothat queue.</span></span> <span data-ttu-id="b994c-151">Deze sectie helpt u bij het toevoegen van een berichtenwachtrij tooa *test wachtrij*.</span><span class="sxs-lookup"><span data-stu-id="b994c-151">This section walks you through adding a message tooa queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="b994c-152">Deze sectie wordt ervan uitgegaan dat u Hallo stappen hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="b994c-152">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="b994c-153">Open Hallo `QueuesController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="b994c-153">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="b994c-154">Toevoegen van een methode aangeroepen **AddMessage** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="b994c-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="b994c-155">Binnen Hallo **AddMessage** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="b994c-155">Within hello **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b994c-156">Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="b994c-156">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="b994c-157">Ophalen van een **CloudQueueClient** object vertegenwoordigt een queue-serviceclient.</span><span class="sxs-lookup"><span data-stu-id="b994c-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="b994c-158">Ophalen van een **CloudQueueContainer** -object met een verwijzing toohello wachtrij.</span><span class="sxs-lookup"><span data-stu-id="b994c-158">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="b994c-159">Hallo maken **CloudQueueMessage** -object dat u wilt dat tooadd toohello wachtrij het Hallo-bericht vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="b994c-159">Create hello **CloudQueueMessage** object representing hello message you want tooadd toohello queue.</span></span> <span data-ttu-id="b994c-160">Een **CloudQueueMessage** object kan worden gemaakt vanuit een tekenreeks (in UTF-8-indeling) of een byte-matrix.</span><span class="sxs-lookup"><span data-stu-id="b994c-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="b994c-161">Hallo aanroepen **CloudQueue.AddMessage** methode tooadd Hallo mailberichten toohello wachtrij.</span><span class="sxs-lookup"><span data-stu-id="b994c-161">Call hello **CloudQueue.AddMessage** method tooadd hello messaged toohello queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="b994c-162">Maken en een aantal **ViewBag** eigenschappen weergegeven in de Hallo weergeven.</span><span class="sxs-lookup"><span data-stu-id="b994c-162">Create and set a couple of **ViewBag** properties for display in hello view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="b994c-163">In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **wachtrijen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="b994c-163">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b994c-164">Op Hallo **weergave toevoegen** dialoogvenster Voer **AddMessage** voor Hallo weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b994c-164">On hello **Add View** dialog, enter **AddMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="b994c-165">Open `AddMessage.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="b994c-165">Open `AddMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="b994c-166">In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="b994c-166">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b994c-167">Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="b994c-167">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="b994c-168">Voer Hallo toepassing uit en selecteer **toevoegen bericht** toosee resulteert vergelijkbare toohello schermopname te volgen:</span><span class="sxs-lookup"><span data-stu-id="b994c-168">Run hello application, and select **Add message** toosee results similar toohello following screen shot:</span></span>
  
    ![Bericht toevoegen](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="b994c-170">twee secties - Hallo [een bericht in een wachtrij lezen zonder het te verwijderen](#read-a-message-from-a-queue-without-removing-it) en [lezen en verwijderen van een bericht van een wachtrij](#read-and-remove-a-message-from-a-queue) -laten zien hoe tooread berichten uit een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="b994c-170">hello two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how tooread messages from a queue.</span></span>  

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="b994c-171">Een bericht in een wachtrij lezen zonder het te verwijderen</span><span class="sxs-lookup"><span data-stu-id="b994c-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="b994c-172">Deze sectie ziet u hoe toopeek op een bericht in de wachtrij (lezen Hallo eerste bericht zonder het te verwijderen).</span><span class="sxs-lookup"><span data-stu-id="b994c-172">This section illustrates how toopeek at a queued message (read hello first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="b994c-173">Deze sectie wordt ervan uitgegaan dat u Hallo stappen hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="b994c-173">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="b994c-174">Open Hallo `QueuesController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="b994c-174">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="b994c-175">Toevoegen van een methode aangeroepen **PeekMessage** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="b994c-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="b994c-176">Binnen Hallo **PeekMessage** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="b994c-176">Within hello **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b994c-177">Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="b994c-177">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="b994c-178">Ophalen van een **CloudQueueClient** object vertegenwoordigt een queue-serviceclient.</span><span class="sxs-lookup"><span data-stu-id="b994c-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="b994c-179">Ophalen van een **CloudQueueContainer** -object met een verwijzing toohello wachtrij.</span><span class="sxs-lookup"><span data-stu-id="b994c-179">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="b994c-180">Hallo aanroepen **CloudQueue.PeekMessage** methode tooread Hallo eerste bericht in de wachtrij Hallo zonder het te verwijderen uit de wachtrij Hallo.</span><span class="sxs-lookup"><span data-stu-id="b994c-180">Call hello **CloudQueue.PeekMessage** method tooread hello first message in hello queue without removing it from hello queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="b994c-181">Update Hallo **ViewBag** met twee waarden: Hallo wachtrijnaam en het Hallo-bericht dat is gelezen.</span><span class="sxs-lookup"><span data-stu-id="b994c-181">Update hello **ViewBag** with two values: hello queue name and hello message that was read.</span></span> <span data-ttu-id="b994c-182">Hallo **CloudQueueMessage** object beschrijft de twee eigenschappen voor het ophalen van de waarde van het object Hallo: **CloudQueueMessage.AsBytes** en **CloudQueueMessage.AsString**.</span><span class="sxs-lookup"><span data-stu-id="b994c-182">hello **CloudQueueMessage** object exposes two properties for getting hello object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="b994c-183">**AsString** (gebruikt in dit voorbeeld) retourneert een tekenreeks, terwijl **AsBytes** retourneert een bytematrix.</span><span class="sxs-lookup"><span data-stu-id="b994c-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="b994c-184">In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **wachtrijen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="b994c-184">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b994c-185">Op Hallo **weergave toevoegen** dialoogvenster Voer **PeekMessage** voor Hallo weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b994c-185">On hello **Add View** dialog, enter **PeekMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="b994c-186">Open `PeekMessage.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="b994c-186">Open `PeekMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="b994c-187">In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="b994c-187">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b994c-188">Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="b994c-188">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="b994c-189">Voer Hallo toepassing uit en selecteer **Peek bericht** toosee resulteert vergelijkbare toohello schermopname te volgen:</span><span class="sxs-lookup"><span data-stu-id="b994c-189">Run hello application, and select **Peek message** toosee results similar toohello following screen shot:</span></span>
  
    ![Bericht](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="b994c-191">Lezen en verwijderen van een bericht van een wachtrij</span><span class="sxs-lookup"><span data-stu-id="b994c-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="b994c-192">In deze sectie leest u hoe tooread en verwijderen van een bericht van een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="b994c-192">In this section, you learn how tooread and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="b994c-193">Deze sectie wordt ervan uitgegaan dat u Hallo stappen hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="b994c-193">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="b994c-194">Open Hallo `QueuesController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="b994c-194">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="b994c-195">Toevoegen van een methode aangeroepen **gelezenBericht** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="b994c-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="b994c-196">Binnen Hallo **gelezenBericht** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="b994c-196">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b994c-197">Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="b994c-197">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="b994c-198">Ophalen van een **CloudQueueClient** object vertegenwoordigt een queue-serviceclient.</span><span class="sxs-lookup"><span data-stu-id="b994c-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="b994c-199">Ophalen van een **CloudQueueContainer** -object met een verwijzing toohello wachtrij.</span><span class="sxs-lookup"><span data-stu-id="b994c-199">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="b994c-200">Hallo aanroepen **CloudQueue.GetMessage** methode tooread Hallo eerste bericht in Hallo wachtrij.</span><span class="sxs-lookup"><span data-stu-id="b994c-200">Call hello **CloudQueue.GetMessage** method tooread hello first message in hello queue.</span></span> <span data-ttu-id="b994c-201">Hallo **CloudQueue.GetMessage** Hallo bericht onzichtbaar voor 30 seconden (standaard) tooany andere codes die berichten lezen, zodat er geen andere code kunt wijzigen of verwijderen van het Hallo-bericht tijdens de verwerking van deze methode kunt u.</span><span class="sxs-lookup"><span data-stu-id="b994c-201">hello **CloudQueue.GetMessage** method makes hello message invisible for 30 seconds (by default) tooany other code reading messages so that no other code can modify or delete hello message while your processing it.</span></span> <span data-ttu-id="b994c-202">toochange hello hoeveelheid tijd Hallo-bericht onzichtbaar is, wijzigt u Hallo **visibilityTimeout** parameter worden doorgegeven toohello **CloudQueue.GetMessage** methode.</span><span class="sxs-lookup"><span data-stu-id="b994c-202">toochange hello amount of time hello message is invisible, modify hello **visibilityTimeout** parameter being passed toohello **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="b994c-203">Hallo aanroepen **CloudQueueMessage.Delete** methode toodelete Hallo-bericht uit de wachtrij Hallo.</span><span class="sxs-lookup"><span data-stu-id="b994c-203">Call hello **CloudQueueMessage.Delete** method toodelete hello message from hello queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="b994c-204">Update Hallo **ViewBag** Hello bericht verwijderd en de naam van de wachtrij Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b994c-204">Update hello **ViewBag** with hello message deleted, and hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="b994c-205">In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **wachtrijen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="b994c-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b994c-206">Op Hallo **weergave toevoegen** dialoogvenster Voer **gelezenBericht** voor Hallo weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b994c-206">On hello **Add View** dialog, enter **ReadMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="b994c-207">Open `ReadMessage.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="b994c-207">Open `ReadMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="b994c-208">In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="b994c-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b994c-209">Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="b994c-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="b994c-210">Voer Hallo toepassing uit en selecteer **Lees-/ verwijderingsbericht** toosee resulteert vergelijkbare toohello schermopname te volgen:</span><span class="sxs-lookup"><span data-stu-id="b994c-210">Run hello application, and select **Read/Delete message** toosee results similar toohello following screen shot:</span></span>
  
    ![Lezen en verwijderen van bericht](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a><span data-ttu-id="b994c-212">Hallo-wachtrijlengte ophalen</span><span class="sxs-lookup"><span data-stu-id="b994c-212">Get hello queue length</span></span>

<span data-ttu-id="b994c-213">Deze sectie ziet u hoe tooget Hallo wachtrijlengte (aantal berichten).</span><span class="sxs-lookup"><span data-stu-id="b994c-213">This section illustrates how tooget hello queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="b994c-214">Deze sectie wordt ervan uitgegaan dat u Hallo stappen hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="b994c-214">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="b994c-215">Open Hallo `QueuesController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="b994c-215">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="b994c-216">Toevoegen van een methode aangeroepen **GetQueueLength** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="b994c-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="b994c-217">Binnen Hallo **gelezenBericht** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="b994c-217">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b994c-218">Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="b994c-218">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="b994c-219">Ophalen van een **CloudQueueClient** object vertegenwoordigt een queue-serviceclient.</span><span class="sxs-lookup"><span data-stu-id="b994c-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="b994c-220">Ophalen van een **CloudQueueContainer** -object met een verwijzing toohello wachtrij.</span><span class="sxs-lookup"><span data-stu-id="b994c-220">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="b994c-221">Hallo aanroepen **CloudQueue.FetchAttributes** methode tooretrieve Hallo van wachtrij-kenmerken (met inbegrip van de lengte).</span><span class="sxs-lookup"><span data-stu-id="b994c-221">Call hello **CloudQueue.FetchAttributes** method tooretrieve hello queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="b994c-222">Toegang Hallo **CloudQueue.ApproximateMessageCount** wachtrijlengte van eigenschap tooget Hallo.</span><span class="sxs-lookup"><span data-stu-id="b994c-222">Access hello **CloudQueue.ApproximateMessageCount** property tooget hello queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="b994c-223">Update Hallo **ViewBag** Hallo-naam van Hallo wachtrij en de lengte.</span><span class="sxs-lookup"><span data-stu-id="b994c-223">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="b994c-224">In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **wachtrijen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="b994c-224">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b994c-225">Op Hallo **weergave toevoegen** dialoogvenster Voer **GetQueueLength** voor Hallo weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b994c-225">On hello **Add View** dialog, enter **GetQueueLength** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="b994c-226">Open `GetQueueLengthMessage.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="b994c-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="b994c-227">In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="b994c-227">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b994c-228">Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="b994c-228">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="b994c-229">Voer Hallo toepassing uit en selecteer **ophalen wachtrijlengte** toosee resulteert vergelijkbare toohello schermopname te volgen:</span><span class="sxs-lookup"><span data-stu-id="b994c-229">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![Wachtrijlengte ophalen](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="b994c-231">Een wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="b994c-231">Delete a queue</span></span>
<span data-ttu-id="b994c-232">Deze sectie wordt beschreven hoe een wachtrij toodelete.</span><span class="sxs-lookup"><span data-stu-id="b994c-232">This section illustrates how toodelete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="b994c-233">Deze sectie wordt ervan uitgegaan dat u Hallo stappen hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="b994c-233">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="b994c-234">Open Hallo `QueuesController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="b994c-234">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="b994c-235">Toevoegen van een methode aangeroepen **DeleteQueue** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="b994c-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="b994c-236">Binnen Hallo **DeleteQueue** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="b994c-236">Within hello **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b994c-237">Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="b994c-237">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="b994c-238">Ophalen van een **CloudQueueClient** object vertegenwoordigt een queue-serviceclient.</span><span class="sxs-lookup"><span data-stu-id="b994c-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="b994c-239">Ophalen van een **CloudQueueContainer** -object met een verwijzing toohello wachtrij.</span><span class="sxs-lookup"><span data-stu-id="b994c-239">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="b994c-240">Hallo aanroepen **CloudQueue.Delete** methode toodelete Hallo wachtrij vertegenwoordigd door Hallo **CloudQueue** object.</span><span class="sxs-lookup"><span data-stu-id="b994c-240">Call hello **CloudQueue.Delete** method toodelete hello queue represented by hello **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="b994c-241">Update Hallo **ViewBag** Hallo-naam van Hallo wachtrij en de lengte.</span><span class="sxs-lookup"><span data-stu-id="b994c-241">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="b994c-242">In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **wachtrijen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="b994c-242">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b994c-243">Op Hallo **weergave toevoegen** dialoogvenster Voer **DeleteQueue** voor Hallo weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b994c-243">On hello **Add View** dialog, enter **DeleteQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="b994c-244">Open `DeleteQueue.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="b994c-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="b994c-245">In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="b994c-245">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b994c-246">Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="b994c-246">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="b994c-247">Voer Hallo toepassing uit en selecteer **ophalen wachtrijlengte** toosee resulteert vergelijkbare toohello schermopname te volgen:</span><span class="sxs-lookup"><span data-stu-id="b994c-247">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![Wachtrij verwijderen](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="b994c-249">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b994c-249">Next steps</span></span>
<span data-ttu-id="b994c-250">Bekijk meer functie handleidingen toolearn over aanvullende mogelijkheden voor het opslaan van gegevens in Azure.</span><span class="sxs-lookup"><span data-stu-id="b994c-250">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="b994c-251">Aan de slag met Azure blob storage en Visual Studio verbonden Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="b994c-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="b994c-252">Aan de slag met Azure-tabelopslag en Visual Studio verbonden Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="b994c-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
