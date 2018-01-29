---
title: "Gegevens bulksgewijs kopiëren met behulp van Azure Data Factory | Microsoft Docs"
description: "Informatie over het gebruik van Azure Data Factory en Activiteit kopiëren om gegevens bulksgewijs van een brongegevensopslag naar een doelgegevensopslag te kopiëren."
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
ms.openlocfilehash: 9971eb9e069d9fe1148c293c3459a8b11d931c2a
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/23/2018
---
# <a name="copy-multiple-tables-in-bulk-by-using-azure-data-factory"></a>Meerdere tabellen bulksgewijs kopiëren met behulp van Azure Data Factory
Deze zelfstudie demonstreert het **kopiëren van een aantal tabellen uit Azure SQL Database naar Azure SQL Data Warehouse**. U kunt hetzelfde patroon toepassen in andere kopieerscenario's. Bijvoorbeeld het kopiëren van tabellen van SQL Server/Oracle naar Azure SQL Database/Data Warehouse/Azure Blob, verschillende paden kopiëren van Blob naar Azure SQL Database-tabellen.

> [!NOTE]
> Dit artikel is van toepassing op versie 2 van Data Factory, dat zich momenteel in de previewfase bevindt. Als u versie 1 van de Data Factory-service gebruikt, die algemeen beschikbaar is (GA), raadpleegt u [Documentatie van versie 1 van Data Factory](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Op hoog niveau bevat deze zelfstudie de volgende stappen:

> [!div class="checklist"]
> * Een data factory maken.
> * Gekoppelde Azure SQL Database-, Azure SQL Data Warehouse- en Azure Storage-services maken.
> * Gegevenssets voor Azure SQL Database en Azure SQL Data Warehouse maken.
> * Een pijplijn maken om de te kopiëren tabellen op te zoeken en een andere pijplijn om de kopieerbewerking daadwerkelijk uit te voeren. 
> * Een pijplijnuitvoering starten.
> * De uitvoering van de pijplijn en van de activiteit controleren.

In deze zelfstudie wordt Azure PowerShell gebruikt. Zie [Quickstarts](quickstart-create-data-factory-dot-net.md) (Snelstartgidsen) voor meer informatie over het gebruik van andere hulpprogramma's/SDK's voor het maken van een gegevensfactory. 

## <a name="end-to-end-workflow"></a>End-to-end werkstroom
In dit scenario hebben we een aantal tabellen in Azure SQL Database die we willen kopiëren naar SQL Data Warehouse. Dit is de logische volgorde van de stappen in de werkstroom die in pijplijnen plaatsvindt:

![Werkstroom](media/tutorial-bulk-copy/tutorial-copy-multiple-tables.png)

* De eerste pijplijn zoekt de lijst op met tabellen die moeten worden gekopieerd naar de sinkgegevensopslag.  U kunt ook een metagegevenstabel bijhouden waarin alle tabellen worden vermeld die moeten worden gekopieerd naar de sinkgegevensopslag. De pijplijn activeert vervolgens een andere pijplijn, die elke tabel in de database langsloopt en de bewerking uitvoert waarmee de gegevens worden gekopieerd.
* De tweede pijplijn voert de daadwerkelijke kopieerbewerking uit. De lijst met tabellen wordt gebruikt als parameter. Kopieer voor elke tabel in de lijst de specifieke tabel in Azure SQL Database naar de bijbehorende tabel in SQL Data Warehouse met behulp van [gefaseerd kopiëren via Blob storage en PolyBase](connector-azure-sql-data-warehouse.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) (Engelstalig artikel) voor de beste prestaties. In dit voorbeeld wordt de lijst met tabellen in de eerste pijplijn doorgegeven als een waarde voor de parameter. 

Als u nog geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/) voordat u begint.

## <a name="prerequisites"></a>Vereisten

* **Azure PowerShell**. Volg de instructies in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps) (Azure PowerShell installeren en configureren).
* **Een Azure Storage-account**. Het Azure Storage-account wordt gebruikt als faseringsblobopslag in de bulksgewijze kopieerbewerking. 
* **Azure SQL-database**. Deze database bevat de brongegevens. 
* **Azure SQL Data Warehouse**. Dit datawarehouse bevat de uit de SQL Database gekopieerde gegevens. 

