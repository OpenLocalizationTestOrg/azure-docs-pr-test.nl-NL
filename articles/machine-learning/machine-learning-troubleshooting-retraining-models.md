---
title: aaaTroubleshoot retraining een klassieke Azure Machine Learning-webservice | Microsoft Docs
description: Identificeren en te corrigeren van algemene problemen tegengekomen wanneer u Hallo model zijn retraining voor een Azure Machine Learning-webservice.
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="cd923-103">Het oplossen van problemen Hallo retraining van een Azure Machine Learning klassieke webservice</span><span class="sxs-lookup"><span data-stu-id="cd923-103">Troubleshooting hello retraining of an Azure Machine Learning Classic Web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="cd923-104">Overzicht retraining</span><span class="sxs-lookup"><span data-stu-id="cd923-104">Retraining overview</span></span>
<span data-ttu-id="cd923-105">Dit is een statische model wanneer u een Voorspellend experiment als scoreprofiel webservice implementeert.</span><span class="sxs-lookup"><span data-stu-id="cd923-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="cd923-106">Zodra er nieuwe gegevens beschikbaar of als consument Hallo Hallo API hun eigen gegevens bevat, moet Hallo model toobe retrained.</span><span class="sxs-lookup"><span data-stu-id="cd923-106">As new data becomes available or when hello consumer of hello API has their own data, hello model needs toobe retrained.</span></span> 

