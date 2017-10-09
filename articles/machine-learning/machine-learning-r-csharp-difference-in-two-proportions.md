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
# <a name="deprecated-difference-in-proportions-test"></a>(afgeschaft) Verschil in verhouding Test

> [!NOTE]
> Hallo Microsoft DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft. 
> 
> U vindt veel nuttige voorbeeld experimenten en API's in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Zie voor meer informatie over Hallo galerie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

Zijn de twee verhoudingen statistisch verschillen? Stel dat een gebruiker wil toocompare twee films toodetermine als één film een aanzienlijk hoger deel van heeft 'graag' wanneer toohello andere vergeleken. Met een grote steekproef, kan er een statistisch aanzienlijke verschil tussen Hallo verhoudingen 0,50 en 0,51. Met een kort voorbeeld er mogelijk niet voldoende gegevens toodetermine als deze verhoudingen daadwerkelijk verschillen. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Dit [webservice](https://datamarket.azure.com/dataset/aml_labs/prop_test) voert een test hypothese van Hallo verschil in twee verhoudingen op basis van gebruikersinvoer van Hallo aantal successen en Hallo kunt u het totale aantal proefversies voor Hallo 2 vergelijking groepen. In een voorbeeldscenario kan deze webservice worden aangeroepen vanuit een film vergelijking-app waarin Hallo gebruiker of een van de Hallo films echt 'bevallen is' vaker dan Hallo andere, op basis van classificatie van films.

> Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer. Maar Hallo doel van de webservice Hallo is ook tooserve als een voorbeeld van hoe Azure Machine Learning-webservices gebruikte toocreate boven op R-code kan zijn. Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice. Hallo-webservice vervolgens gepubliceerde toohello Azure Marketplace kan worden en verbruikt door gebruikers en apparaten via Hallo wereld zonder instellingen infrastructuur door de auteur Hallo van Hallo-webservice.
> 
> 

## <a name="consumption-of-web-service"></a>Gebruik van web-service
Deze service accepteert 4 argumenten en biedt een hypothese test van verhoudingen.

Hallo invoerargumenten zijn:

* Successes1 - aantal geslaagde gebeurtenissen in voorbeeld 1.
* Successes2 - aantal geslaagde gebeurtenissen in voorbeeld 2.
* Total1 - grootte van voorbeeld 1.
* Total2 - grootte van voorbeeld 2.

Hallo-uitvoer van Hallo-service is Hallo resultaat van Hallo hypothese testen samen met de Hallo chi-square statistiek, df, p-waarde en het aandeel in voorbeeld 1/2- en betrouwbaarheidsinterval grenzen.

> Deze service is gehost op Azure Marketplace Hallo een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden. 
> 
> 

Er zijn meerdere manieren Hallo-service op automatische wijze verbruikt (een voorbeeld-app is [hier](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>C#-code voor het web service starten:
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


## <a name="creation-of-web-service"></a>Maken van de webservice
> Deze webservice is gemaakt met behulp van Azure Machine Learning. Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml). Hieronder staat een screenshot van Hallo experiment die Hallo web service en voorbeeld-code hebt gemaakt voor elk Hallo-modules in Hallo experiment.
> 
> 

In Azure Machine Learning, een nieuw, leeg experiment is gemaakt met twee [R-Script uitvoeren] [ execute-r-script] modules. Hallo gegevensschema is in de eerste module Hallo gedefinieerd, terwijl de tweede Hallo-module met Hallo prop.test opdracht in R tooperform Hallo hypothese test voor 2 verhoudingen. 

### <a name="experiment-flow"></a>Stroom experiment:
![Experiment stroom][2]

#### <a name="module-1"></a>Module 1:
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data toooutput port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a>2-module:
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


## <a name="limitations"></a>Beperkingen
Dit is een zeer eenvoudige voorbeeld voor een test van verschil in verhouding van 2. Zoals u kunt zien van Hallo voorbeeldcode hierboven, geen fout vastgelegd is geïmplementeerd en Hallo-service wordt ervan uitgegaan dat alle Hallo variabelen continue.

## <a name="faq"></a>Veelgestelde vragen
Zie voor veelgestelde vragen over het verbruik van de webservice Hallo of publishing toohello Azure Marketplace [hier](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

