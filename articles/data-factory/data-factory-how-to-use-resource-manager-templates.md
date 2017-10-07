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
# <a name="use-templates-toocreate-azure-data-factory-entities"></a><span data-ttu-id="587b7-103">Gebruik sjablonen toocreate Azure Data Factory-entiteiten</span><span class="sxs-lookup"><span data-stu-id="587b7-103">Use templates toocreate Azure Data Factory entities</span></span>
## <a name="overview"></a><span data-ttu-id="587b7-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="587b7-104">Overview</span></span>
<span data-ttu-id="587b7-105">Tijdens het gebruik van Azure Data Factory voor uw behoeften van de integratie gegevens u zult zien hetzelfde patroon hergebruiken Hallo in verschillende omgevingen of implementeren van Hallo dezelfde taak herhaaldelijk binnen Hallo dezelfde oplossing.</span><span class="sxs-lookup"><span data-stu-id="587b7-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing hello same pattern across different environments or implementing hello same task repetitively within hello same solution.</span></span> <span data-ttu-id="587b7-106">Sjablonen te implementeren en beheren van deze scenario's in een eenvoudige manier.</span><span class="sxs-lookup"><span data-stu-id="587b7-106">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="587b7-107">Sjablonen in Azure Data Factory zijn ideaal voor scenario's voor hergebruik en herhaling.</span><span class="sxs-lookup"><span data-stu-id="587b7-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="587b7-108">Neem Hallo situatie waarbij een organisatie 10 fabrieken in Hallo wereld heeft.</span><span class="sxs-lookup"><span data-stu-id="587b7-108">Consider hello situation where an organization has 10 manufacturing plants across hello world.</span></span> <span data-ttu-id="587b7-109">Hallo-logboeken van elke plant worden opgeslagen in een afzonderlijke on-premises SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="587b7-109">hello logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="587b7-110">Hallo bedrijf wil toobuild een enkele datawarehouse in de cloud Hallo voor ad-hoc analyses.</span><span class="sxs-lookup"><span data-stu-id="587b7-110">hello company wants toobuild a single data warehouse in hello cloud for ad-hoc analytics.</span></span> <span data-ttu-id="587b7-111">Wil ook dat toohave Hallo dezelfde logica maar verschillende configuraties voor ontwikkeling, testen en productie-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="587b7-111">It also wants toohave hello same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="587b7-112">In dit geval wordt een taak herhaald toobe moet in dezelfde omgeving Hallo, maar met verschillende waarden voor Hallo 10 data factory voor iedere fabriek.</span><span class="sxs-lookup"><span data-stu-id="587b7-112">In this case, a task needs toobe repeated within hello same environment, but with different values across hello 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="587b7-113">In feite **herhaling** aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="587b7-113">In effect, **repetition** is present.</span></span> <span data-ttu-id="587b7-114">Templating kunt Hallo abstractie van deze algemene stroom (dat wil zeggen, pijplijnen Hallo hebben dezelfde activiteiten in elke gegevensfactory), maar gebruikt u een afzonderlijke parameter-bestand voor iedere fabriek.</span><span class="sxs-lookup"><span data-stu-id="587b7-114">Templating allows hello abstraction of this generic flow (that is, pipelines having hello same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="587b7-115">Bovendien zoals Hallo organisatie wil toodeploy deze 10 gegevensfactory meerdere keren in verschillende omgevingen, sjablonen kunnen gebruiken dit **hergebruik** door het gebruik van afzonderlijke parameterbestanden voor ontwikkeling, testen, en productieomgevingen.</span><span class="sxs-lookup"><span data-stu-id="587b7-115">Furthermore, as hello organization wants toodeploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="587b7-116">Templating met Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="587b7-116">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="587b7-117">[Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-overview.md#template-deployment) zijn een goede manier tooachieve templating in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="587b7-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way tooachieve templating in Azure Data Factory.</span></span> <span data-ttu-id="587b7-118">Resource Manager-sjablonen worden Hallo-infrastructuur en configuratie van uw Azure-oplossing via een JSON-bestand definieert.</span><span class="sxs-lookup"><span data-stu-id="587b7-118">Resource Manager templates define hello infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="587b7-119">Omdat Azure Resource Manager-sjablonen met alle/de meeste Azure-services werkt, kan deze worden veel gebruikt tooeasily alle bronnen van uw Azure assets beheren.</span><span class="sxs-lookup"><span data-stu-id="587b7-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used tooeasily manage all resources of your Azure assets.</span></span> <span data-ttu-id="587b7-120">Zie [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md) toolearn informatie over Hallo Resource Manager-sjablonen in het algemeen.</span><span class="sxs-lookup"><span data-stu-id="587b7-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn more about hello Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="587b7-121">Zelfstudies</span><span class="sxs-lookup"><span data-stu-id="587b7-121">Tutorials</span></span>
<span data-ttu-id="587b7-122">Zie Hallo-zelfstudies voor stapsgewijze instructies toocreate Data Factory-entiteiten te volgen met behulp van Resource Manager-sjablonen:</span><span class="sxs-lookup"><span data-stu-id="587b7-122">See hello following tutorials for step-by-step instructions toocreate Data Factory entities by using Resource Manager templates:</span></span>

* [<span data-ttu-id="587b7-123">Zelfstudie: Een pijplijn toocopy gegevens met behulp van Azure Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="587b7-123">Tutorial: Create a pipeline toocopy data by using Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="587b7-124">Zelfstudie: Een pijplijn tooprocess gegevens met behulp van Azure Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="587b7-124">Tutorial: Create a pipeline tooprocess data by using Azure Resource Manager template</span></span>](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="587b7-125">Data Factory-sjablonen op GitHub</span><span class="sxs-lookup"><span data-stu-id="587b7-125">Data Factory templates on GitHub</span></span>
<span data-ttu-id="587b7-126">Bekijk hello Azure snel starten-sjablonen op GitHub te volgen:</span><span class="sxs-lookup"><span data-stu-id="587b7-126">Check out hello following Azure quick start templates on GitHub:</span></span>

* [<span data-ttu-id="587b7-127">Een Data factory toocopy gegevens uit Azure Blob Storage tooAzure SQL-Database maken</span><span class="sxs-lookup"><span data-stu-id="587b7-127">Create a Data factory toocopy data from Azure Blob Storage tooAzure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [<span data-ttu-id="587b7-128">Maak een gegevensfactory met Hive-activiteit op Azure HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="587b7-128">Create a Data factory with Hive activity on Azure HDInsight cluster</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [<span data-ttu-id="587b7-129">Een Data factory toocopy gegevens maken van Salesforce tooAzure Blobs</span><span class="sxs-lookup"><span data-stu-id="587b7-129">Create a Data factory toocopy data from Salesforce tooAzure Blobs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [<span data-ttu-id="587b7-130">Maak een gegevensfactory dat gekoppeld is activiteiten: gegevens worden gekopieerd van een FTP-server tooAzure Blobs, roept u een hive-script van een bellen op HDInsight-cluster tootransform Hallo gegevens en kopieert het resultaat in Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="587b7-130">Create a Data factory that chains activities: copies data from an FTP server tooAzure Blobs, invokes a hive script on an on-demand HDInsight cluster tootransform hello data, and copies result into Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

<span data-ttu-id="587b7-131">U kunt gratis tooshare uw Azure Data Factory-sjablonen op [Azure snel starten](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="587b7-131">Feel free tooshare your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="587b7-132">Raadpleeg toohello [bijdrage handleiding](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) tijdens de ontwikkeling van sjablonen die kunnen worden gedeeld via deze opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="587b7-132">Refer toohello [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="587b7-133">Hallo volgende secties vindt u informatie over het definiëren van Data Factory-resources in een Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="587b7-133">hello following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="587b7-134">Het definiëren van Data Factory-resources in sjablonen</span><span class="sxs-lookup"><span data-stu-id="587b7-134">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="587b7-135">Hallo op het hoogste niveau sjabloon voor het definiëren van een gegevensfactory is:</span><span class="sxs-lookup"><span data-stu-id="587b7-135">hello top-level template for defining a data factory is:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="587b7-136">Een gegevensfactory definiëren</span><span class="sxs-lookup"><span data-stu-id="587b7-136">Define data factory</span></span>
<span data-ttu-id="587b7-137">U definieert een gegevensfactory in Hallo Resource Manager-sjabloon zoals weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="587b7-137">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="587b7-138">Hallo dataFactoryName is in 'variabelen' gedefinieerd als:</span><span class="sxs-lookup"><span data-stu-id="587b7-138">hello dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="587b7-139">Gekoppelde services definiëren</span><span class="sxs-lookup"><span data-stu-id="587b7-139">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="587b7-140">Zie [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) of [gekoppelde Services berekenen](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie over de JSON-eigenschappen voor de specifieke gekoppelde service Hallo Hallo gewenste toodeploy.</span><span class="sxs-lookup"><span data-stu-id="587b7-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about hello JSON properties for hello specific linked service you wish toodeploy.</span></span> <span data-ttu-id="587b7-141">Hallo 'dependsOn' parameter geeft de naam van de bijbehorende gegevensfactory Hallo.</span><span class="sxs-lookup"><span data-stu-id="587b7-141">hello “dependsOn” parameter specifies name of hello corresponding data factory.</span></span> <span data-ttu-id="587b7-142">Een voorbeeld van het definiëren van een gekoppelde service voor Azure Storage wordt weergegeven in de volgende JSON-definitie Hallo:</span><span class="sxs-lookup"><span data-stu-id="587b7-142">An example of defining a linked service for Azure Storage is shown in hello following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="587b7-143">Gegevenssets definiëren</span><span class="sxs-lookup"><span data-stu-id="587b7-143">Define datasets</span></span>

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
<span data-ttu-id="587b7-144">Raadpleeg te[ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor meer informatie over de JSON-eigenschappen voor type van de specifieke dataset Hallo Hallo gewenste toodeploy.</span><span class="sxs-lookup"><span data-stu-id="587b7-144">Refer too[Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about hello JSON properties for hello specific dataset type you wish toodeploy.</span></span> <span data-ttu-id="587b7-145">Opmerking Hallo 'dependsOn' parameter geeft u de naam van de bijbehorende gegevens Hallo factory en opslag gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="587b7-145">Note hello “dependsOn” parameter specifies name of hello corresponding data factory and storage linked service.</span></span> <span data-ttu-id="587b7-146">Een voorbeeld van het type van de dataset van Azure blob storage definiëren wordt weergegeven in de volgende JSON-definitie Hallo:</span><span class="sxs-lookup"><span data-stu-id="587b7-146">An example of defining dataset type of Azure blob storage is shown in hello following JSON definition:</span></span>

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

### <a name="define-pipelines"></a><span data-ttu-id="587b7-147">Pijplijnen definiëren</span><span class="sxs-lookup"><span data-stu-id="587b7-147">Define pipelines</span></span>

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

<span data-ttu-id="587b7-148">Raadpleeg te[pijplijnen definiëren](data-factory-create-pipelines.md#pipeline-json) voor meer informatie over de JSON-eigenschappen voor het definiëren van Hallo Hallo specifieke pijplijn en activiteiten gewenste toodeploy.</span><span class="sxs-lookup"><span data-stu-id="587b7-148">Refer too[defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about hello JSON properties for defining hello specific pipeline and activities you wish toodeploy.</span></span> <span data-ttu-id="587b7-149">Opmerking Hallo 'dependsOn' parameter specificeert de naam van de gegevensfactory hello, en eventuele bijbehorende gekoppelde services of gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="587b7-149">Note hello “dependsOn” parameter specifies name of hello data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="587b7-150">Een voorbeeld van een pijplijn waarmee gegevens worden gekopieerd van Azure Blob Storage tooAzure SQL-Database wordt weergegeven in de volgende JSON-codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="587b7-150">An example of a pipeline that copies data from Azure Blob Storage tooAzure SQL Database is shown in hello following JSON snippet:</span></span>

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
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="587b7-151">Data Factory-sjabloon parameters voorzien</span><span class="sxs-lookup"><span data-stu-id="587b7-151">Parameterizing Data Factory template</span></span>
<span data-ttu-id="587b7-152">Zie voor aanbevolen procedures op parameters voorzien [aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) artikel.</span><span class="sxs-lookup"><span data-stu-id="587b7-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span></span> <span data-ttu-id="587b7-153">In het algemeen moet gebruik van parameters worden geminimaliseerd, vooral als variabelen in plaats daarvan kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="587b7-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="587b7-154">Geef alleen parameters in Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="587b7-154">Only provide parameters in hello following scenarios:</span></span>

* <span data-ttu-id="587b7-155">Instellingen variëren door omgeving (voorbeeld: ontwikkeling, testen en productie)</span><span class="sxs-lookup"><span data-stu-id="587b7-155">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="587b7-156">Geheimen (zoals wachtwoorden)</span><span class="sxs-lookup"><span data-stu-id="587b7-156">Secrets (such as passwords)</span></span>

<span data-ttu-id="587b7-157">Als u nodig hebt toopull geheimen van [Azure Key Vault](../key-vault/key-vault-get-started.md) bij het implementeren van Azure Data Factory-entiteiten met behulp van sjablonen opgeven Hallo **sleutelkluis** en **geheime naam** zoals weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="587b7-157">If you need toopull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify hello **key vault** and **secret name** as shown in hello following example:</span></span>

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
> <span data-ttu-id="587b7-158">Tijdens het exporteren van sjablonen voor bestaande data Factory wordt momenteel nog niet ondersteund, is het in Hallo werkt.</span><span class="sxs-lookup"><span data-stu-id="587b7-158">While exporting templates for existing data factories is currently not yet supported, it is in hello works.</span></span>
>
>
