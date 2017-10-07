---
title: aaaHow tooscale uw omgeving Azure Time Series Insights | Microsoft Docs
description: Deze zelfstudie bevat informatie over hoe tooscale uw Azure Time Series Insights-omgeving
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: 55eda388997589185bd34228762b95e182b228ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-your-time-series-insights-environment"></a><span data-ttu-id="03e91-103">Hoe tooscale uw omgeving Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="03e91-103">How tooscale your Time Series Insights environment</span></span>

<span data-ttu-id="03e91-104">Deze zelfstudie bevat informatie over hoe tooscale uw Time Series Insights-omgeving.</span><span class="sxs-lookup"><span data-stu-id="03e91-104">This tutorial covers how tooscale your Time Series Insights environment.</span></span>

> [!NOTE]
> <span data-ttu-id="03e91-105">Opschaling van de verschillende typen sku is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="03e91-105">Scale up across sku types is not allowed.</span></span> <span data-ttu-id="03e91-106">Een omgeving met een Sku S1 kan niet worden geconverteerd naar een S2-omgeving.</span><span class="sxs-lookup"><span data-stu-id="03e91-106">An environment with a S1 Sku cannot be converted into an S2 environment.</span></span>

## <a name="s1-sku-ingress-rates-and-capacities"></a><span data-ttu-id="03e91-107">S1 SKU inkomend tarieven en capaciteit</span><span class="sxs-lookup"><span data-stu-id="03e91-107">S1 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="03e91-108">S1 SKU-capaciteit</span><span class="sxs-lookup"><span data-stu-id="03e91-108">S1 SKU Capacity</span></span> | <span data-ttu-id="03e91-109">Snelheid van inkomende gegevens</span><span class="sxs-lookup"><span data-stu-id="03e91-109">Ingress Rate</span></span> | <span data-ttu-id="03e91-110">Maximale opslagcapaciteit</span><span class="sxs-lookup"><span data-stu-id="03e91-110">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="03e91-111">1</span><span class="sxs-lookup"><span data-stu-id="03e91-111">1</span></span> | <span data-ttu-id="03e91-112">1 GB (1 miljoen gebeurtenissen)</span><span class="sxs-lookup"><span data-stu-id="03e91-112">1 GB (1 million events)</span></span> | <span data-ttu-id="03e91-113">30 GB (30 miljoen gebeurtenissen) per maand</span><span class="sxs-lookup"><span data-stu-id="03e91-113">30 GB (30 million events) per month</span></span> |
| <span data-ttu-id="03e91-114">10</span><span class="sxs-lookup"><span data-stu-id="03e91-114">10</span></span> | <span data-ttu-id="03e91-115">10 GB (10 miljoen gebeurtenissen)</span><span class="sxs-lookup"><span data-stu-id="03e91-115">10 GB (10 million events)</span></span> | <span data-ttu-id="03e91-116">300 GB (300 miljoen gebeurtenissen) per maand</span><span class="sxs-lookup"><span data-stu-id="03e91-116">300 GB (300 million events) per month</span></span> |

## <a name="s2-sku-ingress-rates-and-capacities"></a><span data-ttu-id="03e91-117">S2 SKU inkomend tarieven en capaciteit</span><span class="sxs-lookup"><span data-stu-id="03e91-117">S2 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="03e91-118">S2 SKU-capaciteit</span><span class="sxs-lookup"><span data-stu-id="03e91-118">S2 SKU Capacity</span></span> | <span data-ttu-id="03e91-119">Snelheid van inkomende gegevens</span><span class="sxs-lookup"><span data-stu-id="03e91-119">Ingress Rate</span></span> | <span data-ttu-id="03e91-120">Maximale opslagcapaciteit</span><span class="sxs-lookup"><span data-stu-id="03e91-120">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="03e91-121">1</span><span class="sxs-lookup"><span data-stu-id="03e91-121">1</span></span> | <span data-ttu-id="03e91-122">10 GB (10 miljoen gebeurtenissen)</span><span class="sxs-lookup"><span data-stu-id="03e91-122">10 GB (10 million events)</span></span> | <span data-ttu-id="03e91-123">300 GB (300 miljoen gebeurtenissen) per maand</span><span class="sxs-lookup"><span data-stu-id="03e91-123">300 GB (300 million events) per month</span></span> |
| <span data-ttu-id="03e91-124">10</span><span class="sxs-lookup"><span data-stu-id="03e91-124">10</span></span> | <span data-ttu-id="03e91-125">100 GB (100 miljoen gebeurtenissen)</span><span class="sxs-lookup"><span data-stu-id="03e91-125">100 GB (100 million events)</span></span> | <span data-ttu-id="03e91-126">3 TB (3 miljard gebeurtenissen) per maand</span><span class="sxs-lookup"><span data-stu-id="03e91-126">3 TB (3 billion events) per month</span></span> |

<span data-ttu-id="03e91-127">Capaciteitswaarden evenredig, zodat een sku S1 capaciteit 2 2 GB (2 miljoen) gebeurtenissen per dag inkomend en 60 GB (60 miljoen gebeurtenissen) per maand ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="03e91-127">Capacities scale linearly, so a S1 sku with capacity 2 supports 2 GB (2 million) events per day ingress rate and 60 GB (60 million events) per month.</span></span>

## <a name="changing-hello-capacity-of-your-environment"></a><span data-ttu-id="03e91-128">Hallo-capaciteit van uw omgeving wijzigen</span><span class="sxs-lookup"><span data-stu-id="03e91-128">Changing hello capacity of your environment</span></span>

1. <span data-ttu-id="03e91-129">In hello Azure-portal, selecteer Hallo omgeving waarvan capaciteit gewenste toochange.</span><span class="sxs-lookup"><span data-stu-id="03e91-129">In hello Azure portal, select hello environment whose capacity you want toochange.</span></span>
1. <span data-ttu-id="03e91-130">Klik onder instellingen configureren.</span><span class="sxs-lookup"><span data-stu-id="03e91-130">Under Settings, click Configure.</span></span>
1. <span data-ttu-id="03e91-131">Gebruik Hallo capaciteit schuifregelaar tooselect Hallo capaciteit die voldoet aan vereisten voor de tarieven van de inkomende hello- en opslagcapaciteit.</span><span class="sxs-lookup"><span data-stu-id="03e91-131">Use hello Capacity slider tooselect hello capacity that meets hello requirements for your ingress rates and storage capacity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03e91-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="03e91-132">Next steps</span></span>

* <span data-ttu-id="03e91-133">Controleer of de nieuwe capaciteit Hallo voldoende tooprevent beperking.</span><span class="sxs-lookup"><span data-stu-id="03e91-133">Verify that hello new capacity is sufficient tooprevent throttling.</span></span> <span data-ttu-id="03e91-134">Zie voor meer informatie, Hallo *uw omgeving kan worden opgehaald beperkt* sectie [hier](time-series-insights-diagnose-and-solve-problems.md).</span><span class="sxs-lookup"><span data-stu-id="03e91-134">For more details, see hello *Your environment might be getting throttled* section [here](time-series-insights-diagnose-and-solve-problems.md).</span></span>
