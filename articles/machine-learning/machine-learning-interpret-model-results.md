---
title: aaaInterpret model resulteert in een Machine Learning | Microsoft Docs
description: Hoe toochoose Hallo optimale parameterset voor het gebruik van een algoritme en visualiseren score-model levert.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6230e5ab-a5c0-4c21-a061-47675ba3342c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52161b1aa5ff3e7a63fc4b1bfb7c5e354eabcc50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="interpret-model-results-in-azure-machine-learning"></a>Model resulteert in een Azure Machine Learning interpreteren
Dit onderwerp wordt uitgelegd hoe toovisualize en interpreteren voorspelling resulteert in een Azure Machine Learning Studio. Nadat u hebt een model wordt getraind en gedaan voorspellingen toe ('hello model score'), u moet toounderstand en Hallo voorspelling resultaat interpreteren.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Er zijn vier belangrijke typen van machine learning-modellen in Azure Machine Learning:

* Classificatie
* Clustering
* Regressie
* Recommender systemen

Hallo-modules die worden gebruikt voor de prognose boven op deze modellen zijn:

* [Score Model] [ score-model] -module voor de classificatie en regressie
* [Toewijzen van tooClusters] [ assign-to-clusters] -module voor clustering
* [Score Matchbox Recommender] [ score-matchbox-recommender] voor systemen die aanbeveling

Dit document wordt uitgelegd hoe toointerpret voorspelling resulteert voor elk van deze modules. Zie voor een overzicht van deze modules [hoe toochoose parameters toooptimize uw algoritmen in Azure Machine Learning](machine-learning-algorithm-parameters-optimize.md).

Dit onderwerp bevat voorspelling interpretatie maar niet de evaluatie van het model. Voor meer informatie over het tooevaluate uw model Zie [hoe tooevaluate prestaties in Azure Machine Learning model](machine-learning-evaluate-model-performance.md).

Als u nieuwe tooAzure Machine Learning en hoeft te maken van een eenvoudig experiment tooget gestart, Zie [een eenvoudig experiment maken in Azure Machine Learning Studio](machine-learning-create-experiment.md) in Azure Machine Learning Studio.

## <a name="classification"></a>Classificatie
Er zijn twee subcategorieën van classificatie problemen:

* Problemen met slechts twee klassen (tweeklasse of binaire classificatie)
* Problemen met meer dan twee klassen (meerdere klasse-indeling)

Azure Machine Learning heeft verschillende modules toodeal met elk van deze typen van classificatie, maar Hallo methoden voor het interpreteren van de resultaten van hun voorspelling vergelijkbaar zijn.

### <a name="two-class-classification"></a>Classificatie van de twee-klasse
**Voorbeeld experiment**

