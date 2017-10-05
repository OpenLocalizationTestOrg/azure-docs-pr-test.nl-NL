---
title: Een nieuwe webservice in Azure Machine Learning implementeren | Microsoft Docs
description: De werkstroom voor het implementeren van een ARM gebaseerde webservice
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: a358b04f-0d08-4d50-820e-eeac971854cf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: v-donglo
ROBOTS: NOINDEX
redirect_url: machine-learning-publish-a-machine-learning-web-service
redirect_document_id: TRUE
ms.openlocfilehash: 1415709f9da2bb2cce859af9feb0ec15c1fa5801
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-new-web-service"></a><span data-ttu-id="0a701-103">Een nieuwe webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="0a701-103">Deploy a new web service</span></span>
<span data-ttu-id="0a701-104">Microsoft Azure Machine learning-nu biedt webservices die zijn gebaseerd op [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) waardoor het nieuwe plan opties facturering en uw webservice implementeren in meerdere regio's.</span><span class="sxs-lookup"><span data-stu-id="0a701-104">Microsoft Azure Machine learning now provides web services that are based on [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) allowing for new billing plan options and deploying your web service to multiple regions.</span></span>

<span data-ttu-id="0a701-105">De algemene werkstroom voor het implementeren van een webservice met behulp van Microsoft Azure Machine Learning-webservices is:</span><span class="sxs-lookup"><span data-stu-id="0a701-105">The general workflow to deploy a web service using Microsoft Azure Machine Learning Web Services is:</span></span>

* <span data-ttu-id="0a701-106">Een Voorspellend experiment maken</span><span class="sxs-lookup"><span data-stu-id="0a701-106">Create a predictive experiment</span></span>
* <span data-ttu-id="0a701-107">Implementeren</span><span class="sxs-lookup"><span data-stu-id="0a701-107">deploy it</span></span>
* <span data-ttu-id="0a701-108">de naam ervan configureren</span><span class="sxs-lookup"><span data-stu-id="0a701-108">configure its name</span></span>
* <span data-ttu-id="0a701-109">abonnement</span><span class="sxs-lookup"><span data-stu-id="0a701-109">billing plan</span></span>
* <span data-ttu-id="0a701-110">Testen</span><span class="sxs-lookup"><span data-stu-id="0a701-110">test it</span></span>
* <span data-ttu-id="0a701-111">Deze wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0a701-111">consume it.</span></span>

<span data-ttu-id="0a701-112">De volgende afbeelding ziet u de werkstroom.</span><span class="sxs-lookup"><span data-stu-id="0a701-112">The following graphic illustrates the workflow.</span></span>

![Werkstroom voor de implementatie van Web service][1]

## <a name="deploy-web-service-from-studio"></a><span data-ttu-id="0a701-114">Webservice implementeren vanuit Studio</span><span class="sxs-lookup"><span data-stu-id="0a701-114">Deploy web service from Studio</span></span>
<span data-ttu-id="0a701-115">Voor het implementeren van een experiment als een nieuwe webservice.</span><span class="sxs-lookup"><span data-stu-id="0a701-115">To deploy an experiment as a new web service.</span></span> <span data-ttu-id="0a701-116">Meld u aan bij de Machine Learning Studio en maak een nieuwe voorspellende webservice.</span><span class="sxs-lookup"><span data-stu-id="0a701-116">Sign into the Machine Learning Studio and create a new predictive web service.</span></span> 

<span data-ttu-id="0a701-117">**Opmerking**: als u een experiment als een klassieke webservice al hebt geïmplementeerd u deze niet implementeren als een nieuwe webservice.</span><span class="sxs-lookup"><span data-stu-id="0a701-117">**Note**: If you have already deployed an experiment as a classic web service you cannot deploy it as a new web service.</span></span>

<span data-ttu-id="0a701-118">Klik op **uitvoeren** aan de onderkant van het experiment canvas en klik vervolgens op **webservice implementeren** en **Web Service implementeren [New]**.</span><span class="sxs-lookup"><span data-stu-id="0a701-118">Click **Run** at the bottom of the experiment canvas and then click **Deploy Web Service** and **Deploy Web Service [New]**.</span></span> <span data-ttu-id="0a701-119">De pagina implementatie van de Machine Learning Web Service manager wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="0a701-119">The deployment page of the Machine Learning Web Service manager will open.</span></span>

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a><span data-ttu-id="0a701-120">Machine Learning Web Service Manager Experiment pagina implementeren</span><span class="sxs-lookup"><span data-stu-id="0a701-120">Machine Learning Web Service Manager Deploy Experiment Page</span></span>
<span data-ttu-id="0a701-121">Voer een naam voor de web-service op de pagina Experiment implementeren.</span><span class="sxs-lookup"><span data-stu-id="0a701-121">On the Deploy Experiment page, enter a name for the web service.</span></span>
<span data-ttu-id="0a701-122">Een prijscategorie selecteren.</span><span class="sxs-lookup"><span data-stu-id="0a701-122">Select a pricing plan.</span></span> <span data-ttu-id="0a701-123">Als u een bestaande prijsstelling dat kunt u dit hebt, moet anders u een nieuw plan prijs voor de service.</span><span class="sxs-lookup"><span data-stu-id="0a701-123">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for the service.</span></span> 

