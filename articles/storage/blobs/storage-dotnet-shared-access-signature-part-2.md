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
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a>Shared Access Signatures, deel 2: Maken en gebruiken van een SAS met Blob-opslag

[Deel 1](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) shared access signatures (SAS) van deze zelfstudie verkend en aanbevolen procedures voor het gebruik ervan beschreven. Deel 2 ziet u hoe toogenerate en gebruik vervolgens toegang gedeeld handtekeningen met Blob storage. Hallo-voorbeelden zijn geschreven in C# en gebruiken van hello Azure Storage-clientbibliotheek voor .NET. Hallo-voorbeelden in deze zelfstudie:

* Een shared access signature in een container genereren
* Een shared access signature op een blob genereren
* Een opgeslagen toegang beleid toomanage handtekeningen maken op een container bronnen
* Handtekeningen voor gedeelde Hallo toegang testen in een clienttoepassing

## <a name="about-this-tutorial"></a>Over deze zelfstudie
In deze zelfstudie maken we twee consoletoepassingen die laten zien maken en gebruiken van handtekeningen voor gedeelde toegang voor containers en blobs:

**1 toepassing**: Hallo management-toepassing. Genereert een shared access signature voor een container en een blob. Hallo toegangssleutel voor opslagaccount bevat in de broncode.

**Toepassing 2**: Hallo van client-toepassing. Toegang tot een container en blob bronnen gebruiken van handtekeningen van Hallo gedeelde toegang gemaakt met de eerste toepassing hello. Maakt gebruik van alleen Hallo gedeelde toegang handtekeningen tooaccess container en resources van de blob--biedt *niet* Hallo toegangssleutel voor opslagaccount bevatten.

