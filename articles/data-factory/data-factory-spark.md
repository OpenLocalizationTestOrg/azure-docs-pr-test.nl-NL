---
title: aaaInvoke Spark programma's van Azure Data Factory | Microsoft Docs
description: Meer informatie over hoe tooinvoke Spark-programma's vanuit een Azure data factory met Hallo MapReduce-activiteit.
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
ms.openlocfilehash: f88943ece7ee3d21dedbd857609f1b2713b62741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="2ee41-103">Spark-programma's van Azure Data Factory-pijplijnen aanroepen</span><span class="sxs-lookup"><span data-stu-id="2ee41-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="2ee41-104">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="2ee41-104">Hive Activity</span></span>](data-factory-hive-activity.md)
> * [<span data-ttu-id="2ee41-105">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="2ee41-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="2ee41-106">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="2ee41-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="2ee41-107">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="2ee41-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="2ee41-108">Spark-activiteit</span><span class="sxs-lookup"><span data-stu-id="2ee41-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="2ee41-109">Machine Learning-batchuitvoeringsactiviteit</span><span class="sxs-lookup"><span data-stu-id="2ee41-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="2ee41-110">Machine Learning-activiteit resources bijwerken</span><span class="sxs-lookup"><span data-stu-id="2ee41-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="2ee41-111">Opgeslagen procedureactiviteit</span><span class="sxs-lookup"><span data-stu-id="2ee41-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="2ee41-112">Data Lake Analytics U-SQL-activiteit</span><span class="sxs-lookup"><span data-stu-id="2ee41-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="2ee41-113">Aangepaste activiteit .NET</span><span class="sxs-lookup"><span data-stu-id="2ee41-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="2ee41-114">Inleiding</span><span class="sxs-lookup"><span data-stu-id="2ee41-114">Introduction</span></span>
<span data-ttu-id="2ee41-115">Spark-activiteit is een van de Hallo [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) ondersteund door Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2ee41-115">Spark Activity is one of hello [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span></span> <span data-ttu-id="2ee41-116">Deze activiteit wordt uitgevoerd Hallo opgegeven programma op uw Apache Spark-cluster in Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="2ee41-116">This activity runs hello specified Spark program on your Apache Spark cluster in Azure HDInsight.</span></span>    

> [!IMPORTANT]
> - <span data-ttu-id="2ee41-117">Spark activiteit biedt geen ondersteuning voor HDInsight Spark-clusters die gebruikmaken van een Azure Data Lake Store als primaire opslag.</span><span class="sxs-lookup"><span data-stu-id="2ee41-117">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
> - <span data-ttu-id="2ee41-118">Spark-activiteit ondersteunt alleen bestaande (uw eigen) HDInsight Spark-clusters.</span><span class="sxs-lookup"><span data-stu-id="2ee41-118">Spark Activity supports only existing (your own) HDInsight Spark clusters.</span></span> <span data-ttu-id="2ee41-119">Een gekoppelde HDInsight-service op aanvraag worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="2ee41-119">It does not support an on-demand HDInsight linked service.</span></span>

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a><span data-ttu-id="2ee41-120">Overzicht: een pijplijn maken met Spark-activiteit</span><span class="sxs-lookup"><span data-stu-id="2ee41-120">Walkthrough: create a pipeline with Spark activity</span></span>
<span data-ttu-id="2ee41-121">Hier volgen Hallo gebruikelijke stappen toocreate een Data Factory-pijplijn met een Spark-activiteit.</span><span class="sxs-lookup"><span data-stu-id="2ee41-121">Here are hello typical steps toocreate a Data Factory pipeline with a Spark activity.</span></span>  

1. <span data-ttu-id="2ee41-122">Een gegevensfactory maakt.</span><span class="sxs-lookup"><span data-stu-id="2ee41-122">Create a data factory.</span></span>
2. <span data-ttu-id="2ee41-123">Maak een gekoppelde Azure Storage-service toolink uw Azure-opslag die is gekoppeld aan uw HDInsight Spark-cluster toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="2ee41-123">Create an Azure Storage linked service toolink your Azure storage that is associated with your HDInsight Spark cluster toohello data factory.</span></span>     
2. <span data-ttu-id="2ee41-124">Maak een gekoppelde HDInsight-service toolink Apache Spark-cluster in Azure HDInsight toohello gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="2ee41-124">Create an Azure HDInsight linked service toolink your Apache Spark cluster in Azure HDInsight toohello data factory.</span></span>
3. <span data-ttu-id="2ee41-125">Maak een gegevensset die toohello Azure Storage gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="2ee41-125">Create a dataset that refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="2ee41-126">U moet een uitvoergegevensset voor een activiteit op dit moment kunt opgeven, zelfs als er wordt geen uitvoer wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="2ee41-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span>  
4. <span data-ttu-id="2ee41-127">Een pijplijn maken met Spark-activiteit die toohello gekoppelde HDInsight-service is gemaakt in #2 verwijst.</span><span class="sxs-lookup"><span data-stu-id="2ee41-127">Create a pipeline with Spark activity that refers toohello HDInsight linked service created in #2.</span></span> <span data-ttu-id="2ee41-128">Hallo-activiteit is geconfigureerd met Hallo gegevensset die u hebt gemaakt in de vorige stap Hallo als een uitvoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="2ee41-128">hello activity is configured with hello dataset you created in hello previous step as an output dataset.</span></span> <span data-ttu-id="2ee41-129">Hallo uitvoergegevensset is welke stations Hallo planning (elk uur, dagelijks, enz.).</span><span class="sxs-lookup"><span data-stu-id="2ee41-129">hello output dataset is what drives hello schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="2ee41-130">Daarom moet u Hallo uitvoergegevensset zelfs als er geen activiteit Hallo echt uitvoer te produceren.</span><span class="sxs-lookup"><span data-stu-id="2ee41-130">Therefore, you must specify hello output dataset even though hello activity does not really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2ee41-131">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2ee41-131">Prerequisites</span></span>
1. <span data-ttu-id="2ee41-132">Maak een **voor algemene doeleinden Azure Storage-Account** door de instructies te volgen in Hallo overzicht te: [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="2ee41-132">Create a **general-purpose Azure Storage Account** by following instructions in hello walkthrough: [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
2. <span data-ttu-id="2ee41-133">Maak een **Apache Spark-cluster in Azure HDInsight** door de instructies te volgen in Hallo-zelfstudie: [maken Apache Spark-cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="2ee41-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in hello tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="2ee41-134">Hello Azure storage-account die u hebt gemaakt in stap 1 van # met dit cluster koppelen.</span><span class="sxs-lookup"><span data-stu-id="2ee41-134">Associate hello Azure storage account you created in step #1 with this cluster.</span></span>  
3. <span data-ttu-id="2ee41-135">Downloaden en bekijken Hallo python-scriptbestand **test.py** vinden op: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span><span class="sxs-lookup"><span data-stu-id="2ee41-135">Download and review hello python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>  
3.  <span data-ttu-id="2ee41-136">Uploaden **test.py** toohello **pyFiles** map in Hallo **adfspark** container in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="2ee41-136">Upload **test.py** toohello **pyFiles** folder in hello **adfspark** container in your Azure Blob storage.</span></span> <span data-ttu-id="2ee41-137">Hallo-container en map Hallo maken als ze bestaan niet.</span><span class="sxs-lookup"><span data-stu-id="2ee41-137">Create hello container and hello folder if they do not exist.</span></span>

### <a name="create-data-factory"></a><span data-ttu-id="2ee41-138">Een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="2ee41-138">Create data factory</span></span>
<span data-ttu-id="2ee41-139">Laten we beginnen met het maken van de gegevensfactory Hallo in deze stap.</span><span class="sxs-lookup"><span data-stu-id="2ee41-139">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="2ee41-140">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2ee41-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2ee41-141">Klik op **nieuw** op Hallo menu links, klikt u op **gegevens en analyse**, en klik op **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="2ee41-141">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="2ee41-142">In Hallo **nieuwe gegevensfactory** blade Voer **SparkDF** voor Hallo naam.</span><span class="sxs-lookup"><span data-stu-id="2ee41-142">In hello **New data factory** blade, enter **SparkDF** for hello Name.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="2ee41-143">Hallo-naam van hello Azure-gegevensfactory moet **globaal unieke**.</span><span class="sxs-lookup"><span data-stu-id="2ee41-143">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="2ee41-144">Als u Hallo fout ziet: **Data factory-naam 'SparkDF' is niet beschikbaar**.</span><span class="sxs-lookup"><span data-stu-id="2ee41-144">If you see hello error: **Data factory name “SparkDF” is not available**.</span></span> <span data-ttu-id="2ee41-145">Wijzig de naam van de Hallo van gegevensfactory hello (bijvoorbeeld yournameSparkDFdate en probeer het opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="2ee41-145">Change hello name of hello data factory (for example, yournameSparkDFdate, and try creating again.</span></span> <span data-ttu-id="2ee41-146">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="2ee41-146">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
4. <span data-ttu-id="2ee41-147">Selecteer Hallo **Azure-abonnement** waar u Hallo data factory toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2ee41-147">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="2ee41-148">Selecteer een bestaande **resourcegroep** of maak een Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="2ee41-148">Select an existing **resource group** or create an Azure resource group.</span></span>
6. <span data-ttu-id="2ee41-149">Selecteer **pincode toodashboard** optie.</span><span class="sxs-lookup"><span data-stu-id="2ee41-149">Select **Pin toodashboard** option.</span></span>  
6. <span data-ttu-id="2ee41-150">Klik op **maken** op Hallo **nieuwe gegevensfactory** blade.</span><span class="sxs-lookup"><span data-stu-id="2ee41-150">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="2ee41-151">toocreate Data Factory-exemplaren, moet u lid zijn van Hallo [Data Factory Inzender](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol op het niveau van de Hallo abonnement/resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="2ee41-151">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
7. <span data-ttu-id="2ee41-152">Zie van Hallo gegevensfactory wordt gemaakt in Hallo **dashboard** Hallo Azure-portal als volgt:</span><span class="sxs-lookup"><span data-stu-id="2ee41-152">You see hello data factory being created in hello **dashboard** of hello Azure portal as follows:</span></span>   
8. <span data-ttu-id="2ee41-153">Nadat het Hallo-gegevensfactory is gemaakt, ziet u Hallo data factory-pagina waarop u inhoud van de gegevensfactory Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="2ee41-153">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span> <span data-ttu-id="2ee41-154">Als u Hallo data factory-pagina niet ziet, klikt u op Hallo tegel voor uw gegevensfactory op Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="2ee41-154">If you do not see hello data factory page, click hello tile for your data factory on hello dashboard.</span></span>

    ![Blade Gegevensfactory](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="2ee41-156">Gekoppelde services maken</span><span class="sxs-lookup"><span data-stu-id="2ee41-156">Create linked services</span></span>
<span data-ttu-id="2ee41-157">In deze stap kunt u twee gekoppelde services, één toolink uw Spark-cluster tooyour een gegevensfactory maken en andere toolink Hallo uw Azure-opslag tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="2ee41-157">In this step, you create two linked services, one toolink your Spark cluster tooyour data factory, and hello other toolink your Azure storage tooyour data factory.</span></span>  

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="2ee41-158">Een gekoppelde Azure Storage-service maken</span><span class="sxs-lookup"><span data-stu-id="2ee41-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="2ee41-159">In deze stap koppelt u uw Azure Storage-account tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="2ee41-159">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="2ee41-160">Een gegevensset die u in stap verderop in dit scenario maakt verwijst toothis gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="2ee41-160">A dataset you create in a step later in this walkthrough refers toothis linked service.</span></span> <span data-ttu-id="2ee41-161">Hallo gekoppelde HDInsight-service die u in de volgende stap Hallo definieert verwijst te toothis gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="2ee41-161">hello HDInsight linked service that you define in hello next step refers toothis linked service too.</span></span>  

1. <span data-ttu-id="2ee41-162">Klik op **auteur en implementeren van** op Hallo **Data Factory** blade van uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="2ee41-162">Click **Author and deploy** on hello **Data Factory** blade for your data factory.</span></span> <span data-ttu-id="2ee41-163">U ziet Hallo Data Factory-Editor.</span><span class="sxs-lookup"><span data-stu-id="2ee41-163">You should see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="2ee41-164">Klik op **Nieuwe gegevensopslag** en kies **Azure-opslag**.</span><span class="sxs-lookup"><span data-stu-id="2ee41-164">Click **New data store** and choose **Azure storage**.</span></span>

   ![Nieuwe gegevensopslag - Azure Storage - menu](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="2ee41-166">U ziet Hallo **JSON-script** voor het maken van een Azure Storage gekoppelde service in Hallo-editor.</span><span class="sxs-lookup"><span data-stu-id="2ee41-166">You should see hello **JSON script** for creating an Azure Storage linked service in hello editor.</span></span>

   ![Een gekoppelde Azure Storage-service](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="2ee41-168">Vervang **accountnaam** en **accountsleutel** met de naam en toegangssleutel Hallo van uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="2ee41-168">Replace **account name** and **account key** with hello name and access key of your Azure storage account.</span></span> <span data-ttu-id="2ee41-169">toolearn hoe tooget uw opslag heeft toegang tot sleutel, raadpleegt u Hallo informatie over hoe tooview, kopiëren en opnieuw genereren opslag toegangstoetsen in [uw opslagaccount beheren](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="2ee41-169">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="2ee41-170">toodeploy Hallo gekoppelde service, klikt u op **implementeren** op Hallo opdrachtbalk klikken.</span><span class="sxs-lookup"><span data-stu-id="2ee41-170">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="2ee41-171">Nadat hello gekoppelde service is geïmplementeerd, Hallo **Draft-1** venster verdwijnt en ziet u **AzureStorageLinkedService** in Hallo structuurweergave Hallo links.</span><span class="sxs-lookup"><span data-stu-id="2ee41-171">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

#### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="2ee41-172">Een gekoppelde HDInsight-service maken</span><span class="sxs-lookup"><span data-stu-id="2ee41-172">Create HDInsight linked service</span></span>
<span data-ttu-id="2ee41-173">In deze stap maakt u een gekoppelde HDInsight-service toolink uw HDInsight Spark-cluster toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="2ee41-173">In this step, you create Azure HDInsight linked service toolink your HDInsight Spark cluster toohello data factory.</span></span> <span data-ttu-id="2ee41-174">Hallo HDInsight-cluster is gebruikte toorun Hallo Spark programma dat is opgegeven in de Hallo Spark activiteit van Hallo pijplijn in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="2ee41-174">hello HDInsight cluster is used toorun hello Spark program specified in hello Spark activity of hello pipeline in this sample.</span></span>  

1. <span data-ttu-id="2ee41-175">Klik op **... Meer** op de werkbalk Hallo **nieuwe berekening**, en klik vervolgens op **HDInsight-cluster**.</span><span class="sxs-lookup"><span data-stu-id="2ee41-175">Click **... More** on hello toolbar, click **New compute**, and then click **HDInsight cluster**.</span></span>

    ![Een gekoppelde HDInsight-service maken](media/data-factory-spark/new-hdinsight-linked-service.png)
2. <span data-ttu-id="2ee41-177">Kopieer en plak de volgende codefragment toohello hello **Draft-1** venster.</span><span class="sxs-lookup"><span data-stu-id="2ee41-177">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="2ee41-178">In de JSON-editor Hallo Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2ee41-178">In hello JSON editor, do hello following steps:</span></span>
    1. <span data-ttu-id="2ee41-179">Geef Hallo **URI** voor Hallo HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="2ee41-179">Specify hello **URI** for hello HDInsight Spark cluster.</span></span> <span data-ttu-id="2ee41-180">Bijvoorbeeld: `https://<sparkclustername>.azurehdinsight.net/`.</span><span class="sxs-lookup"><span data-stu-id="2ee41-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span>
    2. <span data-ttu-id="2ee41-181">Geef de naam Hallo Hallo **gebruiker** wie heeft toegang tot toohello Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="2ee41-181">Specify hello name of hello **user** who has access toohello Spark cluster.</span></span>
    3. <span data-ttu-id="2ee41-182">Geef Hallo **wachtwoord** voor de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2ee41-182">Specify hello **password** for user.</span></span>
    4. <span data-ttu-id="2ee41-183">Geef Hallo **gekoppelde Azure Storage-service** dat is gekoppeld aan Hallo HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="2ee41-183">Specify hello **Azure Storage linked service** that is associated with hello HDInsight Spark cluster.</span></span> <span data-ttu-id="2ee41-184">In dit voorbeeld is: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="2ee41-184">In this example, it is: **AzureStorageLinkedService**.</span></span>

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
    > - <span data-ttu-id="2ee41-185">Spark activiteit biedt geen ondersteuning voor HDInsight Spark-clusters die gebruikmaken van een Azure Data Lake Store als primaire opslag.</span><span class="sxs-lookup"><span data-stu-id="2ee41-185">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
    > - <span data-ttu-id="2ee41-186">Spark-activiteit ondersteunt alleen bestaande (uw eigen) HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="2ee41-186">Spark Activity supports only existing (your own) HDInsight Spark cluster.</span></span> <span data-ttu-id="2ee41-187">Een gekoppelde HDInsight-service op aanvraag worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="2ee41-187">It does not support an on-demand HDInsight linked service.</span></span>

    <span data-ttu-id="2ee41-188">Zie [gekoppelde HDInsight-Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) voor meer informatie over Hallo HDInsight gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="2ee41-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about hello HDInsight linked service.</span></span>
3.  <span data-ttu-id="2ee41-189">toodeploy Hallo gekoppelde service, klikt u op **implementeren** op Hallo opdrachtbalk klikken.</span><span class="sxs-lookup"><span data-stu-id="2ee41-189">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="2ee41-190">Uitvoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="2ee41-190">Create output dataset</span></span>
<span data-ttu-id="2ee41-191">Hallo uitvoergegevensset is welke stations Hallo planning (elk uur, dagelijks, enz.).</span><span class="sxs-lookup"><span data-stu-id="2ee41-191">hello output dataset is what drives hello schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="2ee41-192">Daarom moet u een uitvoergegevensset voor Hallo spark activiteit in de pijplijn Hallo Hoewel Hallo activiteit geen echt geen uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="2ee41-192">Therefore, you must specify an output dataset for hello spark activity in hello pipeline even though hello activity does not really produce any output.</span></span> <span data-ttu-id="2ee41-193">Het opgeven van een invoergegevensset voor Hallo-activiteit is optioneel.</span><span class="sxs-lookup"><span data-stu-id="2ee41-193">Specifying an input dataset for hello activity is optional.</span></span>

1. <span data-ttu-id="2ee41-194">In Hallo **Data Factory-Editor**, klikt u op **... Meer** op de opdrachtbalk hello, klikt u op **nieuwe gegevensset**, en selecteer **Azure Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="2ee41-194">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="2ee41-195">Kopieer en plak Hallo na codefragment toohello Draft-1-venster.</span><span class="sxs-lookup"><span data-stu-id="2ee41-195">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="2ee41-196">Hallo JSON-fragment een gegevensset met de naam definieert **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="2ee41-196">hello JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="2ee41-197">Bovendien u opgeven dat Hallo resultaten worden opgeslagen in blob-container Hallo aangeroepen **adfspark** en Hallo map met de naam **pyFiles/uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="2ee41-197">In addition, you specify that hello results are stored in hello blob container called **adfspark** and hello folder called **pyFiles/output**.</span></span> <span data-ttu-id="2ee41-198">Zoals eerder vermeld, is deze gegevensset een dummy-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="2ee41-198">As mentioned earlier, this dataset is a dummy dataset.</span></span> <span data-ttu-id="2ee41-199">Hallo Spark programma in dit voorbeeld heeft geen uitvoer wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="2ee41-199">hello Spark program in this example does not produce any output.</span></span> <span data-ttu-id="2ee41-200">Hallo **beschikbaarheid** sectie geeft die Hallo-uitvoergegevensset dagelijks wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="2ee41-200">hello **availability** section specifies that hello output dataset is produced daily.</span></span>  

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
3. <span data-ttu-id="2ee41-201">toodeploy Hallo gegevensset, klikt u op **implementeren** op Hallo opdrachtbalk klikken.</span><span class="sxs-lookup"><span data-stu-id="2ee41-201">toodeploy hello dataset, click **Deploy** on hello command bar.</span></span>


### <a name="create-pipeline"></a><span data-ttu-id="2ee41-202">Pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="2ee41-202">Create pipeline</span></span>
<span data-ttu-id="2ee41-203">In deze stap maakt u een pijplijn met een **HDInsightSpark** activiteit.</span><span class="sxs-lookup"><span data-stu-id="2ee41-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span></span> <span data-ttu-id="2ee41-204">Uitvoergegevensset is momenteel welke stations Hallo planning, dus u een uitvoergegevensset maken moet, zelfs als Hallo activiteit geen uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="2ee41-204">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="2ee41-205">Als Hallo activiteit geen invoer neemt, kunt u maken Hallo invoergegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="2ee41-205">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="2ee41-206">Daarom is geen invoergegevensset opgegeven in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="2ee41-206">Therefore, no input dataset is specified in this example.</span></span>

1. <span data-ttu-id="2ee41-207">In Hallo **Data Factory-Editor**, klikt u op **... Meer** op Hallo opdrachtbalk en klik vervolgens op **nieuwe pijplijn**.</span><span class="sxs-lookup"><span data-stu-id="2ee41-207">In hello **Data Factory Editor**, click **… More** on hello command bar, and then click **New pipeline**.</span></span>
2. <span data-ttu-id="2ee41-208">Hallo-script in het venster Draft-1 Hallo vervangen door Hallo script volgen:</span><span class="sxs-lookup"><span data-stu-id="2ee41-208">Replace hello script in hello Draft-1 window with hello following script:</span></span>

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
    <span data-ttu-id="2ee41-209">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="2ee41-209">Note hello following points:</span></span>
    - <span data-ttu-id="2ee41-210">Hallo **type** eigenschap is ingesteld, te**HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="2ee41-210">hello **type** property is set too**HDInsightSpark**.</span></span>
    - <span data-ttu-id="2ee41-211">Hallo **rootPath** te is ingesteld,**adfspark\\pyFiles** waarbij adfspark hello Azure Blob-container en pyFiles is map in de container.</span><span class="sxs-lookup"><span data-stu-id="2ee41-211">hello **rootPath** is set too**adfspark\\pyFiles** where adfspark is hello Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="2ee41-212">In dit voorbeeld is hello Azure Blob Storage Hallo die is gekoppeld aan Hallo Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="2ee41-212">In this example, hello Azure Blob Storage is hello one that is associated with hello Spark cluster.</span></span> <span data-ttu-id="2ee41-213">U kunt uploaden Hallo bestand tooa andere Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="2ee41-213">You can upload hello file tooa different Azure Storage.</span></span> <span data-ttu-id="2ee41-214">Als u doet dit, wordt een gekoppelde Azure Storage-service toolink die storage account toohello een gegevensfactory maken.</span><span class="sxs-lookup"><span data-stu-id="2ee41-214">If you do so, create an Azure Storage linked service toolink that storage account toohello data factory.</span></span> <span data-ttu-id="2ee41-215">Hallo-naam van gekoppelde Hallo-service vervolgens opgeven als een waarde voor Hallo **sparkJobLinkedService** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="2ee41-215">Then, specify hello name of hello linked service as a value for hello **sparkJobLinkedService** property.</span></span> <span data-ttu-id="2ee41-216">Zie [Spark activiteitseigenschappen](#spark-activity-properties) voor meer informatie over deze eigenschap en andere eigenschappen die ondersteund worden door Hallo Spark-activiteit.</span><span class="sxs-lookup"><span data-stu-id="2ee41-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by hello Spark Activity.</span></span>  
    - <span data-ttu-id="2ee41-217">Hallo **entryFilePath** toohello is ingesteld **test.py**, namelijk Hallo python-bestand.</span><span class="sxs-lookup"><span data-stu-id="2ee41-217">hello **entryFilePath** is set toohello **test.py**, which is hello python file.</span></span>
    - <span data-ttu-id="2ee41-218">Hallo **getDebugInfo** eigenschap is ingesteld, te**altijd**, wat betekent dat het Hallo-logboekbestanden zijn altijd gegenereerd (slagen of mislukken).</span><span class="sxs-lookup"><span data-stu-id="2ee41-218">hello **getDebugInfo** property is set too**Always**, which means hello log files are always generated (success or failure).</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="2ee41-219">Het is raadzaam dat u niet deze eigenschap te stelt`Always` in een productieomgeving tenzij u een probleem wilt oplossen.</span><span class="sxs-lookup"><span data-stu-id="2ee41-219">We recommend that you do not set this property too`Always` in a production environment unless you are troubleshooting an issue.</span></span>
    - <span data-ttu-id="2ee41-220">Hallo **levert** sectie heeft één uitvoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="2ee41-220">hello **outputs** section has one output dataset.</span></span> <span data-ttu-id="2ee41-221">U kunt een uitvoergegevensset moet opgeven, zelfs als Hallo spark programma geen uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="2ee41-221">You must specify an output dataset even if hello spark program does not produce any output.</span></span> <span data-ttu-id="2ee41-222">Hallo output dataset stations Hallo planning voor Hallo pijplijn (elk uur, dagelijks, enz.).</span><span class="sxs-lookup"><span data-stu-id="2ee41-222">hello output dataset drives hello schedule for hello pipeline (hourly, daily, etc.).</span></span>  

        <span data-ttu-id="2ee41-223">Zie voor meer informatie over het Hallo-eigenschappen die ondersteund worden door de activiteit Spark [activiteitseigenschappen Spark](#spark-activity-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="2ee41-223">For details about hello properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span></span>
3. <span data-ttu-id="2ee41-224">toodeploy hello pipeline, klikt u op **implementeren** op Hallo opdrachtbalk klikken.</span><span class="sxs-lookup"><span data-stu-id="2ee41-224">toodeploy hello pipeline, click **Deploy** on hello command bar.</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="2ee41-225">De pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="2ee41-225">Monitor pipeline</span></span>
1. <span data-ttu-id="2ee41-226">Klik op **X** tooclose Data Factory-Editor blades en toonavigate weer toohello Data Factory-startpagina.</span><span class="sxs-lookup"><span data-stu-id="2ee41-226">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory home page.</span></span> <span data-ttu-id="2ee41-227">Klik op **bewaken en beheren** toolaunch Hallo monitoring-toepassing in een ander tabblad.</span><span class="sxs-lookup"><span data-stu-id="2ee41-227">Click **Monitor and Manage** toolaunch hello monitoring application in another tab.</span></span>

    ![Bewaken en beheren van de tegel](media/data-factory-spark/monitor-and-manage-tile.png)
2. <span data-ttu-id="2ee41-229">Wijziging Hallo **begintijd** te filteren Hallo boven**2/1/2017**, en klik op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="2ee41-229">Change hello **Start time** filter at hello top too**2/1/2017**, and click **Apply**.</span></span>
3. <span data-ttu-id="2ee41-230">Omdat er slechts één dag tussen hello (2017-02-01) start- en eindtijden (2017-02-02) van de pijplijn hello, moet u slechts één activiteitvenster zien.</span><span class="sxs-lookup"><span data-stu-id="2ee41-230">You should see only one activity window as there is only one day between hello start (2017-02-01) and end times (2017-02-02) of hello pipeline.</span></span> <span data-ttu-id="2ee41-231">Bevestig dat gegevenssegment Hallo **gereed** status.</span><span class="sxs-lookup"><span data-stu-id="2ee41-231">Confirm that hello data slice is in **ready** state.</span></span>

    ![Hallo-pijplijn bewaken](media/data-factory-spark/monitor-and-manage-app.png)    
4. <span data-ttu-id="2ee41-233">Selecteer Hallo **activiteitsvenster** toosee details over Hallo activiteit die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2ee41-233">Select hello **activity window** toosee details about hello activity run.</span></span> <span data-ttu-id="2ee41-234">Als er een fout is, ziet u meer informatie over het in het rechterdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="2ee41-234">If there is an error, you see details about it in hello right pane.</span></span>

### <a name="verify-hello-results"></a><span data-ttu-id="2ee41-235">Hallo resultaten controleren</span><span class="sxs-lookup"><span data-stu-id="2ee41-235">Verify hello results</span></span>

1. <span data-ttu-id="2ee41-236">Start **Jupyter-notebook** voor uw HDInsight Spark-cluster door te navigeren naar: https://CLUSTERNAME.azurehdinsight.NET/jupyter.</span><span class="sxs-lookup"><span data-stu-id="2ee41-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="2ee41-237">U kunt ook starten cluster-dashboard voor uw HDInsight Spark-cluster en start vervolgens **Jupyter-Notebook**.</span><span class="sxs-lookup"><span data-stu-id="2ee41-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span></span>
2. <span data-ttu-id="2ee41-238">Klik op **nieuw** -> **PySpark** toostart een nieuwe notebook.</span><span class="sxs-lookup"><span data-stu-id="2ee41-238">Click **New** -> **PySpark** toostart a new notebook.</span></span>

    ![Nieuwe Jupyter-notebook](media/data-factory-spark/jupyter-new-book.png)
3. <span data-ttu-id="2ee41-240">Voer hello na de opdracht door de tekst hello kopiëren/plakken en drukt u op **SHIFT + ENTER** aan Hallo einde van de tweede instructie Hallo.</span><span class="sxs-lookup"><span data-stu-id="2ee41-240">Run hello following command by copy/pasting hello text and pressing **SHIFT + ENTER** at hello end of hello second statement.</span></span>  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. <span data-ttu-id="2ee41-241">Controleer of u Hallo gegevens uit Hallo hvac tabel:</span><span class="sxs-lookup"><span data-stu-id="2ee41-241">Confirm that you see hello data from hello hvac table:</span></span>  

    ![Jupyter-queryresultaten](media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="2ee41-243">Zie [een Spark SQL-query uitvoeren](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) gedeelte voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2ee41-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) section for detailed instructions.</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="2ee41-244">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="2ee41-244">Troubleshooting</span></span>
<span data-ttu-id="2ee41-245">Aangezien u ingesteld **getDebugInfo** te**altijd**, ziet u een **logboek** submap Hallo **pyFiles** map in uw Azure Blob-container.</span><span class="sxs-lookup"><span data-stu-id="2ee41-245">Since you set **getDebugInfo** too**Always**, you see a **log** subfolder in hello **pyFiles** folder in your Azure Blob container.</span></span> <span data-ttu-id="2ee41-246">Hallo-logboekbestand in de logboekmap Hallo vindt u meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2ee41-246">hello log file in hello log folder provides additional details.</span></span> <span data-ttu-id="2ee41-247">Dit logboekbestand is vooral nuttig wanneer er een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="2ee41-247">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="2ee41-248">In een productieomgeving kunt u tooset deze te**fout**.</span><span class="sxs-lookup"><span data-stu-id="2ee41-248">In a production environment, you may want tooset it too**Failure**.</span></span>

<span data-ttu-id="2ee41-249">Voor meer informatie over Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2ee41-249">For further troubleshooting, do hello following steps:</span></span>


1. <span data-ttu-id="2ee41-250">Navigeer te`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span><span class="sxs-lookup"><span data-stu-id="2ee41-250">Navigate too`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![Gebruikersinterface van YARN-toepassing](media/data-factory-spark/yarnui-application.png)  
2. <span data-ttu-id="2ee41-252">Klik op **logboeken** uitvoeren voor een Hallo pogingen.</span><span class="sxs-lookup"><span data-stu-id="2ee41-252">Click **Logs** for one of hello run attempts.</span></span>

    ![Toepassingspagina](media/data-factory-spark/yarn-applications.png)
3. <span data-ttu-id="2ee41-254">U kunt aanvullende foutinformatie in Hallo logboek pagina moeten zien.</span><span class="sxs-lookup"><span data-stu-id="2ee41-254">You should see additional error information in hello log page.</span></span>

    ![Fout in logboek](media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="2ee41-256">Hallo volgende secties bevatten informatie over Data Factory-entiteiten toouse Apache Spark-cluster en Spark-activiteit in uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="2ee41-256">hello following sections provide information about Data Factory entities toouse Apache Spark cluster and Spark Activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="2ee41-257">Spark-activiteitseigenschappen</span><span class="sxs-lookup"><span data-stu-id="2ee41-257">Spark activity properties</span></span>
<span data-ttu-id="2ee41-258">Hier volgt Hallo voorbeeld JSON-definitie van een pijplijn met Spark-activiteit:</span><span class="sxs-lookup"><span data-stu-id="2ee41-258">Here is hello sample JSON definition of a pipeline with Spark Activity:</span></span>    

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
                "description": "This activity invokes hello Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

<span data-ttu-id="2ee41-259">Hallo staan volgende tabel Hallo JSON-eigenschappen die in Hallo JSON-definitie:</span><span class="sxs-lookup"><span data-stu-id="2ee41-259">hello following table describes hello JSON properties used in hello JSON definition:</span></span>

| <span data-ttu-id="2ee41-260">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="2ee41-260">Property</span></span> | <span data-ttu-id="2ee41-261">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2ee41-261">Description</span></span> | <span data-ttu-id="2ee41-262">Vereist</span><span class="sxs-lookup"><span data-stu-id="2ee41-262">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="2ee41-263">naam</span><span class="sxs-lookup"><span data-stu-id="2ee41-263">name</span></span> | <span data-ttu-id="2ee41-264">Naam van de activiteit Hallo in Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="2ee41-264">Name of hello activity in hello pipeline.</span></span> | <span data-ttu-id="2ee41-265">Ja</span><span class="sxs-lookup"><span data-stu-id="2ee41-265">Yes</span></span> |
| <span data-ttu-id="2ee41-266">description</span><span class="sxs-lookup"><span data-stu-id="2ee41-266">description</span></span> | <span data-ttu-id="2ee41-267">Tekst die beschrijft welke activiteit Hallo komt.</span><span class="sxs-lookup"><span data-stu-id="2ee41-267">Text describing what hello activity does.</span></span> | <span data-ttu-id="2ee41-268">Nee</span><span class="sxs-lookup"><span data-stu-id="2ee41-268">No</span></span> |
| <span data-ttu-id="2ee41-269">type</span><span class="sxs-lookup"><span data-stu-id="2ee41-269">type</span></span> | <span data-ttu-id="2ee41-270">Deze eigenschap moet worden ingesteld als tooHDInsightSpark.</span><span class="sxs-lookup"><span data-stu-id="2ee41-270">This property must be set tooHDInsightSpark.</span></span> | <span data-ttu-id="2ee41-271">Ja</span><span class="sxs-lookup"><span data-stu-id="2ee41-271">Yes</span></span> |
| <span data-ttu-id="2ee41-272">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="2ee41-272">linkedServiceName</span></span> | <span data-ttu-id="2ee41-273">Naam van Hallo HDInsight gekoppelde service op welke Hallo Spark programma wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2ee41-273">Name of hello HDInsight linked service on which hello Spark program runs.</span></span> | <span data-ttu-id="2ee41-274">Ja</span><span class="sxs-lookup"><span data-stu-id="2ee41-274">Yes</span></span> |
| <span data-ttu-id="2ee41-275">rootPath</span><span class="sxs-lookup"><span data-stu-id="2ee41-275">rootPath</span></span> | <span data-ttu-id="2ee41-276">Hello Azure Blob-container en map met Hallo Spark-bestand.</span><span class="sxs-lookup"><span data-stu-id="2ee41-276">hello Azure Blob container and folder that contains hello Spark file.</span></span> <span data-ttu-id="2ee41-277">Hallo-bestandsnaam is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="2ee41-277">hello file name is case-sensitive.</span></span> | <span data-ttu-id="2ee41-278">Ja</span><span class="sxs-lookup"><span data-stu-id="2ee41-278">Yes</span></span> |
| <span data-ttu-id="2ee41-279">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="2ee41-279">entryFilePath</span></span> | <span data-ttu-id="2ee41-280">Relatief pad toohello Hallo Spark codepakket hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="2ee41-280">Relative path toohello root folder of hello Spark code/package.</span></span> | <span data-ttu-id="2ee41-281">Ja</span><span class="sxs-lookup"><span data-stu-id="2ee41-281">Yes</span></span> |
| <span data-ttu-id="2ee41-282">className</span><span class="sxs-lookup"><span data-stu-id="2ee41-282">className</span></span> | <span data-ttu-id="2ee41-283">Belangrijkste Java/Spark-klasse van de toepassing</span><span class="sxs-lookup"><span data-stu-id="2ee41-283">Application's Java/Spark main class</span></span> | <span data-ttu-id="2ee41-284">Nee</span><span class="sxs-lookup"><span data-stu-id="2ee41-284">No</span></span> |
| <span data-ttu-id="2ee41-285">Argumenten</span><span class="sxs-lookup"><span data-stu-id="2ee41-285">arguments</span></span> | <span data-ttu-id="2ee41-286">Een lijst met opdrachtregelargumenten toohello Spark programma.</span><span class="sxs-lookup"><span data-stu-id="2ee41-286">A list of command-line arguments toohello Spark program.</span></span> | <span data-ttu-id="2ee41-287">Nee</span><span class="sxs-lookup"><span data-stu-id="2ee41-287">No</span></span> |
| <span data-ttu-id="2ee41-288">proxyUser</span><span class="sxs-lookup"><span data-stu-id="2ee41-288">proxyUser</span></span> | <span data-ttu-id="2ee41-289">Hallo account tooimpersonate tooexecute Hallo Spark programma door de gebruiker</span><span class="sxs-lookup"><span data-stu-id="2ee41-289">hello user account tooimpersonate tooexecute hello Spark program</span></span> | <span data-ttu-id="2ee41-290">Nee</span><span class="sxs-lookup"><span data-stu-id="2ee41-290">No</span></span> |
| <span data-ttu-id="2ee41-291">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="2ee41-291">sparkConfig</span></span> | <span data-ttu-id="2ee41-292">Geef waarden voor Spark configuratie-eigenschappen die worden vermeld in het onderwerp Hallo: [Spark-configuratie - eigenschappen van Application](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span><span class="sxs-lookup"><span data-stu-id="2ee41-292">Specify values for Spark configuration properties listed in hello topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="2ee41-293">Nee</span><span class="sxs-lookup"><span data-stu-id="2ee41-293">No</span></span> |
| <span data-ttu-id="2ee41-294">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="2ee41-294">getDebugInfo</span></span> | <span data-ttu-id="2ee41-295">Geeft aan wanneer Hallo Spark logboekbestanden gekopieerde toohello Azure-opslag die wordt gebruikt door HDInsight-cluster zijn (of) opgegeven door sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="2ee41-295">Specifies when hello Spark log files are copied toohello Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="2ee41-296">Toegestane waarden: None, altijd of fout.</span><span class="sxs-lookup"><span data-stu-id="2ee41-296">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="2ee41-297">Standaardwaarde: geen.</span><span class="sxs-lookup"><span data-stu-id="2ee41-297">Default value: None.</span></span> | <span data-ttu-id="2ee41-298">Nee</span><span class="sxs-lookup"><span data-stu-id="2ee41-298">No</span></span> |
| <span data-ttu-id="2ee41-299">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="2ee41-299">sparkJobLinkedService</span></span> | <span data-ttu-id="2ee41-300">Hallo gekoppelde Azure Storage-service die Hallo Spark taakbestand, afhankelijkheden en Logboeken bevat.</span><span class="sxs-lookup"><span data-stu-id="2ee41-300">hello Azure Storage linked service that holds hello Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="2ee41-301">Als u een waarde op voor deze eigenschap niet opgeeft, wordt Hallo opslag die is gekoppeld aan de HDInsight-cluster gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2ee41-301">If you do not specify a value for this property, hello storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="2ee41-302">Nee</span><span class="sxs-lookup"><span data-stu-id="2ee41-302">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="2ee41-303">Mapstructuur</span><span class="sxs-lookup"><span data-stu-id="2ee41-303">Folder structure</span></span>
<span data-ttu-id="2ee41-304">Hallo Spark activiteit biedt geen ondersteuning voor een in-line-script als Pig en Hive-activiteiten doen.</span><span class="sxs-lookup"><span data-stu-id="2ee41-304">hello Spark activity does not support an in-line script as Pig and Hive activities do.</span></span> <span data-ttu-id="2ee41-305">Spark-taken zijn ook meer extensible dan Pig/Hive-taken.</span><span class="sxs-lookup"><span data-stu-id="2ee41-305">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="2ee41-306">Voor Spark taken, kunt u meerdere afhankelijkheden, zoals opgeven jar-pakketten (in Hallo java CLASSPATH geplaatst), python-bestanden (geplaatst op Hallo PYTHONPATH) en andere bestanden.</span><span class="sxs-lookup"><span data-stu-id="2ee41-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in hello java CLASSPATH), python files (placed on hello PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="2ee41-307">Hallo volgende mapstructuur in hello Azure Blob storage waarnaar wordt verwezen door Hallo gekoppelde HDInsight-service maken.</span><span class="sxs-lookup"><span data-stu-id="2ee41-307">Create hello following folder structure in hello Azure Blob storage referenced by hello HDInsight linked service.</span></span> <span data-ttu-id="2ee41-308">Vervolgens kunt u uploaden afhankelijke bestanden toohello juiste submappen in de hoofdmap Hallo dat wordt vertegenwoordigd door **entryFilePath**.</span><span class="sxs-lookup"><span data-stu-id="2ee41-308">Then, upload dependent files toohello appropriate sub folders in hello root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="2ee41-309">Bijvoorbeeld, python bestanden toohello pyFiles submap en jar-bestanden toohello potten submap van hoofdmap Hallo uploaden.</span><span class="sxs-lookup"><span data-stu-id="2ee41-309">For example, upload python files toohello pyFiles subfolder and jar files toohello jars subfolder of hello root folder.</span></span> <span data-ttu-id="2ee41-310">Tijdens runtime verwacht Data Factory-service Hallo mapstructuur in hello Azure Blob-opslag te volgen:</span><span class="sxs-lookup"><span data-stu-id="2ee41-310">At runtime, Data Factory service expects hello following folder structure in hello Azure Blob storage:</span></span>     

| <span data-ttu-id="2ee41-311">Pad</span><span class="sxs-lookup"><span data-stu-id="2ee41-311">Path</span></span> | <span data-ttu-id="2ee41-312">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2ee41-312">Description</span></span> | <span data-ttu-id="2ee41-313">Vereist</span><span class="sxs-lookup"><span data-stu-id="2ee41-313">Required</span></span> | <span data-ttu-id="2ee41-314">Type</span><span class="sxs-lookup"><span data-stu-id="2ee41-314">Type</span></span> |
| ---- | ----------- | -------- | ---- |
| <span data-ttu-id="2ee41-315">.</span><span class="sxs-lookup"><span data-stu-id="2ee41-315">.</span></span> | <span data-ttu-id="2ee41-316">Hallo hoofdpad van Hallo Spark taak in Hallo opslag gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="2ee41-316">hello root path of hello Spark job in hello storage linked service</span></span>    | <span data-ttu-id="2ee41-317">Ja</span><span class="sxs-lookup"><span data-stu-id="2ee41-317">Yes</span></span> | <span data-ttu-id="2ee41-318">Map</span><span class="sxs-lookup"><span data-stu-id="2ee41-318">Folder</span></span> |
| <span data-ttu-id="2ee41-319">&lt;de gebruiker gedefinieerde&gt;</span><span class="sxs-lookup"><span data-stu-id="2ee41-319">&lt;user defined &gt;</span></span> | <span data-ttu-id="2ee41-320">Hallo pad toohello het gegevensbestand van Hallo Spark taak aan te wijzen</span><span class="sxs-lookup"><span data-stu-id="2ee41-320">hello path pointing toohello entry file of hello Spark job</span></span> | <span data-ttu-id="2ee41-321">Ja</span><span class="sxs-lookup"><span data-stu-id="2ee41-321">Yes</span></span> | <span data-ttu-id="2ee41-322">File</span><span class="sxs-lookup"><span data-stu-id="2ee41-322">File</span></span> |
| <span data-ttu-id="2ee41-323">. / jars</span><span class="sxs-lookup"><span data-stu-id="2ee41-323">./jars</span></span> | <span data-ttu-id="2ee41-324">Alle bestanden onder deze map worden geüpload en op Hallo java klassenpad van Hallo cluster geplaatst</span><span class="sxs-lookup"><span data-stu-id="2ee41-324">All files under this folder are uploaded and placed on hello java classpath of hello cluster</span></span> | <span data-ttu-id="2ee41-325">Nee</span><span class="sxs-lookup"><span data-stu-id="2ee41-325">No</span></span> | <span data-ttu-id="2ee41-326">Map</span><span class="sxs-lookup"><span data-stu-id="2ee41-326">Folder</span></span> |
| <span data-ttu-id="2ee41-327">. / pyFiles</span><span class="sxs-lookup"><span data-stu-id="2ee41-327">./pyFiles</span></span> | <span data-ttu-id="2ee41-328">Alle bestanden onder deze map worden geüpload en op Hallo PYTHONPATH van Hallo cluster geplaatst</span><span class="sxs-lookup"><span data-stu-id="2ee41-328">All files under this folder are uploaded and placed on hello PYTHONPATH of hello cluster</span></span> | <span data-ttu-id="2ee41-329">Nee</span><span class="sxs-lookup"><span data-stu-id="2ee41-329">No</span></span> | <span data-ttu-id="2ee41-330">Map</span><span class="sxs-lookup"><span data-stu-id="2ee41-330">Folder</span></span> |
| <span data-ttu-id="2ee41-331">. / bestanden</span><span class="sxs-lookup"><span data-stu-id="2ee41-331">./files</span></span> | <span data-ttu-id="2ee41-332">Alle bestanden onder deze map worden geüpload en in de werkmap executor geplaatst</span><span class="sxs-lookup"><span data-stu-id="2ee41-332">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="2ee41-333">Nee</span><span class="sxs-lookup"><span data-stu-id="2ee41-333">No</span></span> | <span data-ttu-id="2ee41-334">Map</span><span class="sxs-lookup"><span data-stu-id="2ee41-334">Folder</span></span> |
| <span data-ttu-id="2ee41-335">. / archiveert</span><span class="sxs-lookup"><span data-stu-id="2ee41-335">./archives</span></span> | <span data-ttu-id="2ee41-336">Alle bestanden onder deze map zijn gecomprimeerd</span><span class="sxs-lookup"><span data-stu-id="2ee41-336">All files under this folder are uncompressed</span></span> | <span data-ttu-id="2ee41-337">Nee</span><span class="sxs-lookup"><span data-stu-id="2ee41-337">No</span></span> | <span data-ttu-id="2ee41-338">Map</span><span class="sxs-lookup"><span data-stu-id="2ee41-338">Folder</span></span> |
| <span data-ttu-id="2ee41-339">. / Logboeken</span><span class="sxs-lookup"><span data-stu-id="2ee41-339">./logs</span></span> | <span data-ttu-id="2ee41-340">Hallo-map waarin de logboeken van Hallo Spark-cluster worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2ee41-340">hello folder where logs from hello Spark cluster are stored.</span></span>| <span data-ttu-id="2ee41-341">Nee</span><span class="sxs-lookup"><span data-stu-id="2ee41-341">No</span></span> | <span data-ttu-id="2ee41-342">Map</span><span class="sxs-lookup"><span data-stu-id="2ee41-342">Folder</span></span> |

<span data-ttu-id="2ee41-343">Hier volgt een voorbeeld van een opslagruimte met twee Spark taakbestanden in hello Azure Blob Storage waarnaar wordt verwezen door Hallo gekoppelde HDInsight-service.</span><span class="sxs-lookup"><span data-stu-id="2ee41-343">Here is an example for a storage containing two Spark job files in hello Azure Blob Storage referenced by hello HDInsight linked service.</span></span>

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
