---
title: "Incrementeel meerdere tabellen kopiëren met behulp van Azure Data Factory | Microsoft Docs"
description: In deze zelfstudie maakt u een Azure Data Factory-pijplijn waarmee wijzigingsgegevens incrementeel uit meerdere tabellen van een lokale Microsoft SQL Server worden gekopieerd naar een Azure SQL-database.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/22/2018
ms.author: jingwang
ms.openlocfilehash: 9eeb265e063e6642b90dd641d41d0a54cbc6951e
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/23/2018
---
# <a name="incrementally-load-data-from-multiple-tables-in-sql-server-to-an-azure-sql-database"></a>Incrementeel gegevens uit meerdere tabellen in SQL Server naar een Azure SQL-database kopiëren
In deze zelfstudie maakt u een Azure Data Factory met een pijplijn waarmee wijzigingsgegevens uit meerdere tabellen van een lokale SQL-server naar een Azure SWL-database worden gekopieerd.    

In deze zelfstudie voert u de volgende stappen uit:

> [!div class="checklist"]
> * Bereid de bron- en doelserver gegevensopslag voor.
> * Een data factory maken.
> * Een zelf-hostende Integration Runtime maken.
> * De Integration Runtime installeren. 
> * Maak gekoppelde services. 
> * Bron-, sink- en grenswaardegegevenssets maken.
> * Maken, starten en controleren van een pijplijn.
> * Bekijk de resultaten.
> * Gegevens in brontabellen toevoegen of bijwerken.
> * De pijplijn opnieuw uitvoeren en controleren.
> * De eindresultaten bekijken.

> [!NOTE]
> Dit artikel is van toepassing op versie 2 van Azure Data Factory, dat zich momenteel in de previewfase bevindt. Als u versie 1 van de Data Factory-service gebruikt, die algemeen beschikbaar is, raadpleegt u de [documentatie voor versie 1 van Data Factory](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="overview"></a>Overzicht
Dit zijn de belangrijke stappen voor het maken van deze oplossing: 

1. **Selecteer de grenswaardekolom**.
    Selecteer één kolom in elke tabel van de brongegevensopslag, die kan worden gebruikt om de nieuwe of bijgewerkte records voor elke uitvoering te segmenteren. Normaal gesproken nemen de gegevens in deze geselecteerde kolom (bijvoorbeeld, last_modify_time of id) toe wanneer de rijen worden gemaakt of bijgewerkt. De maximale waarde in deze kolom wordt gebruikt als grenswaarde.

2. **Bereid een gegevensopslag voor om de grenswaarde in op te slaan**.   
    In deze zelfstudie slaat u de grenswaarde op in een SQL-database.

3. **Maak een pijplijn met de volgende activiteiten**: 
    
    a. Maak een ForEach-activiteit die door een lijst met namen van gegevensbrontabellen loopt, die als parameter is doorgegeven aan de pijplijn. Voor elke brontabel roept deze de volgende activiteiten voor het laden van de deltagegevens voor deze tabel op.

    b. Maak twee opzoekactiviteiten. Gebruik de eerste opzoekactiviteit om de laatste grenswaarde op te halen. Gebruik de tweede opzoekactiviteit om de nieuwe grenswaarde op te halen. Deze grenswaarden worden doorgegeven aan de kopieeractiviteit.

    c. Maak een kopieeractiviteit waarmee rijen uit de brongegevensopslag worden gekopieerd met een waarde uit de grenswaardekolom die groter is dan de oude grenswaarde en kleiner dan de nieuwe grenswaarde. Vervolgens worden de deltagegevens uit de brongegevensopslag als een nieuw bestand gekopieerd naar een Azure Blob-opslag.

    d. Maak een opgeslagen-procedureactiviteit waarmee de grenswaarde wordt bijgewerkt voor de pijplijn die de volgende keer wordt uitgevoerd. 

    Hier volgt de diagramoplossing op hoog niveau: 

    ![Stapsgewijs gegevens laden](media\tutorial-incremental-copy-multiple-tables-powershell\high-level-solution-diagram.png)


Als u nog geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/) voordat u begint.

## <a name="prerequisites"></a>Vereisten
* **SQL Server**. In deze zelfstudie gebruikt u een on-premises SQL Server-database als een brongegevensopslag. 
* **Azure SQL-database**. U gebruikt een SQL database als de sink-gegevensopslag. Als u geen SQL-database hebt, raadpleegt u het artikel [Een Azure SQL-database maken](../sql-database/sql-database-get-started-portal.md) om een database te maken. 