## <a name="part-1-create-a-console-application-toogenerate-shared-access-signatures"></a>Deel 1: Een toogenerate gedeelde toegang tot de console application handtekeningen maken
Eerst voor zorgen dat er hello Azure Storage-clientbibliotheek voor .NET is geïnstalleerd. U kunt installeren Hallo [NuGet-pakket](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet-pakket") met Hallo meest recente assembly's voor Hallo-clientbibliotheek. Dit is de aanbevolen methode om ervoor te zorgen dat u de meest recente oplossingen Hallo hebt Hallo. U kunt ook de clientbibliotheek Hallo downloaden als onderdeel van de meest recente versie Hallo Hallo [Azure SDK voor .NET](https://azure.microsoft.com/downloads/).

Maak een nieuwe Windows-consoletoepassing in Visual Studio en noem deze **GenerateSharedAccessSignatures**. Voeg verwijzingen te[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) en [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) met behulp van een Hallo benaderingen te volgen:

* Gebruik Hallo [NuGet-Pakketbeheer](https://docs.nuget.org/consume/installing-nuget) in Visual Studio. Selecteer **Project** > **NuGet-pakketten beheren**, online zoeken naar elk pakket (Microsoft.WindowsAzure.ConfigurationManager en WindowsAzure.Storage) en deze installeren.
* U kunt ook deze assembly's in uw installatie van hello Azure SDK en verwijzingen toothem toevoegen:
  * Microsoft.WindowsAzure.Configuration.dll
  * Microsoft.WindowsAzure.Storage.dll

Aan de bovenkant van de Hallo van het bestand Program.cs hello, voeg Hallo volgende **met** richtlijnen:

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

Hallo app.config-bestand bewerken zodat deze een configuratie-instelling met een verbindingsreeks die tooyour opslagaccount wijst bevat. Het bestand app.config ziet vergelijkbare toothis een:

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

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a>Een shared access signature URI voor een container genereren
toobegin met we een toogenerate methode een shared access signature voor een nieuwe container toevoegen. In dit geval Hallo handtekening is niet gekoppeld aan een opgeslagen-beleid, zodat zij werkzaam Hallo URI Hallo informatie geeft de verloopdatum tijd en Hallo machtigingen verleent.

Voeg eerst code toohello **Main()** methode tooauthenticate tooyour storage-account openen en een nieuwe container maken:

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

Vervolgens voegt u een methode die genereert Hallo shared access signature voor Hallo-container en Hallo handtekening URI geretourneerd:

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

Toevoegen van de volgende regels onderin Hallo HALLO hallo **Main()** methode voordat Hallo aanroepen te**Console.ReadLine()**, toocall **GetContainerSasUri()** en schrijf Hallo handtekening URI toohello consolevenster:

```csharp
//Generate a SAS URI for hello container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

Compileren en toooutput Hallo shared access signature URI voor de nieuwe container Hallo uitvoeren. Hallo URI zijn vergelijkbaar toohello volgende:

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

Zodra u Hallo code hebt uitgevoerd, is Hallo shared access signature voor die u voor de container Hallo gemaakt geldig voor Hallo binnen 24 uur. Hallo handtekening verleent een client machtiging toolist blobs in Hallo-container en toowrite nieuwe blobs toohello container.

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a>Een shared access signature URI voor een blob genereren
Vervolgens we schrijven vergelijkbare code toocreate een nieuwe blob in Hallo-container en een shared access signature voor het genereren. Deze shared access signature is niet gekoppeld aan een opgeslagen-beleid, zodat deze functie Hallo begintijd, verlooptijd en toestemming informatie Hallo URI bevat.

Voeg een nieuwe methode die u maakt een nieuwe blob en sommige tooit tekst schrijft vervolgens genereert een shared access signature en Hallo handtekening URI geretourneerd:

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

Hallo Hallo onderaan in **Main()** methode toevoegen van de volgende regels toocall Hallo **GetBlobSasUri()**, voordat Hallo aanroepen te**Console.ReadLine()**, en schrijf Hallo gedeeld toegang handtekening URI toohello consolevenster:

```csharp
//Generate a SAS URI for a blob within hello container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

Compileren en toooutput Hallo shared access signature URI voor de nieuwe blob Hallo uitvoeren. Hallo URI zijn vergelijkbaar toohello volgende:

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-hello-container"></a>Een opgeslagen toegangsbeleid maken op Hallo-container
Nu gaan we een opgeslagen toegangsbeleid maken op Hallo-container die definieert Hallo beperkingen voor alle handtekeningen voor gedeelde toegang die gekoppeld zijn.

In de voorgaande voorbeelden hello, we Hallo begintijd opgegeven (impliciet of expliciet), Hallo verlooptijd en machtigingen op Hallo Hallo gedeeld access signature voor URI zelf. In de Hallo volgen voorbeelden, geef deze op Hallo opgeslagen toegangsbeleid en niet op Hallo shared access signature voor. In dat geval schakelt doen ons toochange deze beperkingen zonder opnieuw uitgeven van Hallo gedeelde toegang tot handtekening.

Het is mogelijk toohave een of meer Hallo beperkingen voor shared access signature voor Hallo en Hallo-rest van het toegangsbeleid Hallo opgeslagen. U kunt de begintijd hello, verlooptijd en machtigingen alleen opgeven in een plaats of Hallo andere. U kan bijvoorbeeld machtigingen opgeven op Hallo shared access signature voor en geef ze ook op Hallo opgeslagen toegangsbeleid.

Wanneer u een opgeslagen toegang beleid tooa container toevoegt, moet u bestaande machtigingen van de container Hallo ophalen, Hallo nieuwe toegangsbeleid toevoegen en vervolgens Hallo-container machtigingen instellen.

Voeg een nieuwe methode die een nieuw opgeslagen-beleid maakt in een container en retourneert Hallo-naam van het Hallo-beleid:

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

Hallo Hallo onderaan in **Main()** methode voordat Hallo aanroepen te**Console.ReadLine()**, Hallo volgende regels toofirst Wis alle bestaande beleidsregels voor toegang toevoegen en vervolgens aanroepen Hallo  **CreateSharedAccessPolicy()** methode:

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

Wanneer u Hallo-beleid in een container uitschakelt, moet u eerst ophalen van de container Hallo bestaande machtigingen en klik vervolgens wissen Hallo machtigingen vervolgens Hallo machtigingen opnieuw instellen.

### <a name="generate-a-shared-access-signature-uri-on-hello-container-that-uses-an-access-policy"></a>Een shared access signature-URI op Hallo-container die gebruikmaakt van een toegangsbeleid genereren
Vervolgens maken we een andere shared access signature voor Hallo-container die we eerder hebben gemaakt, maar nu we Hallo handtekening koppelen aan toegangsbeleid Hallo opgeslagen die in het vorige voorbeeld Hallo is gemaakt.

Een nieuwe methode toogenerate een andere shared access signature voor Hallo-container toevoegen:

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

Hallo Hallo onderaan in **Main()** methode voordat Hallo aanroepen te**Console.ReadLine()**, toevoegen van de volgende regels toocall Hallo Hallo **GetContainerSasUriWithPolicy** methode :

```csharp
//Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-hello-blob-that-uses-an-access-policy"></a>Genereren van een gedeelde toegang handtekening-URI op Hallo Blob dat gebruikmaakt van een toegangsbeleid
Ten slotte we een vergelijkbare methode toocreate een andere blob toevoegen en een shared access signature die is gekoppeld aan een opgeslagen toegangsbeleid genereren.

Voeg een nieuwe methode toocreate een blob en een shared access signature genereren:

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

Hallo Hallo onderaan in **Main()** methode voordat Hallo aanroepen te**Console.ReadLine()**, toevoegen van de volgende regels toocall Hallo Hallo **GetBlobSasUriWithPolicy** methode:

```csharp
//Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

Hallo **Main()** methode ziet er nu als volgt in zijn geheel. Deze shared access signature toohello consolevenster URI's voor toowrite Hallo uitvoeren Kopieer en plak ze in een tekstbestand voor gebruik in Hallo tweede deel van deze zelfstudie.

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

Wanneer u Hallo GenerateSharedAccessSignatures consoletoepassing uitvoert, ziet u uitvoer vergelijkbare toohello volgende. Dit zijn de handtekeningen voor gedeelde Hallo toegang die u in deel 2 van de zelfstudie hello gebruiken.

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-tootest-hello-shared-access-signatures"></a>Deel 2: Een toegang tot de console application tootest Hallo gedeelde handtekeningen maken
Hallo tootest gedeelde toegang handtekeningen die zijn gemaakt in de voorgaande voorbeelden hello, maken we een tweede consoletoepassing die gebruikmaakt van Hallo handtekeningen tooperform bewerkingen op Hallo-container en op een blob.

> [!NOTE]
> Als meer dan 24 uur zijn verstreken sinds u Hallo eerste deel van Hallo-zelfstudie hebt voltooid, is Hallo handtekeningen die u hebt gegenereerd niet langer geldig. In dit geval moet u uitvoeren Hallo code in Hallo eerste console toepassing toogenerate handtekeningen voor gebruik in Hallo tweede deel van de zelfstudie Hallo vers gedeelde toegang.
>

Maak een nieuwe Windows-consoletoepassing in Visual Studio en noem deze **ConsumeSharedAccessSignatures**. Voeg verwijzingen te[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) en [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), zoals u eerder hebt gedaan.

Aan de bovenkant van de Hallo van het bestand Program.cs hello, voeg Hallo volgende **met** richtlijnen:

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

In de hoofdtekst Hallo Hallo **Main()** methode Hallo tekenreeksconstanten te volgen, wijzigen de waarden toohello gedeelde toegang handtekeningen u gegenereerd in de zelfstudie hello, deel 1 toevoegen.

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-tootry-container-operations-using-a-shared-access-signature"></a>Een methode tootry container bewerkingen met behulp van een shared access signature toevoegen
Vervolgens voegt we een methode die een bepaalde container-bewerkingen met behulp van een shared access signature voor Hallo container wordt getest. shared access signature voor Hallo is gebruikte tooreturn een verwijzing toohello-container toegang toohello container op basis van Hallo handtekening alleen verifiëren.

Hallo methode tooProgram.cs volgende toevoegen:

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

Update Hallo **Main()** methode toocall **UseContainerSAS()** met beide Hallo gedeelde handtekeningen voor u op Hallo container gemaakt toegang:

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

### <a name="add-a-method-tootry-blob-operations-using-a-shared-access-signature"></a>Een methode tootry blob-bewerkingen met behulp van een shared access signature toevoegen
Ten slotte toevoegen we een methode die bepaalde blob-bewerkingen met behulp van een shared access signature op Hallo blob test. In dit geval we Hallo constructor gebruiken **CloudBlockBlob(String)**doorgegeven in Hallo shared access signature voor tooreturn een verwijzing toohello blob. Er is geen andere verificatie vereist. deze gebaseerd op Hallo handtekening alleen.

Hallo methode tooProgram.cs volgende toevoegen:

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

Update Hallo **Main()** methode toocall **UseBlobSAS()** met beide Hallo gedeelde handtekeningen voor toegang die u op Hallo blob gemaakt:

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

Hallo-consoletoepassing uitgevoerd en zien Hallo uitvoer toosee welke bewerkingen zijn toegestaan voor welke handtekeningen. Hallo-uitvoer in het consolevenster Hallo ziet vergelijkbare toohello volgende:

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a>Volgende stappen

* [Handtekeningen voor gedeelde toegang, deel 1: Understanding Hallo SAS-Model](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [Anonieme leestoegang toocontainers en blobs beheren](storage-manage-access-to-resources.md)
* [Delegeren van toegang met een shared access signature (REST-API)](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [Inleiding tot Table en Queue SAS](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
