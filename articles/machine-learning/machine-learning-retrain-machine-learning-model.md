---
title: Opnieuw een Machine Learning-Model te trainen | Microsoft Docs
description: Informatie over het opnieuw een model te trainen en bijwerken van de webservice voor het gebruik van het zojuist getrainde model in Azure Machine Learning.
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
ms.openlocfilehash: f86c2bc41dd7ff0bc31454a56b84d136dc7d026c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-machine-learning-model"></a><span data-ttu-id="aedab-103">Opnieuw een Machine Learning-Model te trainen</span><span class="sxs-lookup"><span data-stu-id="aedab-103">Retrain a Machine Learning Model</span></span>
<span data-ttu-id="aedab-104">Het model is getraind en opgeslagen als onderdeel van het proces van uitoefening van machine learning-modellen in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="aedab-104">As part of the process of operationalization of machine learning models in Azure Machine Learning, your model is trained and saved.</span></span> <span data-ttu-id="aedab-105">U vervolgens worden gebruikt voor het maken van een predicative webservice.</span><span class="sxs-lookup"><span data-stu-id="aedab-105">You then use it to create a predicative Web service.</span></span> <span data-ttu-id="aedab-106">De webservice kan vervolgens worden gebruikt in websites, dashboards en mobiele apps.</span><span class="sxs-lookup"><span data-stu-id="aedab-106">The Web service can then be consumed in web sites, dashboards, and mobile apps.</span></span> 

<span data-ttu-id="aedab-107">U maakt met behulp van Machine Learning modellen zijn meestal niet statisch.</span><span class="sxs-lookup"><span data-stu-id="aedab-107">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="aedab-108">Zodra er nieuwe gegevens beschikbaar, of wanneer de gebruiker van de API hun eigen gegevens heeft moet het model worden retrained.</span><span class="sxs-lookup"><span data-stu-id="aedab-108">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span></span> 

<span data-ttu-id="aedab-109">Retraining kan vaak optreden.</span><span class="sxs-lookup"><span data-stu-id="aedab-109">Retraining may occur frequently.</span></span> <span data-ttu-id="aedab-110">Met de functie programmatische Retraining API kunt u programmatisch opnieuw trainen van het model met behulp van de Retraining API's en de webservice bijwerken met het nieuwe getrainde model.</span><span class="sxs-lookup"><span data-stu-id="aedab-110">With the Programmatic Retraining API feature, you can programmatically retrain the model using the Retraining APIs and update the Web service with the newly trained model.</span></span> 

<span data-ttu-id="aedab-111">Dit document worden de retraining beschreven en ziet u hoe de Retraining API's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aedab-111">This document describes the retraining process, and shows you how to use the Retraining APIs.</span></span>

## <a name="why-retrain-defining-the-problem"></a><span data-ttu-id="aedab-112">Waarom retrain: het probleem definiëren</span><span class="sxs-lookup"><span data-stu-id="aedab-112">Why retrain: defining the problem</span></span>
<span data-ttu-id="aedab-113">Een model wordt getraind met een verzameling van gegevens als onderdeel van de machine learning trainingsproces.</span><span class="sxs-lookup"><span data-stu-id="aedab-113">As part of the machine learning training process, a model is trained using a set of data.</span></span> <span data-ttu-id="aedab-114">U maakt met behulp van Machine Learning modellen zijn meestal niet statisch.</span><span class="sxs-lookup"><span data-stu-id="aedab-114">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="aedab-115">Zodra er nieuwe gegevens beschikbaar, of wanneer de gebruiker van de API hun eigen gegevens heeft moet het model worden retrained.</span><span class="sxs-lookup"><span data-stu-id="aedab-115">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span></span>

<span data-ttu-id="aedab-116">In deze scenario's biedt een programmatische API een handige manier waarmee u of de consument van uw API's voor het maken van een client die u kunt op eenmalige of regelmatige basis retrain het model met hun eigen gegevens.</span><span class="sxs-lookup"><span data-stu-id="aedab-116">In these scenarios, a programmatic API provides a convenient way to allow you or the consumer of your APIs to create a client that can, on a one-time or regular basis, retrain the model using their own data.</span></span> <span data-ttu-id="aedab-117">Vervolgens kunnen ze evalueren van de resultaten van de retraining en bijwerken van de Web service-API voor het gebruik van het zojuist getrainde model.</span><span class="sxs-lookup"><span data-stu-id="aedab-117">They can then evaluate the results of retraining, and update the Web service API to use the newly trained model.</span></span>

