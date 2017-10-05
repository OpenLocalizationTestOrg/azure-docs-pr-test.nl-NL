---
title: 'Machine Learning API''s: Text Analytics | Microsoft Docs'
description: API's van Microsoft Machine Learning-Analytics tekst kan worden gebruikt voor het analyseren van niet-gestructureerde tekst voor gevoel analyse, uitpakken van sleutel woordgroep, taal wordt gedetecteerd en onderwerp detectie.
services: machine-learning
documentationcenter: 
author: onewth
manager: jhubbard
editor: cgronlun
ms.assetid: 5b60694e-5521-4e4d-bf6a-1a92fdf94b65
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: onewth
ROBOTS: NOINDEX
redirect_url: ../cognitive-services/cognitive-services-text-analytics-quick-start
redirect_document_id: TRUE
ms.openlocfilehash: 10eae2ff5624dcb57de1cf72b326147f35bc2a0b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a><span data-ttu-id="58346-103">API’s voor Machine Learning: Tekstanalyse voor sentimenten, Sleuteltermextractie, Taaldetectie en Onderwerpdetectie</span><span class="sxs-lookup"><span data-stu-id="58346-103">Machine Learning APIs: Text Analytics for Sentiment, Key Phrase Extraction, Language Detection and Topic Detection</span></span>
> [!NOTE]
> <span data-ttu-id="58346-104">Deze handleiding is bedoeld voor versie 1 van de API.</span><span class="sxs-lookup"><span data-stu-id="58346-104">This guide is for version 1 of the API.</span></span> <span data-ttu-id="58346-105">Voor versie 2, [ **verwijzen naar dit document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="58346-105">For version 2, [**refer to this document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span></span> <span data-ttu-id="58346-106">Versie 2 is nu de gewenste versie van deze API.</span><span class="sxs-lookup"><span data-stu-id="58346-106">Version 2 is now the preferred version of this API.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="58346-107">Overzicht</span><span class="sxs-lookup"><span data-stu-id="58346-107">Overview</span></span>
<span data-ttu-id="58346-108">De tekst Analytics-API is een suite met tekstanalyse [webservices](https://datamarket.azure.com/dataset/amla/text-analytics) gebouwd met Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="58346-108">The Text Analytics API is a suite of text analytics [web services](https://datamarket.azure.com/dataset/amla/text-analytics) built with Azure Machine Learning.</span></span> <span data-ttu-id="58346-109">De API kan worden gebruikt voor het analyseren van niet-gestructureerde tekst voor taken zoals gevoel analyse, uitpakken van sleutel woordgroep, taal wordt gedetecteerd en onderwerp detectie.</span><span class="sxs-lookup"><span data-stu-id="58346-109">The API can be used to analyze unstructured text for tasks such as sentiment analysis, key phrase extraction, language detection and topic detection.</span></span> <span data-ttu-id="58346-110">U hebt geen trainingsgegevens nodig om deze API: NET laat uw tekstgegevens.</span><span class="sxs-lookup"><span data-stu-id="58346-110">No training data is needed to use this API: just bring your text data.</span></span> <span data-ttu-id="58346-111">Deze API maakt gebruik van geavanceerde natuurlijke taal verwerken technieken best in klasse voorspellingen leveren.</span><span class="sxs-lookup"><span data-stu-id="58346-111">This API uses advanced natural language processing techniques to deliver best in class predictions.</span></span>

<span data-ttu-id="58346-112">U kunt tekstanalyse in actie zien op onze [demo site](https://text-analytics-demo.azurewebsites.net/), waar u ook vinden [voorbeelden](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) over het implementeren van tekstanalyse in C# en Python.</span><span class="sxs-lookup"><span data-stu-id="58346-112">You can see text analytics in action on our [demo site](https://text-analytics-demo.azurewebsites.net/), where you will also find [samples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) on how to implement text analytics in C# and Python.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a><span data-ttu-id="58346-113">Sentimentanalyse</span><span class="sxs-lookup"><span data-stu-id="58346-113">Sentiment analysis</span></span>
<span data-ttu-id="58346-114">De API retourneert een numerieke score tussen 0 en 1.</span><span class="sxs-lookup"><span data-stu-id="58346-114">The API returns a numeric score between 0 & 1.</span></span> <span data-ttu-id="58346-115">Scores bijna 1 aangeven positief gevoel terwijl scores dicht bij 0 negatieve gevoel geven.</span><span class="sxs-lookup"><span data-stu-id="58346-115">Scores close to 1 indicate positive sentiment, while scores close to 0 indicate negative sentiment.</span></span> <span data-ttu-id="58346-116">Stemmingscores worden gegenereerd met classificatietechnieken.</span><span class="sxs-lookup"><span data-stu-id="58346-116">Sentiment score is generated using classification techniques.</span></span> <span data-ttu-id="58346-117">De functies van de invoer aan de classificatie behoren n-g, functies die worden gegenereerd op basis van het onderdeel van spraak tags en word insluitingen.</span><span class="sxs-lookup"><span data-stu-id="58346-117">The input features to the classifier include n-grams, features generated from part-of-speech tags, and word embeddings.</span></span> <span data-ttu-id="58346-118">Engels is momenteel de enige ondersteunde taal.</span><span class="sxs-lookup"><span data-stu-id="58346-118">Currently, English is the only supported language.</span></span>

## <a name="key-phrase-extraction"></a><span data-ttu-id="58346-119">Sleuteluitdrukkingen extraheren</span><span class="sxs-lookup"><span data-stu-id="58346-119">Key phrase extraction</span></span>
<span data-ttu-id="58346-120">De API retourneert een lijst met tekenreeksen die de belangrijkste gespreksonderwerpen in de invoertekst aanduiden.</span><span class="sxs-lookup"><span data-stu-id="58346-120">The API returns a list of strings denoting the key talking points in the input text.</span></span> <span data-ttu-id="58346-121">Er worden technieken uit de geavanceerde Natural Language Processing-toolkit van Microsoft Office gebruikt.</span><span class="sxs-lookup"><span data-stu-id="58346-121">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span></span> <span data-ttu-id="58346-122">Engels is momenteel de enige ondersteunde taal.</span><span class="sxs-lookup"><span data-stu-id="58346-122">Currently, English is the only supported language.</span></span>

## <a name="language-detection"></a><span data-ttu-id="58346-123">Taaldetectie</span><span class="sxs-lookup"><span data-stu-id="58346-123">Language detection</span></span>
<span data-ttu-id="58346-124">De API retourneert de taal aangetroffen en een numerieke score tussen 0 en 1.</span><span class="sxs-lookup"><span data-stu-id="58346-124">The API returns the detected language and a numeric score between 0 & 1.</span></span> <span data-ttu-id="58346-125">Scores dichtbij 1 geven aan dat het 100% zeker is dat de geïdentificeerde taal waar is.</span><span class="sxs-lookup"><span data-stu-id="58346-125">Scores close to 1 indicate 100% certainty that the identified language is true.</span></span> <span data-ttu-id="58346-126">Er worden in totaal 120 talen ondersteund.</span><span class="sxs-lookup"><span data-stu-id="58346-126">A total of 120 languages are supported.</span></span>

## <a name="topic-detection"></a><span data-ttu-id="58346-127">Onderwerpherkenning</span><span class="sxs-lookup"><span data-stu-id="58346-127">Topic detection</span></span>
<span data-ttu-id="58346-128">Dit is een nieuw uitgebrachte API welke retourneert de bovenste gedetecteerd onderwerpen voor een lijst met tekstrecords verzonden.</span><span class="sxs-lookup"><span data-stu-id="58346-128">This is a newly released API which returns the top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="58346-129">Een onderwerp wordt geïdentificeerd met een sleutelfrase die uit een of meer verwante woorden kan bestaan.</span><span class="sxs-lookup"><span data-stu-id="58346-129">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="58346-130">Deze API vereist dat er minimaal 100 tekstrecords worden ingediend, maar de API is ontworpen om onderwerpen in honderdduizenden records te detecteren.</span><span class="sxs-lookup"><span data-stu-id="58346-130">This API requires a minimum of 100 text records to be submitted, but is designed to detect topics across hundreds to thousands of records.</span></span> <span data-ttu-id="58346-131">Bij de API wordt er één transactie per ingediende tekstrecord in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="58346-131">Note that this API charges 1 transaction per text record submitted.</span></span> <span data-ttu-id="58346-132">De API is ontworpen voor korte, menselijke geschreven tekst zoals beoordelingen en feedback van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="58346-132">The API is designed to work well for short, human written text such as reviews and user feedback.</span></span>

- - -
## <a name="api-definition"></a><span data-ttu-id="58346-133">API-definitie</span><span class="sxs-lookup"><span data-stu-id="58346-133">API Definition</span></span>
### <a name="headers"></a><span data-ttu-id="58346-134">Headers</span><span class="sxs-lookup"><span data-stu-id="58346-134">Headers</span></span>
<span data-ttu-id="58346-135">Zorg ervoor dat u de juiste headers in uw aanvraag opnemen, als volgt moet:</span><span class="sxs-lookup"><span data-stu-id="58346-135">Ensure that you include the correct headers in your request, which should be as follows:</span></span>

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

<span data-ttu-id="58346-136">U vindt de accountsleutel uit uw account in de [Azure gegevens markt](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="58346-136">You can find your account key from your account in the [Azure Data Market](https://datamarket.azure.com/account/keys).</span></span> <span data-ttu-id="58346-137">Houd er rekening mee dat momenteel wordt alleen JSON voor invoer en uitvoer indelingen is geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="58346-137">Note that currently only JSON is accepted for input and output formats.</span></span> <span data-ttu-id="58346-138">XML wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="58346-138">XML is not supported.</span></span>

- - -
## <a name="single-response-apis"></a><span data-ttu-id="58346-139">Enkele Antwoordthread API 's</span><span class="sxs-lookup"><span data-stu-id="58346-139">Single Response APIs</span></span>
### <a name="getsentiment"></a><span data-ttu-id="58346-140">GetSentiment</span><span class="sxs-lookup"><span data-stu-id="58346-140">GetSentiment</span></span>
<span data-ttu-id="58346-141">**URL**</span><span class="sxs-lookup"><span data-stu-id="58346-141">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

<span data-ttu-id="58346-142">**Voorbeeld van een aanvraag**</span><span class="sxs-lookup"><span data-stu-id="58346-142">**Example request**</span></span>

<span data-ttu-id="58346-143">We aanvraagt gevoel analyse voor de zinsnede 'Hallo wereld' in de aanroep hieronder:</span><span class="sxs-lookup"><span data-stu-id="58346-143">In the call below, we are requesting sentiment analysis for the phrase "Hello World":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

<span data-ttu-id="58346-144">Het resultaat is een antwoord als volgt:</span><span class="sxs-lookup"><span data-stu-id="58346-144">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a><span data-ttu-id="58346-145">GetKeyPhrases</span><span class="sxs-lookup"><span data-stu-id="58346-145">GetKeyPhrases</span></span>
<span data-ttu-id="58346-146">**URL**</span><span class="sxs-lookup"><span data-stu-id="58346-146">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

<span data-ttu-id="58346-147">**Voorbeeld van een aanvraag**</span><span class="sxs-lookup"><span data-stu-id="58346-147">**Example request**</span></span>

<span data-ttu-id="58346-148">In de onderstaande aanroep aanvraagt we dat de sleutel vermeldingen gevonden in de tekst 'Dit is een fantastische hotel om te blijven, met unieke decor en beschrijvende medewerkers':</span><span class="sxs-lookup"><span data-stu-id="58346-148">In the call below, we are requesting the key phrases found in the text "It was a wonderful hotel to stay at, with unique decor and friendly staff":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

<span data-ttu-id="58346-149">Het resultaat is een antwoord als volgt:</span><span class="sxs-lookup"><span data-stu-id="58346-149">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a><span data-ttu-id="58346-150">GetLanguage</span><span class="sxs-lookup"><span data-stu-id="58346-150">GetLanguage</span></span>
<span data-ttu-id="58346-151">**URL**</span><span class="sxs-lookup"><span data-stu-id="58346-151">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

<span data-ttu-id="58346-152">**Voorbeeld van een aanvraag**</span><span class="sxs-lookup"><span data-stu-id="58346-152">**Example request**</span></span>

<span data-ttu-id="58346-153">In de onderstaande aanroep GET we aanvraagt voor de gevoel voor de sleutel zinnen in de tekst *Hallo wereld*</span><span class="sxs-lookup"><span data-stu-id="58346-153">In the GET call below, we are requesting for the sentiment for the key phrases in the text *Hello World*</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

<span data-ttu-id="58346-154">Het resultaat is een antwoord als volgt:</span><span class="sxs-lookup"><span data-stu-id="58346-154">This will return a response as follows:</span></span>

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

<span data-ttu-id="58346-155">**Optionele parameters:**</span><span class="sxs-lookup"><span data-stu-id="58346-155">**Optional parameters**</span></span>

<span data-ttu-id="58346-156">`NumberOfLanguagesToDetect`is een optionele parameter.</span><span class="sxs-lookup"><span data-stu-id="58346-156">`NumberOfLanguagesToDetect` is an optional parameter.</span></span> <span data-ttu-id="58346-157">De standaardwaarde is 1.</span><span class="sxs-lookup"><span data-stu-id="58346-157">The default is 1.</span></span>

- - -
## <a name="batch-apis"></a><span data-ttu-id="58346-158">Batch-API 's</span><span class="sxs-lookup"><span data-stu-id="58346-158">Batch APIs</span></span>
<span data-ttu-id="58346-159">De tekst Analytics-service kunt u doen gevoel en sleutel-zin extracties in batchmodus.</span><span class="sxs-lookup"><span data-stu-id="58346-159">The Text Analytics service allows you to do sentiment and key-phrase extractions in batch mode.</span></span> <span data-ttu-id="58346-160">Houd er rekening mee dat elk van de records met aantallen als één transactie verkregen.</span><span class="sxs-lookup"><span data-stu-id="58346-160">Note that each of the records scored counts as one transaction.</span></span> <span data-ttu-id="58346-161">Een voorbeeld: als u gevoel voor 1000 records in één aanroep vragen 1000 transacties wordt afgetrokken.</span><span class="sxs-lookup"><span data-stu-id="58346-161">As an example, if you request sentiment for 1000 records in a single call, 1000 transactions will be deducted.</span></span>

<span data-ttu-id="58346-162">Houd er rekening mee dat de id's opgegeven in het systeem de geretourneerd door het systeem-id's zijn.</span><span class="sxs-lookup"><span data-stu-id="58346-162">Note that the IDs entered into the system are the IDs returned by the system.</span></span> <span data-ttu-id="58346-163">De webservice controleert niet of deze id uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="58346-163">The web service does not check that these IDs are unique.</span></span> <span data-ttu-id="58346-164">Het is de verantwoordelijkheid van de aanroepfunctie uniekheid controleren.</span><span class="sxs-lookup"><span data-stu-id="58346-164">It is the responsibility of the caller to verify uniqueness.</span></span> 

### <a name="getsentimentbatch"></a><span data-ttu-id="58346-165">GetSentimentBatch</span><span class="sxs-lookup"><span data-stu-id="58346-165">GetSentimentBatch</span></span>
<span data-ttu-id="58346-166">**URL**</span><span class="sxs-lookup"><span data-stu-id="58346-166">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

<span data-ttu-id="58346-167">**Voorbeeld van een aanvraag**</span><span class="sxs-lookup"><span data-stu-id="58346-167">**Example request**</span></span>

<span data-ttu-id="58346-168">In de POST-aanroep hieronder aanvraagt we voor de patronen van de vermeldingen 'Hallo wereld', 'Hallo Foo wereld' en 'Hallo Mijn wereld' in de hoofdtekst van de aanvraag:</span><span class="sxs-lookup"><span data-stu-id="58346-168">In the POST call below, we are requesting for the sentiments of the phrases "Hello World", "Hello Foo World" and "Hello My World" in the body of the request:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

<span data-ttu-id="58346-169">Hoofdtekst van de aanvraag:</span><span class="sxs-lookup"><span data-stu-id="58346-169">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

<span data-ttu-id="58346-170">In het onderstaande antwoord, moet u de lijst met scores die zijn gekoppeld aan uw tekst-id's ophalen:</span><span class="sxs-lookup"><span data-stu-id="58346-170">In the response below, you get the list of scores associated with your text Ids:</span></span>

    {
      "odata.metadata":"<url>", 
      "SentimentBatch":
      [
        {"Score":0.9549767,"Id":"1"},
        {"Score":0.7767222,"Id":"2"},
        {"Score":0.8988889,"Id":"3"}
      ],  
      "Errors":[]
    }


- - -
### <a name="getkeyphrasesbatch"></a><span data-ttu-id="58346-171">GetKeyPhrasesBatch</span><span class="sxs-lookup"><span data-stu-id="58346-171">GetKeyPhrasesBatch</span></span>
<span data-ttu-id="58346-172">**URL**</span><span class="sxs-lookup"><span data-stu-id="58346-172">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="58346-173">**Voorbeeld van een aanvraag**</span><span class="sxs-lookup"><span data-stu-id="58346-173">**Example request**</span></span>

<span data-ttu-id="58346-174">In dit voorbeeld aanvraagt we voor de lijst met patronen voor de sleutel zinnen in de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="58346-174">In this example, we are requesting for the list of sentiments for the key phrases in the following texts:</span></span> 

* <span data-ttu-id="58346-175">"Er is een fantastische hotel om te blijven, met unieke decor en beschrijvende medewerkers"</span><span class="sxs-lookup"><span data-stu-id="58346-175">"It was a wonderful hotel to stay at, with unique decor and friendly staff"</span></span>
* <span data-ttu-id="58346-176">"Er is een fantastische build conferentie, met zeer interessante vertelt"</span><span class="sxs-lookup"><span data-stu-id="58346-176">"It was an amazing build conference, with very interesting talks"</span></span>
* <span data-ttu-id="58346-177">"Het verkeer is verschrikkelijke, ik drie uur naar de luchthaven besteed"</span><span class="sxs-lookup"><span data-stu-id="58346-177">"The traffic was terrible, I spent three hours going to the airport"</span></span>

<span data-ttu-id="58346-178">Deze aanvraag wordt gedaan als een POST-aanroep naar het eindpunt:</span><span class="sxs-lookup"><span data-stu-id="58346-178">This request is made as a POST call to the endpoint:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="58346-179">Hoofdtekst van de aanvraag:</span><span class="sxs-lookup"><span data-stu-id="58346-179">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel to stay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"The traffic was terrible, I spent three hours going to the airport"}
    ]}

<span data-ttu-id="58346-180">In het antwoord hieronder, moet u de lijst met belangrijke termen die zijn gekoppeld aan uw tekst-id's ophalen:</span><span class="sxs-lookup"><span data-stu-id="58346-180">In the response below, you get the list of key phrases associated with your text Ids:</span></span>

    { "odata.metadata":"<url>",
         "KeyPhrasesBatch":
        [
           {"KeyPhrases":["unique decor","friendly staff","wonderful hotel"],"Id":"1"},
           {"KeyPhrases":["amazing build conference","interesting talks"],"Id":"2"},
           {"KeyPhrases":["hours","traffic","airport"],"Id":"3" }
        ],
        "Errors":[]
    }

- - -
### <a name="getlanguagebatch"></a><span data-ttu-id="58346-181">GetLanguageBatch</span><span class="sxs-lookup"><span data-stu-id="58346-181">GetLanguageBatch</span></span>

<span data-ttu-id="58346-182">We aanvraagt taaldetectie voor twee tekst invoeren in de POST-aanroep hieronder:</span><span class="sxs-lookup"><span data-stu-id="58346-182">In the POST call below, we are requesting language detection for two text inputs:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

<span data-ttu-id="58346-183">Hoofdtekst van de aanvraag:</span><span class="sxs-lookup"><span data-stu-id="58346-183">Request body:</span></span>

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

<span data-ttu-id="58346-184">Hiermee wordt het volgende antwoord waar Engels is gedetecteerd in de eerste invoer- en Frans in de tweede invoer:</span><span class="sxs-lookup"><span data-stu-id="58346-184">This returns the following response, where English is detected in the first input and French in the second input:</span></span>

    {
       "LanguageBatch": [{
         "Id": "1",
         "DetectedLanguages": [{
            "Name": "English",
            "Iso6391Name": "en",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       },
       {
         "Id": "2",
         "DetectedLanguages": [{
            "Name": "French",
            "Iso6391Name": "fr",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       }],
       "Errors": []
    }

- - -
## <a name="topic-detection-apis"></a><span data-ttu-id="58346-185">Onderwerp Detection-API 's</span><span class="sxs-lookup"><span data-stu-id="58346-185">Topic Detection APIs</span></span>
<span data-ttu-id="58346-186">Dit is een nieuw uitgebrachte API welke retourneert de bovenste gedetecteerd onderwerpen voor een lijst met tekstrecords verzonden.</span><span class="sxs-lookup"><span data-stu-id="58346-186">This is a newly released API which returns the top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="58346-187">Een onderwerp wordt geïdentificeerd met een sleutelfrase die uit een of meer verwante woorden kan bestaan.</span><span class="sxs-lookup"><span data-stu-id="58346-187">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="58346-188">Bij de API wordt er één transactie per ingediende tekstrecord in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="58346-188">Note that this API charges 1 transaction per text record submitted.</span></span>

<span data-ttu-id="58346-189">Deze API vereist dat er minimaal 100 tekstrecords worden ingediend, maar de API is ontworpen om onderwerpen in honderdduizenden records te detecteren.</span><span class="sxs-lookup"><span data-stu-id="58346-189">This API requires a minimum of 100 text records to be submitted, but is designed to detect topics across hundreds to thousands of records.</span></span>

### <a name="topics--submit-job"></a><span data-ttu-id="58346-190">Onderwerpen – taak verzenden</span><span class="sxs-lookup"><span data-stu-id="58346-190">Topics – Submit job</span></span>
<span data-ttu-id="58346-191">**URL**</span><span class="sxs-lookup"><span data-stu-id="58346-191">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

<span data-ttu-id="58346-192">**Voorbeeld van een aanvraag**</span><span class="sxs-lookup"><span data-stu-id="58346-192">**Example request**</span></span>

<span data-ttu-id="58346-193">In de POST-aanroep hieronder vragen wij onderwerpen voor een set van 100 artikelen, waarbij de eerste en laatste invoer artikelen worden weergegeven en twee StopPhrases zijn opgenomen.</span><span class="sxs-lookup"><span data-stu-id="58346-193">In the POST call below, we are requesting topics for a set of 100 articles, where the first and last input articles are shown, and two StopPhrases are included.</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

<span data-ttu-id="58346-194">Hoofdtekst van de aanvraag:</span><span class="sxs-lookup"><span data-stu-id="58346-194">Request body:</span></span>

    {"Inputs":[
        {"Id":"1","Text":"I loved the food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated the decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

<span data-ttu-id="58346-195">In het antwoord hieronder, kunt u de taak-id voor de opgegeven taak opvragen:</span><span class="sxs-lookup"><span data-stu-id="58346-195">In the response below, you get the JobId for the submitted job:</span></span>

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

<span data-ttu-id="58346-196">Een lijst van één woord of meerdere word zinnen die niet moeten worden geretourneerd als onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="58346-196">A list of single word or multiple word phrases which should not be returned as topics.</span></span> <span data-ttu-id="58346-197">Kan worden gebruikt voor het filteren van zeer algemene onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="58346-197">Can be used to filter out very generic topics.</span></span> <span data-ttu-id="58346-198">Bijvoorbeeld in een gegevensset over hotel beoordelingen 'hotels' en 'hostel' mogelijk logisch stop zinnen.</span><span class="sxs-lookup"><span data-stu-id="58346-198">For example, in a dataset about hotel reviews, "hotel" and "hostel" may be sensible stop phrases.</span></span>  

### <a name="topics--poll-for-job-results"></a><span data-ttu-id="58346-199">Onderwerpen – Poll voor de resultaten van de taak</span><span class="sxs-lookup"><span data-stu-id="58346-199">Topics – Poll for job results</span></span>
<span data-ttu-id="58346-200">**URL**</span><span class="sxs-lookup"><span data-stu-id="58346-200">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

<span data-ttu-id="58346-201">**Voorbeeld van een aanvraag**</span><span class="sxs-lookup"><span data-stu-id="58346-201">**Example request**</span></span>

<span data-ttu-id="58346-202">De taak-id geretourneerd van de indienings-taakstap voor het ophalen van de resultaten worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="58346-202">Pass the JobId returned from the ‘Submit job’ step to fetch the results.</span></span> <span data-ttu-id="58346-203">Het is raadzaam dat u dit eindpunt per minuut tot en met Status aanroept = 'Complete' in het antwoord.</span><span class="sxs-lookup"><span data-stu-id="58346-203">We recommend that you call this endpoint every minute until Status=’Complete’ in the response.</span></span> <span data-ttu-id="58346-204">Het duurt ongeveer 10 minuten voor een taak voltooid of langer van taken met duizenden records.</span><span class="sxs-lookup"><span data-stu-id="58346-204">It will take around 10 mins for a job to complete, or longer for jobs with many thousands of records.</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


<span data-ttu-id="58346-205">Tijdens het verwerken van, zijn het antwoord als volgt:</span><span class="sxs-lookup"><span data-stu-id="58346-205">While it is processing, the response will be as follows:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


<span data-ttu-id="58346-206">De API wordt de uitvoer geretourneerd in JSON-indeling in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="58346-206">The API returns output in JSON format in the following format:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Finished",
        "TopicInfo":[
        {
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Score":8.0,
            "KeyPhrase":"food"
        },
        ...
        {
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Score":6.0,
            "KeyPhrase":"decor"
            }
          ],
        "TopicAssignment":[
        {
            "Id":"1",
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Distance":0.7809
        },
        ...
        {
            "Id":"100",
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Distance":0.8034
        }
        ],
        "Errors":[]


<span data-ttu-id="58346-207">De eigenschappen voor elk onderdeel van het antwoord zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="58346-207">The properties for each part of the response are as follows:</span></span>

<span data-ttu-id="58346-208">**TopicInfo eigenschappen**</span><span class="sxs-lookup"><span data-stu-id="58346-208">**TopicInfo properties**</span></span>

| <span data-ttu-id="58346-209">Sleutel</span><span class="sxs-lookup"><span data-stu-id="58346-209">Key</span></span> | <span data-ttu-id="58346-210">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="58346-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="58346-211">Onderwerpklasse</span><span class="sxs-lookup"><span data-stu-id="58346-211">TopicId</span></span> |<span data-ttu-id="58346-212">Een unieke id voor elk onderwerp.</span><span class="sxs-lookup"><span data-stu-id="58346-212">A unique identifier for each topic.</span></span> |
| <span data-ttu-id="58346-213">Score</span><span class="sxs-lookup"><span data-stu-id="58346-213">Score</span></span> |<span data-ttu-id="58346-214">Het aantal records dat is toegewezen aan het onderwerp.</span><span class="sxs-lookup"><span data-stu-id="58346-214">Count of records assigned to topic.</span></span> |
| <span data-ttu-id="58346-215">KeyPhrase</span><span class="sxs-lookup"><span data-stu-id="58346-215">KeyPhrase</span></span> |<span data-ttu-id="58346-216">Een samengevat woord of woordgroep voor het onderwerp.</span><span class="sxs-lookup"><span data-stu-id="58346-216">A summarizing word or phrase for the topic.</span></span> <span data-ttu-id="58346-217">1 of meer woorden kan zijn.</span><span class="sxs-lookup"><span data-stu-id="58346-217">Can be 1 or multiple words.</span></span> |

<span data-ttu-id="58346-218">**TopicAssignment eigenschappen**</span><span class="sxs-lookup"><span data-stu-id="58346-218">**TopicAssignment properties**</span></span>

| <span data-ttu-id="58346-219">Sleutel</span><span class="sxs-lookup"><span data-stu-id="58346-219">Key</span></span> | <span data-ttu-id="58346-220">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="58346-220">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="58346-221">Id</span><span class="sxs-lookup"><span data-stu-id="58346-221">Id</span></span> |<span data-ttu-id="58346-222">ID voor de record.</span><span class="sxs-lookup"><span data-stu-id="58346-222">Identifier for the record.</span></span> <span data-ttu-id="58346-223">Is gelijk aan de ID die is opgenomen in de invoer.</span><span class="sxs-lookup"><span data-stu-id="58346-223">Equates to the ID included in the input.</span></span> |
| <span data-ttu-id="58346-224">Onderwerpklasse</span><span class="sxs-lookup"><span data-stu-id="58346-224">TopicId</span></span> |<span data-ttu-id="58346-225">De onderwerp-ID die aan de record is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="58346-225">The topic ID which the record has been assigned to.</span></span> |
| <span data-ttu-id="58346-226">afstand</span><span class="sxs-lookup"><span data-stu-id="58346-226">Distance</span></span> |<span data-ttu-id="58346-227">Vertrouwen dat de record deel uitmaakt van het onderwerp.</span><span class="sxs-lookup"><span data-stu-id="58346-227">Confidence that the record belongs to the topic.</span></span> <span data-ttu-id="58346-228">Afstand dichter op nul geeft aan dat hoger vertrouwen.</span><span class="sxs-lookup"><span data-stu-id="58346-228">Distance closer to zero indicates higher confidence.</span></span> |

