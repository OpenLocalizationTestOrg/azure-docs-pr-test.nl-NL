---
title: "(afgeschaft) Prognose: Autoregressive geïntegreerd zwevend gemiddelde (ARIMA) - Azure | Microsoft Docs"
description: "(afgeschaft) Prognose - Autoregressive geïntegreerd zwevend gemiddelde (ARIMA)"
services: machine-learning
documentationcenter: 
author: yijichen
manager: jhubbard
editor: cgronlun
ms.assetid: 1e0d525f-8a9e-4b42-87e0-c9423f059f8c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 4f3af41fd8873fdf75c6426fd395351cb41db190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-forecasting---autoregressive-integrated-moving-average-arima"></a>(afgeschaft) Prognose - Autoregressive geïntegreerd zwevend gemiddelde (ARIMA)

> [!NOTE]
> Hallo Microsoft DataMarket wordt buiten gebruik gesteld en deze API is afgeschaft. 
> 
> U vindt veel nuttige voorbeeld experimenten en API's in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Zie voor meer informatie over Hallo galerie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).


Dit [service](https://datamarket.azure.com/dataset/aml_labs/arima) Autoregressive geïntegreerde zwevend gemiddelde (ARIMA) tooproduce voorspellingen op basis van de historische gegevens Hallo opgegeven door de gebruiker Hallo implementeert. Wordt Hallo aanvraag voor een specifiek product verhoging van dit jaar? Kan ik voorspellen mijn product sales voor Hallo Kerstmis seizoen, zodat ik kan mijn voorraad effectief plannen? Prognosemodellen apt tooaddress dergelijke vragen zijn. Hallo gegeven voorbij gegevens, deze modellen verborgen trends en seizoensgebonden toopredict toekomstige trends onderzoeken. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Deze webservice kan bijvoorbeeld worden gebruikt door gebruikers – mogelijk via een mobiele app via een website of zelfs op een lokale computer. Maar Hallo doel van de webservice Hallo is ook tooserve als een voorbeeld van hoe Azure Machine Learning-webservices gebruikte toocreate boven op R-code kan zijn. Met een paar regels code R en klikt op een knop in Azure Machine Learning Studio, worden een experiment gemaakt met R code en gepubliceerd als een webservice. Hallo-webservice vervolgens gepubliceerde toohello Azure Marketplace kan worden en verbruikt door gebruikers en apparaten via Hallo wereld zonder instellingen infrastructuur door de auteur Hallo van Hallo-webservice.
> 
> 

## <a name="consumption-of-web-service"></a>Gebruik van web-service
Deze service accepteert 4 argumenten en Hallo ARIMA prognoses berekent.
Hallo invoerargumenten zijn:

* Frequentie - Hallo frequentie van Hallo onbewerkte gegevens (dagelijks/wekelijks/maandelijks/elk kwartaal/jaarlijks) aangeeft.
* Horizon - toekomstige forecast periode.
* Datum - toevoegen in de nieuwe tijdreeks Hallo gegevens voor tijd.
* Waarde: toevoegen in Hallo nieuwe time series gegevenswaarden.

Hallo-uitvoer van Hallo-service is Hallo berekende voorspelde waarden. 

Voorbeeldinvoer mogelijk: 

* Frequentie - 12
* Horizon - 12
* Datum - 15/1/2012; 15-2/2012 3-15/2012; 15-4-2012; 15-5-2012; 15/6/2012; 15/7/2012; 8 / 15-2012; 15/9/2012; 10/15/2012; 11-15/2012; 15-12/2012; 15/1/2013; 15-2/2013 15-3/2013; 15-4/2013; 15/5/2013; 15/6/2013; 15/7/2013; 8 / 15/2013; 15/9/2013 15/10/2013; 15-11/2013; 15-12/2013; 15-1-2014; 15-2-2014 15-3-2014; 15-4-2014; 15-5-2014; 15-6-2014; 15-7-2014; 8 / 15-2014; 15-9-2014
* Waarde - 3.479; 3,68; 3.832; 3.941; 3.797; 3.586; 3.508; 3.731; 3.915; 3.844; 3.634; 3.549; 3.557; 3.785; 3.782; 3.601; 3.544; 3.556; 3.65; 3.709; 3.682; 3.511; 3.429; 3.51; 3.523; 3.525; 3.626; 3.695; 3.711; 3.711; 3.693; 3.571; 3.509

> Deze service is gehost op Azure Marketplace Hallo een OData-service Deze kunnen worden aangeroepen via POST of GET-methoden. 
> 
> 

Er zijn meerdere manieren Hallo-service op automatische wijze verbruikt (een voorbeeld-app is [hier](http://microsoftazuremachinelearning.azurewebsites.net/ArimaForecasting.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>C#-code voor het web service starten:
    public class Input
    {
        public string frequency;
        public string horizon;
        public string date;
        public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
         byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
         return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }


    void Main()
    {
          var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };
        var json = JsonConvert.SerializeObject(input);
        var acitionUri =  "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";

          var httpClient = new HttpClient();
           httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere","ChangeToAPIKey");
           httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));
          var query = httpClient.PostAsync(acitionUri,new StringContent(json));
          var result = query.Result.Content;
          var scoreResult = result.ReadAsStringAsync().Result;
      }

## <a name="creation-of-web-service"></a>Maken van de webservice
> Deze webservice is gemaakt met behulp van Azure Machine Learning. Voor een gratis proefversie, evenals de inleidende video's over het maken van experimenten en [web publicatieservices](machine-learning-publish-a-machine-learning-web-service.md), Zie [azure.com/ml](http://azure.com/ml). Hieronder staat een screenshot van Hallo experiment die Hallo web service en voorbeeld-code hebt gemaakt voor elk Hallo-modules in Hallo experiment.
> 
> 

In Azure Machine Learning, is een nieuw, leeg experiment gemaakt. Voorbeeldgegevens voor invoer is geüpload met een vooraf gedefinieerde gegevensschema. Gekoppelde toohello gegevensschema is een [R-Script uitvoeren] [ execute-r-script] module waardoor Hallo ARIMA prognosemodel gegenereerd met behulp van 'auto.arima' en 'Prognose' functies van R. 

### <a name="experiment-flow"></a>Stroom experiment:
![Werkruimte maken][2]

#### <a name="module-1"></a>Module 1:
    # Add in hello CSV file with hello data in hello format shown below 
![Werkruimte maken][3]    

#### <a name="module-2"></a>2-module:
    # data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # fit a time-series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- auto.arima(train_ts)
    train_model <- forecast(fit1, h = data$horizon)
    plot(train_model)

    # produce forecasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # data output
    maml.mapOutputPort("data.forecast");


## <a name="limitations"></a>Beperkingen
Dit is een zeer eenvoudige voorbeeld voor het voorspellen van ARIMA. Zoals u kunt zien van Hallo voorbeeldcode hierboven, er is geen fout vastgelegd is geïmplementeerd en Hallo-service wordt ervan uitgegaan dat alle Hallo-variabelen waarden voor continue-positieve zijn en Hallo frequentie een geheel getal groter dan 1 moet. Hallo-lengte van de datum en waarde vectoren Hallo moet dezelfde Hallo. Hallo datum variabele moet toohello indeling 'mm/dd/jjjj' voldoen.

## <a name="faq"></a>Veelgestelde vragen
Zie voor veelgestelde vragen over het verbruik van de webservice Hallo of publishing toomarketplace [hier](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-arima/arima-img1.png
[2]: ./media/machine-learning-r-csharp-arima/arima-img2.png
[3]: ./media/machine-learning-r-csharp-arima/arima-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

