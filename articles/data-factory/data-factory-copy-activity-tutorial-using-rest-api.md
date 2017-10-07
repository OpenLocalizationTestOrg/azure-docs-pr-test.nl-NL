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
# <a name="tutorial-use-rest-api-toocreate-an-azure-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="f0b60-103">Zelfstudie: Gebruik REST-API toocreate toocopy gegevens in een Azure Data Factory-pipeline</span><span class="sxs-lookup"><span data-stu-id="f0b60-103">Tutorial: Use REST API toocreate an Azure Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f0b60-104">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="f0b60-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="f0b60-105">De wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="f0b60-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="f0b60-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f0b60-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="f0b60-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f0b60-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="f0b60-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f0b60-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="f0b60-109">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="f0b60-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="f0b60-110">REST API</span><span class="sxs-lookup"><span data-stu-id="f0b60-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="f0b60-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="f0b60-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="f0b60-112">In dit artikel leert u hoe toouse REST-API toocreate een gegevensfactory met een pijplijn waarmee gegevens worden gekopieerd van een Azure blob storage tooan Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="f0b60-112">In this article, you learn how toouse REST API toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="f0b60-113">Als u nieuwe tooAzure Data Factory, lees Hallo [inleiding tooAzure Data Factory](data-factory-introduction.md) artikel voordat u deze zelfstudie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="f0b60-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="f0b60-114">In deze zelfstudie maakt u een pijplijn met één activiteit erin: kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="f0b60-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="f0b60-115">Hallo kopieeractiviteit kopieert gegevens van een gegevensarchief voor ondersteunde gegevens store tooa ondersteunde sink.</span><span class="sxs-lookup"><span data-stu-id="f0b60-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="f0b60-116">Zie [Ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met gegevensarchieven die worden ondersteund als bron en als sink.</span><span class="sxs-lookup"><span data-stu-id="f0b60-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="f0b60-117">Hallo-activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens tussen verschillende gegevensarchieven op een manier veilig, betrouwbaar en schaalbaar kan worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="f0b60-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="f0b60-118">Zie voor meer informatie over Hallo Kopieeractiviteit [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="f0b60-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="f0b60-119">Een pijplijn kan meer dan één activiteit hebben.</span><span class="sxs-lookup"><span data-stu-id="f0b60-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="f0b60-120">En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="f0b60-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="f0b60-121">Zie [Meerdere activiteiten in een pijplijn](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f0b60-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="f0b60-122">In dit artikel omvat niet alle Hallo REST-API van Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f0b60-122">This article does not cover all hello Data Factory REST API.</span></span> <span data-ttu-id="f0b60-123">Zie [Naslaginformatie voor Data Factory-REST API](/rest/api/datafactory/) voor uitgebreide documentatie over Data Factory-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="f0b60-123">See [Data Factory REST API Reference](/rest/api/datafactory/) for comprehensive documentation on Data Factory cmdlets.</span></span>
>  
> <span data-ttu-id="f0b60-124">Hallo data pipeline in deze zelfstudie worden gegevens gekopieerd van een bron data store tooa doelgegevensopslagplaats.</span><span class="sxs-lookup"><span data-stu-id="f0b60-124">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="f0b60-125">Voor een zelfstudie over het tootransform van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: een pijplijn tootransform gegevens met Hadoop-cluster bouwen](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="f0b60-125">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0b60-126">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f0b60-126">Prerequisites</span></span>
* <span data-ttu-id="f0b60-127">Doorloop [overzicht van de zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) en volledige Hallo **vereiste** stappen.</span><span class="sxs-lookup"><span data-stu-id="f0b60-127">Go through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="f0b60-128">Installeer [Curl](https://curl.haxx.se/dlwiz/) op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f0b60-128">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="f0b60-129">U gebruikt Hallo Curl hulpprogramma met REST opdrachten toocreate een gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="f0b60-129">You use hello Curl tool with REST commands toocreate a data factory.</span></span> 
* <span data-ttu-id="f0b60-130">Volg de instructies in [dit artikel](../azure-resource-manager/resource-group-create-service-principal-portal.md) voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="f0b60-130">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span> 
  1. <span data-ttu-id="f0b60-131">Maak een webtoepassing met de naam **ADFCopyTutorialApp** in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f0b60-131">Create a Web application named **ADFCopyTutorialApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="f0b60-132">Haal de **client-id** en **geheime sleutel** op.</span><span class="sxs-lookup"><span data-stu-id="f0b60-132">Get **client ID** and **secret key**.</span></span> 
  3. <span data-ttu-id="f0b60-133">Haal de **tenant-id** op.</span><span class="sxs-lookup"><span data-stu-id="f0b60-133">Get **tenant ID**.</span></span> 
  4. <span data-ttu-id="f0b60-134">Hallo toewijzen **ADFCopyTutorialApp** toepassing toohello **Data Factory Inzender** rol.</span><span class="sxs-lookup"><span data-stu-id="f0b60-134">Assign hello **ADFCopyTutorialApp** application toohello **Data Factory Contributor** role.</span></span>  
* <span data-ttu-id="f0b60-135">Installeer [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f0b60-135">Install [Azure PowerShell](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="f0b60-136">Start **PowerShell** en Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="f0b60-136">Launch **PowerShell** and do hello following steps.</span></span> <span data-ttu-id="f0b60-137">Houd Azure PowerShell open tot Hallo einde van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f0b60-137">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="f0b60-138">Als u sluiten en opnieuw opent, moet u toorun Hallo opdrachten opnieuw.</span><span class="sxs-lookup"><span data-stu-id="f0b60-138">If you close and reopen, you need toorun hello commands again.</span></span>
  
  1. <span data-ttu-id="f0b60-139">Voer Hallo volgende opdracht en Voer Hallo-gebruikersnaam en wachtwoord toosign in toohello Azure-portal te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f0b60-139">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal:</span></span>
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. <span data-ttu-id="f0b60-140">Voer Hallo opdracht tooview na alle Hallo abonnementen voor dit account:</span><span class="sxs-lookup"><span data-stu-id="f0b60-140">Run hello following command tooview all hello subscriptions for this account:</span></span>

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. <span data-ttu-id="f0b60-141">Hallo opdracht tooselect Hallo abonnement dat u wilt dat toowork met volgende worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f0b60-141">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="f0b60-142">Vervang  **&lt;NameOfAzureSubscription** &gt; met Hallo-naam van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f0b60-142">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span> 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. <span data-ttu-id="f0b60-143">Maak een Azure-resourcegroep met de naam **ADFTutorialResourceGroup** door het uitvoeren van de volgende opdracht in PowerShell Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="f0b60-143">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      <span data-ttu-id="f0b60-144">Als de resourcegroep Hallo al bestaat, die u opgeeft of tooupdate deze (Y) of als (N).</span><span class="sxs-lookup"><span data-stu-id="f0b60-144">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span> 
     
      <span data-ttu-id="f0b60-145">Sommige van Hallo stappen in deze zelfstudie wordt ervan uitgegaan dat u het Hallo-resourcegroep met de naam ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="f0b60-145">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="f0b60-146">Als u een andere resourcegroep gebruikt, moet u toouse Hallo-naam van de resourcegroep in plaats van ADFTutorialResourceGroup in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f0b60-146">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="f0b60-147">JSON-definities maken</span><span class="sxs-lookup"><span data-stu-id="f0b60-147">Create JSON definitions</span></span>
<span data-ttu-id="f0b60-148">Maken de volgende JSON-bestanden in Hallo map waar curl.exe zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="f0b60-148">Create following JSON files in hello folder where curl.exe is located.</span></span> 

### <a name="datafactoryjson"></a><span data-ttu-id="f0b60-149">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="f0b60-149">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f0b60-150">Naam moet globaal uniek zijn, zodat u tooprefix-/ achtervoegseltekenreeks ADFCopyTutorialDF toomake kunt deze een unieke naam op.</span><span class="sxs-lookup"><span data-stu-id="f0b60-150">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span> 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="f0b60-151">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="f0b60-151">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f0b60-152">Vervang **accountname** en **accountkey** door de naam en sleutel van uw Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="f0b60-152">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="f0b60-153">toolearn hoe tooget uw opslag toegang krijgen tot sleutel, Zie [toegangssleutels voor opslag weergeven, kopiëren en opnieuw genereren](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="f0b60-153">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>

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

<span data-ttu-id="f0b60-154">Zie [Gekoppelde Azure Storage-service](data-factory-azure-blob-connector.md#azure-storage-linked-service) voor meer informatie over de JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="f0b60-154">For details about JSON properties, see [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span></span>

### <a name="azuersqllinkedservicejson"></a><span data-ttu-id="f0b60-155">azuersqllinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="f0b60-155">azuersqllinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f0b60-156">Vervang **servername**, **databasename**, **gebruikersnaam**, en **wachtwoord** met de naam van uw Azure SQL-server van SQL-database, de naam van gebruiker account en wachtwoord voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="f0b60-156">Replace **servername**, **databasename**, **username**, and **password** with name of your Azure SQL server, name of SQL database, user account, and password for hello account.</span></span>  
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

<span data-ttu-id="f0b60-157">Zie [Gekoppelde Azure SQL-service](data-factory-azure-sql-connector.md#linked-service-properties) voor meer informatie over de JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="f0b60-157">For details about JSON properties, see [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="f0b60-158">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="f0b60-158">inputdataset.json</span></span>

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

<span data-ttu-id="f0b60-159">Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:</span><span class="sxs-lookup"><span data-stu-id="f0b60-159">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="f0b60-160">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="f0b60-160">Property</span></span> | <span data-ttu-id="f0b60-161">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f0b60-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f0b60-162">type</span><span class="sxs-lookup"><span data-stu-id="f0b60-162">type</span></span> | <span data-ttu-id="f0b60-163">Hallo type wordt ingesteld te**AzureBlob** omdat de gegevens zich in een Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="f0b60-163">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
| <span data-ttu-id="f0b60-164">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="f0b60-164">linkedServiceName</span></span> | <span data-ttu-id="f0b60-165">Toohello verwijst **AzureStorageLinkedService** die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f0b60-165">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="f0b60-166">folderPath</span><span class="sxs-lookup"><span data-stu-id="f0b60-166">folderPath</span></span> | <span data-ttu-id="f0b60-167">Hiermee geeft u op Hallo blob **container** en Hallo **map** die invoer blobs bevat.</span><span class="sxs-lookup"><span data-stu-id="f0b60-167">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="f0b60-168">In deze zelfstudie adftutorial is Hallo blob-container en map Hallo-hoofdmap is.</span><span class="sxs-lookup"><span data-stu-id="f0b60-168">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
| <span data-ttu-id="f0b60-169">fileName</span><span class="sxs-lookup"><span data-stu-id="f0b60-169">fileName</span></span> | <span data-ttu-id="f0b60-170">Deze eigenschap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="f0b60-170">This property is optional.</span></span> <span data-ttu-id="f0b60-171">Als u deze eigenschap niet opgeeft, worden alle bestanden uit folderPath Hallo opgenomen.</span><span class="sxs-lookup"><span data-stu-id="f0b60-171">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="f0b60-172">In deze zelfstudie **emp.txt** hello bestandsnaam, zodat alleen dat bestand wordt opgehaald voor de verwerking wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f0b60-172">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
| <span data-ttu-id="f0b60-173">format -> type</span><span class="sxs-lookup"><span data-stu-id="f0b60-173">format -> type</span></span> |<span data-ttu-id="f0b60-174">Hallo-bestand voor invoer is in de indeling van de tekst hello, zodat we gebruiken **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="f0b60-174">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
| <span data-ttu-id="f0b60-175">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="f0b60-175">columnDelimiter</span></span> | <span data-ttu-id="f0b60-176">Hallo-kolommen in het invoerbestand Hallo worden gescheiden door **kommateken (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="f0b60-176">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
| <span data-ttu-id="f0b60-177">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="f0b60-177">frequency/interval</span></span> | <span data-ttu-id="f0b60-178">Hallo frequentie te is ingesteld**uur** en interval is ingesteld, te**1**, wat betekent dat Hallo invoer segmenten zijn beschikbaar **per uur**.</span><span class="sxs-lookup"><span data-stu-id="f0b60-178">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="f0b60-179">Met andere woorden, Hallo Data Factory-service zoekt invoergegevens elk uur in de hoofdmap Hallo van blob-container (**adftutorial**) u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f0b60-179">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="f0b60-180">Hallo-gegevens binnen Hallo pijplijn begin- en tijden, niet voor of na deze tijden zoekt.</span><span class="sxs-lookup"><span data-stu-id="f0b60-180">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
| <span data-ttu-id="f0b60-181">external</span><span class="sxs-lookup"><span data-stu-id="f0b60-181">external</span></span> | <span data-ttu-id="f0b60-182">Deze eigenschap is ingesteld, te**true** als Hallo gegevens niet worden gegenereerd door deze pijplijn.</span><span class="sxs-lookup"><span data-stu-id="f0b60-182">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="f0b60-183">Hallo invoergegevens in deze zelfstudie wordt Hallo emp.txt bestand, die niet worden gegenereerd door deze pipeline, zodat we de tootrue van deze eigenschap wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f0b60-183">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

<span data-ttu-id="f0b60-184">Zie het [artikel over Azure Blob-connectoren](data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over deze JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="f0b60-184">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>

### <a name="outputdatasetjson"></a><span data-ttu-id="f0b60-185">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="f0b60-185">outputdataset.json</span></span>

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
<span data-ttu-id="f0b60-186">Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:</span><span class="sxs-lookup"><span data-stu-id="f0b60-186">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="f0b60-187">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="f0b60-187">Property</span></span> | <span data-ttu-id="f0b60-188">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f0b60-188">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f0b60-189">type</span><span class="sxs-lookup"><span data-stu-id="f0b60-189">type</span></span> | <span data-ttu-id="f0b60-190">Hallo type wordt ingesteld te**AzureSqlTable** omdat gegevens gekopieerde tooa tabel in een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="f0b60-190">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
| <span data-ttu-id="f0b60-191">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="f0b60-191">linkedServiceName</span></span> | <span data-ttu-id="f0b60-192">Toohello verwijst **AzureSqlLinkedService** die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f0b60-192">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="f0b60-193">tableName</span><span class="sxs-lookup"><span data-stu-id="f0b60-193">tableName</span></span> | <span data-ttu-id="f0b60-194">Opgegeven Hallo **tabel** toowhich Hallo gegevens worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="f0b60-194">Specified hello **table** toowhich hello data is copied.</span></span> | 
| <span data-ttu-id="f0b60-195">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="f0b60-195">frequency/interval</span></span> | <span data-ttu-id="f0b60-196">Hallo frequentie is ingesteld te**uur** en interval is **1**, wat betekent dat Hallo uitvoer segmenten worden geproduceerd **per uur** tussen Hallo pijplijn begin- en tijden niet voor of na deze tijden.</span><span class="sxs-lookup"><span data-stu-id="f0b60-196">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

<span data-ttu-id="f0b60-197">Er zijn drie kolommen – **ID**, **FirstName**, en **LastName** – in Hallo emp-tabel in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="f0b60-197">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="f0b60-198">-ID is een identiteitskolom, dus u alleen toospecify hoeft **FirstName** en **LastName** hier.</span><span class="sxs-lookup"><span data-stu-id="f0b60-198">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

<span data-ttu-id="f0b60-199">Zie het [artikel over Azure SQL-connectoren](data-factory-azure-sql-connector.md#dataset-properties) voor meer informatie over deze JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="f0b60-199">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="f0b60-200">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="f0b60-200">pipeline.json</span></span>

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

<span data-ttu-id="f0b60-201">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="f0b60-201">Note hello following points:</span></span>

- <span data-ttu-id="f0b60-202">In Hallo gedeelte activiteiten is er slechts één activiteit waarvan **type** te is ingesteld,**kopie**.</span><span class="sxs-lookup"><span data-stu-id="f0b60-202">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="f0b60-203">Zie voor meer informatie over de kopieeractiviteit hello [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="f0b60-203">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="f0b60-204">In Data Factory-oplossingen kunt u ook [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f0b60-204">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
- <span data-ttu-id="f0b60-205">Invoer voor Hallo-activiteit is ingesteld, te**AzureBlobInput** en de uitvoer voor Hallo activiteit te is ingesteld**AzureSqlOutput**.</span><span class="sxs-lookup"><span data-stu-id="f0b60-205">Input for hello activity is set too**AzureBlobInput** and output for hello activity is set too**AzureSqlOutput**.</span></span> 
- <span data-ttu-id="f0b60-206">In Hallo **typeProperties** sectie **BlobSource** is opgegeven als Hallo brontype en **SqlSink** is opgegeven als Hallo sink-type.</span><span class="sxs-lookup"><span data-stu-id="f0b60-206">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="f0b60-207">Zie voor een volledige lijst van gegevensarchieven die worden ondersteund door Hallo kopieeractiviteit als bronnen en put [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="f0b60-207">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="f0b60-208">toolearn hoe toouse een specifieke ondersteunde gegevens opslaan als een bron/sink, klikt u op Hallo-koppeling in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="f0b60-208">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
 
<span data-ttu-id="f0b60-209">Vervang de waarde Hallo Hallo **start** eigenschap met de huidige dag Hallo en **end** waarde met de volgende dag Hallo.</span><span class="sxs-lookup"><span data-stu-id="f0b60-209">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="f0b60-210">U kunt alleen Hallo datumgedeelte opgeven en Hallo tijdgedeelte van Hallo datum / tijd overslaan.</span><span class="sxs-lookup"><span data-stu-id="f0b60-210">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="f0b60-211">Bijvoorbeeld '2017-02-03', dat te gelijk ' 2017-02-03T00:00:00Z '</span><span class="sxs-lookup"><span data-stu-id="f0b60-211">For example, "2017-02-03", which is equivalent too"2017-02-03T00:00:00Z"</span></span>
 
<span data-ttu-id="f0b60-212">Zowel de begin- als einddatum en -tijd moeten de [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601) hebben.</span><span class="sxs-lookup"><span data-stu-id="f0b60-212">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="f0b60-213">Bijvoorbeeld: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="f0b60-213">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="f0b60-214">Hallo **end** tijd is optioneel, maar er worden gebruikt in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f0b60-214">hello **end** time is optional, but we use it in this tutorial.</span></span> 
 
<span data-ttu-id="f0b60-215">Als u geen waarde voor Hallo opgeeft **end** eigenschap, wordt berekend als '**start + 48 uur**'.</span><span class="sxs-lookup"><span data-stu-id="f0b60-215">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="f0b60-216">toorun hello pijplijn voor onbepaalde tijd, geef **9999-09-09** als waarde voor Hallo Hallo **end** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="f0b60-216">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
 
<span data-ttu-id="f0b60-217">In de Hallo voorgaande voorbeeld, zijn er 24 gegevenssegmenten omdat elke gegevenssegment per uur is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f0b60-217">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

<span data-ttu-id="f0b60-218">Zie het artikel [Pijplijnen maken](data-factory-create-pipelines.md) voor beschrijvingen van JSON-eigenschappen in de definitie van een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="f0b60-218">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f0b60-219">Zie [Gegevensverplaatsingsactiviteiten](data-factory-data-movement-activities.md) voor beschrijvingen van JSON-eigenschappen in de definitie van een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="f0b60-219">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="f0b60-220">Zie het [artikel over Azure Blob-connectoren](data-factory-azure-blob-connector.md) voor beschrijvingen van JSON-eigenschappen die worden ondersteund door BlobSource.</span><span class="sxs-lookup"><span data-stu-id="f0b60-220">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="f0b60-221">Zie het [artikel over Azure SQL Database-connectoren](data-factory-azure-sql-connector.md) voor beschrijvingen van JSON-eigenschappen die worden ondersteund door SqlSink.</span><span class="sxs-lookup"><span data-stu-id="f0b60-221">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="set-global-variables"></a><span data-ttu-id="f0b60-222">Globale variabelen instellen</span><span class="sxs-lookup"><span data-stu-id="f0b60-222">Set global variables</span></span>
<span data-ttu-id="f0b60-223">Uitvoeren in Azure PowerShell Hallo opdrachten na waarbij Hallo waarden vervangt door uw eigen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f0b60-223">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0b60-224">Zie de sectie [Vereisten](#prerequisites) voor instructies over het verkrijgen van de client-id, het clientgeheim, de tenant-id en de abonnements-id.</span><span class="sxs-lookup"><span data-stu-id="f0b60-224">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

<span data-ttu-id="f0b60-225">Voer Hallo volgende opdracht na het bijwerken van de naam van de gegevensfactory Hallo Hallo die u gebruikt:</span><span class="sxs-lookup"><span data-stu-id="f0b60-225">Run hello following command after updating hello name of hello data factory you are using:</span></span> 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a><span data-ttu-id="f0b60-226">Verifiëren met AAD</span><span class="sxs-lookup"><span data-stu-id="f0b60-226">Authenticate with AAD</span></span>
<span data-ttu-id="f0b60-227">Voer Hallo opdracht tooauthenticate met Azure Active Directory (AAD) te volgen:</span><span class="sxs-lookup"><span data-stu-id="f0b60-227">Run hello following command tooauthenticate with Azure Active Directory (AAD):</span></span> 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a><span data-ttu-id="f0b60-228">Een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="f0b60-228">Create data factory</span></span>
<span data-ttu-id="f0b60-229">In deze stap maakt u een Azure-gegevensfactory met de naam **ADFCopyTutorialDF**.</span><span class="sxs-lookup"><span data-stu-id="f0b60-229">In this step, you create an Azure Data Factory named **ADFCopyTutorialDF**.</span></span> <span data-ttu-id="f0b60-230">Een gegevensfactory kan één of meer pijplijnen hebben.</span><span class="sxs-lookup"><span data-stu-id="f0b60-230">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="f0b60-231">Een pijplijn kan één of meer activiteiten bevatten.</span><span class="sxs-lookup"><span data-stu-id="f0b60-231">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="f0b60-232">Bijvoorbeeld een Kopieeractiviteit toocopy gegevens uit een bron tooa bestemming gegevens opslaan.</span><span class="sxs-lookup"><span data-stu-id="f0b60-232">For example, a Copy Activity toocopy data from a source tooa destination data store.</span></span> <span data-ttu-id="f0b60-233">Het toorun in een HDInsight Hive-activiteit een Hive-script tootransform invoer gegevens tooproduct uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="f0b60-233">A HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="f0b60-234">Voer Hallo opdrachten toocreate hello gegevensfactory te volgen:</span><span class="sxs-lookup"><span data-stu-id="f0b60-234">Run hello following commands toocreate hello data factory:</span></span> 

1. <span data-ttu-id="f0b60-235">Hallo opdracht toovariable met de naam toewijzen **cmd**.</span><span class="sxs-lookup"><span data-stu-id="f0b60-235">Assign hello command toovariable named **cmd**.</span></span> 
   
    > [!IMPORTANT]
    > <span data-ttu-id="f0b60-236">Bevestig dat Hallo de naam van gegevensfactory Hallo u hier opgeeft (ADFCopyTutorialDF) komt overeen met de naam opgegeven in Hallo Hallo **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="f0b60-236">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. <span data-ttu-id="f0b60-237">Hallo-opdracht uitvoeren met behulp van **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="f0b60-237">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="f0b60-238">Hallo resultaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="f0b60-238">View hello results.</span></span> <span data-ttu-id="f0b60-239">Als Hallo gegevensfactory is gemaakt, ziet u Hallo JSON voor Hallo data factory in Hallo **resultaten**; anders wordt een foutbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f0b60-239">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>  
   
    ```
    Write-Host $results
    ```

<span data-ttu-id="f0b60-240">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="f0b60-240">Note hello following points:</span></span>

* <span data-ttu-id="f0b60-241">Hallo-naam van hello Azure Data Factory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="f0b60-241">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="f0b60-242">Als er een fout in resultaten Hallo: **Data factory-naam 'ADFCopyTutorialDF' is niet beschikbaar**, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="f0b60-242">If you see hello error in results: **Data factory name “ADFCopyTutorialDF” is not available**, do hello following steps:</span></span>  
  
  1. <span data-ttu-id="f0b60-243">Hallo naam wijzigen (bijvoorbeeld yournameADFCopyTutorialDF) in Hallo **datafactory.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="f0b60-243">Change hello name (for example, yournameADFCopyTutorialDF) in hello **datafactory.json** file.</span></span>
  2. <span data-ttu-id="f0b60-244">In de eerste opdracht Hallo waar Hallo **$cmd** variabele een waarde is toegewezen, ADFCopyTutorialDF vervangen door de nieuwe naam Hallo en het Hallo-opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f0b60-244">In hello first command where hello **$cmd** variable is assigned a value, replace ADFCopyTutorialDF with hello new name and run hello command.</span></span> 
  3. <span data-ttu-id="f0b60-245">Hallo volgende twee opdrachten tooinvoke Hallo REST-API toocreate Hallo data factory en printers Hallo resultaten van Hallo bewerking uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f0b60-245">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span> 
     
     <span data-ttu-id="f0b60-246">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="f0b60-246">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="f0b60-247">toocreate Data Factory-exemplaren, moet u bijdrager/beheerder zijn van hello Azure-abonnement toobe</span><span class="sxs-lookup"><span data-stu-id="f0b60-247">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="f0b60-248">Hallo-naam van de gegevensfactory Hallo kan worden geregistreerd als DNS-naam in toekomstige Hallo en daarom ook openbaar zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="f0b60-248">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="f0b60-249">Als u Hallo-foutmelding: '**dit abonnement is niet geregistreerd toouse namespace Microsoft.DataFactory**', voer een van de volgende Hallo en probeer opnieuw te publiceren:</span><span class="sxs-lookup"><span data-stu-id="f0b60-249">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span> 
  
  * <span data-ttu-id="f0b60-250">Voer in Azure PowerShell Hallo opdracht tooregister Hallo Data Factory-provider te volgen:</span><span class="sxs-lookup"><span data-stu-id="f0b60-250">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="f0b60-251">Die Hallo Data Factory-provider is geregistreerd, kunt u na de opdracht tooconfirm Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f0b60-251">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="f0b60-252">Aanmelding via het Azure-abonnement in Hallo Hallo [Azure-portal](https://portal.azure.com) en navigeer tooa Data Factory-blade of maak een gegevensfactory in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f0b60-252">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="f0b60-253">Deze actie automatisch Hallo provider voor u geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="f0b60-253">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="f0b60-254">Voordat u een pijplijn maakt, moet u toocreate enkele Data Factory-entiteiten eerst.</span><span class="sxs-lookup"><span data-stu-id="f0b60-254">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="f0b60-255">Maakt u eerst gekoppelde services toolink bron en bestemming gegevens slaat tooyour gegevens opslaan.</span><span class="sxs-lookup"><span data-stu-id="f0b60-255">You first create linked services toolink source and destination data stores tooyour data store.</span></span> <span data-ttu-id="f0b60-256">Vervolgens definieert invoer- en uitvoergegevenssets toorepresent gegevens in de gekoppelde gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="f0b60-256">Then, define input and output datasets toorepresent data in linked data stores.</span></span> <span data-ttu-id="f0b60-257">Maak ten slotte Hallo pijplijn met een activiteit die gebruikmaakt van deze gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="f0b60-257">Finally, create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="f0b60-258">Gekoppelde services maken</span><span class="sxs-lookup"><span data-stu-id="f0b60-258">Create linked services</span></span>
<span data-ttu-id="f0b60-259">U maken gekoppelde services in een data factory-toolink uw gegevens worden opgeslagen en compute services toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="f0b60-259">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="f0b60-260">In deze zelfstudie gebruikt u niet een willekeurige compute-service, zoals Azure HDInsight of Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="f0b60-260">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="f0b60-261">U gebruikt twee gegevensarchieven van het type Azure Storage (bron) en Azure SQL Database (doel).</span><span class="sxs-lookup"><span data-stu-id="f0b60-261">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> <span data-ttu-id="f0b60-262">Daarom maakt u twee gekoppelde services met de naam AzureStorageLinkedService en AzureSqlLinkedService van het type: AzureStorage en AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="f0b60-262">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="f0b60-263">Hallo AzureStorageLinkedService koppelt u uw Azure storage-account toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="f0b60-263">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="f0b60-264">Dit opslagaccount wordt Hallo een waarop u container gemaakt en Hallo gegevens geüpload als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="f0b60-264">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="f0b60-265">Azuresqllinkedservice wordt uw Azure SQL database toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="f0b60-265">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="f0b60-266">Hallo-gegevens die worden gekopieerd van de blob-opslag hello wordt opgeslagen in deze database.</span><span class="sxs-lookup"><span data-stu-id="f0b60-266">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="f0b60-267">Hallo emp-tabel in deze database wordt gemaakt als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="f0b60-267">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="f0b60-268">Een gekoppelde Azure Storage-service maken</span><span class="sxs-lookup"><span data-stu-id="f0b60-268">Create Azure Storage linked service</span></span>
<span data-ttu-id="f0b60-269">In deze stap koppelt u uw Azure storage-account tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="f0b60-269">In this step, you link your Azure storage account tooyour data factory.</span></span> <span data-ttu-id="f0b60-270">U geeft Hallo naam en sleutel van uw Azure storage-account in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="f0b60-270">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="f0b60-271">Zie [gekoppelde Azure Storage-service](data-factory-azure-blob-connector.md#azure-storage-linked-service) voor meer informatie over de JSON-eigenschappen die toodefine een Azure Storage gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="f0b60-271">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span>  

1. <span data-ttu-id="f0b60-272">Hallo opdracht toovariable met de naam toewijzen **cmd**.</span><span class="sxs-lookup"><span data-stu-id="f0b60-272">Assign hello command toovariable named **cmd**.</span></span> 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="f0b60-273">Hallo-opdracht uitvoeren met behulp van **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="f0b60-273">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="f0b60-274">Hallo resultaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="f0b60-274">View hello results.</span></span> <span data-ttu-id="f0b60-275">Hallo gekoppeld service is gemaakt, ziet u Hallo JSON voor Hallo gekoppelde service in Hallo **resultaten**; anders wordt een foutbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f0b60-275">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a><span data-ttu-id="f0b60-276">Gekoppelde Azure SQL-service maken</span><span class="sxs-lookup"><span data-stu-id="f0b60-276">Create Azure SQL linked service</span></span>
<span data-ttu-id="f0b60-277">In deze stap koppelt u uw Azure SQL database tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="f0b60-277">In this step, you link your Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="f0b60-278">U opgeven hello Azure SQL-servernaam, databasenaam, gebruikersnaam en wachtwoord in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="f0b60-278">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="f0b60-279">Zie [Azure SQL gekoppelde service](data-factory-azure-sql-connector.md#linked-service-properties) voor meer informatie over de JSON-eigenschappen die toodefine een Azure SQL gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="f0b60-279">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used toodefine an Azure SQL linked service.</span></span>

1. <span data-ttu-id="f0b60-280">Hallo opdracht toovariable met de naam toewijzen **cmd**.</span><span class="sxs-lookup"><span data-stu-id="f0b60-280">Assign hello command toovariable named **cmd**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="f0b60-281">Hallo-opdracht uitvoeren met behulp van **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="f0b60-281">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="f0b60-282">Hallo resultaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="f0b60-282">View hello results.</span></span> <span data-ttu-id="f0b60-283">Hallo gekoppeld service is gemaakt, ziet u Hallo JSON voor Hallo gekoppelde service in Hallo **resultaten**; anders wordt een foutbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f0b60-283">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="f0b60-284">Gegevenssets maken</span><span class="sxs-lookup"><span data-stu-id="f0b60-284">Create datasets</span></span>
<span data-ttu-id="f0b60-285">In de vorige stap Hallo gemaakt gekoppelde services toolink uw Azure Storage-account en de Azure SQL database tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="f0b60-285">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="f0b60-286">In deze stap definieert u twee gegevenssets met de naam AzureBlobInput en AzureSqlOutput die vertegenwoordigen de invoer- en uitvoergegevens die zijn opgeslagen in Hallo gegevensarchieven waarnaar wordt verwezen door de AzureStorageLinkedService en AzureSqlLinkedService respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="f0b60-286">In this step, you define two datasets named AzureBlobInput and AzureSqlOutput that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="f0b60-287">Hallo gekoppelde Azure storage-service geeft Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op uitvoeringstijd tooconnect tooyour Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="f0b60-287">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="f0b60-288">En Hallo blob-invoerbron gegevensset (AzureBlobInput) geeft Hallo-container en Hallo-map met invoergegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="f0b60-288">And, hello input blob dataset (AzureBlobInput) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="f0b60-289">Op deze manier geeft hello Azure SQL Database gekoppeld service Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op de runtime tooconnect tooyour Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="f0b60-289">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="f0b60-290">En Hallo uitvoer gegevensset met SQL-tabel (OututDataset) geeft Hallo tabel in Hallo database toowhich Hallo gegevens uit Hallo blob-opslag worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="f0b60-290">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="f0b60-291">Invoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="f0b60-291">Create input dataset</span></span>
<span data-ttu-id="f0b60-292">In deze stap maakt u een gegevensset met de naam AzureBlobInput die tooa blob-bestand (emp.txt) verwijst in de hoofdmap Hallo van een blob-container (adftutorial) in hello Azure Storage dat wordt vertegenwoordigd door Hallo gekoppelde AzureStorageLinkedService-service.</span><span class="sxs-lookup"><span data-stu-id="f0b60-292">In this step, you create a dataset named AzureBlobInput that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="f0b60-293">Als u niet een waarde voor fileName hello opgeven (of overslaan), zijn gegevens uit alle blobs in de invoermap Hallo gekopieerde toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="f0b60-293">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="f0b60-294">In deze zelfstudie maakt opgeven u een waarde voor Hallo fileName.</span><span class="sxs-lookup"><span data-stu-id="f0b60-294">In this tutorial, you specify a value for hello fileName.</span></span> 

1. <span data-ttu-id="f0b60-295">Hallo opdracht toovariable met de naam toewijzen **cmd**.</span><span class="sxs-lookup"><span data-stu-id="f0b60-295">Assign hello command toovariable named **cmd**.</span></span> 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="f0b60-296">Hallo-opdracht uitvoeren met behulp van **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="f0b60-296">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="f0b60-297">Hallo resultaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="f0b60-297">View hello results.</span></span> <span data-ttu-id="f0b60-298">Als Hallo gegevensset is gemaakt, ziet u Hallo JSON voor de gegevensset in Hallo Hallo **resultaten**; anders wordt een foutbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f0b60-298">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="f0b60-299">Uitvoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="f0b60-299">Create output dataset</span></span>
<span data-ttu-id="f0b60-300">Hello Azure SQL Database gekoppeld-service geeft Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op de runtime tooconnect tooyour Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="f0b60-300">hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="f0b60-301">Hallo SQL tabel uitvoergegevensset (OututDataset) in deze stap hebt u Hiermee geeft u Hallo-tabel in Hallo toowhich Hallo databasegegevens van Hallo blob-opslag is gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="f0b60-301">hello output SQL table dataset (OututDataset) you create in this step specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

1. <span data-ttu-id="f0b60-302">Hallo opdracht toovariable met de naam toewijzen **cmd**.</span><span class="sxs-lookup"><span data-stu-id="f0b60-302">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="f0b60-303">Hallo-opdracht uitvoeren met behulp van **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="f0b60-303">Run hello command by using **Invoke-Command**.</span></span>
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="f0b60-304">Hallo resultaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="f0b60-304">View hello results.</span></span> <span data-ttu-id="f0b60-305">Als Hallo gegevensset is gemaakt, ziet u Hallo JSON voor de gegevensset in Hallo Hallo **resultaten**; anders wordt een foutbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f0b60-305">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a><span data-ttu-id="f0b60-306">Pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="f0b60-306">Create pipeline</span></span>
<span data-ttu-id="f0b60-307">In deze stap maakt u een pijplijn met een **kopieeractiviteit** die gebruikmaakt van **AzureBlobInput** als invoer en **AzureSqlOutput** als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="f0b60-307">In this step, you create a pipeline with a **copy activity** that uses **AzureBlobInput** as an input and **AzureSqlOutput** as an output.</span></span>

<span data-ttu-id="f0b60-308">Uitvoergegevensset is momenteel welke stations Hallo planning.</span><span class="sxs-lookup"><span data-stu-id="f0b60-308">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="f0b60-309">In deze zelfstudie is uitvoergegevensset geconfigureerde tooproduce een segment eens per uur.</span><span class="sxs-lookup"><span data-stu-id="f0b60-309">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="f0b60-310">Hallo pijplijn heeft een begintijd en eindtijd die één dag uit elkaar liggen, wat is 24 uur zijn.</span><span class="sxs-lookup"><span data-stu-id="f0b60-310">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="f0b60-311">Daarom worden 24 segmenten van uitvoergegevensset geproduceerd door Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="f0b60-311">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="f0b60-312">Hallo opdracht toovariable met de naam toewijzen **cmd**.</span><span class="sxs-lookup"><span data-stu-id="f0b60-312">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="f0b60-313">Hallo-opdracht uitvoeren met behulp van **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="f0b60-313">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="f0b60-314">Hallo resultaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="f0b60-314">View hello results.</span></span> <span data-ttu-id="f0b60-315">Als Hallo gegevensset is gemaakt, ziet u Hallo JSON voor de gegevensset in Hallo Hallo **resultaten**; anders wordt een foutbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f0b60-315">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>  

    ```PowerShell   
    Write-Host $results
    ```

<span data-ttu-id="f0b60-316">**Gefeliciteerd!**</span><span class="sxs-lookup"><span data-stu-id="f0b60-316">**Congratulations!**</span></span> <span data-ttu-id="f0b60-317">U hebt een Azure-gegevensfactory, met een pijplijn waarmee gegevens worden gekopieerd uit Azure Blob Storage tooAzure SQL-database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f0b60-317">You have successfully created an Azure data factory, with a pipeline that copies data from Azure Blob Storage tooAzure SQL database.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="f0b60-318">De pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="f0b60-318">Monitor pipeline</span></span>
<span data-ttu-id="f0b60-319">In deze stap gebruikt u REST API van Data Factory toomonitor segmenten wordt geproduceerd door Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="f0b60-319">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> <span data-ttu-id="f0b60-320">Zorg ervoor dat Hallo begin- en tijden opgegeven in de Hallo na overeen Hallo start opdracht en van Hallo pijplijn eindtijden.</span><span class="sxs-lookup"><span data-stu-id="f0b60-320">Make sure that hello start and end times specified in hello following command match hello start and end times of hello pipeline.</span></span> 

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

<span data-ttu-id="f0b60-321">Hallo Invoke-Command en uitgevoerd Hallo volgende totdat er een segment in **gereed** status of **mislukt** status.</span><span class="sxs-lookup"><span data-stu-id="f0b60-321">Run hello Invoke-Command and hello next one until you see a slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="f0b60-322">Als Hallo segment status gereed is, Controleer Hallo **emp** tabel in uw Azure SQL database voor de uitvoergegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="f0b60-322">When hello slice is in Ready state, check hello **emp** table in your Azure SQL database for hello output data.</span></span> 

<span data-ttu-id="f0b60-323">Voor elk segment zijn twee rijen met gegevens uit het bronbestand Hallo gekopieerde toohello emp-tabel in hello Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="f0b60-323">For each slice, two rows of data from hello source file are copied toohello emp table in hello Azure SQL database.</span></span> <span data-ttu-id="f0b60-324">U ziet daarom 24 nieuwe records in Hallo emp-tabel wanneer alle Hallo segmenten worden verwerkt (in de status Ready heeft).</span><span class="sxs-lookup"><span data-stu-id="f0b60-324">Therefore, you see 24 new records in hello emp table when all hello slices are successfully processed (in Ready state).</span></span> 

## <a name="summary"></a><span data-ttu-id="f0b60-325">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="f0b60-325">Summary</span></span>
<span data-ttu-id="f0b60-326">In deze zelfstudie gebruikt u REST-API toocreate een Azure data factory toocopy gegevens uit een Azure-blobopslag tooan Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="f0b60-326">In this tutorial, you used REST API toocreate an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="f0b60-327">Hier volgen Hallo hoofdstappen die u in deze zelfstudie hebt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="f0b60-327">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="f0b60-328">U hebt een Azure-**gegevensfactory** gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f0b60-328">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="f0b60-329">U hebt **gekoppelde services** gemaakt:</span><span class="sxs-lookup"><span data-stu-id="f0b60-329">Created **linked services**:</span></span>
   1. <span data-ttu-id="f0b60-330">Een Azure Storage gekoppelde service toolink uw Azure Storage-account dat invoergegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="f0b60-330">An Azure Storage linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="f0b60-331">Een Azure SQL gekoppelde service toolink uw Azure SQL-database die uitvoergegevens Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="f0b60-331">An Azure SQL linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="f0b60-332">U hebt **gegevenssets** gemaakt waarin de invoer- en uitvoergegevens van pijplijnen worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="f0b60-332">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="f0b60-333">U hebt een **pijplijn** gemaakt met een kopieeractiviteit met BlobSource als bron en SqlSink als sink.</span><span class="sxs-lookup"><span data-stu-id="f0b60-333">Created a **pipeline** with a Copy Activity with BlobSource as source and SqlSink as sink.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f0b60-334">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f0b60-334">Next steps</span></span>
<span data-ttu-id="f0b60-335">In deze zelfstudie hebt u voor een kopieerbewerking een Azure Blob-opslag gebruikt als brongegevensarchief en een Azure SQL-database als doelgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="f0b60-335">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="f0b60-336">Hallo bevat volgende tabel een lijst met gegevensarchieven als bronnen en bestemmingen wordt ondersteund door Hallo kopieeractiviteit:</span><span class="sxs-lookup"><span data-stu-id="f0b60-336">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="f0b60-337">toolearn over hoe gegevens uit een data toocopy opslaan, klikt u op Hallo-koppeling voor de gegevensopslag Hallo in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="f0b60-337">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
