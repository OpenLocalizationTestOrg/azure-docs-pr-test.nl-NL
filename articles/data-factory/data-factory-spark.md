---
title: aaaInvoke Spark programma's van Azure Data Factory | Microsoft Docs
description: Meer informatie over hoe tooinvoke Spark-programma's vanuit een Azure data factory met Hallo MapReduce-activiteit.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: f88943ece7ee3d21dedbd857609f1b2713b62741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a>Spark-programma's van Azure Data Factory-pijplijnen aanroepen

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

## <a name="introduction"></a>Inleiding
Spark-activiteit is een van de Hallo [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) ondersteund door Azure Data Factory. Deze activiteit wordt uitgevoerd Hallo opgegeven programma op uw Apache Spark-cluster in Azure HDInsight Spark.    

> [!IMPORTANT]
> - Spark activiteit biedt geen ondersteuning voor HDInsight Spark-clusters die gebruikmaken van een Azure Data Lake Store als primaire opslag.
> - Spark-activiteit ondersteunt alleen bestaande (uw eigen) HDInsight Spark-clusters. Een gekoppelde HDInsight-service op aanvraag worden niet ondersteund.

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a>Overzicht: een pijplijn maken met Spark-activiteit
Hier volgen Hallo gebruikelijke stappen toocreate een Data Factory-pijplijn met een Spark-activiteit.  

1. Een gegevensfactory maakt.
2. Maak een gekoppelde Azure Storage-service toolink uw Azure-opslag die is gekoppeld aan uw HDInsight Spark-cluster toohello data factory.     
2. Maak een gekoppelde HDInsight-service toolink Apache Spark-cluster in Azure HDInsight toohello gegevensfactory.
3. Maak een gegevensset die toohello Azure Storage gekoppelde service verwijst. U moet een uitvoergegevensset voor een activiteit op dit moment kunt opgeven, zelfs als er wordt geen uitvoer wordt geproduceerd.  
4. Een pijplijn maken met Spark-activiteit die toohello gekoppelde HDInsight-service is gemaakt in #2 verwijst. Hallo-activiteit is geconfigureerd met Hallo gegevensset die u hebt gemaakt in de vorige stap Hallo als een uitvoergegevensset. Hallo uitvoergegevensset is welke stations Hallo planning (elk uur, dagelijks, enz.). Daarom moet u Hallo uitvoergegevensset zelfs als er geen activiteit Hallo echt uitvoer te produceren.

### <a name="prerequisites"></a>Vereisten
1. Maak een **voor algemene doeleinden Azure Storage-Account** door de instructies te volgen in Hallo overzicht te: [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account).  
2. Maak een **Apache Spark-cluster in Azure HDInsight** door de instructies te volgen in Hallo-zelfstudie: [maken Apache Spark-cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). Hello Azure storage-account die u hebt gemaakt in stap 1 van # met dit cluster koppelen.  
3. Downloaden en bekijken Hallo python-scriptbestand **test.py** vinden op: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).  
3.  Uploaden **test.py** toohello **pyFiles** map in Hallo **adfspark** container in uw Azure-blobopslag. Hallo-container en map Hallo maken als ze bestaan niet.

