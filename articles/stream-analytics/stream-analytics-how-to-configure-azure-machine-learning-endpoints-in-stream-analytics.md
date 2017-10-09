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
# <a name="machine-learning-integration-in-stream-analytics"></a><span data-ttu-id="60c42-103">Machine Learning-integratie in Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="60c42-103">Machine Learning integration in Stream Analytics</span></span>
<span data-ttu-id="60c42-104">Stream Analytics ondersteunt de gebruiker gedefinieerde functies tooAzure Machine Learning-eindpunten roepen.</span><span class="sxs-lookup"><span data-stu-id="60c42-104">Stream Analytics supports user-defined functions that call out tooAzure Machine Learning endpoints.</span></span> <span data-ttu-id="60c42-105">REST-API-ondersteuning voor deze functie wordt beschreven in Hallo [REST-API voor Stream Analytics-bibliotheek](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span><span class="sxs-lookup"><span data-stu-id="60c42-105">REST API support for this feature is detailed in hello [Stream Analytics REST API library](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span></span> <span data-ttu-id="60c42-106">In dit artikel biedt extra informatie die nodig zijn voor een succesvolle implementatie van deze mogelijkheid in Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="60c42-106">This article provides supplemental information needed for successful implementation of this capability in Stream Analytics.</span></span> <span data-ttu-id="60c42-107">Een zelfstudie is ook geplaatst en is beschikbaar [hier](stream-analytics-machine-learning-integration-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="60c42-107">A tutorial has also been posted and is available [here](stream-analytics-machine-learning-integration-tutorial.md).</span></span>

## <a name="overview-azure-machine-learning-terminology"></a><span data-ttu-id="60c42-108">Overzicht: Azure Machine Learning-terminologie</span><span class="sxs-lookup"><span data-stu-id="60c42-108">Overview: Azure Machine Learning terminology</span></span>
<span data-ttu-id="60c42-109">Microsoft Azure Machine Learning voorziet in een gezamenlijke, slepen en neerzetten-hulpprogramma kunt u toobuild, testen en implementeren van predictive analytics-oplossingen voor uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="60c42-109">Microsoft Azure Machine Learning provides a collaborative, drag-and-drop tool you can use toobuild, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="60c42-110">Dit programma heet Hallo *Azure Machine Learning Studio*.</span><span class="sxs-lookup"><span data-stu-id="60c42-110">This tool is called hello *Azure Machine Learning Studio*.</span></span> <span data-ttu-id="60c42-111">Hallo studio gebruikte toointeract Hello is Machine Learning-bronnen en gemakkelijk maken, testen en uw ontwerp herhalen.</span><span class="sxs-lookup"><span data-stu-id="60c42-111">hello studio is used toointeract with hello Machine Learning resources and easily build, test, and iterate on your design.</span></span> <span data-ttu-id="60c42-112">Deze resources en de bijbehorende definities zijn hieronder.</span><span class="sxs-lookup"><span data-stu-id="60c42-112">These resources and their definitions are below.</span></span>

* <span data-ttu-id="60c42-113">**Werkruimte**: Hallo *werkruimte* is een container met alle andere bronnen van Machine Learning samen in een container voor beheer en controle.</span><span class="sxs-lookup"><span data-stu-id="60c42-113">**Workspace**: hello *workspace* is a container that holds all other Machine Learning resources together in a container for management and control.</span></span>
* <span data-ttu-id="60c42-114">**Experiment**: *experimenten* worden gemaakt door gegevens verzameld tooutilize gegevenssets en een machine learning-model te trainen.</span><span class="sxs-lookup"><span data-stu-id="60c42-114">**Experiment**: *Experiments* are created by data scientists tooutilize datasets and train a machine learning model.</span></span>
* <span data-ttu-id="60c42-115">**Eindpunt**: *eindpunten* zijn functies voor tootake van Azure Machine Learning object dat wordt gebruikt als invoer hello, toepassen van een opgegeven machine learning-model en retourneert scored uitvoer.</span><span class="sxs-lookup"><span data-stu-id="60c42-115">**Endpoint**: *Endpoints* are hello Azure Machine Learning object used tootake features as input, apply a specified machine learning model and return scored output.</span></span>
* <span data-ttu-id="60c42-116">**Score berekenen voor Webservice**: A *score berekenen voor webservice* is een verzameling van eindpunten zoals hierboven vermeld.</span><span class="sxs-lookup"><span data-stu-id="60c42-116">**Scoring Webservice**: A *scoring webservice* is a collection of endpoints as mentioned above.</span></span>

<span data-ttu-id="60c42-117">Elk eindpunt heeft API's voor Batchuitvoering en synchrone uitvoering.</span><span class="sxs-lookup"><span data-stu-id="60c42-117">Each endpoint has apis for batch execution and synchronous execution.</span></span> <span data-ttu-id="60c42-118">Stream Analytics gebruikt synchrone uitvoering.</span><span class="sxs-lookup"><span data-stu-id="60c42-118">Stream Analytics uses synchronous execution.</span></span> <span data-ttu-id="60c42-119">Hallo specifieke service heet een [aanvraag/antwoord-Service](../machine-learning/machine-learning-consume-web-services.md) in AzureML studio.</span><span class="sxs-lookup"><span data-stu-id="60c42-119">hello specific service is named a [Request/Response Service](../machine-learning/machine-learning-consume-web-services.md) in AzureML studio.</span></span>

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a><span data-ttu-id="60c42-120">Machine Learning-bronnen die nodig zijn voor Stream Analytics-taken</span><span class="sxs-lookup"><span data-stu-id="60c42-120">Machine Learning resources needed for Stream Analytics jobs</span></span>
<span data-ttu-id="60c42-121">Taak verwerken is een aanvraag/antwoord-eindpunt voor de toepassing hello van Stream Analytics een [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), en een swagger-definitie voor alle nodig zijn voor uitvoering te doen slagen.</span><span class="sxs-lookup"><span data-stu-id="60c42-121">For hello purposes of Stream Analytics job processing, a Request/Response endpoint, an [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), and a swagger definition are all necessary for successful execution.</span></span> <span data-ttu-id="60c42-122">Stream Analytics is een extra eindpunt dat constructs Hallo-url voor het swagger-eindpunt, Hallo interface worden opgezocht en retourneert een standaardgebruiker UDF definitie toohello.</span><span class="sxs-lookup"><span data-stu-id="60c42-122">Stream Analytics has an additional endpoint that constructs hello url for swagger endpoint, looks up hello interface and returns a default UDF definition toohello user.</span></span>

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a><span data-ttu-id="60c42-123">Configureren van een Stream Analytics en Machine Learning-UDF via REST-API</span><span class="sxs-lookup"><span data-stu-id="60c42-123">Configure a Stream Analytics and Machine Learning UDF via REST API</span></span>
<span data-ttu-id="60c42-124">U kunt uw taak toocall Azure Machine Language functies configureren met behulp van REST-API's.</span><span class="sxs-lookup"><span data-stu-id="60c42-124">By using REST APIs you may configure your job toocall Azure Machine Language functions.</span></span> <span data-ttu-id="60c42-125">Hallo stappen zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="60c42-125">hello steps are as follows:</span></span>

1. <span data-ttu-id="60c42-126">Een Stream Analytics-taak maken</span><span class="sxs-lookup"><span data-stu-id="60c42-126">Create a Stream Analytics job</span></span>
2. <span data-ttu-id="60c42-127">Invoer definiëren</span><span class="sxs-lookup"><span data-stu-id="60c42-127">Define an input</span></span>
3. <span data-ttu-id="60c42-128">Uitvoer definiëren</span><span class="sxs-lookup"><span data-stu-id="60c42-128">Define an output</span></span>
4. <span data-ttu-id="60c42-129">Maken van een door de gebruiker gedefinieerde functie (UDF)</span><span class="sxs-lookup"><span data-stu-id="60c42-129">Create a user-defined function (UDF)</span></span>
5. <span data-ttu-id="60c42-130">Schrijven van een Stream Analytics-transformatie dat aanroepen UDF Hallo</span><span class="sxs-lookup"><span data-stu-id="60c42-130">Write a Stream Analytics transformation that calls hello UDF</span></span>
6. <span data-ttu-id="60c42-131">Hallo taak starten</span><span class="sxs-lookup"><span data-stu-id="60c42-131">Start hello job</span></span>

## <a name="creating-a-udf-with-basic-properties"></a><span data-ttu-id="60c42-132">Het maken van een UDF met basiseigenschappen</span><span class="sxs-lookup"><span data-stu-id="60c42-132">Creating a UDF with basic properties</span></span>
<span data-ttu-id="60c42-133">Als u bijvoorbeeld Hallo volgende voorbeeldcode maakt een scalaire UDF met de naam *newudf* die tooan Azure Machine Learning-eindpunt wordt gebonden.</span><span class="sxs-lookup"><span data-stu-id="60c42-133">As an example, hello following sample code creates a scalar UDF named *newudf* that binds tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="60c42-134">Houd er rekening mee dat Hallo *eindpunt* (service-URI) vindt u op Hallo API help-pagina voor de gekozen service en Hallo Hallo *apiKey* vindt u op de hoofdpagina Hallo-Services.</span><span class="sxs-lookup"><span data-stu-id="60c42-134">Note that hello *endpoint* (service URI) can be found on hello API help page for hello chosen service and hello *apiKey* can be found on hello Services main page.</span></span>

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

<span data-ttu-id="60c42-135">Voorbeeld van de aanvraag hoofdtekst:</span><span class="sxs-lookup"><span data-stu-id="60c42-135">Example request body:</span></span>  

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

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a><span data-ttu-id="60c42-136">Eindpunt van de RetrieveDefaultDefinition-aanroep voor standaard UDF</span><span class="sxs-lookup"><span data-stu-id="60c42-136">Call RetrieveDefaultDefinition endpoint for default UDF</span></span>
<span data-ttu-id="60c42-137">Eenmaal Hallo basisproject die UDF Hallo volledige definitie van Hallo die UDF nodig is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="60c42-137">Once hello skeleton UDF is created hello complete definition of hello UDF is needed.</span></span> <span data-ttu-id="60c42-138">Hallo RetreiveDefaultDefinition eindpunt kun je optimaal Hallo default-definitie voor een scalaire functie die is gebonden tooan Azure Machine Learning-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="60c42-138">hello RetreiveDefaultDefinition endpoint helps you get hello default definition for a scalar function that is bound tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="60c42-139">Hallo nettolading onderstaande vereist tooget Hallo standaarddefinitie UDF voor een scalaire functie die is gebonden tooan Azure Machine Learning-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="60c42-139">hello payload below requires you tooget hello default UDF definition for a scalar function that is bound tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="60c42-140">Hallo echt eindpunt wordt niet gedefinieerd als deze al is opgegeven tijdens de PUT-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="60c42-140">It doesn’t specify hello actual endpoint as it has already been provided during PUT request.</span></span> <span data-ttu-id="60c42-141">Stream Analytics roept Hallo-eindpunt is opgegeven in de aanvraag Hallo als expliciet is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="60c42-141">Stream Analytics calls hello endpoint provided in hello request if it is provided explicitly.</span></span> <span data-ttu-id="60c42-142">Als deze wordt gebruikt met Hallo een oorspronkelijk waarnaar wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="60c42-142">Otherwise it uses hello one originally referenced.</span></span> <span data-ttu-id="60c42-143">Hier Hallo UDF vergt één parameter (een zin) en retourneert één uitvoer van het type tekenreeks waarmee wordt aangegeven Hallo 'gevoel' label voor de zin dat de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="60c42-143">Here hello UDF takes a single string parameter (a sentence) and returns a single output of type string which indicates hello “sentiment” label for that sentence.</span></span>

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

<span data-ttu-id="60c42-144">Voorbeeld van de aanvraag hoofdtekst:</span><span class="sxs-lookup"><span data-stu-id="60c42-144">Example request body:</span></span>  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

<span data-ttu-id="60c42-145">Een voorbeeld van uitvoer van deze zoekt u naar iets wilt hieronder.</span><span class="sxs-lookup"><span data-stu-id="60c42-145">A sample output of this would look something like below.</span></span>  

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

## <a name="patch-udf-with-hello-response"></a><span data-ttu-id="60c42-146">Patch UDF met antwoord Hallo</span><span class="sxs-lookup"><span data-stu-id="60c42-146">Patch UDF with hello response</span></span>
<span data-ttu-id="60c42-147">Nu moet hello UDF worden gevuld met het vorige antwoord hello, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="60c42-147">Now hello UDF must be patched with hello previous response, as shown below.</span></span>

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

<span data-ttu-id="60c42-148">Aanvraagtekst (uitvoer van de RetrieveDefaultDefinition):</span><span class="sxs-lookup"><span data-stu-id="60c42-148">Request Body (Output from RetrieveDefaultDefinition):</span></span>

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

## <a name="implement-stream-analytics-transformation-toocall-hello-udf"></a><span data-ttu-id="60c42-149">Stream Analytics transformatie toocall Hallo UDF implementeren</span><span class="sxs-lookup"><span data-stu-id="60c42-149">Implement Stream Analytics transformation toocall hello UDF</span></span>
<span data-ttu-id="60c42-150">Nu query Hallo UDF (scoreTweet hier de naam) voor elke gebeurtenis invoer en een antwoord voor die gebeurtenis tooan uitvoer schrijven.</span><span class="sxs-lookup"><span data-stu-id="60c42-150">Now query hello UDF (here named scoreTweet) for every input event and write a response for that event tooan output.</span></span>  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a><span data-ttu-id="60c42-151">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="60c42-151">Get help</span></span>
<span data-ttu-id="60c42-152">Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="60c42-152">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="60c42-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="60c42-153">Next steps</span></span>
* [<span data-ttu-id="60c42-154">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="60c42-154">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="60c42-155">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="60c42-155">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="60c42-156">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="60c42-156">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="60c42-157">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="60c42-157">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="60c42-158">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="60c42-158">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
