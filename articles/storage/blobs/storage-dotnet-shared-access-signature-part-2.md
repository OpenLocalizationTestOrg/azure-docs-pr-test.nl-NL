---
title: aaaCreate en een shared access signature (SAS) gebruiken met Azure Blob storage | Microsoft Docs
description: Deze zelfstudie leert u hoe toocreate shared access signatures voor gebruik met Blob storage en hoe tooconsume ze in uw clienttoepassingen.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 491e0b3c-76d4-4149-9a80-bbbd683b1f3e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 32004d7d29a190a7ed7234513428c3c156b833b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a><span data-ttu-id="a834c-103">Shared Access Signatures, deel 2: Maken en gebruiken van een SAS met Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="a834c-103">Shared Access Signatures, Part 2: Create and use a SAS with Blob storage</span></span>

<span data-ttu-id="a834c-104">[Deel 1](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) shared access signatures (SAS) van deze zelfstudie verkend en aanbevolen procedures voor het gebruik ervan beschreven.</span><span class="sxs-lookup"><span data-stu-id="a834c-104">[Part 1](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) of this tutorial explored shared access signatures (SAS) and explained best practices for using them.</span></span> <span data-ttu-id="a834c-105">Deel 2 ziet u hoe toogenerate en gebruik vervolgens toegang gedeeld handtekeningen met Blob storage.</span><span class="sxs-lookup"><span data-stu-id="a834c-105">Part 2 shows you how toogenerate and then use shared access signatures with Blob storage.</span></span> <span data-ttu-id="a834c-106">Hallo-voorbeelden zijn geschreven in C# en gebruiken van hello Azure Storage-clientbibliotheek voor .NET.</span><span class="sxs-lookup"><span data-stu-id="a834c-106">hello examples are written in C# and use hello Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="a834c-107">Hallo-voorbeelden in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="a834c-107">hello examples in this tutorial:</span></span>

* <span data-ttu-id="a834c-108">Een shared access signature in een container genereren</span><span class="sxs-lookup"><span data-stu-id="a834c-108">Generate a shared access signature on a container</span></span>
* <span data-ttu-id="a834c-109">Een shared access signature op een blob genereren</span><span class="sxs-lookup"><span data-stu-id="a834c-109">Generate a shared access signature on a blob</span></span>
* <span data-ttu-id="a834c-110">Een opgeslagen toegang beleid toomanage handtekeningen maken op een container bronnen</span><span class="sxs-lookup"><span data-stu-id="a834c-110">Create a stored access policy toomanage signatures on a container's resources</span></span>
* <span data-ttu-id="a834c-111">Handtekeningen voor gedeelde Hallo toegang testen in een clienttoepassing</span><span class="sxs-lookup"><span data-stu-id="a834c-111">Test hello shared access signatures in a client application</span></span>

## <a name="about-this-tutorial"></a><span data-ttu-id="a834c-112">Over deze zelfstudie</span><span class="sxs-lookup"><span data-stu-id="a834c-112">About this tutorial</span></span>
<span data-ttu-id="a834c-113">In deze zelfstudie maken we twee consoletoepassingen die laten zien maken en gebruiken van handtekeningen voor gedeelde toegang voor containers en blobs:</span><span class="sxs-lookup"><span data-stu-id="a834c-113">In this tutorial, we create two console applications that demonstrate creating and using shared access signatures for containers and blobs:</span></span>

<span data-ttu-id="a834c-114">**1 toepassing**: Hallo management-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a834c-114">**Application 1**: hello management application.</span></span> <span data-ttu-id="a834c-115">Genereert een shared access signature voor een container en een blob.</span><span class="sxs-lookup"><span data-stu-id="a834c-115">Generates a shared access signature for a container and a blob.</span></span> <span data-ttu-id="a834c-116">Hallo toegangssleutel voor opslagaccount bevat in de broncode.</span><span class="sxs-lookup"><span data-stu-id="a834c-116">Includes hello storage account access key in source code.</span></span>

<span data-ttu-id="a834c-117">**Toepassing 2**: Hallo van client-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a834c-117">**Application 2**: hello client application.</span></span> <span data-ttu-id="a834c-118">Toegang tot een container en blob bronnen gebruiken van handtekeningen van Hallo gedeelde toegang gemaakt met de eerste toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="a834c-118">Accesses container and blob resources using hello shared access signatures created with hello first application.</span></span> <span data-ttu-id="a834c-119">Maakt gebruik van alleen Hallo gedeelde toegang handtekeningen tooaccess container en resources van de blob--biedt *niet* Hallo toegangssleutel voor opslagaccount bevatten.</span><span class="sxs-lookup"><span data-stu-id="a834c-119">Uses only hello shared access signatures tooaccess container and blob resources--it does *not* include hello storage account access key.</span></span>

