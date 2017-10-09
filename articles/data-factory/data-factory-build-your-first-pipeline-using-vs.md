---
title: aaaBuild uw eerste gegevensfactory (Visual Studio) | Microsoft Docs
description: In deze zelfstudie maakt u een Azure Data Factory-voorbeeldpijplijn met behulp van Visual Studio.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7398c0c9-7a03-4628-94b3-f2aaef4a72c5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 0c5eb01b685d978d80916da0293cc2d3701b2d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a>Zelfstudie: Een data factory maken met behulp van Visual Studio
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [Overzicht en vereisten](data-factory-build-your-first-pipeline.md)
> * [Azure Portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager-sjabloon](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)

Deze zelfstudie leert u hoe toocreate een Azure data factory met behulp van Visual Studio. U een Visual Studio-project met behulp van de Data Factory-projectsjabloon Hallo maken, het definiëren van Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) in JSON-indeling en vervolgens publiceren/implementeren deze entiteiten toohello cloud. 

Hallo-pijplijn in deze zelfstudie is één activiteit: **HDInsight Hive-activiteit**. Deze activiteit wordt een hive-script uitgevoerd op een Azure HDInsight-cluster dat transformaties invoergegevens gegevens tooproduce uitvoer. Hallo pijplijn is geplande toorun wanneer een maand tussen Hallo begin- en eindtijden opgegeven. 

> [!NOTE]
> In deze zelfstudie wordt niet getoond hoe u gegevens met Azure Data Factory kopieert. Voor een zelfstudie over het toocopy van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: gegevens kopiëren van Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Een pijplijn kan meer dan één activiteit hebben. En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit. Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.


## <a name="walkthrough-create-and-publish-data-factory-entities"></a>Walkthrough: Data Factory-entiteiten maken en publiceren
Hier volgen Hallo stappen die u als onderdeel van dit scenario uitvoert:

1. Maak twee gekoppelde services: **AzureStorageLinkedService1** en **HDInsightOnDemandLinkedService1**. 
   
    In deze zelfstudie Hallo invoer-en uitvoergegevens voor hive-activiteit Hallo zijn dezelfde Azure Blob Storage. U gebruikt een bellen op HDInsight-cluster tooprocess bestaande invoergegevens tooproduce uitvoergegevens. Hallo bellen op HDInsight-cluster wordt automatisch voor u gemaakt door Azure Data Factory tijdens het uitvoeren als de invoergegevens Hallo gereed toobe verwerkt is. U moet toolink uw gegevens opslaat of tooyour gegevensfactory berekent zodat Hallo Data Factory-service verbinding van toothem tijdens runtime maken kan. Daarom moet u koppelen van uw Azure Storage-Account toohello data factory via Hallo AzureStorageLinkedService1 en koppelen van een HDInsight-cluster op aanvraag via Hallo HDInsightOnDemandLinkedService1. Wanneer u publiceert, geeft u Hallo-naam voor Hallo data factory toobe gemaakt of een bestaande gegevensfactory.  
2. Twee gegevenssets maken: **InputDataset** en **OutputDataset**, die staan voor Hallo invoer-en uitvoergegevens die zijn opgeslagen in hello Azure blob-opslag. 
   
    Deze gegevensset definities Raadpleeg toohello u hebt gemaakt in de vorige stap Hallo gekoppelde Azure Storage-service. Voor Hallo InputDataset, geef Hallo blob-container (adfgetstarted) en map (inptutdata) met een blob met de invoergegevens Hallo Hallo. U Hallo blob-container (adfgetstarted) opgeven voor Hallo OutputDataset, en Hallo-map (partitioneddata) die uitvoergegevens Hallo bevat. U geeft ook andere eigenschappen op, zoals de structuur, de beschikbaarheid en het beleid.
3. Maak een pijplijn met de naam **MyFirstPipeline**. 
  
    In dit overzicht Hallo pipeline heeft slechts één activiteit: **HDInsight Hive-activiteit**. Deze activiteit transformatie invoergegevens tooproduce uitvoergegevens door een hive-script uitgevoerd op een HDInsight-cluster op aanvraag. Zie toolearn meer informatie over het hive-activiteit [Hive-activiteit](data-factory-hive-activity.md) 
4. Maak een data factory met de naam **DataFactoryUsingVS**. Hallo gegevensfactory en alle Data Factory-entiteiten (gekoppelde services, tabellen en pijplijn Hallo) implementeren.
5. Nadat u publiceert, gebruikt u Azure portal-blades en beheer-App voor bewaking en toomonitor Hallo pijplijn. 
  
