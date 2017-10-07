---
title: aaaGet de slag met Azure queue storage- en Visual Studio verbonden Services (ASP.NET) | Microsoft Docs
description: Hoe tooget gestart met behulp van Azure queue storage nadat u hebt aangesloten tooa storage-account met behulp van Visual Studio verbonden Services in een ASP.NET-project in Visual Studio
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 94ca3413-5497-433f-abbe-836f83a9de72
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/23/2016
ms.author: tarcher
ms.openlocfilehash: a9d6ecb1e8d61d75f59658d0ea3fa63d26fd7354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a>Aan de slag met Azure queue storage- en Visual Studio verbonden Services (ASP.NET)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Overzicht

Azure queue storage biedt cloud messaging tussen toepassingsonderdelen. Bij het ontwerpen van schaalbare toepassingen worden toepassingsonderdelen vaak ontkoppeld, zodat ze onafhankelijk van elkaar kunnen worden geschaald. Queue storage biedt asynchrone messaging voor communicatie tussen toepassingsonderdelen, of ze worden uitgevoerd in Hallo cloud, op Hallo bureaublad, op een on-premises server of op een mobiel apparaat. Queue Storage biedt daarnaast ondersteuning voor het beheren van asynchrone taken en het samenstellen van proceswerkstromen.

Deze zelfstudie laat zien hoe toowrite ASP.NET-code voor enkele algemene scenario's met Azure queue storage entiteiten. Deze scenario's omvatten algemene taken, zoals het maken van een Azure-wachtrij en toevoegen, wijzigen, lezen en verwijderen van Wachtrijberichten.

