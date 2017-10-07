---
title: 'Machine Learning API''s: Text Analytics | Microsoft Docs'
description: API's van Microsoft Machine Learning-Analytics tekst kan worden gebruikt tooanalyze ongestructureerde tekst voor gevoel analyse, uitpakken van sleutel woordgroep, taal wordt gedetecteerd en onderwerp detectie.
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
redirect_document_id: True
ms.openlocfilehash: 49380c83849c5d5fdd8dce4f3899ebcb3d6870f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a><span data-ttu-id="15ef7-103">API’s voor Machine Learning: Tekstanalyse voor sentimenten, Sleuteltermextractie, Taaldetectie en Onderwerpdetectie</span><span class="sxs-lookup"><span data-stu-id="15ef7-103">Machine Learning APIs: Text Analytics for Sentiment, Key Phrase Extraction, Language Detection and Topic Detection</span></span>
> [!NOTE]
> <span data-ttu-id="15ef7-104">Deze handleiding is bedoeld voor versie 1 van Hallo API.</span><span class="sxs-lookup"><span data-stu-id="15ef7-104">This guide is for version 1 of hello API.</span></span> <span data-ttu-id="15ef7-105">Voor versie 2, [ **toothis document verwijzen**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="15ef7-105">For version 2, [**refer toothis document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span></span> <span data-ttu-id="15ef7-106">Versie 2 is nu Hallo aanbevolen versie van deze API.</span><span class="sxs-lookup"><span data-stu-id="15ef7-106">Version 2 is now hello preferred version of this API.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="15ef7-107">Overzicht</span><span class="sxs-lookup"><span data-stu-id="15ef7-107">Overview</span></span>
<span data-ttu-id="15ef7-108">Hallo Text Analytics API is een suite met tekstanalyse [webservices](https://datamarket.azure.com/dataset/amla/text-analytics) gebouwd met Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="15ef7-108">hello Text Analytics API is a suite of text analytics [web services](https://datamarket.azure.com/dataset/amla/text-analytics) built with Azure Machine Learning.</span></span> <span data-ttu-id="15ef7-109">Hallo API kan worden gebruikt tooanalyze ongestructureerde tekst voor taken zoals gevoel analyse, uitpakken van sleutel woordgroep, taal wordt gedetecteerd en onderwerp detectie.</span><span class="sxs-lookup"><span data-stu-id="15ef7-109">hello API can be used tooanalyze unstructured text for tasks such as sentiment analysis, key phrase extraction, language detection and topic detection.</span></span> <span data-ttu-id="15ef7-110">Er zijn geen gegevens training nodig toouse deze API: NET laat uw tekstgegevens.</span><span class="sxs-lookup"><span data-stu-id="15ef7-110">No training data is needed toouse this API: just bring your text data.</span></span> <span data-ttu-id="15ef7-111">Deze API maakt gebruik van geavanceerde natuurlijke taal technieken toodeliver beste worden verwerkt in de klasse voorspellingen.</span><span class="sxs-lookup"><span data-stu-id="15ef7-111">This API uses advanced natural language processing techniques toodeliver best in class predictions.</span></span>

<span data-ttu-id="15ef7-112">U kunt tekstanalyse in actie zien op onze [demo site](https://text-analytics-demo.azurewebsites.net/), waar u ook vinden [voorbeelden](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) over het tooimplement tekstanalyse in C# en Python.</span><span class="sxs-lookup"><span data-stu-id="15ef7-112">You can see text analytics in action on our [demo site](https://text-analytics-demo.azurewebsites.net/), where you will also find [samples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) on how tooimplement text analytics in C# and Python.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a><span data-ttu-id="15ef7-113">Sentimentanalyse</span><span class="sxs-lookup"><span data-stu-id="15ef7-113">Sentiment analysis</span></span>
<span data-ttu-id="15ef7-114">Hallo API retourneert een numerieke score tussen 0 en 1.</span><span class="sxs-lookup"><span data-stu-id="15ef7-114">hello API returns a numeric score between 0 & 1.</span></span> <span data-ttu-id="15ef7-115">Scores sluiten too1 aangeven positief gevoel terwijl scores sluiten too0 negatieve gevoel geven.</span><span class="sxs-lookup"><span data-stu-id="15ef7-115">Scores close too1 indicate positive sentiment, while scores close too0 indicate negative sentiment.</span></span> <span data-ttu-id="15ef7-116">Stemmingscores worden gegenereerd met classificatietechnieken.</span><span class="sxs-lookup"><span data-stu-id="15ef7-116">Sentiment score is generated using classification techniques.</span></span> <span data-ttu-id="15ef7-117">Hallo invoer functies toohello classificatie n-g, functies die worden gegenereerd op basis van het onderdeel van spraak tags en word insluitingen bevatten.</span><span class="sxs-lookup"><span data-stu-id="15ef7-117">hello input features toohello classifier include n-grams, features generated from part-of-speech tags, and word embeddings.</span></span> <span data-ttu-id="15ef7-118">Engels is momenteel alleen ondersteund taal Hallo.</span><span class="sxs-lookup"><span data-stu-id="15ef7-118">Currently, English is hello only supported language.</span></span>

## <a name="key-phrase-extraction"></a><span data-ttu-id="15ef7-119">Sleuteluitdrukkingen extraheren</span><span class="sxs-lookup"><span data-stu-id="15ef7-119">Key phrase extraction</span></span>
<span data-ttu-id="15ef7-120">Hallo API retourneert een lijst met tekenreeksen die aangeeft Hallo sleutel bespreken punten in de ingevoerde tekst hello.</span><span class="sxs-lookup"><span data-stu-id="15ef7-120">hello API returns a list of strings denoting hello key talking points in hello input text.</span></span> <span data-ttu-id="15ef7-121">Er worden technieken uit de geavanceerde Natural Language Processing-toolkit van Microsoft Office gebruikt.</span><span class="sxs-lookup"><span data-stu-id="15ef7-121">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span></span> <span data-ttu-id="15ef7-122">Engels is momenteel alleen ondersteund taal Hallo.</span><span class="sxs-lookup"><span data-stu-id="15ef7-122">Currently, English is hello only supported language.</span></span>

## <a name="language-detection"></a><span data-ttu-id="15ef7-123">Taaldetectie</span><span class="sxs-lookup"><span data-stu-id="15ef7-123">Language detection</span></span>
<span data-ttu-id="15ef7-124">Hallo API retourneert Hallo gedetecteerd taal en een numerieke score tussen 0 en 1.</span><span class="sxs-lookup"><span data-stu-id="15ef7-124">hello API returns hello detected language and a numeric score between 0 & 1.</span></span> <span data-ttu-id="15ef7-125">Scores sluiten too1 duiden op 100% zekerheid Hallo geïdentificeerd taal is ingesteld op true.</span><span class="sxs-lookup"><span data-stu-id="15ef7-125">Scores close too1 indicate 100% certainty that hello identified language is true.</span></span> <span data-ttu-id="15ef7-126">Er worden in totaal 120 talen ondersteund.</span><span class="sxs-lookup"><span data-stu-id="15ef7-126">A total of 120 languages are supported.</span></span>

## <a name="topic-detection"></a><span data-ttu-id="15ef7-127">Onderwerpherkenning</span><span class="sxs-lookup"><span data-stu-id="15ef7-127">Topic detection</span></span>
<span data-ttu-id="15ef7-128">Dit is een nieuw uitgebrachte API Hallo bovenste gedetecteerde onderwerpen voor een lijst met verzonden tekstrecords geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="15ef7-128">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="15ef7-129">Een onderwerp wordt geïdentificeerd met een sleutelfrase die uit een of meer verwante woorden kan bestaan.</span><span class="sxs-lookup"><span data-stu-id="15ef7-129">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="15ef7-130">Deze API vereist een minimum van 100 tekst registreert toobe verzonden, maar is ontworpen toodetect onderwerpen over honderden toothousands met records.</span><span class="sxs-lookup"><span data-stu-id="15ef7-130">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span> <span data-ttu-id="15ef7-131">Bij de API wordt er één transactie per ingediende tekstrecord in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="15ef7-131">Note that this API charges 1 transaction per text record submitted.</span></span> <span data-ttu-id="15ef7-132">Hallo API is ontworpen toowork voor korte human tekst zoals beoordelingen en feedback van gebruikers geschreven.</span><span class="sxs-lookup"><span data-stu-id="15ef7-132">hello API is designed toowork well for short, human written text such as reviews and user feedback.</span></span>

- - -
## <a name="api-definition"></a><span data-ttu-id="15ef7-133">API-definitie</span><span class="sxs-lookup"><span data-stu-id="15ef7-133">API Definition</span></span>
### <a name="headers"></a><span data-ttu-id="15ef7-134">Headers</span><span class="sxs-lookup"><span data-stu-id="15ef7-134">Headers</span></span>
<span data-ttu-id="15ef7-135">Zorg ervoor dat u de juiste headers Hallo in uw aanvraag opneemt, als volgt moet:</span><span class="sxs-lookup"><span data-stu-id="15ef7-135">Ensure that you include hello correct headers in your request, which should be as follows:</span></span>

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

<span data-ttu-id="15ef7-136">U vindt de accountsleutel uit uw account in Hallo [Azure gegevens markt](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="15ef7-136">You can find your account key from your account in hello [Azure Data Market](https://datamarket.azure.com/account/keys).</span></span> <span data-ttu-id="15ef7-137">Houd er rekening mee dat momenteel wordt alleen JSON voor invoer en uitvoer indelingen is geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="15ef7-137">Note that currently only JSON is accepted for input and output formats.</span></span> <span data-ttu-id="15ef7-138">XML wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="15ef7-138">XML is not supported.</span></span>

- - -
## <a name="single-response-apis"></a><span data-ttu-id="15ef7-139">Enkele Antwoordthread API 's</span><span class="sxs-lookup"><span data-stu-id="15ef7-139">Single Response APIs</span></span>
### <a name="getsentiment"></a><span data-ttu-id="15ef7-140">GetSentiment</span><span class="sxs-lookup"><span data-stu-id="15ef7-140">GetSentiment</span></span>
<span data-ttu-id="15ef7-141">**URL**</span><span class="sxs-lookup"><span data-stu-id="15ef7-141">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

<span data-ttu-id="15ef7-142">**Voorbeeld van een aanvraag**</span><span class="sxs-lookup"><span data-stu-id="15ef7-142">**Example request**</span></span>

<span data-ttu-id="15ef7-143">We aanvraagt gevoel analyse voor de zinsnede Hallo "Hallo wereld" in het Hallo-aanroep die hieronder wordt:</span><span class="sxs-lookup"><span data-stu-id="15ef7-143">In hello call below, we are requesting sentiment analysis for hello phrase "Hello World":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

<span data-ttu-id="15ef7-144">Het resultaat is een antwoord als volgt:</span><span class="sxs-lookup"><span data-stu-id="15ef7-144">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a><span data-ttu-id="15ef7-145">GetKeyPhrases</span><span class="sxs-lookup"><span data-stu-id="15ef7-145">GetKeyPhrases</span></span>
<span data-ttu-id="15ef7-146">**URL**</span><span class="sxs-lookup"><span data-stu-id="15ef7-146">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

<span data-ttu-id="15ef7-147">**Voorbeeld van een aanvraag**</span><span class="sxs-lookup"><span data-stu-id="15ef7-147">**Example request**</span></span>

<span data-ttu-id="15ef7-148">In het Hallo-aanroep die hieronder wordt aanvraagt we Hallo sleutel zinnen gevonden in de tekst hello 'Was een fantastische hotel toostay op, met unieke decor en beschrijvende medewerkers':</span><span class="sxs-lookup"><span data-stu-id="15ef7-148">In hello call below, we are requesting hello key phrases found in hello text "It was a wonderful hotel toostay at, with unique decor and friendly staff":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

<span data-ttu-id="15ef7-149">Het resultaat is een antwoord als volgt:</span><span class="sxs-lookup"><span data-stu-id="15ef7-149">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a><span data-ttu-id="15ef7-150">GetLanguage</span><span class="sxs-lookup"><span data-stu-id="15ef7-150">GetLanguage</span></span>
<span data-ttu-id="15ef7-151">**URL**</span><span class="sxs-lookup"><span data-stu-id="15ef7-151">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

<span data-ttu-id="15ef7-152">**Voorbeeld van een aanvraag**</span><span class="sxs-lookup"><span data-stu-id="15ef7-152">**Example request**</span></span>

<span data-ttu-id="15ef7-153">Hallo GET-aanroep hieronder, we aanvraagt voor Hallo gevoel voor belangrijke zinnen Hallo tekst hello *Hallo wereld*</span><span class="sxs-lookup"><span data-stu-id="15ef7-153">In hello GET call below, we are requesting for hello sentiment for hello key phrases in hello text *Hello World*</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

<span data-ttu-id="15ef7-154">Het resultaat is een antwoord als volgt:</span><span class="sxs-lookup"><span data-stu-id="15ef7-154">This will return a response as follows:</span></span>

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

<span data-ttu-id="15ef7-155">**Optionele parameters:**</span><span class="sxs-lookup"><span data-stu-id="15ef7-155">**Optional parameters**</span></span>

<span data-ttu-id="15ef7-156">`NumberOfLanguagesToDetect`is een optionele parameter.</span><span class="sxs-lookup"><span data-stu-id="15ef7-156">`NumberOfLanguagesToDetect` is an optional parameter.</span></span> <span data-ttu-id="15ef7-157">Hallo standaardwaarde is 1.</span><span class="sxs-lookup"><span data-stu-id="15ef7-157">hello default is 1.</span></span>

- - -
## <a name="batch-apis"></a><span data-ttu-id="15ef7-158">Batch-API 's</span><span class="sxs-lookup"><span data-stu-id="15ef7-158">Batch APIs</span></span>
<span data-ttu-id="15ef7-159">Hallo Text Analytics-service kunt u toodo gevoel en sleutel-zin extracties in batchmodus.</span><span class="sxs-lookup"><span data-stu-id="15ef7-159">hello Text Analytics service allows you toodo sentiment and key-phrase extractions in batch mode.</span></span> <span data-ttu-id="15ef7-160">Houd er rekening mee dat elk van de records Hallo aantallen als één transactie verkregen.</span><span class="sxs-lookup"><span data-stu-id="15ef7-160">Note that each of hello records scored counts as one transaction.</span></span> <span data-ttu-id="15ef7-161">Een voorbeeld: als u gevoel voor 1000 records in één aanroep vragen 1000 transacties wordt afgetrokken.</span><span class="sxs-lookup"><span data-stu-id="15ef7-161">As an example, if you request sentiment for 1000 records in a single call, 1000 transactions will be deducted.</span></span>

<span data-ttu-id="15ef7-162">Let op: Hallo-id's in Hallo systeem ingevoerd zijn Hallo-id's die zijn geretourneerd door Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="15ef7-162">Note that hello IDs entered into hello system are hello IDs returned by hello system.</span></span> <span data-ttu-id="15ef7-163">Hallo-webservice wordt niet gecontroleerd of deze id uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="15ef7-163">hello web service does not check that these IDs are unique.</span></span> <span data-ttu-id="15ef7-164">Het is de verantwoordelijkheid Hallo van Hallo aanroeper tooverify uniekheid.</span><span class="sxs-lookup"><span data-stu-id="15ef7-164">It is hello responsibility of hello caller tooverify uniqueness.</span></span> 

### <a name="getsentimentbatch"></a><span data-ttu-id="15ef7-165">GetSentimentBatch</span><span class="sxs-lookup"><span data-stu-id="15ef7-165">GetSentimentBatch</span></span>
<span data-ttu-id="15ef7-166">**URL**</span><span class="sxs-lookup"><span data-stu-id="15ef7-166">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

<span data-ttu-id="15ef7-167">**Voorbeeld van een aanvraag**</span><span class="sxs-lookup"><span data-stu-id="15ef7-167">**Example request**</span></span>

<span data-ttu-id="15ef7-168">In Hallo POST roept hieronder, wij zijn aangevraagd voor Hallo patronen Hallo woordgroepen "Hello World", "Wereld Hallo Foo" en "Hello mijn World" in de hoofdtekst Hallo van Hallo-aanvraag:</span><span class="sxs-lookup"><span data-stu-id="15ef7-168">In hello POST call below, we are requesting for hello sentiments of hello phrases "Hello World", "Hello Foo World" and "Hello My World" in hello body of hello request:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

<span data-ttu-id="15ef7-169">Hoofdtekst van de aanvraag:</span><span class="sxs-lookup"><span data-stu-id="15ef7-169">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

<span data-ttu-id="15ef7-170">Hallo-antwoord hieronder wordt ophalen u Hallo lijst met scores die zijn gekoppeld aan uw tekst-id's:</span><span class="sxs-lookup"><span data-stu-id="15ef7-170">In hello response below, you get hello list of scores associated with your text Ids:</span></span>

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
### <a name="getkeyphrasesbatch"></a><span data-ttu-id="15ef7-171">GetKeyPhrasesBatch</span><span class="sxs-lookup"><span data-stu-id="15ef7-171">GetKeyPhrasesBatch</span></span>
<span data-ttu-id="15ef7-172">**URL**</span><span class="sxs-lookup"><span data-stu-id="15ef7-172">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="15ef7-173">**Voorbeeld van een aanvraag**</span><span class="sxs-lookup"><span data-stu-id="15ef7-173">**Example request**</span></span>

<span data-ttu-id="15ef7-174">In dit voorbeeld aanvraagt we voor Hallo lijst met patronen voor Hallo sleutel zinnen in Hallo teksten te volgen:</span><span class="sxs-lookup"><span data-stu-id="15ef7-174">In this example, we are requesting for hello list of sentiments for hello key phrases in hello following texts:</span></span> 

* <span data-ttu-id="15ef7-175">"Er is een fantastische hotel toostay op, met unieke decor en beschrijvende medewerkers"</span><span class="sxs-lookup"><span data-stu-id="15ef7-175">"It was a wonderful hotel toostay at, with unique decor and friendly staff"</span></span>
* <span data-ttu-id="15ef7-176">"Er is een fantastische build conferentie, met zeer interessante vertelt"</span><span class="sxs-lookup"><span data-stu-id="15ef7-176">"It was an amazing build conference, with very interesting talks"</span></span>
* <span data-ttu-id="15ef7-177">"Hallo verkeer is verschrikkelijke, ik drie uur gebeurt toohello luchthaven besteed"</span><span class="sxs-lookup"><span data-stu-id="15ef7-177">"hello traffic was terrible, I spent three hours going toohello airport"</span></span>

<span data-ttu-id="15ef7-178">Deze aanvraag wordt gedaan als een POST-aanroep toohello eindpunt:</span><span class="sxs-lookup"><span data-stu-id="15ef7-178">This request is made as a POST call toohello endpoint:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="15ef7-179">Hoofdtekst van de aanvraag:</span><span class="sxs-lookup"><span data-stu-id="15ef7-179">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

<span data-ttu-id="15ef7-180">Hallo-antwoord hieronder wordt ophalen u Hallo-lijst met belangrijke termen die zijn gekoppeld aan uw tekst-id's:</span><span class="sxs-lookup"><span data-stu-id="15ef7-180">In hello response below, you get hello list of key phrases associated with your text Ids:</span></span>

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
### <a name="getlanguagebatch"></a><span data-ttu-id="15ef7-181">GetLanguageBatch</span><span class="sxs-lookup"><span data-stu-id="15ef7-181">GetLanguageBatch</span></span>

<span data-ttu-id="15ef7-182">We aanvraagt taaldetectie voor twee tekst invoeren in Hallo POST-aanroep die hieronder wordt:</span><span class="sxs-lookup"><span data-stu-id="15ef7-182">In hello POST call below, we are requesting language detection for two text inputs:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

<span data-ttu-id="15ef7-183">Hoofdtekst van de aanvraag:</span><span class="sxs-lookup"><span data-stu-id="15ef7-183">Request body:</span></span>

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

<span data-ttu-id="15ef7-184">Hiermee wordt de Hallo na antwoord, waarbij Engels is gedetecteerd in hello eerste invoer- en Frans in Hallo tweede invoer:</span><span class="sxs-lookup"><span data-stu-id="15ef7-184">This returns hello following response, where English is detected in hello first input and French in hello second input:</span></span>

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
## <a name="topic-detection-apis"></a><span data-ttu-id="15ef7-185">Onderwerp Detection-API 's</span><span class="sxs-lookup"><span data-stu-id="15ef7-185">Topic Detection APIs</span></span>
<span data-ttu-id="15ef7-186">Dit is een nieuw uitgebrachte API Hallo bovenste gedetecteerde onderwerpen voor een lijst met verzonden tekstrecords geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="15ef7-186">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="15ef7-187">Een onderwerp wordt geïdentificeerd met een sleutelfrase die uit een of meer verwante woorden kan bestaan.</span><span class="sxs-lookup"><span data-stu-id="15ef7-187">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="15ef7-188">Bij de API wordt er één transactie per ingediende tekstrecord in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="15ef7-188">Note that this API charges 1 transaction per text record submitted.</span></span>

<span data-ttu-id="15ef7-189">Deze API vereist een minimum van 100 tekst registreert toobe verzonden, maar is ontworpen toodetect onderwerpen over honderden toothousands met records.</span><span class="sxs-lookup"><span data-stu-id="15ef7-189">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span>

### <a name="topics--submit-job"></a><span data-ttu-id="15ef7-190">Onderwerpen – taak verzenden</span><span class="sxs-lookup"><span data-stu-id="15ef7-190">Topics – Submit job</span></span>
<span data-ttu-id="15ef7-191">**URL**</span><span class="sxs-lookup"><span data-stu-id="15ef7-191">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

<span data-ttu-id="15ef7-192">**Voorbeeld van een aanvraag**</span><span class="sxs-lookup"><span data-stu-id="15ef7-192">**Example request**</span></span>

<span data-ttu-id="15ef7-193">Hallo POST-aanroep hieronder vragen we onderwerpen voor een set van 100 artikelen, waarbij Hallo voornaam en achternaam invoer artikelen worden weergegeven en twee StopPhrases zijn opgenomen.</span><span class="sxs-lookup"><span data-stu-id="15ef7-193">In hello POST call below, we are requesting topics for a set of 100 articles, where hello first and last input articles are shown, and two StopPhrases are included.</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

<span data-ttu-id="15ef7-194">Hoofdtekst van de aanvraag:</span><span class="sxs-lookup"><span data-stu-id="15ef7-194">Request body:</span></span>

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

<span data-ttu-id="15ef7-195">Hallo-antwoord hieronder wordt ophalen u Hallo JobId voor Hallo ingediende taak:</span><span class="sxs-lookup"><span data-stu-id="15ef7-195">In hello response below, you get hello JobId for hello submitted job:</span></span>

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

<span data-ttu-id="15ef7-196">Een lijst van één woord of meerdere word zinnen die niet moeten worden geretourneerd als onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="15ef7-196">A list of single word or multiple word phrases which should not be returned as topics.</span></span> <span data-ttu-id="15ef7-197">Kan worden gebruikt toofilter uit zeer algemene onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="15ef7-197">Can be used toofilter out very generic topics.</span></span> <span data-ttu-id="15ef7-198">Bijvoorbeeld in een gegevensset over hotel beoordelingen 'hotels' en 'hostel' mogelijk logisch stop zinnen.</span><span class="sxs-lookup"><span data-stu-id="15ef7-198">For example, in a dataset about hotel reviews, "hotel" and "hostel" may be sensible stop phrases.</span></span>  

### <a name="topics--poll-for-job-results"></a><span data-ttu-id="15ef7-199">Onderwerpen – Poll voor de resultaten van de taak</span><span class="sxs-lookup"><span data-stu-id="15ef7-199">Topics – Poll for job results</span></span>
<span data-ttu-id="15ef7-200">**URL**</span><span class="sxs-lookup"><span data-stu-id="15ef7-200">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

<span data-ttu-id="15ef7-201">**Voorbeeld van een aanvraag**</span><span class="sxs-lookup"><span data-stu-id="15ef7-201">**Example request**</span></span>

<span data-ttu-id="15ef7-202">Hallo die JobId geretourneerd uit Hallo indienings-taak stap toofetch Hallo resultaten worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="15ef7-202">Pass hello JobId returned from hello ‘Submit job’ step toofetch hello results.</span></span> <span data-ttu-id="15ef7-203">Het is raadzaam dat u dit eindpunt per minuut tot en met Status aanroept = 'Complete' hello reactie.</span><span class="sxs-lookup"><span data-stu-id="15ef7-203">We recommend that you call this endpoint every minute until Status=’Complete’ in hello response.</span></span> <span data-ttu-id="15ef7-204">Het duurt ongeveer 10 minuten of langer van taken met duizenden records voor een toocomplete taak.</span><span class="sxs-lookup"><span data-stu-id="15ef7-204">It will take around 10 mins for a job toocomplete, or longer for jobs with many thousands of records.</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


<span data-ttu-id="15ef7-205">Tijdens het verwerken van, zijn antwoord Hallo als volgt:</span><span class="sxs-lookup"><span data-stu-id="15ef7-205">While it is processing, hello response will be as follows:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


<span data-ttu-id="15ef7-206">Hallo API retourneert uitvoer in JSON-indeling in de volgende indeling Hallo:</span><span class="sxs-lookup"><span data-stu-id="15ef7-206">hello API returns output in JSON format in hello following format:</span></span>

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


<span data-ttu-id="15ef7-207">Hallo-eigenschappen voor elk onderdeel van het antwoord Hallo zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="15ef7-207">hello properties for each part of hello response are as follows:</span></span>

<span data-ttu-id="15ef7-208">**TopicInfo eigenschappen**</span><span class="sxs-lookup"><span data-stu-id="15ef7-208">**TopicInfo properties**</span></span>

| <span data-ttu-id="15ef7-209">Sleutel</span><span class="sxs-lookup"><span data-stu-id="15ef7-209">Key</span></span> | <span data-ttu-id="15ef7-210">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="15ef7-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="15ef7-211">Onderwerpklasse</span><span class="sxs-lookup"><span data-stu-id="15ef7-211">TopicId</span></span> |<span data-ttu-id="15ef7-212">Een unieke id voor elk onderwerp.</span><span class="sxs-lookup"><span data-stu-id="15ef7-212">A unique identifier for each topic.</span></span> |
| <span data-ttu-id="15ef7-213">Score</span><span class="sxs-lookup"><span data-stu-id="15ef7-213">Score</span></span> |<span data-ttu-id="15ef7-214">Het aantal records tootopic toegewezen.</span><span class="sxs-lookup"><span data-stu-id="15ef7-214">Count of records assigned tootopic.</span></span> |
| <span data-ttu-id="15ef7-215">KeyPhrase</span><span class="sxs-lookup"><span data-stu-id="15ef7-215">KeyPhrase</span></span> |<span data-ttu-id="15ef7-216">Een samengevat woord of woordgroep voor Hallo onderwerp.</span><span class="sxs-lookup"><span data-stu-id="15ef7-216">A summarizing word or phrase for hello topic.</span></span> <span data-ttu-id="15ef7-217">1 of meer woorden kan zijn.</span><span class="sxs-lookup"><span data-stu-id="15ef7-217">Can be 1 or multiple words.</span></span> |

<span data-ttu-id="15ef7-218">**TopicAssignment eigenschappen**</span><span class="sxs-lookup"><span data-stu-id="15ef7-218">**TopicAssignment properties**</span></span>

| <span data-ttu-id="15ef7-219">Sleutel</span><span class="sxs-lookup"><span data-stu-id="15ef7-219">Key</span></span> | <span data-ttu-id="15ef7-220">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="15ef7-220">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="15ef7-221">Id</span><span class="sxs-lookup"><span data-stu-id="15ef7-221">Id</span></span> |<span data-ttu-id="15ef7-222">ID voor Hallo record.</span><span class="sxs-lookup"><span data-stu-id="15ef7-222">Identifier for hello record.</span></span> <span data-ttu-id="15ef7-223">Opgenomen in invoer Hallo toohello-ID is gelijk.</span><span class="sxs-lookup"><span data-stu-id="15ef7-223">Equates toohello ID included in hello input.</span></span> |
| <span data-ttu-id="15ef7-224">Onderwerpklasse</span><span class="sxs-lookup"><span data-stu-id="15ef7-224">TopicId</span></span> |<span data-ttu-id="15ef7-225">onderwerp-ID Hallo welke Hallo-record is toegewezen aan.</span><span class="sxs-lookup"><span data-stu-id="15ef7-225">hello topic ID which hello record has been assigned to.</span></span> |
| <span data-ttu-id="15ef7-226">afstand</span><span class="sxs-lookup"><span data-stu-id="15ef7-226">Distance</span></span> |<span data-ttu-id="15ef7-227">Vertrouwen dat Hallo record toohello onderwerp behoort.</span><span class="sxs-lookup"><span data-stu-id="15ef7-227">Confidence that hello record belongs toohello topic.</span></span> <span data-ttu-id="15ef7-228">Afstand dichter toozero geeft hoger vertrouwen.</span><span class="sxs-lookup"><span data-stu-id="15ef7-228">Distance closer toozero indicates higher confidence.</span></span> |