### <a name="prerequisites"></a>Vereisten
1. Lees [overzicht van de zelfstudie](data-factory-build-your-first-pipeline.md) artikel en volledige Hallo **vereiste** stappen. U kunt ook selecteren Hallo **overzicht en vereisten** optie in de keuzelijst Hallo op Hallo bovenste tooswitch toohello artikel. Nadat u Hallo vereisten hebt voltooid, schakelen back toothis artikel door te selecteren **Visual Studio** optie in de vervolgkeuzelijst Hallo.
2. toocreate Data Factory-exemplaren, moet u lid zijn van Hallo [Data Factory Inzender](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol op het niveau van de Hallo abonnement/resourcegroep.  
3. Hallo volgende op uw computer geïnstalleerd, moet u hebben:
   * Visual Studio 2013 of Visual Studio 2015
   * Download de Azure SDK voor Visual Studio 2013 of Visual Studio 2015. Navigeer te[Azure-downloadpagina](https://azure.microsoft.com/downloads/) en klik op **VS 2013** of **VS 2015** in Hallo **.NET** sectie.
   * Download de nieuwste Azure Data Factory-invoegtoepassing Hallo voor Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) of [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). U kunt ook Hallo invoegtoepassing Hallo volgende stappen uit als volgt bijwerken: op het menu Hallo **extra** -> **uitbreidingen en Updates** -> **Online**  ->  **Visual Studio-galerie** -> **Microsoft Azure Data Factory-hulpprogramma's voor Visual Studio** -> **Update**.

Nu gaan we toocreate Visual Studio een Azure data factory gebruiken.

### <a name="create-visual-studio-project"></a>Een Visual Studio-project maken
1. Open **Visual Studio 2013** of **Visual Studio 2015**. Klik op **bestand**, wijst u te**nieuw**, en klik op **Project**. U ziet Hallo **nieuw Project** in het dialoogvenster.  
2. In Hallo **nieuw Project** dialoogvenster, selecteer Hallo **DataFactory** sjabloon en klikt u op **Empty Data Factory Project**.   

    ![Het dialoogvenster New Project](./media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. Voer een **naam** voor Hallo-project **locatie**, en een naam voor Hallo **oplossing**, en klik op **OK**.

    ![Solution Explorer](./media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a>Gekoppelde services maken
In deze stap maakt u twee gekoppelde services: **Azure Storage** en **HDInsight op aanvraag**. 

Hello Azure Storage gekoppelde service uw Azure Storage-account toohello data factory door Hallo verbindingsinformatie te verstrekken. Data Factory-service gebruikt de verbindingsreeks Hallo van Hallo gekoppelde service-instelling tooconnect toohello Azure storage tijdens runtime. Deze opslag invoer bevat en uitvoergegevens voor Hallo pijplijn en Hallo hive-scriptbestand gebruikt door Hallo hive-activiteit. 

Met de gekoppelde HDInsight-service op aanvraag, wordt Hallo HDInsight-cluster automatisch gemaakt tijdens runtime wanneer Hallo invoergegevens tooprocessed gereed is. Hallo-cluster wordt verwijderd nadat het verwerken is voltooid en niet-actieve Hallo opgegeven tijdsduur. 

> [!NOTE]
> U kunt een gegevensfactory maken door op te geven van de naam en instellingen op Hallo moment van publicatie van uw Data Factory-oplossing.

#### <a name="create-azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service maken
1. Met de rechtermuisknop op **gekoppelde Services** in solution explorer Hallo punt te**toevoegen**, en klik op **Nieuw Item**.      
2. In Hallo **Add New Item** dialoogvenster, **Azure Storage Linked Service** in Hallo lijst en klik op **toevoegen**.
    ![Gekoppelde Azure Storage-service](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)
3. Vervang `<accountname>` en `<accountkey>` met Hallo-naam van uw Azure storage-account en de bijbehorende sleutel. toolearn hoe tooget uw opslag heeft toegang tot sleutel, raadpleegt u Hallo informatie over hoe tooview, kopiëren en opnieuw genereren opslag toegangstoetsen in [uw opslagaccount beheren](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
    ![Gekoppelde Azure Storage-service](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)
4. Hallo opslaan **AzureStorageLinkedService1.json** bestand.

#### <a name="create-azure-hdinsight-linked-service"></a>Een gekoppelde HDInsight-service maken
1. In Hallo **Solution Explorer**, met de rechtermuisknop op **gekoppelde Services**, wijst u te**toevoegen**, en klik op **Nieuw Item**.
2. Selecteer **HDInsight On Demand Linked Service** en klik op **Add**.
3. Vervang Hallo **JSON** Hello JSON te volgen:

     ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
        "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService1"
            }
        }
    }
    ```

    Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:

    Eigenschap | Beschrijving
    -------- | ----------- 
    ClusterSize | Hiermee wordt de grootte Hallo Hallo HDInsight Hadoop-cluster.
    TimeToLive | Hiermee geeft u op dat niet-actieve tijd Hallo voor Hallo HDInsight-cluster, voordat deze wordt verwijderd.
    linkedServiceName | Hiermee geeft u Hallo storage-account dat is gebruikt toostore Hallo logboeken die worden gegenereerd door HDInsight Hadoop-cluster. 

    > [!IMPORTANT]
    > Hallo HDInsight-cluster maakt een **standaardcontainer** in Hallo-blobopslag die u hebt opgegeven in Hallo JSON (linkedServiceName). HDInsight verwijdert deze container niet wanneer Hallo-cluster is verwijderd. Dit gedrag is standaard. Met de gekoppelde service HDInsight op aanvraag wordt er steeds een HDInsight-cluster gemaakt wanneer er een segment wordt verwerkt, tenzij er een bestaand livecluster is (timeToLive). Hallo-cluster wordt automatisch verwijderd als het Hallo-verwerking is voltooid.
    > 
    > Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag. Als u niet ze hoeft voor het oplossen van problemen met taken hello, kunt u toodelete ze tooreduce Hallo opslag kosten. Hallo-namen van deze containers een patroon volgen: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`. Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) toodelete containers in uw Azure-blobopslag.

    Zie de [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Gekoppelde Compute Services) voor meer informatie over JSON-eigenschappen. 
