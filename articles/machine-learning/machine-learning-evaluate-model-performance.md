---
title: prestaties van de aaaEvaluate model in Machine Learning | Microsoft Docs
description: Legt uit hoe tooevaluate prestaties in Azure Machine Learning model.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 5dc5348a-4488-4536-99eb-ff105be9b160
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bradsev;garye
ms.openlocfilehash: 03477368758dbb13aa6f54c5d27fb215615d1f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooevaluate-model-performance-in-azure-machine-learning"></a>Hoe tooevaluate prestaties in Azure Machine Learning model
In dit artikel laat zien hoe tooevaluate Hallo prestaties van een model in Azure Machine Learning Studio en bevat een korte uitleg van Hallo metrische gegevens beschikbaar voor deze taak. Drie gangbare scenario's met leren met supervisie worden weergegeven: 

* Regressie
* binaire classificatie 
* multiklassen classificatie

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Hallo-prestaties van een model evalueren, is een Hallo core fasen in Hallo gegevens wetenschap proces. Hiermee wordt aangegeven hoe geslaagde Hallo score berekenen (voorspellingen) van een dataset is door een getraind model. 

Azure Machine Learning ondersteunt model evaluatie via twee van de belangrijkste machine learning-modules: [Evaluate Model] [ evaluate-model] en [gekruist te valideren Model][cross-validate-model]. Deze modules kunnen u toosee hoe uw model uitvoert in termen van een aantal metrische gegevens die vaak worden gebruikt in machine learning en statistieken.

## <a name="evaluation-vs-cross-validation"></a>Vs evaluatie. Cross-validatie
Evaluatie en cross validatie zijn standaard manieren toomeasure Hallo prestaties van uw model. Beide evaluatie metrische gegevens die u kunt controleren of vergelijken met die van andere modellen genereren.

[Model evalueren] [ evaluate-model] een scored gegevensset verwacht als invoer (of 2 in geval u graag toocompare Hallo prestaties van 2 verschillende modellen). Dit betekent dat u moet tootrain uw model met Hallo [Train Model] [ train-model] module en maak voorspellingen op bepaalde gegevensset met Hallo [Score Model] [ score-model] -module, voordat u Hallo resultaten kunt evalueren. Hallo evaluatie is gebaseerd op Hallo labels/kansen samen met de Hallo true labels, die allemaal uitgevoerd door Hallo worden berekend [Score Model] [ score-model] module.

U kunt ook cross validatie tooperform een aantal train score evalueren bewerkingen (10 vouwen) automatisch op verschillende subsets van de invoergegevens hello gebruiken. Hallo invoergegevens opgesplitst 10 delen, waarbij één is gereserveerd voor het testen en andere 9 voor training Hallo. Dit proces wordt herhaald 10 keer en het gemiddelde genomen van Hallo evaluatie metrische gegevens. Dit helpt bij het bepalen hoe goed een model toonew gegevenssets zou generalize. Hallo [gekruist te valideren Model] [ cross-validate-model] module duurt in een ongetrainde model en sommige gegevensset en uitgangen Hallo resultaten van evaluatie van elk van de Hallo gelabeld 10 vouwen, Daarnaast toohello gemiddeld resultaten.

In de Hallo uit te voeren, we eenvoudige regressie en classificatie modellen bouwt en evalueren van de prestaties, met behulp van beide Hallo [Evaluate Model] [ evaluate-model] en Hallo [gekruist te valideren Model] [ cross-validate-model] modules.

