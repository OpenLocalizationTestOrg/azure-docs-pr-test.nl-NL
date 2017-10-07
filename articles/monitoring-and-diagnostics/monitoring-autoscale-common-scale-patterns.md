---
title: aaaOverview van algemene patronen voor automatisch schalen | Microsoft Docs
description: Meer informatie over dat sommige van de algemene patronen tooauto Hallo uw resource schalen in Azure.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: fc5bd97852e0af01aa32940c99721ab8e21033ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-common-autoscale-patterns"></a><span data-ttu-id="e1a76-103">Overzicht van algemene patronen voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="e1a76-103">Overview of common autoscale patterns</span></span>
<span data-ttu-id="e1a76-104">Dit artikel worden enkele van de algemene patronen tooscale Hallo uw Azure-resource.</span><span class="sxs-lookup"><span data-stu-id="e1a76-104">This article describes some of hello common patterns tooscale your resource in Azure.</span></span>

<span data-ttu-id="e1a76-105">Azure Monitor automatisch schalen geldt alleen tooVirtual Machine Scale Sets (VMSS), cloudservices, app-serviceabonnementen en app service-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="e1a76-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="e1a76-106">Hiermee kunnen aan de slag</span><span class="sxs-lookup"><span data-stu-id="e1a76-106">Lets get started</span></span>

<span data-ttu-id="e1a76-107">In dit artikel wordt ervan uitgegaan dat u bekend met automatisch schalen bent.</span><span class="sxs-lookup"><span data-stu-id="e1a76-107">This article assumes that you are familiar with auto scale.</span></span> <span data-ttu-id="e1a76-108">U kunt [ophalen gestart hier tooscale uw resource][1].</span><span class="sxs-lookup"><span data-stu-id="e1a76-108">You can [get started here tooscale your resource][1].</span></span> <span data-ttu-id="e1a76-109">Hallo Hieronder volgen enkele Hallo algemene scale patronen.</span><span class="sxs-lookup"><span data-stu-id="e1a76-109">hello following are some of hello common scale patterns.</span></span>

## <a name="scale-based-on-cpu"></a><span data-ttu-id="e1a76-110">Schalen op basis van CPU</span><span class="sxs-lookup"><span data-stu-id="e1a76-110">Scale based on CPU</span></span>

<span data-ttu-id="e1a76-111">U hebt een web-app (VMSS/cloud service rol) en</span><span class="sxs-lookup"><span data-stu-id="e1a76-111">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="e1a76-112">Gewenste tooscale out/schaal in op basis van de CPU.</span><span class="sxs-lookup"><span data-stu-id="e1a76-112">You want tooscale out/scale in based on CPU.</span></span>
- <span data-ttu-id="e1a76-113">Bovendien wilt u tooensure er is een minimum aantal exemplaren.</span><span class="sxs-lookup"><span data-stu-id="e1a76-113">Additionally, you want tooensure there is a minimum number of instances.</span></span> 
- <span data-ttu-id="e1a76-114">Bovendien wilt u tooensure die u instelt dat een maximumlimiet toohello aantal exemplaren die om te kunnen worden geschaald.</span><span class="sxs-lookup"><span data-stu-id="e1a76-114">Also, you want tooensure that you set a maximum limit toohello number of instances you can scale to.</span></span>

![Schalen op basis van CPU][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a><span data-ttu-id="e1a76-116">Anders weekdagen tegenover tijdens het weekend schalen</span><span class="sxs-lookup"><span data-stu-id="e1a76-116">Scale differently on weekdays vs weekends</span></span>

<span data-ttu-id="e1a76-117">U hebt een web-app (VMSS/cloud service rol) en</span><span class="sxs-lookup"><span data-stu-id="e1a76-117">You have a web app (/VMSS/cloud service role) and</span></span>

- <span data-ttu-id="e1a76-118">Op het gewenste 3 exemplaren standaard (weekdagen)</span><span class="sxs-lookup"><span data-stu-id="e1a76-118">You want 3 instances by default (on weekdays)</span></span>
- <span data-ttu-id="e1a76-119">U geen verkeer verwacht tijdens het weekend en daarom het gewenste tooscale omlaag too1 exemplaar in het weekend.</span><span class="sxs-lookup"><span data-stu-id="e1a76-119">You don't expect traffic on weekends and hence you want tooscale down too1 instance on weekends.</span></span>

![Anders weekdagen tegenover tijdens het weekend schalen][3]

## <a name="scale-differently-during-holidays"></a><span data-ttu-id="e1a76-121">Anders tijdens de feestdagen schalen</span><span class="sxs-lookup"><span data-stu-id="e1a76-121">Scale differently during holidays</span></span>

<span data-ttu-id="e1a76-122">U hebt een web-app (VMSS/cloud service rol) en</span><span class="sxs-lookup"><span data-stu-id="e1a76-122">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="e1a76-123">Gewenste tooscale omhoog/omlaag op basis van CPU-gebruik standaard</span><span class="sxs-lookup"><span data-stu-id="e1a76-123">You want tooscale up/down based on CPU usage by default</span></span>
- <span data-ttu-id="e1a76-124">Echter, tijdens de feestdagen (of specifieke dagen die belangrijk voor uw bedrijf zijn) u wilt toooverride Hallo standaardwaarden en meer capaciteit hebben tot uw beschikking staan.</span><span class="sxs-lookup"><span data-stu-id="e1a76-124">However, during holiday season (or specific days that are important for your business) you want toooverride hello defaults and have more capacity at your disposal.</span></span>

![Anders op feestdagen schaal][4]

## <a name="scale-based-on-custom-metric"></a><span data-ttu-id="e1a76-126">Schalen op basis van aangepaste metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="e1a76-126">Scale based on custom metric</span></span>

<span data-ttu-id="e1a76-127">U hebt een webfront-end en een API-laag die met Hallo back-end communiceert.</span><span class="sxs-lookup"><span data-stu-id="e1a76-127">You have a web front end and a API tier that communicates with hello backend.</span></span> 

- <span data-ttu-id="e1a76-128">Gewenste tooscale Hallo API laag op basis van aangepaste gebeurtenissen in de front-end hello (voorbeeld: U wilt dat uw afrekenen op basis van het aantal items dat in winkelwagen Hallo Hallo tooscale)</span><span class="sxs-lookup"><span data-stu-id="e1a76-128">You want tooscale hello API tier based on custom events in hello front end (example: You want tooscale your checkout process based on hello number of items in hello shopping cart)</span></span>

![Schalen op basis van aangepaste metrische gegevens][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png