---
title: (afgeschaft) Normale verdeling Web Service Suite - Azure | Microsoft Docs
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
redirect_document_id: TRUE
ms.openlocfilehash: 79d1621330ad56b0c62ca46cfac424c2306e371f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-normal-distribution-suite"></a><span data-ttu-id="cdf85-103">(afgeschaft) Normale verdeling Suite</span><span class="sxs-lookup"><span data-stu-id="cdf85-103">(deprecated) Normal Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="cdf85-104">De Microsoft-DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="cdf85-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="cdf85-105">U kunt zoeken veel nuttige voorbeeld experimenten en API's in de [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="cdf85-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="cdf85-106">Zie voor meer informatie over de Gallery [Share en het detecteren van bronnen in de Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="cdf85-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="cdf85-107">De normaalverdeling Suite is een reeks webservices voorbeeld ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [kwantiel Rekenmachine](https://datamarket.azure.com/dataset/aml_labs/ndq5), [kans Rekenmachine](https://datamarket.azure.com/dataset/aml_labs/ndp5)) die helpen bij het genereren en verwerking van de normale verdelingen.</span><span class="sxs-lookup"><span data-stu-id="cdf85-107">The Normal Distribution Suite is a set of sample web services ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/ndp5)) that help in generating and handling normal distributions.</span></span> <span data-ttu-id="cdf85-108">De services kunnen genereren van een reeks normale verdeling van een willekeurige lengte, quantiles van een bepaalde waarschijnlijkheid berekenen en waarschijnlijkheid van een bepaalde kwantiel berekenen.</span><span class="sxs-lookup"><span data-stu-id="cdf85-108">The services allow generating a normal distribution sequence of any length, calculating quantiles from a given probability, and calculating probability from a given quantile.</span></span> <span data-ttu-id="cdf85-109">Elk van de services andere uitvoer, op basis van de geselecteerde service verzendt (Zie onderstaande beschrijving).</span><span class="sxs-lookup"><span data-stu-id="cdf85-109">Each of the services emits different outputs based on the selected service (see description below).</span></span> <span data-ttu-id="cdf85-110">De Suite normale distributie is gebaseerd op de R functies qnorm rnorm en pnorm, die zijn opgenomen in statistieken-R-pakket.</span><span class="sxs-lookup"><span data-stu-id="cdf85-110">The Normal Distribution Suite is based on the R functions qnorm, rnorm, and pnorm, which are included in R stats package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="cdf85-111">Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer.</span><span class="sxs-lookup"><span data-stu-id="cdf85-111">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="cdf85-112">Maar het doel van de webservice is ook als een voorbeeld van hoe Azure Machine Learning-webservices boven op R code maken kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cdf85-112">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="cdf85-113">Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice.</span><span class="sxs-lookup"><span data-stu-id="cdf85-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="cdf85-114">De webservice kan vervolgens worden gepubliceerd naar Azure Marketplace en verbruikt door gebruikers en apparaten over de hele wereld zonder instellingen infrastructuur door de auteur van de webservice.</span><span class="sxs-lookup"><span data-stu-id="cdf85-114">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="cdf85-115">Gebruik van web-service</span><span class="sxs-lookup"><span data-stu-id="cdf85-115">Consumption of web service</span></span>
<span data-ttu-id="cdf85-116">De normaalverdeling Suite omvat de volgende 3-services.</span><span class="sxs-lookup"><span data-stu-id="cdf85-116">The Normal Distribution Suite includes the following 3 services.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="cdf85-117">Normale verdeling kwantiel Rekenmachine</span><span class="sxs-lookup"><span data-stu-id="cdf85-117">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="cdf85-118">Deze service accepteert 4 argumenten van een normale verdeling en de bijbehorende kwantiel berekent.</span><span class="sxs-lookup"><span data-stu-id="cdf85-118">This service accepts 4 arguments of a normal distribution and calculates the associated quantile.</span></span>

<span data-ttu-id="cdf85-119">De invoerargumenten zijn:</span><span class="sxs-lookup"><span data-stu-id="cdf85-119">The input arguments are:</span></span>

