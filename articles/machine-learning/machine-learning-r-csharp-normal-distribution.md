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
# <a name="deprecated-normal-distribution-suite"></a>(afgeschaft) Normale verdeling Suite

> [!NOTE]
> De Microsoft-DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft. 
> 
> U kunt zoeken veel nuttige voorbeeld experimenten en API's in de [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Zie voor meer informatie over de Gallery [Share en het detecteren van bronnen in de Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

De normaalverdeling Suite is een reeks webservices voorbeeld ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [kwantiel Rekenmachine](https://datamarket.azure.com/dataset/aml_labs/ndq5), [kans Rekenmachine](https://datamarket.azure.com/dataset/aml_labs/ndp5)) die helpen bij het genereren en verwerking van de normale verdelingen. De services kunnen genereren van een reeks normale verdeling van een willekeurige lengte, quantiles van een bepaalde waarschijnlijkheid berekenen en waarschijnlijkheid van een bepaalde kwantiel berekenen. Elk van de services andere uitvoer, op basis van de geselecteerde service verzendt (Zie onderstaande beschrijving). De Suite normale distributie is gebaseerd op de R functies qnorm rnorm en pnorm, die zijn opgenomen in statistieken-R-pakket.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer. Maar het doel van de webservice is ook als een voorbeeld van hoe Azure Machine Learning-webservices boven op R code maken kan worden gebruikt. Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice. De webservice kan vervolgens worden gepubliceerd naar Azure Marketplace en verbruikt door gebruikers en apparaten over de hele wereld zonder instellingen infrastructuur door de auteur van de webservice.  
> 
> 

## <a name="consumption-of-web-service"></a>Gebruik van web-service
De normaalverdeling Suite omvat de volgende 3-services.

### <a name="normal-distribution-quantile-calculator"></a>Normale verdeling kwantiel Rekenmachine
Deze service accepteert 4 argumenten van een normale verdeling en de bijbehorende kwantiel berekent.

De invoerargumenten zijn:

* p - een enkele waarschijnlijkheid van een gebeurtenis met normale verdeling. 
* gemiddelde - het gemiddelde van de normale verdeling.
* SD - de standaarddeviatie van de normale verdeling. 
* Side - L voor het onderste gedeelte van het distributiepunt en U voor de bovenzijde van het distributiepunt.

De uitvoer van de service is de berekende kwantiel die is gekoppeld aan de opgegeven kans.

### <a name="normal-distribution-probability-calculator"></a>Normale verdeling kans Rekenmachine
Deze service accepteert 4 argumenten van een normale verdeling en de bijbehorende kans berekent.

De invoerargumenten zijn:

* q - a één kwantiel van een gebeurtenis met normale verdeling. 
* gemiddelde - het gemiddelde van de normale verdeling.
* SD - de standaarddeviatie van de normale verdeling. 
* Side - L voor het onderste gedeelte van het distributiepunt en U voor de bovenzijde van het distributiepunt.

De uitvoer van de service is de berekende kans die is gekoppeld aan de opgegeven kwantiel.

### <a name="normal-distribution-generator"></a>Normale verdeling Generator
Deze service accepteert 3 argumenten van een normale verdeling en genereert een willekeurige volgorde van de cijfers die normaal gesproken worden gedistribueerd. De volgende argumenten moeten worden opgegeven in de aanvraag:

* n - het aantal metingen. 
* gemiddelde - het gemiddelde van de normale verdeling.
* SD - de standaarddeviatie van de normale verdeling. 

De uitvoer van de service is een opeenvolging van lengte n met een normale verdeling op basis van de gemiddelde en sd-argumenten.

> Deze service wordt gehost op Azure Marketplace, een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden. 
> 
> 

Er zijn meerdere manieren van de consumptie van de service op automatische wijze (voorbeeld-apps worden hier: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [kans Rekenmachine](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [kwantiel Rekenmachine](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>C#-code voor het web service starten:
### <a name="normal-distribution-quantile-calculator"></a>Normale verdeling kwantiel Rekenmachine
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


### <a name="normal-distribution-probability-calculator"></a>Normale verdeling kans Rekenmachine
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

### <a name="normal-distribution-generator"></a>Normale verdeling Generator
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


## <a name="creation-of-web-service"></a>Maken van de webservice
> Deze webservice is gemaakt met behulp van Azure Machine Learning. Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml). 
> 
> 

Hieronder vindt u een schermopname van het experiment dat de web-service en een voorbeeld van code voor elk van de modules in het experiment gemaakt.

### <a name="normal-distribution-quantile-calculator"></a>Normale verdeling kwantiel Rekenmachine
Stroom experiment:

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

### <a name="normal-distribution-probability-calculator"></a>Normale verdeling kans Rekenmachine
Stroom experiment:

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

### <a name="normal-distribution-generator"></a>Normale verdeling Generator
Stroom experiment:

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

## <a name="limitations"></a>Beperkingen
Dit zijn eenvoudige voorbeelden rondom de normale verdeling. Zoals u kunt zien van de bovenstaande voorbeeldcode, is weinig fout vastgelegd geïmplementeerd.

## <a name="faq"></a>Veelgestelde vragen
Zie voor veelgestelde vragen over het verbruik van de webservice of publiceren naar Azure Marketplace [hier](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

