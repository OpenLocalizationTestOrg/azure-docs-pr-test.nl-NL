---
title: Verschil in verhouding Test - Azure aaa(deprecated) | Microsoft Docs
description: (afgeschaft) Verschil in verhouding Test
services: machine-learning
documentationcenter: 
author: aniedea
manager: jhubbard
editor: cgronlun
ms.assetid: 9356b821-5345-44f6-8e26-719f2dea5e6d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: aniedea
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 820aad377f9dec12b0ef455974aaa95f6e8d723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-difference-in-proportions-test"></a><span data-ttu-id="2460f-103">(afgeschaft) Verschil in verhouding Test</span><span class="sxs-lookup"><span data-stu-id="2460f-103">(deprecated) Difference in Proportions Test</span></span>

> [!NOTE]
> <span data-ttu-id="2460f-104">Hallo Microsoft DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="2460f-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="2460f-105">U vindt veel nuttige voorbeeld experimenten en API's in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="2460f-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="2460f-106">Zie voor meer informatie over Hallo galerie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="2460f-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="2460f-107">Zijn de twee verhoudingen statistisch verschillen?</span><span class="sxs-lookup"><span data-stu-id="2460f-107">Are two proportions statistically different?</span></span> <span data-ttu-id="2460f-108">Stel dat een gebruiker wil toocompare twee films toodetermine als één film een aanzienlijk hoger deel van heeft 'graag' wanneer toohello andere vergeleken.</span><span class="sxs-lookup"><span data-stu-id="2460f-108">Suppose a user wants toocompare two movies toodetermine if one movie has a significantly higher proportion of ‘likes’ when compared toohello other.</span></span> <span data-ttu-id="2460f-109">Met een grote steekproef, kan er een statistisch aanzienlijke verschil tussen Hallo verhoudingen 0,50 en 0,51.</span><span class="sxs-lookup"><span data-stu-id="2460f-109">With a large sample, there could be a statistically significant difference between hello proportions 0.50 and 0.51.</span></span> <span data-ttu-id="2460f-110">Met een kort voorbeeld er mogelijk niet voldoende gegevens toodetermine als deze verhoudingen daadwerkelijk verschillen.</span><span class="sxs-lookup"><span data-stu-id="2460f-110">With a small sample, there may not be enough data toodetermine if these proportions are actually different.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="2460f-111">Dit [webservice](https://datamarket.azure.com/dataset/aml_labs/prop_test) voert een test hypothese van Hallo verschil in twee verhoudingen op basis van gebruikersinvoer van Hallo aantal successen en Hallo kunt u het totale aantal proefversies voor Hallo 2 vergelijking groepen.</span><span class="sxs-lookup"><span data-stu-id="2460f-111">This [web service](https://datamarket.azure.com/dataset/aml_labs/prop_test) conducts a hypothesis test of hello difference in two proportions based on user input of hello number of successes and hello total number of trials for hello 2 comparison groups.</span></span> <span data-ttu-id="2460f-112">In een voorbeeldscenario kan deze webservice worden aangeroepen vanuit een film vergelijking-app waarin Hallo gebruiker of een van de Hallo films echt 'bevallen is' vaker dan Hallo andere, op basis van classificatie van films.</span><span class="sxs-lookup"><span data-stu-id="2460f-112">In one possible scenario, this web service could be called from within a movie comparison app, telling hello user whether one of hello movies is really ‘liked’ more often than hello other, based on movie ratings.</span></span>

> <span data-ttu-id="2460f-113">Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer.</span><span class="sxs-lookup"><span data-stu-id="2460f-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="2460f-114">Maar Hallo doel van de webservice Hallo is ook tooserve als een voorbeeld van hoe Azure Machine Learning-webservices gebruikte toocreate boven op R-code kan zijn.</span><span class="sxs-lookup"><span data-stu-id="2460f-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="2460f-115">Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice.</span><span class="sxs-lookup"><span data-stu-id="2460f-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="2460f-116">Hallo-webservice vervolgens gepubliceerde toohello Azure Marketplace kan worden en verbruikt door gebruikers en apparaten via Hallo wereld zonder instellingen infrastructuur door de auteur Hallo van Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="2460f-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="2460f-117">Gebruik van web-service</span><span class="sxs-lookup"><span data-stu-id="2460f-117">Consumption of web service</span></span>
<span data-ttu-id="2460f-118">Deze service accepteert 4 argumenten en biedt een hypothese test van verhoudingen.</span><span class="sxs-lookup"><span data-stu-id="2460f-118">This service accepts 4 arguments and does a hypothesis test of proportions.</span></span>

<span data-ttu-id="2460f-119">Hallo invoerargumenten zijn:</span><span class="sxs-lookup"><span data-stu-id="2460f-119">hello input arguments are:</span></span>

