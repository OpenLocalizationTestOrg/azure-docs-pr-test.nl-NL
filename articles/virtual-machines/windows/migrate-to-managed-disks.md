---
title: Azure Virtual machines tooManaged schijven aaaMigrate | Microsoft Docs
description: Azure virtuele machines die zijn gemaakt met behulp van niet-beheerde schijven in de storage-accounts toouse beheerde schijven migreren.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 29420f13c4ffd5b25726e0ef1aafe89347286a89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-vms-toomanaged-disks-in-azure"></a>Migreren van virtuele Azure-machines tooManaged schijven in Azure

Azure-schijven die worden beheerd vereenvoudigt het beheer van uw opslag door het verwijderen van Hallo nodig tooseparately storage-accounts beheren.  U kunt ook uw bestaande virtuele Azure-machines tooManaged schijven toobenefit migreren van betere betrouwbaarheid van virtuele machines in een Beschikbaarheidsset. Hiermee zorgt u ervoor dat de schijven Hallo van andere virtuele machines in een Beschikbaarheidsset voldoende geïsoleerd van elk andere tooavoid één punt van fouten worden. Schijven met een andere virtuele machines automatisch geplaatst in een Beschikbaarheidsset in verschillende opslagunits (stempels) Hiermee beperkt u Hallo impact van één scale unit Opslagfouten veroorzaakt vervaldatums toohardware-en software.
Op basis van uw behoeften, kunt u kiezen uit twee soorten opties voor opslag:

- [Premium-schijven beheerd](../../storage/common/storage-premium-storage.md) Solid State station (SSD) op basis van opslagmedia die highperformance, schijfondersteuning voor virtuele machines met I/O-intensieve werkbelastingen met lage latentie zorgt. U kunt profiteren van Hallo snelheid en prestaties van deze schijven migreren tooPremium beheerd schijven op te nemen.

- [Standard-beheerde schijven](../../storage/common/storage-standard-storage.md) opslagmedia harde schijf (HDD) op basis van gebruik en geschikt zijn voor het ontwikkelen en testen en andere werkbelastingen incidentele toegang die minder gevoelig tooperformance variabiliteit zijn.

U kunt migreren tooManaged schijven in de volgende scenario's:

| Migreren...                                            | Koppeling van documentatie                                                                                                                                                                                                                                                                  |
|----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Zelfstandige virtuele machines en virtuele machines in een beschikbaarheidsgroep set toomanaged schijven converteren   | [Virtuele machines toouse beheerd schijven converteren](convert-unmanaged-to-managed-disks.md) |
| Een enkele virtuele machine van klassieke tooResource Manager op beheerde schijven     | [Een enkele virtuele machine migreren](migrate-single-classic-to-resource-manager.md)  | 
| Alle Hallo-VM's in een vNet van klassieke tooResource Manager op beheerde schijven     | [Migreren van IaaS-resources van klassieke tooResource Manager](migration-classic-resource-manager-ps.md) en vervolgens [een virtuele machine van niet-beheerde schijven toomanaged schijven converteren](convert-unmanaged-to-managed-disks.md) | 






## <a name="plan-for-hello-conversion-toomanaged-disks"></a>Plannen voor de conversie Hallo tooManaged schijven

Deze sectie helpt u bij toomake Hallo beste beslissing op schijf en VM-typen.


## <a name="location"></a>Locatie

Kies een locatie waar Azure beheerd schijven beschikbaar zijn. Als u tooPremium beheerd schijven overstapt, zorg er ook voor Premium-opslag is beschikbaar in Hallo regio waar u van plan bent toomove aan. Zie [Azure-Services per regio](https://azure.microsoft.com/regions/#services) voor actuele informatie over beschikbare locaties.

## <a name="vm-sizes"></a>Formaten van virtuele machines

Als u tooPremium beheerd schijven migreert, hebt u tooupdate Hallo grootte van Hallo VM tooPremium kan grootte van de opslagruimte beschikbaar is in Hallo regio waar de VM zich bevindt. Bekijk Hallo VM-grootten die Premium-opslag die geschikt zijn. Hello Azure VM-grootte specificaties worden vermeld in [grootten voor virtuele machines](sizes.md).
Bekijk de prestatiekenmerken Hallo van virtuele machines die geschikt is voor Premium-opslag en kies Hallo meest geschikte VM-grootte die het beste past bij uw werkbelasting. Zorg ervoor dat er voldoende bandbreedte beschikbaar op uw VM toodrive Hallo schijf verkeer is.

## <a name="disk-sizes"></a>Schijfformaten

**Premium beheerde schijven**

Er zijn zeven soorten beheerde premium-schijven die kunnen worden gebruikt met uw virtuele machine en elke principal heeft bepaalde IOPs en doorvoerlimieten limieten. In overweging nemen deze limieten bij het kiezen van Hallo Premium schijftype voor uw virtuele machine op basis van Hallo behoeften van uw toepassing in termen van capaciteit, prestaties, schaalbaarheid en piek worden geladen.

| Premium-schijven Type  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Schijfgrootte           | 128 GB| 512 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| IOP's per schijf       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Doorvoer per schijf | 25 MB per seconde  | 50 MB per seconde  | 100 MB per seconde | 150 MB per seconde | 200 MB per seconde | 250 MB per seconde | 250 MB per seconde |

**Beheerde standaardschijven**

Er zijn zeven soorten beheerde standaardschijven die kunnen worden gebruikt met uw virtuele machine. Elk van deze andere capaciteit hebben maar dezelfde IOPS en doorvoerlimieten hebben. Standard-beheerde schijven op basis van de capaciteitsbehoeften Hallo van uw toepassing hello type kiezen.

| Standard-schijftype  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| Schijfgrootte           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   | 2048 GB (2TB)    | 4095 GB (4 TB)   | 
| IOP's per schijf       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| Doorvoer per schijf | 60 MB per seconde | 60 MB per seconde | 60 MB per seconde | 60 MB per seconde | 60 MB per seconde | 60 MB per seconde | 60 MB per seconde | 

## <a name="disk-caching-policy"></a>Het beleid voor schijf

**Premium beheerde schijven**

Beleid voor de schijfcache is standaard *alleen-lezen* voor alle gegevensschijven Premium, Hallo en *lezen-schrijven* voor Hallo Premium besturingssysteemschijf gekoppeld toohello VM. Deze configuratieinstelling wordt aanbevolen tooachieve Hallo optimale prestaties voor uw toepassing IOs. Voor schijven schrijven zware of alleen-schrijven gegevens (zoals SQL Server-logboekbestanden), uitschakelen schijfcache, zodat u kunt betere prestaties bereiken.

## <a name="pricing"></a>Prijzen

Bekijk Hallo [prijzen voor schijven beheerd](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Prijzen van beheerde Premium-schijven is hetzelfde als Hallo onbeheerde Premium-schijven. Maar prijzen voor beheerde standaardschijven is anders dan standaardschijven zonder begeleiding.



## <a name="next-steps"></a>Volgende stappen

- Meer informatie over [schijven beheerd](managed-disks-overview.md)
