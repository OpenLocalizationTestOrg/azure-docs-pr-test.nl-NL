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
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a>API’s voor Machine Learning: Tekstanalyse voor sentimenten, Sleuteltermextractie, Taaldetectie en Onderwerpdetectie
> [!NOTE]
> Deze handleiding is bedoeld voor versie 1 van de API. Voor versie 2, [ **verwijzen naar dit document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md). Versie 2 is nu de gewenste versie van deze API.
> 
> 

## <a name="overview"></a>Overzicht
De tekst Analytics-API is een suite met tekstanalyse [webservices](https://datamarket.azure.com/dataset/amla/text-analytics) gebouwd met Azure Machine Learning. De API kan worden gebruikt voor het analyseren van niet-gestructureerde tekst voor taken zoals gevoel analyse, uitpakken van sleutel woordgroep, taal wordt gedetecteerd en onderwerp detectie. U hebt geen trainingsgegevens nodig om deze API: NET laat uw tekstgegevens. Deze API maakt gebruik van geavanceerde natuurlijke taal verwerken technieken best in klasse voorspellingen leveren.

U kunt tekstanalyse in actie zien op onze [demo site](https://text-analytics-demo.azurewebsites.net/), waar u ook vinden [voorbeelden](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) over het implementeren van tekstanalyse in C# en Python.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a>Sentimentanalyse
De API retourneert een numerieke score tussen 0 en 1. Scores bijna 1 aangeven positief gevoel terwijl scores dicht bij 0 negatieve gevoel geven. Stemmingscores worden gegenereerd met classificatietechnieken. De functies van de invoer aan de classificatie behoren n-g, functies die worden gegenereerd op basis van het onderdeel van spraak tags en word insluitingen. Engels is momenteel de enige ondersteunde taal.

## <a name="key-phrase-extraction"></a>Sleuteluitdrukkingen extraheren
De API retourneert een lijst met tekenreeksen die de belangrijkste gespreksonderwerpen in de invoertekst aanduiden. Er worden technieken uit de geavanceerde Natural Language Processing-toolkit van Microsoft Office gebruikt. Engels is momenteel de enige ondersteunde taal.

## <a name="language-detection"></a>Taaldetectie
De API retourneert de taal aangetroffen en een numerieke score tussen 0 en 1. Scores dichtbij 1 geven aan dat het 100% zeker is dat de geïdentificeerde taal waar is. Er worden in totaal 120 talen ondersteund.

## <a name="topic-detection"></a>Onderwerpherkenning
Dit is een nieuw uitgebrachte API welke retourneert de bovenste gedetecteerd onderwerpen voor een lijst met tekstrecords verzonden. Een onderwerp wordt geïdentificeerd met een sleutelfrase die uit een of meer verwante woorden kan bestaan. Deze API vereist dat er minimaal 100 tekstrecords worden ingediend, maar de API is ontworpen om onderwerpen in honderdduizenden records te detecteren. Bij de API wordt er één transactie per ingediende tekstrecord in rekening gebracht. De API is ontworpen voor korte, menselijke geschreven tekst zoals beoordelingen en feedback van gebruikers.

- - -
## <a name="api-definition"></a>API-definitie
### <a name="headers"></a>Headers
Zorg ervoor dat u de juiste headers in uw aanvraag opnemen, als volgt moet:

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

U vindt de accountsleutel uit uw account in de [Azure gegevens markt](https://datamarket.azure.com/account/keys). Houd er rekening mee dat momenteel wordt alleen JSON voor invoer en uitvoer indelingen is geaccepteerd. XML wordt niet ondersteund.

- - -
## <a name="single-response-apis"></a>Enkele Antwoordthread API 's
### <a name="getsentiment"></a>GetSentiment
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

**Voorbeeld van een aanvraag**

We aanvraagt gevoel analyse voor de zinsnede 'Hallo wereld' in de aanroep hieronder:

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

In de onderstaande aanroep aanvraagt we dat de sleutel vermeldingen gevonden in de tekst 'Dit is een fantastische hotel om te blijven, met unieke decor en beschrijvende medewerkers':

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

In de onderstaande aanroep GET we aanvraagt voor de gevoel voor de sleutel zinnen in de tekst *Hallo wereld*

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

`NumberOfLanguagesToDetect`is een optionele parameter. De standaardwaarde is 1.

- - -
## <a name="batch-apis"></a>Batch-API 's
De tekst Analytics-service kunt u doen gevoel en sleutel-zin extracties in batchmodus. Houd er rekening mee dat elk van de records met aantallen als één transactie verkregen. Een voorbeeld: als u gevoel voor 1000 records in één aanroep vragen 1000 transacties wordt afgetrokken.

Houd er rekening mee dat de id's opgegeven in het systeem de geretourneerd door het systeem-id's zijn. De webservice controleert niet of deze id uniek zijn. Het is de verantwoordelijkheid van de aanroepfunctie uniekheid controleren. 

### <a name="getsentimentbatch"></a>GetSentimentBatch
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

**Voorbeeld van een aanvraag**

In de POST-aanroep hieronder aanvraagt we voor de patronen van de vermeldingen 'Hallo wereld', 'Hallo Foo wereld' en 'Hallo Mijn wereld' in de hoofdtekst van de aanvraag:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

Hoofdtekst van de aanvraag:

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

In het onderstaande antwoord, moet u de lijst met scores die zijn gekoppeld aan uw tekst-id's ophalen:

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

In dit voorbeeld aanvraagt we voor de lijst met patronen voor de sleutel zinnen in de volgende tekst: 

* "Er is een fantastische hotel om te blijven, met unieke decor en beschrijvende medewerkers"
* "Er is een fantastische build conferentie, met zeer interessante vertelt"
* "Het verkeer is verschrikkelijke, ik drie uur naar de luchthaven besteed"

Deze aanvraag wordt gedaan als een POST-aanroep naar het eindpunt:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

Hoofdtekst van de aanvraag:

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel to stay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"The traffic was terrible, I spent three hours going to the airport"}
    ]}

