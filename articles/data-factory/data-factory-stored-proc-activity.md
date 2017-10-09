---
title: Activiteiten van de Server opgeslagen Procedure aaaSQL
description: Meer informatie over hoe u kunt Hallo activiteit opgeslagen Procedure van SQL Server tooinvoke een opgeslagen procedure in een Azure SQL Database of een Azure SQL Data Warehouse van een Data Factory-pijplijn.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: spelluru
ms.openlocfilehash: 9116f80eefc59d95e866b2ba1de2feb1bdc4b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-stored-procedure-activity"></a>SQL Server opgeslagen Procedure-activiteit
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

## <a name="overview"></a>Overzicht
U activiteiten voor gegevenstransformatie gebruiken in een Data Factory [pijplijn](data-factory-create-pipelines.md) tootransform en proces onbewerkte gegevens in de voorspellingen en inzichten. Hallo is activiteit opgeslagen Procedure een van activiteiten voor gegevenstransformatie Hallo die ondersteuning biedt voor Data Factory. In dit artikel is gebaseerd op Hallo [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) artikel, hetgeen een algemeen overzicht van gegevenstransformatie en Hallo ondersteund activiteiten voor gegevenstransformatie in Data Factory toont.

Hallo activiteit opgeslagen Procedure tooinvoke een opgeslagen procedure in een Hallo volgt gegevens worden opgeslagen in uw onderneming of op Azure een virtuele machine (VM), kunt u gebruiken: 

- Azure SQL Database
- Azure SQL Data Warehouse
- SQL Server-Database.  Als u SQL Server gebruikt, moet u Data Management Gateway installeren op dezelfde machine dat hosts Hallo database of op een afzonderlijke computer die toegang toohello database Hallo. Data Management Gateway is een onderdeel dat wordt verbinding gemaakt op-premises/op virtuele machine van Azure met cloudservices gegevensbronnen op een manier veilig en beheerd. Zie [Data Management Gateway](data-factory-data-management-gateway.md) artikel voor meer informatie.

> [!IMPORTANT]
> Wanneer gegevens worden gekopieerd naar Azure SQL Database of SQL Server, kunt u Hallo **SqlSink** in kopiëren activiteit tooinvoke een opgeslagen procedure met behulp van Hallo **sqlWriterStoredProcedureName** eigenschap. Zie voor meer informatie [aanroepen van opgeslagen procedure uit kopieeractiviteit](data-factory-invoke-stored-procedure-from-copy-activity.md). Voor meer informatie over het Hallo-eigenschap, Zie de volgende artikelen connector: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties). Een opgeslagen procedure aanroepen tijdens het kopiëren van gegevens in een Azure SQL Data Warehouse met behulp van een kopieeractiviteit wordt niet ondersteund. Maar u kunt Hallo opgeslagen procedure activiteit tooinvoke een opgeslagen procedure gebruiken in een SQL Data Warehouse. 
>  
> Wanneer het kopiëren van gegevens van Azure SQL Database of SQL Server of Azure SQL Data Warehouse, kunt u configureren **SqlSource** in kopiëren activiteit tooinvoke een opgeslagen procedure tooread gegevens uit de brondatabase Hallo via Hallo  **sqlReaderStoredProcedureName** eigenschap. Zie voor meer informatie, Hallo connector artikelen te volgen: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          


Hallo volgen stapsgewijze Kennismaking gebruikt Hallo activiteit opgeslagen Procedure in een pijplijn tooinvoke een opgeslagen procedure in een Azure SQL database. 

## <a name="walkthrough"></a>Walkthrough
### <a name="sample-table-and-stored-procedure"></a>Voorbeeldtabel en opgeslagen procedure
1. Maak de volgende Hallo **tabel** in uw Azure SQL Database met behulp van SQL Server Management Studio of een ander hulpmiddel u vertrouwd met bent. Hallo datum kolom is Hallo-datum en tijd wanneer de bijbehorende ID hello wordt gegenereerd.

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    ID is uniek geïdentificeerd Hallo en Hallo datum kolom is Hallo-datum en tijd wanneer de bijbehorende ID hello wordt gegenereerd.
    
    ![Voorbeeldgegevens](./media/data-factory-stored-proc-activity/sample-data.png)

    Hallo opgeslagen procedure wordt in dit voorbeeld wordt een Azure SQL Database. Als hello opgeslagen procedure in een Azure SQL Data Warehouse en SQL Server-Database is, lijkt Hallo benadering. Voor een SQL Server-database, moet u een [Data Management Gateway](data-factory-data-management-gateway.md).
