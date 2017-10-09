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
# <a name="deprecated-normal-distribution-suite"></a>(afgeschaft) Normale verdeling Suite

> [!NOTE]
> Hallo Microsoft DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft. 
> 
> U vindt veel nuttige voorbeeld experimenten en API's in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Zie voor meer informatie over Hallo galerie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

Hallo normaalverdeling Suite is een reeks webservices voorbeeld ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [kwantiel Rekenmachine](https://datamarket.azure.com/dataset/aml_labs/ndq5), [kans Rekenmachine](https://datamarket.azure.com/dataset/aml_labs/ndp5)) die helpen bij het genereren en verwerking normale verdelingen. Hallo-services kunnen genereren van een reeks normale verdeling van een willekeurige lengte, quantiles van een bepaalde waarschijnlijkheid berekenen en waarschijnlijkheid van een bepaalde kwantiel berekenen. Elk van de services Hallo andere uitvoer, op basis van geselecteerde Hallo service verzendt (Zie onderstaande beschrijving). Hallo normaalverdeling Suite is gebaseerd op Hallo R functies qnorm rnorm en pnorm, die zijn opgenomen in statistieken-R-pakket.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer. Maar Hallo doel van de webservice Hallo is ook tooserve als een voorbeeld van hoe Azure Machine Learning-webservices gebruikte toocreate boven op R-code kan zijn. Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice. Hallo-webservice vervolgens gepubliceerde toohello Azure Marketplace kan worden en verbruikt door gebruikers en apparaten via Hallo wereld zonder instellingen infrastructuur door de auteur Hallo van Hallo-webservice.  
> 
> 

## <a name="consumption-of-web-service"></a>Gebruik van web-service
Hallo normaalverdeling Suite bevat Hallo 3-services te volgen.

### <a name="normal-distribution-quantile-calculator"></a>Normale verdeling kwantiel Rekenmachine
Deze service accepteert 4 argumenten van een normale verdeling en berekent kwantiel Hallo die zijn gekoppeld.

Hallo invoerargumenten zijn:

* p - een enkele waarschijnlijkheid van een gebeurtenis met normale verdeling. 
* Gemiddelde - Hallo normale verdeling gemiddelde.
* SD - standaardafwijking Hallo-normale distributie. 
* Side - L voor lagere zijde Hallo Hallo verdeling en U voor Hallo bovenzijde Hallo-verdeling.

Hallo-uitvoer van Hallo-service is Hallo berekend kwantiel die is gekoppeld aan Hallo kans gegeven.

### <a name="normal-distribution-probability-calculator"></a>Normale verdeling kans Rekenmachine
Deze service accepteert 4 argumenten van een normale verdeling en berekent de kans op Hallo die zijn gekoppeld.

Hallo invoerargumenten zijn:

* q - a één kwantiel van een gebeurtenis met normale verdeling. 
* Gemiddelde - Hallo normale verdeling gemiddelde.
* SD - standaardafwijking Hallo-normale distributie. 
* Side - L voor lagere zijde Hallo Hallo verdeling en U voor Hallo bovenzijde Hallo-verdeling.

Hallo-uitvoer van Hallo-service is Hallo berekend kans dat is gekoppeld aan Hallo kwantiel gegeven.

### <a name="normal-distribution-generator"></a>Normale verdeling Generator
Deze service accepteert 3 argumenten van een normale verdeling en genereert een willekeurige volgorde van de cijfers die normaal gesproken worden gedistribueerd. Hallo moeten volgende argumenten worden opgegeven tooit binnen Hallo-aanvraag:

* n - Hallo aantal metingen. 
* gemiddelde - Hallo normale verdeling gemiddelde.
* SD - standaardafwijking Hallo-normale distributie. 

Hallo-uitvoer van Hallo-service is een reeks van lengte n met een normale verdeling op basis van Hallo gemiddelde en sd-argumenten.

> Deze service is gehost op Azure Marketplace Hallo een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden. 
> 
> 

Er zijn meerdere manieren Hallo-service op automatische wijze verbruikt (voorbeeld-apps worden hier: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [kans Rekenmachine](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [kwantiel Rekenmachine](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).

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

Hieronder staat een screenshot van Hallo experiment die Hallo web service en voorbeeld-code hebt gemaakt voor elk Hallo-modules in Hallo experiment.

### <a name="normal-distribution-quantile-calculator"></a>Normale verdeling kwantiel Rekenmachine
Stroom experiment:

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

### <a name="normal-distribution-probability-calculator"></a>Normale verdeling kans Rekenmachine
Stroom experiment:

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

### <a name="normal-distribution-generator"></a>Normale verdeling Generator
Stroom experiment:

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

## <a name="limitations"></a>Beperkingen
Dit zijn eenvoudige voorbeelden omringende Hallo normaalverdeling. Zoals u kunt zien van Hallo voorbeeldcode hierboven, is weinig fout vastgelegd geïmplementeerd.

## <a name="faq"></a>Veelgestelde vragen
Zie voor veelgestelde vragen over het verbruik van de webservice Hallo of publishing toohello Azure Marketplace [hier](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

