---
title: Maken van een momentopname van een alleen-lezen van een blob in Azure Storage | Microsoft Docs
description: Informatie over het maken van een momentopname van een blob naar de back-up van blob-gegevens op een gegeven moment. Begrijpen hoe momentopnamen worden gefactureerd en het gebruik ervan capaciteit, kosten te minimaliseren.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 3710705d-e127-4b01-8d0f-29853fb06d0d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: marsma
ms.openlocfilehash: 6ebb77f4ec5f1887e5c55bf1c8c64224a9233654
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-blob-snapshot"></a><span data-ttu-id="7c3b5-104">Een blob-momentopname maken</span><span class="sxs-lookup"><span data-stu-id="7c3b5-104">Create a blob snapshot</span></span>

<span data-ttu-id="7c3b5-105">Een momentopname is een alleen-lezen-versie van een blob die wordt uitgevoerd op een punt in tijd.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-105">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="7c3b5-106">Momentopnamen zijn nuttig voor back-up blobs.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-106">Snapshots are useful for backing up blobs.</span></span> <span data-ttu-id="7c3b5-107">Nadat u een momentopname gemaakt, lezen, kopiëren of verwijderen, maar u kunt dit niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-107">After you create a snapshot, you can read, copy, or delete it, but you cannot modify it.</span></span>

<span data-ttu-id="7c3b5-108">Een momentopname van een blob is identiek aan de base blob, behalve dat de blob-URI bevat een **DateTime** waarde toegevoegd aan de blob-URI om aan te geven van de tijd waarop de momentopname werd gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-108">A snapshot of a blob is identical to its base blob, except that the blob URI has a **DateTime** value appended to the blob URI to indicate the time at which the snapshot was taken.</span></span> <span data-ttu-id="7c3b5-109">Bijvoorbeeld, als een pagina blob-URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, de momentopname van de URI vergelijkbaar met is `http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-109">For example, if a page blob URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, the snapshot URI is similar to `http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span></span>

> [!NOTE]
> <span data-ttu-id="7c3b5-110">Alle momentopnamen delen de base blob-URI.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-110">All snapshots share the base blob's URI.</span></span> <span data-ttu-id="7c3b5-111">Het enige verschil tussen de base blob en de momentopname is de toegevoegde **DateTime** waarde.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-111">The only distinction between the base blob and the snapshot is the appended **DateTime** value.</span></span>
>

<span data-ttu-id="7c3b5-112">Een blob kan een onbeperkt aantal momentopnamen hebben.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-112">A blob can have any number of snapshots.</span></span> <span data-ttu-id="7c3b5-113">Momentopnamen bewaard totdat ze expliciet worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-113">Snapshots persist until they are explicitly deleted.</span></span> <span data-ttu-id="7c3b5-114">Een momentopname kan niet de base blob outlive.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-114">A snapshot cannot outlive its base blob.</span></span> <span data-ttu-id="7c3b5-115">U kunt de momentopnamen die zijn gekoppeld aan de basis blob om bij te houden van uw huidige momentopnamen opsommen.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-115">You can enumerate the snapshots associated with the base blob to track your current snapshots.</span></span>

<span data-ttu-id="7c3b5-116">Wanneer u een momentopname van een blob maakt, worden de blob-Systeemeigenschappen gekopieerd naar de momentopname met dezelfde waarden.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-116">When you create a snapshot of a blob, the blob's system properties are copied to the snapshot with the same values.</span></span> <span data-ttu-id="7c3b5-117">De base blob metagegevens wordt ook gekopieerd naar de momentopname, tenzij u afzonderlijke metagegevens voor de momentopname opgeven wanneer u dit hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-117">The base blob's metadata is also copied to the snapshot, unless you specify separate metadata for the snapshot when you create it.</span></span>

<span data-ttu-id="7c3b5-118">Alle leases die zijn gekoppeld aan de basis blob hebben geen invloed op de momentopname.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-118">Any leases associated with the base blob do not affect the snapshot.</span></span> <span data-ttu-id="7c3b5-119">U kunt een lease op een momentopname kan niet verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-119">You cannot acquire a lease on a snapshot.</span></span>

<span data-ttu-id="7c3b5-120">Een VHD-bestand wordt gebruikt voor het opslaan van de huidige informatie en status voor een VM-schijf.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-120">A VHD file is used to store the current information and status for a VM disk.</span></span> <span data-ttu-id="7c3b5-121">U kunt loskoppelen van een schijf uit vanuit de virtuele machine of sluit de virtuele machine en vervolgens een momentopname van de VHD-bestand.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-121">You can detach a disk from within the VM or shut down the VM, and then take a snapshot of its VHD file.</span></span> <span data-ttu-id="7c3b5-122">U kunt dat momentopnamebestand later gebruiken voor het ophalen van het VHD-bestand op dat moment en de virtuele machine opnieuw.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-122">You can use that snapshot file later to retrieve the VHD file at that point in time and recreate the VM.</span></span>

<span data-ttu-id="7c3b5-123">Versleuteling voor opslag-Service (SSE) is ingeschakeld voor het opslagaccount waarin de blob zich bevindt, wordt alle momentopnamen gehouden met de blob worden versleuteld in rust.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-123">If Storage Service Encryption (SSE) is enabled for the storage account in which the blob resides, then any snapshots taken of that blob will be encrypted at rest.</span></span>

## <a name="create-a-snapshot"></a><span data-ttu-id="7c3b5-124">Een momentopname maken</span><span class="sxs-lookup"><span data-stu-id="7c3b5-124">Create a snapshot</span></span>
<span data-ttu-id="7c3b5-125">De volgende voorbeeldcode laat zien hoe een momentopname te maken met behulp van de [Azure Storage-clientbibliotheek voor .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="7c3b5-125">The following code example shows how to create a snapshot by using the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="7c3b5-126">In dit voorbeeld bevat aanvullende metagegevens voor de momentopname wanneer deze wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-126">This example specifies additional metadata for the snapshot when it is created.</span></span>

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in the container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload the blob to create it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of the base blob.
        // Specify metadata at the time that the snapshot is created to specify unique metadata for the snapshot.
        // If no metadata is specified when the snapshot is created, the base blob's metadata is copied to the snapshot.
        Dictionary<string, string> metadata = new Dictionary<string, string>();
        metadata.Add("ApproxSnapshotCreatedDate", DateTime.UtcNow.ToString());
        await baseBlob.CreateSnapshotAsync(metadata, null, null, null);
    }
    catch (StorageException e)
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}
```

