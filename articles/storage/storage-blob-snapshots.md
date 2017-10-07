---
title: een alleen-lezen momentopname van een blob in Azure Storage aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een momentopname van een blob-tooback van blob-gegevens op een gegeven moment. Begrijpen hoe momentopnamen worden gefactureerd en hoe toouse ze toominimize capaciteit kosten.
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
ms.openlocfilehash: 9e7af611e885d83df69d3329217f261b3f3f333e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-blob-snapshot"></a><span data-ttu-id="7f1c5-104">Een blob-momentopname maken</span><span class="sxs-lookup"><span data-stu-id="7f1c5-104">Create a blob snapshot</span></span>

<span data-ttu-id="7f1c5-105">Een momentopname is een alleen-lezen-versie van een blob die wordt uitgevoerd op een punt in tijd.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-105">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="7f1c5-106">Momentopnamen zijn nuttig voor back-up blobs.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-106">Snapshots are useful for backing up blobs.</span></span> <span data-ttu-id="7f1c5-107">Nadat u een momentopname gemaakt, lezen, kopiëren of verwijderen, maar u kunt dit niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-107">After you create a snapshot, you can read, copy, or delete it, but you cannot modify it.</span></span>

<span data-ttu-id="7f1c5-108">Een momentopname van een blob is identiek tooits base blob, behalve Hallo blob-URI bevat een **DateTime** waarde toegevoegd toohello blob-URI tooindicate Hallo moment op welke Hallo momentopname werd gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-108">A snapshot of a blob is identical tooits base blob, except that hello blob URI has a **DateTime** value appended toohello blob URI tooindicate hello time at which hello snapshot was taken.</span></span> <span data-ttu-id="7f1c5-109">Bijvoorbeeld, als een pagina blob-URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, Hallo momentopname URI lijkt te`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-109">For example, if a page blob URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, hello snapshot URI is similar too`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span></span>

> [!NOTE]
> <span data-ttu-id="7f1c5-110">Alle momentopnamen delen Hallo base blob-URI.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-110">All snapshots share hello base blob's URI.</span></span> <span data-ttu-id="7f1c5-111">alleen onderscheid tussen Hallo base blob en Hallo momentopname toegevoegd Hallo is Hallo **DateTime** waarde.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-111">hello only distinction between hello base blob and hello snapshot is hello appended **DateTime** value.</span></span>
>

<span data-ttu-id="7f1c5-112">Een blob kan een onbeperkt aantal momentopnamen hebben.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-112">A blob can have any number of snapshots.</span></span> <span data-ttu-id="7f1c5-113">Momentopnamen bewaard totdat ze expliciet worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-113">Snapshots persist until they are explicitly deleted.</span></span> <span data-ttu-id="7f1c5-114">Een momentopname kan niet de base blob outlive.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-114">A snapshot cannot outlive its base blob.</span></span> <span data-ttu-id="7f1c5-115">U kunt Hallo momentopnamen die zijn gekoppeld aan Hallo base blob tootrack opsommen uw huidige momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-115">You can enumerate hello snapshots associated with hello base blob tootrack your current snapshots.</span></span>

<span data-ttu-id="7f1c5-116">Bij het maken van een momentopname van een blob Hallo Systeemeigenschappen van blob zijn gekopieerde toohello momentopname Hello dezelfde waarden.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-116">When you create a snapshot of a blob, hello blob's system properties are copied toohello snapshot with hello same values.</span></span> <span data-ttu-id="7f1c5-117">Hallo base blob-metagegevens zijn ook gekopieerde toohello momentopname, tenzij u afzonderlijke metagegevens voor wanneer u deze maakt een momentopname Hallo opgeeft.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-117">hello base blob's metadata is also copied toohello snapshot, unless you specify separate metadata for hello snapshot when you create it.</span></span>

<span data-ttu-id="7f1c5-118">Alle leases die zijn gekoppeld aan basis blob Hallo hebben geen invloed op Hallo momentopname.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-118">Any leases associated with hello base blob do not affect hello snapshot.</span></span> <span data-ttu-id="7f1c5-119">U kunt een lease op een momentopname kan niet verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-119">You cannot acquire a lease on a snapshot.</span></span>

<span data-ttu-id="7f1c5-120">Een VHD-bestand is gebruikte toostore Hallo actuele informatie en status voor een VM-schijf.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-120">A VHD file is used toostore hello current information and status for a VM disk.</span></span> <span data-ttu-id="7f1c5-121">U kunt een schijf uit binnen Hallo VM loskoppelen of Hallo VM afsluiten en vervolgens een momentopname van de VHD-bestand.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-121">You can detach a disk from within hello VM or shut down hello VM, and then take a snapshot of its VHD file.</span></span> <span data-ttu-id="7f1c5-122">Kunt u dat momentopnamebestand hoger tooretrieve Hallo VHD-bestand op dat punt in tijd en maak deze opnieuw Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-122">You can use that snapshot file later tooretrieve hello VHD file at that point in time and recreate hello VM.</span></span>

<span data-ttu-id="7f1c5-123">Als versleuteling voor opslag-Service (SSE) is ingeschakeld voor Hallo storage-account in welke Hallo blob zich bevindt en vervolgens alle momentopnamen van blob is genomen, worden versleuteld in rust.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-123">If Storage Service Encryption (SSE) is enabled for hello storage account in which hello blob resides, then any snapshots taken of that blob will be encrypted at rest.</span></span>

## <a name="create-a-snapshot"></a><span data-ttu-id="7f1c5-124">Een momentopname maken</span><span class="sxs-lookup"><span data-stu-id="7f1c5-124">Create a snapshot</span></span>
<span data-ttu-id="7f1c5-125">Hallo volgende voorbeeldcode laat zien hoe een momentopname met behulp van toocreate Hallo [Azure Storage-clientbibliotheek voor .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="7f1c5-125">hello following code example shows how toocreate a snapshot by using hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="7f1c5-126">In dit voorbeeld bevat aanvullende metagegevens voor Hallo momentopname wanneer deze wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-126">This example specifies additional metadata for hello snapshot when it is created.</span></span>

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in hello container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload hello blob toocreate it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of hello base blob.
        // Specify metadata at hello time that hello snapshot is created toospecify unique metadata for hello snapshot.
        // If no metadata is specified when hello snapshot is created, hello base blob's metadata is copied toohello snapshot.
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

## <a name="copy-snapshots"></a><span data-ttu-id="7f1c5-127">Kopiëren van momentopnamen</span><span class="sxs-lookup"><span data-stu-id="7f1c5-127">Copy snapshots</span></span>
<span data-ttu-id="7f1c5-128">Kopieerbewerkingen met betrekking tot de blobs en momentopnamen van voldoen deze regels:</span><span class="sxs-lookup"><span data-stu-id="7f1c5-128">Copy operations involving blobs and snapshots follow these rules:</span></span>

* <span data-ttu-id="7f1c5-129">U kunt een momentopname via de base blob kopiëren.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-129">You can copy a snapshot over its base blob.</span></span> <span data-ttu-id="7f1c5-130">Door de positie van een momentopname toohello van Hallo base blob te promoveren, kunt u een eerdere versie van een blob herstellen.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-130">By promoting a snapshot toohello position of hello base blob, you can restore an earlier version of a blob.</span></span> <span data-ttu-id="7f1c5-131">Hallo momentopname blijft, maar Hallo base blob wordt overschreven met een beschrijfbare kopie van Hallo momentopname.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-131">hello snapshot remains, but hello base blob is overwritten with a writable copy of hello snapshot.</span></span>
* <span data-ttu-id="7f1c5-132">U kunt een momentopname tooa bestemmings-blob met een andere naam kopiëren.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-132">You can copy a snapshot tooa destination blob with a different name.</span></span> <span data-ttu-id="7f1c5-133">Hallo resulterende bestemmings-blob is een beschrijfbare blob en niet een momentopname.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-133">hello resulting destination blob is a writable blob and not a snapshot.</span></span>
* <span data-ttu-id="7f1c5-134">Als een bron-blob zijn gekopieerd, zijn de momentopnamen van de bron-blob Hallo niet gekopieerde toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-134">When a source blob is copied, any snapshots of hello source blob are not copied toohello destination.</span></span> <span data-ttu-id="7f1c5-135">Wanneer een bestemmings-blob is overschreven door een exemplaar, zijn de momentopnamen die zijn gekoppeld aan de oorspronkelijke bestemmings-blob Hallo blijven behouden.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-135">When a destination blob is overwritten with a copy, any snapshots associated with hello original destination blob remain intact.</span></span>
* <span data-ttu-id="7f1c5-136">Bij het maken van een momentopname van een blok-blob is doorgevoerd Hallo-blob-blokkeringslijst ook gekopieerde toohello momentopname.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-136">When you create a snapshot of a block blob, hello blob's committed block list is also copied toohello snapshot.</span></span> <span data-ttu-id="7f1c5-137">Een niet-doorgevoerde blokken worden niet gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-137">Any uncommitted blocks are not copied.</span></span>

## <a name="specify-an-access-condition"></a><span data-ttu-id="7f1c5-138">Geef een voorwaarde voor toegang</span><span class="sxs-lookup"><span data-stu-id="7f1c5-138">Specify an access condition</span></span>
<span data-ttu-id="7f1c5-139">Als u aanroept [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], kunt u een voorwaarde voor toegang opgeven zodat hello momentopname alleen gemaakt wordt als een voorwaarde wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-139">When you call [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], you can specify an access condition so that hello snapshot is created only if a condition is met.</span></span> <span data-ttu-id="7f1c5-140">toospecify een voorwaarde voor toegang, gebruik Hallo [AccessCondition] [ dotnet_AccessCondition] parameter.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-140">toospecify an access condition, use hello [AccessCondition][dotnet_AccessCondition] parameter.</span></span> <span data-ttu-id="7f1c5-141">Als Hallo opgegeven niet aan de voorwaarde is voldaan, Hallo momentopname is niet gemaakt en Hallo Blob-service retourneert statuscode [HTTPStatusCode][dotnet_HTTPStatusCode]. PreconditionFailed.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-141">If hello specified condition is not met, hello snapshot is not created, and hello Blob service returns status code [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span></span>

## <a name="delete-snapshots"></a><span data-ttu-id="7f1c5-142">Verwijder momentopnamen</span><span class="sxs-lookup"><span data-stu-id="7f1c5-142">Delete snapshots</span></span>
<span data-ttu-id="7f1c5-143">U kunt een blob met de momentopnamen niet verwijderen, tenzij Hallo momentopnamen worden ook verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-143">You can't delete a blob with snapshots unless hello snapshots are also deleted.</span></span> <span data-ttu-id="7f1c5-144">U kunt een momentopname van een afzonderlijk verwijderen of u kunt opgeven dat alle momentopnamen worden verwijderd wanneer de bron-blob hello wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-144">You can delete a snapshot individually, or specify that all snapshots be deleted when hello source blob is deleted.</span></span> <span data-ttu-id="7f1c5-145">Als u een blob die nog steeds momentopnamen toodelete probeert, wordt er een fout resulteert.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-145">If you attempt toodelete a blob that still has snapshots, an error results.</span></span>

<span data-ttu-id="7f1c5-146">Hallo van de volgende code voorbeeld ziet u hoe toodelete een blob en bijbehorende momentopnamen in .NET waar `blockBlob` is een object van het type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span><span class="sxs-lookup"><span data-stu-id="7f1c5-146">hello following code example shows how toodelete a blob and its snapshots in .NET, where `blockBlob` is an object of type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span></span>

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a><span data-ttu-id="7f1c5-147">Momentopnamen met Azure Premium-opslag</span><span class="sxs-lookup"><span data-stu-id="7f1c5-147">Snapshots with Azure Premium Storage</span></span>
<span data-ttu-id="7f1c5-148">Als u momentopnamen met Premium-opslag, Hallo volgens de regels van toepassing:</span><span class="sxs-lookup"><span data-stu-id="7f1c5-148">When using snapshots with Premium Storage, hello following rules apply:</span></span>

* <span data-ttu-id="7f1c5-149">Hallo kunt u het maximum aantal momentopnamen per pagina-blob in een premium storage-account is 100.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-149">hello maximum number of snapshots per page blob in a premium storage account is 100.</span></span> <span data-ttu-id="7f1c5-150">Als deze limiet wordt overschreden, Hallo momentopname Blob bewerking retourneert foutcode 409 (`SnapshotCountExceeded`).</span><span class="sxs-lookup"><span data-stu-id="7f1c5-150">If that limit is exceeded, hello Snapshot Blob operation returns error code 409 (`SnapshotCountExceeded`).</span></span>
* <span data-ttu-id="7f1c5-151">U kunt een momentopname van een pagina-blob nemen in een premium storage-account om de 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-151">You can take a snapshot of a page blob in a premium storage account once every 10 minutes.</span></span> <span data-ttu-id="7f1c5-152">Als dit percentage wordt overschreden, Hallo momentopname Blob bewerking retourneert foutcode 409 (`SnapshotOperationRateExceeded`).</span><span class="sxs-lookup"><span data-stu-id="7f1c5-152">If that rate is exceeded, hello Snapshot Blob operation returns error code 409 (`SnapshotOperationRateExceeded`).</span></span>
* <span data-ttu-id="7f1c5-153">tooread een momentopname, kunt u Hallo Blob kopiëren bewerking toocopy een momentopname tooanother pagina-blob in Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-153">tooread a snapshot, you can use hello Copy Blob operation toocopy a snapshot tooanother page blob in hello account.</span></span> <span data-ttu-id="7f1c5-154">Hallo bestemmings-blob voor de kopieerbewerking Hallo mag geen eventuele bestaande momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-154">hello destination blob for hello copy operation must not have any existing snapshots.</span></span> <span data-ttu-id="7f1c5-155">Als Hallo bestemmings-blob momentopnamen heeft, dan Hallo Blob kopiëren bewerking foutcode 409 retourneert (`SnapshotsPresent`).</span><span class="sxs-lookup"><span data-stu-id="7f1c5-155">If hello destination blob does have snapshots, then hello Copy Blob operation returns error code 409 (`SnapshotsPresent`).</span></span>

## <a name="return-hello-absolute-uri-tooa-snapshot"></a><span data-ttu-id="7f1c5-156">Hallo absolute URI tooa momentopname retourneren</span><span class="sxs-lookup"><span data-stu-id="7f1c5-156">Return hello absolute URI tooa snapshot</span></span>
<span data-ttu-id="7f1c5-157">In dit voorbeeld C#-code wordt een momentopname gemaakt en schrijft Hallo absolute URI voor de primaire locatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-157">This C# code example creates a snapshot and writes out hello absolute URI for hello primary location.</span></span>

```csharp
//Create hello blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference tooa blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of hello blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a><span data-ttu-id="7f1c5-158">Begrijpen hoe de kosten voor het samenvoegen van momentopnamen</span><span class="sxs-lookup"><span data-stu-id="7f1c5-158">Understand how snapshots accrue charges</span></span>
<span data-ttu-id="7f1c5-159">Maken van een momentopname een alleen-lezen kopie van een blob is, kan leiden tot aanvullende gegevens storage kosten tooyour-account.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-159">Creating a snapshot, which is a read-only copy of a blob, can result in additional data storage charges tooyour account.</span></span> <span data-ttu-id="7f1c5-160">Bij het ontwerpen van uw toepassing, is het belangrijk toobe weten hoe deze kosten doorlopen kunnen, zodat u de kosten kunt minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-160">When designing your application, it is important toobe aware of how these charges might accrue so that you can minimize costs.</span></span>