### <a name="create-source-tables-in-your-sql-server-database"></a>Brontabellen maken in uw SQL Server-database

1. Start SQL Server Management Studio en maak verbinding met uw on-premises SQL-database.

2. Klik in **Server Explorer** met de rechtermuisknop op de database en kies **Nieuwe query**.

3. Voer de volgende SQL-opdracht uit op uw database om tabellen te maken met de naam `customer_table` en `project_table`:

    ```sql
    create table customer_table
    (
        PersonID int,
        Name varchar(255),
        LastModifytime datetime
    );
    
    create table project_table
    (
        Project varchar(255),
        Creationtime datetime
    );
        
    INSERT INTO customer_table
    (PersonID, Name, LastModifytime)
    VALUES
    (1, 'John','9/1/2017 12:56:00 AM'),
    (2, 'Mike','9/2/2017 5:23:00 AM'),
    (3, 'Alice','9/3/2017 2:36:00 AM'),
    (4, 'Andy','9/4/2017 3:21:00 AM'),
    (5, 'Anny','9/5/2017 8:06:00 AM');
    
    INSERT INTO project_table
    (Project, Creationtime)
    VALUES
    ('project1','1/1/2015 0:00:00 AM'),
    ('project2','2/2/2016 1:23:00 AM'),
    ('project3','3/4/2017 5:16:00 AM');
    
    ```

### <a name="create-destination-tables-in-your-sql-database"></a>Doeltabellen in uw SQL database maken
1. Open SQL Server Management Studio en maak verbinding met de SQL Server-database.

2. Klik in **Server Explorer** met de rechtermuisknop op de database en kies **Nieuwe query**.

3. Voer de volgende SQL-opdracht uit op uw SQL-database om tabellen te maken met de naam `customer_table` en `project_table`:  
    
    ```sql
    create table customer_table
    (
        PersonID int,
        Name varchar(255),
        LastModifytime datetime
    );
    
    create table project_table
    (
        Project varchar(255),
        Creationtime datetime
    );

    ```

### <a name="create-another-table-in-the-sql-database-to-store-the-high-watermark-value"></a>Nog een tabel in de SQL-database maken om de bovengrenswaarde op te slaan
1. Voer de volgende SQL-opdracht uit op de SQL-database om een tabel met de naam `watermarktable` te maken om de grenswaarde op te slaan: 
    
    ```sql
    create table watermarktable
    (
    
        TableName varchar(255),
        WatermarkValue datetime,
    );
    ```
2. Initiële watermerkwaarden voor beide brontabellen in de watermerktabel invoegen.

    ```sql

    INSERT INTO watermarktable
    VALUES 
    ('customer_table','1/1/2010 12:00:00 AM'),
    ('project_table','1/1/2010 12:00:00 AM');
    
    ```

### <a name="create-a-stored-procedure-in-the-sql-database"></a>Een opgeslagen procedure maken in de SQL-database 

Voer de volgende opdracht uit om een opgeslagen procedure te maken in de SQL-database. Deze opgeslagen procedure werkt de bovengrenswaarde bij elke pijplijnuitvoering bij. 

```sql
CREATE PROCEDURE sp_write_watermark @LastModifiedtime datetime, @TableName varchar(50)
AS

BEGIN

    UPDATE watermarktable
    SET [WatermarkValue] = @LastModifiedtime 
WHERE [TableName] = @TableName

END

```

### <a name="create-data-types-and-additional-stored-procedures"></a>Gegevenstypen en aanvullende opgeslagen procedures maken
Voer de volgende query uit om twee opgeslagen procedures en twee gegevenstypen te maken in de SQL-database. Deze worden gebruikt voor het samenvoegen van de gegevens uit de brontabellen in doeltabellen.

```sql
CREATE TYPE DataTypeforCustomerTable AS TABLE(
    PersonID int,
    Name varchar(255),
    LastModifytime datetime
);

GO

CREATE PROCEDURE sp_upsert_customer_table @customer_table DataTypeforCustomerTable READONLY
AS

BEGIN
  MERGE customer_table AS target
  USING @customer_table AS source
  ON (target.PersonID = source.PersonID)
  WHEN MATCHED THEN
      UPDATE SET Name = source.Name,LastModifytime = source.LastModifytime
  WHEN NOT MATCHED THEN
      INSERT (PersonID, Name, LastModifytime)
      VALUES (source.PersonID, source.Name, source.LastModifytime);
END

GO

CREATE TYPE DataTypeforProjectTable AS TABLE(
    Project varchar(255),
    Creationtime datetime
);

GO

CREATE PROCEDURE sp_upsert_project_table @project_table DataTypeforProjectTable READONLY
AS

BEGIN
  MERGE project_table AS target
  USING @project_table AS source
  ON (target.Project = source.Project)
  WHEN MATCHED THEN
      UPDATE SET Creationtime = source.Creationtime
  WHEN NOT MATCHED THEN
      INSERT (Project, Creationtime)
      VALUES (source.Project, source.Creationtime);
END

```

