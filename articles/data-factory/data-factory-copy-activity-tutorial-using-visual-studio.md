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
ms.openlocfilehash: f90b158e45a3679210685765b23c8299eb76ed50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a><span data-ttu-id="764c2-103">Zelfstudie: een pijplijn maken met de kopieeractiviteit in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="764c2-103">Tutorial: Create a pipeline with Copy Activity using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="764c2-104">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="764c2-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="764c2-105">De wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="764c2-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="764c2-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="764c2-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="764c2-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="764c2-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="764c2-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="764c2-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="764c2-109">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="764c2-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="764c2-110">REST API</span><span class="sxs-lookup"><span data-stu-id="764c2-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="764c2-111">.NET-API</span><span class="sxs-lookup"><span data-stu-id="764c2-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="764c2-112">In dit artikel leert u hoe u Microsoft Visual Studio kunt gebruiken om een gegevensfactory te maken met een pijplijn waarmee gegevens worden gekopieerd van een Azure blobopslag naar een Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="764c2-112">In this article, you learn how to use the Microsoft Visual Studio to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="764c2-113">Als u niet bekend bent met Azure Data Factory, lees dan het artikel [Inleiding tot Azure Data Factory](data-factory-introduction.md) voordat u deze zelfstudie volgt.</span><span class="sxs-lookup"><span data-stu-id="764c2-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="764c2-114">In deze zelfstudie maakt u een pijplijn met één activiteit erin: kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="764c2-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="764c2-115">De kopieeractiviteit in Data Factory kopieert gegevens uit een ondersteund gegevensarchief naar een ondersteund sinkgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="764c2-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="764c2-116">Zie [Ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met gegevensarchieven die worden ondersteund als bron en als sink.</span><span class="sxs-lookup"><span data-stu-id="764c2-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="764c2-117">De activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens veilig, betrouwbaar en schaalbaar kunnen worden gekopieerd tussen verschillende gegevensarchieven.</span><span class="sxs-lookup"><span data-stu-id="764c2-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="764c2-118">Zie het artikel [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie over kopieeractiviteiten.</span><span class="sxs-lookup"><span data-stu-id="764c2-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="764c2-119">Een pijplijn kan meer dan één activiteit hebben.</span><span class="sxs-lookup"><span data-stu-id="764c2-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="764c2-120">Ook kunt u twee activiteiten koppelen (de ene activiteit na de andere laten uitvoeren) door de uitvoergegevensset van één activiteit in te stellen als invoergegevensset voor een andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="764c2-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="764c2-121">Zie [Meerdere activiteiten in een pijplijn](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="764c2-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE] 
> <span data-ttu-id="764c2-122">In de gegevenspijplijn in deze zelfstudie worden gegevens van een brongegevensarchief gekopieerd naar een doelgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="764c2-122">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="764c2-123">Zie [Zelfstudie: een pijplijn maken om gegevens te transformeren met een Hadoop-cluster](data-factory-build-your-first-pipeline.md) voor meer informatie over het transformeren van gegevens met Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="764c2-123">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="764c2-124">Vereisten</span><span class="sxs-lookup"><span data-stu-id="764c2-124">Prerequisites</span></span>
1. <span data-ttu-id="764c2-125">Lees het artikel [Overzicht van de zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) en voer de **vereiste** stappen uit.</span><span class="sxs-lookup"><span data-stu-id="764c2-125">Read through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article and complete the **prerequisite** steps.</span></span>       
2. <span data-ttu-id="764c2-126">Als u Data Factory-exemplaren wilt maken, moet u lid zijn van de rol [Inzender Data Factory](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) op abonnements-/resourcegroepsniveau.</span><span class="sxs-lookup"><span data-stu-id="764c2-126">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
3. <span data-ttu-id="764c2-127">De volgende zaken moeten op uw computer zijn geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="764c2-127">You must have the following installed on your computer:</span></span> 
   * <span data-ttu-id="764c2-128">Visual Studio 2013 of Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="764c2-128">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="764c2-129">Download de Azure SDK voor Visual Studio 2013 of Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="764c2-129">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="764c2-130">Ga naar de [Azure-downloadpagina](https://azure.microsoft.com/downloads/) en klik in het gedeelte **.NET** op **VS 2013** of **VS 2015**.</span><span class="sxs-lookup"><span data-stu-id="764c2-130">Navigate to [Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in the **.NET** section.</span></span>
   * <span data-ttu-id="764c2-131">Download de nieuwste Azure Data Factory-invoegtoepassing voor Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) of [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="764c2-131">Download the latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="764c2-132">U kunt de invoegtoepassing ook als volgt bijwerken: klik in het menu op **Extra** -> **Extensies en updates** -> **Online** -> **Visual Studio-galerie** -> **Microsoft Azure Data Factory-hulpprogramma's voor Visual Studio** -> **Bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="764c2-132">You can also update the plugin by doing the following steps: On the menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

## <a name="steps"></a><span data-ttu-id="764c2-133">Stappen</span><span class="sxs-lookup"><span data-stu-id="764c2-133">Steps</span></span>
<span data-ttu-id="764c2-134">Hier volgen de stappen die u uitvoert als onderdeel van deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="764c2-134">Here are the steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="764c2-135">**Gekoppelde services** maken in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="764c2-135">Create **linked services** in the data factory.</span></span> <span data-ttu-id="764c2-136">In deze stap maakt u twee gekoppelde services van het type: Azure Storage en Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="764c2-136">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="764c2-137">De AzureStorageLinkedService koppelt uw Azure-opslagaccount aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="764c2-137">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="764c2-138">U hebt een container gemaakt en gegevens naar dit opslagaccount geüpload als onderdeel van de [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="764c2-138">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="764c2-139">De AzureSqlLinkedService koppelt uw Azure SQL-database aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="764c2-139">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="764c2-140">De gegevens die worden gekopieerd uit de blobopslag worden opgeslagen in deze database.</span><span class="sxs-lookup"><span data-stu-id="764c2-140">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="764c2-141">Als onderdeel van de [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) hebt u een SQL-tabel in deze database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="764c2-141">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>     
2. <span data-ttu-id="764c2-142">Maak **invoer- en uitvoergegevenssets** in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="764c2-142">Create input and output **datasets** in the data factory.</span></span>  
    
    <span data-ttu-id="764c2-143">De gekoppelde Azure Storage-service geeft de verbindingsreeks op die de Data Factory-service tijdens runtime gebruikt om verbinding te maken met uw Azure-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="764c2-143">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="764c2-144">En de blobgegevensset voor invoer geeft de container en de map met de invoergegevens op.</span><span class="sxs-lookup"><span data-stu-id="764c2-144">And, the input blob dataset specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="764c2-145">Op dezelfde manier geeft de gekoppelde Azure SQL Database-service de verbindingsreeks op die de Data Factory-service in runtime gebruikt om verbinding te maken met uw Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="764c2-145">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="764c2-146">En de uitvoergegevensset van de SQL-tabel geeft de tabel in de database op waarnaar de gegevens uit de blobopslag worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="764c2-146">And, the output SQL table dataset specifies the table in the database to which the data from the blob storage is copied.</span></span>
3. <span data-ttu-id="764c2-147">Maak een **pijplijn** in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="764c2-147">Create a **pipeline** in the data factory.</span></span> <span data-ttu-id="764c2-148">In deze stap maakt u een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="764c2-148">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="764c2-149">Met de kopieeractiviteit worden gegevens uit een blob in de Azure-blobopslag naar een tabel in de Azure SQL-database gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="764c2-149">The copy activity copies data from a blob in the Azure blob storage to a table in the Azure SQL database.</span></span> <span data-ttu-id="764c2-150">U kunt een kopieeractiviteit gebruiken in een pijplijn om gegevens uit ondersteunde bronnen te kopiëren naar een ondersteunde bestemming.</span><span class="sxs-lookup"><span data-stu-id="764c2-150">You can use a copy activity in a pipeline to copy data from any supported source to any supported destination.</span></span> <span data-ttu-id="764c2-151">Zie het artikel [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met ondersteunde gegevensarchieven.</span><span class="sxs-lookup"><span data-stu-id="764c2-151">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
4. <span data-ttu-id="764c2-152">Maak een Azure-**gegevensfactory** tijdens het implementeren van de Data Factory-entiteiten (gekoppelde services, gegevenssets/tabellen en pijplijnen).</span><span class="sxs-lookup"><span data-stu-id="764c2-152">Create an Azure **data factory** when deploying Data Factory entities (linked services, datasets/tables, and pipelines).</span></span> 

## <a name="create-visual-studio-project"></a><span data-ttu-id="764c2-153">Een Visual Studio-project maken</span><span class="sxs-lookup"><span data-stu-id="764c2-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="764c2-154">Open **Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="764c2-154">Launch **Visual Studio 2015**.</span></span> <span data-ttu-id="764c2-155">Klik op **File**, houd de muisaanwijzer op **New** en klik op **Project**.</span><span class="sxs-lookup"><span data-stu-id="764c2-155">Click **File**, point to **New**, and click **Project**.</span></span> <span data-ttu-id="764c2-156">Het dialoogvenster **New Project** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="764c2-156">You should see the **New Project** dialog box.</span></span>  
2. <span data-ttu-id="764c2-157">Selecteer in het dialoogvenster **New Project** de sjabloon **DataFactory** en klik op **Empty Data Factory Project**.</span><span class="sxs-lookup"><span data-stu-id="764c2-157">In the **New Project** dialog, select the **DataFactory** template, and click **Empty Data Factory Project**.</span></span>  
   
    ![Het dialoogvenster New Project](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. <span data-ttu-id="764c2-159">Geef de naam van het project, de locatie van de oplossing en de naam van de oplossing op en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="764c2-159">Specify the name of the project, location for the solution, and name of the solution, and then click **OK**.</span></span>
   
    ![Solution Explorer](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a><span data-ttu-id="764c2-161">Gekoppelde services maken</span><span class="sxs-lookup"><span data-stu-id="764c2-161">Create linked services</span></span>
<span data-ttu-id="764c2-162">U maakt gekoppelde services in een gegevensfactory om uw gegevensarchieven en compute-services aan de gegevensfactory te koppelen.</span><span class="sxs-lookup"><span data-stu-id="764c2-162">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="764c2-163">In deze zelfstudie gebruikt u niet een willekeurige compute-service, zoals Azure HDInsight of Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="764c2-163">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="764c2-164">U gebruikt twee gegevensarchieven van het type Azure Storage (bron) en Azure SQL Database (doel).</span><span class="sxs-lookup"><span data-stu-id="764c2-164">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="764c2-165">Daarom maakt u twee gekoppelde services van het type: Azure Storage en AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="764c2-165">Therefore, you create two linked services of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="764c2-166">De gekoppelde Azure Storage-service koppelt uw Azure-opslagaccount aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="764c2-166">The Azure Storage linked service links your Azure storage account to the data factory.</span></span> <span data-ttu-id="764c2-167">Dit opslagaccount is het account waarin u een container hebt gemaakt en gegevens hebt geüpload als onderdeel van de [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="764c2-167">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="764c2-168">De gekoppelde Azure SGL-service koppelt uw Azure SQL-database aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="764c2-168">Azure SQL linked service links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="764c2-169">De gegevens die worden gekopieerd uit de blobopslag worden opgeslagen in deze database.</span><span class="sxs-lookup"><span data-stu-id="764c2-169">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="764c2-170">Als onderdeel van de [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) hebt u de emp-tabel in deze database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="764c2-170">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="764c2-171">Met gekoppelde services worden gegevensarchieven of compute-services gekoppeld aan een Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="764c2-171">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="764c2-172">Zie [Ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor alle bronnen en sinks die worden ondersteund door de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="764c2-172">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="764c2-173">Zie [Gekoppelde services berekenen](data-factory-compute-linked-services.md) voor de lijst met compute-services die worden ondersteund door Data Factory.</span><span class="sxs-lookup"><span data-stu-id="764c2-173">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory.</span></span> <span data-ttu-id="764c2-174">In deze zelfstudie gebruikt u geen compute-service.</span><span class="sxs-lookup"><span data-stu-id="764c2-174">In this tutorial, you do not use any compute service.</span></span> 

### <a name="create-the-azure-storage-linked-service"></a><span data-ttu-id="764c2-175">De gekoppelde Azure Storage-service maken</span><span class="sxs-lookup"><span data-stu-id="764c2-175">Create the Azure Storage linked service</span></span>
1. <span data-ttu-id="764c2-176">Klik in **Solution Explorer** met de rechtermuisknop op **Linked Services**. Houd de muisaanwijzer op **Add** en klik op **New Item**.</span><span class="sxs-lookup"><span data-stu-id="764c2-176">In **Solution Explorer**, right-click **Linked Services**, point to **Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="764c2-177">Selecteer in het dialoogvenster **Add New Item** de optie **Azure Storage Linked Service** in de lijst en klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="764c2-177">In the **Add New Item** dialog box, select **Azure Storage Linked Service** from the list, and click **Add**.</span></span> 
   
    ![Nieuwe gekoppelde service](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. <span data-ttu-id="764c2-179">Vervang `<accountname>` en `<accountkey>`* door de naam van uw Azure-opslagaccount en de bijbehorende sleutel.</span><span class="sxs-lookup"><span data-stu-id="764c2-179">Replace `<accountname>` and `<accountkey>`* with the name of your Azure storage account and its key.</span></span> 
   
    ![Een gekoppelde Azure Storage-service](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. <span data-ttu-id="764c2-181">Sla het bestand **AzureStorageLinkedService1.json** op.</span><span class="sxs-lookup"><span data-stu-id="764c2-181">Save the **AzureStorageLinkedService1.json** file.</span></span>

    <span data-ttu-id="764c2-182">Zie het artikel [Azure Blob Storage-connector](data-factory-azure-blob-connector.md#linked-service-properties) voor meer informatie over de JSON-eigenschappen in de definitie van de gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="764c2-182">For more information about JSON properties in the linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-the-azure-sql-linked-service"></a><span data-ttu-id="764c2-183">De gekoppelde Azure SQL-service maken</span><span class="sxs-lookup"><span data-stu-id="764c2-183">Create the Azure SQL linked service</span></span>
1. <span data-ttu-id="764c2-184">Klik met de rechtermuisknop opnieuw op het knooppunt **Linked Services** in **Solution Explorer**. Houd de muisaanwijzer op **Add** en klik op **New Item**.</span><span class="sxs-lookup"><span data-stu-id="764c2-184">Right-click on **Linked Services** node in the **Solution Explorer** again, point to **Add**, and click **New Item**.</span></span> 
2. <span data-ttu-id="764c2-185">Selecteer deze keer **Azure SQL Linked Service** en klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="764c2-185">This time, select **Azure SQL Linked Service**, and click **Add**.</span></span> 
3. <span data-ttu-id="764c2-186">In het bestand **AzureSqlLinkedService1.json** vervangt u `<servername>`, `<databasename>`, `<username@servername>` en `<password>` door de namen van uw Azure SQL-server, -database en -gebruikersaccount en voert u uw wachtwoord in.</span><span class="sxs-lookup"><span data-stu-id="764c2-186">In the **AzureSqlLinkedService1.json file**, replace `<servername>`, `<databasename>`, `<username@servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span>    
4. <span data-ttu-id="764c2-187">Sla het bestand **AzureSqlLinkedService1.json** op.</span><span class="sxs-lookup"><span data-stu-id="764c2-187">Save the **AzureSqlLinkedService1.json** file.</span></span> 
    
    <span data-ttu-id="764c2-188">Zie [Azure SQL Database-connector](data-factory-azure-sql-connector.md#linked-service-properties) voor meer informatie over deze JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="764c2-188">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>


## <a name="create-datasets"></a><span data-ttu-id="764c2-189">Gegevenssets maken</span><span class="sxs-lookup"><span data-stu-id="764c2-189">Create datasets</span></span>
<span data-ttu-id="764c2-190">In de vorige stap hebt u gekoppelde services gemaakt om uw Azure-opslagaccount en Azure SQL-database aan de gegevensfactory te koppelen.</span><span class="sxs-lookup"><span data-stu-id="764c2-190">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="764c2-191">In deze stap definieert u twee gegevenssets, InputDataset en OutputDataset genaamd, die staan voor de invoer- en uitvoergegevens die zijn opgeslagen in de gegevensarchieven waarnaar wordt verwezen door respectievelijk de AzureStorageLinkedService1 en de AzureSqlLinkedService1.</span><span class="sxs-lookup"><span data-stu-id="764c2-191">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService1 and AzureSqlLinkedService1 respectively.</span></span>

<span data-ttu-id="764c2-192">De gekoppelde Azure Storage-service geeft de verbindingsreeks op die de Data Factory-service tijdens runtime gebruikt om verbinding te maken met uw Azure-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="764c2-192">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="764c2-193">En de blobgegevensset voor invoer (InputDataset) geeft de container en de map met de invoergegevens op.</span><span class="sxs-lookup"><span data-stu-id="764c2-193">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="764c2-194">Op dezelfde manier geeft de gekoppelde Azure SQL Database-service de verbindingsreeks op die de Data Factory-service in runtime gebruikt om verbinding te maken met uw Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="764c2-194">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="764c2-195">En de uitvoergegevensset van de SQL-tabel (OututDataset) geeft de tabel in de database op waarnaar de gegevens uit de blobopslag worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="764c2-195">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="764c2-196">Invoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="764c2-196">Create input dataset</span></span>
<span data-ttu-id="764c2-197">In deze stap maakt u een gegevensset met de naam InputDataset die verwijst naar een blobbestand (emp.txt) in de hoofdmap van een blobcontainer (adftutorial) in Azure Storage. Deze container wordt vertegenwoordigd door de gekoppelde AzureStorageLinkedService1-service.</span><span class="sxs-lookup"><span data-stu-id="764c2-197">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService1 linked service.</span></span> <span data-ttu-id="764c2-198">Als u geen waarde voor de fileName hebt opgeven (of hebt overgeslagen), worden gegevens uit alle blobs in de invoermap naar het doel gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="764c2-198">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="764c2-199">In deze zelfstudie geeft u een waarde op voor de fileName.</span><span class="sxs-lookup"><span data-stu-id="764c2-199">In this tutorial, you specify a value for the fileName.</span></span> 

<span data-ttu-id="764c2-200">Hier kunt u de term 'tabellen' gebruiken in plaats van 'gegevenssets'.</span><span class="sxs-lookup"><span data-stu-id="764c2-200">Here, you use the term "tables" rather than "datasets".</span></span> <span data-ttu-id="764c2-201">Een tabel is een rechthoekige gegevensset en is het enige type gegevensset dat nu wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="764c2-201">A table is a rectangular dataset and is the only type of dataset supported right now.</span></span> 

1. <span data-ttu-id="764c2-202">Klik in **Solution Explorer** met de rechtermuisknop op **Tables**. Houd de muisaanwijzer op **Add** en klik op **New Item**.</span><span class="sxs-lookup"><span data-stu-id="764c2-202">Right-click **Tables** in the **Solution Explorer**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="764c2-203">In het dialoogvenster **Add New Item** selecteert u **Azure Blob** en klikt u op **Add**.</span><span class="sxs-lookup"><span data-stu-id="764c2-203">In the **Add New Item** dialog box, select **Azure Blob**, and click **Add**.</span></span>   
3. <span data-ttu-id="764c2-204">Vervang de JSON-tekst door de volgende tekst en sla het bestand **AzureBlobLocation1.json** op.</span><span class="sxs-lookup"><span data-stu-id="764c2-204">Replace the JSON text with the following text and save the **AzureBlobLocation1.json** file.</span></span> 

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
    <span data-ttu-id="764c2-205">De volgende tabel bevat beschrijvingen van de JSON-eigenschappen die in het codefragment worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="764c2-205">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="764c2-206">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="764c2-206">Property</span></span> | <span data-ttu-id="764c2-207">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="764c2-207">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="764c2-208">type</span><span class="sxs-lookup"><span data-stu-id="764c2-208">type</span></span> | <span data-ttu-id="764c2-209">De eigenschap type wordt ingesteld op **AzureBlob**, omdat de gegevens zich in een Azure-blobopslag bevinden.</span><span class="sxs-lookup"><span data-stu-id="764c2-209">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="764c2-210">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="764c2-210">linkedServiceName</span></span> | <span data-ttu-id="764c2-211">Deze eigenschap verwijst naar de **AzureStorageLinkedService** die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="764c2-211">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="764c2-212">folderPath</span><span class="sxs-lookup"><span data-stu-id="764c2-212">folderPath</span></span> | <span data-ttu-id="764c2-213">Deze eigenschap verwijst naar de blob**container** en de **map** die de blobs voor invoer bevat.</span><span class="sxs-lookup"><span data-stu-id="764c2-213">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="764c2-214">In deze zelfstudie is adftutorial de blobcontainer en is folder de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="764c2-214">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
    | <span data-ttu-id="764c2-215">fileName</span><span class="sxs-lookup"><span data-stu-id="764c2-215">fileName</span></span> | <span data-ttu-id="764c2-216">Deze eigenschap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="764c2-216">This property is optional.</span></span> <span data-ttu-id="764c2-217">Als u deze eigenschap niet opgeeft, worden alle bestanden uit folderPath gekozen.</span><span class="sxs-lookup"><span data-stu-id="764c2-217">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="764c2-218">In deze zelfstudie wordt **emp.txt** opgegeven voor de fileName, zodat alleen dat bestand wordt opgehaald voor de verwerking.</span><span class="sxs-lookup"><span data-stu-id="764c2-218">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="764c2-219">format -> type</span><span class="sxs-lookup"><span data-stu-id="764c2-219">format -> type</span></span> |<span data-ttu-id="764c2-220">Het invoerbestand is in de tekstindeling, zodat we **TextFormat** gebruiken.</span><span class="sxs-lookup"><span data-stu-id="764c2-220">The input file is in the text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="764c2-221">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="764c2-221">columnDelimiter</span></span> | <span data-ttu-id="764c2-222">De kolommen in het invoerbestand worden gescheiden door een **komma (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="764c2-222">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="764c2-223">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="764c2-223">frequency/interval</span></span> | <span data-ttu-id="764c2-224">Als frequency wordt ingesteld op **Hour** en het interval wordt ingesteld op **1**, betekent dit dat de invoersegmenten één keer per **uur** beschikbaar worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="764c2-224">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="764c2-225">Met andere woorden, de Data Factory-service zoekt elk uur naar invoergegevens in de hoofdmap van de opgegeven blobcontainer (**adftutorial**).</span><span class="sxs-lookup"><span data-stu-id="764c2-225">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="764c2-226">Er wordt gezocht naar gegevens binnen de begin- en eindtijd van de pijplijn, niet voor of na deze tijden.</span><span class="sxs-lookup"><span data-stu-id="764c2-226">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="764c2-227">external</span><span class="sxs-lookup"><span data-stu-id="764c2-227">external</span></span> | <span data-ttu-id="764c2-228">Deze eigenschap wordt ingesteld op **true** als de gegevens niet worden gegenereerd door deze pijplijn.</span><span class="sxs-lookup"><span data-stu-id="764c2-228">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="764c2-229">De invoergegevens in deze zelfstudie bevinden zich in het bestand emp.txt, dat niet wordt gegenereerd door deze pijplijn. Daarom stellen we deze eigenschap in op true.</span><span class="sxs-lookup"><span data-stu-id="764c2-229">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

    <span data-ttu-id="764c2-230">Zie het [artikel over Azure Blob-connectoren](data-factory-azure-blob-connector.md#dataset-properties) voor meer informatie over deze JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="764c2-230">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>   

### <a name="create-output-dataset"></a><span data-ttu-id="764c2-231">Uitvoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="764c2-231">Create output dataset</span></span>
<span data-ttu-id="764c2-232">In deze stap maakt u een uitvoergegevensset met de naam **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="764c2-232">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="764c2-233">Deze gegevensset wijst naar een SQL-tabel in de Azure SQL-database die wordt vertegenwoordigd door **AzureSqlLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="764c2-233">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService1**.</span></span> 

1. <span data-ttu-id="764c2-234">Klik in **Solution Explorer** opnieuw met de rechtermuisknop op **Tables**. Houd de muisaanwijzer op **Add** en klik op **New Item**.</span><span class="sxs-lookup"><span data-stu-id="764c2-234">Right-click **Tables** in the **Solution Explorer** again, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="764c2-235">In het dialoogvenster **Add New Item** selecteert u **Azure SQL** en klikt u op **Add**.</span><span class="sxs-lookup"><span data-stu-id="764c2-235">In the **Add New Item** dialog box, select **Azure SQL**, and click **Add**.</span></span> 
3. <span data-ttu-id="764c2-236">Vervang de JSON-tekst door de volgende JSON en sla het bestand **AzureSqlTableLocation1.json** op.</span><span class="sxs-lookup"><span data-stu-id="764c2-236">Replace the JSON text with the following JSON and save the **AzureSqlTableLocation1.json** file.</span></span>

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
    <span data-ttu-id="764c2-237">De volgende tabel bevat beschrijvingen van de JSON-eigenschappen die in het codefragment worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="764c2-237">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="764c2-238">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="764c2-238">Property</span></span> | <span data-ttu-id="764c2-239">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="764c2-239">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="764c2-240">type</span><span class="sxs-lookup"><span data-stu-id="764c2-240">type</span></span> | <span data-ttu-id="764c2-241">De eigenschap type wordt ingesteld op **AzureSqlTable** omdat gegevens naar een tabel in een Azure SQL-database worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="764c2-241">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="764c2-242">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="764c2-242">linkedServiceName</span></span> | <span data-ttu-id="764c2-243">Deze eigenschap verwijst naar de **AzureSqlLinkedService** die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="764c2-243">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="764c2-244">tableName</span><span class="sxs-lookup"><span data-stu-id="764c2-244">tableName</span></span> | <span data-ttu-id="764c2-245">Geeft de **tabel** aan waarnaar de gegevens worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="764c2-245">Specified the **table** to which the data is copied.</span></span> | 
    | <span data-ttu-id="764c2-246">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="764c2-246">frequency/interval</span></span> | <span data-ttu-id="764c2-247">De frequentie is ingesteld op **Hour** en het interval is **1**, wat betekent dat de uitvoersegmenten worden geproduceerd **per uur** tussen de begin- en eindtijd van de pijplijn, niet voor of na deze tijden.</span><span class="sxs-lookup"><span data-stu-id="764c2-247">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="764c2-248">De tabel emp in de database bevat drie kolommen: **ID**, **FirstName** en **LastName**.</span><span class="sxs-lookup"><span data-stu-id="764c2-248">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="764c2-249">ID is een identiteitskolom, zodat u alleen **FirstName** en **LastName** hoeft op te geven.</span><span class="sxs-lookup"><span data-stu-id="764c2-249">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="764c2-250">Zie het [artikel over Azure SQL-connectoren](data-factory-azure-sql-connector.md#dataset-properties) voor meer informatie over deze JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="764c2-250">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

## <a name="create-pipeline"></a><span data-ttu-id="764c2-251">Pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="764c2-251">Create pipeline</span></span>
<span data-ttu-id="764c2-252">In deze stap maakt u een pijplijn met een **kopieeractiviteit** die gebruikmaakt van **InputDataset** als invoer en **OutputDataset** als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="764c2-252">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="764c2-253">Momenteel is de uitvoergegevensset dat wat de planning aanstuurt.</span><span class="sxs-lookup"><span data-stu-id="764c2-253">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="764c2-254">In deze zelfstudie is de uitvoergegevensset geconfigureerd voor het produceren van een segment eenmaal per uur.</span><span class="sxs-lookup"><span data-stu-id="764c2-254">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="764c2-255">De pijplijn heeft een begintijd en eindtijd die één dag uit elkaar liggen, ofwel 24 uur.</span><span class="sxs-lookup"><span data-stu-id="764c2-255">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="764c2-256">Daarom worden 24 segmenten van de uitvoergegevensset door de pijplijn geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="764c2-256">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 

1. <span data-ttu-id="764c2-257">Klik in **Solution Explorer** met de rechtermuisknop op **Pipelines**. Houd de muisaanwijzer op **Add** en klik op **New Item**.</span><span class="sxs-lookup"><span data-stu-id="764c2-257">Right-click **Pipelines** in the **Solution Explorer**, point to **Add**, and click **New Item**.</span></span>  
2. <span data-ttu-id="764c2-258">Selecteer **Copy Data Pipeline** in het dialoogvenster **Add New Item** en klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="764c2-258">Select **Copy Data Pipeline** in the **Add New Item** dialog box and click **Add**.</span></span> 
3. <span data-ttu-id="764c2-259">Vervang de JSON door de volgende JSON en sla het bestand **CopyActivity1.json** op.</span><span class="sxs-lookup"><span data-stu-id="764c2-259">Replace the JSON with the following JSON and save the **CopyActivity1.json** file.</span></span>

  ```json   
    {
     "name": "ADFTutorialPipeline",
     "properties": {
       "description": "Copy data from a blob to Azure SQL table",
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
    - <span data-ttu-id="764c2-260">In het gedeelte Activiteiten is er slechts één activiteit waarvan **type** is ingesteld op **Copy**.</span><span class="sxs-lookup"><span data-stu-id="764c2-260">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="764c2-261">Zie het artikel [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie over kopieeractiviteiten.</span><span class="sxs-lookup"><span data-stu-id="764c2-261">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="764c2-262">In Data Factory-oplossingen kunt u ook [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="764c2-262">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="764c2-263">De invoer voor de activiteit is ingesteld op **InputDataset** en de uitvoer voor de activiteit is ingesteld op **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="764c2-263">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="764c2-264">In het gedeelte **typeProperties** is **BlobSource** opgegeven als het brontype en **SqlSink** als het sink-type.</span><span class="sxs-lookup"><span data-stu-id="764c2-264">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="764c2-265">Zie [Ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een volledige lijst van gegevensarchieven die worden ondersteund door kopieeractiviteiten als bronnen en sinks.</span><span class="sxs-lookup"><span data-stu-id="764c2-265">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="764c2-266">Klik op de koppeling in de tabel voor informatie over het gebruik van een specifiek ondersteund gegevensarchief als een bron/sink.</span><span class="sxs-lookup"><span data-stu-id="764c2-266">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
     
    <span data-ttu-id="764c2-267">Vervang de waarde van de eigenschap **start** door de huidige dag en de waarde **end** door de volgende dag.</span><span class="sxs-lookup"><span data-stu-id="764c2-267">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="764c2-268">U hoeft alleen de datum in te vullen en kunt de tijd overslaan.</span><span class="sxs-lookup"><span data-stu-id="764c2-268">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="764c2-269">Dit wordt dan bijvoorbeeld 2016-02-03, wat gelijk staat aan 2016-02-03T00:00:00Z</span><span class="sxs-lookup"><span data-stu-id="764c2-269">For example, "2016-02-03", which is equivalent to "2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="764c2-270">Zowel de begin- als einddatum en -tijd moeten de [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601) hebben.</span><span class="sxs-lookup"><span data-stu-id="764c2-270">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="764c2-271">Bijvoorbeeld: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="764c2-271">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="764c2-272">De **eindtijd** is optioneel, maar we gebruiken hem in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="764c2-272">The **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="764c2-273">Als u geen waarde opgeeft voor de eigenschap **end**, wordt automatisch **start + 48 uur** gebruikt.</span><span class="sxs-lookup"><span data-stu-id="764c2-273">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="764c2-274">Als u de pijplijn voor onbepaalde tijd wilt uitvoeren, geeft u **9999-09-09** op als waarde voor de eigenschap **end**.</span><span class="sxs-lookup"><span data-stu-id="764c2-274">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
     
    <span data-ttu-id="764c2-275">In het voorgaande voorbeeld zijn er 24 gegevenssegmenten omdat er elk uur één gegevenssegment wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="764c2-275">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="764c2-276">Zie het artikel [Pijplijnen maken](data-factory-create-pipelines.md) voor beschrijvingen van JSON-eigenschappen in de definitie van een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="764c2-276">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="764c2-277">Zie [Gegevensverplaatsingsactiviteiten](data-factory-data-movement-activities.md) voor beschrijvingen van JSON-eigenschappen in de definitie van een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="764c2-277">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="764c2-278">Zie het [artikel over Azure Blob-connectoren](data-factory-azure-blob-connector.md) voor beschrijvingen van JSON-eigenschappen die worden ondersteund door BlobSource.</span><span class="sxs-lookup"><span data-stu-id="764c2-278">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="764c2-279">Zie het [artikel over Azure SQL Database-connectoren](data-factory-azure-sql-connector.md) voor beschrijvingen van JSON-eigenschappen die worden ondersteund door SqlSink.</span><span class="sxs-lookup"><span data-stu-id="764c2-279">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="764c2-280">Data Factory-entiteiten publiceren/implementeren</span><span class="sxs-lookup"><span data-stu-id="764c2-280">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="764c2-281">In deze stap publiceert u Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="764c2-281">In this step, you publish Data Factory entities (linked services, datasets, and pipeline) you created earlier.</span></span> <span data-ttu-id="764c2-282">U specificeert ook de naam van de nieuwe gegevensfactory die moet worden gemaakt voor deze entiteiten.</span><span class="sxs-lookup"><span data-stu-id="764c2-282">You also specify the name of the new data factory to be created to hold these entities.</span></span>  

1. <span data-ttu-id="764c2-283">Klik met de rechtermuisknop op het project in Solution Explorer. Klik vervolgens op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="764c2-283">Right-click project in the Solution Explorer, and click **Publish**.</span></span> 
2. <span data-ttu-id="764c2-284">Als u het dialoogvenster **Sign in to your Microsoft account** ziet, voert u uw referenties in voor het account met het Azure-abonnement en klikt u op **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="764c2-284">If you see **Sign in to your Microsoft account** dialog box, enter your credentials for the account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="764c2-285">Het volgende dialoogvenster wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="764c2-285">You should see the following dialog box:</span></span>
   
   ![Het dialoogvenster Publish](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. <span data-ttu-id="764c2-287">Op de pagina Configure data factory voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="764c2-287">In the Configure data factory page, do the following steps:</span></span> 
   
   1. <span data-ttu-id="764c2-288">Selecteer **Create New Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="764c2-288">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="764c2-289">Voer **VSTutorialFactory** in als **naam**.</span><span class="sxs-lookup"><span data-stu-id="764c2-289">Enter **VSTutorialFactory** for **Name**.</span></span>  
      
      > [!IMPORTANT]
      > <span data-ttu-id="764c2-290">De naam van de Azure-gegevensfactory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="764c2-290">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="764c2-291">Als u tijdens het publiceren een foutmelding ontvangt over de naam van de gegevensfactory, wijzigt u de naam ervan (naar bijvoorbeeld uwnaamVSTutorialFactory) en publiceert u opnieuw.</span><span class="sxs-lookup"><span data-stu-id="764c2-291">If you receive an error about the name of data factory when publishing, change the name of the data factory (for example, yournameVSTutorialFactory) and try publishing again.</span></span> <span data-ttu-id="764c2-292">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="764c2-292">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>        
      > 
      > 
   3. <span data-ttu-id="764c2-293">Selecteer uw Azure-abonnement voor het veld **Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="764c2-293">Select your Azure subscription for the **Subscription** field.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="764c2-294">Als u geen abonnement niet ziet, controleert u of u bent aangemeld met een account dat een beheerder of co-beheerder is van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="764c2-294">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of the subscription.</span></span>  
      > 
      > 
   4. <span data-ttu-id="764c2-295">Selecteer de **resourcegroep** voor de gegevensfactory die u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="764c2-295">Select the **resource group** for the data factory to be created.</span></span> 
   5. <span data-ttu-id="764c2-296">Selecteer de **regio** voor de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="764c2-296">Select the **region** for the data factory.</span></span> <span data-ttu-id="764c2-297">Alleen regio's die worden ondersteund door de Data Factory-service worden weergegeven in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="764c2-297">Only regions supported by the Data Factory service are shown in the drop-down list.</span></span>
   6. <span data-ttu-id="764c2-298">Klik op **Next** om over te schakelen naar de pagina **Publish Items**.</span><span class="sxs-lookup"><span data-stu-id="764c2-298">Click **Next** to switch to the **Publish Items** page.</span></span>
      
       ![Pagina Data Factory configureren](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. <span data-ttu-id="764c2-300">Op de pagina **Publish Items** controleert u of alle Data Factory-entiteiten zijn geselecteerd en klikt u op **Next** om over te schakelen naar de pagina **Summary**.</span><span class="sxs-lookup"><span data-stu-id="764c2-300">In the **Publish Items** page, ensure that all the Data Factories entities are selected, and click **Next** to switch to the **Summary** page.</span></span>
   
   ![Pagina Items publiceren](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. <span data-ttu-id="764c2-302">Controleer de samenvatting en klik op **Next** om te beginnen met het implementatieproces en om de **implementatiestatus** te bekijken.</span><span class="sxs-lookup"><span data-stu-id="764c2-302">Review the summary and click **Next** to start the deployment process and view the **Deployment Status**.</span></span>
   
   ![Pagina Samenvatting publiceren](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. <span data-ttu-id="764c2-304">Op de pagina **Deployment Status** ziet u de status van het implementatieproces.</span><span class="sxs-lookup"><span data-stu-id="764c2-304">In the **Deployment Status** page, you should see the status of the deployment process.</span></span> <span data-ttu-id="764c2-305">Klik op Finish wanneer de implementatie is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="764c2-305">Click Finish after the deployment is done.</span></span>
 
   ![Pagina Deployment Status](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

<span data-ttu-id="764c2-307">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="764c2-307">Note the following points:</span></span> 

* <span data-ttu-id="764c2-308">Als u de foutmelding 'This subscription is not registered to use namespace Microsoft.DataFactory' ontvangt, voert u een van de volgende stappen uit en probeert u opnieuw te publiceren:</span><span class="sxs-lookup"><span data-stu-id="764c2-308">If you receive the error: "This subscription is not registered to use namespace Microsoft.DataFactory", do one of the following and try publishing again:</span></span> 
  
  * <span data-ttu-id="764c2-309">Voer in Azure PowerShell de volgende opdracht uit om de Data Factory-provider te registreren.</span><span class="sxs-lookup"><span data-stu-id="764c2-309">In Azure PowerShell, run the following command to register the Data Factory provider.</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="764c2-310">U kunt de volgende opdracht uitvoeren om te bevestigen dat de Data Factory-provider is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="764c2-310">You can run the following command to confirm that the Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="764c2-311">Meld u bij de [Azure Portal](https://portal.azure.com) aan met behulp van het Azure-abonnement en navigeer naar een Data Factory-blade of maak een gegevensfactory in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="764c2-311">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="764c2-312">Door deze actie wordt de provider automatisch voor u geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="764c2-312">This action automatically registers the provider for you.</span></span>
* <span data-ttu-id="764c2-313">De naam van de gegevensfactory wordt in de toekomst mogelijk geregistreerd als DNS-naam en wordt daarmee ook voor iedereen zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="764c2-313">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="764c2-314">Als u Data Factory-exemplaren wilt maken, moet u beheerder/co-beheerder van het Azure-abonnement zijn</span><span class="sxs-lookup"><span data-stu-id="764c2-314">To create Data Factory instances, you need to be a admin/co-admin of the Azure subscription</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="764c2-315">De pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="764c2-315">Monitor pipeline</span></span>
<span data-ttu-id="764c2-316">Navigeer naar de startpagina van uw gegevensfactory:</span><span class="sxs-lookup"><span data-stu-id="764c2-316">Navigate to the home page for your data factory:</span></span>

1. <span data-ttu-id="764c2-317">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="764c2-317">Log in to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="764c2-318">Klik op **Meer services** in het linkermenu en op **Gegevensfactory's**.</span><span class="sxs-lookup"><span data-stu-id="764c2-318">Click **More services** on the left menu, and click **Data factories**.</span></span>

    ![Door gegevensfactory’s bladeren](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. <span data-ttu-id="764c2-320">Begin de naam van uw gegevensfactory te typen.</span><span class="sxs-lookup"><span data-stu-id="764c2-320">Start typing the name of your data factory.</span></span>

    ![Naam van gegevensfactory](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. <span data-ttu-id="764c2-322">Klik op uw gegevensfactory in de lijst met resultaten om de startpagina van uw gegevensfactory te bekijken.</span><span class="sxs-lookup"><span data-stu-id="764c2-322">Click your data factory in the results list to see the home page for your data factory.</span></span>

    ![Startpagina van de gegevensfactory](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. <span data-ttu-id="764c2-324">Volg de instructies in [Gegevenssets en pijplijn bewaken](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) voor het bewaken van de pijplijn en gegevenssets die u tijdens deze zelfstudie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="764c2-324">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) to monitor the pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="764c2-325">Visual Studio biedt momenteel geen ondersteuning voor het bewaken van Data Factory-pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="764c2-325">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span> 

## <a name="summary"></a><span data-ttu-id="764c2-326">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="764c2-326">Summary</span></span>
<span data-ttu-id="764c2-327">In deze zelfstudie hebt u een Azure-gegevensfactory gemaakt om gegevens te kopiëren van een Azure-blob naar een Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="764c2-327">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="764c2-328">U hebt Visual Studio gebruikt om de gegevensfactory, gekoppelde services, gegevenssets en pijplijn te maken.</span><span class="sxs-lookup"><span data-stu-id="764c2-328">You used Visual Studio to create the data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="764c2-329">In deze zelfstudie hebt u de volgende hoofdstappen uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="764c2-329">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="764c2-330">U hebt een Azure-**gegevensfactory** gemaakt.</span><span class="sxs-lookup"><span data-stu-id="764c2-330">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="764c2-331">U hebt **gekoppelde services** gemaakt:</span><span class="sxs-lookup"><span data-stu-id="764c2-331">Created **linked services**:</span></span>
   1. <span data-ttu-id="764c2-332">Een gekoppelde **Azure Storage**-service om uw Azure-opslagaccount te koppelen dat invoergegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="764c2-332">An **Azure Storage** linked service to link your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="764c2-333">Een gekoppelde **Azure SQL**-service om uw Azure SQL Database te koppelen die uitvoergegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="764c2-333">An **Azure SQL** linked service to link your Azure SQL database that holds the output data.</span></span> 
3. <span data-ttu-id="764c2-334">U hebt **gegevenssets** gemaakt waarin de invoer- en uitvoergegevens van pijplijnen worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="764c2-334">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="764c2-335">U hebt een **pijplijn** gemaakt met een **kopieeractiviteit** met **BlobSource** als bron en **SqlSink** als sink.</span><span class="sxs-lookup"><span data-stu-id="764c2-335">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span> 

<span data-ttu-id="764c2-336">Zie [Zelfstudie: uw eerste pijplijn maken om gegevens te transformeren met een Hadoop-cluster](data-factory-build-your-first-pipeline.md) voor meer informatie over het gebruik van een HDInsight Hive-activiteit voor het transformeren van gegevens met een Azure HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="764c2-336">To see how to use a HDInsight Hive Activity to transform data by using Azure HDInsight cluster, see [ Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="764c2-337">U kunt twee activiteiten koppelen (de ene activiteit na de andere laten uitvoeren) door de uitvoergegevensset van één activiteit in te stellen als invoergegevensset voor een andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="764c2-337">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="764c2-338">Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="764c2-338">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 

## <a name="view-all-data-factories-in-server-explorer"></a><span data-ttu-id="764c2-339">Alle gegevensfactory’s weergeven in Server Explorer</span><span class="sxs-lookup"><span data-stu-id="764c2-339">View all data factories in Server Explorer</span></span>
<span data-ttu-id="764c2-340">In deze sectie wordt beschreven hoe u Server Explorer in Visual Studio gebruikt voor het weergeven van alle gegevensfactory’s in uw Azure-abonnement en het maken van een Visual Studio-project op basis van een bestaande gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="764c2-340">This section describes how to use the Server Explorer in Visual Studio to view all the data factories in your Azure subscription and create a Visual Studio project based on an existing data factory.</span></span> 

1. <span data-ttu-id="764c2-341">Klik in het menu van **Visual Studio** op **View** en vervolgens op **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="764c2-341">In **Visual Studio**, click **View** on the menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="764c2-342">Vouw in het Server Explorer-venster **Azure** en **Data Factory** uit.</span><span class="sxs-lookup"><span data-stu-id="764c2-342">In the Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="764c2-343">Wanneer u **Sign in to Visual Studio** ziet, voert u het **account** in dat aan uw Azure-abonnement is gekoppeld, en klikt u op **Continue**.</span><span class="sxs-lookup"><span data-stu-id="764c2-343">If you see **Sign in to Visual Studio**, enter the **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="764c2-344">Voer het **wachtwoord** in en klik op **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="764c2-344">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="764c2-345">Visual Studio haalt informatie op uit alle Azure Data Factory’s in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="764c2-345">Visual Studio tries to get information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="764c2-346">U ziet de status van deze bewerking in het venster **Data Factory Task List**.</span><span class="sxs-lookup"><span data-stu-id="764c2-346">You see the status of this operation in the **Data Factory Task List** window.</span></span>

    ![Server Explorer](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a><span data-ttu-id="764c2-348">Een Visual Studio-project maken voor een bestaande gegevensfactory</span><span class="sxs-lookup"><span data-stu-id="764c2-348">Create a Visual Studio project for an existing data factory</span></span>

- <span data-ttu-id="764c2-349">Klik met de rechtermuisknop op een gegevensfactory in Server Explorer en selecteer **Export Data Factory to New Project** om een Visual Studio-project te maken op basis van een bestaande gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="764c2-349">Right-click a data factory in Server Explorer, and select **Export Data Factory to New Project** to create a Visual Studio project based on an existing data factory.</span></span>

    ![Een gegevensfactory exporteren naar een VS-project](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="764c2-351">Data Factory-hulpprogramma's voor Visual Studio bijwerken</span><span class="sxs-lookup"><span data-stu-id="764c2-351">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="764c2-352">Voer de volgende stappen uit om Azure Data Factory-hulpprogramma's voor Visual Studio bij te werken:</span><span class="sxs-lookup"><span data-stu-id="764c2-352">To update Azure Data Factory tools for Visual Studio, do the following steps:</span></span>

1. <span data-ttu-id="764c2-353">Klik in het menu op **Extra** en selecteer **Extensies en updates**.</span><span class="sxs-lookup"><span data-stu-id="764c2-353">Click **Tools** on the menu and select **Extensions and Updates**.</span></span> 
2. <span data-ttu-id="764c2-354">Selecteer **Updates** in het linkerdeelvenster en selecteer vervolgens **Visual Studio-galerie**.</span><span class="sxs-lookup"><span data-stu-id="764c2-354">Select **Updates** in the left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="764c2-355">Selecteer **Azure Data Factory-hulpprogramma's voor Visual Studio** en klik op **Bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="764c2-355">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="764c2-356">Als u deze vermelding niet ziet, beschikt u al over de nieuwste versie van de hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="764c2-356">If you do not see this entry, you already have the latest version of the tools.</span></span> 

## <a name="use-configuration-files"></a><span data-ttu-id="764c2-357">Configuratiebestanden gebruiken</span><span class="sxs-lookup"><span data-stu-id="764c2-357">Use configuration files</span></span>
<span data-ttu-id="764c2-358">U kunt in Visual Studio configuratiebestanden gebruiken om de eigenschappen voor gekoppelde services/tabellen/pijplijnen anders te configureren voor elke omgeving.</span><span class="sxs-lookup"><span data-stu-id="764c2-358">You can use configuration files in Visual Studio to configure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="764c2-359">Overweeg de volgende JSON-definitie te gebruiken voor een gekoppelde Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="764c2-359">Consider the following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="764c2-360">Geef **connectionString** op met verschillende waarden voor accountname en accountkey op basis van de omgeving (ontwikkeling/tests/productie) waarin u Data Factory-entiteiten implementeert.</span><span class="sxs-lookup"><span data-stu-id="764c2-360">To specify **connectionString** with different values for accountname and accountkey based on the environment (Dev/Test/Production) to which you are deploying Data Factory entities.</span></span> <span data-ttu-id="764c2-361">U kunt dit gedrag bewerkstelligen door een afzonderlijk configuratiebestand te gebruiken voor elke omgeving.</span><span class="sxs-lookup"><span data-stu-id="764c2-361">You can achieve this behavior by using separate configuration file for each environment.</span></span>

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

### <a name="add-a-configuration-file"></a><span data-ttu-id="764c2-362">Een configuratiebestand toevoegen</span><span class="sxs-lookup"><span data-stu-id="764c2-362">Add a configuration file</span></span>
<span data-ttu-id="764c2-363">Voeg een configuratiebestand voor elke omgeving toe door de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="764c2-363">Add a configuration file for each environment by performing the following steps:</span></span>   

1. <span data-ttu-id="764c2-364">Klik met de rechtermuisknop op het Data Factory-project in uw Visual Studio-oplossing, houd de muisaanwijzer op **Add** en klik op **New item**.</span><span class="sxs-lookup"><span data-stu-id="764c2-364">Right-click the Data Factory project in your Visual Studio solution, point to **Add**, and click **New item**.</span></span>
2. <span data-ttu-id="764c2-365">Selecteer in de lijst met geïnstalleerde sjablonen aan de linkerkant de optie **Config**, selecteer **Configuration File**, voer een **naam** in voor het configuratiebestand en klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="764c2-365">Select **Config** from the list of installed templates on the left, select **Configuration File**, enter a **name** for the configuration file, and click **Add**.</span></span>

    ![Een configuratiebestand toevoegen](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="764c2-367">Voeg configuratieparameters en de bijbehorende waarden toe in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="764c2-367">Add configuration parameters and their values in the following format:</span></span>

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

    <span data-ttu-id="764c2-368">In dit voorbeeld configureert u de eigenschap connectionString van een gekoppelde Azure Storage-service en een gekoppelde Azure SQL-service.</span><span class="sxs-lookup"><span data-stu-id="764c2-368">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="764c2-369">De syntaxis voor het opgeven van de naam is [JsonPath](http://goessner.net/articles/JsonPath/).</span><span class="sxs-lookup"><span data-stu-id="764c2-369">Notice that the syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="764c2-370">Als JSON een eigenschap heeft met een matrix van waarden zoals in de volgende code wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="764c2-370">If JSON has a property that has an array of values as shown in the following code:</span></span>  

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

    <span data-ttu-id="764c2-371">Eigenschappen configureren zoals wordt weergegeven in het volgende configuratiebestand (gebruik op nul gebaseerde indexering):</span><span class="sxs-lookup"><span data-stu-id="764c2-371">Configure properties as shown in the following configuration file (use zero-based indexing):</span></span>

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

### <a name="property-names-with-spaces"></a><span data-ttu-id="764c2-372">Eigenschapnamen met spaties</span><span class="sxs-lookup"><span data-stu-id="764c2-372">Property names with spaces</span></span>
<span data-ttu-id="764c2-373">Als de naam van een eigenschap spaties bevat, gebruikt u vierkante haken, zoals in het volgende voorbeeld wordt weergegeven (databaseservernaam):</span><span class="sxs-lookup"><span data-stu-id="764c2-373">If a property name has spaces in it, use square brackets as shown in the following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="764c2-374">Een oplossing implementeren met behulp van een configuratie</span><span class="sxs-lookup"><span data-stu-id="764c2-374">Deploy solution using a configuration</span></span>
<span data-ttu-id="764c2-375">Wanneer u Azure Data Factory-entiteiten publiceert in de VS, kunt u opgeven welke configuratie u voor die publicatiebewerking wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="764c2-375">When you are publishing Azure Data Factory entities in VS, you can specify the configuration that you want to use for that publishing operation.</span></span>

<span data-ttu-id="764c2-376">Entiteiten publiceren in een Azure Data Factory-project via een configuratiebestand:</span><span class="sxs-lookup"><span data-stu-id="764c2-376">To publish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="764c2-377">Klik met de rechtermuisknop op het Data Factory-project en klik op **Publish** om het dialoogvenster **Publish Items** weer te geven.</span><span class="sxs-lookup"><span data-stu-id="764c2-377">Right-click Data Factory project and click **Publish** to see the **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="764c2-378">Selecteer een bestaande gegevensfactory of geef op de pagina **Configure data factory** waarden op voor het maken van een nieuwe gegevensfactory. Klik vervolgens op **Next**.</span><span class="sxs-lookup"><span data-stu-id="764c2-378">Select an existing data factory or specify values for creating a data factory on the **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="764c2-379">Op de pagina **Publish Items**: u ziet een vervolgkeuzelijst met beschikbare configuraties voor het veld **Select Deployment Config**.</span><span class="sxs-lookup"><span data-stu-id="764c2-379">On the **Publish Items** page: you see a drop-down list with available configurations for the **Select Deployment Config** field.</span></span>

    ![Een configuratiebestand selecteren](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="764c2-381">Selecteer het **configuratiebestand** dat u wilt gebruiken en klik op **Next**.</span><span class="sxs-lookup"><span data-stu-id="764c2-381">Select the **configuration file** that you would like to use and click **Next**.</span></span>
5. <span data-ttu-id="764c2-382">Controleer of u de naam van het JSON-bestand ziet op de pagina **Summary** en klik op **Next**.</span><span class="sxs-lookup"><span data-stu-id="764c2-382">Confirm that you see the name of JSON file in the **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="764c2-383">Klik op **Finish** nadat de implementatiebewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="764c2-383">Click **Finish** after the deployment operation is finished.</span></span>

<span data-ttu-id="764c2-384">Tijdens de implementatie worden de waarden van het configuratiebestand gebruikt voor de eigenschappen in de JSON-bestanden voor Data Factory-entiteiten voordat de entiteiten worden geïmplementeerd in de Azure Data Factory-service.</span><span class="sxs-lookup"><span data-stu-id="764c2-384">When you deploy, the values from the configuration file are used to set values for properties in the JSON files before the entities are deployed to Azure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="764c2-385">Azure Key Vault gebruiken</span><span class="sxs-lookup"><span data-stu-id="764c2-385">Use Azure Key Vault</span></span>
<span data-ttu-id="764c2-386">Het wordt niet aangeraden en het is vaak in strijd met het beveiligingsbeleid om gevoelige gegevens, zoals verbindingsreeksen, op te slaan in de codeopslagplaats.</span><span class="sxs-lookup"><span data-stu-id="764c2-386">It is not advisable and often against security policy to commit sensitive data such as connection strings to the code repository.</span></span> <span data-ttu-id="764c2-387">Zie het voorbeeld [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) op GitHub voor meer informatie over de opslag van vertrouwelijke gegevens in Azure Key Vault en het gebruik daarvan tijdens de publicatie van Data Factory-entiteiten.</span><span class="sxs-lookup"><span data-stu-id="764c2-387">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub to learn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="764c2-388">Met de extensie Secure Publish voor Visual Studio kunnen de geheimen worden opgeslagen in Key Vault en worden alleen verwijzingen naar deze geheimen opgegeven in de gekoppelde services/implementatieconfiguraties.</span><span class="sxs-lookup"><span data-stu-id="764c2-388">The Secure Publish extension for Visual Studio allows the secrets to be stored in Key Vault and only references to them are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="764c2-389">Deze verwijzingen worden opgelost wanneer u Data Factory-entiteiten publiceert naar Azure.</span><span class="sxs-lookup"><span data-stu-id="764c2-389">These references are resolved when you publish Data Factory entities to Azure.</span></span> <span data-ttu-id="764c2-390">Deze bestanden kunnen vervolgens worden doorgevoerd naar een bronopslagplaats zonder dat er geheimen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="764c2-390">These files can then be committed to source repository without exposing any secrets.</span></span>


## <a name="next-steps"></a><span data-ttu-id="764c2-391">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="764c2-391">Next steps</span></span>
<span data-ttu-id="764c2-392">In deze zelfstudie hebt u voor een kopieerbewerking een Azure Blob-opslag gebruikt als brongegevensarchief en een Azure SQL-database als doelgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="764c2-392">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="764c2-393">De volgende tabel bevat een lijst met gegevensarchieven die worden ondersteund als bron en doel voor de kopieeractiviteit:</span><span class="sxs-lookup"><span data-stu-id="764c2-393">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="764c2-394">Klik op de koppeling voor de gegevensopslag in de tabel voor meer informatie over het kopiëren van gegevens naar/uit een gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="764c2-394">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>