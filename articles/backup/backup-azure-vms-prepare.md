---
title: aaaPreparing uw omgeving tooback van virtuele machines in Azure | Microsoft Docs
description: Zorg ervoor dat uw omgeving is voorbereid voor de back-ups van virtuele machines in Azure
services: backup
documentationcenter: 
author: markgalioto
manager: carmonn
editor: 
keywords: back-ups; een back-up;
ms.assetid: 238ab93b-8acc-4262-81b7-ce930f76a662
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/25/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 3b914c507dd6ad703ea799115ae84ac229e27787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-azure-virtual-machines"></a>Voorbereiden van uw omgeving tooback van virtuele machines in Azure
> [!div class="op_single_selector"]
> * [Resource Manager-model](backup-azure-arm-vms-prepare.md)
> * [Klassieke model](backup-azure-vms-prepare.md)
>
>

Voordat u kunt back-up Azure een virtuele machine (VM), zijn er drie voorwaarden moeten bestaan.

* U moet een back-upkluis toocreate of een bestaande back-upkluis identificeren *in Hallo dezelfde regio bevinden als uw VM*.
* Geen netwerkverbinding tussen hello Azure Internet adressen en hello Azure storage-eindpunten.
* Hallo VM-agent installeren op Hallo VM.

Als u deze voorwaarden al bestaat in uw omgeving en doorgaan toohello [Back-up van uw virtuele machines artikel](backup-azure-vms.md). Anders loodst lezen op, in dit artikel u door Hallo stappen tooprepare uw tooback omgeving van een virtuele machine in Azure.

##<a name="supported-operating-system-for-backup"></a>Ondersteund besturingssysteem voor back-up
 * **Linux**: Azure Backup ondersteunt [een lijst met distributies die zijn goedgekeurd door Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), met uitzondering van Core OS Linux. _Andere Bring-Your-eigenaar-Linux-distributies ook mogelijk werken zolang Hallo VM-agent beschikbaar op Hallo virtuele machine is en ondersteuning voor Python bestaat. We tekent echter niet de distributies voor back-up._
 * **Windows Server**: versies ouder dan Windows Server 2008 R2 worden niet ondersteund.


## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>Beperkingen bij een back-up en herstellen van een virtuele machine
> [!NOTE]
> Azure heeft twee implementatiemodellen voor het maken en werken met resources: [Resource Manager en classic](../azure-resource-manager/resource-manager-deployment-model.md). Hallo volgende lijst bevat Hallo beperkingen bij implementatie in het klassieke model Hallo.
>
>

