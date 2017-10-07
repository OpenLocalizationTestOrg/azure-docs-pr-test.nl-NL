---
title: de vraaggegevens van een beantwoorden kan - aaaAsk problemen wetenschap - Azure Machine Learning | Microsoft Docs
description: Meer informatie over hoe een kruis gegevenswetenschap tooformulate vraag in de wetenschap voor beginnende gebruikers gegevens video 3. Bevat een vergelijking van classificatie en regressie vragen.
keywords: vragen over de wetenschap van gegevens van problemen wetenschappelijke gegevens formuleren vragen, regressie vragen, classificatievragen, kruis vraag
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: 5b9501e3-9964-417a-8ffc-8913103da77b
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: 00c328f51e6d9ff6654b5966eb97d6762582f7e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="ask-a-question-you-can-answer-with-data"></a>Stel een vraag die u met gegevens kunt beantwoorden
## <a name="video-3-data-science-for-beginners-series"></a>Video 3: Gegevenswetenschap voor beginnende gebruikers reeks
Meer informatie over hoe tooformulate een probleem met wetenschappelijke gegevens in een vraag in Gegevenswetenschap voor beginnende gebruikers video 3. In deze video bevat een vergelijking van vragen voor classificatie en regressie algoritmen.

tooget hello optimaal gebruik van reeksen Hallo, bekijk ze allemaal. [Ga toohello lijst met video 's](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Data-science-for-beginners-Ask-a-question-you-can-answer-with-data/player]
>
>

## <a name="other-videos-in-this-series"></a>Andere video's in deze reeks
*Gegevenswetenschap voor beginnende gebruikers* is een korte inleiding toodata wetenschappelijke in vijf korte video's.

* Video 1: [Hallo 5 gegevens wetenschappelijke antwoorden op vragen](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*
* Video 2: [uw gegevens gereed Is voor gegevenswetenschap?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 min 56 sec)*
* Video 3: Stel een vraag die u met gegevens beantwoorden kunt
* Video 4: [voorspellen een antwoord met een eenvoudige model](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*
* Video 5: [kopiëren van anderen werk toodo voor gegevenswetenschap](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*

## <a name="transcript-ask-a-question-you-can-answer-with-data"></a>De tekst: Stel een vraag die u met gegevens beantwoorden kunt
Welkom toohello derde video in de reeks Hallo 'Wetenschappelijke gegevens voor beginnende gebruikers'.  

In dit voorbeeld krijgt u een aantal tips voor het opstellen van een vraag die u met gegevens kan beantwoorden.

Mogelijk krijgt u meer buiten deze video als u eerst video Hallo twee eerder in deze serie: 'hello 5 vragen gegevenswetenschap kan beantwoorden' en 'Is uw gegevens is gereed voor gegevenswetenschap?'

## <a name="ask-a-sharp-question"></a>Stel een vraag kruis
Besproken over hoe gegevenswetenschap is Hallo proces van het gebruik van namen (ook wel categorieën of labels) en cijfers toopredict een antwoord tooa vraag. Maar niet elke vraag; Deze toobe heeft een *kruis vraag.*

Een vaag vraag heeft geen toobe beantwoord met een naam of een cijfer. Er moet een kruis vraag.

Stel dat u een magische licht met een genie die wordt naar waarheid elke vraag die u vragen beantwoorden gevonden. Maar er is een mischievous genie en hij proberen toomake zijn antwoord als vaag en verwarrend zijn als hij met opslag kunt ophalen. Gewenste toopin hem omlaag met een vraag dus luchtdichte hij niet kan helpen maar vertellen wat u wilt dat tooknow.

Als u een vaag vraag tooask zoals 'Wat er gebeurt toohappen met mijn stock?', Hallo genie mogelijk beantwoorden, 'Hallo prijs verandert'. Die een ware antwoord is, maar het is niet erg nuttig.

Maar als u een kruis vraag, zoals 'Wat mijn stock prijzen worden volgende week?', hello genie kan niet helpen maar bieden u een specifieke tooask waren beantwoorden en een verkoopprijs voorspellen.

## <a name="examples-of-your-answer-target-data"></a>Voorbeelden van uw antwoord: gegevens zijn gericht
Nadat u uw vraag formuleren, Controleer toosee of hebt u voorbeelden van Hallo antwoord in uw gegevens.

Als de vraag "Wat kan mijn stock verkoopprijs zijn volgende week?" vervolgens hebben we toomake zorgen dat onze gegevens Hallo aandelenkoersen geschiedenis bevat.

Als de vraag 'welke auto in mijn wagenpark is momenteel toofail eerst?' vervolgens hebben we zeker dat onze gegevens omvatten informatie over eerdere mislukte toomake.

![Doelgegevens - voorbeelden van het antwoord. Een wetenschappelijke gegevens vraag formuleren.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/target-data.png)

Deze voorbeelden van antwoorden worden een doel genoemd. Een doel is wat we zijn toopredict over toekomstige gegevenspunten probeert een categorie of een getal.

Als u geen doelgegevens, moet u enkele tooget. U niet kunt tooanswer uw vraag zonder deze.

## <a name="reformulate-your-question"></a>Uw vraag reformulate
U kunt ook uw vraag tooget een nuttiger antwoord uitgelegd.

Hallo vraag 'Is deze gegevens punt A of B?' voorspelt Hallo categorie (of de naam of label) van iets. tooanswer, gebruiken we een *classificatiealgoritme*.

Hallo vraag 'Hoeveel?' of 'Hoeveel?' voorspelt een bedrag. tooanswer deze gebruiken we een *regression-algoritme*.

toosee hoe kunnen we deze, transformeren bekijken we Hallo vraag 'welke verhaal nieuws is de meest interessante toothis lezer Hallo?' Wordt de gebruiker gevraagd een voorspelling van één keuze uit tal van mogelijkheden - met andere woorden 'Is deze A of B of C of D?' - en een classificatie-algoritme zou gebruiken.

Maar deze vraag mogelijk eenvoudiger tooanswer als uitgelegd als 'hoe interessante is elk artikel in deze lijst toothis lezer?' Nu kunt u geven elk artikel een numerieke score en wordt het eenvoudig tooidentify Hallo hoogste score berekenen artikel. Dit is een formuleren Hallo classificatie vraag in een vraag regressie of hoeveel?

![Uw vraag reformulate. Classificatie vraag versus regressie vraag.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/classification-question-vs-regression-question.png)

Hoe u een vraag is een aanwijzing toowhich algoritme vragen geven, kunnen u een antwoord.

U vindt dat bepaalde families van algoritmen - zoals Hallo die in ons voorbeeld van het artikel nieuws - nauw verwant zijn. U kunt uw vraag toouse Hallo algoritme waarmee u reformulate Hallo nuttigst antwoord.

Maar zeer belangrijk, vraag die kruis - Hallo vraag die u met gegevens kan beantwoorden. En controleer of u Hallo juiste gegevens tooanswer zijn deze.

Besproken over sommige basisprincipes voor u een vraag stelt dat u met gegevens kan beantwoorden.

Niet zeker toocheck uit Hallo andere video's in 'Data wetenschappelijke voor beginnende gebruikers' van Microsoft Azure Machine Learning.

## <a name="next-steps"></a>Volgende stappen
* [Probeer een eerste gegevens wetenschappelijke experiment met Machine Learning Studio](machine-learning-create-experiment.md)
* [Ophalen van een inleiding tooMachine Learning in Microsoft Azure](machine-learning-what-is-machine-learning.md)
