---
title: aaaGet de slag met Azure blob storage en Visual Studio verbonden Services (ASP.NET) | Microsoft Docs
description: Hoe tooget gestart met behulp van Azure blob-opslag in een ASP.NET-project in Visual Studio nadat u hebt aangesloten tooa storage-account met behulp van Visual Studio verbonden Services
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: b3497055-bef8-4c95-8567-181556b50d95
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: tarcher
ms.openlocfilehash: eb38889f239a63852d6928e8be10c3d3f1746e9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a>Aan de slag met Azure blob storage en Visual Studio verbonden Services (ASP.NET)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Overzicht

Azure blob-opslag is een service die niet-gestructureerde gegevens in de cloud Hallo als objecten/blobs opslaat. In Blob Storage kan elk type tekst of binaire gegevens, zoals een document, mediabestand of toepassingsinstallatieprogramma, worden opgeslagen. BLOB-opslag is ook bedoeld tooas vorm van objectopslag.

Deze zelfstudie laat zien hoe toowrite ASP.NET-code voor enkele algemene scenario's met behulp van Azure blob-opslag. Scenario's omvatten een blob-container maken en uploaden, aanbieding, downloaden en verwijderen van blobs.

##<a name="prerequisites"></a>Vereisten

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Azure Storage-account](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Maken van een MVC-controller 

1. In Hallo **Solution Explorer**, met de rechtermuisknop op **domeincontrollers**, en selecteer in het contextmenu hello, **toevoegen -> Controller**.

    ![Een controller tooan ASP.NET MVC-app toevoegen](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. Op Hallo **Add Scaffold** dialoogvenster Selecteer **MVC 5 Controller - leeg**, en selecteer **toevoegen**.

    ![Geef een MVC-controller](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. Op Hallo **Controller toevoegen** dialoogvenster, naam Hallo controller *BlobsController*, en selecteer **toevoegen**.

    ![Naam Hallo MVC-controller](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. Voeg de volgende Hallo *met* richtlijnen toohello `BlobsController.cs` bestand:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a>Een blob-container maken

Een blob-container is een geneste hiërarchie blobs en-mappen. Hallo volgende stappen laten zien hoe toocreate een blob-container:

> [!NOTE]
> 
> Hallo code in deze sectie wordt ervan uitgegaan dat u de stappen in de sectie Hallo Hallo hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment). 

1. Open Hallo `BlobsController.cs` bestand.

1. Toevoegen van een methode aangeroepen **CreateBlobContainer** die retourneert een **ActionResult**.

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Binnen Hallo **CreateBlobContainer** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account. Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsgegevens uit hello Azure-service-configuratie gebruiken. (Wijziging  *&lt;storage-account-name >* toohello naam Hallo u toegang hebt tot Azure storage-account.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Ophalen van een **CloudBlobClient** object vertegenwoordigt een blob-service-client.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Ophalen van een **CloudBlobContainer** -object met een referentienaam toohello gewenste blob-container. Hallo **CloudBlobClient.GetContainerReference** methode maakt u niet een aanvraag bij blob storage. Hallo verwijzing wordt geretourneerd of Hallo blob-container bestaat of niet. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Hallo aanroepen **CloudBlobContainer.CreateIfNotExists** methode toocreate Hallo container als deze nog niet bestaat. Hallo **CloudBlobContainer.CreateIfNotExists** methode retourneert **true** als Hallo-container niet bestaat en is gemaakt. Anders **false** wordt geretourneerd.    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. Update Hallo **ViewBag** met de naam van de blob-container Hallo Hallo.

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **Blobs**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.

1. Op Hallo **weergave toevoegen** dialoogvenster Voer **CreateBlobContainer** voor Hallo weergavenaam en selecteer **toevoegen**.

1. Open `CreateBlobContainer.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.

1. Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. Voer Hallo toepassing uit en selecteer **Blob-Container maken** toosee resulteert vergelijkbare toohello schermopname te volgen:
  
    ![blob-container maken](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    Zoals eerder vermeld, Hallo **CloudBlobContainer.CreateIfNotExists** methode retourneert **true** alleen wanneer Hallo-container bestaat niet en is gemaakt. Dus als u Hallo-app wordt uitgevoerd wanneer het Hallo-container bestaat, Hallo methode retourneert **false**. toorun Hallo app meerdere keren verwijdert u de container Hallo voordat Hallo app opnieuw uit te voeren. Verwijderen Hallo-container kan worden uitgevoerd via Hallo **CloudBlobContainer.Delete** methode. U kunt ook verwijderen met behulp van Hallo Hallo-container [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) of Hallo [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="upload-a-blob-into-a-blob-container"></a>Een blob uploaden naar een blob-container

Zodra u hebt [een blob-container gemaakt](#create-a-blob-container), kunt u bestanden uploaden naar deze container. Deze sectie helpt u bij het uploaden van een lokaal bestand tooa blob-container. Hallo stappen wordt ervan uitgegaan dat u hebt gemaakt dat een blob-container met de naam *test blobcontainer*. 

> [!NOTE]
> 
> Hallo code in deze sectie wordt ervan uitgegaan dat u de stappen in de sectie Hallo Hallo hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment). 

1. Open Hallo `BlobsController.cs` bestand.

1. Toevoegen van een methode aangeroepen **UploadBlob** die retourneert een **EmptyResult**.

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. Binnen Hallo **UploadBlob** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account. Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Ophalen van een **CloudBlobClient** object vertegenwoordigt een blob-service-client.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Ophalen van een **CloudBlobContainer** -object met een referentienaam toohello blob-container. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Zoals eerder beschreven, ondersteunt Azure storage blob met verschillende typen. tooretrieve een verwijzing tooa pagina-blob aanroep Hallo **CloudBlobContainer.GetPageBlobReference** methode. tooretrieve een verwijzing tooa blok-blob aanroep Hallo **CloudBlobContainer.GetBlockBlobReference** methode. Blok-blob is meestal Hallo type toouse aanbevolen. (Wijziging < blob-naam > * toohello naam toogive Hallo blob eenmaal geüpload.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. Zodra u een blobverwijzing hebt, kunt u alle gegevensstroom tooit uploaden door het aanroepen van Hallo blob verwijzing van het object **UploadFromStream** methode. Hallo **UploadFromStream** methode Hallo blob wordt gemaakt als deze niet bestaat, of deze wordt overschreven als deze bestaat. (Wijziging  *&lt;uploaden bestand >* tooa volledig gekwalificeerd pad toohello bestand gewenste tooupload.)

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **Blobs**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.

1. Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. Voer de toepassing hello en selecteer **blob uploaden**.  
  
sectie - Hallo [Hallo blobs in een blobcontainer lijst](#list-the-blobs-in-a-blob-container) -illustreert hoe toolist Hallo blobs in een blob-container.  

## <a name="list-hello-blobs-in-a-blob-container"></a>Lijst Hallo blobs in een blobcontainer

Deze sectie ziet u hoe toolist Hallo blobs in een blob-container. Hallo voorbeeldcode verwijst naar Hallo *test blobcontainer* gemaakt in de sectie hello, [maken van een blob-container](#create-a-blob-container).

> [!NOTE]
> 
> Hallo code in deze sectie wordt ervan uitgegaan dat u de stappen in de sectie Hallo Hallo hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment). 

1. Open Hallo `BlobsController.cs` bestand.

1. Toevoegen van een methode aangeroepen **ListBlobs** die retourneert een **ActionResult**.

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Binnen Hallo **ListBlobs** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account. Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Ophalen van een **CloudBlobClient** object vertegenwoordigt een blob-service-client.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Ophalen van een **CloudBlobContainer** -object met een referentienaam toohello blob-container. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. toolist hello blobs in een blob-container gebruiken Hallo **CloudBlobContainer.ListBlobs** methode. Hallo **CloudBlobContainer.ListBlobs** methode retourneert een **IListBlobItem** object dat u tooa uitbrengt **CloudBlockBlob**, **CloudPageBlob**, of **CloudBlobDirectory** object. Hallo inventariseren volgende codefragment alle Hallo blobs in een blob-container. Elke blob cast toohello juiste object op basis van het type en de naam ervan is (of URI in geval van Hallo een **CloudBlobDirectory**) tooa lijst wordt toegevoegd.

    ```csharp
    List<string> blobs = new List<string>();

    foreach (IListBlobItem item in container.ListBlobs(null, false))
    {
        if (item.GetType() == typeof(CloudBlockBlob))
        {
            CloudBlockBlob blob = (CloudBlockBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudPageBlob))
        {
            CloudPageBlob blob = (CloudPageBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudBlobDirectory))
        {
            CloudBlobDirectory dir = (CloudBlobDirectory)item;
            blobs.Add(dir.Uri.ToString());
        }
    }

    return View(blobs);
    ```

    In toevoeging tooblobs, kunnen de blob-containers mappen bevatten. Stel u hebt een blob-container aangeroepen *test blobcontainer* Hello hiërarchie te volgen:

        foo.png
        dir1/bar.png
        dir2/baz.png

    Hallo voorgaande codevoorbeeld gebruikt, Hallo **blobs** tekenreekslijst waarden vergelijkbare toohello volgende bevat:

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    Zoals u ziet, bevat Hallo lijst alleen Hallo op het hoogste niveau entiteiten; geen Hallo genest zijn (*bar.png* en *baz.png*). toolist alle entiteiten in een blob-container Hallo, moet u Hallo aanroepen **CloudBlobContainer.ListBlobs** methode aan en geeft **true** voor Hallo **useFlatBlobListing** parameter.    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    Instelling Hallo **useFlatBlobListing** parameter te**true** retourneert een platte lijst van alle entiteiten in de blob-container Hallo en levert Hallo resultaten te volgen:

        foo.png
        dir1/bar.png
        dir2/baz.png

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **Blobs**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.

1. Op Hallo **weergave toevoegen** dialoogvenster Voer **ListBlobs** voor Hallo weergavenaam en selecteer **toevoegen**.

1. Open `ListBlobs.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:

    ```html
    @model List<string>
    @{
        ViewBag.Title = "List blobs";
    }
    
    <h2>List blobs</h2>
    
    <ul>
        @foreach (var item in Model)
        {
        <li>@item</li>
        }
    </ul>
    ```

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.

1. Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. Voer Hallo toepassing uit en selecteer **lijst blobs** toosee resulteert vergelijkbare toohello schermopname te volgen:
  
    ![BLOB-aanbieding](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a>Blobs downloaden

Deze sectie ziet u hoe een blob toodownload vallen of persistent het toolocal opslag- of Hallo inhoud in een tekenreeks maken. Hallo voorbeeldcode verwijst naar Hallo *test blobcontainer* gemaakt in de sectie hello, [maken van een blob-container](#create-a-blob-container).

1. Open Hallo `BlobsController.cs` bestand.

1. Toevoegen van een methode aangeroepen **DownloadBlob** die retourneert een **ActionResult**.

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. Binnen Hallo **DownloadBlob** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account. Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Ophalen van een **CloudBlobClient** object vertegenwoordigt een blob-service-client.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Ophalen van een **CloudBlobContainer** -object met een referentienaam toohello blob-container. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Een blob reference-object ophalen door het aanroepen van **CloudBlobContainer.GetBlockBlobReference** of **CloudBlobContainer.GetPageBlobReference** methode. (Wijziging  *&lt;blob-naam >* toohello-naam van Hallo-blob die u downloadt.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. een blob toodownload gebruiken Hallo **CloudBlockBlob.DownloadToStream** of **CloudPageBlob.DownloadToStream** methode, afhankelijk van Hallo blobtype. Hallo volgende codefragment wordt Hallo **CloudBlockBlob.DownloadToStream** methode tootransfer een blob inhoud tooa stroom dat object persistent vervolgens lokaal bestand tooa: (wijziging  *&lt;lokale bestandsnaam >* toohello volledig gekwalificeerd bestand naam die aangeeft waar u Hallo blob gedownload.) 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.

1. Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. Voer de toepassing hello en selecteer **downloaden blob** toodownload Hallo blob. Hallo blob is opgegeven in Hallo **CloudBlobContainer.GetBlockBlobReference** methodeaanroep downloadt toohello-locatie die u in Hallo opgeeft **File.OpenWrite** methodeaanroep. 

## <a name="delete-blobs"></a>Blobs verwijderen

Hallo volgende stappen laten zien hoe een blob toodelete:

> [!NOTE]
> 
> Hallo code in deze sectie wordt ervan uitgegaan dat u de stappen in de sectie Hallo Hallo hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment). 

1. Open Hallo `BlobsController.cs` bestand.

1. Toevoegen van een methode aangeroepen **DeleteBlob** die retourneert een **ActionResult**.

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. Ophalen van een **CloudStorageAccount** -object met gegevens over uw storage-account. Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Ophalen van een **CloudBlobClient** object vertegenwoordigt een blob-service-client.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Ophalen van een **CloudBlobContainer** -object met een referentienaam toohello blob-container. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Een blob reference-object ophalen door het aanroepen van **CloudBlobContainer.GetBlockBlobReference** of **CloudBlobContainer.GetPageBlobReference** methode. (Wijziging  *&lt;blob-naam >* toohello-naam van Hallo-blob die u wilt verwijderen.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.

1. Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. Voer Hallo toepassing uit en selecteer **verwijderen blob** toodelete Hallo blob is opgegeven in Hallo **CloudBlobContainer.GetBlockBlobReference** methodeaanroep. 

## <a name="next-steps"></a>Volgende stappen
Bekijk meer functie handleidingen toolearn over aanvullende mogelijkheden voor het opslaan van gegevens in Azure.

  * [Aan de slag met Azure-tabelopslag en Visual Studio verbonden Services (ASP.NET)](./vs-storage-aspnet-getting-started-tables.md)
  * [Aan de slag met Azure queue storage- en Visual Studio verbonden Services (ASP.NET)](./vs-storage-aspnet-getting-started-queues.md)
