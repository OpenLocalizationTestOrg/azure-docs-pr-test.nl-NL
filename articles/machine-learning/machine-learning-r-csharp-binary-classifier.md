---
title: AAA(deprecated) binaire classificatie - Azure | Microsoft Docs
description: (afgeschaft) Binaire classificatie
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 8045038a-9dcf-44b9-a6de-7f1f8e791575
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
ms.openlocfilehash: 0496fcec9952ca243270caf67f55fe191b2dc9f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binary-classifier"></a>(afgeschaft) Binaire classificatie

> [!NOTE]
> Hallo Microsoft DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft. 
> 
> U vindt veel nuttige voorbeeld experimenten en API's in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Zie voor meer informatie over Hallo galerie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

Stel dat u hebt een gegevensset en wilt toopredict een binaire afhankelijke variabele op basis van Hallo onafhankelijke variabelen. 'Logistic Regression' is een populair statistische techniek voor dergelijke voorspellingen. Hier Hallo afhankelijke variabele binary of dichotomous, en p Hallo kans van de aanwezigheid van Hallo-kenmerk van belang. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Een eenvoudig scenario mogelijk waarin een onderzoeker probeert toopredict of een potentiële student waarschijnlijk tooaccept een toelating aanbieding tooa universiteit op basis van gegevens is (GPA in middelbare school, familie inkomsten, residente status gendervraagstukken). Hallo voorspelde uitkomst is de kans op Hallo van Hallo potentiële student Hallo toelating aanbieding accepteren. Dit [webservice](https://datamarket.azure.com/dataset/aml_labs/log_regression) past Hallo logistic regression toohello modelgegevens en uitvoer Hallo waarschijnlijkheidswaarde (y) voor elk Hallo metingen in Hallo-gegevens.  

> Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer. Maar Hallo doel van de webservice Hallo is ook tooserve als een voorbeeld van hoe Azure Machine Learning-webservices gebruikte toocreate boven op R-code kan zijn. Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice. Hallo-webservice vervolgens gepubliceerde toohello Azure Marketplace kan worden en verbruikt door gebruikers en apparaten via Hallo wereld zonder instellingen infrastructuur door de auteur Hallo van Hallo-webservice.  
> 
> 

## <a name="consumption-of-web-service"></a>Gebruik van web-service
Deze web-service biedt Hallo voorspelde waarden van Hallo afhankelijke variabele op basis van onafhankelijke variabelen Hallo voor alle Hallo opmerkingen. Hallo-webservice verwacht Hallo eindgebruiker tooinput gegevens als een tekenreeks waarin rijen worden gescheiden door komma (,) en kolommen worden gescheiden door puntkomma (;). Hallo-webservice 1 rij tegelijk verwacht en Hallo eerste kolom toobe Hallo afhankelijke variabele verwacht. Een voorbeeld van de gegevensset kan er als volgt uitzien:

![Voorbeeldgegevens][1]

Opmerkingen zonder een afhankelijke variabele moeten worden ingevoerd als 'N.V.T.' voor y. Hallo gegevens invoeren voor Hallo hierboven gegevensset zou worden Hallo de volgende tekenreeks: '1; 5; 2,1; 1; 6,0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2; 1, N.V.T.; 3; 4'. Hallo-uitvoer is hello voorspelde waarde voor elk van de rijen Hallo gebaseerd op Hallo onafhankelijke variabelen. 

> Deze service is gehost op Azure Marketplace Hallo een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden. 
> 
> 

Er zijn meerdere manieren Hallo-service op automatische wijze verbruikt (een voorbeeld-app is [hier](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).

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

In Azure Machine Learning, een nieuw, leeg experiment is gemaakt en twee [R-Script uitvoeren] [ execute-r-script] modules opgehaald op Hallo-werkruimte. Deze webservice wordt een Azure Machine Learning-experiment uitgevoerd met een onderliggende R-script. Er zijn 2-onderdelen toothis experimenteren: schemadefinitie, en training model + score berekenen. de eerste module Hallo Hallo verwacht-structuur van Hallo invoergegevensset, waarbij de eerste variabele Hallo Hallo afhankelijke variabele en resterende Hallo-variabelen zijn onafhankelijk wordt gedefinieerd. Hallo tweede module past een algemene logistic regressiemodel voor Hallo invoergegevens.    

![Experiment stroom][2]

#### <a name="module-1"></a>Module 1:
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a>2-module:
    #GLM modeling   
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]] 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- as.data.frame(t(data.split)) data.split <- 
    data.matrix(data.split) 
    data.split <- data.frame(data.split) 

    model <- glm(data.split$V1 ~., family='binomial', data=data.split)  
    out <- data.frame(predict(model,data.split, type="response")) 
    pred1 <- as.data.frame(out) 
    group <- array(1:nrow(pred1)) 
    for (i in 1:nrow(pred1))  
        {
        if(as.numeric(pred1[i,])>0.5) {group[i]=1} 
        else {group[i]=0}
        } 
    pred2 <- as.data.frame(group) 
    maml.mapOutputPort("pred2");  


## <a name="limitations"></a>Beperkingen
Dit is een zeer eenvoudig voorbeeld van een binaire classificatie-webservice. Zoals u kunt zien van Hallo voorbeeldcode hierboven, geen fout vastgelegd is geïmplementeerd en Hallo-service wordt ervan uitgegaan dat alles een binary/continue variabele (geen categorische functies toegestaan), als Hallo service alleen invoer numerieke waarden op Hallo moment Hallo gemaakt van deze Web-service. Bovendien Hallo-service verwerkt momenteel beperkt gegevensgrootte, vanwege toohello aanvragen/reacties aard van de webservice Hallo aanroep en Hallo feit dat Hallo model is wordt geschikt telkens wanneer Hallo-webservice wordt aangeroepen. 

## <a name="faq"></a>Veelgestelde vragen
Zie voor veelgestelde vragen over het verbruik van de webservice Hallo of publishing toohello Azure Marketplace [hier](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

