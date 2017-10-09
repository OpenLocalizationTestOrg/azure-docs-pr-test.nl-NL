---
title: aaaFeature engineering en selectie in Azure Machine Learning | Microsoft Docs
description: Hallo doeleinden van functieselectie en functie-engineering wordt en vindt u voorbeelden van hun rol binnen Hallo gegevens verbetering proces van machine learning.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ceb524d-842e-4f77-9eae-a18e599442d6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2017
ms.author: zhangya;bradsev
ROBOTS: NOINDEX
redirect_url: machine-learning-data-science-create-features
redirect_document_id: True
ms.openlocfilehash: e3e59329bf46f334396f5975b4e656137362d7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="feature-engineering-and-selection-in-azure-machine-learning"></a>Functietechniek en -selectie in Azure Machine Learning
Dit onderwerp wordt uitgelegd Hallo doeleinden van functie-engineering en Functieselectie in Hallo gegevens verbetering proces van machine learning. Dit wordt geïllustreerd hoe deze processen eruit ziet met behulp van de voorbeelden die worden geleverd door Azure Machine Learning Studio.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Hallo trainingsgegevens gebruikt in machine learning kan vaak worden verbeterd door Hallo selectie of extractie van functies van Hallo ruwe gegevens verzameld. Een voorbeeld van een engineering functie in de context hello te leren hoe tooclassify Hallo installatiekopieën geschreven tekens is een kaart bits dichtheid gemaakt op basis van Hallo onbewerkte bits distributiegegevens. Deze kaart kunt u efficiënter dan onbewerkte distributie Hallo Hallo randen van Hallo tekens vinden.

Engineering en geselecteerde functies efficiënter Hallo Hallo trainingsproces tooextract Hallo belangrijke informatie in Hallo-gegevens probeert. Bovendien de Hallo kracht van deze modellen tooclassify Hallo ingevoerde gegevens correct en toopredict resultaten van belang meer krachtig. Selectie van functie-engineering en kunnen u ook toomake Hallo learning meer rekenkundig tractable combineren. Dit gebeurt met verbeteren en vervolgens terug te brengen Hallo aantal functies nodig toocalibrate of trein een model. Wiskundig spreken Hallo functies geselecteerde tootrain Hallo model zijn een minimale set van onafhankelijke variabelen die Hallo patronen in Hallo gegevens leggen en vervolgens de resultaten met succes voorspellen.

Hallo engineering en selectie kenmerken maakt deel uit van een groter proces, die normaal gesproken uit vier stappen bestaat:

* Gegevensverzameling
* Gegevensverbetering
* Bouw model
* Naverwerking

Engineering en selectie vormen Hallo gegevens verbetering stap van de machine learning. Drie aspecten van dit proces kunnen worden onderscheiden voor onze toepassing:

* **Gegevens vooraf verwerken**: dit proces probeert tooensure die verzamelde gegevens Hallo schoon en consistent is. Dit omvat taken zoals het integreren van meerdere gegevenssets, verwerking ontbrekende gegevens, verwerking inconsistente gegevens en converteren van gegevenstypen.
* **Functie-engineering**: dit proces probeert toocreate extra relevante functies van bestaande Hallo onbewerkte functies in Hallo gegevens en tooincrease predictive vermogen toohello learning-algoritme.
* **Functie selectie**: dit proces Hallo sleutel subset van de oorspronkelijke gegevens functies tooreduce Hallo dimensionaliteit van Hallo training probleem selecteert.

In dit onderwerp alleen worden Hallo functie-engineering en functie selectie aspecten van Hallo gegevens verbetering processen. Zie voor meer informatie over Hallo gegevens vooraf verwerken stap [vooraf verwerken van gegevens in Azure Machine Learning Studio](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/).

## <a name="creating-features-from-your-data--feature-engineering"></a>Maken van de functies van uw gegevens--functie-engineering
Hallo trainingsgegevens bestaat uit een matrix die bestaan uit voorbeelden (records of opmerkingen die zijn opgeslagen in rijen), die allemaal een aantal functies (variabelen of velden die zijn opgeslagen in de kolommen). Hallo-functies die zijn opgegeven in de opzet Hallo zijn verwachte toocharacterize Hallo patronen in Hallo gegevens. Hoewel veel van de onbewerkte gegevens Hallo velden kunnen rechtstreeks worden opgenomen in de geselecteerde functie set die wordt gebruikt tootrain een model hello, moeten aanvullende engineering functies vaak toobe gemaakt op basis van het Hallo-functies in Hallo onbewerkte gegevens toogenerate een set trainingsgegevens verbeterde.