##<a name="prerequisites"></a>Vereisten

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Azure Storage-account](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Maken van een MVC-controller 

1. In Hallo **Solution Explorer**, met de rechtermuisknop op **domeincontrollers**, en selecteer in het contextmenu hello, **toevoegen -> Controller**.

    ![Een controller tooan ASP.NET MVC-app toevoegen](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. Op Hallo **Add Scaffold** dialoogvenster Selecteer **MVC 5 Controller - leeg**, en selecteer **toevoegen**.

    ![Geef een MVC-controller](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. Op Hallo **Controller toevoegen** dialoogvenster, naam Hallo controller *QueuesController*, en selecteer **toevoegen**.

    ![Naam Hallo MVC-controller](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. Voeg de volgende Hallo *met* richtlijnen toohello `QueuesController.cs` bestand:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a>Een wachtrij maken

Hallo volgende stappen laten zien hoe een wachtrij toocreate:

> [!NOTE]
> 
> Deze sectie wordt ervan uitgegaan dat u Hallo stappen hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment). 

1. Open Hallo `QueuesController.cs` bestand. 

1. Toevoegen van een methode aangeroepen **CreateQueue** die retourneert een **ActionResult**.

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Binnen Hallo **CreateQueue** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account. Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Ophalen van een **CloudQueueClient** object vertegenwoordigt een queue-serviceclient.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. Ophalen van een **CloudQueue** -object met de naam van een verwijzing toohello gewenste wachtrij. Hallo **CloudQueueClient.GetQueueReference** methode heeft een aanvraag in voor wachtrijopslag moet fungeren niet maken. Hallo verwijzing wordt geretourneerd of Hallo wachtrij bestaat of niet. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Hallo aanroepen **CloudQueue.CreateIfNotExists** methode toocreate Hallo wachtrij als deze nog niet bestaat. Hallo **CloudQueue.CreateIfNotExists** methode retourneert **true** als Hallo wachtrij niet bestaat en is gemaakt. Anders **false** wordt geretourneerd.    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. Update Hallo **ViewBag** met de naam van de wachtrij Hallo Hallo.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **wachtrijen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.

1. Op Hallo **weergave toevoegen** dialoogvenster Voer **CreateQueue** voor Hallo weergavenaam en selecteer **toevoegen**.

1. Open `CreateQueue.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.

1. Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. Voer Hallo toepassing uit en selecteer **wachtrij maken** toosee resulteert vergelijkbare toohello schermopname te volgen:
  
    ![Wachtrij maken](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    Zoals eerder vermeld, Hallo **CloudQueue.CreateIfNotExists** methode retourneert **true** alleen wanneer Hallo wachtrij bestaat niet en is gemaakt. Dus als u Hallo app uitvoeren wanneer de wachtrij Hallo bestaat, Hallo methode retourneert **false**. toorun hello app meerdere keren moet u Hallo wachtrij verwijderen voordat u Hallo app opnieuw uitvoert. Verwijderen Hallo wachtrij kan worden uitgevoerd via Hallo **CloudQueue.Delete** methode. U kunt ook Hallo wachtrij met Hallo verwijderen [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) of Hallo [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="add-a-message-tooa-queue"></a>Een berichtenwachtrij tooa toevoegen

Zodra u hebt [wachtrij](#create-a-queue), kunt u berichten toothat wachtrij toevoegen. Deze sectie helpt u bij het toevoegen van een berichtenwachtrij tooa *test wachtrij*. 

> [!NOTE]
> 
> Deze sectie wordt ervan uitgegaan dat u Hallo stappen hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment). 

1. Open Hallo `QueuesController.cs` bestand.

1. Toevoegen van een methode aangeroepen **AddMessage** die retourneert een **ActionResult**.

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Binnen Hallo **AddMessage** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account. Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Ophalen van een **CloudQueueClient** object vertegenwoordigt een queue-serviceclient.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Ophalen van een **CloudQueueContainer** -object met een verwijzing toohello wachtrij. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Hallo maken **CloudQueueMessage** -object dat u wilt dat tooadd toohello wachtrij het Hallo-bericht vertegenwoordigt. Een **CloudQueueMessage** object kan worden gemaakt vanuit een tekenreeks (in UTF-8-indeling) of een byte-matrix.

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. Hallo aanroepen **CloudQueue.AddMessage** methode tooadd Hallo mailberichten toohello wachtrij.

    ```csharp
    queue.AddMessage(message);
    ```

1. Maken en een aantal **ViewBag** eigenschappen weergegeven in de Hallo weergeven.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **wachtrijen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.

1. Op Hallo **weergave toevoegen** dialoogvenster Voer **AddMessage** voor Hallo weergavenaam en selecteer **toevoegen**.

1. Open `AddMessage.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.

1. Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. Voer Hallo toepassing uit en selecteer **toevoegen bericht** toosee resulteert vergelijkbare toohello schermopname te volgen:
  
    ![Bericht toevoegen](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

twee secties - Hallo [een bericht in een wachtrij lezen zonder het te verwijderen](#read-a-message-from-a-queue-without-removing-it) en [lezen en verwijderen van een bericht van een wachtrij](#read-and-remove-a-message-from-a-queue) -laten zien hoe tooread berichten uit een wachtrij.  

## <a name="read-a-message-from-a-queue-without-removing-it"></a>Een bericht in een wachtrij lezen zonder het te verwijderen

Deze sectie ziet u hoe toopeek op een bericht in de wachtrij (lezen Hallo eerste bericht zonder het te verwijderen).  

> [!NOTE]
> 
> Deze sectie wordt ervan uitgegaan dat u Hallo stappen hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment). 

1. Open Hallo `QueuesController.cs` bestand.

1. Toevoegen van een methode aangeroepen **PeekMessage** die retourneert een **ActionResult**.

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Binnen Hallo **PeekMessage** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account. Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Ophalen van een **CloudQueueClient** object vertegenwoordigt een queue-serviceclient.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Ophalen van een **CloudQueueContainer** -object met een verwijzing toohello wachtrij. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Hallo aanroepen **CloudQueue.PeekMessage** methode tooread Hallo eerste bericht in de wachtrij Hallo zonder het te verwijderen uit de wachtrij Hallo. 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. Update Hallo **ViewBag** met twee waarden: Hallo wachtrijnaam en het Hallo-bericht dat is gelezen. Hallo **CloudQueueMessage** object beschrijft de twee eigenschappen voor het ophalen van de waarde van het object Hallo: **CloudQueueMessage.AsBytes** en **CloudQueueMessage.AsString**. **AsString** (gebruikt in dit voorbeeld) retourneert een tekenreeks, terwijl **AsBytes** retourneert een bytematrix.

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **wachtrijen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.

1. Op Hallo **weergave toevoegen** dialoogvenster Voer **PeekMessage** voor Hallo weergavenaam en selecteer **toevoegen**.

1. Open `PeekMessage.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:

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

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.

1. Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. Voer Hallo toepassing uit en selecteer **Peek bericht** toosee resulteert vergelijkbare toohello schermopname te volgen:
  
    ![Bericht](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a>Lezen en verwijderen van een bericht van een wachtrij

In deze sectie leest u hoe tooread en verwijderen van een bericht van een wachtrij.   

> [!NOTE]
> 
> Deze sectie wordt ervan uitgegaan dat u Hallo stappen hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment). 

1. Open Hallo `QueuesController.cs` bestand.

1. Toevoegen van een methode aangeroepen **gelezenBericht** die retourneert een **ActionResult**.

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Binnen Hallo **gelezenBericht** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account. Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Ophalen van een **CloudQueueClient** object vertegenwoordigt een queue-serviceclient.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Ophalen van een **CloudQueueContainer** -object met een verwijzing toohello wachtrij. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Hallo aanroepen **CloudQueue.GetMessage** methode tooread Hallo eerste bericht in Hallo wachtrij. Hallo **CloudQueue.GetMessage** Hallo bericht onzichtbaar voor 30 seconden (standaard) tooany andere codes die berichten lezen, zodat er geen andere code kunt wijzigen of verwijderen van het Hallo-bericht tijdens de verwerking van deze methode kunt u. toochange hello hoeveelheid tijd Hallo-bericht onzichtbaar is, wijzigt u Hallo **visibilityTimeout** parameter worden doorgegeven toohello **CloudQueue.GetMessage** methode.

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. Hallo aanroepen **CloudQueueMessage.Delete** methode toodelete Hallo-bericht uit de wachtrij Hallo.

    ```csharp
    queue.DeleteMessage(message);
    ```

1. Update Hallo **ViewBag** Hello bericht verwijderd en de naam van de wachtrij Hallo Hallo.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **wachtrijen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.

1. Op Hallo **weergave toevoegen** dialoogvenster Voer **gelezenBericht** voor Hallo weergavenaam en selecteer **toevoegen**.

1. Open `ReadMessage.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:

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

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.

1. Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. Voer Hallo toepassing uit en selecteer **Lees-/ verwijderingsbericht** toosee resulteert vergelijkbare toohello schermopname te volgen:
  
    ![Lezen en verwijderen van bericht](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a>Hallo-wachtrijlengte ophalen

Deze sectie ziet u hoe tooget Hallo wachtrijlengte (aantal berichten). 

> [!NOTE]
> 
> Deze sectie wordt ervan uitgegaan dat u Hallo stappen hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment). 

1. Open Hallo `QueuesController.cs` bestand.

1. Toevoegen van een methode aangeroepen **GetQueueLength** die retourneert een **ActionResult**.

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Binnen Hallo **gelezenBericht** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account. Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Ophalen van een **CloudQueueClient** object vertegenwoordigt een queue-serviceclient.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Ophalen van een **CloudQueueContainer** -object met een verwijzing toohello wachtrij. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Hallo aanroepen **CloudQueue.FetchAttributes** methode tooretrieve Hallo van wachtrij-kenmerken (met inbegrip van de lengte). 

    ```csharp
    queue.FetchAttributes();
    ```

6. Toegang Hallo **CloudQueue.ApproximateMessageCount** wachtrijlengte van eigenschap tooget Hallo.
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. Update Hallo **ViewBag** Hallo-naam van Hallo wachtrij en de lengte.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **wachtrijen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.

1. Op Hallo **weergave toevoegen** dialoogvenster Voer **GetQueueLength** voor Hallo weergavenaam en selecteer **toevoegen**.

1. Open `GetQueueLengthMessage.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.

1. Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. Voer Hallo toepassing uit en selecteer **ophalen wachtrijlengte** toosee resulteert vergelijkbare toohello schermopname te volgen:
  
    ![Wachtrijlengte ophalen](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a>Een wachtrij verwijderen
Deze sectie wordt beschreven hoe een wachtrij toodelete. 

> [!NOTE]
> 
> Deze sectie wordt ervan uitgegaan dat u Hallo stappen hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment). 

1. Open Hallo `QueuesController.cs` bestand.

1. Toevoegen van een methode aangeroepen **DeleteQueue** die retourneert een **ActionResult**.

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Binnen Hallo **DeleteQueue** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account. Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Ophalen van een **CloudQueueClient** object vertegenwoordigt een queue-serviceclient.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Ophalen van een **CloudQueueContainer** -object met een verwijzing toohello wachtrij. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Hallo aanroepen **CloudQueue.Delete** methode toodelete Hallo wachtrij vertegenwoordigd door Hallo **CloudQueue** object.

    ```csharp
    queue.Delete();
    ```

1. Update Hallo **ViewBag** Hallo-naam van Hallo wachtrij en de lengte.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **wachtrijen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.

1. Op Hallo **weergave toevoegen** dialoogvenster Voer **DeleteQueue** voor Hallo weergavenaam en selecteer **toevoegen**.

1. Open `DeleteQueue.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.

1. Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. Voer Hallo toepassing uit en selecteer **ophalen wachtrijlengte** toosee resulteert vergelijkbare toohello schermopname te volgen:
  
    ![Wachtrij verwijderen](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a>Volgende stappen
Bekijk meer functie handleidingen toolearn over aanvullende mogelijkheden voor het opslaan van gegevens in Azure.

  * [Aan de slag met Azure blob storage en Visual Studio verbonden Services (ASP.NET)](./vs-storage-aspnet-getting-started-blobs.md)
  * [Aan de slag met Azure-tabelopslag en Visual Studio verbonden Services (ASP.NET)](./vs-storage-aspnet-getting-started-tables.md)
