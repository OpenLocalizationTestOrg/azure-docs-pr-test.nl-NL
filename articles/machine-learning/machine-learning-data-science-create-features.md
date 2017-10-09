---
title: aaaFeature engineering in gegevenswetenschap | Microsoft Docs
description: Hallo doeleinden van functie-engineering worden en voorbeelden gegeven van de rol in de procedure voor de verbetering van Hallo gegevens van machine learning.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 3fde69e8-5e7b-49ad-b3fb-ab8ef6503a4d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: zhangya;bradsev
ms.openlocfilehash: af40ea9cc9395bc87fe695eeaef26aa71e0ec9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="feature-engineering-in-data-science"></a>Functie-engineering in gegevenswetenschap
In dit onderwerp wordt uitgelegd Hallo doeleinden van functie-engineering en vindt u voorbeelden van de rol in de procedure voor de verbetering van Hallo gegevens van machine learning. Hallo voorbeelden gebruikt tooillustrate dit proces zijn afkomstig van Azure Machine Learning Studio. 

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Dit **menu** koppelingen tootopics waarin wordt beschreven hoe toocreate functies voor gegevens in verschillende omgevingen. Deze taak is een stap in Hallo [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

Functie engineering pogingen tooincrease Hallo voorspellend vermogen van learning-algoritmen door het maken van de functies van ruwe gegevens waarmee Hallo leerproces vergemakkelijken. Hallo engineering en selectie kenmerken één deel uitmaakt van Hallo TDSP die worden beschreven in Hallo [wat Hallo Team gegevens wetenschap proces lifecycle is?](data-science-process-overview.md) Selectie van functie-engineering en zijn onderdelen van Hallo **functies ontwikkelen** stap Hallo TDSP. 

* **functie-engineering**: dit proces probeert toocreate extra relevante functies van bestaande Hallo onbewerkte functies in Hallo gegevens en tooincrease Hallo predictive vermogen van Hallo learning-algoritme.
* **functie selectie**: dit proces Hallo sleutel subset van functies van de oorspronkelijke gegevens in een poging tooreduce Hallo dimensionaliteit van Hallo training probleem selecteren.

Normaal gesproken **functie-engineering** is toegepaste eerste toogenerate extra functies en Hallo **functie selectie** stap is uitgevoerd tooeliminate irrelevante, redundante of maximaal gecorreleerde functies.

Hallo trainingsgegevens gebruikt in machine learning kan vaak worden verbeterd door extractie van functies van Hallo ruwe gegevens verzameld. Een voorbeeld van een engineering-functie in de context te leren hoe tooclassify Hallo installatiekopieën geschreven tekens is voor het maken van een beetje dichtheid kaart gemaakt op basis van Hallo onbewerkte bits distributiegegevens Hallo. Dit overzicht kunt u efficiënter dan gewoon rechtstreeks met de onbewerkte verdeling Hallo Hallo randen van Hallo tekens vinden.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="creating-features-from-your-data---feature-engineering"></a>Maken van de functies van uw gegevens - functie-Engineering
Hallo trainingsgegevens bestaat uit een matrix die bestaan uit voorbeelden (records of opmerkingen die zijn opgeslagen in rijen), die allemaal een aantal functies (variabelen of velden die zijn opgeslagen in de kolommen). Hallo-functies die zijn opgegeven in de opzet Hallo zijn verwachte toocharacterize Hallo patronen in Hallo gegevens. Hoewel veel van de onbewerkte gegevens Hallo velden kunnen rechtstreeks worden opgenomen in de geselecteerde functie set die wordt gebruikt tootrain een model hello, is het vaak Hallo geval die aanvullende (Engineering) functies toobe gemaakt op basis van functies in Hallo onbewerkte gegevens toogenerate een verbeterde Hallo moeten training gegevensset.

Wat voor soort functies moet tooenhance Hallo gegevensset gemaakt bij het trainen van een model? Engineering functies waarmee u Hallo training kunt bieden informatie die beter Hallo patronen in Hallo-gegevens onderscheidt. We verwachten Hallo nieuwe functies tooprovide aanvullende informatie die niet de oorspronkelijke of een bestaande functieset Hallo duidelijk vastgelegde of gemakkelijk zichtbaar in. Maar dit proces is er een illustratie. Audio- en productief beslissingen vereist vaak sommige expertise in verschillende domeinen.

Bij het starten met Azure Machine Learning, is het eenvoudigste toograsp dit proces concrete invulling te geven met behulp van voorbeelden die is opgegeven in Hallo Studio. Twee voorbeelden worden hier weergegeven:

* Een voorbeeld van een regressie [voorspelling van het aantal fiets huren Hallo](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4) in een bewaakte experiment waarbij Hallo doelwaarden bekend zijn
* Een tekst analysemodel classificatie voorbeeld met [hash-functies](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/)

## <a name="example-1-adding-temporal-features-for-regression-model"></a>Voorbeeld 1: Tijdelijke functies toe te voegen voor regressiemodel
We gaan gebruiken Hallo experiment 'voorspellen van de vraag van bikes' in Azure Machine Learning Studio toodemonstrate hoe tooengineer functies voor een taak regressie. Hallo-doel van dit experiment is toopredict Hallo vraag naar Hallo fietsen, dat wil zeggen, Hallo aantal fiets huren binnen een specifieke maand/dag/uur. dataset Hallo ' fiets verhuur UCI gegevensset ' wordt gebruikt als Hallo onbewerkte invoergegevens. Deze gegevensset is gebaseerd op echte gegevens van Hallo kapitaal Bikeshare bedrijf die een fiets verhuur-netwerk in Washington DC in Hallo Verenigde Staten heeft. Hallo gegevensset Hallo aantal fiets huren binnen een specifieke uur van een dag in Hallo jaar 2011 en het jaar 2012 vertegenwoordigt en bevat 17379 rijen en kolommen 17. Hallo onbewerkte functieset bevat weer voorwaarden (vochtigheid-temperatuur/o-snelheid) en type Hallo Hallo dag (vakantiedag/werkdag). Hallo veld toopredict is 'cnt', een aantal die staat voor Hallo fiets huren binnen een specifieke uur en die variëren van 1 too977 bereiken.

Met Hallo doel van het construeren van effectieve functies in Hallo trainingsgegevens, vier regressie modellen zijn gebouwd met behulp van Hallo dezelfde algoritme, maar met vier verschillende training gegevenssets. Hallo vier gegevenssets vertegenwoordigen Hallo dezelfde onbewerkte invoergegevens, maar met een toenemend aantal functies ingesteld. Deze functies zijn gegroepeerd in vier categorieën:

1. A = weer + vakantiedag + weekdag + functies voor het weekend voor Hallo voorspelde dag
2. B = aantal eventueel een gehuurd zijn in elk Hallo vorige 12 uur
3. C = aantal eventueel een zijn gehuurd in elk Hallo vorige 12 dagen op Hallo dezelfde uur
4. D = aantal eventueel een zijn gehuurd in elk Hallo vorige 12 weken op Hallo dezelfde uur en Hallo dezelfde dag

Naast de functie set A, die al bestaan in de oorspronkelijke onbewerkte gegevens hello, hello andere drie sets van functies worden gemaakt via Hallo functie technisch proces. Functie ingesteld B opnamen recente aanvraag voor Hallo bikes. Functie ingesteld C opnamen Hallo-aanvraag voor bikes op een bepaald uur. D opnamen aanvraag voor bikes functie ingesteld op bepaalde uur en bepaalde dag van week Hallo. Hallo vier training gegevenssets elke omvat set-functie A, A + B, A + B + C en A + B + C + D, respectievelijk.

In Azure Machine Learning-experiment hello, worden deze vier training gegevenssets via vier vertakkingen van voorverwerkte invoergegevensset Hallo gevormd. Behalve hello links de meeste vertakking, bevat elk van deze filialen van een [R-Script uitvoeren](https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/) module, waarin een verzameling afgeleide functies (functie ingesteld B en C D) respectievelijk gebouwd en toegevoegde toohello geïmporteerd gegevensset zijn. Hallo volgende afbeelding ziet u Hallo R-script gebruikt toocreate functieset B in Hallo tweede links vertakking.

![functies maken](./media/machine-learning-data-science-create-features/addFeature-Rscripts.png)

vergelijking van de testresultaten en prestaties van vier modellen worden samengevat in de volgende tabel Hallo Hallo HALLO hallo. de beste resultaten Hallo worden weergegeven door functies A + B + C. Let op Hallo fout tarief neemt af wanneer extra functies zijn opgenomen in Hallo trainingsgegevens. Er wordt gecontroleerd met onze vermoeden dat Hallo-functieset B, C bieden aanvullende relevante informatie voor Hallo regressie taak. Maar toe te voegen Hallo D functie lijkt niet tooprovide elke extra daling Hallo Foutfrequentie.

![resultaat-vergelijking](./media/machine-learning-data-science-create-features/result1.png)

## <a name="example2"></a>Voorbeeld 2: Het maken van functies in analysemodel tekst
Functie-engineering is breed in taken gerelateerde tootext mijnbouw, zoals document indeling en het gevoel analyse toegepast. Bijvoorbeeld, wanneer we tooclassify documenten in verschillende categorieën willen, is een typische veronderstelling dat Hallo word/zinnen opgenomen in een document categorie minder waarschijnlijk toooccur in een andere doc-categorie zijn. Hallo replicatiefrequentie Hallo woorden/woordgroepen distributie is in een andere woorden, kunnen toocharacterize document verschillende categorieën. Omdat afzonderlijke stukjes tekstinhoud gewoonlijk als invoergegevens hello gebruikt, is Hallo functie proces engineering in tekst gegevensanalyse-toepassingen nodig toocreate Hallo functies met betrekking tot woord of woordgroep frequenties.

tooachieve dit taak, een techniek die genoemd **hash-functie** is toegepaste tooefficiently Schakel willekeurige tekstfuncties in indexen. In plaats van elke functie (woorden/zinnen) tooa bepaalde tekstindex, deze methode werkt door het toepassen van een hash-functie toohello onderdelen en hun hash-waarden als indexen rechtstreeks koppelen.

In Azure Machine Learning is een [hash-functie](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) module die u maakt deze woord of woordgroep functies gemakkelijk. Volgende afbeelding toont een voorbeeld van het gebruik van deze module. Hallo-invoergegevensset bestaat uit twee kolommen: Hallo adresboek classificatie variëren van 1 too5 en Hallo werkelijke revisie inhoud. Hallo-doel van dit [hash-functie](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) module is tooretrieve een aantal nieuwe functies die Hallo exemplaar frequentie Hallo overeenkomt woorden weergeven / s-zin(nen) binnen Hallo bepaald boek controleren. toouse deze module moet toocomplete Hallo stappen te volgen:

* Selecteer eerst Hallo kolom met de ingevoerde tekst hello ('Col2' in dit voorbeeld).
* Ten tweede ingesteld Hallo 'Hashing bitsize' too8, wat betekent 2 dat ^ 8 = 256 functies wordt gemaakt. Hallo woord of fase in alle Hallo tekst worden too256 hash-indexen. Hallo-parameter 'Hashing bitsize' varieert van 1 too31. Hallo woorden / r-zin(nen) zijn minder waarschijnlijk toobe opgedeeld in Hallo dezelfde index als een groter aantal toobe instellen.
* Hallo parameter 'N-grams' too2 derde is ingesteld. Dit Hallo exemplaar frequentie van unigrams (een functie voor elke één woord) en bigrams (een functie voor elk paar aangrenzende woorden) van de ingevoerde tekst hello opgehaald. Hallo parameter 'N-grams' kan variëren van 0 too10 waarmee wordt aangegeven Hallo kunt u het maximum aantal opeenvolgende woorden toobe opgenomen in een functie.  

![Module 'Functie Hashing'](./media/machine-learning-data-science-create-features/feature-Hashing1.png)

Hallo volgende afbeelding ziet u wat Hallo deze nieuwe functie eruit.

![Voorbeeld 'Functie Hashing'](./media/machine-learning-data-science-create-features/feature-Hashing2.png)

## <a name="conclusion"></a>Conclusie
Engineering en geselecteerde functies efficiënter Hallo Hallo trainingsproces tooextract Hallo belangrijke informatie in Hallo-gegevens probeert. Bovendien de Hallo kracht van deze modellen tooclassify Hallo ingevoerde gegevens correct en toopredict resultaten van belang meer krachtig. Selectie van functie-engineering en kunnen u ook toomake Hallo learning meer rekenkundig tractable combineren. Dit gebeurt met verbeteren en vervolgens terug te brengen Hallo aantal functies nodig toocalibrate of trein een model. Wiskundig spreken Hallo functies geselecteerde tootrain Hallo model zijn een minimale set van onafhankelijke variabelen die Hallo patronen in Hallo gegevens leggen en vervolgens de resultaten met succes voorspellen.

Houd er rekening mee dat het is niet altijd noodzakelijkerwijs tooperform techniek of functie Functieselectie. Hiermee wordt aangegeven of het nodig is of niet, is afhankelijk van Hallo gegevens we hebben of verzamelen, Hallo algoritme die we kiest, en Hallo doelstelling van Hallo experiment.

