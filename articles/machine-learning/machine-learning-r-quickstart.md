---
title: zelfstudie voor R-taal voor Machine Learning aaaQuickstart | Microsoft Docs
description: Deze zelfstudie tooget gestart snel Hallo R taal gebruiken met Azure Machine Learning Studio toocreate een prognosemodel oplossing programming R gebruiken.
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
ms.openlocfilehash: 9995f8728f4d7bf9a5c15412015e4cf769cdac96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-tutorial-for-hello-r-programming-language-for-azure-machine-learning"></a><span data-ttu-id="d9091-104">Quick Start-zelfstudie voor Hallo R programmeertaal voor Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d9091-104">Quickstart tutorial for hello R programming language for Azure Machine Learning</span></span>

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a><span data-ttu-id="d9091-105">Inleiding</span><span class="sxs-lookup"><span data-stu-id="d9091-105">Introduction</span></span>
<span data-ttu-id="d9091-106">Deze zelfstudie snel aan de slag kunt u snel starten Azure Machine Learning met behulp van de programmeertaal Hallo R uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="d9091-106">This quickstart tutorial helps you quickly start extending Azure Machine Learning by using hello R programming language.</span></span> <span data-ttu-id="d9091-107">Volg deze zelfstudie toocreate programming R, testen en R-code in Azure Machine Learning uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d9091-107">Follow this R programming tutorial toocreate, test and execute R code within Azure Machine Learning.</span></span> <span data-ttu-id="d9091-108">Als u de zelfstudie doorloopt, maakt u een volledige prognoses oplossing met behulp van Hallo R taal in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d9091-108">As you work through tutorial, you will create a complete forecasting solution by using hello R language in Azure Machine Learning.</span></span>  

<span data-ttu-id="d9091-109">Microsoft Azure Machine Learning bevat veel krachtige machine learning en manipulatie modules.</span><span class="sxs-lookup"><span data-stu-id="d9091-109">Microsoft Azure Machine Learning contains many powerful machine learning and data manipulation modules.</span></span> <span data-ttu-id="d9091-110">Hallo krachtige R taal heeft als Hallo lingua franca van analytics zijn beschreven.</span><span class="sxs-lookup"><span data-stu-id="d9091-110">hello powerful R language has been described as hello lingua franca of analytics.</span></span> <span data-ttu-id="d9091-111">Manipulatie analytics en gegevens in Azure Machine Learning kan worden uitgebreid met R. Deze combinatie biedt Hallo schaalbaarheid en het gemak van de implementatie van Azure Machine Learning met Hallo flexibiliteit en grondige analyse van R.</span><span class="sxs-lookup"><span data-stu-id="d9091-111">Happily, analytics and data manipulation in Azure Machine Learning can be extended by using R. This combination provides hello scalability and ease of deployment of Azure Machine Learning with hello flexibility and deep analytics of R.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-hello-dataset"></a><span data-ttu-id="d9091-112">Prognose en Hallo gegevensset</span><span class="sxs-lookup"><span data-stu-id="d9091-112">Forecasting and hello dataset</span></span>
<span data-ttu-id="d9091-113">Prognose is veel werknemers en wel handig analytische methode.</span><span class="sxs-lookup"><span data-stu-id="d9091-113">Forecasting is a widely employed and quite useful analytical method.</span></span> <span data-ttu-id="d9091-114">Algemeen gebruik bereik van het voorspellen van de verkoop van seizoensgebonden items, optimaal voorraadbeheer, toopredicting macro-economische variabelen te bepalen.</span><span class="sxs-lookup"><span data-stu-id="d9091-114">Common uses range from predicting sales of seasonal items, determining optimal inventory levels, toopredicting macroeconomic variables.</span></span> <span data-ttu-id="d9091-115">Prognose gewoonlijk wordt uitgevoerd met time series-modellen.</span><span class="sxs-lookup"><span data-stu-id="d9091-115">Forecasting is typically done with time series models.</span></span>

<span data-ttu-id="d9091-116">Reeks tijdgegevens zijn gegevens waarin Hallo waarden een tijdsindex hebben.</span><span class="sxs-lookup"><span data-stu-id="d9091-116">Time series data is data in which hello values have a time index.</span></span> <span data-ttu-id="d9091-117">Hallo tijdsindex worden regelmatig, bijvoorbeeld elke maand of elke minuut of onregelmatig.</span><span class="sxs-lookup"><span data-stu-id="d9091-117">hello time index can be regular, e.g. every month or every minute, or irregular.</span></span> <span data-ttu-id="d9091-118">Een tijdreeksmodel is gebaseerd op een reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="d9091-118">A time series model is based on time series data.</span></span> <span data-ttu-id="d9091-119">Hallo R programmeertaal bevat een flexibele framework en de uitgebreide analytics voor tijd reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="d9091-119">hello R programming language contains a flexible framework and extensive analytics for time series data.</span></span>

<span data-ttu-id="d9091-120">In deze snelstartgids wordt worden werken met Californië zuivelproductie en prijzen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="d9091-120">In this quickstart guide we will be working with California dairy production and pricing data.</span></span> <span data-ttu-id="d9091-121">Deze gegevens omvatten maandelijkse informatie op Hallo productie van verschillende producten en Hallo prijs van melkvet, een benchmark basisproduct.</span><span class="sxs-lookup"><span data-stu-id="d9091-121">This data includes monthly information on hello production of several dairy products and hello price of milk fat, a benchmark commodity.</span></span>

<span data-ttu-id="d9091-122">Hallo-gegevens in dit artikel, samen met het R-scripts gebruikt kunnen worden [hier gedownload][download].</span><span class="sxs-lookup"><span data-stu-id="d9091-122">hello data used in this article, along with R scripts, can be [downloaded here][download].</span></span> <span data-ttu-id="d9091-123">Deze gegevens is oorspronkelijk gemaakt van gegevens van Hallo universiteit van Wisconsin op http://future.aae.wisc.edu/tab/production.html.</span><span class="sxs-lookup"><span data-stu-id="d9091-123">This data was originally synthesized from information available from hello University of Wisconsin at http://future.aae.wisc.edu/tab/production.html.</span></span>

### <a name="organization"></a><span data-ttu-id="d9091-124">Organisatie</span><span class="sxs-lookup"><span data-stu-id="d9091-124">Organization</span></span>
<span data-ttu-id="d9091-125">We zullen verschillende stappen doorlopen terwijl u leert hoe toocreate, testen en analytics en data manipulatie R-code in hello Azure Machine Learning-omgeving uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d9091-125">We will progress through several steps as you learn how toocreate, test and execute analytics and data manipulation R code in hello Azure Machine Learning environment.</span></span>  

* <span data-ttu-id="d9091-126">Eerst verkennen we Hallo grondbeginselen van het gebruik van Hallo R taal in hello Azure Machine Learning Studio-omgeving.</span><span class="sxs-lookup"><span data-stu-id="d9091-126">First we will explore hello basics of using hello R language in hello Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="d9091-127">Vervolgens wordt de voortgang toodiscussing verschillende aspecten van i/o voor gegevens, R-code en afbeeldingen in hello Azure Machine Learning-omgeving.</span><span class="sxs-lookup"><span data-stu-id="d9091-127">Then we progress toodiscussing various aspects of I/O for data, R code and graphics in hello Azure Machine Learning environment.</span></span>
* <span data-ttu-id="d9091-128">We wordt vervolgens Hallo eerste deel van onze prognoses oplossing maken door het maken van code voor het reinigen van gegevens en transformatie.</span><span class="sxs-lookup"><span data-stu-id="d9091-128">We will then construct hello first part of our forecasting solution by creating code for data cleaning and transformation.</span></span>
* <span data-ttu-id="d9091-129">Met onze gegevens voorbereid wordt uitgevoerd, er een analyse van Hallo correlatie tussen verschillende Hallo variabelen in onze gegevensset.</span><span class="sxs-lookup"><span data-stu-id="d9091-129">With our data prepared we will perform an analysis of hello correlations between several of hello variables in our dataset.</span></span>
* <span data-ttu-id="d9091-130">We gaan ten slotte een seizoen prognoses tijdreeksmodel voor maken.</span><span class="sxs-lookup"><span data-stu-id="d9091-130">Finally, we will create a seasonal time series forecasting model for milk production.</span></span>

## <span data-ttu-id="d9091-131"><a id="mlstudio"></a>Interactie met R-taal in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="d9091-131"><a id="mlstudio"></a>Interact with R language in Machine Learning Studio</span></span>
<span data-ttu-id="d9091-132">Deze sectie leert u enkele van de basisprincipes van de interactie met de programmeertaal Hallo R in Hallo Machine Learning Studio-omgeving.</span><span class="sxs-lookup"><span data-stu-id="d9091-132">This section takes you through some basics of interacting with hello R programming language in hello Machine Learning Studio environment.</span></span> <span data-ttu-id="d9091-133">Hallo R taal biedt een krachtig hulpprogramma toocreate aangepast analytics en data manipulatie modules binnen hello Azure Machine Learning-omgeving.</span><span class="sxs-lookup"><span data-stu-id="d9091-133">hello R language provides a powerful tool toocreate customized analytics and data manipulation modules within hello Azure Machine Learning environment.</span></span>

<span data-ttu-id="d9091-134">Ik gebruik RStudio toodevelop, testen en foutopsporing R-code op kleine schaal.</span><span class="sxs-lookup"><span data-stu-id="d9091-134">I will use RStudio toodevelop, test and debug R code on a small scale.</span></span> <span data-ttu-id="d9091-135">Deze code wordt vervolgens knippen en plakken in een [R-Script uitvoeren] [ execute-r-script] -module in Machine Learning Studio gereed toorun.</span><span class="sxs-lookup"><span data-stu-id="d9091-135">This code is then cut and paste into an [Execute R Script][execute-r-script] module in Machine Learning Studio ready toorun.</span></span>  

