---
title: aangepaste activiteiten in een Azure Data Factory-pijplijn aaaUse
description: Meer informatie over hoe toocreate aangepaste activiteiten en deze gebruiken in een Azure Data Factory-pijplijn.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 23e33727b2160541ab40938ffd911fdd484b3daa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a><span data-ttu-id="701ef-103">Use custom activities in an Azure Data Factory pipeline (Aangepaste activiteiten gebruiken in een Azure Data Factory-pijplijn)</span><span class="sxs-lookup"><span data-stu-id="701ef-103">Use custom activities in an Azure Data Factory pipeline</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="701ef-104">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="701ef-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="701ef-105">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="701ef-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="701ef-106">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="701ef-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="701ef-107">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="701ef-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="701ef-108">Spark-activiteit</span><span class="sxs-lookup"><span data-stu-id="701ef-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="701ef-109">Machine Learning-batchuitvoeringsactiviteit</span><span class="sxs-lookup"><span data-stu-id="701ef-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="701ef-110">Machine Learning-activiteit resources bijwerken</span><span class="sxs-lookup"><span data-stu-id="701ef-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="701ef-111">Opgeslagen procedureactiviteit</span><span class="sxs-lookup"><span data-stu-id="701ef-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="701ef-112">Data Lake Analytics U-SQL-activiteit</span><span class="sxs-lookup"><span data-stu-id="701ef-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="701ef-113">Aangepaste activiteit .NET</span><span class="sxs-lookup"><span data-stu-id="701ef-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="701ef-114">Er zijn twee soorten activiteiten die u in een Azure Data Factory-pijplijn gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="701ef-114">There are two types of activities that you can use in an Azure Data Factory pipeline.</span></span>

