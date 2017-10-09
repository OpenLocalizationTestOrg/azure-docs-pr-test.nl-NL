---
title: aaaMachine learning algorithm cheat sheet | Microsoft Docs
description: Een afdrukbaar machine learning-algoritme-referentieoverzicht helpt u rechts Hallo-algoritme voor het voorspellende model kiezen in Azure Machine Learning Studio.
keywords: algoritme referentieoverzicht, referentieoverzicht, machine learning-algoritme
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e1dc31ec-1acb-463f-ba77-de565d4ddf4d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: garye
ms.openlocfilehash: 2bedd77bfc65128a90c6128743016415dd8609d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-algorithm-cheat-sheet-for-microsoft-azure-machine-learning-studio"></a>Overzichtskaart voor Machine Learning-algoritme voor Microsoft Azure Machine Learning Studio
Hallo **Microsoft Azure Machine Learning-algoritme cheats blad** helpt u de juiste algoritme Hallo voor een predictive analytics-model kiezen.

[Azure Machine Learning Studio](https://studio.azureml.net/) heeft een grote bibliotheek met algoritmen uit Hallo ***regressie***, ***classificatie***, ***clustering***, en ***afwijkingsdetectie*** families. Elk is ontworpen tooaddress een ander type van machine learning-probleem.

## <a name="download-machine-learning-algorithm-cheat-sheet"></a>Download: Machine learning-algoritme-referentieoverzicht
**Hallo-referentieoverzicht hier downloaden: [Machine Learning-algoritme cheats blad (11 x 17.)](http://download.microsoft.com/download/A/6/1/A613E11E-8F9C-424A-B99D-65344785C288/microsoft-machine-learning-algorithm-cheat-sheet-v6.pdf)**

![Machine Learning-algoritme-referentieoverzicht: meer informatie over hoe toochoose een Machine Learning-algoritme.][cheat-sheet]

[cheat-sheet]: ./media/machine-learning-algorithm-cheat-sheet/machine-learning-algorithm-cheat-sheet-small_v_0_6-01.png

Downloaden en deze kunt raadplegen en get-help kiezen van een algoritme Hallo Machine Learning-algoritme cheats blad in a3 grootte tookeep afdrukken.

> [!NOTE]
> Zie het artikel Hallo [hoe toochoose algoritmen voor Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) voor een gedetailleerde uitleg van toousing deze referentieoverzicht.
> 
> 

## <a name="more-help-with-algorithms"></a>Meer hulp bij algoritmen
* Zie voor informatie over het gebruik van deze referentieoverzicht voor het kiezen van de juiste algoritme hello, plus een meer gedetailleerde bespreking van de verschillende typen Hallo van machine learning-algoritmen en hoe deze worden gebruikt, [hoe toochoose algoritmen voor Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).
* Zie voor een downloadbare infographic die beschrijving algoritmen en voorbeelden, [downloadbare Infographic: Machine learning-algoritme voorbeelden voor alledaagse](machine-learning-basics-infographic-with-algorithm-examples.md).
* Zie voor een lijst door de categorie van alle Hallo machine learning-algoritmen in Machine Learning Studio [Model initialiseren] [ initialize-model] in de Help van de Module en Hallo Machine Learning Studio algoritme.
* Zie voor een volledige alfabetische lijst van algoritmen en modules in Machine Learning Studio [lijst A-Z van Machine Learning Studio-modules] [ a-z-list] in de Help van de Module en Machine Learning Studio-algoritme.
* een diagram waarin u een overzicht van Hallo-mogelijkheden van Machine Learning Studio, Zie toodownload en het afdrukken [overzichtsdiagram van de mogelijkheden van Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="notes-and-terminology-definitions-for-hello-machine-learning-algorithm-cheat-sheet"></a>Opmerkingen en termen die voor Hallo machine learning-algoritme cheats blad

* Hallo suggesties aangeboden in dit algoritme-referentieoverzicht zijn bij benadering regels van de miniatuur. Sommige kunnen worden verbogen en sommige flagrantly kunnen worden geschonden. Dit is bedoeld toosuggest een beginpunt. Wees niet bang toorun een man concurrentie tussen verschillende algoritmen voor uw gegevens. Er is gewoon geen vervanging voor de beginselen van elk algoritme Hallo kennis en inzicht Hallo system dat uw gegevens gegenereerd.

* Elke machine learning-algoritme heeft een eigen stijl of *inductieve afwijking*. Voor een specifiek probleem verschillende algoritmen is wellicht beter en één algoritme is mogelijk beter geschikt dan andere. Maar het is niet altijd mogelijk tooknow tevoren die Hallo zodat deze optimaal passen. In dergelijke gevallen worden verschillende algoritmen samen weergegeven in Hallo-referentieoverzicht. Een passende strategie zou worden tootry één algoritme en als Hallo resultaten nog niet voldoende zijn, probeert u het Hallo anderen. Hier volgt een voorbeeld van Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/) Hallo resultaten van een experiment die verschillende algoritmen tegen Hallo probeert dezelfde gegevens en vergelijkt: [vergelijken met meerdere klasse classificaties: erkenning Letter ](http://gallery.cortanaintelligence.com/Details/a635502fc98b402a890efe21cec65b92).

* Er zijn drie hoofdcategorieën van machine learning: **onder supervisie learning**, **leren zonder supervisie**, en **versterking learning**.

  * In **onder supervisie learning**, elk gegevenspunt is met het label of die zijn gekoppeld aan een categorie of de waarde van belang.  Een voorbeeld van een categorische label met het toewijzen van een afbeelding als een 'cat' of een 'aquaduct'.  Een voorbeeld van een Waardelabel is Hallo verkoopprijs die zijn gekoppeld aan een gebruikte auto. Hallo doel van leren met supervisie is toostudy veel gelabeld voorbeelden zoals deze, en toobe kunnen toomake voorspellingen over toekomstige gegevenspunten. Bijvoorbeeld, identificeren nieuwe foto's Hello juist dieren of het toewijzen van nauwkeurige verkoopprijzen tooother auto's gebruikt. Dit is een populair en nuttige type machine learning. Zijn alle Hallo-modules in Azure Machine Learning-algoritmen, behalve voor leren met supervisie [K-Means Clustering][k-means-clustering].

  * In **leren zonder supervisie**, gegevenspunten hebben geen labels worden gekoppeld. In plaats daarvan Hallo doel van een leeralgoritme zonder supervisie tooorganize Hallo gegevens in een bepaalde manier of toodescribe is de structuur. Dit kan betekenen groeperen in clusters, zoals het K-means of het vinden van verschillende manieren van complexe gegevens bekijkt, zodat deze eenvoudiger weergegeven.

  * In **versterking learning**, Hallo algoritme opgehaald toochoose een actie in antwoord tooeach gegevenspunt. Er is een algemene benadering in robotics, waarbij Hallo reeks sensormetingen op één punt in tijd een gegevenspunt en Hallo-algoritme moet de volgende actie van Hallo robot kiezen. Het is ook een natuurlijke geschikt is voor Internet der dingen-toepassingen. Hallo leeralgoritme ontvangt ook een derden signaal korte tijd later, die aangeeft hoe goed Hallo besluit is. Op basis hiervan Hallo algoritme Hiermee wijzigt u de strategie voor de volgorde tooachieve Hallo hoogste derden. Er zijn momenteel geen versterking learning-algoritme-modules in Azure ML.

* **Bayesiaanse methoden** Hallo veronderstelling van statistisch onafhankelijke gegevenspunten maken. Dit betekent dat Hallo unmodeled variabiliteit in één gegevenspunt is niet-gerelateerde met anderen, dat wil zeggen, niet kan worden voorspeld. Bijvoorbeeld, als Hallo gegevens geregistreerd Hallo aantal minuten op waarna de volgende trein train Hallo aankomt, twee metingen bij een dag bij elkaar statistisch onafhankelijk zijn. Echter twee metingen bij een minuut bij elkaar zijn niet statistisch onafhankelijke - Hallo-waarde van een maximaal voorspellende van Hallo-waarde van andere Hallo is.

* **Boosted decision tree regressie** wordt gebruikgemaakt van de functie overlapping of interactie tussen onderdelen. Dat betekent dat in een bepaalde gegevens aanwijst, waarde van een functie Hallo is enigszins voorspellende van Hallo-waarde van een andere. Bijvoorbeeld dagelijks hoge en lage temperatuur gegevens kunt lage temperatuur Hallo weten voor Hallo dag u toomake een redelijke schatting op Hallo hoog. Hallo-gegevens in de twee functies Hallo is enigszins overbodig.

* Gegevens classificeren in meer dan twee categorieën kan worden gedaan met behulp van een classificatie inherent meerdere klasse, of door een combinatie van een set van twee klasse classificaties in een **ensemble**. Hallo ensemble verstrekt, is een afzonderlijke tweeklasse classificatie voor elke objectklasse - elkaar worden gescheiden Hallo gegevens in twee categorieën: 'dit class' en "niet deze klasse." Vervolgens wordt deze classificaties stemmen op de juiste toewijzing van het gegevenspunt Hallo Hallo. Dit is de operationele principe Hallo achter [One-vs-All-Multiklasse][one-vs-all-multiclass].

* Verschillende methoden, met inbegrip van logistic regression en Hallo Bayes point machine wordt ervan uitgegaan dat **lineaire klassengrenzen**. Dat wil zeggen, ze wordt ervan uitgegaan dat Hallo grenzen tussen klassen zijn ongeveer rechte lijnen (of hyperplanes in meer algemene geval Hallo). Vaak is dit een kenmerk van Hallo gegevens dat u niet weet pas nadat u tooseparate hebt geprobeerd, maar er is iets dat doorgaans kan worden geleerd door het visualiseren van tevoren. Als uw Hallo klassengrenzen zeer onregelmatige wensen, houd beslissingsstructuren, besluit jungles, ondersteuning voor vector machines of neural networks.

* Neural networks met categorische variabelen kunnen worden gebruikt door het maken van een **dummy-variabele** voor elke categorie instellen too1 in gevallen waarin Hallo categorie is toegepast, wordt 0 waarbij dit niet het geval.


<!-- This is how you can embed a link in an image in HTML. Don't know how toodo this in markdown.
<a href="http://download.microsoft.com/download/A/6/1/A613E11E-8F9C-424A-B99D-65344785C288/microsoft-machine-learning-algorithm-cheat-sheet.pdf">
<img src="C:\Users\garye\azure-docs-pr\articles\media\machine-learning-algorithm-cheat-sheet\cheat-sheet-small.png">
</a>
-->

<!-- Module References -->
[a-z-list]: https://msdn.microsoft.com/library/azure/dn906033.aspx
[initialize-model]: https://msdn.microsoft.com/library/azure/0c67013c-bfbc-428b-87f3-f552d8dd41f6/
[k-means-clustering]: https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/
[one-vs-all-multiclass]: https://msdn.microsoft.com/library/azure/7191efae-b4b1-4d03-a6f8-7205f87be664/