Wat voor soort functies moet tooenhance Hallo gegevensset gemaakt bij het trainen van een model? Engineering functies waarmee u Hallo training kunt bieden informatie die beter Hallo patronen in Hallo-gegevens onderscheidt. Hallo nieuwe functies tooprovide aanvullende informatie die niet duidelijk vastgelegde of gemakkelijk zichtbaar in de oorspronkelijke Hallo verwacht of bestaande functie ingesteld, maar dit proces is er een illustratie. Audio- en productief beslissingen vereist vaak sommige expertise in verschillende domeinen.

Bij het starten met Azure Machine Learning, is het eenvoudigste toograsp dit proces concrete invulling te geven met behulp van de voorbeelden die is opgegeven in Machine Learning Studio. Twee voorbeelden worden hier weergegeven:

* Een voorbeeld van een regressie ([voorspelling van het aantal fiets huren Hallo](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4)) in een bewaakte experiment waarbij Hallo doelwaarden bekend zijn
* Een tekst-analysemodel classificatie voorbeeld met [hash-functies][feature-hashing]

### <a name="example-1-adding-temporal-features-for-a-regression-model"></a>Voorbeeld 1: Tijdelijke functies voor een regressiemodel toevoegen
toodemonstrate hoe tooengineer functies voor een taak regressie we gebruik Hallo experiment 'voorspellen van de vraag van bikes' in Azure Machine Learning Studio. Hallo-doel van dit experiment is toopredict Hallo vraag naar Hallo fietsen, dat wil zeggen, Hallo aantal fiets huren binnen een specifieke maand, dag of uur. Hallo-gegevensset **fiets verhuur UCI gegevensset** wordt gebruikt als Hallo onbewerkte invoergegevens.

Deze gegevensset is gebaseerd op echte gegevens van Hallo kapitaal Bikeshare bedrijf die een fiets verhuur-netwerk in Washington DC in Hallo Verenigde Staten heeft. Hallo-gegevensset staat Hallo aantal fiets huren binnen een specifieke uur van een dag, uit 2011 too2012 en bevat 17379 rijen en kolommen 17. Hallo onbewerkte functieset bevat weer voorwaarden (temperatuur, vochtigheid, o snelheid) en type Hallo Hallo dag (vakantiedag of weekdag). Hallo veld toopredict is **cnt**, een aantal die Hallo fiets huren binnen een specifieke uur staat en die een bereik van 1 too977.

tooconstruct effectieve functies in Hallo trainingsgegevens, vier regressie modellen zijn gebouwd met behulp van Hallo dezelfde algoritme, maar met vier verschillende trainingsgegevens ingesteld. Hallo vier gegevenssets vertegenwoordigen Hallo dezelfde onbewerkte invoergegevens, maar met een toenemend aantal functies ingesteld. Deze functies zijn gegroepeerd in vier categorieën:

1. A = weer + vakantiedag + weekdag + functies voor het weekend voor Hallo voorspelde dag
2. B = aantal eventueel een gehuurd zijn in elk Hallo vorige 12 uur
3. C = aantal eventueel een zijn gehuurd in elk Hallo vorige 12 dagen op Hallo dezelfde uur
4. D = aantal eventueel een zijn gehuurd in elk Hallo vorige 12 weken op Hallo dezelfde uur en Hallo dezelfde dag

Naast de functie set A, die al in de oorspronkelijke onbewerkte gegevens hello bestaat, hello andere drie sets van functies worden gemaakt via Hallo functie technisch proces. Functie B opnamen Hallo recente aanvraag voor Hallo bikes ingesteld. Functie ingesteld C opnamen Hallo-aanvraag voor bikes op een bepaald uur. D opnamen aanvraag voor bikes functie ingesteld op bepaalde uur en bepaalde dag van week Hallo. Elk van de vier Hallo training gegevenssets functiesets bevat A, A + B, A + B + C en A + B + C + D, respectievelijk.

In Azure Machine Learning-experiment hello, worden deze vier training gegevenssets via vier vertakkingen van Hallo voorverwerkte gegevens invoerset gevormd. Met uitzondering van de meest linkse vertakking hello, elk van deze vertakkingen bevat een [R-Script uitvoeren] [ execute-r-script] module waarin een set functies (functie stelt B en C D) afgeleid respectievelijk is gemaakt en toegevoegd toohello geïmporteerd gegevensset. Hallo volgende afbeelding ziet u Hallo R-script gebruikt toocreate functieset B in Hallo tweede links vertakking.

![Een verzameling functies maken](./media/machine-learning-feature-selection-and-engineering/addFeature-Rscripts.png)