## <a name="part-1-create-a-console-application-toogenerate-shared-access-signatures"></a><span data-ttu-id="a834c-120">Deel 1: Een toogenerate gedeelde toegang tot de console application handtekeningen maken</span><span class="sxs-lookup"><span data-stu-id="a834c-120">Part 1: Create a console application toogenerate shared access signatures</span></span>
<span data-ttu-id="a834c-121">Eerst voor zorgen dat er hello Azure Storage-clientbibliotheek voor .NET is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a834c-121">First, ensure that you have hello Azure Storage Client Library for .NET installed.</span></span> <span data-ttu-id="a834c-122">U kunt installeren Hallo [NuGet-pakket](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet-pakket") met Hallo meest recente assembly's voor Hallo-clientbibliotheek.</span><span class="sxs-lookup"><span data-stu-id="a834c-122">You can install hello [NuGet package](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet package") containing hello most up-to-date assemblies for hello client library.</span></span> <span data-ttu-id="a834c-123">Dit is de aanbevolen methode om ervoor te zorgen dat u de meest recente oplossingen Hallo hebt Hallo.</span><span class="sxs-lookup"><span data-stu-id="a834c-123">This is hello recommended method for ensuring that you have hello most recent fixes.</span></span> <span data-ttu-id="a834c-124">U kunt ook de clientbibliotheek Hallo downloaden als onderdeel van de meest recente versie Hallo Hallo [Azure SDK voor .NET](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a834c-124">You can also download hello client library as part of hello most recent version of hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/).</span></span>

<span data-ttu-id="a834c-125">Maak een nieuwe Windows-consoletoepassing in Visual Studio en noem deze **GenerateSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="a834c-125">In Visual Studio, create a new Windows console application and name it **GenerateSharedAccessSignatures**.</span></span> <span data-ttu-id="a834c-126">Voeg verwijzingen te[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) en [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) met behulp van een Hallo benaderingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a834c-126">Add references too[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) by using one of hello following approaches:</span></span>

