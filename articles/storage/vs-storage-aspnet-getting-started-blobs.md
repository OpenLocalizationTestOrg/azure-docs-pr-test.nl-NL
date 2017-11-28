---
title: Aan de slag met Azure blob storage en Visual Studio verbonden Services (ASP.NET) | Microsoft Docs
description: Hoe u aan de slag met Azure blob-opslag in een ASP.NET-project in Visual Studio nadat u een opslagaccount met behulp van Visual Studio verbonden Services
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
ms.openlocfilehash: 8fd13efdbdd98c6d7dff1b88a6b232a08aa5a13d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="97077-103">Aan de slag met Azure blob storage en Visual Studio verbonden Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="97077-103">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="97077-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="97077-104">Overview</span></span>

<span data-ttu-id="97077-105">Azure blob-opslag is een service die niet-gestructureerde gegevens in de cloud als objecten/blobs opslaat.</span><span class="sxs-lookup"><span data-stu-id="97077-105">Azure blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="97077-106">In Blob Storage kan elk type tekst of binaire gegevens, zoals een document, mediabestand of toepassingsinstallatieprogramma, worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="97077-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="97077-107">U kunt Blob Storage zien als een vorm van objectopslag.</span><span class="sxs-lookup"><span data-stu-id="97077-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="97077-108">Deze zelfstudie laat zien hoe ASP.NET code schrijven voor enkele algemene scenario's met behulp van Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="97077-108">This tutorial shows how to write ASP.NET code for some common scenarios using Azure blob storage.</span></span> <span data-ttu-id="97077-109">Scenario's omvatten een blob-container maken en uploaden, aanbieding, downloaden en verwijderen van blobs.</span><span class="sxs-lookup"><span data-stu-id="97077-109">Scenarios include creating a blob container, and uploading, listing, downloading, and deleting blobs.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="97077-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="97077-110">Prerequisites</span></span>

