---
title: aaaConnect tooa Machine Learning-webservice | Microsoft Docs
description: Verbinding met C# of Python, tooan Azure Machine Learning Web service met behulp van een autorisatiesleutel.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 59b07bab-b60f-48c4-a385-a162e50ec7c2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: garye
ROBOTS: NOINDEX
redirect_url: machine-learning-consume-web-services
redirect_document_id: True
ms.openlocfilehash: 0108e71e30a05539a8c0ee93d5aadb07e3d1efa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-machine-learning-web-service"></a>Verbinding maken met tooan Azure Machine Learning-webservice
Hallo ontwikkelaarservaring Azure Machine Learning is een voorspellingen Web service API toomake invoergegevens in realtime of in de batchmodus. U gebruikt Azure Machine Learning Studio toocreate voorspellingen en implementeren van een Azure Machine Learning-webservice.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

toolearn over het toocreate en implementeren van een Machine Learning-webservice met behulp van Machine Learning Studio:

* Voor een zelfstudie over hoe toocreate een experiment in Machine Learning Studio, Zie [uw eerste experiment maken](machine-learning-create-experiment.md).
* Voor meer informatie over het toodeploy een webservice, Zie [een Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).
* Bezoek voor meer informatie over Machine Learning in het algemeen Hallo [Machine Learning-documentatiecentrum](https://azure.microsoft.com/documentation/services/machine-learning/).

## <a name="azure-machine-learning-web-service"></a>Azure Machine Learning-webservice
Hello Azure Machine Learning-webservice communiceert een externe toepassing met een Machine Learning werkstroom score-model in realtime. Aanroep van een Machine Learning-webservice retourneert voorspelling resultaten tooan externe toepassing. toomake aanroep van een Machine Learning-webservice, geeft u een API-sleutel die wordt gemaakt bij het implementeren van een voorspelling. Hallo Machine Learning-webservice is gebaseerd op REST, een populaire architectuur keuze voor web programming projecten.

Azure Machine Learning heeft twee soorten services:

* Aanvraag en antwoord-Service (RSS) – een lage latentie en zeer schaalbare service die voorziet in een interface toohello staatloze modellen gemaakt en geïmplementeerd vanuit Hallo Machine Learning Studio.
* Batch uitvoering-Service (BES) – een asynchrone service die scores per batch voor records met gegevens.

Zie voor meer informatie over Machine Learning-webservices [een Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="get-an-azure-machine-learning-authorization-key"></a>Een Azure Machine Learning-autorisatie-sleutel ophalen
Wanneer u uw experiment implementeert, wordt API-sleutels worden gegenereerd voor Hallo-webservice. U kunt Hallo-sleutels ophalen vanaf verschillende locaties.

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a>Vanuit Hallo-portal voor Microsoft Azure Machine Learning-webservices
Meld u aan toohello [Microsoft Azure Machine Learning-webservices](https://services.azureml.net) portal.

tooretrieve hello API-sleutel voor een nieuwe Machine-Learning-webservice:

1. Klik in hello Azure Machine Learning-webservices portal op **webservices** Hallo bovenste menu.
2. Klik op waarvoor u tooretrieve Hallo sleutel wilt Hallo-webservice.
3. Klik op het bovenste menu Hallo **verbruiken**.
4. Kopiëren en opslaan van Hallo **primaire sleutel**.

tooretrieve hello API-sleutel voor een klassieke Machine-Learning-webservice:

1. Klik in hello Azure Machine Learning-webservices portal op **klassieke webservices** Hallo bovenste menu.
2. Klik op Hallo webservice waarmee u werkt.
3. Klik op waarvoor u tooretrieve Hallo sleutel wilt Hallo-eindpunt.
4. Klik op het bovenste menu Hallo **verbruiken**.
5. Kopiëren en opslaan van Hallo **primaire sleutel**.

### <a name="classic-web-service"></a>Klassieke-webservice
 U kunt ook een sleutel voor een klassieke webservice ophalen van Machine Learning Studio of Hallo klassieke Azure-portal.

#### <a name="machine-learning-studio"></a>Machine Learning Studio
1. Klik in Machine Learning Studio **WEBSERVICES** op Hallo links.
2. Klik op een webservice. Hallo **API-sleutel** is op Hallo **DASHBOARD** tabblad.

#### <a name="azure-classic-portal"></a>Klassieke Azure-portal
1. Klik op **MACHINE LEARNING** op Hallo links.
2. Klik op Hallo werkruimte waarin uw Web-service zich bevindt.
3. Klik op **WEBSERVICES**.
4. Klik op een webservice.
5. Klik op een eindpunt. Hallo 'API KEY' loopt Hallo rechtsonder.

## <a id="connect"></a>Verbinding maken met tooa Machine Learning-webservice
U kunt tooa Machine Learning-webservice met behulp van elke programmeertaal die ondersteuning biedt voor HTTP-aanvraag en antwoord verbinden. U kunt de voorbeelden in C#, Python en R weergeven van een help-pagina Machine Learning-webservice.

**Machine Learning API help** Machine Learning API help wordt gemaakt wanneer u een webservice implementeert. Zie [overzicht van Azure Machine Learning - webservice implementeren](machine-learning-walkthrough-5-publish-web-service.md).
Hallo Machine Learning API help bevat details over een voorspelling webservice.

1. Klik op Hallo webservice waarmee u werkt.
2. Klik op Hallo eindpunt waarvoor u wilt dat tooview Hallo API Help-pagina.
3. Klik op het bovenste menu Hallo **verbruiken**.
4. Klik op **API help-pagina** onder Hallo aanvragen en antwoorden of Batchuitvoering eindpunten.

**tooview Machine Learning API help voor een nieuwe webservice**

Hallo in Azure Machine Learning Web Services-Portal:

1. Klik op **WEBSERVICES** in het bovenste menu Hallo.
2. Klik op waarvoor u tooretrieve Hallo sleutel wilt Hallo-webservice.

Klik op **verbruiken** tooget hello URI's voor Hallo aanvraag Reposonse en Batch uitvoering Services en voorbeeld-code in C#, R en Python.

Klik op **Swagger API** tooget Swagger op basis van de documentatie voor Hallo API vanuit Hallo aangeroepen opgegeven URI's.

### <a name="c-sample"></a>C#-voorbeeld
Gebruik tooconnect tooa Machine Learning-webservice, een **HttpClient** ScoreData wordt doorgegeven. ScoreData bevat een FeatureVector, een n-dimensionale vector van numerieke functies die Hallo ScoreData vertegenwoordigt. U verifiëren toohello Machine Learning-service met een API-sleutel.

tooconnect tooa Machine Learning-webservice, Hallo **Microsoft.AspNet.WebApi.Client** NuGet-pakket moet worden geïnstalleerd.

**Microsoft.AspNet.WebApi.Client NuGet in Visual Studio installeren**

1. Hallo downloaden gegevensset van UCI publiceren: volwassenen 2 klasse gegevensset Web Service.
2. Klik op **Hulpprogramma's** > **NuGet Package Manager** > **Package Manager-console**.
3. Kies **Install-pakket Microsoft.AspNet.WebApi.Client**.

**toorun Hallo-codevoorbeeld**

1. Publiceren ' voorbeeld 1: gegevensset downloaden van UCI: volwassene 2 klasse gegevensset ' experiment, deel van Hallo Machine Learning voorbeeld verzameling.
2. Wijs apiKey met Hallo sleutel van een webservice. Zie **ophalen van een Azure Machine Learning-autorisatiesleutel** hierboven.
3. Wijs serviceUri Hello aanvraag-URI.

### <a name="python-sample"></a>Python-voorbeeld
tooconnect tooa Machine Learning-webservice, gebruik Hallo **urllib2** bibliotheek ScoreData wordt doorgegeven. ScoreData bevat een FeatureVector, een n-dimensionale vector van numerieke functies die Hallo ScoreData vertegenwoordigt. U verifiëren toohello Machine Learning-service met een API-sleutel.

**toorun Hallo-codevoorbeeld**

1. Implementeren ' voorbeeld 1: gegevensset downloaden van UCI: volwassene 2 klasse gegevensset ' experiment, deel van Hallo Machine Learning voorbeeld verzameling.
2. Wijs apiKey met Hallo sleutel van een webservice. Zie Hallo **ophalen van een Azure Machine Learning-autorisatiesleutel** sectie bijna Hallo begin van dit artikel.
3. Wijs serviceUri Hello aanvraag-URI.

