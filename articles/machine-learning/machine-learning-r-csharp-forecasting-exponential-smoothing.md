---
title: "AAA(deprecated) prognose - exponentiële demping - Azure | Microsoft Docs"
description: "(afgeschaft) Webservice: prognose exponentiële vloeiend maken"
services: machine-learning
documentationcenter: 
author: yijichen
manager: jhubbard
editor: cgronlun
ms.assetid: a4150681-6eac-4145-9eca-0cdf60781dde
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: ebc732d3a47943405b0cb26a373f529a50de9005
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-forecasting---exponential-smoothing"></a><span data-ttu-id="85dab-103">(afgeschaft) Prognose - exponentiële demping</span><span class="sxs-lookup"><span data-stu-id="85dab-103">(deprecated) Forecasting - Exponential Smoothing</span></span>

> [!NOTE]
> <span data-ttu-id="85dab-104">Hallo Microsoft DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="85dab-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="85dab-105">U vindt veel nuttige voorbeeld experimenten en API's in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="85dab-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="85dab-106">Zie voor meer informatie over Hallo galerie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="85dab-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="85dab-107">Dit [webservice](https://datamarket.azure.com/dataset/aml_labs/ets) implements Hallo exponentiële demping model (ETS) tooproduce voorspellingen op basis van de historische gegevens Hallo opgegeven door de gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="85dab-107">This [web service](https://datamarket.azure.com/dataset/aml_labs/ets) implements hello Exponential Smoothing model (ETS) tooproduce predictions based on hello historical data provided by hello user.</span></span> <span data-ttu-id="85dab-108">Wordt Hallo aanvraag voor een specifiek product verhoging van dit jaar?</span><span class="sxs-lookup"><span data-stu-id="85dab-108">Will hello demand for a specific product increase this year?</span></span> <span data-ttu-id="85dab-109">Kan ik voorspellen mijn product sales voor Hallo Kerstmis seizoen, zodat ik kan mijn voorraad effectief plannen?</span><span class="sxs-lookup"><span data-stu-id="85dab-109">Can I predict my product sales for hello Christmas season, so that I can effectively plan my inventory?</span></span> <span data-ttu-id="85dab-110">Prognosemodellen apt tooaddress dergelijke vragen zijn.</span><span class="sxs-lookup"><span data-stu-id="85dab-110">Forecasting models are apt tooaddress such questions.</span></span> <span data-ttu-id="85dab-111">Hallo gegeven voorbij gegevens, deze modellen verborgen trends en seizoensgebonden toopredict toekomstige trends onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="85dab-111">Given hello past data, these models examine hidden trends and seasonality toopredict future trends.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="85dab-112">Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer.</span><span class="sxs-lookup"><span data-stu-id="85dab-112">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="85dab-113">Maar Hallo doel van de webservice Hallo is ook tooserve als een voorbeeld van hoe Azure Machine Learning-webservices gebruikte toocreate boven op R-code kan zijn.</span><span class="sxs-lookup"><span data-stu-id="85dab-113">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="85dab-114">Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice.</span><span class="sxs-lookup"><span data-stu-id="85dab-114">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="85dab-115">Hallo-webservice vervolgens gepubliceerde toohello Azure Marketplace kan worden en verbruikt door gebruikers en apparaten via Hallo wereld zonder instellingen infrastructuur door de auteur Hallo van Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="85dab-115">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="85dab-116">Gebruik van web-service</span><span class="sxs-lookup"><span data-stu-id="85dab-116">Consumption of web service</span></span>
<span data-ttu-id="85dab-117">Deze service accepteert 4 argumenten en Hallo ETS prognoses berekent.</span><span class="sxs-lookup"><span data-stu-id="85dab-117">This service accepts 4 arguments and calculates hello ETS forecasts.</span></span>
<span data-ttu-id="85dab-118">Hallo invoerargumenten zijn:</span><span class="sxs-lookup"><span data-stu-id="85dab-118">hello input arguments are:</span></span>