* Back-ups van virtuele machines met meer dan 16 gegevensschijven wordt niet ondersteund.
* Back-ups van virtuele machines met een gereserveerd IP-adres en er is geen gedefinieerde eindpunt wordt niet ondersteund.
* Back-upgegevens bevat geen tooVM van netwerk gekoppelde stations die zijn gekoppeld.
* Een bestaande virtuele machine kan tijdens het herstel niet worden vervangen. Hallo bestaande virtuele machine en alle gekoppelde schijven eerst te verwijderen en vervolgens Hallo gegevens terugzetten vanaf back-up.
* Regio-overschrijdende back-up en herstel wordt niet ondersteund.
* Back-ups van virtuele machines met behulp van hello Azure Backup-service wordt ondersteund in alle openbare gebieden van Azure (Zie Hallo [controlelijst](https://azure.microsoft.com/regions/#services) van ondersteunde regio's). Als Hallo regio die u zoekt niet vandaag ondersteund wordt, wordt deze niet weergegeven in de vervolgkeuzelijst Hallo tijdens het maken van de kluis.
* Back-ups van virtuele machines met behulp van hello Azure Backup-service wordt alleen ondersteund voor Selecteer besturingssystemen:
* Herstellen van een domeincontroller wordt (DC) VM die deel uitmaakt van een multi-DC-configuratie alleen ondersteund door PowerShell. Lees meer over [een multi-DC-domeincontroller terugzetten](backup-azure-restore-vms.md#restoring-domain-controller-vms).
* Herstellen van virtuele machines waarvoor speciale netwerkconfiguraties na hello wordt alleen ondersteund door PowerShell. Virtuele machines die u maakt met behulp van Hallo terugzetten werkstroom in Hallo UI geen deze netwerkconfiguraties nadat Hallo restore-bewerking voltooid is. toolearn meer, Zie [herstellen van virtuele machines met speciale netwerkconfiguraties](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).
  * Virtuele machines onder een load balancer-configuratie (intern en extern)
  * Virtuele machines met meerdere gereserveerde IP-adressen
  * Virtuele machines met meerdere netwerkadapters

## <a name="create-a-backup-vault-for-a-vm"></a>Een back-upkluis maken voor een virtuele machine
Een back-upkluis is een entiteit waarmee alle Hallo back-ups en herstelpunten die zijn gemaakt na verloop van tijd worden opgeslagen. Hallo back-upkluis bevat ook back-upbeleid Hallo die worden toegepast toohello virtuele machines back-up wordt gemaakt.

> [!IMPORTANT]
> Vanaf maart 2017, kunt u niet meer gebruiken Hallo klassieke portal toocreate Backup-kluizen. Bestaande Backup-kluizen worden nog steeds ondersteund en is het mogelijk te[gebruik van Azure PowerShell toocreate Backup-kluizen](./backup-client-automation-classic.md#create-a-backup-vault). Microsoft raadt echter aan dat u Recovery Services-kluizen voor alle implementaties maken omdat toekomstige verbeteringen tooRecovery Services-kluizen, alleen van toepassing.


Deze afbeelding ziet u Hallo relaties tussen Hallo entiteiten met verschillende Azure Backup: ![Azure Backup-entiteiten en relaties](./media/backup-azure-vms-prepare/vault-policy-vm.png)



## <a name="network-connectivity"></a>Netwerkverbinding
In de volgorde toomanage Hallo VM momentopnamen Hallo Backup-extensie moet connectiviteit toohello Azure openbare IP-adressen. Zonder Hallo juiste verbinding met Internet mislukt Hallo virtuele machine HTTP-aanvragen time-out en Hallo back-up. Als uw implementatie beschikt over toegangsbeperkingen (via een netwerkbeveiligingsgroep (NSG), bijvoorbeeld), kies een van deze opties voor het ontwikkelen van een duidelijke pad voor de back-verkeer:

* [Geaccepteerde hello Azure datacenter IP-adresbereiken](http://www.microsoft.com/en-us/download/details.aspx?id=41653) -Zie Hallo-artikel voor instructies over hoe toowhitelist Hallo IP-adressen.
* Implementeer een HTTP-proxyserver voor het routeren van verkeer.

Wanneer u beslist welke optie toouse, zijn Hallo verschillen tussen beheerbaarheid, gedetailleerde controle en kosten.

| Optie | Voordelen | Nadelen |
| --- | --- | --- |
| Whitelist IP-adresbereiken |Er zijn geen extra kosten.<br><br>Gebruik voor toegang tot te openen in een NSG, Hallo <i>Set AzureNetworkSecurityRule</i> cmdlet. |Complexe toomanage als Hallo van invloed op IP-adresbereiken wijzigen gedurende een bepaalde periode.<br><br>Biedt toegang tot toohello geheel van Azure en niet alleen de opslag. |
| HTTP-proxy |Gedetailleerde controle in Hallo proxy over Hallo opslag URL's toegestaan. gedetailleerde controle toosetup in Hallo-proxy https://\*.blob.core.windows.net/\* URL patroon moet toobe wilt plaatsen. alleen Hallo storage-account die wordt gebruikt door de virtuele machine, Hallo toowhitelist https://\<storageAccount\>.blob.core.windows.net/\* URL patroon moet toobe wilt plaatsen. <br>Één punt Internet toegang tooVMs.<br>Geen onderwerp tooAzure IP-adreswijzigingen. |Extra kosten voor het uitvoeren van een virtuele machine met Hallo proxysoftware. |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a>Geaccepteerde hello Azure datacenter IP-adresbereiken
Raadpleeg Hallo toowhitelist hello Azure datacenter IP-adresbereiken [Azure-website](http://www.microsoft.com/en-us/download/details.aspx?id=41653) voor meer informatie over het Hallo-IP-adresbereiken en instructies.

### <a name="using-an-http-proxy-for-vm-backups"></a>Met behulp van een HTTP-proxy voor VM-back-ups
Wanneer een back-up van een VM, verzendt Hallo Backup-extensie op Hallo VM Hallo momentopname management opdrachten tooAzure opslag met een HTTPS-API. Hallo Backup-extensie-verkeer via Hallo HTTP-proxy te routeren omdat dit de enige onderdeel Hallo geconfigureerd voor toegang tot toohello openbare Internet.

> [!NOTE]
> Er is geen aanbeveling voor Hallo proxysoftware die moet worden gebruikt. Zorg ervoor dat u kiest een proxy die uitgaande gebruikerspad heeft en dit is compatibel met de onderstaande Hallo configuratiestappen. Zorg ervoor dat de procedure van derden Hallo proxy-instellingen niet wijzigen
>
>

Hallo voorbeeld in onderstaande afbeelding ziet u drie Hallo-configuratiestappen nodig toouse een HTTP-proxy:

* App VM routes die alle HTTP-verkeer voor gebonden Hallo Internet via Proxy VM.
* Proxy VM zorgt ervoor dat binnenkomend verkeer van virtuele machines in het virtuele netwerk Hallo.
* Hallo Netwerkbeveiligingsgroep (NSG) met de naam NSF-lockdown moet een beveiliging regel waardoor uitgaand internetverkeer van Proxy VM.

![NSG met HTTP-proxy-implementatie-diagram](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

toouse een HTTP-proxy toocommunicating toohello openbare Internet, als volgt te werk:

#### <a name="step-1-configure-outgoing-network-connections"></a>Step 1. Uitgaande netwerkverbindingen configureren
###### <a name="for-windows-machines"></a>Voor Windows-machines
Hiermee wordt het instellen van proxyserver-configuratie voor Lokaal systeemaccount.

1. Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553)
2. Voer de volgende opdracht uit met verhoogde bevoegdheid om

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     Internet explorer-venster wordt geopend.
3. Ga tooTools -> Internet-opties -> verbindingen LAN-instellingen ->.
4. Controleer de proxy-instellingen voor systeem-account. Stel Proxy IP-adres en poort.
5. Sluit Internet Explorer.

Dit stelt een proxyconfiguratie voor alle computers en wordt gebruikt voor alle uitgaande HTTP/HTTPS-verkeer.

Als u hebt een proxyserver ingesteld op het huidige gebruikersaccount (niet een lokaal systeemaccount), gebruikt u Hallo na script tooapply ze tooSYSTEMACCOUNT:

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> Als u '(407) proxyverificatie is vereist' in het logboek voor proxy server ziet, Controleer dat de verificatie van uw correct is ingesteld.
>
>

###### <a name="for-linux-machines"></a>Voor Linux-machines
Hallo volgende regel toohello toevoegen ```/etc/environment``` bestand:

```
http_proxy=http://<proxy IP>:<proxy port>
```

Toevoegen van de volgende regels toohello Hallo ```/etc/waagent.conf``` bestand:

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-hello-proxy-server"></a>Stap 2. Binnenkomende verbindingen toestaan op Hallo proxyserver:
1. Open Windows Firewall op Hallo proxy-server. Hallo gemakkelijkste manier tooaccess Hallo firewall is toosearch voor Windows Firewall met geavanceerde beveiliging.

    ![Hallo Firewall openen](./media/backup-azure-vms-prepare/firewall-01.png)
2. In het dialoogvenster Hallo Windows Firewall met de rechtermuisknop op **regels voor binnenkomende verbindingen** en klik op **nieuwe regel...** .

    ![Een nieuwe regel maken](./media/backup-azure-vms-prepare/firewall-02.png)
3. In Hallo **nieuwe Wizard regel voor binnenkomende**, kies Hallo **aangepaste** optie voor Hallo **regeltype** en klik op **volgende**.
4. Op Hallo pagina tooselect hello **programma**, kies **alle programma's** en klik op **volgende**.
5. Op Hallo **protocollen en poorten** pagina, Voer Hallo volgende informatie en klik op **volgende**:

    ![Een nieuwe regel maken](./media/backup-azure-vms-prepare/firewall-03.png)

   * voor *protocoltype* kiezen *TCP*
   * voor *lokale poort* kiezen *bepaalde poorten*, opgeven in onderstaande Hallo veld Hallo ```<Proxy Port>``` die is geconfigureerd.
   * voor *externe poort* Selecteer *alle poorten*

     Voor Hallo rest van de wizard hello, klik op alle Hallo manier toohello einde en geef een naam op voor deze regel.

#### <a name="step-3-add-an-exception-rule-toohello-nsg"></a>Stap 3. Een uitzondering regel toohello NSG toevoegen:
Voer Hallo volgende opdracht in een Azure PowerShell-opdrachtprompt:

Hallo volgende opdracht wordt een uitzondering toohello NSG toegevoegd. Deze uitzondering kan TCP-verkeer vanaf een willekeurige poort op 10.0.0.5 tooany internetadres op poort 80 (HTTP) of 443 (HTTPS). Als u een specifieke poort in nodig Hallo openbare Internet worden ervoor tooadd die poort toohello ```-DestinationPortRange``` ook.

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```

*Zorg ervoor dat u Hallo namen in Hallo voorbeeld door Hallo details juiste tooyour implementatie vervangen.*

## <a name="vm-agent"></a>VM-agent
Voordat u kunt back-up hello Azure virtuele machine, moet u ervoor zorgen dat hello Azure VM-agent correct is geïnstalleerd op Hallo virtuele machine. Aangezien Hallo VM-agent is een optioneel onderdeel Hallo hoelang Hallo van virtuele machine wordt gemaakt, zorg ervoor dat het selectievakje Hallo voor Hallo VM-agent is ingeschakeld voordat Hallo virtuele machine is ingericht.

### <a name="manual-installation-and-update"></a>Handmatige installatie en bijwerken
Hallo VM-agent is al aanwezig in virtuele machines die zijn gemaakt van hello Azure-galerie. Virtuele machines die worden gemigreerd van lokale datacenters zou echter geen Hallo VM-agent is geïnstalleerd. Voor deze virtuele machines moet Hallo VM-agent toobe expliciet worden geïnstalleerd. Lees meer over [installeren Hallo VM-agent op een bestaande virtuele machine](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).

| **Bewerking** | **Windows** | **Linux** |
| --- | --- | --- |
| Hallo VM-agent installeren |<li>Download en installeer Hallo [agent-MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). U moet Administrator-bevoegdheden toocomplete Hallo installatie. <li>[Werk Hallo VM eigenschap](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate die Hallo agent is geïnstalleerd. |<li> Meest recente Hallo installeren [Linux-agent](https://github.com/Azure/WALinuxAgent) vanuit GitHub. U moet Administrator-bevoegdheden toocomplete Hallo installatie. <li> [Werk Hallo VM eigenschap](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate die Hallo agent is geïnstalleerd. |
| Hallo VM-agent bijwerken |Bijwerken Hallo VM-agent is net zo eenvoudig als opnieuw geïnstalleerd Hallo [binaire bestanden voor VM-agent](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br><br>Zorg ervoor dat er geen back-upbewerking wordt uitgevoerd terwijl Hallo VM-agent wordt bijgewerkt. |Volg de instructies Hallo op [Hallo Linux VM-agent bijwerken ](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). <br><br>Zorg ervoor dat er geen back-upbewerking wordt uitgevoerd terwijl Hallo VM-agent wordt bijgewerkt. |
| Hallo VM-agent-installatie valideren |<li>Navigeer toohello *C:\WindowsAzure\Packages* map in hello Azure VM. <li>U moet Hallo WaAppAgent.exe bestand aanwezig is.<li> Met de rechtermuisknop op het Hallo-bestand, gaat u te**eigenschappen**, en selecteer vervolgens Hallo **Details** tabblad Hallo productversie veld moet 2.6.1198.718 of hoger. |N.v.t. |

Meer informatie over Hallo [VM-agent](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) en [hoe tooinstall het](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/).

### <a name="backup-extension"></a>Backup-extensie
tooback hello virtuele machine hello Azure Backup-service installeert een extensie toohello VM-agent. upgrades naadloos Hello Azure Backup-service en -patches Hallo Backup-extensie zonder tussenkomst van de extra kosten voor gebruikers.

Hallo Backup-extensie is geïnstalleerd als Hallo VM wordt uitgevoerd. Een actieve virtuele machine biedt ook Hallo grootste kans een toepassingsconsistente herstelpunt. Echter hello Azure Backup-service tooback up Hallo VM--wordt voortgezet zelfs als deze is uitgeschakeld en Hallo-extensie kan niet worden geïnstalleerd (aka Offline VM). In dit geval Hallo herstelpunt zich *crashconsistent* zoals hierboven wordt beschreven.

## <a name="questions"></a>Vragen?
Als u vragen hebt of als er een functie die u toosee opgenomen wilt, [Stuur ons feedback](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Volgende stappen
Nu u uw omgeving voor back-ups van uw virtuele machine hebt voorbereid, de volgende logische stap is toocreate een back-up. Hallo planning artikel biedt gedetailleerde informatie over back-ups van virtuele machines.

* [Back-up van virtuele machines](backup-azure-vms.md)
* [Uw VM-back-infrastructuur plannen](backup-azure-vms-introduction.md)
* [Back-ups van virtuele machine beheren](backup-azure-manage-vms.md)
