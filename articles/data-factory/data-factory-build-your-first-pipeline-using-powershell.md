---
title: aaaBuild uw eerste gegevensfactory (PowerShell) | Microsoft Docs
description: In deze zelfstudie maakt u een Azure Data Factory-voorbeeldpijplijn met behulp van Azure PowerShell.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 22ec1236-ea86-4eb7-b903-0e79a58b90c7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 626260798b56d590577b3c4b24f7cf52873c9f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a>Zelfstudie: uw eerste Azure-gegevensfactory bouwen met Azure PowerShell
> [!div class="op_single_selector"]
> * [Overzicht en vereisten](data-factory-build-your-first-pipeline.md)
> * [Azure Portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager-sjabloon](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

In dit artikel gebruikt u Azure PowerShell toocreate uw eerste Azure-gegevensfactory. toodo hello zelfstudie met andere hulpprogramma's / SDK, selecteer een van de Hallo opties uit de vervolgkeuzelijst Hallo.

Hallo-pijplijn in deze zelfstudie is één activiteit: **HDInsight Hive-activiteit**. Deze activiteit wordt een hive-script uitgevoerd op een Azure HDInsight-cluster dat transformaties invoergegevens gegevens tooproduce uitvoer. Hallo pijplijn is geplande toorun wanneer een maand tussen Hallo begin- en eindtijden opgegeven. 

> [!NOTE]
> Hallo gegevens pijplijn in deze zelfstudie getransformeerd invoergegevens tooproduce uitvoergegevens. Er worden geen gegevens gekopieerd van een bron data store tooa doelgegevensopslagplaats. Voor een zelfstudie over het toocopy van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: gegevens kopiëren van Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Een pijplijn kan meer dan één activiteit hebben. En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit. Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.

## <a name="prerequisites"></a>Vereisten
* Lees [overzicht van de zelfstudie](data-factory-build-your-first-pipeline.md) artikel en volledige Hallo **vereiste** stappen.
* Volg de instructies in [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) artikel tooinstall meest recente versie van Azure PowerShell op uw computer.
* (optioneel) In dit artikel omvat niet alle Hallo Data Factory-cmdlets. Zie [Naslaginformatie voor Data Factory-cmdlets](/powershell/module/azurerm.datafactories) (Data Factory Cmdlet Reference) voor uitgebreide documentatie over Data Factory-cmdlets.

## <a name="create-data-factory"></a>Een gegevensfactory maken
In deze stap gebruikt u Azure PowerShell toocreate een Azure-Gegevensfactory met de naam **FirstDataFactoryPSH**. Een gegevensfactory kan één of meer pijplijnen hebben. Een pijplijn kan één of meer activiteiten bevatten. Bijvoorbeeld invoergegevens een Kopieeractiviteit toocopy-gegevens van een doelgegevensopslagplaats tooa bron en het toorun in een HDInsight Hive-activiteit een Hive-script tootransform. Laten we beginnen met het maken van de gegevensfactory Hallo in deze stap.

1. Open Azure PowerShell en Voer Hallo volgende opdracht uit. Houd Azure PowerShell open tot Hallo einde van deze zelfstudie. Als u sluiten en opnieuw opent, moet u toorun deze opdrachten opnieuw.
   * Voer Hallo volgende opdracht en Voer Hallo-gebruikersnaam en wachtwoord toosign in toohello Azure-portal te gebruiken.
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * Hallo opdracht tooview na alle Hallo abonnementen voor dit account uitgevoerd.
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * Hallo opdracht tooselect Hallo abonnement dat u wilt dat toowork met volgende worden uitgevoerd. Dit abonnement moet hetzelfde zijn als u die wordt gebruikt bij de Azure-portal Hallo HALLO hallo.
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. Maak een Azure-resourcegroep met de naam **ADFTutorialResourceGroup** door het uitvoeren van de volgende opdracht Hallo:
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    Sommige van Hallo stappen in deze zelfstudie wordt ervan uitgegaan dat u het Hallo-resourcegroep met de naam ADFTutorialResourceGroup. Als u een andere resourcegroep gebruikt, moet u toouse deze in plaats van ADFTutorialResourceGroup in deze zelfstudie.
3. Voer Hallo **New-AzureRmDataFactory** cmdlet die wordt gemaakt van een gegevensfactory met de naam **FirstDataFactoryPSH**.

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
Houd er rekening mee Hallo volgende punten:

* Hallo-naam van hello Azure Data Factory moet wereldwijd uniek zijn. Als u de foutmelding Hallo **Data factory-naam 'FirstDataFactoryPSH' is niet beschikbaar**, wijzig de naam van hello (bijvoorbeeld in yournameFirstDataFactoryPSH). Gebruik deze naam in plaats van ADFTutorialFactoryPSH tijdens het uitvoeren van de stappen in de zelfstudie. Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.
* toocreate Data Factory-exemplaren, moet u bijdrager/beheerder zijn van hello Azure-abonnement toobe
* Hallo-naam van de gegevensfactory Hallo kan worden geregistreerd als DNS-naam in toekomstige Hallo en daarmee ook voor iedereen zichtbaar.
* Als u Hallo-foutmelding: '**dit abonnement is niet geregistreerd toouse namespace Microsoft.DataFactory**', voer een van de volgende Hallo en probeer opnieuw te publiceren:

  * Voer in Azure PowerShell Hallo opdracht tooregister Hallo Data Factory-provider te volgen:

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      Die Hallo Data Factory-provider is geregistreerd, kunt u na de opdracht tooconfirm Hallo uitvoeren:

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Aanmelding via het Azure-abonnement in Hallo Hallo [Azure-portal](https://portal.azure.com) en navigeer tooa Data Factory-blade of maak een gegevensfactory in hello Azure-portal. Deze actie automatisch Hallo provider voor u geregistreerd.

Voordat u een pijplijn maakt, moet u toocreate enkele Data Factory-entiteiten eerst. Maakt u eerst gekoppelde services toolink gegevens/berekeningen tooyour gegevens opslaan, definieert u welke invoer en uitvoer van gegevenssets toorepresent i/o-gegevens in de gekoppelde gegevensopslag en vervolgens Hallo pijplijn maken met een activiteit die gebruikmaakt van deze gegevenssets.

## <a name="create-linked-services"></a>Gekoppelde services maken
In deze stap koppelt u uw Azure-opslagaccount en een bellen op Azure HDInsight-cluster tooyour data factory. Hallo blokkeringen Hallo invoer en uitvoer-gegevens voor de pijplijn in dit voorbeeld hello Azure Storage-account. Hallo gekoppelde HDInsight-service is gebruikte toorun een Hive-script dat is opgegeven in de activiteit Hallo van Hallo pijplijn in dit voorbeeld. Aangeven welk(e) gegevensarchief/rekenservices er services worden gebruikt in uw scenario en koppelen van deze services toohello-gegevensfactory door gekoppelde services te maken.

### <a name="create-azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service maken
In deze stap koppelt u uw Azure Storage-account tooyour data factory. U hello gebruiken dezelfde Azure-opslagaccount invoer-en uitvoergegevens toostore en Hallo HQL-script bestand.

1. Maak een JSON-bestand met de naam StorageLinkedService.json in Hallo C:\ADFGetStarted map Hello volgende inhoud. Maak Hallo map ADFGetStarted als deze niet al bestaat.

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
    Vervang **accountnaam** met Hallo-naam van uw Azure storage-account en **accountsleutel** door de toegangssleutel Hallo van hello Azure storage-account. toolearn hoe tooget uw opslag heeft toegang tot sleutel, raadpleegt u Hallo informatie over hoe tooview, kopiëren en opnieuw genereren opslag toegangstoetsen in [uw opslagaccount beheren](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
2. Schakel over de map ADFGetStarted toohello in Azure PowerShell.
3. U kunt Hallo **New-AzureRmDataFactoryLinkedService** cmdlet die wordt gemaakt van een gekoppelde service. Deze cmdlet en andere Data Factory-cmdlets die u in deze zelfstudie gebruikt moeten u toopass waarden voor Hallo *ResourceGroupName* en *DataFactoryName* parameters. U kunt ook gebruiken **Get-AzureRmDataFactory** tooget een **DataFactory** object en het Hallo-object doorgeven zonder te hoeven typen *ResourceGroupName* en  *DataFactoryName* telkens wanneer u een cmdlet uitvoert. Voer Hallo volgende opdracht tooassign Hallo uitvoer Hallo **Get-AzureRmDataFactory** cmdlet tooa **$df** variabele.

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. Voer nu Hallo **New-AzureRmDataFactoryLinkedService** cmdlet die wordt gemaakt van Hallo gekoppeld **StorageLinkedService** service.

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    Als u hadn't hello **Get-AzureRmDataFactory** cmdlet en toegewezen Hallo uitvoer toohello **$df** variabele, hebt u toospecify waarden voor Hallo *ResourceGroupName*en *DataFactoryName* parameters als volgt.

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    Als u Azure PowerShell in het midden van de zelfstudie Hallo hello sluit, hebt u toorun hello **Get-AzureRmDataFactory** cmdlet volgende keer dat u Azure PowerShell toocomplete Hallo zelfstudie begint.

### <a name="create-azure-hdinsight-linked-service"></a>Een gekoppelde HDInsight-service maken
In deze stap maakt koppelen u een gegevensfactory op aanvraag HDInsight-cluster tooyour. Hallo HDInsight-cluster wordt automatisch gemaakt tijdens runtime en na het verwerken is voltooid en niet-actieve voor de opgegeven tijdsduur Hallo verwijderd. U kunt uw eigen HDInsight-cluster gebruiken in plaats van een on-demand HDInsight-cluster. Zie [Gekoppelde services berekenen](data-factory-compute-linked-services.md) voor meer informatie.

1. Maak een JSON-bestand met de naam **HDInsightOnDemandLinkedService**.json in Hallo **C:\ADFGetStarted** map Hello inhoud te volgen.

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
                "linkedServiceName": "StorageLinkedService"
            }
        }
    }
    ```
    Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:

   | Eigenschap | Beschrijving |
   |:--- |:--- |
   | ClusterSize |Hiermee wordt de grootte Hallo van Hallo HDInsight-cluster. |
   | TimeToLive |Hiermee geeft u op dat niet-actieve tijd Hallo voor Hallo HDInsight-cluster, voordat deze wordt verwijderd. |
   | linkedServiceName |Hiermee geeft u op Hallo storage-account dat is gebruikt toostore Hallo logboeken die door HDInsight worden gegenereerd |

    Houd er rekening mee Hallo volgende punten:

   * Hallo Data Factory maakt een **op basis van Linux** HDInsight-cluster voor u Hello JSON. Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.
   * U kunt **uw eigen HDInsight-cluster** gebruiken in plaats van een on-demand HDInsight-cluster. Zie [Gekoppelde HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) voor meer informatie.
   * Hallo HDInsight-cluster maakt een **standaardcontainer** in Hallo-blobopslag die u hebt opgegeven in Hallo JSON (**linkedServiceName**). HDInsight verwijdert deze container niet wanneer Hallo-cluster is verwijderd. Dit gedrag is standaard. Met een gekoppelde on-demand HDInsight-service wordt er steeds een HDInsight-cluster gemaakt wanneer er een segment wordt verwerkt, tenzij er een bestaand livecluster is (**timeToLive**). Hallo-cluster wordt automatisch verwijderd als het Hallo-verwerking is voltooid.

       Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag. Als u niet ze hoeft voor het oplossen van problemen met taken hello, kunt u toodelete ze tooreduce Hallo opslag kosten. Hallo-namen van deze containers worden als volgt: ' adf**naamvanuwgegevensfactory**-**linkedservicename**- datum '. Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) toodelete containers in uw Azure-blobopslag.

     Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.
2. Voer Hallo **New-AzureRmDataFactoryLinkedService** cmdlet die wordt gemaakt van Hallo gekoppelde service met de naam HDInsightOnDemandLinkedService.
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a>Gegevenssets maken
In deze stap maakt u gegevenssets toorepresent Hallo invoer maken en uitvoergegevens voor Hive-verwerking. Deze gegevenssets verwijzen toohello **StorageLinkedService** u eerder in deze zelfstudie hebt gemaakt. Hallo gekoppelde service verwijst tooan Azure Storage-account en gegevenssets vindt u container, map en bestandsnaam in Hallo opslag van de invoer- en uitvoergegevens.

### <a name="create-input-dataset"></a>Invoergegevensset maken
1. Maak een JSON-bestand met de naam **InputTable.json** in Hallo **C:\ADFGetStarted** map Hello volgende inhoud:

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
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
    Hallo JSON wordt een gegevensset met de naam gedefinieerd **AzureBlobInput**, die staat voor invoergegevens van een activiteit in Hallo pijplijn. Bovendien wordt hiermee aangegeven dat Hallo invoergegevens in de blob-container Hallo aangeroepen bevinden zich **adfgetstarted** en Hallo map met de naam **inputdata**.

    Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:

   | Eigenschap | Beschrijving |
   |:--- |:--- |
   | type |Hallo type eigenschap wordt ingesteld tooAzureBlob omdat de gegevens zich in Azure blob-opslag. |
   | linkedServiceName |verwijst toohello StorageLinkedService die u eerder hebt gemaakt. |
   | fileName |Deze eigenschap is optioneel. Als u deze eigenschap niet opgeeft, worden alle Hallo-bestanden uit folderPath Hallo opgenomen. In dit geval wordt alleen Hallo input.log verwerkt. |
   | type |Hallo-logboekbestanden zijn tekstbestanden, zodat we TextFormat gebruiken. |
   | columnDelimiter |kolommen in de logboekbestanden Hallo worden gescheiden door een kommateken hello (,). |
   | frequency/interval |frequentie tooMonth ingesteld en interval is 1, wat betekent dat Hallo invoersegmenten één keer per maand beschikbaar zijn. |
   | external |Deze eigenschap wordt tootrue ingesteld als Hallo invoergegevens niet worden gegenereerd door Hallo Data Factory-service. |
2. Voer Hallo-opdracht in Azure PowerShell toocreate Hallo Data Factory-gegevensset te volgen:

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a>Uitvoergegevensset maken
U maakt nu Hallo gegevensset toorepresent Hallo uitvoer uitvoergegevens opgeslagen in hello Azure Blob-opslag.

1. Maak een JSON-bestand met de naam **OutputTable.json** in Hallo **C:\ADFGetStarted** map Hello volgende inhoud:

    ```json
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
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
    Hallo JSON wordt een gegevensset met de naam gedefinieerd **AzureBlobOutput**, die uitvoergegevens voor een activiteit in de pijplijn Hallo vertegenwoordigt. Bovendien wordt hiermee aangegeven dat Hallo resultaten worden opgeslagen in blob-container Hallo aangeroepen **adfgetstarted** en Hallo map met de naam **partitioneddata**. Hallo **beschikbaarheid** sectie geeft die Hallo-uitvoergegevensset op maandelijkse basis wordt geproduceerd.
