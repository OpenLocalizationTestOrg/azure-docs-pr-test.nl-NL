---
title: aaaCreate op aanvraag Hadoop-clusters met behulp van de Data Factory - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toocreate op aanvraag Hadoop-clusters in HDInsight met behulp van Azure Data Factory.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: spelluru
ms.openlocfilehash: c869776ac270e37dec710b5fc8d2a792d9263129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a>Hadoop-clusters op aanvraag maken in HDInsight met behulp van Azure Data Factory
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

[Azure Data Factory](../data-factory/data-factory-introduction.md) is een cloud-gebaseerde gegevens integration-service die ingedeeld en automatiseert Hallo verplaatsing en transformatie van gegevens. Dit kan een HDInsight Hadoop-cluster just in time tooprocess een segment invoergegevens maken en Hallo cluster verwijderen als Hallo-verwerking voltooid is. Enkele van de voordelen van het gebruik van een on-demand HDInsight Hadoop-cluster Hallo zijn:

- U alleen betalen voor Hallo tijd taak wordt uitgevoerd op Hallo HDInsight Hadoop-cluster (plus een korte configureerbare niet-actieve tijd). Hallo facturering voor HDInsight-clusters worden pro rato per minuut, of u ze worden gebruikt of niet. Wanneer u een gekoppelde HDInsight-service op aanvraag in de Data Factory gebruikt, Hallo clusters op aanvraag gemaakt. En Hallo clusters worden automatisch verwijderd wanneer Hallo taken zijn voltooid. Daarom betaalt u alleen voor actieve tijd en Hallo korte niet-actieve tijd (time to live-instelling) Hallo-taak.
- U kunt een werkstroom met behulp van een Data Factory-pijplijn maken. U kunt bijvoorbeeld Hallo pijplijn toocopy gegevens uit een lokale SQL Server tooan Azure blob-opslag, gegevens over het installatieproces Hallo door het uitvoeren van een Hive-script en Pig-script op een on-demand HDInsight Hadoop-cluster hebben. Kopieer vervolgens Hallo resultaat gegevens tooan Azure SQL Data Warehouse voor BI toepassingen tooconsume.
- U kunt plannen Hallo werkstroom toorun periodiek (elk uur, dagelijks, wekelijks, maandelijks, enzovoort).

Een gegevensfactory kan één of meer gegevenspijplijnen hebben in Azure Data Factory. Een pijplijn gegevens heeft een of meer activiteiten. Er zijn twee soorten activiteiten: [activiteiten voor gegevensverplaatsing](../data-factory/data-factory-data-movement-activities.md) en [activiteiten voor gegevenstransformatie](../data-factory/data-factory-data-transformation-activities.md). U gebruikt data movement activiteiten (momenteel alleen Kopieeractiviteit) toomove gegevens uit een bron data store tooa doelgegevensopslagplaats. U gebruikt gegevenstransformatie activiteiten tootransform/proces gegevens. HDInsight Hive-activiteit is een van de activiteiten voor gegevenstransformatie hello wordt ondersteund door de Data Factory. U Hallo Hive-transformatie-activiteit gebruiken in deze zelfstudie.

Uw eigen HDInsight Hadoop-cluster of een on-demand HDInsight Hadoop-cluster, kunt u een hive-activiteit toouse configureren. In deze zelfstudie is Hallo Hive-activiteit in Hallo data factory-pijplijn geconfigureerde toouse een HDInsight-cluster op aanvraag. Daarom wanneer Hallo activiteit actief tooprocess een gegevenssegment, is dit wat er gebeurt:

1. Een HDInsight Hadoop-cluster wordt automatisch gemaakt voor u just in time tooprocess Hallo segment.  
2. Hallo invoergegevens wordt verwerkt door een HiveQL-script uitvoeren op Hallo-cluster.
3. Hallo HDInsight Hadoop-cluster wordt verwijderd nadat het Hallo-verwerking is voltooid en Hallo cluster Hallo geconfigureerd en de hoeveelheid tijd (timeToLive-instelling) niet actief is. Als de volgende gegevenssegment Hallo beschikbaar voor verwerking met van inactiviteit timeToLive is, is hello hetzelfde cluster gebruikte tooprocess Hallo segment.  

