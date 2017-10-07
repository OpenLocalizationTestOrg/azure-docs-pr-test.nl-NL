---
title: aaaDevelop voor Azure File storage met .NET | Microsoft Docs
description: Meer informatie over hoe toodevelop .NET-toepassingen en services die gebruikmaken van Azure File storage toostore bestandsgegevens.
services: storage
documentationcenter: .net
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6a889ee1-1e60-46ec-a592-ae854f9fb8b6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: aa8f84f1c93249055370e2a2cb33d7118b972be1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a>Ontwikkelen voor Azure File Storage met .NET 
> [!NOTE]
> Dit artikel laat zien hoe toomanage Azure File storage met .NET-code. Raadpleeg Hallo toolearn meer informatie over Azure File storage [inleiding tooAzure bestandsopslag](storage-files-introduction.md).
>

[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a>Over deze zelfstudie
Deze zelfstudie wordt gedemonstreerd Hallo grondbeginselen van het gebruik van .NET-toodevelop toepassingen of services die gebruikmaken van Azure File storage toostore bestandsgegevens. In deze zelfstudie wordt een eenvoudige consoletoepassing maken en weergeven hoe tooperform basisbewerkingen uitvoeren met .NET- en Azure File storage:

* Hallo-inhoud van een bestand ophalen
* Hallo quotum (maximumgrootte) voor bestandsshare Hallo instellen.
* Maak een shared access signature (SAS-sleutel) voor een bestand dat gebruikmaakt van een gedeeld toegangsbeleid dat is gedefinieerd op Hallo-share.
* Kopieer een bestand tooanother in Hallo hetzelfde opslagaccount.
* Kopieer een bestand tooa blob in Hallo hetzelfde opslagaccount.
* Metrische gegevens van Azure Storage gebruiken voor het oplossen van problemen

> [!Note]  
> Omdat Azure File storage zijn toegankelijk via SMB, is het mogelijk toowrite eenvoudige toepassingen die toegang hebben tot hello Azure bestandsshare met behulp van Hallo standaardklassen System.IO voor i/o-bestand. In dit artikel wordt beschreven hoe toowrite toepassingen die gebruikmaken van Azure Storage .NET SDK, die gebruikmaakt van Hallo Hallo [Azure File storage REST-API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage. 


## <a name="create-hello-console-application-and-obtain-hello-assembly"></a>Hallo-consoletoepassing maken en Hallo assembly verkrijgen
Maak in Visual Studio een nieuwe Windows-consoletoepassing. Hallo stappen ziet u hoe toocreate een consoletoepassing in Visual Studio 2017 echter Hallo stappen zijn vergelijkbaar in andere versies van Visual Studio.

1. Selecteer **Bestand** > **Nieuw** > **Project**
2. Selecteer **Geïnstalleerd** > **Sjablonen** > **Visual C#** > **Klassiek Windows-bureaublad**
3. Selecteer **Consoletoepassing (.NET Framework)**
4. Voer een naam voor uw toepassing in Hallo **naam:** veld
5. Selecteer **OK**

Alle codevoorbeelden in deze zelfstudie kunnen worden toegevoegd toohello `Main()` methode van uw consoletoepassing `Program.cs` bestand.

U kunt hello Azure Storage-clientbibliotheek gebruiken in elk type .NET-toepassing, met inbegrip van een Azure-cloud service of web-app en desktop- en mobiele toepassingen. In deze gids gebruiken we een consoletoepassing voor de eenvoud.

## <a name="use-nuget-tooinstall-hello-required-packages"></a>Gebruik NuGet tooinstall vereist hello-pakketten
Er zijn twee pakketten die u in deze zelfstudie tooreference in uw project toocomplete nodig:

* [Microsoft Azure Storage-clientbibliotheek voor .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): dit pakket biedt programmatisch toegang toodata resources in uw opslagaccount.
* [Configuration Manager-bibliotheek van Microsoft Azure voor .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): dit pakket biedt een klasse voor het parseren van een verbindingsreeks in een configuratiebestand, ongeacht waar de toepassing wordt uitgevoerd.

U kunt beide pakketten NuGet tooobtain. Volg deze stappen:

1. Klik met de rechtermuisknop op het project in **Solution Explorer** en kies **NuGet-pakketten beheren**.
2. Zoek online naar 'WindowsAzure.Storage' en klik op **installeren** tooinstall Hallo Storage-clientbibliotheek en de bijbehorende afhankelijkheden.
3. Zoek online naar 'WindowsAzure.ConfigurationManager' en klik op **installeren** tooinstall hello Azure Configuration Manager.

## <a name="save-your-storage-account-credentials-toohello-appconfig-file"></a>Het storage-account referenties toohello app.config-bestand opslaan
Vervolgens slaat u uw referenties op in het bestand app.config van het project. Hallo app.config-bestand bewerken zodat het lijkt of vergelijkbare toohello voorbeeld te volgen en vervangt `myaccount` met de naam van uw opslagaccount, en `mykey` door de sleutel van uw opslagaccount.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=StorageAccountKeyEndingIn==" />
    </appSettings>
</configuration>
```

> [!NOTE]
> Hallo meest recente versie van hello Azure-opslagemulator biedt geen ondersteuning voor Azure File storage. De verbindingsreeks moet gericht zijn op een Azure Storage-Account in Hallo cloud toowork met Azure File storage.

## <a name="add-using-directives"></a>Using-instructies toevoegen
Open Hallo `Program.cs` bestand van Solution Explorer, en voeg de volgende Hallo met richtlijnen toohello boven in Hallo-bestand.

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-hello-file-share-programmatically"></a>Toegang tot Hallo-bestand delen via een programma
Vervolgens voegt u code toohello na Hallo `Main()` methode (na de hierboven weergegeven code Hallo) tooretrieve Hallo-verbindingsreeks. Deze code wordt een referentiebestand toohello die we eerder hebben gemaakt en levert het consolevenster van inhoud toohello.

```csharp
// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello file exists.
        if (file.Exists())
        {
            // Write hello contents of hello file toohello console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

Hallo console toepassing toosee Hallo-uitvoer worden uitgevoerd.

## <a name="set-hello-maximum-size-for-a-file-share"></a>Hallo maximale grootte voor een bestandsshare instellen
Vanaf versie 5.x van hello Azure Storage-clientbibliotheek kunt u instellen set Hallo quotum (of maximumgrootte) voor een bestandsshare in gigabytes. U kunt ook controleren hoeveel gegevens er momenteel zijn opgeslagen op Hallo share toosee.

Door de instelling Hallo quotum voor een share, kunt u Hallo totale grootte van bestanden op Hallo share Hallo beperken. Als Hallo totale grootte van bestanden op Hallo share overschrijdt Hallo quota ingesteld voor de share Hallo en clients worden niet kan tooincrease Hallo grootte van de bestaande bestanden of nieuwe bestanden maken, tenzij deze bestanden leeg zijn.

Hallo voorbeeld hieronder ziet u hoe toocheck huidige gebruik voor een share Hallo en hoe tooset quotum voor de share Hallo Hallo.

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Check current usage stats for hello share.
    // Note that hello ShareStats object is part of hello protocol layer for hello File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify hello maximum size of hello share, in GB.
    // This line sets hello quota toobe 10 GB greater than hello current usage of hello share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check hello quota for hello share. Call FetchAttributes() toopopulate hello share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>Een Shared Access Signature genereren voor een bestand of bestandsshare
Vanaf versie 5.x van Azure Storage-clientbibliotheek Hallo, kunt u een shared access signature (SAS) voor een bestandsshare of voor een afzonderlijk bestand genereren. U kunt ook een gedeeld toegangsbeleid op een bestandsshare-toomanage gedeelde toegang handtekeningen maken. Maken van een gedeeld toegangsbeleid wordt aanbevolen, aangezien deze een manier om Hallo SAS intrekken biedt als deze verdacht.

Hallo volgende voorbeeld wordt een beleid voor gedeelde toegang gemaakt op een bestandsshare op en gebruikt u vervolgens dat tooprovide Hallo beleidsbeperkingen voor een SAS voor een bestand in Hallo delen.

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for hello share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add hello shared access policy toohello share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in hello share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

Voor meer informatie over het maken en gebruiken van handtekeningen voor gedeelde toegang, raadpleegt u [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) (Shared Access Signatures (SAS) gebruiken) en [Create and use a SAS with Azure Blobs](storage-dotnet-shared-access-signature-part-2.md) (Een SAS maken en gebruiken met Azure Blobs).

## <a name="copy-files"></a>Bestanden kopiëren
Vanaf versie 5.x van Azure Storage-clientbibliotheek hello, kunt u een bestand tooanother, een bestand tooa blob of een blob tooa-bestand kopiëren. In de volgende secties hello, ziet u hoe tooperform die deze kopiëren bewerkingen via een programma.

U kunt ook AzCopy toocopy één bestand tooanother of toocopy een blob tooa bestand of vice versa. Zie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md).

> [!NOTE]
> Als u een blob tooa-bestand of een bestand tooa blob kopieert, moet u een shared access signature (SAS) tooauthenticate Hallo bronobject, zelfs als u binnen Hallo dezelfde kopieert storage-account.
> 
> 

**Kopieer een bestand tooanother** hello volgende voorbeeld wordt een bestand tooanother in Hallo dezelfde share. Omdat deze kopieerbewerking gekopieerd tussen de bestanden in hetzelfde opslagaccount Hallo, kunt u gedeelde sleutel verificatie tooperform Hallo kopiëren.

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference toohello destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start hello copy operation.
            destFile.StartCopy(sourceFile);

            // Write hello contents of hello destination file toohello console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

**Kopieer een bestand tooa blob** hello volgende voorbeeld wordt een bestand gemaakt en gekopieerd tooa blob in Hallo hetzelfde opslagaccount. Hallo-voorbeeld wordt een SAS voor bronbestand hello, welke service Hallo tooauthenticate toegang toohello bronbestand tijdens de kopieerbewerking Hallo gebruikt gemaakt.

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in hello root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in hello root directory.");

// Get a reference toohello blob toowhich hello file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for hello file that's valid for 24 hours.
// Note that when you are copying a file tooa blob, or a blob tooa file, you must use a SAS
// tooauthenticate access toohello source object, even if you are copying within hello same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for hello source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct hello URI toohello source file, including hello SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy hello file toohello blob.
destBlob.StartCopy(fileSasUri);

// Write hello contents of hello file toohello console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

U kunt een blob tooa-bestand kopiëren in Hallo dezelfde manier. Als Hallo bronobject een blob is, maakt u een blob SAS tooauthenticate toegang toothat tijdens de kopieerbewerking Hallo.

## <a name="troubleshooting-azure-file-storage-using-metrics"></a>Problemen met Azure File Storage oplossen met metrische gegevens
Azure Storage Analytics ondersteunt nu metrische gegevens voor Azure File Storage. Met metrische gegevens kunt u aanvragen volgen en problemen diagnosticeren.


U kunt metrische gegevens voor Azure File storage uit Hallo inschakelen [Azure Portal](https://portal.azure.com). U kunt ook de metrische gegevens via een programma door de aanroepende Hallo bewerking Set File Service Properties via Hallo REST-API of een van de analogen daarvan in Hallo Storage-clientbibliotheek inschakelen.


Hallo volgende codevoorbeeld toont hoe toouse Storage-clientbibliotheek voor .NET tooenable metrische gegevens voor Azure File storage Hallo.

Voeg eerst de volgende Hallo `using` richtlijnen tooyour `Program.cs` bestand bovendien toothose die u hebt toegevoegd:

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

Denk eraan dat bij Azure Blobs, Azure Table en Azure wachtrijen Hallo gedeeld gebruiken `ServiceProperties` type in Hallo `Microsoft.WindowsAzure.Storage.Shared.Protocol` naamruimte, Azure File storage heeft een eigen type, hello `FileServiceProperties` type in Hallo `Microsoft.WindowsAzure.Storage.File.Protocol` naamruimte. Beide naamruimten moet worden verwezen vanuit uw code echter voor Hallo code toocompile te volgen.

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create hello File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that hello File service currently uses its own service properties type,
// available in hello Microsoft.WindowsAzure.Storage.File.Protocol namespace.
fileClient.SetServiceProperties(new FileServiceProperties()
{
    // Set hour metrics
    HourMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 14,
        Version = "1.0"
    },
    // Set minute metrics
    MinuteMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 7,
        Version = "1.0"
    }
});

// Read hello metrics properties we just set.
FileServiceProperties serviceProperties = fileClient.GetServiceProperties();
Console.WriteLine("Hour metrics:");
Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
Console.WriteLine(serviceProperties.HourMetrics.Version);
Console.WriteLine();
Console.WriteLine("Minute metrics:");
Console.WriteLine(serviceProperties.MinuteMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.MinuteMetrics.RetentionDays);
Console.WriteLine(serviceProperties.MinuteMetrics.Version);
```

Bovendien kunt u verwijzen te[Azure File storage probleemoplossing artikel](storage-troubleshoot-file-connection-problems.md) voor richtlijnen voor probleemoplossing voor end-to-end.

## <a name="next-steps"></a>Volgende stappen
Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.

### <a name="conceptual-articles-and-videos"></a>Conceptuele artikelen en video's
* [Azure File Storage: een naadloos SMB-bestandssysteem voor Windows en Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [Hoe toouse Azure File storage met Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>Hulpprogramma-ondersteuning voor File Storage
* [Azure PowerShell gebruiken met Azure Storage](storage-powershell-guide-full.md)
* [Hoe toouse AzCopy met Microsoft Azure Storage](storage-use-azcopy.md)
* [Hello Azure CLI gebruiken met Azure Storage](storage-azure-cli.md#create-and-manage-file-shares)
* [Problemen met betrekking tot Azure File Storage oplossen](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a>Naslaginformatie
* [Naslaginformatie over de Storage-clientbibliotheek voor .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Naslaginformatie over REST API voor bestandsservices](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a>Blogberichten
* [Azure File storage is now generally available (Azure File Storage is nu algemeen beschikbaar)](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Inside Azure File Storage (Een kijkje achter de schermen van Azure File Storage)](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Introducing Microsoft Azure File Service (Introductie van Microsoft Azure File-service)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Persistente verbindingen tooMicrosoft Azure File storage](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