### <a name="prepare-sql-database-and-sql-data-warehouse"></a>SQL Database en SQL Data Warehouse voorbereiden

**De Azure SQL Database-bron voorbereiden**:

Maak een Azure SQL Database met Adventure Works LT-testgegevens door het artikel [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) (Een Azure SQL-database maken) te volgen. In deze zelfstudie worden alle tabellen van deze voorbeelddatabase naar een SQL0datawarehouse gekopieerd.

**De Azure SQL Data Warehouse-sink voorbereiden**:

1. Als u geen Azure SQL Data Warehouse hebt, raadpleegt u het artikel [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-tutorial.md) (Een Azure SQL-database maken) voor de stappen om er een te maken.

2. Maak bijbehorende tabelschema's in SQL Data Warehouse. U kunt het [hulpprogramma voor migratie](https://www.microsoft.com/download/details.aspx?id=49100) gebruiken om het **schema te migreren** van Azure SQL Database naar Azure SQL Data Warehouse. U gebruikt Azure Data Factory om gegevens in een latere stap te migreren/kopiëren.

## <a name="azure-services-to-access-sql-server"></a>Azure-services voor toegang tot SQL-server

Geef Azure-services toegang tot SQL-server voor zowel SQL Database als SQL Data Warehouse. Zorg ervoor dat de instelling **Toegang tot Azure-services toestaan** voor uw Azure SQL-server op **AAN** staat. Met deze instelling kan de Data Factory-service gegevens lezen uit uw Azure SQL Database en schrijven naar uw Azure SQL Data Warehouse. Voer de volgende stappen uit om dit te controleren en de instelling in te schakelen:

1. Klik op de hub **Meer services** aan de linkerkant en klik op **SQL-servers**.
2. Selecteer uw server en klik op **Firewall** onder **INSTELLINGEN**.
3. Klik op de pagina **Firewallinstellingen** op **AAN** bij **Toegang tot Azure-services toestaan**.

## <a name="create-a-data-factory"></a>Een gegevensfactory maken

1. Start **PowerShell**. Houd Azure PowerShell open tot het einde van deze zelfstudie. Als u het programma sluit en opnieuw opent, moet u de opdrachten opnieuw uitvoeren.

    Voer de volgende opdracht uit en geef de gebruikersnaam en het wachtwoord op waarmee u zich aanmeldt bij Azure Portal:
        
    ```powershell
    Login-AzureRmAccount
    ```
    Voer de volgende opdracht uit om alle abonnementen voor dit account weer te geven:

    ```powershell
    Get-AzureRmSubscription
    ```
    Voer de volgende opdracht uit om het abonnement te selecteren waarmee u wilt werken. Vervang **SubscriptionId** door de id van uw Azure-abonnement:

    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<SubscriptionId>"
    ```
2. Voer de cmdlet **Set AzureRmDataFactoryV2** uit om een data factory te maken. Vervang voordat u de opdracht uitvoert de tijdelijke aanduidingen door uw eigen waarden. 

    ```powershell
    $resourceGroupName = "<your resource group to create the factory>"
    $dataFactoryName = "<specify the name of data factory to create. It must be globally unique.>"
    Set-AzureRmDataFactoryV2 -ResourceGroupName $resourceGroupName -Location "East US" -Name $dataFactoryName
    ```

    Houd rekening met de volgende punten:

    * De naam van de Azure-gegevensfactory moet wereldwijd uniek zijn. Als de volgende fout zich voordoet, wijzigt u de naam en probeert u het opnieuw.

        ```
        The specified Data Factory name 'ADFv2QuickStartDataFactory' is already in use. Data Factory names must be globally unique.
        ```

    * Als u Data Factory-exemplaren wilt maken, moet u bijdrager of beheerder zijn van het Azure-abonnement.
    * Momenteel kunt u in Data Factory V2 alleen data factory's maken in de regio's VS - oost, VS - oost 2 en West-Europa. De gegevensopslagexemplaren (Azure Storage, Azure SQL Database, enzovoort) en berekeningen (HDInsight, enzovoort) die worden gebruikt in Data Factory, kunnen zich in andere regio's bevinden.

## <a name="create-linked-services"></a>Gekoppelde services maken

In deze zelfstudie maakt u drie gekoppelde services maken voor respectievelijk de bron-, sink- en faseringsblob, met verbindingen met uw gegevensopslag:

### <a name="create-the-source-azure-sql-database-linked-service"></a>Maak de gekoppelde Azure SQL Database-bronservice.

1. Maak een JSON-bestand met de naam **AzureSqlDatabaseLinkedService.json** in de map **C:\ADFv2TutorialBulkCopy** met de volgende inhoud (maak de map ADFv2TutorialBulkCopy als deze nog niet bestaat):

    > [!IMPORTANT]
    > Vervang &lt;servername&gt;, &lt;databasename&gt;, &lt;username&gt;@&lt;servername&gt; en &lt;password&gt; door de waarden van uw Azure SQL Database voordat u het bestand opslaat.

    ```json
    {
        "name": "AzureSqlDatabaseLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
                }
            }
        }
    }
    ```

2. Schakel in **Azure PowerShell** over naar de map **ADFv2TutorialBulkCopy**.

3. Voer de cmdlet **Set-AzureRmDataFactoryV2LinkedService** uit om de gekoppelde service **AzureSqlDatabaseLinkedService** te maken. 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureSqlDatabaseLinkedService" -File ".\AzureSqlDatabaseLinkedService.json"
    ```

    Hier volgt een voorbeeld van uitvoer:

    ```json
    LinkedServiceName : AzureSqlDatabaseLinkedService
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlDatabaseLinkedService
    ```

