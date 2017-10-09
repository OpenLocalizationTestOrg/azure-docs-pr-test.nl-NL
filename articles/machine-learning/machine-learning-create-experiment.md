---
title: aaaA eenvoudig experiment in Machine Learning Studio | Microsoft Docs
description: Deze zelfstudie over Machine Learning leidt u door een eenvoudig gegevenswetenschapexperiment. We moet Hallo prijs van een auto met een regression-algoritme voorspellen.
keywords: experiment,lineaire regressie,machine learning-algoritmen,zelfstudie over machine learning,voorspellende modelleringstechnieken,gegevenswetenschapexperiment
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: fb215851d380acf7d0f4934a426283369f9c4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a><span data-ttu-id="33d78-105">Zelfstudie over Machine Learning: uw eerste gegevenswetenschapexperiment maken in Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="33d78-105">Machine learning tutorial: Create your first data science experiment in Azure Machine Learning Studio</span></span>

<span data-ttu-id="33d78-106">Als u **Azure Machine Learning Studio** niet eerder hebt gebruikt, biedt deze zelfstudie een goede basis.</span><span class="sxs-lookup"><span data-stu-id="33d78-106">If you've never used **Azure Machine Learning Studio** before, this tutorial is for you.</span></span>

<span data-ttu-id="33d78-107">In deze zelfstudie behandelen we hoe toouse Studio voor Hallo dit de eerste keer toocreate een machine learning-experiment.</span><span class="sxs-lookup"><span data-stu-id="33d78-107">In this tutorial, we'll walk through how toouse Studio for hello first time toocreate a machine learning experiment.</span></span> <span data-ttu-id="33d78-108">Hallo-experiment wordt een analytische model dat Hallo prijs van een auto op basis van verschillende variabelen, zoals het merk en technische specificaties voorspelt testen.</span><span class="sxs-lookup"><span data-stu-id="33d78-108">hello experiment will test an analytical model that predicts hello price of an automobile based on different variables such as make and technical specifications.</span></span>

