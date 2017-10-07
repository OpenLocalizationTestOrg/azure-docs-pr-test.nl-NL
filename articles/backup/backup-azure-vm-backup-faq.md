---
title: Veelgestelde vragen over VM Backup aaaAzure | Microsoft Docs
description: 'Toocommon vragen beantwoord over: hoe Azure VM-back-up werkt, beperkingen en wat er gebeurt wanneer toopolicy wijzigingen optreden'
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: azure vm backup, virtuele azure-machines herstellen, back-upbeleid
ms.assetid: c4cd7ff6-8206-45a3-adf5-787f64dbd7e1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: a1ad2cb3a379577a8c4258c8207ce75809e11a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-vm-backup-service"></a>Vragen over hello Azure VM Backup-service
Dit artikel bevat antwoorden toocommon vragen toohelp u snel inzicht in hello Azure VM Backup-onderdelen. In sommige Hallo-antwoorden zijn er koppelingen toohello artikelen waarvoor uitgebreide informatie. U kunt ook vragen over Azure Backup-service Hallo boeken in Hallo [discussieforum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="configure-backup"></a>Back-up configureren
### <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>Ondersteunen Recovery Services-kluizen klassieke virtuele machines of virtuele machines op basis van Resource Manager? <br/>
Recovery Services-kluizen ondersteunen beide modellen.  U kunt back-up een klassieke virtuele machine (gemaakt in Hallo-Classic-portal), of een Resource Manager VM (gemaakt in hello Azure-portal) tooa die Recovery Services-kluis.

### <a name="what-configurations-are-not-supported-by-azure-vm-backup-"></a>Welke configuraties worden niet ondersteund door Azure VM Backup?
Lees de informatie over [ondersteunde besturingssystemen](backup-azure-arm-vms-prepare.md#supported-operating-system-for-backup) en [beperkingen van Azure VM Backup](backup-azure-arm-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)

### <a name="why-cant-i-see-my-vm-in-configure-backup-wizard"></a>Waarom zie ik mijn virtuele machine niet in de wizard Back-up configureren?
In de wizard Back-up configureren geeft Azure Backup alleen virtuele machines weer die:
* U kunt nog niet beveiligd - Hallo back-status van een virtuele machine controleren door te gaan tooVM blade en controleren van de status van de back-up van het Menu van Hallo-blade instellingen. Meer informatie over het te[Controleer de status van de back-up van een virtuele machine](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-vm-management-blade)
* Toosame regio hoort als virtuele machine

## <a name="backup"></a>Back-up
### <a name="will-on-demand-backup-job-follow-same-retention-schedule-as-scheduled-backups"></a>Geldt voor back-uptaken op aanvraag hetzelfde bewaarschema als voor geplande back-ups?
Nee. U moet toospecify Hallo bewaartermijn voor een back-uptaak op aanvraag. Bij activering vanuit de portal wordt een dergelijke taak standaard 30 dagen bewaard. 

### <a name="i-recently-enabled-azure-disk-encryption-on-some-vms-will-my-backups-continue-toowork"></a>Ik heb onlangs Azure Disk Encryption ingeschakeld op een aantal virtuele machines. Mijn back-ups toowork blijven?
U hebt toogive machtigingen nodig voor Azure Backup-service tooaccess Sleutelkluis. De hiervoor benodigde machtigingen kunt u in PowerShell opgeven door de stappen te volgen die worden beschreven in het gedeelte *Back-up inschakelen* van de documentatie voor [PowerShell](backup-azure-vms-automation.md).

### <a name="i-migrated-disks-of-a-vm-toomanaged-disks-will-my-backups-continue-toowork"></a>Ik schijven van de schijven van een VM toomanaged gemigreerd. Mijn back-ups toowork blijven?
Ja, back-ups naadloos werkt en er geen noodzaak toore-back-up configureren. 

## <a name="restore"></a>Herstellen
### <a name="how-do-i-decide-between-restoring-disks-versus-full-vm-restore"></a>Hoe bepaal ik of ik beter afzonderlijke schijven kan herstellen of de virtuele machine als geheel?
Met de Azure-functie voor het herstellen van de virtuele machine als geheel hebt u snel de beschikking over een herstelde virtuele machine. Virtuele machine herstellen optie Hallo namen van schijven wordt gewijzigd, containers die worden gebruikt door de schijven, openbare IP-adressen, netwerkinterface namen voor Uniekheid van bronnen ophalen gemaakt als onderdeel van het maken van VM. Dit wordt ook Hallo VM tooavailability set niet toevoegen. 

Gebruik de optie voor het herstellen van afzonderlijke schijven voor het volgende:
* Hallo VM die wordt gemaakt van een punt in tijd configuratie zoals Hallo grootte wijzigen van de back-upconfiguratie aanpassen
* De configuraties die niet aanwezig op moment van back-up Hallo zijn toevoegen 
* Besturingselement Hallo naamgevingsconventie voor resources ophalen van gemaakt
* VM tooavailability set toevoegen
* U hebt een configuratie die alleen kan worden uitgevoerd met PowerShell of een declaratieve sjabloondefinitie

## <a name="manage-vm-backups"></a>Back-ups van uw virtuele machine beheren
### <a name="what-happens-when-i-change-a-backup-policy-on-vms"></a>Wat gebeurt er wanneer ik het back-upbeleid voor een of meer virtuele machines wijzig?
Wanneer een nieuw beleid wordt toegepast op VM('s), worden de planning en het bewaren van het nieuwe beleid Hallo gevolgd. Als de bewaarperiode is uitgebreid, bestaande herstelpunten tookeep gemarkeerd ze volgens het beleid voor nieuwe. Als de bewaartermijn wordt beperkt, ze zijn gemarkeerd voor verwijderen in de volgende opschoontaak Hallo en wordt verwijderd. 