### <a name="azure-powershell"></a>Azure PowerShell
Installeer de nieuwste Azure PowerShell-modules met de instructies in [Azure PowerShell installeren en configureren](/powershell/azure/install-azurerm-ps).

## <a name="create-a-data-factory"></a>Een gegevensfactory maken
1. Definieer een variabele voor de naam van de resourcegroep die u later gaat gebruiken in PowerShell-opdrachten. Kopieer de tekst van de volgende opdracht naar PowerShell, geef tussen dubbele aanhalingstekens een naam op voor de [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) en voer de opdracht uit. Een voorbeeld is `"adfrg"`. 
   
     ```powershell
    $resourceGroupName = "ADFTutorialResourceGroup";
    ```

    Als de resourcegroep al bestaat, wilt u waarschijnlijk niet dat deze wordt overschreven. Wijs een andere waarde toe aan de `$resourceGroupName`-variabele en voer de opdracht opnieuw uit.

2. Definieer een variabele voor de locatie van de data factory. 

    ```powershell
    $location = "East US"
    ```
3. Voer de volgende opdracht uit om de resourcegroep te maken: 

    ```powershell
    New-AzureRmResourceGroup $resourceGroupName $location
    ``` 
    Als de resourcegroep al bestaat, wilt u waarschijnlijk niet dat deze wordt overschreven. Wijs een andere waarde toe aan de `$resourceGroupName`-variabele en voer de opdracht opnieuw uit.

4. Definieer een variabele voor de naam van de data factory. 

    > [!IMPORTANT]
    >  Werk de naam van de data factory zodanig bij dat deze uniek is. Bijvoorbeeld: ADFIncMultiCopyTutorialFactorySP1127. 

    ```powershell
    $dataFactoryName = "ADFIncMultiCopyTutorialFactory";
    ```
5. Voer de volgende cmdlet **Set AzureRmDataFactoryV2** uit om de data factory te maken: 
    
    ```powershell       
    Set-AzureRmDataFactoryV2 -ResourceGroupName $resourceGroupName -Location $location -Name $dataFactoryName 
    ```

Houd rekening met de volgende punten:

* De naam van de data factory moet een Globally Unique Identifier zijn. Als de volgende fout zich voordoet, wijzigt u de naam en probeert u het opnieuw:

    ```
    The specified Data Factory name 'ADFIncMultiCopyTutorialFactory' is already in use. Data Factory names must be globally unique.
    ```
* Als u Data Factory-exemplaren wilt maken, moet het gebruikersaccount waarmee u zich bij Azure aanmeldt, lid zijn van de rollen Inzender of Eigenaar, of moet dit een beheerder van het Azure-abonnement zijn.
* Momenteel kunt u met Data Factory versie 2 alleen data factory's maken in de regio's VS - oost, VS - oost 2 en West-Europa. De gegevensopslagexemplaren (Azure Storage, SQL Database, enzovoort) en berekeningen (Azure HDInsight, enzovoort) die worden gebruikt door de data factory, kunnen zich in andere regio's bevinden.

[!INCLUDE [data-factory-create-install-integration-runtime](../../includes/data-factory-create-install-integration-runtime.md)]



## <a name="create-linked-services"></a>Gekoppelde services maken
U maakt gekoppelde services in een gegevensfactory om uw gegevensarchieven en compute-services aan de gegevensfactory te koppelen. In deze sectie maakt u gekoppelde services in de lokale SQL Server en de SQL-database. 

### <a name="create-the-sql-server-linked-service"></a>De gekoppelde service voor SQL Server maken
In deze stap gaat u uw on-premises SQL Server-database aan de data factory koppelen.

