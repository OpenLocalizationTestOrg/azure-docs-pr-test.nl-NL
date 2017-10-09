---
title: 'Stap 5: Hallo Machine Learning-webservice implementeren | Microsoft Docs'
description: 'Stap 5 van Hallo een overzicht van de voorspellende oplossing ontwikkelen: implementeert een Voorspellend experiment in Machine Learning Studio als een webservice.'
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 3fca74a3-c44b-4583-a218-c14c46ee5338
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 76391010972ed1450bbda8bfb2352c7b22b51ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-5-deploy-hello-azure-machine-learning-web-service"></a><span data-ttu-id="4be19-103">Scenario-stap 5: Hello Azure Machine Learning-webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="4be19-103">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>
<span data-ttu-id="4be19-104">Dit is de vijfde stap Hallo van Hallo-rondleiding [predictive analytics-oplossing in Azure Machine Learning ontwikkelen](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="4be19-104">This is hello fifth step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="4be19-105">Een Machine Learning-werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="4be19-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="4be19-106">Bestaande gegevens uploaden</span><span class="sxs-lookup"><span data-stu-id="4be19-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="4be19-107">Een nieuw experiment maken</span><span class="sxs-lookup"><span data-stu-id="4be19-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="4be19-108">Trainen en evalueren Hallo modellen</span><span class="sxs-lookup"><span data-stu-id="4be19-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. <span data-ttu-id="4be19-109">**Hallo-webservice implementeren**</span><span class="sxs-lookup"><span data-stu-id="4be19-109">**Deploy hello web service**</span></span>
6. [<span data-ttu-id="4be19-110">Toegang Hallo-webservice</span><span class="sxs-lookup"><span data-stu-id="4be19-110">Access hello web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="4be19-111">toogive anderen een kans toouse Hallo Voorspellend model dat we hebben ontwikkeld in dit scenario, we deze kunt implementeren als een webservice in Azure.</span><span class="sxs-lookup"><span data-stu-id="4be19-111">toogive others a chance toouse hello predictive model we've developed in this walkthrough, we can deploy it as a web service on Azure.</span></span>

<span data-ttu-id="4be19-112">Toothis punt Experimenteer we met het model te trainen.</span><span class="sxs-lookup"><span data-stu-id="4be19-112">Up toothis point we've been experimenting with training our model.</span></span> <span data-ttu-id="4be19-113">Maar Hallo geïmplementeerd service zal niet langer toodo training - toogenerate nieuwe voorspellingen door score berekenen Hallo gebruikersinvoer op basis van onze model gaat.</span><span class="sxs-lookup"><span data-stu-id="4be19-113">But hello deployed service is no longer going toodo training - it's going toogenerate new predictions by scoring hello user's input based on our model.</span></span> <span data-ttu-id="4be19-114">Dus gaan we toodo sommige tooconvert voorbereiding dit experiment uit een ***training*** experimenteren tooa ***voorspellende*** experimenteren.</span><span class="sxs-lookup"><span data-stu-id="4be19-114">So we're going toodo some preparation tooconvert this experiment from a ***training*** experiment tooa ***predictive*** experiment.</span></span> 

<span data-ttu-id="4be19-115">Dit is een proces drie stappen:</span><span class="sxs-lookup"><span data-stu-id="4be19-115">This is a three-step process:</span></span>  

1. <span data-ttu-id="4be19-116">Verwijder een van de Hallo modellen</span><span class="sxs-lookup"><span data-stu-id="4be19-116">Remove one of hello models</span></span>
2. <span data-ttu-id="4be19-117">Hallo converteren *trainingsexperiment* we hebt gemaakt in een *Voorspellend experiment*</span><span class="sxs-lookup"><span data-stu-id="4be19-117">Convert hello *training experiment* we've created into a *predictive experiment*</span></span>
3. <span data-ttu-id="4be19-118">Hallo Voorspellend experiment implementeren als een webservice</span><span class="sxs-lookup"><span data-stu-id="4be19-118">Deploy hello predictive experiment as a web service</span></span>

## <a name="remove-one-of-hello-models"></a><span data-ttu-id="4be19-119">Verwijder een van de Hallo modellen</span><span class="sxs-lookup"><span data-stu-id="4be19-119">Remove one of hello models</span></span>

<span data-ttu-id="4be19-120">We moeten eerst tootrim dit experiment omlaag enigszins.</span><span class="sxs-lookup"><span data-stu-id="4be19-120">First, we need tootrim this experiment down a little.</span></span> <span data-ttu-id="4be19-121">Momenteel hebben we twee verschillende modellen in Hallo-experiment, maar we willen alleen één model toouse wanneer we dit als een webservice implementeert.</span><span class="sxs-lookup"><span data-stu-id="4be19-121">We currently have two different models in hello experiment, but we only want toouse one model when we deploy this as a web service.</span></span>  

<span data-ttu-id="4be19-122">Stel, dat we hebt besloten dat Hallo boosted structuur model beter presteert dan Hallo SVM model.</span><span class="sxs-lookup"><span data-stu-id="4be19-122">Let's say we've decided that hello boosted tree model performed better than hello SVM model.</span></span> <span data-ttu-id="4be19-123">Zodat het eerste wat toodo Hallo verwijderen Hallo [Two-Class ondersteuning Vectormachine] [ two-class-support-vector-machine] module en Hallo-modules die zijn gebruikt voor het trainen van het.</span><span class="sxs-lookup"><span data-stu-id="4be19-123">So hello first thing toodo is remove hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module and hello modules that were used for training it.</span></span> <span data-ttu-id="4be19-124">U kunt een kopie van Hallo experiment toomake eerst door te klikken op **OpslaanAls** onderin Hallo Hallo experimenteren canvas.</span><span class="sxs-lookup"><span data-stu-id="4be19-124">You may want toomake a copy of hello experiment first by clicking **Save As** at hello bottom of hello experiment canvas.</span></span>

<span data-ttu-id="4be19-125">We moeten toodelete Hallo modules te volgen:</span><span class="sxs-lookup"><span data-stu-id="4be19-125">We need toodelete hello following modules:</span></span>  

* <span data-ttu-id="4be19-126">[Vectormachine Two-Class-ondersteuning][two-class-support-vector-machine]</span><span class="sxs-lookup"><span data-stu-id="4be19-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span></span>
* <span data-ttu-id="4be19-127">[Model trainen] [ train-model] en [Score Model] [ score-model] modules die verbonden tooit zijn</span><span class="sxs-lookup"><span data-stu-id="4be19-127">[Train Model][train-model] and [Score Model][score-model] modules that were connected tooit</span></span>
* <span data-ttu-id="4be19-128">[Gegevens normaliseren] [ normalize-data] (van beide)</span><span class="sxs-lookup"><span data-stu-id="4be19-128">[Normalize Data][normalize-data] (both of them)</span></span>
* <span data-ttu-id="4be19-129">[Model evalueren] [ evaluate-model] (omdat we klaar bent met het evalueren van Hallo modellen)</span><span class="sxs-lookup"><span data-stu-id="4be19-129">[Evaluate Model][evaluate-model] (because we're finished evaluating hello models)</span></span>

<span data-ttu-id="4be19-130">Selecteer elke module en druk op Hallo verwijderen sleutel, of klik met de rechtermuisknop Hallo module en selecteer **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="4be19-130">Select each module and press hello Delete key, or right-click hello module and select **Delete**.</span></span> 

![Hallo SVM model verwijderd][3a]

<span data-ttu-id="4be19-132">Het model moet nu als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="4be19-132">Our model should now look something like this:</span></span>

![Hallo SVM model verwijderd][3]

<span data-ttu-id="4be19-134">Nu we klaar toodeploy dit model met behulp van Hallo [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span><span class="sxs-lookup"><span data-stu-id="4be19-134">Now we're ready toodeploy this model using hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span></span>

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a><span data-ttu-id="4be19-135">Hallo training experiment tooa Voorspellend experiment converteren</span><span class="sxs-lookup"><span data-stu-id="4be19-135">Convert hello training experiment tooa predictive experiment</span></span>

<span data-ttu-id="4be19-136">tooget dit model is klaar voor implementatie, moeten we tooconvert dit experiment tooa Voorspellend experiment training.</span><span class="sxs-lookup"><span data-stu-id="4be19-136">tooget this model ready for deployment, we need tooconvert this training experiment tooa predictive experiment.</span></span> <span data-ttu-id="4be19-137">Dit omvat drie stappen:</span><span class="sxs-lookup"><span data-stu-id="4be19-137">This involves three steps:</span></span>

1. <span data-ttu-id="4be19-138">Hallo model we hebben getraind en vervang onze trainingsmodules opslaan</span><span class="sxs-lookup"><span data-stu-id="4be19-138">Save hello model we've trained and then replace our training modules</span></span>
2. <span data-ttu-id="4be19-139">Trim Hallo experiment tooremove modules die zijn alleen nodig voor training</span><span class="sxs-lookup"><span data-stu-id="4be19-139">Trim hello experiment tooremove modules that were only needed for training</span></span>
3. <span data-ttu-id="4be19-140">Definiëren waar Hallo webservice invoer accepteert en waarbij het Hallo-uitvoer genereert</span><span class="sxs-lookup"><span data-stu-id="4be19-140">Define where hello web service will accept input and where it generates hello output</span></span>

<span data-ttu-id="4be19-141">We kunnen dit handmatig doen, maar gelukkig alle drie stappen kunnen worden uitgevoerd door te klikken op **webservice ingesteld** Hallo Hallo experimentcanvas onderaan in (en het selecteren van Hallo **voorspellende webservice** optie).</span><span class="sxs-lookup"><span data-stu-id="4be19-141">We could do this manually, but fortunately all three steps can be accomplished by clicking **Set Up Web Service** at hello bottom of hello experiment canvas (and selecting hello **Predictive Web Service** option).</span></span>

> [!TIP]
> <span data-ttu-id="4be19-142">Als u meer informatie wilt over wat er gebeurt wanneer u een Voorspellend training experiment tooa converteren experimenteren, raadpleegt u [hoe tooprepare uw model voor de implementatie in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="4be19-142">If you want more details on what happens when you convert a training experiment tooa predictive experiment, see [How tooprepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="4be19-143">Wanneer u klikt op **webservice ingesteld**, op verschillende manieren gebeuren:</span><span class="sxs-lookup"><span data-stu-id="4be19-143">When you click **Set Up Web Service**, several things happen:</span></span>

* <span data-ttu-id="4be19-144">Hallo getrainde model is geconverteerde tooa één **getrainde Model** module en opgeslagen in Hallo module palet toohello links van Hallo Experimenteer canvas (u vindt deze onder **Trained Models**)</span><span class="sxs-lookup"><span data-stu-id="4be19-144">hello trained model is converted tooa single **Trained Model** module and stored in hello module palette toohello left of hello experiment canvas (you can find it under **Trained Models**)</span></span>
* <span data-ttu-id="4be19-145">Modules die zijn gebruikt voor training zijn verwijderd; specifieke opdrachten:</span><span class="sxs-lookup"><span data-stu-id="4be19-145">Modules that were used for training are removed; specifically:</span></span>
  * <span data-ttu-id="4be19-146">[Two-Class gestimuleerd beslissingsstructuur][two-class-boosted-decision-tree]</span><span class="sxs-lookup"><span data-stu-id="4be19-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span></span>
  * <span data-ttu-id="4be19-147">[Train Model][train-model]</span><span class="sxs-lookup"><span data-stu-id="4be19-147">[Train Model][train-model]</span></span>
  * <span data-ttu-id="4be19-148">[Gegevens splitsen][split]</span><span class="sxs-lookup"><span data-stu-id="4be19-148">[Split Data][split]</span></span>
  * <span data-ttu-id="4be19-149">tweede Hallo [R-Script uitvoeren] [ execute-r-script] module die is gebruikt voor testgegevens</span><span class="sxs-lookup"><span data-stu-id="4be19-149">hello second [Execute R Script][execute-r-script] module that was used for test data</span></span>
* <span data-ttu-id="4be19-150">Hallo opgeslagen getrainde model weer toegevoegd aan Hallo experiment</span><span class="sxs-lookup"><span data-stu-id="4be19-150">hello saved trained model is added back into hello experiment</span></span>
* <span data-ttu-id="4be19-151">**Web-invoer** en **Web service uitvoer** modules worden toegevoegd (deze vaststellen waar Hallo gebruikersgegevens voert Hallo model en welke gegevens worden geretourneerd wanneer Hallo-webservice wordt geopend)</span><span class="sxs-lookup"><span data-stu-id="4be19-151">**Web service input** and **Web service output** modules are added (these identify where hello user's data will enter hello model, and what data is returned, when hello web service is accessed)</span></span>

> [!NOTE]
> <span data-ttu-id="4be19-152">U kunt zien dat Hallo experiment wordt opgeslagen in twee delen onder tabbladen die Hallo boven aan het experimentcanvas Hallo zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="4be19-152">You can see that hello experiment is saved in two parts under tabs that have been added at hello top of hello experiment canvas.</span></span> <span data-ttu-id="4be19-153">Hallo oorspronkelijke trainingsexperiment ligt onder de Hallo tabblad **trainingsexperiment**, en Hallo nieuw gemaakte Voorspellend experiment ligt onder de **Voorspellend experiment**.</span><span class="sxs-lookup"><span data-stu-id="4be19-153">hello original training experiment is under hello tab **Training experiment**, and hello newly created predictive experiment is under **Predictive experiment**.</span></span> <span data-ttu-id="4be19-154">Hallo Voorspellend experiment is Hallo een die we als een webservice implementeert.</span><span class="sxs-lookup"><span data-stu-id="4be19-154">hello predictive experiment is hello one we'll deploy as a web service.</span></span>

<span data-ttu-id="4be19-155">Moet een extra stap tootake met dit bepaalde experiment.</span><span class="sxs-lookup"><span data-stu-id="4be19-155">We need tootake one additional step with this particular experiment.</span></span>
<span data-ttu-id="4be19-156">We twee toegevoegd [R-Script uitvoeren] [ execute-r-script] modules tooprovide een weging toohello gegevens werken.</span><span class="sxs-lookup"><span data-stu-id="4be19-156">We added two [Execute R Script][execute-r-script] modules tooprovide a weighting function toohello data.</span></span> <span data-ttu-id="4be19-157">Dat is slechts een slag die we nodig voor het trainen en te testen, zodat we uit deze modules in de laatste model Hallo kunt nemen.</span><span class="sxs-lookup"><span data-stu-id="4be19-157">That was just a trick we needed for training and testing, so we can take out those modules in hello final model.</span></span>
<span data-ttu-id="4be19-158">Machine Learning Studio verwijderd een [R-Script uitvoeren] [ execute-r-script] module wanneer het Hallo verwijderd [gesplitste] [ split] module.</span><span class="sxs-lookup"><span data-stu-id="4be19-158">Machine Learning Studio removed one [Execute R Script][execute-r-script] module when it removed hello [Split][split] module.</span></span> <span data-ttu-id="4be19-159">Nu we verwijderen andere Hallo en maak verbinding [metagegevens Editor] [ metadata-editor] rechtstreeks te[Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="4be19-159">Now we can remove hello other and connect [Metadata Editor][metadata-editor] directly too[Score Model][score-model].</span></span>    

<span data-ttu-id="4be19-160">Onze experiment ziet er nu als volgt:</span><span class="sxs-lookup"><span data-stu-id="4be19-160">Our experiment should now look like this:</span></span>  

![Score berekenen voor het getrainde model Hallo][4]  

> [!NOTE]
> <span data-ttu-id="4be19-162">U vraagt zich misschien af waarom we Hallo UCI Duits creditcardgegevens gegevensset links in Hallo Voorspellend experiment.</span><span class="sxs-lookup"><span data-stu-id="4be19-162">You may be wondering why we left hello UCI German Credit Card Data dataset in hello predictive experiment.</span></span> <span data-ttu-id="4be19-163">Hallo-service gaat tooscore Hallo van gebruikersgegevens, niet Hallo oorspronkelijke gegevensset, dus waarom laat de oorspronkelijke gegevensset Hallo in Hallo model?</span><span class="sxs-lookup"><span data-stu-id="4be19-163">hello service is going tooscore hello user's data, not hello original dataset, so why leave hello original dataset in hello model?</span></span>
> 
> <span data-ttu-id="4be19-164">Het is waar Hallo service oorspronkelijke creditcardgegevens niet nodig Hallo.</span><span class="sxs-lookup"><span data-stu-id="4be19-164">It's true that hello service doesn't need hello original credit card data.</span></span> <span data-ttu-id="4be19-165">Maar hoeft Hallo-schema voor die gegevens, waaronder gegevens zoals het aantal kolommen zijn en welke kolommen numeriek zijn.</span><span class="sxs-lookup"><span data-stu-id="4be19-165">But it does need hello schema for that data, which includes information such as how many columns there are and which columns are numeric.</span></span> <span data-ttu-id="4be19-166">Deze schema-informatie is nodig toointerpret Hallo gegevens van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4be19-166">This schema information is necessary toointerpret hello user's data.</span></span> <span data-ttu-id="4be19-167">We laten deze onderdelen die zijn verbonden, zodat hello scoremodule Hallo gegevensset-schema heeft wanneer Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4be19-167">We leave these components connected so that hello scoring module has hello dataset schema when hello service is running.</span></span> <span data-ttu-id="4be19-168">Hallo gegevens wordt niet gebruikt, alleen Hallo schema.</span><span class="sxs-lookup"><span data-stu-id="4be19-168">hello data isn't used, just hello schema.</span></span>  
> 
> 

<span data-ttu-id="4be19-169">Hallo-experiment een keer worden uitgevoerd (Klik op **uitvoeren**.) Als u nog steeds tooverify die Hallo model werkt wilt, klikt u op Hallo uitvoer Hallo [Score Model] [ score-model] module en selecteer **resultaten weergeven**.</span><span class="sxs-lookup"><span data-stu-id="4be19-169">Run hello experiment one last time (click **Run**.) If you want tooverify that hello model is still working, click hello output of hello [Score Model][score-model] module and select **View Results**.</span></span> <span data-ttu-id="4be19-170">U kunt zien dat de oorspronkelijke gegevens hello wordt weergegeven, samen met de Hallo tegoed risico waarde ('Scored Labels') en Hallo score berekenen voor waarschijnlijkheidswaarde ('berekend kansen'.)</span><span class="sxs-lookup"><span data-stu-id="4be19-170">You can see that hello original data is displayed, along with hello credit risk value ("Scored Labels") and hello scoring probability value ("Scored Probabilities".)</span></span> 

## <a name="deploy-hello-web-service"></a><span data-ttu-id="4be19-171">Hallo-webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="4be19-171">Deploy hello web service</span></span>
<span data-ttu-id="4be19-172">U kunt Hallo experiment implementeren als ofwel Classic webservice of als een nieuwe webservice die gebaseerd op Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4be19-172">You can deploy hello experiment as either a Classic web service, or as a New web service that's based on Azure Resource Manager.</span></span>

### <a name="deploy-as-a-classic-web-service"></a><span data-ttu-id="4be19-173">Als een klassiek-webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="4be19-173">Deploy as a Classic web service</span></span>
<span data-ttu-id="4be19-174">een klassiek webservice afgeleid van onze experiment toodeploy klikt u op **webservice implementeren** hieronder Hallo canvas en selecteer **webservice implementeren [klassieke]**.</span><span class="sxs-lookup"><span data-stu-id="4be19-174">toodeploy a Classic web service derived from our experiment, click **Deploy Web Service** below hello canvas and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="4be19-175">Machine Learning Studio Hallo experiment als een webservice implementeert en gaat u verder toohello dashboard voor de webservice.</span><span class="sxs-lookup"><span data-stu-id="4be19-175">Machine Learning Studio deploys hello experiment as a web service and takes you toohello dashboard for that web service.</span></span> <span data-ttu-id="4be19-176">Op deze pagina kunt u terugkeren toohello experiment (**weergave momentopname** of **weergeven het meest recente**) en een eenvoudige test van de webservice Hallo uitvoeren (Zie **Hallo webservice testen** hieronder).</span><span class="sxs-lookup"><span data-stu-id="4be19-176">From this page you can return toohello experiment (**View snapshot** or **View latest**) and run a simple test of hello web service (see **Test hello web service** below).</span></span> <span data-ttu-id="4be19-177">Er is ook hier informatie voor het maken van toepassingen die toegang heeft tot Hallo webservice (meer informatie over die in de volgende stap Hallo van deze rondleiding).</span><span class="sxs-lookup"><span data-stu-id="4be19-177">There is also information here for creating applications that can access hello web service (more on that in hello next step of this walkthrough).</span></span>

![Web service-dashboard][6]

<span data-ttu-id="4be19-179">U kunt Hallo service configureren door te klikken op Hallo **configuratie** tabblad. Hier kunt u de naam van de service Hallo (dit is opgegeven Hallo experiment naam standaard) wijzigen en wijs hieraan een beschrijving.</span><span class="sxs-lookup"><span data-stu-id="4be19-179">You can configure hello service by clicking hello **CONFIGURATION** tab. Here you can modify hello service name (it's given hello experiment name by default) and give it a description.</span></span> <span data-ttu-id="4be19-180">U kunt ook meer beschrijvende labels voor Hallo geeft en uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="4be19-180">You can also give more friendly labels for hello input and output data.</span></span>  

![Hallo-webservice configureren][5]  

### <a name="deploy-as-a-new-web-service"></a><span data-ttu-id="4be19-182">Als een nieuwe webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="4be19-182">Deploy as a New web service</span></span>

> [!NOTE] 
> <span data-ttu-id="4be19-183">een nieuwe webservice die u moet voldoende machtigingen hebben in Hallo abonnement toowhich die u implementeert toodeploy Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="4be19-183">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you are deploying hello web service.</span></span> <span data-ttu-id="4be19-184">Zie voor meer informatie [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="4be19-184">For more information, see [Manage a web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="4be19-185">een nieuwe webservice toodeploy afgeleid van onze experiment:</span><span class="sxs-lookup"><span data-stu-id="4be19-185">toodeploy a New web service derived from our experiment:</span></span>

1. <span data-ttu-id="4be19-186">Klik op **webservice implementeren** hieronder Hallo canvas en selecteer **Web Service implementeren [New]**.</span><span class="sxs-lookup"><span data-stu-id="4be19-186">Click **Deploy Web Service** below hello canvas and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="4be19-187">Machine Learning Studio, brengt u toohello Azure Machine Learning-webservices **implementeren Experiment** pagina.</span><span class="sxs-lookup"><span data-stu-id="4be19-187">Machine Learning Studio transfers you toohello Azure Machine Learning web services **Deploy Experiment** page.</span></span>

2. <span data-ttu-id="4be19-188">Voer een naam voor Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="4be19-188">Enter a name for hello web service.</span></span> 

3. <span data-ttu-id="4be19-189">Voor **prijs Plan**, kunt u een bestaande prijsstelling of Selecteer 'Nieuw maken' en geven Hallo nieuwe van plan bent een naam en selecteer Hallo-optie voor maandelijks plannen.</span><span class="sxs-lookup"><span data-stu-id="4be19-189">For **Price Plan**, you can select an existing pricing plan, or select "Create new" and give hello new plan a name and select hello monthly plan option.</span></span> <span data-ttu-id="4be19-190">Hallo plan lagen standaard toohello plannen voor uw regio standaard en uw webservice is geïmplementeerde toothat regio.</span><span class="sxs-lookup"><span data-stu-id="4be19-190">hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

4. <span data-ttu-id="4be19-191">Klik op **implementeren**.</span><span class="sxs-lookup"><span data-stu-id="4be19-191">Click **Deploy**.</span></span>

<span data-ttu-id="4be19-192">Na een paar minuten Hallo **Quick Start** pagina voor uw webservice wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="4be19-192">After a few minutes, hello **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="4be19-193">U kunt Hallo service configureren door te klikken op Hallo **configureren** tabblad. Hier kunt u wijzigen Hallo service title en wijs hieraan een beschrijving.</span><span class="sxs-lookup"><span data-stu-id="4be19-193">You can configure hello service by clicking hello **Configure** tab. Here you can modify hello service title and give it a description.</span></span> 

<span data-ttu-id="4be19-194">tootest hello webservice, klikt u op Hallo **Test** tabblad (Zie **Hallo webservice testen** hieronder).</span><span class="sxs-lookup"><span data-stu-id="4be19-194">tootest hello web service, click hello **Test** tab (see **Test hello web service** below).</span></span> <span data-ttu-id="4be19-195">Klik op Help voor meer informatie over het maken van toepassingen die toegang heeft tot de webservice Hallo Hallo **verbruiken** tabblad (de volgende stap in dit overzicht Hallo Ga dieper).</span><span class="sxs-lookup"><span data-stu-id="4be19-195">For information on creating applications that can access hello web service, click hello **Consume** tab (hello next step in this walkthrough will go into more detail).</span></span>

> [!TIP]
> <span data-ttu-id="4be19-196">Nadat u deze hebt geïmplementeerd, kunt u Hallo webservice bijwerken.</span><span class="sxs-lookup"><span data-stu-id="4be19-196">You can update hello web service after you've deployed it.</span></span> <span data-ttu-id="4be19-197">Bijvoorbeeld, als u uw model toochange wilt, vervolgens u kunt bewerken Hallo trainingsexperiment, Hallo Modelparameters aanpassen, en op **webservice implementeren**, selecteren **webservice implementeren [klassieke]** of  **[New]-webservice implementeren**.</span><span class="sxs-lookup"><span data-stu-id="4be19-197">For example, if you want toochange your model, then you can edit hello training experiment, tweak hello model parameters, and click **Deploy Web Service**, selecting **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span> <span data-ttu-id="4be19-198">Wanneer u een experiment Hallo opnieuw implementeert, vervangt het Hallo-webservice, nu met gebruik van uw bijgewerkte model.</span><span class="sxs-lookup"><span data-stu-id="4be19-198">When you deploy hello experiment again, it replaces hello web service, now using your updated model.</span></span>  
> 
> 

## <a name="test-hello-web-service"></a><span data-ttu-id="4be19-199">Hallo webservice testen</span><span class="sxs-lookup"><span data-stu-id="4be19-199">Test hello web service</span></span>

<span data-ttu-id="4be19-200">Als de webservice hello wordt geopend, krijgt de Hallo gebruikersgegevens via Hallo **Web service invoer** module waar deze toohello heeft doorgegeven [Score Model] [ score-model] module en gewaardeerd.</span><span class="sxs-lookup"><span data-stu-id="4be19-200">When hello web service is accessed, hello user's data enters through hello **Web service input** module where it's passed toohello [Score Model][score-model] module and scored.</span></span> <span data-ttu-id="4be19-201">Hallo manier die we Hallo Voorspellend experiment hebt ingesteld, Hallo-model verwacht gegevens in dezelfde notatie als Hallo oorspronkelijke tegoed risico gegevensset Hallo.</span><span class="sxs-lookup"><span data-stu-id="4be19-201">hello way we've set up hello predictive experiment, hello model expects data in hello same format as hello original credit risk dataset.</span></span>
<span data-ttu-id="4be19-202">Hallo resultaten zijn toohello gebruiker van de webservice Hallo via Hallo **Web service uitvoer** module.</span><span class="sxs-lookup"><span data-stu-id="4be19-202">hello results are returned toohello user from hello web service through hello **Web service output** module.</span></span>

> [!TIP]
> <span data-ttu-id="4be19-203">Hallo manier hebben we Hallo Voorspellend experiment geconfigureerd, Hallo gehele resultaat is van een Hallo [Score Model] [ score-model] module worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="4be19-203">hello way we have hello predictive experiment configured, hello entire results from hello [Score Model][score-model] module are returned.</span></span> <span data-ttu-id="4be19-204">Dit omvat alle invoergegevens Hallo plus Hallo tegoed risico waarde en Hallo kans score berekenen.</span><span class="sxs-lookup"><span data-stu-id="4be19-204">This includes all hello input data plus hello credit risk value and hello scoring probability.</span></span> <span data-ttu-id="4be19-205">Maar u kunt een iets andere betekenis als u wilt terugkeren - u kan bijvoorbeeld alleen Hallo tegoed risico waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="4be19-205">But you can return something different if you want - for example, you could return just hello credit risk value.</span></span> <span data-ttu-id="4be19-206">toodo deze, invoegen een [Projectkolommen] [ project-columns] module tussen [Score Model] [ score-model] en Hallo **Web service uitvoer** tooeliminate kolommen die u niet wilt dat de web service tooreturn Hallo.</span><span class="sxs-lookup"><span data-stu-id="4be19-206">toodo this, insert a [Project Columns][project-columns] module between [Score Model][score-model] and hello **Web service output** tooeliminate columns you don't want hello web service tooreturn.</span></span> 
> 
> 

<span data-ttu-id="4be19-207">U kunt een klassiek web testen in service **Machine Learning Studio** of in Hallo **Azure Machine Learning-webservices** portal.</span><span class="sxs-lookup"><span data-stu-id="4be19-207">You can test a Classic web service either in **Machine Learning Studio** or in hello **Azure Machine Learning Web Services** portal.</span></span>
<span data-ttu-id="4be19-208">U kunt een nieuwe webservice testen alleen in Hallo **Machine Learning-webservices** portal.</span><span class="sxs-lookup"><span data-stu-id="4be19-208">You can test a New web service only in hello **Machine Learning Web Services** portal.</span></span>

> [!TIP]
> <span data-ttu-id="4be19-209">Bij het testen in hello Azure Machine Learning-webservices-portal, kunt u Hallo portal maken waarmee u tootest Hallo aanvragen en antwoorden service kunt voorbeeldgegevens kunt hebben.</span><span class="sxs-lookup"><span data-stu-id="4be19-209">When testing in hello Azure Machine Learning Web Services portal, you can have hello portal create sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="4be19-210">Op Hallo **configureren** pagina, selecteert u 'Ja' voor **voorbeeld gegevens ingeschakeld?**.</span><span class="sxs-lookup"><span data-stu-id="4be19-210">On hello **Configure** page, select "Yes" for **Sample Data Enabled?**.</span></span> <span data-ttu-id="4be19-211">Bij het openen van tabblad Hallo aanvragen en antwoorden op Hallo **Test** pagina Hallo portal ingevuld voorbeeldgegevens die afkomstig zijn uit Hallo oorspronkelijke tegoed risico gegevensset.</span><span class="sxs-lookup"><span data-stu-id="4be19-211">When you open hello Request-Response tab on hello **Test** page, hello portal fills in sample data taken from hello original credit risk dataset.</span></span>

### <a name="test-a-classic-web-service"></a><span data-ttu-id="4be19-212">Een klassieke webservice testen</span><span class="sxs-lookup"><span data-stu-id="4be19-212">Test a Classic web service</span></span>

<span data-ttu-id="4be19-213">In Machine Learning Studio of Hallo Machine Learning-webservices portal, kunt u een webservice klassieke testen.</span><span class="sxs-lookup"><span data-stu-id="4be19-213">You can test a Classic web service in Machine Learning Studio or in hello Machine Learning Web Services portal.</span></span> 

#### <a name="test-in-machine-learning-studio"></a><span data-ttu-id="4be19-214">Testen in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="4be19-214">Test in Machine Learning Studio</span></span>

1. <span data-ttu-id="4be19-215">Op Hallo **DASHBOARD** pagina voor Hallo-webservice, klikt u op Hallo **Test** knop onder **eindpunt standaard**.</span><span class="sxs-lookup"><span data-stu-id="4be19-215">On hello **DASHBOARD** page for hello web service, click hello **Test** button under **Default Endpoint**.</span></span> <span data-ttu-id="4be19-216">Een dialoogvenster verschijnt en vraagt u om Hallo invoergegevens voor Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="4be19-216">A dialog pops up and asks you for hello input data for hello service.</span></span> <span data-ttu-id="4be19-217">Deze Hallo dezelfde kolommen die zijn opgetreden in Hallo oorspronkelijke tegoed risico gegevensset zijn.</span><span class="sxs-lookup"><span data-stu-id="4be19-217">These are hello same columns that appeared in hello original credit risk dataset.</span></span>  

2. <span data-ttu-id="4be19-218">Geef een set gegevens en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4be19-218">Enter a set of data and then click **OK**.</span></span> 

#### <a name="test-in-hello-machine-learning-web-services-portal"></a><span data-ttu-id="4be19-219">Testen in Hallo Machine Learning-webservices-portal</span><span class="sxs-lookup"><span data-stu-id="4be19-219">Test in hello Machine Learning Web Services portal</span></span>

1. <span data-ttu-id="4be19-220">Op Hallo **DASHBOARD** pagina voor Hallo-webservice, klikt u op Hallo **Test preview** koppeling onder **eindpunt standaard**.</span><span class="sxs-lookup"><span data-stu-id="4be19-220">On hello **DASHBOARD** page for hello web service, click hello **Test preview** link under **Default Endpoint**.</span></span> <span data-ttu-id="4be19-221">Hallo testpagina in hello Azure Machine Learning-webservices-portal voor Hallo webservice-eindpunt wordt geopend en u wordt gevraagd de invoergegevens Hallo voor Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="4be19-221">hello test page in hello Azure Machine Learning Web Services portal for hello web service endpoint opens and asks you for hello input data for hello service.</span></span> <span data-ttu-id="4be19-222">Deze Hallo dezelfde kolommen die zijn opgetreden in Hallo oorspronkelijke tegoed risico gegevensset zijn.</span><span class="sxs-lookup"><span data-stu-id="4be19-222">These are hello same columns that appeared in hello original credit risk dataset.</span></span>

2. <span data-ttu-id="4be19-223">Klik op **testen aanvragen en antwoorden**.</span><span class="sxs-lookup"><span data-stu-id="4be19-223">Click **Test Request-Response**.</span></span> 

### <a name="test-a-new-web-service"></a><span data-ttu-id="4be19-224">Een nieuwe webservice testen</span><span class="sxs-lookup"><span data-stu-id="4be19-224">Test a New web service</span></span>

<span data-ttu-id="4be19-225">U kunt een nieuwe webservice testen alleen in Hallo Machine Learning-webservices-portal.</span><span class="sxs-lookup"><span data-stu-id="4be19-225">You can test a New web service only in hello Machine Learning Web Services portal.</span></span>

1. <span data-ttu-id="4be19-226">In Hallo [Azure Machine Learning-webservices](https://services.azureml.net/quickstart) en klik op **Test** bovenaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="4be19-226">In hello [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal, click **Test** at hello top of hello page.</span></span> <span data-ttu-id="4be19-227">Hallo **Test** pagina wordt geopend en kunt u gegevens voor de service Hallo invoeren.</span><span class="sxs-lookup"><span data-stu-id="4be19-227">hello **Test** page opens and you can input data for hello service.</span></span> <span data-ttu-id="4be19-228">Hallo invoervelden weergegeven overeenkomen toohello kolommen die zijn opgetreden in de oorspronkelijke gegevensset van tegoed risico Hallo.</span><span class="sxs-lookup"><span data-stu-id="4be19-228">hello input fields displayed correspond toohello columns that appeared in hello original credit risk dataset.</span></span> 

2. <span data-ttu-id="4be19-229">Geef een set gegevens en klik op **Test aanvragen en antwoorden**.</span><span class="sxs-lookup"><span data-stu-id="4be19-229">Enter a set of data and then click **Test Request-Response**.</span></span>

<span data-ttu-id="4be19-230">Hallo worden resultaten van de test Hallo weergegeven op de rechterkant van de pagina Hallo in uitvoerkolom Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4be19-230">hello results of hello test are displayed on hello right-hand side of hello page in hello output column.</span></span> 


## <a name="manage-hello-web-service"></a><span data-ttu-id="4be19-231">Hallo-webservice beheren</span><span class="sxs-lookup"><span data-stu-id="4be19-231">Manage hello web service</span></span>

### <a name="manage-a-classic-web-service-in-hello-azure-classic-portal"></a><span data-ttu-id="4be19-232">Een klassieke webservice in de klassieke Azure-portal Hallo beheren</span><span class="sxs-lookup"><span data-stu-id="4be19-232">Manage a Classic web service in hello Azure classic portal</span></span>

<span data-ttu-id="4be19-233">Nadat u uw webservice klassieke hebt geïmplementeerd, kunt u het beheren van Hallo [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4be19-233">Once you've deployed your Classic web service, you can manage it from hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="4be19-234">Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="4be19-234">Sign in toohello [Azure classic portal](https://manage.windowsazure.com)</span></span>
2. <span data-ttu-id="4be19-235">In het Configuratiescherm Hallo Microsoft Azure-services, klikt u op **MACHINE LEARNING**</span><span class="sxs-lookup"><span data-stu-id="4be19-235">In hello Microsoft Azure services panel, click **MACHINE LEARNING**</span></span>
3. <span data-ttu-id="4be19-236">Klik op de werkruimte</span><span class="sxs-lookup"><span data-stu-id="4be19-236">Click your workspace</span></span>
4. <span data-ttu-id="4be19-237">Klik op Hallo **webservices** tabblad</span><span class="sxs-lookup"><span data-stu-id="4be19-237">Click hello **Web services** tab</span></span>
5. <span data-ttu-id="4be19-238">Klik op Hallo-webservice die is gemaakt</span><span class="sxs-lookup"><span data-stu-id="4be19-238">Click hello web service we created</span></span>
6. <span data-ttu-id="4be19-239">Klik op Hallo 'standaard' eindpunt</span><span class="sxs-lookup"><span data-stu-id="4be19-239">Click hello "default" endpoint</span></span>

<span data-ttu-id="4be19-240">Hier kunt u bijvoorbeeld controleren hoe Hallo webservice presteert en prestaties trucs maken door het wijzigen van het aantal gelijktijdige aanroepen Hallo-service kan verwerken.</span><span class="sxs-lookup"><span data-stu-id="4be19-240">From here, you can do things like monitor how hello web service is doing and make performance tweaks by changing how many concurrent calls hello service can handle.</span></span>

<span data-ttu-id="4be19-241">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="4be19-241">For more details, see:</span></span>

* [<span data-ttu-id="4be19-242">Eindpunten maken</span><span class="sxs-lookup"><span data-stu-id="4be19-242">Creating Endpoints</span></span>](machine-learning-create-endpoint.md)
* [<span data-ttu-id="4be19-243">Web-service schalen</span><span class="sxs-lookup"><span data-stu-id="4be19-243">Scaling web service</span></span>](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="4be19-244">Een klassieke of een nieuwe webservice in hello Azure Machine Learning-webservices portal beheren</span><span class="sxs-lookup"><span data-stu-id="4be19-244">Manage a Classic or New web service in hello Azure Machine Learning Web Services portal</span></span>

<span data-ttu-id="4be19-245">Zodra u hebt uw webservice geïmplementeerd of klassieke of nieuwe, kunt u het beheren van Hallo [Microsoft Azure Machine Learning-webservices](https://services.azureml.net/quickstart) portal.</span><span class="sxs-lookup"><span data-stu-id="4be19-245">Once you've deployed your web service, whether Classic or New, you can manage it from hello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal.</span></span>

<span data-ttu-id="4be19-246">toomonitor hello prestaties van uw web-service:</span><span class="sxs-lookup"><span data-stu-id="4be19-246">toomonitor hello performance of your web service:</span></span>

1. <span data-ttu-id="4be19-247">Meld u aan toohello [Microsoft Azure Machine Learning-webservices](https://services.azureml.net/quickstart) portal</span><span class="sxs-lookup"><span data-stu-id="4be19-247">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal</span></span>
2. <span data-ttu-id="4be19-248">Klik op **webservices**</span><span class="sxs-lookup"><span data-stu-id="4be19-248">Click **Web services**</span></span>
3. <span data-ttu-id="4be19-249">Klik op uw web-service</span><span class="sxs-lookup"><span data-stu-id="4be19-249">Click your web service</span></span>
4. <span data-ttu-id="4be19-250">Klik op Hallo **Dashboard**</span><span class="sxs-lookup"><span data-stu-id="4be19-250">Click hello **Dashboard**</span></span>

- - -
<span data-ttu-id="4be19-251">**Volgende stap: [toegang tot Hallo-webservice](machine-learning-walkthrough-6-access-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="4be19-251">**Next: [Access hello web service](machine-learning-walkthrough-6-access-web-service.md)**</span></span>

[3]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3.png
[3a]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3a.png
[4]: ./media/machine-learning-walkthrough-5-publish-web-service/publish4.png
[5]: ./media/machine-learning-walkthrough-5-publish-web-service/publish5.png
[6]: ./media/machine-learning-walkthrough-5-publish-web-service/publish6.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[metadata-editor]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[project-columns]: https://msdn.microsoft.com/en-us/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
