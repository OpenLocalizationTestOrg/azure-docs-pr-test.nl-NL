---
title: aangepaste activiteiten in een Azure Data Factory-pijplijn aaaUse
description: Meer informatie over hoe toocreate aangepaste activiteiten en deze gebruiken in een Azure Data Factory-pijplijn.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 23e33727b2160541ab40938ffd911fdd484b3daa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a>Use custom activities in an Azure Data Factory pipeline (Aangepaste activiteiten gebruiken in een Azure Data Factory-pijplijn)

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive-activiteit](data-factory-hive-activity.md) 
> * [Pig-activiteit](data-factory-pig-activity.md)
> * [MapReduce-activiteit](data-factory-map-reduce.md)
> * [Hadoop-Streamingactiviteit](data-factory-hadoop-streaming-activity.md)
> * [Spark-activiteit](data-factory-spark.md)
> * [Machine Learning-batchuitvoeringsactiviteit](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning-activiteit resources bijwerken](data-factory-azure-ml-update-resource-activity.md)
> * [Opgeslagen procedureactiviteit](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL-activiteit](data-factory-usql-activity.md)
> * [Aangepaste activiteit .NET](data-factory-use-custom-activities.md)

Er zijn twee soorten activiteiten die u in een Azure Data Factory-pijplijn gebruiken kunt.

- [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) toomove gegevens tussen [ondersteunde bron- en sink gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats).
- [Activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) tootransform gegevens met behulp van compute-services zoals Azure HDInsight Azure Batch en Azure Machine Learning. 

toomove gegevens van/naar een gegevensopslag die biedt geen ondersteuning voor Data Factory, maak een **aangepaste activiteit** met uw eigen gegevens gegevensverplaatsing logica en gebruik Hallo activiteit in een pijplijn. Op deze manier tootransform/proces gegevens op een manier die niet wordt ondersteund door Data Factory, een aangepaste activiteit maken met uw eigen logica van de transformatie van gegevens en Hallo-activiteit gebruiken in een pijplijn. 

U kunt een aangepaste activiteit toorun configureren op een **Azure Batch** pool van virtuele machines of een op Windows gebaseerde **Azure HDInsight** cluster. Wanneer u Azure Batch gebruikt, kunt u een bestaande Azure Batch pool. Terwijl bij gebruik van HDInsight, kunt u een bestaand HDInsight-cluster of een cluster dat automatisch wordt gemaakt voor u op aanvraag tijdens runtime.  

