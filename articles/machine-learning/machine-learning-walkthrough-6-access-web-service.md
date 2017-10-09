---
title: 'Stap 6: Toegang tot Hallo Machine Learning-webservice | Microsoft Docs'
description: 'Stap 6 van Hallo een overzicht van de voorspellende oplossing ontwikkelen: toegang tot een actieve Azure Machine Learning-webservice.'
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a65c89a-40ab-4673-8dd8-8eee0a150e3b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 211de0294092c6a6b5e6eb608d5d3b88107674c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-6-access-hello-azure-machine-learning-web-service"></a><span data-ttu-id="9617d-103">Overzicht stap 6: Toegang tot hello Azure Machine Learning-webservice</span><span class="sxs-lookup"><span data-stu-id="9617d-103">Walkthrough Step 6: Access hello Azure Machine Learning web service</span></span>

<span data-ttu-id="9617d-104">Dit is de laatste stap Hallo van Hallo-rondleiding [predictive analytics-oplossing in Azure Machine Learning ontwikkelen](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="9617d-104">This is hello last step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="9617d-105">Een Machine Learning-werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="9617d-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="9617d-106">Bestaande gegevens uploaden</span><span class="sxs-lookup"><span data-stu-id="9617d-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="9617d-107">Een nieuw experiment maken</span><span class="sxs-lookup"><span data-stu-id="9617d-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="9617d-108">Trainen en evalueren Hallo modellen</span><span class="sxs-lookup"><span data-stu-id="9617d-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="9617d-109">Hallo-webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="9617d-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. <span data-ttu-id="9617d-110">**Toegang tot Hallo-webservice**</span><span class="sxs-lookup"><span data-stu-id="9617d-110">**Access hello Web service**</span></span>

- - -
<span data-ttu-id="9617d-111">In de vorige stap Hallo in dit scenario wordt een webservice die gebruikmaakt van onze voorspelling van tegoed risicomodel geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="9617d-111">In hello previous step in this walkthrough we deployed a web service that uses our credit risk prediction model.</span></span> <span data-ttu-id="9617d-112">Nu dat gebruikers kunnen toosend gegevens tooit zijn en resultaten krijgen.</span><span class="sxs-lookup"><span data-stu-id="9617d-112">Now users are able toosend data tooit and receive results.</span></span> 

<span data-ttu-id="9617d-113">Hallo-webservice is een Azure-web-service die u kunt ontvangen en retourneren van gegevens met behulp van REST-API's op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="9617d-113">hello Web service is an Azure web service that can receive and return data using REST APIs in one of two ways:</span></span>  

* <span data-ttu-id="9617d-114">**Aanvragen/reacties** - Hallo gebruiker verzendt een of meer rijen met tegoed gegevens toohello service via een HTTP-protocol en Hallo service reageert met een of meer sets van resultaten.</span><span class="sxs-lookup"><span data-stu-id="9617d-114">**Request/Response** - hello user sends one or more rows of credit data toohello service by using an HTTP protocol, and hello service responds with one or more sets of results.</span></span>
* <span data-ttu-id="9617d-115">**Batchuitvoering** - Hallo gebruiker opslaat een of meer rijen tegoed gegevens in een Azure blob- en stuurt vervolgens Hallo blob locatie toohello-service.</span><span class="sxs-lookup"><span data-stu-id="9617d-115">**Batch Execution** - hello user stores one or more rows of credit data in an Azure blob and then sends hello blob location toohello service.</span></span> <span data-ttu-id="9617d-116">Hallo service scores die alle rijen van de gegevens in Hallo Hallo blob-invoerbron, winkels hello resulteert in een andere blob- en retourneert de URL van de container waarin Hallo.</span><span class="sxs-lookup"><span data-stu-id="9617d-116">hello service scores all hello rows of data in hello input blob, stores hello results in another blob, and returns hello URL of that container.</span></span>  

<span data-ttu-id="9617d-117">snelste en gemakkelijkste manier tooaccess een klassiek webservice via Hallo is Hallo [Web-App voor Azure ML aanvragen en antwoorden Service](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) of [Azure ML Batch uitvoering Web App servicesjabloon](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span><span class="sxs-lookup"><span data-stu-id="9617d-117">hello quickest and easiest way tooaccess a Classic web service is through hello [Azure ML Request-Response Service Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) or [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span></span>

<span data-ttu-id="9617d-118">Deze web-app-sjablonen kunnen maken van een aangepaste web-app die u kent uw webservice invoergegevens en wat wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9617d-118">These web app templates can build a custom web app that knows your web service's input data and what it will return.</span></span> <span data-ttu-id="9617d-119">Toodo hoeft u access tooyour-webservice en gegevens bieden en Hallo sjabloon Hallo rest.</span><span class="sxs-lookup"><span data-stu-id="9617d-119">All you need toodo is provide access tooyour web service and data, and hello template does hello rest.</span></span>

<span data-ttu-id="9617d-120">Zie voor meer informatie over het gebruik van de app websjablonen Hallo [een webservice Azure Machine Learning met een web-app-sjabloon gebruiken](machine-learning-consume-web-service-with-web-app-template.md).</span><span class="sxs-lookup"><span data-stu-id="9617d-120">For more information on using hello web app templates, see [Consume an Azure Machine Learning Web service with a web app template](machine-learning-consume-web-service-with-web-app-template.md).</span></span>

<span data-ttu-id="9617d-121">U kunt ook een aangepaste toepassing tooaccess Hallo webservice met starter code voorzien in R, C# en Python programmeertalen ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="9617d-121">You can also develop a custom application tooaccess hello web service using starter code provided for you in R, C#, and Python programming languages.</span></span>

<span data-ttu-id="9617d-122">U vindt meer informatie in [hoe een Azure Machine Learning-webservice tooconsume](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="9617d-122">You can find complete details in [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