> [!NOTE]
> <span data-ttu-id="aedab-118">Hebt u een bestaande Trainingsexperiment en een nieuwe webservice, wilt u mogelijk Retrain uitchecken met een bestaande voorspellende webservice in plaats van na de procedure beschreven in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="aedab-118">If you have an existing Training Experiment and New Web service, you may want to check out Retrain an existing Predictive Web service instead of following the walkthrough mentioned in the following section.</span></span>
> 
> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="aedab-119">End-to-end werkstroom</span><span class="sxs-lookup"><span data-stu-id="aedab-119">End-to-end workflow</span></span>
<span data-ttu-id="aedab-120">Het proces omvat de volgende onderdelen: een Trainingsexperiment en een Voorspellend Experiment gepubliceerd als een webservice.</span><span class="sxs-lookup"><span data-stu-id="aedab-120">The process involves the following components: A Training Experiment and a Predictive Experiment published as a Web service.</span></span> <span data-ttu-id="aedab-121">Om in te schakelen van een getraind model retraining, moet het Experiment Training als een webservice met de uitvoer van een getraind model worden gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="aedab-121">To enable retraining of a trained model, the Training Experiment must be published as a Web service with the output of a trained model.</span></span> <span data-ttu-id="aedab-122">Hierdoor kan API-toegang in het model voor retraining.</span><span class="sxs-lookup"><span data-stu-id="aedab-122">This enables API access to the model for retraining.</span></span> 

<span data-ttu-id="aedab-123">De volgende stappen van toepassing op zowel nieuwe als klassieke Web services:</span><span class="sxs-lookup"><span data-stu-id="aedab-123">The following steps apply to both New and Classic Web services:</span></span>

<span data-ttu-id="aedab-124">De eerste voorspellende webservice maken:</span><span class="sxs-lookup"><span data-stu-id="aedab-124">Create the initial Predictive Web service:</span></span>

* <span data-ttu-id="aedab-125">Een trainingsexperiment maken</span><span class="sxs-lookup"><span data-stu-id="aedab-125">Create a training experiment</span></span>
* <span data-ttu-id="aedab-126">Een web Voorspellend experiment maken</span><span class="sxs-lookup"><span data-stu-id="aedab-126">Create a predictive web experiment</span></span>
* <span data-ttu-id="aedab-127">Een predictive webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="aedab-127">Deploy a predictive web service</span></span>

<span data-ttu-id="aedab-128">De webservice Retrain:</span><span class="sxs-lookup"><span data-stu-id="aedab-128">Retrain the Web service:</span></span>

* <span data-ttu-id="aedab-129">Trainingsexperiment om toe te staan voor de retraining bijwerken</span><span class="sxs-lookup"><span data-stu-id="aedab-129">Update training experiment to allow for retraining</span></span>
* <span data-ttu-id="aedab-130">De retraining-webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="aedab-130">Deploy the retraining web service</span></span>
* <span data-ttu-id="aedab-131">De Batch-Service voor uitvoering van code gebruiken voor het model opnieuw trainen</span><span class="sxs-lookup"><span data-stu-id="aedab-131">Use the Batch Execution Service code to retrain the model</span></span>

