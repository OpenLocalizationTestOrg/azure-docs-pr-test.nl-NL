---
title: aaaSupportability van het toevoegen van Azure Virtual machines tooan bestaande beschikbaarheidsset | Microsoft Docs
description: Ondersteuning voor het toevoegen van Azure Virtual machines tooan bestaande beschikbaarheidsset.
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a><span data-ttu-id="9d9c9-103">Ondersteuning voor het toevoegen van Azure Virtual machines tooan bestaande beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="9d9c9-103">Supportability of adding Azure VMs tooan existing availability set</span></span>

<span data-ttu-id="9d9c9-104">Beperkingen kan van tijd tot tijd verschijnen wanneer u nieuwe virtuele machines (VM's) tooan bestaande beschikbaarheidsset toevoegt.</span><span class="sxs-lookup"><span data-stu-id="9d9c9-104">You may occasionally encounter limitations when you add new virtual machines (VMs) tooan existing availability set.</span></span> <span data-ttu-id="9d9c9-105">Hallo volgende grafiekdetails welke VM-reeks kunt u mengen in dezelfde beschikbaarheidsset Hallo.</span><span class="sxs-lookup"><span data-stu-id="9d9c9-105">hello following chart details which VM series you can mix in hello same availability set.</span></span>

<span data-ttu-id="9d9c9-106">Hier volgt Hallo ondersteuningsmogelijkheden matrix toomix verschillende typen virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="9d9c9-106">Here is hello supportability matrix toomix different types of VMs:</span></span>

<span data-ttu-id="9d9c9-107">Reeks & Beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="9d9c9-107">Series & Availability Set</span></span>|<span data-ttu-id="9d9c9-108">Tweede VM</span><span class="sxs-lookup"><span data-stu-id="9d9c9-108">Second VM</span></span>|<span data-ttu-id="9d9c9-109">A</span><span class="sxs-lookup"><span data-stu-id="9d9c9-109">A</span></span>|<span data-ttu-id="9d9c9-110">Av2</span><span class="sxs-lookup"><span data-stu-id="9d9c9-110">Av2</span></span>|<span data-ttu-id="9d9c9-111">D</span><span class="sxs-lookup"><span data-stu-id="9d9c9-111">D</span></span>|<span data-ttu-id="9d9c9-112">Dv2</span><span class="sxs-lookup"><span data-stu-id="9d9c9-112">Dv2</span></span>|<span data-ttu-id="9d9c9-113">Dv3</span><span class="sxs-lookup"><span data-stu-id="9d9c9-113">Dv3</span></span>|
|---|---|---|---|---|---|---|
|<span data-ttu-id="9d9c9-114">Eerste VM</span><span class="sxs-lookup"><span data-stu-id="9d9c9-114">First VM</span></span>|||||||
|<span data-ttu-id="9d9c9-115">A</span><span class="sxs-lookup"><span data-stu-id="9d9c9-115">A</span></span>||<span data-ttu-id="9d9c9-116">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-116">OK</span></span>|<span data-ttu-id="9d9c9-117">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-117">OK</span></span>|<span data-ttu-id="9d9c9-118">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-118">OK</span></span>|<span data-ttu-id="9d9c9-119">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-119">OK</span></span>|<span data-ttu-id="9d9c9-120">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-120">OK</span></span>|
|<span data-ttu-id="9d9c9-121">Av2</span><span class="sxs-lookup"><span data-stu-id="9d9c9-121">Av2</span></span>||<span data-ttu-id="9d9c9-122">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-122">OK</span></span>|<span data-ttu-id="9d9c9-123">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-123">OK</span></span>|<span data-ttu-id="9d9c9-124">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-124">OK</span></span>|<span data-ttu-id="9d9c9-125">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-125">OK</span></span>|<span data-ttu-id="9d9c9-126">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-126">OK</span></span>|
|<span data-ttu-id="9d9c9-127">D</span><span class="sxs-lookup"><span data-stu-id="9d9c9-127">D</span></span>||<span data-ttu-id="9d9c9-128">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-128">OK</span></span>|<span data-ttu-id="9d9c9-129">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-129">OK</span></span>|<span data-ttu-id="9d9c9-130">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-130">OK</span></span>|<span data-ttu-id="9d9c9-131">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-131">OK</span></span>|<span data-ttu-id="9d9c9-132">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-132">OK</span></span>|
|<span data-ttu-id="9d9c9-133">Dv2</span><span class="sxs-lookup"><span data-stu-id="9d9c9-133">Dv2</span></span>||<span data-ttu-id="9d9c9-134">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-134">OK</span></span>|<span data-ttu-id="9d9c9-135">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-135">OK</span></span>|<span data-ttu-id="9d9c9-136">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-136">OK</span></span>|<span data-ttu-id="9d9c9-137">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-137">OK</span></span>|<span data-ttu-id="9d9c9-138">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-138">OK</span></span>|
|<span data-ttu-id="9d9c9-139">Dv3</span><span class="sxs-lookup"><span data-stu-id="9d9c9-139">Dv3</span></span>||<span data-ttu-id="9d9c9-140">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-140">OK</span></span>|<span data-ttu-id="9d9c9-141">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-141">OK</span></span>|<span data-ttu-id="9d9c9-142">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-142">OK</span></span>|<span data-ttu-id="9d9c9-143">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-143">OK</span></span>|<span data-ttu-id="9d9c9-144">OK</span><span class="sxs-lookup"><span data-stu-id="9d9c9-144">OK</span></span>|

<span data-ttu-id="9d9c9-145">Alle andere reeks kan niet worden in dezelfde beschikbaarheidsset omdat ze een specifieke hardware vereist Hallo.</span><span class="sxs-lookup"><span data-stu-id="9d9c9-145">All other series could not be in hello same availability set because they require a specific hardware.</span></span>
