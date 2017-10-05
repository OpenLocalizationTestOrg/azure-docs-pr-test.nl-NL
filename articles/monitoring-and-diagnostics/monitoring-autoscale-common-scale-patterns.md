---
title: Overzicht van algemene patronen voor automatisch schalen | Microsoft Docs
description: Informatie over sommige van de algemene patronen automatisch schalen uw Azure-resource.
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
ms.openlocfilehash: fce51546e041c8989d813c3935e058c52b38ba77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-common-autoscale-patterns"></a><span data-ttu-id="3f316-103">Overzicht van algemene patronen voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="3f316-103">Overview of common autoscale patterns</span></span>
<span data-ttu-id="3f316-104">Dit artikel worden enkele van de algemene patronen voor het schalen van uw resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="3f316-104">This article describes some of the common patterns to scale your resource in Azure.</span></span>

<span data-ttu-id="3f316-105">Azure Monitor automatisch schalen geldt alleen voor virtuele Machine Scale Sets (VMSS), cloudservices, app-serviceabonnementen en app service-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="3f316-105">Azure Monitor auto scale applies only to Virtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="3f316-106">Hiermee kunnen aan de slag</span><span class="sxs-lookup"><span data-stu-id="3f316-106">Lets get started</span></span>

<span data-ttu-id="3f316-107">In dit artikel wordt ervan uitgegaan dat u bekend met automatisch schalen bent.</span><span class="sxs-lookup"><span data-stu-id="3f316-107">This article assumes that you are familiar with auto scale.</span></span> <span data-ttu-id="3f316-108">U kunt [hier uw resource schalen aan de slag][1].</span><span class="sxs-lookup"><span data-stu-id="3f316-108">You can [get started here to scale your resource][1].</span></span> <span data-ttu-id="3f316-109">Hier volgen enkele van de algemene patronen van de schaal.</span><span class="sxs-lookup"><span data-stu-id="3f316-109">The following are some of the common scale patterns.</span></span>

## <a name="scale-based-on-cpu"></a><span data-ttu-id="3f316-110">Schalen op basis van CPU</span><span class="sxs-lookup"><span data-stu-id="3f316-110">Scale based on CPU</span></span>

<span data-ttu-id="3f316-111">U hebt een web-app (VMSS/cloud service rol) en</span><span class="sxs-lookup"><span data-stu-id="3f316-111">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="3f316-112">U wilt scale-out/schaal in op basis van de CPU.</span><span class="sxs-lookup"><span data-stu-id="3f316-112">You want to scale out/scale in based on CPU.</span></span>
- <span data-ttu-id="3f316-113">Bovendien wilt u Zorg dat er een minimum aantal exemplaren.</span><span class="sxs-lookup"><span data-stu-id="3f316-113">Additionally, you want to ensure there is a minimum number of instances.</span></span> 
- <span data-ttu-id="3f316-114">Bovendien wilt u ervoor te zorgen dat u een limiet ingesteld op het aantal exemplaren die om te kunnen worden geschaald.</span><span class="sxs-lookup"><span data-stu-id="3f316-114">Also, you want to ensure that you set a maximum limit to the number of instances you can scale to.</span></span>

![Schalen op basis van CPU][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a><span data-ttu-id="3f316-116">Anders weekdagen tegenover tijdens het weekend schalen</span><span class="sxs-lookup"><span data-stu-id="3f316-116">Scale differently on weekdays vs weekends</span></span>

<span data-ttu-id="3f316-117">U hebt een web-app (VMSS/cloud service rol) en</span><span class="sxs-lookup"><span data-stu-id="3f316-117">You have a web app (/VMSS/cloud service role) and</span></span>

- <span data-ttu-id="3f316-118">Op het gewenste 3 exemplaren standaard (weekdagen)</span><span class="sxs-lookup"><span data-stu-id="3f316-118">You want 3 instances by default (on weekdays)</span></span>
- <span data-ttu-id="3f316-119">U geen verkeer verwacht tijdens het weekend en moet daarom worden geschaald naar beneden 1 exemplaar in het weekend.</span><span class="sxs-lookup"><span data-stu-id="3f316-119">You don't expect traffic on weekends and hence you want to scale down to 1 instance on weekends.</span></span>

![Anders weekdagen tegenover tijdens het weekend schalen][3]

## <a name="scale-differently-during-holidays"></a><span data-ttu-id="3f316-121">Anders tijdens de feestdagen schalen</span><span class="sxs-lookup"><span data-stu-id="3f316-121">Scale differently during holidays</span></span>

<span data-ttu-id="3f316-122">U hebt een web-app (VMSS/cloud service rol) en</span><span class="sxs-lookup"><span data-stu-id="3f316-122">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="3f316-123">U wilt omhoog/omlaag schalen op basis van CPU-gebruik standaard</span><span class="sxs-lookup"><span data-stu-id="3f316-123">You want to scale up/down based on CPU usage by default</span></span>
- <span data-ttu-id="3f316-124">Echter tijdens feestdagen (of specifieke dagen die belangrijk voor uw bedrijf zijn) wilt u de standaardinstellingen overschrijven en meer capaciteit hebben tot uw beschikking staan.</span><span class="sxs-lookup"><span data-stu-id="3f316-124">However, during holiday season (or specific days that are important for your business) you want to override the defaults and have more capacity at your disposal.</span></span>

![Anders op feestdagen schaal][4]

## <a name="scale-based-on-custom-metric"></a><span data-ttu-id="3f316-126">Schalen op basis van aangepaste metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="3f316-126">Scale based on custom metric</span></span>

<span data-ttu-id="3f316-127">U hebt een webfront-end en een API-laag die met de back-end communiceert.</span><span class="sxs-lookup"><span data-stu-id="3f316-127">You have a web front end and a API tier that communicates with the backend.</span></span> 

- <span data-ttu-id="3f316-128">U wilt schalen van de API-laag op basis van aangepaste gebeurtenissen in de front-end (voorbeeld: U wilt schalen van uw afrekenen op basis van het aantal items in de winkelwagen)</span><span class="sxs-lookup"><span data-stu-id="3f316-128">You want to scale the API tier based on custom events in the front end (example: You want to scale your checkout process based on the number of items in the shopping cart)</span></span>

![Schalen op basis van aangepaste metrische gegevens][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png