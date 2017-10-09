---
title: AAA(deprecated) Machine learning-webservices voorbeelden die zijn gebouwd met R - Azure | Microsoft Docs
description: (afgeschaft) Een handig reeks voorbeelden van web-services met R code en Machine Learning gemaakt en gepubliceerd toohello Azure Marketplace vinden.
keywords: csharp, r-code, web services-voorbeelden
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 97d66cb7-6a84-4ae9-8095-0b5f5ba82d7f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 20b074d38e65aed907d40549bb61f124cb5dfe1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-toomicrosoft-azure-marketplace"></a><span data-ttu-id="9bb58-104">(afgeschaft) Voorbeelden met R-code op Azure Machine Learning en gepubliceerde tooMicrosoft Azure Marketplace-webservices</span><span class="sxs-lookup"><span data-stu-id="9bb58-104">(deprecated) Web services examples using R code on Azure Machine Learning and published tooMicrosoft Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="9bb58-105">Hallo Microsoft DataMarket wordt buiten gebruik gesteld en deze API's zijn afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="9bb58-105">hello Microsoft DataMarket is being retired and these APIs have been deprecated.</span></span> 
> 
> <span data-ttu-id="9bb58-106">U vindt veel nuttige voorbeeld experimenten en API's in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="9bb58-106">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="9bb58-107">Zie voor meer informatie over Hallo galerie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="9bb58-107">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="9bb58-108">In dit artikel zijn met het voorbeeld web services zijn gemaakt met Azure Machine Learning en gepubliceerd toohello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="9bb58-108">In this article are example web services were created using Azure Machine Learning and published toohello Azure Marketplace.</span></span> <span data-ttu-id="9bb58-109">Elke web service-voorbeeld heeft een uitgebreide document is gekoppeld, insluiten gegevenssets voorbeeld voor het Hallo-services testen en waarin wordt uitgelegd hoe Hallo-gebruiker kunt maken van een vergelijkbare service zelf.</span><span class="sxs-lookup"><span data-stu-id="9bb58-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing hello services and explaining how hello user can create a similar service themselves.</span></span> 

<span data-ttu-id="9bb58-110">Gebruikers kunnen in Azure Machine Learning Studio R code schrijven en met een paar klikken kunt publiceren als een webservice voor toepassingen en apparaten tooconsume Hallo wereld.</span><span class="sxs-lookup"><span data-stu-id="9bb58-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices tooconsume around hello world.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="9bb58-111">Van het opstellen van eenvoudige rekenmachines waarmee statistische functies toocreating aangepaste tekst analysemodel gevoel analyse te voorspellen, kunnen zowel nieuwe als ervaren R-gebruikers profiteren van Hallo eenvoudig waarmee gebruikers van Azure Machine Learning R kunnen operationeel de code.</span><span class="sxs-lookup"><span data-stu-id="9bb58-111">From producing simple calculators that provide statistical functionality toocreating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from hello ease with which users of Azure Machine Learning can operationalize R code.</span></span> <span data-ttu-id="9bb58-112">Hoewel deze webservices kunnen worden gebruikt door gebruikers mogelijk via een mobiele app of een website Hallo doel van deze voorbeelden is tooshow hoe Machine Learning kunnen operationeel webservices R scripts voor analysedoeleinden en gebruikte toocreate webservices op begin van R-code.</span><span class="sxs-lookup"><span data-stu-id="9bb58-112">While these web services could be consumed by users, potentially through a mobile app or a website, hello purpose of these web services examples is tooshow how Machine Learning can operationalize R scripts for analytical purposes and be used toocreate web services on top of R code.</span></span>

<span data-ttu-id="9bb58-113">Elke voorbeeld bevat een C#-voorbeeld voor het web service.</span><span class="sxs-lookup"><span data-stu-id="9bb58-113">Each example includes a C# example for web service consumption.</span></span>

![Diagram van R-code in Azure Machine Learning: R-oplossingen voor eigen gebruik of gepubliceerde toohello Azure Marketplace.][1]

<span data-ttu-id="9bb58-115">Overweeg het Hallo-scenario's te volgen.</span><span class="sxs-lookup"><span data-stu-id="9bb58-115">Consider hello following scenarios.</span></span>

## <a name="scenario-1-generic-model"></a><span data-ttu-id="9bb58-116">Scenario 1: Algemeen model</span><span class="sxs-lookup"><span data-stu-id="9bb58-116">Scenario 1: Generic model</span></span>
<span data-ttu-id="9bb58-117">Een gebruiker werkt met een algemene model die toegepast tooa nieuwe gebruiker-gegevens worden kan, zoals een basic prognose van reeksgegevens tijd of een op maat gemaakte R-methode met geavanceerde analyses.</span><span class="sxs-lookup"><span data-stu-id="9bb58-117">A user works with a generic model that can be applied tooa new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span></span> <span data-ttu-id="9bb58-118">Deze gebruiker publiceert Hallo model als een webservice voor anderen tooconsume met hun gegevens.</span><span class="sxs-lookup"><span data-stu-id="9bb58-118">This user publishes hello model as a web service for others tooconsume with their data.</span></span>

