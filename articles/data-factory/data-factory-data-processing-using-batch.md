---
title: aaaProcess grootschalige gegevenssets met behulp van Data Factory en Batch | Microsoft Docs
description: Hierin wordt beschreven hoe tooprocess grote hoeveelheden gegevens in een Azure Data Factory met behulp van de mogelijkheid parallelle verwerking van Azure Batch pipeline.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a><span data-ttu-id="06d6a-103">Grootschalige gegevenssets verwerken met Data Factory en Batch</span><span class="sxs-lookup"><span data-stu-id="06d6a-103">Process large-scale datasets using Data Factory and Batch</span></span>
<span data-ttu-id="06d6a-104">In dit artikel beschrijft een architectuur van een Voorbeeldoplossing die wordt verplaatst en grootschalige gegevenssets in een automatische en geplande wijze verwerkt.</span><span class="sxs-lookup"><span data-stu-id="06d6a-104">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span></span> <span data-ttu-id="06d6a-105">Het bevat ook een end-to-end-overzicht tooimplement Hallo oplossing met behulp van Azure Data Factory en Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="06d6a-105">It also provides an end-to-end walkthrough tooimplement hello solution using Azure Data Factory and Azure Batch.</span></span>

<span data-ttu-id="06d6a-106">In dit artikel is langer dan het typische artikel omdat deze een overzicht van een Voorbeeldoplossing voor het volledige bevat.</span><span class="sxs-lookup"><span data-stu-id="06d6a-106">This article is longer than our typical article because it contains a walkthrough of an entire sample solution.</span></span> <span data-ttu-id="06d6a-107">Als u nieuwe tooBatch en Data Factory, kunt u lezen over deze services en hoe ze samen werken.</span><span class="sxs-lookup"><span data-stu-id="06d6a-107">If you are new tooBatch and Data Factory, you can learn about these services and how they work together.</span></span> <span data-ttu-id="06d6a-108">Als u over Hallo services weet en zijn ontwerpen/veranderd een oplossing, kunt u zich richten alleen op Hallo [architectuur sectie](#architecture-of-sample-solution) van Hallo artikel en als u een prototype of een oplossing ontwikkelt, u kunt ook tootry uit Stapsgewijze instructies in Hallo [scenario](#implementation-of-sample-solution).</span><span class="sxs-lookup"><span data-stu-id="06d6a-108">If you know something about hello services and are designing/architecting a solution, you may focus just on hello [architecture section](#architecture-of-sample-solution) of hello article and if you are developing a prototype or a solution, you may also want tootry out step-by-step instructions in hello [walkthrough](#implementation-of-sample-solution).</span></span> <span data-ttu-id="06d6a-109">Wij willen graag uw opmerkingen over deze inhoud en hoe u deze gebruiken.</span><span class="sxs-lookup"><span data-stu-id="06d6a-109">We invite your comments about this content and how you use it.</span></span>

<span data-ttu-id="06d6a-110">Eerst gaan we kijken hoe Data Factory en Batch services helpen kunnen bij het verwerken van grote gegevenssets in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="06d6a-110">First, let's look at how Data Factory and Batch services can help with processing large datasets in hello cloud.</span></span>     

## <a name="why-azure-batch"></a><span data-ttu-id="06d6a-111">Waarom Azure Batch?</span><span class="sxs-lookup"><span data-stu-id="06d6a-111">Why Azure Batch?</span></span>
<span data-ttu-id="06d6a-112">Azure Batch kunt u toorun grootschalige parallelle en high-performance computing (HPC) toepassingen efficiënt in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="06d6a-112">Azure Batch enables you toorun large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="06d6a-113">Het is een platformservice die toorun rekenintensief werk op een beheerde verzameling van virtuele machines plant en kan automatisch scale compute resources toomeet Hallo behoeften van uw jobs.</span><span class="sxs-lookup"><span data-stu-id="06d6a-113">It's a platform service that schedules compute-intensive work toorun on a managed collection of virtual machines, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span>

<span data-ttu-id="06d6a-114">Met de Hallo Batch-service definieert u Azure compute resources tooexecute uw toepassingen parallel, en op schaal.</span><span class="sxs-lookup"><span data-stu-id="06d6a-114">With hello Batch service, you define Azure compute resources tooexecute your applications in parallel, and at scale.</span></span> <span data-ttu-id="06d6a-115">U kunt uitvoeren op aanvraag of geplande taken en u hoeft niet toomanually maken, configureren en beheren van een HPC-cluster, individuele virtuele machines, virtuele netwerken of een complexe job en taakplanningsinfrastructuur.</span><span class="sxs-lookup"><span data-stu-id="06d6a-115">You can run on-demand or scheduled jobs, and you don't need toomanually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span>

<span data-ttu-id="06d6a-116">Zie Hallo artikelen te volgen als u niet bekend met Azure Batch bent als het helpt Hallo architectuur/implementatie van Hallo-oplossing wordt beschreven in dit artikel gaan.</span><span class="sxs-lookup"><span data-stu-id="06d6a-116">See hello following articles if you are not familiar with Azure Batch as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>   

* [<span data-ttu-id="06d6a-117">Basisbeginselen van Azure Batch</span><span class="sxs-lookup"><span data-stu-id="06d6a-117">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
* [<span data-ttu-id="06d6a-118">Overzicht van de functies van Batch</span><span class="sxs-lookup"><span data-stu-id="06d6a-118">Batch feature overview</span></span>](../batch/batch-api-basics.md)

<span data-ttu-id="06d6a-119">(optioneel) toolearn meer informatie over Azure Batch Zie Hallo [leertraject voor Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span><span class="sxs-lookup"><span data-stu-id="06d6a-119">(optional) toolearn more about Azure Batch, see hello [Learning path for Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span></span>

## <a name="why-azure-data-factory"></a><span data-ttu-id="06d6a-120">Waarom Azure Data Factory?</span><span class="sxs-lookup"><span data-stu-id="06d6a-120">Why Azure Data Factory?</span></span>
<span data-ttu-id="06d6a-121">Data Factory is een cloud-gebaseerde gegevens integration-service die is ingedeeld en automatiseert Hallo verplaatsing en transformatie van gegevens.</span><span class="sxs-lookup"><span data-stu-id="06d6a-121">Data Factory is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="06d6a-122">Hallo Data Factory-service gebruikt, kunt u beheerde gegevenspijplijnen die gegevens verplaatsen van on-premises en in de cloud gegevensarchief winkels tooa gecentraliseerde gegevens (bijvoorbeeld: Azure Blob-opslag), en gegevens met services zoals Azure HDInsight en Azure proces/transformatie Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="06d6a-122">Using hello Data Factory service, you can create managed data pipelines that move data from on-premises and cloud data stores tooa centralized data store (for example: Azure Blob Storage), and process/transform data using services such as Azure HDInsight and Azure Machine Learning.</span></span> <span data-ttu-id="06d6a-123">U kunt ook gegevens pijplijnen toorun plannen in een geplande manier (elk uur, dagelijks, wekelijks, enz.) en een monitor en deze in een oogopslag tooidentify problemen beheren en actie ondernemen.</span><span class="sxs-lookup"><span data-stu-id="06d6a-123">You can also schedule data pipelines toorun in a scheduled manner (hourly, daily, weekly, etc.) and monitor and manage them at a glance tooidentify issues and take action.</span></span>

<span data-ttu-id="06d6a-124">Zie Hallo artikelen te volgen als u niet bekend met Azure Data Factory bent als het helpt Hallo architectuur/implementatie van Hallo-oplossing wordt beschreven in dit artikel gaan.</span><span class="sxs-lookup"><span data-stu-id="06d6a-124">See hello following articles if you are not familiar with Azure Data Factory as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>  

* [<span data-ttu-id="06d6a-125">Introductie van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="06d6a-125">Introduction of Azure Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="06d6a-126">Uw eerste pijplijn voor gegevens</span><span class="sxs-lookup"><span data-stu-id="06d6a-126">Build your first data pipeline</span></span>](data-factory-build-your-first-pipeline.md)   

<span data-ttu-id="06d6a-127">(optioneel) toolearn meer informatie over Azure Data Factory Zie Hallo [leertraject voor Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="06d6a-127">(optional) toolearn more about Azure Data Factory, see hello [Learning path for Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span></span>

## <a name="data-factory-and-batch-together"></a><span data-ttu-id="06d6a-128">Data Factory en in Batch samen</span><span class="sxs-lookup"><span data-stu-id="06d6a-128">Data Factory and Batch together</span></span>
<span data-ttu-id="06d6a-129">Data Factory bevat ingebouwde activiteiten zoals Kopieeractiviteit toocopy of verplaatsen van een brongegevens gegevensarchief tooa doelgegevensopslagplaats en Hive-activiteit tooprocess gegevens met behulp van Hadoop-clusters (HDInsight) in Azure.</span><span class="sxs-lookup"><span data-stu-id="06d6a-129">Data Factory includes built-in activities such as Copy Activity toocopy/move data from a source data store tooa destination data store and Hive Activity tooprocess data using Hadoop clusters (HDInsight) on Azure.</span></span> <span data-ttu-id="06d6a-130">Zie [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) voor een lijst van activiteiten voor gegevenstransformatie ondersteund.</span><span class="sxs-lookup"><span data-stu-id="06d6a-130">See [Data Transformation Activities](data-factory-data-transformation-activities.md) for a list of supported transformation activities.</span></span>

<span data-ttu-id="06d6a-131">Ook kunt u toocreate aangepaste .NET-activiteiten toomove of proces gegevens met uw eigen logica en deze activiteiten worden uitgevoerd op een Azure HDInsight-cluster of op een Azure Batch-pool van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="06d6a-131">It also allows you toocreate custom .NET activities toomove or process data with your own logic and run these activities on an Azure HDInsight cluster or on an Azure Batch pool of VMs.</span></span> <span data-ttu-id="06d6a-132">Wanneer u Azure Batch gebruikt, kunt u Hallo groep tooauto-scale configureren (toevoegen of verwijderen van virtuele machines op basis van de werkbelasting Hallo) op basis van een formule die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="06d6a-132">When you use Azure Batch, you can configure hello pool tooauto-scale (add or remove VMs based on hello workload) based on a formula you provide.</span></span>     

## <a name="architecture-of-sample-solution"></a><span data-ttu-id="06d6a-133">Architectuur van Voorbeeldoplossing</span><span class="sxs-lookup"><span data-stu-id="06d6a-133">Architecture of sample solution</span></span>
<span data-ttu-id="06d6a-134">Hoewel Hallo architectuur die wordt beschreven in dit artikel is bedoeld voor een eenvoudige oplossing, is de relevante toocomplex scenario's zoals risico modellering van financiële diensten, verwerking van afbeeldingen en rendering en Toepassingsgeoriënteerde analyse.</span><span class="sxs-lookup"><span data-stu-id="06d6a-134">Even though hello architecture described in this article is for a simple solution, it is relevant toocomplex scenarios such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span></span>

<span data-ttu-id="06d6a-135">Hallo diagram illustreert 1) hoe Data Factory gegevensverplaatsing ingedeeld en verwerking en 2) de manier waarop Azure Batch verwerkt Hallo gegevens op een parallelle manier.</span><span class="sxs-lookup"><span data-stu-id="06d6a-135">hello diagram illustrates 1) how Data Factory orchestrates data movement and processing and 2) how Azure Batch processes hello data in a parallel manner.</span></span> <span data-ttu-id="06d6a-136">Downloaden en afdrukken Hallo diagram ter referentie (11 x 17.</span><span class="sxs-lookup"><span data-stu-id="06d6a-136">Download and print hello diagram for easy reference (11 x 17 in.</span></span> <span data-ttu-id="06d6a-137">of A3-grootte): [HPC en gegevens orchestration met behulp van Azure Batch- en Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span><span class="sxs-lookup"><span data-stu-id="06d6a-137">or A3 size): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span></span>

<span data-ttu-id="06d6a-138">[![Diagram van grootschalige gegevensverwerking](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="06d6a-138">[![Large-scale data processing diagram](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span></span>

<span data-ttu-id="06d6a-139">Hallo bevat volgende lijst de basisstappen Hallo van Hallo proces.</span><span class="sxs-lookup"><span data-stu-id="06d6a-139">hello following list provides hello basic steps of hello process.</span></span> <span data-ttu-id="06d6a-140">Hallo-oplossing omvat code en uitleg toobuild Hallo end-to-end-oplossing.</span><span class="sxs-lookup"><span data-stu-id="06d6a-140">hello solution includes code and explanations toobuild hello end-to-end solution.</span></span>

1. <span data-ttu-id="06d6a-141">**Azure Batch configureren met een pool van rekenknooppunten (virtuele machines)**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-141">**Configure Azure Batch with a pool of compute nodes (VMs)**.</span></span> <span data-ttu-id="06d6a-142">U kunt het aantal knooppunten Hallo en de grootte van elk knooppunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="06d6a-142">You can specify hello number of nodes and size of each node.</span></span>
2. <span data-ttu-id="06d6a-143">**Maak een Azure Data Factory-instantie** die is geconfigureerd met de entiteiten die Azure blob-opslag, Azure Batch compute-service, invoer-en uitvoergegevens en een werkstroom/pijplijn met activiteiten die verplaatsen en gegevens transformeren vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="06d6a-143">**Create an Azure Data Factory instance** that is configured with entities that represent Azure blob storage, Azure Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span></span>
3. <span data-ttu-id="06d6a-144">**Maak een aangepaste .NET-activiteit in Hallo Data Factory-pijplijn**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-144">**Create a custom .NET activity in hello Data Factory pipeline**.</span></span> <span data-ttu-id="06d6a-145">Hallo-activiteit is uw gebruikerscode die wordt uitgevoerd op Hallo Azure Batch-pool.</span><span class="sxs-lookup"><span data-stu-id="06d6a-145">hello activity is your user code that runs on hello Azure Batch pool.</span></span>
4. <span data-ttu-id="06d6a-146">**Opslaan van grote hoeveelheden gegevens als blobs in Azure storage**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-146">**Store large amounts of input data as blobs in Azure storage**.</span></span> <span data-ttu-id="06d6a-147">Gegevens worden in logische segmenten verdeeld (meestal door time).</span><span class="sxs-lookup"><span data-stu-id="06d6a-147">Data is divided into logical slices (usually by time).</span></span>
5. <span data-ttu-id="06d6a-148">**Data Factory kopieert de gegevens die wordt verwerkt parallel** toohello secundaire locatie.</span><span class="sxs-lookup"><span data-stu-id="06d6a-148">**Data Factory copies data that is processed in parallel** toohello secondary location.</span></span>
6. <span data-ttu-id="06d6a-149">**Data Factory uitgevoerd Hallo aangepaste activiteit gebruikmaken van Hallo toegewezen door Batch**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-149">**Data Factory runs hello custom activity using hello pool allocated by Batch**.</span></span> <span data-ttu-id="06d6a-150">Data Factory kunt activiteiten tegelijkertijd worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="06d6a-150">Data Factory can run activities concurrently.</span></span> <span data-ttu-id="06d6a-151">Elke activiteit verwerkt een segment met gegevens.</span><span class="sxs-lookup"><span data-stu-id="06d6a-151">Each activity processes a slice of data.</span></span> <span data-ttu-id="06d6a-152">Hallo resultaten worden opgeslagen in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="06d6a-152">hello results are stored in Azure storage.</span></span>
7. <span data-ttu-id="06d6a-153">**Data Factory Hallo eindresultaat tooa derde locatie verplaatst**, voor distributie via een app of voor verdere verwerking door andere hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="06d6a-153">**Data Factory moves hello final results tooa third location**, either for distribution via an app, or for further processing by other tools.</span></span>

## <a name="implementation-of-sample-solution"></a><span data-ttu-id="06d6a-154">Implementatie van Voorbeeldoplossing</span><span class="sxs-lookup"><span data-stu-id="06d6a-154">Implementation of sample solution</span></span>
<span data-ttu-id="06d6a-155">Hallo Voorbeeldoplossing opzet eenvoudig en tooshow u hoe toouse Data Factory en Batch samen tooprocess gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="06d6a-155">hello sample solution is intentionally simple and is tooshow you how toouse Data Factory and Batch together tooprocess datasets.</span></span> <span data-ttu-id="06d6a-156">Hallo oplossing telt gewoon Hallo aantal exemplaren van een zoekterm ('Microsoft') in invoerbestanden georganiseerd in een tijdreeks.</span><span class="sxs-lookup"><span data-stu-id="06d6a-156">hello solution simply counts hello number of occurrences of a search term (“Microsoft”) in input files organized in a time series.</span></span> <span data-ttu-id="06d6a-157">Het levert Hallo aantal toooutput bestanden.</span><span class="sxs-lookup"><span data-stu-id="06d6a-157">It outputs hello count toooutput files.</span></span>

<span data-ttu-id="06d6a-158">**Tijd**: als u bekend met de basisprincipes van Azure Data Factory en Batch bent en hebben voltooid Hallo vereisten hieronder vermeld, schatten we deze oplossing toocomplete van 1 tot 2 uur duurt.</span><span class="sxs-lookup"><span data-stu-id="06d6a-158">**Time**: If you are familiar with basics of Azure, Data Factory, and Batch, and have completed hello prerequisites listed below, we estimate this solution takes 1-2 hours toocomplete.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="06d6a-159">Vereisten</span><span class="sxs-lookup"><span data-stu-id="06d6a-159">Prerequisites</span></span>
#### <a name="azure-subscription"></a><span data-ttu-id="06d6a-160">Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="06d6a-160">Azure subscription</span></span>
<span data-ttu-id="06d6a-161">Als u geen Azure-abonnement hebt, kunt u een gratis proefaccount maken binnen een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="06d6a-161">If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="06d6a-162">Zie [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="06d6a-162">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

#### <a name="azure-storage-account"></a><span data-ttu-id="06d6a-163">Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="06d6a-163">Azure storage account</span></span>
<span data-ttu-id="06d6a-164">U kunt een Azure storage-account gebruiken voor het opslaan van Hallo gegevens in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="06d6a-164">You use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="06d6a-165">Als u geen Azure storage-account hebt, raadpleegt u [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="06d6a-165">If you don't have an Azure storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="06d6a-166">Hallo Voorbeeldoplossing maakt gebruik van blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="06d6a-166">hello sample solution uses blob storage.</span></span>

#### <a name="azure-batch-account"></a><span data-ttu-id="06d6a-167">Azure Batch-account</span><span class="sxs-lookup"><span data-stu-id="06d6a-167">Azure Batch account</span></span>
<span data-ttu-id="06d6a-168">Een Azure Batch-account maken met Hallo [Azure-portal](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="06d6a-168">Create an Azure Batch account using hello [Azure portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="06d6a-169">Zie [maken en beheren van Azure Batch-account](../batch/batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="06d6a-169">See [Create and manage an Azure Batch account](../batch/batch-account-create-portal.md).</span></span> <span data-ttu-id="06d6a-170">Houd er rekening mee hello Azure Batch-account en de accountsleutel sleutel.</span><span class="sxs-lookup"><span data-stu-id="06d6a-170">Note hello Azure Batch account name and account key.</span></span> <span data-ttu-id="06d6a-171">U kunt ook [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate Azure Batch-account.</span><span class="sxs-lookup"><span data-stu-id="06d6a-171">You can also use [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate an Azure Batch account.</span></span> <span data-ttu-id="06d6a-172">Zie [aan de slag met Azure Batch PowerShell-cmdlets](../batch/batch-powershell-cmdlets-get-started.md) voor gedetailleerde instructies over het gebruik van deze cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06d6a-172">See [Get started with Azure Batch PowerShell cmdlets](../batch/batch-powershell-cmdlets-get-started.md) for detailed instructions on using this cmdlet.</span></span>

<span data-ttu-id="06d6a-173">Hallo Voorbeeldoplossing gebruikt Azure Batch (indirect via een Azure Data Factory-pijplijn) tooprocess gegevens op een parallelle manier op een pool van rekenknooppunten (een beheerde verzameling van virtuele machines).</span><span class="sxs-lookup"><span data-stu-id="06d6a-173">hello sample solution uses Azure Batch (indirectly via an Azure Data Factory pipeline) tooprocess data in a parallel manner on a pool of compute nodes (a managed collection of virtual machines).</span></span>

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a><span data-ttu-id="06d6a-174">Azure Batch-pool van virtuele machines (VM's)</span><span class="sxs-lookup"><span data-stu-id="06d6a-174">Azure Batch pool of virtual machines (VMs)</span></span>
<span data-ttu-id="06d6a-175">Maak een **Azure Batch-pool** met ten minste 2 rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="06d6a-175">Create an **Azure Batch pool** with at least 2 compute nodes.</span></span>

1. <span data-ttu-id="06d6a-176">In Hallo [Azure-portal](https://portal.azure.com), klikt u op **Bladeren** in Hallo menu aan de linkerkant en klik op **Batch-Accounts**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-176">In hello [Azure portal](https://portal.azure.com), click **Browse** in hello left menu, and click **Batch Accounts**.</span></span>
2. <span data-ttu-id="06d6a-177">Selecteer uw Azure Batch-account tooopen hello **Batch-Account** blade.</span><span class="sxs-lookup"><span data-stu-id="06d6a-177">Select your Azure Batch account tooopen hello **Batch Account** blade.</span></span>
3. <span data-ttu-id="06d6a-178">Klik op **Pools** tegel.</span><span class="sxs-lookup"><span data-stu-id="06d6a-178">Click **Pools** tile.</span></span>
4. <span data-ttu-id="06d6a-179">In Hallo **Pools** blade, klik op de knop toevoegen op Hallo werkbalk tooadd een pool.</span><span class="sxs-lookup"><span data-stu-id="06d6a-179">In hello **Pools** blade, click Add button on hello toolbar tooadd a pool.</span></span>
   1. <span data-ttu-id="06d6a-180">Geef een ID voor Hallo pool (**Pool-ID**).</span><span class="sxs-lookup"><span data-stu-id="06d6a-180">Enter an ID for hello pool (**Pool ID**).</span></span> <span data-ttu-id="06d6a-181">Opmerking Hallo **ID van de pool Hallo**; u deze nodig hebt bij het maken van Hallo Data Factory-oplossing.</span><span class="sxs-lookup"><span data-stu-id="06d6a-181">Note hello **ID of hello pool**; you need it when creating hello Data Factory solution.</span></span>
   2. <span data-ttu-id="06d6a-182">Geef **Windows Server 2012 R2** voor Hallo besturingssysteemgroep instelling.</span><span class="sxs-lookup"><span data-stu-id="06d6a-182">Specify **Windows Server 2012 R2** for hello Operating System Family setting.</span></span>
   3. <span data-ttu-id="06d6a-183">Selecteer een **knooppunt prijscategorie**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-183">Select a **node pricing tier**.</span></span>
   4. <span data-ttu-id="06d6a-184">Voer **2** als waarde voor Hallo **doel toegewezen** instelling.</span><span class="sxs-lookup"><span data-stu-id="06d6a-184">Enter **2** as value for hello **Target Dedicated** setting.</span></span>
   5. <span data-ttu-id="06d6a-185">Voer **2** als waarde voor Hallo **maximum aantal taken per knooppunt** instelling.</span><span class="sxs-lookup"><span data-stu-id="06d6a-185">Enter **2** as value for hello **Max tasks per node** setting.</span></span>
   6. <span data-ttu-id="06d6a-186">Klik op **OK** toocreate Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="06d6a-186">Click **OK** toocreate hello pool.</span></span>

#### <a name="azure-storage-explorer"></a><span data-ttu-id="06d6a-187">Azure Opslagverkenner</span><span class="sxs-lookup"><span data-stu-id="06d6a-187">Azure Storage Explorer</span></span>
<span data-ttu-id="06d6a-188">[Azure Storage Explorer 6 (hulpprogramma)](https://azurestorageexplorer.codeplex.com/) of [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (van ClumsyLeaf Software).</span><span class="sxs-lookup"><span data-stu-id="06d6a-188">[Azure Storage Explorer 6 (tool)](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software).</span></span> <span data-ttu-id="06d6a-189">U gebruikt deze hulpprogramma's voor te bekijken en wijzigen van Hallo-gegevens in uw Azure Storage-projecten inclusief Hallo logboeken van uw cloud-gebaseerde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="06d6a-189">You use these tools for inspecting and altering hello data in your Azure Storage projects including hello logs of your cloud-hosted applications.</span></span>

1. <span data-ttu-id="06d6a-190">Maken van een container met de naam **mycontainer** met persoonlijke toegang (geen anonieme toegang)</span><span class="sxs-lookup"><span data-stu-id="06d6a-190">Create a container named **mycontainer** with private access (no anonymous access)</span></span>
2. <span data-ttu-id="06d6a-191">Als u **CloudXplorer**, maakt u mappen en submappen met Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="06d6a-191">If you are using **CloudXplorer**, create folders and subfolders with hello following structure:</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   <span data-ttu-id="06d6a-192">`Inputfolder`en `outputfolder` zijn op het hoogste niveau van de mappen in `mycontainer`.</span><span class="sxs-lookup"><span data-stu-id="06d6a-192">`Inputfolder` and `outputfolder` are top-level folders in `mycontainer`.</span></span> <span data-ttu-id="06d6a-193">Hallo `inputfolder` submappen met de datum / tijd stempels (jjjj-MM-DD-UU).</span><span class="sxs-lookup"><span data-stu-id="06d6a-193">hello `inputfolder` has subfolders with date-time stamps (YYYY-MM-DD-HH).</span></span>

   <span data-ttu-id="06d6a-194">Als u **Azure Opslagverkenner**, in de volgende stap hello, moet u tooupload bestanden met namen: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` enzovoort.</span><span class="sxs-lookup"><span data-stu-id="06d6a-194">If you are using **Azure Storage Explorer**, in hello next step, you need tooupload files with names: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` and so on.</span></span> <span data-ttu-id="06d6a-195">Deze stap maakt automatisch Hallo mappen.</span><span class="sxs-lookup"><span data-stu-id="06d6a-195">This step automatically creates hello folders.</span></span>
3. <span data-ttu-id="06d6a-196">Maak een tekstbestand **bestand.txt** op uw computer met inhoud die Hallo sleutelwoord is **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-196">Create a text file **file.txt** on your machine with content that has hello keyword **Microsoft**.</span></span> <span data-ttu-id="06d6a-197">Bijvoorbeeld: 'aangepaste activiteit Microsoft test aangepaste activiteit Microsoft test'.</span><span class="sxs-lookup"><span data-stu-id="06d6a-197">For example: “test custom activity Microsoft test custom activity Microsoft”.</span></span>
4. <span data-ttu-id="06d6a-198">Het uploaden van Hallo bestand toohello volgende invoer mappen in Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="06d6a-198">Upload hello file toohello following input folders in Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   <span data-ttu-id="06d6a-199">Als u **Azure Opslagverkenner**, Hallo-bestand uploaden **bestand.txt** te**mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-199">If you are using **Azure Storage Explorer**, upload hello file **file.txt** too**mycontainer**.</span></span> <span data-ttu-id="06d6a-200">Klik op **kopie** op Hallo werkbalk toocreate een kopie van het Hallo-blob.</span><span class="sxs-lookup"><span data-stu-id="06d6a-200">Click **Copy** on hello toolbar toocreate a copy of hello blob.</span></span> <span data-ttu-id="06d6a-201">In Hallo **Blob kopiëren** dialoogvenster, wijziging Hallo **blob doelnaam** te`inputfolder/2015-11-16-00/file.txt`.</span><span class="sxs-lookup"><span data-stu-id="06d6a-201">In hello **Copy Blob** dialog box, change hello **destination blob name** too`inputfolder/2015-11-16-00/file.txt`.</span></span> <span data-ttu-id="06d6a-202">Herhaal deze stap toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` enzovoort.</span><span class="sxs-lookup"><span data-stu-id="06d6a-202">Repeat this step toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` and so on.</span></span> <span data-ttu-id="06d6a-203">Deze actie wordt automatisch gemaakt Hallo mappen.</span><span class="sxs-lookup"><span data-stu-id="06d6a-203">This action automatically creates hello folders.</span></span>
5. <span data-ttu-id="06d6a-204">Maken van een andere container met de naam: `customactivitycontainer`.</span><span class="sxs-lookup"><span data-stu-id="06d6a-204">Create another container named: `customactivitycontainer`.</span></span> <span data-ttu-id="06d6a-205">U uploaden Hallo aangepaste activiteit zip-bestand toothis container.</span><span class="sxs-lookup"><span data-stu-id="06d6a-205">You upload hello custom activity zip file toothis container.</span></span>

#### <a name="visual-studio"></a><span data-ttu-id="06d6a-206">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="06d6a-206">Visual Studio</span></span>
<span data-ttu-id="06d6a-207">Installeer Microsoft Visual Studio 2012 of hoger toocreate Hallo aangepaste Batch activiteit toobe in Hallo Data Factory-oplossing gebruikt.</span><span class="sxs-lookup"><span data-stu-id="06d6a-207">Install Microsoft Visual Studio 2012 or later toocreate hello custom Batch activity toobe used in hello Data Factory solution.</span></span>

### <a name="high-level-steps-toocreate-hello-solution"></a><span data-ttu-id="06d6a-208">Stappen op hoog niveau toocreate Hallo oplossing</span><span class="sxs-lookup"><span data-stu-id="06d6a-208">High-level steps toocreate hello solution</span></span>
1. <span data-ttu-id="06d6a-209">Maak een aangepaste activiteit die Hallo gegevensverwerking logica bevat.</span><span class="sxs-lookup"><span data-stu-id="06d6a-209">Create a custom activity that contains hello data processing logic.</span></span>
2. <span data-ttu-id="06d6a-210">Maak een Azure data factory die gebruikmaakt van aangepaste activiteit Hallo:</span><span class="sxs-lookup"><span data-stu-id="06d6a-210">Create an Azure data factory that uses hello custom activity:</span></span>

### <a name="create-hello-custom-activity"></a><span data-ttu-id="06d6a-211">Hallo aangepaste activiteit maken</span><span class="sxs-lookup"><span data-stu-id="06d6a-211">Create hello custom activity</span></span>
<span data-ttu-id="06d6a-212">Hallo Data Factory aangepaste activiteit vormt de kern Hallo van deze Voorbeeldoplossing.</span><span class="sxs-lookup"><span data-stu-id="06d6a-212">hello Data Factory custom activity is hello heart of this sample solution.</span></span> <span data-ttu-id="06d6a-213">Hallo Voorbeeldoplossing gebruikt Azure Batch toorun Hallo aangepaste activiteit.</span><span class="sxs-lookup"><span data-stu-id="06d6a-213">hello sample solution uses Azure Batch toorun hello custom activity.</span></span> <span data-ttu-id="06d6a-214">Zie [aangepaste activiteiten gebruiken in een Azure Data Factory-pijplijn](data-factory-use-custom-activities.md) voor Hallo basisinformatie toodevelop aangepaste activiteiten en gebruik ze in Azure Data Factory pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="06d6a-214">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) for hello basic information toodevelop custom activities and use them in Azure Data Factory pipelines.</span></span>

<span data-ttu-id="06d6a-215">een aangepaste .NET-activiteit die u in een Azure Data Factory-pijplijn gebruiken kunt toocreate, moet u toocreate een **.NET Class Library** project met een klasse die die implementeert **IDotNetActivity** interface.</span><span class="sxs-lookup"><span data-stu-id="06d6a-215">toocreate a .NET custom activity that you can use in an Azure Data Factory pipeline, you need toocreate a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="06d6a-216">Deze interface heeft slechts één methode: **Execute**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-216">This interface has only one method: **Execute**.</span></span> <span data-ttu-id="06d6a-217">Hier volgt Hallo handtekening van Hallo-methode:</span><span class="sxs-lookup"><span data-stu-id="06d6a-217">Here is hello signature of hello method:</span></span>

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

<span data-ttu-id="06d6a-218">Hallo-methode heeft enkele belangrijke onderdelen moet u toounderstand.</span><span class="sxs-lookup"><span data-stu-id="06d6a-218">hello method has a few key components that you need toounderstand.</span></span>

* <span data-ttu-id="06d6a-219">Hallo-methode heeft vier parameters:</span><span class="sxs-lookup"><span data-stu-id="06d6a-219">hello method takes four parameters:</span></span>

  1. <span data-ttu-id="06d6a-220">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-220">**linkedServices**.</span></span> <span data-ttu-id="06d6a-221">Een inventariseerbare lijst met gekoppelde services die een koppeling i/o-gegevensbronnen (bijvoorbeeld: Azure Blob Storage) toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="06d6a-221">An enumerable list of linked services that link input/output data sources (for example: Azure Blob Storage) toohello data factory.</span></span> <span data-ttu-id="06d6a-222">In dit voorbeeld is er slechts één van de gekoppelde service van het type Azure Storage gebruikt voor invoer en uitvoer.</span><span class="sxs-lookup"><span data-stu-id="06d6a-222">In this sample, there is only one linked service of type Azure Storage used for both input and output.</span></span>
  2. <span data-ttu-id="06d6a-223">**gegevenssets**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-223">**datasets**.</span></span> <span data-ttu-id="06d6a-224">Dit is een inventariseerbare lijst van gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="06d6a-224">This is an enumerable list of datasets.</span></span> <span data-ttu-id="06d6a-225">U kunt deze parameter tooget Hallo locaties en schema's die zijn gedefinieerd door de invoer- en uitvoergegevenssets gebruiken.</span><span class="sxs-lookup"><span data-stu-id="06d6a-225">You can use this parameter tooget hello locations and schemas defined by input and output datasets.</span></span>
  3. <span data-ttu-id="06d6a-226">**activiteit**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-226">**activity**.</span></span> <span data-ttu-id="06d6a-227">Deze parameter vertegenwoordigt Hallo huidige compute entiteit - in dit geval wordt een Azure Batch-service.</span><span class="sxs-lookup"><span data-stu-id="06d6a-227">This parameter represents hello current compute entity - in this case, an Azure Batch service.</span></span>
  4. <span data-ttu-id="06d6a-228">**Berichtenlogboek**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-228">**logger**.</span></span> <span data-ttu-id="06d6a-229">Hallo Berichtenlogboek kunt die u foutopsporing opmerkingen die surface Hallo schrijft 'Gebruiker' melden Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="06d6a-229">hello logger lets you write debug comments that surface as hello “User” log for hello pipeline.</span></span>
* <span data-ttu-id="06d6a-230">Hallo-methode retourneert een woordenlijst die gebruikt toochain aangepaste activiteiten samen in de toekomst Hallo worden kan.</span><span class="sxs-lookup"><span data-stu-id="06d6a-230">hello method returns a dictionary that can be used toochain custom activities together in hello future.</span></span> <span data-ttu-id="06d6a-231">Deze functie is nog niet geïmplementeerd, kunt u dus een woordenboek leeg retourneren van Hallo-methode.</span><span class="sxs-lookup"><span data-stu-id="06d6a-231">This feature is not implemented yet, so return an empty dictionary from hello method.</span></span>

#### <a name="procedure-create-hello-custom-activity"></a><span data-ttu-id="06d6a-232">Procedure: Hallo aangepaste activiteit maken</span><span class="sxs-lookup"><span data-stu-id="06d6a-232">Procedure: Create hello custom activity</span></span>
1. <span data-ttu-id="06d6a-233">Maak een .NET Class Library-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="06d6a-233">Create a .NET Class Library project in Visual Studio.</span></span>

   1. <span data-ttu-id="06d6a-234">Start **Visual Studio 2012**/**2013-2015**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-234">Launch **Visual Studio 2012**/**2013/2015**.</span></span>
   2. <span data-ttu-id="06d6a-235">Klik op **bestand**, wijst u te**nieuw**, en klik op **Project**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-235">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="06d6a-236">Vouw **sjablonen**, en selecteer **Visual C\#**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-236">Expand **Templates**, and select **Visual C\#**.</span></span> <span data-ttu-id="06d6a-237">In dit scenario gebruikt u C\#, maar u kunt .NET taal toodevelop Hallo aangepaste activiteit.</span><span class="sxs-lookup"><span data-stu-id="06d6a-237">In this walkthrough, you use C\#, but you can use any .NET language toodevelop hello custom activity.</span></span>
   4. <span data-ttu-id="06d6a-238">Selecteer **Class Library** uit de lijst Hallo van projecttypen op Hallo rechts.</span><span class="sxs-lookup"><span data-stu-id="06d6a-238">Select **Class Library** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="06d6a-239">Voer **MyDotNetActivity** voor Hallo **naam**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-239">Enter **MyDotNetActivity** for hello **Name**.</span></span>
   6. <span data-ttu-id="06d6a-240">Selecteer **C:\\ADF** voor Hallo **locatie**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-240">Select **C:\\ADF** for hello **Location**.</span></span> <span data-ttu-id="06d6a-241">Maak de map Hallo **ADF** als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="06d6a-241">Create hello folder **ADF** if it does not exist.</span></span>
   7. <span data-ttu-id="06d6a-242">Klik op **OK** toocreate Hallo project.</span><span class="sxs-lookup"><span data-stu-id="06d6a-242">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="06d6a-243">Klik op **extra**, wijst u te**NuGet Package Manager**, en klik op **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-243">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="06d6a-244">In Hallo **Package Manager Console**, uitvoeren na de opdracht tooimport hello **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-244">In hello **Package Manager Console**, execute hello following command tooimport **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="06d6a-245">Importeren Hallo **Azure Storage** NuGet-pakket in toohello-project.</span><span class="sxs-lookup"><span data-stu-id="06d6a-245">Import hello **Azure Storage** NuGet package in toohello project.</span></span> <span data-ttu-id="06d6a-246">Omdat u Hallo Blob storage-API in dit voorbeeld gebruiken moet u dit pakket.</span><span class="sxs-lookup"><span data-stu-id="06d6a-246">You need this package because you use hello Blob storage API in this sample.</span></span>

    ```powershell
    Install-Package Azure.Storage
    ```
5. <span data-ttu-id="06d6a-247">Voeg de volgende Hallo **met** richtlijnen toohello bronbestand in Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="06d6a-247">Add hello following **using** directives toohello source file in hello project.</span></span>

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="06d6a-248">Hallo naam wijzigen van Hallo **naamruimte** te**MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-248">Change hello name of hello **namespace** too**MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="06d6a-249">Hallo-naam van de klasse Hallo te wijzigen**MyDotNetActivity** en afgeleid Hallo **IDotNetActivity** interface zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="06d6a-249">Change hello name of hello class too**MyDotNetActivity** and derive it from hello **IDotNetActivity** interface as shown below.</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="06d6a-250">Hallo implementeren (toevoegen) **Execute** methode Hallo **IDotNetActivity** interface toohello **MyDotNetActivity** klasse en kopieer Hallo voorbeeldmethode code toohello te volgen.</span><span class="sxs-lookup"><span data-stu-id="06d6a-250">Implement (Add) hello **Execute** method of hello **IDotNetActivity** interface toohello **MyDotNetActivity** class and copy hello following sample code toohello method.</span></span> <span data-ttu-id="06d6a-251">Zie Hallo [methode Execute](#execute-method) sectie voor uitleg voor Hallo logica in deze methode gebruikt.</span><span class="sxs-lookup"><span data-stu-id="06d6a-251">See hello [Execute Method](#execute-method) section for explanation for hello logic used in this method.</span></span>

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
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
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
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
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
9. <span data-ttu-id="06d6a-252">Hallo na helperklasse methoden toohello toevoegen.</span><span class="sxs-lookup"><span data-stu-id="06d6a-252">Add hello following helper methods toohello class.</span></span> <span data-ttu-id="06d6a-253">Deze methoden worden aangeroepen door Hallo **Execute** methode.</span><span class="sxs-lookup"><span data-stu-id="06d6a-253">These methods are invoked by hello **Execute** method.</span></span> <span data-ttu-id="06d6a-254">Het belangrijkste is dat Hallo **Calculate** methode isoleert Hallo-code die elke blob doorlopen.</span><span class="sxs-lookup"><span data-stu-id="06d6a-254">Most importantly, hello **Calculate** method isolates hello code that iterates through each blob.</span></span>

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
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
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
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
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
    <span data-ttu-id="06d6a-255">Hallo **GetFolderPath** methode retourneert Hallo pad toohello map die Hallo gegevensset punten tooand hello **GetFileName** methode retourneert Hallo-naam van Hallo-blob/bestand dat verwijst naar gegevensset Hallo.</span><span class="sxs-lookup"><span data-stu-id="06d6a-255">hello **GetFolderPath** method returns hello path toohello folder that hello dataset points tooand hello **GetFileName** method returns hello name of hello blob/file that hello dataset points to.</span></span>

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    <span data-ttu-id="06d6a-256">Hallo **Calculate** methode berekent het aantal exemplaren van het sleutelwoord Hallo **Microsoft** in Hallo invoerbestanden (BLOB's in de map Hallo).</span><span class="sxs-lookup"><span data-stu-id="06d6a-256">hello **Calculate** method calculates hello number of instances of keyword **Microsoft** in hello input files (blobs in hello folder).</span></span> <span data-ttu-id="06d6a-257">Hallo zoekterm ('Microsoft') is vastgelegd in het Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="06d6a-257">hello search term (“Microsoft”) is hard-coded in hello code.</span></span>

1. <span data-ttu-id="06d6a-258">Hallo project compileren.</span><span class="sxs-lookup"><span data-stu-id="06d6a-258">Compile hello project.</span></span> <span data-ttu-id="06d6a-259">Klik op **bouwen** uit en klik op Hallo **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-259">Click **Build** from hello menu and click **Build Solution**.</span></span>
2. <span data-ttu-id="06d6a-260">Start **Windows Verkenner**, en te navigeren**bin\\debug** of **bin\\release** map afhankelijk van Hallo type build.</span><span class="sxs-lookup"><span data-stu-id="06d6a-260">Launch **Windows Explorer**, and navigate too**bin\\debug** or **bin\\release** folder depending on hello type of build.</span></span>
3. <span data-ttu-id="06d6a-261">Maak een zipbestand **MyDotNetActivity.zip** die alle Hallo binaire bestanden in Hallo bevat  **\\bin\\Debug** map.</span><span class="sxs-lookup"><span data-stu-id="06d6a-261">Create a zip file **MyDotNetActivity.zip** that contains all hello binaries in hello **\\bin\\Debug** folder.</span></span> <span data-ttu-id="06d6a-262">U kunt tooinclude hello MyDotNetActivity. **pdb** bestand zodat u aanvullende informatie zoals regelnummer in de broncode Hallo die Hallo probleem veroorzaakt ophalen wanneer er een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="06d6a-262">You may want tooinclude hello MyDotNetActivity.**pdb** file so that you get additional details such as line number in hello source code that caused hello issue when a failure occurs.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. <span data-ttu-id="06d6a-263">Uploaden **MyDotNetActivity.zip** als een blob toohello blob-container: `customactivitycontainer` in hello Azure blob storage-die Hallo **StorageLinkedService** gekoppelde service in Hallo  **ADFTutorialDataFactory** gebruikt.</span><span class="sxs-lookup"><span data-stu-id="06d6a-263">Upload **MyDotNetActivity.zip** as a blob toohello blob container: `customactivitycontainer` in hello Azure blob storage that hello **StorageLinkedService** linked service in hello **ADFTutorialDataFactory** uses.</span></span> <span data-ttu-id="06d6a-264">Maken van de blob-container Hallo `customactivitycontainer` als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="06d6a-264">Create hello blob container `customactivitycontainer` if it does not already exist.</span></span>

#### <a name="execute-method"></a><span data-ttu-id="06d6a-265">De methode Execute</span><span class="sxs-lookup"><span data-stu-id="06d6a-265">Execute method</span></span>
<span data-ttu-id="06d6a-266">Deze sectie bevat meer informatie en opmerkingen over Hallo-code in Hallo Execute-methode.</span><span class="sxs-lookup"><span data-stu-id="06d6a-266">This section provides more details and notes about hello code in hello Execute method.</span></span>

1. <span data-ttu-id="06d6a-267">Hallo-leden voor doorloopt Hallo invoerverzameling vindt u in Hallo [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) naamruimte.</span><span class="sxs-lookup"><span data-stu-id="06d6a-267">hello members for iterating through hello input collection are found in hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span></span> <span data-ttu-id="06d6a-268">Hallo blob verzameling doorloopt, moet u Hallo **BlobContinuationToken** klasse.</span><span class="sxs-lookup"><span data-stu-id="06d6a-268">Iterating through hello blob collection requires using hello **BlobContinuationToken** class.</span></span> <span data-ttu-id="06d6a-269">In wezen, moet u een do-tijdens lus met Hallo-token als Hallo-mechanisme voor het Hallo-lus wordt afgesloten.</span><span class="sxs-lookup"><span data-stu-id="06d6a-269">In essence, you must use a do-while loop with hello token as hello mechanism for exiting hello loop.</span></span> <span data-ttu-id="06d6a-270">Zie voor meer informatie [hoe toouse Blob storage uit het .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="06d6a-270">For more information, see [How toouse Blob storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="06d6a-271">Hier ziet u een eenvoudige lus:</span><span class="sxs-lookup"><span data-stu-id="06d6a-271">A basic loop is shown here:</span></span>

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   <span data-ttu-id="06d6a-272">Raadpleeg de documentatie Hallo voor Hallo [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) methode voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="06d6a-272">See hello documentation for hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method for details.</span></span>
2. <span data-ttu-id="06d6a-273">Hallo code voor binnen Hallo Hallo reeks blobs logisch doorloopt gaat doen-tijdens lus.</span><span class="sxs-lookup"><span data-stu-id="06d6a-273">hello code for working through hello set of blobs logically goes within hello do-while loop.</span></span> <span data-ttu-id="06d6a-274">In Hallo **Execute** methode, komen Hallo-terwijl lus Hallo lijst met blobs tooa methode met de naam verstuurt **Calculate**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-274">In hello **Execute** method, hello do-while loop passes hello list of blobs tooa method named **Calculate**.</span></span> <span data-ttu-id="06d6a-275">Hallo-methode retourneert een string-variabele met de naam **uitvoer** die Hallo resultaat van gelet herhaald via alle Hallo blobs in Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="06d6a-275">hello method returns a string variable named **output** that is hello result of having iterated through all hello blobs in hello segment.</span></span>

   <span data-ttu-id="06d6a-276">Deze retourneert het aantal exemplaren van de zoekterm Hallo Hallo (**Microsoft**) in de blob Hallo doorgegeven toohello **Calculate** methode.</span><span class="sxs-lookup"><span data-stu-id="06d6a-276">It returns hello number of occurrences of hello search term (**Microsoft**) in hello blob passed toohello **Calculate** method.</span></span>

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. <span data-ttu-id="06d6a-277">Eenmaal Hallo **Calculate** methode heeft Hallo werk gedaan, deze moet worden geschreven tooa nieuwe blob.</span><span class="sxs-lookup"><span data-stu-id="06d6a-277">Once hello **Calculate** method has done hello work, it must be written tooa new blob.</span></span> <span data-ttu-id="06d6a-278">Dus voor elke set van BLOB's verwerkt, kan een nieuwe blob met Hallo resultaten worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="06d6a-278">So for every set of blobs processed, a new blob can be written with hello results.</span></span> <span data-ttu-id="06d6a-279">toowrite tooa nieuwe blob, het eerste zoeken Hallo-uitvoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="06d6a-279">toowrite tooa new blob, first find hello output dataset.</span></span>

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. <span data-ttu-id="06d6a-280">Hallo code ook een Help-methode aanroept: **GetFolderPath** tooretrieve Hallo mappad (Hallo opslag containernaam).</span><span class="sxs-lookup"><span data-stu-id="06d6a-280">hello code also calls a helper method: **GetFolderPath** tooretrieve hello folder path (hello storage container name).</span></span>

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   <span data-ttu-id="06d6a-281">Hallo **GetFolderPath** webcasts Hallo gegevensset object tooan AzureBlobDataSet met een eigenschap genaamd FolderPath.</span><span class="sxs-lookup"><span data-stu-id="06d6a-281">hello **GetFolderPath** casts hello DataSet object tooan AzureBlobDataSet, which has a property named FolderPath.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. <span data-ttu-id="06d6a-282">Hallo code aanroepen Hallo **GetFileName** methode tooretrieve Hallo-bestandsnaam (blob-naam).</span><span class="sxs-lookup"><span data-stu-id="06d6a-282">hello code calls hello **GetFileName** method tooretrieve hello file name (blob name).</span></span> <span data-ttu-id="06d6a-283">Hallo-code is vergelijkbaar toohello bovenstaande code tooget Hallo mappad.</span><span class="sxs-lookup"><span data-stu-id="06d6a-283">hello code is similar toohello above code tooget hello folder path.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. <span data-ttu-id="06d6a-284">Hallo-naam van Hallo-bestand is geschreven door een URI-object te maken.</span><span class="sxs-lookup"><span data-stu-id="06d6a-284">hello name of hello file is written by creating a URI object.</span></span> <span data-ttu-id="06d6a-285">Hallo URI constructor gebruikt Hallo **BlobEndpoint** tooreturn Hallo container eigenschapsnaam.</span><span class="sxs-lookup"><span data-stu-id="06d6a-285">hello URI constructor uses hello **BlobEndpoint** property tooreturn hello container name.</span></span> <span data-ttu-id="06d6a-286">Hallo map pad en de naam toegevoegd tooconstruct Hallo uitvoer blob-URI.</span><span class="sxs-lookup"><span data-stu-id="06d6a-286">hello folder path and file name are added tooconstruct hello output blob URI.</span></span>  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. <span data-ttu-id="06d6a-287">Hallo-naam van Hallo-bestand is geschreven en nu kunt u Hallo uitvoertekenreeks schrijven van Hallo **Calculate** methode tooa nieuwe blob:</span><span class="sxs-lookup"><span data-stu-id="06d6a-287">hello name of hello file has been written and now you can write hello output string from hello **Calculate** method tooa new blob:</span></span>

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a><span data-ttu-id="06d6a-288">Hallo een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="06d6a-288">Create hello data factory</span></span>
<span data-ttu-id="06d6a-289">In Hallo [maken van aangepaste activiteit Hallo](#create-the-custom-activity) sectie maakt u een aangepaste activiteit hebt gemaakt en geüploade Hallo zip-bestand met de binaire bestanden en Hallo PDB-bestand tooan Azure blob-container.</span><span class="sxs-lookup"><span data-stu-id="06d6a-289">In hello [Create hello custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded hello zip file with binaries and hello PDB file tooan Azure blob container.</span></span> <span data-ttu-id="06d6a-290">In deze sectie maakt u een Azure **gegevensfactory** met een **pijplijn** die gebruikmaakt van Hallo **aangepaste activiteit**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-290">In this section, you create an Azure **data factory** with a **pipeline** that uses hello **custom activity**.</span></span>

<span data-ttu-id="06d6a-291">Hallo invoergegevensset voor Hallo aangepaste activiteit Hallo-blobs (bestanden) in de invoermap hello vertegenwoordigt (`mycontainer\\inputfolder`) in de blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="06d6a-291">hello input dataset for hello custom activity represents hello blobs (files) in hello input folder (`mycontainer\\inputfolder`) in blob storage.</span></span> <span data-ttu-id="06d6a-292">Hallo uitvoergegevensset voor Hallo activiteit Hallo uitvoer blobs in de uitvoermap hello vertegenwoordigt (`mycontainer\\outputfolder`) in de blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="06d6a-292">hello output dataset for hello activity represents hello output blobs in hello output folder (`mycontainer\\outputfolder`) in blob storage.</span></span>

<span data-ttu-id="06d6a-293">Een of meer bestanden neerzetten in Hallo invoer mappen:</span><span class="sxs-lookup"><span data-stu-id="06d6a-293">Drop one or more files in hello input folders:</span></span>

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

<span data-ttu-id="06d6a-294">Bijvoorbeeld: één bestand (bestand.txt) verwijderen met de volgende inhoud in elk van de mappen Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="06d6a-294">For example, drop one file (file.txt) with hello following content into each of hello folders.</span></span>

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="06d6a-295">Elke invoermap komt overeen tooa segment in Azure Data Factory, zelfs als Hallo map 2 of meer bestanden bevat.</span><span class="sxs-lookup"><span data-stu-id="06d6a-295">Each input folder corresponds tooa slice in Azure Data Factory even if hello folder has 2 or more files.</span></span> <span data-ttu-id="06d6a-296">Wanneer elk segment wordt verwerkt door de pijplijn hello, doorlopen aangepaste activiteit Hallo alle Hallo blobs in de invoermap Hallo voor dat segment.</span><span class="sxs-lookup"><span data-stu-id="06d6a-296">When each slice is processed by hello pipeline, hello custom activity iterates through all hello blobs in hello input folder for that slice.</span></span>

<span data-ttu-id="06d6a-297">Ziet u vijf uitvoerbestanden Hello dezelfde inhoud.</span><span class="sxs-lookup"><span data-stu-id="06d6a-297">You see five output files with hello same content.</span></span> <span data-ttu-id="06d6a-298">Hallo-uitvoerbestand van het verwerken van bestand in map Hallo 2015-11-16-00 Hallo heeft bijvoorbeeld Hallo volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="06d6a-298">For example, hello output file from processing hello file in hello 2015-11-16-00 folder has hello following content:</span></span>

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

<span data-ttu-id="06d6a-299">Als u meerdere bestanden (bestand.txt, bestand2.txt samengevoegd, file3.txt) verwijderen Hello dezelfde toohello invoermap inhoud, ziet u de volgende inhoud in het uitvoerbestand Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="06d6a-299">If you drop multiple files (file.txt, file2.txt, file3.txt) with hello same content toohello input folder, you see hello following content in hello output file.</span></span> <span data-ttu-id="06d6a-300">Elke map (2015-11-16-00, enz.) tooa segment in dit voorbeeld komt overeen, hoewel Hallo map meerdere invoerbestanden heeft.</span><span class="sxs-lookup"><span data-stu-id="06d6a-300">Each folder (2015-11-16-00, etc.) corresponds tooa slice in this sample even though hello folder has multiple input files.</span></span>

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

<span data-ttu-id="06d6a-301">Hallo-bestand voor uitvoer heeft drie regels nu één voor elk bestand voor invoer (blob) in Hallo map die is gekoppeld aan het Hallo-segment (2015-11-16-00).</span><span class="sxs-lookup"><span data-stu-id="06d6a-301">hello output file has three lines now, one for each input file (blob) in hello folder associated with hello slice (2015-11-16-00).</span></span>

<span data-ttu-id="06d6a-302">Een taak is gemaakt voor elke activiteit die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="06d6a-302">A task is created for each activity run.</span></span> <span data-ttu-id="06d6a-303">In dit voorbeeld moet u er slechts één activiteit is in Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="06d6a-303">In this sample, there is only one activity in hello pipeline.</span></span> <span data-ttu-id="06d6a-304">Wanneer een segment wordt verwerkt door de pijplijn hello, is Hallo aangepaste activiteit wordt uitgevoerd op Azure Batch tooprocess Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="06d6a-304">When a slice is processed by hello pipeline, hello custom activity runs on Azure Batch tooprocess hello slice.</span></span> <span data-ttu-id="06d6a-305">Aangezien er zijn vijf segmenten (elk segment kan hebben meerdere blobs of -bestand), moet u er vijf taken die zijn gemaakt in Azure Batch zijn.</span><span class="sxs-lookup"><span data-stu-id="06d6a-305">Since there are five slices (each slice can have multiple blobs or file), there are five tasks created in Azure Batch.</span></span> <span data-ttu-id="06d6a-306">Wanneer een taak wordt uitgevoerd op de Batch, is het daadwerkelijk Hallo aangepaste activiteit die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="06d6a-306">When a task runs on Batch, it is actually hello custom activity that is running.</span></span>

<span data-ttu-id="06d6a-307">Hallo volgen Stapsgewijze instructies vindt u meer informatie.</span><span class="sxs-lookup"><span data-stu-id="06d6a-307">hello following walkthrough provides additional details.</span></span>

#### <a name="step-1-create-hello-data-factory"></a><span data-ttu-id="06d6a-308">Stap 1: Hallo een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="06d6a-308">Step 1: Create hello data factory</span></span>
1. <span data-ttu-id="06d6a-309">Na het aanmelden toohello [Azure-portal](https://portal.azure.com/), Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="06d6a-309">After logging in toohello [Azure portal](https://portal.azure.com/), do hello following steps:</span></span>

   1. <span data-ttu-id="06d6a-310">Klik op **nieuw** op Hallo linkermenu.</span><span class="sxs-lookup"><span data-stu-id="06d6a-310">Click **NEW** on hello left menu.</span></span>
   2. <span data-ttu-id="06d6a-311">Klik op **gegevens en analyse** in Hallo **nieuw** blade.</span><span class="sxs-lookup"><span data-stu-id="06d6a-311">Click **Data + Analytics** in hello **New** blade.</span></span>
   3. <span data-ttu-id="06d6a-312">Klik op **Data Factory** op Hallo **gegevensanalyse** blade.</span><span class="sxs-lookup"><span data-stu-id="06d6a-312">Click **Data Factory** on hello **Data analytics** blade.</span></span>
2. <span data-ttu-id="06d6a-313">In Hallo **nieuwe gegevensfactory** blade Voer **CustomActivityFactory** voor Hallo naam.</span><span class="sxs-lookup"><span data-stu-id="06d6a-313">In hello **New data factory** blade, enter **CustomActivityFactory** for hello Name.</span></span> <span data-ttu-id="06d6a-314">Hallo-naam van hello Azure-gegevensfactory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="06d6a-314">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="06d6a-315">Als u de foutmelding Hallo: **Data factory-naam 'CustomActivityFactory' is niet beschikbaar**, Hallo-naam van gegevensfactory Hallo wijzigen (bijvoorbeeld **yournameCustomActivityFactory**) en probeert te maken opnieuw.</span><span class="sxs-lookup"><span data-stu-id="06d6a-315">If you receive hello error: **Data factory name “CustomActivityFactory” is not available**, change hello name of hello data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>
3. <span data-ttu-id="06d6a-316">Klik op **RESOURCEGROEPNAAM**, en selecteer een bestaande resourcegroep of maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="06d6a-316">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="06d6a-317">Controleer of dat u gebruikmaakt van het juiste abonnement Hallo en regio waar u Hallo data factory toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="06d6a-317">Verify that you are using hello correct subscription and region where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="06d6a-318">Klik op **maken** op Hallo **nieuwe gegevensfactory** blade.</span><span class="sxs-lookup"><span data-stu-id="06d6a-318">Click **Create** on hello **New data factory** blade.</span></span>
6. <span data-ttu-id="06d6a-319">Zie van Hallo gegevensfactory wordt gemaakt in Hallo **Dashboard** Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="06d6a-319">You see hello data factory being created in hello **Dashboard** of hello Azure portal.</span></span>
7. <span data-ttu-id="06d6a-320">Nadat het Hallo-gegevensfactory is gemaakt, ziet u Hallo data factory-pagina waarop u inhoud van de gegevensfactory Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="06d6a-320">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a><span data-ttu-id="06d6a-321">Stap 2: Gekoppelde services maken</span><span class="sxs-lookup"><span data-stu-id="06d6a-321">Step 2: Create linked services</span></span>
<span data-ttu-id="06d6a-322">Gekoppelde services worden gegevensarchieven of compute-services tooan Azure-gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="06d6a-322">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="06d6a-323">In deze stap koppelt u uw **Azure Storage** account en **Azure Batch** account tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="06d6a-323">In this step, you link your **Azure Storage** account and **Azure Batch** account tooyour data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="06d6a-324">Een gekoppelde Azure Storage-service maken</span><span class="sxs-lookup"><span data-stu-id="06d6a-324">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="06d6a-325">Klik op Hallo **auteur en implementeren van** tegel op Hallo **DATA FACTORY** blade voor **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-325">Click hello **Author and deploy** tile on hello **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="06d6a-326">U ziet Hallo Data Factory-Editor.</span><span class="sxs-lookup"><span data-stu-id="06d6a-326">You see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="06d6a-327">Klik op **nieuwe gegevensopslag** op Hallo opdrachtbalk en kies **Azure-opslag.**</span><span class="sxs-lookup"><span data-stu-id="06d6a-327">Click **New data store** on hello command bar and choose **Azure storage.**</span></span> <span data-ttu-id="06d6a-328">U ziet Hallo JSON-script voor het maken van een Azure Storage gekoppelde service in Hallo-editor.</span><span class="sxs-lookup"><span data-stu-id="06d6a-328">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. <span data-ttu-id="06d6a-329">Vervang **accountnaam** met Hallo-naam van uw Azure storage-account en **accountsleutel** door de toegangssleutel Hallo van hello Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="06d6a-329">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="06d6a-330">toolearn hoe tooget uw opslag toegang krijgen tot sleutel, Zie [toegangssleutels voor opslag weergeven, kopiëren en opnieuw genereren](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="06d6a-330">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

4. <span data-ttu-id="06d6a-331">Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="06d6a-331">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="06d6a-332">Azure Batch gekoppelde service maken</span><span class="sxs-lookup"><span data-stu-id="06d6a-332">Create Azure Batch linked service</span></span>
<span data-ttu-id="06d6a-333">In deze stap maakt u een gekoppelde service maken voor uw **Azure Batch** account die is gebruikt toorun Hallo Data Factory aangepaste activiteit.</span><span class="sxs-lookup"><span data-stu-id="06d6a-333">In this step, you create a linked service for your **Azure Batch** account that is used toorun hello Data Factory custom activity.</span></span>

1. <span data-ttu-id="06d6a-334">Klik op **nieuwe berekening** op Hallo opdrachtbalk en kies **Azure Batch.**</span><span class="sxs-lookup"><span data-stu-id="06d6a-334">Click **New compute** on hello command bar and choose **Azure Batch.**</span></span> <span data-ttu-id="06d6a-335">U ziet Hallo JSON-script voor het maken van een Azure-Batch gekoppelde service in Hallo-editor.</span><span class="sxs-lookup"><span data-stu-id="06d6a-335">You should see hello JSON script for creating an Azure Batch linked service in hello editor.</span></span>
2. <span data-ttu-id="06d6a-336">In Hallo JSON-script:</span><span class="sxs-lookup"><span data-stu-id="06d6a-336">In hello JSON script:</span></span>

   1. <span data-ttu-id="06d6a-337">Vervang **accountnaam** met Hallo-naam van uw Azure Batch-account.</span><span class="sxs-lookup"><span data-stu-id="06d6a-337">Replace **account name** with hello name of your Azure Batch account.</span></span>
   2. <span data-ttu-id="06d6a-338">Vervang **toegangssleutel** door de toegangssleutel Hallo van hello Azure Batch-account.</span><span class="sxs-lookup"><span data-stu-id="06d6a-338">Replace **access key** with hello access key of hello Azure Batch account.</span></span>
   3. <span data-ttu-id="06d6a-339">Voer Hallo-ID van Hallo pool voor Hallo **poolName** eigenschap**.**</span><span class="sxs-lookup"><span data-stu-id="06d6a-339">Enter hello ID of hello pool for hello **poolName** property**.**</span></span> <span data-ttu-id="06d6a-340">Voor deze eigenschap kunt u de naam van de toepassingen opgeven of id-groep</span><span class="sxs-lookup"><span data-stu-id="06d6a-340">For this property, you can specify either pool name or pool ID.</span></span>
   4. <span data-ttu-id="06d6a-341">Voer Hallo batch URI voor Hallo **batchUri** JSON-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="06d6a-341">Enter hello batch URI for hello **batchUri** JSON property.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="06d6a-342">Hallo **URL** van Hallo **blade van Azure Batch-account** bevindt zich in de volgende indeling Hallo: \<accountname\>.\< regio\>. batch.azure.com. Voor Hallo **batchUri** eigenschap in JSON hello, moet u te**verwijderen "accountname."**</span><span class="sxs-lookup"><span data-stu-id="06d6a-342">hello **URL** from hello **Azure Batch account blade** is in hello following format: \<accountname\>.\<region\>.batch.azure.com. For hello **batchUri** property in hello JSON, you need too**remove "accountname."**</span></span> <span data-ttu-id="06d6a-343">van Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="06d6a-343">from hello URL.</span></span> <span data-ttu-id="06d6a-344">Voorbeeld: `"batchUri": "https://eastus.batch.azure.com"`.</span><span class="sxs-lookup"><span data-stu-id="06d6a-344">Example: `"batchUri": "https://eastus.batch.azure.com"`.</span></span>
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      <span data-ttu-id="06d6a-345">Voor Hallo **poolName** eigenschap, kunt u ook Hallo-ID van Hallo pool in plaats van Hallo-naam van Hallo van toepassingen opgeven.</span><span class="sxs-lookup"><span data-stu-id="06d6a-345">For hello **poolName** property, you can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>

      > [!NOTE]
      > <span data-ttu-id="06d6a-346">Hallo Data Factory-service biedt een optie op aanvraag geen ondersteuning voor Azure Batch als voor HDInsight.</span><span class="sxs-lookup"><span data-stu-id="06d6a-346">hello Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="06d6a-347">U kunt uw eigen Azure Batch-pool alleen gebruiken in een Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="06d6a-347">You can only use your own Azure Batch pool in an Azure data factory.</span></span>
      >
      >
   5. <span data-ttu-id="06d6a-348">Geef **StorageLinkedService** voor Hallo **linkedServiceName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="06d6a-348">Specify **StorageLinkedService** for hello **linkedServiceName** property.</span></span> <span data-ttu-id="06d6a-349">U kunt deze gekoppelde service gemaakt in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="06d6a-349">You created this linked service in hello previous step.</span></span> <span data-ttu-id="06d6a-350">Deze opslag wordt gebruikt als een faseringsgebied voor bestanden en de logboeken.</span><span class="sxs-lookup"><span data-stu-id="06d6a-350">This storage is used as a staging area for files and logs.</span></span>
3. <span data-ttu-id="06d6a-351">Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="06d6a-351">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

#### <a name="step-3-create-datasets"></a><span data-ttu-id="06d6a-352">Stap 3: Gegevenssets maken</span><span class="sxs-lookup"><span data-stu-id="06d6a-352">Step 3: Create datasets</span></span>
<span data-ttu-id="06d6a-353">In deze stap maakt u gegevenssets toorepresent invoer maken en uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="06d6a-353">In this step, you create datasets toorepresent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="06d6a-354">Invoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="06d6a-354">Create input dataset</span></span>
1. <span data-ttu-id="06d6a-355">In Hallo **Editor** Hallo Data Factory, klikt u op **nieuwe gegevensset** op Hallo werkbalk en klikt u op **Azure Blob storage** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="06d6a-355">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="06d6a-356">Hallo JSON in het rechterdeelvenster Hallo vervangen door Hallo volgende JSON-fragment:</span><span class="sxs-lookup"><span data-stu-id="06d6a-356">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
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

    <span data-ttu-id="06d6a-357">U maakt een pijplijn verderop in dit scenario met begintijd: 2015-11-16T00:00:00Z-en eindtijd: 2015-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="06d6a-357">You create a pipeline later in this walkthrough with start time: 2015-11-16T00:00:00Z and end time: 2015-11-16T05:00:00Z.</span></span> <span data-ttu-id="06d6a-358">Geplande tooproduce gegevens is **per uur**, zodat er 5 segmenten van de invoer/uitvoer (tussen **00**: 00:00 -\> **05**: 00:00).</span><span class="sxs-lookup"><span data-stu-id="06d6a-358">It is scheduled tooproduce data **hourly**, so there are 5 input/output slices (between **00**:00:00 -\> **05**:00:00).</span></span>

    <span data-ttu-id="06d6a-359">Hallo **frequentie** en **interval** voor invoergegevensset hello te is ingesteld**uur** en **1**, wat betekent dat Hallo invoer segment is beschikbaar elk uur.</span><span class="sxs-lookup"><span data-stu-id="06d6a-359">hello **frequency** and **interval** for hello input dataset is set too**Hour** and **1**, which means that hello input slice is available hourly.</span></span>

    <span data-ttu-id="06d6a-360">Hier volgen Hallo begintijden voor elk segment, die wordt vertegenwoordigd door **SliceStart** systeemvariabele in Hallo hierboven JSON-codefragment.</span><span class="sxs-lookup"><span data-stu-id="06d6a-360">Here are hello start times for each slice, which is represented by **SliceStart** system variable in hello above JSON snippet.</span></span>

    | <span data-ttu-id="06d6a-361">**Segment**</span><span class="sxs-lookup"><span data-stu-id="06d6a-361">**Slice**</span></span> | <span data-ttu-id="06d6a-362">**Begintijd**</span><span class="sxs-lookup"><span data-stu-id="06d6a-362">**Start time**</span></span>          |
    |-----------|-------------------------|
    | <span data-ttu-id="06d6a-363">1</span><span class="sxs-lookup"><span data-stu-id="06d6a-363">1</span></span>         | <span data-ttu-id="06d6a-364">2015-11-16T**00**: 00:00</span><span class="sxs-lookup"><span data-stu-id="06d6a-364">2015-11-16T**00**:00:00</span></span> |
    | <span data-ttu-id="06d6a-365">2</span><span class="sxs-lookup"><span data-stu-id="06d6a-365">2</span></span>         | <span data-ttu-id="06d6a-366">2015-11-16T**01**: 00:00</span><span class="sxs-lookup"><span data-stu-id="06d6a-366">2015-11-16T**01**:00:00</span></span> |
    | <span data-ttu-id="06d6a-367">3</span><span class="sxs-lookup"><span data-stu-id="06d6a-367">3</span></span>         | <span data-ttu-id="06d6a-368">2015-11-16T**02**: 00:00</span><span class="sxs-lookup"><span data-stu-id="06d6a-368">2015-11-16T**02**:00:00</span></span> |
    | <span data-ttu-id="06d6a-369">4</span><span class="sxs-lookup"><span data-stu-id="06d6a-369">4</span></span>         | <span data-ttu-id="06d6a-370">2015-11-16T**03**: 00:00</span><span class="sxs-lookup"><span data-stu-id="06d6a-370">2015-11-16T**03**:00:00</span></span> |
    | <span data-ttu-id="06d6a-371">5</span><span class="sxs-lookup"><span data-stu-id="06d6a-371">5</span></span>         | <span data-ttu-id="06d6a-372">2015-11-16T**04**: 00:00</span><span class="sxs-lookup"><span data-stu-id="06d6a-372">2015-11-16T**04**:00:00</span></span> |

    <span data-ttu-id="06d6a-373">Hallo **folderPath** wordt berekend met behulp van Hallo jaar, maand, dag en uur onderdeel van de begintijd Hallo-segment (**SliceStart**).</span><span class="sxs-lookup"><span data-stu-id="06d6a-373">hello **folderPath** is calculated by using hello year, month, day, and hour part of hello slice start time (**SliceStart**).</span></span> <span data-ttu-id="06d6a-374">Hier is daarom hoe een invoermap toegewezen tooa segment is.</span><span class="sxs-lookup"><span data-stu-id="06d6a-374">Therefore, here is how an input folder is mapped tooa slice.</span></span>

    | <span data-ttu-id="06d6a-375">**Segment**</span><span class="sxs-lookup"><span data-stu-id="06d6a-375">**Slice**</span></span> | <span data-ttu-id="06d6a-376">**Begintijd**</span><span class="sxs-lookup"><span data-stu-id="06d6a-376">**Start time**</span></span>          | <span data-ttu-id="06d6a-377">**Invoermap**</span><span class="sxs-lookup"><span data-stu-id="06d6a-377">**Input folder**</span></span>  |
    |-----------|-------------------------|-------------------|
    | <span data-ttu-id="06d6a-378">1</span><span class="sxs-lookup"><span data-stu-id="06d6a-378">1</span></span>         | <span data-ttu-id="06d6a-379">2015-11-16T**00**: 00:00</span><span class="sxs-lookup"><span data-stu-id="06d6a-379">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="06d6a-380">2015-11-16-**00**</span><span class="sxs-lookup"><span data-stu-id="06d6a-380">2015-11-16-**00**</span></span> |
    | <span data-ttu-id="06d6a-381">2</span><span class="sxs-lookup"><span data-stu-id="06d6a-381">2</span></span>         | <span data-ttu-id="06d6a-382">2015-11-16T**01**: 00:00</span><span class="sxs-lookup"><span data-stu-id="06d6a-382">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="06d6a-383">2015-11-16-**01**</span><span class="sxs-lookup"><span data-stu-id="06d6a-383">2015-11-16-**01**</span></span> |
    | <span data-ttu-id="06d6a-384">3</span><span class="sxs-lookup"><span data-stu-id="06d6a-384">3</span></span>         | <span data-ttu-id="06d6a-385">2015-11-16T**02**: 00:00</span><span class="sxs-lookup"><span data-stu-id="06d6a-385">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="06d6a-386">2015-11-16-**02**</span><span class="sxs-lookup"><span data-stu-id="06d6a-386">2015-11-16-**02**</span></span> |
    | <span data-ttu-id="06d6a-387">4</span><span class="sxs-lookup"><span data-stu-id="06d6a-387">4</span></span>         | <span data-ttu-id="06d6a-388">2015-11-16T**03**: 00:00</span><span class="sxs-lookup"><span data-stu-id="06d6a-388">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="06d6a-389">2015-11-16-**03**</span><span class="sxs-lookup"><span data-stu-id="06d6a-389">2015-11-16-**03**</span></span> |
    | <span data-ttu-id="06d6a-390">5</span><span class="sxs-lookup"><span data-stu-id="06d6a-390">5</span></span>         | <span data-ttu-id="06d6a-391">2015-11-16T**04**: 00:00</span><span class="sxs-lookup"><span data-stu-id="06d6a-391">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="06d6a-392">2015-11-16-**04**</span><span class="sxs-lookup"><span data-stu-id="06d6a-392">2015-11-16-**04**</span></span> |

1. <span data-ttu-id="06d6a-393">Klik op **implementeren** op Hallo werkbalk toocreate en implementeren van Hallo **InputDataset** tabel.</span><span class="sxs-lookup"><span data-stu-id="06d6a-393">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset** table.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="06d6a-394">Uitvoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="06d6a-394">Create output dataset</span></span>
<span data-ttu-id="06d6a-395">In deze stap maakt u een andere dataset van het type AzureBlob toorepresent Hallo uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="06d6a-395">In this step, you create another dataset of type AzureBlob toorepresent hello output data.</span></span>

1. <span data-ttu-id="06d6a-396">In Hallo **Editor** Hallo Data Factory, klikt u op **nieuwe gegevensset** op Hallo werkbalk en klikt u op **Azure Blob storage** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="06d6a-396">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="06d6a-397">Hallo JSON in het rechterdeelvenster Hallo vervangen door Hallo volgende JSON-fragment:</span><span class="sxs-lookup"><span data-stu-id="06d6a-397">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
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

    <span data-ttu-id="06d6a-398">Een uitvoer-blob/bestand wordt gegenereerd voor elk segment invoer.</span><span class="sxs-lookup"><span data-stu-id="06d6a-398">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="06d6a-399">Hier ziet u hoe een bestand voor uitvoer met de naam van elk segment.</span><span class="sxs-lookup"><span data-stu-id="06d6a-399">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="06d6a-400">Alle Hallo uitvoerbestanden worden gegenereerd in een uitvoermap: `mycontainer\\outputfolder`.</span><span class="sxs-lookup"><span data-stu-id="06d6a-400">All hello output files are generated in one output folder: `mycontainer\\outputfolder`.</span></span>

    | <span data-ttu-id="06d6a-401">**Segment**</span><span class="sxs-lookup"><span data-stu-id="06d6a-401">**Slice**</span></span> | <span data-ttu-id="06d6a-402">**Begintijd**</span><span class="sxs-lookup"><span data-stu-id="06d6a-402">**Start time**</span></span>          | <span data-ttu-id="06d6a-403">**Bestand voor uitvoer**</span><span class="sxs-lookup"><span data-stu-id="06d6a-403">**Output file**</span></span>       |
    |-----------|-------------------------|-----------------------|
    | <span data-ttu-id="06d6a-404">1</span><span class="sxs-lookup"><span data-stu-id="06d6a-404">1</span></span>         | <span data-ttu-id="06d6a-405">2015-11-16T**00**: 00:00</span><span class="sxs-lookup"><span data-stu-id="06d6a-405">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="06d6a-406">2015-11-16 -**00. txt**</span><span class="sxs-lookup"><span data-stu-id="06d6a-406">2015-11-16-**00.txt**</span></span> |
    | <span data-ttu-id="06d6a-407">2</span><span class="sxs-lookup"><span data-stu-id="06d6a-407">2</span></span>         | <span data-ttu-id="06d6a-408">2015-11-16T**01**: 00:00</span><span class="sxs-lookup"><span data-stu-id="06d6a-408">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="06d6a-409">2015-11-16 -**01. txt**</span><span class="sxs-lookup"><span data-stu-id="06d6a-409">2015-11-16-**01.txt**</span></span> |
    | <span data-ttu-id="06d6a-410">3</span><span class="sxs-lookup"><span data-stu-id="06d6a-410">3</span></span>         | <span data-ttu-id="06d6a-411">2015-11-16T**02**: 00:00</span><span class="sxs-lookup"><span data-stu-id="06d6a-411">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="06d6a-412">2015-11-16 -**02. txt**</span><span class="sxs-lookup"><span data-stu-id="06d6a-412">2015-11-16-**02.txt**</span></span> |
    | <span data-ttu-id="06d6a-413">4</span><span class="sxs-lookup"><span data-stu-id="06d6a-413">4</span></span>         | <span data-ttu-id="06d6a-414">2015-11-16T**03**: 00:00</span><span class="sxs-lookup"><span data-stu-id="06d6a-414">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="06d6a-415">2015-11-16 -**03. txt**</span><span class="sxs-lookup"><span data-stu-id="06d6a-415">2015-11-16-**03.txt**</span></span> |
    | <span data-ttu-id="06d6a-416">5</span><span class="sxs-lookup"><span data-stu-id="06d6a-416">5</span></span>         | <span data-ttu-id="06d6a-417">2015-11-16T**04**: 00:00</span><span class="sxs-lookup"><span data-stu-id="06d6a-417">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="06d6a-418">2015-11-16 -**04. txt**</span><span class="sxs-lookup"><span data-stu-id="06d6a-418">2015-11-16-**04.txt**</span></span> |

    <span data-ttu-id="06d6a-419">Houd er rekening mee dat alle bestanden in een invoermap Hallo (bijvoorbeeld: 2015-11-16-00) deel uitmaken van een segment met Hallo begintijd: 2015-11-16-00.</span><span class="sxs-lookup"><span data-stu-id="06d6a-419">Remember that all hello files in an input folder (for example: 2015-11-16-00) are part of a slice with hello start time: 2015-11-16-00.</span></span> <span data-ttu-id="06d6a-420">Als dit segment is verwerkt, wordt Hallo aangepaste activiteit gescand door elk bestand en resulteert in een regel in het uitvoerbestand Hallo met Hallo aantal exemplaren van zoekterm ('Microsoft').</span><span class="sxs-lookup"><span data-stu-id="06d6a-420">When this slice is processed, hello custom activity scans through each file and produces a line in hello output file with hello number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="06d6a-421">Als er drie bestanden in de map Hallo 2015-11-16-00, er zijn drie regels in het uitvoerbestand Hallo: 2015-11-16-00.txt.</span><span class="sxs-lookup"><span data-stu-id="06d6a-421">If there are three files in hello folder 2015-11-16-00, there are three lines in hello output file: 2015-11-16-00.txt.</span></span>

1. <span data-ttu-id="06d6a-422">Klik op **implementeren** op Hallo werkbalk toocreate en implementeren van Hallo **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-422">Click **Deploy** on hello toolbar toocreate and deploy hello **OutputDataset**.</span></span>

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a><span data-ttu-id="06d6a-423">Stap 4: Maken en uitvoeren van Hallo pijplijn met een aangepaste activiteit</span><span class="sxs-lookup"><span data-stu-id="06d6a-423">Step 4: Create and run hello pipeline with custom activity</span></span>
<span data-ttu-id="06d6a-424">In deze stap maakt maken u een pijplijn met één activiteit, Hallo aangepaste activiteit die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="06d6a-424">In this step, you create a pipeline with one activity, hello custom activity you created earlier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06d6a-425">Als u dit nog niet hebt geüpload Hallo **bestand.txt** tooinput mappen in de blob-container hello, dit doen voordat u Hallo pijplijn maakt.</span><span class="sxs-lookup"><span data-stu-id="06d6a-425">If you haven't uploaded hello **file.txt** tooinput folders in hello blob container, do so before creating hello pipeline.</span></span> <span data-ttu-id="06d6a-426">Hallo **isPaused** eigenschap toofalse in Hallo pijplijn JSON, is ingesteld zodat Hallo pijplijn wordt onmiddellijk uitgevoerd als Hallo **start** Hallo afgelopen datum is.</span><span class="sxs-lookup"><span data-stu-id="06d6a-426">hello **isPaused** property is set toofalse in hello pipeline JSON, so hello pipeline runs immediately as hello **start** date is in hello past.</span></span>
>
>

1. <span data-ttu-id="06d6a-427">In Hallo Data Factory-Editor, klikt u op **nieuwe pijplijn** op Hallo opdrachtbalk klikken.</span><span class="sxs-lookup"><span data-stu-id="06d6a-427">In hello Data Factory Editor, click **New pipeline** on hello command bar.</span></span> <span data-ttu-id="06d6a-428">Als u de opdracht Hallo niet ziet, klikt u op **... (Ellips)**  toosee deze.</span><span class="sxs-lookup"><span data-stu-id="06d6a-428">If you do not see hello command, click **... (Ellipsis)** toosee it.</span></span>
2. <span data-ttu-id="06d6a-429">Hallo JSON in het rechterdeelvenster Hallo vervangen door Hallo volgende JSON-script:</span><span class="sxs-lookup"><span data-stu-id="06d6a-429">Replace hello JSON in hello right pane with hello following JSON script:</span></span>

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
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
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   <span data-ttu-id="06d6a-430">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="06d6a-430">Note hello following points:</span></span>

   * <span data-ttu-id="06d6a-431">Er is slechts één activiteit in de pijplijn Hallo en die is van het type: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-431">There is only one activity in hello pipeline and that is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="06d6a-432">**AssemblyName** toohello naam Hallo dll-bestand dat is ingesteld: **MyDotNetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-432">**AssemblyName** is set toohello name of hello DLL: **MyDotNetActivity.dll**.</span></span>
   * <span data-ttu-id="06d6a-433">**EntryPoint** te is ingesteld,**MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-433">**EntryPoint** is set too**MyDotNetActivityNS.MyDotNetActivity**.</span></span> <span data-ttu-id="06d6a-434">Het is in feite \<naamruimte\>.\< ClassName\> in uw code.</span><span class="sxs-lookup"><span data-stu-id="06d6a-434">It is basically \<namespace\>.\<classname\> in your code.</span></span>
   * <span data-ttu-id="06d6a-435">**PackageLinkedService** te is ingesteld,**StorageLinkedService** die toohello blob-opslag met Hallo aangepaste activiteit zip-bestand verwijst.</span><span class="sxs-lookup"><span data-stu-id="06d6a-435">**PackageLinkedService** is set too**StorageLinkedService** that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="06d6a-436">Als u van andere Azure Storage-accounts voor i/o-bestanden en Hallo aangepaste activiteit zip-bestand gebruikmaakt, hebt u toocreate een andere Azure Storage gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="06d6a-436">If you are using different Azure Storage accounts for input/output files and hello custom activity zip file, you have toocreate another Azure Storage linked service.</span></span> <span data-ttu-id="06d6a-437">In dit artikel wordt ervan uitgegaan dat u hetzelfde Azure-opslagaccount Hallo.</span><span class="sxs-lookup"><span data-stu-id="06d6a-437">This article assumes that you are using hello same Azure Storage account.</span></span>
   * <span data-ttu-id="06d6a-438">**PackageFile** te is ingesteld,**customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-438">**PackageFile** is set too**customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="06d6a-439">Het Hallo-indeling is: \<containerforthezip\>/\<nameofthezip.zip\>.</span><span class="sxs-lookup"><span data-stu-id="06d6a-439">It is in hello format: \<containerforthezip\>/\<nameofthezip.zip\>.</span></span>
   * <span data-ttu-id="06d6a-440">Hallo aangepaste activiteit wordt **InputDataset** als invoer en **OutputDataset** als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="06d6a-440">hello custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="06d6a-441">Hallo **linkedServiceName** eigenschap van de aangepaste activiteit Hallo verwijst toohello **AzureBatchLinkedService**, waarin u Azure Data Factory bepaald die Hallo aangepaste activiteit moet toorun op Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="06d6a-441">hello **linkedServiceName** property of hello custom activity points toohello **AzureBatchLinkedService**, which tells Azure Data Factory that hello custom activity needs toorun on Azure Batch.</span></span>
   * <span data-ttu-id="06d6a-442">Hallo **gelijktijdigheid** instelling is belangrijk.</span><span class="sxs-lookup"><span data-stu-id="06d6a-442">hello **concurrency** setting is important.</span></span> <span data-ttu-id="06d6a-443">Als u Hallo-standaardwaarde, die 1, is zelfs als er 2 of meer in hello Azure Batch-pool rekenknooppunten, Hallo segmenten worden verwerkt achter elkaar.</span><span class="sxs-lookup"><span data-stu-id="06d6a-443">If you use hello default value, which is 1, even if you have 2 or more compute nodes in hello Azure Batch pool, hello slices are processed one after another.</span></span> <span data-ttu-id="06d6a-444">U onderneemt daarom niet profiteren van Hallo parallelle verwerking mogelijkheden van Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="06d6a-444">Therefore, you are not taking advantage of hello parallel processing capability of Azure Batch.</span></span> <span data-ttu-id="06d6a-445">Als u instelt **gelijktijdigheid** tooa hogere waarde, bijvoorbeeld 2 is, betekent dit dat twee segmenten (komt overeen tootwo taken in Azure Batch) kunnen worden verwerkt op Hallo dezelfde tijd, in welk geval beide VM Hallo in hello Azure Batch pool worden benut.</span><span class="sxs-lookup"><span data-stu-id="06d6a-445">If you set **concurrency** tooa higher value, say 2, it means that two slices (corresponds tootwo tasks in Azure Batch) can be processed at hello same time, in which case, both hello VMs in hello Azure Batch pool are utilized.</span></span> <span data-ttu-id="06d6a-446">Daarom op de juiste wijze Hallo gelijktijdigheid eigenschap instellen.</span><span class="sxs-lookup"><span data-stu-id="06d6a-446">Therefore, set hello concurrency property appropriately.</span></span>
   * <span data-ttu-id="06d6a-447">Slechts één taak (segment) wordt standaard uitgevoerd op een virtuele machine op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="06d6a-447">Only one task (slice) is executed on a VM at any point by default.</span></span> <span data-ttu-id="06d6a-448">Hallo reden is dat standaard hello **maximum aantal taken per VM** too1 voor een Azure Batch-toepassingen is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="06d6a-448">hello reason is that, by default, hello **Maximum tasks per VM** is set too1 for an Azure Batch pool.</span></span> <span data-ttu-id="06d6a-449">Als onderdeel van de vereisten, u hebt gemaakt een groep met deze eigenschap set too2, zodat twee segmenten van de Data Factory op een virtuele machine op Hallo uitvoeren kunnen hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="06d6a-449">As part of prerequisites, you created a pool with this property set too2, so two Data Factory slices can be running on a VM at hello same time.</span></span>

    -   <span data-ttu-id="06d6a-450">**isPaused** eigenschap toofalse standaard is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="06d6a-450">**isPaused** property is set toofalse by default.</span></span> <span data-ttu-id="06d6a-451">Hallo-pijplijn wordt onmiddellijk uitgevoerd in dit voorbeeld omdat Hallo segmenten te in de afgelopen Hallo starten.</span><span class="sxs-lookup"><span data-stu-id="06d6a-451">hello pipeline runs immediately in this example because hello slices start in hello past.</span></span> <span data-ttu-id="06d6a-452">U kunt deze eigenschap tootrue toopause Hallo pijplijn en zijn ingesteld dat deze back-toofalse toorestart.</span><span class="sxs-lookup"><span data-stu-id="06d6a-452">You can set this property tootrue toopause hello pipeline and set it back toofalse toorestart.</span></span>

    -   <span data-ttu-id="06d6a-453">Hallo **start** tijd en **end** segmenten hourly, geproduceerde zodat vijf segmenten worden geproduceerd door Hallo pijplijn en tijden zijn vijf uur uit elkaar liggen.</span><span class="sxs-lookup"><span data-stu-id="06d6a-453">hello **start** time and **end** times are five hours apart and slices are produced hourly, so five slices are produced by hello pipeline.</span></span>

1. <span data-ttu-id="06d6a-454">Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="06d6a-454">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span>

#### <a name="step-5-test-hello-pipeline"></a><span data-ttu-id="06d6a-455">Stap 5: Hallo pijplijn testen</span><span class="sxs-lookup"><span data-stu-id="06d6a-455">Step 5: Test hello pipeline</span></span>
<span data-ttu-id="06d6a-456">In deze stap kunt u Hallo pijplijn testen door de bestanden neerzetten in invoer Hallo-mappen.</span><span class="sxs-lookup"><span data-stu-id="06d6a-456">In this step, you test hello pipeline by dropping files into hello input folders.</span></span> <span data-ttu-id="06d6a-457">U begint met testen Hallo-pipeline met één bestand per één invoer map.</span><span class="sxs-lookup"><span data-stu-id="06d6a-457">Let’s start with testing hello pipeline with one file per one input folder.</span></span>

1. <span data-ttu-id="06d6a-458">Klik in de Data Factory-blade Hallo in hello Azure-portal, op **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-458">In hello Data Factory blade in hello Azure portal, click **Diagram**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. <span data-ttu-id="06d6a-459">Dubbelklik in de diagramweergave Hallo invoergegevensset: **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-459">In hello diagram view, double-click input dataset: **InputDataset**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. <span data-ttu-id="06d6a-460">U ziet Hallo **InputDataset** blade met alle vijf segmenten gereed.</span><span class="sxs-lookup"><span data-stu-id="06d6a-460">You should see hello **InputDataset** blade with all five slices ready.</span></span> <span data-ttu-id="06d6a-461">Kennisgeving Hallo **segment BEGINTIJD** en **segment EINDTIJD** voor elk segment.</span><span class="sxs-lookup"><span data-stu-id="06d6a-461">Notice hello **SLICE START TIME** and **SLICE END TIME** for each slice.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. <span data-ttu-id="06d6a-462">In Hallo **diagramweergave**, klik op nu **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-462">In hello **Diagram View**, now click **OutputDataset**.</span></span>
5. <span data-ttu-id="06d6a-463">U ziet dat Hallo vijf uitvoer segmenten Hallo status Ready heeft zijn als ze zijn al gemaakt.</span><span class="sxs-lookup"><span data-stu-id="06d6a-463">You should see that hello five output slices are in hello Ready state if they have already been produced.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. <span data-ttu-id="06d6a-464">Gebruik Azure portal tooview hello **taken** die zijn gekoppeld aan Hallo **segmenten** en zien welke VM die is uitgevoerd op elk segment.</span><span class="sxs-lookup"><span data-stu-id="06d6a-464">Use Azure portal tooview hello **tasks** associated with hello **slices** and see what VM each slice ran on.</span></span> <span data-ttu-id="06d6a-465">Zie [Data Factory en Batch-integratie](#data-factory-and-batch-integration) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="06d6a-465">See [Data Factory and Batch integration](#data-factory-and-batch-integration) section for details.</span></span>
7. <span data-ttu-id="06d6a-466">U ziet de uitvoerbestanden Hallo in Hallo `outputfolder` van `mycontainer` in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="06d6a-466">You should see hello output files in hello `outputfolder` of `mycontainer` in your Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   <span data-ttu-id="06d6a-467">Hier ziet u vijf uitvoerbestanden, één voor elke invoersegment.</span><span class="sxs-lookup"><span data-stu-id="06d6a-467">You should see five output files, one for each input slice.</span></span> <span data-ttu-id="06d6a-468">Elk Hallo uitvoervenster het volgende bestand inhoud vergelijkbare toohello na uitvoer moet hebben:</span><span class="sxs-lookup"><span data-stu-id="06d6a-468">Each of hello output file should have content similar toohello following output:</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   <span data-ttu-id="06d6a-469">Hallo volgende diagram illustreert hoe Hallo Data Factory segmenten tootasks in Azure Batch toegewezen.</span><span class="sxs-lookup"><span data-stu-id="06d6a-469">hello following diagram illustrates how hello Data Factory slices map tootasks in Azure Batch.</span></span> <span data-ttu-id="06d6a-470">In dit voorbeeld heeft een segment slechts één uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="06d6a-470">In this example, a slice has only one run.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. <span data-ttu-id="06d6a-471">Nu gaan we proberen met meerdere bestanden in een map.</span><span class="sxs-lookup"><span data-stu-id="06d6a-471">Now, let’s try with multiple files in a folder.</span></span> <span data-ttu-id="06d6a-472">Bestanden maken: **bestand2.txt samengevoegd**, **file3.txt**, **file4.txt**, en **file5.txt** Hello dezelfde inhoud zoals in bestand.txt in Hallo map: **2015-11-06-01**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-472">Create files: **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with hello same content as in file.txt in hello folder: **2015-11-06-01**.</span></span>
9. <span data-ttu-id="06d6a-473">In de uitvoermap hello, **verwijderen** Hallo uitvoerbestand: **2015-11-16-01.txt**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-473">In hello output folder, **delete** hello output file: **2015-11-16-01.txt**.</span></span>
10. <span data-ttu-id="06d6a-474">Nu in Hallo **OutputDataset** blade, klik met de rechtermuisknop Hallo segment met **segment BEGINTIJD** instellen te**16-11-2015 01:00:00 AM**, en klik op **uitvoeren**toorerun/opnieuw-proceskleuren Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="06d6a-474">Now, in hello **OutputDataset** blade, right-click hello slice with **SLICE START TIME** set too**11/16/2015 01:00:00 AM**, and click **Run** toorerun/re-process hello slice.</span></span> <span data-ttu-id="06d6a-475">Hallo-segment is nu vijf bestanden in plaats van een bestand.</span><span class="sxs-lookup"><span data-stu-id="06d6a-475">Now, hello slice has five files instead of one file.</span></span>

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. <span data-ttu-id="06d6a-476">Nadat het Hallo-segment wordt uitgevoerd en de status is **gereed**, Controleer Hallo inhoud in het uitvoerbestand Hallo voor dit segment (**2015-11-16-01.txt**) in Hallo `outputfolder` van `mycontainer` in de blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="06d6a-476">After hello slice runs and its status is **Ready**, verify hello content in hello output file for this slice (**2015-11-16-01.txt**) in hello `outputfolder` of `mycontainer` in your blob storage.</span></span> <span data-ttu-id="06d6a-477">Er moet een regel voor elk bestand van Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="06d6a-477">There should be a line for each file of hello slice.</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> <span data-ttu-id="06d6a-478">Als u niet 2015 in de Hallo uitvoer-bestand-11-16-01.txt verwijderen kon voordat u met vijf invoerbestanden, ziet u één regel van de vorige segment Hallo uitvoeren en vijf de regels van de huidige segment Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="06d6a-478">If you did not delete hello output file 2015-11-16-01.txt before trying with five input files, you see one line from hello previous slice run and five lines from hello current slice run.</span></span> <span data-ttu-id="06d6a-479">Standaard is Hallo inhoud toegevoegde toooutput bestand als dit al bestaat.</span><span class="sxs-lookup"><span data-stu-id="06d6a-479">By default, hello content is appended toooutput file if it already exists.</span></span>
>
>

#### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="06d6a-480">Data Factory en Batch-integratie</span><span class="sxs-lookup"><span data-stu-id="06d6a-480">Data Factory and Batch integration</span></span>
<span data-ttu-id="06d6a-481">Hallo Data Factory-service maakt een taak in Azure Batch met de naam van de Hallo: `adf-poolname:job-xxx`.</span><span class="sxs-lookup"><span data-stu-id="06d6a-481">hello Data Factory service creates a job in Azure Batch with hello name: `adf-poolname:job-xxx`.</span></span>

![Azure Data Factory - Batch-taken](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

<span data-ttu-id="06d6a-483">Een taak in Hallo-taak is gemaakt voor elke activiteit uitvoering van een segment.</span><span class="sxs-lookup"><span data-stu-id="06d6a-483">A task in hello job is created for each activity run of a slice.</span></span> <span data-ttu-id="06d6a-484">Als er 10 segmenten gereed toobe verwerkt, wordt 10 taken worden gemaakt in Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="06d6a-484">If there are 10 slices ready toobe processed, 10 tasks are created in hello job.</span></span> <span data-ttu-id="06d6a-485">U kunt meer dan één segment parallel worden uitgevoerd als er meerdere rekenknooppunten in de groep Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="06d6a-485">You can have more than one slice running in parallel if you have multiple compute nodes in hello pool.</span></span> <span data-ttu-id="06d6a-486">Als Hallo maximum aantal taken per knooppunt is ingesteld, te berekenen > 1, kunnen er meer dan één segmenteren op Hallo uitgevoerd dezelfde compute.</span><span class="sxs-lookup"><span data-stu-id="06d6a-486">If hello maximum tasks per compute node is set too> 1, there can be more than one slice running on hello same compute.</span></span>

<span data-ttu-id="06d6a-487">In dit voorbeeld zijn er vijf segmenten, dus vijf taken in Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="06d6a-487">In this example, there are five slices, so five tasks in Azure Batch.</span></span> <span data-ttu-id="06d6a-488">Hello **gelijktijdigheid** instellen te**5** in Hallo pipeline-JSON-code in Azure Data Factory en **maximum aantal taken per VM** instellen te**2** in Azure Batch groep met **2** virtuele machines, Hallo taken uitgevoerd snelle (Raadpleeg de begin- en eindtijden voor taken).</span><span class="sxs-lookup"><span data-stu-id="06d6a-488">With hello **concurrency** set too**5** in hello pipeline JSON in Azure Data Factory and **Maximum tasks per VM** set too**2** in Azure Batch pool with **2** VMs, hello tasks runs fast (check start and end times for tasks).</span></span>

<span data-ttu-id="06d6a-489">Gebruik Hallo portal tooview Hallo Batch-job en de bijbehorende taken die gekoppeld aan Hallo zijn **segmenten** en zien welke VM die is uitgevoerd op elk segment.</span><span class="sxs-lookup"><span data-stu-id="06d6a-489">Use hello portal tooview hello Batch job and its tasks that are associated with hello **slices** and see what VM each slice ran on.</span></span>

![Azure Data Factory - taken voor Batch-job](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a><span data-ttu-id="06d6a-491">Fouten opsporen in Hallo-pipeline</span><span class="sxs-lookup"><span data-stu-id="06d6a-491">Debug hello pipeline</span></span>
<span data-ttu-id="06d6a-492">De foutopsporing bestaat uit enkele basistechnieken:</span><span class="sxs-lookup"><span data-stu-id="06d6a-492">Debugging consists of a few basic techniques:</span></span>

1. <span data-ttu-id="06d6a-493">Als invoersegment met de Hallo te niet is ingesteld**gereed**, bevestigen dat de mapstructuur van Hallo invoer juist is en bestand.txt in de invoer mappen Hallo bestaat.</span><span class="sxs-lookup"><span data-stu-id="06d6a-493">If hello input slice is not set too**Ready**, confirm that hello input folder structure is correct and file.txt exists in hello input folders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. <span data-ttu-id="06d6a-494">In Hallo **Execute** methode van uw aangepaste activiteit, gebruik Hallo **IActivityLogger** object toolog informatie die u helpt oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="06d6a-494">In hello **Execute** method of your custom activity, use hello **IActivityLogger** object toolog information that helps you troubleshoot issues.</span></span> <span data-ttu-id="06d6a-495">in het logboek geregistreerd Hallo-berichten weergegeven in het Hallo-gebruiker\_0-logboekbestand.</span><span class="sxs-lookup"><span data-stu-id="06d6a-495">hello logged messages show up in hello user\_0.log file.</span></span>

   <span data-ttu-id="06d6a-496">In Hallo **OutputDataset** blade, klikt u op Hallo segment toosee hello **GEGEVENSSEGMENT** blade voor die segment.</span><span class="sxs-lookup"><span data-stu-id="06d6a-496">In hello **OutputDataset** blade, click hello slice toosee hello **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="06d6a-497">U ziet **activiteiten bij uitvoering** voor dit segment.</span><span class="sxs-lookup"><span data-stu-id="06d6a-497">You see **activity runs** for that slice.</span></span> <span data-ttu-id="06d6a-498">Hier ziet u een activiteit die wordt uitgevoerd voor Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="06d6a-498">You should see one activity run for hello slice.</span></span> <span data-ttu-id="06d6a-499">Als u op **uitvoeren** in de opdrachtbalk hello, begint u een andere activiteit die wordt uitgevoerd voor Hallo hetzelfde segment.</span><span class="sxs-lookup"><span data-stu-id="06d6a-499">If you click **Run** in hello command bar, you can start another activity run for hello same slice.</span></span>

   <span data-ttu-id="06d6a-500">Wanneer u klikt op Hallo activiteit die wordt uitgevoerd, ziet u Hallo **DETAILS uitvoering van activiteit** blade met een lijst met logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="06d6a-500">When you click hello activity run, you see hello **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="06d6a-501">Ziet u de geregistreerde berichten in Hallo **gebruiker\_0 logboek** bestand.</span><span class="sxs-lookup"><span data-stu-id="06d6a-501">You see logged messages in hello **user\_0.log** file.</span></span> <span data-ttu-id="06d6a-502">Wanneer er een fout optreedt, ziet u drie activiteiten bij uitvoering omdat het maximale aantal pogingen Hallo too3 in Hallo pipeline/activiteits-JSON is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="06d6a-502">When an error occurs, you see three activity runs because hello retry count is set too3 in hello pipeline/activity JSON.</span></span> <span data-ttu-id="06d6a-503">Wanneer u klikt op Hallo activiteit die wordt uitgevoerd, ziet u logboekbestanden Hallo tootroubleshoot Hallo fout kunt controleren.</span><span class="sxs-lookup"><span data-stu-id="06d6a-503">When you click hello activity run, you see hello log files that you can review tootroubleshoot hello error.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   <span data-ttu-id="06d6a-504">Klik in Hallo lijst van logboekbestanden op Hallo **gebruiker 0.log**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-504">In hello list of log files, click hello **user-0.log**.</span></span> <span data-ttu-id="06d6a-505">In het rechterpaneel Hallo zijn Hallo resultaten van het gebruik van Hallo **IActivityLogger.Write** methode.</span><span class="sxs-lookup"><span data-stu-id="06d6a-505">In hello right panel are hello results of using hello **IActivityLogger.Write** method.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   <span data-ttu-id="06d6a-506">Controleer de systeem-0.log voor elk systeem foutberichten en uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="06d6a-506">Check system-0.log for any system error messages and exceptions.</span></span>

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. <span data-ttu-id="06d6a-507">Hallo omvatten **PDB** bestand in het zip-bestand Hallo zodat Hallo foutdetails beschikt over informatie zoals **aanroepstack** wanneer er een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="06d6a-507">Include hello **PDB** file in hello zip file so that hello error details have information such as **call stack** when an error occurs.</span></span>
4. <span data-ttu-id="06d6a-508">Alle bestanden in het zip-bestand Hallo Hallo voor Hallo aangepaste activiteit op Hallo moet **bovenste niveau** zonder submappen.</span><span class="sxs-lookup"><span data-stu-id="06d6a-508">All hello files in hello zip file for hello custom activity must be at hello **top level** with no subfolders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. <span data-ttu-id="06d6a-509">Zorg ervoor dat Hallo **assemblyName** (MyDotNetActivity.dll) **entryPoint** (MyDotNetActivityNS.MyDotNetActivity) **packageFile** (customactivitycontainer / MyDotNetActivity.zip) en **packageLinkedService** (moet punt toohello Azure blob-opslag die Hallo zip-bestand bevat) toocorrect waarden zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="06d6a-509">Ensure that hello **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point toohello Azure blob storage that contains hello zip file) are set toocorrect values.</span></span>
6. <span data-ttu-id="06d6a-510">Als u een fout en wilt tooreprocess Hallo segment hebt opgelost, met de rechtermuisknop op Hallo segment Hallo **OutputDataset** blade en klik op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-510">If you fixed an error and want tooreprocess hello slice, right-click hello slice in hello **OutputDataset** blade and click **Run**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > <span data-ttu-id="06d6a-511">U ziet een **container** in uw Azure Blob-opslag met de naam: `adfjobs`.</span><span class="sxs-lookup"><span data-stu-id="06d6a-511">You see a **container** in your Azure Blob storage named: `adfjobs`.</span></span> <span data-ttu-id="06d6a-512">Deze container wordt niet automatisch verwijderd, maar u het veilig kunt verwijderen nadat u klaar bent met testen Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="06d6a-512">This container is not automatically deleted, but you can safely delete it after you are done testing hello solution.</span></span> <span data-ttu-id="06d6a-513">Op deze manier Hallo Data Factory-oplossing maakt u een Azure-Batch **taak** met de naam: `adf-\<pool ID/name\>:job-0000000001`.</span><span class="sxs-lookup"><span data-stu-id="06d6a-513">Similarly, hello Data Factory solution creates an Azure Batch **job** named: `adf-\<pool ID/name\>:job-0000000001`.</span></span> <span data-ttu-id="06d6a-514">Nadat u Hallo oplossing als u dit wilt testen, kunt u deze taak verwijderen.</span><span class="sxs-lookup"><span data-stu-id="06d6a-514">You can delete this job after you test hello solution if you like.</span></span>
   >
   >
7. <span data-ttu-id="06d6a-515">Hallo aangepaste activiteit gebruikt geen Hallo **app.config** bestand van het pakket.</span><span class="sxs-lookup"><span data-stu-id="06d6a-515">hello custom activity does not use hello **app.config** file from your package.</span></span> <span data-ttu-id="06d6a-516">Dus als uw code wordt een verbindingsreeksen uit het Hallo-configuratiebestand gelezen, werkt het niet tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="06d6a-516">Therefore, if your code reads any connection strings from hello configuration file, it does not work at runtime.</span></span> <span data-ttu-id="06d6a-517">Hallo beste wanneer toohold met behulp van Azure Batch is geen geheimen in een **Azure KeyVault**, gebruikt u een certificaat gebaseerde service principal tooprotect hello keyvault en distribueren Hallo certificaat tooAzure Batch-pool.</span><span class="sxs-lookup"><span data-stu-id="06d6a-517">hello best practice when using Azure Batch is toohold any secrets in an **Azure KeyVault**, use a certificate-based service principal tooprotect hello keyvault, and distribute hello certificate tooAzure Batch pool.</span></span> <span data-ttu-id="06d6a-518">Hallo aangepaste activiteit .NET vervolgens toegang tot geheimen Hallo KeyVault tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="06d6a-518">hello .NET custom activity then can access secrets from hello KeyVault at runtime.</span></span> <span data-ttu-id="06d6a-519">Deze oplossing is een algemene en tooany type geheim, niet alleen verbindingsreeks kunt schalen.</span><span class="sxs-lookup"><span data-stu-id="06d6a-519">This solution is a generic one and can scale tooany type of secret, not just connection string.</span></span>

    <span data-ttu-id="06d6a-520">Er is een eenvoudiger tijdelijke oplossing (maar niet aanbevolen): kunt u een **Azure SQL gekoppelde service** met verbindingstekenreeksinstellingen, maken een gegevensset dat wordt gebruikt Hallo gekoppelde service en de keten Hallo dataset als een dummy invoergegevensset toohello aangepaste .NET-activiteit.</span><span class="sxs-lookup"><span data-stu-id="06d6a-520">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses hello linked service, and chain hello dataset as a dummy input dataset toohello custom .NET activity.</span></span> <span data-ttu-id="06d6a-521">U kunt vervolgens toegang Hallo gekoppeld de verbindingsreeks van de service in Hallo aangepaste activiteitscode en deze tijdens runtime werken moet.</span><span class="sxs-lookup"><span data-stu-id="06d6a-521">You can then access hello linked service's connection string in hello custom activity code and it should work fine at runtime.</span></span>  

#### <a name="extend-hello-sample"></a><span data-ttu-id="06d6a-522">Hallo voorbeeld uitbreiden</span><span class="sxs-lookup"><span data-stu-id="06d6a-522">Extend hello sample</span></span>
<span data-ttu-id="06d6a-523">U kunt uitbreiden in dit voorbeeld toolearn informatie over Azure Data Factory en Azure Batch-functies.</span><span class="sxs-lookup"><span data-stu-id="06d6a-523">You can extend this sample toolearn more about Azure Data Factory and Azure Batch features.</span></span> <span data-ttu-id="06d6a-524">Bijvoorbeeld tooprocess segmenten in een ander tijdsbereik Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="06d6a-524">For example, tooprocess slices in a different time range, do hello following steps:</span></span>

1. <span data-ttu-id="06d6a-525">Toevoegen van de volgende submappen in Hallo Hallo `inputfolder`: 2015-11-16-05 2015-11-16-06 201-11-16-07, 2011-11-16-08, 2015-11-16-09 en plaats invoerbestanden in deze mappen.</span><span class="sxs-lookup"><span data-stu-id="06d6a-525">Add hello following subfolders in hello `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 and place input files in those folders.</span></span> <span data-ttu-id="06d6a-526">Hallo-eindtijd voor de pijplijn Hallo van wijzigen `2015-11-16T05:00:00Z` te`2015-11-16T10:00:00Z`.</span><span class="sxs-lookup"><span data-stu-id="06d6a-526">Change hello end time for hello pipeline from `2015-11-16T05:00:00Z` too`2015-11-16T10:00:00Z`.</span></span> <span data-ttu-id="06d6a-527">In Hallo **diagramweergave**, dubbelklikt u op Hallo **InputDataset**, en controleer of de invoersegmenten één keer Hallo gereed zijn.</span><span class="sxs-lookup"><span data-stu-id="06d6a-527">In hello **Diagram View**, double-click hello **InputDataset**, and confirm that hello input slices are ready.</span></span> <span data-ttu-id="06d6a-528">Dubbelklik op **OuptutDataset** toosee Hallo status van de uitvoer-segmenten.</span><span class="sxs-lookup"><span data-stu-id="06d6a-528">Double-click **OuptutDataset** toosee hello state of output slices.</span></span> <span data-ttu-id="06d6a-529">Als ze zich in de status Ready heeft, controleert u Hallo uitvoermap voor uitvoerbestanden Hallo.</span><span class="sxs-lookup"><span data-stu-id="06d6a-529">If they are in Ready state, check hello output folder for hello output files.</span></span>
2. <span data-ttu-id="06d6a-530">Vergroten of verkleinen Hallo **gelijktijdigheid** instelling toounderstand hoe dit van invloed op prestaties van uw oplossing Hallo vooral Hallo verwerken die wordt uitgevoerd op Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="06d6a-530">Increase or decrease hello **concurrency** setting toounderstand how it affects hello performance of your solution, especially hello processing that occurs on Azure Batch.</span></span> <span data-ttu-id="06d6a-531">(Zie stap 4: maken en uitvoeren van Hallo pijplijn voor meer informatie over Hallo **gelijktijdigheid** instelling.)</span><span class="sxs-lookup"><span data-stu-id="06d6a-531">(See Step 4: Create and run hello pipeline for more on hello **concurrency** setting.)</span></span>
3. <span data-ttu-id="06d6a-532">Een pool maken met de hogere en kleine **maximum aantal taken per VM**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-532">Create a pool with higher/lower **Maximum tasks per VM**.</span></span> <span data-ttu-id="06d6a-533">toouse Hallo u hebt gemaakt, nieuwe pool update Hallo gekoppelde Azure-Batch-service in Hallo Data Factory-oplossing.</span><span class="sxs-lookup"><span data-stu-id="06d6a-533">toouse hello new pool you created, update hello Azure Batch linked service in hello Data Factory solution.</span></span> <span data-ttu-id="06d6a-534">(Zie stap 4: maken en uitvoeren van Hallo pijplijn voor meer informatie over Hallo **maximum aantal taken per VM** instelling.)</span><span class="sxs-lookup"><span data-stu-id="06d6a-534">(See Step 4: Create and run hello pipeline for more on hello **Maximum tasks per VM** setting.)</span></span>
4. <span data-ttu-id="06d6a-535">Maken van een Azure Batch-pool met **automatisch schalen** functie.</span><span class="sxs-lookup"><span data-stu-id="06d6a-535">Create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="06d6a-536">Automatisch vergroten/verkleinen rekenknooppunten in een Azure Batch-pool is Hallo dynamische aanpassing van de verwerkingskracht die worden gebruikt door de toepassing.</span><span class="sxs-lookup"><span data-stu-id="06d6a-536">Automatically scaling compute nodes in an Azure Batch pool is hello dynamic adjustment of processing power used by your application.</span></span> 

    <span data-ttu-id="06d6a-537">Hallo formule hier realiseert Hallo volgende gedrag: wanneer Hallo van toepassingen in eerste instantie is gemaakt, wordt 1 VM gestart.</span><span class="sxs-lookup"><span data-stu-id="06d6a-537">hello sample formula here achieves hello following behavior: When hello pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="06d6a-538">$PendingTasks metriek definieert Hallo aantal taken in uitvoering + actief (in de wachtrij) staat.</span><span class="sxs-lookup"><span data-stu-id="06d6a-538">$PendingTasks metric defines hello number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="06d6a-539">Hallo formule zoekt Hallo gemiddelde aantal in behandeling zijnde taken in Hallo afgelopen 180 seconden en dienovereenkomstig TargetDedicated ingesteld.</span><span class="sxs-lookup"><span data-stu-id="06d6a-539">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="06d6a-540">Hiermee zorgt u ervoor dat TargetDedicated nooit zich verder uitstrekt dan 25 virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="06d6a-540">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="06d6a-541">Dus als nieuwe taken worden verzonden, pool automatisch groeit en als taken zijn voltooid, virtuele machines worden gratis één voor één en Hallo automatisch schalen die virtuele machines wordt verkleind.</span><span class="sxs-lookup"><span data-stu-id="06d6a-541">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and hello autoscaling shrinks those VMs.</span></span> <span data-ttu-id="06d6a-542">startingNumberOfVMs en maxNumberofVMs kunnen worden aangepast tooyour behoeften.</span><span class="sxs-lookup"><span data-stu-id="06d6a-542">startingNumberOfVMs and maxNumberofVMs can be adjusted tooyour needs.</span></span>
 
    <span data-ttu-id="06d6a-543">De formule voor automatisch schalen:</span><span class="sxs-lookup"><span data-stu-id="06d6a-543">Autoscale formula:</span></span>

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   <span data-ttu-id="06d6a-544">Zie [automatisch schalen rekenknooppunten in een Azure Batch-pool](../batch/batch-automatic-scaling.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="06d6a-544">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

   <span data-ttu-id="06d6a-545">Als groep Hallo Hallo standaard [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), Hallo Batch-service kan enige tijd duren 15-30 minuten tooprepare Hallo VM voordat Hallo aangepaste activiteit wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="06d6a-545">If hello pool is using hello default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch service could take 15-30 minutes tooprepare hello VM before running hello custom activity.</span></span>  <span data-ttu-id="06d6a-546">Als Hallo groep van een andere autoScaleEvaluationInterval gebruikmaakt, Hallo Batch-service kan enige tijd duren autoScaleEvaluationInterval + 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="06d6a-546">If hello pool is using a different autoScaleEvaluationInterval, hello Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>
5. <span data-ttu-id="06d6a-547">In de voorbeeld-oplossing Hallo Hallo **Execute** methode aanroept Hallo **Calculate** methode die een invoergegevens segment tooproduce een gegevenssegment uitvoer verwerkt.</span><span class="sxs-lookup"><span data-stu-id="06d6a-547">In hello sample solution, hello **Execute** method invokes hello **Calculate** method that processes an input data slice tooproduce an output data slice.</span></span> <span data-ttu-id="06d6a-548">U kunt uw eigen methode tooprocess invoergegevens en vervang Hallo Calculate methodeaanroep in Hallo Execute-methode door een aanroep van tooyour methode schrijven.</span><span class="sxs-lookup"><span data-stu-id="06d6a-548">You can write your own method tooprocess input data and replace hello Calculate method call in hello Execute method with a call tooyour method.</span></span>

### <a name="next-steps-consume-hello-data"></a><span data-ttu-id="06d6a-549">Volgende stappen: Hallo gegevens gebruiken</span><span class="sxs-lookup"><span data-stu-id="06d6a-549">Next steps: Consume hello data</span></span>
<span data-ttu-id="06d6a-550">Nadat u gegevens verwerken, kunt u het verbruiken met online hulpmiddelen zoals **Microsoft Power BI**.</span><span class="sxs-lookup"><span data-stu-id="06d6a-550">After you process data, you can consume it with online tools like **Microsoft Power BI**.</span></span> <span data-ttu-id="06d6a-551">Hier vindt u koppelingen toohelp begrijpen van Power BI en hoe toouse in Azure:</span><span class="sxs-lookup"><span data-stu-id="06d6a-551">Here are links toohelp you understand Power BI and how toouse it in Azure:</span></span>

* [<span data-ttu-id="06d6a-552">Een gegevensset in Power BI verkennen</span><span class="sxs-lookup"><span data-stu-id="06d6a-552">Explore a dataset in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [<span data-ttu-id="06d6a-553">Aan de slag met Power BI Desktop Hallo</span><span class="sxs-lookup"><span data-stu-id="06d6a-553">Getting started with hello Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [<span data-ttu-id="06d6a-554">Vernieuwen van gegevens in Power BI</span><span class="sxs-lookup"><span data-stu-id="06d6a-554">Refresh data in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [<span data-ttu-id="06d6a-555">Azure en Power BI - basisoverzicht</span><span class="sxs-lookup"><span data-stu-id="06d6a-555">Azure and Power BI - basic overview</span></span>](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a><span data-ttu-id="06d6a-556">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="06d6a-556">References</span></span>
* [<span data-ttu-id="06d6a-557">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="06d6a-557">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

  * [<span data-ttu-id="06d6a-558">Inleiding tooAzure Data Factory-service</span><span class="sxs-lookup"><span data-stu-id="06d6a-558">Introduction tooAzure Data Factory service</span></span>](data-factory-introduction.md)
  * [<span data-ttu-id="06d6a-559">Aan de slag met Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="06d6a-559">Get started with Azure Data Factory</span></span>](data-factory-build-your-first-pipeline.md)
  * [<span data-ttu-id="06d6a-560">Aangepaste activiteiten gebruiken in een Azure Data Factory-pijplijn</span><span class="sxs-lookup"><span data-stu-id="06d6a-560">Use custom activities in an Azure Data Factory pipeline</span></span>](data-factory-use-custom-activities.md)
* [<span data-ttu-id="06d6a-561">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="06d6a-561">Azure Batch</span></span>](https://azure.microsoft.com/documentation/services/batch/)

  * [<span data-ttu-id="06d6a-562">Basisbeginselen van Azure Batch</span><span class="sxs-lookup"><span data-stu-id="06d6a-562">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
  * [<span data-ttu-id="06d6a-563">Overzicht van Azure Batch-functies</span><span class="sxs-lookup"><span data-stu-id="06d6a-563">Overview of Azure Batch features</span></span>](../batch/batch-api-basics.md)
  * [<span data-ttu-id="06d6a-564">Maken en beheren van Azure Batch-account in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="06d6a-564">Create and manage Azure Batch account in hello Azure portal</span></span>](../batch/batch-account-create-portal.md)
  * [<span data-ttu-id="06d6a-565">Aan de slag met Azure Batch-bibliotheek .NET</span><span class="sxs-lookup"><span data-stu-id="06d6a-565">Get started with Azure Batch Library .NET</span></span>](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