<span data-ttu-id="cd923-107">Zie voor een volledig overzicht Hallo proces van een klassieke webservice retraining [Retrain Machine Learning-modellen programmatisch](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="cd923-107">For a complete walkthrough of hello retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="cd923-108">Proces retraining</span><span class="sxs-lookup"><span data-stu-id="cd923-108">Retraining process</span></span>
<span data-ttu-id="cd923-109">Wanneer u tooretrain Hallo-webservice, moet u enkele aanvullende onderdelen toevoegen:</span><span class="sxs-lookup"><span data-stu-id="cd923-109">When you need tooretrain hello Web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="cd923-110">Een webservice van Hallo Trainingsexperiment geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="cd923-110">A Web service deployed from hello Training Experiment.</span></span> <span data-ttu-id="cd923-111">Hallo-experiment moet hebben een **Web Service uitvoer** module gekoppeld toohello uitvoer van Hallo **Train Model** module.</span><span class="sxs-lookup"><span data-stu-id="cd923-111">hello experiment must have a **Web Service Output** module attached toohello output of hello **Train Model** module.</span></span>  
  
    ![Koppel Hallo web service uitvoer toohello train-model.][image1]
* <span data-ttu-id="cd923-113">Een nieuw eindpunt toegevoegd tooyour score berekenen voor Web-service.</span><span class="sxs-lookup"><span data-stu-id="cd923-113">A new endpoint added tooyour scoring Web service.</span></span>  <span data-ttu-id="cd923-114">Kunt u programmatisch Hallo eindpunt toevoegen met behulp van Hallo voorbeeldcode waarnaar wordt verwezen in Hallo Retrain Machine Learning-modellen programmatisch onderwerp of via Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="cd923-114">You can add hello endpoint programmatically using hello sample code referenced in hello Retrain Machine Learning models programmatically topic or through hello Azure classic portal.</span></span>

<span data-ttu-id="cd923-115">Vervolgens kunt u Hallo voorbeeld C#-code uit Hallo Training Web Service API help pagina tooretrain model.</span><span class="sxs-lookup"><span data-stu-id="cd923-115">You can then use hello sample C# code from hello Training Web Service's API help page tooretrain model.</span></span> <span data-ttu-id="cd923-116">Nadat u Hallo resultaten hebt geëvalueerd, en u tevreden met bent, bijwerken Hallo getrainde model score berekenen voor webservice met behulp van nieuwe Hallo-eindpunt dat u hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="cd923-116">Once you have evaluated hello results and are satisfied with them, you update hello trained model scoring web service using hello new endpoint that you added.</span></span>

<span data-ttu-id="cd923-117">Met alle Hallo stukken erin zijn Hallo belangrijke stappen die u moet rekening houden met tooretrain Hallo model als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="cd923-117">With all hello pieces in place, hello major steps you must take tooretrain hello model are as follows:</span></span>

1. <span data-ttu-id="cd923-118">Hallo Training webservice aanroepen: Hallo aanroep toohello Batch uitvoering Service (BES) is, niet Hallo aanvragen antwoord Service (RR's).</span><span class="sxs-lookup"><span data-stu-id="cd923-118">Call hello Training Web Service:  hello call is toohello Batch Execution Service (BES), not hello Request Response Service (RRS).</span></span> <span data-ttu-id="cd923-119">Hallo-voorbeeld C#-code kunt u op Hallo API help pagina toomake Hallo aanroep.</span><span class="sxs-lookup"><span data-stu-id="cd923-119">You can use hello sample C# code on hello API help page toomake hello call.</span></span> 
2. <span data-ttu-id="cd923-120">Hallo waarden vinden voor Hallo *BaseLocation*, *RelativeLocation*, en *SasBlobToken*: deze waarden worden geretourneerd in Hallo uitvoer van de aanroep toohello Training Web De service.</span><span class="sxs-lookup"><span data-stu-id="cd923-120">Find hello values for hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in hello output from your call toohello Training Web Service.</span></span> 
   <span data-ttu-id="cd923-121">![Hallo-uitvoer van Hallo retraining hello en voorbeelden BaseLocation RelativeLocation en SasBlobToken waarden weergegeven.][image6]</span><span class="sxs-lookup"><span data-stu-id="cd923-121">![showing hello output of hello retraining sample and hello BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="cd923-122">Update Hallo toegevoegd endpoint van nieuwe score berekenen voor webservice met Hallo Hallo getraind model: Hallo voorbeeldcode met opgegeven in Machine Learning Retrain Hallo modellen programmatisch Hallo nieuwe eindpunt bijgewerkt u toohello score model Hello zojuist toegevoegd getraind model uit Hallo Training Web Service.</span><span class="sxs-lookup"><span data-stu-id="cd923-122">Update hello added endpoint from hello scoring web service with hello new trained model: Using hello sample code provided in hello Retrain Machine Learning models programmatically, update hello new endpoint you added toohello scoring model with hello newly trained model from hello Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="cd923-123">Algemene obstakels</span><span class="sxs-lookup"><span data-stu-id="cd923-123">Common obstacles</span></span>
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a><span data-ttu-id="cd923-124">Toosee controleren als er Hallo Corrigeer URL PATCH</span><span class="sxs-lookup"><span data-stu-id="cd923-124">Check toosee if you have hello correct PATCH URL</span></span>
<span data-ttu-id="cd923-125">Hallo PATCH URL die u gebruikt moet Hallo die is gekoppeld aan Hallo nieuwe score-eindpunt u toegevoegd toohello score berekenen voor Web-service.</span><span class="sxs-lookup"><span data-stu-id="cd923-125">hello PATCH URL you are using must be hello one associated with hello new scoring endpoint you added toohello scoring Web service.</span></span> <span data-ttu-id="cd923-126">Er zijn een aantal manieren tooobtain Hallo PATCH URL:</span><span class="sxs-lookup"><span data-stu-id="cd923-126">There are a number of ways tooobtain hello PATCH URL:</span></span>

<span data-ttu-id="cd923-127">**Optie 1: via programmacode**</span><span class="sxs-lookup"><span data-stu-id="cd923-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="cd923-128">Hallo tooget corrigeren PATCH URL:</span><span class="sxs-lookup"><span data-stu-id="cd923-128">tooget hello correct PATCH URL:</span></span>

1. <span data-ttu-id="cd923-129">Voer Hallo [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="cd923-129">Run hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="cd923-130">Hallo zoeken van uitvoer Hallo van AddEndpoint *HelpLocation* waarde en kopieer Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="cd923-130">From hello output of AddEndpoint, find hello *HelpLocation* value and copy hello URL.</span></span>
   
   ![HelpLocation in Hallo-uitvoer van Hallo addEndpoint voorbeeld.][image2]
3. <span data-ttu-id="cd923-132">Hallo-URL in een browser toonavigate tooa pagina waarmee help-koppelingen Hallo webservice plakken.</span><span class="sxs-lookup"><span data-stu-id="cd923-132">Paste hello URL into a browser toonavigate tooa page that provides help links for hello Web service.</span></span>
4. <span data-ttu-id="cd923-133">Klik op Hallo **Update Resource** koppeling tooopen Hallo patch help-pagina.</span><span class="sxs-lookup"><span data-stu-id="cd923-133">Click hello **Update Resource** link tooopen hello patch help page.</span></span>

<span data-ttu-id="cd923-134">**Optie 2: Hallo klassieke Azure-portal gebruiken**</span><span class="sxs-lookup"><span data-stu-id="cd923-134">**Option 2: Use hello Azure classic portal**</span></span>

1. <span data-ttu-id="cd923-135">Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="cd923-135">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="cd923-136">Open Hallo Machine Learning-tabblad. ![Machine bijvoorbeeld tabblad.][image4]</span><span class="sxs-lookup"><span data-stu-id="cd923-136">Open hello Machine Learning tab. ![Machine leaning tab.][image4]</span></span>
3. <span data-ttu-id="cd923-137">Klik op de naam van uw werkruimte **webservices**.</span><span class="sxs-lookup"><span data-stu-id="cd923-137">Click your workspace name, then **Web Services**.</span></span>
4. <span data-ttu-id="cd923-138">Klik op Hallo score berekenen voor u werkt met de webservice.</span><span class="sxs-lookup"><span data-stu-id="cd923-138">Click hello scoring Web service you are working with.</span></span> <span data-ttu-id="cd923-139">(Als u niet de standaardnaam Hallo van webservice Hallo wijzigt hebt, wordt het beëindigd in [score berekenen Exp.].)</span><span class="sxs-lookup"><span data-stu-id="cd923-139">(If you did not modify hello default name of hello web service, it will end in [Scoring Exp.].)</span></span>
5. <span data-ttu-id="cd923-140">Klik op **eindpunt toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="cd923-140">Click **Add Endpoint**.</span></span>
6. <span data-ttu-id="cd923-141">Nadat het Hallo-eindpunt wordt toegevoegd, klikt u op Hallo eindpuntnaam.</span><span class="sxs-lookup"><span data-stu-id="cd923-141">After hello endpoint is added, click hello endpoint name.</span></span> <span data-ttu-id="cd923-142">Klik vervolgens op **Update Resource** tooopen Hallo patch help-pagina.</span><span class="sxs-lookup"><span data-stu-id="cd923-142">Then click **Update Resource** tooopen hello patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="cd923-143">Als u Hallo eindpunt toohello Training webservice in plaats van Hallo voorspellende webservice hebt toegevoegd, ontvangt u de volgende fout wanneer u klikt op Hallo Hallo **Update Resource** koppeling: Sorry, maar deze functie wordt niet ondersteund of beschikbaar in deze context.</span><span class="sxs-lookup"><span data-stu-id="cd923-143">If you have added hello endpoint toohello Training Web Service instead of hello Predictive Web Service, you will receive hello following error when you click hello **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="cd923-144">Deze webservice heeft geen bronnen worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="cd923-144">This Web Service has no updatable resources.</span></span> <span data-ttu-id="cd923-145">We onze excuses voor het ongemak Hallo en werkt op het verbeteren van deze werkstroom.</span><span class="sxs-lookup"><span data-stu-id="cd923-145">We apologize for hello inconvenience and are working on improving this workflow.</span></span>
> 
> 

![Nieuwe endpoint-dashboard.][image3]

<span data-ttu-id="cd923-147">Hallo PATCH help-pagina Hallo moet u de PATCH-URL bevat en wordt een voorbeeldcode kunt u toocall deze.</span><span class="sxs-lookup"><span data-stu-id="cd923-147">hello PATCH help page contains hello PATCH URL you must use and provides sample code you can use toocall it.</span></span>

![URL van de patch.][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a><span data-ttu-id="cd923-149">Controleer dat u de juiste scoreprofiel eindpunt Hallo bijwerkt toosee</span><span class="sxs-lookup"><span data-stu-id="cd923-149">Check toosee that you are updating hello correct scoring endpoint</span></span>
* <span data-ttu-id="cd923-150">Hallo Training webservice niet doen patch: Hallo patch-bewerking moet worden uitgevoerd op Hallo score berekenen voor Web-service.</span><span class="sxs-lookup"><span data-stu-id="cd923-150">Do not patch hello Training Web Service: hello patch operation must be performed on hello scoring Web service.</span></span>
* <span data-ttu-id="cd923-151">Hallo standaardeindpunt op Web-service niet doen patch: Hallo patch-bewerking moet worden uitgevoerd op Hallo scoren van nieuwe webservice-eindpunt dat u hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="cd923-151">Do not patch hello default endpoint on Web service: hello patch operation must be performed on hello new scoring Web service endpoint that you added.</span></span>

<span data-ttu-id="cd923-152">U kunt controleren welke Hallo webservice-eindpunt op door bezoekende Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="cd923-152">You can verify which Web service hello endpoint is on by visiting hello Azure classic portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="cd923-153">Zorg ervoor dat u toevoegt Hallo eindpunt toohello voorspellende webservice niet Hallo Training Web Service.</span><span class="sxs-lookup"><span data-stu-id="cd923-153">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="cd923-154">Als u correct zowel een trainings- en een Voorspellend webservice hebt geïmplementeerd, ziet u twee verschillende Web-services die worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="cd923-154">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span></span> <span data-ttu-id="cd923-155">Hallo voorspellende webservice moet eindigen met '[voorspellende exp.]'.</span><span class="sxs-lookup"><span data-stu-id="cd923-155">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="cd923-156">Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="cd923-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="cd923-157">Open Hallo Machine Learning-tabblad. ![Machine learning-werkruimte gebruikersinterface.][image4]</span><span class="sxs-lookup"><span data-stu-id="cd923-157">Open hello Machine Learning tab. ![Machine learning workspace UI.][image4]</span></span>
3. <span data-ttu-id="cd923-158">Selecteer uw werkruimte.</span><span class="sxs-lookup"><span data-stu-id="cd923-158">Select your workspace.</span></span>
4. <span data-ttu-id="cd923-159">Klik op **webservices**.</span><span class="sxs-lookup"><span data-stu-id="cd923-159">Click **Web Services**.</span></span>
5. <span data-ttu-id="cd923-160">Selecteer uw Predictive webservice.</span><span class="sxs-lookup"><span data-stu-id="cd923-160">Select your Predictive Web Service.</span></span>
6. <span data-ttu-id="cd923-161">Controleren of uw nieuwe eindpunt toohello Web-service is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="cd923-161">Verify that your new endpoint was added toohello Web service.</span></span>

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a><span data-ttu-id="cd923-162">Hallo-werkruimte die uw web-service in het zich in de juiste regio Hallo tooensure controleren</span><span class="sxs-lookup"><span data-stu-id="cd923-162">Check hello workspace that your web service is in tooensure it is in hello correct region</span></span>
1. <span data-ttu-id="cd923-163">Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="cd923-163">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="cd923-164">Selecteer Machine Learning Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="cd923-164">Select Machine Learning from hello menu.</span></span>
   <span data-ttu-id="cd923-165">![Machine learning regio gebruikersinterface.][image4]</span><span class="sxs-lookup"><span data-stu-id="cd923-165">![Machine learning region UI.][image4]</span></span>
3. <span data-ttu-id="cd923-166">Hallo-locatie van de werkruimte controleren.</span><span class="sxs-lookup"><span data-stu-id="cd923-166">Verify hello location of your workspace.</span></span>

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
