---
title: Uw eerste gegevensfactory bouwen (Azure Portal) | Microsoft Docs
description: In deze zelfstudie maakt u een Azure Data Factory-voorbeeldpijplijn met behulp van de Data Factory-editor in Azure Portal.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 9c958aecb841fa02349c6b9e5e1984f6ba4fb611
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a><span data-ttu-id="c4cf9-103">Zelfstudie: uw eerste Azure-gegevensfactory bouwen met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c4cf9-103">Tutorial: Build your first Azure data factory using Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c4cf9-104">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="c4cf9-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="c4cf9-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c4cf9-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="c4cf9-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c4cf9-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="c4cf9-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4cf9-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="c4cf9-108">Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="c4cf9-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="c4cf9-109">REST API</span><span class="sxs-lookup"><span data-stu-id="c4cf9-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)


<span data-ttu-id="c4cf9-110">In dit artikel leert u hoe u [Azure Portal](https://portal.azure.com/) gebruikt voor het maken van uw eerste Azure-gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-110">In this article, you learn how to use [Azure portal](https://portal.azure.com/) to create your first Azure data factory.</span></span> <span data-ttu-id="c4cf9-111">Als u de zelfstudie wilt volgen met andere hulpprogramma's/SDK's, selecteert u een van de opties uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span> 

<span data-ttu-id="c4cf9-112">De pijplijn in deze zelfstudie heeft één activiteit: **HDInsight-componentactiviteit**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="c4cf9-113">Deze activiteit voert een Hive-script uit op een Azure HDInsight-cluster dat invoergegevens transformeert om uitvoergegevens te produceren.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="c4cf9-114">De pijplijn is gepland on één keer per maand tussen de opgegeven begin- en eindtijd te worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="c4cf9-115">Met de gegevenspijplijn in deze zelfstudie worden invoergegevens getransformeerd in uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-115">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="c4cf9-116">Zie [Zelfstudie: gegevens kopiëren van Blob Storage naar SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor informatie over het kopiëren van gegevens met Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-116">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="c4cf9-117">Een pijplijn kan meer dan één activiteit hebben.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="c4cf9-118">Ook kunt u twee activiteiten koppelen (de ene activiteit na de andere laten uitvoeren) door de uitvoergegevensset van één activiteit in te stellen als invoergegevensset voor een andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-118">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="c4cf9-119">Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4cf9-120">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c4cf9-120">Prerequisites</span></span>
1. <span data-ttu-id="c4cf9-121">Lees het artikel [Overzicht van de zelfstudie](data-factory-build-your-first-pipeline.md) en voer de **vereiste** stappen uit.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
2. <span data-ttu-id="c4cf9-122">Dit artikel biedt geen conceptueel overzicht van de Azure Data Factory-service.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-122">This article does not provide a conceptual overview of the Azure Data Factory service.</span></span> <span data-ttu-id="c4cf9-123">Lees voor een gedetailleerd overzicht van de service het artikel [Inleiding tot Azure Data Factory](data-factory-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c4cf9-123">We recommend that you go through [Introduction to Azure Data Factory](data-factory-introduction.md) article for a detailed overview of the service.</span></span>  

## <a name="create-data-factory"></a><span data-ttu-id="c4cf9-124">Een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="c4cf9-124">Create data factory</span></span>
<span data-ttu-id="c4cf9-125">Een gegevensfactory kan één of meer pijplijnen hebben.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-125">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="c4cf9-126">Een pijplijn kan één of meer activiteiten bevatten.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-126">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="c4cf9-127">Bijvoorbeeld een kopieeractiviteit om gegevens van een bron- naar een doelgegevensopslagplaats te kopiëren en een HDInsight Hive-activiteit om een Hive-script uit te voeren voor het transformeren van invoergegevens naar productuitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-127">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="c4cf9-128">U begint in deze stap met het maken van de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-128">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="c4cf9-129">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c4cf9-129">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c4cf9-130">Klik op **NIEUW** in het linkermenu en klik vervolgens op **Gegevens en analyses** en **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-130">Click **NEW** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>

   ![Blade maken](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. <span data-ttu-id="c4cf9-132">Voer op de blade **Nieuwe gegevensfactory** **GetStartedDF** in als naam.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-132">In the **New data factory** blade, enter **GetStartedDF** for the Name.</span></span>

   ![Blade voor een nieuwe gegevensfactory](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > <span data-ttu-id="c4cf9-134">De naam van de Azure-gegevensfactory moet **wereldwijd uniek** zijn.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-134">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="c4cf9-135">Als u de volgende fout ontvangt: **Naam data factory “GetStartedDF” is niet beschikbaar**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-135">If you receive the error: **Data factory name “GetStartedDF” is not available**.</span></span> <span data-ttu-id="c4cf9-136">Wijzig de naam van de datafactory (bijvoorbeeld yournameGetStartedDF) en probeer om opnieuw te maken.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-136">Change the name of the data factory (for example, yournameGetStartedDF) and try creating again.</span></span> <span data-ttu-id="c4cf9-137">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-137">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
   >
   > <span data-ttu-id="c4cf9-138">De naam van de gegevensfactory wordt in de toekomst mogelijk geregistreerd als **DNS**-naam en wordt daarmee ook voor iedereen zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-138">The name of the data factory may be registered as a **DNS** name in the future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="c4cf9-139">Selecteer het **Azure-abonnement** waarvoor u de gegevensfactory wilt maken.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-139">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="c4cf9-140">Selecteer een bestaande **resourcegroep** of maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-140">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="c4cf9-141">Maak voor deze zelfstudie een resourcegroep met de naam **ADFGetStartedRG**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-141">For the tutorial, create a resource group named: **ADFGetStartedRG**.</span></span>
6. <span data-ttu-id="c4cf9-142">Selecteer de **locatie** voor de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-142">Select the **location** for the data factory.</span></span> <span data-ttu-id="c4cf9-143">Alleen regio's die worden ondersteund door de Data Factory-service worden weergegeven in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-143">Only regions supported by the Data Factory service are shown in the drop-down list.</span></span>
7. <span data-ttu-id="c4cf9-144">Selecteer **Vastmaken aan dashboard**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-144">Select **Pin to dashboard**.</span></span> 
8. <span data-ttu-id="c4cf9-145">Klik op de blade **Nieuwe gegevensfactory** op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-145">Click **Create** on the **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c4cf9-146">Als u Data Factory-exemplaren wilt maken, moet u lid zijn van de rol [Inzender Data Factory](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) op abonnements-/resourcegroepsniveau.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-146">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="c4cf9-147">Op het dashboard ziet u de volgende tegel met de status: Gegevensfactory implementeren.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-147">On the dashboard, you see the following tile with status: Deploying data factory.</span></span>    

   ![Status van gegevensfactory maken](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. <span data-ttu-id="c4cf9-149">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-149">Congratulations!</span></span> <span data-ttu-id="c4cf9-150">U hebt uw eerste gegevensfactory gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-150">You have successfully created your first data factory.</span></span> <span data-ttu-id="c4cf9-151">Nadat de gegevensfactory is gemaakt, ziet u de gegevensfactorypagina. Hierop wordt de inhoud van de gegevensfactory weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-151">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>     

    ![Blade Gegevensfactory](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

<span data-ttu-id="c4cf9-153">Voordat u een pijplijn maakt in de gegevensfactory, moet u eerst enkele Data Factory-exemplaren maken.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-153">Before creating a pipeline in the data factory, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="c4cf9-154">U maakt eerst gekoppelde services om gegevensopslag/berekeningen te koppelen aan uw gegevensopslag, vervolgens definieert u welke invoer- en uitvoergegevenssets de invoer- en uitvoergegevens in de gekoppelde gegevensopslag vertegenwoordigen en daarna maakt u de pijplijn met een activiteit waarvoor gebruik wordt gemaakt van die gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-154">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent input/output data in linked data stores, and then create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="c4cf9-155">Gekoppelde services maken</span><span class="sxs-lookup"><span data-stu-id="c4cf9-155">Create linked services</span></span>
<span data-ttu-id="c4cf9-156">In deze stap koppelt u uw Azure Storage-account en een on-demand Azure HDInsight-cluster aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-156">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span></span> <span data-ttu-id="c4cf9-157">Het Azure Storage-account bevat de in- en uitvoergegevens van de pijplijn in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-157">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> <span data-ttu-id="c4cf9-158">De gekoppelde HDInsight-service wordt gebruikt om een Hive-script uit te voeren dat is opgegeven in de activiteit van de pijplijn in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-158">The HDInsight linked service is used to run a Hive script specified in the activity of the pipeline in this sample.</span></span> <span data-ttu-id="c4cf9-159">Geef aan welk(e) [gegevensarchief](data-factory-data-movement-activities.md)/[rekenservices](data-factory-compute-linked-services.md) er in uw scenario worden gebruikt. Koppel die services aan de gegevensfactory door gekoppelde services te maken.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-159">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario and link those services to the data factory by creating linked services.</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="c4cf9-160">Een gekoppelde Azure Storage-service maken</span><span class="sxs-lookup"><span data-stu-id="c4cf9-160">Create Azure Storage linked service</span></span>
<span data-ttu-id="c4cf9-161">In deze stap koppelt u uw Azure Storage-account aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-161">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="c4cf9-162">Voor deze zelfstudie gebruikt u hetzelfde Azure Storage-account om invoer- en uitvoergegevens en het HQL-scriptbestand op te slaan.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-162">In this tutorial, you use the same Azure Storage account to store input/output data and the HQL script file.</span></span>

1. <span data-ttu-id="c4cf9-163">Klik op de blade **GEGEVENSFACTORY** van **GetStartedDF** op **Maken en implementeren**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-163">Click **Author and deploy** on the **DATA FACTORY** blade for **GetStartedDF**.</span></span> <span data-ttu-id="c4cf9-164">U krijgt de Data Factory-editor te zien.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-164">You should see the Data Factory Editor.</span></span>

   ![Tegel ontwerpen en implementeren](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. <span data-ttu-id="c4cf9-166">Klik op **Nieuwe gegevensopslag** en kies **Azure-opslag**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-166">Click **New data store** and choose **Azure storage**.</span></span>

   ![Nieuwe gegevensopslag - Azure Storage - menu](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="c4cf9-168">U ziet het JSON-script voor het maken van een gekoppelde Azure Storage-service in de editor.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-168">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>

   ![Een gekoppelde Azure Storage-service](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="c4cf9-170">Vervang de **accountnaam** door de naam van uw Azure-opslagaccount en vervang de **accountsleutel** door de toegangssleutel van het Azure-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-170">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="c4cf9-171">Raadpleeg de informatie over het weergeven, kopiëren en opnieuw genereren van toegangssleutels voor opslag in [Uw opslagaccount beheren](../storage/common/storage-create-storage-account.md#manage-your-storage-account) als u meer wilt weten over het verkrijgen van een toegangssleutel voor opslag.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-171">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="c4cf9-172">Klik op de opdrachtbalk op **Implementeren** om de gekoppelde service te implementeren.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-172">Click **Deploy** on the command bar to deploy the linked service.</span></span>

    ![Implementatieknop](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   <span data-ttu-id="c4cf9-174">Wanneer de gekoppelde service is geïmplementeerd, verdwijnt het venster **Draft-1** en ziet u **AzureStorageLinkedService** in de structuurweergave links.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-174">After the linked service is deployed successfully, the **Draft-1** window should disappear and you see **AzureStorageLinkedService** in the tree view on the left.</span></span>

    ![Een gekoppelde opslagservice in het menu](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="c4cf9-176">Een gekoppelde HDInsight-service maken</span><span class="sxs-lookup"><span data-stu-id="c4cf9-176">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="c4cf9-177">In deze stap koppelt u een on-demand HDInsight-cluster aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-177">In this step, you link an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="c4cf9-178">Het HDInsight-cluster wordt automatisch gemaakt tijdens runtime en wordt verwijderd wanneer het verwerken is voltooid en het cluster gedurende een opgegeven tijdsperiode niet actief is geweest.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-178">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span></span>

1. <span data-ttu-id="c4cf9-179">Klik in de **Data Factory-editor** op **... Meer** en op **Nieuwe berekening**. Selecteer vervolgens **On-demand HDInsight-cluster**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-179">In the **Data Factory Editor**, click **... More**, click **New compute**, and select **On-demand HDInsight cluster**.</span></span>

    ![Nieuwe berekening](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. <span data-ttu-id="c4cf9-181">Kopieer het onderstaande codefragment en plak het in het venster **Draft-1**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-181">Copy and paste the following snippet to the **Draft-1** window.</span></span> <span data-ttu-id="c4cf9-182">Het JSON-codefragment bevat de eigenschappen die worden gebruikt voor het maken van het on-demand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-182">The JSON snippet describes the properties that are used to create the HDInsight cluster on-demand.</span></span>

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

    <span data-ttu-id="c4cf9-183">De volgende tabel bevat beschrijvingen van de JSON-eigenschappen die in het codefragment worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="c4cf9-183">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="c4cf9-184">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c4cf9-184">Property</span></span> | <span data-ttu-id="c4cf9-185">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c4cf9-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="c4cf9-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="c4cf9-186">ClusterSize</span></span> |<span data-ttu-id="c4cf9-187">Geeft de grootte van het HDInsight-cluster aan.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-187">Specifies the size of the HDInsight cluster.</span></span> |
   | <span data-ttu-id="c4cf9-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="c4cf9-188">TimeToLive</span></span> | <span data-ttu-id="c4cf9-189">Geeft aan hoelang het HDInsight-cluster inactief moet zijn voordat het wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-189">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="c4cf9-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c4cf9-190">linkedServiceName</span></span> | <span data-ttu-id="c4cf9-191">Geeft het opslagaccount aan dat wordt gebruikt voor het opslaan van de logboeken die door HDInsight worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-191">Specifies the storage account that is used to store the logs that are generated by HDInsight.</span></span> |

    <span data-ttu-id="c4cf9-192">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="c4cf9-192">Note the following points:</span></span>

   * <span data-ttu-id="c4cf9-193">Met de JSON maakt Data Factory voor u een HDInsight-cluster **op basis van Linux**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-193">The Data Factory creates a **Linux-based** HDInsight cluster for you with the JSON.</span></span> <span data-ttu-id="c4cf9-194">Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="c4cf9-195">U kunt **uw eigen HDInsight-cluster** gebruiken in plaats van een on-demand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="c4cf9-196">Zie [Gekoppelde HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="c4cf9-197">Het HDInsight-cluster maakt een **standaardcontainer** in de blobopslag die u hebt opgegeven in de JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="c4cf9-197">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="c4cf9-198">HDInsight verwijdert deze container niet wanneer het cluster wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-198">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="c4cf9-199">Dit gedrag is standaard.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-199">This behavior is by design.</span></span> <span data-ttu-id="c4cf9-200">Met een gekoppelde on-demand HDInsight-service wordt er steeds een HDInsight-cluster gemaakt wanneer er een segment wordt verwerkt, tenzij er een bestaand livecluster is (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="c4cf9-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="c4cf9-201">Het cluster wordt verwijderd wanneer het verwerken is voltooid.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-201">The cluster is automatically deleted when the processing is done.</span></span>

       <span data-ttu-id="c4cf9-202">Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="c4cf9-203">Als u deze niet nodig hebt voor het oplossen van problemen met taken, kunt u ze verwijderen om de opslagkosten te verlagen.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-203">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="c4cf9-204">De namen van deze containers worden als volgt opgebouwd: adf**naamvanuwgegevensfactory**-**naamvangekoppeldeservice**-datum-/tijdstempel.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-204">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="c4cf9-205">Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) om containers in uw Azure-blobopslag te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="c4cf9-206">Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
3. <span data-ttu-id="c4cf9-207">Klik op de opdrachtbalk op **Implementeren** om de gekoppelde service te implementeren.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-207">Click **Deploy** on the command bar to deploy the linked service.</span></span>

    ![Gekoppelde on-demand HDInsight-service implementeren](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. <span data-ttu-id="c4cf9-209">Controleer of u in de structuurweergave links zowel **AzureStorageLinkedService** als **HDInsightOnDemandLinkedService** ziet.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-209">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in the tree view on the left.</span></span>

    ![Structuurweergave met gekoppelde services](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a><span data-ttu-id="c4cf9-211">Gegevenssets maken</span><span class="sxs-lookup"><span data-stu-id="c4cf9-211">Create datasets</span></span>
<span data-ttu-id="c4cf9-212">In deze stap maakt u gegevenssets die de invoer- en uitvoergegevens voor Hive-verwerking vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-212">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="c4cf9-213">Deze gegevenssets verwijzen naar de **AzureStorageLinkedService** die u eerder in deze zelfstudie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-213">These datasets refer to the **AzureStorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="c4cf9-214">De gekoppelde service verwijst naar een Azure-opslagaccount en in de gegevenssets vindt u de container, map en bestandsnaam in de opslag van de invoer- en uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-214">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>   

### <a name="create-input-dataset"></a><span data-ttu-id="c4cf9-215">Invoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="c4cf9-215">Create input dataset</span></span>
1. <span data-ttu-id="c4cf9-216">Klik in de **Data Factory-editor** op **... Meer** op de opdrachtbalk, klik op **Nieuwe gegevensset** en selecteer **Azure-blobopslag**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-216">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>

    ![Nieuwe gegevensset](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. <span data-ttu-id="c4cf9-218">Kopieer het onderstaande codefragment en plak het in het venster Draft-1.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-218">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="c4cf9-219">U maakt in het JSON-fragment een gegevensset met de naam **AzureBlobInput** die staat voor invoergegevens van een activiteit in de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-219">In the JSON snippet, you are creating a dataset called **AzureBlobInput** that represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="c4cf9-220">Daarbij geeft u op dat de invoergegevens zich bevinden in de blobcontainer met de naam **adfgetstarted** en de map met de naam **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-220">In addition, you specify that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span></span>

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
    <span data-ttu-id="c4cf9-221">De volgende tabel bevat beschrijvingen van de JSON-eigenschappen die in het codefragment worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="c4cf9-221">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="c4cf9-222">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c4cf9-222">Property</span></span> | <span data-ttu-id="c4cf9-223">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c4cf9-223">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="c4cf9-224">type</span><span class="sxs-lookup"><span data-stu-id="c4cf9-224">type</span></span> |<span data-ttu-id="c4cf9-225">De eigenschap type wordt ingesteld op **AzureBlob**, omdat de gegevens zich in een Azure-blobopslag bevinden.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-225">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
   | <span data-ttu-id="c4cf9-226">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c4cf9-226">linkedServiceName</span></span> |<span data-ttu-id="c4cf9-227">Deze eigenschap verwijst naar de **AzureStorageLinkedService** die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-227">Refers to the **AzureStorageLinkedService** you created earlier.</span></span> |
   | <span data-ttu-id="c4cf9-228">folderPath</span><span class="sxs-lookup"><span data-stu-id="c4cf9-228">folderPath</span></span> | <span data-ttu-id="c4cf9-229">Deze eigenschap verwijst naar de blob**container** en de **map** die de blobs voor invoer bevat.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-229">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> | 
   | <span data-ttu-id="c4cf9-230">fileName</span><span class="sxs-lookup"><span data-stu-id="c4cf9-230">fileName</span></span> |<span data-ttu-id="c4cf9-231">Deze eigenschap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-231">This property is optional.</span></span> <span data-ttu-id="c4cf9-232">Als u deze eigenschap niet opgeeft, worden alle bestanden uit folderPath gekozen.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-232">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="c4cf9-233">In deze zelfstudie wordt alleen de **input.log** verwerkt.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-233">In this tutorial, only the **input.log** is processed.</span></span> |
   | <span data-ttu-id="c4cf9-234">type</span><span class="sxs-lookup"><span data-stu-id="c4cf9-234">type</span></span> |<span data-ttu-id="c4cf9-235">Omdat de logboekbestanden tekstbestanden zijn, gebruiken we **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-235">The log files are in text format, so we use **TextFormat**.</span></span> |
   | <span data-ttu-id="c4cf9-236">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="c4cf9-236">columnDelimiter</span></span> |<span data-ttu-id="c4cf9-237">Kolommen in de logboekbestanden worden gescheiden door een **komma (,) (`,`)**</span><span class="sxs-lookup"><span data-stu-id="c4cf9-237">columns in the log files are delimited by **comma character (`,`)**</span></span> |
   | <span data-ttu-id="c4cf9-238">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="c4cf9-238">frequency/interval</span></span> |<span data-ttu-id="c4cf9-239">Als frequency wordt ingesteld op **Month** en het interval **1** is, betekent dit dat de invoersegmenten één keer per maand beschikbaar worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-239">frequency set to **Month** and interval is **1**, which means that the input slices are available monthly.</span></span> |
   | <span data-ttu-id="c4cf9-240">external</span><span class="sxs-lookup"><span data-stu-id="c4cf9-240">external</span></span> | <span data-ttu-id="c4cf9-241">Deze eigenschap wordt ingesteld op **true** als de invoergegevens niet worden gegenereerd door deze pijplijn.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-241">This property is set to **true** if the input data is not generated by this pipeline.</span></span> <span data-ttu-id="c4cf9-242">In deze zelfstudie wordt het bestand input.log niet gegenereerd door deze pijplijn, daarom hebben we de eigenschap ingesteld op true.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-242">In this tutorial, the input.log file is not generated by this pipeline, so we set the property to true.</span></span> |

    <span data-ttu-id="c4cf9-243">Zie het [artikel over Azure Blob-connectoren](data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over deze JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-243">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="c4cf9-244">Klik op de opdrachtbalk op **Implementeren** om de zojuist gemaakte gegevensset te implementeren.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-244">Click **Deploy** on the command bar to deploy the newly created dataset.</span></span> <span data-ttu-id="c4cf9-245">U ziet de gegevensset in de structuurweergave links.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-245">You should see the dataset in the tree view on the left.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="c4cf9-246">Uitvoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="c4cf9-246">Create output dataset</span></span>
<span data-ttu-id="c4cf9-247">U maakt nu de uitvoergegevensset die staat voor de uitvoergegevens die worden opgeslagen in de Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-247">Now, you create the output dataset to represent the output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="c4cf9-248">Klik in de **Data Factory-editor** op **... Meer** op de opdrachtbalk, klik op **Nieuwe gegevensset** en selecteer **Azure-blobopslag**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-248">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="c4cf9-249">Kopieer het onderstaande codefragment en plak het in het venster Draft-1.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-249">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="c4cf9-250">In het JSON-codefragment maakt u een gegevensset met de naam **AzureBlobOutput** en geeft u op welke gegevensstructuur er door het Hive-script wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-250">In the JSON snippet, you are creating a dataset called **AzureBlobOutput**, and specifying the structure of the data that is produced by the Hive script.</span></span> <span data-ttu-id="c4cf9-251">Bovendien geeft u op dat de resultaten worden opgeslagen in de blobcontainer met de naam **adfgetstarted** en in de map met de naam **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-251">In addition, you specify that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span></span> <span data-ttu-id="c4cf9-252">In het gedeelte **availability** wordt opgegeven dat de uitvoergegevensset op maandelijkse basis wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-252">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span>

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
    <span data-ttu-id="c4cf9-253">Raadpleeg het gedeelte **Invoergegevensset maken** voor een beschrijving van deze eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-253">See **Create the input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="c4cf9-254">U stelt de externe eigenschap niet in op een uitvoergegevensset, omdat de gegevensset wordt geproduceerd door de Data Factory-service.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-254">You do not set the external property on an output dataset as the dataset is produced by the Data Factory service.</span></span>
3. <span data-ttu-id="c4cf9-255">Klik op de opdrachtbalk op **Implementeren** om de zojuist gemaakte gegevensset te implementeren.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-255">Click **Deploy** on the command bar to deploy the newly created dataset.</span></span>
4. <span data-ttu-id="c4cf9-256">Controleer of de gegevensset is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-256">Verify that the dataset is created successfully.</span></span>

    ![Structuurweergave met gekoppelde services](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a><span data-ttu-id="c4cf9-258">Pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="c4cf9-258">Create pipeline</span></span>
<span data-ttu-id="c4cf9-259">In deze stap maakt u uw eerste pijplijn met een **HDInsightHive**-activiteit.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-259">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="c4cf9-260">Het invoersegment wordt elke maand beschikbaar gesteld (frequentie: Maand, interval: 1), evenals het uitvoersegment. Ook de plannereigenschap van de activiteit wordt op maandelijks ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-260">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span></span> <span data-ttu-id="c4cf9-261">De instellingen voor de uitvoergegevensset en de activiteitenplanner moeten overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-261">The settings for the output dataset and the activity scheduler must match.</span></span> <span data-ttu-id="c4cf9-262">Op dit moment wordt de planning gebaseerd op de uitvoergegevensset. Daarom moet u ook een uitvoergegevensset maken als er tijdens de activiteit geen uitvoer wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-262">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="c4cf9-263">Als er voor de activiteit geen invoer nodig is, kunt u het maken van de invoergegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-263">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="c4cf9-264">De eigenschappen die in de volgende JSON worden gebruikt, worden aan het einde van dit gedeelte beschreven.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-264">The properties used in the following JSON are explained at the end of this section.</span></span>

1. <span data-ttu-id="c4cf9-265">Klik in de **Data Factory-editor** op **Ellips (...) Meer opdrachten**. Klik vervolgens op **Nieuwe pijplijn**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-265">In the **Data Factory Editor**, click **Ellipsis (…) More commands** and then click **New pipeline**.</span></span>

    ![Knop Nieuw pijplijn](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. <span data-ttu-id="c4cf9-267">Kopieer het onderstaande codefragment en plak het in het venster Draft-1.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-267">Copy and paste the following snippet to the Draft-1 window.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c4cf9-268">Vervang **storageaccountname** door de naam van uw opslagaccount in de JSON.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-268">Replace **storageaccountname** with the name of your storage account in the JSON.</span></span>
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
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

    <span data-ttu-id="c4cf9-269">In het JSON-codefragment maakt u een pijplijn die bestaat uit een enkele activiteit waarvoor gebruik wordt gemaakt van Hive om gegevens in een HDInsight-cluster te verwerken.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-269">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="c4cf9-270">Het Hive-scriptbestand **partitionweblogs.hql** wordt opgeslagen in het Azure-opslagaccount (opgegeven door de scriptLinkedService met de naam **AzureStorageLinkedService**) en in de map **script** van de container **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-270">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>

    <span data-ttu-id="c4cf9-271">Het gedeelte **defines** wordt gebruikt om de runtime-instellingen die worden doorgegeven aan het Hive-script op te geven als Hive-configuratiewaarden (bijvoorbeeld ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="c4cf9-271">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="c4cf9-272">Met de eigenschappen **start** en **end** van de pijplijn wordt opgegeven in welke periode de pijplijn actief is.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-272">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span>

    <span data-ttu-id="c4cf9-273">In de activiteits-JSON geeft u op dat het Hive-script wordt uitgevoerd in de berekening die is opgegeven door de **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-273">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c4cf9-274">Zie 'Pijplijn JSON' in [Pijplijnen en activiteiten in Azure Data Factory](data-factory-create-pipelines.md) voor meer informatie over de JSON-eigenschappen die in het voorbeeld worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-274">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in the example.</span></span>
   >
   >
3. <span data-ttu-id="c4cf9-275">Bevestig het volgende:</span><span class="sxs-lookup"><span data-stu-id="c4cf9-275">Confirm the following:</span></span>

   1. <span data-ttu-id="c4cf9-276">Het bestand **Input.log** staat in de map **inputdata** van de container **adfgetstarted** in de Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-276">**input.log** file exists in the **inputdata** folder of the **adfgetstarted** container in the Azure blob storage</span></span>
   2. <span data-ttu-id="c4cf9-277">Het bestand **partitionweblogs.hql** staat in de map **script** van de container **adfgetstarted** in de Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-277">**partitionweblogs.hql** file exists in the **script** folder of the **adfgetstarted** container in the Azure blob storage.</span></span> <span data-ttu-id="c4cf9-278">Voltooi de vereiste stappen in [Overzicht van de zelfstudie](data-factory-build-your-first-pipeline.md) als deze bestanden niet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-278">Complete the prerequisite steps in the [Tutorial Overview](data-factory-build-your-first-pipeline.md) if you don't see these files.</span></span>
   3. <span data-ttu-id="c4cf9-279">Controleer of u **storageaccountname** hebt vervangen door de naam van uw opslagaccount in de pijplijn-JSON.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-279">Confirm that you replaced **storageaccountname** with the name of your storage account in the pipeline JSON.</span></span>
4. <span data-ttu-id="c4cf9-280">Klik op de opdrachtbalk op **Implementeren** om de pijplijn te implementeren.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-280">Click **Deploy** on the command bar to deploy the pipeline.</span></span> <span data-ttu-id="c4cf9-281">Aangezien de tijden voor **start** en **end** in het verleden vallen en **isPaused** is ingesteld op false, wordt de pijplijn (activiteit in de pijplijn) direct na het implementeren uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-281">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span></span>
5. <span data-ttu-id="c4cf9-282">Controleer of de pijplijn in de structuurweergave wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-282">Confirm that you see the pipeline in the tree view.</span></span>

    ![Structuurweergave met de pijplijn](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. <span data-ttu-id="c4cf9-284">U hebt uw eerste pijplijn gemaakt!</span><span class="sxs-lookup"><span data-stu-id="c4cf9-284">Congratulations, you have successfully created your first pipeline!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="c4cf9-285">De pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="c4cf9-285">Monitor pipeline</span></span>
### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="c4cf9-286">De pijplijn bewaken met Diagramweergave</span><span class="sxs-lookup"><span data-stu-id="c4cf9-286">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="c4cf9-287">Klik op **X** om de blades van de Data Factory-editor te sluiten en om terug te keren naar de Data Factory-blade. Klik op **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-287">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span></span>

    ![Tegel Diagram](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. <span data-ttu-id="c4cf9-289">In de diagramweergave ziet u een overzicht van de pijplijnen en gegevenssets die voor deze zelfstudie worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-289">In the Diagram View, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![Diagramweergave](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. <span data-ttu-id="c4cf9-291">Als u alle activiteiten in de pijplijn wilt weergeven, klikt u met de rechtermuisknop op de pijplijn in het diagram. Klik vervolgens op Pijplijn openen.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-291">To view all activities in the pipeline, right-click pipeline in the diagram and click Open Pipeline.</span></span>

    ![Menu Pijplijn openen](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. <span data-ttu-id="c4cf9-293">Bevestig dat u de HDInsightHive-activiteit in de pijplijn ziet.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-293">Confirm that you see the HDInsightHive activity in the pipeline.</span></span>

    ![Pijplijnweergave openen](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    <span data-ttu-id="c4cf9-295">Als u naar de vorige weergave wilt terugkeren, klikt u op **Gegevensfactory** in het koppelingenmenu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-295">To navigate back to the previous view, click **Data factory** in the breadcrumb menu at the top.</span></span>
5. <span data-ttu-id="c4cf9-296">Dubbelklik in de **diagramweergave** op de gegevensset **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-296">In the **Diagram View**, double-click the dataset **AzureBlobInput**.</span></span> <span data-ttu-id="c4cf9-297">Controleer of het segment de status **Gereed** heeft.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-297">Confirm that the slice is in **Ready** state.</span></span> <span data-ttu-id="c4cf9-298">Het kan enkele minuten duren voordat het segment de status Gereed heeft.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-298">It may take a couple of minutes for the slice to show up in Ready state.</span></span> <span data-ttu-id="c4cf9-299">Als dit niet is gebeurd nadat u enige tijd hebt gewacht, controleert u of het invoerbestand (input.log) in de juiste container (adfgetstarted) en in de juiste map (inputdata) staat.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-299">If it does not happen after you wait for sometime, see if you have the input file (input.log) placed in the right container (adfgetstarted) and folder (inputdata).</span></span>

   ![Invoersegment met de status Gereed](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. <span data-ttu-id="c4cf9-301">Klik op **X** om de blade **AzureBlobInput** te sluiten.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-301">Click **X** to close **AzureBlobInput** blade.</span></span>
7. <span data-ttu-id="c4cf9-302">Dubbelklik in de **diagramweergave** op de gegevensset **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-302">In the **Diagram View**, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="c4cf9-303">U ziet het segment dat momenteel wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-303">You see that the slice that is currently being processed.</span></span>

   ![Gegevensset](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. <span data-ttu-id="c4cf9-305">Als het verwerken is voltooid, ziet u dat het segment de status **Gereed** heeft.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-305">When processing is done, you see the slice in **Ready** state.</span></span>

   ![Gegevensset](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > <span data-ttu-id="c4cf9-307">Het maken van een on-demand HDInsight-cluster duurt normaal gesproken enige tijd (ongeveer 20 minuten).</span><span class="sxs-lookup"><span data-stu-id="c4cf9-307">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="c4cf9-308">Daarom kunt u ervan uitgaan dat het **ongeveer 30 minuten** duurt voordat het segment in de pijplijn is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-308">Therefore, expect the pipeline to       take **approximately 30 minutes** to process the slice.</span></span>
   >
   >

9. <span data-ttu-id="c4cf9-309">Wanneer het segment de status **Gereed** heeft, controleert u de map **partitioneddata** in de container **adfgetstarted** in uw blobopslag voor de uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-309">When the slice is in **Ready** state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  

   ![Uitvoergegevens](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. <span data-ttu-id="c4cf9-311">Klik op het segment voor details van het segment in de blade **Gegevenssegment**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-311">Click the slice to see details about it in a **Data slice** blade.</span></span>

   ![Details gegevenssegment](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. <span data-ttu-id="c4cf9-313">Klik in de lijst **Uitvoeringen van activiteit** op een activiteit die wordt uitgevoerd om details van een bepaalde activiteit die wordt uitgevoerd (Hive-activiteit in ons scenario) te bekijken in het venster **Details uitvoering van activiteit**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-313">Click an activity run in the **Activity runs list** to see details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span>   

   ![Details uitvoering van activiteit](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   <span data-ttu-id="c4cf9-315">In de logboekbestanden ziet u de Hive-query die is uitgevoerd en de statusinformatie.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-315">From the log files, you can see the Hive query that was executed and status information.</span></span> <span data-ttu-id="c4cf9-316">Deze logboeken komen van pas bij het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-316">These logs are useful for troubleshooting any issues.</span></span>
   <span data-ttu-id="c4cf9-317">Zie [Pijplijnen bewaken en beheren met Azure Portal-blades](data-factory-monitor-manage-pipelines.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-317">See [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) article for more details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4cf9-318">Het invoerbestand wordt verwijderd zodra het segment is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-318">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="c4cf9-319">Als u het segment dus opnieuw wilt uitvoeren of als u de zelfstudie opnieuw wilt doorlopen, uploadt u het invoerbestand (input.log) naar de map met invoergegevens van de container adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-319">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="c4cf9-320">De pijplijn bewaken met de app Bewaking en beheer</span><span class="sxs-lookup"><span data-stu-id="c4cf9-320">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="c4cf9-321">U kunt de toepassing Bewaking en beheer ook gebruiken om uw pijplijnen te bewaken.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-321">You can also use Monitor & Manage application to monitor your pipelines.</span></span> <span data-ttu-id="c4cf9-322">Zie [Azure Data Factory-pijplijnen bewaken en beheren met de app voor bewaking en beheer](data-factory-monitor-manage-app.md) voor meer informatie over het gebruik van deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-322">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="c4cf9-323">Klik op de tegel **Bewaking en beheer** op de startpagina van uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-323">Click **Monitor & Manage** tile on the home page for your data factory.</span></span>

    ![De tegel Bewaking en beheer](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. <span data-ttu-id="c4cf9-325">De toepassing **Bewaking en beheer** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-325">You should see **Monitor & Manage application**.</span></span> <span data-ttu-id="c4cf9-326">Wijzig **Begintijd** en **Eindtijd** zodanig dat deze overeenkomen met de starttijd en de eindtijd van uw pijplijn. Klik vervolgens op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-326">Change the **Start time** and **End time** to match start and end times of your pipeline, and click **Apply**.</span></span>

    ![De app Bewaking en beheer](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. <span data-ttu-id="c4cf9-328">Selecteer een activiteitsvenster in de lijst **Activiteitsvensters** voor details van dit venster.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-328">Select an activity window in the **Activity Windows** list to see details about it.</span></span>

    ![Details van activiteitsvenster](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a><span data-ttu-id="c4cf9-330">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="c4cf9-330">Summary</span></span>
<span data-ttu-id="c4cf9-331">In deze zelfstudie hebt u een Azure-gegevensfactory gemaakt voor het verwerken van gegevens. Dit hebt u gedaan door Hive-script uit te voeren op een HDInsight Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-331">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="c4cf9-332">U hebt in de Azure Portal de Data Factory-editor gebruikt om de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="c4cf9-332">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>  

1. <span data-ttu-id="c4cf9-333">U hebt een Azure-**gegevensfactory** gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-333">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="c4cf9-334">U hebt twee **gekoppelde services** gemaakt:</span><span class="sxs-lookup"><span data-stu-id="c4cf9-334">Created two **linked services**:</span></span>
   1. <span data-ttu-id="c4cf9-335">Een gekoppelde **Azure Storage**-service om te koppelen aan de Azure-blobopslag die de invoer-/uitvoerbestanden van de gegevensfactory bevat.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-335">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="c4cf9-336">Een gekoppelde on-demand **Azure HDInsight**-service om te koppelen aan een on-demand HDInsight Hadoop-cluster van de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-336">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="c4cf9-337">Azure Data Factory maakt op tijd een HDInsight Hadoop-cluster om invoergegevens te verwerken en uitvoergegevens te produceren.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-337">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="c4cf9-338">U hebt twee **gegevenssets** gemaakt, waarin de invoer- en uitvoergegevens van de HDInsight Hive-activiteit in de pijplijn worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-338">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="c4cf9-339">U hebt een **pijplijn** gemaakt met een **HDInsight Hive**-activiteit.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-339">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4cf9-340">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c4cf9-340">Next Steps</span></span>
<span data-ttu-id="c4cf9-341">In dit artikel hebt u een pijplijn gemaakt met een transformatieactiviteit (HDInsight-activiteit) waarvoor een Hive-script wordt uitgevoerd op een on-demand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-341">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="c4cf9-342">Zie [Zelfstudie: gegevens van een Azure-blob kopiëren naar Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor meer informatie over het gebruik van een kopieeractiviteit om gegevens van een Azure-blob te kopiëren naar Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-342">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="c4cf9-343">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c4cf9-343">See Also</span></span>
| <span data-ttu-id="c4cf9-344">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="c4cf9-344">Topic</span></span> | <span data-ttu-id="c4cf9-345">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c4cf9-345">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="c4cf9-346">Pijplijnen</span><span class="sxs-lookup"><span data-stu-id="c4cf9-346">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="c4cf9-347">Met behulp van dit artikel krijgt u inzicht in de pijplijnen en activiteiten in Azure Data Factory en in de wijze waarop u deze kunt gebruiken om end-to-end gegevensgestuurde werkstromen te maken voor uw scenario of bedrijf.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-347">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="c4cf9-348">Gegevenssets</span><span class="sxs-lookup"><span data-stu-id="c4cf9-348">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="c4cf9-349">Op basis van dit artikel krijgt u inzicht in de gegevenssets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-349">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="c4cf9-350">Plannen en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c4cf9-350">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="c4cf9-351">In dit artikel wordt uitleg gegeven over de plannings- en uitvoeringsaspecten van het Azure Data Factory-toepassingsmodel.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-351">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="c4cf9-352">Pijplijnen bewaken en beheren met de app voor bewaking en beheer</span><span class="sxs-lookup"><span data-stu-id="c4cf9-352">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="c4cf9-353">In dit artikel wordt beschreven hoe u pijplijnen bewaakt en beheert en hoe u fouten hierin oplost met de app voor bewaking en beheer.</span><span class="sxs-lookup"><span data-stu-id="c4cf9-353">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