4. Hallo opslaan **HDInsightOnDemandLinkedService1.json** bestand.

### <a name="create-datasets"></a>Gegevenssets maken
In deze stap maakt u gegevenssets toorepresent Hallo invoer maken en uitvoergegevens voor Hive-verwerking. Deze gegevenssets verwijzen toohello **AzureStorageLinkedService1** u eerder in deze zelfstudie hebt gemaakt. Hallo gekoppelde service verwijst tooan Azure Storage-account en gegevenssets vindt u container, map en bestandsnaam in Hallo opslag van de invoer- en uitvoergegevens.   

#### <a name="create-input-dataset"></a>Invoergegevensset maken
1. In Hallo **Solution Explorer**, met de rechtermuisknop op **tabellen**, wijst u te**toevoegen**, en klik op **Nieuw Item**.
2. Selecteer **Azure Blob** in Hallo-lijst, wijzig Hallo-naam van Hallo-bestand te**InputDataSet.json**, en klik op **toevoegen**.
3. Vervang Hallo **JSON** in Hallo-editor met Hallo volgende JSON-fragment:

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
            "typeProperties": {
                "fileName": "input.log",
                "folderPath": "adfgetstarted/inputdata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            },
            "external": true,
            "policy": {}
        }
    }
    ```
    Deze JSON-fragment een gegevensset met de naam definieert **AzureBlobInput** die staat voor invoergegevens van hive-activiteit in de pijplijn Hallo Hallo. U opgeven dat Hallo invoergegevens in de blob-container Hallo aangeroepen bevinden zich `adfgetstarted` en Hallo map met de naam `inputdata`.

    Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:

    Eigenschap | Beschrijving |
    -------- | ----------- |
    type |Hallo type wordt ingesteld te**AzureBlob** omdat de gegevens zich in Azure Blob Storage.
    linkedServiceName | Verwijst toohello AzureStorageLinkedService1 die u eerder hebt gemaakt.
    fileName |Deze eigenschap is optioneel. Als u deze eigenschap niet opgeeft, worden alle Hallo-bestanden uit folderPath Hallo opgenomen. In dit geval wordt alleen Hallo input.log verwerkt.
    type | Hallo-logboekbestanden zijn tekstbestanden, zodat we TextFormat gebruiken. |
    columnDelimiter | kolommen in Hallo logboekbestanden worden gescheiden door een kommateken hello (`,`)
    frequency/interval | frequentie tooMonth ingesteld en interval is 1, wat betekent dat Hallo invoersegmenten één keer per maand beschikbaar zijn.
    external | Deze eigenschap is tootrue ingesteld als invoergegevens voor activiteit Hallo Hallo niet worden gegenereerd door Hallo pijplijn. Deze eigenschap wordt alleen opgegeven voor invoergegevenssets. Voor invoergegevensset Hallo van de eerste activiteit Hallo altijd ingesteld dat deze tootrue.
4. Hallo opslaan **InputDataset.json** bestand.

#### <a name="create-output-dataset"></a>Uitvoergegevensset maken
U maakt nu Hallo gegevensset toorepresent uitvoer uitvoergegevens opgeslagen in hello Azure Blob-opslag.

1. In Hallo **Solution Explorer**, met de rechtermuisknop op **tabellen**, wijst u te**toevoegen**, en klik op **Nieuw Item**.
2. Selecteer **Azure Blob** in Hallo-lijst, wijzig Hallo-naam van Hallo-bestand te**OutputDataset.json**, en klik op **toevoegen**.
3. Vervang Hallo **JSON** in Hallo-editor met Hallo JSON te volgen:
    
    ```json
    {
        "name": "AzureBlobOutput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
            "typeProperties": {
                "folderPath": "adfgetstarted/partitioneddata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            }
        }
    }
    ```
    Hallo JSON-fragment een gegevensset met de naam definieert **AzureBlobOutput** dat vertegenwoordigt uitvoergegevens die wordt geproduceerd door Hallo hive-activiteit in Hallo pijplijn. U opgeven dat gegevens wordt geproduceerd door de hive-activiteit Hallo Hallo-uitvoer wordt geplaatst in blob-container Hallo aangeroepen `adfgetstarted` en Hallo map met de naam `partitioneddata`. 
    
    Hallo **beschikbaarheid** sectie geeft die Hallo-uitvoergegevensset op maandelijkse basis wordt geproduceerd. Hallo uitvoer gegevensset stations Hallo planning van Hallo pijplijn. Hallo-pijplijn wordt uitgevoerd tussen de begin- en eindtijden per maand. 

    Zie **hello invoergegevensset maken** sectie voor beschrijvingen van deze eigenschappen. U instelt geen Hallo externe eigenschap op een uitvoergegevensset omdat Hallo gegevensset wordt geproduceerd door Hallo pijplijn.
4. Hallo opslaan **OutputDataset.json** bestand.

### <a name="create-pipeline"></a>Pijplijn maken
U hebt gemaakt Hallo gekoppelde Azure Storage-service en invoer- en uitvoergegevenssets tot nu toe. Nu gaat u een pijplijn met een **HDInsightHive**-activiteit maken. Hallo **invoer** voor Hallo hive activiteit te ingesteld**AzureBlobInput** en **uitvoer** te is ingesteld,**AzureBlobOutput**. Een segment van een invoergegevensset maandelijks beschikbaar is (frequency: Month, interval: 1), en Hallo uitvoer segment wordt maandelijks geproduceerd te. 

1. In Hallo **Solution Explorer**, met de rechtermuisknop op **pijplijnen**, wijst u te**toevoegen**, en klik op **Nieuw Item.**
2. Selecteer **Hive Transformation Pipeline** in Hallo lijst en klik op **toevoegen**.
3. Vervang Hallo **JSON** Hello codefragment te volgen:

    > [!IMPORTANT]
    > Vervang `<storageaccountname>` met Hallo-naam van uw opslagaccount.

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService1",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                        }
                    },
                    "inputs": [
                        {
                            "name": "AzureBlobInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobOutput"
                        }
                    ],
                    "policy": {
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2016-04-01T00:00:00Z",
            "end": "2016-04-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    > [!IMPORTANT]
    > Vervang `<storageaccountname>` met Hallo-naam van uw opslagaccount.

    Hallo JSON-codefragment definieert een pijplijn die uit een enkele activiteit (Hive-activiteit bestaat). Deze activiteit wordt uitgevoerd op een invoergegevens van Hive-script tooprocess een bellen op HDInsight-cluster tooproduce uitvoergegevens. In Hallo gedeelte van de activiteiten van Hallo pijplijn JSON, ziet u slechts één activiteit in Hallo matrix met soort te**HDInsightHive**. 

    In de eigenschappen van type Hallo die specifieke tooHDInsight Hive-activiteit, kunt u opgeven welke gekoppelde Azure Storage-service heeft Hallo hive-scriptbestand, Hallo pad toohello scriptbestand en parameters toohello scriptbestand. 

    Hallo Hive-scriptbestand **partitionweblogs.hql**, wordt opgeslagen in hello Azure-opslagaccount (opgegeven door de scriptLinkedService Hallo) en in Hallo `script` map in container Hallo `adfgetstarted`.

    Hallo `defines` sectie is gebruikte toospecify Hallo runtime-instellingen die toohello hive-script worden doorgegeven als Hive-configuratiewaarden (bijvoorbeeld `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.

    Hallo **start** en **end** eigenschappen van de pijplijn Hallo geeft Hallo actieve periode van Hallo-pijplijn. U hebt geconfigureerd Hallo gegevensset toobe geproduceerd maandelijks, daarom alleen wanneer het segment wordt geproduceerd door de pijplijn hello (omdat Hallo maand hetzelfde in de begin- en einddatums).

    In Hallo activiteits-JSON geeft u opgeven dat Hallo Hive-script wordt uitgevoerd op Hallo berekening die is opgegeven door Hallo **linkedServiceName** – **HDInsightOnDemandLinkedService**.
