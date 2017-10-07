---
title: 'Stap 4: Trainen en evalueren van voorspellende analytische modellen Hallo | Microsoft Docs'
description: 'Stap 4 van Hallo een overzicht van de voorspellende oplossing ontwikkelen: trein, beoordelen en evalueren van meerdere modellen in Azure Machine Learning Studio.'
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a>Scenario-stap 4: Trainen en evalueren Hallo voorspellende analytische modellen
Dit onderwerp bevat Hallo vierde stap van Hallo scenario [predictive analytics-oplossing in Azure Machine Learning ontwikkelen](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Een Machine Learning-werkruimte maken](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Bestaande gegevens uploaden](machine-learning-walkthrough-2-upload-data.md)
3. [Een nieuw experiment maken](machine-learning-walkthrough-3-create-new-experiment.md)
4. **Trainen en evalueren Hallo modellen**
5. [Hallo-webservice implementeren](machine-learning-walkthrough-5-publish-web-service.md)
6. [Toegang tot Hallo-webservice](machine-learning-walkthrough-6-access-web-service.md)

- - -
Een van de voordelen van het gebruik van Azure Machine Learning Studio voor het maken van machine learning-modellen Hallo Hallo mogelijkheid tootry meer dan één type model is op een tijd in een enkel experiment en vergelijk Hallo resultaten. Dit type experimenteren kunt u de beste oplossing Hallo vinden voor uw probleem.

Hallo-experiment we in dit overzicht ontwikkelt, we twee verschillende soorten modellen maken en vervolgens welk algoritme vergelijken hun scoreprofiel resultaten toodecide willen we toouse in onze laatste experiment.  

Er zijn verschillende modellen die we kan kiezen uit. toosee hello modellen die beschikbaar is, vouw Hallo **Machine Learning** knooppunt in het modulepalet hello, en vouw vervolgens **Model initialiseren** en Hallo knooppunten eronder. Voor Hallo toepassing van dit experiment, selecteren we Hallo [Two-Class ondersteuning Vectormachine] [ two-class-support-vector-machine] (SVM) en Hallo [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] modules.    

> [!TIP]
> help van tooget beslist welke Machine Learning-algoritme beste tegemoetkomt aan Hallo bepaald probleem probeert u toosolve, Zie [hoe toochoose algoritmen voor Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).
> 
> 

## <a name="train-hello-models"></a>Hallo modellen trainen

We voegen toe beide Hallo [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] module en [Two-Class ondersteuning Vectormachine] [ two-class-support-vector-machine] module in dit experiment.

### <a name="two-class-boosted-decision-tree"></a>Two-Class gestimuleerd beslissingsstructuur

Eerst laten we instellen Hallo boosted decision tree model.

1. Hallo zoeken [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] -module in het modulepalet hello en sleep deze naar Hallo canvas.

2. Hallo zoeken [Train Model] [ train-model] -module, sleep deze naar het canvas Hallo en sluit vervolgens Hallo uitvoer Hallo [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree]module toohello links invoerpoort Hallo [Train Model] [ train-model] module.
   
   Hallo [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] module initialiseert de algemene model Hallo en [Train Model] [ train-model] trainingsgegevens gebruikt tootrain Hallo-model. 

3. Verbinding maken met de Hallo links uitvoer van Hallo links [R-Script uitvoeren] [ execute-r-script] module toohello rechts invoer poort Hallo [Train Model] [ train-model] module (we besloten [stap 3](machine-learning-walkthrough-3-create-new-experiment.md) van deze stapsgewijze Kennismaking toouse Hallo gegevens afkomstig zijn van de linkerkant van Hallo Split Data-module voor training Hallo).
   
   > [!TIP]
   > We hebben twee Hallo invoer en een van de uitvoer Hallo Hallo [R-Script uitvoeren] [ execute-r-script] -module voor dit experiment, zodat we kunt ze niet-gekoppelde laten. 
   > 
   > 

Dit gedeelte van het Hallo-experiment ziet nu er ongeveer als volgt:  

![Een model trainen][1]

