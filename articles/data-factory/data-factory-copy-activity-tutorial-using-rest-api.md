---
title: 'Zelfstudie: REST-API gebruiken voor het maken van een Azure Data Factory-pijplijn | Microsoft Docs'
description: "In deze zelfstudie gebruikt u REST API om een Azure Data Factory-pijplijn te maken met een kopieeractiviteit om gegevens uit een Azure-blobopslag naar een Azure SQL-database te kopiëren."
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
ms.openlocfilehash: 6663774497aa18aa98e7e8c5aed6183c599b2172
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-use-rest-api-to-create-an-azure-data-factory-pipeline-to-copy-data"></a><span data-ttu-id="4d641-103">Zelfstudie: REST-API gebruiken voor het maken van een Azure Data Factory-pijplijn</span><span class="sxs-lookup"><span data-stu-id="4d641-103">Tutorial: Use REST API to create an Azure Data Factory pipeline to copy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4d641-104">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="4d641-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="4d641-105">De wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="4d641-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="4d641-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4d641-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="4d641-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4d641-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="4d641-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d641-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="4d641-109">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="4d641-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="4d641-110">REST API</span><span class="sxs-lookup"><span data-stu-id="4d641-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="4d641-111">.NET-API</span><span class="sxs-lookup"><span data-stu-id="4d641-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="4d641-112">In dit artikel leert u hoe u REST API kunt gebruiken om een gegevensfactory te maken met een pijplijn waarmee gegevens worden gekopieerd van een Azure blobopslag naar een Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="4d641-112">In this article, you learn how to use REST API to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="4d641-113">Als u niet bekend bent met Azure Data Factory, lees dan het artikel [Inleiding tot Azure Data Factory](data-factory-introduction.md) voordat u deze zelfstudie volgt.</span><span class="sxs-lookup"><span data-stu-id="4d641-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="4d641-114">In deze zelfstudie maakt u een pijplijn met één activiteit erin: kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="4d641-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="4d641-115">De kopieeractiviteit in Data Factory kopieert gegevens uit een ondersteund gegevensarchief naar een ondersteund sinkgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="4d641-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="4d641-116">Zie [Ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met gegevensarchieven die worden ondersteund als bron en als sink.</span><span class="sxs-lookup"><span data-stu-id="4d641-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="4d641-117">De activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens veilig, betrouwbaar en schaalbaar kunnen worden gekopieerd tussen verschillende gegevensarchieven.</span><span class="sxs-lookup"><span data-stu-id="4d641-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="4d641-118">Zie het artikel [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie over kopieeractiviteiten.</span><span class="sxs-lookup"><span data-stu-id="4d641-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="4d641-119">Een pijplijn kan meer dan één activiteit hebben.</span><span class="sxs-lookup"><span data-stu-id="4d641-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="4d641-120">Ook kunt u twee activiteiten koppelen (de ene activiteit na de andere laten uitvoeren) door de uitvoergegevensset van één activiteit in te stellen als invoergegevensset voor een andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="4d641-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="4d641-121">Zie [Meerdere activiteiten in een pijplijn](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4d641-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="4d641-122">Dit artikel omvat niet alle Data Factory-REST API.</span><span class="sxs-lookup"><span data-stu-id="4d641-122">This article does not cover all the Data Factory REST API.</span></span> <span data-ttu-id="4d641-123">Zie [Naslaginformatie voor Data Factory-REST API](/rest/api/datafactory/) voor uitgebreide documentatie over Data Factory-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="4d641-123">See [Data Factory REST API Reference](/rest/api/datafactory/) for comprehensive documentation on Data Factory cmdlets.</span></span>
>  
> <span data-ttu-id="4d641-124">In de gegevenspijplijn in deze zelfstudie worden gegevens van een brongegevensarchief gekopieerd naar een doelgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="4d641-124">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="4d641-125">Zie [Zelfstudie: een pijplijn maken om gegevens te transformeren met een Hadoop-cluster](data-factory-build-your-first-pipeline.md) voor meer informatie over het transformeren van gegevens met Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4d641-125">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d641-126">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4d641-126">Prerequisites</span></span>
* <span data-ttu-id="4d641-127">Neem het artikel [Overzicht van de zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) door en voer de **vereiste** stappen uit.</span><span class="sxs-lookup"><span data-stu-id="4d641-127">Go through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="4d641-128">Installeer [Curl](https://curl.haxx.se/dlwiz/) op uw computer.</span><span class="sxs-lookup"><span data-stu-id="4d641-128">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="4d641-129">U kunt in het hulpprogramma Curl REST-opdrachten gebruiken om een gegevensfactory te maken.</span><span class="sxs-lookup"><span data-stu-id="4d641-129">You use the Curl tool with REST commands to create a data factory.</span></span> 
* <span data-ttu-id="4d641-130">Volg de instructies in [dit artikel](../azure-resource-manager/resource-group-create-service-principal-portal.md) voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="4d641-130">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span> 
  1. <span data-ttu-id="4d641-131">Maak een webtoepassing met de naam **ADFCopyTutorialApp** in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4d641-131">Create a Web application named **ADFCopyTutorialApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="4d641-132">Haal de **client-id** en **geheime sleutel** op.</span><span class="sxs-lookup"><span data-stu-id="4d641-132">Get **client ID** and **secret key**.</span></span> 
  3. <span data-ttu-id="4d641-133">Haal de **tenant-id** op.</span><span class="sxs-lookup"><span data-stu-id="4d641-133">Get **tenant ID**.</span></span> 
  4. <span data-ttu-id="4d641-134">Wijs de toepassing **ADFCopyTutorialApp** toe aan de rol **Inzender Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="4d641-134">Assign the **ADFCopyTutorialApp** application to the **Data Factory Contributor** role.</span></span>  
* <span data-ttu-id="4d641-135">Installeer [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4d641-135">Install [Azure PowerShell](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="4d641-136">Start **PowerShell** en voer de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="4d641-136">Launch **PowerShell** and do the following steps.</span></span> <span data-ttu-id="4d641-137">Houd Azure PowerShell open tot het einde van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="4d641-137">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="4d641-138">Als u het programma sluit en opnieuw opent, moet u de opdrachten opnieuw uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4d641-138">If you close and reopen, you need to run the commands again.</span></span>
  
  1. <span data-ttu-id="4d641-139">Voer de volgende opdracht uit en geef de gebruikersnaam en het wachtwoord op waarmee u zich aanmeldt bij Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="4d641-139">Run the following command and enter the user name and password that you use to sign in to the Azure portal:</span></span>
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. <span data-ttu-id="4d641-140">Voer de volgende opdracht uit om alle abonnementen voor dit account weer te geven:</span><span class="sxs-lookup"><span data-stu-id="4d641-140">Run the following command to view all the subscriptions for this account:</span></span>

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. <span data-ttu-id="4d641-141">Voer de volgende opdracht uit om het abonnement te selecteren waarmee u wilt werken.</span><span class="sxs-lookup"><span data-stu-id="4d641-141">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="4d641-142">Vervang **&lt;NameOfAzureSubscription**&gt; door de naam van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="4d641-142">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span> 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. <span data-ttu-id="4d641-143">Maak een Azure-resourcegroep met de naam **ADFTutorialResourceGroup** door de volgende opdracht uit te voeren in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4d641-143">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell:</span></span>  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      <span data-ttu-id="4d641-144">Als de resourcegroep al bestaat, geeft u aan of u deze wilt bijwerken (Y) of ongewijzigd wilt laten (N).</span><span class="sxs-lookup"><span data-stu-id="4d641-144">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span> 
     
      <span data-ttu-id="4d641-145">Voor sommige van de stappen in deze zelfstudie wordt ervan uitgegaan dat u de resourcegroep met de naam ADFTutorialResourceGroup gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4d641-145">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="4d641-146">Als u een andere resourcegroep gebruikt, moet u voor deze zelfstudie de naam van uw resourcegroep gebruiken in plaats van ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="4d641-146">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="4d641-147">JSON-definities maken</span><span class="sxs-lookup"><span data-stu-id="4d641-147">Create JSON definitions</span></span>
<span data-ttu-id="4d641-148">Maak de volgende JSON-bestanden in de map waar curl.exe staat.</span><span class="sxs-lookup"><span data-stu-id="4d641-148">Create following JSON files in the folder where curl.exe is located.</span></span> 

### <a name="datafactoryjson"></a><span data-ttu-id="4d641-149">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="4d641-149">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4d641-150">Naam moet uniek zijn, dus het is raadzaam om voor- en/of achtervoegsels te gebruiken bij ADFCopyTutorialDF, zodat het een unieke naam wordt.</span><span class="sxs-lookup"><span data-stu-id="4d641-150">Name must be globally unique, so you may want to prefix/suffix ADFCopyTutorialDF to make it a unique name.</span></span> 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="4d641-151">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="4d641-151">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4d641-152">Vervang **accountname** en **accountkey** door de naam en sleutel van uw Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="4d641-152">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="4d641-153">Zie [Toegangssleutels voor opslag weergeven, kopiëren en opnieuw genereren](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys) voor meer informatie over het verkrijgen van uw toegangssleutel voor opslag.</span><span class="sxs-lookup"><span data-stu-id="4d641-153">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>

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

<span data-ttu-id="4d641-154">Zie [Gekoppelde Azure Storage-service](data-factory-azure-blob-connector.md#azure-storage-linked-service) voor meer informatie over de JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="4d641-154">For details about JSON properties, see [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span></span>

### <a name="azuersqllinkedservicejson"></a><span data-ttu-id="4d641-155">azuersqllinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="4d641-155">azuersqllinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4d641-156">Vervang **servername**, **databasename**, **username** en **password** door de naam van uw Azure SQL-server, de naam van de SQL-database, het gebruikersaccount en het wachtwoord van het account.</span><span class="sxs-lookup"><span data-stu-id="4d641-156">Replace **servername**, **databasename**, **username**, and **password** with name of your Azure SQL server, name of SQL database, user account, and password for the account.</span></span>  
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

<span data-ttu-id="4d641-157">Zie [Gekoppelde Azure SQL-service](data-factory-azure-sql-connector.md#linked-service-properties) voor meer informatie over de JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="4d641-157">For details about JSON properties, see [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="4d641-158">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="4d641-158">inputdataset.json</span></span>

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

<span data-ttu-id="4d641-159">De volgende tabel bevat beschrijvingen van de JSON-eigenschappen die in het codefragment worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="4d641-159">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="4d641-160">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4d641-160">Property</span></span> | <span data-ttu-id="4d641-161">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4d641-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4d641-162">type</span><span class="sxs-lookup"><span data-stu-id="4d641-162">type</span></span> | <span data-ttu-id="4d641-163">De eigenschap type wordt ingesteld op **AzureBlob**, omdat de gegevens zich in een Azure-blobopslag bevinden.</span><span class="sxs-lookup"><span data-stu-id="4d641-163">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
| <span data-ttu-id="4d641-164">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="4d641-164">linkedServiceName</span></span> | <span data-ttu-id="4d641-165">Deze eigenschap verwijst naar de **AzureStorageLinkedService** die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4d641-165">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="4d641-166">folderPath</span><span class="sxs-lookup"><span data-stu-id="4d641-166">folderPath</span></span> | <span data-ttu-id="4d641-167">Deze eigenschap verwijst naar de blob**container** en de **map** die de blobs voor invoer bevat.</span><span class="sxs-lookup"><span data-stu-id="4d641-167">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="4d641-168">In deze zelfstudie is adftutorial de blobcontainer en is folder de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="4d641-168">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
| <span data-ttu-id="4d641-169">fileName</span><span class="sxs-lookup"><span data-stu-id="4d641-169">fileName</span></span> | <span data-ttu-id="4d641-170">Deze eigenschap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="4d641-170">This property is optional.</span></span> <span data-ttu-id="4d641-171">Als u deze eigenschap niet opgeeft, worden alle bestanden uit folderPath gekozen.</span><span class="sxs-lookup"><span data-stu-id="4d641-171">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="4d641-172">In deze zelfstudie wordt **emp.txt** opgegeven voor de fileName, zodat alleen dat bestand wordt opgehaald voor de verwerking.</span><span class="sxs-lookup"><span data-stu-id="4d641-172">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
| <span data-ttu-id="4d641-173">format -> type</span><span class="sxs-lookup"><span data-stu-id="4d641-173">format -> type</span></span> |<span data-ttu-id="4d641-174">Het invoerbestand is in de tekstindeling, zodat we **TextFormat** gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4d641-174">The input file is in the text format, so we use **TextFormat**.</span></span> |
| <span data-ttu-id="4d641-175">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="4d641-175">columnDelimiter</span></span> | <span data-ttu-id="4d641-176">De kolommen in het invoerbestand worden gescheiden door een **komma (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="4d641-176">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
| <span data-ttu-id="4d641-177">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="4d641-177">frequency/interval</span></span> | <span data-ttu-id="4d641-178">Als frequency wordt ingesteld op **Hour** en het interval wordt ingesteld op **1**, betekent dit dat de invoersegmenten één keer per **uur** beschikbaar worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4d641-178">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="4d641-179">Met andere woorden, de Data Factory-service zoekt elk uur naar invoergegevens in de hoofdmap van de opgegeven blobcontainer (**adftutorial**).</span><span class="sxs-lookup"><span data-stu-id="4d641-179">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="4d641-180">Er wordt gezocht naar gegevens binnen de begin- en eindtijd van de pijplijn, niet voor of na deze tijden.</span><span class="sxs-lookup"><span data-stu-id="4d641-180">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
| <span data-ttu-id="4d641-181">external</span><span class="sxs-lookup"><span data-stu-id="4d641-181">external</span></span> | <span data-ttu-id="4d641-182">Deze eigenschap wordt ingesteld op **true** als de gegevens niet worden gegenereerd door deze pijplijn.</span><span class="sxs-lookup"><span data-stu-id="4d641-182">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="4d641-183">De invoergegevens in deze zelfstudie bevinden zich in het bestand emp.txt, dat niet wordt gegenereerd door deze pijplijn. Daarom stellen we deze eigenschap in op true.</span><span class="sxs-lookup"><span data-stu-id="4d641-183">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

<span data-ttu-id="4d641-184">Zie het [artikel over Azure Blob-connectoren](data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over deze JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="4d641-184">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>

### <a name="outputdatasetjson"></a><span data-ttu-id="4d641-185">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="4d641-185">outputdataset.json</span></span>

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
<span data-ttu-id="4d641-186">De volgende tabel bevat beschrijvingen van de JSON-eigenschappen die in het codefragment worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="4d641-186">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="4d641-187">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4d641-187">Property</span></span> | <span data-ttu-id="4d641-188">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4d641-188">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4d641-189">type</span><span class="sxs-lookup"><span data-stu-id="4d641-189">type</span></span> | <span data-ttu-id="4d641-190">De eigenschap type wordt ingesteld op **AzureSqlTable** omdat gegevens naar een tabel in een Azure SQL-database worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="4d641-190">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
| <span data-ttu-id="4d641-191">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="4d641-191">linkedServiceName</span></span> | <span data-ttu-id="4d641-192">Deze eigenschap verwijst naar de **AzureSqlLinkedService** die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4d641-192">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="4d641-193">tableName</span><span class="sxs-lookup"><span data-stu-id="4d641-193">tableName</span></span> | <span data-ttu-id="4d641-194">Geeft de **tabel** aan waarnaar de gegevens worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="4d641-194">Specified the **table** to which the data is copied.</span></span> | 
| <span data-ttu-id="4d641-195">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="4d641-195">frequency/interval</span></span> | <span data-ttu-id="4d641-196">De frequentie is ingesteld op **Hour** en het interval is **1**, wat betekent dat de uitvoersegmenten worden geproduceerd **per uur** tussen de begin- en eindtijd van de pijplijn, niet voor of na deze tijden.</span><span class="sxs-lookup"><span data-stu-id="4d641-196">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

<span data-ttu-id="4d641-197">De tabel emp in de database bevat drie kolommen: **ID**, **FirstName** en **LastName**.</span><span class="sxs-lookup"><span data-stu-id="4d641-197">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="4d641-198">ID is een identiteitskolom, zodat u alleen **FirstName** en **LastName** hoeft op te geven.</span><span class="sxs-lookup"><span data-stu-id="4d641-198">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

<span data-ttu-id="4d641-199">Zie het [artikel over Azure SQL-connectoren](data-factory-azure-sql-connector.md#dataset-properties) voor meer informatie over deze JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="4d641-199">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="4d641-200">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="4d641-200">pipeline.json</span></span>

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob to Azure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data to Azure SQL database",
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

<span data-ttu-id="4d641-201">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="4d641-201">Note the following points:</span></span>

- <span data-ttu-id="4d641-202">In het gedeelte Activiteiten is er slechts één activiteit waarvan **type** is ingesteld op **Copy**.</span><span class="sxs-lookup"><span data-stu-id="4d641-202">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="4d641-203">Zie het artikel [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie over kopieeractiviteiten.</span><span class="sxs-lookup"><span data-stu-id="4d641-203">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="4d641-204">In Data Factory-oplossingen kunt u ook [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4d641-204">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
- <span data-ttu-id="4d641-205">De invoer voor de activiteit is ingesteld op **AzureBlobInput** en de uitvoer voor de activiteit is ingesteld op **AzureSqlOutput**.</span><span class="sxs-lookup"><span data-stu-id="4d641-205">Input for the activity is set to **AzureBlobInput** and output for the activity is set to **AzureSqlOutput**.</span></span> 
- <span data-ttu-id="4d641-206">In het gedeelte **typeProperties** is **BlobSource** opgegeven als het brontype en **SqlSink** als het sink-type.</span><span class="sxs-lookup"><span data-stu-id="4d641-206">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="4d641-207">Zie [Ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een volledige lijst van gegevensarchieven die worden ondersteund door kopieeractiviteiten als bronnen en sinks.</span><span class="sxs-lookup"><span data-stu-id="4d641-207">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="4d641-208">Klik op de koppeling in de tabel voor informatie over het gebruik van een specifiek ondersteund gegevensarchief als een bron/sink.</span><span class="sxs-lookup"><span data-stu-id="4d641-208">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
 
<span data-ttu-id="4d641-209">Vervang de waarde van de eigenschap **start** door de huidige dag en de waarde **end** door de volgende dag.</span><span class="sxs-lookup"><span data-stu-id="4d641-209">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="4d641-210">U hoeft alleen de datum in te vullen en kunt de tijd overslaan.</span><span class="sxs-lookup"><span data-stu-id="4d641-210">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="4d641-211">Dit wordt dan bijvoorbeeld 2017-02-03, wat gelijk staat aan 2017-02-03T00:00:00Z</span><span class="sxs-lookup"><span data-stu-id="4d641-211">For example, "2017-02-03", which is equivalent to "2017-02-03T00:00:00Z"</span></span>
 
<span data-ttu-id="4d641-212">Zowel de begin- als einddatum en -tijd moeten de [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601) hebben.</span><span class="sxs-lookup"><span data-stu-id="4d641-212">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="4d641-213">Bijvoorbeeld: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="4d641-213">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="4d641-214">De **eindtijd** is optioneel, maar we gebruiken hem in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="4d641-214">The **end** time is optional, but we use it in this tutorial.</span></span> 
 
<span data-ttu-id="4d641-215">Als u geen waarde opgeeft voor de eigenschap **end**, wordt automatisch **start + 48 uur** gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4d641-215">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="4d641-216">Als u de pijplijn voor onbepaalde tijd wilt uitvoeren, geeft u **9999-09-09** op als waarde voor de eigenschap **end**.</span><span class="sxs-lookup"><span data-stu-id="4d641-216">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
 
<span data-ttu-id="4d641-217">In het voorgaande voorbeeld zijn er 24 gegevenssegmenten omdat er elk uur één gegevenssegment wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4d641-217">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

<span data-ttu-id="4d641-218">Zie het artikel [Pijplijnen maken](data-factory-create-pipelines.md) voor beschrijvingen van JSON-eigenschappen in de definitie van een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="4d641-218">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="4d641-219">Zie [Gegevensverplaatsingsactiviteiten](data-factory-data-movement-activities.md) voor beschrijvingen van JSON-eigenschappen in de definitie van een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="4d641-219">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="4d641-220">Zie het [artikel over Azure Blob-connectoren](data-factory-azure-blob-connector.md) voor beschrijvingen van JSON-eigenschappen die worden ondersteund door BlobSource.</span><span class="sxs-lookup"><span data-stu-id="4d641-220">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="4d641-221">Zie het [artikel over Azure SQL Database-connectoren](data-factory-azure-sql-connector.md) voor beschrijvingen van JSON-eigenschappen die worden ondersteund door SqlSink.</span><span class="sxs-lookup"><span data-stu-id="4d641-221">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="set-global-variables"></a><span data-ttu-id="4d641-222">Globale variabelen instellen</span><span class="sxs-lookup"><span data-stu-id="4d641-222">Set global variables</span></span>
<span data-ttu-id="4d641-223">Voer in Azure PowerShell de volgende opdrachten uit nadat u de waarden hebt vervangen door uw eigen waarden:</span><span class="sxs-lookup"><span data-stu-id="4d641-223">In Azure PowerShell, execute the following commands after replacing the values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d641-224">Zie de sectie [Vereisten](#prerequisites) voor instructies over het verkrijgen van de client-id, het clientgeheim, de tenant-id en de abonnements-id.</span><span class="sxs-lookup"><span data-stu-id="4d641-224">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

<span data-ttu-id="4d641-225">Voer de volgende opdracht uit na het bijwerken van de naam van de gegevensfactory die u gebruikt:</span><span class="sxs-lookup"><span data-stu-id="4d641-225">Run the following command after updating the name of the data factory you are using:</span></span> 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a><span data-ttu-id="4d641-226">Verifiëren met AAD</span><span class="sxs-lookup"><span data-stu-id="4d641-226">Authenticate with AAD</span></span>
<span data-ttu-id="4d641-227">Voer de volgende opdracht uit om te verifiëren met Azure Active Directory (AAD):</span><span class="sxs-lookup"><span data-stu-id="4d641-227">Run the following command to authenticate with Azure Active Directory (AAD):</span></span> 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a><span data-ttu-id="4d641-228">Een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="4d641-228">Create data factory</span></span>
<span data-ttu-id="4d641-229">In deze stap maakt u een Azure-gegevensfactory met de naam **ADFCopyTutorialDF**.</span><span class="sxs-lookup"><span data-stu-id="4d641-229">In this step, you create an Azure Data Factory named **ADFCopyTutorialDF**.</span></span> <span data-ttu-id="4d641-230">Een gegevensfactory kan één of meer pijplijnen hebben.</span><span class="sxs-lookup"><span data-stu-id="4d641-230">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="4d641-231">Een pijplijn kan één of meer activiteiten bevatten.</span><span class="sxs-lookup"><span data-stu-id="4d641-231">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="4d641-232">Bijvoorbeeld een kopieeractiviteit om gegevens te kopiëren van een brongegevensarchief naar een doelgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="4d641-232">For example, a Copy Activity to copy data from a source to a destination data store.</span></span> <span data-ttu-id="4d641-233">Een HDInsight Hive-activiteit om een Hive-script uit te voeren dat invoergegevens omzet in productuitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="4d641-233">A HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="4d641-234">Voer de volgende opdracht uit om de gegevensfactory te maken:</span><span class="sxs-lookup"><span data-stu-id="4d641-234">Run the following commands to create the data factory:</span></span> 

1. <span data-ttu-id="4d641-235">Wijs de opdracht toe aan de variabele met de naam **cmd**.</span><span class="sxs-lookup"><span data-stu-id="4d641-235">Assign the command to variable named **cmd**.</span></span> 
   
    > [!IMPORTANT]
    > <span data-ttu-id="4d641-236">Bevestig dat de naam van de gegevensfactory die u hier opgeeft (ADFCopyTutorialDF) overeenkomt met de naam die is opgegeven in de **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="4d641-236">Confirm that the name of the data factory you specify here (ADFCopyTutorialDF) matches the name specified in the **datafactory.json**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. <span data-ttu-id="4d641-237">Voer de opdracht uit via **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="4d641-237">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="4d641-238">Bekijk de resultaten.</span><span class="sxs-lookup"><span data-stu-id="4d641-238">View the results.</span></span> <span data-ttu-id="4d641-239">Als de gegevensfactory is gemaakt, ziet u de JSON voor de gegevensfactory in de **resultaten**. Anders wordt er een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4d641-239">If the data factory has been successfully created, you see the JSON for the data factory in the **results**; otherwise, you see an error message.</span></span>  
   
    ```
    Write-Host $results
    ```

<span data-ttu-id="4d641-240">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="4d641-240">Note the following points:</span></span>

* <span data-ttu-id="4d641-241">De naam van de Azure-gegevensfactory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="4d641-241">The name of the Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="4d641-242">Als u deze fout ziet in de resultaten: **Naam gegevensfactory 'ADFCopyTutorialDF' is niet beschikbaar**, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="4d641-242">If you see the error in results: **Data factory name “ADFCopyTutorialDF” is not available**, do the following steps:</span></span>  
  
  1. <span data-ttu-id="4d641-243">Wijzig de naam (bijvoorbeeld uwnaamADFCopyTutorialDF) in het **datafactory.json**-bestand.</span><span class="sxs-lookup"><span data-stu-id="4d641-243">Change the name (for example, yournameADFCopyTutorialDF) in the **datafactory.json** file.</span></span>
  2. <span data-ttu-id="4d641-244">In de eerste opdracht waar de **$cmd**-variabele een waarde is toegewezen, vervangt u ADFCopyTutorialDF door de nieuwe naam en voert u de opdracht uit.</span><span class="sxs-lookup"><span data-stu-id="4d641-244">In the first command where the **$cmd** variable is assigned a value, replace ADFCopyTutorialDF with the new name and run the command.</span></span> 
  3. <span data-ttu-id="4d641-245">Voer de volgende twee opdrachten uit voor het aanroepen van de REST API om de gegevensfactory te maken en de resultaten van de bewerking af te drukken.</span><span class="sxs-lookup"><span data-stu-id="4d641-245">Run the next two commands to invoke the REST API to create the data factory and print the results of the operation.</span></span> 
     
     <span data-ttu-id="4d641-246">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="4d641-246">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="4d641-247">Als u Data Factory-exemplaren wilt maken, moet u bijdrager/beheerder zijn van het Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="4d641-247">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span></span>
* <span data-ttu-id="4d641-248">De naam van de gegevensfactory wordt in de toekomst mogelijk geregistreerd als DNS-naam en wordt daarmee ook voor iedereen zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="4d641-248">The name of the data factory may be registered as a DNS name in the future and hence become publicly visible.</span></span>
* <span data-ttu-id="4d641-249">Als u de foutmelding **Dit abonnement is niet geregistreerd voor gebruik van de naamruimte Microsoft.DataFactory** ontvangt, voert u een van de volgende stappen uit en probeert u opnieuw te publiceren:</span><span class="sxs-lookup"><span data-stu-id="4d641-249">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span></span> 
  
  * <span data-ttu-id="4d641-250">Voer in Azure PowerShell de volgende opdracht uit om de Data Factory-provider te registreren:</span><span class="sxs-lookup"><span data-stu-id="4d641-250">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="4d641-251">U kunt de volgende opdracht uitvoeren om te bevestigen dat de Data Factory-provider is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="4d641-251">You can run the following command to confirm that the Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="4d641-252">Meld u bij de [Azure Portal](https://portal.azure.com) aan met behulp van het Azure-abonnement en navigeer naar een Data Factory-blade of maak een gegevensfactory in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4d641-252">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="4d641-253">Door deze actie wordt de provider automatisch voor u geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="4d641-253">This action automatically registers the provider for you.</span></span>

<span data-ttu-id="4d641-254">Voordat u een pijplijn maakt, moet u eerst enkele Data Factory-entiteiten maken.</span><span class="sxs-lookup"><span data-stu-id="4d641-254">Before creating a pipeline, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="4d641-255">U maakt eerst gekoppelde services om de bron- en doelgegevensarchieven te koppelen aan uw gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="4d641-255">You first create linked services to link source and destination data stores to your data store.</span></span> <span data-ttu-id="4d641-256">Vervolgens definieert u in- en uitvoergegevenssets die de gegevens in de gekoppelde gegevensarchieven vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="4d641-256">Then, define input and output datasets to represent data in linked data stores.</span></span> <span data-ttu-id="4d641-257">Ten slotte maakt u de pijplijn met een activiteit die deze gegevenssets gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4d641-257">Finally, create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="4d641-258">Gekoppelde services maken</span><span class="sxs-lookup"><span data-stu-id="4d641-258">Create linked services</span></span>
<span data-ttu-id="4d641-259">U maakt gekoppelde services in een gegevensfactory om uw gegevensarchieven en compute-services aan de gegevensfactory te koppelen.</span><span class="sxs-lookup"><span data-stu-id="4d641-259">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="4d641-260">In deze zelfstudie gebruikt u niet een willekeurige compute-service, zoals Azure HDInsight of Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4d641-260">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="4d641-261">U gebruikt twee gegevensarchieven van het type Azure Storage (bron) en Azure SQL Database (doel).</span><span class="sxs-lookup"><span data-stu-id="4d641-261">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> <span data-ttu-id="4d641-262">Daarom maakt u twee gekoppelde services met de naam AzureStorageLinkedService en AzureSqlLinkedService van het type: AzureStorage en AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="4d641-262">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="4d641-263">De AzureStorageLinkedService koppelt uw Azure-opslagaccount aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="4d641-263">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="4d641-264">Dit opslagaccount is het account waarin u een container hebt gemaakt en gegevens hebt geüpload als onderdeel van de [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="4d641-264">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="4d641-265">De AzureSqlLinkedService koppelt uw Azure SQL-database aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="4d641-265">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="4d641-266">De gegevens die worden gekopieerd uit de blobopslag worden opgeslagen in deze database.</span><span class="sxs-lookup"><span data-stu-id="4d641-266">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="4d641-267">Als onderdeel van de [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) hebt u de emp-tabel in deze database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4d641-267">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="4d641-268">Een gekoppelde Azure Storage-service maken</span><span class="sxs-lookup"><span data-stu-id="4d641-268">Create Azure Storage linked service</span></span>
<span data-ttu-id="4d641-269">In deze stap koppelt u uw Azure Storage-account aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="4d641-269">In this step, you link your Azure storage account to your data factory.</span></span> <span data-ttu-id="4d641-270">In deze sectie geeft u de naam en sleutel van uw Azure Storage-account op.</span><span class="sxs-lookup"><span data-stu-id="4d641-270">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="4d641-271">Zie [Een gekoppelde Azure Storage-service](data-factory-azure-blob-connector.md#azure-storage-linked-service) voor meer informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van een gekoppelde Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="4d641-271">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span>  

1. <span data-ttu-id="4d641-272">Wijs de opdracht toe aan de variabele met de naam **cmd**.</span><span class="sxs-lookup"><span data-stu-id="4d641-272">Assign the command to variable named **cmd**.</span></span> 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="4d641-273">Voer de opdracht uit via **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="4d641-273">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="4d641-274">Bekijk de resultaten.</span><span class="sxs-lookup"><span data-stu-id="4d641-274">View the results.</span></span> <span data-ttu-id="4d641-275">Als de gekoppelde service is gemaakt, ziet u de JSON voor de gekoppelde service in de **resultaten**. Anders wordt er een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4d641-275">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a><span data-ttu-id="4d641-276">Gekoppelde Azure SQL-service maken</span><span class="sxs-lookup"><span data-stu-id="4d641-276">Create Azure SQL linked service</span></span>
<span data-ttu-id="4d641-277">In deze stap koppelt u uw Azure SQL Database aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="4d641-277">In this step, you link your Azure SQL database to your data factory.</span></span> <span data-ttu-id="4d641-278">U geeft in deze sectie de Azure SQL-servernaam, -databasenaam, -gebruikersnaam en -wachtwoord op.</span><span class="sxs-lookup"><span data-stu-id="4d641-278">You specify the Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="4d641-279">Zie [Een gekoppelde Azure SQL-service](data-factory-azure-sql-connector.md#linked-service-properties) voor meer informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van een gekoppelde Azure SQL-service.</span><span class="sxs-lookup"><span data-stu-id="4d641-279">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used to define an Azure SQL linked service.</span></span>

1. <span data-ttu-id="4d641-280">Wijs de opdracht toe aan de variabele met de naam **cmd**.</span><span class="sxs-lookup"><span data-stu-id="4d641-280">Assign the command to variable named **cmd**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="4d641-281">Voer de opdracht uit via **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="4d641-281">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="4d641-282">Bekijk de resultaten.</span><span class="sxs-lookup"><span data-stu-id="4d641-282">View the results.</span></span> <span data-ttu-id="4d641-283">Als de gekoppelde service is gemaakt, ziet u de JSON voor de gekoppelde service in de **resultaten**. Anders wordt er een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4d641-283">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="4d641-284">Gegevenssets maken</span><span class="sxs-lookup"><span data-stu-id="4d641-284">Create datasets</span></span>
<span data-ttu-id="4d641-285">In de vorige stap hebt u gekoppelde services gemaakt om uw Azure-opslagaccount en Azure SQL-database aan de gegevensfactory te koppelen.</span><span class="sxs-lookup"><span data-stu-id="4d641-285">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="4d641-286">In deze stap definieert u twee gegevenssets, AzureBlobInput en AzureSqlOutput genaamd, die staan voor de invoer- en uitvoergegevens die zijn opgeslagen in de gegevensarchieven waarnaar wordt verwezen door respectievelijk de AzureStorageLinkedService en de AzureSqlLinkedService.</span><span class="sxs-lookup"><span data-stu-id="4d641-286">In this step, you define two datasets named AzureBlobInput and AzureSqlOutput that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="4d641-287">De gekoppelde Azure Storage-service geeft de verbindingsreeks op die de Data Factory-service tijdens runtime gebruikt om verbinding te maken met uw Azure-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="4d641-287">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="4d641-288">En de blobgegevensset voor invoer (AzureBlobInput) geeft de container en de map met de invoergegevens op.</span><span class="sxs-lookup"><span data-stu-id="4d641-288">And, the input blob dataset (AzureBlobInput) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="4d641-289">Op dezelfde manier geeft de gekoppelde Azure SQL Database-service de verbindingsreeks op die de Data Factory-service in runtime gebruikt om verbinding te maken met uw Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="4d641-289">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="4d641-290">En de uitvoergegevensset van de SQL-tabel (OututDataset) geeft de tabel in de database op waarnaar de gegevens uit de blobopslag worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="4d641-290">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="4d641-291">Invoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="4d641-291">Create input dataset</span></span>
<span data-ttu-id="4d641-292">In deze stap maakt u een gegevensset met de naam AzureBlobInput die verwijst naar een blobbestand (emp.txt) in de hoofdmap van een blobcontainer (adftutorial) in Azure Storage. Deze container wordt vertegenwoordigd door de gekoppelde AzureStorageLinkedService-service.</span><span class="sxs-lookup"><span data-stu-id="4d641-292">In this step, you create a dataset named AzureBlobInput that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="4d641-293">Als u geen waarde voor de fileName hebt opgeven (of hebt overgeslagen), worden gegevens uit alle blobs in de invoermap naar het doel gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="4d641-293">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="4d641-294">In deze zelfstudie geeft u een waarde op voor de fileName.</span><span class="sxs-lookup"><span data-stu-id="4d641-294">In this tutorial, you specify a value for the fileName.</span></span> 

1. <span data-ttu-id="4d641-295">Wijs de opdracht toe aan de variabele met de naam **cmd**.</span><span class="sxs-lookup"><span data-stu-id="4d641-295">Assign the command to variable named **cmd**.</span></span> 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="4d641-296">Voer de opdracht uit via **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="4d641-296">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="4d641-297">Bekijk de resultaten.</span><span class="sxs-lookup"><span data-stu-id="4d641-297">View the results.</span></span> <span data-ttu-id="4d641-298">Als de gegevensset is gemaakt, ziet u de JSON voor de gegevensset in de **resultaten**. Anders wordt er een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4d641-298">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="4d641-299">Uitvoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="4d641-299">Create output dataset</span></span>
<span data-ttu-id="4d641-300">De gekoppelde Azure SQL Database-service geeft de verbindingsreeks op die de Data Factory-service in runtime gebruikt om verbinding te maken met uw Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="4d641-300">The Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="4d641-301">De uitvoergegevensset van de SQL-tabel (OututDataset) die u in deze stap hebt gemaakt, geeft de tabel in de database op waarnaar de gegevens uit de blobopslag worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="4d641-301">The output SQL table dataset (OututDataset) you create in this step specifies the table in the database to which the data from the blob storage is copied.</span></span>

1. <span data-ttu-id="4d641-302">Wijs de opdracht toe aan de variabele met de naam **cmd**.</span><span class="sxs-lookup"><span data-stu-id="4d641-302">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="4d641-303">Voer de opdracht uit via **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="4d641-303">Run the command by using **Invoke-Command**.</span></span>
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="4d641-304">Bekijk de resultaten.</span><span class="sxs-lookup"><span data-stu-id="4d641-304">View the results.</span></span> <span data-ttu-id="4d641-305">Als de gegevensset is gemaakt, ziet u de JSON voor de gegevensset in de **resultaten**. Anders wordt er een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4d641-305">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a><span data-ttu-id="4d641-306">Pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="4d641-306">Create pipeline</span></span>
<span data-ttu-id="4d641-307">In deze stap maakt u een pijplijn met een **kopieeractiviteit** die gebruikmaakt van **AzureBlobInput** als invoer en **AzureSqlOutput** als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="4d641-307">In this step, you create a pipeline with a **copy activity** that uses **AzureBlobInput** as an input and **AzureSqlOutput** as an output.</span></span>

<span data-ttu-id="4d641-308">Momenteel is de uitvoergegevensset dat wat de planning aanstuurt.</span><span class="sxs-lookup"><span data-stu-id="4d641-308">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="4d641-309">In deze zelfstudie is de uitvoergegevensset geconfigureerd voor het produceren van een segment eenmaal per uur.</span><span class="sxs-lookup"><span data-stu-id="4d641-309">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="4d641-310">De pijplijn heeft een begintijd en eindtijd die één dag uit elkaar liggen, ofwel 24 uur.</span><span class="sxs-lookup"><span data-stu-id="4d641-310">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="4d641-311">Daarom worden 24 segmenten van de uitvoergegevensset door de pijplijn geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="4d641-311">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 

1. <span data-ttu-id="4d641-312">Wijs de opdracht toe aan de variabele met de naam **cmd**.</span><span class="sxs-lookup"><span data-stu-id="4d641-312">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="4d641-313">Voer de opdracht uit via **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="4d641-313">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="4d641-314">Bekijk de resultaten.</span><span class="sxs-lookup"><span data-stu-id="4d641-314">View the results.</span></span> <span data-ttu-id="4d641-315">Als de gegevensset is gemaakt, ziet u de JSON voor de gegevensset in de **resultaten**. Anders wordt er een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4d641-315">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>  

    ```PowerShell   
    Write-Host $results
    ```

<span data-ttu-id="4d641-316">**Gefeliciteerd!**</span><span class="sxs-lookup"><span data-stu-id="4d641-316">**Congratulations!**</span></span> <span data-ttu-id="4d641-317">U hebt een Azure-gegevensfactory gemaakt met een pijplijn die gegevens van Azure-blobopslag kopieert naar de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="4d641-317">You have successfully created an Azure data factory, with a pipeline that copies data from Azure Blob Storage to Azure SQL database.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="4d641-318">De pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="4d641-318">Monitor pipeline</span></span>
<span data-ttu-id="4d641-319">In deze stap gebruikt u Data Factory-REST API voor het bewaken van segmenten die worden geproduceerd door de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="4d641-319">In this step, you use Data Factory REST API to monitor slices being produced by the pipeline.</span></span>

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> <span data-ttu-id="4d641-320">Controleer of de begin- en eindtijden die zijn opgegeven in de volgende opdracht overeenkomen met de begin- en eindtijden van de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="4d641-320">Make sure that the start and end times specified in the following command match the start and end times of the pipeline.</span></span> 

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

<span data-ttu-id="4d641-321">Voer de Invoke-Command en de volgende uit totdat u het segment in de status **Gereed** of **Mislukt** ziet.</span><span class="sxs-lookup"><span data-stu-id="4d641-321">Run the Invoke-Command and the next one until you see a slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="4d641-322">Als het segment de status Gereed heeft, controleert u de uitvoergegevens in de **emp**-tabel in uw Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="4d641-322">When the slice is in Ready state, check the **emp** table in your Azure SQL database for the output data.</span></span> 

<span data-ttu-id="4d641-323">Voor elk segment worden twee rijen gegevens uit het bronbestand gekopieerd naar de emp-tabel in de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="4d641-323">For each slice, two rows of data from the source file are copied to the emp table in the Azure SQL database.</span></span> <span data-ttu-id="4d641-324">U ziet daarom 24 nieuwe records in de emp-tabel wanneer alle segmenten zijn verwerkt (in de status Gereed).</span><span class="sxs-lookup"><span data-stu-id="4d641-324">Therefore, you see 24 new records in the emp table when all the slices are successfully processed (in Ready state).</span></span> 

## <a name="summary"></a><span data-ttu-id="4d641-325">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="4d641-325">Summary</span></span>
<span data-ttu-id="4d641-326">In deze zelfstudie hebt u REST API gebruikt om een Azure-gegevensfactory te maken voor het kopiëren van gegevens van een Azure-blob naar een Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="4d641-326">In this tutorial, you used REST API to create an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="4d641-327">In deze zelfstudie hebt u de volgende hoofdstappen uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="4d641-327">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="4d641-328">U hebt een Azure-**gegevensfactory** gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4d641-328">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="4d641-329">U hebt **gekoppelde services** gemaakt:</span><span class="sxs-lookup"><span data-stu-id="4d641-329">Created **linked services**:</span></span>
   1. <span data-ttu-id="4d641-330">Een gekoppelde Azure Storage-service om uw Azure Storage-account te koppelen dat invoergegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="4d641-330">An Azure Storage linked service to link your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="4d641-331">Een gekoppelde Azure SQL-service om uw Azure SQL Database te koppelen die uitvoergegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="4d641-331">An Azure SQL linked service to link your Azure SQL database that holds the output data.</span></span> 
3. <span data-ttu-id="4d641-332">U hebt **gegevenssets** gemaakt waarin de invoer- en uitvoergegevens van pijplijnen worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="4d641-332">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="4d641-333">U hebt een **pijplijn** gemaakt met een kopieeractiviteit met BlobSource als bron en SqlSink als sink.</span><span class="sxs-lookup"><span data-stu-id="4d641-333">Created a **pipeline** with a Copy Activity with BlobSource as source and SqlSink as sink.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4d641-334">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4d641-334">Next steps</span></span>
<span data-ttu-id="4d641-335">In deze zelfstudie hebt u voor een kopieerbewerking een Azure Blob-opslag gebruikt als brongegevensarchief en een Azure SQL-database als doelgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="4d641-335">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="4d641-336">De volgende tabel bevat een lijst met gegevensarchieven die worden ondersteund als bron en doel voor de kopieeractiviteit:</span><span class="sxs-lookup"><span data-stu-id="4d641-336">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="4d641-337">Klik op de koppeling voor de gegevensopslag in de tabel voor meer informatie over het kopiëren van gegevens naar/uit een gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="4d641-337">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>