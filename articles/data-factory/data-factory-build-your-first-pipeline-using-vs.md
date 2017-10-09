---
title: aaaBuild uw eerste gegevensfactory (Visual Studio) | Microsoft Docs
description: In deze zelfstudie maakt u een Azure Data Factory-voorbeeldpijplijn met behulp van Visual Studio.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7398c0c9-7a03-4628-94b3-f2aaef4a72c5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 0c5eb01b685d978d80916da0293cc2d3701b2d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a><span data-ttu-id="407a6-103">Zelfstudie: Een data factory maken met behulp van Visual Studio</span><span class="sxs-lookup"><span data-stu-id="407a6-103">Tutorial: Create a data factory by using Visual Studio</span></span>
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [<span data-ttu-id="407a6-104">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="407a6-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="407a6-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="407a6-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="407a6-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="407a6-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="407a6-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="407a6-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="407a6-108">Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="407a6-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="407a6-109">REST API</span><span class="sxs-lookup"><span data-stu-id="407a6-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)

<span data-ttu-id="407a6-110">Deze zelfstudie leert u hoe toocreate een Azure data factory met behulp van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="407a6-110">This tutorial shows you how toocreate an Azure data factory by using Visual Studio.</span></span> <span data-ttu-id="407a6-111">U een Visual Studio-project met behulp van de Data Factory-projectsjabloon Hallo maken, het definiëren van Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) in JSON-indeling en vervolgens publiceren/implementeren deze entiteiten toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="407a6-111">You create a Visual Studio project using hello Data Factory project template, define Data Factory entities (linked services, datasets, and pipeline) in JSON format, and then publish/deploy these entities toohello cloud.</span></span> 

<span data-ttu-id="407a6-112">Hallo-pijplijn in deze zelfstudie is één activiteit: **HDInsight Hive-activiteit**.</span><span class="sxs-lookup"><span data-stu-id="407a6-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="407a6-113">Deze activiteit wordt een hive-script uitgevoerd op een Azure HDInsight-cluster dat transformaties invoergegevens gegevens tooproduce uitvoer.</span><span class="sxs-lookup"><span data-stu-id="407a6-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="407a6-114">Hallo pijplijn is geplande toorun wanneer een maand tussen Hallo begin- en eindtijden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="407a6-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="407a6-115">In deze zelfstudie wordt niet getoond hoe u gegevens met Azure Data Factory kopieert.</span><span class="sxs-lookup"><span data-stu-id="407a6-115">This tutorial does not show how copy data by using Azure Data Factory.</span></span> <span data-ttu-id="407a6-116">Voor een zelfstudie over het toocopy van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: gegevens kopiëren van Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="407a6-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="407a6-117">Een pijplijn kan meer dan één activiteit hebben.</span><span class="sxs-lookup"><span data-stu-id="407a6-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="407a6-118">En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="407a6-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="407a6-119">Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="407a6-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="walkthrough-create-and-publish-data-factory-entities"></a><span data-ttu-id="407a6-120">Walkthrough: Data Factory-entiteiten maken en publiceren</span><span class="sxs-lookup"><span data-stu-id="407a6-120">Walkthrough: Create and publish Data Factory entities</span></span>
<span data-ttu-id="407a6-121">Hier volgen Hallo stappen die u als onderdeel van dit scenario uitvoert:</span><span class="sxs-lookup"><span data-stu-id="407a6-121">Here are hello steps you perform as part of this walkthrough:</span></span>

1. <span data-ttu-id="407a6-122">Maak twee gekoppelde services: **AzureStorageLinkedService1** en **HDInsightOnDemandLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="407a6-122">Create two linked services: **AzureStorageLinkedService1** and **HDInsightOnDemandLinkedService1**.</span></span> 
   
    <span data-ttu-id="407a6-123">In deze zelfstudie Hallo invoer-en uitvoergegevens voor hive-activiteit Hallo zijn dezelfde Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="407a6-123">In this tutorial, both input and output data for hello hive activity are in hello same Azure Blob Storage.</span></span> <span data-ttu-id="407a6-124">U gebruikt een bellen op HDInsight-cluster tooprocess bestaande invoergegevens tooproduce uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="407a6-124">You use an on-demand HDInsight cluster tooprocess existing input data tooproduce output data.</span></span> <span data-ttu-id="407a6-125">Hallo bellen op HDInsight-cluster wordt automatisch voor u gemaakt door Azure Data Factory tijdens het uitvoeren als de invoergegevens Hallo gereed toobe verwerkt is.</span><span class="sxs-lookup"><span data-stu-id="407a6-125">hello on-demand HDInsight cluster is automatically created for you by Azure Data Factory at run time when hello input data is ready toobe processed.</span></span> <span data-ttu-id="407a6-126">U moet toolink uw gegevens opslaat of tooyour gegevensfactory berekent zodat Hallo Data Factory-service verbinding van toothem tijdens runtime maken kan.</span><span class="sxs-lookup"><span data-stu-id="407a6-126">You need toolink your data stores or computes tooyour data factory so that hello Data Factory service can connect toothem at runtime.</span></span> <span data-ttu-id="407a6-127">Daarom moet u koppelen van uw Azure Storage-Account toohello data factory via Hallo AzureStorageLinkedService1 en koppelen van een HDInsight-cluster op aanvraag via Hallo HDInsightOnDemandLinkedService1.</span><span class="sxs-lookup"><span data-stu-id="407a6-127">Therefore, you link your Azure Storage Account toohello data factory by using hello AzureStorageLinkedService1, and link an on-demand HDInsight cluster by using hello HDInsightOnDemandLinkedService1.</span></span> <span data-ttu-id="407a6-128">Wanneer u publiceert, geeft u Hallo-naam voor Hallo data factory toobe gemaakt of een bestaande gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="407a6-128">When publishing, you specify hello name for hello data factory toobe created or an existing data factory.</span></span>  
2. <span data-ttu-id="407a6-129">Twee gegevenssets maken: **InputDataset** en **OutputDataset**, die staan voor Hallo invoer-en uitvoergegevens die zijn opgeslagen in hello Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="407a6-129">Create two datasets: **InputDataset** and **OutputDataset**, which represent hello input/output data that is stored in hello Azure blob storage.</span></span> 
   
    <span data-ttu-id="407a6-130">Deze gegevensset definities Raadpleeg toohello u hebt gemaakt in de vorige stap Hallo gekoppelde Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="407a6-130">These dataset definitions refer toohello Azure Storage linked service you created in hello previous step.</span></span> <span data-ttu-id="407a6-131">Voor Hallo InputDataset, geef Hallo blob-container (adfgetstarted) en map (inptutdata) met een blob met de invoergegevens Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="407a6-131">For hello InputDataset, you specify hello blob container (adfgetstarted) and hello folder (inptutdata) that contains a blob with hello input data.</span></span> <span data-ttu-id="407a6-132">U Hallo blob-container (adfgetstarted) opgeven voor Hallo OutputDataset, en Hallo-map (partitioneddata) die uitvoergegevens Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="407a6-132">For hello OutputDataset, you specify hello blob container (adfgetstarted) and hello folder (partitioneddata) that holds hello output data.</span></span> <span data-ttu-id="407a6-133">U geeft ook andere eigenschappen op, zoals de structuur, de beschikbaarheid en het beleid.</span><span class="sxs-lookup"><span data-stu-id="407a6-133">You also specify other properties such as structure, availability, and policy.</span></span>
3. <span data-ttu-id="407a6-134">Maak een pijplijn met de naam **MyFirstPipeline**.</span><span class="sxs-lookup"><span data-stu-id="407a6-134">Create a pipeline named **MyFirstPipeline**.</span></span> 
  
    <span data-ttu-id="407a6-135">In dit overzicht Hallo pipeline heeft slechts één activiteit: **HDInsight Hive-activiteit**.</span><span class="sxs-lookup"><span data-stu-id="407a6-135">In this walkthrough, hello pipeline has only one activity: **HDInsight Hive Activity**.</span></span> <span data-ttu-id="407a6-136">Deze activiteit transformatie invoergegevens tooproduce uitvoergegevens door een hive-script uitgevoerd op een HDInsight-cluster op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="407a6-136">This activity transform input data tooproduce output data by running a hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="407a6-137">Zie toolearn meer informatie over het hive-activiteit [Hive-activiteit](data-factory-hive-activity.md)</span><span class="sxs-lookup"><span data-stu-id="407a6-137">toolearn more about hive activity, see [Hive Activity](data-factory-hive-activity.md)</span></span> 
4. <span data-ttu-id="407a6-138">Maak een data factory met de naam **DataFactoryUsingVS**.</span><span class="sxs-lookup"><span data-stu-id="407a6-138">Create a data factory named **DataFactoryUsingVS**.</span></span> <span data-ttu-id="407a6-139">Hallo gegevensfactory en alle Data Factory-entiteiten (gekoppelde services, tabellen en pijplijn Hallo) implementeren.</span><span class="sxs-lookup"><span data-stu-id="407a6-139">Deploy hello data factory and all Data Factory entities (linked services, tables, and hello pipeline).</span></span>
5. <span data-ttu-id="407a6-140">Nadat u publiceert, gebruikt u Azure portal-blades en beheer-App voor bewaking en toomonitor Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="407a6-140">After you publish, you use Azure portal blades and Monitoring & Management App toomonitor hello pipeline.</span></span> 
  