Hallo bevat volgende overzicht Stapsgewijze instructies voor het maken van een aangepaste .NET-activiteit en gebruik van aangepaste activiteit Hallo in een pijplijn. Hallo scenario maakt gebruik van een **Azure Batch** gekoppelde service. een Azure HDInsight toouse gekoppelde service in plaats daarvan, maakt u een gekoppelde service van het type **HDInsight** (uw eigen HDInsight-cluster) of **HDInsightOnDemand** (Data Factory maakt een HDInsight-cluster op aanvraag). Configureer vervolgens een aangepaste activiteit toouse Hallo gekoppelde HDInsight-service. Zie [gebruik Azure HDInsight gekoppelde services](#use-hdinsight-compute-service) sectie voor meer informatie over het gebruik van Azure HDInsight toorun Hallo aangepaste activiteit.

> [!IMPORTANT]
> - Hallo aangepaste .NET-activiteiten alleen op Windows gebaseerde HDInsight-clusters worden uitgevoerd. Een tijdelijke oplossing voor deze beperking is toouse Hallo kaart verminderen activiteit toorun aangepaste Java-code op een Linux gebaseerde HDInsight-cluster. Een andere optie is toouse een Azure Batch-pool van virtuele machines toorun aangepaste activiteiten in plaats van een HDInsight-cluster.
> - Het is niet mogelijk toouse een Data Management Gateway vanuit een aangepaste activiteit tooaccess on-premises-gegevensbronnen. Op dit moment [Data Management Gateway](data-factory-data-management-gateway.md) ondersteunt alleen Hallo kopieeractiviteit en de activiteit opgeslagen procedure in de Data Factory.   

## <a name="walkthrough-create-a-custom-activity"></a>Overzicht: een aangepaste activiteit maken
### <a name="prerequisites"></a>Vereisten
* Visual Studio 2012-2013-2015
* Download en installeer [Azure .NET SDK](https://azure.microsoft.com/downloads/)

### <a name="azure-batch-prerequisites"></a>Vereisten voor Azure Batch
In Hallo scenario maakt uitvoeren u uw aangepaste .NET-activiteiten met behulp van Azure Batch als een berekeningsresource. **Azure Batch** is een platform service voor het uitvoeren van grootschalige parallelle en high-performance computing (HPC) toepassingen efficiënt in Hallo cloud. Azure Batch plant toorun rekenintensief werk op een beheerde **verzameling van virtuele machines**, en kan automatisch scale compute resources toomeet Hallo behoeften van uw jobs. Zie [basisbeginselen van Azure Batch] [ batch-technical-overview] artikel voor een gedetailleerd overzicht van hello Azure Batch-service.

Hallo-zelfstudie Azure Batch-account te maken met een pool van virtuele machines. Hier volgen Hallo stappen:

1. Maak een **Azure Batch-account** met Hallo [Azure-portal](http://portal.azure.com). Zie [maken en beheren van Azure Batch-account] [ batch-create-account] artikel voor instructies.
2. Noteer hello Azure Batch-accountnaam, accountsleutel URI en de naam van de groep van toepassingen. U moet ze toocreate een gekoppelde Azure-Batch-service.
    1. Op Hallo startpagina van Azure Batch-account, ziet u een **URL** in Hallo volgende indeling: `https://myaccount.westus.batch.azure.com`. In dit voorbeeld **myaccount** Hallo naam is van hello Azure Batch-account. U in de servicedefinitie Hallo gekoppeld gebruikt-URI is Hallo URL zonder Hallo-naam van het Hallo-account. Bijvoorbeeld: `https://<region>.batch.azure.com`.
    2. Klik op **sleutels** op Hallo linkermenu en kopiëren Hallo **primaire TOEGANGSSLEUTEL**.
    3. toouse een bestaande groep, klikt u op **Pools** op Hallo menu en noteer Hallo **ID** van Hallo van toepassingen. Als u een bestaande toepassingen hebt, verplaatst u de volgende stap toohello.     
2. Maak een **Azure Batch-pool**.

   1. In Hallo [Azure-portal](https://portal.azure.com), klikt u op **Bladeren** in Hallo menu aan de linkerkant en klik op **Batch-Accounts**.
   2. Selecteer uw Azure Batch-account tooopen hello **Batch-Account** blade.
   3. Klik op **Pools** tegel.
   4. In Hallo **Pools** blade, klik op de knop toevoegen op Hallo werkbalk tooadd een pool.
      1. Geef een ID voor Hallo van toepassingen (groep-ID). Opmerking Hallo **ID van de pool Hallo**; u deze nodig hebt bij het maken van Hallo Data Factory-oplossing.
      2. Geef **Windows Server 2012 R2** voor Hallo besturingssysteemgroep instelling.
      3. Selecteer een **knooppunt prijscategorie**.
      4. Voer **2** als waarde voor Hallo **doel toegewezen** instelling.
      5. Voer **2** als waarde voor Hallo **maximum aantal taken per knooppunt** instelling.
   5. Klik op **OK** toocreate Hallo van toepassingen.
   6. Noteer Hallo **ID** van Hallo van toepassingen. 



### <a name="high-level-steps"></a>Stappen op hoog niveau
Hier volgen Hallo twee stappen op hoog niveau die u als onderdeel van dit scenario uitvoeren: 

1. Maak een aangepaste activiteit die eenvoudige transformatie/verwerking logica bevat.
2. Maak een Azure data factory met een pipeline die gebruikmaakt van Hallo aangepaste activiteit.

### <a name="create-a-custom-activity"></a>Een aangepaste activiteit maken
maken van een aangepaste activiteit .NET toocreate een **.NET Class Library** project met een klasse die die implementeert **IDotNetActivity** interface. Deze interface heeft slechts één methode: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) en de handtekening is:

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


Hallo-methode heeft vier parameters:

- **linkedServices**. Deze eigenschap is een inventariseerbare lijst van gegevensarchief gekoppelde services waarnaar wordt verwezen door een i/o-gegevenssets voor Hallo-activiteit.   
- **gegevenssets**. Deze eigenschap is een inventariseerbare lijst van i/o-gegevenssets voor Hallo-activiteit. U kunt deze parameter tooget Hallo locaties en schema's die zijn gedefinieerd door de invoer- en uitvoergegevenssets gebruiken.
- **activiteit**. Deze eigenschap vertegenwoordigt de huidige activiteit Hallo. Het kan gebruikte tooaccess uitgebreide eigenschappen die zijn gekoppeld aan de aangepaste activiteit Hallo zijn. Zie [toegang uitgebreide eigenschappen](#access-extended-properties) voor meer informatie.
- **Berichtenlogboek**. Dit object kunt u foutopsporing opmerkingen die surface schrijven in Hallo gebruikersaanmelding voor Hallo pijplijn.

Hallo-methode retourneert een woordenlijst die gebruikt toochain aangepaste activiteiten samen in de toekomst Hallo worden kan. Deze functie is nog niet geïmplementeerd, kunt u dus een woordenboek leeg retourneren van Hallo-methode.  

### <a name="procedure"></a>Procedure
1. Maak een **.NET Class Library** project.
   <ol type="a">
     <li>Start <b>Visual Studio 2017</b> of <b>Visual Studio 2015</b> of <b>Visual Studio 2013</b> of <b>Visual Studio 2012</b>.</li>
     <li>Klik op <b>bestand</b>, wijst u te<b>nieuw</b>, en klik op <b>Project</b>.</li>
     <li>Vouw <b>Templates</b> uit en selecteer <b>Visual C#</b>. In dit scenario maakt u gebruik C#, maar kunt u een .NET taal toodevelop Hallo aangepaste activiteit.</li>
     <li>Selecteer <b>Class Library</b> uit de lijst Hallo van projecttypen op Hallo rechts. Kies in de VS 2017 <b>Class Library (.NET Framework)</b> </li>
     <li>Voer <b>MyDotNetActivity</b> voor Hallo <b>naam</b>.</li>
     <li>Selecteer <b>C:\ADFGetStarted</b> voor Hallo <b>locatie</b>.</li>
     <li>Klik op <b>OK</b> toocreate Hallo project.</li>
   </ol>
2.Klik op **extra**, wijst u te**NuGet Package Manager**, en klik op **Package Manager Console**.
3. In Hallo Package Manager-Console, uitvoeren na de opdracht tooimport hello **Microsoft.Azure.Management.DataFactories**.

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. Importeren Hallo **Azure Storage** NuGet-pakket in toohello-project.

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > Data Factory-service starten vereist Hallo 4.3-versie van WindowsAzure.Storage. Als u een tooa verwijzing toevoegt latere versie van Azure Storage-assembly in uw project aangepaste activiteit er een foutbericht wanneer Hallo activiteit wordt uitgevoerd. tooresolve hello fout, Zie [Appdomain isolatie](#appdomain-isolation) sectie. 
5. Voeg de volgende Hallo **met** instructies toohello bronbestand in Hallo-project.

    ```csharp

    // Comment these lines if using VS 2017
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    // --------------------

    // Comment these lines if using <= VS 2015
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    // ---------------------

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. Hallo naam wijzigen van Hallo **naamruimte** te**MyDotNetActivityNS**.

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. Hallo-naam van de klasse Hallo te wijzigen**MyDotNetActivity** en afgeleid Hallo **IDotNetActivity** interface zoals weergegeven in het volgende codefragment Hallo:

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. Hallo implementeren (toevoegen) **Execute** methode Hallo **IDotNetActivity** interface toohello **MyDotNetActivity** klasse en kopieer Hallo voorbeeldmethode code toohello te volgen.

    Hallo telt volgende voorbeeld Hallo aantal exemplaren van Hallo zoekterm ('Microsoft') in elke blob die is gekoppeld aan een gegevenssegment.

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
    /// </summary>
    
    public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
    {
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // toolog information, use hello logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get hello input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables toohold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from hello dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and hello other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get hello first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using hello same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get hello connection string in hello linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get hello folder path from hello input dataset definition
        string folderPath = GetFolderPath(inputDataset);
        string output = string.Empty; // for use later.
    
        // create storage client for input. Pass hello connection string.
        CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
        CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
        // initialize hello continuation token before using it in hello do-while loop.
        BlobContinuationToken continuationToken = null;
        do
        {   // get hello list of input blobs from hello input storage client object.
            BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                     true,
                                     BlobListingDetails.Metadata,
                                     null,
                                     continuationToken,
                                     null,
                                     null);
    
            // Calculate method returns hello number of occurrences of
            // hello search term (“Microsoft”) in each blob associated
               // with hello data slice. definition of hello method is shown in hello next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for hello output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get hello folder path from hello output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log hello output folder path 
        logger.Write("Writing blob toohello folder: {0}", folderPath);
    
        // create a storage object for hello output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write hello name of hello file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log hello output file name
        logger.Write("output blob URI: {0}", outputBlobUri.ToString());

        // create a blob and upload hello output text.
        CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
        logger.Write("Writing {0} toohello output blob", output);
        outputBlob.UploadText(output);
    
        // hello dictionary can be used toochain custom activities together in hello future.
        // This feature is not implemented yet, so just return an empty dictionary.  
    
        return new Dictionary<string, string>();
    }
    ```
9. Hallo volgende Help-methoden toevoegen: 

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    
    private static string GetFolderPath(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }

        // get type properties of hello dataset 
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello folder path found in hello type properties
        return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.   
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }
    
        // get type properties of hello dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello blob/file name in hello type properties
        return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
        string output = string.Empty;
        logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
        foreach (IListBlobItem listBlobItem in Bresult.Results)
        {
            CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
            if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
            {
                string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
                logger.Write("input blob text: {0}", blobText);
                string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
                var matchQuery = from word in source
                                 where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                 select word;
                int wordCount = matchQuery.Count();
                output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
            }
        }
        return output;
    }
    ```

    Hallo GetFolderPath methode retourneert Hallo pad toohello map Hallo gegevensset tooand Hallo GetFileName retourneert Hallo methodenaam van Hallo-blob /-bestand dat verwijst naar gegevensset Hallo verwijst. Als u havefolderPath is gedefinieerd met behulp van de variabelen zoals {Year}, {Month}, {Day} enz., Hallo-methode retourneert Hallo tekenreeks omdat deze zonder deze te vervangen door waarden van de runtime. Zie [toegang uitgebreide eigenschappen](#access-extended-properties) sectie voor meer informatie over de toegang tot SliceStart, SliceEnd, enzovoort.    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    Hallo berekeningsmethode berekent Hallo aantal exemplaren van het sleutelwoord Microsoft in Hallo invoerbestanden (BLOB's in de map Hallo). Hallo zoekterm ('Microsoft') is vastgelegd in het Hallo-code.
10. Hallo project compileren. Klik op **bouwen** uit en klik op Hallo **Build Solution**.

    > [!IMPORTANT]
    > Stel 4.5.2 de versie van .NET Framework als doel-framework voor uw project Hallo: met de rechtermuisknop op het Hallo-project en klik op **eigenschappen** tooset Hallo doel-framework. Data Factory biedt geen ondersteuning voor aangepaste activiteiten gecompileerd met .NET Framework-versies hoger is dan 4.5.2.

11. Start **Windows Verkenner**, en te navigeren**bin\debug** of **bin\release** map afhankelijk van Hallo type build.
12. Maak een zipbestand **MyDotNetActivity.zip** die alle Hallo binaire bestanden in Hallo bevat <project folder>map \bin\Debug. Hallo omvatten **MyDotNetActivity.pdb** zodat u aanvullende informatie zoals regelnummer in de broncode Hallo die Hallo probleem veroorzaakt ophalen als er een fout is het bestand. 

    > [!IMPORTANT]
    > Alle bestanden in het zip-bestand Hallo Hallo voor Hallo aangepaste activiteit op Hallo moet **bovenste niveau** met geen submappen.

    ![Binaire uitvoerbestanden](./media/data-factory-use-custom-activities/Binaries.png)
14. Maak een blobcontainer met de naam **customactivitycontainer** als deze niet al bestaat. 
15. MyDotNetActivity.zip uploaden als een blob toohello customactivitycontainer in een **algemeen** Azure blob-opslag (geen hot/cool Blob-opslag) waarnaar wordt verwezen door AzureStorageLinkedService.  

> [!IMPORTANT]
> Als u deze .NET activiteit project tooa oplossing in Visual Studio met een Data Factory-project toevoegen en voeg een verwijzing too.NET activiteit-project uit Hallo Data Factory-toepassingsproject, hoeft u niet tooperform Hallo laatste twee stappen voor het handmatig maken Hallo zip-bestand en uploaden toohello algemeen Azure blob-opslag. Wanneer u met behulp van Visual Studio Data Factory-entiteiten publiceert, worden deze stappen automatisch uitgevoerd door Hallo publicatieproces. Zie voor meer informatie [Data Factory-project in Visual Studio](#data-factory-project-in-visual-studio) sectie.

## <a name="create-a-pipeline-with-custom-activity"></a>Een pijplijn maken met aangepaste activiteit
U hebt gemaakt van een aangepaste activiteit en geüpload Hallo zip-bestand met de binaire bestanden tooa blob-container in een **algemeen** Azure Storage-Account. In deze sectie maakt u een Azure data factory met een pipeline die gebruikmaakt van aangepaste activiteit Hallo.

Hallo invoergegevensset voor Hallo aangepaste activiteit vertegenwoordigt BLOB's (bestanden) in Hallo customactivityinput map van de container adftutorial in Hallo blob-opslag. Hallo uitvoergegevensset voor Hallo activiteit vertegenwoordigt uitvoer blobs in Hallo customactivityoutput map van de container adftutorial in Hallo blob-opslag.

Maak **bestand.txt** bestand met de Hallo volgende inhoud en te uploaden**customactivityinput** map Hallo **adftutorial** container. Hallo adftutorial container maken als deze niet al bestaat. 

```
test custom activity Microsoft test custom activity Microsoft
```

Hallo invoermap komt overeen tooa segment in Azure Data Factory, zelfs als de map Hallo twee of meer bestanden heeft. Wanneer elk segment wordt verwerkt door de pijplijn hello, doorlopen aangepaste activiteit Hallo alle Hallo blobs in de invoermap Hallo voor dat segment.

Ziet u een bestand met in Hallo adftutorial\customactivityoutput map uitvoer met een of meer regels (zelfde als aantal blobs in de invoermap Hallo):

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
```


Hier volgen Hallo stappen die u in deze sectie uitvoeren:

1. Maak een **gegevensfactory**.
2. Maak **gekoppelde services** voor hello Azure Batch-pool van virtuele machines op welke Hallo aangepaste activiteit wordt uitgevoerd en hello Azure Storage dat Hallo invoer/uitvoer-BLOB's bevat.
3. Maken van de invoer en uitvoer **gegevenssets** die invoer en uitvoer van de aangepaste activiteit Hallo staan.
4. Maak een **pijplijn** die gebruikmaakt van Hallo aangepaste activiteit.

> [!NOTE]
> Hallo maken **bestand.txt** en upload het blob-container tooa als u dat nog niet hebt gedaan. Zie de instructies in de voorgaande sectie Hallo.   

### <a name="step-1-create-hello-data-factory"></a>Stap 1: Hallo een gegevensfactory maken
1. Na het aanmelden toohello Azure-portal, Hallo stappen te volgen:
   1. Klik op **nieuw** op Hallo linkermenu.
   2. Klik op **gegevens en analyse** in Hallo **nieuw** blade.
   3. Klik op **Data Factory** op Hallo **gegevensanalyse** blade.
   
    ![Nieuwe Azure Data Factory-menu](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. In Hallo **nieuwe gegevensfactory** blade Voer **CustomActivityFactory** voor Hallo naam. Hallo-naam van hello Azure-gegevensfactory moet wereldwijd uniek zijn. Als u de foutmelding Hallo: **Data factory-naam 'CustomActivityFactory' is niet beschikbaar**, Hallo-naam van gegevensfactory Hallo wijzigen (bijvoorbeeld **yournameCustomActivityFactory**) en probeert te maken opnieuw.

    ![Nieuwe Azure Data Factory-blade](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. Klik op **RESOURCEGROEPNAAM**, en selecteer een bestaande resourcegroep of maak een resourcegroep.
4. Controleer of u Hallo juist **abonnement** en **regio** waar u Hallo data factory toobe gemaakt.
5. Klik op **maken** op Hallo **nieuwe gegevensfactory** blade.
6. Zie van Hallo gegevensfactory wordt gemaakt in Hallo **Dashboard** Hallo Azure-portal.
7. Nadat het Hallo gegevensfactory is gemaakt, ziet u de Data Factory-blade hello, waarin u inhoud van de gegevensfactory Hallo Hallo.
    
    ![Blade Gegevensfactory](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a>Stap 2: Gekoppelde services maken
Gekoppelde services worden gegevensarchieven of compute-services tooan Azure-gegevensfactory. In deze stap koppelt u uw Azure Storage-account en de Azure Batch-account tooyour data factory.

#### <a name="create-azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service maken
1. Klik op Hallo **auteur en implementeren van** tegel op Hallo **DATA FACTORY** blade voor **CustomActivityFactory**. U ziet Hallo Data Factory-Editor.
2. Klik op **nieuwe gegevensopslag** op Hallo opdrachtbalk en kies **Azure storage**. U ziet Hallo JSON-script voor het maken van een Azure Storage gekoppelde service in Hallo-editor.
    
    ![Nieuwe gegevensopslag - Azure Storage](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. Vervang `<accountname>` met de naam van uw Azure storage-account en `<accountkey>` door toegangssleutel van hello Azure storage-account. toolearn hoe tooget uw opslag toegang krijgen tot sleutel, Zie [toegangssleutels voor opslag weergeven, kopiëren en opnieuw genereren](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

    ![Azure-opslag leuk service gevonden](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gekoppelde service.

#### <a name="create-azure-batch-linked-service"></a>Azure Batch gekoppelde service maken
1. In Hallo Data Factory-Editor, klikt u op **... Meer** op de opdrachtbalk hello, klikt u op **nieuwe berekening**, en selecteer vervolgens **Azure Batch** in Hallo-menu.

    ![Nieuwe berekening - Azure Batch](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. Hallo na wijzigingen toohello JSON-script maken:

   1. Azure Batch-accountnaam voor Hallo **accountName** eigenschap. Hallo **URL** van Hallo **blade van Azure Batch-account** bevindt zich in de volgende indeling Hallo: `http://accountname.region.batch.azure.com`. Voor Hallo **batchUri** eigenschap in JSON hello, moet u tooremove `accountname.` van de URL en gebruik Hallo Hallo `accountname` voor Hallo `accountName` JSON-eigenschap.
   2. Hello Azure Batch-accountsleutel opgeven voor Hallo **accessKey** eigenschap.
   3. Hallo naam opgeven van Hallo-groep die u hebt gemaakt als onderdeel van de vereisten voor Hallo **poolName** eigenschap. U kunt ook Hallo-ID van Hallo pool in plaats van Hallo-naam van Hallo van toepassingen opgeven.
   4. Azure Batch-URI opgeven voor Hallo **batchUri** eigenschap. Voorbeeld: `https://westus.batch.azure.com`.  
   5. Geef Hallo **AzureStorageLinkedService** voor Hallo **linkedServiceName** eigenschap.

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       Voor Hallo **poolName** eigenschap, kunt u ook Hallo-ID van Hallo pool in plaats van Hallo-naam van Hallo van toepassingen opgeven.

      > [!IMPORTANT]
      > Hallo Data Factory-service biedt een optie op aanvraag geen ondersteuning voor Azure Batch als voor HDInsight. U kunt uw eigen Azure Batch-pool alleen gebruiken in een Azure data factory.   
    

### <a name="step-3-create-datasets"></a>Stap 3: Gegevenssets maken
In deze stap maakt u gegevenssets toorepresent invoer maken en uitvoergegevens.

#### <a name="create-input-dataset"></a>Invoergegevensset maken
1. In Hallo **Editor** Hallo Data Factory, klikt u op **... Meer** op de opdrachtbalk hello, klikt u op **nieuwe gegevensset**, en selecteer vervolgens **Azure Blob storage** uit de vervolgkeuzelijst Hallo.
2. Hallo JSON in het rechterdeelvenster Hallo vervangen door Hallo volgende JSON-fragment:

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
         },
         "availability": {
             "frequency": "Hour",
             "interval": 1
         },
         "external": true,
         "policy": {}
     }
    }
    ```

   U maakt een pijplijn verderop in dit scenario met begintijd: 2016-11-16T00:00:00Z-en eindtijd: 2016-11-16T05:00:00Z. Is het geplande tooproduce gegevens elk uur, dus er vijf i/o-segmenten zijn (tussen **00**: 00:00 -> **05**: 00:00).

   Hallo **frequentie** en **interval** voor invoergegevensset hello te is ingesteld**uur** en **1**, wat betekent dat Hallo invoer segment is beschikbaar elk uur. In dit voorbeeld wordt dezelfde Hallo-bestand (bestand.txt) in Hallo intputfolder.

   Hier volgen Hallo begintijden voor elk segment, wordt vertegenwoordigd door SliceStart systeemvariabele in Hallo hierboven JSON-codefragment.
3. Klik op **implementeren** op Hallo werkbalk toocreate en implementeren van Hallo **InputDataset**. Controleer of u Hallo **tabel gemaakt met SUCCES** bericht op de titelbalk Hallo Hallo Editor.

#### <a name="create-an-output-dataset"></a>Een uitvoergegevensset maken
1. In Hallo **Data Factory-editor**, klikt u op **... Meer** op de opdrachtbalk hello, klikt u op **nieuwe gegevensset**, en selecteer vervolgens **Azure Blob storage**.
2. Hallo JSON-script in het rechterdeelvenster Hallo vervangen door Hallo volgende JSON-script:

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
                "partitionedBy": [
                    {
                        "name": "slice",
                        "value": {
                            "type": "DateTime",
                            "date": "SliceStart",
                            "format": "yyyy-MM-dd-HH"
                        }
                    }
                ]
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

     Uitvoerlocatie van de is **adftutorial/customactivityoutput/** en naam van het uitvoerbestand is jjjj-MM-dd-HH.txt waarbij JJJJ-MM-dd uu staat voor Hallo jaar, maand, datum en het uur van de Hallo-segment wordt geproduceerd. Zie [referentie voor ontwikkelaars] [ adf-developer-reference] voor meer informatie.

    Een uitvoer-blob/bestand wordt gegenereerd voor elk segment invoer. Hier ziet u hoe een bestand voor uitvoer met de naam van elk segment. Alle Hallo uitvoerbestanden worden gegenereerd in een uitvoermap: **adftutorial\customactivityoutput**.

   | Segment | Begintijd | Bestand voor uitvoer |
   |:--- |:--- |:--- |
   | 1 |2016-11-16T00:00:00 |2016-11-16-00.txt |
   | 2 |2016-11-16T01:00:00 |2016-11-16-01.txt |
   | 3 |2016-11-16T02:00:00 |2016-11-16-02.txt |
   | 4 |2016-11-16T03:00:00 |2016-11-16-03.txt |
   | 5 |2016-11-16T04:00:00 |2016-11-16-04.txt |

    Houd er rekening mee dat alle Hallo-bestanden in een invoermap deel van een segment met Hallo begintijden uitmaken hierboven vermeld. Als dit segment is verwerkt, wordt Hallo aangepaste activiteit gescand door elk bestand en resulteert in een regel in het uitvoerbestand Hallo met Hallo aantal exemplaren van zoekterm ('Microsoft'). Als er drie bestanden in Hallo inputfolder, er zijn drie regels in het uitvoerbestand Hallo voor elk segment per uur: 2016-11-16-00.txt 2016-11-16:01:00:00.txt, enzovoort.
3. Hallo toodeploy **OutputDataset**, klikt u op **implementeren** op Hallo opdrachtbalk klikken.

### <a name="create-and-run-a-pipeline-that-uses-hello-custom-activity"></a>Maken en uitvoeren van een pijplijn die gebruikmaakt van aangepaste activiteit Hallo
1. In Hallo Data Factory-Editor, klikt u op **... Meer**, en selecteer vervolgens **nieuwe pijplijn** op Hallo opdrachtbalk klikken. 
2. Hallo JSON in het rechterdeelvenster Hallo vervangen door Hallo volgende JSON-script:

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    Houd er rekening mee Hallo volgende punten:

   * **Gelijktijdigheid** te is ingesteld,**2** zodat twee segmenten parallel door 2 virtuele machines in hello Azure Batch-pool verwerkt worden.
   * Er is één activiteit in de sectie activiteiten Hallo en is van het type: **DotNetActivity**.
   * **AssemblyName** toohello naam Hallo dll-bestand dat is ingesteld: **MyDotnetActivity.dll**.
   * **EntryPoint** te is ingesteld,**MyDotNetActivityNS.MyDotNetActivity**.
   * **PackageLinkedService** te is ingesteld,**AzureStorageLinkedService** die toohello blob-opslag met Hallo aangepaste activiteit zip-bestand verwijst. Als u gebruikmaakt van andere Azure Storage-accounts voor i/o-bestanden en hello aangepaste activiteit zip-bestand, u maakt een andere gekoppelde Azure Storage-service. In dit artikel wordt ervan uitgegaan dat u hetzelfde Azure-opslagaccount Hallo.
   * **PackageFile** te is ingesteld,**customactivitycontainer/MyDotNetActivity.zip**. Het Hallo-indeling is: containerforthezip/nameofthezip.zip.
   * Hallo aangepaste activiteit wordt **InputDataset** als invoer en **OutputDataset** als uitvoer.
   * Hallo linkedServiceName eigenschap van de aangepaste activiteit Hallo verwijst toohello **AzureBatchLinkedService**, waarin u Azure Data Factory bepaald die Hallo aangepaste activiteit moet toorun op Azure Batch-VM's.
   * **isPaused** eigenschap is ingesteld, te**false** standaard. Hallo-pijplijn wordt onmiddellijk uitgevoerd in dit voorbeeld omdat Hallo segmenten te in de afgelopen Hallo starten. U kunt deze eigenschap tootrue toopause Hallo pijplijn en zijn ingesteld dat deze back-toofalse toorestart.
   * Hallo **start** tijd en **end** tijden zijn **vijf** uur uit elkaar en segmenten worden elk uur, geproduceerd zodat vijf segmenten worden geproduceerd door Hallo pijplijn.
3. toodeploy hello pipeline, klikt u op **implementeren** op Hallo opdrachtbalk klikken.

### <a name="monitor-hello-pipeline"></a>Hallo-pijplijn bewaken
1. Klik in de Data Factory-blade Hallo in hello Azure-portal, op **Diagram**.

    ![Tegel Diagram](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. Klik in de diagramweergave hello, op Hallo OutputDataset.

    ![Diagramweergave](./media/data-factory-use-custom-activities/diagram.png)
3. U ziet dat Hallo vijf uitvoer segmenten Hallo status Ready heeft zijn. Als ze zich niet in de status gereed voor hello, nog niet ze nog gemaakt. 

   ![Uitvoer segmenten](./media/data-factory-use-custom-activities/OutputSlices.png)
4. Controleer of dat de uitvoerbestanden Hallo worden gegenereerd in de blobopslag Hallo in Hallo **adftutorial** container.

   ![de uitvoer van aangepaste activiteit][image-data-factory-ouput-from-custom-activity]
5. Als u het uitvoerbestand Hallo opent, ziet u Hallo uitvoer vergelijkbare toohello volgende uitvoer:

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
    ```
6. Gebruik Hallo [Azure-portal] [ azure-preview-portal] of Azure PowerShell-cmdlets toomonitor uw gegevensfactory, pijplijnen en gegevenssets. Ziet u berichten van Hallo **ActivityLogger** in Hallo-code voor de aangepaste activiteit Hallo in Hallo-Logboeken (specifiek gebruiker-0.log) die u kunt downloaden van het Hallo-portal of met behulp van cmdlets.

   ![Logboeken downloaden van de aangepaste activiteit][image-data-factory-download-logs-from-custom-activity]

Zie [pijplijnen bewaken en beheren](data-factory-monitor-manage-pipelines.md) voor gedetailleerde stappen voor het bewaken van gegevenssets en pijplijnen.      

## <a name="data-factory-project-in-visual-studio"></a>Data Factory-project in Visual Studio  
U kunt maken en Data Factory-entiteiten publiceren met behulp van Visual Studio in plaats van Azure-portal. Voor informatie over het maken gedetailleerde en Data Factory-entiteiten publiceren met behulp van Visual Studio, Zie [bouwen van uw eerste pijplijn met Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) en [gegevens kopiëren van Azure Blob-tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) artikelen.

Hallo extra stappen te volgen als u Data Factory-project in Visual Studio maakt:
 
1. Hallo Data Factory project toohello Visual Studio-oplossing met Hallo aangepaste activiteit project toevoegen. 
2. Een verwijzing toohello .NET activiteit project uit Hallo Data Factory-project toevoegen. Met de rechtermuisknop op de Data Factory-project, wijst u te**toevoegen**, en klik vervolgens op **verwijzing**. 
3. In Hallo **verwijzing toevoegen** dialoogvenster, selecteer Hallo **MyDotNetActivity** project en klik op **OK**.
4. Bouw en Hallo oplossing publiceert.

    > [!IMPORTANT]
    > Als u Data Factory-entiteiten publiceert, een zip-bestand wordt automatisch voor u gemaakt en is toohello geüploade blob-container: customactivitycontainer. Als Hallo blob-container niet bestaat, wordt deze automatisch gemaakt te.  


## <a name="data-factory-and-batch-integration"></a>Data Factory en Batch-integratie
Hallo Data Factory-service maakt een taak in Azure Batch met de naam van de Hallo: **adf poolname: taak-xxx**. Klik op **taken** in het linkermenu Hallo. 

![Azure Data Factory - Batch-taken](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

Een taak is gemaakt voor elke activiteit uitvoering van een segment. Als er vijf segmenten gereed toobe verwerkt, worden de vijf taken gemaakt in deze taak. Als er meerdere rekenknooppunten in Hallo Batch-pool, kunnen twee of meer segmenten parallel worden uitgevoerd. Als het maximum aantal taken per Hallo compute knooppunt is ingesteld te > 1, kunnen ook hebt u meer dan één segment Hallo waarop dezelfde compute.

![Azure Data Factory - taken voor Batch-job](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

Hallo volgende diagram illustreert Hallo relatie tussen Azure Data Factory en Batch-taken.

![Data Factory & Batch](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a>Fouten oplossen
Het oplossen van problemen bestaat uit een paar eenvoudige technieken:

1. Als u de volgende fout Hallo ziet, kunt u een Hot/Cool blob-opslag in plaats van een algemene Azure blob-opslag. Hallo zip-bestand tooa uploaden **voor algemene doeleinden Azure Storage-Account**. 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of hello specified Azure Blob(s).
    ``` 
2. Als u de volgende fout Hallo ziet, bevestig de naam van die Hallo van Hallo klasse in Hallo CS komt overeen met Hallo opgegeven bestandsnaam voor Hallo **EntryPoint** eigenschap in de JSON van de Hallo-pijplijn. In Hallo-scenario is de naam van de klasse Hallo: MyDotNetActivity en Hallo ingangspunt in Hallo JSON is: MyDotNetActivityNS. **MyDotNetActivity**.

    ```
    MyDotNetActivity assembly does not exist or doesn't implement hello type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   Als het Hallo-namen komen overeen, bevestig dat alle binaire bestanden van Hallo op Hallo **hoofdmap** van Hallo zip-bestand. Dat wil zeggen, wanneer u Hallo zip-bestand opent, ziet u alle Hallo-bestanden in de hoofdmap hello, niet in alle submappen.   
3. Als invoersegment met de Hallo te niet is ingesteld**gereed**, bevestig dat de invoer mapstructuur Hallo juist is en **bestand.txt** bestaat in de invoer Hallo-mappen.
3. In Hallo **Execute** methode van uw aangepaste activiteit, gebruik Hallo **IActivityLogger** object toolog informatie die u helpt oplossen van problemen. geregistreerd Hallo-berichten weergegeven in de logboekbestanden van Hallo gebruiker (een of meer bestanden met de naam: gebruiker 0.log, gebruiker 1.log, gebruiker 2.log, enz.).

   In Hallo **OutputDataset** blade, klikt u op Hallo segment toosee hello **GEGEVENSSEGMENT** blade voor die segment. U ziet **activiteiten bij uitvoering** voor dit segment. Hier ziet u een activiteit die wordt uitgevoerd voor Hallo segment. Als u in de opdrachtbalk Hallo op uitvoeren klikt, kunt u een andere activiteit die wordt uitgevoerd voor Hallo starten hetzelfde segment.

   Wanneer u klikt op Hallo activiteit die wordt uitgevoerd, ziet u Hallo **DETAILS uitvoering van activiteit** blade met een lijst met logboekbestanden. Ziet u geregistreerde berichten in Hallo user_0.log-bestand. Wanneer er een fout optreedt, ziet u drie activiteiten bij uitvoering omdat het maximale aantal pogingen Hallo too3 in Hallo pipeline/activiteits-JSON is ingesteld. Wanneer u klikt op Hallo activiteit die wordt uitgevoerd, ziet u logboekbestanden Hallo tootroubleshoot Hallo fout kunt controleren.

   Klik in Hallo lijst van logboekbestanden op Hallo **gebruiker 0.log**. In het rechterpaneel Hallo zijn Hallo resultaten van het gebruik van Hallo **IActivityLogger.Write** methode. Als u alle berichten niet ziet, controleert u of er meer logboekbestanden met de naam: user_1.log, user_2.log enzovoort. Anders Hallo code is mogelijk niet nadat Hallo laatste bericht vastgelegd.

   Controleer daarnaast **system 0.log** voor elk systeem foutberichten en uitzonderingen.
4. Hallo omvatten **PDB** bestand in het zip-bestand Hallo zodat Hallo foutdetails beschikt over informatie zoals **aanroepstack** wanneer er een fout optreedt.
5. Alle bestanden in het zip-bestand Hallo Hallo voor Hallo aangepaste activiteit op Hallo moet **bovenste niveau** met geen submappen.
6. Zorg ervoor dat Hallo **assemblyName** (MyDotNetActivity.dll) **entryPoint**(MyDotNetActivityNS.MyDotNetActivity) **packageFile** (customactivitycontainer / MyDotNetActivity.zip) en **packageLinkedService** (toohello moet verwijzen **algemeen**Azure blob-opslag met Hallo zip-bestand) toocorrect waarden zijn ingesteld.
7. Als u een fout en wilt tooreprocess Hallo segment hebt opgelost, met de rechtermuisknop op Hallo segment Hallo **OutputDataset** blade en klik op **uitvoeren**.
8. Als u de volgende fout Hallo ziet, gebruikt u hello Azure Storage-pakket van versie > 4.3.0. Data Factory-service starten vereist Hallo 4.3-versie van WindowsAzure.Storage. Zie [Appdomain isolatie](#appdomain-isolation) sectie voor een tijdelijke oplossing als u Hallo gebruiken moet latere versie van Azure Storage-assembly. 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by hello target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    Als u Hallo 4.3.0 versie van Azure Storage-pakket gebruiken kunt, verwijdert u Hallo bestaande verwijzing tooAzure opslag pakket versie > 4.3.0. Voer vervolgens de volgende opdracht uit NuGet Package Manager Console Hallo. 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    Hallo-project maken. Assembly van versie > 4.3.0 Azure.Storage uit Hallo bin\Debug map verwijderen. Maak een zip-bestand met de binaire bestanden en Hallo PDB-bestand. Hallo oude zip-bestand vervangen door deze gegevensset in Hallo blob-container (customactivitycontainer). Voer Hallo segmenten die niet zijn geslaagd (met de rechtermuisknop op het segment en klik op uitvoeren).   
8. Hallo aangepaste activiteit gebruikt geen Hallo **app.config** bestand van het pakket. Dus als uw code wordt een verbindingsreeksen uit het Hallo-configuratiebestand gelezen, werkt het niet tijdens runtime. Hallo beste wanneer toohold met behulp van Azure Batch is geen geheimen in een **Azure KeyVault**, gebruiken een certificaat gebaseerde service principal tooprotect hello **keyvault**, en het Hallo-certificaat distribueren tooAzure Batch-pool. Hallo aangepaste activiteit .NET vervolgens toegang tot geheimen Hallo KeyVault tijdens runtime. Deze oplossing is een algemene oplossing en tooany type geheim, niet alleen verbindingsreeks kunt schalen.

   Er is een eenvoudiger tijdelijke oplossing (maar niet aanbevolen): kunt u een **Azure SQL gekoppelde service** met verbindingstekenreeksinstellingen, maken een gegevensset dat wordt gebruikt Hallo gekoppelde service en de keten Hallo dataset als een dummy invoergegevensset toohello aangepaste .NET-activiteit. U kunt vervolgens toegang Hallo van service-verbindingsreeks in Hallo aangepaste activiteitscode gekoppeld.  

## <a name="update-custom-activity"></a>Aangepaste activiteit bijwerken
Als u de code voor de aangepaste activiteit Hallo Hallo bijwerkt, samenstellen en Hallo zip-bestand met nieuwe toohello blob-opslag van de binaire bestanden uploaden.

## <a name="appdomain-isolation"></a>AppDomain-isolatie
Zie [Cross AppDomain voorbeeld](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) die laat zien u hoe toocreate een aangepaste activiteit die geen beperkte tooassembly-versies die worden gebruikt door Hallo Data Factory launcher (voorbeeld: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, enz.).

## <a name="access-extended-properties"></a>Uitgebreide eigenschappen toegang
U kunt uitgebreide eigenschappen declareren in Hallo activiteits-JSON zoals weergegeven in Hallo voorbeeld te volgen:

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


In voorbeeld hello, zijn er twee uitgebreide eigenschappen: **SliceStart** en **DataFactoryName**. Hallo-waarde voor SliceStart is gebaseerd op Hallo SliceStart systeemvariabele. Zie [systeemvariabelen](data-factory-functions-variables.md) voor een lijst met ondersteunde systeemvariabelen. Hallo-waarde voor DataFactoryName is vastgelegde tooCustomActivityFactory.

tooaccess deze uitgebreide eigenschappen in Hallo **Execute** methode gebruik code vergelijkbare toohello code te volgen:

```csharp
// tooget extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// toolog all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a>Automatische schaling van Azure Batch
U kunt ook maken met een Azure Batch-pool met **automatisch schalen** functie. U kunt bijvoorbeeld een azure batch-pool maken met 0 toegewezen virtuele machines en een formule voor automatisch schalen is op basis van Hallo aantal in behandeling zijnde taken. 

Hallo formule hier realiseert Hallo volgende gedrag: wanneer Hallo van toepassingen in eerste instantie is gemaakt, wordt 1 VM gestart. $PendingTasks metriek definieert Hallo aantal taken in uitvoering + actief (in de wachtrij) staat.  Hallo formule zoekt Hallo gemiddelde aantal in behandeling zijnde taken in Hallo afgelopen 180 seconden en dienovereenkomstig TargetDedicated ingesteld. Hiermee zorgt u ervoor dat TargetDedicated nooit zich verder uitstrekt dan 25 virtuele machines. Dus als nieuwe taken worden verzonden, pool automatisch groeit en als taken zijn voltooid, virtuele machines worden gratis één voor één en Hallo automatisch schalen die virtuele machines wordt verkleind. startingNumberOfVMs en maxNumberofVMs kunnen worden aangepast tooyour behoeften.

De formule voor automatisch schalen:

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

Zie [automatisch schalen rekenknooppunten in een Azure Batch-pool](../batch/batch-automatic-scaling.md) voor meer informatie.

Als groep Hallo Hallo standaard [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), Hallo Batch-service kan enige tijd duren 15-30 minuten tooprepare Hallo VM voordat Hallo aangepaste activiteit wordt uitgevoerd.  Als Hallo groep van een andere autoScaleEvaluationInterval gebruikmaakt, Hallo Batch-service kan enige tijd duren autoScaleEvaluationInterval + 10 minuten.

## <a name="use-hdinsight-compute-service"></a>HDInsight compute-service gebruiken
In scenario hello gebruikt u Azure Batch compute toorun Hallo aangepaste activiteit. U kunt ook uw eigen HDInsight op basis van Windows-cluster gebruiken of Data Factory Windows gebaseerd HDInsight-cluster op aanvraag maken en deze Hallo aangepaste activiteit op Hallo HDInsight-cluster worden uitgevoerd. Hier volgen Hallo hoofdstappen voor het gebruik van een HDInsight-cluster.

> [!IMPORTANT]
> Hallo aangepaste .NET-activiteiten alleen op Windows gebaseerde HDInsight-clusters worden uitgevoerd. Een tijdelijke oplossing voor deze beperking is toouse Hallo kaart verminderen activiteit toorun aangepaste Java-code op een Linux gebaseerde HDInsight-cluster. Een andere optie is toouse een Azure Batch-pool van virtuele machines toorun aangepaste activiteiten in plaats van een HDInsight-cluster.
 

1. Maak een gekoppelde HDInsight-service.   
2. Gebruik HDInsight gekoppelde service in plaats van **AzureBatchLinkedService** in Hallo pipeline JSON.

Als u wilt dat tootest met Hallo scenario wijziging **start** en **end** time-out voor de pijplijn hello, zodat u Hallo scenario Hello Azure HDInsight-service testen kunt.

#### <a name="create-azure-hdinsight-linked-service"></a>Een gekoppelde HDInsight-service maken
Hello Azure Data Factory-service ondersteunt het maken van een cluster op aanvraag en gebruik ze tooprocess invoer tooproduce uitvoergegevens. U kunt ook uw eigen cluster tooperform Hallo dezelfde. Wanneer u de HDInsight-cluster op aanvraag, wordt een cluster wordt gemaakt voor elk segment. Dat als u uw eigen HDInsight-cluster gebruikt, Hallo cluster gereed is Hallo tooprocess onmiddellijk segment. Daarom wanneer u on-demand-cluster gebruikt, kan er geen uitvoergegevens Hallo zo snel wanneer u uw eigen cluster gebruikt.

> [!NOTE]
> Tijdens runtime werkt een exemplaar van een .NET-activiteit alleen op een knooppunt van de werknemer in Hallo HDInsight-cluster. kan niet uitgebreid toorun op meerdere knooppunten. Meerdere exemplaren van de activiteit .NET kunnen parallel worden uitgevoerd op verschillende knooppunten van Hallo HDInsight-cluster.
>
>

##### <a name="toouse-an-on-demand-hdinsight-cluster"></a>toouse een HDInsight-cluster op aanvraag
1. In Hallo **Azure-portal**, klikt u op **maken en implementeren** in Hallo Data Factory-startpagina.
2. In Hallo Data Factory-Editor, klikt u op **nieuwe berekening** van Hallo opdracht en selecteer **On-demand HDInsight-cluster** in Hallo-menu.
3. Hallo na wijzigingen toohello JSON-script maken:

   1. Voor Hallo **de clustergrootte** eigenschap Hallo grootte van Hallo HDInsight-cluster opgeven.
   2. Voor Hallo **timeToLive** eigenschap, opgeven hoe lang Hallo klant inactief mag zijn voordat deze wordt verwijderd.
   3. Voor Hallo **versie** eigenschap Hallo HDInsight versie gewenste toouse opgeven. Als u deze eigenschap uitsluit, wordt de meest recente versie Hallo gebruikt.  
   4. Voor Hallo **linkedServiceName**, geef **AzureStorageLinkedService**.

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```

    > [!IMPORTANT]
    > Hallo aangepaste .NET-activiteiten alleen op Windows gebaseerde HDInsight-clusters worden uitgevoerd. Een tijdelijke oplossing voor deze beperking is toouse Hallo kaart verminderen activiteit toorun aangepaste Java-code op een Linux gebaseerde HDInsight-cluster. Een andere optie is toouse een Azure Batch-pool van virtuele machines toorun aangepaste activiteiten in plaats van een HDInsight-cluster.

4. Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gekoppelde service.

##### <a name="toouse-your-own-hdinsight-cluster"></a>toouse uw eigen HDInsight-cluster:
1. In Hallo **Azure-portal**, klikt u op **maken en implementeren** in Hallo Data Factory-startpagina.
2. In Hallo **Data Factory-Editor**, klikt u op **nieuwe berekening** van Hallo opdracht en selecteer **HDInsight-cluster** in Hallo-menu.
3. Hallo na wijzigingen toohello JSON-script maken:

   1. Voor Hallo **clusterUri** eigenschap, Voer Hallo-URL voor uw HDInsight. Bijvoorbeeld: https://<clustername>.azurehdinsight.net/     
   2. Voor Hallo **gebruikersnaam** eigenschap, voer de gebruikersnaam Hallo wie toegang tot toohello HDInsight-cluster heeft.
   3. Voor Hallo **wachtwoord** eigenschap Hallo wachtwoord invoeren voor Hallo-gebruiker.
   4. Voor Hallo **LinkedServiceName** eigenschap, voer **AzureStorageLinkedService**.
4. Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gekoppelde service.

Zie [gekoppelde services berekenen](data-factory-compute-linked-services.md) voor meer informatie.

In Hallo **pipeline JSON**, HDInsight gebruiken (op aanvraag of uw eigen) gekoppelde service:

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="create-a-custom-activity-by-using-net-sdk"></a>Een aangepaste activiteit maken met behulp van de .NET SDK
In het Hallo-procedure in dit artikel maakt u een gegevensfactory met een pipeline die gebruikmaakt van aangepaste activiteit Hallo via hello Azure-portal. Hallo volgende code laat zien u hoe toocreate gegevensfactory Hallo in plaats daarvan via .NET SDK. U vindt meer informatie over het gebruik van de SDK tooprogrammatically pijplijnen maken in Hallo [een pijplijn maken met de kopieeractiviteit met behulp van de .NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md) artikel. 

```csharp
using System;
using System.Configuration;
using System.Collections.ObjectModel;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.Azure;
using Microsoft.Azure.Management.DataFactories;
using Microsoft.Azure.Management.DataFactories.Models;
using Microsoft.Azure.Management.DataFactories.Common.Models;

using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Collections.Generic;

namespace DataFactoryAPITestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // create data factory management client

            // TODO: replace ADFTutorialResourceGroup with hello name of your resource group.
            string resourceGroupName = "ADFTutorialResourceGroup";

            // TODO: replace APITutorialFactory with a name that is globally unique. For example: APITutorialFactory04212017
            string dataFactoryName = "APITutorialFactory";

            TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
                ConfigurationManager.AppSettings["SubscriptionId"],
                GetAuthorizationHeader().Result);

            Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

            DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);

            Console.WriteLine("Creating a data factory");
            client.DataFactories.CreateOrUpdate(resourceGroupName,
                new DataFactoryCreateOrUpdateParameters()
                {
                    DataFactory = new DataFactory()
                    {
                        Name = dataFactoryName,
                        Location = "westus",
                        Properties = new DataFactoryProperties()
                    }
                }
            );

            // create a linked service for input data store: Azure Storage
            Console.WriteLine("Creating Azure Storage linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureStorageLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: Replace <accountname> and <accountkey> with name and key of your Azure Storage account.
                            new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>")
                        )
                    }
                }
            );

            // create a linked service for output data store: Azure SQL Database
            Console.WriteLine("Creating Azure Batch linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureBatchLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: replace <batchaccountname> and <yourbatchaccountkey> with name and key of your Azure Batch account
                            new AzureBatchLinkedService("<batchaccountname>", "https://westus.batch.azure.com", "<yourbatchaccountkey>", "myazurebatchpool", "AzureStorageLinkedService")
                        )
                    }
                }
            );

            // create input and output datasets
            Console.WriteLine("Creating input and output datasets");
            string Dataset_Source = "InputDataset";
            string Dataset_Destination = "OutputDataset";

            Console.WriteLine("Creating input dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Source,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FolderPath = "adftutorial/customactivityinput/",
                                Format = new TextFormat()
                            },
                            External = true,
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },

                            Policy = new Policy() { }
                        }
                    }
                });

            Console.WriteLine("Creating output dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Destination,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FileName = "{slice}.txt",
                                FolderPath = "adftutorial/customactivityoutput/",
                                PartitionedBy = new List<Partition>()
                                {
                                    new Partition()
                                    {
                                        Name = "slice",
                                        Value = new DateTimePartitionValue()
                                        {
                                            Date = "SliceStart",
                                            Format = "yyyy-MM-dd-HH"
                                        }
                                    }
                                }
                            },
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },
                        }
                    }
                });

            Console.WriteLine("Creating a custom activity pipeline");
            DateTime PipelineActivePeriodStartTime = new DateTime(2017, 3, 9, 0, 0, 0, 0, DateTimeKind.Utc);
            DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
            string PipelineName = "ADFTutorialPipelineCustom";

            client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new PipelineCreateOrUpdateParameters()
                {
                    Pipeline = new Pipeline()
                    {
                        Name = PipelineName,
                        Properties = new PipelineProperties()
                        {
                            Description = "Use custom activity",

                            // Initial value for pipeline's active period. With this, you won't need tooset slice status
                            Start = PipelineActivePeriodStartTime,
                            End = PipelineActivePeriodEndTime,
                            IsPaused = false,

                            Activities = new List<Activity>()
                            {
                                new Activity()
                                {
                                    Name = "MyDotNetActivity",
                                    Inputs = new List<ActivityInput>()
                                    {
                                        new ActivityInput() {
                                            Name = Dataset_Source
                                        }
                                    },
                                    Outputs = new List<ActivityOutput>()
                                    {
                                        new ActivityOutput()
                                        {
                                            Name = Dataset_Destination
                                        }
                                    },
                                    LinkedServiceName = "AzureBatchLinkedService",
                                    TypeProperties = new DotNetActivity()
                                    {
                                        AssemblyName = "MyDotNetActivity.dll",
                                        EntryPoint = "MyDotNetActivityNS.MyDotNetActivity",
                                        PackageLinkedService = "AzureStorageLinkedService",
                                        PackageFile = "customactivitycontainer/MyDotNetActivity.zip",
                                        ExtendedProperties = new Dictionary<string, string>()
                                        {
                                            { "SliceStart", "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"}
                                        }
                                    },
                                    Policy = new ActivityPolicy()
                                    {
                                        Concurrency = 2,
                                        ExecutionPriorityOrder = "OldestFirst",
                                        Retry = 3,
                                        Timeout = new TimeSpan(0,0,30,0),
                                        Delay = new TimeSpan()
                                    }
                                }
                            }
                        }
                    }
                });
        }

        public static async Task<string> GetAuthorizationHeader()
        {
            AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
            ClientCredential credential = new ClientCredential(
                ConfigurationManager.AppSettings["ApplicationId"],
                ConfigurationManager.AppSettings["Password"]);
            AuthenticationResult result = await context.AcquireTokenAsync(
                resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                clientCredential: credential);

            if (result != null)
                return result.AccessToken;

            throw new InvalidOperationException("Failed tooacquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a>Fouten opsporen in aangepaste activiteit in Visual Studio
Hallo [Azure Data Factory - lokale omgeving](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) voorbeeld op GitHub omvat een hulpprogramma waarmee u aangepaste .NET-activiteiten toodebug vanuit Visual Studio.  


## <a name="sample-custom-activities-on-github"></a>Aangepaste activiteiten voorbeeld op GitHub
| Voorbeeld | Welke aangepaste activiteit doet |
| --- | --- |
| [Het Downloadprogramma voor het HTTP-gegevens](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample). |Downloadt gegevens van een HTTP-eindpunt tooAzure Blob Storage met aangepaste C#-activiteit in de Data Factory. |
| [Twitter-gevoel Analysis-voorbeeld](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |Hiermee wordt een Azure ML-model en komen gevoel analyse, score berekenen, voorspelling enzovoort. |
| [R-Script uitvoeren](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample). |R-script worden opgeroepen door RScript.exe uitgevoerd op uw HDInsight-cluster al met R is geïnstalleerd op. |
| [Cross-activiteit van AppDomain .NET](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |Maakt gebruik van verschillende assembly-versies van de waarden die worden gebruikt door Hallo Data Factory starten |
| [Opnieuw verwerken van een model in Azure Analysis Services](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  Een model in Azure Analysis Services opnieuw verwerken. |

[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: ./media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: ./media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png
