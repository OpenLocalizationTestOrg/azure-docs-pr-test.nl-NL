---
title: AAA(deprecated) binomiaalverdeling Suite - Azure | Microsoft Docs
description: (afgeschaft) Binomiaalverdeling Suite
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: 6d102d57-8f20-4ab3-be31-02fcfe4d15ed
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
ms.openlocfilehash: 6f94436cd19abeb518d179f340c8d4f43fcf4520
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binomial-distribution-suite"></a><span data-ttu-id="8d3e3-103">(afgeschaft) Binomiaalverdeling Suite</span><span class="sxs-lookup"><span data-stu-id="8d3e3-103">(deprecated) Binomial Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="8d3e3-104">Hallo Microsoft DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="8d3e3-105">U vindt veel nuttige voorbeeld experimenten en API's in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="8d3e3-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="8d3e3-106">Zie voor meer informatie over Hallo galerie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="8d3e3-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="8d3e3-107">Hallo binomiaalverdeling Suite is een reeks webservices voorbeeld ([binomiale Generator](https://datamarket.azure.com/dataset/aml_labs/bdg5), [kans Rekenmachine](https://datamarket.azure.com/dataset/aml_labs/bdp4), [kwantiel Rekenmachine](https://datamarket.azure.com/dataset/aml_labs/bdq5)) die helpen bij het genereren en Omgaan met binomiale distributies.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-107">hello Binomial Distribution Suite is a set of sample web services ([Binomial Generator](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/bdq5)) that help in generating and dealing with binomial distributions.</span></span> <span data-ttu-id="8d3e3-108">Hallo services kunnen genereren van een reeks binomiaalverdeling van een willekeurige lengte, quantiles berekenen gegeven van kans en berekenen waarschijnlijkheid van een bepaalde kwantiel.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-108">hello services allow generating a binomial distribution sequence of any length, calculating quantiles out of given probability and calculating probability from a given quantile.</span></span> <span data-ttu-id="8d3e3-109">Elk van de services Hallo andere uitvoer, op basis van geselecteerde Hallo service verzendt (Zie onderstaande beschrijving).</span><span class="sxs-lookup"><span data-stu-id="8d3e3-109">Each of hello services emits different outputs based on hello selected service (see description below).</span></span> <span data-ttu-id="8d3e3-110">Hallo binomiaalverdeling Suite is gebaseerd op Hallo R functies qbinom rbinom en pbinom, die zijn opgenomen in Hallo R statistieken-pakket.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-110">hello Binomial Distribution Suite is based on hello R functions qbinom, rbinom, and pbinom, which are included in hello R stats package.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="8d3e3-111">Deze webservices kunnen worden gebruikt door gebruikers – mogelijk rechtstreeks op Hallo marketplace, via een mobiele app via een website of zelfs op een lokale computer, bijvoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-111">These web services could be consumed by users – potentially directly on hello marketplace, through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="8d3e3-112">Maar Hallo doel van de webservice Hallo is ook tooserve als een voorbeeld van hoe Azure Machine Learning-webservices gebruikte toocreate boven op R-code kan zijn.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-112">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="8d3e3-113">Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="8d3e3-114">Hallo-webservice kan vervolgens worden gepubliceerde toohello Azure Marketplace en gebruikt door gebruikers en apparaten via hello world – geen instellingen infrastructuur door de auteur Hallo van Hallo-webservice is vereist.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-114">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world – no infrastructure setup by hello author of hello web service is required.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="8d3e3-115">Gebruik van web-service</span><span class="sxs-lookup"><span data-stu-id="8d3e3-115">Consumption of web service</span></span>
<span data-ttu-id="8d3e3-116">Hallo binomiaalverdeling Suite bevat Hallo 3-services te volgen.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-116">hello Binomial Distribution Suite includes hello following 3 services.</span></span>

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="8d3e3-117">Binomiaalverdeling kwantiel Rekenmachine</span><span class="sxs-lookup"><span data-stu-id="8d3e3-117">Binomial Distribution Quantile Calculator</span></span>
<span data-ttu-id="8d3e3-118">Deze service accepteert 4 argumenten van een normale verdeling en berekent kwantiel Hallo die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-118">This service accepts 4 arguments of a normal distribution and calculates hello associated quantile.</span></span>
<span data-ttu-id="8d3e3-119">Hallo invoerargumenten zijn:</span><span class="sxs-lookup"><span data-stu-id="8d3e3-119">hello input arguments are:</span></span>