### <a name="prerequisites"></a><span data-ttu-id="407a6-141">Vereisten</span><span class="sxs-lookup"><span data-stu-id="407a6-141">Prerequisites</span></span>
1. <span data-ttu-id="407a6-142">Lees [overzicht van de zelfstudie](data-factory-build-your-first-pipeline.md) artikel en volledige Hallo **vereiste** stappen.</span><span class="sxs-lookup"><span data-stu-id="407a6-142">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span> <span data-ttu-id="407a6-143">U kunt ook selecteren Hallo **overzicht en vereisten** optie in de keuzelijst Hallo op Hallo bovenste tooswitch toohello artikel.</span><span class="sxs-lookup"><span data-stu-id="407a6-143">You can also select hello **Overview and prerequisites** option in hello drop-down list at hello top tooswitch toohello article.</span></span> <span data-ttu-id="407a6-144">Nadat u Hallo vereisten hebt voltooid, schakelen back toothis artikel door te selecteren **Visual Studio** optie in de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="407a6-144">After you complete hello prerequisites, switch back toothis article by selecting **Visual Studio** option in hello drop-down list.</span></span>
2. <span data-ttu-id="407a6-145">toocreate Data Factory-exemplaren, moet u lid zijn van Hallo [Data Factory Inzender](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol op het niveau van de Hallo abonnement/resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="407a6-145">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>  
3. <span data-ttu-id="407a6-146">Hallo volgende op uw computer geïnstalleerd, moet u hebben:</span><span class="sxs-lookup"><span data-stu-id="407a6-146">You must have hello following installed on your computer:</span></span>
   * <span data-ttu-id="407a6-147">Visual Studio 2013 of Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="407a6-147">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="407a6-148">Download de Azure SDK voor Visual Studio 2013 of Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="407a6-148">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="407a6-149">Navigeer te[Azure-downloadpagina](https://azure.microsoft.com/downloads/) en klik op **VS 2013** of **VS 2015** in Hallo **.NET** sectie.</span><span class="sxs-lookup"><span data-stu-id="407a6-149">Navigate too[Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in hello **.NET** section.</span></span>
   * <span data-ttu-id="407a6-150">Download de nieuwste Azure Data Factory-invoegtoepassing Hallo voor Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) of [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="407a6-150">Download hello latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="407a6-151">U kunt ook Hallo invoegtoepassing Hallo volgende stappen uit als volgt bijwerken: op het menu Hallo **extra** -> **uitbreidingen en Updates** -> **Online**  ->  **Visual Studio-galerie** -> **Microsoft Azure Data Factory-hulpprogramma's voor Visual Studio** -> **Update**.</span><span class="sxs-lookup"><span data-stu-id="407a6-151">You can also update hello plugin by doing hello following steps: On hello menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

<span data-ttu-id="407a6-152">Nu gaan we toocreate Visual Studio een Azure data factory gebruiken.</span><span class="sxs-lookup"><span data-stu-id="407a6-152">Now, let's use Visual Studio toocreate an Azure data factory.</span></span>

### <a name="create-visual-studio-project"></a><span data-ttu-id="407a6-153">Een Visual Studio-project maken</span><span class="sxs-lookup"><span data-stu-id="407a6-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="407a6-154">Open **Visual Studio 2013** of **Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="407a6-154">Launch **Visual Studio 2013** or **Visual Studio 2015**.</span></span> <span data-ttu-id="407a6-155">Klik op **bestand**, wijst u te**nieuw**, en klik op **Project**.</span><span class="sxs-lookup"><span data-stu-id="407a6-155">Click **File**, point too**New**, and click **Project**.</span></span> <span data-ttu-id="407a6-156">U ziet Hallo **nieuw Project** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="407a6-156">You should see hello **New Project** dialog box.</span></span>  
2. <span data-ttu-id="407a6-157">In Hallo **nieuw Project** dialoogvenster, selecteer Hallo **DataFactory** sjabloon en klikt u op **Empty Data Factory Project**.</span><span class="sxs-lookup"><span data-stu-id="407a6-157">In hello **New Project** dialog, select hello **DataFactory** template, and click **Empty Data Factory Project**.</span></span>   

    ![Het dialoogvenster New Project](./media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. <span data-ttu-id="407a6-159">Voer een **naam** voor Hallo-project **locatie**, en een naam voor Hallo **oplossing**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="407a6-159">Enter a **name** for hello project, **location**, and a name for hello **solution**, and click **OK**.</span></span>

    ![Solution Explorer](./media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a><span data-ttu-id="407a6-161">Gekoppelde services maken</span><span class="sxs-lookup"><span data-stu-id="407a6-161">Create linked services</span></span>
<span data-ttu-id="407a6-162">In deze stap maakt u twee gekoppelde services: **Azure Storage** en **HDInsight op aanvraag**.</span><span class="sxs-lookup"><span data-stu-id="407a6-162">In this step, you create two linked services: **Azure Storage** and **HDInsight on-demand**.</span></span> 

<span data-ttu-id="407a6-163">Hello Azure Storage gekoppelde service uw Azure Storage-account toohello data factory door Hallo verbindingsinformatie te verstrekken.</span><span class="sxs-lookup"><span data-stu-id="407a6-163">hello Azure Storage linked service links your Azure Storage account toohello data factory by providing hello connection information.</span></span> <span data-ttu-id="407a6-164">Data Factory-service gebruikt de verbindingsreeks Hallo van Hallo gekoppelde service-instelling tooconnect toohello Azure storage tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="407a6-164">Data Factory service uses hello connection string from hello linked service setting tooconnect toohello Azure storage at runtime.</span></span> <span data-ttu-id="407a6-165">Deze opslag invoer bevat en uitvoergegevens voor Hallo pijplijn en Hallo hive-scriptbestand gebruikt door Hallo hive-activiteit.</span><span class="sxs-lookup"><span data-stu-id="407a6-165">This storage holds input and output data for hello pipeline, and hello hive script file used by hello hive activity.</span></span> 

<span data-ttu-id="407a6-166">Met de gekoppelde HDInsight-service op aanvraag, wordt Hallo HDInsight-cluster automatisch gemaakt tijdens runtime wanneer Hallo invoergegevens tooprocessed gereed is.</span><span class="sxs-lookup"><span data-stu-id="407a6-166">With on-demand HDInsight linked service, hello HDInsight cluster is automatically created at runtime when hello input data is ready tooprocessed.</span></span> <span data-ttu-id="407a6-167">Hallo-cluster wordt verwijderd nadat het verwerken is voltooid en niet-actieve Hallo opgegeven tijdsduur.</span><span class="sxs-lookup"><span data-stu-id="407a6-167">hello cluster is deleted after it is done processing and idle for hello specified amount of time.</span></span> 

> [!NOTE]
> <span data-ttu-id="407a6-168">U kunt een gegevensfactory maken door op te geven van de naam en instellingen op Hallo moment van publicatie van uw Data Factory-oplossing.</span><span class="sxs-lookup"><span data-stu-id="407a6-168">You create a data factory by specifying its name and settings at hello time of publishing your Data Factory solution.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="407a6-169">Een gekoppelde Azure Storage-service maken</span><span class="sxs-lookup"><span data-stu-id="407a6-169">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="407a6-170">Met de rechtermuisknop op **gekoppelde Services** in solution explorer Hallo punt te**toevoegen**, en klik op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="407a6-170">Right-click **Linked Services** in hello solution explorer, point too**Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="407a6-171">In Hallo **Add New Item** dialoogvenster, **Azure Storage Linked Service** in Hallo lijst en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="407a6-171">In hello **Add New Item** dialog box, select **Azure Storage Linked Service** from hello list, and click **Add**.</span></span>
    <span data-ttu-id="407a6-172">![Gekoppelde Azure Storage-service](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="407a6-172">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span></span>
3. <span data-ttu-id="407a6-173">Vervang `<accountname>` en `<accountkey>` met Hallo-naam van uw Azure storage-account en de bijbehorende sleutel.</span><span class="sxs-lookup"><span data-stu-id="407a6-173">Replace `<accountname>` and `<accountkey>` with hello name of your Azure storage account and its key.</span></span> <span data-ttu-id="407a6-174">toolearn hoe tooget uw opslag heeft toegang tot sleutel, raadpleegt u Hallo informatie over hoe tooview, kopiëren en opnieuw genereren opslag toegangstoetsen in [uw opslagaccount beheren](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="407a6-174">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
    <span data-ttu-id="407a6-175">![Gekoppelde Azure Storage-service](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="407a6-175">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span></span>
4. <span data-ttu-id="407a6-176">Hallo opslaan **AzureStorageLinkedService1.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="407a6-176">Save hello **AzureStorageLinkedService1.json** file.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="407a6-177">Een gekoppelde HDInsight-service maken</span><span class="sxs-lookup"><span data-stu-id="407a6-177">Create Azure HDInsight linked service</span></span>
1. <span data-ttu-id="407a6-178">In Hallo **Solution Explorer**, met de rechtermuisknop op **gekoppelde Services**, wijst u te**toevoegen**, en klik op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="407a6-178">In hello **Solution Explorer**, right-click **Linked Services**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="407a6-179">Selecteer **HDInsight On Demand Linked Service** en klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="407a6-179">Select **HDInsight On Demand Linked Service**, and click **Add**.</span></span>
3. <span data-ttu-id="407a6-180">Vervang Hallo **JSON** Hello JSON te volgen:</span><span class="sxs-lookup"><span data-stu-id="407a6-180">Replace hello **JSON** with hello following JSON:</span></span>

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
                "linkedServiceName": "AzureStorageLinkedService1"
            }
        }
    }
    ```

    <span data-ttu-id="407a6-181">Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:</span><span class="sxs-lookup"><span data-stu-id="407a6-181">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    <span data-ttu-id="407a6-182">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="407a6-182">Property</span></span> | <span data-ttu-id="407a6-183">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="407a6-183">Description</span></span>
    -------- | ----------- 
    <span data-ttu-id="407a6-184">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="407a6-184">ClusterSize</span></span> | <span data-ttu-id="407a6-185">Hiermee wordt de grootte Hallo Hallo HDInsight Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="407a6-185">Specifies hello size of hello HDInsight Hadoop cluster.</span></span>
    <span data-ttu-id="407a6-186">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="407a6-186">TimeToLive</span></span> | <span data-ttu-id="407a6-187">Hiermee geeft u op dat niet-actieve tijd Hallo voor Hallo HDInsight-cluster, voordat deze wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="407a6-187">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span>
    <span data-ttu-id="407a6-188">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="407a6-188">linkedServiceName</span></span> | <span data-ttu-id="407a6-189">Hiermee geeft u Hallo storage-account dat is gebruikt toostore Hallo logboeken die worden gegenereerd door HDInsight Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="407a6-189">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight Hadoop cluster.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="407a6-190">Hallo HDInsight-cluster maakt een **standaardcontainer** in Hallo-blobopslag die u hebt opgegeven in Hallo JSON (linkedServiceName).</span><span class="sxs-lookup"><span data-stu-id="407a6-190">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (linkedServiceName).</span></span> <span data-ttu-id="407a6-191">HDInsight verwijdert deze container niet wanneer Hallo-cluster is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="407a6-191">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="407a6-192">Dit gedrag is standaard.</span><span class="sxs-lookup"><span data-stu-id="407a6-192">This behavior is by design.</span></span> <span data-ttu-id="407a6-193">Met de gekoppelde service HDInsight op aanvraag wordt er steeds een HDInsight-cluster gemaakt wanneer er een segment wordt verwerkt, tenzij er een bestaand livecluster is (timeToLive).</span><span class="sxs-lookup"><span data-stu-id="407a6-193">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span></span> <span data-ttu-id="407a6-194">Hallo-cluster wordt automatisch verwijderd als het Hallo-verwerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="407a6-194">hello cluster is automatically deleted when hello processing is done.</span></span>
    > 
    > <span data-ttu-id="407a6-195">Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="407a6-195">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="407a6-196">Als u niet ze hoeft voor het oplossen van problemen met taken hello, kunt u toodelete ze tooreduce Hallo opslag kosten.</span><span class="sxs-lookup"><span data-stu-id="407a6-196">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="407a6-197">Hallo-namen van deze containers een patroon volgen: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="407a6-197">hello names of these containers follow a pattern: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`.</span></span> <span data-ttu-id="407a6-198">Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) toodelete containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="407a6-198">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

    <span data-ttu-id="407a6-199">Zie de [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Gekoppelde Compute Services) voor meer informatie over JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="407a6-199">For more information about JSON properties, see [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article.</span></span> 
4. <span data-ttu-id="407a6-200">Hallo opslaan **HDInsightOnDemandLinkedService1.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="407a6-200">Save hello **HDInsightOnDemandLinkedService1.json** file.</span></span>

### <a name="create-datasets"></a><span data-ttu-id="407a6-201">Gegevenssets maken</span><span class="sxs-lookup"><span data-stu-id="407a6-201">Create datasets</span></span>
<span data-ttu-id="407a6-202">In deze stap maakt u gegevenssets toorepresent Hallo invoer maken en uitvoergegevens voor Hive-verwerking.</span><span class="sxs-lookup"><span data-stu-id="407a6-202">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="407a6-203">Deze gegevenssets verwijzen toohello **AzureStorageLinkedService1** u eerder in deze zelfstudie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="407a6-203">These datasets refer toohello **AzureStorageLinkedService1** you have created earlier in this tutorial.</span></span> <span data-ttu-id="407a6-204">Hallo gekoppelde service verwijst tooan Azure Storage-account en gegevenssets vindt u container, map en bestandsnaam in Hallo opslag van de invoer- en uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="407a6-204">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>   

#### <a name="create-input-dataset"></a><span data-ttu-id="407a6-205">Invoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="407a6-205">Create input dataset</span></span>
1. <span data-ttu-id="407a6-206">In Hallo **Solution Explorer**, met de rechtermuisknop op **tabellen**, wijst u te**toevoegen**, en klik op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="407a6-206">In hello **Solution Explorer**, right-click **Tables**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="407a6-207">Selecteer **Azure Blob** in Hallo-lijst, wijzig Hallo-naam van Hallo-bestand te**InputDataSet.json**, en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="407a6-207">Select **Azure Blob** from hello list, change hello name of hello file too**InputDataSet.json**, and click **Add**.</span></span>
3. <span data-ttu-id="407a6-208">Vervang Hallo **JSON** in Hallo-editor met Hallo volgende JSON-fragment:</span><span class="sxs-lookup"><span data-stu-id="407a6-208">Replace hello **JSON** in hello editor with hello following JSON snippet:</span></span>

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    <span data-ttu-id="407a6-209">Deze JSON-fragment een gegevensset met de naam definieert **AzureBlobInput** die staat voor invoergegevens van hive-activiteit in de pijplijn Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="407a6-209">This JSON snippet defines a dataset called **AzureBlobInput** that represents input data for hello hive activity in hello pipeline.</span></span> <span data-ttu-id="407a6-210">U opgeven dat Hallo invoergegevens in de blob-container Hallo aangeroepen bevinden zich `adfgetstarted` en Hallo map met de naam `inputdata`.</span><span class="sxs-lookup"><span data-stu-id="407a6-210">You specify that hello input data is located in hello blob container called `adfgetstarted` and hello folder called `inputdata`.</span></span>

    <span data-ttu-id="407a6-211">Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:</span><span class="sxs-lookup"><span data-stu-id="407a6-211">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    <span data-ttu-id="407a6-212">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="407a6-212">Property</span></span> | <span data-ttu-id="407a6-213">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="407a6-213">Description</span></span> |
    -------- | ----------- |
    <span data-ttu-id="407a6-214">type</span><span class="sxs-lookup"><span data-stu-id="407a6-214">type</span></span> |<span data-ttu-id="407a6-215">Hallo type wordt ingesteld te**AzureBlob** omdat de gegevens zich in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="407a6-215">hello type property is set too**AzureBlob** because data resides in Azure Blob Storage.</span></span>
    <span data-ttu-id="407a6-216">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="407a6-216">linkedServiceName</span></span> | <span data-ttu-id="407a6-217">Verwijst toohello AzureStorageLinkedService1 die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="407a6-217">Refers toohello AzureStorageLinkedService1 you created earlier.</span></span>
    <span data-ttu-id="407a6-218">fileName</span><span class="sxs-lookup"><span data-stu-id="407a6-218">fileName</span></span> |<span data-ttu-id="407a6-219">Deze eigenschap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="407a6-219">This property is optional.</span></span> <span data-ttu-id="407a6-220">Als u deze eigenschap niet opgeeft, worden alle Hallo-bestanden uit folderPath Hallo opgenomen.</span><span class="sxs-lookup"><span data-stu-id="407a6-220">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="407a6-221">In dit geval wordt alleen Hallo input.log verwerkt.</span><span class="sxs-lookup"><span data-stu-id="407a6-221">In this case, only hello input.log is processed.</span></span>
    <span data-ttu-id="407a6-222">type</span><span class="sxs-lookup"><span data-stu-id="407a6-222">type</span></span> | <span data-ttu-id="407a6-223">Hallo-logboekbestanden zijn tekstbestanden, zodat we TextFormat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="407a6-223">hello log files are in text format, so we use TextFormat.</span></span> |
    <span data-ttu-id="407a6-224">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="407a6-224">columnDelimiter</span></span> | <span data-ttu-id="407a6-225">kolommen in Hallo logboekbestanden worden gescheiden door een kommateken hello (`,`)</span><span class="sxs-lookup"><span data-stu-id="407a6-225">columns in hello log files are delimited by hello comma character (`,`)</span></span>
    <span data-ttu-id="407a6-226">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="407a6-226">frequency/interval</span></span> | <span data-ttu-id="407a6-227">frequentie tooMonth ingesteld en interval is 1, wat betekent dat Hallo invoersegmenten één keer per maand beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="407a6-227">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span>
    <span data-ttu-id="407a6-228">external</span><span class="sxs-lookup"><span data-stu-id="407a6-228">external</span></span> | <span data-ttu-id="407a6-229">Deze eigenschap is tootrue ingesteld als invoergegevens voor activiteit Hallo Hallo niet worden gegenereerd door Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="407a6-229">This property is set tootrue if hello input data for hello activity is not generated by hello pipeline.</span></span> <span data-ttu-id="407a6-230">Deze eigenschap wordt alleen opgegeven voor invoergegevenssets.</span><span class="sxs-lookup"><span data-stu-id="407a6-230">This property is only specified on input datasets.</span></span> <span data-ttu-id="407a6-231">Voor invoergegevensset Hallo van de eerste activiteit Hallo altijd ingesteld dat deze tootrue.</span><span class="sxs-lookup"><span data-stu-id="407a6-231">For hello input dataset of hello first activity, always set it tootrue.</span></span>
4. <span data-ttu-id="407a6-232">Hallo opslaan **InputDataset.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="407a6-232">Save hello **InputDataset.json** file.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="407a6-233">Uitvoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="407a6-233">Create output dataset</span></span>
<span data-ttu-id="407a6-234">U maakt nu Hallo gegevensset toorepresent uitvoer uitvoergegevens opgeslagen in hello Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="407a6-234">Now, you create hello output dataset toorepresent output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="407a6-235">In Hallo **Solution Explorer**, met de rechtermuisknop op **tabellen**, wijst u te**toevoegen**, en klik op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="407a6-235">In hello **Solution Explorer**, right-click **tables**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="407a6-236">Selecteer **Azure Blob** in Hallo-lijst, wijzig Hallo-naam van Hallo-bestand te**OutputDataset.json**, en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="407a6-236">Select **Azure Blob** from hello list, change hello name of hello file too**OutputDataset.json**, and click **Add**.</span></span>
3. <span data-ttu-id="407a6-237">Vervang Hallo **JSON** in Hallo-editor met Hallo JSON te volgen:</span><span class="sxs-lookup"><span data-stu-id="407a6-237">Replace hello **JSON** in hello editor with hello following JSON:</span></span>
    
    ```json
    {
        "name": "AzureBlobOutput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    <span data-ttu-id="407a6-238">Hallo JSON-fragment een gegevensset met de naam definieert **AzureBlobOutput** dat vertegenwoordigt uitvoergegevens die wordt geproduceerd door Hallo hive-activiteit in Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="407a6-238">hello JSON snippet defines a dataset called **AzureBlobOutput** that represents output data produced by hello hive activity in hello pipeline.</span></span> <span data-ttu-id="407a6-239">U opgeven dat gegevens wordt geproduceerd door de hive-activiteit Hallo Hallo-uitvoer wordt geplaatst in blob-container Hallo aangeroepen `adfgetstarted` en Hallo map met de naam `partitioneddata`.</span><span class="sxs-lookup"><span data-stu-id="407a6-239">You specify that hello output data is produced by hello hive activity is placed in hello blob container called `adfgetstarted` and hello folder called `partitioneddata`.</span></span> 
    
    <span data-ttu-id="407a6-240">Hallo **beschikbaarheid** sectie geeft die Hallo-uitvoergegevensset op maandelijkse basis wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="407a6-240">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span> <span data-ttu-id="407a6-241">Hallo uitvoer gegevensset stations Hallo planning van Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="407a6-241">hello output dataset drives hello schedule of hello pipeline.</span></span> <span data-ttu-id="407a6-242">Hallo-pijplijn wordt uitgevoerd tussen de begin- en eindtijden per maand.</span><span class="sxs-lookup"><span data-stu-id="407a6-242">hello pipeline runs monthly between its start and end times.</span></span> 

    <span data-ttu-id="407a6-243">Zie **hello invoergegevensset maken** sectie voor beschrijvingen van deze eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="407a6-243">See **Create hello input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="407a6-244">U instelt geen Hallo externe eigenschap op een uitvoergegevensset omdat Hallo gegevensset wordt geproduceerd door Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="407a6-244">You do not set hello external property on an output dataset as hello dataset is produced by hello pipeline.</span></span>
4. <span data-ttu-id="407a6-245">Hallo opslaan **OutputDataset.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="407a6-245">Save hello **OutputDataset.json** file.</span></span>

### <a name="create-pipeline"></a><span data-ttu-id="407a6-246">Pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="407a6-246">Create pipeline</span></span>
<span data-ttu-id="407a6-247">U hebt gemaakt Hallo gekoppelde Azure Storage-service en invoer- en uitvoergegevenssets tot nu toe.</span><span class="sxs-lookup"><span data-stu-id="407a6-247">You have created hello Azure Storage linked service, and input and output datasets so far.</span></span> <span data-ttu-id="407a6-248">Nu gaat u een pijplijn met een **HDInsightHive**-activiteit maken.</span><span class="sxs-lookup"><span data-stu-id="407a6-248">Now, you create a pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="407a6-249">Hallo **invoer** voor Hallo hive activiteit te ingesteld**AzureBlobInput** en **uitvoer** te is ingesteld,**AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="407a6-249">hello **input** for hello hive activity is set too**AzureBlobInput** and **output** is set too**AzureBlobOutput**.</span></span> <span data-ttu-id="407a6-250">Een segment van een invoergegevensset maandelijks beschikbaar is (frequency: Month, interval: 1), en Hallo uitvoer segment wordt maandelijks geproduceerd te.</span><span class="sxs-lookup"><span data-stu-id="407a6-250">A slice of an input dataset is available monthly (frequency: Month, interval: 1), and hello output slice is produced monthly too.</span></span> 

1. <span data-ttu-id="407a6-251">In Hallo **Solution Explorer**, met de rechtermuisknop op **pijplijnen**, wijst u te**toevoegen**, en klik op **Nieuw Item.**</span><span class="sxs-lookup"><span data-stu-id="407a6-251">In hello **Solution Explorer**, right-click **Pipelines**, point too**Add**, and click **New Item.**</span></span>
2. <span data-ttu-id="407a6-252">Selecteer **Hive Transformation Pipeline** in Hallo lijst en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="407a6-252">Select **Hive Transformation Pipeline** from hello list, and click **Add**.</span></span>
3. <span data-ttu-id="407a6-253">Vervang Hallo **JSON** Hello codefragment te volgen:</span><span class="sxs-lookup"><span data-stu-id="407a6-253">Replace hello **JSON** with hello following snippet:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="407a6-254">Vervang `<storageaccountname>` met Hallo-naam van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="407a6-254">Replace `<storageaccountname>` with hello name of your storage account.</span></span>

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
                        "scriptLinkedService": "AzureStorageLinkedService1",
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
            "start": "2016-04-01T00:00:00Z",
            "end": "2016-04-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="407a6-255">Vervang `<storageaccountname>` met Hallo-naam van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="407a6-255">Replace `<storageaccountname>` with hello name of your storage account.</span></span>

    <span data-ttu-id="407a6-256">Hallo JSON-codefragment definieert een pijplijn die uit een enkele activiteit (Hive-activiteit bestaat).</span><span class="sxs-lookup"><span data-stu-id="407a6-256">hello JSON snippet defines a pipeline that consists of a single activity (Hive Activity).</span></span> <span data-ttu-id="407a6-257">Deze activiteit wordt uitgevoerd op een invoergegevens van Hive-script tooprocess een bellen op HDInsight-cluster tooproduce uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="407a6-257">This activity runs a Hive script tooprocess input data on an on-demand HDInsight cluster tooproduce output data.</span></span> <span data-ttu-id="407a6-258">In Hallo gedeelte van de activiteiten van Hallo pijplijn JSON, ziet u slechts één activiteit in Hallo matrix met soort te**HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="407a6-258">In hello activities section of hello pipeline JSON, you see only one activity in hello array with type set too**HDInsightHive**.</span></span> 

    <span data-ttu-id="407a6-259">In de eigenschappen van type Hallo die specifieke tooHDInsight Hive-activiteit, kunt u opgeven welke gekoppelde Azure Storage-service heeft Hallo hive-scriptbestand, Hallo pad toohello scriptbestand en parameters toohello scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="407a6-259">In hello type properties that are specific tooHDInsight Hive activity, you specify what Azure Storage linked service has hello hive script file, hello path toohello script file, and parameters toohello script file.</span></span> 

    <span data-ttu-id="407a6-260">Hallo Hive-scriptbestand **partitionweblogs.hql**, wordt opgeslagen in hello Azure-opslagaccount (opgegeven door de scriptLinkedService Hallo) en in Hallo `script` map in container Hallo `adfgetstarted`.</span><span class="sxs-lookup"><span data-stu-id="407a6-260">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService), and in hello `script` folder in hello container `adfgetstarted`.</span></span>

    <span data-ttu-id="407a6-261">Hallo `defines` sectie is gebruikte toospecify Hallo runtime-instellingen die toohello hive-script worden doorgegeven als Hive-configuratiewaarden (bijvoorbeeld `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.</span><span class="sxs-lookup"><span data-stu-id="407a6-261">hello `defines` section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.</span></span>

    <span data-ttu-id="407a6-262">Hallo **start** en **end** eigenschappen van de pijplijn Hallo geeft Hallo actieve periode van Hallo-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="407a6-262">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span> <span data-ttu-id="407a6-263">U hebt geconfigureerd Hallo gegevensset toobe geproduceerd maandelijks, daarom alleen wanneer het segment wordt geproduceerd door de pijplijn hello (omdat Hallo maand hetzelfde in de begin- en einddatums).</span><span class="sxs-lookup"><span data-stu-id="407a6-263">You configured hello dataset toobe produced monthly, therefore, only once slice is produced by hello pipeline (because hello month is same in start and end dates).</span></span>

    <span data-ttu-id="407a6-264">In Hallo activiteits-JSON geeft u opgeven dat Hallo Hive-script wordt uitgevoerd op Hallo berekening die is opgegeven door Hallo **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="407a6-264">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>
4. <span data-ttu-id="407a6-265">Hallo opslaan **HiveActivity1.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="407a6-265">Save hello **HiveActivity1.json** file.</span></span>

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a><span data-ttu-id="407a6-266">partitionweblogs.hql en input.log toevoegen als afhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="407a6-266">Add partitionweblogs.hql and input.log as a dependency</span></span>
1. <span data-ttu-id="407a6-267">Met de rechtermuisknop op **afhankelijkheden** in Hallo **Solution Explorer** venster te verwijzen**toevoegen**, en klik op **bestaand Item**.</span><span class="sxs-lookup"><span data-stu-id="407a6-267">Right-click **Dependencies** in hello **Solution Explorer** window, point too**Add**, and click **Existing Item**.</span></span>  
2. <span data-ttu-id="407a6-268">Navigeer toohello **C:\ADFGettingStarted** en selecteer **partitionweblogs.hql**, **input.log** bestanden en klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="407a6-268">Navigate toohello **C:\ADFGettingStarted** and select **partitionweblogs.hql**, **input.log** files, and click **Add**.</span></span> <span data-ttu-id="407a6-269">U hebt deze twee bestanden gemaakt als onderdeel van de vereisten van Hallo [overzicht van de zelfstudie](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="407a6-269">You created these two files as part of prerequisites from hello [Tutorial Overview](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="407a6-270">Wanneer u Hallo oplossing in de volgende stap hello publiceert, Hallo **partitionweblogs.hql** bestand is geüpload toohello **script** map in Hallo `adfgetstarted` blob-container.</span><span class="sxs-lookup"><span data-stu-id="407a6-270">When you publish hello solution in hello next step, hello **partitionweblogs.hql** file is uploaded toohello **script** folder in hello `adfgetstarted` blob container.</span></span>   

### <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="407a6-271">Data Factory-entiteiten publiceren/implementeren</span><span class="sxs-lookup"><span data-stu-id="407a6-271">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="407a6-272">In deze stap maakt publiceren u Hallo Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) in uw project toohello Azure Data Factory-service.</span><span class="sxs-lookup"><span data-stu-id="407a6-272">In this step, you publish hello Data Factory entities (linked services, datasets, and pipeline) in your project toohello Azure Data Factory service.</span></span> <span data-ttu-id="407a6-273">In Hallo proces van publiceren, moet u Hallo-naam van uw gegevensfactory opgeven.</span><span class="sxs-lookup"><span data-stu-id="407a6-273">In hello process of publishing, you specify hello name for your data factory.</span></span> 

1. <span data-ttu-id="407a6-274">Met de rechtermuisknop op het project in Solution Explorer Hallo en klik op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="407a6-274">Right-click project in hello Solution Explorer, and click **Publish**.</span></span>
2. <span data-ttu-id="407a6-275">Als u ziet **tooyour Microsoft-account aanmelden** in het dialoogvenster Geef uw referenties voor het Hallo-account met Azure-abonnement en klikt u op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="407a6-275">If you see **Sign in tooyour Microsoft account** dialog box, enter your credentials for hello account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="407a6-276">U ziet Hallo in het dialoogvenster te volgen:</span><span class="sxs-lookup"><span data-stu-id="407a6-276">You should see hello following dialog box:</span></span>

   ![Het dialoogvenster Publish](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. <span data-ttu-id="407a6-278">In Hallo **Configure data factory** pagina, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="407a6-278">In hello **Configure data factory** page, do hello following steps:</span></span>

    ![Publiceren - Nieuwe data factory-instellingen](media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. <span data-ttu-id="407a6-280">Selecteer **Create New Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="407a6-280">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="407a6-281">Voer een unieke **naam** voor Hallo data factory.</span><span class="sxs-lookup"><span data-stu-id="407a6-281">Enter a unique **name** for hello data factory.</span></span> <span data-ttu-id="407a6-282">Bijvoorbeeld: **DataFactoryUsingVS09152016**.</span><span class="sxs-lookup"><span data-stu-id="407a6-282">For example: **DataFactoryUsingVS09152016**.</span></span> <span data-ttu-id="407a6-283">Hallo-naam moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="407a6-283">hello name must be globally unique.</span></span>
   3. <span data-ttu-id="407a6-284">Selecteer de juiste abonnement Hallo voor Hallo **abonnement** veld.</span><span class="sxs-lookup"><span data-stu-id="407a6-284">Select hello right subscription for hello **Subscription** field.</span></span> 
        > [!IMPORTANT]
        > <span data-ttu-id="407a6-285">Als u een abonnement niet ziet, zorg ervoor dat u aangemeld met een account dat een beheerder of co-beheerder van het Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="407a6-285">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of hello subscription.</span></span>
   4. <span data-ttu-id="407a6-286">Selecteer Hallo **resourcegroep** voor Hallo data factory toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="407a6-286">Select hello **resource group** for hello data factory toobe created.</span></span>
   5. <span data-ttu-id="407a6-287">Selecteer Hallo **regio** voor Hallo data factory.</span><span class="sxs-lookup"><span data-stu-id="407a6-287">Select hello **region** for hello data factory.</span></span>
   6. <span data-ttu-id="407a6-288">Klik op **volgende** tooswitch toohello **Publish Items** pagina.</span><span class="sxs-lookup"><span data-stu-id="407a6-288">Click **Next** tooswitch toohello **Publish Items** page.</span></span> <span data-ttu-id="407a6-289">(Druk op **tabblad** toomove buiten Hallo naam veld tooif hello **volgende** knop is uitgeschakeld.)</span><span class="sxs-lookup"><span data-stu-id="407a6-289">(Press **TAB** toomove out of hello Name field tooif hello **Next** button is disabled.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="407a6-290">Als u de foutmelding Hallo **Data factory-naam 'DataFactoryUsingVS' is niet beschikbaar** tijdens het publiceren Hallo-naam (bijvoorbeeld yournameDataFactoryUsingVS) wijzigen.</span><span class="sxs-lookup"><span data-stu-id="407a6-290">If you receive hello error **Data factory name “DataFactoryUsingVS” is not available** when publishing, change hello name (for example, yournameDataFactoryUsingVS).</span></span> <span data-ttu-id="407a6-291">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="407a6-291">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
1. <span data-ttu-id="407a6-292">In Hallo **Publish Items** pagina, zorg ervoor dat alle Data Factory-entiteiten zijn geselecteerd en klik op Hallo **volgende** tooswitch toohello **samenvatting** pagina.</span><span class="sxs-lookup"><span data-stu-id="407a6-292">In hello **Publish Items** page, ensure that all hello Data Factories entities are selected, and click **Next** tooswitch toohello **Summary** page.</span></span>

    ![Pagina Items publiceren](media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. <span data-ttu-id="407a6-294">Controleer Hallo samenvatting en klik op **volgende** toostart Hallo implementatie proces en bekijkt hello **Implementatiestatus**.</span><span class="sxs-lookup"><span data-stu-id="407a6-294">Review hello summary and click **Next** toostart hello deployment process and view hello **Deployment Status**.</span></span>

    ![Overzichtspagina](media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. <span data-ttu-id="407a6-296">In Hallo **Implementatiestatus** pagina ziet u Hallo status van implementatieproces Hallo.</span><span class="sxs-lookup"><span data-stu-id="407a6-296">In hello **Deployment Status** page, you should see hello status of hello deployment process.</span></span> <span data-ttu-id="407a6-297">Klik op Voltooien nadat het Hallo-implementatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="407a6-297">Click Finish after hello deployment is done.</span></span>

<span data-ttu-id="407a6-298">Belangrijke punten toonote:</span><span class="sxs-lookup"><span data-stu-id="407a6-298">Important points toonote:</span></span>

- <span data-ttu-id="407a6-299">Als u de foutmelding Hallo: **dit abonnement is niet geregistreerd toouse namespace Microsoft.DataFactory**, voer een van de volgende Hallo en probeer opnieuw te publiceren:</span><span class="sxs-lookup"><span data-stu-id="407a6-299">If you receive hello error: **This subscription is not registered toouse namespace Microsoft.DataFactory**, do one of hello following and try publishing again:</span></span>
    - <span data-ttu-id="407a6-300">Voer in Azure PowerShell Hallo opdracht tooregister Hallo Data Factory-provider te volgen.</span><span class="sxs-lookup"><span data-stu-id="407a6-300">In Azure PowerShell, run hello following command tooregister hello Data Factory provider.</span></span>
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        <span data-ttu-id="407a6-301">Die Hallo Data Factory-provider is geregistreerd, kunt u na de opdracht tooconfirm Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="407a6-301">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span>

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - <span data-ttu-id="407a6-302">Aanmelding via het Azure-abonnement in toohello Hallo [Azure-portal](https://portal.azure.com) en navigeer tooa Data Factory-blade of maak een gegevensfactory in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="407a6-302">Login using hello Azure subscription in toohello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="407a6-303">Deze actie automatisch Hallo provider voor u geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="407a6-303">This action automatically registers hello provider for you.</span></span>
- <span data-ttu-id="407a6-304">Hallo-naam van de gegevensfactory Hallo kan worden geregistreerd als DNS-naam in toekomstige Hallo en daarmee ook voor iedereen zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="407a6-304">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>
- <span data-ttu-id="407a6-305">toocreate Data Factory-exemplaren, moet u een beheerder toobe of co-beheerder van hello Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="407a6-305">toocreate Data Factory instances, you need toobe an admin or co-admin of hello Azure subscription</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="407a6-306">De pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="407a6-306">Monitor pipeline</span></span>
<span data-ttu-id="407a6-307">In deze stap maakt bewaken u Hallo pijplijn diagramweergave van Hallo gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="407a6-307">In this step, you monitor hello pipeline using Diagram View of hello data factory.</span></span> 

#### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="407a6-308">De pijplijn bewaken met Diagramweergave</span><span class="sxs-lookup"><span data-stu-id="407a6-308">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="407a6-309">Meld u bij toohello [Azure-portal](https://portal.azure.com/), Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="407a6-309">Log in toohello [Azure portal](https://portal.azure.com/), do hello following steps:</span></span>
   1. <span data-ttu-id="407a6-310">Klik op **Meer services** en op **Gegevensfactory's**.</span><span class="sxs-lookup"><span data-stu-id="407a6-310">Click **More services** and click **Data factories**.</span></span>
       
        ![Door gegevensfactory’s bladeren](./media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. <span data-ttu-id="407a6-312">Selecteer Hallo-naam van uw gegevensfactory (bijvoorbeeld: **DataFactoryUsingVS09152016**) uit de lijst Hallo van data Factory.</span><span class="sxs-lookup"><span data-stu-id="407a6-312">Select hello name of your data factory (for example: **DataFactoryUsingVS09152016**) from hello list of data factories.</span></span>
   
       ![Uw gegevensfactory selecteren](./media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. <span data-ttu-id="407a6-314">In de startpagina van uw gegevensfactory hello, klikt u op **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="407a6-314">In hello home page for your data factory, click **Diagram**.</span></span>

    ![Tegel Diagram](./media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. <span data-ttu-id="407a6-316">In de diagramweergave hello ziet u een overzicht van Hallo pijplijnen en gegevenssets die in deze zelfstudie worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="407a6-316">In hello Diagram View, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![Diagramweergave](./media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. <span data-ttu-id="407a6-318">tooview alle activiteiten in de pijplijn voor hello, klik met de rechtermuisknop pijplijn in Hallo diagram en klikt u op pijplijn openen.</span><span class="sxs-lookup"><span data-stu-id="407a6-318">tooview all activities in hello pipeline, right-click pipeline in hello diagram and click Open Pipeline.</span></span>

    ![Menu Pijplijn openen](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. <span data-ttu-id="407a6-320">Controleer of u Hallo HDInsightHive-activiteit in Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="407a6-320">Confirm that you see hello HDInsightHive activity in hello pipeline.</span></span>

    ![Pijplijnweergave openen](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    <span data-ttu-id="407a6-322">back-toonavigate toohello vorige weergave, klikt u op **Data factory** in Hallo breadcrumb menu Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="407a6-322">toonavigate back toohello previous view, click **Data factory** in hello breadcrumb menu at hello top.</span></span>
6. <span data-ttu-id="407a6-323">In Hallo **diagramweergave**, dubbelklikt u op Hallo gegevensset **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="407a6-323">In hello **Diagram View**, double-click hello dataset **AzureBlobInput**.</span></span> <span data-ttu-id="407a6-324">Bevestig dat segment Hallo **gereed** status.</span><span class="sxs-lookup"><span data-stu-id="407a6-324">Confirm that hello slice is in **Ready** state.</span></span> <span data-ttu-id="407a6-325">Het kan enkele minuten voor Hallo segment tooshow duren status Ready heeft.</span><span class="sxs-lookup"><span data-stu-id="407a6-325">It may take a couple of minutes for hello slice tooshow up in Ready state.</span></span> <span data-ttu-id="407a6-326">Als deze niet is gebeurd nadat u enige tijd wacht, bekijken of er Hallo invoerbestand (input.log in de juiste container Hallo geplaatst) (`adfgetstarted`) en de map (`inputdata`).</span><span class="sxs-lookup"><span data-stu-id="407a6-326">If it does not happen after you wait for sometime, see if you have hello input file (input.log) placed in hello right container (`adfgetstarted`) and folder (`inputdata`).</span></span> <span data-ttu-id="407a6-327">En zorg ervoor dat Hallo **externe** eigenschap op Hallo invoergegevensset is ingesteld, te**true**.</span><span class="sxs-lookup"><span data-stu-id="407a6-327">And, make sure that hello **external** property on hello input dataset is set too**true**.</span></span> 

   ![Invoersegment met de status Gereed](./media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. <span data-ttu-id="407a6-329">Klik op **X** tooclose **AzureBlobInput** blade.</span><span class="sxs-lookup"><span data-stu-id="407a6-329">Click **X** tooclose **AzureBlobInput** blade.</span></span>
8. <span data-ttu-id="407a6-330">In Hallo **diagramweergave**, dubbelklikt u op Hallo gegevensset **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="407a6-330">In hello **Diagram View**, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="407a6-331">U ziet dat Hallo-segment dat momenteel wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="407a6-331">You see that hello slice that is currently being processed.</span></span>

   ![Gegevensset](./media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. <span data-ttu-id="407a6-333">Wanneer het verwerken is voltooid, ziet u Hallo segment **gereed** status.</span><span class="sxs-lookup"><span data-stu-id="407a6-333">When processing is done, you see hello slice in **Ready** state.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="407a6-334">Het maken van een on-demand HDInsight-cluster duurt normaal gesproken enige tijd (ongeveer 20 minuten).</span><span class="sxs-lookup"><span data-stu-id="407a6-334">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="407a6-335">Daarom verwachten Hallo pijplijn tootake **ongeveer 30 minuten** tooprocess Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="407a6-335">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>  
   
    ![Gegevensset](./media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. <span data-ttu-id="407a6-337">Wanneer Hallo segment is in **gereed** staat, controleert u Hallo `partitioneddata` map in Hallo `adfgetstarted` container in uw blobopslag voor Hallo uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="407a6-337">When hello slice is in **Ready** state, check hello `partitioneddata` folder in hello `adfgetstarted` container in your blob storage for hello output data.</span></span>  

    ![Uitvoergegevens](./media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. <span data-ttu-id="407a6-339">Klik op Hallo segment toosee details over deze in een **gegevenssegment** blade.</span><span class="sxs-lookup"><span data-stu-id="407a6-339">Click hello slice toosee details about it in a **Data slice** blade.</span></span>

    ![Details gegevenssegment](./media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. <span data-ttu-id="407a6-341">Klik op een activiteit die wordt uitgevoerd in Hallo **activiteit wordt uitgevoerd lijst** toosee details over een activiteit (Hive-activiteit in ons scenario) uitgevoerd in een **details uitvoering van activiteit** venster.</span><span class="sxs-lookup"><span data-stu-id="407a6-341">Click an activity run in hello **Activity runs list** toosee details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span> 
  
    ![Details uitvoering van activiteit](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    <span data-ttu-id="407a6-343">Uit Hallo-logboekbestanden ziet u Hallo Hive-query die is uitgevoerd en statusinformatie.</span><span class="sxs-lookup"><span data-stu-id="407a6-343">From hello log files, you can see hello Hive query that was executed and status information.</span></span> <span data-ttu-id="407a6-344">Deze logboeken komen van pas bij het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="407a6-344">These logs are useful for troubleshooting any issues.</span></span>  

<span data-ttu-id="407a6-345">Zie [gegevenssets en pijplijn bewaken](data-factory-monitor-manage-pipelines.md) voor instructies over hoe toouse hello Azure portal toomonitor Hallo pijplijn en gegevenssets u hebt gemaakt in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="407a6-345">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how toouse hello Azure portal toomonitor hello pipeline and datasets you have created in this tutorial.</span></span>

#### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="407a6-346">De pijplijn bewaken met de app Bewaking en beheer</span><span class="sxs-lookup"><span data-stu-id="407a6-346">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="407a6-347">U kunt ook controleren en beheren van toepassing toomonitor uw pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="407a6-347">You can also use Monitor & Manage application toomonitor your pipelines.</span></span> <span data-ttu-id="407a6-348">Zie [Azure Data Factory-pijplijnen bewaken en beheren met de app voor bewaking en beheer](data-factory-monitor-manage-app.md) voor meer informatie over het gebruik van deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="407a6-348">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="407a6-349">Klik op de tegel Bewaking en beheer.</span><span class="sxs-lookup"><span data-stu-id="407a6-349">Click Monitor & Manage tile.</span></span>

    ![De tegel Bewaking en beheer](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. <span data-ttu-id="407a6-351">De toepassing Bewaking en beheer wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="407a6-351">You should see Monitor & Manage application.</span></span> <span data-ttu-id="407a6-352">Wijziging Hallo **begintijd** en **eindtijd** toomatch start (01-04-2016 12:00 A.M.)- en eindtijden (04-02-2016 12:00 uur) van uw pijplijn en klik op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="407a6-352">Change hello **Start time** and **End time** toomatch start (04-01-2016 12:00 AM) and end times (04-02-2016 12:00 AM) of your pipeline, and click **Apply**.</span></span>

    ![De app Bewaking en beheer](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. <span data-ttu-id="407a6-354">toosee details over een activiteitvenster selecteren in Hallo **Activiteitsvensters lijst** toosee details over deze.</span><span class="sxs-lookup"><span data-stu-id="407a6-354">toosee details about an activity window, select it in hello **Activity Windows list** toosee details about it.</span></span>
    <span data-ttu-id="407a6-355">![Details van activiteitsvenster](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span><span class="sxs-lookup"><span data-stu-id="407a6-355">![Activity window details](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="407a6-356">Hallo-invoerbestand wordt verwijderd zodra het Hallo-segment is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="407a6-356">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="407a6-357">Dus als u toorerun Hallo segment wilt of zelfstudie opnieuw hello, uploadt Hallo invoerbestand (input.log) toohello `inputdata` map Hallo `adfgetstarted` container.</span><span class="sxs-lookup"><span data-stu-id="407a6-357">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello `inputdata` folder of hello `adfgetstarted` container.</span></span>

### <a name="additional-notes"></a><span data-ttu-id="407a6-358">Aanvullende opmerkingen</span><span class="sxs-lookup"><span data-stu-id="407a6-358">Additional notes</span></span>
- <span data-ttu-id="407a6-359">Een gegevensfactory kan één of meer pijplijnen hebben.</span><span class="sxs-lookup"><span data-stu-id="407a6-359">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="407a6-360">Een pijplijn kan één of meer activiteiten bevatten.</span><span class="sxs-lookup"><span data-stu-id="407a6-360">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="407a6-361">Bijvoorbeeld invoergegevens een Kopieeractiviteit toocopy-gegevens van een doelgegevensopslagplaats tooa bron en het toorun in een HDInsight Hive-activiteit een Hive-script tootransform.</span><span class="sxs-lookup"><span data-stu-id="407a6-361">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data.</span></span> <span data-ttu-id="407a6-362">Zie [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor alle bronnen en put wordt ondersteund door Hallo Kopieeractiviteit Hallo.</span><span class="sxs-lookup"><span data-stu-id="407a6-362">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all hello sources and sinks supported by hello Copy Activity.</span></span> <span data-ttu-id="407a6-363">Zie [gekoppelde services berekenen](data-factory-compute-linked-services.md) voor Hallo overzicht van de compute-services die door Data Factory worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="407a6-363">See [compute linked services](data-factory-compute-linked-services.md) for hello list of compute services supported by Data Factory.</span></span>
- <span data-ttu-id="407a6-364">Gekoppelde services worden gegevensarchieven of compute-services tooan Azure-gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="407a6-364">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="407a6-365">Zie [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor alle bronnen en put wordt ondersteund door Hallo Kopieeractiviteit Hallo.</span><span class="sxs-lookup"><span data-stu-id="407a6-365">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all hello sources and sinks supported by hello Copy Activity.</span></span> <span data-ttu-id="407a6-366">Zie [gekoppelde services berekenen](data-factory-compute-linked-services.md) voor Hallo overzicht van de compute-services die door Data Factory worden ondersteund en [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) die erop kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="407a6-366">See [compute linked services](data-factory-compute-linked-services.md) for hello list of compute services supported by Data Factory and [transformation activities](data-factory-data-transformation-activities.md) that can run on them.</span></span>
- <span data-ttu-id="407a6-367">Zie [verplaatsen van gegevens uit / tooAzure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) voor meer informatie over de JSON-eigenschappen die in Hallo gekoppelde Azure Storage-servicedefinitie.</span><span class="sxs-lookup"><span data-stu-id="407a6-367">See [Move data from/tooAzure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used in hello Azure Storage linked service definition.</span></span>
- <span data-ttu-id="407a6-368">U kunt uw eigen HDInsight-cluster gebruiken in plaats van een on-demand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="407a6-368">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="407a6-369">Zie [Gekoppelde services berekenen](data-factory-compute-linked-services.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="407a6-369">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>
-  <span data-ttu-id="407a6-370">Hallo Data Factory maakt een **op basis van Linux** HDInsight-cluster voor u Hello voorafgaand aan JSON.</span><span class="sxs-lookup"><span data-stu-id="407a6-370">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello preceding JSON.</span></span> <span data-ttu-id="407a6-371">Zie [Gekoppelde on-demand HDInsight-service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="407a6-371">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
- <span data-ttu-id="407a6-372">Hallo HDInsight-cluster maakt een **standaardcontainer** in Hallo-blobopslag die u hebt opgegeven in Hallo JSON (linkedServiceName).</span><span class="sxs-lookup"><span data-stu-id="407a6-372">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (linkedServiceName).</span></span> <span data-ttu-id="407a6-373">HDInsight verwijdert deze container niet wanneer Hallo-cluster is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="407a6-373">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="407a6-374">Dit gedrag is standaard.</span><span class="sxs-lookup"><span data-stu-id="407a6-374">This behavior is by design.</span></span> <span data-ttu-id="407a6-375">Met de gekoppelde service HDInsight op aanvraag wordt er steeds een HDInsight-cluster gemaakt wanneer er een segment wordt verwerkt, tenzij er een bestaand livecluster is (timeToLive).</span><span class="sxs-lookup"><span data-stu-id="407a6-375">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span></span> <span data-ttu-id="407a6-376">Hallo-cluster wordt automatisch verwijderd als het Hallo-verwerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="407a6-376">hello cluster is automatically deleted when hello processing is done.</span></span>
    
    <span data-ttu-id="407a6-377">Naarmate er meer segmenten worden verwerkt, verschijnen er meer containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="407a6-377">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="407a6-378">Als u niet ze hoeft voor het oplossen van problemen met taken hello, kunt u toodelete ze tooreduce Hallo opslag kosten.</span><span class="sxs-lookup"><span data-stu-id="407a6-378">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="407a6-379">Hallo-namen van deze containers een patroon volgen: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="407a6-379">hello names of these containers follow a pattern: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span></span> <span data-ttu-id="407a6-380">Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) toodelete containers in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="407a6-380">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>
- <span data-ttu-id="407a6-381">Uitvoergegevensset is momenteel welke stations Hallo planning, dus u een uitvoergegevensset maken moet, zelfs als Hallo activiteit geen uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="407a6-381">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="407a6-382">Als Hallo activiteit geen invoer neemt, kunt u maken Hallo invoergegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="407a6-382">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> 
- <span data-ttu-id="407a6-383">In deze zelfstudie wordt niet getoond hoe u gegevens met Azure Data Factory kopieert.</span><span class="sxs-lookup"><span data-stu-id="407a6-383">This tutorial does not show how copy data by using Azure Data Factory.</span></span> <span data-ttu-id="407a6-384">Voor een zelfstudie over het toocopy van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: gegevens kopiëren van Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="407a6-384">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>


## <a name="use-server-explorer-tooview-data-factories"></a><span data-ttu-id="407a6-385">Server Explorer tooview data Factory gebruiken</span><span class="sxs-lookup"><span data-stu-id="407a6-385">Use Server Explorer tooview data factories</span></span>
1. <span data-ttu-id="407a6-386">In **Visual Studio**, klikt u op **weergave** op Hallo van menu en klik op **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="407a6-386">In **Visual Studio**, click **View** on hello menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="407a6-387">Vouw in Server Explorer-venster Hallo **Azure** en vouw **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="407a6-387">In hello Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="407a6-388">Als u ziet **tooVisual Studio aanmelden**, Voer Hallo **account** die zijn gekoppeld aan uw Azure-abonnement en klik op **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="407a6-388">If you see **Sign in tooVisual Studio**, enter hello **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="407a6-389">Voer het **wachtwoord** in en klik op **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="407a6-389">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="407a6-390">Visual Studio haalt tooget informatie over alle Azure data factory's in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="407a6-390">Visual Studio tries tooget information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="407a6-391">Hallo-status van deze bewerking in Hallo weergegeven **Data Factory Task List** venster.</span><span class="sxs-lookup"><span data-stu-id="407a6-391">You see hello status of this operation in hello **Data Factory Task List** window.</span></span>

    ![Server Explorer](./media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. <span data-ttu-id="407a6-393">U kunt met de rechtermuisknop op een gegevensfactory en selecteer **tooNew Export Data Factory Project** toocreate een Visual Studio-project op basis van een bestaande gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="407a6-393">You can right-click a data factory, and select **Export Data Factory tooNew Project** toocreate a Visual Studio project based on an existing data factory.</span></span>

    ![Een gegevensfactory exporteren](./media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="407a6-395">Data Factory-hulpprogramma's voor Visual Studio bijwerken</span><span class="sxs-lookup"><span data-stu-id="407a6-395">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="407a6-396">tooupdate Azure Data Factory-hulpprogramma's voor Visual Studio Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="407a6-396">tooupdate Azure Data Factory tools for Visual Studio, do hello following steps:</span></span>

1. <span data-ttu-id="407a6-397">Klik op **extra** op Hallo menu en selecteer **uitbreidingen en Updates**.</span><span class="sxs-lookup"><span data-stu-id="407a6-397">Click **Tools** on hello menu and select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="407a6-398">Selecteer **Updates** in Hallo linkerdeelvenster en selecteer vervolgens **Visual Studio-galerie**.</span><span class="sxs-lookup"><span data-stu-id="407a6-398">Select **Updates** in hello left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="407a6-399">Selecteer **Azure Data Factory-hulpprogramma's voor Visual Studio** en klik op **Bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="407a6-399">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="407a6-400">Als u deze vermelding niet ziet, hebt u al de meest recente versie Hallo Hallo-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="407a6-400">If you do not see this entry, you already have hello latest version of hello tools.</span></span>

## <a name="use-configuration-files"></a><span data-ttu-id="407a6-401">Configuratiebestanden gebruiken</span><span class="sxs-lookup"><span data-stu-id="407a6-401">Use configuration files</span></span>
<span data-ttu-id="407a6-402">U kunt de configuratiebestanden in Visual Studio tooconfigure eigenschappen voor de gekoppelde services/tabellen/pijplijnen anders voor elke omgeving.</span><span class="sxs-lookup"><span data-stu-id="407a6-402">You can use configuration files in Visual Studio tooconfigure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="407a6-403">Houd rekening met Hallo volgende JSON-definitie voor een gekoppelde Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="407a6-403">Consider hello following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="407a6-404">toospecify **connectionString** met verschillende waarden voor accountname en accountkey op basis van het Hallo-omgeving (ontwikkeling/tests/productie) toowhich u Data Factory-entiteiten implementeert.</span><span class="sxs-lookup"><span data-stu-id="407a6-404">toospecify **connectionString** with different values for accountname and accountkey based on hello environment (Dev/Test/Production) toowhich you are deploying Data Factory entities.</span></span> <span data-ttu-id="407a6-405">U kunt dit gedrag bewerkstelligen door een afzonderlijk configuratiebestand te gebruiken voor elke omgeving.</span><span class="sxs-lookup"><span data-stu-id="407a6-405">You can achieve this behavior by using separate configuration file for each environment.</span></span>

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

### <a name="add-a-configuration-file"></a><span data-ttu-id="407a6-406">Een configuratiebestand toevoegen</span><span class="sxs-lookup"><span data-stu-id="407a6-406">Add a configuration file</span></span>
<span data-ttu-id="407a6-407">Voeg een configuratiebestand voor elke omgeving toe door Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="407a6-407">Add a configuration file for each environment by performing hello following steps:</span></span>   

1. <span data-ttu-id="407a6-408">Met de rechtermuisknop op Hallo Data Factory-project in Visual Studio-oplossing, wijst u te**toevoegen**, en klik op **nieuw item**.</span><span class="sxs-lookup"><span data-stu-id="407a6-408">Right-click hello Data Factory project in your Visual Studio solution, point too**Add**, and click **New item**.</span></span>
2. <span data-ttu-id="407a6-409">Selecteer **Config** Selecteer in de lijst met geïnstalleerde sjablonen aan de linkerkant Hallo Hallo **configuratiebestand**, voer een **naam** voor Hallo configuratie bestand en klik op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="407a6-409">Select **Config** from hello list of installed templates on hello left, select **Configuration File**, enter a **name** for hello configuration file, and click **Add**.</span></span>

    ![Een configuratiebestand toevoegen](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="407a6-411">Configuratieparameters en hun waarden in de volgende indeling Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="407a6-411">Add configuration parameters and their values in hello following format:</span></span>

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    <span data-ttu-id="407a6-412">In dit voorbeeld configureert u de eigenschap connectionString van een gekoppelde Azure Storage-service en een gekoppelde Azure SQL-service.</span><span class="sxs-lookup"><span data-stu-id="407a6-412">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="407a6-413">U ziet dat Hallo-syntaxis voor het opgeven van de naam is [JsonPath](http://goessner.net/articles/JsonPath/).</span><span class="sxs-lookup"><span data-stu-id="407a6-413">Notice that hello syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="407a6-414">Als JSON een eigenschap die een matrix met waarden heeft is zoals weergegeven in de volgende code Hallo:</span><span class="sxs-lookup"><span data-stu-id="407a6-414">If JSON has a property that has an array of values as shown in hello following code:</span></span>  

    ```json
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
    ```

    <span data-ttu-id="407a6-415">Eigenschappen configureren zoals wordt weergegeven in het Hallo-configuratiebestand (gebruik op nul gebaseerde indexering) te volgen:</span><span class="sxs-lookup"><span data-stu-id="407a6-415">Configure properties as shown in hello following configuration file (use zero-based indexing):</span></span>

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a><span data-ttu-id="407a6-416">Eigenschapnamen met spaties</span><span class="sxs-lookup"><span data-stu-id="407a6-416">Property names with spaces</span></span>
<span data-ttu-id="407a6-417">Als de naam van een eigenschap spaties bevat, gebruikt u vierkante haken, zoals in Hallo volgt (databaseservernaam):</span><span class="sxs-lookup"><span data-stu-id="407a6-417">If a property name has spaces in it, use square brackets as shown in hello following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="407a6-418">Een oplossing implementeren met behulp van een configuratie</span><span class="sxs-lookup"><span data-stu-id="407a6-418">Deploy solution using a configuration</span></span>
<span data-ttu-id="407a6-419">Wanneer u Azure Data Factory-entiteiten in de VS publiceert, kunt u Hallo configuratie dat u toouse voor die publicatiebewerking wilt opgeven.</span><span class="sxs-lookup"><span data-stu-id="407a6-419">When you are publishing Azure Data Factory entities in VS, you can specify hello configuration that you want toouse for that publishing operation.</span></span>

<span data-ttu-id="407a6-420">toopublish entiteiten in een configuratiebestand met Azure Data Factory-project:</span><span class="sxs-lookup"><span data-stu-id="407a6-420">toopublish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="407a6-421">Met de rechtermuisknop op de Data Factory-project en klik op **publiceren** toosee hello **Publish Items** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="407a6-421">Right-click Data Factory project and click **Publish** toosee hello **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="407a6-422">Selecteer een bestaande gegevensfactory of geef waarden voor het maken van een gegevensfactory op Hallo **Configure data factory** pagina en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="407a6-422">Select an existing data factory or specify values for creating a data factory on hello **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="407a6-423">Op Hallo **Publish Items** pagina: u ziet een vervolgkeuzelijst met beschikbare configuraties voor Hallo **Select Deployment Config** veld.</span><span class="sxs-lookup"><span data-stu-id="407a6-423">On hello **Publish Items** page: you see a drop-down list with available configurations for hello **Select Deployment Config** field.</span></span>

    ![Een configuratiebestand selecteren](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="407a6-425">Selecteer Hallo **configuratiebestand** dat u wilt, zoals toouse en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="407a6-425">Select hello **configuration file** that you would like toouse and click **Next**.</span></span>
5. <span data-ttu-id="407a6-426">Controleer of u Hallo-naam van de JSON-bestand in Hallo **samenvatting** pagina en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="407a6-426">Confirm that you see hello name of JSON file in hello **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="407a6-427">Klik op **voltooien** nadat Hallo implementatiebewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="407a6-427">Click **Finish** after hello deployment operation is finished.</span></span>

<span data-ttu-id="407a6-428">Wanneer u implementeert, zijn Hallo waarden uit het configuratiebestand Hallo gebruikte tooset waarden voor eigenschappen in de JSON-bestanden Hallo voordat Hallo entiteiten geïmplementeerde tooAzure Data Factory-service worden.</span><span class="sxs-lookup"><span data-stu-id="407a6-428">When you deploy, hello values from hello configuration file are used tooset values for properties in hello JSON files before hello entities are deployed tooAzure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="407a6-429">Azure Key Vault gebruiken</span><span class="sxs-lookup"><span data-stu-id="407a6-429">Use Azure Key Vault</span></span>
<span data-ttu-id="407a6-430">Het is niet aangeraden en vaak tegen beveiliging beleid toocommit gevoelige gegevens zoals verbinding tekenreeksen toohello code opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="407a6-430">It is not advisable and often against security policy toocommit sensitive data such as connection strings toohello code repository.</span></span> <span data-ttu-id="407a6-431">Zie [ADF Secure publiceren](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) voorbeeld op GitHub toolearn over gevoelige informatie op te slaan in Azure Sleutelkluis en dit gebruikt bij het publiceren van de Data Factory-entiteiten.</span><span class="sxs-lookup"><span data-stu-id="407a6-431">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub toolearn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="407a6-432">Hallo-extensie beveiligde publiceren voor Visual Studio kunt Hallo geheimen toobe opgeslagen in de Sleutelkluis en alleen verwijzingen toothem zijn opgegeven in de gekoppelde services / implementatieconfiguraties.</span><span class="sxs-lookup"><span data-stu-id="407a6-432">hello Secure Publish extension for Visual Studio allows hello secrets toobe stored in Key Vault and only references toothem are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="407a6-433">Deze verwijzingen zijn opgelost als u Data Factory-entiteiten tooAzure publiceren.</span><span class="sxs-lookup"><span data-stu-id="407a6-433">These references are resolved when you publish Data Factory entities tooAzure.</span></span> <span data-ttu-id="407a6-434">Deze bestanden kunnen vervolgens worden doorgevoerd toosource opslagplaats zonder dat geen geheimen.</span><span class="sxs-lookup"><span data-stu-id="407a6-434">These files can then be committed toosource repository without exposing any secrets.</span></span>

## <a name="summary"></a><span data-ttu-id="407a6-435">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="407a6-435">Summary</span></span>
<span data-ttu-id="407a6-436">In deze zelfstudie maakt u een Azure data factory tooprocess gegevens gemaakt door het Hive-script uitvoeren op een HDInsight hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="407a6-436">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="407a6-437">U hebt gebruikt Hallo Data Factory-Editor in hello Azure portal toodo Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="407a6-437">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>  

1. <span data-ttu-id="407a6-438">U hebt een Azure-**gegevensfactory** gemaakt.</span><span class="sxs-lookup"><span data-stu-id="407a6-438">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="407a6-439">U hebt twee **gekoppelde services** gemaakt:</span><span class="sxs-lookup"><span data-stu-id="407a6-439">Created two **linked services**:</span></span>
   1. <span data-ttu-id="407a6-440">**Azure Storage** gekoppelde service toolink uw Azure-blobopslag die invoer-/ uitvoerbestanden toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="407a6-440">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="407a6-441">**Azure HDInsight** op aanvraag gekoppelde service toolink een bellen op HDInsight Hadoop-cluster toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="407a6-441">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="407a6-442">Azure Data Factory maakt een HDInsight Hadoop-cluster just in time tooprocess invoergegevens en uitvoergegevens produceren.</span><span class="sxs-lookup"><span data-stu-id="407a6-442">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="407a6-443">Twee gemaakt **gegevenssets**, die invoer- en gegevens voor HDInsight Hive-activiteit in Hallo pijplijn worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="407a6-443">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="407a6-444">U hebt een **pijplijn** gemaakt met een **HDInsight Hive**-activiteit.</span><span class="sxs-lookup"><span data-stu-id="407a6-444">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="407a6-445">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="407a6-445">Next Steps</span></span>
<span data-ttu-id="407a6-446">In dit artikel hebt u een pijplijn gemaakt met een transformatieactiviteit (HDInsight-activiteit) waarvoor een Hive-script wordt uitgevoerd op een on-demand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="407a6-446">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="407a6-447">hoe de gegevens van een Kopieeractiviteit toocopy van een Azure Blob-tooAzure SQL, toouse zien toosee [zelfstudie: gegevens kopiëren van een Azure blob-tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="407a6-447">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="407a6-448">U kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="407a6-448">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="407a6-449">Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="407a6-449">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 


## <a name="see-also"></a><span data-ttu-id="407a6-450">Zie ook</span><span class="sxs-lookup"><span data-stu-id="407a6-450">See Also</span></span>
| <span data-ttu-id="407a6-451">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="407a6-451">Topic</span></span> | <span data-ttu-id="407a6-452">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="407a6-452">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="407a6-453">Pijplijnen</span><span class="sxs-lookup"><span data-stu-id="407a6-453">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="407a6-454">In dit artikel helpt u begrijpen pijplijnen en activiteiten in Azure Data Factory en hoe toouse ze tooconstruct gegevensgestuurde werkstromen voor uw scenario of bedrijf.</span><span class="sxs-lookup"><span data-stu-id="407a6-454">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="407a6-455">Gegevenssets</span><span class="sxs-lookup"><span data-stu-id="407a6-455">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="407a6-456">Op basis van dit artikel krijgt u inzicht in de gegevenssets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="407a6-456">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="407a6-457">Activiteiten voor gegevenstransformatie</span><span class="sxs-lookup"><span data-stu-id="407a6-457">Data Transformation Activities</span></span>](data-factory-data-transformation-activities.md) |<span data-ttu-id="407a6-458">Dit artikel bevat een lijst van activiteiten voor gegevenstransformatie (zoals de HDInsight Hive-transformatie die u in deze zelfstudie hebt gebruikt) die door Azure Data Factory worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="407a6-458">This article provides a list of data transformation activities (such as HDInsight Hive transformation you used in this tutorial) supported by Azure Data Factory.</span></span> |
| [<span data-ttu-id="407a6-459">Plannen en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="407a6-459">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="407a6-460">Dit artikel wordt uitgelegd Hallo plannings- en uitvoeringsaspecten van het Azure Data Factory-toepassingsmodel.</span><span class="sxs-lookup"><span data-stu-id="407a6-460">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="407a6-461">Pijplijnen bewaken en beheren met de app voor bewaking en beheer</span><span class="sxs-lookup"><span data-stu-id="407a6-461">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="407a6-462">Dit artikel wordt beschreven hoe toomonitor, beheren en fouten opsporen in pijplijnen met behulp van Hallo voor bewaking en beheer-App.</span><span class="sxs-lookup"><span data-stu-id="407a6-462">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
