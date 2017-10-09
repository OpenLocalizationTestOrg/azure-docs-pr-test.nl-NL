---
title: aaaTutorial - gebruik hello Azure Batch-clientbibliotheek voor .NET | Microsoft Docs
description: Leer de basisconcepten Hallo van Azure Batch en bouwen van een eenvoudige oplossing met behulp van .NET.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 76cb9807-cbc1-405a-8136-d1e53e66e82b
ms.service: batch
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06062b3886a8081bd9a831824a981503ef55f9b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-building-solutions-with-hello-batch-client-library-for-net"></a>Aan de slag bouwen van oplossingen met Hallo Batch-clientbibliotheek voor .NET

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Leer de basisbeginselen Hallo van [Azure Batch] [ azure_batch] en Hallo [Batch .NET] [ net_api] bibliotheek in dit artikel als bespreken we een C#-voorbeeld stap toepassing door stap. Kijken we hoe Hallo Batch-service tooprocess in Hallo-voorbeeldtoepassing gebruikmaakt van een parallelle workload in Hallo cloud en hoe deze samenwerkt met [Azure Storage](../storage/common/storage-introduction.md) voor Faseren en ophalen. U hebt meer informatie over een algemene werkstroom voor Batch-toepassing en een elementair inzicht in Hallo belangrijkste onderdelen van Batch zoals jobs, taken, pools en rekenknooppunten.

![Werkstroom van de Batch-oplossing (basis)][11]<br/>

## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u praktische kennis hebt van C# en Visual Studio. Ook wordt ervan uitgegaan dat u kunnen toosatisfy Hallo-account maken vereisten die bent hieronder zijn opgegeven voor de Azure- en hello Batch- en opslagservices.

