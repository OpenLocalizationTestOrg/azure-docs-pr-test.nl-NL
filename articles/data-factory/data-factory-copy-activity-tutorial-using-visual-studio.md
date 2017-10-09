---
title: 'Zelfstudie: een pijplijn maken met de kopieeractiviteit in Visual Studio | Microsoft Docs'
description: In deze zelfstudie maakt u een Azure Data Factory-pijplijn met een kopieeractiviteit. Hiervoor gebruikt u Visual Studio.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: d99d8875807bab41f5122ab95a09f83f82923529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a>Zelfstudie: een pijplijn maken met de kopieeractiviteit in Visual Studio
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

In dit artikel leert u hoe toouse Hallo toocreate Microsoft Visual Studio een gegevensfactory met een pijplijn waarmee gegevens worden gekopieerd van een Azure blob storage tooan Azure SQL database. Als u nieuwe tooAzure Data Factory, lees Hallo [inleiding tooAzure Data Factory](data-factory-introduction.md) artikel voordat u deze zelfstudie uitvoert.   

In deze zelfstudie maakt u een pijplijn met één activiteit erin: kopieeractiviteit. Hallo kopieeractiviteit kopieert gegevens van een gegevensarchief voor ondersteunde gegevens store tooa ondersteunde sink. Zie [Ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met gegevensarchieven die worden ondersteund als bron en als sink. Hallo-activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens tussen verschillende gegevensarchieven op een manier veilig, betrouwbaar en schaalbaar kan worden gekopieerd. Zie voor meer informatie over Hallo Kopieeractiviteit [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md).

Een pijplijn kan meer dan één activiteit hebben. En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit. Zie [Meerdere activiteiten in een pijplijn](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.

> [!NOTE] 
> Hallo data pipeline in deze zelfstudie worden gegevens gekopieerd van een bron data store tooa doelgegevensopslagplaats. Voor een zelfstudie over het tootransform van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: een pijplijn tootransform gegevens met Hadoop-cluster bouwen](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Vereisten
1. Lees [overzicht van de zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artikel en volledige Hallo **vereiste** stappen.       
2. toocreate Data Factory-exemplaren, moet u lid zijn van Hallo [Data Factory Inzender](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol op het niveau van de Hallo abonnement/resourcegroep.
3. Hallo volgende op uw computer geïnstalleerd, moet u hebben: 
   * Visual Studio 2013 of Visual Studio 2015
   * Download de Azure SDK voor Visual Studio 2013 of Visual Studio 2015. Navigeer te[Azure-downloadpagina](https://azure.microsoft.com/downloads/) en klik op **VS 2013** of **VS 2015** in Hallo **.NET** sectie.
   * Download de nieuwste Azure Data Factory-invoegtoepassing Hallo voor Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) of [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). U kunt ook Hallo invoegtoepassing Hallo volgende stappen uit als volgt bijwerken: op het menu Hallo **extra** -> **uitbreidingen en Updates** -> **Online**  ->  **Visual Studio-galerie** -> **Microsoft Azure Data Factory-hulpprogramma's voor Visual Studio** -> **Update**.

## <a name="steps"></a>Stappen
Hier volgen Hallo stappen die u als onderdeel van deze zelfstudie uitvoeren:

1. Maak **gekoppelde services** in Hallo gegevensfactory. In deze stap maakt u twee gekoppelde services van het type: Azure Storage en Azure SQL Database. 
    
    Hallo AzureStorageLinkedService koppelt u uw Azure storage-account toohello data factory. U hebt gemaakt van een container en gegevens toothis opslagaccount geüpload als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    Azuresqllinkedservice wordt uw Azure SQL database toohello data factory. Hallo-gegevens die worden gekopieerd van de blob-opslag hello wordt opgeslagen in deze database. Als onderdeel van de [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) hebt u een SQL-tabel in deze database gemaakt.     
2. Maken van de invoer en uitvoer **gegevenssets** in Hallo gegevensfactory.  
    
    Hallo gekoppelde Azure storage-service geeft Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op uitvoeringstijd tooconnect tooyour Azure storage-account. En Hallo blob-invoerbron gegevensset geeft Hallo-container en Hallo-map met invoergegevens Hallo.  

    Op deze manier geeft hello Azure SQL Database gekoppeld service Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op de runtime tooconnect tooyour Azure SQL database. En SQL Hallo-tabel uitvoergegevensset geeft Hallo-tabel in Hallo toowhich Hallo databasegegevens van Hallo blob-opslag is gekopieerd.
3. Maak een **pijplijn** in Hallo gegevensfactory. In deze stap maakt u een pijplijn met een kopieeractiviteit.   
    
    Hallo kopieeractiviteit kopieert gegevens van een blob in hello Azure blob storage tooa tabel in hello Azure SQL-database. U kunt een kopieeractiviteit gebruiken in een pijplijn toocopy gegevens van het doel van een ondersteunde bron-tooany ondersteund. Zie het artikel [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met ondersteunde gegevensarchieven. 
4. Maak een Azure-**gegevensfactory** tijdens het implementeren van de Data Factory-entiteiten (gekoppelde services, gegevenssets/tabellen en pijplijnen). 

## <a name="create-visual-studio-project"></a>Een Visual Studio-project maken
1. Open **Visual Studio 2015**. Klik op **bestand**, wijst u te**nieuw**, en klik op **Project**. U ziet Hallo **nieuw Project** in het dialoogvenster.  
2. In Hallo **nieuw Project** dialoogvenster, selecteer Hallo **DataFactory** sjabloon en klikt u op **Empty Data Factory Project**.  
   
    ![Het dialoogvenster New Project](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. Hallo-naam van het Hallo-project, de locatie voor de oplossing Hallo en naam van oplossing Hallo opgeven en klik vervolgens op **OK**.
   
    ![Solution Explorer](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a>Gekoppelde services maken
U maken gekoppelde services in een data factory-toolink uw gegevens worden opgeslagen en compute services toohello data factory. In deze zelfstudie gebruikt u niet een willekeurige compute-service, zoals Azure HDInsight of Azure Data Lake Analytics. U gebruikt twee gegevensarchieven van het type Azure Storage (bron) en Azure SQL Database (doel). 

Daarom maakt u twee gekoppelde services van het type: Azure Storage en AzureSqlDatabase.  

Hello Azure Storage gekoppelde service uw Azure storage-account toohello data factory. Dit opslagaccount wordt Hallo een waarop u container gemaakt en Hallo gegevens geüpload als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

Azure SQL gekoppelde service uw Azure SQL database toohello data factory. Hallo-gegevens die worden gekopieerd van de blob-opslag hello wordt opgeslagen in deze database. Hallo emp-tabel in deze database wordt gemaakt als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Gekoppelde services worden gegevensarchieven of compute-services tooan Azure-gegevensfactory. Zie [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor alle bronnen en put wordt ondersteund door Hallo Kopieeractiviteit Hallo. Zie [gekoppelde services berekenen](data-factory-compute-linked-services.md) voor Hallo overzicht van de compute-services die door Data Factory worden ondersteund. In deze zelfstudie gebruikt u geen compute-service. 

### <a name="create-hello-azure-storage-linked-service"></a>Hallo gekoppelde Azure Storage-service maken
1. In **Solution Explorer**, met de rechtermuisknop op **gekoppelde Services**, wijst u te**toevoegen**, en klik op **Nieuw Item**.      
2. In Hallo **Add New Item** dialoogvenster, **Azure Storage Linked Service** in Hallo lijst en klik op **toevoegen**. 
   
    ![Nieuwe gekoppelde service](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. Vervang `<accountname>` en `<accountkey>`* met Hallo-naam van uw Azure storage-account en de bijbehorende sleutel. 
   
    ![Een gekoppelde Azure Storage-service](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. Hallo opslaan **AzureStorageLinkedService1.json** bestand.

    Zie voor meer informatie over de JSON-eigenschappen in de servicedefinitie Hallo gekoppeld [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) artikel.

### <a name="create-hello-azure-sql-linked-service"></a>Hello Azure SQL gekoppelde service maken
1. Met de rechtermuisknop op **gekoppelde Services** knooppunt in Hallo **Solution Explorer** opnieuw in en wijst te**toevoegen**, en klik op **Nieuw Item**. 
2. Selecteer deze keer **Azure SQL Linked Service** en klik op **Add**. 
3. In Hallo **AzureSqlLinkedService1.json bestand**, Vervang `<servername>`, `<databasename>`, `<username@servername>`, en `<password>` met namen van uw Azure SQL-server, database-gebruikersaccount en wachtwoord.    
4. Hallo opslaan **AzureSqlLinkedService1.json** bestand. 
    
    Zie [Azure SQL Database-connector](data-factory-azure-sql-connector.md#linked-service-properties) voor meer informatie over deze JSON-eigenschappen.


## <a name="create-datasets"></a>Gegevenssets maken
In de vorige stap Hallo gemaakt gekoppelde services toolink uw Azure Storage-account en de Azure SQL database tooyour data factory. In deze stap definieert u twee gegevenssets met de naam InputDataset en OutputDataset die vertegenwoordigen de invoer- en uitvoergegevens die zijn opgeslagen in Hallo gegevensarchieven waarnaar wordt verwezen door de AzureStorageLinkedService1 en AzureSqlLinkedService1 respectievelijk.

Hallo gekoppelde Azure storage-service geeft Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op uitvoeringstijd tooconnect tooyour Azure storage-account. En Hallo blob-invoerbron gegevensset (InputDataset) geeft Hallo-container en Hallo-map met invoergegevens Hallo.  

Op deze manier geeft hello Azure SQL Database gekoppeld service Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op de runtime tooconnect tooyour Azure SQL database. En Hallo uitvoer gegevensset met SQL-tabel (OututDataset) geeft Hallo tabel in Hallo database toowhich Hallo gegevens uit Hallo blob-opslag worden gekopieerd. 

### <a name="create-input-dataset"></a>Invoergegevensset maken
In deze stap maakt u een gegevensset met de naam InputDataset die tooa blob-bestand (emp.txt) verwijst in de hoofdmap Hallo van een blob-container (adftutorial) in hello Azure Storage dat wordt vertegenwoordigd door Hallo gekoppelde AzureStorageLinkedService1-service. Als u niet een waarde voor fileName hello opgeven (of overslaan), zijn gegevens uit alle blobs in de invoermap Hallo gekopieerde toohello bestemming. In deze zelfstudie maakt opgeven u een waarde voor Hallo fileName. 

U kunt hier Hallo term 'tabellen' gebruiken in plaats van 'gegevenssets'. Een tabel is een rechthoekige gegevensset en Hallo enige type gegevensset dat momenteel wordt ondersteund. 

1. Met de rechtermuisknop op **tabellen** in Hallo **Solution Explorer**, wijst u te**toevoegen**, en klik op **Nieuw Item**.
2. In Hallo **Add New Item** dialoogvenster, **Azure Blob**, en klik op **toevoegen**.   
3. Hallo JSON-tekst vervangen door de volgende tekst hello en Hallo opslaan **AzureBlobLocation1.json** bestand. 

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
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
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

### <a name="create-output-dataset"></a>Uitvoergegevensset maken
In deze stap maakt u een uitvoergegevensset met de naam **OutputDataset**. Deze gegevensset verwijst tooa SQL-tabel in hello Azure SQL-database dat wordt vertegenwoordigd door **AzureSqlLinkedService1**. 

1. Met de rechtermuisknop op **tabellen** in Hallo **Solution Explorer** opnieuw in en wijst te**toevoegen**, en klik op **Nieuw Item**.
2. In Hallo **Add New Item** dialoogvenster, **Azure SQL**, en klik op **toevoegen**. 
3. Hallo JSON-tekst vervangen door Hallo volgende JSON en sla Hallo **AzureSqlTableLocation1.json** bestand.

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
       "linkedServiceName": "AzureSqlLinkedService1",
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

## <a name="create-pipeline"></a>Pijplijn maken
In deze stap maakt u een pijplijn met een **kopieeractiviteit** die gebruikmaakt van **InputDataset** als invoer en **OutputDataset** als uitvoer.

Uitvoergegevensset is momenteel welke stations Hallo planning. In deze zelfstudie is uitvoergegevensset geconfigureerde tooproduce een segment eens per uur. Hallo pijplijn heeft een begintijd en eindtijd die één dag uit elkaar liggen, wat is 24 uur zijn. Daarom worden 24 segmenten van uitvoergegevensset geproduceerd door Hallo pijplijn. 

1. Met de rechtermuisknop op **pijplijnen** in Hallo **Solution Explorer**, wijst u te**toevoegen**, en klik op **Nieuw Item**.  
2. Selecteer **Copy Data Pipeline** in Hallo **Add New Item** dialoogvenster en klik op **toevoegen**. 
3. Hallo JSON vervangen door Hallo volgende JSON en sla Hallo **CopyActivity1.json** bestand.

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
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - In Hallo gedeelte activiteiten is er slechts één activiteit waarvan **type** te is ingesteld,**kopie**. Zie voor meer informatie over de kopieeractiviteit hello [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md). In Data Factory-oplossingen kunt u ook [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) gebruiken.
    - Invoer voor Hallo-activiteit is ingesteld, te**InputDataset** en de uitvoer voor Hallo activiteit te is ingesteld**OutputDataset**. 
    - In Hallo **typeProperties** sectie **BlobSource** is opgegeven als Hallo brontype en **SqlSink** is opgegeven als Hallo sink-type. Zie voor een volledige lijst van gegevensarchieven die worden ondersteund door Hallo kopieeractiviteit als bronnen en put [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn hoe toouse een specifieke ondersteunde gegevens opslaan als een bron/sink, klikt u op Hallo-koppeling in Hallo tabel.  
     
    Vervang de waarde Hallo Hallo **start** eigenschap met de huidige dag Hallo en **end** waarde met de volgende dag Hallo. U kunt alleen Hallo datumgedeelte opgeven en Hallo tijdgedeelte van Hallo datum / tijd overslaan. Bijvoorbeeld '2016-02-03', dat te gelijk ' 2016-02-03T00:00:00Z '
     
    Zowel de begin- als einddatum en -tijd moeten de [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601) hebben. Bijvoorbeeld: 2016-10-14T16:32:41Z. Hallo **end** tijd is optioneel, maar er worden gebruikt in deze zelfstudie. 
     
    Als u geen waarde voor Hallo opgeeft **end** eigenschap, wordt berekend als '**start + 48 uur**'. toorun hello pijplijn voor onbepaalde tijd, geef **9999-09-09** als waarde voor Hallo Hallo **end** eigenschap.
     
    In de Hallo voorgaande voorbeeld, zijn er 24 gegevenssegmenten omdat elke gegevenssegment per uur is gemaakt.

    Zie het artikel [Pijplijnen maken](data-factory-create-pipelines.md) voor beschrijvingen van JSON-eigenschappen in de definitie van een pijplijn. Zie [Gegevensverplaatsingsactiviteiten](data-factory-data-movement-activities.md) voor beschrijvingen van JSON-eigenschappen in de definitie van een kopieeractiviteit. Zie het [artikel over Azure Blob-connectoren](data-factory-azure-blob-connector.md) voor beschrijvingen van JSON-eigenschappen die worden ondersteund door BlobSource. Zie het [artikel over Azure SQL Database-connectoren](data-factory-azure-sql-connector.md) voor beschrijvingen van JSON-eigenschappen die worden ondersteund door SqlSink.

## <a name="publishdeploy-data-factory-entities"></a>Data Factory-entiteiten publiceren/implementeren
In deze stap publiceert u Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) die u eerder hebt gemaakt. U kunt ook opgeven Hallo-naam van Hallo nieuwe data factory toobe gemaakt toohold deze entiteiten.  

1. Met de rechtermuisknop op het project in Solution Explorer Hallo en klik op **publiceren**. 
2. Als u ziet **tooyour Microsoft-account aanmelden** in het dialoogvenster Geef uw referenties voor het Hallo-account met Azure-abonnement en klikt u op **aanmelden**.
3. U ziet Hallo in het dialoogvenster te volgen:
   
   ![Het dialoogvenster Publish](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. In de pagina voor Hallo Configure data factory Hallo volgende stappen: 
   
   1. Selecteer **Create New Data Factory**.
   2. Voer **VSTutorialFactory** in als **naam**.  
      
      > [!IMPORTANT]
      > Hallo-naam van hello Azure-gegevensfactory moet wereldwijd uniek zijn. Als er een over Hallo-naam van gegevensfactory foutbericht bij het publiceren, moet u Hallo-naam van gegevensfactory hello (bijvoorbeeld yournameVSTutorialFactory) en publiceert u opnieuw wijzigen. Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.        
      > 
      > 
   3. Selecteer uw Azure-abonnement voor Hallo **abonnement** veld.
      
      > [!IMPORTANT]
      > Als u een abonnement niet ziet, zorg ervoor dat u aangemeld met een account dat een beheerder of co-beheerder van het Hallo-abonnement.  
      > 
      > 
   4. Selecteer Hallo **resourcegroep** voor Hallo data factory toobe gemaakt. 
   5. Selecteer Hallo **regio** voor Hallo data factory. Regio's wordt ondersteund door Hallo Data Factory-service worden weergegeven in de vervolgkeuzelijst Hallo.
   6. Klik op **volgende** tooswitch toohello **Publish Items** pagina.
      
       ![Pagina Data Factory configureren](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. In Hallo **Publish Items** pagina, zorg ervoor dat alle Data Factory-entiteiten zijn geselecteerd en klik op Hallo **volgende** tooswitch toohello **samenvatting** pagina.
   
   ![Pagina Items publiceren](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. Controleer Hallo samenvatting en klik op **volgende** toostart Hallo implementatie proces en bekijkt hello **Implementatiestatus**.
   
   ![Pagina Samenvatting publiceren](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. In Hallo **Implementatiestatus** pagina ziet u Hallo status van implementatieproces Hallo. Klik op Voltooien nadat het Hallo-implementatie is voltooid.
 
   ![Pagina Deployment Status](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

Houd er rekening mee Hallo volgende punten: 

* Als u Hallo-foutmelding: 'dit abonnement is niet geregistreerd toouse namespace Microsoft.DataFactory', voer een van de volgende Hallo en probeer opnieuw te publiceren: 
  
  * Voer in Azure PowerShell Hallo opdracht tooregister Hallo Data Factory-provider te volgen. 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    Die Hallo Data Factory-provider is geregistreerd, kunt u na de opdracht tooconfirm Hallo uitvoeren. 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Aanmelding via het Azure-abonnement in Hallo Hallo [Azure-portal](https://portal.azure.com) en navigeer tooa Data Factory-blade of maak een gegevensfactory in hello Azure-portal. Deze actie automatisch Hallo provider voor u geregistreerd.
* Hallo-naam van de gegevensfactory Hallo kan worden geregistreerd als DNS-naam in toekomstige Hallo en daarmee ook voor iedereen zichtbaar.

> [!IMPORTANT]
> toocreate Data Factory-exemplaren, moet u toobe beheerder/co-beheerder van hello Azure-abonnement

## <a name="monitor-pipeline"></a>De pijplijn bewaken
Navigeer toohello startpagina voor uw data factory:

1. Meld u bij te[Azure-portal](https://portal.azure.com).
2. Klik op **meer services** op Hallo van menu aan de linkerkant en klik op **gegevensfactory**.

    ![Door gegevensfactory’s bladeren](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. Naam begint te typen Hallo van uw gegevensfactory.

    ![Naam van gegevensfactory](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. Klik op uw gegevensfactory in Hallo resultaten lijst toosee Hallo de startpagina van uw gegevensfactory.

    ![Startpagina van de gegevensfactory](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. Volg de instructies uit [gegevenssets en pijplijn bewaken](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor Hallo pijplijn en gegevenssets u in deze zelfstudie hebt gemaakt. Visual Studio biedt momenteel geen ondersteuning voor het bewaken van Data Factory-pijplijnen. 

## <a name="summary"></a>Samenvatting
In deze zelfstudie maakt u een Azure data factory toocopy gegevens uit een Azure-blobopslag tooan Azure SQL database gemaakt. U hebt Visual Studio toocreate hello gegevensfactory, gekoppelde services, gegevenssets en een pijplijn gebruikt. Hier volgen Hallo hoofdstappen die u in deze zelfstudie hebt uitgevoerd:  

1. U hebt een Azure-**gegevensfactory** gemaakt.
2. U hebt **gekoppelde services** gemaakt:
   1. Een **Azure Storage** service toolink uw Azure Storage-account dat invoergegevens bevat gekoppeld.     
   2. Een **Azure SQL** gekoppelde service toolink uw Azure SQL-database die uitvoergegevens Hallo bevat. 
3. U hebt **gegevenssets** gemaakt waarin de invoer- en uitvoergegevens van pijplijnen worden beschreven.
4. U hebt een **pijplijn** gemaakt met een **kopieeractiviteit** met **BlobSource** als bron en **SqlSink** als sink. 

hoe de gegevens van een HDInsight Hive-activiteit tootransform met behulp van Azure HDInsight-cluster toouse zien toosee [ zelfstudie: bouwen van uw eerste pijplijn tootransform gegevens met Hadoop-cluster](data-factory-build-your-first-pipeline.md).

U kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit. Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md) voor gedetailleerde informatie. 

## <a name="view-all-data-factories-in-server-explorer"></a>Alle gegevensfactory’s weergeven in Server Explorer
Deze sectie beschrijft hoe toouse Hallo van Server Explorer in Visual Studio tooview alle Hallo data Factory in uw Azure-abonnement en maak een Visual Studio-project op basis van een bestaande gegevensfactory. 

1. In **Visual Studio**, klikt u op **weergave** op Hallo van menu en klik op **Server Explorer**.
2. Vouw in Server Explorer-venster Hallo **Azure** en vouw **Data Factory**. Als u ziet **tooVisual Studio aanmelden**, Voer Hallo **account** die zijn gekoppeld aan uw Azure-abonnement en klik op **doorgaan**. Voer het **wachtwoord** in en klik op **Sign in**. Visual Studio haalt tooget informatie over alle Azure data factory's in uw abonnement. Hallo-status van deze bewerking in Hallo weergegeven **Data Factory Task List** venster.

    ![Server Explorer](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a>Een Visual Studio-project maken voor een bestaande gegevensfactory

- Met de rechtermuisknop op een gegevensfactory in Server Explorer en selecteer **tooNew Export Data Factory Project** toocreate een Visual Studio-project op basis van een bestaande gegevensfactory.

    ![Export data factory tooa VS-project](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

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


## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u voor een kopieerbewerking een Azure Blob-opslag gebruikt als brongegevensarchief en een Azure SQL-database als doelgegevensarchief. Hallo bevat volgende tabel een lijst met gegevensarchieven als bronnen en bestemmingen wordt ondersteund door Hallo kopieeractiviteit: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn over hoe gegevens uit een data toocopy opslaan, klikt u op Hallo-koppeling voor de gegevensopslag Hallo in Hallo tabel.
