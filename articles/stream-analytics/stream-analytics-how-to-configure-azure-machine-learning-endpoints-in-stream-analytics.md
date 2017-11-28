---
title: Gebruik van Azure Machine Learning-eindpunten in Stream Analytics | Microsoft Docs
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
ms.openlocfilehash: d3a46190dd802bf31ea03ef38304d58e6e63b66d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="machine-learning-integration-in-stream-analytics"></a><span data-ttu-id="37f70-103">Machine Learning-integratie in Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="37f70-103">Machine Learning integration in Stream Analytics</span></span>
<span data-ttu-id="37f70-104">Stream Analytics ondersteunt de gebruiker gedefinieerde functies met Azure Machine Learning-eindpunten roepen.</span><span class="sxs-lookup"><span data-stu-id="37f70-104">Stream Analytics supports user-defined functions that call out to Azure Machine Learning endpoints.</span></span> <span data-ttu-id="37f70-105">REST-API-ondersteuning voor deze functie wordt beschreven in de [REST-API voor Stream Analytics-bibliotheek](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span><span class="sxs-lookup"><span data-stu-id="37f70-105">REST API support for this feature is detailed in the [Stream Analytics REST API library](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span></span> <span data-ttu-id="37f70-106">In dit artikel biedt extra informatie die nodig zijn voor een succesvolle implementatie van deze mogelijkheid in Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="37f70-106">This article provides supplemental information needed for successful implementation of this capability in Stream Analytics.</span></span> <span data-ttu-id="37f70-107">Een zelfstudie is ook geplaatst en is beschikbaar [hier](stream-analytics-machine-learning-integration-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="37f70-107">A tutorial has also been posted and is available [here](stream-analytics-machine-learning-integration-tutorial.md).</span></span>

## <a name="overview-azure-machine-learning-terminology"></a><span data-ttu-id="37f70-108">Overzicht: Azure Machine Learning-terminologie</span><span class="sxs-lookup"><span data-stu-id="37f70-108">Overview: Azure Machine Learning terminology</span></span>
<span data-ttu-id="37f70-109">Microsoft Azure Machine Learning biedt een gezamenlijke slepen en neerzetten hulpprogramma die kunt u om te bouwen, testen en implementeren van predictive analytics-oplossingen voor uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="37f70-109">Microsoft Azure Machine Learning provides a collaborative, drag-and-drop tool you can use to build, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="37f70-110">Dit programma heet de *Azure Machine Learning Studio*.</span><span class="sxs-lookup"><span data-stu-id="37f70-110">This tool is called the *Azure Machine Learning Studio*.</span></span> <span data-ttu-id="37f70-111">De studio wordt gebruikt om te communiceren met de Machine Learning-bronnen en eenvoudig bouwen, testen en te herhalen uw ontwerp.</span><span class="sxs-lookup"><span data-stu-id="37f70-111">The studio is used to interact with the Machine Learning resources and easily build, test, and iterate on your design.</span></span> <span data-ttu-id="37f70-112">Deze resources en de bijbehorende definities zijn hieronder.</span><span class="sxs-lookup"><span data-stu-id="37f70-112">These resources and their definitions are below.</span></span>

* <span data-ttu-id="37f70-113">**Werkruimte**: de *werkruimte* is een container met alle andere bronnen van Machine Learning samen in een container voor beheer en controle.</span><span class="sxs-lookup"><span data-stu-id="37f70-113">**Workspace**: The *workspace* is a container that holds all other Machine Learning resources together in a container for management and control.</span></span>
* <span data-ttu-id="37f70-114">**Experiment**: *experimenten* zijn gemaakt door gegevenswetenschappers tot gegevenssets te gebruiken en een machine learning-model te trainen.</span><span class="sxs-lookup"><span data-stu-id="37f70-114">**Experiment**: *Experiments* are created by data scientists to utilize datasets and train a machine learning model.</span></span>
* <span data-ttu-id="37f70-115">**Eindpunt**: *eindpunten* het Azure Machine Learning-object is gebruikt voor functies als invoer ophaalt, een opgegeven machine learning-model en retourneert scored uitvoer zijn.</span><span class="sxs-lookup"><span data-stu-id="37f70-115">**Endpoint**: *Endpoints* are the Azure Machine Learning object used to take features as input, apply a specified machine learning model and return scored output.</span></span>
* <span data-ttu-id="37f70-116">**Score berekenen voor Webservice**: A *score berekenen voor webservice* is een verzameling van eindpunten zoals hierboven vermeld.</span><span class="sxs-lookup"><span data-stu-id="37f70-116">**Scoring Webservice**: A *scoring webservice* is a collection of endpoints as mentioned above.</span></span>

<span data-ttu-id="37f70-117">Elk eindpunt heeft API's voor Batchuitvoering en synchrone uitvoering.</span><span class="sxs-lookup"><span data-stu-id="37f70-117">Each endpoint has apis for batch execution and synchronous execution.</span></span> <span data-ttu-id="37f70-118">Stream Analytics gebruikt synchrone uitvoering.</span><span class="sxs-lookup"><span data-stu-id="37f70-118">Stream Analytics uses synchronous execution.</span></span> <span data-ttu-id="37f70-119">De specifieke service heet een [aanvraag/antwoord-Service](../machine-learning/machine-learning-consume-web-services.md) in AzureML studio.</span><span class="sxs-lookup"><span data-stu-id="37f70-119">The specific service is named a [Request/Response Service](../machine-learning/machine-learning-consume-web-services.md) in AzureML studio.</span></span>

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a><span data-ttu-id="37f70-120">Machine Learning-bronnen die nodig zijn voor Stream Analytics-taken</span><span class="sxs-lookup"><span data-stu-id="37f70-120">Machine Learning resources needed for Stream Analytics jobs</span></span>
<span data-ttu-id="37f70-121">Taak verwerken is een aanvraag/antwoord-eindpunt voor de toepassing van de Stream Analytics een [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), en een swagger-definitie voor alle nodig zijn voor uitvoering te doen slagen.</span><span class="sxs-lookup"><span data-stu-id="37f70-121">For the purposes of Stream Analytics job processing, a Request/Response endpoint, an [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), and a swagger definition are all necessary for successful execution.</span></span> <span data-ttu-id="37f70-122">Stream Analytics is een extra eindpunt dat Hiermee wordt de url voor het swagger-eindpunt, de interface worden opgezocht en retourneert een default UDF-definitie voor de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="37f70-122">Stream Analytics has an additional endpoint that constructs the url for swagger endpoint, looks up the interface and returns a default UDF definition to the user.</span></span>

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a><span data-ttu-id="37f70-123">Configureren van een Stream Analytics en Machine Learning-UDF via REST-API</span><span class="sxs-lookup"><span data-stu-id="37f70-123">Configure a Stream Analytics and Machine Learning UDF via REST API</span></span>
<span data-ttu-id="37f70-124">U kunt de taak voor het Azure Machine Language-functies aanroepen configureren met behulp van REST-API's.</span><span class="sxs-lookup"><span data-stu-id="37f70-124">By using REST APIs you may configure your job to call Azure Machine Language functions.</span></span> <span data-ttu-id="37f70-125">De stappen zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="37f70-125">The steps are as follows:</span></span>

1. <span data-ttu-id="37f70-126">Een Stream Analytics-taak maken</span><span class="sxs-lookup"><span data-stu-id="37f70-126">Create a Stream Analytics job</span></span>
2. <span data-ttu-id="37f70-127">Invoer definiëren</span><span class="sxs-lookup"><span data-stu-id="37f70-127">Define an input</span></span>
3. <span data-ttu-id="37f70-128">Uitvoer definiëren</span><span class="sxs-lookup"><span data-stu-id="37f70-128">Define an output</span></span>
4. <span data-ttu-id="37f70-129">Maken van een door de gebruiker gedefinieerde functie (UDF)</span><span class="sxs-lookup"><span data-stu-id="37f70-129">Create a user-defined function (UDF)</span></span>
5. <span data-ttu-id="37f70-130">Schrijven van een Stream Analytics-transformatie die de UDF-aanroepen</span><span class="sxs-lookup"><span data-stu-id="37f70-130">Write a Stream Analytics transformation that calls the UDF</span></span>
6. <span data-ttu-id="37f70-131">Start de taak</span><span class="sxs-lookup"><span data-stu-id="37f70-131">Start the job</span></span>

## <a name="creating-a-udf-with-basic-properties"></a><span data-ttu-id="37f70-132">Het maken van een UDF met basiseigenschappen</span><span class="sxs-lookup"><span data-stu-id="37f70-132">Creating a UDF with basic properties</span></span>
<span data-ttu-id="37f70-133">Als u bijvoorbeeld de volgende voorbeeldcode maakt een scalaire UDF met de naam *newudf* die wordt gekoppeld aan een Azure Machine Learning-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="37f70-133">As an example, the following sample code creates a scalar UDF named *newudf* that binds to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="37f70-134">Houd er rekening mee dat de *eindpunt* (service-URI) kunt u vinden op de help-pagina van de API voor de gekozen service en de *apiKey* vindt u op de hoofdpagina van Services.</span><span class="sxs-lookup"><span data-stu-id="37f70-134">Note that the *endpoint* (service URI) can be found on the API help page for the chosen service and the *apiKey* can be found on the Services main page.</span></span>

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

<span data-ttu-id="37f70-135">Voorbeeld van de aanvraag hoofdtekst:</span><span class="sxs-lookup"><span data-stu-id="37f70-135">Example request body:</span></span>  

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

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a><span data-ttu-id="37f70-136">Eindpunt van de RetrieveDefaultDefinition-aanroep voor standaard UDF</span><span class="sxs-lookup"><span data-stu-id="37f70-136">Call RetrieveDefaultDefinition endpoint for default UDF</span></span>
<span data-ttu-id="37f70-137">Zodra het basisproject UDF is gemaakt is de volledige definitie van de UDF nodig.</span><span class="sxs-lookup"><span data-stu-id="37f70-137">Once the skeleton UDF is created the complete definition of the UDF is needed.</span></span> <span data-ttu-id="37f70-138">Het eindpunt RetreiveDefaultDefinition krijgt u de default-definitie voor een scalaire functie die is gebonden aan een Azure Machine Learning-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="37f70-138">The RetreiveDefaultDefinition endpoint helps you get the default definition for a scalar function that is bound to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="37f70-139">De nettolading van de onderstaande moet u de standaard UDF-definitie voor een scalaire functie die is gebonden aan een Azure Machine Learning-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="37f70-139">The payload below requires you to get the default UDF definition for a scalar function that is bound to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="37f70-140">Het werkelijke eindpunt wordt niet gedefinieerd als deze al is opgegeven tijdens de PUT-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="37f70-140">It doesn’t specify the actual endpoint as it has already been provided during PUT request.</span></span> <span data-ttu-id="37f70-141">Stream Analytics roept het eindpunt dat is opgegeven in de aanvraag als expliciet is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="37f70-141">Stream Analytics calls the endpoint provided in the request if it is provided explicitly.</span></span> <span data-ttu-id="37f70-142">Als deze wordt gebruikt met een oorspronkelijk waarnaar wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="37f70-142">Otherwise it uses the one originally referenced.</span></span> <span data-ttu-id="37f70-143">Hier tekenreeks het UDF vindt één parameter (een zin) en retourneert één uitvoer van het type string die aangeeft dat het label 'gevoel' voor de die zin.</span><span class="sxs-lookup"><span data-stu-id="37f70-143">Here the UDF takes a single string parameter (a sentence) and returns a single output of type string which indicates the “sentiment” label for that sentence.</span></span>

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

<span data-ttu-id="37f70-144">Voorbeeld van de aanvraag hoofdtekst:</span><span class="sxs-lookup"><span data-stu-id="37f70-144">Example request body:</span></span>  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

<span data-ttu-id="37f70-145">Een voorbeeld van uitvoer van deze zoekt u naar iets wilt hieronder.</span><span class="sxs-lookup"><span data-stu-id="37f70-145">A sample output of this would look something like below.</span></span>  

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

## <a name="patch-udf-with-the-response"></a><span data-ttu-id="37f70-146">Patch UDF met de reactie</span><span class="sxs-lookup"><span data-stu-id="37f70-146">Patch UDF with the response</span></span>
<span data-ttu-id="37f70-147">De UDF moet nu worden gevuld met het vorige antwoord, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="37f70-147">Now the UDF must be patched with the previous response, as shown below.</span></span>

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

<span data-ttu-id="37f70-148">Aanvraagtekst (uitvoer van de RetrieveDefaultDefinition):</span><span class="sxs-lookup"><span data-stu-id="37f70-148">Request Body (Output from RetrieveDefaultDefinition):</span></span>

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

## <a name="implement-stream-analytics-transformation-to-call-the-udf"></a><span data-ttu-id="37f70-149">Transformatie van de Stream Analytics om aan te roepen de UDF implementeren</span><span class="sxs-lookup"><span data-stu-id="37f70-149">Implement Stream Analytics transformation to call the UDF</span></span>
<span data-ttu-id="37f70-150">Nu de UDF (scoreTweet hier de naam) voor elke gebeurtenis invoer vragen en in een antwoord voor die gebeurtenis geschreven naar uitvoer.</span><span class="sxs-lookup"><span data-stu-id="37f70-150">Now query the UDF (here named scoreTweet) for every input event and write a response for that event to an output.</span></span>  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a><span data-ttu-id="37f70-151">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="37f70-151">Get help</span></span>
<span data-ttu-id="37f70-152">Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="37f70-152">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="37f70-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="37f70-153">Next steps</span></span>
* [<span data-ttu-id="37f70-154">Inleiding tot Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="37f70-154">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="37f70-155">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="37f70-155">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="37f70-156">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="37f70-156">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="37f70-157">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="37f70-157">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="37f70-158">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="37f70-158">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