* <span data-ttu-id="85dab-119">Frequentie - Hallo frequentie van Hallo onbewerkte gegevens (dagelijks/wekelijks/maandelijks/elk kwartaal/jaarlijks) aangeeft.</span><span class="sxs-lookup"><span data-stu-id="85dab-119">Frequency - Indicates hello frequency of hello raw data (daily/weekly/monthly/quarterly/yearly).</span></span>
* <span data-ttu-id="85dab-120">Horizon - toekomstige forecast periode.</span><span class="sxs-lookup"><span data-stu-id="85dab-120">Horizon - Future forecast time-frame.</span></span>
* <span data-ttu-id="85dab-121">Datum - toevoegen in de nieuwe tijdreeks Hallo gegevens voor tijd.</span><span class="sxs-lookup"><span data-stu-id="85dab-121">Date - Add in hello new time series data for time.</span></span>
* <span data-ttu-id="85dab-122">Waarde: toevoegen in Hallo nieuwe time series gegevenswaarden.</span><span class="sxs-lookup"><span data-stu-id="85dab-122">Value - Add in hello new time series data values.</span></span>

<span data-ttu-id="85dab-123">Hallo-uitvoer van Hallo-service is Hallo berekende voorspelde waarden.</span><span class="sxs-lookup"><span data-stu-id="85dab-123">hello output of hello service is hello calculated forecast values.</span></span>

<span data-ttu-id="85dab-124">Voorbeeldinvoer mogelijk:</span><span class="sxs-lookup"><span data-stu-id="85dab-124">Sample input could be:</span></span> 

* <span data-ttu-id="85dab-125">Frequentie - 12</span><span class="sxs-lookup"><span data-stu-id="85dab-125">Frequency - 12</span></span>
* <span data-ttu-id="85dab-126">Horizon - 12</span><span class="sxs-lookup"><span data-stu-id="85dab-126">Horizon - 12</span></span>
* <span data-ttu-id="85dab-127">Datum - 15/1/2012; 15-2/2012 3-15/2012; 15-4-2012; 15-5-2012; 15/6/2012; 15/7/2012; 8 / 15-2012; 15/9/2012; 10/15/2012; 11-15/2012; 15-12/2012; 15/1/2013; 15-2/2013 15-3/2013; 15-4/2013; 15/5/2013; 15/6/2013; 15/7/2013; 8 / 15/2013; 15/9/2013 15/10/2013; 15-11/2013; 15-12/2013; 15-1-2014; 15-2-2014 15-3-2014; 15-4-2014; 15-5-2014; 15-6-2014; 15-7-2014; 8 / 15-2014; 15-9-2014</span><span class="sxs-lookup"><span data-stu-id="85dab-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span></span>
* <span data-ttu-id="85dab-128">Waarde - 3.479; 3,68; 3.832; 3.941; 3.797; 3.586; 3.508; 3.731; 3.915; 3.844; 3.634; 3.549; 3.557; 3.785; 3.782; 3.601; 3.544; 3.556; 3.65; 3.709; 3.682; 3.511; 3.429; 3.51; 3.523; 3.525; 3.626; 3.695; 3.711; 3.711; 3.693; 3.571; 3.509</span><span class="sxs-lookup"><span data-stu-id="85dab-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span></span>

