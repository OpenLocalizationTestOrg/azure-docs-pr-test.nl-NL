---
title: aaaHow tooconsume een Azure Machine Learning-webservice | Microsoft Docs
description: "Zodra een machine learning-service is geïmplementeerd, kan Hallo RESTFul-webservice die beschikbaar wordt gesteld worden gebruikt als realtime aanvragen en antwoorden service of als een batch-service kan worden uitgevoerd."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 804f8211-9437-4982-98e9-ca841b7edf56
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: 19095604169e5af1daed12c17ba66258233178bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconsume-an-azure-machine-learning-web-service"></a><span data-ttu-id="97f55-103">Hoe tooconsume een Azure Machine Learning-webservice</span><span class="sxs-lookup"><span data-stu-id="97f55-103">How tooconsume an Azure Machine Learning Web service</span></span>

<span data-ttu-id="97f55-104">Wanneer u een Azure Machine Learning Voorspellend model als een webservice implementeert, kunt u een REST-API-toosend gebruiken deze gegevens en get voorspellingen.</span><span class="sxs-lookup"><span data-stu-id="97f55-104">Once you deploy an Azure Machine Learning predictive model as a Web service, you can use a REST API toosend it data and get predictions.</span></span> <span data-ttu-id="97f55-105">U kunt hello gegevens verzenden in realtime of in de batchmodus.</span><span class="sxs-lookup"><span data-stu-id="97f55-105">You can send hello data in real-time or in batch mode.</span></span>

<span data-ttu-id="97f55-106">U vindt meer informatie over het toocreate en implementeren van een Machine Learning-webservice met Machine Learning Studio hier:</span><span class="sxs-lookup"><span data-stu-id="97f55-106">You can find more information about how toocreate and deploy a Machine Learning Web service using Machine Learning Studio here:</span></span>