* [<span data-ttu-id="97077-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="97077-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="97077-112">Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="97077-112">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="97077-113">Maken van een MVC-controller</span><span class="sxs-lookup"><span data-stu-id="97077-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="97077-114">In de **Solution Explorer**, met de rechtermuisknop op **domeincontrollers**, en selecteer in het contextmenu **toevoegen -> Controller**.</span><span class="sxs-lookup"><span data-stu-id="97077-114">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![Een domeincontroller toevoegen aan een ASP.NET MVC-app](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. <span data-ttu-id="97077-116">Op de **Add Scaffold** dialoogvenster Selecteer **MVC 5 Controller - leeg**, en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="97077-116">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Geef een MVC-controller](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. <span data-ttu-id="97077-118">Op de **Controller toevoegen** dialoogvenster, de naam van de controller *BlobsController*, en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="97077-118">On the **Add Controller** dialog, name the controller *BlobsController*, and select **Add**.</span></span>

    ![De naam van de MVC-controller](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. <span data-ttu-id="97077-120">Voeg de volgende *met* richtlijnen voor de `BlobsController.cs` bestand:</span><span class="sxs-lookup"><span data-stu-id="97077-120">Add the following *using* directives to the `BlobsController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a><span data-ttu-id="97077-121">Een blob-container maken</span><span class="sxs-lookup"><span data-stu-id="97077-121">Create a blob container</span></span>

<span data-ttu-id="97077-122">Een blob-container is een geneste hiërarchie blobs en-mappen.</span><span class="sxs-lookup"><span data-stu-id="97077-122">A blob container is a nested hierarchy of blobs and folders.</span></span> <span data-ttu-id="97077-123">De volgende stappen laten zien hoe u van een blob-container:</span><span class="sxs-lookup"><span data-stu-id="97077-123">The following steps illustrate how to create a blob container:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="97077-124">De code in deze sectie wordt ervan uitgegaan dat u de stappen in de sectie hebt voltooid [de ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="97077-124">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="97077-125">Open het `BlobsController.cs`-bestand.</span><span class="sxs-lookup"><span data-stu-id="97077-125">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="97077-126">Toevoegen van een methode aangeroepen **CreateBlobContainer** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="97077-126">Add a method called **CreateBlobContainer** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="97077-127">Binnen de **CreateBlobContainer** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="97077-127">Within the **CreateBlobContainer** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="97077-128">Gebruik de volgende code de verbindingsreeks voor opslag en storage-account-gegevens ophalen uit de configuratie van de Azure-service.</span><span class="sxs-lookup"><span data-stu-id="97077-128">Use the following code to get the storage connection string and storage account information from the Azure service configuration.</span></span> <span data-ttu-id="97077-129">(Wijziging  *&lt;storage-account-name >* op de naam van de Azure storage-account u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="97077-129">(Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="97077-130">Ophalen van een **CloudBlobClient** object vertegenwoordigt een blob-service-client.</span><span class="sxs-lookup"><span data-stu-id="97077-130">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="97077-131">Ophalen van een **CloudBlobContainer** -object met een verwijzing naar de naam van de gewenste blob-container.</span><span class="sxs-lookup"><span data-stu-id="97077-131">Get a **CloudBlobContainer** object that represents a reference to the desired blob container name.</span></span> <span data-ttu-id="97077-132">De **CloudBlobClient.GetContainerReference** methode maakt u niet een aanvraag bij blob storage.</span><span class="sxs-lookup"><span data-stu-id="97077-132">The **CloudBlobClient.GetContainerReference** method does not make a request against blob storage.</span></span> <span data-ttu-id="97077-133">De verwijzing wordt geretourneerd of de blob-container bestaat of niet.</span><span class="sxs-lookup"><span data-stu-id="97077-133">The reference is returned whether or not the blob container exists.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="97077-134">Roep de **CloudBlobContainer.CreateIfNotExists** methode voor het maken van de container als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="97077-134">Call the **CloudBlobContainer.CreateIfNotExists** method to create the container if it does not yet exist.</span></span> <span data-ttu-id="97077-135">De **CloudBlobContainer.CreateIfNotExists** methode retourneert **true** als de container niet bestaat en is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="97077-135">The **CloudBlobContainer.CreateIfNotExists** method returns **true** if the container does not exist, and is successfully created.</span></span> <span data-ttu-id="97077-136">Anders **false** wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="97077-136">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. <span data-ttu-id="97077-137">Update de **ViewBag** met de naam van de blob-container.</span><span class="sxs-lookup"><span data-stu-id="97077-137">Update the **ViewBag** with the name of the blob container.</span></span>

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. <span data-ttu-id="97077-138">In de **Solution Explorer**, vouw de **weergaven** map met de rechtermuisknop op **Blobs**, en selecteer in het contextmenu **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="97077-138">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="97077-139">Op de **weergave toevoegen** dialoogvenster Voer **CreateBlobContainer** voor de weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="97077-139">On the **Add View** dialog, enter **CreateBlobContainer** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="97077-140">Open `CreateBlobContainer.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment:</span><span class="sxs-lookup"><span data-stu-id="97077-140">Open `CreateBlobContainer.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="97077-141">In de **Solution Explorer**, vouw de **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="97077-141">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="97077-142">Nadat de laatste **Html.ActionLink**, voeg de volgende **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="97077-142">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. <span data-ttu-id="97077-143">Voer de toepassing en selecteer **Blob-Container maken** om vergelijkbaar met de volgende schermopname resultaten te bekijken:</span><span class="sxs-lookup"><span data-stu-id="97077-143">Run the application, and select **Create Blob Container** to see results similar to the following screen shot:</span></span>
  
    ![blob-container maken](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    <span data-ttu-id="97077-145">Zoals eerder vermeld de **CloudBlobContainer.CreateIfNotExists** methode retourneert **true** alleen wanneer de container bestaat niet en is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="97077-145">As mentioned previously, the **CloudBlobContainer.CreateIfNotExists** method returns **true** only when the container doesn't exist and is created.</span></span> <span data-ttu-id="97077-146">Dus als u de app uitvoeren wanneer de container bestaat, retourneert de methode **false**.</span><span class="sxs-lookup"><span data-stu-id="97077-146">Therefore, if you run the app when the container exists, the method returns **false**.</span></span> <span data-ttu-id="97077-147">Als u wilt de app meerdere keren uitvoert, moet u de container verwijderen voordat u de app opnieuw uitvoert.</span><span class="sxs-lookup"><span data-stu-id="97077-147">To run the app multiple times, you must delete the container before running the app again.</span></span> <span data-ttu-id="97077-148">Verwijderen van de container kan worden uitgevoerd via de **CloudBlobContainer.Delete** methode.</span><span class="sxs-lookup"><span data-stu-id="97077-148">Deleting the container can be done via the **CloudBlobContainer.Delete** method.</span></span> <span data-ttu-id="97077-149">U kunt ook verwijderen voor de container met behulp van de [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) of de [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="97077-149">You can also delete the container using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="upload-a-blob-into-a-blob-container"></a><span data-ttu-id="97077-150">Een blob uploaden naar een blob-container</span><span class="sxs-lookup"><span data-stu-id="97077-150">Upload a blob into a blob container</span></span>

<span data-ttu-id="97077-151">Zodra u hebt [een blob-container gemaakt](#create-a-blob-container), kunt u bestanden uploaden naar deze container.</span><span class="sxs-lookup"><span data-stu-id="97077-151">Once you've [created a blob container](#create-a-blob-container), you can upload files into that container.</span></span> <span data-ttu-id="97077-152">Deze sectie helpt u bij het uploaden van een lokaal bestand naar een blob-container.</span><span class="sxs-lookup"><span data-stu-id="97077-152">This section walks you through uploading a local file to a blob container.</span></span> <span data-ttu-id="97077-153">De stappen wordt ervan uitgegaan dat u hebt gemaakt dat een blob-container met de naam *test blobcontainer*.</span><span class="sxs-lookup"><span data-stu-id="97077-153">The steps assume you've created a blob container named *test-blob-container*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="97077-154">De code in deze sectie wordt ervan uitgegaan dat u de stappen in de sectie hebt voltooid [de ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="97077-154">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="97077-155">Open het `BlobsController.cs`-bestand.</span><span class="sxs-lookup"><span data-stu-id="97077-155">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="97077-156">Toevoegen van een methode aangeroepen **UploadBlob** die retourneert een **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="97077-156">Add a method called **UploadBlob** that returns an **EmptyResult**.</span></span>

    ```csharp
    public EmptyResult UploadBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="97077-157">Binnen de **UploadBlob** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="97077-157">Within the **UploadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="97077-158">Gebruik de volgende code de verbindingsreeks voor opslag en storage-account-gegevens ophalen uit de configuratie van Azure service: (wijziging  *&lt;storage-account-name >* op de naam van de Azure storage-account u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="97077-158">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="97077-159">Ophalen van een **CloudBlobClient** object vertegenwoordigt een blob-service-client.</span><span class="sxs-lookup"><span data-stu-id="97077-159">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="97077-160">Ophalen van een **CloudBlobContainer** -object met een verwijzing naar de naam van de blob-container.</span><span class="sxs-lookup"><span data-stu-id="97077-160">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="97077-161">Zoals eerder beschreven, ondersteunt Azure storage blob met verschillende typen.</span><span class="sxs-lookup"><span data-stu-id="97077-161">As explained earlier, Azure storage supports different blob types.</span></span> <span data-ttu-id="97077-162">Aanroepen voor het ophalen van een verwijzing naar een pagina-blob, de **CloudBlobContainer.GetPageBlobReference** methode.</span><span class="sxs-lookup"><span data-stu-id="97077-162">To retrieve a reference to a page blob, call the **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="97077-163">Aanroepen voor het ophalen van een verwijzing naar een blok-blob, de **CloudBlobContainer.GetBlockBlobReference** methode.</span><span class="sxs-lookup"><span data-stu-id="97077-163">To retrieve a reference to a block blob, call the **CloudBlobContainer.GetBlockBlobReference** method.</span></span> <span data-ttu-id="97077-164">Meestal is de blok-blob het aangewezen type om te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="97077-164">Usually, block blob is the recommended type to use.</span></span> <span data-ttu-id="97077-165">(Wijziging < blob-naam > * op de naam die u wilt geven de blob eenmaal geüpload.)</span><span class="sxs-lookup"><span data-stu-id="97077-165">(Change <blob-name>* to the name you want to give the blob once uploaded.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="97077-166">Zodra u een blobverwijzing hebt, kunt u elke gewenste gegevensstroom gegevens uploaden naar het door het aanroepen van de blob-verwijzingsobject **UploadFromStream** methode.</span><span class="sxs-lookup"><span data-stu-id="97077-166">Once you have a blob reference, you can upload any data stream to it by calling the blob reference object's **UploadFromStream** method.</span></span> <span data-ttu-id="97077-167">De **UploadFromStream** methode maakt u de blob als deze niet bestaat, of deze wordt overschreven als deze bestaat.</span><span class="sxs-lookup"><span data-stu-id="97077-167">The **UploadFromStream** method creates the blob if it doesn't exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="97077-168">(Wijziging  *&lt;uploaden bestand >* naar een volledig gekwalificeerde pad naar het bestand dat u wilt uploaden.)</span><span class="sxs-lookup"><span data-stu-id="97077-168">(Change *&lt;file-to-upload>* to a fully qualified path to the file you want to upload.)</span></span>

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. <span data-ttu-id="97077-169">In de **Solution Explorer**, vouw de **weergaven** map met de rechtermuisknop op **Blobs**, en selecteer in het contextmenu **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="97077-169">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="97077-170">In de **Solution Explorer**, vouw de **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="97077-170">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="97077-171">Nadat de laatste **Html.ActionLink**, voeg de volgende **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="97077-171">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="97077-172">Voer de toepassing en selecteer **blob uploaden**.</span><span class="sxs-lookup"><span data-stu-id="97077-172">Run the application, and select **Upload blob**.</span></span>  
  
<span data-ttu-id="97077-173">De sectie - [lijst van de blobs in een blob-container](#list-the-blobs-in-a-blob-container) -ziet u hoe u de blobs in een blob-container.</span><span class="sxs-lookup"><span data-stu-id="97077-173">The section - [List the blobs in a blob container](#list-the-blobs-in-a-blob-container) - illustrates how to list the blobs in a blob container.</span></span>    

## <a name="list-the-blobs-in-a-blob-container"></a><span data-ttu-id="97077-174">Lijst van de blobs in een blob-container</span><span class="sxs-lookup"><span data-stu-id="97077-174">List the blobs in a blob container</span></span>

<span data-ttu-id="97077-175">Deze sectie ziet u hoe u de blobs in een blob-container.</span><span class="sxs-lookup"><span data-stu-id="97077-175">This section illustrates how to list the blobs in a blob container.</span></span> <span data-ttu-id="97077-176">De voorbeeld-code verwijst naar de *test blobcontainer* gemaakt in de sectie [maken van een blob-container](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="97077-176">The sample code references the *test-blob-container* created in the section, [Create a blob container](#create-a-blob-container).</span></span>

> [!NOTE]
> 
> <span data-ttu-id="97077-177">De code in deze sectie wordt ervan uitgegaan dat u de stappen in de sectie hebt voltooid [de ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="97077-177">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="97077-178">Open het `BlobsController.cs`-bestand.</span><span class="sxs-lookup"><span data-stu-id="97077-178">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="97077-179">Toevoegen van een methode aangeroepen **ListBlobs** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="97077-179">Add a method called **ListBlobs** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ListBlobs()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="97077-180">Binnen de **ListBlobs** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="97077-180">Within the **ListBlobs** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="97077-181">Gebruik de volgende code de verbindingsreeks voor opslag en storage-account-gegevens ophalen uit de configuratie van Azure service: (wijziging  *&lt;storage-account-name >* op de naam van de Azure storage-account u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="97077-181">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="97077-182">Ophalen van een **CloudBlobClient** object vertegenwoordigt een blob-service-client.</span><span class="sxs-lookup"><span data-stu-id="97077-182">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="97077-183">Ophalen van een **CloudBlobContainer** -object met een verwijzing naar de naam van de blob-container.</span><span class="sxs-lookup"><span data-stu-id="97077-183">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="97077-184">Als de blobs in een blob-container wilt weergeven, gebruikt de **CloudBlobContainer.ListBlobs** methode.</span><span class="sxs-lookup"><span data-stu-id="97077-184">To list the blobs in a blob container, use the **CloudBlobContainer.ListBlobs** method.</span></span> <span data-ttu-id="97077-185">De **CloudBlobContainer.ListBlobs** methode retourneert een **IListBlobItem** -object dat u geconverteerd naar een **CloudBlockBlob**, **CloudPageBlob**, of **CloudBlobDirectory** object.</span><span class="sxs-lookup"><span data-stu-id="97077-185">The **CloudBlobContainer.ListBlobs** method returns an **IListBlobItem** object that you cast to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="97077-186">Het volgende codefragment inventariseren alle blobs in een blob-container.</span><span class="sxs-lookup"><span data-stu-id="97077-186">The following code snippet enumerates all the blobs in a blob container.</span></span> <span data-ttu-id="97077-187">Elke blob is geconverteerd naar het juiste object op basis van het type en de naam ervan (of URI in het geval van een **CloudBlobDirectory**) is toegevoegd aan de lijst.</span><span class="sxs-lookup"><span data-stu-id="97077-187">Each blob is cast to the appropriate object based on its type, and its name (or URI in the case of a **CloudBlobDirectory**) is added to a list.</span></span>

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

    <span data-ttu-id="97077-188">Naast blobs, kunnen de blob-containers mappen bevatten.</span><span class="sxs-lookup"><span data-stu-id="97077-188">In addition to blobs, blob containers can contain directories.</span></span> <span data-ttu-id="97077-189">Stel u hebt een blob-container aangeroepen *test blobcontainer* met de volgende hiërarchie:</span><span class="sxs-lookup"><span data-stu-id="97077-189">Let's suppose you have a blob container called *test-blob-container* with the following hierarchy:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

    <span data-ttu-id="97077-190">Met behulp van het voorgaande voorbeeld, de **blobs** lijst vergelijkbaar met de volgende waarden bevat:</span><span class="sxs-lookup"><span data-stu-id="97077-190">Using the preceding code example, the **blobs** string list contains values similar to the following:</span></span>

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    <span data-ttu-id="97077-191">Zoals u ziet, bevat de lijst alleen de site op het hoogste entiteiten; geen geneste die (*bar.png* en *baz.png*).</span><span class="sxs-lookup"><span data-stu-id="97077-191">As you can see, the list includes only the top-level entities; not the nested ones (*bar.png* and *baz.png*).</span></span> <span data-ttu-id="97077-192">Als alle entiteiten in een blob-container wilt weergeven, moet u aanroepen de **CloudBlobContainer.ListBlobs** methode aan en geeft **true** voor de **useFlatBlobListing** parameter.</span><span class="sxs-lookup"><span data-stu-id="97077-192">To list all the entities within a blob container, you must call the **CloudBlobContainer.ListBlobs** method and pass **true** for the **useFlatBlobListing** parameter.</span></span>    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    <span data-ttu-id="97077-193">Instellen van de **useFlatBlobListing** -parameter voor **true** retourneert een platte lijst van alle entiteiten in de blob-container en levert de volgende resultaten:</span><span class="sxs-lookup"><span data-stu-id="97077-193">Setting the **useFlatBlobListing** parameter to **true** returns a flat listing of all entities in the blob container, and yields the following results:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

1. <span data-ttu-id="97077-194">In de **Solution Explorer**, vouw de **weergaven** map met de rechtermuisknop op **Blobs**, en selecteer in het contextmenu **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="97077-194">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="97077-195">Op de **weergave toevoegen** dialoogvenster Voer **ListBlobs** voor de weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="97077-195">On the **Add View** dialog, enter **ListBlobs** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="97077-196">Open `ListBlobs.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment:</span><span class="sxs-lookup"><span data-stu-id="97077-196">Open `ListBlobs.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="97077-197">In de **Solution Explorer**, vouw de **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="97077-197">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="97077-198">Nadat de laatste **Html.ActionLink**, voeg de volgende **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="97077-198">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. <span data-ttu-id="97077-199">Voer de toepassing en selecteer **lijst blobs** om vergelijkbaar met de volgende schermopname resultaten te bekijken:</span><span class="sxs-lookup"><span data-stu-id="97077-199">Run the application, and select **List blobs** to see results similar to the following screen shot:</span></span>
  
    ![BLOB-aanbieding](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a><span data-ttu-id="97077-201">Blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="97077-201">Download blobs</span></span>

<span data-ttu-id="97077-202">Deze sectie ziet u hoe u een blob te downloaden en een persistent maken met lokale opslag of de inhoud lezen in een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="97077-202">This section illustrates how to download a blob and either persist it to local storage or read the contents into a string.</span></span> <span data-ttu-id="97077-203">De voorbeeld-code verwijst naar de *test blobcontainer* gemaakt in de sectie [maken van een blob-container](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="97077-203">The sample code references the *test-blob-container* created in the section, [Create a blob container](#create-a-blob-container).</span></span>

1. <span data-ttu-id="97077-204">Open het `BlobsController.cs`-bestand.</span><span class="sxs-lookup"><span data-stu-id="97077-204">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="97077-205">Toevoegen van een methode aangeroepen **DownloadBlob** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="97077-205">Add a method called **DownloadBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="97077-206">Binnen de **DownloadBlob** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="97077-206">Within the **DownloadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="97077-207">Gebruik de volgende code de verbindingsreeks voor opslag en storage-account-gegevens ophalen uit de configuratie van Azure service: (wijziging  *&lt;storage-account-name >* op de naam van de Azure storage-account u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="97077-207">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="97077-208">Ophalen van een **CloudBlobClient** object vertegenwoordigt een blob-service-client.</span><span class="sxs-lookup"><span data-stu-id="97077-208">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="97077-209">Ophalen van een **CloudBlobContainer** -object met een verwijzing naar de naam van de blob-container.</span><span class="sxs-lookup"><span data-stu-id="97077-209">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="97077-210">Een blob reference-object ophalen door het aanroepen van **CloudBlobContainer.GetBlockBlobReference** of **CloudBlobContainer.GetPageBlobReference** methode.</span><span class="sxs-lookup"><span data-stu-id="97077-210">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="97077-211">(Wijziging  *&lt;blob-naam >* op de naam van de blob die u wilt downloaden.)</span><span class="sxs-lookup"><span data-stu-id="97077-211">(Change *&lt;blob-name>* to the name of the blob you are downloading.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="97077-212">Als u wilt downloaden van een blob de **CloudBlockBlob.DownloadToStream** of **CloudPageBlob.DownloadToStream** methode, afhankelijk van het blobtype.</span><span class="sxs-lookup"><span data-stu-id="97077-212">To download a blob, use the **CloudBlockBlob.DownloadToStream** or **CloudPageBlob.DownloadToStream** method, depending on the blob type.</span></span> <span data-ttu-id="97077-213">De volgende code codefragment gebruikt de **CloudBlockBlob.DownloadToStream** methode een blob-inhoud overdraagt naar een stroomobject dat vervolgens wordt opgeslagen in een lokaal bestand: (wijziging  *&lt;lokale bestandsnaam >* naar het bestand volledig gekwalificeerde naam die aangeeft waar u de blob gedownload.)</span><span class="sxs-lookup"><span data-stu-id="97077-213">The following code snippet uses the **CloudBlockBlob.DownloadToStream** method to transfer a blob's contents to a stream object that is then persisted to a local file: (Change *&lt;local-file-name>* to the fully qualified file name representing where you want the blob downloaded.)</span></span> 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. <span data-ttu-id="97077-214">In de **Solution Explorer**, vouw de **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="97077-214">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="97077-215">Nadat de laatste **Html.ActionLink**, voeg de volgende **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="97077-215">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="97077-216">Voer de toepassing en selecteer **downloaden blob** voor het downloaden van de blob.</span><span class="sxs-lookup"><span data-stu-id="97077-216">Run the application, and select **Download blob** to download the blob.</span></span> <span data-ttu-id="97077-217">De blob die is opgegeven in de **CloudBlobContainer.GetBlockBlobReference** methodeaanroep downloadt naar de locatie die u opgeeft in de **File.OpenWrite** methodeaanroep.</span><span class="sxs-lookup"><span data-stu-id="97077-217">The blob specified in the **CloudBlobContainer.GetBlockBlobReference** method call downloads to the location you specify in the **File.OpenWrite** method call.</span></span> 

## <a name="delete-blobs"></a><span data-ttu-id="97077-218">Blobs verwijderen</span><span class="sxs-lookup"><span data-stu-id="97077-218">Delete blobs</span></span>

<span data-ttu-id="97077-219">De volgende stappen uit te laten zien hoe u een blob verwijderen:</span><span class="sxs-lookup"><span data-stu-id="97077-219">The following steps illustrate how to delete a blob:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="97077-220">De code in deze sectie wordt ervan uitgegaan dat u de stappen in de sectie hebt voltooid [de ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="97077-220">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="97077-221">Open het `BlobsController.cs`-bestand.</span><span class="sxs-lookup"><span data-stu-id="97077-221">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="97077-222">Toevoegen van een methode aangeroepen **DeleteBlob** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="97077-222">Add a method called **DeleteBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```

1. <span data-ttu-id="97077-223">Ophalen van een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="97077-223">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="97077-224">Gebruik de volgende code de verbindingsreeks voor opslag en storage-account-gegevens ophalen uit de configuratie van Azure service: (wijziging  *&lt;storage-account-name >* op de naam van de Azure storage-account u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="97077-224">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="97077-225">Ophalen van een **CloudBlobClient** object vertegenwoordigt een blob-service-client.</span><span class="sxs-lookup"><span data-stu-id="97077-225">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="97077-226">Ophalen van een **CloudBlobContainer** -object met een verwijzing naar de naam van de blob-container.</span><span class="sxs-lookup"><span data-stu-id="97077-226">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="97077-227">Een blob reference-object ophalen door het aanroepen van **CloudBlobContainer.GetBlockBlobReference** of **CloudBlobContainer.GetPageBlobReference** methode.</span><span class="sxs-lookup"><span data-stu-id="97077-227">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="97077-228">(Wijziging  *&lt;blob-naam >* op de naam van de blob die u wilt verwijderen.)</span><span class="sxs-lookup"><span data-stu-id="97077-228">(Change *&lt;blob-name>* to the name of the blob you are deleting.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. To delete a blob, use the **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. <span data-ttu-id="97077-229">In de **Solution Explorer**, vouw de **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="97077-229">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="97077-230">Nadat de laatste **Html.ActionLink**, voeg de volgende **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="97077-230">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="97077-231">Voer de toepassing en selecteer **verwijderen blob** verwijderen van de blob die is opgegeven in de **CloudBlobContainer.GetBlockBlobReference** methodeaanroep.</span><span class="sxs-lookup"><span data-stu-id="97077-231">Run the application, and select **Delete blob** to delete the blob specified in the **CloudBlobContainer.GetBlockBlobReference** method call.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="97077-232">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="97077-232">Next steps</span></span>
<span data-ttu-id="97077-233">Bekijk meer functiehandleidingen voor informatie over aanvullende mogelijkheden voor het opslaan van gegevens in Azure.</span><span class="sxs-lookup"><span data-stu-id="97077-233">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="97077-234">Aan de slag met Azure-tabelopslag en Visual Studio verbonden Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="97077-234">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-tables.md)
  * [<span data-ttu-id="97077-235">Aan de slag met Azure queue storage- en Visual Studio verbonden Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="97077-235">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-queues.md)
