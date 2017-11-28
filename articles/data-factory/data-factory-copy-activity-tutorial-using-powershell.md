---
title: 'Zelfstudie: Een pijplijn toomove gegevens maken met behulp van Azure PowerShell | Microsoft Docs'
description: In deze zelfstudie maakt u een Azure Data Factory-pijplijn met een kopieeractiviteit. Hiervoor gebruikt u Azure PowerShell.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 21406d7dfaa0c555b2538fbb52839d761c140fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a><span data-ttu-id="6bff2-103">Zelfstudie: Een Data Factory-pijplijn maken die gegevens verplaatst met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bff2-103">Tutorial: Create a Data Factory pipeline that moves data by using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6bff2-104">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="6bff2-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="6bff2-105">De wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="6bff2-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="6bff2-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6bff2-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="6bff2-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6bff2-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="6bff2-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bff2-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="6bff2-109">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="6bff2-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="6bff2-110">REST API</span><span class="sxs-lookup"><span data-stu-id="6bff2-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="6bff2-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="6bff2-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
>
>

<span data-ttu-id="6bff2-112">In dit artikel leert u hoe toouse PowerShell toocreate een gegevensfactory met een pijplijn waarmee gegevens worden gekopieerd van een Azure blob storage tooan Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="6bff2-112">In this article, you learn how toouse PowerShell toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="6bff2-113">Als u nieuwe tooAzure Data Factory, lees Hallo [inleiding tooAzure Data Factory](data-factory-introduction.md) artikel voordat u deze zelfstudie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="6bff2-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="6bff2-114">In deze zelfstudie maakt u een pijplijn met één activiteit erin: kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="6bff2-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="6bff2-115">Hallo kopieeractiviteit kopieert gegevens van een gegevensarchief voor ondersteunde gegevens store tooa ondersteunde sink.</span><span class="sxs-lookup"><span data-stu-id="6bff2-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="6bff2-116">Zie [Ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met gegevensarchieven die worden ondersteund als bron en als sink.</span><span class="sxs-lookup"><span data-stu-id="6bff2-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="6bff2-117">Hallo-activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens tussen verschillende gegevensarchieven op een manier veilig, betrouwbaar en schaalbaar kan worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="6bff2-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="6bff2-118">Zie voor meer informatie over Hallo Kopieeractiviteit [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6bff2-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="6bff2-119">Een pijplijn kan meer dan één activiteit hebben.</span><span class="sxs-lookup"><span data-stu-id="6bff2-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="6bff2-120">En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="6bff2-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="6bff2-121">Zie [Meerdere activiteiten in een pijplijn](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6bff2-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="6bff2-122">In dit artikel omvat niet alle Hallo Data Factory-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="6bff2-122">This article does not cover all hello Data Factory cmdlets.</span></span> <span data-ttu-id="6bff2-123">Zie [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) (Naslaginformatie voor Data Factory-cmdlets) voor uitgebreide documentatie over deze cmdlets.</span><span class="sxs-lookup"><span data-stu-id="6bff2-123">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on these cmdlets.</span></span>
> 
> <span data-ttu-id="6bff2-124">Hallo data pipeline in deze zelfstudie worden gegevens gekopieerd van een bron data store tooa doelgegevensopslagplaats.</span><span class="sxs-lookup"><span data-stu-id="6bff2-124">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="6bff2-125">Voor een zelfstudie over het tootransform van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: een pijplijn tootransform gegevens met Hadoop-cluster bouwen](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="6bff2-125">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bff2-126">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6bff2-126">Prerequisites</span></span>
- <span data-ttu-id="6bff2-127">Voldoen aan vereisten die worden vermeld in Hallo [vereisten voor de zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="6bff2-127">Complete prerequisites listed in hello [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article.</span></span>
- <span data-ttu-id="6bff2-128">Installeer **Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="6bff2-128">Install **Azure PowerShell**.</span></span> <span data-ttu-id="6bff2-129">Volg de instructies in Hallo [hoe tooinstall en configureren van Azure PowerShell](../powershell-install-configure.md).</span><span class="sxs-lookup"><span data-stu-id="6bff2-129">Follow hello instructions in [How tooinstall and configure Azure PowerShell](../powershell-install-configure.md).</span></span>

## <a name="steps"></a><span data-ttu-id="6bff2-130">Stappen</span><span class="sxs-lookup"><span data-stu-id="6bff2-130">Steps</span></span>
<span data-ttu-id="6bff2-131">Hier volgen Hallo stappen die u als onderdeel van deze zelfstudie uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6bff2-131">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="6bff2-132">Een Azure-**gegevensfactory** maken.</span><span class="sxs-lookup"><span data-stu-id="6bff2-132">Create an Azure **data factory**.</span></span> <span data-ttu-id="6bff2-133">In deze stap maakt u een gegevensfactory met de naam ADFTutorialDataFactoryPSH.</span><span class="sxs-lookup"><span data-stu-id="6bff2-133">In this step, you create a data factory named ADFTutorialDataFactoryPSH.</span></span> 
2. <span data-ttu-id="6bff2-134">Maak **gekoppelde services** in Hallo gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="6bff2-134">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="6bff2-135">In deze stap maakt u twee gekoppelde services van het type: Azure Storage en Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="6bff2-135">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="6bff2-136">Hallo AzureStorageLinkedService koppelt u uw Azure storage-account toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="6bff2-136">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="6bff2-137">U hebt gemaakt van een container en gegevens toothis opslagaccount geüpload als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="6bff2-137">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="6bff2-138">Azuresqllinkedservice wordt uw Azure SQL database toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="6bff2-138">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="6bff2-139">Hallo-gegevens die worden gekopieerd van de blob-opslag hello wordt opgeslagen in deze database.</span><span class="sxs-lookup"><span data-stu-id="6bff2-139">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="6bff2-140">Als onderdeel van de [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) hebt u een SQL-tabel in deze database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6bff2-140">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
3. <span data-ttu-id="6bff2-141">Maken van de invoer en uitvoer **gegevenssets** in Hallo gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="6bff2-141">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="6bff2-142">Hallo gekoppelde Azure storage-service geeft Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op uitvoeringstijd tooconnect tooyour Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="6bff2-142">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="6bff2-143">En Hallo blob-invoerbron gegevensset geeft Hallo-container en Hallo-map met invoergegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="6bff2-143">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="6bff2-144">Op deze manier geeft hello Azure SQL Database gekoppeld service Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op de runtime tooconnect tooyour Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="6bff2-144">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="6bff2-145">En SQL Hallo-tabel uitvoergegevensset geeft Hallo-tabel in Hallo toowhich Hallo databasegegevens van Hallo blob-opslag is gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="6bff2-145">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
4. <span data-ttu-id="6bff2-146">Maak een **pijplijn** in Hallo gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="6bff2-146">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="6bff2-147">In deze stap maakt u een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="6bff2-147">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="6bff2-148">Hallo kopieeractiviteit kopieert gegevens van een blob in hello Azure blob storage tooa tabel in hello Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="6bff2-148">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="6bff2-149">U kunt een kopieeractiviteit gebruiken in een pijplijn toocopy gegevens van het doel van een ondersteunde bron-tooany ondersteund.</span><span class="sxs-lookup"><span data-stu-id="6bff2-149">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="6bff2-150">Zie het artikel [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met ondersteunde gegevensarchieven.</span><span class="sxs-lookup"><span data-stu-id="6bff2-150">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
5. <span data-ttu-id="6bff2-151">Hallo-pijplijn bewaken.</span><span class="sxs-lookup"><span data-stu-id="6bff2-151">Monitor hello pipeline.</span></span> <span data-ttu-id="6bff2-152">In deze stap maakt u **monitor** Hallo segmenten van de invoer- en uitvoergegevenssets met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6bff2-152">In this step, you **monitor** hello slices of input and output datasets by using PowerShell.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="6bff2-153">Een data factory maken</span><span class="sxs-lookup"><span data-stu-id="6bff2-153">Create a data factory</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6bff2-154">Volledige [vereisten voor Hallo zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) als u dat nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="6bff2-154">Complete [prerequisites for hello tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.</span></span>   

<span data-ttu-id="6bff2-155">Een gegevensfactory kan één of meer pijplijnen hebben.</span><span class="sxs-lookup"><span data-stu-id="6bff2-155">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="6bff2-156">Een pijplijn kan één of meer activiteiten bevatten.</span><span class="sxs-lookup"><span data-stu-id="6bff2-156">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="6bff2-157">Bijvoorbeeld invoergegevens een Kopieeractiviteit toocopy-gegevens van een doelgegevensopslagplaats tooa bron en het toorun in een HDInsight Hive-activiteit een Hive-script tootransform gegevens tooproduct uitvoer.</span><span class="sxs-lookup"><span data-stu-id="6bff2-157">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="6bff2-158">Laten we beginnen met het maken van de gegevensfactory Hallo in deze stap.</span><span class="sxs-lookup"><span data-stu-id="6bff2-158">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="6bff2-159">Start **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="6bff2-159">Launch **PowerShell**.</span></span> <span data-ttu-id="6bff2-160">Houd Azure PowerShell open tot Hallo einde van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6bff2-160">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="6bff2-161">Als u sluiten en opnieuw opent, moet u toorun Hallo opdrachten opnieuw.</span><span class="sxs-lookup"><span data-stu-id="6bff2-161">If you close and reopen, you need toorun hello commands again.</span></span>

    <span data-ttu-id="6bff2-162">Hallo volgende opdracht uitvoeren en voert u Hallo-gebruikersnaam en wachtwoord toosign in toohello Azure-portal te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="6bff2-162">Run hello following command, and enter hello user name and password that you use toosign in toohello Azure portal:</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    <span data-ttu-id="6bff2-163">Voer Hallo opdracht tooview na alle Hallo abonnementen voor dit account:</span><span class="sxs-lookup"><span data-stu-id="6bff2-163">Run hello following command tooview all hello subscriptions for this account:</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="6bff2-164">Hallo opdracht tooselect Hallo abonnement dat u wilt dat toowork met volgende worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6bff2-164">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="6bff2-165">Vervang  **&lt;NameOfAzureSubscription** &gt; met Hallo-naam van uw Azure-abonnement:</span><span class="sxs-lookup"><span data-stu-id="6bff2-165">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription:</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. <span data-ttu-id="6bff2-166">Maak een Azure-resourcegroep met de naam **ADFTutorialResourceGroup** door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="6bff2-166">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    <span data-ttu-id="6bff2-167">Sommige van Hallo stappen in deze zelfstudie wordt ervan uitgegaan dat u het Hallo-resourcegroep met de naam **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="6bff2-167">Some of hello steps in this tutorial assume that you use hello resource group named **ADFTutorialResourceGroup**.</span></span> <span data-ttu-id="6bff2-168">Als u een andere resourcegroep gebruikt, moet u toouse deze in plaats van ADFTutorialResourceGroup in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6bff2-168">If you use a different resource group, you need toouse it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="6bff2-169">Voer Hallo **New-AzureRmDataFactory** cmdlet toocreate een gegevensfactory met de naam **ADFTutorialDataFactoryPSH**:</span><span class="sxs-lookup"><span data-stu-id="6bff2-169">Run hello **New-AzureRmDataFactory** cmdlet toocreate a data factory named **ADFTutorialDataFactoryPSH**:</span></span>  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    <span data-ttu-id="6bff2-170">Deze naam is mogelijk al in gebruik.</span><span class="sxs-lookup"><span data-stu-id="6bff2-170">This name may already have been taken.</span></span> <span data-ttu-id="6bff2-171">Zorg daarom Hallo-naam van de gegevensfactory Hallo unieke door toe te voegen voor- of achtervoegsel (bijvoorbeeld: ADFTutorialDataFactoryPSH05152017) en Voer Hallo opdracht opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="6bff2-171">Therefore, make hello name of hello data factory unique by adding a prefix or suffix (for example: ADFTutorialDataFactoryPSH05152017) and run hello command again.</span></span>  

<span data-ttu-id="6bff2-172">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="6bff2-172">Note hello following points:</span></span>

* <span data-ttu-id="6bff2-173">Hallo-naam van hello Azure-gegevensfactory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="6bff2-173">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="6bff2-174">Als u de volgende fout Hallo ontvangt, moet u Hallo-naam (bijvoorbeeld in Uwnaamadfstutorialdatafactorypsh) wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6bff2-174">If you receive hello following error, change hello name (for example, yournameADFTutorialDataFactoryPSH).</span></span> <span data-ttu-id="6bff2-175">Gebruik deze naam in plaats van ADFTutorialFactoryPSH tijdens het uitvoeren van de stappen in de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6bff2-175">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="6bff2-176">Raadpleeg [Data Factory - Naming Rules](data-factory-naming-rules.md) (Data Factory - Naamgevingsregels) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="6bff2-176">See [Data Factory - Naming Rules](data-factory-naming-rules.md) for Data Factory artifacts.</span></span>

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* <span data-ttu-id="6bff2-177">toocreate Data Factory-exemplaren, moet u een bijdrager of de beheerder van hello Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="6bff2-177">toocreate Data Factory instances, you must be a contributor or administrator of hello Azure subscription.</span></span>
* <span data-ttu-id="6bff2-178">Hallo-naam van de gegevensfactory Hallo mogelijk geregistreerd als DNS-naam in toekomstige hello, en daarom ook openbaar zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="6bff2-178">hello name of hello data factory may be registered as a DNS name in hello future, and hence become publicly visible.</span></span>
* <span data-ttu-id="6bff2-179">U ontvangt mogelijk Hallo volgende fout: "**dit abonnement is niet geregistreerd toouse namespace Microsoft.DataFactory.**'</span><span class="sxs-lookup"><span data-stu-id="6bff2-179">You may receive hello following error: "**This subscription is not registered toouse namespace Microsoft.DataFactory.**"</span></span> <span data-ttu-id="6bff2-180">Voer een van de volgende Hallo en probeer opnieuw te publiceren:</span><span class="sxs-lookup"><span data-stu-id="6bff2-180">Do one of hello following, and try publishing again:</span></span>

  * <span data-ttu-id="6bff2-181">Voer in Azure PowerShell Hallo opdracht tooregister Hallo Data Factory-provider te volgen:</span><span class="sxs-lookup"><span data-stu-id="6bff2-181">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    <span data-ttu-id="6bff2-182">Voer Hallo opdracht tooconfirm te volgen die Hallo Data Factory-provider wordt geregistreerd:</span><span class="sxs-lookup"><span data-stu-id="6bff2-182">Run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="6bff2-183">Meld u aan met behulp van Azure-abonnement toohello Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6bff2-183">Sign in by using hello Azure subscription toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6bff2-184">Ga tooa Data Factory-blade of maak een gegevensfactory in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6bff2-184">Go tooa Data Factory blade, or create a data factory in hello Azure portal.</span></span> <span data-ttu-id="6bff2-185">Deze actie automatisch Hallo provider voor u geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="6bff2-185">This action automatically registers hello provider for you.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="6bff2-186">Gekoppelde services maken</span><span class="sxs-lookup"><span data-stu-id="6bff2-186">Create linked services</span></span>
<span data-ttu-id="6bff2-187">U maken gekoppelde services in een data factory-toolink uw gegevens worden opgeslagen en compute services toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="6bff2-187">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="6bff2-188">In deze zelfstudie gebruikt u niet een willekeurige compute-service, zoals Azure HDInsight of Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6bff2-188">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="6bff2-189">U gebruikt twee gegevensarchieven van het type Azure Storage (bron) en Azure SQL Database (doel).</span><span class="sxs-lookup"><span data-stu-id="6bff2-189">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="6bff2-190">Daarom maakt u twee gekoppelde services met de naam AzureStorageLinkedService en AzureSqlLinkedService van het type: AzureStorage en AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="6bff2-190">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="6bff2-191">Hallo AzureStorageLinkedService koppelt u uw Azure storage-account toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="6bff2-191">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="6bff2-192">Dit opslagaccount wordt Hallo een waarop u container gemaakt en Hallo gegevens geüpload als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="6bff2-192">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="6bff2-193">Azuresqllinkedservice wordt uw Azure SQL database toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="6bff2-193">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="6bff2-194">Hallo-gegevens die worden gekopieerd van de blob-opslag hello wordt opgeslagen in deze database.</span><span class="sxs-lookup"><span data-stu-id="6bff2-194">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="6bff2-195">Hallo emp-tabel in deze database wordt gemaakt als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="6bff2-195">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="6bff2-196">Een gekoppelde service maken voor een Azure-opslagaccount</span><span class="sxs-lookup"><span data-stu-id="6bff2-196">Create a linked service for an Azure storage account</span></span>
<span data-ttu-id="6bff2-197">In deze stap koppelt u uw Azure storage-account tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="6bff2-197">In this step, you link your Azure storage account tooyour data factory.</span></span>

1. <span data-ttu-id="6bff2-198">Maak een JSON-bestand met de naam **AzureStorageLinkedService.json** in **C:\ADFGetStartedPSH** map met inhoud na Hallo: (maken Hallo map ADFGetStartedPSH als deze nog niet bestaat).</span><span class="sxs-lookup"><span data-stu-id="6bff2-198">Create a JSON file named **AzureStorageLinkedService.json** in **C:\ADFGetStartedPSH** folder with hello following content: (Create hello folder ADFGetStartedPSH if it does not already exist.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6bff2-199">Vervang &lt;accountname&gt; en &lt;accountkey&gt; met de naam en sleutel van uw Azure storage-account voordat het Hallo-bestand op te slaan.</span><span class="sxs-lookup"><span data-stu-id="6bff2-199">Replace &lt;accountname&gt; and &lt;accountkey&gt; with name and key of your Azure storage account before saving hello file.</span></span> 

    ```json
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
2. <span data-ttu-id="6bff2-200">In **Azure PowerShell**, switch toohello **ADFGetStartedPSH** map.</span><span class="sxs-lookup"><span data-stu-id="6bff2-200">In **Azure PowerShell**, switch toohello **ADFGetStartedPSH** folder.</span></span>
4. <span data-ttu-id="6bff2-201">Voer Hallo **New-AzureRmDataFactoryLinkedService** cmdlet toocreate Hallo gekoppelde service: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="6bff2-201">Run hello **New-AzureRmDataFactoryLinkedService** cmdlet toocreate hello linked service: **AzureStorageLinkedService**.</span></span> <span data-ttu-id="6bff2-202">Deze cmdlet en andere Data Factory-cmdlets die u gebruikt in deze zelfstudie moeten u toopass waarden voor Hallo **ResourceGroupName** en **DataFactoryName** parameters.</span><span class="sxs-lookup"><span data-stu-id="6bff2-202">This cmdlet, and other Data Factory cmdlets you use in this tutorial requires you toopass values for hello **ResourceGroupName** and **DataFactoryName** parameters.</span></span> <span data-ttu-id="6bff2-203">U kunt ook doorgeven Hallo DataFactory-object geretourneerd door Hallo New-AzureRmDataFactory cmdlet zonder te hoeven typen ResourceGroupName en DataFactoryName telkens wanneer die u een cmdlet uitvoert.</span><span class="sxs-lookup"><span data-stu-id="6bff2-203">Alternatively, you can pass hello DataFactory object returned by hello New-AzureRmDataFactory cmdlet without typing ResourceGroupName and DataFactoryName each time you run a cmdlet.</span></span> 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    <span data-ttu-id="6bff2-204">Hier volgt voorbeelduitvoer Hallo:</span><span class="sxs-lookup"><span data-stu-id="6bff2-204">Here is hello sample output:</span></span>

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    <span data-ttu-id="6bff2-205">Andere manier voor het maken van deze gekoppelde service is toospecify Resourcegroepnaam en de naam gegevensfactory in plaats van Hallo DataFactory-object opgeven.</span><span class="sxs-lookup"><span data-stu-id="6bff2-205">Other way of creating this linked service is toospecify resource group name and data factory name instead of specifying hello DataFactory object.</span></span>  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a><span data-ttu-id="6bff2-206">Een gekoppelde service maken voor een Azure SQL-database</span><span class="sxs-lookup"><span data-stu-id="6bff2-206">Create a linked service for an Azure SQL database</span></span>
<span data-ttu-id="6bff2-207">In deze stap koppelt u uw Azure SQL database tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="6bff2-207">In this step, you link your Azure SQL database tooyour data factory.</span></span>

1. <span data-ttu-id="6bff2-208">Maak een JSON-bestand met de naam AzureSqlLinkedService.json in de map C:\ADFGetStartedPSH Hello volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="6bff2-208">Create a JSON file named AzureSqlLinkedService.json in C:\ADFGetStartedPSH folder with hello following content:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6bff2-209">Vervang &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt; en &lt;password&gt; door de namen van uw Azure SQL-server, database, gebruiker en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="6bff2-209">Replace &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt;, and &lt;password&gt; with names of your Azure SQL server, database, user account, and password.</span></span>
    
    ```json
    {
        "name": "AzureSqlLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<server>.database.windows.net,1433;Database=<databasename>;User ID=<user>@<server>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
     }
    ```
2. <span data-ttu-id="6bff2-210">Voer Hallo opdracht toocreate na een gekoppelde service:</span><span class="sxs-lookup"><span data-stu-id="6bff2-210">Run hello following command toocreate a linked service:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    <span data-ttu-id="6bff2-211">Hier volgt voorbeelduitvoer Hallo:</span><span class="sxs-lookup"><span data-stu-id="6bff2-211">Here is hello sample output:</span></span>

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   <span data-ttu-id="6bff2-212">Bevestig dat **tooAzure-services toegang toestaan** instelling is ingeschakeld voor uw SQL database-server.</span><span class="sxs-lookup"><span data-stu-id="6bff2-212">Confirm that **Allow access tooAzure services** setting is turned on for your SQL database server.</span></span> <span data-ttu-id="6bff2-213">tooverify en weer in, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="6bff2-213">tooverify and turn it on, do hello following steps:</span></span>

    1. <span data-ttu-id="6bff2-214">Meld u bij toohello [Azure-portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="6bff2-214">Log in toohello [Azure portal](https://portal.azure.com)</span></span>
    2. <span data-ttu-id="6bff2-215">Klik op **meer services >** op Hallo linkerkant en klik op **SQL-servers** in Hallo **DATABASES** categorie.</span><span class="sxs-lookup"><span data-stu-id="6bff2-215">Click **More services >** on hello left, and click **SQL servers** in hello **DATABASES** category.</span></span>
    3. <span data-ttu-id="6bff2-216">Selecteer uw server in de lijst Hallo van SQL-servers.</span><span class="sxs-lookup"><span data-stu-id="6bff2-216">Select your server in hello list of SQL servers.</span></span>
    4. <span data-ttu-id="6bff2-217">Klik op Hallo SQL server-blade **firewall-instellingen weergeven** koppeling.</span><span class="sxs-lookup"><span data-stu-id="6bff2-217">On hello SQL server blade, click **Show firewall settings** link.</span></span>
    5. <span data-ttu-id="6bff2-218">In Hallo **Firewall-instellingen** blade, klikt u op **ON** voor **tooAzure-services toegang toestaan**.</span><span class="sxs-lookup"><span data-stu-id="6bff2-218">In hello **Firewall settings** blade, click **ON** for **Allow access tooAzure services**.</span></span>
    6. <span data-ttu-id="6bff2-219">Klik op **opslaan** op Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="6bff2-219">Click **Save** on hello toolbar.</span></span> 

## <a name="create-datasets"></a><span data-ttu-id="6bff2-220">Gegevenssets maken</span><span class="sxs-lookup"><span data-stu-id="6bff2-220">Create datasets</span></span>
<span data-ttu-id="6bff2-221">In de vorige stap Hallo gemaakt gekoppelde services toolink uw Azure Storage-account en de Azure SQL database tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="6bff2-221">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="6bff2-222">In deze stap definieert u twee gegevenssets met de naam InputDataset en OutputDataset die vertegenwoordigen de invoer- en uitvoergegevens die zijn opgeslagen in Hallo gegevensarchieven waarnaar wordt verwezen door de AzureStorageLinkedService en AzureSqlLinkedService respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="6bff2-222">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="6bff2-223">Hallo gekoppelde Azure storage-service geeft Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op uitvoeringstijd tooconnect tooyour Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="6bff2-223">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="6bff2-224">En Hallo blob-invoerbron gegevensset (InputDataset) geeft Hallo-container en Hallo-map met invoergegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="6bff2-224">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="6bff2-225">Op deze manier geeft hello Azure SQL Database gekoppeld service Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op de runtime tooconnect tooyour Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="6bff2-225">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="6bff2-226">En Hallo uitvoer gegevensset met SQL-tabel (OututDataset) geeft Hallo tabel in Hallo database toowhich Hallo gegevens uit Hallo blob-opslag worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="6bff2-226">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-an-input-dataset"></a><span data-ttu-id="6bff2-227">Een invoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="6bff2-227">Create an input dataset</span></span>
<span data-ttu-id="6bff2-228">In deze stap maakt u een gegevensset met de naam InputDataset die tooa blob-bestand (emp.txt) verwijst in de hoofdmap Hallo van een blob-container (adftutorial) in hello Azure Storage dat wordt vertegenwoordigd door Hallo gekoppelde AzureStorageLinkedService-service.</span><span class="sxs-lookup"><span data-stu-id="6bff2-228">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="6bff2-229">Als u niet een waarde voor fileName hello opgeven (of overslaan), zijn gegevens uit alle blobs in de invoermap Hallo gekopieerde toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="6bff2-229">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="6bff2-230">In deze zelfstudie maakt opgeven u een waarde voor Hallo fileName.</span><span class="sxs-lookup"><span data-stu-id="6bff2-230">In this tutorial, you specify a value for hello fileName.</span></span>  

1. <span data-ttu-id="6bff2-231">Maak een JSON-bestand met de naam **InputDataset.json** in Hallo **C:\ADFGetStartedPSH** map Hello volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="6bff2-231">Create a JSON file named **InputDataset.json** in hello **C:\ADFGetStartedPSH** folder, with hello following content:</span></span>

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
                "fileName": "emp.txt",
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

    <span data-ttu-id="6bff2-232">Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:</span><span class="sxs-lookup"><span data-stu-id="6bff2-232">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="6bff2-233">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="6bff2-233">Property</span></span> | <span data-ttu-id="6bff2-234">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6bff2-234">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="6bff2-235">type</span><span class="sxs-lookup"><span data-stu-id="6bff2-235">type</span></span> | <span data-ttu-id="6bff2-236">Hallo type wordt ingesteld te**AzureBlob** omdat de gegevens zich in een Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="6bff2-236">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="6bff2-237">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="6bff2-237">linkedServiceName</span></span> | <span data-ttu-id="6bff2-238">Toohello verwijst **AzureStorageLinkedService** die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6bff2-238">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="6bff2-239">folderPath</span><span class="sxs-lookup"><span data-stu-id="6bff2-239">folderPath</span></span> | <span data-ttu-id="6bff2-240">Hiermee geeft u op Hallo blob **container** en Hallo **map** die invoer blobs bevat.</span><span class="sxs-lookup"><span data-stu-id="6bff2-240">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="6bff2-241">In deze zelfstudie adftutorial is Hallo blob-container en map Hallo-hoofdmap is.</span><span class="sxs-lookup"><span data-stu-id="6bff2-241">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="6bff2-242">fileName</span><span class="sxs-lookup"><span data-stu-id="6bff2-242">fileName</span></span> | <span data-ttu-id="6bff2-243">Deze eigenschap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="6bff2-243">This property is optional.</span></span> <span data-ttu-id="6bff2-244">Als u deze eigenschap niet opgeeft, worden alle bestanden uit folderPath Hallo opgenomen.</span><span class="sxs-lookup"><span data-stu-id="6bff2-244">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="6bff2-245">In deze zelfstudie **emp.txt** hello bestandsnaam, zodat alleen dat bestand wordt opgehaald voor de verwerking wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6bff2-245">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="6bff2-246">format -> type</span><span class="sxs-lookup"><span data-stu-id="6bff2-246">format -> type</span></span> |<span data-ttu-id="6bff2-247">Hallo-bestand voor invoer is in de indeling van de tekst hello, zodat we gebruiken **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="6bff2-247">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="6bff2-248">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="6bff2-248">columnDelimiter</span></span> | <span data-ttu-id="6bff2-249">Hallo-kolommen in het invoerbestand Hallo worden gescheiden door **kommateken (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="6bff2-249">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="6bff2-250">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="6bff2-250">frequency/interval</span></span> | <span data-ttu-id="6bff2-251">Hallo frequentie te is ingesteld**uur** en interval is ingesteld, te**1**, wat betekent dat Hallo invoer segmenten zijn beschikbaar **per uur**.</span><span class="sxs-lookup"><span data-stu-id="6bff2-251">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="6bff2-252">Met andere woorden, Hallo Data Factory-service zoekt invoergegevens elk uur in de hoofdmap Hallo van blob-container (**adftutorial**) u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6bff2-252">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="6bff2-253">Hallo-gegevens binnen Hallo pijplijn begin- en tijden, niet voor of na deze tijden zoekt.</span><span class="sxs-lookup"><span data-stu-id="6bff2-253">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="6bff2-254">external</span><span class="sxs-lookup"><span data-stu-id="6bff2-254">external</span></span> | <span data-ttu-id="6bff2-255">Deze eigenschap is ingesteld, te**true** als Hallo gegevens niet worden gegenereerd door deze pijplijn.</span><span class="sxs-lookup"><span data-stu-id="6bff2-255">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="6bff2-256">Hallo invoergegevens in deze zelfstudie wordt Hallo emp.txt bestand, die niet worden gegenereerd door deze pipeline, zodat we de tootrue van deze eigenschap wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6bff2-256">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="6bff2-257">Zie het [artikel over Azure Blob-connectoren](data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over deze JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="6bff2-257">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="6bff2-258">Voer Hallo opdracht toocreate Hallo Data Factory-gegevensset te volgen.</span><span class="sxs-lookup"><span data-stu-id="6bff2-258">Run hello following command toocreate hello Data Factory dataset.</span></span>

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    <span data-ttu-id="6bff2-259">Hier volgt voorbeelduitvoer Hallo:</span><span class="sxs-lookup"><span data-stu-id="6bff2-259">Here is hello sample output:</span></span>

    ```
    DatasetName       : InputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureBlobDataset
    Policy            : Microsoft.Azure.Management.DataFactories.Common.Models.Policy
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

### <a name="create-an-output-dataset"></a><span data-ttu-id="6bff2-260">Een uitvoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="6bff2-260">Create an output dataset</span></span>
<span data-ttu-id="6bff2-261">In dit deel van stap hello, maakt u een uitvoergegevensset met de naam **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="6bff2-261">In this part of hello step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="6bff2-262">Deze gegevensset verwijst tooa SQL-tabel in hello Azure SQL-database dat wordt vertegenwoordigd door **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="6bff2-262">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService**.</span></span> 

1. <span data-ttu-id="6bff2-263">Maak een JSON-bestand met de naam **OutputDataset.json** in Hallo **C:\ADFGetStartedPSH** map Hello volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="6bff2-263">Create a JSON file named **OutputDataset.json** in hello **C:\ADFGetStartedPSH** folder with hello following content:</span></span>

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

    <span data-ttu-id="6bff2-264">Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:</span><span class="sxs-lookup"><span data-stu-id="6bff2-264">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="6bff2-265">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="6bff2-265">Property</span></span> | <span data-ttu-id="6bff2-266">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6bff2-266">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="6bff2-267">type</span><span class="sxs-lookup"><span data-stu-id="6bff2-267">type</span></span> | <span data-ttu-id="6bff2-268">Hallo type wordt ingesteld te**AzureSqlTable** omdat gegevens gekopieerde tooa tabel in een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="6bff2-268">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="6bff2-269">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="6bff2-269">linkedServiceName</span></span> | <span data-ttu-id="6bff2-270">Toohello verwijst **AzureSqlLinkedService** die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6bff2-270">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="6bff2-271">tableName</span><span class="sxs-lookup"><span data-stu-id="6bff2-271">tableName</span></span> | <span data-ttu-id="6bff2-272">Opgegeven Hallo **tabel** toowhich Hallo gegevens worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="6bff2-272">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="6bff2-273">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="6bff2-273">frequency/interval</span></span> | <span data-ttu-id="6bff2-274">Hallo frequentie is ingesteld te**uur** en interval is **1**, wat betekent dat Hallo uitvoer segmenten worden geproduceerd **per uur** tussen Hallo pijplijn begin- en tijden niet voor of na deze tijden.</span><span class="sxs-lookup"><span data-stu-id="6bff2-274">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="6bff2-275">Er zijn drie kolommen – **ID**, **FirstName**, en **LastName** – in Hallo emp-tabel in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="6bff2-275">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="6bff2-276">-ID is een identiteitskolom, dus u alleen toospecify hoeft **FirstName** en **LastName** hier.</span><span class="sxs-lookup"><span data-stu-id="6bff2-276">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="6bff2-277">Zie het [artikel over Azure SQL-connectoren](data-factory-azure-sql-connector.md#dataset-properties) voor meer informatie over deze JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="6bff2-277">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="6bff2-278">Voer Hallo opdracht toocreate Hallo data factory-gegevensset te volgen.</span><span class="sxs-lookup"><span data-stu-id="6bff2-278">Run hello following command toocreate hello data factory dataset.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    <span data-ttu-id="6bff2-279">Hier volgt voorbeelduitvoer Hallo:</span><span class="sxs-lookup"><span data-stu-id="6bff2-279">Here is hello sample output:</span></span>

    ```
    DatasetName       : OutputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureSqlTableDataset
    Policy            :
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

## <a name="create-a-pipeline"></a><span data-ttu-id="6bff2-280">Een pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="6bff2-280">Create a pipeline</span></span>
<span data-ttu-id="6bff2-281">In deze stap maakt u een pijplijn met een **kopieeractiviteit** die gebruikmaakt van **InputDataset** als invoer en **OutputDataset** als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="6bff2-281">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="6bff2-282">Uitvoergegevensset is momenteel welke stations Hallo planning.</span><span class="sxs-lookup"><span data-stu-id="6bff2-282">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="6bff2-283">In deze zelfstudie is uitvoergegevensset geconfigureerde tooproduce een segment eens per uur.</span><span class="sxs-lookup"><span data-stu-id="6bff2-283">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="6bff2-284">Hallo pijplijn heeft een begintijd en eindtijd die één dag uit elkaar liggen, wat is 24 uur zijn.</span><span class="sxs-lookup"><span data-stu-id="6bff2-284">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="6bff2-285">Daarom worden 24 segmenten van uitvoergegevensset geproduceerd door Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="6bff2-285">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 


1. <span data-ttu-id="6bff2-286">Maak een JSON-bestand met de naam **ADFTutorialPipeline.json** in Hallo **C:\ADFGetStartedPSH** map Hello volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="6bff2-286">Create a JSON file named **ADFTutorialPipeline.json** in hello **C:\ADFGetStartedPSH** folder, with hello following content:</span></span>

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
    <span data-ttu-id="6bff2-287">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="6bff2-287">Note hello following points:</span></span>
   
    - <span data-ttu-id="6bff2-288">In Hallo gedeelte activiteiten is er slechts één activiteit waarvan **type** te is ingesteld,**kopie**.</span><span class="sxs-lookup"><span data-stu-id="6bff2-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="6bff2-289">Zie voor meer informatie over de kopieeractiviteit hello [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6bff2-289">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="6bff2-290">In Data Factory-oplossingen kunt u ook [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6bff2-290">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="6bff2-291">Invoer voor Hallo-activiteit is ingesteld, te**InputDataset** en de uitvoer voor Hallo activiteit te is ingesteld**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="6bff2-291">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="6bff2-292">In Hallo **typeProperties** sectie **BlobSource** is opgegeven als Hallo brontype en **SqlSink** is opgegeven als Hallo sink-type.</span><span class="sxs-lookup"><span data-stu-id="6bff2-292">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="6bff2-293">Zie voor een volledige lijst van gegevensarchieven die worden ondersteund door Hallo kopieeractiviteit als bronnen en put [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="6bff2-293">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="6bff2-294">toolearn hoe toouse een specifieke ondersteunde gegevens opslaan als een bron/sink, klikt u op Hallo-koppeling in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="6bff2-294">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
     
    <span data-ttu-id="6bff2-295">Vervang de waarde Hallo Hallo **start** eigenschap met de huidige dag Hallo en **end** waarde met de volgende dag Hallo.</span><span class="sxs-lookup"><span data-stu-id="6bff2-295">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="6bff2-296">U kunt alleen Hallo datumgedeelte opgeven en Hallo tijdgedeelte van Hallo datum / tijd overslaan.</span><span class="sxs-lookup"><span data-stu-id="6bff2-296">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="6bff2-297">Bijvoorbeeld '2016-02-03', dat te gelijk ' 2016-02-03T00:00:00Z '</span><span class="sxs-lookup"><span data-stu-id="6bff2-297">For example, "2016-02-03", which is equivalent too"2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="6bff2-298">Zowel de begin- als einddatum en -tijd moeten de [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601) hebben.</span><span class="sxs-lookup"><span data-stu-id="6bff2-298">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="6bff2-299">Bijvoorbeeld: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="6bff2-299">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="6bff2-300">Hallo **end** tijd is optioneel, maar er worden gebruikt in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6bff2-300">hello **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="6bff2-301">Als u geen waarde voor Hallo opgeeft **end** eigenschap, wordt berekend als '**start + 48 uur**'.</span><span class="sxs-lookup"><span data-stu-id="6bff2-301">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="6bff2-302">toorun hello pijplijn voor onbepaalde tijd, geef **9999-09-09** als waarde voor Hallo Hallo **end** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="6bff2-302">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="6bff2-303">In de Hallo voorgaande voorbeeld, zijn er 24 gegevenssegmenten omdat elke gegevenssegment per uur is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6bff2-303">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="6bff2-304">Zie het artikel [Pijplijnen maken](data-factory-create-pipelines.md) voor beschrijvingen van JSON-eigenschappen in de definitie van een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="6bff2-304">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6bff2-305">Zie [Gegevensverplaatsingsactiviteiten](data-factory-data-movement-activities.md) voor beschrijvingen van JSON-eigenschappen in de definitie van een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="6bff2-305">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="6bff2-306">Zie het [artikel over Azure Blob-connectoren](data-factory-azure-blob-connector.md) voor beschrijvingen van JSON-eigenschappen die worden ondersteund door BlobSource.</span><span class="sxs-lookup"><span data-stu-id="6bff2-306">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="6bff2-307">Zie het [artikel over Azure SQL Database-connectoren](data-factory-azure-sql-connector.md) voor beschrijvingen van JSON-eigenschappen die worden ondersteund door SqlSink.</span><span class="sxs-lookup"><span data-stu-id="6bff2-307">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
2. <span data-ttu-id="6bff2-308">Voer Hallo opdracht toocreate Hallo data factory-tabel te volgen.</span><span class="sxs-lookup"><span data-stu-id="6bff2-308">Run hello following command toocreate hello data factory table.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    <span data-ttu-id="6bff2-309">Hier volgt voorbeelduitvoer Hallo:</span><span class="sxs-lookup"><span data-stu-id="6bff2-309">Here is hello sample output:</span></span> 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

<span data-ttu-id="6bff2-310">**Gefeliciteerd!**</span><span class="sxs-lookup"><span data-stu-id="6bff2-310">**Congratulations!**</span></span> <span data-ttu-id="6bff2-311">U hebt een Azure-gegevensfactory gemaakt met een pipeline toocopy-gegevens van een Azure blob storage tooan Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="6bff2-311">You have successfully created an Azure data factory with a pipeline toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> 

## <a name="monitor-hello-pipeline"></a><span data-ttu-id="6bff2-312">Hallo-pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="6bff2-312">Monitor hello pipeline</span></span>
<span data-ttu-id="6bff2-313">In deze stap gebruikt u Azure PowerShell toomonitor wat er gebeurt in een Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="6bff2-313">In this step, you use Azure PowerShell toomonitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="6bff2-314">Vervang &lt;DataFactoryName&gt; met de naam van uw gegevensfactory en het uitvoeren van Hallo **Get-AzureRmDataFactory**, en Hallo uitvoer tooa variabele $df toewijzen.</span><span class="sxs-lookup"><span data-stu-id="6bff2-314">Replace &lt;DataFactoryName&gt; with hello name of your data factory and run **Get-AzureRmDataFactory**, and assign hello output tooa variable $df.</span></span>

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    <span data-ttu-id="6bff2-315">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6bff2-315">For example:</span></span>
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    <span data-ttu-id="6bff2-316">Voer vervolgens de inhoud afdrukken Hallo $df toosee Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="6bff2-316">Then, run print hello contents of $df toosee hello following output:</span></span> 
    
    ```
    PS C:\ADFGetStartedPSH> $df
    
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DataFactoryId     : 6f194b34-03b3-49ab-8f03-9f8a7b9d3e30
    ResourceGroupName : ADFTutorialResourceGroup
    Location          : West US
    Tags              : {}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DataFactoryProperties
    ProvisioningState : Succeeded
    ```
2. <span data-ttu-id="6bff2-317">Uitvoeren **Get-AzureRmDataFactorySlice** tooget details over alle segmenten van Hallo **OutputDataset**, namelijk uitvoergegevensset Hallo van Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="6bff2-317">Run **Get-AzureRmDataFactorySlice** tooget details about all slices of hello **OutputDataset**, which is hello output dataset of hello pipeline.</span></span>  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   <span data-ttu-id="6bff2-318">Deze instelling moet overeenkomen met de Hallo **Start** waarde in de JSON van de Hallo-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="6bff2-318">This setting should match hello **Start** value in hello pipeline JSON.</span></span> <span data-ttu-id="6bff2-319">U ziet 24 segmenten; één voor elk uur vanaf 12: 00 A.M. van Hallo huidige dag too12 BEN Hallo volgende dag.</span><span class="sxs-lookup"><span data-stu-id="6bff2-319">You should see 24 slices, one for each hour from 12 AM of hello current day too12 AM of hello next day.</span></span>

   <span data-ttu-id="6bff2-320">Hier volgen drie voorbeeld segmenten van Hallo uitvoer:</span><span class="sxs-lookup"><span data-stu-id="6bff2-320">Here are three sample slices from hello output:</span></span> 

    ``` 
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 11:00:00 PM
    End               : 5/12/2017 12:00:00 AM
    RetryCount        : 0
    State             : Ready
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 9:00:00 PM
    End               : 5/11/2017 10:00:00 PM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0   

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 8:00:00 PM
    End               : 5/11/2017 9:00:00 PM
    RetryCount        : 0
    State             : Waiting
    SubState          : ConcurrencyLimit
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. <span data-ttu-id="6bff2-321">Voer **Get-AzureRmDataFactoryRun** tooget Hallo details van de activiteit wordt uitgevoerd voor een **specifieke** segment.</span><span class="sxs-lookup"><span data-stu-id="6bff2-321">Run **Get-AzureRmDataFactoryRun** tooget hello details of activity runs for a **specific** slice.</span></span> <span data-ttu-id="6bff2-322">Hallo datum / tijd-waarde van de uitvoer Hallo van Hallo vorige opdracht toospecify Hallo waarde voor Hallo StartDateTime parameter kopiëren.</span><span class="sxs-lookup"><span data-stu-id="6bff2-322">Copy hello date-time value from hello output of hello previous command toospecify hello value for hello StartDateTime parameter.</span></span> 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   <span data-ttu-id="6bff2-323">Hier volgt voorbeelduitvoer Hallo:</span><span class="sxs-lookup"><span data-stu-id="6bff2-323">Here is hello sample output:</span></span> 

    ```
    Id                  : c0ddbd75-d0c7-4816-a775-704bbd7c7eab_636301332000000000_636301368000000000_OutputDataset
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH0516
    DatasetName         : OutputDataset
    ProcessingStartTime : 5/16/2017 8:00:33 PM
    ProcessingEndTime   : 5/16/2017 8:01:36 PM
    PercentComplete     : 100
    DataSliceStart      : 5/11/2017 9:00:00 PM
    DataSliceEnd        : 5/11/2017 10:00:00 PM
    Status              : Succeeded
    Timestamp           : 5/16/2017 8:00:33 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy  
    ```

<span data-ttu-id="6bff2-324">Zie [Naslaginformatie voor Data Factory-cmdlets](/powershell/module/azurerm.datafactories) voor uitgebreide documentatie over Data Factory-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="6bff2-324">For comprehensive documentation on Data Factory cmdlets, see [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories).</span></span>

## <a name="summary"></a><span data-ttu-id="6bff2-325">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="6bff2-325">Summary</span></span>
<span data-ttu-id="6bff2-326">In deze zelfstudie maakt u een Azure data factory toocopy gegevens uit een Azure-blobopslag tooan Azure SQL database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6bff2-326">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="6bff2-327">U hebt PowerShell toocreate hello gegevensfactory, gekoppelde services, gegevenssets en een pijplijn gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6bff2-327">You used PowerShell toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="6bff2-328">Hier volgen Hallo hoofdstappen die u in deze zelfstudie hebt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="6bff2-328">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="6bff2-329">U hebt een Azure-**gegevensfactory** gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6bff2-329">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="6bff2-330">U hebt **gekoppelde services** gemaakt:</span><span class="sxs-lookup"><span data-stu-id="6bff2-330">Created **linked services**:</span></span>

   <span data-ttu-id="6bff2-331">a.</span><span class="sxs-lookup"><span data-stu-id="6bff2-331">a.</span></span> <span data-ttu-id="6bff2-332">Een **Azure Storage** gekoppelde service toolink uw Azure storage-account dat invoergegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="6bff2-332">An **Azure Storage** linked service toolink your Azure storage account that holds input data.</span></span>     
   <span data-ttu-id="6bff2-333">b.</span><span class="sxs-lookup"><span data-stu-id="6bff2-333">b.</span></span> <span data-ttu-id="6bff2-334">Een **Azure SQL** gekoppelde service toolink uw SQL-database die uitvoergegevens Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="6bff2-334">An **Azure SQL** linked service toolink your SQL database that holds hello output data.</span></span>
3. <span data-ttu-id="6bff2-335">U hebt **gegevenssets** gemaakt waarin de invoer- en uitvoergegevens van pijplijnen worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="6bff2-335">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="6bff2-336">Gemaakt een **pijplijn** met **Kopieeractiviteit**, met **BlobSource** als Hallo bron en **SqlSink** als Hallo sink.</span><span class="sxs-lookup"><span data-stu-id="6bff2-336">Created a **pipeline** with **Copy Activity**, with **BlobSource** as hello source and **SqlSink** as hello sink.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bff2-337">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6bff2-337">Next steps</span></span>
<span data-ttu-id="6bff2-338">In deze zelfstudie hebt u voor een kopieerbewerking een Azure Blob-opslag gebruikt als brongegevensarchief en een Azure SQL-database als doelgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="6bff2-338">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="6bff2-339">Hallo bevat volgende tabel een lijst met gegevensarchieven als bronnen en bestemmingen wordt ondersteund door Hallo kopieeractiviteit:</span><span class="sxs-lookup"><span data-stu-id="6bff2-339">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="6bff2-340">toolearn over hoe gegevens uit een data toocopy opslaan, klikt u op Hallo-koppeling voor de gegevensopslag Hallo in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="6bff2-340">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span> 