4. Hallo opslaan **HiveActivity1.json** bestand.

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a>partitionweblogs.hql en input.log toevoegen als afhankelijkheid
1. Met de rechtermuisknop op **afhankelijkheden** in Hallo **Solution Explorer** venster te verwijzen**toevoegen**, en klik op **bestaand Item**.  
2. Navigeer toohello **C:\ADFGettingStarted** en selecteer **partitionweblogs.hql**, **input.log** bestanden en klikt u op **toevoegen**. U hebt deze twee bestanden gemaakt als onderdeel van de vereisten van Hallo [overzicht van de zelfstudie](data-factory-build-your-first-pipeline.md).

Wanneer u Hallo oplossing in de volgende stap hello publiceert, Hallo **partitionweblogs.hql** bestand is geüpload toohello **script** map in Hallo `adfgetstarted` blob-container.   

### <a name="publishdeploy-data-factory-entities"></a>Data Factory-entiteiten publiceren/implementeren
In deze stap maakt publiceren u Hallo Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) in uw project toohello Azure Data Factory-service. In Hallo proces van publiceren, moet u Hallo-naam van uw gegevensfactory opgeven. 

1. Met de rechtermuisknop op het project in Solution Explorer Hallo en klik op **publiceren**.
2. Als u ziet **tooyour Microsoft-account aanmelden** in het dialoogvenster Geef uw referenties voor het Hallo-account met Azure-abonnement en klikt u op **aanmelden**.
3. U ziet Hallo in het dialoogvenster te volgen:

   ![Het dialoogvenster Publish](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. In Hallo **Configure data factory** pagina, Hallo volgende stappen:

    ![Publiceren - Nieuwe data factory-instellingen](media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. Selecteer **Create New Data Factory**.
   2. Voer een unieke **naam** voor Hallo data factory. Bijvoorbeeld: **DataFactoryUsingVS09152016**. Hallo-naam moet uniek zijn.
   3. Selecteer de juiste abonnement Hallo voor Hallo **abonnement** veld. 
        > [!IMPORTANT]
        > Als u een abonnement niet ziet, zorg ervoor dat u aangemeld met een account dat een beheerder of co-beheerder van het Hallo-abonnement.
   4. Selecteer Hallo **resourcegroep** voor Hallo data factory toobe gemaakt.
   5. Selecteer Hallo **regio** voor Hallo data factory.
   6. Klik op **volgende** tooswitch toohello **Publish Items** pagina. (Druk op **tabblad** toomove buiten Hallo naam veld tooif hello **volgende** knop is uitgeschakeld.)

    > [!IMPORTANT]
    > Als u de foutmelding Hallo **Data factory-naam 'DataFactoryUsingVS' is niet beschikbaar** tijdens het publiceren Hallo-naam (bijvoorbeeld yournameDataFactoryUsingVS) wijzigen. Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.   
1. In Hallo **Publish Items** pagina, zorg ervoor dat alle Data Factory-entiteiten zijn geselecteerd en klik op Hallo **volgende** tooswitch toohello **samenvatting** pagina.

    ![Pagina Items publiceren](media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. Controleer Hallo samenvatting en klik op **volgende** toostart Hallo implementatie proces en bekijkt hello **Implementatiestatus**.

    ![Overzichtspagina](media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. In Hallo **Implementatiestatus** pagina ziet u Hallo status van implementatieproces Hallo. Klik op Voltooien nadat het Hallo-implementatie is voltooid.

Belangrijke punten toonote:

- Als u de foutmelding Hallo: **dit abonnement is niet geregistreerd toouse namespace Microsoft.DataFactory**, voer een van de volgende Hallo en probeer opnieuw te publiceren:
    - Voer in Azure PowerShell Hallo opdracht tooregister Hallo Data Factory-provider te volgen.
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        Die Hallo Data Factory-provider is geregistreerd, kunt u na de opdracht tooconfirm Hallo uitvoeren.

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - Aanmelding via het Azure-abonnement in toohello Hallo [Azure-portal](https://portal.azure.com) en navigeer tooa Data Factory-blade of maak een gegevensfactory in hello Azure-portal. Deze actie automatisch Hallo provider voor u geregistreerd.
- Hallo-naam van de gegevensfactory Hallo kan worden geregistreerd als DNS-naam in toekomstige Hallo en daarmee ook voor iedereen zichtbaar.
- toocreate Data Factory-exemplaren, moet u een beheerder toobe of co-beheerder van hello Azure-abonnement

### <a name="monitor-pipeline"></a>De pijplijn bewaken
In deze stap maakt bewaken u Hallo pijplijn diagramweergave van Hallo gegevensfactory. 

#### <a name="monitor-pipeline-using-diagram-view"></a>De pijplijn bewaken met Diagramweergave
1. Meld u bij toohello [Azure-portal](https://portal.azure.com/), Hallo volgende stappen:
   1. Klik op **Meer services** en op **Gegevensfactory's**.
       
        ![Door gegevensfactory’s bladeren](./media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. Selecteer Hallo-naam van uw gegevensfactory (bijvoorbeeld: **DataFactoryUsingVS09152016**) uit de lijst Hallo van data Factory.
   
       ![Uw gegevensfactory selecteren](./media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. In de startpagina van uw gegevensfactory hello, klikt u op **Diagram**.

    ![Tegel Diagram](./media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. In de diagramweergave hello ziet u een overzicht van Hallo pijplijnen en gegevenssets die in deze zelfstudie worden gebruikt.

    ![Diagramweergave](./media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. tooview alle activiteiten in de pijplijn voor hello, klik met de rechtermuisknop pijplijn in Hallo diagram en klikt u op pijplijn openen.

    ![Menu Pijplijn openen](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. Controleer of u Hallo HDInsightHive-activiteit in Hallo pijplijn.

    ![Pijplijnweergave openen](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    back-toonavigate toohello vorige weergave, klikt u op **Data factory** in Hallo breadcrumb menu Hallo bovenaan.
6. In Hallo **diagramweergave**, dubbelklikt u op Hallo gegevensset **AzureBlobInput**. Bevestig dat segment Hallo **gereed** status. Het kan enkele minuten voor Hallo segment tooshow duren status Ready heeft. Als deze niet is gebeurd nadat u enige tijd wacht, bekijken of er Hallo invoerbestand (input.log in de juiste container Hallo geplaatst) (`adfgetstarted`) en de map (`inputdata`). En zorg ervoor dat Hallo **externe** eigenschap op Hallo invoergegevensset is ingesteld, te**true**. 

   ![Invoersegment met de status Gereed](./media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. Klik op **X** tooclose **AzureBlobInput** blade.
8. In Hallo **diagramweergave**, dubbelklikt u op Hallo gegevensset **AzureBlobOutput**. U ziet dat Hallo-segment dat momenteel wordt verwerkt.

   ![Gegevensset](./media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. Wanneer het verwerken is voltooid, ziet u Hallo segment **gereed** status.

   > [!IMPORTANT]
   > Het maken van een on-demand HDInsight-cluster duurt normaal gesproken enige tijd (ongeveer 20 minuten). Daarom verwachten Hallo pijplijn tootake **ongeveer 30 minuten** tooprocess Hallo segment.  
   
    ![Gegevensset](./media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. Wanneer Hallo segment is in **gereed** staat, controleert u Hallo `partitioneddata` map in Hallo `adfgetstarted` container in uw blobopslag voor Hallo uitvoergegevens.  

    ![Uitvoergegevens](./media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. Klik op Hallo segment toosee details over deze in een **gegevenssegment** blade.

    ![Details gegevenssegment](./media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. Klik op een activiteit die wordt uitgevoerd in Hallo **activiteit wordt uitgevoerd lijst** toosee details over een activiteit (Hive-activiteit in ons scenario) uitgevoerd in een **details uitvoering van activiteit** venster. 
  
    ![Details uitvoering van activiteit](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    Uit Hallo-logboekbestanden ziet u Hallo Hive-query die is uitgevoerd en statusinformatie. Deze logboeken komen van pas bij het oplossen van problemen.  

Zie [gegevenssets en pijplijn bewaken](data-factory-monitor-manage-pipelines.md) voor instructies over hoe toouse hello Azure portal toomonitor Hallo pijplijn en gegevenssets u hebt gemaakt in deze zelfstudie.

#### <a name="monitor-pipeline-using-monitor--manage-app"></a>De pijplijn bewaken met de app Bewaking en beheer
U kunt ook controleren en beheren van toepassing toomonitor uw pijplijnen. Zie [Azure Data Factory-pijplijnen bewaken en beheren met de app voor bewaking en beheer](data-factory-monitor-manage-app.md) voor meer informatie over het gebruik van deze toepassing.

1. Klik op de tegel Bewaking en beheer.

    ![De tegel Bewaking en beheer](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. De toepassing Bewaking en beheer wordt weergegeven. Wijziging Hallo **begintijd** en **eindtijd** toomatch start (01-04-2016 12:00 A.M.)- en eindtijden (04-02-2016 12:00 uur) van uw pijplijn en klik op **toepassen**.

    ![De app Bewaking en beheer](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. toosee details over een activiteitvenster selecteren in Hallo **Activiteitsvensters lijst** toosee details over deze.
    ![Details van activiteitsvenster](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)

> [!IMPORTANT]
> Hallo-invoerbestand wordt verwijderd zodra het Hallo-segment is verwerkt. Dus als u toorerun Hallo segment wilt of zelfstudie opnieuw hello, uploadt Hallo invoerbestand (input.log) toohello `inputdata` map Hallo `adfgetstarted` container.

### <a name="additional-notes"></a>Aanvullende opmerkingen
- Een gegevensfactory kan één of meer pijplijnen hebben. Een pijplijn kan één of meer activiteiten bevatten. Bijvoorbeeld invoergegevens een Kopieeractiviteit toocopy-gegevens van een doelgegevensopslagplaats tooa bron en het toorun in een HDInsight Hive-activiteit een Hive-script tootransform. Zie [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor alle bronnen en put wordt ondersteund door Hallo Kopieeractiviteit Hallo. Zie [gekoppelde services berekenen](data-factory-compute-linked-services.md) voor Hallo overzicht van de compute-services die door Data Factory worden ondersteund.
- Gekoppelde services worden gegevensarchieven of compute-services tooan Azure-gegevensfactory. Zie [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor alle bronnen en put wordt ondersteund door Hallo Kopieeractiviteit Hallo. Zie [gekoppelde services berekenen](data-factory-compute-linked-services.md) voor Hallo overzicht van de compute-services die door Data Factory worden ondersteund en [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) die erop kunt uitvoeren.
- Zie [verplaatsen van gegevens uit / tooAzure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) voor meer informatie over de JSON-eigenschappen die in Hallo gekoppelde Azure Storage-servicedefinitie.
- U kunt uw eigen HDInsight-cluster gebruiken in plaats van een on-demand HDInsight-cluster. Zie [Gekoppelde services berekenen](data-factory-compute-linked-services.md) voor meer informatie.
-  Hallo Data Factory maakt een **op basis van Linux** HDInsight-cluster voor u Hello voorafgaand aan JSON. Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.
- Hallo HDInsight-cluster maakt een **standaardcontainer** in Hallo-blobopslag die u hebt opgegeven in Hallo JSON (linkedServiceName). HDInsight verwijdert deze container niet wanneer Hallo-cluster is verwijderd. Dit gedrag is standaard. Met de gekoppelde service HDInsight op aanvraag wordt er steeds een HDInsight-cluster gemaakt wanneer er een segment wordt verwerkt, tenzij er een bestaand livecluster is (timeToLive). Hallo-cluster wordt automatisch verwijderd als het Hallo-verwerking is voltooid.
    
    Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag. Als u niet ze hoeft voor het oplossen van problemen met taken hello, kunt u toodelete ze tooreduce Hallo opslag kosten. Hallo-namen van deze containers een patroon volgen: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`. Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) toodelete containers in uw Azure-blobopslag.
- Uitvoergegevensset is momenteel welke stations Hallo planning, dus u een uitvoergegevensset maken moet, zelfs als Hallo activiteit geen uitvoer produceert. Als Hallo activiteit geen invoer neemt, kunt u maken Hallo invoergegevensset overslaan. 
- In deze zelfstudie wordt niet getoond hoe u gegevens met Azure Data Factory kopieert. Voor een zelfstudie over het toocopy van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: gegevens kopiëren van Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).


## <a name="use-server-explorer-tooview-data-factories"></a>Server Explorer tooview data Factory gebruiken
1. In **Visual Studio**, klikt u op **weergave** op Hallo van menu en klik op **Server Explorer**.
2. Vouw in Server Explorer-venster Hallo **Azure** en vouw **Data Factory**. Als u ziet **tooVisual Studio aanmelden**, Voer Hallo **account** die zijn gekoppeld aan uw Azure-abonnement en klik op **doorgaan**. Voer het **wachtwoord** in en klik op **Sign in**. Visual Studio haalt tooget informatie over alle Azure data factory's in uw abonnement. Hallo-status van deze bewerking in Hallo weergegeven **Data Factory Task List** venster.

    ![Server Explorer](./media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. U kunt met de rechtermuisknop op een gegevensfactory en selecteer **tooNew Export Data Factory Project** toocreate een Visual Studio-project op basis van een bestaande gegevensfactory.

    ![Een gegevensfactory exporteren](./media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

## <a name="update-data-factory-tools-for-visual-studio"></a>Data Factory-hulpprogramma's voor Visual Studio bijwerken
tooupdate Azure Data Factory-hulpprogramma's voor Visual Studio Hallo stappen te volgen:

1. Klik op **extra** op Hallo menu en selecteer **uitbreidingen en Updates**.
2. Selecteer **Updates** in Hallo linkerdeelvenster en selecteer vervolgens **Visual Studio-galerie**.
3. Selecteer **Azure Data Factory-hulpprogramma's voor Visual Studio** en klik op **Bijwerken**. Als u deze vermelding niet ziet, hebt u al de meest recente versie Hallo Hallo-hulpprogramma's.

## <a name="use-configuration-files"></a>Configuratiebestanden gebruiken
U kunt de configuratiebestanden in Visual Studio tooconfigure eigenschappen voor de gekoppelde services/tabellen/pijplijnen anders voor elke omgeving.

Houd rekening met Hallo volgende JSON-definitie voor een gekoppelde Azure Storage-service. toospecify **connectionString** met verschillende waarden voor accountname en accountkey op basis van het Hallo-omgeving (ontwikkeling/tests/productie) toowhich u Data Factory-entiteiten implementeert. U kunt dit gedrag bewerkstelligen door een afzonderlijk configuratiebestand te gebruiken voor elke omgeving.

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="add-a-configuration-file"></a>Een configuratiebestand toevoegen
Voeg een configuratiebestand voor elke omgeving toe door Hallo volgende stappen uit te voeren:   

1. Met de rechtermuisknop op Hallo Data Factory-project in Visual Studio-oplossing, wijst u te**toevoegen**, en klik op **nieuw item**.
2. Selecteer **Config** Selecteer in de lijst met geïnstalleerde sjablonen aan de linkerkant Hallo Hallo **configuratiebestand**, voer een **naam** voor Hallo configuratie bestand en klik op **Toevoegen**.

    ![Een configuratiebestand toevoegen](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. Configuratieparameters en hun waarden in de volgende indeling Hallo toevoegen:

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    In dit voorbeeld configureert u de eigenschap connectionString van een gekoppelde Azure Storage-service en een gekoppelde Azure SQL-service. U ziet dat Hallo-syntaxis voor het opgeven van de naam is [JsonPath](http://goessner.net/articles/JsonPath/).   

    Als JSON een eigenschap die een matrix met waarden heeft is zoals weergegeven in de volgende code Hallo:  

    ```json
    "structure": [
          {
              "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
        }
    ],
    ```

    Eigenschappen configureren zoals wordt weergegeven in het Hallo-configuratiebestand (gebruik op nul gebaseerde indexering) te volgen:

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a>Eigenschapnamen met spaties
Als de naam van een eigenschap spaties bevat, gebruikt u vierkante haken, zoals in Hallo volgt (databaseservernaam):

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a>Een oplossing implementeren met behulp van een configuratie
Wanneer u Azure Data Factory-entiteiten in de VS publiceert, kunt u Hallo configuratie dat u toouse voor die publicatiebewerking wilt opgeven.

toopublish entiteiten in een configuratiebestand met Azure Data Factory-project:   

1. Met de rechtermuisknop op de Data Factory-project en klik op **publiceren** toosee hello **Publish Items** in het dialoogvenster.
2. Selecteer een bestaande gegevensfactory of geef waarden voor het maken van een gegevensfactory op Hallo **Configure data factory** pagina en klik op **volgende**.   
3. Op Hallo **Publish Items** pagina: u ziet een vervolgkeuzelijst met beschikbare configuraties voor Hallo **Select Deployment Config** veld.

    ![Een configuratiebestand selecteren](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. Selecteer Hallo **configuratiebestand** dat u wilt, zoals toouse en klik op **volgende**.
5. Controleer of u Hallo-naam van de JSON-bestand in Hallo **samenvatting** pagina en klik op **volgende**.
6. Klik op **voltooien** nadat Hallo implementatiebewerking is voltooid.

Wanneer u implementeert, zijn Hallo waarden uit het configuratiebestand Hallo gebruikte tooset waarden voor eigenschappen in de JSON-bestanden Hallo voordat Hallo entiteiten geïmplementeerde tooAzure Data Factory-service worden.   

## <a name="use-azure-key-vault"></a>Azure Key Vault gebruiken
Het is niet aangeraden en vaak tegen beveiliging beleid toocommit gevoelige gegevens zoals verbinding tekenreeksen toohello code opslagplaats. Zie [ADF Secure publiceren](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) voorbeeld op GitHub toolearn over gevoelige informatie op te slaan in Azure Sleutelkluis en dit gebruikt bij het publiceren van de Data Factory-entiteiten. Hallo-extensie beveiligde publiceren voor Visual Studio kunt Hallo geheimen toobe opgeslagen in de Sleutelkluis en alleen verwijzingen toothem zijn opgegeven in de gekoppelde services / implementatieconfiguraties. Deze verwijzingen zijn opgelost als u Data Factory-entiteiten tooAzure publiceren. Deze bestanden kunnen vervolgens worden doorgevoerd toosource opslagplaats zonder dat geen geheimen.

## <a name="summary"></a>Samenvatting
In deze zelfstudie maakt u een Azure data factory tooprocess gegevens gemaakt door het Hive-script uitvoeren op een HDInsight hadoop-cluster. U hebt gebruikt Hallo Data Factory-Editor in hello Azure portal toodo Hallo stappen te volgen:  

1. U hebt een Azure-**gegevensfactory** gemaakt.
2. U hebt twee **gekoppelde services** gemaakt:
   1. **Azure Storage** gekoppelde service toolink uw Azure-blobopslag die invoer-/ uitvoerbestanden toohello data factory.
   2. **Azure HDInsight** op aanvraag gekoppelde service toolink een bellen op HDInsight Hadoop-cluster toohello data factory. Azure Data Factory maakt een HDInsight Hadoop-cluster just in time tooprocess invoergegevens en uitvoergegevens produceren.
3. Twee gemaakt **gegevenssets**, die invoer- en gegevens voor HDInsight Hive-activiteit in Hallo pijplijn worden beschreven.
4. U hebt een **pijplijn** gemaakt met een **HDInsight Hive**-activiteit.  

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u een pijplijn gemaakt met een transformatieactiviteit (HDInsight-activiteit) waarvoor een Hive-script wordt uitgevoerd op een on-demand HDInsight-cluster. hoe de gegevens van een Kopieeractiviteit toocopy van een Azure Blob-tooAzure SQL, toouse zien toosee [zelfstudie: gegevens kopiëren van een Azure blob-tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

U kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit. Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md) voor gedetailleerde informatie. 


## <a name="see-also"></a>Zie ook
| Onderwerp | Beschrijving |
|:--- |:--- |
| [Pijplijnen](data-factory-create-pipelines.md) |In dit artikel helpt u begrijpen pijplijnen en activiteiten in Azure Data Factory en hoe toouse ze tooconstruct gegevensgestuurde werkstromen voor uw scenario of bedrijf. |
| [Gegevenssets](data-factory-create-datasets.md) |Op basis van dit artikel krijgt u inzicht in de gegevenssets in Azure Data Factory. |
| [Activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) |Dit artikel bevat een lijst van activiteiten voor gegevenstransformatie (zoals de HDInsight Hive-transformatie die u in deze zelfstudie hebt gebruikt) die door Azure Data Factory worden ondersteund. |
| [Plannen en uitvoeren](data-factory-scheduling-and-execution.md) |Dit artikel wordt uitgelegd Hallo plannings- en uitvoeringsaspecten van het Azure Data Factory-toepassingsmodel. |
| [Pijplijnen bewaken en beheren met de app voor bewaking en beheer](data-factory-monitor-manage-app.md) |Dit artikel wordt beschreven hoe toomonitor, beheren en fouten opsporen in pijplijnen met behulp van Hallo voor bewaking en beheer-App. |
