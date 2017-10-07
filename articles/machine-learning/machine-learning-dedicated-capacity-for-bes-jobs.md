---
title: aaaDedicated capaciteit voor Machine Learning uitvoering Service batchtaken | Microsoft Docs
description: Overzicht van Azure Batch-services voor Machine Learning-taken.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: bba7970bb31c50e5b0b9d5f4ff4f0d2dacf942e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a><span data-ttu-id="5c4c2-103">Azure Batch-service voor Machine Learning-taken</span><span class="sxs-lookup"><span data-stu-id="5c4c2-103">Azure Batch service for Machine Learning jobs</span></span>

<span data-ttu-id="5c4c2-104">Machine Learning Batch-Pool verwerking voorziet door de klant beheerde scale in hello Azure Machine Learning Batch uitvoering-Service.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-104">Machine Learning Batch Pool processing provides customer-managed scale for hello Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="5c4c2-105">Klassieke batchverwerking voor machine learning vindt plaats in een omgeving met meerdere tenants welke limieten Hallo aantal gelijktijdige taken u kunt verzenden en taken in de wachtrij op basis van de eerste in first out.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-105">Classic batch processing for machine learning takes place in a multi-tenant environment, which limits hello number of concurrent jobs you can submit, and jobs are queued on a first-in-first-out basis.</span></span> <span data-ttu-id="5c4c2-106">Deze onzekerheid betekent dat valt niet nauwkeurig te voorspellen wanneer de taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-106">This uncertainty means that you can't accurately predict when your job will run.</span></span>

<span data-ttu-id="5c4c2-107">Batch-Pool verwerking kunt u toocreate groepen waarop u batch-taken kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-107">Batch Pool processing allows you toocreate pools on which you can submit batch jobs.</span></span> <span data-ttu-id="5c4c2-108">U bepaalt de Hallo grootte van Hallo pool en toowhich groep Hallo job wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-108">You control hello size of hello pool, and toowhich pool hello job is submitted.</span></span> <span data-ttu-id="5c4c2-109">Uw BES-taak wordt uitgevoerd in een eigen verwerken ruimte biedt voorspelbare verwerkingsprestaties en Hallo mogelijkheid toocreate resourcegroepen die overeenkomen met de verwerkingsbelasting toohello die u verzendt.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-109">Your BES job runs in its own processing space providing predictable processing performance and hello ability toocreate resource pools that correspond toohello processing load that you submit.</span></span>

## <a name="how-toouse-batch-pool-processing"></a><span data-ttu-id="5c4c2-110">Hoe toouse Batch-Pool verwerking</span><span class="sxs-lookup"><span data-stu-id="5c4c2-110">How toouse Batch Pool processing</span></span>

<span data-ttu-id="5c4c2-111">Configuratie van de verwerking van de Batch-Pool is momenteel niet beschikbaar via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-111">Configuration of Batch Pool Processing is not currently available through hello Azure portal.</span></span> <span data-ttu-id="5c4c2-112">Batch-Pool toouse verwerken, moet:</span><span class="sxs-lookup"><span data-stu-id="5c4c2-112">toouse Batch Pool processing, you must:</span></span>

-   <span data-ttu-id="5c4c2-113">Aanroepen van CSS toocreate een Batch-Pool-Account en de URL van een Pool-Service en een autorisatiesleutel verkrijgen</span><span class="sxs-lookup"><span data-stu-id="5c4c2-113">Call CSS toocreate a Batch Pool Account and obtain a Pool Service URL and an authorization key</span></span>
-   <span data-ttu-id="5c4c2-114">Een nieuwe Resource Manager gebaseerde web-service en een abonnement maken</span><span class="sxs-lookup"><span data-stu-id="5c4c2-114">Create a New Resource Manager based web service and billing plan</span></span>