In het antwoord hieronder, moet u de lijst met belangrijke termen die zijn gekoppeld aan uw tekst-id's ophalen:

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

We aanvraagt taaldetectie voor twee tekst invoeren in de POST-aanroep hieronder:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

Hoofdtekst van de aanvraag:

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

Hiermee wordt het volgende antwoord waar Engels is gedetecteerd in de eerste invoer- en Frans in de tweede invoer:

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
Dit is een nieuw uitgebrachte API welke retourneert de bovenste gedetecteerd onderwerpen voor een lijst met tekstrecords verzonden. Een onderwerp wordt geïdentificeerd met een sleutelfrase die uit een of meer verwante woorden kan bestaan. Bij de API wordt er één transactie per ingediende tekstrecord in rekening gebracht.

Deze API vereist dat er minimaal 100 tekstrecords worden ingediend, maar de API is ontworpen om onderwerpen in honderdduizenden records te detecteren.

### <a name="topics--submit-job"></a>Onderwerpen – taak verzenden
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

**Voorbeeld van een aanvraag**

In de POST-aanroep hieronder vragen wij onderwerpen voor een set van 100 artikelen, waarbij de eerste en laatste invoer artikelen worden weergegeven en twee StopPhrases zijn opgenomen.

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

Hoofdtekst van de aanvraag:

    {"Inputs":[
        {"Id":"1","Text":"I loved the food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated the decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

In het antwoord hieronder, kunt u de taak-id voor de opgegeven taak opvragen:

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

Een lijst van één woord of meerdere word zinnen die niet moeten worden geretourneerd als onderwerpen. Kan worden gebruikt voor het filteren van zeer algemene onderwerpen. Bijvoorbeeld in een gegevensset over hotel beoordelingen 'hotels' en 'hostel' mogelijk logisch stop zinnen.  

### <a name="topics--poll-for-job-results"></a>Onderwerpen – Poll voor de resultaten van de taak
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

**Voorbeeld van een aanvraag**

De taak-id geretourneerd van de indienings-taakstap voor het ophalen van de resultaten worden doorgegeven. Het is raadzaam dat u dit eindpunt per minuut tot en met Status aanroept = 'Complete' in het antwoord. Het duurt ongeveer 10 minuten voor een taak voltooid of langer van taken met duizenden records.

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


Tijdens het verwerken van, zijn het antwoord als volgt:

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


De API wordt de uitvoer geretourneerd in JSON-indeling in de volgende indeling:

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


De eigenschappen voor elk onderdeel van het antwoord zijn als volgt:

**TopicInfo eigenschappen**

| Sleutel | Beschrijving |
|:--- |:--- |
| Onderwerpklasse |Een unieke id voor elk onderwerp. |
| Score |Het aantal records dat is toegewezen aan het onderwerp. |
| KeyPhrase |Een samengevat woord of woordgroep voor het onderwerp. 1 of meer woorden kan zijn. |

**TopicAssignment eigenschappen**

| Sleutel | Beschrijving |
|:--- |:--- |
| Id |ID voor de record. Is gelijk aan de ID die is opgenomen in de invoer. |
| Onderwerpklasse |De onderwerp-ID die aan de record is toegewezen. |
| afstand |Vertrouwen dat de record deel uitmaakt van het onderwerp. Afstand dichter op nul geeft aan dat hoger vertrouwen. |

