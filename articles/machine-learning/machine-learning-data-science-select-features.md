---
title: aaaFeature selectie in Hallo Team gegevens wetenschap proces | Microsoft Docs
description: Hallo-doel van functieselectie worden en voorbeelden gegeven van hun rol in de procedure voor de verbetering van Hallo gegevens van machine learning.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 878541f5-1df8-4368-889a-ced6852aba47
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: zhangya;bradsev
ms.openlocfilehash: 54af93c83e4cc6a3670b3ad62490e0f74082b4ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="feature-selection-in-hello-team-data-science-process-tdsp"></a>Functieselectie in Hallo Team gegevens wetenschap proces (TDSP)
In dit artikel wordt uitgelegd Hallo doeleinden van functieselectie en vindt u voorbeelden van de rol in de procedure voor de verbetering van Hallo gegevens van machine learning. Deze voorbeelden zijn afkomstig van Azure Machine Learning Studio. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Hallo engineering en selectie van functies is een onderdeel van Hallo Team gegevens wetenschap proces (TDSP) die worden beschreven in [wat is er Hallo Team gegevens wetenschap proces?](data-science-process-overview.md). Selectie van functie-engineering en zijn onderdelen van Hallo **functies ontwikkelen** stap Hallo TDSP.

* **functie-engineering**: dit proces probeert toocreate extra relevante functies van bestaande onbewerkte functies Hallo Hallo gegevens en tooincrease predictive vermogen toohello learning-algoritme.
* **functie selectie**: dit proces Hallo sleutel subset van functies van de oorspronkelijke gegevens in een poging tooreduce Hallo dimensionaliteit van Hallo training probleem selecteren.

Normaal gesproken **functie-engineering** is toegepaste eerste toogenerate extra functies en Hallo **functie selectie** stap is uitgevoerd tooeliminate irrelevante, redundante of maximaal gecorreleerde functies.

## <a name="filtering-features-from-your-data---feature-selection"></a>Filteren van de functies van uw gegevens - Functieselectie
Functieselectie is een proces dat vaak voor Hallo constructie van training gegevenssets voor voorspellende modelleertaken zoals classificatie- of regressiemodel taken wordt toegepast. Hallo-doel is een subset van Hallo-functies uit de oorspronkelijke gegevensset Hallo die de afmetingen verminderen met behulp van een minimale set functies toorepresent Hallo maximale hoeveelheid variantie in Hallo gegevens tooselect. Deze subset van functies worden vervolgens Hallo alleen functies toobe tootrain Hallo model opgenomen. Functieselectie fungeert twee hoofddoelen.

* Eerst Functieselectie vaak verhoogt de nauwkeurigheid van de classificatie doordat irrelevante, redundante of maximaal gecorreleerde functies.
* Ten tweede neemt Hallo aantal functies waardoor model trainingsproces efficiënter af. Dit is vooral belangrijk voor overbrengen die dure tootrain zoals ondersteuning vector machines zijn.

Hoewel Functieselectie tooreduce Hallo aantal functies in Hallo gegevensset gebruikt tootrain Hallo model zoeken, is het niet meestal waarnaar wordt verwezen tooby Hallo term 'dimensionaliteit vermindering'. Functie selectiemethodes extraheren een subset van de oorspronkelijke functies in Hallo gegevens niet wijzigen.  Dimensionaliteit vermindering methoden gebruiken engineering functies die u kunnen de oorspronkelijke functies Hallo transformeren en ze zo te wijzigen. Voorbeelden van dimensionaliteit vermindering methoden zijn Principal onderdeel analyse, canonieke correlatieanalyse en enkelvoud waarde afbreken.

Onder andere wordt één breed worden toegepast categorie van functie selectiemethoden in een context die onder supervisie 'filteren op basis van functieselectie' genoemd. Deze methoden toepassen door te evalueren Hallo correlatie tussen elke functie en Hallo target-kenmerk, een statistische meting tooassign een score tooeach-functie. Hallo-functies zijn vervolgens gerangschikt op Hallo score, die mogelijk gebruikte toohelp ingestelde Hallo drempelwaarde voor behouden of een specifieke functie geëlimineerd. Voorbeelden van Hallo statistische metingen die worden gebruikt in deze methoden zijn persoon correlatie, wederzijdse informatie en test Hallo Chi-kwadraat.

