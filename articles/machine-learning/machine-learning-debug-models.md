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
# <a name="debug-your-model-in-azure-machine-learning"></a><span data-ttu-id="5b6e0-103">Fouten opsporen in uw model in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5b6e0-103">Debug your Model in Azure Machine Learning</span></span>

<span data-ttu-id="5b6e0-104">Dit artikel wordt uitgelegd Hallo mogelijke redenen waarom een Hallo na twee fouten aangetroffen mogelijk bij het uitvoeren van een model:</span><span class="sxs-lookup"><span data-stu-id="5b6e0-104">This article explains hello potential reasons why either of hello following two failures might be encountered when running a model:</span></span>

* <span data-ttu-id="5b6e0-105">Hallo [Train Model] [ train-model] module, treedt een fout</span><span class="sxs-lookup"><span data-stu-id="5b6e0-105">hello [Train Model][train-model] module produces an error</span></span> 
* <span data-ttu-id="5b6e0-106">Hallo [Score Model] [ score-model] module onjuiste resultaten oplevert</span><span class="sxs-lookup"><span data-stu-id="5b6e0-106">hello [Score Model][score-model] module produces incorrect results</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a><span data-ttu-id="5b6e0-107">Module Train-Model, treedt een fout</span><span class="sxs-lookup"><span data-stu-id="5b6e0-107">Train Model Module produces an error</span></span>

![image1](./media/machine-learning-debug-models/train_model-1.png)

<span data-ttu-id="5b6e0-109">Hallo [Train Model] [ train-model] Module verwacht twee invoeritems:</span><span class="sxs-lookup"><span data-stu-id="5b6e0-109">hello [Train Model][train-model] Module expects two inputs:</span></span>

1. <span data-ttu-id="5b6e0-110">Hallo-type van machine learning-model uit Hallo-verzameling van modellen die worden geleverd door het Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-110">hello type of machine learning model from hello collection of models provided by Azure Machine Learning.</span></span>
2. <span data-ttu-id="5b6e0-111">Hallo trainingsgegevens met een opgegeven labelkolom waarin Hallo variabele toopredict (hello andere kolommen wordt uitgegaan van toobe functies).</span><span class="sxs-lookup"><span data-stu-id="5b6e0-111">hello training data with a specified Label column which specifies hello variable toopredict (hello other columns are assumed toobe Features).</span></span>

<span data-ttu-id="5b6e0-112">Deze module kan een fout in de volgende gevallen Hallo produceren:</span><span class="sxs-lookup"><span data-stu-id="5b6e0-112">This module can produce an error in hello following cases:</span></span>

1. <span data-ttu-id="5b6e0-113">Hallo labelkolom is onjuist opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-113">hello Label column is specified incorrectly.</span></span> <span data-ttu-id="5b6e0-114">Dit kan gebeuren als u meer dan één kolom is geselecteerd als Hallo Label of een onjuiste kolomindex selecteert.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-114">This can happen if either more than one column is selected as hello Label or an incorrect column index is selected.</span></span> <span data-ttu-id="5b6e0-115">Het tweede geval Hallo zou bijvoorbeeld van toepassing als een kolomindex 30 wordt gebruikt met een invoergegevensset die alleen 25 kolommen heeft.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-115">For example, hello second case would apply if a column index of 30 is used with an input dataset which has only 25 columns.</span></span>

2. <span data-ttu-id="5b6e0-116">Hallo gegevensset bevat geen functie kolommen.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-116">hello dataset does not contain any Feature columns.</span></span> <span data-ttu-id="5b6e0-117">Bijvoorbeeld, als invoergegevensset Hallo slechts één kolom, die is gemarkeerd als de kolom Label hello heeft, zou er geen onderdelen die u aan welke toobuild Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-117">For example, if hello input dataset has only one column, which is marked as hello Label column, there would be no features with which toobuild hello model.</span></span> <span data-ttu-id="5b6e0-118">In dit geval Hallo [Train Model] [ train-model] module, treedt een fout.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-118">In this case, hello [Train Model][train-model] module produces an error.</span></span>

3. <span data-ttu-id="5b6e0-119">Hallo-invoergegevensset (functies of Label) bevat oneindig als een waarde.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-119">hello input dataset (Features or Label) contains Infinity as a value.</span></span>

## <a name="score-model-module-produces-incorrect-results"></a><span data-ttu-id="5b6e0-120">De Module score Model oplevert onjuiste resultaten</span><span class="sxs-lookup"><span data-stu-id="5b6e0-120">Score Model Module produces incorrect results</span></span>

![image2](./media/machine-learning-debug-models/train_test-2.png)

