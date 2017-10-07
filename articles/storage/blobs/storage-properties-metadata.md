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
# <a name="set-and-retrieve-properties-and-metadata"></a><span data-ttu-id="85bf8-103">Eigenschappen en metagegevens instellen en ophalen</span><span class="sxs-lookup"><span data-stu-id="85bf8-103">Set and retrieve properties and metadata</span></span>

<span data-ttu-id="85bf8-104">Objecten in Azure Storage ondersteuning Systeemeigenschappen en de gebruiker gedefinieerde metagegevens bovendien toohello gegevens die ze bevatten.</span><span class="sxs-lookup"><span data-stu-id="85bf8-104">Objects in Azure Storage support system properties and user-defined metadata, in addition toohello data they contain.</span></span> <span data-ttu-id="85bf8-105">Dit artikel worden de eigenschappen van het beheren en de gebruiker gedefinieerde metagegevens Hello [Azure Storage-clientbibliotheek voor .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="85bf8-105">This article discusses managing system properties and user-defined metadata with hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span>

* <span data-ttu-id="85bf8-106">**Systeemeigenschappen**: Systeemeigenschappen op elke opslagresource bestaan.</span><span class="sxs-lookup"><span data-stu-id="85bf8-106">**System properties**: System properties exist on each storage resource.</span></span> <span data-ttu-id="85bf8-107">Enkele van deze kunnen worden gelezen of ingesteld, terwijl andere alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="85bf8-107">Some of them can be read or set, while others are read-only.</span></span> <span data-ttu-id="85bf8-108">Sommige eigenschappen overeen onder Hallo dekt, toocertain HTTP-headers.</span><span class="sxs-lookup"><span data-stu-id="85bf8-108">Under hello covers, some system properties correspond toocertain standard HTTP headers.</span></span> <span data-ttu-id="85bf8-109">Hello Azure storage-clientbibliotheek houdt deze voor u.</span><span class="sxs-lookup"><span data-stu-id="85bf8-109">hello Azure storage client library maintains these for you.</span></span>

* <span data-ttu-id="85bf8-110">**Gebruiker gedefinieerde metagegevens**: gebruiker gedefinieerde metagegevens zijn metagegevens die u op een bepaalde bron Hallo vorm van een naam / waarde-paar opgeeft.</span><span class="sxs-lookup"><span data-stu-id="85bf8-110">**User-defined metadata**: User-defined metadata is metadata that you specify on a given resource in hello form of a name-value pair.</span></span> <span data-ttu-id="85bf8-111">U kunt metagegevens toostore aanvullende waarden met een opslagresource gebruiken.</span><span class="sxs-lookup"><span data-stu-id="85bf8-111">You can use metadata toostore additional values with a storage resource.</span></span> <span data-ttu-id="85bf8-112">Deze aanvullende metagegevens-waarden zijn voor uw eigen doeleinden alleen en hebben geen invloed op de werking van Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="85bf8-112">These additional metadata values are for your own purposes only, and do not affect how hello resource behaves.</span></span>

<span data-ttu-id="85bf8-113">Bij het ophalen van eigenschap en metagegevens waarden voor een opslagresource is een proces.</span><span class="sxs-lookup"><span data-stu-id="85bf8-113">Retrieving property and metadata values for a storage resource is a two-step process.</span></span> <span data-ttu-id="85bf8-114">Voordat u deze waarden lezen kunt, u moet expliciet halen ze door de aanroepende Hallo **FetchAttributes** methode.</span><span class="sxs-lookup"><span data-stu-id="85bf8-114">Before you can read these values, you must explicitly fetch them by calling hello **FetchAttributes** method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="85bf8-115">Eigenschap en metagegevens waarden voor een opslagresource zijn niet gevuld tenzij u een van de Hallo aanroepen **FetchAttributes** methoden.</span><span class="sxs-lookup"><span data-stu-id="85bf8-115">Property and metadata values for a storage resource are not populated unless you call one of hello **FetchAttributes** methods.</span></span>
>
> <span data-ttu-id="85bf8-116">U ontvangt een `400 Bad Request` als een naam/waarde-paren niet-ASCII-tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="85bf8-116">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span></span> <span data-ttu-id="85bf8-117">Naam/waarde-paren metagegevens zijn geldig HTTP-headers, en dus tooall beperkingen voor HTTP-headers moet voldoen.</span><span class="sxs-lookup"><span data-stu-id="85bf8-117">Metadata name/value pairs are valid HTTP headers, and so must adhere tooall restrictions governing HTTP headers.</span></span> <span data-ttu-id="85bf8-118">Het is daarom raadzaam dat u URL-codering of Base64-codering voor namen en waarden die niet-ASCII-tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="85bf8-118">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span></span>
>

## <a name="setting-and-retrieving-properties"></a><span data-ttu-id="85bf8-119">Bijwerken en het ophalen van eigenschappen</span><span class="sxs-lookup"><span data-stu-id="85bf8-119">Setting and retrieving properties</span></span>
<span data-ttu-id="85bf8-120">tooretrieve eigenschapswaarden en aanroep Hallo **FetchAttributes** leest u de methode op uw blob-container toopopulate Hallo eigenschappen of Hallo waarden.</span><span class="sxs-lookup"><span data-stu-id="85bf8-120">tooretrieve property values, call hello **FetchAttributes** method on your blob or container toopopulate hello properties, then read hello values.</span></span>

<span data-ttu-id="85bf8-121">tooset eigenschappen op een object, geef Hallo eigenschapswaarde Roep vervolgens Hallo **SetProperties** methode.</span><span class="sxs-lookup"><span data-stu-id="85bf8-121">tooset properties on an object, specify hello property value, then call hello **SetProperties** method.</span></span>

<span data-ttu-id="85bf8-122">Hallo volgende codevoorbeeld maakt een container en schrijft enkele van de eigenschap waarden tooa-consolevenster.</span><span class="sxs-lookup"><span data-stu-id="85bf8-122">hello following code example creates a container, then writes some of its property values tooa console window.</span></span>

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

## <a name="setting-and-retrieving-metadata"></a><span data-ttu-id="85bf8-123">Instellen en ophalen van metagegevens</span><span class="sxs-lookup"><span data-stu-id="85bf8-123">Setting and retrieving metadata</span></span>
<span data-ttu-id="85bf8-124">U kunt metagegevens opgeven als een of meer naam / waarde-paren van een blob of container resource.</span><span class="sxs-lookup"><span data-stu-id="85bf8-124">You can specify metadata as one or more name-value pairs on a blob or container resource.</span></span> <span data-ttu-id="85bf8-125">tooset metagegevens, naam / waarde-paren toohello toevoegen **metagegevens** verzameling op Hallo resource, roept u vervolgens Hallo **SetMetadata** methode toosave Hallo waarden toohello service.</span><span class="sxs-lookup"><span data-stu-id="85bf8-125">tooset metadata, add name-value pairs toohello **Metadata** collection on hello resource, then call hello **SetMetadata** method toosave hello values toohello service.</span></span>

> [!NOTE]
> <span data-ttu-id="85bf8-126">Hallo-naam van de metagegevens moet toohello naamgevingsregels voor C#-id's voldoen.</span><span class="sxs-lookup"><span data-stu-id="85bf8-126">hello name of your metadata must conform toohello naming conventions for C# identifiers.</span></span>
>
>

<span data-ttu-id="85bf8-127">Hallo stelt volgende codevoorbeeld metagegevens in een container.</span><span class="sxs-lookup"><span data-stu-id="85bf8-127">hello following code example sets metadata on a container.</span></span> <span data-ttu-id="85bf8-128">Een waarde wordt ingesteld met behulp van een verzameling Hallo **toevoegen** methode.</span><span class="sxs-lookup"><span data-stu-id="85bf8-128">One value is set using hello collection's **Add** method.</span></span> <span data-ttu-id="85bf8-129">Hallo andere waarde wordt ingesteld met impliciete sleutel/waarde-syntaxis.</span><span class="sxs-lookup"><span data-stu-id="85bf8-129">hello other value is set using implicit key/value syntax.</span></span> <span data-ttu-id="85bf8-130">Beide zijn geldig.</span><span class="sxs-lookup"><span data-stu-id="85bf8-130">Both are valid.</span></span>

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

<span data-ttu-id="85bf8-131">tooretrieve metagegevens, aanroep Hallo **FetchAttributes** methode op uw toopopulate blob of container Hallo **metagegevens** verzameling, leest u Hallo waarden, zoals weergegeven in Hallo voorbeeld hieronder.</span><span class="sxs-lookup"><span data-stu-id="85bf8-131">tooretrieve metadata, call hello **FetchAttributes** method on your blob or container toopopulate hello **Metadata** collection, then read hello values, as shown in hello example below.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="85bf8-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="85bf8-132">Next steps</span></span>
* [<span data-ttu-id="85bf8-133">Azure Storage-clientbibliotheek voor .NET-verwijzing</span><span class="sxs-lookup"><span data-stu-id="85bf8-133">Azure Storage Client Library for .NET reference</span></span>](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [<span data-ttu-id="85bf8-134">Azure Storage-clientbibliotheek voor .NET-NuGet-pakket</span><span class="sxs-lookup"><span data-stu-id="85bf8-134">Azure Storage Client Library for .NET NuGet package</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