* <span data-ttu-id="8d3e3-120">p - één geaggregeerd kans van meerdere proefversies.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-120">p - A single aggregated probability of multiple trials.</span></span>  
* <span data-ttu-id="8d3e3-121">grootte - Hallo aantal proefversies.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-121">size - hello number of trials.</span></span>
* <span data-ttu-id="8d3e3-122">kans - Hallo kans van slagen van een evaluatieversie.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-122">prob - hello probability of success in a trial.</span></span>
* <span data-ttu-id="8d3e3-123">Side - L voor lagere Hallo-zijde van Hallo distributie, U voor Hallo bovenzijde Hallo-verdeling.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-123">Side - L for hello lower side of hello distribution, U for hello upper side of hello distribution.</span></span> 

<span data-ttu-id="8d3e3-124">Hallo-uitvoer van Hallo-service is Hallo berekend kwantiel die is gekoppeld aan Hallo kans gegeven.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-124">hello output of hello service is hello calculated quantile that is associated with hello given probability.</span></span>

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="8d3e3-125">Binomiaalverdeling kans Rekenmachine</span><span class="sxs-lookup"><span data-stu-id="8d3e3-125">Binomial Distribution Probability Calculator</span></span>
<span data-ttu-id="8d3e3-126">Deze service accepteert 4 argumenten van een binomiaalverdeling en berekent de kans op Hallo die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-126">This service accepts 4 arguments of a binomial distribution and calculates hello associated probability.</span></span>
<span data-ttu-id="8d3e3-127">Hallo invoerargumenten zijn:</span><span class="sxs-lookup"><span data-stu-id="8d3e3-127">hello input arguments are:</span></span>

* <span data-ttu-id="8d3e3-128">q - a één kwantiel van een gebeurtenis met binomiaalverdeling.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-128">q - A single quantile of an event with binomial distribution.</span></span> 
* <span data-ttu-id="8d3e3-129">grootte - Hallo aantal proefversies.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-129">size - hello number of trials.</span></span>
* <span data-ttu-id="8d3e3-130">kans - Hallo kans van slagen van een evaluatieversie.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-130">prob - hello probability of success in a trial.</span></span>
* <span data-ttu-id="8d3e3-131">side - L voor lagere Hallo-zijde van Hallo distributiepunt, U voor Hallo bovenzijde Hallo verdeling of E dat één aantal geslaagde gelijk tooa.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-131">side - L for hello lower side of hello distribution, U for hello upper side of hello distribution, or E that is equal tooa single number of successes.</span></span>

<span data-ttu-id="8d3e3-132">Hallo-uitvoer van Hallo-service is Hallo berekend kans dat is gekoppeld aan Hallo kwantiel gegeven.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-132">hello output of hello service is hello calculated probability that is associated with hello given quantile.</span></span>

### <a name="binomial-distribution-generator"></a><span data-ttu-id="8d3e3-133">Binomiaalverdeling Generator</span><span class="sxs-lookup"><span data-stu-id="8d3e3-133">Binomial Distribution Generator</span></span>
<span data-ttu-id="8d3e3-134">Deze service accepteert 3 argumenten van een binomiaalverdeling en genereert een willekeurige volgorde van de getallen die met een binomially worden gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-134">This service accepts 3 arguments of a binomial distribution and generates a random sequence of numbers that are binomially distributed.</span></span> <span data-ttu-id="8d3e3-135">Hallo moeten volgende argumenten worden opgegeven tooit binnen Hallo-aanvraag:</span><span class="sxs-lookup"><span data-stu-id="8d3e3-135">hello following arguments should be provided tooit within hello request:</span></span>

* <span data-ttu-id="8d3e3-136">n - aantal metingen.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-136">n - Number of observations.</span></span> 
* <span data-ttu-id="8d3e3-137">grootte - aantal experimenten.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-137">size - Number of trials.</span></span>
* <span data-ttu-id="8d3e3-138">kans - kans van slagen.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-138">prob - Probability of success.</span></span>

<span data-ttu-id="8d3e3-139">Hallo-uitvoer van Hallo-service is een reeks van lengte n met een binomiaalverdeling op basis van de grootte en de kans argumenten Hallo.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-139">hello output of hello service is a sequence of length n with a binomial distribution based on hello size and prob arguments.</span></span>