1. <span data-ttu-id="0a701-124">In de **prijs Plan** vervolgkeuzelijst, selecteer een bestaande planning of Selecteer de **Selecteer nieuw plan** optie.</span><span class="sxs-lookup"><span data-stu-id="0a701-124">In the **Price Plan** drop down, select an existing plan or select the **Select new plan** option.</span></span>
2. <span data-ttu-id="0a701-125">In **naam**, typ een naam waarmee het plan op uw factuur wordt geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="0a701-125">In **Plan Name**, type a name that will identify the plan on your bill.</span></span>
3. <span data-ttu-id="0a701-126">Selecteer een van de **maandelijks plannen lagen**.</span><span class="sxs-lookup"><span data-stu-id="0a701-126">Select one of the **Monthly Plan Tiers**.</span></span> <span data-ttu-id="0a701-127">Houd er rekening mee dat de standaardwaarde van de lagen abonnement op de plannen voor uw regio standaard en uw web-service wordt geïmplementeerd naar deze regio.</span><span class="sxs-lookup"><span data-stu-id="0a701-127">Note that the plan tiers default to the plans for your default region and your web service is deployed to that region.</span></span>

<span data-ttu-id="0a701-128">Klik op **implementeren** en de pagina Quick Start voor uw webservice wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="0a701-128">Click **Deploy** and the Quickstart page for your web service opens.</span></span>

## <a name="quickstart-page"></a><span data-ttu-id="0a701-129">De pagina Quick Start</span><span class="sxs-lookup"><span data-stu-id="0a701-129">Quickstart page</span></span>
<span data-ttu-id="0a701-130">De pagina Quick Start webservice biedt u toegang en richtlijnen op de meest algemene taken die u uitvoeren wilt na het maken van een nieuwe webservice.</span><span class="sxs-lookup"><span data-stu-id="0a701-130">The web service Quickstart page gives you access and guidance on the most common tasks you will perform after creating a new web service.</span></span> <span data-ttu-id="0a701-131">Vanaf hier u kunt eenvoudig toegang tot zowel de **Test** pagina en **verbruiken** pagina.</span><span class="sxs-lookup"><span data-stu-id="0a701-131">From here you can easily access both the **Test** page and **Consume** page.</span></span>

## <a name="testing-your-web-service"></a><span data-ttu-id="0a701-132">Testen van uw web-service</span><span class="sxs-lookup"><span data-stu-id="0a701-132">Testing your web service</span></span>
<span data-ttu-id="0a701-133">Klik op Test webservice onder algemene taken van de pagina Quick Start.</span><span class="sxs-lookup"><span data-stu-id="0a701-133">From the Quickstart page, click Test web service under common tasks.</span></span>   

