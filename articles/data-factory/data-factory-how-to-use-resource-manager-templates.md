---
title: aaaUse Resource Manager-sjablonen in de Data Factory | Microsoft Docs
description: Meer informatie over hoe toocreate en gebruik Azure Resource Manager-sjablonen toocreate Data Factory-entiteiten.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: 
ms.assetid: 37724021-f55f-4e85-9206-6d4a48bda3d8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 60d5dbd29494420006aed6d5bd9a10a63c36bec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-templates-toocreate-azure-data-factory-entities"></a>Gebruik sjablonen toocreate Azure Data Factory-entiteiten
## <a name="overview"></a>Overzicht
Tijdens het gebruik van Azure Data Factory voor uw behoeften van de integratie gegevens u zult zien hetzelfde patroon hergebruiken Hallo in verschillende omgevingen of implementeren van Hallo dezelfde taak herhaaldelijk binnen Hallo dezelfde oplossing. Sjablonen te implementeren en beheren van deze scenario's in een eenvoudige manier. Sjablonen in Azure Data Factory zijn ideaal voor scenario's voor hergebruik en herhaling.

Neem Hallo situatie waarbij een organisatie 10 fabrieken in Hallo wereld heeft. Hallo-logboeken van elke plant worden opgeslagen in een afzonderlijke on-premises SQL Server-database. Hallo bedrijf wil toobuild een enkele datawarehouse in de cloud Hallo voor ad-hoc analyses. Wil ook dat toohave Hallo dezelfde logica maar verschillende configuraties voor ontwikkeling, testen en productie-omgevingen.

In dit geval wordt een taak herhaald toobe moet in dezelfde omgeving Hallo, maar met verschillende waarden voor Hallo 10 data factory voor iedere fabriek. In feite **herhaling** aanwezig is. Templating kunt Hallo abstractie van deze algemene stroom (dat wil zeggen, pijplijnen Hallo hebben dezelfde activiteiten in elke gegevensfactory), maar gebruikt u een afzonderlijke parameter-bestand voor iedere fabriek.

Bovendien zoals Hallo organisatie wil toodeploy deze 10 gegevensfactory meerdere keren in verschillende omgevingen, sjablonen kunnen gebruiken dit **hergebruik** door het gebruik van afzonderlijke parameterbestanden voor ontwikkeling, testen, en productieomgevingen.