* <span data-ttu-id="2460f-120">Successes1 - aantal geslaagde gebeurtenissen in voorbeeld 1.</span><span class="sxs-lookup"><span data-stu-id="2460f-120">Successes1 - Number of success events in sample 1.</span></span>
* <span data-ttu-id="2460f-121">Successes2 - aantal geslaagde gebeurtenissen in voorbeeld 2.</span><span class="sxs-lookup"><span data-stu-id="2460f-121">Successes2 - Number of success events in sample 2.</span></span>
* <span data-ttu-id="2460f-122">Total1 - grootte van voorbeeld 1.</span><span class="sxs-lookup"><span data-stu-id="2460f-122">Total1 -  Size of sample 1.</span></span>
* <span data-ttu-id="2460f-123">Total2 - grootte van voorbeeld 2.</span><span class="sxs-lookup"><span data-stu-id="2460f-123">Total2 - Size of sample 2.</span></span>

<span data-ttu-id="2460f-124">Hallo-uitvoer van Hallo-service is Hallo resultaat van Hallo hypothese testen samen met de Hallo chi-square statistiek, df, p-waarde en het aandeel in voorbeeld 1/2- en betrouwbaarheidsinterval grenzen.</span><span class="sxs-lookup"><span data-stu-id="2460f-124">hello output of hello service is hello result of hello hypothesis test along with hello chi-square statistic, df, p-value, and proportion in sample 1/2 and confidence interval bounds.</span></span>

> <span data-ttu-id="2460f-125">Deze service is gehost op Azure Marketplace Hallo een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden.</span><span class="sxs-lookup"><span data-stu-id="2460f-125">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="2460f-126">Er zijn meerdere manieren Hallo-service op automatische wijze verbruikt (een voorbeeld-app is [hier](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span><span class="sxs-lookup"><span data-stu-id="2460f-126">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="2460f-127">C#-code voor het web service starten:</span><span class="sxs-lookup"><span data-stu-id="2460f-127">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string successes1;
            public string successes2;
            public string total1;
            public string total2;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { successes1 = TextBox1.Text, successes2 = TextBox2.Text, total1 = TextBox3.Text, total2 = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="2460f-128">Maken van de webservice</span><span class="sxs-lookup"><span data-stu-id="2460f-128">Creation of web service</span></span>
> <span data-ttu-id="2460f-129">Deze webservice is gemaakt met behulp van Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="2460f-129">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="2460f-130">Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="2460f-130">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="2460f-131">Hieronder staat een screenshot van Hallo experiment die Hallo web service en voorbeeld-code hebt gemaakt voor elk Hallo-modules in Hallo experiment.</span><span class="sxs-lookup"><span data-stu-id="2460f-131">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="2460f-132">In Azure Machine Learning, een nieuw, leeg experiment is gemaakt met twee [R-Script uitvoeren] [ execute-r-script] modules.</span><span class="sxs-lookup"><span data-stu-id="2460f-132">From within Azure Machine Learning, a new blank experiment was created with two [Execute R Script][execute-r-script] modules.</span></span> <span data-ttu-id="2460f-133">Hallo gegevensschema is in de eerste module Hallo gedefinieerd, terwijl de tweede Hallo-module met Hallo prop.test opdracht in R tooperform Hallo hypothese test voor 2 verhoudingen.</span><span class="sxs-lookup"><span data-stu-id="2460f-133">In hello first module hello data schema is defined, while hello second module uses hello prop.test command within R tooperform hello hypothesis test for 2 proportions.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="2460f-134">Stroom experiment:</span><span class="sxs-lookup"><span data-stu-id="2460f-134">Experiment flow:</span></span>
![Experiment stroom][2]

#### <a name="module-1"></a><span data-ttu-id="2460f-136">Module 1:</span><span class="sxs-lookup"><span data-stu-id="2460f-136">Module 1:</span></span>
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data toooutput port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a><span data-ttu-id="2460f-137">2-module:</span><span class="sxs-lookup"><span data-stu-id="2460f-137">Module 2:</span></span>
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"hello proportions are different!",
    "hello proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a><span data-ttu-id="2460f-138">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="2460f-138">Limitations</span></span>
<span data-ttu-id="2460f-139">Dit is een zeer eenvoudige voorbeeld voor een test van verschil in verhouding van 2.</span><span class="sxs-lookup"><span data-stu-id="2460f-139">This is a very simple example for a test of difference in 2 proportions.</span></span> <span data-ttu-id="2460f-140">Zoals u kunt zien van Hallo voorbeeldcode hierboven, geen fout vastgelegd is geïmplementeerd en Hallo-service wordt ervan uitgegaan dat alle Hallo variabelen continue.</span><span class="sxs-lookup"><span data-stu-id="2460f-140">As can be seen from hello example code above, no error catching is implemented and hello service assumes that all hello variables are continuous.</span></span>

## <a name="faq"></a><span data-ttu-id="2460f-141">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="2460f-141">FAQ</span></span>
<span data-ttu-id="2460f-142">Zie voor veelgestelde vragen over het verbruik van de webservice Hallo of publishing toohello Azure Marketplace [hier](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="2460f-142">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

