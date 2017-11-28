---
title: Openbare leestoegang voor containers en blobs in Azure Blob-opslag inschakelen | Microsoft Docs
description: Informatie over hoe u containers en blobs beschikbaar voor anonieme toegang en hoe programmatisch toegang toe hebben.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a2cffee6-3224-4f2a-8183-66ca23b2d2d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: marsma
ms.openlocfilehash: 8d4f4c7c208baf0db6155eb78a53e37c4ec1e023
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-anonymous-read-access-to-containers-and-blobs"></a><span data-ttu-id="e210b-103">Anonieme leestoegang tot containers en blobs beheren</span><span class="sxs-lookup"><span data-stu-id="e210b-103">Manage anonymous read access to containers and blobs</span></span>
<span data-ttu-id="e210b-104">U kunt anonieme, openbare leestoegang tot een container en de blobs in Azure Blob storage inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e210b-104">You can enable anonymous, public read access to a container and its blobs in Azure Blob storage.</span></span> <span data-ttu-id="e210b-105">Op deze manier kunt u alleen-lezen toegang tot deze bronnen verlenen zonder het delen van de accountsleutel en zonder een shared access signature (SAS).</span><span class="sxs-lookup"><span data-stu-id="e210b-105">By doing so, you can grant read-only access to these resources without sharing your account key, and without requiring a shared access signature (SAS).</span></span>

<span data-ttu-id="e210b-106">Openbare leestoegang wordt aanbevolen voor scenario's waar u wilt dat bepaalde blobs altijd alleen beschikbaar voor anonieme toegang voor lezen.</span><span class="sxs-lookup"><span data-stu-id="e210b-106">Public read access is best for scenarios where you want certain blobs to always be available for anonymous read access.</span></span> <span data-ttu-id="e210b-107">Voor nauwkeuriger beheer, kunt u een shared access signature maken.</span><span class="sxs-lookup"><span data-stu-id="e210b-107">For more fine-grained control, you can create a shared access signature.</span></span> <span data-ttu-id="e210b-108">Handtekeningen voor gedeelde toegang kunnen u beperkte toegang met andere machtigingen voor een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="e210b-108">Shared access signatures enable you to provide restricted access using different permissions, for a specific time period.</span></span> <span data-ttu-id="e210b-109">Voor meer informatie over het maken van gedeelde handtekeningen krijgen, Zie [Using shared access signatures (SAS) in Azure Storage](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e210b-109">For more information about creating shared access signatures, see [Using shared access signatures (SAS) in Azure Storage](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="grant-anonymous-users-permissions-to-containers-and-blobs"></a><span data-ttu-id="e210b-110">Anonieme gebruikers machtigen tot containers en blobs</span><span class="sxs-lookup"><span data-stu-id="e210b-110">Grant anonymous users permissions to containers and blobs</span></span>
<span data-ttu-id="e210b-111">Standaard kunnen een container en alle bestaande blobs erin alleen worden geopend door de eigenaar van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e210b-111">By default, a container and any blobs within it may be accessed only by the owner of the storage account.</span></span> <span data-ttu-id="e210b-112">Als u anonieme gebruikers leesmachtigingen voor een container en de blobs geven, kunt u de container-machtigingen voor openbare toegang instellen.</span><span class="sxs-lookup"><span data-stu-id="e210b-112">To give anonymous users read permissions to a container and its blobs, you can set the container permissions to allow public access.</span></span> <span data-ttu-id="e210b-113">Anonieme gebruikers kunnen BLOB's binnen een container openbaar toegankelijk lezen zonder verificatie van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="e210b-113">Anonymous users can read blobs within a publicly accessible container without authenticating the request.</span></span>

<span data-ttu-id="e210b-114">U kunt een container configureren met de volgende machtigingen:</span><span class="sxs-lookup"><span data-stu-id="e210b-114">You can configure a container with the following permissions:</span></span>

