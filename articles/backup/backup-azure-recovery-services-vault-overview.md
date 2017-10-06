---
title: aaaOverview van Recovery Services-kluizen | Microsoft Docs
description: Een overzicht en de vergelijking tussen de Recovery Services-kluizen en Azure Backup-kluizen.
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.assetid: 38d4078b-ebc8-41ff-9bc8-47acf256dc80
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/15/2017
ms.author: markgal;arunak
ms.openlocfilehash: 77dd9ece7fe86429cc6f9a47a68b5150a1f4af71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vaults-overview"></a>Overzicht van Recovery Services-kluizen

In dit artikel beschrijft Hallo functies van een Recovery Services-kluis. Een Recovery Services-kluis is een entiteit opslag in Azure met gegevens. Hallo-gegevens zijn meestal kopieën van gegevens of configuratie-informatie voor virtuele machines (VM's), werkbelastingen, servers of werkstations. Een Recovery Services-kluis is Hallo Resource Manager-versie van een back-upkluis. Microsoft raadt u toouse Recovery Services-kluizen en tooconvert back-up-kluizen tooRecovery Services-kluizen.

## <a name="what-is-a-recovery-services-vault"></a>Wat is een Recovery Services-kluis?

Een Recovery Services-kluis is dat een entiteit online opslag in Azure gebruikt toohold gegevens zoals back-ups en herstelpunten back-upbeleid. U kunt de Recovery Services-kluizen toohold back-upgegevens gebruiken voor verschillende Azure-services zoals IaaS VM's (Linux of Windows) en Azure SQL-databases. Recovery Services-kluizen ondersteuning van System Center DPM, Windows Server back-upserver van Azure, en meer. Recovery Services-kluizen maken het gemakkelijk tooorganize uw back-upgegevens, terwijl de beheeroverhead minimaliseert.

U kunt zoveel Recovery Services-kluizen als u wilt maken binnen een Azure-abonnement.

## <a name="comparing-recovery-services-vaults-and-backup-vaults"></a>Vergelijken Recovery Services-kluizen en back-upkluizen

Recovery Services-kluizen zijn gebaseerd op Hallo Azure Resource Manager-model van Azure, terwijl de Backup-kluizen zijn gebaseerd op Hallo Azure Service Manager-model. Wanneer u een upgrade uitvoert van een Backup-kluis tooa Recovery Services-kluis, blijft de back-upgegevens Hallo intact tijdens en na de upgrade Hallo. Recovery Services-kluizen bieden, zoals functies die niet beschikbaar voor de Backup-kluizen:

- **Uitgebreide mogelijkheden toohelp veilige back-upgegevens**: met Recovery Services-kluizen, Azure Backup biedt beveiliging mogelijkheden tooprotect cloudback-ups. Deze beveiligingsfuncties Zorg ervoor dat u kunt uw back-ups te beveiligen en veilig gegevens herstellen vanaf back-ups van de cloud, zelfs als de productie- en back-up-servers worden getroffen. [Meer informatie](backup-azure-security-feature.md)

- **Centrale bewaking voor uw hybride IT-omgeving**: met Recovery Services-kluizen, kunt u controleren niet alleen uw [Azure IaaS VM's](backup-azure-manage-vms.md) , maar ook uw [lokale activa](backup-azure-manage-windows-server.md#manage-backup-items) vanuit een centrale portal. [Meer informatie](http://azure.microsoft.com/blog/alerting-and-monitoring-for-azure-backup)

- **Op rollen gebaseerde toegangsbeheer (RBAC)**: RBAC verfijnd toegangsbeheer management in Azure biedt. [Azure biedt diverse ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md), en de Azure Backup bevat drie [ingebouwde rollen toomanage herstelpunten](backup-rbac-rs-vault.md). Recovery Services-kluizen compatibel zijn met RBAC waarmee de beperkt back-up en herstel toegang toohello gedefinieerd set van gebruikersrollen. [Meer informatie](backup-rbac-rs-vault.md)

- **Alle configuraties van Azure Virtual Machines beveiligen**: Recovery Services-kluizen beveiligen Resource Manager gebaseerde virtuele machines met inbegrip van Premium-schijven, schijven beheerd en virtuele machines versleuteld. Upgraden van een back-up kluis tooa Recovery Services-kluis biedt u kans tooupgrade Hallo uw virtuele machines op basis van Service Manager tooResource Manager gebaseerde virtuele machines. Tijdens het upgraden van de kluis hello, kunt u uw herstelpunten op basis van Service Manager VM bewaren en configureren van beveiliging voor Hallo VMs (Resource Manager is ingeschakeld bijgewerkt). [Meer informatie](http://azure.microsoft.com/blog/azure-backup-recovery-services-vault-ga)

- **Chatberichten terugzetten voor IaaS VM's**: met behulp van Recovery Services-kluizen, kunt u bestanden terugzetten en mappen in een IaaS VM zonder te herstellen Hallo hele virtuele machine, waardoor sneller worden hersteld. Chatberichten terugzetten voor IaaS VM's is beschikbaar voor zowel Windows als een virtuele Linux-machines. [Meer informatie](http://azure.microsoft.com/blog/instant-file-recovery-from-azure-linux-vm-backup-using-azure-backup-preview)

## <a name="managing-your-recovery-services-vaults-in-hello-portal"></a>Het beheren van de Recovery Services-kluizen in Hallo-portal
Maken en beheren van de Recovery Services-kluizen in hello Azure-portal is eenvoudig omdat Hallo Backup-service is geïntegreerd in hello Azure instellingenblade. Deze integratie zorgt ervoor dat u kunt maken of beheren van een Recovery Services-kluis *in de context van de doelservice Hallo Hallo*. Bijvoorbeeld: tooview Hallo herstelpunten voor een virtuele machine, selecteert u deze en klikt u op **back-up** op de blade Hallo-instellingen. Hallo back-upgegevens specifieke toothat VM wordt weergegeven. In Hallo bijvoorbeeld na **ContosoVM** Hallo-naam van Hallo virtuele machine is. **ContosoVM demovault** heet Hallo Hallo Recovery Services-kluis. U hoeft niet tooremember Hallo-naam van Hallo Recovery Services-kluis die Hallo herstelpunten opslaat, u kunt deze informatie kunt openen vanaf Hallo virtuele machine.  

![Recovery services-kluis details VM](./media/backup-azure-recovery-services-vault-overview/rs-vault-in-context.png)

Als meerdere servers worden beschermd met Hallo kan dezelfde Recovery Services-kluis, dit meer logische toolook op Hallo die Recovery Services-kluis. U kunt zoeken naar alle Recovery Services-kluizen in Hallo-abonnement en maak een keuze uit de lijst Hallo.

Hallo bevatten volgende secties koppelingen tooarticles waarin wordt uitgelegd hoe toouse een Recovery Services-kluis in elk type activiteit.

### <a name="back-up-data"></a>Back-up van gegevens
- [Back-up van een Azure VM](backup-azure-vms-first-look-arm.md)
- [Back-up van Windows Server of Windows-werkstation](backup-try-azure-backup-in-10-mins.md)
- [Back-up DPM workloads tooAzure](backup-azure-dpm-introduction.md)
- [Tooback van de werkbelasting met behulp van Azure Backup-Server voorbereiden](backup-azure-microsoft-azure-backup.md)

### <a name="manage-recovery-points"></a>Herstelpunten beheren
- [Back-ups van virtuele machine in Azure beheren](backup-azure-manage-vms.md)
- [Bestanden en mappen beheren](backup-azure-manage-windows-server.md)

### <a name="restore-data-from-hello-vault"></a>Gegevens terugzetten vanaf Hallo kluis
- [Afzonderlijke bestanden terugzetten vanuit een virtuele machine in Azure](backup-azure-restore-files-from-vm.md)
- [Een Azure-virtuele machine herstellen](backup-azure-arm-restore-vms.md)

### <a name="secure-hello-vault"></a>Beveiligde Hallo kluis
- [Back-upgegevens van de cloud in de Recovery Services-kluizen beveiligen](backup-azure-security-feature.md)



## <a name="next-steps"></a>Volgende stappen
Hallo volgende artikel voor gebruiken:</br>
[Back-up van een IaaS VM](backup-azure-arm-vms-prepare.md)</br>
[Back-up van een Azure Backup-Server](backup-azure-microsoft-azure-backup.md)</br>
[Back-up van een Windows-Server](backup-configure-vault.md)
