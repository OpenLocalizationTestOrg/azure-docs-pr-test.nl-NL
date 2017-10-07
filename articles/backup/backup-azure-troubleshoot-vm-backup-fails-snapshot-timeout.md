---
title: 'Azure Backup-fout oplossen: Guest Agent Status niet beschikbaar | Microsoft Docs'
description: 'Symptomen, oorzaken en oplossingen van Azure Backup fouten gerelateerde tooerror: kan niet communiceren met de Hallo VM-agent'
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
keywords: Azure back-up. VM-agent; Verbinding met het netwerk;
ms.assetid: 4b02ffa4-c48e-45f6-8363-73d536be4639
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: genli;markgal;
ms.openlocfilehash: 724c61ba80d0a9ef91a5f8543ae72bb86968881b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-backup-failure-issues-with-agent-andor-extension"></a>Azure Backup-fout oplossen: problemen met de agent en/of extensie

Dit artikel bevat voor probleemoplossing stappen toohelp u back-up fouten oplossen gerelateerde tooproblems communicatie met VM-agent en de extensie.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="vm-agent-unable-toocommunicate-with-azure-backup"></a>VM-Agent kan geen toocommunicate met Azure Backup
Nadat u registreren en plannen van een VM voor hello Azure Backup-service, initieert back-up Hallo taak door de communicatie met de Hallo VM-agent tootake een momentopname van een punt in tijd. Een van de volgende voorwaarden Hallo Hallo momentopname wordt geactiveerd, wat op zijn beurt tooBackup fout kan leiden mogelijk niet. Volg onderstaande stappen in de gegeven volgorde Hallo voor probleemoplossing en probeer de bewerking opnieuw.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>1 oorzaak: [Hallo VM geen internettoegang heeft](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>2 oorzaak: [Hallo-agent is geïnstalleerd in Hallo VM, maar reageert (voor Windows-VM's)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>3 oorzaak: [Hallo-agent is geïnstalleerd in Hallo VM is verouderd (voor Linux VM's)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>4 oorzaak: [Hallo momentopname status kan niet worden opgehaald of een momentopname kan niet worden gemaakt.](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>5 oorzaak: [Hallo Backup-extensie tooupdate of laden mislukt](#the-backup-extension-fails-to-update-or-load)

## <a name="snapshot-operation-failed-due-toono-network-connectivity-on-hello-virtual-machine"></a>Momentopname-bewerking is mislukt vanwege de netwerkverbinding toono op Hallo virtuele machine
Nadat u registreren en plannen van een VM voor hello Azure Backup-service, initieert back-up taak Hallo door Hallo VM Backup-extensie tootake punt in tijd momentopname communiceert. Een van de volgende voorwaarden Hallo Hallo momentopname wordt geactiveerd, wat op zijn beurt tooBackup fout kan leiden mogelijk niet. Volg onderstaande stappen in de gegeven volgorde Hallo voor probleemoplossing en probeer de bewerking opnieuw.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>1 oorzaak: [Hallo VM geen internettoegang heeft](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>2 oorzaak: [Hallo momentopname status kan niet worden opgehaald of een momentopname kan niet worden gemaakt.](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-3-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>3 oorzaak: [Hallo Backup-extensie tooupdate of laden mislukt](#the-backup-extension-fails-to-update-or-load)

## <a name="vmsnapshot-extension-operation-failed"></a>VMSnapshot extensie-bewerking is mislukt.

Nadat u registreren en plannen van een VM voor hello Azure Backup-service, initieert back-up taak Hallo door Hallo VM Backup-extensie tootake punt in tijd momentopname communiceert. Een van de volgende voorwaarden Hallo Hallo momentopname wordt geactiveerd, wat op zijn beurt tooBackup fout kan leiden mogelijk niet. Volg onderstaande stappen in de gegeven volgorde Hallo voor probleemoplossing en probeer de bewerking opnieuw.
##### <a name="cause-1-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>1 oorzaak: [Hallo momentopname status kan niet worden opgehaald of een momentopname kan niet worden gemaakt.](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-2-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>2 oorzaak: [Hallo Backup-extensie tooupdate of laden mislukt](#the-backup-extension-fails-to-update-or-load)
##### <a name="cause-3-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>3 oorzaak: [Hallo VM geen internettoegang heeft](#the-vm-has-no-internet-access)
##### <a name="cause-4-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>4 oorzaak: [Hallo-agent is geïnstalleerd in Hallo VM, maar reageert (voor Windows-VM's)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-5-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>5 oorzaak: [Hallo-agent is geïnstalleerd in Hallo VM is verouderd (voor Linux VM's)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)

## <a name="unable-tooperform-hello-operation-as-hello-vm-agent-is-not-responsive"></a>Kan geen tooperform Hallo bewerking als Hallo VM-Agent is niet reageren

Nadat u registreren en plannen van een VM voor hello Azure Backup-service, initieert back-up taak Hallo door Hallo VM Backup-extensie tootake punt in tijd momentopname communiceert. Een van de volgende voorwaarden Hallo Hallo momentopname wordt geactiveerd, wat op zijn beurt tooBackup fout kan leiden mogelijk niet. Volg onderstaande stappen in de gegeven volgorde Hallo voor probleemoplossing en probeer de bewerking opnieuw.
##### <a name="cause-1-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>1 oorzaak: [Hallo-agent is geïnstalleerd in Hallo VM, maar reageert (voor Windows-VM's)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-2-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>2 oorzaak: [Hallo-agent is geïnstalleerd in Hallo VM is verouderd (voor Linux VM's)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-3-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>3 oorzaak: [Hallo VM geen internettoegang heeft](#the-vm-has-no-internet-access)

## <a name="backup-failed-with-an-internal-error---please-retry-hello-operation-in-a-few-minutes"></a>Back-up is mislukt met een interne fout: Voer de bewerking Hallo over een paar minuten opnieuw uit

Nadat u registreren en plannen van een VM voor hello Azure Backup-service, initieert back-up taak Hallo door Hallo VM Backup-extensie tootake punt in tijd momentopname communiceert. Een van de volgende voorwaarden Hallo Hallo momentopname wordt geactiveerd, wat op zijn beurt tooBackup fout kan leiden mogelijk niet. Volg onderstaande stappen in de gegeven volgorde Hallo voor probleemoplossing en probeer de bewerking opnieuw.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>1 oorzaak: [Hallo VM geen internettoegang heeft](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-agent-installed-in-hello-vm-but-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>2 oorzaak: [Hallo-agent is geïnstalleerd in Hallo VM maar niet reageert (voor Windows-VM's)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>3 oorzaak: [Hallo-agent is geïnstalleerd in Hallo VM is verouderd (voor Linux VM's)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>4 oorzaak: [Hallo momentopname status kan niet worden opgehaald of een momentopname kan niet worden gemaakt.](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>5 oorzaak: [Hallo Backup-extensie tooupdate of laden mislukt](#the-backup-extension-fails-to-update-or-load)


## <a name="causes-and-solutions"></a>Oorzaken en oplossingen

### <a name="hello-vm-has-no-internet-access"></a>Hallo VM heeft geen internettoegang
Per implementatievereiste hello, Hallo VM geen internettoegang heeft of beperkingen waardoor toegang toohello Azure-infrastructuur heeft.

toofunction correct Hallo Backup-extensie vereist connectiviteit toohello Azure openbare IP-adressen. Hallo-extensie verzendt opdrachten tooan Azure Storage-eindpunt (http-URL) toomanage Hallo momentopnamen van Hallo VM. Als het Hallo-uitbreiding heeft geen toegang tot toohello die openbare Internet, uiteindelijk Backup mislukt.

####  <a name="solution"></a>Oplossing
tooresolve hello probleem, probeer van Hallo methoden die hier worden vermeld.
##### <a name="allow-access-toohello-azure-datacenter-ip-ranges"></a>Toegang toestaan toohello Azure datacenter IP-adresbereiken

1. Hallo verkrijgen [lijst met Azure datacenter IP-adressen](https://www.microsoft.com/download/details.aspx?id=41653) tooallow toegang tot.
2. Hallo IP-adressen door het uitvoeren van Hallo deblokkeren **nieuw NetRoute** cmdlet in hello Azure virtuele machine in een PowerShell-venster met verhoogde bevoegdheid. Hallo-cmdlet uitvoeren als beheerder.
3. tooallow toegang toohello IP-adressen, toevoegen regels toohello netwerkbeveiligingsgroep, als er een.

##### <a name="create-a-path-for-http-traffic-tooflow"></a>Een pad voor de HTTP-verkeer tooflow maken

1. Als u beschikken over netwerkbeperkingen (bijvoorbeeld een netwerkbeveiligingsgroep), implementeert u een HTTP-proxy server tooroute Hallo verkeer.
2. tooallow toegang toohello Internet van de HTTP-proxyserver Hallo toevoegen regels toohello netwerkbeveiligingsgroep, als er een.

hoe tooset van een HTTP-proxy voor back-ups van virtuele machine, Zie toolearn [voorbereiden van uw omgeving tooback van virtuele machines in Azure](backup-azure-vms-prepare.md#using-an-http-proxy-for-vm-backups).

Als u van schijven worden beheerd gebruikmaakt, moet u een extra poort (8443) openen op Hallo firewalls.

### <a name="hello-agent-installed-in-hello-vm-but-unresponsive-for-windows-vms"></a>Hallo-agent is geïnstalleerd in Hallo VM maar niet reageert (voor Windows-VM's)

#### <a name="solution"></a>Oplossing
Hallo VM-Agent is beschadigd of Hallo-service is gestopt. Opnieuw te installeren Hallo VM-agent kan helpen de meest recente versie Hallo ophalen en start opnieuw op Hallo communicatie.

1. Controleer of Windows Guest Agent-service die wordt uitgevoerd in services (services.msc) van de virtuele Machine Hallo. Probeer Hallo Windows Guest Agent-service opnieuw starten en Hallo back-up starten<br>
2. Als dit niet zichtbaar in de services is, controleert u of in programma's en onderdelen of Windows Guest agent-service is geïnstalleerd.
4. Als u kunnen tooview in programma's en onderdelen verwijderen Hallo Windows Guest Agent.
5. Download en installeer Hallo [meest recente versie van de agent-MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). U moet Administrator-bevoegdheden toocomplete Hallo installatie.
6. Vervolgens moet u kunnen tooview Guest-Agent voor Windows-services in services
7. Voer een op-verzoek/ad-hoc back-up door te klikken op 'Nu back-up' in Hallo-portal.

Controleer ook de virtuele Machine is  **[.NET 4.5 geïnstalleerd in Hallo systeem](https://docs.microsoft.com/en-us/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed)**. Het is vereist voor Hallo VM-agent toocommunicate met Hallo-service

### <a name="hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vms"></a>Hallo-agent is geïnstalleerd in Hallo VM is verouderd (voor Linux VM's)

#### <a name="solution"></a>Oplossing
Meest agent gerelateerde of extensie-gerelateerde fouten voor virtuele Linux-machines worden veroorzaakt door problemen met een verouderd VM-agent. tootroubleshoot dit probleem, volgt u deze algemene richtlijnen:

1. Volg de instructies Hallo voor [Hallo Linux VM-agent bijwerken](../virtual-machines/linux/update-agent.md).

 >[!NOTE]
 >We *aangeraden* Hallo agent beperken tot een opslagplaats distributiepunten bij te werken. We raden niet Hallo agent code rechtstreeks vanuit GitHub downloaden en wordt bijgewerkt. Als de nieuwste agent Hallo niet beschikbaar voor de distributie is, contact op met ondersteuning van de distributie voor instructies over het tooinstall deze. toocheck voor de meest recente agent hello, Ga toohello [Windows Azure Linux agent](https://github.com/Azure/WALinuxAgent/releases) pagina in Hallo GitHub-opslagplaats.

2. Zorg ervoor dat hello Azure-agent wordt uitgevoerd op Hallo VM door het uitvoeren van de volgende opdracht Hallo:`ps -e`

 Als Hallo proces niet wordt uitgevoerd, start u deze opnieuw met Hallo volgende opdrachten:

 * Voor Ubuntu:`service walinuxagent start`
 * Voor andere distributies:`service waagent start`

3. [Hallo automatisch opnieuw opstarten agent configureren](https://github.com/Azure/WALinuxAgent/wiki/Known-Issues#mitigate_agent_crash).
4. Voer een nieuwe test back-up. Als Hallo fout zich blijft voordoen, neem Hallo volgende Logboeken uit van de klant Hallo VM te verzamelen:

   * /var/lib/waagent/*.XML
   * /var/log/waagent.log
   * / var/aanmelden/azure / *

Als we uitgebreide logboekregistratie is vereist voor waagent, volg deze stappen:

1. Zoek in Hallo /etc/waagent.conf bestand Hallo volgt regel: **uitgebreide logboekregistratie inschakelen (y | n)**
2. Wijziging Hallo **Logs.Verbose** waarde uit de  *n*  te*y*.
3. Hallo wijziging opslaan en start waagent Hallo vorige stappen in deze sectie.

### <a name="hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Hallo momentopname status kan niet worden opgehaald of een momentopname kan niet worden gemaakt.
VM-back-Hallo afhankelijk van het uitgeven van een momentopname opdracht toohello onderliggende storage-account. Back-up kan mislukken omdat er geen toegang tot toohello storage-account of omdat het Hallo-uitvoering van Hallo momentopname taak wordt vertraagd.

#### <a name="solution"></a>Oplossing
Taakfout momentopname kan worden veroorzaakt door Hallo volgende voorwaarden:

| Oorzaak | Oplossing |
| --- | --- |
| Hallo VM heeft SQL Server back-up is geconfigureerd. | Standaard wordt een volledige back-up voor VSS Hallo VM-back-uitgevoerd op virtuele machines van Windows. Op virtuele machines die worden uitgevoerd op basis van SQL Server-servers en op welke SQL-Server worden de back-up geconfigureerd, is de momentopname uitvoering vertragingen optreden.<br><br>Als er een back-up mislukt vanwege een probleem met de momentopname, stel Hallo volgende registersleutel:<br><br>**[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT] 'USEVSSCOPYBACKUP '=' TRUE'** |
| Hallo VM-status is niet juist gerapporteerd, omdat Hallo VM wordt afgesloten in RDP. | Als u Hallo VM in Remote Desktop Protocol (RDP) afsluit, controleert u Hallo portal toodetermine of Hallo VM-status juist is. Als dit niet juist is, afgesloten Hallo VM in Hallo-portal met behulp van Hallo **afsluiten** optie op Hallo VM dashboard. |
| Veel virtuele machines van Hallo dezelfde cloudservice zijn geconfigureerd tooback up op Hallo hetzelfde moment. | Het is een best practice toospread uit Hallo back-upschema's voor virtuele machines van Hallo dezelfde cloudservice. |
| Hallo VM wordt uitgevoerd op een hoog gebruik van CPU of geheugen. | Hallo VM wordt uitgevoerd op een hoog CPU-gebruik (meer dan 90 procent) of hoog geheugengebruik, Hallo momentopname taak in de wachtrij geplaatst en wordt vertraagd als er uiteindelijk een time-out optreedt. In deze situatie probeert een-op-verzoek back-up. |
| Hallo VM ontvangen geen Hallo host/fabric-adres van DHCP. | DHCP moet binnen Hallo gastbesturingssysteem voor Hallo back-toowork IaaS VM zijn ingeschakeld.  Als hello VM niet Hallo host/fabric-adres van de DHCP-antwoord 245, kan het downloaden of uitvoeren van de uitbreidingen. Als u een statisch privé IP-adres nodig hebt, moet u deze configureren via Hallo-platform. Hallo DHCP-optie binnen Hallo VM moet blijven ingeschakeld. Zie voor meer informatie [instellen van een statische interne persoonlijke IP-adres](../virtual-network/virtual-networks-reserved-private-ip.md). |

### <a name="hello-backup-extension-fails-tooupdate-or-load"></a>Hallo Backup-extensie mislukt tooupdate of laden
Als extensies kunnen niet worden geladen, wordt de back-up mislukt omdat een momentopname kan niet worden gemaakt.

#### <a name="solution"></a>Oplossing

**Voor Windows-gasten:** Verifieer dat Hallo iaasvmprovider service is ingeschakeld en een opstarttype is *automatische*. Als Hallo-service is niet geconfigureerd op deze manier, inschakelen toodetermine of Hallo volgende back-up is geslaagd.

**Voor Linux-gasten:** Controleer Hallo meest recente versie van VMSnapshot voor Linux (Hallo-extensie wordt gebruikt door de back-up) 1.0.91.0 is.<br>


Als de Backup-extensie Hallo nog steeds niet tooupdate of belasting, kunt u Hallo VMSnapshot extensie toobe is opnieuw geladen met het verwijderen van extensie Hallo afdwingen. de volgende back-poging Hallo laadt u opnieuw Hallo-extensie.

toouninstall Hallo uitbreiding, Hallo te volgen:

1. Ga toohello [Azure-portal](https://portal.azure.com/).
2. Zoek Hallo VM die back-problemen.
3. Klik op **instellingen**.
4. Klik op **extensies**.
5. Klik op **Vmsnapshot extensie**.
6. Klik op **verwijderen**.

Deze procedure wordt Hallo extensie toobe opnieuw geïnstalleerd tijdens de volgende back-up Hallo.

