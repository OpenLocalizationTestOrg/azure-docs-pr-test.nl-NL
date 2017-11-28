---
title: Een antwoord met een eenvoudige regressiemodel - Azure Machine Learning voorspellen | Microsoft Docs
description: Het maken van een eenvoudige regressiemodel om te voorspellen een prijs in Gegevenswetenschap voor beginnende gebruikers video 4. Bevat een lineaire regressie met doelgegevens.
keywords: maken van een model, eenvoudige model, prijs voorspelling, eenvoudige regressiemodel
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: a28f1fab-e2d8-4663-aa7d-ca3530c8b525
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: 24df1823af2610a5111118f47e4cadbcfcc0eff1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="predict-an-answer-with-a-simple-model"></a><span data-ttu-id="5bf52-105">Met een eenvoudig model een antwoord voorspellen</span><span class="sxs-lookup"><span data-stu-id="5bf52-105">Predict an answer with a simple model</span></span>
## <a name="video-4-data-science-for-beginners-series"></a><span data-ttu-id="5bf52-106">Video 4: Gegevenswetenschap voor beginnende gebruikers reeks</span><span class="sxs-lookup"><span data-stu-id="5bf52-106">Video 4: Data Science for Beginners series</span></span>
<span data-ttu-id="5bf52-107">Informatie over het maken van een eenvoudige regressiemodel om te voorspellen van de prijs van een ruitvormige in Gegevenswetenschap voor beginnende gebruikers video 4.</span><span class="sxs-lookup"><span data-stu-id="5bf52-107">Learn how to create a simple regression model to predict the price of a diamond in Data Science for Beginners video 4.</span></span> <span data-ttu-id="5bf52-108">We gaat een regressiemodel met doelgegevens tekenen.</span><span class="sxs-lookup"><span data-stu-id="5bf52-108">We'll draw a regression model with target data.</span></span>