1. Maak een JSON-bestand met de naam SqlServerLinkedService.json in de map C:\ADFTutorials\IncCopyMultiTableTutorial met de volgende inhoud. Selecteer de juiste sectie op basis van de verificatie die u gebruikt om verbinding te maken met SQL Server. Maak de lokale mappen als deze nog niet bestaan. 

    > [!IMPORTANT]
    > Selecteer de juiste sectie op basis van de verificatie die u gebruikt om verbinding te maken met SQL Server.

    Als u gebruikmaakt van SQL-verificatie, moet u de volgende JSON-definitie kopiëren:

    ```json
    {
        "properties": {
            "type": "SqlServer",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=<servername>;Database=<databasename>;User ID=<username>;Password=<password>;Timeout=60"
                }
            },
            "connectVia": {
                "type": "integrationRuntimeReference",
                "referenceName": "<integration runtime name>"
            }
        },
        "name": "SqlServerLinkedService"
    }
   ```    
    Als u gebruikmaakt van Windows-verificatie, moet u de volgende JSON-definitie kopiëren:

    ```json
    {
        "properties": {
            "type": "SqlServer",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=<server>;Database=<database>;Integrated Security=True"
                },
                "userName": "<user> or <domain>\\<user>",
                "password": {
                    "type": "SecureString",
                    "value": "<password>"
                }
            },
            "connectVia": {
                "type": "integrationRuntimeReference",
                "referenceName": "<integration runtime name>"
            }
        },
        "name": "SqlServerLinkedService"
    }    
    ```
    > [!IMPORTANT]
    > - Selecteer de juiste sectie op basis van de verificatie die u gebruikt om verbinding te maken met SQL Server.
    > - Vervang de &lt;naam> van de integration runtime door de naam van uw integration runtime.
    > - Vervang &lt;servername>, &lt;databasename>,&lt; username> en&lt; password> door de waarden van uw SQL Server-exemplaar voordat u het bestand opslaat.
    > - Als u een slash wilt gebruiken (`\`) in de naam van uw gebruikersaccount of server, moet u het escapeteken (`\`) gebruiken. Een voorbeeld is `mydomain\\myuser`.

2. Schakel in PowerShell over naar de map C:\ADFTutorials\IncCopyMultiTableTutorial.

3. Voer de cmdlet **Set-AzureRmDataFactoryV2LinkedService** uit om de gekoppelde service AzureStorageLinkedService te maken. In het volgende voorbeeld geeft u de waarden door voor de parameters *ResourceGroupName* en *DataFactoryName*: 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SqlServerLinkedService" -File ".\SqlServerLinkedService.json"
    ```

    Hier volgt een voorbeeld van uitvoer:

    ```json
    LinkedServiceName : SqlServerLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFIncMultiCopyTutorialFactory1201
    Properties        : Microsoft.Azure.Management.DataFactory.Models.SqlServerLinkedService
    ```

### <a name="create-the-sql-database-linked-service"></a>De gekoppelde SQL-databaseservice maken
1. Maak een JSON-bestand met de naam AzureSQLDatabaseLinkedService.json in de map C:\ADFTutorials\IncCopyMultiTableTutorial met de volgende inhoud. (Maak de map ADF als deze nog niet bestaat.) Vervang voordat u het bestand opslaat &lt;server&gt; &lt;database name&gt;, &lt;user id&gt; en &lt;password&gt; door de naam van uw SQL-serverdatabase, databasenaam, gebruikers-id en wachtwoord. 

    ```json
    {
        "name": "AzureSQLDatabaseLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": {
                    "value": "Server = tcp:<server>.database.windows.net,1433;Initial Catalog=<database name>; Persist Security Info=False; User ID=<user name>; Password=<password>; MultipleActiveResultSets = False; Encrypt = True; TrustServerCertificate = False; Connection Timeout = 30;",
                    "type": "SecureString"
                }
            }
        }
    }
    ```
2. Voer in PowerShell de cmdlet **Set-AzureRmDataFactoryV2LinkedService** uit om de gekoppelde service AzureSQLDatabaseLinkedService te maken. 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureSQLDatabaseLinkedService" -File ".\AzureSQLDatabaseLinkedService.json"
    ```

    Hier volgt een voorbeeld van uitvoer:

    ```json
    LinkedServiceName : AzureSQLDatabaseLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFIncMultiCopyTutorialFactory1201
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlDatabaseLinkedService
    ```

## <a name="create-datasets"></a>Gegevenssets maken
In deze stap maakt u gegevenssets die de gegevensbron, het gegevensdoel en de plaats voor het opslaan van de bovengrens aangeven.

### <a name="create-a-source-dataset"></a>Een brongegevensset maken

1. Maak een JSON-bestand met de naam SourceDataset.json in dezelfde map met de volgende inhoud: 

    ```json
    {
        "name": "SourceDataset",
        "properties": {
            "type": "SqlServerTable",
            "typeProperties": {
                "tableName": "dummyName"
            },
            "linkedServiceName": {
                "referenceName": "SqlServerLinkedService",
                "type": "LinkedServiceReference"
            }
        }
    }
   
    ```

    Naam van de tabel is een dummy-naam. De kopieeractiviteit in de pijplijn gebruikt een SQL-query voor het laden van de gegevens in plaats van de hele tabel te laden.

2. Voer de cmdlet **Set-AzureRmDataFactoryV2Dataset** uit om de gegevensset SourceDataset te maken.
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SourceDataset" -File ".\SourceDataset.json"
    ```

    Hier volgt een uitvoervoorbeeld van de cmdlet:
    
    ```json
    DatasetName       : SourceDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFIncMultiCopyTutorialFactory1201
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.SqlServerTableDataset
    ```

### <a name="create-a-sink-dataset"></a>Een sinkgegevensset maken

1. Maak een JSON-bestand met de naam SinkDataset.json in dezelfde map met de volgende inhoud. Het element tableName wordt in runtime dynamisch ingesteld door de pijplijn. De ForEach-activiteit in de pijplijn doorloopt een lijst met namen van tabellen en geeft de tabelnaam door aan deze gegevensset in elke iteratie. 

    ```json
    {
        "name": "SinkDataset",
        "properties": {
            "type": "AzureSqlTable",
            "typeProperties": {
                "tableName": {
                    "value": "@{dataset().SinkTableName}",
                    "type": "Expression"
                }
            },
            "linkedServiceName": {
                "referenceName": "AzureSQLDatabaseLinkedService",
                "type": "LinkedServiceReference"
            },
            "parameters": {
                "SinkTableName": {
                    "type": "String"
                }
            }
        }
    }
    ```

2. Voer de cmdlet **Set-AzureRmDataFactoryV2Dataset** uit om de gegevensset SinkDataset te maken.
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SinkDataset" -File ".\SinkDataset.json"
    ```

    Hier volgt een uitvoervoorbeeld van de cmdlet:
    
    ```json
    DatasetName       : SinkDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFIncMultiCopyTutorialFactory1201
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlTableDataset
    ```

### <a name="create-a-dataset-for-a-watermark"></a>Een gegevensset maken voor een grenswaarde
In deze stap maakt u een gegevensset voor het opslaan van een bovengrenswaarde. 

1. Maak een JSON-bestand met de naam WatermarkDataset.json in dezelfde map met de volgende inhoud: 

    ```json
    {
        "name": " WatermarkDataset ",
        "properties": {
            "type": "AzureSqlTable",
            "typeProperties": {
                "tableName": "watermarktable"
            },
            "linkedServiceName": {
                "referenceName": "AzureSQLDatabaseLinkedService",
                "type": "LinkedServiceReference"
            }
        }
    }    
    ```
2. Voer de cmdlet **Set-AzureRmDataFactoryV2Dataset** uit om de gegevensset WatermarkDataset te maken.
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "WatermarkDataset" -File ".\WatermarkDataset.json"
    ```

    Hier volgt een uitvoervoorbeeld van de cmdlet:
    
    ```json
    DatasetName       : WatermarkDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : <data factory name>
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlTableDataset    
    ```

## <a name="create-a-pipeline"></a>Een pijplijn maken
In deze pijplijn wordt een lijst met tabelnamen gebruikt als parameter. De ForEach-activiteit doorloopt de lijst met namen van tabellen en voert de volgende bewerkingen uit: 

1. Gebruik de opzoekactiviteit voor het ophalen van de oude bovengrenswaarde (de initiële waarde, of de waarde die is gebruikt in de laatste iteratie).

2. Gebruik de opzoekactiviteit voor het ophalen van de nieuwe bovengrenswaarde (de maximale waarde van de bovengrenskolom in de brontabel).

3. Gebruik de kopieeractiviteit voor het kopiëren van gegevens tussen deze twee bovengrenswaarden uit de brondatabase naar de doeldatabase.

4. Gebruik de opgeslagen-procedureactiviteit voor het bijwerken van de oude bovengrenswaarde die in de eerste stap van de volgende iteratie moet worden gebruikt. 

### <a name="create-the-pipeline"></a>Maak de pijplijn
1. Maak een JSON-bestand met de naam IncrementalCopyPipeline.json in dezelfde map met de volgende inhoud: 

    ```json
    {
        "name": "IncrementalCopyPipeline",
        "properties": {
            "activities": [{
    
                "name": "IterateSQLTables",
                "type": "ForEach",
                "typeProperties": {
                    "isSequential": "false",
                    "items": {
                        "value": "@pipeline().parameters.tableList",
                        "type": "Expression"
                    },
    
                    "activities": [
                        {
                            "name": "LookupOldWaterMarkActivity",
                            "type": "Lookup",
                            "typeProperties": {
                                "source": {
                                    "type": "SqlSource",
                                    "sqlReaderQuery": "select * from watermarktable where TableName  =  '@{item().TABLE_NAME}'"
                                },
    
                                "dataset": {
                                    "referenceName": "WatermarkDataset",
                                    "type": "DatasetReference"
                                }
                            }
                        },
                        {
                            "name": "LookupNewWaterMarkActivity",
                            "type": "Lookup",
                            "typeProperties": {
                                "source": {
                                    "type": "SqlSource",
                                    "sqlReaderQuery": "select MAX(@{item().WaterMark_Column}) as NewWatermarkvalue from @{item().TABLE_NAME}"
                                },
    
                                "dataset": {
                                    "referenceName": "SourceDataset",
                                    "type": "DatasetReference"
                                }
                            }
                        },
    
                        {
                            "name": "IncrementalCopyActivity",
                            "type": "Copy",
                            "typeProperties": {
                                "source": {
                                    "type": "SqlSource",
                                    "sqlReaderQuery": "select * from @{item().TABLE_NAME} where @{item().WaterMark_Column} > '@{activity('LookupOldWaterMarkActivity').output.firstRow.WatermarkValue}' and @{item().WaterMark_Column} <= '@{activity('LookupNewWaterMarkActivity').output.firstRow.NewWatermarkvalue}'"
                                },
                                "sink": {
                                    "type": "SqlSink",
                                    "SqlWriterTableType": "@{item().TableType}",
                                    "SqlWriterStoredProcedureName": "@{item().StoredProcedureNameForMergeOperation}"
                                }
                            },
                            "dependsOn": [{
                                    "activity": "LookupNewWaterMarkActivity",
                                    "dependencyConditions": [
                                        "Succeeded"
                                    ]
                                },
                                {
                                    "activity": "LookupOldWaterMarkActivity",
                                    "dependencyConditions": [
                                        "Succeeded"
                                    ]
                                }
                            ],
    
                            "inputs": [{
                                "referenceName": "SourceDataset",
                                "type": "DatasetReference"
                            }],
                            "outputs": [{
                                "referenceName": "SinkDataset",
                                "type": "DatasetReference",
                                "parameters": {
                                    "SinkTableName": "@{item().TABLE_NAME}"
                                }
                            }]
                        },
    
                        {
                            "name": "StoredProceduretoWriteWatermarkActivity",
                            "type": "SqlServerStoredProcedure",
                            "typeProperties": {
    
                                "storedProcedureName": "sp_write_watermark",
                                "storedProcedureParameters": {
                                    "LastModifiedtime": {
                                        "value": "@{activity('LookupNewWaterMarkActivity').output.firstRow.NewWatermarkvalue}",
                                        "type": "datetime"
                                    },
                                    "TableName": {
                                        "value": "@{activity('LookupOldWaterMarkActivity').output.firstRow.TableName}",
                                        "type": "String"
                                    }
                                }
                            },
    
                            "linkedServiceName": {
                                "referenceName": "AzureSQLDatabaseLinkedService",
                                "type": "LinkedServiceReference"
                            },
    
                            "dependsOn": [{
                                "activity": "IncrementalCopyActivity",
                                "dependencyConditions": [
                                    "Succeeded"
                                ]
                            }]
                        }
    
                    ]
    
                }
            }],
    
            "parameters": {
                "tableList": {
                    "type": "Object"
                }
            }
        }
    }
    ```
2. Voer de cdmlet **Set-AzureRmDataFactoryV2Pipeline** uit om de pijplijn IncrementalCopyPipeline te maken.
    
   ```powershell
   Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "IncrementalCopyPipeline" -File ".\IncrementalCopyPipeline.json"
   ``` 

   Hier volgt een voorbeeld van uitvoer: 

   ```json
    PipelineName      : IncrementalCopyPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFIncMultiCopyTutorialFactory1201
    Activities        : {IterateSQLTables}
    Parameters        : {[tableList, Microsoft.Azure.Management.DataFactory.Models.ParameterSpecification]}
   ```
 
## <a name="run-the-pipeline"></a>De pijplijn uitvoeren

1. Maak een parameterbestand met de naam Parameters.json in dezelfde map met de volgende inhoud:

    ```json
    {
        "tableList": 
        [
            {
                "TABLE_NAME": "customer_table",
                "WaterMark_Column": "LastModifytime",
                "TableType": "DataTypeforCustomerTable",
                "StoredProcedureNameForMergeOperation": "sp_upsert_customer_table"
            },
            {
                "TABLE_NAME": "project_table",
                "WaterMark_Column": "Creationtime",
                "TableType": "DataTypeforProjectTable",
                "StoredProcedureNameForMergeOperation": "sp_upsert_project_table"
            }
        ]
    }
    ```
2. Voer de pijplijn IncrementalCopyPipeline uit met behulp van de cmdlet **Invoke-AzureRmDataFactoryV2Pipeline**. Vervang tijdelijke aanduidingen door de namen van uw eigen resourcegroep en data factory.

    ```powershell
    $RunId = Invoke-AzureRmDataFactoryV2Pipeline -PipelineName "IncrementalCopyPipeline" -ResourceGroup $resourceGroupName -dataFactoryName $dataFactoryName -ParameterFile ".\Parameters.json"        
    ``` 

## <a name="monitor-the-pipeline"></a>De pijplijn bewaken

1. Meld u aan bij [Azure Portal](https://portal.azure.com).

2. Selecteer **Meer services**, zoek met het trefwoord *Data Factory’s* en selecteer **Data factory’s**. 

    ![Het menu voor gegevensfactory's](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-data-factories-menu-1.png)

3. Zoek naar uw data factory in de lijst met data factory’s, en selecteer deze om de pagina **Data Factory** te openen. 

    ![Naar de data factory zoeken](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-search-data-factory-2.png)

4. Selecteer op de pagina **Data Factory** op de tegel de optie **Controleren en beheren**. 

    ![De tegel Bewaking en beheer](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-monitor-manage-tile-3.png)

5. De toepassing **Gegevensintegratie** wordt geopend op een afzonderlijk tabblad. U kunt alle pijplijnactiviteiten en hun status zien. Let erop dat in het volgende voorbeeld de status van de pijplijnactiviteit **Geslaagd** is. U kunt parameters controleren die zijn doorgegeven aan de pijplijn door de koppeling in de kolom **Parameters** te selecteren. Als er een fout is opgetreden, ziet u een koppeling in de kolom **Fout**. Selecteer de koppeling in de kolom **Acties**. 

    ![Pijplijnuitvoeringen](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-pipeline-runs-4.png)    
6. Wanneer u de koppeling in de kolom **Acties** selecteert, ziet u de volgende pagina met alle uitvoeringen van activiteiten voor de pijplijn: 

    ![Uitvoering van activiteiten](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-activity-runs-5.png)

7. Als u wilt teruggaan naar de weergave met **pijplijnuitvoeringen**, selecteert u **Pijplijnen** zoals weergegeven op de afbeelding. 

## <a name="review-the-results"></a>De resultaten bekijken
Voer in SQL Server Management Studio de volgende query's uit op de SQL-doeldatabase om te controleren of de gegevens van de brontabellen naar de doeltabellen zijn gekopieerd: 

**Query** 
```sql
select * from customer_table
```

**Uitvoer**
```
===========================================
PersonID    Name    LastModifytime
===========================================
1           John    2017-09-01 00:56:00.000
2           Mike    2017-09-02 05:23:00.000
3           Alice   2017-09-03 02:36:00.000
4           Andy    2017-09-04 03:21:00.000
5           Anny    2017-09-05 08:06:00.000
```

**Query**

```sql
select * from project_table
```

**Uitvoer**

```
===================================
Project     Creationtime
===================================
project1    2015-01-01 00:00:00.000
project2    2016-02-02 01:23:00.000
project3    2017-03-04 05:16:00.000
```

**Query**

```sql
select * from watermarktable
```

**Uitvoer**

```
======================================
TableName       WatermarkValue
======================================
customer_table  2017-09-05 08:06:00.000
project_table   2017-03-04 05:16:00.000
```

U ziet dat de bovengrenswaarden voor beide tabellen zijn bijgewerkt. 

## <a name="add-more-data-to-the-source-tables"></a>Meer gegevens toevoegen aan de brontabellen

Voer de volgende query uit op de SQL Server-brondatabase om een bestaande rij bij te werken in customer_table. Voeg een nieuwe rij in project_table in. 

```sql
UPDATE customer_table
SET [LastModifytime] = '2017-09-08T00:00:00Z', [name]='NewName' where [PersonID] = 3

INSERT INTO project_table
(Project, Creationtime)
VALUES
('NewProject','10/1/2017 0:00:00 AM');
``` 

## <a name="rerun-the-pipeline"></a>Voer de pijplijn uit

1. Voer nu de pijplijn opnieuw uit door de volgende PowerShell-opdracht te gebruiken:

    ```powershell
    $RunId = Invoke-AzureRmDataFactoryV2Pipeline -PipelineName "IncrementalCopyPipeline" -ResourceGroup $resourceGroupname -dataFactoryName $dataFactoryName -ParameterFile ".\Parameters.json"
    ```
2. Volg de pijplijnuitvoeringen met behulp van de instructies in de sectie [De pijplijn bewaken](#monitor-the-pipeline). Omdat de pijplijnstatus **In uitvoering** is, ziet u een andere actiekoppeling onder **Acties** om de pijplijn te annuleren. 

    ![Pijplijnuitvoeringen worden uitgevoerd](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-pipeline-runs-6.png)

3. Klik op **Vernieuwen** om te lijst te vernieuwen totdat de uitvoering van de pijplijn is voltooid. 

    ![Pijplijnuitvoeringen vernieuwen](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-pipeline-runs-succeded-7.png)

4. Selecteer desgewenst de koppeling **Uitvoeringen van activiteit weergeven** onder **Acties** om alle activiteitsuitvoeringen te bekijken die gekoppeld zijn aan deze pijplijnuitvoering. 

## <a name="review-the-final-results"></a>De eindresultaten bekijken
Voer in SQL Server Management Studio de volgende query's uit op de doeldatabase om te controleren dat de bijgewerkte/nieuwe gegevens van de brontabellen naar de doeltabellen zijn gekopieerd. 

**Query** 
```sql
select * from customer_table
```

**Uitvoer**
```
===========================================
PersonID    Name    LastModifytime
===========================================
1           John    2017-09-01 00:56:00.000
2           Mike    2017-09-02 05:23:00.000
3           NewName 2017-09-08 00:00:00.000
4           Andy    2017-09-04 03:21:00.000
5           Anny    2017-09-05 08:06:00.000
```

Let op de nieuwe waarden van **Name** en **LastModifytime** voor de **PersonID** voor nummer 3. 

**Query**

```sql
select * from project_table
```

**Uitvoer**

```
===================================
Project     Creationtime
===================================
project1    2015-01-01 00:00:00.000
project2    2016-02-02 01:23:00.000
project3    2017-03-04 05:16:00.000
NewProject  2017-10-01 00:00:00.000
```

Let erop dat de invoer van **NewProject** toegevoegd is aan project_table. 

**Query**

```sql
select * from watermarktable
```

**Uitvoer**

```
======================================
TableName       WatermarkValue
======================================
customer_table  2017-09-08 00:00:00.000
project_table   2017-10-01 00:00:00.000
```

U ziet dat de bovengrenswaarden voor beide tabellen zijn bijgewerkt.
     
## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u de volgende stappen uitgevoerd: 

> [!div class="checklist"]
> * Bereid de bron- en doelserver gegevensopslag voor.
> * Een data factory maken.
> * Een zelf-hostende integration runtime (IR) maken.
> * De Integration Runtime installeren.
> * Maak gekoppelde services. 
> * Bron-, sink- en grenswaardegegevenssets maken.
> * Maken, starten en controleren van een pijplijn.
> * Bekijk de resultaten.
> * Gegevens in brontabellen toevoegen of bijwerken.
> * De pijplijn opnieuw uitvoeren en controleren.
> * De eindresultaten bekijken.

Ga naar de volgende zelfstudie voor meer informatie over het transformeren van gegevens met behulp van een Spark-cluster in Azure:

> [!div class="nextstepaction"]
>[Incrementeel gegevens kopiëren van Azure SQL Database naar Azure Blob Storage met behulp van technologie voor het bijhouden van wijzigingen](tutorial-incremental-copy-change-tracking-feature-powershell.md)


