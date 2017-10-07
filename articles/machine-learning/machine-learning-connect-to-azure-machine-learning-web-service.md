---
title: aaaConnect tooa Machine Learning-webservice | Microsoft Docs
description: Verbinding met C# of Python, tooan Azure Machine Learning Web service met behulp van een autorisatiesleutel.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 59b07bab-b60f-48c4-a385-a162e50ec7c2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: garye
ROBOTS: NOINDEX
redirect_url: machine-learning-consume-web-services
redirect_document_id: True
ms.openlocfilehash: 0108e71e30a05539a8c0ee93d5aadb07e3d1efa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-machine-learning-web-service"></a><span data-ttu-id="eb672-103">Verbinding maken met tooan Azure Machine Learning-webservice</span><span class="sxs-lookup"><span data-stu-id="eb672-103">Connect tooan Azure Machine Learning Web Service</span></span>
<span data-ttu-id="eb672-104">Hallo ontwikkelaarservaring Azure Machine Learning is een voorspellingen Web service API toomake invoergegevens in realtime of in de batchmodus.</span><span class="sxs-lookup"><span data-stu-id="eb672-104">hello Azure Machine Learning developer experience is a Web service API toomake predictions from input data in real time or in batch mode.</span></span> <span data-ttu-id="eb672-105">U gebruikt Azure Machine Learning Studio toocreate voorspellingen en implementeren van een Azure Machine Learning-webservice.</span><span class="sxs-lookup"><span data-stu-id="eb672-105">You use Azure Machine Learning Studio toocreate predictions and deploy an Azure Machine Learning Web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="eb672-106">toolearn over het toocreate en implementeren van een Machine Learning-webservice met behulp van Machine Learning Studio:</span><span class="sxs-lookup"><span data-stu-id="eb672-106">toolearn about how toocreate and deploy a Machine Learning Web service using Machine Learning Studio:</span></span>

