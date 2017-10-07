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
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a>API’s voor Machine Learning: Tekstanalyse voor sentimenten, Sleuteltermextractie, Taaldetectie en Onderwerpdetectie
> [!NOTE]
> Deze handleiding is bedoeld voor versie 1 van Hallo API. Voor versie 2, [ **toothis document verwijzen**](../cognitive-services/cognitive-services-text-analytics-quick-start.md). Versie 2 is nu Hallo aanbevolen versie van deze API.
> 
> 

## <a name="overview"></a>Overzicht
Hallo Text Analytics API is een suite met tekstanalyse [webservices](https://datamarket.azure.com/dataset/amla/text-analytics) gebouwd met Azure Machine Learning. Hallo API kan worden gebruikt tooanalyze ongestructureerde tekst voor taken zoals gevoel analyse, uitpakken van sleutel woordgroep, taal wordt gedetecteerd en onderwerp detectie. Er zijn geen gegevens training nodig toouse deze API: NET laat uw tekstgegevens. Deze API maakt gebruik van geavanceerde natuurlijke taal technieken toodeliver beste worden verwerkt in de klasse voorspellingen.

U kunt tekstanalyse in actie zien op onze [demo site](https://text-analytics-demo.azurewebsites.net/), waar u ook vinden [voorbeelden](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) over het tooimplement tekstanalyse in C# en Python.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a>Sentimentanalyse
Hallo API retourneert een numerieke score tussen 0 en 1. Scores sluiten too1 aangeven positief gevoel terwijl scores sluiten too0 negatieve gevoel geven. Stemmingscores worden gegenereerd met classificatietechnieken. Hallo invoer functies toohello classificatie n-g, functies die worden gegenereerd op basis van het onderdeel van spraak tags en word insluitingen bevatten. Engels is momenteel alleen ondersteund taal Hallo.

## <a name="key-phrase-extraction"></a>Sleuteluitdrukkingen extraheren
Hallo API retourneert een lijst met tekenreeksen die aangeeft Hallo sleutel bespreken punten in de ingevoerde tekst hello. Er worden technieken uit de geavanceerde Natural Language Processing-toolkit van Microsoft Office gebruikt. Engels is momenteel alleen ondersteund taal Hallo.

## <a name="language-detection"></a>Taaldetectie
Hallo API retourneert Hallo gedetecteerd taal en een numerieke score tussen 0 en 1. Scores sluiten too1 duiden op 100% zekerheid Hallo geïdentificeerd taal is ingesteld op true. Er worden in totaal 120 talen ondersteund.

## <a name="topic-detection"></a>Onderwerpherkenning
Dit is een nieuw uitgebrachte API Hallo bovenste gedetecteerde onderwerpen voor een lijst met verzonden tekstrecords geretourneerd. Een onderwerp wordt geïdentificeerd met een sleutelfrase die uit een of meer verwante woorden kan bestaan. Deze API vereist een minimum van 100 tekst registreert toobe verzonden, maar is ontworpen toodetect onderwerpen over honderden toothousands met records. Bij de API wordt er één transactie per ingediende tekstrecord in rekening gebracht. Hallo API is ontworpen toowork voor korte human tekst zoals beoordelingen en feedback van gebruikers geschreven.

- - -
## <a name="api-definition"></a>API-definitie
### <a name="headers"></a>Headers
Zorg ervoor dat u de juiste headers Hallo in uw aanvraag opneemt, als volgt moet:

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

U vindt de accountsleutel uit uw account in Hallo [Azure gegevens markt](https://datamarket.azure.com/account/keys). Houd er rekening mee dat momenteel wordt alleen JSON voor invoer en uitvoer indelingen is geaccepteerd. XML wordt niet ondersteund.

- - -
## <a name="single-response-apis"></a>Enkele Antwoordthread API 's
### <a name="getsentiment"></a>GetSentiment
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

**Voorbeeld van een aanvraag**

We aanvraagt gevoel analyse voor de zinsnede Hallo "Hallo wereld" in het Hallo-aanroep die hieronder wordt:

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

Het resultaat is een antwoord als volgt:

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a>GetKeyPhrases
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

**Voorbeeld van een aanvraag**

In het Hallo-aanroep die hieronder wordt aanvraagt we Hallo sleutel zinnen gevonden in de tekst hello 'Was een fantastische hotel toostay op, met unieke decor en beschrijvende medewerkers':

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

Het resultaat is een antwoord als volgt:

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a>GetLanguage
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

**Voorbeeld van een aanvraag**

Hallo GET-aanroep hieronder, we aanvraagt voor Hallo gevoel voor belangrijke zinnen Hallo tekst hello *Hallo wereld*

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

Het resultaat is een antwoord als volgt:

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

**Optionele parameters:**

`NumberOfLanguagesToDetect`is een optionele parameter. Hallo standaardwaarde is 1.

- - -
## <a name="batch-apis"></a>Batch-API 's
Hallo Text Analytics-service kunt u toodo gevoel en sleutel-zin extracties in batchmodus. Houd er rekening mee dat elk van de records Hallo aantallen als één transactie verkregen. Een voorbeeld: als u gevoel voor 1000 records in één aanroep vragen 1000 transacties wordt afgetrokken.

Let op: Hallo-id's in Hallo systeem ingevoerd zijn Hallo-id's die zijn geretourneerd door Hallo-systeem. Hallo-webservice wordt niet gecontroleerd of deze id uniek zijn. Het is de verantwoordelijkheid Hallo van Hallo aanroeper tooverify uniekheid. 

### <a name="getsentimentbatch"></a>GetSentimentBatch
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

**Voorbeeld van een aanvraag**

In Hallo POST roept hieronder, wij zijn aangevraagd voor Hallo patronen Hallo woordgroepen "Hello World", "Wereld Hallo Foo" en "Hello mijn World" in de hoofdtekst Hallo van Hallo-aanvraag:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

Hoofdtekst van de aanvraag:

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

Hallo-antwoord hieronder wordt ophalen u Hallo lijst met scores die zijn gekoppeld aan uw tekst-id's:

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
### <a name="getkeyphrasesbatch"></a>GetKeyPhrasesBatch
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

**Voorbeeld van een aanvraag**

In dit voorbeeld aanvraagt we voor Hallo lijst met patronen voor Hallo sleutel zinnen in Hallo teksten te volgen: 

* "Er is een fantastische hotel toostay op, met unieke decor en beschrijvende medewerkers"
* "Er is een fantastische build conferentie, met zeer interessante vertelt"
* "Hallo verkeer is verschrikkelijke, ik drie uur gebeurt toohello luchthaven besteed"

Deze aanvraag wordt gedaan als een POST-aanroep toohello eindpunt:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

Hoofdtekst van de aanvraag:

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

Hallo-antwoord hieronder wordt ophalen u Hallo-lijst met belangrijke termen die zijn gekoppeld aan uw tekst-id's:

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
### <a name="getlanguagebatch"></a>GetLanguageBatch

We aanvraagt taaldetectie voor twee tekst invoeren in Hallo POST-aanroep die hieronder wordt:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

Hoofdtekst van de aanvraag:

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

Hiermee wordt de Hallo na antwoord, waarbij Engels is gedetecteerd in hello eerste invoer- en Frans in Hallo tweede invoer:

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
## <a name="topic-detection-apis"></a>Onderwerp Detection-API 's
Dit is een nieuw uitgebrachte API Hallo bovenste gedetecteerde onderwerpen voor een lijst met verzonden tekstrecords geretourneerd. Een onderwerp wordt geïdentificeerd met een sleutelfrase die uit een of meer verwante woorden kan bestaan. Bij de API wordt er één transactie per ingediende tekstrecord in rekening gebracht.

Deze API vereist een minimum van 100 tekst registreert toobe verzonden, maar is ontworpen toodetect onderwerpen over honderden toothousands met records.

### <a name="topics--submit-job"></a>Onderwerpen – taak verzenden
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

**Voorbeeld van een aanvraag**

Hallo POST-aanroep hieronder vragen we onderwerpen voor een set van 100 artikelen, waarbij Hallo voornaam en achternaam invoer artikelen worden weergegeven en twee StopPhrases zijn opgenomen.

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

Hoofdtekst van de aanvraag:

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

Hallo-antwoord hieronder wordt ophalen u Hallo JobId voor Hallo ingediende taak:

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

Een lijst van één woord of meerdere word zinnen die niet moeten worden geretourneerd als onderwerpen. Kan worden gebruikt toofilter uit zeer algemene onderwerpen. Bijvoorbeeld in een gegevensset over hotel beoordelingen 'hotels' en 'hostel' mogelijk logisch stop zinnen.  

### <a name="topics--poll-for-job-results"></a>Onderwerpen – Poll voor de resultaten van de taak
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

**Voorbeeld van een aanvraag**

Hallo die JobId geretourneerd uit Hallo indienings-taak stap toofetch Hallo resultaten worden doorgegeven. Het is raadzaam dat u dit eindpunt per minuut tot en met Status aanroept = 'Complete' hello reactie. Het duurt ongeveer 10 minuten of langer van taken met duizenden records voor een toocomplete taak.

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


Tijdens het verwerken van, zijn antwoord Hallo als volgt:

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


Hallo API retourneert uitvoer in JSON-indeling in de volgende indeling Hallo:

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


Hallo-eigenschappen voor elk onderdeel van het antwoord Hallo zijn als volgt:

**TopicInfo eigenschappen**

| Sleutel | Beschrijving |
|:--- |:--- |
| Onderwerpklasse |Een unieke id voor elk onderwerp. |
| Score |Het aantal records tootopic toegewezen. |
| KeyPhrase |Een samengevat woord of woordgroep voor Hallo onderwerp. 1 of meer woorden kan zijn. |

**TopicAssignment eigenschappen**

| Sleutel | Beschrijving |
|:--- |:--- |
| Id |ID voor Hallo record. Opgenomen in invoer Hallo toohello-ID is gelijk. |
| Onderwerpklasse |onderwerp-ID Hallo welke Hallo-record is toegewezen aan. |
| afstand |Vertrouwen dat Hallo record toohello onderwerp behoort. Afstand dichter toozero geeft hoger vertrouwen. |