### <a name="create-the-sink-azure-sql-data-warehouse-linked-service"></a>De gekoppelde Azure SQL Data Warehouse-sinkservice maken

1. Maak een JSON-bestand met de naam **AzureSqlDWLinkedService.json** in de map **C:\ADFv2TutorialBulkCopy**. Geef dit bestand de volgende inhoud:

    > [!IMPORTANT]
    > Vervang &lt;servername&gt;, &lt;databasename&gt;, &lt;username&gt;@&lt;servername&gt; en &lt;password&gt; door de waarden van uw Azure SQL Database voordat u het bestand opslaat.

    ```json
    {
        "name": "AzureSqlDWLinkedService",
        "properties": {
            "type": "AzureSqlDW",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
            }
        }
    }
    ```

2. Maak de gekoppelde service **AzureSqlDWLinkedService** door de cmdlet **Set-AzureRmDataFactoryV2LinkedService** uit te voeren.

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureSqlDWLinkedService" -File ".\AzureSqlDWLinkedService.json"
    ```

    Hier volgt een voorbeeld van uitvoer:

    ```json
    LinkedServiceName : AzureSqlDWLinkedService
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlDWLinkedService
    ```

### <a name="create-the-staging-azure-storage-linked-service"></a>De gekoppelde Azure Storage-faseringsservice maken

In deze zelfstudie gebruikt u Azure Blob-opslag als een tussentijds faseringsgebied voor het inschakelen van PolyBase voor betere kopieerprestaties.

1. Maak een JSON-bestand met de naam **AzureStorageLinkedService.json** in de map **C:\ADFv2TutorialBulkCopy** met de volgende inhoud:

    > [!IMPORTANT]
    > Vervang &lt;accountName&gt; en &lt;accountKey&gt; door de naam en sleutel van uw Azure Storage-account voordat u het bestand opslaat.

    ```json
    {
        "name": "AzureStorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "DefaultEndpointsProtocol=https;AccountName=<accountName>;AccountKey=<accountKey>"
                }
            }
        }
    }
    ```

2. Maak de gekoppelde service **AzureStorageLinkedService** door de cmdlet **Set-AzureRmDataFactoryV2LinkedService** uit te voeren.

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureStorageLinkedService" -File ".\AzureStorageLinkedService.json"
    ```

    Hier volgt een voorbeeld van uitvoer:

    ```json
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureStorageLinkedService
    ```

## <a name="create-datasets"></a>Gegevenssets maken

In deze zelfstudie maakt u bron- en sinkgegevenssets, waarmee de locatie wordt opgegeven waar de gegevens zijn opgeslagen:

### <a name="create-a-dataset-for-source-sql-database"></a>Een gegevensset maken voor bron SQL-Database

