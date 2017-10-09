---
title: AAA(deprecated) Multivariate Linear Regression - Azure | Microsoft Docs
description: (afgeschaft) Multidimensionale lineaire regressie
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 2fb78220-ced9-4564-a439-9e5df6772994
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
ms.openlocfilehash: 0ff7221cd06c0ef059b0c5bf327016588174dcfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-multivariate-linear-regression"></a>(afgeschaft) Multidimensionale lineaire regressie

> [!NOTE]
> Hallo Microsoft DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft. 
> 
> U vindt veel nuttige voorbeeld experimenten en API's in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Zie voor meer informatie over Hallo galerie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

Stel dat u hebt een gegevensset en zou zoals tooquickly voorspellen een afhankelijke variabele (y) voor elke afzonderlijke (i) op basis van onafhankelijke variabelen. Lineaire regressie is een populair statistische techniek voor dergelijke voorspellingen. Hallo afhankelijke variabele y wordt hier uitgegaan van een doorlopende waarde toobe.  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Een eenvoudig scenario mogelijk waarin Hallo onderzoeker probeert toopredict Hallo gewicht van een persoon (y), op basis van hun hoogte (x). Een meer geavanceerde scenario mogelijk waarbij Hallo onderzoeker bevat extra informatie voor Hallo afzonderlijke (zoals gewicht, geslacht, race) en probeert toopredict Hallo gewicht van Hallo afzonderlijk. Dit [webservice](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) past Hallo lineaire regressie toohello modelgegevens en uitvoer Hallo voorspelde waarde (y) voor elk Hallo metingen in Hallo-gegevens.

> Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer. Maar Hallo doel van de webservice Hallo is ook tooserve als een voorbeeld van hoe Azure Machine Learning-webservices gebruikte toocreate boven op R-code kan zijn. Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice. Hallo-webservice vervolgens gepubliceerde toohello Azure Marketplace kan worden en verbruikt door gebruikers en apparaten via Hallo wereld zonder instellingen infrastructuur door de auteur Hallo van Hallo-webservice.  
> 
> 

## <a name="consumption-of-web-service"></a>Gebruik van web-service
Deze web-service biedt Hallo voorspelde waarden van Hallo afhankelijke variabele op basis van onafhankelijke variabelen Hallo voor alle Hallo opmerkingen. Hallo-webservice verwacht Hallo eindgebruiker tooinput gegevens als een tekenreeks waarin rijen worden gescheiden door een komma (,) en kolommen worden gescheiden door puntkomma's (;). Hallo-webservice 1 rij tegelijk verwacht en Hallo eerste kolom toobe Hallo afhankelijke variabele verwacht. Een voorbeeld van de gegevensset kan er als volgt uitzien:

![Voorbeeldgegevens][1]

Opmerkingen zonder een afhankelijke variabele moeten worden ingevoerd als 'N.V.T.' voor y. Hallo gegevens invoeren voor Hallo hierboven gegevensset zou worden Hallo de volgende tekenreeks: "10, 5, 2,18; 1; 6,6; 5.3; 2.1,7; 5; 5,22; 3; 4,12; 2, 1, N.V.T.; 3; 4 '. Hallo-uitvoer is hello voorspelde waarde voor elk van de rijen Hallo gebaseerd op Hallo onafhankelijke variabelen. 

> Deze service is gehost op Azure Marketplace Hallo een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden. 
> 
> 

Er zijn meerdere manieren Hallo-service op automatische wijze verbruikt (een voorbeeld-app is [hier](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>C#-code voor het web service starten:
    public class Input
    {
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text };
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

In Azure Machine Learning, een nieuw, leeg experiment is gemaakt en twee [R-Script uitvoeren] [ execute-r-script] modules op Hallo werkruimte zijn opgehaald. Deze webservice wordt een Azure Machine Learning-experiment uitgevoerd met een onderliggende R-script. Er zijn 2-onderdelen toothis experimenteren: schemadefinitie, en training model + score berekenen. de eerste module Hallo Hallo verwacht-structuur van Hallo invoergegevensset, waarbij de eerste variabele Hallo Hallo afhankelijke variabele en resterende Hallo-variabelen zijn onafhankelijk wordt gedefinieerd. Hallo tweede module past een algemene lineair regressiemodel voor Hallo invoergegevens.  

![Experiment stroom][3]

#### <a name="module-1"></a>Module 1:
#### <a name="schema-definition"></a>Schemadefinitie
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a>2-module:
#### <a name="lm-modeling"></a>LM-model
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]]  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- as.data.frame(t(data.split)) 
    data.split <- data.matrix(data.split) 
    data.split <- data.frame(data.split) 
    model <- lm(data.split)  

    out=data.frame(predict(model,data.split))  
    out <- data.frame(t(out))

    maml.mapOutputPort("out");  

## <a name="limitations"></a>Beperkingen
Dit is een zeer eenvoudig voorbeeld van een meerdere lineaire regressie-webservice. Zoals u kunt zien van Hallo voorbeeldcode hierboven, geen fout vastgelegd is geïmplementeerd en Hallo-service wordt ervan uitgegaan dat alles is een continue variabele (geen categorische functies toegestaan), als Hallo service alleen invoer numerieke waarden op Hallo moment Hallo van dit web de service. Bovendien Hallo-service verwerkt momenteel beperkt gegevensgrootte, vanwege toohello aanvragen/reacties aard van de webservice Hallo aanroep en Hallo feit dat Hallo model is wordt geschikt telkens wanneer Hallo-webservice wordt aangeroepen. 

## <a name="faq"></a>Veelgestelde vragen
Zie voor veelgestelde vragen over het verbruik van de webservice Hallo of publishing toohello Azure Marketplace [hier](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

