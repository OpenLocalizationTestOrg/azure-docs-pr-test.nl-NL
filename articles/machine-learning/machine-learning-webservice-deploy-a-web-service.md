---
title: een nieuwe webservice in Azure Machine Learning aaaDeploying | Microsoft Docs
description: Hallo-werkstroom voor het implementeren van een ARM gebaseerde webservice
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
redirect_document_id: True
ms.openlocfilehash: 2cbfda44b97a6b992fbdfdfb0c761e6c9e169035
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-new-web-service"></a><span data-ttu-id="73460-103">Een nieuwe webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="73460-103">Deploy a new web service</span></span>
<span data-ttu-id="73460-104">Microsoft Azure Machine learning-nu biedt webservices die zijn gebaseerd op [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) zodat voor nieuwe opties voor facturerings- en implementeren van uw web-service toomultiple regio's.</span><span class="sxs-lookup"><span data-stu-id="73460-104">Microsoft Azure Machine learning now provides web services that are based on [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) allowing for new billing plan options and deploying your web service toomultiple regions.</span></span>

<span data-ttu-id="73460-105">Hallo algemene werkstroom toodeploy Microsoft Azure Machine Learning-webservices met een webservice is:</span><span class="sxs-lookup"><span data-stu-id="73460-105">hello general workflow toodeploy a web service using Microsoft Azure Machine Learning Web Services is:</span></span>

* <span data-ttu-id="73460-106">Een Voorspellend experiment maken</span><span class="sxs-lookup"><span data-stu-id="73460-106">Create a predictive experiment</span></span>
* <span data-ttu-id="73460-107">Implementeren</span><span class="sxs-lookup"><span data-stu-id="73460-107">deploy it</span></span>
* <span data-ttu-id="73460-108">de naam ervan configureren</span><span class="sxs-lookup"><span data-stu-id="73460-108">configure its name</span></span>
* <span data-ttu-id="73460-109">abonnement</span><span class="sxs-lookup"><span data-stu-id="73460-109">billing plan</span></span>
* <span data-ttu-id="73460-110">Testen</span><span class="sxs-lookup"><span data-stu-id="73460-110">test it</span></span>
* <span data-ttu-id="73460-111">Deze wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="73460-111">consume it.</span></span>

<span data-ttu-id="73460-112">Hallo volgende afbeelding ziet u Hallo-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="73460-112">hello following graphic illustrates hello workflow.</span></span>

![Werkstroom voor de implementatie van Web service][1]

## <a name="deploy-web-service-from-studio"></a><span data-ttu-id="73460-114">Webservice implementeren vanuit Studio</span><span class="sxs-lookup"><span data-stu-id="73460-114">Deploy web service from Studio</span></span>
<span data-ttu-id="73460-115">toodeploy een experiment als een nieuwe webservice.</span><span class="sxs-lookup"><span data-stu-id="73460-115">toodeploy an experiment as a new web service.</span></span> <span data-ttu-id="73460-116">Meld u aan bij Hallo Machine Learning Studio en maak een nieuwe voorspellende webservice.</span><span class="sxs-lookup"><span data-stu-id="73460-116">Sign into hello Machine Learning Studio and create a new predictive web service.</span></span> 

<span data-ttu-id="73460-117">**Opmerking**: als u een experiment als een klassieke webservice al hebt geïmplementeerd u deze niet implementeren als een nieuwe webservice.</span><span class="sxs-lookup"><span data-stu-id="73460-117">**Note**: If you have already deployed an experiment as a classic web service you cannot deploy it as a new web service.</span></span>

<span data-ttu-id="73460-118">Klik op **uitvoeren** experimenteren canvas Hallo Hallo onderaan in en klik vervolgens op **webservice implementeren** en **Web Service implementeren [New]**.</span><span class="sxs-lookup"><span data-stu-id="73460-118">Click **Run** at hello bottom of hello experiment canvas and then click **Deploy Web Service** and **Deploy Web Service [New]**.</span></span> <span data-ttu-id="73460-119">Hallo implementatie pagina van Hallo Machine Learning Web Service manager wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="73460-119">hello deployment page of hello Machine Learning Web Service manager will open.</span></span>

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a><span data-ttu-id="73460-120">Machine Learning Web Service Manager Experiment pagina implementeren</span><span class="sxs-lookup"><span data-stu-id="73460-120">Machine Learning Web Service Manager Deploy Experiment Page</span></span>
<span data-ttu-id="73460-121">Voer een naam voor de webservice Hallo op Hallo implementeren Experiment pagina.</span><span class="sxs-lookup"><span data-stu-id="73460-121">On hello Deploy Experiment page, enter a name for hello web service.</span></span>
<span data-ttu-id="73460-122">Een prijscategorie selecteren.</span><span class="sxs-lookup"><span data-stu-id="73460-122">Select a pricing plan.</span></span> <span data-ttu-id="73460-123">Als u een bestaande prijsstelling dat kunt u dit hebt, moet anders u een nieuw plan prijs voor Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="73460-123">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for hello service.</span></span> 

