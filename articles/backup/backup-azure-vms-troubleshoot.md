---
title: back-fouten met de virtuele machine van Azure aaaTroubleshoot | Microsoft Docs
description: Back-up en herstel van virtuele machines in Azure oplossen
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 73214212-57a4-4b57-a2e2-eaf9d7fde67f
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: trinadhk;markgal;jpallavi;
ms.openlocfilehash: 9224c47e02b52688adcba5876c674c88502557c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-virtual-machine-backup"></a>Problemen oplossen met back-ups van virtuele Azure-machines
> [!div class="op_single_selector"]
> * [Recovery services-kluis](backup-azure-vms-troubleshoot.md)
> * [Back-upkluis](backup-azure-vms-troubleshoot-classic.md)
>
>

U kunt er zijn fouten opgetreden tijdens het gebruik van Azure Backup met informatie in onderstaande tabel voor Hallo oplossen.

## <a name="backup"></a>Back-up
| Details van fouten | Tijdelijke oplossing |
| --- | --- |
| Kan de Hallo-bewerking niet uitvoeren omdat de virtuele machine niet meer bestaat. -Stop de beveiliging van virtuele machine zonder back-upgegevens te verwijderen. Meer informatie op http://go.microsoft.com/fwlink/?LinkId=808124 |Dit gebeurt wanneer hello primaire virtuele machine wordt verwijderd, maar de back-upbeleid Hallo blijft opzoeken voor een VM-tooback. toofix deze fout: <ol><li> Hallo virtuele machine met de Hallo opnieuw dezelfde naam en hetzelfde Resourcegroepnaam [cloudservicenaam]<br>(OR)</li><li> Stop de beveiliging van virtuele machine met of zonder Hallo back-upgegevens te verwijderen. [Meer informatie](http://go.microsoft.com/fwlink/?LinkId=808124)</li></ol> |
| Momentopname-bewerking is mislukt vanwege de netwerkverbinding toono op Hallo virtuele machine - Zorg ervoor dat virtuele machine toegang tot het netwerk. Voor de momentopname toosucceed, ofwel geaccepteerde Azure datacenter IP-adresbereiken of instellen van een proxyserver voor toegang tot het netwerk. Voor meer informatie raadpleegt u te http://go.microsoft.com/fwlink/?LinkId=800034. Als u al proxyserver gebruikt, zorg ervoor dat de instellingen van proxyserver correct zijn geconfigureerd | Deze fout wordt gegenereerd wanneer u Hallo uitgaande internetverbinding op Hallo virtuele machine weigeren. Verbinding met Internet is vereist voor VM-momentopname extensie tootake een momentopname van de onderliggende schijven van Hallo virtuele machine. [Meer informatie](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#snapshot-operation-failed-due-to-no-network-connectivity-on-the-virtual-machine) op hoe toofix-fouten vanwege tooblocked toegang tot het netwerk Snapshot. |
| VM-agent is kan geen toocommunicate Hello Azure Backup-Service. -Zorg ervoor dat Hallo VM heeft verbinding met het netwerk en Hallo VM-agent is de meest recente en wordt uitgevoerd. Voor meer informatie raadpleegt u te http://go.microsoft.com/fwlink/?LinkId=800034 |Deze fout wordt gegenereerd als er een probleem met de Hallo VM-Agent of netwerk toegang toohello Azure-infrastructuur is geblokkeerd op een bepaalde manier. [Meer informatie](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#vm-agent-unable-to-communicate-with-azure-backup) over foutopsporing van de virtuele machine een momentopname van problemen.<br> Als Hallo VM-agent is niet wordt veroorzaakt door problemen, start u Hallo VM. Een onjuiste status voor de virtuele machine kan soms problemen veroorzaken en opnieuw te starten Hallo VM herstelt u de deze 'slechte 'staat. |
| De VM bevindt zich in een mislukte inrichten status - Hallo VM Start en zorg ervoor dat Hallo die virtuele machine uitgevoerd of afsluiten van de status voor back-up wordt | Dit gebeurt wanneer een van de Hallo extensie fouten VM status toobe in mislukte Inrichtingsstatus leidt. Ga tooextensions lijst en zien of er een mislukte extensie Verwijder deze en probeer het Hallo virtuele machine opnieuw te starten. Als alle uitbreidingen zijn uitgevoerd, controleert u of de VM-agent-service wordt uitgevoerd. Als dat niet het geval is, Hallo VM-agent-service opnieuw starten. | 
| VMSnapshot-uitbreiding is mislukt voor beheerde schijven - Neem Hallo back-up opnieuw. Als Hallo probleem zich weer voordoet, voert u de instructies op 'http://go.microsoft.com/fwlink/?LinkId=800034' Hallo. Als dat niet meer werkt, neem contact op met Microsoft ondersteuning | Deze fout als een momentopname tootrigger Azure Backup-service is mislukt. [Meer informatie](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#vmsnapshot-extension-operation-failed) over foutopsporing van de virtuele machine een momentopname van problemen. |
| Kan niet kopiëren Hallo momentopname van Hallo virtuele machine vanwege tooinsufficient vrije ruimte in het opslagaccount Hallo - Zorg ervoor dat opslagaccount vrije ruimte gelijkwaardige heeft toohello gegevens op Hallo premium opslagschijven toohello virtuele machine gekoppeld | In geval van een VM's voor premium kopieert u Hallo momentopname toostorage account. Dit is toomake ervoor dat back-beheer van verkeer, die op momentopname werkt, Hallo aantal IOPS beschikbaar toohello toepassing met premium-schijven niet beperkt. Microsoft raadt dat u slechts 50% van de totale opslagruimte account Hallo toewijzen zodat hello Azure Backup-service Hallo toostorage account en overdracht momentopnamegegevens vanaf deze locatie gekopieerd in storage account toohello kluis kopiëren kunt. | 
| Kan geen tooperform Hallo bewerking als Hallo VM-agent is niet reageren |Deze fout wordt gegenereerd als er een probleem met de Hallo VM-Agent of netwerk toegang toohello Azure-infrastructuur is geblokkeerd op een bepaalde manier. Controleer voor VM's van Windows hello VM-agent-servicestatus op services en of Hallo-agent wordt weergegeven in het Configuratiescherm. Probeer verwijderen Hallo programma Configuratiescherm en opnieuw te installeren Hallo agent voor beheer op zoals vermeld [hieronder](#vm-agent). Activeert een ad-hoc back-tooverify na het Hallo-agent opnieuw te installeren. |
| Recovery services-uitbreiding is mislukt. -Zorg dat de meest recente agent van de virtuele machine aanwezig op Hallo virtuele machine is en agent-service wordt uitgevoerd. Probeer de back-upbewerking en als het mislukt, neem dan contact op met Microsoft ondersteuning. |Deze fout wordt gegenereerd wanneer de VM-agent is verouderd. Raadpleeg de sectie 'Updating Hallo VM-Agent' hieronder tooupdate Hallo VM-agent. |
| Virtuele machine bestaat niet. -Geef Zorg ervoor dat de virtuele machine bestaat, of Selecteer een andere virtuele machine. |Dit gebeurt wanneer hello primaire virtuele machine is verwijderd, maar Hallo back-upbeleid toolook voor een VM-tooperform back-up blijft. toofix deze fout: <ol><li> Hallo virtuele machine met de Hallo opnieuw dezelfde naam en hetzelfde Resourcegroepnaam [cloudservicenaam]<br>(OR)<br></li><li>Stop de beveiliging van Hallo virtuele machine zonder Hallo back-upgegevens te verwijderen. [Meer informatie](http://go.microsoft.com/fwlink/?LinkId=808124)</li></ol> |
| Opdrachtuitvoering is mislukt. -Een andere bewerking wordt momenteel uitgevoerd voor dit item. Wacht totdat de vorige bewerking Hallo is voltooid en probeer het vervolgens opnieuw |Een bestaande back-up op Hallo VM wordt uitgevoerd en een nieuwe taak kan niet worden gestart terwijl bestaande Hallo-taak wordt uitgevoerd. |
| Kopiëren van virtuele harde schijven vanuit de back-upkluis Hallo time-out - probeer de bewerking Hallo over een paar minuten opnieuw. Als Hallo probleem zich blijft voordoen, neem contact op met Microsoft Support. | Dit gebeurt als er een tijdelijke fout aan de opslag, of als Backup-service is niet voldoende IOP's uit die als host fungeert voor Hallo VM in volgorde tootransfer gegevens binnen de periode toovault time-out storage-account. Zorg ervoor dat u hebt gevolgd [Best practices](backup-azure-vms-introduction.md#best-practices) tijdens het instellen van back-up. Verplaats virtuele machine tooa verschillende storage-account niet is geladen en probeer opnieuw de back-up.|
| Back-up is mislukt met een interne fout: Voer de bewerking Hallo over een paar minuten opnieuw uit. Als Hallo probleem zich blijft voordoen, neem dan contact op met Microsoft Support |U kunt deze fout krijgen omwille van 2: <ol><li> Er is een tijdelijk probleem bij het openen van Hallo VM-opslag. Controleer of [Azure Status](https://azure.microsoft.com/en-us/status/) toosee als er een probleem continu gerelateerde toocompute-, opslag- of netwerken in Hallo regio. Probeer Hallo back-uptaak zodra Hallo probleem is opgelost. <li>Hallo oorspronkelijke VM is verwijderd en daarom Hallo herstelpunt kan niet worden uitgevoerd. tookeep hello back-upgegevens voor een verwijderde virtuele machine, maar verwijder Hallo back-fouten: beveiliging opheffen Hallo VM en Hallo optie tookeep Hallo gegevens te selecteren. Deze actie stopt geplande back-uptaak Hallo Hallo terugkerende foutberichten worden weergegeven. |
| Tooinstall hello Azure Recovery Services-extensie op Hallo geselecteerd item is mislukt - hello VM-agent is een vereiste voor hello Azure Recovery Services-extensie. Hello Azure VM-agent installeren en start Hallo registratie bewerking opnieuw |<ol> <li>Controleer of de Hallo VM-agent correct is geïnstalleerd. <li>Zorg ervoor dat de vlag Hallo op Hallo VM-configuratie correct is ingesteld.</ol> [Lees meer](#validating-vm-agent-installation) Hallo VM-agent en hoe toovalidate Hallo voor de installatie van de VM-agent installeren. |
| Installatie van de uitbreiding is mislukt met fout Hallo 'COM + is tootalk toohello Microsoft Distributed Transaction Coordinator |Dit betekent meestal dat Hallo COM +-service niet wordt uitgevoerd. Neem contact op met Microsoft ondersteuning voor hulp bij het oplossen van dit probleem. |
| Momentopname-bewerking is mislukt met de Hallo VSS-fout voor bewerking 'dit station is vergrendeld door BitLocker-stationsversleuteling. U moet deze schijf van het Configuratiescherm Hallo ontgrendelen. |BitLocker uitschakelen voor alle stations op Hallo virtuele machine en bekijk of Hallo VSS probleem is opgelost |
| Virtuele machine zich niet in een status waarin de back-ups. |<ul><li>Controleer of VM een tijdelijke status tussen die wordt uitgevoerd en computer afsluiten omlaag is. Als het, wacht Hallo VM status toobe één hiervan en activeren back-up opnieuw. <li> Als Hallo VM een Linux-VM en kernel-module [Security Enhanced Linux] gebruikt is, moet u tooexclude Hallo pad van de Linux-Agent (_/var/lib/waagent_) van de beveiliging ervoor dat de back-extensie voor toomake wordt geïnstalleerd.  |
| Azure virtuele Machine is niet gevonden. |Dit gebeurt wanneer hello primaire virtuele machine is verwijderd, maar de back-upbeleid Hallo toolook voor een VM-tooperform back-up blijft. toofix deze fout: <ol><li>Hallo virtuele machine met de Hallo opnieuw dezelfde naam en hetzelfde Resourcegroepnaam [cloudservicenaam] <br>(OR) <li> Schakel de beveiliging voor deze virtuele machine zodat de back-uptaken Hallo wordt niet gemaakt. </ol> |
| Agent van de virtuele machine is niet aanwezig op Hallo virtuele machine - Installeer eventuele vereiste en Hallo VM-agent en Hallo bewerking vervolgens opnieuw te starten. |[Lees meer](#vm-agent) over de installatie van de VM-agent en hoe toovalidate Hallo voor de installatie van de VM-agent. |
| Momentopname-bewerking is mislukt vanwege tooVSS-schrijvers in orde |U moet toorestart VSS (Volume Shadow copy Service)-schrijvers in orde. tooachieve, vanaf een opdrachtprompt met verhoogde bevoegdheden uitvoeren _vssadmin lijst schrijvers_. Uitvoer bevat alle VSS-schrijvers en hun status. Voor elke VSS-schrijver waarvan de status is niet '[1] stabiel' opnieuw starten VSS-schrijver met opdrachten na vanaf een opdrachtprompt met verhoogde bevoegdheid:<br> _net stop serviceName_ <br> _net start serviceName_|
| Momentopname-bewerking is mislukt vanwege tooa parseren fout van Hallo-configuratie |Dit gebeurt vanwege toochanged machtigingen op Hallo MachineKeys directory: _%systemdrive%\programdata\microsoft\crypto\rsa\machinekeys_ <br>Voer onderstaande opdracht en Ga na of machtigingen voor map MachineKeys standaard waarden:<br>_icacls %systemdrive%\programdata\microsoft\crypto\rsa\machinekeys_ <br><br> Standaardmachtigingen zijn:<br>Everyone:(R,W) <br>BUILTIN\Administrators:(F)<br><br>Als u machtigingen op MachineKeys directory is anders dan standaard ziet, verwijder Volg onderstaande stappen toocorrect machtigingen, Hallo-certificaat en Hallo back-up te activeren.<ol><li>Los machtigingen op de map MachineKeys op.<br>Explorer beveiligingseigenschappen en geavanceerde beveiligingsinstellingen op Hallo directory gebruikt, opnieuw instellen van machtigingen back-toohello standaardwaarden, verwijdert u eventuele extra (dan standaard) gebruikersobject uit Hallo directory en zorg ervoor dat Hallo 'Iedereen' machtigingen had speciale toegang voor:<br>-Map weergeven / gegevens lezen <br>-Kenmerken lezen <br>-Uitgebreide kenmerken lezen <br>-Bestanden maken / gegevens schrijven <br>-Mappen maken / gegevens toevoegen<br>-Kenmerken schrijven<br>-Uitgebreide kenmerken schrijven<br>-De machtiging lezen<br><br><li>Verwijder alle certificaten die met veld 'Verleend aan' = 'Azure Service Management voor uitbreidingen voor Windows' of 'Windows Azure CRP certificaat Generator'.<ul><li>[Open de console van certificaten (lokale computer)](https://msdn.microsoft.com/library/ms788967(v=vs.110).aspx)<li>Alle certificaten verwijderen (-> certificaten onder Personal) met veld 'Verleend aan' = 'Azure Service Management voor uitbreidingen voor Windows' of 'Windows Azure CRP certificaat Generator'.</ul><li>Trigger VM back-up. </ol>|
| Validatie is mislukt, omdat virtuele machine is versleuteld met BEK alleen. Back-ups kunnen alleen worden ingeschakeld voor virtuele machines die zijn versleuteld met BEK en KEK-sleutel. |Virtuele machine moeten worden versleuteld met BitLocker-versleutelingssleutel en coderingssleutel Key. Daarna wordt de back-up moet worden ingeschakeld. |
| Azure Backup-Service heeft geen voldoende machtigingen tooKey kluis voor back-up van versleuteld virtuele Machines. |Backup-service moet worden opgegeven deze machtigingen in PowerShell met stappen die worden vermeld in **back-up inschakelen** sectie van [PowerShell documentatie](backup-azure-vms-automation.md). |
|Installatie van een momentopname van extensie is mislukt met fout - de COM + is tootalk toohello Microsoft Distributed Transaction Coordinator | Neem probeer toostart windows service 'COM + System Application' (vanaf een opdrachtprompt met verhoogde bevoegdheid - _net start COMSysApp_). <br>Als het mislukt tijdens het starten, volgt u onderstaande stappen te volgen:<ol><li> Valideren dat de aanmeldingsaccount Hallo van service 'Distributed Transaction Coordinator' 'Netwerkservice'. Wijzig het als dit niet het geval is, te 'Netwerkservice', start deze service opnieuw en probeer het toostart service 'COM + System Application'.'<li>Als het toostart nog steeds mislukt, verwijderen/installeren service 'Distributed Transaction Coordinator' aan de hand van onderstaande stappen te volgen:<br> -Hallo MSDTC-service stoppen<br> -Open een opdrachtprompt (cmd) <br> -Voer de opdracht ' msdtc-verwijderen " <br> -Voer de opdracht ' msdtc-installeren " <br> -Hallo MSDTC-service starten<li>'COM + System Application' van de windows-service starten en nadat deze is gestart, activeert u back-up van de portal.</ol> |
|  Momentopname-bewerking is mislukt vanwege tooCOM +-fout | Hallo aanbevolen actie is toorestart windows-service 'COM + System Application' (vanaf een opdrachtprompt met verhoogde bevoegdheid - _net start COMSysApp_). Als Hallo probleem zich blijft voordoen, start opnieuw op Hallo VM. Als Hallo VM help niet opnieuw is opgestart, probeert u [VMSnapshot extensie verwijderen Hallo](https://docs.microsoft.com/en-us/azure/backup/backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout#cause-3-the-backup-extension-fails-to-update-or-load) en om back-up Hallo handmatig te activeren. |
| Kan toofreeze een of meer koppelpunten van Hallo VM tootake een consistente momentopname bestandssysteem | Gebruik Hallo stappen te volgen: <ol><li>Controleer de status van het bestandssysteem Hallo van alle gekoppelde apparaten met behulp van _'tune2fs'_ opdracht.<br> Bijvoorbeeld: tune2fs -l/dev/sdb1 \| GREP 'Bestandssysteem status' <li>Hallo-apparaten voor welke bestandssysteem status niet met behulp van schone is ontkoppelen _'umount'_ opdracht <li> Voer FileSystemConsistency uit op deze apparaten met behulp van _'fsck'_ opdracht <li> Hallo-apparaten opnieuw koppelen en probeer het back-up.</ol> |
| De bewerking is mislukt vanwege een momentopname toofailure bij het maken van het communicatiekanaal beveiligd netwerk | <ol><Li> Open de Register-Editor door te voeren regedit.exe in een modus met uitgebreide bevoegdheden. <li> Alle versies van identificeren. NetFramework aanwezig is in het systeem. Ze zijn aanwezig op de hiërarchie van registersleutel 'HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft' Hallo <li> Voor elk. NetFramework aanwezig is in de registersleutel, plaats de volgende sleutel: <br> "SchUseStrongCrypto" = dword: 00000001 </ol>|
| De bewerking is mislukt vanwege een momentopname toofailure in de installatie van Visual C++ Redistributable voor Visual Studio 2012 | Navigeer tooC:\Packages\Plugins\Microsoft.Azure.RecoveryServices.VMSnapshot\agentVersion en vcredist2012_x64 installeren. Zorg ervoor dat registersleutelwaarde voor het toestaan van de installatie van deze service toocorrect waarde, dat wil zeggen de waarde van registersleutel is ingesteld _HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Msiserver_ too3 en niet 4 is ingesteld. Als u problemen met de installatie nog steeds worden geconfronteerd, start u de installatieservice opnieuw door te voeren _MSIEXEC/UNREGISTER_ gevolgd door _MSIEXEC /REGISTER_ vanaf een opdrachtprompt met verhoogde bevoegdheid.  |


## <a name="jobs"></a>Taken
| Details van fouten | Tijdelijke oplossing |
| --- | --- |
| Annulering wordt niet ondersteund voor dit taaktype: wacht totdat het Hallo-taak is voltooid. |Geen |
| Hallo-taak is niet in een status Annuleerbare - wacht totdat het Hallo-taak is voltooid. <br>OF<br> Hallo geselecteerde taak is niet in een status Annuleerbare - Hallo taak toocomplete een ogenblik geduld. |Hallo-taak is naar alle waarschijnlijkheid bijna voltooid. Wacht totdat het Hallo-taak is voltooid.|
| Kan het Hallo-taak niet annuleren omdat deze niet uitgevoerd is-deze annulering wordt alleen ondersteund voor taken die uitgevoerd worden. Annuleer van poging op een onderhanden taak. |Dit gebeurt vanwege tooa tijdelijke status. Wacht een paar minuten en probeer Hallo annuleren opnieuw. |
| Mislukte toocancel Hallo functie - wacht totdat de taak is voltooid. |Geen |

## <a name="restore"></a>Herstellen
| Details van fouten | Tijdelijke oplossing |
| --- | --- |
| Terugzetten is mislukt vanwege een interne Cloud fout |<ol><li>Cloud service toowhich u toorestore probeert is geconfigureerd met DNS-instellingen. U kunt controleren <br>$deployment = get-AzureDeployment - ServiceName "ServiceName"-sleuf 'Productie' Get-AzureDns - DnsSettings $deployment. DnsSettings<br>Als er is een adres dat is geconfigureerd, betekent dit dat de DNS-instellingen zijn geconfigureerd.<br> <li>Cloud service toowhich tooyou probeert toorestore is geconfigureerd met ReservedIP en bestaande virtuele machines in de cloudservice wordt gestopt.<br>U kunt controleren dat een cloudservice is gereserveerde IP-adres via de volgende powershell-cmdlets:<br>$deployment = get-AzureDeployment - ServiceName "servicename"-sleuf 'Productie' $dep. ReservedIPName <br><li>U probeert een virtuele machine met de volgende speciale netwerkconfiguraties in toosame cloudservice toorestore. <br>-Virtuele machines onder load balancer-configuratie (intern en extern)<br>-Virtuele machines met meerdere gereserveerde IP 's<br>-Virtuele machines met meerdere NIC 's<br>Selecteer een nieuwe cloudservice in Hallo UI of Raadpleeg het te[terugzetten overwegingen](backup-azure-arm-restore-vms.md#restoring-vms-with-special-network-configurations) voor virtuele machines met speciale netwerkconfiguraties.</ol> |
| Hallo geselecteerd DNS-naam is al in gebruik: Geef een andere DNS-naam en probeer het opnieuw. |Hallo DNS-naam hier verwijst toohello cloudservicenaam (meestal eindigend. cloudapp.net). Dit moet toobe uniek zijn. Als deze fout optreedt, moet u toochoose een andere naam voor de virtuele machine tijdens het terugzetten. <br><br> Deze fout wordt alleen toousers Hallo Azure-portal weergegeven. Hallo slaagt herstelbewerking via PowerShell omdat deze alleen worden hersteld Hallo schijven en Hallo VM niet maken. Hallo fout zal worden geconfronteerd wanneer Hallo VM na Hallo schijf terugzetten expliciet door u is gemaakt. |
| Hallo opgegeven virtuele netwerkconfiguratie is niet correct: Geef een ander virtueel netwerk-configuratie en probeer het opnieuw. |Geen |
| Hallo opgegeven service in de cloud met behulp van een gereserveerd IP-adres die komt niet overeen met het Hallo-configuratie van Hallo virtuele machine wordt hersteld - Geef een andere cloudservice, die niet van gereserveerde IP-adres gebruikmaakt, of kies een ander herstelpunt punt toorestore uit. |Geen |
| Cloudservice heeft de limiet voor aantal eindpunten voor invoer - opnieuw Hallo uitvoeren door te geven van een andere cloudservice of met behulp van een bestaand eindpunt bereikt. |Geen |
| Back-kluis en doel storage-account zijn in twee verschillende regio's: Zorg ervoor dat Hallo storage-account opgegeven in de herstelbewerking Hallo dezelfde Azure-regio als Hallo back-upkluis. |Geen |
| Storage-Account opgegeven voor Hallo restore-bewerking niet is ondersteund - alleen Basic/Standard storage-accounts met lokaal redundante of geografisch redundante replicatie-instellingen worden ondersteund. Selecteer een ondersteunde storage-account |Geen |
| Type Opslagaccount dat is opgegeven voor de herstelbewerking is niet online - Zorg ervoor dat de Hallo storage-account opgegeven in restore-bewerking online is |Dit kan gebeuren vanwege een tijdelijke fout in Azure Storage of vervaldatum tooan storing. Kies een ander opslagaccount. |
| Resourcegroep quotum is bereikt - Verwijder een aantal resourcegroepen vanuit Azure-portal of neem contact op met de ondersteuning van Azure tooincrease Hallo limieten. |Geen |
| Geselecteerde subnet bestaat niet: Selecteer een subnet dat bestaat |Geen |
| Backup-Service heeft geen autorisatie tooaccess resources in uw abonnement. |tooresolve deze, eerste schijven herstellen met behulp van de stappen die worden vermeld in de sectie **terugzetten een back-up schijven** in [kiezen VM restore-configuratie](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Daarna Gebruik PowerShell-stappen die worden vermeld [een virtuele machine maken van herstelde schijven](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate volledige VM van herstelde schijven. |

## <a name="backup-or-restore-taking-time"></a>Backup of Restore duurt
Als u uw backup(>12 hours) of terugzetten duurt time(>6 hours):
* Begrijpen [factoren die bijdragen toobackup tijd](backup-azure-vms-introduction.md#total-vm-backup-time) en [factoren die bijdragen toorestore tijd](backup-azure-vms-introduction.md#total-restore-time).
* Zorg ervoor dat u volgt [back-up van best practices](backup-azure-vms-introduction.md#best-practices). 

## <a name="vm-agent"></a>VM-Agent
### <a name="setting-up-hello-vm-agent"></a>Instellen van Hallo VM-Agent
Normaal gesproken is Hallo VM-Agent al aanwezig in virtuele machines die zijn gemaakt van hello Azure-galerie. Virtuele machines die worden gemigreerd van lokale datacenters zou echter geen Hallo VM-Agent is geïnstalleerd. Voor deze virtuele machines moet Hallo VM-Agent toobe expliciet worden geïnstalleerd.

Voor VM's van Windows:

* Download en installeer Hallo [agent-MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). U moet Administrator-bevoegdheden toocomplete Hallo installatie.
* Voor klassieke virtuele machines, [werk Hallo VM eigenschap](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate die Hallo agent is geïnstalleerd. Deze stap is niet vereist voor Resource Manager virtuele machines.

Voor virtuele Linux-machines:

* Meest recente installeren uit de opslagplaats voor distributie. We **aangeraden** installeren van de agent beperken tot de opslagplaats voor distributie. Voor informatie over de naam van het pakket, raadpleegt u te[opslagplaats voor Linux-agent](https://github.com/Azure/WALinuxAgent) 
* Voor klassieke virtuele machines, [werk Hallo VM eigenschap](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate die Hallo agent is geïnstalleerd. Deze stap is niet vereist voor Resource Manager virtuele machines.

### <a name="updating-hello-vm-agent"></a>Hallo VM-Agent bijwerken
Voor VM's van Windows:

* Bijwerken Hallo VM-Agent is net zo eenvoudig als opnieuw geïnstalleerd Hallo [binaire bestanden voor VM-Agent](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). U moet echter tooensure die geen back-upbewerking wordt uitgevoerd tijdens het Hallo die VM-Agent wordt bijgewerkt.

Voor virtuele Linux-machines:

* Volg de instructies Hallo op [Linux VM-Agent bijwerken](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
We **aangeraden** bijwerken agent beperken tot de opslagplaats voor distributie. We raden niet Hallo agent code downloaden vanuit rechtstreeks github en wordt bijgewerkt. Als de nieuwste agent is niet beschikbaar voor uw distributiepunt, kunt contact toodistribution ondersteuning voor instructies over het nieuwste tooinstall-agent. U kunt de meest recente controleren [Windows Azure Linux agent](https://github.com/Azure/WALinuxAgent/releases) informatie in de github-opslagplaats.

### <a name="validating-vm-agent-installation"></a>Installatie van de VM-Agent valideren
Hoe Hallo toocheck voor VM-Agent-versie van Windows virtuele machines:

1. Meld u aan de virtuele machine van Azure toohello en navigeer toohello map *C:\WindowsAzure\Packages*. U moet Hallo WaAppAgent.exe bestand aanwezig is.
2. Met de rechtermuisknop op het Hallo-bestand, gaat u te**eigenschappen**, en selecteer vervolgens Hallo **Details** tabblad Hallo productversie veld moet 2.6.1198.718 of hoger

## <a name="troubleshoot-vm-snapshot-issues"></a>VM-momentopname oplossen
VM-back-afhankelijk van de momentopnameopdrachten uitgeven toounderlying opslag. Geen kunnen toegang tot toostorage of vertragingen in uitvoering van een momentopname van de taak zorgen Hallo back-uptaak toofail. de volgende Hallo kan leiden tot momentopname taak mislukt.

1. Network access tooStorage is geblokkeerd met behulp van de NSG<br>
    Meer informatie over het te[-netwerktoegang inschakelen](backup-azure-vms-prepare.md#network-connectivity) tooStorage met beide WhiteListing van IP-adressen of proxyserver.
2. Virtuele machines met Sql Server back-up is geconfigureerd, kunnen leiden tot vertragingen momentopname <br>
   Standaard VM back-up problemen VSS volledige back-up op VM's van Windows. Dit kan op virtuele machines die worden uitgevoerd op het Sql-Servers en als de back-up van Sql Server is geconfigureerd, vertraging veroorzaken in momentopname worden uitgevoerd. Stel volgende registersleutel als u mislukte back-ups vanwege momentopname problemen ondervindt.

   ```
   [HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT]
   "USEVSSCOPYBACKUP"="TRUE"
   ```
3. VM-status gerapporteerd onjuist, omdat virtuele machine wordt afgesloten in RDP.  <br>
   Als u op Hallo virtuele machine in RDP hebt afgesloten, Controleer in de portal Hallo status van de virtuele machine correct wordt weergegeven. Als dat niet het geval is, sluit Hallo VM in de portal met de optie 'Afsluiten' in de VM-dashboard.
4. Als meer dan vier VMs share Hallo dezelfde cloudservice, dus geen is meer dan vier VM-back-ups worden gestart op Hallo back-ups voor meerdere back-upbeleid toostage Hallo configureren hetzelfde moment. Probeer toospread Hallo back-up begintijden een uur uit elkaar liggen tussen beleidsregels.
5. Virtuele machine wordt uitgevoerd op veel CPU/geheugen.<br>
   Als Hallo virtuele machine wordt uitgevoerd op een hoog CPU usage(>90%) en geheugen, momentopname taak in de wachtrij, vertraging en uiteindelijk time-out wordt opgehaald. Probeer het op aanvraag back-up in dergelijke situaties.

<br>

## <a name="networking"></a>Netwerken
Backup-extensie moet toegang tot het openbare internet toowork toohello zoals alle uitbreidingen. Geen toegang toohello met merkt openbare internet op verschillende manieren:

* Hallo-extensie installatie kan mislukken
* back-upbewerkingen hello (zoals schijf-momentopname) kunnen mislukken
* Weergeven van status van de back-upbewerking Hallo Hallo kan mislukken

Hallo nodig voor het oplossen van openbare internetadressen is gelede [hier](http://blogs.msdn.com/b/mast/archive/2014/06/18/azure-vm-provisioning-stuck-on-quot-installing-extensions-on-virtual-machine-quot.aspx). U moet toocheck Hallo DNS-configuraties voor Hallo VNET en zorg ervoor dat hello die Azure URI's kunnen worden opgelost.

Als het Hallo-naamomzetting correct is uitgevoerd, toegang tot de toohello die Azure IP-adressen ook toobe opgegeven moet. toounblock toegang toohello Azure-infrastructuur, voer een van de volgende stappen uit:

1. Geaccepteerde hello Azure datacenter IP-adresbereiken.
   * Lijst met Hallo [Azure datacenter IP-adressen](https://www.microsoft.com/download/details.aspx?id=41653) toobe wilt plaatsen.
   * De blokkering opheffen IP-adressen met Hallo Hallo [nieuw NetRoute](https://technet.microsoft.com/library/hh826148.aspx) cmdlet. Deze cmdlet binnen hello Azure VM worden uitgevoerd in een verhoogde PowerShell-venster (als Administrator uitvoeren).
   * Voeg regels toohello NSG (als u geïmplementeerd hebt) tooallow toegang toohello IP-adressen.
2. Een pad voor de HTTP-verkeer tooflow maken
   * Als u hebt implementeren sommige netwerkbeperking aanwezig (een Netwerkbeveiligingsgroep, bijvoorbeeld) een HTTP-proxy server tooroute Hallo verkeer. Stappen toodeploy u een HTTP-proxyserver vindt [hier](backup-azure-vms-prepare.md#network-connectivity).
   * Voeg regels toohello NSG (als u geïmplementeerd hebt) tooallow toegang toohello INTERNET van Hallo HTTP-Proxy.

> [!NOTE]
> DHCP moet zijn ingeschakeld in de Gast Hallo voor IaaS VM-back-toowork.  Als u een statisch privé IP-adres nodig hebt, moet u deze configureren via Hallo-platform. Hallo DHCP-optie binnen Hallo VM moet blijven ingeschakeld.
> Meer informatie weergeven over [instellen van een statische interne persoonlijke IP-adres](../virtual-network/virtual-networks-reserved-private-ip.md).
>
>
