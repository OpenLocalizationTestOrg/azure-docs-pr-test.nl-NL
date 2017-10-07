---
title: aaaSet en ophalen van het object eigenschappen en metagegevens in Azure Storage | Microsoft Docs
description: Aangepaste metagegevens voor objecten in Azure Storage, opslaan en instelt en ophaalt Systeemeigenschappen.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 036f9006-273e-400b-844b-3329045e9e1f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 44f9243183014845964f337b476a6b0069dc0902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-and-retrieve-properties-and-metadata"></a>Eigenschappen en metagegevens instellen en ophalen

Objecten in Azure Storage ondersteuning Systeemeigenschappen en de gebruiker gedefinieerde metagegevens bovendien toohello gegevens die ze bevatten. Dit artikel worden de eigenschappen van het beheren en de gebruiker gedefinieerde metagegevens Hello [Azure Storage-clientbibliotheek voor .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).

* **Systeemeigenschappen**: Systeemeigenschappen op elke opslagresource bestaan. Enkele van deze kunnen worden gelezen of ingesteld, terwijl andere alleen-lezen. Sommige eigenschappen overeen onder Hallo dekt, toocertain HTTP-headers. Hello Azure storage-clientbibliotheek houdt deze voor u.

* **Gebruiker gedefinieerde metagegevens**: gebruiker gedefinieerde metagegevens zijn metagegevens die u op een bepaalde bron Hallo vorm van een naam / waarde-paar opgeeft. U kunt metagegevens toostore aanvullende waarden met een opslagresource gebruiken. Deze aanvullende metagegevens-waarden zijn voor uw eigen doeleinden alleen en hebben geen invloed op de werking van Hallo resource.

Bij het ophalen van eigenschap en metagegevens waarden voor een opslagresource is een proces. Voordat u deze waarden lezen kunt, u moet expliciet halen ze door de aanroepende Hallo **FetchAttributes** methode.

> [!IMPORTANT]
> Eigenschap en metagegevens waarden voor een opslagresource zijn niet gevuld tenzij u een van de Hallo aanroepen **FetchAttributes** methoden.
>
> U ontvangt een `400 Bad Request` als een naam/waarde-paren niet-ASCII-tekens bevatten. Naam/waarde-paren metagegevens zijn geldig HTTP-headers, en dus tooall beperkingen voor HTTP-headers moet voldoen. Het is daarom raadzaam dat u URL-codering of Base64-codering voor namen en waarden die niet-ASCII-tekens bevat.
>

## <a name="setting-and-retrieving-properties"></a>Bijwerken en het ophalen van eigenschappen
tooretrieve eigenschapswaarden en aanroep Hallo **FetchAttributes** leest u de methode op uw blob-container toopopulate Hallo eigenschappen of Hallo waarden.

tooset eigenschappen op een object, geef Hallo eigenschapswaarde Roep vervolgens Hallo **SetProperties** methode.

Hallo volgende codevoorbeeld maakt een container en schrijft enkele van de eigenschap waarden tooa-consolevenster.

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create hello service client object for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a>Instellen en ophalen van metagegevens
U kunt metagegevens opgeven als een of meer naam / waarde-paren van een blob of container resource. tooset metagegevens, naam / waarde-paren toohello toevoegen **metagegevens** verzameling op Hallo resource, roept u vervolgens Hallo **SetMetadata** methode toosave Hallo waarden toohello service.

> [!NOTE]
> Hallo-naam van de metagegevens moet toohello naamgevingsregels voor C#-id's voldoen.
>
>

Hallo stelt volgende codevoorbeeld metagegevens in een container. Een waarde wordt ingesteld met behulp van een verzameling Hallo **toevoegen** methode. Hallo andere waarde wordt ingesteld met impliciete sleutel/waarde-syntaxis. Beide zijn geldig.

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata toohello container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set hello container's metadata.
    container.SetMetadata();
}
```

tooretrieve metagegevens, aanroep Hallo **FetchAttributes** methode op uw toopopulate blob of container Hallo **metagegevens** verzameling, leest u Hallo waarden, zoals weergegeven in Hallo voorbeeld hieronder.

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order toopopulate hello container's properties and metadata.
    container.FetchAttributes();

    //Enumerate hello container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a>Volgende stappen
* [Azure Storage-clientbibliotheek voor .NET-verwijzing](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [Azure Storage-clientbibliotheek voor .NET-NuGet-pakket](https://www.nuget.org/packages/WindowsAzure.Storage/)