### <a name="important-billing-considerations"></a><span data-ttu-id="7f1c5-161">Belangrijke overwegingen voor facturering</span><span class="sxs-lookup"><span data-stu-id="7f1c5-161">Important billing considerations</span></span>
<span data-ttu-id="7f1c5-162">Hallo volgende lijst bevat belangrijke punten tooconsider bij het maken van een momentopname.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-162">hello following list includes key points tooconsider when creating a snapshot.</span></span>

* <span data-ttu-id="7f1c5-163">Uw opslagaccount leidt ertoe dat de kosten voor unieke blokken of pagina's, ongeacht of deze in de blob Hallo of in momentopname Hallo.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-163">Your storage account incurs charges for unique blocks or pages, whether they are in hello blob or in hello snapshot.</span></span> <span data-ttu-id="7f1c5-164">Uw account heeft geen gevolgen voor de extra kosten voor momentopnamen die zijn gekoppeld met een blob, totdat u bijwerkt Hallo blob waarop ze zijn gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-164">Your account does not incur additional charges for snapshots associated with a blob until you update hello blob on which they are based.</span></span> <span data-ttu-id="7f1c5-165">Na het bijwerken van Hallo base blob, wordt deze afwijkt van de momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-165">After you update hello base blob, it diverges from its snapshots.</span></span> <span data-ttu-id="7f1c5-166">Als dit gebeurt, wordt u in rekening gebracht voor unieke Hallo-blokken of pagina's in elke blob of een momentopname.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-166">When this happens, you are charged for hello unique blocks or pages in each blob or snapshot.</span></span>
* <span data-ttu-id="7f1c5-167">Wanneer u een blok binnen een blok-blob vervangt, dat blok wordt vervolgens in rekening gebracht als unieke blok.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-167">When you replace a block within a block blob, that block is subsequently charged as a unique block.</span></span> <span data-ttu-id="7f1c5-168">Dit geldt zelfs wanneer Hallo-blok heeft Hallo dezelfde ID blokkeren en Hallo dezelfde gegevens zoals deze in momentopname Hallo heeft.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-168">This is true even if hello block has hello same block ID and hello same data as it has in hello snapshot.</span></span> <span data-ttu-id="7f1c5-169">Nadat Hallo blok doorgevoerd is opnieuw het afwijkt van het bijbehorende equivalent in een momentopname en wordt u gefactureerd voor de gegevens.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-169">After hello block is committed again, it diverges from its counterpart in any snapshot, and you will be charged for its data.</span></span> <span data-ttu-id="7f1c5-170">Hallo die dezelfde geldt voor een pagina in een pagina-blob bijgewerkt met identieke gegevens.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-170">hello same holds true for a page in a page blob that's updated with identical data.</span></span>
* <span data-ttu-id="7f1c5-171">Een blok-blob vervangen door de aanroepende Hallo [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream] [ dotnet_UploadFromStream], of [UploadFromByteArray] [ dotnet_UploadFromByteArray] vervangt alle blokken in Hallo blob-methode.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-171">Replacing a block blob by calling hello [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] method replaces all blocks in hello blob.</span></span> <span data-ttu-id="7f1c5-172">Als er een momentopname die is gekoppeld aan blob, alle blokken in Hallo base blob en momentopname nu luidsprekers en wordt u gefactureerd voor alle Hallo gegevensblokken die zich in beide blobs.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-172">If you have a snapshot associated with that blob, all blocks in hello base blob and snapshot now diverge, and you will be charged for all hello blocks in both blobs.</span></span> <span data-ttu-id="7f1c5-173">Dit geldt zelfs als het Hallo-gegevens in Hallo base blob en het Hallo-momentopname blijven identiek zijn.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-173">This is true even if hello data in hello base blob and hello snapshot remain identical.</span></span>
* <span data-ttu-id="7f1c5-174">Hello Azure Blob-service heeft geen een toodetermine betekent of twee blokken identieke gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-174">hello Azure Blob service does not have a means toodetermine whether two blocks contain identical data.</span></span> <span data-ttu-id="7f1c5-175">Elk blok dat wordt geüpload en doorgevoerd als uniek wordt behandeld, zelfs als deze heeft dezelfde gegevens en Hallo Hallo dezelfde ID. blokkeren</span><span class="sxs-lookup"><span data-stu-id="7f1c5-175">Each block that is uploaded and committed is treated as unique, even if it has hello same data and hello same block ID.</span></span> <span data-ttu-id="7f1c5-176">Omdat de kosten doorlopen voor unieke blokken, is het belangrijk tooconsider die voor het bijwerken van een blob met een momentopname in extra unieke blokken en extra kosten resulteert.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-176">Because charges accrue for unique blocks, it's important tooconsider that updating a blob that has a snapshot results in additional unique blocks and additional charges.</span></span>