* <span data-ttu-id="a834c-127">Gebruik Hallo [NuGet-Pakketbeheer](https://docs.nuget.org/consume/installing-nuget) in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a834c-127">Use hello [NuGet package manager](https://docs.nuget.org/consume/installing-nuget) in Visual Studio.</span></span> <span data-ttu-id="a834c-128">Selecteer **Project** > **NuGet-pakketten beheren**, online zoeken naar elk pakket (Microsoft.WindowsAzure.ConfigurationManager en WindowsAzure.Storage) en deze installeren.</span><span class="sxs-lookup"><span data-stu-id="a834c-128">Select **Project** > **Manage NuGet Packages**, search online for each package (Microsoft.WindowsAzure.ConfigurationManager and WindowsAzure.Storage) and install them.</span></span>
* <span data-ttu-id="a834c-129">U kunt ook deze assembly's in uw installatie van hello Azure SDK en verwijzingen toothem toevoegen:</span><span class="sxs-lookup"><span data-stu-id="a834c-129">Alternatively, locate these assemblies in your installation of hello Azure SDK and add references toothem:</span></span>
  * <span data-ttu-id="a834c-130">Microsoft.WindowsAzure.Configuration.dll</span><span class="sxs-lookup"><span data-stu-id="a834c-130">Microsoft.WindowsAzure.Configuration.dll</span></span>
  * <span data-ttu-id="a834c-131">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="a834c-131">Microsoft.WindowsAzure.Storage.dll</span></span>

<span data-ttu-id="a834c-132">Aan de bovenkant van de Hallo van het bestand Program.cs hello, voeg Hallo volgende **met** richtlijnen:</span><span class="sxs-lookup"><span data-stu-id="a834c-132">At hello top of hello Program.cs file, add hello following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="a834c-133">Hallo app.config-bestand bewerken zodat deze een configuratie-instelling met een verbindingsreeks die tooyour opslagaccount wijst bevat.</span><span class="sxs-lookup"><span data-stu-id="a834c-133">Edit hello app.config file so that it contains a configuration setting with a connection string that points tooyour storage account.</span></span> <span data-ttu-id="a834c-134">Het bestand app.config ziet vergelijkbare toothis een:</span><span class="sxs-lookup"><span data-stu-id="a834c-134">Your app.config file should look similar toothis one:</span></span>

```xml
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
  </startup>
  <appSettings>
    <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey"/>
  </appSettings>
</configuration>
```

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a><span data-ttu-id="a834c-135">Een shared access signature URI voor een container genereren</span><span class="sxs-lookup"><span data-stu-id="a834c-135">Generate a shared access signature URI for a container</span></span>
<span data-ttu-id="a834c-136">toobegin met we een toogenerate methode een shared access signature voor een nieuwe container toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a834c-136">toobegin with, we add a method toogenerate a shared access signature on a new container.</span></span> <span data-ttu-id="a834c-137">In dit geval Hallo handtekening is niet gekoppeld aan een opgeslagen-beleid, zodat zij werkzaam Hallo URI Hallo informatie geeft de verloopdatum tijd en Hallo machtigingen verleent.</span><span class="sxs-lookup"><span data-stu-id="a834c-137">In this case, hello signature is not associated with a stored access policy, so it carries on hello URI hello information indicating its expiry time and hello permissions it grants.</span></span>

<span data-ttu-id="a834c-138">Voeg eerst code toohello **Main()** methode tooauthenticate tooyour storage-account openen en een nieuwe container maken:</span><span class="sxs-lookup"><span data-stu-id="a834c-138">First, add code toohello **Main()** method tooauthenticate access tooyour storage account and create a new container:</span></span>

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Insert calls toohello methods created below here...

    //Require user input before closing hello console window.
    Console.ReadLine();
}
```

<span data-ttu-id="a834c-139">Vervolgens voegt u een methode die genereert Hallo shared access signature voor Hallo-container en Hallo handtekening URI geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="a834c-139">Next, add a method that generates hello shared access signature for hello container and returns hello signature URI:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
    //Set hello expiry time and permissions for hello container.
    //In this case no start time is specified, so hello shared access signature becomes valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="a834c-140">Toevoegen van de volgende regels onderin Hallo HALLO hallo **Main()** methode voordat Hallo aanroepen te**Console.ReadLine()**, toocall **GetContainerSasUri()** en schrijf Hallo handtekening URI toohello consolevenster:</span><span class="sxs-lookup"><span data-stu-id="a834c-140">Add hello following lines at hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, toocall **GetContainerSasUri()** and write hello signature URI toohello console window:</span></span>

```csharp
//Generate a SAS URI for hello container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="a834c-141">Compileren en toooutput Hallo shared access signature URI voor de nieuwe container Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a834c-141">Compile and run toooutput hello shared access signature URI for hello new container.</span></span> <span data-ttu-id="a834c-142">Hallo URI zijn vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="a834c-142">hello URI will be similar toohello following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

<span data-ttu-id="a834c-143">Zodra u Hallo code hebt uitgevoerd, is Hallo shared access signature voor die u voor de container Hallo gemaakt geldig voor Hallo binnen 24 uur.</span><span class="sxs-lookup"><span data-stu-id="a834c-143">Once you have run hello code, hello shared access signature you created for hello container will be valid for hello next 24 hours.</span></span> <span data-ttu-id="a834c-144">Hallo handtekening verleent een client machtiging toolist blobs in Hallo-container en toowrite nieuwe blobs toohello container.</span><span class="sxs-lookup"><span data-stu-id="a834c-144">hello signature grants a client permission toolist blobs in hello container and toowrite new blobs toohello container.</span></span>

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a><span data-ttu-id="a834c-145">Een shared access signature URI voor een blob genereren</span><span class="sxs-lookup"><span data-stu-id="a834c-145">Generate a shared access signature URI for a blob</span></span>
<span data-ttu-id="a834c-146">Vervolgens we schrijven vergelijkbare code toocreate een nieuwe blob in Hallo-container en een shared access signature voor het genereren.</span><span class="sxs-lookup"><span data-stu-id="a834c-146">Next, we write similar code toocreate a new blob within hello container and generate a shared access signature for it.</span></span> <span data-ttu-id="a834c-147">Deze shared access signature is niet gekoppeld aan een opgeslagen-beleid, zodat deze functie Hallo begintijd, verlooptijd en toestemming informatie Hallo URI bevat.</span><span class="sxs-lookup"><span data-stu-id="a834c-147">This shared access signature is not associated with a stored access policy, so it includes hello start time, expiry time, and permission information in hello URI.</span></span>

