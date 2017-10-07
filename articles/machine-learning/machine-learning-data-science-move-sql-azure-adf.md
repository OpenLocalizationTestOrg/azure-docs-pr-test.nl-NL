---
title: aaaMove gegevens uit een lokale SQL Server tooSQL Azure met Azure Data Factory | Microsoft Docs
description: Een ADF-pijplijn die twee activiteiten van de gegevens migreren die gegevens samen dagelijks tussen databases on-premises en in de cloud Hallo verplaatsen stelt het bericht instellen.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 7f7e78c7a84a259539221d3235b76bb5a3cf9866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-sql-server-toosql-azure-with-azure-data-factory"></a>Gegevens verplaatsen van een lokale SQL server tooSQL Azure met Azure Data Factory
Dit onderwerp leest hoe toomove gegevens uit een lokale SQL Server-Database tooa SQL Azure Database via Azure Blob Storage met behulp van Azure Data Factory (ADF) Hallo.

Zie voor een tabel die een overzicht van de verschillende opties voor verplaatsen gegevens tooan Azure SQL Database, [verplaatsen van gegevens tooan Azure SQL Database voor Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).

## <a name="intro"></a>Inleiding: Wat is er ADF en wanneer moet het gebruikte toomigrate gegevens?
Azure Data Factory is een volledig beheerde gegevens cloud-gebaseerde integration-service die is ingedeeld en automatiseert Hallo verplaatsing en transformatie van gegevens. Hallo sleutel concept in Hallo ADF model is pijplijn. Een pijplijn is een logische groepering van activiteiten, die elk Hallo acties tooperform op Hallo gegevens in de gegevenssets definieert. Gekoppelde services zijn gebruikte toodefine Hallo informatie die nodig is voor de gegevensbronnen voor Data Factory tooconnect toohello.

Met ADF, bestaande services voor gegevensverwerking in gegevenspijplijnen die maximaal beschikbaar en wordt beheerd in de cloud Hallo samengesteld. Deze gegevenspijplijnen kunnen worden geplande tooingest, voorbereiden, transformeren, analyseren en gegevens publiceren en ADF beheert en stuurt Hallo complexe gegevens en afhankelijkheden voor verwerking. Oplossingen worden snel gebouwd en geïmplementeerde in Hallo cloud, verbinding maken met een toenemend aantal lokale en cloud-gegevensbronnen.

Overweeg het gebruik van ADF:

* Wanneer gegevens die behoeften toobe voortdurend gemigreerd in een hybride scenario die toegang heeft tot zowel on-premises en cloudresources
* Wanneer gegevens Hallo is transactionele of behoeften toobe gewijzigd of bedrijfslogica toegevoegd tooit wanneer wordt gemigreerd.

ADF kunt Hallo planning en bewaking van taken met behulp van eenvoudige JSON-scripts die Hallo verplaatsing van gegevens op periodieke basis beheren. ADF heeft ook andere mogelijkheden, zoals ondersteuning voor complexe bewerkingen. Zie voor meer informatie over ADF Hallo-documentatie op [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).

## <a name="scenario"></a>Hallo Scenario
We instellen een ADF-pijplijn die de activiteiten van de migratie twee gegevens stelt het bericht. Samen wordt gegevens dagelijks verplaatsen tussen een lokale SQL-database en een Azure SQL Database in de cloud Hallo. Hallo twee activiteiten zijn:

* gegevens kopiëren van een lokale SQL Server-database tooan Azure Blob Storage-account
* gegevens kopiëren van hello Azure Blob Storage-account tooan Azure SQL Database.

> [!NOTE]
> stappen die hier zijn aangepast van Hallo meer zelfstudie geleverd door Hallo ADF-team gedetailleerde weergegeven Hallo: [gegevens verplaatsen tussen lokale bronnen en cloud met Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) toohello relevante secties van dit onderwerp verwijst naar Als het nodig zijn worden opgegeven.
>
>

## <a name="prereqs"></a>Vereisten
Deze zelfstudie wordt ervan uitgegaan dat u hebt:

* Een **Azure-abonnement**. Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).
* Een **Azure storage-account**. U kunt een Azure storage-account gebruiken voor het opslaan van Hallo gegevens in deze zelfstudie. Als u geen Azure storage-account hebt, raadpleegt u Hallo [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) artikel. Nadat u Hallo storage-account hebt gemaakt, moet u tooobtain Hallo account sleutel tooaccess Hallo opslagruimte hebt gebruikt. Zie [beheren van uw toegangssleutels voor opslag](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Toegang tooan **Azure SQL Database**. Als u een Azure SQL Database, moet Hallo tpoic [aan de slag met Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) bevat informatie over het tooprovision een nieuw exemplaar van een Azure SQL Database.
* Geïnstalleerd en geconfigureerd **Azure PowerShell** lokaal. Zie voor instructies [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

> [!NOTE]
> Met deze procedure gebruikt Hallo [Azure-portal](https://portal.azure.com/).
>
>

## <a name="upload-data"></a>Het uploaden van Hallo gegevens tooyour lokale SQL Server
We gebruiken Hallo [NYC Taxi gegevensset](http://chriswhong.com/open-data/foil_nyc_taxi/) toodemonstrate Hallo-migratieproces. Hallo NYC Taxi gegevensset beschikbaar is, zoals beschreven in deze post, op Azure-blobopslag [NYC Taxi gegevens](http://www.andresmh.com/nyctaxitrips/). Hallo gegevens heeft twee bestanden, Hallo trip_data.csv bestand, dat reis details bevat, en Hallo trip_far.csv bestand, met details over Hallo tarief voor elke reis betaald. Een beschrijving van deze bestanden en voorbeelden vindt u in [NYC Taxi reizen gegevensset beschrijving](machine-learning-data-science-process-sql-walkthrough.md#dataset).

Hallo-procedure die hier tooa set van uw eigen gegevens aanpassen of Hallo stappen zoals beschreven met behulp van Hallo NYC Taxi gegevensset. tooupload hello NYC Taxi gegevensset in uw lokale SQL Server-database, volgt u Hallo procedure beschreven in [gegevens voor bulksgewijs importeren in SQL Server-Database](machine-learning-data-science-process-sql-walkthrough.md#dbload). Deze instructies zijn voor een SQL-Server op een virtuele Machine van Azure, maar de procedure voor het uploaden van de lokale SQL Server is toohello Hallo Hallo dezelfde.

## <a name="create-adf"></a>Een Azure-Gegevensfactory maken
instructies voor het maken van een nieuwe Azure Data Factory en een resourcegroep in Hallo Hallo [Azure-portal](https://portal.azure.com/) vindt u [maken van een Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory). Naam Hallo nieuw ADF exemplaar *adfdsp* en naam Hallo-resourcegroep gemaakt *adfdsprg*.

## <a name="install-and-configure-up-hello-data-management-gateway"></a>Installeren en configureren van Hallo Data Management Gateway
tooenable uw pijplijnen in een Azure data factory-toowork met een lokale SQL Server, moet u tooadd als een gekoppelde Service toohello data factory. toocreate een gekoppelde Service voor een lokale SQL Server, moet u:

* Download en installeer Microsoft Data Management Gateway op Hallo lokale computer.
* Hallo gekoppelde service voor Hallo lokale bron toouse Hallo gegevensgateway configureren.

Hallo Data Management Gateway serialiseert en deserializes Hallo bron- en sink-gegevens op Hallo-computer waarop deze wordt gehost.

Zie voor installatie-instructies en informatie over Data Management Gateway [gegevens verplaatsen tussen lokale bronnen en cloud met Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)

## <a name="adflinkedservices"></a>Gekoppelde services tooconnect toohello gegevens resources maken
Een gekoppelde service definieert Hallo-informatie die nodig is voor Azure Data Factory tooconnect tooa Gegevensresource. Hallo Stapsgewijze instructies voor het maken van de gekoppelde services is beschikbaar in [gekoppelde services maken](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).

Er zijn drie bronnen in dit scenario waarvoor de gekoppelde services vereist zijn.

1. [Gekoppelde service voor on-premises SQL-Server](#adf-linked-service-onprem-sql)
2. [Gekoppelde service voor Azure Blob-opslag](#adf-linked-service-blob-store)
3. [Gekoppelde service voor Azure SQL database](#adf-linked-service-azure-sql)

### <a name="adf-linked-service-onprem-sql"></a>Gekoppelde service voor on-premises SQL Server-database
toocreate hello gekoppelde service voor Hallo lokale SQL Server:

* Klik op Hallo **gegevensarchief** in Hallo ADF-startpagina op de klassieke Azure-Portal
* Selecteer **SQL** en Voer Hallo *gebruikersnaam* en *wachtwoord* voor Hallo on-premises SQL Server-referenties. U moet tooenter Hallo servername als een **volledig gekwalificeerde servernaam backslash exemplaarnaam (servernaam\exemplaarnaam)**. Naam Hallo gekoppelde service *adfonpremsql*.

### <a name="adf-linked-service-blob-store"></a>Gekoppelde service voor Blob
toocreate Hallo gekoppelde service voor hello Azure Blob Storage-account:

* Klik op Hallo **gegevensarchief** in Hallo ADF-startpagina op de klassieke Azure-Portal
* Selecteer **Azure Storage-Account**
* Geef hello Azure Blob Storage-account sleutel en container. Naam Hallo gekoppelde Service *adfds*.

### <a name="adf-linked-service-azure-sql"></a>Gekoppelde service voor Azure SQL database
toocreate Hallo gekoppelde service voor hello Azure SQL Database:

* Klik op Hallo **gegevensarchief** in Hallo ADF-startpagina op de klassieke Azure-Portal
* Selecteer **Azure SQL** en Voer Hallo *gebruikersnaam* en *wachtwoord* referenties voor hello Azure SQL Database. Hallo *gebruikersnaam* moet worden opgegeven als  *user@servername* .   

## <a name="adf-tables"></a>Definieer en maken van tabellen toospecify hoe tooaccess Hallo gegevenssets
Maak tabellen die Hallo structuur, de locatie en de beschikbaarheid van Hallo gegevenssets Hello volgen van procedures op basis van een script opgeeft. JSON-bestanden zijn gebruikte toodefine Hallo tabellen. Zie voor meer informatie over de structuur Hallo van deze bestanden [gegevenssets](../data-factory/data-factory-create-datasets.md).

> [!NOTE]
> Hallo moet worden uitgevoerd `Add-AzureAccount` cmdlet alvorens uit te voeren Hallo [nieuw AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet tooconfirm die Hallo rechts Azure-abonnement is geselecteerd voor Hallo opdrachten uit te voeren. Zie voor documentatie van deze cmdlet [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).
>
>

Hallo JSON gebaseerde definities in Hallo tabellen gebruiken Hallo namen te volgen:

* Hallo **tabelnaam** in Hallo is het lokale SQL server *nyctaxi_data*
* Hallo **containernaam** in hello Azure Blob Storage-account is *containername*  

Drie tabeldefinities nodig zijn voor deze ADF-pijplijn:

1. [On-premises SQL-tabel](#adf-table-onprem-sql)
2. [Blobtabel](#adf-table-blob-store)
3. [SQL Azure-tabel](#adf-table-azure-sql)

> [!NOTE]
> Deze procedures gebruikt u Azure PowerShell toodefine en Hallo ADF activiteiten maken. Maar deze taken kunnen ook worden gerealiseerd met hello Azure-portal. Zie voor meer informatie [gegevenssets maken](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).
>
>

### <a name="adf-table-onprem-sql"></a>On-premises SQL-tabel
de tabeldefinitie Hallo voor Hallo lokale SQL Server is opgegeven in de volgende JSON-bestand Hallo:

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

Hallo kolomnamen zijn niet opgenomen in hier. U kunt subplan selecteren op Hallo kolomnamen door ze hier (voor meer informatie Hallo verplicht [ADF documentatie](../data-factory/data-factory-data-movement-activities.md) onderwerp.

Hallo JSON-definitie van Hallo tabel kopiëren naar een bestand met de naam *onpremtabledef.json* bestand en sla het tooa bekende locatie (hier uitgegaan toobe *C:\temp\onpremtabledef.json*). Hallo-tabel maken in ADF Hello Azure PowerShell-cmdlet te volgen:

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <a name="adf-table-blob-store"></a>Blobtabel
Definitie voor de tabel voor Hallo Hallo uitvoer blob bevindt zich in Hallo volgende (toegewezen Hallo ingenomen gegevens van de lokale tooAzure blob):

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

Hallo JSON-definitie van Hallo tabel kopiëren naar een bestand met de naam *bloboutputtabledef.json* bestand en sla het tooa bekende locatie (hier uitgegaan toobe *C:\temp\bloboutputtabledef.json*). Hallo-tabel maken in ADF Hello Azure PowerShell-cmdlet te volgen:

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <a name="adf-table-azure-sq"></a>SQL Azure-tabel
Definitie voor de tabel Hallo voor Hallo die SQL Azure-uitvoer heeft Hallo volgende (dit schema toegewezen Hallo-gegevens die afkomstig zijn van een blob Hallo):

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

Hallo JSON-definitie van Hallo tabel kopiëren naar een bestand met de naam *AzureSqlTable.json* bestand en sla het tooa bekende locatie (hier uitgegaan toobe *C:\temp\AzureSqlTable.json*). Hallo-tabel maken in ADF Hello Azure PowerShell-cmdlet te volgen:

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <a name="adf-pipeline"></a>Definieer en Hallo pijplijn maken
Hallo-activiteiten die toohello behoren pipeline en Hallo pijplijn maken met de Hallo volgen van procedures op basis van scripts opgeven. Een JSON-bestand is gebruikte toodefine Hallo pipeline-eigenschappen.

* Hallo script wordt ervan uitgegaan dat Hallo **pijplijn naam** is *AMLDSProcessPipeline*.
* Vergeet niet dat we Hallo periodiciteit van Hallo pijplijn toobe uitgevoerd op dagelijks basis en gebruik Hallo standaard uitvoeringstijd voor Hallo taak (12: 00 a.m. UTC) ingesteld.

> [!NOTE]
> Hallo volgende procedures gebruikt u Azure PowerShell toodefine en Hallo ADF pijplijn maken. Maar deze taak kan ook worden bereikt met de Azure-portal. Zie voor meer informatie [maken pijplijn](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).
>
>

Hallo tabeldefinities opgegeven voorheen Hallo pijplijn definitie voor Hallo die ADF is opgegeven, als volgt:

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL tooAzure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server tooblob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data tooSql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

Kopieer deze JSON-definitie van de pijplijn Hallo naar een bestand met de naam *pipelinedef.json* bestand en sla het tooa bekende locatie (hier uitgegaan toobe *C:\temp\pipelinedef.json*). Hallo pijplijn in ADF maken met de Hallo Azure PowerShell-cmdlet te volgen:

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

Controleer of u kunt Hallo pijplijn op Hallo ADF in Hallo klassieke Azure-Portal weergegeven als volgt (wanneer u klikt op Hallo diagram)

![ADF-pipeline](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <a name="adf-pipeline-start"></a>Hallo pijplijn starten
Hallo-pijplijn kan nu worden uitgevoerd met behulp van de volgende opdracht Hallo:

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

Hallo *startdate* en *enddate* parameterwaarden toobe vervangen door de werkelijke Hallo-datums tussen wie u wilt dat Hallo pijplijn toorun nodig.

Zodra het Hallo-pijplijn wordt uitgevoerd, moet u kunnen toosee Hallo gegevens weergegeven in het Hallo-container die zijn geselecteerd voor Hallo blob, één bestand per dag.

Houd er rekening mee dat we geen Hallo functionaliteit van ADF toopipe gegevens stapsgewijs hebt gebruikt. Voor meer informatie over hoe toodo deze en andere mogelijkheden van ADF, zien Hallo [ADF documentatie](https://azure.microsoft.com/services/data-factory/).