1. <span data-ttu-id="73460-124">In Hallo **prijs Plan** vervolgkeuzelijst, selecteer een bestaand abonnement of Hallo **Selecteer nieuw plan** optie.</span><span class="sxs-lookup"><span data-stu-id="73460-124">In hello **Price Plan** drop down, select an existing plan or select hello **Select new plan** option.</span></span>
2. <span data-ttu-id="73460-125">In **naam**, typ een naam die wordt geïdentificeerd Hallo plan op uw factuur.</span><span class="sxs-lookup"><span data-stu-id="73460-125">In **Plan Name**, type a name that will identify hello plan on your bill.</span></span>
3. <span data-ttu-id="73460-126">Selecteer een van de Hallo **maandelijks plannen lagen**.</span><span class="sxs-lookup"><span data-stu-id="73460-126">Select one of hello **Monthly Plan Tiers**.</span></span> <span data-ttu-id="73460-127">Houd er rekening mee dat Hallo plan lagen standaard toohello plannen voor uw regio standaard en uw webservice geïmplementeerde toothat regio.</span><span class="sxs-lookup"><span data-stu-id="73460-127">Note that hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

<span data-ttu-id="73460-128">Klik op **implementeren** en Hallo Quick Start-pagina voor uw webservice wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="73460-128">Click **Deploy** and hello Quickstart page for your web service opens.</span></span>

## <a name="quickstart-page"></a><span data-ttu-id="73460-129">De pagina Quick Start</span><span class="sxs-lookup"><span data-stu-id="73460-129">Quickstart page</span></span>
<span data-ttu-id="73460-130">Hallo pagina Quick Start webservice biedt u toegang en richtlijnen op Hallo van de meest algemene taken die u na het maken van een nieuwe webservice wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="73460-130">hello web service Quickstart page gives you access and guidance on hello most common tasks you will perform after creating a new web service.</span></span> <span data-ttu-id="73460-131">Hier kunt u eenvoudig beide Hallo openen **Test** pagina en **verbruiken** pagina.</span><span class="sxs-lookup"><span data-stu-id="73460-131">From here you can easily access both hello **Test** page and **Consume** page.</span></span>

## <a name="testing-your-web-service"></a><span data-ttu-id="73460-132">Testen van uw web-service</span><span class="sxs-lookup"><span data-stu-id="73460-132">Testing your web service</span></span>
<span data-ttu-id="73460-133">Klik op Test webservice onder algemene taken Hallo Quick Start-pagina.</span><span class="sxs-lookup"><span data-stu-id="73460-133">From hello Quickstart page, click Test web service under common tasks.</span></span>   