Nu tootell hello moet [Train Model] [ train-model] module dat we Hallo model toopredict Hallo kredietrisico waarde wilt bepalen.

1. Selecteer Hallo [Train Model] [ train-model] module. In Hallo **eigenschappen** deelvenster, klikt u op **Launch column selector**.

2. In Hallo **één kolom selecteren** dialoogvenster Typ 'kredietrisico' hello zoekveld opgegeven onder **beschikbare kolommen**'Kredietrisico' hieronder selecteert en klikt u op de pijlknop-rechts hello ( **>** ) toomove 'Kredietrisico' te**geselecteerde kolommen**. 

    ![Hallo kredietrisico kolom voor Hallo Train Model-module selecteren][0]

3. Klik op Hallo **OK** selectievakje is ingeschakeld.

### <a name="two-class-support-vector-machine"></a>Two-Class Support Vector Machine

Vervolgens stelt Hallo SVM model.  

Eerste, uitleg over SVM. Gestimuleerd beslissingsstructuren werken goed met functies van elk type. Aangezien Hallo SVM module een lineaire classificatie genereert, Hallo model die wordt gegenereerd heeft echter aanbevolen testfout Hallo wanneer alle functies van de numerieke Hallo hebt dezelfde schaal. alle numerieke tooconvert functies toohello dezelfde schalen, gebruiken we een 'Tanh' transformatie (Hello [gegevens normaliseren] [ normalize-data] module). Hiermee transformeert onze cijfers in bereik Hallo [0,1]. Hallo SVM module converteert tekenreeks functies toocategorical functies en onderdelen toobinary 0/1, zodat we niet nodig toomanually transformeert u functies van de tekenreeks. Bovendien we willen tootransform Hallo kredietrisico kolom (kolom 21) niet - numerieke is, maar het is Hallo waarde we je training Hallo model toopredict, dus moeten we er tooleave deze alleen.  

tooset up Hallo SVM model, Hallo te volgen:

1. Hallo zoeken [Two-Class ondersteuning Vectormachine] [ two-class-support-vector-machine] -module in het modulepalet hello en sleep deze naar Hallo canvas.

2. Met de rechtermuisknop op Hallo [Train Model] [ train-model] -module, selecteer **kopie**, klik met de rechtermuisknop op het canvas Hallo en selecteer **plakken**. kopie van Hallo Hallo [Train Model] [ train-model] module Hallo heeft dezelfde kolom selecteren als de oorspronkelijke Hallo.

3. Verbinding maken met uitvoer Hallo Hallo [Two-Class ondersteuning Vectormachine] [ two-class-support-vector-machine] module toohello links invoerpoort Hallo tweede [Train Model] [ train-model] module.

4. Hallo zoeken [gegevens normaliseren] [ normalize-data] module en sleep deze naar Hallo canvas.

5. Verbinding maken met de Hallo links uitvoer van Hallo links [R-Script uitvoeren] [ execute-r-script] module-invoer toohello van deze module (Let op de uitvoerpoort Hallo van een module mogelijk verbonden toomore dan een andere module).

6. Hallo links uitvoerpoort Hallo verbinding [gegevens normaliseren] [ normalize-data] module toohello rechts poort Hallo tweede invoer [Train Model] [ train-model] module.

Dit gedeelte van onze experiment moet nu als volgt uitzien:  

![Training Hallo tweede model][2]  

Nu configureren Hallo [gegevens normaliseren] [ normalize-data] module:

1. Klik op tooselect hello [gegevens normaliseren] [ normalize-data] module. In Hallo **eigenschappen** deelvenster **Tanh** voor Hallo **transformatiemethode** parameter.

2. Klik op **Launch column selector**, "Geen kolommen" Selecteer voor **begint met**, selecteer **opnemen** Selecteer in de eerste vervolgkeuzelijst Hallo **kolomtype**in Hallo tweede vervolgkeuzelijst en selecteer **numerieke** Hallo derde vervolgkeuzelijst. Hiermee wordt aangegeven dat alle Hallo numerieke kolommen (en alleen numerieke) worden getransformeerd.