Een voorbeeld van een tweeklasse klassificatieprobleem is Hallo classificatie van iris bloemen. Hallo-taak is tooclassify iris bloemen op basis van hun functies. Hallo Iris gegevensset vindt u in Azure Machine Learning is een subset van populaire Hallo [Iris gegevensset](http://en.wikipedia.org/wiki/Iris_flower_data_set) exemplaren van die alleen de twee bloem soorten (klassen 0 en 1). Er zijn vier functies voor elke bloem (sepal breedte sepal lengte Bloemblad lengte en Bloemblad breedte).

![Schermopname van iris experiment](./media/machine-learning-interpret-model-results/1.png)

Afbeelding 1. IRIS tweeklasse classificatie probleem experiment

Een experiment is uitgevoerd toosolve dit probleem, zoals wordt weergegeven in afbeelding 1. Een tweeklasse gestimuleerd besluit structuur model is getraind en berekend. Nu kunt u Hallo voorspelling resultaten van Hallo visualiseren [Score Model] [ score-model] module door te klikken op de uitvoerpoort Hallo Hallo [Score Model] [ score-model]module en vervolgens te klikken op **Visualize**.

![De module score model](./media/machine-learning-interpret-model-results/1_1.png)

Hiermee wordt Hallo score berekenen resultaten zoals in afbeelding 2.

![Resultaten van iris tweeklasse classificatie experiment](./media/machine-learning-interpret-model-results/2.png)

Afbeelding 2. Een resultaat score-model in twee klasse classificatie visualiseren

**Resultaat interpretatie**

Er zijn zes kolommen in tabel met Hallo resultaten. Hallo links vier kolommen zijn Hallo vier functies. Hallo rechts twee kolommen, Scored Labels en kansen berekend zijn Hallo voorspelling resultaten. Hallo berekend kansen kolom bevat Hallo kans dat een bloem toohello positief class (klasse 1) behoort. Bijvoorbeeld, Hallo eerste nummer in Hallo kolom (0.028571) wordt aangegeven dat er 0.028571 kans dat eerste bloem Hallo tooClass 1 behoort. Hallo Scored Labels kolom bevat Hallo voorspelde klasse voor elke bloem. Dit is gebaseerd op Hallo berekend kansen kolom. Als de kans op een bloem berekend Hallo groter is dan 0,5, wordt het voorspeld als klasse 1. Anders wordt deze als klasse 0 voorspeld.

**Publicatie van de Web service**

Nadat het Hallo voorspelling resultaten zijn begrepen en geluid beoordeeld, kan hello experiment worden gepubliceerd als een webservice zodat u kunt deze in verschillende toepassingen implementeren en tooobtain klasse voorspellingen voor elke nieuwe iris bloem aanroepen. toolearn hoe toochange een training in een score experiment experimenteren en publiceren als een webservice, Zie [hello Azure Machine Learning-webservice publiceert](machine-learning-walkthrough-5-publish-web-service.md). Deze procedure biedt u een experiment scoreprofiel zoals in afbeelding 3.

![Schermopname van het experiment score berekenen](./media/machine-learning-interpret-model-results/3.png)

Afbeelding 3. Score berekenen Hallo iris tweeklasse classificatie probleem experiment

Nu moet u tooset Hallo invoer en uitvoer voor Hallo-webservice. Hallo-invoer is Hallo rechteruitvoerpoort van [Score Model][score-model], die is Hallo Iris bloem functies invoer. Hallo keuze van Hallo uitvoer is afhankelijk van of u geïnteresseerd bent in Hallo voorspeld klasse (scored label), Hallo berekend kans of beide. In dit voorbeeld wordt ervan uitgegaan dat u geïnteresseerd in beide bent. Hallo tooselect gewenst uitvoerkolommen, gebruik een [kolommen in gegevensset selecteren] [ select-columns] module. Klik op [kolommen in gegevensset selecteren][select-columns], klikt u op **Launch column selector**, en selecteer **Scored Labels** en **berekend kansen**. Na het instellen van de uitvoerpoort Hallo van [kolommen in gegevensset selecteren] [ select-columns] en opnieuw wordt uitgevoerd, moet u gereed toopublish hello scoreprofiel experiment als een webservice door te klikken op **PUBLISH WEB SERVICE**. Hallo laatste experiment ziet er afbeelding 4.

![Hallo iris tweeklasse classificatie experiment](./media/machine-learning-interpret-model-results/4.png)

Afbeelding 4. Laatste scoreprofiel experiment van een tweeklasse classificatie iris probleem

Nadat u Hallo-webservice wordt uitgevoerd en voer de waarden van bepaalde functie van een exemplaar van de test, resultaat Hallo bestaat uit twee getallen. Hallo eerste getal Hallo label berekend en Hallo tweede Hallo kansdichtheidsfunctie berekend. Deze bloem wordt voorspeld als klasse 1 met 0.9655 kans.

![Test interpreteren score-model](./media/machine-learning-interpret-model-results/4_1.png)

![Score berekenen testresultaten](./media/machine-learning-interpret-model-results/5.png)

Afbeelding 5. Resultaat van de Web service van iris tweeklasse classificatie

### <a name="multi-class-classification"></a>Meerdere klasse-classificatie
**Voorbeeld experiment**

In dit experiment voert u een taak letter erkenning als voorbeeld voor multiklassen classificatie. Hallo classificatie probeert toopredict een bepaalde letter (klasse) op basis van enkele hand geschreven kenmerkwaarden opgehaald uit Hallo hand geschreven installatiekopieën.

![Voorbeeld van de letter erkenning](./media/machine-learning-interpret-model-results/5_1.png)

In Hallo trainingsgegevens zijn er 16 functies opgehaald uit de letter hand geschreven installatiekopieën. Hallo 26 letters vormen onze 26 klassen. Afbeelding 6 ziet een experiment die een multiklassen classificatie wordt train model voor letter opname en voorspelt op Hallo dezelfde functie op een test-gegevensset.

![Letter erkenning multiklassen classificatie experiment](./media/machine-learning-interpret-model-results/6.png)

Afbeelding 6. Letter erkenning multiklassen classificatie probleem experiment

Hallo-resultaten van Hallo visualiseren [Score Model] [ score-model] module door te klikken op de uitvoerpoort Hallo van [Score Model] [ score-model] module en vervolgens te klikken op **Visualize**, ziet u inhoud zoals in afbeelding 7.

![Resultaten van score-model](./media/machine-learning-interpret-model-results/7.png)

Afbeelding 7. Scoreresultaten visualiseren model in een klasse met meerdere categorie

**Resultaat interpretatie**

Hallo links 16 kolommen vertegenwoordigen Hallo functie waarden van Hallo testset. Hallo-kolommen met de namen zijn berekend kansen voor de klasse 'XX' net als Hallo berekend kansen kolom in geval van Hallo twee-klasse. Geven ze Hallo-kans dat de bijbehorende vermelding Hallo worden onderverdeeld in een bepaalde klasse. Voor het eerste item hello is er bijvoorbeeld 0.003571 waarschijnlijkheid aan dat dit een 'A,' 0.000451 waarschijnlijkheid aan dat het een "B", enzovoort. Hallo laatste kolom (Scored Labels) is hetzelfde als Scored Labels in geval van Hallo tweeklasse Hallo. Deze klasse met de grootste kans berekend als voorspelde klasse van de bijbehorende vermelding Hallo HALLO hallo Hallo geselecteerd. Voor het eerste item hello is Hallo label berekend bijvoorbeeld 'F' omdat het Hallo grootste kans toobe een 'F' (0.916995) heeft.

**Publicatie van de Web service**

U kunt ook Hallo label berekend voor elke vermelding en Hallo kans Hallo berekend label ophalen. Hallo basislogica is toofind Hallo grootste kans tussen alle Hallo kansen berekend. toodo, moet u toouse hello [R-Script uitvoeren] [ execute-r-script] module. Hallo R code wordt weergegeven in afbeelding 8 en Hallo resultaat van het Hallo-experiment wordt weergegeven in afbeelding 9.

![R-codevoorbeeld](./media/machine-learning-interpret-model-results/8.png)

Afbeelding 8. R-code voor het uitpakken van Scored Labels en Hallo waarschijnlijkheid van Hallo-labels die is gekoppeld

![Experiment resultaat](./media/machine-learning-interpret-model-results/9.png)

Afbeelding 9. Laatste scoreprofiel experiment van Hallo letter erkenning multiklassen classificatie probleem

Nadat u publiceren en Hallo-webservice wordt uitgevoerd en voer de waarden van bepaalde functie gebruikersinvoer, geretourneerd Hallo resultaat lijkt erop afbeelding 10. Deze brief hand geschreven met de uitgepakte 16 functies is voorspelde toobe "H" met 0.9715 kans.

![Testmodule interpreteren score](./media/machine-learning-interpret-model-results/9_1.png)

![Testresultaat](./media/machine-learning-interpret-model-results/10.png)

Afbeelding 10. Resultaat van de Web service van multiklassen classificatie

## <a name="regression"></a>Regressie
Regressie problemen worden verschillende problemen met de classificatie. U probeert een probleem classificatie toopredict discrete klassen, zoals welke klasse een bloem iris behoort. Maar zoals u in het volgende voorbeeld van een probleem regressie hello ziet, probeert u een continue variabele zijn, zoals Hallo prijs van een auto toopredict.

**Voorbeeld experiment**

Auto's voorspellen gebruiken als uw voorbeeld voor regressie. U probeert toopredict Hallo prijs van een auto op basis van de functies, zoals maken, brandstoftype, hoofdtekst en station wheel. Hallo-experiment wordt weergegeven in afbeelding 11.

![Auto prijs regressie-experiment](./media/machine-learning-interpret-model-results/11.png)

Afbeelding 11. Auto prijs regressie probleem experiment

Hallo visualiseren [Score Model] [ score-model] module Hallo resultaat ziet eruit als afbeelding 12.

![Resultaten van score berekenen voor auto prijs voorspelling probleem](./media/machine-learning-interpret-model-results/12.png)

Afbeelding 12. Score berekenen voor resultaat voor Hallo auto prijs voorspelling probleem

**Resultaat interpretatie**

Scored Labels is Hallo resultatenkolom in deze scoreprofiel resultaat. Hallo-nummers zijn Hallo voorspelde prijs voor elke auto.

**Publicatie van de Web service**

U kunt publiceren Hallo regressie-experiment in een web-service en deze aanroepen voor auto's voorspellen in Hallo dezelfde manier als in Hallo tweeklasse classificatie gebruiksvoorbeeld.

![Score berekenen voor experiment voor auto prijs regressie probleem](./media/machine-learning-interpret-model-results/13.png)

Afbeelding 13. Score berekenen experiment van een auto prijs regressie probleem

Met de webservice hello, hello resultaat lijkt erop afbeelding 14 geretourneerd. Hallo voorspelde prijs voor deze auto is $15,085.52.

![Interpreteren scoremodule testen](./media/machine-learning-interpret-model-results/13_1.png)

![Resultaten van de module score berekenen](./media/machine-learning-interpret-model-results/14.png)

Afbeelding 14. Web service resultaat van een auto prijs regressie probleem

## <a name="clustering"></a>Clustering
**Voorbeeld experiment**

We gebruiken Hallo Iris gegevensset opnieuw toobuild een clustering experiment. Hier kunt u filteren uit Hallo klasse labels in de gegevensset Hallo zodat deze alleen functies en kan worden gebruikt voor clustering. In deze iris gebruiksvoorbeeld, het aantal clusters toobe twee tijdens Hallo training, wat betekent dat u Hallo bloemen zou clusteren in de twee klassen Hallo opgeven. Hallo-experiment wordt weergegeven in afbeelding 15.

![Clustering probleem iris experimenteren](./media/machine-learning-interpret-model-results/15.png)

Afbeelding 15. Clustering probleem iris experimenteren

Clustering verschilt van de classificatie in die set trainingsgegevens Hallo geen compleet waarheid labels op zichzelf. Clustering groepen Hallo training gegevensset instanties in verschillende clusters. Tijdens het Hallo training Hallo Hallo modellabels vermeldingen door te leren Hallo verschillen tussen hun functies. Daarna Hallo getrainde model kan worden gebruikt toofurther toekomstige classificeren. Er zijn twee onderdelen van Hallo resultaat die we geïnteresseerd in het binnen een clustering probleem bent. het eerste deel Hallo is set trainingsgegevens Hallo labels en Hallo tweede classificeert een nieuwe gegevensset met Hallo getrainde model.

Hallo eerste deel van Hallo resultaat kan worden weergegeven door te klikken op de uitvoerpoort van links Hallo [Clustering Train-Model] [ train-clustering-model] en vervolgens te klikken op **Visualize**. Hallo visualisatie wordt weergegeven in afbeelding 16.

![Clustering resultaat](./media/machine-learning-interpret-model-results/16.png)

Afbeelding 16. Resultaat van een set trainingsgegevens Hallo clustering visualiseren

Hallo resultaat van het tweede gedeelte hello, nieuwe vermeldingen met Hallo getraind clustering-model, clustering wordt weergegeven in afbeelding 17.

![Clustering resultaat visualiseren](./media/machine-learning-interpret-model-results/17.png)

Afbeelding 17. Resultaat van een nieuwe gegevensset clustering visualiseren

**Resultaat interpretatie**

Hoewel het Hallo-resultaten van Hallo twee onderdelen voortvloeien uit verschillende experiment fasen, ze zoeken Hallo dezelfde en worden geïnterpreteerd in Hallo dezelfde manier. Hallo zijn eerste vier kolommen functies. Hallo laatste kolom toewijzingen is Hallo voorspelling resultaat. Hallo vermeldingen toegewezen Hallo hetzelfde nummer worden voorspeld toobe in Hallo dezelfde, dat wil zeggen clusteren, ze delen overeenkomsten op een bepaalde manier (Hallo standaard Euclidean afstand metric dit experiment gebruikt). Omdat u het aantal clusters toobe 2 Hallo hebt opgegeven, worden de Hallo vermeldingen in de toewijzingen label 0 of 1.

**Publicatie van de Web service**

U kunt publiceren Hallo clustering experiment in een web-service en deze aanroepen voor clustering voorspellingen Hallo dezelfde manier als in Hallo tweeklasse classificatie gebruiksvoorbeeld.

![Score berekenen voor experiment voor iris clustering probleem](./media/machine-learning-interpret-model-results/18.png)

Afbeelding 18. Score berekenen experiment van een iris clustering probleem

Hallo geretourneerd na het uitvoeren van de webservice hello, resultaat lijkt erop afbeelding 19. Deze bloem is voorspelde toobe in cluster 0.

![Test scoremodule interpreteren](./media/machine-learning-interpret-model-results/18_1.png)

![Resultaat van de module score berekenen](./media/machine-learning-interpret-model-results/19.png)

Afbeelding 19. Resultaat van de Web service van iris tweeklasse classificatie

## <a name="recommender-system"></a>Recommender systeem
**Voorbeeld experiment**

Voor recommender systemen, kunt u Hallo restaurant aanbeveling probleem als een voorbeeld: u kunt restaurant aanbevelen voor klanten op basis van de geschiedenis van hun classificatie. Hallo invoergegevens bestaat uit drie delen:

* Beoordelingen van klanten restaurant
* Functie klantgegevens
* Gegevens van de functie restaurant

Er zijn verschillende dingen die we met Hallo doen kunt [Train Matchbox Recommender] [ train-matchbox-recommender] -module in Azure Machine Learning:

* De classificaties voor een bepaalde gebruiker en het item te voorspellen
* Items tooa toegekend aan het beste
* Zoeken naar gebruikers gerelateerde tooa opgegeven gebruiker
* Verwante items-tooa opgegeven item zoeken

U kunt u de gewenste toodo door te selecteren in Hallo vier opties in Hallo **Recommender voorspelling soort** menu. Hier kunt u alle vier scenario's doorlopen.

![Matchbox recommender](./media/machine-learning-interpret-model-results/19_1.png)

Een typische Azure Machine Learning-experiment voor een systeem recommender eruit als afbeelding 20. Voor informatie over hoe toouse die aanbevelingsmodules system zien [Train matchbox recommender] [ train-matchbox-recommender] en [Score matchbox recommender] [ score-matchbox-recommender].

![Recommender system experiment](./media/machine-learning-interpret-model-results/20.png)

Afbeelding 20. Recommender system experiment

**Resultaat interpretatie**

**De classificaties voor een bepaalde gebruiker en het item te voorspellen**

Door het selecteren van **classificatie voorspelling** onder **Recommender voorspelling soort**, vraagt u Hallo recommender system toopredict Hallo classificatie voor een bepaalde gebruiker en het item. visualisatie van Hallo Hallo [Score Matchbox Recommender] [ score-matchbox-recommender] uitvoer ziet eruit als afbeelding 21.

![Resultaat van Hallo recommender system--classificatie voorspelling beoordelen](./media/machine-learning-interpret-model-results/21.png)

Afbeelding 21. Hallo score resultaat van Hallo recommender system--classificatie voorspelling visualiseren

de eerste twee kolommen Hallo zijn de Hallo-item voor gebruikersgegevens paren geleverd door Hallo invoergegevens. de derde kolom Hallo is Hallo voorspelde score van een gebruiker voor een bepaald onderdeel. Bijvoorbeeld, in de eerste rij hello voorspelde klant die u1048 is toorate restaurant 135026 als 2.

**Items tooa toegekend aan het beste**

Door het selecteren van **aanbeveling Item** onder **Recommender voorspelling soort**, vraagt u Hallo recommender system toorecommend items tooa toegekend. Hallo laatste parameter toochoose in dit scenario is *item selectie aanbevolen*. Hallo optie **van beoordeeld-Items (voor de evaluatie van het model)** is voornamelijk bedoeld voor evaluatie Hallo training tijdens model. Voor deze fase voorspelling kiest **van alle Items**. visualisatie van Hallo Hallo [Score Matchbox Recommender] [ score-matchbox-recommender] uitvoer ziet eruit als afbeelding 22.

![Resultaat van het systeem recommender--aanbeveling item beoordelen](./media/machine-learning-interpret-model-results/22.png)

Afbeelding 22. Resultaat van de score van Hallo recommender system--aanbeveling item visualiseren

Hallo eerste Hallo zes kolommen vertegenwoordigt Hallo gegeven toorecommend items voor gebruikersgegevens-id's, zoals bepaald door de invoergegevens Hallo. Hallo vertegenwoordigen andere vijf kolommen Hallo items aanbevolen toohello gebruiker in aflopende volgorde van belang. Bijvoorbeeld, in de eerste rij hello aanbevolen Hallo meest restaurant voor klant U1048 is 134986, gevolgd door 135018, 134975 135021 en 132862.

**Zoeken naar gebruikers gerelateerde tooa opgegeven gebruiker**

Door het selecteren van **gerelateerde gebruikers** onder **Recommender voorspelling soort**, vraagt u Hallo recommender systeemgebruiker toofind gerelateerde gebruikers tooa gegeven. Verwante gebruikers Hallo gebruikers zijn die vergelijkbaar voorkeuren hebben. Hallo laatste parameter toochoose in dit scenario is *gebruikersselectie gerelateerde*. Hallo optie **van gebruikers dat beoordeeld artikelen (voor het model evaluatie)** is voornamelijk bedoeld voor evaluatie Hallo training tijdens model. Kies **van alle gebruikers** voor deze fase van de voorspelling. visualisatie van Hallo Hallo [Score Matchbox Recommender] [ score-matchbox-recommender] uitvoer ziet eruit als afbeelding 23.

![Resultaat van de score van recommender system--gerelateerde gebruikers](./media/machine-learning-interpret-model-results/23.png)

Afbeelding 23. Scoreresultaten visualiseren van Hallo recommender systeem--gerelateerde gebruikers

eerst Hallo Hallo zes kolommen bevat Hallo opgegeven gebruikers-id's die nodig zijn toofind gerelateerde gebruikers, zoals bepaald door de invoergegevens. Hallo andere store vijf kolommen Hallo voorspelde gerelateerde gebruikers van de gebruiker Hallo in aflopende volgorde van belang. In de eerste rij hello is de meest relevante klant Hallo voor klant U1048 bijvoorbeeld U1051, gevolgd door U1066, U1044 U1017 en U1072.

**Verwante items-tooa opgegeven item zoeken**

Door het selecteren van **verwante Items** onder **Recommender voorspelling soort**, vraagt u Hallo recommender system toofind verwante items tooa opgegeven item. Gerelateerde items zijn Hallo items waarschijnlijk toobe bevallen door Hallo dezelfde gebruiker. Hallo laatste parameter toochoose in dit scenario is *gerelateerd item selectie*. Hallo optie **van beoordeeld-Items (voor de evaluatie van het model)** is voornamelijk bedoeld voor evaluatie Hallo training tijdens model. We kiezen **van alle Items** voor deze fase van de voorspelling. visualisatie van Hallo Hallo [Score Matchbox Recommender] [ score-matchbox-recommender] uitvoer ziet eruit als afbeelding 24.

![Resultaat van de score van recommender system--verwante items](./media/machine-learning-interpret-model-results/24.png)

Afbeelding 24. Scoreresultaten visualiseren van Hallo recommender systeem--verwante items

eerste Hallo zes kolommen vertegenwoordigt Hallo item-id's die nodig zijn gegeven Hallo toofind verwante objecten, zoals bepaald door de invoergegevens Hallo. Hallo andere store vijf kolommen Hallo voorspelde verwante items van Hallo item in aflopende volgorde in termen van belang. In de eerste rij hello is de meest relevante artikel Hallo voor artikel 135026 bijvoorbeeld 135074, gevolgd door 135035, 132875 135055 en 134992.

**Publicatie van de Web service**

Hallo-proces voor het publiceren van deze experimenten als web services tooget voorspellingen lijkt voor elk van de vier Hallo-scenario's. We nemen hier Hallo tweede scenario (aanbevolen items tooa toegekend aan) als voorbeeld. Volg dezelfde procedure Hallo Hello andere drie.

Opslaan Hallo recommender systeem als een getraind model getraind en filteren Hallo invoergegevens tooa één gebruiker-ID-kolom als aangevraagd, kunt u aansluiten Hallo experiment zoals in afbeelding 25 en publiceren als een webservice.

![Score berekenen experiment van Hallo restaurant aanbeveling probleem](./media/machine-learning-interpret-model-results/25.png)

Afbeelding 25. Score berekenen experiment van Hallo restaurant aanbeveling probleem

Met de webservice hello, hello resultaat lijkt erop afbeelding 26 geretourneerd. Hallo vijf aanbevolen restaurant voor gebruiker U1048 zijn 134986, 135018 134975, 135021 en 132862.

![Voorbeeld van recommender systeemservice](./media/machine-learning-interpret-model-results/25_1.png)

![Voorbeeldresultaten experiment](./media/machine-learning-interpret-model-results/26.png)

Afbeelding 26. Resultaat van de Web service restaurant aanbeveling probleem

<!-- Module References -->
[assign-to-clusters]: https://msdn.microsoft.com/library/azure/eed3ee76-e8aa-46e6-907c-9ca767f5c114/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-matchbox-recommender]: https://msdn.microsoft.com/library/azure/55544522-9a10-44bd-884f-9a91a9cec2cd/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-clustering-model]: https://msdn.microsoft.com/library/azure/bb43c744-f7fa-41d0-ae67-74ae75da3ffd/
[train-matchbox-recommender]: https://msdn.microsoft.com/library/azure/fa4aa69d-2f1c-4ba4-ad5f-90ea3a515b4c/
