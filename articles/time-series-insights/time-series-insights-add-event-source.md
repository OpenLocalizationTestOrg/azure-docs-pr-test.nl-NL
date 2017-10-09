---
title: een gebeurtenis tooyour Azure Time Series Insights bronomgeving aaaAdd | Microsoft Docs
description: In deze zelfstudie maakt u verbinding maakt een gebeurtenis tooyour Time Series Insights bronomgeving
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 817df5e81cb4dc3d7376914a4651aabebadbcc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a><span data-ttu-id="cc7d3-103">Maken van een gebeurtenisbron voor uw Time Series Insights-omgeving met behulp van de portal Ibiza Hallo</span><span class="sxs-lookup"><span data-stu-id="cc7d3-103">Create an event source for your Time Series Insights environment using hello Ibiza portal</span></span>

<span data-ttu-id="cc7d3-104">Een Time Series Insights-gebeurtenisbron is afgeleid van een gebeurtenis-broker, zoals Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="cc7d3-104">Time Series Insights Event Source is derived from an event broker, like Azure Event Hubs.</span></span> <span data-ttu-id="cc7d3-105">Time Series Insights maakt rechtstreeks verbinding tooEvent bronnen, Hallo gegevensstroom zonder gebruikers toowrite één regel code opnemen.</span><span class="sxs-lookup"><span data-stu-id="cc7d3-105">Time Series Insights connects directly tooEvent Sources, ingesting hello data stream without requiring users toowrite a single line of code.</span></span> <span data-ttu-id="cc7d3-106">Op dit moment biedt Time Series Insights ondersteuning voor Azure Event Hubs en Azure IoT Hubs.</span><span class="sxs-lookup"><span data-stu-id="cc7d3-106">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs.</span></span> <span data-ttu-id="cc7d3-107">In toekomstige hello, worden meer bronnen van gebeurtenissen toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="cc7d3-107">In hello future, more Event Sources will be added.</span></span>

## <a name="steps-tooadd-an-event-source-tooyour-environment"></a><span data-ttu-id="cc7d3-108">Stappen tooadd tooyour bronomgeving van een gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="cc7d3-108">Steps tooadd an event source tooyour environment</span></span>

1.  <span data-ttu-id="cc7d3-109">Meld u aan toohello [portal Ibiza](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cc7d3-109">Sign in toohello [Ibiza portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="cc7d3-110">Klik op 'Alle resources' in hello menu aan de linkerkant van de portal Ibiza Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="cc7d3-110">Click “All resources” in hello menu on hello left side of hello Ibiza portal.</span></span>
3.  <span data-ttu-id="cc7d3-111">Selecteer uw Time Series Insights-omgeving.</span><span class="sxs-lookup"><span data-stu-id="cc7d3-111">Select your Time Series Insights environment.</span></span>

  ![Hallo Time Series Insights gebeurtenisbron maken](media/add-event-source/getstarted-create-event-source-1.png)

4.  <span data-ttu-id="cc7d3-113">Selecteer Gebeurtenisbronnen en klik op + Toevoegen.</span><span class="sxs-lookup"><span data-stu-id="cc7d3-113">Select “Event Sources”, click “+ Add.”</span></span>

  ![Hallo Time Series Insights gebeurtenisbron - details maken](media/add-event-source/getstarted-create-event-source-2.png)

5.  <span data-ttu-id="cc7d3-115">Hallo-naam van de gebeurtenisbron Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="cc7d3-115">Specify hello name of hello event source.</span></span> <span data-ttu-id="cc7d3-116">Deze naam is gekoppeld aan alle gebeurtenissen afkomstig uit deze gebeurtenisbron en komt tijdens het uitvoeren van query's beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="cc7d3-116">This name is associated with all events coming from this event source and is available at query time.</span></span>
6.  <span data-ttu-id="cc7d3-117">Selecteer een event hub uit Hallo lijst met resources in het huidige abonnement Hallo Event Hub.</span><span class="sxs-lookup"><span data-stu-id="cc7d3-117">Select an event hub from hello list of Event Hub resources in hello current subscription.</span></span> <span data-ttu-id="cc7d3-118">Kies anders optie importeren ' Geef Event Hub-instellingen handmatig ' toospecify een event hub in een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="cc7d3-118">Otherwise choose import option "Provide Event Hub settings manually” toospecify an event hub in another subscription.</span></span> <span data-ttu-id="cc7d3-119">Gebeurtenissen moeten worden gepubliceerd in de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="cc7d3-119">Events must be published in JSON format.</span></span>
7.  <span data-ttu-id="cc7d3-120">Selecteer beleid dat u beschikt over leesmachtiging in Hallo event hub.</span><span class="sxs-lookup"><span data-stu-id="cc7d3-120">Select policy that has read permission in hello event hub.</span></span>
8.  <span data-ttu-id="cc7d3-121">Specificeer de Event Hub-consumergroep.</span><span class="sxs-lookup"><span data-stu-id="cc7d3-121">Specify event hub consumer group.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="cc7d3-122">Deze consumergroep mag niet worden gebruikt door een andere service (zoals een Stream Analytics-taak of een andere Time Series Insights-omgeving).</span><span class="sxs-lookup"><span data-stu-id="cc7d3-122">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="cc7d3-123">Als consumergroep wordt gebruikt door andere services, bewerking nadelig wordt beïnvloed voor deze omgeving lees- en andere services Hallo.</span><span class="sxs-lookup"><span data-stu-id="cc7d3-123">If consumer group is used by other services, read operation is negatively affected for this environment and hello other services.</span></span> <span data-ttu-id="cc7d3-124">Als u '$Default' als consumergroep hello, kan dit ertoe leiden toopotential opnieuw kunnen worden gebruikt door andere lezers.</span><span class="sxs-lookup"><span data-stu-id="cc7d3-124">If you are using “$Default” as hello consumer group, it could lead toopotential reuse by other readers.</span></span>

9.  <span data-ttu-id="cc7d3-125">Klik op Maken.</span><span class="sxs-lookup"><span data-stu-id="cc7d3-125">Click “Create.”</span></span>

<span data-ttu-id="cc7d3-126">Nadat het maken van de gebeurtenisbron hello, wordt Time Series Insights automatisch gestart gegevensstromen in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="cc7d3-126">After creation of hello event source, Time Series Insights will automatically start streaming data into your environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc7d3-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cc7d3-127">Next steps</span></span>

* <span data-ttu-id="cc7d3-128">[Verzenden van gebeurtenissen](time-series-insights-send-events.md) toohello gebeurtenisbron</span><span class="sxs-lookup"><span data-stu-id="cc7d3-128">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="cc7d3-129">Uw omgeving bekijken in de [Time Series Insights-portal](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="cc7d3-129">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
