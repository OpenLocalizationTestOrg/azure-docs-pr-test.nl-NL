---
title: een Machine Learning-Model aaaRetrain | Microsoft Docs
description: Meer informatie over hoe Hallo Web service toouse Hallo zojuist getrainde model in Azure Machine Learning tooretrain een model en bij te werken.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: d1cb6088-4f7c-4c32-94f2-f7523dad9059
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 342bb9954105339b4b634ff20968a64f4f9f750e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-machine-learning-model"></a><span data-ttu-id="89721-103">Opnieuw een Machine Learning-Model te trainen</span><span class="sxs-lookup"><span data-stu-id="89721-103">Retrain a Machine Learning Model</span></span>
<span data-ttu-id="89721-104">Het model is als onderdeel van het proces van uitoefening van machine learning-modellen in Azure Machine Learning Hallo getraind en opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="89721-104">As part of hello process of operationalization of machine learning models in Azure Machine Learning, your model is trained and saved.</span></span> <span data-ttu-id="89721-105">Vervolgens gebruikt u deze toocreate predicative Web-service.</span><span class="sxs-lookup"><span data-stu-id="89721-105">You then use it toocreate a predicative Web service.</span></span> <span data-ttu-id="89721-106">Hallo-webservice kan vervolgens worden gebruikt in websites, dashboards en mobiele apps.</span><span class="sxs-lookup"><span data-stu-id="89721-106">hello Web service can then be consumed in web sites, dashboards, and mobile apps.</span></span> 

<span data-ttu-id="89721-107">U maakt met behulp van Machine Learning modellen zijn meestal niet statisch.</span><span class="sxs-lookup"><span data-stu-id="89721-107">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="89721-108">Zodra er nieuwe gegevens beschikbaar of wanneer de consument Hallo Hallo API heeft moet hun eigen Hallo gegevensmodel toobe retrained.</span><span class="sxs-lookup"><span data-stu-id="89721-108">As new data becomes available or when hello consumer of hello API has their own data hello model needs toobe retrained.</span></span> 

<span data-ttu-id="89721-109">Retraining kan vaak optreden.</span><span class="sxs-lookup"><span data-stu-id="89721-109">Retraining may occur frequently.</span></span> <span data-ttu-id="89721-110">Met Hallo programmatische Retraining API-functie kunt u programmatisch opnieuw trainen via Hallo Retraining API's en update Hallo webservice met nieuwe getrainde model Hallo Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="89721-110">With hello Programmatic Retraining API feature, you can programmatically retrain hello model using hello Retraining APIs and update hello Web service with hello newly trained model.</span></span> 

<span data-ttu-id="89721-111">Dit document beschrijft Hallo retraining proces en ziet u hoe toouse Hallo Retraining API's.</span><span class="sxs-lookup"><span data-stu-id="89721-111">This document describes hello retraining process, and shows you how toouse hello Retraining APIs.</span></span>

## <a name="why-retrain-defining-hello-problem"></a><span data-ttu-id="89721-112">Waarom retrain: Hallo probleem definiëren</span><span class="sxs-lookup"><span data-stu-id="89721-112">Why retrain: defining hello problem</span></span>
<span data-ttu-id="89721-113">Een model wordt getraind met een verzameling van gegevens als onderdeel van Hallo machine learning training proces.</span><span class="sxs-lookup"><span data-stu-id="89721-113">As part of hello machine learning training process, a model is trained using a set of data.</span></span> <span data-ttu-id="89721-114">U maakt met behulp van Machine Learning modellen zijn meestal niet statisch.</span><span class="sxs-lookup"><span data-stu-id="89721-114">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="89721-115">Zodra er nieuwe gegevens beschikbaar of wanneer de consument Hallo Hallo API heeft moet hun eigen Hallo gegevensmodel toobe retrained.</span><span class="sxs-lookup"><span data-stu-id="89721-115">As new data becomes available or when hello consumer of hello API has their own data hello model needs toobe retrained.</span></span>

<span data-ttu-id="89721-116">In deze scenario's, een programmatische API biedt een handige manier tooallow u of Hallo consument van uw API's toocreate een client die u kunt op eenmalige of regelmatige basis retrain Hallo-model met hun eigen gegevens.</span><span class="sxs-lookup"><span data-stu-id="89721-116">In these scenarios, a programmatic API provides a convenient way tooallow you or hello consumer of your APIs toocreate a client that can, on a one-time or regular basis, retrain hello model using their own data.</span></span> <span data-ttu-id="89721-117">Vervolgens kunnen ze evalueren van de resultaten van de retraining Hallo en Hallo Web service API toouse Hallo zojuist getraind model bijwerken.</span><span class="sxs-lookup"><span data-stu-id="89721-117">They can then evaluate hello results of retraining, and update hello Web service API toouse hello newly trained model.</span></span>

