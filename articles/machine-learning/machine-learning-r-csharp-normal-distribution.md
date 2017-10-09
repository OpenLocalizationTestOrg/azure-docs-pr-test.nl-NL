---
title: AAA(deprecated) normaalverdeling Web Service Suite - Azure | Microsoft Docs
description: (afgeschaft) Normale verdeling Web Service Suite
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: aab7b92e-953b-43d8-b0af-031394406bfe
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: ireiter
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 8bdb5afd9fee88587f548d7c5299480f64289bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-normal-distribution-suite"></a><span data-ttu-id="d414f-103">(afgeschaft) Normale verdeling Suite</span><span class="sxs-lookup"><span data-stu-id="d414f-103">(deprecated) Normal Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="d414f-104">Hallo Microsoft DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="d414f-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="d414f-105">U vindt veel nuttige voorbeeld experimenten en API's in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="d414f-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="d414f-106">Zie voor meer informatie over Hallo galerie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="d414f-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="d414f-107">Hallo normaalverdeling Suite is een reeks webservices voorbeeld ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [kwantiel Rekenmachine](https://datamarket.azure.com/dataset/aml_labs/ndq5), [kans Rekenmachine](https://datamarket.azure.com/dataset/aml_labs/ndp5)) die helpen bij het genereren en verwerking normale verdelingen.</span><span class="sxs-lookup"><span data-stu-id="d414f-107">hello Normal Distribution Suite is a set of sample web services ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/ndp5)) that help in generating and handling normal distributions.</span></span> <span data-ttu-id="d414f-108">Hallo-services kunnen genereren van een reeks normale verdeling van een willekeurige lengte, quantiles van een bepaalde waarschijnlijkheid berekenen en waarschijnlijkheid van een bepaalde kwantiel berekenen.</span><span class="sxs-lookup"><span data-stu-id="d414f-108">hello services allow generating a normal distribution sequence of any length, calculating quantiles from a given probability, and calculating probability from a given quantile.</span></span> <span data-ttu-id="d414f-109">Elk van de services Hallo andere uitvoer, op basis van geselecteerde Hallo service verzendt (Zie onderstaande beschrijving).</span><span class="sxs-lookup"><span data-stu-id="d414f-109">Each of hello services emits different outputs based on hello selected service (see description below).</span></span> <span data-ttu-id="d414f-110">Hallo normaalverdeling Suite is gebaseerd op Hallo R functies qnorm rnorm en pnorm, die zijn opgenomen in statistieken-R-pakket.</span><span class="sxs-lookup"><span data-stu-id="d414f-110">hello Normal Distribution Suite is based on hello R functions qnorm, rnorm, and pnorm, which are included in R stats package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="d414f-111">Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer.</span><span class="sxs-lookup"><span data-stu-id="d414f-111">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="d414f-112">Maar Hallo doel van de webservice Hallo is ook tooserve als een voorbeeld van hoe Azure Machine Learning-webservices gebruikte toocreate boven op R-code kan zijn.</span><span class="sxs-lookup"><span data-stu-id="d414f-112">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="d414f-113">Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice.</span><span class="sxs-lookup"><span data-stu-id="d414f-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="d414f-114">Hallo-webservice vervolgens gepubliceerde toohello Azure Marketplace kan worden en verbruikt door gebruikers en apparaten via Hallo wereld zonder instellingen infrastructuur door de auteur Hallo van Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="d414f-114">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="d414f-115">Gebruik van web-service</span><span class="sxs-lookup"><span data-stu-id="d414f-115">Consumption of web service</span></span>
<span data-ttu-id="d414f-116">Hallo normaalverdeling Suite bevat Hallo 3-services te volgen.</span><span class="sxs-lookup"><span data-stu-id="d414f-116">hello Normal Distribution Suite includes hello following 3 services.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="d414f-117">Normale verdeling kwantiel Rekenmachine</span><span class="sxs-lookup"><span data-stu-id="d414f-117">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="d414f-118">Deze service accepteert 4 argumenten van een normale verdeling en berekent kwantiel Hallo die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="d414f-118">This service accepts 4 arguments of a normal distribution and calculates hello associated quantile.</span></span>

<span data-ttu-id="d414f-119">Hallo invoerargumenten zijn:</span><span class="sxs-lookup"><span data-stu-id="d414f-119">hello input arguments are:</span></span>

