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
ms.openlocfilehash: 0675b5dc4d32a3a0a34376ae4c049542b07ba03a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-anonymous-read-access-toocontainers-and-blobs"></a>Anonieme leestoegang toocontainers en blobs beheren
U kunt anonieme, openbare leestoegang tooa container en de blobs in Azure Blob-opslag inschakelen. Op deze manier kunt u alleen-lezentoegang toothese resources verlenen zonder het delen van de accountsleutel en zonder een shared access signature (SAS).

Openbare leestoegang wordt aanbevolen voor scenario's waar u wilt dat bepaalde blobs tooalways worden beschikbaar voor anonieme toegang voor lezen. Voor nauwkeuriger beheer, kunt u een shared access signature maken. Handtekeningen voor gedeelde toegang inschakelen tooprovide beperkt via toegang tot andere machtigingen voor een bepaalde periode. Voor meer informatie over het maken van gedeelde handtekeningen krijgen, Zie [Using shared access signatures (SAS) in Azure Storage](storage-dotnet-shared-access-signature-part-1.md).

## <a name="grant-anonymous-users-permissions-toocontainers-and-blobs"></a>Anonieme gebruikers machtigingen toocontainers en blobs verlenen
Standaard kunnen een container en alle bestaande blobs erin alleen worden geopend door Hallo eigenaar van Hallo storage-account. toogive anonieme gebruikers leesmachtigingen tooa container en de blobs, kunt u Hallo container machtigingen tooallow openbare toegang instellen. Anonieme gebruikers kunnen BLOB's binnen een container openbaar toegankelijk lezen zonder verificatie Hallo-aanvraag.

U kunt een container met de volgende machtigingen Hallo configureren:

* **Geen enkele openbare leestoegang:** Hallo-container en de blobs kunnen alleen worden geopend door Hallo eigenaar van het opslagaccount. Dit is de standaardinstelling Hallo voor alle nieuwe containers.
* **Openbare leestoegang voor blobs alleen:** Blobs in de container Hallo kunnen worden gelezen door anonieme aanvraag, maar de containergegevens is niet beschikbaar. Anonieme clients kunnen blobs in de container Hallo Hallo niet opsommen.
* **Volledige openbare leestoegang:** alle container en de blob-gegevens kunnen worden gelezen door anonieme aanvraag. Clients blobs in de container Hallo anonieme aanvraag kunnen opsommen, maar kunnen de containers in Hallo storage-account niet inventariseren.

U kunt de volgende tooset container machtigingen hello gebruiken:

* [Azure Portal](https://portal.azure.com)
* [Azure PowerShell](storage-powershell-guide-full.md#how-to-manage-azure-blobs)
* [Azure CLI 2.0](storage-azure-cli.md#create-and-manage-blobs)
* Programmatisch met behulp van een van de opslagclientbibliotheken Hallo of Hallo REST-API

### <a name="set-container-permissions-in-hello-azure-portal"></a>Container machtigingen instellen in hello Azure-portal
tooset container machtigingen in Hallo [Azure-portal](https://portal.azure.com), als volgt te werk:

1. Open uw **opslagaccount** blade in Hallo-portal. U kunt uw storage-account vinden door te selecteren **opslagaccounts** Hallo portal hoofdmenu blade.
1. Onder **BLOB-SERVICE** selecteren op Hallo menu blade **Containers**.
1. Met de rechtermuisknop op het Hallo-container rij of selecteer Hallo weglatingsteken tooopen Hallo van container **contextmenu**.
1. Selecteer **toegangsbeleid** in het contextmenu Hallo.
1. Selecteer een **toegangstype** van Hallo vervolgkeuzemenu.

    ![Dialoogvenster metagegevens bewerken](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a>Container machtigingen instellen met .NET
Hallo-container bestaande machtigingen tooset machtigingen voor een container met C# en Hallo Storage-clientbibliotheek voor .NET, eerst ophalen door de aanroepende Hallo **GetPermissions** methode. Vervolgens set Hallo **PublicAccess** eigenschap voor Hallo **BlobContainerPermissions** -object dat wordt geretourneerd door Hallo **GetPermissions** methode. Tenslotte roept Hallo **SetPermissions** methode Hello machtigingen bijgewerkt.

Hallo volgt stelt Hallo-container machtigingen toofull openbare leestoegang. tooset machtigingen toopublic leestoegang voor blobs ingesteld alleen Hallo **PublicAccess** eigenschap te**BlobContainerPublicAccessType.Blob**. tooremove alle machtigingen voor anonieme gebruikers instellen eigenschap te Hallo**BlobContainerPublicAccessType.Off**.

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a>Toegang tot containers en blobs anoniem
Een client die toegang heeft tot containers en blobs anoniem kan constructors waarvoor geen referenties gebruiken. Hallo volgen voorbeelden weergeven resources die een aantal verschillende manieren tooreference Blob-service anoniem.

### <a name="create-an-anonymous-client-object"></a>Een clientobject anonieme maken
Dankzij de Hallo eindpunt voor Blob-service voor Hallo account kunt u een nieuw serviceobject voor een client voor anonieme toegang. U moet echter ook Hallo-naam van een container in het account dat beschikbaar is voor anonieme toegang kennen.

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

### <a name="reference-a-container-anonymously"></a>Een container anoniem verwijst naar
Als er Hallo URL tooa container die anoniem beschikbaar is, kunt u deze tooreference Hallo container rechtstreeks.

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

### <a name="reference-a-blob-anonymously"></a>Een blob anoniem verwijst naar
Als u Hallo URL tooa blob die beschikbaar is voor anonieme toegang hebt, kunt u verwijzen naar Hallo blob die URL direct met:

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-tooanonymous-users"></a>Functies beschikbaar tooanonymous gebruikers
Hallo volgende tabel ziet u welke bewerkingen door anonieme gebruikers kunnen worden aangeroepen wanneer een container-ACL tooallow openbare toegang is ingesteld.

| REST-bewerking | Machtiging met volledige openbare leestoegang | Machtiging met openbare leestoegang voor blobs alleen |
| --- | --- | --- |
| Lijst Containers |Alleen de eigenaar |Alleen de eigenaar |
| Container maken |Alleen de eigenaar |Alleen de eigenaar |
| Eigenschappen van Container ophalen |Alle |Alleen de eigenaar |
| Container metagegevens ophalen |Alle |Alleen de eigenaar |
| Metagegevens van de Container instellen |Alleen de eigenaar |Alleen de eigenaar |
| Container-ACL ophalen |Alleen de eigenaar |Alleen de eigenaar |
| Container-ACL instellen |Alleen de eigenaar |Alleen de eigenaar |
| Verwijderen van Container |Alleen de eigenaar |Alleen de eigenaar |
| Lijst met BLOB 's |Alle |Alleen de eigenaar |
| Blob plaatsen |Alleen de eigenaar |Alleen de eigenaar |
| Ophalen van Blob |Alle |Alle |
| Blob-eigenschappen ophalen |Alle |Alle |
| Blob-eigenschappen instellen |Alleen de eigenaar |Alleen de eigenaar |
| Blobmetagegevens ophalen |Alle |Alle |
| Blobmetagegevens instellen |Alleen de eigenaar |Alleen de eigenaar |
| Blok plaatsen |Alleen de eigenaar |Alleen de eigenaar |
| Ophalen van lijst met geblokkeerde websites (alleen doorgevoerde blokken) |Alle |Alle |
| Ophalen van lijst met geblokkeerde websites (alleen niet-doorgevoerde blokken of alle blokken) |Alleen de eigenaar |Alleen de eigenaar |
| Lijst met geblokkeerde websites plaatsen |Alleen de eigenaar |Alleen de eigenaar |
| Verwijderen van Blob |Alleen de eigenaar |Alleen de eigenaar |
| Blob kopiëren |Alleen de eigenaar |Alleen de eigenaar |
| Momentopname Blob |Alleen de eigenaar |Alleen de eigenaar |
| Lease Blob |Alleen de eigenaar |Alleen de eigenaar |
| Pagina plaatsen |Alleen de eigenaar |Alleen de eigenaar |
| Get-paginabereiken |Alle |Alle |
| Toevoeg-Blob |Alleen de eigenaar |Alleen de eigenaar |

## <a name="next-steps"></a>Volgende stappen

* [Verificatie voor hello Azure Storage-Services](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [Met behulp van Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md)
* [Toegang delegeren met een Shared Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx)
