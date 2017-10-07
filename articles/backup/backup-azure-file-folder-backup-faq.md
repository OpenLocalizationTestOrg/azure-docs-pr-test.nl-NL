---
title: aaaAzure backup-agent Veelgestelde vragen | Microsoft Docs
description: 'Toocommon vragen beantwoord over: hoe hello Azure backup-agent werkt, back-up en retentie limieten.'
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: back-up en herstel na noodgeval; Backup-service
ms.assetid: 778c6ccf-3e57-4103-a022-367cc60c411a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: bdefb4efb39301f38cdf692bdc93c841a2bbb441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-agent"></a>Vragen over hello Azure backup-agent
In dit artikel bevat antwoorden toocommon vragen toohelp u sneller inzicht in hello Azure Backup agent-onderdelen. In sommige Hallo-antwoorden zijn er koppelingen toohello artikelen waarvoor uitgebreide informatie. U kunt ook vragen over Azure Backup-service Hallo boeken in Hallo [discussieforum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="configure-backup"></a>Back-up configureren
### <a name="where-can-i-download-hello-latest-azure-backup-agent-br"></a>Waar kan ik Hallo meest recente Azure backup-agent downloaden? <br/>
U kunt Hallo meest recente agent downloaden voor back-ups van Windows Server, System Center DPM of Windows-clients van [hier](http://aka.ms/azurebackup_agent). Als u tooback een virtuele machine wilt, gebruikt u Hallo VM-Agent (die installeert automatisch het juiste toestelnummer Hallo). Hallo VM-Agent is al aanwezig op de virtuele machines die zijn gemaakt op basis van hello Azure-galerie.

### <a name="when-configuring-hello-azure-backup-agent-i-am-prompted-tooenter-hello-vault-credentials-do-vault-credentials-expire"></a>Ik ben vraag tooenter hello kluisreferenties bij het configureren van hello Azure backup-agent. Verlopen kluisreferenties?
Ja, Hallo kluisreferenties verlopen na 48 uur. Als het Hallo-bestand is verlopen, aanmelden toohello Azure portal en download Hallo kluisreferentiebestanden vanaf uw kluis.

### <a name="what-types-of-drives-can-i-back-up-files-and-folders-from-br"></a>Van welke typen stations kan ik back-ups van bestanden en mappen maken? <br/>
U back geen-up Hallo stations/volumes te volgen:

* Verwisselbare media: de bron van alle back-upitems moet worden gerapporteerd als vast.
* Alleen-lezen Volumes: Hallo volume moet schrijfbaar Hallo volume shadow copy service (VSS) toofunction.
* Offlinevolumes: Hallo volume moet voor VSS toofunction online zijn.
* Netwerkshare: Hallo volume moet lokale toohello server toobe back-ups met online back-up.
* Met BitLocker beveiligde volumes: Hallo volume moet worden ontgrendeld voordat Hallo back-up kan plaatsvinden.
* Bestandsysteemidentificatie: NTFS is Hallo enige bestandssysteem ondersteund.

### <a name="what-file-and-folder-types-can-i-back-up-from-my-serverbr"></a>Van welke typen bestanden en mappen op mijn server kan ik een back-up maken?<br/>
Hallo volgende typen worden ondersteund:

* Versleuteld
* Gecomprimeerd
* Sparse
* Gecomprimeerd + Sparse
* Vaste koppelingen: niet ondersteund, worden overgeslagen
* Reparsepunt: niet ondersteund, wordt overgeslagen
* Versleuteld + sparse: niet ondersteund, wordt overgeslagen
* Gecomprimeerde stream: niet ondersteund, wordt overgeslagen
* Sparse stream: niet ondersteund, wordt overgeslagen

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-already-backed-by-hello-azure-backup-service-using-hello-vm-extension-br"></a>Kan ik hello Azure backup-agent installeren op een Azure-virtuele machine al is gemaakt door hello Azure Backup-service met behulp van Hallo VM-extensie? <br/>
Absoluut. Azure Backup biedt back-up van VM-niveau voor virtuele Azure-machines met behulp van Hallo VM-extensie. tooprotect bestanden en mappen op Hallo gastbesturingssysteem Windows, moet u hello Azure backup-agent installeren op Hallo gastbesturingssysteem van Windows.

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-tooback-up-files-and-folders-present-on-temporary-storage-provided-by-hello-azure-vm-br"></a>Kan ik hello Azure backup-agent installeren op een virtuele machine van Azure tooback van bestanden en mappen aanwezig zijn op de tijdelijke opslag van hello Azure VM? <br/>
Ja. Hello Azure backup-agent installeren op Hallo gastbesturingssysteem van Windows en back-up van bestanden en mappen tootemporary opslag. Houd er rekening mee dat back-ups mislukken als de tijdelijke opslaggegevens worden gewist. Als de tijdelijke opslaggegevens Hallo is verwijderd, kunt u ook alleen toonon-vluchtige opslag herstellen.

### <a name="whats-hello-minimum-size-requirement-for-hello-cache-folder-br"></a>Wat is Hallo minimaal vereiste grootte voor de cachemap Hallo? <br/>
Hallo-grootte van de cachemap Hallo bepaalt Hallo hoeveelheid gegevens die u een back-up. Uw cachemap moet 5% van Hallo vereiste ruimte voor de opslag van gegevens.

### <a name="how-do-i-register-my-server-tooanother-datacenterbr"></a>Hoe kan ik mijn server tooanother datacenter registreren?<br/>
Back-upgegevens verzonden toohello datacenter van Hallo kluis toowhich die is geregistreerd. Hallo gemakkelijkste manier toochange Hallo datacenter toouninstall Hallo-agent en Hallo-agent opnieuw installeren en registreren tooa nieuwe kluis die deel uitmaakt van toodesired datacenter.

### <a name="does-hello-azure-backup-agent-work-on-a-server-that-uses-windows-server-2012-deduplication-br"></a>Ondersteunt hello Azure Backup agent werkt op een server die gebruikmaakt van Windows Server 2012-gegevensontdubbeling? <br/>
Ja. Hallo-agentservice converteert Hallo ontdubbelde gegevens toonormal gegevens wanneer het Hallo-back-upbewerking wordt voorbereid. Deze vervolgens optimaliseert de gegevens voor back-up hello, Hallo gegevens worden gecodeerd en stuurt vervolgens Hallo versleutelde gegevens toohello online Backup-service.

## <a name="backup"></a>Back-up
### <a name="how-do-i-change-hello-cache-location-specified-for-hello-azure-backup-agentbr"></a>Hoe kan ik de cachelocatie Hallo opgegeven voor hello Azure backup-agent wijzigen?<br/>
Gebruik hello lijst toochange Hallo cachelocatie te volgen.

1. Hallo Backup-engine door het uitvoeren van de volgende opdracht in een verhoogde opdrachtprompt Hallo stoppen:

    ```PS C:\> Net stop obengine``` 
  
2. Hallo-bestanden niet verplaatsen. Kopieer in plaats daarvan Hallo cache ruimte map tooa ander station met voldoende ruimte. Hallo oorspronkelijke cacheruimte kan worden verwijderd nadat is bevestigd Hallo back-ups met de nieuwe cacheruimte Hallo werkt.
3. Update hello registervermeldingen met Hallo pad toohello nieuwe ruimte cachemap te volgen.<br/>

    | Registerpad | Registersleutel | Waarde |
    | --- | --- | --- |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config` |ScratchLocation |*Nieuwe locatie van de cachemap* |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider` |ScratchLocation |*Nieuwe locatie van de cachemap* |

4. Hallo Backup-engine opnieuw door het uitvoeren van de volgende opdracht in een verhoogde opdrachtprompt Hallo:

    ```PS C:\> Net start obengine```

Zodra de back-up maken van Hallo in Hallo nieuwe cachelocatie is voltooid, kunt u Hallo oorspronkelijke cachemap verwijderen.


### <a name="where-can-i-put-hello-cache-folder-for-hello-azure-backup-agent-toowork-as-expectedbr"></a>Waar kan ik de cachemap Hallo voor hello Azure Backup Agent toowork zoals verwacht plaatsen?<br/>
Hallo volgende locaties voor de cachemap Hallo niet aanbevolen:

* Netwerkshare of verwisselbare Media: Hallo cachemap moet lokale toohello-server waarvoor u een back-up met online back-up. Netwerklocaties of verwisselbare media zoals USB-stations worden niet ondersteund.
* Offlinevolumes: de Hallo cachemap moet online zijn voor de verwacht back-up met behulp van Azure Backup Agent.

### <a name="are-there-any-attributes-of-hello-cache-folder-that-are-not-supportedbr"></a>Zijn er kenmerken van Hallo cachemap die niet worden ondersteund?<br/>
Hallo worden volgende kenmerken of combinaties daarvan niet ondersteund voor de cachemap Hallo:

* Versleuteld
* Ontdubbeld
* Gecomprimeerd
* Sparse
* Reparsepunt

Hallo cachemap en Hallo metagegevens VHD hoeft geen Hallo vereiste kenmerken voor hello Azure backup-agent.

### <a name="is-there-a-way-tooadjust-hello-amount-of-bandwidth-used-by-hello-backup-servicebr"></a>Is er een manier tooadjust Hallo hoeveelheid bandbreedte die wordt gebruikt door Hallo Backup-service?<br/>
  Ja, gebruiken Hallo **eigenschappen wijzigen** optie in Hallo Backup-Agent tooadjust bandbreedte. Hallo hoeveelheid bandbreedte en Hallo keer wanneer u dat er bandbreedte gebruikt, kunt u aanpassen. Zie **[Enable network throttling](backup-configure-vault.md#enable-network-throttling)** (Netwerkbeperking inschakelen) voor stapsgewijze instructies.

## <a name="manage-backups"></a>Back-ups beheren
### <a name="what-happens-if-i-rename-a-windows-server-that-is-backing-up-data-tooazurebr"></a>Wat gebeurt er als ik de naam van een Windows-server die back-ups van gegevens tooAzure?<br/>
Wanneer u de naam van een server wijzigt, worden alle back-ups die momenteel zijn geconfigureerd, gestopt.
Nieuwe naam van de Hallo van Hallo-server registreren met Hallo Backup-kluis. Wanneer u de nieuwe naam Hallo met Hallo kluis registreert, Hallo eerste back-upbewerking is een *volledige* back-up. Als u toorecover gegevensback-ups toohello kluis met de oude servernaam hello moet, gebruikt u Hallo [ **een andere server** ](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) optie in Hallo **gegevens herstellen** wizard.

### <a name="what-is-hello-maximum-file-path-length-that-can-be-specified-in-backup-policy-using-azure-backup-agent-br"></a>Wat is Hallo maximale padlengte die kan worden opgegeven in de Backup-beleid met Azure backup-agent? <br/>
De Azure Backup-agent is afhankelijk van NTFS. Hallo [engtespecificatie wordt beperkt door de API voor Windows hello](https://msdn.microsoft.com/library/aa365247.aspx#fully_qualified_vs._relative_paths). Hallo-bestanden die u wilt dat tooprotect hebt een bestandspad lengte langer is dan is toegestaan door de API voor Windows hello, back-up Hallo bovenliggende map of Hallo-schijf.  

### <a name="what-characters-are-allowed-in-file-path-of-azure-backup-policy-using-azure-backup-agent-br"></a>Welke tekens zijn toegestaan in het bestandspad van het Azure Backup-beleid met Azure Backup-agent? <br>
 De Azure Backup-agent is afhankelijk van NTFS. Er worden [NTFS-ondersteunde tekens](https://msdn.microsoft.com/library/aa365247.aspx#naming_conventions) ingeschakeld als onderdeel van de bestandsspecificatie. 
 
### <a name="i-receive-hello-warning-azure-backups-have-not-been-configured-for-this-server-even-though-i-configured-a-backup-policy-br"></a>Zelfs als ik een back-upbeleid hebt geconfigureerd, ontvangen Hallo waarschuwing, 'Azure back-ups zijn niet geconfigureerd voor deze server' <br/>
Deze waarschuwing treedt op wanneer er zijn geen Hallo back-upschema instellingen opgeslagen op de lokale server Hallo Hallo gelijk zijn aan instellingen die zijn opgeslagen in de back-upkluis Hallo Hallo. Wanneer het Hallo-server of Hallo-instellingen zijn herstelde tooa bekende goede staat verkeren, hebben Hallo back-upschema niet meer gesynchroniseerd. Als u deze waarschuwing ontvangt [opnieuw configureren van de back-upbeleid Hallo](backup-azure-manage-windows-server.md) en vervolgens **uitvoeren Back-Up uit** tooresynchronize Hallo lokale server met Azure.