* <span data-ttu-id="e210b-115">**Geen enkele openbare leestoegang:** de container en de blobs kunnen alleen worden geopend door de eigenaar van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e210b-115">**No public read access:** The container and its blobs can be accessed only by the storage account owner.</span></span> <span data-ttu-id="e210b-116">Dit is de standaardwaarde voor alle nieuwe containers.</span><span class="sxs-lookup"><span data-stu-id="e210b-116">This is the default for all new containers.</span></span>
* <span data-ttu-id="e210b-117">**Openbare leestoegang voor blobs alleen:** Blobs in de container kunnen worden gelezen door anonieme aanvraag, maar de containergegevens is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="e210b-117">**Public read access for blobs only:** Blobs within the container can be read by anonymous request, but container data is not available.</span></span> <span data-ttu-id="e210b-118">Anonieme clients kunnen de blobs in de container niet opsommen.</span><span class="sxs-lookup"><span data-stu-id="e210b-118">Anonymous clients cannot enumerate the blobs within the container.</span></span>
* <span data-ttu-id="e210b-119">**Volledige openbare leestoegang:** alle container en de blob-gegevens kunnen worden gelezen door anonieme aanvraag.</span><span class="sxs-lookup"><span data-stu-id="e210b-119">**Full public read access:** All container and blob data can be read by anonymous request.</span></span> <span data-ttu-id="e210b-120">Clients anonieme aanvraag kunnen opsommen blobs in de container, maar kunnen de containers in het opslagaccount niet inventariseren.</span><span class="sxs-lookup"><span data-stu-id="e210b-120">Clients can enumerate blobs within the container by anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="e210b-121">U kunt de volgende container machtigingen worden ingesteld:</span><span class="sxs-lookup"><span data-stu-id="e210b-121">You can use the following to set container permissions:</span></span>