> <span data-ttu-id="85dab-129">Deze service is gehost op Azure Marketplace Hallo een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden.</span><span class="sxs-lookup"><span data-stu-id="85dab-129">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="85dab-130">Er zijn meerdere manieren Hallo-service op automatische wijze verbruikt (een voorbeeld-app is [hier](http://microsoftazuremachinelearning.azurewebsites.net/etsForecasting.aspx)).</span><span class="sxs-lookup"><span data-stu-id="85dab-130">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/etsForecasting.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="85dab-131">C#-code voor het web service starten:</span><span class="sxs-lookup"><span data-stu-id="85dab-131">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string frequency;
            public string horizon;
            public string date;
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }



## <a name="creation-of-web-service"></a><span data-ttu-id="85dab-132">Maken van de webservice</span><span class="sxs-lookup"><span data-stu-id="85dab-132">Creation of web service</span></span>
> <span data-ttu-id="85dab-133">Deze webservice is gemaakt met behulp van Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="85dab-133">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="85dab-134">Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="85dab-134">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="85dab-135">Hieronder staat een screenshot van Hallo experiment die Hallo web service en voorbeeld-code hebt gemaakt voor elk Hallo-modules in Hallo experiment.</span><span class="sxs-lookup"><span data-stu-id="85dab-135">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="85dab-136">In Azure Machine Learning, is een nieuw, leeg experiment gemaakt.</span><span class="sxs-lookup"><span data-stu-id="85dab-136">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="85dab-137">Voorbeeldgegevens voor invoer is geüpload met een vooraf gedefinieerde gegevensschema.</span><span class="sxs-lookup"><span data-stu-id="85dab-137">Sample input data was uploaded with a predefined data schema.</span></span> <span data-ttu-id="85dab-138">Gekoppelde toohello gegevensschema is een [R-Script uitvoeren] [ execute-r-script] module die wordt gegenereerd Hallo ETS prognose model met behulp van 'ets' en 'forecast' functies van R.</span><span class="sxs-lookup"><span data-stu-id="85dab-138">Linked toohello data schema is an [Execute R Script][execute-r-script] module that generates hello ETS forecasting model by using ‘ets’ and ‘forecast’ functions from R.</span></span> 

![Experiment stroom][2]

#### <a name="module-1"></a><span data-ttu-id="85dab-140">Module 1:</span><span class="sxs-lookup"><span data-stu-id="85dab-140">Module 1:</span></span>
    # Add in hello CSV file with hello data in hello format shown below 
![Steekproef][3]    

#### <a name="module-2"></a><span data-ttu-id="85dab-142">2-module:</span><span class="sxs-lookup"><span data-stu-id="85dab-142">Module 2:</span></span>
    # Data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # Preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # Fit a time-series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- ets(train_ts)
    train_model <- forecast(fit1, h = data$horizon)
    plot(train_model)

    # Produce forcasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # Data output
    maml.mapOutputPort("data.forecast");


## <a name="limitations"></a><span data-ttu-id="85dab-143">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="85dab-143">Limitations</span></span>
<span data-ttu-id="85dab-144">Dit is een zeer eenvoudige voorbeeld voor het voorspellen van ETS.</span><span class="sxs-lookup"><span data-stu-id="85dab-144">This is a very simple example for ETS forecasting.</span></span> <span data-ttu-id="85dab-145">Zoals u kunt zien van Hallo voorbeeldcode hierboven, er is geen fout vastgelegd is geïmplementeerd en Hallo-service wordt ervan uitgegaan dat alle Hallo-variabelen waarden voor continue-positieve zijn en Hallo frequentie een geheel getal groter dan 1 moet.</span><span class="sxs-lookup"><span data-stu-id="85dab-145">As can be seen from hello example code above, no error catching is implemented, and hello service assumes that all hello variables are continuous/positive values and hello frequency should be an integer greater than 1.</span></span> <span data-ttu-id="85dab-146">Hallo-lengte van de datum en waarde vectoren Hallo moet dezelfde Hallo.</span><span class="sxs-lookup"><span data-stu-id="85dab-146">hello length of hello date and value vectors should be hello same.</span></span> <span data-ttu-id="85dab-147">Hallo datum variabele moet toohello indeling 'mm/dd/jjjj' voldoen.</span><span class="sxs-lookup"><span data-stu-id="85dab-147">hello date variable should adhere toohello format ‘mm/dd/yyyy’.</span></span>

## <a name="faq"></a><span data-ttu-id="85dab-148">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="85dab-148">FAQ</span></span>
<span data-ttu-id="85dab-149">Zie voor veelgestelde vragen over het verbruik van de webservice Hallo of publishing toohello Azure Marketplace [hier](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="85dab-149">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img1.png
[2]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img2.png
[3]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