## <a name="copy-snapshots"></a><span data-ttu-id="7c3b5-127">Kopiëren van momentopnamen</span><span class="sxs-lookup"><span data-stu-id="7c3b5-127">Copy snapshots</span></span>
<span data-ttu-id="7c3b5-128">Kopieerbewerkingen met betrekking tot de blobs en momentopnamen van voldoen deze regels:</span><span class="sxs-lookup"><span data-stu-id="7c3b5-128">Copy operations involving blobs and snapshots follow these rules:</span></span>

* <span data-ttu-id="7c3b5-129">U kunt een momentopname via de base blob kopiëren.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-129">You can copy a snapshot over its base blob.</span></span> <span data-ttu-id="7c3b5-130">Door een momentopname met de positie van de basis blob te promoveren, kunt u een eerdere versie van een blob herstellen.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-130">By promoting a snapshot to the position of the base blob, you can restore an earlier version of a blob.</span></span> <span data-ttu-id="7c3b5-131">De momentopname blijft, maar de base blob wordt overschreven met een beschrijfbare kopie van de momentopname.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-131">The snapshot remains, but the base blob is overwritten with a writable copy of the snapshot.</span></span>
* <span data-ttu-id="7c3b5-132">U kunt een momentopname kopiëren naar een bestemmings-blob met een andere naam.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-132">You can copy a snapshot to a destination blob with a different name.</span></span> <span data-ttu-id="7c3b5-133">De resulterende bestemmings-blob is een beschrijfbare blob en niet een momentopname.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-133">The resulting destination blob is a writable blob and not a snapshot.</span></span>
* <span data-ttu-id="7c3b5-134">Als een bron-blob zijn gekopieerd, worden alle momentopnamen van de bron-blob niet gekopieerd naar de bestemming.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-134">When a source blob is copied, any snapshots of the source blob are not copied to the destination.</span></span> <span data-ttu-id="7c3b5-135">Wanneer een bestemmings-blob is overschreven door een exemplaar, zijn de momentopnamen die zijn gekoppeld aan de oorspronkelijke bestemmings-blob blijven behouden.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-135">When a destination blob is overwritten with a copy, any snapshots associated with the original destination blob remain intact.</span></span>
* <span data-ttu-id="7c3b5-136">Bij het maken van een momentopname van een blok-blob is ook de blob doorgevoerd blokkeringslijst gekopieerd naar de momentopname.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-136">When you create a snapshot of a block blob, the blob's committed block list is also copied to the snapshot.</span></span> <span data-ttu-id="7c3b5-137">Een niet-doorgevoerde blokken worden niet gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-137">Any uncommitted blocks are not copied.</span></span>

