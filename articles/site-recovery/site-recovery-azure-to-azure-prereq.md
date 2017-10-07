---
title: aaaPrerequisites voor replicatie tooAzure met behulp van Azure Site Recovery | Microsoft Docs
description: In dit artikel bevat een overzicht van vereisten voor het repliceren van virtuele machines en fysieke machines tooAzure met hello Azure Site Recovery-service.
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/01/2017
ms.author: rajanaki
ms.openlocfilehash: c66cea8b097a872bae57e7b42e659e58c4b0b1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replicating-azure-virtual-machines-tooanother-region-by-using-azure-site-recovery"></a>Vereisten voor het repliceren van virtuele machines in Azure tooanother regio met behulp van Azure Site Recovery

> [!div class="op_single_selector"]
> * [Repliceren vanaf Azure tooAzure](site-recovery-azure-to-azure-prereq.md)
> * [Repliceren vanaf de lokale tooAzure](site-recovery-prereq.md)

Hello Azure Site Recovery-service bijdraagt tooyour zakelijke continuïteit en noodherstelplan (BCDR) door te organiseren:
* Replicatie van virtuele machines in Azure tooanother Azure-regio.
* Replicatie van on-premises fysieke servers en virtuele machines tooAzure of tooa secundaire datacentrum. 

Wanneer er storingen optreden op uw primaire locatie, kunt u failover-overschakeling tooa secundaire locatie tookeep toepassingen en workloads beschikbaar. U kunt primaire locatie back tooyour mislukken wanneer deze toonormal bewerkingen weer. Zie voor meer informatie over Site Recovery [wat is Site Recovery?](site-recovery-overview.md).

In dit artikel bevat een overzicht van Hallo vereisten Site Recovery de replicatie van lokale tooAzure toobegin vereist.

Na de eventuele opmerkingen onder Hallo van Hallo artikel of technische vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="azure-requirements"></a>Azure-vereisten

**Vereiste** | **Details**
--- | ---
**Azure-account** | Een [Microsoft Azure](http://azure.microsoft.com/) account.<br/><br/> U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).
**Site Recovery-service** | Zie voor meer informatie over prijzen voor Site Recovery [prijzen voor Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/). U wordt aangeraden dat u een Recovery Services-kluis in Hallo doel-Azure-regio maken die u toouse als herstellocatie na noodgevallen wilt. Bijvoorbeeld, als uw virtuele bronmachines worden uitgevoerd in de VS-Oost en u tooreplicate tooCentral ons wilt, raden wij u Hallo kluis maken in VS-midden.|
**Azure capaciteit** | Voor Hallo doel Azure-regio dat u toouse wilt gebruiken als uw locatie van de herstel na noodgevallen, moet u een abonnement met voldoende capaciteit voor virtuele machines, opslagaccounts en netwerkonderdelen toohave. Neem contact op met ondersteuning tooadd meer capaciteit.
**Richtlijnen voor opslag** | Zorg ervoor dat u Hallo volgt [richtlijnen voor opslag](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) voor de bron van Azure virtual machines tooavoid eventuele prestatieproblemen. Als u de standaardinstellingen Hallo volgt, maakt Site Recovery Hallo vereist storage-accounts op basis van Hallo bron configuratie. Als u aanpassen en uw eigen instellingen selecteert, zorg ervoor dat u Hallo volgt [schaalbaarheidsdoelen voor virtuele-machineschijven](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
**Richtlijnen voor netwerken** | U moet toowhitelist Hallo uitgaande verbinding van uw Azure-VM voor specifieke URL's of het IP-adresbereiken. Raadpleeg voor meer informatie, toohello [richtlijnen voor het repliceren van virtuele machines van Azure toegang](site-recovery-azure-to-azure-networking-guidance.md) artikel.
**Azure VM** | Zorg ervoor dat alle Hallo nieuwste basiscertificaten op Hallo Windows of Linux-VM. Als de meest recente basiscertificaten Hallo niet aanwezig zijn, niet Hallo VM geregistreerde tooSite herstel vanwege toosecurity beperkingen worden.

>[!NOTE]
>Lees voor meer informatie over ondersteuning voor specifieke configuraties Hallo [ondersteuningsmatrix](site-recovery-support-matrix-azure-to-azure.md).

## <a name="next-steps"></a>Volgende stappen
- Meer informatie over [richtlijnen voor het repliceren van virtuele machines van Azure toegang](site-recovery-azure-to-azure-networking-guidance.md).
- Beginnen met het beveiligen van uw werkbelastingen door [virtuele Azure-machines repliceren](site-recovery-azure-to-azure.md).
