---
title: aaaBuild uw eerste gegevensfactory (REST) | Microsoft Docs
description: In deze zelfstudie maakt u een Azure Data Factory-voorbeeldpijplijn met behulp van de Data Factory-REST API.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7e0a2465-2d85-4143-a4bb-42e03c273097
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 5d8e39bd598cca35f91d501bad74e8a8436f8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a>Zelfstudie: uw eerste Azure-gegevensfactory bouwen met de Data Factory-REST API
> [!div class="op_single_selector"]
> * [Overzicht en vereisten](data-factory-build-your-first-pipeline.md)
> * [Azure Portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager-sjabloon](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


In dit artikel gebruikt u REST API van Data Factory toocreate uw eerste Azure-gegevensfactory. toodo hello zelfstudie met andere hulpprogramma's / SDK, selecteer een van de Hallo opties uit de vervolgkeuzelijst Hallo.

Hallo-pijplijn in deze zelfstudie is één activiteit: **HDInsight Hive-activiteit**. Deze activiteit wordt een hive-script uitgevoerd op een Azure HDInsight-cluster dat transformaties invoergegevens gegevens tooproduce uitvoer. Hallo pijplijn is geplande toorun wanneer een maand tussen Hallo begin- en eindtijden opgegeven.

> [!NOTE]
> In dit artikel omvat niet alle Hallo REST-API. Zie [Naslaginformatie voor Data Factory-REST API](/rest/api/datafactory/) voor uitgebreide documentatie over REST API.
> 
> Een pijplijn kan meer dan één activiteit hebben. En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit. Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.


## <a name="prerequisites"></a>Vereisten
* Lees [overzicht van de zelfstudie](data-factory-build-your-first-pipeline.md) artikel en volledige Hallo **vereiste** stappen.
* Installeer [Curl](https://curl.haxx.se/dlwiz/) op uw computer. U gebruikt Hallo CURL hulpprogramma met REST opdrachten toocreate een gegevensfactory.
* Volg de instructies in [dit artikel](../azure-resource-manager/resource-group-create-service-principal-portal.md) voor het volgende:
  1. Maak een webtoepassing met de naam **ADFGetStartedApp** in Azure Active Directory.
  2. Haal de **client-id** en **geheime sleutel** op.
  3. Haal de **tenant-id** op.
  4. Hallo toewijzen **ADFGetStartedApp** toepassing toohello **Data Factory Inzender** rol.
* Installeer [Azure PowerShell](/powershell/azure/overview).
* Start **PowerShell** en Voer Hallo de volgende opdracht. Houd Azure PowerShell open tot Hallo einde van deze zelfstudie. Als u sluiten en opnieuw opent, moet u toorun Hallo opdrachten opnieuw.
  1. Voer **Login-AzureRmAccount** en geef Hallo-gebruikersnaam en wachtwoord toosign in toohello Azure-portal te gebruiken.
  2. Voer **Get-AzureRmSubscription** tooview alle abonnementen voor dit account Hallo.
  3. Voer **Get-AzureRmSubscription - SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** tooselect Hallo abonnement dat u wilt dat toowork met. Vervang **NameOfAzureSubscription** met Hallo-naam van uw Azure-abonnement.
* Maak een Azure-resourcegroep met de naam **ADFTutorialResourceGroup** door het uitvoeren van de volgende opdracht in PowerShell Hallo Hallo:

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

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
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a>azurestoragelinkedservice.json
> [!IMPORTANT]
> Vervang **accountname** en **accountkey** door de naam en sleutel van uw Azure Storage-account. toolearn hoe tooget uw opslag heeft toegang tot sleutel, raadpleegt u Hallo informatie over hoe tooview, kopiëren en opnieuw genereren opslag toegangstoetsen in [uw opslagaccount beheren](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
>
>

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

### <a name="hdinsightondemandlinkedservicejson"></a>hdinsightondemandlinkedservice.json

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
| ClusterSize |De grootte van Hallo HDInsight-cluster. |
| TimeToLive |Hiermee geeft u op dat niet-actieve tijd Hallo voor Hallo HDInsight-cluster, voordat deze wordt verwijderd. |
| linkedServiceName |Hiermee geeft u op Hallo storage-account dat is gebruikt toostore Hallo logboeken die door HDInsight worden gegenereerd |

Houd er rekening mee Hallo volgende punten:

* Hallo Data Factory maakt een **op basis van Linux** HDInsight-cluster voor u Hello hierboven JSON. Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.
* U kunt **uw eigen HDInsight-cluster** gebruiken in plaats van een on-demand HDInsight-cluster. Zie [Gekoppelde HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) voor meer informatie.
* Hallo HDInsight-cluster maakt een **standaardcontainer** in Hallo-blobopslag die u hebt opgegeven in Hallo JSON (**linkedServiceName**). HDInsight verwijdert deze container niet wanneer Hallo-cluster is verwijderd. Dit gedrag is standaard. Met de gekoppelde HDInsight-service op aanvraag een HDInsight-cluster wordt gemaakt telkens wanneer een segment is verwerkt, tenzij er een bestaand livecluster (**timeToLive**) en wordt verwijderd als het Hallo-verwerking is voltooid.

    Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag. Als u niet ze hoeft voor het oplossen van problemen met taken hello, kunt u toodelete ze tooreduce Hallo opslag kosten. Hallo-namen van deze containers worden als volgt: ' adf**naamvanuwgegevensfactory**-**linkedservicename**- datum '. Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) toodelete containers in uw Azure-blobopslag.

Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.

### <a name="inputdatasetjson"></a>inputdataset.json

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

Hallo JSON wordt een gegevensset met de naam gedefinieerd **AzureBlobInput**, die staat voor invoergegevens van een activiteit in Hallo pijplijn. Bovendien wordt hiermee aangegeven dat Hallo invoergegevens in de blob-container Hallo aangeroepen bevinden zich **adfgetstarted** en Hallo map met de naam **inputdata**.

Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:

| Eigenschap | Beschrijving |
|:--- |:--- |
| type |Hallo type eigenschap wordt ingesteld tooAzureBlob omdat de gegevens zich in Azure blob-opslag. |
| linkedServiceName |verwijst toohello StorageLinkedService die u eerder hebt gemaakt. |
| fileName |Deze eigenschap is optioneel. Als u deze eigenschap niet opgeeft, worden alle Hallo-bestanden uit folderPath Hallo opgenomen. In dit geval wordt alleen Hallo input.log verwerkt. |
| type |Hallo-logboekbestanden zijn tekstbestanden, zodat we TextFormat gebruiken. |
| columnDelimiter |kolommen in Hallo logboekbestanden worden gescheiden door een kommateken () |
| frequency/interval |frequentie tooMonth ingesteld en interval is 1, wat betekent dat Hallo invoersegmenten één keer per maand beschikbaar zijn. |
| external |Deze eigenschap wordt tootrue ingesteld als Hallo invoergegevens niet worden gegenereerd door Hallo Data Factory-service. |

### <a name="outputdatasetjson"></a>outputdataset.json

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

Hallo JSON wordt een gegevensset met de naam gedefinieerd **AzureBlobOutput**, die uitvoergegevens voor een activiteit in de pijplijn Hallo vertegenwoordigt. Bovendien wordt hiermee aangegeven dat Hallo resultaten worden opgeslagen in blob-container Hallo aangeroepen **adfgetstarted** en Hallo map met de naam **partitioneddata**. Hallo **beschikbaarheid** sectie geeft die Hallo-uitvoergegevensset op maandelijkse basis wordt geproduceerd.

### <a name="pipelinejson"></a>pipeline.json
> [!IMPORTANT]
> Vervang **storageaccountname** door de naam van uw Azure Storage-account.
>
>

```JSON
{
    "name": "MyFirstPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [{
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                "scriptLinkedService": "AzureStorageLinkedService",
                "defines": {
                    "inputtable": "wasb://adfgetstarted@<stroageaccountname>.blob.core.windows.net/inputdata",
                    "partitionedtable": "wasb://adfgetstarted@<stroageaccountname>t.blob.core.windows.net/partitioneddata"
                }
            },
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }],
        "start": "2017-07-10T00:00:00Z",
        "end": "2017-07-11T00:00:00Z",
        "isPaused": false
    }
}
```

In de JSON-codefragment hello maakt u een pijplijn die bestaat uit een enkele activiteit waarvoor Hive tooprocess gegevens op een HDInsight-cluster worden gebruikt.

Hallo Hive-scriptbestand **partitionweblogs.hql**, wordt opgeslagen in hello Azure storage-account (Hallo door scriptLinkedService met de opgegeven **StorageLinkedService**), en in **script**  map in container Hallo **adfgetstarted**.

Hallo **definieert** sectie geeft een runtime-instellingen die toohello hive-script worden doorgegeven als Hive-configuratiewaarden (bijvoorbeeld ${hiveconf: inputtable}, ${partitionedtable}).

Hallo **start** en **end** eigenschappen van de pijplijn Hallo geeft Hallo actieve periode van Hallo-pijplijn.

In Hallo activiteits-JSON geeft u opgeven dat Hallo Hive-script wordt uitgevoerd op Hallo berekening die is opgegeven door Hallo **linkedServiceName** – **HDInsightOnDemandLinkedService**.

> [!NOTE]
> Zie 'Pijplijn-JSON' in [pijplijnen en activiteiten in Azure Data Factory](data-factory-create-pipelines.md) voor meer informatie over de JSON-eigenschappen die in het voorgaande voorbeeld Hallo.
>
>

## <a name="set-global-variables"></a>Globale variabelen instellen
Uitvoeren in Azure PowerShell Hallo opdrachten na waarbij Hallo waarden vervangt door uw eigen te volgen:

> [!IMPORTANT]
> Zie de sectie [Vereisten](#prerequisites) voor instructies over het verkrijgen van de client-id, het clientgeheim, de tenant-id en de abonnements-id.
>
>

```PowerShell
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
$adf = "FirstDataFactoryREST"
```


## <a name="authenticate-with-aad"></a>Verifiëren met AAD

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a>Een gegevensfactory maken
In deze stap maakt u een Azure-gegevensfactory met de naam **FirstDataFactoryREST**. Een gegevensfactory kan één of meer pijplijnen hebben. Een pijplijn kan één of meer activiteiten bevatten. Bijvoorbeeld een Kopieeractiviteit toocopy gegevens uit een doelgegevensopslagplaats tooa bron en het toorun in een HDInsight Hive-activiteit een Hive-script tootransform gegevens. Voer Hallo opdrachten toocreate hello gegevensfactory te volgen:

1. Hallo opdracht toovariable met de naam toewijzen **cmd**.

    Bevestig dat Hallo de naam van gegevensfactory Hallo u hier opgeeft (ADFCopyTutorialDF) komt overeen met de naam opgegeven in Hallo Hallo **datafactory.json**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. Hallo-opdracht uitvoeren met behulp van **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Hallo resultaten weergeven. Als Hallo gegevensfactory is gemaakt, ziet u Hallo JSON voor Hallo data factory in Hallo **resultaten**; anders wordt een foutbericht wordt weergegeven.

    ```PowerShell
    Write-Host $results
    ```

Houd er rekening mee Hallo volgende punten:

* Hallo-naam van hello Azure Data Factory moet wereldwijd uniek zijn. Als er een fout in resultaten Hallo: **Data factory-naam 'FirstDataFactoryREST' is niet beschikbaar**, Hallo volgende stappen:
  1. Hallo naam wijzigen (bijvoorbeeld yournameFirstDataFactoryREST) in Hallo **datafactory.json** bestand. Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.
  2. In de eerste opdracht Hallo waar Hallo **$cmd** variabele een waarde is toegewezen, FirstDataFactoryREST vervangen door de nieuwe naam Hallo en het Hallo-opdracht uitvoeren.
  3. Hallo volgende twee opdrachten tooinvoke Hallo REST-API toocreate Hallo data factory en printers Hallo resultaten van Hallo bewerking uitgevoerd.
* toocreate Data Factory-exemplaren, moet u bijdrager/beheerder zijn van hello Azure-abonnement toobe
* Hallo-naam van de gegevensfactory Hallo kan worden geregistreerd als DNS-naam in toekomstige Hallo en daarom ook openbaar zichtbaar.
* Als u Hallo-foutmelding: '**dit abonnement is niet geregistreerd toouse namespace Microsoft.DataFactory**', voer een van de volgende Hallo en probeer opnieuw te publiceren:

  * Voer in Azure PowerShell Hallo opdracht tooregister Hallo Data Factory-provider te volgen:

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      Die Hallo Data Factory-provider is geregistreerd, kunt u na de opdracht tooconfirm Hallo uitvoeren:
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Aanmelding via het Azure-abonnement in Hallo Hallo [Azure-portal](https://portal.azure.com) en navigeer tooa Data Factory-blade of maak een gegevensfactory in hello Azure-portal. Deze actie automatisch Hallo provider voor u geregistreerd.

Voordat u een pijplijn maakt, moet u toocreate enkele Data Factory-entiteiten eerst. U maakt eerst gekoppelde services toolink gegevens opslaan, definieert u welke invoer en uitvoer gegevenssets toorepresent gegevens in de gekoppelde gegevensopslag/berekeningen tooyour gegevens.

## <a name="create-linked-services"></a>Gekoppelde services maken
In deze stap koppelt u uw Azure-opslagaccount en een bellen op Azure HDInsight-cluster tooyour data factory. Hallo blokkeringen Hallo invoer en uitvoer-gegevens voor de pijplijn in dit voorbeeld hello Azure Storage-account. Hallo gekoppelde HDInsight-service is gebruikte toorun een Hive-script dat is opgegeven in de activiteit Hallo van Hallo pijplijn in dit voorbeeld.

### <a name="create-azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service maken
In deze stap koppelt u uw Azure Storage-account tooyour data factory. Met deze zelfstudie gebruikt u Hallo dezelfde Azure-opslagaccount invoer-en uitvoergegevens toostore en Hallo HQL-script bestand.

1. Hallo opdracht toovariable met de naam toewijzen **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. Hallo-opdracht uitvoeren met behulp van **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Hallo resultaten weergeven. Hallo gekoppeld service is gemaakt, ziet u Hallo JSON voor Hallo gekoppelde service in Hallo **resultaten**; anders wordt een foutbericht wordt weergegeven.

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a>Een gekoppelde HDInsight-service maken
In deze stap maakt koppelen u een gegevensfactory op aanvraag HDInsight-cluster tooyour. Hallo HDInsight-cluster wordt automatisch gemaakt tijdens runtime en na het verwerken is voltooid en niet-actieve voor de opgegeven tijdsduur Hallo verwijderd. U kunt uw eigen HDInsight-cluster gebruiken in plaats van een on-demand HDInsight-cluster. Zie [Gekoppelde services berekenen](data-factory-compute-linked-services.md) voor meer informatie.

1. Hallo opdracht toovariable met de naam toewijzen **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
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
In deze stap maakt u gegevenssets toorepresent Hallo invoer maken en uitvoergegevens voor Hive-verwerking. Deze gegevenssets verwijzen toohello **StorageLinkedService** u eerder in deze zelfstudie hebt gemaakt. Hallo gekoppelde service verwijst tooan Azure Storage-account en gegevenssets vindt u container, map en bestandsnaam in Hallo opslag van de invoer- en uitvoergegevens.

### <a name="create-input-dataset"></a>Invoergegevensset maken
In deze stap maakt u Hallo invoergegevensset toorepresent invoergegevens opgeslagen in hello Azure Blob storage.

1. Hallo opdracht toovariable met de naam toewijzen **cmd**.

    ```PowerShell
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
In deze stap maakt u Hallo gegevensset toorepresent uitvoer uitvoergegevens opgeslagen in hello Azure Blob-opslag.

1. Hallo opdracht toovariable met de naam toewijzen **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
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
In deze stap maakt u uw eerste pijplijn met een **HDInsightHive**-activiteit. Invoersegment maandelijks beschikbaar is (frequency: Month, interval: 1), uitvoer segment wordt geproduceerd, maandelijks en Hallo scheduler-eigenschap voor activiteit Hallo toomonthly ook is ingesteld. Hallo-instellingen voor Hallo uitvoergegevensset en Hallo activiteitenplanner moeten overeenkomen met. Uitvoergegevensset is momenteel welke stations Hallo planning, dus u een uitvoergegevensset maken moet, zelfs als Hallo activiteit geen uitvoer produceert. Als Hallo activiteit geen invoer neemt, kunt u maken Hallo invoergegevensset overslaan.

Controleer of u Hallo **input.log** bestand in Hallo **adfgetstarted/inputdata** map in hello Azure blob-opslag- en Voer Hallo opdracht toodeploy Hallo pijplijn te volgen. Sinds Hallo **start** en **end** keren worden ingesteld in de afgelopen Hallo en **isPaused** set toofalse, Hallo pijplijn is (activiteit in de pijplijn Hallo) wordt uitgevoerd onmiddellijk nadat u hebt geïmplementeerd.

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
4. U hebt uw eerste pijplijn gemaakt met Azure PowerShell!

## <a name="monitor-pipeline"></a>De pijplijn bewaken
In deze stap gebruikt u REST API van Data Factory toomonitor segmenten wordt geproduceerd door Hallo pijplijn.

```PowerShell
$ds ="AzureBlobOutput"

$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=1970-01-01T00%3a00%3a00.0000000Z"&"end=2016-08-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};

$results2 = Invoke-Command -scriptblock $cmd;

IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

> [!IMPORTANT]
> Het maken van een on-demand HDInsight-cluster duurt normaal gesproken enige tijd (ongeveer 20 minuten). Daarom verwachten Hallo pijplijn tootake **ongeveer 30 minuten** tooprocess Hallo segment.
>
>

Hallo Invoke-Command en uitgevoerd Hallo volgende totdat er Hallo segment **gereed** status of **mislukt** status. Als Hallo segment status gereed is, Controleer Hallo **partitioneddata** map in Hallo **adfgetstarted** container in uw blobopslag voor Hallo uitvoergegevens.  Hallo maken van een HDInsight-cluster op aanvraag duurt normaal gesproken enige tijd.

![Uitvoergegevens](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> Hallo-invoerbestand wordt verwijderd zodra het Hallo-segment is verwerkt. Als u toorerun Hallo segment of zelfstudie opnieuw hello, dus Hallo invoerbestand (input.log) toohello inputdata map van de container adfgetstarted Hallo uploadt.
>
>

U kunt ook gebruik van Azure portal toomonitor segmenten en los eventuele problemen. Zie voor meer informatie [Pijplijnen bewaken met de Azure Portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline).

## <a name="summary"></a>Samenvatting
In deze zelfstudie maakt u een Azure data factory tooprocess gegevens gemaakt door het Hive-script uitvoeren op een HDInsight hadoop-cluster. U hebt gebruikt Hallo Data Factory-Editor in hello Azure portal toodo Hallo stappen te volgen:

1. U hebt een Azure-**gegevensfactory** gemaakt.
2. U hebt twee **gekoppelde services** gemaakt:
   1. **Azure Storage** gekoppelde service toolink uw Azure-blobopslag die invoer-/ uitvoerbestanden toohello data factory.
   2. **Azure HDInsight** op aanvraag gekoppelde service toolink een bellen op HDInsight Hadoop-cluster toohello data factory. Azure Data Factory maakt een HDInsight Hadoop-cluster just in time tooprocess invoergegevens en uitvoergegevens produceren.
3. Twee gemaakt **gegevenssets**, die invoer- en gegevens voor HDInsight Hive-activiteit in Hallo pijplijn worden beschreven.
4. U hebt een **pijplijn** gemaakt met een **HDInsight Hive**-activiteit.

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u een pijplijn gemaakt met een transformatieactiviteit (HDInsight-activiteit) waarvoor een Hive-script wordt uitgevoerd op een on-demand Azure HDInsight-cluster. hoe de gegevens van een Kopieeractiviteit toocopy van een Azure Blob-tooAzure SQL, toouse zien toosee [zelfstudie: gegevens kopiëren van een Azure Blob-tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="see-also"></a>Zie ook
| Onderwerp | Beschrijving |
|:--- |:--- |
| [Naslaginformatie over de REST-API voor Data Factory](/rest/api/datafactory/) |Zie de uitgebreide documentatie over Data Factory-cmdlets |
| [Pijplijnen](data-factory-create-pipelines.md) |In dit artikel helpt u begrijpen pijplijnen en activiteiten in Azure Data Factory en hoe toouse ze tooconstruct end-to-end gegevensgestuurde werkstromen voor uw scenario of bedrijf. |
| [Gegevenssets](data-factory-create-datasets.md) |Op basis van dit artikel krijgt u inzicht in de gegevenssets in Azure Data Factory. |
| [Plannen en uitvoeren](data-factory-scheduling-and-execution.md) |Dit artikel wordt uitgelegd Hallo plannings- en uitvoeringsaspecten van het Azure Data Factory-toepassingsmodel. |
| [Pijplijnen bewaken en beheren met de app voor bewaking en beheer](data-factory-monitor-manage-app.md) |Dit artikel wordt beschreven hoe toomonitor, beheren en fouten opsporen in pijplijnen met behulp van Hallo voor bewaking en beheer-App. |
