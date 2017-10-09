---
title: aaaVM behouden onderhoud voor Windows-machines in Azure | Microsoft Docs
description: In-place migratie VM voor het geheugen voor het behouden van updates.
services: virtual-machines-windows
documentationcenter: 
author: 
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: 
ms.openlocfilehash: 544a2dcca52bb3ac51d341bceaf4ba3e7c71fd82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="vm-preserving-maintenance-in-place-vm-migration"></a><span data-ttu-id="1e6d7-103">Virtuele machine (VM In-place migratie) onderhoud behouden</span><span class="sxs-lookup"><span data-stu-id="1e6d7-103">VM preserving maintenance (In-place VM migration)</span></span>

<span data-ttu-id="1e6d7-104">Hallo merendeel van de updates hebben geen invloed toohosted virtuele machines, zijn er ook gevallen waarbij updates toocomponents of services ertoe leiden dat minimale storing toorunning virtuele machines (zonder een volledige opnieuw opstarten van Hallo virtuele machine).</span><span class="sxs-lookup"><span data-stu-id="1e6d7-104">While hello majority of updates have no impact toohosted VMs, there are cases where updates toocomponents or services result in minimal interference toorunning VMs (without a full reboot of hello virtual machine).</span></span>

<span data-ttu-id="1e6d7-105">Deze updates worden bewerkstelligd met-technologie waarmee in-place live migratie, ook wel 'update geheugen behouden'.</span><span class="sxs-lookup"><span data-stu-id="1e6d7-105">These updates are accomplished with technology that enables in-place live migration, also called "memory-preserving update".</span></span> <span data-ttu-id="1e6d7-106">Bij het bijwerken van de host Hallo Hallo virtuele machine wordt geplaatst in de modus 'onderbroken' hello geheugen in RAM, behouden terwijl Hallo hostomgeving (bv. het onderliggende besturingssysteem) van toepassing hello vereiste updates en -patches.</span><span class="sxs-lookup"><span data-stu-id="1e6d7-106">When updating hello host, hello virtual machine is placed into a “paused” state, preserving hello memory in RAM, while hello hosting environment (e.g. the underlying operating system) applies hello necessary updates and patches.</span></span>
<span data-ttu-id="1e6d7-107">Hallo virtuele machine wordt vervolgens hervat binnen 30 seconden wordt onderbroken.</span><span class="sxs-lookup"><span data-stu-id="1e6d7-107">hello virtual machine is then resumed within 30 seconds of being paused.</span></span>
<span data-ttu-id="1e6d7-108">Hallo klok van Hallo virtuele machine is na hervatten, automatisch gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="1e6d7-108">After resuming, hello clock of hello virtual machine is automatically synchronized.</span></span>

<span data-ttu-id="1e6d7-109">Niet alle updates kunnen worden geïmplementeerd met behulp van dit mechanisme, maar gegeven de periode korte pauze impact toovirtual machines implementeren van updates in deze manier aanzienlijk minder.</span><span class="sxs-lookup"><span data-stu-id="1e6d7-109">Not all updates can be deployed by using this mechanism, but given the short pause period, deploying updates in this way greatly reduces impact toovirtual machines.</span></span>

<span data-ttu-id="1e6d7-110">Meerdere exemplaren updates (VM's in een beschikbaarheidsset) zijn toegepaste één updatedomein tegelijk.</span><span class="sxs-lookup"><span data-stu-id="1e6d7-110">Multi-instance updates (VMs in an availability set) are applied one update domain at a time.</span></span>

<span data-ttu-id="1e6d7-111">Sommige toepassingen worden beïnvloed door deze meer dan andere updates.</span><span class="sxs-lookup"><span data-stu-id="1e6d7-111">Some applications may be impacted by these updates more than others.</span></span> <span data-ttu-id="1e6d7-112">Toepassingen die de verwerking van realtime-gebeurtenissen, mediastreaming of transcodering of hoge doorvoersnelheid networking scenario's, bijvoorbeeld mogelijk niet ontworpen tootolerate een pauze van 30 seconde.</span><span class="sxs-lookup"><span data-stu-id="1e6d7-112">Applications that perform real-time event processing, media streaming or transcoding, or high throughput networking scenarios, for example, may not be designed tootolerate a 30 second pause.</span></span> <span data-ttu-id="1e6d7-113">Toepassingen die worden uitgevoerd in een virtuele machine kunnen leren over toekomstige updates door aanroepen Hallo [gepland gebeurtenissen](../virtual-machines-scheduled-events.md) API Hallo [Azure metagegevens Service](../virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1e6d7-113">Applications running in a virtual machine can learn about upcoming updates by calling hello [Scheduled Events](../virtual-machines-scheduled-events.md) API of hello [Azure Metadata Service](../virtual-machines-instancemetadataservice-overview.md).</span></span>
