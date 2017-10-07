---
title: Parameters voor Azure Machine Learning Web Service aaaUse | Microsoft Docs
description: Hoe Hallo toouse Azure Machine Learning Webserviceparameters toomodify gedrag van uw model wanneer Hallo-webservice wordt geopend.
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c49187db-b976-4731-89d6-11a0bf653db1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2017
ms.author: raymondl;garye
ms.openlocfilehash: 214711eb819a6cea34db905abdf015da11e846d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-web-service-parameters"></a><span data-ttu-id="b0c7c-103">Parameters voor Azure Machine Learning-webservice</span><span class="sxs-lookup"><span data-stu-id="b0c7c-103">Use Azure Machine Learning Web Service Parameters</span></span>
<span data-ttu-id="b0c7c-104">Een Azure Machine Learning-webservice wordt gemaakt door het publiceren van een experiment die modules met configureerbare parameters bevat.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-104">An Azure Machine Learning web service is created by publishing an experiment that contains modules with configurable parameters.</span></span> <span data-ttu-id="b0c7c-105">In sommige gevallen kunt u toochange Hallo module gedrag tijdens het Hallo-webservice wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-105">In some cases, you may want toochange hello module behavior while hello web service is running.</span></span> <span data-ttu-id="b0c7c-106">*Web-Service Parameters* kunt u toodo deze taak.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-106">*Web Service Parameters* allow you toodo this task.</span></span> 

<span data-ttu-id="b0c7c-107">Een veelvoorkomend voorbeeld tot stand brengen van Hallo [importgegevens] [ reader] module dus die gebruiker Hallo Hallo gepubliceerd web-service een andere gegevensbron kunt opgeven wanneer Hallo-webservice wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-107">A common example is setting up hello [Import Data][reader] module so that hello user of hello published web service can specify a different data source when hello web service is accessed.</span></span> <span data-ttu-id="b0c7c-108">Of het configureren van Hallo [gegevens exporteren] [ writer] module zodat een andere bestemming kan worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-108">Or configuring hello [Export Data][writer] module so that a different destination can be specified.</span></span> <span data-ttu-id="b0c7c-109">Enkele andere voorbeelden zijn als u het aantal bits voor Hallo Hallo [hash-functie] [ feature-hashing] module of Hallo aantal gewenste functies voor Hallo [Functieselectie op basis van het Filter] [ filter-based-feature-selection] module.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-109">Some other examples include changing hello number of bits for hello [Feature Hashing][feature-hashing] module or hello number of desired features for hello [Filter-Based Feature Selection][filter-based-feature-selection] module.</span></span> 

<span data-ttu-id="b0c7c-110">U kunt de Parameters van de Web-Service en koppel deze aan een of meer moduleparameters in uw experiment en kunt u opgeven of ze vereist of optioneel zijn.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-110">You can set Web Service Parameters and associate them with one or more module parameters in your experiment, and you can specify whether they are required or optional.</span></span> <span data-ttu-id="b0c7c-111">gebruiker van de webservice Hallo Hallo kunt vervolgens waarden opgeven voor deze parameters wanneer ze Hallo-webservice aanroept.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-111">hello user of hello web service can then provide values for these parameters when they call hello web service.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-tooset-and-use-web-service-parameters"></a><span data-ttu-id="b0c7c-112">Hoe tooset en gebruik Webserviceparameters</span><span class="sxs-lookup"><span data-stu-id="b0c7c-112">How tooset and use Web Service Parameters</span></span>
<span data-ttu-id="b0c7c-113">U definieert u een Web Service-Parameter op Hallo pictogram volgende toohello-parameter voor een module en selecteer 'Instellen als web Serviceparameter'.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-113">You define a Web Service Parameter by clicking hello icon next toohello parameter for a module and selecting "Set as web service parameter".</span></span> <span data-ttu-id="b0c7c-114">Hiermee maakt u een nieuwe Web Service-Parameter en toothat module parameter is verbonden.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-114">This creates a new Web Service Parameter and connects it toothat module parameter.</span></span> <span data-ttu-id="b0c7c-115">Vervolgens als Hallo-webservice wordt geopend, Hallo-gebruiker kan een waarde voor Hallo Web Service Parameter opgeven en het toegepaste toohello module parameter is.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-115">Then, when hello web service is accessed, hello user can specify a value for hello Web Service Parameter and it is applied toohello module parameter.</span></span>

