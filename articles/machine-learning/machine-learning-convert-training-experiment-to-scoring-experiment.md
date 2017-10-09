---
title: aaaHow tooprepare uw model voor de implementatie in Azure Machine Learning Studio | Microsoft Docs
description: Hoe tooprepare het getrainde model voor de implementatie als een web-service door te converteren experimenteren uw Machine Learning Studio training tooa Voorspellend experiment.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: eb943c45-541a-401d-844a-c3337de82da6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: garye
ms.openlocfilehash: d25bc68be63679a803bfc24a9e29e009a9263f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprepare-your-model-for-deployment-in-azure-machine-learning-studio"></a>Hoe tooprepare uw model voor de implementatie in Azure Machine Learning Studio

Azure Machine Learning Studio biedt u hulpprogramma's moet u een predictive analytics toodevelop Hallo modelleren en vervolgens dit door deze te implementeren als een Azure-web-service te implementeren.

toodo dit u Studio toocreate een experiment - aangeroepen gebruiken een *trainingsexperiment* - waarbij u trainen, beoordelen en bewerken van het model. Als u tevreden bent u uw model klaar toodeploy ophalen door het converteren van uw experiment training tooa *Voorspellend experiment* die gebruikersgegevens tooscore geconfigureerd.

U ziet een voorbeeld van dit proces in [scenario: een predictive analytics-oplossing voor kredietrisicobeoordeling in Azure Machine Learning ontwikkelen](machine-learning-walkthrough-develop-predictive-solution.md).

In dit artikel wordt een diepgaand in Hallo-details van hoe een trainingsexperiment opgehaald geconverteerd worden naar een Voorspellend experiment en hoe die Voorspellend experiment wordt geïmplementeerd. Door de kennis van deze gegevens, leert u hoe tooconfigure uw geïmplementeerde model toomake deze effectiever.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a>Overzicht 

Hallo-proces van het converteren van een Voorspellend experiment voor training experiment tooa omvat drie stappen:

1. Vervang Hallo machine learning-algoritme modules met het getrainde model.
2. Trim Hallo experiment tooonly de modules die nodig zijn voor score berekenen. Een trainingsexperiment omvat een aantal modules die nodig zijn voor training zijn echter niet nodig als Hallo model wordt getraind.
3. Definieer hoe het model van uw gegevens Hallo web servicegebruiker accepteert en welke gegevens worden geretourneerd.

> [!TIP]
> U hebt betrokken zijn bij de trainings- en score berekenen voor het model met behulp van uw eigen gegevens zijn in uw trainingsexperiment. Maar zodra geïmplementeerd, gebruikers stuurt nieuwe tooyour gegevensmodel en voorspelling resultaten wordt geretourneerd. Dus als u uw training experiment tooa Voorspellend experiment tooget deze klaar voor implementatie converteert, houd er rekening mee hoe Hallo model wordt gebruikt door anderen.
> 
> 

## <a name="set-up-web-service-button"></a>Knop Web Service instellen
Nadat u uw experiment uitvoeren (klikt u op **uitvoeren** Hallo onder het experimentcanvas Hallo aan), klikt u op Hallo **webservice ingesteld** knop (Selecteer Hallo **voorspellende webservice** optie). **Web-Service instellen** voor Hallo van drie stappen van het converteren van uw training experiment tooa Voorspellend experiment uitvoert:

1. Het getrainde model worden opgeslagen in Hallo **Trained Models** sectie van het modulepalet hello (toohello links van het experimentcanvas Hallo). Hallo machine learning-algoritme wordt en [Train Model] [ train-model] modules Hello opgeslagen getraind model.
2. Uw experiment wordt geanalyseerd en verwijdert u de modules die zijn duidelijk wordt alleen gebruikt voor training en niet langer nodig zijn.
3. Voegt _Web service invoer_ en _uitvoer_ modules in standaardlocaties in uw experiment (deze modules accepteren en retourneren van gebruikersgegevens).

Bijvoorbeeld: experimenteren Hallo volgende treinen een tweeklasse gestimuleerd besluit-boomstructuur met voorbeeldgegevens telling:

![Trainingsexperiment][figure1]