In Azure Machine Learning Studio zijn er modules die zijn opgegeven voor de Functieselectie van de. Zoals u in de volgende afbeelding Hallo, deze modules bevatten [Functieselectie op basis van het Filter] [ filter-based-feature-selection] en [Fisher lineaire Discriminant analyse] [ fisher-linear-discriminant-analysis].

![Voorbeeld van de functie-selectie](./media/machine-learning-data-science-select-features/feature-Selection.png)

U kunt bijvoorbeeld Hallo Hallo [Functieselectie op basis van het Filter] [ filter-based-feature-selection] module. Hallo doel gemak gaan we toouse Hallo analysemodel tekstvoorbeeld die hierboven worden beschreven. Wordt ervan uitgegaan dat willen we een regressiemodel nadat een set van 256 functies worden gemaakt via Hallo toobuild [hash-functie] [ feature-hashing] module en die Hallo antwoord variabele Hallo 'Col1' en een boek vertegenwoordigt bekijken beoordelingen variëren van 1 too5. Hiervoor 'Functie score berekenen methode' toobe 'Pearson correlatie' Hallo 'Doelkolom' toobe 'Col1' en Hallo 'Het aantal gewenste functies' too50. Vervolgens Hallo module [Functieselectie op basis van het Filter] [ filter-based-feature-selection] waarmee een gegevensset met 50 functies samen met het doelkenmerk Hallo 'Col1' wordt geproduceerd. Hallo volgende afbeelding toont Hallo stroom van dit experiment en Hallo invoerparameters die hierboven wordt beschreven.

![Voorbeeld van de functie-selectie](./media/machine-learning-data-science-select-features/feature-Selection1.png)

Hallo toont volgende afbeelding Hallo resulterende gegevenssets. Elke functie wordt berekend op basis van Hallo Pearson correlatie tussen zichzelf en target-kenmerk 'Col1' Hallo. Hallo-functies met de hoogste scores worden bewaard.

![Voorbeeld van de functie-selectie](./media/machine-learning-data-science-select-features/feature-Selection2.png)

Hallo bijbehorende scores van functies Hallo geselecteerd worden weergegeven in Hallo volgende afbeelding.

![Voorbeeld van de functie-selectie](./media/machine-learning-data-science-select-features/feature-Selection3.png)

Door het toepassen van dit [Functieselectie op basis van het Filter] [ filter-based-feature-selection] 50 van 256 functies worden geselecteerd omdat ze hebben meest gecorreleerde functies met doelvariabele Hallo 'Col1' Hallo-module op basis van het Hallo score berekenen methode 'Pearson correlatie'.

## <a name="conclusion"></a>Conclusie
Functie-engineering en Functieselectie zijn twee meestal ontworpen en geselecteerde onderdelen efficiënter Hallo Hallo dat tooextract Hallo belangrijke informatie in Hallo gegevens probeert te trainen. Bovendien de Hallo kracht van deze modellen tooclassify Hallo ingevoerde gegevens correct en toopredict resultaten van belang meer krachtig. Selectie van functie-engineering en kunnen u ook toomake Hallo learning meer rekenkundig tractable combineren. Dit gebeurt met verbeteren en vervolgens terug te brengen Hallo aantal functies nodig toocalibrate of trein een model. Wiskundig spreken Hallo functies geselecteerde tootrain Hallo model zijn een minimale set van onafhankelijke variabelen die Hallo patronen in Hallo gegevens leggen en vervolgens de resultaten met succes voorspellen.

Houd er rekening mee dat het is niet altijd noodzakelijkerwijs tooperform techniek of functie Functieselectie. Hiermee wordt aangegeven of het nodig is of niet, is afhankelijk van Hallo gegevens we hebben of verzamelen, Hallo algoritme die we kiest, en Hallo doelstelling van Hallo experiment.

<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/

