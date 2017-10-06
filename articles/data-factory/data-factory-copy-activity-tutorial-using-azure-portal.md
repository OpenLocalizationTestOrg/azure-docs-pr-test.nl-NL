---
title: 'Zelfstudie: Maak een Azure Data Factory pijplijn toocopy gegevens (Azure-portal) | Microsoft Docs'
description: In deze zelfstudie gebruikt u toocreate met Azure portal een Azure Data Factory-pijplijn met een Kopieeractiviteit toocopy-gegevens van een Azure blob storage tooan Azure SQL database.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d9317652-0170-4fd3-b9b2-37711272162b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fadd840fe9a15cd8831cdb25dccbd10ac42fa161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-portal-toocreate-a-data-factory-pipeline-toocopy-data"></a>Zelfstudie: Gebruik Azure portal toocreate een Data Factory-pijplijn toocopy gegevens 
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

In dit artikel leert u hoe toouse [Azure-portal](https://portal.azure.com) toocreate een gegevensfactory met een pijplijn waarmee gegevens worden gekopieerd van een Azure blob storage tooan Azure SQL database. Als u nieuwe tooAzure Data Factory, lees Hallo [inleiding tooAzure Data Factory](data-factory-introduction.md) artikel voordat u deze zelfstudie uitvoert.   

In deze zelfstudie maakt u een pijplijn met één activiteit erin: kopieeractiviteit. Hallo kopieeractiviteit kopieert gegevens van een gegevensarchief voor ondersteunde gegevens store tooa ondersteunde sink. Zie [Ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met gegevensarchieven die worden ondersteund als bron en als sink. Hallo-activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens tussen verschillende gegevensarchieven op een manier veilig, betrouwbaar en schaalbaar kan worden gekopieerd. Zie voor meer informatie over Hallo Kopieeractiviteit [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md).

Een pijplijn kan meer dan één activiteit hebben. En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit. Zie [Meerdere activiteiten in een pijplijn](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie. 

> [!NOTE] 
> Hallo data pipeline in deze zelfstudie worden gegevens gekopieerd van een bron data store tooa doelgegevensopslagplaats. Voor een zelfstudie over het tootransform van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: een pijplijn tootransform gegevens met Hadoop-cluster bouwen](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Vereisten
Voldoen aan vereisten die worden vermeld in Hallo [vereisten voor de zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artikel voordat u deze zelfstudie.

## <a name="steps"></a>Stappen
Hier volgen Hallo stappen die u als onderdeel van deze zelfstudie uitvoeren:

1. Een Azure-**gegevensfactory** maken. In deze stap maakt u een gegevensfactory met de naam ADFTutorialDataFactory. 
2. Maak **gekoppelde services** in Hallo gegevensfactory. In deze stap maakt u twee gekoppelde services van het type: Azure Storage en Azure SQL Database. 
    
    Hallo AzureStorageLinkedService koppelt u uw Azure storage-account toohello data factory. U hebt gemaakt van een container en gegevens toothis opslagaccount geüpload als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    Azuresqllinkedservice wordt uw Azure SQL database toohello data factory. Hallo-gegevens die worden gekopieerd van de blob-opslag hello wordt opgeslagen in deze database. Als onderdeel van de [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) hebt u een SQL-tabel in deze database gemaakt.   
3. Maken van de invoer en uitvoer **gegevenssets** in Hallo gegevensfactory.  
    
    Hallo gekoppelde Azure storage-service geeft Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op uitvoeringstijd tooconnect tooyour Azure storage-account. En Hallo blob-invoerbron gegevensset geeft Hallo-container en Hallo-map met invoergegevens Hallo.  

    Op deze manier geeft hello Azure SQL Database gekoppeld service Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op de runtime tooconnect tooyour Azure SQL database. En SQL Hallo-tabel uitvoergegevensset geeft Hallo-tabel in Hallo toowhich Hallo databasegegevens van Hallo blob-opslag is gekopieerd.
4. Maak een **pijplijn** in Hallo gegevensfactory. In deze stap maakt u een pijplijn met een kopieeractiviteit.   
    
    Hallo kopieeractiviteit kopieert gegevens van een blob in hello Azure blob storage tooa tabel in hello Azure SQL-database. U kunt een kopieeractiviteit gebruiken in een pijplijn toocopy gegevens van het doel van een ondersteunde bron-tooany ondersteund. Zie het artikel [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met ondersteunde gegevensarchieven. 
5. Hallo-pijplijn bewaken. In deze stap maakt u **monitor** Hallo segmenten van de invoer- en uitvoergegevenssets met behulp van Azure portal. 

## <a name="create-data-factory"></a>Een gegevensfactory maken
> [!IMPORTANT]
> Volledige [vereisten voor Hallo zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) als u dat nog niet hebt gedaan.   

Een gegevensfactory kan één of meer pijplijnen hebben. Een pijplijn kan één of meer activiteiten bevatten. Bijvoorbeeld invoergegevens een Kopieeractiviteit toocopy-gegevens van een doelgegevensopslagplaats tooa bron en het toorun in een HDInsight Hive-activiteit een Hive-script tootransform gegevens tooproduct uitvoer. Laten we beginnen met het maken van de gegevensfactory Hallo in deze stap.

1. Na het aanmelden toohello [Azure-portal](https://portal.azure.com/), klikt u op **nieuw** op Hallo menu links, klikt u op **gegevens en analyse**, en klik op **Data Factory**. 
   
   ![Nieuw -> DataFactory](./media/data-factory-copy-activity-tutorial-using-azure-portal/NewDataFactoryMenu.png)    
2. In Hallo **nieuwe gegevensfactory** blade:
   
   1. Voer **ADFTutorialDataFactory** voor Hallo **naam**. 
      
         ![Blade voor een nieuwe gegevensfactory](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-new-data-factory.png)
      
       Hallo-naam van hello Azure-gegevensfactory moet **globaal unieke**. Als u de volgende fout Hallo ontvangt, wijzigt u Hallo-naam van gegevensfactory hello (naar bijvoorbeeld Uwnaamadftutorialdatafactory) en probeer het opnieuw maken. Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.
      
           Data factory name “ADFTutorialDataFactory” is not available  
      
       ![Naam van gegevensfactory niet beschikbaar](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-not-available.png)
   2. Selecteer uw Azure **abonnement** waarin wordt gezocht toocreate Hallo data factory. 
   3. Voor Hallo **resourcegroep**, doe Hallo stappen te volgen:
      
      - Selecteer **gebruik bestaande**, en selecteer een bestaande resourcegroep in de vervolgkeuzelijst Hallo. 
      - Selecteer **nieuw**, en Voer Hallo-naam van een resourcegroep.   
         
          Sommige van Hallo stappen in deze zelfstudie wordt ervan uitgegaan dat u de naam van de Hallo: **ADFTutorialResourceGroup** voor Hallo resourcegroep. toolearn over resourcegroepen, Zie [toomanage uw Azure-resources met behulp van de resource groepen](../azure-resource-manager/resource-group-overview.md).  
   4. Selecteer Hallo **locatie** voor Hallo data factory. Regio's wordt ondersteund door Hallo Data Factory-service worden weergegeven in de vervolgkeuzelijst Hallo.
   5. Selecteer **pincode toodashboard**.     
   6. Klik op **Create**.
      
      > [!IMPORTANT]
      > toocreate Data Factory-exemplaren, moet u lid zijn van Hallo [Data Factory Inzender](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol op het niveau van de Hallo abonnement/resourcegroep.
      > 
      > Hallo-naam van de gegevensfactory Hallo kan worden geregistreerd als DNS-naam in toekomstige Hallo en daarmee ook voor iedereen zichtbaar.                
      > 
      > 
3. Op Hallo-dashboard ziet er Hallo tegel met de status: **Deploying data factory**. 

    ![tegel met de status 'gegevensfactory implementeren'](media/data-factory-copy-activity-tutorial-using-azure-portal/deploying-data-factory.png)
4. Nadat het maken van Hallo voltooid is, ziet u Hallo **Data Factory** blade zoals in afbeelding Hallo.
   
   ![Startpagina van de gegevensfactory](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-home-page.png)

## <a name="create-linked-services"></a>Gekoppelde services maken
U maken gekoppelde services in een data factory-toolink uw gegevens worden opgeslagen en compute services toohello data factory. In deze zelfstudie gebruikt u niet een willekeurige compute-service, zoals Azure HDInsight of Azure Data Lake Analytics. U gebruikt twee gegevensarchieven van het type Azure Storage (bron) en Azure SQL Database (doel). 

Daarom maakt u twee gekoppelde services met de naam AzureStorageLinkedService en AzureSqlLinkedService van het type: AzureStorage en AzureSqlDatabase.  

Hallo AzureStorageLinkedService koppelt u uw Azure storage-account toohello data factory. Dit opslagaccount wordt Hallo een waarop u container gemaakt en Hallo gegevens geüpload als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

Azuresqllinkedservice wordt uw Azure SQL database toohello data factory. Hallo-gegevens die worden gekopieerd van de blob-opslag hello wordt opgeslagen in deze database. Hallo emp-tabel in deze database wordt gemaakt als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).  

### <a name="create-azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service maken
In deze stap koppelt u uw Azure storage-account tooyour data factory. U geeft Hallo naam en sleutel van uw Azure storage-account in deze sectie.  

1. In Hallo **Data Factory** blade, klikt u op **auteur en implementeren van** tegel.
   
   ![Tegel Ontwerpen en implementeren](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-author-deploy-tile.png) 
2. U ziet Hallo **Data Factory-Editor** zoals weergegeven in Hallo installatiekopie te volgen: 

    ![Data Factory Editor](./media/data-factory-copy-activity-tutorial-using-azure-portal/data-factory-editor.png)
3. In de editor Hallo op **nieuwe gegevensopslag** op Hallo werkbalk en selecteer **Azure storage** uit de vervolgkeuzelijst Hallo. U ziet Hallo JSON-sjabloon voor het maken van een gekoppelde Azure storage-service in het rechterdeelvenster Hallo. 
   
    ![Knop Nieuw gegevensarchief in de editor](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-newdatastore-button.png)    
3. Vervang `<accountname>` en `<accountkey>` met Hallo naam en accountsleutel van uw Azure storage-account. 
   
    ![JSON voor Blob Storage in de editor](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-json.png)    
4. Klik op **implementeren** op Hallo-werkbalk. U ziet Hallo geïmplementeerd **AzureStorageLinkedService** in de boomstructuur Hallo nu weergeven. 
   
    ![Blob Storage implementeren in de editor](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-deploy.png)

    Zie voor meer informatie over de JSON-eigenschappen in de servicedefinitie Hallo gekoppeld [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) artikel.

### <a name="create-a-linked-service-for-hello-azure-sql-database"></a>Een gekoppelde service voor hello Azure SQL Database maken
In deze stap koppelt u uw Azure SQL database tooyour data factory. U opgeven hello Azure SQL-servernaam, databasenaam, gebruikersnaam en wachtwoord in deze sectie. 

1. In Hallo **Data Factory-Editor**, klikt u op **nieuwe gegevensopslag** op Hallo werkbalk en selecteer **Azure SQL Database** uit de vervolgkeuzelijst Hallo. U ziet Hallo JSON-sjabloon voor het maken van hello Azure SQL gekoppelde service in het rechterdeelvenster Hallo.
2. Vervang `<servername>`, `<databasename>`, `<username>@<servername>` en `<password>` door de namen van uw Azure SQL-server, -database en -gebruikersaccount en voer uw wachtwoord in. 
3. Klik op **implementeren** op Hallo werkbalk toocreate en implementeren van Hallo **AzureSqlLinkedService**.
4. Controleer of u **AzureSqlLinkedService** in de structuurweergave Hallo onder **gekoppelde services**.  

    Zie [Azure SQL Database-connector](data-factory-azure-sql-connector.md#linked-service-properties) voor meer informatie over deze JSON-eigenschappen.

## <a name="create-datasets"></a>Gegevenssets maken
In de vorige stap Hallo gemaakt gekoppelde services toolink uw Azure Storage-account en de Azure SQL database tooyour data factory. In deze stap definieert u twee gegevenssets met de naam InputDataset en OutputDataset die vertegenwoordigen de invoer- en uitvoergegevens die zijn opgeslagen in Hallo gegevensarchieven waarnaar wordt verwezen door de AzureStorageLinkedService en AzureSqlLinkedService respectievelijk.

Hallo gekoppelde Azure storage-service geeft Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op uitvoeringstijd tooconnect tooyour Azure storage-account. En Hallo blob-invoerbron gegevensset (InputDataset) geeft Hallo-container en Hallo-map met invoergegevens Hallo.  

Op deze manier geeft hello Azure SQL Database gekoppeld service Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op de runtime tooconnect tooyour Azure SQL database. En Hallo uitvoer gegevensset met SQL-tabel (OututDataset) geeft Hallo tabel in Hallo database toowhich Hallo gegevens uit Hallo blob-opslag worden gekopieerd. 

### <a name="create-input-dataset"></a>Invoergegevensset maken
In deze stap maakt u een gegevensset met de naam InputDataset die tooa blob-bestand (emp.txt) verwijst in de hoofdmap Hallo van een blob-container (adftutorial) in hello Azure Storage dat wordt vertegenwoordigd door Hallo gekoppelde AzureStorageLinkedService-service. Als u niet een waarde voor fileName hello opgeven (of overslaan), zijn gegevens uit alle blobs in de invoermap Hallo gekopieerde toohello bestemming. In deze zelfstudie maakt opgeven u een waarde voor Hallo fileName. 

1. In Hallo **Editor** Hallo Data Factory, klikt u op **... Meer**, klikt u op **nieuwe gegevensset**, en klik op **Azure Blob storage** uit de vervolgkeuzelijst Hallo. 
   
    ![Nieuw gegevenssetmenu](./media/data-factory-copy-activity-tutorial-using-azure-portal/new-dataset-menu.png)
2. Vervang JSON in het rechterdeelvenster Hallo Hello volgende JSON-fragment: 
   
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
          "folderPath": "adftutorial/",
          "fileName": "emp.txt",
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
3. Klik op **implementeren** op Hallo werkbalk toocreate en implementeren van Hallo **InputDataset** gegevensset. Controleer of u Hallo **InputDataset** in de structuurweergave Hallo.

### <a name="create-output-dataset"></a>Uitvoergegevensset maken
Hello Azure SQL Database gekoppeld-service geeft Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op de runtime tooconnect tooyour Azure SQL database. Hallo SQL tabel uitvoergegevensset (OututDataset) in deze stap hebt u Hiermee geeft u Hallo-tabel in Hallo toowhich Hallo databasegegevens van Hallo blob-opslag is gekopieerd.

1. In Hallo **Editor** Hallo Data Factory, klikt u op **... Meer**, klikt u op **nieuwe gegevensset**, en klik op **Azure SQL** uit de vervolgkeuzelijst Hallo. 
2. Vervang JSON in het rechterdeelvenster Hallo Hello volgende JSON-fragment:

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
3. Klik op **implementeren** op Hallo werkbalk toocreate en implementeren van Hallo **OutputDataset** gegevensset. Controleer of u Hallo **OutputDataset** in de structuurweergave Hallo onder **gegevenssets**. 

## <a name="create-pipeline"></a>Pijplijn maken
In deze stap maakt u een pijplijn met een **kopieeractiviteit** die gebruikmaakt van **InputDataset** als invoer en **OutputDataset** als uitvoer.

Uitvoergegevensset is momenteel welke stations Hallo planning. In deze zelfstudie is uitvoergegevensset geconfigureerde tooproduce een segment eens per uur. Hallo pijplijn heeft een begintijd en eindtijd die één dag uit elkaar liggen, wat is 24 uur zijn. Daarom worden 24 segmenten van uitvoergegevensset geproduceerd door Hallo pijplijn. 

1. In Hallo **Editor** Hallo Data Factory, klikt u op **... Meer** en vervolgens op **Nieuwe pijplijn**. U kunt ook u kunt met de rechtermuisknop op **pijplijnen** in Hallo structuurweergave en klik op **nieuwe pijplijn**.
2. Vervang JSON in het rechterdeelvenster Hallo Hello volgende JSON-fragment: 

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
    - Zowel de begin- als einddatum en -tijd moeten de [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601) hebben. Bijvoorbeeld: 2016-10-14T16:32:41Z. Hallo **end** tijd is optioneel, maar er worden gebruikt in deze zelfstudie. Als u geen waarde voor Hallo opgeeft **end** eigenschap, wordt berekend als '**start + 48 uur**'. toorun hello pijplijn voor onbepaalde tijd, geef **9999-09-09** als waarde voor Hallo Hallo **end** eigenschap.
     
    In de Hallo voorgaande voorbeeld, zijn er 24 gegevenssegmenten omdat elke gegevenssegment per uur is gemaakt.

    Zie het artikel [Pijplijnen maken](data-factory-create-pipelines.md) voor beschrijvingen van JSON-eigenschappen in de definitie van een pijplijn. Zie [Gegevensverplaatsingsactiviteiten](data-factory-data-movement-activities.md) voor beschrijvingen van JSON-eigenschappen in de definitie van een kopieeractiviteit. Zie het [artikel over Azure Blob-connectoren](data-factory-azure-blob-connector.md) voor beschrijvingen van JSON-eigenschappen die worden ondersteund door BlobSource. Zie het [artikel over Azure SQL Database-connectoren](data-factory-azure-sql-connector.md) voor beschrijvingen van JSON-eigenschappen die worden ondersteund door SqlSink.
3. Klik op **implementeren** op Hallo werkbalk toocreate en implementeren van Hallo **ADFTutorialPipeline**. Controleer of u Hallo pijplijn in de structuurweergave Hallo. 
4. Sluit nu Hallo **Editor** blade door te klikken op **X**. Klik op **X** opnieuw toosee hello **Data Factory** startpagina van Hallo **ADFTutorialDataFactory**.

**Gefeliciteerd!** U hebt een Azure-gegevensfactory gemaakt met een pipeline toocopy-gegevens van een Azure blob storage tooan Azure SQL database. 


## <a name="monitor-pipeline"></a>De pijplijn bewaken
In deze stap gebruikt u hello Azure portal toomonitor wat in een Azure data factory gebeurt er.    

### <a name="monitor-pipeline-using-monitor--manage-app"></a>De pijplijn bewaken met de app Bewaking en beheer
Hallo volgende stappen ziet u hoe toomonitor pijplijnen in uw data factory met behulp van de Monitor & beheren toepassing hello: 

1. Klik op **Monitor & beheren** tegel op Hallo-startpagina van uw gegevensfactory.
   
    ![De tegel Bewaking en beheer](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-manage-tile.png) 
2. De toepassing **Bewaking en beheer** wordt op een afzonderlijk tabblad weergegeven. 

    > [!NOTE]
    > Als u ziet dat Hallo webbrowser is vastgelopen bij 'Autoriseren...', voert u een van de volgende Hallo: Schakel Hallo **blokkeren van cookies van derden en sitegegevens** selectievakje (of) maakt een uitzondering voor **login.microsoftonline.com**, en probeer het vervolgens opnieuw tooopen Hallo app.

    ![De app Bewaking en beheer](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-and-manage-app.png)
3. Wijziging Hallo **begintijd** en **eindtijd** tooinclude start (2017-05-11) en eindtijden (2017-05-12) van de pijplijn en op **toepassen**.     
3. Zie van Hallo **activiteitsvensters** die zijn gekoppeld aan elk uur tussen het begin van de pipeline- en tijden in de lijst in het middelste deelvenster Hallo Hallo. 
4. toosee details over een activiteitvenster, selecteer activiteitenvenster in Hallo Hallo **Activiteitsvensters** lijst. 
    ![Details van activiteitsvenster](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)

    In activiteit venster Explorer op de juiste hello, ziet u dat Hallo segmenten van de huidige UTC-tijd toohello (8:12 PM) worden verwerkt (in groen). Hallo 8-9 uur, 9-10 uur, 10 11 PM, 23: 00 uur - 12: 00 uur segmenten nog niet zijn verwerkt.

    Hallo **pogingen** sectie in het rechter deelvenster bevat informatie over Hallo activiteit die wordt uitgevoerd voor het gegevenssegment Hallo Hallo. Als er een fout opgetreden is, biedt het meer informatie over Hallo-fout. Bijvoorbeeld, als Hallo invoer map of container niet bestaat en Hallo segment verwerking mislukt, ziet u een foutmelding die Hallo-container of map bestaat niet.

    ![Pogingen tot uitvoering van activiteit](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-run-attempts.png) 
4. Start **SQL Server Management Studio**, verbinding toohello Azure SQL Database en controleer of dat Hallo rijen worden ingevoegd in toohello **emp** tabel in Hallo-database.
    
    ![SQL-queryresultaten](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)

Zie [Azure Data Factory-pijplijnen bewaken en beheren met de app voor bewaking en beheer](data-factory-monitor-manage-app.md) voor meer informatie over het gebruik van deze toepassing.

### <a name="monitor-pipeline-using-diagram-view"></a>De pijplijn bewaken met Diagramweergave
U kunt ook gegevenspijplijnen bewaken met behulp van de diagramweergave Hallo.  

1. In Hallo **Data Factory** blade, klikt u op **Diagram**.
   
    ![Blade Gegevensfactory - tegel Diagram](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datafactoryblade-diagramtile.png)
2. U ziet Hallo diagram vergelijkbare toohello installatiekopie te volgen: 
   
    ![Diagramweergave](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-diagram-blade.png)  
5. Dubbelklik in de diagramweergave Hallo **InputDataset** toosee segmenten voor Hallo dataset.  
   
    ![Gegevenssets waarvoor InputDataset is geselecteerd](./media/data-factory-copy-activity-tutorial-using-azure-portal/DataSetsWithInputDatasetFromBlobSelected.png)   
5. Klik op **Zie voor meer informatie** toosee alle Hallo gegevenssegmenten koppelen. U ziet 24 uurlijkse segmenten tussen de begin- en eindtijd van de pijplijn. 
   
    ![Alle invoergegevenssegmenten](./media/data-factory-copy-activity-tutorial-using-azure-portal/all-input-slices.png)  
   
    Ziet u dat alle gegevenssegmenten toohello huidige UTC-tijd Hallo **gereed** omdat Hallo **emp.txt** bestand alle Hallo tijd bestaat in de blob-container Hallo: **adftutorial\input**. Hallo segmenten voor toekomstige tijden Hallo nog niet in de status ready heeft. Bevestig dat er geen segmenten in Hallo weergegeven **recent mislukte segmenten** sectie Hallo onder aan.
6. Sluiten Hallo blades totdat u Zie Hallo diagram weergave (of) schuiven links toosee Hallo diagram weergeven. Dubbelklik vervolgens op **OutputDataset**. 
8. Klik op **Zie voor meer informatie** koppeling op Hallo **tabel** blade voor **OutputDataset** toosee alle segmenten Hallo.

    ![blade gegevenssegmenten](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslices-blade.png) 
9. U ziet dat alle segmenten van de huidige UTC-tijd toohello Hallo verplaatsen van **in afwachting van uitvoering** status = > **Bezig** ==> **gereed** status. Hallo segmenten van afgelopen hello (voor de huidige tijd) worden verwerkt vanuit de meest recente toooldest standaard. Bijvoorbeeld, als Hallo huidige tijd 8:12 uur UTC is, Hallo segment voor 19: 00 - 8 uur is verwerkt tevoren Hallo 6 PM - 7 uur segment. Hallo 20: 00 - 9 uur segment is verwerkt na Hallo Hallo tijdsinterval standaard na 21: 00.  
10. Klik op een gegevenssegment uit de lijst Hallo en ziet u Hallo **gegevenssegment** blade. Een hoeveelheid gegevens die is gekoppeld aan een activiteitsvenster wordt een segment genoemd. Een segment kan één bestand of meerdere bestanden zijn.  
    
     ![blade Gegevenssegment](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslice-blade.png)
    
     Als Hallo segment zich niet in Hallo **gereed** staat, kunt u zien Hallo upstreamsegmenten die niet gereed zijn en blokkeren het huidige segment uitgevoerd Hallo Hallo **upstreamsegmenten die niet gereed** lijst.
11. In Hallo **GEGEVENSSEGMENT** blade ziet u alle activiteiten wordt uitgevoerd in de lijst Hallo Hallo onderaan. Klik op een **activiteit die wordt uitgevoerd** toosee hello **details uitvoering van activiteit** blade. 
    
    ![Details uitvoering van activiteit](./media/data-factory-copy-activity-tutorial-using-azure-portal/ActivityRunDetails.png)

    In deze blade ziet u hoe lang Hallo kopieerbewerking duurde, welke doorvoer is, het aantal bytes aan gegevens zijn gelezen en geschreven, voert begintijd, eindtijd enzovoort worden uitgevoerd.  
12. Klik op **X** tooclose alle Hallo blades totdat u teruggaan toohello startblade voor Hallo **ADFTutorialDataFactory**.
13. (optioneel) Klik op Hallo **gegevenssets** tegel of **pijplijnen** tegel tooget Hallo blades die u hebt al gezien Hallo voorgaande stappen hebt uitgevoerd. 
14. Start **SQL Server Management Studio**, verbinding toohello Azure SQL Database en controleer of dat Hallo rijen worden ingevoegd in toohello **emp** tabel in Hallo-database.
    
    ![SQL-queryresultaten](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)


## <a name="summary"></a>Samenvatting
In deze zelfstudie maakt u een Azure data factory toocopy gegevens uit een Azure-blobopslag tooan Azure SQL database gemaakt. U hebt gebruikt hello Azure portal toocreate hello gegevensfactory, gekoppelde services, gegevenssets en een pijplijn. Hier volgen Hallo hoofdstappen die u in deze zelfstudie hebt uitgevoerd:  

1. U hebt een Azure-**gegevensfactory** gemaakt.
2. U hebt **gekoppelde services** gemaakt:
   1. Een **Azure Storage** service toolink uw Azure Storage-account dat invoergegevens bevat gekoppeld.     
   2. Een **Azure SQL** gekoppelde service toolink uw Azure SQL-database die uitvoergegevens Hallo bevat. 
3. U hebt **gegevenssets** gemaakt waarin de invoer- en uitvoergegevens van pijplijnen worden beschreven.
4. U hebt een **pijplijn** gemaakt met een **kopieeractiviteit** met **BlobSource** als bron en **SqlSink** als sink.  

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u voor een kopieerbewerking een Azure Blob-opslag gebruikt als brongegevensarchief en een Azure SQL-database als doelgegevensarchief. Hallo bevat volgende tabel een lijst met gegevensarchieven als bronnen en bestemmingen wordt ondersteund door Hallo kopieeractiviteit: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn over hoe gegevens uit een data toocopy opslaan, klikt u op Hallo-koppeling voor de gegevensopslag Hallo in Hallo tabel.
