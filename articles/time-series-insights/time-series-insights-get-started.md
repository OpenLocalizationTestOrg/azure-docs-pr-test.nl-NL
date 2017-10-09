---
title: een Azure Time Series Insights omgeving aaaCreate | Microsoft Docs
description: In deze zelfstudie leert u hoe toocreate Time Series-omgeving, verbindt u deze tooan gebeurtenisbron en klaar tooanalyze de gebeurtenisgegevens in minuten.
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
ms.openlocfilehash: 7120fc9a6e4d4a4972f8cb37e4d9945cfb746fd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-time-series-insights-environment-in-hello-azure-portal"></a><span data-ttu-id="8712b-103">Maak een nieuwe Time Series Insights-omgeving in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="8712b-103">Create a new Time Series Insights environment in hello Azure portal</span></span>

<span data-ttu-id="8712b-104">Een Time Series Insights-omgeving is een Azure-resource met inkomend verkeer en opslagcapaciteit.</span><span class="sxs-lookup"><span data-stu-id="8712b-104">Time Series Insights environment is an Azure resource with ingress and storage capacity.</span></span> <span data-ttu-id="8712b-105">Klanten inrichten omgevingen via hello Azure-portal met Hallo vereist capaciteit.</span><span class="sxs-lookup"><span data-stu-id="8712b-105">Customers provision environments via hello Azure portal with hello required capacity.</span></span>

## <a name="steps-toocreate-hello-environment"></a><span data-ttu-id="8712b-106">Stappen toocreate Hallo-omgeving</span><span class="sxs-lookup"><span data-stu-id="8712b-106">Steps toocreate hello environment</span></span>

<span data-ttu-id="8712b-107">Volg deze stappen toocreate uw omgeving:</span><span class="sxs-lookup"><span data-stu-id="8712b-107">Follow these steps toocreate your environment:</span></span>

1.  <span data-ttu-id="8712b-108">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8712b-108">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="8712b-109">Klik op Hallo plus -teken ('+') in de linkerbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="8712b-109">Click hello plus sign (“+”) in hello top left corner.</span></span>
3.  <span data-ttu-id="8712b-110">Zoeken naar 'Time Series Insights' in het zoekvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="8712b-110">Search for “Time Series Insights” in hello search box.</span></span>

  ![Hallo Time Series Insights omgeving maken](media/get-started/getstarted-create-environment1.png)

4.  <span data-ttu-id="8712b-112">Selecteer Time Series Insights en klik op Maken.</span><span class="sxs-lookup"><span data-stu-id="8712b-112">Select “Time Series Insights”, click “Create”.</span></span>

  ![Hallo Time Series Insights resourcegroep maken](media/get-started/getstarted-create-environment2.png)

5.  <span data-ttu-id="8712b-114">Geef de naam van de omgeving op.</span><span class="sxs-lookup"><span data-stu-id="8712b-114">Specify environment name.</span></span> <span data-ttu-id="8712b-115">Deze naam vertegenwoordigt Hallo-omgeving in [time series explorer](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8712b-115">This name will represent hello environment in [time series explorer](https://insights.timeseries.azure.com).</span></span>
6.  <span data-ttu-id="8712b-116">Selecteer een abonnement.</span><span class="sxs-lookup"><span data-stu-id="8712b-116">Select a subscription.</span></span> <span data-ttu-id="8712b-117">Kies een abonnement dat uw gebeurtenisbron bevat.</span><span class="sxs-lookup"><span data-stu-id="8712b-117">Choose one that contains your event source.</span></span> <span data-ttu-id="8712b-118">Time Series inzichten kunt automatische detectie Azure IoT Hub en Event Hub-resources in bestaande Hallo hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="8712b-118">Time Series Insights can auto-detect Azure IoT Hub and Event Hub resources existing in hello same subscription.</span></span>
7.  <span data-ttu-id="8712b-119">Selecteer of maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="8712b-119">Select or create a resource group.</span></span> <span data-ttu-id="8712b-120">Een resourcegroep is een verzameling Azure-resources die samen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8712b-120">A resource group is a collection of Azure resources used together.</span></span>
8.  <span data-ttu-id="8712b-121">Selecteer een hostinglocatie.</span><span class="sxs-lookup"><span data-stu-id="8712b-121">Select a hosting location.</span></span> <span data-ttu-id="8712b-122">tooavoid verplaatsen tussen gegevens datacenters, kies de locatie waarin de gebeurtenisbron.</span><span class="sxs-lookup"><span data-stu-id="8712b-122">tooavoid moving data across data centers, choose location that contains your event source.</span></span>
9.  <span data-ttu-id="8712b-123">Selecteer een prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="8712b-123">Select a pricing tier.</span></span>
10. <span data-ttu-id="8712b-124">Selecteer de capaciteit.</span><span class="sxs-lookup"><span data-stu-id="8712b-124">Select capacity.</span></span> <span data-ttu-id="8712b-125">U kunt de capaciteit van een omgeving wijzigen nadat deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8712b-125">You can change capacity of an environment after creation.</span></span>
11. <span data-ttu-id="8712b-126">Maak uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="8712b-126">Create your environment.</span></span> <span data-ttu-id="8712b-127">Wanneer u zich aanmeldt, kunt u uw dashboard omgeving toohello voor eenvoudige toegang vastmaken.</span><span class="sxs-lookup"><span data-stu-id="8712b-127">You can also pin your environment toohello dashboard for easy access whenever you sign in.</span></span>

  ![Hallo Time Series Insights pincode toodashboard maken](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a><span data-ttu-id="8712b-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8712b-129">Next steps</span></span>

* <span data-ttu-id="8712b-130">[Definieer gegevenstoegangsbeleid](time-series-insights-data-access.md) tooaccess uw omgeving in [Time Series Insights-Portal](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="8712b-130">[Define data access policies](time-series-insights-data-access.md) tooaccess your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
* [<span data-ttu-id="8712b-131">Een gebeurtenisbron maken</span><span class="sxs-lookup"><span data-stu-id="8712b-131">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="8712b-132">[Verzenden van gebeurtenissen](time-series-insights-send-events.md) toohello gebeurtenisbron</span><span class="sxs-lookup"><span data-stu-id="8712b-132">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