2. Voer Hallo-opdracht in Azure PowerShell toocreate Hallo Data Factory-gegevensset te volgen:

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a>Pijplijn maken
In deze stap maakt u uw eerste pijplijn met een **HDInsightHive**-activiteit. Invoersegment maandelijks beschikbaar is (frequency: Month, interval: 1), uitvoer segment wordt geproduceerd, maandelijks en Hallo scheduler-eigenschap voor activiteit Hallo toomonthly ook is ingesteld. Hallo-instellingen voor Hallo uitvoergegevensset en Hallo activiteitenplanner moeten overeenkomen met. Uitvoergegevensset is momenteel welke stations Hallo planning, dus u een uitvoergegevensset maken moet, zelfs als Hallo activiteit geen uitvoer produceert. Als Hallo activiteit geen invoer neemt, kunt u maken Hallo invoergegevensset overslaan. Hallo-eigenschappen die in de volgende JSON Hallo worden aan Hallo einde van deze sectie beschreven.

1. Maak een JSON-bestand met de naam MyFirstPipelinePSH.json in Hallo C:\ADFGetStarted map Hello volgende inhoud:

   > [!IMPORTANT]
   > Vervang **storageaccountname** met de naam van uw opslagaccount in JSON Hallo Hallo.
   >
   >

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
                        "scriptLinkedService": "StorageLinkedService",
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
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```
    In de JSON-codefragment hello maakt u een pijplijn die bestaat uit een enkele activiteit waarvoor gebruik van Hive tooprocess gegevens op een HDInsight-cluster.

    Hallo Hive-scriptbestand **partitionweblogs.hql**, wordt opgeslagen in hello Azure storage-account (Hallo door scriptLinkedService met de opgegeven **StorageLinkedService**), en in **script**  map in container Hallo **adfgetstarted**.

    Hallo **definieert** sectie is gebruikte toospecify Hallo runtime-instellingen die worden doorgegeven toohello hive-script als Hive-configuratiewaarden (bijvoorbeeld ${hiveconf: inputtable}, ${partitionedtable}).

    Hallo **start** en **end** eigenschappen van de pijplijn Hallo geeft Hallo actieve periode van Hallo-pijplijn.

    In Hallo activiteits-JSON geeft u opgeven dat Hallo Hive-script wordt uitgevoerd op Hallo berekening die is opgegeven door Hallo **linkedServiceName** – **HDInsightOnDemandLinkedService**.

   > [!NOTE]
   > Zie 'Pijplijn-JSON' in [pijplijnen en activiteiten in Azure Data Factory](data-factory-create-pipelines.md) voor meer informatie over de JSON-eigenschappen die worden gebruikt in het Hallo-voorbeeld.

2. Controleer of u Hallo **input.log** bestand in Hallo **adfgetstarted/inputdata** map in hello Azure blob-opslag- en Voer Hallo opdracht toodeploy Hallo pijplijn te volgen. Sinds Hallo **start** en **end** keren worden ingesteld in de afgelopen Hallo en **isPaused** set toofalse, Hallo pijplijn is (activiteit in de pijplijn Hallo) wordt uitgevoerd onmiddellijk nadat u hebt geïmplementeerd.

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. U hebt uw eerste pijplijn gemaakt met Azure PowerShell!

## <a name="monitor-pipeline"></a>De pijplijn bewaken
In deze stap gebruikt u Azure PowerShell toomonitor wat er gebeurt in een Azure data factory.

1. Voer **Get-AzureRmDataFactory** en toewijzen van Hallo uitvoer tooa **$df** variabele.

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. Voer **Get-AzureRmDataFactorySlice** tooget details over alle segmenten van Hallo **EmpSQLTable**, Hallo uitvoertabel van de pijplijn Hallo.

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    U ziet dat Hallo StartDateTime die u hier opgeeft, is dezelfde begintijd opgegeven in de JSON van de pijplijn Hallo Hallo. Hier volgt voorbeelduitvoer Hallo:

    ```PowerShell
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : FirstDataFactoryPSH
    DatasetName       : AzureBlobOutput
    Start             : 7/1/2017 12:00:00 AM
    End               : 7/2/2017 12:00:00 AM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. Voer **Get-AzureRmDataFactoryRun** tooget Hallo details van de activiteit wordt uitgevoerd voor een bepaald segment.

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    Hier volgt voorbeelduitvoer Hallo: 

    ```PowerShell
    Id                  : 0f6334f2-d56c-4d48-b427-d4f0fb4ef883_635268096000000000_635292288000000000_AzureBlobOutput
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : FirstDataFactoryPSH
    DatasetName         : AzureBlobOutput
    ProcessingStartTime : 12/18/2015 4:50:33 AM
    ProcessingEndTime   : 12/31/9999 11:59:59 PM
    PercentComplete     : 0
    DataSliceStart      : 7/1/2017 12:00:00 AM
    DataSliceEnd        : 7/2/2017 12:00:00 AM
    Status              : AllocatingResources
    Timestamp           : 12/18/2015 4:50:33 AM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : RunSampleHiveActivity
    PipelineName        : MyFirstPipeline
    Type                : Script
    ```
    U kunt deze cmdlet blijven uitvoeren totdat er Hallo segment **gereed** status of **mislukt** status. Als Hallo segment status gereed is, Controleer Hallo **partitioneddata** map in Hallo **adfgetstarted** container in uw blobopslag voor Hallo uitvoergegevens.  Het maken van een on-demand HDInsight-cluster duurt normaal gesproken enige tijd.

    ![Uitvoergegevens](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> Het maken van een on-demand HDInsight-cluster duurt normaal gesproken enige tijd (ongeveer 20 minuten). Daarom verwachten Hallo pijplijn tootake **ongeveer 30 minuten** tooprocess Hallo segment.
>
> Hallo-invoerbestand wordt verwijderd zodra het Hallo-segment is verwerkt. Als u toorerun Hallo segment of zelfstudie opnieuw hello, dus Hallo invoerbestand (input.log) toohello inputdata map van de container adfgetstarted Hallo uploadt.
>
>

## <a name="summary"></a>Samenvatting
In deze zelfstudie maakt u een Azure data factory tooprocess gegevens gemaakt door het Hive-script uitvoeren op een HDInsight hadoop-cluster. U hebt gebruikt Hallo Data Factory-Editor in hello Azure portal toodo Hallo stappen te volgen:

1. U hebt een Azure-**gegevensfactory** gemaakt.
2. U hebt twee **gekoppelde services** gemaakt:
   1. **Azure Storage** gekoppelde service toolink uw Azure-blobopslag die invoer-/ uitvoerbestanden toohello data factory.
   2. **Azure HDInsight** op aanvraag gekoppelde service toolink een bellen op HDInsight Hadoop-cluster toohello data factory. Azure Data Factory maakt een HDInsight Hadoop-cluster just in time tooprocess invoergegevens en uitvoergegevens produceren.
3. Twee gemaakt **gegevenssets**, die invoer- en gegevens voor HDInsight Hive-activiteit in Hallo pijplijn worden beschreven.
4. U hebt een **pijplijn** gemaakt met een **HDInsight Hive**-activiteit.

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u een pijplijn gemaakt met een transformatieactiviteit (HDInsight-activiteit) waarvoor een Hive-script wordt uitgevoerd op een on-demand Azure HDInsight-cluster. hoe de gegevens van een Kopieeractiviteit toocopy van een Azure Blob-tooAzure SQL, toouse zien toosee [zelfstudie: gegevens kopiëren van een Azure Blob-tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="see-also"></a>Zie ook
| Onderwerp | Beschrijving |
|:--- |:--- |
| [Data Factory-cmdlet-verwijzing](/powershell/module/azurerm.datafactories) |Zie de uitgebreide documentatie over Data Factory-cmdlets |
| [Pijplijnen](data-factory-create-pipelines.md) |In dit artikel helpt u begrijpen pijplijnen en activiteiten in Azure Data Factory en hoe toouse ze tooconstruct end-to-end gegevensgestuurde werkstromen voor uw scenario of bedrijf. |
| [Gegevenssets](data-factory-create-datasets.md) |Op basis van dit artikel krijgt u inzicht in de gegevenssets in Azure Data Factory. |
| [Plannen en uitvoeren](data-factory-scheduling-and-execution.md) |Dit artikel wordt uitgelegd Hallo plannings- en uitvoeringsaspecten van het Azure Data Factory-toepassingsmodel. |
| [Pijplijnen bewaken en beheren met de app voor bewaking en beheer](data-factory-monitor-manage-app.md) |Dit artikel wordt beschreven hoe toomonitor, beheren en fouten opsporen in pijplijnen met behulp van Hallo voor bewaking en beheer-App. |
