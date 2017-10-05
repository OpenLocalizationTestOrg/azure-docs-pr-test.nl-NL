---
title: Ondersteuning van Azure Virtual machines toevoegen aan de bestaande beschikbaarheidsset instellen | Microsoft Docs
description: Ondersteuning van Azure Virtual machines toevoegen aan een bestaande beschikbaarheidsset.
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
ms.openlocfilehash: 3ce9b8a79108cb9e57df14bcb3354cc637193233
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="supportability-of-adding-azure-vms-to-an-existing-availability-set"></a><span data-ttu-id="bc13a-103">Ondersteuning van Azure Virtual machines toevoegen aan een bestaande beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="bc13a-103">Supportability of adding Azure VMs to an existing availability set</span></span>

<span data-ttu-id="bc13a-104">Van tijd tot tijd kan verschijnen beperkingen wanneer u nieuwe virtuele machines (VM's) toevoegen aan een bestaande beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="bc13a-104">You may occasionally encounter limitations when you add new virtual machines (VMs) to an existing availability set.</span></span> <span data-ttu-id="bc13a-105">Het volgende diagram details over welke VM-reeks u in dezelfde beschikbaarheidsset mengen kunt.</span><span class="sxs-lookup"><span data-stu-id="bc13a-105">The following chart details which VM series you can mix in the same availability set.</span></span>

<span data-ttu-id="bc13a-106">Dit is de matrix ondersteuningsmogelijkheden mix van verschillende typen van virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="bc13a-106">Here is the supportability matrix to mix different types of VMs:</span></span>

<span data-ttu-id="bc13a-107">Reeks & Beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="bc13a-107">Series & Availability Set</span></span>|<span data-ttu-id="bc13a-108">Tweede VM</span><span class="sxs-lookup"><span data-stu-id="bc13a-108">Second VM</span></span>|<span data-ttu-id="bc13a-109">A</span><span class="sxs-lookup"><span data-stu-id="bc13a-109">A</span></span>|<span data-ttu-id="bc13a-110">Av2</span><span class="sxs-lookup"><span data-stu-id="bc13a-110">Av2</span></span>|<span data-ttu-id="bc13a-111">D</span><span class="sxs-lookup"><span data-stu-id="bc13a-111">D</span></span>|<span data-ttu-id="bc13a-112">Dv2</span><span class="sxs-lookup"><span data-stu-id="bc13a-112">Dv2</span></span>|<span data-ttu-id="bc13a-113">Dv3</span><span class="sxs-lookup"><span data-stu-id="bc13a-113">Dv3</span></span>|
|---|---|---|---|---|---|---|
|<span data-ttu-id="bc13a-114">Eerste VM</span><span class="sxs-lookup"><span data-stu-id="bc13a-114">First VM</span></span>|||||||
|<span data-ttu-id="bc13a-115">A</span><span class="sxs-lookup"><span data-stu-id="bc13a-115">A</span></span>||<span data-ttu-id="bc13a-116">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-116">OK</span></span>|<span data-ttu-id="bc13a-117">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-117">OK</span></span>|<span data-ttu-id="bc13a-118">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-118">OK</span></span>|<span data-ttu-id="bc13a-119">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-119">OK</span></span>|<span data-ttu-id="bc13a-120">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-120">OK</span></span>|
|<span data-ttu-id="bc13a-121">Av2</span><span class="sxs-lookup"><span data-stu-id="bc13a-121">Av2</span></span>||<span data-ttu-id="bc13a-122">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-122">OK</span></span>|<span data-ttu-id="bc13a-123">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-123">OK</span></span>|<span data-ttu-id="bc13a-124">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-124">OK</span></span>|<span data-ttu-id="bc13a-125">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-125">OK</span></span>|<span data-ttu-id="bc13a-126">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-126">OK</span></span>|
|<span data-ttu-id="bc13a-127">D</span><span class="sxs-lookup"><span data-stu-id="bc13a-127">D</span></span>||<span data-ttu-id="bc13a-128">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-128">OK</span></span>|<span data-ttu-id="bc13a-129">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-129">OK</span></span>|<span data-ttu-id="bc13a-130">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-130">OK</span></span>|<span data-ttu-id="bc13a-131">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-131">OK</span></span>|<span data-ttu-id="bc13a-132">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-132">OK</span></span>|
|<span data-ttu-id="bc13a-133">Dv2</span><span class="sxs-lookup"><span data-stu-id="bc13a-133">Dv2</span></span>||<span data-ttu-id="bc13a-134">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-134">OK</span></span>|<span data-ttu-id="bc13a-135">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-135">OK</span></span>|<span data-ttu-id="bc13a-136">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-136">OK</span></span>|<span data-ttu-id="bc13a-137">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-137">OK</span></span>|<span data-ttu-id="bc13a-138">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-138">OK</span></span>|
|<span data-ttu-id="bc13a-139">Dv3</span><span class="sxs-lookup"><span data-stu-id="bc13a-139">Dv3</span></span>||<span data-ttu-id="bc13a-140">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-140">OK</span></span>|<span data-ttu-id="bc13a-141">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-141">OK</span></span>|<span data-ttu-id="bc13a-142">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-142">OK</span></span>|<span data-ttu-id="bc13a-143">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-143">OK</span></span>|<span data-ttu-id="bc13a-144">OK</span><span class="sxs-lookup"><span data-stu-id="bc13a-144">OK</span></span>|

<span data-ttu-id="bc13a-145">Alle andere reeks kan niet worden in dezelfde beschikbaarheidsset omdat ze een specifieke hardware vereist.</span><span class="sxs-lookup"><span data-stu-id="bc13a-145">All other series could not be in the same availability set because they require a specific hardware.</span></span>