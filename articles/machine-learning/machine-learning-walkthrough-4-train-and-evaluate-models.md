---
title: 'Stap 4: Trainen en evalueren van de voorspellende analytische modellen | Microsoft Docs'
description: 'Stap 4 van de prognose een overzicht van de voorspellende oplossing: trein, beoordelen en evalueren van meerdere modellen in Azure Machine Learning Studio.'
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
ms.openlocfilehash: 58d46dd1464ec0a3fc9639f78d4429e0e778c2bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-the-predictive-analytic-models"></a><span data-ttu-id="3ee3e-103">Kennismaken, stap 4: De voorspellende analysemodellen trainen en evalueren</span><span class="sxs-lookup"><span data-stu-id="3ee3e-103">Walkthrough Step 4: Train and evaluate the predictive analytic models</span></span>
<span data-ttu-id="3ee3e-104">Dit onderwerp bevat de vierde stap van de procedure [predictive analytics-oplossing in Azure Machine Learning ontwikkelen](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="3ee3e-104">This topic contains the fourth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="3ee3e-105">Een Machine Learning-werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="3ee3e-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="3ee3e-106">Bestaande gegevens uploaden</span><span class="sxs-lookup"><span data-stu-id="3ee3e-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="3ee3e-107">Een nieuw experiment maken</span><span class="sxs-lookup"><span data-stu-id="3ee3e-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="3ee3e-108">**De modellen trainen en evalueren**</span><span class="sxs-lookup"><span data-stu-id="3ee3e-108">**Train and evaluate the models**</span></span>
5. [<span data-ttu-id="3ee3e-109">De webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="3ee3e-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="3ee3e-110">Toegang tot de webservice</span><span class="sxs-lookup"><span data-stu-id="3ee3e-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="3ee3e-111">Een van de voordelen van het gebruik van Azure Machine Learning Studio voor het maken van machine learning-modellen is de mogelijkheid om meer dan één type model tegelijk in een enkel experiment te vergelijken van de resultaten.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-111">One of the benefits of using Azure Machine Learning Studio for creating machine learning models is the ability to try more than one type of model at a time in a single experiment and compare the results.</span></span> <span data-ttu-id="3ee3e-112">Dit type experimenteren kunt u de beste oplossing voor uw probleem vinden.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-112">This type of experimentation helps you find the best solution for your problem.</span></span>

<span data-ttu-id="3ee3e-113">In het experiment dat we in dit overzicht ontwikkelt, we twee verschillende soorten modellen maken en vervolgens de resultaten van score berekenen om te beslissen welk algoritme we wilt gebruiken in onze laatste experiment te vergelijken.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-113">In the experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results to decide which algorithm we want to use in our final experiment.</span></span>  

<span data-ttu-id="3ee3e-114">Er zijn verschillende modellen die we kan kiezen uit.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-114">There are various models we could choose from.</span></span> <span data-ttu-id="3ee3e-115">Overzicht van de beschikbare modellen, vouw de **Machine Learning** knooppunt in het modulepalet en vouw vervolgens **Model initialiseren** en de knooppunten eronder.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-115">To see the models available, expand the **Machine Learning** node in the module palette, and then expand **Initialize Model** and the nodes beneath it.</span></span> <span data-ttu-id="3ee3e-116">Voor de doeleinden van dit experiment selecteren we de [Two-Class ondersteuning Vectormachine] [ two-class-support-vector-machine] (SVM) en de [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] modules.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-116">For the purposes of this experiment, we'll select the [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="3ee3e-117">Als u informatie om te bepalen welke Machine Learning-algoritme beste tegemoetkomt aan het specifieke probleem dat u probeert op te lossen, raadpleegt u [algoritmen kiezen voor Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span><span class="sxs-lookup"><span data-stu-id="3ee3e-117">To get help deciding which Machine Learning algorithm best suits the particular problem you're trying to solve, see [How to choose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-the-models"></a><span data-ttu-id="3ee3e-118">De modellen trainen</span><span class="sxs-lookup"><span data-stu-id="3ee3e-118">Train the models</span></span>

<span data-ttu-id="3ee3e-119">We voegen toe zowel de [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] module en [Two-Class ondersteuning Vectormachine] [ two-class-support-vector-machine] dit experiment de module.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-119">We'll add both the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="3ee3e-120">Two-Class gestimuleerd beslissingsstructuur</span><span class="sxs-lookup"><span data-stu-id="3ee3e-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="3ee3e-121">Eerst laten we instellen van het model van de boomstructuur gestimuleerd besluit.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-121">First, let's set up the boosted decision tree model.</span></span>

1. <span data-ttu-id="3ee3e-122">Zoek de [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] module in het modulepalet en sleep deze naar het canvas.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-122">Find the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in the module palette and drag it onto the canvas.</span></span>

2. <span data-ttu-id="3ee3e-123">Zoek de [Train Model] [ train-model] module, sleep deze naar het canvas en sluit vervolgens de uitvoer van de [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] module aan de linkerkant invoer-poort van de [Train Model] [ train-model] module.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-123">Find the [Train Model][train-model] module, drag it onto the canvas, and then connect the output of the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="3ee3e-124">De [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] module initialiseert de algemene model en [Model trainen] [ train-model] trainingsgegevens gebruikt voor het trainen van het model.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-124">The [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes the generic model, and [Train Model][train-model] uses training data to train the model.</span></span> 

3. <span data-ttu-id="3ee3e-125">Verbinding maken met de linker-uitvoer van de linkerkant [R-Script uitvoeren] [ execute-r-script] module aan de rechterkant invoer-poort van de [Train Model] [ train-model] module (we besloten [stap 3](machine-learning-walkthrough-3-create-new-experiment.md) van deze rondleiding gebruiken de gegevens die afkomstig zijn vanaf de linkerkant van de module gesplitste gegevens voor training).</span><span class="sxs-lookup"><span data-stu-id="3ee3e-125">Connect the left output of the left [Execute R Script][execute-r-script] module to the right input port of the [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough to use the data coming from the left side of the Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="3ee3e-126">We hebben twee van de invoer en een van de uitvoer van de [R-Script uitvoeren] [ execute-r-script] -module voor dit experiment, zodat we kunt ze niet-gekoppelde laten.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-126">We don't need two of the inputs and one of the outputs of the [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="3ee3e-127">Dit gedeelte van het experiment ziet nu er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="3ee3e-127">This portion of the experiment now looks something like this:</span></span>  

![Een model trainen][1]

<span data-ttu-id="3ee3e-129">Nu moet u vertelt de [Train Model] [ train-model] module willen we het model te voorspellen van de kredietrisico-waarde.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-129">Now we need to tell the [Train Model][train-model] module that we want the model to predict the Credit Risk value.</span></span>

1. <span data-ttu-id="3ee3e-130">Selecteer de [Train Model] [ train-model] module.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-130">Select the [Train Model][train-model] module.</span></span> <span data-ttu-id="3ee3e-131">In de **eigenschappen** deelvenster, klikt u op **Launch column selector**.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-131">In the **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="3ee3e-132">In de **één kolom selecteren** dialoogvenster 'kredietrisico' typt in het zoekveld onder **beschikbare kolommen**'Kredietrisico' hieronder hebt geselecteerd en klik op de knop pijl-rechts (**>**) 'Kredietrisico' verplaatsen naar **geselecteerde kolommen**.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-132">In the **Select a single column** dialog, type "credit risk" in the search field under **Available Columns**, select "Credit risk" below, and click the right arrow button (**>**) to move "Credit risk" to **Selected Columns**.</span></span> 

    ![Selecteer de kolom kredietrisico voor de module Train Model][0]

3. <span data-ttu-id="3ee3e-134">Klik op de **OK** selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-134">Click the **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="3ee3e-135">Two-Class Support Vector Machine</span><span class="sxs-lookup"><span data-stu-id="3ee3e-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="3ee3e-136">Vervolgens wordt het model SVM hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-136">Next, we set up the SVM model.</span></span>  

<span data-ttu-id="3ee3e-137">Eerste, uitleg over SVM.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="3ee3e-138">Gestimuleerd beslissingsstructuren werken goed met functies van elk type.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="3ee3e-139">Omdat de module SVM een lineaire classificatie genereert, heeft het model die wordt gegenereerd echter het beste testfout wanneer alle functies van de numerieke dezelfde schaal hebben.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-139">However, since the SVM module generates a linear classifier, the model that it generates has the best test error when all numeric features have the same scale.</span></span> <span data-ttu-id="3ee3e-140">Als u wilt converteren alle numerieke functies op dezelfde schaal, gebruiken we een transformatie 'Tanh' (met de [gegevens normaliseren] [ normalize-data] module).</span><span class="sxs-lookup"><span data-stu-id="3ee3e-140">To convert all numeric features to the same scale, we use a "Tanh" transformation (with the [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="3ee3e-141">Hiermee transformeert onze cijfers in het bereik [0,1].</span><span class="sxs-lookup"><span data-stu-id="3ee3e-141">This transforms our numbers into the [0,1] range.</span></span> <span data-ttu-id="3ee3e-142">De module SVM converteert tekenreeks functies met categorische functies en vervolgens met binaire 0/1-functies, zodat we niet hoeven te transformeren handmatig tekenreeks functies.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-142">The SVM module converts string features to categorical features and then to binary 0/1 features, so we don't need to manually transform string features.</span></span> <span data-ttu-id="3ee3e-143">Bovendien we willen niet voor het transformeren van de kredietrisico kolom (kolom 21) - het numerieke is, maar is de waarde die we van het model te voorspellen, trainen bent dus moeten we er alleen laat.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-143">Also, we don't want to transform the Credit Risk column (column 21) - it's numeric, but it's the value we're training the model to predict, so we need to leave it alone.</span></span>  

<span data-ttu-id="3ee3e-144">Als u het model SVM instelt, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="3ee3e-144">To set up the SVM model, do the following:</span></span>

1. <span data-ttu-id="3ee3e-145">Zoek de [Two-Class ondersteuning Vectormachine] [ two-class-support-vector-machine] module in het modulepalet en sleep deze naar het canvas.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-145">Find the [Two-Class Support Vector Machine][two-class-support-vector-machine] module in the module palette and drag it onto the canvas.</span></span>

2. <span data-ttu-id="3ee3e-146">Met de rechtermuisknop op de [Train Model] [ train-model] -module, selecteer **kopie**, en klik vervolgens met de rechtermuisknop op het canvas en selecteer **plakken**.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-146">Right-click the [Train Model][train-model] module, select **Copy**, and then right-click the canvas and select **Paste**.</span></span> <span data-ttu-id="3ee3e-147">De kopie van de [Train Model] [ train-model] module heeft de dezelfde kolom selecteren als het origineel.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-147">The copy of the [Train Model][train-model] module has the same column selection as the original.</span></span>

3. <span data-ttu-id="3ee3e-148">Verbinding maken met de uitvoer van de [Two-Class ondersteuning Vectormachine] [ two-class-support-vector-machine] module links-poort van de tweede invoer [Train Model] [ train-model] module.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-148">Connect the output of the [Two-Class Support Vector Machine][two-class-support-vector-machine] module to the left input port of the second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="3ee3e-149">Zoek de [gegevens normaliseren] [ normalize-data] module en sleep deze naar het canvas.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-149">Find the [Normalize Data][normalize-data] module and drag it onto the canvas.</span></span>

5. <span data-ttu-id="3ee3e-150">Verbinding maken met de linker-uitvoer van de linkerkant [R-Script uitvoeren] [ execute-r-script] module die u wilt de invoer van deze module (Let op dat de uitvoerpoort van een module kan worden verbonden met meer dan een andere module).</span><span class="sxs-lookup"><span data-stu-id="3ee3e-150">Connect the left output of the left [Execute R Script][execute-r-script] module to the input of this module (notice that the output port of a module may be connected to more than one other module).</span></span>

6. <span data-ttu-id="3ee3e-151">Verbinding maken met de uitvoerpoort links van de [gegevens normaliseren] [ normalize-data] module aan de rechterkant poort van de tweede invoer [Train Model] [ train-model] module.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-151">Connect the left output port of the [Normalize Data][normalize-data] module to the right input port of the second [Train Model][train-model] module.</span></span>

<span data-ttu-id="3ee3e-152">Dit gedeelte van onze experiment moet nu als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="3ee3e-152">This portion of our experiment should now look something like this:</span></span>  

![Het tweede model te trainen][2]  

<span data-ttu-id="3ee3e-154">Nu configureren de [gegevens normaliseren] [ normalize-data] module:</span><span class="sxs-lookup"><span data-stu-id="3ee3e-154">Now configure the [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="3ee3e-155">Selecteer de [gegevens normaliseren] [ normalize-data] module.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-155">Click to select the [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="3ee3e-156">In de **eigenschappen** deelvenster **Tanh** voor de **transformatiemethode** parameter.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-156">In the **Properties** pane, select **Tanh** for the **Transformation method** parameter.</span></span>

2. <span data-ttu-id="3ee3e-157">Klik op **Launch column selector**, "Geen kolommen" Selecteer voor **begint met**, selecteer **opnemen** selecteren in de eerste vervolgkeuzelijst **kolomtype** in het tweede vervolgkeuzelijst en selecteer **numerieke** in de vervolgkeuzelijst voor derde.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in the first dropdown, select **column type** in the second dropdown, and select **Numeric** in the third dropdown.</span></span> <span data-ttu-id="3ee3e-158">Hiermee wordt aangegeven dat alle numerieke kolommen (en alleen numerieke) worden getransformeerd.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-158">This specifies that all the numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="3ee3e-159">Klik op het plusteken (+) rechts van deze rij - Hiermee maakt u een rij van vervolgkeuzelijsten.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-159">Click the plus sign (+) to the right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="3ee3e-160">Selecteer **uitsluiten** selecteren in de eerste vervolgkeuzelijst **kolomnamen** in de tweede vervolgkeuzelijst en voer 'Kredietrisico' in het tekstveld.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-160">Select **Exclude** in the first dropdown, select **column names** in the second dropdown, and enter "Credit risk" in the text field.</span></span> <span data-ttu-id="3ee3e-161">Hiermee wordt aangegeven dat de kolom kredietrisico moet worden genegeerd (we nodig om dit te doen omdat deze kolom numerieke en daarom zou worden omgezet als we deze niet uitsluiten).</span><span class="sxs-lookup"><span data-stu-id="3ee3e-161">This specifies that the Credit Risk column should be ignored (we need to do this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="3ee3e-162">Klik op de **OK** selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-162">Click the **OK** check mark.</span></span>  

    ![Kolommen voor de module normaliseren gegevens selecteren][5]

<span data-ttu-id="3ee3e-164">De [gegevens normaliseren] [ normalize-data] module nu is ingesteld voor het uitvoeren van een transformatie Tanh op alle numerieke kolommen, met uitzondering van de kolom kredietrisico.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-164">The [Normalize Data][normalize-data] module is now set to perform a Tanh transformation on all numeric columns except for the Credit Risk column.</span></span>  

## <a name="score-and-evaluate-the-models"></a><span data-ttu-id="3ee3e-165">Beoordelen en evalueren van de modellen</span><span class="sxs-lookup"><span data-stu-id="3ee3e-165">Score and evaluate the models</span></span>

<span data-ttu-id="3ee3e-166">We gebruiken de testgegevens die is gescheiden uit door de [Split Data] [ split] module voor de beoordeling van onze getraind modellen.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-166">We use the testing data that was separated out by the [Split Data][split] module to score our trained models.</span></span> <span data-ttu-id="3ee3e-167">We kunnen de resultaten van de twee modellen om te zien die betere resultaten gegenereerd vervolgens vergelijken.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-167">We can then compare the results of the two models to see which generated better results.</span></span>  

### <a name="add-the-score-model-modules"></a><span data-ttu-id="3ee3e-168">De modules Score Model toevoegen</span><span class="sxs-lookup"><span data-stu-id="3ee3e-168">Add the Score Model modules</span></span>

1. <span data-ttu-id="3ee3e-169">Zoek de [Score Model] [ score-model] module en sleep deze naar het canvas.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-169">Find the [Score Model][score-model] module and drag it onto the canvas.</span></span>

2. <span data-ttu-id="3ee3e-170">Verbinding maken met de [Train Model] [ train-model] module die verbonden met de [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] module aan de linkerkant invoer-poort van de [Score Model] [ score-model] module.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-170">Connect the [Train Model][train-model] module that's connected to the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="3ee3e-171">Verbinding maken met het recht [R-Script uitvoeren] [ execute-r-script] module (onze testgegevens) naar rechts invoer-poort van de [Score Model] [ score-model] module.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-171">Connect the right [Execute R Script][execute-r-script] module (our testing data) to the right input port of the [Score Model][score-model] module.</span></span>

    ![Module score-Model verbonden][6]
   
   <span data-ttu-id="3ee3e-173">De [Score Model] [ score-model] module kunt nu de tegoed gegevens uit de testgegevens, voeren via het model en de voorspellingen het model wordt gegenereerd met de werkelijke tegoed risico kolom in de testgegevens vergelijken.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-173">The [Score Model][score-model] module can now take the credit information from the testing data, run it through the model, and compare the predictions the model generates with the actual credit risk column in the testing data.</span></span>

4. <span data-ttu-id="3ee3e-174">Kopieer en plak de [Score Model] [ score-model] module om een tweede kopie te maken.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-174">Copy and paste the [Score Model][score-model] module to create a second copy.</span></span>

5. <span data-ttu-id="3ee3e-175">Verbinding maken met de uitvoer van het model SVM (dat wil zeggen, de uitvoerpoort van de [Train Model] [ train-model] module die verbonden met de [Two-Class ondersteuning Vectormachine] [ two-class-support-vector-machine] module) met de invoer-poort van de tweede [Score Model] [ score-model] module.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-175">Connect the output of the SVM model (that is, the output port of the [Train Model][train-model] module that's connected to the [Two-Class Support Vector Machine][two-class-support-vector-machine] module) to the input port of the second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="3ee3e-176">Voor het model SVM hebben we de dezelfde transformatie naar de testgegevens zoals we hebben gedaan aan de trainingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-176">For the SVM model, we have to do the same transformation to the test data as we did to the training data.</span></span> <span data-ttu-id="3ee3e-177">Dus kopieer en plak de [gegevens normaliseren] [ normalize-data] module die u wilt een tweede exemplaar maken en te verbinden met het recht [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-177">So copy and paste the [Normalize Data][normalize-data] module to create a second copy and connect it to the right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="3ee3e-178">Verbinding maken met de linker-uitvoer van de tweede [gegevens normaliseren] [ normalize-data] module aan de rechterkant poort van de tweede invoer [Score Model] [ score-model] module.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-178">Connect the left output of the second [Normalize Data][normalize-data] module to the right input port of the second [Score Model][score-model] module.</span></span>

    ![Beide Score Model modules verbonden][7]

### <a name="add-the-evaluate-model-module"></a><span data-ttu-id="3ee3e-180">De module Evaluate Model toevoegen</span><span class="sxs-lookup"><span data-stu-id="3ee3e-180">Add the Evaluate Model module</span></span>

<span data-ttu-id="3ee3e-181">Als u wilt evalueren van de resultaten van de twee score berekenen en deze te vergelijken, gebruiken we een [Evaluate Model] [ evaluate-model] module.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-181">To evaluate the two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="3ee3e-182">Zoek de [Evaluate Model] [ evaluate-model] module en sleep deze naar het canvas.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-182">Find the [Evaluate Model][evaluate-model] module and drag it onto the canvas.</span></span>

2. <span data-ttu-id="3ee3e-183">Verbinding maken met de uitvoerpoort van de [Score Model] [ score-model] module die is gekoppeld aan het model gestimuleerd decision tree aan de linkerinvoerpoort van de [Evaluate Model] [ evaluate-model] module.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-183">Connect the output port of the [Score Model][score-model] module associated with the boosted decision tree model to the left input port of the [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="3ee3e-184">Verbinding maken met de andere [Score Model] [ score-model] module aan de rechterkant invoer poort.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-184">Connect the other [Score Model][score-model] module to the right input port.</span></span>  

    ![Model evalueren module verbonden][8]

### <a name="run-the-experiment-and-check-the-results"></a><span data-ttu-id="3ee3e-186">Voer het experiment en de resultaten controleren</span><span class="sxs-lookup"><span data-stu-id="3ee3e-186">Run the experiment and check the results</span></span>

<span data-ttu-id="3ee3e-187">Als u wilt het experiment uitvoeren, klikt u op de **uitvoeren** knop onder het canvas.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-187">To run the experiment, click the **RUN** button below the canvas.</span></span> <span data-ttu-id="3ee3e-188">Het kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-188">It may take a few minutes.</span></span> <span data-ttu-id="3ee3e-189">Een draaiende indicator voor elke module ziet u dat deze wordt uitgevoerd en wordt een groen vinkje weergegeven wanneer de module is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when the module is finished.</span></span> <span data-ttu-id="3ee3e-190">Wanneer alle modules ingeschakeld hebt, is het experiment voltooid.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-190">When all the modules have a check mark, the experiment has finished running.</span></span>

<span data-ttu-id="3ee3e-191">Het experiment moet nu als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="3ee3e-191">The experiment should now look something like this:</span></span>  

![Beide modellen evalueren][3]

<span data-ttu-id="3ee3e-193">Als u wilt de resultaten controleren, klikt u op de uitvoerpoort van de [Evaluate Model] [ evaluate-model] module en selecteer **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-193">To check the results, click the output port of the [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="3ee3e-194">De [Evaluate Model] [ evaluate-model] module produceert een paar curven en metrische gegevens waarmee u kunt de resultaten van de twee modellen scored vergelijken.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-194">The [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you to compare the results of the two scored models.</span></span> <span data-ttu-id="3ee3e-195">U kunt de resultaten als ontvanger Operator kenmerk (ROC) curven, curven precisie/intrekken of Lift curven weergeven.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-195">You can view the results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="3ee3e-196">Aanvullende gegevens die worden weergegeven, bevat een matrix verwarring, cumulatieve waarden voor het gebied onder de curve (AUC) en andere metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-196">Additional data displayed includes a confusion matrix, cumulative values for the area under the curve (AUC), and other metrics.</span></span> <span data-ttu-id="3ee3e-197">U kunt de drempelwaarde wijzigen met de schuifregelaar naar links of rechts en Zie hoe dit invloed heeft op de metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-197">You can change the threshold value by moving the slider left or right and see how it affects the set of metrics.</span></span>  

<span data-ttu-id="3ee3e-198">Aan de rechterkant van de grafiek, klikt u op **berekend gegevensset** of **berekend gegevensset vergelijken** gekoppeld curve markeren en de bijbehorende metrische gegevens die hieronder worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-198">To the right of the graph, click **Scored dataset** or **Scored dataset to compare** to highlight the associated curve and to display the associated metrics below.</span></span> <span data-ttu-id="3ee3e-199">In de legenda voor de curven 'Berekend gegevensset' komt overeen met de linkerinvoerpoort van de [Evaluate Model] [ evaluate-model] module - in ons geval is dit het gestimuleerd decision tree-model.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-199">In the legend for the curves, "Scored dataset" corresponds to the left input port of the [Evaluate Model][evaluate-model] module - in our case, this is the boosted decision tree model.</span></span> <span data-ttu-id="3ee3e-200">'Berekend gegevensset vergelijken' komt overeen met de rechteruitvoerpoort - het model SVM in ons geval.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-200">"Scored dataset to compare" corresponds to the right input port - the SVM model in our case.</span></span> <span data-ttu-id="3ee3e-201">Als u op een van deze labels, curve voor dit model is gemarkeerd en de bijbehorende metrische gegevens worden weergegeven, zoals wordt weergegeven in de volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-201">When you click one of these labels, the curve for that model is highlighted and the corresponding metrics are displayed, as shown in the following graphic.</span></span>  

![ROC curven voor modellen][4]

<span data-ttu-id="3ee3e-203">Door deze waarden in, kunt u bepalen welk model zich het dichtst bij zodat u de resultaten die u zoekt.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-203">By examining these values, you can decide which model is closest to giving you the results you're looking for.</span></span> <span data-ttu-id="3ee3e-204">U kunt teruggaan en uw experiment herhalen door de parameterwaarden in de verschillende modellen te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-204">You can go back and iterate on your experiment by changing parameter values in the different models.</span></span> 

<span data-ttu-id="3ee3e-205">De wetenschap en illustraties van deze resultaten te interpreteren en het afstemmen van de prestaties van het model is buiten het bereik van deze rondleiding.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-205">The science and art of interpreting these results and tuning the model performance is outside the scope of this walkthrough.</span></span> <span data-ttu-id="3ee3e-206">U kunt de volgende artikelen lezen voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="3ee3e-206">For additional help, you might read the following articles:</span></span>
- [<span data-ttu-id="3ee3e-207">Het evalueren van de prestaties van het model in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3ee3e-207">How to evaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="3ee3e-208">Parameters voor het optimaliseren van uw algoritmen in Azure Machine Learning kiezen</span><span class="sxs-lookup"><span data-stu-id="3ee3e-208">Choose parameters to optimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="3ee3e-209">Model resulteert in een Azure Machine Learning interpreteren</span><span class="sxs-lookup"><span data-stu-id="3ee3e-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="3ee3e-210">Telkens wanneer u het experiment een record van deze herhaling uitvoert wordt opgeslagen in de geschiedenis uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-210">Each time you run the experiment a record of that iteration is kept in the Run History.</span></span> <span data-ttu-id="3ee3e-211">U kunt deze herhalingen zien en terugkeren naar elk van deze door te klikken op **weergave uitvoeren geschiedenis** onder het canvas.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-211">You can view these iterations, and return to any of them, by clicking **VIEW RUN HISTORY** below the canvas.</span></span> <span data-ttu-id="3ee3e-212">U kunt ook klikken op **voorafgaande uitvoeren** in de **eigenschappen** deelvenster terugkeren naar de herhaling direct vóór de naam die u hebt geopend.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-212">You can also click **Prior Run** in the **Properties** pane to return to the iteration immediately preceding the one you have open.</span></span>
> 
> <span data-ttu-id="3ee3e-213">U kunt een kopie van elke herhaling van uw experiment maken door te klikken op **SAVE AS** onder het canvas.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below the canvas.</span></span> 
> <span data-ttu-id="3ee3e-214">Gebruik het experiment **samenvatting** en **beschrijving** eigenschappen voor het bijhouden van wat u hebt geprobeerd in uw experimentherhalingen.</span><span class="sxs-lookup"><span data-stu-id="3ee3e-214">Use the experiment's **Summary** and **Description** properties to keep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="3ee3e-215">Zie voor meer informatie [experimentherhalingen in Azure Machine Learning Studio beheren](machine-learning-manage-experiment-iterations.md).</span><span class="sxs-lookup"><span data-stu-id="3ee3e-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="3ee3e-216">**Volgende stap: [de webservice implementeren](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="3ee3e-216">**Next: [Deploy the web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

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
