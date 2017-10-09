---
title: aaaPredict een antwoord met een eenvoudige regressiemodel - Azure Machine Learning | Microsoft Docs
description: Hoe een eenvoudige regressie toocreate model toopredict een prijs in Gegevenswetenschap voor beginnende gebruikers video 4. Bevat een lineaire regressie met doelgegevens.
keywords: maken van een model, eenvoudige model, prijs voorspelling, eenvoudige regressiemodel
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: a28f1fab-e2d8-4663-aa7d-ca3530c8b525
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: d4270c2237c33b7e898b78a08b292bc9d62e49ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="predict-an-answer-with-a-simple-model"></a>Met een eenvoudig model een antwoord voorspellen
## <a name="video-4-data-science-for-beginners-series"></a>Video 4: Gegevenswetenschap voor beginnende gebruikers reeks
Meer informatie over hoe een eenvoudige regressie model toopredict toocreate prijs van een ruitvormige in Gegevenswetenschap voor beginnende gebruikers video 4 Hallo. We gaat een regressiemodel met doelgegevens tekenen.

tooget hello optimaal gebruik van reeksen Hallo, bekijk ze allemaal. [Ga toohello lijst met video 's](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-predict-an-answer-with-a-simple-model/player]
>
>

## <a name="other-videos-in-this-series"></a>Andere video's in deze reeks
*Gegevenswetenschap voor beginnende gebruikers* is een korte inleiding toodata wetenschappelijke in vijf korte video's.

* Video 1: [Hallo 5 gegevens wetenschappelijke antwoorden op vragen](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*
* Video 2: [uw gegevens gereed Is voor gegevenswetenschap?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 min 56 sec)*
* Video 3: [Stel een vraag kunt u met gegevens beantwoorden](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*
* Video 4: Een antwoord met een eenvoudige model voorspellen
* Video 5: [kopiëren van anderen werk toodo voor gegevenswetenschap](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*

## <a name="transcript-predict-an-answer-with-a-simple-model"></a>De tekst: Een antwoord met een eenvoudige model voorspellen
Welkom toohello vierde video in Hallo 'Data wetenschappelijke voor beginnende gebruikers' reeks. In dit voorbeeld we een eenvoudige model bouwen en maken van een voorspelling.

Een *model* wordt een vereenvoudigde artikel over onze gegevens. Ik ziet u heb.

## <a name="collect-relevant-accurate-connected-enough-data"></a>Collect relevante, nauwkeurige, verbonden, voldoende gegevens
Ik wil zeggen tooshop voor een ruitvormige. Ik heb een ring die deel uitmaakten van toomy oma met een instelling voor een ruitvormige 1.35 karaat en ik wil tooget een idee van wat er gaat kosten. Ik een Kladblok en pen rekening gehouden Hallo juwelen store en ik schrijf Hallo prijs van alle Hallo uur per maand werken Hallo en hoeveel ze afwegen in carats. Beginnen met Hallo eerste ruitvormige - de 1.01 carats en $7,366.

Ik Ga nu via en doe dit voor alle Hallo andere diamanten Hallo store.

![Kolommen met gegevens ruitvormige](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/diamond-data.png)

U ziet dat onze lijst twee kolommen. Elke kolom heeft een ander kenmerk - gewicht in carats en prijs- en elke rij is één gegevenspunt dat een enkele ruitvormige vertegenwoordigt.

Er is een klein daadwerkelijk gemaakt van gegevensset hier - een tabel. U ziet dat het voldoet aan de criteria voor kwaliteit:

* Hallo gegevens **relevante** -gewicht is definitief gerelateerde tooprice
* Deze heeft **nauwkeurige** -we goed Hallo prijzen die we Noteer gecontroleerd
* Deze heeft **verbonden** -er zijn geen spaties in een van deze kolommen
* En zullen we zien, heeft **voldoende** gegevens tooanswer onze vraag

## <a name="ask-a-sharp-question"></a>Stel een vraag kruis
Nu we onze vraag kruis zodanig hebt inhouden: 'hoeveel kosten toobuy een ruitvormige 1.35 karaat?'

Onze lijst geen een ruitvormige 1.35 karaat, dus we toouse Hallo rest van onze gegevens tooget een antwoord toohello vraag hebt.

## <a name="plot-hello-existing-data"></a>Bestaande gegevens Hallo tekenen
Hallo van de eerste wat die we doen is een horizontale lijn van het aantal as, toochart Hallo gewichten aangeroepen worden getekend. Hallo-bereik van de gewichten Hallo is 0 too2 zodat we je een lijn die betrekking heeft op die variëren en ticks voor elk half karaat plaatsen tekenen.

Naast we tekenen van een verticale as toorecord Hallo prijs en verbindt u deze toohello gewicht horizontale as. Dit is in eenheden van bedragen. Nu hebben we een reeks coördinaat assen.

![Gewicht en prijs assen](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/weight-and-price-axes.png)

We gaan tootake nu deze gegevens zijn en er een *spreidingsgrafiek tekent*. Dit is een uitstekende manier toovisualize numerieke gegevenssets.

Voor het eerste gegevenspunt hello krijgen we van een verticale lijn op 1.01 carats. Vervolgens wordt een horizontale lijn op $7,366 krijgen. Wanneer ze voldoen aan, we een punt wordt getekend. Hiermee wordt de eerste ruitvormige.

Nu we elke ruitvormige op deze lijst doorlopen en hetzelfde Hallo. Wanneer we via, is dit krijgen we: een aantal punten, één voor elke ruitvormige.

![Spreiding van de grafiek](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/scatter-plot.png)

## <a name="draw-hello-model-through-hello-data-points"></a>Hallo-model door Hallo gegevenspunten worden getekend
Nu als u hello puntjes en squint bekijkt, Hallo verzameling ziet eruit als een fat fuzzy lijn. We kunnen onze markering nemen en een lineaire ermee wordt getekend.

Door het tekenen van een regel gemaakt een *model*. Beschouwen als de echte wereld Hallo duurt en het aanbrengen van een eenvoudig cartoon versie ervan. Nu Hallo cartoon is onjuist: Hallo regel niet kan worden verstuurd alle Hallo gegevenspunten. Maar is een nuttig vereenvoudiging.

![Lineaire regressie regel](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/linear-regression-line.png)

Hallo feit dat alle Hallo punten gaan niet precies door Hallo-regel is in orde. Gegevenswetenschappers Leg dit door in te spreken dat Hallo model is - die Hallo regel - en vervolgens elk punt heeft enkele *ruis* of *variantie* gekoppeld. Er is perfect relatie onderliggende hello en is de Hallo ingaan, echte wereld waardoor ruis en onzekerheid worden toegevoegd.

Omdat we tooanswer Hallo vraag proberen *hoeveel?* dit heet een *regressie*. En omdat we maken gebruik van een lineaire is een *lineaire regressie*.

## <a name="use-hello-model-toofind-hello-answer"></a>Hallo model toofind Hallo antwoord gebruiken
Nu we een model hebben en we onze vraag vragen: hoeveel kost een ruitvormige 1.35 karaat?

tooanswer onze vraag, wij krijgen 1.35 carats en tekenen van een verticale lijn. Wanneer het Hallo Modelregel bestrijkt, krijgen we een horizontale lijn toohello dollar as. Het treffers recht op 10.000. Giek! Dat is Hallo-antwoord: een ruitvormige 1.35 karaat kost ongeveer 10.000 $.

![Hallo antwoord vinden op Hallo-model](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/find-the-answer.png)

## <a name="create-a-confidence-interval"></a>Een betrouwbaarheidsinterval maken
Het is natuurlijk toowonder hoe precies deze voorspelling. Het is nuttig tooknow of Hallo 1.35 karaat ruitvormige te bijna worden $10.000 of veel hoger of lager. toofigure deze, we tekenen een envelop rond Hallo regressielijn die de meeste Hallo punten bevat. Deze envelop heet onze *betrouwbaarheidsinterval*: we vrij zeker van bent dat prijzen binnen deze envelop vallen, omdat in de afgelopen Hallo de meeste van deze hebben. We tekenen twee meer horizontale lijnen van waarbij Hallo 1.35 karaat regel Hallo boven- en Hallo van envelop overschrijden.

![Betrouwbaarheidsinterval](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/confidence-interval.png)

Nu je iets over onze betrouwbaarheidsinterval: je zorgeloos dat Hallo prijs van een ruitvormige 1.35 karaat ongeveer $10.000 is - maar mogelijk zo laag fl 8.000 en mogelijk fl 12.000 zo hoog.

## <a name="were-done-with-no-math-or-computers"></a>We klaar bent, zonder math of computers
We hebben gedaan welke gegevenswetenschappers betaald toodo en we deze door te tekenen voldoet:

* We vraag een dat we met gegevens beantwoorden kan
* Moesten een *model* met *lineaire regressie*
* Er een *voorspelling*, voltooid met een *betrouwbaarheidsinterval*

En gebruiken we niet toodo math of computers deze.

Nu als we gehad meer informatie, zoals...

* Hallo Hallo ruitvormige knippen
* kleurvariaties (Hallo ruitvormige is hoe dicht toobeing wit)
* het aantal insluitingen in Hallo ruitvormige Hallo

.. .en we zouden hebben meer kolommen. Math wordt in dat geval handig zijn. Als u meer dan twee kolommen hebben, is het vaste toodraw punten op papier. Hallo math kunt u die regel of die vlak tooyour gegevens zeer mooi passen.

Ook als in plaats van slechts een handvol ruiten, zijn twee duizend of twee miljoen en vervolgens kunt u die werken veel sneller uitvoeren met een computer.

Vandaag de dag besproken over hoe de lineaire regressie toodo en we een voorspelling met behulp van gegevens gemaakt.

Niet zeker toocheck uit Hallo andere video's in 'Data wetenschappelijke voor beginnende gebruikers' van Microsoft Azure Machine Learning.

## <a name="next-steps"></a>Volgende stappen
* [Probeer een eerste gegevens wetenschappelijke experiment met Machine Learning Studio](machine-learning-create-experiment.md)
* [Ophalen van een inleiding tooMachine Learning in Microsoft Azure](machine-learning-what-is-machine-learning.md)
