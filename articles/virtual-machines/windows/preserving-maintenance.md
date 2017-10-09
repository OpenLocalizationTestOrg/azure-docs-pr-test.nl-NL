---
title: AAA VM behouden onderhoud voor Windows-machines in Azure | Microsoft Docs
description: In-place migratie VM voor het geheugen voor het behouden van updates.
services: virtual-machines-windows
documentationcenter: 
author: zivr
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
ms.author: zivr
ms.openlocfilehash: b798f0afd9d8dc60ca8a78f7cc77435a0ddc76fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="vm-preserving-maintenance-with-in-place-vm-migration"></a>VM behouden onderhoud met een VM In-place migratie

Hallo merendeel van de updates hebben geen invloed toohosted virtuele machines, zijn er ook gevallen waarbij updates toocomponents of services ertoe leiden dat minimale storing toorunning virtuele machines (zonder een volledige opnieuw opstarten van Hallo virtuele machine).

Deze updates worden bewerkstelligd met-technologie waarmee in-place live migratie, ook wel 'update geheugen behouden'. Bij het bijwerken van de host Hallo Hallo virtuele machine wordt geplaatst in de modus 'onderbroken' hello geheugen in RAM, behouden terwijl Hallo hostomgeving (bv. het onderliggende besturingssysteem) van toepassing hello vereiste updates en -patches.
Hallo virtuele machine wordt vervolgens hervat binnen 30 seconden wordt onderbroken.
Hallo klok van Hallo virtuele machine is na hervatten, automatisch gesynchroniseerd.

Niet alle updates kunnen worden geïmplementeerd met behulp van dit mechanisme, maar gegeven de periode korte pauze impact toovirtual machines implementeren van updates in deze manier aanzienlijk minder.

Meerdere exemplaren updates (VM's in een beschikbaarheidsset) zijn toegepaste één updatedomein tegelijk.

Sommige toepassingen worden beïnvloed door deze meer dan andere updates. Toepassingen die de verwerking van realtime-gebeurtenissen, mediastreaming of transcodering of hoge doorvoersnelheid networking scenario's, bijvoorbeeld mogelijk niet ontworpen tootolerate een pauze van 30 seconde. Toepassingen die worden uitgevoerd in een virtuele machine kunnen leren over toekomstige updates door aanroepen Hallo [gepland gebeurtenissen](../virtual-machines-scheduled-events.md) API Hallo [Azure metagegevens Service](../virtual-machines-instancemetadataservice-overview.md).