* <span data-ttu-id="d414f-120">p - een enkele waarschijnlijkheid van een gebeurtenis met normale verdeling.</span><span class="sxs-lookup"><span data-stu-id="d414f-120">p - A single probability of an event with normal distribution.</span></span> 
* <span data-ttu-id="d414f-121">Gemiddelde - Hallo normale verdeling gemiddelde.</span><span class="sxs-lookup"><span data-stu-id="d414f-121">Mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="d414f-122">SD - standaardafwijking Hallo-normale distributie.</span><span class="sxs-lookup"><span data-stu-id="d414f-122">SD - hello normal distribution standard deviation.</span></span> 
* <span data-ttu-id="d414f-123">Side - L voor lagere zijde Hallo Hallo verdeling en U voor Hallo bovenzijde Hallo-verdeling.</span><span class="sxs-lookup"><span data-stu-id="d414f-123">Side - L for hello lower side of hello distribution and U for hello upper side of hello distribution.</span></span>

<span data-ttu-id="d414f-124">Hallo-uitvoer van Hallo-service is Hallo berekend kwantiel die is gekoppeld aan Hallo kans gegeven.</span><span class="sxs-lookup"><span data-stu-id="d414f-124">hello output of hello service is hello calculated quantile that is associated with hello given probability.</span></span>

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="d414f-125">Normale verdeling kans Rekenmachine</span><span class="sxs-lookup"><span data-stu-id="d414f-125">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="d414f-126">Deze service accepteert 4 argumenten van een normale verdeling en berekent de kans op Hallo die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="d414f-126">This service accepts 4 arguments of a normal distribution and calculates hello associated probability.</span></span>

<span data-ttu-id="d414f-127">Hallo invoerargumenten zijn:</span><span class="sxs-lookup"><span data-stu-id="d414f-127">hello input arguments are:</span></span>

* <span data-ttu-id="d414f-128">q - a één kwantiel van een gebeurtenis met normale verdeling.</span><span class="sxs-lookup"><span data-stu-id="d414f-128">q - A single quantile of an event with normal distribution.</span></span> 
* <span data-ttu-id="d414f-129">Gemiddelde - Hallo normale verdeling gemiddelde.</span><span class="sxs-lookup"><span data-stu-id="d414f-129">Mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="d414f-130">SD - standaardafwijking Hallo-normale distributie.</span><span class="sxs-lookup"><span data-stu-id="d414f-130">SD - hello normal distribution standard deviation.</span></span> 
* <span data-ttu-id="d414f-131">Side - L voor lagere zijde Hallo Hallo verdeling en U voor Hallo bovenzijde Hallo-verdeling.</span><span class="sxs-lookup"><span data-stu-id="d414f-131">Side - L for hello lower side of hello distribution and U for hello upper side of hello distribution.</span></span>

<span data-ttu-id="d414f-132">Hallo-uitvoer van Hallo-service is Hallo berekend kans dat is gekoppeld aan Hallo kwantiel gegeven.</span><span class="sxs-lookup"><span data-stu-id="d414f-132">hello output of hello service is hello calculated probability that is associated with hello given quantile.</span></span>

### <a name="normal-distribution-generator"></a><span data-ttu-id="d414f-133">Normale verdeling Generator</span><span class="sxs-lookup"><span data-stu-id="d414f-133">Normal Distribution Generator</span></span>
<span data-ttu-id="d414f-134">Deze service accepteert 3 argumenten van een normale verdeling en genereert een willekeurige volgorde van de cijfers die normaal gesproken worden gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="d414f-134">This service accepts 3 arguments of a normal distribution and generates a random sequence of numbers that are normally distributed.</span></span> <span data-ttu-id="d414f-135">Hallo moeten volgende argumenten worden opgegeven tooit binnen Hallo-aanvraag:</span><span class="sxs-lookup"><span data-stu-id="d414f-135">hello following arguments should be provided tooit within hello request:</span></span>

* <span data-ttu-id="d414f-136">n - Hallo aantal metingen.</span><span class="sxs-lookup"><span data-stu-id="d414f-136">n - hello number of observations.</span></span> 
* <span data-ttu-id="d414f-137">gemiddelde - Hallo normale verdeling gemiddelde.</span><span class="sxs-lookup"><span data-stu-id="d414f-137">mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="d414f-138">SD - standaardafwijking Hallo-normale distributie.</span><span class="sxs-lookup"><span data-stu-id="d414f-138">sd - hello normal distribution standard deviation.</span></span> 