3. Klik op Hallo toohello rechts van deze rij plusteken (+): Hiermee maakt u een rij van vervolgkeuzelijsten. Selecteer **uitsluiten** Selecteer in de eerste vervolgkeuzelijst Hallo **kolomnamen** in Hallo tweede vervolgkeuzelijst en voer 'Kredietrisico' in hello tekstveld. Hiermee wordt aangegeven dat Hallo kredietrisico kolom moet worden genegeerd (moeten we dit omdat deze kolom numerieke en in dat geval zou worden omgezet als we deze niet uitsluit toodo).

4. Klik op Hallo **OK** selectievakje is ingeschakeld.  

    ![Selecteer kolommen voor Hallo normaliseren Data-module][5]

Hallo [gegevens normaliseren] [ normalize-data] -module is nu ingesteld tooperform een transformatie Tanh voor alle numerieke kolommen, met uitzondering van Hallo kredietrisico kolom.  

## <a name="score-and-evaluate-hello-models"></a>Beoordelen en evalueren Hallo modellen

We gebruiken Hallo gegevens die uit is gescheiden door Hallo testen [Split Data] [ split] module tooscore onze getraind modellen. Vervolgens kunnen we vergelijken Hallo resultaten van het twee modellen toosee hello, die betere resultaten gegenereerd.  

### <a name="add-hello-score-model-modules"></a>Hallo Score Model modules toevoegen

1. Hallo zoeken [Score Model] [ score-model] module en sleep deze naar Hallo canvas.

2. Verbinding maken met de Hallo [Train Model] [ train-model] module die is verbonden toohello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] module toohello links-invoer poort Hallo [Score Model] [ score-model] module.

3. Verbinding maken met de Hallo rechts [R-Script uitvoeren] [ execute-r-script] module (onze testgegevens) toohello rechts invoer poort Hallo [Score Model] [ score-model] module.

    ![Module score-Model verbonden][6]
   
   Hallo [Score Model] [ score-model] module kunt nu Hallo tegoed informatie uit Hallo gegevens, voert u via het Hallo-model te testen en vergelijken Hallo voorspellingen Hallo model Hello werkelijke genereert kredietrisico kolom in Hallo gegevens testen.

4. Kopieer en plak Hallo [Score Model] [ score-model] module toocreate een tweede kopie.

5. Verbinding maken met uitvoer Hallo van Hallo SVM model (dat wil zeggen, Hallo uitvoerpoort Hallo [Train Model] [ train-model] module die is verbonden toohello [Two-Class ondersteuning Vectormachine] [ two-class-support-vector-machine] module) toohello poort Hallo tweede invoer [Score Model] [ score-model] module.

6. We hebben toodo Hallo dezelfde transformatie toohello testgegevens zoals we hebben gedaan toohello trainingsgegevens voor Hallo SVM model. Dus kopieer en plak Hallo [gegevens normaliseren] [ normalize-data] module toocreate een tweede exemplaar en verbind deze toohello rechts [R-Script uitvoeren] [ execute-r-script] module.

7. Hallo links uitvoer Hallo tweede verbinding [gegevens normaliseren] [ normalize-data] module toohello rechts poort Hallo tweede invoer [Score Model] [ score-model] module.

    ![Beide Score Model modules verbonden][7]

### <a name="add-hello-evaluate-model-module"></a>De module Evaluate Model Hallo toevoegen

tooevaluate Hallo twee resultaten van score berekenen en deze te vergelijken, gebruiken we een [Evaluate Model] [ evaluate-model] module.  

1. Hallo zoeken [Evaluate Model] [ evaluate-model] module en sleep deze naar Hallo canvas.

2. Verbinding maken met de uitvoerpoort Hallo Hallo [Score Model] [ score-model] module die is gekoppeld aan Hallo boosted decision tree model toohello links invoer poort Hallo [Evaluate Model] [ evaluate-model] module.

3. Verbinding maken met andere Hallo [Score Model] [ score-model] module toohello rechts invoer poort.  

    ![Model evalueren module verbonden][8]

### <a name="run-hello-experiment-and-check-hello-results"></a>Hallo-experiment uitvoeren en Hallo resultaten controleren

