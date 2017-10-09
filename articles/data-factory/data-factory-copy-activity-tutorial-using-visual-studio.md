---
title: 'Zelfstudie: een pijplijn maken met de kopieeractiviteit in Visual Studio | Microsoft Docs'
description: In deze zelfstudie maakt u een Azure Data Factory-pijplijn met een kopieeractiviteit. Hiervoor gebruikt u Visual Studio.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: d99d8875807bab41f5122ab95a09f83f82923529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a><span data-ttu-id="50d2b-103">Zelfstudie: een pijplijn maken met de kopieeractiviteit in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="50d2b-103">Tutorial: Create a pipeline with Copy Activity using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="50d2b-104">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="50d2b-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="50d2b-105">De wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="50d2b-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="50d2b-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="50d2b-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="50d2b-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="50d2b-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="50d2b-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="50d2b-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="50d2b-109">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="50d2b-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="50d2b-110">REST API</span><span class="sxs-lookup"><span data-stu-id="50d2b-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="50d2b-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="50d2b-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="50d2b-112">In dit artikel leert u hoe toouse Hallo toocreate Microsoft Visual Studio een gegevensfactory met een pijplijn waarmee gegevens worden gekopieerd van een Azure blob storage tooan Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="50d2b-112">In this article, you learn how toouse hello Microsoft Visual Studio toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="50d2b-113">Als u nieuwe tooAzure Data Factory, lees Hallo [inleiding tooAzure Data Factory](data-factory-introduction.md) artikel voordat u deze zelfstudie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="50d2b-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="50d2b-114">In deze zelfstudie maakt u een pijplijn met één activiteit erin: kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="50d2b-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="50d2b-115">Hallo kopieeractiviteit kopieert gegevens van een gegevensarchief voor ondersteunde gegevens store tooa ondersteunde sink.</span><span class="sxs-lookup"><span data-stu-id="50d2b-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="50d2b-116">Zie [Ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met gegevensarchieven die worden ondersteund als bron en als sink.</span><span class="sxs-lookup"><span data-stu-id="50d2b-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="50d2b-117">Hallo-activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens tussen verschillende gegevensarchieven op een manier veilig, betrouwbaar en schaalbaar kan worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="50d2b-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="50d2b-118">Zie voor meer informatie over Hallo Kopieeractiviteit [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="50d2b-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="50d2b-119">Een pijplijn kan meer dan één activiteit hebben.</span><span class="sxs-lookup"><span data-stu-id="50d2b-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="50d2b-120">En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="50d2b-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="50d2b-121">Zie [Meerdere activiteiten in een pijplijn](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="50d2b-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE] 
> <span data-ttu-id="50d2b-122">Hallo data pipeline in deze zelfstudie worden gegevens gekopieerd van een bron data store tooa doelgegevensopslagplaats.</span><span class="sxs-lookup"><span data-stu-id="50d2b-122">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="50d2b-123">Voor een zelfstudie over het tootransform van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: een pijplijn tootransform gegevens met Hadoop-cluster bouwen](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="50d2b-123">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50d2b-124">Vereisten</span><span class="sxs-lookup"><span data-stu-id="50d2b-124">Prerequisites</span></span>
1. <span data-ttu-id="50d2b-125">Lees [overzicht van de zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artikel en volledige Hallo **vereiste** stappen.</span><span class="sxs-lookup"><span data-stu-id="50d2b-125">Read through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article and complete hello **prerequisite** steps.</span></span>       
2. <span data-ttu-id="50d2b-126">toocreate Data Factory-exemplaren, moet u lid zijn van Hallo [Data Factory Inzender](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol op het niveau van de Hallo abonnement/resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="50d2b-126">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
3. <span data-ttu-id="50d2b-127">Hallo volgende op uw computer geïnstalleerd, moet u hebben:</span><span class="sxs-lookup"><span data-stu-id="50d2b-127">You must have hello following installed on your computer:</span></span> 
   * <span data-ttu-id="50d2b-128">Visual Studio 2013 of Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="50d2b-128">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="50d2b-129">Download de Azure SDK voor Visual Studio 2013 of Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="50d2b-129">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="50d2b-130">Navigeer te[Azure-downloadpagina](https://azure.microsoft.com/downloads/) en klik op **VS 2013** of **VS 2015** in Hallo **.NET** sectie.</span><span class="sxs-lookup"><span data-stu-id="50d2b-130">Navigate too[Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in hello **.NET** section.</span></span>
   * <span data-ttu-id="50d2b-131">Download de nieuwste Azure Data Factory-invoegtoepassing Hallo voor Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) of [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="50d2b-131">Download hello latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="50d2b-132">U kunt ook Hallo invoegtoepassing Hallo volgende stappen uit als volgt bijwerken: op het menu Hallo **extra** -> **uitbreidingen en Updates** -> **Online**  ->  **Visual Studio-galerie** -> **Microsoft Azure Data Factory-hulpprogramma's voor Visual Studio** -> **Update**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-132">You can also update hello plugin by doing hello following steps: On hello menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

## <a name="steps"></a><span data-ttu-id="50d2b-133">Stappen</span><span class="sxs-lookup"><span data-stu-id="50d2b-133">Steps</span></span>
<span data-ttu-id="50d2b-134">Hier volgen Hallo stappen die u als onderdeel van deze zelfstudie uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="50d2b-134">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="50d2b-135">Maak **gekoppelde services** in Hallo gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="50d2b-135">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="50d2b-136">In deze stap maakt u twee gekoppelde services van het type: Azure Storage en Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="50d2b-136">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="50d2b-137">Hallo AzureStorageLinkedService koppelt u uw Azure storage-account toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="50d2b-137">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="50d2b-138">U hebt gemaakt van een container en gegevens toothis opslagaccount geüpload als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="50d2b-138">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="50d2b-139">Azuresqllinkedservice wordt uw Azure SQL database toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="50d2b-139">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="50d2b-140">Hallo-gegevens die worden gekopieerd van de blob-opslag hello wordt opgeslagen in deze database.</span><span class="sxs-lookup"><span data-stu-id="50d2b-140">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="50d2b-141">Als onderdeel van de [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) hebt u een SQL-tabel in deze database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="50d2b-141">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>     
2. <span data-ttu-id="50d2b-142">Maken van de invoer en uitvoer **gegevenssets** in Hallo gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="50d2b-142">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="50d2b-143">Hallo gekoppelde Azure storage-service geeft Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op uitvoeringstijd tooconnect tooyour Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="50d2b-143">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="50d2b-144">En Hallo blob-invoerbron gegevensset geeft Hallo-container en Hallo-map met invoergegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="50d2b-144">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="50d2b-145">Op deze manier geeft hello Azure SQL Database gekoppeld service Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op de runtime tooconnect tooyour Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="50d2b-145">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="50d2b-146">En SQL Hallo-tabel uitvoergegevensset geeft Hallo-tabel in Hallo toowhich Hallo databasegegevens van Hallo blob-opslag is gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="50d2b-146">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
3. <span data-ttu-id="50d2b-147">Maak een **pijplijn** in Hallo gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="50d2b-147">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="50d2b-148">In deze stap maakt u een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="50d2b-148">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="50d2b-149">Hallo kopieeractiviteit kopieert gegevens van een blob in hello Azure blob storage tooa tabel in hello Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="50d2b-149">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="50d2b-150">U kunt een kopieeractiviteit gebruiken in een pijplijn toocopy gegevens van het doel van een ondersteunde bron-tooany ondersteund.</span><span class="sxs-lookup"><span data-stu-id="50d2b-150">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="50d2b-151">Zie het artikel [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met ondersteunde gegevensarchieven.</span><span class="sxs-lookup"><span data-stu-id="50d2b-151">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
4. <span data-ttu-id="50d2b-152">Maak een Azure-**gegevensfactory** tijdens het implementeren van de Data Factory-entiteiten (gekoppelde services, gegevenssets/tabellen en pijplijnen).</span><span class="sxs-lookup"><span data-stu-id="50d2b-152">Create an Azure **data factory** when deploying Data Factory entities (linked services, datasets/tables, and pipelines).</span></span> 

## <a name="create-visual-studio-project"></a><span data-ttu-id="50d2b-153">Een Visual Studio-project maken</span><span class="sxs-lookup"><span data-stu-id="50d2b-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="50d2b-154">Open **Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-154">Launch **Visual Studio 2015**.</span></span> <span data-ttu-id="50d2b-155">Klik op **bestand**, wijst u te**nieuw**, en klik op **Project**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-155">Click **File**, point too**New**, and click **Project**.</span></span> <span data-ttu-id="50d2b-156">U ziet Hallo **nieuw Project** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="50d2b-156">You should see hello **New Project** dialog box.</span></span>  
2. <span data-ttu-id="50d2b-157">In Hallo **nieuw Project** dialoogvenster, selecteer Hallo **DataFactory** sjabloon en klikt u op **Empty Data Factory Project**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-157">In hello **New Project** dialog, select hello **DataFactory** template, and click **Empty Data Factory Project**.</span></span>  
   
    ![Het dialoogvenster New Project](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. <span data-ttu-id="50d2b-159">Hallo-naam van het Hallo-project, de locatie voor de oplossing Hallo en naam van oplossing Hallo opgeven en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-159">Specify hello name of hello project, location for hello solution, and name of hello solution, and then click **OK**.</span></span>
   
    ![Solution Explorer](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a><span data-ttu-id="50d2b-161">Gekoppelde services maken</span><span class="sxs-lookup"><span data-stu-id="50d2b-161">Create linked services</span></span>
<span data-ttu-id="50d2b-162">U maken gekoppelde services in een data factory-toolink uw gegevens worden opgeslagen en compute services toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="50d2b-162">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="50d2b-163">In deze zelfstudie gebruikt u niet een willekeurige compute-service, zoals Azure HDInsight of Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="50d2b-163">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="50d2b-164">U gebruikt twee gegevensarchieven van het type Azure Storage (bron) en Azure SQL Database (doel).</span><span class="sxs-lookup"><span data-stu-id="50d2b-164">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="50d2b-165">Daarom maakt u twee gekoppelde services van het type: Azure Storage en AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="50d2b-165">Therefore, you create two linked services of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="50d2b-166">Hello Azure Storage gekoppelde service uw Azure storage-account toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="50d2b-166">hello Azure Storage linked service links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="50d2b-167">Dit opslagaccount wordt Hallo een waarop u container gemaakt en Hallo gegevens geüpload als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="50d2b-167">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="50d2b-168">Azure SQL gekoppelde service uw Azure SQL database toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="50d2b-168">Azure SQL linked service links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="50d2b-169">Hallo-gegevens die worden gekopieerd van de blob-opslag hello wordt opgeslagen in deze database.</span><span class="sxs-lookup"><span data-stu-id="50d2b-169">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="50d2b-170">Hallo emp-tabel in deze database wordt gemaakt als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="50d2b-170">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="50d2b-171">Gekoppelde services worden gegevensarchieven of compute-services tooan Azure-gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="50d2b-171">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="50d2b-172">Zie [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor alle bronnen en put wordt ondersteund door Hallo Kopieeractiviteit Hallo.</span><span class="sxs-lookup"><span data-stu-id="50d2b-172">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all hello sources and sinks supported by hello Copy Activity.</span></span> <span data-ttu-id="50d2b-173">Zie [gekoppelde services berekenen](data-factory-compute-linked-services.md) voor Hallo overzicht van de compute-services die door Data Factory worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="50d2b-173">See [compute linked services](data-factory-compute-linked-services.md) for hello list of compute services supported by Data Factory.</span></span> <span data-ttu-id="50d2b-174">In deze zelfstudie gebruikt u geen compute-service.</span><span class="sxs-lookup"><span data-stu-id="50d2b-174">In this tutorial, you do not use any compute service.</span></span> 

### <a name="create-hello-azure-storage-linked-service"></a><span data-ttu-id="50d2b-175">Hallo gekoppelde Azure Storage-service maken</span><span class="sxs-lookup"><span data-stu-id="50d2b-175">Create hello Azure Storage linked service</span></span>
1. <span data-ttu-id="50d2b-176">In **Solution Explorer**, met de rechtermuisknop op **gekoppelde Services**, wijst u te**toevoegen**, en klik op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-176">In **Solution Explorer**, right-click **Linked Services**, point too**Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="50d2b-177">In Hallo **Add New Item** dialoogvenster, **Azure Storage Linked Service** in Hallo lijst en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-177">In hello **Add New Item** dialog box, select **Azure Storage Linked Service** from hello list, and click **Add**.</span></span> 
   
    ![Nieuwe gekoppelde service](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. <span data-ttu-id="50d2b-179">Vervang `<accountname>` en `<accountkey>`* met Hallo-naam van uw Azure storage-account en de bijbehorende sleutel.</span><span class="sxs-lookup"><span data-stu-id="50d2b-179">Replace `<accountname>` and `<accountkey>`* with hello name of your Azure storage account and its key.</span></span> 
   
    ![Een gekoppelde Azure Storage-service](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. <span data-ttu-id="50d2b-181">Hallo opslaan **AzureStorageLinkedService1.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="50d2b-181">Save hello **AzureStorageLinkedService1.json** file.</span></span>

    <span data-ttu-id="50d2b-182">Zie voor meer informatie over de JSON-eigenschappen in de servicedefinitie Hallo gekoppeld [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="50d2b-182">For more information about JSON properties in hello linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-hello-azure-sql-linked-service"></a><span data-ttu-id="50d2b-183">Hello Azure SQL gekoppelde service maken</span><span class="sxs-lookup"><span data-stu-id="50d2b-183">Create hello Azure SQL linked service</span></span>
1. <span data-ttu-id="50d2b-184">Met de rechtermuisknop op **gekoppelde Services** knooppunt in Hallo **Solution Explorer** opnieuw in en wijst te**toevoegen**, en klik op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-184">Right-click on **Linked Services** node in hello **Solution Explorer** again, point too**Add**, and click **New Item**.</span></span> 
2. <span data-ttu-id="50d2b-185">Selecteer deze keer **Azure SQL Linked Service** en klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-185">This time, select **Azure SQL Linked Service**, and click **Add**.</span></span> 
3. <span data-ttu-id="50d2b-186">In Hallo **AzureSqlLinkedService1.json bestand**, Vervang `<servername>`, `<databasename>`, `<username@servername>`, en `<password>` met namen van uw Azure SQL-server, database-gebruikersaccount en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="50d2b-186">In hello **AzureSqlLinkedService1.json file**, replace `<servername>`, `<databasename>`, `<username@servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span>    
4. <span data-ttu-id="50d2b-187">Hallo opslaan **AzureSqlLinkedService1.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="50d2b-187">Save hello **AzureSqlLinkedService1.json** file.</span></span> 
    
    <span data-ttu-id="50d2b-188">Zie [Azure SQL Database-connector](data-factory-azure-sql-connector.md#linked-service-properties) voor meer informatie over deze JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="50d2b-188">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>


## <a name="create-datasets"></a><span data-ttu-id="50d2b-189">Gegevenssets maken</span><span class="sxs-lookup"><span data-stu-id="50d2b-189">Create datasets</span></span>
<span data-ttu-id="50d2b-190">In de vorige stap Hallo gemaakt gekoppelde services toolink uw Azure Storage-account en de Azure SQL database tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="50d2b-190">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="50d2b-191">In deze stap definieert u twee gegevenssets met de naam InputDataset en OutputDataset die vertegenwoordigen de invoer- en uitvoergegevens die zijn opgeslagen in Hallo gegevensarchieven waarnaar wordt verwezen door de AzureStorageLinkedService1 en AzureSqlLinkedService1 respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="50d2b-191">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService1 and AzureSqlLinkedService1 respectively.</span></span>

<span data-ttu-id="50d2b-192">Hallo gekoppelde Azure storage-service geeft Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op uitvoeringstijd tooconnect tooyour Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="50d2b-192">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="50d2b-193">En Hallo blob-invoerbron gegevensset (InputDataset) geeft Hallo-container en Hallo-map met invoergegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="50d2b-193">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="50d2b-194">Op deze manier geeft hello Azure SQL Database gekoppeld service Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op de runtime tooconnect tooyour Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="50d2b-194">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="50d2b-195">En Hallo uitvoer gegevensset met SQL-tabel (OututDataset) geeft Hallo tabel in Hallo database toowhich Hallo gegevens uit Hallo blob-opslag worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="50d2b-195">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="50d2b-196">Invoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="50d2b-196">Create input dataset</span></span>
<span data-ttu-id="50d2b-197">In deze stap maakt u een gegevensset met de naam InputDataset die tooa blob-bestand (emp.txt) verwijst in de hoofdmap Hallo van een blob-container (adftutorial) in hello Azure Storage dat wordt vertegenwoordigd door Hallo gekoppelde AzureStorageLinkedService1-service.</span><span class="sxs-lookup"><span data-stu-id="50d2b-197">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService1 linked service.</span></span> <span data-ttu-id="50d2b-198">Als u niet een waarde voor fileName hello opgeven (of overslaan), zijn gegevens uit alle blobs in de invoermap Hallo gekopieerde toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="50d2b-198">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="50d2b-199">In deze zelfstudie maakt opgeven u een waarde voor Hallo fileName.</span><span class="sxs-lookup"><span data-stu-id="50d2b-199">In this tutorial, you specify a value for hello fileName.</span></span> 

<span data-ttu-id="50d2b-200">U kunt hier Hallo term 'tabellen' gebruiken in plaats van 'gegevenssets'.</span><span class="sxs-lookup"><span data-stu-id="50d2b-200">Here, you use hello term "tables" rather than "datasets".</span></span> <span data-ttu-id="50d2b-201">Een tabel is een rechthoekige gegevensset en Hallo enige type gegevensset dat momenteel wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="50d2b-201">A table is a rectangular dataset and is hello only type of dataset supported right now.</span></span> 

1. <span data-ttu-id="50d2b-202">Met de rechtermuisknop op **tabellen** in Hallo **Solution Explorer**, wijst u te**toevoegen**, en klik op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-202">Right-click **Tables** in hello **Solution Explorer**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="50d2b-203">In Hallo **Add New Item** dialoogvenster, **Azure Blob**, en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-203">In hello **Add New Item** dialog box, select **Azure Blob**, and click **Add**.</span></span>   
3. <span data-ttu-id="50d2b-204">Hallo JSON-tekst vervangen door de volgende tekst hello en Hallo opslaan **AzureBlobLocation1.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="50d2b-204">Replace hello JSON text with hello following text and save hello **AzureBlobLocation1.json** file.</span></span> 

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
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
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
    <span data-ttu-id="50d2b-205">Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:</span><span class="sxs-lookup"><span data-stu-id="50d2b-205">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="50d2b-206">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="50d2b-206">Property</span></span> | <span data-ttu-id="50d2b-207">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="50d2b-207">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="50d2b-208">type</span><span class="sxs-lookup"><span data-stu-id="50d2b-208">type</span></span> | <span data-ttu-id="50d2b-209">Hallo type wordt ingesteld te**AzureBlob** omdat de gegevens zich in een Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="50d2b-209">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="50d2b-210">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="50d2b-210">linkedServiceName</span></span> | <span data-ttu-id="50d2b-211">Toohello verwijst **AzureStorageLinkedService** die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="50d2b-211">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="50d2b-212">folderPath</span><span class="sxs-lookup"><span data-stu-id="50d2b-212">folderPath</span></span> | <span data-ttu-id="50d2b-213">Hiermee geeft u op Hallo blob **container** en Hallo **map** die invoer blobs bevat.</span><span class="sxs-lookup"><span data-stu-id="50d2b-213">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="50d2b-214">In deze zelfstudie adftutorial is Hallo blob-container en map Hallo-hoofdmap is.</span><span class="sxs-lookup"><span data-stu-id="50d2b-214">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="50d2b-215">fileName</span><span class="sxs-lookup"><span data-stu-id="50d2b-215">fileName</span></span> | <span data-ttu-id="50d2b-216">Deze eigenschap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="50d2b-216">This property is optional.</span></span> <span data-ttu-id="50d2b-217">Als u deze eigenschap niet opgeeft, worden alle bestanden uit folderPath Hallo opgenomen.</span><span class="sxs-lookup"><span data-stu-id="50d2b-217">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="50d2b-218">In deze zelfstudie **emp.txt** hello bestandsnaam, zodat alleen dat bestand wordt opgehaald voor de verwerking wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="50d2b-218">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="50d2b-219">format -> type</span><span class="sxs-lookup"><span data-stu-id="50d2b-219">format -> type</span></span> |<span data-ttu-id="50d2b-220">Hallo-bestand voor invoer is in de indeling van de tekst hello, zodat we gebruiken **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-220">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="50d2b-221">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="50d2b-221">columnDelimiter</span></span> | <span data-ttu-id="50d2b-222">Hallo-kolommen in het invoerbestand Hallo worden gescheiden door **kommateken (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-222">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="50d2b-223">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="50d2b-223">frequency/interval</span></span> | <span data-ttu-id="50d2b-224">Hallo frequentie te is ingesteld**uur** en interval is ingesteld, te**1**, wat betekent dat Hallo invoer segmenten zijn beschikbaar **per uur**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-224">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="50d2b-225">Met andere woorden, Hallo Data Factory-service zoekt invoergegevens elk uur in de hoofdmap Hallo van blob-container (**adftutorial**) u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="50d2b-225">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="50d2b-226">Hallo-gegevens binnen Hallo pijplijn begin- en tijden, niet voor of na deze tijden zoekt.</span><span class="sxs-lookup"><span data-stu-id="50d2b-226">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="50d2b-227">external</span><span class="sxs-lookup"><span data-stu-id="50d2b-227">external</span></span> | <span data-ttu-id="50d2b-228">Deze eigenschap is ingesteld, te**true** als Hallo gegevens niet worden gegenereerd door deze pijplijn.</span><span class="sxs-lookup"><span data-stu-id="50d2b-228">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="50d2b-229">Hallo invoergegevens in deze zelfstudie wordt Hallo emp.txt bestand, die niet worden gegenereerd door deze pipeline, zodat we de tootrue van deze eigenschap wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="50d2b-229">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="50d2b-230">Zie het [artikel over Azure Blob-connectoren](data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over deze JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="50d2b-230">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>   

### <a name="create-output-dataset"></a><span data-ttu-id="50d2b-231">Uitvoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="50d2b-231">Create output dataset</span></span>
<span data-ttu-id="50d2b-232">In deze stap maakt u een uitvoergegevensset met de naam **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-232">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="50d2b-233">Deze gegevensset verwijst tooa SQL-tabel in hello Azure SQL-database dat wordt vertegenwoordigd door **AzureSqlLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-233">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService1**.</span></span> 

1. <span data-ttu-id="50d2b-234">Met de rechtermuisknop op **tabellen** in Hallo **Solution Explorer** opnieuw in en wijst te**toevoegen**, en klik op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-234">Right-click **Tables** in hello **Solution Explorer** again, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="50d2b-235">In Hallo **Add New Item** dialoogvenster, **Azure SQL**, en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-235">In hello **Add New Item** dialog box, select **Azure SQL**, and click **Add**.</span></span> 
3. <span data-ttu-id="50d2b-236">Hallo JSON-tekst vervangen door Hallo volgende JSON en sla Hallo **AzureSqlTableLocation1.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="50d2b-236">Replace hello JSON text with hello following JSON and save hello **AzureSqlTableLocation1.json** file.</span></span>

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
       "linkedServiceName": "AzureSqlLinkedService1",
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
    <span data-ttu-id="50d2b-237">Hallo bevat volgende tabel beschrijvingen van Hallo JSON-eigenschappen die in Hallo codefragment:</span><span class="sxs-lookup"><span data-stu-id="50d2b-237">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="50d2b-238">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="50d2b-238">Property</span></span> | <span data-ttu-id="50d2b-239">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="50d2b-239">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="50d2b-240">type</span><span class="sxs-lookup"><span data-stu-id="50d2b-240">type</span></span> | <span data-ttu-id="50d2b-241">Hallo type wordt ingesteld te**AzureSqlTable** omdat gegevens gekopieerde tooa tabel in een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="50d2b-241">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="50d2b-242">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="50d2b-242">linkedServiceName</span></span> | <span data-ttu-id="50d2b-243">Toohello verwijst **AzureSqlLinkedService** die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="50d2b-243">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="50d2b-244">tableName</span><span class="sxs-lookup"><span data-stu-id="50d2b-244">tableName</span></span> | <span data-ttu-id="50d2b-245">Opgegeven Hallo **tabel** toowhich Hallo gegevens worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="50d2b-245">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="50d2b-246">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="50d2b-246">frequency/interval</span></span> | <span data-ttu-id="50d2b-247">Hallo frequentie is ingesteld te**uur** en interval is **1**, wat betekent dat Hallo uitvoer segmenten worden geproduceerd **per uur** tussen Hallo pijplijn begin- en tijden niet voor of na deze tijden.</span><span class="sxs-lookup"><span data-stu-id="50d2b-247">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="50d2b-248">Er zijn drie kolommen – **ID**, **FirstName**, en **LastName** – in Hallo emp-tabel in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="50d2b-248">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="50d2b-249">-ID is een identiteitskolom, dus u alleen toospecify hoeft **FirstName** en **LastName** hier.</span><span class="sxs-lookup"><span data-stu-id="50d2b-249">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="50d2b-250">Zie het [artikel over Azure SQL-connectoren](data-factory-azure-sql-connector.md#dataset-properties) voor meer informatie over deze JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="50d2b-250">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

## <a name="create-pipeline"></a><span data-ttu-id="50d2b-251">Pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="50d2b-251">Create pipeline</span></span>
<span data-ttu-id="50d2b-252">In deze stap maakt u een pijplijn met een **kopieeractiviteit** die gebruikmaakt van **InputDataset** als invoer en **OutputDataset** als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="50d2b-252">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="50d2b-253">Uitvoergegevensset is momenteel welke stations Hallo planning.</span><span class="sxs-lookup"><span data-stu-id="50d2b-253">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="50d2b-254">In deze zelfstudie is uitvoergegevensset geconfigureerde tooproduce een segment eens per uur.</span><span class="sxs-lookup"><span data-stu-id="50d2b-254">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="50d2b-255">Hallo pijplijn heeft een begintijd en eindtijd die één dag uit elkaar liggen, wat is 24 uur zijn.</span><span class="sxs-lookup"><span data-stu-id="50d2b-255">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="50d2b-256">Daarom worden 24 segmenten van uitvoergegevensset geproduceerd door Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="50d2b-256">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="50d2b-257">Met de rechtermuisknop op **pijplijnen** in Hallo **Solution Explorer**, wijst u te**toevoegen**, en klik op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-257">Right-click **Pipelines** in hello **Solution Explorer**, point too**Add**, and click **New Item**.</span></span>  
2. <span data-ttu-id="50d2b-258">Selecteer **Copy Data Pipeline** in Hallo **Add New Item** dialoogvenster en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-258">Select **Copy Data Pipeline** in hello **Add New Item** dialog box and click **Add**.</span></span> 
3. <span data-ttu-id="50d2b-259">Hallo JSON vervangen door Hallo volgende JSON en sla Hallo **CopyActivity1.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="50d2b-259">Replace hello JSON with hello following JSON and save hello **CopyActivity1.json** file.</span></span>

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
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - <span data-ttu-id="50d2b-260">In Hallo gedeelte activiteiten is er slechts één activiteit waarvan **type** te is ingesteld,**kopie**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-260">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="50d2b-261">Zie voor meer informatie over de kopieeractiviteit hello [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="50d2b-261">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="50d2b-262">In Data Factory-oplossingen kunt u ook [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="50d2b-262">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="50d2b-263">Invoer voor Hallo-activiteit is ingesteld, te**InputDataset** en de uitvoer voor Hallo activiteit te is ingesteld**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-263">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="50d2b-264">In Hallo **typeProperties** sectie **BlobSource** is opgegeven als Hallo brontype en **SqlSink** is opgegeven als Hallo sink-type.</span><span class="sxs-lookup"><span data-stu-id="50d2b-264">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="50d2b-265">Zie voor een volledige lijst van gegevensarchieven die worden ondersteund door Hallo kopieeractiviteit als bronnen en put [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="50d2b-265">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="50d2b-266">toolearn hoe toouse een specifieke ondersteunde gegevens opslaan als een bron/sink, klikt u op Hallo-koppeling in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="50d2b-266">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
     
    <span data-ttu-id="50d2b-267">Vervang de waarde Hallo Hallo **start** eigenschap met de huidige dag Hallo en **end** waarde met de volgende dag Hallo.</span><span class="sxs-lookup"><span data-stu-id="50d2b-267">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="50d2b-268">U kunt alleen Hallo datumgedeelte opgeven en Hallo tijdgedeelte van Hallo datum / tijd overslaan.</span><span class="sxs-lookup"><span data-stu-id="50d2b-268">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="50d2b-269">Bijvoorbeeld '2016-02-03', dat te gelijk ' 2016-02-03T00:00:00Z '</span><span class="sxs-lookup"><span data-stu-id="50d2b-269">For example, "2016-02-03", which is equivalent too"2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="50d2b-270">Zowel de begin- als einddatum en -tijd moeten de [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601) hebben.</span><span class="sxs-lookup"><span data-stu-id="50d2b-270">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="50d2b-271">Bijvoorbeeld: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="50d2b-271">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="50d2b-272">Hallo **end** tijd is optioneel, maar er worden gebruikt in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="50d2b-272">hello **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="50d2b-273">Als u geen waarde voor Hallo opgeeft **end** eigenschap, wordt berekend als '**start + 48 uur**'.</span><span class="sxs-lookup"><span data-stu-id="50d2b-273">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="50d2b-274">toorun hello pijplijn voor onbepaalde tijd, geef **9999-09-09** als waarde voor Hallo Hallo **end** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="50d2b-274">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="50d2b-275">In de Hallo voorgaande voorbeeld, zijn er 24 gegevenssegmenten omdat elke gegevenssegment per uur is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="50d2b-275">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="50d2b-276">Zie het artikel [Pijplijnen maken](data-factory-create-pipelines.md) voor beschrijvingen van JSON-eigenschappen in de definitie van een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="50d2b-276">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="50d2b-277">Zie [Gegevensverplaatsingsactiviteiten](data-factory-data-movement-activities.md) voor beschrijvingen van JSON-eigenschappen in de definitie van een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="50d2b-277">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="50d2b-278">Zie het [artikel over Azure Blob-connectoren](data-factory-azure-blob-connector.md) voor beschrijvingen van JSON-eigenschappen die worden ondersteund door BlobSource.</span><span class="sxs-lookup"><span data-stu-id="50d2b-278">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="50d2b-279">Zie het [artikel over Azure SQL Database-connectoren](data-factory-azure-sql-connector.md) voor beschrijvingen van JSON-eigenschappen die worden ondersteund door SqlSink.</span><span class="sxs-lookup"><span data-stu-id="50d2b-279">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="50d2b-280">Data Factory-entiteiten publiceren/implementeren</span><span class="sxs-lookup"><span data-stu-id="50d2b-280">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="50d2b-281">In deze stap publiceert u Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="50d2b-281">In this step, you publish Data Factory entities (linked services, datasets, and pipeline) you created earlier.</span></span> <span data-ttu-id="50d2b-282">U kunt ook opgeven Hallo-naam van Hallo nieuwe data factory toobe gemaakt toohold deze entiteiten.</span><span class="sxs-lookup"><span data-stu-id="50d2b-282">You also specify hello name of hello new data factory toobe created toohold these entities.</span></span>  

1. <span data-ttu-id="50d2b-283">Met de rechtermuisknop op het project in Solution Explorer Hallo en klik op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-283">Right-click project in hello Solution Explorer, and click **Publish**.</span></span> 
2. <span data-ttu-id="50d2b-284">Als u ziet **tooyour Microsoft-account aanmelden** in het dialoogvenster Geef uw referenties voor het Hallo-account met Azure-abonnement en klikt u op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-284">If you see **Sign in tooyour Microsoft account** dialog box, enter your credentials for hello account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="50d2b-285">U ziet Hallo in het dialoogvenster te volgen:</span><span class="sxs-lookup"><span data-stu-id="50d2b-285">You should see hello following dialog box:</span></span>
   
   ![Het dialoogvenster Publish](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. <span data-ttu-id="50d2b-287">In de pagina voor Hallo Configure data factory Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="50d2b-287">In hello Configure data factory page, do hello following steps:</span></span> 
   
   1. <span data-ttu-id="50d2b-288">Selecteer **Create New Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-288">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="50d2b-289">Voer **VSTutorialFactory** in als **naam**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-289">Enter **VSTutorialFactory** for **Name**.</span></span>  
      
      > [!IMPORTANT]
      > <span data-ttu-id="50d2b-290">Hallo-naam van hello Azure-gegevensfactory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="50d2b-290">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="50d2b-291">Als er een over Hallo-naam van gegevensfactory foutbericht bij het publiceren, moet u Hallo-naam van gegevensfactory hello (bijvoorbeeld yournameVSTutorialFactory) en publiceert u opnieuw wijzigen.</span><span class="sxs-lookup"><span data-stu-id="50d2b-291">If you receive an error about hello name of data factory when publishing, change hello name of hello data factory (for example, yournameVSTutorialFactory) and try publishing again.</span></span> <span data-ttu-id="50d2b-292">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="50d2b-292">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>        
      > 
      > 
   3. <span data-ttu-id="50d2b-293">Selecteer uw Azure-abonnement voor Hallo **abonnement** veld.</span><span class="sxs-lookup"><span data-stu-id="50d2b-293">Select your Azure subscription for hello **Subscription** field.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="50d2b-294">Als u een abonnement niet ziet, zorg ervoor dat u aangemeld met een account dat een beheerder of co-beheerder van het Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="50d2b-294">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of hello subscription.</span></span>  
      > 
      > 
   4. <span data-ttu-id="50d2b-295">Selecteer Hallo **resourcegroep** voor Hallo data factory toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="50d2b-295">Select hello **resource group** for hello data factory toobe created.</span></span> 
   5. <span data-ttu-id="50d2b-296">Selecteer Hallo **regio** voor Hallo data factory.</span><span class="sxs-lookup"><span data-stu-id="50d2b-296">Select hello **region** for hello data factory.</span></span> <span data-ttu-id="50d2b-297">Regio's wordt ondersteund door Hallo Data Factory-service worden weergegeven in de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="50d2b-297">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
   6. <span data-ttu-id="50d2b-298">Klik op **volgende** tooswitch toohello **Publish Items** pagina.</span><span class="sxs-lookup"><span data-stu-id="50d2b-298">Click **Next** tooswitch toohello **Publish Items** page.</span></span>
      
       ![Pagina Data Factory configureren](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. <span data-ttu-id="50d2b-300">In Hallo **Publish Items** pagina, zorg ervoor dat alle Data Factory-entiteiten zijn geselecteerd en klik op Hallo **volgende** tooswitch toohello **samenvatting** pagina.</span><span class="sxs-lookup"><span data-stu-id="50d2b-300">In hello **Publish Items** page, ensure that all hello Data Factories entities are selected, and click **Next** tooswitch toohello **Summary** page.</span></span>
   
   ![Pagina Items publiceren](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. <span data-ttu-id="50d2b-302">Controleer Hallo samenvatting en klik op **volgende** toostart Hallo implementatie proces en bekijkt hello **Implementatiestatus**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-302">Review hello summary and click **Next** toostart hello deployment process and view hello **Deployment Status**.</span></span>
   
   ![Pagina Samenvatting publiceren](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. <span data-ttu-id="50d2b-304">In Hallo **Implementatiestatus** pagina ziet u Hallo status van implementatieproces Hallo.</span><span class="sxs-lookup"><span data-stu-id="50d2b-304">In hello **Deployment Status** page, you should see hello status of hello deployment process.</span></span> <span data-ttu-id="50d2b-305">Klik op Voltooien nadat het Hallo-implementatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="50d2b-305">Click Finish after hello deployment is done.</span></span>
 
   ![Pagina Deployment Status](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

<span data-ttu-id="50d2b-307">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="50d2b-307">Note hello following points:</span></span> 

* <span data-ttu-id="50d2b-308">Als u Hallo-foutmelding: 'dit abonnement is niet geregistreerd toouse namespace Microsoft.DataFactory', voer een van de volgende Hallo en probeer opnieuw te publiceren:</span><span class="sxs-lookup"><span data-stu-id="50d2b-308">If you receive hello error: "This subscription is not registered toouse namespace Microsoft.DataFactory", do one of hello following and try publishing again:</span></span> 
  
  * <span data-ttu-id="50d2b-309">Voer in Azure PowerShell Hallo opdracht tooregister Hallo Data Factory-provider te volgen.</span><span class="sxs-lookup"><span data-stu-id="50d2b-309">In Azure PowerShell, run hello following command tooregister hello Data Factory provider.</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="50d2b-310">Die Hallo Data Factory-provider is geregistreerd, kunt u na de opdracht tooconfirm Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="50d2b-310">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="50d2b-311">Aanmelding via het Azure-abonnement in Hallo Hallo [Azure-portal](https://portal.azure.com) en navigeer tooa Data Factory-blade of maak een gegevensfactory in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="50d2b-311">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="50d2b-312">Deze actie automatisch Hallo provider voor u geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="50d2b-312">This action automatically registers hello provider for you.</span></span>
* <span data-ttu-id="50d2b-313">Hallo-naam van de gegevensfactory Hallo kan worden geregistreerd als DNS-naam in toekomstige Hallo en daarmee ook voor iedereen zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="50d2b-313">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="50d2b-314">toocreate Data Factory-exemplaren, moet u toobe beheerder/co-beheerder van hello Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="50d2b-314">toocreate Data Factory instances, you need toobe a admin/co-admin of hello Azure subscription</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="50d2b-315">De pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="50d2b-315">Monitor pipeline</span></span>
<span data-ttu-id="50d2b-316">Navigeer toohello startpagina voor uw data factory:</span><span class="sxs-lookup"><span data-stu-id="50d2b-316">Navigate toohello home page for your data factory:</span></span>

1. <span data-ttu-id="50d2b-317">Meld u bij te[Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="50d2b-317">Log in too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="50d2b-318">Klik op **meer services** op Hallo van menu aan de linkerkant en klik op **gegevensfactory**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-318">Click **More services** on hello left menu, and click **Data factories**.</span></span>

    ![Door gegevensfactory’s bladeren](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. <span data-ttu-id="50d2b-320">Naam begint te typen Hallo van uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="50d2b-320">Start typing hello name of your data factory.</span></span>

    ![Naam van gegevensfactory](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. <span data-ttu-id="50d2b-322">Klik op uw gegevensfactory in Hallo resultaten lijst toosee Hallo de startpagina van uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="50d2b-322">Click your data factory in hello results list toosee hello home page for your data factory.</span></span>

    ![Startpagina van de gegevensfactory](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. <span data-ttu-id="50d2b-324">Volg de instructies uit [gegevenssets en pijplijn bewaken](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor Hallo pijplijn en gegevenssets u in deze zelfstudie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="50d2b-324">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="50d2b-325">Visual Studio biedt momenteel geen ondersteuning voor het bewaken van Data Factory-pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="50d2b-325">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span> 

## <a name="summary"></a><span data-ttu-id="50d2b-326">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="50d2b-326">Summary</span></span>
<span data-ttu-id="50d2b-327">In deze zelfstudie maakt u een Azure data factory toocopy gegevens uit een Azure-blobopslag tooan Azure SQL database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="50d2b-327">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="50d2b-328">U hebt Visual Studio toocreate hello gegevensfactory, gekoppelde services, gegevenssets en een pijplijn gebruikt.</span><span class="sxs-lookup"><span data-stu-id="50d2b-328">You used Visual Studio toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="50d2b-329">Hier volgen Hallo hoofdstappen die u in deze zelfstudie hebt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="50d2b-329">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="50d2b-330">U hebt een Azure-**gegevensfactory** gemaakt.</span><span class="sxs-lookup"><span data-stu-id="50d2b-330">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="50d2b-331">U hebt **gekoppelde services** gemaakt:</span><span class="sxs-lookup"><span data-stu-id="50d2b-331">Created **linked services**:</span></span>
   1. <span data-ttu-id="50d2b-332">Een **Azure Storage** service toolink uw Azure Storage-account dat invoergegevens bevat gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="50d2b-332">An **Azure Storage** linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="50d2b-333">Een **Azure SQL** gekoppelde service toolink uw Azure SQL-database die uitvoergegevens Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="50d2b-333">An **Azure SQL** linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="50d2b-334">U hebt **gegevenssets** gemaakt waarin de invoer- en uitvoergegevens van pijplijnen worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="50d2b-334">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="50d2b-335">U hebt een **pijplijn** gemaakt met een **kopieeractiviteit** met **BlobSource** als bron en **SqlSink** als sink.</span><span class="sxs-lookup"><span data-stu-id="50d2b-335">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span> 

<span data-ttu-id="50d2b-336">hoe de gegevens van een HDInsight Hive-activiteit tootransform met behulp van Azure HDInsight-cluster toouse zien toosee [ zelfstudie: bouwen van uw eerste pijplijn tootransform gegevens met Hadoop-cluster](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="50d2b-336">toosee how toouse a HDInsight Hive Activity tootransform data by using Azure HDInsight cluster, see [ Tutorial: Build your first pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="50d2b-337">U kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="50d2b-337">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="50d2b-338">Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="50d2b-338">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 

## <a name="view-all-data-factories-in-server-explorer"></a><span data-ttu-id="50d2b-339">Alle gegevensfactory’s weergeven in Server Explorer</span><span class="sxs-lookup"><span data-stu-id="50d2b-339">View all data factories in Server Explorer</span></span>
<span data-ttu-id="50d2b-340">Deze sectie beschrijft hoe toouse Hallo van Server Explorer in Visual Studio tooview alle Hallo data Factory in uw Azure-abonnement en maak een Visual Studio-project op basis van een bestaande gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="50d2b-340">This section describes how toouse hello Server Explorer in Visual Studio tooview all hello data factories in your Azure subscription and create a Visual Studio project based on an existing data factory.</span></span> 

1. <span data-ttu-id="50d2b-341">In **Visual Studio**, klikt u op **weergave** op Hallo van menu en klik op **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-341">In **Visual Studio**, click **View** on hello menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="50d2b-342">Vouw in Server Explorer-venster Hallo **Azure** en vouw **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-342">In hello Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="50d2b-343">Als u ziet **tooVisual Studio aanmelden**, Voer Hallo **account** die zijn gekoppeld aan uw Azure-abonnement en klik op **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-343">If you see **Sign in tooVisual Studio**, enter hello **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="50d2b-344">Voer het **wachtwoord** in en klik op **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-344">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="50d2b-345">Visual Studio haalt tooget informatie over alle Azure data factory's in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="50d2b-345">Visual Studio tries tooget information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="50d2b-346">Hallo-status van deze bewerking in Hallo weergegeven **Data Factory Task List** venster.</span><span class="sxs-lookup"><span data-stu-id="50d2b-346">You see hello status of this operation in hello **Data Factory Task List** window.</span></span>

    ![Server Explorer](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a><span data-ttu-id="50d2b-348">Een Visual Studio-project maken voor een bestaande gegevensfactory</span><span class="sxs-lookup"><span data-stu-id="50d2b-348">Create a Visual Studio project for an existing data factory</span></span>

- <span data-ttu-id="50d2b-349">Met de rechtermuisknop op een gegevensfactory in Server Explorer en selecteer **tooNew Export Data Factory Project** toocreate een Visual Studio-project op basis van een bestaande gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="50d2b-349">Right-click a data factory in Server Explorer, and select **Export Data Factory tooNew Project** toocreate a Visual Studio project based on an existing data factory.</span></span>

    ![Export data factory tooa VS-project](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="50d2b-351">Data Factory-hulpprogramma's voor Visual Studio bijwerken</span><span class="sxs-lookup"><span data-stu-id="50d2b-351">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="50d2b-352">tooupdate Azure Data Factory-hulpprogramma's voor Visual Studio Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="50d2b-352">tooupdate Azure Data Factory tools for Visual Studio, do hello following steps:</span></span>

1. <span data-ttu-id="50d2b-353">Klik op **extra** op Hallo menu en selecteer **uitbreidingen en Updates**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-353">Click **Tools** on hello menu and select **Extensions and Updates**.</span></span> 
2. <span data-ttu-id="50d2b-354">Selecteer **Updates** in Hallo linkerdeelvenster en selecteer vervolgens **Visual Studio-galerie**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-354">Select **Updates** in hello left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="50d2b-355">Selecteer **Azure Data Factory-hulpprogramma's voor Visual Studio** en klik op **Bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-355">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="50d2b-356">Als u deze vermelding niet ziet, hebt u al de meest recente versie Hallo Hallo-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="50d2b-356">If you do not see this entry, you already have hello latest version of hello tools.</span></span> 

## <a name="use-configuration-files"></a><span data-ttu-id="50d2b-357">Configuratiebestanden gebruiken</span><span class="sxs-lookup"><span data-stu-id="50d2b-357">Use configuration files</span></span>
<span data-ttu-id="50d2b-358">U kunt de configuratiebestanden in Visual Studio tooconfigure eigenschappen voor de gekoppelde services/tabellen/pijplijnen anders voor elke omgeving.</span><span class="sxs-lookup"><span data-stu-id="50d2b-358">You can use configuration files in Visual Studio tooconfigure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="50d2b-359">Houd rekening met Hallo volgende JSON-definitie voor een gekoppelde Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="50d2b-359">Consider hello following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="50d2b-360">toospecify **connectionString** met verschillende waarden voor accountname en accountkey op basis van het Hallo-omgeving (ontwikkeling/tests/productie) toowhich u Data Factory-entiteiten implementeert.</span><span class="sxs-lookup"><span data-stu-id="50d2b-360">toospecify **connectionString** with different values for accountname and accountkey based on hello environment (Dev/Test/Production) toowhich you are deploying Data Factory entities.</span></span> <span data-ttu-id="50d2b-361">U kunt dit gedrag bewerkstelligen door een afzonderlijk configuratiebestand te gebruiken voor elke omgeving.</span><span class="sxs-lookup"><span data-stu-id="50d2b-361">You can achieve this behavior by using separate configuration file for each environment.</span></span>

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

### <a name="add-a-configuration-file"></a><span data-ttu-id="50d2b-362">Een configuratiebestand toevoegen</span><span class="sxs-lookup"><span data-stu-id="50d2b-362">Add a configuration file</span></span>
<span data-ttu-id="50d2b-363">Voeg een configuratiebestand voor elke omgeving toe door Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="50d2b-363">Add a configuration file for each environment by performing hello following steps:</span></span>   

1. <span data-ttu-id="50d2b-364">Met de rechtermuisknop op Hallo Data Factory-project in Visual Studio-oplossing, wijst u te**toevoegen**, en klik op **nieuw item**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-364">Right-click hello Data Factory project in your Visual Studio solution, point too**Add**, and click **New item**.</span></span>
2. <span data-ttu-id="50d2b-365">Selecteer **Config** Selecteer in de lijst met geïnstalleerde sjablonen aan de linkerkant Hallo Hallo **configuratiebestand**, voer een **naam** voor Hallo configuratie bestand en klik op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-365">Select **Config** from hello list of installed templates on hello left, select **Configuration File**, enter a **name** for hello configuration file, and click **Add**.</span></span>

    ![Een configuratiebestand toevoegen](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="50d2b-367">Configuratieparameters en hun waarden in de volgende indeling Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="50d2b-367">Add configuration parameters and their values in hello following format:</span></span>

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

    <span data-ttu-id="50d2b-368">In dit voorbeeld configureert u de eigenschap connectionString van een gekoppelde Azure Storage-service en een gekoppelde Azure SQL-service.</span><span class="sxs-lookup"><span data-stu-id="50d2b-368">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="50d2b-369">U ziet dat Hallo-syntaxis voor het opgeven van de naam is [JsonPath](http://goessner.net/articles/JsonPath/).</span><span class="sxs-lookup"><span data-stu-id="50d2b-369">Notice that hello syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="50d2b-370">Als JSON een eigenschap die een matrix met waarden heeft is zoals weergegeven in de volgende code Hallo:</span><span class="sxs-lookup"><span data-stu-id="50d2b-370">If JSON has a property that has an array of values as shown in hello following code:</span></span>  

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

    <span data-ttu-id="50d2b-371">Eigenschappen configureren zoals wordt weergegeven in het Hallo-configuratiebestand (gebruik op nul gebaseerde indexering) te volgen:</span><span class="sxs-lookup"><span data-stu-id="50d2b-371">Configure properties as shown in hello following configuration file (use zero-based indexing):</span></span>

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

### <a name="property-names-with-spaces"></a><span data-ttu-id="50d2b-372">Eigenschapnamen met spaties</span><span class="sxs-lookup"><span data-stu-id="50d2b-372">Property names with spaces</span></span>
<span data-ttu-id="50d2b-373">Als de naam van een eigenschap spaties bevat, gebruikt u vierkante haken, zoals in Hallo volgt (databaseservernaam):</span><span class="sxs-lookup"><span data-stu-id="50d2b-373">If a property name has spaces in it, use square brackets as shown in hello following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="50d2b-374">Een oplossing implementeren met behulp van een configuratie</span><span class="sxs-lookup"><span data-stu-id="50d2b-374">Deploy solution using a configuration</span></span>
<span data-ttu-id="50d2b-375">Wanneer u Azure Data Factory-entiteiten in de VS publiceert, kunt u Hallo configuratie dat u toouse voor die publicatiebewerking wilt opgeven.</span><span class="sxs-lookup"><span data-stu-id="50d2b-375">When you are publishing Azure Data Factory entities in VS, you can specify hello configuration that you want toouse for that publishing operation.</span></span>

<span data-ttu-id="50d2b-376">toopublish entiteiten in een configuratiebestand met Azure Data Factory-project:</span><span class="sxs-lookup"><span data-stu-id="50d2b-376">toopublish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="50d2b-377">Met de rechtermuisknop op de Data Factory-project en klik op **publiceren** toosee hello **Publish Items** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="50d2b-377">Right-click Data Factory project and click **Publish** toosee hello **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="50d2b-378">Selecteer een bestaande gegevensfactory of geef waarden voor het maken van een gegevensfactory op Hallo **Configure data factory** pagina en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-378">Select an existing data factory or specify values for creating a data factory on hello **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="50d2b-379">Op Hallo **Publish Items** pagina: u ziet een vervolgkeuzelijst met beschikbare configuraties voor Hallo **Select Deployment Config** veld.</span><span class="sxs-lookup"><span data-stu-id="50d2b-379">On hello **Publish Items** page: you see a drop-down list with available configurations for hello **Select Deployment Config** field.</span></span>

    ![Een configuratiebestand selecteren](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="50d2b-381">Selecteer Hallo **configuratiebestand** dat u wilt, zoals toouse en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-381">Select hello **configuration file** that you would like toouse and click **Next**.</span></span>
5. <span data-ttu-id="50d2b-382">Controleer of u Hallo-naam van de JSON-bestand in Hallo **samenvatting** pagina en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="50d2b-382">Confirm that you see hello name of JSON file in hello **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="50d2b-383">Klik op **voltooien** nadat Hallo implementatiebewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="50d2b-383">Click **Finish** after hello deployment operation is finished.</span></span>

<span data-ttu-id="50d2b-384">Wanneer u implementeert, zijn Hallo waarden uit het configuratiebestand Hallo gebruikte tooset waarden voor eigenschappen in de JSON-bestanden Hallo voordat Hallo entiteiten geïmplementeerde tooAzure Data Factory-service worden.</span><span class="sxs-lookup"><span data-stu-id="50d2b-384">When you deploy, hello values from hello configuration file are used tooset values for properties in hello JSON files before hello entities are deployed tooAzure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="50d2b-385">Azure Key Vault gebruiken</span><span class="sxs-lookup"><span data-stu-id="50d2b-385">Use Azure Key Vault</span></span>
<span data-ttu-id="50d2b-386">Het is niet aangeraden en vaak tegen beveiliging beleid toocommit gevoelige gegevens zoals verbinding tekenreeksen toohello code opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="50d2b-386">It is not advisable and often against security policy toocommit sensitive data such as connection strings toohello code repository.</span></span> <span data-ttu-id="50d2b-387">Zie [ADF Secure publiceren](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) voorbeeld op GitHub toolearn over gevoelige informatie op te slaan in Azure Sleutelkluis en dit gebruikt bij het publiceren van de Data Factory-entiteiten.</span><span class="sxs-lookup"><span data-stu-id="50d2b-387">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub toolearn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="50d2b-388">Hallo-extensie beveiligde publiceren voor Visual Studio kunt Hallo geheimen toobe opgeslagen in de Sleutelkluis en alleen verwijzingen toothem zijn opgegeven in de gekoppelde services / implementatieconfiguraties.</span><span class="sxs-lookup"><span data-stu-id="50d2b-388">hello Secure Publish extension for Visual Studio allows hello secrets toobe stored in Key Vault and only references toothem are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="50d2b-389">Deze verwijzingen zijn opgelost als u Data Factory-entiteiten tooAzure publiceren.</span><span class="sxs-lookup"><span data-stu-id="50d2b-389">These references are resolved when you publish Data Factory entities tooAzure.</span></span> <span data-ttu-id="50d2b-390">Deze bestanden kunnen vervolgens worden doorgevoerd toosource opslagplaats zonder dat geen geheimen.</span><span class="sxs-lookup"><span data-stu-id="50d2b-390">These files can then be committed toosource repository without exposing any secrets.</span></span>


## <a name="next-steps"></a><span data-ttu-id="50d2b-391">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="50d2b-391">Next steps</span></span>
<span data-ttu-id="50d2b-392">In deze zelfstudie hebt u voor een kopieerbewerking een Azure Blob-opslag gebruikt als brongegevensarchief en een Azure SQL-database als doelgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="50d2b-392">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="50d2b-393">Hallo bevat volgende tabel een lijst met gegevensarchieven als bronnen en bestemmingen wordt ondersteund door Hallo kopieeractiviteit:</span><span class="sxs-lookup"><span data-stu-id="50d2b-393">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="50d2b-394">toolearn over hoe gegevens uit een data toocopy opslaan, klikt u op Hallo-koppeling voor de gegevensopslag Hallo in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="50d2b-394">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
