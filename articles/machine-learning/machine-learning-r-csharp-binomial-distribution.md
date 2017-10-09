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
# <a name="deprecated-binomial-distribution-suite"></a>(afgeschaft) Binomiaalverdeling Suite

> [!NOTE]
> Hallo Microsoft DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft. 
> 
> U vindt veel nuttige voorbeeld experimenten en API's in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Zie voor meer informatie over Hallo galerie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

Hallo binomiaalverdeling Suite is een reeks webservices voorbeeld ([binomiale Generator](https://datamarket.azure.com/dataset/aml_labs/bdg5), [kans Rekenmachine](https://datamarket.azure.com/dataset/aml_labs/bdp4), [kwantiel Rekenmachine](https://datamarket.azure.com/dataset/aml_labs/bdq5)) die helpen bij het genereren en Omgaan met binomiale distributies. Hallo services kunnen genereren van een reeks binomiaalverdeling van een willekeurige lengte, quantiles berekenen gegeven van kans en berekenen waarschijnlijkheid van een bepaalde kwantiel. Elk van de services Hallo andere uitvoer, op basis van geselecteerde Hallo service verzendt (Zie onderstaande beschrijving). Hallo binomiaalverdeling Suite is gebaseerd op Hallo R functies qbinom rbinom en pbinom, die zijn opgenomen in Hallo R statistieken-pakket. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Deze webservices kunnen worden gebruikt door gebruikers – mogelijk rechtstreeks op Hallo marketplace, via een mobiele app via een website of zelfs op een lokale computer, bijvoorbeeld. Maar Hallo doel van de webservice Hallo is ook tooserve als een voorbeeld van hoe Azure Machine Learning-webservices gebruikte toocreate boven op R-code kan zijn. Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice. Hallo-webservice kan vervolgens worden gepubliceerde toohello Azure Marketplace en gebruikt door gebruikers en apparaten via hello world – geen instellingen infrastructuur door de auteur Hallo van Hallo-webservice is vereist.
> 
> 

## <a name="consumption-of-web-service"></a>Gebruik van web-service
Hallo binomiaalverdeling Suite bevat Hallo 3-services te volgen.

### <a name="binomial-distribution-quantile-calculator"></a>Binomiaalverdeling kwantiel Rekenmachine
Deze service accepteert 4 argumenten van een normale verdeling en berekent kwantiel Hallo die zijn gekoppeld.
Hallo invoerargumenten zijn:

* p - één geaggregeerd kans van meerdere proefversies.  
* grootte - Hallo aantal proefversies.
* kans - Hallo kans van slagen van een evaluatieversie.
* Side - L voor lagere Hallo-zijde van Hallo distributie, U voor Hallo bovenzijde Hallo-verdeling. 

Hallo-uitvoer van Hallo-service is Hallo berekend kwantiel die is gekoppeld aan Hallo kans gegeven.

### <a name="binomial-distribution-probability-calculator"></a>Binomiaalverdeling kans Rekenmachine
Deze service accepteert 4 argumenten van een binomiaalverdeling en berekent de kans op Hallo die zijn gekoppeld.
Hallo invoerargumenten zijn:

* q - a één kwantiel van een gebeurtenis met binomiaalverdeling. 
* grootte - Hallo aantal proefversies.
* kans - Hallo kans van slagen van een evaluatieversie.
* side - L voor lagere Hallo-zijde van Hallo distributiepunt, U voor Hallo bovenzijde Hallo verdeling of E dat één aantal geslaagde gelijk tooa.

Hallo-uitvoer van Hallo-service is Hallo berekend kans dat is gekoppeld aan Hallo kwantiel gegeven.

### <a name="binomial-distribution-generator"></a>Binomiaalverdeling Generator
Deze service accepteert 3 argumenten van een binomiaalverdeling en genereert een willekeurige volgorde van de getallen die met een binomially worden gedistribueerd. Hallo moeten volgende argumenten worden opgegeven tooit binnen Hallo-aanvraag:

* n - aantal metingen. 
* grootte - aantal experimenten.
* kans - kans van slagen.

Hallo-uitvoer van Hallo-service is een reeks van lengte n met een binomiaalverdeling op basis van de grootte en de kans argumenten Hallo.

> Deze service is gehost op Azure Marketplace Hallo een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden. 
> 
> 

Er zijn meerdere manieren Hallo-service op automatische wijze verbruikt (voorbeeld-apps worden hier: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [kans Rekenmachine](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [kwantiel Rekenmachine](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)). 

### <a name="starting-c-code-for-web-service-consumption"></a>C#-code voor het web service starten:
### <a name="binomial-distribution-quantile-calculator"></a>Binomiaalverdeling kwantiel Rekenmachine
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

### <a name="binomial-distribution-probability-calculator"></a>Binomiaalverdeling kans Rekenmachine
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


### <a name="binomial-distribution-generator"></a>Binomiaalverdeling Generator
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





## <a name="creation-of-web-service"></a>Maken van de webservice
> Deze webservice is gemaakt met behulp van Azure Machine Learning. Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml). Hieronder staat een screenshot van Hallo experiment die Hallo web service en voorbeeld-code hebt gemaakt voor elk Hallo-modules in Hallo experiment.
> 
> 

### <a name="binomial-distribution-quantile-calculator"></a>Binomiaalverdeling kwantiel Rekenmachine
![Werkruimte maken][4]

#### <a name="module-1"></a>Module 1:
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port
#### <a name="module-2"></a>2-module:
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


### <a name="binomial-distribution-probability-calculator"></a>Binomiaalverdeling kans Rekenmachine
![Werkruimte maken][5]

#### <a name="module-1"></a>Module 1:
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port


#### <a name="module-2"></a>2-module:
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

### <a name="binomial-distribution-generator"></a>Binomiaalverdeling Generator
![Werkruimte maken][6]

#### <a name="module-1"></a>Module 1:
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data toooutput port

#### <a name="module-2"></a>2-module:
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a>Beperkingen
Dit zijn eenvoudige voorbeelden omringende Hallo binomiaalverdeling. Zoals u kunt zien van Hallo voorbeeldcode hierboven, is weinig fout vastgelegd geïmplementeerd.

## <a name="faq"></a>Veelgestelde vragen
Zie voor veelgestelde vragen over het verbruik van de webservice Hallo of publishing toohello Azure Marketplace [hier](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