<span data-ttu-id="73460-134">tootest Hallo-webservice als een aanvraag en antwoord-Service (RR's):</span><span class="sxs-lookup"><span data-stu-id="73460-134">tootest hello web service as a Request-Response Service (RRS):</span></span>

* <span data-ttu-id="73460-135">Klik op **Test** op de menubalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="73460-135">Click **Test** on hello menu bar.</span></span>
* <span data-ttu-id="73460-136">Klik op **aanvragen en antwoorden**.</span><span class="sxs-lookup"><span data-stu-id="73460-136">Click **Request-Response**.</span></span>
* <span data-ttu-id="73460-137">Waarden invoeren voor Hallo invoerkolommen van uw experiment.</span><span class="sxs-lookup"><span data-stu-id="73460-137">Enter appropriate values for hello input columns of your experiment.</span></span>
* <span data-ttu-id="73460-138">Klik op Test **aanvragen en antwoorden**.</span><span class="sxs-lookup"><span data-stu-id="73460-138">Click Test **Request-Response**.</span></span>

<span data-ttu-id="73460-139">U resultaten wordt weergegeven op Hallo de rechterzijde van Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="73460-139">You results will display on hello right hand side of hello page.</span></span>

<span data-ttu-id="73460-140">tootest een webservice Batch uitvoering Service (BES), gebruikt u een CSV-bestand:</span><span class="sxs-lookup"><span data-stu-id="73460-140">tootest a Batch Execution Service (BES) web service, you will use a CSV file:</span></span>

* <span data-ttu-id="73460-141">Klik op **Test** op de menubalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="73460-141">Click **Test** on hello menu bar.</span></span>
* <span data-ttu-id="73460-142">Klik op **Batch**.</span><span class="sxs-lookup"><span data-stu-id="73460-142">Click **Batch**.</span></span>
* <span data-ttu-id="73460-143">Klik op Bladeren en navigeer tooyour voorbeeldgegevensbestand onder uw invoer.</span><span class="sxs-lookup"><span data-stu-id="73460-143">Under your input, click Browse and navigate tooyour sample data file.</span></span>
* <span data-ttu-id="73460-144">Klik op **Test**.</span><span class="sxs-lookup"><span data-stu-id="73460-144">Click **Test**.</span></span>

<span data-ttu-id="73460-145">Hallo-status van de test wordt weergegeven onder **batchtaken testen**.</span><span class="sxs-lookup"><span data-stu-id="73460-145">hello status of your test is displayed under **Test Batch Jobs**.</span></span>

## <a name="consuming-your-web-service"></a><span data-ttu-id="73460-146">Uw Web-Service gebruiken</span><span class="sxs-lookup"><span data-stu-id="73460-146">Consuming your Web Service</span></span>
<span data-ttu-id="73460-147">Wanneer dit wordt geïmplementeerd als een webservice, bevatten Azure Machine Learning-experimenten een REST-API die kan worden gebruikt door een breed scala aan apparaten en platforms.</span><span class="sxs-lookup"><span data-stu-id="73460-147">When deployed as a web service, Azure Machine Learning experiments provide a REST API that can be consumed by a wide range of devices and platforms.</span></span> <span data-ttu-id="73460-148">Dit is omdat Hallo eenvoudige REST-API accepteert en reageert met JSON-indeling berichten.</span><span class="sxs-lookup"><span data-stu-id="73460-148">This is because hello simple REST API accepts and responds with JSON formatted messages.</span></span> <span data-ttu-id="73460-149">Hello Azure Machine Learning-portal biedt code die kan worden gebruikt toocall Hallo-webservice in R, C# en Python.</span><span class="sxs-lookup"><span data-stu-id="73460-149">hello Azure Machine Learning portal provides code that can be used toocall hello web service in R, C#, and Python.</span></span>

<span data-ttu-id="73460-150">U kunt op Hallo verbruik pagina zoeken:</span><span class="sxs-lookup"><span data-stu-id="73460-150">On hello Consuming page you can find:</span></span>

* <span data-ttu-id="73460-151">Hallo API-sleutel en URI's voor het verbruik van de webservice in apps.</span><span class="sxs-lookup"><span data-stu-id="73460-151">hello API key and URI's for consuming web service in apps.</span></span>
* <span data-ttu-id="73460-152">Excel en web-app sjablonen tookick start het proces van uw verbruik.</span><span class="sxs-lookup"><span data-stu-id="73460-152">Excel and web app templates tookick start your consumption process.</span></span>
* <span data-ttu-id="73460-153">Voorbeeldcode in C#, python en R tooget gestart.</span><span class="sxs-lookup"><span data-stu-id="73460-153">Sample code in C#, python, and R tooget you started.</span></span>

<span data-ttu-id="73460-154">Zie voor meer informatie over het gebruiken van webservices [hoe een Azure Machine Learning-webservice tooconsume](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="73460-154">For more information on consuming web services, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="73460-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="73460-155">Next Steps</span></span>
<span data-ttu-id="73460-156">Zie voor meer informatie over het gebruiken van web-services:</span><span class="sxs-lookup"><span data-stu-id="73460-156">For more information on consuming web services, see:</span></span>

[<span data-ttu-id="73460-157">Hoe tooconsume een Azure Machine Learning-webservice</span><span class="sxs-lookup"><span data-stu-id="73460-157">How tooconsume an Azure Machine Learning Web service</span></span>](machine-learning-consume-web-services.md)

[<span data-ttu-id="73460-158">Azure Machine Learning-webservices: De implementatie en het verbruik</span><span class="sxs-lookup"><span data-stu-id="73460-158">Azure Machine Learning Web Services: Deployment and consumption</span></span>](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
