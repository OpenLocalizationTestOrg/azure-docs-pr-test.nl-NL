---
title: aaaGet de slag met Azure blob storage en Visual Studio verbonden Services (ASP.NET) | Microsoft Docs
description: Hoe tooget gestart met behulp van Azure blob-opslag in een ASP.NET-project in Visual Studio nadat u hebt aangesloten tooa storage-account met behulp van Visual Studio verbonden Services
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: b3497055-bef8-4c95-8567-181556b50d95
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: kraig
ms.openlocfilehash: 7b3e160da5bb95967ca4650b124afb8e867c03d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="b7204-103">Aan de slag met Azure blob storage en Visual Studio verbonden Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="b7204-103">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="b7204-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b7204-104">Overview</span></span>

<span data-ttu-id="b7204-105">Azure blob-opslag is een service die niet-gestructureerde gegevens in de cloud Hallo als objecten/blobs opslaat.</span><span class="sxs-lookup"><span data-stu-id="b7204-105">Azure blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="b7204-106">In Blob Storage kan elk type tekst of binaire gegevens, zoals een document, mediabestand of toepassingsinstallatieprogramma, worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="b7204-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="b7204-107">BLOB-opslag is ook bedoeld tooas vorm van objectopslag.</span><span class="sxs-lookup"><span data-stu-id="b7204-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="b7204-108">Deze zelfstudie laat zien hoe toowrite ASP.NET-code voor enkele algemene scenario's met behulp van Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="b7204-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure blob storage.</span></span> <span data-ttu-id="b7204-109">Scenario's omvatten een blob-container maken en uploaden, aanbieding, downloaden en verwijderen van blobs.</span><span class="sxs-lookup"><span data-stu-id="b7204-109">Scenarios include creating a blob container, and uploading, listing, downloading, and deleting blobs.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="b7204-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b7204-110">Prerequisites</span></span>