2. Maak de volgende Hallo **opgeslagen procedure** die voegt de gegevens in toohello **sampletable**.

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > **Naam** en **hoofdlettergebruik** Hallo parameter (DateTime in dit voorbeeld) moet overeenkomen met die van de parameter die is opgegeven in de Hallo pijplijn activiteit JSON. In de definitie van de opgeslagen procedure hello, zorg ervoor dat  **@**  wordt gebruikt als een voorvoegsel voor Hallo-parameter.

### <a name="create-a-data-factory"></a>Een data factory maken
1. Meld u bij te[Azure-portal](https://portal.azure.com/).
2. Klik op **nieuw** op Hallo menu links, klikt u op **Intelligence en analyse**, en klik op **Data Factory**.

    ![Nieuwe gegevensfactory](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. In Hallo **nieuwe gegevensfactory** blade Voer **SProcDF** voor Hallo naam. Azure Data Factory-namen zijn **globaal unieke**. U moet tooprefix Hallo-naam van gegevensfactory Hallo met de naam van uw tooenable Hallo gemaakt Hallo factory.

   ![Nieuwe gegevensfactory](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. Selecteer uw **Azure-abonnement**.
5. Voor **resourcegroep**, doe Hallo stappen te volgen:
   1. Klik op **nieuw** en voer een naam voor de resourcegroep Hallo.
   2. Klik op **gebruik bestaande** en selecteer een bestaande resourcegroep.  
6. Selecteer Hallo **locatie** voor Hallo data factory.
7. Selecteer **pincode toodashboard** zodat u Hallo gegevensfactory op Hallo dashboard volgende keer dat u zich zien kunt aanmeldt.
8. Klik op **maken** op Hallo **nieuwe gegevensfactory** blade.
9. Zie van Hallo gegevensfactory wordt gemaakt in Hallo **dashboard** Hallo Azure-portal. Nadat het Hallo-gegevensfactory is gemaakt, ziet u Hallo data factory-pagina waarop u inhoud van de gegevensfactory Hallo Hallo.

   ![Data Factory-startpagina](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a>Een Azure SQL gekoppelde service maken
Na het maken van de gegevensfactory hello, moet u een Azure SQL gekoppelde service die is gekoppeld aan uw Azure SQL-database waarin Hallo sampletable tabel en sp_sample opgeslagen procedure, tooyour data factory maken.

1. Klik op **auteur en implementeren van** op Hallo **Data Factory** blade voor **SProcDF** toolaunch Hallo Data Factory-Editor.
2. Klik op **nieuwe gegevensopslag** op Hallo opdrachtbalk en kies **Azure SQL Database**. U ziet Hallo JSON-script voor het maken van een Azure SQL gekoppelde service in Hallo-editor.

   ![Nieuwe gegevensopslag](media/data-factory-stored-proc-activity/new-data-store.png)
3. Controleer in Hallo JSON-script, Hallo volgende wijzigingen:

   1. Vervang `<servername>` met Hallo-naam van uw Azure SQL Database-server.
   2. Vervang `<databasename>` opgeslagen procedure met Hallo-database waarin u Hallo tabel en Hallo gemaakt.
   3. Vervang `<username@servername>` met Hallo-gebruikersaccount dat toegang toohello database heeft.
   4. Vervang `<password>` met wachtwoord voor gebruikersaccount Hallo Hallo.

      ![Nieuwe gegevensopslag](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. toodeploy Hallo gekoppelde service, klikt u op **implementeren** op Hallo opdrachtbalk klikken. Controleer of u Hallo AzureSqlLinkedService in Hallo structuur op Hallo links weergeven.

    ![structuurweergave met gekoppelde service](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a>Een uitvoergegevensset maken
Geef dat een uitvoergegevensset voor een activiteit opgeslagen procedure zelfs als Hallo procedure opgeslagen geen produceert geen gegevens. Dat komt doordat de Hallo uitvoergegevensset die stations Hallo planning van Hallo activiteit (hoe vaak hello activiteit wordt uitgevoerd - per uur, dagelijks, enzovoort). Hallo uitvoergegevensset moet gebruiken een **gekoppelde service** die tooan Azure SQL Database of een Azure SQL Data Warehouse of een SQL Server-Database die u wilt opgeslagen procedure toorun Hallo verwijst. Hallo uitvoergegevensset kan fungeren als een manier toopass Hallo resultaat van Hallo opgeslagen procedure voor verdere verwerking door een andere activiteit ([activiteiten chaining](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in Hallo pijplijn. Data Factory biedt Hallo-uitvoer van een gegevensset met de opgeslagen procedure toothis echter automatisch niet schrijven. Het is Hallo opgeslagen procedure dat SQL-tabel voor schrijfbewerkingen tooa Hallo uitvoer gegevensset verwijst naar. In sommige gevallen Hallo uitvoergegevensset mag een **dummy gegevensset** (een gegevensset die tooa tabel waarop geen echt uitvoer Hallo verwijst opgeslagen procedure). Dit dummy-gegevensset wordt alleen toospecify Hallo schema voor het uitvoeren van Hallo procedure-activiteit opgeslagen gebruikt. 

1. Klik op **... Meer** op de werkbalk Hallo **nieuwe gegevensset**, en klik op **Azure SQL**. **Nieuwe gegevensset** op Hallo opdracht en selecteer **Azure SQL**.

    ![structuurweergave met gekoppelde service](media/data-factory-stored-proc-activity/new-dataset.png)
2. Kopiëren en plakken hello volgende JSON-script in toohello JSON-editor.

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. toodeploy Hallo gegevensset, klikt u op **implementeren** op Hallo opdrachtbalk klikken. Controleer of u Hallo gegevensset in de structuurweergave Hallo.

    ![Structuurweergave met gekoppelde services](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a>Een pijplijn maken met SqlServerStoredProcedure activiteit
Nu gaan we een pijplijn maken met een activiteit opgeslagen procedure. 

U ziet Hallo volgende eigenschappen: 

- Hallo **type** eigenschap is ingesteld, te**SqlServerStoredProcedure**. 
- Hallo **storedProcedureName** in het type-eigenschappen te ingesteld**sp_sample** (naam van Hallo opgeslagen procedure).
- Hallo **storedProcedureParameters** sectie bevat een parameter met de naam **datum/tijd**. Naam en het hoofdlettergebruik van Hallo-parameter in JSON moeten overeenkomen met Hallo naam en het hoofdlettergebruik van Hallo-parameter in de definitie van Hallo opgeslagen procedure. Als u null zijn voor een parameter doorgeven moet, Hallo syntaxis gebruiken: `"param1": null` (alle kleine letters).
 
1. Klik op **... Meer** op Hallo opdrachtbalk en klik op **nieuwe pijplijn**.
2. Kopiëren en plakken Hallo volgende JSON-fragment:   

    ```JSON
    {
        "name": "SprocActivitySamplePipeline",
        "properties": {
            "activities": [
                {
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
                        "storedProcedureName": "sp_sample",
                        "storedProcedureParameters": {
                            "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                        }
                    },
                    "outputs": [
                        {
                            "name": "sprocsampleout"
                        }
                    ],
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "SprocActivitySample"
                }
            ],
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. toodeploy hello pipeline, klikt u op **implementeren** op Hallo-werkbalk.  

### <a name="monitor-hello-pipeline"></a>Hallo-pijplijn bewaken
1. Klik op **X** tooclose Data Factory-Editor blades toonavigate back-toohello Data Factory-blade en klik op **Diagram**.

    ![Tegel diagram](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. In Hallo **diagramweergave**, ziet u een overzicht van Hallo pijplijnen en gegevenssets gebruikt in deze zelfstudie.

    ![Tegel diagram](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. Dubbelklik in de diagramweergave hello, op Hallo gegevensset `sprocsampleout`. U ziet Hallo segmenten in de status Ready heeft. Moet er vijf segmenten omdat een segment wordt geproduceerd voor elk uur tussen Hallo-begintijd en eindtijd van Hallo JSON.

    ![Tegel diagram](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. Wanneer een segment is in **gereed** staat, voer een `select * from sampletable` -query op Hallo Azure SQL database tooverify die gegevens Hallo is ingevoegd in de tabel toohello door Hallo opgeslagen procedure.

   ![uitvoergegevens](./media/data-factory-stored-proc-activity/output.png)

   Zie [Hallo-pijplijn bewaken](data-factory-monitor-manage-pipelines.md) voor gedetailleerde informatie over het Azure Data Factory-pijplijnen bewaken.  


## <a name="specify-an-input-dataset"></a>Geef een invoergegevensset
In scenario Hallo heeft activiteit opgeslagen procedure geen eventuele invoergegevenssets. Als u een invoergegevensset opgeeft, hello activiteit opgeslagen procedure wordt niet uitgevoerd totdat Hallo segment van de invoergegevensset beschikbaar (in de status Ready heeft is). Hallo dataset kan een externe gegevensset zijn (dat niet wordt geproduceerd door een andere activiteit in Hallo dezelfde pijplijn) of een interne gegevensset die wordt geproduceerd door een upstream-activiteit (Hallo-activiteit die wordt uitgevoerd voordat deze activiteit). U kunt meerdere invoergegevenssets voor Hallo opgeslagen procedure activiteit opgeven. Als u doet dit, hello activiteit opgeslagen procedure wordt alleen uitgevoerd als alle Hallo invoergegevensset segmenten beschikbaar (in de status Ready heeft zijn). Hallo invoergegevensset kan niet worden gebruikt in Hallo opgeslagen procedure als een parameter. Het is alleen gebruikte toocheck Hallo afhankelijkheid voordat begin Hallo procedure-activiteit opgeslagen.

## <a name="chaining-with-other-activities"></a>Keten met andere activiteiten
Als u een upstream-activiteit met deze activiteit toochain wilt, geef Hallo-uitvoer van de upstream-activiteit Hallo als invoer van deze activiteit. Wanneer u doet dit, hello activiteit opgeslagen procedure wordt niet uitgevoerd totdat de Hallo upstream-activiteit is voltooid en de uitvoergegevensset Hallo van Hallo upstream-activiteit (in de status gereed) beschikbaar. U kunt uitvoergegevenssets uit meerdere activiteiten van de upstream opgeven als invoer gegevenssets van de activiteit van Hallo opgeslagen procedure. Wanneer u dit doet, Hallo opgeslagen procedure activiteit wordt alleen uitgevoerd als alle Hallo invoergegevensset segmenten beschikbaar zijn.  

In Hallo voorbeeld te volgen, is het Hallo-uitvoer van de kopieeractiviteit Hallo: OutputDataset die invoer Hallo opgeslagen procedure-activiteit. Daarom hello activiteit opgeslagen procedure wordt niet uitgevoerd totdat Hallo kopieeractiviteit is voltooid en Hallo OutputDataset segment (op status gereed) beschikbaar is. Als u meerdere invoergegevenssets opgeeft, hello activiteit opgeslagen procedure wordt niet uitgevoerd totdat alle Hallo invoergegevensset segmenten beschikbaar (in de status Ready heeft zijn). Hallo invoergegevenssets kan niet rechtstreeks worden gebruikt als parameters toohello opgeslagen procedure activiteit. 

Zie voor meer informatie over het koppelen van activiteiten [meerdere activiteiten in een pijplijn](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob tooblob",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

Op deze manier toolink Hallo store activiteit procedure met **downstream-activiteiten** (Hallo activiteiten die worden uitgevoerd nadat hello activiteit opgeslagen procedure is voltooid), geef de uitvoergegevensset Hallo van Hallo opgeslagen procedure activiteit als een invoer van Hallo downstream activiteit in Hallo-pijplijn.

> [!IMPORTANT]
> Wanneer gegevens worden gekopieerd naar Azure SQL Database of SQL Server, kunt u Hallo **SqlSink** in kopiëren activiteit tooinvoke een opgeslagen procedure met behulp van Hallo **sqlWriterStoredProcedureName** eigenschap. Zie voor meer informatie [aanroepen van opgeslagen procedure uit kopieeractiviteit](data-factory-invoke-stored-procedure-from-copy-activity.md). Zie voor meer informatie over de eigenschap Hallo Hallo connector artikelen te volgen: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).
>  
> Wanneer het kopiëren van gegevens van Azure SQL Database of SQL Server of Azure SQL Data Warehouse, kunt u configureren **SqlSource** in kopiëren activiteit tooinvoke een opgeslagen procedure tooread gegevens uit de brondatabase Hallo via Hallo  **sqlReaderStoredProcedureName** eigenschap. Zie voor meer informatie, Hallo connector artikelen te volgen: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          

## <a name="json-format"></a>JSON-indeling
Hier volgt Hallo JSON-indeling voor het definiëren van een activiteit opgeslagen Procedure:

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of hello stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

Hallo volgende tabel beschrijft deze JSON-eigenschappen:

| Eigenschap | Beschrijving | Vereist |
| --- | --- | --- |
| naam | Naam van de activiteit Hallo |Ja |
| description |Tekst die beschrijft wat Hallo-activiteit wordt gebruikt voor |Nee |
| type | Moet worden ingesteld op: **SqlServerStoredProcedure** | Ja |
| Invoer | Optioneel. Als u een invoergegevensset opgeeft, moet dit beschikbaar is (in de status 'Gereed') voor Hallo opgeslagen procedure activiteit toorun. Hallo invoergegevensset kan niet worden gebruikt in Hallo opgeslagen procedure als een parameter. Het is alleen gebruikte toocheck Hallo afhankelijkheid voordat begin Hallo procedure-activiteit opgeslagen. |Nee |
| uitvoer | U moet een uitvoergegevensset voor een activiteit opgeslagen procedure opgeven. Uitvoergegevensset geeft Hallo **planning** voor Hallo opgeslagen procedure activiteit (elk uur, wekelijks, maandelijks, enzovoort). <br/><br/>Hallo uitvoergegevensset moet gebruiken een **gekoppelde service** die tooan Azure SQL Database of een Azure SQL Data Warehouse of een SQL Server-Database die u wilt opgeslagen procedure toorun Hallo verwijst. <br/><br/>Hallo uitvoergegevensset kan fungeren als een manier toopass Hallo resultaat van Hallo opgeslagen procedure voor verdere verwerking door een andere activiteit ([activiteiten chaining](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in Hallo pijplijn. Data Factory biedt Hallo-uitvoer van een gegevensset met de opgeslagen procedure toothis echter automatisch niet schrijven. Het is Hallo opgeslagen procedure dat SQL-tabel voor schrijfbewerkingen tooa Hallo uitvoer gegevensset verwijst naar. <br/><br/>In sommige gevallen Hallo uitvoergegevensset mag een **dummy gegevensset**, waarmee alleen toospecify Hallo schema voor het uitvoeren van Hallo procedure-activiteit opgeslagen. |Ja |
| storedProcedureName |Hallo naam opgeven van Hallo opgeslagen procedure in hello Azure SQL database- of Azure SQL Data Warehouse of SQL Server-database die wordt vertegenwoordigd door Hallo gekoppelde service die Hallo uitvoer tabel gebruikt. |Ja |
| storedProcedureParameters |Geef waarden op voor parameters van opgeslagen procedure. Als u toopass null voor een parameter moet, Hallo syntaxis gebruiken: "param1": null (alle kleine letter). Zie Hallo toolearn voorbeeld over het gebruik van deze eigenschap te volgen. |Nee |

## <a name="passing-a-static-value"></a>Het doorgeven van een statische waarde
Nu we eens het toevoegen van een andere kolom met de naam 'Scenario' in met een statische waarde met de naam 'Document voorbeeld' Hallo-tabel.

![Voorbeeldgegevens 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

**Tabel:**

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

**Opgeslagen procedure:**

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

Nu doorgeven Hallo **Scenario** parameter en de Hallo van Hallo opgeslagen procedure-activiteit. Hallo **typeProperties** sectie in het voorgaande voorbeeld lijkt erop volgende codefragment Hallo Hallo:

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

**Data Factory-gegevensset:**

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Data Factory-pijplijn**

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```