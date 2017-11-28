---
title: aaaBuild uw eerste gegevensfactory (PowerShell) | Microsoft Docs
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
ms.openlocfilehash: 626260798b56d590577b3c4b24f7cf52873c9f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a><span data-ttu-id="36580-103">Zelfstudie: uw eerste Azure-gegevensfactory bouwen met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="36580-103">Tutorial: Build your first Azure data factory using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="36580-104">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="36580-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="36580-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="36580-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="36580-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="36580-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="36580-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="36580-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="36580-108">Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="36580-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="36580-109">REST API</span><span class="sxs-lookup"><span data-stu-id="36580-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

<span data-ttu-id="36580-110">In dit artikel gebruikt u Azure PowerShell toocreate uw eerste Azure-gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="36580-110">In this article, you use Azure PowerShell toocreate your first Azure data factory.</span></span> <span data-ttu-id="36580-111">toodo hello zelfstudie met andere hulpprogramma's / SDK, selecteer een van de Hallo opties uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="36580-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="36580-112">Hallo-pijplijn in deze zelfstudie is één activiteit: **HDInsight Hive-activiteit**.</span><span class="sxs-lookup"><span data-stu-id="36580-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="36580-113">Deze activiteit wordt een hive-script uitgevoerd op een Azure HDInsight-cluster dat transformaties invoergegevens gegevens tooproduce uitvoer.</span><span class="sxs-lookup"><span data-stu-id="36580-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="36580-114">Hallo pijplijn is geplande toorun wanneer een maand tussen Hallo begin- en eindtijden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="36580-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="36580-115">Hallo gegevens pijplijn in deze zelfstudie getransformeerd invoergegevens tooproduce uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="36580-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="36580-116">Er worden geen gegevens gekopieerd van een bron data store tooa doelgegevensopslagplaats.</span><span class="sxs-lookup"><span data-stu-id="36580-116">It does not copy data from a source data store tooa destination data store.</span></span> <span data-ttu-id="36580-117">Voor een zelfstudie over het toocopy van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: gegevens kopiëren van Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="36580-117">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="36580-118">Een pijplijn kan meer dan één activiteit hebben.</span><span class="sxs-lookup"><span data-stu-id="36580-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="36580-119">En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="36580-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="36580-120">Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="36580-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36580-121">Vereisten</span><span class="sxs-lookup"><span data-stu-id="36580-121">Prerequisites</span></span>
* <span data-ttu-id="36580-122">Lees [overzicht van de zelfstudie](data-factory-build-your-first-pipeline.md) artikel en volledige Hallo **vereiste** stappen.</span><span class="sxs-lookup"><span data-stu-id="36580-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="36580-123">Volg de instructies in [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) artikel tooinstall meest recente versie van Azure PowerShell op uw computer.</span><span class="sxs-lookup"><span data-stu-id="36580-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="36580-124">(optioneel) In dit artikel omvat niet alle Hallo Data Factory-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="36580-124">(optional) This article does not cover all hello Data Factory cmdlets.</span></span> <span data-ttu-id="36580-125">Zie [Naslaginformatie voor Data Factory-cmdlets](/powershell/module/azurerm.datafactories) (Data Factory Cmdlet Reference) voor uitgebreide documentatie over Data Factory-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="36580-125">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on Data Factory cmdlets.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="36580-126">Een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="36580-126">Create data factory</span></span>
<span data-ttu-id="36580-127">In deze stap gebruikt u Azure PowerShell toocreate een Azure-Gegevensfactory met de naam **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="36580-127">In this step, you use Azure PowerShell toocreate an Azure Data Factory named **FirstDataFactoryPSH**.</span></span> <span data-ttu-id="36580-128">Een gegevensfactory kan één of meer pijplijnen hebben.</span><span class="sxs-lookup"><span data-stu-id="36580-128">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="36580-129">Een pijplijn kan één of meer activiteiten bevatten.</span><span class="sxs-lookup"><span data-stu-id="36580-129">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="36580-130">Bijvoorbeeld invoergegevens een Kopieeractiviteit toocopy-gegevens van een doelgegevensopslagplaats tooa bron en het toorun in een HDInsight Hive-activiteit een Hive-script tootransform.</span><span class="sxs-lookup"><span data-stu-id="36580-130">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data.</span></span> <span data-ttu-id="36580-131">Laten we beginnen met het maken van de gegevensfactory Hallo in deze stap.</span><span class="sxs-lookup"><span data-stu-id="36580-131">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="36580-132">Open Azure PowerShell en Voer Hallo volgende opdracht uit.</span><span class="sxs-lookup"><span data-stu-id="36580-132">Start Azure PowerShell and run hello following command.</span></span> <span data-ttu-id="36580-133">Houd Azure PowerShell open tot Hallo einde van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="36580-133">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="36580-134">Als u sluiten en opnieuw opent, moet u toorun deze opdrachten opnieuw.</span><span class="sxs-lookup"><span data-stu-id="36580-134">If you close and reopen, you need toorun these commands again.</span></span>
   * <span data-ttu-id="36580-135">Voer Hallo volgende opdracht en Voer Hallo-gebruikersnaam en wachtwoord toosign in toohello Azure-portal te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="36580-135">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * <span data-ttu-id="36580-136">Hallo opdracht tooview na alle Hallo abonnementen voor dit account uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="36580-136">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * <span data-ttu-id="36580-137">Hallo opdracht tooselect Hallo abonnement dat u wilt dat toowork met volgende worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="36580-137">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="36580-138">Dit abonnement moet hetzelfde zijn als u die wordt gebruikt bij de Azure-portal Hallo HALLO hallo.</span><span class="sxs-lookup"><span data-stu-id="36580-138">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. <span data-ttu-id="36580-139">Maak een Azure-resourcegroep met de naam **ADFTutorialResourceGroup** door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="36580-139">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command:</span></span>
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    <span data-ttu-id="36580-140">Sommige van Hallo stappen in deze zelfstudie wordt ervan uitgegaan dat u het Hallo-resourcegroep met de naam ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="36580-140">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="36580-141">Als u een andere resourcegroep gebruikt, moet u toouse deze in plaats van ADFTutorialResourceGroup in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="36580-141">If you use a different resource group, you need toouse it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="36580-142">Voer Hallo **New-AzureRmDataFactory** cmdlet die wordt gemaakt van een gegevensfactory met de naam **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="36580-142">Run hello **New-AzureRmDataFactory** cmdlet that creates a data factory named **FirstDataFactoryPSH**.</span></span>

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
<span data-ttu-id="36580-143">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="36580-143">Note hello following points:</span></span>

