---
title: aaaConsume een Machine Learning-webservice met een web-app-sjabloon | Microsoft Docs
description: Gebruik de sjabloon voor een web-apps in Azure Marketplace tooconsume een Voorspellend webservice in Azure Machine Learning.
keywords: Web-service, uitoefening, REST API, machine learning
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a>Een Azure Machine Learning-webservice gebruiken met een web-app-sjabloon

Eenmaal hebt u uw Voorspellend model ontwikkeld en geïmplementeerd als een Azure-web-service met behulp van Machine Learning Studio of hulpprogramma's zoals R- of Python gebruikt, u toegang tot Hallo geoperationaliseerd model met behulp van een REST-API.

Er zijn een aantal manieren tooconsume Hallo REST-API en toegang Hallo-webservice. Bijvoorbeeld, kunt u een toepassing in C#, R, schrijven of Python Hallo met voorbeeldcode voor u gegenereerd tijdens de implementatie van de webservice Hallo (beschikbaar in Hallo [Machine Learning Web Services-Portal](https://services.azureml.net/quickstart) of in Hallo web servicedashboard in Machine Learning Studio). Of u kunt gebruiken voor u gemaakt op Hallo van Hallo voorbeeld Microsoft Excel-werkmap hetzelfde moment.

Maar de snelste en gemakkelijkste manier tooaccess uw webservice via Hallo Web App sjablonen beschikbaar zijn in Hallo wordt Hallo [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a>Hello Azure Machine Learning Web-App-sjablonen
Hallo web app sjablonen beschikbaar zijn in Azure Marketplace Hallo kunnen maken van een aangepaste web-app dat de invoergegevens van uw webservice en de verwachte resultaten kent. Toodo hoeft u Hallo web app toegang tooyour-webservice en gegevens geven en Hallo sjabloon Hallo rest.

Twee sjablonen zijn beschikbaar:

* [Azure ML-aanvragen en antwoorden Service Web-App-sjabloon](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [Azure ML-Batch uitvoering Web App servicesjabloon](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

Elke sjabloon een voorbeeldtoepassing ASP.NET, met behulp van Hallo API-URI en sleutel van uw web-service maakt en implementeert dit als een tooAzure website. Hallo aanvraag en antwoord-Service (RR's)-sjabloon maakt u een web-app waarmee u toosend één rij met gegevens toohello web service tooget een enkelvoudig resultaat wordt verkregen. Hallo Batch uitvoering Service (BES)-sjabloon maakt u een web-app waarmee u toosend veel rijen met gegevens tooget meerdere resultaten.

Er is geen codering is vereist toouse deze sjablonen. U gewoon Hallo API-sleutel en de URI en toepassing hello Hallo-sjabloon is gebaseerd.

tooget hello API-sleutel en de aanvraag-URI voor een webservice:

1. In Hallo [Web Services-Portal](https://services.azureml.net/quickstart), voor een nieuwe webservice, klikt u op **webservices** Hallo bovenaan. Of voor een klassieke web service Klik **klassieke webservices**.
2. Klik op de gewenste tooaccess Hallo-webservice.
3. Een klassieke-webservice, klikt u op Hallo eindpunt gewenste tooaccess.
4. Klik op **verbruiken** Hallo bovenaan.
5. Kopiëren Hallo **primaire** of **secundaire sleutel** en op te slaan.
6. Als u een aanvraag en antwoord-Service (RR's)-sjabloon maakt, kopieert u Hallo **aanvragen en antwoorden** URI en op te slaan. Als u een Batch uitvoering Service (BES)-sjabloon maakt, kopieert u Hallo **batchaanvragen** URI en op te slaan.


## <a name="how-toouse-hello-request-response-service-rrs-template"></a>Hoe toouse Hallo sjabloon aanvraag en antwoord-Service (RR's)
Volg deze stappen toouse Hallo RRS web-app-sjabloon, zoals wordt weergegeven in het volgende diagram Hallo.

![Processjabloon toouse RRS web][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. Ga toohello [Azure-portal](https://portal.azure.com), **aanmelding**, klikt u op **nieuw**, zoekt en selecteert u **Web-App voor Azure ML aanvragen en antwoorden Service**, klikt u vervolgens op **Maken**. 
   
   * Een unieke naam voor uw web-app geven. Hallo-URL van de web-app Hallo worden deze naam gevolgd door `.azurewebsites.net.` bijvoorbeeld:`http://carprediction.azurewebsites.net.`
   * Selecteer hello Azure-abonnement en services die uw webservice wordt uitgevoerd.
   * Klik op **Create**.
     
     ![Een web-app maken][image5]

4. Wanneer Azure is voltooid Hallo web-app implementeren, klikt u op Hallo **URL** op Hallo van pagina voor de web-app-instellingen in Azure of Hallo-URL opgeven in een webbrowser. Bijvoorbeeld: `http://carprediction.azurewebsites.net.`
5. Wanneer Hallo web app eerste wordt uitgevoerd, u voor Hallo gevraagt wordt **API Post URL** en **API-sleutel**.
   Voer Hallo-waarden die u eerder hebt opgeslagen (**aanvraag-URI** en **API-sleutel**respectievelijk).
     
     Klik op **indienen**.
     
     ![Voer Post URI en API-sleutel][image6]

6. Hallo web app geeft de **Web-App-configuratie** pagina met Hallo huidige web service-instellingen. Hier kunt u wijzigingen aanbrengen toohello-instellingen die door Hallo web-app gebruikt.
   
   > [!NOTE]
   > Hallo instellingen hier alleen wijzigt, worden ze voor deze web-app. Het wijzigen Hallo-standaardinstellingen van uw web-service niet. Bijvoorbeeld, als u Hallo wijzigen **beschrijving** hier het Hallo-beschrijving weergegeven op Hallo web servicedashboard in Machine Learning Studio niet wijzigen.
   > 
   > 
   
    Wanneer u bent klaar, klikt u op **wijzigingen opslaan**, en klik vervolgens op **tooHome pagina gaat**.

7. Startpagina die kunt u waarden van Hallo toosend tooyour-webservice. Klik op **indienen** wanneer u klaar bent en Hallo resultaat geretourneerd.

Als u wilt dat tooreturn toohello **configuratie** pagina, gaat u toohello `setting.aspx` pagina van Hallo web-app. Bijvoorbeeld: `http://carprediction.azurewebsites.net/setting.aspx.` kunt u zich na vragen aan gebruiker tooenter Hallo API-sleutel opnieuw: u hebt nodig dat tooaccess pagina Hallo en Hallo-instellingen worden bijgewerkt.

U kunt stoppen, starten of te verwijderen van Hallo web-app in hello Azure-portal als elke andere web-app. U kunt toohello thuis webadres bladeren en voer nieuwe waarden, zolang deze wordt uitgevoerd.

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a>Hoe toouse Hallo Batch uitvoering Service (BES)-sjabloon
Hallo BES kunt u web-app-sjabloon in Hallo dezelfde manier als Hallo RRS-sjabloon, met uitzondering van die Hallo web-app die gemaakt, kunt u toosubmit meerdere rijen met gegevens en meerdere resultaten krijgt.

Hallo invoerwaarden voor een webservice van de batch-uitvoering kunnen afkomstig zijn van Azure-opslag of een lokaal bestand; Hallo resultaten worden opgeslagen in een Azure storage-container.
Ja, u hebt een Azure storage-container toohold Hallo moet resultaten geretourneerd door Hallo web-app, en moet u tooget uw invoergegevens gereed.

![Verwerken toouse BES websjabloon][image2]

1. Volg dezelfde Hallo procedure toocreate Hallo BES web-app als voor Hallo RRS sjabloon, behalve Ga te[Azure ML Batch uitvoering Web App servicesjabloon](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen Hallo BES sjabloon op Azure Marketplace en klik op **Web-App maken** .

2. toospecify waar u Hallo resultaten die zijn opgeslagen, Geef informatie op Hallo bestemming container op Hallo web-app-startpagina. Ook kunt u opgeven waar vind Hallo web-app Hallo invoerwaarden, in een lokaal bestand of een Azure storage-container.
   Klik op **indienen**.
   
    ![Storage-gegevens][image7]

Hallo-web-app wordt een pagina met de taakstatus weergegeven.
Wanneer het Hallo-taak is voltooid krijgt u Hallo-locatie van Hallo resulteert in een Azure-blobopslag. U hebt ook Hallo optie Hallo resultaten tooa lokale bestand te downloaden.

## <a name="for-more-information"></a>Voor meer informatie
meer informatie over toolearn...

* het maken van een machine learning-experiment met Machine Learning Studio, Zie [uw eerste experiment maken in Azure Machine Learning Studio](machine-learning-create-experiment.md)
* hoe uw machine learning-experiment als een webservice toodeploy zien [een Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md)
* andere manieren tooaccess uw webservice Zie [hoe tooconsume een Azure Machine Learning-webservice](machine-learning-consume-web-services.md)

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
