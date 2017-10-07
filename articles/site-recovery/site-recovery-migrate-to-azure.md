---
title: aaaMigrate tooAzure met Site Recovery | Microsoft Docs
description: In dit artikel biedt een overzicht van migratie virtuele machines en fysieke servers tooAzure met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/05/2017
ms.author: raynew
ms.openlocfilehash: 6e65deee337c5371d441812ddb820dc8bc233684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-tooazure-with-site-recovery"></a>Migreren van tooAzure met Site Recovery

Lees dit artikel voor een overzicht van het gebruik van hello Azure Site Recovery-service voor de migratie van virtuele machines en fysieke servers.

Site Recovery is een Azure-service die tooyour-BCDR-strategie door replicatie van fysieke on-premises servers en virtuele machines toohello cloud (Azure) of tooa secundair datacenter organiseren bijdraagt. Wanneer er storingen optreden op uw primaire locatie, schakelt u over toohello secundaire locatie tookeep toepassingen en workloads beschikbaar. U mislukken back tooyour primaire locatie wanneer deze toonormal bewerkingen weer. Meer informatie vindt u in [Wat is Site Recovery?](site-recovery-overview.md) Ook kunt u Site Recovery toomigrate uw bestaande on-premises werkbelastingen tooAzure tooexpedite uw cloud reis en beschikbare Hallo matrix van functies die Azure biedt.

Voor een snel overzicht van hoe tooperform migratie, raadpleegt u toothis video.
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/ASRHowTo-Video2-Migrate-Virtual-Machines-to-Azure/player]

Dit artikel wordt beschreven implementatie in Hallo [Azure-portal](https://portal.azure.com). Hallo [klassieke Azure-portal](https://manage.windowsazure.com/) kan worden gebruikt toomaintain bestaande Site Recovery-kluizen, maar u kunt geen nieuwe kluizen maken.

Na de eventuele opmerkingen onder Hallo van dit artikel. Technische vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="what-do-we-mean-by-migration"></a>Wat wordt precies bedoeld met 'migreren’?

U kunt Site Recovery implementeren voor de replicatie van de lokale virtuele machines en fysieke servers, tooAzure of tooa secundaire site. Replicatie van machines, ze via failover van de primaire site Hallo wanneer er storingen optreden en failback ervan back toohello primaire site wanneer deze wordt hersteld. In aanvulling toothis, kunt u Site Recovery toomigrate virtuele machines en fysieke servers tooAzure, zodat gebruikers er toegang toe hebt als Azure virtuele machines. Migratie moet replicatie en failover van Hallo primaire site tooAzure en een gebaar van de volledige migratie.

## <a name="what-can-site-recovery-migrate"></a>Wat kan er met Site Recovery worden gemigreerd?

U kunt:

- Migreren van werkbelastingen die worden uitgevoerd op een lokale Hyper-V-machines, virtuele VMware-machines en fysieke servers toorun op Azure Virtual machines. U kunt in dit scenario ook een volledige replicatie en failback uitvoeren.
- [Azure IaaS-VM's](site-recovery-migrate-azure-to-azure.md) migreren tussen Azure-regio's. Momenteel wordt in dit scenario alleen migratie ondersteund, dus geen failback.
- Migreren [AWS Windows-exemplaren](site-recovery-migrate-aws-to-azure.md) tooAzure IaaS VM's. Momenteel wordt in dit scenario alleen migratie ondersteund, dus geen failback.

## <a name="migrate-on-premises-vms-and-physical-servers"></a>Virtuele machines en fysieke servers on-premises migreren

toomigrate lokale Hyper-V-machines, virtuele VMware-machines en fysieke servers, u bijna Hallo dezelfde als bij normale replicatie stappen volgen.

1. Een Recovery Services-kluis instellen
2. Hallo vereist beheerservers configureren (VMware, VMM, Hyper-V -, afhankelijk van wat u wilt toomigrate), deze toohello kluis toevoegen en replicatie-instellingen opgeven.
3. Replicatie inschakelen voor Hallo machines u wilt dat toomigrate
4. Na de initiële migratie Hallo een snelle test failover tooensure dat alles werkt zoals het moet worden uitgevoerd.
5. Nadat u hebt gecontroleerd of de replicatieomgeving werkt, gebruikt u een geplande of niet-geplande failover, afhankelijk van [wat er wordt ondersteund](site-recovery-failover.md) voor uw scenario. We raden u aan om waar mogelijk een geplande failover te gebruiken.
6. Voor de migratie, u hebt toocommit een failover of verwijderen. In plaats daarvan het selecteren van Hallo **volledige migratie** optie voor elke computer die u wilt toomigrate.
     - In **gerepliceerde Items**, met de rechtermuisknop op Hallo VM en klikt u op **volledige migratie**. Klik op **OK** toocomplete. U kunt de voortgang in de eigenschappen van Hallo VM in volgen door de bewaking van Hallo voltooid migratietaak in **Site Recovery-taken**.
     - Hallo **volledige migratie** actie is van het migratieproces Hallo is voltooid, verwijdert u de replicatie voor Hallo machine en Hiermee stopt u Site Recovery facturering voor Hallo machine.

![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

## <a name="migrate-between-azure-regions"></a>Migreren tussen Azure-regio's

Met Site Recovery kunt u virtuele Azure-machines migreren tussen gebieden. In dit scenario wordt alleen migratie ondersteund. Met andere woorden, u kunt repliceren hello Azure VM's en failover tooanother regio, maar het kan geen failback uit voor. In dit scenario dat u een Recovery Services-kluis instelt, een lokale configuratie server toomanage replicatie implementeren, toe te voegen toohello kluis en replicatie-instellingen opgeven. U kunt replicatie inschakelen voor Hallo machines u wilt dat toomigrate en voer een snelle failover testen. U voert een niet-geplande failover Hello **volledige migratie** optie.

## <a name="migrate-aws-tooazure"></a>AWS tooAzure migreren

U kunt AWS exemplaren tooAzure virtuele machines migreren. In dit scenario wordt alleen migratie ondersteund. Met andere woorden, u kunt repliceren Hallo AWS-exemplaren en tooAzure failover echter niet kunt u een failback uit. AWS-exemplaren worden verwerkt in de Hallo dezelfde manier als de fysieke servers voor migratiedoeleinden. Instellen van een Recovery Services-kluis, een lokale configuratie server toomanage replicatie implementeren, voegt u deze toohello kluis, en geeft replicatie-instellingen. U kunt replicatie inschakelen voor Hallo machines u wilt dat toomigrate en voer een snelle failover testen. U voert een niet-geplande failover Hello **volledige migratie** optie.




## <a name="next-steps"></a>Volgende stappen

- [Virtuele VMware-machines tooAzure migreren](site-recovery-vmware-to-azure.md)
- [Hyper-V-machines in VMM-clouds tooAzure migreren](site-recovery-vmm-to-azure.md)
- [Hyper-V-machines migreren zonder VMM tooAzure](site-recovery-hyper-v-site-to-azure.md)
- [Virtuele Azure-machines migreren tussen Azure-regio's](site-recovery-migrate-azure-to-azure.md)
- [AWS exemplaren tooAzure migreren](site-recovery-migrate-aws-to-azure.md)
- [Voorbereiden van de gemigreerde machines tooenable replicatie](site-recovery-azure-to-azure-after-migration.md) tooanother regio voor herstel nodig zijn na noodgevallen.
- Beginnen met het beveiligen van uw werkbelastingen door [virtuele machines in Azure te repliceren.](site-recovery-azure-to-azure.md)