<span data-ttu-id="5bf52-109">Als u optimaal gebruik van de reeks, bekijk ze allemaal.</span><span class="sxs-lookup"><span data-stu-id="5bf52-109">To get the most out of the series, watch them all.</span></span> <span data-ttu-id="5bf52-110">[Ga naar de lijst met video 's](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="5bf52-110">[Go to the list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-predict-an-answer-with-a-simple-model/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="5bf52-111">Andere video's in deze reeks</span><span class="sxs-lookup"><span data-stu-id="5bf52-111">Other videos in this series</span></span>
<span data-ttu-id="5bf52-112">*Gegevenswetenschap voor beginnende gebruikers* is een korte inleiding voor gegevenswetenschap in vijf korte video's.</span><span class="sxs-lookup"><span data-stu-id="5bf52-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span></span>

* <span data-ttu-id="5bf52-113">Video 1: [gegevens wetenschappelijke antwoorden op vragen het 5](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span><span class="sxs-lookup"><span data-stu-id="5bf52-113">Video 1: [The 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="5bf52-114">Video 2: [uw gegevens gereed Is voor gegevenswetenschap?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span><span class="sxs-lookup"><span data-stu-id="5bf52-114">Video 2: [Is your data ready for data science?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span></span> <span data-ttu-id="5bf52-115">*(4 min 56 sec)*</span><span class="sxs-lookup"><span data-stu-id="5bf52-115">*(4 min 56 sec)*</span></span>
* <span data-ttu-id="5bf52-116">Video 3: [Stel een vraag kunt u met gegevens beantwoorden](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span><span class="sxs-lookup"><span data-stu-id="5bf52-116">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="5bf52-117">Video 4: Een antwoord met een eenvoudige model voorspellen</span><span class="sxs-lookup"><span data-stu-id="5bf52-117">Video 4: Predict an answer with a simple model</span></span>
* <span data-ttu-id="5bf52-118">Video 5: [kopiëren van anderen werk hiervoor gegevenswetenschap](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span><span class="sxs-lookup"><span data-stu-id="5bf52-118">Video 5: [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-predict-an-answer-with-a-simple-model"></a><span data-ttu-id="5bf52-119">De tekst: Een antwoord met een eenvoudige model voorspellen</span><span class="sxs-lookup"><span data-stu-id="5bf52-119">Transcript: Predict an answer with a simple model</span></span>
<span data-ttu-id="5bf52-120">Welkom bij de vierde video in de 'Data wetenschappelijke voor beginnende gebruikers' reeks.</span><span class="sxs-lookup"><span data-stu-id="5bf52-120">Welcome to the fourth video in the "Data Science for Beginners" series.</span></span> <span data-ttu-id="5bf52-121">In dit voorbeeld we een eenvoudige model bouwen en maken van een voorspelling.</span><span class="sxs-lookup"><span data-stu-id="5bf52-121">In this one, we'll build a simple model and make a prediction.</span></span>

<span data-ttu-id="5bf52-122">Een *model* wordt een vereenvoudigde artikel over onze gegevens.</span><span class="sxs-lookup"><span data-stu-id="5bf52-122">A *model* is a simplified story about our data.</span></span> <span data-ttu-id="5bf52-123">Ik ziet u heb.</span><span class="sxs-lookup"><span data-stu-id="5bf52-123">I'll show you what I mean.</span></span>

## <a name="collect-relevant-accurate-connected-enough-data"></a><span data-ttu-id="5bf52-124">Collect relevante, nauwkeurige, verbonden, voldoende gegevens</span><span class="sxs-lookup"><span data-stu-id="5bf52-124">Collect relevant, accurate, connected, enough data</span></span>
<span data-ttu-id="5bf52-125">Stel dat ik shop voor een ruitvormige wilt.</span><span class="sxs-lookup"><span data-stu-id="5bf52-125">Say I want to shop for a diamond.</span></span> <span data-ttu-id="5bf52-126">Ik heb een ring die deel uitmaakten van mijn oma met een instelling voor een ruitvormige 1.35 karaat en ik wil een idee krijgen van wat er gaat kosten.</span><span class="sxs-lookup"><span data-stu-id="5bf52-126">I have a ring that belonged to my grandmother with a setting for a 1.35 carat diamond, and I want to get an idea of how much it will cost.</span></span> <span data-ttu-id="5bf52-127">Ik een Kladblok en pen nemen in het archief juwelen en ik Noteer de prijs van alle in het geval en hoeveel ze in carats Weeg de uur per maand werken.</span><span class="sxs-lookup"><span data-stu-id="5bf52-127">I take a notepad and pen into the jewelry store, and I write down the price of all of the diamonds in the case and how much they weigh in carats.</span></span> <span data-ttu-id="5bf52-128">Beginnen met het eerste ruitvormige - de 1.01 carats en $7,366.</span><span class="sxs-lookup"><span data-stu-id="5bf52-128">Starting with the first diamond - it's 1.01 carats and $7,366.</span></span>

<span data-ttu-id="5bf52-129">Ik Ga nu via en doe dit voor alle andere ruiten in het archief.</span><span class="sxs-lookup"><span data-stu-id="5bf52-129">Now I go through and do this for all the other diamonds in the store.</span></span>

![Kolommen met gegevens ruitvormige](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/diamond-data.png)

<span data-ttu-id="5bf52-131">U ziet dat onze lijst twee kolommen.</span><span class="sxs-lookup"><span data-stu-id="5bf52-131">Notice that our list has two columns.</span></span> <span data-ttu-id="5bf52-132">Elke kolom heeft een ander kenmerk - gewicht in carats en prijs- en elke rij is één gegevenspunt dat een enkele ruitvormige vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="5bf52-132">Each column has a different attribute - weight in carats and price - and each row is a single data point that represents a single diamond.</span></span>

<span data-ttu-id="5bf52-133">Er is een klein daadwerkelijk gemaakt van gegevensset hier - een tabel.</span><span class="sxs-lookup"><span data-stu-id="5bf52-133">We've actually created a small data set here - a table.</span></span> <span data-ttu-id="5bf52-134">U ziet dat het voldoet aan de criteria voor kwaliteit:</span><span class="sxs-lookup"><span data-stu-id="5bf52-134">Notice that it meets our criteria for quality:</span></span>

* <span data-ttu-id="5bf52-135">De gegevens zijn **relevante** -gewicht definitief is gerelateerd aan prijs</span><span class="sxs-lookup"><span data-stu-id="5bf52-135">The data is **relevant** - weight is definitely related to price</span></span>
* <span data-ttu-id="5bf52-136">Deze heeft **nauwkeurige** -we de prijzen die we Noteer goed gecontroleerd</span><span class="sxs-lookup"><span data-stu-id="5bf52-136">It's **accurate** - we double-checked the prices that we write down</span></span>
* <span data-ttu-id="5bf52-137">Deze heeft **verbonden** -er zijn geen spaties in een van deze kolommen</span><span class="sxs-lookup"><span data-stu-id="5bf52-137">It's **connected** - there are no blank spaces in either of these columns</span></span>
* <span data-ttu-id="5bf52-138">En zullen we zien, heeft **voldoende** gegevens onze vragen te beantwoorden</span><span class="sxs-lookup"><span data-stu-id="5bf52-138">And, as we'll see, it's **enough** data to answer our question</span></span>

## <a name="ask-a-sharp-question"></a><span data-ttu-id="5bf52-139">Stel een vraag kruis</span><span class="sxs-lookup"><span data-stu-id="5bf52-139">Ask a sharp question</span></span>
<span data-ttu-id="5bf52-140">Nu we onze vraag kruis zodanig hebt inhouden: 'hoeveel kost het aanschaffen van een ruitvormige 1.35 karaat?'</span><span class="sxs-lookup"><span data-stu-id="5bf52-140">Now we'll pose our question in a sharp way: "How much will it cost to buy a 1.35 carat diamond?"</span></span>

<span data-ttu-id="5bf52-141">Onze lijst geen een ruitvormige 1.35 karaat in, zodat we de rest van onze gegevens gebruiken voor een antwoord op de vraag hebt.</span><span class="sxs-lookup"><span data-stu-id="5bf52-141">Our list doesn't have a 1.35 carat diamond in it, so we'll have to use the rest of our data to get an answer to the question.</span></span>

## <a name="plot-the-existing-data"></a><span data-ttu-id="5bf52-142">Tekenen van de bestaande gegevens</span><span class="sxs-lookup"><span data-stu-id="5bf52-142">Plot the existing data</span></span>
<span data-ttu-id="5bf52-143">Het eerste wat dat we doen is een horizontale lijn van het aantal aangeroepen as, om het gewicht van grafiek wordt getekend.</span><span class="sxs-lookup"><span data-stu-id="5bf52-143">The first thing we'll do is draw a horizontal number line, called an axis, to chart the weights.</span></span> <span data-ttu-id="5bf52-144">Het bereik van de gewichten is 0 tot en met 2, zodat we je een lijn die betrekking heeft op die variëren en ticks voor elk half karaat plaatsen tekenen.</span><span class="sxs-lookup"><span data-stu-id="5bf52-144">The range of the weights is 0 to 2, so we'll draw a line that covers that range and put ticks for each half carat.</span></span>

<span data-ttu-id="5bf52-145">Vervolgens moet er een verticale as voor het vastleggen van de prijs en de verbinding met het gewicht van de horizontale as tekenen.</span><span class="sxs-lookup"><span data-stu-id="5bf52-145">Next we'll draw a vertical axis to record the price and connect it to the horizontal weight axis.</span></span> <span data-ttu-id="5bf52-146">Dit is in eenheden van bedragen.</span><span class="sxs-lookup"><span data-stu-id="5bf52-146">This will be in units of dollars.</span></span> <span data-ttu-id="5bf52-147">Nu hebben we een reeks coördinaat assen.</span><span class="sxs-lookup"><span data-stu-id="5bf52-147">Now we have a set of coordinate axes.</span></span>

![Gewicht en prijs assen](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/weight-and-price-axes.png)

<span data-ttu-id="5bf52-149">We gaan nu deze gegevens nemen en schakel dit in een *spreidingsgrafiek tekent*.</span><span class="sxs-lookup"><span data-stu-id="5bf52-149">We're going to take this data now and turn it into a *scatter plot*.</span></span> <span data-ttu-id="5bf52-150">Dit is een uitstekende manier om te visualiseren numerieke gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="5bf52-150">This is a great way to visualize numerical data sets.</span></span>

<span data-ttu-id="5bf52-151">Wij krijgen voor het eerste gegevenspunt van een verticale lijn op 1.01 carats.</span><span class="sxs-lookup"><span data-stu-id="5bf52-151">For the first data point, we eyeball a vertical line at 1.01 carats.</span></span> <span data-ttu-id="5bf52-152">Vervolgens wordt een horizontale lijn op $7,366 krijgen.</span><span class="sxs-lookup"><span data-stu-id="5bf52-152">Then, we eyeball a horizontal line at $7,366.</span></span> <span data-ttu-id="5bf52-153">Wanneer ze voldoen aan, we een punt wordt getekend.</span><span class="sxs-lookup"><span data-stu-id="5bf52-153">Where they meet, we draw a dot.</span></span> <span data-ttu-id="5bf52-154">Hiermee wordt de eerste ruitvormige.</span><span class="sxs-lookup"><span data-stu-id="5bf52-154">This represents our first diamond.</span></span>

<span data-ttu-id="5bf52-155">Nu we elke ruitvormige op deze lijst doorlopen en doe hetzelfde.</span><span class="sxs-lookup"><span data-stu-id="5bf52-155">Now we go through each diamond on this list and do the same thing.</span></span> <span data-ttu-id="5bf52-156">Wanneer we via, is dit krijgen we: een aantal punten, één voor elke ruitvormige.</span><span class="sxs-lookup"><span data-stu-id="5bf52-156">When we're through, this is what we get: a bunch of dots, one for each diamond.</span></span>

![Spreiding van de grafiek](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/scatter-plot.png)

## <a name="draw-the-model-through-the-data-points"></a><span data-ttu-id="5bf52-158">Het model door de gegevenspunten worden getekend</span><span class="sxs-lookup"><span data-stu-id="5bf52-158">Draw the model through the data points</span></span>
<span data-ttu-id="5bf52-159">Als u de punten en squint bekijkt, lijkt de verzameling nu op een fat fuzzy lijn.</span><span class="sxs-lookup"><span data-stu-id="5bf52-159">Now if you look at the dots and squint, the collection looks like a fat, fuzzy line.</span></span> <span data-ttu-id="5bf52-160">We kunnen onze markering nemen en een lineaire ermee wordt getekend.</span><span class="sxs-lookup"><span data-stu-id="5bf52-160">We can take our marker and draw a straight line through it.</span></span>

<span data-ttu-id="5bf52-161">Door het tekenen van een regel gemaakt een *model*.</span><span class="sxs-lookup"><span data-stu-id="5bf52-161">By drawing a line, we created a *model*.</span></span> <span data-ttu-id="5bf52-162">Beschouwen als duurt de praktijk en het aanbrengen van een eenvoudig cartoon versie ervan.</span><span class="sxs-lookup"><span data-stu-id="5bf52-162">Think of this as taking the real world and making a simplistic cartoon version of it.</span></span> <span data-ttu-id="5bf52-163">Nu de cartoon is onjuist: de regel niet kan worden verstuurd alle gegevenspunten.</span><span class="sxs-lookup"><span data-stu-id="5bf52-163">Now the cartoon is wrong - the line doesn't go through all the data points.</span></span> <span data-ttu-id="5bf52-164">Maar is een nuttig vereenvoudiging.</span><span class="sxs-lookup"><span data-stu-id="5bf52-164">But, it's a useful simplification.</span></span>

![Lineaire regressie regel](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/linear-regression-line.png)

<span data-ttu-id="5bf52-166">Het feit dat alle punten gaan niet precies door de regel is in orde.</span><span class="sxs-lookup"><span data-stu-id="5bf52-166">The fact that all the dots don't go exactly through the line is OK.</span></span> <span data-ttu-id="5bf52-167">Gegevenswetenschappers uitgelegd dit door te zeggen dat er de model - die de regel - en vervolgens elk punt een aantal is *ruis* of *variantie* gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="5bf52-167">Data scientists explain this by saying that there's the model - that's the line - and then each dot has some *noise* or *variance* associated with it.</span></span> <span data-ttu-id="5bf52-168">Er is de onderliggende perfect relatie en is de ingaan, echte wereld waardoor ruis en onzekerheid worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="5bf52-168">There's the underlying perfect relationship, and then there's the gritty, real world that adds noise and uncertainty.</span></span>

<span data-ttu-id="5bf52-169">Omdat we proberen om de vraag te beantwoorden *hoeveel?* dit heet een *regressie*.</span><span class="sxs-lookup"><span data-stu-id="5bf52-169">Because we're trying to answer the question *How much?* this is called a *regression*.</span></span> <span data-ttu-id="5bf52-170">En omdat we maken gebruik van een lineaire is een *lineaire regressie*.</span><span class="sxs-lookup"><span data-stu-id="5bf52-170">And because we're using a straight line, it's a *linear regression*.</span></span>

## <a name="use-the-model-to-find-the-answer"></a><span data-ttu-id="5bf52-171">Gebruik het model in het antwoord gevonden</span><span class="sxs-lookup"><span data-stu-id="5bf52-171">Use the model to find the answer</span></span>
<span data-ttu-id="5bf52-172">Nu we een model hebben en we onze vraag vragen: hoeveel kost een ruitvormige 1.35 karaat?</span><span class="sxs-lookup"><span data-stu-id="5bf52-172">Now we have a model and we ask it our question: How much will a 1.35 carat diamond cost?</span></span>

<span data-ttu-id="5bf52-173">Voor onze vraag 1.35 carats krijgen we en tekenen van een verticale lijn.</span><span class="sxs-lookup"><span data-stu-id="5bf52-173">To answer our question, we eyeball 1.35 carats and draw a vertical line.</span></span> <span data-ttu-id="5bf52-174">Wanneer deze de modelregel bestrijkt krijgen we een horizontale lijn op de as dollar.</span><span class="sxs-lookup"><span data-stu-id="5bf52-174">Where it crosses the model line, we eyeball a horizontal line to the dollar axis.</span></span> <span data-ttu-id="5bf52-175">Het treffers recht op 10.000.</span><span class="sxs-lookup"><span data-stu-id="5bf52-175">It hits right at 10,000.</span></span> <span data-ttu-id="5bf52-176">Giek!</span><span class="sxs-lookup"><span data-stu-id="5bf52-176">Boom!</span></span> <span data-ttu-id="5bf52-177">Het antwoord is: een ruitvormige 1.35 karaat kost ongeveer 10.000 $.</span><span class="sxs-lookup"><span data-stu-id="5bf52-177">That's the answer: A 1.35 carat diamond costs about $10,000.</span></span>

![Het antwoord vinden op het model](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/find-the-answer.png)

## <a name="create-a-confidence-interval"></a><span data-ttu-id="5bf52-179">Een betrouwbaarheidsinterval maken</span><span class="sxs-lookup"><span data-stu-id="5bf52-179">Create a confidence interval</span></span>
<span data-ttu-id="5bf52-180">Het is natuurlijk zich afvragen hoe precies deze voorspelling is.</span><span class="sxs-lookup"><span data-stu-id="5bf52-180">It's natural to wonder how precise this prediction is.</span></span> <span data-ttu-id="5bf52-181">Het is handig om te weten of de ruitvormige 1.35 karaat heel dicht bij $10.000 wordt, of veel hoger of lager.</span><span class="sxs-lookup"><span data-stu-id="5bf52-181">It's useful to know whether the 1.35 carat diamond will be very close to $10,000, or a lot higher or lower.</span></span> <span data-ttu-id="5bf52-182">Om te bepalen welke, we een envelop rond de regressie regel bevat het merendeel van de puntjes tekenen.</span><span class="sxs-lookup"><span data-stu-id="5bf52-182">To figure this out, let's draw an envelope around the regression line that includes most of the dots.</span></span> <span data-ttu-id="5bf52-183">Deze envelop heet onze *betrouwbaarheidsinterval*: we vrij zeker van bent dat prijzen binnen deze envelop vallen, omdat in de afgelopen meest hiervan hebben.</span><span class="sxs-lookup"><span data-stu-id="5bf52-183">This envelope is called our *confidence interval*: We're pretty confident that prices fall within this envelope, because in the past most of them have.</span></span> <span data-ttu-id="5bf52-184">We tekenen twee meer horizontale lijnen van waar de regel 1.35 karaat de bovenkant en de onderkant van de envelop overschrijden.</span><span class="sxs-lookup"><span data-stu-id="5bf52-184">We can draw two more horizontal lines from where the 1.35 carat line crosses the top and the bottom of that envelope.</span></span>

![Betrouwbaarheidsinterval](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/confidence-interval.png)

<span data-ttu-id="5bf52-186">Nu je iets over onze betrouwbaarheidsinterval: je zorgeloos dat de prijs van een ruitvormige 1.35 karaat ongeveer $10.000 is - maar mogelijk zo laag fl 8.000 en mogelijk fl 12.000 zo hoog.</span><span class="sxs-lookup"><span data-stu-id="5bf52-186">Now we can say something about our confidence interval:  We can say confidently that the price of a 1.35 carat diamond is about $10,000 - but it might be as low as $8,000 and it might be as high as $12,000.</span></span>

## <a name="were-done-with-no-math-or-computers"></a><span data-ttu-id="5bf52-187">We klaar bent, zonder math of computers</span><span class="sxs-lookup"><span data-stu-id="5bf52-187">We're done, with no math or computers</span></span>
<span data-ttu-id="5bf52-188">We hebben gedaan welke gegevenswetenschappers betaald krijgen te doen en we deze door te tekenen voldoet:</span><span class="sxs-lookup"><span data-stu-id="5bf52-188">We did what data scientists get paid to do, and we did it just by drawing:</span></span>

* <span data-ttu-id="5bf52-189">We vraag een dat we met gegevens beantwoorden kan</span><span class="sxs-lookup"><span data-stu-id="5bf52-189">We asked a question that we could answer with data</span></span>
* <span data-ttu-id="5bf52-190">Moesten een *model* met *lineaire regressie*</span><span class="sxs-lookup"><span data-stu-id="5bf52-190">We built a *model* using *linear regression*</span></span>
* <span data-ttu-id="5bf52-191">Er een *voorspelling*, voltooid met een *betrouwbaarheidsinterval*</span><span class="sxs-lookup"><span data-stu-id="5bf52-191">We made a *prediction*, complete with a *confidence interval*</span></span>

<span data-ttu-id="5bf52-192">En we math of computers niet gebruiken om dat te doen.</span><span class="sxs-lookup"><span data-stu-id="5bf52-192">And we didn't use math or computers to do it.</span></span>

<span data-ttu-id="5bf52-193">Nu als we gehad meer informatie, zoals...</span><span class="sxs-lookup"><span data-stu-id="5bf52-193">Now if we'd had more information, like...</span></span>

* <span data-ttu-id="5bf52-194">de ruitvormige knippen</span><span class="sxs-lookup"><span data-stu-id="5bf52-194">the cut of the diamond</span></span>
* <span data-ttu-id="5bf52-195">kleurvariaties (hoe sluiten de ruitvormige is voor een wit)</span><span class="sxs-lookup"><span data-stu-id="5bf52-195">color variations (how close the diamond is to being white)</span></span>
* <span data-ttu-id="5bf52-196">het aantal insluitingen in de ruitvormige</span><span class="sxs-lookup"><span data-stu-id="5bf52-196">the number of inclusions in the diamond</span></span>

<span data-ttu-id="5bf52-197">.. .en we zouden hebben meer kolommen.</span><span class="sxs-lookup"><span data-stu-id="5bf52-197">...then we would have had more columns.</span></span> <span data-ttu-id="5bf52-198">Math wordt in dat geval handig zijn.</span><span class="sxs-lookup"><span data-stu-id="5bf52-198">In that case, math becomes helpful.</span></span> <span data-ttu-id="5bf52-199">Als er meer dan twee kolommen, is het moeilijk te tekenen punten op papier.</span><span class="sxs-lookup"><span data-stu-id="5bf52-199">If you have more than two columns, it's hard to draw dots on paper.</span></span> <span data-ttu-id="5bf52-200">De berekening kunt u die regel of dit vlak tot uw gegevens zeer mooi passen.</span><span class="sxs-lookup"><span data-stu-id="5bf52-200">The math lets you fit that line or that plane to your data very nicely.</span></span>

<span data-ttu-id="5bf52-201">Ook als in plaats van slechts een handvol ruiten, zijn twee duizend of twee miljoen en vervolgens kunt u die werken veel sneller uitvoeren met een computer.</span><span class="sxs-lookup"><span data-stu-id="5bf52-201">Also, if instead of just a handful of diamonds, we had two thousand or two million, then you can do that work much faster with a computer.</span></span>

<span data-ttu-id="5bf52-202">Vandaag de dag besproken hierover lineaire regressie en er een voorspelling met behulp van gegevens hebt aangebracht.</span><span class="sxs-lookup"><span data-stu-id="5bf52-202">Today, we've talked about how to do linear regression, and we made a prediction using data.</span></span>

<span data-ttu-id="5bf52-203">Zorg ervoor dat de andere video's in 'Data wetenschappelijke voor beginnende gebruikers' van Microsoft Azure Machine Learning uitchecken.</span><span class="sxs-lookup"><span data-stu-id="5bf52-203">Be sure to check out the other videos in "Data Science for Beginners" from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5bf52-204">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5bf52-204">Next steps</span></span>
* [<span data-ttu-id="5bf52-205">Probeer een eerste gegevens wetenschappelijke experiment met Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="5bf52-205">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="5bf52-206">Maak kennis met Machine Learning in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5bf52-206">Get an introduction to Machine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)
