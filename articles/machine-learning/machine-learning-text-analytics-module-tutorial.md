---
title: aaaCreate text analytics-modellen in Azure Machine Learning Studio | Microsoft Docs
description: Hoe toocreate tekstanalyse modellen in Azure Machine Learning Studio gebruik van modules voor voorverwerking van de tekst, N g of hash-functies
services: machine-learning
documentationcenter: 
author: rastala
manager: jhubbard
editor: 
ms.assetid: 08cd6723-3ae6-4e99-a924-e650942e461b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: roastala
ms.openlocfilehash: e3799f37ba54bb2ec8815ecf5ed34e145ffb20e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-text-analytics-models-in-azure-machine-learning-studio"></a>Tekstanalysemodellen maken in Azure Machine Learning Studio
U kunt Azure Machine Learning toobuild gebruiken en text analytics-modellen operationeel maken. Deze modellen kunt u, bijvoorbeeld document classificatie of gevoel analysis problemen oplossen.

Een text analytics-experiment zou u meestal:

1. Reinigen en tekst gegevensset voorverwerken
2. Numerieke functie vectoren extraheren uit tekst voorverwerkte
3. De classificatie- of regressiemodel model trainen
4. Beoordelen en Hallo model valideren
5. Hallo model tooproduction implementeren

In deze zelfstudie leert u deze stappen als we doorlopen een gevoel Analytics-model met Amazon adresboek beoordelingen gegevensset (Zie het onderzoeksrapport ' biografieën, Bollywood, giek vakken en Blenders: domein aanpassing voor gevoel classificatie ' door John Blitzer, Markeren Dredze en Fernando Pereira; Koppeling van rekenkundige Linguistics (ACL) 2007.) Deze gegevensset bestaat uit revisie scores (1-2 of 4 en 5) en vrije tekst. Hallo doel is toopredict Hallo revisie score: lage (1 - 2) of hoge (4-5).

U vindt in deze zelfstudie wordt besproken in Cortana Intelligence Gallery experimenten:

