---
title: aaaUse Azure Machine Learning-eindpunten in Stream Analytics | Microsoft Docs
description: Taal van de machine door de gebruiker gedefinieerde functies in Stream Analytics
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 406b258f-b8c2-4e55-953c-b7f84e8e5354
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 013b841ee85b1e0b6d8139a9ba0dde88fc3f8ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-integration-in-stream-analytics"></a>Machine Learning-integratie in Stream Analytics
Stream Analytics ondersteunt de gebruiker gedefinieerde functies tooAzure Machine Learning-eindpunten roepen. REST-API-ondersteuning voor deze functie wordt beschreven in Hallo [REST-API voor Stream Analytics-bibliotheek](https://msdn.microsoft.com/library/azure/dn835031.aspx). In dit artikel biedt extra informatie die nodig zijn voor een succesvolle implementatie van deze mogelijkheid in Stream Analytics. Een zelfstudie is ook geplaatst en is beschikbaar [hier](stream-analytics-machine-learning-integration-tutorial.md).

## <a name="overview-azure-machine-learning-terminology"></a>Overzicht: Azure Machine Learning-terminologie
Microsoft Azure Machine Learning voorziet in een gezamenlijke, slepen en neerzetten-hulpprogramma kunt u toobuild, testen en implementeren van predictive analytics-oplossingen voor uw gegevens. Dit programma heet Hallo *Azure Machine Learning Studio*. Hallo studio gebruikte toointeract Hello is Machine Learning-bronnen en gemakkelijk maken, testen en uw ontwerp herhalen. Deze resources en de bijbehorende definities zijn hieronder.

* **Werkruimte**: Hallo *werkruimte* is een container met alle andere bronnen van Machine Learning samen in een container voor beheer en controle.
* **Experiment**: *experimenten* worden gemaakt door gegevens verzameld tooutilize gegevenssets en een machine learning-model te trainen.
* **Eindpunt**: *eindpunten* zijn functies voor tootake van Azure Machine Learning object dat wordt gebruikt als invoer hello, toepassen van een opgegeven machine learning-model en retourneert scored uitvoer.
* **Score berekenen voor Webservice**: A *score berekenen voor webservice* is een verzameling van eindpunten zoals hierboven vermeld.

Elk eindpunt heeft API's voor Batchuitvoering en synchrone uitvoering. Stream Analytics gebruikt synchrone uitvoering. Hallo specifieke service heet een [aanvraag/antwoord-Service](../machine-learning/machine-learning-consume-web-services.md) in AzureML studio.

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a>Machine Learning-bronnen die nodig zijn voor Stream Analytics-taken
Taak verwerken is een aanvraag/antwoord-eindpunt voor de toepassing hello van Stream Analytics een [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), en een swagger-definitie voor alle nodig zijn voor uitvoering te doen slagen. Stream Analytics is een extra eindpunt dat constructs Hallo-url voor het swagger-eindpunt, Hallo interface worden opgezocht en retourneert een standaardgebruiker UDF definitie toohello.

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a>Configureren van een Stream Analytics en Machine Learning-UDF via REST-API
U kunt uw taak toocall Azure Machine Language functies configureren met behulp van REST-API's. Hallo stappen zijn als volgt:

1. Een Stream Analytics-taak maken
2. Invoer definiëren
3. Uitvoer definiëren
4. Maken van een door de gebruiker gedefinieerde functie (UDF)
5. Schrijven van een Stream Analytics-transformatie dat aanroepen UDF Hallo
6. Hallo taak starten

## <a name="creating-a-udf-with-basic-properties"></a>Het maken van een UDF met basiseigenschappen
Als u bijvoorbeeld Hallo volgende voorbeeldcode maakt een scalaire UDF met de naam *newudf* die tooan Azure Machine Learning-eindpunt wordt gebonden. Houd er rekening mee dat Hallo *eindpunt* (service-URI) vindt u op Hallo API help-pagina voor de gekozen service en Hallo Hallo *apiKey* vindt u op de hoofdpagina Hallo-Services.

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

Voorbeeld van de aanvraag hoofdtekst:  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77fb4b46bf2a30c63c078dca/services/b7be5e40fd194258796fb402c1958eaf/execute ",
                        "apiKey": "replacekeyhere"
                    }
                }
            }
        }
    }
````

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a>Eindpunt van de RetrieveDefaultDefinition-aanroep voor standaard UDF
Eenmaal Hallo basisproject die UDF Hallo volledige definitie van Hallo die UDF nodig is gemaakt. Hallo RetreiveDefaultDefinition eindpunt kun je optimaal Hallo default-definitie voor een scalaire functie die is gebonden tooan Azure Machine Learning-eindpunt. Hallo nettolading onderstaande vereist tooget Hallo standaarddefinitie UDF voor een scalaire functie die is gebonden tooan Azure Machine Learning-eindpunt. Hallo echt eindpunt wordt niet gedefinieerd als deze al is opgegeven tijdens de PUT-aanvraag. Stream Analytics roept Hallo-eindpunt is opgegeven in de aanvraag Hallo als expliciet is opgegeven. Als deze wordt gebruikt met Hallo een oorspronkelijk waarnaar wordt verwezen. Hier Hallo UDF vergt één parameter (een zin) en retourneert één uitvoer van het type tekenreeks waarmee wordt aangegeven Hallo 'gevoel' label voor de zin dat de tekenreeks.

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

Voorbeeld van de aanvraag hoofdtekst:  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

Een voorbeeld van uitvoer van deze zoekt u naar iets wilt hieronder.  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="patch-udf-with-hello-response"></a>Patch UDF met antwoord Hallo
Nu moet hello UDF worden gevuld met het vorige antwoord hello, zoals hieronder wordt weergegeven.

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

Aanvraagtekst (uitvoer van de RetrieveDefaultDefinition):

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="implement-stream-analytics-transformation-toocall-hello-udf"></a>Stream Analytics transformatie toocall Hallo UDF implementeren
Nu query Hallo UDF (scoreTweet hier de naam) voor elke gebeurtenis invoer en een antwoord voor die gebeurtenis tooan uitvoer schrijven.  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a>Help opvragen
Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)
