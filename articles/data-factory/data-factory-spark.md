---
title: Aanroepen van Spark-programma's van Azure Data Factory | Microsoft Docs
description: Informatie over het aanroepen van Spark-programma's van een Azure data factory met behulp van de MapReduce-activiteit.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 57894bbdd9208f8c32eb65e29f04e2ae723780ca
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="cf908-103">Spark-programma's van Azure Data Factory-pijplijnen aanroepen</span><span class="sxs-lookup"><span data-stu-id="cf908-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="cf908-104">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="cf908-104">Hive Activity</span></span>](data-factory-hive-activity.md)
> * [<span data-ttu-id="cf908-105">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="cf908-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="cf908-106">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="cf908-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="cf908-107">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="cf908-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="cf908-108">Spark-activiteit</span><span class="sxs-lookup"><span data-stu-id="cf908-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="cf908-109">Machine Learning-batchuitvoeringsactiviteit</span><span class="sxs-lookup"><span data-stu-id="cf908-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="cf908-110">Machine Learning-activiteit resources bijwerken</span><span class="sxs-lookup"><span data-stu-id="cf908-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="cf908-111">Opgeslagen procedureactiviteit</span><span class="sxs-lookup"><span data-stu-id="cf908-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="cf908-112">Data Lake Analytics U-SQL-activiteit</span><span class="sxs-lookup"><span data-stu-id="cf908-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="cf908-113">Aangepaste activiteit .NET</span><span class="sxs-lookup"><span data-stu-id="cf908-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="cf908-114">Inleiding</span><span class="sxs-lookup"><span data-stu-id="cf908-114">Introduction</span></span>
<span data-ttu-id="cf908-115">Spark-activiteit is een van de [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) ondersteund door Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="cf908-115">Spark Activity is one of the [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span></span> <span data-ttu-id="cf908-116">Deze activiteit wordt het opgegeven Spark-programma uitgevoerd op uw Apache Spark-cluster in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cf908-116">This activity runs the specified Spark program on your Apache Spark cluster in Azure HDInsight.</span></span>    

> [!IMPORTANT]
> - <span data-ttu-id="cf908-117">Spark activiteit biedt geen ondersteuning voor HDInsight Spark-clusters die gebruikmaken van een Azure Data Lake Store als primaire opslag.</span><span class="sxs-lookup"><span data-stu-id="cf908-117">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
> - <span data-ttu-id="cf908-118">Spark-activiteit ondersteunt alleen bestaande (uw eigen) HDInsight Spark-clusters.</span><span class="sxs-lookup"><span data-stu-id="cf908-118">Spark Activity supports only existing (your own) HDInsight Spark clusters.</span></span> <span data-ttu-id="cf908-119">Een gekoppelde HDInsight-service op aanvraag worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="cf908-119">It does not support an on-demand HDInsight linked service.</span></span>

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a><span data-ttu-id="cf908-120">Overzicht: een pijplijn maken met Spark-activiteit</span><span class="sxs-lookup"><span data-stu-id="cf908-120">Walkthrough: create a pipeline with Spark activity</span></span>
<span data-ttu-id="cf908-121">Hier volgen de gebruikelijke stappen voor het maken van een Data Factory-pijplijn met een Spark-activiteit.</span><span class="sxs-lookup"><span data-stu-id="cf908-121">Here are the typical steps to create a Data Factory pipeline with a Spark activity.</span></span>  

1. <span data-ttu-id="cf908-122">Maak een gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="cf908-122">Create a data factory.</span></span>
2. <span data-ttu-id="cf908-123">Maak een gekoppelde Azure Storage-service om te koppelen van uw Azure-opslag die is gekoppeld aan uw HDInsight Spark-cluster aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="cf908-123">Create an Azure Storage linked service to link your Azure storage that is associated with your HDInsight Spark cluster to the data factory.</span></span>     
2. <span data-ttu-id="cf908-124">Maak een gekoppelde HDInsight-service als u wilt uw Apache Spark-cluster in Azure HDInsight koppelen aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="cf908-124">Create an Azure HDInsight linked service to link your Apache Spark cluster in Azure HDInsight to the data factory.</span></span>
3. <span data-ttu-id="cf908-125">Maak een gegevensset die naar de gekoppelde Azure Storage-service verwijst.</span><span class="sxs-lookup"><span data-stu-id="cf908-125">Create a dataset that refers to the Azure Storage linked service.</span></span> <span data-ttu-id="cf908-126">U moet een uitvoergegevensset voor een activiteit op dit moment kunt opgeven, zelfs als er wordt geen uitvoer wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="cf908-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span>  
4. <span data-ttu-id="cf908-127">Een pijplijn maken met Spark-activiteit die naar de gekoppelde HDInsight-service in #2 hebt gemaakt verwijst.</span><span class="sxs-lookup"><span data-stu-id="cf908-127">Create a pipeline with Spark activity that refers to the HDInsight linked service created in #2.</span></span> <span data-ttu-id="cf908-128">De activiteit is geconfigureerd met de gegevensset die u hebt gemaakt in de vorige stap als een uitvoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="cf908-128">The activity is configured with the dataset you created in the previous step as an output dataset.</span></span> <span data-ttu-id="cf908-129">De uitvoergegevensset is uitvoergegevensset het schema (elk uur, dagelijks, enz.).</span><span class="sxs-lookup"><span data-stu-id="cf908-129">The output dataset is what drives the schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="cf908-130">Daarom moet u de uitvoergegevensset opgeven, zelfs als de activiteit geen echt uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="cf908-130">Therefore, you must specify the output dataset even though the activity does not really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="cf908-131">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cf908-131">Prerequisites</span></span>
1. <span data-ttu-id="cf908-132">Maak een **voor algemene doeleinden Azure Storage-Account** door de instructies te volgen in het overzicht: [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="cf908-132">Create a **general-purpose Azure Storage Account** by following instructions in the walkthrough: [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
2. <span data-ttu-id="cf908-133">Maak een **Apache Spark-cluster in Azure HDInsight** door de instructies in de zelfstudie te volgen: [maken Apache Spark-cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="cf908-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in the tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="cf908-134">Koppel de Azure storage-account dat u hebt gemaakt in stap 1 van # met dit cluster.</span><span class="sxs-lookup"><span data-stu-id="cf908-134">Associate the Azure storage account you created in step #1 with this cluster.</span></span>  
3. <span data-ttu-id="cf908-135">Downloaden en bekijken van het scriptbestand python **test.py** vinden op: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span><span class="sxs-lookup"><span data-stu-id="cf908-135">Download and review the python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>  
3.  <span data-ttu-id="cf908-136">Uploaden **test.py** naar de **pyFiles** map in de **adfspark** container in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="cf908-136">Upload **test.py** to the **pyFiles** folder in the **adfspark** container in your Azure Blob storage.</span></span> <span data-ttu-id="cf908-137">De container en de map maken als ze bestaan niet.</span><span class="sxs-lookup"><span data-stu-id="cf908-137">Create the container and the folder if they do not exist.</span></span>

### <a name="create-data-factory"></a><span data-ttu-id="cf908-138">Een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="cf908-138">Create data factory</span></span>
<span data-ttu-id="cf908-139">U begint in deze stap met het maken van de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="cf908-139">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="cf908-140">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cf908-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="cf908-141">Klik op **NIEUW** in het linkermenu en klik vervolgens op **Gegevens en analyses** en **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="cf908-141">Click **NEW** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="cf908-142">In de **nieuwe gegevensfactory** blade Voer **SparkDF** voor de naam.</span><span class="sxs-lookup"><span data-stu-id="cf908-142">In the **New data factory** blade, enter **SparkDF** for the Name.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="cf908-143">De naam van de Azure-gegevensfactory moet **wereldwijd uniek** zijn.</span><span class="sxs-lookup"><span data-stu-id="cf908-143">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="cf908-144">Als u de volgende fout: **Data factory-naam 'SparkDF' is niet beschikbaar**.</span><span class="sxs-lookup"><span data-stu-id="cf908-144">If you see the error: **Data factory name “SparkDF” is not available**.</span></span> <span data-ttu-id="cf908-145">Wijzig de naam van de gegevensfactory (bijvoorbeeld yournameSparkDFdate en probeer het opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="cf908-145">Change the name of the data factory (for example, yournameSparkDFdate, and try creating again.</span></span> <span data-ttu-id="cf908-146">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="cf908-146">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
4. <span data-ttu-id="cf908-147">Selecteer het **Azure-abonnement** waarvoor u de gegevensfactory wilt maken.</span><span class="sxs-lookup"><span data-stu-id="cf908-147">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="cf908-148">Selecteer een bestaande **resourcegroep** of maak een Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="cf908-148">Select an existing **resource group** or create an Azure resource group.</span></span>
6. <span data-ttu-id="cf908-149">Selecteer **vastmaken aan dashboard** optie.</span><span class="sxs-lookup"><span data-stu-id="cf908-149">Select **Pin to dashboard** option.</span></span>  
6. <span data-ttu-id="cf908-150">Klik op de blade **Nieuwe gegevensfactory** op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="cf908-150">Click **Create** on the **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="cf908-151">Als u Data Factory-exemplaren wilt maken, moet u lid zijn van de rol [Inzender Data Factory](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) op abonnements-/resourcegroepsniveau.</span><span class="sxs-lookup"><span data-stu-id="cf908-151">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
7. <span data-ttu-id="cf908-152">U ziet de gegevensfactory wordt gemaakt in de **dashboard** van de Azure portal als volgt:</span><span class="sxs-lookup"><span data-stu-id="cf908-152">You see the data factory being created in the **dashboard** of the Azure portal as follows:</span></span>   
8. <span data-ttu-id="cf908-153">Nadat de gegevensfactory is gemaakt, ziet u de gegevensfactorypagina. Hierop wordt de inhoud van de gegevensfactory weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cf908-153">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span> <span data-ttu-id="cf908-154">Als u de data factory-pagina niet ziet, klikt u op de tegel voor uw gegevensfactory op het dashboard.</span><span class="sxs-lookup"><span data-stu-id="cf908-154">If you do not see the data factory page, click the tile for your data factory on the dashboard.</span></span>

    ![Blade Gegevensfactory](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="cf908-156">Gekoppelde services maken</span><span class="sxs-lookup"><span data-stu-id="cf908-156">Create linked services</span></span>
<span data-ttu-id="cf908-157">In deze stap maakt u twee gekoppelde services, een Spark-cluster koppelen aan uw gegevensfactory en de andere met uw Azure-opslag te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="cf908-157">In this step, you create two linked services, one to link your Spark cluster to your data factory, and the other to link your Azure storage to your data factory.</span></span>  

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="cf908-158">Een gekoppelde Azure Storage-service maken</span><span class="sxs-lookup"><span data-stu-id="cf908-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="cf908-159">In deze stap koppelt u uw Azure Storage-account aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="cf908-159">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="cf908-160">Een gegevensset die u in een stap verderop in dit overzicht maakt verwijst naar deze gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="cf908-160">A dataset you create in a step later in this walkthrough refers to this linked service.</span></span> <span data-ttu-id="cf908-161">De gekoppelde HDInsight-service die u in de volgende stap definieert verwijst te naar deze gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="cf908-161">The HDInsight linked service that you define in the next step refers to this linked service too.</span></span>  

1. <span data-ttu-id="cf908-162">Klik op **auteur en implementeren van** op de **Data Factory** blade van uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="cf908-162">Click **Author and deploy** on the **Data Factory** blade for your data factory.</span></span> <span data-ttu-id="cf908-163">U krijgt de Data Factory-editor te zien.</span><span class="sxs-lookup"><span data-stu-id="cf908-163">You should see the Data Factory Editor.</span></span>
2. <span data-ttu-id="cf908-164">Klik op **Nieuwe gegevensopslag** en kies **Azure-opslag**.</span><span class="sxs-lookup"><span data-stu-id="cf908-164">Click **New data store** and choose **Azure storage**.</span></span>

   ![Nieuwe gegevensopslag - Azure Storage - menu](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="cf908-166">U ziet de **JSON-script** voor het maken van een Azure Storage gekoppelde service in de editor.</span><span class="sxs-lookup"><span data-stu-id="cf908-166">You should see the **JSON script** for creating an Azure Storage linked service in the editor.</span></span>

   ![Een gekoppelde Azure Storage-service](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="cf908-168">Vervang **accountnaam** en **accountsleutel** met de naam en toegangssleutel van uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="cf908-168">Replace **account name** and **account key** with the name and access key of your Azure storage account.</span></span> <span data-ttu-id="cf908-169">Raadpleeg de informatie over het weergeven, kopiëren en opnieuw genereren van toegangssleutels voor opslag in [Uw opslagaccount beheren](../storage/common/storage-create-storage-account.md#manage-your-storage-account) als u meer wilt weten over het verkrijgen van een toegangssleutel voor opslag.</span><span class="sxs-lookup"><span data-stu-id="cf908-169">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="cf908-170">Voor het implementeren van de gekoppelde service, klikt u op **implementeren** op de opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="cf908-170">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="cf908-171">Wanneer de gekoppelde service is geïmplementeerd, verdwijnt het venster **Draft-1** en ziet u **AzureStorageLinkedService** in de structuurweergave links.</span><span class="sxs-lookup"><span data-stu-id="cf908-171">After the linked service is deployed successfully, the **Draft-1** window should disappear and you see **AzureStorageLinkedService** in the tree view on the left.</span></span>

#### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="cf908-172">Een gekoppelde HDInsight-service maken</span><span class="sxs-lookup"><span data-stu-id="cf908-172">Create HDInsight linked service</span></span>
<span data-ttu-id="cf908-173">In deze stap maakt u een gekoppelde HDInsight-service als u wilt uw HDInsight Spark-cluster koppelen aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="cf908-173">In this step, you create Azure HDInsight linked service to link your HDInsight Spark cluster to the data factory.</span></span> <span data-ttu-id="cf908-174">Het HDInsight-cluster wordt gebruikt voor het programma Spark is opgegeven in de Spark-activiteit van de pijplijn in dit voorbeeld uitvoert.</span><span class="sxs-lookup"><span data-stu-id="cf908-174">The HDInsight cluster is used to run the Spark program specified in the Spark activity of the pipeline in this sample.</span></span>  

1. <span data-ttu-id="cf908-175">Klik op **... Meer** op de werkbalk klikt **nieuwe berekening**, en klik vervolgens op **HDInsight-cluster**.</span><span class="sxs-lookup"><span data-stu-id="cf908-175">Click **... More** on the toolbar, click **New compute**, and then click **HDInsight cluster**.</span></span>

    ![Een gekoppelde HDInsight-service maken](media/data-factory-spark/new-hdinsight-linked-service.png)
2. <span data-ttu-id="cf908-177">Kopieer het onderstaande codefragment en plak het in het venster **Draft-1**.</span><span class="sxs-lookup"><span data-stu-id="cf908-177">Copy and paste the following snippet to the **Draft-1** window.</span></span> <span data-ttu-id="cf908-178">Voer de volgende stappen uit in de JSON-editor:</span><span class="sxs-lookup"><span data-stu-id="cf908-178">In the JSON editor, do the following steps:</span></span>
    1. <span data-ttu-id="cf908-179">Geef de **URI** voor het HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="cf908-179">Specify the **URI** for the HDInsight Spark cluster.</span></span> <span data-ttu-id="cf908-180">Bijvoorbeeld: `https://<sparkclustername>.azurehdinsight.net/`.</span><span class="sxs-lookup"><span data-stu-id="cf908-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span>
    2. <span data-ttu-id="cf908-181">Geef de naam van de **gebruiker** wie toegang heeft tot het Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="cf908-181">Specify the name of the **user** who has access to the Spark cluster.</span></span>
    3. <span data-ttu-id="cf908-182">Geef de **wachtwoord** voor de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="cf908-182">Specify the **password** for user.</span></span>
    4. <span data-ttu-id="cf908-183">Geef de **gekoppelde Azure Storage-service** dat is gekoppeld aan de HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="cf908-183">Specify the **Azure Storage linked service** that is associated with the HDInsight Spark cluster.</span></span> <span data-ttu-id="cf908-184">In dit voorbeeld is: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="cf908-184">In this example, it is: **AzureStorageLinkedService**.</span></span>

    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - <span data-ttu-id="cf908-185">Spark activiteit biedt geen ondersteuning voor HDInsight Spark-clusters die gebruikmaken van een Azure Data Lake Store als primaire opslag.</span><span class="sxs-lookup"><span data-stu-id="cf908-185">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
    > - <span data-ttu-id="cf908-186">Spark-activiteit ondersteunt alleen bestaande (uw eigen) HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="cf908-186">Spark Activity supports only existing (your own) HDInsight Spark cluster.</span></span> <span data-ttu-id="cf908-187">Een gekoppelde HDInsight-service op aanvraag worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="cf908-187">It does not support an on-demand HDInsight linked service.</span></span>

    <span data-ttu-id="cf908-188">Zie [gekoppelde HDInsight-Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) voor meer informatie over de HDInsight gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="cf908-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about the HDInsight linked service.</span></span>
3.  <span data-ttu-id="cf908-189">Voor het implementeren van de gekoppelde service, klikt u op **implementeren** op de opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="cf908-189">To deploy the linked service, click **Deploy** on the command bar.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="cf908-190">Uitvoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="cf908-190">Create output dataset</span></span>
<span data-ttu-id="cf908-191">De uitvoergegevensset is uitvoergegevensset het schema (elk uur, dagelijks, enz.).</span><span class="sxs-lookup"><span data-stu-id="cf908-191">The output dataset is what drives the schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="cf908-192">U moet daarom een uitvoergegevensset voor de activiteit spark in de pijplijn opgeven, zelfs als de activiteit geen echt geen uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="cf908-192">Therefore, you must specify an output dataset for the spark activity in the pipeline even though the activity does not really produce any output.</span></span> <span data-ttu-id="cf908-193">Het opgeven van een invoergegevensset voor de activiteit is optioneel.</span><span class="sxs-lookup"><span data-stu-id="cf908-193">Specifying an input dataset for the activity is optional.</span></span>

1. <span data-ttu-id="cf908-194">Klik in de **Data Factory-editor** op **... Meer** op de opdrachtbalk, klik op **Nieuwe gegevensset** en selecteer **Azure-blobopslag**.</span><span class="sxs-lookup"><span data-stu-id="cf908-194">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="cf908-195">Kopieer het onderstaande codefragment en plak het in het venster Draft-1.</span><span class="sxs-lookup"><span data-stu-id="cf908-195">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="cf908-196">Het JSON-fragment een gegevensset met de naam definieert **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="cf908-196">The JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="cf908-197">Bovendien u opgeven dat de resultaten worden opgeslagen in de blob-container aangeroepen **adfspark** en de map met de naam **pyFiles/uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="cf908-197">In addition, you specify that the results are stored in the blob container called **adfspark** and the folder called **pyFiles/output**.</span></span> <span data-ttu-id="cf908-198">Zoals eerder vermeld, is deze gegevensset een dummy-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="cf908-198">As mentioned earlier, this dataset is a dummy dataset.</span></span> <span data-ttu-id="cf908-199">De Spark-programma in dit voorbeeld heeft geen uitvoer wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="cf908-199">The Spark program in this example does not produce any output.</span></span> <span data-ttu-id="cf908-200">De **beschikbaarheid** sectie geeft aan dat de uitvoergegevensset die dagelijks wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="cf908-200">The **availability** section specifies that the output dataset is produced daily.</span></span>  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": "\t"
                }
            },
            "availability": {
                "frequency": "Day",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="cf908-201">Voor het implementeren van de gegevensset, klikt u op **implementeren** op de opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="cf908-201">To deploy the dataset, click **Deploy** on the command bar.</span></span>


### <a name="create-pipeline"></a><span data-ttu-id="cf908-202">Pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="cf908-202">Create pipeline</span></span>
<span data-ttu-id="cf908-203">In deze stap maakt u een pijplijn met een **HDInsightSpark** activiteit.</span><span class="sxs-lookup"><span data-stu-id="cf908-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span></span> <span data-ttu-id="cf908-204">Op dit moment wordt de planning gebaseerd op de uitvoergegevensset. Daarom moet u ook een uitvoergegevensset maken als er tijdens de activiteit geen uitvoer wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="cf908-204">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="cf908-205">Als er voor de activiteit geen invoer nodig is, kunt u het maken van de invoergegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="cf908-205">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="cf908-206">Daarom is geen invoergegevensset opgegeven in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="cf908-206">Therefore, no input dataset is specified in this example.</span></span>

1. <span data-ttu-id="cf908-207">In de **Data Factory-Editor**, klikt u op **... Meer** op de opdrachtbalk en klik vervolgens op **nieuwe pijplijn**.</span><span class="sxs-lookup"><span data-stu-id="cf908-207">In the **Data Factory Editor**, click **… More** on the command bar, and then click **New pipeline**.</span></span>
2. <span data-ttu-id="cf908-208">Het script in het venster Draft-1 vervangen door het volgende script:</span><span class="sxs-lookup"><span data-stu-id="cf908-208">Replace the script in the Draft-1 window with the following script:</span></span>

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    <span data-ttu-id="cf908-209">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="cf908-209">Note the following points:</span></span>
    - <span data-ttu-id="cf908-210">De **type** eigenschap is ingesteld op **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="cf908-210">The **type** property is set to **HDInsightSpark**.</span></span>
    - <span data-ttu-id="cf908-211">De **rootPath** is ingesteld op **adfspark\\pyFiles** waarbij adfspark Azure Blob-container en pyFiles fijn map in de container.</span><span class="sxs-lookup"><span data-stu-id="cf908-211">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="cf908-212">In dit voorbeeld is de Azure Blob-opslag die is gekoppeld aan het Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="cf908-212">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="cf908-213">U kunt het bestand uploaden naar een andere Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="cf908-213">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="cf908-214">Als u doet dit, maakt u een gekoppelde Azure Storage-service als u wilt dat storage-account koppelen aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="cf908-214">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="cf908-215">Geef de naam van de gekoppelde service als een waarde voor de **sparkJobLinkedService** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="cf908-215">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="cf908-216">Zie [Spark activiteitseigenschappen](#spark-activity-properties) voor meer informatie over deze eigenschap en andere eigenschappen die ondersteund worden door de activiteit Spark.</span><span class="sxs-lookup"><span data-stu-id="cf908-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>  
    - <span data-ttu-id="cf908-217">De **entryFilePath** is ingesteld op de **test.py**, namelijk het python-bestand.</span><span class="sxs-lookup"><span data-stu-id="cf908-217">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span>
    - <span data-ttu-id="cf908-218">De **getDebugInfo** eigenschap is ingesteld op **altijd**, wat betekent dat de logboekbestanden altijd zijn gegenereerd (slagen of mislukken).</span><span class="sxs-lookup"><span data-stu-id="cf908-218">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="cf908-219">Het is raadzaam dat u deze eigenschap niet instellen op `Always` in een productieomgeving tenzij u een probleem wilt oplossen.</span><span class="sxs-lookup"><span data-stu-id="cf908-219">We recommend that you do not set this property to `Always` in a production environment unless you are troubleshooting an issue.</span></span>
    - <span data-ttu-id="cf908-220">De **levert** sectie heeft één uitvoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="cf908-220">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="cf908-221">U kunt een uitvoergegevensset moet opgeven, zelfs als het programma spark geen uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="cf908-221">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="cf908-222">De uitvoergegevensset stations de planning voor de pijplijn (elk uur, dagelijks, enz.).</span><span class="sxs-lookup"><span data-stu-id="cf908-222">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>  

        <span data-ttu-id="cf908-223">Zie voor meer informatie over de eigenschappen die worden ondersteund door de activiteit Spark [activiteitseigenschappen Spark](#spark-activity-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="cf908-223">For details about the properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span></span>
3. <span data-ttu-id="cf908-224">Voor het implementeren van de pijplijn, klikt u op **implementeren** op de opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="cf908-224">To deploy the pipeline, click **Deploy** on the command bar.</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="cf908-225">De pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="cf908-225">Monitor pipeline</span></span>
1. <span data-ttu-id="cf908-226">Klik op **X** blades Data Factory-Editor sluiten en terug naar de startpagina van de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="cf908-226">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory home page.</span></span> <span data-ttu-id="cf908-227">Klik op **bewaken en beheren** om de bewaking toepassing in een ander tabblad te starten.</span><span class="sxs-lookup"><span data-stu-id="cf908-227">Click **Monitor and Manage** to launch the monitoring application in another tab.</span></span>

    ![Bewaken en beheren van de tegel](media/data-factory-spark/monitor-and-manage-tile.png)
2. <span data-ttu-id="cf908-229">Wijzig de **begintijd** filter boven aan **2/1/2017**, en klik op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="cf908-229">Change the **Start time** filter at the top to **2/1/2017**, and click **Apply**.</span></span>
3. <span data-ttu-id="cf908-230">Als er slechts één dag tussen het begin (2017-02-01)- en eindtijden (2017-02-02) van de pijplijn is, moet u slechts één activiteitvenster zien.</span><span class="sxs-lookup"><span data-stu-id="cf908-230">You should see only one activity window as there is only one day between the start (2017-02-01) and end times (2017-02-02) of the pipeline.</span></span> <span data-ttu-id="cf908-231">Controleer of het gegevenssegment **gereed** status.</span><span class="sxs-lookup"><span data-stu-id="cf908-231">Confirm that the data slice is in **ready** state.</span></span>

    ![De pijplijn bewaken](media/data-factory-spark/monitor-and-manage-app.png)    
4. <span data-ttu-id="cf908-233">Selecteer de **activiteitvenster** voor informatie over de activiteit die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cf908-233">Select the **activity window** to see details about the activity run.</span></span> <span data-ttu-id="cf908-234">Als er een fout is, ziet u informatie over het in het rechterdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="cf908-234">If there is an error, you see details about it in the right pane.</span></span>

### <a name="verify-the-results"></a><span data-ttu-id="cf908-235">De resultaten controleren</span><span class="sxs-lookup"><span data-stu-id="cf908-235">Verify the results</span></span>

1. <span data-ttu-id="cf908-236">Start **Jupyter-notebook** voor uw HDInsight Spark-cluster door te navigeren naar: https://CLUSTERNAME.azurehdinsight.NET/jupyter.</span><span class="sxs-lookup"><span data-stu-id="cf908-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="cf908-237">U kunt ook starten cluster-dashboard voor uw HDInsight Spark-cluster en start vervolgens **Jupyter-Notebook**.</span><span class="sxs-lookup"><span data-stu-id="cf908-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span></span>
2. <span data-ttu-id="cf908-238">Klik op **nieuw** -> **PySpark** starten van een nieuwe notebook.</span><span class="sxs-lookup"><span data-stu-id="cf908-238">Click **New** -> **PySpark** to start a new notebook.</span></span>

    ![Nieuwe Jupyter-notebook](media/data-factory-spark/jupyter-new-book.png)
3. <span data-ttu-id="cf908-240">Voer de volgende opdracht door de tekst kopiëren/plakken en drukt u op **SHIFT + ENTER** aan het einde van de tweede instructie.</span><span class="sxs-lookup"><span data-stu-id="cf908-240">Run the following command by copy/pasting the text and pressing **SHIFT + ENTER** at the end of the second statement.</span></span>  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. <span data-ttu-id="cf908-241">Controleer of u de gegevens uit de tabel hvac:</span><span class="sxs-lookup"><span data-stu-id="cf908-241">Confirm that you see the data from the hvac table:</span></span>  

    ![Jupyter-queryresultaten](media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="cf908-243">Zie [een Spark SQL-query uitvoeren](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) gedeelte voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cf908-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) section for detailed instructions.</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="cf908-244">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="cf908-244">Troubleshooting</span></span>
<span data-ttu-id="cf908-245">Aangezien u ingesteld **getDebugInfo** naar **altijd**, ziet u een **logboek** submap in de **pyFiles** map in uw Azure Blob-container.</span><span class="sxs-lookup"><span data-stu-id="cf908-245">Since you set **getDebugInfo** to **Always**, you see a **log** subfolder in the **pyFiles** folder in your Azure Blob container.</span></span> <span data-ttu-id="cf908-246">Het logboekbestand in de logboekmap biedt aanvullende informatie.</span><span class="sxs-lookup"><span data-stu-id="cf908-246">The log file in the log folder provides additional details.</span></span> <span data-ttu-id="cf908-247">Dit logboekbestand is vooral nuttig wanneer er een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="cf908-247">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="cf908-248">In een productieomgeving kunt u instellen op **fout**.</span><span class="sxs-lookup"><span data-stu-id="cf908-248">In a production environment, you may want to set it to **Failure**.</span></span>

<span data-ttu-id="cf908-249">Ga voor meer informatie over de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="cf908-249">For further troubleshooting, do the following steps:</span></span>


1. <span data-ttu-id="cf908-250">Navigeer naar `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span><span class="sxs-lookup"><span data-stu-id="cf908-250">Navigate to `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![Gebruikersinterface van YARN-toepassing](media/data-factory-spark/yarnui-application.png)  
2. <span data-ttu-id="cf908-252">Klik op **logboeken** probeert om een van de uitvoering.</span><span class="sxs-lookup"><span data-stu-id="cf908-252">Click **Logs** for one of the run attempts.</span></span>

    ![Toepassingspagina](media/data-factory-spark/yarn-applications.png)
3. <span data-ttu-id="cf908-254">Hier ziet u aanvullende foutinformatie in de pagina.</span><span class="sxs-lookup"><span data-stu-id="cf908-254">You should see additional error information in the log page.</span></span>

    ![Fout in logboek](media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="cf908-256">De volgende secties bevatten informatie over Data Factory-entiteiten met Apache Spark-cluster en Spark-activiteit in uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="cf908-256">The following sections provide information about Data Factory entities to use Apache Spark cluster and Spark Activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="cf908-257">Spark-activiteitseigenschappen</span><span class="sxs-lookup"><span data-stu-id="cf908-257">Spark activity properties</span></span>
<span data-ttu-id="cf908-258">Hier volgt de voorbeeld-JSON-definitie van een pijplijn met Spark-activiteit:</span><span class="sxs-lookup"><span data-stu-id="cf908-258">Here is the sample JSON definition of a pipeline with Spark Activity:</span></span>    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes the Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

<span data-ttu-id="cf908-259">De volgende tabel beschrijft de JSON-eigenschappen die in de JSON-definitie:</span><span class="sxs-lookup"><span data-stu-id="cf908-259">The following table describes the JSON properties used in the JSON definition:</span></span>

| <span data-ttu-id="cf908-260">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="cf908-260">Property</span></span> | <span data-ttu-id="cf908-261">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cf908-261">Description</span></span> | <span data-ttu-id="cf908-262">Vereist</span><span class="sxs-lookup"><span data-stu-id="cf908-262">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="cf908-263">naam</span><span class="sxs-lookup"><span data-stu-id="cf908-263">name</span></span> | <span data-ttu-id="cf908-264">De naam van de activiteit in de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="cf908-264">Name of the activity in the pipeline.</span></span> | <span data-ttu-id="cf908-265">Ja</span><span class="sxs-lookup"><span data-stu-id="cf908-265">Yes</span></span> |
| <span data-ttu-id="cf908-266">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cf908-266">description</span></span> | <span data-ttu-id="cf908-267">Tekst die beschrijft wat de activiteit doet.</span><span class="sxs-lookup"><span data-stu-id="cf908-267">Text describing what the activity does.</span></span> | <span data-ttu-id="cf908-268">Nee</span><span class="sxs-lookup"><span data-stu-id="cf908-268">No</span></span> |
| <span data-ttu-id="cf908-269">type</span><span class="sxs-lookup"><span data-stu-id="cf908-269">type</span></span> | <span data-ttu-id="cf908-270">Deze eigenschap moet worden ingesteld op HDInsightSpark.</span><span class="sxs-lookup"><span data-stu-id="cf908-270">This property must be set to HDInsightSpark.</span></span> | <span data-ttu-id="cf908-271">Ja</span><span class="sxs-lookup"><span data-stu-id="cf908-271">Yes</span></span> |
| <span data-ttu-id="cf908-272">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="cf908-272">linkedServiceName</span></span> | <span data-ttu-id="cf908-273">De naam van de gekoppelde HDInsight-service op het Spark-programma wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cf908-273">Name of the HDInsight linked service on which the Spark program runs.</span></span> | <span data-ttu-id="cf908-274">Ja</span><span class="sxs-lookup"><span data-stu-id="cf908-274">Yes</span></span> |
| <span data-ttu-id="cf908-275">rootPath</span><span class="sxs-lookup"><span data-stu-id="cf908-275">rootPath</span></span> | <span data-ttu-id="cf908-276">De Azure Blob-container en de map waarin het Spark-bestand.</span><span class="sxs-lookup"><span data-stu-id="cf908-276">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="cf908-277">De bestandsnaam is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="cf908-277">The file name is case-sensitive.</span></span> | <span data-ttu-id="cf908-278">Ja</span><span class="sxs-lookup"><span data-stu-id="cf908-278">Yes</span></span> |
| <span data-ttu-id="cf908-279">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="cf908-279">entryFilePath</span></span> | <span data-ttu-id="cf908-280">Relatief pad naar de hoofdmap van het Spark/codepakket.</span><span class="sxs-lookup"><span data-stu-id="cf908-280">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="cf908-281">Ja</span><span class="sxs-lookup"><span data-stu-id="cf908-281">Yes</span></span> |
| <span data-ttu-id="cf908-282">className</span><span class="sxs-lookup"><span data-stu-id="cf908-282">className</span></span> | <span data-ttu-id="cf908-283">Belangrijkste Java/Spark-klasse van de toepassing</span><span class="sxs-lookup"><span data-stu-id="cf908-283">Application's Java/Spark main class</span></span> | <span data-ttu-id="cf908-284">Nee</span><span class="sxs-lookup"><span data-stu-id="cf908-284">No</span></span> |
| <span data-ttu-id="cf908-285">Argumenten</span><span class="sxs-lookup"><span data-stu-id="cf908-285">arguments</span></span> | <span data-ttu-id="cf908-286">Een lijst met opdrachtregelargumenten aan het programma Spark.</span><span class="sxs-lookup"><span data-stu-id="cf908-286">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="cf908-287">Nee</span><span class="sxs-lookup"><span data-stu-id="cf908-287">No</span></span> |
| <span data-ttu-id="cf908-288">proxyUser</span><span class="sxs-lookup"><span data-stu-id="cf908-288">proxyUser</span></span> | <span data-ttu-id="cf908-289">De account van de gebruiker te imiteren voor het uitvoeren van het Spark-programma</span><span class="sxs-lookup"><span data-stu-id="cf908-289">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="cf908-290">Nee</span><span class="sxs-lookup"><span data-stu-id="cf908-290">No</span></span> |
| <span data-ttu-id="cf908-291">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="cf908-291">sparkConfig</span></span> | <span data-ttu-id="cf908-292">Geef waarden voor Spark configuratie-eigenschappen die worden vermeld in het onderwerp: [Spark-configuratie - eigenschappen van Application](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span><span class="sxs-lookup"><span data-stu-id="cf908-292">Specify values for Spark configuration properties listed in the topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="cf908-293">Nee</span><span class="sxs-lookup"><span data-stu-id="cf908-293">No</span></span> |
| <span data-ttu-id="cf908-294">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="cf908-294">getDebugInfo</span></span> | <span data-ttu-id="cf908-295">Geeft aan wanneer de Spark-logboekbestanden worden gekopieerd naar de Azure-opslag door HDInsight-cluster gebruikt (of) opgegeven door sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="cf908-295">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="cf908-296">Toegestane waarden: None, altijd of fout.</span><span class="sxs-lookup"><span data-stu-id="cf908-296">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="cf908-297">Standaardwaarde: geen.</span><span class="sxs-lookup"><span data-stu-id="cf908-297">Default value: None.</span></span> | <span data-ttu-id="cf908-298">Nee</span><span class="sxs-lookup"><span data-stu-id="cf908-298">No</span></span> |
| <span data-ttu-id="cf908-299">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="cf908-299">sparkJobLinkedService</span></span> | <span data-ttu-id="cf908-300">Azure Storage gekoppelde service die de Spark taakbestand, afhankelijkheden en Logboeken bevat.</span><span class="sxs-lookup"><span data-stu-id="cf908-300">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="cf908-301">Als u een waarde op voor deze eigenschap niet opgeeft, wordt de opslag die is gekoppeld aan de HDInsight-cluster gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cf908-301">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="cf908-302">Nee</span><span class="sxs-lookup"><span data-stu-id="cf908-302">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="cf908-303">Mapstructuur</span><span class="sxs-lookup"><span data-stu-id="cf908-303">Folder structure</span></span>
<span data-ttu-id="cf908-304">Een in-line-script als Pig biedt geen ondersteuning voor de activiteit Spark en Hive-activiteiten doen.</span><span class="sxs-lookup"><span data-stu-id="cf908-304">The Spark activity does not support an in-line script as Pig and Hive activities do.</span></span> <span data-ttu-id="cf908-305">Spark-taken zijn ook meer extensible dan Pig/Hive-taken.</span><span class="sxs-lookup"><span data-stu-id="cf908-305">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="cf908-306">Voor Spark taken, kunt u meerdere afhankelijkheden, zoals opgeven jar-pakketten (geplaatst in de java CLASSPATH), python-bestanden (geplaatst op de PYTHONPATH) en andere bestanden.</span><span class="sxs-lookup"><span data-stu-id="cf908-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in the java CLASSPATH), python files (placed on the PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="cf908-307">De volgende mapstructuur maken in Azure Blob storage waarnaar wordt verwezen door de gekoppelde HDInsight-service.</span><span class="sxs-lookup"><span data-stu-id="cf908-307">Create the following folder structure in the Azure Blob storage referenced by the HDInsight linked service.</span></span> <span data-ttu-id="cf908-308">Vervolgens afhankelijke bestanden uploaden naar de juiste submappen in de hoofdmap dat wordt vertegenwoordigd door **entryFilePath**.</span><span class="sxs-lookup"><span data-stu-id="cf908-308">Then, upload dependent files to the appropriate sub folders in the root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="cf908-309">Bijvoorbeeld, python-bestanden naar de submap pyFiles en jar-bestanden uploaden naar de submap potten van de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="cf908-309">For example, upload python files to the pyFiles subfolder and jar files to the jars subfolder of the root folder.</span></span> <span data-ttu-id="cf908-310">Tijdens runtime verwacht Data Factory-service de volgende mapstructuur in de Azure Blob-opslag:</span><span class="sxs-lookup"><span data-stu-id="cf908-310">At runtime, Data Factory service expects the following folder structure in the Azure Blob storage:</span></span>     

| <span data-ttu-id="cf908-311">Pad</span><span class="sxs-lookup"><span data-stu-id="cf908-311">Path</span></span> | <span data-ttu-id="cf908-312">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cf908-312">Description</span></span> | <span data-ttu-id="cf908-313">Vereist</span><span class="sxs-lookup"><span data-stu-id="cf908-313">Required</span></span> | <span data-ttu-id="cf908-314">Type</span><span class="sxs-lookup"><span data-stu-id="cf908-314">Type</span></span> |
| ---- | ----------- | -------- | ---- |
| <span data-ttu-id="cf908-315">.</span><span class="sxs-lookup"><span data-stu-id="cf908-315">.</span></span> | <span data-ttu-id="cf908-316">Het pad naar de hoofdmap van de taak Spark in gekoppelde storage-service</span><span class="sxs-lookup"><span data-stu-id="cf908-316">The root path of the Spark job in the storage linked service</span></span>  | <span data-ttu-id="cf908-317">Ja</span><span class="sxs-lookup"><span data-stu-id="cf908-317">Yes</span></span> | <span data-ttu-id="cf908-318">Map</span><span class="sxs-lookup"><span data-stu-id="cf908-318">Folder</span></span> |
| <span data-ttu-id="cf908-319">&lt;de gebruiker gedefinieerde&gt;</span><span class="sxs-lookup"><span data-stu-id="cf908-319">&lt;user defined &gt;</span></span> | <span data-ttu-id="cf908-320">Het pad verwijst naar het bestand vermelding van de Spark-taak</span><span class="sxs-lookup"><span data-stu-id="cf908-320">The path pointing to the entry file of the Spark job</span></span> | <span data-ttu-id="cf908-321">Ja</span><span class="sxs-lookup"><span data-stu-id="cf908-321">Yes</span></span> | <span data-ttu-id="cf908-322">File</span><span class="sxs-lookup"><span data-stu-id="cf908-322">File</span></span> |
| <span data-ttu-id="cf908-323">. / jars</span><span class="sxs-lookup"><span data-stu-id="cf908-323">./jars</span></span> | <span data-ttu-id="cf908-324">Alle bestanden onder deze map worden geüpload en op de java-klassenpad van het cluster geplaatst</span><span class="sxs-lookup"><span data-stu-id="cf908-324">All files under this folder are uploaded and placed on the java classpath of the cluster</span></span> | <span data-ttu-id="cf908-325">Nee</span><span class="sxs-lookup"><span data-stu-id="cf908-325">No</span></span> | <span data-ttu-id="cf908-326">Map</span><span class="sxs-lookup"><span data-stu-id="cf908-326">Folder</span></span> |
| <span data-ttu-id="cf908-327">. / pyFiles</span><span class="sxs-lookup"><span data-stu-id="cf908-327">./pyFiles</span></span> | <span data-ttu-id="cf908-328">Alle bestanden onder deze map worden geüpload en op de PYTHONPATH van het cluster geplaatst</span><span class="sxs-lookup"><span data-stu-id="cf908-328">All files under this folder are uploaded and placed on the PYTHONPATH of the cluster</span></span> | <span data-ttu-id="cf908-329">Nee</span><span class="sxs-lookup"><span data-stu-id="cf908-329">No</span></span> | <span data-ttu-id="cf908-330">Map</span><span class="sxs-lookup"><span data-stu-id="cf908-330">Folder</span></span> |
| <span data-ttu-id="cf908-331">. / bestanden</span><span class="sxs-lookup"><span data-stu-id="cf908-331">./files</span></span> | <span data-ttu-id="cf908-332">Alle bestanden onder deze map worden geüpload en in de werkmap executor geplaatst</span><span class="sxs-lookup"><span data-stu-id="cf908-332">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="cf908-333">Nee</span><span class="sxs-lookup"><span data-stu-id="cf908-333">No</span></span> | <span data-ttu-id="cf908-334">Map</span><span class="sxs-lookup"><span data-stu-id="cf908-334">Folder</span></span> |
| <span data-ttu-id="cf908-335">. / archiveert</span><span class="sxs-lookup"><span data-stu-id="cf908-335">./archives</span></span> | <span data-ttu-id="cf908-336">Alle bestanden onder deze map zijn gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="cf908-336">All files under this folder are uncompressed</span></span> | <span data-ttu-id="cf908-337">Nee</span><span class="sxs-lookup"><span data-stu-id="cf908-337">No</span></span> | <span data-ttu-id="cf908-338">Map</span><span class="sxs-lookup"><span data-stu-id="cf908-338">Folder</span></span> |
| <span data-ttu-id="cf908-339">. / Logboeken</span><span class="sxs-lookup"><span data-stu-id="cf908-339">./logs</span></span> | <span data-ttu-id="cf908-340">De map waar de logboeken van het Spark-cluster worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="cf908-340">The folder where logs from the Spark cluster are stored.</span></span>| <span data-ttu-id="cf908-341">Nee</span><span class="sxs-lookup"><span data-stu-id="cf908-341">No</span></span> | <span data-ttu-id="cf908-342">Map</span><span class="sxs-lookup"><span data-stu-id="cf908-342">Folder</span></span> |

<span data-ttu-id="cf908-343">Hier volgt een voorbeeld van een opslagruimte met twee Spark taakbestanden in de Azure-blobopslag waarnaar wordt verwezen door de gekoppelde HDInsight-service.</span><span class="sxs-lookup"><span data-stu-id="cf908-343">Here is an example for a storage containing two Spark job files in the Azure Blob Storage referenced by the HDInsight linked service.</span></span>

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
