---
title: aaaMigrate van AWS en andere platforms tooManaged schijven in Azure | Microsoft Docs
description: "Virtuele machines in Azure met behulp van VHD's geüpload uit andere clouds zoals AWS of andere virtualisatieplatforms maken en te profiteren van beheerde Azure-schijven."
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
ms.date: 02/07/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 66c3912397ab905aafb3910e13ac711befb8f502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-amazon-web-services-aws-and-other-platforms-toomanaged-disks-in-azure"></a>Migreren van Amazon Web Services (AWS) en andere platforms tooManaged schijven in Azure

U kunt VHD-bestanden van AWS of on-premises virtualisatie oplossingen tooAzure toocreate virtuele machines die van beheerde schijven gebruikmaken uploaden. Azure-beheerde schijven verwijdert Hallo behoefte van toomanaging storage-accounts voor Azure IaaS VM's. U hebt tooonly Hallo type (Premium of standaard) en de grootte van de schijf die u moet opgeven en Azure wordt gemaakt en beheerd Hallo schijf voor u. 

U kunt algemene en gespecialiseerde VHD's uploaden. 
- **VHD gegeneraliseerd** -heeft al uw persoonlijke accountgegevens verwijderd met behulp van Sysprep. 
- **VHD gespecialiseerde** -onderhoudt Hallo gebruikersaccounts, toepassingen en andere statusgegevens van uw oorspronkelijke VM. 