<span data-ttu-id="a834c-148">Voeg een nieuwe methode die u maakt een nieuwe blob en sommige tooit tekst schrijft vervolgens genereert een shared access signature en Hallo handtekening URI geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="a834c-148">Add a new method that creates a new blob and writes some text tooit, then generates a shared access signature and returns hello signature URI:</span></span>

```csharp
static string GetBlobSasUri(CloudBlobContainer container)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblob.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature (SAS).";
    blob.UploadText(blobContent);

    //Set hello expiry time and permissions for hello blob.
    //In this case, hello start time is specified as a few minutes in hello past, toomitigate clock skew.
    //hello shared access signature will be valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessStartTime = DateTimeOffset.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="a834c-149">Hallo Hallo onderaan in **Main()** methode toevoegen van de volgende regels toocall Hallo **GetBlobSasUri()**, voordat Hallo aanroepen te**Console.ReadLine()**, en schrijf Hallo gedeeld toegang handtekening URI toohello consolevenster:</span><span class="sxs-lookup"><span data-stu-id="a834c-149">At hello bottom of hello **Main()** method, add hello following lines toocall **GetBlobSasUri()**, before hello call too**Console.ReadLine()**, and write hello shared access signature URI toohello console window:</span></span>

```csharp
//Generate a SAS URI for a blob within hello container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="a834c-150">Compileren en toooutput Hallo shared access signature URI voor de nieuwe blob Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a834c-150">Compile and run toooutput hello shared access signature URI for hello new blob.</span></span> <span data-ttu-id="a834c-151">Hallo URI zijn vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="a834c-151">hello URI will be similar toohello following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-hello-container"></a><span data-ttu-id="a834c-152">Een opgeslagen toegangsbeleid maken op Hallo-container</span><span class="sxs-lookup"><span data-stu-id="a834c-152">Create a stored access policy on hello container</span></span>
<span data-ttu-id="a834c-153">Nu gaan we een opgeslagen toegangsbeleid maken op Hallo-container die definieert Hallo beperkingen voor alle handtekeningen voor gedeelde toegang die gekoppeld zijn.</span><span class="sxs-lookup"><span data-stu-id="a834c-153">Now let's create a stored access policy on hello container, which will define hello constraints for any shared access signatures that are associated with it.</span></span>

<span data-ttu-id="a834c-154">In de voorgaande voorbeelden hello, we Hallo begintijd opgegeven (impliciet of expliciet), Hallo verlooptijd en machtigingen op Hallo Hallo gedeeld access signature voor URI zelf.</span><span class="sxs-lookup"><span data-stu-id="a834c-154">In hello previous examples, we specified hello start time (implicitly or explicitly), hello expiry time, and hello permissions on hello shared access signature URI itself.</span></span> <span data-ttu-id="a834c-155">In de Hallo volgen voorbeelden, geef deze op Hallo opgeslagen toegangsbeleid en niet op Hallo shared access signature voor.</span><span class="sxs-lookup"><span data-stu-id="a834c-155">In hello following examples, we specify these on hello stored access policy, not on hello shared access signature.</span></span> <span data-ttu-id="a834c-156">In dat geval schakelt doen ons toochange deze beperkingen zonder opnieuw uitgeven van Hallo gedeelde toegang tot handtekening.</span><span class="sxs-lookup"><span data-stu-id="a834c-156">Doing so enables us toochange these constraints without reissuing hello shared access signature.</span></span>

<span data-ttu-id="a834c-157">Het is mogelijk toohave een of meer Hallo beperkingen voor shared access signature voor Hallo en Hallo-rest van het toegangsbeleid Hallo opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a834c-157">It's possible toohave one or more of hello constraints on hello shared access signature, and hello remainder on hello stored access policy.</span></span> <span data-ttu-id="a834c-158">U kunt de begintijd hello, verlooptijd en machtigingen alleen opgeven in een plaats of Hallo andere.</span><span class="sxs-lookup"><span data-stu-id="a834c-158">However, you can only specify hello start time, expiry time, and permissions in one place or hello other.</span></span> <span data-ttu-id="a834c-159">U kan bijvoorbeeld machtigingen opgeven op Hallo shared access signature voor en geef ze ook op Hallo opgeslagen toegangsbeleid.</span><span class="sxs-lookup"><span data-stu-id="a834c-159">For example, you can't specify permissions on hello shared access signature and also specify them on hello stored access policy.</span></span>

