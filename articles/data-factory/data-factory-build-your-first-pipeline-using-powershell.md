---
title: Uw eerste gegevensfactory bouwen (PowerShell) | Microsoft Docs
description: In deze zelfstudie maakt u een Azure Data Factory-voorbeeldpijplijn met behulp van Azure PowerShell.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 22ec1236-ea86-4eb7-b903-0e79a58b90c7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 40a63339be90d0c5d972605c7f6fa029ca1e2ba4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a><span data-ttu-id="f99af-103">Zelfstudie: uw eerste Azure-gegevensfactory bouwen met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f99af-103">Tutorial: Build your first Azure data factory using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f99af-104">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="f99af-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="f99af-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f99af-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="f99af-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f99af-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="f99af-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f99af-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="f99af-108">Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="f99af-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="f99af-109">REST API</span><span class="sxs-lookup"><span data-stu-id="f99af-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

<span data-ttu-id="f99af-110">In dit artikel gebruikt u Azure PowerShell voor het maken van uw eerste Azure-gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="f99af-110">In this article, you use Azure PowerShell to create your first Azure data factory.</span></span> <span data-ttu-id="f99af-111">Als u de zelfstudie wilt volgen met andere hulpprogramma's/SDK's, selecteert u een van de opties uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="f99af-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

<span data-ttu-id="f99af-112">De pijplijn in deze zelfstudie heeft één activiteit: **HDInsight-componentactiviteit**.</span><span class="sxs-lookup"><span data-stu-id="f99af-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="f99af-113">Deze activiteit voert een Hive-script uit op een Azure HDInsight-cluster dat invoergegevens transformeert om uitvoergegevens te produceren.</span><span class="sxs-lookup"><span data-stu-id="f99af-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="f99af-114">De pijplijn is gepland on één keer per maand tussen de opgegeven begin- en eindtijd te worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f99af-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="f99af-115">Met de gegevenspijplijn in deze zelfstudie worden invoergegevens getransformeerd in uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="f99af-115">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="f99af-116">Er worden bijvoorbeeld geen gegevens gekopieerd van een brongegevensarchief naar een doelgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="f99af-116">It does not copy data from a source data store to a destination data store.</span></span> <span data-ttu-id="f99af-117">Zie [Zelfstudie: gegevens kopiëren van Blob Storage naar SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor informatie over het kopiëren van gegevens met Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f99af-117">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="f99af-118">Een pijplijn kan meer dan één activiteit hebben.</span><span class="sxs-lookup"><span data-stu-id="f99af-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="f99af-119">Ook kunt u twee activiteiten koppelen (de ene activiteit na de andere laten uitvoeren) door de uitvoergegevensset van één activiteit in te stellen als invoergegevensset voor een andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="f99af-119">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="f99af-120">Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f99af-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f99af-121">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f99af-121">Prerequisites</span></span>
* <span data-ttu-id="f99af-122">Lees het artikel [Overzicht van de zelfstudie](data-factory-build-your-first-pipeline.md) en voer de **vereiste** stappen uit.</span><span class="sxs-lookup"><span data-stu-id="f99af-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="f99af-123">Volg de instructies in [Azure PowerShell installeren en configureren](/powershell/azure/overview) om de meest recente versie van Azure PowerShell te installeren op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f99af-123">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="f99af-124">(optioneel) Dit artikel omvat niet alle Data Factory-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="f99af-124">(optional) This article does not cover all the Data Factory cmdlets.</span></span> <span data-ttu-id="f99af-125">Zie [Naslaginformatie voor Data Factory-cmdlets](/powershell/module/azurerm.datafactories) (Data Factory Cmdlet Reference) voor uitgebreide documentatie over Data Factory-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="f99af-125">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on Data Factory cmdlets.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="f99af-126">Een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="f99af-126">Create data factory</span></span>
<span data-ttu-id="f99af-127">In deze stap gebruikt u Azure PowerShell om een Azure-gegevensfactory met de naam **FirstDataFactoryPSH** te maken.</span><span class="sxs-lookup"><span data-stu-id="f99af-127">In this step, you use Azure PowerShell to create an Azure Data Factory named **FirstDataFactoryPSH**.</span></span> <span data-ttu-id="f99af-128">Een gegevensfactory kan één of meer pijplijnen hebben.</span><span class="sxs-lookup"><span data-stu-id="f99af-128">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="f99af-129">Een pijplijn kan één of meer activiteiten bevatten.</span><span class="sxs-lookup"><span data-stu-id="f99af-129">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="f99af-130">Bijvoorbeeld een kopieeractiviteit om gegevens van een bron- naar een doelgegevensopslagplaats te kopiëren en een HDInsight Hive-activiteit om een Hive-script uit te voeren voor het transformeren van invoergegevens.</span><span class="sxs-lookup"><span data-stu-id="f99af-130">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data.</span></span> <span data-ttu-id="f99af-131">U begint in deze stap met het maken van de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="f99af-131">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="f99af-132">Open Azure PowerShell en voer de volgende opdracht uit.</span><span class="sxs-lookup"><span data-stu-id="f99af-132">Start Azure PowerShell and run the following command.</span></span> <span data-ttu-id="f99af-133">Houd Azure PowerShell open tot het einde van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f99af-133">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="f99af-134">Als u het programma sluit en opnieuw opent, moet u deze opdrachten opnieuw uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f99af-134">If you close and reopen, you need to run these commands again.</span></span>
   * <span data-ttu-id="f99af-135">Voer de volgende opdracht uit en geef de gebruikersnaam en het wachtwoord op waarmee u zich aanmeldt bij Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f99af-135">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * <span data-ttu-id="f99af-136">Voer de volgende opdracht uit om alle abonnementen voor dit account weer te geven.</span><span class="sxs-lookup"><span data-stu-id="f99af-136">Run the following command to view all the subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * <span data-ttu-id="f99af-137">Voer de volgende opdracht uit om het abonnement te selecteren waarmee u wilt werken.</span><span class="sxs-lookup"><span data-stu-id="f99af-137">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="f99af-138">Dit moet hetzelfde abonnement zijn als het abonnement dat u in de Azure Portal gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f99af-138">This subscription should be the same as the one you used in the Azure portal.</span></span>
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. <span data-ttu-id="f99af-139">Maak een Azure-resourcegroep met de naam **ADFTutorialResourceGroup** door de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="f99af-139">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command:</span></span>
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    <span data-ttu-id="f99af-140">Voor sommige van de stappen in deze zelfstudie wordt ervan uitgegaan dat u de resourcegroep met de naam ADFTutorialResourceGroup gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f99af-140">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="f99af-141">Als u een andere resourcegroep gebruikt, moet u voor deze zelfstudie die groep gebruiken in plaats van ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="f99af-141">If you use a different resource group, you need to use it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="f99af-142">Voer de cmdlet **New-AzureRmDataFactory** uit om een gegevensfactory met de naam **FirstDataFactoryPSH** te maken.</span><span class="sxs-lookup"><span data-stu-id="f99af-142">Run the **New-AzureRmDataFactory** cmdlet that creates a data factory named **FirstDataFactoryPSH**.</span></span>

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
<span data-ttu-id="f99af-143">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="f99af-143">Note the following points:</span></span>

* <span data-ttu-id="f99af-144">De naam van de Azure-gegevensfactory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="f99af-144">The name of the Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="f99af-145">Als u de foutmelding **De gegevensfactorynaam FirstDataFactoryPSH is niet beschikbaar** ziet, wijzigt u de naam (bijvoorbeeld in yournameFirstDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="f99af-145">If you receive the error **Data factory name “FirstDataFactoryPSH” is not available**, change the name (for example, yournameFirstDataFactoryPSH).</span></span> <span data-ttu-id="f99af-146">Gebruik deze naam in plaats van ADFTutorialFactoryPSH tijdens het uitvoeren van de stappen in de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f99af-146">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="f99af-147">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="f99af-147">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="f99af-148">Als u Data Factory-exemplaren wilt maken, moet u bijdrager/beheerder zijn van het Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="f99af-148">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span></span>
* <span data-ttu-id="f99af-149">De naam van de gegevensfactory wordt in de toekomst mogelijk geregistreerd als DNS-naam en wordt daarmee ook voor iedereen zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="f99af-149">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>
* <span data-ttu-id="f99af-150">Als u de foutmelding **This subscription is not registered to use namespace Microsoft.DataFactory** ontvangt, voert u een van de volgende stappen uit en probeert u opnieuw te publiceren:</span><span class="sxs-lookup"><span data-stu-id="f99af-150">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span></span>

  * <span data-ttu-id="f99af-151">Voer in Azure PowerShell de volgende opdracht uit om de Data Factory-provider te registreren:</span><span class="sxs-lookup"><span data-stu-id="f99af-151">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      <span data-ttu-id="f99af-152">U kunt de volgende opdracht uitvoeren om te bevestigen dat de Data Factory-provider is geregistreerd:</span><span class="sxs-lookup"><span data-stu-id="f99af-152">You can run the following command to confirm that the Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="f99af-153">Meld u bij de [Azure Portal](https://portal.azure.com) aan met behulp van het Azure-abonnement en navigeer naar een Data Factory-blade of maak een gegevensfactory in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f99af-153">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="f99af-154">Door deze actie wordt de provider automatisch voor u geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="f99af-154">This action automatically registers the provider for you.</span></span>

<span data-ttu-id="f99af-155">Voordat u een pijplijn maakt, moet u eerst enkele Data Factory-entiteiten maken.</span><span class="sxs-lookup"><span data-stu-id="f99af-155">Before creating a pipeline, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="f99af-156">U maakt eerst gekoppelde services om gegevensopslag/berekeningen te koppelen aan uw gegevensopslag, vervolgens definieert u welke invoer- en uitvoergegevenssets de invoer- en uitvoergegevens in de gekoppelde gegevensopslag vertegenwoordigen en daarna maakt u de pijplijn met een activiteit waarvoor gebruik wordt gemaakt van die gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="f99af-156">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent input/output data in linked data stores, and then create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="f99af-157">Gekoppelde services maken</span><span class="sxs-lookup"><span data-stu-id="f99af-157">Create linked services</span></span>
<span data-ttu-id="f99af-158">In deze stap koppelt u uw Azure Storage-account en een on-demand Azure HDInsight-cluster aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="f99af-158">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span></span> <span data-ttu-id="f99af-159">Het Azure Storage-account bevat de in- en uitvoergegevens van de pijplijn in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f99af-159">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> <span data-ttu-id="f99af-160">De gekoppelde HDInsight-service wordt gebruikt om een Hive-script uit te voeren dat is opgegeven in de activiteit van de pijplijn in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f99af-160">The HDInsight linked service is used to run a Hive script specified in the activity of the pipeline in this sample.</span></span> <span data-ttu-id="f99af-161">Geef aan welk(e) gegevensarchief/rekenservices er in uw scenario worden gebruikt. Koppel die services aan de gegevensfactory door gekoppelde services te maken.</span><span class="sxs-lookup"><span data-stu-id="f99af-161">Identify what data store/compute services are used in your scenario and link those services to the data factory by creating linked services.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="f99af-162">Een gekoppelde Azure Storage-service maken</span><span class="sxs-lookup"><span data-stu-id="f99af-162">Create Azure Storage linked service</span></span>
<span data-ttu-id="f99af-163">In deze stap koppelt u uw Azure Storage-account aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="f99af-163">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="f99af-164">U gebruikt hetzelfde Azure Storage-account om invoer- en uitvoergegevens en het HQL-scriptbestand op te slaan.</span><span class="sxs-lookup"><span data-stu-id="f99af-164">You use the same Azure Storage account to store input/output data and the HQL script file.</span></span>

1. <span data-ttu-id="f99af-165">Maak een JSON-bestand met de naam StorageLinkedService.json in de map C:\ADFGetStarted. Geef dit bestand de volgende inhoud.</span><span class="sxs-lookup"><span data-stu-id="f99af-165">Create a JSON file named StorageLinkedService.json in the C:\ADFGetStarted folder with the following content.</span></span> <span data-ttu-id="f99af-166">Maak de map ADFGetStarted als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="f99af-166">Create the folder ADFGetStarted if it does not already exist.</span></span>

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
    <span data-ttu-id="f99af-167">Vervang de **accountnaam** door de naam van uw Azure-opslagaccount en vervang de **accountsleutel** door de toegangssleutel van het Azure-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="f99af-167">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="f99af-168">Raadpleeg de informatie over het weergeven, kopiëren en opnieuw genereren van toegangssleutels voor opslag in [Uw opslagaccount beheren](../storage/common/storage-create-storage-account.md#manage-your-storage-account) als u meer wilt weten over het verkrijgen van een toegangssleutel voor opslag.</span><span class="sxs-lookup"><span data-stu-id="f99af-168">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
2. <span data-ttu-id="f99af-169">Schakel in Azure PowerShell over naar de map ADFGetStarted.</span><span class="sxs-lookup"><span data-stu-id="f99af-169">In Azure PowerShell, switch to the ADFGetStarted folder.</span></span>
3. <span data-ttu-id="f99af-170">U kunt de cmdlet **New-AzureRmDataFactoryLinkedService** gebruiken om een gekoppelde service te maken.</span><span class="sxs-lookup"><span data-stu-id="f99af-170">You can use the **New-AzureRmDataFactoryLinkedService** cmdlet that creates a linked service.</span></span> <span data-ttu-id="f99af-171">Voor deze cmdlet en andere Data Factory-cmdlets die u in deze zelfstudie gebruikt, moet u waarden doorgeven voor de parameters *ResourceGroupName* en *DataFactoryName*.</span><span class="sxs-lookup"><span data-stu-id="f99af-171">This cmdlet and other Data Factory cmdlets you use in this tutorial requires you to pass values for the *ResourceGroupName* and *DataFactoryName* parameters.</span></span> <span data-ttu-id="f99af-172">U kunt ook **Get-AzureRmDataFactory** gebruiken om een **DataFactory**-object te verkrijgen. U geeft daarmee het object door zonder dat u de *ResourceGroupName* en de *DataFactoryName* hoeft op te geven telkens wanneer u een cmdlet uitvoert.</span><span class="sxs-lookup"><span data-stu-id="f99af-172">Alternatively, you can use **Get-AzureRmDataFactory** to get a **DataFactory** object and pass the object without typing *ResourceGroupName* and *DataFactoryName* each time you run a cmdlet.</span></span> <span data-ttu-id="f99af-173">Voer de volgende opdracht om de uitvoer van de cmdlet **Get-AzureRmDataFactory** toe te wijzen aan een **$df**-variabele.</span><span class="sxs-lookup"><span data-stu-id="f99af-173">Run the following command to assign the output of the **Get-AzureRmDataFactory** cmdlet to a **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. <span data-ttu-id="f99af-174">Voer nu de cmdlet **New-AzureRmDataFactoryLinkedService** uit om de gekoppelde **StorageLinkedService**-service te maken.</span><span class="sxs-lookup"><span data-stu-id="f99af-174">Now, run the **New-AzureRmDataFactoryLinkedService** cmdlet that creates the linked **StorageLinkedService** service.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="f99af-175">Als u de cmdlet **Get-AzureRmDataFactory** niet had uitgevoerd en u de uitvoer niet had toegewezen aan de **$df**-variabele, zou u als volgt waarden moeten opgeven voor de parameters *ResourceGroupName* en *DataFactoryName*.</span><span class="sxs-lookup"><span data-stu-id="f99af-175">If you hadn't run the **Get-AzureRmDataFactory** cmdlet and assigned the output to the **$df** variable, you would have to specify values for the *ResourceGroupName* and *DataFactoryName* parameters as follows.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="f99af-176">Als u Azure PowerShell gedurende deze zelfstudie sluit, moet u de volgende keer dat u Azure PowerShell opent, de cmdlet **Get-AzureRmDataFactory** uitvoeren om de zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="f99af-176">If you close Azure PowerShell in the middle of the tutorial, you have to run the **Get-AzureRmDataFactory** cmdlet next time you start Azure PowerShell to complete the tutorial.</span></span>

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="f99af-177">Een gekoppelde HDInsight-service maken</span><span class="sxs-lookup"><span data-stu-id="f99af-177">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="f99af-178">In deze stap koppelt u een on-demand HDInsight-cluster aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="f99af-178">In this step, you link an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="f99af-179">Het HDInsight-cluster wordt automatisch gemaakt tijdens runtime en wordt verwijderd wanneer het verwerken is voltooid en het cluster gedurende een opgegeven tijdsperiode niet actief is geweest.</span><span class="sxs-lookup"><span data-stu-id="f99af-179">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span></span> <span data-ttu-id="f99af-180">U kunt uw eigen HDInsight-cluster gebruiken in plaats van een on-demand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="f99af-180">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="f99af-181">Zie [Gekoppelde services berekenen](data-factory-compute-linked-services.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f99af-181">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="f99af-182">Maak een JSON-bestand met de naam **HDInsightOnDemandLinkedService**.json in de map **C:\ADFGetStarted**. Geef dit bestand de volgende inhoud.</span><span class="sxs-lookup"><span data-stu-id="f99af-182">Create a JSON file named **HDInsightOnDemandLinkedService**.json in the **C:\ADFGetStarted** folder with the following content.</span></span>

    ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "StorageLinkedService"
            }
        }
    }
    ```
    <span data-ttu-id="f99af-183">De volgende tabel bevat beschrijvingen van de JSON-eigenschappen die in het codefragment worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="f99af-183">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="f99af-184">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="f99af-184">Property</span></span> | <span data-ttu-id="f99af-185">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f99af-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="f99af-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="f99af-186">ClusterSize</span></span> |<span data-ttu-id="f99af-187">Geeft de grootte van het HDInsight-cluster aan.</span><span class="sxs-lookup"><span data-stu-id="f99af-187">Specifies the size of the HDInsight cluster.</span></span> |
   | <span data-ttu-id="f99af-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="f99af-188">TimeToLive</span></span> |<span data-ttu-id="f99af-189">Geeft aan hoelang het HDInsight-cluster inactief moet zijn voordat het wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f99af-189">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="f99af-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="f99af-190">linkedServiceName</span></span> |<span data-ttu-id="f99af-191">Geeft het opslagaccount aan dat wordt gebruikt voor het opslaan van de logboeken die door HDInsight worden gegenereerd</span><span class="sxs-lookup"><span data-stu-id="f99af-191">Specifies the storage account that is used to store the logs that are generated by HDInsight</span></span> |

    <span data-ttu-id="f99af-192">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="f99af-192">Note the following points:</span></span>

   * <span data-ttu-id="f99af-193">Met de JSON maakt Data Factory voor u een HDInsight-cluster **op basis van Linux**.</span><span class="sxs-lookup"><span data-stu-id="f99af-193">The Data Factory creates a **Linux-based** HDInsight cluster for you with the JSON.</span></span> <span data-ttu-id="f99af-194">Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f99af-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="f99af-195">U kunt **uw eigen HDInsight-cluster** gebruiken in plaats van een on-demand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="f99af-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="f99af-196">Zie [Gekoppelde HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f99af-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="f99af-197">Het HDInsight-cluster maakt een **standaardcontainer** in de blobopslag die u hebt opgegeven in de JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="f99af-197">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="f99af-198">HDInsight verwijdert deze container niet wanneer het cluster wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f99af-198">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="f99af-199">Dit gedrag is standaard.</span><span class="sxs-lookup"><span data-stu-id="f99af-199">This behavior is by design.</span></span> <span data-ttu-id="f99af-200">Met een gekoppelde on-demand HDInsight-service wordt er steeds een HDInsight-cluster gemaakt wanneer er een segment wordt verwerkt, tenzij er een bestaand livecluster is (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="f99af-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="f99af-201">Het cluster wordt verwijderd wanneer het verwerken is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f99af-201">The cluster is automatically deleted when the processing is done.</span></span>

       <span data-ttu-id="f99af-202">Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="f99af-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="f99af-203">Als u deze niet nodig hebt voor het oplossen van problemen met taken, kunt u ze verwijderen om de opslagkosten te verlagen.</span><span class="sxs-lookup"><span data-stu-id="f99af-203">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="f99af-204">De namen van deze containers worden als volgt opgebouwd: adf**naamvanuwgegevensfactory**-**naamvangekoppeldeservice**-datum-/tijdstempel.</span><span class="sxs-lookup"><span data-stu-id="f99af-204">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="f99af-205">Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) om containers in uw Azure-blobopslag te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f99af-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="f99af-206">Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f99af-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
2. <span data-ttu-id="f99af-207">Voer de cmdlet **New-AzureRmDataFactoryLinkedService** uit om de gekoppelde service met de naam HDInsightOnDemandLinkedService te maken.</span><span class="sxs-lookup"><span data-stu-id="f99af-207">Run the **New-AzureRmDataFactoryLinkedService** cmdlet that creates the linked service called HDInsightOnDemandLinkedService.</span></span>
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a><span data-ttu-id="f99af-208">Gegevenssets maken</span><span class="sxs-lookup"><span data-stu-id="f99af-208">Create datasets</span></span>
<span data-ttu-id="f99af-209">In deze stap maakt u gegevenssets die de invoer- en uitvoergegevens voor Hive-verwerking vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="f99af-209">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="f99af-210">Deze gegevenssets verwijzen naar de **StorageLinkedService** die u eerder in deze zelfstudie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f99af-210">These datasets refer to the **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="f99af-211">De gekoppelde service verwijst naar een Azure-opslagaccount en in de gegevenssets vindt u de container, map en bestandsnaam in de opslag van de invoer- en uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="f99af-211">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="f99af-212">Invoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="f99af-212">Create input dataset</span></span>
1. <span data-ttu-id="f99af-213">Maak een JSON-bestand met de naam **InputTable.json** in de map **C:\ADFGetStarted**. Geef dit bestand de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="f99af-213">Create a JSON file named **InputTable.json** in the **C:\ADFGetStarted** folder with the following content:</span></span>

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
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
    <span data-ttu-id="f99af-214">Met de JSON wordt een gegevensset gedefinieerd met de naam **AzureBlobInput**. Deze bevat de invoergegevens voor een activiteit in de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="f99af-214">The JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="f99af-215">Bovendien wordt hiermee aangegeven dat de invoergegevens zich bevinden in de blobcontainer met de naam **adfgetstarted** en in de map met de naam **inputdata**</span><span class="sxs-lookup"><span data-stu-id="f99af-215">In addition, it specifies that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span></span>

    <span data-ttu-id="f99af-216">De volgende tabel bevat beschrijvingen van de JSON-eigenschappen die in het codefragment worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="f99af-216">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="f99af-217">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="f99af-217">Property</span></span> | <span data-ttu-id="f99af-218">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f99af-218">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="f99af-219">type</span><span class="sxs-lookup"><span data-stu-id="f99af-219">type</span></span> |<span data-ttu-id="f99af-220">De eigenschap type wordt ingesteld op AzureBlob, omdat de gegevens zich in de Azure-blobopslag bevinden.</span><span class="sxs-lookup"><span data-stu-id="f99af-220">The type property is set to AzureBlob because data resides in Azure blob storage.</span></span> |
   | <span data-ttu-id="f99af-221">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="f99af-221">linkedServiceName</span></span> |<span data-ttu-id="f99af-222">Deze eigenschap verwijst naar de StorageLinkedService die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f99af-222">refers to the StorageLinkedService you created earlier.</span></span> |
   | <span data-ttu-id="f99af-223">fileName</span><span class="sxs-lookup"><span data-stu-id="f99af-223">fileName</span></span> |<span data-ttu-id="f99af-224">Deze eigenschap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="f99af-224">This property is optional.</span></span> <span data-ttu-id="f99af-225">Als u deze eigenschap niet opgeeft, worden alle bestanden uit folderPath gekozen.</span><span class="sxs-lookup"><span data-stu-id="f99af-225">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="f99af-226">In dit geval wordt alleen input.log verwerkt.</span><span class="sxs-lookup"><span data-stu-id="f99af-226">In this case, only the input.log is processed.</span></span> |
   | <span data-ttu-id="f99af-227">type</span><span class="sxs-lookup"><span data-stu-id="f99af-227">type</span></span> |<span data-ttu-id="f99af-228">Omdat de logboekbestanden tekstbestanden zijn, gebruiken we TextFormat.</span><span class="sxs-lookup"><span data-stu-id="f99af-228">The log files are in text format, so we use TextFormat.</span></span> |
   | <span data-ttu-id="f99af-229">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="f99af-229">columnDelimiter</span></span> |<span data-ttu-id="f99af-230">Kolommen in de logboekbestanden worden gescheiden door een komma (,).</span><span class="sxs-lookup"><span data-stu-id="f99af-230">columns in the log files are delimited by the comma character (,).</span></span> |
   | <span data-ttu-id="f99af-231">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="f99af-231">frequency/interval</span></span> |<span data-ttu-id="f99af-232">Als frequency wordt ingesteld op Month en de interval 1 is, betekent dat dat de invoersegmenten één keer per maand beschikbaar worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f99af-232">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span></span> |
   | <span data-ttu-id="f99af-233">external</span><span class="sxs-lookup"><span data-stu-id="f99af-233">external</span></span> |<span data-ttu-id="f99af-234">Deze eigenschap wordt ingesteld op true als de invoergegevens niet worden gegenereerd door de Data Factory-service.</span><span class="sxs-lookup"><span data-stu-id="f99af-234">this property is set to true if the input data is not generated by the Data Factory service.</span></span> |
2. <span data-ttu-id="f99af-235">Voer in Azure PowerShell de volgende opdracht uit om de Data Factory-gegevensset te maken:</span><span class="sxs-lookup"><span data-stu-id="f99af-235">Run the following command in Azure PowerShell to create the Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="f99af-236">Uitvoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="f99af-236">Create output dataset</span></span>
<span data-ttu-id="f99af-237">U maakt nu de uitvoergegevensset die staat voor de uitvoergegevens die worden opgeslagen in de Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="f99af-237">Now, you create the output dataset to represent the output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="f99af-238">Maak een JSON-bestand met de naam **OutputTable.json** in de map **C:\ADFGetStarted**. Geef dit bestand de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="f99af-238">Create a JSON file named **OutputTable.json** in the **C:\ADFGetStarted** folder with the following content:</span></span>

    ```json
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
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
    <span data-ttu-id="f99af-239">Met de JSON wordt een gegevensset gedefinieerd met de naam **AzureBlobOutput**. Deze bevat de uitvoergegevens voor een activiteit in de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="f99af-239">The JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in the pipeline.</span></span> <span data-ttu-id="f99af-240">Bovendien wordt hiermee aangegeven dat de resultaten worden opgeslagen in de blobcontainer met de naam **adfgetstarted** en in de map met de naam **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="f99af-240">In addition, it specifies that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span></span> <span data-ttu-id="f99af-241">In het gedeelte **availability** wordt opgegeven dat de uitvoergegevensset op maandelijkse basis wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="f99af-241">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span>
2. <span data-ttu-id="f99af-242">Voer in Azure PowerShell de volgende opdracht uit om de Data Factory-gegevensset te maken:</span><span class="sxs-lookup"><span data-stu-id="f99af-242">Run the following command in Azure PowerShell to create the Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a><span data-ttu-id="f99af-243">Pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="f99af-243">Create pipeline</span></span>
<span data-ttu-id="f99af-244">In deze stap maakt u uw eerste pijplijn met een **HDInsightHive**-activiteit.</span><span class="sxs-lookup"><span data-stu-id="f99af-244">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="f99af-245">Het invoersegment wordt elke maand beschikbaar gesteld (frequentie: Maand, interval: 1), evenals het uitvoersegment. Ook de plannereigenschap van de activiteit wordt op maandelijks ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f99af-245">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span></span> <span data-ttu-id="f99af-246">De instellingen voor de uitvoergegevensset en de activiteitenplanner moeten overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="f99af-246">The settings for the output dataset and the activity scheduler must match.</span></span> <span data-ttu-id="f99af-247">Op dit moment wordt de planning gebaseerd op de uitvoergegevensset. Daarom moet u ook een uitvoergegevensset maken als er tijdens de activiteit geen uitvoer wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="f99af-247">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="f99af-248">Als er voor de activiteit geen invoer nodig is, kunt u het maken van de invoergegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="f99af-248">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="f99af-249">De eigenschappen die in de volgende JSON worden gebruikt, worden aan het einde van dit gedeelte beschreven.</span><span class="sxs-lookup"><span data-stu-id="f99af-249">The properties used in the following JSON are explained at the end of this section.</span></span>

1. <span data-ttu-id="f99af-250">Maak een JSON-bestand met de naam MyFirstPipelinePSH.json in de map C:\ADFGetStarted. Geef dit bestand de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="f99af-250">Create a JSON file named MyFirstPipelinePSH.json in the C:\ADFGetStarted folder with the following content:</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f99af-251">Vervang **storageaccountname** door de naam van uw opslagaccount in de JSON.</span><span class="sxs-lookup"><span data-stu-id="f99af-251">Replace **storageaccountname** with the name of your storage account in the JSON.</span></span>
   >
   >

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "StorageLinkedService",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
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
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```
    <span data-ttu-id="f99af-252">In het JSON-codefragment maakt u een pijplijn die bestaat uit een enkele activiteit waarvoor gebruik wordt gemaakt van Hive om gegevens in een HDInsight-cluster te verwerken.</span><span class="sxs-lookup"><span data-stu-id="f99af-252">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="f99af-253">Het Hive-scriptbestand **partitionweblogs.hql** wordt opgeslagen in het Azure-opslagaccount (opgegeven door de scriptLinkedService met de naam **StorageLinkedService**) en in de map **script** van de container **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="f99af-253">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **StorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>

    <span data-ttu-id="f99af-254">Het gedeelte **defines** wordt gebruikt om de runtime-instellingen die worden doorgegeven aan het Hive-script, op te geven als Hive-configuratiewaarden (bijvoorbeeld ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="f99af-254">The **defines** section is used to specify the runtime settings that be passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="f99af-255">Met de eigenschappen **start** en **end** van de pijplijn wordt opgegeven in welke periode de pijplijn actief is.</span><span class="sxs-lookup"><span data-stu-id="f99af-255">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span>

    <span data-ttu-id="f99af-256">In de activiteits-JSON geeft u op dat het Hive-script wordt uitgevoerd in de berekening die is opgegeven door de **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="f99af-256">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f99af-257">Zie 'Pijplijn JSON' in [Pijplijnen en activiteiten in Azure Data Factory](data-factory-create-pipelines.md) voor meer informatie over de JSON-eigenschappen die in dit voorbeeld worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f99af-257">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties that are used in the example.</span></span>

2. <span data-ttu-id="f99af-258">Controleer of u het bestand **input.log** ziet in de map **adfgetstarted/inputdata** in de Azure-blobopslag en voer de volgende opdracht uit om de pijplijn te implementeren.</span><span class="sxs-lookup"><span data-stu-id="f99af-258">Confirm that you see the **input.log** file in the **adfgetstarted/inputdata** folder in the Azure blob storage, and run the following command to deploy the pipeline.</span></span> <span data-ttu-id="f99af-259">Aangezien de tijden voor **start** en **end** in het verleden vallen en **isPaused** is ingesteld op false, wordt de pijplijn (activiteit in de pijplijn) direct na het implementeren uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f99af-259">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. <span data-ttu-id="f99af-260">U hebt uw eerste pijplijn gemaakt met Azure PowerShell!</span><span class="sxs-lookup"><span data-stu-id="f99af-260">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="f99af-261">De pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="f99af-261">Monitor pipeline</span></span>
<span data-ttu-id="f99af-262">In deze stap gebruikt u Azure PowerShell om te bewaken wat er gebeurt in een Azure-gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="f99af-262">In this step, you use Azure PowerShell to monitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="f99af-263">Voer **Get-AzureRmDataFactory** uit en wijs de uitvoer toe aan een **$df**-variabele.</span><span class="sxs-lookup"><span data-stu-id="f99af-263">Run **Get-AzureRmDataFactory** and assign the output to a **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. <span data-ttu-id="f99af-264">Voer **Get-AzureRmDataFactorySlice** uit voor meer informatie over alle segmenten van **EmpSQLTable**, de uitvoertabel van de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="f99af-264">Run **Get-AzureRmDataFactorySlice** to get details about all slices of the **EmpSQLTable**, which is the output table of the pipeline.</span></span>

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    <span data-ttu-id="f99af-265">De StartDateTime die u hier opgeeft, is dezelfde begintijd die u hebt opgegeven in de JSON van de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="f99af-265">Notice that the StartDateTime you specify here is the same start time specified in the pipeline JSON.</span></span> <span data-ttu-id="f99af-266">Hier volgt een voorbeeld van uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f99af-266">Here is the sample output:</span></span>

    ```PowerShell
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : FirstDataFactoryPSH
    DatasetName       : AzureBlobOutput
    Start             : 7/1/2017 12:00:00 AM
    End               : 7/2/2017 12:00:00 AM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. <span data-ttu-id="f99af-267">Voer **Get-AzureRmDataFactoryRun** uit om voor een bepaald segment gegevens over het uitvoeren van de activiteit op te halen.</span><span class="sxs-lookup"><span data-stu-id="f99af-267">Run **Get-AzureRmDataFactoryRun** to get the details of activity runs for a specific slice.</span></span>

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    <span data-ttu-id="f99af-268">Hier volgt een voorbeeld van uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f99af-268">Here is the sample output:</span></span> 

    ```PowerShell
    Id                  : 0f6334f2-d56c-4d48-b427-d4f0fb4ef883_635268096000000000_635292288000000000_AzureBlobOutput
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : FirstDataFactoryPSH
    DatasetName         : AzureBlobOutput
    ProcessingStartTime : 12/18/2015 4:50:33 AM
    ProcessingEndTime   : 12/31/9999 11:59:59 PM
    PercentComplete     : 0
    DataSliceStart      : 7/1/2017 12:00:00 AM
    DataSliceEnd        : 7/2/2017 12:00:00 AM
    Status              : AllocatingResources
    Timestamp           : 12/18/2015 4:50:33 AM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : RunSampleHiveActivity
    PipelineName        : MyFirstPipeline
    Type                : Script
    ```
    <span data-ttu-id="f99af-269">U kunt deze cmdlet blijven uitvoeren tot u ziet dat het segment de status **Gereed** of **Mislukt** heeft gekregen.</span><span class="sxs-lookup"><span data-stu-id="f99af-269">You can keep running this cmdlet until you see the slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="f99af-270">Wanneer het segment de status Gereed heeft, controleert u de map **partitioneddata** in de container **adfgetstarted** in uw blobopslag voor de uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="f99af-270">When the slice is in Ready state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  <span data-ttu-id="f99af-271">Het maken van een on-demand HDInsight-cluster duurt normaal gesproken enige tijd.</span><span class="sxs-lookup"><span data-stu-id="f99af-271">Creation of an on-demand HDInsight cluster usually takes some time.</span></span>

    ![Uitvoergegevens](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="f99af-273">Het maken van een on-demand HDInsight-cluster duurt normaal gesproken enige tijd (ongeveer 20 minuten).</span><span class="sxs-lookup"><span data-stu-id="f99af-273">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="f99af-274">Daarom kunt u ervan uitgaan dat het **ongeveer 30 minuten** duurt voordat het segment in de pijplijn is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="f99af-274">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>
>
> <span data-ttu-id="f99af-275">Het invoerbestand wordt verwijderd zodra het segment is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="f99af-275">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="f99af-276">Als u het segment dus opnieuw wilt uitvoeren of als u de zelfstudie opnieuw wilt doorlopen, uploadt u het invoerbestand (input.log) naar de map met invoergegevens van de container adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="f99af-276">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
>
>

## <a name="summary"></a><span data-ttu-id="f99af-277">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="f99af-277">Summary</span></span>
<span data-ttu-id="f99af-278">In deze zelfstudie hebt u een Azure-gegevensfactory gemaakt voor het verwerken van gegevens. Dit hebt u gedaan door Hive-script uit te voeren op een HDInsight Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="f99af-278">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="f99af-279">U hebt in de Azure Portal de Data Factory-editor gebruikt om de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="f99af-279">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>

1. <span data-ttu-id="f99af-280">U hebt een Azure-**gegevensfactory** gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f99af-280">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="f99af-281">U hebt twee **gekoppelde services** gemaakt:</span><span class="sxs-lookup"><span data-stu-id="f99af-281">Created two **linked services**:</span></span>
   1. <span data-ttu-id="f99af-282">Een gekoppelde **Azure Storage**-service om te koppelen aan de Azure-blobopslag die de invoer-/uitvoerbestanden van de gegevensfactory bevat.</span><span class="sxs-lookup"><span data-stu-id="f99af-282">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="f99af-283">Een gekoppelde on-demand **Azure HDInsight**-service om te koppelen aan een on-demand HDInsight Hadoop-cluster van de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="f99af-283">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="f99af-284">Azure Data Factory maakt op tijd een HDInsight Hadoop-cluster om invoergegevens te verwerken en uitvoergegevens te produceren.</span><span class="sxs-lookup"><span data-stu-id="f99af-284">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="f99af-285">U hebt twee **gegevenssets** gemaakt, waarin de invoer- en uitvoergegevens van de HDInsight Hive-activiteit in de pijplijn worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="f99af-285">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="f99af-286">U hebt een **pijplijn** gemaakt met een **HDInsight Hive**-activiteit.</span><span class="sxs-lookup"><span data-stu-id="f99af-286">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f99af-287">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f99af-287">Next steps</span></span>
<span data-ttu-id="f99af-288">In dit artikel hebt u een pijplijn gemaakt met een transformatieactiviteit (HDInsight-activiteit) waarvoor een Hive-script wordt uitgevoerd op een on-demand Azure HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="f99af-288">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="f99af-289">Zie [Zelfstudie: gegevens van een Azure-blob kopiëren naar Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor meer informatie over het gebruiken van een kopieeractiviteit om gegevens van een Azure-blob te kopiëren naar Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="f99af-289">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="f99af-290">Zie ook</span><span class="sxs-lookup"><span data-stu-id="f99af-290">See Also</span></span>
| <span data-ttu-id="f99af-291">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="f99af-291">Topic</span></span> | <span data-ttu-id="f99af-292">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f99af-292">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="f99af-293">Data Factory-cmdlet-verwijzing</span><span class="sxs-lookup"><span data-stu-id="f99af-293">Data Factory Cmdlet Reference</span></span>](/powershell/module/azurerm.datafactories) |<span data-ttu-id="f99af-294">Zie de uitgebreide documentatie over Data Factory-cmdlets</span><span class="sxs-lookup"><span data-stu-id="f99af-294">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="f99af-295">Pijplijnen</span><span class="sxs-lookup"><span data-stu-id="f99af-295">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="f99af-296">Met behulp van dit artikel krijgt u inzicht in de pijplijnen en activiteiten in Azure Data Factory en in de wijze waarop u deze kunt gebruiken om end-to-end gegevensgestuurde werkstromen te maken voor uw scenario of bedrijf.</span><span class="sxs-lookup"><span data-stu-id="f99af-296">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="f99af-297">Gegevenssets</span><span class="sxs-lookup"><span data-stu-id="f99af-297">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="f99af-298">Op basis van dit artikel krijgt u inzicht in de gegevenssets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f99af-298">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="f99af-299">Plannen en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="f99af-299">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="f99af-300">In dit artikel wordt uitleg gegeven over de plannings- en uitvoeringsaspecten van het Azure Data Factory-toepassingsmodel.</span><span class="sxs-lookup"><span data-stu-id="f99af-300">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="f99af-301">Pijplijnen bewaken en beheren met de app voor bewaking en beheer</span><span class="sxs-lookup"><span data-stu-id="f99af-301">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="f99af-302">In dit artikel wordt beschreven hoe u pijplijnen bewaakt en beheert en hoe u fouten hierin oplost met de app voor bewaking en beheer.</span><span class="sxs-lookup"><span data-stu-id="f99af-302">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
