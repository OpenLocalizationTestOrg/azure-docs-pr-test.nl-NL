---
title: aaaTroubleshoot Azure back-up van fouten in de klassieke portal | Microsoft Docs
description: Los problemen met Azure back-up en herstel van virtuele machines in de klassieke portal Hallo in Azure.
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 117201fb-c0cd-4be4-b47f-abd88fe914cf
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: trinadhk;markgal;
ms.openlocfilehash: b9907f6fa57c631f5446c4d00f946a57c4efd72b
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

## <a name="discovery"></a>Detectie
| Back-upbewerking | Details van fouten | Tijdelijke oplossing |
| --- | --- | --- |
| Detectie |Mislukte toodiscover nieuwe items - Microsoft Azure Backup aangetroffen en interne fout. Wacht een paar minuten en probeer Hallo opnieuw. |Probeer het detectieproces Hallo na 15 minuten. |
| Detectie |Kan geen nieuwe items toodiscover – detectie van een andere bewerking al uitgevoerd wordt. Wacht totdat de huidige detectiebewerking Hallo is voltooid. |Geen |

## <a name="register"></a>Registreren
| Back-upbewerking | Details van fouten | Tijdelijke oplossing |
| --- | --- | --- |
| Registreren |Aantal gegevensschijven gekoppeld toohello virtuele machine overschreden Hallo ondersteund limiet - Neem een aantal gegevensschijven op deze virtuele machine en probeer het opnieuw Hallo-bewerking los te koppelen. Biedt ondersteuning voor Azure-back-up too16 gegevensschijven gekoppeld tooan Azure virtuele machine voor back-up |Geen |
| Registreren |Microsoft Azure Backup heeft een interne fout - wacht een paar minuten en probeer opnieuw Hallo. Als Hallo probleem zich blijft voordoen, neem dan contact op met Microsoft Support. |U kunt deze fout vanwege tooone Hallo volgende niet-ondersteunde configuratie van de virtuele machine op Premium LRS ophalen. <br> Premium-opslag virtuele machines kan worden back-up met behulp van de recovery services-kluis. [Meer informatie](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup) |
| Registreren |Registratie is mislukt met de time-out voor de bewerking van Agent installeren |Controleer of de besturingssysteemversie Hallo van Hallo virtuele machine wordt ondersteund. |
| Registreren |Opdracht is mislukt: een andere bewerking wordt uitgevoerd voor dit item. Wacht totdat de vorige bewerking Hallo is voltooid |Geen |
| Registreren |Virtuele machines met virtuele harde schijven die zijn opgeslagen op Premium-opslag worden niet ondersteund voor back-up |Geen |
| Registreren |Agent van de virtuele machine is niet aanwezig op Hallo virtuele machine: Installeer Hallo vereist vereiste, VM-agent en start Hallo-bewerking opnieuw. |[Lees meer](#vm-agent) over de installatie van de VM-agent en hoe toovalidate Hallo voor de installatie van de VM-agent. |

## <a name="backup"></a>Back-up
| Back-upbewerking | Details van fouten | Tijdelijke oplossing |
| --- | --- | --- |
| Back-up |Kan niet communiceren met de Hallo VM-agent voor de status van de momentopname. Er is een time-out opgetreden voor de momentopname VM sub-taak. -Zie Hallo probleemoplossing handleiding voor het tooresolve dit. |Deze fout wordt gegenereerd als er een probleem met de Hallo VM-Agent of netwerk toegang toohello Azure-infrastructuur is geblokkeerd op een bepaalde manier. Meer informatie over [problemen momentopname maken van VM-foutopsporing](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md). <br> Als Hallo VM-agent is niet wordt veroorzaakt door problemen, start u Hallo VM. Een onjuiste status voor de virtuele machine kan soms problemen veroorzaken en opnieuw te starten Hallo VM herstelt u deze 'slechte staat' |
| Back-up |Back-up is mislukt met een interne fout: Voer de bewerking Hallo over een paar minuten opnieuw uit. Als Hallo probleem zich blijft voordoen, neem dan contact op met Microsoft Support |Controleer of er een tijdelijk probleem bij het openen van de VM-opslag. Controleer of [Azure Status](https://azure.microsoft.com/en-us/status/) toosee als er continu gerelateerde toocompute / / opslagnetwerk in Hallo regio uitgeven. Controleer is opnieuw Hallo back-up post probleem verholpen. |
| Back-up |Kan de Hallo-bewerking niet uitvoeren omdat de virtuele machine niet meer bestaat. |Back-up kan niet worden uitgevoerd omdat hello VM geconfigureerd voor back-up is verwijderd. Stop verdere back-ups gaat tooProtected items weergeven, selecteert u beveiligde item op en klik op beveiliging stoppen. U kunt gegevens behouden door back-up behouden gegevensoptie te selecteren. U kunt later beveiliging hervatten voor deze virtuele machine door te klikken op beveiligingsconfiguratie van geregistreerde Items weergeven |
| Back-up |Mislukte tooinstall hello Azure Recovery Services-extensie op Hallo geselecteerd item - VM-Agent is een vereiste voor Azure Recovery Services-extensie. Installeer hello Azure VM-agent en start Hallo registratie bewerking opnieuw |<ol> <li>Controleer of de Hallo VM-agent correct is geïnstalleerd. <li>Zorg ervoor dat Hallo vlag op Hallo VM-configuratie correct is ingesteld.</ol> [Lees meer](#validating-vm-agent-installation) over de installatie van de VM-agent en hoe toovalidate Hallo voor de installatie van de VM-agent. |
| Back-up |Opdracht uitvoering is mislukt: een andere bewerking wordt momenteel uitgevoerd voor dit item. Wacht totdat de vorige bewerking Hallo is voltooid en probeer het vervolgens opnieuw |Een bestaande back-up of herstel van de taak voor Hallo VM wordt uitgevoerd en een nieuwe taak kan niet worden gestart terwijl bestaande Hallo-taak wordt uitgevoerd. |
| Back-up |Installatie van de uitbreiding is mislukt met fout Hallo 'COM + is tootalk toohello Microsoft Distributed Transaction Coordinator |Dit betekent meestal dat Hallo COM +-service niet wordt uitgevoerd. Neem contact op met Microsoft ondersteuning voor hulp bij het oplossen van dit probleem. |
| Back-up |Momentopname-bewerking is mislukt met de Hallo VSS-fout voor bewerking 'dit station is vergrendeld door BitLocker-stationsversleuteling. U moet deze schijf van het Configuratiescherm ontgrendelen. |BitLocker uitschakelen voor alle stations op Hallo virtuele machine en bekijk of Hallo VSS probleem is opgelost |
| Back-up |Virtuele machines met virtuele harde schijven die zijn opgeslagen op Premium-opslag worden niet ondersteund voor back-up |Geen |
| Back-up |Azure virtuele Machine is niet gevonden. |Dit gebeurt wanneer hello primaire virtuele machine is verwijderd, maar Hallo back-upbeleid toolook voor een VM-tooperform back-up blijft. toofix deze fout: <ol><li>Hallo virtuele machine met de Hallo opnieuw dezelfde naam en hetzelfde Resourcegroepnaam [cloudservicenaam] <br>(OR) <li> Schakel de beveiliging voor deze virtuele machine zodat de volgende back-ups worden niet ophalen geactiveerd. </ol> |
| Back-up |Agent van de virtuele machine is niet aanwezig op Hallo virtuele machine: Installeer Hallo vereist vereiste, VM-agent en start Hallo-bewerking opnieuw. |[Lees meer](#vm-agent) over de installatie van de VM-agent en hoe toovalidate Hallo voor de installatie van de VM-agent. |

## <a name="jobs"></a>Taken
| Bewerking | Details van fouten | Tijdelijke oplossing |
| --- | --- | --- |
| Taak annuleren |Annulering wordt niet ondersteund voor dit taaktype: wacht totdat het Hallo-taak is voltooid. |Geen |
| Taak annuleren |Hallo-taak is niet in een status Annuleerbare - wacht totdat het Hallo-taak is voltooid. <br>OF<br> Hallo geselecteerde taak is niet in een status Annuleerbare - Hallo taak toocomplete een ogenblik geduld. |Hallo-taak is bijna voltooid naar alle waarschijnlijkheid; Wacht totdat het Hallo-taak is voltooid |
| Taak annuleren |Kan het Hallo-taak niet annuleren omdat deze niet uitgevoerd is-deze annulering wordt alleen ondersteund voor taken die uitgevoerd worden. Annuleer van poging op een onderhanden taak. |Dit gebeurt vanwege tooa tijdelijke status. Wacht een paar minuten en probeer de bewerking annuleren Hallo |
| Taak annuleren |Mislukte toocancel Hallo functie - wacht totdat de taak is voltooid. |Geen |

## <a name="restore"></a>Herstellen
| Bewerking | Details van fouten | Tijdelijke oplossing |
| --- | --- | --- |
| Herstellen |Terugzetten is mislukt vanwege een interne Cloud fout |<ol><li>Cloud service toowhich u toorestore probeert is geconfigureerd met DNS-instellingen. U kunt controleren <br>$deployment = get-AzureDeployment - ServiceName "ServiceName"-sleuf 'Productie' Get-AzureDns - DnsSettings $deployment. DnsSettings<br>Als er is een adres dat is geconfigureerd, betekent dit dat de DNS-instellingen zijn geconfigureerd.<br> <li>Cloud service toowhich tooyou probeert toorestore is geconfigureerd met ReservedIP en bestaande virtuele machines in de cloudservice wordt gestopt.<br>U kunt controleren dat een cloudservice is gereserveerde IP-adres via de volgende powershell-cmdlets:<br>$deployment = get-AzureDeployment - ServiceName "servicename"-sleuf 'Productie' $dep. ReservedIPName <br><li>U probeert een virtuele machine met de volgende speciale netwerkconfiguraties in toosame cloudservice toorestore. <br>-Virtuele machines onder load balancer-configuratie (intern en extern)<br>-Virtuele machines met meerdere gereserveerde IP 's<br>-Virtuele machines met meerdere NIC 's<br>Selecteer een nieuwe cloudservice in Hallo UI of Raadpleeg het te[terugzetten overwegingen](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations) voor virtuele machines met speciale netwerkconfiguraties</ol> |
| Herstellen |Hallo geselecteerd DNS-naam is al in gebruik: Geef een andere DNS-naam en probeer het opnieuw. |Hallo DNS-naam hier verwijst toohello cloudservicenaam (meestal eindigend. cloudapp.net). Dit moet toobe uniek zijn. Als deze fout optreedt, moet u toochoose een andere naam voor de virtuele machine tijdens het terugzetten. <br><br> Deze fout wordt alleen toousers Hallo Azure-portal weergegeven. Hallo c:\Windows via PowerShell omdat deze alleen worden hersteld Hallo schijven en Hallo VM niet maken. Hallo fout zal worden geconfronteerd wanneer Hallo VM na Hallo schijf terugzetten expliciet door u is gemaakt. |
| Herstellen |Hallo opgegeven virtuele netwerkconfiguratie is niet correct: Geef een ander virtueel netwerk-configuratie en probeer het opnieuw. |Geen |
| Herstellen |Hallo opgegeven service in de cloud met behulp van een gereserveerd IP-adres die komt niet overeen met het Hallo-configuratie van Hallo virtuele machine wordt hersteld - Geef een andere cloudservice die geen gebruik van gereserveerde IP-adres maakt, of kies een ander herstelpunt punt toorestore uit. |Geen |
| Herstellen |Cloudservice heeft de limiet voor aantal eindpunten voor invoer - opnieuw Hallo uitvoeren door te geven van een andere cloudservice of met behulp van een bestaand eindpunt bereikt. |Geen |
| Herstellen |Back-kluis en doel storage-account zijn in twee verschillende regio's: Zorg ervoor dat Hallo storage-account opgegeven in de herstelbewerking Hallo dezelfde Azure-regio als Hallo back-upkluis. |Geen |
| Herstellen |Storage-Account opgegeven voor Hallo restore-bewerking niet is ondersteund - alleen Basic/Standard storage-accounts met lokaal redundante of geografisch redundante replicatie-instellingen worden ondersteund. Selecteer een ondersteunde storage-account |Geen |
| Herstellen |Type Opslagaccount dat is opgegeven voor de herstelbewerking is niet online - Zorg ervoor dat de Hallo storage-account opgegeven in restore-bewerking online is |Dit kan gebeuren vanwege een tijdelijke fout in Azure Storage of vervaldatum tooan storing. Kies een ander opslagaccount. |
| Herstellen |Resourcegroep quotum is bereikt - Verwijder een aantal resourcegroepen vanuit Azure-portal of neem contact op met de ondersteuning van Azure tooincrease Hallo limieten. |Geen |
| Herstellen |Geselecteerde subnet bestaat niet: Selecteer een subnet dat bestaat |Geen |

## <a name="policy"></a>Beleid
| Bewerking | Details van fouten | Tijdelijke oplossing |
| --- | --- | --- |
| Beleid maken |Kan geen beleid voor toocreate Hallo - Verminder Hallo bewaren keuzes toocontinue met de configuratie van beleid. |Geen |

## <a name="vm-agent"></a>VM-Agent
### <a name="setting-up-hello-vm-agent"></a>Instellen van Hallo VM-Agent
Normaal gesproken is Hallo VM-Agent al aanwezig in virtuele machines die zijn gemaakt van hello Azure-galerie. Virtuele machines die worden gemigreerd van lokale datacenters zou echter geen Hallo VM-Agent is geïnstalleerd. Voor deze virtuele machines moet Hallo VM-Agent toobe expliciet worden geïnstalleerd. Lees meer over [installeren Hallo VM-agent op een bestaande virtuele machine](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).

Voor VM's van Windows:

* Download en installeer Hallo [agent-MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). U moet Administrator-bevoegdheden toocomplete Hallo installatie.
* [Werk Hallo VM eigenschap](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate die Hallo agent is geïnstalleerd.

Voor virtuele Linux-machines:

* Installeer de meest recente [Linux-agent](https://github.com/Azure/WALinuxAgent) vanuit github.
* [Werk Hallo VM eigenschap](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate die Hallo agent is geïnstalleerd.

### <a name="updating-hello-vm-agent"></a>Hallo VM-Agent bijwerken
Voor VM's van Windows:

* Bijwerken Hallo VM-Agent is net zo eenvoudig als opnieuw geïnstalleerd Hallo [binaire bestanden voor VM-Agent](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). U moet echter tooensure die geen back-upbewerking wordt uitgevoerd tijdens het Hallo die VM-Agent wordt bijgewerkt.

Voor virtuele Linux-machines:

* Volg de instructies Hallo op [Linux VM-Agent bijwerken](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="validating-vm-agent-installation"></a>Installatie van de VM-Agent valideren
Hoe Hallo toocheck voor VM-Agent-versie van Windows virtuele machines:

1. Meld u aan de virtuele machine van Azure toohello en navigeer toohello map *C:\WindowsAzure\Packages*. U moet Hallo WaAppAgent.exe bestand aanwezig is.
2. Met de rechtermuisknop op het Hallo-bestand, gaat u te**eigenschappen**, en selecteer vervolgens Hallo **Details** tabblad Hallo productversie veld moet 2.6.1198.718 of hoger