<span data-ttu-id="a834c-160">Wanneer u een opgeslagen toegang beleid tooa container toevoegt, moet u bestaande machtigingen van de container Hallo ophalen, Hallo nieuwe toegangsbeleid toevoegen en vervolgens Hallo-container machtigingen instellen.</span><span class="sxs-lookup"><span data-stu-id="a834c-160">When you add a stored access policy tooa container, you must get hello container's existing permissions, add hello new access policy, and then set hello container's permissions.</span></span>

<span data-ttu-id="a834c-161">Voeg een nieuwe methode die een nieuw opgeslagen-beleid maakt in een container en retourneert Hallo-naam van het Hallo-beleid:</span><span class="sxs-lookup"><span data-stu-id="a834c-161">Add a new method that creates a new stored access policy on a container and returns hello name of hello policy:</span></span>

```csharp
static void CreateSharedAccessPolicy(CloudBlobClient blobClient, CloudBlobContainer container,
    string policyName)
{
    //Get hello container's existing permissions.
    BlobContainerPermissions permissions = container.GetPermissions();

    //Create a new shared access policy and define its constraints.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Read
    };

    //Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    container.SetPermissions(permissions);
}
```

<span data-ttu-id="a834c-162">Hallo Hallo onderaan in **Main()** methode voordat Hallo aanroepen te**Console.ReadLine()**, Hallo volgende regels toofirst Wis alle bestaande beleidsregels voor toegang toevoegen en vervolgens aanroepen Hallo  **CreateSharedAccessPolicy()** methode:</span><span class="sxs-lookup"><span data-stu-id="a834c-162">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toofirst clear any existing access policies, and then call hello **CreateSharedAccessPolicy()** method:</span></span>

```csharp
//Clear any existing access policies on container.
BlobContainerPermissions perms = container.GetPermissions();
perms.SharedAccessPolicies.Clear();
container.SetPermissions(perms);

//Create a new access policy on hello container, which may be optionally used tooprovide constraints for
//shared access signatures on hello container and hello blob.
string sharedAccessPolicyName = "tutorialpolicy";
CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);
```

<span data-ttu-id="a834c-163">Wanneer u Hallo-beleid in een container uitschakelt, moet u eerst ophalen van de container Hallo bestaande machtigingen en klik vervolgens wissen Hallo machtigingen vervolgens Hallo machtigingen opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="a834c-163">When you clear hello access policies on a container, you must first get hello container's existing permissions, then clear hello permissions, then set hello permissions again.</span></span>

### <a name="generate-a-shared-access-signature-uri-on-hello-container-that-uses-an-access-policy"></a><span data-ttu-id="a834c-164">Een shared access signature-URI op Hallo-container die gebruikmaakt van een toegangsbeleid genereren</span><span class="sxs-lookup"><span data-stu-id="a834c-164">Generate a shared access signature URI on hello container that uses an access policy</span></span>
<span data-ttu-id="a834c-165">Vervolgens maken we een andere shared access signature voor Hallo-container die we eerder hebben gemaakt, maar nu we Hallo handtekening koppelen aan toegangsbeleid Hallo opgeslagen die in het vorige voorbeeld Hallo is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a834c-165">Next, we create another shared access signature for hello container that we created earlier, but this time we associate hello signature with hello stored access policy we created in hello previous example.</span></span>

<span data-ttu-id="a834c-166">Een nieuwe methode toogenerate een andere shared access signature voor Hallo-container toevoegen:</span><span class="sxs-lookup"><span data-stu-id="a834c-166">Add a new method toogenerate another shared access signature for hello container:</span></span>

