---
title: aaaBuild uw eerste gegevensfactory (Azure-portal) | Microsoft Docs
description: In deze zelfstudie maakt u een Azure Data Factory-voorbeeldpijplijn met behulp van de Data Factory-Editor in hello Azure-portal.
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
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a><span data-ttu-id="6e609-103">Zelfstudie: uw eerste Azure-gegevensfactory bouwen met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6e609-103">Tutorial: Build your first Azure data factory using Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6e609-104">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="6e609-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="6e609-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6e609-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="6e609-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6e609-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="6e609-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e609-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="6e609-108">Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="6e609-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="6e609-109">REST API</span><span class="sxs-lookup"><span data-stu-id="6e609-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)


<span data-ttu-id="6e609-110">In dit artikel leert u hoe toouse [Azure-portal](https://portal.azure.com/) toocreate uw eerste Azure-gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="6e609-110">In this article, you learn how toouse [Azure portal](https://portal.azure.com/) toocreate your first Azure data factory.</span></span> <span data-ttu-id="6e609-111">toodo hello zelfstudie met andere hulpprogramma's / SDK, selecteer een van de Hallo opties uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e609-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span> 

<span data-ttu-id="6e609-112">Hallo-pijplijn in deze zelfstudie is één activiteit: **HDInsight Hive-activiteit**.</span><span class="sxs-lookup"><span data-stu-id="6e609-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="6e609-113">Deze activiteit wordt een hive-script uitgevoerd op een Azure HDInsight-cluster dat transformaties invoergegevens gegevens tooproduce uitvoer.</span><span class="sxs-lookup"><span data-stu-id="6e609-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="6e609-114">Hallo pijplijn is geplande toorun wanneer een maand tussen Hallo begin- en eindtijden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6e609-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="6e609-115">Hallo gegevens pijplijn in deze zelfstudie getransformeerd invoergegevens tooproduce uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="6e609-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="6e609-116">Voor een zelfstudie over het toocopy van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: gegevens kopiëren van Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="6e609-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="6e609-117">Een pijplijn kan meer dan één activiteit hebben.</span><span class="sxs-lookup"><span data-stu-id="6e609-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="6e609-118">En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="6e609-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="6e609-119">Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6e609-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e609-120">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6e609-120">Prerequisites</span></span>
1. <span data-ttu-id="6e609-121">Lees [overzicht van de zelfstudie](data-factory-build-your-first-pipeline.md) artikel en volledige Hallo **vereiste** stappen.</span><span class="sxs-lookup"><span data-stu-id="6e609-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
2. <span data-ttu-id="6e609-122">In dit artikel biedt geen conceptueel overzicht van hello Azure Data Factory-service.</span><span class="sxs-lookup"><span data-stu-id="6e609-122">This article does not provide a conceptual overview of hello Azure Data Factory service.</span></span> <span data-ttu-id="6e609-123">Het is raadzaam dat u doorloopt [inleiding tooAzure Data Factory](data-factory-introduction.md) voor een gedetailleerd overzicht van Hallo service het artikel.</span><span class="sxs-lookup"><span data-stu-id="6e609-123">We recommend that you go through [Introduction tooAzure Data Factory](data-factory-introduction.md) article for a detailed overview of hello service.</span></span>  

## <a name="create-data-factory"></a><span data-ttu-id="6e609-124">Een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="6e609-124">Create data factory</span></span>
<span data-ttu-id="6e609-125">Een gegevensfactory kan één of meer pijplijnen hebben.</span><span class="sxs-lookup"><span data-stu-id="6e609-125">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="6e609-126">Een pijplijn kan één of meer activiteiten bevatten.</span><span class="sxs-lookup"><span data-stu-id="6e609-126">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="6e609-127">Bijvoorbeeld invoergegevens een Kopieeractiviteit toocopy-gegevens van een doelgegevensopslagplaats tooa bron en het toorun in een HDInsight Hive-activiteit een Hive-script tootransform gegevens tooproduct uitvoer.</span><span class="sxs-lookup"><span data-stu-id="6e609-127">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="6e609-128">Laten we beginnen met het maken van de gegevensfactory Hallo in deze stap.</span><span class="sxs-lookup"><span data-stu-id="6e609-128">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="6e609-129">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6e609-129">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6e609-130">Klik op **nieuw** op Hallo menu links, klikt u op **gegevens en analyse**, en klik op **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="6e609-130">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>

   ![Blade maken](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. <span data-ttu-id="6e609-132">In Hallo **nieuwe gegevensfactory** blade Voer **GetStartedDF** voor Hallo naam.</span><span class="sxs-lookup"><span data-stu-id="6e609-132">In hello **New data factory** blade, enter **GetStartedDF** for hello Name.</span></span>

   ![Blade voor een nieuwe gegevensfactory](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > <span data-ttu-id="6e609-134">Hallo-naam van hello Azure-gegevensfactory moet **globaal unieke**.</span><span class="sxs-lookup"><span data-stu-id="6e609-134">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="6e609-135">Als u de foutmelding Hallo: **Data factory-naam 'GetStartedDF' is niet beschikbaar**.</span><span class="sxs-lookup"><span data-stu-id="6e609-135">If you receive hello error: **Data factory name “GetStartedDF” is not available**.</span></span> <span data-ttu-id="6e609-136">Hallo-naam van gegevensfactory hello (bijvoorbeeld Uwnaamgetstarteddf) wijzigen en probeer het opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="6e609-136">Change hello name of hello data factory (for example, yournameGetStartedDF) and try creating again.</span></span> <span data-ttu-id="6e609-137">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="6e609-137">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
   >
   > <span data-ttu-id="6e609-138">Hallo-naam van de gegevensfactory Hallo mogelijk geregistreerd als een **DNS** naam in de toekomst Hallo en daarmee ook voor iedereen zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="6e609-138">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="6e609-139">Selecteer Hallo **Azure-abonnement** waar u Hallo data factory toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6e609-139">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="6e609-140">Selecteer een bestaande **resourcegroep** of maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="6e609-140">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="6e609-141">Maak een resourcegroep met de naam voor Hallo-zelfstudie: **ADFGetStartedRG**.</span><span class="sxs-lookup"><span data-stu-id="6e609-141">For hello tutorial, create a resource group named: **ADFGetStartedRG**.</span></span>
6. <span data-ttu-id="6e609-142">Selecteer Hallo **locatie** voor Hallo data factory.</span><span class="sxs-lookup"><span data-stu-id="6e609-142">Select hello **location** for hello data factory.</span></span> <span data-ttu-id="6e609-143">Regio's wordt ondersteund door Hallo Data Factory-service worden weergegeven in de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e609-143">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
7. <span data-ttu-id="6e609-144">Selecteer **pincode toodashboard**.</span><span class="sxs-lookup"><span data-stu-id="6e609-144">Select **Pin toodashboard**.</span></span> 
8. <span data-ttu-id="6e609-145">Klik op **maken** op Hallo **nieuwe gegevensfactory** blade.</span><span class="sxs-lookup"><span data-stu-id="6e609-145">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="6e609-146">toocreate Data Factory-exemplaren, moet u lid zijn van Hallo [Data Factory Inzender](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol op het niveau van de Hallo abonnement/resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="6e609-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="6e609-147">Op Hallo-dashboard ziet er Hallo tegel met de status: implementatie van de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="6e609-147">On hello dashboard, you see hello following tile with status: Deploying data factory.</span></span>    

   ![Status van gegevensfactory maken](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. <span data-ttu-id="6e609-149">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="6e609-149">Congratulations!</span></span> <span data-ttu-id="6e609-150">U hebt uw eerste gegevensfactory gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6e609-150">You have successfully created your first data factory.</span></span> <span data-ttu-id="6e609-151">Nadat het Hallo-gegevensfactory is gemaakt, ziet u Hallo data factory-pagina waarop u inhoud van de gegevensfactory Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e609-151">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>     

    ![Blade Gegevensfactory](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

<span data-ttu-id="6e609-153">Voordat u een pijplijn maakt in de gegevensfactory hello, moet u toocreate enkele Data Factory-entiteiten eerst.</span><span class="sxs-lookup"><span data-stu-id="6e609-153">Before creating a pipeline in hello data factory, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="6e609-154">Maakt u eerst gekoppelde services toolink gegevens/berekeningen tooyour gegevens opslaan, definieert u welke invoer en uitvoer van gegevenssets toorepresent i/o-gegevens in de gekoppelde gegevensopslag en vervolgens Hallo pijplijn maken met een activiteit die gebruikmaakt van deze gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="6e609-154">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="6e609-155">Gekoppelde services maken</span><span class="sxs-lookup"><span data-stu-id="6e609-155">Create linked services</span></span>
<span data-ttu-id="6e609-156">In deze stap koppelt u uw Azure-opslagaccount en een bellen op Azure HDInsight-cluster tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="6e609-156">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="6e609-157">Hallo blokkeringen Hallo invoer en uitvoer-gegevens voor de pijplijn in dit voorbeeld hello Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="6e609-157">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="6e609-158">Hallo gekoppelde HDInsight-service is gebruikte toorun een Hive-script dat is opgegeven in de activiteit Hallo van Hallo pijplijn in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="6e609-158">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="6e609-159">Bepalen wat [gegevensarchief](data-factory-data-movement-activities.md)/[compute-services](data-factory-compute-linked-services.md) worden gebruikt in uw scenario en koppelen van deze services toohello-gegevensfactory door gekoppelde services te maken.</span><span class="sxs-lookup"><span data-stu-id="6e609-159">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario and link those services toohello data factory by creating linked services.</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="6e609-160">Een gekoppelde Azure Storage-service maken</span><span class="sxs-lookup"><span data-stu-id="6e609-160">Create Azure Storage linked service</span></span>
<span data-ttu-id="6e609-161">In deze stap koppelt u uw Azure Storage-account tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="6e609-161">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="6e609-162">In deze zelfstudie gebruikt u Hallo dezelfde Azure-opslagaccount invoer-en uitvoergegevens toostore en Hallo HQL-script bestand.</span><span class="sxs-lookup"><span data-stu-id="6e609-162">In this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="6e609-163">Klik op **auteur en implementeren van** op Hallo **DATA FACTORY** blade voor **GetStartedDF**.</span><span class="sxs-lookup"><span data-stu-id="6e609-163">Click **Author and deploy** on hello **DATA FACTORY** blade for **GetStartedDF**.</span></span> <span data-ttu-id="6e609-164">U ziet Hallo Data Factory-Editor.</span><span class="sxs-lookup"><span data-stu-id="6e609-164">You should see hello Data Factory Editor.</span></span>

   ![Tegel ontwerpen en implementeren](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. <span data-ttu-id="6e609-166">Klik op **Nieuwe gegevensopslag** en kies **Azure-opslag**.</span><span class="sxs-lookup"><span data-stu-id="6e609-166">Click **New data store** and choose **Azure storage**.</span></span>

   ![Nieuwe gegevensopslag - Azure Storage - menu](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="6e609-168">U ziet Hallo JSON-script voor het maken van een Azure Storage gekoppelde service in Hallo-editor.</span><span class="sxs-lookup"><span data-stu-id="6e609-168">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![Een gekoppelde Azure Storage-service](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="6e609-170">Vervang **accountnaam** met Hallo-naam van uw Azure storage-account en **accountsleutel** door de toegangssleutel Hallo van hello Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="6e609-170">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="6e609-171">toolearn hoe tooget uw opslag heeft toegang tot sleutel, raadpleegt u Hallo informatie over hoe tooview, kopiëren en opnieuw genereren opslag toegangstoetsen in [uw opslagaccount beheren](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="6e609-171">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="6e609-172">Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="6e609-172">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![Implementatieknop](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   <span data-ttu-id="6e609-174">Nadat hello gekoppelde service is geïmplementeerd, Hallo **Draft-1** venster verdwijnt en ziet u **AzureStorageLinkedService** in Hallo structuurweergave Hallo links.</span><span class="sxs-lookup"><span data-stu-id="6e609-174">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

    ![Een gekoppelde opslagservice in het menu](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="6e609-176">Een gekoppelde HDInsight-service maken</span><span class="sxs-lookup"><span data-stu-id="6e609-176">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="6e609-177">In deze stap maakt koppelen u een gegevensfactory op aanvraag HDInsight-cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="6e609-177">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="6e609-178">Hallo HDInsight-cluster wordt automatisch gemaakt tijdens runtime en na het verwerken is voltooid en niet-actieve voor de opgegeven tijdsduur Hallo verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6e609-178">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span>

1. <span data-ttu-id="6e609-179">In Hallo **Data Factory-Editor**, klikt u op **... Meer** en op **Nieuwe berekening**. Selecteer vervolgens **On-demand HDInsight-cluster**.</span><span class="sxs-lookup"><span data-stu-id="6e609-179">In hello **Data Factory Editor**, click **... More**, click **New compute**, and select **On-demand HDInsight cluster**.</span></span>

    ![Nieuwe berekening](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. <span data-ttu-id="6e609-181">Kopieer en plak de volgende codefragment toohello hello **Draft-1** venster.</span><span class="sxs-lookup"><span data-stu-id="6e609-181">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="6e609-182">Hallo JSON-codefragment bevat de Hallo-eigenschappen die gebruikt toocreate hello HDInsight-cluster op de aanvraag zijn.</span><span class="sxs-lookup"><span data-stu-id="6e609-182">hello JSON snippet describes hello properties that are used toocreate hello HDInsight cluster on-demand.</span></span>

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

    <span data-ttu-id="6e609-183">Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:</span><span class="sxs-lookup"><span data-stu-id="6e609-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="6e609-184">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="6e609-184">Property</span></span> | <span data-ttu-id="6e609-185">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6e609-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="6e609-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="6e609-186">ClusterSize</span></span> |<span data-ttu-id="6e609-187">Hiermee wordt de grootte Hallo van Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6e609-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="6e609-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="6e609-188">TimeToLive</span></span> | <span data-ttu-id="6e609-189">Hiermee geeft u op dat niet-actieve tijd Hallo voor Hallo HDInsight-cluster, voordat deze wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6e609-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="6e609-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="6e609-190">linkedServiceName</span></span> | <span data-ttu-id="6e609-191">Hiermee geeft u Hallo storage-account dat is gebruikt toostore Hallo logboeken die door HDInsight worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="6e609-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight.</span></span> |

    <span data-ttu-id="6e609-192">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="6e609-192">Note hello following points:</span></span>

   * <span data-ttu-id="6e609-193">Hallo Data Factory maakt een **op basis van Linux** HDInsight-cluster voor u Hello JSON.</span><span class="sxs-lookup"><span data-stu-id="6e609-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="6e609-194">Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6e609-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="6e609-195">U kunt **uw eigen HDInsight-cluster** gebruiken in plaats van een on-demand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6e609-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="6e609-196">Zie [Gekoppelde HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6e609-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="6e609-197">Hallo HDInsight-cluster maakt een **standaardcontainer** in Hallo-blobopslag die u hebt opgegeven in Hallo JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="6e609-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="6e609-198">HDInsight verwijdert deze container niet wanneer Hallo-cluster is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6e609-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="6e609-199">Dit gedrag is standaard.</span><span class="sxs-lookup"><span data-stu-id="6e609-199">This behavior is by design.</span></span> <span data-ttu-id="6e609-200">Met een gekoppelde on-demand HDInsight-service wordt er steeds een HDInsight-cluster gemaakt wanneer er een segment wordt verwerkt, tenzij er een bestaand livecluster is (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="6e609-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="6e609-201">Hallo-cluster wordt automatisch verwijderd als het Hallo-verwerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="6e609-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="6e609-202">Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="6e609-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="6e609-203">Als u niet ze hoeft voor het oplossen van problemen met taken hello, kunt u toodelete ze tooreduce Hallo opslag kosten.</span><span class="sxs-lookup"><span data-stu-id="6e609-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="6e609-204">Hallo-namen van deze containers worden als volgt: ' adf**naamvanuwgegevensfactory**-**linkedservicename**- datum '.</span><span class="sxs-lookup"><span data-stu-id="6e609-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="6e609-205">Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) toodelete containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="6e609-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="6e609-206">Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6e609-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
3. <span data-ttu-id="6e609-207">Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="6e609-207">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![Gekoppelde on-demand HDInsight-service implementeren](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. <span data-ttu-id="6e609-209">Controleer of u beide **AzureStorageLinkedService** en **HDInsightOnDemandLinkedService** in Hallo structuurweergave Hallo links.</span><span class="sxs-lookup"><span data-stu-id="6e609-209">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in hello tree view on hello left.</span></span>

    ![Structuurweergave met gekoppelde services](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a><span data-ttu-id="6e609-211">Gegevenssets maken</span><span class="sxs-lookup"><span data-stu-id="6e609-211">Create datasets</span></span>
<span data-ttu-id="6e609-212">In deze stap maakt u gegevenssets toorepresent Hallo invoer maken en uitvoergegevens voor Hive-verwerking.</span><span class="sxs-lookup"><span data-stu-id="6e609-212">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="6e609-213">Deze gegevenssets verwijzen toohello **AzureStorageLinkedService** u eerder in deze zelfstudie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6e609-213">These datasets refer toohello **AzureStorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="6e609-214">Hallo gekoppelde service verwijst tooan Azure Storage-account en gegevenssets vindt u container, map en bestandsnaam in Hallo opslag van de invoer- en uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="6e609-214">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>   

### <a name="create-input-dataset"></a><span data-ttu-id="6e609-215">Invoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="6e609-215">Create input dataset</span></span>
1. <span data-ttu-id="6e609-216">In Hallo **Data Factory-Editor**, klikt u op **... Meer** op de opdrachtbalk hello, klikt u op **nieuwe gegevensset**, en selecteer **Azure Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="6e609-216">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>

    ![Nieuwe gegevensset](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. <span data-ttu-id="6e609-218">Kopieer en plak Hallo na codefragment toohello Draft-1-venster.</span><span class="sxs-lookup"><span data-stu-id="6e609-218">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="6e609-219">Hallo JSON-codefragment maakt u maakt in een gegevensset met de naam **AzureBlobInput** die staat voor invoergegevens van een activiteit in Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="6e609-219">In hello JSON snippet, you are creating a dataset called **AzureBlobInput** that represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="6e609-220">Bovendien u opgeven dat Hallo invoergegevens in de blob-container Hallo aangeroepen bevinden zich **adfgetstarted** en Hallo map met de naam **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="6e609-220">In addition, you specify that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

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
    <span data-ttu-id="6e609-221">Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:</span><span class="sxs-lookup"><span data-stu-id="6e609-221">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="6e609-222">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="6e609-222">Property</span></span> | <span data-ttu-id="6e609-223">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6e609-223">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="6e609-224">type</span><span class="sxs-lookup"><span data-stu-id="6e609-224">type</span></span> |<span data-ttu-id="6e609-225">Hallo type wordt ingesteld te**AzureBlob** omdat de gegevens zich in een Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="6e609-225">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
   | <span data-ttu-id="6e609-226">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="6e609-226">linkedServiceName</span></span> |<span data-ttu-id="6e609-227">Toohello verwijst **AzureStorageLinkedService** u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6e609-227">Refers toohello **AzureStorageLinkedService** you created earlier.</span></span> |
   | <span data-ttu-id="6e609-228">folderPath</span><span class="sxs-lookup"><span data-stu-id="6e609-228">folderPath</span></span> | <span data-ttu-id="6e609-229">Hiermee geeft u op Hallo blob **container** en Hallo **map** die invoer blobs bevat.</span><span class="sxs-lookup"><span data-stu-id="6e609-229">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> | 
   | <span data-ttu-id="6e609-230">fileName</span><span class="sxs-lookup"><span data-stu-id="6e609-230">fileName</span></span> |<span data-ttu-id="6e609-231">Deze eigenschap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="6e609-231">This property is optional.</span></span> <span data-ttu-id="6e609-232">Als u deze eigenschap niet opgeeft, worden alle Hallo-bestanden uit folderPath Hallo opgenomen.</span><span class="sxs-lookup"><span data-stu-id="6e609-232">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="6e609-233">In deze zelfstudie alleen Hallo **input.log** wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="6e609-233">In this tutorial, only hello **input.log** is processed.</span></span> |
   | <span data-ttu-id="6e609-234">type</span><span class="sxs-lookup"><span data-stu-id="6e609-234">type</span></span> |<span data-ttu-id="6e609-235">Hallo-logboekbestanden tekstbestanden zijn, zodat we gebruiken **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="6e609-235">hello log files are in text format, so we use **TextFormat**.</span></span> |
   | <span data-ttu-id="6e609-236">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="6e609-236">columnDelimiter</span></span> |<span data-ttu-id="6e609-237">kolommen in Hallo logboekbestanden worden gescheiden door **kommateken (`,`)**</span><span class="sxs-lookup"><span data-stu-id="6e609-237">columns in hello log files are delimited by **comma character (`,`)**</span></span> |
   | <span data-ttu-id="6e609-238">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="6e609-238">frequency/interval</span></span> |<span data-ttu-id="6e609-239">frequentie ingesteld te**maand** en interval is **1**, wat betekent dat Hallo invoer segmenten maandelijks beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="6e609-239">frequency set too**Month** and interval is **1**, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="6e609-240">external</span><span class="sxs-lookup"><span data-stu-id="6e609-240">external</span></span> | <span data-ttu-id="6e609-241">Deze eigenschap is ingesteld, te**true** als Hallo invoergegevens niet worden gegenereerd door deze pijplijn.</span><span class="sxs-lookup"><span data-stu-id="6e609-241">This property is set too**true** if hello input data is not generated by this pipeline.</span></span> <span data-ttu-id="6e609-242">In deze zelfstudie Hallo input.log bestand niet worden gegenereerd door deze pipeline zodat we Hallo eigenschap tootrue instellen.</span><span class="sxs-lookup"><span data-stu-id="6e609-242">In this tutorial, hello input.log file is not generated by this pipeline, so we set hello property tootrue.</span></span> |

    <span data-ttu-id="6e609-243">Zie het [artikel over Azure Blob-connectoren](data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over deze JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="6e609-243">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="6e609-244">Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo nieuwe gegevensset.</span><span class="sxs-lookup"><span data-stu-id="6e609-244">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span> <span data-ttu-id="6e609-245">U ziet de gegevensset in Hallo structuurweergave links Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e609-245">You should see hello dataset in hello tree view on hello left.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="6e609-246">Uitvoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="6e609-246">Create output dataset</span></span>
<span data-ttu-id="6e609-247">U maakt nu Hallo gegevensset toorepresent Hallo uitvoer uitvoergegevens opgeslagen in hello Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="6e609-247">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="6e609-248">In Hallo **Data Factory-Editor**, klikt u op **... Meer** op de opdrachtbalk hello, klikt u op **nieuwe gegevensset**, en selecteer **Azure Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="6e609-248">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="6e609-249">Kopieer en plak Hallo na codefragment toohello Draft-1-venster.</span><span class="sxs-lookup"><span data-stu-id="6e609-249">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="6e609-250">Hallo JSON-codefragment maakt u maakt in een gegevensset met de naam **AzureBlobOutput**, en geeft u op Hallo van Hallo-gegevens die door Hallo Hive-script wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="6e609-250">In hello JSON snippet, you are creating a dataset called **AzureBlobOutput**, and specifying hello structure of hello data that is produced by hello Hive script.</span></span> <span data-ttu-id="6e609-251">Bovendien u opgeven dat Hallo resultaten worden opgeslagen in blob-container Hallo aangeroepen **adfgetstarted** en Hallo map met de naam **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="6e609-251">In addition, you specify that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="6e609-252">Hallo **beschikbaarheid** sectie geeft die Hallo-uitvoergegevensset op maandelijkse basis wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="6e609-252">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

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
    <span data-ttu-id="6e609-253">Zie **hello invoergegevensset maken** sectie voor beschrijvingen van deze eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="6e609-253">See **Create hello input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="6e609-254">U instelt geen Hallo externe eigenschap op een uitvoergegevensset omdat Hallo gegevensset wordt geproduceerd door Hallo Data Factory-service.</span><span class="sxs-lookup"><span data-stu-id="6e609-254">You do not set hello external property on an output dataset as hello dataset is produced by hello Data Factory service.</span></span>
3. <span data-ttu-id="6e609-255">Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo nieuwe gegevensset.</span><span class="sxs-lookup"><span data-stu-id="6e609-255">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span>
4. <span data-ttu-id="6e609-256">Controleer of dat deze Hallo gegevensset is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6e609-256">Verify that hello dataset is created successfully.</span></span>

    ![Structuurweergave met gekoppelde services](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a><span data-ttu-id="6e609-258">Pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="6e609-258">Create pipeline</span></span>
<span data-ttu-id="6e609-259">In deze stap maakt u uw eerste pijplijn met een **HDInsightHive**-activiteit.</span><span class="sxs-lookup"><span data-stu-id="6e609-259">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="6e609-260">Invoersegment maandelijks beschikbaar is (frequency: Month, interval: 1), uitvoer segment wordt geproduceerd, maandelijks en Hallo scheduler-eigenschap voor activiteit Hallo toomonthly ook is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6e609-260">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="6e609-261">Hallo-instellingen voor Hallo uitvoergegevensset en Hallo activiteitenplanner moeten overeenkomen met.</span><span class="sxs-lookup"><span data-stu-id="6e609-261">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="6e609-262">Uitvoergegevensset is momenteel welke stations Hallo planning, dus u een uitvoergegevensset maken moet, zelfs als Hallo activiteit geen uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="6e609-262">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="6e609-263">Als Hallo activiteit geen invoer neemt, kunt u maken Hallo invoergegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="6e609-263">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="6e609-264">Hallo-eigenschappen die in de volgende JSON Hallo worden aan Hallo einde van deze sectie beschreven.</span><span class="sxs-lookup"><span data-stu-id="6e609-264">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="6e609-265">In Hallo **Data Factory-Editor**, klikt u op **weglatingsteken (...) Meer opdrachten** en klik vervolgens op **nieuwe pijplijn**.</span><span class="sxs-lookup"><span data-stu-id="6e609-265">In hello **Data Factory Editor**, click **Ellipsis (…) More commands** and then click **New pipeline**.</span></span>

    ![Knop Nieuw pijplijn](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. <span data-ttu-id="6e609-267">Kopieer en plak Hallo na codefragment toohello Draft-1-venster.</span><span class="sxs-lookup"><span data-stu-id="6e609-267">Copy and paste hello following snippet toohello Draft-1 window.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="6e609-268">Vervang **storageaccountname** met de naam van uw opslagaccount in JSON Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e609-268">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
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

    <span data-ttu-id="6e609-269">In de JSON-codefragment hello maakt u een pijplijn die bestaat uit een enkele activiteit waarvoor gebruik van Hive tooprocess gegevens op een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6e609-269">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="6e609-270">Hallo Hive-scriptbestand **partitionweblogs.hql**, wordt opgeslagen in hello Azure storage-account (Hallo door scriptLinkedService met de opgegeven **AzureStorageLinkedService**), en in  **script** map in container Hallo **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="6e609-270">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="6e609-271">Hallo **definieert** sectie is gebruikte toospecify Hallo runtime-instellingen die toohello hive-script worden doorgegeven als Hive-configuratiewaarden (bijvoorbeeld ${hiveconf: inputtable}, ${partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="6e609-271">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="6e609-272">Hallo **start** en **end** eigenschappen van de pijplijn Hallo geeft Hallo actieve periode van Hallo-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="6e609-272">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="6e609-273">In Hallo activiteits-JSON geeft u opgeven dat Hallo Hive-script wordt uitgevoerd op Hallo berekening die is opgegeven door Hallo **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="6e609-273">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6e609-274">Zie 'Pijplijn-JSON' in [pijplijnen en activiteiten in Azure Data Factory](data-factory-create-pipelines.md) voor meer informatie over de JSON-eigenschappen die in Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="6e609-274">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello example.</span></span>
   >
   >
3. <span data-ttu-id="6e609-275">Bevestig Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="6e609-275">Confirm hello following:</span></span>

   1. <span data-ttu-id="6e609-276">**Input.log** bestand aanwezig is op Hallo **inputdata** map Hallo **adfgetstarted** container in hello Azure blob-opslag</span><span class="sxs-lookup"><span data-stu-id="6e609-276">**input.log** file exists in hello **inputdata** folder of hello **adfgetstarted** container in hello Azure blob storage</span></span>
   2. <span data-ttu-id="6e609-277">**partitionweblogs.hql** bestand aanwezig is op Hallo **script** map Hallo **adfgetstarted** container in hello Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="6e609-277">**partitionweblogs.hql** file exists in hello **script** folder of hello **adfgetstarted** container in hello Azure blob storage.</span></span> <span data-ttu-id="6e609-278">Volledige Hallo vereiste stappen voor het Hallo [overzicht van de zelfstudie](data-factory-build-your-first-pipeline.md) als u deze bestanden niet ziet.</span><span class="sxs-lookup"><span data-stu-id="6e609-278">Complete hello prerequisite steps in hello [Tutorial Overview](data-factory-build-your-first-pipeline.md) if you don't see these files.</span></span>
   3. <span data-ttu-id="6e609-279">Bevestig dat u hebt vervangen **storageaccountname** pijplijn met de naam van uw opslagaccount in Hallo Hallo JSON.</span><span class="sxs-lookup"><span data-stu-id="6e609-279">Confirm that you replaced **storageaccountname** with hello name of your storage account in hello pipeline JSON.</span></span>
4. <span data-ttu-id="6e609-280">Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="6e609-280">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span> <span data-ttu-id="6e609-281">Sinds Hallo **start** en **end** keren worden ingesteld in de afgelopen Hallo en **isPaused** set toofalse, Hallo pijplijn is (activiteit in de pijplijn Hallo) wordt uitgevoerd onmiddellijk nadat u hebt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="6e609-281">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>
5. <span data-ttu-id="6e609-282">Controleer of u Hallo pijplijn in de structuurweergave Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e609-282">Confirm that you see hello pipeline in hello tree view.</span></span>

    ![Structuurweergave met de pijplijn](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. <span data-ttu-id="6e609-284">U hebt uw eerste pijplijn gemaakt!</span><span class="sxs-lookup"><span data-stu-id="6e609-284">Congratulations, you have successfully created your first pipeline!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="6e609-285">De pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="6e609-285">Monitor pipeline</span></span>
### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="6e609-286">De pijplijn bewaken met Diagramweergave</span><span class="sxs-lookup"><span data-stu-id="6e609-286">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="6e609-287">Klik op **X** tooclose Data Factory-Editor blades toonavigate back-toohello Data Factory-blade en klik op **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="6e609-287">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![Tegel Diagram](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. <span data-ttu-id="6e609-289">In de diagramweergave hello ziet u een overzicht van Hallo pijplijnen en gegevenssets die in deze zelfstudie worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6e609-289">In hello Diagram View, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![Diagramweergave](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. <span data-ttu-id="6e609-291">tooview alle activiteiten in de pijplijn voor hello, klik met de rechtermuisknop pijplijn in Hallo diagram en klikt u op pijplijn openen.</span><span class="sxs-lookup"><span data-stu-id="6e609-291">tooview all activities in hello pipeline, right-click pipeline in hello diagram and click Open Pipeline.</span></span>

    ![Menu Pijplijn openen](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. <span data-ttu-id="6e609-293">Controleer of u Hallo HDInsightHive-activiteit in Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="6e609-293">Confirm that you see hello HDInsightHive activity in hello pipeline.</span></span>

    ![Pijplijnweergave openen](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    <span data-ttu-id="6e609-295">back-toonavigate toohello vorige weergave, klikt u op **Data factory** in Hallo breadcrumb menu Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="6e609-295">toonavigate back toohello previous view, click **Data factory** in hello breadcrumb menu at hello top.</span></span>
5. <span data-ttu-id="6e609-296">In Hallo **diagramweergave**, dubbelklikt u op Hallo gegevensset **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="6e609-296">In hello **Diagram View**, double-click hello dataset **AzureBlobInput**.</span></span> <span data-ttu-id="6e609-297">Bevestig dat segment Hallo **gereed** status.</span><span class="sxs-lookup"><span data-stu-id="6e609-297">Confirm that hello slice is in **Ready** state.</span></span> <span data-ttu-id="6e609-298">Het kan enkele minuten voor Hallo segment tooshow duren status Ready heeft.</span><span class="sxs-lookup"><span data-stu-id="6e609-298">It may take a couple of minutes for hello slice tooshow up in Ready state.</span></span> <span data-ttu-id="6e609-299">Als deze niet is gebeurd nadat u enige tijd wacht, ziet u of er Hallo invoerbestand (input.log in de juiste Hallo-container (adfgetstarted) en map (inputdata) geplaatst).</span><span class="sxs-lookup"><span data-stu-id="6e609-299">If it does not happen after you wait for sometime, see if you have hello input file (input.log) placed in hello right container (adfgetstarted) and folder (inputdata).</span></span>

   ![Invoersegment met de status Gereed](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. <span data-ttu-id="6e609-301">Klik op **X** tooclose **AzureBlobInput** blade.</span><span class="sxs-lookup"><span data-stu-id="6e609-301">Click **X** tooclose **AzureBlobInput** blade.</span></span>
7. <span data-ttu-id="6e609-302">In Hallo **diagramweergave**, dubbelklikt u op Hallo gegevensset **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="6e609-302">In hello **Diagram View**, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="6e609-303">U ziet dat Hallo-segment dat momenteel wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="6e609-303">You see that hello slice that is currently being processed.</span></span>

   ![Gegevensset](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. <span data-ttu-id="6e609-305">Wanneer het verwerken is voltooid, ziet u Hallo segment **gereed** status.</span><span class="sxs-lookup"><span data-stu-id="6e609-305">When processing is done, you see hello slice in **Ready** state.</span></span>

   ![Gegevensset](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > <span data-ttu-id="6e609-307">Het maken van een on-demand HDInsight-cluster duurt normaal gesproken enige tijd (ongeveer 20 minuten).</span><span class="sxs-lookup"><span data-stu-id="6e609-307">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="6e609-308">Daarom verwachten Hallo pipeline te laten **ongeveer 30 minuten** tooprocess Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="6e609-308">Therefore, expect hello pipeline too      take **approximately 30 minutes** tooprocess hello slice.</span></span>
   >
   >

9. <span data-ttu-id="6e609-309">Wanneer Hallo segment is in **gereed** staat, controleert u Hallo **partitioneddata** map in Hallo **adfgetstarted** container in uw blobopslag voor Hallo uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="6e609-309">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

   ![Uitvoergegevens](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. <span data-ttu-id="6e609-311">Klik op Hallo segment toosee details over deze in een **gegevenssegment** blade.</span><span class="sxs-lookup"><span data-stu-id="6e609-311">Click hello slice toosee details about it in a **Data slice** blade.</span></span>

   ![Details gegevenssegment](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. <span data-ttu-id="6e609-313">Klik op een activiteit die wordt uitgevoerd in Hallo **activiteit wordt uitgevoerd lijst** toosee details over een activiteit (Hive-activiteit in ons scenario) uitgevoerd in een **details uitvoering van activiteit** venster.</span><span class="sxs-lookup"><span data-stu-id="6e609-313">Click an activity run in hello **Activity runs list** toosee details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span>   

   ![Details uitvoering van activiteit](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   <span data-ttu-id="6e609-315">Uit Hallo-logboekbestanden ziet u Hallo Hive-query die is uitgevoerd en statusinformatie.</span><span class="sxs-lookup"><span data-stu-id="6e609-315">From hello log files, you can see hello Hive query that was executed and status information.</span></span> <span data-ttu-id="6e609-316">Deze logboeken komen van pas bij het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="6e609-316">These logs are useful for troubleshooting any issues.</span></span>
   <span data-ttu-id="6e609-317">Zie [Pijplijnen bewaken en beheren met Azure Portal-blades](data-factory-monitor-manage-pipelines.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6e609-317">See [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) article for more details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6e609-318">Hallo-invoerbestand wordt verwijderd zodra het Hallo-segment is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="6e609-318">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="6e609-319">Als u toorerun Hallo segment of zelfstudie opnieuw hello, dus Hallo invoerbestand (input.log) toohello inputdata map van de container adfgetstarted Hallo uploadt.</span><span class="sxs-lookup"><span data-stu-id="6e609-319">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="6e609-320">De pijplijn bewaken met de app Bewaking en beheer</span><span class="sxs-lookup"><span data-stu-id="6e609-320">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="6e609-321">U kunt ook controleren en beheren van toepassing toomonitor uw pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="6e609-321">You can also use Monitor & Manage application toomonitor your pipelines.</span></span> <span data-ttu-id="6e609-322">Zie [Azure Data Factory-pijplijnen bewaken en beheren met de app voor bewaking en beheer](data-factory-monitor-manage-app.md) voor meer informatie over het gebruik van deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="6e609-322">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="6e609-323">Klik op **Monitor & beheren** tegel op Hallo-startpagina van uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="6e609-323">Click **Monitor & Manage** tile on hello home page for your data factory.</span></span>

    ![De tegel Bewaking en beheer](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. <span data-ttu-id="6e609-325">De toepassing **Bewaking en beheer** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6e609-325">You should see **Monitor & Manage application**.</span></span> <span data-ttu-id="6e609-326">Wijziging Hallo **begintijd** en **eindtijd** toomatch start en eindtijd van de pijplijn en op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="6e609-326">Change hello **Start time** and **End time** toomatch start and end times of your pipeline, and click **Apply**.</span></span>

    ![De app Bewaking en beheer](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. <span data-ttu-id="6e609-328">Selecteer een venster van de activiteit in Hallo **Activiteitsvensters** toosee details over deze lijst.</span><span class="sxs-lookup"><span data-stu-id="6e609-328">Select an activity window in hello **Activity Windows** list toosee details about it.</span></span>

    ![Details van activiteitsvenster](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a><span data-ttu-id="6e609-330">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="6e609-330">Summary</span></span>
<span data-ttu-id="6e609-331">In deze zelfstudie maakt u een Azure data factory tooprocess gegevens gemaakt door het Hive-script uitvoeren op een HDInsight hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="6e609-331">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="6e609-332">U hebt gebruikt Hallo Data Factory-Editor in hello Azure portal toodo Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6e609-332">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>  

1. <span data-ttu-id="6e609-333">U hebt een Azure-**gegevensfactory** gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6e609-333">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="6e609-334">U hebt twee **gekoppelde services** gemaakt:</span><span class="sxs-lookup"><span data-stu-id="6e609-334">Created two **linked services**:</span></span>
   1. <span data-ttu-id="6e609-335">**Azure Storage** gekoppelde service toolink uw Azure-blobopslag die invoer-/ uitvoerbestanden toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="6e609-335">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="6e609-336">**Azure HDInsight** op aanvraag gekoppelde service toolink een bellen op HDInsight Hadoop-cluster toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="6e609-336">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="6e609-337">Azure Data Factory maakt een HDInsight Hadoop-cluster just in time tooprocess invoergegevens en uitvoergegevens produceren.</span><span class="sxs-lookup"><span data-stu-id="6e609-337">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="6e609-338">Twee gemaakt **gegevenssets**, die invoer- en gegevens voor HDInsight Hive-activiteit in Hallo pijplijn worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="6e609-338">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="6e609-339">U hebt een **pijplijn** gemaakt met een **HDInsight Hive**-activiteit.</span><span class="sxs-lookup"><span data-stu-id="6e609-339">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e609-340">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6e609-340">Next Steps</span></span>
<span data-ttu-id="6e609-341">In dit artikel hebt u een pijplijn gemaakt met een transformatieactiviteit (HDInsight-activiteit) waarvoor een Hive-script wordt uitgevoerd op een on-demand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6e609-341">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="6e609-342">hoe de gegevens van een Kopieeractiviteit toocopy van een Azure Blob-tooAzure SQL, toouse zien toosee [zelfstudie: gegevens kopiëren van een Azure blob-tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="6e609-342">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="6e609-343">Zie ook</span><span class="sxs-lookup"><span data-stu-id="6e609-343">See Also</span></span>
| <span data-ttu-id="6e609-344">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="6e609-344">Topic</span></span> | <span data-ttu-id="6e609-345">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6e609-345">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="6e609-346">Pijplijnen</span><span class="sxs-lookup"><span data-stu-id="6e609-346">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="6e609-347">In dit artikel helpt u begrijpen pijplijnen en activiteiten in Azure Data Factory en hoe toouse ze tooconstruct end-to-end gegevensgestuurde werkstromen voor uw scenario of bedrijf.</span><span class="sxs-lookup"><span data-stu-id="6e609-347">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="6e609-348">Gegevenssets</span><span class="sxs-lookup"><span data-stu-id="6e609-348">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="6e609-349">Op basis van dit artikel krijgt u inzicht in de gegevenssets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6e609-349">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="6e609-350">Plannen en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="6e609-350">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="6e609-351">Dit artikel wordt uitgelegd Hallo plannings- en uitvoeringsaspecten van het Azure Data Factory-toepassingsmodel.</span><span class="sxs-lookup"><span data-stu-id="6e609-351">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="6e609-352">Pijplijnen bewaken en beheren met de app voor bewaking en beheer</span><span class="sxs-lookup"><span data-stu-id="6e609-352">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="6e609-353">Dit artikel wordt beschreven hoe toomonitor, beheren en fouten opsporen in pijplijnen met behulp van Hallo voor bewaking en beheer-App.</span><span class="sxs-lookup"><span data-stu-id="6e609-353">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
