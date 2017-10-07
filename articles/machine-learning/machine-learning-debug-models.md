---
title: aaaDebug uw Model in Azure Machine Learning | Microsoft Docs
description: Hoe toodebug fouten geproduceerd door Train Model en Score Model modules in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 629dc45e-ac1e-4b7d-b120-08813dc448be
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bradsev;garye
ms.openlocfilehash: ee38ca8ce38d4fc7add5ba70c80ab9bb2ceaf1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a>Fouten opsporen in uw model in Azure Machine Learning

Dit artikel wordt uitgelegd Hallo mogelijke redenen waarom een Hallo na twee fouten aangetroffen mogelijk bij het uitvoeren van een model:

* Hallo [Train Model] [ train-model] module, treedt een fout 
* Hallo [Score Model] [ score-model] module onjuiste resultaten oplevert 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a>Module Train-Model, treedt een fout

![image1](./media/machine-learning-debug-models/train_model-1.png)

Hallo [Train Model] [ train-model] Module verwacht twee invoeritems:

1. Hallo-type van machine learning-model uit Hallo-verzameling van modellen die worden geleverd door het Azure Machine Learning.
2. Hallo trainingsgegevens met een opgegeven labelkolom waarin Hallo variabele toopredict (hello andere kolommen wordt uitgegaan van toobe functies).

Deze module kan een fout in de volgende gevallen Hallo produceren:

1. Hallo labelkolom is onjuist opgegeven. Dit kan gebeuren als u meer dan één kolom is geselecteerd als Hallo Label of een onjuiste kolomindex selecteert. Het tweede geval Hallo zou bijvoorbeeld van toepassing als een kolomindex 30 wordt gebruikt met een invoergegevensset die alleen 25 kolommen heeft.

2. Hallo gegevensset bevat geen functie kolommen. Bijvoorbeeld, als invoergegevensset Hallo slechts één kolom, die is gemarkeerd als de kolom Label hello heeft, zou er geen onderdelen die u aan welke toobuild Hallo-model. In dit geval Hallo [Train Model] [ train-model] module, treedt een fout.

3. Hallo-invoergegevensset (functies of Label) bevat oneindig als een waarde.

## <a name="score-model-module-produces-incorrect-results"></a>De Module score Model oplevert onjuiste resultaten

![image2](./media/machine-learning-debug-models/train_test-2.png)

In een typische training/testen experiment voor leren met supervisie, Hallo [Split Data] [ split] module verdeelt de oorspronkelijke gegevensset Hallo in twee delen: één onderdeel gebruikte tootrain Hallo model en één onderdeel wordt gebruikt tooscore hoe goed het getrainde model hello wordt uitgevoerd. Hallo getrainde model wordt gebruikte tooscore Hallo testgegevens, waarna Hallo resultaten geëvalueerde toodetermine Hallo nauwkeurig Hallo model zijn.

Hallo [Score Model] [ score-model] module vereist twee invoeritems:

1. De uitvoer van een getraind model van Hallo [Train Model] [ train-model] module.
2. Een score gegevensset die verschilt van de gegevensset Hallo tootrain Hallo model gebruikt.

Het kan zijn dat hoewel Hallo experiment is geslaagd, Hallo [Score Model] [ score-model] module onjuiste resultaten oplevert. Verschillende scenario's kunnen ertoe leiden dat deze toohappen:

1. Als Hallo opgegeven Label categorische is en een regressiemodel wordt getraind op Hallo gegevens, een onjuiste uitvoer zou worden geproduceerd door Hallo [Score Model] [ score-model] module. Dit is omdat regressie een continue antwoord-variabele vereist. In dit geval zou het geschikte toouse een classificatie-model zijn. 

2. Op dezelfde manier als een classificatie-model wordt getraind van een gegevensset met getallen met drijvende komma in de kolom Label hello, kan deze ongewenste resultaten opleveren. Dit is omdat classificatie vereist een discrete antwoord-variabele, waarmee alleen waarden die variëren ten opzichte van een set eindig en meestal erg klein van klassen.

3. Als Hallo score berekenen voor gegevensset geen Hallo-model alle Hallo-tootrain voor functies die worden gebruikt bevat, Hallo [Score Model] [ score-model] , treedt een fout.

4. Als een rij in Hallo score berekenen voor gegevensset een ontbrekende waarde of een oneindige waarde voor een van de functies bevat, Hallo [Score Model] [ score-model] produceert uitvoer bijbehorende toothat rij niet.

5. Hallo [Score Model] [ score-model] kan leiden tot identiek outputs voor alle rijen in Hallo score berekenen voor gegevensset. Dit kan bijvoorbeeld gebeuren tijdens een poging de classificatie met besluit Forests als Hallo minimum aantal steekproeven per leaf-knooppunt wordt gekozen toobe meer dan Hallo aantal training voorbeelden beschikbaar.

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

