---
title: Vraag een vraaggegevens kunnen beantwoorden - problemen wetenschap - Azure Machine Learning | Microsoft Docs
description: Ontdek hoe u een vraag van de wetenschap kruis gegevens in Gegevenswetenschap voor beginnende gebruikers video 3 formuleren. Bevat een vergelijking van classificatie en regressie vragen.
keywords: vragen over de wetenschap van gegevens van problemen wetenschappelijke gegevens formuleren vragen, regressie vragen, classificatievragen, kruis vraag
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: 5b9501e3-9964-417a-8ffc-8913103da77b
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: 0495dbab72024e504ae33d35f16a212a2084bc10
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="ask-a-question-you-can-answer-with-data"></a><span data-ttu-id="9ad89-105">Stel een vraag die u met gegevens kunt beantwoorden</span><span class="sxs-lookup"><span data-stu-id="9ad89-105">Ask a question you can answer with data</span></span>
## <a name="video-3-data-science-for-beginners-series"></a><span data-ttu-id="9ad89-106">Video 3: Gegevenswetenschap voor beginnende gebruikers reeks</span><span class="sxs-lookup"><span data-stu-id="9ad89-106">Video 3: Data Science for Beginners series</span></span>
<span data-ttu-id="9ad89-107">Informatie over het probleem wetenschappelijke gegevens in een vraag in Gegevenswetenschap voor beginnende gebruikers video 3 formuleren.</span><span class="sxs-lookup"><span data-stu-id="9ad89-107">Learn how to formulate a data science problem into a question in Data Science for Beginners video 3.</span></span> <span data-ttu-id="9ad89-108">In deze video bevat een vergelijking van vragen voor classificatie en regressie algoritmen.</span><span class="sxs-lookup"><span data-stu-id="9ad89-108">This video includes a comparison of questions for classification and regression algorithms.</span></span>

