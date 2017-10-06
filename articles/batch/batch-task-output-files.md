---
title: taak aaaPersist en uitvoer tooAzure opslag Hello Azure Batch service API | Microsoft Docs
description: Meer informatie over hoe toopersist Batch-taak toouse API van Batch-service en de taak uitvoer tooAzure opslag.
services: batch
author: tamram
manager: timlt
editor: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.openlocfilehash: 71b3f7c0dda2d2a9d8eb3eef83229873c70ca22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="persist-task-data-tooazure-storage-with-hello-batch-service-api"></a>Taak gegevens tooAzure opslag Hello API van Batch-service behouden

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Hallo API van Batch-service ondersteunt persistent maken uitvoer gegevens tooAzure opslag voor taken en jobbeheertaken die worden uitgevoerd op de groepen met virtuele-machineconfiguratie Hallo vanaf 2017-05-01-versie. Wanneer u een taak toevoegt, kunt u een container in Azure Storage als Hallo bestemming voor Hallo taakuitvoer. Hallo Batch-service schrijft vervolgens een uitvoer-gegevenscontainer toothat wanneer Hallo-taak voltooid is.

Een voordeel toousing Hallo Batch service API toopersist de taakuitvoer is dat u hoeft niet toomodify Hallo toepassing die Hallo taak wordt uitgevoerd. In plaats daarvan met enkele eenvoudige wijzigingen tooyour-clienttoepassing, u kunt deze persistent maken van de taak van het Hallo-uitvoer van Hallo-code die Hallo taak maakt.   

## <a name="when-do-i-use-hello-batch-service-api-toopersist-task-output"></a>Wanneer kan ik de uitvoer van de taak toopersist Hallo API van Batch-service gebruiken?

Azure Batch voorziet in meer dan een manier toopersist taakuitvoer. Met behulp van Hallo API van Batch-service is een handige benadering die wordt aanbevolen geschikt toothese-scenario's:

- Wilt u toowrite code toopersist taakuitvoer uit vanuit de clienttoepassing zonder te wijzigen Hallo-toepassing die de taak wordt uitgevoerd.
- Wilt u toopersist uitvoer van de Batch-taken en jobbeheertaken in groepen die zijn gemaakt met de Hallo Virtuele-machineconfiguratie.
- Wilt u toopersist uitvoer tooan Azure Storage-container met een willekeurige naam.
- Gewenste toopersist uitvoer tooan Azure Storage-container met de naam volgens toohello [Batch bestand conventies standaard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). 

Als uw scenario van die verschilt hierboven zijn vermeld, moet u mogelijk een andere benadering tooconsider. Bijvoorbeeld, Hallo Batch-service API ondersteunt momenteel geen streaming uitvoer tooAzure opslag terwijl Hallo-taak wordt uitgevoerd. toostream uitvoert, kunt u overwegen Hallo Batch bestand conventies bibliotheek, beschikbaar voor .NET. Voor andere talen moet u tooimplement uw eigen oplossing. Zie voor meer informatie over andere opties voor het persistent maken van de taakuitvoer [Persist taak en uitvoer tooAzure opslag](batch-task-output.md). 

## <a name="create-a-container-in-azure-storage"></a>Een container maken in Azure Storage

toopersist taak uitvoer tooAzure opslag, moet u een container die als bestemming voor de uitvoerbestanden Hallo fungeert toocreate. Hallo-container maken voordat u uw taak, bij voorkeur uitvoeren voordat het verzenden van de taak. toocreate hello container, gebruik Hallo juiste Azure Storage-clientbibliotheek of SDK. Zie voor meer informatie over Azure Storage-API's, Hallo [documentatie bij Azure Storage](https://docs.microsoft.com/azure/storage/).

Bijvoorbeeld: als u uw toepassing in C# schrijft, hello gebruiken [Azure Storage-clientbibliotheek voor .NET](https://www.nuget.org/packages/WindowsAzure.Storage/). Hallo volgende voorbeeld wordt getoond hoe toocreate een container:

```csharp
CloudBlobContainer container = storageAccount.CreateCloudBlobClient().GetContainerReference(containerName);
await conainer.CreateIfNotExists();
```

## <a name="get-a-shared-access-signature-for-hello-container"></a>Een shared access signature voor Hallo container ophalen