<span data-ttu-id="d414f-139">Hallo-uitvoer van Hallo-service is een reeks van lengte n met een normale verdeling op basis van Hallo gemiddelde en sd-argumenten.</span><span class="sxs-lookup"><span data-stu-id="d414f-139">hello output of hello service is a sequence of length n with a normal distribution based on hello mean and sd arguments.</span></span>

> <span data-ttu-id="d414f-140">Deze service is gehost op Azure Marketplace Hallo een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden.</span><span class="sxs-lookup"><span data-stu-id="d414f-140">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="d414f-141">Er zijn meerdere manieren Hallo-service op automatische wijze verbruikt (voorbeeld-apps worden hier: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [kans Rekenmachine](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [kwantiel Rekenmachine](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span><span class="sxs-lookup"><span data-stu-id="d414f-141">There are multiple ways of consuming hello service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="d414f-142">C#-code voor het web service starten:</span><span class="sxs-lookup"><span data-stu-id="d414f-142">Starting C# code for web service consumption:</span></span>
### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="d414f-143">Normale verdeling kwantiel Rekenmachine</span><span class="sxs-lookup"><span data-stu-id="d414f-143">Normal Distribution Quantile Calculator</span></span>
    public class Input
    {
            public string p;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { p = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="d414f-144">Normale verdeling kans Rekenmachine</span><span class="sxs-lookup"><span data-stu-id="d414f-144">Normal Distribution Probability Calculator</span></span>
    public class Input
    {
            public string q;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="normal-distribution-generator"></a><span data-ttu-id="d414f-145">Normale verdeling Generator</span><span class="sxs-lookup"><span data-stu-id="d414f-145">Normal Distribution Generator</span></span>
    public class Input
    {
            public string n;
            public string mean;
            public string sd;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="d414f-146">Maken van de webservice</span><span class="sxs-lookup"><span data-stu-id="d414f-146">Creation of web service</span></span>
> <span data-ttu-id="d414f-147">Deze webservice is gemaakt met behulp van Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d414f-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="d414f-148">Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="d414f-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> 
> 
> 

<span data-ttu-id="d414f-149">Hieronder staat een screenshot van Hallo experiment die Hallo web service en voorbeeld-code hebt gemaakt voor elk Hallo-modules in Hallo experiment.</span><span class="sxs-lookup"><span data-stu-id="d414f-149">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="d414f-150">Normale verdeling kwantiel Rekenmachine</span><span class="sxs-lookup"><span data-stu-id="d414f-150">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="d414f-151">Stroom experiment:</span><span class="sxs-lookup"><span data-stu-id="d414f-151">Experiment flow:</span></span>

![Experiment stroom][2]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }
    q = qnorm(param$p,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    q = 2* param$mean - q
    } else if (param$side =='L') {
    q = q
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(q)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="d414f-153">Normale verdeling kans Rekenmachine</span><span class="sxs-lookup"><span data-stu-id="d414f-153">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="d414f-154">Stroom experiment:</span><span class="sxs-lookup"><span data-stu-id="d414f-154">Experiment flow:</span></span>

![Experiment stroom][3]

     #Data schema with example data (replaced with data from web service)
    data.set=data.frame(q=-1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    prob = pnorm(param$q,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    prob = 1 - prob
    } else if (param$side =='B') {
    prob = ifelse(prob<=0.5,prob * 2, 1)
    } else if (param$side =='L') {
    prob = prob
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-generator"></a><span data-ttu-id="d414f-156">Normale verdeling Generator</span><span class="sxs-lookup"><span data-stu-id="d414f-156">Normal Distribution Generator</span></span>
<span data-ttu-id="d414f-157">Stroom experiment:</span><span class="sxs-lookup"><span data-stu-id="d414f-157">Experiment flow:</span></span>

![Experiment stroom][4]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,mean=0,sd=1);
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    dist = rnorm(param$n,mean=param$mean,sd=param$sd)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="d414f-159">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="d414f-159">Limitations</span></span>
<span data-ttu-id="d414f-160">Dit zijn eenvoudige voorbeelden omringende Hallo normaalverdeling.</span><span class="sxs-lookup"><span data-stu-id="d414f-160">These are very simple examples surrounding hello normal distribution.</span></span> <span data-ttu-id="d414f-161">Zoals u kunt zien van Hallo voorbeeldcode hierboven, is weinig fout vastgelegd geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="d414f-161">As can be seen from hello example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="d414f-162">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="d414f-162">FAQ</span></span>
<span data-ttu-id="d414f-163">Zie voor veelgestelde vragen over het verbruik van de webservice Hallo of publishing toohello Azure Marketplace [hier](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="d414f-163">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