1. Maak een JSON-bestand met de naam **AzureSqlDatabaseDataset.json** in de map **C:\ADFv2TutorialBulkCopy**. Geef dit bestand de volgende inhoud. De 'tableName' is a dummy; u gebruikt later de SQL-query in de kopieeractiviteit om gegevens op te halen.

    ```json
    {
        "name": "AzureSqlDatabaseDataset",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": {
                "referenceName": "AzureSqlDatabaseLinkedService",
                "type": "LinkedServiceReference"
            },
            "typeProperties": {
                "tableName": "dummy"
            }
        }
    }
    ```

2. Maak de gegevensset **AzureSqlDatabaseDataset** door de cmdlet **Set-AzureRmDataFactoryV2Dataset** uit te voeren.

    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureSqlDatabaseDataset" -File ".\AzureSqlDatabaseDataset.json"
    ```

    Hier volgt een voorbeeld van uitvoer:

    ```json
    DatasetName       : AzureSqlDatabaseDataset
    ResourceGroupName : <resourceGroupname>
    DataFactoryName   : <dataFactoryName>
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlTableDataset
    ```

### <a name="create-a-dataset-for-sink-sql-data-warehouse"></a>Een gegevensset maken voor de sink in SQL Data Warehouse

1. Maak een JSON-bestand met de naam **AzureSqlDWDataset.json** in de map **C:\ADFv2TutorialBulkCopy**, met de volgende inhoud: De tableName' wordt ingesteld als een parameter; de kopieeractiviteit waarin naar deze gegevensset wordt verwezen, geeft later de werkelijke waarde door naar de gegevensset.

    ```json
    {
        "name": "AzureSqlDWDataset",
        "properties": {
            "type": "AzureSqlDWTable",
            "linkedServiceName": {
                "referenceName": "AzureSqlDWLinkedService",
                "type": "LinkedServiceReference"
            },
            "typeProperties": {
                "tableName": {
                    "value": "@{dataset().DWTableName}",
                    "type": "Expression"
                }
            },
            "parameters":{
                "DWTableName":{
                    "type":"String"
                }
            }
        }
    }
    ```

2. Maak de gegevensset **AzureSqlDWDataset** door de cmdlet **Set-AzureRmDataFactoryV2Dataset** uit te voeren.

    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureSqlDWDataset" -File ".\AzureSqlDWDataset.json"
    ```

    Hier volgt een voorbeeld van uitvoer:

    ```json
    DatasetName       : AzureSqlDWDataset
    ResourceGroupName : <resourceGroupname>
    DataFactoryName   : <dataFactoryName>
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlDwTableDataset
    ```

## <a name="create-pipelines"></a>Pijplijnen maken

In deze zelfstudie maakt u twee pijplijnen:

### <a name="create-the-pipeline-iterateandcopysqltables"></a>De pijplijn 'IterateAndCopySQLTables' maken

In deze pijplijn wordt een lijst met tabellen gebruikt als parameter. Voor elke tabel in de lijst worden gegevens uit de tabel in Azure SQL Database naar Azure SQL Data Warehouse gekopieerd met behulp van gefaseerd kopiëren en PolyBase.

1. Maak een JSON-bestand met de naam **IterateAndCopySQLTables.json** in de map **C:\ADFv2TutorialBulkCopy**. Geef dit bestand de volgende inhoud:

    ```json
    {
        "name": "IterateAndCopySQLTables",
        "properties": {
            "activities": [
                {
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
                                "name": "CopyData",
                                "description": "Copy data from SQL database to SQL DW",
                                "type": "Copy",
                                "inputs": [
                                    {
                                        "referenceName": "AzureSqlDatabaseDataset",
                                        "type": "DatasetReference"
                                    }
                                ],
                                "outputs": [
                                    {
                                        "referenceName": "AzureSqlDWDataset",
                                        "type": "DatasetReference",
                                        "parameters": {
                                            "DWTableName": "[@{item().TABLE_SCHEMA}].[@{item().TABLE_NAME}]"
                                        }
                                    }
                                ],
                                "typeProperties": {
                                    "source": {
                                        "type": "SqlSource",
                                        "sqlReaderQuery": "SELECT * FROM [@{item().TABLE_SCHEMA}].[@{item().TABLE_NAME}]"
                                    },
                                    "sink": {
                                        "type": "SqlDWSink",
                                        "preCopyScript": "TRUNCATE TABLE [@{item().TABLE_SCHEMA}].[@{item().TABLE_NAME}]",
                                        "allowPolyBase": true
                                    },
                                    "enableStaging": true,
                                    "stagingSettings": {
                                        "linkedServiceName": {
                                            "referenceName": "AzureStorageLinkedService",
                                            "type": "LinkedServiceReference"
                                        }
                                    }
                                }
                            }
                        ]
                    }
                }
            ],
            "parameters": {
                "tableList": {
                    "type": "Object"
                }
            }
        }
    }
    ```