In deze zelfstudie voert Hallo HiveQL-script die zijn gekoppeld aan het hive-activiteit Hallo Hallo van de volgende activiteiten:

1. Maakt een externe tabel waarin verwijzingen Hallo onbewerkte web logboekgegevens opgeslagen in een Azure-blobopslag.
2. Partities Hallo onbewerkte gegevens op jaar en maand.
3. Winkels Hallo gepartitioneerde gegevens in hello Azure blob-opslag.

In deze zelfstudie maakt Hallo HiveQL-script die zijn gekoppeld aan het hive-activiteit Hallo een externe tabel waarin verwijzingen Hallo onbewerkte web logboekgegevens opgeslagen in hello Azure Blob Storage. Hier vindt u voor elke maand Hallo voorbeeld rijen in het invoerbestand Hallo.

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

Hallo HiveQL-script partities Hallo onbewerkte gegevens op jaar en maand. Drie uitvoermappen op basis van de vorige invoer hello wordt gemaakt. Elke map bevat een bestand met vermeldingen van elke maand.

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

Zie voor een lijst van activiteiten voor gegevenstransformatie Data Factory in toevoeging tooHive activiteit [transformeren en analyseren met Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).

> [!NOTE]
> U kunt op dit moment alleen HDInsight-cluster versie 3.2 maken uit Azure Data Factory.

## <a name="prerequisites"></a>Vereisten
Voordat u Hallo-instructies in dit artikel, moet u de volgende items Hallo hebben:

* [Azure-abonnement](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Azure PowerShell.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a>Voorbereiden van de storage-account
U kunt gebruiken om toothree storage-accounts in dit scenario:

- storage-standaardaccount voor Hallo HDInsight-cluster
- Storage-account voor de invoergegevens Hallo
- Storage-account voor de uitvoergegevens Hallo

toosimplify hello zelfstudie maakt u één storage account tooserve Hallo drie doeleinden. Hello Azure PowerShell-voorbeeldscript vinden in deze sectie voert Hallo taken te volgen:

1. Meld u bij tooAzure.
2. Maak een Azure-resourcegroep.
3. Maak een Azure Storage-account.
4. Een Blob-container in Hallo storage-account maken
5. Kopieer Hallo twee bestanden toohello Blob-container te volgen:

   * Invoergegevens bestand: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)
   * HiveQL-script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)

     Beide bestanden worden opgeslagen in een openbare Blob-container.


**tooprepare hello opslag en kopieer Hallo bestanden met Azure PowerShell:**
> [!IMPORTANT]
> Geef namen voor hello Azure-resourcegroep en hello Azure storage-account die door het Hallo-script wordt gemaakt.
> Noteer **Resourcegroepnaam**, **opslagaccountnaam**, en **opslagaccountsleutel** output door Hallo-script. U moet deze in de volgende sectie Hallo.

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect tooAzure
####################################
#region - Connect tooAzure subscription
Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use hello following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