## <a name="templating-with-azure-resource-manager"></a>Templating met Azure Resource Manager
[Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-overview.md#template-deployment) zijn een goede manier tooachieve templating in Azure Data Factory. Resource Manager-sjablonen worden Hallo-infrastructuur en configuratie van uw Azure-oplossing via een JSON-bestand definieert. Omdat Azure Resource Manager-sjablonen met alle/de meeste Azure-services werkt, kan deze worden veel gebruikt tooeasily alle bronnen van uw Azure assets beheren. Zie [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md) toolearn informatie over Hallo Resource Manager-sjablonen in het algemeen.

## <a name="tutorials"></a>Zelfstudies
Zie Hallo-zelfstudies voor stapsgewijze instructies toocreate Data Factory-entiteiten te volgen met behulp van Resource Manager-sjablonen:

* [Zelfstudie: Een pijplijn toocopy gegevens met behulp van Azure Resource Manager-sjabloon maken](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [Zelfstudie: Een pijplijn tooprocess gegevens met behulp van Azure Resource Manager-sjabloon maken](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a>Data Factory-sjablonen op GitHub
Bekijk hello Azure snel starten-sjablonen op GitHub te volgen:

* [Een Data factory toocopy gegevens uit Azure Blob Storage tooAzure SQL-Database maken](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [Maak een gegevensfactory met Hive-activiteit op Azure HDInsight-cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [Een Data factory toocopy gegevens maken van Salesforce tooAzure Blobs](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [Maak een gegevensfactory dat gekoppeld is activiteiten: gegevens worden gekopieerd van een FTP-server tooAzure Blobs, roept u een hive-script van een bellen op HDInsight-cluster tootransform Hallo gegevens en kopieert het resultaat in Azure SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

U kunt gratis tooshare uw Azure Data Factory-sjablonen op [Azure snel starten](https://azure.microsoft.com/documentation/templates/). Raadpleeg toohello [bijdrage handleiding](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) tijdens de ontwikkeling van sjablonen die kunnen worden gedeeld via deze opslagplaats.

Hallo volgende secties vindt u informatie over het definiëren van Data Factory-resources in een Resource Manager-sjabloon.

## <a name="defining-data-factory-resources-in-templates"></a>Het definiëren van Data Factory-resources in sjablonen
Hallo op het hoogste niveau sjabloon voor het definiëren van een gegevensfactory is:

```JSON
"$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
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
    { "type": "linkedservices",
        ...
    },
    {"type": "datasets",
        ...
    },
    {"type": "dataPipelines",
        ...
    }
}
```

### <a name="define-data-factory"></a>Een gegevensfactory definiëren
U definieert een gegevensfactory in Hallo Resource Manager-sjabloon zoals weergegeven in Hallo voorbeeld te volgen:

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
Hallo dataFactoryName is in 'variabelen' gedefinieerd als:

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a>Gekoppelde services definiëren

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

Zie [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) of [gekoppelde Services berekenen](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie over de JSON-eigenschappen voor de specifieke gekoppelde service Hallo Hallo gewenste toodeploy. Hallo 'dependsOn' parameter geeft de naam van de bijbehorende gegevensfactory Hallo. Een voorbeeld van het definiëren van een gekoppelde service voor Azure Storage wordt weergegeven in de volgende JSON-definitie Hallo:

### <a name="define-datasets"></a>Gegevenssets definiëren

```JSON
"type": "datasets",
"name": "[variables('<myDatasetName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<myDatasetLinkedServiceName>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    ...
}
```
Raadpleeg te[ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor meer informatie over de JSON-eigenschappen voor type van de specifieke dataset Hallo Hallo gewenste toodeploy. Opmerking Hallo 'dependsOn' parameter geeft u de naam van de bijbehorende gegevens Hallo factory en opslag gekoppelde service. Een voorbeeld van het type van de dataset van Azure blob storage definiëren wordt weergegeven in de volgende JSON-definitie Hallo:

```JSON
"type": "datasets",
"name": "[variables('storageDataset')]",
"dependsOn": [
    "[variables('dataFactoryName')]",
    "[variables('storageLinkedServiceName')]"
],
"apiVersion": "2015-10-01",
"properties": {
"type": "AzureBlob",
"linkedServiceName": "[variables('storageLinkedServiceName')]",
"typeProperties": {
    "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
    "fileName": "[parameters('sourceBlobName')]",
    "format": {
        "type": "TextFormat"
    }
},
"availability": {
    "frequency": "Hour",
    "interval": 1
}
```

### <a name="define-pipelines"></a>Pijplijnen definiëren

```JSON
"type": "dataPipelines",
"name": "[variables('<mypipelineName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<inputDatasetLinkedServiceName>')]",
    "[variables('<outputDatasetLinkedServiceName>')]",
    "[variables('<inputDataset>')]",
    "[variables('<outputDataset>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    activities: {
        ...
    }
}
```

Raadpleeg te[pijplijnen definiëren](data-factory-create-pipelines.md#pipeline-json) voor meer informatie over de JSON-eigenschappen voor het definiëren van Hallo Hallo specifieke pijplijn en activiteiten gewenste toodeploy. Opmerking Hallo 'dependsOn' parameter specificeert de naam van de gegevensfactory hello, en eventuele bijbehorende gekoppelde services of gegevenssets. Een voorbeeld van een pijplijn waarmee gegevens worden gekopieerd van Azure Blob Storage tooAzure SQL-Database wordt weergegeven in de volgende JSON-codefragment Hallo:

```JSON
"type": "datapipelines",
"name": "[variables('pipelineName')]",
"dependsOn": [
    "[variables('dataFactoryName')]",
    "[variables('azureStorageLinkedServiceName')]",
    "[variables('azureSqlLinkedServiceName')]",
    "[variables('blobInputDatasetName')]",
    "[variables('sqlOutputDatasetName')]"
],
"apiVersion": "2015-10-01",
"properties": {
    "activities": [
    {
        "name": "CopyFromAzureBlobToAzureSQL",
        "description": "Copy data frm Azure blob tooAzure SQL",
        "type": "Copy",
        "inputs": [
            {
                "name": "[variables('blobInputDatasetName')]"
            }
        ],
        "outputs": [
            {
                "name": "[variables('sqlOutputDatasetName')]"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "BlobSource"
            },
            "sink": {
                "type": "SqlSink",
                "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
            },
            "translator": {
                "type": "TabularTranslator",
                "columnMappings": "Column0:FirstName,Column1:LastName"
            }
        },
        "Policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 3,
            "timeout": "01:00:00"
        }
    }
    ],
    "start": "2016-10-03T00:00:00Z",
    "end": "2016-10-04T00:00:00Z"
}
```
## <a name="parameterizing-data-factory-template"></a>Data Factory-sjabloon parameters voorzien
Zie voor aanbevolen procedures op parameters voorzien [aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) artikel. In het algemeen moet gebruik van parameters worden geminimaliseerd, vooral als variabelen in plaats daarvan kunnen worden gebruikt. Geef alleen parameters in Hallo volgen scenario's:

* Instellingen variëren door omgeving (voorbeeld: ontwikkeling, testen en productie)
* Geheimen (zoals wachtwoorden)

Als u nodig hebt toopull geheimen van [Azure Key Vault](../key-vault/key-vault-get-started.md) bij het implementeren van Azure Data Factory-entiteiten met behulp van sjablonen opgeven Hallo **sleutelkluis** en **geheime naam** zoals weergegeven in Hallo voorbeeld te volgen:

```JSON
"parameters": {
    "storageAccountKey": {
        "reference": {
            "keyVault": {
                "id":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.KeyVault/vaults/<keyVaultName>",
             },
            "secretName": "<secretName>"
           },
       },
       ...
}
```

> [!NOTE]
> Tijdens het exporteren van sjablonen voor bestaande data Factory wordt momenteel nog niet ondersteund, is het in Hallo werkt.
>
>