2. Maak de pijplijn **IterateAndCopySQLTables** door de cmdlet **Set-AzureRmDataFactoryV2Pipeline** uit te voeren.

    ```powershell
    Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "IterateAndCopySQLTables" -File ".\IterateAndCopySQLTables.json"
    ```

    Hier volgt een voorbeeld van uitvoer:

    ```json
    PipelineName      : IterateAndCopySQLTables
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Activities        : {IterateSQLTables}
    Parameters        : {[tableList, Microsoft.Azure.Management.DataFactory.Models.ParameterSpecification]}
    ```

### <a name="create-the-pipeline-gettablelistandtriggercopydata"></a>De pijplijn 'GetTableListAndTriggerCopyData' maken

Deze pijplijn voert twee stappen uit:

* Zoekt de systeemtabel van Azure SQL Database op om de lijst met te kopiëren tabellen op te halen.
* Activeert de pijplijn 'IterateAndCopySQLTables' om het kopiëren van de gegevens daadwerkelijk uit te voeren.

1. Maak een JSON-bestand met de naam **GetTableListAndTriggerCopyData.json** in de map **C:\ADFv2TutorialBulkCopy**. Geef dit bestand de volgende inhoud:

    ```json
    {
        "name":"GetTableListAndTriggerCopyData",
        "properties":{
            "activities":[
                { 
                    "name": "LookupTableList",
                    "description": "Retrieve the table list from Azure SQL dataabse",
                    "type": "Lookup",
                    "typeProperties": {
                        "source": {
                            "type": "SqlSource",
                            "sqlReaderQuery": "SELECT TABLE_SCHEMA, TABLE_NAME FROM information_schema.TABLES WHERE TABLE_TYPE = 'BASE TABLE' and TABLE_SCHEMA = 'SalesLT' and TABLE_NAME <> 'ProductModel'"
                        },
                        "dataset": {
                            "referenceName": "AzureSqlDatabaseDataset",
                            "type": "DatasetReference"
                        },
                        "firstRowOnly": false
                    }
                },
                {
                    "name": "TriggerCopy",
                    "type": "ExecutePipeline",
                    "typeProperties": {
                        "parameters": {
                            "tableList": {
                                "value": "@activity('LookupTableList').output.value",
                                "type": "Expression"
                            }
                        },
                        "pipeline": {
                            "referenceName": "IterateAndCopySQLTables",
                            "type": "PipelineReference"
                        },
                        "waitOnCompletion": true
                    },
                    "dependsOn": [
                        {
                            "activity": "LookupTableList",
                            "dependencyConditions": [
                                "Succeeded"
                            ]
                        }
                    ]
                }
            ]
        }
    }
    ```

2. Maak de pijplijn **GetTableListAndTriggerCopyData** door de cmdlet **Set-AzureRmDataFactoryV2Pipeline** uit te voeren.

    ```powershell
    Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "GetTableListAndTriggerCopyData" -File ".\GetTableListAndTriggerCopyData.json"
    ```

    Hier volgt een voorbeeld van uitvoer:

    ```json
    PipelineName      : GetTableListAndTriggerCopyData
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Activities        : {LookupTableList, TriggerCopy}
    Parameters        :
    ```

## <a name="start-and-monitor-pipeline-run"></a>Pijplijnuitvoering starten en controleren

1. Start een pijplijnuitvoering voor de pijplijn GetTableListAndTriggerCopyData en leg de id voor de pijplijnuitvoering vast voor toekomstige controle. Onder wordt het uitvoeren van de pijplijn 'IterateAndCopySQLTables' geactiveerd zoals opgegeven in de activiteit ExecutePipeline.

    ```powershell
    $runId = Invoke-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineName 'GetTableListAndTriggerCopyData'
    ```

