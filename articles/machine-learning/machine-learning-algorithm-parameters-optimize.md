---
title: aaaOptimize uw algoritmen in Azure Machine Learning | Microsoft Docs
description: Legt uit hoe toochoose Hallo optimale parameterset voor een Azure Machine Learning-algoritme.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6717e30e-b8d8-4cc1-ad0b-1d4727928d32
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: fbf2f71abdbce19483fb048d67a39cbb368a928e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="choose-parameters-toooptimize-your-algorithms-in-azure-machine-learning"></a>Het kiezen van de parameters toooptimize uw algoritmen in Azure Machine Learning
Dit onderwerp wordt beschreven hoe toochoose Hallo rechts hyperparameter ingesteld voor een Azure Machine Learning-algoritme. De meeste machine learning-algoritmen hebben tooset parameters. Wanneer u het model trainen, moet u tooprovide waarden voor die parameters. Hallo effectiviteit van het getrainde model hello, is afhankelijk van Hallo Modelparameters die u kiest. Hallo Hallo optimale set parameters voor zoeken wordt genoemd *model selectie*.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Er zijn verschillende manieren toodo modelselectie. Kruisvalidatie is een van de meest gebruikte Hallo methoden voor het modelselectie in machine learning zijn en het Hallo model selectie standaardmechanisme in Azure Machine Learning is. Omdat Azure Machine Learning R- en Python ondersteunt, kunt u altijd hun eigen model selectie mechanismen implementeren met behulp van R of Python.

Er zijn vier stappen in Hallo-proces van het beste parameterset Hallo vinden:

1. **Hallo parameter ruimte definiëren**: voor Hallo-algoritme exacte parameterwaarden Hallo gewenste tooconsider eerst bepalen.
2. **Hallo kruisvalidatie instellingen definiëren**: bepalen hoe toochoose kruisvalidatie vouwen voor Hallo dataset.
3. **Hallo metriek definiëren**: Bepaal welke metrische toouse voor het bepalen van Hallo aanbevolen set parameters, zoals nauwkeurigheid, root mean squared fout, precisie, intrekken of f-score.
4. **Trainen, te evalueren en te vergelijken**: voor elke unieke combinatie van parameterwaarden Hallo kruisvalidatie is uitgevoerd door en gebaseerd op Hallo fout metriek die u definieert. Na evaluatie en vergelijking kunt u de best presterende Hallo-model.

Hallo volgende afbeelding ziet u dat toont hoe u kunt dit in Azure Machine Learning doen.

![De beste parameterset Hallo vinden](./media/machine-learning-algorithm-parameters-optimize/fig1.png)

## <a name="define-hello-parameter-space"></a>Hallo parameter ruimte definiëren
Hallo-parameter is ingesteld op Hallo model initialisatie stap kunt u definiëren. Hallo deelvenster parameter van alle machine learning-algoritmen heeft twee trainer modi: *één Parameter* en *Parameter bereik*. Kies bereik van de Parameter-modus. In het bereik van de Parameter-modus, kunt u meerdere waarden opgeven voor elke parameter. In het tekstvak Hallo kunt u door komma's gescheiden waarden.

![Twee klasse gestimuleerd beslissingsstructuur één parameter](./media/machine-learning-algorithm-parameters-optimize/fig2.png)

 U kunt ook Hallo maximale en minimale punten van Hallo raster en totaal aantal punten toobe gegenereerd met Hallo definiëren **gebruik bereik Builder**. Standaard worden Hallo parameterwaarden een lineaire schaal gegenereerd. Maar als **logaritmische schaal** is ingeschakeld, Hallo waarden worden gegenereerd in Hallo logaritmische schaal (dat wil zeggen, Hallo ratio van de aangrenzende punten Hallo constant is in plaats van hun verschil). Voor integer-parameters, kunt u een bereik definiëren met een koppelteken. Bijvoorbeeld "1-10" betekent dat alle gehele getallen tussen 1 en 10 (zowel liggen) Hallo parameterset vormen. Een gemengde modus wordt ook ondersteund. Bijvoorbeeld, Hallo parameterset ' 1-10, 20, 50 ' bevatten gehele getallen van 1 tot 10, 20, en 50.