## <a name="specify-an-access-condition"></a><span data-ttu-id="7c3b5-138">Geef een voorwaarde voor toegang</span><span class="sxs-lookup"><span data-stu-id="7c3b5-138">Specify an access condition</span></span>
<span data-ttu-id="7c3b5-139">Als u aanroept [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], kunt u een voorwaarde voor toegang opgeven, zodat de momentopname alleen gemaakt wordt als een voorwaarde wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-139">When you call [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], you can specify an access condition so that the snapshot is created only if a condition is met.</span></span> <span data-ttu-id="7c3b5-140">Als u een voorwaarde voor toegang, gebruik de [AccessCondition] [ dotnet_AccessCondition] parameter.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-140">To specify an access condition, use the [AccessCondition][dotnet_AccessCondition] parameter.</span></span> <span data-ttu-id="7c3b5-141">Als niet aan de opgegeven voorwaarde wordt voldaan, wordt de momentopname niet gemaakt is en de Blob-service statuscode retourneert [HTTPStatusCode][dotnet_HTTPStatusCode]. PreconditionFailed.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-141">If the specified condition is not met, the snapshot is not created, and the Blob service returns status code [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span></span>

## <a name="delete-snapshots"></a><span data-ttu-id="7c3b5-142">Verwijder momentopnamen</span><span class="sxs-lookup"><span data-stu-id="7c3b5-142">Delete snapshots</span></span>
<span data-ttu-id="7c3b5-143">U kunt een blob met de momentopnamen niet verwijderen, tenzij de momentopnamen worden ook verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-143">You can't delete a blob with snapshots unless the snapshots are also deleted.</span></span> <span data-ttu-id="7c3b5-144">U kunt een momentopname van een afzonderlijk verwijderen of opgeven dat alle momentopnamen worden verwijderd wanneer de bron-blob is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-144">You can delete a snapshot individually, or specify that all snapshots be deleted when the source blob is deleted.</span></span> <span data-ttu-id="7c3b5-145">Als u probeert te verwijderen van een blob die nog steeds momentopnamen bevat, wordt een fout resulteert.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-145">If you attempt to delete a blob that still has snapshots, an error results.</span></span>

<span data-ttu-id="7c3b5-146">De volgende voorbeeldcode laat zien hoe een blob en bijbehorende momentopnamen in .NET, te verwijderen waar `blockBlob` is een object van het type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span><span class="sxs-lookup"><span data-stu-id="7c3b5-146">The following code example shows how to delete a blob and its snapshots in .NET, where `blockBlob` is an object of type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span></span>

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a><span data-ttu-id="7c3b5-147">Momentopnamen met Azure Premium-opslag</span><span class="sxs-lookup"><span data-stu-id="7c3b5-147">Snapshots with Azure Premium Storage</span></span>
<span data-ttu-id="7c3b5-148">Als u momentopnamen met Premium-opslag, gelden de volgende regels:</span><span class="sxs-lookup"><span data-stu-id="7c3b5-148">When using snapshots with Premium Storage, the following rules apply:</span></span>

