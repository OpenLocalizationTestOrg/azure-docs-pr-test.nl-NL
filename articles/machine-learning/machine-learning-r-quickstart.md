---
title: Quick Start-zelfstudie voor R-taal voor Machine Learning | Microsoft Docs
description: Gebruik deze R programming zelfstudie aan de slag snel met de taal R Azure Machine Learning Studio om een prognosemodel oplossing te maken.
keywords: Quick Start, r-taal, de programmeertaal r, programming r-zelfstudie
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 99a3a0fd-b359-481a-b236-66868deccd96
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 598f5ce445e520b6cdc347c80f7f3dcbc9c2c9e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="quickstart-tutorial-for-the-r-programming-language-for-azure-machine-learning"></a><span data-ttu-id="0e77a-104">Beknopte zelfstudie voor programmeertaal R voor Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0e77a-104">Quickstart tutorial for the R programming language for Azure Machine Learning</span></span>

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a><span data-ttu-id="0e77a-105">Inleiding</span><span class="sxs-lookup"><span data-stu-id="0e77a-105">Introduction</span></span>
<span data-ttu-id="0e77a-106">Deze zelfstudie snel aan de slag kunt u snel starten Azure Machine Learning met behulp van de programmeertaal R uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="0e77a-106">This quickstart tutorial helps you quickly start extending Azure Machine Learning by using the R programming language.</span></span> <span data-ttu-id="0e77a-107">Volg deze programming R-zelfstudie voor het maken, testen en R-code in Azure Machine Learning uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0e77a-107">Follow this R programming tutorial to create, test and execute R code within Azure Machine Learning.</span></span> <span data-ttu-id="0e77a-108">Als u de zelfstudie doorloopt, maakt u een volledige prognoses oplossing met behulp van de R-taal in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0e77a-108">As you work through tutorial, you will create a complete forecasting solution by using the R language in Azure Machine Learning.</span></span>  

<span data-ttu-id="0e77a-109">Microsoft Azure Machine Learning bevat veel krachtige machine learning en manipulatie modules.</span><span class="sxs-lookup"><span data-stu-id="0e77a-109">Microsoft Azure Machine Learning contains many powerful machine learning and data manipulation modules.</span></span> <span data-ttu-id="0e77a-110">De krachtige R taal heeft als lingua franca van analytics zijn beschreven.</span><span class="sxs-lookup"><span data-stu-id="0e77a-110">The powerful R language has been described as the lingua franca of analytics.</span></span> <span data-ttu-id="0e77a-111">Manipulatie analytics en gegevens in Azure Machine Learning kan worden uitgebreid met R. Deze combinatie biedt de schaalbaarheid en het gemak van implementatie van Azure Machine Learning met de flexibiliteit en grondige analyse van R.</span><span class="sxs-lookup"><span data-stu-id="0e77a-111">Happily, analytics and data manipulation in Azure Machine Learning can be extended by using R. This combination provides the scalability and ease of deployment of Azure Machine Learning with the flexibility and deep analytics of R.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-the-dataset"></a><span data-ttu-id="0e77a-112">Prognose en de gegevensset</span><span class="sxs-lookup"><span data-stu-id="0e77a-112">Forecasting and the dataset</span></span>
<span data-ttu-id="0e77a-113">Prognose is veel werknemers en wel handig analytische methode.</span><span class="sxs-lookup"><span data-stu-id="0e77a-113">Forecasting is a widely employed and quite useful analytical method.</span></span> <span data-ttu-id="0e77a-114">Algemeen gebruik bereik van het voorspellen van de verkoop van seizoensgebonden items, optimaal voorraadbeheer te voorspellen macro-economische variabelen te bepalen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-114">Common uses range from predicting sales of seasonal items, determining optimal inventory levels, to predicting macroeconomic variables.</span></span> <span data-ttu-id="0e77a-115">Prognose gewoonlijk wordt uitgevoerd met time series-modellen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-115">Forecasting is typically done with time series models.</span></span>

<span data-ttu-id="0e77a-116">Reeks tijdgegevens zijn gegevens waarin de waarden een tijdsindex hebben.</span><span class="sxs-lookup"><span data-stu-id="0e77a-116">Time series data is data in which the values have a time index.</span></span> <span data-ttu-id="0e77a-117">De tijdsindex worden regelmatig, bijvoorbeeld elke maand of elke minuut of onregelmatig.</span><span class="sxs-lookup"><span data-stu-id="0e77a-117">The time index can be regular, e.g. every month or every minute, or irregular.</span></span> <span data-ttu-id="0e77a-118">Een tijdreeksmodel is gebaseerd op een reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="0e77a-118">A time series model is based on time series data.</span></span> <span data-ttu-id="0e77a-119">Het R programmeertaal bevat een flexibele framework en de uitgebreide analytics voor tijd reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="0e77a-119">The R programming language contains a flexible framework and extensive analytics for time series data.</span></span>

<span data-ttu-id="0e77a-120">In deze snelstartgids wordt worden werken met Californië zuivelproductie en prijzen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="0e77a-120">In this quickstart guide we will be working with California dairy production and pricing data.</span></span> <span data-ttu-id="0e77a-121">Deze gegevens omvatten maandelijkse informatie op de productie van verschillende producten en de prijs van melkvet, een benchmark basisproduct.</span><span class="sxs-lookup"><span data-stu-id="0e77a-121">This data includes monthly information on the production of several dairy products and the price of milk fat, a benchmark commodity.</span></span>

<span data-ttu-id="0e77a-122">De gegevens die worden gebruikt in dit artikel, samen met het R-scripts kunnen worden [hier gedownload][download].</span><span class="sxs-lookup"><span data-stu-id="0e77a-122">The data used in this article, along with R scripts, can be [downloaded here][download].</span></span> <span data-ttu-id="0e77a-123">Deze gegevens is oorspronkelijk gemaakt van gegevens op de universiteit Wisconsin op http://future.aae.wisc.edu/tab/production.html.</span><span class="sxs-lookup"><span data-stu-id="0e77a-123">This data was originally synthesized from information available from the University of Wisconsin at http://future.aae.wisc.edu/tab/production.html.</span></span>

### <a name="organization"></a><span data-ttu-id="0e77a-124">Organisatie</span><span class="sxs-lookup"><span data-stu-id="0e77a-124">Organization</span></span>
<span data-ttu-id="0e77a-125">We zullen verschillende stappen doorlopen als u meer informatie over het maken, testen en uitvoeren van analyses en gegevens manipulatie R-code in de Azure Machine Learning-omgeving.</span><span class="sxs-lookup"><span data-stu-id="0e77a-125">We will progress through several steps as you learn how to create, test and execute analytics and data manipulation R code in the Azure Machine Learning environment.</span></span>  

* <span data-ttu-id="0e77a-126">Eerst verkennen we de basisbeginselen van het gebruik van de R-taal in de Azure Machine Learning Studio-omgeving.</span><span class="sxs-lookup"><span data-stu-id="0e77a-126">First we will explore the basics of using the R language in the Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="0e77a-127">Vervolgens wordt de voortgang bespreking van de verschillende aspecten van i/o voor gegevens, R-code en afbeeldingen in de Azure Machine Learning-omgeving.</span><span class="sxs-lookup"><span data-stu-id="0e77a-127">Then we progress to discussing various aspects of I/O for data, R code and graphics in the Azure Machine Learning environment.</span></span>
* <span data-ttu-id="0e77a-128">We wordt vervolgens het eerste deel van onze prognoses oplossing maken door het maken van code voor het reinigen van gegevens en transformatie.</span><span class="sxs-lookup"><span data-stu-id="0e77a-128">We will then construct the first part of our forecasting solution by creating code for data cleaning and transformation.</span></span>
* <span data-ttu-id="0e77a-129">Met onze gegevens voorbereid wordt uitgevoerd, er een analyse van de correlatie tussen verschillende van de variabelen in onze gegevensset.</span><span class="sxs-lookup"><span data-stu-id="0e77a-129">With our data prepared we will perform an analysis of the correlations between several of the variables in our dataset.</span></span>
* <span data-ttu-id="0e77a-130">We gaan ten slotte een seizoen prognoses tijdreeksmodel voor maken.</span><span class="sxs-lookup"><span data-stu-id="0e77a-130">Finally, we will create a seasonal time series forecasting model for milk production.</span></span>

## <span data-ttu-id="0e77a-131"><a id="mlstudio"></a>Interactie met R-taal in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="0e77a-131"><a id="mlstudio"></a>Interact with R language in Machine Learning Studio</span></span>
<span data-ttu-id="0e77a-132">Deze sectie leert u enkele van de basisprincipes van de interactie met de programmeertaal R in de omgeving Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="0e77a-132">This section takes you through some basics of interacting with the R programming language in the Machine Learning Studio environment.</span></span> <span data-ttu-id="0e77a-133">De taal R biedt een krachtig hulpprogramma om aangepaste analytics en data manipulatie modules in de Azure Machine Learning-omgeving te maken.</span><span class="sxs-lookup"><span data-stu-id="0e77a-133">The R language provides a powerful tool to create customized analytics and data manipulation modules within the Azure Machine Learning environment.</span></span>

<span data-ttu-id="0e77a-134">Ik gebruik RStudio ontwikkelen, testen en foutopsporing van R-code op kleine schaal.</span><span class="sxs-lookup"><span data-stu-id="0e77a-134">I will use RStudio to develop, test and debug R code on a small scale.</span></span> <span data-ttu-id="0e77a-135">Deze code wordt vervolgens knippen en plakken in een [R-Script uitvoeren] [ execute-r-script] module in Machine Learning Studio om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="0e77a-135">This code is then cut and paste into an [Execute R Script][execute-r-script] module in Machine Learning Studio ready to run.</span></span>  

