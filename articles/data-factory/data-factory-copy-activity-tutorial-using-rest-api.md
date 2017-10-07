---
title: 'Zelfstudie: Gebruik REST-API toocreate een Azure Data Factory-pijplijn | Microsoft Docs'
description: In deze zelfstudie gebruikt u REST-API toocreate een Azure Data Factory-pijplijn met een Kopieeractiviteit toocopy-gegevens van een Azure blob storage een Azure SQL database.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1704cdf8-30ad-49bc-a71c-4057e26e7350
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: aa6c9b035101c4ff9acff90117ca6e3e7067f418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-rest-api-toocreate-an-azure-data-factory-pipeline-toocopy-data"></a>Zelfstudie: Gebruik REST-API toocreate toocopy gegevens in een Azure Data Factory-pipeline 
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

In dit artikel leert u hoe toouse REST-API toocreate een gegevensfactory met een pijplijn waarmee gegevens worden gekopieerd van een Azure blob storage tooan Azure SQL database. Als u nieuwe tooAzure Data Factory, lees Hallo [inleiding tooAzure Data Factory](data-factory-introduction.md) artikel voordat u deze zelfstudie uitvoert.   

In deze zelfstudie maakt u een pijplijn met één activiteit erin: kopieeractiviteit. Hallo kopieeractiviteit kopieert gegevens van een gegevensarchief voor ondersteunde gegevens store tooa ondersteunde sink. Zie [Ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met gegevensarchieven die worden ondersteund als bron en als sink. Hallo-activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens tussen verschillende gegevensarchieven op een manier veilig, betrouwbaar en schaalbaar kan worden gekopieerd. Zie voor meer informatie over Hallo Kopieeractiviteit [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md).

Een pijplijn kan meer dan één activiteit hebben. En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit. Zie [Meerdere activiteiten in een pijplijn](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.

> [!NOTE]
> In dit artikel omvat niet alle Hallo REST-API van Data Factory. Zie [Naslaginformatie voor Data Factory-REST API](/rest/api/datafactory/) voor uitgebreide documentatie over Data Factory-cmdlets.
>  
> Hallo data pipeline in deze zelfstudie worden gegevens gekopieerd van een bron data store tooa doelgegevensopslagplaats. Voor een zelfstudie over het tootransform van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: een pijplijn tootransform gegevens met Hadoop-cluster bouwen](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Vereisten
* Doorloop [overzicht van de zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) en volledige Hallo **vereiste** stappen.
* Installeer [Curl](https://curl.haxx.se/dlwiz/) op uw computer. U gebruikt Hallo Curl hulpprogramma met REST opdrachten toocreate een gegevensfactory. 
* Volg de instructies in [dit artikel](../azure-resource-manager/resource-group-create-service-principal-portal.md) voor het volgende: 
  1. Maak een webtoepassing met de naam **ADFCopyTutorialApp** in Azure Active Directory.
  2. Haal de **client-id** en **geheime sleutel** op. 
  3. Haal de **tenant-id** op. 
  4. Hallo toewijzen **ADFCopyTutorialApp** toepassing toohello **Data Factory Inzender** rol.  
* Installeer [Azure PowerShell](/powershell/azure/overview).  
* Start **PowerShell** en Hallo volgende stappen. Houd Azure PowerShell open tot Hallo einde van deze zelfstudie. Als u sluiten en opnieuw opent, moet u toorun Hallo opdrachten opnieuw.
  
  1. Voer Hallo volgende opdracht en Voer Hallo-gebruikersnaam en wachtwoord toosign in toohello Azure-portal te gebruiken:
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. Voer Hallo opdracht tooview na alle Hallo abonnementen voor dit account:

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. Hallo opdracht tooselect Hallo abonnement dat u wilt dat toowork met volgende worden uitgevoerd. Vervang  **&lt;NameOfAzureSubscription** &gt; met Hallo-naam van uw Azure-abonnement. 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. Maak een Azure-resourcegroep met de naam **ADFTutorialResourceGroup** door het uitvoeren van de volgende opdracht in PowerShell Hallo Hallo:  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      Als de resourcegroep Hallo al bestaat, die u opgeeft of tooupdate deze (Y) of als (N). 
     
      Sommige van Hallo stappen in deze zelfstudie wordt ervan uitgegaan dat u het Hallo-resourcegroep met de naam ADFTutorialResourceGroup. Als u een andere resourcegroep gebruikt, moet u toouse Hallo-naam van de resourcegroep in plaats van ADFTutorialResourceGroup in deze zelfstudie.

## <a name="create-json-definitions"></a>JSON-definities maken
Maken de volgende JSON-bestanden in Hallo map waar curl.exe zich bevindt. 

### <a name="datafactoryjson"></a>datafactory.json
> [!IMPORTANT]
> Naam moet globaal uniek zijn, zodat u tooprefix-/ achtervoegseltekenreeks ADFCopyTutorialDF toomake kunt deze een unieke naam op. 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a>azurestoragelinkedservice.json
> [!IMPORTANT]
> Vervang **accountname** en **accountkey** door de naam en sleutel van uw Azure Storage-account. toolearn hoe tooget uw opslag toegang krijgen tot sleutel, Zie [toegangssleutels voor opslag weergeven, kopiëren en opnieuw genereren](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).

```JSON
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

Zie [Gekoppelde Azure Storage-service](data-factory-azure-blob-connector.md#azure-storage-linked-service) voor meer informatie over de JSON-eigenschappen.

### <a name="azuersqllinkedservicejson"></a>azuersqllinkedservice.json
> [!IMPORTANT]
> Vervang **servername**, **databasename**, **gebruikersnaam**, en **wachtwoord** met de naam van uw Azure SQL-server van SQL-database, de naam van gebruiker account en wachtwoord voor Hallo-account.  
> 
>

```JSON
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

Zie [Gekoppelde Azure SQL-service](data-factory-azure-sql-connector.md#linked-service-properties) voor meer informatie over de JSON-eigenschappen.

### <a name="inputdatasetjson"></a>inputdataset.json

```JSON
{
  "name": "AzureBlobInput",
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

### <a name="outputdatasetjson"></a>outputdataset.json

```JSON
{
  "name": "AzureSqlOutput",
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

### <a name="pipelinejson"></a>pipeline.json

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data tooAzure SQL database",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
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
- Invoer voor Hallo-activiteit is ingesteld, te**AzureBlobInput** en de uitvoer voor Hallo activiteit te is ingesteld**AzureSqlOutput**. 
- In Hallo **typeProperties** sectie **BlobSource** is opgegeven als Hallo brontype en **SqlSink** is opgegeven als Hallo sink-type. Zie voor een volledige lijst van gegevensarchieven die worden ondersteund door Hallo kopieeractiviteit als bronnen en put [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn hoe toouse een specifieke ondersteunde gegevens opslaan als een bron/sink, klikt u op Hallo-koppeling in Hallo tabel.  
 
Vervang de waarde Hallo Hallo **start** eigenschap met de huidige dag Hallo en **end** waarde met de volgende dag Hallo. U kunt alleen Hallo datumgedeelte opgeven en Hallo tijdgedeelte van Hallo datum / tijd overslaan. Bijvoorbeeld '2017-02-03', dat te gelijk ' 2017-02-03T00:00:00Z '
 
Zowel de begin- als einddatum en -tijd moeten de [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601) hebben. Bijvoorbeeld: 2016-10-14T16:32:41Z. Hallo **end** tijd is optioneel, maar er worden gebruikt in deze zelfstudie. 
 
Als u geen waarde voor Hallo opgeeft **end** eigenschap, wordt berekend als '**start + 48 uur**'. toorun hello pijplijn voor onbepaalde tijd, geef **9999-09-09** als waarde voor Hallo Hallo **end** eigenschap.
 
In de Hallo voorgaande voorbeeld, zijn er 24 gegevenssegmenten omdat elke gegevenssegment per uur is gemaakt.

Zie het artikel [Pijplijnen maken](data-factory-create-pipelines.md) voor beschrijvingen van JSON-eigenschappen in de definitie van een pijplijn. Zie [Gegevensverplaatsingsactiviteiten](data-factory-data-movement-activities.md) voor beschrijvingen van JSON-eigenschappen in de definitie van een kopieeractiviteit. Zie het [artikel over Azure Blob-connectoren](data-factory-azure-blob-connector.md) voor beschrijvingen van JSON-eigenschappen die worden ondersteund door BlobSource. Zie het [artikel over Azure SQL Database-connectoren](data-factory-azure-sql-connector.md) voor beschrijvingen van JSON-eigenschappen die worden ondersteund door SqlSink.

## <a name="set-global-variables"></a>Globale variabelen instellen
Uitvoeren in Azure PowerShell Hallo opdrachten na waarbij Hallo waarden vervangt door uw eigen te volgen:

> [!IMPORTANT]
> Zie de sectie [Vereisten](#prerequisites) voor instructies over het verkrijgen van de client-id, het clientgeheim, de tenant-id en de abonnements-id.   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

Voer Hallo volgende opdracht na het bijwerken van de naam van de gegevensfactory Hallo Hallo die u gebruikt: 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a>Verifiëren met AAD
Voer Hallo opdracht tooauthenticate met Azure Active Directory (AAD) te volgen: 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a>Een gegevensfactory maken
In deze stap maakt u een Azure-gegevensfactory met de naam **ADFCopyTutorialDF**. Een gegevensfactory kan één of meer pijplijnen hebben. Een pijplijn kan één of meer activiteiten bevatten. Bijvoorbeeld een Kopieeractiviteit toocopy gegevens uit een bron tooa bestemming gegevens opslaan. Het toorun in een HDInsight Hive-activiteit een Hive-script tootransform invoer gegevens tooproduct uitvoergegevens. Voer Hallo opdrachten toocreate hello gegevensfactory te volgen: 

1. Hallo opdracht toovariable met de naam toewijzen **cmd**. 
   
    > [!IMPORTANT]
    > Bevestig dat Hallo de naam van gegevensfactory Hallo u hier opgeeft (ADFCopyTutorialDF) komt overeen met de naam opgegeven in Hallo Hallo **datafactory.json**. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. Hallo-opdracht uitvoeren met behulp van **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Hallo resultaten weergeven. Als Hallo gegevensfactory is gemaakt, ziet u Hallo JSON voor Hallo data factory in Hallo **resultaten**; anders wordt een foutbericht wordt weergegeven.  
   
    ```
    Write-Host $results
    ```

Houd er rekening mee Hallo volgende punten:

* Hallo-naam van hello Azure Data Factory moet wereldwijd uniek zijn. Als er een fout in resultaten Hallo: **Data factory-naam 'ADFCopyTutorialDF' is niet beschikbaar**, Hallo volgende stappen:  
  
  1. Hallo naam wijzigen (bijvoorbeeld yournameADFCopyTutorialDF) in Hallo **datafactory.json** bestand.
  2. In de eerste opdracht Hallo waar Hallo **$cmd** variabele een waarde is toegewezen, ADFCopyTutorialDF vervangen door de nieuwe naam Hallo en het Hallo-opdracht uitvoeren. 
  3. Hallo volgende twee opdrachten tooinvoke Hallo REST-API toocreate Hallo data factory en printers Hallo resultaten van Hallo bewerking uitgevoerd. 
     
     Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.
* toocreate Data Factory-exemplaren, moet u bijdrager/beheerder zijn van hello Azure-abonnement toobe
* Hallo-naam van de gegevensfactory Hallo kan worden geregistreerd als DNS-naam in toekomstige Hallo en daarom ook openbaar zichtbaar.
* Als u Hallo-foutmelding: '**dit abonnement is niet geregistreerd toouse namespace Microsoft.DataFactory**', voer een van de volgende Hallo en probeer opnieuw te publiceren: 
  
  * Voer in Azure PowerShell Hallo opdracht tooregister Hallo Data Factory-provider te volgen: 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    Die Hallo Data Factory-provider is geregistreerd, kunt u na de opdracht tooconfirm Hallo uitvoeren. 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Aanmelding via het Azure-abonnement in Hallo Hallo [Azure-portal](https://portal.azure.com) en navigeer tooa Data Factory-blade of maak een gegevensfactory in hello Azure-portal. Deze actie automatisch Hallo provider voor u geregistreerd.

Voordat u een pijplijn maakt, moet u toocreate enkele Data Factory-entiteiten eerst. Maakt u eerst gekoppelde services toolink bron en bestemming gegevens slaat tooyour gegevens opslaan. Vervolgens definieert invoer- en uitvoergegevenssets toorepresent gegevens in de gekoppelde gegevensopslag. Maak ten slotte Hallo pijplijn met een activiteit die gebruikmaakt van deze gegevenssets.

## <a name="create-linked-services"></a>Gekoppelde services maken
U maken gekoppelde services in een data factory-toolink uw gegevens worden opgeslagen en compute services toohello data factory. In deze zelfstudie gebruikt u niet een willekeurige compute-service, zoals Azure HDInsight of Azure Data Lake Analytics. U gebruikt twee gegevensarchieven van het type Azure Storage (bron) en Azure SQL Database (doel). Daarom maakt u twee gekoppelde services met de naam AzureStorageLinkedService en AzureSqlLinkedService van het type: AzureStorage en AzureSqlDatabase.  

Hallo AzureStorageLinkedService koppelt u uw Azure storage-account toohello data factory. Dit opslagaccount wordt Hallo een waarop u container gemaakt en Hallo gegevens geüpload als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

Azuresqllinkedservice wordt uw Azure SQL database toohello data factory. Hallo-gegevens die worden gekopieerd van de blob-opslag hello wordt opgeslagen in deze database. Hallo emp-tabel in deze database wordt gemaakt als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).  

### <a name="create-azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service maken
In deze stap koppelt u uw Azure storage-account tooyour data factory. U geeft Hallo naam en sleutel van uw Azure storage-account in deze sectie. Zie [gekoppelde Azure Storage-service](data-factory-azure-blob-connector.md#azure-storage-linked-service) voor meer informatie over de JSON-eigenschappen die toodefine een Azure Storage gekoppelde service.  

1. Hallo opdracht toovariable met de naam toewijzen **cmd**. 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. Hallo-opdracht uitvoeren met behulp van **Invoke-Command**.

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Hallo resultaten weergeven. Hallo gekoppeld service is gemaakt, ziet u Hallo JSON voor Hallo gekoppelde service in Hallo **resultaten**; anders wordt een foutbericht wordt weergegeven.

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a>Gekoppelde Azure SQL-service maken
In deze stap koppelt u uw Azure SQL database tooyour data factory. U opgeven hello Azure SQL-servernaam, databasenaam, gebruikersnaam en wachtwoord in deze sectie. Zie [Azure SQL gekoppelde service](data-factory-azure-sql-connector.md#linked-service-properties) voor meer informatie over de JSON-eigenschappen die toodefine een Azure SQL gekoppelde service.

1. Hallo opdracht toovariable met de naam toewijzen **cmd**. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. Hallo-opdracht uitvoeren met behulp van **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Hallo resultaten weergeven. Hallo gekoppeld service is gemaakt, ziet u Hallo JSON voor Hallo gekoppelde service in Hallo **resultaten**; anders wordt een foutbericht wordt weergegeven.
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a>Gegevenssets maken
In de vorige stap Hallo gemaakt gekoppelde services toolink uw Azure Storage-account en de Azure SQL database tooyour data factory. In deze stap definieert u twee gegevenssets met de naam AzureBlobInput en AzureSqlOutput die vertegenwoordigen de invoer- en uitvoergegevens die zijn opgeslagen in Hallo gegevensarchieven waarnaar wordt verwezen door de AzureStorageLinkedService en AzureSqlLinkedService respectievelijk.

Hallo gekoppelde Azure storage-service geeft Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op uitvoeringstijd tooconnect tooyour Azure storage-account. En Hallo blob-invoerbron gegevensset (AzureBlobInput) geeft Hallo-container en Hallo-map met invoergegevens Hallo.  

Op deze manier geeft hello Azure SQL Database gekoppeld service Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op de runtime tooconnect tooyour Azure SQL database. En Hallo uitvoer gegevensset met SQL-tabel (OututDataset) geeft Hallo tabel in Hallo database toowhich Hallo gegevens uit Hallo blob-opslag worden gekopieerd. 

### <a name="create-input-dataset"></a>Invoergegevensset maken
In deze stap maakt u een gegevensset met de naam AzureBlobInput die tooa blob-bestand (emp.txt) verwijst in de hoofdmap Hallo van een blob-container (adftutorial) in hello Azure Storage dat wordt vertegenwoordigd door Hallo gekoppelde AzureStorageLinkedService-service. Als u niet een waarde voor fileName hello opgeven (of overslaan), zijn gegevens uit alle blobs in de invoermap Hallo gekopieerde toohello bestemming. In deze zelfstudie maakt opgeven u een waarde voor Hallo fileName. 

1. Hallo opdracht toovariable met de naam toewijzen **cmd**. 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. Hallo-opdracht uitvoeren met behulp van **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Hallo resultaten weergeven. Als Hallo gegevensset is gemaakt, ziet u Hallo JSON voor de gegevensset in Hallo Hallo **resultaten**; anders wordt een foutbericht wordt weergegeven.
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a>Uitvoergegevensset maken
Hello Azure SQL Database gekoppeld-service geeft Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op de runtime tooconnect tooyour Azure SQL database. Hallo SQL tabel uitvoergegevensset (OututDataset) in deze stap hebt u Hiermee geeft u Hallo-tabel in Hallo toowhich Hallo databasegegevens van Hallo blob-opslag is gekopieerd.

1. Hallo opdracht toovariable met de naam toewijzen **cmd**.

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. Hallo-opdracht uitvoeren met behulp van **Invoke-Command**.
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Hallo resultaten weergeven. Als Hallo gegevensset is gemaakt, ziet u Hallo JSON voor de gegevensset in Hallo Hallo **resultaten**; anders wordt een foutbericht wordt weergegeven.
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a>Pijplijn maken
In deze stap maakt u een pijplijn met een **kopieeractiviteit** die gebruikmaakt van **AzureBlobInput** als invoer en **AzureSqlOutput** als uitvoer.

Uitvoergegevensset is momenteel welke stations Hallo planning. In deze zelfstudie is uitvoergegevensset geconfigureerde tooproduce een segment eens per uur. Hallo pijplijn heeft een begintijd en eindtijd die één dag uit elkaar liggen, wat is 24 uur zijn. Daarom worden 24 segmenten van uitvoergegevensset geproduceerd door Hallo pijplijn. 

1. Hallo opdracht toovariable met de naam toewijzen **cmd**.

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. Hallo-opdracht uitvoeren met behulp van **Invoke-Command**.

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Hallo resultaten weergeven. Als Hallo gegevensset is gemaakt, ziet u Hallo JSON voor de gegevensset in Hallo Hallo **resultaten**; anders wordt een foutbericht wordt weergegeven.  

    ```PowerShell   
    Write-Host $results
    ```

**Gefeliciteerd!** U hebt een Azure-gegevensfactory, met een pijplijn waarmee gegevens worden gekopieerd uit Azure Blob Storage tooAzure SQL-database gemaakt.

## <a name="monitor-pipeline"></a>De pijplijn bewaken
In deze stap gebruikt u REST API van Data Factory toomonitor segmenten wordt geproduceerd door Hallo pijplijn.

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> Zorg ervoor dat Hallo begin- en tijden opgegeven in de Hallo na overeen Hallo start opdracht en van Hallo pijplijn eindtijden. 

```PowerShell
$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=2017-05-11T00%3a00%3a00.0000000Z"&"end=2017-05-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};
```

```PowerShell
$results2 = Invoke-Command -scriptblock $cmd;
```

```PowerShell
IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

Hallo Invoke-Command en uitgevoerd Hallo volgende totdat er een segment in **gereed** status of **mislukt** status. Als Hallo segment status gereed is, Controleer Hallo **emp** tabel in uw Azure SQL database voor de uitvoergegevens Hallo. 

Voor elk segment zijn twee rijen met gegevens uit het bronbestand Hallo gekopieerde toohello emp-tabel in hello Azure SQL-database. U ziet daarom 24 nieuwe records in Hallo emp-tabel wanneer alle Hallo segmenten worden verwerkt (in de status Ready heeft). 

## <a name="summary"></a>Samenvatting
In deze zelfstudie gebruikt u REST-API toocreate een Azure data factory toocopy gegevens uit een Azure-blobopslag tooan Azure SQL database. Hier volgen Hallo hoofdstappen die u in deze zelfstudie hebt uitgevoerd:  

1. U hebt een Azure-**gegevensfactory** gemaakt.
2. U hebt **gekoppelde services** gemaakt:
   1. Een Azure Storage gekoppelde service toolink uw Azure Storage-account dat invoergegevens bevat.     
   2. Een Azure SQL gekoppelde service toolink uw Azure SQL-database die uitvoergegevens Hallo bevat. 
3. U hebt **gegevenssets** gemaakt waarin de invoer- en uitvoergegevens van pijplijnen worden beschreven.
4. U hebt een **pijplijn** gemaakt met een kopieeractiviteit met BlobSource als bron en SqlSink als sink. 

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u voor een kopieerbewerking een Azure Blob-opslag gebruikt als brongegevensarchief en een Azure SQL-database als doelgegevensarchief. Hallo bevat volgende tabel een lijst met gegevensarchieven als bronnen en bestemmingen wordt ondersteund door Hallo kopieeractiviteit: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn over hoe gegevens uit een data toocopy opslaan, klikt u op Hallo-koppeling voor de gegevensopslag Hallo in Hallo tabel.
