---
title: Een nieuwe webservice in Azure Machine Learning implementeren | Microsoft Docs
description: De werkstroom voor het implementeren van een ARM gebaseerde webservice
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: a358b04f-0d08-4d50-820e-eeac971854cf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: v-donglo
ROBOTS: NOINDEX
redirect_url: machine-learning-publish-a-machine-learning-web-service
redirect_document_id: TRUE
ms.openlocfilehash: 1415709f9da2bb2cce859af9feb0ec15c1fa5801
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-new-web-service"></a>Een nieuwe webservice implementeren
Microsoft Azure Machine learning-nu biedt webservices die zijn gebaseerd op [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) waardoor het nieuwe plan opties facturering en uw webservice implementeren in meerdere regio's.

De algemene werkstroom voor het implementeren van een webservice met behulp van Microsoft Azure Machine Learning-webservices is:

* Een Voorspellend experiment maken
* Implementeren
* de naam ervan configureren
* abonnement
* Testen
* Deze wordt gebruikt.

De volgende afbeelding ziet u de werkstroom.

![Werkstroom voor de implementatie van Web service][1]

## <a name="deploy-web-service-from-studio"></a>Webservice implementeren vanuit Studio
Voor het implementeren van een experiment als een nieuwe webservice. Meld u aan bij de Machine Learning Studio en maak een nieuwe voorspellende webservice. 

**Opmerking**: als u een experiment als een klassieke webservice al hebt geïmplementeerd u deze niet implementeren als een nieuwe webservice.

Klik op **uitvoeren** aan de onderkant van het experiment canvas en klik vervolgens op **webservice implementeren** en **Web Service implementeren [New]**. De pagina implementatie van de Machine Learning Web Service manager wordt geopend.

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a>Machine Learning Web Service Manager Experiment pagina implementeren
Voer een naam voor de web-service op de pagina Experiment implementeren.
Een prijscategorie selecteren. Als u een bestaande prijsstelling dat kunt u dit hebt, moet anders u een nieuw plan prijs voor de service. 

1. In de **prijs Plan** vervolgkeuzelijst, selecteer een bestaande planning of Selecteer de **Selecteer nieuw plan** optie.
2. In **naam**, typ een naam waarmee het plan op uw factuur wordt geïdentificeerd.
3. Selecteer een van de **maandelijks plannen lagen**. Houd er rekening mee dat de standaardwaarde van de lagen abonnement op de plannen voor uw regio standaard en uw web-service wordt geïmplementeerd naar deze regio.

Klik op **implementeren** en de pagina Quick Start voor uw webservice wordt geopend.

## <a name="quickstart-page"></a>De pagina Quick Start
De pagina Quick Start webservice biedt u toegang en richtlijnen op de meest algemene taken die u uitvoeren wilt na het maken van een nieuwe webservice. Vanaf hier u kunt eenvoudig toegang tot zowel de **Test** pagina en **verbruiken** pagina.

## <a name="testing-your-web-service"></a>Testen van uw web-service
Klik op Test webservice onder algemene taken van de pagina Quick Start.   

Als een aanvraag en antwoord-Service (RR's) voor de webservice testen:

* Klik op **Test** op de menubalk.
* Klik op **aanvragen en antwoorden**.
* Voer de juiste waarden voor de invoerkolommen van uw experiment.
* Klik op Test **aanvragen en antwoorden**.

U resultaten wilt weergeven aan de rechterkant van de pagina.

Als u wilt een webservice Batch uitvoering Service (BES) testen, gebruikt u een CSV-bestand:

* Klik op **Test** op de menubalk.
* Klik op **Batch**.
* Klik op Bladeren en navigeer naar uw voorbeeldgegevensbestand onder uw invoer.
* Klik op **Test**.

De status van de test wordt weergegeven onder **batchtaken testen**.

## <a name="consuming-your-web-service"></a>Uw Web-Service gebruiken
Wanneer dit wordt geïmplementeerd als een webservice, bevatten Azure Machine Learning-experimenten een REST-API die kan worden gebruikt door een breed scala aan apparaten en platforms. Dit komt doordat eenvoudige REST-API accepteert en reageert met JSON-indeling berichten. De Azure Machine Learning-portal biedt code die kan worden gebruikt voor het aanroepen van de webservice in R, C# en Python.

U kunt op de pagina verbruik vinden:

* De API-sleutel en de URI's voor het verbruik van de webservice in apps.
* Excel en web-app sjablonen Activeer starten uw verbruik-proces.
* De voorbeeldcode in C#, python en R u op weg.

Zie voor meer informatie over het gebruiken van webservices [gebruiken van een Azure Machine Learning-webservice](machine-learning-consume-web-services.md).

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het gebruiken van web-services:

[Een Azure Machine Learning-webservice gebruiken](machine-learning-consume-web-services.md)

[Azure Machine Learning-webservices: De implementatie en het verbruik](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
