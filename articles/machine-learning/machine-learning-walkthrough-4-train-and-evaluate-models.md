---
title: 'Stap 4: Trainen en evalueren van voorspellende analytische modellen Hallo | Microsoft Docs'
description: 'Stap 4 van Hallo een overzicht van de voorspellende oplossing ontwikkelen: trein, beoordelen en evalueren van meerdere modellen in Azure Machine Learning Studio.'
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a><span data-ttu-id="53287-103">Scenario-stap 4: Trainen en evalueren Hallo voorspellende analytische modellen</span><span class="sxs-lookup"><span data-stu-id="53287-103">Walkthrough Step 4: Train and evaluate hello predictive analytic models</span></span>
<span data-ttu-id="53287-104">Dit onderwerp bevat Hallo vierde stap van Hallo scenario [predictive analytics-oplossing in Azure Machine Learning ontwikkelen](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="53287-104">This topic contains hello fourth step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="53287-105">Een Machine Learning-werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="53287-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="53287-106">Bestaande gegevens uploaden</span><span class="sxs-lookup"><span data-stu-id="53287-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="53287-107">Een nieuw experiment maken</span><span class="sxs-lookup"><span data-stu-id="53287-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="53287-108">**Trainen en evalueren Hallo modellen**</span><span class="sxs-lookup"><span data-stu-id="53287-108">**Train and evaluate hello models**</span></span>
5. [<span data-ttu-id="53287-109">Hallo-webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="53287-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="53287-110">Toegang tot Hallo-webservice</span><span class="sxs-lookup"><span data-stu-id="53287-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="53287-111">Een van de voordelen van het gebruik van Azure Machine Learning Studio voor het maken van machine learning-modellen Hallo Hallo mogelijkheid tootry meer dan één type model is op een tijd in een enkel experiment en vergelijk Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="53287-111">One of hello benefits of using Azure Machine Learning Studio for creating machine learning models is hello ability tootry more than one type of model at a time in a single experiment and compare hello results.</span></span> <span data-ttu-id="53287-112">Dit type experimenteren kunt u de beste oplossing Hallo vinden voor uw probleem.</span><span class="sxs-lookup"><span data-stu-id="53287-112">This type of experimentation helps you find hello best solution for your problem.</span></span>

<span data-ttu-id="53287-113">Hallo-experiment we in dit overzicht ontwikkelt, we twee verschillende soorten modellen maken en vervolgens welk algoritme vergelijken hun scoreprofiel resultaten toodecide willen we toouse in onze laatste experiment.</span><span class="sxs-lookup"><span data-stu-id="53287-113">In hello experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results toodecide which algorithm we want toouse in our final experiment.</span></span>  

<span data-ttu-id="53287-114">Er zijn verschillende modellen die we kan kiezen uit.</span><span class="sxs-lookup"><span data-stu-id="53287-114">There are various models we could choose from.</span></span> <span data-ttu-id="53287-115">toosee hello modellen die beschikbaar is, vouw Hallo **Machine Learning** knooppunt in het modulepalet hello, en vouw vervolgens **Model initialiseren** en Hallo knooppunten eronder.</span><span class="sxs-lookup"><span data-stu-id="53287-115">toosee hello models available, expand hello **Machine Learning** node in hello module palette, and then expand **Initialize Model** and hello nodes beneath it.</span></span> <span data-ttu-id="53287-116">Voor Hallo toepassing van dit experiment, selecteren we Hallo [Two-Class ondersteuning Vectormachine] [ two-class-support-vector-machine] (SVM) en Hallo [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] modules.</span><span class="sxs-lookup"><span data-stu-id="53287-116">For hello purposes of this experiment, we'll select hello [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="53287-117">help van tooget beslist welke Machine Learning-algoritme beste tegemoetkomt aan Hallo bepaald probleem probeert u toosolve, Zie [hoe toochoose algoritmen voor Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span><span class="sxs-lookup"><span data-stu-id="53287-117">tooget help deciding which Machine Learning algorithm best suits hello particular problem you're trying toosolve, see [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-hello-models"></a><span data-ttu-id="53287-118">Hallo modellen trainen</span><span class="sxs-lookup"><span data-stu-id="53287-118">Train hello models</span></span>

<span data-ttu-id="53287-119">We voegen toe beide Hallo [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] module en [Two-Class ondersteuning Vectormachine] [ two-class-support-vector-machine] module in dit experiment.</span><span class="sxs-lookup"><span data-stu-id="53287-119">We'll add both hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="53287-120">Two-Class gestimuleerd beslissingsstructuur</span><span class="sxs-lookup"><span data-stu-id="53287-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="53287-121">Eerst laten we instellen Hallo boosted decision tree model.</span><span class="sxs-lookup"><span data-stu-id="53287-121">First, let's set up hello boosted decision tree model.</span></span>

1. <span data-ttu-id="53287-122">Hallo zoeken [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] -module in het modulepalet hello en sleep deze naar Hallo canvas.</span><span class="sxs-lookup"><span data-stu-id="53287-122">Find hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="53287-123">Hallo zoeken [Train Model] [ train-model] -module, sleep deze naar het canvas Hallo en sluit vervolgens Hallo uitvoer Hallo [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree]module toohello links invoerpoort Hallo [Train Model] [ train-model] module.</span><span class="sxs-lookup"><span data-stu-id="53287-123">Find hello [Train Model][train-model] module, drag it onto hello canvas, and then connect hello output of hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="53287-124">Hallo [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] module initialiseert de algemene model Hallo en [Train Model] [ train-model] trainingsgegevens gebruikt tootrain Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="53287-124">hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes hello generic model, and [Train Model][train-model] uses training data tootrain hello model.</span></span> 

3. <span data-ttu-id="53287-125">Verbinding maken met de Hallo links uitvoer van Hallo links [R-Script uitvoeren] [ execute-r-script] module toohello rechts invoer poort Hallo [Train Model] [ train-model] module (we besloten [stap 3](machine-learning-walkthrough-3-create-new-experiment.md) van deze stapsgewijze Kennismaking toouse Hallo gegevens afkomstig zijn van de linkerkant van Hallo Split Data-module voor training Hallo).</span><span class="sxs-lookup"><span data-stu-id="53287-125">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello right input port of hello [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough toouse hello data coming from hello left side of hello Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="53287-126">We hebben twee Hallo invoer en een van de uitvoer Hallo Hallo [R-Script uitvoeren] [ execute-r-script] -module voor dit experiment, zodat we kunt ze niet-gekoppelde laten.</span><span class="sxs-lookup"><span data-stu-id="53287-126">We don't need two of hello inputs and one of hello outputs of hello [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="53287-127">Dit gedeelte van het Hallo-experiment ziet nu er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="53287-127">This portion of hello experiment now looks something like this:</span></span>  

![Een model trainen][1]

<span data-ttu-id="53287-129">Nu tootell hello moet [Train Model] [ train-model] module dat we Hallo model toopredict Hallo kredietrisico waarde wilt bepalen.</span><span class="sxs-lookup"><span data-stu-id="53287-129">Now we need tootell hello [Train Model][train-model] module that we want hello model toopredict hello Credit Risk value.</span></span>

1. <span data-ttu-id="53287-130">Selecteer Hallo [Train Model] [ train-model] module.</span><span class="sxs-lookup"><span data-stu-id="53287-130">Select hello [Train Model][train-model] module.</span></span> <span data-ttu-id="53287-131">In Hallo **eigenschappen** deelvenster, klikt u op **Launch column selector**.</span><span class="sxs-lookup"><span data-stu-id="53287-131">In hello **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="53287-132">In Hallo **één kolom selecteren** dialoogvenster Typ 'kredietrisico' hello zoekveld opgegeven onder **beschikbare kolommen**'Kredietrisico' hieronder selecteert en klikt u op de pijlknop-rechts hello ( **>** ) toomove 'Kredietrisico' te**geselecteerde kolommen**.</span><span class="sxs-lookup"><span data-stu-id="53287-132">In hello **Select a single column** dialog, type "credit risk" in hello search field under **Available Columns**, select "Credit risk" below, and click hello right arrow button (**>**) toomove "Credit risk" too**Selected Columns**.</span></span> 

    ![Hallo kredietrisico kolom voor Hallo Train Model-module selecteren][0]

3. <span data-ttu-id="53287-134">Klik op Hallo **OK** selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="53287-134">Click hello **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="53287-135">Two-Class Support Vector Machine</span><span class="sxs-lookup"><span data-stu-id="53287-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="53287-136">Vervolgens stelt Hallo SVM model.</span><span class="sxs-lookup"><span data-stu-id="53287-136">Next, we set up hello SVM model.</span></span>  

<span data-ttu-id="53287-137">Eerste, uitleg over SVM.</span><span class="sxs-lookup"><span data-stu-id="53287-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="53287-138">Gestimuleerd beslissingsstructuren werken goed met functies van elk type.</span><span class="sxs-lookup"><span data-stu-id="53287-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="53287-139">Aangezien Hallo SVM module een lineaire classificatie genereert, Hallo model die wordt gegenereerd heeft echter aanbevolen testfout Hallo wanneer alle functies van de numerieke Hallo hebt dezelfde schaal.</span><span class="sxs-lookup"><span data-stu-id="53287-139">However, since hello SVM module generates a linear classifier, hello model that it generates has hello best test error when all numeric features have hello same scale.</span></span> <span data-ttu-id="53287-140">alle numerieke tooconvert functies toohello dezelfde schalen, gebruiken we een 'Tanh' transformatie (Hello [gegevens normaliseren] [ normalize-data] module).</span><span class="sxs-lookup"><span data-stu-id="53287-140">tooconvert all numeric features toohello same scale, we use a "Tanh" transformation (with hello [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="53287-141">Hiermee transformeert onze cijfers in bereik Hallo [0,1].</span><span class="sxs-lookup"><span data-stu-id="53287-141">This transforms our numbers into hello [0,1] range.</span></span> <span data-ttu-id="53287-142">Hallo SVM module converteert tekenreeks functies toocategorical functies en onderdelen toobinary 0/1, zodat we niet nodig toomanually transformeert u functies van de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="53287-142">hello SVM module converts string features toocategorical features and then toobinary 0/1 features, so we don't need toomanually transform string features.</span></span> <span data-ttu-id="53287-143">Bovendien we willen tootransform Hallo kredietrisico kolom (kolom 21) niet - numerieke is, maar het is Hallo waarde we je training Hallo model toopredict, dus moeten we er tooleave deze alleen.</span><span class="sxs-lookup"><span data-stu-id="53287-143">Also, we don't want tootransform hello Credit Risk column (column 21) - it's numeric, but it's hello value we're training hello model toopredict, so we need tooleave it alone.</span></span>  

<span data-ttu-id="53287-144">tooset up Hallo SVM model, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="53287-144">tooset up hello SVM model, do hello following:</span></span>

1. <span data-ttu-id="53287-145">Hallo zoeken [Two-Class ondersteuning Vectormachine] [ two-class-support-vector-machine] -module in het modulepalet hello en sleep deze naar Hallo canvas.</span><span class="sxs-lookup"><span data-stu-id="53287-145">Find hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="53287-146">Met de rechtermuisknop op Hallo [Train Model] [ train-model] -module, selecteer **kopie**, klik met de rechtermuisknop op het canvas Hallo en selecteer **plakken**.</span><span class="sxs-lookup"><span data-stu-id="53287-146">Right-click hello [Train Model][train-model] module, select **Copy**, and then right-click hello canvas and select **Paste**.</span></span> <span data-ttu-id="53287-147">kopie van Hallo Hallo [Train Model] [ train-model] module Hallo heeft dezelfde kolom selecteren als de oorspronkelijke Hallo.</span><span class="sxs-lookup"><span data-stu-id="53287-147">hello copy of hello [Train Model][train-model] module has hello same column selection as hello original.</span></span>

3. <span data-ttu-id="53287-148">Verbinding maken met uitvoer Hallo Hallo [Two-Class ondersteuning Vectormachine] [ two-class-support-vector-machine] module toohello links invoerpoort Hallo tweede [Train Model] [ train-model] module.</span><span class="sxs-lookup"><span data-stu-id="53287-148">Connect hello output of hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module toohello left input port of hello second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="53287-149">Hallo zoeken [gegevens normaliseren] [ normalize-data] module en sleep deze naar Hallo canvas.</span><span class="sxs-lookup"><span data-stu-id="53287-149">Find hello [Normalize Data][normalize-data] module and drag it onto hello canvas.</span></span>

5. <span data-ttu-id="53287-150">Verbinding maken met de Hallo links uitvoer van Hallo links [R-Script uitvoeren] [ execute-r-script] module-invoer toohello van deze module (Let op de uitvoerpoort Hallo van een module mogelijk verbonden toomore dan een andere module).</span><span class="sxs-lookup"><span data-stu-id="53287-150">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello input of this module (notice that hello output port of a module may be connected toomore than one other module).</span></span>

6. <span data-ttu-id="53287-151">Hallo links uitvoerpoort Hallo verbinding [gegevens normaliseren] [ normalize-data] module toohello rechts poort Hallo tweede invoer [Train Model] [ train-model] module.</span><span class="sxs-lookup"><span data-stu-id="53287-151">Connect hello left output port of hello [Normalize Data][normalize-data] module toohello right input port of hello second [Train Model][train-model] module.</span></span>

<span data-ttu-id="53287-152">Dit gedeelte van onze experiment moet nu als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="53287-152">This portion of our experiment should now look something like this:</span></span>  

![Training Hallo tweede model][2]  

<span data-ttu-id="53287-154">Nu configureren Hallo [gegevens normaliseren] [ normalize-data] module:</span><span class="sxs-lookup"><span data-stu-id="53287-154">Now configure hello [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="53287-155">Klik op tooselect hello [gegevens normaliseren] [ normalize-data] module.</span><span class="sxs-lookup"><span data-stu-id="53287-155">Click tooselect hello [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="53287-156">In Hallo **eigenschappen** deelvenster **Tanh** voor Hallo **transformatiemethode** parameter.</span><span class="sxs-lookup"><span data-stu-id="53287-156">In hello **Properties** pane, select **Tanh** for hello **Transformation method** parameter.</span></span>

2. <span data-ttu-id="53287-157">Klik op **Launch column selector**, "Geen kolommen" Selecteer voor **begint met**, selecteer **opnemen** Selecteer in de eerste vervolgkeuzelijst Hallo **kolomtype**in Hallo tweede vervolgkeuzelijst en selecteer **numerieke** Hallo derde vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="53287-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in hello first dropdown, select **column type** in hello second dropdown, and select **Numeric** in hello third dropdown.</span></span> <span data-ttu-id="53287-158">Hiermee wordt aangegeven dat alle Hallo numerieke kolommen (en alleen numerieke) worden getransformeerd.</span><span class="sxs-lookup"><span data-stu-id="53287-158">This specifies that all hello numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="53287-159">Klik op Hallo toohello rechts van deze rij plusteken (+): Hiermee maakt u een rij van vervolgkeuzelijsten.</span><span class="sxs-lookup"><span data-stu-id="53287-159">Click hello plus sign (+) toohello right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="53287-160">Selecteer **uitsluiten** Selecteer in de eerste vervolgkeuzelijst Hallo **kolomnamen** in Hallo tweede vervolgkeuzelijst en voer 'Kredietrisico' in hello tekstveld.</span><span class="sxs-lookup"><span data-stu-id="53287-160">Select **Exclude** in hello first dropdown, select **column names** in hello second dropdown, and enter "Credit risk" in hello text field.</span></span> <span data-ttu-id="53287-161">Hiermee wordt aangegeven dat Hallo kredietrisico kolom moet worden genegeerd (moeten we dit omdat deze kolom numerieke en in dat geval zou worden omgezet als we deze niet uitsluit toodo).</span><span class="sxs-lookup"><span data-stu-id="53287-161">This specifies that hello Credit Risk column should be ignored (we need toodo this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="53287-162">Klik op Hallo **OK** selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="53287-162">Click hello **OK** check mark.</span></span>  

    ![Selecteer kolommen voor Hallo normaliseren Data-module][5]

<span data-ttu-id="53287-164">Hallo [gegevens normaliseren] [ normalize-data] -module is nu ingesteld tooperform een transformatie Tanh voor alle numerieke kolommen, met uitzondering van Hallo kredietrisico kolom.</span><span class="sxs-lookup"><span data-stu-id="53287-164">hello [Normalize Data][normalize-data] module is now set tooperform a Tanh transformation on all numeric columns except for hello Credit Risk column.</span></span>  

## <a name="score-and-evaluate-hello-models"></a><span data-ttu-id="53287-165">Beoordelen en evalueren Hallo modellen</span><span class="sxs-lookup"><span data-stu-id="53287-165">Score and evaluate hello models</span></span>

<span data-ttu-id="53287-166">We gebruiken Hallo gegevens die uit is gescheiden door Hallo testen [Split Data] [ split] module tooscore onze getraind modellen.</span><span class="sxs-lookup"><span data-stu-id="53287-166">We use hello testing data that was separated out by hello [Split Data][split] module tooscore our trained models.</span></span> <span data-ttu-id="53287-167">Vervolgens kunnen we vergelijken Hallo resultaten van het twee modellen toosee hello, die betere resultaten gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="53287-167">We can then compare hello results of hello two models toosee which generated better results.</span></span>  

### <a name="add-hello-score-model-modules"></a><span data-ttu-id="53287-168">Hallo Score Model modules toevoegen</span><span class="sxs-lookup"><span data-stu-id="53287-168">Add hello Score Model modules</span></span>

1. <span data-ttu-id="53287-169">Hallo zoeken [Score Model] [ score-model] module en sleep deze naar Hallo canvas.</span><span class="sxs-lookup"><span data-stu-id="53287-169">Find hello [Score Model][score-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="53287-170">Verbinding maken met de Hallo [Train Model] [ train-model] module die is verbonden toohello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] module toohello links-invoer poort Hallo [Score Model] [ score-model] module.</span><span class="sxs-lookup"><span data-stu-id="53287-170">Connect hello [Train Model][train-model] module that's connected toohello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="53287-171">Verbinding maken met de Hallo rechts [R-Script uitvoeren] [ execute-r-script] module (onze testgegevens) toohello rechts invoer poort Hallo [Score Model] [ score-model] module.</span><span class="sxs-lookup"><span data-stu-id="53287-171">Connect hello right [Execute R Script][execute-r-script] module (our testing data) toohello right input port of hello [Score Model][score-model] module.</span></span>

    ![Module score-Model verbonden][6]
   
   <span data-ttu-id="53287-173">Hallo [Score Model] [ score-model] module kunt nu Hallo tegoed informatie uit Hallo gegevens, voert u via het Hallo-model te testen en vergelijken Hallo voorspellingen Hallo model Hello werkelijke genereert kredietrisico kolom in Hallo gegevens testen.</span><span class="sxs-lookup"><span data-stu-id="53287-173">hello [Score Model][score-model] module can now take hello credit information from hello testing data, run it through hello model, and compare hello predictions hello model generates with hello actual credit risk column in hello testing data.</span></span>

4. <span data-ttu-id="53287-174">Kopieer en plak Hallo [Score Model] [ score-model] module toocreate een tweede kopie.</span><span class="sxs-lookup"><span data-stu-id="53287-174">Copy and paste hello [Score Model][score-model] module toocreate a second copy.</span></span>

5. <span data-ttu-id="53287-175">Verbinding maken met uitvoer Hallo van Hallo SVM model (dat wil zeggen, Hallo uitvoerpoort Hallo [Train Model] [ train-model] module die is verbonden toohello [Two-Class ondersteuning Vectormachine] [ two-class-support-vector-machine] module) toohello poort Hallo tweede invoer [Score Model] [ score-model] module.</span><span class="sxs-lookup"><span data-stu-id="53287-175">Connect hello output of hello SVM model (that is, hello output port of hello [Train Model][train-model] module that's connected toohello [Two-Class Support Vector Machine][two-class-support-vector-machine] module) toohello input port of hello second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="53287-176">We hebben toodo Hallo dezelfde transformatie toohello testgegevens zoals we hebben gedaan toohello trainingsgegevens voor Hallo SVM model.</span><span class="sxs-lookup"><span data-stu-id="53287-176">For hello SVM model, we have toodo hello same transformation toohello test data as we did toohello training data.</span></span> <span data-ttu-id="53287-177">Dus kopieer en plak Hallo [gegevens normaliseren] [ normalize-data] module toocreate een tweede exemplaar en verbind deze toohello rechts [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="53287-177">So copy and paste hello [Normalize Data][normalize-data] module toocreate a second copy and connect it toohello right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="53287-178">Hallo links uitvoer Hallo tweede verbinding [gegevens normaliseren] [ normalize-data] module toohello rechts poort Hallo tweede invoer [Score Model] [ score-model] module.</span><span class="sxs-lookup"><span data-stu-id="53287-178">Connect hello left output of hello second [Normalize Data][normalize-data] module toohello right input port of hello second [Score Model][score-model] module.</span></span>

    ![Beide Score Model modules verbonden][7]

### <a name="add-hello-evaluate-model-module"></a><span data-ttu-id="53287-180">De module Evaluate Model Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="53287-180">Add hello Evaluate Model module</span></span>

<span data-ttu-id="53287-181">tooevaluate Hallo twee resultaten van score berekenen en deze te vergelijken, gebruiken we een [Evaluate Model] [ evaluate-model] module.</span><span class="sxs-lookup"><span data-stu-id="53287-181">tooevaluate hello two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="53287-182">Hallo zoeken [Evaluate Model] [ evaluate-model] module en sleep deze naar Hallo canvas.</span><span class="sxs-lookup"><span data-stu-id="53287-182">Find hello [Evaluate Model][evaluate-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="53287-183">Verbinding maken met de uitvoerpoort Hallo Hallo [Score Model] [ score-model] module die is gekoppeld aan Hallo boosted decision tree model toohello links invoer poort Hallo [Evaluate Model] [ evaluate-model] module.</span><span class="sxs-lookup"><span data-stu-id="53287-183">Connect hello output port of hello [Score Model][score-model] module associated with hello boosted decision tree model toohello left input port of hello [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="53287-184">Verbinding maken met andere Hallo [Score Model] [ score-model] module toohello rechts invoer poort.</span><span class="sxs-lookup"><span data-stu-id="53287-184">Connect hello other [Score Model][score-model] module toohello right input port.</span></span>  

    ![Model evalueren module verbonden][8]

### <a name="run-hello-experiment-and-check-hello-results"></a><span data-ttu-id="53287-186">Hallo-experiment uitvoeren en Hallo resultaten controleren</span><span class="sxs-lookup"><span data-stu-id="53287-186">Run hello experiment and check hello results</span></span>

<span data-ttu-id="53287-187">toorun experiment hello, klikt u op Hallo **uitvoeren** knop onder Hallo canvas.</span><span class="sxs-lookup"><span data-stu-id="53287-187">toorun hello experiment, click hello **RUN** button below hello canvas.</span></span> <span data-ttu-id="53287-188">Het kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="53287-188">It may take a few minutes.</span></span> <span data-ttu-id="53287-189">Een draaiende indicator voor elke module ziet u dat deze wordt uitgevoerd en wordt een groen vinkje weergegeven wanneer de module Hallo is voltooid.</span><span class="sxs-lookup"><span data-stu-id="53287-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when hello module is finished.</span></span> <span data-ttu-id="53287-190">Wanneer alle Hallo-modules ingeschakeld zijn, is Hallo experiment voltooid.</span><span class="sxs-lookup"><span data-stu-id="53287-190">When all hello modules have a check mark, hello experiment has finished running.</span></span>

<span data-ttu-id="53287-191">Hallo-experiment moet nu als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="53287-191">hello experiment should now look something like this:</span></span>  

![Beide modellen evalueren][3]

<span data-ttu-id="53287-193">toocheck hello resultaten, klik op de uitvoerpoort Hallo Hallo [Evaluate Model] [ evaluate-model] module en selecteer **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="53287-193">toocheck hello results, click hello output port of hello [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="53287-194">Hallo [Evaluate Model] [ evaluate-model] module produceert een paar curven en metrische gegevens die u toelaten om toocompare Hallo resultaten van de twee scored modellen Hallo.</span><span class="sxs-lookup"><span data-stu-id="53287-194">hello [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you toocompare hello results of hello two scored models.</span></span> <span data-ttu-id="53287-195">U kunt Hallo resultaten als ontvanger Operator kenmerk (ROC) curven, curven precisie/intrekken of Lift curven weergeven.</span><span class="sxs-lookup"><span data-stu-id="53287-195">You can view hello results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="53287-196">Aanvullende gegevens die worden weergegeven, bevat een matrix verwarring cumulatieve waarden voor Hallo gebied onder Hallo kromme (AUC) en andere metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="53287-196">Additional data displayed includes a confusion matrix, cumulative values for hello area under hello curve (AUC), and other metrics.</span></span> <span data-ttu-id="53287-197">U kunt Hallo drempelwaarde wijzigen door bewegende Hallo schuifregelaar naar links of rechts en Zie hoe het is van invloed op Hallo set van metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="53287-197">You can change hello threshold value by moving hello slider left or right and see how it affects hello set of metrics.</span></span>  

<span data-ttu-id="53287-198">toohello rechts van de grafiek hello, klikt u op **berekend gegevensset** of **berekend gegevensset toocompare** toohighlight Hallo gekoppeld curve en toodisplay Hallo onderstaande metrische gegevens die is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="53287-198">toohello right of hello graph, click **Scored dataset** or **Scored dataset toocompare** toohighlight hello associated curve and toodisplay hello associated metrics below.</span></span> <span data-ttu-id="53287-199">In legenda Hallo voor Hallo curven toohello links invoerpoort Hallo 'Berekend gegevensset' overeen [Evaluate Model] [ evaluate-model] module - in ons geval dit Hallo boosted decision tree model is.</span><span class="sxs-lookup"><span data-stu-id="53287-199">In hello legend for hello curves, "Scored dataset" corresponds toohello left input port of hello [Evaluate Model][evaluate-model] module - in our case, this is hello boosted decision tree model.</span></span> <span data-ttu-id="53287-200">'Berekend gegevensset toocompare' komt overeen toohello rechteruitvoerpoort - Hallo SVM model in ons geval.</span><span class="sxs-lookup"><span data-stu-id="53287-200">"Scored dataset toocompare" corresponds toohello right input port - hello SVM model in our case.</span></span> <span data-ttu-id="53287-201">Als u op een van deze labels, Hallo curve voor dit model is gemarkeerd en Hallo bijbehorende metrische gegevens worden weergegeven, zoals wordt weergegeven in de volgende afbeelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="53287-201">When you click one of these labels, hello curve for that model is highlighted and hello corresponding metrics are displayed, as shown in hello following graphic.</span></span>  

![ROC curven voor modellen][4]

<span data-ttu-id="53287-203">Door deze waarden in, kunt u beslissen welk model dichtstbijzijnde toogiving Hallo van resultaten die u zoekt.</span><span class="sxs-lookup"><span data-stu-id="53287-203">By examining these values, you can decide which model is closest toogiving you hello results you're looking for.</span></span> <span data-ttu-id="53287-204">U kunt teruggaan en door het wijzigen van parameterwaarden Hallo verschillende modellen in uw experiment herhalen.</span><span class="sxs-lookup"><span data-stu-id="53287-204">You can go back and iterate on your experiment by changing parameter values in hello different models.</span></span> 

<span data-ttu-id="53287-205">Hallo wetenschappelijke en illustraties van deze resultaten te interpreteren en Hallo model prestaties afstemmen is buiten Hallo-bereik van deze rondleiding.</span><span class="sxs-lookup"><span data-stu-id="53287-205">hello science and art of interpreting these results and tuning hello model performance is outside hello scope of this walkthrough.</span></span> <span data-ttu-id="53287-206">Voor meer informatie kan u Hallo artikelen volgende lezen:</span><span class="sxs-lookup"><span data-stu-id="53287-206">For additional help, you might read hello following articles:</span></span>
- [<span data-ttu-id="53287-207">Hoe tooevaluate prestaties in Azure Machine Learning model</span><span class="sxs-lookup"><span data-stu-id="53287-207">How tooevaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="53287-208">Het kiezen van de parameters toooptimize uw algoritmen in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="53287-208">Choose parameters toooptimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="53287-209">Model resulteert in een Azure Machine Learning interpreteren</span><span class="sxs-lookup"><span data-stu-id="53287-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="53287-210">Telkens wanneer u een record van deze herhaling Hallo experiment uitvoeren wordt opgeslagen in Hallo geschiedenis uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="53287-210">Each time you run hello experiment a record of that iteration is kept in hello Run History.</span></span> <span data-ttu-id="53287-211">U kunt deze herhalingen zien en retourneren tooany, door te klikken op **weergave uitvoeren geschiedenis** hieronder Hallo canvas.</span><span class="sxs-lookup"><span data-stu-id="53287-211">You can view these iterations, and return tooany of them, by clicking **VIEW RUN HISTORY** below hello canvas.</span></span> <span data-ttu-id="53287-212">U kunt ook klikken op **voorafgaande uitvoeren** in Hallo **eigenschappen** deelvenster tooreturn toohello herhaling voorafgaat Hallo een dat u hebt geopend.</span><span class="sxs-lookup"><span data-stu-id="53287-212">You can also click **Prior Run** in hello **Properties** pane tooreturn toohello iteration immediately preceding hello one you have open.</span></span>
> 
> <span data-ttu-id="53287-213">U kunt een kopie van elke herhaling van uw experiment maken door te klikken op **SAVE AS** hieronder Hallo canvas.</span><span class="sxs-lookup"><span data-stu-id="53287-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below hello canvas.</span></span> 
> <span data-ttu-id="53287-214">Gebruik van het experiment Hallo **samenvatting** en **beschrijving** eigenschappen tookeep een record van wat u hebt geprobeerd in uw experimentherhalingen.</span><span class="sxs-lookup"><span data-stu-id="53287-214">Use hello experiment's **Summary** and **Description** properties tookeep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="53287-215">Zie voor meer informatie [experimentherhalingen in Azure Machine Learning Studio beheren](machine-learning-manage-experiment-iterations.md).</span><span class="sxs-lookup"><span data-stu-id="53287-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="53287-216">**Volgende stap: [Hallo-webservice implementeren](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="53287-216">**Next: [Deploy hello web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