* <span data-ttu-id="97f55-107">Voor een zelfstudie over hoe toocreate een experiment in Machine Learning Studio, Zie [uw eerste experiment maken](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="97f55-107">For a tutorial on how toocreate an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="97f55-108">Voor meer informatie over het toodeploy een webservice, Zie [een Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="97f55-108">For details on how toodeploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="97f55-109">Bezoek voor meer informatie over Machine Learning in het algemeen Hallo [Machine Learning-documentatiecentrum](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="97f55-109">For more information about Machine Learning in general, visit hello [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a><span data-ttu-id="97f55-110">Overzicht</span><span class="sxs-lookup"><span data-stu-id="97f55-110">Overview</span></span>
<span data-ttu-id="97f55-111">Hello Azure Machine Learning-webservice communiceert een externe toepassing met een Machine Learning werkstroom score-model in realtime.</span><span class="sxs-lookup"><span data-stu-id="97f55-111">With hello Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="97f55-112">Aanroep van een Machine Learning-webservice retourneert voorspelling resultaten tooan externe toepassing.</span><span class="sxs-lookup"><span data-stu-id="97f55-112">A Machine Learning Web service call returns prediction results tooan external application.</span></span> <span data-ttu-id="97f55-113">toomake aanroep van een Machine Learning-webservice, geeft u een API-sleutel die wordt gemaakt bij het implementeren van een voorspelling.</span><span class="sxs-lookup"><span data-stu-id="97f55-113">toomake a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="97f55-114">Hallo Machine Learning-webservice is gebaseerd op REST, een populaire architectuur keuze voor web programming projecten.</span><span class="sxs-lookup"><span data-stu-id="97f55-114">hello Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="97f55-115">Azure Machine Learning heeft twee soorten services:</span><span class="sxs-lookup"><span data-stu-id="97f55-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="97f55-116">Aanvraag en antwoord-Service (RSS) – een lage latentie en zeer schaalbare service die voorziet in een interface toohello staatloze modellen gemaakt en geïmplementeerd vanuit Hallo Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="97f55-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface toohello stateless models created and deployed from hello Machine Learning Studio.</span></span>
* <span data-ttu-id="97f55-117">Batch uitvoering-Service (BES) – een asynchrone service die scores per batch voor records met gegevens.</span><span class="sxs-lookup"><span data-stu-id="97f55-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="97f55-118">Zie voor meer informatie over Machine Learning-webservices [een Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="97f55-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="97f55-119">Een Azure Machine Learning-autorisatie-sleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="97f55-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="97f55-120">Wanneer u uw experiment implementeert, wordt API-sleutels worden gegenereerd voor Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="97f55-120">When you deploy your experiment, API keys are generated for hello Web service.</span></span> <span data-ttu-id="97f55-121">U kunt Hallo-sleutels ophalen vanaf verschillende locaties.</span><span class="sxs-lookup"><span data-stu-id="97f55-121">You can retrieve hello keys from several locations.</span></span>

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="97f55-122">Vanuit Hallo-portal voor Microsoft Azure Machine Learning-webservices</span><span class="sxs-lookup"><span data-stu-id="97f55-122">From hello Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="97f55-123">Meld u aan toohello [Microsoft Azure Machine Learning-webservices](https://services.azureml.net) portal.</span><span class="sxs-lookup"><span data-stu-id="97f55-123">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="97f55-124">tooretrieve hello API-sleutel voor een nieuwe Machine-Learning-webservice:</span><span class="sxs-lookup"><span data-stu-id="97f55-124">tooretrieve hello API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="97f55-125">Klik in hello Azure Machine Learning-webservices portal op **webservices** Hallo bovenste menu.</span><span class="sxs-lookup"><span data-stu-id="97f55-125">In hello Azure Machine Learning Web Services portal, click **Web Services** hello top menu.</span></span>
2. <span data-ttu-id="97f55-126">Klik op waarvoor u tooretrieve Hallo sleutel wilt Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="97f55-126">Click hello Web service for which you want tooretrieve hello key.</span></span>
3. <span data-ttu-id="97f55-127">Klik op het bovenste menu Hallo **verbruiken**.</span><span class="sxs-lookup"><span data-stu-id="97f55-127">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="97f55-128">Kopiëren en opslaan van Hallo **primaire sleutel**.</span><span class="sxs-lookup"><span data-stu-id="97f55-128">Copy and save hello **Primary Key**.</span></span>

<span data-ttu-id="97f55-129">tooretrieve hello API-sleutel voor een klassieke Machine-Learning-webservice:</span><span class="sxs-lookup"><span data-stu-id="97f55-129">tooretrieve hello API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="97f55-130">Klik in hello Azure Machine Learning-webservices portal op **klassieke webservices** Hallo bovenste menu.</span><span class="sxs-lookup"><span data-stu-id="97f55-130">In hello Azure Machine Learning Web Services portal, click **Classic Web Services** hello top menu.</span></span>
2. <span data-ttu-id="97f55-131">Klik op Hallo webservice waarmee u werkt.</span><span class="sxs-lookup"><span data-stu-id="97f55-131">Click hello Web service with which you are working.</span></span>
3. <span data-ttu-id="97f55-132">Klik op waarvoor u tooretrieve Hallo sleutel wilt Hallo-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="97f55-132">Click hello endpoint for which you want tooretrieve hello key.</span></span>
4. <span data-ttu-id="97f55-133">Klik op het bovenste menu Hallo **verbruiken**.</span><span class="sxs-lookup"><span data-stu-id="97f55-133">On hello top menu, click **Consume**.</span></span>
5. <span data-ttu-id="97f55-134">Kopiëren en opslaan van Hallo **primaire sleutel**.</span><span class="sxs-lookup"><span data-stu-id="97f55-134">Copy and save hello **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="97f55-135">Klassieke-webservice</span><span class="sxs-lookup"><span data-stu-id="97f55-135">Classic Web service</span></span>
 <span data-ttu-id="97f55-136">U kunt ook een sleutel voor een klassieke webservice ophalen van Machine Learning Studio of Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="97f55-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or hello Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="97f55-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="97f55-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="97f55-138">Klik in Machine Learning Studio **WEBSERVICES** op Hallo links.</span><span class="sxs-lookup"><span data-stu-id="97f55-138">In Machine Learning Studio, click **WEB SERVICES** on hello left.</span></span>
2. <span data-ttu-id="97f55-139">Klik op een webservice.</span><span class="sxs-lookup"><span data-stu-id="97f55-139">Click a Web service.</span></span> <span data-ttu-id="97f55-140">Hallo **API-sleutel** is op Hallo **DASHBOARD** tabblad.</span><span class="sxs-lookup"><span data-stu-id="97f55-140">hello **API key** is on hello **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="97f55-141">Klassieke Azure-portal</span><span class="sxs-lookup"><span data-stu-id="97f55-141">Azure classic portal</span></span>
1. <span data-ttu-id="97f55-142">Klik op **MACHINE LEARNING** op Hallo links.</span><span class="sxs-lookup"><span data-stu-id="97f55-142">Click **MACHINE LEARNING** on hello left.</span></span>
2. <span data-ttu-id="97f55-143">Klik op Hallo werkruimte waarin uw Web-service zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="97f55-143">Click hello workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="97f55-144">Klik op **WEBSERVICES**.</span><span class="sxs-lookup"><span data-stu-id="97f55-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="97f55-145">Klik op een webservice.</span><span class="sxs-lookup"><span data-stu-id="97f55-145">Click a Web service.</span></span>
5. <span data-ttu-id="97f55-146">Klik op een eindpunt.</span><span class="sxs-lookup"><span data-stu-id="97f55-146">Click an endpoint.</span></span> <span data-ttu-id="97f55-147">Hallo 'API KEY' loopt Hallo rechtsonder.</span><span class="sxs-lookup"><span data-stu-id="97f55-147">hello “API KEY” is down at hello lower-right.</span></span>

## <span data-ttu-id="97f55-148"><a id="connect"></a>Verbinding maken met tooa Machine Learning-webservice</span><span class="sxs-lookup"><span data-stu-id="97f55-148"><a id="connect"></a>Connect tooa Machine Learning Web service</span></span>
<span data-ttu-id="97f55-149">U kunt tooa Machine Learning-webservice met behulp van elke programmeertaal die ondersteuning biedt voor HTTP-aanvraag en antwoord verbinden.</span><span class="sxs-lookup"><span data-stu-id="97f55-149">You can connect tooa Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="97f55-150">U kunt de voorbeelden in C#, Python en R weergeven van een help-pagina Machine Learning-webservice.</span><span class="sxs-lookup"><span data-stu-id="97f55-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="97f55-151">**Machine Learning API help** Machine Learning API help wordt gemaakt wanneer u een webservice implementeert.</span><span class="sxs-lookup"><span data-stu-id="97f55-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="97f55-152">Zie [overzicht van Azure Machine Learning - webservice implementeren](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="97f55-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="97f55-153">Hallo Machine Learning API help bevat details over een voorspelling webservice.</span><span class="sxs-lookup"><span data-stu-id="97f55-153">hello Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="97f55-154">Klik op Hallo webservice waarmee u werkt.</span><span class="sxs-lookup"><span data-stu-id="97f55-154">Click hello Web service with which you are working.</span></span>
2. <span data-ttu-id="97f55-155">Klik op Hallo eindpunt waarvoor u wilt dat tooview Hallo API Help-pagina.</span><span class="sxs-lookup"><span data-stu-id="97f55-155">Click hello endpoint for which you want tooview hello API Help Page.</span></span>
3. <span data-ttu-id="97f55-156">Klik op het bovenste menu Hallo **verbruiken**.</span><span class="sxs-lookup"><span data-stu-id="97f55-156">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="97f55-157">Klik op **API help-pagina** onder Hallo aanvragen en antwoorden of Batchuitvoering eindpunten.</span><span class="sxs-lookup"><span data-stu-id="97f55-157">Click **API help page** under either hello Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="97f55-158">**tooview Machine Learning API help voor een nieuwe webservice**</span><span class="sxs-lookup"><span data-stu-id="97f55-158">**tooview Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="97f55-159">Hallo in Azure Machine Learning Web Services-Portal:</span><span class="sxs-lookup"><span data-stu-id="97f55-159">In hello Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="97f55-160">Klik op **WEBSERVICES** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="97f55-160">Click **WEB SERVICES** on hello top menu.</span></span>
2. <span data-ttu-id="97f55-161">Klik op waarvoor u tooretrieve Hallo sleutel wilt Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="97f55-161">Click hello Web service for which you want tooretrieve hello key.</span></span>

<span data-ttu-id="97f55-162">Klik op **verbruiken** tooget hello URI's voor Hallo aanvraag Reposonse en Batch uitvoering Services en voorbeeld-code in C#, R en Python.</span><span class="sxs-lookup"><span data-stu-id="97f55-162">Click **Consume** tooget hello URIs for hello Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="97f55-163">Klik op **Swagger API** tooget Swagger op basis van de documentatie voor Hallo API vanuit Hallo aangeroepen opgegeven URI's.</span><span class="sxs-lookup"><span data-stu-id="97f55-163">Click **Swagger API** tooget Swagger based documentation for hello APIs called from hello supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="97f55-164">C#-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="97f55-164">C# Sample</span></span>
<span data-ttu-id="97f55-165">Gebruik tooconnect tooa Machine Learning-webservice, een **HttpClient** ScoreData wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="97f55-165">tooconnect tooa Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="97f55-166">ScoreData bevat een FeatureVector, een n-dimensionale vector van numerieke functies die Hallo ScoreData vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="97f55-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="97f55-167">U verifiëren toohello Machine Learning-service met een API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="97f55-167">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="97f55-168">tooconnect tooa Machine Learning-webservice, Hallo **Microsoft.AspNet.WebApi.Client** NuGet-pakket moet worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="97f55-168">tooconnect tooa Machine Learning Web service, hello **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="97f55-169">**Microsoft.AspNet.WebApi.Client NuGet in Visual Studio installeren**</span><span class="sxs-lookup"><span data-stu-id="97f55-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="97f55-170">Hallo downloaden gegevensset van UCI publiceren: volwassenen 2 klasse gegevensset Web Service.</span><span class="sxs-lookup"><span data-stu-id="97f55-170">Publish hello Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="97f55-171">Klik op **Hulpprogramma's** > **NuGet Package Manager** > **Package Manager-console**.</span><span class="sxs-lookup"><span data-stu-id="97f55-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="97f55-172">Kies **Install-pakket Microsoft.AspNet.WebApi.Client**.</span><span class="sxs-lookup"><span data-stu-id="97f55-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="97f55-173">**toorun Hallo-codevoorbeeld**</span><span class="sxs-lookup"><span data-stu-id="97f55-173">**toorun hello code sample**</span></span>

1. <span data-ttu-id="97f55-174">Publiceren ' voorbeeld 1: gegevensset downloaden van UCI: volwassene 2 klasse gegevensset ' experiment, deel van Hallo Machine Learning voorbeeld verzameling.</span><span class="sxs-lookup"><span data-stu-id="97f55-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="97f55-175">Wijs apiKey met Hallo sleutel van een webservice.</span><span class="sxs-lookup"><span data-stu-id="97f55-175">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="97f55-176">Zie **ophalen van een Azure Machine Learning-autorisatiesleutel** hierboven.</span><span class="sxs-lookup"><span data-stu-id="97f55-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="97f55-177">Wijs serviceUri Hello aanvraag-URI.</span><span class="sxs-lookup"><span data-stu-id="97f55-177">Assign serviceUri with hello Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="97f55-178">Python-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="97f55-178">Python Sample</span></span>
<span data-ttu-id="97f55-179">tooconnect tooa Machine Learning-webservice, gebruik Hallo **urllib2** bibliotheek ScoreData wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="97f55-179">tooconnect tooa Machine Learning Web service, use hello **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="97f55-180">ScoreData bevat een FeatureVector, een n-dimensionale vector van numerieke functies die Hallo ScoreData vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="97f55-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="97f55-181">U verifiëren toohello Machine Learning-service met een API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="97f55-181">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="97f55-182">**toorun Hallo-codevoorbeeld**</span><span class="sxs-lookup"><span data-stu-id="97f55-182">**toorun hello code sample**</span></span>

1. <span data-ttu-id="97f55-183">Implementeren ' voorbeeld 1: gegevensset downloaden van UCI: volwassene 2 klasse gegevensset ' experiment, deel van Hallo Machine Learning voorbeeld verzameling.</span><span class="sxs-lookup"><span data-stu-id="97f55-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="97f55-184">Wijs apiKey met Hallo sleutel van een webservice.</span><span class="sxs-lookup"><span data-stu-id="97f55-184">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="97f55-185">Zie Hallo **ophalen van een Azure Machine Learning-autorisatiesleutel** sectie bijna Hallo begin van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="97f55-185">See hello **Get an Azure Machine Learning authorization key** section near hello beginning of this article.</span></span>
3. <span data-ttu-id="97f55-186">Wijs serviceUri Hello aanvraag-URI.</span><span class="sxs-lookup"><span data-stu-id="97f55-186">Assign serviceUri with hello Request URI.</span></span>