### <a name="minimize-cost-with-snapshot-management"></a><span data-ttu-id="7f1c5-177">Kosten met beheer van momentopnamen beperken</span><span class="sxs-lookup"><span data-stu-id="7f1c5-177">Minimize cost with snapshot management</span></span>

<span data-ttu-id="7f1c5-178">Het is raadzaam het beheren van uw momentopnamen zorgvuldig tooavoid extra kosten.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-178">We recommend managing your snapshots carefully tooavoid extra charges.</span></span> <span data-ttu-id="7f1c5-179">U kunt deze best practices toohelp minimaliseren Hallo kosten van de opslag van uw momentopnamen Hallo volgen:</span><span class="sxs-lookup"><span data-stu-id="7f1c5-179">You can follow these best practices toohelp minimize hello costs incurred by hello storage of your snapshots:</span></span>

* <span data-ttu-id="7f1c5-180">Verwijderen en opnieuw maken van momentopnamen die zijn gekoppeld met een blob telkens wanneer u Hallo blob bijwerkt, zelfs als u met identieke gegevens bijwerken wilt tenzij ontwerp van uw toepassing vereist is voor het onderhouden van momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-180">Delete and re-create snapshots associated with a blob whenever you update hello blob, even if you are updating with identical data, unless your application design requires that you maintain snapshots.</span></span> <span data-ttu-id="7f1c5-181">Verwijderd en opnieuw maken van momentopnamen Hallo-blob, kunt u ervoor zorgen dat Hallo blob en momentopnamen niet luidsprekers.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-181">By deleting and re-creating hello blob's snapshots, you can ensure that hello blob and snapshots do not diverge.</span></span>
* <span data-ttu-id="7f1c5-182">Als u momentopnamen voor een blob en onderhoudt voorkomen dat de aanroepen [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], of [UploadFromByteArray] [ dotnet_UploadFromByteArray] tooupdate Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-182">If you are maintaining snapshots for a blob, avoid calling [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] tooupdate hello blob.</span></span> <span data-ttu-id="7f1c5-183">Deze methoden vervangen van alle Hallo-blokken in Hallo blob, waardoor uw base blob en het bijbehorende momentopnamen toodiverge aanzienlijk.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-183">These methods replace all of hello blocks in hello blob, causing your base blob and its snapshots toodiverge significantly.</span></span> <span data-ttu-id="7f1c5-184">In plaats daarvan update minst mogelijke aantal blokken met behulp van Hallo Hallo [PutBlock] [ dotnet_PutBlock] en [PutBlockList] [ dotnet_PutBlockList] methoden.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-184">Instead, update hello fewest possible number of blocks by using hello [PutBlock][dotnet_PutBlock] and [PutBlockList][dotnet_PutBlockList] methods.</span></span>