<span data-ttu-id="b0c7c-116">Als u een Parameter van Web Service definieert, is beschikbaar tooany andere module-parameter in Hallo-experiment.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-116">Once you define a Web Service Parameter, it's available tooany other module parameter in hello experiment.</span></span> <span data-ttu-id="b0c7c-117">Als u een Web Service-Parameter die is gekoppeld aan een parameter voor één module definieert, kunt u die dezelfde Web Service-Parameter voor module, zolang Hallo parameter Hallo dezelfde waarde soort verwacht.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-117">If you define a Web Service Parameter associated with a parameter for one module, you can use that same Web Service Parameter for any other module, as long as hello parameter expects hello same type of value.</span></span> <span data-ttu-id="b0c7c-118">Bijvoorbeeld, als Hallo Web Service Parameter een numerieke waarde is, kan klikt u vervolgens alleen worden gebruikt voor de parameters van de module die een numerieke waarde verwacht.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-118">For example, if hello Web Service Parameter is a numeric value, then it can only be used for module parameters that expect a numeric value.</span></span> <span data-ttu-id="b0c7c-119">Wanneer het Hallo-gebruiker een waarde voor Hallo Web Service Parameter wordt ingesteld, zal de parameters van de module toegepaste tooall die zijn gekoppeld zijn.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-119">When hello user sets a value for hello Web Service Parameter, it will be applied tooall associated module parameters.</span></span>

<span data-ttu-id="b0c7c-120">U kunt bepalen of een standaard tooprovide waarde voor Hallo Web Service-Parameter.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-120">You can decide whether tooprovide a default value for hello Web Service Parameter.</span></span> <span data-ttu-id="b0c7c-121">Als u dit doet, klikt u vervolgens Hallo is parameter optioneel voor gebruiker Hallo van Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-121">If you do, then hello parameter is optional for hello user of hello web service.</span></span> <span data-ttu-id="b0c7c-122">Als u een standaardwaarde niet opgeeft, is Hallo gebruiker vereist tooenter een waarde wanneer Hallo-webservice wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-122">If you don't provide a default value, then hello user is required tooenter a value when hello web service is accessed.</span></span>

<span data-ttu-id="b0c7c-123">Hallo API-documentatie voor de webservice Hallo bevat informatie voor Hallo web servicegebruiker op hoe toospecify Hallo Web Service Parameter programmatisch bij het openen van Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-123">hello API documentation for hello web service includes information for hello web service user on how toospecify hello Web Service Parameter programmatically when accessing hello web service.</span></span>