Nadat u Hallo-container gemaakt, krijgen een shared access signature (SAS) met schrijftoegang toohello container. Een SAS biedt gedelegeerde toegang toohello container. Hallo SAS verleent toegang met een opgegeven set machtigingen en via een opgegeven tijdsinterval. Hallo Batch-service moet een SAS met schrijven machtigingen toowrite taak uitvoer toohello container. Zie voor meer informatie over SAS [gedeelde handtekeningen voor toegang \(SAS\) in Azure Storage](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

Als u een SAS met hello Azure Storage-API's krijgt, retourneert Hallo API een tekenreeks van SAS-token. Deze tekenreeks token bevat alle parameters Hallo SAS, met inbegrip van Hallo machtigingen en hello-interval via welke Hallo SAS geldig is. toouse hello SAS tooaccess een container in Azure Storage, moet u tooappend Hallo SAS-token tekenreeks toohello resource-URI. Hallo resource-URI, samen met de Hallo toegevoegd SAS-token, biedt geverifieerde toegang tooAzure opslag.

Hallo volgende voorbeeld ziet u hoe tooget een alleen-schrijven SAS-tekenreeks voor de container Hallo token en vervolgens voegt Hallo SAS toohello container URI:

```csharp
string containerSasToken = container.GetSharedAccessSignature(new SharedAccessBlobPolicy()
{
    SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddDays(1),
    Permissions = SharedAccessBlobPermissions.Write
});

string containerSasUrl = container.Uri.AbsoluteUri + containerSasToken; 
```

## <a name="specify-output-files-for-task-output"></a>Uitvoerbestanden voor de uitvoer van de taak opgeven

een verzameling van de uitvoerbestanden toospecify voor een taak maken [uitvoerbestand](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile) objecten en toe te wijzen toohello [CloudTask.OutputFiles](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudtask.outputfiles#Microsoft_Azure_Batch_CloudTask_OutputFiles) eigenschap als Hallo-taak gemaakt. 

Hallo volgende .NET codevoorbeeld maakt een taak die u willekeurige getallen tooa bestand met de naam schrijft `output.txt`. Hallo voorbeeld maakt u een bestand voor uitvoer voor `output.txt` toobe toohello container geschreven. Hallo voorbeeld maakt ook uitvoerbestanden voor alle logboekbestanden die overeenkomen met het bestandspatroon Hallo `std*.txt` (_bijvoorbeeld_, `stdout.txt` en `stderr.txt`). Hallo container URL vereist eerder Hallo SA's dat is gemaakt voor Hallo-container. Hallo Batch-service Hallo SAS tooauthenticate toegang toohello container gebruikt: 

```csharp
new CloudTask(taskId, "cmd /v:ON /c \"echo off && set && (FOR /L %i IN (1,1,100000) DO (ECHO !RANDOM!)) > output.txt\"")
{
    OutputFiles = new List<OutputFile>
    {
        new OutputFile(
            filePattern: @"..\std*.txt",
            destination: new OutputFileDestination(
         new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId)),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
        new OutputFile(
            filePattern: @"output.txt",
            destination: 
         new OutputFileDestination(new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId + @"\output.txt")),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
}
```

### <a name="specify-a-file-pattern-for-matching"></a>Geef een patroon voor overeenkomende

Wanneer u een uitvoerbestand opgeeft, kunt u Hallo [OutputFile.FilePattern](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile.filepattern#Microsoft_Azure_Batch_OutputFile_FilePattern) eigenschap toospecify een patroon voor overeenkomende. Hallo bestandspatroon mogelijk overeen met nul bestanden, één bestand of een set bestanden die zijn gemaakt door Hallo-taak.

Hallo **FilePattern** eigenschap ondersteunt standaard bestandssysteem jokertekens zoals `*` (voor niet-recursieve komt overeen met) en `**` (voor recursieve komt overeen met). Hallo-codevoorbeeld bovenstaande geeft bijvoorbeeld Hallo bestand patroon toomatch `std*.txt` niet-recursief: 

`filePattern: @"..\std*.txt"`

een bestandspatroon tooupload één bestand opgeven met geen jokertekens. Hallo-codevoorbeeld bovenstaande geeft bijvoorbeeld Hallo bestand patroon toomatch `output.txt`:

`filePattern: @"output.txt"`

### <a name="specify-an-upload-condition"></a>Geef een voorwaarde uploaden

Hallo [OutputFileUploadOptions.UploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileuploadoptions.uploadcondition#Microsoft_Azure_Batch_OutputFileUploadOptions_UploadCondition) eigenschap toestaat uitvoerbestanden voorwaardelijke worden geüpload. Een gebruikelijk scenario is een reeks bestanden als Hallo taak lukt tooupload en een andere set van bestanden als deze uitvalt. U kunt de uitgebreide logboekbestanden tooupload bijvoorbeeld wanneer Hallo taak mislukt en wordt afgesloten met de afsluitcode van een andere waarde dan nul. Op deze manier kunt u bestanden met tooupload resultaten alleen als Hallo-taak is voltooid, omdat deze bestanden mogelijk ontbreken of zijn onvolledig als Hallo taak mislukt.

Hallo bovenstaande codevoorbeeld ingesteld Hallo **UploadCondition** eigenschap te**TaskCompletion**. Deze instelling geeft aan dat bestand Hallo toobe nadat Hallo taken is voltooid, ongeacht het Hallo-waarde van de afsluitcode Hallo geüpload. 

`uploadCondition: OutputFileUploadCondition.TaskCompletion`

Zie voor andere instellingen Hallo [OutputFileUploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.common.outputfileuploadcondition) enum.

### <a name="disambiguate-files-with-hello-same-name"></a>Bestanden met Hallo heffen dezelfde naam

Hallo-taken in een taak kunnen leiden tot bestanden die Hallo hebben dezelfde naam. Bijvoorbeeld: `stdout.txt` en `stderr.txt` worden gemaakt voor elke taak die in een taak wordt uitgevoerd. Omdat elke taak wordt uitgevoerd in een eigen context, zijn deze bestanden niet in conflict op Hallo van het knooppunt bestandssysteem. Tijdens het uploaden van bestanden van meerdere taken tooa gedeelde container hebt u echter toodisambiguate bestanden met Hallo nodig dezelfde naam.

Hallo [OutputFileBlobContainerDestination.Path](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination.path#Microsoft_Azure_Batch_OutputFileBlobContainerDestination_Path) -eigenschap geeft op Hallo bestemmings-blob of virtuele map voor uitvoerbestanden. U kunt Hallo **pad** eigenschap tooname Hallo blob of virtuele map zodanig dat de uitvoerbestanden Hello dezelfde naam een unieke naam op basis van Azure Storage. Hallo taak-ID in het Hallo-pad is een uitstekende manier tooensure unieke namen en eenvoudig bestanden te identificeren.

Als hello **FilePattern** eigenschap tooa de jokertekenexpressie is ingesteld, wordt alle bestanden die overeenkomen met Hallo patroon zijn geüploade toohello virtuele map die is opgegeven door Hallo **pad** eigenschap. Bijvoorbeeld, als hello container is `mycontainer`, Hallo-taak-ID is `mytask`, en het bestandspatroon Hallo `..\std*.txt`, vervolgens Hallo absolute URI's toohello uitvoerbestanden in Azure Storage vergelijkbaar met is:

```
https://myaccount.blob.core.windows.net/mycontainer/mytask/stderr.txt
https://myaccount.blob.core.windows.net/mycontainer/mytask/stdout.txt
```

Als hello **FilePattern** eigenschap set toomatch één bestandsnaam, wat betekent dat deze geen jokertekens bevat geen waarde van Hallo vervolgens Hallo **pad** -eigenschap geeft op Hallo volledig gekwalificeerde blob-naam . Als u naamconflicten met één bestand uit meerdere taken verwacht, neem Hallo-naam van de virtuele map Hallo als onderdeel van Hallo bestand naam toodisambiguate die bestanden. Bijvoorbeeld: set Hallo **pad** eigenschap tooinclude Hallo taak-ID, Hallo scheidingsteken (meestal een slash) en Hallo-bestandsnaam:

`path: taskId + @"/output.txt"`

Hallo absolute URI's toohello uitvoerbestanden voor een aantal taken zijn vergelijkbaar met:

```
https://myaccount.blob.core.windows.net/mycontainer/task1/output.txt
https://myaccount.blob.core.windows.net/mycontainer/task2/output.txt
```

Zie voor meer informatie over virtuele mappen in Azure Storage [lijst Hallo blobs in een container](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container).


## <a name="diagnose-file-upload-errors"></a>Bestand uploadfouten opsporen

Als uitvoer uploaden van bestanden tooAzure opslag mislukt Hallo taak en gaat vervolgens toohello **voltooid** status en Hallo [TaskExecutionInformation.FailureInformation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.taskexecutioninformation.failureinformation#Microsoft_Azure_Batch_TaskExecutionInformation_FailureInformation) eigenschap is ingesteld. Hallo onderzoeken **FailureInformation** eigenschap toodetermine welke fout is opgetreden. Dit is bijvoorbeeld een fout die tijdens het bestand uploaden optreedt als Hallo container kan niet worden gevonden: 

```
Category: UserError
Code: FileUploadContainerNotFound
Message: One of hello specified Azure container(s) was not found while attempting tooupload an output file
```

Op elke uploaden bestand Batch schrijft twee bestanden toohello rekenknooppunt, meld `fileuploadout.txt` en `fileuploaderr.txt`. U kunt deze informatie over een specifieke fout logboek bestanden toolearn onderzoeken. In gevallen waarbij Hallo-bestand uploaden is nooit uitgevoerd, bijvoorbeeld omdat het Hallo-taak zelf kan niet worden uitgevoerd, klikt u vervolgens bestaat deze logboekbestanden niet.

## <a name="diagnose-file-upload-performance"></a>Bestand uploaden van prestaties vaststellen

Hallo `fileuploadout.txt` bestand uploadvoortgang registreert. U kunt dit bestand toolearn meer informatie over hoe lang het bestand uploadt duurt onderzoeken. Houd er rekening mee dat er veel factoren tooupload prestaties zijn, waaronder Hallo grootte van andere activiteiten op Hallo knooppunt Hallo gelijktijdig met het uploaden van het Hallo-Hallo knooppunt of Hallo doelcontainer in Hallo dezelfde regio bevinden als de Batch-pool hello, hoeveel knooppunten zijn uploaden van de opslagaccount toohello op Hallo dezelfde tijd, enzovoort.

## <a name="use-hello-batch-service-api-with-hello-batch-file-conventions-standard"></a>Hallo Batch-service API Hello Batch bestand conventies standaard gebruiken

Wanneer u de uitvoer van de taak met Batch-service API Hallo zich blijven voordoen, kunt u uw doelcontainer kunt naam en gewenste echter blobs. U kunt ook tooname ze volgens toohello [Batch bestand conventies standaard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). Hallo bestand conventies standaard bepaalt Hallo namen van de doelcontainer Hallo en voor een bepaalde uitvoerbestand op basis van Hallo namen van de taak hello en in Azure Storage-blob. Als u Hallo bestand conventies standaard gebruikt voor het benoemen van uitvoerbestanden, wordt de uitvoerbestanden beschikbaar voor weergave in Hallo zijn [Azure-portal](https://portal.azure.com).

Als u in C# ontwikkelt, kunt u Hallo-methoden die zijn ingebouwd in Hallo [bestand conventies van Batch-bibliotheek voor .NET](https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files). Deze bibliotheek maakt Hallo goed containers en blobs paden voor u met de naam. U kunt bijvoorbeeld Hallo API tooget Hallo juiste naam voor het Hallo-container, op basis van de taaknaam Hallo aanroepen:

```csharp
string containerName = job.OutputStorageContainerName();
```

U kunt Hallo [CloudJobExtensions.GetOutputStorageContainerUrl](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files.cloudjobextensions.getoutputstoragecontainerurl) tooreturn methode een shared access signature (SAS)-URL die gebruikte toowrite toohello container is. Vervolgens kunt u deze SAS-toohello doorgeven [OutputFileBlobContainerDestination](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination) constructor.

Als u in een andere taal dan C# ontwikkelt, moet u tooimplement Hallo bestand conventies standaard zelf.

## <a name="code-sample"></a>Codevoorbeeld

Hallo [PersistOutputs] [ github_persistoutputs] voorbeeldproject is een van de Hallo [Azure Batch-codevoorbeelden] [ github_samples] op GitHub. Deze Visual Studio-oplossing laat zien hoe toouse Hallo Batch-clientbibliotheek voor .NET toopersist taak toodurable opslag uitvoer. toorun hello steekproef, als volgt te werk:

1. Open Hallo-project in **Visual Studio 2015 of hoger**.
2. Toevoegen van uw Batch- en Storage **accountreferenties** te**AccountSettings.settings** hello Microsoft.Azure.Batch.Samples.Common project.
3. **Bouwen** (maar niet worden uitgevoerd) Hallo oplossing. Herstel alle NuGet-pakketten als daarom wordt gevraagd.
4. Gebruik hello Azure portal tooupload een [toepassingspakket](batch-application-packages.md) voor **PersistOutputsTask**. Hallo omvatten `PersistOutputsTask.exe` en afhankelijke assembly's in Hallo ZIP-pakket, set Hallo toepassings-ID te 'PersistOutputsTask' en de toepassing hello Pakketversie te "1.0".
5. **Start** (uitvoeren) Hallo **PersistOutputs** project.
6. Wanneer de vraag toochoose Hallo persistentie technologie toouse voor actieve Hallo voorbeeld invoert **2** toorun Hallo voorbeeld met behulp van de uitvoer van de taak toopersist Hallo API van Batch-service.
7. Indien gewenst, Hallo voorbeeld opnieuw uitvoeren, voeren **3** toopersist uitvoer met Hallo Batch-service API en tooname Hallo-container en blob doelpad volgens toohello bestand conventies standaard.

## <a name="next-steps"></a>Volgende stappen

- Zie voor meer informatie over persistent maken van de taakuitvoer met Hallo bestand Conventions-bibliotheek voor .NET [behouden van de taak en gegevens tooAzure opslag met Hallo Batch bestand Conventions-bibliotheek voor .NET toopersist ](batch-task-output-file-conventions.md).
- Zie voor informatie over andere benaderingen voor persistent maken uitvoergegevens in Azure Batch, [Persist taak en uitvoer tooAzure opslag](batch-task-output.md).

[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