* <span data-ttu-id="7c3b5-149">Het maximum aantal momentopnamen per pagina-blob in een premium storage-account is 100.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-149">The maximum number of snapshots per page blob in a premium storage account is 100.</span></span> <span data-ttu-id="7c3b5-150">Als deze limiet wordt overschreden, de momentopname Blob-bewerking retourneert foutcode 409 (`SnapshotCountExceeded`).</span><span class="sxs-lookup"><span data-stu-id="7c3b5-150">If that limit is exceeded, the Snapshot Blob operation returns error code 409 (`SnapshotCountExceeded`).</span></span>
* <span data-ttu-id="7c3b5-151">U kunt een momentopname van een pagina-blob nemen in een premium storage-account om de 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-151">You can take a snapshot of a page blob in a premium storage account once every 10 minutes.</span></span> <span data-ttu-id="7c3b5-152">Als dit percentage wordt overschreden, de momentopname Blob-bewerking retourneert foutcode 409 (`SnapshotOperationRateExceeded`).</span><span class="sxs-lookup"><span data-stu-id="7c3b5-152">If that rate is exceeded, the Snapshot Blob operation returns error code 409 (`SnapshotOperationRateExceeded`).</span></span>
* <span data-ttu-id="7c3b5-153">Om te lezen van een momentopname, kunt u de bewerking Blob kopiëren naar een momentopname kopiëren naar een andere paginablob in het account.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-153">To read a snapshot, you can use the Copy Blob operation to copy a snapshot to another page blob in the account.</span></span> <span data-ttu-id="7c3b5-154">De bestemmings-blob voor de kopieerbewerking mag geen eventuele bestaande momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-154">The destination blob for the copy operation must not have any existing snapshots.</span></span> <span data-ttu-id="7c3b5-155">Als de bestemmings-blob momentopnamen heeft, wordt de kopie Blob-bewerking foutcode 409 retourneert (`SnapshotsPresent`).</span><span class="sxs-lookup"><span data-stu-id="7c3b5-155">If the destination blob does have snapshots, then the Copy Blob operation returns error code 409 (`SnapshotsPresent`).</span></span>

## <a name="return-the-absolute-uri-to-a-snapshot"></a><span data-ttu-id="7c3b5-156">Retourneert de absolute URI naar een momentopname</span><span class="sxs-lookup"><span data-stu-id="7c3b5-156">Return the absolute URI to a snapshot</span></span>
<span data-ttu-id="7c3b5-157">In dit voorbeeld C#-code maakt een momentopname en schrijft de absolute URI voor de primaire locatie.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-157">This C# code example creates a snapshot and writes out the absolute URI for the primary location.</span></span>

