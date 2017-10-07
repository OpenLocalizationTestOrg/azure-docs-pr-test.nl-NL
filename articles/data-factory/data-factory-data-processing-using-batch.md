---
title: aaaProcess grootschalige gegevenssets met behulp van Data Factory en Batch | Microsoft Docs
description: Hierin wordt beschreven hoe tooprocess grote hoeveelheden gegevens in een Azure Data Factory met behulp van de mogelijkheid parallelle verwerking van Azure Batch pipeline.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a>Grootschalige gegevenssets verwerken met Data Factory en Batch
In dit artikel beschrijft een architectuur van een Voorbeeldoplossing die wordt verplaatst en grootschalige gegevenssets in een automatische en geplande wijze verwerkt. Het bevat ook een end-to-end-overzicht tooimplement Hallo oplossing met behulp van Azure Data Factory en Azure Batch.

In dit artikel is langer dan het typische artikel omdat deze een overzicht van een Voorbeeldoplossing voor het volledige bevat. Als u nieuwe tooBatch en Data Factory, kunt u lezen over deze services en hoe ze samen werken. Als u over Hallo services weet en zijn ontwerpen/veranderd een oplossing, kunt u zich richten alleen op Hallo [architectuur sectie](#architecture-of-sample-solution) van Hallo artikel en als u een prototype of een oplossing ontwikkelt, u kunt ook tootry uit Stapsgewijze instructies in Hallo [scenario](#implementation-of-sample-solution). Wij willen graag uw opmerkingen over deze inhoud en hoe u deze gebruiken.

Eerst gaan we kijken hoe Data Factory en Batch services helpen kunnen bij het verwerken van grote gegevenssets in Hallo cloud.     

## <a name="why-azure-batch"></a>Waarom Azure Batch?
Azure Batch kunt u toorun grootschalige parallelle en high-performance computing (HPC) toepassingen efficiënt in Hallo cloud. Het is een platformservice die toorun rekenintensief werk op een beheerde verzameling van virtuele machines plant en kan automatisch scale compute resources toomeet Hallo behoeften van uw jobs.

Met de Hallo Batch-service definieert u Azure compute resources tooexecute uw toepassingen parallel, en op schaal. U kunt uitvoeren op aanvraag of geplande taken en u hoeft niet toomanually maken, configureren en beheren van een HPC-cluster, individuele virtuele machines, virtuele netwerken of een complexe job en taakplanningsinfrastructuur.

Zie Hallo artikelen te volgen als u niet bekend met Azure Batch bent als het helpt Hallo architectuur/implementatie van Hallo-oplossing wordt beschreven in dit artikel gaan.   

* [Basisbeginselen van Azure Batch](../batch/batch-technical-overview.md)
* [Overzicht van de functies van Batch](../batch/batch-api-basics.md)

(optioneel) toolearn meer informatie over Azure Batch Zie Hallo [leertraject voor Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).

## <a name="why-azure-data-factory"></a>Waarom Azure Data Factory?
Data Factory is een cloud-gebaseerde gegevens integration-service die is ingedeeld en automatiseert Hallo verplaatsing en transformatie van gegevens. Hallo Data Factory-service gebruikt, kunt u beheerde gegevenspijplijnen die gegevens verplaatsen van on-premises en in de cloud gegevensarchief winkels tooa gecentraliseerde gegevens (bijvoorbeeld: Azure Blob-opslag), en gegevens met services zoals Azure HDInsight en Azure proces/transformatie Machine Learning. U kunt ook gegevens pijplijnen toorun plannen in een geplande manier (elk uur, dagelijks, wekelijks, enz.) en een monitor en deze in een oogopslag tooidentify problemen beheren en actie ondernemen.

Zie Hallo artikelen te volgen als u niet bekend met Azure Data Factory bent als het helpt Hallo architectuur/implementatie van Hallo-oplossing wordt beschreven in dit artikel gaan.  

* [Introductie van Azure Data Factory](data-factory-introduction.md)
* [Uw eerste pijplijn voor gegevens](data-factory-build-your-first-pipeline.md)   

(optioneel) toolearn meer informatie over Azure Data Factory Zie Hallo [leertraject voor Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).

## <a name="data-factory-and-batch-together"></a>Data Factory en in Batch samen
Data Factory bevat ingebouwde activiteiten zoals Kopieeractiviteit toocopy of verplaatsen van een brongegevens gegevensarchief tooa doelgegevensopslagplaats en Hive-activiteit tooprocess gegevens met behulp van Hadoop-clusters (HDInsight) in Azure. Zie [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) voor een lijst van activiteiten voor gegevenstransformatie ondersteund.

Ook kunt u toocreate aangepaste .NET-activiteiten toomove of proces gegevens met uw eigen logica en deze activiteiten worden uitgevoerd op een Azure HDInsight-cluster of op een Azure Batch-pool van virtuele machines. Wanneer u Azure Batch gebruikt, kunt u Hallo groep tooauto-scale configureren (toevoegen of verwijderen van virtuele machines op basis van de werkbelasting Hallo) op basis van een formule die u opgeeft.     

## <a name="architecture-of-sample-solution"></a>Architectuur van Voorbeeldoplossing
Hoewel Hallo architectuur die wordt beschreven in dit artikel is bedoeld voor een eenvoudige oplossing, is de relevante toocomplex scenario's zoals risico modellering van financiële diensten, verwerking van afbeeldingen en rendering en Toepassingsgeoriënteerde analyse.

Hallo diagram illustreert 1) hoe Data Factory gegevensverplaatsing ingedeeld en verwerking en 2) de manier waarop Azure Batch verwerkt Hallo gegevens op een parallelle manier. Downloaden en afdrukken Hallo diagram ter referentie (11 x 17. of A3-grootte): [HPC en gegevens orchestration met behulp van Azure Batch- en Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).