[Beoordelingen adresboek voorspellen](https://gallery.cortanaintelligence.com/Experiment/Predict-Book-Reviews-1)

[Adresboek beoordelingen - Voorspellend Experiment voorspellen](https://gallery.cortanaintelligence.com/Experiment/Predict-Book-Reviews-Predictive-Experiment-1)

## <a name="step-1-clean-and-preprocess-text-dataset"></a>Stap 1: Opschonen en tekst gegevensset voorverwerken
We eerst delen Hallo revisie scores categorische hoge en lage buckets tooformulate Hallo probleem als tweeklasse classificatie Hallo experiment. We gebruiken [metagegevens bewerken](https://msdn.microsoft.com/library/azure/dn905986.aspx) en [Categorische waarden](https://msdn.microsoft.com/library/azure/dn906014.aspx) modules.

![Label maken](./media/machine-learning-text-analytics-module-tutorial/create-label.png)

Vervolgens opschonen Hallo tekst met [voorverwerken tekst](https://msdn.microsoft.com/library/azure/mt762915.aspx) module. Hallo reinigen vermindert Hallo ruis in Hallo gegevensset, kunt u de belangrijkste functies van Hallo zoeken en verbeteren de nauwkeurigheid van het laatste model Hallo Hallo. We verwijderen stopwoorden - veelvoorkomende woorden zoals ' "of"a"- en getallen, speciale tekens, dubbele tekens, e-mailadressen en URL's. We ook Hallo tekst toolowercase converteren, lemmatize Hallo woorden en detecteren zin grenzen die vervolgens worden aangeduid met ' ||| ' symbool in voorverwerkte tekst.

![Tekst voorverwerken](./media/machine-learning-text-analytics-module-tutorial/preprocess-text.png)

Wat gebeurt er als u wilt dat een aangepaste lijst met stopwoorden toouse? U kunt in doorgeven als optionele invoer. U kunt ook aangepaste C# syntaxis van de reguliere expressie tooreplace subtekenreeksen gebruiken en verwijderen van woorden met spraak: woorden of termen bijvoeglijke naamwoorden.

Nadat Hallo voorverwerking voltooid is, we Hallo gegevens splitsen in train en sets testen.

## <a name="step-2-extract-numeric-feature-vectors-from-pre-processed-text"></a>Stap 2: Haal de numerieke functie vectoren uit voorverwerkte tekst
een model voor tekstgegevens toobuild, u hebben doorgaans tooconvert vrije tekst in numerieke functie vectoren. In dit voorbeeld gebruiken we [N-Gram-functies extraheren uit tekst](https://msdn.microsoft.com/library/azure/mt762916.aspx) module tootransform Hallo gegevens toosuch tekstindeling. Deze module wordt een kolom met witruimte gescheiden woorden en berekent een dictionary van woorden of N-grams van woorden die worden weergegeven in uw gegevensset. Vervolgens wordt dit geteld hoeveel keren elk woord of N-gram wordt weergegeven in elke record en functie vectoren maakt van de telt. In deze zelfstudie ingesteld we N-gram grootte too2, zodat onze vectoren functie enkele woorden en combinaties van de twee volgende woorden bevatten.

![N-grams extraheren](./media/machine-learning-text-analytics-module-tutorial/extract-ngrams.png)

We beginnen met TF toepassen * IDF (Term frequentie Inverse Document frequentie) weging tooN-gram telt. Deze aanpak wordt gewicht van woorden die vaak worden weergegeven in één record, maar door de volledige gegevensset Hallo zeldzame worden toegevoegd. Andere opties omvatten binair TF, en wegen grafiek.

Dergelijke tekstfuncties hebben vaak hoge dimensionaliteit. Bijvoorbeeld, als uw corpus 100.000 unieke woorden heeft, moet de ruimte van de functie 100.000 dimensies of meer als N g worden gebruikt. Hallo N-Gram-functies extraheren module biedt u een reeks opties tooreduce Hallo dimensionaliteit. U kunt tooexclude woorden die toohave korte of lange, of te vaak of te vaak waardevol voorspeld. We uitsluiten N-grams die worden weergegeven in minder dan 5 records of in meer dan 80% van de records in deze zelfstudie.

Bovendien kunt u functie selectie tooselect alleen de functies die Hallo meest zijn gecorreleerd met het doel-voorspelling. We gebruiken de chi-kwadraatverdeling functie selectie tooselect 1000 functies. U kunt Hallo vocabulaire van geselecteerde woorden of N-grams weergeven door te klikken op de juiste uitvoer Hallo van Extract N-gram-module.

Als een alternatieve methode toousing extraheren N-Gram-functies, kunt u hash-functies-module. Let echter [hash-functie](https://msdn.microsoft.com/library/azure/dn906018.aspx) heeft geen ingebouwde functie selectie mogelijkheden of TF * IDF weging.

## <a name="step-3-train-classification-or-regression-model"></a>Stap 3: De classificatie- of regressiemodel model trainen
Hallo-tekst is nu getransformeerde toonumeric functie kolommen. Hallo gegevensset bevat nog steeds tekenreekskolommen uit de vorige fasen, zodat we Select Columns in Dataset tooexclude gebruiken ze.

Vervolgens gebruiken we [Two-Class Logistic Regression](https://msdn.microsoft.com/library/azure/dn905994.aspx) toopredict onze doel: hoog of laag revisie score. Hallo text analytics probleem heeft op dit moment is omgezet in een normale klassificatieprobleem. U kunt Hallo beschikbare hulpprogramma's in Azure Machine Learning tooimprove Hallo-model gebruiken. U kunt bijvoorbeeld experimenteren met verschillende classificaties toofind hoe nauwkeurige resultaten ze geven of hyperparameter tooimprove Hallo nauwkeurigheid afstemmen gebruiken.

![Trein en Score](./media/machine-learning-text-analytics-module-tutorial/scoring-text.png)

## <a name="step-4-score-and-validate-hello-model"></a>Stap 4: Beoordelen en Hallo model valideren
Hoe wilt u het getrainde model Hallo valideren? We deze tegen Hallo testgegevensset te beoordelen en evalueren Hallo nauwkeurig. Hallo model geleerd echter Hallo vocabulaire van N-grams en hun gewichten uit Hallo training gegevensset. Daarom, moeten we die vocabulair en gemeenschappelijke die gewichten gebruiken bij het uitpakken van de functies van testgegevens, als toocreating Hallo woordenlijst opnieuw worden geboden. Daarom we toevoegen N-Gram-functies extraheren module toohello score berekenen vertakking van Hallo experiment Hallo uitvoer woordenlijst verbinding vanuit training vertakking en Hallo woordenlijst modus instellen tooread alleen-lezen. We ook uitschakelen Hallo N g filteren door de gebruiksfrequentie op Hallo minimale too1 exemplaar instellen en maximale too100% en Hallo Functieselectie uitschakelen.

Nadat hello tekstkolom in test gegevens zijn omgezet toonumeric functie kolommen, sluiten we Hallo tekenreeks kolommen uit de vorige fasen, zoals in training vertakking. Vervolgens gebruiken we Evaluate Model-module tooevaluate Hallo nauwkeurigheid en Score Model-module toomake voorspellingen.

## <a name="step-5-deploy-hello-model-tooproduction"></a>Stap 5: Hallo model tooproduction implementeren
Hallo-model is bijna klaar toobe geïmplementeerd tooproduction. Als geïmplementeerd als webservice, wordt tekst tekenreeks als invoer en retourneren een voorspelling 'hoog' of 'laag'. Hallo geleerd N-gram woordenlijst tootransform Hallo tekst toofeatures wordt gebruikt, en getraind logistic regression model toomake een voorspelling van deze functies. 

tooset up Hallo Voorspellend experiment we eerst opslaan Hallo N-gram woordenlijst als gegevensset en Hallo getraind regressiemodel logistic Hallo training vertakken van Hallo experiment. We Sla vervolgens een grafiek experiment voor Voorspellend experiment Hallo experiment met behulp van 'OpslaanAls' toocreate. We verwijderen Hallo Split Data-module en Hallo training vertakking uit Hallo experiment. We vervolgens verbinding eerder hebt opgeslagen Hallo N-gram vocabulair en model tooExtract N-Gram-functies en Score Model modules, respectievelijk. We ook verwijderen de module Evaluate Model Hallo.

We Select Columns in Dataset module voordat voorverwerken module tooremove Hallo label tekstkolom invoegen en schakel de optie 'Append score kolom toodataset' in de Module Score. Op die manier Hallo webservice aanvragen niet Hallo label probeert toopredict en biedt Hallo invoer functies in het antwoord niet echo.

![Voorspellend Experiment](./media/machine-learning-text-analytics-module-tutorial/predictive-text.png)

Nu hebben we een experiment die kan worden gepubliceerd als een webservice en kan worden aangeroepen met behulp van de reactie op aanvragen of batch uitvoering API's.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over tekst analytics modules uit [MSDN-documentatie](https://msdn.microsoft.com/library/azure/dn905886.aspx).

