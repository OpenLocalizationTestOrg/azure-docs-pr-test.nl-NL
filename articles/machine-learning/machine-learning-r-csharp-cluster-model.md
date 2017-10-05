---
title: (afgeschaft) Model - Azure-cluster | Microsoft Docs
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
redirect_document_id: TRUE
ms.openlocfilehash: 7cbbbd6d4236dab638eb3051595a584557480841
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-cluster-model"></a>(afgeschaft) Clustermodel

> [!NOTE]
> De Microsoft-DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft. 
> 
> U kunt zoeken veel nuttige voorbeeld experimenten en API's in de [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Zie voor meer informatie over de Gallery [Share en het detecteren van bronnen in de Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).

Hoe kunnen we groepen tegoed kaarthouders gedrag voorspellen om de risico-uitstaand creditcard uitgevers van certificaten te reduceren? Hoe definiëren we groepen van kenmerken karakter van werknemers om te verbeteren de prestaties op het werk? Hoe kunnen arts patiënten classificeren in groepen op basis van de kenmerken van hun ziekten In principe kunnen al deze vragen worden beantwoord door cluster analyse.   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Analyse van de cluster deelt een set van metingen in twee of meer sluiten elkaar wederzijds uit onbekende groepen op basis van combinaties van variabelen. Het doel van de cluster-analyse is voor het detecteren van een systeem van opmerkingen, meestal personen of hun kenmerken te organiseren in groepen, waar leden van de groepen eigenschappen gemeen delen. Dit [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) maakt gebruik van de methodologie K-Means, een veelgebruikte clustering techniek tot willekeurige gegevens van de cluster in groepen. Deze webservice neemt de gegevens en het aantal k clusters als invoer en produceert voorspellingen waarvan de k groepen waartoe elke waarnemingen behoort. 

> Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer. Maar het doel van de webservice is ook als een voorbeeld van hoe Azure Machine Learning-webservices boven op R code maken kan worden gebruikt. Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice. De webservice kan vervolgens worden gepubliceerd naar Azure Marketplace en verbruikt door gebruikers en apparaten over de hele wereld zonder instellingen infrastructuur door de auteur van de webservice.  
> 
> 

## <a name="consumption-of-web-service"></a>Gebruik van web-service
Deze webservice worden de gegevens in een set k groepen gegroepeerd en levert de groepstoewijzing van de voor elke rij. De webservice voor verwacht de eindgebruiker voor het invoeren van gegevens als een tekenreeks waarin rijen worden gescheiden door een komma (,) en kolommen worden gescheiden door puntkomma's (;). De webservice verwacht 1 rij tegelijk. Een voorbeeld van de gegevensset kan er als volgt uitzien:

![Voorbeeldgegevens][1]

Stel dat de gebruiker wil deze gegevens verdelen in groepen van 3 sluiten elkaar wederzijds uit. De invoer voor de bovenstaande gegevensset de volgende zijn gegevens: waarde = '10; 5 2,18; 1; 6,7; 5; 5,22; 3; 4,12; 2; 1,10; 3; 4'; k = "3". De uitvoer is de voorspelde groepslidmaatschap voor elk van de rijen.

> Deze service wordt gehost op Azure Marketplace, een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden. 
> 
> 

Er zijn meerdere manieren van de consumptie van de service op automatische wijze (een voorbeeld-app is [hier](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).

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
> Deze webservice is gemaakt met behulp van Azure Machine Learning. Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml). Hieronder vindt u een schermopname van het experiment dat de web-service en een voorbeeld van code voor elk van de modules in het experiment gemaakt.
> 
> 

In Azure Machine Learning, een nieuw, leeg experiment is gemaakt en twee [R-Script uitvoeren] [ execute-r-script] modules opgehaald naar de werkruimte. Het schema van de is gemaakt met een eenvoudige [R-Script uitvoeren][execute-r-script]. Vervolgens, wordt het schema van de is gekoppeld aan de sectie cluster model, opnieuw worden gemaakt met een [R-Script uitvoeren][execute-r-script]. In de [R-Script uitvoeren] [ execute-r-script] gebruikt voor het clustermodel, de webservice vervolgens maakt gebruik van de functie 'k-means', dat vooraf gedefinieerde in de [R-Script uitvoeren] [ execute-r-script] van Azure Machine Learning.    

![Experiment stroom][3]

#### <a name="module-1"></a>Module 1:
    #Enter the input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a>2-module:
    # Map 1-based optional input ports to variables
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

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a>Beperkingen
Dit is een zeer eenvoudig voorbeeld van een web-clusteringservice. Zoals u kunt zien van de bovenstaande voorbeeldcode, er is geen fout vastgelegd is geïmplementeerd en de service wordt ervan uitgegaan dat alles is een continue variabele (geen categorische functies toegestaan), als de service alleen invoer numerieke waarden op het moment van het maken van deze webservice. Ook de service momenteel worden verwerkt beperkt gegevensgrootte, behoren tot de aard van de aanvraag/antwoord van de aanroep van webservice en het feit dat het model is wordt passen elke keer dat de webservice wordt aangeroepen. 

## <a name="faq"></a>Veelgestelde vragen
Zie voor veelgestelde vragen over het verbruik van de webservice of publiceren naar Azure Marketplace [hier](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

