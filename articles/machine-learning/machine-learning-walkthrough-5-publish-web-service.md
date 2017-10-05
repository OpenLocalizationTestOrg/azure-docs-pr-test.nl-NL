---
title: 'Stap 5: De Machine Learning-webservice implementeren | Microsoft Docs'
description: 'Stap 5 van de prognose een voorspellende oplossing overzicht: een Voorspellend experiment in Machine Learning Studio als een webservice implementeert.'
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
ms.openlocfilehash: cec1bcceea158a20742c7019a266dcefaac4c9cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-5-deploy-the-azure-machine-learning-web-service"></a><span data-ttu-id="3dd48-103">Kennismaken, stap 5: De Azure Machine Learning-webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="3dd48-103">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>
<span data-ttu-id="3dd48-104">Dit is de vijfde stap van de procedure [predictive analytics-oplossing in Azure Machine Learning ontwikkelen](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="3dd48-104">This is the fifth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="3dd48-105">Een Machine Learning-werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="3dd48-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="3dd48-106">Bestaande gegevens uploaden</span><span class="sxs-lookup"><span data-stu-id="3dd48-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="3dd48-107">Een nieuw experiment maken</span><span class="sxs-lookup"><span data-stu-id="3dd48-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="3dd48-108">De modellen trainen en evalueren</span><span class="sxs-lookup"><span data-stu-id="3dd48-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. <span data-ttu-id="3dd48-109">**De webservice implementeren**</span><span class="sxs-lookup"><span data-stu-id="3dd48-109">**Deploy the web service**</span></span>
6. [<span data-ttu-id="3dd48-110">De webservice openen</span><span class="sxs-lookup"><span data-stu-id="3dd48-110">Access the web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="3dd48-111">Om de kans te gebruiken het voorspellende model dat we hebben ontwikkeld in dit overzicht anderen, kunnen we het implementeren als een webservice in Azure.</span><span class="sxs-lookup"><span data-stu-id="3dd48-111">To give others a chance to use the predictive model we've developed in this walkthrough, we can deploy it as a web service on Azure.</span></span>

<span data-ttu-id="3dd48-112">Naar dit punt Experimenteer we met het model te trainen.</span><span class="sxs-lookup"><span data-stu-id="3dd48-112">Up to this point we've been experimenting with training our model.</span></span> <span data-ttu-id="3dd48-113">Maar de geïmplementeerde service niet meer wilt doen training - gaat het genereren van nieuwe voorspellingen door score berekenen voor invoer van de gebruiker op basis van het model.</span><span class="sxs-lookup"><span data-stu-id="3dd48-113">But the deployed service is no longer going to do training - it's going to generate new predictions by scoring the user's input based on our model.</span></span> <span data-ttu-id="3dd48-114">Dus gaan we voorbereiding converteren dit experiment uit een ***training*** experimenteren naar een ***voorspellende*** experimenteren.</span><span class="sxs-lookup"><span data-stu-id="3dd48-114">So we're going to do some preparation to convert this experiment from a ***training*** experiment to a ***predictive*** experiment.</span></span> 

<span data-ttu-id="3dd48-115">Dit is een proces drie stappen:</span><span class="sxs-lookup"><span data-stu-id="3dd48-115">This is a three-step process:</span></span>  

1. <span data-ttu-id="3dd48-116">Verwijder een van de modellen</span><span class="sxs-lookup"><span data-stu-id="3dd48-116">Remove one of the models</span></span>
2. <span data-ttu-id="3dd48-117">Converteer de *trainingsexperiment* we hebt gemaakt in een *Voorspellend experiment*</span><span class="sxs-lookup"><span data-stu-id="3dd48-117">Convert the *training experiment* we've created into a *predictive experiment*</span></span>
3. <span data-ttu-id="3dd48-118">De Voorspellend experiment implementeren als een webservice</span><span class="sxs-lookup"><span data-stu-id="3dd48-118">Deploy the predictive experiment as a web service</span></span>

## <a name="remove-one-of-the-models"></a><span data-ttu-id="3dd48-119">Verwijder een van de modellen</span><span class="sxs-lookup"><span data-stu-id="3dd48-119">Remove one of the models</span></span>

<span data-ttu-id="3dd48-120">Eerst moet dit experiment enigszins trim omlaag.</span><span class="sxs-lookup"><span data-stu-id="3dd48-120">First, we need to trim this experiment down a little.</span></span> <span data-ttu-id="3dd48-121">Momenteel hebben we twee verschillende modellen in het experiment, maar we alleen wilt gebruiken één model wanneer we dit als een webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="3dd48-121">We currently have two different models in the experiment, but we only want to use one model when we deploy this as a web service.</span></span>  

<span data-ttu-id="3dd48-122">Stel, dat we hebt besloten dat de gestimuleerd structuur model beter presteert dan het SVM-model.</span><span class="sxs-lookup"><span data-stu-id="3dd48-122">Let's say we've decided that the boosted tree model performed better than the SVM model.</span></span> <span data-ttu-id="3dd48-123">Zodat het eerste wat te doen is verwijderen de [Two-Class ondersteuning Vectormachine] [ two-class-support-vector-machine] module en de modules die werden gebruikt voor het trainen van het.</span><span class="sxs-lookup"><span data-stu-id="3dd48-123">So the first thing to do is remove the [Two-Class Support Vector Machine][two-class-support-vector-machine] module and the modules that were used for training it.</span></span> <span data-ttu-id="3dd48-124">U kunt een kopie maken van het experiment eerst door te klikken op **OpslaanAls** aan de onderkant van het experimentcanvas.</span><span class="sxs-lookup"><span data-stu-id="3dd48-124">You may want to make a copy of the experiment first by clicking **Save As** at the bottom of the experiment canvas.</span></span>

<span data-ttu-id="3dd48-125">We moeten de volgende modules te verwijderen:</span><span class="sxs-lookup"><span data-stu-id="3dd48-125">We need to delete the following modules:</span></span>  

* <span data-ttu-id="3dd48-126">[Vectormachine Two-Class-ondersteuning][two-class-support-vector-machine]</span><span class="sxs-lookup"><span data-stu-id="3dd48-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span></span>
* <span data-ttu-id="3dd48-127">[Model trainen] [ train-model] en [Score Model] [ score-model] modules die zijn verbonden</span><span class="sxs-lookup"><span data-stu-id="3dd48-127">[Train Model][train-model] and [Score Model][score-model] modules that were connected to it</span></span>
* <span data-ttu-id="3dd48-128">[Gegevens normaliseren] [ normalize-data] (van beide)</span><span class="sxs-lookup"><span data-stu-id="3dd48-128">[Normalize Data][normalize-data] (both of them)</span></span>
* <span data-ttu-id="3dd48-129">[Model evalueren] [ evaluate-model] (omdat we klaar bent met het evalueren van de modellen)</span><span class="sxs-lookup"><span data-stu-id="3dd48-129">[Evaluate Model][evaluate-model] (because we're finished evaluating the models)</span></span>

<span data-ttu-id="3dd48-130">Selecteer elke module en druk op de toets Delete of met de rechtermuisknop op de module en selecteer **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="3dd48-130">Select each module and press the Delete key, or right-click the module and select **Delete**.</span></span> 

![Het model SVM verwijderd][3a]

<span data-ttu-id="3dd48-132">Het model moet nu als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="3dd48-132">Our model should now look something like this:</span></span>

![Het model SVM verwijderd][3]

<span data-ttu-id="3dd48-134">Nu we klaar zijn voor het implementeren van dit model met behulp van de [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span><span class="sxs-lookup"><span data-stu-id="3dd48-134">Now we're ready to deploy this model using the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span></span>

## <a name="convert-the-training-experiment-to-a-predictive-experiment"></a><span data-ttu-id="3dd48-135">Het trainingsexperiment converteren naar een Voorspellend experiment</span><span class="sxs-lookup"><span data-stu-id="3dd48-135">Convert the training experiment to a predictive experiment</span></span>

<span data-ttu-id="3dd48-136">Om dit model klaar voor implementatie, moet dit trainingsexperiment converteren naar een Voorspellend experiment.</span><span class="sxs-lookup"><span data-stu-id="3dd48-136">To get this model ready for deployment, we need to convert this training experiment to a predictive experiment.</span></span> <span data-ttu-id="3dd48-137">Dit omvat drie stappen:</span><span class="sxs-lookup"><span data-stu-id="3dd48-137">This involves three steps:</span></span>

1. <span data-ttu-id="3dd48-138">Sla het model dat we hebben getraind en vervang onze trainingsmodules</span><span class="sxs-lookup"><span data-stu-id="3dd48-138">Save the model we've trained and then replace our training modules</span></span>
2. <span data-ttu-id="3dd48-139">Het experiment voor het verwijderen van modules die zijn alleen nodig voor training Trim</span><span class="sxs-lookup"><span data-stu-id="3dd48-139">Trim the experiment to remove modules that were only needed for training</span></span>
3. <span data-ttu-id="3dd48-140">Definiëren waar de webservice invoer accepteert en waarin de uitvoer wordt gegenereerd</span><span class="sxs-lookup"><span data-stu-id="3dd48-140">Define where the web service will accept input and where it generates the output</span></span>

<span data-ttu-id="3dd48-141">We kunnen dit handmatig doen, maar gelukkig alle drie stappen kunnen worden uitgevoerd door te klikken op **webservice ingesteld** aan de onderkant van het experimentcanvas (en het selecteren van de **voorspellende webservice** optie).</span><span class="sxs-lookup"><span data-stu-id="3dd48-141">We could do this manually, but fortunately all three steps can be accomplished by clicking **Set Up Web Service** at the bottom of the experiment canvas (and selecting the **Predictive Web Service** option).</span></span>

> [!TIP]
> <span data-ttu-id="3dd48-142">Als u meer informatie wilt over wat er gebeurt wanneer u een trainingsexperiment converteren naar een Voorspellend experiment, Zie [uw model voorbereiden voor implementatie in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="3dd48-142">If you want more details on what happens when you convert a training experiment to a predictive experiment, see [How to prepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="3dd48-143">Wanneer u klikt op **webservice ingesteld**, op verschillende manieren gebeuren:</span><span class="sxs-lookup"><span data-stu-id="3dd48-143">When you click **Set Up Web Service**, several things happen:</span></span>

* <span data-ttu-id="3dd48-144">Het getrainde model wordt geconverteerd naar één **getrainde Model** module en opgeslagen in het modulepalet links van het experimentcanvas (u vindt deze onder **Trained Models**)</span><span class="sxs-lookup"><span data-stu-id="3dd48-144">The trained model is converted to a single **Trained Model** module and stored in the module palette to the left of the experiment canvas (you can find it under **Trained Models**)</span></span>
* <span data-ttu-id="3dd48-145">Modules die zijn gebruikt voor training zijn verwijderd; specifieke opdrachten:</span><span class="sxs-lookup"><span data-stu-id="3dd48-145">Modules that were used for training are removed; specifically:</span></span>
  * <span data-ttu-id="3dd48-146">[Two-Class gestimuleerd beslissingsstructuur][two-class-boosted-decision-tree]</span><span class="sxs-lookup"><span data-stu-id="3dd48-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span></span>
  * <span data-ttu-id="3dd48-147">[Train Model][train-model]</span><span class="sxs-lookup"><span data-stu-id="3dd48-147">[Train Model][train-model]</span></span>
  * <span data-ttu-id="3dd48-148">[Gegevens splitsen][split]</span><span class="sxs-lookup"><span data-stu-id="3dd48-148">[Split Data][split]</span></span>
  * <span data-ttu-id="3dd48-149">de tweede [R-Script uitvoeren] [ execute-r-script] module die is gebruikt voor testgegevens</span><span class="sxs-lookup"><span data-stu-id="3dd48-149">the second [Execute R Script][execute-r-script] module that was used for test data</span></span>
* <span data-ttu-id="3dd48-150">Het opgeslagen getrainde model weer toegevoegd aan het experiment</span><span class="sxs-lookup"><span data-stu-id="3dd48-150">The saved trained model is added back into the experiment</span></span>
* <span data-ttu-id="3dd48-151">**Web-invoer** en **Web service uitvoer** modules worden toegevoegd (deze vaststellen waar gegevens van de gebruiker voert het model en welke gegevens worden geretourneerd wanneer de web-service is geopend)</span><span class="sxs-lookup"><span data-stu-id="3dd48-151">**Web service input** and **Web service output** modules are added (these identify where the user's data will enter the model, and what data is returned, when the web service is accessed)</span></span>

> [!NOTE]
> <span data-ttu-id="3dd48-152">U kunt zien dat het experiment wordt opgeslagen in twee delen onder tabbladen die zijn toegevoegd aan de bovenkant van het experimentcanvas.</span><span class="sxs-lookup"><span data-stu-id="3dd48-152">You can see that the experiment is saved in two parts under tabs that have been added at the top of the experiment canvas.</span></span> <span data-ttu-id="3dd48-153">De oorspronkelijke trainingsexperiment is op het tabblad **trainingsexperiment**, en de zojuist gemaakte Voorspellend experiment ligt onder de **Voorspellend experiment**.</span><span class="sxs-lookup"><span data-stu-id="3dd48-153">The original training experiment is under the tab **Training experiment**, and the newly created predictive experiment is under **Predictive experiment**.</span></span> <span data-ttu-id="3dd48-154">De Voorspellend experiment is de die we als een webservice implementeert.</span><span class="sxs-lookup"><span data-stu-id="3dd48-154">The predictive experiment is the one we'll deploy as a web service.</span></span>

<span data-ttu-id="3dd48-155">Er moet een aanvullende stap met dit bepaalde experiment uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3dd48-155">We need to take one additional step with this particular experiment.</span></span>
<span data-ttu-id="3dd48-156">We twee toegevoegd [R-Script uitvoeren] [ execute-r-script] modules voor een functie weging tot de gegevens.</span><span class="sxs-lookup"><span data-stu-id="3dd48-156">We added two [Execute R Script][execute-r-script] modules to provide a weighting function to the data.</span></span> <span data-ttu-id="3dd48-157">Dat is slechts een slag die we nodig voor het trainen en te testen, zodat we uit deze modules in het laatste model kunt nemen.</span><span class="sxs-lookup"><span data-stu-id="3dd48-157">That was just a trick we needed for training and testing, so we can take out those modules in the final model.</span></span>
<span data-ttu-id="3dd48-158">Machine Learning Studio verwijderd een [R-Script uitvoeren] [ execute-r-script] module wanneer u deze verwijderen de [gesplitste] [ split] module.</span><span class="sxs-lookup"><span data-stu-id="3dd48-158">Machine Learning Studio removed one [Execute R Script][execute-r-script] module when it removed the [Split][split] module.</span></span> <span data-ttu-id="3dd48-159">Nu kan het andere verwijderen en verbinding maken met [metagegevens Editor] [ metadata-editor] rechtstreeks naar [Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="3dd48-159">Now we can remove the other and connect [Metadata Editor][metadata-editor] directly to [Score Model][score-model].</span></span>    

<span data-ttu-id="3dd48-160">Onze experiment ziet er nu als volgt:</span><span class="sxs-lookup"><span data-stu-id="3dd48-160">Our experiment should now look like this:</span></span>  

![Score berekenen voor het getrainde model][4]  

> [!NOTE]
> <span data-ttu-id="3dd48-162">U vraagt zich misschien af waarom we de gegevensset UCI Duits creditcardgegevens achtergebleven in de Voorspellend experiment.</span><span class="sxs-lookup"><span data-stu-id="3dd48-162">You may be wondering why we left the UCI German Credit Card Data dataset in the predictive experiment.</span></span> <span data-ttu-id="3dd48-163">De service wilt beoordelen van gegevens van de gebruiker, niet de oorspronkelijke gegevensset, dus waarom laat de oorspronkelijke gegevensset in het model?</span><span class="sxs-lookup"><span data-stu-id="3dd48-163">The service is going to score the user's data, not the original dataset, so why leave the original dataset in the model?</span></span>
> 
> <span data-ttu-id="3dd48-164">Het is waar de service hoeft niet de oorspronkelijke creditcard-gegevens.</span><span class="sxs-lookup"><span data-stu-id="3dd48-164">It's true that the service doesn't need the original credit card data.</span></span> <span data-ttu-id="3dd48-165">Maar hoeft het schema voor die gegevens, waaronder gegevens zoals het aantal kolommen zijn en welke kolommen numeriek zijn.</span><span class="sxs-lookup"><span data-stu-id="3dd48-165">But it does need the schema for that data, which includes information such as how many columns there are and which columns are numeric.</span></span> <span data-ttu-id="3dd48-166">Dit schema-informatie is nodig om gegevens van de gebruiker te interpreteren.</span><span class="sxs-lookup"><span data-stu-id="3dd48-166">This schema information is necessary to interpret the user's data.</span></span> <span data-ttu-id="3dd48-167">We laten deze onderdelen die zijn verbonden, zodat de scoremodule het schema van de dataset heeft wanneer de service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3dd48-167">We leave these components connected so that the scoring module has the dataset schema when the service is running.</span></span> <span data-ttu-id="3dd48-168">De gegevens wordt niet gebruikt, alleen het schema.</span><span class="sxs-lookup"><span data-stu-id="3dd48-168">The data isn't used, just the schema.</span></span>  
> 
> 

<span data-ttu-id="3dd48-169">Voer het experiment outproblemen (Klik op **uitvoeren**.) Als u controleren wilt of het model nog steeds werkt, klikt u op de uitvoer van de [Score Model] [ score-model] module en selecteer **resultaten weergeven**.</span><span class="sxs-lookup"><span data-stu-id="3dd48-169">Run the experiment one last time (click **Run**.) If you want to verify that the model is still working, click the output of the [Score Model][score-model] module and select **View Results**.</span></span> <span data-ttu-id="3dd48-170">U kunt zien dat de oorspronkelijke gegevens worden weergegeven, samen met de waarde van tegoed risico's ('Scored Labels') en de scoreprofiel waarschijnlijkheidswaarde ('berekend kansen'.)</span><span class="sxs-lookup"><span data-stu-id="3dd48-170">You can see that the original data is displayed, along with the credit risk value ("Scored Labels") and the scoring probability value ("Scored Probabilities".)</span></span> 

## <a name="deploy-the-web-service"></a><span data-ttu-id="3dd48-171">De webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="3dd48-171">Deploy the web service</span></span>
<span data-ttu-id="3dd48-172">U kunt het experiment implementeren als ofwel Classic webservice of als een nieuwe webservice die gebaseerd op Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3dd48-172">You can deploy the experiment as either a Classic web service, or as a New web service that's based on Azure Resource Manager.</span></span>

### <a name="deploy-as-a-classic-web-service"></a><span data-ttu-id="3dd48-173">Als een klassiek-webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="3dd48-173">Deploy as a Classic web service</span></span>
<span data-ttu-id="3dd48-174">Klik voor het implementeren van een klassiek-webservice die is afgeleid van onze experiment **webservice implementeren** onder het canvas en selecteer **webservice implementeren [klassieke]**.</span><span class="sxs-lookup"><span data-stu-id="3dd48-174">To deploy a Classic web service derived from our experiment, click **Deploy Web Service** below the canvas and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="3dd48-175">Machine Learning Studio implementeert het experiment als een webservice en gaat u naar het dashboard voor de webservice.</span><span class="sxs-lookup"><span data-stu-id="3dd48-175">Machine Learning Studio deploys the experiment as a web service and takes you to the dashboard for that web service.</span></span> <span data-ttu-id="3dd48-176">Op deze pagina kunt u terugkeren naar het experimentcanvas (**weergave momentopname** of **geven het meest recente**) en een eenvoudige test van de webservice wordt uitgevoerd (Zie **testen van de webservice** hieronder).</span><span class="sxs-lookup"><span data-stu-id="3dd48-176">From this page you can return to the experiment (**View snapshot** or **View latest**) and run a simple test of the web service (see **Test the web service** below).</span></span> <span data-ttu-id="3dd48-177">Er is ook hier informatie voor het maken van toepassingen die toegang heeft tot de webservice (meer informatie over die in de volgende stap van deze rondleiding).</span><span class="sxs-lookup"><span data-stu-id="3dd48-177">There is also information here for creating applications that can access the web service (more on that in the next step of this walkthrough).</span></span>

![Web service-dashboard][6]

<span data-ttu-id="3dd48-179">U kunt de service configureren door te klikken op de **configuratie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="3dd48-179">You can configure the service by clicking the **CONFIGURATION** tab.</span></span> <span data-ttu-id="3dd48-180">Hier kunt u de naam van de service (dit is de naam van het experiment standaard toegekend) wijzigen en wijs hieraan een beschrijving.</span><span class="sxs-lookup"><span data-stu-id="3dd48-180">Here you can modify the service name (it's given the experiment name by default) and give it a description.</span></span> <span data-ttu-id="3dd48-181">U kunt ook meer beschrijvende labels geven voor de invoer- en -gegevens.</span><span class="sxs-lookup"><span data-stu-id="3dd48-181">You can also give more friendly labels for the input and output data.</span></span>  

![Configureer de webservice][5]  

### <a name="deploy-as-a-new-web-service"></a><span data-ttu-id="3dd48-183">Als een nieuwe webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="3dd48-183">Deploy as a New web service</span></span>

> [!NOTE] 
> <span data-ttu-id="3dd48-184">Voor het implementeren van een nieuwe webservice moet u voldoende machtigingen hebben in het abonnement waaraan u de webservice implementeert.</span><span class="sxs-lookup"><span data-stu-id="3dd48-184">To deploy a New web service you must have sufficient permissions in the subscription to which you are deploying the web service.</span></span> <span data-ttu-id="3dd48-185">Zie voor meer informatie [beheren van een webservice via de portal voor Azure Machine Learning-webservices](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="3dd48-185">For more information, see [Manage a web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="3dd48-186">Voor het implementeren van een nieuwe webservice afgeleid van onze experiment:</span><span class="sxs-lookup"><span data-stu-id="3dd48-186">To deploy a New web service derived from our experiment:</span></span>

1. <span data-ttu-id="3dd48-187">Klik op **webservice implementeren** onder het canvas en selecteer **Web Service implementeren [New]**.</span><span class="sxs-lookup"><span data-stu-id="3dd48-187">Click **Deploy Web Service** below the canvas and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="3dd48-188">Machine Learning Studio brengt u naar de Azure Machine Learning-webservices **implementeren Experiment** pagina.</span><span class="sxs-lookup"><span data-stu-id="3dd48-188">Machine Learning Studio transfers you to the Azure Machine Learning web services **Deploy Experiment** page.</span></span>

2. <span data-ttu-id="3dd48-189">Voer een naam voor de webservice.</span><span class="sxs-lookup"><span data-stu-id="3dd48-189">Enter a name for the web service.</span></span> 

3. <span data-ttu-id="3dd48-190">Voor **prijs Plan**, kan een bestaande prijscategorie selecteren of 'Nieuw maken' en geef een naam op voor het nieuwe plan en selecteer de optie voor maandelijks plannen.</span><span class="sxs-lookup"><span data-stu-id="3dd48-190">For **Price Plan**, you can select an existing pricing plan, or select "Create new" and give the new plan a name and select the monthly plan option.</span></span> <span data-ttu-id="3dd48-191">De standaardwaarde van de lagen abonnement op de plannen voor uw regio standaard en uw web-service wordt geïmplementeerd in deze regio.</span><span class="sxs-lookup"><span data-stu-id="3dd48-191">The plan tiers default to the plans for your default region and your web service is deployed to that region.</span></span>

4. <span data-ttu-id="3dd48-192">Klik op **implementeren**.</span><span class="sxs-lookup"><span data-stu-id="3dd48-192">Click **Deploy**.</span></span>

<span data-ttu-id="3dd48-193">Na een paar minuten de **Quick Start** pagina voor uw webservice wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="3dd48-193">After a few minutes, the **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="3dd48-194">U kunt de service configureren door te klikken op de **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="3dd48-194">You can configure the service by clicking the **Configure** tab.</span></span> <span data-ttu-id="3dd48-195">Hier kunt u de service wijzigen title en wijs hieraan een beschrijving.</span><span class="sxs-lookup"><span data-stu-id="3dd48-195">Here you can modify the service title and give it a description.</span></span> 

<span data-ttu-id="3dd48-196">Als u wilt testen van de webservice, klikt u op de **testen** tabblad (Zie **testen van de webservice** hieronder).</span><span class="sxs-lookup"><span data-stu-id="3dd48-196">To test the web service, click the **Test** tab (see **Test the web service** below).</span></span> <span data-ttu-id="3dd48-197">Voor informatie over het maken van toepassingen die toegang heeft tot de webservice, klikt u op de **verbruiken** tabblad (de volgende stap in dit scenario gaat in meer detail).</span><span class="sxs-lookup"><span data-stu-id="3dd48-197">For information on creating applications that can access the web service, click the **Consume** tab (the next step in this walkthrough will go into more detail).</span></span>

> [!TIP]
> <span data-ttu-id="3dd48-198">Nadat u deze hebt geïmplementeerd, kunt u de webservice bijwerken.</span><span class="sxs-lookup"><span data-stu-id="3dd48-198">You can update the web service after you've deployed it.</span></span> <span data-ttu-id="3dd48-199">Bijvoorbeeld, als u uw model wijzigen wilt en vervolgens kunt u het trainingsexperiment, aanpassen van de Modelparameters en klikt u op **webservice implementeren**, selecteren **webservice implementeren [klassieke]** of **[New]-webservice implementeren**.</span><span class="sxs-lookup"><span data-stu-id="3dd48-199">For example, if you want to change your model, then you can edit the training experiment, tweak the model parameters, and click **Deploy Web Service**, selecting **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span> <span data-ttu-id="3dd48-200">Wanneer u het experiment opnieuw implementeert, vervangt dan de web-service, nu met gebruik van uw bijgewerkte model.</span><span class="sxs-lookup"><span data-stu-id="3dd48-200">When you deploy the experiment again, it replaces the web service, now using your updated model.</span></span>  
> 
> 

## <a name="test-the-web-service"></a><span data-ttu-id="3dd48-201">De webservice testen</span><span class="sxs-lookup"><span data-stu-id="3dd48-201">Test the web service</span></span>

<span data-ttu-id="3dd48-202">Als de webservice wordt geopend, krijgt de gegevens van de gebruiker via de **Web service invoer** module waar wordt doorgegeven aan de [Score Model] [ score-model] module en gewaardeerd.</span><span class="sxs-lookup"><span data-stu-id="3dd48-202">When the web service is accessed, the user's data enters through the **Web service input** module where it's passed to the [Score Model][score-model] module and scored.</span></span> <span data-ttu-id="3dd48-203">De manier waarop die we de Voorspellend experiment hebt ingesteld, het model verwacht gegevens in dezelfde indeling als de oorspronkelijke tegoed risico gegevensset.</span><span class="sxs-lookup"><span data-stu-id="3dd48-203">The way we've set up the predictive experiment, the model expects data in the same format as the original credit risk dataset.</span></span>
<span data-ttu-id="3dd48-204">De resultaten worden geretourneerd naar de gebruiker van de webservice via de **Web service uitvoer** module.</span><span class="sxs-lookup"><span data-stu-id="3dd48-204">The results are returned to the user from the web service through the **Web service output** module.</span></span>

> [!TIP]
> <span data-ttu-id="3dd48-205">De manier waarop we de Voorspellend experiment geconfigureerd, hebben de gehele resultaat is van de [Score Model] [ score-model] module worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3dd48-205">The way we have the predictive experiment configured, the entire results from the [Score Model][score-model] module are returned.</span></span> <span data-ttu-id="3dd48-206">Dit omvat alle ingevoerde gegevens plus de tegoed risico waarde en de kans op scoreprofiel.</span><span class="sxs-lookup"><span data-stu-id="3dd48-206">This includes all the input data plus the credit risk value and the scoring probability.</span></span> <span data-ttu-id="3dd48-207">Maar u kunt een iets andere betekenis als u wilt terugkeren - u kan bijvoorbeeld alleen de tegoed risico waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="3dd48-207">But you can return something different if you want - for example, you could return just the credit risk value.</span></span> <span data-ttu-id="3dd48-208">U doet dit door invoegen een [Projectkolommen] [ project-columns] module tussen [Score Model] [ score-model] en de **Web service uitvoer**elimineren kolommen u niet wilt dat de webservice om terug te keren.</span><span class="sxs-lookup"><span data-stu-id="3dd48-208">To do this, insert a [Project Columns][project-columns] module between [Score Model][score-model] and the **Web service output** to eliminate columns you don't want the web service to return.</span></span> 
> 
> 

<span data-ttu-id="3dd48-209">U kunt een klassiek web testen in service **Machine Learning Studio** of in de **Azure Machine Learning-webservices** portal.</span><span class="sxs-lookup"><span data-stu-id="3dd48-209">You can test a Classic web service either in **Machine Learning Studio** or in the **Azure Machine Learning Web Services** portal.</span></span>
<span data-ttu-id="3dd48-210">U kunt een nieuw web testen service alleen in de **Machine Learning-webservices** portal.</span><span class="sxs-lookup"><span data-stu-id="3dd48-210">You can test a New web service only in the **Machine Learning Web Services** portal.</span></span>

> [!TIP]
> <span data-ttu-id="3dd48-211">Wanneer u in de portal voor Azure Machine Learning-webservices test, kunt u de portal voorbeeldgegevens die u gebruiken kunt voor het testen van de service aanvragen en antwoorden maken kunt hebben.</span><span class="sxs-lookup"><span data-stu-id="3dd48-211">When testing in the Azure Machine Learning Web Services portal, you can have the portal create sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="3dd48-212">Op de **configureren** pagina, selecteert u 'Ja' voor **voorbeeld gegevens ingeschakeld?**.</span><span class="sxs-lookup"><span data-stu-id="3dd48-212">On the **Configure** page, select "Yes" for **Sample Data Enabled?**.</span></span> <span data-ttu-id="3dd48-213">Wanneer u opent het tabblad aanvragen en antwoorden op de **Test** pagina de portal ingevuld voorbeeldgegevens die afkomstig zijn uit de oorspronkelijke tegoed risico gegevensset.</span><span class="sxs-lookup"><span data-stu-id="3dd48-213">When you open the Request-Response tab on the **Test** page, the portal fills in sample data taken from the original credit risk dataset.</span></span>

### <a name="test-a-classic-web-service"></a><span data-ttu-id="3dd48-214">Een klassieke webservice testen</span><span class="sxs-lookup"><span data-stu-id="3dd48-214">Test a Classic web service</span></span>

<span data-ttu-id="3dd48-215">U kunt een webservice klassieke testen in Machine Learning Studio of in de portal van de Machine Learning-webservices.</span><span class="sxs-lookup"><span data-stu-id="3dd48-215">You can test a Classic web service in Machine Learning Studio or in the Machine Learning Web Services portal.</span></span> 

#### <a name="test-in-machine-learning-studio"></a><span data-ttu-id="3dd48-216">Testen in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="3dd48-216">Test in Machine Learning Studio</span></span>

1. <span data-ttu-id="3dd48-217">Op de **DASHBOARD** pagina voor de webservice, klikt u op de **Test** knop onder **eindpunt standaard**.</span><span class="sxs-lookup"><span data-stu-id="3dd48-217">On the **DASHBOARD** page for the web service, click the **Test** button under **Default Endpoint**.</span></span> <span data-ttu-id="3dd48-218">Een dialoogvenster weergegeven en u wordt gevraagd de invoergegevens van de service.</span><span class="sxs-lookup"><span data-stu-id="3dd48-218">A dialog pops up and asks you for the input data for the service.</span></span> <span data-ttu-id="3dd48-219">Dit zijn dezelfde kolommen die zijn opgetreden in de oorspronkelijke tegoed risico gegevensset.</span><span class="sxs-lookup"><span data-stu-id="3dd48-219">These are the same columns that appeared in the original credit risk dataset.</span></span>  

2. <span data-ttu-id="3dd48-220">Geef een set gegevens en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3dd48-220">Enter a set of data and then click **OK**.</span></span> 

#### <a name="test-in-the-machine-learning-web-services-portal"></a><span data-ttu-id="3dd48-221">Testen in de portal voor Machine Learning-webservices</span><span class="sxs-lookup"><span data-stu-id="3dd48-221">Test in the Machine Learning Web Services portal</span></span>

1. <span data-ttu-id="3dd48-222">Op de **DASHBOARD** pagina voor de webservice, klikt u op de **Test preview** koppeling onder **eindpunt standaard**.</span><span class="sxs-lookup"><span data-stu-id="3dd48-222">On the **DASHBOARD** page for the web service, click the **Test preview** link under **Default Endpoint**.</span></span> <span data-ttu-id="3dd48-223">De testpagina in de portal voor Azure Machine Learning-webservices voor de webservice-eindpunt wordt geopend en u wordt gevraagd de invoergegevens van de service.</span><span class="sxs-lookup"><span data-stu-id="3dd48-223">The test page in the Azure Machine Learning Web Services portal for the web service endpoint opens and asks you for the input data for the service.</span></span> <span data-ttu-id="3dd48-224">Dit zijn dezelfde kolommen die zijn opgetreden in de oorspronkelijke tegoed risico gegevensset.</span><span class="sxs-lookup"><span data-stu-id="3dd48-224">These are the same columns that appeared in the original credit risk dataset.</span></span>

2. <span data-ttu-id="3dd48-225">Klik op **testen aanvragen en antwoorden**.</span><span class="sxs-lookup"><span data-stu-id="3dd48-225">Click **Test Request-Response**.</span></span> 

### <a name="test-a-new-web-service"></a><span data-ttu-id="3dd48-226">Een nieuwe webservice testen</span><span class="sxs-lookup"><span data-stu-id="3dd48-226">Test a New web service</span></span>

<span data-ttu-id="3dd48-227">U kunt een nieuwe webservice testen alleen in de portal voor Machine Learning-webservices.</span><span class="sxs-lookup"><span data-stu-id="3dd48-227">You can test a New web service only in the Machine Learning Web Services portal.</span></span>

1. <span data-ttu-id="3dd48-228">In de [Azure Machine Learning-webservices](https://services.azureml.net/quickstart) en klik op **Test** boven aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="3dd48-228">In the [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal, click **Test** at the top of the page.</span></span> <span data-ttu-id="3dd48-229">De **Test** pagina wordt geopend en u kunt gegevens voor de service.</span><span class="sxs-lookup"><span data-stu-id="3dd48-229">The **Test** page opens and you can input data for the service.</span></span> <span data-ttu-id="3dd48-230">De invoervelden weergegeven overeenkomen met de kolommen die zijn opgetreden in de oorspronkelijke tegoed risico gegevensset.</span><span class="sxs-lookup"><span data-stu-id="3dd48-230">The input fields displayed correspond to the columns that appeared in the original credit risk dataset.</span></span> 

2. <span data-ttu-id="3dd48-231">Geef een set gegevens en klik op **Test aanvragen en antwoorden**.</span><span class="sxs-lookup"><span data-stu-id="3dd48-231">Enter a set of data and then click **Test Request-Response**.</span></span>

<span data-ttu-id="3dd48-232">De resultaten van de test worden weergegeven aan de rechterkant van de pagina in de uitvoerkolom.</span><span class="sxs-lookup"><span data-stu-id="3dd48-232">The results of the test are displayed on the right-hand side of the page in the output column.</span></span> 


## <a name="manage-the-web-service"></a><span data-ttu-id="3dd48-233">De webservice beheren</span><span class="sxs-lookup"><span data-stu-id="3dd48-233">Manage the web service</span></span>

### <a name="manage-a-classic-web-service-in-the-azure-classic-portal"></a><span data-ttu-id="3dd48-234">Een klassieke webservice in de klassieke Azure portal beheren</span><span class="sxs-lookup"><span data-stu-id="3dd48-234">Manage a Classic web service in the Azure classic portal</span></span>

<span data-ttu-id="3dd48-235">Als u uw webservice klassieke hebt geïmplementeerd, kunt u het beheren van de [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="3dd48-235">Once you've deployed your Classic web service, you can manage it from the [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="3dd48-236">Aanmelden bij de [klassieke Azure-portal](https://manage.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="3dd48-236">Sign in to the [Azure classic portal](https://manage.windowsazure.com)</span></span>
2. <span data-ttu-id="3dd48-237">Klik in het deelvenster Microsoft Azure-services op **MACHINE LEARNING**</span><span class="sxs-lookup"><span data-stu-id="3dd48-237">In the Microsoft Azure services panel, click **MACHINE LEARNING**</span></span>
3. <span data-ttu-id="3dd48-238">Klik op de werkruimte</span><span class="sxs-lookup"><span data-stu-id="3dd48-238">Click your workspace</span></span>
4. <span data-ttu-id="3dd48-239">Klik op de **webservices** tabblad</span><span class="sxs-lookup"><span data-stu-id="3dd48-239">Click the **Web services** tab</span></span>
5. <span data-ttu-id="3dd48-240">Klik op de webservice die is gemaakt</span><span class="sxs-lookup"><span data-stu-id="3dd48-240">Click the web service we created</span></span>
6. <span data-ttu-id="3dd48-241">Klik op het eindpunt 'standaard'</span><span class="sxs-lookup"><span data-stu-id="3dd48-241">Click the "default" endpoint</span></span>

<span data-ttu-id="3dd48-242">Hier kunt u doen zoals controleren hoe de webservice presteert en controleer prestaties trucs door het wijzigen van het aantal gelijktijdige roept de service kunnen verwerken.</span><span class="sxs-lookup"><span data-stu-id="3dd48-242">From here, you can do things like monitor how the web service is doing and make performance tweaks by changing how many concurrent calls the service can handle.</span></span>

<span data-ttu-id="3dd48-243">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="3dd48-243">For more details, see:</span></span>

* [<span data-ttu-id="3dd48-244">Eindpunten maken</span><span class="sxs-lookup"><span data-stu-id="3dd48-244">Creating Endpoints</span></span>](machine-learning-create-endpoint.md)
* [<span data-ttu-id="3dd48-245">Web-service schalen</span><span class="sxs-lookup"><span data-stu-id="3dd48-245">Scaling web service</span></span>](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="3dd48-246">Een klassieke of een nieuwe webservice in de portal voor Azure Machine Learning-webservices worden beheerd</span><span class="sxs-lookup"><span data-stu-id="3dd48-246">Manage a Classic or New web service in the Azure Machine Learning Web Services portal</span></span>

<span data-ttu-id="3dd48-247">Als u hebt uw webservice geïmplementeerd of klassieke of nieuwe, kunt u het beheren van de [Microsoft Azure Machine Learning-webservices](https://services.azureml.net/quickstart) portal.</span><span class="sxs-lookup"><span data-stu-id="3dd48-247">Once you've deployed your web service, whether Classic or New, you can manage it from the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal.</span></span>

<span data-ttu-id="3dd48-248">Voor het bewaken van de prestaties van uw web-service:</span><span class="sxs-lookup"><span data-stu-id="3dd48-248">To monitor the performance of your web service:</span></span>

1. <span data-ttu-id="3dd48-249">Aanmelden bij de [Microsoft Azure Machine Learning-webservices](https://services.azureml.net/quickstart) portal</span><span class="sxs-lookup"><span data-stu-id="3dd48-249">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal</span></span>
2. <span data-ttu-id="3dd48-250">Klik op **webservices**</span><span class="sxs-lookup"><span data-stu-id="3dd48-250">Click **Web services**</span></span>
3. <span data-ttu-id="3dd48-251">Klik op uw web-service</span><span class="sxs-lookup"><span data-stu-id="3dd48-251">Click your web service</span></span>
4. <span data-ttu-id="3dd48-252">Klik op de **Dashboard**</span><span class="sxs-lookup"><span data-stu-id="3dd48-252">Click the **Dashboard**</span></span>

- - -
<span data-ttu-id="3dd48-253">**Volgende stap: [toegang tot de webservice](machine-learning-walkthrough-6-access-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="3dd48-253">**Next: [Access the web service](machine-learning-walkthrough-6-access-web-service.md)**</span></span>

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
