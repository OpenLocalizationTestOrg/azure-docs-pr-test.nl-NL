---
title: aaaTroubleshoot retraining een klassieke Azure Machine Learning-webservice | Microsoft Docs
description: Identificeren en te corrigeren van algemene problemen tegengekomen wanneer u Hallo model zijn retraining voor een Azure Machine Learning-webservice.
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a>Het oplossen van problemen Hallo retraining van een Azure Machine Learning klassieke webservice
## <a name="retraining-overview"></a>Overzicht retraining
Dit is een statische model wanneer u een Voorspellend experiment als scoreprofiel webservice implementeert. Zodra er nieuwe gegevens beschikbaar of als consument Hallo Hallo API hun eigen gegevens bevat, moet Hallo model toobe retrained. 

Zie voor een volledig overzicht Hallo proces van een klassieke webservice retraining [Retrain Machine Learning-modellen programmatisch](machine-learning-retrain-models-programmatically.md).

## <a name="retraining-process"></a>Proces retraining
Wanneer u tooretrain Hallo-webservice, moet u enkele aanvullende onderdelen toevoegen:

* Een webservice van Hallo Trainingsexperiment geïmplementeerd. Hallo-experiment moet hebben een **Web Service uitvoer** module gekoppeld toohello uitvoer van Hallo **Train Model** module.  
  
    ![Koppel Hallo web service uitvoer toohello train-model.][image1]
* Een nieuw eindpunt toegevoegd tooyour score berekenen voor Web-service.  Kunt u programmatisch Hallo eindpunt toevoegen met behulp van Hallo voorbeeldcode waarnaar wordt verwezen in Hallo Retrain Machine Learning-modellen programmatisch onderwerp of via Hallo klassieke Azure-portal.

Vervolgens kunt u Hallo voorbeeld C#-code uit Hallo Training Web Service API help pagina tooretrain model. Nadat u Hallo resultaten hebt geëvalueerd, en u tevreden met bent, bijwerken Hallo getrainde model score berekenen voor webservice met behulp van nieuwe Hallo-eindpunt dat u hebt toegevoegd.

Met alle Hallo stukken erin zijn Hallo belangrijke stappen die u moet rekening houden met tooretrain Hallo model als volgt uit:

1. Hallo Training webservice aanroepen: Hallo aanroep toohello Batch uitvoering Service (BES) is, niet Hallo aanvragen antwoord Service (RR's). Hallo-voorbeeld C#-code kunt u op Hallo API help pagina toomake Hallo aanroep. 
2. Hallo waarden vinden voor Hallo *BaseLocation*, *RelativeLocation*, en *SasBlobToken*: deze waarden worden geretourneerd in Hallo uitvoer van de aanroep toohello Training Web De service. 
   ![Hallo-uitvoer van Hallo retraining hello en voorbeelden BaseLocation RelativeLocation en SasBlobToken waarden weergegeven.][image6]
3. Update Hallo toegevoegd endpoint van nieuwe score berekenen voor webservice met Hallo Hallo getraind model: Hallo voorbeeldcode met opgegeven in Machine Learning Retrain Hallo modellen programmatisch Hallo nieuwe eindpunt bijgewerkt u toohello score model Hello zojuist toegevoegd getraind model uit Hallo Training Web Service.

## <a name="common-obstacles"></a>Algemene obstakels
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a>Toosee controleren als er Hallo Corrigeer URL PATCH
Hallo PATCH URL die u gebruikt moet Hallo die is gekoppeld aan Hallo nieuwe score-eindpunt u toegevoegd toohello score berekenen voor Web-service. Er zijn een aantal manieren tooobtain Hallo PATCH URL:

**Optie 1: via programmacode**

Hallo tooget corrigeren PATCH URL:

1. Voer Hallo [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) voorbeeldcode.
2. Hallo zoeken van uitvoer Hallo van AddEndpoint *HelpLocation* waarde en kopieer Hallo-URL.
   
   ![HelpLocation in Hallo-uitvoer van Hallo addEndpoint voorbeeld.][image2]
3. Hallo-URL in een browser toonavigate tooa pagina waarmee help-koppelingen Hallo webservice plakken.
4. Klik op Hallo **Update Resource** koppeling tooopen Hallo patch help-pagina.

**Optie 2: Hallo klassieke Azure-portal gebruiken**

1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Open Hallo Machine Learning-tabblad. ![Machine bijvoorbeeld tabblad.][image4]
3. Klik op de naam van uw werkruimte **webservices**.
4. Klik op Hallo score berekenen voor u werkt met de webservice. (Als u niet de standaardnaam Hallo van webservice Hallo wijzigt hebt, wordt het beëindigd in [score berekenen Exp.].)
5. Klik op **eindpunt toevoegen**.
6. Nadat het Hallo-eindpunt wordt toegevoegd, klikt u op Hallo eindpuntnaam. Klik vervolgens op **Update Resource** tooopen Hallo patch help-pagina.

> [!NOTE]
> Als u Hallo eindpunt toohello Training webservice in plaats van Hallo voorspellende webservice hebt toegevoegd, ontvangt u de volgende fout wanneer u klikt op Hallo Hallo **Update Resource** koppeling: Sorry, maar deze functie wordt niet ondersteund of beschikbaar in deze context. Deze webservice heeft geen bronnen worden bijgewerkt. We onze excuses voor het ongemak Hallo en werkt op het verbeteren van deze werkstroom.
> 
> 

![Nieuwe endpoint-dashboard.][image3]

Hallo PATCH help-pagina Hallo moet u de PATCH-URL bevat en wordt een voorbeeldcode kunt u toocall deze.

![URL van de patch.][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a>Controleer dat u de juiste scoreprofiel eindpunt Hallo bijwerkt toosee
* Hallo Training webservice niet doen patch: Hallo patch-bewerking moet worden uitgevoerd op Hallo score berekenen voor Web-service.
* Hallo standaardeindpunt op Web-service niet doen patch: Hallo patch-bewerking moet worden uitgevoerd op Hallo scoren van nieuwe webservice-eindpunt dat u hebt toegevoegd.

U kunt controleren welke Hallo webservice-eindpunt op door bezoekende Hallo klassieke Azure-portal. 

> [!NOTE]
> Zorg ervoor dat u toevoegt Hallo eindpunt toohello voorspellende webservice niet Hallo Training Web Service. Als u correct zowel een trainings- en een Voorspellend webservice hebt geïmplementeerd, ziet u twee verschillende Web-services die worden vermeld. Hallo voorspellende webservice moet eindigen met '[voorspellende exp.]'.
> 
> 

1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Open Hallo Machine Learning-tabblad. ![Machine learning-werkruimte gebruikersinterface.][image4]
3. Selecteer uw werkruimte.
4. Klik op **webservices**.
5. Selecteer uw Predictive webservice.
6. Controleren of uw nieuwe eindpunt toohello Web-service is toegevoegd.

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a>Hallo-werkruimte die uw web-service in het zich in de juiste regio Hallo tooensure controleren
1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Selecteer Machine Learning Hallo-menu.
   ![Machine learning regio gebruikersinterface.][image4]
3. Hallo-locatie van de werkruimte controleren.

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