### <a name="snapshot-billing-scenarios"></a><span data-ttu-id="7f1c5-185">Momentopname facturering scenario 's</span><span class="sxs-lookup"><span data-stu-id="7f1c5-185">Snapshot billing scenarios</span></span>
<span data-ttu-id="7f1c5-186">Hallo volgen scenario's laten zien hoe de kosten voor een blok-blob en bijbehorende momentopnamen doorlopen.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-186">hello following scenarios demonstrate how charges accrue for a block blob and its snapshots.</span></span>

<span data-ttu-id="7f1c5-187">**Scenario 1**</span><span class="sxs-lookup"><span data-stu-id="7f1c5-187">**Scenario 1**</span></span>

<span data-ttu-id="7f1c5-188">In scenario 1 is Hallo base blob niet bijgewerkt nadat het Hallo-momentopname werd gemaakt, zodat de kosten verbonden zijn alleen voor unieke blokken 1, 2 en 3.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-188">In scenario 1, hello base blob has not been updated after hello snapshot was taken, so charges are incurred only for unique blocks 1, 2, and 3.</span></span>

![Azure Storage-resources](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

<span data-ttu-id="7f1c5-190">**Scenario 2**</span><span class="sxs-lookup"><span data-stu-id="7f1c5-190">**Scenario 2**</span></span>

<span data-ttu-id="7f1c5-191">In scenario 2 Hallo base blob is bijgewerkt, maar Hallo momentopname niet heeft.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-191">In scenario 2, hello base blob has been updated, but hello snapshot has not.</span></span> <span data-ttu-id="7f1c5-192">Blok 3 is bijgewerkt, en hoewel bevat dezelfde gegevens Hallo en dezelfde ID hello, is het Hallo niet hetzelfde als 3 in momentopname Hallo blokkeren.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-192">Block 3 was updated, and even though it contains hello same data and hello same ID, it is not hello same as block 3 in hello snapshot.</span></span> <span data-ttu-id="7f1c5-193">Als gevolg hiervan Hallo-account wordt in rekening gebracht voor vier blokken.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-193">As a result, hello account is charged for four blocks.</span></span>

![Azure Storage-resources](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

<span data-ttu-id="7f1c5-195">**Scenario 3**</span><span class="sxs-lookup"><span data-stu-id="7f1c5-195">**Scenario 3**</span></span>

<span data-ttu-id="7f1c5-196">In scenario 3 Hallo base blob is bijgewerkt, maar Hallo momentopname niet heeft.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-196">In scenario 3, hello base blob has been updated, but hello snapshot has not.</span></span> <span data-ttu-id="7f1c5-197">Blok 3 is vervangen door blok 4 in Hallo base blob, maar Hallo momentopname weerspiegelt nog steeds blok 3.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-197">Block 3 was replaced with block 4 in hello base blob, but hello snapshot still reflects block 3.</span></span> <span data-ttu-id="7f1c5-198">Als gevolg hiervan Hallo-account wordt in rekening gebracht voor vier blokken.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-198">As a result, hello account is charged for four blocks.</span></span>

![Azure Storage-resources](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

<span data-ttu-id="7f1c5-200">**Scenario 4**</span><span class="sxs-lookup"><span data-stu-id="7f1c5-200">**Scenario 4**</span></span>

<span data-ttu-id="7f1c5-201">In scenario 4 Hallo base blob volledig is bijgewerkt en geen van de oorspronkelijke blokken bevat.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-201">In scenario 4, hello base blob has been completely updated and contains none of its original blocks.</span></span> <span data-ttu-id="7f1c5-202">Als gevolg hiervan Hallo-account wordt in rekening gebracht voor alle acht unieke blokken.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-202">As a result, hello account is charged for all eight unique blocks.</span></span> <span data-ttu-id="7f1c5-203">Dit kan gebeuren als u een update-methode, zoals [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], of [UploadFromByteArray][dotnet_UploadFromByteArray], omdat deze methoden vervangen van alle inhoud van een blob Hallo.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-203">This scenario can occur if you are using an update method such as [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray], because these methods replace all of hello contents of a blob.</span></span>

![Azure Storage-resources](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a><span data-ttu-id="7f1c5-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7f1c5-205">Next steps</span></span>

* <span data-ttu-id="7f1c5-206">U vindt meer informatie over het werken met momentopnamen van virtuele machine (VM)-schijf in [Back-up van Azure niet-beheerde VM-schijven met incrementele momentopnamen](storage-incremental-snapshots.md)</span><span class="sxs-lookup"><span data-stu-id="7f1c5-206">You can find more information about working with virtual machine (VM) disk snapshots in [Back up Azure unmanaged VM disks with incremental snapshots](storage-incremental-snapshots.md)</span></span>

* <span data-ttu-id="7f1c5-207">Zie voor aanvullende codevoorbeelden met behulp van Blob-opslag, [Azure codevoorbeelden](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span><span class="sxs-lookup"><span data-stu-id="7f1c5-207">For additional code examples using Blob storage, see [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span></span> <span data-ttu-id="7f1c5-208">Een voorbeeld van een toepassing te downloaden en uitvoeren, of blader Hallo-code op GitHub.</span><span class="sxs-lookup"><span data-stu-id="7f1c5-208">You can download a sample application and run it, or browse hello code on GitHub.</span></span>

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