* <span data-ttu-id="cdf85-120">p - een enkele waarschijnlijkheid van een gebeurtenis met normale verdeling.</span><span class="sxs-lookup"><span data-stu-id="cdf85-120">p - A single probability of an event with normal distribution.</span></span> 
* <span data-ttu-id="cdf85-121">gemiddelde - het gemiddelde van de normale verdeling.</span><span class="sxs-lookup"><span data-stu-id="cdf85-121">Mean - The normal distribution mean.</span></span>
* <span data-ttu-id="cdf85-122">SD - de standaarddeviatie van de normale verdeling.</span><span class="sxs-lookup"><span data-stu-id="cdf85-122">SD - The normal distribution standard deviation.</span></span> 
* <span data-ttu-id="cdf85-123">Side - L voor het onderste gedeelte van het distributiepunt en U voor de bovenzijde van het distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="cdf85-123">Side - L for the lower side of the distribution and U for the upper side of the distribution.</span></span>

<span data-ttu-id="cdf85-124">De uitvoer van de service is de berekende kwantiel die is gekoppeld aan de opgegeven kans.</span><span class="sxs-lookup"><span data-stu-id="cdf85-124">The output of the service is the calculated quantile that is associated with the given probability.</span></span>

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="cdf85-125">Normale verdeling kans Rekenmachine</span><span class="sxs-lookup"><span data-stu-id="cdf85-125">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="cdf85-126">Deze service accepteert 4 argumenten van een normale verdeling en de bijbehorende kans berekent.</span><span class="sxs-lookup"><span data-stu-id="cdf85-126">This service accepts 4 arguments of a normal distribution and calculates the associated probability.</span></span>

<span data-ttu-id="cdf85-127">De invoerargumenten zijn:</span><span class="sxs-lookup"><span data-stu-id="cdf85-127">The input arguments are:</span></span>

* <span data-ttu-id="cdf85-128">q - a één kwantiel van een gebeurtenis met normale verdeling.</span><span class="sxs-lookup"><span data-stu-id="cdf85-128">q - A single quantile of an event with normal distribution.</span></span> 
* <span data-ttu-id="cdf85-129">gemiddelde - het gemiddelde van de normale verdeling.</span><span class="sxs-lookup"><span data-stu-id="cdf85-129">Mean - The normal distribution mean.</span></span>
* <span data-ttu-id="cdf85-130">SD - de standaarddeviatie van de normale verdeling.</span><span class="sxs-lookup"><span data-stu-id="cdf85-130">SD - The normal distribution standard deviation.</span></span> 
* <span data-ttu-id="cdf85-131">Side - L voor het onderste gedeelte van het distributiepunt en U voor de bovenzijde van het distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="cdf85-131">Side - L for the lower side of the distribution and U for the upper side of the distribution.</span></span>

<span data-ttu-id="cdf85-132">De uitvoer van de service is de berekende kans die is gekoppeld aan de opgegeven kwantiel.</span><span class="sxs-lookup"><span data-stu-id="cdf85-132">The output of the service is the calculated probability that is associated with the given quantile.</span></span>

### <a name="normal-distribution-generator"></a><span data-ttu-id="cdf85-133">Normale verdeling Generator</span><span class="sxs-lookup"><span data-stu-id="cdf85-133">Normal Distribution Generator</span></span>
<span data-ttu-id="cdf85-134">Deze service accepteert 3 argumenten van een normale verdeling en genereert een willekeurige volgorde van de cijfers die normaal gesproken worden gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="cdf85-134">This service accepts 3 arguments of a normal distribution and generates a random sequence of numbers that are normally distributed.</span></span> <span data-ttu-id="cdf85-135">De volgende argumenten moeten worden opgegeven in de aanvraag:</span><span class="sxs-lookup"><span data-stu-id="cdf85-135">The following arguments should be provided to it within the request:</span></span>

* <span data-ttu-id="cdf85-136">n - het aantal metingen.</span><span class="sxs-lookup"><span data-stu-id="cdf85-136">n - The number of observations.</span></span> 
* <span data-ttu-id="cdf85-137">gemiddelde - het gemiddelde van de normale verdeling.</span><span class="sxs-lookup"><span data-stu-id="cdf85-137">mean - The normal distribution mean.</span></span>
* <span data-ttu-id="cdf85-138">SD - de standaarddeviatie van de normale verdeling.</span><span class="sxs-lookup"><span data-stu-id="cdf85-138">sd - The normal distribution standard deviation.</span></span> 

