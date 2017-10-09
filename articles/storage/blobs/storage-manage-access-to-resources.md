---
title: aaaEnable openbare leestoegang voor containers en blobs in Azure Blob storage | Microsoft Docs
description: Meer informatie over hoe toomake containers en blobs beschikbaar voor anonieme toegang en hoe tooaccess ze via een programma.
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
ms.openlocfilehash: dd8ffdb39a66aa06f65ad3cdd4315d47c117f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-anonymous-read-access-toocontainers-and-blobs"></a><span data-ttu-id="0acef-103">Anonieme leestoegang toocontainers en blobs beheren</span><span class="sxs-lookup"><span data-stu-id="0acef-103">Manage anonymous read access toocontainers and blobs</span></span>
<span data-ttu-id="0acef-104">U kunt anonieme, openbare leestoegang tooa container en de blobs in Azure Blob-opslag inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0acef-104">You can enable anonymous, public read access tooa container and its blobs in Azure Blob storage.</span></span> <span data-ttu-id="0acef-105">Op deze manier kunt u alleen-lezentoegang toothese resources verlenen zonder het delen van de accountsleutel en zonder een shared access signature (SAS).</span><span class="sxs-lookup"><span data-stu-id="0acef-105">By doing so, you can grant read-only access toothese resources without sharing your account key, and without requiring a shared access signature (SAS).</span></span>

<span data-ttu-id="0acef-106">Openbare leestoegang wordt aanbevolen voor scenario's waar u wilt dat bepaalde blobs tooalways worden beschikbaar voor anonieme toegang voor lezen.</span><span class="sxs-lookup"><span data-stu-id="0acef-106">Public read access is best for scenarios where you want certain blobs tooalways be available for anonymous read access.</span></span> <span data-ttu-id="0acef-107">Voor nauwkeuriger beheer, kunt u een shared access signature maken.</span><span class="sxs-lookup"><span data-stu-id="0acef-107">For more fine-grained control, you can create a shared access signature.</span></span> <span data-ttu-id="0acef-108">Handtekeningen voor gedeelde toegang inschakelen tooprovide beperkt via toegang tot andere machtigingen voor een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="0acef-108">Shared access signatures enable you tooprovide restricted access using different permissions, for a specific time period.</span></span> <span data-ttu-id="0acef-109">Voor meer informatie over het maken van gedeelde handtekeningen krijgen, Zie [Using shared access signatures (SAS) in Azure Storage](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0acef-109">For more information about creating shared access signatures, see [Using shared access signatures (SAS) in Azure Storage](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="grant-anonymous-users-permissions-toocontainers-and-blobs"></a><span data-ttu-id="0acef-110">Anonieme gebruikers machtigingen toocontainers en blobs verlenen</span><span class="sxs-lookup"><span data-stu-id="0acef-110">Grant anonymous users permissions toocontainers and blobs</span></span>
<span data-ttu-id="0acef-111">Standaard kunnen een container en alle bestaande blobs erin alleen worden geopend door Hallo eigenaar van Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="0acef-111">By default, a container and any blobs within it may be accessed only by hello owner of hello storage account.</span></span> <span data-ttu-id="0acef-112">toogive anonieme gebruikers leesmachtigingen tooa container en de blobs, kunt u Hallo container machtigingen tooallow openbare toegang instellen.</span><span class="sxs-lookup"><span data-stu-id="0acef-112">toogive anonymous users read permissions tooa container and its blobs, you can set hello container permissions tooallow public access.</span></span> <span data-ttu-id="0acef-113">Anonieme gebruikers kunnen BLOB's binnen een container openbaar toegankelijk lezen zonder verificatie Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="0acef-113">Anonymous users can read blobs within a publicly accessible container without authenticating hello request.</span></span>

<span data-ttu-id="0acef-114">U kunt een container met de volgende machtigingen Hallo configureren:</span><span class="sxs-lookup"><span data-stu-id="0acef-114">You can configure a container with hello following permissions:</span></span>