* [<span data-ttu-id="e210b-122">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e210b-122">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="e210b-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e210b-123">Azure PowerShell</span></span>](../common/storage-powershell-guide-full.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#how-to-manage-azure-blobs)
* [<span data-ttu-id="e210b-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e210b-124">Azure CLI 2.0</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-and-manage-blobs)
* <span data-ttu-id="e210b-125">Programmatisch met behulp van een van de opslag-clientbibliotheken of de REST-API</span><span class="sxs-lookup"><span data-stu-id="e210b-125">Programmatically, by using one of the storage client libraries or the REST API</span></span>

### <a name="set-container-permissions-in-the-azure-portal"></a><span data-ttu-id="e210b-126">Container machtigingen instellen in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="e210b-126">Set container permissions in the Azure portal</span></span>
<span data-ttu-id="e210b-127">Container machtigingen instellen de [Azure-portal](https://portal.azure.com), als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="e210b-127">To set container permissions in the [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="e210b-128">Open uw **opslagaccount** blade in de portal.</span><span class="sxs-lookup"><span data-stu-id="e210b-128">Open your **Storage account** blade in the portal.</span></span> <span data-ttu-id="e210b-129">U kunt uw storage-account vinden door te selecteren **opslagaccounts** in de portal hoofdmenu-blade.</span><span class="sxs-lookup"><span data-stu-id="e210b-129">You can find your storage account by selecting **Storage accounts** in the main portal menu blade.</span></span>
1. <span data-ttu-id="e210b-130">Onder **BLOB-SERVICE** Selecteer op de blade menu **Containers**.</span><span class="sxs-lookup"><span data-stu-id="e210b-130">Under **BLOB SERVICE** on the menu blade, select **Containers**.</span></span>
1. <span data-ttu-id="e210b-131">Met de rechtermuisknop op de rij container of Selecteer het weglatingsteken openen van de container **contextmenu**.</span><span class="sxs-lookup"><span data-stu-id="e210b-131">Right-click on the container row or select the ellipsis to open the container's **Context menu**.</span></span>
1. <span data-ttu-id="e210b-132">Selecteer **toegangsbeleid** in het contextmenu.</span><span class="sxs-lookup"><span data-stu-id="e210b-132">Select **Access policy** in the context menu.</span></span>
1. <span data-ttu-id="e210b-133">Selecteer een **toegangstype** in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="e210b-133">Select an **Access type** from the drop down menu.</span></span>

    ![Dialoogvenster metagegevens bewerken](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a><span data-ttu-id="e210b-135">Container machtigingen instellen met .NET</span><span class="sxs-lookup"><span data-stu-id="e210b-135">Set container permissions with .NET</span></span>
<span data-ttu-id="e210b-136">Als machtigingen wilt instellen voor een container met C# en de Storage-clientbibliotheek voor .NET, eerst ophalen van de container bestaande machtigingen door het aanroepen van de **GetPermissions** methode.</span><span class="sxs-lookup"><span data-stu-id="e210b-136">To set permissions for a container using C# and the Storage Client Library for .NET, first retrieve the container's existing permissions by calling the **GetPermissions** method.</span></span> <span data-ttu-id="e210b-137">Stel de **PublicAccess** eigenschap voor de **BlobContainerPermissions** -object dat wordt geretourneerd door de **GetPermissions** methode.</span><span class="sxs-lookup"><span data-stu-id="e210b-137">Then set the **PublicAccess** property for the **BlobContainerPermissions** object that is returned by the **GetPermissions** method.</span></span> <span data-ttu-id="e210b-138">Tenslotte roept de **SetPermissions** methode met de bijgewerkte machtigingen.</span><span class="sxs-lookup"><span data-stu-id="e210b-138">Finally, call the **SetPermissions** method with the updated permissions.</span></span>

<span data-ttu-id="e210b-139">Het volgende voorbeeld wordt de container machtigingen voor volledige openbare leestoegang.</span><span class="sxs-lookup"><span data-stu-id="e210b-139">The following example sets the container's permissions to full public read access.</span></span> <span data-ttu-id="e210b-140">Om in te stellen van machtigingen voor openbare leestoegang voor blobs alleen de **PublicAccess** eigenschap **BlobContainerPublicAccessType.Blob**.</span><span class="sxs-lookup"><span data-stu-id="e210b-140">To set permissions to public read access for blobs only, set the **PublicAccess** property to **BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="e210b-141">De eigenschap voor het verwijderen van alle machtigingen voor anonieme gebruikers instellen op **BlobContainerPublicAccessType.Off**.</span><span class="sxs-lookup"><span data-stu-id="e210b-141">To remove all permissions for anonymous users, set the property to **BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="e210b-142">Toegang tot containers en blobs anoniem</span><span class="sxs-lookup"><span data-stu-id="e210b-142">Access containers and blobs anonymously</span></span>
<span data-ttu-id="e210b-143">Een client die toegang heeft tot containers en blobs anoniem kan constructors waarvoor geen referenties gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e210b-143">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="e210b-144">De volgende voorbeelden ziet diverse manieren om te verwijzen naar van Blob-serviceresources anoniem.</span><span class="sxs-lookup"><span data-stu-id="e210b-144">The following examples show a few different ways to reference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="e210b-145">Een clientobject anonieme maken</span><span class="sxs-lookup"><span data-stu-id="e210b-145">Create an anonymous client object</span></span>
<span data-ttu-id="e210b-146">U kunt een nieuw serviceobject voor een client voor anonieme toegang maken door het eindpunt van de Blob-service voor het account.</span><span class="sxs-lookup"><span data-stu-id="e210b-146">You can create a new service client object for anonymous access by providing the Blob service endpoint for the account.</span></span> <span data-ttu-id="e210b-147">U moet echter ook de naam van een container in het account dat beschikbaar is voor anonieme toegang kennen.</span><span class="sxs-lookup"><span data-stu-id="e210b-147">However, you must also know the name of a container in that account that's available for anonymous access.</span></span>

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create the client object using the Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference to a container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read the container's properties. Note this is only possible when the container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="e210b-148">Een container anoniem verwijst naar</span><span class="sxs-lookup"><span data-stu-id="e210b-148">Reference a container anonymously</span></span>
<span data-ttu-id="e210b-149">Als u de URL naar een container die anoniem beschikbaar hebt, kunt u deze rechtstreeks verwijzen naar de container.</span><span class="sxs-lookup"><span data-stu-id="e210b-149">If you have the URL to a container that is anonymously available, you can use it to reference the container directly.</span></span>

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference to a container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in the container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="e210b-150">Een blob anoniem verwijst naar</span><span class="sxs-lookup"><span data-stu-id="e210b-150">Reference a blob anonymously</span></span>
<span data-ttu-id="e210b-151">Als u de URL naar een blob die beschikbaar is voor anonieme toegang hebt, kunt u verwijzen naar de blob die URL direct met:</span><span class="sxs-lookup"><span data-stu-id="e210b-151">If you have the URL to a blob that is available for anonymous access, you can reference the blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-to-anonymous-users"></a><span data-ttu-id="e210b-152">Functies die beschikbaar voor anonieme gebruikers</span><span class="sxs-lookup"><span data-stu-id="e210b-152">Features available to anonymous users</span></span>
<span data-ttu-id="e210b-153">De volgende tabel ziet u welke bewerkingen door anonieme gebruikers kunnen worden aangeroepen wanneer een container-ACL is ingesteld op het toestaan van openbare toegang.</span><span class="sxs-lookup"><span data-stu-id="e210b-153">The following table shows which operations may be called by anonymous users when a container's ACL is set to allow public access.</span></span>

| <span data-ttu-id="e210b-154">REST-bewerking</span><span class="sxs-lookup"><span data-stu-id="e210b-154">REST Operation</span></span> | <span data-ttu-id="e210b-155">Machtiging met volledige openbare leestoegang</span><span class="sxs-lookup"><span data-stu-id="e210b-155">Permission with full public read access</span></span> | <span data-ttu-id="e210b-156">Machtiging met openbare leestoegang voor blobs alleen</span><span class="sxs-lookup"><span data-stu-id="e210b-156">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e210b-157">Lijst Containers</span><span class="sxs-lookup"><span data-stu-id="e210b-157">List Containers</span></span> |<span data-ttu-id="e210b-158">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-158">Owner only</span></span> |<span data-ttu-id="e210b-159">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-159">Owner only</span></span> |
| <span data-ttu-id="e210b-160">Container maken</span><span class="sxs-lookup"><span data-stu-id="e210b-160">Create Container</span></span> |<span data-ttu-id="e210b-161">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-161">Owner only</span></span> |<span data-ttu-id="e210b-162">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-162">Owner only</span></span> |
| <span data-ttu-id="e210b-163">Eigenschappen van Container ophalen</span><span class="sxs-lookup"><span data-stu-id="e210b-163">Get Container Properties</span></span> |<span data-ttu-id="e210b-164">Alle</span><span class="sxs-lookup"><span data-stu-id="e210b-164">All</span></span> |<span data-ttu-id="e210b-165">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-165">Owner only</span></span> |
| <span data-ttu-id="e210b-166">Container metagegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="e210b-166">Get Container Metadata</span></span> |<span data-ttu-id="e210b-167">Alle</span><span class="sxs-lookup"><span data-stu-id="e210b-167">All</span></span> |<span data-ttu-id="e210b-168">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-168">Owner only</span></span> |
| <span data-ttu-id="e210b-169">Metagegevens van de Container instellen</span><span class="sxs-lookup"><span data-stu-id="e210b-169">Set Container Metadata</span></span> |<span data-ttu-id="e210b-170">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-170">Owner only</span></span> |<span data-ttu-id="e210b-171">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-171">Owner only</span></span> |
| <span data-ttu-id="e210b-172">Container-ACL ophalen</span><span class="sxs-lookup"><span data-stu-id="e210b-172">Get Container ACL</span></span> |<span data-ttu-id="e210b-173">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-173">Owner only</span></span> |<span data-ttu-id="e210b-174">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-174">Owner only</span></span> |
| <span data-ttu-id="e210b-175">Container-ACL instellen</span><span class="sxs-lookup"><span data-stu-id="e210b-175">Set Container ACL</span></span> |<span data-ttu-id="e210b-176">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-176">Owner only</span></span> |<span data-ttu-id="e210b-177">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-177">Owner only</span></span> |
| <span data-ttu-id="e210b-178">Verwijderen van Container</span><span class="sxs-lookup"><span data-stu-id="e210b-178">Delete Container</span></span> |<span data-ttu-id="e210b-179">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-179">Owner only</span></span> |<span data-ttu-id="e210b-180">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-180">Owner only</span></span> |
| <span data-ttu-id="e210b-181">Lijst met BLOB 's</span><span class="sxs-lookup"><span data-stu-id="e210b-181">List Blobs</span></span> |<span data-ttu-id="e210b-182">Alle</span><span class="sxs-lookup"><span data-stu-id="e210b-182">All</span></span> |<span data-ttu-id="e210b-183">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-183">Owner only</span></span> |
| <span data-ttu-id="e210b-184">Blob plaatsen</span><span class="sxs-lookup"><span data-stu-id="e210b-184">Put Blob</span></span> |<span data-ttu-id="e210b-185">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-185">Owner only</span></span> |<span data-ttu-id="e210b-186">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-186">Owner only</span></span> |
| <span data-ttu-id="e210b-187">Ophalen van Blob</span><span class="sxs-lookup"><span data-stu-id="e210b-187">Get Blob</span></span> |<span data-ttu-id="e210b-188">Alle</span><span class="sxs-lookup"><span data-stu-id="e210b-188">All</span></span> |<span data-ttu-id="e210b-189">Alle</span><span class="sxs-lookup"><span data-stu-id="e210b-189">All</span></span> |
| <span data-ttu-id="e210b-190">Blob-eigenschappen ophalen</span><span class="sxs-lookup"><span data-stu-id="e210b-190">Get Blob Properties</span></span> |<span data-ttu-id="e210b-191">Alle</span><span class="sxs-lookup"><span data-stu-id="e210b-191">All</span></span> |<span data-ttu-id="e210b-192">Alle</span><span class="sxs-lookup"><span data-stu-id="e210b-192">All</span></span> |
| <span data-ttu-id="e210b-193">Blob-eigenschappen instellen</span><span class="sxs-lookup"><span data-stu-id="e210b-193">Set Blob Properties</span></span> |<span data-ttu-id="e210b-194">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-194">Owner only</span></span> |<span data-ttu-id="e210b-195">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-195">Owner only</span></span> |
| <span data-ttu-id="e210b-196">Blobmetagegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="e210b-196">Get Blob Metadata</span></span> |<span data-ttu-id="e210b-197">Alle</span><span class="sxs-lookup"><span data-stu-id="e210b-197">All</span></span> |<span data-ttu-id="e210b-198">Alle</span><span class="sxs-lookup"><span data-stu-id="e210b-198">All</span></span> |
| <span data-ttu-id="e210b-199">Blobmetagegevens instellen</span><span class="sxs-lookup"><span data-stu-id="e210b-199">Set Blob Metadata</span></span> |<span data-ttu-id="e210b-200">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-200">Owner only</span></span> |<span data-ttu-id="e210b-201">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-201">Owner only</span></span> |
| <span data-ttu-id="e210b-202">Blok plaatsen</span><span class="sxs-lookup"><span data-stu-id="e210b-202">Put Block</span></span> |<span data-ttu-id="e210b-203">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-203">Owner only</span></span> |<span data-ttu-id="e210b-204">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-204">Owner only</span></span> |
| <span data-ttu-id="e210b-205">Ophalen van lijst met geblokkeerde websites (alleen doorgevoerde blokken)</span><span class="sxs-lookup"><span data-stu-id="e210b-205">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="e210b-206">Alle</span><span class="sxs-lookup"><span data-stu-id="e210b-206">All</span></span> |<span data-ttu-id="e210b-207">Alle</span><span class="sxs-lookup"><span data-stu-id="e210b-207">All</span></span> |
| <span data-ttu-id="e210b-208">Ophalen van lijst met geblokkeerde websites (alleen niet-doorgevoerde blokken of alle blokken)</span><span class="sxs-lookup"><span data-stu-id="e210b-208">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="e210b-209">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-209">Owner only</span></span> |<span data-ttu-id="e210b-210">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-210">Owner only</span></span> |
| <span data-ttu-id="e210b-211">Lijst met geblokkeerde websites plaatsen</span><span class="sxs-lookup"><span data-stu-id="e210b-211">Put Block List</span></span> |<span data-ttu-id="e210b-212">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-212">Owner only</span></span> |<span data-ttu-id="e210b-213">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-213">Owner only</span></span> |
| <span data-ttu-id="e210b-214">Verwijderen van Blob</span><span class="sxs-lookup"><span data-stu-id="e210b-214">Delete Blob</span></span> |<span data-ttu-id="e210b-215">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-215">Owner only</span></span> |<span data-ttu-id="e210b-216">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-216">Owner only</span></span> |
| <span data-ttu-id="e210b-217">Blob kopiëren</span><span class="sxs-lookup"><span data-stu-id="e210b-217">Copy Blob</span></span> |<span data-ttu-id="e210b-218">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-218">Owner only</span></span> |<span data-ttu-id="e210b-219">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-219">Owner only</span></span> |
| <span data-ttu-id="e210b-220">Momentopname Blob</span><span class="sxs-lookup"><span data-stu-id="e210b-220">Snapshot Blob</span></span> |<span data-ttu-id="e210b-221">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-221">Owner only</span></span> |<span data-ttu-id="e210b-222">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-222">Owner only</span></span> |
| <span data-ttu-id="e210b-223">Lease Blob</span><span class="sxs-lookup"><span data-stu-id="e210b-223">Lease Blob</span></span> |<span data-ttu-id="e210b-224">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-224">Owner only</span></span> |<span data-ttu-id="e210b-225">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-225">Owner only</span></span> |
| <span data-ttu-id="e210b-226">Pagina plaatsen</span><span class="sxs-lookup"><span data-stu-id="e210b-226">Put Page</span></span> |<span data-ttu-id="e210b-227">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-227">Owner only</span></span> |<span data-ttu-id="e210b-228">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-228">Owner only</span></span> |
| <span data-ttu-id="e210b-229">Get-paginabereiken</span><span class="sxs-lookup"><span data-stu-id="e210b-229">Get Page Ranges</span></span> |<span data-ttu-id="e210b-230">Alle</span><span class="sxs-lookup"><span data-stu-id="e210b-230">All</span></span> |<span data-ttu-id="e210b-231">Alle</span><span class="sxs-lookup"><span data-stu-id="e210b-231">All</span></span> |
| <span data-ttu-id="e210b-232">Toevoeg-Blob</span><span class="sxs-lookup"><span data-stu-id="e210b-232">Append Blob</span></span> |<span data-ttu-id="e210b-233">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-233">Owner only</span></span> |<span data-ttu-id="e210b-234">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="e210b-234">Owner only</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e210b-235">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e210b-235">Next steps</span></span>

* [<span data-ttu-id="e210b-236">Verificatie voor de Azure Storage-Services</span><span class="sxs-lookup"><span data-stu-id="e210b-236">Authentication for the Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="e210b-237">Met behulp van Shared Access Signatures (SAS)</span><span class="sxs-lookup"><span data-stu-id="e210b-237">Using Shared Access Signatures (SAS)</span></span>](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="e210b-238">Toegang delegeren met een Shared Access Signature</span><span class="sxs-lookup"><span data-stu-id="e210b-238">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)