## <a name="evaluating-a-regression-model"></a>Een regressiemodel evalueren
Stel dat we willen toopredict prijs van een auto met bepaalde functies zoals dimensies, paardenkracht en engine-specificaties. Dit is een probleem typische regressie, waarbij Hallo doelvariabele (*prijs*) is een continue numerieke waarde. We past een eenvoudige lineair regressiemodel dat gegeven Hallo functie waarden van een bepaalde auto kunnen voorspellen Hallo prijs van die auto. Deze regressiemodel kan worden gebruikt tooscore Hallo dezelfde gegevensset we getraind op. Nadat we hebben hello voorspelde prijzen voor alle Hallo auto's, kunnen we Hallo prestaties van Hallo model evalueren door te kijken Hallo voorspellingen hoeveel van de werkelijke prijzen Hallo gemiddeld afwijken. tooillustrate, gebruiken we Hallo *Automobile price data (Raw) gegevensset* beschikbaar in Hallo **gegevenssets opgeslagen** sectie in Azure Machine Learning Studio.

### <a name="creating-hello-experiment"></a>Hallo Experiment maken
Hallo modules tooyour werkruimte in Azure Machine Learning Studio volgende toevoegen:

* Auto price data (Raw)
* [Lineaire regressie][linear-regression]
* [Train Model][train-model]
* [Score-Model][score-model]
* [Model evalueren][evaluate-model]

Verbinding maken met Hallo poorten, zoals hieronder wordt weergegeven in afbeelding 1 en set-kolom Hallo Label Hallo [Train Model] [ train-model] module te*prijs*.

![Een regressiemodel evalueren](media/machine-learning-evaluate-model-performance/1.png)

Afbeelding 1. Evalueren van een regressiemodel.

### <a name="inspecting-hello-evaluation-results"></a>Resultaten van evaluatie van hello te bekijken
Na actieve Hallo-experiment, kunt u klikken op de uitvoerpoort Hallo Hallo [Evaluate Model] [ evaluate-model] module en selecteer *Visualize* toosee Hallo evaluatieresultaten. Hallo evaluatie metrische gegevens beschikbaar voor regressie modellen zijn: *Absolute Error betekenen*, *hoofdmap betekenen Absolute Error*, *Relative Absolute Error*,  *Relative Squared Error*, en Hallo *determinatiecoëfficiënt*.

Hallo term "error" hier vertegenwoordigt Hallo verschil tussen de voorspelde waarde en de waarde true Hallo Hallo. Hallo absolute waarde of vierkante van dit verschil hello, meestal berekende toocapture Hallo totale omvang van de fout in alle exemplaren als Hallo verschil tussen Hallo voorspeld en waarde ' True ' kan niet negatief zijn in sommige gevallen zijn. Hallo fout metrische gegevens meten Hallo voorspellende prestaties van een regressiemodel in termen van Hallo gemiddelde afwijking van de voorspellingen van Hallo waar de waarden. Lagere foutwaarden betekent dat Hallo model nauwkeurigere bij het maken van voorspellingen is. Een algemene fout metriek 0 betekent dat model Hallo past perfect Hallo-gegevens.

Hallo determinatiecoëfficiënt, wat ook wel bekend als R kwadraat, is ook een standaardmanier meten hoe goed Hallo model Hallo gegevens past. Het kan worden geïnterpreteerd als Hallo deel van de variatie worden gedekt door Hallo-model. Een hogere verhouding is beter in dit geval waarbij 1 geeft aan een past.

![Lineaire regressie evaluatie metrische gegevens](media/machine-learning-evaluate-model-performance/2.png)

Afbeelding 2. Lineaire regressie evaluatie metrische gegevens.

### <a name="using-cross-validation"></a>Met behulp van Cross-validatie
Zoals eerder gezegd, kunt u herhaalde training uitvoeren, scores en evaluaties automatisch met Hallo [gekruist te valideren Model] [ cross-validate-model] module. In dit geval hoeft u een gegevensset, een ongetrainde model en een [gekruist te valideren Model] [ cross-validate-model] module (Zie afbeelding hieronder). Opmerking dat u de kolom tooset Hallo-label te moet*prijs* in Hallo [gekruist te valideren Model] [ cross-validate-model] eigenschappen van de module.

![Een regressiemodel cross valideren](media/machine-learning-evaluate-model-performance/3.png)

Afbeelding 3. Cross-valideren van een regressiemodel.