> <span data-ttu-id="8d3e3-140">Deze service is gehost op Azure Marketplace Hallo een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-140">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="8d3e3-141">Er zijn meerdere manieren Hallo-service op automatische wijze verbruikt (voorbeeld-apps worden hier: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [kans Rekenmachine](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [kwantiel Rekenmachine](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span><span class="sxs-lookup"><span data-stu-id="8d3e3-141">There are multiple ways of consuming hello service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="8d3e3-142">C#-code voor het web service starten:</span><span class="sxs-lookup"><span data-stu-id="8d3e3-142">Starting C# code for web service consumption:</span></span>
### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="8d3e3-143">Binomiaalverdeling kwantiel Rekenmachine</span><span class="sxs-lookup"><span data-stu-id="8d3e3-143">Binomial Distribution Quantile Calculator</span></span>
    public class Input
    {
            public string p;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void main()
    {
            var input = new Input() { p = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="8d3e3-144">Binomiaalverdeling kans Rekenmachine</span><span class="sxs-lookup"><span data-stu-id="8d3e3-144">Binomial Distribution Probability Calculator</span></span>
    public class Input
    {
            public string q;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = " PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="binomial-distribution-generator"></a><span data-ttu-id="8d3e3-145">Binomiaalverdeling Generator</span><span class="sxs-lookup"><span data-stu-id="8d3e3-145">Binomial Distribution Generator</span></span>
    public class Input
    {
            public string n;
            public string size;
            public string p;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, size = TextBox2.Text, p = TextBox3.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }





## <a name="creation-of-web-service"></a><span data-ttu-id="8d3e3-146">Maken van de webservice</span><span class="sxs-lookup"><span data-stu-id="8d3e3-146">Creation of web service</span></span>
> <span data-ttu-id="8d3e3-147">Deze webservice is gemaakt met behulp van Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="8d3e3-148">Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="8d3e3-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="8d3e3-149">Hieronder staat een screenshot van Hallo experiment die Hallo web service en voorbeeld-code hebt gemaakt voor elk Hallo-modules in Hallo experiment.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-149">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="8d3e3-150">Binomiaalverdeling kwantiel Rekenmachine</span><span class="sxs-lookup"><span data-stu-id="8d3e3-150">Binomial Distribution Quantile Calculator</span></span>
![Werkruimte maken][4]

#### <a name="module-1"></a><span data-ttu-id="8d3e3-152">Module 1:</span><span class="sxs-lookup"><span data-stu-id="8d3e3-152">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port
#### <a name="module-2"></a><span data-ttu-id="8d3e3-153">2-module:</span><span class="sxs-lookup"><span data-stu-id="8d3e3-153">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }

    if (param$prob < 0 ) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 0
    } else if (param$prob > 1) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 1
    }

    quantile = qbinom(param$p,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    quantile

    if (param$side == 'U'){
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = F)
    band=subset(df,x>quantile)
    } else if (param$side =='L') {
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = T)
    band=subset(df,x<=quantile)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(quantile)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");


### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="8d3e3-154">Binomiaalverdeling kans Rekenmachine</span><span class="sxs-lookup"><span data-stu-id="8d3e3-154">Binomial Distribution Probability Calculator</span></span>
![Werkruimte maken][5]

#### <a name="module-1"></a><span data-ttu-id="8d3e3-156">Module 1:</span><span class="sxs-lookup"><span data-stu-id="8d3e3-156">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port


#### <a name="module-2"></a><span data-ttu-id="8d3e3-157">2-module:</span><span class="sxs-lookup"><span data-stu-id="8d3e3-157">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    prob = pbinom(param$q,size=param$size,prob=param$prob)
    prob.eq = dbinom(param$q,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    prob

    if (param$side == 'U'){
    prob = 1 - prob
    band=subset(df,x>param$q)
    } else if (param$side =='E') {
    prob = prob.eq
    band=subset(df,x==param$q)
    } else if (param$side =='L') {
    prob = prob
    band=subset(df,x<=param$q)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="binomial-distribution-generator"></a><span data-ttu-id="8d3e3-158">Binomiaalverdeling Generator</span><span class="sxs-lookup"><span data-stu-id="8d3e3-158">Binomial Distribution Generator</span></span>
![Werkruimte maken][6]

#### <a name="module-1"></a><span data-ttu-id="8d3e3-160">Module 1:</span><span class="sxs-lookup"><span data-stu-id="8d3e3-160">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data toooutput port

#### <a name="module-2"></a><span data-ttu-id="8d3e3-161">2-module:</span><span class="sxs-lookup"><span data-stu-id="8d3e3-161">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="8d3e3-162">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="8d3e3-162">Limitations</span></span>
<span data-ttu-id="8d3e3-163">Dit zijn eenvoudige voorbeelden omringende Hallo binomiaalverdeling.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-163">These are very simple examples surrounding hello binomial distribution.</span></span> <span data-ttu-id="8d3e3-164">Zoals u kunt zien van Hallo voorbeeldcode hierboven, is weinig fout vastgelegd geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="8d3e3-164">As can be seen from hello example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="8d3e3-165">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="8d3e3-165">FAQ</span></span>
<span data-ttu-id="8d3e3-166">Zie voor veelgestelde vragen over het verbruik van de webservice Hallo of publishing toohello Azure Marketplace [hier](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="8d3e3-166">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