- <span data-ttu-id="701ef-115">[Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) toomove gegevens tussen [ondersteunde bron- en sink gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="701ef-115">[Data Movement Activities](data-factory-data-movement-activities.md) toomove data between [supported source and sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>
- <span data-ttu-id="701ef-116">[Activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) tootransform gegevens met behulp van compute-services zoals Azure HDInsight Azure Batch en Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="701ef-116">[Data Transformation Activities](data-factory-data-transformation-activities.md) tootransform data using compute services such as Azure HDInsight, Azure Batch, and Azure Machine Learning.</span></span> 

<span data-ttu-id="701ef-117">toomove gegevens van/naar een gegevensopslag die biedt geen ondersteuning voor Data Factory, maak een **aangepaste activiteit** met uw eigen gegevens gegevensverplaatsing logica en gebruik Hallo activiteit in een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="701ef-117">toomove data to/from a data store that Data Factory does not support, create a **custom activity** with your own data movement logic and use hello activity in a pipeline.</span></span> <span data-ttu-id="701ef-118">Op deze manier tootransform/proces gegevens op een manier die niet wordt ondersteund door Data Factory, een aangepaste activiteit maken met uw eigen logica van de transformatie van gegevens en Hallo-activiteit gebruiken in een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="701ef-118">Similarly, tootransform/process data in a way that isn't supported by Data Factory, create a custom activity with your own data transformation logic and use hello activity in a pipeline.</span></span> 

<span data-ttu-id="701ef-119">U kunt een aangepaste activiteit toorun configureren op een **Azure Batch** pool van virtuele machines of een op Windows gebaseerde **Azure HDInsight** cluster.</span><span class="sxs-lookup"><span data-stu-id="701ef-119">You can configure a custom activity toorun on an **Azure Batch** pool of virtual machines or a Windows-based **Azure HDInsight** cluster.</span></span> <span data-ttu-id="701ef-120">Wanneer u Azure Batch gebruikt, kunt u een bestaande Azure Batch pool.</span><span class="sxs-lookup"><span data-stu-id="701ef-120">When using Azure Batch, you can use only an existing Azure Batch pool.</span></span> <span data-ttu-id="701ef-121">Terwijl bij gebruik van HDInsight, kunt u een bestaand HDInsight-cluster of een cluster dat automatisch wordt gemaakt voor u op aanvraag tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="701ef-121">Whereas, when using HDInsight, you can use an existing HDInsight cluster or a cluster that is automatically created for you on-demand at runtime.</span></span>  

<span data-ttu-id="701ef-122">Hallo bevat volgende overzicht Stapsgewijze instructies voor het maken van een aangepaste .NET-activiteit en gebruik van aangepaste activiteit Hallo in een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="701ef-122">hello following walkthrough provides step-by-step instructions for creating a custom .NET activity and using hello custom activity in a pipeline.</span></span> <span data-ttu-id="701ef-123">Hallo scenario maakt gebruik van een **Azure Batch** gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="701ef-123">hello walkthrough uses an **Azure Batch** linked service.</span></span> <span data-ttu-id="701ef-124">een Azure HDInsight toouse gekoppelde service in plaats daarvan, maakt u een gekoppelde service van het type **HDInsight** (uw eigen HDInsight-cluster) of **HDInsightOnDemand** (Data Factory maakt een HDInsight-cluster op aanvraag).</span><span class="sxs-lookup"><span data-stu-id="701ef-124">toouse an Azure HDInsight linked service instead, you create a linked service of type **HDInsight** (your own HDInsight cluster) or **HDInsightOnDemand** (Data Factory creates an HDInsight cluster on-demand).</span></span> <span data-ttu-id="701ef-125">Configureer vervolgens een aangepaste activiteit toouse Hallo gekoppelde HDInsight-service.</span><span class="sxs-lookup"><span data-stu-id="701ef-125">Then, configure custom activity toouse hello HDInsight linked service.</span></span> <span data-ttu-id="701ef-126">Zie [gebruik Azure HDInsight gekoppelde services](#use-hdinsight-compute-service) sectie voor meer informatie over het gebruik van Azure HDInsight toorun Hallo aangepaste activiteit.</span><span class="sxs-lookup"><span data-stu-id="701ef-126">See [Use Azure HDInsight linked services](#use-hdinsight-compute-service) section for details on using Azure HDInsight toorun hello custom activity.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="701ef-127">Hallo aangepaste .NET-activiteiten alleen op Windows gebaseerde HDInsight-clusters worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="701ef-127">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="701ef-128">Een tijdelijke oplossing voor deze beperking is toouse Hallo kaart verminderen activiteit toorun aangepaste Java-code op een Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="701ef-128">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="701ef-129">Een andere optie is toouse een Azure Batch-pool van virtuele machines toorun aangepaste activiteiten in plaats van een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="701ef-129">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>
> - <span data-ttu-id="701ef-130">Het is niet mogelijk toouse een Data Management Gateway vanuit een aangepaste activiteit tooaccess on-premises-gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="701ef-130">It is not possible toouse a Data Management Gateway from a custom activity tooaccess on-premises data sources.</span></span> <span data-ttu-id="701ef-131">Op dit moment [Data Management Gateway](data-factory-data-management-gateway.md) ondersteunt alleen Hallo kopieeractiviteit en de activiteit opgeslagen procedure in de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="701ef-131">Currently, [Data Management Gateway](data-factory-data-management-gateway.md) supports only hello copy activity and stored procedure activity in Data Factory.</span></span>   

## <a name="walkthrough-create-a-custom-activity"></a><span data-ttu-id="701ef-132">Overzicht: een aangepaste activiteit maken</span><span class="sxs-lookup"><span data-stu-id="701ef-132">Walkthrough: create a custom activity</span></span>
### <a name="prerequisites"></a><span data-ttu-id="701ef-133">Vereisten</span><span class="sxs-lookup"><span data-stu-id="701ef-133">Prerequisites</span></span>
* <span data-ttu-id="701ef-134">Visual Studio 2012-2013-2015</span><span class="sxs-lookup"><span data-stu-id="701ef-134">Visual Studio 2012/2013/2015</span></span>
* <span data-ttu-id="701ef-135">Download en installeer [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="701ef-135">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span></span>

### <a name="azure-batch-prerequisites"></a><span data-ttu-id="701ef-136">Vereisten voor Azure Batch</span><span class="sxs-lookup"><span data-stu-id="701ef-136">Azure Batch prerequisites</span></span>
<span data-ttu-id="701ef-137">In Hallo scenario maakt uitvoeren u uw aangepaste .NET-activiteiten met behulp van Azure Batch als een berekeningsresource.</span><span class="sxs-lookup"><span data-stu-id="701ef-137">In hello walkthrough, you run your custom .NET activities using Azure Batch as a compute resource.</span></span> <span data-ttu-id="701ef-138">**Azure Batch** is een platform service voor het uitvoeren van grootschalige parallelle en high-performance computing (HPC) toepassingen efficiënt in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="701ef-138">**Azure Batch** is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="701ef-139">Azure Batch plant toorun rekenintensief werk op een beheerde **verzameling van virtuele machines**, en kan automatisch scale compute resources toomeet Hallo behoeften van uw jobs.</span><span class="sxs-lookup"><span data-stu-id="701ef-139">Azure Batch schedules compute-intensive work toorun on a managed **collection of virtual machines**, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span> <span data-ttu-id="701ef-140">Zie [basisbeginselen van Azure Batch] [ batch-technical-overview] artikel voor een gedetailleerd overzicht van hello Azure Batch-service.</span><span class="sxs-lookup"><span data-stu-id="701ef-140">See [Azure Batch basics][batch-technical-overview] article for a detailed overview of hello Azure Batch service.</span></span>

<span data-ttu-id="701ef-141">Hallo-zelfstudie Azure Batch-account te maken met een pool van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="701ef-141">For hello tutorial, create an Azure Batch account with a pool of VMs.</span></span> <span data-ttu-id="701ef-142">Hier volgen Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="701ef-142">Here are hello steps:</span></span>

1. <span data-ttu-id="701ef-143">Maak een **Azure Batch-account** met Hallo [Azure-portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="701ef-143">Create an **Azure Batch account** using hello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="701ef-144">Zie [maken en beheren van Azure Batch-account] [ batch-create-account] artikel voor instructies.</span><span class="sxs-lookup"><span data-stu-id="701ef-144">See [Create and manage an Azure Batch account][batch-create-account] article for instructions.</span></span>
2. <span data-ttu-id="701ef-145">Noteer hello Azure Batch-accountnaam, accountsleutel URI en de naam van de groep van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="701ef-145">Note down hello Azure Batch account name, account key, URI, and pool name.</span></span> <span data-ttu-id="701ef-146">U moet ze toocreate een gekoppelde Azure-Batch-service.</span><span class="sxs-lookup"><span data-stu-id="701ef-146">You need them toocreate an Azure Batch linked service.</span></span>
    1. <span data-ttu-id="701ef-147">Op Hallo startpagina van Azure Batch-account, ziet u een **URL** in Hallo volgende indeling: `https://myaccount.westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="701ef-147">On hello home page for Azure Batch account, you see a **URL** in hello following format: `https://myaccount.westus.batch.azure.com`.</span></span> <span data-ttu-id="701ef-148">In dit voorbeeld **myaccount** Hallo naam is van hello Azure Batch-account.</span><span class="sxs-lookup"><span data-stu-id="701ef-148">In this example, **myaccount** is hello name of hello Azure Batch account.</span></span> <span data-ttu-id="701ef-149">U in de servicedefinitie Hallo gekoppeld gebruikt-URI is Hallo URL zonder Hallo-naam van het Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="701ef-149">URI you use in hello linked service definition is hello URL without hello name of hello account.</span></span> <span data-ttu-id="701ef-150">Bijvoorbeeld: `https://<region>.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="701ef-150">For example: `https://<region>.batch.azure.com`.</span></span>
    2. <span data-ttu-id="701ef-151">Klik op **sleutels** op Hallo linkermenu en kopiëren Hallo **primaire TOEGANGSSLEUTEL**.</span><span class="sxs-lookup"><span data-stu-id="701ef-151">Click **Keys** on hello left menu, and copy hello **PRIMARY ACCESS KEY**.</span></span>
    3. <span data-ttu-id="701ef-152">toouse een bestaande groep, klikt u op **Pools** op Hallo menu en noteer Hallo **ID** van Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="701ef-152">toouse an existing pool, click **Pools** on hello menu, and note down hello **ID** of hello pool.</span></span> <span data-ttu-id="701ef-153">Als u een bestaande toepassingen hebt, verplaatst u de volgende stap toohello.</span><span class="sxs-lookup"><span data-stu-id="701ef-153">If you don't have an existing pool, move toohello next step.</span></span>     
2. <span data-ttu-id="701ef-154">Maak een **Azure Batch-pool**.</span><span class="sxs-lookup"><span data-stu-id="701ef-154">Create an **Azure Batch pool**.</span></span>

   1. <span data-ttu-id="701ef-155">In Hallo [Azure-portal](https://portal.azure.com), klikt u op **Bladeren** in Hallo menu aan de linkerkant en klik op **Batch-Accounts**.</span><span class="sxs-lookup"><span data-stu-id="701ef-155">In hello [Azure portal](https://portal.azure.com), click **Browse** in hello left menu, and click **Batch Accounts**.</span></span>
   2. <span data-ttu-id="701ef-156">Selecteer uw Azure Batch-account tooopen hello **Batch-Account** blade.</span><span class="sxs-lookup"><span data-stu-id="701ef-156">Select your Azure Batch account tooopen hello **Batch Account** blade.</span></span>
   3. <span data-ttu-id="701ef-157">Klik op **Pools** tegel.</span><span class="sxs-lookup"><span data-stu-id="701ef-157">Click **Pools** tile.</span></span>
   4. <span data-ttu-id="701ef-158">In Hallo **Pools** blade, klik op de knop toevoegen op Hallo werkbalk tooadd een pool.</span><span class="sxs-lookup"><span data-stu-id="701ef-158">In hello **Pools** blade, click Add button on hello toolbar tooadd a pool.</span></span>
      1. <span data-ttu-id="701ef-159">Geef een ID voor Hallo van toepassingen (groep-ID).</span><span class="sxs-lookup"><span data-stu-id="701ef-159">Enter an ID for hello pool (Pool ID).</span></span> <span data-ttu-id="701ef-160">Opmerking Hallo **ID van de pool Hallo**; u deze nodig hebt bij het maken van Hallo Data Factory-oplossing.</span><span class="sxs-lookup"><span data-stu-id="701ef-160">Note hello **ID of hello pool**; you need it when creating hello Data Factory solution.</span></span>
      2. <span data-ttu-id="701ef-161">Geef **Windows Server 2012 R2** voor Hallo besturingssysteemgroep instelling.</span><span class="sxs-lookup"><span data-stu-id="701ef-161">Specify **Windows Server 2012 R2** for hello Operating System Family setting.</span></span>
      3. <span data-ttu-id="701ef-162">Selecteer een **knooppunt prijscategorie**.</span><span class="sxs-lookup"><span data-stu-id="701ef-162">Select a **node pricing tier**.</span></span>
      4. <span data-ttu-id="701ef-163">Voer **2** als waarde voor Hallo **doel toegewezen** instelling.</span><span class="sxs-lookup"><span data-stu-id="701ef-163">Enter **2** as value for hello **Target Dedicated** setting.</span></span>
      5. <span data-ttu-id="701ef-164">Voer **2** als waarde voor Hallo **maximum aantal taken per knooppunt** instelling.</span><span class="sxs-lookup"><span data-stu-id="701ef-164">Enter **2** as value for hello **Max tasks per node** setting.</span></span>
   5. <span data-ttu-id="701ef-165">Klik op **OK** toocreate Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="701ef-165">Click **OK** toocreate hello pool.</span></span>
   6. <span data-ttu-id="701ef-166">Noteer Hallo **ID** van Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="701ef-166">Note down hello **ID** of hello pool.</span></span> 



### <a name="high-level-steps"></a><span data-ttu-id="701ef-167">Stappen op hoog niveau</span><span class="sxs-lookup"><span data-stu-id="701ef-167">High-level steps</span></span>
<span data-ttu-id="701ef-168">Hier volgen Hallo twee stappen op hoog niveau die u als onderdeel van dit scenario uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="701ef-168">Here are hello two high-level steps you perform as part of this walkthrough:</span></span> 

1. <span data-ttu-id="701ef-169">Maak een aangepaste activiteit die eenvoudige transformatie/verwerking logica bevat.</span><span class="sxs-lookup"><span data-stu-id="701ef-169">Create a custom activity that contains simple data transformation/processing logic.</span></span>
2. <span data-ttu-id="701ef-170">Maak een Azure data factory met een pipeline die gebruikmaakt van Hallo aangepaste activiteit.</span><span class="sxs-lookup"><span data-stu-id="701ef-170">Create an Azure data factory with a pipeline that uses hello custom activity.</span></span>

### <a name="create-a-custom-activity"></a><span data-ttu-id="701ef-171">Een aangepaste activiteit maken</span><span class="sxs-lookup"><span data-stu-id="701ef-171">Create a custom activity</span></span>
<span data-ttu-id="701ef-172">maken van een aangepaste activiteit .NET toocreate een **.NET Class Library** project met een klasse die die implementeert **IDotNetActivity** interface.</span><span class="sxs-lookup"><span data-stu-id="701ef-172">toocreate a .NET custom activity, create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="701ef-173">Deze interface heeft slechts één methode: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) en de handtekening is:</span><span class="sxs-lookup"><span data-stu-id="701ef-173">This interface has only one method: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) and its signature is:</span></span>

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


<span data-ttu-id="701ef-174">Hallo-methode heeft vier parameters:</span><span class="sxs-lookup"><span data-stu-id="701ef-174">hello method takes four parameters:</span></span>

- <span data-ttu-id="701ef-175">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="701ef-175">**linkedServices**.</span></span> <span data-ttu-id="701ef-176">Deze eigenschap is een inventariseerbare lijst van gegevensarchief gekoppelde services waarnaar wordt verwezen door een i/o-gegevenssets voor Hallo-activiteit.</span><span class="sxs-lookup"><span data-stu-id="701ef-176">This property is an enumerable list of Data Store linked services referenced by input/output datasets for hello activity.</span></span>   
- <span data-ttu-id="701ef-177">**gegevenssets**.</span><span class="sxs-lookup"><span data-stu-id="701ef-177">**datasets**.</span></span> <span data-ttu-id="701ef-178">Deze eigenschap is een inventariseerbare lijst van i/o-gegevenssets voor Hallo-activiteit.</span><span class="sxs-lookup"><span data-stu-id="701ef-178">This property is an enumerable list of input/output datasets for hello activity.</span></span> <span data-ttu-id="701ef-179">U kunt deze parameter tooget Hallo locaties en schema's die zijn gedefinieerd door de invoer- en uitvoergegevenssets gebruiken.</span><span class="sxs-lookup"><span data-stu-id="701ef-179">You can use this parameter tooget hello locations and schemas defined by input and output datasets.</span></span>
- <span data-ttu-id="701ef-180">**activiteit**.</span><span class="sxs-lookup"><span data-stu-id="701ef-180">**activity**.</span></span> <span data-ttu-id="701ef-181">Deze eigenschap vertegenwoordigt de huidige activiteit Hallo.</span><span class="sxs-lookup"><span data-stu-id="701ef-181">This property represents hello current activity.</span></span> <span data-ttu-id="701ef-182">Het kan gebruikte tooaccess uitgebreide eigenschappen die zijn gekoppeld aan de aangepaste activiteit Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="701ef-182">It can be used tooaccess extended properties associated with hello custom activity.</span></span> <span data-ttu-id="701ef-183">Zie [toegang uitgebreide eigenschappen](#access-extended-properties) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="701ef-183">See [Access extended properties](#access-extended-properties) for details.</span></span>
- <span data-ttu-id="701ef-184">**Berichtenlogboek**.</span><span class="sxs-lookup"><span data-stu-id="701ef-184">**logger**.</span></span> <span data-ttu-id="701ef-185">Dit object kunt u foutopsporing opmerkingen die surface schrijven in Hallo gebruikersaanmelding voor Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="701ef-185">This object lets you write debug comments that surface in hello user log for hello pipeline.</span></span>

<span data-ttu-id="701ef-186">Hallo-methode retourneert een woordenlijst die gebruikt toochain aangepaste activiteiten samen in de toekomst Hallo worden kan.</span><span class="sxs-lookup"><span data-stu-id="701ef-186">hello method returns a dictionary that can be used toochain custom activities together in hello future.</span></span> <span data-ttu-id="701ef-187">Deze functie is nog niet geïmplementeerd, kunt u dus een woordenboek leeg retourneren van Hallo-methode.</span><span class="sxs-lookup"><span data-stu-id="701ef-187">This feature is not implemented yet, so return an empty dictionary from hello method.</span></span>  

### <a name="procedure"></a><span data-ttu-id="701ef-188">Procedure</span><span class="sxs-lookup"><span data-stu-id="701ef-188">Procedure</span></span>
1. <span data-ttu-id="701ef-189">Maak een **.NET Class Library** project.</span><span class="sxs-lookup"><span data-stu-id="701ef-189">Create a **.NET Class Library** project.</span></span>
   <ol type="a">
     <li><span data-ttu-id="701ef-190">Start <b>Visual Studio 2017</b> of <b>Visual Studio 2015</b> of <b>Visual Studio 2013</b> of <b>Visual Studio 2012</b>.</span><span class="sxs-lookup"><span data-stu-id="701ef-190">Launch <b>Visual Studio 2017</b> or <b>Visual Studio 2015</b> or <b>Visual Studio 2013</b> or <b>Visual Studio 2012</b>.</span></span></li>
     <li><span data-ttu-id="701ef-191">Klik op <b>bestand</b>, wijst u te<b>nieuw</b>, en klik op <b>Project</b>.</span><span class="sxs-lookup"><span data-stu-id="701ef-191">Click <b>File</b>, point too<b>New</b>, and click <b>Project</b>.</span></span></li>
     <li><span data-ttu-id="701ef-192">Vouw <b>Templates</b> uit en selecteer <b>Visual C#</b>.</span><span class="sxs-lookup"><span data-stu-id="701ef-192">Expand <b>Templates</b>, and select <b>Visual C#</b>.</span></span> <span data-ttu-id="701ef-193">In dit scenario maakt u gebruik C#, maar kunt u een .NET taal toodevelop Hallo aangepaste activiteit.</span><span class="sxs-lookup"><span data-stu-id="701ef-193">In this walkthrough, you use C#, but you can use any .NET language toodevelop hello custom activity.</span></span></li>
     <li><span data-ttu-id="701ef-194">Selecteer <b>Class Library</b> uit de lijst Hallo van projecttypen op Hallo rechts.</span><span class="sxs-lookup"><span data-stu-id="701ef-194">Select <b>Class Library</b> from hello list of project types on hello right.</span></span> <span data-ttu-id="701ef-195">Kies in de VS 2017 <b>Class Library (.NET Framework)</b> </span><span class="sxs-lookup"><span data-stu-id="701ef-195">In VS 2017, choose <b>Class Library (.NET Framework)</b> </span></span></li>
     <li><span data-ttu-id="701ef-196">Voer <b>MyDotNetActivity</b> voor Hallo <b>naam</b>.</span><span class="sxs-lookup"><span data-stu-id="701ef-196">Enter <b>MyDotNetActivity</b> for hello <b>Name</b>.</span></span></li>
     <li><span data-ttu-id="701ef-197">Selecteer <b>C:\ADFGetStarted</b> voor Hallo <b>locatie</b>.</span><span class="sxs-lookup"><span data-stu-id="701ef-197">Select <b>C:\ADFGetStarted</b> for hello <b>Location</b>.</span></span></li>
     <li><span data-ttu-id="701ef-198">Klik op <b>OK</b> toocreate Hallo project.</span><span class="sxs-lookup"><span data-stu-id="701ef-198">Click <b>OK</b> toocreate hello project.</span></span></li>
   </ol><span data-ttu-id="701ef-199">
2.Klik op **extra**, wijst u te**NuGet Package Manager**, en klik op **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="701ef-199">
2. Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
<span data-ttu-id="701ef-200">3.</span><span class="sxs-lookup"><span data-stu-id="701ef-200">3.</span></span> <span data-ttu-id="701ef-201">In Hallo Package Manager-Console, uitvoeren na de opdracht tooimport hello **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="701ef-201">In hello Package Manager Console, execute hello following command tooimport **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="701ef-202">Importeren Hallo **Azure Storage** NuGet-pakket in toohello-project.</span><span class="sxs-lookup"><span data-stu-id="701ef-202">Import hello **Azure Storage** NuGet package in toohello project.</span></span>

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="701ef-203">Data Factory-service starten vereist Hallo 4.3-versie van WindowsAzure.Storage.</span><span class="sxs-lookup"><span data-stu-id="701ef-203">Data Factory service launcher requires hello 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="701ef-204">Als u een tooa verwijzing toevoegt latere versie van Azure Storage-assembly in uw project aangepaste activiteit er een foutbericht wanneer Hallo activiteit wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="701ef-204">If you add a reference tooa later version of Azure Storage assembly in your custom activity project, you see an error when hello activity executes.</span></span> <span data-ttu-id="701ef-205">tooresolve hello fout, Zie [Appdomain isolatie](#appdomain-isolation) sectie.</span><span class="sxs-lookup"><span data-stu-id="701ef-205">tooresolve hello error, see [Appdomain isolation](#appdomain-isolation) section.</span></span> 
5. <span data-ttu-id="701ef-206">Voeg de volgende Hallo **met** instructies toohello bronbestand in Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="701ef-206">Add hello following **using** statements toohello source file in hello project.</span></span>

    ```csharp

    // Comment these lines if using VS 2017
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    // --------------------

    // Comment these lines if using <= VS 2015
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    // ---------------------

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="701ef-207">Hallo naam wijzigen van Hallo **naamruimte** te**MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="701ef-207">Change hello name of hello **namespace** too**MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="701ef-208">Hallo-naam van de klasse Hallo te wijzigen**MyDotNetActivity** en afgeleid Hallo **IDotNetActivity** interface zoals weergegeven in het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="701ef-208">Change hello name of hello class too**MyDotNetActivity** and derive it from hello **IDotNetActivity** interface as shown in hello following code snippet:</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="701ef-209">Hallo implementeren (toevoegen) **Execute** methode Hallo **IDotNetActivity** interface toohello **MyDotNetActivity** klasse en kopieer Hallo voorbeeldmethode code toohello te volgen.</span><span class="sxs-lookup"><span data-stu-id="701ef-209">Implement (Add) hello **Execute** method of hello **IDotNetActivity** interface toohello **MyDotNetActivity** class and copy hello following sample code toohello method.</span></span>

    <span data-ttu-id="701ef-210">Hallo telt volgende voorbeeld Hallo aantal exemplaren van Hallo zoekterm ('Microsoft') in elke blob die is gekoppeld aan een gegevenssegment.</span><span class="sxs-lookup"><span data-stu-id="701ef-210">hello following sample counts hello number of occurrences of hello search term (“Microsoft”) in each blob associated with a data slice.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
    /// </summary>
    
    public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
    {
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // toolog information, use hello logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get hello input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables toohold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from hello dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and hello other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get hello first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using hello same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get hello connection string in hello linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get hello folder path from hello input dataset definition
        string folderPath = GetFolderPath(inputDataset);
        string output = string.Empty; // for use later.
    
        // create storage client for input. Pass hello connection string.
        CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
        CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
        // initialize hello continuation token before using it in hello do-while loop.
        BlobContinuationToken continuationToken = null;
        do
        {   // get hello list of input blobs from hello input storage client object.
            BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                     true,
                                     BlobListingDetails.Metadata,
                                     null,
                                     continuationToken,
                                     null,
                                     null);
    
            // Calculate method returns hello number of occurrences of
            // hello search term (“Microsoft”) in each blob associated
               // with hello data slice. definition of hello method is shown in hello next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for hello output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get hello folder path from hello output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log hello output folder path 
        logger.Write("Writing blob toohello folder: {0}", folderPath);
    
        // create a storage object for hello output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write hello name of hello file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log hello output file name
        logger.Write("output blob URI: {0}", outputBlobUri.ToString());

        // create a blob and upload hello output text.
        CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
        logger.Write("Writing {0} toohello output blob", output);
        outputBlob.UploadText(output);
    
        // hello dictionary can be used toochain custom activities together in hello future.
        // This feature is not implemented yet, so just return an empty dictionary.  
    
        return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="701ef-211">Hallo volgende Help-methoden toevoegen:</span><span class="sxs-lookup"><span data-stu-id="701ef-211">Add hello following helper methods:</span></span> 

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    
    private static string GetFolderPath(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }

        // get type properties of hello dataset 
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello folder path found in hello type properties
        return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.   
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }
    
        // get type properties of hello dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello blob/file name in hello type properties
        return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
        string output = string.Empty;
        logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
        foreach (IListBlobItem listBlobItem in Bresult.Results)
        {
            CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
            if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
            {
                string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
                logger.Write("input blob text: {0}", blobText);
                string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
                var matchQuery = from word in source
                                 where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                 select word;
                int wordCount = matchQuery.Count();
                output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
            }
        }
        return output;
    }
    ```

    <span data-ttu-id="701ef-212">Hallo GetFolderPath methode retourneert Hallo pad toohello map Hallo gegevensset tooand Hallo GetFileName retourneert Hallo methodenaam van Hallo-blob /-bestand dat verwijst naar gegevensset Hallo verwijst.</span><span class="sxs-lookup"><span data-stu-id="701ef-212">hello GetFolderPath method returns hello path toohello folder that hello dataset points tooand hello GetFileName method returns hello name of hello blob/file that hello dataset points to.</span></span> <span data-ttu-id="701ef-213">Als u havefolderPath is gedefinieerd met behulp van de variabelen zoals {Year}, {Month}, {Day} enz., Hallo-methode retourneert Hallo tekenreeks omdat deze zonder deze te vervangen door waarden van de runtime.</span><span class="sxs-lookup"><span data-stu-id="701ef-213">If you havefolderPath defines using variables such as {Year}, {Month}, {Day} etc., hello method returns hello string as it is without replacing them with runtime values.</span></span> <span data-ttu-id="701ef-214">Zie [toegang uitgebreide eigenschappen](#access-extended-properties) sectie voor meer informatie over de toegang tot SliceStart, SliceEnd, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="701ef-214">See [Access extended properties](#access-extended-properties) section for details on accessing SliceStart, SliceEnd, etc.</span></span>    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    <span data-ttu-id="701ef-215">Hallo berekeningsmethode berekent Hallo aantal exemplaren van het sleutelwoord Microsoft in Hallo invoerbestanden (BLOB's in de map Hallo).</span><span class="sxs-lookup"><span data-stu-id="701ef-215">hello Calculate method calculates hello number of instances of keyword Microsoft in hello input files (blobs in hello folder).</span></span> <span data-ttu-id="701ef-216">Hallo zoekterm ('Microsoft') is vastgelegd in het Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="701ef-216">hello search term (“Microsoft”) is hard-coded in hello code.</span></span>
10. <span data-ttu-id="701ef-217">Hallo project compileren.</span><span class="sxs-lookup"><span data-stu-id="701ef-217">Compile hello project.</span></span> <span data-ttu-id="701ef-218">Klik op **bouwen** uit en klik op Hallo **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="701ef-218">Click **Build** from hello menu and click **Build Solution**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="701ef-219">Stel 4.5.2 de versie van .NET Framework als doel-framework voor uw project Hallo: met de rechtermuisknop op het Hallo-project en klik op **eigenschappen** tooset Hallo doel-framework.</span><span class="sxs-lookup"><span data-stu-id="701ef-219">Set 4.5.2 version of .NET Framework as hello target framework for your project: right-click hello project, and click **Properties** tooset hello target framework.</span></span> <span data-ttu-id="701ef-220">Data Factory biedt geen ondersteuning voor aangepaste activiteiten gecompileerd met .NET Framework-versies hoger is dan 4.5.2.</span><span class="sxs-lookup"><span data-stu-id="701ef-220">Data Factory does not support custom activities compiled against .NET Framework versions later than 4.5.2.</span></span>

11. <span data-ttu-id="701ef-221">Start **Windows Verkenner**, en te navigeren**bin\debug** of **bin\release** map afhankelijk van Hallo type build.</span><span class="sxs-lookup"><span data-stu-id="701ef-221">Launch **Windows Explorer**, and navigate too**bin\debug** or **bin\release** folder depending on hello type of build.</span></span>
12. <span data-ttu-id="701ef-222">Maak een zipbestand **MyDotNetActivity.zip** die alle Hallo binaire bestanden in Hallo bevat <project folder>map \bin\Debug.</span><span class="sxs-lookup"><span data-stu-id="701ef-222">Create a zip file **MyDotNetActivity.zip** that contains all hello binaries in hello <project folder>\bin\Debug folder.</span></span> <span data-ttu-id="701ef-223">Hallo omvatten **MyDotNetActivity.pdb** zodat u aanvullende informatie zoals regelnummer in de broncode Hallo die Hallo probleem veroorzaakt ophalen als er een fout is het bestand.</span><span class="sxs-lookup"><span data-stu-id="701ef-223">Include hello **MyDotNetActivity.pdb** file so that you get additional details such as line number in hello source code that caused hello issue if there was a failure.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="701ef-224">Alle bestanden in het zip-bestand Hallo Hallo voor Hallo aangepaste activiteit op Hallo moet **bovenste niveau** met geen submappen.</span><span class="sxs-lookup"><span data-stu-id="701ef-224">All hello files in hello zip file for hello custom activity must be at hello **top level** with no sub folders.</span></span>

    ![Binaire uitvoerbestanden](./media/data-factory-use-custom-activities/Binaries.png)
14. <span data-ttu-id="701ef-226">Maak een blobcontainer met de naam **customactivitycontainer** als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="701ef-226">Create a blob container named **customactivitycontainer** if it does not already exist.</span></span> 
15. <span data-ttu-id="701ef-227">MyDotNetActivity.zip uploaden als een blob toohello customactivitycontainer in een **algemeen** Azure blob-opslag (geen hot/cool Blob-opslag) waarnaar wordt verwezen door AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="701ef-227">Upload MyDotNetActivity.zip as a blob toohello customactivitycontainer in a **general-purpose** Azure blob storage (not hot/cool Blob storage) that is referred by AzureStorageLinkedService.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="701ef-228">Als u deze .NET activiteit project tooa oplossing in Visual Studio met een Data Factory-project toevoegen en voeg een verwijzing too.NET activiteit-project uit Hallo Data Factory-toepassingsproject, hoeft u niet tooperform Hallo laatste twee stappen voor het handmatig maken Hallo zip-bestand en uploaden toohello algemeen Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="701ef-228">If you add this .NET activity project tooa solution in Visual Studio that contains a Data Factory project, and add a reference too.NET activity project from hello Data Factory application project, you do not need tooperform hello last two steps of manually creating hello zip file and uploading it toohello general-purpose Azure blob storage.</span></span> <span data-ttu-id="701ef-229">Wanneer u met behulp van Visual Studio Data Factory-entiteiten publiceert, worden deze stappen automatisch uitgevoerd door Hallo publicatieproces.</span><span class="sxs-lookup"><span data-stu-id="701ef-229">When you publish Data Factory entities using Visual Studio, these steps are automatically done by hello publishing process.</span></span> <span data-ttu-id="701ef-230">Zie voor meer informatie [Data Factory-project in Visual Studio](#data-factory-project-in-visual-studio) sectie.</span><span class="sxs-lookup"><span data-stu-id="701ef-230">For more information, see [Data Factory project in Visual Studio](#data-factory-project-in-visual-studio) section.</span></span>

## <a name="create-a-pipeline-with-custom-activity"></a><span data-ttu-id="701ef-231">Een pijplijn maken met aangepaste activiteit</span><span class="sxs-lookup"><span data-stu-id="701ef-231">Create a pipeline with custom activity</span></span>
<span data-ttu-id="701ef-232">U hebt gemaakt van een aangepaste activiteit en geüpload Hallo zip-bestand met de binaire bestanden tooa blob-container in een **algemeen** Azure Storage-Account.</span><span class="sxs-lookup"><span data-stu-id="701ef-232">You have created a custom activity and uploaded hello zip file with binaries tooa blob container in a **general-purpose** Azure Storage Account.</span></span> <span data-ttu-id="701ef-233">In deze sectie maakt u een Azure data factory met een pipeline die gebruikmaakt van aangepaste activiteit Hallo.</span><span class="sxs-lookup"><span data-stu-id="701ef-233">In this section, you create an Azure data factory with a pipeline that uses hello custom activity.</span></span>

<span data-ttu-id="701ef-234">Hallo invoergegevensset voor Hallo aangepaste activiteit vertegenwoordigt BLOB's (bestanden) in Hallo customactivityinput map van de container adftutorial in Hallo blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="701ef-234">hello input dataset for hello custom activity represents blobs (files) in hello customactivityinput folder of adftutorial container in hello blob storage.</span></span> <span data-ttu-id="701ef-235">Hallo uitvoergegevensset voor Hallo activiteit vertegenwoordigt uitvoer blobs in Hallo customactivityoutput map van de container adftutorial in Hallo blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="701ef-235">hello output dataset for hello activity represents output blobs in hello customactivityoutput folder of adftutorial container in hello blob storage.</span></span>

<span data-ttu-id="701ef-236">Maak **bestand.txt** bestand met de Hallo volgende inhoud en te uploaden**customactivityinput** map Hallo **adftutorial** container.</span><span class="sxs-lookup"><span data-stu-id="701ef-236">Create **file.txt** file with hello following content and upload it too**customactivityinput** folder of hello **adftutorial** container.</span></span> <span data-ttu-id="701ef-237">Hallo adftutorial container maken als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="701ef-237">Create hello adftutorial container if it does not exist already.</span></span> 

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="701ef-238">Hallo invoermap komt overeen tooa segment in Azure Data Factory, zelfs als de map Hallo twee of meer bestanden heeft.</span><span class="sxs-lookup"><span data-stu-id="701ef-238">hello input folder corresponds tooa slice in Azure Data Factory even if hello folder has two or more files.</span></span> <span data-ttu-id="701ef-239">Wanneer elk segment wordt verwerkt door de pijplijn hello, doorlopen aangepaste activiteit Hallo alle Hallo blobs in de invoermap Hallo voor dat segment.</span><span class="sxs-lookup"><span data-stu-id="701ef-239">When each slice is processed by hello pipeline, hello custom activity iterates through all hello blobs in hello input folder for that slice.</span></span>

<span data-ttu-id="701ef-240">Ziet u een bestand met in Hallo adftutorial\customactivityoutput map uitvoer met een of meer regels (zelfde als aantal blobs in de invoermap Hallo):</span><span class="sxs-lookup"><span data-stu-id="701ef-240">You see one output file with in hello adftutorial\customactivityoutput folder with one or more lines (same as number of blobs in hello input folder):</span></span>

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
```


<span data-ttu-id="701ef-241">Hier volgen Hallo stappen die u in deze sectie uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="701ef-241">Here are hello steps you perform in this section:</span></span>

1. <span data-ttu-id="701ef-242">Maak een **gegevensfactory**.</span><span class="sxs-lookup"><span data-stu-id="701ef-242">Create a **data factory**.</span></span>
2. <span data-ttu-id="701ef-243">Maak **gekoppelde services** voor hello Azure Batch-pool van virtuele machines op welke Hallo aangepaste activiteit wordt uitgevoerd en hello Azure Storage dat Hallo invoer/uitvoer-BLOB's bevat.</span><span class="sxs-lookup"><span data-stu-id="701ef-243">Create **Linked services** for hello Azure Batch pool of VMs on which hello custom activity runs and hello Azure Storage that holds hello input/output blobs.</span></span>
3. <span data-ttu-id="701ef-244">Maken van de invoer en uitvoer **gegevenssets** die invoer en uitvoer van de aangepaste activiteit Hallo staan.</span><span class="sxs-lookup"><span data-stu-id="701ef-244">Create input and output **datasets** that represent input and output of hello custom activity.</span></span>
4. <span data-ttu-id="701ef-245">Maak een **pijplijn** die gebruikmaakt van Hallo aangepaste activiteit.</span><span class="sxs-lookup"><span data-stu-id="701ef-245">Create a **pipeline** that uses hello custom activity.</span></span>

> [!NOTE]
> <span data-ttu-id="701ef-246">Hallo maken **bestand.txt** en upload het blob-container tooa als u dat nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="701ef-246">Create hello **file.txt** and upload it tooa blob container if you haven't already done so.</span></span> <span data-ttu-id="701ef-247">Zie de instructies in de voorgaande sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="701ef-247">See instructions in hello preceding section.</span></span>   

### <a name="step-1-create-hello-data-factory"></a><span data-ttu-id="701ef-248">Stap 1: Hallo een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="701ef-248">Step 1: Create hello data factory</span></span>
1. <span data-ttu-id="701ef-249">Na het aanmelden toohello Azure-portal, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="701ef-249">After logging in toohello Azure portal, do hello following steps:</span></span>
   1. <span data-ttu-id="701ef-250">Klik op **nieuw** op Hallo linkermenu.</span><span class="sxs-lookup"><span data-stu-id="701ef-250">Click **NEW** on hello left menu.</span></span>
   2. <span data-ttu-id="701ef-251">Klik op **gegevens en analyse** in Hallo **nieuw** blade.</span><span class="sxs-lookup"><span data-stu-id="701ef-251">Click **Data + Analytics** in hello **New** blade.</span></span>
   3. <span data-ttu-id="701ef-252">Klik op **Data Factory** op Hallo **gegevensanalyse** blade.</span><span class="sxs-lookup"><span data-stu-id="701ef-252">Click **Data Factory** on hello **Data analytics** blade.</span></span>
   
    ![Nieuwe Azure Data Factory-menu](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. <span data-ttu-id="701ef-254">In Hallo **nieuwe gegevensfactory** blade Voer **CustomActivityFactory** voor Hallo naam.</span><span class="sxs-lookup"><span data-stu-id="701ef-254">In hello **New data factory** blade, enter **CustomActivityFactory** for hello Name.</span></span> <span data-ttu-id="701ef-255">Hallo-naam van hello Azure-gegevensfactory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="701ef-255">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="701ef-256">Als u de foutmelding Hallo: **Data factory-naam 'CustomActivityFactory' is niet beschikbaar**, Hallo-naam van gegevensfactory Hallo wijzigen (bijvoorbeeld **yournameCustomActivityFactory**) en probeert te maken opnieuw.</span><span class="sxs-lookup"><span data-stu-id="701ef-256">If you receive hello error: **Data factory name “CustomActivityFactory” is not available**, change hello name of hello data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>

    ![Nieuwe Azure Data Factory-blade](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. <span data-ttu-id="701ef-258">Klik op **RESOURCEGROEPNAAM**, en selecteer een bestaande resourcegroep of maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="701ef-258">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="701ef-259">Controleer of u Hallo juist **abonnement** en **regio** waar u Hallo data factory toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="701ef-259">Verify that you are using hello correct **subscription** and **region** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="701ef-260">Klik op **maken** op Hallo **nieuwe gegevensfactory** blade.</span><span class="sxs-lookup"><span data-stu-id="701ef-260">Click **Create** on hello **New data factory** blade.</span></span>
6. <span data-ttu-id="701ef-261">Zie van Hallo gegevensfactory wordt gemaakt in Hallo **Dashboard** Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="701ef-261">You see hello data factory being created in hello **Dashboard** of hello Azure portal.</span></span>
7. <span data-ttu-id="701ef-262">Nadat het Hallo gegevensfactory is gemaakt, ziet u de Data Factory-blade hello, waarin u inhoud van de gegevensfactory Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="701ef-262">After hello data factory has been created successfully, you see hello Data Factory blade, which shows you hello contents of hello data factory.</span></span>
    
    ![Blade Gegevensfactory](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a><span data-ttu-id="701ef-264">Stap 2: Gekoppelde services maken</span><span class="sxs-lookup"><span data-stu-id="701ef-264">Step 2: Create linked services</span></span>
<span data-ttu-id="701ef-265">Gekoppelde services worden gegevensarchieven of compute-services tooan Azure-gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="701ef-265">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="701ef-266">In deze stap koppelt u uw Azure Storage-account en de Azure Batch-account tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="701ef-266">In this step, you link your Azure Storage account and Azure Batch account tooyour data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="701ef-267">Een gekoppelde Azure Storage-service maken</span><span class="sxs-lookup"><span data-stu-id="701ef-267">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="701ef-268">Klik op Hallo **auteur en implementeren van** tegel op Hallo **DATA FACTORY** blade voor **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="701ef-268">Click hello **Author and deploy** tile on hello **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="701ef-269">U ziet Hallo Data Factory-Editor.</span><span class="sxs-lookup"><span data-stu-id="701ef-269">You see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="701ef-270">Klik op **nieuwe gegevensopslag** op Hallo opdrachtbalk en kies **Azure storage**.</span><span class="sxs-lookup"><span data-stu-id="701ef-270">Click **New data store** on hello command bar and choose **Azure storage**.</span></span> <span data-ttu-id="701ef-271">U ziet Hallo JSON-script voor het maken van een Azure Storage gekoppelde service in Hallo-editor.</span><span class="sxs-lookup"><span data-stu-id="701ef-271">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>
    
    ![Nieuwe gegevensopslag - Azure Storage](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. <span data-ttu-id="701ef-273">Vervang `<accountname>` met de naam van uw Azure storage-account en `<accountkey>` door toegangssleutel van hello Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="701ef-273">Replace `<accountname>` with name of your Azure storage account and `<accountkey>` with access key of hello Azure storage account.</span></span> <span data-ttu-id="701ef-274">toolearn hoe tooget uw opslag toegang krijgen tot sleutel, Zie [toegangssleutels voor opslag weergeven, kopiëren en opnieuw genereren](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="701ef-274">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

    ![Azure-opslag leuk service gevonden](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. <span data-ttu-id="701ef-276">Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="701ef-276">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="701ef-277">Azure Batch gekoppelde service maken</span><span class="sxs-lookup"><span data-stu-id="701ef-277">Create Azure Batch linked service</span></span>
1. <span data-ttu-id="701ef-278">In Hallo Data Factory-Editor, klikt u op **... Meer** op de opdrachtbalk hello, klikt u op **nieuwe berekening**, en selecteer vervolgens **Azure Batch** in Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="701ef-278">In hello Data Factory Editor, click **... More** on hello command bar, click **New compute**, and then select **Azure Batch** from hello menu.</span></span>

    ![Nieuwe berekening - Azure Batch](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. <span data-ttu-id="701ef-280">Hallo na wijzigingen toohello JSON-script maken:</span><span class="sxs-lookup"><span data-stu-id="701ef-280">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="701ef-281">Azure Batch-accountnaam voor Hallo **accountName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="701ef-281">Specify Azure Batch account name for hello **accountName** property.</span></span> <span data-ttu-id="701ef-282">Hallo **URL** van Hallo **blade van Azure Batch-account** bevindt zich in de volgende indeling Hallo: `http://accountname.region.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="701ef-282">hello **URL** from hello **Azure Batch account blade** is in hello following format: `http://accountname.region.batch.azure.com`.</span></span> <span data-ttu-id="701ef-283">Voor Hallo **batchUri** eigenschap in JSON hello, moet u tooremove `accountname.` van de URL en gebruik Hallo Hallo `accountname` voor Hallo `accountName` JSON-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="701ef-283">For hello **batchUri** property in hello JSON, you need tooremove `accountname.` from hello URL and use hello `accountname` for hello `accountName` JSON property.</span></span>
   2. <span data-ttu-id="701ef-284">Hello Azure Batch-accountsleutel opgeven voor Hallo **accessKey** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="701ef-284">Specify hello Azure Batch account key for hello **accessKey** property.</span></span>
   3. <span data-ttu-id="701ef-285">Hallo naam opgeven van Hallo-groep die u hebt gemaakt als onderdeel van de vereisten voor Hallo **poolName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="701ef-285">Specify hello name of hello pool you created as part of prerequisites for hello **poolName** property.</span></span> <span data-ttu-id="701ef-286">U kunt ook Hallo-ID van Hallo pool in plaats van Hallo-naam van Hallo van toepassingen opgeven.</span><span class="sxs-lookup"><span data-stu-id="701ef-286">You can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>
   4. <span data-ttu-id="701ef-287">Azure Batch-URI opgeven voor Hallo **batchUri** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="701ef-287">Specify Azure Batch URI for hello **batchUri** property.</span></span> <span data-ttu-id="701ef-288">Voorbeeld: `https://westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="701ef-288">Example: `https://westus.batch.azure.com`.</span></span>  
   5. <span data-ttu-id="701ef-289">Geef Hallo **AzureStorageLinkedService** voor Hallo **linkedServiceName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="701ef-289">Specify hello **AzureStorageLinkedService** for hello **linkedServiceName** property.</span></span>

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       <span data-ttu-id="701ef-290">Voor Hallo **poolName** eigenschap, kunt u ook Hallo-ID van Hallo pool in plaats van Hallo-naam van Hallo van toepassingen opgeven.</span><span class="sxs-lookup"><span data-stu-id="701ef-290">For hello **poolName** property, you can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="701ef-291">Hallo Data Factory-service biedt een optie op aanvraag geen ondersteuning voor Azure Batch als voor HDInsight.</span><span class="sxs-lookup"><span data-stu-id="701ef-291">hello Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="701ef-292">U kunt uw eigen Azure Batch-pool alleen gebruiken in een Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="701ef-292">You can only use your own Azure Batch pool in an Azure data factory.</span></span>   
    

### <a name="step-3-create-datasets"></a><span data-ttu-id="701ef-293">Stap 3: Gegevenssets maken</span><span class="sxs-lookup"><span data-stu-id="701ef-293">Step 3: Create datasets</span></span>
<span data-ttu-id="701ef-294">In deze stap maakt u gegevenssets toorepresent invoer maken en uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="701ef-294">In this step, you create datasets toorepresent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="701ef-295">Invoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="701ef-295">Create input dataset</span></span>
1. <span data-ttu-id="701ef-296">In Hallo **Editor** Hallo Data Factory, klikt u op **... Meer** op de opdrachtbalk hello, klikt u op **nieuwe gegevensset**, en selecteer vervolgens **Azure Blob storage** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="701ef-296">In hello **Editor** for hello Data Factory, click **... More** on hello command bar, click **New dataset**, and then select **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="701ef-297">Hallo JSON in het rechterdeelvenster Hallo vervangen door Hallo volgende JSON-fragment:</span><span class="sxs-lookup"><span data-stu-id="701ef-297">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
         },
         "availability": {
             "frequency": "Hour",
             "interval": 1
         },
         "external": true,
         "policy": {}
     }
    }
    ```

   <span data-ttu-id="701ef-298">U maakt een pijplijn verderop in dit scenario met begintijd: 2016-11-16T00:00:00Z-en eindtijd: 2016-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="701ef-298">You create a pipeline later in this walkthrough with start time: 2016-11-16T00:00:00Z and end time: 2016-11-16T05:00:00Z.</span></span> <span data-ttu-id="701ef-299">Is het geplande tooproduce gegevens elk uur, dus er vijf i/o-segmenten zijn (tussen **00**: 00:00 -> **05**: 00:00).</span><span class="sxs-lookup"><span data-stu-id="701ef-299">It is scheduled tooproduce data hourly, so there are five input/output slices (between **00**:00:00 -> **05**:00:00).</span></span>

   <span data-ttu-id="701ef-300">Hallo **frequentie** en **interval** voor invoergegevensset hello te is ingesteld**uur** en **1**, wat betekent dat Hallo invoer segment is beschikbaar elk uur.</span><span class="sxs-lookup"><span data-stu-id="701ef-300">hello **frequency** and **interval** for hello input dataset is set too**Hour** and **1**, which means that hello input slice is available hourly.</span></span> <span data-ttu-id="701ef-301">In dit voorbeeld wordt dezelfde Hallo-bestand (bestand.txt) in Hallo intputfolder.</span><span class="sxs-lookup"><span data-stu-id="701ef-301">In this sample, it is hello same file (file.txt) in hello intputfolder.</span></span>

   <span data-ttu-id="701ef-302">Hier volgen Hallo begintijden voor elk segment, wordt vertegenwoordigd door SliceStart systeemvariabele in Hallo hierboven JSON-codefragment.</span><span class="sxs-lookup"><span data-stu-id="701ef-302">Here are hello start times for each slice, which is represented by SliceStart system variable in hello above JSON snippet.</span></span>
3. <span data-ttu-id="701ef-303">Klik op **implementeren** op Hallo werkbalk toocreate en implementeren van Hallo **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="701ef-303">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset**.</span></span> <span data-ttu-id="701ef-304">Controleer of u Hallo **tabel gemaakt met SUCCES** bericht op de titelbalk Hallo Hallo Editor.</span><span class="sxs-lookup"><span data-stu-id="701ef-304">Confirm that you see hello **TABLE CREATED SUCCESSFULLY** message on hello title bar of hello Editor.</span></span>

#### <a name="create-an-output-dataset"></a><span data-ttu-id="701ef-305">Een uitvoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="701ef-305">Create an output dataset</span></span>
1. <span data-ttu-id="701ef-306">In Hallo **Data Factory-editor**, klikt u op **... Meer** op de opdrachtbalk hello, klikt u op **nieuwe gegevensset**, en selecteer vervolgens **Azure Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="701ef-306">In hello **Data Factory editor**, click **... More** on hello command bar, click **New dataset**, and then select **Azure Blob storage**.</span></span>
2. <span data-ttu-id="701ef-307">Hallo JSON-script in het rechterdeelvenster Hallo vervangen door Hallo volgende JSON-script:</span><span class="sxs-lookup"><span data-stu-id="701ef-307">Replace hello JSON script in hello right pane with hello following JSON script:</span></span>

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
                "partitionedBy": [
                    {
                        "name": "slice",
                        "value": {
                            "type": "DateTime",
                            "date": "SliceStart",
                            "format": "yyyy-MM-dd-HH"
                        }
                    }
                ]
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

     <span data-ttu-id="701ef-308">Uitvoerlocatie van de is **adftutorial/customactivityoutput/** en naam van het uitvoerbestand is jjjj-MM-dd-HH.txt waarbij JJJJ-MM-dd uu staat voor Hallo jaar, maand, datum en het uur van de Hallo-segment wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="701ef-308">Output location is **adftutorial/customactivityoutput/** and output file name is yyyy-MM-dd-HH.txt where yyyy-MM-dd-HH is hello year, month, date, and hour of hello slice being produced.</span></span> <span data-ttu-id="701ef-309">Zie [referentie voor ontwikkelaars] [ adf-developer-reference] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="701ef-309">See [Developer Reference][adf-developer-reference] for details.</span></span>

    <span data-ttu-id="701ef-310">Een uitvoer-blob/bestand wordt gegenereerd voor elk segment invoer.</span><span class="sxs-lookup"><span data-stu-id="701ef-310">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="701ef-311">Hier ziet u hoe een bestand voor uitvoer met de naam van elk segment.</span><span class="sxs-lookup"><span data-stu-id="701ef-311">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="701ef-312">Alle Hallo uitvoerbestanden worden gegenereerd in een uitvoermap: **adftutorial\customactivityoutput**.</span><span class="sxs-lookup"><span data-stu-id="701ef-312">All hello output files are generated in one output folder: **adftutorial\customactivityoutput**.</span></span>

   | <span data-ttu-id="701ef-313">Segment</span><span class="sxs-lookup"><span data-stu-id="701ef-313">Slice</span></span> | <span data-ttu-id="701ef-314">Begintijd</span><span class="sxs-lookup"><span data-stu-id="701ef-314">Start time</span></span> | <span data-ttu-id="701ef-315">Bestand voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="701ef-315">Output file</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="701ef-316">1</span><span class="sxs-lookup"><span data-stu-id="701ef-316">1</span></span> |<span data-ttu-id="701ef-317">2016-11-16T00:00:00</span><span class="sxs-lookup"><span data-stu-id="701ef-317">2016-11-16T00:00:00</span></span> |<span data-ttu-id="701ef-318">2016-11-16-00.txt</span><span class="sxs-lookup"><span data-stu-id="701ef-318">2016-11-16-00.txt</span></span> |
   | <span data-ttu-id="701ef-319">2</span><span class="sxs-lookup"><span data-stu-id="701ef-319">2</span></span> |<span data-ttu-id="701ef-320">2016-11-16T01:00:00</span><span class="sxs-lookup"><span data-stu-id="701ef-320">2016-11-16T01:00:00</span></span> |<span data-ttu-id="701ef-321">2016-11-16-01.txt</span><span class="sxs-lookup"><span data-stu-id="701ef-321">2016-11-16-01.txt</span></span> |
   | <span data-ttu-id="701ef-322">3</span><span class="sxs-lookup"><span data-stu-id="701ef-322">3</span></span> |<span data-ttu-id="701ef-323">2016-11-16T02:00:00</span><span class="sxs-lookup"><span data-stu-id="701ef-323">2016-11-16T02:00:00</span></span> |<span data-ttu-id="701ef-324">2016-11-16-02.txt</span><span class="sxs-lookup"><span data-stu-id="701ef-324">2016-11-16-02.txt</span></span> |
   | <span data-ttu-id="701ef-325">4</span><span class="sxs-lookup"><span data-stu-id="701ef-325">4</span></span> |<span data-ttu-id="701ef-326">2016-11-16T03:00:00</span><span class="sxs-lookup"><span data-stu-id="701ef-326">2016-11-16T03:00:00</span></span> |<span data-ttu-id="701ef-327">2016-11-16-03.txt</span><span class="sxs-lookup"><span data-stu-id="701ef-327">2016-11-16-03.txt</span></span> |
   | <span data-ttu-id="701ef-328">5</span><span class="sxs-lookup"><span data-stu-id="701ef-328">5</span></span> |<span data-ttu-id="701ef-329">2016-11-16T04:00:00</span><span class="sxs-lookup"><span data-stu-id="701ef-329">2016-11-16T04:00:00</span></span> |<span data-ttu-id="701ef-330">2016-11-16-04.txt</span><span class="sxs-lookup"><span data-stu-id="701ef-330">2016-11-16-04.txt</span></span> |

    <span data-ttu-id="701ef-331">Houd er rekening mee dat alle Hallo-bestanden in een invoermap deel van een segment met Hallo begintijden uitmaken hierboven vermeld.</span><span class="sxs-lookup"><span data-stu-id="701ef-331">Remember that all hello files in an input folder are part of a slice with hello start times mentioned above.</span></span> <span data-ttu-id="701ef-332">Als dit segment is verwerkt, wordt Hallo aangepaste activiteit gescand door elk bestand en resulteert in een regel in het uitvoerbestand Hallo met Hallo aantal exemplaren van zoekterm ('Microsoft').</span><span class="sxs-lookup"><span data-stu-id="701ef-332">When this slice is processed, hello custom activity scans through each file and produces a line in hello output file with hello number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="701ef-333">Als er drie bestanden in Hallo inputfolder, er zijn drie regels in het uitvoerbestand Hallo voor elk segment per uur: 2016-11-16-00.txt 2016-11-16:01:00:00.txt, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="701ef-333">If there are three files in hello inputfolder, there are three lines in hello output file for each hourly slice: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.</span></span>
3. <span data-ttu-id="701ef-334">Hallo toodeploy **OutputDataset**, klikt u op **implementeren** op Hallo opdrachtbalk klikken.</span><span class="sxs-lookup"><span data-stu-id="701ef-334">toodeploy hello **OutputDataset**, click **Deploy** on hello command bar.</span></span>

### <a name="create-and-run-a-pipeline-that-uses-hello-custom-activity"></a><span data-ttu-id="701ef-335">Maken en uitvoeren van een pijplijn die gebruikmaakt van aangepaste activiteit Hallo</span><span class="sxs-lookup"><span data-stu-id="701ef-335">Create and run a pipeline that uses hello custom activity</span></span>
1. <span data-ttu-id="701ef-336">In Hallo Data Factory-Editor, klikt u op **... Meer**, en selecteer vervolgens **nieuwe pijplijn** op Hallo opdrachtbalk klikken.</span><span class="sxs-lookup"><span data-stu-id="701ef-336">In hello Data Factory Editor, click **... More**, and then select **New pipeline** on hello command bar.</span></span> 
2. <span data-ttu-id="701ef-337">Hallo JSON in het rechterdeelvenster Hallo vervangen door Hallo volgende JSON-script:</span><span class="sxs-lookup"><span data-stu-id="701ef-337">Replace hello JSON in hello right pane with hello following JSON script:</span></span>

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    <span data-ttu-id="701ef-338">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="701ef-338">Note hello following points:</span></span>

   * <span data-ttu-id="701ef-339">**Gelijktijdigheid** te is ingesteld,**2** zodat twee segmenten parallel door 2 virtuele machines in hello Azure Batch-pool verwerkt worden.</span><span class="sxs-lookup"><span data-stu-id="701ef-339">**Concurrency** is set too**2** so that two slices are processed in parallel by 2 VMs in hello Azure Batch pool.</span></span>
   * <span data-ttu-id="701ef-340">Er is één activiteit in de sectie activiteiten Hallo en is van het type: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="701ef-340">There is one activity in hello activities section and it is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="701ef-341">**AssemblyName** toohello naam Hallo dll-bestand dat is ingesteld: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="701ef-341">**AssemblyName** is set toohello name of hello DLL: **MyDotnetActivity.dll**.</span></span>
   * <span data-ttu-id="701ef-342">**EntryPoint** te is ingesteld,**MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="701ef-342">**EntryPoint** is set too**MyDotNetActivityNS.MyDotNetActivity**.</span></span>
   * <span data-ttu-id="701ef-343">**PackageLinkedService** te is ingesteld,**AzureStorageLinkedService** die toohello blob-opslag met Hallo aangepaste activiteit zip-bestand verwijst.</span><span class="sxs-lookup"><span data-stu-id="701ef-343">**PackageLinkedService** is set too**AzureStorageLinkedService** that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="701ef-344">Als u gebruikmaakt van andere Azure Storage-accounts voor i/o-bestanden en hello aangepaste activiteit zip-bestand, u maakt een andere gekoppelde Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="701ef-344">If you are using different Azure Storage accounts for input/output files and hello custom activity zip file, you create another Azure Storage linked service.</span></span> <span data-ttu-id="701ef-345">In dit artikel wordt ervan uitgegaan dat u hetzelfde Azure-opslagaccount Hallo.</span><span class="sxs-lookup"><span data-stu-id="701ef-345">This article assumes that you are using hello same Azure Storage account.</span></span>
   * <span data-ttu-id="701ef-346">**PackageFile** te is ingesteld,**customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="701ef-346">**PackageFile** is set too**customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="701ef-347">Het Hallo-indeling is: containerforthezip/nameofthezip.zip.</span><span class="sxs-lookup"><span data-stu-id="701ef-347">It is in hello format: containerforthezip/nameofthezip.zip.</span></span>
   * <span data-ttu-id="701ef-348">Hallo aangepaste activiteit wordt **InputDataset** als invoer en **OutputDataset** als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="701ef-348">hello custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="701ef-349">Hallo linkedServiceName eigenschap van de aangepaste activiteit Hallo verwijst toohello **AzureBatchLinkedService**, waarin u Azure Data Factory bepaald die Hallo aangepaste activiteit moet toorun op Azure Batch-VM's.</span><span class="sxs-lookup"><span data-stu-id="701ef-349">hello linkedServiceName property of hello custom activity points toohello **AzureBatchLinkedService**, which tells Azure Data Factory that hello custom activity needs toorun on Azure Batch VMs.</span></span>
   * <span data-ttu-id="701ef-350">**isPaused** eigenschap is ingesteld, te**false** standaard.</span><span class="sxs-lookup"><span data-stu-id="701ef-350">**isPaused** property is set too**false** by default.</span></span> <span data-ttu-id="701ef-351">Hallo-pijplijn wordt onmiddellijk uitgevoerd in dit voorbeeld omdat Hallo segmenten te in de afgelopen Hallo starten.</span><span class="sxs-lookup"><span data-stu-id="701ef-351">hello pipeline runs immediately in this example because hello slices start in hello past.</span></span> <span data-ttu-id="701ef-352">U kunt deze eigenschap tootrue toopause Hallo pijplijn en zijn ingesteld dat deze back-toofalse toorestart.</span><span class="sxs-lookup"><span data-stu-id="701ef-352">You can set this property tootrue toopause hello pipeline and set it back toofalse toorestart.</span></span>
   * <span data-ttu-id="701ef-353">Hallo **start** tijd en **end** tijden zijn **vijf** uur uit elkaar en segmenten worden elk uur, geproduceerd zodat vijf segmenten worden geproduceerd door Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="701ef-353">hello **start** time and **end** times are **five** hours apart and slices are produced hourly, so five slices are produced by hello pipeline.</span></span>
3. <span data-ttu-id="701ef-354">toodeploy hello pipeline, klikt u op **implementeren** op Hallo opdrachtbalk klikken.</span><span class="sxs-lookup"><span data-stu-id="701ef-354">toodeploy hello pipeline, click **Deploy** on hello command bar.</span></span>

### <a name="monitor-hello-pipeline"></a><span data-ttu-id="701ef-355">Hallo-pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="701ef-355">Monitor hello pipeline</span></span>
1. <span data-ttu-id="701ef-356">Klik in de Data Factory-blade Hallo in hello Azure-portal, op **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="701ef-356">In hello Data Factory blade in hello Azure portal, click **Diagram**.</span></span>

    ![Tegel Diagram](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. <span data-ttu-id="701ef-358">Klik in de diagramweergave hello, op Hallo OutputDataset.</span><span class="sxs-lookup"><span data-stu-id="701ef-358">In hello Diagram View, now click hello OutputDataset.</span></span>

    ![Diagramweergave](./media/data-factory-use-custom-activities/diagram.png)
3. <span data-ttu-id="701ef-360">U ziet dat Hallo vijf uitvoer segmenten Hallo status Ready heeft zijn.</span><span class="sxs-lookup"><span data-stu-id="701ef-360">You should see that hello five output slices are in hello Ready state.</span></span> <span data-ttu-id="701ef-361">Als ze zich niet in de status gereed voor hello, nog niet ze nog gemaakt.</span><span class="sxs-lookup"><span data-stu-id="701ef-361">If they are not in hello Ready state, they haven't been produced yet.</span></span> 

   ![Uitvoer segmenten](./media/data-factory-use-custom-activities/OutputSlices.png)
4. <span data-ttu-id="701ef-363">Controleer of dat de uitvoerbestanden Hallo worden gegenereerd in de blobopslag Hallo in Hallo **adftutorial** container.</span><span class="sxs-lookup"><span data-stu-id="701ef-363">Verify that hello output files are generated in hello blob storage in hello **adftutorial** container.</span></span>

   ![de uitvoer van aangepaste activiteit][image-data-factory-ouput-from-custom-activity]
5. <span data-ttu-id="701ef-365">Als u het uitvoerbestand Hallo opent, ziet u Hallo uitvoer vergelijkbare toohello volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="701ef-365">If you open hello output file, you should see hello output similar toohello following output:</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
    ```
6. <span data-ttu-id="701ef-366">Gebruik Hallo [Azure-portal] [ azure-preview-portal] of Azure PowerShell-cmdlets toomonitor uw gegevensfactory, pijplijnen en gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="701ef-366">Use hello [Azure portal][azure-preview-portal] or Azure PowerShell cmdlets toomonitor your data factory, pipelines, and data sets.</span></span> <span data-ttu-id="701ef-367">Ziet u berichten van Hallo **ActivityLogger** in Hallo-code voor de aangepaste activiteit Hallo in Hallo-Logboeken (specifiek gebruiker-0.log) die u kunt downloaden van het Hallo-portal of met behulp van cmdlets.</span><span class="sxs-lookup"><span data-stu-id="701ef-367">You can see messages from hello **ActivityLogger** in hello code for hello custom activity in hello logs (specifically user-0.log) that you can download from hello portal or using cmdlets.</span></span>

   ![Logboeken downloaden van de aangepaste activiteit][image-data-factory-download-logs-from-custom-activity]

<span data-ttu-id="701ef-369">Zie [pijplijnen bewaken en beheren](data-factory-monitor-manage-pipelines.md) voor gedetailleerde stappen voor het bewaken van gegevenssets en pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="701ef-369">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) for detailed steps for monitoring datasets and pipelines.</span></span>      

## <a name="data-factory-project-in-visual-studio"></a><span data-ttu-id="701ef-370">Data Factory-project in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="701ef-370">Data Factory project in Visual Studio</span></span>  
<span data-ttu-id="701ef-371">U kunt maken en Data Factory-entiteiten publiceren met behulp van Visual Studio in plaats van Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="701ef-371">You can create and publish Data Factory entities by using Visual Studio instead of using Azure portal.</span></span> <span data-ttu-id="701ef-372">Voor informatie over het maken gedetailleerde en Data Factory-entiteiten publiceren met behulp van Visual Studio, Zie [bouwen van uw eerste pijplijn met Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) en [gegevens kopiëren van Azure Blob-tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) artikelen.</span><span class="sxs-lookup"><span data-stu-id="701ef-372">For detailed information about creating and publishing Data Factory entities by using Visual Studio, See [Build your first pipeline using Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) and [Copy data from Azure Blob tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) articles.</span></span>

<span data-ttu-id="701ef-373">Hallo extra stappen te volgen als u Data Factory-project in Visual Studio maakt:</span><span class="sxs-lookup"><span data-stu-id="701ef-373">Do hello following additional steps if you are creating Data Factory project in Visual Studio:</span></span>
 
1. <span data-ttu-id="701ef-374">Hallo Data Factory project toohello Visual Studio-oplossing met Hallo aangepaste activiteit project toevoegen.</span><span class="sxs-lookup"><span data-stu-id="701ef-374">Add hello Data Factory project toohello Visual Studio solution that contains hello custom activity project.</span></span> 
2. <span data-ttu-id="701ef-375">Een verwijzing toohello .NET activiteit project uit Hallo Data Factory-project toevoegen.</span><span class="sxs-lookup"><span data-stu-id="701ef-375">Add a reference toohello .NET activity project from hello Data Factory project.</span></span> <span data-ttu-id="701ef-376">Met de rechtermuisknop op de Data Factory-project, wijst u te**toevoegen**, en klik vervolgens op **verwijzing**.</span><span class="sxs-lookup"><span data-stu-id="701ef-376">Right-click Data Factory project, point too**Add**, and then click **Reference**.</span></span> 
3. <span data-ttu-id="701ef-377">In Hallo **verwijzing toevoegen** dialoogvenster, selecteer Hallo **MyDotNetActivity** project en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="701ef-377">In hello **Add Reference** dialog box, select hello **MyDotNetActivity** project, and click **OK**.</span></span>
4. <span data-ttu-id="701ef-378">Bouw en Hallo oplossing publiceert.</span><span class="sxs-lookup"><span data-stu-id="701ef-378">Build and publish hello solution.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="701ef-379">Als u Data Factory-entiteiten publiceert, een zip-bestand wordt automatisch voor u gemaakt en is toohello geüploade blob-container: customactivitycontainer.</span><span class="sxs-lookup"><span data-stu-id="701ef-379">When you publish Data Factory entities, a zip file is automatically created for you and is uploaded toohello blob container: customactivitycontainer.</span></span> <span data-ttu-id="701ef-380">Als Hallo blob-container niet bestaat, wordt deze automatisch gemaakt te.</span><span class="sxs-lookup"><span data-stu-id="701ef-380">If hello blob container does not exist, it is automatically created too.</span></span>  


## <a name="data-factory-and-batch-integration"></a><span data-ttu-id="701ef-381">Data Factory en Batch-integratie</span><span class="sxs-lookup"><span data-stu-id="701ef-381">Data Factory and Batch integration</span></span>
<span data-ttu-id="701ef-382">Hallo Data Factory-service maakt een taak in Azure Batch met de naam van de Hallo: **adf poolname: taak-xxx**.</span><span class="sxs-lookup"><span data-stu-id="701ef-382">hello Data Factory service creates a job in Azure Batch with hello name: **adf-poolname: job-xxx**.</span></span> <span data-ttu-id="701ef-383">Klik op **taken** in het linkermenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="701ef-383">Click **Jobs** from hello left menu.</span></span> 

![Azure Data Factory - Batch-taken](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

<span data-ttu-id="701ef-385">Een taak is gemaakt voor elke activiteit uitvoering van een segment.</span><span class="sxs-lookup"><span data-stu-id="701ef-385">A task is created for each activity run of a slice.</span></span> <span data-ttu-id="701ef-386">Als er vijf segmenten gereed toobe verwerkt, worden de vijf taken gemaakt in deze taak.</span><span class="sxs-lookup"><span data-stu-id="701ef-386">If there are five slices ready toobe processed, five tasks are created in this job.</span></span> <span data-ttu-id="701ef-387">Als er meerdere rekenknooppunten in Hallo Batch-pool, kunnen twee of meer segmenten parallel worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="701ef-387">If there are multiple compute nodes in hello Batch pool, two or more slices can run in parallel.</span></span> <span data-ttu-id="701ef-388">Als het maximum aantal taken per Hallo compute knooppunt is ingesteld te > 1, kunnen ook hebt u meer dan één segment Hallo waarop dezelfde compute.</span><span class="sxs-lookup"><span data-stu-id="701ef-388">If hello maximum tasks per compute node is set too> 1, you can also have more than one slice running on hello same compute.</span></span>

![Azure Data Factory - taken voor Batch-job](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

<span data-ttu-id="701ef-390">Hallo volgende diagram illustreert Hallo relatie tussen Azure Data Factory en Batch-taken.</span><span class="sxs-lookup"><span data-stu-id="701ef-390">hello following diagram illustrates hello relationship between Azure Data Factory and Batch tasks.</span></span>

![Data Factory & Batch](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a><span data-ttu-id="701ef-392">Fouten oplossen</span><span class="sxs-lookup"><span data-stu-id="701ef-392">Troubleshoot failures</span></span>
<span data-ttu-id="701ef-393">Het oplossen van problemen bestaat uit een paar eenvoudige technieken:</span><span class="sxs-lookup"><span data-stu-id="701ef-393">Troubleshooting consists of a few basic techniques:</span></span>

1. <span data-ttu-id="701ef-394">Als u de volgende fout Hallo ziet, kunt u een Hot/Cool blob-opslag in plaats van een algemene Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="701ef-394">If you see hello following error, you may be using a Hot/Cool blob storage instead of using a general-purpose Azure blob storage.</span></span> <span data-ttu-id="701ef-395">Hallo zip-bestand tooa uploaden **voor algemene doeleinden Azure Storage-Account**.</span><span class="sxs-lookup"><span data-stu-id="701ef-395">Upload hello zip file tooa **general-purpose Azure Storage Account**.</span></span> 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of hello specified Azure Blob(s).
    ``` 
2. <span data-ttu-id="701ef-396">Als u de volgende fout Hallo ziet, bevestig de naam van die Hallo van Hallo klasse in Hallo CS komt overeen met Hallo opgegeven bestandsnaam voor Hallo **EntryPoint** eigenschap in de JSON van de Hallo-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="701ef-396">If you see hello following error, confirm that hello name of hello class in hello CS file matches hello name you specified for hello **EntryPoint** property in hello pipeline JSON.</span></span> <span data-ttu-id="701ef-397">In Hallo-scenario is de naam van de klasse Hallo: MyDotNetActivity en Hallo ingangspunt in Hallo JSON is: MyDotNetActivityNS. **MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="701ef-397">In hello walkthrough, name of hello class is: MyDotNetActivity, and hello EntryPoint in hello JSON is: MyDotNetActivityNS.**MyDotNetActivity**.</span></span>

    ```
    MyDotNetActivity assembly does not exist or doesn't implement hello type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   <span data-ttu-id="701ef-398">Als het Hallo-namen komen overeen, bevestig dat alle binaire bestanden van Hallo op Hallo **hoofdmap** van Hallo zip-bestand.</span><span class="sxs-lookup"><span data-stu-id="701ef-398">If hello names do match, confirm that all hello binaries are in hello **root folder** of hello zip file.</span></span> <span data-ttu-id="701ef-399">Dat wil zeggen, wanneer u Hallo zip-bestand opent, ziet u alle Hallo-bestanden in de hoofdmap hello, niet in alle submappen.</span><span class="sxs-lookup"><span data-stu-id="701ef-399">That is, when you open hello zip file, you should see all hello files in hello root folder, not in any sub folders.</span></span>   
3. <span data-ttu-id="701ef-400">Als invoersegment met de Hallo te niet is ingesteld**gereed**, bevestig dat de invoer mapstructuur Hallo juist is en **bestand.txt** bestaat in de invoer Hallo-mappen.</span><span class="sxs-lookup"><span data-stu-id="701ef-400">If hello input slice is not set too**Ready**, confirm that hello input folder structure is correct and **file.txt** exists in hello input folders.</span></span>
3. <span data-ttu-id="701ef-401">In Hallo **Execute** methode van uw aangepaste activiteit, gebruik Hallo **IActivityLogger** object toolog informatie die u helpt oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="701ef-401">In hello **Execute** method of your custom activity, use hello **IActivityLogger** object toolog information that helps you troubleshoot issues.</span></span> <span data-ttu-id="701ef-402">geregistreerd Hallo-berichten weergegeven in de logboekbestanden van Hallo gebruiker (een of meer bestanden met de naam: gebruiker 0.log, gebruiker 1.log, gebruiker 2.log, enz.).</span><span class="sxs-lookup"><span data-stu-id="701ef-402">hello logged messages show up in hello user log files (one or more files named: user-0.log, user-1.log, user-2.log, etc.).</span></span>

   <span data-ttu-id="701ef-403">In Hallo **OutputDataset** blade, klikt u op Hallo segment toosee hello **GEGEVENSSEGMENT** blade voor die segment.</span><span class="sxs-lookup"><span data-stu-id="701ef-403">In hello **OutputDataset** blade, click hello slice toosee hello **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="701ef-404">U ziet **activiteiten bij uitvoering** voor dit segment.</span><span class="sxs-lookup"><span data-stu-id="701ef-404">You see **activity runs** for that slice.</span></span> <span data-ttu-id="701ef-405">Hier ziet u een activiteit die wordt uitgevoerd voor Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="701ef-405">You should see one activity run for hello slice.</span></span> <span data-ttu-id="701ef-406">Als u in de opdrachtbalk Hallo op uitvoeren klikt, kunt u een andere activiteit die wordt uitgevoerd voor Hallo starten hetzelfde segment.</span><span class="sxs-lookup"><span data-stu-id="701ef-406">If you click Run in hello command bar, you can start another activity run for hello same slice.</span></span>

   <span data-ttu-id="701ef-407">Wanneer u klikt op Hallo activiteit die wordt uitgevoerd, ziet u Hallo **DETAILS uitvoering van activiteit** blade met een lijst met logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="701ef-407">When you click hello activity run, you see hello **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="701ef-408">Ziet u geregistreerde berichten in Hallo user_0.log-bestand.</span><span class="sxs-lookup"><span data-stu-id="701ef-408">You see logged messages in hello user_0.log file.</span></span> <span data-ttu-id="701ef-409">Wanneer er een fout optreedt, ziet u drie activiteiten bij uitvoering omdat het maximale aantal pogingen Hallo too3 in Hallo pipeline/activiteits-JSON is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="701ef-409">When an error occurs, you see three activity runs because hello retry count is set too3 in hello pipeline/activity JSON.</span></span> <span data-ttu-id="701ef-410">Wanneer u klikt op Hallo activiteit die wordt uitgevoerd, ziet u logboekbestanden Hallo tootroubleshoot Hallo fout kunt controleren.</span><span class="sxs-lookup"><span data-stu-id="701ef-410">When you click hello activity run, you see hello log files that you can review tootroubleshoot hello error.</span></span>

   <span data-ttu-id="701ef-411">Klik in Hallo lijst van logboekbestanden op Hallo **gebruiker 0.log**.</span><span class="sxs-lookup"><span data-stu-id="701ef-411">In hello list of log files, click hello **user-0.log**.</span></span> <span data-ttu-id="701ef-412">In het rechterpaneel Hallo zijn Hallo resultaten van het gebruik van Hallo **IActivityLogger.Write** methode.</span><span class="sxs-lookup"><span data-stu-id="701ef-412">In hello right panel are hello results of using hello **IActivityLogger.Write** method.</span></span> <span data-ttu-id="701ef-413">Als u alle berichten niet ziet, controleert u of er meer logboekbestanden met de naam: user_1.log, user_2.log enzovoort. Anders Hallo code is mogelijk niet nadat Hallo laatste bericht vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="701ef-413">If you don't see all messages, check if you have more log files named: user_1.log, user_2.log etc. Otherwise, hello code may have failed after hello last logged message.</span></span>

   <span data-ttu-id="701ef-414">Controleer daarnaast **system 0.log** voor elk systeem foutberichten en uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="701ef-414">In addition, check **system-0.log** for any system error messages and exceptions.</span></span>
4. <span data-ttu-id="701ef-415">Hallo omvatten **PDB** bestand in het zip-bestand Hallo zodat Hallo foutdetails beschikt over informatie zoals **aanroepstack** wanneer er een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="701ef-415">Include hello **PDB** file in hello zip file so that hello error details have information such as **call stack** when an error occurs.</span></span>
5. <span data-ttu-id="701ef-416">Alle bestanden in het zip-bestand Hallo Hallo voor Hallo aangepaste activiteit op Hallo moet **bovenste niveau** met geen submappen.</span><span class="sxs-lookup"><span data-stu-id="701ef-416">All hello files in hello zip file for hello custom activity must be at hello **top level** with no sub folders.</span></span>
6. <span data-ttu-id="701ef-417">Zorg ervoor dat Hallo **assemblyName** (MyDotNetActivity.dll) **entryPoint**(MyDotNetActivityNS.MyDotNetActivity) **packageFile** (customactivitycontainer / MyDotNetActivity.zip) en **packageLinkedService** (toohello moet verwijzen **algemeen**Azure blob-opslag met Hallo zip-bestand) toocorrect waarden zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="701ef-417">Ensure that hello **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point toohello **general-purpose**Azure blob storage that contains hello zip file) are set toocorrect values.</span></span>
7. <span data-ttu-id="701ef-418">Als u een fout en wilt tooreprocess Hallo segment hebt opgelost, met de rechtermuisknop op Hallo segment Hallo **OutputDataset** blade en klik op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="701ef-418">If you fixed an error and want tooreprocess hello slice, right-click hello slice in hello **OutputDataset** blade and click **Run**.</span></span>
8. <span data-ttu-id="701ef-419">Als u de volgende fout Hallo ziet, gebruikt u hello Azure Storage-pakket van versie > 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="701ef-419">If you see hello following error, you are using hello Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="701ef-420">Data Factory-service starten vereist Hallo 4.3-versie van WindowsAzure.Storage.</span><span class="sxs-lookup"><span data-stu-id="701ef-420">Data Factory service launcher requires hello 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="701ef-421">Zie [Appdomain isolatie](#appdomain-isolation) sectie voor een tijdelijke oplossing als u Hallo gebruiken moet latere versie van Azure Storage-assembly.</span><span class="sxs-lookup"><span data-stu-id="701ef-421">See [Appdomain isolation](#appdomain-isolation) section for a work-around if you must use hello later version of Azure Storage assembly.</span></span> 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by hello target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    <span data-ttu-id="701ef-422">Als u Hallo 4.3.0 versie van Azure Storage-pakket gebruiken kunt, verwijdert u Hallo bestaande verwijzing tooAzure opslag pakket versie > 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="701ef-422">If you can use hello 4.3.0 version of Azure Storage package, remove hello existing reference tooAzure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="701ef-423">Voer vervolgens de volgende opdracht uit NuGet Package Manager Console Hallo.</span><span class="sxs-lookup"><span data-stu-id="701ef-423">Then, run hello following command from NuGet Package Manager Console.</span></span> 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    <span data-ttu-id="701ef-424">Hallo-project maken.</span><span class="sxs-lookup"><span data-stu-id="701ef-424">Build hello project.</span></span> <span data-ttu-id="701ef-425">Assembly van versie > 4.3.0 Azure.Storage uit Hallo bin\Debug map verwijderen.</span><span class="sxs-lookup"><span data-stu-id="701ef-425">Delete Azure.Storage assembly of version > 4.3.0 from hello bin\Debug folder.</span></span> <span data-ttu-id="701ef-426">Maak een zip-bestand met de binaire bestanden en Hallo PDB-bestand.</span><span class="sxs-lookup"><span data-stu-id="701ef-426">Create a zip file with binaries and hello PDB file.</span></span> <span data-ttu-id="701ef-427">Hallo oude zip-bestand vervangen door deze gegevensset in Hallo blob-container (customactivitycontainer).</span><span class="sxs-lookup"><span data-stu-id="701ef-427">Replace hello old zip file with this one in hello blob container (customactivitycontainer).</span></span> <span data-ttu-id="701ef-428">Voer Hallo segmenten die niet zijn geslaagd (met de rechtermuisknop op het segment en klik op uitvoeren).</span><span class="sxs-lookup"><span data-stu-id="701ef-428">Rerun hello slices that failed (right-click slice, and click Run).</span></span>   
8. <span data-ttu-id="701ef-429">Hallo aangepaste activiteit gebruikt geen Hallo **app.config** bestand van het pakket.</span><span class="sxs-lookup"><span data-stu-id="701ef-429">hello custom activity does not use hello **app.config** file from your package.</span></span> <span data-ttu-id="701ef-430">Dus als uw code wordt een verbindingsreeksen uit het Hallo-configuratiebestand gelezen, werkt het niet tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="701ef-430">Therefore, if your code reads any connection strings from hello configuration file, it does not work at runtime.</span></span> <span data-ttu-id="701ef-431">Hallo beste wanneer toohold met behulp van Azure Batch is geen geheimen in een **Azure KeyVault**, gebruiken een certificaat gebaseerde service principal tooprotect hello **keyvault**, en het Hallo-certificaat distribueren tooAzure Batch-pool.</span><span class="sxs-lookup"><span data-stu-id="701ef-431">hello best practice when using Azure Batch is toohold any secrets in an **Azure KeyVault**, use a certificate-based service principal tooprotect hello **keyvault**, and distribute hello certificate tooAzure Batch pool.</span></span> <span data-ttu-id="701ef-432">Hallo aangepaste activiteit .NET vervolgens toegang tot geheimen Hallo KeyVault tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="701ef-432">hello .NET custom activity then can access secrets from hello KeyVault at runtime.</span></span> <span data-ttu-id="701ef-433">Deze oplossing is een algemene oplossing en tooany type geheim, niet alleen verbindingsreeks kunt schalen.</span><span class="sxs-lookup"><span data-stu-id="701ef-433">This solution is a generic solution and can scale tooany type of secret, not just connection string.</span></span>

   <span data-ttu-id="701ef-434">Er is een eenvoudiger tijdelijke oplossing (maar niet aanbevolen): kunt u een **Azure SQL gekoppelde service** met verbindingstekenreeksinstellingen, maken een gegevensset dat wordt gebruikt Hallo gekoppelde service en de keten Hallo dataset als een dummy invoergegevensset toohello aangepaste .NET-activiteit.</span><span class="sxs-lookup"><span data-stu-id="701ef-434">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses hello linked service, and chain hello dataset as a dummy input dataset toohello custom .NET activity.</span></span> <span data-ttu-id="701ef-435">U kunt vervolgens toegang Hallo van service-verbindingsreeks in Hallo aangepaste activiteitscode gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="701ef-435">You can then access hello linked service's connection string in hello custom activity code.</span></span>  

## <a name="update-custom-activity"></a><span data-ttu-id="701ef-436">Aangepaste activiteit bijwerken</span><span class="sxs-lookup"><span data-stu-id="701ef-436">Update custom activity</span></span>
<span data-ttu-id="701ef-437">Als u de code voor de aangepaste activiteit Hallo Hallo bijwerkt, samenstellen en Hallo zip-bestand met nieuwe toohello blob-opslag van de binaire bestanden uploaden.</span><span class="sxs-lookup"><span data-stu-id="701ef-437">If you update hello code for hello custom activity, build it, and upload hello zip file that contains new binaries toohello blob storage.</span></span>

## <a name="appdomain-isolation"></a><span data-ttu-id="701ef-438">AppDomain-isolatie</span><span class="sxs-lookup"><span data-stu-id="701ef-438">Appdomain isolation</span></span>
<span data-ttu-id="701ef-439">Zie [Cross AppDomain voorbeeld](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) die laat zien u hoe toocreate een aangepaste activiteit die geen beperkte tooassembly-versies die worden gebruikt door Hallo Data Factory launcher (voorbeeld: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, enz.).</span><span class="sxs-lookup"><span data-stu-id="701ef-439">See [Cross AppDomain Sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) that shows you how toocreate a custom activity that is not constrained tooassembly versions used by hello Data Factory launcher (example: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.).</span></span>

## <a name="access-extended-properties"></a><span data-ttu-id="701ef-440">Uitgebreide eigenschappen toegang</span><span class="sxs-lookup"><span data-stu-id="701ef-440">Access extended properties</span></span>
<span data-ttu-id="701ef-441">U kunt uitgebreide eigenschappen declareren in Hallo activiteits-JSON zoals weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="701ef-441">You can declare extended properties in hello activity JSON as shown in hello following sample:</span></span>

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


<span data-ttu-id="701ef-442">In voorbeeld hello, zijn er twee uitgebreide eigenschappen: **SliceStart** en **DataFactoryName**.</span><span class="sxs-lookup"><span data-stu-id="701ef-442">In hello example, there are two extended properties: **SliceStart** and **DataFactoryName**.</span></span> <span data-ttu-id="701ef-443">Hallo-waarde voor SliceStart is gebaseerd op Hallo SliceStart systeemvariabele.</span><span class="sxs-lookup"><span data-stu-id="701ef-443">hello value for SliceStart is based on hello SliceStart system variable.</span></span> <span data-ttu-id="701ef-444">Zie [systeemvariabelen](data-factory-functions-variables.md) voor een lijst met ondersteunde systeemvariabelen.</span><span class="sxs-lookup"><span data-stu-id="701ef-444">See [System Variables](data-factory-functions-variables.md) for a list of supported system variables.</span></span> <span data-ttu-id="701ef-445">Hallo-waarde voor DataFactoryName is vastgelegde tooCustomActivityFactory.</span><span class="sxs-lookup"><span data-stu-id="701ef-445">hello value for DataFactoryName is hard-coded tooCustomActivityFactory.</span></span>

<span data-ttu-id="701ef-446">tooaccess deze uitgebreide eigenschappen in Hallo **Execute** methode gebruik code vergelijkbare toohello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="701ef-446">tooaccess these extended properties in hello **Execute** method, use code similar toohello following code:</span></span>

```csharp
// tooget extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// toolog all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a><span data-ttu-id="701ef-447">Automatische schaling van Azure Batch</span><span class="sxs-lookup"><span data-stu-id="701ef-447">Auto-scaling of Azure Batch</span></span>
<span data-ttu-id="701ef-448">U kunt ook maken met een Azure Batch-pool met **automatisch schalen** functie.</span><span class="sxs-lookup"><span data-stu-id="701ef-448">You can also create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="701ef-449">U kunt bijvoorbeeld een azure batch-pool maken met 0 toegewezen virtuele machines en een formule voor automatisch schalen is op basis van Hallo aantal in behandeling zijnde taken.</span><span class="sxs-lookup"><span data-stu-id="701ef-449">For example, you could create an azure batch pool with 0 dedicated VMs and an autoscale formula based on hello number of pending tasks.</span></span> 

<span data-ttu-id="701ef-450">Hallo formule hier realiseert Hallo volgende gedrag: wanneer Hallo van toepassingen in eerste instantie is gemaakt, wordt 1 VM gestart.</span><span class="sxs-lookup"><span data-stu-id="701ef-450">hello sample formula here achieves hello following behavior: When hello pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="701ef-451">$PendingTasks metriek definieert Hallo aantal taken in uitvoering + actief (in de wachtrij) staat.</span><span class="sxs-lookup"><span data-stu-id="701ef-451">$PendingTasks metric defines hello number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="701ef-452">Hallo formule zoekt Hallo gemiddelde aantal in behandeling zijnde taken in Hallo afgelopen 180 seconden en dienovereenkomstig TargetDedicated ingesteld.</span><span class="sxs-lookup"><span data-stu-id="701ef-452">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="701ef-453">Hiermee zorgt u ervoor dat TargetDedicated nooit zich verder uitstrekt dan 25 virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="701ef-453">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="701ef-454">Dus als nieuwe taken worden verzonden, pool automatisch groeit en als taken zijn voltooid, virtuele machines worden gratis één voor één en Hallo automatisch schalen die virtuele machines wordt verkleind.</span><span class="sxs-lookup"><span data-stu-id="701ef-454">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and hello autoscaling shrinks those VMs.</span></span> <span data-ttu-id="701ef-455">startingNumberOfVMs en maxNumberofVMs kunnen worden aangepast tooyour behoeften.</span><span class="sxs-lookup"><span data-stu-id="701ef-455">startingNumberOfVMs and maxNumberofVMs can be adjusted tooyour needs.</span></span>

<span data-ttu-id="701ef-456">De formule voor automatisch schalen:</span><span class="sxs-lookup"><span data-stu-id="701ef-456">Autoscale formula:</span></span>

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

<span data-ttu-id="701ef-457">Zie [automatisch schalen rekenknooppunten in een Azure Batch-pool](../batch/batch-automatic-scaling.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="701ef-457">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

<span data-ttu-id="701ef-458">Als groep Hallo Hallo standaard [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), Hallo Batch-service kan enige tijd duren 15-30 minuten tooprepare Hallo VM voordat Hallo aangepaste activiteit wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="701ef-458">If hello pool is using hello default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch service could take 15-30 minutes tooprepare hello VM before running hello custom activity.</span></span>  <span data-ttu-id="701ef-459">Als Hallo groep van een andere autoScaleEvaluationInterval gebruikmaakt, Hallo Batch-service kan enige tijd duren autoScaleEvaluationInterval + 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="701ef-459">If hello pool is using a different autoScaleEvaluationInterval, hello Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>

## <a name="use-hdinsight-compute-service"></a><span data-ttu-id="701ef-460">HDInsight compute-service gebruiken</span><span class="sxs-lookup"><span data-stu-id="701ef-460">Use HDInsight compute service</span></span>
<span data-ttu-id="701ef-461">In scenario hello gebruikt u Azure Batch compute toorun Hallo aangepaste activiteit.</span><span class="sxs-lookup"><span data-stu-id="701ef-461">In hello walkthrough, you used Azure Batch compute toorun hello custom activity.</span></span> <span data-ttu-id="701ef-462">U kunt ook uw eigen HDInsight op basis van Windows-cluster gebruiken of Data Factory Windows gebaseerd HDInsight-cluster op aanvraag maken en deze Hallo aangepaste activiteit op Hallo HDInsight-cluster worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="701ef-462">You can also use your own Windows-based HDInsight cluster or have Data Factory create an on-demand Windows-based HDInsight cluster and have hello custom activity run on hello HDInsight cluster.</span></span> <span data-ttu-id="701ef-463">Hier volgen Hallo hoofdstappen voor het gebruik van een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="701ef-463">Here are hello high-level steps for using an HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="701ef-464">Hallo aangepaste .NET-activiteiten alleen op Windows gebaseerde HDInsight-clusters worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="701ef-464">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="701ef-465">Een tijdelijke oplossing voor deze beperking is toouse Hallo kaart verminderen activiteit toorun aangepaste Java-code op een Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="701ef-465">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="701ef-466">Een andere optie is toouse een Azure Batch-pool van virtuele machines toorun aangepaste activiteiten in plaats van een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="701ef-466">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>
 

1. <span data-ttu-id="701ef-467">Maak een gekoppelde HDInsight-service.</span><span class="sxs-lookup"><span data-stu-id="701ef-467">Create an Azure HDInsight linked service.</span></span>   
2. <span data-ttu-id="701ef-468">Gebruik HDInsight gekoppelde service in plaats van **AzureBatchLinkedService** in Hallo pipeline JSON.</span><span class="sxs-lookup"><span data-stu-id="701ef-468">Use HDInsight linked service in place of **AzureBatchLinkedService** in hello pipeline JSON.</span></span>

<span data-ttu-id="701ef-469">Als u wilt dat tootest met Hallo scenario wijziging **start** en **end** time-out voor de pijplijn hello, zodat u Hallo scenario Hello Azure HDInsight-service testen kunt.</span><span class="sxs-lookup"><span data-stu-id="701ef-469">If you want tootest it with hello walkthrough, change **start** and **end** times for hello pipeline so that you can test hello scenario with hello Azure HDInsight service.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="701ef-470">Een gekoppelde HDInsight-service maken</span><span class="sxs-lookup"><span data-stu-id="701ef-470">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="701ef-471">Hello Azure Data Factory-service ondersteunt het maken van een cluster op aanvraag en gebruik ze tooprocess invoer tooproduce uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="701ef-471">hello Azure Data Factory service supports creation of an on-demand cluster and use it tooprocess input tooproduce output data.</span></span> <span data-ttu-id="701ef-472">U kunt ook uw eigen cluster tooperform Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="701ef-472">You can also use your own cluster tooperform hello same.</span></span> <span data-ttu-id="701ef-473">Wanneer u de HDInsight-cluster op aanvraag, wordt een cluster wordt gemaakt voor elk segment.</span><span class="sxs-lookup"><span data-stu-id="701ef-473">When you use on-demand HDInsight cluster, a cluster gets created for each slice.</span></span> <span data-ttu-id="701ef-474">Dat als u uw eigen HDInsight-cluster gebruikt, Hallo cluster gereed is Hallo tooprocess onmiddellijk segment.</span><span class="sxs-lookup"><span data-stu-id="701ef-474">Whereas, if you use your own HDInsight cluster, hello cluster is ready tooprocess hello slice immediately.</span></span> <span data-ttu-id="701ef-475">Daarom wanneer u on-demand-cluster gebruikt, kan er geen uitvoergegevens Hallo zo snel wanneer u uw eigen cluster gebruikt.</span><span class="sxs-lookup"><span data-stu-id="701ef-475">Therefore, when you use on-demand cluster, you may not see hello output data as quickly as when you use your own cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="701ef-476">Tijdens runtime werkt een exemplaar van een .NET-activiteit alleen op een knooppunt van de werknemer in Hallo HDInsight-cluster. kan niet uitgebreid toorun op meerdere knooppunten.</span><span class="sxs-lookup"><span data-stu-id="701ef-476">At runtime, an instance of a .NET activity runs only on one worker node in hello HDInsight cluster; it cannot be scaled toorun on multiple nodes.</span></span> <span data-ttu-id="701ef-477">Meerdere exemplaren van de activiteit .NET kunnen parallel worden uitgevoerd op verschillende knooppunten van Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="701ef-477">Multiple instances of .NET activity can run in parallel on different nodes of hello HDInsight cluster.</span></span>
>
>

##### <a name="toouse-an-on-demand-hdinsight-cluster"></a><span data-ttu-id="701ef-478">toouse een HDInsight-cluster op aanvraag</span><span class="sxs-lookup"><span data-stu-id="701ef-478">toouse an on-demand HDInsight cluster</span></span>
1. <span data-ttu-id="701ef-479">In Hallo **Azure-portal**, klikt u op **maken en implementeren** in Hallo Data Factory-startpagina.</span><span class="sxs-lookup"><span data-stu-id="701ef-479">In hello **Azure portal**, click **Author and Deploy** in hello Data Factory home page.</span></span>
2. <span data-ttu-id="701ef-480">In Hallo Data Factory-Editor, klikt u op **nieuwe berekening** van Hallo opdracht en selecteer **On-demand HDInsight-cluster** in Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="701ef-480">In hello Data Factory Editor, click **New compute** from hello command bar and select **On-demand HDInsight cluster** from hello menu.</span></span>
3. <span data-ttu-id="701ef-481">Hallo na wijzigingen toohello JSON-script maken:</span><span class="sxs-lookup"><span data-stu-id="701ef-481">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="701ef-482">Voor Hallo **de clustergrootte** eigenschap Hallo grootte van Hallo HDInsight-cluster opgeven.</span><span class="sxs-lookup"><span data-stu-id="701ef-482">For hello **clusterSize** property, specify hello size of hello HDInsight cluster.</span></span>
   2. <span data-ttu-id="701ef-483">Voor Hallo **timeToLive** eigenschap, opgeven hoe lang Hallo klant inactief mag zijn voordat deze wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="701ef-483">For hello **timeToLive** property, specify how long hello customer can be idle before it is deleted.</span></span>
   3. <span data-ttu-id="701ef-484">Voor Hallo **versie** eigenschap Hallo HDInsight versie gewenste toouse opgeven.</span><span class="sxs-lookup"><span data-stu-id="701ef-484">For hello **version** property, specify hello HDInsight version you want toouse.</span></span> <span data-ttu-id="701ef-485">Als u deze eigenschap uitsluit, wordt de meest recente versie Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="701ef-485">If you exclude this property, hello latest version is used.</span></span>  
   4. <span data-ttu-id="701ef-486">Voor Hallo **linkedServiceName**, geef **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="701ef-486">For hello **linkedServiceName**, specify **AzureStorageLinkedService**.</span></span>

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```

    > [!IMPORTANT]
    > <span data-ttu-id="701ef-487">Hallo aangepaste .NET-activiteiten alleen op Windows gebaseerde HDInsight-clusters worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="701ef-487">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="701ef-488">Een tijdelijke oplossing voor deze beperking is toouse Hallo kaart verminderen activiteit toorun aangepaste Java-code op een Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="701ef-488">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="701ef-489">Een andere optie is toouse een Azure Batch-pool van virtuele machines toorun aangepaste activiteiten in plaats van een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="701ef-489">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>

4. <span data-ttu-id="701ef-490">Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="701ef-490">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

##### <a name="toouse-your-own-hdinsight-cluster"></a><span data-ttu-id="701ef-491">toouse uw eigen HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="701ef-491">toouse your own HDInsight cluster:</span></span>
1. <span data-ttu-id="701ef-492">In Hallo **Azure-portal**, klikt u op **maken en implementeren** in Hallo Data Factory-startpagina.</span><span class="sxs-lookup"><span data-stu-id="701ef-492">In hello **Azure portal**, click **Author and Deploy** in hello Data Factory home page.</span></span>
2. <span data-ttu-id="701ef-493">In Hallo **Data Factory-Editor**, klikt u op **nieuwe berekening** van Hallo opdracht en selecteer **HDInsight-cluster** in Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="701ef-493">In hello **Data Factory Editor**, click **New compute** from hello command bar and select **HDInsight cluster** from hello menu.</span></span>
3. <span data-ttu-id="701ef-494">Hallo na wijzigingen toohello JSON-script maken:</span><span class="sxs-lookup"><span data-stu-id="701ef-494">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="701ef-495">Voor Hallo **clusterUri** eigenschap, Voer Hallo-URL voor uw HDInsight.</span><span class="sxs-lookup"><span data-stu-id="701ef-495">For hello **clusterUri** property, enter hello URL for your HDInsight.</span></span> <span data-ttu-id="701ef-496">Bijvoorbeeld: https://<clustername>.azurehdinsight.net/</span><span class="sxs-lookup"><span data-stu-id="701ef-496">For example: https://<clustername>.azurehdinsight.net/</span></span>     
   2. <span data-ttu-id="701ef-497">Voor Hallo **gebruikersnaam** eigenschap, voer de gebruikersnaam Hallo wie toegang tot toohello HDInsight-cluster heeft.</span><span class="sxs-lookup"><span data-stu-id="701ef-497">For hello **UserName** property, enter hello user name who has access toohello HDInsight cluster.</span></span>
   3. <span data-ttu-id="701ef-498">Voor Hallo **wachtwoord** eigenschap Hallo wachtwoord invoeren voor Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="701ef-498">For hello **Password** property, enter hello password for hello user.</span></span>
   4. <span data-ttu-id="701ef-499">Voor Hallo **LinkedServiceName** eigenschap, voer **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="701ef-499">For hello **LinkedServiceName** property, enter **AzureStorageLinkedService**.</span></span>
4. <span data-ttu-id="701ef-500">Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="701ef-500">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

<span data-ttu-id="701ef-501">Zie [gekoppelde services berekenen](data-factory-compute-linked-services.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="701ef-501">See [Compute linked services](data-factory-compute-linked-services.md) for details.</span></span>

<span data-ttu-id="701ef-502">In Hallo **pipeline JSON**, HDInsight gebruiken (op aanvraag of uw eigen) gekoppelde service:</span><span class="sxs-lookup"><span data-stu-id="701ef-502">In hello **pipeline JSON**, use HDInsight (on-demand or your own) linked service:</span></span>

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="create-a-custom-activity-by-using-net-sdk"></a><span data-ttu-id="701ef-503">Een aangepaste activiteit maken met behulp van de .NET SDK</span><span class="sxs-lookup"><span data-stu-id="701ef-503">Create a custom activity by using .NET SDK</span></span>
<span data-ttu-id="701ef-504">In het Hallo-procedure in dit artikel maakt u een gegevensfactory met een pipeline die gebruikmaakt van aangepaste activiteit Hallo via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="701ef-504">In hello walkthrough in this article, you create a data factory with a pipeline that uses hello custom activity by using hello Azure portal.</span></span> <span data-ttu-id="701ef-505">Hallo volgende code laat zien u hoe toocreate gegevensfactory Hallo in plaats daarvan via .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="701ef-505">hello following code shows you how toocreate hello data factory by using .NET SDK instead.</span></span> <span data-ttu-id="701ef-506">U vindt meer informatie over het gebruik van de SDK tooprogrammatically pijplijnen maken in Hallo [een pijplijn maken met de kopieeractiviteit met behulp van de .NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="701ef-506">You can find more details about using SDK tooprogrammatically create pipelines in hello [create a pipeline with copy activity by using .NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md) article.</span></span> 

```csharp
using System;
using System.Configuration;
using System.Collections.ObjectModel;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.Azure;
using Microsoft.Azure.Management.DataFactories;
using Microsoft.Azure.Management.DataFactories.Models;
using Microsoft.Azure.Management.DataFactories.Common.Models;

using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Collections.Generic;

namespace DataFactoryAPITestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // create data factory management client

            // TODO: replace ADFTutorialResourceGroup with hello name of your resource group.
            string resourceGroupName = "ADFTutorialResourceGroup";

            // TODO: replace APITutorialFactory with a name that is globally unique. For example: APITutorialFactory04212017
            string dataFactoryName = "APITutorialFactory";

            TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
                ConfigurationManager.AppSettings["SubscriptionId"],
                GetAuthorizationHeader().Result);

            Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

            DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);

            Console.WriteLine("Creating a data factory");
            client.DataFactories.CreateOrUpdate(resourceGroupName,
                new DataFactoryCreateOrUpdateParameters()
                {
                    DataFactory = new DataFactory()
                    {
                        Name = dataFactoryName,
                        Location = "westus",
                        Properties = new DataFactoryProperties()
                    }
                }
            );

            // create a linked service for input data store: Azure Storage
            Console.WriteLine("Creating Azure Storage linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureStorageLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: Replace <accountname> and <accountkey> with name and key of your Azure Storage account.
                            new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>")
                        )
                    }
                }
            );

            // create a linked service for output data store: Azure SQL Database
            Console.WriteLine("Creating Azure Batch linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureBatchLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: replace <batchaccountname> and <yourbatchaccountkey> with name and key of your Azure Batch account
                            new AzureBatchLinkedService("<batchaccountname>", "https://westus.batch.azure.com", "<yourbatchaccountkey>", "myazurebatchpool", "AzureStorageLinkedService")
                        )
                    }
                }
            );

            // create input and output datasets
            Console.WriteLine("Creating input and output datasets");
            string Dataset_Source = "InputDataset";
            string Dataset_Destination = "OutputDataset";

            Console.WriteLine("Creating input dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Source,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FolderPath = "adftutorial/customactivityinput/",
                                Format = new TextFormat()
                            },
                            External = true,
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },

                            Policy = new Policy() { }
                        }
                    }
                });

            Console.WriteLine("Creating output dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Destination,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FileName = "{slice}.txt",
                                FolderPath = "adftutorial/customactivityoutput/",
                                PartitionedBy = new List<Partition>()
                                {
                                    new Partition()
                                    {
                                        Name = "slice",
                                        Value = new DateTimePartitionValue()
                                        {
                                            Date = "SliceStart",
                                            Format = "yyyy-MM-dd-HH"
                                        }
                                    }
                                }
                            },
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },
                        }
                    }
                });

            Console.WriteLine("Creating a custom activity pipeline");
            DateTime PipelineActivePeriodStartTime = new DateTime(2017, 3, 9, 0, 0, 0, 0, DateTimeKind.Utc);
            DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
            string PipelineName = "ADFTutorialPipelineCustom";

            client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new PipelineCreateOrUpdateParameters()
                {
                    Pipeline = new Pipeline()
                    {
                        Name = PipelineName,
                        Properties = new PipelineProperties()
                        {
                            Description = "Use custom activity",

                            // Initial value for pipeline's active period. With this, you won't need tooset slice status
                            Start = PipelineActivePeriodStartTime,
                            End = PipelineActivePeriodEndTime,
                            IsPaused = false,

                            Activities = new List<Activity>()
                            {
                                new Activity()
                                {
                                    Name = "MyDotNetActivity",
                                    Inputs = new List<ActivityInput>()
                                    {
                                        new ActivityInput() {
                                            Name = Dataset_Source
                                        }
                                    },
                                    Outputs = new List<ActivityOutput>()
                                    {
                                        new ActivityOutput()
                                        {
                                            Name = Dataset_Destination
                                        }
                                    },
                                    LinkedServiceName = "AzureBatchLinkedService",
                                    TypeProperties = new DotNetActivity()
                                    {
                                        AssemblyName = "MyDotNetActivity.dll",
                                        EntryPoint = "MyDotNetActivityNS.MyDotNetActivity",
                                        PackageLinkedService = "AzureStorageLinkedService",
                                        PackageFile = "customactivitycontainer/MyDotNetActivity.zip",
                                        ExtendedProperties = new Dictionary<string, string>()
                                        {
                                            { "SliceStart", "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"}
                                        }
                                    },
                                    Policy = new ActivityPolicy()
                                    {
                                        Concurrency = 2,
                                        ExecutionPriorityOrder = "OldestFirst",
                                        Retry = 3,
                                        Timeout = new TimeSpan(0,0,30,0),
                                        Delay = new TimeSpan()
                                    }
                                }
                            }
                        }
                    }
                });
        }

        public static async Task<string> GetAuthorizationHeader()
        {
            AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
            ClientCredential credential = new ClientCredential(
                ConfigurationManager.AppSettings["ApplicationId"],
                ConfigurationManager.AppSettings["Password"]);
            AuthenticationResult result = await context.AcquireTokenAsync(
                resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                clientCredential: credential);

            if (result != null)
                return result.AccessToken;

            throw new InvalidOperationException("Failed tooacquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a><span data-ttu-id="701ef-507">Fouten opsporen in aangepaste activiteit in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="701ef-507">Debug custom activity in Visual Studio</span></span>
<span data-ttu-id="701ef-508">Hallo [Azure Data Factory - lokale omgeving](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) voorbeeld op GitHub omvat een hulpprogramma waarmee u aangepaste .NET-activiteiten toodebug vanuit Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="701ef-508">hello [Azure Data Factory - local environment](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) sample on GitHub includes a tool that allows you toodebug custom .NET activities within Visual Studio.</span></span>  


## <a name="sample-custom-activities-on-github"></a><span data-ttu-id="701ef-509">Aangepaste activiteiten voorbeeld op GitHub</span><span class="sxs-lookup"><span data-stu-id="701ef-509">Sample custom activities on GitHub</span></span>
| <span data-ttu-id="701ef-510">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="701ef-510">Sample</span></span> | <span data-ttu-id="701ef-511">Welke aangepaste activiteit doet</span><span class="sxs-lookup"><span data-stu-id="701ef-511">What custom activity does</span></span> |
| --- | --- |
| <span data-ttu-id="701ef-512">[Het Downloadprogramma voor het HTTP-gegevens](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span><span class="sxs-lookup"><span data-stu-id="701ef-512">[HTTP Data Downloader](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span></span> |<span data-ttu-id="701ef-513">Downloadt gegevens van een HTTP-eindpunt tooAzure Blob Storage met aangepaste C#-activiteit in de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="701ef-513">Downloads data from an HTTP Endpoint tooAzure Blob Storage using custom C# Activity in Data Factory.</span></span> |
| [<span data-ttu-id="701ef-514">Twitter-gevoel Analysis-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="701ef-514">Twitter Sentiment Analysis sample</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |<span data-ttu-id="701ef-515">Hiermee wordt een Azure ML-model en komen gevoel analyse, score berekenen, voorspelling enzovoort.</span><span class="sxs-lookup"><span data-stu-id="701ef-515">Invokes an Azure ML model and do sentiment analysis, scoring, prediction etc.</span></span> |
| <span data-ttu-id="701ef-516">[R-Script uitvoeren](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span><span class="sxs-lookup"><span data-stu-id="701ef-516">[Run R Script](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span></span> |<span data-ttu-id="701ef-517">R-script worden opgeroepen door RScript.exe uitgevoerd op uw HDInsight-cluster al met R is geïnstalleerd op.</span><span class="sxs-lookup"><span data-stu-id="701ef-517">Invokes R script by running RScript.exe on your HDInsight cluster that already has R Installed on it.</span></span> |
| [<span data-ttu-id="701ef-518">Cross-activiteit van AppDomain .NET</span><span class="sxs-lookup"><span data-stu-id="701ef-518">Cross AppDomain .NET Activity</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |<span data-ttu-id="701ef-519">Maakt gebruik van verschillende assembly-versies van de waarden die worden gebruikt door Hallo Data Factory starten</span><span class="sxs-lookup"><span data-stu-id="701ef-519">Uses different assembly versions from ones used by hello Data Factory launcher</span></span> |
| [<span data-ttu-id="701ef-520">Opnieuw verwerken van een model in Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="701ef-520">Reprocess a model in Azure Analysis Services</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  <span data-ttu-id="701ef-521">Een model in Azure Analysis Services opnieuw verwerken.</span><span class="sxs-lookup"><span data-stu-id="701ef-521">Reprocesses a model in Azure Analysis Services.</span></span> |

[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: ./media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: ./media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png