> [!NOTE]
> <span data-ttu-id="89721-118">Als u een bestaande Trainingsexperiment en de nieuwe Web-service hebt, kunt u toocheck uit een bestaand voorspellende Web service in plaats van de volgende Hallo scenario vermeld in de volgende sectie Hallo Retrain.</span><span class="sxs-lookup"><span data-stu-id="89721-118">If you have an existing Training Experiment and New Web service, you may want toocheck out Retrain an existing Predictive Web service instead of following hello walkthrough mentioned in hello following section.</span></span>
> 
> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="89721-119">End-to-end werkstroom</span><span class="sxs-lookup"><span data-stu-id="89721-119">End-to-end workflow</span></span>
<span data-ttu-id="89721-120">Hallo proces omvat Hallo volgende onderdelen: een Trainingsexperiment en een Voorspellend Experiment gepubliceerd als een webservice.</span><span class="sxs-lookup"><span data-stu-id="89721-120">hello process involves hello following components: A Training Experiment and a Predictive Experiment published as a Web service.</span></span> <span data-ttu-id="89721-121">tooenable retraining van een getraind model Hallo Trainingsexperiment moet worden gepubliceerd als een webservice met Hallo-uitvoer van een getraind model.</span><span class="sxs-lookup"><span data-stu-id="89721-121">tooenable retraining of a trained model, hello Training Experiment must be published as a Web service with hello output of a trained model.</span></span> <span data-ttu-id="89721-122">Hierdoor API toegang toohello model voor retraining.</span><span class="sxs-lookup"><span data-stu-id="89721-122">This enables API access toohello model for retraining.</span></span> 

<span data-ttu-id="89721-123">Hallo stappen te volgen toepassing tooboth nieuw en klassieke Web services:</span><span class="sxs-lookup"><span data-stu-id="89721-123">hello following steps apply tooboth New and Classic Web services:</span></span>

<span data-ttu-id="89721-124">Hallo initiële voorspellende-webservice maken:</span><span class="sxs-lookup"><span data-stu-id="89721-124">Create hello initial Predictive Web service:</span></span>

* <span data-ttu-id="89721-125">Een trainingsexperiment maken</span><span class="sxs-lookup"><span data-stu-id="89721-125">Create a training experiment</span></span>
* <span data-ttu-id="89721-126">Een web Voorspellend experiment maken</span><span class="sxs-lookup"><span data-stu-id="89721-126">Create a predictive web experiment</span></span>
* <span data-ttu-id="89721-127">Een predictive webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="89721-127">Deploy a predictive web service</span></span>

<span data-ttu-id="89721-128">Opnieuw trainen Hallo-webservice:</span><span class="sxs-lookup"><span data-stu-id="89721-128">Retrain hello Web service:</span></span>

* <span data-ttu-id="89721-129">Training experiment tooallow voor retraining bijwerken</span><span class="sxs-lookup"><span data-stu-id="89721-129">Update training experiment tooallow for retraining</span></span>
* <span data-ttu-id="89721-130">Hallo retraining-webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="89721-130">Deploy hello retraining web service</span></span>
* <span data-ttu-id="89721-131">Hallo Batch-Service voor uitvoering van code tooretrain Hallo-model te gebruiken</span><span class="sxs-lookup"><span data-stu-id="89721-131">Use hello Batch Execution Service code tooretrain hello model</span></span>