![Twee klasse gestimuleerd beslissingsstructuur parameter bereik](./media/machine-learning-algorithm-parameters-optimize/fig3.png)

## <a name="define-cross-validation-folds"></a>Kruisvalidatie vouwen definiëren
Hallo [partitie en steekproef] [ partition-and-sample] module gebruikte toorandomly toewijzen vouwen toohello gegevens kan worden. In Hallo volgende voorbeeldconfiguratie voor de module hello, we vijf vouwen definiëren en een vouw willekeurig aantal exemplaren van toohello voorbeeld toewijzen.

![Partitie en steekproef](./media/machine-learning-algorithm-parameters-optimize/fig4.png)

## <a name="define-hello-metric"></a>Hallo metriek definiëren
Hallo [Tune Model Hyperparameters] [ tune-model-hyperparameters] module biedt ondersteuning voor het kiezen van langs Hallo aanbevolen set parameters voor een bepaald algoritme en de gegevensset. Bovendien tooother informatie met betrekking tot training Hallo model hello **eigenschappen** deelvenster van deze module Hallo metrische gegevens voor het bepalen van de beste parameterset Hallo bevat. Twee verschillende vervolgkeuzelijst vakken voor de classificatie en regressie algoritmen, heeft respectievelijk. Als Hallo algoritme betrokken een classificatie-algoritme is, Hallo regressie metriek is genegeerd en vice versa. In dit specifieke voorbeeld Hallo meetwaarde is **nauwkeurigheid**.   

![Vegen parameters](./media/machine-learning-algorithm-parameters-optimize/fig5.png)

## <a name="train-evaluate-and-compare"></a>Trainen, te evalueren en te vergelijken
Hallo dezelfde [Tune Model Hyperparameters] [ tune-model-hyperparameters] module traint alle Hallo modellen die overeenkomen met de parameterset toohello, evalueert verschillende metrische gegevens en maakt vervolgens Hallo best getrainde model op basis van Hallo metriek die u kiest. Deze module heeft twee verplichte invoeren:

* Hallo ongetrainde cursist
* Hallo-gegevensset

Hallo-module heeft ook een optionele gegevensset invoer. Hallo dataset verbinden met vouwen informatie toohello verplichte gegevensset invoer. Als Hallo gegevensset vouwen informatie niet is toegewezen, klikt u vervolgens een 10-fold kruisvalidatie automatisch standaard uitgevoerd. Hallo vouwen toewijzing is niet uitgevoerd en een gegevensset validatie op Hallo optionele gegevensset poort wordt aangeboden, vervolgens een train-test-modus is gekozen als Hallo eerste gegevensset gebruikt tootrain Hallo model voor elke parametercombinatie is.

![Gestimuleerd decision tree classificatie](./media/machine-learning-algorithm-parameters-optimize/fig6a.png)

Hallo model wordt vervolgens geëvalueerd op Hallo validatie gegevensset. Hallo links uitvoerpoort van Hallo-module bevat verschillende metrische gegevens als functies van parameterwaarden. Hallo rechts uitvoerpoort biedt Hallo getrainde model dat overeenkomt met de best presterende model toohello volgens toohello metriek gekozen (**nauwkeurigheid** in dit geval).  

![Validatie van gegevensset](./media/machine-learning-algorithm-parameters-optimize/fig6b.png)

Hallo exacte parameters gekozen door de juiste uitvoerpoort Hallo visualiseren, kunt u zien. Dit model kan worden gebruikt in een testset score berekenen of in een geoperationaliseerd webservice nadat ze zijn opgeslagen als een getraind model.

<!-- Module References -->
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[tune-model-hyperparameters]: https://msdn.microsoft.com/library/azure/038d91b6-c2f2-42a1-9215-1f2c20ed1b40/