* <span data-ttu-id="0acef-115">**Geen enkele openbare leestoegang:** Hallo-container en de blobs kunnen alleen worden geopend door Hallo eigenaar van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="0acef-115">**No public read access:** hello container and its blobs can be accessed only by hello storage account owner.</span></span> <span data-ttu-id="0acef-116">Dit is de standaardinstelling Hallo voor alle nieuwe containers.</span><span class="sxs-lookup"><span data-stu-id="0acef-116">This is hello default for all new containers.</span></span>
* <span data-ttu-id="0acef-117">**Openbare leestoegang voor blobs alleen:** Blobs in de container Hallo kunnen worden gelezen door anonieme aanvraag, maar de containergegevens is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="0acef-117">**Public read access for blobs only:** Blobs within hello container can be read by anonymous request, but container data is not available.</span></span> <span data-ttu-id="0acef-118">Anonieme clients kunnen blobs in de container Hallo Hallo niet opsommen.</span><span class="sxs-lookup"><span data-stu-id="0acef-118">Anonymous clients cannot enumerate hello blobs within hello container.</span></span>
* <span data-ttu-id="0acef-119">**Volledige openbare leestoegang:** alle container en de blob-gegevens kunnen worden gelezen door anonieme aanvraag.</span><span class="sxs-lookup"><span data-stu-id="0acef-119">**Full public read access:** All container and blob data can be read by anonymous request.</span></span> <span data-ttu-id="0acef-120">Clients blobs in de container Hallo anonieme aanvraag kunnen opsommen, maar kunnen de containers in Hallo storage-account niet inventariseren.</span><span class="sxs-lookup"><span data-stu-id="0acef-120">Clients can enumerate blobs within hello container by anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="0acef-121">U kunt de volgende tooset container machtigingen hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="0acef-121">You can use hello following tooset container permissions:</span></span>