[![Diagram van grootschalige gegevensverwerking](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)

Hallo bevat volgende lijst de basisstappen Hallo van Hallo proces. Hallo-oplossing omvat code en uitleg toobuild Hallo end-to-end-oplossing.

1. **Azure Batch configureren met een pool van rekenknooppunten (virtuele machines)**. U kunt het aantal knooppunten Hallo en de grootte van elk knooppunt opgeven.
2. **Maak een Azure Data Factory-instantie** die is geconfigureerd met de entiteiten die Azure blob-opslag, Azure Batch compute-service, invoer-en uitvoergegevens en een werkstroom/pijplijn met activiteiten die verplaatsen en gegevens transformeren vertegenwoordigen.
3. **Maak een aangepaste .NET-activiteit in Hallo Data Factory-pijplijn**. Hallo-activiteit is uw gebruikerscode die wordt uitgevoerd op Hallo Azure Batch-pool.
4. **Opslaan van grote hoeveelheden gegevens als blobs in Azure storage**. Gegevens worden in logische segmenten verdeeld (meestal door time).
5. **Data Factory kopieert de gegevens die wordt verwerkt parallel** toohello secundaire locatie.
6. **Data Factory uitgevoerd Hallo aangepaste activiteit gebruikmaken van Hallo toegewezen door Batch**. Data Factory kunt activiteiten tegelijkertijd worden uitgevoerd. Elke activiteit verwerkt een segment met gegevens. Hallo resultaten worden opgeslagen in Azure storage.
7. **Data Factory Hallo eindresultaat tooa derde locatie verplaatst**, voor distributie via een app of voor verdere verwerking door andere hulpprogramma's.

## <a name="implementation-of-sample-solution"></a>Implementatie van Voorbeeldoplossing
Hallo Voorbeeldoplossing opzet eenvoudig en tooshow u hoe toouse Data Factory en Batch samen tooprocess gegevenssets. Hallo oplossing telt gewoon Hallo aantal exemplaren van een zoekterm ('Microsoft') in invoerbestanden georganiseerd in een tijdreeks. Het levert Hallo aantal toooutput bestanden.

**Tijd**: als u bekend met de basisprincipes van Azure Data Factory en Batch bent en hebben voltooid Hallo vereisten hieronder vermeld, schatten we deze oplossing toocomplete van 1 tot 2 uur duurt.

### <a name="prerequisites"></a>Vereisten
#### <a name="azure-subscription"></a>Azure-abonnement
Als u geen Azure-abonnement hebt, kunt u een gratis proefaccount maken binnen een paar minuten. Zie [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="azure-storage-account"></a>Azure Storage-account
U kunt een Azure storage-account gebruiken voor het opslaan van Hallo gegevens in deze zelfstudie. Als u geen Azure storage-account hebt, raadpleegt u [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account). Hallo Voorbeeldoplossing maakt gebruik van blob-opslag.

#### <a name="azure-batch-account"></a>Azure Batch-account
Een Azure Batch-account maken met Hallo [Azure-portal](http://manage.windowsazure.com/). Zie [maken en beheren van Azure Batch-account](../batch/batch-account-create-portal.md). Houd er rekening mee hello Azure Batch-account en de accountsleutel sleutel. U kunt ook [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate Azure Batch-account. Zie [aan de slag met Azure Batch PowerShell-cmdlets](../batch/batch-powershell-cmdlets-get-started.md) voor gedetailleerde instructies over het gebruik van deze cmdlet.

Hallo Voorbeeldoplossing gebruikt Azure Batch (indirect via een Azure Data Factory-pijplijn) tooprocess gegevens op een parallelle manier op een pool van rekenknooppunten (een beheerde verzameling van virtuele machines).

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a>Azure Batch-pool van virtuele machines (VM's)
Maak een **Azure Batch-pool** met ten minste 2 rekenknooppunten.

1. In Hallo [Azure-portal](https://portal.azure.com), klikt u op **Bladeren** in Hallo menu aan de linkerkant en klik op **Batch-Accounts**.
2. Selecteer uw Azure Batch-account tooopen hello **Batch-Account** blade.
3. Klik op **Pools** tegel.
4. In Hallo **Pools** blade, klik op de knop toevoegen op Hallo werkbalk tooadd een pool.
   1. Geef een ID voor Hallo pool (**Pool-ID**). Opmerking Hallo **ID van de pool Hallo**; u deze nodig hebt bij het maken van Hallo Data Factory-oplossing.
   2. Geef **Windows Server 2012 R2** voor Hallo besturingssysteemgroep instelling.
   3. Selecteer een **knooppunt prijscategorie**.
   4. Voer **2** als waarde voor Hallo **doel toegewezen** instelling.
   5. Voer **2** als waarde voor Hallo **maximum aantal taken per knooppunt** instelling.
   6. Klik op **OK** toocreate Hallo van toepassingen.

#### <a name="azure-storage-explorer"></a>Azure Opslagverkenner
[Azure Storage Explorer 6 (hulpprogramma)](https://azurestorageexplorer.codeplex.com/) of [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (van ClumsyLeaf Software). U gebruikt deze hulpprogramma's voor te bekijken en wijzigen van Hallo-gegevens in uw Azure Storage-projecten inclusief Hallo logboeken van uw cloud-gebaseerde toepassingen.

1. Maken van een container met de naam **mycontainer** met persoonlijke toegang (geen anonieme toegang)
2. Als u **CloudXplorer**, maakt u mappen en submappen met Hallo structuur te volgen:

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   `Inputfolder`en `outputfolder` zijn op het hoogste niveau van de mappen in `mycontainer`. Hallo `inputfolder` submappen met de datum / tijd stempels (jjjj-MM-DD-UU).

   Als u **Azure Opslagverkenner**, in de volgende stap hello, moet u tooupload bestanden met namen: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` enzovoort. Deze stap maakt automatisch Hallo mappen.
3. Maak een tekstbestand **bestand.txt** op uw computer met inhoud die Hallo sleutelwoord is **Microsoft**. Bijvoorbeeld: 'aangepaste activiteit Microsoft test aangepaste activiteit Microsoft test'.
4. Het uploaden van Hallo bestand toohello volgende invoer mappen in Azure blob-opslag.

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   Als u **Azure Opslagverkenner**, Hallo-bestand uploaden **bestand.txt** te**mycontainer**. Klik op **kopie** op Hallo werkbalk toocreate een kopie van het Hallo-blob. In Hallo **Blob kopiëren** dialoogvenster, wijziging Hallo **blob doelnaam** te`inputfolder/2015-11-16-00/file.txt`. Herhaal deze stap toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` enzovoort. Deze actie wordt automatisch gemaakt Hallo mappen.
5. Maken van een andere container met de naam: `customactivitycontainer`. U uploaden Hallo aangepaste activiteit zip-bestand toothis container.

#### <a name="visual-studio"></a>Visual Studio
Installeer Microsoft Visual Studio 2012 of hoger toocreate Hallo aangepaste Batch activiteit toobe in Hallo Data Factory-oplossing gebruikt.

### <a name="high-level-steps-toocreate-hello-solution"></a>Stappen op hoog niveau toocreate Hallo oplossing
1. Maak een aangepaste activiteit die Hallo gegevensverwerking logica bevat.
2. Maak een Azure data factory die gebruikmaakt van aangepaste activiteit Hallo:

### <a name="create-hello-custom-activity"></a>Hallo aangepaste activiteit maken
Hallo Data Factory aangepaste activiteit vormt de kern Hallo van deze Voorbeeldoplossing. Hallo Voorbeeldoplossing gebruikt Azure Batch toorun Hallo aangepaste activiteit. Zie [aangepaste activiteiten gebruiken in een Azure Data Factory-pijplijn](data-factory-use-custom-activities.md) voor Hallo basisinformatie toodevelop aangepaste activiteiten en gebruik ze in Azure Data Factory pijplijnen.

een aangepaste .NET-activiteit die u in een Azure Data Factory-pijplijn gebruiken kunt toocreate, moet u toocreate een **.NET Class Library** project met een klasse die die implementeert **IDotNetActivity** interface. Deze interface heeft slechts één methode: **Execute**. Hier volgt Hallo handtekening van Hallo-methode:

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

Hallo-methode heeft enkele belangrijke onderdelen moet u toounderstand.

* Hallo-methode heeft vier parameters:

  1. **linkedServices**. Een inventariseerbare lijst met gekoppelde services die een koppeling i/o-gegevensbronnen (bijvoorbeeld: Azure Blob Storage) toohello data factory. In dit voorbeeld is er slechts één van de gekoppelde service van het type Azure Storage gebruikt voor invoer en uitvoer.
  2. **gegevenssets**. Dit is een inventariseerbare lijst van gegevenssets. U kunt deze parameter tooget Hallo locaties en schema's die zijn gedefinieerd door de invoer- en uitvoergegevenssets gebruiken.
  3. **activiteit**. Deze parameter vertegenwoordigt Hallo huidige compute entiteit - in dit geval wordt een Azure Batch-service.
  4. **Berichtenlogboek**. Hallo Berichtenlogboek kunt die u foutopsporing opmerkingen die surface Hallo schrijft 'Gebruiker' melden Hallo pijplijn.
* Hallo-methode retourneert een woordenlijst die gebruikt toochain aangepaste activiteiten samen in de toekomst Hallo worden kan. Deze functie is nog niet geïmplementeerd, kunt u dus een woordenboek leeg retourneren van Hallo-methode.

#### <a name="procedure-create-hello-custom-activity"></a>Procedure: Hallo aangepaste activiteit maken
1. Maak een .NET Class Library-project in Visual Studio.

   1. Start **Visual Studio 2012**/**2013-2015**.
   2. Klik op **bestand**, wijst u te**nieuw**, en klik op **Project**.
   3. Vouw **sjablonen**, en selecteer **Visual C\#**. In dit scenario gebruikt u C\#, maar u kunt .NET taal toodevelop Hallo aangepaste activiteit.
   4. Selecteer **Class Library** uit de lijst Hallo van projecttypen op Hallo rechts.
   5. Voer **MyDotNetActivity** voor Hallo **naam**.
   6. Selecteer **C:\\ADF** voor Hallo **locatie**. Maak de map Hallo **ADF** als deze niet bestaat.
   7. Klik op **OK** toocreate Hallo project.
2. Klik op **extra**, wijst u te**NuGet Package Manager**, en klik op **Package Manager Console**.
3. In Hallo **Package Manager Console**, uitvoeren na de opdracht tooimport hello **Microsoft.Azure.Management.DataFactories**.

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. Importeren Hallo **Azure Storage** NuGet-pakket in toohello-project. Omdat u Hallo Blob storage-API in dit voorbeeld gebruiken moet u dit pakket.

    ```powershell
    Install-Package Azure.Storage
    ```
5. Voeg de volgende Hallo **met** richtlijnen toohello bronbestand in Hallo-project.

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. Hallo naam wijzigen van Hallo **naamruimte** te**MyDotNetActivityNS**.

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. Hallo-naam van de klasse Hallo te wijzigen**MyDotNetActivity** en afgeleid Hallo **IDotNetActivity** interface zoals hieronder wordt weergegeven.

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. Hallo implementeren (toevoegen) **Execute** methode Hallo **IDotNetActivity** interface toohello **MyDotNetActivity** klasse en kopieer Hallo voorbeeldmethode code toohello te volgen. Zie Hallo [methode Execute](#execute-method) sectie voor uitleg voor Hallo logica in deze methode gebruikt.

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
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
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
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
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
9. Hallo na helperklasse methoden toohello toevoegen. Deze methoden worden aangeroepen door Hallo **Execute** methode. Het belangrijkste is dat Hallo **Calculate** methode isoleert Hallo-code die elke blob doorlopen.

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
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
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
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
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
    Hallo **GetFolderPath** methode retourneert Hallo pad toohello map die Hallo gegevensset punten tooand hello **GetFileName** methode retourneert Hallo-naam van Hallo-blob/bestand dat verwijst naar gegevensset Hallo.

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    Hallo **Calculate** methode berekent het aantal exemplaren van het sleutelwoord Hallo **Microsoft** in Hallo invoerbestanden (BLOB's in de map Hallo). Hallo zoekterm ('Microsoft') is vastgelegd in het Hallo-code.

1. Hallo project compileren. Klik op **bouwen** uit en klik op Hallo **Build Solution**.
2. Start **Windows Verkenner**, en te navigeren**bin\\debug** of **bin\\release** map afhankelijk van Hallo type build.
3. Maak een zipbestand **MyDotNetActivity.zip** die alle Hallo binaire bestanden in Hallo bevat  **\\bin\\Debug** map. U kunt tooinclude hello MyDotNetActivity. **pdb** bestand zodat u aanvullende informatie zoals regelnummer in de broncode Hallo die Hallo probleem veroorzaakt ophalen wanneer er een fout optreedt.

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. Uploaden **MyDotNetActivity.zip** als een blob toohello blob-container: `customactivitycontainer` in hello Azure blob storage-die Hallo **StorageLinkedService** gekoppelde service in Hallo  **ADFTutorialDataFactory** gebruikt. Maken van de blob-container Hallo `customactivitycontainer` als deze niet al bestaat.

#### <a name="execute-method"></a>De methode Execute
Deze sectie bevat meer informatie en opmerkingen over Hallo-code in Hallo Execute-methode.

1. Hallo-leden voor doorloopt Hallo invoerverzameling vindt u in Hallo [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) naamruimte. Hallo blob verzameling doorloopt, moet u Hallo **BlobContinuationToken** klasse. In wezen, moet u een do-tijdens lus met Hallo-token als Hallo-mechanisme voor het Hallo-lus wordt afgesloten. Zie voor meer informatie [hoe toouse Blob storage uit het .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Hier ziet u een eenvoudige lus:

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   Raadpleeg de documentatie Hallo voor Hallo [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) methode voor meer informatie.
2. Hallo code voor binnen Hallo Hallo reeks blobs logisch doorloopt gaat doen-tijdens lus. In Hallo **Execute** methode, komen Hallo-terwijl lus Hallo lijst met blobs tooa methode met de naam verstuurt **Calculate**. Hallo-methode retourneert een string-variabele met de naam **uitvoer** die Hallo resultaat van gelet herhaald via alle Hallo blobs in Hallo segment.

   Deze retourneert het aantal exemplaren van de zoekterm Hallo Hallo (**Microsoft**) in de blob Hallo doorgegeven toohello **Calculate** methode.

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. Eenmaal Hallo **Calculate** methode heeft Hallo werk gedaan, deze moet worden geschreven tooa nieuwe blob. Dus voor elke set van BLOB's verwerkt, kan een nieuwe blob met Hallo resultaten worden geschreven. toowrite tooa nieuwe blob, het eerste zoeken Hallo-uitvoergegevensset.

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. Hallo code ook een Help-methode aanroept: **GetFolderPath** tooretrieve Hallo mappad (Hallo opslag containernaam).

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   Hallo **GetFolderPath** webcasts Hallo gegevensset object tooan AzureBlobDataSet met een eigenschap genaamd FolderPath.

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. Hallo code aanroepen Hallo **GetFileName** methode tooretrieve Hallo-bestandsnaam (blob-naam). Hallo-code is vergelijkbaar toohello bovenstaande code tooget Hallo mappad.

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. Hallo-naam van Hallo-bestand is geschreven door een URI-object te maken. Hallo URI constructor gebruikt Hallo **BlobEndpoint** tooreturn Hallo container eigenschapsnaam. Hallo map pad en de naam toegevoegd tooconstruct Hallo uitvoer blob-URI.  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. Hallo-naam van Hallo-bestand is geschreven en nu kunt u Hallo uitvoertekenreeks schrijven van Hallo **Calculate** methode tooa nieuwe blob:

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a>Hallo een gegevensfactory maken
In Hallo [maken van aangepaste activiteit Hallo](#create-the-custom-activity) sectie maakt u een aangepaste activiteit hebt gemaakt en geüploade Hallo zip-bestand met de binaire bestanden en Hallo PDB-bestand tooan Azure blob-container. In deze sectie maakt u een Azure **gegevensfactory** met een **pijplijn** die gebruikmaakt van Hallo **aangepaste activiteit**.

Hallo invoergegevensset voor Hallo aangepaste activiteit Hallo-blobs (bestanden) in de invoermap hello vertegenwoordigt (`mycontainer\\inputfolder`) in de blob-opslag. Hallo uitvoergegevensset voor Hallo activiteit Hallo uitvoer blobs in de uitvoermap hello vertegenwoordigt (`mycontainer\\outputfolder`) in de blob-opslag.

Een of meer bestanden neerzetten in Hallo invoer mappen:

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

Bijvoorbeeld: één bestand (bestand.txt) verwijderen met de volgende inhoud in elk van de mappen Hallo Hallo.

```
test custom activity Microsoft test custom activity Microsoft
```

Elke invoermap komt overeen tooa segment in Azure Data Factory, zelfs als Hallo map 2 of meer bestanden bevat. Wanneer elk segment wordt verwerkt door de pijplijn hello, doorlopen aangepaste activiteit Hallo alle Hallo blobs in de invoermap Hallo voor dat segment.

Ziet u vijf uitvoerbestanden Hello dezelfde inhoud. Hallo-uitvoerbestand van het verwerken van bestand in map Hallo 2015-11-16-00 Hallo heeft bijvoorbeeld Hallo volgende inhoud:

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

Als u meerdere bestanden (bestand.txt, bestand2.txt samengevoegd, file3.txt) verwijderen Hello dezelfde toohello invoermap inhoud, ziet u de volgende inhoud in het uitvoerbestand Hallo Hallo. Elke map (2015-11-16-00, enz.) tooa segment in dit voorbeeld komt overeen, hoewel Hallo map meerdere invoerbestanden heeft.

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

Hallo-bestand voor uitvoer heeft drie regels nu één voor elk bestand voor invoer (blob) in Hallo map die is gekoppeld aan het Hallo-segment (2015-11-16-00).

Een taak is gemaakt voor elke activiteit die wordt uitgevoerd. In dit voorbeeld moet u er slechts één activiteit is in Hallo pijplijn. Wanneer een segment wordt verwerkt door de pijplijn hello, is Hallo aangepaste activiteit wordt uitgevoerd op Azure Batch tooprocess Hallo segment. Aangezien er zijn vijf segmenten (elk segment kan hebben meerdere blobs of -bestand), moet u er vijf taken die zijn gemaakt in Azure Batch zijn. Wanneer een taak wordt uitgevoerd op de Batch, is het daadwerkelijk Hallo aangepaste activiteit die wordt uitgevoerd.

Hallo volgen Stapsgewijze instructies vindt u meer informatie.

#### <a name="step-1-create-hello-data-factory"></a>Stap 1: Hallo een gegevensfactory maken
1. Na het aanmelden toohello [Azure-portal](https://portal.azure.com/), Hallo volgende stappen:

   1. Klik op **nieuw** op Hallo linkermenu.
   2. Klik op **gegevens en analyse** in Hallo **nieuw** blade.
   3. Klik op **Data Factory** op Hallo **gegevensanalyse** blade.
2. In Hallo **nieuwe gegevensfactory** blade Voer **CustomActivityFactory** voor Hallo naam. Hallo-naam van hello Azure-gegevensfactory moet wereldwijd uniek zijn. Als u de foutmelding Hallo: **Data factory-naam 'CustomActivityFactory' is niet beschikbaar**, Hallo-naam van gegevensfactory Hallo wijzigen (bijvoorbeeld **yournameCustomActivityFactory**) en probeert te maken opnieuw.
3. Klik op **RESOURCEGROEPNAAM**, en selecteer een bestaande resourcegroep of maak een resourcegroep.
4. Controleer of dat u gebruikmaakt van het juiste abonnement Hallo en regio waar u Hallo data factory toobe gemaakt.
5. Klik op **maken** op Hallo **nieuwe gegevensfactory** blade.
6. Zie van Hallo gegevensfactory wordt gemaakt in Hallo **Dashboard** Hallo Azure-portal.
7. Nadat het Hallo-gegevensfactory is gemaakt, ziet u Hallo data factory-pagina waarop u inhoud van de gegevensfactory Hallo Hallo.

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a>Stap 2: Gekoppelde services maken
Gekoppelde services worden gegevensarchieven of compute-services tooan Azure-gegevensfactory. In deze stap koppelt u uw **Azure Storage** account en **Azure Batch** account tooyour data factory.

#### <a name="create-azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service maken
1. Klik op Hallo **auteur en implementeren van** tegel op Hallo **DATA FACTORY** blade voor **CustomActivityFactory**. U ziet Hallo Data Factory-Editor.
2. Klik op **nieuwe gegevensopslag** op Hallo opdrachtbalk en kies **Azure-opslag.** U ziet Hallo JSON-script voor het maken van een Azure Storage gekoppelde service in Hallo-editor.

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. Vervang **accountnaam** met Hallo-naam van uw Azure storage-account en **accountsleutel** door de toegangssleutel Hallo van hello Azure storage-account. toolearn hoe tooget uw opslag toegang krijgen tot sleutel, Zie [toegangssleutels voor opslag weergeven, kopiëren en opnieuw genereren](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

4. Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gekoppelde service.

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a>Azure Batch gekoppelde service maken
In deze stap maakt u een gekoppelde service maken voor uw **Azure Batch** account die is gebruikt toorun Hallo Data Factory aangepaste activiteit.

1. Klik op **nieuwe berekening** op Hallo opdrachtbalk en kies **Azure Batch.** U ziet Hallo JSON-script voor het maken van een Azure-Batch gekoppelde service in Hallo-editor.
2. In Hallo JSON-script:

   1. Vervang **accountnaam** met Hallo-naam van uw Azure Batch-account.
   2. Vervang **toegangssleutel** door de toegangssleutel Hallo van hello Azure Batch-account.
   3. Voer Hallo-ID van Hallo pool voor Hallo **poolName** eigenschap**.** Voor deze eigenschap kunt u de naam van de toepassingen opgeven of id-groep
   4. Voer Hallo batch URI voor Hallo **batchUri** JSON-eigenschap.

      > [!IMPORTANT]
      > Hallo **URL** van Hallo **blade van Azure Batch-account** bevindt zich in de volgende indeling Hallo: \<accountname\>.\< regio\>. batch.azure.com. Voor Hallo **batchUri** eigenschap in JSON hello, moet u te**verwijderen "accountname."** van Hallo-URL. Voorbeeld: `"batchUri": "https://eastus.batch.azure.com"`.
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      Voor Hallo **poolName** eigenschap, kunt u ook Hallo-ID van Hallo pool in plaats van Hallo-naam van Hallo van toepassingen opgeven.

      > [!NOTE]
      > Hallo Data Factory-service biedt een optie op aanvraag geen ondersteuning voor Azure Batch als voor HDInsight. U kunt uw eigen Azure Batch-pool alleen gebruiken in een Azure data factory.
      >
      >
   5. Geef **StorageLinkedService** voor Hallo **linkedServiceName** eigenschap. U kunt deze gekoppelde service gemaakt in de vorige stap Hallo. Deze opslag wordt gebruikt als een faseringsgebied voor bestanden en de logboeken.
3. Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gekoppelde service.

#### <a name="step-3-create-datasets"></a>Stap 3: Gegevenssets maken
In deze stap maakt u gegevenssets toorepresent invoer maken en uitvoergegevens.

#### <a name="create-input-dataset"></a>Invoergegevensset maken
1. In Hallo **Editor** Hallo Data Factory, klikt u op **nieuwe gegevensset** op Hallo werkbalk en klikt u op **Azure Blob storage** uit de vervolgkeuzelijst Hallo.
2. Hallo JSON in het rechterdeelvenster Hallo vervangen door Hallo volgende JSON-fragment:

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
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

    U maakt een pijplijn verderop in dit scenario met begintijd: 2015-11-16T00:00:00Z-en eindtijd: 2015-11-16T05:00:00Z. Geplande tooproduce gegevens is **per uur**, zodat er 5 segmenten van de invoer/uitvoer (tussen **00**: 00:00 -\> **05**: 00:00).

    Hallo **frequentie** en **interval** voor invoergegevensset hello te is ingesteld**uur** en **1**, wat betekent dat Hallo invoer segment is beschikbaar elk uur.

    Hier volgen Hallo begintijden voor elk segment, die wordt vertegenwoordigd door **SliceStart** systeemvariabele in Hallo hierboven JSON-codefragment.

    | **Segment** | **Begintijd**          |
    |-----------|-------------------------|
    | 1         | 2015-11-16T**00**: 00:00 |
    | 2         | 2015-11-16T**01**: 00:00 |
    | 3         | 2015-11-16T**02**: 00:00 |
    | 4         | 2015-11-16T**03**: 00:00 |
    | 5         | 2015-11-16T**04**: 00:00 |

    Hallo **folderPath** wordt berekend met behulp van Hallo jaar, maand, dag en uur onderdeel van de begintijd Hallo-segment (**SliceStart**). Hier is daarom hoe een invoermap toegewezen tooa segment is.

    | **Segment** | **Begintijd**          | **Invoermap**  |
    |-----------|-------------------------|-------------------|
    | 1         | 2015-11-16T**00**: 00:00 | 2015-11-16-**00** |
    | 2         | 2015-11-16T**01**: 00:00 | 2015-11-16-**01** |
    | 3         | 2015-11-16T**02**: 00:00 | 2015-11-16-**02** |
    | 4         | 2015-11-16T**03**: 00:00 | 2015-11-16-**03** |
    | 5         | 2015-11-16T**04**: 00:00 | 2015-11-16-**04** |

1. Klik op **implementeren** op Hallo werkbalk toocreate en implementeren van Hallo **InputDataset** tabel.

#### <a name="create-output-dataset"></a>Uitvoergegevensset maken
In deze stap maakt u een andere dataset van het type AzureBlob toorepresent Hallo uitvoergegevens.

1. In Hallo **Editor** Hallo Data Factory, klikt u op **nieuwe gegevensset** op Hallo werkbalk en klikt u op **Azure Blob storage** uit de vervolgkeuzelijst Hallo.
2. Hallo JSON in het rechterdeelvenster Hallo vervangen door Hallo volgende JSON-fragment:

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
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

    Een uitvoer-blob/bestand wordt gegenereerd voor elk segment invoer. Hier ziet u hoe een bestand voor uitvoer met de naam van elk segment. Alle Hallo uitvoerbestanden worden gegenereerd in een uitvoermap: `mycontainer\\outputfolder`.

    | **Segment** | **Begintijd**          | **Bestand voor uitvoer**       |
    |-----------|-------------------------|-----------------------|
    | 1         | 2015-11-16T**00**: 00:00 | 2015-11-16 -**00. txt** |
    | 2         | 2015-11-16T**01**: 00:00 | 2015-11-16 -**01. txt** |
    | 3         | 2015-11-16T**02**: 00:00 | 2015-11-16 -**02. txt** |
    | 4         | 2015-11-16T**03**: 00:00 | 2015-11-16 -**03. txt** |
    | 5         | 2015-11-16T**04**: 00:00 | 2015-11-16 -**04. txt** |

    Houd er rekening mee dat alle bestanden in een invoermap Hallo (bijvoorbeeld: 2015-11-16-00) deel uitmaken van een segment met Hallo begintijd: 2015-11-16-00. Als dit segment is verwerkt, wordt Hallo aangepaste activiteit gescand door elk bestand en resulteert in een regel in het uitvoerbestand Hallo met Hallo aantal exemplaren van zoekterm ('Microsoft'). Als er drie bestanden in de map Hallo 2015-11-16-00, er zijn drie regels in het uitvoerbestand Hallo: 2015-11-16-00.txt.

1. Klik op **implementeren** op Hallo werkbalk toocreate en implementeren van Hallo **OutputDataset**.

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a>Stap 4: Maken en uitvoeren van Hallo pijplijn met een aangepaste activiteit
In deze stap maakt maken u een pijplijn met één activiteit, Hallo aangepaste activiteit die u eerder hebt gemaakt.

> [!IMPORTANT]
> Als u dit nog niet hebt geüpload Hallo **bestand.txt** tooinput mappen in de blob-container hello, dit doen voordat u Hallo pijplijn maakt. Hallo **isPaused** eigenschap toofalse in Hallo pijplijn JSON, is ingesteld zodat Hallo pijplijn wordt onmiddellijk uitgevoerd als Hallo **start** Hallo afgelopen datum is.
>
>

1. In Hallo Data Factory-Editor, klikt u op **nieuwe pijplijn** op Hallo opdrachtbalk klikken. Als u de opdracht Hallo niet ziet, klikt u op **... (Ellips)**  toosee deze.
2. Hallo JSON in het rechterdeelvenster Hallo vervangen door Hallo volgende JSON-script:

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   Houd er rekening mee Hallo volgende punten:

   * Er is slechts één activiteit in de pijplijn Hallo en die is van het type: **DotNetActivity**.
   * **AssemblyName** toohello naam Hallo dll-bestand dat is ingesteld: **MyDotNetActivity.dll**.
   * **EntryPoint** te is ingesteld,**MyDotNetActivityNS.MyDotNetActivity**. Het is in feite \<naamruimte\>.\< ClassName\> in uw code.
   * **PackageLinkedService** te is ingesteld,**StorageLinkedService** die toohello blob-opslag met Hallo aangepaste activiteit zip-bestand verwijst. Als u van andere Azure Storage-accounts voor i/o-bestanden en Hallo aangepaste activiteit zip-bestand gebruikmaakt, hebt u toocreate een andere Azure Storage gekoppelde service. In dit artikel wordt ervan uitgegaan dat u hetzelfde Azure-opslagaccount Hallo.
   * **PackageFile** te is ingesteld,**customactivitycontainer/MyDotNetActivity.zip**. Het Hallo-indeling is: \<containerforthezip\>/\<nameofthezip.zip\>.
   * Hallo aangepaste activiteit wordt **InputDataset** als invoer en **OutputDataset** als uitvoer.
   * Hallo **linkedServiceName** eigenschap van de aangepaste activiteit Hallo verwijst toohello **AzureBatchLinkedService**, waarin u Azure Data Factory bepaald die Hallo aangepaste activiteit moet toorun op Azure Batch.
   * Hallo **gelijktijdigheid** instelling is belangrijk. Als u Hallo-standaardwaarde, die 1, is zelfs als er 2 of meer in hello Azure Batch-pool rekenknooppunten, Hallo segmenten worden verwerkt achter elkaar. U onderneemt daarom niet profiteren van Hallo parallelle verwerking mogelijkheden van Azure Batch. Als u instelt **gelijktijdigheid** tooa hogere waarde, bijvoorbeeld 2 is, betekent dit dat twee segmenten (komt overeen tootwo taken in Azure Batch) kunnen worden verwerkt op Hallo dezelfde tijd, in welk geval beide VM Hallo in hello Azure Batch pool worden benut. Daarom op de juiste wijze Hallo gelijktijdigheid eigenschap instellen.
   * Slechts één taak (segment) wordt standaard uitgevoerd op een virtuele machine op elk gewenst moment. Hallo reden is dat standaard hello **maximum aantal taken per VM** too1 voor een Azure Batch-toepassingen is ingesteld. Als onderdeel van de vereisten, u hebt gemaakt een groep met deze eigenschap set too2, zodat twee segmenten van de Data Factory op een virtuele machine op Hallo uitvoeren kunnen hetzelfde moment.

    -   **isPaused** eigenschap toofalse standaard is ingesteld. Hallo-pijplijn wordt onmiddellijk uitgevoerd in dit voorbeeld omdat Hallo segmenten te in de afgelopen Hallo starten. U kunt deze eigenschap tootrue toopause Hallo pijplijn en zijn ingesteld dat deze back-toofalse toorestart.

    -   Hallo **start** tijd en **end** segmenten hourly, geproduceerde zodat vijf segmenten worden geproduceerd door Hallo pijplijn en tijden zijn vijf uur uit elkaar liggen.

1. Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo pijplijn.

#### <a name="step-5-test-hello-pipeline"></a>Stap 5: Hallo pijplijn testen
In deze stap kunt u Hallo pijplijn testen door de bestanden neerzetten in invoer Hallo-mappen. U begint met testen Hallo-pipeline met één bestand per één invoer map.

1. Klik in de Data Factory-blade Hallo in hello Azure-portal, op **Diagram**.

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. Dubbelklik in de diagramweergave Hallo invoergegevensset: **InputDataset**.

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. U ziet Hallo **InputDataset** blade met alle vijf segmenten gereed. Kennisgeving Hallo **segment BEGINTIJD** en **segment EINDTIJD** voor elk segment.

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. In Hallo **diagramweergave**, klik op nu **OutputDataset**.
5. U ziet dat Hallo vijf uitvoer segmenten Hallo status Ready heeft zijn als ze zijn al gemaakt.

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. Gebruik Azure portal tooview hello **taken** die zijn gekoppeld aan Hallo **segmenten** en zien welke VM die is uitgevoerd op elk segment. Zie [Data Factory en Batch-integratie](#data-factory-and-batch-integration) sectie voor meer informatie.
7. U ziet de uitvoerbestanden Hallo in Hallo `outputfolder` van `mycontainer` in uw Azure-blobopslag.

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   Hier ziet u vijf uitvoerbestanden, één voor elke invoersegment. Elk Hallo uitvoervenster het volgende bestand inhoud vergelijkbare toohello na uitvoer moet hebben:

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   Hallo volgende diagram illustreert hoe Hallo Data Factory segmenten tootasks in Azure Batch toegewezen. In dit voorbeeld heeft een segment slechts één uitvoeren.

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. Nu gaan we proberen met meerdere bestanden in een map. Bestanden maken: **bestand2.txt samengevoegd**, **file3.txt**, **file4.txt**, en **file5.txt** Hello dezelfde inhoud zoals in bestand.txt in Hallo map: **2015-11-06-01**.
9. In de uitvoermap hello, **verwijderen** Hallo uitvoerbestand: **2015-11-16-01.txt**.
10. Nu in Hallo **OutputDataset** blade, klik met de rechtermuisknop Hallo segment met **segment BEGINTIJD** instellen te**16-11-2015 01:00:00 AM**, en klik op **uitvoeren**toorerun/opnieuw-proceskleuren Hallo segment. Hallo-segment is nu vijf bestanden in plaats van een bestand.

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. Nadat het Hallo-segment wordt uitgevoerd en de status is **gereed**, Controleer Hallo inhoud in het uitvoerbestand Hallo voor dit segment (**2015-11-16-01.txt**) in Hallo `outputfolder` van `mycontainer` in de blob-opslag. Er moet een regel voor elk bestand van Hallo segment.

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> Als u niet 2015 in de Hallo uitvoer-bestand-11-16-01.txt verwijderen kon voordat u met vijf invoerbestanden, ziet u één regel van de vorige segment Hallo uitvoeren en vijf de regels van de huidige segment Hallo uitvoeren. Standaard is Hallo inhoud toegevoegde toooutput bestand als dit al bestaat.
>
>

#### <a name="data-factory-and-batch-integration"></a>Data Factory en Batch-integratie
Hallo Data Factory-service maakt een taak in Azure Batch met de naam van de Hallo: `adf-poolname:job-xxx`.

![Azure Data Factory - Batch-taken](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

Een taak in Hallo-taak is gemaakt voor elke activiteit uitvoering van een segment. Als er 10 segmenten gereed toobe verwerkt, wordt 10 taken worden gemaakt in Hallo-taak. U kunt meer dan één segment parallel worden uitgevoerd als er meerdere rekenknooppunten in de groep Hallo hebben. Als Hallo maximum aantal taken per knooppunt is ingesteld, te berekenen > 1, kunnen er meer dan één segmenteren op Hallo uitgevoerd dezelfde compute.

In dit voorbeeld zijn er vijf segmenten, dus vijf taken in Azure Batch. Hello **gelijktijdigheid** instellen te**5** in Hallo pipeline-JSON-code in Azure Data Factory en **maximum aantal taken per VM** instellen te**2** in Azure Batch groep met **2** virtuele machines, Hallo taken uitgevoerd snelle (Raadpleeg de begin- en eindtijden voor taken).

Gebruik Hallo portal tooview Hallo Batch-job en de bijbehorende taken die gekoppeld aan Hallo zijn **segmenten** en zien welke VM die is uitgevoerd op elk segment.

![Azure Data Factory - taken voor Batch-job](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a>Fouten opsporen in Hallo-pipeline
De foutopsporing bestaat uit enkele basistechnieken:

1. Als invoersegment met de Hallo te niet is ingesteld**gereed**, bevestigen dat de mapstructuur van Hallo invoer juist is en bestand.txt in de invoer mappen Hallo bestaat.

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. In Hallo **Execute** methode van uw aangepaste activiteit, gebruik Hallo **IActivityLogger** object toolog informatie die u helpt oplossen van problemen. in het logboek geregistreerd Hallo-berichten weergegeven in het Hallo-gebruiker\_0-logboekbestand.

   In Hallo **OutputDataset** blade, klikt u op Hallo segment toosee hello **GEGEVENSSEGMENT** blade voor die segment. U ziet **activiteiten bij uitvoering** voor dit segment. Hier ziet u een activiteit die wordt uitgevoerd voor Hallo segment. Als u op **uitvoeren** in de opdrachtbalk hello, begint u een andere activiteit die wordt uitgevoerd voor Hallo hetzelfde segment.

   Wanneer u klikt op Hallo activiteit die wordt uitgevoerd, ziet u Hallo **DETAILS uitvoering van activiteit** blade met een lijst met logboekbestanden. Ziet u de geregistreerde berichten in Hallo **gebruiker\_0 logboek** bestand. Wanneer er een fout optreedt, ziet u drie activiteiten bij uitvoering omdat het maximale aantal pogingen Hallo too3 in Hallo pipeline/activiteits-JSON is ingesteld. Wanneer u klikt op Hallo activiteit die wordt uitgevoerd, ziet u logboekbestanden Hallo tootroubleshoot Hallo fout kunt controleren.

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   Klik in Hallo lijst van logboekbestanden op Hallo **gebruiker 0.log**. In het rechterpaneel Hallo zijn Hallo resultaten van het gebruik van Hallo **IActivityLogger.Write** methode.

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   Controleer de systeem-0.log voor elk systeem foutberichten en uitzonderingen.

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. Hallo omvatten **PDB** bestand in het zip-bestand Hallo zodat Hallo foutdetails beschikt over informatie zoals **aanroepstack** wanneer er een fout optreedt.
4. Alle bestanden in het zip-bestand Hallo Hallo voor Hallo aangepaste activiteit op Hallo moet **bovenste niveau** zonder submappen.

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. Zorg ervoor dat Hallo **assemblyName** (MyDotNetActivity.dll) **entryPoint** (MyDotNetActivityNS.MyDotNetActivity) **packageFile** (customactivitycontainer / MyDotNetActivity.zip) en **packageLinkedService** (moet punt toohello Azure blob-opslag die Hallo zip-bestand bevat) toocorrect waarden zijn ingesteld.
6. Als u een fout en wilt tooreprocess Hallo segment hebt opgelost, met de rechtermuisknop op Hallo segment Hallo **OutputDataset** blade en klik op **uitvoeren**.

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > U ziet een **container** in uw Azure Blob-opslag met de naam: `adfjobs`. Deze container wordt niet automatisch verwijderd, maar u het veilig kunt verwijderen nadat u klaar bent met testen Hallo-oplossing. Op deze manier Hallo Data Factory-oplossing maakt u een Azure-Batch **taak** met de naam: `adf-\<pool ID/name\>:job-0000000001`. Nadat u Hallo oplossing als u dit wilt testen, kunt u deze taak verwijderen.
   >
   >
7. Hallo aangepaste activiteit gebruikt geen Hallo **app.config** bestand van het pakket. Dus als uw code wordt een verbindingsreeksen uit het Hallo-configuratiebestand gelezen, werkt het niet tijdens runtime. Hallo beste wanneer toohold met behulp van Azure Batch is geen geheimen in een **Azure KeyVault**, gebruikt u een certificaat gebaseerde service principal tooprotect hello keyvault en distribueren Hallo certificaat tooAzure Batch-pool. Hallo aangepaste activiteit .NET vervolgens toegang tot geheimen Hallo KeyVault tijdens runtime. Deze oplossing is een algemene en tooany type geheim, niet alleen verbindingsreeks kunt schalen.

    Er is een eenvoudiger tijdelijke oplossing (maar niet aanbevolen): kunt u een **Azure SQL gekoppelde service** met verbindingstekenreeksinstellingen, maken een gegevensset dat wordt gebruikt Hallo gekoppelde service en de keten Hallo dataset als een dummy invoergegevensset toohello aangepaste .NET-activiteit. U kunt vervolgens toegang Hallo gekoppeld de verbindingsreeks van de service in Hallo aangepaste activiteitscode en deze tijdens runtime werken moet.  

#### <a name="extend-hello-sample"></a>Hallo voorbeeld uitbreiden
U kunt uitbreiden in dit voorbeeld toolearn informatie over Azure Data Factory en Azure Batch-functies. Bijvoorbeeld tooprocess segmenten in een ander tijdsbereik Hallo stappen te volgen:

1. Toevoegen van de volgende submappen in Hallo Hallo `inputfolder`: 2015-11-16-05 2015-11-16-06 201-11-16-07, 2011-11-16-08, 2015-11-16-09 en plaats invoerbestanden in deze mappen. Hallo-eindtijd voor de pijplijn Hallo van wijzigen `2015-11-16T05:00:00Z` te`2015-11-16T10:00:00Z`. In Hallo **diagramweergave**, dubbelklikt u op Hallo **InputDataset**, en controleer of de invoersegmenten één keer Hallo gereed zijn. Dubbelklik op **OuptutDataset** toosee Hallo status van de uitvoer-segmenten. Als ze zich in de status Ready heeft, controleert u Hallo uitvoermap voor uitvoerbestanden Hallo.
2. Vergroten of verkleinen Hallo **gelijktijdigheid** instelling toounderstand hoe dit van invloed op prestaties van uw oplossing Hallo vooral Hallo verwerken die wordt uitgevoerd op Azure Batch. (Zie stap 4: maken en uitvoeren van Hallo pijplijn voor meer informatie over Hallo **gelijktijdigheid** instelling.)
3. Een pool maken met de hogere en kleine **maximum aantal taken per VM**. toouse Hallo u hebt gemaakt, nieuwe pool update Hallo gekoppelde Azure-Batch-service in Hallo Data Factory-oplossing. (Zie stap 4: maken en uitvoeren van Hallo pijplijn voor meer informatie over Hallo **maximum aantal taken per VM** instelling.)
4. Maken van een Azure Batch-pool met **automatisch schalen** functie. Automatisch vergroten/verkleinen rekenknooppunten in een Azure Batch-pool is Hallo dynamische aanpassing van de verwerkingskracht die worden gebruikt door de toepassing. 

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
5. In de voorbeeld-oplossing Hallo Hallo **Execute** methode aanroept Hallo **Calculate** methode die een invoergegevens segment tooproduce een gegevenssegment uitvoer verwerkt. U kunt uw eigen methode tooprocess invoergegevens en vervang Hallo Calculate methodeaanroep in Hallo Execute-methode door een aanroep van tooyour methode schrijven.

### <a name="next-steps-consume-hello-data"></a>Volgende stappen: Hallo gegevens gebruiken
Nadat u gegevens verwerken, kunt u het verbruiken met online hulpmiddelen zoals **Microsoft Power BI**. Hier vindt u koppelingen toohelp begrijpen van Power BI en hoe toouse in Azure:

* [Een gegevensset in Power BI verkennen](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [Aan de slag met Power BI Desktop Hallo](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [Vernieuwen van gegevens in Power BI](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [Azure en Power BI - basisoverzicht](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a>Verwijzingen
* [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)

  * [Inleiding tooAzure Data Factory-service](data-factory-introduction.md)
  * [Aan de slag met Azure Data Factory](data-factory-build-your-first-pipeline.md)
  * [Aangepaste activiteiten gebruiken in een Azure Data Factory-pijplijn](data-factory-use-custom-activities.md)
* [Azure Batch](https://azure.microsoft.com/documentation/services/batch/)

  * [Basisbeginselen van Azure Batch](../batch/batch-technical-overview.md)
  * [Overzicht van Azure Batch-functies](../batch/batch-api-basics.md)
  * [Maken en beheren van Azure Batch-account in hello Azure-portal](../batch/batch-account-create-portal.md)
  * [Aan de slag met Azure Batch-bibliotheek .NET](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