> [!IMPORTANT]
> Voordat u een VHD-tooAzure uploadt, u moet volgen [voorbereiden van een Windows-VHD of VHDX tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
>
>


| Scenario                                                                                                                         | Documentatie                                                                                                                       |
|----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| U hebt een bestaande EC2 AWS-exemplaren dat u toomigrate tooAzure beheerde schijven kan de configuratie                                     | [Een virtuele machine verplaatsen van tooAzure Amazon Web Services (AWS)](aws-to-azure.md)                           |
| U hebt een virtuele machine uit en andere virtualisatieplatform dat u toouse toouse als een installatiekopie toocreate wilt meerdere Azure-virtuele machines. | [Een gegeneraliseerde VHD uploaden en toocreate een nieuwe virtuele machines in Azure gebruiken](upload-generalized-managed.md) |
| U hebt een unieke aangepaste virtuele machine die u toorecreate in Azure wilt.                                                      | [Een speciale VHD tooAzure uploaden en een nieuwe virtuele machine maken](create-vm-specialized.md)         |


## <a name="overview-of-managed-disks"></a>Overzicht van beheerde schijven

Azure-beheerde schijven vereenvoudigt VM beheer door het verwijderen van Hallo nodig toomanage storage-accounts. Schijven die worden beheerd ook voordeel van betere betrouwbaarheid van virtuele machines in een Beschikbaarheidsset. Hiermee zorgt u ervoor dat de schijven Hallo van andere virtuele machines in een Beschikbaarheidsset voldoende geïsoleerd van elk andere tooavoid één punt van fouten worden. Schijven met een andere virtuele machines automatisch geplaatst in een Beschikbaarheidsset in verschillende opslagunits (stempels) Hiermee beperkt u Hallo impact van één scale unit Opslagfouten veroorzaakt vervaldatums toohardware-en software. Op basis van uw behoeften, kunt u kiezen uit twee soorten opties voor opslag: 
 
- [Premium-schijven beheerd](../../storage/common/storage-premium-storage.md) Solid State station (SSD) op basis van opslagmedia opslag die highperformance, schijfondersteuning voor virtuele machines met I/O-intensieve werkbelastingen met lage latentie zorgt. U kunt profiteren van Hallo snelheid en prestaties van deze schijven migreren tooPremium beheerd schijven op te nemen.  

- [Standard-beheerde schijven](../../storage/common/storage-standard-storage.md) opslagmedia harde schijf (HDD) op basis van gebruik en geschikt zijn voor het ontwikkelen en testen en andere werkbelastingen incidentele toegang die minder gevoelig tooperformance variabiliteit zijn.  

## <a name="plan-for-hello-migration-toomanaged-disks"></a>Hallo-migratie plannen tooManaged schijven

Deze sectie helpt u bij toomake Hallo beste beslissing op schijf en VM-typen.


### <a name="location"></a>Locatie

Kies een locatie waar Azure beheerd schijven beschikbaar zijn. Als u tooPremium beheerd schijven migreert, zorg er ook voor Premium-opslag is beschikbaar in Hallo regio waar u van plan bent toomigrate aan. Zie [Azure-Services per regio](https://azure.microsoft.com/regions/#services) voor actuele informatie over beschikbare locaties.

### <a name="vm-sizes"></a>Formaten van virtuele machines

Als u tooPremium beheerd schijven migreert, hebt u tooupdate Hallo grootte van Hallo VM tooPremium kan grootte van de opslagruimte beschikbaar is in Hallo regio waar de VM zich bevindt. Bekijk Hallo VM-grootten die Premium-opslag die geschikt zijn. Hello Azure VM-grootte specificaties worden vermeld in [grootten voor virtuele machines](sizes.md).
Bekijk de prestatiekenmerken Hallo van virtuele machines die geschikt is voor Premium-opslag en kies Hallo meest geschikte VM-grootte die het beste past bij uw werkbelasting. Zorg ervoor dat er voldoende bandbreedte beschikbaar op uw VM toodrive Hallo schijf verkeer is.

### <a name="disk-sizes"></a>Schijfformaten

**Premium beheerde schijven**

Er zijn drie soorten beheerde Premium-schijven die kunnen worden gebruikt met uw virtuele machine en elke principal heeft bepaalde IOPs en doorvoerlimieten limieten. Houd rekening met deze limieten bij het kiezen van Hallo Premium schijftype voor uw virtuele machine op basis van Hallo behoeften van uw toepassing in termen van capaciteit, prestaties, schaalbaarheid en piek worden geladen.

| Premium-schijven Type  | P10               | P20               | P30               |
|---------------------|-------------------|-------------------|-------------------|
| Schijfgrootte           | 128 GB            | 512 GB            | 1024 GB (1 TB)    |
| IOP's per schijf       | 500               | 2300              | 5000              |
| Doorvoer per schijf | 100 MB per seconde | 150 MB per seconde | 200 MB per seconde |

**Beheerde standaardschijven**

Er zijn vijf typen Standard-beheerde schijven die kunnen worden gebruikt met uw virtuele machine. Elk van deze andere capaciteit hebben maar dezelfde IOPS en doorvoerlimieten hebben. Standard-beheerde schijven op basis van de capaciteitsbehoeften Hallo van uw toepassing hello type kiezen.

| Standard-schijftype  | S4               | S6               | S10              | S20              | S30              |
|---------------------|------------------|------------------|------------------|------------------|------------------|
| Schijfgrootte           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   |
| IOP's per schijf       | 500              | 500              | 500              | 500              | 500              |
| Doorvoer per schijf | 60 MB per seconde | 60 MB per seconde | 60 MB per seconde | 60 MB per seconde | 60 MB per seconde |

### <a name="disk-caching-policy"></a>Het beleid voor schijf 

**Premium beheerde schijven**

Beleid voor de schijfcache is standaard *alleen-lezen* voor alle gegevensschijven Premium, Hallo en *lezen-schrijven* voor Hallo Premium besturingssysteemschijf gekoppeld toohello VM. Deze configuratieinstelling wordt aanbevolen tooachieve Hallo optimale prestaties voor uw toepassing IOs. Voor schijven schrijven zware of alleen-schrijven gegevens (zoals SQL Server-logboekbestanden), uitschakelen schijfcache, zodat u kunt betere prestaties bereiken.

### <a name="pricing"></a>Prijzen

Bekijk Hallo [prijzen voor schijven beheerd](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Prijzen van beheerde Premium-schijven is hetzelfde als Hallo onbeheerde Premium-schijven. Maar prijzen voor beheerde standaardschijven is anders dan standaardschijven zonder begeleiding.


## <a name="next-steps"></a>Volgende stappen

- Voordat u een VHD-tooAzure uploadt, u moet volgen [voorbereiden van een Windows-VHD of VHDX tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
