---
title: aaaWhat is Azure Machine Learning Studio? | Microsoft Docs
description: Overzicht van Azure ML Studio, een hulpprogramma waarmee u met slepen en neerzetten snel modellen kunt ontwikkelen met behulp van een kant-en-klare bibliotheek van algoritmen en modules.
keywords: azure machine learning,azure ml, ml studio
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e65c8fe1-7991-4a2a-86ef-fd80a7a06269
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: a25f2d9e75d088a37930de98240c6e14c9567fa4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-machine-learning-studio"></a>Wat is Azure Machine Learning Studio?
Microsoft Azure Machine Learning Studio is een gezamenlijke, slepen en neerzetten hulpprogramma kunt u toobuild, testen en implementeren van predictive analytics-oplossingen voor uw gegevens. Machine Learning Studio publiceert modellen als webservices die eenvoudig kunnen worden gebruikt door aangepaste apps of BI-hulpprogramma's zoals Excel.

In Machine Learning Studio komen gegevens, wetenschap, predictive analytics, cloudresources en uw gegevens samen.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-machine-learning-studio-interactive-workspace"></a>Hallo interactieve werkruimte van Machine Learning Studio
een predictive Analytics-model toodevelop, doorgaans gebruikt u gegevens uit een of meer bronnen, transformeren en analyseert deze gegevens met verschillende gegevensmanipulatie en statistische functies en een set resultaten genereren. Het ontwikkelen van een model als dit is een iteratief proces. Als u wijzigen Hallo diverse functies en de bijbehorende parameters, de resultaten geconvergeerd tot u tevreden bent dat u een getraind en doeltreffend model hebt.

**Azure Machine Learning Studio** biedt u een interactieve, visuele werkruimte tooeasily bouwen, testen en herhalen een predictive Analytics-model. U slepen en neerzetten ***gegevenssets*** en analyse ***modules*** op een interactieve canvas deze te verbinden samen tooform een ***experimenteren***, die u uitvoert in Machine Learning Studio. tooiterate het modelontwerp Hallo-experiment Sla een kopie indien gewenst, bewerken en voer dit opnieuw. Wanneer u klaar bent, kunt u omzetten uw ***trainingsexperiment*** tooa ***Voorspellend experiment***, en vervolgens publiceren als een ***webservice*** zodat uw model kan worden benaderd door anderen.

Er is niets te programmeren, gegevenssets en modules tooconstruct NET visueel uw predictive Analytics-model te verbinden.

> [!TIP]
> een diagram waarin u een overzicht van Hallo-mogelijkheden van Machine Learning Studio, Zie toodownload en het afdrukken [overzichtsdiagram van de mogelijkheden van Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).
> 
> 

![Azure ML Studio-diagram: experimenten opzetten, gegevens uit verschillende bronnen lezen, beoordeelde gegevens wegschrijven, modellen maken.][ml-studio-overview]