```csharp
static string GetContainerSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Generate hello shared access signature on hello container. In this case, all of hello constraints for the
    //shared access signature are specified on hello stored access policy.
    string sasContainerToken = container.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="a834c-167">Hallo Hallo onderaan in **Main()** methode voordat Hallo aanroepen te**Console.ReadLine()**, toevoegen van de volgende regels toocall Hallo Hallo **GetContainerSasUriWithPolicy** methode :</span><span class="sxs-lookup"><span data-stu-id="a834c-167">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toocall hello **GetContainerSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-hello-blob-that-uses-an-access-policy"></a><span data-ttu-id="a834c-168">Genereren van een gedeelde toegang handtekening-URI op Hallo Blob dat gebruikmaakt van een toegangsbeleid</span><span class="sxs-lookup"><span data-stu-id="a834c-168">Generate a Shared Access Signature URI on hello Blob That Uses an Access Policy</span></span>
<span data-ttu-id="a834c-169">Ten slotte we een vergelijkbare methode toocreate een andere blob toevoegen en een shared access signature die is gekoppeld aan een opgeslagen toegangsbeleid genereren.</span><span class="sxs-lookup"><span data-stu-id="a834c-169">Finally, we add a similar method toocreate another blob and generate a shared access signature that's associated with a stored access policy.</span></span>

<span data-ttu-id="a834c-170">Voeg een nieuwe methode toocreate een blob en een shared access signature genereren:</span><span class="sxs-lookup"><span data-stu-id="a834c-170">Add a new method toocreate a blob and generate a shared access signature:</span></span>

```csharp
static string GetBlobSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblobpolicy.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature. " +
    "A stored access policy defines hello constraints for hello signature.";
    MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    ms.Position = 0;
    using (ms)
    {
        blob.UploadFromStream(ms);
    }

    //Generate hello shared access signature on hello blob.
    string sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="a834c-171">Hallo Hallo onderaan in **Main()** methode voordat Hallo aanroepen te**Console.ReadLine()**, toevoegen van de volgende regels toocall Hallo Hallo **GetBlobSasUriWithPolicy** methode:</span><span class="sxs-lookup"><span data-stu-id="a834c-171">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toocall hello **GetBlobSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