### <a name="accounts"></a>Accounts
* **Azure-account**: als u nog geen Azure-abonnement hebt, [maakt u een gratis Azure-account][azure_free_account].
* **Batch-account**: als u al een Azure-abonnement hebt, [maakt u een Azure Batch-account](batch-account-create-portal.md).
* **Opslagaccount**: zie [Een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [Over Azure-opslagaccounts](../storage/common/storage-create-storage-account.md).

> [!IMPORTANT]
> Batch ondersteunt momenteel *alleen* hello **algemeen** opslagaccounttype, zoals beschreven in stap &#5; [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [over Azure Storage-accounts](../storage/common/storage-create-storage-account.md).
>
>

### <a name="visual-studio"></a>Visual Studio
U moet hebben **Visual Studio 2015 of hoger** toobuild Hallo-voorbeeldproject. U vindt gratis en evaluatieversies van Visual Studio in Hallo [overzicht van Visual Studio-producten][visual_studio].

### <a name="dotnettutorial-code-sample"></a>*DotNetTutorial*-codevoorbeeld
Hallo [DotNetTutorial] [ github_dotnettutorial] voorbeeld is een van de vele Batch-codevoorbeelden in Hallo gevonden Hallo [azure-batch-samples] [ github_samples] opslagplaats op GitHub. U kunt alle Hallo voorbeelden downloaden door te klikken op **klonen of downloaden > ZIP downloaden** op de startpagina Hallo-opslagplaats of door te klikken op Hallo [azure-batch-samples-master.zip] [ github_samples_zip]directe downloadkoppeling. Nadat u de inhoud van het ZIP-bestand Hallo Hallo hebt uitgepakt, vindt u Hallo oplossing in Hallo volgende map:

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a>Azure Batch Explorer (optioneel)
Hallo [Azure Batch Explorer] [ github_batchexplorer] is een gratis hulpprogramma dat is opgenomen in Hallo [azure-batch-samples] [ github_samples] opslagplaats op GitHub. Tijdens het niet vereist toocomplete in deze zelfstudie, dit kan nuttig zijn bij de ontwikkeling en foutopsporing van uw Batch-oplossingen.

## <a name="dotnettutorial-sample-project-overview"></a>Overzicht DotNetTutorial-voorbeeldproject
Hallo *DotNetTutorial* codevoorbeeld is een Visual Studio-oplossing die uit twee projecten bestaat: **DotNetTutorial** en **TaskApplication**.

* **DotNetTutorial** is Hallo-clienttoepassing die met de Hallo Batch- en Storage services tooexecute een parallelle workload op rekenknooppunten (virtuele machines communiceert). DotNetTutorial wordt uitgevoerd op uw lokale werkstation.
* **TaskApplication** is Hallo programma dat wordt uitgevoerd op rekenknooppunten in Azure tooperform Hallo echte werk. In voorbeeld Hallo `TaskApplication.exe` parseert Hallo tekst in een bestand gedownload van Azure Storage (Hallo-invoerbestand). En vervolgens het genereert een tekstbestand (Hallo uitvoerbestand) die een lijst van Hallo eerste drie woorden die worden weergegeven in het invoerbestand Hallo bevat. Nadat het Hallo-uitvoerbestand heeft gemaakt, uploadt TaskApplication Hallo bestand tooAzure opslag. Hierdoor kunt u de clienttoepassing beschikbaar toohello downloaden. TaskApplication wordt parallel uitgevoerd op meerdere rekenknooppunten in Hallo Batch-service.

Hallo volgende diagram illustreert Hallo primaire bewerkingen die worden uitgevoerd door de clienttoepassing Hallo *DotNetTutorial*, en het Hallo-toepassing die wordt uitgevoerd door Hallo-taken *TaskApplication*. Deze basiswerkstroom is typerend voor vele rekenoplossingen die met Batch worden gemaakt. Hoewel hierin niet elke beschikbare functie in Hallo Batch-service, omvat vrijwel elk Batch-scenario gedeelten van deze werkstroom.

![Batch-voorbeeldwerkstroom][8]<br/>

[**Stap 1.**](#step-1-create-storage-containers) Maak **containers** in Azure Blob Storage.<br/>
[**Stap 2.**](#step-2-upload-task-application-and-data-files) Upload taaktoepassings- en invoerbestanden toocontainers.<br/>
[**Stap 3.**](#step-3-create-batch-pool) Maak een Batch-**pool**.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** Hallo groep **StartTask** downloads Hallo taak binaire bestanden (TaskApplication) toonodes wanneer ze aan Hallo groep worden toegevoegd.<br/>
[**Stap 4.**](#step-4-create-batch-job) Maak een Batch-**job**.<br/>
[**Stap 5.**](#step-5-add-tasks-to-job) Voeg **taken** toohello taak.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** Hallo-taken zijn gepland tooexecute op knooppunten.<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;**5b.** Elke taak downloadt de bijbehorende invoergegevens uit Azure Storage en wordt daarna uitgevoerd.<br/>
[**Stap 6.**](#step-6-monitor-tasks) Controleer taken.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** Nadat taken zijn voltooid, uploaden zij hun uitvoer gegevens tooAzure opslag.<br/>
[**Stap 7.**](#step-7-download-task-output) Download taakuitvoer uit Storage.

Zoals gezegd, niet elke Batch-oplossing deze exacte stappen worden uitgevoerd en kan nog veel meer bevatten, maar Hallo *DotNetTutorial* voorbeeldtoepassing toont de algemene processen die in een Batch-oplossing.

## <a name="build-hello-dotnettutorial-sample-project"></a>Hallo bouwen *DotNetTutorial* voorbeeldproject
Voordat u Hallo voorbeeld met succes uitvoeren kunt, moet u de Batch- en Storage-accountreferenties opgeven in Hallo *DotNetTutorial* van het project `Program.cs` bestand. Als u dit nog niet hebt gedaan, opent u Hallo oplossing in Visual Studio door te dubbelklikken op Hallo `DotNetTutorial.sln` oplossingsbestand. Openen in Visual Studio met behulp van Hallo **bestand > openen > Project/oplossing** menu.

Open `Program.cs` binnen Hallo *DotNetTutorial* project. Voeg vervolgens uw referenties toe zoals opgegeven in de buurt Hallo bovenaan Hallo-bestand:

```csharp
// Update hello Batch and Storage account credential strings below with hello values
// unique tooyour accounts. These are used when constructing connection strings
// for hello Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> Zoals eerder vermeld, moet u momenteel opgeven Hallo referenties voor een **algemeen** storage-account in Azure Storage. Uw Batch-toepassingen gebruiken blob storage in Hallo **algemeen** storage-account. Geef geen referenties voor een opslagaccount dat is gemaakt door het selecteren van Hallo Hallo *Blob storage* accounttype.
>
>

U vindt uw Batch- en Storage-accountreferenties op Hallo accountblade van elke service op Hallo [Azure-portal][azure_portal]:

![Batch-referenties in portal Hallo][9]
![Storage-referenties in portal Hallo][10]<br/>

Nu dat u Hallo-project met uw referenties hebt bijgewerkt, met de rechtermuisknop op het Hallo-oplossing in Solution Explorer en klikt u op **Build Solution**. Bevestig Hallo herstel van alle NuGet-pakketten als u wordt gevraagd.

> [!TIP]
> Zorg ervoor dat er Hallo als Hallo NuGet-pakketten niet automatisch worden hersteld of als er fouten over een mislukte toorestore hello-pakketten, [NuGet Package Manager] [ nuget_packagemgr] geïnstalleerd. Schakel vervolgens Hallo downloaden van ontbrekende pakketten. Zie [inschakelen pakket herstellen tijdens bouwen] [ nuget_restore] tooenable pakket downloaden.
>
>

In Hallo uit te voeren, we Hallo voorbeeldtoepassing uitgesplitst in Hallo stappen die het tooprocess uitvoert een workload in Hallo Batch-service en worden die stappen in detail. We raden u toorefer toohello geopende oplossing in Visual Studio terwijl u zich door de rest van dit artikel Hallo werkt, omdat niet elke regel code in Hallo voorbeeld wordt besproken.

Navigeer toohello bovenaan Hallo `MainAsync` methode in Hallo *DotNetTutorial* van het project `Program.cs` bestand toostart bij stap 1. Elke stap hieronder vervolgens ongeveer volgt Hallo voortgang van de methode aanroept `MainAsync`.

## <a name="step-1-create-storage-containers"></a>Stap 1: opslagcontainers maken
![Containers maken in Azure Storage][1]
<br/>

Batch bevat ingebouwde ondersteuning voor interactie met Azure Storage. Containers in uw opslagaccount biedt Hallo-bestanden die nodig zijn door Hallo-taken die worden uitgevoerd in uw Batch-account. Hallo containers bieden ook een uitvoergegevens van plaats toostore Hallo die Hallo taken opleveren. Hallo eerst te beginnen Hallo *DotNetTutorial* clienttoepassing biedt is drie containers maken in [Azure Blob Storage](../storage/common/storage-introduction.md):

* **toepassing**: deze container slaat Hallo toepassing hello taken, evenals alle afhankelijkheden hiervan, zoals dll's uitvoeren.
* **invoer**: taken downloaden de Hallo gegevens bestanden tooprocess vanaf Hallo *invoer* container.
* **uitvoer**: bij de verwerking van invoerbestanden taken hebt voltooid, uploaden zij Hallo resultaten toohello *uitvoer* container.

In de volgorde toointeract met een Storage-account in en containers, maken we hello gebruiken [Azure Storage-clientbibliotheek voor .NET][net_api_storage]. We maken een verwijzing toohello-account met [CloudStorageAccount][net_cloudstorageaccount], en van hieruit maken een [CloudBlobClient][net_cloudblobclient]:

```csharp
// Construct hello Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve hello storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create hello blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

We gebruiken Hallo `blobClient` verwijzing in de toepassing hello en tooseveral methoden doorgegeven als parameter. Een voorbeeld hiervan is in Hallo codeblok dat onmiddellijk volgt Hallo bovenstaande waar we noemen `CreateContainerIfNotExistAsync` tooactually Hallo containers te maken.

```csharp
// Use hello blob client toocreate hello containers in Azure Storage if they don't
// yet exist
const string appContainerName    = "application";
const string inputContainerName  = "input";
const string outputContainerName = "output";
await CreateContainerIfNotExistAsync(blobClient, appContainerName);
await CreateContainerIfNotExistAsync(blobClient, inputContainerName);
await CreateContainerIfNotExistAsync(blobClient, outputContainerName);
```

```csharp
private static async Task CreateContainerIfNotExistAsync(
    CloudBlobClient blobClient,
    string containerName)
{
        CloudBlobContainer container =
            blobClient.GetContainerReference(containerName);

        if (await container.CreateIfNotExistsAsync())
        {
                Console.WriteLine("Container [{0}] created.", containerName);
        }
        else
        {
                Console.WriteLine("Container [{0}] exists, skipping creation.",
                    containerName);
        }
}
```

Zodra het Hallo-containers zijn gemaakt, Hallo toepassing kan nu Hallo bestanden uploaden die wordt gebruikt door Hallo taken.

> [!TIP]
> [Hoe toouse Blob Storage in .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) biedt een goed overzicht van het werken met Azure Storage-containers en blobs. Deze moet aan de bovenkant Hallo van uw leeslijst als u met Batch begint te werken.
>
>

## <a name="step-2-upload-task-application-and-data-files"></a>Stap 2: taaktoepassings- en gegevensbestanden uploaden
![Het uploaden van taak toepassing en invoer (gegevens) bestanden toocontainers][2]
<br/>

In Hallo uploaden bewerking *DotNetTutorial* definieert eerst verzamelingen van **toepassing** en **invoer** bestandspaden die op de lokale machine Hallo zijn. Vervolgens wordt deze bestanden toohello containers die u hebt gemaakt in de vorige stap Hallo geüpload.

```csharp
// Paths toohello executable and its dependencies that will be executed by hello tasks
List<string> applicationFilePaths = new List<string>
{
    // hello DotNetTutorial project includes a project reference tooTaskApplication,
    // allowing us toodetermine hello path of hello task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// hello collection of data files that are toobe processed by hello tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload hello application and its dependencies tooAzure Storage. This is the
// application that will process hello data files, and will be executed by each
// of hello tasks on hello compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload hello data files. This is hello data that will be processed by each of
// hello tasks that are executed on hello compute nodes within hello pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

Er zijn twee methoden in `Program.cs` die betrokken zijn bij het uploadproces Hallo:

* `UploadFilesToContainerAsync`: Deze methode retourneert een verzameling [ResourceFile] [ net_resourcefile] objecten (Zie hieronder) en roept intern `UploadFileToContainerAsync` tooupload elk bestand dat wordt doorgegeven in Hallo *filePaths* parameter.
* `UploadFileToContainerAsync`: Dit is Hallo-methode die daadwerkelijk Hallo-bestand uploaden uitvoert en maakt Hallo [ResourceFile] [ net_resourcefile] objecten. Na het Hallo-bestand uploadt, het verkrijgt een shared access signature (SAS) voor het Hallo-bestand en retourneert een ResourceFile-object dat vertegenwoordigt. Ook Shared Access Signatures worden hieronder besproken.

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} toocontainer [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set hello expiry time and permissions for hello blob shared access signature.
        // In this case, no start time is specified, so hello shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct hello SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a>ResourceFiles
Een [ResourceFile] [ net_resourcefile] biedt taken in Batch met Hallo URL tooa bestand in Azure Storage dat is gedownload tooa rekenknooppunt voordat deze taak wordt uitgevoerd. Hallo [ResourceFile.BlobSource] [ net_resourcefile_blobsource] eigenschap geeft u de volledige URL Hallo van Hallo-bestand zoals dit zich in Azure Storage. Hallo-URL kan ook een shared access signature (SAS) waarmee u veilige toegang tot toohello bestand bevatten. De meeste typen taken in Batch .NET bevatten een eigenschap *ResourceFiles*, waaronder:

* [CloudTask][net_task]
* [StartTask][net_pool_starttask]
* [JobPreparationTask][net_jobpreptask]
* [JobReleaseTask][net_jobreltask]

Hallo DotNetTutorial-voorbeeldtoepassing gebruikt niet Hallo JobPreparationTask of JobReleaseTask taaktypen maar vindt u meer informatie hierover in [uitvoeren jobvoorbereidingstaken en jobvrijgevingstaken taken op Azure Batch-rekenknooppunten](batch-job-prep-release.md).

### <a name="shared-access-signature-sas"></a>Shared Access Signature (SAS)
Shared access signatures zijn tekenreeksen die, wanneer ze deel uitmaken van een URL, bieden veilige toegang toocontainers en blobs in Azure Storage. Hallo DotNetTutorial-toepassing gebruikt blobs en container shared access signature-URL en laat zien hoe deze gedeelde tooobtain vanaf toegang tot tekenreeksen Hallo Storage-service.

* **Shared access signatures voor blobs**: StartTask van Hallo pool in DotNetTutorial maakt gebruik van handtekeningen voor gedeelde blob-toegang wanneer het Hallo binaire bestanden van toepassingen en invoergegevensbestanden uit Storage downloadt (Zie stap 3 hieronder). Hallo `UploadFileToContainerAsync` methode in het DotNetTutorial `Program.cs` bevat Hallo-code die shared access signature van elke blob verkrijgt. Dit gebeurt door het aanroepen van [CloudBlob.GetSharedAccessSignature][net_sas_blob].
* **Container shared access signatures**: als elke taak zijn werk heeft verricht op Hallo rekenknooppunt, uploadt het bestand uitvoer toohello *uitvoer* container in Azure Storage. toodo dus maakt TaskApplication gebruik van een shared access signature voor containers die schrijftoegang toohello container als onderdeel van Hallo pad biedt, wanneer het Hallo-bestand wordt geüpload. Shared access signature voor het ophalen van Hallo container wordt uitgevoerd op een vergelijkbare manier als wanneer het verkrijgen van Hallo blob toegangshandtekening gedeeld. In DotNetTutorial zult u die Hallo `GetContainerSasUrl` helper methodeaanroepen [CloudBlobContainer.GetSharedAccessSignature] [ net_sas_container] toodo zodat. U moet lees meer over hoe TaskApplication Hallo container gebruikt gedeelde-toegangshandtekening in ' stap 6: taken controleren. '

> [!TIP]
> Uitchecken Hallo tweedelige reeks over handtekeningen voor gedeelde toegang [deel 1: Understanding Hallo shared access signature (SAS) model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) en [deel 2: maken en een shared access signature (SAS) gebruiken met Blob storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn meer over het opgeven van beveiligde toegang toodata in uw opslagaccount.
>
>

## <a name="step-3-create-batch-pool"></a>Stap 3: Batch-pool maken
![Een Batch-pool maken][3]
<br/>

Een Batch-**pool** is een verzameling rekenknooppunten (virtuele machines) waarop Batch de taken van een job uitvoert.

Na het uploaden van de toepassing hello en gegevens bestanden toohello Storage-account met Azure Storage-API's *DotNetTutorial* begonnen met het aanbrengen van aanroepen toohello Batch-service met API's die worden geleverd door Hallo Batch .NET-bibliotheek. Hallo code maakt eerst een [BatchClient][net_batchclient]:

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

Vervolgens Hallo voorbeeld maakt u een pool van rekenknooppunten in Hallo Batch-account met een aanroep te`CreatePoolIfNotExistsAsync`. `CreatePoolIfNotExistsAsync`maakt gebruik van Hallo [BatchClient.PoolOperations.CreatePool] [ net_pool_create] methode toocreate een nieuwe groep in Hallo Batch-service:

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create hello unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign hello StartTask that will be executed when compute nodes join hello pool.
        // In this case, we copy hello StartTask's resource files (that will be automatically downloaded
        // toohello node by hello StartTask) into hello shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for hello StartTask that copies hello task application files toothe
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need toomanually exit with a 0 for Batch toorecognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow hello specific error code PoolExists since that is expected if hello pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("hello pool {0} already existed when we tried toocreate it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

Wanneer u een pool maakt met [CreatePool][net_pool_create], u verschillende parameters zoals het aantal rekenknooppunten, Hallo Hallo [grootte van de knooppunten Hallo](../cloud-services/cloud-services-sizes-specs.md), en Hallo knooppunten besturingssysteem systeem. In *DotNetTutorial*, gebruiken we [CloudServiceConfiguration] [ net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 van [Cloudservices](../cloud-services/cloud-services-guestos-update-matrix.md). 

U kunt ook pools van rekenknooppunten die Azure Virtual Machines (VM's zijn) maken door op te geven Hallo [VirtualMachineConfiguration] [ net_virtualmachineconfiguration] voor uw toepassingen. U kunt een pool van VM-rekenknooppunten maken vanuit een Windows of [Linux-installatiekopie](batch-linux-nodes.md). Hallo-bron voor VM-installatiekopieën kan zijn:

- Hallo [Azure Virtual Machines Marketplace][vm_marketplace], waarmee u Windows- en Linux-installatiekopieën die kant-en-klare zijn. 
- Een aangepaste installatiekopie die u voorbereidt en aanlevert. Zie [Grootschalige parallelle rekenoplossingen ontwikkelen met Batch](batch-api-basics.md#pool) voor meer informatie over aangepaste installatiekopieën.

> [!IMPORTANT]
> De rekenresources in Batch worden in rekening gebracht. toominimize kosten, kunt u het verlagen `targetDedicatedComputeNodes` too1 voordat u Hallo voorbeeld uitvoert.
>
>

Samen met deze fysieke knooppunteigenschappen, kunt u ook opgeven een [StartTask] [ net_pool_starttask] voor Hallo van toepassingen. Hallo StartTask wordt uitgevoerd op elk knooppunt, zoals u dat knooppunt aan Hallo-pool wordt toegevoegd en telkens wanneer een knooppunt opnieuw wordt gestart. Hallo StartTask is vooral nuttig voor het installeren van toepassingen op compute knooppunten voorafgaande toohello uitvoering van taken. Bijvoorbeeld, als uw taken gegevens verwerken met behulp van Python-scripts, kunt u een StartTask tooinstall Python op Hallo rekenknooppunten.

In deze voorbeeldtoepassing kopieert StartTask Hallo Hallo-bestanden die het van Storage downloadt (die zijn opgegeven met behulp van Hallo [StartTask][net_starttask].[ ResourceFiles] [ net_starttask_resourcefiles] eigenschap) vanuit Hallo StartTask directory toohello gedeelde werkmap die *alle* taken op Hallo knooppunt uitgevoerd toegang hebben. In wezen Hiermee kopieert u `TaskApplication.exe` en de afhankelijkheden toohello gedeelde map in elk knooppunt zoals Hallo knooppunt lid van groep Hallo, zodat alle taken die worden uitgevoerd op Hallo-knooppunt toegang deze tot.

> [!TIP]
> Hallo **toepassingspakketten** functie van Azure Batch biedt een andere manier tooget uw toepassing op Hallo van rekenknooppunten in een pool. Zie [implementeren van toepassingen toocompute knooppunten met Batch-toepassingspakketten](batch-application-packages.md) voor meer informatie.
>
>

Opmerkelijk in bovenstaande Hallo codefragment is ook gebruik van twee omgevingsvariabelen in Hallo Hallo *CommandLine* eigenschap Hallo StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` en `%AZ_BATCH_NODE_SHARED_DIR%`. Elk rekenknooppunt in een Batch-pool wordt automatisch geconfigureerd met meerdere omgevingsvariabelen die specifiek tooBatch zijn. Een proces dat wordt uitgevoerd door een taak heeft toegang tot toothese omgevingsvariabelen.

> [!TIP]
> toofind voor meer informatie over Hallo omgevingsvariabelen die beschikbaar op rekenknooppunten in een Batch-pool en informatie over taakwerkmappen zijn, Zie Hallo [omgevingsinstellingen voor taken](batch-api-basics.md#environment-settings-for-tasks) en [bestanden en mappen ](batch-api-basics.md#files-and-directories) secties in Hallo [overzicht van de Batch-functies voor ontwikkelaars](batch-api-basics.md).
>
>

## <a name="step-4-create-batch-job"></a>Stap 4: Batch-job maken
![Een Batch-job maken][4]<br/>

Een Batch-**job** is een verzameling taken en is gekoppeld aan een pool van rekenknooppunten. Hallo-taken in een taak uitgevoerd op de rekenknooppunten van de pool Hallo die zijn gekoppeld.

U kunt een job niet alleen voor het organiseren en te volgen taken in gerelateerde workloads, maar ook voor de toepassing van bepaalde beperkingen--zoals Hallo maximale runtime voor Hallo job (en bij uitbreiding, de taken ervan) en de taakprioriteit van de in de relatie tooother taken in Batch Hallo account. In dit voorbeeld is Hallo-taak echter alleen gekoppeld aan Hallo-groep die is gemaakt in stap #3. Er worden geen aanvullende eigenschappen geconfigureerd.

Alle Batch-jobs worden gekoppeld aan een specifieke pool. Deze koppeling geeft aan welke knooppunten Hallo taken worden uitgevoerd. U geeft dit met behulp van Hallo [CloudJob.PoolInformation] [ net_job_poolinfo] eigenschap, zoals wordt weergegeven in onderstaande Hallo codefragment.

```csharp
private static async Task CreateJobAsync(
    BatchClient batchClient,
    string jobId,
    string poolId)
{
    Console.WriteLine("Creating job [{0}]...", jobId);

    CloudJob job = batchClient.JobOperations.CreateJob();
    job.Id = jobId;
    job.PoolInformation = new PoolInformation { PoolId = poolId };

    await job.CommitAsync();
}
```

Nu dat een taak is gemaakt, worden taken tooperform Hallo werk toegevoegd.

## <a name="step-5-add-tasks-toojob"></a>Stap 5: Taken toojob toevoegen
![Taken toojob toevoegen][5]<br/>
*(1) taken toohello taak worden toegevoegd, (2) Hallo taken zijn gepland toorun op knooppunten en (3) Hallo taken Hallo gegevens bestanden tooprocess downloaden*

Batch **taken** zijn Hallo afzonderlijke werkeenheden die worden uitgevoerd op Hallo van rekenknooppunten. Een taak heeft een opdrachtregel en voert Hallo scripts of uitvoerbare bestanden die u in die opdrachtregel opgeeft.

tooactually werk verrichten en taken tooa taak moeten worden toegevoegd. Elke [CloudTask] [ net_task] wordt geconfigureerd met behulp van een opdrachtregeleigenschap en [ResourceFiles] [ net_task_resourcefiles] (net als bij StartTask van Hallo pool) die Hallo taak downloadt toohello knooppunt voordat de opdrachtregel ervan automatisch wordt uitgevoerd. In Hallo *DotNetTutorial* voorbeeldproject, elke taak slechts één bestand wordt verwerkt. Hierdoor bevat de verzameling ResourceFiles één element.

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks toojob [{1}]...", inputFiles.Count, jobId);

    // Create a collection toohold hello tasks that we'll be adding toohello job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of hello tasks. Because we copied hello task application toothe
    // node's shared directory with hello pool's StartTask, we can access it via
    // hello shared directory on hello node that hello task runs on.
    foreach (ResourceFile inputFile in inputFiles)
    {
        string taskId = "topNtask" + inputFiles.IndexOf(inputFile);
        string taskCommandLine = String.Format(
            "cmd /c %AZ_BATCH_NODE_SHARED_DIR%\\TaskApplication.exe {0} 3 \"{1}\"",
            inputFile.FilePath,
            outputContainerSasUrl);

        CloudTask task = new CloudTask(taskId, taskCommandLine);
        task.ResourceFiles = new List<ResourceFile> { inputFile };
        tasks.Add(task);
    }

    // Add hello tasks as a collection, as opposed tooissuing a separate AddTask call
    // for each. Bulk task submission helps tooensure efficient underlying API calls
    // toohello Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> Wanneer ze toegang krijgen tot omgevingsvariabelen zoals `%AZ_BATCH_NODE_SHARED_DIR%` of een toepassing niet gevonden in het Hallo-knooppunt uitvoeren `PATH`, opdrachtregels taak moet worden voorafgegaan door `cmd /c`. Hiermee wordt expliciet Hallo opdrachtinterpreter uitgevoerd en krijgt deze de instructie tooterminate nadat uw opdracht is uitgevoerd. Deze vereiste is niet nodig als uw taken een toepassing in Hallo-knooppunt uitvoeren `PATH` (zoals *robocopy.exe* of *powershell.exe*) en er geen omgevingsvariabelen worden gebruikt.
>
>

Binnen Hallo `foreach` lus in bovenstaande Hallo codefragment, kunt u zien dat Hallo vanaf de opdrachtregel voor Hallo taak zodanig is opgesteld dat drie opdrachtregelargumenten te worden doorgegeven*TaskApplication.exe*:

1. Hallo **eerste argument** Hallo Hallo bestand tooprocess pad is. Dit is Hallo lokaal pad toohello bestand zoals dit zich op Hallo-knooppunt. Wanneer Hallo ResourceFile-object in `UploadFileToContainerAsync` is gemaakt, Hallo bestandsnaam voor deze eigenschap is gebruikt (als een parameter constructor ResourceFile toohello). Dit geeft aan dat Hallo-bestand kan worden gevonden in Hallo dezelfde map als *TaskApplication.exe*.
2. Hallo **tweede argument** die boven Hallo *N* woorden moeten toohello uitvoerbestand worden geschreven. In de steekproef hello, dit in code vastgelegd zodat de eerste drie woorden Hallo toohello uitvoerbestand worden geschreven.
3. Hallo **derde argument** is Hallo shared access signature (SAS) die schrijftoegang toohello biedt **uitvoer** container in Azure Storage. *TaskApplication.exe* gebruikt deze shared access signature-URL wanneer het Hallo uitvoer bestand tooAzure Storage uploadt. U vindt Hallo code voor deze in Hallo `UploadFileToContainer` methode in Hallo TaskApplication project `Program.cs` bestand:

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference toohello container using hello SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload hello file (as a new blob) toohello container
        try
        {
                CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
                blob.UploadFromFile(filePath);

                Console.WriteLine("Write operation succeeded for SAS URL " + containerSas);
                Console.WriteLine();
        }
        catch (StorageException e)
        {

                Console.WriteLine("Write operation failed for SAS URL " + containerSas);
                Console.WriteLine("Additional error information: " + e.Message);
                Console.WriteLine();

                // Indicate that a failure has occurred so that when hello Batch service
                // sets hello CloudTask.ExecutionInformation.ExitCode for hello task that
                // executed this application, it properly indicates that there was a
                // problem with hello task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a>Stap 6: taken controleren
![Taken controleren][6]<br/>
*Hallo client-toepassing (1) monitors Hallo taken voor de status voltooid en geslaagd en (2) Hallo taken uploaden resultaat gegevens tooAzure opslag*

Wanneer taken zijn tooa taak toegevoegd, worden ze automatisch in de wachtrij geplaatst en gepland voor uitvoering op rekenknooppunten in die zijn gekoppeld aan taak Hallo Hallo-pool. Batch verwerkt op basis van het Hallo-instellingen die u opgeeft, alle taak queuing, planning, opnieuw uit te voeren en andere taakbeheerverrichtingen voor u.

Er zijn veel manieren toomonitoring uitvoering van de taak. DotNetTutorial toont een eenvoudig voorbeeld waarbij alleen wordt gerapporteerd bij voltooiing en wanneer de taak mislukt of slaagt. Binnen Hallo `MonitorTasks` methode in het DotNetTutorial `Program.cs`, zijn er drie Batch .NET-concepten die discussies garanderen. Ze worden hieronder weergegeven in de volgorde waarin ze voorkomen:

1. **ODATADetailLevel**: [ODATADetailLevel][net_odatadetaillevel] opgeven in lijstbewerkingen (zoals het verkrijgen van een lijst met taken van een job) is essentieel om Batch-toepassingen goed te laten presteren. Voeg [hello Azure Batch-service efficiënt Query](batch-efficient-list-queries.md) tooyour leeslijst als u van plan bent een of andere vorm van controle van de status binnen uw Batch-toepassingen.
2. **TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] biedt Batch .NET-toepassingen met Help-hulpprogramma's voor het controleren van taakstatuswaarden. In `MonitorTasks`, *DotNetTutorial* wacht tot alle taken tooreach [TaskState.Completed] [ net_taskstate] binnen een tijdslimiet. Vervolgens wordt de taak Hallo beëindigd.
3. **TerminateJobAsync**: een taak met beëindigd [JobOperations.TerminateJobAsync] [ net_joboperations_terminatejob] (of Hallo blokkering JobOperations.TerminateJob) die taak wordt gemarkeerd als voltooid. Het is essentieel toodo dus als uw Batch-oplossing maakt gebruik van een [JobReleaseTask][net_jobreltask]. Dit is een speciaal type taak, dat wordt beschreven in [Job preparation and completion tasks](batch-job-prep-release.md) (Jobvoorbereidings- en jobvoltooiingstaken).

Hallo `MonitorTasks` methode van *DotNetTutorial*van `Program.cs` wordt hieronder weergegeven:

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed tooreach hello Completed state within hello timeout period.";

    // Obtain hello collection of tasks currently managed by hello job. Note that we use
    // a detail level too specify that only hello "id" property of each task should be
    // populated. Using a detail level for all list operations helps toolower
    // response time from hello Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor toomonitor hello state of our tasks. In this case, we
    // will wait for all tasks tooreach hello Completed state.
    TaskStateMonitor taskStateMonitor
        = batchClient.Utilities.CreateTaskStateMonitor();

    try
    {
        await taskStateMonitor.WhenAll(tasks, TaskState.Completed, timeout);
    }
    catch (TimeoutException)
    {
        await batchClient.JobOperations.TerminateJobAsync(jobId, failureMessage);
        Console.WriteLine(failureMessage);
        return false;
    }

    await batchClient.JobOperations.TerminateJobAsync(jobId, successMessage);

    // All tasks have reached hello "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property tooensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update hello detail level toopopulate only hello task id and executionInfo
    // properties. We refresh hello tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate hello task's properties with hello latest info from hello Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with hello task. It is important toonote that
            // hello task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that hello application executed by hello task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within hello specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a>Stap 7: taakuitvoer downloaden
![Taakuitvoer downloaden uit Storage][7]<br/>

Nu dat hello taak is voltooid, kan Hallo-uitvoer van Hallo taken worden gedownload uit Azure Storage. Hierbij wordt een aanroep te`DownloadBlobsFromContainerAsync` in *DotNetTutorial*van `Program.cs`:

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference tooa previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all hello block blobs in hello specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference toohello current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents tooa file in hello specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded too{0}", directoryPath);
}
```

> [!NOTE]
> Hallo aanroep te`DownloadBlobsFromContainerAsync` in Hallo *DotNetTutorial* toepassing geeft aan dat Hallo-bestanden gedownloade tooyour moeten `%TEMP%` map. Gratis toomodify van mening bent dat dit locatie uitvoer.
>
>

## <a name="step-8-delete-containers"></a>Stap 8: containers verwijderen
Omdat u in rekening voor gegevens die zich in Azure Storage bevindt gebracht, maar het is altijd een goed idee tooremove blobs die niet langer nodig zijn voor uw Batch-taken. In het DotNetTutorial `Program.cs`, dit wordt gedaan met drie aanroepen toohello Help-methode `DeleteContainerAsync`:

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

Hallo-methode zelf krijgt alleen een verwijzing toohello-container en roept vervolgens [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:

```csharp
private static async Task DeleteContainerAsync(
    CloudBlobClient blobClient,
    string containerName)
{
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);

    if (await container.DeleteIfExistsAsync())
    {
        Console.WriteLine("Container [{0}] deleted.", containerName);
    }
    else
    {
        Console.WriteLine("Container [{0}] does not exist, skipping deletion.",
            containerName);
    }
}
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a>Stap 9: Hallo job en Hallo pool verwijderen
In de laatste stap hello bent u na vragen aan gebruiker toodelete Hallo taak en Hallo van toepassingen die zijn gemaakt door de DotNetTutorial-toepassing hello. Hoewel jobs en taken zelf niet in rekening worden gebracht, worden rekenknooppunten *wel* in rekening gebracht. Daarom is het raadzaam om knooppunten alleen toe te wijzen als dat nodig is. Het verwijderen van ongebruikte pools kan een onderdeel zijn van uw onderhoudsprocedure.

Hallo BatchClient van [JobOperations] [ net_joboperations] en [PoolOperations] [ net_pooloperations] hebben beide overeenkomstige verwijderingsmethoden, die worden aangeroepen wanneer Hallo gebruiker de verwijdering bevestigt:

```csharp
// Clean up hello resources we've created in hello Batch account if hello user so chooses
Console.WriteLine();
Console.WriteLine("Delete job? [yes] no");
string response = Console.ReadLine().ToLower();
if (response != "n" && response != "no")
{
    await batchClient.JobOperations.DeleteJobAsync(JobId);
}

Console.WriteLine("Delete pool? [yes] no");
response = Console.ReadLine();
if (response != "n" && response != "no")
{
    await batchClient.PoolOperations.DeletePoolAsync(PoolId);
}
```

> [!IMPORTANT]
> Houd er rekening mee dat rekenresources in rekening worden gebracht. Door ongebruikte pools te verwijderen, beperkt u uw kosten tot een minimum. Let op dat een pool verwijdert alle rekenknooppunten in die groep en dat alle gegevens op Hallo knooppunten kunnen niet worden teruggezet nadat het Hallo-pool wordt verwijderd.
>
>

## <a name="run-hello-dotnettutorial-sample"></a>Voer Hallo *DotNetTutorial* voorbeeld
Wanneer u de voorbeeldtoepassing Hallo uitvoert, worden Hallo console-uitvoer vergelijkbare toohello volgende. Tijdens het uitvoeren, wordt er op een pauze `Awaiting task completion, timeout in 00:30:00...` terwijl de rekenknooppunten van Hallo pool worden gestart. Gebruik Hallo [Azure-portal] [ azure_portal] toomonitor uw pool, rekenknooppunten, job en taken tijdens en na de uitvoering. Gebruik Hallo [Azure-portal] [ azure_portal] of Hallo [Azure Opslagverkenner] [ storage_explorers] tooview Hallo Storage-resources (containers en blobs) die zijn gemaakt door de toepassing hello.

Uitvoeringstijd doorgaans **ongeveer 5 minuten** wanneer u Hallo toepassing uitvoert in de standaardconfiguratie.

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe toocontainer [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll toocontainer [application]...
Uploading file ..\..\taskdata1.txt toocontainer [input]...
Uploading file ..\..\taskdata2.txt toocontainer [input]...
Uploading file ..\..\taskdata3.txt toocontainer [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks toojob [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within hello specified timeout period.
Downloading all files from container [output]...
All files downloaded tooC:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a>Volgende stappen
Gratis toomake wijzigingen te denken*DotNetTutorial* en *TaskApplication* tooexperiment met andere compute-scenario's. Probeer bijvoorbeeld een uitvoeringsvertraging te toevoegen*TaskApplication*, bijvoorbeeld net als bij [Thread.Sleep][net_thread_sleep], toosimulate langlopende taken en deze in de portal Hallo controleren. Probeer meer taken toe te voegen of Hallo aantal rekenknooppunten aan te passen. Voeg logica toocheck voor en Hallo gebruik van een bestaande groep toospeed uitvoeringstijd toestaan (*hint*: Bekijk `ArticleHelpers.cs` in Hallo [Microsoft.Azure.Batch.Samples.Common] [ github_samples_common] project in [azure-batch-samples][github_samples]).

Nu u bekend bent met de basiswerkstroom Hallo van een Batch-oplossing, is het tijd toodig in toohello aanvullende functies van Hallo Batch-service.

* Bekijk Hallo [overzicht van Azure Batch-functies](batch-api-basics.md) artikel, waarin het is raadzaam als je nieuwe toohello-service.
* Start op de andere artikelen Batch-ontwikkeling onder Hallo **Development in-depth** in Hallo [Batch-leertraject][batch_learning_path].
* Bekijk een andere implementatie van de verwerking van de workload Hallo 'eerste N woorden' met behulp van Batch in Hallo [TopNWords] [ github_topnwords] voorbeeld.
* Bekijk Hallo Batch .NET [release-opmerkingen](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) voor de meest recente wijzigingen in de bibliotheek Hallo Hallo.

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[github_dotnettutorial]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/DotNetTutorial
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_common]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/Common
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[net_api]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[net_api_storage]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudblobclient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobclient.aspx
[net_cloudblobcontainer]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudserviceconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudserviceconfiguration.aspx
[net_container_delete]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteifexistsasync.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_poolinfo]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.protocol.models.cloudjob.poolinformation.aspx
[net_joboperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.joboperations
[net_joboperations_terminatejob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_jobpreptask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_jobreltask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_odatadetaillevel]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_pooloperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.pooloperations
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_resourcefile_blobsource]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.blobsource.aspx
[net_sas_blob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblob.getsharedaccesssignature.aspx
[net_sas_container]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblobcontainer.getsharedaccesssignature.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.resourcefiles.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_task_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.resourcefiles.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_taskstatemonitor]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskstatemonitor.aspx
[net_thread_sleep]: https://msdn.microsoft.com/library/274eh01d(v=vs.110).aspx
[net_virtualmachineconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.virtualmachineconfiguration.aspx
[nuget_packagemgr]: https://docs.nuget.org/consume/installing-nuget
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build
[storage_explorers]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/vs/
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-dotnet-get-started/batch_workflow_01_sm.png "Containers maken in Azure Storage"
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "Het uploaden van taak toepassing en invoer (gegevens) bestanden toocontainers"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Batch-pool maken"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Batch-job maken"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "Taken toojob toevoegen"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "Taken controleren"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Taakuitvoer downloaden uit Storage"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Werkstroom van de Batch-oplossing (volledige diagram)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "Batch-referenties in Portal"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "Storage-referenties in Portal"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Werkstroom van de Batch-oplossing (minimaal diagram)"