toorun experiment hello, klikt u op Hallo **uitvoeren** knop onder Hallo canvas. Het kan enkele minuten duren. Een draaiende indicator voor elke module ziet u dat deze wordt uitgevoerd en wordt een groen vinkje weergegeven wanneer de module Hallo is voltooid. Wanneer alle Hallo-modules ingeschakeld zijn, is Hallo experiment voltooid.

Hallo-experiment moet nu als volgt uitzien:  

![Beide modellen evalueren][3]

toocheck hello resultaten, klik op de uitvoerpoort Hallo Hallo [Evaluate Model] [ evaluate-model] module en selecteer **Visualize**.  

Hallo [Evaluate Model] [ evaluate-model] module produceert een paar curven en metrische gegevens die u toelaten om toocompare Hallo resultaten van de twee scored modellen Hallo. U kunt Hallo resultaten als ontvanger Operator kenmerk (ROC) curven, curven precisie/intrekken of Lift curven weergeven. Aanvullende gegevens die worden weergegeven, bevat een matrix verwarring cumulatieve waarden voor Hallo gebied onder Hallo kromme (AUC) en andere metrische gegevens. U kunt Hallo drempelwaarde wijzigen door bewegende Hallo schuifregelaar naar links of rechts en Zie hoe het is van invloed op Hallo set van metrische gegevens.  

toohello rechts van de grafiek hello, klikt u op **berekend gegevensset** of **berekend gegevensset toocompare** toohighlight Hallo gekoppeld curve en toodisplay Hallo onderstaande metrische gegevens die is gekoppeld. In legenda Hallo voor Hallo curven toohello links invoerpoort Hallo 'Berekend gegevensset' overeen [Evaluate Model] [ evaluate-model] module - in ons geval dit Hallo boosted decision tree model is. 'Berekend gegevensset toocompare' komt overeen toohello rechteruitvoerpoort - Hallo SVM model in ons geval. Als u op een van deze labels, Hallo curve voor dit model is gemarkeerd en Hallo bijbehorende metrische gegevens worden weergegeven, zoals wordt weergegeven in de volgende afbeelding Hallo.  

![ROC curven voor modellen][4]

Door deze waarden in, kunt u beslissen welk model dichtstbijzijnde toogiving Hallo van resultaten die u zoekt. U kunt teruggaan en door het wijzigen van parameterwaarden Hallo verschillende modellen in uw experiment herhalen. 

Hallo wetenschappelijke en illustraties van deze resultaten te interpreteren en Hallo model prestaties afstemmen is buiten Hallo-bereik van deze rondleiding. Voor meer informatie kan u Hallo artikelen volgende lezen:
- [Hoe tooevaluate prestaties in Azure Machine Learning model](machine-learning-evaluate-model-performance.md)
- [Het kiezen van de parameters toooptimize uw algoritmen in Azure Machine Learning](machine-learning-algorithm-parameters-optimize.md)
- [Model resulteert in een Azure Machine Learning interpreteren](machine-learning-interpret-model-results.md)

> [!TIP]
> Telkens wanneer u een record van deze herhaling Hallo experiment uitvoeren wordt opgeslagen in Hallo geschiedenis uitvoeren. U kunt deze herhalingen zien en retourneren tooany, door te klikken op **weergave uitvoeren geschiedenis** hieronder Hallo canvas. U kunt ook klikken op **voorafgaande uitvoeren** in Hallo **eigenschappen** deelvenster tooreturn toohello herhaling voorafgaat Hallo een dat u hebt geopend.
> 
> U kunt een kopie van elke herhaling van uw experiment maken door te klikken op **SAVE AS** hieronder Hallo canvas. 
> Gebruik van het experiment Hallo **samenvatting** en **beschrijving** eigenschappen tookeep een record van wat u hebt geprobeerd in uw experimentherhalingen.
> 
> Zie voor meer informatie [experimentherhalingen in Azure Machine Learning Studio beheren](machine-learning-manage-experiment-iterations.md).  
> 
> 

- - -
**Volgende stap: [Hallo-webservice implementeren](machine-learning-walkthrough-5-publish-web-service.md)**

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