### <a name="the-execute-r-script-module"></a><span data-ttu-id="0e77a-136">De module R-Script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="0e77a-136">The Execute R Script module</span></span>
<span data-ttu-id="0e77a-137">In Machine Learning Studio R scripts worden uitgevoerd binnen de [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="0e77a-137">Within Machine Learning Studio, R scripts are run within the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="0e77a-138">Een voorbeeld van de [R-Script uitvoeren] [ execute-r-script] module in Machine Learning Studio wordt weergegeven in afbeelding 1.</span><span class="sxs-lookup"><span data-stu-id="0e77a-138">An example of the [Execute R Script][execute-r-script] module in Machine Learning Studio is shown in Figure 1.</span></span>

 ![R programmeertaal: R voor het uitvoeren van Script-module is geselecteerd in Machine Learning Studio][1]

<span data-ttu-id="0e77a-140">*Afbeelding 1. De Machine Learning Studio-omgeving met de module R-Script uitvoeren is geselecteerd.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-140">*Figure 1. The Machine Learning Studio environment showing the Execute R Script module selected.*</span></span>

<span data-ttu-id="0e77a-141">Verwijzen naar afbeelding 1, bekijken we enkele van de belangrijkste onderdelen van de Machine Learning Studio-omgeving voor het werken met de [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="0e77a-141">Referring to Figure 1, let's look at some of the key parts of the Machine Learning Studio environment for working with the [Execute R Script][execute-r-script] module.</span></span>

* <span data-ttu-id="0e77a-142">De modules in het experiment worden in het middelste deelvenster weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0e77a-142">The modules in the experiment are shown in the center pane.</span></span>
* <span data-ttu-id="0e77a-143">Het bovenste gedeelte van het rechter deelvenster bevat een venster voor het weergeven en bewerken van uw R-scripts.</span><span class="sxs-lookup"><span data-stu-id="0e77a-143">The upper part of the right pane contains a window to view and edit your R scripts.</span></span>  
* <span data-ttu-id="0e77a-144">Het onderste gedeelte van het rechter deelvenster ziet u enkele eigenschappen van de [R-Script uitvoeren][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="0e77a-144">The lower part of right pane shows some properties of the [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="0e77a-145">U kunt de logboeken van de fout en uitvoer weergeven door te klikken op de juiste plaatsen van dit deelvenster.</span><span class="sxs-lookup"><span data-stu-id="0e77a-145">You can view the error and output logs by clicking on the appropriate spots of this pane.</span></span>

<span data-ttu-id="0e77a-146">We zullen natuurlijk bespreken de [R-Script uitvoeren] [ execute-r-script] in meer detail in de rest van dit document.</span><span class="sxs-lookup"><span data-stu-id="0e77a-146">We will, of course, be discussing the [Execute R Script][execute-r-script] in greater detail in the rest of this document.</span></span>

<span data-ttu-id="0e77a-147">Als u werkt met complexe R-functies, ik raden aan dat u bewerkt, testen en fouten in RStudio opsporen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-147">When working with complex R functions, I recommend that you edit, test and debug in RStudio.</span></span> <span data-ttu-id="0e77a-148">Net als bij de ontwikkeling van alle software uw code stapsgewijs uitbreiden en het testen op kleine simpele testcases.</span><span class="sxs-lookup"><span data-stu-id="0e77a-148">As with any software development, extend your code incrementally and test it on small simple test cases.</span></span> <span data-ttu-id="0e77a-149">Vervolgens knippen en plakken van uw functies in het venster R-script van de [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="0e77a-149">Then cut and paste your functions into the R script window of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="0e77a-150">Deze aanpak kunt u zowel de RStudio integrated development environment (IDE) en de kracht van Azure Machine Learning benutten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-150">This approach allows you to harness both the RStudio integrated development environment (IDE) and the power of Azure Machine Learning.</span></span>  

#### <a name="execute-r-code"></a><span data-ttu-id="0e77a-151">R code uitvoeren</span><span class="sxs-lookup"><span data-stu-id="0e77a-151">Execute R code</span></span>
<span data-ttu-id="0e77a-152">Geen R-code in de [R-Script uitvoeren] [ execute-r-script] module wordt uitgevoerd wanneer u het experiment uitvoeren door te klikken op de **uitvoeren** knop.</span><span class="sxs-lookup"><span data-stu-id="0e77a-152">Any R code in the [Execute R Script][execute-r-script] module will execute when you run the experiment by clicking on the **Run** button.</span></span> <span data-ttu-id="0e77a-153">Wanneer de uitvoering is voltooid, een vinkje worden weergegeven op de [R-Script uitvoeren] [ execute-r-script] pictogram.</span><span class="sxs-lookup"><span data-stu-id="0e77a-153">When execution has completed, a check mark will appear on the [Execute R Script][execute-r-script] icon.</span></span>

#### <a name="defensive-r-coding-for-azure-machine-learning"></a><span data-ttu-id="0e77a-154">Defensive R coderen voor Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0e77a-154">Defensive R coding for Azure Machine Learning</span></span>
<span data-ttu-id="0e77a-155">Als u R-code voor, bijvoorbeeld een web-service ontwikkelt met behulp van Azure Machine Learning, moet u zeker plannen hoe uw code wordt omgaan met een onverwachte gegevensinvoer en uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-155">If you are developing R code for, say, a web service by using Azure Machine Learning, you should definitely plan how your code will deal with an unexpected data input and exceptions.</span></span> <span data-ttu-id="0e77a-156">Als u wilt behouden duidelijkheid, ik niet opgenomen veel heeft op het gebied met het controleren of de afhandeling van uitzonderingen in de meeste van de codevoorbeelden die wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0e77a-156">To maintain clarity, I have not included much in the way of checking or exception handling in most of the code examples shown.</span></span> <span data-ttu-id="0e77a-157">Echter, als we gaan ik krijgt u enkele voorbeelden van functies met behulp van de mogelijkheid voor het verwerken van het R-uitzondering.</span><span class="sxs-lookup"><span data-stu-id="0e77a-157">However, as we proceed I will give you several examples of functions by using R's exception handling capability.</span></span>  

<span data-ttu-id="0e77a-158">Als u een uitgebreidere behandeling van R uitzonderingsverwerking moet, ik lezen van de betreffende gedeelten van het rapport door Wickham die worden vermeld in het beste [bijlage B - verdere lezen](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="0e77a-158">If you need a more complete treatment of R exception handling, I recommend you read the applicable sections of the book by Wickham listed in [Appendix B - Further Reading](#appendixb).</span></span>

#### <a name="debug-and-test-r-in-machine-learning-studio"></a><span data-ttu-id="0e77a-159">Debuggen en testen van R in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="0e77a-159">Debug and test R in Machine Learning Studio</span></span>
<span data-ttu-id="0e77a-160">Als u wilt vast, aanbevelen ik u testen en foutopsporing van uw R-code op kleine schaal in RStudio.</span><span class="sxs-lookup"><span data-stu-id="0e77a-160">To reiterate, I recommend you test and debug your R code on a small scale in RStudio.</span></span> <span data-ttu-id="0e77a-161">Er zijn echter gevallen waarbij u moet voor het opsporen van R code in de [R-Script uitvoeren] [ execute-r-script] zelf.</span><span class="sxs-lookup"><span data-stu-id="0e77a-161">However, there are cases where you will need to track down R code problems in the [Execute R Script][execute-r-script] itself.</span></span> <span data-ttu-id="0e77a-162">Daarnaast is het raadzaam om te controleren van de resultaten in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="0e77a-162">In addition, it is good practice to check your results in Machine Learning Studio.</span></span>

<span data-ttu-id="0e77a-163">De uitvoer van de uitvoering van uw R-code en op het Azure Machine Learning-platform is voornamelijk in uitvoer.log gevonden.</span><span class="sxs-lookup"><span data-stu-id="0e77a-163">Output from the execution of your R code and on the Azure Machine Learning platform is found primarily in output.log.</span></span> <span data-ttu-id="0e77a-164">Aanvullende informatie wordt weergegeven in error.log.</span><span class="sxs-lookup"><span data-stu-id="0e77a-164">Some additional information will be seen in error.log.</span></span>  

<span data-ttu-id="0e77a-165">Als een fout in Machine Learning Studio optreedt tijdens het uitvoeren van uw code R, moet uw eerste training van actie om te kijken naar error.log.</span><span class="sxs-lookup"><span data-stu-id="0e77a-165">If an error occurs in Machine Learning Studio while running your R code, your first course of action should be to look at error.log.</span></span> <span data-ttu-id="0e77a-166">Dit bestand kunt nuttige foutberichten om te begrijpen en corrigeer de fout bevatten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-166">This file can contain useful error messages to help you understand and correct your error.</span></span> <span data-ttu-id="0e77a-167">Als u wilt error.log weergeven, klikt u op **foutenlogboek weergeven** op de **eigenschappendeelvenster** voor de [R-Script uitvoeren] [ execute-r-script] met de fout.</span><span class="sxs-lookup"><span data-stu-id="0e77a-167">To view error.log, click on **View error log** on the **properties pane** for the [Execute R Script][execute-r-script] containing the error.</span></span>

<span data-ttu-id="0e77a-168">Bijvoorbeeld ik de volgende R-code wordt uitgevoerd met een niet-gedefinieerde variabele y in een [R-Script uitvoeren] [ execute-r-script] module:</span><span class="sxs-lookup"><span data-stu-id="0e77a-168">For example, I ran the following R code, with an undefined variable y, in an [Execute R Script][execute-r-script] module:</span></span>

    x <- 1.0
    z <- x + y

<span data-ttu-id="0e77a-169">Deze code kan niet worden uitgevoerd, wat resulteert in een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="0e77a-169">This code fails to execute, resulting in an error condition.</span></span> <span data-ttu-id="0e77a-170">Te klikken op **foutenlogboek weergeven** op de **eigenschappendeelvenster** resulteert in de weergave wordt weergegeven in afbeelding 2.</span><span class="sxs-lookup"><span data-stu-id="0e77a-170">Clicking on **View error log** on the **properties pane** produces the display shown in Figure 2.</span></span>

  ![Foutbericht pop up][2]

<span data-ttu-id="0e77a-172">*Afbeelding 2. Foutbericht pop-upvenster.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-172">*Figure 2. Error message pop-up.*</span></span>

<span data-ttu-id="0e77a-173">Het lijkt erop dat we moet zoeken in uitvoer.log om de R-foutbericht te zien.</span><span class="sxs-lookup"><span data-stu-id="0e77a-173">It looks like we need to look in output.log to see the R error message.</span></span> <span data-ttu-id="0e77a-174">Klik op de [R-Script uitvoeren] [ execute-r-script] en klik vervolgens op de **uitvoer.log weergeven** item op de **eigenschappendeelvenster** naar rechts.</span><span class="sxs-lookup"><span data-stu-id="0e77a-174">Click on the [Execute R Script][execute-r-script] and then click on the **View output.log** item on the **properties pane** to the right.</span></span> <span data-ttu-id="0e77a-175">Een nieuw browservenster wordt geopend en ik Zie de volgende.</span><span class="sxs-lookup"><span data-stu-id="0e77a-175">A new browser window opens, and I see the following.</span></span>

    [Critical]     Error: Error 0063: The following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

<span data-ttu-id="0e77a-176">Dit foutbericht bevat geen verrassingen en duidelijk identificeert het probleem.</span><span class="sxs-lookup"><span data-stu-id="0e77a-176">This error message contains no surprises and clearly identifies the problem.</span></span>

<span data-ttu-id="0e77a-177">Om te controleren van de waarde van een object in R, kunt u deze waarden naar het bestand uitvoer.log afdrukken.</span><span class="sxs-lookup"><span data-stu-id="0e77a-177">To inspect the value of any object in R, you can print these values to the output.log file.</span></span> <span data-ttu-id="0e77a-178">De regels voor het onderzoeken van objectwaarden zijn in wezen hetzelfde als in een interactieve R-sessie.</span><span class="sxs-lookup"><span data-stu-id="0e77a-178">The rules for examining object values are essentially the same as in an interactive R session.</span></span> <span data-ttu-id="0e77a-179">Als u de naam van een variabele op een regel typt, wordt bijvoorbeeld de waarde van het object afgedrukt naar het bestand uitvoer.log.</span><span class="sxs-lookup"><span data-stu-id="0e77a-179">For example, if you type a variable name on a line, the value of the object will be printed to the output.log file.</span></span>  

#### <a name="packages-in-machine-learning-studio"></a><span data-ttu-id="0e77a-180">Pakketten in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="0e77a-180">Packages in Machine Learning Studio</span></span>
<span data-ttu-id="0e77a-181">Azure Machine Learning wordt geleverd met meer dan 350 vooraf geïnstalleerde R-taalpakketten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-181">Azure Machine Learning comes with over 350 preinstalled R language packages.</span></span> <span data-ttu-id="0e77a-182">U kunt de volgende code in de [R-Script uitvoeren] [ execute-r-script] module voor het ophalen van een lijst van de vooraf geïnstalleerde pakketten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-182">You can use the following code in the [Execute R Script][execute-r-script] module to retrieve a list of the preinstalled packages.</span></span>

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

<span data-ttu-id="0e77a-183">Als u niet de laatste regel van deze code op het moment dat begrijpt, kunt u lezen op.</span><span class="sxs-lookup"><span data-stu-id="0e77a-183">If you don't understand the last line of this code at the moment, read on.</span></span> <span data-ttu-id="0e77a-184">In de rest van dit document wordt uitvoerig besproken R gebruiken in de Azure Machine Learning-omgeving.</span><span class="sxs-lookup"><span data-stu-id="0e77a-184">In the rest of this document we will extensively discuss using R in the Azure Machine Learning environment.</span></span>

### <a name="introduction-to-rstudio"></a><span data-ttu-id="0e77a-185">Inleiding tot RStudio</span><span class="sxs-lookup"><span data-stu-id="0e77a-185">Introduction to RStudio</span></span>
<span data-ttu-id="0e77a-186">RStudio is een veelgebruikte IDE voor R. Ik gebruik RStudio bewerken, testen en foutopsporing enkele van de R-code die wordt gebruikt in deze snelstartgids.</span><span class="sxs-lookup"><span data-stu-id="0e77a-186">RStudio is a widely used IDE for R. I will use RStudio for editing, testing and debugging some of the R code used in this quick start guide.</span></span> <span data-ttu-id="0e77a-187">Zodra de R-code is getest en klaar zijn, u gewoon knippen en plakken in de editor RStudio naar een Machine Learning Studio [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="0e77a-187">Once R code is tested and ready, you simply cut and paste from the RStudio editor into a Machine Learning Studio [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="0e77a-188">Als u niet de R-programmeertaal op uw computer geïnstalleerd hebt, ik het beste dat u doet u dat nu.</span><span class="sxs-lookup"><span data-stu-id="0e77a-188">If you do not have the R programming language installed on your desktop machine, I recommend you do so now.</span></span> <span data-ttu-id="0e77a-189">Gratis downloads van open-source R taal zijn beschikbaar op de uitgebreide R archief netwerk (CRAN) op [http://www.r-project.org/](http://www.r-project.org/).</span><span class="sxs-lookup"><span data-stu-id="0e77a-189">Free downloads of open source R language are available at the Comprehensive R Archive Network (CRAN) at [http://www.r-project.org/](http://www.r-project.org/).</span></span> <span data-ttu-id="0e77a-190">Er zijn downloads beschikbaar voor Windows, Mac OS- en Linux/UNIX.</span><span class="sxs-lookup"><span data-stu-id="0e77a-190">There are downloads available for Windows, Mac OS, and Linux/UNIX.</span></span> <span data-ttu-id="0e77a-191">Kies een mirror in de buurt en volg de aanwijzingen downloaden.</span><span class="sxs-lookup"><span data-stu-id="0e77a-191">Choose a nearby mirror and follow the download directions.</span></span> <span data-ttu-id="0e77a-192">CRAN bevat bovendien een schat aan nuttig analytics en data manipulatie pakketten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-192">In addition, CRAN contains a wealth of useful analytics and data manipulation packages.</span></span>

<span data-ttu-id="0e77a-193">Als u niet bekend met RStudio bent, moet u downloadt en installeert de bureaubladversie.</span><span class="sxs-lookup"><span data-stu-id="0e77a-193">If you are new to RStudio, you should download and install the desktop version.</span></span> <span data-ttu-id="0e77a-194">U vindt dat de RStudio downloads voor Windows-, Mac OS- en Linux/UNIX op http://www.rstudio.com/products/RStudio/.</span><span class="sxs-lookup"><span data-stu-id="0e77a-194">You can find the RStudio downloads for Windows, Mac OS, and Linux/UNIX at http://www.rstudio.com/products/RStudio/.</span></span> <span data-ttu-id="0e77a-195">Volg de aanwijzingen voor het installeren van RStudio op uw computer.</span><span class="sxs-lookup"><span data-stu-id="0e77a-195">Follow the directions provided to install RStudio on your desktop machine.</span></span>  

<span data-ttu-id="0e77a-196">Een zelfstudie Inleiding tot RStudio is beschikbaar op https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span><span class="sxs-lookup"><span data-stu-id="0e77a-196">A tutorial introduction to RStudio is available at https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span></span>

<span data-ttu-id="0e77a-197">Ik aanvullende informatie geven over het gebruik van RStudio in [bijlage A][appendixa].</span><span class="sxs-lookup"><span data-stu-id="0e77a-197">I provide some additional information on using RStudio in [Appendix A][appendixa].</span></span>  

## <span data-ttu-id="0e77a-198"><a id="scriptmodule"></a>Ophalen van gegevens in en uit de module R-Script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="0e77a-198"><a id="scriptmodule"></a>Get data in and out of the Execute R Script module</span></span>
<span data-ttu-id="0e77a-199">In deze sectie bespreken we hoe u gegevens ophalen naar en van de [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="0e77a-199">In this section we will discuss how you get data into and out of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="0e77a-200">Bespreken we hoe u voor het afhandelen van verschillende soorten gegevens gelezen in en buiten de [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="0e77a-200">We will review how to handle various data types read into and out of the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="0e77a-201">De volledige code voor deze sectie wordt het zip-bestand dat u eerder hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="0e77a-201">The complete code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="load-and-check-data-in-machine-learning-studio"></a><span data-ttu-id="0e77a-202">Laden en controleren van de gegevens in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="0e77a-202">Load and check data in Machine Learning Studio</span></span>
#### <span data-ttu-id="0e77a-203"><a id="loading"></a>Laden van de gegevensset</span><span class="sxs-lookup"><span data-stu-id="0e77a-203"><a id="loading"></a>Load the dataset</span></span>
<span data-ttu-id="0e77a-204">Er wordt gestart door bij het laden van de **csdairydata.csv** -bestand in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="0e77a-204">We will start by loading the **csdairydata.csv** file into Azure Machine Learning Studio.</span></span>

* <span data-ttu-id="0e77a-205">Start uw Azure Machine Learning Studio-omgeving.</span><span class="sxs-lookup"><span data-stu-id="0e77a-205">Start your Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="0e77a-206">Klik op **+ nieuw** in de linkerbenedenhoek van het scherm en selecteer **gegevensset**.</span><span class="sxs-lookup"><span data-stu-id="0e77a-206">Click on **+ NEW** at the lower left of your screen and select **Dataset**.</span></span>
* <span data-ttu-id="0e77a-207">Selecteer **uit lokale bestand**, en vervolgens **Bladeren** om het bestand te selecteren.</span><span class="sxs-lookup"><span data-stu-id="0e77a-207">Select **From Local File**, and then **Browse** to select the file.</span></span>
* <span data-ttu-id="0e77a-208">Zorg ervoor dat u hebt geselecteerd **generieke CSV-bestand met de header (.csv)** als het type voor de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="0e77a-208">Make sure you have selected **Generic CSV file with header (.csv)** as the type for the dataset.</span></span>
* <span data-ttu-id="0e77a-209">Klik op het vinkje.</span><span class="sxs-lookup"><span data-stu-id="0e77a-209">Click the check mark.</span></span>
* <span data-ttu-id="0e77a-210">Nadat de gegevensset zijn geüpload, ziet u de nieuwe gegevensset door te klikken op de **gegevenssets** tabblad.</span><span class="sxs-lookup"><span data-stu-id="0e77a-210">After the dataset has been uploaded, you should see the new dataset by clicking on the **Datasets** tab.</span></span>  

#### <a name="create-an-experiment"></a><span data-ttu-id="0e77a-211">Een experiment maken</span><span class="sxs-lookup"><span data-stu-id="0e77a-211">Create an experiment</span></span>
<span data-ttu-id="0e77a-212">Nu we hebben enkele gegevens in Machine Learning Studio, moet we maken van een experiment voor de analyse wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0e77a-212">Now that we have some data in Machine Learning Studio, we need to create an experiment to do the analysis.</span></span>  

* <span data-ttu-id="0e77a-213">Klik op **+ nieuw** op de lagere links en selecteer **Experiment**, klikt u vervolgens **leeg Experiment**.</span><span class="sxs-lookup"><span data-stu-id="0e77a-213">Click on **+ NEW** at the lower left and select **Experiment**, then **Blank Experiment**.</span></span>
* <span data-ttu-id="0e77a-214">U kunt uw experiment naam door te selecteren en te wijzigen, de **Experiment op wordt gemaakt...**  titel boven aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="0e77a-214">You can name your experiment by selecting, and modifying, the **Experiment created on ...** title at the top of the page.</span></span> <span data-ttu-id="0e77a-215">Bijvoorbeeld wijzigen naar **CA Zuivel Analysis**.</span><span class="sxs-lookup"><span data-stu-id="0e77a-215">For example, changing it to **CA Dairy Analysis**.</span></span>
* <span data-ttu-id="0e77a-216">Vouw op de linkerkant van de pagina experiment **gegevenssets opgeslagen**, en vervolgens **mijn gegevenssets**.</span><span class="sxs-lookup"><span data-stu-id="0e77a-216">On the left of the experiment page, expand **Saved Datasets**, and then **My Datasets**.</span></span> <span data-ttu-id="0e77a-217">U ziet de **cadairydata.csv** die u eerder hebt geüpload.</span><span class="sxs-lookup"><span data-stu-id="0e77a-217">You should see the **cadairydata.csv** that you uploaded earlier.</span></span>
* <span data-ttu-id="0e77a-218">Slepen en neerzetten de **csdairydata.csv gegevensset** naar het experiment.</span><span class="sxs-lookup"><span data-stu-id="0e77a-218">Drag and drop the **csdairydata.csv dataset** onto the experiment.</span></span>
* <span data-ttu-id="0e77a-219">In de **zoeken items experimenteren** vak boven aan het linkerdeelvenster type [R-Script uitvoeren][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="0e77a-219">In the **Search experiment items** box on the top of the left pane, type [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="0e77a-220">Hier ziet u de module worden weergegeven in de zoeklijst.</span><span class="sxs-lookup"><span data-stu-id="0e77a-220">You will see the module appear in the search list.</span></span>
* <span data-ttu-id="0e77a-221">Slepen en neerzetten de [R-Script uitvoeren] [ execute-r-script] module naar uw palet.</span><span class="sxs-lookup"><span data-stu-id="0e77a-221">Drag and drop the [Execute R Script][execute-r-script] module onto your pallet.</span></span>  
* <span data-ttu-id="0e77a-222">Verbinding maken met de uitvoer van de **csdairydata.csv gegevensset** naar de meest linkse invoer (**Dataset1**) van de [R-Script uitvoeren][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="0e77a-222">Connect the output of the **csdairydata.csv dataset** to the leftmost input (**Dataset1**) of the [Execute R Script][execute-r-script].</span></span>
* <span data-ttu-id="0e77a-223">**Vergeet niet op 'Opslaan' te klikken.**</span><span class="sxs-lookup"><span data-stu-id="0e77a-223">**Don't forget to click on 'Save'!**</span></span>  

<span data-ttu-id="0e77a-224">Op dit moment ziet uw experiment er ongeveer als afbeelding 3.</span><span class="sxs-lookup"><span data-stu-id="0e77a-224">At this point your experiment should look something like Figure 3.</span></span>

![De CA Zuivel analyse experimenteren met de gegevensset en module R-Script uitvoeren][3]

<span data-ttu-id="0e77a-226">*Afbeelding 3. De CA Zuivel analyse experimenteren met gegevensset en module R-Script niet uitvoeren.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-226">*Figure 3. The CA Dairy Analysis experiment with dataset and Execute R Script module.*</span></span>

#### <a name="check-on-the-data"></a><span data-ttu-id="0e77a-227">Controleer op de gegevens</span><span class="sxs-lookup"><span data-stu-id="0e77a-227">Check on the data</span></span>
<span data-ttu-id="0e77a-228">We hebben een overzicht van de gegevens die we in ons experiment hebben geladen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-228">Let's have a look at the data we have loaded into our experiment.</span></span> <span data-ttu-id="0e77a-229">Klik in het experiment op in de uitvoer van de **cadairydata.csv gegevensset** en selecteer **visualiseren**.</span><span class="sxs-lookup"><span data-stu-id="0e77a-229">In the experiment, click on the output of the **cadairydata.csv dataset** and select **visualize**.</span></span> <span data-ttu-id="0e77a-230">U ziet er ongeveer zo afbeelding 4.</span><span class="sxs-lookup"><span data-stu-id="0e77a-230">You should see something like Figure 4.</span></span>  

![Samenvatting van de gegevensset cadairydata.csv][4]

<span data-ttu-id="0e77a-232">*Afbeelding 4. Samenvatting van de gegevensset cadairydata.csv.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-232">*Figure 4. Summary of the cadairydata.csv dataset.*</span></span>

<span data-ttu-id="0e77a-233">In deze weergave ziet u een groot aantal nuttige informatie.</span><span class="sxs-lookup"><span data-stu-id="0e77a-233">In this view we see a lot of useful information.</span></span> <span data-ttu-id="0e77a-234">U ziet de eerste verschillende rijen van deze dataset.</span><span class="sxs-lookup"><span data-stu-id="0e77a-234">We can see the first several rows of that dataset.</span></span> <span data-ttu-id="0e77a-235">Als we een kolom selecteert, ziet u de sectie statistieken meer informatie over de kolom.</span><span class="sxs-lookup"><span data-stu-id="0e77a-235">If we select a column, the Statistics section shows more information about the column.</span></span> <span data-ttu-id="0e77a-236">Bijvoorbeeld, staan de rij onderdeeltype ons welke gegevenstypen Azure Machine Learning Studio aan de kolom toegewezen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-236">For example, the Feature Type row shows us what data types Azure Machine Learning Studio assigned to the column.</span></span> <span data-ttu-id="0e77a-237">Een goede controle met een kort overzicht als volgt worden is voordat we ernstige werk.</span><span class="sxs-lookup"><span data-stu-id="0e77a-237">Having a quick look like this is a good sanity check before we start to do any serious work.</span></span>

### <a name="first-r-script"></a><span data-ttu-id="0e77a-238">Eerste R-script</span><span class="sxs-lookup"><span data-stu-id="0e77a-238">First R script</span></span>
<span data-ttu-id="0e77a-239">We gaan een eenvoudige eerste R-script om te experimenteren met in Azure Machine Learning Studio maken.</span><span class="sxs-lookup"><span data-stu-id="0e77a-239">Let's create a simple first R script to experiment with in Azure Machine Learning Studio.</span></span> <span data-ttu-id="0e77a-240">Ik heb gemaakt en getest met het volgende script in RStudio.</span><span class="sxs-lookup"><span data-stu-id="0e77a-240">I have created and tested the following script in RStudio.</span></span>  

    ## Only one of the following two lines should be used
    ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
    ## If in RStudio, use the second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="0e77a-241">Nu moet ik dit script overdragen naar Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="0e77a-241">Now I need to transfer this script to Azure Machine Learning Studio.</span></span> <span data-ttu-id="0e77a-242">Ik kan eenvoudig knippen en plakken.</span><span class="sxs-lookup"><span data-stu-id="0e77a-242">I could simply cut and paste.</span></span> <span data-ttu-id="0e77a-243">Echter, in dit geval ik draagt mijn R-script via een zip-bestand.</span><span class="sxs-lookup"><span data-stu-id="0e77a-243">However, in this case, I will transfer my R script via a zip file.</span></span>

### <a name="data-input-to-the-execute-r-script-module"></a><span data-ttu-id="0e77a-244">Gegevensinvoer voor de module R-Script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="0e77a-244">Data input to the Execute R Script module</span></span>
<span data-ttu-id="0e77a-245">We hebben een overzicht van de invoer voor de [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="0e77a-245">Let's have a look at the inputs to the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="0e77a-246">In dit voorbeeld leest de Californië melkkoeien gegevens in de [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="0e77a-246">In this example we will read the California dairy data into the [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="0e77a-247">Er zijn drie mogelijke ingangen voor de [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="0e77a-247">There are three possible inputs for the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="0e77a-248">U kunt een of meer van deze invoer, afhankelijk van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="0e77a-248">You may use any one or all of these inputs, depending on your application.</span></span> <span data-ttu-id="0e77a-249">Het is ook perfect redelijke een R-script waarmee geen invoer helemaal te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0e77a-249">It is also perfectly reasonable to use an R script that takes no input at all.</span></span>  

<span data-ttu-id="0e77a-250">We bekijken elk van deze invoer, die van links naar rechts.</span><span class="sxs-lookup"><span data-stu-id="0e77a-250">Let's look at each of these inputs, going from left to right.</span></span> <span data-ttu-id="0e77a-251">U ziet de namen van elk van de invoerwaarden door plaatst u de cursor op de invoer en de knopinfo te lezen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-251">You can see the names of each of the inputs by placing your cursor over the input and reading the tooltip.</span></span>  

#### <a name="script-bundle"></a><span data-ttu-id="0e77a-252">Script bundel</span><span class="sxs-lookup"><span data-stu-id="0e77a-252">Script Bundle</span></span>
<span data-ttu-id="0e77a-253">De Script-bundel invoer kunt u de inhoud van een zip-bestand in doorgeven [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="0e77a-253">The Script Bundle input allows you to pass the contents of a zip file into [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="0e77a-254">U kunt een van de volgende opdrachten gebruiken om de inhoud van het zip-bestand in uw R-code.</span><span class="sxs-lookup"><span data-stu-id="0e77a-254">You can use one of the following commands to read the contents of the zip file into your R code.</span></span>

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> <span data-ttu-id="0e77a-255">Azure Machine Learning-bestanden in het ZIP-bestand wordt behandeld alsof ze zich in de src / Active directory, dus moet u uw bestandsnamen met deze directorynaam voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="0e77a-255">Azure Machine Learning treats files in the zip as if they are in the src/ directory, so you need to prefix your file names with this directory name.</span></span> <span data-ttu-id="0e77a-256">Bijvoorbeeld, als het ZIP-bestand bevat de bestanden `yourfile.R` en `yourData.rdata` in de hoofdmap van het ZIP-bestand, zou u deze poorten als adresseren `src/yourfile.R` en `src/yourData.rdata` bij gebruik van `source` en `load`.</span><span class="sxs-lookup"><span data-stu-id="0e77a-256">For example, if the zip contains the files `yourfile.R` and `yourData.rdata` in the root of the zip, you would address these as `src/yourfile.R` and `src/yourData.rdata` when using `source` and `load`.</span></span>
> 
> 

<span data-ttu-id="0e77a-257">Besproken al gegevenssets laden in [bij het laden van de gegevensset](#loading).</span><span class="sxs-lookup"><span data-stu-id="0e77a-257">We already discussed loading datasets in [Loading the dataset](#loading).</span></span> <span data-ttu-id="0e77a-258">Zodra u hebt gemaakt en getest het R-script dat wordt weergegeven in de vorige sectie, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="0e77a-258">Once you have created and tested the R script shown in the previous section, do the following:</span></span>

1. <span data-ttu-id="0e77a-259">Sla het R-script in een. R-bestand.</span><span class="sxs-lookup"><span data-stu-id="0e77a-259">Save the R script into a .R file.</span></span> <span data-ttu-id="0e77a-260">Ik mijn scriptbestand 'simpleplot aanroepen. R'.</span><span class="sxs-lookup"><span data-stu-id="0e77a-260">I call my script file "simpleplot.R".</span></span> <span data-ttu-id="0e77a-261">Hier volgt de inhoud.</span><span class="sxs-lookup"><span data-stu-id="0e77a-261">Here's the contents.</span></span>
   
        ## Only one of the following two lines should be used
        ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
        ## If in RStudio, use the second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## The following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. <span data-ttu-id="0e77a-262">Maak een zip-bestand en kopieer het script naar dit zipbestand.</span><span class="sxs-lookup"><span data-stu-id="0e77a-262">Create a zip file and copy your script into this zip file.</span></span> <span data-ttu-id="0e77a-263">Op Windows, kunt u met de rechtermuisknop op het bestand en selecteer **verzenden naar**, en vervolgens **gecomprimeerde map**.</span><span class="sxs-lookup"><span data-stu-id="0e77a-263">On Windows, you can right-click on the file and select **Send to**, and then **Compressed folder**.</span></span> <span data-ttu-id="0e77a-264">Hiermee maakt u een nieuwe zip-bestand met de 'simpleplot. R'-bestand.</span><span class="sxs-lookup"><span data-stu-id="0e77a-264">This will create a new zip file containing the "simpleplot.R" file.</span></span>
3. <span data-ttu-id="0e77a-265">Toevoegen van het bestand naar de **gegevenssets** in Machine Learning Studio, op te geven als **zip**.</span><span class="sxs-lookup"><span data-stu-id="0e77a-265">Add your file to the **datasets** in Machine Learning Studio, specifying the type as **zip**.</span></span> <span data-ttu-id="0e77a-266">U ziet nu het zip-bestand in de gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="0e77a-266">You should now see the zip file in your datasets.</span></span>
4. <span data-ttu-id="0e77a-267">Slepen en neerzetten van het zip-bestand van **gegevenssets** naar de **ML Studio canvas**.</span><span class="sxs-lookup"><span data-stu-id="0e77a-267">Drag and drop the zip file from **datasets** onto the **ML Studio canvas**.</span></span>
5. <span data-ttu-id="0e77a-268">Verbinding maken met de uitvoer van de **zip-gegevens** pictogram voor de **Script bundel** invoer van de [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="0e77a-268">Connect the output of the **zip data** icon to the **Script Bundle** input of the [Execute R Script][execute-r-script] module.</span></span>
6. <span data-ttu-id="0e77a-269">Typ de `source()` functie met de naam van uw zip-bestand in het codevenster voor de [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="0e77a-269">Type the `source()` function with your zip file name into the code window for the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="0e77a-270">Ik heb getypt in mijn geval `source("src/simpleplot.R")`.</span><span class="sxs-lookup"><span data-stu-id="0e77a-270">In my case I typed `source("src/simpleplot.R")`.</span></span>  
7. <span data-ttu-id="0e77a-271">Controleer of u **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="0e77a-271">Make sure you click **Save**.</span></span>

<span data-ttu-id="0e77a-272">Als deze stappen voltooid zijn, de [R-Script uitvoeren] [ execute-r-script] module het R-script in het zip-bestand wordt uitgevoerd wanneer het experiment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0e77a-272">Once these steps are complete, the [Execute R Script][execute-r-script] module will execute the R script in the zip file when the experiment is run.</span></span> <span data-ttu-id="0e77a-273">Op dit moment ziet uw experiment er ongeveer als afbeelding 5.</span><span class="sxs-lookup"><span data-stu-id="0e77a-273">At this point your experiment should look something like Figure 5.</span></span>

![Experimenteer met gecomprimeerde R-script][6]

<span data-ttu-id="0e77a-275">*Afbeelding 5. Experimenteer met gecomprimeerde R-script.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-275">*Figure 5. Experiment using zipped R script.*</span></span>

#### <a name="dataset1"></a><span data-ttu-id="0e77a-276">Dataset1</span><span class="sxs-lookup"><span data-stu-id="0e77a-276">Dataset1</span></span>
<span data-ttu-id="0e77a-277">U kunt een rechthoekig gegevenstabel doorgeven aan uw R-code met behulp van de invoer Dataset1.</span><span class="sxs-lookup"><span data-stu-id="0e77a-277">You can pass a rectangular table of data to your R code by using the Dataset1 input.</span></span> <span data-ttu-id="0e77a-278">In onze eenvoudig script de `maml.mapInputPort(1)` functie leest de gegevens van poort 1.</span><span class="sxs-lookup"><span data-stu-id="0e77a-278">In our simple script the `maml.mapInputPort(1)` function reads the data from port 1.</span></span> <span data-ttu-id="0e77a-279">Deze gegevens wordt vervolgens toegewezen aan een dataframe variabelenaam in uw code.</span><span class="sxs-lookup"><span data-stu-id="0e77a-279">This data is then assigned to a dataframe variable name in your code.</span></span> <span data-ttu-id="0e77a-280">In onze eenvoudig script voert de eerste coderegel de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="0e77a-280">In our simple script the first line of code performs the assignment.</span></span>

    cadairydata <- maml.mapInputPort(1)

<span data-ttu-id="0e77a-281">Uw experiment uitvoeren door te klikken op de **uitvoeren** knop.</span><span class="sxs-lookup"><span data-stu-id="0e77a-281">Execute your experiment by clicking on the **Run** button.</span></span> <span data-ttu-id="0e77a-282">Als de uitvoering is voltooid, klikt u op de [R-Script uitvoeren] [ execute-r-script] module en klik vervolgens op **weergave logboek** in het eigenschappendeelvenster.</span><span class="sxs-lookup"><span data-stu-id="0e77a-282">When the execution finishes, click on the [Execute R Script][execute-r-script] module and then click **View output log** on the properties pane.</span></span> <span data-ttu-id="0e77a-283">Een nieuwe pagina moet worden weergegeven in uw browser met daarin de inhoud van het bestand uitvoer.log.</span><span class="sxs-lookup"><span data-stu-id="0e77a-283">A new page should appear in your browser showing the contents of the output.log file.</span></span> <span data-ttu-id="0e77a-284">Wanneer u omlaag schuiven ziet u ongeveer als volgt.</span><span class="sxs-lookup"><span data-stu-id="0e77a-284">When you scroll down you should see something like the following.</span></span>

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

<span data-ttu-id="0e77a-285">Verder omlaag op de pagina is dat meer gedetailleerde informatie over de kolommen, ziet er ongeveer als volgt.</span><span class="sxs-lookup"><span data-stu-id="0e77a-285">Farther down the page is more detailed information on the columns, which will look something like the following.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput]
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput]
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month            : chr  "Jan" "Feb" "Mar" "Apr" ...
    [ModuleOutput]
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput]
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput]
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput]
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...

<span data-ttu-id="0e77a-286">Deze resultaten zijn voornamelijk zoals verwacht, met 228 opmerkingen en 9 kolommen in de dataframe.</span><span class="sxs-lookup"><span data-stu-id="0e77a-286">These results are mostly as expected, with 228 observations and 9 columns in the dataframe.</span></span> <span data-ttu-id="0e77a-287">U ziet de kolomnamen, het gegevenstype R en een voorbeeld van elke kolom.</span><span class="sxs-lookup"><span data-stu-id="0e77a-287">We can see the column names, the R data type and a sample of each column.</span></span>

> [!NOTE]
> <span data-ttu-id="0e77a-288">Deze dezelfde afdruk is gemakkelijk beschikbaar vanuit de uitvoer van het R-apparaat van de [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="0e77a-288">This same printed output is conveniently available from the R Device output of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="0e77a-289">Bespreken we de uitvoer van de [R-Script uitvoeren] [ execute-r-script] module in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="0e77a-289">We will discuss the outputs of the [Execute R Script][execute-r-script] module in the next section.</span></span>  
> 
> 

#### <a name="dataset2"></a><span data-ttu-id="0e77a-290">Dataset2</span><span class="sxs-lookup"><span data-stu-id="0e77a-290">Dataset2</span></span>
<span data-ttu-id="0e77a-291">Het gedrag van de invoer Dataset2 is identiek aan die van Dataset1.</span><span class="sxs-lookup"><span data-stu-id="0e77a-291">The behavior of the Dataset2 input is identical to that of Dataset1.</span></span> <span data-ttu-id="0e77a-292">U kunt met behulp van deze invoer een tweede rechthoekige gegevenstabel doorgeven in uw R-code.</span><span class="sxs-lookup"><span data-stu-id="0e77a-292">Using this input you can pass a second rectangular table of data into your R code.</span></span> <span data-ttu-id="0e77a-293">De functie `maml.mapInputPort(2)`, met het argument 2 wordt gebruikt deze gegevens moeten worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="0e77a-293">The function `maml.mapInputPort(2)`, with the argument 2, is used to pass this data.</span></span>  

### <a name="execute-r-script-outputs"></a><span data-ttu-id="0e77a-294">De uitvoer R-Script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="0e77a-294">Execute R Script outputs</span></span>
#### <a name="output-a-dataframe"></a><span data-ttu-id="0e77a-295">Een dataframe uitvoer</span><span class="sxs-lookup"><span data-stu-id="0e77a-295">Output a dataframe</span></span>
<span data-ttu-id="0e77a-296">Kunt u de inhoud van een R-dataframe als een rechthoekig tabel via de poort resultaat Dataset1 uitvoeren met behulp van de `maml.mapOutputPort()` functie.</span><span class="sxs-lookup"><span data-stu-id="0e77a-296">You can output the contents of an R dataframe as a rectangular table through the Result Dataset1 port by using the `maml.mapOutputPort()` function.</span></span> <span data-ttu-id="0e77a-297">In onze eenvoudig R-script wordt uitgevoerd door de volgende regel.</span><span class="sxs-lookup"><span data-stu-id="0e77a-297">In our simple R script this is performed by the following line.</span></span>

    maml.mapOutputPort('cadairydata')

<span data-ttu-id="0e77a-298">Nadat het experiment is uitgevoerd, klikt u op de uitvoerpoort Dataset1 resultaat en klik vervolgens op **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="0e77a-298">After running the experiment, click on the Result Dataset1 output port and then click on **Visualize**.</span></span> <span data-ttu-id="0e77a-299">U ziet er ongeveer zo afbeelding 6.</span><span class="sxs-lookup"><span data-stu-id="0e77a-299">You should see something like Figure 6.</span></span>

![De visualisatie van de uitvoer van de Californië melkkoeien gegevens][7]

<span data-ttu-id="0e77a-301">*Afbeelding 6. De visualisatie van de uitvoer van de Californië melkkoeien gegevens.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-301">*Figure 6. The visualization of the output of the California dairy data.*</span></span>

<span data-ttu-id="0e77a-302">Deze uitvoer ziet er identiek is aan de invoer, precies zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="0e77a-302">This output looks identical to the input, exactly as we expected.</span></span>  

### <a name="r-device-output"></a><span data-ttu-id="0e77a-303">R-apparaat-uitvoer</span><span class="sxs-lookup"><span data-stu-id="0e77a-303">R Device output</span></span>
<span data-ttu-id="0e77a-304">De uitvoer van het apparaat van de [R-Script uitvoeren] [ execute-r-script] -module bevat de uitvoer van berichten en afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-304">The Device output of the [Execute R Script][execute-r-script] module contains messages and graphics output.</span></span> <span data-ttu-id="0e77a-305">Beide standaard uitvoer en de standaardfout van de berichten van R worden verzonden naar de uitvoerpoort R-apparaat.</span><span class="sxs-lookup"><span data-stu-id="0e77a-305">Both standard output and standard error messages from R are sent to the R Device output port.</span></span>  

<span data-ttu-id="0e77a-306">Weergave van de uitvoer van het R-apparaat, klikt u op de poort en klik vervolgens op **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="0e77a-306">To view the R Device output, click on the port and then on **Visualize**.</span></span> <span data-ttu-id="0e77a-307">De standaarduitvoer en de standaardfout van het R-script in afbeelding 7 ziet.</span><span class="sxs-lookup"><span data-stu-id="0e77a-307">We see the standard output and standard error from the R script in Figure 7.</span></span>

![Standaarduitvoer en de standaardfout van de poort R-apparaat][8]

<span data-ttu-id="0e77a-309">*Afbeelding 7. Standaarduitvoer en de standaardfout van de poort R-apparaat.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-309">*Figure 7. Standard output and standard error from the R Device port.*</span></span>

<span data-ttu-id="0e77a-310">De uitvoer van de afbeeldingen van onze R-script in afbeelding 8 verschuift we zien.</span><span class="sxs-lookup"><span data-stu-id="0e77a-310">Scrolling down we see the graphics output from our R script in Figure 8.</span></span>  

![Grafische uitvoer van de poort R-apparaat][9]

<span data-ttu-id="0e77a-312">*Afbeelding 8. Afbeeldingen de uitvoer van de poort R-apparaat.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-312">*Figure 8. Graphics output from the R Device port.*</span></span>  

## <span data-ttu-id="0e77a-313"><a id="filtering"></a>Gegevens filteren en transformatie</span><span class="sxs-lookup"><span data-stu-id="0e77a-313"><a id="filtering"></a>Data filtering and transformation</span></span>
<span data-ttu-id="0e77a-314">In deze sectie wordt uitgevoerd, er enkele elementaire gegevens filteren en transformatiebewerkingen op de Californië melkkoeien gegevens.</span><span class="sxs-lookup"><span data-stu-id="0e77a-314">In this section we will perform some basic data filtering and transformation operations on the California dairy data.</span></span> <span data-ttu-id="0e77a-315">Aan het einde van deze sectie hebben we gegevens in een indeling die geschikt is voor het bouwen van een analytische model.</span><span class="sxs-lookup"><span data-stu-id="0e77a-315">By the end of this section we will have data in a format suitable for building an analytic model.</span></span>  

<span data-ttu-id="0e77a-316">Meer specifiek, in deze sectie wordt we enkele algemene gegevens opruimen en transformatie taken uitvoeren: type transformatie, filteren op dataframes, nieuwe berekende kolommen, toe te voegen en de waarde van transformaties.</span><span class="sxs-lookup"><span data-stu-id="0e77a-316">More specifically, in this section we will perform several common data cleaning and transformation tasks: type transformation, filtering on dataframes, adding new computed columns, and value transformations.</span></span> <span data-ttu-id="0e77a-317">Deze achtergrond kunt u te maken met de veel variaties aangetroffen in de praktische problemen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-317">This background should help you deal with the many variations encountered in real-world problems.</span></span>

<span data-ttu-id="0e77a-318">De volledige R-code voor deze sectie is beschikbaar in het zip-bestand dat u eerder hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="0e77a-318">The complete R code for this section is available in the zip file you downloaded earlier.</span></span>

### <a name="type-transformations"></a><span data-ttu-id="0e77a-319">Type transformaties</span><span class="sxs-lookup"><span data-stu-id="0e77a-319">Type transformations</span></span>
<span data-ttu-id="0e77a-320">Nu dat we de Californië melkkoeien gegevens kunnen lezen in de R-code in de [R-Script uitvoeren] [ execute-r-script] -module, moeten we ervoor zorgen dat de gegevens in de kolommen het gewenste type en de indeling.</span><span class="sxs-lookup"><span data-stu-id="0e77a-320">Now that we can read the California dairy data into the R code in the [Execute R Script][execute-r-script] module, we need to ensure that the data in the columns has the intended type and format.</span></span>  

<span data-ttu-id="0e77a-321">R is een dynamisch getypeerde taal, wat betekent dat gegevenstypen worden gedwongen uit een naar een andere zoals vereist.</span><span class="sxs-lookup"><span data-stu-id="0e77a-321">R is a dynamically typed language, which means that data types are coerced from one to another as required.</span></span> <span data-ttu-id="0e77a-322">De atomic gegevenstypen in R bevatten numerieke waarden, logische en -teken.</span><span class="sxs-lookup"><span data-stu-id="0e77a-322">The atomic data types in R include numeric, logical and character.</span></span> <span data-ttu-id="0e77a-323">Het type factor wordt gebruikt voor het opslaan van compactly categorische gegevens.</span><span class="sxs-lookup"><span data-stu-id="0e77a-323">The factor type is used to compactly store categorical data.</span></span> <span data-ttu-id="0e77a-324">U vindt meer informatie over gegevenstypen in de verwijzingen in [bijlage B – Lees hier meer over](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="0e77a-324">You can find much more information on data types in the references in [Appendix B - Further reading](#appendixb).</span></span>

<span data-ttu-id="0e77a-325">Wanneer tabelgegevens wordt gelezen in R uit een externe bron, maar het is altijd een goed idee om te controleren van de resulterende typen in de kolommen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-325">When tabular data is read into R from an external source, it is always a good idea to check the resulting types in the columns.</span></span> <span data-ttu-id="0e77a-326">U kunt een kolom van het typeteken, maar in veel gevallen dit wordt weergegeven als factor of vice versa.</span><span class="sxs-lookup"><span data-stu-id="0e77a-326">You may want a column of type character, but in many cases this will show up as factor or vice versa.</span></span> <span data-ttu-id="0e77a-327">In andere gevallen een kolom die u denkt dat moet worden wordt numerieke vertegenwoordigd door tekengegevens, bijvoorbeeld '1,23' in plaats van 1,23 als een zwevende-kommagetal.</span><span class="sxs-lookup"><span data-stu-id="0e77a-327">In other cases a column you think should be numeric is represented by character data, e.g. '1.23' rather than 1.23 as a floating point number.</span></span>  

<span data-ttu-id="0e77a-328">Het is gelukkig eenvoudig één type converteren naar een andere, zolang de toewijzing is mogelijk.</span><span class="sxs-lookup"><span data-stu-id="0e77a-328">Fortunately, it is easy to convert one type to another, as long as mapping is possible.</span></span> <span data-ttu-id="0e77a-329">Bijvoorbeeld, u 'Nevada' niet converteren naar een numerieke waarde, maar u kunt deze converteren naar een factor (categorische variabele).</span><span class="sxs-lookup"><span data-stu-id="0e77a-329">For example, you cannot convert 'Nevada' into a numeric value, but you can convert it to a factor (categorical variable).</span></span> <span data-ttu-id="0e77a-330">U kunt bijvoorbeeld een numerieke 1 omzetten in een teken '1' of een factor.</span><span class="sxs-lookup"><span data-stu-id="0e77a-330">As another example, you can convert a numeric 1 into a character '1' or a factor.</span></span>  

<span data-ttu-id="0e77a-331">De syntaxis voor een van deze omzettingen is eenvoudig: `as.datatype()`.</span><span class="sxs-lookup"><span data-stu-id="0e77a-331">The syntax for any of these conversions is simple: `as.datatype()`.</span></span> <span data-ttu-id="0e77a-332">Deze functies voor typeconversie biedt de volgende.</span><span class="sxs-lookup"><span data-stu-id="0e77a-332">These type conversion functions include the following.</span></span>

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

<span data-ttu-id="0e77a-333">Kijken naar de gegevenstypen van de kolommen die we in de vorige sectie invoer: alle kolommen van het type numeriek zijn, met uitzondering van de kolom met het label 'Maand', van het typeteken is zijn.</span><span class="sxs-lookup"><span data-stu-id="0e77a-333">Looking at the data types of the columns we input in the previous section: all columns are of type numeric, except for the column labeled 'Month', which is of type character.</span></span> <span data-ttu-id="0e77a-334">Laten we dit converteren naar een factor en test de resultaten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-334">Let's convert this to a factor and test the results.</span></span>  

<span data-ttu-id="0e77a-335">Ik heb hebt de regel die de scatterplot matrix gemaakt en een regel die de kolom 'Maand' converteren naar een factor toegevoegd verwijderd.</span><span class="sxs-lookup"><span data-stu-id="0e77a-335">I have deleted the line that created the scatterplot matrix and added a line converting the 'Month' column to a factor.</span></span> <span data-ttu-id="0e77a-336">In mijn experiment ik net knippen en plak de code R in het codevenster van de [R-Script uitvoeren] [ execute-r-script] Module.</span><span class="sxs-lookup"><span data-stu-id="0e77a-336">In my experiment I will just cut and paste the R code into the code window of the [Execute R Script][execute-r-script] Module.</span></span> <span data-ttu-id="0e77a-337">U kunt ook het zip-bestand bijwerken en uploaden naar Azure Machine Learning Studio, maar dit verschillende stappen nodig.</span><span class="sxs-lookup"><span data-stu-id="0e77a-337">You could also update the zip file and upload it to Azure Machine Learning Studio, but this takes several steps.</span></span>  

    ## Only one of the following two lines should be used
    ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
    ## If in RStudio, use the second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure the coding is consistent and convert column to a factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check the result
    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="0e77a-338">Laten we deze code uitvoeren en bekijk het uitvoerlogboek voor voor het R-script.</span><span class="sxs-lookup"><span data-stu-id="0e77a-338">Let's execute this code and look at the output log for the R script.</span></span> <span data-ttu-id="0e77a-339">De relevante gegevens uit het logboek wordt weergegeven in afbeelding 9.</span><span class="sxs-lookup"><span data-stu-id="0e77a-339">The relevant data from the log is shown in Figure 9.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 14 levels "Apr","April",..: 6 5 9 1 11 8 7 3 14 13 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="0e77a-340">*Afbeelding 9. Samenvatting van de dataframe met een factor-variabele.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-340">*Figure 9. Summary of the dataframe with a factor variable.*</span></span>

<span data-ttu-id="0e77a-341">Het type voor de maand nu de melding '**Factor met 14 niveaus**'.</span><span class="sxs-lookup"><span data-stu-id="0e77a-341">The type for Month should now say '**Factor w/ 14 levels**'.</span></span> <span data-ttu-id="0e77a-342">Dit is een probleem, omdat er alleen 12 maanden in een jaar.</span><span class="sxs-lookup"><span data-stu-id="0e77a-342">This is a problem since there are only 12 months in the year.</span></span> <span data-ttu-id="0e77a-343">U kunt ook controleren om te zien die het type in **Visualize** van de gegevensset resultaat poort is '**Categorical**'.</span><span class="sxs-lookup"><span data-stu-id="0e77a-343">You can also check to see that the type in **Visualize** of the Result Dataset port is '**Categorical**'.</span></span>

<span data-ttu-id="0e77a-344">Het probleem is dat de kolom 'Maand' niet systematischer heeft is gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="0e77a-344">The problem is that the 'Month' column has not been coded systematically.</span></span> <span data-ttu-id="0e77a-345">In sommige gevallen een maand April wordt genoemd, en in andere gevallen wordt het april afgekort. We kunnen dit probleem oplossen door de tekenreeks die moet 3 tekens.</span><span class="sxs-lookup"><span data-stu-id="0e77a-345">In some cases a month is called April and in others it is abbreviated as Apr. We can solve this problem by trimming the string to 3 characters.</span></span> <span data-ttu-id="0e77a-346">De regel code ziet er nu als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="0e77a-346">The line of code now looks like the following:</span></span>

    ## Ensure the coding is consistent and convert column to a factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

<span data-ttu-id="0e77a-347">Het experiment opnieuw uitvoeren en bekijk het uitvoerlogboek voor.</span><span class="sxs-lookup"><span data-stu-id="0e77a-347">Rerun the experiment and view the output log.</span></span> <span data-ttu-id="0e77a-348">De verwachte resultaten worden weergegeven in afbeelding 10.</span><span class="sxs-lookup"><span data-stu-id="0e77a-348">The expected results are shown in Figure 10.</span></span>  

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="0e77a-349">*Afbeelding 10. Samenvatting van de dataframe met het juiste aantal factorniveaus.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-349">*Figure 10. Summary of the dataframe with correct number of factor levels.*</span></span>

<span data-ttu-id="0e77a-350">Onze variabele factor heeft nu de gewenste 12 niveaus.</span><span class="sxs-lookup"><span data-stu-id="0e77a-350">Our factor variable now has the desired 12 levels.</span></span>

### <a name="basic-data-frame-filtering"></a><span data-ttu-id="0e77a-351">Basisgegevens frame filteren</span><span class="sxs-lookup"><span data-stu-id="0e77a-351">Basic data frame filtering</span></span>
<span data-ttu-id="0e77a-352">R dataframes ondersteunen krachtige filteropties.</span><span class="sxs-lookup"><span data-stu-id="0e77a-352">R dataframes support powerful filtering capabilities.</span></span> <span data-ttu-id="0e77a-353">Gegevenssets kan subset met logische filters op rijen of kolommen zijn.</span><span class="sxs-lookup"><span data-stu-id="0e77a-353">Datasets can be subsetted by using logical filters on either rows or columns.</span></span> <span data-ttu-id="0e77a-354">In veel gevallen zijn complexe filtercriteria vereist.</span><span class="sxs-lookup"><span data-stu-id="0e77a-354">In many cases, complex filter criteria will be required.</span></span> <span data-ttu-id="0e77a-355">De verwijzingen in [bijlage B – Lees hier meer over](#appendixb) uitgebreide voorbeelden voor het filteren van dataframes bevatten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-355">The references in [Appendix B - Further reading](#appendixb) contain extensive examples of filtering dataframes.</span></span>  

<span data-ttu-id="0e77a-356">Er is één bit van het filter moet worden uitgevoerd op onze gegevensset.</span><span class="sxs-lookup"><span data-stu-id="0e77a-356">There is one bit of filtering we should do on our dataset.</span></span> <span data-ttu-id="0e77a-357">Als u de kolommen in de dataframe cadairydata bekijkt, ziet u twee overbodige kolommen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-357">If you look at the columns in the cadairydata dataframe, you will see two unnecessary columns.</span></span> <span data-ttu-id="0e77a-358">De eerste kolom bevat alleen een rijnummer, niet erg nuttig is.</span><span class="sxs-lookup"><span data-stu-id="0e77a-358">The first column just holds a row number, which is not very useful.</span></span> <span data-ttu-id="0e77a-359">De tweede kolom Year.Month, bevat redundante gegevens.</span><span class="sxs-lookup"><span data-stu-id="0e77a-359">The second column, Year.Month, contains redundant information.</span></span> <span data-ttu-id="0e77a-360">We kunnen deze kolommen eenvoudig uitsluiten met behulp van de volgende R-code.</span><span class="sxs-lookup"><span data-stu-id="0e77a-360">We can easily exclude these columns by using the following R code.</span></span>

> [!NOTE]
> <span data-ttu-id="0e77a-361">Voortaan in deze sectie net leest u de aanvullende code ik toe te voegen in de [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="0e77a-361">From now on in this section, I will just show you the additional code I am adding in the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="0e77a-362">Ik zal elke nieuwe regel toevoegen **voordat** de `str()` functie.</span><span class="sxs-lookup"><span data-stu-id="0e77a-362">I will add each new line **before** the `str()` function.</span></span> <span data-ttu-id="0e77a-363">Ik gebruik deze functie om mijn resultaten in Azure Machine Learning Studio te controleren.</span><span class="sxs-lookup"><span data-stu-id="0e77a-363">I use this function to verify my results in Azure Machine Learning Studio.</span></span>
> 
> 

<span data-ttu-id="0e77a-364">Ik de volgende regel toevoegen aan mijn R-code in de [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="0e77a-364">I add the following line to my R code in the [Execute R Script][execute-r-script] module.</span></span>

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

<span data-ttu-id="0e77a-365">Deze code in uw experiment uitvoeren en controleer het resultaat van het uitvoerlogboek voor.</span><span class="sxs-lookup"><span data-stu-id="0e77a-365">Run this code in your experiment and check the result from the output log.</span></span> <span data-ttu-id="0e77a-366">Deze resultaten worden weergegeven in afbeelding 11.</span><span class="sxs-lookup"><span data-stu-id="0e77a-366">These results are shown in Figure 11.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  7 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="0e77a-367">*Afbeelding 11. Samenvatting van de dataframe met twee kolommen die zijn verwijderd.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-367">*Figure 11. Summary of the dataframe with two columns removed.*</span></span>

<span data-ttu-id="0e77a-368">Goed nieuws!</span><span class="sxs-lookup"><span data-stu-id="0e77a-368">Good news!</span></span> <span data-ttu-id="0e77a-369">We krijgt de verwachte resultaten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-369">We get the expected results.</span></span>

### <a name="add-a-new-column"></a><span data-ttu-id="0e77a-370">Een nieuwe kolom toevoegen</span><span class="sxs-lookup"><span data-stu-id="0e77a-370">Add a new column</span></span>
<span data-ttu-id="0e77a-371">Als u wilt maken van de time series modellen zal zijn handig zijn als een kolom met de maanden sinds de start van de tijdreeks.</span><span class="sxs-lookup"><span data-stu-id="0e77a-371">To create time series models it will be convenient to have a column containing the months since the start of the time series.</span></span> <span data-ttu-id="0e77a-372">We gaan een nieuwe kolom 'Month.Count' maken.</span><span class="sxs-lookup"><span data-stu-id="0e77a-372">We will create a new column 'Month.Count'.</span></span>

<span data-ttu-id="0e77a-373">Voor het ordenen van de code maken we onze eerste eenvoudige functie `num.month()`.</span><span class="sxs-lookup"><span data-stu-id="0e77a-373">To help organize the code we will create our first simple function, `num.month()`.</span></span> <span data-ttu-id="0e77a-374">Deze functie om een nieuwe kolom maken in de dataframe wordt vervolgens toegepast.</span><span class="sxs-lookup"><span data-stu-id="0e77a-374">We will then apply this function to create a new column in the dataframe.</span></span> <span data-ttu-id="0e77a-375">De nieuwe code is als volgt.</span><span class="sxs-lookup"><span data-stu-id="0e77a-375">The new code is as follows.</span></span>

    ## Create a new column with the month count
    ## Function to find the number of months from the first
    ## month of the time series
    num.month <- function(Year, Month) {
      ## Find the starting year
      min.year  <- min(Year)

      ## Compute the number of months from the start of the time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute the new column for the dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

<span data-ttu-id="0e77a-376">Nu de bijgewerkte experiment uitvoeren en de logboeken van de uitvoer gebruikt om de resultaten weer te geven.</span><span class="sxs-lookup"><span data-stu-id="0e77a-376">Now run the updated experiment and use the output log to view the results.</span></span> <span data-ttu-id="0e77a-377">Deze resultaten worden weergegeven in afbeelding 12.</span><span class="sxs-lookup"><span data-stu-id="0e77a-377">These results are shown in Figure 12.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="0e77a-378">*Afbeelding 12. Samenvatting van de dataframe met de extra kolom.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-378">*Figure 12. Summary of the dataframe with the additional column.*</span></span>

<span data-ttu-id="0e77a-379">Het lijkt dat alles werkt.</span><span class="sxs-lookup"><span data-stu-id="0e77a-379">It looks like everything is working.</span></span> <span data-ttu-id="0e77a-380">We hebben de nieuwe kolom met de verwachte waarden in onze dataframe.</span><span class="sxs-lookup"><span data-stu-id="0e77a-380">We have the new column with the expected values in our dataframe.</span></span>

### <a name="value-transformations"></a><span data-ttu-id="0e77a-381">Waarde transformaties</span><span class="sxs-lookup"><span data-stu-id="0e77a-381">Value transformations</span></span>
<span data-ttu-id="0e77a-382">In deze sectie zullen we enkele eenvoudige transformaties uitvoeren van de waarden in een aantal van de kolommen van onze dataframe.</span><span class="sxs-lookup"><span data-stu-id="0e77a-382">In this section we will perform some simple transformations on the values in some of the columns of our dataframe.</span></span> <span data-ttu-id="0e77a-383">De R-taal ondersteunt bijna willekeurige waarde transformaties.</span><span class="sxs-lookup"><span data-stu-id="0e77a-383">The R language supports nearly arbitrary value transformations.</span></span> <span data-ttu-id="0e77a-384">De verwijzingen in [bijlage B - verdere lezen](#appendixb) uitgebreide voorbeelden bevatten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-384">The references in [Appendix B - Further Reading](#appendixb) contain extensive examples.</span></span>

<span data-ttu-id="0e77a-385">Als u de waarden in de samenvatting van onze dataframe bekijkt ziet u iets oneven hier.</span><span class="sxs-lookup"><span data-stu-id="0e77a-385">If you look at the values in the summaries of our dataframe you should see something odd here.</span></span> <span data-ttu-id="0e77a-386">Is meer ijs dan melk geproduceerd in Californië?</span><span class="sxs-lookup"><span data-stu-id="0e77a-386">Is more ice cream than milk produced in California?</span></span> <span data-ttu-id="0e77a-387">Nee, natuurlijk omdat dit geen zin jammer als dit feit kunnen niet tot een aantal van ons ijs Ontwikkelaarshulpmiddelen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-387">No, of course not, as this makes no sense, sad as this fact may be to some of us ice cream lovers.</span></span> <span data-ttu-id="0e77a-388">De eenheden zijn verschillend.</span><span class="sxs-lookup"><span data-stu-id="0e77a-388">The units are different.</span></span> <span data-ttu-id="0e77a-389">De prijs is in eenheden van ons pond, melk is in eenheden van 1 M VS pond, ijs in eenheden van 1000 ons gallon en Kwark in eenheden van 1000 VS pond is.</span><span class="sxs-lookup"><span data-stu-id="0e77a-389">The price is in units of US pounds, milk is in units of 1 M US pounds, ice cream is in units of 1,000 US gallons, and cottage cheese is in units of 1,000 US pounds.</span></span> <span data-ttu-id="0e77a-390">Ervan uitgaande dat ijs weegt ongeveer 6,5 pond per gallon, kunnen eenvoudig doen we de vermenigvuldiging als u wilt converteren van deze waarden, zodat ze allemaal in gelijk eenheden van 1000 pond.</span><span class="sxs-lookup"><span data-stu-id="0e77a-390">Assuming ice cream weighs about 6.5 pounds per gallon, we can easily do the multiplication to convert these values so they are all in equal units of 1,000 pounds.</span></span>

<span data-ttu-id="0e77a-391">We gebruiken een Multiplicatieve model voor het trendanalyse en correctie van deze gegevens voor onze prognosemodel.</span><span class="sxs-lookup"><span data-stu-id="0e77a-391">For our forecasting model we use a multiplicative model for trend and seasonal adjustment of this data.</span></span> <span data-ttu-id="0e77a-392">Een transformatie logboek kan we gebruiken een lineaire model, dit proces vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-392">A log transformation allows us to use a linear model, simplifying this process.</span></span> <span data-ttu-id="0e77a-393">De transformatie logboek in dezelfde functie waarin de vermenigvuldiger is toegepast kan worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="0e77a-393">We can apply the log transformation in the same function where the multiplier is applied.</span></span>

<span data-ttu-id="0e77a-394">In de volgende code ik een nieuwe functie definiëren `log.transform()`, en dit toepassen op de rijen met numerieke waarden.</span><span class="sxs-lookup"><span data-stu-id="0e77a-394">In the following code, I define a new function, `log.transform()`, and apply it to the rows containing the numerical values.</span></span> <span data-ttu-id="0e77a-395">Het R `Map()` functie wordt gebruikt om toe te passen de `log.transform()` functie met de geselecteerde kolommen van de dataframe.</span><span class="sxs-lookup"><span data-stu-id="0e77a-395">The R `Map()` function is used to apply the `log.transform()` function to the selected columns of the dataframe.</span></span> <span data-ttu-id="0e77a-396">`Map()`is vergelijkbaar met `apply()` maar kunt u meer dan een lijst met argumenten voor de functie.</span><span class="sxs-lookup"><span data-stu-id="0e77a-396">`Map()` is similar to `apply()` but allows for more than one list of arguments to the function.</span></span> <span data-ttu-id="0e77a-397">Houd er rekening mee dat een lijst met ze het tweede argument levert de `log.transform()` functie.</span><span class="sxs-lookup"><span data-stu-id="0e77a-397">Note that a list of multipliers supplies the second argument to the `log.transform()` function.</span></span> <span data-ttu-id="0e77a-398">De `na.omit()` functie als een stukje opschonen wordt gebruikt om te controleren of er geen ontbreekt of niet-gedefinieerde waarden in de dataframe.</span><span class="sxs-lookup"><span data-stu-id="0e77a-398">The `na.omit()` function is used as a bit of cleanup to ensure we do not have missing or undefined values in the dataframe.</span></span>

    log.transform <- function(invec, multiplier = 1) {
      ## Function for the transformation, which is the log
      ## of the input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments to function log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier to funcition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check the input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap the multiplication in tryCatch
      ## If there is an exception, print the warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply the transformation function to the 4 columns
    ## of the dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

<span data-ttu-id="0e77a-399">Er is zeer bits gebeurt in de `log.transform()` functie.</span><span class="sxs-lookup"><span data-stu-id="0e77a-399">There is quite a bit happening in the `log.transform()` function.</span></span> <span data-ttu-id="0e77a-400">De meeste van deze code controleert op mogelijke problemen met de argumenten of omgaan met uitzonderingen die nog steeds tijdens de berekeningen optreden kunnen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-400">Most of this code is checking for potential problems with the arguments or dealing with exceptions, which can still arise during the computations.</span></span> <span data-ttu-id="0e77a-401">Slechts een paar regels van deze code doen daadwerkelijk berekeningen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-401">Only a few lines of this code actually do the computations.</span></span>

<span data-ttu-id="0e77a-402">Het doel van de defensive programmering is om te voorkomen dat het uitvallen van één functie die voorkomt dat de verwerking niet door kan gaan.</span><span class="sxs-lookup"><span data-stu-id="0e77a-402">The goal of the defensive programming is to prevent the failure of a single function that prevents processing from continuing.</span></span> <span data-ttu-id="0e77a-403">Een plotselinge storing van een analyse langlopende kan frustrerend behoorlijk voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="0e77a-403">An abrupt failure of a long-running analysis can be quite frustrating for users.</span></span> <span data-ttu-id="0e77a-404">Om deze situatie te voorkomen, moeten standaard retourwaarden worden gekozen dat schade aan de downstreamverwerking wordt beperkt.</span><span class="sxs-lookup"><span data-stu-id="0e77a-404">To avoid this situation, default return values must be chosen that will limit damage to downstream processing.</span></span> <span data-ttu-id="0e77a-405">Een bericht wordt ook gemaakt worden gebruikers geïnformeerd dat er iets een opgetreden fout is.</span><span class="sxs-lookup"><span data-stu-id="0e77a-405">A message is also produced to alert users that something has gone wrong.</span></span>

<span data-ttu-id="0e77a-406">Als u niet aan defensive programmering in R worden gebruikt, zijn alle deze code lijkt enigszins overweldigend.</span><span class="sxs-lookup"><span data-stu-id="0e77a-406">If you are not used to defensive programming in R, all this code may seem a bit overwhelming.</span></span> <span data-ttu-id="0e77a-407">Ik begeleidt u stapsgewijs door de belangrijkste stappen:</span><span class="sxs-lookup"><span data-stu-id="0e77a-407">I will walk you through the major steps:</span></span>

1. <span data-ttu-id="0e77a-408">Een vector van vier berichten is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="0e77a-408">A vector of four messages is defined.</span></span> <span data-ttu-id="0e77a-409">Deze berichten worden gebruikt om informatie over een aantal van de mogelijke fouten en uitzonderingen die zich met deze code voordoen kunnen te communiceren.</span><span class="sxs-lookup"><span data-stu-id="0e77a-409">These messages are used to communicate information about some of the possible errors and exceptions that can occur with this code.</span></span>
2. <span data-ttu-id="0e77a-410">Ik retourneren NA de waarde voor elk geval.</span><span class="sxs-lookup"><span data-stu-id="0e77a-410">I return a value of NA for each case.</span></span> <span data-ttu-id="0e77a-411">Er zijn tal van andere mogelijkheden die mogelijk minder neveneffecten hebben.</span><span class="sxs-lookup"><span data-stu-id="0e77a-411">There are many other possibilities that might have fewer side effects.</span></span> <span data-ttu-id="0e77a-412">Ik kan een vector van nullen of de oorspronkelijke invoer vector bijvoorbeeld retourneren.</span><span class="sxs-lookup"><span data-stu-id="0e77a-412">I could return a vector of zeroes, or the original input vector, for example.</span></span>
3. <span data-ttu-id="0e77a-413">Controles worden uitgevoerd op de argumenten voor de functie.</span><span class="sxs-lookup"><span data-stu-id="0e77a-413">Checks are run on the arguments to the function.</span></span> <span data-ttu-id="0e77a-414">In elk geval als een fout wordt gedetecteerd, een standaardwaarde geretourneerd en wordt een bericht wordt geproduceerd door de `warning()` functie.</span><span class="sxs-lookup"><span data-stu-id="0e77a-414">In each case, if an error is detected, a default value is returned and a message is produced by the `warning()` function.</span></span> <span data-ttu-id="0e77a-415">Ik gebruik `warning()` plaats `stop()` als de laatste uitvoering beëindigt, precies wat ik probeer om te voorkomen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-415">I am using `warning()` rather than `stop()` as the latter will terminate execution, exactly what I am trying to avoid.</span></span> <span data-ttu-id="0e77a-416">Houd er rekening mee dat ik hebt geschreven deze code in een procedurele style, zoals in dit geval een functionele benadering leek complex en verborgen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-416">Note that I have written this code in a procedural style, as in this case a functional approach seemed complex and obscure.</span></span>
4. <span data-ttu-id="0e77a-417">De logboek-berekeningen zijn samengevoegd in `tryCatch()` zodat uitzonderingen niet een abrupte stoppen op de verwerking tot leidt.</span><span class="sxs-lookup"><span data-stu-id="0e77a-417">The log computations are wrapped in `tryCatch()` so that exceptions will not cause an abrupt halt to processing.</span></span> <span data-ttu-id="0e77a-418">Zonder `tryCatch()` de meeste fouten die worden gegenereerd door R functies resulteren in een stopsignaal ontvangen die geregeld worden.</span><span class="sxs-lookup"><span data-stu-id="0e77a-418">Without `tryCatch()` most errors raised by R functions result in a stop signal, which does just that.</span></span>

<span data-ttu-id="0e77a-419">Deze R-code in uw experiment uitvoeren en bekijk de uitvoer in het bestand uitvoer.log hebben.</span><span class="sxs-lookup"><span data-stu-id="0e77a-419">Execute this R code in your experiment and have a look at the printed output in the output.log file.</span></span> <span data-ttu-id="0e77a-420">U ziet nu de omgezette waarden van de vier kolommen in het logboek, zoals wordt weergegeven in afbeelding 13.</span><span class="sxs-lookup"><span data-stu-id="0e77a-420">You will now see the transformed values of the four columns in the log, as shown in Figure 13.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="0e77a-421">*Afbeelding 13. Samenvatting van de getransformeerde waarden in de dataframe.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-421">*Figure 13. Summary of the transformed values in the dataframe.*</span></span>

<span data-ttu-id="0e77a-422">Ziet u de waarden zijn getransformeerd.</span><span class="sxs-lookup"><span data-stu-id="0e77a-422">We see the values have been transformed.</span></span> <span data-ttu-id="0e77a-423">Melkproductie nu is aanzienlijk groter dan alle andere melkkoeien product productie, terughalen dat we nu een logaritmische schaal kijkt.</span><span class="sxs-lookup"><span data-stu-id="0e77a-423">Milk production now greatly exceeds all other dairy product production, recalling that we are now looking at a log scale.</span></span>

<span data-ttu-id="0e77a-424">Op dit moment onze gegevens wordt opgeschoond en we klaar zijn voor sommige modellen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-424">At this point our data is cleaned up and we are ready for some modeling.</span></span> <span data-ttu-id="0e77a-425">Kijken naar de samenvatting voor de uitvoer resultaat gegevensset van visualisatie onze [R-Script uitvoeren] [ execute-r-script] module, ziet u de kolom 'Maand' is 'Categorical' met 12 unieke waarden, opnieuw, net zoals we wilden.</span><span class="sxs-lookup"><span data-stu-id="0e77a-425">Looking at the visualization summary for the Result Dataset output of our [Execute R Script][execute-r-script] module, you will see the 'Month' column is 'Categorical' with 12 unique values, again, just as we wanted.</span></span>

## <span data-ttu-id="0e77a-426"><a id="timeseries"></a>Time series-objecten en correlatieanalyse</span><span class="sxs-lookup"><span data-stu-id="0e77a-426"><a id="timeseries"></a>Time series objects and correlation analysis</span></span>
<span data-ttu-id="0e77a-427">In deze sectie wordt een paar basic R time series-objecten te verkennen en analyseren van de correlatie tussen enkele van de variabelen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-427">In this section we will explore a few basic R time series objects and analyze the correlations between some of the variables.</span></span> <span data-ttu-id="0e77a-428">Ons doel is om uit te voeren een dataframe waarin de pairwise correlatie-gegevens op verschillende lag.</span><span class="sxs-lookup"><span data-stu-id="0e77a-428">Our goal is to output a dataframe containing the pairwise correlation information at several lags.</span></span>

<span data-ttu-id="0e77a-429">De volledige R-code voor deze sectie wordt het zip-bestand dat u eerder hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="0e77a-429">The complete R code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="time-series-objects-in-r"></a><span data-ttu-id="0e77a-430">Time series-objecten in R</span><span class="sxs-lookup"><span data-stu-id="0e77a-430">Time series objects in R</span></span>
<span data-ttu-id="0e77a-431">Zoals al is vermeld, tijd reeksen al een reeks gegevenswaarden geïndexeerd door tijd zijn.</span><span class="sxs-lookup"><span data-stu-id="0e77a-431">As already mentioned, time series are a series of data values indexed by time.</span></span> <span data-ttu-id="0e77a-432">R time series-objecten worden gebruikt voor het maken en beheren van de tijdsindex.</span><span class="sxs-lookup"><span data-stu-id="0e77a-432">R time series objects are used to create and manage the time index.</span></span> <span data-ttu-id="0e77a-433">Er zijn enkele voordelen van time series-objecten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-433">There are several advantages to using time series objects.</span></span> <span data-ttu-id="0e77a-434">Time series-objecten vrij u van veel meer informatie over het beheren van de reeks index tijdwaarden die worden ingekapseld in het object.</span><span class="sxs-lookup"><span data-stu-id="0e77a-434">Time series objects free you from the many details of managing the time series index values that are encapsulated in the object.</span></span> <span data-ttu-id="0e77a-435">Bovendien kunnen time series-objecten u het veel tijd reeks methoden gebruiken voor het uitzetten, afdrukken, modellering, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="0e77a-435">In addition, time series objects allow you to use the many time series methods for plotting, printing, modeling, etc.</span></span>

<span data-ttu-id="0e77a-436">De POSIXct time series-klasse wordt vaak gebruikt en relatief eenvoudig is.</span><span class="sxs-lookup"><span data-stu-id="0e77a-436">The POSIXct time series class is commonly used and is relatively simple.</span></span> <span data-ttu-id="0e77a-437">Deze tijdreeks klasse metingen tijd vanaf het begin van de epoche, 1 januari 1970.</span><span class="sxs-lookup"><span data-stu-id="0e77a-437">This time series class measures time from the start of the epoch, January 1, 1970.</span></span> <span data-ttu-id="0e77a-438">In dit voorbeeld gebruiken we POSIXct time series-objecten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-438">We will use POSIXct time series objects in this example.</span></span> <span data-ttu-id="0e77a-439">Andere klassen gebruikte R time series-object zijn zoo en xts, uitbreidbare tijdreeks.</span><span class="sxs-lookup"><span data-stu-id="0e77a-439">Other widely used R time series object classes include zoo and xts, extensible time series.</span></span>
<!-- Additional information on R time series objects is provided in the references in Section 5.7. [commenting because this section doesn't exist, even in the original] -->

### <a name="time-series-object-example"></a><span data-ttu-id="0e77a-440">Voorbeeld van een reeks object tijd</span><span class="sxs-lookup"><span data-stu-id="0e77a-440">Time series object example</span></span>
<span data-ttu-id="0e77a-441">Laten we aan de slag met het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="0e77a-441">Let's get started with our example.</span></span> <span data-ttu-id="0e77a-442">Slepen en neerzetten een **nieuwe** [R-Script uitvoeren] [ execute-r-script] module in uw experiment.</span><span class="sxs-lookup"><span data-stu-id="0e77a-442">Drag and drop a **new** [Execute R Script][execute-r-script] module into your experiment.</span></span> <span data-ttu-id="0e77a-443">Verbinding maken met de uitvoerpoort Dataset1 resultaat van de bestaande [R-Script uitvoeren] [ execute-r-script] module die u wilt de Dataset1 poort van de nieuwe invoer [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="0e77a-443">Connect the Result Dataset1 output port of the existing [Execute R Script][execute-r-script] module to the Dataset1 input port of the new [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="0e77a-444">Zoals ik deed voor de eerste voorbeelden zoals we het voorbeeld doorlopen, op bepaalde tijdstippen leest alleen de incrementele extra regels met code R bij elke stap.</span><span class="sxs-lookup"><span data-stu-id="0e77a-444">As I did for the first examples, as we progress through the example, at some points I will show only the incremental additional lines of R code at each step.</span></span>  

#### <a name="reading-the-dataframe"></a><span data-ttu-id="0e77a-445">Lezen van de dataframe</span><span class="sxs-lookup"><span data-stu-id="0e77a-445">Reading the dataframe</span></span>
<span data-ttu-id="0e77a-446">Laten we als eerste stap in een dataframe gelezen en controleer of krijgen we de verwachte resultaten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-446">As a first step, let's read in a dataframe and make sure we get the expected results.</span></span> <span data-ttu-id="0e77a-447">De taak moet doen, de volgende code.</span><span class="sxs-lookup"><span data-stu-id="0e77a-447">The following code should do the job.</span></span>

    # Comment the following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check the results

<span data-ttu-id="0e77a-448">Voer nu het experiment.</span><span class="sxs-lookup"><span data-stu-id="0e77a-448">Now, run the experiment.</span></span> <span data-ttu-id="0e77a-449">Het logboek van de nieuwe vorm van R-Script uitvoeren moet eruitzien als afbeelding 14.</span><span class="sxs-lookup"><span data-stu-id="0e77a-449">The log of the new Execute R Script shape should look like Figure 14.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...

<span data-ttu-id="0e77a-450">*Afbeelding 14. Samenvatting van de dataframe in de module R-Script niet uitvoeren.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-450">*Figure 14. Summary of the dataframe in the Execute R Script module.*</span></span>

<span data-ttu-id="0e77a-451">Deze gegevens is van het verwachte typen en de indeling.</span><span class="sxs-lookup"><span data-stu-id="0e77a-451">This data is of the expected types and format.</span></span> <span data-ttu-id="0e77a-452">Houd er rekening mee dat de kolom "Maand" type factor en het verwachte aantal niveaus heeft.</span><span class="sxs-lookup"><span data-stu-id="0e77a-452">Note that the 'Month' column is of type factor and has the expected number of levels.</span></span>

#### <a name="creating-a-time-series-object"></a><span data-ttu-id="0e77a-453">Een time series-object maken</span><span class="sxs-lookup"><span data-stu-id="0e77a-453">Creating a time series object</span></span>
<span data-ttu-id="0e77a-454">Er moet een time series-object toevoegen aan onze dataframe.</span><span class="sxs-lookup"><span data-stu-id="0e77a-454">We need to add a time series object to our dataframe.</span></span> <span data-ttu-id="0e77a-455">De huidige code vervangen door de volgende, waarmee een nieuwe kolom van klasse POSIXct worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="0e77a-455">Replace the current code with the following, which adds a new column of class POSIXct.</span></span>

    # Comment the following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check the results

<span data-ttu-id="0e77a-456">Controleer nu het logboek.</span><span class="sxs-lookup"><span data-stu-id="0e77a-456">Now, check the log.</span></span> <span data-ttu-id="0e77a-457">Het moet eruitzien als afbeelding 15.</span><span class="sxs-lookup"><span data-stu-id="0e77a-457">It should look like Figure 15.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="0e77a-458">*Afbeelding 15. Samenvatting van de dataframe met een time series-object.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-458">*Figure 15. Summary of the dataframe with a time series object.*</span></span>

<span data-ttu-id="0e77a-459">We kunt in het overzicht dat de nieuwe kolom die in feite van klasse POSIXct is zien.</span><span class="sxs-lookup"><span data-stu-id="0e77a-459">We can see from the summary that the new column is in fact of class POSIXct.</span></span>

### <a name="exploring-and-transforming-the-data"></a><span data-ttu-id="0e77a-460">Verkennen en de gegevens transformeren</span><span class="sxs-lookup"><span data-stu-id="0e77a-460">Exploring and transforming the data</span></span>
<span data-ttu-id="0e77a-461">We gaan verkennen enkele van de variabelen in deze dataset.</span><span class="sxs-lookup"><span data-stu-id="0e77a-461">Let's explore some of the variables in this dataset.</span></span> <span data-ttu-id="0e77a-462">Een matrix scatterplot is een prima manier voor het produceren van een beknopte beschrijving.</span><span class="sxs-lookup"><span data-stu-id="0e77a-462">A scatterplot matrix is a good way to produce a quick look.</span></span> <span data-ttu-id="0e77a-463">Ik ben vervangen de `str()` functie in de vorige code R met de volgende regel.</span><span class="sxs-lookup"><span data-stu-id="0e77a-463">I am replacing the `str()` function in the previous R code with the following line.</span></span>

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

<span data-ttu-id="0e77a-464">Voer deze code en kijk wat er gebeurt.</span><span class="sxs-lookup"><span data-stu-id="0e77a-464">Run this code and see what happens.</span></span> <span data-ttu-id="0e77a-465">De grafiek geproduceerd op de poort R-apparaat moet eruitzien als afbeelding 16.</span><span class="sxs-lookup"><span data-stu-id="0e77a-465">The plot produced at the R Device port should look like Figure 16.</span></span>

![Matrix van geselecteerde variabelen Scatterplot][17]

<span data-ttu-id="0e77a-467">*Afbeelding 16. Scatterplot matrix van geselecteerde variabelen.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-467">*Figure 16. Scatterplot matrix of selected variables.*</span></span>

<span data-ttu-id="0e77a-468">Er is een aantal vreemd uitziet structuur in de relaties tussen deze variabelen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-468">There is some odd-looking structure in the relationships between these variables.</span></span> <span data-ttu-id="0e77a-469">Hierdoor ontstaat mogelijk van trends in de gegevens en van het feit dat we hebben de variabelen niet gestandaardiseerd.</span><span class="sxs-lookup"><span data-stu-id="0e77a-469">Perhaps this arises from trends in the data and from the fact that we have not standardized the variables.</span></span>

### <a name="correlation-analysis"></a><span data-ttu-id="0e77a-470">Correlatieanalyse</span><span class="sxs-lookup"><span data-stu-id="0e77a-470">Correlation analysis</span></span>
<span data-ttu-id="0e77a-471">Als u wilt de analyse van de correlatie moeten we ongedaan trend en te standaardiseren, de variabelen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-471">To perform correlation analysis we need to both de-trend and standardize the variables.</span></span> <span data-ttu-id="0e77a-472">Het R kan alleen worden gebruikt `scale()` functie, die zowel datacenters en het schalen van variabelen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-472">We could simply use the R `scale()` function, which both centers and scales variables.</span></span> <span data-ttu-id="0e77a-473">Deze functie mogelijk ook sneller worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0e77a-473">This function might well run faster.</span></span> <span data-ttu-id="0e77a-474">Ik wil echter ziet u een voorbeeld van defensive programing in R.</span><span class="sxs-lookup"><span data-stu-id="0e77a-474">However, I want to show you an example of defensive programing in R.</span></span>

<span data-ttu-id="0e77a-475">De `ts.detrend()` functie hieronder beide van deze bewerkingen uitvoert.</span><span class="sxs-lookup"><span data-stu-id="0e77a-475">The `ts.detrend()` function shown below performs both of these operations.</span></span> <span data-ttu-id="0e77a-476">De volgende twee regels code ongedaan trend van de gegevens en vervolgens de waarden te standaardiseren.</span><span class="sxs-lookup"><span data-stu-id="0e77a-476">The following two lines of code de-trend the data and then standardize the values.</span></span>

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function to de-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time to have the same length',
                    'ERROR: ts.detrend requires argument ts to be of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros to return as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # The input arguments are not of the same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If the ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If the ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that the Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend the time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply the detrend.ts function to the variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot the results to look at the relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

<span data-ttu-id="0e77a-477">Er is zeer bits gebeurt in de `ts.detrend()` functie.</span><span class="sxs-lookup"><span data-stu-id="0e77a-477">There is quite a bit happening in the `ts.detrend()` function.</span></span> <span data-ttu-id="0e77a-478">De meeste van deze code controleert op mogelijke problemen met de argumenten of omgaan met uitzonderingen die nog steeds tijdens de berekeningen optreden kunnen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-478">Most of this code is checking for potential problems with the arguments or dealing with exceptions, which can still arise during the computations.</span></span> <span data-ttu-id="0e77a-479">Slechts een paar regels van deze code doen daadwerkelijk berekeningen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-479">Only a few lines of this code actually do the computations.</span></span>

<span data-ttu-id="0e77a-480">We hebben al een voorbeeld van defensive programmering in besproken [transformaties waarde](#valuetransformations).</span><span class="sxs-lookup"><span data-stu-id="0e77a-480">We have already discussed an example of defensive programming in [Value transformations](#valuetransformations).</span></span> <span data-ttu-id="0e77a-481">Beide blokken berekening zijn samengevoegd in `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="0e77a-481">Both computation blocks are wrapped in `tryCatch()`.</span></span> <span data-ttu-id="0e77a-482">Voor een aantal fouten is het verstandig om te retourneren van de oorspronkelijke invoer vector en in andere gevallen ik een vector nullen retourneren.</span><span class="sxs-lookup"><span data-stu-id="0e77a-482">For some errors it makes sense to return the original input vector, and in other cases, I return a vector of zeros.</span></span>  

<span data-ttu-id="0e77a-483">Houd er rekening mee dat de lineaire regressie gebruikt voor trending ongedaan een reeks tijd regressie is.</span><span class="sxs-lookup"><span data-stu-id="0e77a-483">Note that the linear regression used for de-trending is a time series regression.</span></span> <span data-ttu-id="0e77a-484">De variabele manier is een time series-object.</span><span class="sxs-lookup"><span data-stu-id="0e77a-484">The predictor variable is a time series object.</span></span>  

<span data-ttu-id="0e77a-485">Eenmaal `ts.detrend()` is gedefinieerd wordt toegepast op de variabelen in onze dataframe van belang.</span><span class="sxs-lookup"><span data-stu-id="0e77a-485">Once `ts.detrend()` is defined we apply it to the variables of interest in our dataframe.</span></span> <span data-ttu-id="0e77a-486">We moeten de resulterende lijst gemaakt met forceren `lapply()` naar dataframe gegevens met behulp van `as.data.frame()`.</span><span class="sxs-lookup"><span data-stu-id="0e77a-486">We must coerce the resulting list created by `lapply()` to data dataframe by using `as.data.frame()`.</span></span> <span data-ttu-id="0e77a-487">Vanwege defensive aspecten van `ts.detrend()`, niet-proces een van de variabelen voorkomt niet dat de juiste verwerking van de andere.</span><span class="sxs-lookup"><span data-stu-id="0e77a-487">Because of defensive aspects of `ts.detrend()`, failure to process one of the variables will not prevent correct processing of the others.</span></span>  

<span data-ttu-id="0e77a-488">De laatste regel van code maakt een pairwise scatterplot.</span><span class="sxs-lookup"><span data-stu-id="0e77a-488">The final line of code creates a pairwise scatterplot.</span></span> <span data-ttu-id="0e77a-489">Na het uitvoeren van de R-code, worden de resultaten van de scatterplot weergegeven in afbeelding 17.</span><span class="sxs-lookup"><span data-stu-id="0e77a-489">After running the R code, the results of the scatterplot are shown in Figure 17.</span></span>

![Pairwise scatterplot van ongedaan trendanalyse en gestandaardiseerde tijdreeks][18]

<span data-ttu-id="0e77a-491">*Afbeelding 17. Pairwise scatterplot van ongedaan trendanalyse en gestandaardiseerde tijdreeks.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-491">*Figure 17. Pairwise scatterplot of de-trended and standardized time series.*</span></span>

<span data-ttu-id="0e77a-492">U kunt deze resultaten aan die wordt weergegeven in afbeelding 16 vergelijken.</span><span class="sxs-lookup"><span data-stu-id="0e77a-492">You can compare these results to those shown in Figure 16.</span></span> <span data-ttu-id="0e77a-493">Met het trendanalyse verwijderd en de variabelen gestandaardiseerd zien we veel minder structuur in de relaties tussen deze variabelen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-493">With the trend removed and the variables standardized, we see a lot less structure in the relationships between these variables.</span></span>

<span data-ttu-id="0e77a-494">De code voor het berekenen van de correlaties als R ccf objecten is als volgt.</span><span class="sxs-lookup"><span data-stu-id="0e77a-494">The code to compute the correlations as R ccf objects is as follows.</span></span>

    ## A function to compute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of the pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute the list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

<span data-ttu-id="0e77a-495">Deze code wordt het logboek wordt weergegeven in afbeelding 18.</span><span class="sxs-lookup"><span data-stu-id="0e77a-495">Running this code produces the log shown in Figure 18.</span></span>

    [ModuleOutput] Loading objects:
    [ModuleOutput]   port1
    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] [[1]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.148 0.358 0.317 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[2]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.395 -0.186 -0.238 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[3]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.059 -0.089 -0.127 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[4]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.140 0.294 0.293 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[5]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.002 -0.074 -0.124 

<span data-ttu-id="0e77a-496">*Afbeelding 18. Lijst met ccf objecten uit de pairwise correlatieanalyse.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-496">*Figure 18. List of ccf objects from the pairwise correlation analysis.*</span></span>

<span data-ttu-id="0e77a-497">Er is een waarde voor correlation voor elke vertraging.</span><span class="sxs-lookup"><span data-stu-id="0e77a-497">There is a correlation value for each lag.</span></span> <span data-ttu-id="0e77a-498">Geen van deze waarden correlatie is groot genoeg zijn om verwaarloosbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="0e77a-498">None of these correlation values is large enough to be significant.</span></span> <span data-ttu-id="0e77a-499">We kunnen daarom sluiten we elke variabele onafhankelijk kunnen model.</span><span class="sxs-lookup"><span data-stu-id="0e77a-499">We can therefore conclude that we can model each variable independently.</span></span>

### <a name="output-a-dataframe"></a><span data-ttu-id="0e77a-500">Een dataframe uitvoer</span><span class="sxs-lookup"><span data-stu-id="0e77a-500">Output a dataframe</span></span>
<span data-ttu-id="0e77a-501">We hebben de pairwise correlaties berekend als een lijst met R ccf objecten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-501">We have computed the pairwise correlations as a list of R ccf objects.</span></span> <span data-ttu-id="0e77a-502">Dit vormt een bits van een probleem als de uitvoerpoort resultaat gegevensset echt een dataframe vereist.</span><span class="sxs-lookup"><span data-stu-id="0e77a-502">This presents a bit of a problem as the Result Dataset output port really requires a dataframe.</span></span> <span data-ttu-id="0e77a-503">Verder kan het object ccf is zelf een lijst en kunt u alleen de waarden in het eerste element van deze lijst, de correlaties op de verschillende lag.</span><span class="sxs-lookup"><span data-stu-id="0e77a-503">Further, the ccf object is itself a list and we want only the values in the first element of this list, the correlations at the various lags.</span></span>

<span data-ttu-id="0e77a-504">De waarden van de vertraging van de volgende code opgehaald uit de lijst met ccf objecten, die zelf lijsten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-504">The following code extracts the lag values from the list of ccf objects, which are themselves lists.</span></span>

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with the row names column and the
    ## correlation data frame and assign the column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## The following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

<span data-ttu-id="0e77a-505">De eerste coderegel iets lastig is en een verklaring waarmee u begrijpt.</span><span class="sxs-lookup"><span data-stu-id="0e77a-505">The first line of code is a bit tricky, and some explanation may help you understand it.</span></span> <span data-ttu-id="0e77a-506">Werken van binnenuit hebben we het volgende:</span><span class="sxs-lookup"><span data-stu-id="0e77a-506">Working from the inside out we have the following:</span></span>

1. <span data-ttu-id="0e77a-507">De '**[[**'operator met het argument'**1**' de vector van correlaties op de lag uit het eerste element van de lijst met ccf objecten geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="0e77a-507">The '**[[**' operator with the argument '**1**' selects the vector of correlations at the lags from the first element of the ccf object list.</span></span>
2. <span data-ttu-id="0e77a-508">De `do.call()` functie is van toepassing de `rbind()` via de elementen van de lijst met de functie wordt door `lapply()`.</span><span class="sxs-lookup"><span data-stu-id="0e77a-508">The `do.call()` function applies the `rbind()` function over the elements of the list returns by `lapply()`.</span></span>
3. <span data-ttu-id="0e77a-509">De `data.frame()` functie koppelt het resultaat geproduceerd door `do.call()` naar een dataframe.</span><span class="sxs-lookup"><span data-stu-id="0e77a-509">The `data.frame()` function coerces the result produced by `do.call()` to a dataframe.</span></span>

<span data-ttu-id="0e77a-510">Houd er rekening mee dat de rijnamen van de in een kolom van de dataframe zijn.</span><span class="sxs-lookup"><span data-stu-id="0e77a-510">Note that the row names are in a column of the dataframe.</span></span> <span data-ttu-id="0e77a-511">In dat geval behoudt de rij doet namen wanneer ze worden uitgevoerd via de [R-Script uitvoeren][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="0e77a-511">Doing so preserves the row names when they are output from the [Execute R Script][execute-r-script].</span></span>

<span data-ttu-id="0e77a-512">De code wordt de uitvoer wordt weergegeven in afbeelding 19 wanneer ik **Visualize** de uitvoer op de poort resultaat gegevensset.</span><span class="sxs-lookup"><span data-stu-id="0e77a-512">Running the code produces the output shown in Figure 19 when I **Visualize** the output at the Result Dataset port.</span></span> <span data-ttu-id="0e77a-513">De rijnamen van de zijn in de eerste kolom zoals bedoeld.</span><span class="sxs-lookup"><span data-stu-id="0e77a-513">The row names are in the first column, as intended.</span></span>

![Uitvoer van de resultaten van de correlatieanalyse][20]

<span data-ttu-id="0e77a-515">*Afbeelding 19. Resultaten de uitvoer van de correlatieanalyse.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-515">*Figure 19. Results output from the correlation analysis.*</span></span>

## <span data-ttu-id="0e77a-516"><a id="seasonalforecasting"></a>Time series-voorbeeld: seizoensgebonden prognose</span><span class="sxs-lookup"><span data-stu-id="0e77a-516"><a id="seasonalforecasting"></a>Time series example: seasonal forecasting</span></span>
<span data-ttu-id="0e77a-517">Onze gegevens is nu in een formulier dat geschikt is voor analyse en we hebben vastgesteld dat er zijn geen belangrijke correlatie tussen de variabelen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-517">Our data is now in a form suitable for analysis, and we have determined there are no significant correlations between the variables.</span></span> <span data-ttu-id="0e77a-518">We gaan en maken van een tijdreeks prognose model.</span><span class="sxs-lookup"><span data-stu-id="0e77a-518">Let's move on and create a time series forecasting model.</span></span> <span data-ttu-id="0e77a-519">Met dit model forecast we Californië melkproductie voor de 12 maanden van 2013.</span><span class="sxs-lookup"><span data-stu-id="0e77a-519">Using this model we will forecast California milk production for the 12 months of 2013.</span></span>

<span data-ttu-id="0e77a-520">Onze prognosemodel heeft twee componenten, een onderdeel van het trendanalyse en een seizoen onderdeel.</span><span class="sxs-lookup"><span data-stu-id="0e77a-520">Our forecasting model will have two components, a trend component and a seasonal component.</span></span> <span data-ttu-id="0e77a-521">De volledige prognose is het product van deze twee componenten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-521">The complete forecast is the product of these two components.</span></span> <span data-ttu-id="0e77a-522">Dit type model staat bekend als een Multiplicatieve model.</span><span class="sxs-lookup"><span data-stu-id="0e77a-522">This type of model is known as a multiplicative model.</span></span> <span data-ttu-id="0e77a-523">Het alternatief is een additieve model.</span><span class="sxs-lookup"><span data-stu-id="0e77a-523">The alternative is an additive model.</span></span> <span data-ttu-id="0e77a-524">We hebben een transformatie logboek al toegepast op de variabelen van belang, waardoor deze analyse tractable.</span><span class="sxs-lookup"><span data-stu-id="0e77a-524">We have already applied a log transformation to the variables of interest, which makes this analysis tractable.</span></span>

<span data-ttu-id="0e77a-525">De volledige R-code voor deze sectie wordt het zip-bestand dat u eerder hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="0e77a-525">The complete R code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="creating-the-dataframe-for-analysis"></a><span data-ttu-id="0e77a-526">Maken van de dataframe voor analyse</span><span class="sxs-lookup"><span data-stu-id="0e77a-526">Creating the dataframe for analysis</span></span>
<span data-ttu-id="0e77a-527">Voeg eerst een **nieuwe** [R-Script uitvoeren] [ execute-r-script] module die u wilt uw experiment.</span><span class="sxs-lookup"><span data-stu-id="0e77a-527">Start by adding a **new** [Execute R Script][execute-r-script] module to your experiment.</span></span> <span data-ttu-id="0e77a-528">Verbinding maken met de **resultaat gegevensset** uitvoer van de bestaande [R-Script uitvoeren] [ execute-r-script] module die u wilt de **Dataset1** invoer van de nieuwe module.</span><span class="sxs-lookup"><span data-stu-id="0e77a-528">Connect the **Result Dataset** output of the existing [Execute R Script][execute-r-script] module to the **Dataset1** input of the new module.</span></span> <span data-ttu-id="0e77a-529">Het resultaat moet er ongeveer als afbeelding 20.</span><span class="sxs-lookup"><span data-stu-id="0e77a-529">The result should look something like Figure 20.</span></span>

![Het experiment met de nieuwe R-Script uitvoeren module toegevoegd][21]

<span data-ttu-id="0e77a-531">*Afbeelding 20. Het experiment met de nieuwe R-Script uitvoeren module toegevoegd.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-531">*Figure 20. The experiment with the new Execute R Script module added.*</span></span>

<span data-ttu-id="0e77a-532">Als met de correlatieanalyse die we zojuist, moeten we een kolom met een POSIXct time series-object toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-532">As with the correlation analysis we just completed, we need to add a column with a POSIXct time series object.</span></span> <span data-ttu-id="0e77a-533">De volgende code wordt hiervoor alleen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-533">The following code will do just this.</span></span>

    # If running in Machine Learning Studio, uncomment the first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

<span data-ttu-id="0e77a-534">Voer deze code en kijk in het logbestand.</span><span class="sxs-lookup"><span data-stu-id="0e77a-534">Run this code and look at the log.</span></span> <span data-ttu-id="0e77a-535">Het resultaat moet eruitzien als afbeelding 21.</span><span class="sxs-lookup"><span data-stu-id="0e77a-535">The result should look like Figure 21.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="0e77a-536">*Afbeelding 21. Een samenvatting van de dataframe.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-536">*Figure 21. A summary of the dataframe.*</span></span>

<span data-ttu-id="0e77a-537">Met dit resultaat zijn we om te beginnen met onze analyse.</span><span class="sxs-lookup"><span data-stu-id="0e77a-537">With this result, we are ready to start our analysis.</span></span>

### <a name="create-a-training-dataset"></a><span data-ttu-id="0e77a-538">Maken van een gegevensset training</span><span class="sxs-lookup"><span data-stu-id="0e77a-538">Create a training dataset</span></span>
<span data-ttu-id="0e77a-539">We moeten een gegevensset met de training maken met de dataframe samengesteld.</span><span class="sxs-lookup"><span data-stu-id="0e77a-539">With the dataframe constructed we need to create a training dataset.</span></span> <span data-ttu-id="0e77a-540">Deze gegevens omvatten alle van de metingen met uitzondering van de afgelopen 12 van het jaar 2013, die onze testgegevensset is.</span><span class="sxs-lookup"><span data-stu-id="0e77a-540">This data will include all of the observations except the last 12, of the year 2013, which is our test dataset.</span></span> <span data-ttu-id="0e77a-541">De volgende code subsets van de dataframe en curve van de variabelen voor de productie- en melkkoeien maakt.</span><span class="sxs-lookup"><span data-stu-id="0e77a-541">The following code subsets the dataframe and creates plots of the dairy production and price variables.</span></span> <span data-ttu-id="0e77a-542">Ik maak vervolgens curve van de vier productie en prijs variabelen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-542">I then create plots of the four production and price variables.</span></span> <span data-ttu-id="0e77a-543">Een anonieme functie wordt gebruikt voor het definiëren van sommige verbetert voor tekengebied en vervolgens de lijst van de andere twee argumenten met herhalen `Map()`.</span><span class="sxs-lookup"><span data-stu-id="0e77a-543">An anonymous function is used to define some augments for plot, and then iterate over the list of the other two arguments with `Map()`.</span></span> <span data-ttu-id="0e77a-544">Als u denkt u zijn die een voor de lus zou hebt gewerkt probleemloos hier, u juist zijn.</span><span class="sxs-lookup"><span data-stu-id="0e77a-544">If you are thinking that a for loop would have worked fine here, you are correct.</span></span> <span data-ttu-id="0e77a-545">Maar aangezien R is een functionele taal ik ben waarin u een functionele benadering.</span><span class="sxs-lookup"><span data-stu-id="0e77a-545">But, since R is a functional language I am showing you a functional approach.</span></span>

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

<span data-ttu-id="0e77a-546">De code wordt de reeks time series van de uitvoer van het R-apparaat weergegeven in afbeelding 22 grafieken.</span><span class="sxs-lookup"><span data-stu-id="0e77a-546">Running the code produces the series of time series plots from the R Device output shown in Figure 22.</span></span> <span data-ttu-id="0e77a-547">Houd er rekening mee dat de tijdas in eenheden van datums nice voordeel van de reeks methode tekenen tijd.</span><span class="sxs-lookup"><span data-stu-id="0e77a-547">Note that the time axis is in units of dates, a nice benefit of the time series plot method.</span></span>

![Eerste dag van time series curve van Californië melkkoeien productie- en -gegevens](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![Tweede van time series curve van Californië melkkoeien productie- en -gegevens](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![Derde van de time series curve van Californië melkkoeien productie- en -gegevens](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![Vierde van time series curve van Californië melkkoeien productie- en -gegevens](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

<span data-ttu-id="0e77a-552">*Afbeelding 22. Time series curve van Californië zuivelproductie en gegevens voor de prijs.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-552">*Figure 22. Time series plots of California dairy production and price data.*</span></span>

### <a name="a-trend-model"></a><span data-ttu-id="0e77a-553">Een model trend</span><span class="sxs-lookup"><span data-stu-id="0e77a-553">A trend model</span></span>
<span data-ttu-id="0e77a-554">Een time series-object en bekijk de gegevens heeft gehad dat het gemaakt, begint om een model trend voor de Californië melk productie-gegevens samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-554">Having created a time series object and having had a look at the data, let's start to construct a trend model for the California milk production data.</span></span> <span data-ttu-id="0e77a-555">We kunnen dit doen met een reeks tijd regressie.</span><span class="sxs-lookup"><span data-stu-id="0e77a-555">We can do this with a time series regression.</span></span> <span data-ttu-id="0e77a-556">Het is echter wissen van de grafiek wordt meer dan een helling moet en om te modelleren nauwkeurig de waargenomen trend in de trainingsgegevens onderscheppen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-556">However, it is clear from the plot that we will need more than a slope and intercept to accurately model the observed trend in the training data.</span></span>

<span data-ttu-id="0e77a-557">Gezien de kleine schaal van de gegevens, ik het model voor de trend in RStudio maken en vervolgens knippen en plakt u de resulterende model in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0e77a-557">Given the small scale of the data, I will build the model for trend in RStudio and then cut and paste the resulting model into Azure Machine Learning.</span></span> <span data-ttu-id="0e77a-558">RStudio biedt een interactieve omgeving voor dit type interactieve analyses.</span><span class="sxs-lookup"><span data-stu-id="0e77a-558">RStudio provides an interactive environment for this type of interactive analysis.</span></span>

<span data-ttu-id="0e77a-559">Als een eerste poging probeer ik een polynomiale regressie met bevoegdheden maximaal 3.</span><span class="sxs-lookup"><span data-stu-id="0e77a-559">As a first attempt, I will try a polynomial regression with powers up to 3.</span></span> <span data-ttu-id="0e77a-560">Er is een echte gevaar voor dit soort modellen te veel aanpassen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-560">There is a real danger of over-fitting these kinds of models.</span></span> <span data-ttu-id="0e77a-561">Daarom is het aanbevolen om te voorkomen dat hoge voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="0e77a-561">Therefore, it is best to avoid high order terms.</span></span> <span data-ttu-id="0e77a-562">De `I()` functie belemmert interpretatie van de inhoud (interpreteert de inhoud, zoals is') en kunt u een letterlijk geïnterpreteerde functie in een regressievergelijking schrijven.</span><span class="sxs-lookup"><span data-stu-id="0e77a-562">The `I()` function inhibits interpretation of the contents (interprets the contents 'as is') and allows you to write a literally interpreted function in a regression equation.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

<span data-ttu-id="0e77a-563">Hiermee wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="0e77a-563">This generates the following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3),
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12667 -0.02730  0.00236  0.02943  0.10586
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.33e+00   1.45e-01   43.60   <2e-16 ***
    ## Time              1.63e-09   1.72e-10    9.47   <2e-16 ***
    ## I(Month.Count^2) -1.71e-06   4.89e-06   -0.35    0.726
    ## I(Month.Count^3) -3.24e-08   1.49e-08   -2.17    0.031 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0418 on 212 degrees of freedom
    ## Multiple R-squared:  0.941,    Adjusted R-squared:  0.94
    ## F-statistic: 1.12e+03 on 3 and 212 DF,  p-value: <2e-16

<span data-ttu-id="0e77a-564">Van P-waarden (Pr (> | t |)) in deze uitvoer kunt zien we dat de gekwadrateerde term geen aanzienlijke wellicht.</span><span class="sxs-lookup"><span data-stu-id="0e77a-564">From P values (Pr(>|t|)) in this output, we can see that the squared term may not be significant.</span></span> <span data-ttu-id="0e77a-565">Ik gebruik de `update()` functie dit model wijzigen door de gekwadrateerde term slepen en neerzetten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-565">I will use the `update()` function to modify this model by dropping the squared term.</span></span>

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

<span data-ttu-id="0e77a-566">Hiermee wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="0e77a-566">This generates the following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12597 -0.02659  0.00185  0.02963  0.10696
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.38e+00   4.07e-02   156.6   <2e-16 ***
    ## Time              1.57e-09   4.32e-11    36.3   <2e-16 ***
    ## I(Month.Count^3) -3.76e-08   2.50e-09   -15.1   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0417 on 213 degrees of freedom
    ## Multiple R-squared:  0.941,  Adjusted R-squared:  0.94
    ## F-statistic: 1.69e+03 on 2 and 213 DF,  p-value: <2e-16

<span data-ttu-id="0e77a-567">Dit ziet er beter.</span><span class="sxs-lookup"><span data-stu-id="0e77a-567">This looks better.</span></span> <span data-ttu-id="0e77a-568">Alle voorwaarden zijn van belang.</span><span class="sxs-lookup"><span data-stu-id="0e77a-568">All of the terms are significant.</span></span> <span data-ttu-id="0e77a-569">De waarde van de 2e-16 is echter een standaardwaarde, en moet niet ernstig te worden genomen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-569">However, the 2e-16 value is a default value, and should not be taken too seriously.</span></span>  

<span data-ttu-id="0e77a-570">Als een test sanity time series tekent van de gegevens van de zuivelproductie Californië we te maken met het trendanalyse curve weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0e77a-570">As a sanity test, let's make a time series plot of the California dairy production data with the trend curve shown.</span></span> <span data-ttu-id="0e77a-571">Ik heb de volgende code toegevoegd in de Azure Machine Learning [R-Script uitvoeren] [ execute-r-script] model (geen RStudio) maken van het model en tekent.</span><span class="sxs-lookup"><span data-stu-id="0e77a-571">I have added the following code in the Azure Machine Learning [Execute R Script][execute-r-script] model (not RStudio) to create the model and make a plot.</span></span> <span data-ttu-id="0e77a-572">Het resultaat wordt weergegeven in afbeelding 23.</span><span class="sxs-lookup"><span data-stu-id="0e77a-572">The result is shown in Figure 23.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![Californië melk productiegegevens met trend model weergegeven](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

<span data-ttu-id="0e77a-574">*Afbeelding 23. Californië melk trend model weergegeven met productiegegevens.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-574">*Figure 23. California milk production data with trend model shown.*</span></span>

<span data-ttu-id="0e77a-575">Het lijkt dat het trendanalyse model past bij de gegevens vrij goed.</span><span class="sxs-lookup"><span data-stu-id="0e77a-575">It looks like the trend model fits the data fairly well.</span></span> <span data-ttu-id="0e77a-576">Verder kan lijkt er niet te worden bewijs van te veel aanpassen zoals oneven wiggles in de curve model.</span><span class="sxs-lookup"><span data-stu-id="0e77a-576">Further, there does not seem to be evidence of over-fitting, such as odd wiggles in the model curve.</span></span>  

### <a name="seasonal-model"></a><span data-ttu-id="0e77a-577">Seizoensgebonden model</span><span class="sxs-lookup"><span data-stu-id="0e77a-577">Seasonal model</span></span>
<span data-ttu-id="0e77a-578">Met een model van de trend in de hand moeten we push op en de seizoensgebonden effecten bevatten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-578">With a trend model in hand, we need to push on and include the seasonal effects.</span></span> <span data-ttu-id="0e77a-579">We gebruiken de maand van het jaar als een dummy-variabele in het lineaire model voor het vastleggen van het effect per maand.</span><span class="sxs-lookup"><span data-stu-id="0e77a-579">We will use the month of the year as a dummy variable in the linear model to capture the month-by-month effect.</span></span> <span data-ttu-id="0e77a-580">Houd er rekening mee dat wanneer u factor variabelen in een model introduceren, het snijpunt moet niet worden berekend.</span><span class="sxs-lookup"><span data-stu-id="0e77a-580">Note that when you introduce factor variables into a model, the intercept must not be computed.</span></span> <span data-ttu-id="0e77a-581">Als u dit doet, wordt de formule te veel is opgegeven en R wordt verwijdert u een van de gewenste factoren maar de term intercept houden.</span><span class="sxs-lookup"><span data-stu-id="0e77a-581">If you do not do this, the formula is over-specified and R will drop one of the desired factors but keep the intercept term.</span></span>

<span data-ttu-id="0e77a-582">Aangezien we een model tevredenheid trend hebben kunnen we gebruiken de `update()` functie de nieuwe voorwaarden toevoegen aan het bestaande model.</span><span class="sxs-lookup"><span data-stu-id="0e77a-582">Since we have a satisfactory trend model we can use the `update()` function to add the new terms to the existing model.</span></span> <span data-ttu-id="0e77a-583">De formule van de update -1 wordt de term intercept neergezet.</span><span class="sxs-lookup"><span data-stu-id="0e77a-583">The -1 in the update formula drops the intercept term.</span></span> <span data-ttu-id="0e77a-584">Als u doorgaat in RStudio momenteel:</span><span class="sxs-lookup"><span data-stu-id="0e77a-584">Continuing in RStudio for the moment:</span></span>

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

<span data-ttu-id="0e77a-585">Hiermee wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="0e77a-585">This generates the following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3) + Month - 1,
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.06879 -0.01693  0.00346  0.01543  0.08726
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## Time              1.57e-09   2.72e-11    57.7   <2e-16 ***
    ## I(Month.Count^3) -3.74e-08   1.57e-09   -23.8   <2e-16 ***
    ## MonthApr          6.40e+00   2.63e-02   243.3   <2e-16 ***
    ## MonthAug          6.38e+00   2.63e-02   242.2   <2e-16 ***
    ## MonthDec          6.38e+00   2.64e-02   241.9   <2e-16 ***
    ## MonthFeb          6.31e+00   2.63e-02   240.1   <2e-16 ***
    ## MonthJan          6.39e+00   2.63e-02   243.1   <2e-16 ***
    ## MonthJul          6.39e+00   2.63e-02   242.6   <2e-16 ***
    ## MonthJun          6.38e+00   2.63e-02   242.4   <2e-16 ***
    ## MonthMar          6.42e+00   2.63e-02   244.2   <2e-16 ***
    ## MonthMay          6.43e+00   2.63e-02   244.3   <2e-16 ***
    ## MonthNov          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## MonthOct          6.37e+00   2.63e-02   241.8   <2e-16 ***
    ## MonthSep          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0263 on 202 degrees of freedom
    ## Multiple R-squared:     1,    Adjusted R-squared:     1
    ## F-statistic: 1.42e+06 on 14 and 202 DF,  p-value: <2e-16

<span data-ttu-id="0e77a-586">We zien dat het model niet langer een term intercept en 12 aanzienlijke maand factoren heeft.</span><span class="sxs-lookup"><span data-stu-id="0e77a-586">We see that the model no longer has an intercept term and has 12 significant month factors.</span></span> <span data-ttu-id="0e77a-587">Dit is precies we wilden om te zien.</span><span class="sxs-lookup"><span data-stu-id="0e77a-587">This is exactly what we wanted to see.</span></span>

<span data-ttu-id="0e77a-588">We maken een andere tijd reeks tekent Californië zuivelproductie gegevens om te zien hoe goed het seizoen model werkt.</span><span class="sxs-lookup"><span data-stu-id="0e77a-588">Let's make another time series plot of the California dairy production data to see how well the seasonal model is working.</span></span> <span data-ttu-id="0e77a-589">Ik heb de volgende code toegevoegd in de Azure Machine Learning [R-Script uitvoeren] [ execute-r-script] maken van het model en tekent.</span><span class="sxs-lookup"><span data-stu-id="0e77a-589">I have added the following code in the Azure Machine Learning [Execute R Script][execute-r-script] to create the model and make a plot.</span></span>

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

<span data-ttu-id="0e77a-590">Deze code in Azure Machine Learning, wordt de grafiek wordt weergegeven in afbeelding 24.</span><span class="sxs-lookup"><span data-stu-id="0e77a-590">Running this code in Azure Machine Learning produces the plot shown in Figure 24.</span></span>

![Californië melkproductie met model inclusief seizoensgebonden effecten](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

<span data-ttu-id="0e77a-592">*Afbeelding 24. Melkproductie Californië met model inclusief seizoensgebonden gevolgen.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-592">*Figure 24. California milk production with model including seasonal effects.*</span></span>

<span data-ttu-id="0e77a-593">De aanpassen aan de gegevens weergegeven in afbeelding 24 is in plaats van te bevorderen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-593">The fit to the data shown in Figure 24 is rather encouraging.</span></span> <span data-ttu-id="0e77a-594">Zowel het trendanalyse en het seizoen effect (maandelijks variatie) Zoek redelijke.</span><span class="sxs-lookup"><span data-stu-id="0e77a-594">Both the trend and the seasonal effect (monthly variation) look reasonable.</span></span>

<span data-ttu-id="0e77a-595">Als een nieuwe controle uit op het model, gaan we hebben een overzicht van de verschillen opgeven.</span><span class="sxs-lookup"><span data-stu-id="0e77a-595">As another check on our model, let's have a look at the residuals.</span></span> <span data-ttu-id="0e77a-596">De volgende code berekent de voorspelde waarden uit onze twee modellen, berekent de verschillen opgeven voor het seizoen model en vervolgens deze verschillen opgeven voor de trainingsgegevens worden uitgezet.</span><span class="sxs-lookup"><span data-stu-id="0e77a-596">The following code computes the predicted values from our two models, computes the residuals for the seasonal model, and then plots these residuals for the training data.</span></span>

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot the residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

<span data-ttu-id="0e77a-597">De resterende grafiek wordt weergegeven in afbeelding 25.</span><span class="sxs-lookup"><span data-stu-id="0e77a-597">The residual plot is shown in Figure 25.</span></span>

![Verschillen van het seizoen model voor de trainingsgegevens opgeven](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

<span data-ttu-id="0e77a-599">*Afbeelding 25. Als u dit van het seizoen model voor de trainingsgegevens.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-599">*Figure 25. Residuals of the seasonal model for the training data.*</span></span>

<span data-ttu-id="0e77a-600">Deze verschillen opgeven zoeken redelijke.</span><span class="sxs-lookup"><span data-stu-id="0e77a-600">These residuals look reasonable.</span></span> <span data-ttu-id="0e77a-601">Er is geen specifieke structuur, met uitzondering van het effect van de recessie 2008-2009, die het model wordt geen rekening gehouden met name goed.</span><span class="sxs-lookup"><span data-stu-id="0e77a-601">There is no particular structure, except the effect of the 2008-2009 recession, which our model does not account for particularly well.</span></span>

<span data-ttu-id="0e77a-602">De grafiek wordt weergegeven in afbeelding 25 is nuttig voor het detecteren van alle tijdsafhankelijke patronen in de dit.</span><span class="sxs-lookup"><span data-stu-id="0e77a-602">The plot shown in Figure 25 is useful for detecting any time-dependent patterns in the residuals.</span></span> <span data-ttu-id="0e77a-603">De expliciete benadering van computer- en uitzetten van de ik gebruikt dit wordt de verschillen opgeven in volgorde van de tijd op de grafiek geplaatst.</span><span class="sxs-lookup"><span data-stu-id="0e77a-603">The explicit approach of computing and plotting the residuals I used places the residuals in time order on the plot.</span></span> <span data-ttu-id="0e77a-604">Als, aan de andere kant ik had uitgezet `milk.lm$residuals`, de grafiek niet zouden zijn in volgorde van de tijd.</span><span class="sxs-lookup"><span data-stu-id="0e77a-604">If, on the other hand, I had plotted `milk.lm$residuals`, the plot would not have been in time order.</span></span>

<span data-ttu-id="0e77a-605">U kunt ook `plot.lm()` voor het produceren van een reeks diagnostische waarnemingspunten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-605">You can also use `plot.lm()` to produce a series of diagnostic plots.</span></span>

    ## Show the diagnostic plots for the model
    plot(milk.lm2, ask = FALSE)

<span data-ttu-id="0e77a-606">Deze code wordt een reeks diagnostische waarnemingspunten wordt weergegeven in afbeelding 26 geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="0e77a-606">This code produces a series of diagnostic plots shown in Figure 26.</span></span>

![Eerste dag van diagnostische waarnemingspunten voor het seizoen model](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Tweede van diagnostische waarnemingspunten voor het seizoen model](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Derde van diagnostische waarnemingspunten voor het seizoen model](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Vierde van diagnostische waarnemingspunten voor het seizoen model](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

<span data-ttu-id="0e77a-611">*Afbeelding 26. Diagnose worden uitgezet voor het seizoen model.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-611">*Figure 26. Diagnostic plots for the seasonal model.*</span></span>

<span data-ttu-id="0e77a-612">Er zijn een aantal maximaal invloedrijke punten in deze waarnemingspunten, maar niets geweldige opleveren geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="0e77a-612">There are a few highly influential points identified in these plots, but nothing to cause great concern.</span></span> <span data-ttu-id="0e77a-613">Verder kan kunnen we zien van het tekengebied normaal Q-Q dat de dit zich dicht bij normaal gedistribueerd, belangrijke verondersteld voor lineaire modellen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-613">Further, we can see from the Normal Q-Q plot that the residuals are close to normally distributed, an important assumption for linear models.</span></span>

### <a name="forecasting-and-model-evaluation"></a><span data-ttu-id="0e77a-614">Prognosemodel en model evalueren</span><span class="sxs-lookup"><span data-stu-id="0e77a-614">Forecasting and model evaluation</span></span>
<span data-ttu-id="0e77a-615">Er is slechts één ding doen om het voorbeeld te voltooien.</span><span class="sxs-lookup"><span data-stu-id="0e77a-615">There is just one more thing to do to complete our example.</span></span> <span data-ttu-id="0e77a-616">We moeten prognoses berekenen en de fout op basis van de werkelijke gegevens te meten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-616">We need to compute forecasts and measure the error against the actual data.</span></span> <span data-ttu-id="0e77a-617">Onze prognose worden voor de 12 maanden van 2013.</span><span class="sxs-lookup"><span data-stu-id="0e77a-617">Our forecast will be for the 12 months of 2013.</span></span> <span data-ttu-id="0e77a-618">We kunt een meting fout voor deze prognose voor de werkelijke gegevens die geen deel uitmaakt van onze gegevensset training berekenen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-618">We can compute an error measure for this forecast to the actual data that is not part of our training dataset.</span></span> <span data-ttu-id="0e77a-619">Daarnaast kunnen we de prestaties van de 18 jaar trainingsgegevens met de 12 maanden van testgegevens vergelijken.</span><span class="sxs-lookup"><span data-stu-id="0e77a-619">Additionally, we can compare performance on the 18 years of training data to the 12 months of test data.</span></span>  

<span data-ttu-id="0e77a-620">Een aantal metrische gegevens worden gebruikt voor het meten van de prestaties van de time series-modellen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-620">A number of metrics are used to measure the performance of time series models.</span></span> <span data-ttu-id="0e77a-621">In ons geval gebruiken we de root mean vierkant (RMS)-fout.</span><span class="sxs-lookup"><span data-stu-id="0e77a-621">In our case we will use the root mean square (RMS) error.</span></span> <span data-ttu-id="0e77a-622">De volgende functie berekent de RMS-fout tussen twee reeksen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-622">The following function computes the RMS error between two series.</span></span>  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function to compute the RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments to function RMS.error of wrong type encountered",
                    "ERROR: Input vector to function RMS.error is too short",
                    "ERROR: Input vectors to function RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check the arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate the values, else just copy
      if(is.log) {
        tryCatch( {
          temp1 <- exp(series1)
          temp2 <- exp(series2) },
          error = function(e){warning(messages[4]); NA}
        )
      } else {
        temp1 <- series1
        temp2 <- series2
      }

     ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute the RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

<span data-ttu-id="0e77a-623">Net als bij de `log.transform()` functie in de sectie "Waarde transformaties besproken" Er is zeer veel fout controleren en uitzondering code voor herstel in deze functie.</span><span class="sxs-lookup"><span data-stu-id="0e77a-623">As with the `log.transform()` function we discussed in the "Value transformations" section, there is quite a lot of error checking and exception recovery code in this function.</span></span> <span data-ttu-id="0e77a-624">De principes werkzaam zijn hetzelfde.</span><span class="sxs-lookup"><span data-stu-id="0e77a-624">The principles employed are the same.</span></span> <span data-ttu-id="0e77a-625">Het werk wordt uitgevoerd op twee plaatsen die zijn ingepakt `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="0e77a-625">The work is done in two places wrapped in `tryCatch()`.</span></span> <span data-ttu-id="0e77a-626">De tijdreeks zijn eerst exponentiated, omdat we hebt gewerkt met de logboeken van de waarden.</span><span class="sxs-lookup"><span data-stu-id="0e77a-626">First, the time series are exponentiated, since we have been working with the logs of the values.</span></span> <span data-ttu-id="0e77a-627">Ten tweede wordt de werkelijke RMS-fout berekend.</span><span class="sxs-lookup"><span data-stu-id="0e77a-627">Second, the actual RMS error is computed.</span></span>  

<span data-ttu-id="0e77a-628">Uitgerust met een functie voor het meten van de RMS-fout, gaan we bouwen en uitvoeren van een dataframe met de RMS-fouten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-628">Equipped with a function to measure the RMS error, let's build and output a dataframe containing the RMS errors.</span></span> <span data-ttu-id="0e77a-629">Nemen we voorwaarden voor het trendanalyse model alleen en het model voltooid met seizoensgebonden factoren.</span><span class="sxs-lookup"><span data-stu-id="0e77a-629">We will include terms for the trend model alone and the complete model with seasonal factors.</span></span> <span data-ttu-id="0e77a-630">De volgende code wordt de taak met behulp van de twee lineaire modellen die we hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0e77a-630">The following code does the job by using the two linear models we have constructed.</span></span>

    ## Compute the RMS error in a dataframe
    ## Include the row names in the first column so they will
    ## appear in the output of the Execute R Script
    RMS.df  <-  data.frame(
    rowNames = c("Trend Model", "Seasonal Model"),
      Traing = c(
      RMS.error(predict1[1:216], cadairydata$Milk.Prod[1:216]),
      RMS.error(predict2[1:216], cadairydata$Milk.Prod[1:216])),
      Forecast = c(
        RMS.error(predict1[217:228], cadairydata$Milk.Prod[217:228]),
        RMS.error(predict2[217:228], cadairydata$Milk.Prod[217:228]))
    )
    RMS.df

    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

<span data-ttu-id="0e77a-631">Deze code wordt de uitvoer wordt weergegeven in afbeelding 27 op de uitvoerpoort resultaat gegevensset.</span><span class="sxs-lookup"><span data-stu-id="0e77a-631">Running this code produces the output shown in Figure 27 at the Result Dataset output port.</span></span>

![Vergelijking van RMS-fouten voor de modellen][26]

<span data-ttu-id="0e77a-633">*Afbeelding 27. Vergelijking van RMS-fouten voor de modellen.*</span><span class="sxs-lookup"><span data-stu-id="0e77a-633">*Figure 27. Comparison of RMS errors for the models.*</span></span>

<span data-ttu-id="0e77a-634">Van deze resultaten ziet u dat de seizoensgebonden factoren toe te voegen aan het model de RMS-fout aanzienlijk vermindert.</span><span class="sxs-lookup"><span data-stu-id="0e77a-634">From these results, we see that adding the seasonal factors to the model reduces the RMS error significantly.</span></span> <span data-ttu-id="0e77a-635">De RMS-fout voor de trainingsgegevens is geen te verrassing een bit kleiner is dan voor de prognose.</span><span class="sxs-lookup"><span data-stu-id="0e77a-635">Not too surprisingly, the RMS error for the training data is a bit less than for the forecast.</span></span>

## <span data-ttu-id="0e77a-636"><a id="appendixa"></a>BIJLAGE A:-Handleiding voor het RStudio</span><span class="sxs-lookup"><span data-stu-id="0e77a-636"><a id="appendixa"></a>APPENDIX A: Guide to RStudio</span></span>
<span data-ttu-id="0e77a-637">RStudio heel goed wordt gedocumenteerd, zodat in deze bijlage ik enkele koppelingen naar de sleutel secties van de documentatie voor RStudio zodat u op weg bieden.</span><span class="sxs-lookup"><span data-stu-id="0e77a-637">RStudio is quite well documented, so in this appendix I will provide some links to the key sections of the RStudio documentation to get you started.</span></span>

1. <span data-ttu-id="0e77a-638">Projecten maken</span><span class="sxs-lookup"><span data-stu-id="0e77a-638">Creating projects</span></span>
   
   <span data-ttu-id="0e77a-639">U kunt ordenen en beheren van uw R-code in de projecten via RStudio.</span><span class="sxs-lookup"><span data-stu-id="0e77a-639">You can organize and manage your R code into projects by using RStudio.</span></span> <span data-ttu-id="0e77a-640">De documentatie die gebruikmaakt van de projecten kan worden gevonden op https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span><span class="sxs-lookup"><span data-stu-id="0e77a-640">The documentation that uses projects can be found at https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span></span>
   
   <span data-ttu-id="0e77a-641">Ik het beste als volgt uit te voeren en maak een project voor de R-codevoorbeelden in dit document.</span><span class="sxs-lookup"><span data-stu-id="0e77a-641">I recommend that you follow these directions and create a project for the R code examples in this document.</span></span>  
2. <span data-ttu-id="0e77a-642">Bewerken en het uitvoeren van R-code</span><span class="sxs-lookup"><span data-stu-id="0e77a-642">Editing and executing R code</span></span>
   
   <span data-ttu-id="0e77a-643">RStudio biedt een geïntegreerde omgeving voor het bewerken en R-code wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0e77a-643">RStudio provides an integrated environment for editing and executing R code.</span></span> <span data-ttu-id="0e77a-644">Documentatie vindt u op https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span><span class="sxs-lookup"><span data-stu-id="0e77a-644">Documentation can be found at https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span></span>
3. <span data-ttu-id="0e77a-645">Foutopsporing</span><span class="sxs-lookup"><span data-stu-id="0e77a-645">Debugging</span></span>
   
   <span data-ttu-id="0e77a-646">RStudio omvat krachtige mogelijkheden voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="0e77a-646">RStudio includes powerful debugging capabilities.</span></span> <span data-ttu-id="0e77a-647">Documentatie voor deze functies is op https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span><span class="sxs-lookup"><span data-stu-id="0e77a-647">Documentation for these features is at https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span></span>
   
   <span data-ttu-id="0e77a-648">De onderbrekingspunt voor probleemoplossing functies zijn tijdens https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting gedocumenteerd.</span><span class="sxs-lookup"><span data-stu-id="0e77a-648">The breakpoint troubleshooting features are documented at https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span></span>

## <span data-ttu-id="0e77a-649"><a id="appendixb"></a>BIJLAGE B: Lees hier meer over</span><span class="sxs-lookup"><span data-stu-id="0e77a-649"><a id="appendixb"></a>APPENDIX B: Further reading</span></span>
<span data-ttu-id="0e77a-650">Deze R programming zelfstudie bevat informatie over de basisprincipes van wat u moet de taal R gebruiken met Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="0e77a-650">This R programming tutorial covers the basics of what you need to use the R language with Azure Machine Learning Studio.</span></span> <span data-ttu-id="0e77a-651">Als u niet bekend met R bent, zijn twee inleidingen beschikbaar op CRAN:</span><span class="sxs-lookup"><span data-stu-id="0e77a-651">If you are not familiar with R, two introductions are available on CRAN:</span></span>

* <span data-ttu-id="0e77a-652">R voor beginnende gebruikers door Emmanuel Paradis is een goede plaats om te beginnen bij http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span><span class="sxs-lookup"><span data-stu-id="0e77a-652">R for Beginners by Emmanuel Paradis is a good place to start at http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span></span>  
* <span data-ttu-id="0e77a-653">Een inleiding tot R door W. N.</span><span class="sxs-lookup"><span data-stu-id="0e77a-653">An Introduction to R by W. N.</span></span> <span data-ttu-id="0e77a-654">Venables et.</span><span class="sxs-lookup"><span data-stu-id="0e77a-654">Venables et.</span></span> <span data-ttu-id="0e77a-655">al.</span><span class="sxs-lookup"><span data-stu-id="0e77a-655">al.</span></span> <span data-ttu-id="0e77a-656">in iets meer diepte op http://cran.r-project.org/doc/manuals/R-intro.html gaan.</span><span class="sxs-lookup"><span data-stu-id="0e77a-656">goes into a bit more depth, at http://cran.r-project.org/doc/manuals/R-intro.html.</span></span>

<span data-ttu-id="0e77a-657">Er zijn veel books op R waarmee u aan de slag kunt.</span><span class="sxs-lookup"><span data-stu-id="0e77a-657">There are many books on R that can help you get started.</span></span> <span data-ttu-id="0e77a-658">Hier volgen enkele die ik handig:</span><span class="sxs-lookup"><span data-stu-id="0e77a-658">Here are a few I find useful:</span></span>

* <span data-ttu-id="0e77a-659">De illustratie van R programmeren: een rondleiding van statistische softwareontwerp door Norman Matloff is een uitstekende inleiding tot programmering in R.</span><span class="sxs-lookup"><span data-stu-id="0e77a-659">The Art of R Programming: A Tour of Statistical Software Design by Norman Matloff is an excellent introduction to programming in R.</span></span>  
* <span data-ttu-id="0e77a-660">R Cookbook door Paul Teetor biedt een benadering van het probleem en oplossing voor het gebruik van R.</span><span class="sxs-lookup"><span data-stu-id="0e77a-660">R Cookbook by Paul Teetor provides a problem and solution approach to using R.</span></span>  
* <span data-ttu-id="0e77a-661">R in actie door Robert Kabacoff is een ander nuttig inleidende rapport.</span><span class="sxs-lookup"><span data-stu-id="0e77a-661">R in Action by Robert Kabacoff is another useful introductory book.</span></span> <span data-ttu-id="0e77a-662">De aanvullende snelle R-website is een nuttig resource op http://www.statmethods.net/.</span><span class="sxs-lookup"><span data-stu-id="0e77a-662">The companion Quick R website is a useful resource at http://www.statmethods.net/.</span></span>
* <span data-ttu-id="0e77a-663">R Inferno door Patrick Burns is een verrassend grappige adresboek dat met een aantal lastig en moeilijk onderwerpen die u tegenkomen werkt kunt bij het programmeren in R. Het rapport is beschikbaar voor het vrije op http://www.burns-stat.com/documents/books/the-r-inferno/.</span><span class="sxs-lookup"><span data-stu-id="0e77a-663">R Inferno by Patrick Burns is a surprisingly humorous book that deals with a number of tricky and difficult topics that can be encountered when programming in R. The book is available for free at http://www.burns-stat.com/documents/books/the-r-inferno/.</span></span>
* <span data-ttu-id="0e77a-664">Als u een diepgaand in geavanceerde onderwerpen in R wilt, hebt u een overzicht van het adresboek Geavanceerd R door Hadley Wickham.</span><span class="sxs-lookup"><span data-stu-id="0e77a-664">If you want a deep dive into advanced topics in R, have a look at the book Advanced R by Hadley Wickham.</span></span> <span data-ttu-id="0e77a-665">De online versie van deze handleiding is beschikbaar voor het vrije op http://adv-r.had.co.nz/.</span><span class="sxs-lookup"><span data-stu-id="0e77a-665">The online version of this book is available for free at http://adv-r.had.co.nz/.</span></span>

<span data-ttu-id="0e77a-666">Een lijst van R time series-pakketten kunt u vinden in de taakweergave CRAN voor analyse van reeks: http://cran.r-project.org/web/views/TimeSeries.html.</span><span class="sxs-lookup"><span data-stu-id="0e77a-666">A catalogue of R time series packages can be found in the CRAN Task View for time series analysis: http://cran.r-project.org/web/views/TimeSeries.html.</span></span> <span data-ttu-id="0e77a-667">Voor informatie over specifieke tijd reeks object pakketten, moet u de documentatie voor het desbetreffende pakket verwijzen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-667">For information on specific time series object packages, you should refer to the documentation for that package.</span></span>

<span data-ttu-id="0e77a-668">Het rapport inleidende Time Series met R door Paul Cowpertwait en Andrew Metcalfe bevat een inleiding tot R gebruiken voor analyse van reeks.</span><span class="sxs-lookup"><span data-stu-id="0e77a-668">The book Introductory Time Series with R by Paul Cowpertwait and Andrew Metcalfe provides an introduction to using R for time series analysis.</span></span> <span data-ttu-id="0e77a-669">Veel meer theoretische teksten bevatten R voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="0e77a-669">Many more theoretical texts provide R examples.</span></span>

<span data-ttu-id="0e77a-670">Sommige geweldige internetbronnen:</span><span class="sxs-lookup"><span data-stu-id="0e77a-670">Some great internet resources:</span></span>

* <span data-ttu-id="0e77a-671">DataCamp: DataCamp leert R de deur van uw browser met video uitkomsten en codering oefeningen.</span><span class="sxs-lookup"><span data-stu-id="0e77a-671">DataCamp: DataCamp teaches R in the comfort of your browser with video lessons and coding exercises.</span></span> <span data-ttu-id="0e77a-672">Er zijn interactieve zelfstudies voor de meest recente R technieken en pakketten.</span><span class="sxs-lookup"><span data-stu-id="0e77a-672">There are interactive tutorials on the latest R techniques and packages.</span></span> <span data-ttu-id="0e77a-673">Bij https://www.datacamp.com/courses/introduction-to-r worden gehouden met de gratis interactieve R-zelfstudie</span><span class="sxs-lookup"><span data-stu-id="0e77a-673">Take the free interactive R tutorial at https://www.datacamp.com/courses/introduction-to-r</span></span>
* <span data-ttu-id="0e77a-674">Een handleiding op aan de slag met R van Programiz https://www.programiz.com/r-programming</span><span class="sxs-lookup"><span data-stu-id="0e77a-674">A guide on Getting started with R from Programiz https://www.programiz.com/r-programming</span></span>
* <span data-ttu-id="0e77a-675">Een snelle zelfstudie van R door Kelly Black van Clarkson universiteit http://www.cyclismo.org/tutorial/R/</span><span class="sxs-lookup"><span data-stu-id="0e77a-675">A quick R tutorial by Kelly Black from Clarkson University http://www.cyclismo.org/tutorial/R/</span></span>
* <span data-ttu-id="0e77a-676">60 + R-resources die wordt vermeld op http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span><span class="sxs-lookup"><span data-stu-id="0e77a-676">60+ R resources listed at http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span></span>

<!--Image references-->
[1]: ./media/machine-learning-r-quickstart/fig1.png
[2]: ./media/machine-learning-r-quickstart/fig2.png
[3]: ./media/machine-learning-r-quickstart/fig3.png
[4]: ./media/machine-learning-r-quickstart/fig4.png
[5]: ./media/machine-learning-r-quickstart/fig5.png
[6]: ./media/machine-learning-r-quickstart/fig6.png
[7]: ./media/machine-learning-r-quickstart/fig7.png
[8]: ./media/machine-learning-r-quickstart/fig8.png
[9]: ./media/machine-learning-r-quickstart/fig9.png
[10]: ./media/machine-learning-r-quickstart/fig10.png
[11]: ./media/machine-learning-r-quickstart/fig11.png
[12]: ./media/machine-learning-r-quickstart/fig12.png
[13]: ./media/machine-learning-r-quickstart/fig13.png
[14]: ./media/machine-learning-r-quickstart/fig14.png
[15]: ./media/machine-learning-r-quickstart/fig15.png
[16]: ./media/machine-learning-r-quickstart/fig16.png
[17]: ./media/machine-learning-r-quickstart/fig17.png
[18]: ./media/machine-learning-r-quickstart/fig18.png
[19]: ./media/machine-learning-r-quickstart/fig19.png
[20]: ./media/machine-learning-r-quickstart/fig20.png
[21]: ./media/machine-learning-r-quickstart/fig21.png
[22]: ./media/machine-learning-r-quickstart/fig22.png

[26]: ./media/machine-learning-r-quickstart/fig26.png

<!--links-->
[appendixa]: #appendixa
[download]: https://azurebigdatatutorials.blob.core.windows.net/rquickstart/RFiles.zip


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