<span data-ttu-id="9ad89-109">Als u optimaal gebruik van de reeks, bekijk ze allemaal.</span><span class="sxs-lookup"><span data-stu-id="9ad89-109">To get the most out of the series, watch them all.</span></span> <span data-ttu-id="9ad89-110">[Ga naar de lijst met video 's](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="9ad89-110">[Go to the list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Data-science-for-beginners-Ask-a-question-you-can-answer-with-data/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="9ad89-111">Andere video's in deze reeks</span><span class="sxs-lookup"><span data-stu-id="9ad89-111">Other videos in this series</span></span>
<span data-ttu-id="9ad89-112">*Gegevenswetenschap voor beginnende gebruikers* is een korte inleiding voor gegevenswetenschap in vijf korte video's.</span><span class="sxs-lookup"><span data-stu-id="9ad89-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span></span>

* <span data-ttu-id="9ad89-113">Video 1: [gegevens wetenschappelijke antwoorden op vragen het 5](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span><span class="sxs-lookup"><span data-stu-id="9ad89-113">Video 1: [The 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="9ad89-114">Video 2: [uw gegevens gereed Is voor gegevenswetenschap?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span><span class="sxs-lookup"><span data-stu-id="9ad89-114">Video 2: [Is your data ready for data science?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span></span> <span data-ttu-id="9ad89-115">*(4 min 56 sec)*</span><span class="sxs-lookup"><span data-stu-id="9ad89-115">*(4 min 56 sec)*</span></span>
* <span data-ttu-id="9ad89-116">Video 3: Stel een vraag die u met gegevens beantwoorden kunt</span><span class="sxs-lookup"><span data-stu-id="9ad89-116">Video 3: Ask a question you can answer with data</span></span>
* <span data-ttu-id="9ad89-117">Video 4: [voorspellen een antwoord met een eenvoudige model](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span><span class="sxs-lookup"><span data-stu-id="9ad89-117">Video 4: [Predict an answer with a simple model](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span></span>
* <span data-ttu-id="9ad89-118">Video 5: [kopiëren van anderen werk hiervoor gegevenswetenschap](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span><span class="sxs-lookup"><span data-stu-id="9ad89-118">Video 5: [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-ask-a-question-you-can-answer-with-data"></a><span data-ttu-id="9ad89-119">De tekst: Stel een vraag die u met gegevens beantwoorden kunt</span><span class="sxs-lookup"><span data-stu-id="9ad89-119">Transcript: Ask a question you can answer with data</span></span>
<span data-ttu-id="9ad89-120">Welkom bij de derde video in de reeks 'Wetenschappelijke gegevens voor beginnende gebruikers'.</span><span class="sxs-lookup"><span data-stu-id="9ad89-120">Welcome to the third video in the series "Data Science for Beginners."</span></span>  

<span data-ttu-id="9ad89-121">In dit voorbeeld krijgt u een aantal tips voor het opstellen van een vraag die u met gegevens kan beantwoorden.</span><span class="sxs-lookup"><span data-stu-id="9ad89-121">In this one, you'll get some tips for formulating a question you can answer with data.</span></span>

<span data-ttu-id="9ad89-122">Mogelijk krijgt u meer buiten deze video als u eerst video de twee eerder in deze reeks: 'de gegevenswetenschap 5 vragen kan beantwoorden' en 'Is uw gegevens is gereed voor gegevenswetenschap?'</span><span class="sxs-lookup"><span data-stu-id="9ad89-122">You might get more out of this video, if you first watch the two earlier videos in this series: "The 5 questions data science can answer" and "Is your data is ready for data science?"</span></span>

## <a name="ask-a-sharp-question"></a><span data-ttu-id="9ad89-123">Stel een vraag kruis</span><span class="sxs-lookup"><span data-stu-id="9ad89-123">Ask a sharp question</span></span>
<span data-ttu-id="9ad89-124">Besproken over hoe gegevenswetenschap het proces is van het gebruik van namen (ook wel categorieën of labels) en cijfers voor het voorspellen van een antwoord op een vraag.</span><span class="sxs-lookup"><span data-stu-id="9ad89-124">We've talked about how data science is the process of using names (also called categories or labels) and numbers to predict an answer to a question.</span></span> <span data-ttu-id="9ad89-125">Maar niet elke vraag; Er moet een *kruis vraag.*</span><span class="sxs-lookup"><span data-stu-id="9ad89-125">But it can't be just any question; it has to be a *sharp question.*</span></span>

<span data-ttu-id="9ad89-126">Een vaag vraag hoeft niet te worden beantwoord met een naam of een cijfer.</span><span class="sxs-lookup"><span data-stu-id="9ad89-126">A vague question doesn't have to be answered with a name or a number.</span></span> <span data-ttu-id="9ad89-127">Er moet een kruis vraag.</span><span class="sxs-lookup"><span data-stu-id="9ad89-127">A sharp question must.</span></span>

<span data-ttu-id="9ad89-128">Stel dat u een magische licht met een genie die wordt naar waarheid elke vraag die u vragen beantwoorden gevonden.</span><span class="sxs-lookup"><span data-stu-id="9ad89-128">Imagine you found a magic lamp with a genie who will truthfully answer any question you ask.</span></span> <span data-ttu-id="9ad89-129">Maar het is een mischievous genie, en hij proberen aan te brengen van zijn antwoord als vaag en verwarrend zijn als hij opslag met krijgen kan.</span><span class="sxs-lookup"><span data-stu-id="9ad89-129">But it's a mischievous genie, and he'll try to make his answer as vague and confusing as he can get away with.</span></span> <span data-ttu-id="9ad89-130">Wilt u hem omlaag vastmaken aan een vraag dus luchtdichte hij niet kan helpen maar laat u weten wat u wilt weten.</span><span class="sxs-lookup"><span data-stu-id="9ad89-130">You want to pin him down with a question so airtight that he can't help but tell you what you want to know.</span></span>

<span data-ttu-id="9ad89-131">Als u een vraag vaag, zoals 'Wat er gebeurt met mijn stock gebeurt?', de genie mogelijk beantwoorden, 'de prijs gewijzigd'.</span><span class="sxs-lookup"><span data-stu-id="9ad89-131">If you were to ask a vague question, like "What's going to happen with my stock?", the genie might answer, "The price will change".</span></span> <span data-ttu-id="9ad89-132">Die een ware antwoord is, maar het is niet erg nuttig.</span><span class="sxs-lookup"><span data-stu-id="9ad89-132">That's a truthful answer, but it's not very helpful.</span></span>

<span data-ttu-id="9ad89-133">Maar als u zou een vraag kruis, zoals 'Wat mijn stock prijzen worden volgende week?', de genie kan niet helpen maar bieden u een specifieke beantwoorden en een verkoopprijs voorspellen.</span><span class="sxs-lookup"><span data-stu-id="9ad89-133">But if you were to ask a sharp question, like "What will my stock's sale price be next week?", the genie can't help but give you a specific answer and predict a sale price.</span></span>

## <a name="examples-of-your-answer-target-data"></a><span data-ttu-id="9ad89-134">Voorbeelden van uw antwoord: gegevens zijn gericht</span><span class="sxs-lookup"><span data-stu-id="9ad89-134">Examples of your answer: Target data</span></span>
<span data-ttu-id="9ad89-135">Nadat u uw vraag formuleren, controleert u of u voorbeelden van het antwoord in uw gegevens hebt.</span><span class="sxs-lookup"><span data-stu-id="9ad89-135">Once you formulate your question, check to see whether you have examples of the answer in your data.</span></span>

<span data-ttu-id="9ad89-136">Als de vraag "Wat kan mijn stock verkoopprijs zijn volgende week?"</span><span class="sxs-lookup"><span data-stu-id="9ad89-136">If our question is "What will my stock's sale price be next week?"</span></span> <span data-ttu-id="9ad89-137">vervolgens hebben we om ervoor te zorgen dat onze gegevens omvatten de geschiedenis aandelenkoersen.</span><span class="sxs-lookup"><span data-stu-id="9ad89-137">then we have to make sure our data includes the stock price history.</span></span>

<span data-ttu-id="9ad89-138">Als de vraag 'welke auto in mijn wagenpark gaat eerst mislukken?'</span><span class="sxs-lookup"><span data-stu-id="9ad89-138">If our question is "Which car in my fleet is going to fail first?"</span></span> <span data-ttu-id="9ad89-139">vervolgens hebben we om ervoor te zorgen dat onze gegevens omvatten informatie over eerdere fouten.</span><span class="sxs-lookup"><span data-stu-id="9ad89-139">then we have to make sure our data includes information about previous failures.</span></span>

![Doelgegevens - voorbeelden van het antwoord.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/target-data.png)

<span data-ttu-id="9ad89-142">Deze voorbeelden van antwoorden worden een doel genoemd.</span><span class="sxs-lookup"><span data-stu-id="9ad89-142">These examples of answers are called a target.</span></span> <span data-ttu-id="9ad89-143">Een doel is wat we willen voorspellen over toekomstige gegevenspunten of het om een categorie of een cijfer.</span><span class="sxs-lookup"><span data-stu-id="9ad89-143">A target is what we are trying to predict about future data points, whether it's a category or a number.</span></span>

<span data-ttu-id="9ad89-144">Als u geen doelgegevens, moet u enkele ophalen.</span><span class="sxs-lookup"><span data-stu-id="9ad89-144">If you don't have any target data, you'll need to get some.</span></span> <span data-ttu-id="9ad89-145">Het niet mogelijk om uw vraag zonder deze te beantwoorden.</span><span class="sxs-lookup"><span data-stu-id="9ad89-145">You won't be able to answer your question without it.</span></span>

## <a name="reformulate-your-question"></a><span data-ttu-id="9ad89-146">Uw vraag reformulate</span><span class="sxs-lookup"><span data-stu-id="9ad89-146">Reformulate your question</span></span>
<span data-ttu-id="9ad89-147">U kunt ook uw vraag om een nuttiger antwoord uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="9ad89-147">Sometimes you can reword your question to get a more useful answer.</span></span>

<span data-ttu-id="9ad89-148">De vraag 'Is deze gegevens punt A of B?'</span><span class="sxs-lookup"><span data-stu-id="9ad89-148">The question "Is this data point A or B?"</span></span> <span data-ttu-id="9ad89-149">de categorie (of de naam of label) van iets voorspelt.</span><span class="sxs-lookup"><span data-stu-id="9ad89-149">predicts the category (or name or label) of something.</span></span> <span data-ttu-id="9ad89-150">Om te reageren, gebruiken we een *classificatiealgoritme*.</span><span class="sxs-lookup"><span data-stu-id="9ad89-150">To answer it, we use a *classification algorithm*.</span></span>

<span data-ttu-id="9ad89-151">De vraag 'Hoeveel?'</span><span class="sxs-lookup"><span data-stu-id="9ad89-151">The question "How much?"</span></span> <span data-ttu-id="9ad89-152">of 'Hoeveel?'</span><span class="sxs-lookup"><span data-stu-id="9ad89-152">or "How many?"</span></span> <span data-ttu-id="9ad89-153">voorspelt een bedrag.</span><span class="sxs-lookup"><span data-stu-id="9ad89-153">predicts an amount.</span></span> <span data-ttu-id="9ad89-154">Het antwoord te gebruiken we een *regression-algoritme*.</span><span class="sxs-lookup"><span data-stu-id="9ad89-154">To answer it we use a *regression algorithm*.</span></span>

<span data-ttu-id="9ad89-155">Als u wilt zien hoe we deze kunt transformeren, bekijken we de vraag 'welke verhaal nieuws is de meest interessante naar deze lezer?'</span><span class="sxs-lookup"><span data-stu-id="9ad89-155">To see how we can transform these, let's look at the question, "Which news story is the most interesting to this reader?"</span></span> <span data-ttu-id="9ad89-156">Wordt de gebruiker gevraagd een voorspelling van één keuze uit tal van mogelijkheden - met andere woorden 'Is deze A of B of C of D?'</span><span class="sxs-lookup"><span data-stu-id="9ad89-156">It asks for a prediction of a single choice from many possibilities - in other words "Is this A or B or C or D?"</span></span> <span data-ttu-id="9ad89-157">- en een classificatie-algoritme zou gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9ad89-157">- and would use a classification algorithm.</span></span>

<span data-ttu-id="9ad89-158">Maar deze vraag is mogelijk beter te beantwoorden als uitgelegd als 'hoe interessante is elk artikel op deze lijst voor deze lezer?'</span><span class="sxs-lookup"><span data-stu-id="9ad89-158">But, this question may be easier to answer if you reword it as "How interesting is each story on this list to this reader?"</span></span> <span data-ttu-id="9ad89-159">Nu kunt u geven elk artikel een numerieke score en wordt het eenvoudig kunt herkennen van het artikel hoogste score berekenen.</span><span class="sxs-lookup"><span data-stu-id="9ad89-159">Now you can give each article a numerical score, and then it's easy to identify the highest-scoring article.</span></span> <span data-ttu-id="9ad89-160">Dit is een van de vraag classificatie in een vraag regressie formuleren of hoeveel?</span><span class="sxs-lookup"><span data-stu-id="9ad89-160">This is a rephrasing of the classification question into a regression question or How much?</span></span>

![Uw vraag reformulate.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/classification-question-vs-regression-question.png)

<span data-ttu-id="9ad89-163">Hoe u een vraag is een aanwijzing naar welk algoritme vragen kunnen geven u een antwoord.</span><span class="sxs-lookup"><span data-stu-id="9ad89-163">How you ask a question is a clue to which algorithm can give you an answer.</span></span>

<span data-ttu-id="9ad89-164">U vindt dat bepaalde families van algoritmen - zoals de waarden in ons voorbeeld van het artikel nieuws - nauw verwant zijn.</span><span class="sxs-lookup"><span data-stu-id="9ad89-164">You'll find that certain families of algorithms - like the ones in our news story example - are closely related.</span></span> <span data-ttu-id="9ad89-165">U kunt uw vraag voor het gebruik van het algoritme waarmee u het meest geschikt antwoord reformulate.</span><span class="sxs-lookup"><span data-stu-id="9ad89-165">You can reformulate your question to use the algorithm that gives you the most useful answer.</span></span>

<span data-ttu-id="9ad89-166">Maar zeer belangrijk, vraag die kruis - de vraag die u met gegevens kan beantwoorden.</span><span class="sxs-lookup"><span data-stu-id="9ad89-166">But, most important, ask that sharp question - the question that you can answer with data.</span></span> <span data-ttu-id="9ad89-167">En controleer of dat u de juiste gegevens antwoord zijn.</span><span class="sxs-lookup"><span data-stu-id="9ad89-167">And be sure you have the right data to answer it.</span></span>

<span data-ttu-id="9ad89-168">Besproken over sommige basisprincipes voor u een vraag stelt dat u met gegevens kan beantwoorden.</span><span class="sxs-lookup"><span data-stu-id="9ad89-168">We've talked about some basic principles for asking a question you can answer with data.</span></span>

<span data-ttu-id="9ad89-169">Zorg ervoor dat de andere video's in 'Data wetenschappelijke voor beginnende gebruikers' van Microsoft Azure Machine Learning uitchecken.</span><span class="sxs-lookup"><span data-stu-id="9ad89-169">Be sure to check out the other videos in "Data Science for Beginners" from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ad89-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9ad89-170">Next steps</span></span>
* [<span data-ttu-id="9ad89-171">Probeer een eerste gegevens wetenschappelijke experiment met Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="9ad89-171">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="9ad89-172">Maak kennis met Machine Learning in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9ad89-172">Get an introduction to Machine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)
