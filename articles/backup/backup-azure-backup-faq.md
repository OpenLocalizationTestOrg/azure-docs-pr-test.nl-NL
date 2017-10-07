---
title: Veelgestelde vragen over Backup aaaAzure | Microsoft Docs
description: 'Toocommon vragen beantwoord over: Azure Backup-functies zoals Recovery Services-kluizen, wat het back-up, hoe het werkt, versleuteling en limieten. '
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: back-up en herstel na noodgeval; Backup-service
ms.assetid: 1011bdd6-7a64-434f-abd7-2783436668d7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/21/2017
ms.author: markgal;arunak;trinadhk;
ms.openlocfilehash: 3338f7620bcc6ebf53c9c161191f2d8bca1a29da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-service"></a>Vragen over hello Azure Backup-service
Dit artikel bevat antwoorden toocommon vragen toohelp u snel inzicht in hello Azure Backup-onderdelen. In sommige Hallo-antwoorden zijn er koppelingen toohello artikelen waarvoor uitgebreide informatie. U kunt vragen over Azure Backup door te klikken op **opmerkingen** (toohello rechts). Opmerkingen worden weergegeven onder Hallo van dit artikel. Een Livefyre-account is vereist toocomment. U kunt ook vragen over Azure Backup-service Hallo boeken in Hallo [discussieforum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

tooquickly scan Hallo secties in dit artikel gebruiken Hallo koppelingen toohello rechts onder **In dit artikel**.


## <a name="recovery-services-vault"></a>Recovery Services-kluis

### <a name="is-there-any-limit-on-hello-number-of-vaults-that-can-be-created-in-each-azure-subscription-br"></a>Is er een limiet op Hallo aantal kluizen dat kan worden gemaakt in elk Azure-abonnement? <br/>
Ja. Vanaf september 2016 kunt u per abonnement 25 Recovery Services- of Backup-kluizen maken. U kunt too25 Recovery Services maken kluizen per ondersteunde regio van Azure Backup per abonnement. Als u extra kluizen nodig hebt, maakt u een extra abonnement.

### <a name="are-there-limits-on-hello-number-of-serversmachines-that-can-be-registered-against-each-vault-br"></a>Zijn er beperkingen met betrekking tot Hallo aantal servers/machines dat kan worden geregistreerd voor elke kluis? <br/>
Ja, u kunt van too50 machines per kluis registreren. Hallo limiet is voor Azure IaaS virtuele machines, 200 VM's per kluis. Als u tooregister meer machines moet, maakt u een andere kluis.

### <a name="if-my-organization-has-one-vault-how-can-i-isolate-one-servers-data-from-another-server-when-restoring-databr"></a>Als mijn organisatie één kluis heeft, hoe kan ik bij het herstellen van gegevens de gegevens van de ene server dan isoleren van de gegevens van een andere server?<br/>
Alle servers die zijn geregistreerd toohello dezelfde kluis kunt herstellen Hallo gegevensback-ups door andere servers *die gebruikmaken van dezelfde wachtwoordzin Hallo*. Als u servers waarvan back-upgegevens hebt gewenste tooisolate van andere servers in uw organisatie, gebruikt u een speciale wachtwoordzin voor die servers. U kunt bijvoorbeeld verschillende wachtwoordzinnen voor de human resource-server, de accountingserver en de opslagserver gebruiken.

### <a name="can-i-migrate-my-backup-data-or-vault-between-subscriptions-br"></a>Kan ik mijn back-upgegevens- of back-upkluis 'migreren' tussen abonnementen? <br/>
Nee. Hallo-kluis is gemaakt op abonnementsniveau en kan niet opnieuw toegewezen tooanother abonnement zodra deze gemaakt.

### <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>Recovery Services-kluizen zijn op basis van Resource Manager. Worden Backup-kluizen (klassieke modus) nog steeds ondersteund? <br/>
Alle bestaande back-upkluizen in Hallo [klassieke portal](https://manage.windowsazure.com) gaan toobe ondersteund. U kunt echter niet meer Hallo klassieke portal toodeploy nieuwe back-upkluizen gebruiken. Microsoft raadt Recovery Services-kluizen voor alle implementaties omdat toekomstige verbeteringen tooRecovery Services-kluizen, alleen van toepassing. Als u een back-upkluis in de klassieke portal Hallo toocreate probeert, kunt u zich omgeleide toohello [Azure-portal](https://portal.azure.com).

### <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>Kan ik een Backup-kluis tooa Recovery Services-kluis migreren? <br/>
Helaas Nee, migreren u niet Hallo inhoud van een back-up kluis tooa die Recovery Services-kluis. We zijn bezig met het toevoegen van de functionaliteit, maar deze is momenteel nog niet beschikbaar.

### <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>Ik heb in een Backup-kluis een back-up gemaakt van mijn klassieke virtuele machines. Kan ik mijn virtuele machines migreren vanuit de klassieke modus tooResource Manager modus en beveiligt u ze in een Recovery Services-kluis?
Klassieke VM herstelpunten in een back-upkluis migreren niet automatisch tooa Recovery Services-kluis wanneer u Hallo VM van klassieke tooResource Manager-modus verplaatsen. Volg deze stappen tootransfer uw VM back-ups:

1. Ga in de Hallo Backup-kluis, toohello **beveiligde Items** tabblad en selecteer Hallo VM. Klik op [Beveiliging stoppen](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Laat de optie *Gekoppelde back-upgegevens verwijderen* **uitgeschakeld**.
2. Hallo back-up/momentopname uitbreiding uit Hallo VM verwijderen.
3. Hallo virtuele machine migreren vanuit de klassieke modus tooResource Manager-modus. Zorg ervoor dat Hallo opslag en netwerk informatie is ook de bijbehorende toohello virtuele machine gemigreerd tooResource Manager-modus.
4. Een Recovery Services-kluis maken en configureren op Hallo back-up met behulp van virtuele machine gemigreerd **back-** actie boven op het kluisdashboard. Voor gedetailleerde informatie over back-ups van een VM tooa Recovery Services-kluis, Zie Hallo artikel [Azure VM's beveiligen met een Recovery Services-kluis](backup-azure-vms-first-look-arm.md).

## <a name="azure-backup-agent"></a>Azure Backup-agent
Een uitgebreide lijst met vragen vindt u in [FAQ on Azure file-folder backup](backup-azure-file-folder-backup-faq.md) (Veelgestelde vragen over het maken van back-ups van Azure-bestandsmappen)

## <a name="azure-vm-backup"></a>Azure VM Backup
Een uitgebreide lijst met vragen vindt u in [Veelgestelde vragen over Azure VM Backup](backup-azure-vm-backup-faq.md)

## <a name="back-up-vmware-servers"></a>Back-ups maken van VMware-servers

### <a name="can-i-back-up-vmware-vcenter-servers-tooazure"></a>Kan ik back-up VMware vCenter-servers tooAzure?

Ja. U kunt Azure Backup-Server tooback van VMware vCenter- en ESXi tooAzure gebruiken. Zie voor informatie over ondersteunde Hallo VMware versie, Hallo artikel [Azure Backup-Server protection matrix](backup-mabs-protection-matrix.md). Zie voor stapsgewijze instructies [tooback gebruik Azure back-upserver van een server met VMware](backup-azure-backup-server-vmware.md).


## <a name="azure-backup-server-and-system-center-data-protection-manager"></a>Azure Backup-server en System Center Data Protection Manager
### <a name="can-i-use-azure-backup-server-toocreate-a-bare-metal-recovery-bmr-backup-for-a-physical-server-br"></a>Kan ik gebruiken toocreate Azure Backup-Server de back-up van een Bare Metal Recovery (BMR) voor een fysieke server? <br/>
Ja.

### <a name="can-i-register-my-dpm-server-toomultiple-vaults-br"></a>Kan ik mijn DPM-Server toomultiple kluizen registreren? <br/>
Nee. Een server met DPM of MABS worden geregistreerde tooonly een kluis.

### <a name="which-version-of-system-center-data-protection-manager-is-supported-br"></a>Welke versie van System Center Data Protection Manager wordt ondersteund? <br/>
Het is raadzaam dat u Hallo installeert [nieuwste](http://aka.ms/azurebackup_agent) Azure backup-agent op Hallo nieuwste updatepakket (UR) voor System Center Data Protection Manager (DPM). Vanaf augustus 2016 is Update Rollup 11 Hallo meest recente update.

### <a name="i-have-installed-azure-backup-agent-tooprotect-my-files-and-folders-can-i-now-install-system-center-dpm-toowork-with-azure-backup-agent-tooprotect-on-premises-applicationvm-workloads-tooazure-br"></a>Ik heb de Azure Backup agent tooprotect geïnstalleerd deze bestanden en mappen. Kan ik System Center DPM toowork nu met Azure Backup agent tooprotect lokale toepassing/VM-workloads tooAzure installeren? <br/>
toouse Azure Backup met System Center Data Protection Manager (DPM), installeert u eerst DPM en installeer Azure backup-agent. Hello Azure Backup-onderdelen in deze volgorde installeren, zorgt u ervoor hello Azure backup-agent werkt met DPM. Installeren hello Azure backup-agent voordat u DPM installeert, wordt niet aangeraden of ondersteund.


## <a name="how-azure-backup-works"></a>De werking van Azure Backup
### <a name="if-i-cancel-a-backup-job-once-it-has-started-is-hello-transferred-backup-data-deleted-br"></a>Als ik een back-uptaak Annuleer nadat deze is gestart, hello overgedragen back-upgegevens verwijderd? <br/>
Nee. Alle gegevens die binnenkomen in Hallo kluis, voordat de back-uptaak Hallo is geannuleerd, blijft in Hallo kluis. Azure back-up maakt gebruik van een controlepunt mechanisme toooccasionally toevoegen controlepunten toohello back-upgegevens tijdens Hallo back-up. Omdat er controlepunten in de back-upgegevens hello, kunt de volgende back-upproces Hallo Hallo integriteit van Hallo bestanden valideren. de volgende back-uptaak Hallo worden incrementele toohello gegevens eerder een back-up. Incrementele back-ups draagt alleen nieuwe of gewijzigde gegevens, die gelijk toobetter gebruik van de bandbreedte is.

Als u een back-uptaak voor een virtuele Azure-machine annuleert, worden eventuele overgedragen gegevens geannuleerd. de volgende back-uptaak Hallo draagt een incrementele gegevens van Hallo laatste geslaagde back-uptaak.

### <a name="are-there-limits-on-when-or-how-many-times-a-backup-job-can-be-scheduledbr"></a>Gelden er limieten voor het moment waarop een back-uptaak kan worden gepland en voor het aantal keren?<br/>
Ja. U kunt back-uptaken op Windows Server of Windows-werkstations up toothree tijdstippen per dag uitvoeren. U kunt back-uptaken op System Center DPM up tootwice per dag uitvoeren. Voor IaaS VM's kunt u maximaal één keer per dat een back-uptaak uitvoeren. U kunt beleid voor de planning van Windows Server of Windows workstation toospecify Hallo dagelijks of wekelijks schema's. Als u System Center DPM gebruikt, kunt u een dag-, week-, maand- en jaarplanning maken.

### <a name="why-is-hello-size-of-hello-data-transferred-toohello-recovery-services-vault-smaller-than-hello-data-i-backed-upbr"></a>Waarom is Hallo grootte van Hallo overgedragen gegevens toohello die kleiner is dan Hallo gegevens die ik een back-up Recovery Services-kluis?<br/>
 Alle gegevens van Hallo die back-up van de Azure Backup Agent of SCDPM of Azure Backup-Server, wordt gecomprimeerd en versleuteld voordat ze worden overgedragen. Zodra Hallo compressie en codering wordt toegepast, is Hallo-gegevens in Hallo back-upkluis 30 tot 40% kleiner.

## <a name="what-can-i-back-up"></a>Waar kan ik een back-up van maken?
### <a name="which-operating-systems-do-azure-backup-support-br"></a>Welke besturingssystemen worden ondersteund door Azure Backup? <br/>
Azure Backup ondersteunt Hallo lijst met besturingssystemen voor back-up te volgen: bestanden en mappen en werkbelasting toepassingen die zijn beveiligd met Azure Backup-Server en System Center Data Protection Manager (DPM).

| Besturingssysteem | Platform | SKU |
|:--- | --- |:--- |
| Windows 8 en de meest recente SP's |64 bits |Enterprise, Pro |
| Windows 7 en de meest recente SP's |64 bits |Ultimate, Enterprise, Professional, Home Premium Home Basic, Starter |
| Windows 8.1 en de meest recente SP's |64 bits |Enterprise, Pro |
| Windows 10 |64 bits |Enterprise, Pro, Home |
| Windows Server 2016 |64 bits |Standard, Datacenter, Essentials |
| Windows Server 2012 R2 en de meest recente SP's |64 bits |Standard, Datacenter, Foundation |
| Windows Server 2012 en de meest recente SP's |64 bits |Datacenter, Foundation, Standard |
| Windows Storage Server 2016 en de meest recente SP's |64 bits |Standard, Workgroup | 
| Windows Storage Server 2012 R2 en de meest recente SP's |64 bits |Standard, Workgroup |
| Windows Storage Server 2012 en de meest recente SP's |64 bits |Standard, Workgroup |
| Windows Server 2012 R2 en de meest recente SP's |64 bits |Essential |
| Windows Server 2008 R2 SP1 |64 bits |Standard, Enterprise, Datacenter, Foundation |
| Windows Server 2008 SP2 |64 bits |Standard, Enterprise, Datacenter, Foundation |

**Back-up van virtuele Azure-machines:**

* **Linux**: Azure Backup ondersteunt [een lijst met distributies die zijn goedgekeurd door Azure](../virtual-machines/linux/endorsed-distros.md), met uitzondering van Core OS Linux.  Andere Bring-Your-eigenaar-Linux-distributies ook mogelijk werken zolang Hallo VM-agent beschikbaar op Hallo virtuele machine is en ondersteuning voor Python bestaat.
* **Windows Server**: versies ouder dan Windows Server 2008 R2 worden niet ondersteund.


### <a name="is-there-a-limit-on-hello-size-of-each-data-source-being-backed-up-br"></a>Is er een limiet op Hallo grootte van elke gegevensbron back-up wordt gemaakt? <br/>
Er is geen limiet voor Hallo en de hoeveelheid gegevens die u kunt back-ups tooa kluis. Azure Backup de maximale grootte voor de gegevensbron Hallo Hallo beperkt, echter deze limieten groot zijn. Vanaf augustus 2015 is de maximale grootte voor een gegevensbron voor de besturingssystemen ondersteund Hallo Hallo:

| S.Nee | Besturingssysteem | Maximale grootte van de gegevensbron |
|:---:|:--- |:--- |
| 1 |Windows Server 2012 of hoger |54.400 GB |
| 2 |Windows 8 of hoger |54.400 GB |
| 3 |Windows Server 2008, Windows Server 2008 R2 |1700 GB |
| 4 |Windows 7 |1700 GB |

Hallo volgende tabel wordt uitgelegd hoe de grootte van elke gegevensbron wordt bepaald.

| Gegevensbron | Details |
|:---:|:--- |
| Volume |Hallo en de hoeveelheid gegevens wordt een back-up van één volume van een server of client computer |
| Virtuele Hyper-V-machine  |De som van de gegevens van alle Hallo VHD's van Hallo virtuele machine back-up wordt gemaakt |
| Microsoft SQL Server-database |De grootte van één SQL-database waarvan een back-up wordt gemaakt. |
| Microsoft SharePoint |De som van Hallo inhoud en configuratiedatabases in een SharePoint-farm back-up wordt gemaakt |
| Microsoft Exchange |De som van alle Exchange-databases in een Exchange-server waarvan een back-up wordt gemaakt. |
| BMR/systeemstatus |Elke afzonderlijke kopie van de BMR of systeemstatus van Hallo machine back-up wordt gemaakt |

Voor back-up van virtuele machine in Azure, kan elke virtuele machine van gegevensschijven too16 hebben met elke schijf wordt van de grootte van 1023GB of minder. 

## <a name="retention-policy-and-recovery-points"></a>Retentiebeleid en herstelpunten
### <a name="is-there-a-difference-between-hello-retention-policy-for-dpm-and-windows-serverclient-that-is-on-windows-server-without-dpmbr"></a>Is er een verschil tussen het bewaarbeleid Hallo voor DPM en Windows Server /-client (dat wil zeggen op Windows Server zonder DPM)?<br/>
Nee, u kunt zowel voor DPM als voor Windows Server of de Windows-client een dagelijks, wekelijks, maandelijks en jaarlijks bewaarbeleid instellen.

### <a name="can-i-configure-my-retention-policies-selectively--ie-configure-weekly-and-daily-but-not-yearly-and-monthlybr"></a>Kan ik mijn bewaarbeleidsregels selectief configureren, oftewel wekelijks en dagelijks configureren, maar niet jaarlijks en maandelijks?<br/>
Ja, Hallo bewaarstructuur van Azure Backup beschikt u over toohave volledige flexibiliteit bij het definiëren van het bewaarbeleid Hallo volgens uw vereisten.

### <a name="can-i-schedule-a-backup-at-6pm-and-specify-retention-policies-at-a-different-timebr"></a>Kan ik 'een back-up plannen' om 18:00 uur en voor het retentiebeleid een ander tijdstip opgeven?<br/>
Nee. Het bewaarbeleid kan alleen worden toegepast op back-uppunten. In Hallo installatiekopie te volgen, is Hallo bewaarbeleid opgegeven voor back-ups die op 12 uur en 18: 00 uur. <br/>

![Back-up en retentie plannen](./media/backup-azure-backup-faq/Schedule.png)
<br/>

### <a name="if-a-backup-is-retained-for-a-long-duration-does-it-take-more-time-toorecover-an-older-data-point-br"></a>Als u een back-up langdurig wordt bewaard, duurt het meer tijd toorecover een oud gegevenspunt? <br/>
Nee, is tijd Hallo toorecover Hallo oudste of nieuwste punt Hallo Hallo dezelfde. Elk herstelpunt gedraagt zich als een volledig punt.

### <a name="if-each-recovery-point-is-like-a-full-point-does-it-impact-hello-total-billable-backup-storagebr"></a>Als elk herstelpunt een volledig punt is, heeft dit dan invloed Hallo totale factureerbare back-upopslag?<br/>
Producten met een lange bewaartermijn slaan de back-upgegevens doorgaans op als volledige punten. Hallo volledige punten maken opslag *inefficiënte* , maar zijn gemakkelijker en sneller toorestore. Incrementele kopieën maken opslag *efficiënte* maar vereisen dat u toorestore een keten van gegevens die van invloed is op de hersteltijd. Azure back-up opslag architectuur kunt u de beste van beide werelden Hallo door optimaal opslaan van gegevens voor snelle herstelbewerkingen en lage opslagkosten. Deze benadering van gegevensopslag zorgt ervoor dat uw bandbreedte voor inkomend en uitgaand verkeer efficiënt wordt gebruikt. Zowel Hallo tijdsduur gegevens opslag en Hallo toorecover Hallo gegevens nodig, tooa minimale wordt bewaard. Meer informatie over waarom het gebruik van [incrementele back-ups](https://azure.microsoft.com/blog/microsoft-azure-backup-save-on-long-term-storage/) efficiënt is.

### <a name="is-there-a-limit-on-hello-number-of-recovery-points-that-can-be-createdbr"></a>Is er een limiet op Hallo aantal herstelpunten dat kan worden gemaakt?<br/>
U kunt maken van herstelpunten too9999 per beveiligde exemplaar. Een beveiligde exemplaar is een computer, de server (fysiek of virtueel) of de werkbelasting geconfigureerd tooback up tooAzure gegevens. Zie voor meer informatie, Hallo uitleg van [back-up en retentie](./backup-introduction-to-azure-backup.md#backup-and-retention), en [wat is er een beveiligde exemplaar](./backup-introduction-to-azure-backup.md#what-is-a-protected-instance)?

### <a name="how-many-recoveries-can-i-perform-on-hello-data-that-is-backed-up-tooazurebr"></a>Hoeveel herstelbewerkingen kan ik uitvoeren voor Hallo-gegevens met back-up tooAzure?<br/>
Er is geen limiet voor het aantal herstelbewerkingen vanuit Azure Backup Hallo.

### <a name="when-restoring-data-do-i-pay-for-hello-egress-traffic-from-azure-br"></a>Bij het herstellen van gegevens, betaal ik voor Hallo uitgaande verkeer vanuit Azure? <br/>
Nee. Uw herstelbewerkingen zijn gratis en u niet weet in rekening gebracht voor Hallo uitgaande verkeer.

## <a name="azure-backup-encryption"></a>Azure Backup-versleuteling
### <a name="is-hello-data-sent-tooazure-encrypted-br"></a>Verzonden gegevens Hallo tooAzure versleuteld? <br/>
Ja. Gegevens worden versleuteld op Hallo lokale client-server/SCDPM-machine met AES256 en Hallo gegevens worden verzonden via een beveiligde HTTPS-koppeling.

### <a name="is-hello-backup-data-on-azure-encrypted-as-wellbr"></a>Is Hallo back-upgegevens op Azure ook versleuteld?<br/>
Ja. Hallo gegevens verzonden tooAzure blijven versleuteld (at rest). Back-upgegevens op elk gewenst moment Hallo wordt niet door Microsoft worden ontsleuteld. Wanneer een back-up van een virtuele machine in Azure, is Azure Backup is afhankelijk van de versleuteling van Hallo virtuele machine. Bijvoorbeeld, als uw VM is versleuteld met Azure Disk Encryption of een andere technologie voor versleuteling, Azure Backup gebruikt dat versleuteling toosecure uw gegevens.

### <a name="what-is-hello-minimum-length-of-encryption-key-used-tooencrypt-backup-data-br"></a>Wat is de minimale lengte Hallo van versleutelingssleutel gebruikt de back-upgegevens tooencrypt? <br/>
Hallo-versleutelingssleutel moet ten minste 16 tekens wanneer u van Azure backup-agent gebruikmaakt. Er is geen limiet toolength van sleutels die worden gebruikt door Azure KeyVault voor Azure VM's. 

### <a name="what-happens-if-i-misplace-hello-encryption-key-can-i-recover-hello-data-or-can-microsoft-recover-hello-data-br"></a>Wat gebeurt er als ik de versleutelingssleutel Hallo misplace? Kan ik Hallo-gegevens herstellen (of) kunt Microsoft hello gegevens herstellen? <br/>
Hallo sleutel gebruikte tooencrypt Hallo back-upgegevens bevindt zich alleen op Hallo klant beschikt. Microsoft bewaart geen kopie in Azure en heeft geen eventuele toohello toegangssleutel. Als de klant Hallo Hallo sleutel kwijtraakt, kan Microsoft hello back-upgegevens niet herstellen.