### <a name="hello-execute-r-script-module"></a><span data-ttu-id="d9091-136">Hallo-module voor R-Script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="d9091-136">hello Execute R Script module</span></span>
<span data-ttu-id="d9091-137">In Machine Learning Studio R scripts worden uitgevoerd binnen Hallo [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="d9091-137">Within Machine Learning Studio, R scripts are run within hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="d9091-138">Een voorbeeld van Hallo [R-Script uitvoeren] [ execute-r-script] module in Machine Learning Studio wordt weergegeven in afbeelding 1.</span><span class="sxs-lookup"><span data-stu-id="d9091-138">An example of hello [Execute R Script][execute-r-script] module in Machine Learning Studio is shown in Figure 1.</span></span>

 ![R programmeertaal: Hallo R-Script niet uitvoeren-module is geselecteerd in Machine Learning Studio][1]

<span data-ttu-id="d9091-140">*Afbeelding 1. Hallo Machine Learning Studio-omgeving met Hallo R-Script niet uitvoeren-module is geselecteerd.*</span><span class="sxs-lookup"><span data-stu-id="d9091-140">*Figure 1. hello Machine Learning Studio environment showing hello Execute R Script module selected.*</span></span>

<span data-ttu-id="d9091-141">TooFigure 1 verwijst, bekijken we enkele van de belangrijkste onderdelen van Machine Learning Studio-omgeving voor het werken met Hallo HALLO hallo [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="d9091-141">Referring tooFigure 1, let's look at some of hello key parts of hello Machine Learning Studio environment for working with hello [Execute R Script][execute-r-script] module.</span></span>

* <span data-ttu-id="d9091-142">Hallo-modules in Hallo-experiment worden in Hallo middelste deelvenster weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d9091-142">hello modules in hello experiment are shown in hello center pane.</span></span>
* <span data-ttu-id="d9091-143">Hallo bovenste gedeelte van het rechter deelvenster Hallo bevat een venster tooview en uw R-scripts bewerken.</span><span class="sxs-lookup"><span data-stu-id="d9091-143">hello upper part of hello right pane contains a window tooview and edit your R scripts.</span></span>  
* <span data-ttu-id="d9091-144">Hallo onderste gedeelte van het rechter deelvenster ziet u enkele eigenschappen van Hallo [R-Script uitvoeren][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="d9091-144">hello lower part of right pane shows some properties of hello [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="d9091-145">U kunt de logboeken van de fout en uitvoer van de Hallo weergeven door te klikken op de juiste plaatsen Hallo van dit deelvenster.</span><span class="sxs-lookup"><span data-stu-id="d9091-145">You can view hello error and output logs by clicking on hello appropriate spots of this pane.</span></span>

<span data-ttu-id="d9091-146">We zullen natuurlijk worden bespreken Hallo [R-Script uitvoeren] [ execute-r-script] in de rest van dit document Hallo uitgebreider.</span><span class="sxs-lookup"><span data-stu-id="d9091-146">We will, of course, be discussing hello [Execute R Script][execute-r-script] in greater detail in hello rest of this document.</span></span>

<span data-ttu-id="d9091-147">Als u werkt met complexe R-functies, ik raden aan dat u bewerkt, testen en fouten in RStudio opsporen.</span><span class="sxs-lookup"><span data-stu-id="d9091-147">When working with complex R functions, I recommend that you edit, test and debug in RStudio.</span></span> <span data-ttu-id="d9091-148">Net als bij de ontwikkeling van alle software uw code stapsgewijs uitbreiden en het testen op kleine simpele testcases.</span><span class="sxs-lookup"><span data-stu-id="d9091-148">As with any software development, extend your code incrementally and test it on small simple test cases.</span></span> <span data-ttu-id="d9091-149">Vervolgens knippen en plakken van uw functies in de script-venster Hallo R Hallo [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="d9091-149">Then cut and paste your functions into hello R script window of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="d9091-150">Deze aanpak kunt u tooharness zowel Hallo RStudio integrated development environment (IDE) en kracht van Azure Machine Learning Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9091-150">This approach allows you tooharness both hello RStudio integrated development environment (IDE) and hello power of Azure Machine Learning.</span></span>  

#### <a name="execute-r-code"></a><span data-ttu-id="d9091-151">R code uitvoeren</span><span class="sxs-lookup"><span data-stu-id="d9091-151">Execute R code</span></span>
<span data-ttu-id="d9091-152">Geen R-code in Hallo [R-Script uitvoeren] [ execute-r-script] module wordt uitgevoerd wanneer u Hallo experiment uitvoeren door te klikken op Hallo **uitvoeren** knop.</span><span class="sxs-lookup"><span data-stu-id="d9091-152">Any R code in hello [Execute R Script][execute-r-script] module will execute when you run hello experiment by clicking on hello **Run** button.</span></span> <span data-ttu-id="d9091-153">Wanneer de uitvoering is voltooid, een vinkje worden weergegeven op Hallo [R-Script uitvoeren] [ execute-r-script] pictogram.</span><span class="sxs-lookup"><span data-stu-id="d9091-153">When execution has completed, a check mark will appear on hello [Execute R Script][execute-r-script] icon.</span></span>

#### <a name="defensive-r-coding-for-azure-machine-learning"></a><span data-ttu-id="d9091-154">Defensive R coderen voor Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d9091-154">Defensive R coding for Azure Machine Learning</span></span>
<span data-ttu-id="d9091-155">Als u R-code voor, bijvoorbeeld een web-service ontwikkelt met behulp van Azure Machine Learning, moet u zeker plannen hoe uw code wordt omgaan met een onverwachte gegevensinvoer en uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="d9091-155">If you are developing R code for, say, a web service by using Azure Machine Learning, you should definitely plan how your code will deal with an unexpected data input and exceptions.</span></span> <span data-ttu-id="d9091-156">toomaintain duidelijkheid ik niet opgenomen ongeveer Hallo manier van het controleren of de afhandeling van uitzonderingen in de meeste Hallo-codevoorbeelden die wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d9091-156">toomaintain clarity, I have not included much in hello way of checking or exception handling in most of hello code examples shown.</span></span> <span data-ttu-id="d9091-157">Echter, als we gaan ik krijgt u enkele voorbeelden van functies met behulp van de mogelijkheid voor het verwerken van het R-uitzondering.</span><span class="sxs-lookup"><span data-stu-id="d9091-157">However, as we proceed I will give you several examples of functions by using R's exception handling capability.</span></span>  

<span data-ttu-id="d9091-158">Als u een uitgebreidere behandeling van R uitzonderingsverwerking moet, ik lezen van de betreffende gedeelten Hallo van Hallo boek door Wickham die worden vermeld in het beste [bijlage B - verdere lezen](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="d9091-158">If you need a more complete treatment of R exception handling, I recommend you read hello applicable sections of hello book by Wickham listed in [Appendix B - Further Reading](#appendixb).</span></span>

#### <a name="debug-and-test-r-in-machine-learning-studio"></a><span data-ttu-id="d9091-159">Debuggen en testen van R in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="d9091-159">Debug and test R in Machine Learning Studio</span></span>
<span data-ttu-id="d9091-160">tooreiterate, ik aanbevelen u testen en foutopsporing van uw R-code op kleine schaal in RStudio.</span><span class="sxs-lookup"><span data-stu-id="d9091-160">tooreiterate, I recommend you test and debug your R code on a small scale in RStudio.</span></span> <span data-ttu-id="d9091-161">Er zijn echter gevallen u waar tootrack omlaag R code problemen in Hallo moet [R-Script uitvoeren] [ execute-r-script] zelf.</span><span class="sxs-lookup"><span data-stu-id="d9091-161">However, there are cases where you will need tootrack down R code problems in hello [Execute R Script][execute-r-script] itself.</span></span> <span data-ttu-id="d9091-162">Bovendien is raadzaam om toocheck uw resultaten in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="d9091-162">In addition, it is good practice toocheck your results in Machine Learning Studio.</span></span>

<span data-ttu-id="d9091-163">De uitvoer van Hallo uitvoering van uw R-code en op Hallo Azure Machine Learning platform is voornamelijk in uitvoer.log gevonden.</span><span class="sxs-lookup"><span data-stu-id="d9091-163">Output from hello execution of your R code and on hello Azure Machine Learning platform is found primarily in output.log.</span></span> <span data-ttu-id="d9091-164">Aanvullende informatie wordt weergegeven in error.log.</span><span class="sxs-lookup"><span data-stu-id="d9091-164">Some additional information will be seen in error.log.</span></span>  

<span data-ttu-id="d9091-165">Als een fout in Machine Learning Studio optreedt tijdens het uitvoeren van uw code R, moet uw eerste training van actie toolook op error.log.</span><span class="sxs-lookup"><span data-stu-id="d9091-165">If an error occurs in Machine Learning Studio while running your R code, your first course of action should be toolook at error.log.</span></span> <span data-ttu-id="d9091-166">Dit bestand kan nuttig zijn fout berichten toohelp begrijpt en corrigeer de fout bevatten.</span><span class="sxs-lookup"><span data-stu-id="d9091-166">This file can contain useful error messages toohelp you understand and correct your error.</span></span> <span data-ttu-id="d9091-167">tooview error.log, klik op **foutenlogboek weergeven** op Hallo **eigenschappendeelvenster** voor Hallo [R-Script uitvoeren] [ execute-r-script] met Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="d9091-167">tooview error.log, click on **View error log** on hello **properties pane** for hello [Execute R Script][execute-r-script] containing hello error.</span></span>

<span data-ttu-id="d9091-168">Bijvoorbeeld: ik heb uitgevoerd Hallo na R-code met een niet-gedefinieerde variabele y in een [R-Script uitvoeren] [ execute-r-script] module:</span><span class="sxs-lookup"><span data-stu-id="d9091-168">For example, I ran hello following R code, with an undefined variable y, in an [Execute R Script][execute-r-script] module:</span></span>

    x <- 1.0
    z <- x + y

<span data-ttu-id="d9091-169">Deze code mislukt tooexecute, wat resulteert in een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="d9091-169">This code fails tooexecute, resulting in an error condition.</span></span> <span data-ttu-id="d9091-170">Te klikken op **foutenlogboek weergeven** op Hallo **eigenschappendeelvenster** produceert Hallo weergave wordt weergegeven in afbeelding 2.</span><span class="sxs-lookup"><span data-stu-id="d9091-170">Clicking on **View error log** on hello **properties pane** produces hello display shown in Figure 2.</span></span>

  ![Foutbericht pop up][2]

<span data-ttu-id="d9091-172">*Afbeelding 2. Foutbericht pop-upvenster.*</span><span class="sxs-lookup"><span data-stu-id="d9091-172">*Figure 2. Error message pop-up.*</span></span>

<span data-ttu-id="d9091-173">Het lijkt erop dat we toolook uitvoer.log toosee Hallo R foutbericht weergegeven moet.</span><span class="sxs-lookup"><span data-stu-id="d9091-173">It looks like we need toolook in output.log toosee hello R error message.</span></span> <span data-ttu-id="d9091-174">Klik op Hallo [R-Script uitvoeren] [ execute-r-script] en klik vervolgens op Hallo **uitvoer.log weergeven** item op Hallo **eigenschappendeelvenster** toohello rechts.</span><span class="sxs-lookup"><span data-stu-id="d9091-174">Click on hello [Execute R Script][execute-r-script] and then click on hello **View output.log** item on hello **properties pane** toohello right.</span></span> <span data-ttu-id="d9091-175">Hiermee opent u een nieuw browservenster en Zie Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="d9091-175">A new browser window opens, and I see hello following.</span></span>

    [Critical]     Error: Error 0063: hello following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

<span data-ttu-id="d9091-176">Dit foutbericht bevat geen verrassingen en duidelijk identificeert Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="d9091-176">This error message contains no surprises and clearly identifies hello problem.</span></span>

<span data-ttu-id="d9091-177">tooinspect Hallo-waarde van een object in R, kunt u deze waarden toohello uitvoer.log bestand afdrukken.</span><span class="sxs-lookup"><span data-stu-id="d9091-177">tooinspect hello value of any object in R, you can print these values toohello output.log file.</span></span> <span data-ttu-id="d9091-178">Hallo-regels voor het object onderzoek waarden zijn in wezen Hallo hetzelfde als in een interactieve R-sessie.</span><span class="sxs-lookup"><span data-stu-id="d9091-178">hello rules for examining object values are essentially hello same as in an interactive R session.</span></span> <span data-ttu-id="d9091-179">Bijvoorbeeld, als u de naam van een variabele op een regel typt, Hallo waarde van Hallo object zal worden afgedrukt toohello uitvoer.log bestand.</span><span class="sxs-lookup"><span data-stu-id="d9091-179">For example, if you type a variable name on a line, hello value of hello object will be printed toohello output.log file.</span></span>  

#### <a name="packages-in-machine-learning-studio"></a><span data-ttu-id="d9091-180">Pakketten in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="d9091-180">Packages in Machine Learning Studio</span></span>
<span data-ttu-id="d9091-181">Azure Machine Learning wordt geleverd met meer dan 350 vooraf geïnstalleerde R-taalpakketten.</span><span class="sxs-lookup"><span data-stu-id="d9091-181">Azure Machine Learning comes with over 350 preinstalled R language packages.</span></span> <span data-ttu-id="d9091-182">U kunt na de code in Hallo Hallo [R-Script uitvoeren] [ execute-r-script] module tooretrieve een lijst met Hallo vooraf geïnstalleerde pakketten.</span><span class="sxs-lookup"><span data-stu-id="d9091-182">You can use hello following code in hello [Execute R Script][execute-r-script] module tooretrieve a list of hello preinstalled packages.</span></span>

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

<span data-ttu-id="d9091-183">Als u niet de laatste regel Hallo van deze code Hallo momenteel begrijpt, leest u op.</span><span class="sxs-lookup"><span data-stu-id="d9091-183">If you don't understand hello last line of this code at hello moment, read on.</span></span> <span data-ttu-id="d9091-184">In de rest van dit document Hallo behandeld uitvoerig R gebruiken in hello Azure Machine Learning-omgeving.</span><span class="sxs-lookup"><span data-stu-id="d9091-184">In hello rest of this document we will extensively discuss using R in hello Azure Machine Learning environment.</span></span>

### <a name="introduction-toorstudio"></a><span data-ttu-id="d9091-185">Inleiding tooRStudio</span><span class="sxs-lookup"><span data-stu-id="d9091-185">Introduction tooRStudio</span></span>
<span data-ttu-id="d9091-186">RStudio is een veelgebruikte IDE voor R. Ik gebruik RStudio bewerken, testen en foutopsporing aantal Hallo R-code die wordt gebruikt in deze snelstartgids.</span><span class="sxs-lookup"><span data-stu-id="d9091-186">RStudio is a widely used IDE for R. I will use RStudio for editing, testing and debugging some of hello R code used in this quick start guide.</span></span> <span data-ttu-id="d9091-187">Zodra de R-code is getest en klaar zijn, u gewoon knippen en plakken van Hallo RStudio-editor naar een Machine Learning Studio [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="d9091-187">Once R code is tested and ready, you simply cut and paste from hello RStudio editor into a Machine Learning Studio [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="d9091-188">Als u geen Hallo R programmeertaal op uw computer geïnstalleerd, ik het beste dat u doet u dat nu.</span><span class="sxs-lookup"><span data-stu-id="d9091-188">If you do not have hello R programming language installed on your desktop machine, I recommend you do so now.</span></span> <span data-ttu-id="d9091-189">Gratis downloads van open-source R taal zijn beschikbaar op Hallo uitgebreide R archief netwerk (CRAN) op [http://www.r-project.org/](http://www.r-project.org/).</span><span class="sxs-lookup"><span data-stu-id="d9091-189">Free downloads of open source R language are available at hello Comprehensive R Archive Network (CRAN) at [http://www.r-project.org/](http://www.r-project.org/).</span></span> <span data-ttu-id="d9091-190">Er zijn downloads beschikbaar voor Windows, Mac OS- en Linux/UNIX.</span><span class="sxs-lookup"><span data-stu-id="d9091-190">There are downloads available for Windows, Mac OS, and Linux/UNIX.</span></span> <span data-ttu-id="d9091-191">Kies in de buurt mirror en volg Hallo downloaden aanwijzingen.</span><span class="sxs-lookup"><span data-stu-id="d9091-191">Choose a nearby mirror and follow hello download directions.</span></span> <span data-ttu-id="d9091-192">CRAN bevat bovendien een schat aan nuttig analytics en data manipulatie pakketten.</span><span class="sxs-lookup"><span data-stu-id="d9091-192">In addition, CRAN contains a wealth of useful analytics and data manipulation packages.</span></span>

<span data-ttu-id="d9091-193">Als u nieuwe tooRStudio, moet u downloaden en installeren van de bureaubladversie Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9091-193">If you are new tooRStudio, you should download and install hello desktop version.</span></span> <span data-ttu-id="d9091-194">U vindt Hallo die rstudio downloads voor Windows-, Mac OS- en Linux/UNIX op http://www.rstudio.com/products/RStudio/.</span><span class="sxs-lookup"><span data-stu-id="d9091-194">You can find hello RStudio downloads for Windows, Mac OS, and Linux/UNIX at http://www.rstudio.com/products/RStudio/.</span></span> <span data-ttu-id="d9091-195">Volg Hallo instructies tooinstall RStudio op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d9091-195">Follow hello directions provided tooinstall RStudio on your desktop machine.</span></span>  

<span data-ttu-id="d9091-196">Een zelfstudie inleiding tooRStudio is beschikbaar op https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span><span class="sxs-lookup"><span data-stu-id="d9091-196">A tutorial introduction tooRStudio is available at https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span></span>

<span data-ttu-id="d9091-197">Ik aanvullende informatie geven over het gebruik van RStudio in [bijlage A][appendixa].</span><span class="sxs-lookup"><span data-stu-id="d9091-197">I provide some additional information on using RStudio in [Appendix A][appendixa].</span></span>  

## <span data-ttu-id="d9091-198"><a id="scriptmodule"></a>Gegevens in en uit Hallo R-Script uitvoeren module ophalen</span><span class="sxs-lookup"><span data-stu-id="d9091-198"><a id="scriptmodule"></a>Get data in and out of hello Execute R Script module</span></span>
<span data-ttu-id="d9091-199">In deze sectie bespreken we hoe u gegevens ophalen van en naar Hallo [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="d9091-199">In this section we will discuss how you get data into and out of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="d9091-200">Wordt besproken hoe toohandle verschillende soorten gegevens lezen van en naar Hallo [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="d9091-200">We will review how toohandle various data types read into and out of hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="d9091-201">Hallo volledige code voor deze sectie wordt Hallo zip-bestand die u eerder hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="d9091-201">hello complete code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="load-and-check-data-in-machine-learning-studio"></a><span data-ttu-id="d9091-202">Laden en controleren van de gegevens in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="d9091-202">Load and check data in Machine Learning Studio</span></span>
#### <span data-ttu-id="d9091-203"><a id="loading"></a>Hallo gegevensset laden</span><span class="sxs-lookup"><span data-stu-id="d9091-203"><a id="loading"></a>Load hello dataset</span></span>
<span data-ttu-id="d9091-204">We wordt gestart door bij het laden van Hallo **csdairydata.csv** -bestand in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="d9091-204">We will start by loading hello **csdairydata.csv** file into Azure Machine Learning Studio.</span></span>

* <span data-ttu-id="d9091-205">Start uw Azure Machine Learning Studio-omgeving.</span><span class="sxs-lookup"><span data-stu-id="d9091-205">Start your Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="d9091-206">Klik op **+ nieuw** op Hallo linksonder van uw scherm en selecteer **gegevensset**.</span><span class="sxs-lookup"><span data-stu-id="d9091-206">Click on **+ NEW** at hello lower left of your screen and select **Dataset**.</span></span>
* <span data-ttu-id="d9091-207">Selecteer **uit lokale bestand**, en vervolgens **Bladeren** tooselect Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="d9091-207">Select **From Local File**, and then **Browse** tooselect hello file.</span></span>
* <span data-ttu-id="d9091-208">Zorg ervoor dat u hebt geselecteerd **generieke CSV-bestand met de header (.csv)** als type voor de gegevensset Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9091-208">Make sure you have selected **Generic CSV file with header (.csv)** as hello type for hello dataset.</span></span>
* <span data-ttu-id="d9091-209">Klik op het vinkje Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9091-209">Click hello check mark.</span></span>
* <span data-ttu-id="d9091-210">Nadat Hallo gegevensset zijn geüpload, ziet u de nieuwe gegevensset Hallo door te klikken op Hallo **gegevenssets** tabblad.</span><span class="sxs-lookup"><span data-stu-id="d9091-210">After hello dataset has been uploaded, you should see hello new dataset by clicking on hello **Datasets** tab.</span></span>  

#### <a name="create-an-experiment"></a><span data-ttu-id="d9091-211">Een experiment maken</span><span class="sxs-lookup"><span data-stu-id="d9091-211">Create an experiment</span></span>
<span data-ttu-id="d9091-212">Nu dat we enkele gegevens in Machine Learning Studio hebben, moeten we toocreate een experiment toodo Hallo analyse.</span><span class="sxs-lookup"><span data-stu-id="d9091-212">Now that we have some data in Machine Learning Studio, we need toocreate an experiment toodo hello analysis.</span></span>  

* <span data-ttu-id="d9091-213">Klik op **+ nieuw** op Hallo linksonder loopt en selecteer **Experiment**, klikt u vervolgens **leeg Experiment**.</span><span class="sxs-lookup"><span data-stu-id="d9091-213">Click on **+ NEW** at hello lower left and select **Experiment**, then **Blank Experiment**.</span></span>
* <span data-ttu-id="d9091-214">Naam van uw experiment door te selecteren en te wijzigen, Hallo **Experiment op wordt gemaakt...**  titel bovenaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="d9091-214">You can name your experiment by selecting, and modifying, hello **Experiment created on ...** title at hello top of hello page.</span></span> <span data-ttu-id="d9091-215">Bijvoorbeeld, te wijzigen**CA Zuivel Analysis**.</span><span class="sxs-lookup"><span data-stu-id="d9091-215">For example, changing it too**CA Dairy Analysis**.</span></span>
* <span data-ttu-id="d9091-216">Vouw op Hallo links van Hallo experiment pagina **gegevenssets opgeslagen**, en vervolgens **mijn gegevenssets**.</span><span class="sxs-lookup"><span data-stu-id="d9091-216">On hello left of hello experiment page, expand **Saved Datasets**, and then **My Datasets**.</span></span> <span data-ttu-id="d9091-217">U ziet Hallo **cadairydata.csv** die u eerder hebt geüpload.</span><span class="sxs-lookup"><span data-stu-id="d9091-217">You should see hello **cadairydata.csv** that you uploaded earlier.</span></span>
* <span data-ttu-id="d9091-218">Slepen en neerzetten Hallo **csdairydata.csv gegevensset** op Hallo experiment.</span><span class="sxs-lookup"><span data-stu-id="d9091-218">Drag and drop hello **csdairydata.csv dataset** onto hello experiment.</span></span>
* <span data-ttu-id="d9091-219">In Hallo **zoeken items experimenteren** vak op Hallo Hallo linkerdeelvenster type bovenaan [R-Script uitvoeren][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="d9091-219">In hello **Search experiment items** box on hello top of hello left pane, type [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="d9091-220">Hier ziet u Hallo-module worden weergegeven in de zoeklijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9091-220">You will see hello module appear in hello search list.</span></span>
* <span data-ttu-id="d9091-221">Slepen en neerzetten Hallo [R-Script uitvoeren] [ execute-r-script] module naar uw palet.</span><span class="sxs-lookup"><span data-stu-id="d9091-221">Drag and drop hello [Execute R Script][execute-r-script] module onto your pallet.</span></span>  
* <span data-ttu-id="d9091-222">Verbinding maken met uitvoer Hallo Hallo **csdairydata.csv gegevensset** toohello meest linkse invoer (**Dataset1**) Hallo [R-Script uitvoeren][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="d9091-222">Connect hello output of hello **csdairydata.csv dataset** toohello leftmost input (**Dataset1**) of hello [Execute R Script][execute-r-script].</span></span>
* <span data-ttu-id="d9091-223">**Vergeet niet tooclick op 'Save'.**</span><span class="sxs-lookup"><span data-stu-id="d9091-223">**Don't forget tooclick on 'Save'!**</span></span>  

<span data-ttu-id="d9091-224">Op dit moment ziet uw experiment er ongeveer als afbeelding 3.</span><span class="sxs-lookup"><span data-stu-id="d9091-224">At this point your experiment should look something like Figure 3.</span></span>

![Hallo CA Zuivel Analysis experimenteren met de gegevensset en module R-Script uitvoeren][3]

<span data-ttu-id="d9091-226">*Afbeelding 3. Hallo CA Zuivel Analysis experimenteren met gegevensset en module R-Script niet uitvoeren.*</span><span class="sxs-lookup"><span data-stu-id="d9091-226">*Figure 3. hello CA Dairy Analysis experiment with dataset and Execute R Script module.*</span></span>

#### <a name="check-on-hello-data"></a><span data-ttu-id="d9091-227">Controleer op Hallo-gegevens</span><span class="sxs-lookup"><span data-stu-id="d9091-227">Check on hello data</span></span>
<span data-ttu-id="d9091-228">We hebben bekijkt hello gegevens die we in ons experiment hebben geladen.</span><span class="sxs-lookup"><span data-stu-id="d9091-228">Let's have a look at hello data we have loaded into our experiment.</span></span> <span data-ttu-id="d9091-229">Hallo-experiment, klik op Hallo uitvoer Hallo **cadairydata.csv gegevensset** en selecteer **visualiseren**.</span><span class="sxs-lookup"><span data-stu-id="d9091-229">In hello experiment, click on hello output of hello **cadairydata.csv dataset** and select **visualize**.</span></span> <span data-ttu-id="d9091-230">U ziet er ongeveer zo afbeelding 4.</span><span class="sxs-lookup"><span data-stu-id="d9091-230">You should see something like Figure 4.</span></span>  

![Samenvatting van Hallo cadairydata.csv gegevensset][4]

<span data-ttu-id="d9091-232">*Afbeelding 4. Samenvatting van Hallo cadairydata.csv gegevensset.*</span><span class="sxs-lookup"><span data-stu-id="d9091-232">*Figure 4. Summary of hello cadairydata.csv dataset.*</span></span>

<span data-ttu-id="d9091-233">In deze weergave ziet u een groot aantal nuttige informatie.</span><span class="sxs-lookup"><span data-stu-id="d9091-233">In this view we see a lot of useful information.</span></span> <span data-ttu-id="d9091-234">We zien Hallo eerste verschillende rijen van deze dataset.</span><span class="sxs-lookup"><span data-stu-id="d9091-234">We can see hello first several rows of that dataset.</span></span> <span data-ttu-id="d9091-235">Als er een kolom selecteert, ziet u Hallo statistieken sectie meer informatie over het Hallo-kolom.</span><span class="sxs-lookup"><span data-stu-id="d9091-235">If we select a column, hello Statistics section shows more information about hello column.</span></span> <span data-ttu-id="d9091-236">Bijvoorbeeld, staan Hallo onderdeeltype rij ons welke gegevenstypen Azure Machine Learning Studio toohello kolom toegewezen.</span><span class="sxs-lookup"><span data-stu-id="d9091-236">For example, hello Feature Type row shows us what data types Azure Machine Learning Studio assigned toohello column.</span></span> <span data-ttu-id="d9091-237">Een snelle zien er als volgt met is een goede controle, laten we toodo ernstige werk beginnen.</span><span class="sxs-lookup"><span data-stu-id="d9091-237">Having a quick look like this is a good sanity check before we start toodo any serious work.</span></span>

### <a name="first-r-script"></a><span data-ttu-id="d9091-238">Eerste R-script</span><span class="sxs-lookup"><span data-stu-id="d9091-238">First R script</span></span>
<span data-ttu-id="d9091-239">We maken met een eenvoudige eerste R-script tooexperiment met in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="d9091-239">Let's create a simple first R script tooexperiment with in Azure Machine Learning Studio.</span></span> <span data-ttu-id="d9091-240">Ik heb gemaakt en getest Hallo script in RStudio te volgen.</span><span class="sxs-lookup"><span data-stu-id="d9091-240">I have created and tested hello following script in RStudio.</span></span>  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="d9091-241">Nu moet ik tootransfer dit script tooAzure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="d9091-241">Now I need tootransfer this script tooAzure Machine Learning Studio.</span></span> <span data-ttu-id="d9091-242">Ik kan eenvoudig knippen en plakken.</span><span class="sxs-lookup"><span data-stu-id="d9091-242">I could simply cut and paste.</span></span> <span data-ttu-id="d9091-243">Echter, in dit geval ik draagt mijn R-script via een zip-bestand.</span><span class="sxs-lookup"><span data-stu-id="d9091-243">However, in this case, I will transfer my R script via a zip file.</span></span>

### <a name="data-input-toohello-execute-r-script-module"></a><span data-ttu-id="d9091-244">Data-module voor invoer toohello R-Script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="d9091-244">Data input toohello Execute R Script module</span></span>
<span data-ttu-id="d9091-245">We hebben bekijkt hello invoer toohello [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="d9091-245">Let's have a look at hello inputs toohello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="d9091-246">In dit voorbeeld wordt gelezen Hallo Californië melkkoeien gegevens in Hallo [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="d9091-246">In this example we will read hello California dairy data into hello [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="d9091-247">Er zijn drie mogelijke ingangen voor Hallo [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="d9091-247">There are three possible inputs for hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="d9091-248">U kunt een of meer van deze invoer, afhankelijk van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="d9091-248">You may use any one or all of these inputs, depending on your application.</span></span> <span data-ttu-id="d9091-249">Het is ook perfect redelijke toouse een R-script dat u helemaal geen invoer nodig.</span><span class="sxs-lookup"><span data-stu-id="d9091-249">It is also perfectly reasonable toouse an R script that takes no input at all.</span></span>  

<span data-ttu-id="d9091-250">We bekijken op elk van deze invoerwaarden, van links tooright.</span><span class="sxs-lookup"><span data-stu-id="d9091-250">Let's look at each of these inputs, going from left tooright.</span></span> <span data-ttu-id="d9091-251">Namen van elk van de invoerwaarden Hallo Hallo kunt u zien door de cursor op Hallo invoer plaatsen en Hallo knopinfo te lezen.</span><span class="sxs-lookup"><span data-stu-id="d9091-251">You can see hello names of each of hello inputs by placing your cursor over hello input and reading hello tooltip.</span></span>  

#### <a name="script-bundle"></a><span data-ttu-id="d9091-252">Script bundel</span><span class="sxs-lookup"><span data-stu-id="d9091-252">Script Bundle</span></span>
<span data-ttu-id="d9091-253">Hallo Script bundel invoer kunt u toopass Hallo inhoud van een zip-bestand in [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="d9091-253">hello Script Bundle input allows you toopass hello contents of a zip file into [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="d9091-254">U kunt een Hallo opdrachten tooread Hallo inhoud van het zip-bestand hello te volgen in uw R-code.</span><span class="sxs-lookup"><span data-stu-id="d9091-254">You can use one of hello following commands tooread hello contents of hello zip file into your R code.</span></span>

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> <span data-ttu-id="d9091-255">Azure Machine Learning bestanden in Hallo ZIP-bestand wordt behandeld alsof ze zich in Hallo src / Active directory, dus moet u de namen van het bestand met deze directorynaam tooprefix.</span><span class="sxs-lookup"><span data-stu-id="d9091-255">Azure Machine Learning treats files in hello zip as if they are in hello src/ directory, so you need tooprefix your file names with this directory name.</span></span> <span data-ttu-id="d9091-256">Bijvoorbeeld, als hello zip Hallo bestanden bevat `yourfile.R` en `yourData.rdata` in de hoofdmap van de Hallo van Hallo zip, zou u deze poorten als adresseren `src/yourfile.R` en `src/yourData.rdata` bij gebruik van `source` en `load`.</span><span class="sxs-lookup"><span data-stu-id="d9091-256">For example, if hello zip contains hello files `yourfile.R` and `yourData.rdata` in hello root of hello zip, you would address these as `src/yourfile.R` and `src/yourData.rdata` when using `source` and `load`.</span></span>
> 
> 

<span data-ttu-id="d9091-257">Besproken al gegevenssets laden in [Hallo gegevensset laden](#loading).</span><span class="sxs-lookup"><span data-stu-id="d9091-257">We already discussed loading datasets in [Loading hello dataset](#loading).</span></span> <span data-ttu-id="d9091-258">Zodra u hebt gemaakt en getest Hallo R-script wordt weergegeven in de vorige sectie hello, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="d9091-258">Once you have created and tested hello R script shown in hello previous section, do hello following:</span></span>

1. <span data-ttu-id="d9091-259">Sla Hallo R-script in een. R-bestand.</span><span class="sxs-lookup"><span data-stu-id="d9091-259">Save hello R script into a .R file.</span></span> <span data-ttu-id="d9091-260">Ik mijn scriptbestand 'simpleplot aanroepen. R'.</span><span class="sxs-lookup"><span data-stu-id="d9091-260">I call my script file "simpleplot.R".</span></span> <span data-ttu-id="d9091-261">Hier volgt Hallo inhoud.</span><span class="sxs-lookup"><span data-stu-id="d9091-261">Here's hello contents.</span></span>
   
        ## Only one of hello following two lines should be used
        ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
        ## If in RStudio, use hello second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## hello following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. <span data-ttu-id="d9091-262">Maak een zip-bestand en kopieer het script naar dit zipbestand.</span><span class="sxs-lookup"><span data-stu-id="d9091-262">Create a zip file and copy your script into this zip file.</span></span> <span data-ttu-id="d9091-263">Op Windows, kunt u met de rechtermuisknop op het Hallo-bestand en selecteer **verzenden naar**, en vervolgens **gecomprimeerde map**.</span><span class="sxs-lookup"><span data-stu-id="d9091-263">On Windows, you can right-click on hello file and select **Send to**, and then **Compressed folder**.</span></span> <span data-ttu-id="d9091-264">Hiermee maakt u een nieuwe zip-bestand met de Hallo 'simpleplot. R'-bestand.</span><span class="sxs-lookup"><span data-stu-id="d9091-264">This will create a new zip file containing hello "simpleplot.R" file.</span></span>
3. <span data-ttu-id="d9091-265">Toevoegen van uw bestand toohello **gegevenssets** in Machine Learning Studio, geven Hallo type als **zip**.</span><span class="sxs-lookup"><span data-stu-id="d9091-265">Add your file toohello **datasets** in Machine Learning Studio, specifying hello type as **zip**.</span></span> <span data-ttu-id="d9091-266">U ziet nu Hallo zip-bestand in de gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="d9091-266">You should now see hello zip file in your datasets.</span></span>
4. <span data-ttu-id="d9091-267">Slepen en neerzetten Hallo zip-bestand van **gegevenssets** op Hallo **ML Studio canvas**.</span><span class="sxs-lookup"><span data-stu-id="d9091-267">Drag and drop hello zip file from **datasets** onto hello **ML Studio canvas**.</span></span>
5. <span data-ttu-id="d9091-268">Verbinding maken met uitvoer Hallo Hallo **zip-gegevens** pictogram toohello **Script bundel** invoer Hallo [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="d9091-268">Connect hello output of hello **zip data** icon toohello **Script Bundle** input of hello [Execute R Script][execute-r-script] module.</span></span>
6. <span data-ttu-id="d9091-269">Type Hallo `source()` functie met de naam van uw zip-bestand in het venster Hallo-code voor Hallo [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="d9091-269">Type hello `source()` function with your zip file name into hello code window for hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="d9091-270">Ik heb getypt in mijn geval `source("src/simpleplot.R")`.</span><span class="sxs-lookup"><span data-stu-id="d9091-270">In my case I typed `source("src/simpleplot.R")`.</span></span>  
7. <span data-ttu-id="d9091-271">Controleer of u **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="d9091-271">Make sure you click **Save**.</span></span>

<span data-ttu-id="d9091-272">Als deze stappen voltooid zijn, Hallo [R-Script uitvoeren] [ execute-r-script] module Hallo R-script in Hallo zip-bestand wordt uitgevoerd wanneer Hallo experiment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d9091-272">Once these steps are complete, hello [Execute R Script][execute-r-script] module will execute hello R script in hello zip file when hello experiment is run.</span></span> <span data-ttu-id="d9091-273">Op dit moment ziet uw experiment er ongeveer als afbeelding 5.</span><span class="sxs-lookup"><span data-stu-id="d9091-273">At this point your experiment should look something like Figure 5.</span></span>

![Experimenteer met gecomprimeerde R-script][6]

<span data-ttu-id="d9091-275">*Afbeelding 5. Experimenteer met gecomprimeerde R-script.*</span><span class="sxs-lookup"><span data-stu-id="d9091-275">*Figure 5. Experiment using zipped R script.*</span></span>

#### <a name="dataset1"></a><span data-ttu-id="d9091-276">Dataset1</span><span class="sxs-lookup"><span data-stu-id="d9091-276">Dataset1</span></span>
<span data-ttu-id="d9091-277">U kunt een rechthoekig tabel gegevens tooyour R code doorgeven met behulp van Hallo Dataset1 invoer.</span><span class="sxs-lookup"><span data-stu-id="d9091-277">You can pass a rectangular table of data tooyour R code by using hello Dataset1 input.</span></span> <span data-ttu-id="d9091-278">In onze eenvoudig script Hallo `maml.mapInputPort(1)` functie Hallo gegevens leest uit poort 1.</span><span class="sxs-lookup"><span data-stu-id="d9091-278">In our simple script hello `maml.mapInputPort(1)` function reads hello data from port 1.</span></span> <span data-ttu-id="d9091-279">Deze gegevens worden vervolgens toegewezen tooa dataframe variabelenaam in uw code.</span><span class="sxs-lookup"><span data-stu-id="d9091-279">This data is then assigned tooa dataframe variable name in your code.</span></span> <span data-ttu-id="d9091-280">In onze eenvoudig script voert de eerste coderegel Hallo Hallo-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="d9091-280">In our simple script hello first line of code performs hello assignment.</span></span>

    cadairydata <- maml.mapInputPort(1)

<span data-ttu-id="d9091-281">Uw experiment uitvoeren door te klikken op Hallo **uitvoeren** knop.</span><span class="sxs-lookup"><span data-stu-id="d9091-281">Execute your experiment by clicking on hello **Run** button.</span></span> <span data-ttu-id="d9091-282">Wanneer het Hallo-uitvoering is voltooid, klikt u op Hallo [R-Script uitvoeren] [ execute-r-script] module en klik vervolgens op **weergave logboek** op Hallo eigenschappendeelvenster.</span><span class="sxs-lookup"><span data-stu-id="d9091-282">When hello execution finishes, click on hello [Execute R Script][execute-r-script] module and then click **View output log** on hello properties pane.</span></span> <span data-ttu-id="d9091-283">Een nieuwe pagina moet worden weergegeven in uw browser Hallo inhoud van Hallo uitvoer.log bestand weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d9091-283">A new page should appear in your browser showing hello contents of hello output.log file.</span></span> <span data-ttu-id="d9091-284">Wanneer u omlaag schuiven ziet u dat lijkt op Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="d9091-284">When you scroll down you should see something like hello following.</span></span>

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

<span data-ttu-id="d9091-285">Omlaag Hallo is verder pagina meer gedetailleerde informatie over het Hallo-kolommen als volgt Hallo volgende uitzien wordt.</span><span class="sxs-lookup"><span data-stu-id="d9091-285">Farther down hello page is more detailed information on hello columns, which will look something like hello following.</span></span>

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

<span data-ttu-id="d9091-286">Deze resultaten zijn voornamelijk zoals verwacht, met 228 opmerkingen en 9 kolommen in Hallo dataframe.</span><span class="sxs-lookup"><span data-stu-id="d9091-286">These results are mostly as expected, with 228 observations and 9 columns in hello dataframe.</span></span> <span data-ttu-id="d9091-287">We zien kolomnamen hello, Hallo R-gegevenstype en een voorbeeld van elke kolom.</span><span class="sxs-lookup"><span data-stu-id="d9091-287">We can see hello column names, hello R data type and a sample of each column.</span></span>

> [!NOTE]
> <span data-ttu-id="d9091-288">Deze dezelfde afdruk is gemakkelijk beschikbaar zijn via Hallo R-apparaat uitvoer Hallo [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="d9091-288">This same printed output is conveniently available from hello R Device output of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="d9091-289">Bespreken we Hallo uitvoerwaarden van Hallo [R-Script uitvoeren] [ execute-r-script] module in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9091-289">We will discuss hello outputs of hello [Execute R Script][execute-r-script] module in hello next section.</span></span>  
> 
> 

#### <a name="dataset2"></a><span data-ttu-id="d9091-290">Dataset2</span><span class="sxs-lookup"><span data-stu-id="d9091-290">Dataset2</span></span>
<span data-ttu-id="d9091-291">Hallo is gedrag van Hallo Dataset2 invoer identiek toothat van Dataset1.</span><span class="sxs-lookup"><span data-stu-id="d9091-291">hello behavior of hello Dataset2 input is identical toothat of Dataset1.</span></span> <span data-ttu-id="d9091-292">U kunt met behulp van deze invoer een tweede rechthoekige gegevenstabel doorgeven in uw R-code.</span><span class="sxs-lookup"><span data-stu-id="d9091-292">Using this input you can pass a second rectangular table of data into your R code.</span></span> <span data-ttu-id="d9091-293">Hallo functie `maml.mapInputPort(2)`, wordt met Hallo argument 2, toopass gebruikt deze gegevens.</span><span class="sxs-lookup"><span data-stu-id="d9091-293">hello function `maml.mapInputPort(2)`, with hello argument 2, is used toopass this data.</span></span>  

### <a name="execute-r-script-outputs"></a><span data-ttu-id="d9091-294">De uitvoer R-Script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="d9091-294">Execute R Script outputs</span></span>
#### <a name="output-a-dataframe"></a><span data-ttu-id="d9091-295">Een dataframe uitvoer</span><span class="sxs-lookup"><span data-stu-id="d9091-295">Output a dataframe</span></span>
<span data-ttu-id="d9091-296">Kunt u Hallo inhoud van een R-dataframe als een rechthoekig tabel via poort Hallo resultaat Dataset1 uitvoeren met behulp van Hallo `maml.mapOutputPort()` functie.</span><span class="sxs-lookup"><span data-stu-id="d9091-296">You can output hello contents of an R dataframe as a rectangular table through hello Result Dataset1 port by using hello `maml.mapOutputPort()` function.</span></span> <span data-ttu-id="d9091-297">In onze eenvoudig R-script wordt uitgevoerd door Hallo volgt regel.</span><span class="sxs-lookup"><span data-stu-id="d9091-297">In our simple R script this is performed by hello following line.</span></span>

    maml.mapOutputPort('cadairydata')

<span data-ttu-id="d9091-298">Klik op de uitvoerpoort resultaat Dataset1 Hallo na actieve Hallo-experiment, en klik vervolgens op **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="d9091-298">After running hello experiment, click on hello Result Dataset1 output port and then click on **Visualize**.</span></span> <span data-ttu-id="d9091-299">U ziet er ongeveer zo afbeelding 6.</span><span class="sxs-lookup"><span data-stu-id="d9091-299">You should see something like Figure 6.</span></span>

![Hallo-visualisatie van uitvoer Hallo Hallo Californië melkkoeien gegevens][7]

<span data-ttu-id="d9091-301">*Afbeelding 6. Hallo visualisatie van uitvoer Hallo Hallo Californië melkkoeien gegevens.*</span><span class="sxs-lookup"><span data-stu-id="d9091-301">*Figure 6. hello visualization of hello output of hello California dairy data.*</span></span>

<span data-ttu-id="d9091-302">Deze uitvoer ziet er identiek toohello invoer, precies zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="d9091-302">This output looks identical toohello input, exactly as we expected.</span></span>  

### <a name="r-device-output"></a><span data-ttu-id="d9091-303">R-apparaat-uitvoer</span><span class="sxs-lookup"><span data-stu-id="d9091-303">R Device output</span></span>
<span data-ttu-id="d9091-304">Apparaat-uitvoer van Hallo Hallo [R-Script uitvoeren] [ execute-r-script] -module bevat de uitvoer van berichten en afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="d9091-304">hello Device output of hello [Execute R Script][execute-r-script] module contains messages and graphics output.</span></span> <span data-ttu-id="d9091-305">Beide standaard uitvoer en de standaardfout van R berichten worden toohello uitvoerpoort R-apparaat.</span><span class="sxs-lookup"><span data-stu-id="d9091-305">Both standard output and standard error messages from R are sent toohello R Device output port.</span></span>  

<span data-ttu-id="d9091-306">tooview hello R-apparaat uitvoert, klik op Hallo-poort en klik vervolgens op **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="d9091-306">tooview hello R Device output, click on hello port and then on **Visualize**.</span></span> <span data-ttu-id="d9091-307">Hallo standaarduitvoer en de standaardfout van Hallo R-script in afbeelding 7 ziet.</span><span class="sxs-lookup"><span data-stu-id="d9091-307">We see hello standard output and standard error from hello R script in Figure 7.</span></span>

![Standaarduitvoer en de standaardfout van Hallo poort R-apparaat][8]

<span data-ttu-id="d9091-309">*Afbeelding 7. Standaarduitvoer en de standaardfout van Hallo poort R-apparaat.*</span><span class="sxs-lookup"><span data-stu-id="d9091-309">*Figure 7. Standard output and standard error from hello R Device port.*</span></span>

<span data-ttu-id="d9091-310">We verschuift Zie Hallo grafische uitvoer van onze R-script in afbeelding 8.</span><span class="sxs-lookup"><span data-stu-id="d9091-310">Scrolling down we see hello graphics output from our R script in Figure 8.</span></span>  

![Grafische uitvoer van Hallo poort R-apparaat][9]

<span data-ttu-id="d9091-312">*Afbeelding 8. Afbeeldingen de uitvoer van Hallo poort R-apparaat.*</span><span class="sxs-lookup"><span data-stu-id="d9091-312">*Figure 8. Graphics output from hello R Device port.*</span></span>  

## <span data-ttu-id="d9091-313"><a id="filtering"></a>Gegevens filteren en transformatie</span><span class="sxs-lookup"><span data-stu-id="d9091-313"><a id="filtering"></a>Data filtering and transformation</span></span>
<span data-ttu-id="d9091-314">In deze sectie wordt uitgevoerd, er enkele elementaire gegevens filteren en transformatiebewerkingen op Hallo Californië melkkoeien gegevens.</span><span class="sxs-lookup"><span data-stu-id="d9091-314">In this section we will perform some basic data filtering and transformation operations on hello California dairy data.</span></span> <span data-ttu-id="d9091-315">Hallo-einde van deze sectie hebben we gegevens in een indeling die geschikt is voor het bouwen van een analytische model.</span><span class="sxs-lookup"><span data-stu-id="d9091-315">By hello end of this section we will have data in a format suitable for building an analytic model.</span></span>  

<span data-ttu-id="d9091-316">Meer specifiek, in deze sectie wordt we enkele algemene gegevens opruimen en transformatie taken uitvoeren: type transformatie, filteren op dataframes, nieuwe berekende kolommen, toe te voegen en de waarde van transformaties.</span><span class="sxs-lookup"><span data-stu-id="d9091-316">More specifically, in this section we will perform several common data cleaning and transformation tasks: type transformation, filtering on dataframes, adding new computed columns, and value transformations.</span></span> <span data-ttu-id="d9091-317">Deze achtergrond kunt u veel variaties aangetroffen in de praktische problemen te maken met de Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9091-317">This background should help you deal with hello many variations encountered in real-world problems.</span></span>

<span data-ttu-id="d9091-318">Hallo volledige R-code voor deze sectie is beschikbaar in Hallo zip-bestand die u eerder hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="d9091-318">hello complete R code for this section is available in hello zip file you downloaded earlier.</span></span>

### <a name="type-transformations"></a><span data-ttu-id="d9091-319">Type transformaties</span><span class="sxs-lookup"><span data-stu-id="d9091-319">Type transformations</span></span>
<span data-ttu-id="d9091-320">Nu dat we Hallo Californië melkkoeien gegevens in de code in Hallo Hallo R lezen kan [R-Script uitvoeren] [ execute-r-script] -module, moeten we tooensure dat Hallo-gegevens in kolommen Hallo Hallo bedoeld type en de indeling heeft.</span><span class="sxs-lookup"><span data-stu-id="d9091-320">Now that we can read hello California dairy data into hello R code in hello [Execute R Script][execute-r-script] module, we need tooensure that hello data in hello columns has hello intended type and format.</span></span>  

<span data-ttu-id="d9091-321">R is een dynamisch getypeerde taal, wat betekent dat gegevenstypen worden gedwongen van één tooanother zoals vereist.</span><span class="sxs-lookup"><span data-stu-id="d9091-321">R is a dynamically typed language, which means that data types are coerced from one tooanother as required.</span></span> <span data-ttu-id="d9091-322">Hallo-atomic gegevenstypen in R bevatten numerieke waarden, logische en -teken.</span><span class="sxs-lookup"><span data-stu-id="d9091-322">hello atomic data types in R include numeric, logical and character.</span></span> <span data-ttu-id="d9091-323">Hallo factor type is gebruikte toocompactly categorische gegevens op te slaan.</span><span class="sxs-lookup"><span data-stu-id="d9091-323">hello factor type is used toocompactly store categorical data.</span></span> <span data-ttu-id="d9091-324">U vindt meer informatie over gegevenstypen in Hallo-verwijzingen in [bijlage B – Lees hier meer over](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="d9091-324">You can find much more information on data types in hello references in [Appendix B - Further reading](#appendixb).</span></span>

<span data-ttu-id="d9091-325">Wanneer tabelgegevens wordt gelezen in R uit een externe bron, maar het is altijd een goed idee toocheck Hallo resulterende typen in Hallo kolommen.</span><span class="sxs-lookup"><span data-stu-id="d9091-325">When tabular data is read into R from an external source, it is always a good idea toocheck hello resulting types in hello columns.</span></span> <span data-ttu-id="d9091-326">U kunt een kolom van het typeteken, maar in veel gevallen dit wordt weergegeven als factor of vice versa.</span><span class="sxs-lookup"><span data-stu-id="d9091-326">You may want a column of type character, but in many cases this will show up as factor or vice versa.</span></span> <span data-ttu-id="d9091-327">In andere gevallen een kolom die u denkt dat moet worden wordt numerieke vertegenwoordigd door tekengegevens, bijvoorbeeld '1,23' in plaats van 1,23 als een zwevende-kommagetal.</span><span class="sxs-lookup"><span data-stu-id="d9091-327">In other cases a column you think should be numeric is represented by character data, e.g. '1.23' rather than 1.23 as a floating point number.</span></span>  

<span data-ttu-id="d9091-328">Gelukkig is eenvoudig tooconvert één type tooanother, zolang de toewijzing is mogelijk.</span><span class="sxs-lookup"><span data-stu-id="d9091-328">Fortunately, it is easy tooconvert one type tooanother, as long as mapping is possible.</span></span> <span data-ttu-id="d9091-329">Bijvoorbeeld, u 'Nevada' niet converteren naar een numerieke waarde, maar u tooa factor (categorische variabele) kunt converteren.</span><span class="sxs-lookup"><span data-stu-id="d9091-329">For example, you cannot convert 'Nevada' into a numeric value, but you can convert it tooa factor (categorical variable).</span></span> <span data-ttu-id="d9091-330">U kunt bijvoorbeeld een numerieke 1 omzetten in een teken '1' of een factor.</span><span class="sxs-lookup"><span data-stu-id="d9091-330">As another example, you can convert a numeric 1 into a character '1' or a factor.</span></span>  

<span data-ttu-id="d9091-331">Hallo-syntaxis voor een van deze omzettingen is eenvoudig: `as.datatype()`.</span><span class="sxs-lookup"><span data-stu-id="d9091-331">hello syntax for any of these conversions is simple: `as.datatype()`.</span></span> <span data-ttu-id="d9091-332">Deze functies voor typeconversie omvatten Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="d9091-332">These type conversion functions include hello following.</span></span>

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

<span data-ttu-id="d9091-333">Bekijkt hello gegevenstypen Hallo kolommen die we in de vorige sectie Hallo invoer: alle kolommen van het type numeriek zijn, met uitzondering van Hallo kolom met de naam 'Maand', van het typeteken is zijn.</span><span class="sxs-lookup"><span data-stu-id="d9091-333">Looking at hello data types of hello columns we input in hello previous section: all columns are of type numeric, except for hello column labeled 'Month', which is of type character.</span></span> <span data-ttu-id="d9091-334">Laten we deze factor tooa converteren en Hallo testresultaten.</span><span class="sxs-lookup"><span data-stu-id="d9091-334">Let's convert this tooa factor and test hello results.</span></span>  

<span data-ttu-id="d9091-335">Ik heb hebt Hallo-regel die Hallo scatterplot matrix gemaakt en een regel converteren Hallo 'Maand' kolom tooa factor toegevoegd verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d9091-335">I have deleted hello line that created hello scatterplot matrix and added a line converting hello 'Month' column tooa factor.</span></span> <span data-ttu-id="d9091-336">In mijn experiment wordt ik net knippen en plakken Hallo R-code in het venster van de code Hallo Hallo [R-Script uitvoeren] [ execute-r-script] Module.</span><span class="sxs-lookup"><span data-stu-id="d9091-336">In my experiment I will just cut and paste hello R code into hello code window of hello [Execute R Script][execute-r-script] Module.</span></span> <span data-ttu-id="d9091-337">U kunt ook Hallo zip-bestand bijwerken en tooAzure Machine Learning Studio te uploaden, maar verschillende stappen gaat.</span><span class="sxs-lookup"><span data-stu-id="d9091-337">You could also update hello zip file and upload it tooAzure Machine Learning Studio, but this takes several steps.</span></span>  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check hello result
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="d9091-338">Laten we deze code uitvoeren en bekijkt hello logboek voor Hallo R-script.</span><span class="sxs-lookup"><span data-stu-id="d9091-338">Let's execute this code and look at hello output log for hello R script.</span></span> <span data-ttu-id="d9091-339">Hallo relevante gegevens uit Hallo logboek wordt weergegeven in afbeelding 9.</span><span class="sxs-lookup"><span data-stu-id="d9091-339">hello relevant data from hello log is shown in Figure 9.</span></span>

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
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="d9091-340">*Afbeelding 9. Samenvatting van Hallo dataframe met een factor-variabele.*</span><span class="sxs-lookup"><span data-stu-id="d9091-340">*Figure 9. Summary of hello dataframe with a factor variable.*</span></span>

<span data-ttu-id="d9091-341">Hallo-type voor de maand nu de melding '**Factor met 14 niveaus**'.</span><span class="sxs-lookup"><span data-stu-id="d9091-341">hello type for Month should now say '**Factor w/ 14 levels**'.</span></span> <span data-ttu-id="d9091-342">Dit is een probleem, omdat er alleen 12 maanden Hallo jaar.</span><span class="sxs-lookup"><span data-stu-id="d9091-342">This is a problem since there are only 12 months in hello year.</span></span> <span data-ttu-id="d9091-343">U kunt ook controleren toosee die type Hallo in **Visualize** Hallo resultaat gegevensset poort is '**Categorical**'.</span><span class="sxs-lookup"><span data-stu-id="d9091-343">You can also check toosee that hello type in **Visualize** of hello Result Dataset port is '**Categorical**'.</span></span>

<span data-ttu-id="d9091-344">Hallo-probleem is dat Hallo maand kolom heeft systematischer niet gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="d9091-344">hello problem is that hello 'Month' column has not been coded systematically.</span></span> <span data-ttu-id="d9091-345">In sommige gevallen een maand April wordt genoemd, en in andere gevallen wordt het april afgekort. We kunnen dit probleem oplossen door Hallo tekenreeks too3 tekens.</span><span class="sxs-lookup"><span data-stu-id="d9091-345">In some cases a month is called April and in others it is abbreviated as Apr. We can solve this problem by trimming hello string too3 characters.</span></span> <span data-ttu-id="d9091-346">Hallo volgende ziet coderegel Hallo nu:</span><span class="sxs-lookup"><span data-stu-id="d9091-346">hello line of code now looks like hello following:</span></span>

    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

<span data-ttu-id="d9091-347">Hallo-experiment opnieuw uitvoeren en Hallo logboek weergeven.</span><span class="sxs-lookup"><span data-stu-id="d9091-347">Rerun hello experiment and view hello output log.</span></span> <span data-ttu-id="d9091-348">Hallo verwacht resultaten worden weergegeven in afbeelding 10.</span><span class="sxs-lookup"><span data-stu-id="d9091-348">hello expected results are shown in Figure 10.</span></span>  

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
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="d9091-349">*Afbeelding 10. Samenvatting van Hallo dataframe met het juiste aantal factorniveaus.*</span><span class="sxs-lookup"><span data-stu-id="d9091-349">*Figure 10. Summary of hello dataframe with correct number of factor levels.*</span></span>

<span data-ttu-id="d9091-350">Onze variabele factor heeft nu Hallo gewenst 12 niveaus.</span><span class="sxs-lookup"><span data-stu-id="d9091-350">Our factor variable now has hello desired 12 levels.</span></span>

### <a name="basic-data-frame-filtering"></a><span data-ttu-id="d9091-351">Basisgegevens frame filteren</span><span class="sxs-lookup"><span data-stu-id="d9091-351">Basic data frame filtering</span></span>
<span data-ttu-id="d9091-352">R dataframes ondersteunen krachtige filteropties.</span><span class="sxs-lookup"><span data-stu-id="d9091-352">R dataframes support powerful filtering capabilities.</span></span> <span data-ttu-id="d9091-353">Gegevenssets kan subset met logische filters op rijen of kolommen zijn.</span><span class="sxs-lookup"><span data-stu-id="d9091-353">Datasets can be subsetted by using logical filters on either rows or columns.</span></span> <span data-ttu-id="d9091-354">In veel gevallen zijn complexe filtercriteria vereist.</span><span class="sxs-lookup"><span data-stu-id="d9091-354">In many cases, complex filter criteria will be required.</span></span> <span data-ttu-id="d9091-355">Hallo verwijzingen naar naamruimtes in [bijlage B – Lees hier meer over](#appendixb) uitgebreide voorbeelden voor het filteren van dataframes bevatten.</span><span class="sxs-lookup"><span data-stu-id="d9091-355">hello references in [Appendix B - Further reading](#appendixb) contain extensive examples of filtering dataframes.</span></span>  

<span data-ttu-id="d9091-356">Er is één bit van het filter moet worden uitgevoerd op onze gegevensset.</span><span class="sxs-lookup"><span data-stu-id="d9091-356">There is one bit of filtering we should do on our dataset.</span></span> <span data-ttu-id="d9091-357">Als u Hallo kolommen in Hallo cadairydata dataframe bekijkt, ziet u twee overbodige kolommen.</span><span class="sxs-lookup"><span data-stu-id="d9091-357">If you look at hello columns in hello cadairydata dataframe, you will see two unnecessary columns.</span></span> <span data-ttu-id="d9091-358">de eerste kolom Hallo bevat alleen een rijnummer, niet erg nuttig is.</span><span class="sxs-lookup"><span data-stu-id="d9091-358">hello first column just holds a row number, which is not very useful.</span></span> <span data-ttu-id="d9091-359">Hallo tweede kolom Year.Month, bevat redundante gegevens.</span><span class="sxs-lookup"><span data-stu-id="d9091-359">hello second column, Year.Month, contains redundant information.</span></span> <span data-ttu-id="d9091-360">We kunnen deze kolommen eenvoudig uitsluiten door Hallo R code te volgen.</span><span class="sxs-lookup"><span data-stu-id="d9091-360">We can easily exclude these columns by using hello following R code.</span></span>

> [!NOTE]
> <span data-ttu-id="d9091-361">Vanaf nu op in deze sectie net leest u Hallo aanvullende code ik toe te in Hallo voegen [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="d9091-361">From now on in this section, I will just show you hello additional code I am adding in hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="d9091-362">Ik zal elke nieuwe regel toevoegen **voordat** hello `str()` functie.</span><span class="sxs-lookup"><span data-stu-id="d9091-362">I will add each new line **before** hello `str()` function.</span></span> <span data-ttu-id="d9091-363">Ik gebruik deze functie tooverify mijn resultaten in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="d9091-363">I use this function tooverify my results in Azure Machine Learning Studio.</span></span>
> 
> 

<span data-ttu-id="d9091-364">Ik toevoegen na toomy R coderegel in Hallo Hallo [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="d9091-364">I add hello following line toomy R code in hello [Execute R Script][execute-r-script] module.</span></span>

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

<span data-ttu-id="d9091-365">Deze code in uw experiment uitvoeren en controleren van Hallo resultaat uit Hallo-logboek voor uitvoer.</span><span class="sxs-lookup"><span data-stu-id="d9091-365">Run this code in your experiment and check hello result from hello output log.</span></span> <span data-ttu-id="d9091-366">Deze resultaten worden weergegeven in afbeelding 11.</span><span class="sxs-lookup"><span data-stu-id="d9091-366">These results are shown in Figure 11.</span></span>

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
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="d9091-367">*Afbeelding 11. Samenvatting van Hallo dataframe met twee kolommen die zijn verwijderd.*</span><span class="sxs-lookup"><span data-stu-id="d9091-367">*Figure 11. Summary of hello dataframe with two columns removed.*</span></span>

<span data-ttu-id="d9091-368">Goed nieuws!</span><span class="sxs-lookup"><span data-stu-id="d9091-368">Good news!</span></span> <span data-ttu-id="d9091-369">We ophalen Hallo verwacht resultaten.</span><span class="sxs-lookup"><span data-stu-id="d9091-369">We get hello expected results.</span></span>

### <a name="add-a-new-column"></a><span data-ttu-id="d9091-370">Een nieuwe kolom toevoegen</span><span class="sxs-lookup"><span data-stu-id="d9091-370">Add a new column</span></span>
<span data-ttu-id="d9091-371">toocreate time series modellen handige toohave een kolom met maanden sinds het starten van de tijdreeks Hallo HALLO hallo zal zijn.</span><span class="sxs-lookup"><span data-stu-id="d9091-371">toocreate time series models it will be convenient toohave a column containing hello months since hello start of hello time series.</span></span> <span data-ttu-id="d9091-372">We gaan een nieuwe kolom 'Month.Count' maken.</span><span class="sxs-lookup"><span data-stu-id="d9091-372">We will create a new column 'Month.Count'.</span></span>

<span data-ttu-id="d9091-373">toohelp Hallo-code maken we onze eerste eenvoudige functie organiseren `num.month()`.</span><span class="sxs-lookup"><span data-stu-id="d9091-373">toohelp organize hello code we will create our first simple function, `num.month()`.</span></span> <span data-ttu-id="d9091-374">Deze functie toocreate een nieuwe kolom in Hallo dataframe wordt vervolgens toegepast.</span><span class="sxs-lookup"><span data-stu-id="d9091-374">We will then apply this function toocreate a new column in hello dataframe.</span></span> <span data-ttu-id="d9091-375">Hallo nieuwe code is als volgt.</span><span class="sxs-lookup"><span data-stu-id="d9091-375">hello new code is as follows.</span></span>

    ## Create a new column with hello month count
    ## Function toofind hello number of months from hello first
    ## month of hello time series
    num.month <- function(Year, Month) {
      ## Find hello starting year
      min.year  <- min(Year)

      ## Compute hello number of months from hello start of hello time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute hello new column for hello dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

<span data-ttu-id="d9091-376">Nu Hallo bijgewerkt experiment uitvoeren en Hallo uitvoer logboek tooview Hallo resultaten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d9091-376">Now run hello updated experiment and use hello output log tooview hello results.</span></span> <span data-ttu-id="d9091-377">Deze resultaten worden weergegeven in afbeelding 12.</span><span class="sxs-lookup"><span data-stu-id="d9091-377">These results are shown in Figure 12.</span></span>

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
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="d9091-378">*Afbeelding 12. Samenvatting van Hallo dataframe met extra Hallo-kolom.*</span><span class="sxs-lookup"><span data-stu-id="d9091-378">*Figure 12. Summary of hello dataframe with hello additional column.*</span></span>

<span data-ttu-id="d9091-379">Het lijkt dat alles werkt.</span><span class="sxs-lookup"><span data-stu-id="d9091-379">It looks like everything is working.</span></span> <span data-ttu-id="d9091-380">De nieuwe kolom Hallo met Hallo verwachte waarden hebben we in ons dataframe.</span><span class="sxs-lookup"><span data-stu-id="d9091-380">We have hello new column with hello expected values in our dataframe.</span></span>

### <a name="value-transformations"></a><span data-ttu-id="d9091-381">Waarde transformaties</span><span class="sxs-lookup"><span data-stu-id="d9091-381">Value transformations</span></span>
<span data-ttu-id="d9091-382">In deze sectie wordt we enkele eenvoudige transformaties op Hallo-waarden in een aantal Hallo kolommen van onze dataframe uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d9091-382">In this section we will perform some simple transformations on hello values in some of hello columns of our dataframe.</span></span> <span data-ttu-id="d9091-383">Hallo R taal ondersteunt bijna willekeurige waarde transformaties.</span><span class="sxs-lookup"><span data-stu-id="d9091-383">hello R language supports nearly arbitrary value transformations.</span></span> <span data-ttu-id="d9091-384">Hallo verwijzingen naar naamruimtes in [bijlage B - verdere lezen](#appendixb) uitgebreide voorbeelden bevatten.</span><span class="sxs-lookup"><span data-stu-id="d9091-384">hello references in [Appendix B - Further Reading](#appendixb) contain extensive examples.</span></span>

<span data-ttu-id="d9091-385">Als u hello waarden in Hallo samenvattingen van onze dataframe bekijkt ziet u iets oneven hier.</span><span class="sxs-lookup"><span data-stu-id="d9091-385">If you look at hello values in hello summaries of our dataframe you should see something odd here.</span></span> <span data-ttu-id="d9091-386">Is meer ijs dan melk geproduceerd in Californië?</span><span class="sxs-lookup"><span data-stu-id="d9091-386">Is more ice cream than milk produced in California?</span></span> <span data-ttu-id="d9091-387">Nee, natuurlijk niet, omdat dit geen zin jammer als dit feit mogelijk toosome van ons ijs Ontwikkelaarshulpmiddelen.</span><span class="sxs-lookup"><span data-stu-id="d9091-387">No, of course not, as this makes no sense, sad as this fact may be toosome of us ice cream lovers.</span></span> <span data-ttu-id="d9091-388">Hallo eenheden zijn verschillend.</span><span class="sxs-lookup"><span data-stu-id="d9091-388">hello units are different.</span></span> <span data-ttu-id="d9091-389">Er is een Hallo prijs in eenheden van ons pond, melk is in eenheden van 1 M VS pond, ijs in eenheden van 1000 ons gallon en Kwark in eenheden van 1000 VS pond is.</span><span class="sxs-lookup"><span data-stu-id="d9091-389">hello price is in units of US pounds, milk is in units of 1 M US pounds, ice cream is in units of 1,000 US gallons, and cottage cheese is in units of 1,000 US pounds.</span></span> <span data-ttu-id="d9091-390">Ervan uitgaande dat ijs weegt ongeveer 6,5 pond per gallon, kunnen we eenvoudig Hallo vermenigvuldiging tooconvert deze waarden, zodat ze allemaal in gelijk eenheden van 1000 pond.</span><span class="sxs-lookup"><span data-stu-id="d9091-390">Assuming ice cream weighs about 6.5 pounds per gallon, we can easily do hello multiplication tooconvert these values so they are all in equal units of 1,000 pounds.</span></span>

<span data-ttu-id="d9091-391">We gebruiken een Multiplicatieve model voor het trendanalyse en correctie van deze gegevens voor onze prognosemodel.</span><span class="sxs-lookup"><span data-stu-id="d9091-391">For our forecasting model we use a multiplicative model for trend and seasonal adjustment of this data.</span></span> <span data-ttu-id="d9091-392">Een transformatie logboek kan we toouse een lineaire model, dit proces vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="d9091-392">A log transformation allows us toouse a linear model, simplifying this process.</span></span> <span data-ttu-id="d9091-393">Hallo logboek transformatie in dezelfde functie waarin Hallo vermenigvuldiger is toegepast Hallo kan worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="d9091-393">We can apply hello log transformation in hello same function where hello multiplier is applied.</span></span>

<span data-ttu-id="d9091-394">Ik Definieer in Hallo code te volgen, een nieuwe functie `log.transform()`, en deze toohello rijen met Hallo numerieke waarden toe te passen.</span><span class="sxs-lookup"><span data-stu-id="d9091-394">In hello following code, I define a new function, `log.transform()`, and apply it toohello rows containing hello numerical values.</span></span> <span data-ttu-id="d9091-395">Hallo R `Map()` functie is gebruikte tooapply hello `log.transform()` functie toohello kolommen van Hallo dataframe geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="d9091-395">hello R `Map()` function is used tooapply hello `log.transform()` function toohello selected columns of hello dataframe.</span></span> <span data-ttu-id="d9091-396">`Map()`lijkt te`apply()` maar kunt u meer dan een lijst met argumenten toohello functie.</span><span class="sxs-lookup"><span data-stu-id="d9091-396">`Map()` is similar too`apply()` but allows for more than one list of arguments toohello function.</span></span> <span data-ttu-id="d9091-397">Opmerking dat een lijst met ze het tweede argument toohello Hallo levert `log.transform()` functie.</span><span class="sxs-lookup"><span data-stu-id="d9091-397">Note that a list of multipliers supplies hello second argument toohello `log.transform()` function.</span></span> <span data-ttu-id="d9091-398">Hallo `na.omit()` functie wordt gebruikt als een beetje van opschonen tooensure is er geen ontbreekt of niet-gedefinieerde waarden in Hallo dataframe.</span><span class="sxs-lookup"><span data-stu-id="d9091-398">hello `na.omit()` function is used as a bit of cleanup tooensure we do not have missing or undefined values in hello dataframe.</span></span>

    log.transform <- function(invec, multiplier = 1) {
      ## Function for hello transformation, which is hello log
      ## of hello input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments toofunction log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier toofuncition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check hello input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap hello multiplication in tryCatch
      ## If there is an exception, print hello warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply hello transformation function toohello 4 columns
    ## of hello dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

<span data-ttu-id="d9091-399">Er is zeer bits gebeurt in Hallo `log.transform()` functie.</span><span class="sxs-lookup"><span data-stu-id="d9091-399">There is quite a bit happening in hello `log.transform()` function.</span></span> <span data-ttu-id="d9091-400">De meeste van deze code is controleren op mogelijke problemen met Hallo argumenten of omgaan met uitzonderingen die nog steeds tijdens het Hallo-berekeningen optreden kunnen.</span><span class="sxs-lookup"><span data-stu-id="d9091-400">Most of this code is checking for potential problems with hello arguments or dealing with exceptions, which can still arise during hello computations.</span></span> <span data-ttu-id="d9091-401">Slechts een paar regels van deze code daadwerkelijk Hallo berekeningen.</span><span class="sxs-lookup"><span data-stu-id="d9091-401">Only a few lines of this code actually do hello computations.</span></span>

<span data-ttu-id="d9091-402">Hallo-doel van Hallo defensive programmering is tooprevent Hallo uitvallen van één functie die voorkomt dat de verwerking niet door kan gaan.</span><span class="sxs-lookup"><span data-stu-id="d9091-402">hello goal of hello defensive programming is tooprevent hello failure of a single function that prevents processing from continuing.</span></span> <span data-ttu-id="d9091-403">Een plotselinge storing van een analyse langlopende kan frustrerend behoorlijk voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d9091-403">An abrupt failure of a long-running analysis can be quite frustrating for users.</span></span> <span data-ttu-id="d9091-404">Deze situatie retourwaarden moeten worden gekozen die standaard wordt beperkt tooavoid toodownstream verwerking beschadigen.</span><span class="sxs-lookup"><span data-stu-id="d9091-404">tooavoid this situation, default return values must be chosen that will limit damage toodownstream processing.</span></span> <span data-ttu-id="d9091-405">Een bericht is ook geproduceerde tooalert gebruikers die er iets verkeerd is geworden.</span><span class="sxs-lookup"><span data-stu-id="d9091-405">A message is also produced tooalert users that something has gone wrong.</span></span>

<span data-ttu-id="d9091-406">Als u niet gebruikte toodefensive programmering in R, zijn alle deze code lijkt enigszins overweldigend.</span><span class="sxs-lookup"><span data-stu-id="d9091-406">If you are not used toodefensive programming in R, all this code may seem a bit overwhelming.</span></span> <span data-ttu-id="d9091-407">Ik begeleidt u stapsgewijs door Hallo belangrijke stappen:</span><span class="sxs-lookup"><span data-stu-id="d9091-407">I will walk you through hello major steps:</span></span>

1. <span data-ttu-id="d9091-408">Een vector van vier berichten is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="d9091-408">A vector of four messages is defined.</span></span> <span data-ttu-id="d9091-409">Deze berichten zijn gebruikte toocommunicate informatie over een aantal Hallo mogelijke fouten en uitzonderingen die zich met deze code voordoen kunnen.</span><span class="sxs-lookup"><span data-stu-id="d9091-409">These messages are used toocommunicate information about some of hello possible errors and exceptions that can occur with this code.</span></span>
2. <span data-ttu-id="d9091-410">Ik retourneren NA de waarde voor elk geval.</span><span class="sxs-lookup"><span data-stu-id="d9091-410">I return a value of NA for each case.</span></span> <span data-ttu-id="d9091-411">Er zijn tal van andere mogelijkheden die mogelijk minder neveneffecten hebben.</span><span class="sxs-lookup"><span data-stu-id="d9091-411">There are many other possibilities that might have fewer side effects.</span></span> <span data-ttu-id="d9091-412">Ik kan een vector uit nullen of Hallo oorspronkelijke invoer aanvalsvector, bijvoorbeeld retourneren.</span><span class="sxs-lookup"><span data-stu-id="d9091-412">I could return a vector of zeroes, or hello original input vector, for example.</span></span>
3. <span data-ttu-id="d9091-413">Controles worden uitgevoerd op Hallo argumenten toohello functie.</span><span class="sxs-lookup"><span data-stu-id="d9091-413">Checks are run on hello arguments toohello function.</span></span> <span data-ttu-id="d9091-414">In elk geval als een fout wordt gedetecteerd, een standaardwaarde geretourneerd en wordt een bericht wordt geproduceerd door Hallo `warning()` functie.</span><span class="sxs-lookup"><span data-stu-id="d9091-414">In each case, if an error is detected, a default value is returned and a message is produced by hello `warning()` function.</span></span> <span data-ttu-id="d9091-415">Ik gebruik `warning()` plaats `stop()` als laatste Hallo uitvoering beëindigt, precies wat ik probeer tooavoid.</span><span class="sxs-lookup"><span data-stu-id="d9091-415">I am using `warning()` rather than `stop()` as hello latter will terminate execution, exactly what I am trying tooavoid.</span></span> <span data-ttu-id="d9091-416">Houd er rekening mee dat ik hebt geschreven deze code in een procedurele style, zoals in dit geval een functionele benadering leek complex en verborgen.</span><span class="sxs-lookup"><span data-stu-id="d9091-416">Note that I have written this code in a procedural style, as in this case a functional approach seemed complex and obscure.</span></span>
4. <span data-ttu-id="d9091-417">Hallo logboek-berekeningen zijn samengevoegd in `tryCatch()` zodat uitzonderingen niet een abrupte stilstand tooprocessing tot leidt.</span><span class="sxs-lookup"><span data-stu-id="d9091-417">hello log computations are wrapped in `tryCatch()` so that exceptions will not cause an abrupt halt tooprocessing.</span></span> <span data-ttu-id="d9091-418">Zonder `tryCatch()` de meeste fouten die worden gegenereerd door R functies resulteren in een stopsignaal ontvangen die geregeld worden.</span><span class="sxs-lookup"><span data-stu-id="d9091-418">Without `tryCatch()` most errors raised by R functions result in a stop signal, which does just that.</span></span>

<span data-ttu-id="d9091-419">Deze R-code in uw experiment uitvoeren en bekijkt hello uitvoer in Hallo uitvoer.log bestand afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="d9091-419">Execute this R code in your experiment and have a look at hello printed output in hello output.log file.</span></span> <span data-ttu-id="d9091-420">U ziet nu Hallo getransformeerd waarden Hallo vier kolommen in Hallo zich aanmeldt, zoals wordt weergegeven in afbeelding 13.</span><span class="sxs-lookup"><span data-stu-id="d9091-420">You will now see hello transformed values of hello four columns in hello log, as shown in Figure 13.</span></span>

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
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="d9091-421">*Afbeelding 13. Samenvatting van Hallo getransformeerd waarden in Hallo dataframe.*</span><span class="sxs-lookup"><span data-stu-id="d9091-421">*Figure 13. Summary of hello transformed values in hello dataframe.*</span></span>

<span data-ttu-id="d9091-422">We zien Hallo waarden zijn getransformeerd.</span><span class="sxs-lookup"><span data-stu-id="d9091-422">We see hello values have been transformed.</span></span> <span data-ttu-id="d9091-423">Melkproductie nu is aanzienlijk groter dan alle andere melkkoeien product productie, terughalen dat we nu een logaritmische schaal kijkt.</span><span class="sxs-lookup"><span data-stu-id="d9091-423">Milk production now greatly exceeds all other dairy product production, recalling that we are now looking at a log scale.</span></span>

<span data-ttu-id="d9091-424">Op dit moment onze gegevens wordt opgeschoond en we klaar zijn voor sommige modellen.</span><span class="sxs-lookup"><span data-stu-id="d9091-424">At this point our data is cleaned up and we are ready for some modeling.</span></span> <span data-ttu-id="d9091-425">Bekijkt hello visualisatie samenvatting voor Hallo resultaat gegevensset uitvoer van onze [R-Script uitvoeren] [ execute-r-script] -module, ziet u Hallo 'Maand' kolom 'Categorical' met 12 unieke waarden, weer is, net zoals we wilden .</span><span class="sxs-lookup"><span data-stu-id="d9091-425">Looking at hello visualization summary for hello Result Dataset output of our [Execute R Script][execute-r-script] module, you will see hello 'Month' column is 'Categorical' with 12 unique values, again, just as we wanted.</span></span>

## <span data-ttu-id="d9091-426"><a id="timeseries"></a>Time series-objecten en correlatieanalyse</span><span class="sxs-lookup"><span data-stu-id="d9091-426"><a id="timeseries"></a>Time series objects and correlation analysis</span></span>
<span data-ttu-id="d9091-427">In deze sectie we enkele eenvoudige R time series-objecten te verkennen en analyseren Hallo correlaties tussen sommige Hallo variabelen.</span><span class="sxs-lookup"><span data-stu-id="d9091-427">In this section we will explore a few basic R time series objects and analyze hello correlations between some of hello variables.</span></span> <span data-ttu-id="d9091-428">Ons doel is een dataframe daarin Hallo pairwise correlatie informatie op verschillende lag toooutput.</span><span class="sxs-lookup"><span data-stu-id="d9091-428">Our goal is toooutput a dataframe containing hello pairwise correlation information at several lags.</span></span>

<span data-ttu-id="d9091-429">Hallo volledige R-code voor deze sectie wordt Hallo zip-bestand die u eerder hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="d9091-429">hello complete R code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="time-series-objects-in-r"></a><span data-ttu-id="d9091-430">Time series-objecten in R</span><span class="sxs-lookup"><span data-stu-id="d9091-430">Time series objects in R</span></span>
<span data-ttu-id="d9091-431">Zoals al is vermeld, tijd reeksen al een reeks gegevenswaarden geïndexeerd door tijd zijn.</span><span class="sxs-lookup"><span data-stu-id="d9091-431">As already mentioned, time series are a series of data values indexed by time.</span></span> <span data-ttu-id="d9091-432">R time series-objecten zijn gebruikte toocreate en Hallo tijdsindex beheren.</span><span class="sxs-lookup"><span data-stu-id="d9091-432">R time series objects are used toocreate and manage hello time index.</span></span> <span data-ttu-id="d9091-433">Er zijn enkele voordelen toousing time series-objecten.</span><span class="sxs-lookup"><span data-stu-id="d9091-433">There are several advantages toousing time series objects.</span></span> <span data-ttu-id="d9091-434">Time series-objecten vrij u van Hallo veel details van het beheer van Hallo reeks index tijdwaarden die worden ingekapseld in Hallo-object.</span><span class="sxs-lookup"><span data-stu-id="d9091-434">Time series objects free you from hello many details of managing hello time series index values that are encapsulated in hello object.</span></span> <span data-ttu-id="d9091-435">Bovendien kunnen time series-objecten u toouse Hallo veel tijd reeks methoden voor het uitzetten, afdrukken, modellering, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="d9091-435">In addition, time series objects allow you toouse hello many time series methods for plotting, printing, modeling, etc.</span></span>

<span data-ttu-id="d9091-436">Hallo POSIXct time series-klasse wordt vaak gebruikt en relatief eenvoudig is.</span><span class="sxs-lookup"><span data-stu-id="d9091-436">hello POSIXct time series class is commonly used and is relatively simple.</span></span> <span data-ttu-id="d9091-437">Deze time series-klasse metingen tijd uit Hallo Hallo epoche, 1 januari 1970 is gestart.</span><span class="sxs-lookup"><span data-stu-id="d9091-437">This time series class measures time from hello start of hello epoch, January 1, 1970.</span></span> <span data-ttu-id="d9091-438">In dit voorbeeld gebruiken we POSIXct time series-objecten.</span><span class="sxs-lookup"><span data-stu-id="d9091-438">We will use POSIXct time series objects in this example.</span></span> <span data-ttu-id="d9091-439">Andere klassen gebruikte R time series-object zijn zoo en xts, uitbreidbare tijdreeks.</span><span class="sxs-lookup"><span data-stu-id="d9091-439">Other widely used R time series object classes include zoo and xts, extensible time series.</span></span>
<!-- Additional information on R time series objects is provided in hello references in Section 5.7. [commenting because this section doesn't exist, even in hello original] -->

### <a name="time-series-object-example"></a><span data-ttu-id="d9091-440">Voorbeeld van een reeks object tijd</span><span class="sxs-lookup"><span data-stu-id="d9091-440">Time series object example</span></span>
<span data-ttu-id="d9091-441">Laten we aan de slag met het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="d9091-441">Let's get started with our example.</span></span> <span data-ttu-id="d9091-442">Slepen en neerzetten een **nieuwe** [R-Script uitvoeren] [ execute-r-script] module in uw experiment.</span><span class="sxs-lookup"><span data-stu-id="d9091-442">Drag and drop a **new** [Execute R Script][execute-r-script] module into your experiment.</span></span> <span data-ttu-id="d9091-443">Verbinding maken met de uitvoerpoort Hallo resultaat Dataset1 van bestaande Hallo [R-Script uitvoeren] [ execute-r-script] module toohello Dataset1 invoer-poort van de nieuwe Hallo [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="d9091-443">Connect hello Result Dataset1 output port of hello existing [Execute R Script][execute-r-script] module toohello Dataset1 input port of hello new [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="d9091-444">Zoals ik deed voor de eerste voorbeelden hello, als er voortgang via Hallo bijvoorbeeld op bepaalde tijdstippen leest alleen Hallo incrementele extra regels met R code bij elke stap.</span><span class="sxs-lookup"><span data-stu-id="d9091-444">As I did for hello first examples, as we progress through hello example, at some points I will show only hello incremental additional lines of R code at each step.</span></span>  

#### <a name="reading-hello-dataframe"></a><span data-ttu-id="d9091-445">Hallo dataframe lezen</span><span class="sxs-lookup"><span data-stu-id="d9091-445">Reading hello dataframe</span></span>
<span data-ttu-id="d9091-446">Als eerste stap gaan we lezen in een dataframe en controleer of dat we Hallo verwacht resultaten krijgt.</span><span class="sxs-lookup"><span data-stu-id="d9091-446">As a first step, let's read in a dataframe and make sure we get hello expected results.</span></span> <span data-ttu-id="d9091-447">Hallo volgende code moet doen Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="d9091-447">hello following code should do hello job.</span></span>

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check hello results

<span data-ttu-id="d9091-448">Voer nu Hallo experiment.</span><span class="sxs-lookup"><span data-stu-id="d9091-448">Now, run hello experiment.</span></span> <span data-ttu-id="d9091-449">Hallo-logboek van Hallo nieuwe R-Script uitvoeren vorm moet eruitzien als afbeelding 14.</span><span class="sxs-lookup"><span data-stu-id="d9091-449">hello log of hello new Execute R Script shape should look like Figure 14.</span></span>

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

<span data-ttu-id="d9091-450">*Afbeelding 14. Samenvatting van Hallo dataframe module Hallo R-Script niet uitvoeren.*</span><span class="sxs-lookup"><span data-stu-id="d9091-450">*Figure 14. Summary of hello dataframe in hello Execute R Script module.*</span></span>

<span data-ttu-id="d9091-451">Deze gegevens zijn Hallo verwacht typen en opmaak.</span><span class="sxs-lookup"><span data-stu-id="d9091-451">This data is of hello expected types and format.</span></span> <span data-ttu-id="d9091-452">Houd er rekening mee dat het Hallo 'Maand' kolom van het type factor is en Hallo niveaus verwacht heeft.</span><span class="sxs-lookup"><span data-stu-id="d9091-452">Note that hello 'Month' column is of type factor and has hello expected number of levels.</span></span>

#### <a name="creating-a-time-series-object"></a><span data-ttu-id="d9091-453">Een time series-object maken</span><span class="sxs-lookup"><span data-stu-id="d9091-453">Creating a time series object</span></span>
<span data-ttu-id="d9091-454">Er moet een time series-object tooour dataframe tooadd.</span><span class="sxs-lookup"><span data-stu-id="d9091-454">We need tooadd a time series object tooour dataframe.</span></span> <span data-ttu-id="d9091-455">De huidige code Hallo vervangen door Hallo volgende, waarmee een nieuwe kolom van klasse POSIXct worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d9091-455">Replace hello current code with hello following, which adds a new column of class POSIXct.</span></span>

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check hello results

<span data-ttu-id="d9091-456">Controleer nu Hallo logboek.</span><span class="sxs-lookup"><span data-stu-id="d9091-456">Now, check hello log.</span></span> <span data-ttu-id="d9091-457">Het moet eruitzien als afbeelding 15.</span><span class="sxs-lookup"><span data-stu-id="d9091-457">It should look like Figure 15.</span></span>

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

<span data-ttu-id="d9091-458">*Afbeelding 15. Samenvatting van Hallo dataframe met een time series-object.*</span><span class="sxs-lookup"><span data-stu-id="d9091-458">*Figure 15. Summary of hello dataframe with a time series object.*</span></span>

<span data-ttu-id="d9091-459">We zien van Hallo samenvatting dat die nieuwe Hallo-kolom is in feite van klasse POSIXct.</span><span class="sxs-lookup"><span data-stu-id="d9091-459">We can see from hello summary that hello new column is in fact of class POSIXct.</span></span>

### <a name="exploring-and-transforming-hello-data"></a><span data-ttu-id="d9091-460">Verkennen en Hallo gegevens transformeren</span><span class="sxs-lookup"><span data-stu-id="d9091-460">Exploring and transforming hello data</span></span>
<span data-ttu-id="d9091-461">We gaan verkennen aantal Hallo variabelen in deze dataset.</span><span class="sxs-lookup"><span data-stu-id="d9091-461">Let's explore some of hello variables in this dataset.</span></span> <span data-ttu-id="d9091-462">Een matrix scatterplot is een uitstekende manier tooproduce een beknopte beschrijving.</span><span class="sxs-lookup"><span data-stu-id="d9091-462">A scatterplot matrix is a good way tooproduce a quick look.</span></span> <span data-ttu-id="d9091-463">Ik ben Hallo vervangen `str()` functie in de vorige R-code Hallo Hello volgt regel.</span><span class="sxs-lookup"><span data-stu-id="d9091-463">I am replacing hello `str()` function in hello previous R code with hello following line.</span></span>

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

<span data-ttu-id="d9091-464">Voer deze code en kijk wat er gebeurt.</span><span class="sxs-lookup"><span data-stu-id="d9091-464">Run this code and see what happens.</span></span> <span data-ttu-id="d9091-465">Hallo tekent geproduceerd Hallo poort R-apparaat moet eruitzien als afbeelding 16.</span><span class="sxs-lookup"><span data-stu-id="d9091-465">hello plot produced at hello R Device port should look like Figure 16.</span></span>

![Matrix van geselecteerde variabelen Scatterplot][17]

<span data-ttu-id="d9091-467">*Afbeelding 16. Scatterplot matrix van geselecteerde variabelen.*</span><span class="sxs-lookup"><span data-stu-id="d9091-467">*Figure 16. Scatterplot matrix of selected variables.*</span></span>

<span data-ttu-id="d9091-468">Er is een aantal vreemd uitziet structuur in Hallo relaties tussen deze variabelen.</span><span class="sxs-lookup"><span data-stu-id="d9091-468">There is some odd-looking structure in hello relationships between these variables.</span></span> <span data-ttu-id="d9091-469">Misschien dit probleem doet zich van trends in Hallo gegevens en Hallo feit dat we hebben Hallo variabelen niet gestandaardiseerd.</span><span class="sxs-lookup"><span data-stu-id="d9091-469">Perhaps this arises from trends in hello data and from hello fact that we have not standardized hello variables.</span></span>

### <a name="correlation-analysis"></a><span data-ttu-id="d9091-470">Correlatieanalyse</span><span class="sxs-lookup"><span data-stu-id="d9091-470">Correlation analysis</span></span>
<span data-ttu-id="d9091-471">tooperform correlatieanalyse moeten we tooboth ongedaan trend en standaardiseren Hallo-variabelen.</span><span class="sxs-lookup"><span data-stu-id="d9091-471">tooperform correlation analysis we need tooboth de-trend and standardize hello variables.</span></span> <span data-ttu-id="d9091-472">Hallo R kan alleen worden gebruikt `scale()` functie, die zowel datacenters en het schalen van variabelen.</span><span class="sxs-lookup"><span data-stu-id="d9091-472">We could simply use hello R `scale()` function, which both centers and scales variables.</span></span> <span data-ttu-id="d9091-473">Deze functie mogelijk ook sneller worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d9091-473">This function might well run faster.</span></span> <span data-ttu-id="d9091-474">Echter, ik wil dat tooshow u een voorbeeld van defensive programing in R.</span><span class="sxs-lookup"><span data-stu-id="d9091-474">However, I want tooshow you an example of defensive programing in R.</span></span>

<span data-ttu-id="d9091-475">Hallo `ts.detrend()` functie hieronder beide van deze bewerkingen uitvoert.</span><span class="sxs-lookup"><span data-stu-id="d9091-475">hello `ts.detrend()` function shown below performs both of these operations.</span></span> <span data-ttu-id="d9091-476">Hallo volgende twee regels code ongedaan trend Hallo gegevens en vervolgens standaardiseren Hallo waarden.</span><span class="sxs-lookup"><span data-stu-id="d9091-476">hello following two lines of code de-trend hello data and then standardize hello values.</span></span>

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function toode-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time toohave hello same length',
                    'ERROR: ts.detrend requires argument ts toobe of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros tooreturn as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # hello input arguments are not of hello same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If hello ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If hello ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that hello Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend hello time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply hello detrend.ts function toohello variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot hello results toolook at hello relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

<span data-ttu-id="d9091-477">Er is zeer bits gebeurt in Hallo `ts.detrend()` functie.</span><span class="sxs-lookup"><span data-stu-id="d9091-477">There is quite a bit happening in hello `ts.detrend()` function.</span></span> <span data-ttu-id="d9091-478">De meeste van deze code is controleren op mogelijke problemen met Hallo argumenten of omgaan met uitzonderingen die nog steeds tijdens het Hallo-berekeningen optreden kunnen.</span><span class="sxs-lookup"><span data-stu-id="d9091-478">Most of this code is checking for potential problems with hello arguments or dealing with exceptions, which can still arise during hello computations.</span></span> <span data-ttu-id="d9091-479">Slechts een paar regels van deze code daadwerkelijk Hallo berekeningen.</span><span class="sxs-lookup"><span data-stu-id="d9091-479">Only a few lines of this code actually do hello computations.</span></span>

<span data-ttu-id="d9091-480">We hebben al een voorbeeld van defensive programmering in besproken [transformaties waarde](#valuetransformations).</span><span class="sxs-lookup"><span data-stu-id="d9091-480">We have already discussed an example of defensive programming in [Value transformations](#valuetransformations).</span></span> <span data-ttu-id="d9091-481">Beide blokken berekening zijn samengevoegd in `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="d9091-481">Both computation blocks are wrapped in `tryCatch()`.</span></span> <span data-ttu-id="d9091-482">Voor een aantal fouten op deze manier zin tooreturn Hallo oorspronkelijke invoer vector en in andere gevallen ik een vector nullen retourneren.</span><span class="sxs-lookup"><span data-stu-id="d9091-482">For some errors it makes sense tooreturn hello original input vector, and in other cases, I return a vector of zeros.</span></span>  

<span data-ttu-id="d9091-483">Houd er rekening mee dat Hallo lineaire regressie gebruikt voor trending ongedaan een reeks tijd regressie.</span><span class="sxs-lookup"><span data-stu-id="d9091-483">Note that hello linear regression used for de-trending is a time series regression.</span></span> <span data-ttu-id="d9091-484">Hallo manier variabele is een time series-object.</span><span class="sxs-lookup"><span data-stu-id="d9091-484">hello predictor variable is a time series object.</span></span>  

<span data-ttu-id="d9091-485">Eenmaal `ts.detrend()` is gedefinieerd we deze toe te passen toohello variabelen in onze dataframe van belang.</span><span class="sxs-lookup"><span data-stu-id="d9091-485">Once `ts.detrend()` is defined we apply it toohello variables of interest in our dataframe.</span></span> <span data-ttu-id="d9091-486">We moeten de resulterende lijst Hallo gemaakt door forceren `lapply()` toodata dataframe met behulp van `as.data.frame()`.</span><span class="sxs-lookup"><span data-stu-id="d9091-486">We must coerce hello resulting list created by `lapply()` toodata dataframe by using `as.data.frame()`.</span></span> <span data-ttu-id="d9091-487">Vanwege defensive aspecten van `ts.detrend()`, fout tooprocess een van de variabelen Hallo voorkomt niet dat corrigeren verwerking van Hallo anderen.</span><span class="sxs-lookup"><span data-stu-id="d9091-487">Because of defensive aspects of `ts.detrend()`, failure tooprocess one of hello variables will not prevent correct processing of hello others.</span></span>  

<span data-ttu-id="d9091-488">Hallo laatste regel van code maakt een pairwise scatterplot.</span><span class="sxs-lookup"><span data-stu-id="d9091-488">hello final line of code creates a pairwise scatterplot.</span></span> <span data-ttu-id="d9091-489">Hallo-resultaten van Hallo scatterplot worden na het uitvoeren van Hallo R code weergegeven in afbeelding 17.</span><span class="sxs-lookup"><span data-stu-id="d9091-489">After running hello R code, hello results of hello scatterplot are shown in Figure 17.</span></span>

![Pairwise scatterplot van ongedaan trendanalyse en gestandaardiseerde tijdreeks][18]

<span data-ttu-id="d9091-491">*Afbeelding 17. Pairwise scatterplot van ongedaan trendanalyse en gestandaardiseerde tijdreeks.*</span><span class="sxs-lookup"><span data-stu-id="d9091-491">*Figure 17. Pairwise scatterplot of de-trended and standardized time series.*</span></span>

<span data-ttu-id="d9091-492">U kunt deze resultaten toothose weergegeven in afbeelding 16 vergelijken.</span><span class="sxs-lookup"><span data-stu-id="d9091-492">You can compare these results toothose shown in Figure 16.</span></span> <span data-ttu-id="d9091-493">Hello trend verwijderd en variabelen gestandaardiseerd Hallo zien we veel minder structuur in Hallo relaties tussen deze variabelen.</span><span class="sxs-lookup"><span data-stu-id="d9091-493">With hello trend removed and hello variables standardized, we see a lot less structure in hello relationships between these variables.</span></span>

<span data-ttu-id="d9091-494">Hallo code toocompute Hallo correlaties als R ccf objecten is als volgt.</span><span class="sxs-lookup"><span data-stu-id="d9091-494">hello code toocompute hello correlations as R ccf objects is as follows.</span></span>

    ## A function toocompute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of hello pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute hello list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

<span data-ttu-id="d9091-495">Deze code wordt weergegeven in afbeelding 18 Hallo-logboek.</span><span class="sxs-lookup"><span data-stu-id="d9091-495">Running this code produces hello log shown in Figure 18.</span></span>

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

<span data-ttu-id="d9091-496">*Afbeelding 18. Lijst met ccf objecten uit Hallo pairwise correlatieanalyse.*</span><span class="sxs-lookup"><span data-stu-id="d9091-496">*Figure 18. List of ccf objects from hello pairwise correlation analysis.*</span></span>

<span data-ttu-id="d9091-497">Er is een waarde voor correlation voor elke vertraging.</span><span class="sxs-lookup"><span data-stu-id="d9091-497">There is a correlation value for each lag.</span></span> <span data-ttu-id="d9091-498">Geen van deze waarden correlatie is groot genoeg toobe aanzienlijke.</span><span class="sxs-lookup"><span data-stu-id="d9091-498">None of these correlation values is large enough toobe significant.</span></span> <span data-ttu-id="d9091-499">We kunnen daarom sluiten we elke variabele onafhankelijk kunnen model.</span><span class="sxs-lookup"><span data-stu-id="d9091-499">We can therefore conclude that we can model each variable independently.</span></span>

### <a name="output-a-dataframe"></a><span data-ttu-id="d9091-500">Een dataframe uitvoer</span><span class="sxs-lookup"><span data-stu-id="d9091-500">Output a dataframe</span></span>
<span data-ttu-id="d9091-501">We hebben Hallo pairwise correlaties berekend als een lijst met R ccf objecten.</span><span class="sxs-lookup"><span data-stu-id="d9091-501">We have computed hello pairwise correlations as a list of R ccf objects.</span></span> <span data-ttu-id="d9091-502">Dit vormt een bits van een probleem als resultaat gegevensset uitvoerpoort Hallo echt een dataframe vereist.</span><span class="sxs-lookup"><span data-stu-id="d9091-502">This presents a bit of a problem as hello Result Dataset output port really requires a dataframe.</span></span> <span data-ttu-id="d9091-503">Bovendien Hallo ccf object zelf een lijst en willen we alleen Hallo waarden in het eerste element van deze lijst, Hallo correlaties op Hallo Hallo verschillende lag.</span><span class="sxs-lookup"><span data-stu-id="d9091-503">Further, hello ccf object is itself a list and we want only hello values in hello first element of this list, hello correlations at hello various lags.</span></span>

<span data-ttu-id="d9091-504">Hallo code uitgepakt Hallo lag waarden uit de lijst Hallo ccf objecten, die zelf een lijst met te volgen.</span><span class="sxs-lookup"><span data-stu-id="d9091-504">hello following code extracts hello lag values from hello list of ccf objects, which are themselves lists.</span></span>

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with hello row names column and the
    ## correlation data frame and assign hello column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## hello following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

<span data-ttu-id="d9091-505">de eerste coderegel Hallo iets lastig is en een verklaring waarmee u inzicht.</span><span class="sxs-lookup"><span data-stu-id="d9091-505">hello first line of code is a bit tricky, and some explanation may help you understand it.</span></span> <span data-ttu-id="d9091-506">Hallo door werken hebben we Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="d9091-506">Working from hello inside out we have hello following:</span></span>

1. <span data-ttu-id="d9091-507">Hallo '**[[**'operator met Hallo argument'**1**' worden geselecteerd Hallo vector van correlaties op Hallo vertragingen bij het berekenen van Hallo eerste element van Hallo ccf objectenlijst.</span><span class="sxs-lookup"><span data-stu-id="d9091-507">hello '**[[**' operator with hello argument '**1**' selects hello vector of correlations at hello lags from hello first element of hello ccf object list.</span></span>
2. <span data-ttu-id="d9091-508">Hallo `do.call()` functie is van toepassing hello `rbind()` functie via Hallo elementen van Hallo lijst retourneert door `lapply()`.</span><span class="sxs-lookup"><span data-stu-id="d9091-508">hello `do.call()` function applies hello `rbind()` function over hello elements of hello list returns by `lapply()`.</span></span>
3. <span data-ttu-id="d9091-509">Hallo `data.frame()` functie koppelt Hallo resultaat geproduceerd door `do.call()` tooa dataframe.</span><span class="sxs-lookup"><span data-stu-id="d9091-509">hello `data.frame()` function coerces hello result produced by `do.call()` tooa dataframe.</span></span>

<span data-ttu-id="d9091-510">Houd er rekening mee dat Hallo rijnamen in een kolom van Hallo dataframe zijn.</span><span class="sxs-lookup"><span data-stu-id="d9091-510">Note that hello row names are in a column of hello dataframe.</span></span> <span data-ttu-id="d9091-511">In dat geval Hallo rijnamen behouden blijft wanneer ze de uitvoer van Hallo [R-Script uitvoeren][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="d9091-511">Doing so preserves hello row names when they are output from hello [Execute R Script][execute-r-script].</span></span>

<span data-ttu-id="d9091-512">Hallo-code wordt weergegeven in afbeelding 19 Hallo-uitvoer wanneer ik **Visualize** Hallo uitvoer op Hallo resultaat gegevensset poort.</span><span class="sxs-lookup"><span data-stu-id="d9091-512">Running hello code produces hello output shown in Figure 19 when I **Visualize** hello output at hello Result Dataset port.</span></span> <span data-ttu-id="d9091-513">Hallo rijnamen zijn in de eerste kolom hello, zoals bedoeld.</span><span class="sxs-lookup"><span data-stu-id="d9091-513">hello row names are in hello first column, as intended.</span></span>

![Uitvoer van de resultaten van Hallo correlatieanalyse][20]

<span data-ttu-id="d9091-515">*Afbeelding 19. Resultaten de uitvoer van Hallo correlatieanalyse.*</span><span class="sxs-lookup"><span data-stu-id="d9091-515">*Figure 19. Results output from hello correlation analysis.*</span></span>

## <span data-ttu-id="d9091-516"><a id="seasonalforecasting"></a>Time series-voorbeeld: seizoensgebonden prognose</span><span class="sxs-lookup"><span data-stu-id="d9091-516"><a id="seasonalforecasting"></a>Time series example: seasonal forecasting</span></span>
<span data-ttu-id="d9091-517">Onze gegevens is nu in een formulier dat geschikt is voor analyse en we hebben vastgesteld dat er zijn geen belangrijke correlatie tussen het Hallo-variabelen.</span><span class="sxs-lookup"><span data-stu-id="d9091-517">Our data is now in a form suitable for analysis, and we have determined there are no significant correlations between hello variables.</span></span> <span data-ttu-id="d9091-518">We gaan en maken van een tijdreeks prognose model.</span><span class="sxs-lookup"><span data-stu-id="d9091-518">Let's move on and create a time series forecasting model.</span></span> <span data-ttu-id="d9091-519">Met dit model wordt we forecast Californië melkproductie voor Hallo 12 maanden van 2013.</span><span class="sxs-lookup"><span data-stu-id="d9091-519">Using this model we will forecast California milk production for hello 12 months of 2013.</span></span>

<span data-ttu-id="d9091-520">Onze prognosemodel heeft twee componenten, een onderdeel van het trendanalyse en een seizoen onderdeel.</span><span class="sxs-lookup"><span data-stu-id="d9091-520">Our forecasting model will have two components, a trend component and a seasonal component.</span></span> <span data-ttu-id="d9091-521">Hallo voltooid prognose is Hallo product van deze twee componenten.</span><span class="sxs-lookup"><span data-stu-id="d9091-521">hello complete forecast is hello product of these two components.</span></span> <span data-ttu-id="d9091-522">Dit type model staat bekend als een Multiplicatieve model.</span><span class="sxs-lookup"><span data-stu-id="d9091-522">This type of model is known as a multiplicative model.</span></span> <span data-ttu-id="d9091-523">Hallo alternatief is een additieve model.</span><span class="sxs-lookup"><span data-stu-id="d9091-523">hello alternative is an additive model.</span></span> <span data-ttu-id="d9091-524">We hebben al een logboek transformatie toohello variabelen van belang, waardoor deze analyse tractable toegepast.</span><span class="sxs-lookup"><span data-stu-id="d9091-524">We have already applied a log transformation toohello variables of interest, which makes this analysis tractable.</span></span>

<span data-ttu-id="d9091-525">Hallo volledige R-code voor deze sectie wordt Hallo zip-bestand die u eerder hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="d9091-525">hello complete R code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="creating-hello-dataframe-for-analysis"></a><span data-ttu-id="d9091-526">Hallo dataframe voor analyse maken</span><span class="sxs-lookup"><span data-stu-id="d9091-526">Creating hello dataframe for analysis</span></span>
<span data-ttu-id="d9091-527">Voeg eerst een **nieuwe** [R-Script uitvoeren] [ execute-r-script] module tooyour experiment.</span><span class="sxs-lookup"><span data-stu-id="d9091-527">Start by adding a **new** [Execute R Script][execute-r-script] module tooyour experiment.</span></span> <span data-ttu-id="d9091-528">Verbinding maken met de Hallo **resultaat gegevensset** uitvoer van de bestaande Hallo [R-Script uitvoeren] [ execute-r-script] module toohello **Dataset1** invoer van de nieuwe module Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9091-528">Connect hello **Result Dataset** output of hello existing [Execute R Script][execute-r-script] module toohello **Dataset1** input of hello new module.</span></span> <span data-ttu-id="d9091-529">Hallo resultaat ziet er ongeveer als afbeelding 20.</span><span class="sxs-lookup"><span data-stu-id="d9091-529">hello result should look something like Figure 20.</span></span>

![Hallo experimenteren met Hallo nieuwe R-Script uitvoeren module toegevoegd][21]

<span data-ttu-id="d9091-531">*Afbeelding 20. Hallo experimenteren met Hallo nieuwe R-Script uitvoeren module toegevoegd.*</span><span class="sxs-lookup"><span data-stu-id="d9091-531">*Figure 20. hello experiment with hello new Execute R Script module added.*</span></span>

<span data-ttu-id="d9091-532">Als met Hallo correlatie analyses die we zojuist, moeten we tooadd een kolom met een POSIXct time series-object.</span><span class="sxs-lookup"><span data-stu-id="d9091-532">As with hello correlation analysis we just completed, we need tooadd a column with a POSIXct time series object.</span></span> <span data-ttu-id="d9091-533">Hallo volgende code wordt hiervoor alleen.</span><span class="sxs-lookup"><span data-stu-id="d9091-533">hello following code will do just this.</span></span>

    # If running in Machine Learning Studio, uncomment hello first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

<span data-ttu-id="d9091-534">Voer deze code en bekijkt hello logboek.</span><span class="sxs-lookup"><span data-stu-id="d9091-534">Run this code and look at hello log.</span></span> <span data-ttu-id="d9091-535">Hallo resultaat moet eruitzien als afbeelding 21.</span><span class="sxs-lookup"><span data-stu-id="d9091-535">hello result should look like Figure 21.</span></span>

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

<span data-ttu-id="d9091-536">*Afbeelding 21. Een samenvatting van Hallo dataframe.*</span><span class="sxs-lookup"><span data-stu-id="d9091-536">*Figure 21. A summary of hello dataframe.*</span></span>

<span data-ttu-id="d9091-537">Met dit resultaat we klaar toostart zijn onze analyse.</span><span class="sxs-lookup"><span data-stu-id="d9091-537">With this result, we are ready toostart our analysis.</span></span>

### <a name="create-a-training-dataset"></a><span data-ttu-id="d9091-538">Maken van een gegevensset training</span><span class="sxs-lookup"><span data-stu-id="d9091-538">Create a training dataset</span></span>
<span data-ttu-id="d9091-539">We moeten toocreate een gegevensset met de training met Hallo dataframe samengesteld.</span><span class="sxs-lookup"><span data-stu-id="d9091-539">With hello dataframe constructed we need toocreate a training dataset.</span></span> <span data-ttu-id="d9091-540">Deze gegevens omvatten alle Hallo opmerkingen, behalve de afgelopen 12, van Hallo jaar 2013, Hallo die onze testgegevensset is.</span><span class="sxs-lookup"><span data-stu-id="d9091-540">This data will include all of hello observations except hello last 12, of hello year 2013, which is our test dataset.</span></span> <span data-ttu-id="d9091-541">Hallo volgende subsets Hallo dataframe code en curve van Hallo melkkoeien productie- en variabelen maakt.</span><span class="sxs-lookup"><span data-stu-id="d9091-541">hello following code subsets hello dataframe and creates plots of hello dairy production and price variables.</span></span> <span data-ttu-id="d9091-542">Ik vervolgens curve van Hallo vier productie- en variabelen maken.</span><span class="sxs-lookup"><span data-stu-id="d9091-542">I then create plots of hello four production and price variables.</span></span> <span data-ttu-id="d9091-543">Anonieme functie gebruikte toodefine is sommige verbetert voor tekengebied en vervolgens doorlopen Hallo lijst Hallo andere twee argumenten met `Map()`.</span><span class="sxs-lookup"><span data-stu-id="d9091-543">An anonymous function is used toodefine some augments for plot, and then iterate over hello list of hello other two arguments with `Map()`.</span></span> <span data-ttu-id="d9091-544">Als u denkt u zijn die een voor de lus zou hebt gewerkt probleemloos hier, u juist zijn.</span><span class="sxs-lookup"><span data-stu-id="d9091-544">If you are thinking that a for loop would have worked fine here, you are correct.</span></span> <span data-ttu-id="d9091-545">Maar aangezien R is een functionele taal ik ben waarin u een functionele benadering.</span><span class="sxs-lookup"><span data-stu-id="d9091-545">But, since R is a functional language I am showing you a functional approach.</span></span>

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

<span data-ttu-id="d9091-546">Hallo-code wordt Hallo reeks tijdreeks van Hallo R-apparaat uitvoer weergegeven in afbeelding 22 grafieken.</span><span class="sxs-lookup"><span data-stu-id="d9091-546">Running hello code produces hello series of time series plots from hello R Device output shown in Figure 22.</span></span> <span data-ttu-id="d9091-547">Houd er rekening mee dat tijdas Hallo in eenheden van datums nice voordeel van het Hallo-tijd reeks methode tekenen.</span><span class="sxs-lookup"><span data-stu-id="d9091-547">Note that hello time axis is in units of dates, a nice benefit of hello time series plot method.</span></span>

![Eerste dag van time series curve van Californië melkkoeien productie- en -gegevens](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![Tweede van time series curve van Californië melkkoeien productie- en -gegevens](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![Derde van de time series curve van Californië melkkoeien productie- en -gegevens](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![Vierde van time series curve van Californië melkkoeien productie- en -gegevens](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

<span data-ttu-id="d9091-552">*Afbeelding 22. Time series curve van Californië zuivelproductie en gegevens voor de prijs.*</span><span class="sxs-lookup"><span data-stu-id="d9091-552">*Figure 22. Time series plots of California dairy production and price data.*</span></span>

### <a name="a-trend-model"></a><span data-ttu-id="d9091-553">Een model trend</span><span class="sxs-lookup"><span data-stu-id="d9091-553">A trend model</span></span>
<span data-ttu-id="d9091-554">Een time series-object en bekijkt hello gegevens heeft gehad dat het gemaakt, begint tooconstruct een model trend voor Hallo Californië melk productiegegevens.</span><span class="sxs-lookup"><span data-stu-id="d9091-554">Having created a time series object and having had a look at hello data, let's start tooconstruct a trend model for hello California milk production data.</span></span> <span data-ttu-id="d9091-555">We kunnen dit doen met een reeks tijd regressie.</span><span class="sxs-lookup"><span data-stu-id="d9091-555">We can do this with a time series regression.</span></span> <span data-ttu-id="d9091-556">Het is echter wissen uit Hallo tekent dat we wordt moet meer dan een tooaccurately richting en snijpunt model Hallo trend in Hallo trainingsgegevens waargenomen.</span><span class="sxs-lookup"><span data-stu-id="d9091-556">However, it is clear from hello plot that we will need more than a slope and intercept tooaccurately model hello observed trend in hello training data.</span></span>

<span data-ttu-id="d9091-557">Op kleine schaal Hallo Hallo gegevens opgegeven, ik zal Hallo-model voor de trend in RStudio maken en vervolgens knippen en plakken Hallo resulterende model in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d9091-557">Given hello small scale of hello data, I will build hello model for trend in RStudio and then cut and paste hello resulting model into Azure Machine Learning.</span></span> <span data-ttu-id="d9091-558">RStudio biedt een interactieve omgeving voor dit type interactieve analyses.</span><span class="sxs-lookup"><span data-stu-id="d9091-558">RStudio provides an interactive environment for this type of interactive analysis.</span></span>

<span data-ttu-id="d9091-559">Als een eerste poging probeer ik een polynomiale regressie met bevoegdheden up too3.</span><span class="sxs-lookup"><span data-stu-id="d9091-559">As a first attempt, I will try a polynomial regression with powers up too3.</span></span> <span data-ttu-id="d9091-560">Er is een echte gevaar voor dit soort modellen te veel aanpassen.</span><span class="sxs-lookup"><span data-stu-id="d9091-560">There is a real danger of over-fitting these kinds of models.</span></span> <span data-ttu-id="d9091-561">Daarom is het beste tooavoid hoge voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="d9091-561">Therefore, it is best tooavoid high order terms.</span></span> <span data-ttu-id="d9091-562">Hallo `I()` functie belemmert interpretatie van Hallo-inhoud (interpreteert Hallo inhoud 'omdat'), en kunt u een letterlijk geïnterpreteerde functie toowrite in een regressievergelijking.</span><span class="sxs-lookup"><span data-stu-id="d9091-562">hello `I()` function inhibits interpretation of hello contents (interprets hello contents 'as is') and allows you toowrite a literally interpreted function in a regression equation.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

<span data-ttu-id="d9091-563">Hiermee wordt de volgende Hallo gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="d9091-563">This generates hello following.</span></span>

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

<span data-ttu-id="d9091-564">Van P-waarden (Pr (> | t |)) in deze uitvoer kunt zien we dat Hallo mogelijk aanzienlijke gekwadrateerde term niet.</span><span class="sxs-lookup"><span data-stu-id="d9091-564">From P values (Pr(>|t|)) in this output, we can see that hello squared term may not be significant.</span></span> <span data-ttu-id="d9091-565">Ik gebruik Hallo `update()` toomodify dit model door weggehaald Hallo term kwadraat werken.</span><span class="sxs-lookup"><span data-stu-id="d9091-565">I will use hello `update()` function toomodify this model by dropping hello squared term.</span></span>

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

<span data-ttu-id="d9091-566">Hiermee wordt de volgende Hallo gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="d9091-566">This generates hello following.</span></span>

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

<span data-ttu-id="d9091-567">Dit ziet er beter.</span><span class="sxs-lookup"><span data-stu-id="d9091-567">This looks better.</span></span> <span data-ttu-id="d9091-568">Alle Hallo voorwaarden zijn van belang.</span><span class="sxs-lookup"><span data-stu-id="d9091-568">All of hello terms are significant.</span></span> <span data-ttu-id="d9091-569">Hallo 2e-16-waarde is echter een standaardwaarde, en moet niet ernstig te worden genomen.</span><span class="sxs-lookup"><span data-stu-id="d9091-569">However, hello 2e-16 value is a default value, and should not be taken too seriously.</span></span>  

<span data-ttu-id="d9091-570">Als een test sanity time series tekent Hallo Californië zuivelproductie gegevens we te maken met Hallo trend curve weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d9091-570">As a sanity test, let's make a time series plot of hello California dairy production data with hello trend curve shown.</span></span> <span data-ttu-id="d9091-571">Ik heb de volgende code in Azure Machine Learning Hallo Hallo toegevoegd [R-Script uitvoeren] [ execute-r-script] model (geen RStudio) toocreate Hallo model en tekent maken.</span><span class="sxs-lookup"><span data-stu-id="d9091-571">I have added hello following code in hello Azure Machine Learning [Execute R Script][execute-r-script] model (not RStudio) toocreate hello model and make a plot.</span></span> <span data-ttu-id="d9091-572">Hallo resultaat wordt weergegeven in afbeelding 23.</span><span class="sxs-lookup"><span data-stu-id="d9091-572">hello result is shown in Figure 23.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![Californië melk productiegegevens met trend model weergegeven](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

<span data-ttu-id="d9091-574">*Afbeelding 23. Californië melk trend model weergegeven met productiegegevens.*</span><span class="sxs-lookup"><span data-stu-id="d9091-574">*Figure 23. California milk production data with trend model shown.*</span></span>

<span data-ttu-id="d9091-575">Lijkt Hallo trend model Hallo gegevens vrij goed past.</span><span class="sxs-lookup"><span data-stu-id="d9091-575">It looks like hello trend model fits hello data fairly well.</span></span> <span data-ttu-id="d9091-576">Bovendien wordt lijkt er niet toobe bewijs van te veel aanpassen zoals oneven wiggles in Hallo model curve.</span><span class="sxs-lookup"><span data-stu-id="d9091-576">Further, there does not seem toobe evidence of over-fitting, such as odd wiggles in hello model curve.</span></span>  

### <a name="seasonal-model"></a><span data-ttu-id="d9091-577">Seizoensgebonden model</span><span class="sxs-lookup"><span data-stu-id="d9091-577">Seasonal model</span></span>
<span data-ttu-id="d9091-578">Een model van de trend in de hand, we toopush op moet en Hallo seizoensgebonden gevolgen zijn.</span><span class="sxs-lookup"><span data-stu-id="d9091-578">With a trend model in hand, we need toopush on and include hello seasonal effects.</span></span> <span data-ttu-id="d9091-579">Hallo maand van het Hallo jaar zullen worden gebruikt als een dummy-variabele Hallo lineair model toocapture Hallo per maand gelden.</span><span class="sxs-lookup"><span data-stu-id="d9091-579">We will use hello month of hello year as a dummy variable in hello linear model toocapture hello month-by-month effect.</span></span> <span data-ttu-id="d9091-580">Houd er rekening mee dat wanneer u factor variabelen in een model introduceren, Hallo intercept moet niet worden berekend.</span><span class="sxs-lookup"><span data-stu-id="d9091-580">Note that when you introduce factor variables into a model, hello intercept must not be computed.</span></span> <span data-ttu-id="d9091-581">Als u dit niet hebt, Hallo formule is te veel opgegeven R beëindigt een Hallo factoren gewenst maar Hallo intercept term houden.</span><span class="sxs-lookup"><span data-stu-id="d9091-581">If you do not do this, hello formula is over-specified and R will drop one of hello desired factors but keep hello intercept term.</span></span>

<span data-ttu-id="d9091-582">Aangezien we een model tevredenheid trend hebben we Hallo kunt gebruiken `update()` functie tooadd Hallo nieuwe termen toohello bestaande model.</span><span class="sxs-lookup"><span data-stu-id="d9091-582">Since we have a satisfactory trend model we can use hello `update()` function tooadd hello new terms toohello existing model.</span></span> <span data-ttu-id="d9091-583">Hallo -1 in Hallo update formule zakt Hallo intercept term.</span><span class="sxs-lookup"><span data-stu-id="d9091-583">hello -1 in hello update formula drops hello intercept term.</span></span> <span data-ttu-id="d9091-584">Als u doorgaat in RStudio voor Hallo moment:</span><span class="sxs-lookup"><span data-stu-id="d9091-584">Continuing in RStudio for hello moment:</span></span>

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

<span data-ttu-id="d9091-585">Hiermee wordt de volgende Hallo gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="d9091-585">This generates hello following.</span></span>

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

<span data-ttu-id="d9091-586">Ziet u dat model Hallo niet langer een term intercept heeft en 12 maand belangrijke factoren.</span><span class="sxs-lookup"><span data-stu-id="d9091-586">We see that hello model no longer has an intercept term and has 12 significant month factors.</span></span> <span data-ttu-id="d9091-587">Dit is precies wilden we toosee.</span><span class="sxs-lookup"><span data-stu-id="d9091-587">This is exactly what we wanted toosee.</span></span>

<span data-ttu-id="d9091-588">We maken een andere tijd reeks tekent van Hallo Californië zuivelproductie gegevens toosee hoe goed Hallo seizoensgebonden model werkt.</span><span class="sxs-lookup"><span data-stu-id="d9091-588">Let's make another time series plot of hello California dairy production data toosee how well hello seasonal model is working.</span></span> <span data-ttu-id="d9091-589">Ik heb de volgende code in Azure Machine Learning Hallo Hallo toegevoegd [R-Script uitvoeren] [ execute-r-script] toocreate Hallo model en tekent maken.</span><span class="sxs-lookup"><span data-stu-id="d9091-589">I have added hello following code in hello Azure Machine Learning [Execute R Script][execute-r-script] toocreate hello model and make a plot.</span></span>

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

<span data-ttu-id="d9091-590">Deze code uitgevoerd in Azure Machine Learning produceert Hallo grafiek wordt weergegeven in afbeelding 24.</span><span class="sxs-lookup"><span data-stu-id="d9091-590">Running this code in Azure Machine Learning produces hello plot shown in Figure 24.</span></span>

![Californië melkproductie met model inclusief seizoensgebonden effecten](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

<span data-ttu-id="d9091-592">*Afbeelding 24. Melkproductie Californië met model inclusief seizoensgebonden gevolgen.*</span><span class="sxs-lookup"><span data-stu-id="d9091-592">*Figure 24. California milk production with model including seasonal effects.*</span></span>

<span data-ttu-id="d9091-593">Hallo is aanpassen toohello gegevens weergegeven in afbeelding 24 in plaats van te bevorderen.</span><span class="sxs-lookup"><span data-stu-id="d9091-593">hello fit toohello data shown in Figure 24 is rather encouraging.</span></span> <span data-ttu-id="d9091-594">Hallo trend zowel Hallo invloed (maandelijks variatie) Zoek redelijke.</span><span class="sxs-lookup"><span data-stu-id="d9091-594">Both hello trend and hello seasonal effect (monthly variation) look reasonable.</span></span>

<span data-ttu-id="d9091-595">Als een nieuwe controle uit op het model, gaan we hebben bekijkt hello verschillen opgeven.</span><span class="sxs-lookup"><span data-stu-id="d9091-595">As another check on our model, let's have a look at hello residuals.</span></span> <span data-ttu-id="d9091-596">Hallo berekent de volgende code Hallo voorspelde waarden uit onze twee modellen, Hallo verschillen opgeven voor de seizoensgebonden model hello wordt berekend en vervolgens deze verschillen opgeven voor de trainingsgegevens Hallo worden uitgezet.</span><span class="sxs-lookup"><span data-stu-id="d9091-596">hello following code computes hello predicted values from our two models, computes hello residuals for hello seasonal model, and then plots these residuals for hello training data.</span></span>

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot hello residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

<span data-ttu-id="d9091-597">Hallo achtergebleven grafiek wordt weergegeven in afbeelding 25.</span><span class="sxs-lookup"><span data-stu-id="d9091-597">hello residual plot is shown in Figure 25.</span></span>

![Verschillen van de seizoensgebonden model Hallo voor Hallo trainingsgegevens opgeven](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

<span data-ttu-id="d9091-599">*Afbeelding 25. Als u dit van Hallo seizoensgebonden model voor Hallo trainingsgegevens.*</span><span class="sxs-lookup"><span data-stu-id="d9091-599">*Figure 25. Residuals of hello seasonal model for hello training data.*</span></span>

<span data-ttu-id="d9091-600">Deze verschillen opgeven zoeken redelijke.</span><span class="sxs-lookup"><span data-stu-id="d9091-600">These residuals look reasonable.</span></span> <span data-ttu-id="d9091-601">Er is geen specifieke structuur, met uitzondering van Hallo effect van Hallo 2008-2009 recessie, die het model wordt geen rekening gehouden met name goed.</span><span class="sxs-lookup"><span data-stu-id="d9091-601">There is no particular structure, except hello effect of hello 2008-2009 recession, which our model does not account for particularly well.</span></span>

<span data-ttu-id="d9091-602">Hallo-grafiek wordt weergegeven in afbeelding 25 is nuttig voor het detecteren van alle tijdsafhankelijke patronen in Hallo verschillen opgeven.</span><span class="sxs-lookup"><span data-stu-id="d9091-602">hello plot shown in Figure 25 is useful for detecting any time-dependent patterns in hello residuals.</span></span> <span data-ttu-id="d9091-603">Hallo expliciete benadering van computer- en uitzetten Hallo dit die ik gebruikt plaatst Hallo verschillen opgeven in volgorde van de tijd op Hallo tekent.</span><span class="sxs-lookup"><span data-stu-id="d9091-603">hello explicit approach of computing and plotting hello residuals I used places hello residuals in time order on hello plot.</span></span> <span data-ttu-id="d9091-604">Als op Hallo daarentegen ik had uitgezet `milk.lm$residuals`, Hallo tekent zou zijn niet in volgorde van de tijd.</span><span class="sxs-lookup"><span data-stu-id="d9091-604">If, on hello other hand, I had plotted `milk.lm$residuals`, hello plot would not have been in time order.</span></span>

<span data-ttu-id="d9091-605">U kunt ook `plot.lm()` tooproduce een reeks diagnostische waarnemingspunten.</span><span class="sxs-lookup"><span data-stu-id="d9091-605">You can also use `plot.lm()` tooproduce a series of diagnostic plots.</span></span>

    ## Show hello diagnostic plots for hello model
    plot(milk.lm2, ask = FALSE)

<span data-ttu-id="d9091-606">Deze code wordt een reeks diagnostische waarnemingspunten wordt weergegeven in afbeelding 26 geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="d9091-606">This code produces a series of diagnostic plots shown in Figure 26.</span></span>

![Eerste dag van diagnostische waarnemingspunten voor het seizoen Hallo-model](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Tweede van diagnostische waarnemingspunten voor Hallo seizoensgebonden model](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Derde van diagnostische waarnemingspunten voor het seizoen Hallo-model](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Vierde van diagnostische waarnemingspunten voor Hallo seizoensgebonden model](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

<span data-ttu-id="d9091-611">*Afbeelding 26. Diagnose worden uitgezet voor Hallo seizoensgebonden model.*</span><span class="sxs-lookup"><span data-stu-id="d9091-611">*Figure 26. Diagnostic plots for hello seasonal model.*</span></span>

<span data-ttu-id="d9091-612">Er zijn een aantal maximaal invloedrijke punten in deze waarnemingspunten, maar niets geïdentificeerd toocause geweldige zorgen.</span><span class="sxs-lookup"><span data-stu-id="d9091-612">There are a few highly influential points identified in these plots, but nothing toocause great concern.</span></span> <span data-ttu-id="d9091-613">Bovendien ziet u van Hallo normaal Q-Q tekent dat dit Hallo sluiten toonormally gedistribueerd, belangrijke verondersteld voor lineaire modellen zijn.</span><span class="sxs-lookup"><span data-stu-id="d9091-613">Further, we can see from hello Normal Q-Q plot that hello residuals are close toonormally distributed, an important assumption for linear models.</span></span>

### <a name="forecasting-and-model-evaluation"></a><span data-ttu-id="d9091-614">Prognosemodel en model evalueren</span><span class="sxs-lookup"><span data-stu-id="d9091-614">Forecasting and model evaluation</span></span>
<span data-ttu-id="d9091-615">Er is slechts één meer ding toodo toocomplete ons voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="d9091-615">There is just one more thing toodo toocomplete our example.</span></span> <span data-ttu-id="d9091-616">We moet toocompute prognoses en Hallo fout tegen Hallo actuele gegevens te meten.</span><span class="sxs-lookup"><span data-stu-id="d9091-616">We need toocompute forecasts and measure hello error against hello actual data.</span></span> <span data-ttu-id="d9091-617">Onze prognose worden voor Hallo 12 maanden van 2013.</span><span class="sxs-lookup"><span data-stu-id="d9091-617">Our forecast will be for hello 12 months of 2013.</span></span> <span data-ttu-id="d9091-618">We kunt een meting fout voor deze prognose toohello feitelijke gegevens die geen deel uitmaakt van onze gegevensset training berekenen.</span><span class="sxs-lookup"><span data-stu-id="d9091-618">We can compute an error measure for this forecast toohello actual data that is not part of our training dataset.</span></span> <span data-ttu-id="d9091-619">Daarnaast kunnen we vergelijken de prestaties van Hallo 18 jaar training gegevens toohello 12 maanden van testgegevens.</span><span class="sxs-lookup"><span data-stu-id="d9091-619">Additionally, we can compare performance on hello 18 years of training data toohello 12 months of test data.</span></span>  

<span data-ttu-id="d9091-620">Een aantal metrische gegevens gebruikt toomeasure Hallo prestaties van de time series-modellen.</span><span class="sxs-lookup"><span data-stu-id="d9091-620">A number of metrics are used toomeasure hello performance of time series models.</span></span> <span data-ttu-id="d9091-621">In ons geval gebruiken we Hallo root mean vierkant (RMS)-fout.</span><span class="sxs-lookup"><span data-stu-id="d9091-621">In our case we will use hello root mean square (RMS) error.</span></span> <span data-ttu-id="d9091-622">Hallo berekent volgende functie Hallo RMS fout tussen twee reeksen.</span><span class="sxs-lookup"><span data-stu-id="d9091-622">hello following function computes hello RMS error between two series.</span></span>  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function toocompute hello RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments toofunction RMS.error of wrong type encountered",
                    "ERROR: Input vector toofunction RMS.error is too short",
                    "ERROR: Input vectors toofunction RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check hello arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate hello values, else just copy
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

    ## Compute hello RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

<span data-ttu-id="d9091-623">Net als bij Hallo `log.transform()` functie besproken in sectie 'Transformaties waarde' hello, wordt er zeer veel fout controleren en uitzondering code voor herstel in deze functie.</span><span class="sxs-lookup"><span data-stu-id="d9091-623">As with hello `log.transform()` function we discussed in hello "Value transformations" section, there is quite a lot of error checking and exception recovery code in this function.</span></span> <span data-ttu-id="d9091-624">Hallo principes werkzaam zijn Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="d9091-624">hello principles employed are hello same.</span></span> <span data-ttu-id="d9091-625">Hallo werk wordt uitgevoerd op twee plaatsen die zijn ingepakt `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="d9091-625">hello work is done in two places wrapped in `tryCatch()`.</span></span> <span data-ttu-id="d9091-626">Hallo tijdreeks zijn eerst exponentiated, omdat we hebt gewerkt met Hallo logboeken van Hallo waarden.</span><span class="sxs-lookup"><span data-stu-id="d9091-626">First, hello time series are exponentiated, since we have been working with hello logs of hello values.</span></span> <span data-ttu-id="d9091-627">Ten tweede wordt Hallo werkelijke RMS fout berekend.</span><span class="sxs-lookup"><span data-stu-id="d9091-627">Second, hello actual RMS error is computed.</span></span>  

<span data-ttu-id="d9091-628">Uitgerust met een functie toomeasure Hallo RMS-fout, gaan we bouwen en de uitvoer een dataframe met Hallo RMS fouten.</span><span class="sxs-lookup"><span data-stu-id="d9091-628">Equipped with a function toomeasure hello RMS error, let's build and output a dataframe containing hello RMS errors.</span></span> <span data-ttu-id="d9091-629">Nemen we voorwaarden voor Hallo trend model alleen en Hallo volledig model met seizoensgebonden factoren.</span><span class="sxs-lookup"><span data-stu-id="d9091-629">We will include terms for hello trend model alone and hello complete model with seasonal factors.</span></span> <span data-ttu-id="d9091-630">Hallo volgende code Hallo taak met behulp van Hallo twee lineaire modellen die we hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d9091-630">hello following code does hello job by using hello two linear models we have constructed.</span></span>

    ## Compute hello RMS error in a dataframe
    ## Include hello row names in hello first column so they will
    ## appear in hello output of hello Execute R Script
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

    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

<span data-ttu-id="d9091-631">Deze code wordt Hallo-uitvoer die wordt weergegeven in afbeelding 27 op Hallo uitvoerpoort resultaat gegevensset.</span><span class="sxs-lookup"><span data-stu-id="d9091-631">Running this code produces hello output shown in Figure 27 at hello Result Dataset output port.</span></span>

![Vergelijking van RMS-fouten voor Hallo modellen][26]

<span data-ttu-id="d9091-633">*Afbeelding 27. Vergelijking van RMS-fouten voor Hallo-modellen.*</span><span class="sxs-lookup"><span data-stu-id="d9091-633">*Figure 27. Comparison of RMS errors for hello models.*</span></span>

<span data-ttu-id="d9091-634">Van deze resultaten ziet u dat toe te voegen Hallo seizoensgebonden factoren toohello model Hallo RMS-fout aanzienlijk vermindert.</span><span class="sxs-lookup"><span data-stu-id="d9091-634">From these results, we see that adding hello seasonal factors toohello model reduces hello RMS error significantly.</span></span> <span data-ttu-id="d9091-635">Te heten dan Hallo RMS-fout voor Hallo training gegevens een bits kleiner is dan voor Hallo prognose.</span><span class="sxs-lookup"><span data-stu-id="d9091-635">Not too surprisingly, hello RMS error for hello training data is a bit less than for hello forecast.</span></span>

## <span data-ttu-id="d9091-636"><a id="appendixa"></a>BIJLAGE A: Handleiding tooRStudio</span><span class="sxs-lookup"><span data-stu-id="d9091-636"><a id="appendixa"></a>APPENDIX A: Guide tooRStudio</span></span>
<span data-ttu-id="d9091-637">RStudio heel goed wordt gedocumenteerd, zodat in deze bijlage ik bieden sommige koppelingen toohello sleutel secties van Hallo RStudio documentatie tooget die u gestart.</span><span class="sxs-lookup"><span data-stu-id="d9091-637">RStudio is quite well documented, so in this appendix I will provide some links toohello key sections of hello RStudio documentation tooget you started.</span></span>

1. <span data-ttu-id="d9091-638">Projecten maken</span><span class="sxs-lookup"><span data-stu-id="d9091-638">Creating projects</span></span>
   
   <span data-ttu-id="d9091-639">U kunt ordenen en beheren van uw R-code in de projecten via RStudio.</span><span class="sxs-lookup"><span data-stu-id="d9091-639">You can organize and manage your R code into projects by using RStudio.</span></span> <span data-ttu-id="d9091-640">Hallo-documentatie die gebruikmaakt van de projecten kan worden gevonden op https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span><span class="sxs-lookup"><span data-stu-id="d9091-640">hello documentation that uses projects can be found at https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span></span>
   
   <span data-ttu-id="d9091-641">Ik het beste als volgt uit te voeren en maak een project voor Hallo R-codevoorbeelden in dit document.</span><span class="sxs-lookup"><span data-stu-id="d9091-641">I recommend that you follow these directions and create a project for hello R code examples in this document.</span></span>  
2. <span data-ttu-id="d9091-642">Bewerken en het uitvoeren van R-code</span><span class="sxs-lookup"><span data-stu-id="d9091-642">Editing and executing R code</span></span>
   
   <span data-ttu-id="d9091-643">RStudio biedt een geïntegreerde omgeving voor het bewerken en R-code wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d9091-643">RStudio provides an integrated environment for editing and executing R code.</span></span> <span data-ttu-id="d9091-644">Documentatie vindt u op https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span><span class="sxs-lookup"><span data-stu-id="d9091-644">Documentation can be found at https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span></span>
3. <span data-ttu-id="d9091-645">Foutopsporing</span><span class="sxs-lookup"><span data-stu-id="d9091-645">Debugging</span></span>
   
   <span data-ttu-id="d9091-646">RStudio omvat krachtige mogelijkheden voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="d9091-646">RStudio includes powerful debugging capabilities.</span></span> <span data-ttu-id="d9091-647">Documentatie voor deze functies is op https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span><span class="sxs-lookup"><span data-stu-id="d9091-647">Documentation for these features is at https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span></span>
   
   <span data-ttu-id="d9091-648">Hallo onderbrekingspunt voor probleemoplossing functies zijn tijdens https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting gedocumenteerd.</span><span class="sxs-lookup"><span data-stu-id="d9091-648">hello breakpoint troubleshooting features are documented at https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span></span>

## <span data-ttu-id="d9091-649"><a id="appendixb"></a>BIJLAGE B: Lees hier meer over</span><span class="sxs-lookup"><span data-stu-id="d9091-649"><a id="appendixb"></a>APPENDIX B: Further reading</span></span>
<span data-ttu-id="d9091-650">Deze zelfstudie behandelt Hallo basisbeginselen programming R van wat u moet toouse Hallo R taal met Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="d9091-650">This R programming tutorial covers hello basics of what you need toouse hello R language with Azure Machine Learning Studio.</span></span> <span data-ttu-id="d9091-651">Als u niet bekend met R bent, zijn twee inleidingen beschikbaar op CRAN:</span><span class="sxs-lookup"><span data-stu-id="d9091-651">If you are not familiar with R, two introductions are available on CRAN:</span></span>

* <span data-ttu-id="d9091-652">R voor beginnende gebruikers door Emmanuel Paradis is een goede plaats toostart op http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span><span class="sxs-lookup"><span data-stu-id="d9091-652">R for Beginners by Emmanuel Paradis is a good place toostart at http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span></span>  
* <span data-ttu-id="d9091-653">Een rondleiding inleiding door W. N.</span><span class="sxs-lookup"><span data-stu-id="d9091-653">An Introduction tooR by W. N.</span></span> <span data-ttu-id="d9091-654">Venables et.</span><span class="sxs-lookup"><span data-stu-id="d9091-654">Venables et.</span></span> <span data-ttu-id="d9091-655">al.</span><span class="sxs-lookup"><span data-stu-id="d9091-655">al.</span></span> <span data-ttu-id="d9091-656">in iets meer diepte op http://cran.r-project.org/doc/manuals/R-intro.html gaan.</span><span class="sxs-lookup"><span data-stu-id="d9091-656">goes into a bit more depth, at http://cran.r-project.org/doc/manuals/R-intro.html.</span></span>

<span data-ttu-id="d9091-657">Er zijn veel books op R waarmee u aan de slag kunt.</span><span class="sxs-lookup"><span data-stu-id="d9091-657">There are many books on R that can help you get started.</span></span> <span data-ttu-id="d9091-658">Hier volgen enkele die ik handig:</span><span class="sxs-lookup"><span data-stu-id="d9091-658">Here are a few I find useful:</span></span>

* <span data-ttu-id="d9091-659">Hallo illustraties van R Programming: een rondleiding van statistische softwareontwerp door Norman Matloff is een uitstekende inleiding tooprogramming in R.</span><span class="sxs-lookup"><span data-stu-id="d9091-659">hello Art of R Programming: A Tour of Statistical Software Design by Norman Matloff is an excellent introduction tooprogramming in R.</span></span>  
* <span data-ttu-id="d9091-660">R Cookbook door Paul Teetor biedt een probleem en oplossing benadering toousing R.</span><span class="sxs-lookup"><span data-stu-id="d9091-660">R Cookbook by Paul Teetor provides a problem and solution approach toousing R.</span></span>  
* <span data-ttu-id="d9091-661">R in actie door Robert Kabacoff is een ander nuttig inleidende rapport.</span><span class="sxs-lookup"><span data-stu-id="d9091-661">R in Action by Robert Kabacoff is another useful introductory book.</span></span> <span data-ttu-id="d9091-662">Hallo companion snelle R website is een nuttig resource op http://www.statmethods.net/.</span><span class="sxs-lookup"><span data-stu-id="d9091-662">hello companion Quick R website is a useful resource at http://www.statmethods.net/.</span></span>
* <span data-ttu-id="d9091-663">R Inferno door Patrick Burns is een verrassend grappige boek dat met een aantal lastig en moeilijk onderwerpen die kan worden gevonden werkt bij het programmeren in R. Hallo boek is beschikbaar voor het vrije op http://www.burns-stat.com/documents/books/the-r-inferno/.</span><span class="sxs-lookup"><span data-stu-id="d9091-663">R Inferno by Patrick Burns is a surprisingly humorous book that deals with a number of tricky and difficult topics that can be encountered when programming in R. hello book is available for free at http://www.burns-stat.com/documents/books/the-r-inferno/.</span></span>
* <span data-ttu-id="d9091-664">Als u wilt dat een diepgaand in geavanceerde onderwerpen in R, hebt u bekijkt hello adresboek Geavanceerd R door Hadley Wickham.</span><span class="sxs-lookup"><span data-stu-id="d9091-664">If you want a deep dive into advanced topics in R, have a look at hello book Advanced R by Hadley Wickham.</span></span> <span data-ttu-id="d9091-665">Hallo onlineversie van deze handleiding is beschikbaar voor het vrije op http://adv-r.had.co.nz/.</span><span class="sxs-lookup"><span data-stu-id="d9091-665">hello online version of this book is available for free at http://adv-r.had.co.nz/.</span></span>

<span data-ttu-id="d9091-666">Een lijst van R time series-pakketten kunt u vinden in Hallo CRAN taakweergave voor analyse van reeks: http://cran.r-project.org/web/views/TimeSeries.html.</span><span class="sxs-lookup"><span data-stu-id="d9091-666">A catalogue of R time series packages can be found in hello CRAN Task View for time series analysis: http://cran.r-project.org/web/views/TimeSeries.html.</span></span> <span data-ttu-id="d9091-667">Voor informatie over een specifiek tijdstip reeks object pakketten raadpleegt u toohello-documentatie voor dit pakket.</span><span class="sxs-lookup"><span data-stu-id="d9091-667">For information on specific time series object packages, you should refer toohello documentation for that package.</span></span>

<span data-ttu-id="d9091-668">Hallo adresboek inleidende Time Series met R door Paul Cowpertwait en Andrew Metcalfe biedt een inleiding toousing R voor analyse van reeks.</span><span class="sxs-lookup"><span data-stu-id="d9091-668">hello book Introductory Time Series with R by Paul Cowpertwait and Andrew Metcalfe provides an introduction toousing R for time series analysis.</span></span> <span data-ttu-id="d9091-669">Veel meer theoretische teksten bevatten R voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="d9091-669">Many more theoretical texts provide R examples.</span></span>

<span data-ttu-id="d9091-670">Sommige geweldige internetbronnen:</span><span class="sxs-lookup"><span data-stu-id="d9091-670">Some great internet resources:</span></span>

* <span data-ttu-id="d9091-671">DataCamp: DataCamp leert R Hallo deur uit uw browser met video uitkomsten en codering oefeningen.</span><span class="sxs-lookup"><span data-stu-id="d9091-671">DataCamp: DataCamp teaches R in hello comfort of your browser with video lessons and coding exercises.</span></span> <span data-ttu-id="d9091-672">Er zijn interactieve zelfstudies op Hallo nieuwste R technieken en pakketten.</span><span class="sxs-lookup"><span data-stu-id="d9091-672">There are interactive tutorials on hello latest R techniques and packages.</span></span> <span data-ttu-id="d9091-673">Hallo gratis interactieve R zelfstudie bij https://www.datacamp.com/courses/introduction-to-r worden</span><span class="sxs-lookup"><span data-stu-id="d9091-673">Take hello free interactive R tutorial at https://www.datacamp.com/courses/introduction-to-r</span></span>
* <span data-ttu-id="d9091-674">Een handleiding op aan de slag met R van Programiz https://www.programiz.com/r-programming</span><span class="sxs-lookup"><span data-stu-id="d9091-674">A guide on Getting started with R from Programiz https://www.programiz.com/r-programming</span></span>
* <span data-ttu-id="d9091-675">Een snelle zelfstudie van R door Kelly Black van Clarkson universiteit http://www.cyclismo.org/tutorial/R/</span><span class="sxs-lookup"><span data-stu-id="d9091-675">A quick R tutorial by Kelly Black from Clarkson University http://www.cyclismo.org/tutorial/R/</span></span>
* <span data-ttu-id="d9091-676">60 + R-resources die wordt vermeld op http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span><span class="sxs-lookup"><span data-stu-id="d9091-676">60+ R resources listed at http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span></span>

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
