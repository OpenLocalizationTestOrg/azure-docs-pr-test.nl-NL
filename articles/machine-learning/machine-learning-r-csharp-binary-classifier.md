---
title: (afgeschaft) Binaire classificatie - Azure | Microsoft Docs
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
redirect_document_id: TRUE
ms.openlocfilehash: 1a83392f90bb5a9fb183334c03ccec20dd3f3520
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-binary-classifier"></a>(afgeschaft) Binaire classificatie

> [!NOTE]
> De Microsoft-DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft. 
> 
> U kunt zoeken veel nuttige voorbeeld experimenten en API's in de [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Zie voor meer informatie over de Gallery [Share en het detecteren van bronnen in de Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

Stel dat u hebt een gegevensset en zou willen voorspellen van een binaire afhankelijke variabele op basis van de onafhankelijke variabelen. 'Logistic Regression' is een populair statistische techniek voor dergelijke voorspellingen. Hier de afhankelijke variabele is binary of dichotomous en p is de kans van de aanwezigheid van het kenmerk van belang. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Een eenvoudig scenario mogelijk waarin een onderzoeker probeert te voorspellen of een potentiële student waarschijnlijk een aanbieding toelating om een universiteit op basis van gegevens is (GPA in middelbare school, familie inkomsten, residente status gendervraagstukken) te accepteren. Het verwachte resultaat is de kans van de potentiële student de toelating-aanbieding accepteren. Dit [webservice](https://datamarket.azure.com/dataset/aml_labs/log_regression) past het logistic regressiemodel in de gegevens en de waarschijnlijkheidswaarde (y) voor elk van de metingen in de gegevens levert.  

> Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer. Maar het doel van de webservice is ook als een voorbeeld van hoe Azure Machine Learning-webservices boven op R code maken kan worden gebruikt. Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice. De webservice kan vervolgens worden gepubliceerd naar Azure Marketplace en verbruikt door gebruikers en apparaten over de hele wereld zonder instellingen infrastructuur door de auteur van de webservice.  
> 
> 

## <a name="consumption-of-web-service"></a>Gebruik van web-service
Deze webservice geeft de voorspelde waarden van de afhankelijke variabele op basis van de onafhankelijke variabelen voor alle van de metingen. De webservice voor verwacht de eindgebruiker voor het invoeren van gegevens als een tekenreeks waarin rijen worden gescheiden door komma (,) en kolommen worden gescheiden door puntkomma (;). De webservice 1 rij verwacht op een tijdstip en de eerste kolom van de afhankelijke variabele worden verwacht. Een voorbeeld van de gegevensset kan er als volgt uitzien:

![Voorbeeldgegevens][1]

Opmerkingen zonder een afhankelijke variabele moeten worden ingevoerd als 'N.V.T.' voor y. De gegevens die invoer voor de bovenstaande gegevensset zou de volgende tekenreeks zijn: '1; 5; 2,1; 1; 6,0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2; 1, N.V.T.; 3; 4'. De uitvoer is de voorspelde waarde voor elk van de rijen op basis van de onafhankelijke variabelen. 

> Deze service wordt gehost op Azure Marketplace, een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden. 
> 
> 

Er zijn meerdere manieren van de consumptie van de service op automatische wijze (een voorbeeld-app is [hier](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).

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
> Deze webservice is gemaakt met behulp van Azure Machine Learning. Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml). Hieronder vindt u een schermopname van het experiment dat de web-service en een voorbeeld van code voor elk van de modules in het experiment gemaakt.
> 
> 

In Azure Machine Learning, een nieuw, leeg experiment is gemaakt en twee [R-Script uitvoeren] [ execute-r-script] modules opgehaald naar de werkruimte. Deze webservice wordt een Azure Machine Learning-experiment uitgevoerd met een onderliggende R-script. Er zijn 2-onderdelen voor dit experiment: schemadefinitie, en training model + score berekenen. De eerste module definieert de verwachte structuur van de invoergegevensset, waarbij de eerste variabele de afhankelijke variabele en de resterende variabelen onafhankelijk zijn. De tweede module past een algemene logistic regressiemodel van de invoergegevens.    

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
Dit is een zeer eenvoudig voorbeeld van een binaire classificatie-webservice. Zoals u kunt zien van de bovenstaande voorbeeldcode, er is geen fout vastgelegd is geïmplementeerd en wordt de service wordt ervan uitgegaan dat alles een binary/continue variabele (geen categorische functies toegestaan), als de service alleen invoer numerieke waarden op het moment van het maken van deze webservice . Ook de service momenteel worden verwerkt beperkt gegevensgrootte, behoren tot de aard van de aanvraag/antwoord van de aanroep van webservice en het feit dat het model is wordt passen elke keer dat de webservice wordt aangeroepen. 

## <a name="faq"></a>Veelgestelde vragen
Zie voor veelgestelde vragen over het verbruik van de webservice of publiceren naar Azure Marketplace [hier](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

