---
title: aaaBuild uw eerste gegevensfactory (Azure-portal) | Microsoft Docs
description: In deze zelfstudie maakt u een Azure Data Factory-voorbeeldpijplijn met behulp van de Data Factory-Editor in hello Azure-portal.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a>Zelfstudie: uw eerste Azure-gegevensfactory bouwen met Azure Portal
> [!div class="op_single_selector"]
> * [Overzicht en vereisten](data-factory-build-your-first-pipeline.md)
> * [Azure Portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager-sjabloon](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)


In dit artikel leert u hoe toouse [Azure-portal](https://portal.azure.com/) toocreate uw eerste Azure-gegevensfactory. toodo hello zelfstudie met andere hulpprogramma's / SDK, selecteer een van de Hallo opties uit de vervolgkeuzelijst Hallo. 

Hallo-pijplijn in deze zelfstudie is één activiteit: **HDInsight Hive-activiteit**. Deze activiteit wordt een hive-script uitgevoerd op een Azure HDInsight-cluster dat transformaties invoergegevens gegevens tooproduce uitvoer. Hallo pijplijn is geplande toorun wanneer een maand tussen Hallo begin- en eindtijden opgegeven. 

> [!NOTE]
> Hallo gegevens pijplijn in deze zelfstudie getransformeerd invoergegevens tooproduce uitvoergegevens. Voor een zelfstudie over het toocopy van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: gegevens kopiëren van Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Een pijplijn kan meer dan één activiteit hebben. En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit. Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.

## <a name="prerequisites"></a>Vereisten
1. Lees [overzicht van de zelfstudie](data-factory-build-your-first-pipeline.md) artikel en volledige Hallo **vereiste** stappen.
2. In dit artikel biedt geen conceptueel overzicht van hello Azure Data Factory-service. Het is raadzaam dat u doorloopt [inleiding tooAzure Data Factory](data-factory-introduction.md) voor een gedetailleerd overzicht van Hallo service het artikel.  

## <a name="create-data-factory"></a>Een gegevensfactory maken
Een gegevensfactory kan één of meer pijplijnen hebben. Een pijplijn kan één of meer activiteiten bevatten. Bijvoorbeeld invoergegevens een Kopieeractiviteit toocopy-gegevens van een doelgegevensopslagplaats tooa bron en het toorun in een HDInsight Hive-activiteit een Hive-script tootransform gegevens tooproduct uitvoer. Laten we beginnen met het maken van de gegevensfactory Hallo in deze stap.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
2. Klik op **nieuw** op Hallo menu links, klikt u op **gegevens en analyse**, en klik op **Data Factory**.

   ![Blade maken](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. In Hallo **nieuwe gegevensfactory** blade Voer **GetStartedDF** voor Hallo naam.

   ![Blade voor een nieuwe gegevensfactory](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > Hallo-naam van hello Azure-gegevensfactory moet **globaal unieke**. Als u de foutmelding Hallo: **Data factory-naam 'GetStartedDF' is niet beschikbaar**. Hallo-naam van gegevensfactory hello (bijvoorbeeld Uwnaamgetstarteddf) wijzigen en probeer het opnieuw maken. Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.
   >
   > Hallo-naam van de gegevensfactory Hallo mogelijk geregistreerd als een **DNS** naam in de toekomst Hallo en daarmee ook voor iedereen zichtbaar.
   >
   >
4. Selecteer Hallo **Azure-abonnement** waar u Hallo data factory toobe gemaakt.
5. Selecteer een bestaande **resourcegroep** of maak een resourcegroep. Maak een resourcegroep met de naam voor Hallo-zelfstudie: **ADFGetStartedRG**.
6. Selecteer Hallo **locatie** voor Hallo data factory. Regio's wordt ondersteund door Hallo Data Factory-service worden weergegeven in de vervolgkeuzelijst Hallo.
7. Selecteer **pincode toodashboard**. 
8. Klik op **maken** op Hallo **nieuwe gegevensfactory** blade.

   > [!IMPORTANT]
   > toocreate Data Factory-exemplaren, moet u lid zijn van Hallo [Data Factory Inzender](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol op het niveau van de Hallo abonnement/resourcegroep.
   >
   >
7. Op Hallo-dashboard ziet er Hallo tegel met de status: implementatie van de gegevensfactory.    

   ![Status van gegevensfactory maken](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. Gefeliciteerd. U hebt uw eerste gegevensfactory gemaakt. Nadat het Hallo-gegevensfactory is gemaakt, ziet u Hallo data factory-pagina waarop u inhoud van de gegevensfactory Hallo Hallo.     

    ![Blade Gegevensfactory](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

Voordat u een pijplijn maakt in de gegevensfactory hello, moet u toocreate enkele Data Factory-entiteiten eerst. Maakt u eerst gekoppelde services toolink gegevens/berekeningen tooyour gegevens opslaan, definieert u welke invoer en uitvoer van gegevenssets toorepresent i/o-gegevens in de gekoppelde gegevensopslag en vervolgens Hallo pijplijn maken met een activiteit die gebruikmaakt van deze gegevenssets.

## <a name="create-linked-services"></a>Gekoppelde services maken
In deze stap koppelt u uw Azure-opslagaccount en een bellen op Azure HDInsight-cluster tooyour data factory. Hallo blokkeringen Hallo invoer en uitvoer-gegevens voor de pijplijn in dit voorbeeld hello Azure Storage-account. Hallo gekoppelde HDInsight-service is gebruikte toorun een Hive-script dat is opgegeven in de activiteit Hallo van Hallo pijplijn in dit voorbeeld. Bepalen wat [gegevensarchief](data-factory-data-movement-activities.md)/[compute-services](data-factory-compute-linked-services.md) worden gebruikt in uw scenario en koppelen van deze services toohello-gegevensfactory door gekoppelde services te maken.  

### <a name="create-azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service maken
In deze stap koppelt u uw Azure Storage-account tooyour data factory. In deze zelfstudie gebruikt u Hallo dezelfde Azure-opslagaccount invoer-en uitvoergegevens toostore en Hallo HQL-script bestand.

1. Klik op **auteur en implementeren van** op Hallo **DATA FACTORY** blade voor **GetStartedDF**. U ziet Hallo Data Factory-Editor.

   ![Tegel ontwerpen en implementeren](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. Klik op **Nieuwe gegevensopslag** en kies **Azure-opslag**.

   ![Nieuwe gegevensopslag - Azure Storage - menu](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. U ziet Hallo JSON-script voor het maken van een Azure Storage gekoppelde service in Hallo-editor.

   ![Een gekoppelde Azure Storage-service](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. Vervang **accountnaam** met Hallo-naam van uw Azure storage-account en **accountsleutel** door de toegangssleutel Hallo van hello Azure storage-account. toolearn hoe tooget uw opslag heeft toegang tot sleutel, raadpleegt u Hallo informatie over hoe tooview, kopiëren en opnieuw genereren opslag toegangstoetsen in [uw opslagaccount beheren](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
5. Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gekoppelde service.

    ![Implementatieknop](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   Nadat hello gekoppelde service is geïmplementeerd, Hallo **Draft-1** venster verdwijnt en ziet u **AzureStorageLinkedService** in Hallo structuurweergave Hallo links.

    ![Een gekoppelde opslagservice in het menu](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a>Een gekoppelde HDInsight-service maken
In deze stap maakt koppelen u een gegevensfactory op aanvraag HDInsight-cluster tooyour. Hallo HDInsight-cluster wordt automatisch gemaakt tijdens runtime en na het verwerken is voltooid en niet-actieve voor de opgegeven tijdsduur Hallo verwijderd.

1. In Hallo **Data Factory-Editor**, klikt u op **... Meer** en op **Nieuwe berekening**. Selecteer vervolgens **On-demand HDInsight-cluster**.

    ![Nieuwe berekening](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. Kopieer en plak de volgende codefragment toohello hello **Draft-1** venster. Hallo JSON-codefragment bevat de Hallo-eigenschappen die gebruikt toocreate hello HDInsight-cluster op de aanvraag zijn.

    ```JSON
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:

   | Eigenschap | Beschrijving |
   |:--- |:--- |
   | ClusterSize |Hiermee wordt de grootte Hallo van Hallo HDInsight-cluster. |
   | TimeToLive | Hiermee geeft u op dat niet-actieve tijd Hallo voor Hallo HDInsight-cluster, voordat deze wordt verwijderd. |
   | linkedServiceName | Hiermee geeft u Hallo storage-account dat is gebruikt toostore Hallo logboeken die door HDInsight worden gegenereerd. |

    Houd er rekening mee Hallo volgende punten:

   * Hallo Data Factory maakt een **op basis van Linux** HDInsight-cluster voor u Hello JSON. Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.
   * U kunt **uw eigen HDInsight-cluster** gebruiken in plaats van een on-demand HDInsight-cluster. Zie [Gekoppelde HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) voor meer informatie.
   * Hallo HDInsight-cluster maakt een **standaardcontainer** in Hallo-blobopslag die u hebt opgegeven in Hallo JSON (**linkedServiceName**). HDInsight verwijdert deze container niet wanneer Hallo-cluster is verwijderd. Dit gedrag is standaard. Met een gekoppelde on-demand HDInsight-service wordt er steeds een HDInsight-cluster gemaakt wanneer er een segment wordt verwerkt, tenzij er een bestaand livecluster is (**timeToLive**). Hallo-cluster wordt automatisch verwijderd als het Hallo-verwerking is voltooid.

       Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag. Als u niet ze hoeft voor het oplossen van problemen met taken hello, kunt u toodelete ze tooreduce Hallo opslag kosten. Hallo-namen van deze containers worden als volgt: ' adf**naamvanuwgegevensfactory**-**linkedservicename**- datum '. Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) toodelete containers in uw Azure-blobopslag.

     Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.
3. Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gekoppelde service.

    ![Gekoppelde on-demand HDInsight-service implementeren](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. Controleer of u beide **AzureStorageLinkedService** en **HDInsightOnDemandLinkedService** in Hallo structuurweergave Hallo links.

    ![Structuurweergave met gekoppelde services](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a>Gegevenssets maken
In deze stap maakt u gegevenssets toorepresent Hallo invoer maken en uitvoergegevens voor Hive-verwerking. Deze gegevenssets verwijzen toohello **AzureStorageLinkedService** u eerder in deze zelfstudie hebt gemaakt. Hallo gekoppelde service verwijst tooan Azure Storage-account en gegevenssets vindt u container, map en bestandsnaam in Hallo opslag van de invoer- en uitvoergegevens.   

### <a name="create-input-dataset"></a>Invoergegevensset maken
1. In Hallo **Data Factory-Editor**, klikt u op **... Meer** op de opdrachtbalk hello, klikt u op **nieuwe gegevensset**, en selecteer **Azure Blob storage**.

    ![Nieuwe gegevensset](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. Kopieer en plak Hallo na codefragment toohello Draft-1-venster. Hallo JSON-codefragment maakt u maakt in een gegevensset met de naam **AzureBlobInput** die staat voor invoergegevens van een activiteit in Hallo pijplijn. Bovendien u opgeven dat Hallo invoergegevens in de blob-container Hallo aangeroepen bevinden zich **adfgetstarted** en Hallo map met de naam **inputdata**.

    ```JSON
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
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
    Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:

   | Eigenschap | Beschrijving |
   |:--- |:--- |
   | type |Hallo type wordt ingesteld te**AzureBlob** omdat de gegevens zich in een Azure blob storage. |
   | linkedServiceName |Toohello verwijst **AzureStorageLinkedService** u eerder hebt gemaakt. |
   | folderPath | Hiermee geeft u op Hallo blob **container** en Hallo **map** die invoer blobs bevat. | 
   | fileName |Deze eigenschap is optioneel. Als u deze eigenschap niet opgeeft, worden alle Hallo-bestanden uit folderPath Hallo opgenomen. In deze zelfstudie alleen Hallo **input.log** wordt verwerkt. |
   | type |Hallo-logboekbestanden tekstbestanden zijn, zodat we gebruiken **TextFormat**. |
   | columnDelimiter |kolommen in Hallo logboekbestanden worden gescheiden door **kommateken (`,`)** |
   | frequency/interval |frequentie ingesteld te**maand** en interval is **1**, wat betekent dat Hallo invoer segmenten maandelijks beschikbaar zijn. |
   | external | Deze eigenschap is ingesteld, te**true** als Hallo invoergegevens niet worden gegenereerd door deze pijplijn. In deze zelfstudie Hallo input.log bestand niet worden gegenereerd door deze pipeline zodat we Hallo eigenschap tootrue instellen. |

    Zie het [artikel over Azure Blob-connectoren](data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over deze JSON-eigenschappen.
3. Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo nieuwe gegevensset. U ziet de gegevensset in Hallo structuurweergave links Hallo Hallo.

### <a name="create-output-dataset"></a>Uitvoergegevensset maken
U maakt nu Hallo gegevensset toorepresent Hallo uitvoer uitvoergegevens opgeslagen in hello Azure Blob-opslag.

1. In Hallo **Data Factory-Editor**, klikt u op **... Meer** op de opdrachtbalk hello, klikt u op **nieuwe gegevensset**, en selecteer **Azure Blob storage**.  
2. Kopieer en plak Hallo na codefragment toohello Draft-1-venster. Hallo JSON-codefragment maakt u maakt in een gegevensset met de naam **AzureBlobOutput**, en geeft u op Hallo van Hallo-gegevens die door Hallo Hive-script wordt geproduceerd. Bovendien u opgeven dat Hallo resultaten worden opgeslagen in blob-container Hallo aangeroepen **adfgetstarted** en Hallo map met de naam **partitioneddata**. Hallo **beschikbaarheid** sectie geeft die Hallo-uitvoergegevensset op maandelijkse basis wordt geproduceerd.

    ```JSON
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
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
    Zie **hello invoergegevensset maken** sectie voor beschrijvingen van deze eigenschappen. U instelt geen Hallo externe eigenschap op een uitvoergegevensset omdat Hallo gegevensset wordt geproduceerd door Hallo Data Factory-service.
3. Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo nieuwe gegevensset.
4. Controleer of dat deze Hallo gegevensset is gemaakt.

    ![Structuurweergave met gekoppelde services](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a>Pijplijn maken
In deze stap maakt u uw eerste pijplijn met een **HDInsightHive**-activiteit. Invoersegment maandelijks beschikbaar is (frequency: Month, interval: 1), uitvoer segment wordt geproduceerd, maandelijks en Hallo scheduler-eigenschap voor activiteit Hallo toomonthly ook is ingesteld. Hallo-instellingen voor Hallo uitvoergegevensset en Hallo activiteitenplanner moeten overeenkomen met. Uitvoergegevensset is momenteel welke stations Hallo planning, dus u een uitvoergegevensset maken moet, zelfs als Hallo activiteit geen uitvoer produceert. Als Hallo activiteit geen invoer neemt, kunt u maken Hallo invoergegevensset overslaan. Hallo-eigenschappen die in de volgende JSON Hallo worden aan Hallo einde van deze sectie beschreven.

1. In Hallo **Data Factory-Editor**, klikt u op **weglatingsteken (...) Meer opdrachten** en klik vervolgens op **nieuwe pijplijn**.

    ![Knop Nieuw pijplijn](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. Kopieer en plak Hallo na codefragment toohello Draft-1-venster.

   > [!IMPORTANT]
   > Vervang **storageaccountname** met de naam van uw opslagaccount in JSON Hallo Hallo.
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
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

    Hallo Hive-scriptbestand **partitionweblogs.hql**, wordt opgeslagen in hello Azure storage-account (Hallo door scriptLinkedService met de opgegeven **AzureStorageLinkedService**), en in  **script** map in container Hallo **adfgetstarted**.

    Hallo **definieert** sectie is gebruikte toospecify Hallo runtime-instellingen die toohello hive-script worden doorgegeven als Hive-configuratiewaarden (bijvoorbeeld ${hiveconf: inputtable}, ${partitionedtable}).

    Hallo **start** en **end** eigenschappen van de pijplijn Hallo geeft Hallo actieve periode van Hallo-pijplijn.

    In Hallo activiteits-JSON geeft u opgeven dat Hallo Hive-script wordt uitgevoerd op Hallo berekening die is opgegeven door Hallo **linkedServiceName** – **HDInsightOnDemandLinkedService**.

   > [!NOTE]
   > Zie 'Pijplijn-JSON' in [pijplijnen en activiteiten in Azure Data Factory](data-factory-create-pipelines.md) voor meer informatie over de JSON-eigenschappen die in Hallo-voorbeeld.
   >
   >
3. Bevestig Hallo volgende:

   1. **Input.log** bestand aanwezig is op Hallo **inputdata** map Hallo **adfgetstarted** container in hello Azure blob-opslag
   2. **partitionweblogs.hql** bestand aanwezig is op Hallo **script** map Hallo **adfgetstarted** container in hello Azure blob-opslag. Volledige Hallo vereiste stappen voor het Hallo [overzicht van de zelfstudie](data-factory-build-your-first-pipeline.md) als u deze bestanden niet ziet.
   3. Bevestig dat u hebt vervangen **storageaccountname** pijplijn met de naam van uw opslagaccount in Hallo Hallo JSON.
4. Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo pijplijn. Sinds Hallo **start** en **end** keren worden ingesteld in de afgelopen Hallo en **isPaused** set toofalse, Hallo pijplijn is (activiteit in de pijplijn Hallo) wordt uitgevoerd onmiddellijk nadat u hebt geïmplementeerd.
5. Controleer of u Hallo pijplijn in de structuurweergave Hallo.

    ![Structuurweergave met de pijplijn](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. U hebt uw eerste pijplijn gemaakt!

## <a name="monitor-pipeline"></a>De pijplijn bewaken
### <a name="monitor-pipeline-using-diagram-view"></a>De pijplijn bewaken met Diagramweergave
1. Klik op **X** tooclose Data Factory-Editor blades toonavigate back-toohello Data Factory-blade en klik op **Diagram**.

    ![Tegel Diagram](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. In de diagramweergave hello ziet u een overzicht van Hallo pijplijnen en gegevenssets die in deze zelfstudie worden gebruikt.

    ![Diagramweergave](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. tooview alle activiteiten in de pijplijn voor hello, klik met de rechtermuisknop pijplijn in Hallo diagram en klikt u op pijplijn openen.

    ![Menu Pijplijn openen](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. Controleer of u Hallo HDInsightHive-activiteit in Hallo pijplijn.

    ![Pijplijnweergave openen](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    back-toonavigate toohello vorige weergave, klikt u op **Data factory** in Hallo breadcrumb menu Hallo bovenaan.
5. In Hallo **diagramweergave**, dubbelklikt u op Hallo gegevensset **AzureBlobInput**. Bevestig dat segment Hallo **gereed** status. Het kan enkele minuten voor Hallo segment tooshow duren status Ready heeft. Als deze niet is gebeurd nadat u enige tijd wacht, ziet u of er Hallo invoerbestand (input.log in de juiste Hallo-container (adfgetstarted) en map (inputdata) geplaatst).

   ![Invoersegment met de status Gereed](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. Klik op **X** tooclose **AzureBlobInput** blade.
7. In Hallo **diagramweergave**, dubbelklikt u op Hallo gegevensset **AzureBlobOutput**. U ziet dat Hallo-segment dat momenteel wordt verwerkt.

   ![Gegevensset](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. Wanneer het verwerken is voltooid, ziet u Hallo segment **gereed** status.

   ![Gegevensset](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > Het maken van een on-demand HDInsight-cluster duurt normaal gesproken enige tijd (ongeveer 20 minuten). Daarom verwachten Hallo pipeline te laten **ongeveer 30 minuten** tooprocess Hallo segment.
   >
   >

9. Wanneer Hallo segment is in **gereed** staat, controleert u Hallo **partitioneddata** map in Hallo **adfgetstarted** container in uw blobopslag voor Hallo uitvoergegevens.  

   ![Uitvoergegevens](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. Klik op Hallo segment toosee details over deze in een **gegevenssegment** blade.

   ![Details gegevenssegment](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. Klik op een activiteit die wordt uitgevoerd in Hallo **activiteit wordt uitgevoerd lijst** toosee details over een activiteit (Hive-activiteit in ons scenario) uitgevoerd in een **details uitvoering van activiteit** venster.   

   ![Details uitvoering van activiteit](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   Uit Hallo-logboekbestanden ziet u Hallo Hive-query die is uitgevoerd en statusinformatie. Deze logboeken komen van pas bij het oplossen van problemen.
   Zie [Pijplijnen bewaken en beheren met Azure Portal-blades](data-factory-monitor-manage-pipelines.md) voor meer informatie.

> [!IMPORTANT]
> Hallo-invoerbestand wordt verwijderd zodra het Hallo-segment is verwerkt. Als u toorerun Hallo segment of zelfstudie opnieuw hello, dus Hallo invoerbestand (input.log) toohello inputdata map van de container adfgetstarted Hallo uploadt.
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a>De pijplijn bewaken met de app Bewaking en beheer
U kunt ook controleren en beheren van toepassing toomonitor uw pijplijnen. Zie [Azure Data Factory-pijplijnen bewaken en beheren met de app voor bewaking en beheer](data-factory-monitor-manage-app.md) voor meer informatie over het gebruik van deze toepassing.

1. Klik op **Monitor & beheren** tegel op Hallo-startpagina van uw gegevensfactory.

    ![De tegel Bewaking en beheer](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. De toepassing **Bewaking en beheer** wordt weergegeven. Wijziging Hallo **begintijd** en **eindtijd** toomatch start en eindtijd van de pijplijn en op **toepassen**.

    ![De app Bewaking en beheer](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. Selecteer een venster van de activiteit in Hallo **Activiteitsvensters** toosee details over deze lijst.

    ![Details van activiteitsvenster](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

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

## <a name="see-also"></a>Zie ook
| Onderwerp | Beschrijving |
|:--- |:--- |
| [Pijplijnen](data-factory-create-pipelines.md) |In dit artikel helpt u begrijpen pijplijnen en activiteiten in Azure Data Factory en hoe toouse ze tooconstruct end-to-end gegevensgestuurde werkstromen voor uw scenario of bedrijf. |
| [Gegevenssets](data-factory-create-datasets.md) |Op basis van dit artikel krijgt u inzicht in de gegevenssets in Azure Data Factory. |
| [Plannen en uitvoeren](data-factory-scheduling-and-execution.md) |Dit artikel wordt uitgelegd Hallo plannings- en uitvoeringsaspecten van het Azure Data Factory-toepassingsmodel. |
| [Pijplijnen bewaken en beheren met de app voor bewaking en beheer](data-factory-monitor-manage-app.md) |Dit artikel wordt beschreven hoe toomonitor, beheren en fouten opsporen in pijplijnen met behulp van Hallo voor bewaking en beheer-App. |