```csharp
//Create the blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference to a blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of the blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a><span data-ttu-id="7c3b5-158">Begrijpen hoe de kosten voor het samenvoegen van momentopnamen</span><span class="sxs-lookup"><span data-stu-id="7c3b5-158">Understand how snapshots accrue charges</span></span>
<span data-ttu-id="7c3b5-159">Maken van een momentopname een alleen-lezen kopie van een blob is, kan leiden tot aanvullende gegevens opslagkosten aan uw account.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-159">Creating a snapshot, which is a read-only copy of a blob, can result in additional data storage charges to your account.</span></span> <span data-ttu-id="7c3b5-160">Bij het ontwerpen van uw toepassing, is het belangrijk te weten van hoe deze kosten doorlopen kunnen, zodat u de kosten kunt minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-160">When designing your application, it is important to be aware of how these charges might accrue so that you can minimize costs.</span></span>

### <a name="important-billing-considerations"></a><span data-ttu-id="7c3b5-161">Belangrijke overwegingen voor facturering</span><span class="sxs-lookup"><span data-stu-id="7c3b5-161">Important billing considerations</span></span>
<span data-ttu-id="7c3b5-162">De volgende lijst bevat de belangrijkste punten in overweging moet nemen bij het maken van een momentopname.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-162">The following list includes key points to consider when creating a snapshot.</span></span>

* <span data-ttu-id="7c3b5-163">Uw opslagaccount leidt ertoe dat de kosten voor unieke blokken of pagina's, ongeacht of deze in de blob of in de momentopname.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-163">Your storage account incurs charges for unique blocks or pages, whether they are in the blob or in the snapshot.</span></span> <span data-ttu-id="7c3b5-164">Uw account heeft geen gevolgen voor de extra kosten voor momentopnamen die zijn gekoppeld met een blob, totdat u de blob waarop ze zijn gebaseerd bijwerkt.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-164">Your account does not incur additional charges for snapshots associated with a blob until you update the blob on which they are based.</span></span> <span data-ttu-id="7c3b5-165">Na het bijwerken van de basis blob, wordt deze afwijkt van de momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-165">After you update the base blob, it diverges from its snapshots.</span></span> <span data-ttu-id="7c3b5-166">Als dit gebeurt, wordt u in rekening gebracht voor de unieke blokken of pagina's in elke blob of een momentopname.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-166">When this happens, you are charged for the unique blocks or pages in each blob or snapshot.</span></span>
* <span data-ttu-id="7c3b5-167">Wanneer u een blok binnen een blok-blob vervangt, dat blok wordt vervolgens in rekening gebracht als unieke blok.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-167">When you replace a block within a block blob, that block is subsequently charged as a unique block.</span></span> <span data-ttu-id="7c3b5-168">Dit geldt zelfs als het blok heeft dezelfde blok-ID en dezelfde gegevens er in de momentopname.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-168">This is true even if the block has the same block ID and the same data as it has in the snapshot.</span></span> <span data-ttu-id="7c3b5-169">Nadat het blok doorgevoerd is opnieuw het afwijkt van het bijbehorende equivalent in een momentopname en wordt u gefactureerd voor de gegevens.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-169">After the block is committed again, it diverges from its counterpart in any snapshot, and you will be charged for its data.</span></span> <span data-ttu-id="7c3b5-170">Hetzelfde geldt voor een pagina in een pagina-blob bijgewerkt met identieke gegevens.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-170">The same holds true for a page in a page blob that's updated with identical data.</span></span>
* <span data-ttu-id="7c3b5-171">Een blok-blob vervangen door het aanroepen van de [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream] [ dotnet_UploadFromStream], of [UploadFromByteArray] [ dotnet_UploadFromByteArray] vervangt alle blokken in de blob-methode.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-171">Replacing a block blob by calling the [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] method replaces all blocks in the blob.</span></span> <span data-ttu-id="7c3b5-172">Als er een momentopname die is gekoppeld aan blob, alle blokken in de basis-blob en momentopname nu luidsprekers en wordt u gefactureerd voor alle blokken in beide blobs.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-172">If you have a snapshot associated with that blob, all blocks in the base blob and snapshot now diverge, and you will be charged for all the blocks in both blobs.</span></span> <span data-ttu-id="7c3b5-173">Dit geldt zelfs als de gegevens in de base blob en de momentopname identiek.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-173">This is true even if the data in the base blob and the snapshot remain identical.</span></span>
* <span data-ttu-id="7c3b5-174">De Azure Blob-service heeft geen een manier om te bepalen of twee blokken identieke gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-174">The Azure Blob service does not have a means to determine whether two blocks contain identical data.</span></span> <span data-ttu-id="7c3b5-175">Elk blok dat wordt geüpload en doorgevoerd wordt behandeld als uniek zijn, zelfs als deze dezelfde gegevens en de dezelfde blok-ID heeft.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-175">Each block that is uploaded and committed is treated as unique, even if it has the same data and the same block ID.</span></span> <span data-ttu-id="7c3b5-176">Omdat kosten voor unieke blokken doorlopen, is het belangrijk in die voor het bijwerken van een blob met een momentopname resulteert in extra unieke blokken en extra kosten.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-176">Because charges accrue for unique blocks, it's important to consider that updating a blob that has a snapshot results in additional unique blocks and additional charges.</span></span>

### <a name="minimize-cost-with-snapshot-management"></a><span data-ttu-id="7c3b5-177">Kosten met beheer van momentopnamen beperken</span><span class="sxs-lookup"><span data-stu-id="7c3b5-177">Minimize cost with snapshot management</span></span>

<span data-ttu-id="7c3b5-178">Het is raadzaam om het beheer van uw momentopnamen zorgvuldig om te voorkomen dat extra kosten.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-178">We recommend managing your snapshots carefully to avoid extra charges.</span></span> <span data-ttu-id="7c3b5-179">U kunt deze best practices te helpen de kosten van de opslag van uw momentopnamen minimaliseren volgen:</span><span class="sxs-lookup"><span data-stu-id="7c3b5-179">You can follow these best practices to help minimize the costs incurred by the storage of your snapshots:</span></span>

* <span data-ttu-id="7c3b5-180">Verwijderen en opnieuw maken van momentopnamen die zijn gekoppeld met een blob telkens wanneer u de blob bijwerkt, zelfs als u met identieke gegevens bijwerken wilt tenzij ontwerp van uw toepassing vereist is voor het onderhouden van momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-180">Delete and re-create snapshots associated with a blob whenever you update the blob, even if you are updating with identical data, unless your application design requires that you maintain snapshots.</span></span> <span data-ttu-id="7c3b5-181">Door te verwijderen en opnieuw maken van de blob-momentopnamen, kunt u ervoor zorgen dat de blob en momentopnamen niet luidsprekers.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-181">By deleting and re-creating the blob's snapshots, you can ensure that the blob and snapshots do not diverge.</span></span>
* <span data-ttu-id="7c3b5-182">Als u momentopnamen voor een blob en onderhoudt voorkomen dat de aanroepen [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], of [UploadFromByteArray] [ dotnet_UploadFromByteArray] bijwerken van de blob.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-182">If you are maintaining snapshots for a blob, avoid calling [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] to update the blob.</span></span> <span data-ttu-id="7c3b5-183">Deze methoden vervangen van alle van de gegevensblokken die zich in de blob, waardoor uw base blob en bijbehorende momentopnamen aanzienlijk afwijkt.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-183">These methods replace all of the blocks in the blob, causing your base blob and its snapshots to diverge significantly.</span></span> <span data-ttu-id="7c3b5-184">In plaats daarvan het minste aantal blokken bijwerken met behulp van de [PutBlock] [ dotnet_PutBlock] en [PutBlockList] [ dotnet_PutBlockList] methoden.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-184">Instead, update the fewest possible number of blocks by using the [PutBlock][dotnet_PutBlock] and [PutBlockList][dotnet_PutBlockList] methods.</span></span>

### <a name="snapshot-billing-scenarios"></a><span data-ttu-id="7c3b5-185">Momentopname facturering scenario 's</span><span class="sxs-lookup"><span data-stu-id="7c3b5-185">Snapshot billing scenarios</span></span>
<span data-ttu-id="7c3b5-186">De volgende scenario's laten zien hoe de kosten voor een blok-blob en bijbehorende momentopnamen doorlopen.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-186">The following scenarios demonstrate how charges accrue for a block blob and its snapshots.</span></span>

<span data-ttu-id="7c3b5-187">**Scenario 1**</span><span class="sxs-lookup"><span data-stu-id="7c3b5-187">**Scenario 1**</span></span>

<span data-ttu-id="7c3b5-188">In scenario 1, is de base blob niet bijgewerkt nadat de momentopname werd gemaakt, zodat de kosten verbonden zijn alleen voor unieke blokken 1, 2 en 3.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-188">In scenario 1, the base blob has not been updated after the snapshot was taken, so charges are incurred only for unique blocks 1, 2, and 3.</span></span>

![Azure Storage-resources](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

<span data-ttu-id="7c3b5-190">**Scenario 2**</span><span class="sxs-lookup"><span data-stu-id="7c3b5-190">**Scenario 2**</span></span>

<span data-ttu-id="7c3b5-191">In scenario 2 de base blob is bijgewerkt, maar de momentopname niet heeft.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-191">In scenario 2, the base blob has been updated, but the snapshot has not.</span></span> <span data-ttu-id="7c3b5-192">Blok 3 is bijgewerkt en hoewel het bevat dezelfde gegevens en dezelfde ID, het is niet hetzelfde als 3 in de momentopname geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-192">Block 3 was updated, and even though it contains the same data and the same ID, it is not the same as block 3 in the snapshot.</span></span> <span data-ttu-id="7c3b5-193">Als gevolg hiervan het account wordt in rekening gebracht voor vier blokken.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-193">As a result, the account is charged for four blocks.</span></span>

![Azure Storage-resources](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

<span data-ttu-id="7c3b5-195">**Scenario 3**</span><span class="sxs-lookup"><span data-stu-id="7c3b5-195">**Scenario 3**</span></span>

<span data-ttu-id="7c3b5-196">In scenario 3 de base blob is bijgewerkt, maar de momentopname niet heeft.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-196">In scenario 3, the base blob has been updated, but the snapshot has not.</span></span> <span data-ttu-id="7c3b5-197">Blok 3 is vervangen door blok 4 in de base blob, maar de momentopname weerspiegelt nog steeds blok 3.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-197">Block 3 was replaced with block 4 in the base blob, but the snapshot still reflects block 3.</span></span> <span data-ttu-id="7c3b5-198">Als gevolg hiervan het account wordt in rekening gebracht voor vier blokken.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-198">As a result, the account is charged for four blocks.</span></span>

![Azure Storage-resources](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

<span data-ttu-id="7c3b5-200">**Scenario 4**</span><span class="sxs-lookup"><span data-stu-id="7c3b5-200">**Scenario 4**</span></span>

<span data-ttu-id="7c3b5-201">In scenario 4 de base blob volledig is bijgewerkt en geen van de oorspronkelijke blokken bevat.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-201">In scenario 4, the base blob has been completely updated and contains none of its original blocks.</span></span> <span data-ttu-id="7c3b5-202">Het account wordt hierdoor alle acht unieke blokken belast.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-202">As a result, the account is charged for all eight unique blocks.</span></span> <span data-ttu-id="7c3b5-203">Dit kan gebeuren als u een update-methode, zoals [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], of [UploadFromByteArray][dotnet_UploadFromByteArray], omdat deze methoden vervangen van alle van de inhoud van een blob.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-203">This scenario can occur if you are using an update method such as [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray], because these methods replace all of the contents of a blob.</span></span>

![Azure Storage-resources](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a><span data-ttu-id="7c3b5-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7c3b5-205">Next steps</span></span>

* <span data-ttu-id="7c3b5-206">U vindt meer informatie over het werken met momentopnamen van virtuele machine (VM)-schijf in [Back-up van Azure niet-beheerde VM-schijven met incrementele momentopnamen](storage-incremental-snapshots.md)</span><span class="sxs-lookup"><span data-stu-id="7c3b5-206">You can find more information about working with virtual machine (VM) disk snapshots in [Back up Azure unmanaged VM disks with incremental snapshots](storage-incremental-snapshots.md)</span></span>

* <span data-ttu-id="7c3b5-207">Zie voor aanvullende codevoorbeelden met behulp van Blob-opslag, [Azure codevoorbeelden](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span><span class="sxs-lookup"><span data-stu-id="7c3b5-207">For additional code examples using Blob storage, see [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span></span> <span data-ttu-id="7c3b5-208">Een voorbeeld van een toepassing te downloaden en uitvoeren, of de code op GitHub bladeren.</span><span class="sxs-lookup"><span data-stu-id="7c3b5-208">You can download a sample application and run it, or browse the code on GitHub.</span></span>

[dotnet_AccessCondition]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.accesscondition.aspx
[dotnet_CloudBlockBlob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.aspx
[dotnet_CreateSnapshotAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.createsnapshotasync.aspx
[dotnet_HTTPStatusCode]: https://msdn.microsoft.com/library/system.net.httpstatuscode(v=vs.110).aspx
[dotnet_PutBlockList]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblocklist.aspx
[dotnet_PutBlock]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblock.aspx
[dotnet_UploadFromByteArray]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfrombytearray.aspx
[dotnet_UploadFromFile]: https://msdn.microsoft.com/library/azure/mt705654.aspx
[dotnet_UploadFromStream]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfromstream.aspx
[dotnet_UploadText]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadtext.aspx