Hallo volgende tabel ziet u Hallo vergelijking van Hallo de testresultaten en prestaties van vier Hallo-modellen. de beste resultaten Hallo worden weergegeven door functies A + B + C. Houd er rekening mee dat Foutfrequentie Hallo afneemt wanneer extra functiesets zijn opgenomen in Hallo trainingsgegevens. Hiermee wordt gecontroleerd met onze vermoeden dat Hallo functiesets B en C vindt u aanvullende relevante informatie voor Hallo regressie taak. Toe te voegen Hallo D-functieset lijkt niet tooprovide elke extra daling Hallo Foutfrequentie.

![Vergelijk de testresultaten en prestaties](./media/machine-learning-feature-selection-and-engineering/result1.png)

### <a name="example2"></a>Voorbeeld 2: Het maken van functies in analysemodel tekst
Functie-engineering is breed in taken gerelateerde tootext mijnbouw, zoals document indeling en het gevoel analyse toegepast. Bijvoorbeeld, als u wilt dat tooclassify documenten in verschillende categorieën, is een typische veronderstelling dat Hallo woorden of zinnen die zijn opgenomen in één documentcategorie minder waarschijnlijk toooccur in een andere documentcategorie zijn. Hallo frequentie van Hallo woord of woordgroep distributie is met andere woorden, kunnen toocharacterize document verschillende categorieën. In tekst analysemodel toepassingen is het Hallo-functie proces engineering benodigde toocreate Hallo functies met betrekking tot woord of woordgroep frequenties omdat afzonderlijke stukjes tekstinhoud meestal fungeren als invoergegevens Hallo.

tooachieve dit taak, een techniek die genoemd *hash-functie* is toegepaste tooefficiently Schakel willekeurige tekstfuncties in indexen. In plaats van elke functie (woorden of zinnen) tooa bepaalde tekstindex, deze methode werkt door het toepassen van een hash-functie toohello onderdelen en met behulp van de hashwaarden als indexen rechtstreeks koppelen.

In Azure Machine Learning is een [hash-functie] [ feature-hashing] module die u deze functies woord of woordgroep maakt. Hallo toont volgende afbeelding een voorbeeld van het gebruik van deze module. Hallo invoer gegevensset bevat twee kolommen: Hallo adresboek classificatie variëren van 1 too5 en Hallo werkelijke revisie inhoud. Hallo-doel van dit [hash-functie] [ feature-hashing] -module is tooretrieve nieuwe functies die Hallo exemplaar frequentie van Hallo bijbehorende woorden of zinnen binnen Hallo bepaald boek revisie weergeven. toouse deze module, moet u toocomplete Hallo stappen te volgen:

1. Selecteer Hallo kolom met de ingevoerde tekst hello (**Col2** in dit voorbeeld).
2. Stel *Hashing bitsize* too8, wat betekent 2 dat ^ 8 = 256 functies worden gemaakt. Hallo woord of zinsdeel in de tekst hello is vervolgens opgedeeld too256 indexen. parameter Hallo *bitsize Hashing* kan variëren van 1 too31. Als het Hallo-parameter is ingesteld tooa number, Hallo woorden of zinnen is het minder waarschijnlijk toobe opgedeeld in Hallo dezelfde index.
3. Stel de parameter Hallo *N-grams* too2. Dit Hallo exemplaar frequentie van unigrams (een functie voor elke één woord) en bigrams (een functie voor elk paar aangrenzende woorden) opgehaald uit de invoertekst Hallo. parameter Hallo *N-grams* kan variëren van 0 too10 waarmee wordt aangegeven Hallo kunt u het maximum aantal opeenvolgende woorden toobe opgenomen in een functie.  

![Hash-functie-module](./media/machine-learning-feature-selection-and-engineering/feature-Hashing1.png)

Hallo volgende afbeelding ziet u hoe deze nieuwe functies eruit.

![Voorbeeld van de hash-functie](./media/machine-learning-feature-selection-and-engineering/feature-Hashing2.png)

## <a name="filtering-features-from-your-data--feature-selection"></a>Functies van uw gegevens--Functieselectie filteren
*Functie selectie* is een proces dat is meestal toohello constructie van gegevenssets training voor voorspellende modelleertaken zoals classificatie- of regressiemodel taken toegepast. Hallo-doel is een subset van functies van Hallo oorspronkelijke gegevensset die de afmetingen met behulp van een minimale set functies toorepresent Hallo maximale hoeveelheid variantie in Hallo gegevens vermindert Hallo tooselect. Deze subset van functies bevat Hallo alleen functies toobe opgenomen tootrain Hallo model. Functieselectie vervult twee hoofddoelen:

* Functieselectie vaak verhoogt de nauwkeurigheid van de classificatie doordat irrelevante, redundante of maximaal gecorreleerde functies.
* Functie selectie afname Hallo aantal functies, waardoor Hallo model trainingsproces efficiënter. Dit is vooral belangrijk voor overbrengen die dure tootrain zoals ondersteuning vector machines zijn.

Hoewel Functieselectie tooreduce Hallo aantal functies in Hallo gegevensset gebruikt tootrain Hallo model zoekt, is het niet gewoonlijk aangeduid tooby Hallo term *dimensionaliteit te beperken.* Functie selectiemethodes extraheren een subset van de oorspronkelijke functies in Hallo gegevens niet wijzigen.  Dimensionaliteit vermindering methoden gebruiken engineering functies die u kunnen de oorspronkelijke functies Hallo transformeren en ze zo te wijzigen. Voorbeelden van dimensionaliteit vermindering methoden zijn principal onderdeel analyse, canonieke correlatieanalyse en enkelvoud waarde afbreken.

Een breed worden toegepast categorie selectiemethodes functie in een context die onder supervisie is Functieselectie op basis van het filter. Deze methoden toepassen door te evalueren Hallo correlatie tussen elke functie en Hallo target-kenmerk, een statistische meting tooassign een score tooeach-functie. Hallo functies worden vervolgens gerangschikt op Hallo score, waarin u kunt tooset Hallo drempel voor het behouden of een specifieke functie geëlimineerd. Voorbeelden van Hallo statistische metingen die worden gebruikt in deze methoden zijn Pearson correlatie, wederzijdse informatie en Hallo chi-kwadraatttest.

Azure Machine Learning Studio bevat modules voor functies selecteren. Zoals u in de volgende afbeelding Hallo, deze modules bevatten [Functieselectie op basis van het Filter] [ filter-based-feature-selection] en [Fisher lineaire Discriminant analyse] [ fisher-linear-discriminant-analysis].

![Voorbeeld van de functie-selectie](./media/machine-learning-feature-selection-and-engineering/feature-Selection.png)

Gebruik bijvoorbeeld Hallo [Functieselectie op basis van het Filter] [ filter-based-feature-selection] module met Hallo analysemodel tekstvoorbeeld eerder beschreven. Stel nu dat u een regressiemodel toobuild nadat een set van 256 functies is gemaakt via Hallo [hash-functie] [ feature-hashing] -module en die variabele Hallo-antwoord is **Col1**en vertegenwoordigt een boek controleren classificatie variëren van 1 too5. Stel **scoreprofiel methode functie** te**Pearson correlatie**, **doelkolom** te**Col1**, en **gewenst aantal functies** te**50**. Hallo module [Functieselectie op basis van het Filter] [ filter-based-feature-selection] vervolgens produceert een gegevensset met 50 functies samen met de Hallo doelkenmerk **Col1**. Hallo volgende afbeelding toont Hallo stroom van dit experiment en Hallo invoerparameters.

![Voorbeeld van de functie-selectie](./media/machine-learning-feature-selection-and-engineering/feature-Selection1.png)

Hallo volgende afbeelding ziet u de resulterende gegevenssets Hallo. Elke functie wordt berekend op basis van Hallo Pearson correlatie tussen zichzelf en Hallo doelkenmerk **Col1**. Hallo-functies met de hoogste scores worden bewaard.

![Functie voor op basis van het filter selectie gegevenssets](./media/machine-learning-feature-selection-and-engineering/feature-Selection2.png)

Hallo volgende afbeelding toont Hallo bijbehorende scores van Hallo geselecteerde functies.

![Geselecteerde functie scores](./media/machine-learning-feature-selection-and-engineering/feature-Selection3.png)

Door het toepassen van dit [Functieselectie op basis van het Filter] [ filter-based-feature-selection] module, 50 van 256 functies zijn geselecteerd omdat ze hebben de meeste functies gecorreleerd met doelvariabele Hallo Hallo **Col1** op basis van Hallo score berekenen voor methode **Pearson correlatie**.

## <a name="conclusion"></a>Conclusie
Functie-engineering en Functieselectie zijn twee stappen tooprepare Hallo trainingsgegevens vaak worden uitgevoerd tijdens het bouwen van een machine learning-model. Normaal gesproken functie-engineering is toegepast eerste toogenerate extra functies en vervolgens Hallo functie selectie stap is uitgevoerd tooeliminate irrelevante, redundante of maximaal gecorreleerde onderdelen.

Het is niet altijd noodzakelijkerwijs tooperform techniek of functie Functieselectie. Hiermee wordt aangegeven of deze nodig is, is afhankelijk van Hallo gegevens hebben of het verzamelen, Hallo algoritme die u kiest, en het Hallo doelstelling van Hallo experiment.

<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/