* [<span data-ttu-id="0acef-122">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0acef-122">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="0acef-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0acef-123">Azure PowerShell</span></span>](../common/storage-powershell-guide-full.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#how-to-manage-azure-blobs)
* [<span data-ttu-id="0acef-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0acef-124">Azure CLI 2.0</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-and-manage-blobs)
* <span data-ttu-id="0acef-125">Programmatisch met behulp van een van de opslagclientbibliotheken Hallo of Hallo REST-API</span><span class="sxs-lookup"><span data-stu-id="0acef-125">Programmatically, by using one of hello storage client libraries or hello REST API</span></span>

### <a name="set-container-permissions-in-hello-azure-portal"></a><span data-ttu-id="0acef-126">Container machtigingen instellen in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="0acef-126">Set container permissions in hello Azure portal</span></span>
<span data-ttu-id="0acef-127">tooset container machtigingen in Hallo [Azure-portal](https://portal.azure.com), als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="0acef-127">tooset container permissions in hello [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="0acef-128">Open uw **opslagaccount** blade in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="0acef-128">Open your **Storage account** blade in hello portal.</span></span> <span data-ttu-id="0acef-129">U kunt uw storage-account vinden door te selecteren **opslagaccounts** Hallo portal hoofdmenu blade.</span><span class="sxs-lookup"><span data-stu-id="0acef-129">You can find your storage account by selecting **Storage accounts** in hello main portal menu blade.</span></span>
1. <span data-ttu-id="0acef-130">Onder **BLOB-SERVICE** selecteren op Hallo menu blade **Containers**.</span><span class="sxs-lookup"><span data-stu-id="0acef-130">Under **BLOB SERVICE** on hello menu blade, select **Containers**.</span></span>
1. <span data-ttu-id="0acef-131">Met de rechtermuisknop op het Hallo-container rij of selecteer Hallo weglatingsteken tooopen Hallo van container **contextmenu**.</span><span class="sxs-lookup"><span data-stu-id="0acef-131">Right-click on hello container row or select hello ellipsis tooopen hello container's **Context menu**.</span></span>
1. <span data-ttu-id="0acef-132">Selecteer **toegangsbeleid** in het contextmenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="0acef-132">Select **Access policy** in hello context menu.</span></span>
1. <span data-ttu-id="0acef-133">Selecteer een **toegangstype** van Hallo vervolgkeuzemenu.</span><span class="sxs-lookup"><span data-stu-id="0acef-133">Select an **Access type** from hello drop down menu.</span></span>

    ![Dialoogvenster metagegevens bewerken](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a><span data-ttu-id="0acef-135">Container machtigingen instellen met .NET</span><span class="sxs-lookup"><span data-stu-id="0acef-135">Set container permissions with .NET</span></span>
<span data-ttu-id="0acef-136">Hallo-container bestaande machtigingen tooset machtigingen voor een container met C# en Hallo Storage-clientbibliotheek voor .NET, eerst ophalen door de aanroepende Hallo **GetPermissions** methode.</span><span class="sxs-lookup"><span data-stu-id="0acef-136">tooset permissions for a container using C# and hello Storage Client Library for .NET, first retrieve hello container's existing permissions by calling hello **GetPermissions** method.</span></span> <span data-ttu-id="0acef-137">Vervolgens set Hallo **PublicAccess** eigenschap voor Hallo **BlobContainerPermissions** -object dat wordt geretourneerd door Hallo **GetPermissions** methode.</span><span class="sxs-lookup"><span data-stu-id="0acef-137">Then set hello **PublicAccess** property for hello **BlobContainerPermissions** object that is returned by hello **GetPermissions** method.</span></span> <span data-ttu-id="0acef-138">Tenslotte roept Hallo **SetPermissions** methode Hello machtigingen bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="0acef-138">Finally, call hello **SetPermissions** method with hello updated permissions.</span></span>

<span data-ttu-id="0acef-139">Hallo volgt stelt Hallo-container machtigingen toofull openbare leestoegang.</span><span class="sxs-lookup"><span data-stu-id="0acef-139">hello following example sets hello container's permissions toofull public read access.</span></span> <span data-ttu-id="0acef-140">tooset machtigingen toopublic leestoegang voor blobs ingesteld alleen Hallo **PublicAccess** eigenschap te**BlobContainerPublicAccessType.Blob**.</span><span class="sxs-lookup"><span data-stu-id="0acef-140">tooset permissions toopublic read access for blobs only, set hello **PublicAccess** property too**BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="0acef-141">tooremove alle machtigingen voor anonieme gebruikers instellen eigenschap te Hallo**BlobContainerPublicAccessType.Off**.</span><span class="sxs-lookup"><span data-stu-id="0acef-141">tooremove all permissions for anonymous users, set hello property too**BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="0acef-142">Toegang tot containers en blobs anoniem</span><span class="sxs-lookup"><span data-stu-id="0acef-142">Access containers and blobs anonymously</span></span>
<span data-ttu-id="0acef-143">Een client die toegang heeft tot containers en blobs anoniem kan constructors waarvoor geen referenties gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0acef-143">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="0acef-144">Hallo volgen voorbeelden weergeven resources die een aantal verschillende manieren tooreference Blob-service anoniem.</span><span class="sxs-lookup"><span data-stu-id="0acef-144">hello following examples show a few different ways tooreference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="0acef-145">Een clientobject anonieme maken</span><span class="sxs-lookup"><span data-stu-id="0acef-145">Create an anonymous client object</span></span>
<span data-ttu-id="0acef-146">Dankzij de Hallo eindpunt voor Blob-service voor Hallo account kunt u een nieuw serviceobject voor een client voor anonieme toegang.</span><span class="sxs-lookup"><span data-stu-id="0acef-146">You can create a new service client object for anonymous access by providing hello Blob service endpoint for hello account.</span></span> <span data-ttu-id="0acef-147">U moet echter ook Hallo-naam van een container in het account dat beschikbaar is voor anonieme toegang kennen.</span><span class="sxs-lookup"><span data-stu-id="0acef-147">However, you must also know hello name of a container in that account that's available for anonymous access.</span></span>

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create hello client object using hello Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read hello container's properties. Note this is only possible when hello container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="0acef-148">Een container anoniem verwijst naar</span><span class="sxs-lookup"><span data-stu-id="0acef-148">Reference a container anonymously</span></span>
<span data-ttu-id="0acef-149">Als er Hallo URL tooa container die anoniem beschikbaar is, kunt u deze tooreference Hallo container rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="0acef-149">If you have hello URL tooa container that is anonymously available, you can use it tooreference hello container directly.</span></span>

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in hello container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="0acef-150">Een blob anoniem verwijst naar</span><span class="sxs-lookup"><span data-stu-id="0acef-150">Reference a blob anonymously</span></span>
<span data-ttu-id="0acef-151">Als u Hallo URL tooa blob die beschikbaar is voor anonieme toegang hebt, kunt u verwijzen naar Hallo blob die URL direct met:</span><span class="sxs-lookup"><span data-stu-id="0acef-151">If you have hello URL tooa blob that is available for anonymous access, you can reference hello blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-tooanonymous-users"></a><span data-ttu-id="0acef-152">Functies beschikbaar tooanonymous gebruikers</span><span class="sxs-lookup"><span data-stu-id="0acef-152">Features available tooanonymous users</span></span>
<span data-ttu-id="0acef-153">Hallo volgende tabel ziet u welke bewerkingen door anonieme gebruikers kunnen worden aangeroepen wanneer een container-ACL tooallow openbare toegang is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="0acef-153">hello following table shows which operations may be called by anonymous users when a container's ACL is set tooallow public access.</span></span>

| <span data-ttu-id="0acef-154">REST-bewerking</span><span class="sxs-lookup"><span data-stu-id="0acef-154">REST Operation</span></span> | <span data-ttu-id="0acef-155">Machtiging met volledige openbare leestoegang</span><span class="sxs-lookup"><span data-stu-id="0acef-155">Permission with full public read access</span></span> | <span data-ttu-id="0acef-156">Machtiging met openbare leestoegang voor blobs alleen</span><span class="sxs-lookup"><span data-stu-id="0acef-156">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0acef-157">Lijst Containers</span><span class="sxs-lookup"><span data-stu-id="0acef-157">List Containers</span></span> |<span data-ttu-id="0acef-158">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-158">Owner only</span></span> |<span data-ttu-id="0acef-159">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-159">Owner only</span></span> |
| <span data-ttu-id="0acef-160">Container maken</span><span class="sxs-lookup"><span data-stu-id="0acef-160">Create Container</span></span> |<span data-ttu-id="0acef-161">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-161">Owner only</span></span> |<span data-ttu-id="0acef-162">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-162">Owner only</span></span> |
| <span data-ttu-id="0acef-163">Eigenschappen van Container ophalen</span><span class="sxs-lookup"><span data-stu-id="0acef-163">Get Container Properties</span></span> |<span data-ttu-id="0acef-164">Alle</span><span class="sxs-lookup"><span data-stu-id="0acef-164">All</span></span> |<span data-ttu-id="0acef-165">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-165">Owner only</span></span> |
| <span data-ttu-id="0acef-166">Container metagegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="0acef-166">Get Container Metadata</span></span> |<span data-ttu-id="0acef-167">Alle</span><span class="sxs-lookup"><span data-stu-id="0acef-167">All</span></span> |<span data-ttu-id="0acef-168">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-168">Owner only</span></span> |
| <span data-ttu-id="0acef-169">Metagegevens van de Container instellen</span><span class="sxs-lookup"><span data-stu-id="0acef-169">Set Container Metadata</span></span> |<span data-ttu-id="0acef-170">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-170">Owner only</span></span> |<span data-ttu-id="0acef-171">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-171">Owner only</span></span> |
| <span data-ttu-id="0acef-172">Container-ACL ophalen</span><span class="sxs-lookup"><span data-stu-id="0acef-172">Get Container ACL</span></span> |<span data-ttu-id="0acef-173">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-173">Owner only</span></span> |<span data-ttu-id="0acef-174">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-174">Owner only</span></span> |
| <span data-ttu-id="0acef-175">Container-ACL instellen</span><span class="sxs-lookup"><span data-stu-id="0acef-175">Set Container ACL</span></span> |<span data-ttu-id="0acef-176">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-176">Owner only</span></span> |<span data-ttu-id="0acef-177">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-177">Owner only</span></span> |
| <span data-ttu-id="0acef-178">Verwijderen van Container</span><span class="sxs-lookup"><span data-stu-id="0acef-178">Delete Container</span></span> |<span data-ttu-id="0acef-179">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-179">Owner only</span></span> |<span data-ttu-id="0acef-180">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-180">Owner only</span></span> |
| <span data-ttu-id="0acef-181">Lijst met BLOB 's</span><span class="sxs-lookup"><span data-stu-id="0acef-181">List Blobs</span></span> |<span data-ttu-id="0acef-182">Alle</span><span class="sxs-lookup"><span data-stu-id="0acef-182">All</span></span> |<span data-ttu-id="0acef-183">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-183">Owner only</span></span> |
| <span data-ttu-id="0acef-184">Blob plaatsen</span><span class="sxs-lookup"><span data-stu-id="0acef-184">Put Blob</span></span> |<span data-ttu-id="0acef-185">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-185">Owner only</span></span> |<span data-ttu-id="0acef-186">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-186">Owner only</span></span> |
| <span data-ttu-id="0acef-187">Ophalen van Blob</span><span class="sxs-lookup"><span data-stu-id="0acef-187">Get Blob</span></span> |<span data-ttu-id="0acef-188">Alle</span><span class="sxs-lookup"><span data-stu-id="0acef-188">All</span></span> |<span data-ttu-id="0acef-189">Alle</span><span class="sxs-lookup"><span data-stu-id="0acef-189">All</span></span> |
| <span data-ttu-id="0acef-190">Blob-eigenschappen ophalen</span><span class="sxs-lookup"><span data-stu-id="0acef-190">Get Blob Properties</span></span> |<span data-ttu-id="0acef-191">Alle</span><span class="sxs-lookup"><span data-stu-id="0acef-191">All</span></span> |<span data-ttu-id="0acef-192">Alle</span><span class="sxs-lookup"><span data-stu-id="0acef-192">All</span></span> |
| <span data-ttu-id="0acef-193">Blob-eigenschappen instellen</span><span class="sxs-lookup"><span data-stu-id="0acef-193">Set Blob Properties</span></span> |<span data-ttu-id="0acef-194">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-194">Owner only</span></span> |<span data-ttu-id="0acef-195">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-195">Owner only</span></span> |
| <span data-ttu-id="0acef-196">Blobmetagegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="0acef-196">Get Blob Metadata</span></span> |<span data-ttu-id="0acef-197">Alle</span><span class="sxs-lookup"><span data-stu-id="0acef-197">All</span></span> |<span data-ttu-id="0acef-198">Alle</span><span class="sxs-lookup"><span data-stu-id="0acef-198">All</span></span> |
| <span data-ttu-id="0acef-199">Blobmetagegevens instellen</span><span class="sxs-lookup"><span data-stu-id="0acef-199">Set Blob Metadata</span></span> |<span data-ttu-id="0acef-200">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-200">Owner only</span></span> |<span data-ttu-id="0acef-201">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-201">Owner only</span></span> |
| <span data-ttu-id="0acef-202">Blok plaatsen</span><span class="sxs-lookup"><span data-stu-id="0acef-202">Put Block</span></span> |<span data-ttu-id="0acef-203">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-203">Owner only</span></span> |<span data-ttu-id="0acef-204">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-204">Owner only</span></span> |
| <span data-ttu-id="0acef-205">Ophalen van lijst met geblokkeerde websites (alleen doorgevoerde blokken)</span><span class="sxs-lookup"><span data-stu-id="0acef-205">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="0acef-206">Alle</span><span class="sxs-lookup"><span data-stu-id="0acef-206">All</span></span> |<span data-ttu-id="0acef-207">Alle</span><span class="sxs-lookup"><span data-stu-id="0acef-207">All</span></span> |
| <span data-ttu-id="0acef-208">Ophalen van lijst met geblokkeerde websites (alleen niet-doorgevoerde blokken of alle blokken)</span><span class="sxs-lookup"><span data-stu-id="0acef-208">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="0acef-209">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-209">Owner only</span></span> |<span data-ttu-id="0acef-210">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-210">Owner only</span></span> |
| <span data-ttu-id="0acef-211">Lijst met geblokkeerde websites plaatsen</span><span class="sxs-lookup"><span data-stu-id="0acef-211">Put Block List</span></span> |<span data-ttu-id="0acef-212">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-212">Owner only</span></span> |<span data-ttu-id="0acef-213">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-213">Owner only</span></span> |
| <span data-ttu-id="0acef-214">Verwijderen van Blob</span><span class="sxs-lookup"><span data-stu-id="0acef-214">Delete Blob</span></span> |<span data-ttu-id="0acef-215">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-215">Owner only</span></span> |<span data-ttu-id="0acef-216">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-216">Owner only</span></span> |
| <span data-ttu-id="0acef-217">Blob kopiëren</span><span class="sxs-lookup"><span data-stu-id="0acef-217">Copy Blob</span></span> |<span data-ttu-id="0acef-218">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-218">Owner only</span></span> |<span data-ttu-id="0acef-219">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-219">Owner only</span></span> |
| <span data-ttu-id="0acef-220">Momentopname Blob</span><span class="sxs-lookup"><span data-stu-id="0acef-220">Snapshot Blob</span></span> |<span data-ttu-id="0acef-221">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-221">Owner only</span></span> |<span data-ttu-id="0acef-222">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-222">Owner only</span></span> |
| <span data-ttu-id="0acef-223">Lease Blob</span><span class="sxs-lookup"><span data-stu-id="0acef-223">Lease Blob</span></span> |<span data-ttu-id="0acef-224">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-224">Owner only</span></span> |<span data-ttu-id="0acef-225">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-225">Owner only</span></span> |
| <span data-ttu-id="0acef-226">Pagina plaatsen</span><span class="sxs-lookup"><span data-stu-id="0acef-226">Put Page</span></span> |<span data-ttu-id="0acef-227">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-227">Owner only</span></span> |<span data-ttu-id="0acef-228">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-228">Owner only</span></span> |
| <span data-ttu-id="0acef-229">Get-paginabereiken</span><span class="sxs-lookup"><span data-stu-id="0acef-229">Get Page Ranges</span></span> |<span data-ttu-id="0acef-230">Alle</span><span class="sxs-lookup"><span data-stu-id="0acef-230">All</span></span> |<span data-ttu-id="0acef-231">Alle</span><span class="sxs-lookup"><span data-stu-id="0acef-231">All</span></span> |
| <span data-ttu-id="0acef-232">Toevoeg-Blob</span><span class="sxs-lookup"><span data-stu-id="0acef-232">Append Blob</span></span> |<span data-ttu-id="0acef-233">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-233">Owner only</span></span> |<span data-ttu-id="0acef-234">Alleen de eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acef-234">Owner only</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0acef-235">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0acef-235">Next steps</span></span>

* [<span data-ttu-id="0acef-236">Verificatie voor hello Azure Storage-Services</span><span class="sxs-lookup"><span data-stu-id="0acef-236">Authentication for hello Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="0acef-237">Met behulp van Shared Access Signatures (SAS)</span><span class="sxs-lookup"><span data-stu-id="0acef-237">Using Shared Access Signatures (SAS)</span></span>](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="0acef-238">Toegang delegeren met een Shared Access Signature</span><span class="sxs-lookup"><span data-stu-id="0acef-238">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)