Als u hulp nodig bij Hallo PowerShell-script, Zie [Using hello Azure PowerShell gebruiken met Azure Storage](../storage/common/storage-powershell-guide-full.md). Als u Azure CLI toouse in plaats daarvan Hallo raadpleegt [bijlage](#appendix) sectie voor hello Azure CLI-script.

**tooexamine hello storage-account en Hallo inhoud**

1. Meld u aan bij toohello [Azure-portal](https://portal.azure.com).
2. Klik op **resourcegroepen** in het linkerdeelvenster Hallo.
3. Dubbelklik op Hallo Resourcegroepnaam die u hebt gemaakt in uw PowerShell-script. Hallo-filter gebruiken als er te veel resourcegroepen die worden vermeld.
4. Op Hallo **Resources** tegel, wordt er een resource in de lijst, tenzij u de resourcegroep Hallo met andere projecten delen. Deze resource is Hallo opslagaccount met de Hallo-naam die u eerder hebt opgegeven. Klik op Hallo opslagaccountnaam.
5. Klik op Hallo **Blobs** tegels.
6. Klik op Hallo **adfgetstarted** container. U ziet twee mappen: **inputdata** en **script**.
7. Hallo-map openen en controleer Hallo-bestanden in mappen Hallo. Hallo inputdata hello input.log bestand met de invoergegevens bevat en Hallo scriptmap bevat Hallo HiveQL-scriptbestand.

## <a name="create-a-data-factory-using-resource-manager-template"></a>Maak een gegevensfactory met Resource Manager-sjabloon
Hallo storage-account, Hallo invoergegevens en Hallo HiveQL-script is voorbereid, bent u klaar toocreate een Azure data factory. Er zijn verschillende methoden voor het maken van de gegevensfactory. In deze zelfstudie maakt maken u een gegevensfactory door het implementeren van een Azure Resource Manager-sjabloon met hello Azure-portal. U kunt ook een Resource Manager-sjabloon implementeren met behulp van [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) en [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template). Zie voor andere data factory-aanmaakmethoden [zelfstudie: uw eerste gegevensfactory bouwen](../data-factory/data-factory-build-your-first-pipeline.md).

1. Klik op Hallo installatiekopie toosign in tooAzure en open Hallo Resource Manager-sjabloon in hello Azure-portal. Hallo-sjabloon bevindt zich op https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json. Zie Hallo [Data Factory-entiteiten in de sjabloon Hallo](#data-factory-entities-in-the-template) sectie voor gedetailleerde informatie over entiteiten in Hallo sjabloon worden gedefinieerd. 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Selecteer **gebruik bestaande** optie voor Hallo **resourcegroep** -instelling en selecteer Hallo-naam van het Hallo-resourcegroep die u hebt gemaakt in de vorige stap hello (met behulp van PowerShell-script).
3. Voer een naam voor de gegevensfactory hello (**Data Factory Name**). Deze naam moet uniek zijn.
4. Voer Hallo **opslagaccountnaam** en **opslagaccountsleutel** u in de vorige stap Hallo opgeschreven.
5. Selecteer **ik ga akkoord toohello voorwaarden en bepalingen** hierboven vermeld wordt na het lezen van via **voorwaarden en bepalingen**.
6. Selecteer **pincode toodashboard** optie.
6. Klik op **aankoop/maken**. U ziet een tegel op Hallo Dashboard aangeroepen **implementatie van sjabloonimplementatie**. Wachten tot Hallo **resourcegroep** blade voor de resourcegroep wordt geopend. U kunt ook klikken op Hallo tegel als uw groep naam tooopen Hallo resource resourcegroepblade titel.
6. Klik op Hallo tegel tooopen Hallo-resourcegroep als Hallo resourcegroepblade nog niet is geopend. Nu u dat één meer data factory-resource weergegeven naast toohello storage account bron ziet.
7. Klik op de naam van uw gegevensfactory hello (waarde die u hebt opgegeven voor Hallo **Data Factory Name** parameter).
8. Klik op Hallo Hallo Data Factory-Blade **Diagram** tegel. Hallo diagram ziet u een activiteit met een invoergegevensset en een uitvoergegevensset:

    ![Azure Data Factory HDInsight op aanvraag Hive-activiteit pipeline-diagram](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    Hallo-namen zijn gedefinieerd in Hallo Resource Manager-sjabloon.
9. Dubbelklik op **AzureBlobOutput**.
10. Op Hallo **onlangs bijgewerkt segmenten**, ziet u een segment. Als de status van de Hallo **Bezig**, wacht totdat deze te worden gewijzigd**gereed**. Het duurt meestal over **20 minuten** toocreate een HDInsight-cluster.

### <a name="check-hello-data-factory-output"></a>Controleer de Hallo data factory-uitvoer

1. Gebruik Hallo dezelfde procedure in Hallo laatste sessie toocheck Hallo-containers van de container adfgetstarted Hallo. Er zijn twee nieuwe containers bovendien ook**adfgetsarted**:

   * Een container met de naam die volgt op Hallo patroon: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`. Deze container is Hallo standaardcontainer voor Hallo HDInsight-cluster.
   * adfjobs: deze container is Hallo-container voor Hallo ADF taaklogboeken.

     Hallo data factory-uitvoer wordt opgeslagen in **afgetstarted** zoals u hebt geconfigureerd in Hallo Resource Manager-sjabloon.
2. Klik op **adfgetstarted**.
3. Dubbelklik op **partitioneddata**. U ziet een **jaar = 2014** map omdat alle Hallo weblogboeken datum in het jaar 2014.

    ![Azure Data Factory HDInsight op aanvraag Hive pijplijn uitvoer van activiteit](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    Als u de lijst Hallo detailanalyse, ziet u drie mappen voor januari, februari en maart. En er is een logboekbestand voor elke maand.

    ![Azure Data Factory HDInsight op aanvraag Hive pijplijn uitvoer van activiteit](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-hello-template"></a>Data Factory-entiteiten in Hallo-sjabloon
Hier ziet u hoe Hallo op het hoogste niveau Resource Manager-sjabloon voor een data factory eruit:

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```

### <a name="define-data-factory"></a>Een gegevensfactory definiëren
U definieert een gegevensfactory in Hallo Resource Manager-sjabloon zoals weergegeven in Hallo voorbeeld te volgen:  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
Hallo dataFactoryName is Hallo-naam van gegevensfactory Hallo die u opgeeft wanneer u Hallo sjabloon implementeert. Gegevensfactory is momenteel alleen ondersteund in Hallo regio's VS-Oost, VS-West en Noord-Europa.

### <a name="defining-entities-within-hello-data-factory"></a>Entiteiten in de gegevensfactory Hallo definiëren
Hallo worden volgende Data Factory-entiteiten gedefinieerd in de JSON-sjabloon Hallo:

* [Een gekoppelde Azure Storage-service](#azure-storage-linked-service)
* [Een gekoppelde HDInsight-service op aanvraag](#hdinsight-on-demand-linked-service)
* [De Azure Blob-invoergegevensset](#azure-blob-input-dataset)
* [De Azure Blob-uitvoergegevensset](#azure-blob-output-dataset)
* [De gegevenspijplijn met een kopieerbewerking](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service
Hello Azure Storage gekoppelde service uw Azure storage-account toohello data factory. In deze zelfstudie wordt hello hetzelfde opslagaccount gebruikt als Hallo HDInsight storage-standaardaccount, invoergegevens opslag- en uitvoer gegevensopslag. Daarom definieert u slechts één Azure Storage service gekoppelde. In de servicedefinitie Hallo gekoppeld geeft u Hallo naam en sleutel van uw Azure storage-account. Zie [gekoppelde Azure Storage-service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) voor meer informatie over de JSON-eigenschappen die toodefine een Azure Storage gekoppelde service.

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
Hallo **connectionString** maakt gebruik van parameters storageAccountName en storageAccountKey Hallo. U kunt waarden voor deze parameters opgeven tijdens het Hallo-sjabloon implementeren.  

#### <a name="hdinsight-on-demand-linked-service"></a>Een gekoppelde HDInsight-service op aanvraag
In Hallo op aanvraag HDInsight servicedefinitie gekoppeld, u waarden opgeven voor de configuratieparameters die worden gebruikt door Hallo Data Factory-service toocreate een HDInsight Hadoop-cluster tijdens runtime. Zie [gekoppelde services berekenen](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) artikel voor meer informatie over de JSON-eigenschappen die toodefine een gekoppelde HDInsight on demand-service.  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
Houd er rekening mee Hallo volgende punten:

* Hallo Data Factory maakt een **op basis van Linux** HDInsight-cluster voor u.
* Hallo HDInsight Hadoop-cluster wordt gemaakt in Hallo dezelfde regio bevinden als Hallo storage-account.
* Kennisgeving Hallo *timeToLive* instelling. Hallo data factory worden Hallo cluster automatisch verwijderd nadat het Hallo-cluster is inactiviteit gedurende 30 minuten.
* Hallo HDInsight-cluster maakt een **standaardcontainer** in Hallo-blobopslag die u hebt opgegeven in Hallo JSON (**linkedServiceName**). HDInsight verwijdert deze container niet wanneer Hallo-cluster is verwijderd. Dit gedrag is standaard. Met de gekoppelde HDInsight-service op aanvraag een HDInsight-cluster wordt gemaakt telkens wanneer een segment toobe verwerkt moet, tenzij er een bestaand livecluster is (**timeToLive**) en wordt verwijderd als het Hallo-verwerking is voltooid.

Zie [Gekoppelde on-demand HDInsight-service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.

> [!IMPORTANT]
> Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag. Als u niet ze hoeft voor het oplossen van problemen met taken hello, kunt u toodelete ze tooreduce Hallo opslag kosten. Hallo-namen van deze containers worden als volgt: ' adf**naamvanuwgegevensfactory**-**linkedservicename**- datum '. Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) toodelete containers in uw Azure-blobopslag.

#### <a name="azure-blob-input-dataset"></a>Azure Blob-invoergegevensset
In de definitie van de invoergegevensset hello opgeven u Hallo namen van de blob-container, map en -bestand met de invoergegevens Hallo. Zie [eigenschappen van de Azure Blob-gegevensset](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over de JSON-eigenschappen die toodefine een Azure Blob-gegevensset.

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
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

U ziet Hallo specifieke instellingen in de JSON-definitie hello te volgen:

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a>Azure Blob-uitvoergegevensset
In de gegevenssetdefinitie Hallo-uitvoer geeft u Hallo namen van blob-container en map waarin de uitvoergegevens Hallo. Zie [eigenschappen van de Azure Blob-gegevensset](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over de JSON-eigenschappen die toodefine een Azure Blob-gegevensset.  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

Hallo folderPath geeft Hallo pad toohello map die uitvoergegevens Hallo bevat:

```json
"folderPath": "adfgetstarted/partitioneddata",
```

Hallo [gegevensset beschikbaarheid](../data-factory/data-factory-create-datasets.md#dataset-availability) instelling is als volgt:

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

Output dataset beschikbaarheid stations Hallo pijplijn in Azure Data Factory. In dit voorbeeld Hallo segment maandelijks geproduceerd op Hallo laatste dag van de maand (EndOfInterval). Zie voor meer informatie [Data Factory plannen en uitvoeren](../data-factory/data-factory-scheduling-and-execution.md).

#### <a name="data-pipeline"></a>Gegevenspijplijn
Definieert u een pijplijn waarmee gegevens worden omgezet door het Hive-script uitvoeren op een on-demand Azure HDInsight cluster. Zie [pijplijn-JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) voor beschrijvingen van JSON-elementen die worden gebruikt toodefine een pijplijn in dit voorbeeld.

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

Hallo pipeline bevat één activiteit, HDInsightHive-activiteit. Als zowel begin- en einddatum in januari 2016, gegevens zijn voor slechts één maand (een segment) wordt verwerkt. Beide *start* en *end* van Hallo activiteit hebben een datum in het verleden, zodat Hallo Data Factory gegevens Hallo maand onmiddellijk verwerkt. Als Hallo end in de toekomst is, wordt een ander segment in de Hallo data factory maakt als Hallo tijd afkomstig is. Zie voor meer informatie [Data Factory plannen en uitvoeren](../data-factory/data-factory-scheduling-and-execution.md).

## <a name="clean-up-hello-tutorial"></a>Hallo-zelfstudie opschonen

### <a name="delete-hello-blob-containers-created-by-on-demand-hdinsight-cluster"></a>Hallo blob-containers gemaakt door on-demand HDInsight-cluster verwijderen
Met de gekoppelde HDInsight-service op aanvraag wordt een HDInsight-cluster gemaakt telkens wanneer een segment moet toobe verwerkt, tenzij er een bestaand livecluster (timeToLive); en Hallo cluster wordt verwijderd als het Hallo-verwerking is voltooid. Voor elk cluster maakt Azure Data Factory een blob-container in hello Azure blob-opslag gebruikt als Hallo stroage standaardaccount voor Hallo-cluster. Hoewel de HDInsight-cluster wordt verwijderd, worden Hallo standaard blob storage-container en Hallo gekoppeld opslagaccount niet verwijderd. Dit gedrag is standaard. Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag. Als u niet ze hoeft voor het oplossen van problemen met taken hello, kunt u toodelete ze tooreduce Hallo opslag kosten. Hallo-namen van deze containers een patroon volgen: `adfyourdatafactoryname-linkedservicename-datetimestamp`.

Hallo verwijderen **adfjobs** en **adfyourdatafactoryname-linkedservicename-datum** mappen. Hallo adfjobs container bevat taaklogboeken uit Azure Data Factory.

### <a name="delete-hello-resource-group"></a>Hallo-resourcegroep verwijderen
[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) gebruikte toodeploy is beheren en controleren van uw oplossing als een groep.  Een resourcegroep verwijdert, worden alle Hallo onderdelen binnen Hallo-groep.  

1. Meld u aan bij toohello [Azure-portal](https://portal.azure.com).
2. Klik op **resourcegroepen** in het linkerdeelvenster Hallo.
3. Klik op Hallo Resourcegroepnaam die u hebt gemaakt in uw PowerShell-script. Hallo-filter gebruiken als er te veel resourcegroepen die worden vermeld. Hallo-resourcegroep in een nieuwe blade geopend.
4. Op Hallo **Resources** tegel u heeft Hallo storage-standaardaccount en Hallo data factory is vermeld, tenzij u de resourcegroep Hallo met andere projecten delen.
5. Klik op **verwijderen** op Hallo Hallo blade bovenaan. In dat geval worden Hallo storage-account en Hallo-gegevens die zijn opgeslagen in Hallo storage-account verwijderd.
6. Voer Hallo resource group name tooconfirm verwijderen en klik vervolgens op **verwijderen**.

Als u niet dat toodelete Hallo storage-account wilt als u de resourcegroep Hallo verwijdert, overweeg Hallo architectuur volgen door te scheiden Hallo zakelijke gegevens uit Hallo storage-standaardaccount. In dit geval u hebt één resourcegroep voor Hallo storage-account met Hallo zakelijke gegevens en andere resourcegroep voor Hallo storage-standaardaccount voor HDInsight gekoppelde service en Hallo data factory Hallo. Wanneer u de tweede resourcegroep Hallo verwijdert, heeft deze geen invloed op Hallo zakelijke gegevens storage-account. toodo zodat:

* Hallo volgen op het hoogste niveau resourcegroep toohello samen met de Hallo Microsoft.DataFactory/datafactories resource in de Resource Manager-sjabloon toevoegen. Hiermee maakt u een opslagaccount:

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* Een nieuwe gekoppelde servicepunt toohello nieuwe opslagaccount toevoegen:

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* Hallo HDInsight ondemand gekoppelde service met een extra dependsOn en een additionalLinkedServiceNames configureren:

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe toouse Azure Data Factory toocreate bellen op HDInsight-cluster tooprocess Hive-taken. tooread meer:

* [Hadoop-zelfstudie: aan de slag met Hadoop op basis van Linux in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Hadoop op basis van Linux-clusters maken in HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [HDInsight-documentatie](https://azure.microsoft.com/documentation/services/hdinsight/)
* [Data factory-documentatie](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a>Bijlage

### <a name="azure-cli-script"></a>Azure CLI-script
U kunt Azure CLI gebruiken in plaats van Azure PowerShell toodo Hallo zelfstudie. Azure CLI toouse Azure CLI eerst installeren volgens Hallo instructies te volgen:

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-tooprepare-hello-storage-and-copy-hello-files"></a>Azure CLI tooprepare Hallo opslag gebruiken en het Hallo-bestanden te kopiëren

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

Hallo-containernaam is *adfgetstarted*. Houd het omdat deze. Anders moet u tooupdate Hallo Resource Manager-sjabloon. Als u hulp nodig bij dit script CLI, Zie [Using hello Azure CLI met Azure Storage](../storage/common/storage-azure-cli.md).