> [!NOTE]
> <span data-ttu-id="33d78-109">Deze zelfstudie leert u Hallo basisprincipes van hoe toodrag-en-neerzetten modules naar uw experiment ze met elkaar verbinden, Hallo experiment uitvoeren en bekijkt hello resultaten.</span><span class="sxs-lookup"><span data-stu-id="33d78-109">This tutorial shows you hello basics of how toodrag-and-drop modules onto your experiment, connect them together, run hello experiment, and look at hello results.</span></span> <span data-ttu-id="33d78-110">We zullen niet toodiscuss Hallo algemeen onderwerp van machine learning of hoe Hallo 100 + ingebouwde algoritmen en gegevens manipulatie modules opgenomen in Studio tooselect en het gebruik.</span><span class="sxs-lookup"><span data-stu-id="33d78-110">We're not going toodiscuss hello general topic of machine learning or how tooselect and use hello 100+ built-in algorithms and data manipulation modules included in Studio.</span></span>
>
><span data-ttu-id="33d78-111">Als u nieuwe toomachine learning, Hallo video series [Gegevenswetenschap voor beginnende gebruikers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) mogelijk een goede plaats toostart.</span><span class="sxs-lookup"><span data-stu-id="33d78-111">If you're new toomachine learning, hello video series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) might be a good place toostart.</span></span> <span data-ttu-id="33d78-112">Deze video-serie is een uitstekende inleiding toomachine learning met alledaagse taal en -concepten.</span><span class="sxs-lookup"><span data-stu-id="33d78-112">This video series is a great introduction toomachine learning using everyday language and concepts.</span></span>
>
><span data-ttu-id="33d78-113">Als u bekend met machine learning bent, maar u meer algemene informatie over Machine Learning Studio en Hallo machine learning-algoritmen die deze bevat zoekt, zijn er goede bronnen:</span><span class="sxs-lookup"><span data-stu-id="33d78-113">If you're familiar with machine learning, but you're looking for more general information about Machine Learning Studio, and hello machine learning algorithms it contains, here are some good resources:</span></span>
>
- [<span data-ttu-id="33d78-114">Wat is Machine Learning Studio?</span><span class="sxs-lookup"><span data-stu-id="33d78-114">What is Machine Learning Studio?</span></span>](machine-learning-what-is-ml-studio.md) <span data-ttu-id="33d78-115">- Dit geeft een overzicht van Studio.</span><span class="sxs-lookup"><span data-stu-id="33d78-115">- This is a high-level overview of Studio.</span></span>
- <span data-ttu-id="33d78-116">[Machine learning-algoritme voorbeelden voor alledaagse](machine-learning-basics-infographic-with-algorithm-examples.md) -deze infographic is handig als u meer informatie over de verschillende soorten machine learning-algoritmen opgenomen in Machine Learning Studio Hallo toolearn wilt.</span><span class="sxs-lookup"><span data-stu-id="33d78-116">[Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md) - This infographic is useful if you want toolearn more about hello different types of machine learning algorithms included with Machine Learning Studio.</span></span>
- <span data-ttu-id="33d78-117">[Machine Learning-handleiding](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) -in deze gids vindt soortgelijke informatie als Hallo infographic hierboven, maar in een interactieve indeling.</span><span class="sxs-lookup"><span data-stu-id="33d78-117">[Machine Learning Guide](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) - This guide covers similar information as hello infographic above, but in an interactive format.</span></span>
- <span data-ttu-id="33d78-118">[Machine learning-algoritme-referentieoverzicht](machine-learning-algorithm-cheat-sheet.md) en [hoe toochoose algoritmen voor Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) -deze Downloadbare poster en de bijbehorende artikel Hallo Studio algoritmen in de diepte bespreken.</span><span class="sxs-lookup"><span data-stu-id="33d78-118">[Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md) and [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) - This downloadable poster and accompanying article discuss hello Studio algorithms in depth.</span></span>
- <span data-ttu-id="33d78-119">[Machine Learning Studio: Algoritme en Module Help](https://msdn.microsoft.com/library/azure/dn905974.aspx) -dit is de volledige verwijzing Hallo voor alle Studio-modules, waaronder machine learning-algoritmen</span><span class="sxs-lookup"><span data-stu-id="33d78-119">[Machine Learning Studio: Algorithm and Module Help](https://msdn.microsoft.com/library/azure/dn905974.aspx) - This is hello complete reference for all Studio modules, including machine learning algorithms,</span></span>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a><span data-ttu-id="33d78-120">Op welke wijze is Machine Learning Studio nuttig?</span><span class="sxs-lookup"><span data-stu-id="33d78-120">How does Machine Learning Studio help?</span></span>

<span data-ttu-id="33d78-121">Machine Learning Studio maakt het eenvoudig tooset van een experiment met behulp van slepen en neerzetten modules voorgeprogrammeerde met voorspellende modelleringstechnieken.</span><span class="sxs-lookup"><span data-stu-id="33d78-121">Machine Learning Studio makes it easy tooset up an experiment using drag-and-drop modules preprogrammed with predictive modeling techniques.</span></span>

<span data-ttu-id="33d78-122">In de interactieve, visuele werkruimte sleept u ***gegevenssets*** en analyse***modules*** naar een interactief canvas.</span><span class="sxs-lookup"><span data-stu-id="33d78-122">Using an interactive, visual workspace, you drag-and-drop ***datasets*** and analysis ***modules*** onto an interactive canvas.</span></span> <span data-ttu-id="33d78-123">U ze samen tooform verbindt een ***experimenteren*** die u uitvoert in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="33d78-123">You connect them together tooform an ***experiment*** that you run in Machine Learning Studio.</span></span>
<span data-ttu-id="33d78-124">U ***een model maken***, ***Hallo model trainen***, en ***score en test Hallo model***.</span><span class="sxs-lookup"><span data-stu-id="33d78-124">You ***create a model***, ***train hello model***, and ***score and test hello model***.</span></span>

<span data-ttu-id="33d78-125">U kunt bladeren het modelontwerp Hallo experiment bewerken en biedt uitgevoerd totdat het Hallo resultaten die u zoekt.</span><span class="sxs-lookup"><span data-stu-id="33d78-125">You can iterate on your model design, editing hello experiment and running it until it gives you hello results you're looking for.</span></span> <span data-ttu-id="33d78-126">Wanneer uw model klaar is, kunt u het publiceren als een ***webservice***, zodat anderen voorspellingen kunnen krijgen voor de nieuwe gegevens die zij toesturen.</span><span class="sxs-lookup"><span data-stu-id="33d78-126">When your model is ready, you can publish it as a ***web service*** so that others can send it new data and get predictions in return.</span></span>

## <a name="open-machine-learning-studio"></a><span data-ttu-id="33d78-127">Machine Learning Studio openen</span><span class="sxs-lookup"><span data-stu-id="33d78-127">Open Machine Learning Studio</span></span>

<span data-ttu-id="33d78-128">tooget gestart met Studio, ga te[https://studio.azureml.net](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="33d78-128">tooget started with Studio, go too[https://studio.azureml.net](https://studio.azureml.net).</span></span> <span data-ttu-id="33d78-129">Als u zich eerder hebt aangemeld bij Machine Learning Studio, klikt u op **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="33d78-129">If you’ve signed into Machine Learning Studio before, click **Sign In**.</span></span> <span data-ttu-id="33d78-130">Klik anders op **Sign Up** en kies tussen gratis en betaalde opties.</span><span class="sxs-lookup"><span data-stu-id="33d78-130">Otherwise, click **Sign up here** and choose between free and paid options.</span></span>

<span data-ttu-id="33d78-131">![Meld u aan tooMachine Learning Studio][sign-in-to-studio]
</span><span class="sxs-lookup"><span data-stu-id="33d78-131">![Sign in tooMachine Learning Studio][sign-in-to-studio]
</span></span><br/><span data-ttu-id="33d78-132">
***Meld u aan tooMachine Learning Studio***</span><span class="sxs-lookup"><span data-stu-id="33d78-132">
***Sign in tooMachine Learning Studio***</span></span>

## <a name="five-steps-toocreate-an-experiment"></a><span data-ttu-id="33d78-133">Toocreate vijf stappen een experiment</span><span class="sxs-lookup"><span data-stu-id="33d78-133">Five steps toocreate an experiment</span></span>

<span data-ttu-id="33d78-134">In deze machine learning-zelfstudie past u vijf eenvoudige stappen toobuild een experiment in Machine Learning Studio toocreate, trein, volgen en het model beoordelen:</span><span class="sxs-lookup"><span data-stu-id="33d78-134">In this machine learning tutorial, you'll follow five basic steps toobuild an experiment in Machine Learning Studio toocreate, train, and score your model:</span></span>

- <span data-ttu-id="33d78-135">**Een model maken**</span><span class="sxs-lookup"><span data-stu-id="33d78-135">**Create a model**</span></span>
    - <span data-ttu-id="33d78-136">[Stap 1: gegevens ophalen]</span><span class="sxs-lookup"><span data-stu-id="33d78-136">[Step 1: Get data]</span></span>
    - <span data-ttu-id="33d78-137">[Stap 2: Hallo gegevens voorbereiden]</span><span class="sxs-lookup"><span data-stu-id="33d78-137">[Step 2: Prepare hello data]</span></span>
    - <span data-ttu-id="33d78-138">[Stap 3: functies definiëren]</span><span class="sxs-lookup"><span data-stu-id="33d78-138">[Step 3: Define features]</span></span>
- <span data-ttu-id="33d78-139">**Hallo-model trainen**</span><span class="sxs-lookup"><span data-stu-id="33d78-139">**Train hello model**</span></span>
    - <span data-ttu-id="33d78-140">[Stap 4: een leeralgoritme kiezen en toepassen]</span><span class="sxs-lookup"><span data-stu-id="33d78-140">[Step 4: Choose and apply a learning algorithm]</span></span>
- <span data-ttu-id="33d78-141">**Score en test Hallo model**</span><span class="sxs-lookup"><span data-stu-id="33d78-141">**Score and test hello model**</span></span>
    - <span data-ttu-id="33d78-142">[Stap 5: prijzen van nieuwe auto's voorspellen]</span><span class="sxs-lookup"><span data-stu-id="33d78-142">[Step 5: Predict new automobile prices]</span></span>

[Stap 1: gegevens ophalen]: #step-1-get-data
[Stap 2: Hallo gegevens voorbereiden]: #step-2-prepare-the-data
[Stap 3: functies definiëren]: #step-3-define-features
[Stap 4: een leeralgoritme kiezen en toepassen]: #step-4-choose-and-apply-a-learning-algorithm
[Stap 5: prijzen van nieuwe auto's voorspellen]: #step-5-predict-new-automobile-prices

> [!TIP] 
> <span data-ttu-id="33d78-148">U vindt een werkexemplaar Hallo volgende experiment in Hallo [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="33d78-148">You can find a working copy of hello following experiment in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="33d78-149">Ga te**[uw eerste gegevenswetenschap experimenteren - prijzen auto's voorspellen](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)**  en klik op **openen in Studio** toodownload een kopie van het Hallo-experiment in uw Machine Learning Studio-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="33d78-149">Go too**[Your first data science experiment - Automobile price prediction](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** and click **Open in Studio** toodownload a copy of hello experiment into your Machine Learning Studio workspace.</span></span>


## <a name="step-1-get-data"></a><span data-ttu-id="33d78-150">Stap 1: gegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="33d78-150">Step 1: Get data</span></span>

<span data-ttu-id="33d78-151">Hallo eerste wat u moet tooperform machine learning is gegevens.</span><span class="sxs-lookup"><span data-stu-id="33d78-151">hello first thing you need tooperform machine learning is data.</span></span>
<span data-ttu-id="33d78-152">Machine Learning Studio bevat een aantal voorbeeldgegevenssets die u kunt gebruiken. Daarnaast kunt u uit tal van bronnen gegevens importeren.</span><span class="sxs-lookup"><span data-stu-id="33d78-152">There are several sample datasets included with Machine Learning Studio that you can use, or you can import data from many sources.</span></span> <span data-ttu-id="33d78-153">In dit voorbeeld gebruiken we Hallo voorbeeldgegevensset **Automobile price data (Raw)**, die opgenomen in de werkruimte.</span><span class="sxs-lookup"><span data-stu-id="33d78-153">For this example, we'll use hello sample dataset, **Automobile price data (Raw)**, that's included in your workspace.</span></span>
<span data-ttu-id="33d78-154">Deze gegevensset bevat vermeldingen voor verschillende auto's, inclusief informatie over het merk, het model, de technische specificaties en de prijs.</span><span class="sxs-lookup"><span data-stu-id="33d78-154">This dataset includes entries for various individual automobiles, including information such as make, model, technical specifications, and price.</span></span>

<span data-ttu-id="33d78-155">Hier ziet u hoe tooget gegevensset Hallo in uw experiment.</span><span class="sxs-lookup"><span data-stu-id="33d78-155">Here's how tooget hello dataset into your experiment.</span></span>

1. <span data-ttu-id="33d78-156">Een nieuw experiment maken door te klikken op **+ nieuw** aan de onderkant van de Hallo van Hallo Machine Learning Studio-venster, selecteer **EXPERIMENTEREN**, en selecteer vervolgens **leeg Experiment**.</span><span class="sxs-lookup"><span data-stu-id="33d78-156">Create a new experiment by clicking **+NEW** at hello bottom of hello Machine Learning Studio window, select **EXPERIMENT**, and then select **Blank Experiment**.</span></span>

2. <span data-ttu-id="33d78-157">Hallo-experiment krijgt een standaardnaam die u Hallo boven aan het Hallo-canvas zien kunt.</span><span class="sxs-lookup"><span data-stu-id="33d78-157">hello experiment is given a default name that you can see at hello top of hello canvas.</span></span> <span data-ttu-id="33d78-158">Deze tekst selecteren en de naam toosomething zinvolle, bijvoorbeeld **prijzen auto's voorspellen**.</span><span class="sxs-lookup"><span data-stu-id="33d78-158">Select this text and rename it toosomething meaningful, for example, **Automobile price prediction**.</span></span> <span data-ttu-id="33d78-159">Hallo-naam moet niet toobe uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="33d78-159">hello name doesn't need toobe unique.</span></span>

    ![Wijzig de naam van Hallo experiment][rename-experiment]

2. <span data-ttu-id="33d78-161">toohello links van het experimentcanvas Hallo zich een palet met gegevenssets en modules.</span><span class="sxs-lookup"><span data-stu-id="33d78-161">toohello left of hello experiment canvas is a palette of datasets and modules.</span></span> <span data-ttu-id="33d78-162">Type **auto** in het zoekvak Hallo Hallo boven aan dit palet toofind Hallo gegevensset met het label **Automobile price data (Raw)**.</span><span class="sxs-lookup"><span data-stu-id="33d78-162">Type **automobile** in hello Search box at hello top of this palette toofind hello dataset labeled **Automobile price data (Raw)**.</span></span> <span data-ttu-id="33d78-163">Sleep deze gegevensset toohello-experimentcanvas.</span><span class="sxs-lookup"><span data-stu-id="33d78-163">Drag this dataset toohello experiment canvas.</span></span>

    <span data-ttu-id="33d78-164">![Hallo auto gegevensset zoeken en sleep deze naar het experimentcanvas Hallo][type-automobile]
    </span><span class="sxs-lookup"><span data-stu-id="33d78-164">![Find hello automobile dataset and drag it onto hello experiment canvas][type-automobile]
    </span></span><br/>
 <span data-ttu-id="33d78-165">***Hallo auto gegevensset zoeken en sleep deze naar het experimentcanvas Hallo***</span><span class="sxs-lookup"><span data-stu-id="33d78-165">***Find hello automobile dataset and drag it onto hello experiment canvas***</span></span>

<span data-ttu-id="33d78-166">toosee wat deze gegeven eruitzien, klikt u op de uitvoerpoort Hallo HALLO hallo auto gegevensset onderaan in en selecteer vervolgens **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="33d78-166">toosee what this data looks like, click hello output port at hello bottom of hello automobile dataset, and then select **Visualize**.</span></span>

<span data-ttu-id="33d78-167">![Klik op de uitvoerpoort Hallo en selecteer 'Visualiseren'][select-visualize]
</span><span class="sxs-lookup"><span data-stu-id="33d78-167">![Click hello output port and select "Visualize"][select-visualize]
</span></span><br/><span data-ttu-id="33d78-168">
***Klik op de uitvoerpoort Hallo en selecteer 'Visualiseren'***</span><span class="sxs-lookup"><span data-stu-id="33d78-168">
***Click hello output port and select "Visualize"***</span></span>

> [!TIP]
> <span data-ttu-id="33d78-169">Gegevenssets en modules hebben invoer en uitvoerpoorten dat wordt vertegenwoordigd door cirkeltjes - ingangspoorten boven Hallo uitvoer poorten Hallo onderaan.</span><span class="sxs-lookup"><span data-stu-id="33d78-169">Datasets and modules have input and output ports represented by small circles - input ports at hello top, output ports at hello bottom.</span></span>
<span data-ttu-id="33d78-170">een stroom van gegevens door uw experiment toocreate, maakt u verbinding met een uitvoerpoort van één module tooan invoerpoort van een andere.</span><span class="sxs-lookup"><span data-stu-id="33d78-170">toocreate a flow of data through your experiment, you'll connect an output port of one module tooan input port of another.</span></span>
<span data-ttu-id="33d78-171">Op elk gewenst moment kunt u de uitvoerpoort Hallo van een dataset of module toosee welke gegevens Hallo ziet er op dat moment in de gegevensstroom Hallo.</span><span class="sxs-lookup"><span data-stu-id="33d78-171">At any time, you can click hello output port of a dataset or module toosee what hello data looks like at that point in hello data flow.</span></span>

<span data-ttu-id="33d78-172">Elk exemplaar van een auto wordt weergegeven als een rij in deze dataset voorbeeld en Hallo variabelen die zijn gekoppeld aan elke auto worden weergegeven als kolommen.</span><span class="sxs-lookup"><span data-stu-id="33d78-172">In this sample dataset, each instance of an automobile appears as a row, and hello variables associated with each automobile appear as columns.</span></span> <span data-ttu-id="33d78-173">Hallo variabelen gegeven voor een specifieke auto, gaan we tootry toopredict Hallo prijs in de meest rechtse kolom (kolom 26, met de titel ' price').</span><span class="sxs-lookup"><span data-stu-id="33d78-173">Given hello variables for a specific automobile, we're going tootry toopredict hello price in far-right column (column 26, titled "price").</span></span>

<span data-ttu-id="33d78-174">![Hallo auto gegevens weergeven in visualisatievenster Hallo-gegevens][visualize-auto-data]
</span><span class="sxs-lookup"><span data-stu-id="33d78-174">![View hello automobile data in hello data visualization window][visualize-auto-data]
</span></span><br/><span data-ttu-id="33d78-175">
***Hallo auto gegevens weergeven in visualisatievenster Hallo-gegevens***</span><span class="sxs-lookup"><span data-stu-id="33d78-175">
***View hello automobile data in hello data visualization window***</span></span>

<span data-ttu-id="33d78-176">Sluit Hallo visualisatievenster door te klikken op Hallo '**x**' in de rechterbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="33d78-176">Close hello visualization window by clicking hello "**x**" in hello upper-right corner.</span></span>

## <a name="step-2-prepare-hello-data"></a><span data-ttu-id="33d78-177">Stap 2: Hallo gegevens voorbereiden</span><span class="sxs-lookup"><span data-stu-id="33d78-177">Step 2: Prepare hello data</span></span>

<span data-ttu-id="33d78-178">Normaal gesproken moet een gegevensset worden voorverwerkt voordat deze kan worden geanalyseerd.</span><span class="sxs-lookup"><span data-stu-id="33d78-178">A dataset usually requires some preprocessing before it can be analyzed.</span></span> <span data-ttu-id="33d78-179">Bijvoorbeeld, u mogelijk opgevallen Hallo waarden aanwezig zijn in Hallo kolommen van verschillende rijen ontbreken.</span><span class="sxs-lookup"><span data-stu-id="33d78-179">For example, you might have noticed hello missing values present in hello columns of various rows.</span></span> <span data-ttu-id="33d78-180">Deze ontbrekende waarden moeten toobe opgeschoond, zodat het Hallo-model correct Hallo gegevens kunt analyseren.</span><span class="sxs-lookup"><span data-stu-id="33d78-180">These missing values need toobe cleaned so hello model can analyze hello data correctly.</span></span> <span data-ttu-id="33d78-181">In ons geval verwijderen we de rijen met ontbrekende waarden.</span><span class="sxs-lookup"><span data-stu-id="33d78-181">In our case, we'll remove any rows that have missing values.</span></span> <span data-ttu-id="33d78-182">Bovendien Hallo **normalized-losses** kolom heeft een groot deel van de ontbrekende waarden zo worden uitgesloten die kolom uit Hallo model helemaal.</span><span class="sxs-lookup"><span data-stu-id="33d78-182">Also, hello **normalized-losses** column has a large proportion of missing values, so we'll exclude that column from hello model altogether.</span></span>

> [!TIP]
> <span data-ttu-id="33d78-183">Reinigingstape Hallo ontbrekende invoergegevens is een vereiste voor het gebruik van de meeste Hallo-modules.</span><span class="sxs-lookup"><span data-stu-id="33d78-183">Cleaning hello missing values from input data is a prerequisite for using most of hello modules.</span></span>

<span data-ttu-id="33d78-184">Eerst wordt een module die Hallo verwijdert toevoegen **normalized-losses** kolom volledig, en voeg er een andere module die rijen met ontbrekende gegevens verwijdert.</span><span class="sxs-lookup"><span data-stu-id="33d78-184">First we add a module that removes hello **normalized-losses** column completely, and then we add another module that removes any row that has missing data.</span></span>

1. <span data-ttu-id="33d78-185">Type **kolommen selecteren** in het zoekvak Hallo Hallo boven aan het Hallo-module palet toofind hello [Select Columns in Dataset] [ select-columns] -module, sleept u deze toohello experimentcanvas .</span><span class="sxs-lookup"><span data-stu-id="33d78-185">Type **select columns** in hello Search box at hello top of hello module palette toofind hello [Select Columns in Dataset][select-columns] module, then drag it toohello experiment canvas.</span></span> <span data-ttu-id="33d78-186">Deze module kunt tooselect welke kolommen met gegevens die we wilt tooinclude in of uitsluiten Hallo model.</span><span class="sxs-lookup"><span data-stu-id="33d78-186">This module allows us tooselect which columns of data we want tooinclude or exclude in hello model.</span></span>

2. <span data-ttu-id="33d78-187">Verbinding maken met de uitvoerpoort Hallo Hallo **Automobile price data (Raw)** gegevensset toohello invoer poort Hallo [Select Columns in Dataset] [ select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="33d78-187">Connect hello output port of hello **Automobile price data (Raw)** dataset toohello input port of hello [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="33d78-188">![Toevoegen Hallo 'Kolommen in gegevensset selecteren' module toohello-experimentcanvas en koppel][type-select-columns]
    </span><span class="sxs-lookup"><span data-stu-id="33d78-188">![Add hello "Select Columns in Dataset" module toohello experiment canvas and connect it][type-select-columns]
    </span></span><br/>
 <span data-ttu-id="33d78-189">***Toevoegen Hallo 'Kolommen in gegevensset selecteren' module toohello-experimentcanvas en koppel***</span><span class="sxs-lookup"><span data-stu-id="33d78-189">***Add hello "Select Columns in Dataset" module toohello experiment canvas and connect it***</span></span>

3. <span data-ttu-id="33d78-190">Klik op Hallo [Select Columns in Dataset] [ select-columns] module en klikt u op **Launch column selector** in Hallo **eigenschappen** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="33d78-190">Click hello [Select Columns in Dataset][select-columns] module and click **Launch column selector** in hello **Properties** pane.</span></span>

    - <span data-ttu-id="33d78-191">Klik aan de linkerkant Hallo op **met regels**</span><span class="sxs-lookup"><span data-stu-id="33d78-191">On hello left, click **With rules**</span></span>
    - <span data-ttu-id="33d78-192">Klik onder **Begin With** op **All columns**.</span><span class="sxs-lookup"><span data-stu-id="33d78-192">Under **Begin With**, click **All columns**.</span></span> <span data-ttu-id="33d78-193">Dit zorgt ervoor dat [Select Columns in Dataset] [ select-columns] toopass via alle Hallo kolommen (met uitzondering van die kolommen we over tooexclude).</span><span class="sxs-lookup"><span data-stu-id="33d78-193">This directs [Select Columns in Dataset][select-columns] toopass through all hello columns (except those columns we're about tooexclude).</span></span>
    - <span data-ttu-id="33d78-194">Selecteer in het Hallo-vervolgkeuzelijsten **uitsluiten** en **kolomnamen**, en klik vervolgens in het tekstvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="33d78-194">From hello drop-downs, select **Exclude** and **column names**, and then click inside hello text box.</span></span> <span data-ttu-id="33d78-195">Er wordt een lijst met kolommen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="33d78-195">A list of columns is displayed.</span></span> <span data-ttu-id="33d78-196">Selecteer **normalized-losses**, en het tekstvak toegevoegde toohello is.</span><span class="sxs-lookup"><span data-stu-id="33d78-196">Select **normalized-losses**, and it's added toohello text box.</span></span>
    - <span data-ttu-id="33d78-197">Klik op Hallo vinkje (OK) knop tooclose Hallo kolomkiezer (op Hallo rechtsonder).</span><span class="sxs-lookup"><span data-stu-id="33d78-197">Click hello check mark (OK) button tooclose hello column selector (on hello lower-right).</span></span>

    <span data-ttu-id="33d78-198">![Hallo kolomkiezer Start en Hallo 'normalized-losses' kolom uitsluiten][launch-column-selector]
    </span><span class="sxs-lookup"><span data-stu-id="33d78-198">![Launch hello column selector and exclude hello "normalized-losses" column][launch-column-selector]
    </span></span><br/>
 <span data-ttu-id="33d78-199">***Hallo kolomkiezer Start en Hallo 'normalized-losses' kolom uitsluiten***</span><span class="sxs-lookup"><span data-stu-id="33d78-199">***Launch hello column selector and exclude hello "normalized-losses" column***</span></span>

    <span data-ttu-id="33d78-200">Nu Hallo eigenschappendeelvenster voor **Select Columns in Dataset** geeft aan dat deze worden doorgegeven alle kolommen uit de dataset Hallo behalve **normalized-losses**.</span><span class="sxs-lookup"><span data-stu-id="33d78-200">Now hello properties pane for **Select Columns in Dataset** indicates that it will pass through all columns from hello dataset except **normalized-losses**.</span></span>

    <span data-ttu-id="33d78-201">![Hallo eigenschappendeelvenster bevat dat die 'normalized-losses' Hallo-kolom is uitgesloten.][showing-excluded-column]
    </span><span class="sxs-lookup"><span data-stu-id="33d78-201">![hello properties pane shows that hello "normalized-losses" column is excluded][showing-excluded-column]
    </span></span><br/>
 <span data-ttu-id="33d78-202">***Hallo eigenschappendeelvenster bevat dat die 'normalized-losses' Hallo-kolom is uitgesloten.***</span><span class="sxs-lookup"><span data-stu-id="33d78-202">***hello properties pane shows that hello "normalized-losses" column is excluded***</span></span>

    > [!TIP]
    <span data-ttu-id="33d78-203">U kunt een opmerking tooa module door te dubbelklikken op Hallo-module en tekstinvoer toevoegen.</span><span class="sxs-lookup"><span data-stu-id="33d78-203">You can add a comment tooa module by double-clicking hello module and entering text.</span></span> <span data-ttu-id="33d78-204">Hiermee kunt u in één oogopslag zien welke Hallo-module in uw experiment doet.</span><span class="sxs-lookup"><span data-stu-id="33d78-204">This can help you see at a glance what hello module is doing in your experiment.</span></span> <span data-ttu-id="33d78-205">Dubbelklik in dit geval op Hallo [Select Columns in Dataset] [ select-columns] module en type Hallo opmerking "Uitsluiten genormaliseerd verliezen."</span><span class="sxs-lookup"><span data-stu-id="33d78-205">In this case double-click hello [Select Columns in Dataset][select-columns] module and type hello comment "Exclude normalized losses."</span></span>
    >
    >


    <span data-ttu-id="33d78-206">![Dubbelklik op een module tooadd een opmerking][add-comment]
    </span><span class="sxs-lookup"><span data-stu-id="33d78-206">![Double-click a module tooadd a comment][add-comment]
    </span></span><br/>
 <span data-ttu-id="33d78-207">***Dubbelklik op een module tooadd een opmerking***</span><span class="sxs-lookup"><span data-stu-id="33d78-207">***Double-click a module tooadd a comment***</span></span>

3. <span data-ttu-id="33d78-208">Sleep Hallo [Clean Missing Data] [ clean-missing-data] module toohello experimenteren canvas en verbindt u deze toohello [Select Columns in Dataset] [ select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="33d78-208">Drag hello [Clean Missing Data][clean-missing-data] module toohello experiment canvas and connect it toohello [Select Columns in Dataset][select-columns] module.</span></span> <span data-ttu-id="33d78-209">In Hallo **eigenschappen** deelvenster **hele rij verwijderen** onder **Cleaning mode**.</span><span class="sxs-lookup"><span data-stu-id="33d78-209">In hello **Properties** pane, select **Remove entire row** under **Cleaning mode**.</span></span> <span data-ttu-id="33d78-210">Dit zorgt ervoor dat [Clean Missing Data] [ clean-missing-data] tooclean Hallo gegevens door het verwijderen van rijen met ontbrekende waarden.</span><span class="sxs-lookup"><span data-stu-id="33d78-210">This directs [Clean Missing Data][clean-missing-data] tooclean hello data by removing rows that have any missing values.</span></span> <span data-ttu-id="33d78-211">Dubbelklik op Hallo-module en typ Hallo-Opmerking 'Rijen met ontbrekende waarde verwijderen'.</span><span class="sxs-lookup"><span data-stu-id="33d78-211">Double-click hello module and type hello comment "Remove missing value rows."</span></span>

    <span data-ttu-id="33d78-212">![Hallo reinigingstape modus te ' hele rij verwijderen' voor Hallo 'Clean Missing Data' module][set-remove-entire-row]
    </span><span class="sxs-lookup"><span data-stu-id="33d78-212">![Set hello cleaning mode too"Remove entire row" for hello "Clean Missing Data" module][set-remove-entire-row]
    </span></span><br/>
 <span data-ttu-id="33d78-213">***Hallo reinigingstape modus te ' hele rij verwijderen' voor Hallo 'Clean Missing Data' module***</span><span class="sxs-lookup"><span data-stu-id="33d78-213">***Set hello cleaning mode too"Remove entire row" for hello "Clean Missing Data" module***</span></span>

4. <span data-ttu-id="33d78-214">Hallo-experiment uitvoeren door te klikken op **uitvoeren** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="33d78-214">Run hello experiment by clicking **RUN** at hello bottom of hello page.</span></span>

    <span data-ttu-id="33d78-215">Wanneer Hallo experiment is voltooid, hebben alle Hallo modules een groen vinkje tooindicate die deze zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="33d78-215">When hello experiment has finished running, all hello modules have a green check mark tooindicate that they finished successfully.</span></span> <span data-ttu-id="33d78-216">U ziet ook Hallo **uitgevoerd** status in de rechterbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="33d78-216">Notice also hello **Finished running** status in hello upper-right corner.</span></span>

<span data-ttu-id="33d78-217">![Na het uitvoeren van het ziet Hallo-experiment er ongeveer als volgt][early-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="33d78-217">![After running it, hello experiment should look something like this][early-experiment-run]
</span></span><br/><span data-ttu-id="33d78-218">
***Na het uitvoeren van het ziet Hallo-experiment er ongeveer als volgt***</span><span class="sxs-lookup"><span data-stu-id="33d78-218">
***After running it, hello experiment should look something like this***</span></span>

> [!TIP]
> <span data-ttu-id="33d78-219">Waarom we Hallo experiment nu uitvoeren?</span><span class="sxs-lookup"><span data-stu-id="33d78-219">Why did we run hello experiment now?</span></span> <span data-ttu-id="33d78-220">Door actieve Hallo-experiment Hallo kolomdefinities voor onze gegevens uit de dataset hello, via Hallo doorgeven [Select Columns in Dataset] [ select-columns] -module, en via Hallo [Clean Missing Data] [ clean-missing-data] module.</span><span class="sxs-lookup"><span data-stu-id="33d78-220">By running hello experiment, hello column definitions for our data pass from hello dataset, through hello [Select Columns in Dataset][select-columns] module, and through hello [Clean Missing Data][clean-missing-data] module.</span></span> <span data-ttu-id="33d78-221">Dit betekent dat alle modules die we verbinding te maken[Clean Missing Data] [ clean-missing-data] heeft ook dezelfde informatie.</span><span class="sxs-lookup"><span data-stu-id="33d78-221">This means that any modules we connect too[Clean Missing Data][clean-missing-data] will also have this same information.</span></span>

<span data-ttu-id="33d78-222">Hallo-experiment toothis punt hebben we schone Hallo gegevens is.</span><span class="sxs-lookup"><span data-stu-id="33d78-222">All we have done in hello experiment up toothis point is clean hello data.</span></span> <span data-ttu-id="33d78-223">Als u wilt dat tooview Hallo gereinigd gegevensset, klikt u op Hallo uitvoerpoort Hallo links [Clean Missing Data] [ clean-missing-data] module en selecteer **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="33d78-223">If you want tooview hello cleaned dataset, click hello left output port of hello [Clean Missing Data][clean-missing-data] module and select **Visualize**.</span></span> <span data-ttu-id="33d78-224">U ziet dat Hallo **normalized-losses** kolom is niet meer opgenomen en er zijn geen ontbrekende waarden.</span><span class="sxs-lookup"><span data-stu-id="33d78-224">Notice that hello **normalized-losses** column is no longer included, and there are no missing values.</span></span>

<span data-ttu-id="33d78-225">Nu dat Hallo gegevens opgeschoond zijn, we klaar toospecify welke functies we gaan toouse in Hallo Voorspellend model.</span><span class="sxs-lookup"><span data-stu-id="33d78-225">Now that hello data is clean, we're ready toospecify what features we're going toouse in hello predictive model.</span></span>

## <a name="step-3-define-features"></a><span data-ttu-id="33d78-226">Stap 3: functies definiëren</span><span class="sxs-lookup"><span data-stu-id="33d78-226">Step 3: Define features</span></span>

<span data-ttu-id="33d78-227">In machine learning zijn *functies* afzonderlijke meetbare eigenschappen van iets waarin u geïnteresseerd bent.</span><span class="sxs-lookup"><span data-stu-id="33d78-227">In machine learning, *features* are individual measurable properties of something you’re interested in.</span></span> <span data-ttu-id="33d78-228">In onze gegevensset staat elke rij voor één auto en elke kolom bevat een kenmerk van die auto.</span><span class="sxs-lookup"><span data-stu-id="33d78-228">In our dataset, each row represents one automobile, and each column is a feature of that automobile.</span></span>

<span data-ttu-id="33d78-229">Zoeken naar een goede set kenmerken voor het maken van een Voorspellend model moet u experimenteren en kennis over Hallo probleem u toosolve.</span><span class="sxs-lookup"><span data-stu-id="33d78-229">Finding a good set of features for creating a predictive model requires experimentation and knowledge about hello problem you want toosolve.</span></span> <span data-ttu-id="33d78-230">Sommige functies zijn beter voor het voorspellen van Hallo doel dan andere.</span><span class="sxs-lookup"><span data-stu-id="33d78-230">Some features are better for predicting hello target than others.</span></span> <span data-ttu-id="33d78-231">Bovendien bestaat er tussen sommige kenmerken een nauwe correlatie. Deze kunnen daarom worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="33d78-231">Also, some features have a strong correlation with other features and can be removed.</span></span> <span data-ttu-id="33d78-232">Bijvoorbeeld, zijn city-mpg en highway-mpg nauw verwant zodat we kunt een houden en andere Hallo verwijderen zonder aanzienlijke gevolgen hebben voor de voorspelling Hallo.</span><span class="sxs-lookup"><span data-stu-id="33d78-232">For example, city-mpg and highway-mpg are closely related so we can keep one and remove hello other without significantly affecting hello prediction.</span></span>

<span data-ttu-id="33d78-233">Laten we een model bouwen dat gebruikmaakt van een subset van Hallo functies in onze gegevensset.</span><span class="sxs-lookup"><span data-stu-id="33d78-233">Let's build a model that uses a subset of hello features in our dataset.</span></span> <span data-ttu-id="33d78-234">U kunt later terugkeren en andere kenmerken selecteren, Hallo experiment opnieuw uitvoeren en zien als u betere resultaten krijgt.</span><span class="sxs-lookup"><span data-stu-id="33d78-234">You can come back later and select different features, run hello experiment again, and see if you get better results.</span></span> <span data-ttu-id="33d78-235">Maar toostart, gaan we proberen Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="33d78-235">But toostart, let's try hello following features:</span></span>

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. <span data-ttu-id="33d78-236">Sleep nog een [Select Columns in Dataset] [ select-columns] module toohello experimenteren canvas.</span><span class="sxs-lookup"><span data-stu-id="33d78-236">Drag another [Select Columns in Dataset][select-columns] module toohello experiment canvas.</span></span> <span data-ttu-id="33d78-237">Hallo links uitvoerpoort Hallo verbinding [Clean Missing Data] [ clean-missing-data] module-invoer toohello Hallo [Select Columns in Dataset] [ select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="33d78-237">Connect hello left output port of hello [Clean Missing Data][clean-missing-data] module toohello input of hello [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="33d78-238">![Verbinding maken met de Hallo 'Kolommen in gegevensset selecteren' module toohello 'Clean Missing Data' module][connect-clean-to-select]
    </span><span class="sxs-lookup"><span data-stu-id="33d78-238">![Connect hello "Select Columns in Dataset" module toohello "Clean Missing Data" module][connect-clean-to-select]
    </span></span><br/>
 <span data-ttu-id="33d78-239">***Verbinding maken met de Hallo 'Kolommen in gegevensset selecteren' module toohello 'Clean Missing Data' module***</span><span class="sxs-lookup"><span data-stu-id="33d78-239">***Connect hello "Select Columns in Dataset" module toohello "Clean Missing Data" module***</span></span>

2. <span data-ttu-id="33d78-240">Dubbelklik op Hallo-module en typ "Select functies voor de prognose."</span><span class="sxs-lookup"><span data-stu-id="33d78-240">Double-click hello module and type "Select features for prediction."</span></span>

2. <span data-ttu-id="33d78-241">Klik op **Launch column selector** in Hallo **eigenschappen** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="33d78-241">Click **Launch column selector** in hello **Properties** pane.</span></span>

3. <span data-ttu-id="33d78-242">Klik op **With rules**.</span><span class="sxs-lookup"><span data-stu-id="33d78-242">Click **With rules**.</span></span>

4. <span data-ttu-id="33d78-243">Klik onder **Begin With** op **No columns**.</span><span class="sxs-lookup"><span data-stu-id="33d78-243">Under **Begin With**, click **No columns**.</span></span> <span data-ttu-id="33d78-244">Selecteer in de filterrij hello, **opnemen** en **kolomnamen** en onze lijst met kolomnamen in het tekstvak Hallo selecteert.</span><span class="sxs-lookup"><span data-stu-id="33d78-244">In hello filter row, select **Include** and **column names** and select our list of column names in hello text box.</span></span> <span data-ttu-id="33d78-245">Dit stuurt Hallo module toonot pass through-kolommen (functies), behalve Hallo toepassingsgroepen die wij opgeven.</span><span class="sxs-lookup"><span data-stu-id="33d78-245">This directs hello module toonot pass through any columns (features) except hello ones that we specify.</span></span>

5. <span data-ttu-id="33d78-246">Klik op Hallo vinkje (OK).</span><span class="sxs-lookup"><span data-stu-id="33d78-246">Click hello check mark (OK) button.</span></span>

    <span data-ttu-id="33d78-247">![Hallo kolommen (functies) tooinclude in Hallo voorspelling selecteren][select-columns-to-include]
    </span><span class="sxs-lookup"><span data-stu-id="33d78-247">![Select hello columns (features) tooinclude in hello prediction][select-columns-to-include]
    </span></span><br/>
 <span data-ttu-id="33d78-248">***Hallo kolommen (functies) tooinclude in Hallo voorspelling selecteren***</span><span class="sxs-lookup"><span data-stu-id="33d78-248">***Select hello columns (features) tooinclude in hello prediction***</span></span>

<span data-ttu-id="33d78-249">Dit resulteert in een gefilterde gegevensset met alleen Hallo functies willen we toopass toohello learning-algoritme we in de volgende stap Hallo gebruiken.</span><span class="sxs-lookup"><span data-stu-id="33d78-249">This produces a filtered dataset containing only hello features we want toopass toohello learning algorithm we'll use in hello next step.</span></span> <span data-ttu-id="33d78-250">U kunt later terugkeren en het opnieuw proberen met een andere selectie kenmerken.</span><span class="sxs-lookup"><span data-stu-id="33d78-250">Later, you can return and try again with a different selection of features.</span></span>

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a><span data-ttu-id="33d78-251">Stap 4: een leeralgoritme kiezen en toepassen</span><span class="sxs-lookup"><span data-stu-id="33d78-251">Step 4: Choose and apply a learning algorithm</span></span>

<span data-ttu-id="33d78-252">Nu dat Hallo gegevens klaar is, bestaat een Voorspellend model bouwen uit trainen en te testen.</span><span class="sxs-lookup"><span data-stu-id="33d78-252">Now that hello data is ready, constructing a predictive model consists of training and testing.</span></span> <span data-ttu-id="33d78-253">We gebruiken onze gegevens tootrain Hallo-model en controleert we Hallo model toosee hoe nauwkeurig is kunnen toopredict prijzen.</span><span class="sxs-lookup"><span data-stu-id="33d78-253">We'll use our data tootrain hello model, and then we'll test hello model toosee how closely it's able toopredict prices.</span></span>
<!-- For now, don't worry about *why* we need tootrain and then test a model.-->

<span data-ttu-id="33d78-254">*Classificatie* en *regressie* zijn twee soorten beheerde machine learning-algoritmen.</span><span class="sxs-lookup"><span data-stu-id="33d78-254">*Classification* and *regression* are two types of supervised machine learning algorithms.</span></span> <span data-ttu-id="33d78-255">Classificatie voorspelt een antwoord uit een gedefinieerde set categorieën, zoals een kleur (rood, blauw of groen).</span><span class="sxs-lookup"><span data-stu-id="33d78-255">Classification predicts an answer from a defined set of categories, such as a color (red, blue, or green).</span></span> <span data-ttu-id="33d78-256">Regressie is gebruikte toopredict een getal.</span><span class="sxs-lookup"><span data-stu-id="33d78-256">Regression is used toopredict a number.</span></span>

<span data-ttu-id="33d78-257">Aangezien we prijs toopredict, dat een getal is, gebruiken we een regression-algoritme.</span><span class="sxs-lookup"><span data-stu-id="33d78-257">Because we want toopredict price, which is a number, we'll use a regression algorithm.</span></span> <span data-ttu-id="33d78-258">In dit voorbeeld gebruiken we een eenvoudig *lineair regressiemodel*.</span><span class="sxs-lookup"><span data-stu-id="33d78-258">For this example, we'll use a simple *linear regression* model.</span></span>

> [!TIP]
> <span data-ttu-id="33d78-259">Als u meer informatie over de verschillende soorten machine learning-algoritmen toolearn wilt en wanneer toouse ze u mogelijk Hallo eerste video bekijken in Hallo Gegevenswetenschap voor beginnende gebruikers reeks, [Hallo vijf gegevens wetenschappelijke antwoorden op vragen](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="33d78-259">If you want toolearn more about different types of machine learning algorithms and when toouse them, you might view hello first video in hello Data Science for Beginners series, [hello five questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span> <span data-ttu-id="33d78-260">U kunt ook zoeken op Hallo infographic [Machine learning-algoritme voorbeelden voor alledaagse](machine-learning-basics-infographic-with-algorithm-examples.md), of uitchecken Hallo [Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md).</span><span class="sxs-lookup"><span data-stu-id="33d78-260">You might also look at hello infographic [Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md), or check out hello [Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md).</span></span>

<span data-ttu-id="33d78-261">We trainen Hallo model door middel van een set gegevens die Hallo prijs bevat.</span><span class="sxs-lookup"><span data-stu-id="33d78-261">We train hello model by giving it a set of data that includes hello price.</span></span> <span data-ttu-id="33d78-262">Hallo model scant Hallo gegevens en zoeken naar correlatie tussen een auto-functies en de prijs.</span><span class="sxs-lookup"><span data-stu-id="33d78-262">hello model scans hello data and look for correlations between an automobile's features and its price.</span></span> <span data-ttu-id="33d78-263">Klik er Hallo model wordt getest - we een aantal functies voor auto's, die we bekend met bent geven en Zie hoe dicht in Hallo model toopredicting Hallo bekende prijs wordt geleverd.</span><span class="sxs-lookup"><span data-stu-id="33d78-263">Then we'll test hello model - we'll give it a set of features for automobiles we're familiar with and see how close hello model comes toopredicting hello known price.</span></span>

<span data-ttu-id="33d78-264">We gebruiken onze gegevens voor zowel Hallo model trainings- en testen van het door het Hallo-gegevens verdelen in afzonderlijke trainings- en testdoeleinden gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="33d78-264">We'll use our data for both training hello model and testing it by splitting hello data into separate training and testing datasets.</span></span>

1. <span data-ttu-id="33d78-265">Selecteer en sleep Hallo [Split Data] [ split] module toohello experimenteren canvas en verbindt dit laatste toohello [Select Columns in Dataset] [ select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="33d78-265">Select and drag hello [Split Data][split] module toohello experiment canvas and connect it toohello last [Select Columns in Dataset][select-columns] module.</span></span>

2. <span data-ttu-id="33d78-266">Klik op Hallo [Split Data] [ split] module tooselect deze.</span><span class="sxs-lookup"><span data-stu-id="33d78-266">Click hello [Split Data][split] module tooselect it.</span></span> <span data-ttu-id="33d78-267">Hallo zoeken **fractie van rijen in Hallo eerst uitvoergegevensset** (in Hallo **eigenschappen** deelvenster toohello rechts van het canvas Hallo) en stel deze too0.75.</span><span class="sxs-lookup"><span data-stu-id="33d78-267">Find hello **Fraction of rows in hello first output dataset** (in hello **Properties** pane toohello right of hello canvas) and set it too0.75.</span></span> <span data-ttu-id="33d78-268">Deze manier kunnen we 75 procent van de tootrain Hallo-Hallo gegevensmodel gebruiken en 25 procent voor het testen van hinderen (later kunt u experimenteren met het gebruik van verschillende percentages).</span><span class="sxs-lookup"><span data-stu-id="33d78-268">This way, we'll use 75 percent of hello data tootrain hello model, and hold back 25 percent for testing (later, you can experiment with using different percentages).</span></span>

    <span data-ttu-id="33d78-269">![Set Hallo fractie van Hallo 'Split Data' module too0.75 splitsen][set-split-data-percentage]
    </span><span class="sxs-lookup"><span data-stu-id="33d78-269">![Set hello split fraction of hello "Split Data" module too0.75][set-split-data-percentage]
    </span></span><br/>
 <span data-ttu-id="33d78-270">***Set Hallo fractie van Hallo 'Split Data' module too0.75 splitsen***</span><span class="sxs-lookup"><span data-stu-id="33d78-270">***Set hello split fraction of hello "Split Data" module too0.75***</span></span>

    > [!TIP]
    > <span data-ttu-id="33d78-271">Door het wijzigen van Hallo **willekeurige seed** parameter, kunt u verschillende willekeurig samples voor trainings- en testdoeleinden produceren.</span><span class="sxs-lookup"><span data-stu-id="33d78-271">By changing hello **Random seed** parameter, you can produce different random samples for training and testing.</span></span> <span data-ttu-id="33d78-272">Deze parameter bepaalt Hallo seeding van de pseudo-willekeurige nummergenerator Hallo.</span><span class="sxs-lookup"><span data-stu-id="33d78-272">This parameter controls hello seeding of hello pseudo-random number generator.</span></span>

2. <span data-ttu-id="33d78-273">Hallo-experiment uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="33d78-273">Run hello experiment.</span></span> <span data-ttu-id="33d78-274">Wanneer Hallo experiment wordt uitgevoerd, Hallo [Select Columns in Dataset] [ select-columns] en [Split Data] [ split] modules kolom definities toohello doorgeven modules die we hierna zullen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="33d78-274">When hello experiment is run, hello [Select Columns in Dataset][select-columns] and [Split Data][split] modules pass column definitions toohello modules we'll be adding next.</span></span>  

3. <span data-ttu-id="33d78-275">tooselect hello learning-algoritme, vouw Hallo **Machine Learning** categorie in Hallo module palet toohello links Hallo canvas uit en vouw vervolgens **Model initialiseren**.</span><span class="sxs-lookup"><span data-stu-id="33d78-275">tooselect hello learning algorithm, expand hello **Machine Learning** category in hello module palette toohello left of hello canvas, and then expand **Initialize Model**.</span></span> <span data-ttu-id="33d78-276">Hiermee worden verschillende categorieën die gebruikte tooinitialize machine learning-algoritmen kunnen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="33d78-276">This displays several categories of modules that can be used tooinitialize machine learning algorithms.</span></span> <span data-ttu-id="33d78-277">Selecteer voor dit experiment Hallo [lineaire regressie] [ linear-regression] module onder Hallo **regressie** categorie en sleep het experimentcanvas toohello.</span><span class="sxs-lookup"><span data-stu-id="33d78-277">For this experiment, select hello [Linear Regression][linear-regression] module under hello **Regression** category, and drag it toohello experiment canvas.</span></span>
<span data-ttu-id="33d78-278">(U kunt ook de module Hallo vinden door 'linear regression' hello palet zoekvak te typen.)</span><span class="sxs-lookup"><span data-stu-id="33d78-278">(You can also find hello module by typing "linear regression" in hello palette Search box.)</span></span>

4. <span data-ttu-id="33d78-279">Zoek en sleep Hallo [Train Model] [ train-model] module toohello experimenteren canvas.</span><span class="sxs-lookup"><span data-stu-id="33d78-279">Find and drag hello [Train Model][train-model] module toohello experiment canvas.</span></span> <span data-ttu-id="33d78-280">Verbinding maken met uitvoer Hallo Hallo [lineaire regressie] [ linear-regression] module toohello links invoer Hallo [Train Model] [ train-model] module en maak verbinding Hallo training gegevensuitvoer (poort links) Hallo [Split Data] [ split] module toohello juiste invoerwaarden Hallo [Train Model] [ train-model] module.</span><span class="sxs-lookup"><span data-stu-id="33d78-280">Connect hello output of hello [Linear Regression][linear-regression] module toohello left input of hello [Train Model][train-model] module, and connect hello training data output (left port) of hello [Split Data][split] module toohello right input of hello [Train Model][train-model] module.</span></span>

    <span data-ttu-id="33d78-281">![Verbinding maken met de Hallo 'Train-Model' module tooboth Hallo 'Linear Regression' en 'Split Data'-modules][connect-train-model]
    </span><span class="sxs-lookup"><span data-stu-id="33d78-281">![Connect hello "Train Model" module tooboth hello "Linear Regression" and "Split Data" modules][connect-train-model]
    </span></span><br/>
 <span data-ttu-id="33d78-282">***Verbinding maken met de Hallo 'Train-Model' module tooboth Hallo 'Linear Regression' en 'Split Data'-modules***</span><span class="sxs-lookup"><span data-stu-id="33d78-282">***Connect hello "Train Model" module tooboth hello "Linear Regression" and "Split Data" modules***</span></span>

5. <span data-ttu-id="33d78-283">Klik op Hallo [Train Model] [ train-model] -module, klikt u op **Launch column selector** in Hallo **eigenschappen** deelvenster en selecteer vervolgens Hallo **prijs** kolom.</span><span class="sxs-lookup"><span data-stu-id="33d78-283">Click hello [Train Model][train-model] module, click **Launch column selector** in hello **Properties** pane, and then select hello **price** column.</span></span> <span data-ttu-id="33d78-284">Dit is dat het model momenteel toopredict is Hallo-waarde.</span><span class="sxs-lookup"><span data-stu-id="33d78-284">This is hello value that our model is going toopredict.</span></span>

    <span data-ttu-id="33d78-285">U selecteert Hallo **prijs** kolom in de kolomkiezer Hallo door deze te verplaatsen van Hallo **beschikbare kolommen** lijst toohello **kolommen geselecteerd** lijst.</span><span class="sxs-lookup"><span data-stu-id="33d78-285">You select hello **price** column in hello column selector by moving it from hello **Available columns** list toohello **Selected columns** list.</span></span>

    <span data-ttu-id="33d78-286">![Hallo prijs kolom voor Hallo 'Train-Model' module selecteren][select-price-column]
    </span><span class="sxs-lookup"><span data-stu-id="33d78-286">![Select hello price column for hello "Train Model" module][select-price-column]
    </span></span><br/>
 <span data-ttu-id="33d78-287">***Hallo prijs kolom voor Hallo 'Train-Model' module selecteren***</span><span class="sxs-lookup"><span data-stu-id="33d78-287">***Select hello price column for hello "Train Model" module***</span></span>

6. <span data-ttu-id="33d78-288">Hallo-experiment uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="33d78-288">Run hello experiment.</span></span>

<span data-ttu-id="33d78-289">We hebben nu een getraind regressiemodel dat gebruikt tooscore nieuwe auto gegevens toomake prijs voorspellingen worden kan.</span><span class="sxs-lookup"><span data-stu-id="33d78-289">We now have a trained regression model that can be used tooscore new automobile data toomake price predictions.</span></span>

<span data-ttu-id="33d78-290">![Na uitvoering is ziet Hallo experiment er nu ongeveer het volgende][second-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="33d78-290">![After running, hello experiment should now look something like this][second-experiment-run]
</span></span><br/><span data-ttu-id="33d78-291">
***Na uitvoering is ziet Hallo experiment er nu ongeveer het volgende***</span><span class="sxs-lookup"><span data-stu-id="33d78-291">
***After running, hello experiment should now look something like this***</span></span>

## <a name="step-5-predict-new-automobile-prices"></a><span data-ttu-id="33d78-292">Stap 5: prijzen van nieuwe auto's voorspellen</span><span class="sxs-lookup"><span data-stu-id="33d78-292">Step 5: Predict new automobile prices</span></span>

<span data-ttu-id="33d78-293">Nu dat we Hallo-model met 75 procent van onze gegevens hebben getraind, kunnen we deze gebruiken tooscore Hallo overige 25 procent Hallo gegevens toosee hoe goed model werkt.</span><span class="sxs-lookup"><span data-stu-id="33d78-293">Now that we've trained hello model using 75 percent of our data, we can use it tooscore hello other 25 percent of hello data toosee how well our model functions.</span></span>

1. <span data-ttu-id="33d78-294">Zoek en sleep Hallo [Score Model] [ score-model] module toohello experimenteren canvas.</span><span class="sxs-lookup"><span data-stu-id="33d78-294">Find and drag hello [Score Model][score-model] module toohello experiment canvas.</span></span> <span data-ttu-id="33d78-295">Verbinding maken met uitvoer Hallo Hallo [Train Model] [ train-model] module toohello invoerpoort van links [Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="33d78-295">Connect hello output of hello [Train Model][train-model] module toohello left input port of [Score Model][score-model].</span></span> <span data-ttu-id="33d78-296">Verbinding maken met de Hallo test gegevensuitvoer (rechterpoort) van Hallo [Split Data] [ split] module toohello rechts invoer-poort van [Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="33d78-296">Connect hello test data output (right port) of hello [Split Data][split] module toohello right input port of [Score Model][score-model].</span></span>

    <span data-ttu-id="33d78-297">![Verbinding maken met de Hallo 'Score-Model' module tooboth Hallo 'Train-Model' en 'Split Data'-modules][connect-score-model]
    </span><span class="sxs-lookup"><span data-stu-id="33d78-297">![Connect hello "Score Model" module tooboth hello "Train Model" and "Split Data" modules][connect-score-model]
    </span></span><br/>
 <span data-ttu-id="33d78-298">***Verbinding maken met de Hallo 'Score-Model' module tooboth Hallo 'Train-Model' en 'Split Data'-modules***</span><span class="sxs-lookup"><span data-stu-id="33d78-298">***Connect hello "Score Model" module tooboth hello "Train Model" and "Split Data" modules***</span></span>

2. <span data-ttu-id="33d78-299">Hallo experiment uitvoeren en weergeven van Hallo-uitvoer van Hallo [Score Model] [ score-model] module (Klik op de uitvoerpoort Hallo van [Score Model] [ score-model] en selecteer **Visualiseren**).</span><span class="sxs-lookup"><span data-stu-id="33d78-299">Run hello experiment and view hello output from hello [Score Model][score-model] module (click hello output port of [Score Model][score-model] and select **Visualize**).</span></span> <span data-ttu-id="33d78-300">Hallo uitvoer geeft Hallo voorspelde waarden voor de prijs en bekende waarden uit de testgegevens Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="33d78-300">hello output shows hello predicted values for price and hello known values from hello test data.</span></span>  

    <span data-ttu-id="33d78-301">![Uitvoer van de module van de 'Score-Model' Hallo][score-model-output]
    </span><span class="sxs-lookup"><span data-stu-id="33d78-301">![Output of hello "Score Model" module][score-model-output]
    </span></span><br/>
 <span data-ttu-id="33d78-302">***Uitvoer van de module van de 'Score-Model' Hallo***</span><span class="sxs-lookup"><span data-stu-id="33d78-302">***Output of hello "Score Model" module***</span></span>

3. <span data-ttu-id="33d78-303">Ten slotte testen we Hallo kwaliteit van Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="33d78-303">Finally, we test hello quality of hello results.</span></span> <span data-ttu-id="33d78-304">Selecteer en sleep Hallo [Evaluate Model] [ evaluate-model] module toohello canvas experimenteren en uitvoer Hallo Hallo verbinding [Score Model] [ score-model] module toohello links van de invoer van [Evaluate Model][evaluate-model].</span><span class="sxs-lookup"><span data-stu-id="33d78-304">Select and drag hello [Evaluate Model][evaluate-model] module toohello experiment canvas, and connect hello output of hello [Score Model][score-model] module toohello left input of [Evaluate Model][evaluate-model].</span></span>

    > [!TIP]
    > <span data-ttu-id="33d78-305">Er zijn twee invoerpoorten op Hallo [Evaluate Model] [ evaluate-model] module omdat het gebruikte toocompare twee modellen naast elkaar kan zijn.</span><span class="sxs-lookup"><span data-stu-id="33d78-305">There are two input ports on hello [Evaluate Model][evaluate-model] module because it can be used toocompare two models side by side.</span></span> <span data-ttu-id="33d78-306">Later kunt u een ander algoritme toohello experiment toevoegen en gebruiken [Evaluate Model] [ evaluate-model] toosee waarvoor een betere resultaten oplevert.</span><span class="sxs-lookup"><span data-stu-id="33d78-306">Later, you can add another algorithm toohello experiment and use [Evaluate Model][evaluate-model] toosee which one gives better results.</span></span>

4. <span data-ttu-id="33d78-307">Hallo-experiment uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="33d78-307">Run hello experiment.</span></span>

<span data-ttu-id="33d78-308">tooview hello uitvoer van Hallo [Evaluate Model] [ evaluate-model] -module, klikt u op de uitvoerpoort Hallo en selecteer vervolgens **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="33d78-308">tooview hello output from hello [Evaluate Model][evaluate-model] module, click hello output port, and then select **Visualize**.</span></span>

<span data-ttu-id="33d78-309">![Evaluatieresultaten voor Hallo experiment][evaluation-results]
</span><span class="sxs-lookup"><span data-stu-id="33d78-309">![Evaluation results for hello experiment][evaluation-results]
</span></span><br/><span data-ttu-id="33d78-310">
***Evaluatieresultaten voor Hallo experiment***</span><span class="sxs-lookup"><span data-stu-id="33d78-310">
***Evaluation results for hello experiment***</span></span>

<span data-ttu-id="33d78-311">Hallo volgende statistieken worden weergegeven voor het model:</span><span class="sxs-lookup"><span data-stu-id="33d78-311">hello following statistics are shown for our model:</span></span>

- <span data-ttu-id="33d78-312">**Mean Absolute Error** (MAE): gemiddelde aan absolute fouten Hallo (een *fout* Hallo verschil is tussen Hallo voorspelde waarde en de werkelijke waarde Hallo).</span><span class="sxs-lookup"><span data-stu-id="33d78-312">**Mean Absolute Error** (MAE): hello average of absolute errors (an *error* is hello difference between hello predicted value and hello actual value).</span></span>
- <span data-ttu-id="33d78-313">**Root Mean Squared Error** (RMSE): Hallo vierkantswortel van Hallo gemiddelde aan gekwadrateerde fouten voor de voorspellingen op Hallo testgegevensset.</span><span class="sxs-lookup"><span data-stu-id="33d78-313">**Root Mean Squared Error** (RMSE): hello square root of hello average of squared errors of predictions made on hello test dataset.</span></span>
- <span data-ttu-id="33d78-314">**Relative Absolute Error**: Hallo gemiddelde aan absolute fouten relatieve toohello absolute verschil tussen de werkelijke waarden en Hallo gemiddelde van alle werkelijke waarden.</span><span class="sxs-lookup"><span data-stu-id="33d78-314">**Relative Absolute Error**: hello average of absolute errors relative toohello absolute difference between actual values and hello average of all actual values.</span></span>
- <span data-ttu-id="33d78-315">**Relative Squared Error**: Hallo gemiddelde aan gekwadrateerde fouten relatieve toohello kwadraat verschil tussen de werkelijke waarden Hallo en Hallo gemiddelde van alle werkelijke waarden.</span><span class="sxs-lookup"><span data-stu-id="33d78-315">**Relative Squared Error**: hello average of squared errors relative toohello squared difference between hello actual values and hello average of all actual values.</span></span>
- <span data-ttu-id="33d78-316">**Determinatiecoëfficiënt**: ook wel bekend als Hallo **r²-waarde**, dit is een statistische meetwaarde die aangeeft hoe goed een model Hallo gegevens past.</span><span class="sxs-lookup"><span data-stu-id="33d78-316">**Coefficient of Determination**: Also known as hello **R squared value**, this is a statistical metric indicating how well a model fits hello data.</span></span>

<span data-ttu-id="33d78-317">Voor elk van de fout Hallo is statistieken, kleinere beter.</span><span class="sxs-lookup"><span data-stu-id="33d78-317">For each of hello error statistics, smaller is better.</span></span> <span data-ttu-id="33d78-318">Een kleinere waarde geeft aan dat Hallo voorspellingen meer overeenkomt met de werkelijke waarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="33d78-318">A smaller value indicates that hello predictions more closely match hello actual values.</span></span> <span data-ttu-id="33d78-319">Voor **determinatiecoëfficiënt**, hello dichter bij de waarde ervan tooone (1.0) Hallo betere Hallo voorspellingen.</span><span class="sxs-lookup"><span data-stu-id="33d78-319">For **Coefficient of Determination**, hello closer its value is tooone (1.0), hello better hello predictions.</span></span>

## <a name="final-experiment"></a><span data-ttu-id="33d78-320">Laatste experiment</span><span class="sxs-lookup"><span data-stu-id="33d78-320">Final experiment</span></span>

<span data-ttu-id="33d78-321">Hallo laatste experiment ziet er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="33d78-321">hello final experiment should look something like this:</span></span>

<span data-ttu-id="33d78-322">![Hallo laatste experiment][complete-linear-regression-experiment]
</span><span class="sxs-lookup"><span data-stu-id="33d78-322">![hello final experiment][complete-linear-regression-experiment]
</span></span><br/><span data-ttu-id="33d78-323">
***Hallo laatste experiment***</span><span class="sxs-lookup"><span data-stu-id="33d78-323">
***hello final experiment***</span></span>

## <a name="next-steps"></a><span data-ttu-id="33d78-324">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="33d78-324">Next steps</span></span>

<span data-ttu-id="33d78-325">Nu dat u Hallo eerste machine learning-zelfstudie hebt voltooid en uw experiment instellen hebt, kunt u doorgaan tooimprove Hallo model en vervolgens implementeren als webservice voorspeld.</span><span class="sxs-lookup"><span data-stu-id="33d78-325">Now that you've completed hello first machine learning tutorial and have your experiment set up, you can continue tooimprove hello model and then deploy it as a predictive web service.</span></span>

- <span data-ttu-id="33d78-326">**Herhalen tootry tooimprove Hallo model** -u kunt bijvoorbeeld Hallo-functies die u uw voorspelling gebruikt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="33d78-326">**Iterate tootry tooimprove hello model** - For example, you can change hello features you use in your prediction.</span></span> <span data-ttu-id="33d78-327">Of u kunt de eigenschappen Hallo Hallo wijzigen [lineaire regressie] [ linear-regression] algoritme of probeer een ander algoritme kan worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="33d78-327">Or you can modify hello properties of hello [Linear Regression][linear-regression] algorithm or try a different algorithm altogether.</span></span> <span data-ttu-id="33d78-328">Kunt u zelfs meerdere machine learning-algoritmen tooyour experiment in één keer toevoegen en twee van deze te vergelijken met behulp van Hallo [Evaluate Model] [ evaluate-model] module.</span><span class="sxs-lookup"><span data-stu-id="33d78-328">You can even add multiple machine learning algorithms tooyour experiment at one time and compare two of them by using hello [Evaluate Model][evaluate-model] module.</span></span>
<span data-ttu-id="33d78-329">Voor een voorbeeld van hoe toocompare meerdere modellen in een enkel experiment zien [vergelijken Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) in Hallo [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="33d78-329">For an example of how toocompare multiple models in a single experiment, see [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span>

    > [!TIP]
    > <span data-ttu-id="33d78-330">toocopy elke herhaling van uw experiment, gebruik Hallo **SAVE AS** knop Hallo onder Hallo pagina aan.</span><span class="sxs-lookup"><span data-stu-id="33d78-330">toocopy any iteration of your experiment, use hello **SAVE AS** button at hello bottom of hello page.</span></span> <span data-ttu-id="33d78-331">U kunt alle Hallo herhalingen van uw experiment weergeven door te klikken op **weergave uitvoeren geschiedenis** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="33d78-331">You can see all hello iterations of your experiment by clicking **VIEW RUN HISTORY** at hello bottom of hello page.</span></span> <span data-ttu-id="33d78-332">Zie [Iteraties van experimenten beheren in Azure Machine Learning Studio][runhistory] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="33d78-332">For more details, see [Manage experiment iterations in Azure Machine Learning Studio][runhistory].</span></span>

[runhistory]: machine-learning-manage-experiment-iterations.md

- <span data-ttu-id="33d78-333">**Hallo model als een Voorspellend webservice implementeren** : wanneer u tevreden met het model bent, kunt u dit implementeren als een web service toobe toopredict prijzen van auto gebruikt met behulp van nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="33d78-333">**Deploy hello model as a predictive web service** - When you're satisfied with your model, you can deploy it as a web service toobe used toopredict automobile prices by using new data.</span></span> <span data-ttu-id="33d78-334">Zie [Een Azure Machine Learning-webservice implementeren][publish] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="33d78-334">For more details, see [Deploy an Azure Machine Learning web service][publish].</span></span>

[publish]: machine-learning-publish-a-machine-learning-web-service.md

<span data-ttu-id="33d78-335">Wilt u meer toolearn?</span><span class="sxs-lookup"><span data-stu-id="33d78-335">Want toolearn more?</span></span> <span data-ttu-id="33d78-336">Zie voor een uitgebreid en gedetailleerd overzicht van Hallo-proces voor het maken, training, scores en implementeren van een model [een voorspellende oplossing ontwikkelen met behulp van Azure Machine Learning][walkthrough].</span><span class="sxs-lookup"><span data-stu-id="33d78-336">For a more extensive and detailed walkthrough of hello process of creating, training, scoring, and deploying a model, see [Develop a predictive solution by using Azure Machine Learning][walkthrough].</span></span>

[walkthrough]: machine-learning-walkthrough-develop-predictive-solution.md

<!-- Images -->
[sign-in-to-studio]: ./media/machine-learning-create-experiment/sign-in-to-studio.png
[rename-experiment]: ./media/machine-learning-create-experiment/rename-experiment.png
[visualize-auto-data]:./media/machine-learning-create-experiment/visualize-auto-data.png
[select-visualize]: ./media/machine-learning-create-experiment/select-visualize.png
[showing-excluded-column]:./media/machine-learning-create-experiment/showing-excluded-column.png
[set-remove-entire-row]:./media/machine-learning-create-experiment/set-remove-entire-row.png
[early-experiment-run]:./media/machine-learning-create-experiment/early-experiment-run.png
[select-columns-to-include]:./media/machine-learning-create-experiment/select-columns-to-include.png
[second-experiment-run]:./media/machine-learning-create-experiment/second-experiment-run.png
[connect-score-model]:./media/machine-learning-create-experiment/connect-score-model.png
[evaluation-results]:./media/machine-learning-create-experiment/evaluation-results.png
[complete-linear-regression-experiment]:./media/machine-learning-create-experiment/complete-linear-regression-experiment.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[connect-train-model]:./media/machine-learning-create-experiment/connect-train-model.png
[select-price-column]:./media/machine-learning-create-experiment/select-price-column.png

[score-model-output]:./media/machine-learning-create-experiment/score-model-output.png

<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