<span data-ttu-id="0a701-134">Als een aanvraag en antwoord-Service (RR's) voor de webservice testen:</span><span class="sxs-lookup"><span data-stu-id="0a701-134">To test the web service as a Request-Response Service (RRS):</span></span>

* <span data-ttu-id="0a701-135">Klik op **Test** op de menubalk.</span><span class="sxs-lookup"><span data-stu-id="0a701-135">Click **Test** on the menu bar.</span></span>
* <span data-ttu-id="0a701-136">Klik op **aanvragen en antwoorden**.</span><span class="sxs-lookup"><span data-stu-id="0a701-136">Click **Request-Response**.</span></span>
* <span data-ttu-id="0a701-137">Voer de juiste waarden voor de invoerkolommen van uw experiment.</span><span class="sxs-lookup"><span data-stu-id="0a701-137">Enter appropriate values for the input columns of your experiment.</span></span>
* <span data-ttu-id="0a701-138">Klik op Test **aanvragen en antwoorden**.</span><span class="sxs-lookup"><span data-stu-id="0a701-138">Click Test **Request-Response**.</span></span>

<span data-ttu-id="0a701-139">U resultaten wilt weergeven aan de rechterkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="0a701-139">You results will display on the right hand side of the page.</span></span>

<span data-ttu-id="0a701-140">Als u wilt een webservice Batch uitvoering Service (BES) testen, gebruikt u een CSV-bestand:</span><span class="sxs-lookup"><span data-stu-id="0a701-140">To test a Batch Execution Service (BES) web service, you will use a CSV file:</span></span>

* <span data-ttu-id="0a701-141">Klik op **Test** op de menubalk.</span><span class="sxs-lookup"><span data-stu-id="0a701-141">Click **Test** on the menu bar.</span></span>
* <span data-ttu-id="0a701-142">Klik op **Batch**.</span><span class="sxs-lookup"><span data-stu-id="0a701-142">Click **Batch**.</span></span>
* <span data-ttu-id="0a701-143">Klik op Bladeren en navigeer naar uw voorbeeldgegevensbestand onder uw invoer.</span><span class="sxs-lookup"><span data-stu-id="0a701-143">Under your input, click Browse and navigate to your sample data file.</span></span>
* <span data-ttu-id="0a701-144">Klik op **Test**.</span><span class="sxs-lookup"><span data-stu-id="0a701-144">Click **Test**.</span></span>

<span data-ttu-id="0a701-145">De status van de test wordt weergegeven onder **batchtaken testen**.</span><span class="sxs-lookup"><span data-stu-id="0a701-145">The status of your test is displayed under **Test Batch Jobs**.</span></span>

## <a name="consuming-your-web-service"></a><span data-ttu-id="0a701-146">Uw Web-Service gebruiken</span><span class="sxs-lookup"><span data-stu-id="0a701-146">Consuming your Web Service</span></span>
<span data-ttu-id="0a701-147">Wanneer dit wordt geïmplementeerd als een webservice, bevatten Azure Machine Learning-experimenten een REST-API die kan worden gebruikt door een breed scala aan apparaten en platforms.</span><span class="sxs-lookup"><span data-stu-id="0a701-147">When deployed as a web service, Azure Machine Learning experiments provide a REST API that can be consumed by a wide range of devices and platforms.</span></span> <span data-ttu-id="0a701-148">Dit komt doordat eenvoudige REST-API accepteert en reageert met JSON-indeling berichten.</span><span class="sxs-lookup"><span data-stu-id="0a701-148">This is because the simple REST API accepts and responds with JSON formatted messages.</span></span> <span data-ttu-id="0a701-149">De Azure Machine Learning-portal biedt code die kan worden gebruikt voor het aanroepen van de webservice in R, C# en Python.</span><span class="sxs-lookup"><span data-stu-id="0a701-149">The Azure Machine Learning portal provides code that can be used to call the web service in R, C#, and Python.</span></span>

<span data-ttu-id="0a701-150">U kunt op de pagina verbruik vinden:</span><span class="sxs-lookup"><span data-stu-id="0a701-150">On the Consuming page you can find:</span></span>

* <span data-ttu-id="0a701-151">De API-sleutel en de URI's voor het verbruik van de webservice in apps.</span><span class="sxs-lookup"><span data-stu-id="0a701-151">The API key and URI's for consuming web service in apps.</span></span>
* <span data-ttu-id="0a701-152">Excel en web-app sjablonen Activeer starten uw verbruik-proces.</span><span class="sxs-lookup"><span data-stu-id="0a701-152">Excel and web app templates to kick start your consumption process.</span></span>
* <span data-ttu-id="0a701-153">De voorbeeldcode in C#, python en R u op weg.</span><span class="sxs-lookup"><span data-stu-id="0a701-153">Sample code in C#, python, and R to get you started.</span></span>

<span data-ttu-id="0a701-154">Zie voor meer informatie over het gebruiken van webservices [gebruiken van een Azure Machine Learning-webservice](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="0a701-154">For more information on consuming web services, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a701-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0a701-155">Next Steps</span></span>
<span data-ttu-id="0a701-156">Zie voor meer informatie over het gebruiken van web-services:</span><span class="sxs-lookup"><span data-stu-id="0a701-156">For more information on consuming web services, see:</span></span>

[<span data-ttu-id="0a701-157">Een Azure Machine Learning-webservice gebruiken</span><span class="sxs-lookup"><span data-stu-id="0a701-157">How to consume an Azure Machine Learning Web service</span></span>](machine-learning-consume-web-services.md)

[<span data-ttu-id="0a701-158">Azure Machine Learning-webservices: De implementatie en het verbruik</span><span class="sxs-lookup"><span data-stu-id="0a701-158">Azure Machine Learning Web Services: Deployment and consumption</span></span>](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