### <a name="create-data-factory"></a>Een gegevensfactory maken
Laten we beginnen met het maken van de gegevensfactory Hallo in deze stap.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
2. Klik op **nieuw** op Hallo menu links, klikt u op **gegevens en analyse**, en klik op **Data Factory**.
3. In Hallo **nieuwe gegevensfactory** blade Voer **SparkDF** voor Hallo naam.

   > [!IMPORTANT]
   > Hallo-naam van hello Azure-gegevensfactory moet **globaal unieke**. Als u Hallo fout ziet: **Data factory-naam 'SparkDF' is niet beschikbaar**. Wijzig de naam van de Hallo van gegevensfactory hello (bijvoorbeeld yournameSparkDFdate en probeer het opnieuw maken. Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.   
4. Selecteer Hallo **Azure-abonnement** waar u Hallo data factory toobe gemaakt.
5. Selecteer een bestaande **resourcegroep** of maak een Azure-resourcegroep.
6. Selecteer **pincode toodashboard** optie.  
6. Klik op **maken** op Hallo **nieuwe gegevensfactory** blade.

   > [!IMPORTANT]
   > toocreate Data Factory-exemplaren, moet u lid zijn van Hallo [Data Factory Inzender](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol op het niveau van de Hallo abonnement/resourcegroep.
7. Zie van Hallo gegevensfactory wordt gemaakt in Hallo **dashboard** Hallo Azure-portal als volgt:   
8. Nadat het Hallo-gegevensfactory is gemaakt, ziet u Hallo data factory-pagina waarop u inhoud van de gegevensfactory Hallo Hallo. Als u Hallo data factory-pagina niet ziet, klikt u op Hallo tegel voor uw gegevensfactory op Hallo-dashboard.

    ![Blade Gegevensfactory](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a>Gekoppelde services maken
In deze stap kunt u twee gekoppelde services, één toolink uw Spark-cluster tooyour een gegevensfactory maken en andere toolink Hallo uw Azure-opslag tooyour data factory.  

#### <a name="create-azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service maken
In deze stap koppelt u uw Azure Storage-account tooyour data factory. Een gegevensset die u in stap verderop in dit scenario maakt verwijst toothis gekoppelde service. Hallo gekoppelde HDInsight-service die u in de volgende stap Hallo definieert verwijst te toothis gekoppelde service.  

1. Klik op **auteur en implementeren van** op Hallo **Data Factory** blade van uw gegevensfactory. U ziet Hallo Data Factory-Editor.
2. Klik op **Nieuwe gegevensopslag** en kies **Azure-opslag**.

   ![Nieuwe gegevensopslag - Azure Storage - menu](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. U ziet Hallo **JSON-script** voor het maken van een Azure Storage gekoppelde service in Hallo-editor.

   ![Een gekoppelde Azure Storage-service](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. Vervang **accountnaam** en **accountsleutel** met de naam en toegangssleutel Hallo van uw Azure storage-account. toolearn hoe tooget uw opslag heeft toegang tot sleutel, raadpleegt u Hallo informatie over hoe tooview, kopiëren en opnieuw genereren opslag toegangstoetsen in [uw opslagaccount beheren](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
5. toodeploy Hallo gekoppelde service, klikt u op **implementeren** op Hallo opdrachtbalk klikken. Nadat hello gekoppelde service is geïmplementeerd, Hallo **Draft-1** venster verdwijnt en ziet u **AzureStorageLinkedService** in Hallo structuurweergave Hallo links.

#### <a name="create-hdinsight-linked-service"></a>Een gekoppelde HDInsight-service maken
In deze stap maakt u een gekoppelde HDInsight-service toolink uw HDInsight Spark-cluster toohello data factory. Hallo HDInsight-cluster is gebruikte toorun Hallo Spark programma dat is opgegeven in de Hallo Spark activiteit van Hallo pijplijn in dit voorbeeld.  

1. Klik op **... Meer** op de werkbalk Hallo **nieuwe berekening**, en klik vervolgens op **HDInsight-cluster**.

    ![Een gekoppelde HDInsight-service maken](media/data-factory-spark/new-hdinsight-linked-service.png)
2. Kopieer en plak de volgende codefragment toohello hello **Draft-1** venster. In de JSON-editor Hallo Hallo stappen te volgen:
    1. Geef Hallo **URI** voor Hallo HDInsight Spark-cluster. Bijvoorbeeld: `https://<sparkclustername>.azurehdinsight.net/`.
    2. Geef de naam Hallo Hallo **gebruiker** wie heeft toegang tot toohello Spark-cluster.
    3. Geef Hallo **wachtwoord** voor de gebruiker.
    4. Geef Hallo **gekoppelde Azure Storage-service** dat is gekoppeld aan Hallo HDInsight Spark-cluster. In dit voorbeeld is: **AzureStorageLinkedService**.

    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - Spark activiteit biedt geen ondersteuning voor HDInsight Spark-clusters die gebruikmaken van een Azure Data Lake Store als primaire opslag.
    > - Spark-activiteit ondersteunt alleen bestaande (uw eigen) HDInsight Spark-cluster. Een gekoppelde HDInsight-service op aanvraag worden niet ondersteund.

    Zie [gekoppelde HDInsight-Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) voor meer informatie over Hallo HDInsight gekoppelde service.
3.  toodeploy Hallo gekoppelde service, klikt u op **implementeren** op Hallo opdrachtbalk klikken.  

### <a name="create-output-dataset"></a>Uitvoergegevensset maken
Hallo uitvoergegevensset is welke stations Hallo planning (elk uur, dagelijks, enz.). Daarom moet u een uitvoergegevensset voor Hallo spark activiteit in de pijplijn Hallo Hoewel Hallo activiteit geen echt geen uitvoer produceert. Het opgeven van een invoergegevensset voor Hallo-activiteit is optioneel.

1. In Hallo **Data Factory-Editor**, klikt u op **... Meer** op de opdrachtbalk hello, klikt u op **nieuwe gegevensset**, en selecteer **Azure Blob storage**.  
2. Kopieer en plak Hallo na codefragment toohello Draft-1-venster. Hallo JSON-fragment een gegevensset met de naam definieert **OutputDataset**. Bovendien u opgeven dat Hallo resultaten worden opgeslagen in blob-container Hallo aangeroepen **adfspark** en Hallo map met de naam **pyFiles/uitvoer**. Zoals eerder vermeld, is deze gegevensset een dummy-gegevensset. Hallo Spark programma in dit voorbeeld heeft geen uitvoer wordt geproduceerd. Hallo **beschikbaarheid** sectie geeft die Hallo-uitvoergegevensset dagelijks wordt geproduceerd.  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": "\t"
                }
            },
            "availability": {
                "frequency": "Day",
                "interval": 1
            }
        }
    }
    ```
3. toodeploy Hallo gegevensset, klikt u op **implementeren** op Hallo opdrachtbalk klikken.


### <a name="create-pipeline"></a>Pijplijn maken
In deze stap maakt u een pijplijn met een **HDInsightSpark** activiteit. Uitvoergegevensset is momenteel welke stations Hallo planning, dus u een uitvoergegevensset maken moet, zelfs als Hallo activiteit geen uitvoer produceert. Als Hallo activiteit geen invoer neemt, kunt u maken Hallo invoergegevensset overslaan. Daarom is geen invoergegevensset opgegeven in dit voorbeeld.

1. In Hallo **Data Factory-Editor**, klikt u op **... Meer** op Hallo opdrachtbalk en klik vervolgens op **nieuwe pijplijn**.
2. Hallo-script in het venster Draft-1 Hallo vervangen door Hallo script volgen:

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    Houd er rekening mee Hallo volgende punten:
    - Hallo **type** eigenschap is ingesteld, te**HDInsightSpark**.
    - Hallo **rootPath** te is ingesteld,**adfspark\\pyFiles** waarbij adfspark hello Azure Blob-container en pyFiles is map in de container. In dit voorbeeld is hello Azure Blob Storage Hallo die is gekoppeld aan Hallo Spark-cluster. U kunt uploaden Hallo bestand tooa andere Azure-opslag. Als u doet dit, wordt een gekoppelde Azure Storage-service toolink die storage account toohello een gegevensfactory maken. Hallo-naam van gekoppelde Hallo-service vervolgens opgeven als een waarde voor Hallo **sparkJobLinkedService** eigenschap. Zie [Spark activiteitseigenschappen](#spark-activity-properties) voor meer informatie over deze eigenschap en andere eigenschappen die ondersteund worden door Hallo Spark-activiteit.  
    - Hallo **entryFilePath** toohello is ingesteld **test.py**, namelijk Hallo python-bestand.
    - Hallo **getDebugInfo** eigenschap is ingesteld, te**altijd**, wat betekent dat het Hallo-logboekbestanden zijn altijd gegenereerd (slagen of mislukken).

        > [!IMPORTANT]
        > Het is raadzaam dat u niet deze eigenschap te stelt`Always` in een productieomgeving tenzij u een probleem wilt oplossen.
    - Hallo **levert** sectie heeft één uitvoergegevensset. U kunt een uitvoergegevensset moet opgeven, zelfs als Hallo spark programma geen uitvoer produceert. Hallo output dataset stations Hallo planning voor Hallo pijplijn (elk uur, dagelijks, enz.).  

        Zie voor meer informatie over het Hallo-eigenschappen die ondersteund worden door de activiteit Spark [activiteitseigenschappen Spark](#spark-activity-properties) sectie.
3. toodeploy hello pipeline, klikt u op **implementeren** op Hallo opdrachtbalk klikken.

### <a name="monitor-pipeline"></a>De pijplijn bewaken
1. Klik op **X** tooclose Data Factory-Editor blades en toonavigate weer toohello Data Factory-startpagina. Klik op **bewaken en beheren** toolaunch Hallo monitoring-toepassing in een ander tabblad.

    ![Bewaken en beheren van de tegel](media/data-factory-spark/monitor-and-manage-tile.png)
2. Wijziging Hallo **begintijd** te filteren Hallo boven**2/1/2017**, en klik op **toepassen**.
3. Omdat er slechts één dag tussen hello (2017-02-01) start- en eindtijden (2017-02-02) van de pijplijn hello, moet u slechts één activiteitvenster zien. Bevestig dat gegevenssegment Hallo **gereed** status.

    ![Hallo-pijplijn bewaken](media/data-factory-spark/monitor-and-manage-app.png)    
4. Selecteer Hallo **activiteitsvenster** toosee details over Hallo activiteit die wordt uitgevoerd. Als er een fout is, ziet u meer informatie over het in het rechterdeelvenster Hallo.

### <a name="verify-hello-results"></a>Hallo resultaten controleren

1. Start **Jupyter-notebook** voor uw HDInsight Spark-cluster door te navigeren naar: https://CLUSTERNAME.azurehdinsight.NET/jupyter. U kunt ook starten cluster-dashboard voor uw HDInsight Spark-cluster en start vervolgens **Jupyter-Notebook**.
2. Klik op **nieuw** -> **PySpark** toostart een nieuwe notebook.

    ![Nieuwe Jupyter-notebook](media/data-factory-spark/jupyter-new-book.png)
3. Voer hello na de opdracht door de tekst hello kopiëren/plakken en drukt u op **SHIFT + ENTER** aan Hallo einde van de tweede instructie Hallo.  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. Controleer of u Hallo gegevens uit Hallo hvac tabel:  

    ![Jupyter-queryresultaten](media/data-factory-spark/jupyter-notebook-results.png)

Zie [een Spark SQL-query uitvoeren](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) gedeelte voor meer informatie. 

### <a name="troubleshooting"></a>Problemen oplossen
Aangezien u ingesteld **getDebugInfo** te**altijd**, ziet u een **logboek** submap Hallo **pyFiles** map in uw Azure Blob-container. Hallo-logboekbestand in de logboekmap Hallo vindt u meer informatie. Dit logboekbestand is vooral nuttig wanneer er een fout optreedt. In een productieomgeving kunt u tooset deze te**fout**.

Voor meer informatie over Hallo stappen te volgen:


1. Navigeer te`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.

    ![Gebruikersinterface van YARN-toepassing](media/data-factory-spark/yarnui-application.png)  
2. Klik op **logboeken** uitvoeren voor een Hallo pogingen.

    ![Toepassingspagina](media/data-factory-spark/yarn-applications.png)
3. U kunt aanvullende foutinformatie in Hallo logboek pagina moeten zien.

    ![Fout in logboek](media/data-factory-spark/yarnui-application-error.png)

Hallo volgende secties bevatten informatie over Data Factory-entiteiten toouse Apache Spark-cluster en Spark-activiteit in uw gegevensfactory.

## <a name="spark-activity-properties"></a>Spark-activiteitseigenschappen
Hier volgt Hallo voorbeeld JSON-definitie van een pijplijn met Spark-activiteit:    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes hello Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

Hallo staan volgende tabel Hallo JSON-eigenschappen die in Hallo JSON-definitie:

| Eigenschap | Beschrijving | Vereist |
| -------- | ----------- | -------- |
| naam | Naam van de activiteit Hallo in Hallo pijplijn. | Ja |
| description | Tekst die beschrijft welke activiteit Hallo komt. | Nee |
| type | Deze eigenschap moet worden ingesteld als tooHDInsightSpark. | Ja |
| linkedServiceName | Naam van Hallo HDInsight gekoppelde service op welke Hallo Spark programma wordt uitgevoerd. | Ja |
| rootPath | Hello Azure Blob-container en map met Hallo Spark-bestand. Hallo-bestandsnaam is hoofdlettergevoelig. | Ja |
| entryFilePath | Relatief pad toohello Hallo Spark codepakket hoofdmap. | Ja |
| className | Belangrijkste Java/Spark-klasse van de toepassing | Nee |
| Argumenten | Een lijst met opdrachtregelargumenten toohello Spark programma. | Nee |
| proxyUser | Hallo account tooimpersonate tooexecute Hallo Spark programma door de gebruiker | Nee |
| sparkConfig | Geef waarden voor Spark configuratie-eigenschappen die worden vermeld in het onderwerp Hallo: [Spark-configuratie - eigenschappen van Application](https://spark.apache.org/docs/latest/configuration.html#available-properties). | Nee |
| getDebugInfo | Geeft aan wanneer Hallo Spark logboekbestanden gekopieerde toohello Azure-opslag die wordt gebruikt door HDInsight-cluster zijn (of) opgegeven door sparkJobLinkedService. Toegestane waarden: None, altijd of fout. Standaardwaarde: geen. | Nee |
| sparkJobLinkedService | Hallo gekoppelde Azure Storage-service die Hallo Spark taakbestand, afhankelijkheden en Logboeken bevat.  Als u een waarde op voor deze eigenschap niet opgeeft, wordt Hallo opslag die is gekoppeld aan de HDInsight-cluster gebruikt. | Nee |

## <a name="folder-structure"></a>Mapstructuur
Hallo Spark activiteit biedt geen ondersteuning voor een in-line-script als Pig en Hive-activiteiten doen. Spark-taken zijn ook meer extensible dan Pig/Hive-taken. Voor Spark taken, kunt u meerdere afhankelijkheden, zoals opgeven jar-pakketten (in Hallo java CLASSPATH geplaatst), python-bestanden (geplaatst op Hallo PYTHONPATH) en andere bestanden.

Hallo volgende mapstructuur in hello Azure Blob storage waarnaar wordt verwezen door Hallo gekoppelde HDInsight-service maken. Vervolgens kunt u uploaden afhankelijke bestanden toohello juiste submappen in de hoofdmap Hallo dat wordt vertegenwoordigd door **entryFilePath**. Bijvoorbeeld, python bestanden toohello pyFiles submap en jar-bestanden toohello potten submap van hoofdmap Hallo uploaden. Tijdens runtime verwacht Data Factory-service Hallo mapstructuur in hello Azure Blob-opslag te volgen:     

| Pad | Beschrijving | Vereist | Type |
| ---- | ----------- | -------- | ---- |
| . | Hallo hoofdpad van Hallo Spark taak in Hallo opslag gekoppelde service    | Ja | Map |
| &lt;de gebruiker gedefinieerde&gt; | Hallo pad toohello het gegevensbestand van Hallo Spark taak aan te wijzen | Ja | File |
| . / jars | Alle bestanden onder deze map worden geüpload en op Hallo java klassenpad van Hallo cluster geplaatst | Nee | Map |
| . / pyFiles | Alle bestanden onder deze map worden geüpload en op Hallo PYTHONPATH van Hallo cluster geplaatst | Nee | Map |
| . / bestanden | Alle bestanden onder deze map worden geüpload en in de werkmap executor geplaatst | Nee | Map |
| . / archiveert | Alle bestanden onder deze map zijn gecomprimeerd | Nee | Map |
| . / Logboeken | Hallo-map waarin de logboeken van Hallo Spark-cluster worden opgeslagen.| Nee | Map |

Hier volgt een voorbeeld van een opslagruimte met twee Spark taakbestanden in hello Azure Blob Storage waarnaar wordt verwezen door Hallo gekoppelde HDInsight-service.

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