2.  Voer het volgende script uit om continu de uitvoeringsstatus van de pijplijn **GetTableListAndTriggerCopyData** te controleren, en druk het eindresultaat van de pijplijnuitvoering en de uitvoering van de activiteit af.

    ```powershell
    while ($True) {
        $run = Get-AzureRmDataFactoryV2PipelineRun -ResourceGroupName $resourceGroupName -DataFactoryName $DataFactoryName -PipelineRunId $runId

        if ($run) {
            if ($run.Status -ne 'InProgress') {
                Write-Host "Pipeline run finished. The status is: " $run.Status -foregroundcolor "Yellow"
                Write-Host "Pipeline run details:" -foregroundcolor "Yellow"
                $run
                break
            }
            Write-Host  "Pipeline is running...status: InProgress" -foregroundcolor "Yellow"
        }

        Start-Sleep -Seconds 15
    }

    $result = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $runId -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)
    Write-Host "Activity run details:" -foregroundcolor "Yellow"
    $result
    ```

    Hier volgt een voorbeeld van de voorbeelduitvoering:

    ```json
    Pipeline run details:
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    RunId             : 0000000000-00000-0000-0000-000000000000
    PipelineName      : GetTableListAndTriggerCopyData
    LastUpdated       : 9/18/2017 4:08:15 PM
    Parameters        : {}
    RunStart          : 9/18/2017 4:06:44 PM
    RunEnd            : 9/18/2017 4:08:15 PM
    DurationInMs      : 90637
    Status            : Succeeded
    Message           : 

    Activity run details:
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    ActivityName      : LookupTableList
    PipelineRunId     : 0000000000-00000-0000-0000-000000000000
    PipelineName      : GetTableListAndTriggerCopyData
    Input             : {source, dataset, firstRowOnly}
    Output            : {count, value, effectiveIntegrationRuntime}
    LinkedServiceName : 
    ActivityRunStart  : 9/18/2017 4:06:46 PM
    ActivityRunEnd    : 9/18/2017 4:07:09 PM
    DurationInMs      : 22995
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}

    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    ActivityName      : TriggerCopy
    PipelineRunId     : 0000000000-00000-0000-0000-000000000000
    PipelineName      : GetTableListAndTriggerCopyData
    Input             : {pipeline, parameters, waitOnCompletion}
    Output            : {pipelineRunId}
    LinkedServiceName : 
    ActivityRunStart  : 9/18/2017 4:07:11 PM
    ActivityRunEnd    : 9/18/2017 4:08:14 PM
    DurationInMs      : 62581
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    ```

3. U kunt de run-id van de pijplijn '**IterateAndCopySQLTables**' ophalen en vervolgens het gedetailleerde uitvoeringsresultaat van de activiteit controleren.

    ```powershell
    Write-Host "Pipeline 'IterateAndCopySQLTables' run result:" -foregroundcolor "Yellow"
    ($result | Where-Object {$_.ActivityName -eq "TriggerCopy"}).Output.ToString()
    ```

    Hier volgt een voorbeeld van de voorbeelduitvoering:

    ```json
    {
        "pipelineRunId": "7514d165-14bf-41fb-b5fb-789bea6c9e58"
    }
    ```

    ```powershell
    $result2 = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId <copy above run ID> -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)
    $result2
    ```

3. Maak verbinding met de Azure SQL Data Warehouse-sinkopslag en bevestig dat de gegevens juist zijn gekopieerd vanuit Azure SQL Database.

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u de volgende stappen uitgevoerd: 

> [!div class="checklist"]
> * Een data factory maken.
> * Gekoppelde Azure SQL Database-, Azure SQL Data Warehouse- en Azure Storage-services maken.
> * Gegevenssets voor Azure SQL Database en Azure SQL Data Warehouse maken.
> * Een pijplijn maken om de te kopiëren tabellen op te zoeken en een andere pijplijn om de kopieerbewerking daadwerkelijk uit te voeren. 
> * Een pijplijnuitvoering starten.
> * De uitvoering van de pijplijn en van de activiteit controleren.

Ga door naar de volgende zelfstudie voor informatie over het incrementeel kopiëren van gegevens uit een bron naar een bestemming:
> [!div class="nextstepaction"]
>[Gegevens incrementeel kopiëren](tutorial-incremental-copy-powershell.md)