> [!NOTE]
> <span data-ttu-id="b0c7c-124">Hallo API-documentatie voor een klassieke webservice is opgegeven via Hallo **API help-pagina** koppeling in de webservice Hallo **DASHBOARD** in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-124">hello API documentation for a classic web service is provided through hello **API help page** link in hello web service **DASHBOARD** in Machine Learning Studio.</span></span> <span data-ttu-id="b0c7c-125">Hallo API-documentatie voor een nieuwe webservice is opgegeven via Hallo [Azure Machine Learning-webservices](https://services.azureml.net/Quickstart) portal op Hallo **verbruiken** en **Swagger API** pagina's voor uw Web-service.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-125">hello API documentation for a new web service is provided through hello [Azure Machine Learning Web Services](https://services.azureml.net/Quickstart) portal on hello **Consume** and **Swagger API** pages for your web service.</span></span>
> 
> 

## <a name="example"></a><span data-ttu-id="b0c7c-126">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b0c7c-126">Example</span></span>
<span data-ttu-id="b0c7c-127">Een voorbeeld: Stel hebben we een experiment met een [gegevens exporteren] [ writer] module die u informatie tooAzure blob-opslag verzendt.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-127">As an example, let's assume we have an experiment with an [Export Data][writer] module that sends information tooAzure blob storage.</span></span> <span data-ttu-id="b0c7c-128">Definiëren we Web Service Parameter met de naam 'Blob-pad' waarmee Hallo web service gebruiker toochange Hallo pad toohello blobopslag wanneer Hallo-service wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-128">We'll define a Web Service Parameter named "Blob path" that allows hello web service user toochange hello path toohello blob storage when hello service is accessed.</span></span>

1. <span data-ttu-id="b0c7c-129">Klik op Hallo in Machine Learning Studio [gegevens exporteren] [ writer] module tooselect deze.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-129">In Machine Learning Studio, click hello [Export Data][writer] module tooselect it.</span></span> <span data-ttu-id="b0c7c-130">De eigenschappen worden weergegeven in Hallo eigenschappen deelvenster toohello rechts van het experimentcanvas Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-130">Its properties are shown in hello Properties pane toohello right of hello experiment canvas.</span></span>
2. <span data-ttu-id="b0c7c-131">Geef Hallo opslagtype:</span><span class="sxs-lookup"><span data-stu-id="b0c7c-131">Specify hello storage type:</span></span>
   
   * <span data-ttu-id="b0c7c-132">Onder **Geef gegevensbestemming**, selecteert u 'Azure Blob Storage'.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-132">Under **Please specify data destination**, select "Azure Blob Storage".</span></span>
   * <span data-ttu-id="b0c7c-133">Onder **Geef verificatietype**, selecteert u 'Account'.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-133">Under **Please specify authentication type**, select "Account".</span></span>
   * <span data-ttu-id="b0c7c-134">Geef gegevens op Hallo voor hello Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-134">Enter hello account information for hello Azure blob storage.</span></span> 
     <p /><span data-ttu-id="b0c7c-135">
3.Klik op Hallo pictogram toohello rechts van Hallo **pad tooblob die begint met de parameter container**.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-135">
3. Click hello icon toohello right of hello **Path tooblob beginning with container parameter**.</span></span> <span data-ttu-id="b0c7c-136">Als volgt uitziet:</span><span class="sxs-lookup"><span data-stu-id="b0c7c-136">It looks like this:</span></span>
   
   ![Web Service Parameter-pictogram][icon]
   
   <span data-ttu-id="b0c7c-138">Selecteer 'Instellen als web Serviceparameter'.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-138">Select "Set as web service parameter".</span></span>
   
   <span data-ttu-id="b0c7c-139">Een item wordt toegevoegd onder **Webserviceparameters** Hallo Hallo eigenschappendeelvenster waarvan Hallo 'pad tooblob begint met container' onderaan in.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-139">An entry is added under **Web Service Parameters** at hello bottom of hello Properties pane with hello name "Path tooblob beginning with container".</span></span> <span data-ttu-id="b0c7c-140">Dit Hallo Web Service-Parameter die is nu is gekoppeld aan dit [gegevens exporteren] [ writer] module-parameter.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-140">This is hello Web Service Parameter that is now associated with this [Export Data][writer] module parameter.</span></span>
4. <span data-ttu-id="b0c7c-141">toorename Hallo Web Service Parameter, klikt u op naam hello, voer 'Blob-pad' en druk op Hallo **Enter** sleutel.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-141">toorename hello Web Service Parameter, click hello name, enter "Blob path", and press hello **Enter** key.</span></span> 
5. <span data-ttu-id="b0c7c-142">tooprovide een standaardwaarde voor Hallo Web Service-Parameter, klikt u op Hallo pictogram toohello rechts van het Hallo-naam, selecteer 'Provide standaardwaarde', voer een waarde (bijvoorbeeld ' container1/output1.csv') en druk op Hallo **Enter** sleutel.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-142">tooprovide a default value for hello Web Service Parameter, click hello icon toohello right of hello name, select "Provide default value", enter a value (for example, "container1/output1.csv"), and press hello **Enter** key.</span></span>
   
   ![Web Service-Parameter][parameter]
6. <span data-ttu-id="b0c7c-144">Klik op **Run**.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-144">Click **Run**.</span></span> 
7. <span data-ttu-id="b0c7c-145">Klik op **webservice implementeren** en selecteer **webservice implementeren [klassieke]** of **Web Service implementeren [New]** toodeploy Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-145">Click **Deploy Web Service** and select **Deploy Web Service [Classic]** or **Deploy Web Service [New]** toodeploy hello web service.</span></span>

> [!NOTE] 
> <span data-ttu-id="b0c7c-146">toodeploy een nieuwe webservice die u moet voldoende machtigingen hebben in Hallo abonnement toowhich u Hallo-webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-146">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="b0c7c-147">Zie voor meer informatie, [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="b0c7c-147">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="b0c7c-148">gebruiker van de webservice Hallo Hallo kunt nu een nieuwe bestemming voor Hallo opgeven [gegevens exporteren] [ writer] module bij het openen van Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="b0c7c-148">hello user of hello web service can now specify a new destination for hello [Export Data][writer] module when accessing hello web service.</span></span>

## <a name="more-information"></a><span data-ttu-id="b0c7c-149">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="b0c7c-149">More information</span></span>
<span data-ttu-id="b0c7c-150">Zie voor een uitgebreider voorbeeld Hallo [Webserviceparameters](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) vermelding in Hallo [Machine Learning Blog](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0c7c-150">For a more detailed example, see hello [Web Service Parameters](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) entry in hello [Machine Learning Blog](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).</span></span>

<span data-ttu-id="b0c7c-151">Zie voor meer informatie over de toegang tot een Machine Learning-webservice [hoe een Azure Machine Learning-webservice tooconsume](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="b0c7c-151">For more information on accessing a Machine Learning web service, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

<!-- Images -->
[icon]: ./media/machine-learning-web-service-parameters/icon.png
[parameter]: ./media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/