<span data-ttu-id="aedab-132">Zie voor een overzicht van de voorgaande stappen, [Retrain Machine Learning-modellen programmatisch](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="aedab-132">For a walkthrough of the preceding steps, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="aedab-133">Voor het implementeren van een nieuwe webservice moet u voldoende machtigingen hebben in het abonnement waaraan u de webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="aedab-133">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="aedab-134">Zie voor meer informatie, [beheren van een webservice via de portal voor Azure Machine Learning-webservices](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="aedab-134">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="aedab-135">Als u een klassieke webservice geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="aedab-135">If you deployed a Classic Web Service:</span></span>

* <span data-ttu-id="aedab-136">Een nieuw eindpunt op de voorspellende webservice maken</span><span class="sxs-lookup"><span data-stu-id="aedab-136">Create a new Endpoint on the Predictive Web service</span></span>
* <span data-ttu-id="aedab-137">De PATCH-URL en de code ophalen</span><span class="sxs-lookup"><span data-stu-id="aedab-137">Get the PATCH URL and code</span></span>
* <span data-ttu-id="aedab-138">De URL van de PATCH voor het nieuwe eindpunt het retrained model verwijzen gebruiken</span><span class="sxs-lookup"><span data-stu-id="aedab-138">Use the PATCH URL to point the new Endpoint at the retrained model</span></span> 

<span data-ttu-id="aedab-139">Zie voor een overzicht van de voorgaande stappen, [opnieuw trainen een klassieke webservice](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="aedab-139">For a walkthrough of the preceding steps, see [Retrain a Classic Web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="aedab-140">Als u in een klassieke webservice retraining moeilijkheden uitvoert, Zie [probleemoplossing retraining van een Azure Machine Learning klassieke webservice](machine-learning-troubleshooting-retraining-models.md).</span><span class="sxs-lookup"><span data-stu-id="aedab-140">If you run into difficulties retraining a Classic Web service, see [Troubleshooting the retraining of an Azure Machine Learning Classic Web service](machine-learning-troubleshooting-retraining-models.md).</span></span>

<span data-ttu-id="aedab-141">Als u een nieuwe webservice geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="aedab-141">If you deployed a New Web service:</span></span>

* <span data-ttu-id="aedab-142">Aanmelden bij uw account voor Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="aedab-142">Sign in to your Azure Resource Manager account</span></span>
* <span data-ttu-id="aedab-143">Definitie van de webservice ophalen</span><span class="sxs-lookup"><span data-stu-id="aedab-143">Get the Web service definition</span></span>
* <span data-ttu-id="aedab-144">Exporteren van de webservicedefinitie als JSON</span><span class="sxs-lookup"><span data-stu-id="aedab-144">Export the Web Service Definition as JSON</span></span>
* <span data-ttu-id="aedab-145">Bijwerken van de verwijzing naar de `ilearner` blob in de JSON</span><span class="sxs-lookup"><span data-stu-id="aedab-145">Update the reference to the `ilearner` blob in the JSON</span></span>
* <span data-ttu-id="aedab-146">De JSON importeren in de definitie van een Web-Service</span><span class="sxs-lookup"><span data-stu-id="aedab-146">Import the JSON into a Web Service Definition</span></span>
* <span data-ttu-id="aedab-147">De webservice bijwerken met definitie van een nieuwe Web-Service</span><span class="sxs-lookup"><span data-stu-id="aedab-147">Update the Web service with new Web Service Definition</span></span>

<span data-ttu-id="aedab-148">Zie voor een overzicht van de voorgaande stappen, [opnieuw trainen van de Machine Learning Management PowerShell-cmdlets met een nieuwe webservice](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="aedab-148">For a walkthrough of the preceding steps, see [Retrain a New Web service using the Machine Learning Management PowerShell cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="aedab-149">Het proces voor het instellen van de retraining voor een klassieke webservice omvat de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="aedab-149">The process for setting up retraining for a Classic Web service involves the following steps:</span></span>

![Overzicht van het proces retraining][1]

<span data-ttu-id="aedab-151">Het proces voor het instellen van de retraining voor een nieuwe Web-service omvat de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="aedab-151">The process for setting up retraining for a New Web service involves the following steps:</span></span>

![Overzicht van het proces retraining][7]

## <a name="other-resources"></a><span data-ttu-id="aedab-153">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="aedab-153">Other Resources</span></span>
* [<span data-ttu-id="aedab-154">Retraining en bijwerken van Azure Machine Learning-modellen met Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="aedab-154">Retraining and Updating Azure Machine Learning models with Azure Data Factory</span></span>](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)
* [<span data-ttu-id="aedab-155">Groot aantal Machine Learning-modellen en web service-eindpunten maken van een experiment met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="aedab-155">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>](machine-learning-create-models-and-endpoints-with-powershell.md)
* <span data-ttu-id="aedab-156">De [AML Retraining modellen met behulp van API's](https://www.youtube.com/watch?v=wwjglA8xllg) video ziet u hoe opnieuw trainen van Machine Learning-modellen in Azure Machine Learning gemaakt met behulp van de Retraining API's en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aedab-156">The [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) video shows you how to retrain Machine Learning models created in Azure Machine Learning using the Retraining APIs and PowerShell.</span></span>

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