Na actieve Hallo-experiment, kunt u resultaten van evaluatie van Hallo controleren door te klikken op de juiste uitvoerpoort Hallo Hallo [gekruist te valideren Model] [ cross-validate-model] module. Dit biedt een gedetailleerde weergave van Hallo metrische gegevens voor elke herhaling (vouwen) en Hallo gemiddeld resultaten van elke Hallo metrische gegevens (afbeelding 4).

![Kruisvalidatie resultaten van een regressiemodel](media/machine-learning-evaluate-model-performance/4.png)

Afbeelding 4. Kruisvalidatie resultaten van een regressiemodel.

## <a name="evaluating-a-binary-classification-model"></a>Een binaire indeling Model evalueren
In een scenario binaire classificatie is de doelvariabele Hallo slechts twee mogelijke resultaten, bijvoorbeeld: {0, 1} of {false, true}, {negatief, positieve}. Wordt ervan uitgegaan dat u krijgt u een gegevensset volwassenen werknemers met enkele demografische gegevens en arbeid variabelen, en dat u wordt gevraagd toopredict Hallo inkomsten niveau van een binaire variabele met de Hallo waarden {"< = 50K ', ' > 50K '}. Met andere woorden, Hallo negatieve klasse vertegenwoordigt Hallo werknemers die kleiner dan of gelijk too50K per jaar en Hallo positief klasse vertegenwoordigt alle andere werknemers. Zoals in Hallo regressie scenario zou we een model te trainen, score sommige gegevens en Hallo resultaten evalueren. Hallo belangrijkste verschil is hier is de keuze Hallo van metrische gegevens die Azure Machine Learning wordt berekend en uitvoer. tooillustrate hello inkomsten niveau voorspelling scenario gebruiken we Hallo [volwassenen](http://archive.ics.uci.edu/ml/datasets/Adult) gegevensset toocreate een Azure Machine Learning experimenteren en prestaties van een tweeklasse logistic regressiemodel, een veelgebruikte binair Hallo evalueren classificatie.

### <a name="creating-hello-experiment"></a>Hallo Experiment maken
Hallo modules tooyour werkruimte in Azure Machine Learning Studio volgende toevoegen:

* Volwassenen inventarisering Income binaire classificatie gegevensset
* [Two-Class Logistic Regression][two-class-logistic-regression]
* [Train Model][train-model]
* [Score-Model][score-model]
* [Model evalueren][evaluate-model]

Verbinding maken met Hallo poorten, zoals hieronder wordt weergegeven in afbeelding 5 en set-kolom Hallo Label Hallo [Train Model] [ train-model] module te*inkomsten*.

![Een binaire indeling Model evalueren](media/machine-learning-evaluate-model-performance/5.png)

Afbeelding 5. Een binaire indeling Model evalueren.

### <a name="inspecting-hello-evaluation-results"></a>Resultaten van evaluatie van hello te bekijken
Na actieve Hallo-experiment, kunt u klikken op de uitvoerpoort Hallo Hallo [Evaluate Model] [ evaluate-model] module en selecteer *Visualize* toosee Hallo evaluatieresultaten (afbeelding 7). Hallo evaluatie metrische gegevens beschikbaar voor binaire classificatie modellen zijn: *nauwkeurigheid*, *precisie*, *intrekken*, *F1 Score*, en *AUC*. Bovendien Hallo module levert een verwarring matrix Hallo aantal positieven true, false negatieve valse positieven en waar negatieve wordt weergegeven, evenals *ROC*, *precisie/intrekken*, en *Til* curven.

Nauwkeurigheid is gewoon Hallo deel van een correct ingedeeld exemplaren. Meestal is dit de eerste metriek Hallo die u kijken bij het evalueren van een classificatie. Wanneer de testgegevens Hallo is echter in onbalans gebracht (waarvan de meeste Hallo exemplaren tooone Hallo klassen behoort) of als u meer geïnteresseerd in Hallo prestaties op een van de klassen hello, nauwkeurigheid echt Hallo effectiviteit van een classificatie niet vastleggen. In Hallo inkomsten niveau classificatie scenario wordt ervan uitgegaan u test op bepaalde gegevens waar 99% Hallo exemplaren van mensen die kleiner dan of gelijk verdienen vertegenwoordigen too50K per jaar. Mogelijke tooachieve een 0.99 nauwkeurigheid is door het voorspellen van de klasse hello "< = 50K ' voor alle exemplaren. Hallo classificatie in dat geval toobe goed bezig algehele weergegeven, maar in werkelijkheid is het mislukt tooclassify van Hallo hoog inkomen personen (Hallo 1%) correct.

Daarom is handig toocompute aanvullende gegevens die meer specifieke aspecten van de evaluatie van Hallo vastlegt. Voordat u doorgaat naar Hallo details van deze metrische gegevens, is het belangrijk toounderstand Hallo verwarring matrix van de evaluatie van een binaire indeling. Hallo-klasse labels in de trainingset Hallo kunnen uitvoeren op slechts 2 mogelijke waarden die we meestal verwijzen tooas positief of negatief. Hallo positieve en negatieve instanties die een classificatie correct voorspelt worden genoemd waar positieven (TP) en waar negatieve (TN), respectievelijk. Hallo onjuist ingedeeld exemplaren worden op dezelfde manier valse positieven (EP) en fout-negatieve resultaten (FN) genoemd. Hallo verwarring matrix is gewoon een tabel met Hallo-nummer van exemplaren die bij elk van deze 4 categorieën vallen. Azure Machine Learning besluit automatisch welke van twee klassen in de gegevensset Hallo HALLO hallo positief klasse is. Als Hallo klasse labels Boolean of gehele getallen zijn zijn, en vervolgens Hallo 'true' of '1' gelabelde exemplaren Hallo positief klasse toegewezen. Hallo labels zijn tekenreeksen, net als bij Hallo Hallo inkomsten gegevensset, Hallo labels alfabetische volgorde worden gesorteerd als eerste niveau Hallo toobe Hallo negatieve klasse is gekozen, terwijl het tweede niveau Hallo Hallo positief klasse.

![Binaire classificatie verwarring Matrix](media/machine-learning-evaluate-model-performance/6a.png)

Afbeelding 6. Binaire classificatie verwarring Matrix.

Als u terugkeert toohello inkomsten klassificatieprobleem, zou willen we tooask verschillende evaluatievragen die ons te helpen Hallo prestaties van Hallo classificatie die wordt gebruikt begrijpen. Een logisch vraag is: ' buiten het Hallo-personen wie Hallo model voorspelde toobe verdienen > 50 K (TP + FrontPage), hoeveel zijn correct geclassificeerd (TP)?' Kan deze vraag worden beantwoord door te kijken Hallo **precisie** van Hallo-model is Hallo aandeel van positieven die correct zijn geclassificeerd: TP/(TP+FP). Vraag is ' buiten alle Hallo hoge renteproducerende werknemers met inkomsten > 50 k (TP + FN), hoeveel Hallo classificatie classificeren correct (TP) '. Dit is daadwerkelijk Hallo **intrekken**, of waar positief tarief Hallo: TP/(TP+FN) van Hallo classificatie. Er is een duidelijke compromis tussen precision en intrekken, zult u merken. Bijvoorbeeld, een relatief taakverdeling gegevensset wordt opgegeven, heeft een classificatie die voornamelijk positief exemplaren voorspelt een hoge intrekken, maar een relatief laag precisie zo veel mogelijk negatieve exemplaren Hallo zou worden verkeerd geclassificeerd wat resulteert in een groot aantal fout-positieven. toosee tekent van hoe deze twee metrische gegevens variëren, kunt u klikken op Hallo precisie/INTREKKEN curve Hallo evaluatie resultaat uitvoer pagina (boven links deel uit van de afbeelding 7).

![Resultaten van evaluatie van binaire classificatie](media/machine-learning-evaluate-model-performance/7.png)

Afbeelding 7. Resultaten van evaluatie van binaire classificatie.

Een andere gerelateerde metriek die vaak wordt gebruikt is Hallo **F1 Score**, wat zowel precision en terughalen in aanmerking duurt. Het is Hallo harmonische gemiddelde van deze 2 metrische gegevens en als zodanig wordt berekend: F1 = 2 (precisie x intrekken) / (precisie + intrekken). Hallo F1 score is een uitstekende manier toosummarize Hallo evaluatie van een enkel getal, maar het is altijd een goede gewoonte toolook op zowel precision en terughalen samen toobetter begrijpen hoe een classificatie zich gedraagt.

Bovendien een Hallo true positief snelheid versus Hallo false positief frequentie in Hallo kunt inspecteren **ontvanger besturingssysteem kenmerk (ROC)** curve met Hallo overeenkomt **gebied onder Hallo Curve (AUC)** waarde. Hallo dichter bij deze curve is toohello bovenste linkerbovenhoek, Hallo betere Hallo classificatie van prestaties (dat wil maximaliseren Hallo true positief tarief terwijl het minimaliseert Hallo false positief snelheid). Curven die sluiten toohello diagonaal van Hallo tekent, resultaat van de classificaties die toomake voorspellingen die doorgaans sluiten toorandom raden.

### <a name="using-cross-validation"></a>Met behulp van Cross-validatie
Zoals in Hallo regressie voorbeeld, kunt we cross validatie toorepeatedly train uitvoeren, beoordelen en evalueren verschillende subsets van Hallo gegevens automatisch. Op deze manier kunnen we hello gebruiken [gekruist te valideren Model] [ cross-validate-model] module, een ongetrainde logistic regressiemodel en een dataset. de kolom label Hello te moet worden ingesteld*inkomsten* in Hallo [Model gekruist te valideren] [ cross-validate-model] eigenschappen van de module. Nadat de uitvoerpoort Hallo Hallo experiment uitvoeren en te klikken op de juiste Hallo [gekruist te valideren Model] [ cross-validate-model] -module, ziet u Hallo binaire classificatie metriek waarden voor elke vouwen bovendien toohello gemiddelde en de standaarddeviatie van elke. 

![Een binaire indeling Model cross valideren](media/machine-learning-evaluate-model-performance/8.png)

Afbeelding 8. Een binaire indeling Model cross valideren.

![Kruisvalidatie resultaten van een binaire classificatie](media/machine-learning-evaluate-model-performance/9.png)

Afbeelding 9. Kruisvalidatie resultaten van een binaire classificatie.

## <a name="evaluating-a-multiclass-classification-model"></a>Evaluatie van een Model Multiklassen classificatie
In dit experiment gebruiken we populaire Hallo [Iris](http://archive.ics.uci.edu/ml/datasets/Iris "Iris") dataset die exemplaren van 3 soorten (klassen) Hallo iris plant bevat. Er zijn 4 functie waarden (sepal lengte/breedte en lengte Bloemblad/breedte) voor elk exemplaar. In de vorige experimenten Hallo we getraind en geteste Hallo modellen met Hallo dezelfde gegevenssets. Hier gebruiken we Hallo [Split Data] [ split] module toocreate 2 subsets van Hallo gegevens eerst op Hallo trainen en beoordelen en evalueren op Hallo tweede. Hallo Iris gegevensset openbaar beschikbaar is op Hallo [UCI Machine Learning-opslagplaats](http://archive.ics.uci.edu/ml/index.html), en kan worden gedownload met behulp van een [importgegevens] [ import-data] module.

### <a name="creating-hello-experiment"></a>Hallo Experiment maken
Hallo modules tooyour werkruimte in Azure Machine Learning Studio volgende toevoegen:

* [Gegevens importeren][import-data]
* [Multiklasse besluit Forest][multiclass-decision-forest]
* [Gegevens splitsen][split]
* [Train Model][train-model]
* [Score-Model][score-model]
* [Model evalueren][evaluate-model]

Verbinding maken met poorten Hallo zoals hieronder wordt weergegeven in afbeelding 10.

Hallo Label kolomindex Hallo ingesteld [Train Model] [ train-model] module too5. Hallo dataset bevat geen veldnamenrij, maar we weten dat labels in Hallo vijfde kolom zijn Hallo-klasse.

Klik op Hallo [gegevens importeren] [ import-data] module en set Hallo *gegevensbron* eigenschap te*via HTTP-URL voor webinhoud*, en Hallo *URL*  toohttp://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data.

Set Hallo fractie van de exemplaren toobe gebruikt voor training in Hallo [Split Data] [ split] module (0,7 bijvoorbeeld).

![Evaluatie van een Multiklassen classificatie](media/machine-learning-evaluate-model-performance/10.png)

Afbeelding 10. Evaluatie van een Multiklassen classificatie

### <a name="inspecting-hello-evaluation-results"></a>Resultaten van evaluatie van hello te bekijken
Hallo-experiment uitvoeren en klik op de uitvoerpoort Hallo van [Evaluate Model][evaluate-model]. resultaten van evaluatie van Hallo worden in dit geval op Hallo vorm van een matrix verwarring weergegeven. Hallo-matrix bevat Hallo werkelijk vs. voorspelde exemplaren voor alle 3 klassen.

![Resultaten van evaluatie van multiklassen classificatie](media/machine-learning-evaluate-model-performance/11.png)

Afbeelding 11. Resultaten van evaluatie van multiklassen classificatie.

### <a name="using-cross-validation"></a>Met behulp van Cross-validatie
Zoals eerder gezegd, kunt u herhaalde training uitvoeren, scores en evaluaties automatisch met Hallo [gekruist te valideren Model] [ cross-validate-model] module. U moet een gegevensset, een ongetrainde model en een [gekruist te valideren Model] [ cross-validate-model] module (Zie afbeelding hieronder). Opnieuw moet u tooset Hallo labelkolom Hallo [gekruist te valideren Model] [ cross-validate-model] module (kolomindex 5 in dit geval). Nadat de uitvoerpoort Hallo Hallo experiment uitgevoerd en te klikken op Hallo rechts [gekruist te valideren Model][cross-validate-model], controleert u Hallo metrische waarden voor elk worden gesloten als Hallo gemiddelde en standaarddeviatie. Hallo metrische gegevens hier weergegeven zijn Hallo vergelijkbare toohello die zijn besproken in geval van Hallo binaire classificatie. Bedenk wel dat in multiklassen classificatie computing Hallo true positieven/negatieve en fout-positieven/negatieve resultaten wordt gerealiseerd door tellen op basis van per-klasse als er geen klasse algemene positief of negatief is. Bijvoorbeeld, wanneer computing Hallo precisie of intrekken van de klasse 'Iris setosa' hello, wordt ervan uitgegaan dat dit Hallo positief klasse en alle andere negatief is.

![Een Model Multiklassen classificatie cross valideren](media/machine-learning-evaluate-model-performance/12.png)

Afbeelding 12. Een Model Multiklassen classificatie cross valideren.

![Kruisvalidatieresultaten van een Model Multiklassen classificatie](media/machine-learning-evaluate-model-performance/13.png)

Afbeelding 13. De Kruisvalidatieresultaten van een Model Multiklassen classificatie.

<!-- Module References -->
[cross-validate-model]: https://msdn.microsoft.com/library/azure/75fb875d-6b86-4d46-8bcc-74261ade5826/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[multiclass-decision-forest]: https://msdn.microsoft.com/library/azure/5e70108d-2e44-45d9-86e8-94f37c68fe86/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-logistic-regression]: https://msdn.microsoft.com/library/azure/b0fd7660-eeed-43c5-9487-20d9cc79ed5d/