<span data-ttu-id="5c4c2-115">toocreate je account, bellen Microsoft Customer Service and Support (CSS) en geef uw abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-115">toocreate your account, call Microsoft Customer Service and Support (CSS) and provide your Subscription ID.</span></span> <span data-ttu-id="5c4c2-116">CSS geschikt is voor u toodetermine Hallo juiste capaciteit voor uw scenario.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-116">CSS will work with you toodetermine hello appropriate capacity for your scenario.</span></span> <span data-ttu-id="5c4c2-117">CSS configureert vervolgens uw account met Hallo kunt u het maximum aantal groepen kunt u maken en Hallo maximum aantal virtuele machines (VM's) die u kunt in elke groep van toepassingen plaatsen.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-117">CSS then configures your account with hello maximum number of pools you can create and hello maximum number of virtual machines (VMs) that you can place in each pool.</span></span> <span data-ttu-id="5c4c2-118">Wanneer uw account is geconfigureerd, kunt u de URL van de Pool-Service en een autorisatiesleutel zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-118">Once your account is configured, you are provided your Pool Service URL and an authorization key.</span></span>

<span data-ttu-id="5c4c2-119">Nadat uw account is gemaakt, gebruikt u Hallo Pool Service-URL en autorisatie sleutel tooperform groep beheerbewerkingen op uw Batch-Pool.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-119">After your account is created, you use hello Pool Service URL and authorization key tooperform pool management operations on your Batch Pool.</span></span>

![Architectuur van batch pool-service.](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

<span data-ttu-id="5c4c2-121">U maken groepen door het aanroepen van Hallo groep maken-bewerking op Hallo van toepassingen service-URL die tooyou CSS opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-121">You create pools by calling hello Create Pool operation on hello pool service URL that CSS provided tooyou.</span></span> <span data-ttu-id="5c4c2-122">Wanneer u een pool maakt, moet u aangeven Hallo aantal VM's en Hallo-URL van Hallo swagger.json van een nieuwe Resource Manager op basis van Machine Learning-webservice.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-122">When you create a pool, specify hello number of VMs and hello URL of hello swagger.json of a New Resource Manager based Machine Learning web service.</span></span> <span data-ttu-id="5c4c2-123">Deze webservice is tooestablish Hallo facturering koppeling opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-123">This web service is provided tooestablish hello billing association.</span></span> <span data-ttu-id="5c4c2-124">Hallo Batch-Pool-service gebruikt Hallo swagger.json tooassociate Hallo van toepassingen met een abonnement.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-124">hello Batch Pool service uses hello swagger.json tooassociate hello pool with a billing plan.</span></span> <span data-ttu-id="5c4c2-125">U kunt BES uitvoeren beide nieuwe Resource Manager gebaseerde webservice en klassieke, dat u op Hallo van toepassingen kiezen.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-125">You can run any BES web service, both New Resource Manager based and classic, you choose on hello pool.</span></span>

<span data-ttu-id="5c4c2-126">U kunt een nieuwe Resource Manager gebaseerde webservice gebruiken, maar houd er rekening mee dat Hallo facturering voor Hallo taken worden in rekening gebracht tegen Hallo-abonnement is gekoppeld aan die service.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-126">You can use any New Resource Manager based web service, but be aware that hello billing for hello jobs are charged against hello billing plan associated with that service.</span></span> <span data-ttu-id="5c4c2-127">U kunt een web-service en de nieuwe facturering plannen toocreate specifiek voor het uitvoeren van taken in Batch-Pool.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-127">You may want toocreate a web service and new billing plan specifically for running Batch Pool jobs.</span></span>

<span data-ttu-id="5c4c2-128">Zie voor meer informatie over het maken van webservices [Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="5c4c2-128">For more information on creating web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="5c4c2-129">Nadat u een groep hebt gemaakt, dient u Hallo BES taak met behulp van Batch aanvragen URL Hallo voor Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-129">Once you have created a pool, you submit hello BES job using hello Batch Requests URL for hello web service.</span></span> <span data-ttu-id="5c4c2-130">U kunt toosubmit het tooa groep of tooclassic batchverwerking.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-130">You can choose toosubmit it tooa pool or tooclassic batch processing.</span></span> <span data-ttu-id="5c4c2-131">een Pool verwerking van een taak tooBatch toosubmit, u Hallo verzending aanvraagtekst voor parameter toohello taak na toevoegen:</span><span class="sxs-lookup"><span data-stu-id="5c4c2-131">toosubmit a job tooBatch Pool processing, you add hello following parameter toohello job submission request body:</span></span>

<span data-ttu-id="5c4c2-132">'AzureBatchPoolId': '&lt;ID-groep&gt;'</span><span class="sxs-lookup"><span data-stu-id="5c4c2-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span></span>

<span data-ttu-id="5c4c2-133">Als u Hallo-parameter niet toevoegt, worden Hallo-taak wordt uitgevoerd in Hallo klassieke batch procesomgeving.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-133">If you do not add hello parameter, hello job is run in hello classic batch process environment.</span></span> <span data-ttu-id="5c4c2-134">Als Hallo van toepassingen onvoldoende bronnen beschikbaar heeft, Hallo-taak wordt gestart onmiddellijk uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-134">If hello pool has available resources, hello job starts running immediately.</span></span> <span data-ttu-id="5c4c2-135">Als het Hallo-groep heeft geen gratis resources, uw taak in de wachtrij staat tot een resource beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-135">If hello pool does not have free resources, your job is queued until a resource is available.</span></span>

<span data-ttu-id="5c4c2-136">Als u dat u regelmatig Hallo-capaciteit van uw pools bereiken en u de grotere capaciteit moet vinden, kunt u CSS aanroepen en werken met een representatieve tooincrease uw quota's.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-136">If you find that you regularly reach hello capacity of your pools, and you need increased capacity, you can call CSS and work with a representative tooincrease your quotas.</span></span>

<span data-ttu-id="5c4c2-137">Voorbeeld van de aanvraag:</span><span class="sxs-lookup"><span data-stu-id="5c4c2-137">Example Request:</span></span>

<span data-ttu-id="5c4c2-138">https://ussouthcentral.Services.azureml.NET/Subscriptions/80c77c7674ba4c8c82294c3b2957990c/Services/9fe659022c9747e3b9b7b923c3830623/Jobs?API-Version=2.0</span><span class="sxs-lookup"><span data-stu-id="5c4c2-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span></span>

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a><span data-ttu-id="5c4c2-139">Overwegingen bij het gebruik van de verwerking van de Batch-Pool</span><span class="sxs-lookup"><span data-stu-id="5c4c2-139">Considerations when using Batch Pool processing</span></span>

<span data-ttu-id="5c4c2-140">Batch-Pool verwerking is een factureerbare service altijd op en waarvoor u deze met een Resource Manager abonnement gebaseerd tooassociate is vereist.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-140">Batch Pool Processing is an always-on billable service and that requires you tooassociate it with a Resource Manager based billing plan.</span></span> <span data-ttu-id="5c4c2-141">U wordt alleen gefactureerd voor Hallo aantal rekenuren Hallo van toepassingen wordt uitgevoerd. ongeacht Hallo aantal taken gedurende die tijd van toepassingen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-141">You are only billed for hello number of compute hours hello pool is running; regardless of hello number of jobs run during that time pool.</span></span> <span data-ttu-id="5c4c2-142">Als u een pool maakt, wordt u gefactureerd voor Hallo rekenuren van elke virtuele machine in de groep Hallo totdat het Hallo-pool wordt verwijderd, zelfs als er geen batchtaken worden uitgevoerd in de groep Hallo.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-142">If you create a pool, you are billed for hello compute hours of each virtual machine in hello pool until hello pool is deleted, even if no batch jobs are running in hello pool.</span></span> <span data-ttu-id="5c4c2-143">Facturering voor Hallo virtuele machines wordt gestart wanneer ze klaar zijn met het inrichten en stopt wanneer ze zijn verwijderd.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-143">Billing for hello virtual machines starts when they have finished provisioning and stops when they have been deleted.</span></span> <span data-ttu-id="5c4c2-144">U kunt een van de Hallo-abonnementen gevonden op Hallo [Machine Learning-prijzen pagina](https://azure.microsoft.com/pricing/details/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="5c4c2-144">You can use any of hello plans found on hello [Machine Learning Pricing page](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span>

<span data-ttu-id="5c4c2-145">Facturering voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5c4c2-145">Billing example:</span></span>

<span data-ttu-id="5c4c2-146">Als u een Batch-Pool met 2 virtuele machines maken en die na 24 uur die uw abonnement is 48 gedebiteerd rekenuren; verwijderen ongeacht hoeveel taken zijn uitgevoerd tijdens deze periode.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-146">If you create a Batch Pool with 2 virtual machines and delete it after 24 hours your billing plan is debited 48 compute hours; regardless of how many jobs were run during that period.</span></span>

<span data-ttu-id="5c4c2-147">Als u een Batch-Pool met 4 virtuele machines maken en na 12 uur verwijderen, wordt uw abonnement is ook gedebiteerd 48 rekenuren.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-147">If you create a Batch Pool with 4 virtual machines and delete it after 12 hours, your billing plan is also debited 48 compute hours.</span></span>

<span data-ttu-id="5c4c2-148">Het is raadzaam dat u Hallo taak status toodetermine pollen wanneer taken zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-148">We recommend that you poll hello job status toodetermine when jobs complete.</span></span> <span data-ttu-id="5c4c2-149">Wanneer alle uw taken uitgevoerd hebt, roept u Hallo formaat groep bewerking tooset Hallo aantal virtuele machines in Hallo groep toozero.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-149">When all your jobs have finished running, call hello Resize Pool operation tooset hello number of virtual machines in hello pool toozero.</span></span> <span data-ttu-id="5c4c2-150">Als u op de resources in de korte en u toocreate een nieuwe groep, bijvoorbeeld toobill op basis van een ander abonnement moet, kunt u Hallo groep in plaats daarvan verwijderen wanneer alle uw taken uitgevoerd hebt.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-150">If you are short on pool resources and you need toocreate a new pool, for example toobill against a different billing plan, you can delete hello pool instead when all your jobs have finished running.</span></span>


| <span data-ttu-id="5c4c2-151">**Batch-Pool verwerking als gebruiken**</span><span class="sxs-lookup"><span data-stu-id="5c4c2-151">**Use Batch Pool Processing when**</span></span>    | <span data-ttu-id="5c4c2-152">**Klassieke batchverwerking wanneer gebruiken**</span><span class="sxs-lookup"><span data-stu-id="5c4c2-152">**Use classic batch processing when**</span></span>  |
|---|---|
|<span data-ttu-id="5c4c2-153">U moet een groot aantal taken toorun</span><span class="sxs-lookup"><span data-stu-id="5c4c2-153">You need toorun a large number of jobs</span></span><br><span data-ttu-id="5c4c2-154">of</span><span class="sxs-lookup"><span data-stu-id="5c4c2-154">Or</span></span><br/><span data-ttu-id="5c4c2-155">U moet tooknow dat uw taken onmiddellijk wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="5c4c2-155">You need tooknow that your jobs will run immediately</span></span><br/><span data-ttu-id="5c4c2-156">of</span><span class="sxs-lookup"><span data-stu-id="5c4c2-156">Or</span></span><br/><span data-ttu-id="5c4c2-157">U moet gegarandeerde doorvoer.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-157">You need guaranteed throughput.</span></span> <span data-ttu-id="5c4c2-158">Bijvoorbeeld, u moet toorun een aantal taken in een bepaalde periode en tooscale wilt uit uw resources compute toomeet uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="5c4c2-158">For example, you need toorun a number of jobs in a given time frame, and want tooscale out your compute resources toomeet your needs.</span></span>    | <span data-ttu-id="5c4c2-159">U kunt een paar taken worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="5c4c2-159">You are running just a few jobs</span></span><br/><span data-ttu-id="5c4c2-160">En</span><span class="sxs-lookup"><span data-stu-id="5c4c2-160">And</span></span><br/> <span data-ttu-id="5c4c2-161">Hoeft u niet Hallo taken toorun onmiddellijk</span><span class="sxs-lookup"><span data-stu-id="5c4c2-161">You don’t need hello jobs toorun immediately</span></span> |