* <span data-ttu-id="36580-144">Hallo-naam van hello Azure Data Factory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="36580-144">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="36580-145">Als u de foutmelding Hallo **Data factory-naam 'FirstDataFactoryPSH' is niet beschikbaar**, wijzig de naam van hello (bijvoorbeeld in yournameFirstDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="36580-145">If you receive hello error **Data factory name “FirstDataFactoryPSH” is not available**, change hello name (for example, yournameFirstDataFactoryPSH).</span></span> <span data-ttu-id="36580-146">Gebruik deze naam in plaats van ADFTutorialFactoryPSH tijdens het uitvoeren van de stappen in de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="36580-146">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="36580-147">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="36580-147">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="36580-148">toocreate Data Factory-exemplaren, moet u bijdrager/beheerder zijn van hello Azure-abonnement toobe</span><span class="sxs-lookup"><span data-stu-id="36580-148">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="36580-149">Hallo-naam van de gegevensfactory Hallo kan worden geregistreerd als DNS-naam in toekomstige Hallo en daarmee ook voor iedereen zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="36580-149">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>
* <span data-ttu-id="36580-150">Als u Hallo-foutmelding: '**dit abonnement is niet geregistreerd toouse namespace Microsoft.DataFactory**', voer een van de volgende Hallo en probeer opnieuw te publiceren:</span><span class="sxs-lookup"><span data-stu-id="36580-150">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="36580-151">Voer in Azure PowerShell Hallo opdracht tooregister Hallo Data Factory-provider te volgen:</span><span class="sxs-lookup"><span data-stu-id="36580-151">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      <span data-ttu-id="36580-152">Die Hallo Data Factory-provider is geregistreerd, kunt u na de opdracht tooconfirm Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="36580-152">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="36580-153">Aanmelding via het Azure-abonnement in Hallo Hallo [Azure-portal](https://portal.azure.com) en navigeer tooa Data Factory-blade of maak een gegevensfactory in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="36580-153">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="36580-154">Deze actie automatisch Hallo provider voor u geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="36580-154">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="36580-155">Voordat u een pijplijn maakt, moet u toocreate enkele Data Factory-entiteiten eerst.</span><span class="sxs-lookup"><span data-stu-id="36580-155">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="36580-156">Maakt u eerst gekoppelde services toolink gegevens/berekeningen tooyour gegevens opslaan, definieert u welke invoer en uitvoer van gegevenssets toorepresent i/o-gegevens in de gekoppelde gegevensopslag en vervolgens Hallo pijplijn maken met een activiteit die gebruikmaakt van deze gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="36580-156">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="36580-157">Gekoppelde services maken</span><span class="sxs-lookup"><span data-stu-id="36580-157">Create linked services</span></span>
<span data-ttu-id="36580-158">In deze stap koppelt u uw Azure-opslagaccount en een bellen op Azure HDInsight-cluster tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="36580-158">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="36580-159">Hallo blokkeringen Hallo invoer en uitvoer-gegevens voor de pijplijn in dit voorbeeld hello Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="36580-159">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="36580-160">Hallo gekoppelde HDInsight-service is gebruikte toorun een Hive-script dat is opgegeven in de activiteit Hallo van Hallo pijplijn in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="36580-160">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="36580-161">Aangeven welk(e) gegevensarchief/rekenservices er services worden gebruikt in uw scenario en koppelen van deze services toohello-gegevensfactory door gekoppelde services te maken.</span><span class="sxs-lookup"><span data-stu-id="36580-161">Identify what data store/compute services are used in your scenario and link those services toohello data factory by creating linked services.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="36580-162">Een gekoppelde Azure Storage-service maken</span><span class="sxs-lookup"><span data-stu-id="36580-162">Create Azure Storage linked service</span></span>
<span data-ttu-id="36580-163">In deze stap koppelt u uw Azure Storage-account tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="36580-163">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="36580-164">U hello gebruiken dezelfde Azure-opslagaccount invoer-en uitvoergegevens toostore en Hallo HQL-script bestand.</span><span class="sxs-lookup"><span data-stu-id="36580-164">You use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="36580-165">Maak een JSON-bestand met de naam StorageLinkedService.json in Hallo C:\ADFGetStarted map Hello volgende inhoud.</span><span class="sxs-lookup"><span data-stu-id="36580-165">Create a JSON file named StorageLinkedService.json in hello C:\ADFGetStarted folder with hello following content.</span></span> <span data-ttu-id="36580-166">Maak Hallo map ADFGetStarted als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="36580-166">Create hello folder ADFGetStarted if it does not already exist.</span></span>

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
    <span data-ttu-id="36580-167">Vervang **accountnaam** met Hallo-naam van uw Azure storage-account en **accountsleutel** door de toegangssleutel Hallo van hello Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="36580-167">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="36580-168">toolearn hoe tooget uw opslag heeft toegang tot sleutel, raadpleegt u Hallo informatie over hoe tooview, kopiëren en opnieuw genereren opslag toegangstoetsen in [uw opslagaccount beheren](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="36580-168">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
2. <span data-ttu-id="36580-169">Schakel over de map ADFGetStarted toohello in Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="36580-169">In Azure PowerShell, switch toohello ADFGetStarted folder.</span></span>
3. <span data-ttu-id="36580-170">U kunt Hallo **New-AzureRmDataFactoryLinkedService** cmdlet die wordt gemaakt van een gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="36580-170">You can use hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates a linked service.</span></span> <span data-ttu-id="36580-171">Deze cmdlet en andere Data Factory-cmdlets die u in deze zelfstudie gebruikt moeten u toopass waarden voor Hallo *ResourceGroupName* en *DataFactoryName* parameters.</span><span class="sxs-lookup"><span data-stu-id="36580-171">This cmdlet and other Data Factory cmdlets you use in this tutorial requires you toopass values for hello *ResourceGroupName* and *DataFactoryName* parameters.</span></span> <span data-ttu-id="36580-172">U kunt ook gebruiken **Get-AzureRmDataFactory** tooget een **DataFactory** object en het Hallo-object doorgeven zonder te hoeven typen *ResourceGroupName* en  *DataFactoryName* telkens wanneer u een cmdlet uitvoert.</span><span class="sxs-lookup"><span data-stu-id="36580-172">Alternatively, you can use **Get-AzureRmDataFactory** tooget a **DataFactory** object and pass hello object without typing *ResourceGroupName* and *DataFactoryName* each time you run a cmdlet.</span></span> <span data-ttu-id="36580-173">Voer Hallo volgende opdracht tooassign Hallo uitvoer Hallo **Get-AzureRmDataFactory** cmdlet tooa **$df** variabele.</span><span class="sxs-lookup"><span data-stu-id="36580-173">Run hello following command tooassign hello output of hello **Get-AzureRmDataFactory** cmdlet tooa **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. <span data-ttu-id="36580-174">Voer nu Hallo **New-AzureRmDataFactoryLinkedService** cmdlet die wordt gemaakt van Hallo gekoppeld **StorageLinkedService** service.</span><span class="sxs-lookup"><span data-stu-id="36580-174">Now, run hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates hello linked **StorageLinkedService** service.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="36580-175">Als u hadn't hello **Get-AzureRmDataFactory** cmdlet en toegewezen Hallo uitvoer toohello **$df** variabele, hebt u toospecify waarden voor Hallo *ResourceGroupName*en *DataFactoryName* parameters als volgt.</span><span class="sxs-lookup"><span data-stu-id="36580-175">If you hadn't run hello **Get-AzureRmDataFactory** cmdlet and assigned hello output toohello **$df** variable, you would have toospecify values for hello *ResourceGroupName* and *DataFactoryName* parameters as follows.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="36580-176">Als u Azure PowerShell in het midden van de zelfstudie Hallo hello sluit, hebt u toorun hello **Get-AzureRmDataFactory** cmdlet volgende keer dat u Azure PowerShell toocomplete Hallo zelfstudie begint.</span><span class="sxs-lookup"><span data-stu-id="36580-176">If you close Azure PowerShell in hello middle of hello tutorial, you have toorun hello **Get-AzureRmDataFactory** cmdlet next time you start Azure PowerShell toocomplete hello tutorial.</span></span>

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="36580-177">Een gekoppelde HDInsight-service maken</span><span class="sxs-lookup"><span data-stu-id="36580-177">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="36580-178">In deze stap maakt koppelen u een gegevensfactory op aanvraag HDInsight-cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="36580-178">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="36580-179">Hallo HDInsight-cluster wordt automatisch gemaakt tijdens runtime en na het verwerken is voltooid en niet-actieve voor de opgegeven tijdsduur Hallo verwijderd.</span><span class="sxs-lookup"><span data-stu-id="36580-179">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="36580-180">U kunt uw eigen HDInsight-cluster gebruiken in plaats van een on-demand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="36580-180">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="36580-181">Zie [Gekoppelde services berekenen](data-factory-compute-linked-services.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="36580-181">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="36580-182">Maak een JSON-bestand met de naam **HDInsightOnDemandLinkedService**.json in Hallo **C:\ADFGetStarted** map Hello inhoud te volgen.</span><span class="sxs-lookup"><span data-stu-id="36580-182">Create a JSON file named **HDInsightOnDemandLinkedService**.json in hello **C:\ADFGetStarted** folder with hello following content.</span></span>

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
    <span data-ttu-id="36580-183">Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:</span><span class="sxs-lookup"><span data-stu-id="36580-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="36580-184">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="36580-184">Property</span></span> | <span data-ttu-id="36580-185">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="36580-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="36580-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="36580-186">ClusterSize</span></span> |<span data-ttu-id="36580-187">Hiermee wordt de grootte Hallo van Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="36580-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="36580-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="36580-188">TimeToLive</span></span> |<span data-ttu-id="36580-189">Hiermee geeft u op dat niet-actieve tijd Hallo voor Hallo HDInsight-cluster, voordat deze wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="36580-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="36580-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="36580-190">linkedServiceName</span></span> |<span data-ttu-id="36580-191">Hiermee geeft u op Hallo storage-account dat is gebruikt toostore Hallo logboeken die door HDInsight worden gegenereerd</span><span class="sxs-lookup"><span data-stu-id="36580-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

    <span data-ttu-id="36580-192">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="36580-192">Note hello following points:</span></span>

   * <span data-ttu-id="36580-193">Hallo Data Factory maakt een **op basis van Linux** HDInsight-cluster voor u Hello JSON.</span><span class="sxs-lookup"><span data-stu-id="36580-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="36580-194">Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="36580-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="36580-195">U kunt **uw eigen HDInsight-cluster** gebruiken in plaats van een on-demand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="36580-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="36580-196">Zie [Gekoppelde HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="36580-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="36580-197">Hallo HDInsight-cluster maakt een **standaardcontainer** in Hallo-blobopslag die u hebt opgegeven in Hallo JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="36580-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="36580-198">HDInsight verwijdert deze container niet wanneer Hallo-cluster is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="36580-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="36580-199">Dit gedrag is standaard.</span><span class="sxs-lookup"><span data-stu-id="36580-199">This behavior is by design.</span></span> <span data-ttu-id="36580-200">Met een gekoppelde on-demand HDInsight-service wordt er steeds een HDInsight-cluster gemaakt wanneer er een segment wordt verwerkt, tenzij er een bestaand livecluster is (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="36580-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="36580-201">Hallo-cluster wordt automatisch verwijderd als het Hallo-verwerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="36580-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="36580-202">Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="36580-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="36580-203">Als u niet ze hoeft voor het oplossen van problemen met taken hello, kunt u toodelete ze tooreduce Hallo opslag kosten.</span><span class="sxs-lookup"><span data-stu-id="36580-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="36580-204">Hallo-namen van deze containers worden als volgt: ' adf**naamvanuwgegevensfactory**-**linkedservicename**- datum '.</span><span class="sxs-lookup"><span data-stu-id="36580-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="36580-205">Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) toodelete containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="36580-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="36580-206">Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="36580-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
2. <span data-ttu-id="36580-207">Voer Hallo **New-AzureRmDataFactoryLinkedService** cmdlet die wordt gemaakt van Hallo gekoppelde service met de naam HDInsightOnDemandLinkedService.</span><span class="sxs-lookup"><span data-stu-id="36580-207">Run hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates hello linked service called HDInsightOnDemandLinkedService.</span></span>
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a><span data-ttu-id="36580-208">Gegevenssets maken</span><span class="sxs-lookup"><span data-stu-id="36580-208">Create datasets</span></span>
<span data-ttu-id="36580-209">In deze stap maakt u gegevenssets toorepresent Hallo invoer maken en uitvoergegevens voor Hive-verwerking.</span><span class="sxs-lookup"><span data-stu-id="36580-209">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="36580-210">Deze gegevenssets verwijzen toohello **StorageLinkedService** u eerder in deze zelfstudie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="36580-210">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="36580-211">Hallo gekoppelde service verwijst tooan Azure Storage-account en gegevenssets vindt u container, map en bestandsnaam in Hallo opslag van de invoer- en uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="36580-211">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="36580-212">Invoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="36580-212">Create input dataset</span></span>
1. <span data-ttu-id="36580-213">Maak een JSON-bestand met de naam **InputTable.json** in Hallo **C:\ADFGetStarted** map Hello volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="36580-213">Create a JSON file named **InputTable.json** in hello **C:\ADFGetStarted** folder with hello following content:</span></span>

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
    <span data-ttu-id="36580-214">Hallo JSON wordt een gegevensset met de naam gedefinieerd **AzureBlobInput**, die staat voor invoergegevens van een activiteit in Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="36580-214">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="36580-215">Bovendien wordt hiermee aangegeven dat Hallo invoergegevens in de blob-container Hallo aangeroepen bevinden zich **adfgetstarted** en Hallo map met de naam **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="36580-215">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

    <span data-ttu-id="36580-216">Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:</span><span class="sxs-lookup"><span data-stu-id="36580-216">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="36580-217">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="36580-217">Property</span></span> | <span data-ttu-id="36580-218">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="36580-218">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="36580-219">type</span><span class="sxs-lookup"><span data-stu-id="36580-219">type</span></span> |<span data-ttu-id="36580-220">Hallo type eigenschap wordt ingesteld tooAzureBlob omdat de gegevens zich in Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="36580-220">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
   | <span data-ttu-id="36580-221">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="36580-221">linkedServiceName</span></span> |<span data-ttu-id="36580-222">verwijst toohello StorageLinkedService die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="36580-222">refers toohello StorageLinkedService you created earlier.</span></span> |
   | <span data-ttu-id="36580-223">fileName</span><span class="sxs-lookup"><span data-stu-id="36580-223">fileName</span></span> |<span data-ttu-id="36580-224">Deze eigenschap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="36580-224">This property is optional.</span></span> <span data-ttu-id="36580-225">Als u deze eigenschap niet opgeeft, worden alle Hallo-bestanden uit folderPath Hallo opgenomen.</span><span class="sxs-lookup"><span data-stu-id="36580-225">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="36580-226">In dit geval wordt alleen Hallo input.log verwerkt.</span><span class="sxs-lookup"><span data-stu-id="36580-226">In this case, only hello input.log is processed.</span></span> |
   | <span data-ttu-id="36580-227">type</span><span class="sxs-lookup"><span data-stu-id="36580-227">type</span></span> |<span data-ttu-id="36580-228">Hallo-logboekbestanden zijn tekstbestanden, zodat we TextFormat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="36580-228">hello log files are in text format, so we use TextFormat.</span></span> |
   | <span data-ttu-id="36580-229">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="36580-229">columnDelimiter</span></span> |<span data-ttu-id="36580-230">kolommen in de logboekbestanden Hallo worden gescheiden door een kommateken hello (,).</span><span class="sxs-lookup"><span data-stu-id="36580-230">columns in hello log files are delimited by hello comma character (,).</span></span> |
   | <span data-ttu-id="36580-231">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="36580-231">frequency/interval</span></span> |<span data-ttu-id="36580-232">frequentie tooMonth ingesteld en interval is 1, wat betekent dat Hallo invoersegmenten één keer per maand beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="36580-232">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="36580-233">external</span><span class="sxs-lookup"><span data-stu-id="36580-233">external</span></span> |<span data-ttu-id="36580-234">Deze eigenschap wordt tootrue ingesteld als Hallo invoergegevens niet worden gegenereerd door Hallo Data Factory-service.</span><span class="sxs-lookup"><span data-stu-id="36580-234">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |
2. <span data-ttu-id="36580-235">Voer Hallo-opdracht in Azure PowerShell toocreate Hallo Data Factory-gegevensset te volgen:</span><span class="sxs-lookup"><span data-stu-id="36580-235">Run hello following command in Azure PowerShell toocreate hello Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="36580-236">Uitvoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="36580-236">Create output dataset</span></span>
<span data-ttu-id="36580-237">U maakt nu Hallo gegevensset toorepresent Hallo uitvoer uitvoergegevens opgeslagen in hello Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="36580-237">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="36580-238">Maak een JSON-bestand met de naam **OutputTable.json** in Hallo **C:\ADFGetStarted** map Hello volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="36580-238">Create a JSON file named **OutputTable.json** in hello **C:\ADFGetStarted** folder with hello following content:</span></span>

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
    <span data-ttu-id="36580-239">Hallo JSON wordt een gegevensset met de naam gedefinieerd **AzureBlobOutput**, die uitvoergegevens voor een activiteit in de pijplijn Hallo vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="36580-239">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="36580-240">Bovendien wordt hiermee aangegeven dat Hallo resultaten worden opgeslagen in blob-container Hallo aangeroepen **adfgetstarted** en Hallo map met de naam **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="36580-240">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="36580-241">Hallo **beschikbaarheid** sectie geeft die Hallo-uitvoergegevensset op maandelijkse basis wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="36580-241">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>
2. <span data-ttu-id="36580-242">Voer Hallo-opdracht in Azure PowerShell toocreate Hallo Data Factory-gegevensset te volgen:</span><span class="sxs-lookup"><span data-stu-id="36580-242">Run hello following command in Azure PowerShell toocreate hello Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a><span data-ttu-id="36580-243">Pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="36580-243">Create pipeline</span></span>
<span data-ttu-id="36580-244">In deze stap maakt u uw eerste pijplijn met een **HDInsightHive**-activiteit.</span><span class="sxs-lookup"><span data-stu-id="36580-244">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="36580-245">Invoersegment maandelijks beschikbaar is (frequency: Month, interval: 1), uitvoer segment wordt geproduceerd, maandelijks en Hallo scheduler-eigenschap voor activiteit Hallo toomonthly ook is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="36580-245">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="36580-246">Hallo-instellingen voor Hallo uitvoergegevensset en Hallo activiteitenplanner moeten overeenkomen met.</span><span class="sxs-lookup"><span data-stu-id="36580-246">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="36580-247">Uitvoergegevensset is momenteel welke stations Hallo planning, dus u een uitvoergegevensset maken moet, zelfs als Hallo activiteit geen uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="36580-247">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="36580-248">Als Hallo activiteit geen invoer neemt, kunt u maken Hallo invoergegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="36580-248">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="36580-249">Hallo-eigenschappen die in de volgende JSON Hallo worden aan Hallo einde van deze sectie beschreven.</span><span class="sxs-lookup"><span data-stu-id="36580-249">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="36580-250">Maak een JSON-bestand met de naam MyFirstPipelinePSH.json in Hallo C:\ADFGetStarted map Hello volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="36580-250">Create a JSON file named MyFirstPipelinePSH.json in hello C:\ADFGetStarted folder with hello following content:</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="36580-251">Vervang **storageaccountname** met de naam van uw opslagaccount in JSON Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="36580-251">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
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
    <span data-ttu-id="36580-252">In de JSON-codefragment hello maakt u een pijplijn die bestaat uit een enkele activiteit waarvoor gebruik van Hive tooprocess gegevens op een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="36580-252">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="36580-253">Hallo Hive-scriptbestand **partitionweblogs.hql**, wordt opgeslagen in hello Azure storage-account (Hallo door scriptLinkedService met de opgegeven **StorageLinkedService**), en in **script**  map in container Hallo **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="36580-253">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="36580-254">Hallo **definieert** sectie is gebruikte toospecify Hallo runtime-instellingen die worden doorgegeven toohello hive-script als Hive-configuratiewaarden (bijvoorbeeld ${hiveconf: inputtable}, ${partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="36580-254">hello **defines** section is used toospecify hello runtime settings that be passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="36580-255">Hallo **start** en **end** eigenschappen van de pijplijn Hallo geeft Hallo actieve periode van Hallo-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="36580-255">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="36580-256">In Hallo activiteits-JSON geeft u opgeven dat Hallo Hive-script wordt uitgevoerd op Hallo berekening die is opgegeven door Hallo **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="36580-256">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="36580-257">Zie 'Pijplijn-JSON' in [pijplijnen en activiteiten in Azure Data Factory](data-factory-create-pipelines.md) voor meer informatie over de JSON-eigenschappen die worden gebruikt in het Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="36580-257">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties that are used in hello example.</span></span>

2. <span data-ttu-id="36580-258">Controleer of u Hallo **input.log** bestand in Hallo **adfgetstarted/inputdata** map in hello Azure blob-opslag- en Voer Hallo opdracht toodeploy Hallo pijplijn te volgen.</span><span class="sxs-lookup"><span data-stu-id="36580-258">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="36580-259">Sinds Hallo **start** en **end** keren worden ingesteld in de afgelopen Hallo en **isPaused** set toofalse, Hallo pijplijn is (activiteit in de pijplijn Hallo) wordt uitgevoerd onmiddellijk nadat u hebt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="36580-259">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. <span data-ttu-id="36580-260">U hebt uw eerste pijplijn gemaakt met Azure PowerShell!</span><span class="sxs-lookup"><span data-stu-id="36580-260">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="36580-261">De pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="36580-261">Monitor pipeline</span></span>
<span data-ttu-id="36580-262">In deze stap gebruikt u Azure PowerShell toomonitor wat er gebeurt in een Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="36580-262">In this step, you use Azure PowerShell toomonitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="36580-263">Voer **Get-AzureRmDataFactory** en toewijzen van Hallo uitvoer tooa **$df** variabele.</span><span class="sxs-lookup"><span data-stu-id="36580-263">Run **Get-AzureRmDataFactory** and assign hello output tooa **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. <span data-ttu-id="36580-264">Voer **Get-AzureRmDataFactorySlice** tooget details over alle segmenten van Hallo **EmpSQLTable**, Hallo uitvoertabel van de pijplijn Hallo.</span><span class="sxs-lookup"><span data-stu-id="36580-264">Run **Get-AzureRmDataFactorySlice** tooget details about all slices of hello **EmpSQLTable**, which is hello output table of hello pipeline.</span></span>

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    <span data-ttu-id="36580-265">U ziet dat Hallo StartDateTime die u hier opgeeft, is dezelfde begintijd opgegeven in de JSON van de pijplijn Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="36580-265">Notice that hello StartDateTime you specify here is hello same start time specified in hello pipeline JSON.</span></span> <span data-ttu-id="36580-266">Hier volgt voorbeelduitvoer Hallo:</span><span class="sxs-lookup"><span data-stu-id="36580-266">Here is hello sample output:</span></span>

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
3. <span data-ttu-id="36580-267">Voer **Get-AzureRmDataFactoryRun** tooget Hallo details van de activiteit wordt uitgevoerd voor een bepaald segment.</span><span class="sxs-lookup"><span data-stu-id="36580-267">Run **Get-AzureRmDataFactoryRun** tooget hello details of activity runs for a specific slice.</span></span>

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    <span data-ttu-id="36580-268">Hier volgt voorbeelduitvoer Hallo:</span><span class="sxs-lookup"><span data-stu-id="36580-268">Here is hello sample output:</span></span> 

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
    <span data-ttu-id="36580-269">U kunt deze cmdlet blijven uitvoeren totdat er Hallo segment **gereed** status of **mislukt** status.</span><span class="sxs-lookup"><span data-stu-id="36580-269">You can keep running this cmdlet until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="36580-270">Als Hallo segment status gereed is, Controleer Hallo **partitioneddata** map in Hallo **adfgetstarted** container in uw blobopslag voor Hallo uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="36580-270">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="36580-271">Het maken van een on-demand HDInsight-cluster duurt normaal gesproken enige tijd.</span><span class="sxs-lookup"><span data-stu-id="36580-271">Creation of an on-demand HDInsight cluster usually takes some time.</span></span>

    ![Uitvoergegevens](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="36580-273">Het maken van een on-demand HDInsight-cluster duurt normaal gesproken enige tijd (ongeveer 20 minuten).</span><span class="sxs-lookup"><span data-stu-id="36580-273">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="36580-274">Daarom verwachten Hallo pijplijn tootake **ongeveer 30 minuten** tooprocess Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="36580-274">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
> <span data-ttu-id="36580-275">Hallo-invoerbestand wordt verwijderd zodra het Hallo-segment is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="36580-275">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="36580-276">Als u toorerun Hallo segment of zelfstudie opnieuw hello, dus Hallo invoerbestand (input.log) toohello inputdata map van de container adfgetstarted Hallo uploadt.</span><span class="sxs-lookup"><span data-stu-id="36580-276">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

## <a name="summary"></a><span data-ttu-id="36580-277">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="36580-277">Summary</span></span>
<span data-ttu-id="36580-278">In deze zelfstudie maakt u een Azure data factory tooprocess gegevens gemaakt door het Hive-script uitvoeren op een HDInsight hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="36580-278">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="36580-279">U hebt gebruikt Hallo Data Factory-Editor in hello Azure portal toodo Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="36580-279">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="36580-280">U hebt een Azure-**gegevensfactory** gemaakt.</span><span class="sxs-lookup"><span data-stu-id="36580-280">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="36580-281">U hebt twee **gekoppelde services** gemaakt:</span><span class="sxs-lookup"><span data-stu-id="36580-281">Created two **linked services**:</span></span>
   1. <span data-ttu-id="36580-282">**Azure Storage** gekoppelde service toolink uw Azure-blobopslag die invoer-/ uitvoerbestanden toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="36580-282">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="36580-283">**Azure HDInsight** op aanvraag gekoppelde service toolink een bellen op HDInsight Hadoop-cluster toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="36580-283">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="36580-284">Azure Data Factory maakt een HDInsight Hadoop-cluster just in time tooprocess invoergegevens en uitvoergegevens produceren.</span><span class="sxs-lookup"><span data-stu-id="36580-284">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="36580-285">Twee gemaakt **gegevenssets**, die invoer- en gegevens voor HDInsight Hive-activiteit in Hallo pijplijn worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="36580-285">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="36580-286">U hebt een **pijplijn** gemaakt met een **HDInsight Hive**-activiteit.</span><span class="sxs-lookup"><span data-stu-id="36580-286">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36580-287">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="36580-287">Next steps</span></span>
<span data-ttu-id="36580-288">In dit artikel hebt u een pijplijn gemaakt met een transformatieactiviteit (HDInsight-activiteit) waarvoor een Hive-script wordt uitgevoerd op een on-demand Azure HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="36580-288">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="36580-289">hoe de gegevens van een Kopieeractiviteit toocopy van een Azure Blob-tooAzure SQL, toouse zien toosee [zelfstudie: gegevens kopiëren van een Azure Blob-tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="36580-289">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="36580-290">Zie ook</span><span class="sxs-lookup"><span data-stu-id="36580-290">See Also</span></span>
| <span data-ttu-id="36580-291">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="36580-291">Topic</span></span> | <span data-ttu-id="36580-292">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="36580-292">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="36580-293">Data Factory-cmdlet-verwijzing</span><span class="sxs-lookup"><span data-stu-id="36580-293">Data Factory Cmdlet Reference</span></span>](/powershell/module/azurerm.datafactories) |<span data-ttu-id="36580-294">Zie de uitgebreide documentatie over Data Factory-cmdlets</span><span class="sxs-lookup"><span data-stu-id="36580-294">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="36580-295">Pijplijnen</span><span class="sxs-lookup"><span data-stu-id="36580-295">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="36580-296">In dit artikel helpt u begrijpen pijplijnen en activiteiten in Azure Data Factory en hoe toouse ze tooconstruct end-to-end gegevensgestuurde werkstromen voor uw scenario of bedrijf.</span><span class="sxs-lookup"><span data-stu-id="36580-296">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="36580-297">Gegevenssets</span><span class="sxs-lookup"><span data-stu-id="36580-297">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="36580-298">Op basis van dit artikel krijgt u inzicht in de gegevenssets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="36580-298">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="36580-299">Plannen en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="36580-299">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="36580-300">Dit artikel wordt uitgelegd Hallo plannings- en uitvoeringsaspecten van het Azure Data Factory-toepassingsmodel.</span><span class="sxs-lookup"><span data-stu-id="36580-300">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="36580-301">Pijplijnen bewaken en beheren met de app voor bewaking en beheer</span><span class="sxs-lookup"><span data-stu-id="36580-301">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="36580-302">Dit artikel wordt beschreven hoe toomonitor, beheren en fouten opsporen in pijplijnen met behulp van Hallo voor bewaking en beheer-App.</span><span class="sxs-lookup"><span data-stu-id="36580-302">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