<span data-ttu-id="5b6e0-122">In een typische training/testen experiment voor leren met supervisie, Hallo [Split Data] [ split] module verdeelt de oorspronkelijke gegevensset Hallo in twee delen: één onderdeel gebruikte tootrain Hallo model en één onderdeel wordt gebruikt tooscore hoe goed het getrainde model hello wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-122">In a typical training/testing experiment for supervised learning, hello [Split Data][split] module divides hello original dataset into two parts: one part is used tootrain hello model and one part is used tooscore how well hello trained model performs.</span></span> <span data-ttu-id="5b6e0-123">Hallo getrainde model wordt gebruikte tooscore Hallo testgegevens, waarna Hallo resultaten geëvalueerde toodetermine Hallo nauwkeurig Hallo model zijn.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-123">hello trained model is then used tooscore hello test data, after which hello results are evaluated toodetermine hello accuracy of hello model.</span></span>

<span data-ttu-id="5b6e0-124">Hallo [Score Model] [ score-model] module vereist twee invoeritems:</span><span class="sxs-lookup"><span data-stu-id="5b6e0-124">hello [Score Model][score-model] module requires two inputs:</span></span>

1. <span data-ttu-id="5b6e0-125">De uitvoer van een getraind model van Hallo [Train Model] [ train-model] module.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-125">A trained model output from hello [Train Model][train-model] module.</span></span>
2. <span data-ttu-id="5b6e0-126">Een score gegevensset die verschilt van de gegevensset Hallo tootrain Hallo model gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-126">A scoring dataset that is different from hello dataset used tootrain hello model.</span></span>

<span data-ttu-id="5b6e0-127">Het kan zijn dat hoewel Hallo experiment is geslaagd, Hallo [Score Model] [ score-model] module onjuiste resultaten oplevert.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-127">It's possible that even though hello experiment succeeds, hello [Score Model][score-model] module produces incorrect results.</span></span> <span data-ttu-id="5b6e0-128">Verschillende scenario's kunnen ertoe leiden dat deze toohappen:</span><span class="sxs-lookup"><span data-stu-id="5b6e0-128">Several scenarios may cause this toohappen:</span></span>

1. <span data-ttu-id="5b6e0-129">Als Hallo opgegeven Label categorische is en een regressiemodel wordt getraind op Hallo gegevens, een onjuiste uitvoer zou worden geproduceerd door Hallo [Score Model] [ score-model] module.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-129">If hello specified Label is categorical and a regression model is trained on hello data, an incorrect output would be produced by hello [Score Model][score-model] module.</span></span> <span data-ttu-id="5b6e0-130">Dit is omdat regressie een continue antwoord-variabele vereist.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-130">This is because regression requires a continuous response variable.</span></span> <span data-ttu-id="5b6e0-131">In dit geval zou het geschikte toouse een classificatie-model zijn.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-131">In this case, it would be more suitable toouse a classification model.</span></span> 

2. <span data-ttu-id="5b6e0-132">Op dezelfde manier als een classificatie-model wordt getraind van een gegevensset met getallen met drijvende komma in de kolom Label hello, kan deze ongewenste resultaten opleveren.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-132">Similarly, if a classification model is trained on a dataset having floating point numbers in hello Label column, it may produce undesirable results.</span></span> <span data-ttu-id="5b6e0-133">Dit is omdat classificatie vereist een discrete antwoord-variabele, waarmee alleen waarden die variëren ten opzichte van een set eindig en meestal erg klein van klassen.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-133">This is because classification requires a discrete response variable that only allows values that range over a finite, and usually somewhat small, set of classes.</span></span>

3. <span data-ttu-id="5b6e0-134">Als Hallo score berekenen voor gegevensset geen Hallo-model alle Hallo-tootrain voor functies die worden gebruikt bevat, Hallo [Score Model] [ score-model] , treedt een fout.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-134">If hello scoring dataset does not contain all hello features used tootrain hello model, hello [Score Model][score-model] produces an error.</span></span>

4. <span data-ttu-id="5b6e0-135">Als een rij in Hallo score berekenen voor gegevensset een ontbrekende waarde of een oneindige waarde voor een van de functies bevat, Hallo [Score Model] [ score-model] produceert uitvoer bijbehorende toothat rij niet.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-135">If a row in hello scoring dataset contains a missing value or an infinite value for any of its features, hello [Score Model][score-model] will not produce any output corresponding toothat row.</span></span>

5. <span data-ttu-id="5b6e0-136">Hallo [Score Model] [ score-model] kan leiden tot identiek outputs voor alle rijen in Hallo score berekenen voor gegevensset.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-136">hello [Score Model][score-model] may produce identical outputs for all rows in hello scoring dataset.</span></span> <span data-ttu-id="5b6e0-137">Dit kan bijvoorbeeld gebeuren tijdens een poging de classificatie met besluit Forests als Hallo minimum aantal steekproeven per leaf-knooppunt wordt gekozen toobe meer dan Hallo aantal training voorbeelden beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="5b6e0-137">This could occur, for example, when attempting classification using Decision Forests if hello minimum number of samples per leaf node is chosen toobe more than hello number of training examples available.</span></span>

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

