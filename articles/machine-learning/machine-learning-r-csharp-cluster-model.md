---
title: AAA(deprecated) clustermodel - Azure | Microsoft Docs
description: (afgeschaft) Clustermodel
services: machine-learning
documentationcenter: 
author: FrancescaLazzeri
manager: jhubbard
editor: cgronlun
ms.assetid: 51b8d012-ed44-4312-920c-9c808dfd4ff6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: lazzeri
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 7b2dffb855a8d91114752b579115e97d07210e45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-cluster-model"></a>(afgeschaft) Clustermodel

> [!NOTE]
> Hallo Microsoft DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft. 
> 
> U vindt veel nuttige voorbeeld experimenten en API's in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Zie voor meer informatie over Hallo galerie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

Hoe kunnen we groepen tegoed kaarthouders gedrag in volgorde tooreduce Hallo-uitstaand risico creditcard verleners voorspellen? Hoe kunnen we groepen definiëren karakter kenmerken van werknemers in volgorde tooimprove hun prestaties op het werk? Hoe kunnen arts patiënten classificeren in groepen op basis van kenmerken van hun ziekten Hallo In principe kunnen al deze vragen worden beantwoord door cluster analyse.   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Analyse van de cluster deelt een set van metingen in twee of meer sluiten elkaar wederzijds uit onbekende groepen op basis van combinaties van variabelen. Hallo-doel van de cluster analyse is toodiscover een systeem van opmerkingen, meestal personen of hun kenmerken te organiseren in groepen, waar leden van groepen Hallo eigenschappen gemeen delen. Dit [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) gebruikt Hallo K-Means methodologie, een techniek voor vaak gebruikte clustering toocluster willekeurige gegevens in groepen. Hallo-gegevens voor deze webservice worden gehaald en Hallo k aantal clusters als invoer en produceert voorspellingen waarvan Hallo k groepen toowhich elke waarnemingen behoort. 

> Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer. Maar Hallo doel van de webservice Hallo is ook tooserve als een voorbeeld van hoe Azure Machine Learning-webservices gebruikte toocreate boven op R-code kan zijn. Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice. Hallo-webservice vervolgens gepubliceerde toohello Azure Marketplace kan worden en verbruikt door gebruikers en apparaten via Hallo wereld zonder instellingen infrastructuur door de auteur Hallo van Hallo-webservice.  
> 
> 

## <a name="consumption-of-web-service"></a>Gebruik van web-service
Deze webservice groepeert Hallo gegevens in een set k groepen en uitvoer Hallo groepstoewijzing voor elke rij. Hallo-webservice verwacht Hallo eindgebruiker tooinput gegevens als een tekenreeks waarin rijen worden gescheiden door een komma (,) en kolommen worden gescheiden door puntkomma's (;). Hallo-webservice verwacht 1 rij tegelijk. Een voorbeeld van de gegevensset kan er als volgt uitzien:

![Voorbeeldgegevens][1]

Stel Hallo gebruiker wilden tooseparate deze gegevens in groepen van 3 sluiten elkaar wederzijds uit. Hallo gegevensinvoer voor Hallo hierboven gegevensset Hallo volgende zijn: waarde = '10; 5 2,18; 1; 6,7; 5; 5,22; 3; 4,12; 2; 1,10; 3; 4'; k = "3". Hallo-uitvoer is voorspelde groepslidmaatschap Hallo voor elk Hallo rijen.

> Deze service is gehost op Azure Marketplace Hallo een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden. 
> 
> 

Er zijn meerdere manieren Hallo-service op automatische wijze verbruikt (een voorbeeld-app is [hier](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>C#-code voor het web service starten:
    public class Input
    {
            public string value;
            public string k;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text, k = TextBox2.Text };
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

In Azure Machine Learning, een nieuw, leeg experiment is gemaakt en twee [R-Script uitvoeren] [ execute-r-script] modules opgehaald op Hallo-werkruimte. Hallo gegevensschema is gemaakt met een eenvoudige [R-Script uitvoeren][execute-r-script]. Vervolgens Hallo gegevensschema gekoppelde toohello is cluster model sectie opnieuw gemaakt met een [R-Script uitvoeren][execute-r-script]. In Hallo [R-Script uitvoeren] [ execute-r-script] gebruikt voor het clustermodel hello, Hallo webservice vervolgens maakt gebruik van 'k-means' Hallo-functie, die vooraf gedefinieerde in Hallo is [R-Script uitvoeren] [ execute-r-script] van Azure Machine Learning.    

![Experiment stroom][3]

#### <a name="module-1"></a>Module 1:
    #Enter hello input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a>2-module:
    # Map 1-based optional input ports toovariables
    mydata <- maml.mapInputPort(1) # class: data.frame

    data.split <- strsplit(mydata[1,1], ",")[[1]]
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- as.data.frame(t(data.split))

    data.split <- data.matrix(data.split)
    data.split <- data.frame(data.split)

    # K-Means cluster analysis
    fit <- kmeans(data.split, mydata$k) # k-cluster solution

    # Get cluster means 
    aggregate(data.split,by=list(fit$cluster),FUN=mean)
    # Append cluster assignment
    mydatafinal <- data.frame(t(fit$cluster))
    n_col=ncol(mydatafinal)
    colnames(mydatafinal) <- paste("V",1:n_col,sep="")

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a>Beperkingen
Dit is een zeer eenvoudig voorbeeld van een web-clusteringservice. Zoals u kunt zien van Hallo voorbeeldcode hierboven, geen fout vastgelegd is geïmplementeerd en Hallo-service wordt ervan uitgegaan dat alles is een continue variabele (geen categorische functies toegestaan), als Hallo service alleen invoer numerieke waarden op Hallo moment Hallo van dit web de service. Bovendien Hallo-service verwerkt momenteel beperkt gegevensgrootte, vanwege toohello aanvragen/reacties aard van de webservice Hallo aanroep en Hallo feit dat Hallo model is wordt geschikt telkens wanneer Hallo-webservice wordt aangeroepen. 

## <a name="faq"></a>Veelgestelde vragen
Zie voor veelgestelde vragen over het verbruik van de webservice Hallo of publishing toohello Azure Marketplace [hier](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

