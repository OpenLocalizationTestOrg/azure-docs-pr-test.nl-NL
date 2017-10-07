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
# <a name="create-a-blob-snapshot"></a>Een blob-momentopname maken

Een momentopname is een alleen-lezen-versie van een blob die wordt uitgevoerd op een punt in tijd. Momentopnamen zijn nuttig voor back-up blobs. Nadat u een momentopname gemaakt, lezen, kopiëren of verwijderen, maar u kunt dit niet wijzigen.

Een momentopname van een blob is identiek tooits base blob, behalve Hallo blob-URI bevat een **DateTime** waarde toegevoegd toohello blob-URI tooindicate Hallo moment op welke Hallo momentopname werd gemaakt. Bijvoorbeeld, als een pagina blob-URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, Hallo momentopname URI lijkt te`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.

> [!NOTE]
> Alle momentopnamen delen Hallo base blob-URI. alleen onderscheid tussen Hallo base blob en Hallo momentopname toegevoegd Hallo is Hallo **DateTime** waarde.
>

Een blob kan een onbeperkt aantal momentopnamen hebben. Momentopnamen bewaard totdat ze expliciet worden verwijderd. Een momentopname kan niet de base blob outlive. U kunt Hallo momentopnamen die zijn gekoppeld aan Hallo base blob tootrack opsommen uw huidige momentopnamen.

Bij het maken van een momentopname van een blob Hallo Systeemeigenschappen van blob zijn gekopieerde toohello momentopname Hello dezelfde waarden. Hallo base blob-metagegevens zijn ook gekopieerde toohello momentopname, tenzij u afzonderlijke metagegevens voor wanneer u deze maakt een momentopname Hallo opgeeft.

Alle leases die zijn gekoppeld aan basis blob Hallo hebben geen invloed op Hallo momentopname. U kunt een lease op een momentopname kan niet verkrijgen.

Een VHD-bestand is gebruikte toostore Hallo actuele informatie en status voor een VM-schijf. U kunt een schijf uit binnen Hallo VM loskoppelen of Hallo VM afsluiten en vervolgens een momentopname van de VHD-bestand. Kunt u dat momentopnamebestand hoger tooretrieve Hallo VHD-bestand op dat punt in tijd en maak deze opnieuw Hallo VM.

Als versleuteling voor opslag-Service (SSE) is ingeschakeld voor Hallo storage-account in welke Hallo blob zich bevindt en vervolgens alle momentopnamen van blob is genomen, worden versleuteld in rust.

## <a name="create-a-snapshot"></a>Een momentopname maken
Hallo volgende voorbeeldcode laat zien hoe een momentopname met behulp van toocreate Hallo [Azure Storage-clientbibliotheek voor .NET](https://www.nuget.org/packages/WindowsAzure.Storage/). In dit voorbeeld bevat aanvullende metagegevens voor Hallo momentopname wanneer deze wordt gemaakt.

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

## <a name="copy-snapshots"></a>Kopiëren van momentopnamen
Kopieerbewerkingen met betrekking tot de blobs en momentopnamen van voldoen deze regels:

* U kunt een momentopname via de base blob kopiëren. Door de positie van een momentopname toohello van Hallo base blob te promoveren, kunt u een eerdere versie van een blob herstellen. Hallo momentopname blijft, maar Hallo base blob wordt overschreven met een beschrijfbare kopie van Hallo momentopname.
* U kunt een momentopname tooa bestemmings-blob met een andere naam kopiëren. Hallo resulterende bestemmings-blob is een beschrijfbare blob en niet een momentopname.
* Als een bron-blob zijn gekopieerd, zijn de momentopnamen van de bron-blob Hallo niet gekopieerde toohello bestemming. Wanneer een bestemmings-blob is overschreven door een exemplaar, zijn de momentopnamen die zijn gekoppeld aan de oorspronkelijke bestemmings-blob Hallo blijven behouden.
* Bij het maken van een momentopname van een blok-blob is doorgevoerd Hallo-blob-blokkeringslijst ook gekopieerde toohello momentopname. Een niet-doorgevoerde blokken worden niet gekopieerd.

## <a name="specify-an-access-condition"></a>Geef een voorwaarde voor toegang
Als u aanroept [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], kunt u een voorwaarde voor toegang opgeven zodat hello momentopname alleen gemaakt wordt als een voorwaarde wordt voldaan. toospecify een voorwaarde voor toegang, gebruik Hallo [AccessCondition] [ dotnet_AccessCondition] parameter. Als Hallo opgegeven niet aan de voorwaarde is voldaan, Hallo momentopname is niet gemaakt en Hallo Blob-service retourneert statuscode [HTTPStatusCode][dotnet_HTTPStatusCode]. PreconditionFailed.

## <a name="delete-snapshots"></a>Verwijder momentopnamen
U kunt een blob met de momentopnamen niet verwijderen, tenzij Hallo momentopnamen worden ook verwijderd. U kunt een momentopname van een afzonderlijk verwijderen of u kunt opgeven dat alle momentopnamen worden verwijderd wanneer de bron-blob hello wordt verwijderd. Als u een blob die nog steeds momentopnamen toodelete probeert, wordt er een fout resulteert.

Hallo van de volgende code voorbeeld ziet u hoe toodelete een blob en bijbehorende momentopnamen in .NET waar `blockBlob` is een object van het type [CloudBlockBlob][dotnet_CloudBlockBlob]:

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a>Momentopnamen met Azure Premium-opslag
Als u momentopnamen met Premium-opslag, Hallo volgens de regels van toepassing:

* Hallo kunt u het maximum aantal momentopnamen per pagina-blob in een premium storage-account is 100. Als deze limiet wordt overschreden, Hallo momentopname Blob bewerking retourneert foutcode 409 (`SnapshotCountExceeded`).
* U kunt een momentopname van een pagina-blob nemen in een premium storage-account om de 10 minuten. Als dit percentage wordt overschreden, Hallo momentopname Blob bewerking retourneert foutcode 409 (`SnapshotOperationRateExceeded`).
* tooread een momentopname, kunt u Hallo Blob kopiëren bewerking toocopy een momentopname tooanother pagina-blob in Hallo-account. Hallo bestemmings-blob voor de kopieerbewerking Hallo mag geen eventuele bestaande momentopnamen. Als Hallo bestemmings-blob momentopnamen heeft, dan Hallo Blob kopiëren bewerking foutcode 409 retourneert (`SnapshotsPresent`).

## <a name="return-hello-absolute-uri-tooa-snapshot"></a>Hallo absolute URI tooa momentopname retourneren
In dit voorbeeld C#-code wordt een momentopname gemaakt en schrijft Hallo absolute URI voor de primaire locatie Hallo.

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

## <a name="understand-how-snapshots-accrue-charges"></a>Begrijpen hoe de kosten voor het samenvoegen van momentopnamen
Maken van een momentopname een alleen-lezen kopie van een blob is, kan leiden tot aanvullende gegevens storage kosten tooyour-account. Bij het ontwerpen van uw toepassing, is het belangrijk toobe weten hoe deze kosten doorlopen kunnen, zodat u de kosten kunt minimaliseren.

### <a name="important-billing-considerations"></a>Belangrijke overwegingen voor facturering
Hallo volgende lijst bevat belangrijke punten tooconsider bij het maken van een momentopname.

* Uw opslagaccount leidt ertoe dat de kosten voor unieke blokken of pagina's, ongeacht of deze in de blob Hallo of in momentopname Hallo. Uw account heeft geen gevolgen voor de extra kosten voor momentopnamen die zijn gekoppeld met een blob, totdat u bijwerkt Hallo blob waarop ze zijn gebaseerd. Na het bijwerken van Hallo base blob, wordt deze afwijkt van de momentopnamen. Als dit gebeurt, wordt u in rekening gebracht voor unieke Hallo-blokken of pagina's in elke blob of een momentopname.
* Wanneer u een blok binnen een blok-blob vervangt, dat blok wordt vervolgens in rekening gebracht als unieke blok. Dit geldt zelfs wanneer Hallo-blok heeft Hallo dezelfde ID blokkeren en Hallo dezelfde gegevens zoals deze in momentopname Hallo heeft. Nadat Hallo blok doorgevoerd is opnieuw het afwijkt van het bijbehorende equivalent in een momentopname en wordt u gefactureerd voor de gegevens. Hallo die dezelfde geldt voor een pagina in een pagina-blob bijgewerkt met identieke gegevens.
* Een blok-blob vervangen door de aanroepende Hallo [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream] [ dotnet_UploadFromStream], of [UploadFromByteArray] [ dotnet_UploadFromByteArray] vervangt alle blokken in Hallo blob-methode. Als er een momentopname die is gekoppeld aan blob, alle blokken in Hallo base blob en momentopname nu luidsprekers en wordt u gefactureerd voor alle Hallo gegevensblokken die zich in beide blobs. Dit geldt zelfs als het Hallo-gegevens in Hallo base blob en het Hallo-momentopname blijven identiek zijn.
* Hello Azure Blob-service heeft geen een toodetermine betekent of twee blokken identieke gegevens bevatten. Elk blok dat wordt geüpload en doorgevoerd als uniek wordt behandeld, zelfs als deze heeft dezelfde gegevens en Hallo Hallo dezelfde ID. blokkeren Omdat de kosten doorlopen voor unieke blokken, is het belangrijk tooconsider die voor het bijwerken van een blob met een momentopname in extra unieke blokken en extra kosten resulteert.

### <a name="minimize-cost-with-snapshot-management"></a>Kosten met beheer van momentopnamen beperken

Het is raadzaam het beheren van uw momentopnamen zorgvuldig tooavoid extra kosten. U kunt deze best practices toohelp minimaliseren Hallo kosten van de opslag van uw momentopnamen Hallo volgen:

* Verwijderen en opnieuw maken van momentopnamen die zijn gekoppeld met een blob telkens wanneer u Hallo blob bijwerkt, zelfs als u met identieke gegevens bijwerken wilt tenzij ontwerp van uw toepassing vereist is voor het onderhouden van momentopnamen. Verwijderd en opnieuw maken van momentopnamen Hallo-blob, kunt u ervoor zorgen dat Hallo blob en momentopnamen niet luidsprekers.
* Als u momentopnamen voor een blob en onderhoudt voorkomen dat de aanroepen [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], of [UploadFromByteArray] [ dotnet_UploadFromByteArray] tooupdate Hallo blob. Deze methoden vervangen van alle Hallo-blokken in Hallo blob, waardoor uw base blob en het bijbehorende momentopnamen toodiverge aanzienlijk. In plaats daarvan update minst mogelijke aantal blokken met behulp van Hallo Hallo [PutBlock] [ dotnet_PutBlock] en [PutBlockList] [ dotnet_PutBlockList] methoden.

### <a name="snapshot-billing-scenarios"></a>Momentopname facturering scenario 's
Hallo volgen scenario's laten zien hoe de kosten voor een blok-blob en bijbehorende momentopnamen doorlopen.

**Scenario 1**

In scenario 1 is Hallo base blob niet bijgewerkt nadat het Hallo-momentopname werd gemaakt, zodat de kosten verbonden zijn alleen voor unieke blokken 1, 2 en 3.

![Azure Storage-resources](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

**Scenario 2**

In scenario 2 Hallo base blob is bijgewerkt, maar Hallo momentopname niet heeft. Blok 3 is bijgewerkt, en hoewel bevat dezelfde gegevens Hallo en dezelfde ID hello, is het Hallo niet hetzelfde als 3 in momentopname Hallo blokkeren. Als gevolg hiervan Hallo-account wordt in rekening gebracht voor vier blokken.

![Azure Storage-resources](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

**Scenario 3**

In scenario 3 Hallo base blob is bijgewerkt, maar Hallo momentopname niet heeft. Blok 3 is vervangen door blok 4 in Hallo base blob, maar Hallo momentopname weerspiegelt nog steeds blok 3. Als gevolg hiervan Hallo-account wordt in rekening gebracht voor vier blokken.

![Azure Storage-resources](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

**Scenario 4**

In scenario 4 Hallo base blob volledig is bijgewerkt en geen van de oorspronkelijke blokken bevat. Als gevolg hiervan Hallo-account wordt in rekening gebracht voor alle acht unieke blokken. Dit kan gebeuren als u een update-methode, zoals [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], of [UploadFromByteArray][dotnet_UploadFromByteArray], omdat deze methoden vervangen van alle inhoud van een blob Hallo.

![Azure Storage-resources](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a>Volgende stappen

* U vindt meer informatie over het werken met momentopnamen van virtuele machine (VM)-schijf in [Back-up van Azure niet-beheerde VM-schijven met incrementele momentopnamen](storage-incremental-snapshots.md)

* Zie voor aanvullende codevoorbeelden met behulp van Blob-opslag, [Azure codevoorbeelden](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob). Een voorbeeld van een toepassing te downloaden en uitvoeren, of blader Hallo-code op GitHub.

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