* [<span data-ttu-id="9bb58-119">Binaire classificatie</span><span class="sxs-lookup"><span data-stu-id="9bb58-119">Binary Classifier</span></span>](machine-learning-r-csharp-binary-classifier.md)
* [<span data-ttu-id="9bb58-120">Clustermodel</span><span class="sxs-lookup"><span data-stu-id="9bb58-120">Cluster Model</span></span>](machine-learning-r-csharp-cluster-model.md)
* [<span data-ttu-id="9bb58-121">Multidimensionale lineaire regressie</span><span class="sxs-lookup"><span data-stu-id="9bb58-121">Multivariate Linear Regression</span></span>](machine-learning-r-csharp-multivariate-linear-regression.md)
* [<span data-ttu-id="9bb58-122">Prognoses - Exponentieel vloeiend maken</span><span class="sxs-lookup"><span data-stu-id="9bb58-122">Forecasting - Exponential Smoothing</span></span>](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [<span data-ttu-id="9bb58-123">ETS + STL prognose</span><span class="sxs-lookup"><span data-stu-id="9bb58-123">ETS + STL Forecasting</span></span>](machine-learning-r-csharp-retail-demand-forecasting.md)
* [<span data-ttu-id="9bb58-124">Prognose - Autoregressive geïntegreerd zwevend gemiddelde (ARIMA)</span><span class="sxs-lookup"><span data-stu-id="9bb58-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>](machine-learning-r-csharp-arima.md)
* [<span data-ttu-id="9bb58-125">Overlevingsanalyse</span><span class="sxs-lookup"><span data-stu-id="9bb58-125">Survival Analysis</span></span>](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a><span data-ttu-id="9bb58-126">Scenario 2: Getraind model – specifieke gegevens</span><span class="sxs-lookup"><span data-stu-id="9bb58-126">Scenario 2: Trained model – specific data</span></span>
<span data-ttu-id="9bb58-127">Een gebruiker heeft gegevens die handig voorspellingen via R-code bevat, zoals een grote steekproef van karakter vragenlijst via k-means algoritme toopredict Hallo van een gebruiker karakter type geclusterde of status krijgt een overzicht van gegevens die kunnen worden gebruikt toopredict iemands risico voor longkanker met een survival analyse R-pakket.</span><span class="sxs-lookup"><span data-stu-id="9bb58-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm toopredict hello user’s personality type, or health survey data that can be used toopredict an individual’s risk for lung cancer with a survival analysis R package.</span></span> <span data-ttu-id="9bb58-128">Hallo gebruiker publiceert Hallo gegevens via een webservice die een nieuwe gebruiker uitkomst voorspelt.</span><span class="sxs-lookup"><span data-stu-id="9bb58-128">hello user publishes hello data through a web service that predicts a new user’s outcome.</span></span>

## <a name="scenario-3-trained-model--generic-data"></a><span data-ttu-id="9bb58-129">Scenario 3: Getraind model: algemene gegevens</span><span class="sxs-lookup"><span data-stu-id="9bb58-129">Scenario 3: Trained model – generic data</span></span>
<span data-ttu-id="9bb58-130">Een gebruiker heeft algemene gegevens (zoals een corpus tekst) waarmee een web service toobe gebouwd en algemeen via verschillende soorten gebruiksvoorbeelden en scenario's worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="9bb58-130">A user has generic data (such as a text corpus) that allows a web service toobe built and applied generically across different types of use cases and scenarios.</span></span>

* [<span data-ttu-id="9bb58-131">Op woordenlijsten gebaseerde sentimentanalyse</span><span class="sxs-lookup"><span data-stu-id="9bb58-131">Lexicon Based Sentiment Analysis</span></span>](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a><span data-ttu-id="9bb58-132">Scenario 4: Geavanceerde Rekenmachine</span><span class="sxs-lookup"><span data-stu-id="9bb58-132">Scenario 4: Advanced calculator</span></span>
<span data-ttu-id="9bb58-133">Een gebruiker biedt geavanceerde berekeningen of simulaties waarvoor een getraind model of aanpassen van de gegevens van een model toohello gebruiker niet.</span><span class="sxs-lookup"><span data-stu-id="9bb58-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model toohello user’s data.</span></span>

* [<span data-ttu-id="9bb58-134">Verschil in verhoudingen testen</span><span class="sxs-lookup"><span data-stu-id="9bb58-134">Difference in Proportions Test</span></span>](machine-learning-r-csharp-difference-in-two-proportions.md)
* [<span data-ttu-id="9bb58-135">Normal Distribution Suite</span><span class="sxs-lookup"><span data-stu-id="9bb58-135">Normal Distribution Suite</span></span>](machine-learning-r-csharp-normal-distribution.md)
* [<span data-ttu-id="9bb58-136">Binomial Distribution Suite</span><span class="sxs-lookup"><span data-stu-id="9bb58-136">Binomial Distribution Suite</span></span>](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a><span data-ttu-id="9bb58-137">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="9bb58-137">FAQ</span></span>
<span data-ttu-id="9bb58-138">Zie voor veelgestelde vragen over het verbruik van de webservice Hallo of publishing toohello Marketplace [hier](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="9bb58-138">For frequently asked questions on consumption of hello web service or publishing toohello Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