* [<span data-ttu-id="b7204-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b7204-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="b7204-112">Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="b7204-112">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="b7204-113">Maken van een MVC-controller</span><span class="sxs-lookup"><span data-stu-id="b7204-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="b7204-114">In Hallo **Solution Explorer**, met de rechtermuisknop op **domeincontrollers**, en selecteer in het contextmenu hello, **toevoegen -> Controller**.</span><span class="sxs-lookup"><span data-stu-id="b7204-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Een controller tooan ASP.NET MVC-app toevoegen](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. <span data-ttu-id="b7204-116">Op Hallo **Add Scaffold** dialoogvenster Selecteer **MVC 5 Controller - leeg**, en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b7204-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Geef een MVC-controller](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. <span data-ttu-id="b7204-118">Op Hallo **Controller toevoegen** dialoogvenster, naam Hallo controller *BlobsController*, en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b7204-118">On hello **Add Controller** dialog, name hello controller *BlobsController*, and select **Add**.</span></span>

    ![Naam Hallo MVC-controller](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. <span data-ttu-id="b7204-120">Voeg de volgende Hallo *met* richtlijnen toohello `BlobsController.cs` bestand:</span><span class="sxs-lookup"><span data-stu-id="b7204-120">Add hello following *using* directives toohello `BlobsController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a><span data-ttu-id="b7204-121">Een blob-container maken</span><span class="sxs-lookup"><span data-stu-id="b7204-121">Create a blob container</span></span>

<span data-ttu-id="b7204-122">Een blob-container is een geneste hiërarchie blobs en-mappen.</span><span class="sxs-lookup"><span data-stu-id="b7204-122">A blob container is a nested hierarchy of blobs and folders.</span></span> <span data-ttu-id="b7204-123">Hallo volgende stappen laten zien hoe toocreate een blob-container:</span><span class="sxs-lookup"><span data-stu-id="b7204-123">hello following steps illustrate how toocreate a blob container:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="b7204-124">Hallo code in deze sectie wordt ervan uitgegaan dat u de stappen in de sectie Hallo Hallo hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="b7204-124">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="b7204-125">Open Hallo `BlobsController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="b7204-125">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="b7204-126">Toevoegen van een methode aangeroepen **CreateBlobContainer** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="b7204-126">Add a method called **CreateBlobContainer** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="b7204-127">Binnen Hallo **CreateBlobContainer** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="b7204-127">Within hello **CreateBlobContainer** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b7204-128">Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsgegevens uit hello Azure-service-configuratie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b7204-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span> <span data-ttu-id="b7204-129">(Wijziging  *&lt;storage-account-name >* toohello naam Hallo u toegang hebt tot Azure storage-account.)</span><span class="sxs-lookup"><span data-stu-id="b7204-129">(Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="b7204-130">Ophalen van een **CloudBlobClient** object vertegenwoordigt een blob-service-client.</span><span class="sxs-lookup"><span data-stu-id="b7204-130">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="b7204-131">Ophalen van een **CloudBlobContainer** -object met een referentienaam toohello gewenste blob-container.</span><span class="sxs-lookup"><span data-stu-id="b7204-131">Get a **CloudBlobContainer** object that represents a reference toohello desired blob container name.</span></span> <span data-ttu-id="b7204-132">Hallo **CloudBlobClient.GetContainerReference** methode maakt u niet een aanvraag bij blob storage.</span><span class="sxs-lookup"><span data-stu-id="b7204-132">hello **CloudBlobClient.GetContainerReference** method does not make a request against blob storage.</span></span> <span data-ttu-id="b7204-133">Hallo verwijzing wordt geretourneerd of Hallo blob-container bestaat of niet.</span><span class="sxs-lookup"><span data-stu-id="b7204-133">hello reference is returned whether or not hello blob container exists.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="b7204-134">Hallo aanroepen **CloudBlobContainer.CreateIfNotExists** methode toocreate Hallo container als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="b7204-134">Call hello **CloudBlobContainer.CreateIfNotExists** method toocreate hello container if it does not yet exist.</span></span> <span data-ttu-id="b7204-135">Hallo **CloudBlobContainer.CreateIfNotExists** methode retourneert **true** als Hallo-container niet bestaat en is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b7204-135">hello **CloudBlobContainer.CreateIfNotExists** method returns **true** if hello container does not exist, and is successfully created.</span></span> <span data-ttu-id="b7204-136">Anders **false** wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b7204-136">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. <span data-ttu-id="b7204-137">Update Hallo **ViewBag** met de naam van de blob-container Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b7204-137">Update hello **ViewBag** with hello name of hello blob container.</span></span>

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. <span data-ttu-id="b7204-138">In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **Blobs**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="b7204-138">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b7204-139">Op Hallo **weergave toevoegen** dialoogvenster Voer **CreateBlobContainer** voor Hallo weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b7204-139">On hello **Add View** dialog, enter **CreateBlobContainer** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="b7204-140">Open `CreateBlobContainer.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="b7204-140">Open `CreateBlobContainer.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="b7204-141">In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="b7204-141">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b7204-142">Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="b7204-142">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. <span data-ttu-id="b7204-143">Voer Hallo toepassing uit en selecteer **Blob-Container maken** toosee resulteert vergelijkbare toohello schermopname te volgen:</span><span class="sxs-lookup"><span data-stu-id="b7204-143">Run hello application, and select **Create Blob Container** toosee results similar toohello following screen shot:</span></span>
  
    ![blob-container maken](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    <span data-ttu-id="b7204-145">Zoals eerder vermeld, Hallo **CloudBlobContainer.CreateIfNotExists** methode retourneert **true** alleen wanneer Hallo-container bestaat niet en is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b7204-145">As mentioned previously, hello **CloudBlobContainer.CreateIfNotExists** method returns **true** only when hello container doesn't exist and is created.</span></span> <span data-ttu-id="b7204-146">Dus als u Hallo-app wordt uitgevoerd wanneer het Hallo-container bestaat, Hallo methode retourneert **false**.</span><span class="sxs-lookup"><span data-stu-id="b7204-146">Therefore, if you run hello app when hello container exists, hello method returns **false**.</span></span> <span data-ttu-id="b7204-147">toorun Hallo app meerdere keren verwijdert u de container Hallo voordat Hallo app opnieuw uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="b7204-147">toorun hello app multiple times, you must delete hello container before running hello app again.</span></span> <span data-ttu-id="b7204-148">Verwijderen Hallo-container kan worden uitgevoerd via Hallo **CloudBlobContainer.Delete** methode.</span><span class="sxs-lookup"><span data-stu-id="b7204-148">Deleting hello container can be done via hello **CloudBlobContainer.Delete** method.</span></span> <span data-ttu-id="b7204-149">U kunt ook verwijderen met behulp van Hallo Hallo-container [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) of Hallo [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="b7204-149">You can also delete hello container using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="upload-a-blob-into-a-blob-container"></a><span data-ttu-id="b7204-150">Een blob uploaden naar een blob-container</span><span class="sxs-lookup"><span data-stu-id="b7204-150">Upload a blob into a blob container</span></span>

<span data-ttu-id="b7204-151">Zodra u hebt [een blob-container gemaakt](#create-a-blob-container), kunt u bestanden uploaden naar deze container.</span><span class="sxs-lookup"><span data-stu-id="b7204-151">Once you've [created a blob container](#create-a-blob-container), you can upload files into that container.</span></span> <span data-ttu-id="b7204-152">Deze sectie helpt u bij het uploaden van een lokaal bestand tooa blob-container.</span><span class="sxs-lookup"><span data-stu-id="b7204-152">This section walks you through uploading a local file tooa blob container.</span></span> <span data-ttu-id="b7204-153">Hallo stappen wordt ervan uitgegaan dat u hebt gemaakt dat een blob-container met de naam *test blobcontainer*.</span><span class="sxs-lookup"><span data-stu-id="b7204-153">hello steps assume you've created a blob container named *test-blob-container*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="b7204-154">Hallo code in deze sectie wordt ervan uitgegaan dat u de stappen in de sectie Hallo Hallo hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="b7204-154">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="b7204-155">Open Hallo `BlobsController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="b7204-155">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="b7204-156">Toevoegen van een methode aangeroepen **UploadBlob** die retourneert een **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="b7204-156">Add a method called **UploadBlob** that returns an **EmptyResult**.</span></span>

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="b7204-157">Binnen Hallo **UploadBlob** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="b7204-157">Within hello **UploadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b7204-158">Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="b7204-158">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="b7204-159">Ophalen van een **CloudBlobClient** object vertegenwoordigt een blob-service-client.</span><span class="sxs-lookup"><span data-stu-id="b7204-159">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="b7204-160">Ophalen van een **CloudBlobContainer** -object met een referentienaam toohello blob-container.</span><span class="sxs-lookup"><span data-stu-id="b7204-160">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="b7204-161">Zoals eerder beschreven, ondersteunt Azure storage blob met verschillende typen.</span><span class="sxs-lookup"><span data-stu-id="b7204-161">As explained earlier, Azure storage supports different blob types.</span></span> <span data-ttu-id="b7204-162">tooretrieve een verwijzing tooa pagina-blob aanroep Hallo **CloudBlobContainer.GetPageBlobReference** methode.</span><span class="sxs-lookup"><span data-stu-id="b7204-162">tooretrieve a reference tooa page blob, call hello **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="b7204-163">tooretrieve een verwijzing tooa blok-blob aanroep Hallo **CloudBlobContainer.GetBlockBlobReference** methode.</span><span class="sxs-lookup"><span data-stu-id="b7204-163">tooretrieve a reference tooa block blob, call hello **CloudBlobContainer.GetBlockBlobReference** method.</span></span> <span data-ttu-id="b7204-164">Blok-blob is meestal Hallo type toouse aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="b7204-164">Usually, block blob is hello recommended type toouse.</span></span> <span data-ttu-id="b7204-165">(Wijziging < blob-naam > * toohello naam toogive Hallo blob eenmaal geüpload.)</span><span class="sxs-lookup"><span data-stu-id="b7204-165">(Change <blob-name>* toohello name you want toogive hello blob once uploaded.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="b7204-166">Zodra u een blobverwijzing hebt, kunt u alle gegevensstroom tooit uploaden door het aanroepen van Hallo blob verwijzing van het object **UploadFromStream** methode.</span><span class="sxs-lookup"><span data-stu-id="b7204-166">Once you have a blob reference, you can upload any data stream tooit by calling hello blob reference object's **UploadFromStream** method.</span></span> <span data-ttu-id="b7204-167">Hallo **UploadFromStream** methode Hallo blob wordt gemaakt als deze niet bestaat, of deze wordt overschreven als deze bestaat.</span><span class="sxs-lookup"><span data-stu-id="b7204-167">hello **UploadFromStream** method creates hello blob if it doesn't exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="b7204-168">(Wijziging  *&lt;uploaden bestand >* tooa volledig gekwalificeerd pad toohello bestand gewenste tooupload.)</span><span class="sxs-lookup"><span data-stu-id="b7204-168">(Change *&lt;file-to-upload>* tooa fully qualified path toohello file you want tooupload.)</span></span>

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. <span data-ttu-id="b7204-169">In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **Blobs**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="b7204-169">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b7204-170">In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="b7204-170">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b7204-171">Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="b7204-171">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="b7204-172">Voer de toepassing hello en selecteer **blob uploaden**.</span><span class="sxs-lookup"><span data-stu-id="b7204-172">Run hello application, and select **Upload blob**.</span></span>  
  
<span data-ttu-id="b7204-173">sectie - Hallo [Hallo blobs in een blobcontainer lijst](#list-the-blobs-in-a-blob-container) -illustreert hoe toolist Hallo blobs in een blob-container.</span><span class="sxs-lookup"><span data-stu-id="b7204-173">hello section - [List hello blobs in a blob container](#list-the-blobs-in-a-blob-container) - illustrates how toolist hello blobs in a blob container.</span></span>  

## <a name="list-hello-blobs-in-a-blob-container"></a><span data-ttu-id="b7204-174">Lijst Hallo blobs in een blobcontainer</span><span class="sxs-lookup"><span data-stu-id="b7204-174">List hello blobs in a blob container</span></span>

<span data-ttu-id="b7204-175">Deze sectie ziet u hoe toolist Hallo blobs in een blob-container.</span><span class="sxs-lookup"><span data-stu-id="b7204-175">This section illustrates how toolist hello blobs in a blob container.</span></span> <span data-ttu-id="b7204-176">Hallo voorbeeldcode verwijst naar Hallo *test blobcontainer* gemaakt in de sectie hello, [maken van een blob-container](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="b7204-176">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

> [!NOTE]
> 
> <span data-ttu-id="b7204-177">Hallo code in deze sectie wordt ervan uitgegaan dat u de stappen in de sectie Hallo Hallo hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="b7204-177">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="b7204-178">Open Hallo `BlobsController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="b7204-178">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="b7204-179">Toevoegen van een methode aangeroepen **ListBlobs** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="b7204-179">Add a method called **ListBlobs** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="b7204-180">Binnen Hallo **ListBlobs** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="b7204-180">Within hello **ListBlobs** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b7204-181">Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="b7204-181">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="b7204-182">Ophalen van een **CloudBlobClient** object vertegenwoordigt een blob-service-client.</span><span class="sxs-lookup"><span data-stu-id="b7204-182">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="b7204-183">Ophalen van een **CloudBlobContainer** -object met een referentienaam toohello blob-container.</span><span class="sxs-lookup"><span data-stu-id="b7204-183">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="b7204-184">toolist hello blobs in een blob-container gebruiken Hallo **CloudBlobContainer.ListBlobs** methode.</span><span class="sxs-lookup"><span data-stu-id="b7204-184">toolist hello blobs in a blob container, use hello **CloudBlobContainer.ListBlobs** method.</span></span> <span data-ttu-id="b7204-185">Hallo **CloudBlobContainer.ListBlobs** methode retourneert een **IListBlobItem** object dat u tooa uitbrengt **CloudBlockBlob**, **CloudPageBlob**, of **CloudBlobDirectory** object.</span><span class="sxs-lookup"><span data-stu-id="b7204-185">hello **CloudBlobContainer.ListBlobs** method returns an **IListBlobItem** object that you cast tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="b7204-186">Hallo inventariseren volgende codefragment alle Hallo blobs in een blob-container.</span><span class="sxs-lookup"><span data-stu-id="b7204-186">hello following code snippet enumerates all hello blobs in a blob container.</span></span> <span data-ttu-id="b7204-187">Elke blob cast toohello juiste object op basis van het type en de naam ervan is (of URI in geval van Hallo een **CloudBlobDirectory**) tooa lijst wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="b7204-187">Each blob is cast toohello appropriate object based on its type, and its name (or URI in hello case of a **CloudBlobDirectory**) is added tooa list.</span></span>

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

    <span data-ttu-id="b7204-188">In toevoeging tooblobs, kunnen de blob-containers mappen bevatten.</span><span class="sxs-lookup"><span data-stu-id="b7204-188">In addition tooblobs, blob containers can contain directories.</span></span> <span data-ttu-id="b7204-189">Stel u hebt een blob-container aangeroepen *test blobcontainer* Hello hiërarchie te volgen:</span><span class="sxs-lookup"><span data-stu-id="b7204-189">Let's suppose you have a blob container called *test-blob-container* with hello following hierarchy:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

    <span data-ttu-id="b7204-190">Hallo voorgaande codevoorbeeld gebruikt, Hallo **blobs** tekenreekslijst waarden vergelijkbare toohello volgende bevat:</span><span class="sxs-lookup"><span data-stu-id="b7204-190">Using hello preceding code example, hello **blobs** string list contains values similar toohello following:</span></span>

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    <span data-ttu-id="b7204-191">Zoals u ziet, bevat Hallo lijst alleen Hallo op het hoogste niveau entiteiten; geen Hallo genest zijn (*bar.png* en *baz.png*).</span><span class="sxs-lookup"><span data-stu-id="b7204-191">As you can see, hello list includes only hello top-level entities; not hello nested ones (*bar.png* and *baz.png*).</span></span> <span data-ttu-id="b7204-192">toolist alle entiteiten in een blob-container Hallo, moet u Hallo aanroepen **CloudBlobContainer.ListBlobs** methode aan en geeft **true** voor Hallo **useFlatBlobListing** parameter.</span><span class="sxs-lookup"><span data-stu-id="b7204-192">toolist all hello entities within a blob container, you must call hello **CloudBlobContainer.ListBlobs** method and pass **true** for hello **useFlatBlobListing** parameter.</span></span>    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    <span data-ttu-id="b7204-193">Instelling Hallo **useFlatBlobListing** parameter te**true** retourneert een platte lijst van alle entiteiten in de blob-container Hallo en levert Hallo resultaten te volgen:</span><span class="sxs-lookup"><span data-stu-id="b7204-193">Setting hello **useFlatBlobListing** parameter too**true** returns a flat listing of all entities in hello blob container, and yields hello following results:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

1. <span data-ttu-id="b7204-194">In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **Blobs**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="b7204-194">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="b7204-195">Op Hallo **weergave toevoegen** dialoogvenster Voer **ListBlobs** voor Hallo weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b7204-195">On hello **Add View** dialog, enter **ListBlobs** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="b7204-196">Open `ListBlobs.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="b7204-196">Open `ListBlobs.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="b7204-197">In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="b7204-197">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b7204-198">Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="b7204-198">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. <span data-ttu-id="b7204-199">Voer Hallo toepassing uit en selecteer **lijst blobs** toosee resulteert vergelijkbare toohello schermopname te volgen:</span><span class="sxs-lookup"><span data-stu-id="b7204-199">Run hello application, and select **List blobs** toosee results similar toohello following screen shot:</span></span>
  
    ![BLOB-aanbieding](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a><span data-ttu-id="b7204-201">Blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="b7204-201">Download blobs</span></span>

<span data-ttu-id="b7204-202">Deze sectie ziet u hoe een blob toodownload vallen of persistent het toolocal opslag- of Hallo inhoud in een tekenreeks maken.</span><span class="sxs-lookup"><span data-stu-id="b7204-202">This section illustrates how toodownload a blob and either persist it toolocal storage or read hello contents into a string.</span></span> <span data-ttu-id="b7204-203">Hallo voorbeeldcode verwijst naar Hallo *test blobcontainer* gemaakt in de sectie hello, [maken van een blob-container](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="b7204-203">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

1. <span data-ttu-id="b7204-204">Open Hallo `BlobsController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="b7204-204">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="b7204-205">Toevoegen van een methode aangeroepen **DownloadBlob** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="b7204-205">Add a method called **DownloadBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="b7204-206">Binnen Hallo **DownloadBlob** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="b7204-206">Within hello **DownloadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b7204-207">Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="b7204-207">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="b7204-208">Ophalen van een **CloudBlobClient** object vertegenwoordigt een blob-service-client.</span><span class="sxs-lookup"><span data-stu-id="b7204-208">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="b7204-209">Ophalen van een **CloudBlobContainer** -object met een referentienaam toohello blob-container.</span><span class="sxs-lookup"><span data-stu-id="b7204-209">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="b7204-210">Een blob reference-object ophalen door het aanroepen van **CloudBlobContainer.GetBlockBlobReference** of **CloudBlobContainer.GetPageBlobReference** methode.</span><span class="sxs-lookup"><span data-stu-id="b7204-210">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="b7204-211">(Wijziging  *&lt;blob-naam >* toohello-naam van Hallo-blob die u downloadt.)</span><span class="sxs-lookup"><span data-stu-id="b7204-211">(Change *&lt;blob-name>* toohello name of hello blob you are downloading.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="b7204-212">een blob toodownload gebruiken Hallo **CloudBlockBlob.DownloadToStream** of **CloudPageBlob.DownloadToStream** methode, afhankelijk van Hallo blobtype.</span><span class="sxs-lookup"><span data-stu-id="b7204-212">toodownload a blob, use hello **CloudBlockBlob.DownloadToStream** or **CloudPageBlob.DownloadToStream** method, depending on hello blob type.</span></span> <span data-ttu-id="b7204-213">Hallo volgende codefragment wordt Hallo **CloudBlockBlob.DownloadToStream** methode tootransfer een blob inhoud tooa stroom dat object persistent vervolgens lokaal bestand tooa: (wijziging  *&lt;lokale bestandsnaam >* toohello volledig gekwalificeerd bestand naam die aangeeft waar u Hallo blob gedownload.)</span><span class="sxs-lookup"><span data-stu-id="b7204-213">hello following code snippet uses hello **CloudBlockBlob.DownloadToStream** method tootransfer a blob's contents tooa stream object that is then persisted tooa local file: (Change *&lt;local-file-name>* toohello fully qualified file name representing where you want hello blob downloaded.)</span></span> 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. <span data-ttu-id="b7204-214">In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="b7204-214">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b7204-215">Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="b7204-215">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="b7204-216">Voer de toepassing hello en selecteer **downloaden blob** toodownload Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="b7204-216">Run hello application, and select **Download blob** toodownload hello blob.</span></span> <span data-ttu-id="b7204-217">Hallo blob is opgegeven in Hallo **CloudBlobContainer.GetBlockBlobReference** methodeaanroep downloadt toohello-locatie die u in Hallo opgeeft **File.OpenWrite** methodeaanroep.</span><span class="sxs-lookup"><span data-stu-id="b7204-217">hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call downloads toohello location you specify in hello **File.OpenWrite** method call.</span></span> 

## <a name="delete-blobs"></a><span data-ttu-id="b7204-218">Blobs verwijderen</span><span class="sxs-lookup"><span data-stu-id="b7204-218">Delete blobs</span></span>

<span data-ttu-id="b7204-219">Hallo volgende stappen laten zien hoe een blob toodelete:</span><span class="sxs-lookup"><span data-stu-id="b7204-219">hello following steps illustrate how toodelete a blob:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="b7204-220">Hallo code in deze sectie wordt ervan uitgegaan dat u de stappen in de sectie Hallo Hallo hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="b7204-220">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="b7204-221">Open Hallo `BlobsController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="b7204-221">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="b7204-222">Toevoegen van een methode aangeroepen **DeleteBlob** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="b7204-222">Add a method called **DeleteBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. <span data-ttu-id="b7204-223">Ophalen van een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="b7204-223">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b7204-224">Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="b7204-224">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="b7204-225">Ophalen van een **CloudBlobClient** object vertegenwoordigt een blob-service-client.</span><span class="sxs-lookup"><span data-stu-id="b7204-225">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="b7204-226">Ophalen van een **CloudBlobContainer** -object met een referentienaam toohello blob-container.</span><span class="sxs-lookup"><span data-stu-id="b7204-226">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="b7204-227">Een blob reference-object ophalen door het aanroepen van **CloudBlobContainer.GetBlockBlobReference** of **CloudBlobContainer.GetPageBlobReference** methode.</span><span class="sxs-lookup"><span data-stu-id="b7204-227">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="b7204-228">(Wijziging  *&lt;blob-naam >* toohello-naam van Hallo-blob die u wilt verwijderen.)</span><span class="sxs-lookup"><span data-stu-id="b7204-228">(Change *&lt;blob-name>* toohello name of hello blob you are deleting.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. <span data-ttu-id="b7204-229">In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="b7204-229">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="b7204-230">Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="b7204-230">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="b7204-231">Voer Hallo toepassing uit en selecteer **verwijderen blob** toodelete Hallo blob is opgegeven in Hallo **CloudBlobContainer.GetBlockBlobReference** methodeaanroep.</span><span class="sxs-lookup"><span data-stu-id="b7204-231">Run hello application, and select **Delete blob** toodelete hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b7204-232">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b7204-232">Next steps</span></span>
<span data-ttu-id="b7204-233">Bekijk meer functie handleidingen toolearn over aanvullende mogelijkheden voor het opslaan van gegevens in Azure.</span><span class="sxs-lookup"><span data-stu-id="b7204-233">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="b7204-234">Aan de slag met Azure-tabelopslag en Visual Studio verbonden Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="b7204-234">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
  * [<span data-ttu-id="b7204-235">Aan de slag met Azure queue storage- en Visual Studio verbonden Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="b7204-235">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-queues.md)