<span data-ttu-id="a834c-172">Hallo **Main()** methode ziet er nu als volgt in zijn geheel.</span><span class="sxs-lookup"><span data-stu-id="a834c-172">hello **Main()** method should now look like this in its entirety.</span></span> <span data-ttu-id="a834c-173">Deze shared access signature toohello consolevenster URI's voor toowrite Hallo uitvoeren Kopieer en plak ze in een tekstbestand voor gebruik in Hallo tweede deel van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a834c-173">Run it toowrite hello shared access signature URIs toohello console window, then copy and paste them into a text file for use in hello second part of this tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Generate a SAS URI for hello container, without a stored access policy.
    Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, without a stored access policy.
    Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
    Console.WriteLine();

    //Clear any existing access policies on container.
    BlobContainerPermissions perms = container.GetPermissions();
    perms.SharedAccessPolicies.Clear();
    container.SetPermissions(perms);

    //Create a new access policy on hello container, which may be optionally used tooprovide constraints for
    //shared access signatures on hello container and hello blob.
    string sharedAccessPolicyName = "tutorialpolicy";
    CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);

    //Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    Console.ReadLine();
}
```

<span data-ttu-id="a834c-174">Wanneer u Hallo GenerateSharedAccessSignatures consoletoepassing uitvoert, ziet u uitvoer vergelijkbare toohello volgende.</span><span class="sxs-lookup"><span data-stu-id="a834c-174">When you run hello GenerateSharedAccessSignatures console application, you'll see output similar toohello following.</span></span> <span data-ttu-id="a834c-175">Dit zijn de handtekeningen voor gedeelde Hallo toegang die u in deel 2 van de zelfstudie hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a834c-175">These are hello shared access signatures you use in Part 2 of hello tutorial.</span></span>

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-tootest-hello-shared-access-signatures"></a><span data-ttu-id="a834c-176">Deel 2: Een toegang tot de console application tootest Hallo gedeelde handtekeningen maken</span><span class="sxs-lookup"><span data-stu-id="a834c-176">Part 2: Create a console application tootest hello shared access signatures</span></span>
<span data-ttu-id="a834c-177">Hallo tootest gedeelde toegang handtekeningen die zijn gemaakt in de voorgaande voorbeelden hello, maken we een tweede consoletoepassing die gebruikmaakt van Hallo handtekeningen tooperform bewerkingen op Hallo-container en op een blob.</span><span class="sxs-lookup"><span data-stu-id="a834c-177">tootest hello shared access signatures created in hello previous examples, we create a second console application that uses hello signatures tooperform operations on hello container and on a blob.</span></span>

> [!NOTE]
> <span data-ttu-id="a834c-178">Als meer dan 24 uur zijn verstreken sinds u Hallo eerste deel van Hallo-zelfstudie hebt voltooid, is Hallo handtekeningen die u hebt gegenereerd niet langer geldig.</span><span class="sxs-lookup"><span data-stu-id="a834c-178">If more than 24 hours have passed since you completed hello first part of hello tutorial, hello signatures you generated will no longer be valid.</span></span> <span data-ttu-id="a834c-179">In dit geval moet u uitvoeren Hallo code in Hallo eerste console toepassing toogenerate handtekeningen voor gebruik in Hallo tweede deel van de zelfstudie Hallo vers gedeelde toegang.</span><span class="sxs-lookup"><span data-stu-id="a834c-179">In this case, you should run hello code in hello first console application toogenerate fresh shared access signatures for use in hello second part of hello tutorial.</span></span>
>

<span data-ttu-id="a834c-180">Maak een nieuwe Windows-consoletoepassing in Visual Studio en noem deze **ConsumeSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="a834c-180">In Visual Studio, create a new Windows console application and name it **ConsumeSharedAccessSignatures**.</span></span> <span data-ttu-id="a834c-181">Voeg verwijzingen te[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) en [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), zoals u eerder hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="a834c-181">Add references too[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), as you did previously.</span></span>

<span data-ttu-id="a834c-182">Aan de bovenkant van de Hallo van het bestand Program.cs hello, voeg Hallo volgende **met** richtlijnen:</span><span class="sxs-lookup"><span data-stu-id="a834c-182">At hello top of hello Program.cs file, add hello following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="a834c-183">In de hoofdtekst Hallo Hallo **Main()** methode Hallo tekenreeksconstanten te volgen, wijzigen de waarden toohello gedeelde toegang handtekeningen u gegenereerd in de zelfstudie hello, deel 1 toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a834c-183">In hello body of hello **Main()** method, add hello following string constants, changing their values toohello shared access signatures you generated in part 1 of hello tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-tootry-container-operations-using-a-shared-access-signature"></a><span data-ttu-id="a834c-184">Een methode tootry container bewerkingen met behulp van een shared access signature toevoegen</span><span class="sxs-lookup"><span data-stu-id="a834c-184">Add a method tootry container operations using a shared access signature</span></span>
<span data-ttu-id="a834c-185">Vervolgens voegt we een methode die een bepaalde container-bewerkingen met behulp van een shared access signature voor Hallo container wordt getest.</span><span class="sxs-lookup"><span data-stu-id="a834c-185">Next, we add a method that tests some container operations using a shared access signature for hello container.</span></span> <span data-ttu-id="a834c-186">shared access signature voor Hallo is gebruikte tooreturn een verwijzing toohello-container toegang toohello container op basis van Hallo handtekening alleen verifiëren.</span><span class="sxs-lookup"><span data-stu-id="a834c-186">hello shared access signature is used tooreturn a reference toohello container, authenticating access toohello container based on hello signature alone.</span></span>

<span data-ttu-id="a834c-187">Hallo methode tooProgram.cs volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="a834c-187">Add hello following method tooProgram.cs:</span></span>

```csharp
static void UseContainerSAS(string sas)
{
    //Try performing container operations with hello SAS provided.

    //Return a reference toohello container using hello SAS URI.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(sas));

    //Create a list toostore blob URIs returned by a listing operation on hello container.
    List<ICloudBlob> blobList = new List<ICloudBlob>();

    //Write operation: write a new blob toohello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference("blobCreatedViaSAS.txt");
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello container. ";
        blob.UploadText(blobContent);

        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //List operation: List hello blobs in hello container.
    try
    {
        foreach (ICloudBlob blob in container.ListBlobs())
        {
            blobList.Add(blob);
        }
        Console.WriteLine("List operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("List operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Get a reference tooone of hello blobs in hello container and read it.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        MemoryStream msRead = new MemoryStream();
        msRead.Position = 0;
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            Console.WriteLine(msRead.Length);
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    Console.WriteLine();

    //Delete operation: Delete a blob in hello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

<span data-ttu-id="a834c-188">Update Hallo **Main()** methode toocall **UseContainerSAS()** met beide Hallo gedeelde handtekeningen voor u op Hallo container gemaakt toegang:</span><span class="sxs-lookup"><span data-stu-id="a834c-188">Update hello **Main()** method toocall **UseContainerSAS()** with both of hello shared access signatures you created on hello container:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    Console.ReadLine();
}
```

### <a name="add-a-method-tootry-blob-operations-using-a-shared-access-signature"></a><span data-ttu-id="a834c-189">Een methode tootry blob-bewerkingen met behulp van een shared access signature toevoegen</span><span class="sxs-lookup"><span data-stu-id="a834c-189">Add a method tootry blob operations using a shared access signature</span></span>
<span data-ttu-id="a834c-190">Ten slotte toevoegen we een methode die bepaalde blob-bewerkingen met behulp van een shared access signature op Hallo blob test.</span><span class="sxs-lookup"><span data-stu-id="a834c-190">Finally, we add a method that tests some blob operations using a shared access signature on hello blob.</span></span> <span data-ttu-id="a834c-191">In dit geval we Hallo constructor gebruiken **CloudBlockBlob(String)**doorgegeven in Hallo shared access signature voor tooreturn een verwijzing toohello blob.</span><span class="sxs-lookup"><span data-stu-id="a834c-191">In this case, we use hello constructor **CloudBlockBlob(String)**, passing in hello shared access signature, tooreturn a reference toohello blob.</span></span> <span data-ttu-id="a834c-192">Er is geen andere verificatie vereist. deze gebaseerd op Hallo handtekening alleen.</span><span class="sxs-lookup"><span data-stu-id="a834c-192">No other authentication is required; it's based on hello signature alone.</span></span>

<span data-ttu-id="a834c-193">Hallo methode tooProgram.cs volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="a834c-193">Add hello following method tooProgram.cs:</span></span>

```csharp
static void UseBlobSAS(string sas)
{
    //Try performing blob operations using hello SAS provided.

    //Return a reference toohello blob using hello SAS URI.
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(sas));

    //Write operation: Write a new blob toohello container.
    try
    {
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello blob. ";
        MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
        msWrite.Position = 0;
        using (msWrite)
        {
            blob.UploadFromStream(msWrite);
        }
        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Read hello contents of hello blob.
    try
    {
        MemoryStream msRead = new MemoryStream();
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            msRead.Position = 0;
            using (StreamReader reader = new StreamReader(msRead, true))
            {
                string line;
                while ((line = reader.ReadLine()) != null)
                {
                    Console.WriteLine(line);
                }
            }
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Delete operation: Delete hello blob.
    try
    {
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

<span data-ttu-id="a834c-194">Update Hallo **Main()** methode toocall **UseBlobSAS()** met beide Hallo gedeelde handtekeningen voor toegang die u op Hallo blob gemaakt:</span><span class="sxs-lookup"><span data-stu-id="a834c-194">Update hello **Main()** method toocall **UseBlobSAS()** with both of hello shared access signatures that you created on hello blob:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    //Call hello test methods with hello shared access signatures created on hello blob, with and without hello access policy.
    UseBlobSAS(blobSAS);
    UseBlobSAS(blobSASWithAccessPolicy);

    Console.ReadLine();
}
```

<span data-ttu-id="a834c-195">Hallo-consoletoepassing uitgevoerd en zien Hallo uitvoer toosee welke bewerkingen zijn toegestaan voor welke handtekeningen.</span><span class="sxs-lookup"><span data-stu-id="a834c-195">Run hello console application and observe hello output toosee which operations are permitted for which signatures.</span></span> <span data-ttu-id="a834c-196">Hallo-uitvoer in het consolevenster Hallo ziet vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="a834c-196">hello output in hello console window will look similar toohello following:</span></span>

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a><span data-ttu-id="a834c-197">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a834c-197">Next Steps</span></span>

* [<span data-ttu-id="a834c-198">Handtekeningen voor gedeelde toegang, deel 1: Understanding Hallo SAS-Model</span><span class="sxs-lookup"><span data-stu-id="a834c-198">Shared Access Signatures, Part 1: Understanding hello SAS Model</span></span>](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="a834c-199">Anonieme leestoegang toocontainers en blobs beheren</span><span class="sxs-lookup"><span data-stu-id="a834c-199">Manage anonymous read access toocontainers and blobs</span></span>](storage-manage-access-to-resources.md)
* [<span data-ttu-id="a834c-200">Delegeren van toegang met een shared access signature (REST-API)</span><span class="sxs-lookup"><span data-stu-id="a834c-200">Delegating access with a shared access signature (REST API)</span></span>](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [<span data-ttu-id="a834c-201">Inleiding tot Table en Queue SAS</span><span class="sxs-lookup"><span data-stu-id="a834c-201">Introducing Table and Queue SAS</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
