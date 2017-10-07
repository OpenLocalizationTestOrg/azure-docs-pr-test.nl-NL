---
title: 'Zelfstudie: Een pijplijn toomove gegevens maken met behulp van Azure PowerShell | Microsoft Docs'
description: In deze zelfstudie maakt u een Azure Data Factory-pijplijn met een kopieeractiviteit. Hiervoor gebruikt u Azure PowerShell.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 21406d7dfaa0c555b2538fbb52839d761c140fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a>Zelfstudie: Een Data Factory-pijplijn maken die gegevens verplaatst met Azure PowerShell
> [!div class="op_single_selector"]
> * [Overzicht en vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [De wizard Kopiëren](data-factory-copy-data-wizard-tutorial.md)
> * [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager-sjabloon](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)
>
>

In dit artikel leert u hoe toouse PowerShell toocreate een gegevensfactory met een pijplijn waarmee gegevens worden gekopieerd van een Azure blob storage tooan Azure SQL database. Als u nieuwe tooAzure Data Factory, lees Hallo [inleiding tooAzure Data Factory](data-factory-introduction.md) artikel voordat u deze zelfstudie uitvoert.   

In deze zelfstudie maakt u een pijplijn met één activiteit erin: kopieeractiviteit. Hallo kopieeractiviteit kopieert gegevens van een gegevensarchief voor ondersteunde gegevens store tooa ondersteunde sink. Zie [Ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met gegevensarchieven die worden ondersteund als bron en als sink. Hallo-activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens tussen verschillende gegevensarchieven op een manier veilig, betrouwbaar en schaalbaar kan worden gekopieerd. Zie voor meer informatie over Hallo Kopieeractiviteit [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md).

Een pijplijn kan meer dan één activiteit hebben. En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit. Zie [Meerdere activiteiten in een pijplijn](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.

> [!NOTE]
> In dit artikel omvat niet alle Hallo Data Factory-cmdlets. Zie [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) (Naslaginformatie voor Data Factory-cmdlets) voor uitgebreide documentatie over deze cmdlets.
> 
> Hallo data pipeline in deze zelfstudie worden gegevens gekopieerd van een bron data store tooa doelgegevensopslagplaats. Voor een zelfstudie over het tootransform van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: een pijplijn tootransform gegevens met Hadoop-cluster bouwen](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Vereisten
- Voldoen aan vereisten die worden vermeld in Hallo [vereisten voor de zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artikel.
- Installeer **Azure PowerShell**. Volg de instructies in Hallo [hoe tooinstall en configureren van Azure PowerShell](../powershell-install-configure.md).

## <a name="steps"></a>Stappen
Hier volgen Hallo stappen die u als onderdeel van deze zelfstudie uitvoeren:

1. Een Azure-**gegevensfactory** maken. In deze stap maakt u een gegevensfactory met de naam ADFTutorialDataFactoryPSH. 
2. Maak **gekoppelde services** in Hallo gegevensfactory. In deze stap maakt u twee gekoppelde services van het type: Azure Storage en Azure SQL Database. 
    
    Hallo AzureStorageLinkedService koppelt u uw Azure storage-account toohello data factory. U hebt gemaakt van een container en gegevens toothis opslagaccount geüpload als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    Azuresqllinkedservice wordt uw Azure SQL database toohello data factory. Hallo-gegevens die worden gekopieerd van de blob-opslag hello wordt opgeslagen in deze database. Als onderdeel van de [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) hebt u een SQL-tabel in deze database gemaakt.   
3. Maken van de invoer en uitvoer **gegevenssets** in Hallo gegevensfactory.  
    
    Hallo gekoppelde Azure storage-service geeft Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op uitvoeringstijd tooconnect tooyour Azure storage-account. En Hallo blob-invoerbron gegevensset geeft Hallo-container en Hallo-map met invoergegevens Hallo.  

    Op deze manier geeft hello Azure SQL Database gekoppeld service Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op de runtime tooconnect tooyour Azure SQL database. En SQL Hallo-tabel uitvoergegevensset geeft Hallo-tabel in Hallo toowhich Hallo databasegegevens van Hallo blob-opslag is gekopieerd.
4. Maak een **pijplijn** in Hallo gegevensfactory. In deze stap maakt u een pijplijn met een kopieeractiviteit.   
    
    Hallo kopieeractiviteit kopieert gegevens van een blob in hello Azure blob storage tooa tabel in hello Azure SQL-database. U kunt een kopieeractiviteit gebruiken in een pijplijn toocopy gegevens van het doel van een ondersteunde bron-tooany ondersteund. Zie het artikel [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met ondersteunde gegevensarchieven. 
5. Hallo-pijplijn bewaken. In deze stap maakt u **monitor** Hallo segmenten van de invoer- en uitvoergegevenssets met behulp van PowerShell.

## <a name="create-a-data-factory"></a>Een data factory maken
> [!IMPORTANT]
> Volledige [vereisten voor Hallo zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) als u dat nog niet hebt gedaan.   

Een gegevensfactory kan één of meer pijplijnen hebben. Een pijplijn kan één of meer activiteiten bevatten. Bijvoorbeeld invoergegevens een Kopieeractiviteit toocopy-gegevens van een doelgegevensopslagplaats tooa bron en het toorun in een HDInsight Hive-activiteit een Hive-script tootransform gegevens tooproduct uitvoer. Laten we beginnen met het maken van de gegevensfactory Hallo in deze stap.

1. Start **PowerShell**. Houd Azure PowerShell open tot Hallo einde van deze zelfstudie. Als u sluiten en opnieuw opent, moet u toorun Hallo opdrachten opnieuw.

    Hallo volgende opdracht uitvoeren en voert u Hallo-gebruikersnaam en wachtwoord toosign in toohello Azure-portal te gebruiken:

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    Voer Hallo opdracht tooview na alle Hallo abonnementen voor dit account:

    ```PowerShell
    Get-AzureRmSubscription
    ```

    Hallo opdracht tooselect Hallo abonnement dat u wilt dat toowork met volgende worden uitgevoerd. Vervang  **&lt;NameOfAzureSubscription** &gt; met Hallo-naam van uw Azure-abonnement:

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. Maak een Azure-resourcegroep met de naam **ADFTutorialResourceGroup** door het uitvoeren van de volgende opdracht Hallo:

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    Sommige van Hallo stappen in deze zelfstudie wordt ervan uitgegaan dat u het Hallo-resourcegroep met de naam **ADFTutorialResourceGroup**. Als u een andere resourcegroep gebruikt, moet u toouse deze in plaats van ADFTutorialResourceGroup in deze zelfstudie.
3. Voer Hallo **New-AzureRmDataFactory** cmdlet toocreate een gegevensfactory met de naam **ADFTutorialDataFactoryPSH**:  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    Deze naam is mogelijk al in gebruik. Zorg daarom Hallo-naam van de gegevensfactory Hallo unieke door toe te voegen voor- of achtervoegsel (bijvoorbeeld: ADFTutorialDataFactoryPSH05152017) en Voer Hallo opdracht opnieuw uit.  

Houd er rekening mee Hallo volgende punten:

* Hallo-naam van hello Azure-gegevensfactory moet wereldwijd uniek zijn. Als u de volgende fout Hallo ontvangt, moet u Hallo-naam (bijvoorbeeld in Uwnaamadfstutorialdatafactorypsh) wijzigen. Gebruik deze naam in plaats van ADFTutorialFactoryPSH tijdens het uitvoeren van de stappen in de zelfstudie. Raadpleeg [Data Factory - Naming Rules](data-factory-naming-rules.md) (Data Factory - Naamgevingsregels) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* toocreate Data Factory-exemplaren, moet u een bijdrager of de beheerder van hello Azure-abonnement.
* Hallo-naam van de gegevensfactory Hallo mogelijk geregistreerd als DNS-naam in toekomstige hello, en daarom ook openbaar zichtbaar.
* U ontvangt mogelijk Hallo volgende fout: "**dit abonnement is niet geregistreerd toouse namespace Microsoft.DataFactory.**' Voer een van de volgende Hallo en probeer opnieuw te publiceren:

  * Voer in Azure PowerShell Hallo opdracht tooregister Hallo Data Factory-provider te volgen:

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    Voer Hallo opdracht tooconfirm te volgen die Hallo Data Factory-provider wordt geregistreerd:

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Meld u aan met behulp van Azure-abonnement toohello Hallo [Azure-portal](https://portal.azure.com). Ga tooa Data Factory-blade of maak een gegevensfactory in hello Azure-portal. Deze actie automatisch Hallo provider voor u geregistreerd.

## <a name="create-linked-services"></a>Gekoppelde services maken
U maken gekoppelde services in een data factory-toolink uw gegevens worden opgeslagen en compute services toohello data factory. In deze zelfstudie gebruikt u niet een willekeurige compute-service, zoals Azure HDInsight of Azure Data Lake Analytics. U gebruikt twee gegevensarchieven van het type Azure Storage (bron) en Azure SQL Database (doel). 

Daarom maakt u twee gekoppelde services met de naam AzureStorageLinkedService en AzureSqlLinkedService van het type: AzureStorage en AzureSqlDatabase.  

Hallo AzureStorageLinkedService koppelt u uw Azure storage-account toohello data factory. Dit opslagaccount wordt Hallo een waarop u container gemaakt en Hallo gegevens geüpload als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

Azuresqllinkedservice wordt uw Azure SQL database toohello data factory. Hallo-gegevens die worden gekopieerd van de blob-opslag hello wordt opgeslagen in deze database. Hallo emp-tabel in deze database wordt gemaakt als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a>Een gekoppelde service maken voor een Azure-opslagaccount
In deze stap koppelt u uw Azure storage-account tooyour data factory.

1. Maak een JSON-bestand met de naam **AzureStorageLinkedService.json** in **C:\ADFGetStartedPSH** map met inhoud na Hallo: (maken Hallo map ADFGetStartedPSH als deze nog niet bestaat).

    > [!IMPORTANT]
    > Vervang &lt;accountname&gt; en &lt;accountkey&gt; met de naam en sleutel van uw Azure storage-account voordat het Hallo-bestand op te slaan. 

    ```json
    {
        "name": "AzureStorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
     }
    ``` 
2. In **Azure PowerShell**, switch toohello **ADFGetStartedPSH** map.
4. Voer Hallo **New-AzureRmDataFactoryLinkedService** cmdlet toocreate Hallo gekoppelde service: **AzureStorageLinkedService**. Deze cmdlet en andere Data Factory-cmdlets die u gebruikt in deze zelfstudie moeten u toopass waarden voor Hallo **ResourceGroupName** en **DataFactoryName** parameters. U kunt ook doorgeven Hallo DataFactory-object geretourneerd door Hallo New-AzureRmDataFactory cmdlet zonder te hoeven typen ResourceGroupName en DataFactoryName telkens wanneer die u een cmdlet uitvoert. 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    Hier volgt voorbeelduitvoer Hallo:

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    Andere manier voor het maken van deze gekoppelde service is toospecify Resourcegroepnaam en de naam gegevensfactory in plaats van Hallo DataFactory-object opgeven.  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a>Een gekoppelde service maken voor een Azure SQL-database
In deze stap koppelt u uw Azure SQL database tooyour data factory.

1. Maak een JSON-bestand met de naam AzureSqlLinkedService.json in de map C:\ADFGetStartedPSH Hello volgende inhoud:

    > [!IMPORTANT]
    > Vervang &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt; en &lt;password&gt; door de namen van uw Azure SQL-server, database, gebruiker en wachtwoord.
    
    ```json
    {
        "name": "AzureSqlLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<server>.database.windows.net,1433;Database=<databasename>;User ID=<user>@<server>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
     }
    ```
2. Voer Hallo opdracht toocreate na een gekoppelde service:

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    Hier volgt voorbeelduitvoer Hallo:

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   Bevestig dat **tooAzure-services toegang toestaan** instelling is ingeschakeld voor uw SQL database-server. tooverify en weer in, Hallo volgende stappen:

    1. Meld u bij toohello [Azure-portal](https://portal.azure.com)
    2. Klik op **meer services >** op Hallo linkerkant en klik op **SQL-servers** in Hallo **DATABASES** categorie.
    3. Selecteer uw server in de lijst Hallo van SQL-servers.
    4. Klik op Hallo SQL server-blade **firewall-instellingen weergeven** koppeling.
    5. In Hallo **Firewall-instellingen** blade, klikt u op **ON** voor **tooAzure-services toegang toestaan**.
    6. Klik op **opslaan** op Hallo-werkbalk. 

## <a name="create-datasets"></a>Gegevenssets maken
In de vorige stap Hallo gemaakt gekoppelde services toolink uw Azure Storage-account en de Azure SQL database tooyour data factory. In deze stap definieert u twee gegevenssets met de naam InputDataset en OutputDataset die vertegenwoordigen de invoer- en uitvoergegevens die zijn opgeslagen in Hallo gegevensarchieven waarnaar wordt verwezen door de AzureStorageLinkedService en AzureSqlLinkedService respectievelijk.

Hallo gekoppelde Azure storage-service geeft Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op uitvoeringstijd tooconnect tooyour Azure storage-account. En Hallo blob-invoerbron gegevensset (InputDataset) geeft Hallo-container en Hallo-map met invoergegevens Hallo.  

Op deze manier geeft hello Azure SQL Database gekoppeld service Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op de runtime tooconnect tooyour Azure SQL database. En Hallo uitvoer gegevensset met SQL-tabel (OututDataset) geeft Hallo tabel in Hallo database toowhich Hallo gegevens uit Hallo blob-opslag worden gekopieerd. 

### <a name="create-an-input-dataset"></a>Een invoergegevensset maken
In deze stap maakt u een gegevensset met de naam InputDataset die tooa blob-bestand (emp.txt) verwijst in de hoofdmap Hallo van een blob-container (adftutorial) in hello Azure Storage dat wordt vertegenwoordigd door Hallo gekoppelde AzureStorageLinkedService-service. Als u niet een waarde voor fileName hello opgeven (of overslaan), zijn gegevens uit alle blobs in de invoermap Hallo gekopieerde toohello bestemming. In deze zelfstudie maakt opgeven u een waarde voor Hallo fileName.  

1. Maak een JSON-bestand met de naam **InputDataset.json** in Hallo **C:\ADFGetStartedPSH** map Hello volgende inhoud:

    ```json
    {
        "name": "InputDataset",
        "properties": {
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
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "emp.txt",
                "folderPath": "adftutorial/",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```

    Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:

    | Eigenschap | Beschrijving |
    |:--- |:--- |
    | type | Hallo type wordt ingesteld te**AzureBlob** omdat de gegevens zich in een Azure blob storage. |
    | linkedServiceName | Toohello verwijst **AzureStorageLinkedService** die u eerder hebt gemaakt. |
    | folderPath | Hiermee geeft u op Hallo blob **container** en Hallo **map** die invoer blobs bevat. In deze zelfstudie adftutorial is Hallo blob-container en map Hallo-hoofdmap is. | 
    | fileName | Deze eigenschap is optioneel. Als u deze eigenschap niet opgeeft, worden alle bestanden uit folderPath Hallo opgenomen. In deze zelfstudie **emp.txt** hello bestandsnaam, zodat alleen dat bestand wordt opgehaald voor de verwerking wordt opgegeven. |
    | format -> type |Hallo-bestand voor invoer is in de indeling van de tekst hello, zodat we gebruiken **TextFormat**. |
    | columnDelimiter | Hallo-kolommen in het invoerbestand Hallo worden gescheiden door **kommateken (`,`)**. |
    | frequency/interval | Hallo frequentie te is ingesteld**uur** en interval is ingesteld, te**1**, wat betekent dat Hallo invoer segmenten zijn beschikbaar **per uur**. Met andere woorden, Hallo Data Factory-service zoekt invoergegevens elk uur in de hoofdmap Hallo van blob-container (**adftutorial**) u hebt opgegeven. Hallo-gegevens binnen Hallo pijplijn begin- en tijden, niet voor of na deze tijden zoekt.  |
    | external | Deze eigenschap is ingesteld, te**true** als Hallo gegevens niet worden gegenereerd door deze pijplijn. Hallo invoergegevens in deze zelfstudie wordt Hallo emp.txt bestand, die niet worden gegenereerd door deze pipeline, zodat we de tootrue van deze eigenschap wordt ingesteld. |

    Zie het [artikel over Azure Blob-connectoren](data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over deze JSON-eigenschappen.
2. Voer Hallo opdracht toocreate Hallo Data Factory-gegevensset te volgen.

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    Hier volgt voorbeelduitvoer Hallo:

    ```
    DatasetName       : InputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureBlobDataset
    Policy            : Microsoft.Azure.Management.DataFactories.Common.Models.Policy
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

### <a name="create-an-output-dataset"></a>Een uitvoergegevensset maken
In dit deel van stap hello, maakt u een uitvoergegevensset met de naam **OutputDataset**. Deze gegevensset verwijst tooa SQL-tabel in hello Azure SQL-database dat wordt vertegenwoordigd door **AzureSqlLinkedService**. 

1. Maak een JSON-bestand met de naam **OutputDataset.json** in Hallo **C:\ADFGetStartedPSH** map Hello volgende inhoud:

    ```json
    {
        "name": "OutputDataset",
        "properties": {
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
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

    Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:

    | Eigenschap | Beschrijving |
    |:--- |:--- |
    | type | Hallo type wordt ingesteld te**AzureSqlTable** omdat gegevens gekopieerde tooa tabel in een Azure SQL database. |
    | linkedServiceName | Toohello verwijst **AzureSqlLinkedService** die u eerder hebt gemaakt. |
    | tableName | Opgegeven Hallo **tabel** toowhich Hallo gegevens worden gekopieerd. | 
    | frequency/interval | Hallo frequentie is ingesteld te**uur** en interval is **1**, wat betekent dat Hallo uitvoer segmenten worden geproduceerd **per uur** tussen Hallo pijplijn begin- en tijden niet voor of na deze tijden.  |

    Er zijn drie kolommen – **ID**, **FirstName**, en **LastName** – in Hallo emp-tabel in Hallo-database. -ID is een identiteitskolom, dus u alleen toospecify hoeft **FirstName** en **LastName** hier.

    Zie het [artikel over Azure SQL-connectoren](data-factory-azure-sql-connector.md#dataset-properties) voor meer informatie over deze JSON-eigenschappen.
2. Voer Hallo opdracht toocreate Hallo data factory-gegevensset te volgen.

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    Hier volgt voorbeelduitvoer Hallo:

    ```
    DatasetName       : OutputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureSqlTableDataset
    Policy            :
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

## <a name="create-a-pipeline"></a>Een pijplijn maken
In deze stap maakt u een pijplijn met een **kopieeractiviteit** die gebruikmaakt van **InputDataset** als invoer en **OutputDataset** als uitvoer.

Uitvoergegevensset is momenteel welke stations Hallo planning. In deze zelfstudie is uitvoergegevensset geconfigureerde tooproduce een segment eens per uur. Hallo pijplijn heeft een begintijd en eindtijd die één dag uit elkaar liggen, wat is 24 uur zijn. Daarom worden 24 segmenten van uitvoergegevensset geproduceerd door Hallo pijplijn. 


1. Maak een JSON-bestand met de naam **ADFTutorialPipeline.json** in Hallo **C:\ADFGetStartedPSH** map Hello volgende inhoud:

    ```json   
    {
      "name": "ADFTutorialPipeline",
      "properties": {
        "description": "Copy data from a blob tooAzure SQL table",
        "activities": [
          {
            "name": "CopyFromBlobToSQL",
            "type": "Copy",
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
            "typeProperties": {
              "source": {
                "type": "BlobSource"
              },
              "sink": {
                "type": "SqlSink",
                "writeBatchSize": 10000,
                "writeBatchTimeout": "60:00:00"
              }
            },
            "Policy": {
              "concurrency": 1,
              "executionPriorityOrder": "NewestFirst",
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2017-05-11T00:00:00Z",
        "end": "2017-05-12T00:00:00Z"
      }
    } 
    ```
    Houd er rekening mee Hallo volgende punten:
   
    - In Hallo gedeelte activiteiten is er slechts één activiteit waarvan **type** te is ingesteld,**kopie**. Zie voor meer informatie over de kopieeractiviteit hello [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md). In Data Factory-oplossingen kunt u ook [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) gebruiken.
    - Invoer voor Hallo-activiteit is ingesteld, te**InputDataset** en de uitvoer voor Hallo activiteit te is ingesteld**OutputDataset**. 
    - In Hallo **typeProperties** sectie **BlobSource** is opgegeven als Hallo brontype en **SqlSink** is opgegeven als Hallo sink-type. Zie voor een volledige lijst van gegevensarchieven die worden ondersteund door Hallo kopieeractiviteit als bronnen en put [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn hoe toouse een specifieke ondersteunde gegevens opslaan als een bron/sink, klikt u op Hallo-koppeling in Hallo tabel.  
     
    Vervang de waarde Hallo Hallo **start** eigenschap met de huidige dag Hallo en **end** waarde met de volgende dag Hallo. U kunt alleen Hallo datumgedeelte opgeven en Hallo tijdgedeelte van Hallo datum / tijd overslaan. Bijvoorbeeld '2016-02-03', dat te gelijk ' 2016-02-03T00:00:00Z '
     
    Zowel de begin- als einddatum en -tijd moeten de [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601) hebben. Bijvoorbeeld: 2016-10-14T16:32:41Z. Hallo **end** tijd is optioneel, maar er worden gebruikt in deze zelfstudie. 
     
    Als u geen waarde voor Hallo opgeeft **end** eigenschap, wordt berekend als '**start + 48 uur**'. toorun hello pijplijn voor onbepaalde tijd, geef **9999-09-09** als waarde voor Hallo Hallo **end** eigenschap.
     
    In de Hallo voorgaande voorbeeld, zijn er 24 gegevenssegmenten omdat elke gegevenssegment per uur is gemaakt.

    Zie het artikel [Pijplijnen maken](data-factory-create-pipelines.md) voor beschrijvingen van JSON-eigenschappen in de definitie van een pijplijn. Zie [Gegevensverplaatsingsactiviteiten](data-factory-data-movement-activities.md) voor beschrijvingen van JSON-eigenschappen in de definitie van een kopieeractiviteit. Zie het [artikel over Azure Blob-connectoren](data-factory-azure-blob-connector.md) voor beschrijvingen van JSON-eigenschappen die worden ondersteund door BlobSource. Zie het [artikel over Azure SQL Database-connectoren](data-factory-azure-sql-connector.md) voor beschrijvingen van JSON-eigenschappen die worden ondersteund door SqlSink.
2. Voer Hallo opdracht toocreate Hallo data factory-tabel te volgen.

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    Hier volgt voorbeelduitvoer Hallo: 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

**Gefeliciteerd!** U hebt een Azure-gegevensfactory gemaakt met een pipeline toocopy-gegevens van een Azure blob storage tooan Azure SQL database. 

## <a name="monitor-hello-pipeline"></a>Hallo-pijplijn bewaken
In deze stap gebruikt u Azure PowerShell toomonitor wat er gebeurt in een Azure data factory.

1. Vervang &lt;DataFactoryName&gt; met de naam van uw gegevensfactory en het uitvoeren van Hallo **Get-AzureRmDataFactory**, en Hallo uitvoer tooa variabele $df toewijzen.

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    Bijvoorbeeld:
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    Voer vervolgens de inhoud afdrukken Hallo $df toosee Hallo volgende uitvoer: 
    
    ```
    PS C:\ADFGetStartedPSH> $df
    
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DataFactoryId     : 6f194b34-03b3-49ab-8f03-9f8a7b9d3e30
    ResourceGroupName : ADFTutorialResourceGroup
    Location          : West US
    Tags              : {}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DataFactoryProperties
    ProvisioningState : Succeeded
    ```
2. Uitvoeren **Get-AzureRmDataFactorySlice** tooget details over alle segmenten van Hallo **OutputDataset**, namelijk uitvoergegevensset Hallo van Hallo pijplijn.  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   Deze instelling moet overeenkomen met de Hallo **Start** waarde in de JSON van de Hallo-pijplijn. U ziet 24 segmenten; één voor elk uur vanaf 12: 00 A.M. van Hallo huidige dag too12 BEN Hallo volgende dag.

   Hier volgen drie voorbeeld segmenten van Hallo uitvoer: 

    ``` 
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 11:00:00 PM
    End               : 5/12/2017 12:00:00 AM
    RetryCount        : 0
    State             : Ready
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 9:00:00 PM
    End               : 5/11/2017 10:00:00 PM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0   

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 8:00:00 PM
    End               : 5/11/2017 9:00:00 PM
    RetryCount        : 0
    State             : Waiting
    SubState          : ConcurrencyLimit
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. Voer **Get-AzureRmDataFactoryRun** tooget Hallo details van de activiteit wordt uitgevoerd voor een **specifieke** segment. Hallo datum / tijd-waarde van de uitvoer Hallo van Hallo vorige opdracht toospecify Hallo waarde voor Hallo StartDateTime parameter kopiëren. 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   Hier volgt voorbeelduitvoer Hallo: 

    ```
    Id                  : c0ddbd75-d0c7-4816-a775-704bbd7c7eab_636301332000000000_636301368000000000_OutputDataset
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH0516
    DatasetName         : OutputDataset
    ProcessingStartTime : 5/16/2017 8:00:33 PM
    ProcessingEndTime   : 5/16/2017 8:01:36 PM
    PercentComplete     : 100
    DataSliceStart      : 5/11/2017 9:00:00 PM
    DataSliceEnd        : 5/11/2017 10:00:00 PM
    Status              : Succeeded
    Timestamp           : 5/16/2017 8:00:33 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy  
    ```

Zie [Naslaginformatie voor Data Factory-cmdlets](/powershell/module/azurerm.datafactories) voor uitgebreide documentatie over Data Factory-cmdlets.

## <a name="summary"></a>Samenvatting
In deze zelfstudie maakt u een Azure data factory toocopy gegevens uit een Azure-blobopslag tooan Azure SQL database gemaakt. U hebt PowerShell toocreate hello gegevensfactory, gekoppelde services, gegevenssets en een pijplijn gebruikt. Hier volgen Hallo hoofdstappen die u in deze zelfstudie hebt uitgevoerd:  

1. U hebt een Azure-**gegevensfactory** gemaakt.
2. U hebt **gekoppelde services** gemaakt:

   a. Een **Azure Storage** gekoppelde service toolink uw Azure storage-account dat invoergegevens bevat.     
   b. Een **Azure SQL** gekoppelde service toolink uw SQL-database die uitvoergegevens Hallo bevat.
3. U hebt **gegevenssets** gemaakt waarin de invoer- en uitvoergegevens van pijplijnen worden beschreven.
4. Gemaakt een **pijplijn** met **Kopieeractiviteit**, met **BlobSource** als Hallo bron en **SqlSink** als Hallo sink.

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u voor een kopieerbewerking een Azure Blob-opslag gebruikt als brongegevensarchief en een Azure SQL-database als doelgegevensarchief. Hallo bevat volgende tabel een lijst met gegevensarchieven als bronnen en bestemmingen wordt ondersteund door Hallo kopieeractiviteit: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn over hoe gegevens uit een data toocopy opslaan, klikt u op Hallo-koppeling voor de gegevensopslag Hallo in Hallo tabel. 