<span data-ttu-id="89721-132">Zie voor een overzicht van de vorige stappen Hallo [Retrain Machine Learning-modellen programmatisch](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="89721-132">For a walkthrough of hello preceding steps, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="89721-133">toodeploy een nieuwe webservice die u moet voldoende machtigingen hebben in Hallo abonnement toowhich u Hallo-webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="89721-133">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="89721-134">Zie voor meer informatie, [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="89721-134">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="89721-135">Als u een klassieke webservice geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="89721-135">If you deployed a Classic Web Service:</span></span>

* <span data-ttu-id="89721-136">Een nieuw eindpunt op Hallo voorspellende webservice maken</span><span class="sxs-lookup"><span data-stu-id="89721-136">Create a new Endpoint on hello Predictive Web service</span></span>
* <span data-ttu-id="89721-137">Hallo PATCH URL's en code ophalen</span><span class="sxs-lookup"><span data-stu-id="89721-137">Get hello PATCH URL and code</span></span>
* <span data-ttu-id="89721-138">Gebruik Hallo PATCH URL toopoint Hallo nieuwe eindpunt op Hallo retrained model</span><span class="sxs-lookup"><span data-stu-id="89721-138">Use hello PATCH URL toopoint hello new Endpoint at hello retrained model</span></span> 

<span data-ttu-id="89721-139">Zie voor een overzicht van de vorige stappen Hallo [opnieuw trainen een klassieke webservice](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="89721-139">For a walkthrough of hello preceding steps, see [Retrain a Classic Web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="89721-140">Als u in een klassieke webservice retraining moeilijkheden uitvoert, Zie [probleemoplossing Hallo retraining van een Azure Machine Learning klassieke webservice](machine-learning-troubleshooting-retraining-models.md).</span><span class="sxs-lookup"><span data-stu-id="89721-140">If you run into difficulties retraining a Classic Web service, see [Troubleshooting hello retraining of an Azure Machine Learning Classic Web service](machine-learning-troubleshooting-retraining-models.md).</span></span>

<span data-ttu-id="89721-141">Als u een nieuwe webservice geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="89721-141">If you deployed a New Web service:</span></span>

* <span data-ttu-id="89721-142">Meld u aan tooyour Azure Resource Manager-account</span><span class="sxs-lookup"><span data-stu-id="89721-142">Sign in tooyour Azure Resource Manager account</span></span>
* <span data-ttu-id="89721-143">Hallo webservicedefinitie ophalen</span><span class="sxs-lookup"><span data-stu-id="89721-143">Get hello Web service definition</span></span>
* <span data-ttu-id="89721-144">Hallo webservicedefinitie exporteren als JSON</span><span class="sxs-lookup"><span data-stu-id="89721-144">Export hello Web Service Definition as JSON</span></span>
* <span data-ttu-id="89721-145">Hallo verwijzing toohello bijwerken `ilearner` blob in Hallo JSON</span><span class="sxs-lookup"><span data-stu-id="89721-145">Update hello reference toohello `ilearner` blob in hello JSON</span></span>
* <span data-ttu-id="89721-146">Hallo JSON importeren in de definitie van een Web-Service</span><span class="sxs-lookup"><span data-stu-id="89721-146">Import hello JSON into a Web Service Definition</span></span>
* <span data-ttu-id="89721-147">Hallo webservice bijwerken met definitie van een nieuwe Web-Service</span><span class="sxs-lookup"><span data-stu-id="89721-147">Update hello Web service with new Web Service Definition</span></span>

<span data-ttu-id="89721-148">Zie voor een overzicht van de vorige stappen Hallo [opnieuw trainen Hallo Machine Learning Management PowerShell-cmdlets met een nieuwe webservice](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="89721-148">For a walkthrough of hello preceding steps, see [Retrain a New Web service using hello Machine Learning Management PowerShell cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="89721-149">Hallo-proces voor het instellen van de retraining voor een klassieke webservice omvat Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="89721-149">hello process for setting up retraining for a Classic Web service involves hello following steps:</span></span>

![Overzicht van het proces retraining][1]

<span data-ttu-id="89721-151">Hallo-proces voor het instellen van de retraining voor een nieuwe webservice omvat Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="89721-151">hello process for setting up retraining for a New Web service involves hello following steps:</span></span>

![Overzicht van het proces retraining][7]

## <a name="other-resources"></a><span data-ttu-id="89721-153">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="89721-153">Other Resources</span></span>
* [<span data-ttu-id="89721-154">Retraining en bijwerken van Azure Machine Learning-modellen met Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="89721-154">Retraining and Updating Azure Machine Learning models with Azure Data Factory</span></span>](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)
* [<span data-ttu-id="89721-155">Groot aantal Machine Learning-modellen en web service-eindpunten maken van een experiment met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="89721-155">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>](machine-learning-create-models-and-endpoints-with-powershell.md)
* <span data-ttu-id="89721-156">Hallo [AML Retraining modellen met behulp van API's](https://www.youtube.com/watch?v=wwjglA8xllg) video ziet u hoe een Machine Learning-modellen tooretrain gemaakt in Azure Machine Learning met Hallo Retraining API's en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89721-156">hello [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) video shows you how tooretrain Machine Learning models created in Azure Machine Learning using hello Retraining APIs and PowerShell.</span></span>

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