<span data-ttu-id="cdf85-139">De uitvoer van de service is een opeenvolging van lengte n met een normale verdeling op basis van de gemiddelde en sd-argumenten.</span><span class="sxs-lookup"><span data-stu-id="cdf85-139">The output of the service is a sequence of length n with a normal distribution based on the mean and sd arguments.</span></span>

> <span data-ttu-id="cdf85-140">Deze service wordt gehost op Azure Marketplace, een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden.</span><span class="sxs-lookup"><span data-stu-id="cdf85-140">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="cdf85-141">Er zijn meerdere manieren van de consumptie van de service op automatische wijze (voorbeeld-apps worden hier: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [kans Rekenmachine](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [kwantiel Rekenmachine](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span><span class="sxs-lookup"><span data-stu-id="cdf85-141">There are multiple ways of consuming the service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="cdf85-142">C#-code voor het web service starten:</span><span class="sxs-lookup"><span data-stu-id="cdf85-142">Starting C# code for web service consumption:</span></span>
### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="cdf85-143">Normale verdeling kwantiel Rekenmachine</span><span class="sxs-lookup"><span data-stu-id="cdf85-143">Normal Distribution Quantile Calculator</span></span>
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


### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="cdf85-144">Normale verdeling kans Rekenmachine</span><span class="sxs-lookup"><span data-stu-id="cdf85-144">Normal Distribution Probability Calculator</span></span>
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

### <a name="normal-distribution-generator"></a><span data-ttu-id="cdf85-145">Normale verdeling Generator</span><span class="sxs-lookup"><span data-stu-id="cdf85-145">Normal Distribution Generator</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="cdf85-146">Maken van de webservice</span><span class="sxs-lookup"><span data-stu-id="cdf85-146">Creation of web service</span></span>
> <span data-ttu-id="cdf85-147">Deze webservice is gemaakt met behulp van Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="cdf85-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="cdf85-148">Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="cdf85-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> 
> 
> 

<span data-ttu-id="cdf85-149">Hieronder vindt u een schermopname van het experiment dat de web-service en een voorbeeld van code voor elk van de modules in het experiment gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cdf85-149">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="cdf85-150">Normale verdeling kwantiel Rekenmachine</span><span class="sxs-lookup"><span data-stu-id="cdf85-150">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="cdf85-151">Stroom experiment:</span><span class="sxs-lookup"><span data-stu-id="cdf85-151">Experiment flow:</span></span>

![Experiment stroom][2]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
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

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="cdf85-153">Normale verdeling kans Rekenmachine</span><span class="sxs-lookup"><span data-stu-id="cdf85-153">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="cdf85-154">Stroom experiment:</span><span class="sxs-lookup"><span data-stu-id="cdf85-154">Experiment flow:</span></span>

![Experiment stroom][3]

     #Data schema with example data (replaced with data from web service)
    data.set=data.frame(q=-1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
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

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-generator"></a><span data-ttu-id="cdf85-156">Normale verdeling Generator</span><span class="sxs-lookup"><span data-stu-id="cdf85-156">Normal Distribution Generator</span></span>
<span data-ttu-id="cdf85-157">Stroom experiment:</span><span class="sxs-lookup"><span data-stu-id="cdf85-157">Experiment flow:</span></span>

![Experiment stroom][4]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,mean=0,sd=1);
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    dist = rnorm(param$n,mean=param$mean,sd=param$sd)

    output = as.data.frame(t(dist))

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="cdf85-159">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="cdf85-159">Limitations</span></span>
<span data-ttu-id="cdf85-160">Dit zijn eenvoudige voorbeelden rondom de normale verdeling.</span><span class="sxs-lookup"><span data-stu-id="cdf85-160">These are very simple examples surrounding the normal distribution.</span></span> <span data-ttu-id="cdf85-161">Zoals u kunt zien van de bovenstaande voorbeeldcode, is weinig fout vastgelegd geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="cdf85-161">As can be seen from the example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="cdf85-162">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="cdf85-162">FAQ</span></span>
<span data-ttu-id="cdf85-163">Zie voor veelgestelde vragen over het verbruik van de webservice of publiceren naar Azure Marketplace [hier](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="cdf85-163">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

