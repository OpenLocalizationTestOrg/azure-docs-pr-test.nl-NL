---
title: aaaIs uw gegevens klaar te maken voor gegevenswetenschap? Evaluatie van de gegevens - Azure Machine Learning | Microsoft Docs
description: Meer informatie over Hallo 4 criteria voor gegevens toobe gereed voor gegevenswetenschap. Gegevenswetenschap voor beginnende gebruikers video 2 is concrete voorbeelden toohelp met basisgegevens evaluatieversie.
keywords: relevante gegevens gegevens evalueren, gegevens, gegevens criteria, gegevens gereed voorbereiden
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: d502062c-da70-4b21-9054-0bfd9902612e
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: ef6bb680ace771537157dbdd50a4ccce0a3eb7ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="is-your-data-ready-for-data-science"></a>Zijn gegevens gereed voor gegevenswetenschap?
## <a name="video-2-data-science-for-beginners-series"></a>Video 2: Gegevenswetenschap voor beginnende gebruikers reeks
Meer informatie over hoe tooevaluate uw gegevens toomake basic criteria toobe gereed voor gegevenswetenschap voldoet.

tooget hello optimaal gebruik van reeksen Hallo, bekijk ze allemaal. [Ga toohello lijst met video 's](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Shows/SupervisionNotRequired/9/player]
>
>

## <a name="other-videos-in-this-series"></a>Andere video's in deze reeks
*Gegevenswetenschap voor beginnende gebruikers* is een korte inleiding toodata wetenschappelijke in vijf korte video's.

* Video 1: [Hallo 5 gegevens wetenschappelijke antwoorden op vragen](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*
* Video 2: Uw gegevens gereed Is voor gegevenswetenschap?
* Video 3: [Stel een vraag kunt u met gegevens beantwoorden](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*
* Video 4: [voorspellen een antwoord met een eenvoudige model](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*
* Video 5: [kopiëren van anderen werk toodo voor gegevenswetenschap](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*

## <a name="transcript-is-your-data-ready-for-data-science"></a>De tekst: Uw gegevens gereed Is voor gegevenswetenschap?
Welkom te 'Is uw gegevens gereed voor gegevenswetenschap?' tweede video in de reeks Hallo Hallo *Gegevenswetenschap voor beginnende gebruikers*.  

Voordat gegevens wetenschappelijke kunt geven Hallo van antwoorden die u wilt, moet u toogive deze sommige toowork grondstoffen van hoge kwaliteit met. Net als bij het maken van een pizza is Hallo Hallo betere Hallo ingrediënten u beginnen met, beter Hallo uiteindelijke product. 

## <a name="criteria-for-data"></a>Criteria voor gegevens
Dus in Hallo geval van wetenschappelijke gegevens zijn er enkele ingrediënten dat we toopull samen moeten.

We moeten de gegevens die zijn:

* Relevante
* Verbonden
* Nauwkeurige
* Onvoldoende toowork met

## <a name="is-your-data-relevant"></a>Uw gegevens relevant is?
Daarom eerste ingrediënt Hallo - gegevens die relevant is moet.

![Relevante gegevens versus irrelevante gegevens - gegevens worden geëvalueerd](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/relevant-and-irrelevant-data.png)

Hallo tabel aan de linkerkant Hallo kijken. Wij zeven mensen buiten Boston balken voldaan, gemeten hun bloed alcohol niveau, Hallo rood Sox batting gemiddelde in de laatste wedstrijd en Hallo prijs melk in Hallo dichtstbijzijnde gemak store.

Dit zijn alle perfect legitieme gegevens. Het enige probleem is dat niet relevant. Er is geen duidelijke relatie tussen deze getallen. Als ik gegeven Hallo van huidige prijs van melk en Hallo rood Sox batting gemiddelde, is er geen manier kan de inhoud van mijn bloed alcohol geschat.

Nu bekijkt hello tabel op Hallo rechts. Deze tijd wordt gemeten elke persoon hoofdtekst Hallo voor massaopslag en getelde aantal dranken al.  Hallo cijfers in elke rij zijn nu andere relevante tooeach. Als ik gestuurd mijn hoofdtekst massaopslag en Hallo aantal Margaritas ik hebt, kunt u een schatting op mijn bloed alcohol inhoud.

## <a name="do-you-have-connected-data"></a>U verbinding hebt gemaakt gegevens?
de volgende ingrediënt Hallo zijn verbonden gegevens.

![Gekoppelde gegevens versus verbroken gegevens - gegevens criteria, gereed](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/connected-vs-disconnected-data.png)

Hier volgt een aantal relevante gegevens op Hallo kwaliteit van hamburgers: grill temperatuur, patty gewicht en classificatie in lokale voeding Hallo magazine. Maar let op Hallo hiaten in de tabel aan de linkerkant Hallo Hallo.

Sommige waarden ontbreken in de meeste gegevenssets. Algemene toohave gaten als volgt is en er worden manieren toowork omheen. Maar als er te veel ontbreekt, uw gegevens toolook zoals Zwitserland kaas begint.

Als u hello tabel aan de linkerkant hello bekijkt, er is dus veel ontbrekende gegevens, is het vaste toocome up met elk soort relatie tussen grill temperatuur- en patty gewicht. Dit is een voorbeeld van een niet-verbonden gegevens.

Hallo-tabel op Hallo rechts echter vol is en is voltooid - een voorbeeld van verbonden gegevens.

## <a name="is-your-data-accurate"></a>Uw gegevens nauwkeurig is?
Hallo is volgende ingrediënt we moeten nauwkeurig. Hier vindt u vier doelen dat willen we graag toohit met pijlen.

![Nauwkeurige gegevens versus onnauwkeurige gegevens - gegevens criteria](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/inaccurate-vs-accurate-data.png)

Hallo-doel in de rechterbovenhoek Hallo kijken. Wij hebben een nauwe groepering rechts rond Hallo roos. Dat is natuurlijk nauwkeurig. Oddly, in de taal van de Hallo van wetenschappelijke gegevens, onze prestaties op Hallo doel rechts eronder wordt ook beschouwd als nauwkeurig.

Als u toomap uit Hallo center van deze pijlen, ziet u dat het zeer nauwe toohello Roos is. Hallo pijlen zijn verdeeld rondom Hallo doel, zodat deze worden beschouwd als onnauwkeurige, maar ze zijn gericht op het Hallo-Roos zodat deze worden beschouwd als nauwkeurige.

Nu bekijkt hello linksboven doel. Onze pijlen Druk hier heel dicht bij elkaar, een nauwe groepering. Ze zijn nauwkeurig, maar ze zijn onjuist omdat Hallo center manier uit Hallo roos. En natuurlijk Hallo pijlen in Hallo linksonder doel onnauwkeurig en onnauwkeurige zijn. Deze archer moet meer practice.

## <a name="do-you-have-enough-data-toowork-with"></a>Hebt u onvoldoende gegevens toowork met?
Ten slotte ingrediënt #4 - moet toohave onvoldoende gegevens.

![Hebt u voldoende gegevens voor analyse? Evaluatie van de gegevens](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/barely-enough-data.png)

Elk gegevenspunt in de tabel als een lijn verfkwast in een afbeelden zien. Als u slechts enkele van deze, Hallo afbeelden mag vrij fuzzy - harde tootell is wat is.

Als u een aantal meer kwast streken toevoegt, vervolgens uw afbeelden tooget een weinig scherper wordt gestart.

Wanneer u nauwelijks voldoende streken hebt, ziet u net voldoende toomake aantal brede beslissingen nemen. Is het ergens dat mogelijk wil toovisit? Het lijkt erop helder, dat ziet eruit als schoon water: Ja, dat waar ik ga op vakantie is.

Als u meer gegevens toevoegt, Hallo afbeelding wordt duidelijker en u meer gedetailleerde beslissingen kunt nemen. Nu kunt ik bekijkt hello drie hotels op Hallo links bank. U weet, ik echt architecturale functies Hallo Hallo op Hallo voorgrond zoals. Ik moet er, blijven op Hallo derde floor.

Met gegevens die relevant zijn, verbonden, nauwkeurig, en voldoende, hebben we alle Hallo ingrediënten moet toodo sommige gegevenswetenschap van hoge kwaliteit.

Ervoor toocheck uit Hallo worden andere vier video's in *Gegevenswetenschap voor beginnende gebruikers* van Microsoft Azure Machine Learning.

## <a name="next-steps"></a>Volgende stappen
* [Probeer een eerste gegevens wetenschappelijke experiment met Machine Learning Studio](machine-learning-create-experiment.md)
* [Ophalen van een inleiding tooMachine Learning in Microsoft Azure](machine-learning-what-is-machine-learning.md)