* <span data-ttu-id="eb672-107">Voor een zelfstudie over hoe toocreate een experiment in Machine Learning Studio, Zie [uw eerste experiment maken](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="eb672-107">For a tutorial on how toocreate an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="eb672-108">Voor meer informatie over het toodeploy een webservice, Zie [een Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="eb672-108">For details on how toodeploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="eb672-109">Bezoek voor meer informatie over Machine Learning in het algemeen Hallo [Machine Learning-documentatiecentrum](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="eb672-109">For more information about Machine Learning in general, visit hello [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

## <a name="azure-machine-learning-web-service"></a><span data-ttu-id="eb672-110">Azure Machine Learning-webservice</span><span class="sxs-lookup"><span data-stu-id="eb672-110">Azure Machine Learning Web service</span></span>
<span data-ttu-id="eb672-111">Hello Azure Machine Learning-webservice communiceert een externe toepassing met een Machine Learning werkstroom score-model in realtime.</span><span class="sxs-lookup"><span data-stu-id="eb672-111">With hello Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="eb672-112">Aanroep van een Machine Learning-webservice retourneert voorspelling resultaten tooan externe toepassing.</span><span class="sxs-lookup"><span data-stu-id="eb672-112">A Machine Learning Web service call returns prediction results tooan external application.</span></span> <span data-ttu-id="eb672-113">toomake aanroep van een Machine Learning-webservice, geeft u een API-sleutel die wordt gemaakt bij het implementeren van een voorspelling.</span><span class="sxs-lookup"><span data-stu-id="eb672-113">toomake a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="eb672-114">Hallo Machine Learning-webservice is gebaseerd op REST, een populaire architectuur keuze voor web programming projecten.</span><span class="sxs-lookup"><span data-stu-id="eb672-114">hello Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="eb672-115">Azure Machine Learning heeft twee soorten services:</span><span class="sxs-lookup"><span data-stu-id="eb672-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="eb672-116">Aanvraag en antwoord-Service (RSS) – een lage latentie en zeer schaalbare service die voorziet in een interface toohello staatloze modellen gemaakt en geïmplementeerd vanuit Hallo Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="eb672-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface toohello stateless models created and deployed from hello Machine Learning Studio.</span></span>
* <span data-ttu-id="eb672-117">Batch uitvoering-Service (BES) – een asynchrone service die scores per batch voor records met gegevens.</span><span class="sxs-lookup"><span data-stu-id="eb672-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="eb672-118">Zie voor meer informatie over Machine Learning-webservices [een Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="eb672-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="eb672-119">Een Azure Machine Learning-autorisatie-sleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="eb672-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="eb672-120">Wanneer u uw experiment implementeert, wordt API-sleutels worden gegenereerd voor Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="eb672-120">When you deploy your experiment, API keys are generated for hello Web service.</span></span> <span data-ttu-id="eb672-121">U kunt Hallo-sleutels ophalen vanaf verschillende locaties.</span><span class="sxs-lookup"><span data-stu-id="eb672-121">You can retrieve hello keys from several locations.</span></span>

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="eb672-122">Vanuit Hallo-portal voor Microsoft Azure Machine Learning-webservices</span><span class="sxs-lookup"><span data-stu-id="eb672-122">From hello Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="eb672-123">Meld u aan toohello [Microsoft Azure Machine Learning-webservices](https://services.azureml.net) portal.</span><span class="sxs-lookup"><span data-stu-id="eb672-123">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="eb672-124">tooretrieve hello API-sleutel voor een nieuwe Machine-Learning-webservice:</span><span class="sxs-lookup"><span data-stu-id="eb672-124">tooretrieve hello API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="eb672-125">Klik in hello Azure Machine Learning-webservices portal op **webservices** Hallo bovenste menu.</span><span class="sxs-lookup"><span data-stu-id="eb672-125">In hello Azure Machine Learning Web Services portal, click **Web Services** hello top menu.</span></span>
2. <span data-ttu-id="eb672-126">Klik op waarvoor u tooretrieve Hallo sleutel wilt Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="eb672-126">Click hello Web service for which you want tooretrieve hello key.</span></span>
3. <span data-ttu-id="eb672-127">Klik op het bovenste menu Hallo **verbruiken**.</span><span class="sxs-lookup"><span data-stu-id="eb672-127">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="eb672-128">Kopiëren en opslaan van Hallo **primaire sleutel**.</span><span class="sxs-lookup"><span data-stu-id="eb672-128">Copy and save hello **Primary Key**.</span></span>

<span data-ttu-id="eb672-129">tooretrieve hello API-sleutel voor een klassieke Machine-Learning-webservice:</span><span class="sxs-lookup"><span data-stu-id="eb672-129">tooretrieve hello API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="eb672-130">Klik in hello Azure Machine Learning-webservices portal op **klassieke webservices** Hallo bovenste menu.</span><span class="sxs-lookup"><span data-stu-id="eb672-130">In hello Azure Machine Learning Web Services portal, click **Classic Web Services** hello top menu.</span></span>
2. <span data-ttu-id="eb672-131">Klik op Hallo webservice waarmee u werkt.</span><span class="sxs-lookup"><span data-stu-id="eb672-131">Click hello Web service with which you are working.</span></span>
3. <span data-ttu-id="eb672-132">Klik op waarvoor u tooretrieve Hallo sleutel wilt Hallo-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="eb672-132">Click hello endpoint for which you want tooretrieve hello key.</span></span>
4. <span data-ttu-id="eb672-133">Klik op het bovenste menu Hallo **verbruiken**.</span><span class="sxs-lookup"><span data-stu-id="eb672-133">On hello top menu, click **Consume**.</span></span>
5. <span data-ttu-id="eb672-134">Kopiëren en opslaan van Hallo **primaire sleutel**.</span><span class="sxs-lookup"><span data-stu-id="eb672-134">Copy and save hello **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="eb672-135">Klassieke-webservice</span><span class="sxs-lookup"><span data-stu-id="eb672-135">Classic Web service</span></span>
 <span data-ttu-id="eb672-136">U kunt ook een sleutel voor een klassieke webservice ophalen van Machine Learning Studio of Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="eb672-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or hello Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="eb672-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="eb672-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="eb672-138">Klik in Machine Learning Studio **WEBSERVICES** op Hallo links.</span><span class="sxs-lookup"><span data-stu-id="eb672-138">In Machine Learning Studio, click **WEB SERVICES** on hello left.</span></span>
2. <span data-ttu-id="eb672-139">Klik op een webservice.</span><span class="sxs-lookup"><span data-stu-id="eb672-139">Click a Web service.</span></span> <span data-ttu-id="eb672-140">Hallo **API-sleutel** is op Hallo **DASHBOARD** tabblad.</span><span class="sxs-lookup"><span data-stu-id="eb672-140">hello **API key** is on hello **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="eb672-141">Klassieke Azure-portal</span><span class="sxs-lookup"><span data-stu-id="eb672-141">Azure classic portal</span></span>
1. <span data-ttu-id="eb672-142">Klik op **MACHINE LEARNING** op Hallo links.</span><span class="sxs-lookup"><span data-stu-id="eb672-142">Click **MACHINE LEARNING** on hello left.</span></span>
2. <span data-ttu-id="eb672-143">Klik op Hallo werkruimte waarin uw Web-service zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="eb672-143">Click hello workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="eb672-144">Klik op **WEBSERVICES**.</span><span class="sxs-lookup"><span data-stu-id="eb672-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="eb672-145">Klik op een webservice.</span><span class="sxs-lookup"><span data-stu-id="eb672-145">Click a Web service.</span></span>
5. <span data-ttu-id="eb672-146">Klik op een eindpunt.</span><span class="sxs-lookup"><span data-stu-id="eb672-146">Click an endpoint.</span></span> <span data-ttu-id="eb672-147">Hallo 'API KEY' loopt Hallo rechtsonder.</span><span class="sxs-lookup"><span data-stu-id="eb672-147">hello “API KEY” is down at hello lower-right.</span></span>

## <span data-ttu-id="eb672-148"><a id="connect"></a>Verbinding maken met tooa Machine Learning-webservice</span><span class="sxs-lookup"><span data-stu-id="eb672-148"><a id="connect"></a>Connect tooa Machine Learning Web service</span></span>
<span data-ttu-id="eb672-149">U kunt tooa Machine Learning-webservice met behulp van elke programmeertaal die ondersteuning biedt voor HTTP-aanvraag en antwoord verbinden.</span><span class="sxs-lookup"><span data-stu-id="eb672-149">You can connect tooa Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="eb672-150">U kunt de voorbeelden in C#, Python en R weergeven van een help-pagina Machine Learning-webservice.</span><span class="sxs-lookup"><span data-stu-id="eb672-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="eb672-151">**Machine Learning API help** Machine Learning API help wordt gemaakt wanneer u een webservice implementeert.</span><span class="sxs-lookup"><span data-stu-id="eb672-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="eb672-152">Zie [overzicht van Azure Machine Learning - webservice implementeren](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="eb672-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="eb672-153">Hallo Machine Learning API help bevat details over een voorspelling webservice.</span><span class="sxs-lookup"><span data-stu-id="eb672-153">hello Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="eb672-154">Klik op Hallo webservice waarmee u werkt.</span><span class="sxs-lookup"><span data-stu-id="eb672-154">Click hello Web service with which you are working.</span></span>
2. <span data-ttu-id="eb672-155">Klik op Hallo eindpunt waarvoor u wilt dat tooview Hallo API Help-pagina.</span><span class="sxs-lookup"><span data-stu-id="eb672-155">Click hello endpoint for which you want tooview hello API Help Page.</span></span>
3. <span data-ttu-id="eb672-156">Klik op het bovenste menu Hallo **verbruiken**.</span><span class="sxs-lookup"><span data-stu-id="eb672-156">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="eb672-157">Klik op **API help-pagina** onder Hallo aanvragen en antwoorden of Batchuitvoering eindpunten.</span><span class="sxs-lookup"><span data-stu-id="eb672-157">Click **API help page** under either hello Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="eb672-158">**tooview Machine Learning API help voor een nieuwe webservice**</span><span class="sxs-lookup"><span data-stu-id="eb672-158">**tooview Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="eb672-159">Hallo in Azure Machine Learning Web Services-Portal:</span><span class="sxs-lookup"><span data-stu-id="eb672-159">In hello Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="eb672-160">Klik op **WEBSERVICES** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="eb672-160">Click **WEB SERVICES** on hello top menu.</span></span>
2. <span data-ttu-id="eb672-161">Klik op waarvoor u tooretrieve Hallo sleutel wilt Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="eb672-161">Click hello Web service for which you want tooretrieve hello key.</span></span>

<span data-ttu-id="eb672-162">Klik op **verbruiken** tooget hello URI's voor Hallo aanvraag Reposonse en Batch uitvoering Services en voorbeeld-code in C#, R en Python.</span><span class="sxs-lookup"><span data-stu-id="eb672-162">Click **Consume** tooget hello URIs for hello Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="eb672-163">Klik op **Swagger API** tooget Swagger op basis van de documentatie voor Hallo API vanuit Hallo aangeroepen opgegeven URI's.</span><span class="sxs-lookup"><span data-stu-id="eb672-163">Click **Swagger API** tooget Swagger based documentation for hello APIs called from hello supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="eb672-164">C#-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="eb672-164">C# Sample</span></span>
<span data-ttu-id="eb672-165">Gebruik tooconnect tooa Machine Learning-webservice, een **HttpClient** ScoreData wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="eb672-165">tooconnect tooa Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="eb672-166">ScoreData bevat een FeatureVector, een n-dimensionale vector van numerieke functies die Hallo ScoreData vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="eb672-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="eb672-167">U verifiëren toohello Machine Learning-service met een API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="eb672-167">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="eb672-168">tooconnect tooa Machine Learning-webservice, Hallo **Microsoft.AspNet.WebApi.Client** NuGet-pakket moet worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="eb672-168">tooconnect tooa Machine Learning Web service, hello **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="eb672-169">**Microsoft.AspNet.WebApi.Client NuGet in Visual Studio installeren**</span><span class="sxs-lookup"><span data-stu-id="eb672-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="eb672-170">Hallo downloaden gegevensset van UCI publiceren: volwassenen 2 klasse gegevensset Web Service.</span><span class="sxs-lookup"><span data-stu-id="eb672-170">Publish hello Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="eb672-171">Klik op **Hulpprogramma's** > **NuGet Package Manager** > **Package Manager-console**.</span><span class="sxs-lookup"><span data-stu-id="eb672-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="eb672-172">Kies **Install-pakket Microsoft.AspNet.WebApi.Client**.</span><span class="sxs-lookup"><span data-stu-id="eb672-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="eb672-173">**toorun Hallo-codevoorbeeld**</span><span class="sxs-lookup"><span data-stu-id="eb672-173">**toorun hello code sample**</span></span>

1. <span data-ttu-id="eb672-174">Publiceren ' voorbeeld 1: gegevensset downloaden van UCI: volwassene 2 klasse gegevensset ' experiment, deel van Hallo Machine Learning voorbeeld verzameling.</span><span class="sxs-lookup"><span data-stu-id="eb672-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="eb672-175">Wijs apiKey met Hallo sleutel van een webservice.</span><span class="sxs-lookup"><span data-stu-id="eb672-175">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="eb672-176">Zie **ophalen van een Azure Machine Learning-autorisatiesleutel** hierboven.</span><span class="sxs-lookup"><span data-stu-id="eb672-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="eb672-177">Wijs serviceUri Hello aanvraag-URI.</span><span class="sxs-lookup"><span data-stu-id="eb672-177">Assign serviceUri with hello Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="eb672-178">Python-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="eb672-178">Python Sample</span></span>
<span data-ttu-id="eb672-179">tooconnect tooa Machine Learning-webservice, gebruik Hallo **urllib2** bibliotheek ScoreData wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="eb672-179">tooconnect tooa Machine Learning Web service, use hello **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="eb672-180">ScoreData bevat een FeatureVector, een n-dimensionale vector van numerieke functies die Hallo ScoreData vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="eb672-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="eb672-181">U verifiëren toohello Machine Learning-service met een API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="eb672-181">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="eb672-182">**toorun Hallo-codevoorbeeld**</span><span class="sxs-lookup"><span data-stu-id="eb672-182">**toorun hello code sample**</span></span>

1. <span data-ttu-id="eb672-183">Implementeren ' voorbeeld 1: gegevensset downloaden van UCI: volwassene 2 klasse gegevensset ' experiment, deel van Hallo Machine Learning voorbeeld verzameling.</span><span class="sxs-lookup"><span data-stu-id="eb672-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="eb672-184">Wijs apiKey met Hallo sleutel van een webservice.</span><span class="sxs-lookup"><span data-stu-id="eb672-184">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="eb672-185">Zie Hallo **ophalen van een Azure Machine Learning-autorisatiesleutel** sectie bijna Hallo begin van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="eb672-185">See hello **Get an Azure Machine Learning authorization key** section near hello beginning of this article.</span></span>
3. <span data-ttu-id="eb672-186">Wijs serviceUri Hello aanvraag-URI.</span><span class="sxs-lookup"><span data-stu-id="eb672-186">Assign serviceUri with hello Request URI.</span></span>