Hallo-modules in dit experiment uitvoeren in feite vier verschillende functies:

![Module-functies][figure2]

Als u deze training experiment tooa Voorspellend experiment converteert, sommige van deze modules niet langer nodig zijn, of ze nu een ander doel bedienen:

* **Gegevens** -Hallo-gegevens in deze voorbeeldgegevensset niet wordt gebruikt tijdens het berekenen van de score - Hallo gebruiker van de webservice Hallo levert Hallo gegevens toobe berekend. Hallo-metagegevens van deze gegevensset, zoals de gegevenstypen, wordt echter gebruikt door Hallo getrainde model. U moet dus tookeep Hallo gegevensset in Hallo Voorspellend experiment zodat deze metagegevens kan bieden.

* **PREP** - afhankelijk van het Hallo-gebruikersgegevens die worden verzonden voor score berekenen, deze modules kunnen al dan niet nodig tooprocess inkomende hello-gegevens. Hallo **webservice ingesteld** knop deze niet touch - moet u toodecide hoe u wilt dat toohandle ze.
  
    Bijvoorbeeld: in dit voorbeeld Hallo voorbeeldgegevensset wellicht ontbrekende waarden dus een [Clean Missing Data] [ clean-missing-data] module is opgenomen toodeal mee. Hallo voorbeeldgegevensset is tevens kolommen die geen benodigde tootrain Hallo model. Dus een [Select Columns in Dataset] [ select-columns] module is opgenomen tooexclude die extra kolommen van Hallo gegevensstroom. Als u dat Hallo-gegevens die worden verzonden weet voor score berekenen via Hallo-webservice heeft geen ontbrekende waarden en vervolgens kunt u Hallo [Clean Missing Data] [ clean-missing-data] module. Echter, sinds het Hallo [Select Columns in Dataset] [ select-columns] module helpt u bij het definiëren van Hallo kolommen van gegevens die Hallo getrainde model verwacht, die de module moet tooremain.

* **Train** -deze modules gebruikte tootrain Hallo model zijn. Wanneer u klikt op **webservice ingesteld**, deze modules worden vervangen door een enkele module die u getraind Hallo-model bevat. Deze nieuwe module is opgeslagen in Hallo **Trained Models** sectie van het modulepalet Hallo.

* **Score** - In dit voorbeeld Hallo [Split Data] [ split] module gebruikte toodivide Hallo gegevensstroom naar de testgegevens van de en training is. In Hallo Voorspellend experiment, we je niet training voordoet, dus [Split Data] [ split] kunnen worden verwijderd. Op deze manier Hallo tweede [Score Model] [ score-model] module en Hallo [Evaluate Model] [ evaluate-model] module zijn gebruikte toocompare resultaten Hallo-test gegevens, zodat deze modules niet zijn nodig in Hallo voorspellende experimenteren. Hallo resterende [Score Model] [ score-model] -module is echter vereist tooreturn een resultaat score via Hallo-webservice.

Hier wordt de weergave van het voorbeeld na klikken **webservice ingesteld**:

![Geconverteerde Voorspellend experiment][figure3]

werk dat door Hallo **webservice ingesteld** mogelijk voldoende tooprepare uw experiment toobe geïmplementeerd als een webservice. U kunt echter toodo enkele extra werk specifieke tooyour experiment.

### <a name="adjust-input-and-output-modules"></a>Invoer- en uitvoergegevens modules aanpassen
U gebruikt een set trainingsgegevens in uw trainingsexperiment en vervolgens heeft bij sommige tooget verwerking van gegevens in een formulier die machine learning-algoritme nodig Hallo Hallo. Als de verwachte tooreceive via de webservice Hallo Hallo-gegevens wordt niet nodig deze verwerking, kunt u het overslaan: verbinding maken met uitvoer Hallo Hallo **invoer webmodule service** tooa andere module in uw experiment. Hallo gebruikersgegevens worden nu doorgestuurd in Hallo-model op deze locatie.

Bijvoorbeeld standaard **webservice ingesteld** puts Hallo **Web service invoer** module Hallo boven aan de gegevensstroom, zoals wordt weergegeven in de bovenstaande Hallo-afbeelding. Maar we Hallo handmatig kunt plaatsen **Web service invoer** voorbij Hallo gegevensverwerking modules:

![Zwevend Hallo web service invoer][figure4]

Hallo invoergegevens opgegeven Hallo web-service nu rechtstreeks in de module Score Model Hallo zonder eventuele voorverwerking doorlaten wordt.

Op deze manier standaard **webservice ingesteld** puts Hallo service uitvoer webmodule Hallo onder uw gegevensstroom aan. In dit voorbeeld retourneert Hallo webservice toohello gebruiker Hallo uitvoer Hallo [Score Model] [ score-model] module, waaronder Hallo voltooid invoergegevens vector plus Hallo score berekenen voor resultaten.
Echter als u liever tooreturn een ander, klikt u vervolgens kunt u aanvullende modules toevoegen voordat Hallo **Web service uitvoer** module. 

Bijvoorbeeld: tooreturn alleen Hallo resultaten van score berekenen gehele vector niet Hallo van invoergegevens, toevoegen en een [Select Columns in Dataset] [ select-columns] module tooexclude alle kolommen behalve Hallo score berekenen voor resultaten. Verplaats Hallo **Web service uitvoer** module toohello uitvoer van Hallo [Select Columns in Dataset] [ select-columns] module. Hallo-experiment ziet er als volgt:

![Hallo web service uitvoer verplaatsen][figure5]

### <a name="add-or-remove-additional-data-processing-modules"></a>Toevoegen of verwijderen van extra gegevensverwerkende modules
Als er meer modules in uw experiment waarvan u weet dat tijdens het berekenen van de score niet meer nodig, kunnen deze worden verwijderd. Bijvoorbeeld, omdat we Hallo verplaatst **Web service invoer** module tooa wijst nadat hello gegevensverwerking modules kunt verwijderen we Hallo [Clean Missing Data] [ clean-missing-data] module op basis van Hallo Voorspellend experiment.

Onze Voorspellend experiment ziet er nu als volgt uit:

![Extra module verwijderen][figure6]


### <a name="add-optional-web-service-parameters"></a>Toevoegen van optionele Parameters van de Web Service
In sommige gevallen kunt u tooallow Hallo gebruiker van de web service toochange Hallo gedrag van modules wanneer Hallo-service wordt geopend. *Web-Service Parameters* kunt u toodo dit.

Een veelvoorkomend voorbeeld tot stand brengen van een [importgegevens] [ import-data] module zodat de gebruiker Hallo Hallo geïmplementeerd web-service een andere gegevensbron kunt opgeven wanneer Hallo-webservice wordt geopend. Of het configureren van een [gegevens exporteren] [ export-data] module zodat een andere bestemming kan worden opgegeven.

U kunt definiëren Webserviceparameters en koppel deze aan een of meer moduleparameters en kunt u opgeven of ze vereist of optioneel zijn. gebruiker van de webservice Hallo Hallo biedt waarden voor deze parameters wanneer Hallo-service wordt geopend en Hallo module acties zijn gewijzigd.

Voor meer informatie over welke Webserviceparameters zijn en hoe toouse die ze zien [met behulp van Azure Machine Learning Web Service Parameters][webserviceparameters].

[webserviceparameters]: machine-learning-web-service-parameters.md


## <a name="deploy-hello-predictive-experiment-as-a-web-service"></a>Hallo Voorspellend experiment implementeren als een webservice
Nu dat Hallo Voorspellend experiment is voldoende voorbereid, kunt u deze kunt implementeren als een Azure-web-service. Via de webservice hello, kunnen gebruikers tooyour gegevensmodel verzenden en Hallo model retourneert de voorspellingen.

Zie voor meer informatie over de volledige implementatieproces Hallo [Azure Machine Learning-webservice implementeren][deploy]

[deploy]: machine-learning-publish-a-machine-learning-web-service.md


<!-- Images -->
[figure1]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure1.png
[figure2]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure2.png
[figure3]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure3.png
[figure4]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure4.png
[figure5]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure5.png
[figure6]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure6.png


<!-- Module References -->
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[export-data]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/