## <a name="get-started-with-machine-learning-studio"></a>Aan de slag met Machine Learning Studio
Wanneer u eerst invoert [Machine Learning Studio](https://studio.azureml.net) ziet u Hallo **Start** pagina. Vanaf deze pagina kunt u documentatie, video's en webinars bekijken en andere waardevolle informatie zoeken.

Klik op Hallo linksboven menu ![Menu](media/machine-learning-what-is-ml-studio/menu.png) om verschillende opties te bekijken.

### <a name="cortana-intelligence"></a>Cortana Intelligence
Klik op **Cortana Intelligence** en u de startpagina toohello Hallo geleid [Cortana Intelligence Suite](https://www.microsoft.com/cloud-platform/cortana-intelligence-suite). Hallo Cortana Intelligence Suite is een volledig beheerde big data en advanced analytics suite tootransform uw gegevens in intelligent actie. Zie Hallo Suite startpagina voor volledige documentatie, met inbegrip van de klantervaring.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Er zijn twee opties hier **Start**, Hallo pagina waar u gestart, en **Studio**.

Klik op **Studio** en u geleid toohello **Azure Machine Learning Studio**. Eerst wordt u gevraagd toosign aan met uw Microsoft-account of de account van uw werk of school. Wanneer u bent aangemeld, ziet u Hallo tabbladen aan de linkerkant hello te volgen:

* **PROJECTS**: verzamelingen van experimenten, gegevenssets, kladblokken en andere resources die één project vertegenwoordigen
* **EXPERIMENTS**: experimenten die u hebt gemaakt en uitgevoerd, of die u hebt opgeslagen als concept
* **WEB SERVICES**: webservices die u hebt geïmplementeerd vanuit uw experimenten
* **NOTEBOOKS**: Jupyter-notitieblokken die u hebt gemaakt
* **DATASETS**: gegevenssets die u naar Studio hebt geüpload
* **TRAINED MODELS**: modellen die u hebt getraind in experimenten en hebt opgeslagen in Studio
* **INSTELLINGEN** -een verzameling instellingen waarmee u tooconfigure uw account en resources kunt.

### <a name="gallery"></a>Gallery
Klik op **galerie** en u geleid toohello  **[Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/)**. Hallo galerie is een locatie waar een community van gegevenswetenschappers en ontwikkelaars oplossingen delen die zijn gemaakt met onderdelen van Hallo Cortana Intelligence Suite.

Zie voor meer informatie over Hallo galerie [Share en oplossingen in Hallo Cortana Intelligence Gallery detecteren](machine-learning-gallery-how-to-use-contribute-publish.md).

## <a name="components-of-an-experiment"></a>Onderdelen van een experiment
Een experiment bestaat uit gegevenssets die gegevens tooanalytical modules, die u met elkaar verbinden bieden tooconstruct een predictive Analytics-model. Een geldig experiment heeft de volgende kenmerken:

* Hallo-experiment heeft ten minste één gegevensset en één module
* Gegevenssets mogelijk verbonden alleen toomodules
* Modules kunnen worden verbonden tooeither gegevenssets of andere modules
* Alle ingangspoorten voor modules sommige gegevens van de toohello verbinding moeten hebben stroom
* Voor elke module moeten alle vereiste parameters zijn ingesteld

U kunt een geheel nieuw experiment maken, maar u kunt ook een bestaand voorbeeldexperiment als sjabloon gebruiken. Zie voor meer informatie [kopiëren voorbeeld experimenten toocreate nieuwe machine learning-experimenten](machine-learning-sample-experiments.md).

Voor een voorbeeld van het maken van een eenvoudig experiment raadpleegt u [Create a simple experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md) (Een eenvoudig experiment maken in Azure Machine Learning Studio).

Voor de volledige procedure voor het maken van een predictive analytics-oplossing raadpleegt u [Develop a predictive solution with Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md) (Een predictive analytics-oplossing maken met Azure Machine Learning).

### <a name="datasets"></a>Gegevenssets
Een gegevensset bestaat uit gegevens die is geüpload tooMachine Learning Studio, zodat deze kan worden gebruikt in Hallo modelleren proces. Een aantal voorbeeldgegevenssets opgenomen in Machine Learning Studio voor tooexperiment met zijn en u kunt meer gegevenssets uploaden als u deze nodig hebt. Hier volgen enkele voorbeelden van opgenomen gegevenssets:

* **MPG-gegevens voor verschillende auto's**: MPG-waarden (mijl per gallon) voor auto's, geïdentificeerd met het aantal cilinders, paardenkracht, enzovoort.
* **Borstkankergegevens**: gegevens voor borstkankerdiagnose.
* **Bosbrandgegevens**: omvang van bosbranden in het noordoosten van Portugal.

Als u een experiment maakt kunt u kiezen uit Hallo lijst met beschikbare gegevenssets toohello links van Hallo canvas.

Zie voor een lijst van voorbeeldgegevenssets die zijn opgenomen in Machine Learning Studio [Hallo sample data sets in Azure Machine Learning Studio gebruiken](machine-learning-use-sample-datasets.md).

### <a name="modules"></a>Modules
Een module is een algoritme dat u met uw gegevens kunt uitvoeren. Machine Learning Studio beschikt over diverse modules, variërend van ingress-functies tootraining, beoordeling en validatie processen voor gegevens. Hier volgen enkele voorbeelden van opgenomen modules:

* [Converteren van tooARFF] [ convert-to-arff] -converteert een .NET geserialiseerde gegevensset tooAttribute-Relation File Format (ARFF).
* [Compute Elementary Statistics][elementary-statistics]: berekent elementaire statistieken, zoals het gemiddelde, de standaardafwijking, enzovoort.
* [Linear Regression][linear-regression]: maakt een online lineair regressiemodel met daalgradiënt.
* [Score Model][score-model]: beoordeelt een getraind classificatie- of regressiemodel.

Als u een experiment maakt kunt u kiezen uit Hallo lijst met beschikbare modules toohello links van Hallo canvas.  

Een module heeft misschien een set parameters waarmee u de interne algoritmen tooconfigure Hallo module kunt. Wanneer u een module op Hallo canvas selecteert, Hallo moduleparameters worden weergegeven in Hallo **eigenschappen** deelvenster toohello rechts van Hallo canvas. U kunt Hallo-parameters in dit deelvenster tootune uw model te wijzigen.

Zie voor hulp bij het navigeren door Hallo grote bibliotheek met machine learning-algoritmen, [hoe toochoose algoritmen voor Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).

## <a name="deploying-a-predictive-analytics-web-service"></a>Een predictive analytics-web service implementeren
Wanneer uw predictive analytics-model klaar is, kunt u het direct vanuit Machine Learning Studio implementeren als webservice. Voor meer informatie over dit proces raadpleegt u [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md) (Een Azure Machine Learning-webservice implementeren).

[ml-studio-overview]:./media/machine-learning-what-is-ml-studio/azure-ml-studio-diagram.jpg

<!-- Module References -->
[convert-to-arff]: https://msdn.microsoft.com/library/azure/62d2cece-d832-4a7a-a0bd-f01f03af0960/
[elementary-statistics]: https://msdn.microsoft.com/library/azure/3086b8d4-c895-45ba-8aa9-34f0c944d4d3/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
