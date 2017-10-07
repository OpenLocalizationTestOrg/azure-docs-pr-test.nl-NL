---
title: een nieuwe webservice in Azure Machine Learning aaaDeploying | Microsoft Docs
description: Hallo-werkstroom voor het implementeren van een ARM gebaseerde webservice
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
redirect_document_id: True
ms.openlocfilehash: 2cbfda44b97a6b992fbdfdfb0c761e6c9e169035
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-new-web-service"></a>Een nieuwe webservice implementeren
Microsoft Azure Machine learning-nu biedt webservices die zijn gebaseerd op [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) zodat voor nieuwe opties voor facturerings- en implementeren van uw web-service toomultiple regio's.

Hallo algemene werkstroom toodeploy Microsoft Azure Machine Learning-webservices met een webservice is:

* Een Voorspellend experiment maken
* Implementeren
* de naam ervan configureren
* abonnement
* Testen
* Deze wordt gebruikt.

Hallo volgende afbeelding ziet u Hallo-werkstroom.

![Werkstroom voor de implementatie van Web service][1]

## <a name="deploy-web-service-from-studio"></a>Webservice implementeren vanuit Studio
toodeploy een experiment als een nieuwe webservice. Meld u aan bij Hallo Machine Learning Studio en maak een nieuwe voorspellende webservice. 

**Opmerking**: als u een experiment als een klassieke webservice al hebt geïmplementeerd u deze niet implementeren als een nieuwe webservice.

Klik op **uitvoeren** experimenteren canvas Hallo Hallo onderaan in en klik vervolgens op **webservice implementeren** en **Web Service implementeren [New]**. Hallo implementatie pagina van Hallo Machine Learning Web Service manager wordt geopend.

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a>Machine Learning Web Service Manager Experiment pagina implementeren
Voer een naam voor de webservice Hallo op Hallo implementeren Experiment pagina.
Een prijscategorie selecteren. Als u een bestaande prijsstelling dat kunt u dit hebt, moet anders u een nieuw plan prijs voor Hallo-service. 

1. In Hallo **prijs Plan** vervolgkeuzelijst, selecteer een bestaand abonnement of Hallo **Selecteer nieuw plan** optie.
2. In **naam**, typ een naam die wordt geïdentificeerd Hallo plan op uw factuur.
3. Selecteer een van de Hallo **maandelijks plannen lagen**. Houd er rekening mee dat Hallo plan lagen standaard toohello plannen voor uw regio standaard en uw webservice geïmplementeerde toothat regio.

Klik op **implementeren** en Hallo Quick Start-pagina voor uw webservice wordt geopend.

## <a name="quickstart-page"></a>De pagina Quick Start
Hallo pagina Quick Start webservice biedt u toegang en richtlijnen op Hallo van de meest algemene taken die u na het maken van een nieuwe webservice wordt uitgevoerd. Hier kunt u eenvoudig beide Hallo openen **Test** pagina en **verbruiken** pagina.

## <a name="testing-your-web-service"></a>Testen van uw web-service
Klik op Test webservice onder algemene taken Hallo Quick Start-pagina.   

tootest Hallo-webservice als een aanvraag en antwoord-Service (RR's):

* Klik op **Test** op de menubalk Hallo.
* Klik op **aanvragen en antwoorden**.
* Waarden invoeren voor Hallo invoerkolommen van uw experiment.
* Klik op Test **aanvragen en antwoorden**.

U resultaten wordt weergegeven op Hallo de rechterzijde van Hallo pagina.

tootest een webservice Batch uitvoering Service (BES), gebruikt u een CSV-bestand:

* Klik op **Test** op de menubalk Hallo.
* Klik op **Batch**.
* Klik op Bladeren en navigeer tooyour voorbeeldgegevensbestand onder uw invoer.
* Klik op **Test**.

Hallo-status van de test wordt weergegeven onder **batchtaken testen**.

## <a name="consuming-your-web-service"></a>Uw Web-Service gebruiken
Wanneer dit wordt geïmplementeerd als een webservice, bevatten Azure Machine Learning-experimenten een REST-API die kan worden gebruikt door een breed scala aan apparaten en platforms. Dit is omdat Hallo eenvoudige REST-API accepteert en reageert met JSON-indeling berichten. Hello Azure Machine Learning-portal biedt code die kan worden gebruikt toocall Hallo-webservice in R, C# en Python.

U kunt op Hallo verbruik pagina zoeken:

* Hallo API-sleutel en URI's voor het verbruik van de webservice in apps.
* Excel en web-app sjablonen tookick start het proces van uw verbruik.
* Voorbeeldcode in C#, python en R tooget gestart.

Zie voor meer informatie over het gebruiken van webservices [hoe een Azure Machine Learning-webservice tooconsume](machine-learning-consume-web-services.md).

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het gebruiken van web-services:

[Hoe tooconsume een Azure Machine Learning-webservice](machine-learning-consume-web-services.md)

[Azure Machine Learning-webservices: De implementatie en het verbruik](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
