---
title: 'Azure Backup: Tooback van virtuele machines voorbereiden | Microsoft Docs'
description: Zorg ervoor dat uw omgeving is voorbereid voor de back-ups van virtuele machines in Azure.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: back-ups; een back-up;
ms.assetid: e87e8db2-b4d9-40e1-a481-1aa560c03395
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 5c3a41b5d3bd56e62ca5f207442867913aa99816
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-resource-manager-deployed-virtual-machines"></a>Voorbereiden van uw omgeving tooback van Resource Manager geïmplementeerde virtuele machines
> [!div class="op_single_selector"]
> * [Resource Manager-model](backup-azure-arm-vms-prepare.md)
> * [Klassieke model](backup-azure-vms-prepare.md)
>
>

In dit artikel bevat Hallo stappen voor het voorbereiden van uw omgeving tooback een Resource Manager geïmplementeerde virtuele machine (VM). Hallo stappen in de procedures hello gebruiken hello Azure-portal.  

Hello Azure Backup-service heeft twee soorten kluizen (back-up kluizen en recovery services-kluizen) voor het beveiligen van uw virtuele machines. Een back-upkluis beveiligt virtuele machines die zijn geïmplementeerd met behulp van Hallo klassieke implementatiemodel. Een recovery services-kluis beveiligt **zowel klassieke geïmplementeerd of Resource Manager geïmplementeerde VM's**. U moet een Recovery Services-kluis tooprotect een Resource Manager geïmplementeerde VM.

> [!NOTE]
> Azure heeft twee implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md). Zie [voorbereiden van uw omgeving tooback van virtuele machines in Azure](backup-azure-vms-prepare.md) voor meer informatie over het werken met Classic deployment model virtuele machines.
>
>

Voordat u kunt beveiligen of back-up van een Resource Manager geïmplementeerde virtuele machine (VM), zorg er dan voor dat deze vereisten bestaan:

* Een recovery services-kluis maken (of een bestaande recovery services-kluis identificeren) *in Hallo dezelfde locatie als uw VM*.
* Selecteer een scenario, Hallo back-upbeleid definiëren en tooprotect items definiëren.
* Controleer de installatie van Hallo van VM-Agent op de virtuele machine.
* Controleer de netwerkverbinding
* Voor virtuele Linux-machines, als u wilt dat toocustomize uw back-omgeving voor de toepassing consistente back-ups Volg Hallo [stappen tooconfigure vooraf momentopname en na een momentopname van scripts](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)

Als u deze voorwaarden al bestaat in uw omgeving en doorgaan toohello [Back-up van uw virtuele machines artikel](backup-azure-vms.md). Als u nodig hebt tooset of, een van deze vereisten controleren, begeleidt in dit artikel u bij Hallo stappen tooprepare of de vereiste.

##<a name="supported-operating-system-for-backup"></a>Ondersteund besturingssysteem voor back-up
 * **Linux**: Azure Backup ondersteunt [een lijst met distributies die zijn goedgekeurd door Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), met uitzondering van Core OS Linux. _Andere Bring-Your-eigenaar-Linux-distributies ook mogelijk werken zolang Hallo VM-agent beschikbaar op Hallo virtuele machine is en ondersteuning voor Python bestaat. We tekent echter niet de distributies voor back-up._
 * **Windows Server**: versies ouder dan Windows Server 2008 R2 worden niet ondersteund.

## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>Beperkingen bij een back-up en herstellen van een virtuele machine
Voordat u uw omgeving hebt voorbereid, moet u begrijpen Hallo beperkingen.

* Back-ups van virtuele machines met meer dan 16 gegevensschijven wordt niet ondersteund.
* Back-ups van virtuele machines met gegevens groter zijn dan 1023GB schijfgrootten wordt niet ondersteund.
* Back-ups van virtuele machines met een gereserveerd IP-adres en er is geen gedefinieerde eindpunt wordt niet ondersteund.
* Back-up van virtuele machines die zijn versleuteld met NET BEK wordt niet ondersteund. Back-up van Linux virtuele machines die zijn versleuteld met behulp van versleuteling LUKS wordt niet ondersteund.
* Back-up van virtuele machines op schaal bestandsserver configuratie wordt niet aanbevolen.
* Back-upgegevens bevat geen tooVM van netwerk gekoppelde stations die zijn gekoppeld.
* Een bestaande virtuele machine kan tijdens het herstel niet worden vervangen. Als u toorestore Hallo VM probeert wanneer Hallo VM bestaat, mislukt de herstelbewerking Hallo.
* Regio-overschrijdende back-up en herstel worden niet ondersteund.
* U kunt back-ups van virtuele machines in alle openbare gebieden van Azure (Zie Hallo [controlelijst](https://azure.microsoft.com/regions/#services) van ondersteunde regio's). Als Hallo regio die u zoekt niet vandaag ondersteund wordt, wordt deze niet weergegeven in de vervolgkeuzelijst Hallo tijdens het maken van de kluis.
* Herstellen van een domeincontroller wordt (DC) VM die deel uitmaakt van een multi-DC-configuratie alleen ondersteund door PowerShell. Lees meer over [een multi-DC-domeincontroller terugzetten](backup-azure-restore-vms.md#restoring-domain-controller-vms).
* Herstellen van virtuele machines waarvoor speciale netwerkconfiguraties na hello wordt alleen ondersteund door PowerShell. Virtuele machines die zijn gemaakt met behulp van Hallo terugzetten werkstroom in Hallo UI geen deze netwerkconfiguraties nadat Hallo restore-bewerking voltooid is. toolearn meer, Zie [herstellen van virtuele machines met speciale netwerkconfiguraties](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).
  * Virtuele machines onder een load balancer-configuratie (intern en extern)
  * Virtuele machines met meerdere gereserveerde IP-adressen
  * Virtuele machines met meerdere netwerkadapters

## <a name="create-a-recovery-services-vault-for-a-vm"></a>Een Recovery Services-kluis voor een VM maken
Een recovery services-kluis is een entiteit waarmee Hallo back-ups en herstelpunten die zijn gemaakt na verloop van tijd worden opgeslagen. Hallo recovery services-kluis bevat ook Hallo back-upbeleid gekoppeld Hallo beveiligde virtuele machines.

toocreate een recovery services-kluis:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Klik op het menu Hub Hallo **Bladeren** en typt u in de lijst met resources Hallo **Recovery Services**. Als u te typen begint, Hallo lijst gefilterd op basis van uw invoer. Klik op **Recovery Services-kluis**.

    ![Klik op de knop Bladeren Hallo en typ Recovery Services. Wanneer er Hallo Recovery Services-kluis optie, klikt u erop tooopen Hallo Recovery Services-blade kluis.](./media/backup-azure-arm-vms-prepare/browse-to-rs-vaults-updated.png) <br/>

    Hallo-lijst met Recovery Services-kluizen wordt weergegeven.
3. Op Hallo **Recovery Services-kluizen** menu, klikt u op **toevoegen**.

    ![Een Recovery Services-kluis maken, stap 2](./media/backup-azure-arm-vms-prepare/rs-vault-menu.png)

    Hallo Recovery Services vault blade wordt geopend, waarin u wordt gevraagd tooprovide een **naam**, **abonnement**, **resourcegroep**, en **locatie**.

    ![Een Recovery Services-kluis maken, stap 5](./media/backup-azure-arm-vms-prepare/rs-vault-attributes.png)
4. Voor **naam**, voer een beschrijvende naam tooidentify Hallo-kluis. de naam van de Hallo moet toobe unieke voor hello Azure-abonnement. Typ een naam die tussen 2 en 50 tekens bevat. De naam moet beginnen met een letter en mag alleen letters, cijfers en afbreekstreepjes bevatten.
5. Klik op **abonnement** toosee Hallo lijst met beschikbare abonnementen. Als u niet zeker weet welk abonnement toouse Hallo standaard gebruiken (of voorgestelde) abonnement. Er zijn alleen meerdere mogelijkheden als uw organisatieaccount is gekoppeld aan meerdere Azure-abonnementen.
6. Klik op **resourcegroep** toosee Hallo beschikbare lijst met resourcegroepen, of klik op **nieuw** toocreate een nieuwe resourcegroep. Zie [Overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) voor meer informatie over resourcegroepen.
7. Klik op **locatie** tooselect Hallo geografische regio voor Hallo kluis. Hallo kluis **moet** liggen Hallo dezelfde regio bevinden als Hallo virtuele machines die u tooprotect wilt.

   > [!IMPORTANT]
   > Als u niet Hallo-locatie waar uw VM zich bevindt weet, sluit buiten het dialoogvenster voor het Hallo-kluis maken en ga toohello lijst met virtuele Machines in Hallo-portal. Als u virtuele machines in meerdere regio's hebt, moet u toocreate in elke regio een Recovery Services-kluis. Hallo-kluis maken in de eerste locatie Hallo voordat u de volgende locatie toohello doorgaat. Er is geen noodzaak toospecify-opslagaccounts toostore Hallo back-upgegevens--Hallo Recovery Services-kluis en hello Azure Backup-service niet verwerken dit automatisch.
   >
   >

8. Klik op **Create**. Het kan even duren voordat Hallo Recovery Services-kluis toobe gemaakt. Hallo statusmeldingen Hallo rechtsboven in de portal Hallo bewaken. Zodra de kluis is gemaakt, wordt deze weergegeven in de lijst met Recovery Services-kluizen Hallo. Als u uw kluis niet ziet, klikt u op **vernieuwen** naar

    ![Lijst met back-upkluizen](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    Nu u uw kluis hebt gemaakt, kunt u nagaan hoe tooset Hallo storage-replicatie.

## <a name="set-storage-replication"></a>Opslagreplicatie instellen
optie voor opslagreplicatie Hallo kunt u toochoose tussen geografisch redundante opslag en lokaal redundante opslag. Uw kluis heeft standaard geografisch redundante opslag. Laat Hallo optie set toogeo redundante opslag als dit uw primaire back-up. Kies lokaal redundante opslag als u een goedkopere optie wilt die niet zo duurzaam is.

replicatie-instelling voor tooedit Hallo opslag

1. Op Hallo **Recovery Services-kluizen** blade, selecteer uw kluis.
    Als u uw kluis op, Hallo blade instellingen (*die Hallo-naam van de kluis Hallo Hallo boven heeft*) en Hallo kluis beschrijft blade wordt geopend.

    ![Kies uw kluis uit Hallo-lijst met back-upkluizen](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. Op Hallo **instellingen** blade gebruik Hallo verticale schuifregelaar tooscroll omlaag toohello **beheren** sectie. Klik op **back-upinfrastructuur** tooopen de blade. In Hallo **algemene** sectie Klik **back-upconfiguratie** tooopen de blade. Op Hallo **back-upconfiguratie** blade Hallo optie voor opslagreplicatie voor uw kluis kiezen. Uw kluis heeft standaard geografisch redundante opslag. Als u Hallo opslagreplicatietype wijzigt, klikt u op **opslaan**.

    ![Lijst met back-upkluizen](./media/backup-azure-arm-vms-prepare/full-blade.png)

     Als Azure uw primaire eindpunt is voor back-upopslag, blijf dan geografisch redundante opslag gebruiken. Als u van Azure als het eindpunt van een niet-primaire back-upopslag gebruikmaakt, kiest u lokaal redundante opslag. Lees meer over [geografisch redundante](../storage/common/storage-redundancy.md#geo-redundant-storage) en [lokaal redundante](../storage/common/storage-redundancy.md#locally-redundant-storage) opslagopties in Hallo [overzicht van Azure Storage-replicatie](../storage/common/storage-redundancy.md).
    Nadat u hebt gekozen Hallo opslagoptie voor uw kluis, bent u klaar tooassociate Hallo VM met Hallo kluis. toobegin Hallo-koppeling, die u moet detecteren en registreren Hallo van virtuele machines in Azure.

## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a>Selecteer een back-doel, beleid instellen en definiëren van items tooprotect
Voordat u een virtuele machine met een kluis registreert, Voer Hallo detectie proces tooensure dat nieuwe virtuele machines die zijn toegevoegd aan de toohello abonnement worden geïdentificeerd. Hallo wordt een query uitgevoerd Azure voor Hallo lijst met virtuele machines in het Hallo-abonnement, samen met aanvullende informatie zoals Hallo cloudservicenaam en Hallo regio. In hello Azure-portal verwijst scenario toowhat u tooput gaat in Hallo recovery services-kluis. Beleid is Hallo planning voor hoe vaak en wanneer de herstelpunten worden gemaakt. Het beleid bevat ook Hallo bewaartermijn voor Hallo herstelpunten.

1. Als u al een Recovery Services-kluis openen, gaat u verder toostep 2. Als u geen een Recovery Services-kluis openen, opent u Hallo [Azure-portal](https://portal.azure.com/) en klik op het menu Hub Hallo **meer services**.

   * Typ in de lijst met resources Hallo **Recovery Services**.
   * Als u te typen begint, Hallo lijst gefilterd op basis van uw invoer. Wanneer **Recovery Services-kluizen** wordt weergegeven, klikt u erop.

     ![Een Recovery Services-kluis maken, stap 1](./media/backup-azure-arm-vms-prepare/browse-to-rs-vaults-updated.png) <br/>

     Hallo-lijst met Recovery Services-kluizen wordt weergegeven. Als er geen kluizen in uw abonnement, wordt deze lijst niet leeg zijn.

    ![Weergave van Hallo Recovery Services-kluizen lijst](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

   * Selecteer in Hallo lijst met Recovery Services-kluizen een kluis tooopen het dashboard.

     de blade instellingen Hallo en Hallo vault dashboard voor Hallo gekozen kluis wordt geopend.

     ![Blade Kluis openen](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)
2. Klik op het Hallo-kluis dashboard menu **back-up** blade tooopen Hallo-back-up.

    ![Blade Back-up openen](./media/backup-azure-arm-vms-prepare/backup-button.png)

    Hallo back-up- en back-updoel blades geopend.

    ![Blade Scenario openen](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)

3. Stel op de blade back-updoel hello, **waar wordt uw workload uitgevoerd** tooAzure en **wat wilt u wilt toobackup** tooVirtual machine en klik vervolgens op **OK**.

    Dit registreert Hallo VM-extensie met Hallo kluis. Hallo back-updoel blade wordt gesloten en Hallo **back-up maken van beleid** blade wordt geopend.

    ![Blade Scenario openen](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)
4. Selecteer op de blade van Hallo back-up Hallo back-upbeleid gewenste tooapply toohello kluis.

    ![Back-upbeleid selecteren](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    Hallo-details van het standaardbeleid Hallo worden vermeld in de vervolgkeuzelijst Hallo. Als u wilt dat een nieuw beleid toocreate, selecteert u **nieuw** uit de vervolgkeuzelijst Hallo. Zie [Een back-upbeleid definiëren](backup-azure-vms-first-look-arm.md#defining-a-backup-policy) voor instructies over het definiëren van een back-upbeleid.
    Klik op **OK** tooassociate Hallo back-upbeleid met Hallo kluis.

    back-up beleid blade wordt gesloten en Hallo Hallo **virtuele machines selecteren** blade wordt geopend.
5. In Hallo **virtuele machines selecteren** blade kiezen Hallo virtuele machines tooassociate Hello opgegeven beleid en klik op **OK**.

    ![Workload selecteren](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    Hallo geselecteerde virtuele machine wordt gevalideerd. Als u Hallo virtuele machines dat u verwacht dat toosee niet ziet, controleert u of ze in dezelfde Azure-locatie als Hallo Recovery Services-kluis en nog niet zijn beveiligd in een andere kluis Hallo bestaan. Hallo-locatie van Hallo die Recovery Services-kluis wordt weergegeven op het kluisdashboard Hallo.

6. Nu dat u alle instellingen voor Hallo kluis hebt gedefinieerd, in Hallo blade back-up klikt u op **back-up inschakelen**. Hiermee implementeert u Hallo beleid toohello kluis en Hallo virtuele machines. Dit maakt geen Hallo eerste herstelpunt voor Hallo virtuele machine.

    ![Back-up inschakelen](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

Nadat de Hallo back-up is ingeschakeld, wordt uw back-upbeleid uitgevoerd volgens schema. Als u een back-uptaak op aanvraag tooback van Hallo virtuele machines toogenerate nu, Zie [Triggering Hallo back-uptaak](./backup-azure-arm-vms.md#triggering-the-backup-job).

Als u problemen met de registratie van Hallo virtuele machine hebt, raadpleegt u Hallo volgende informatie op Hallo VM-Agent installeren en op de netwerkverbinding. U nodig Hallo volgende informatie als u virtuele machines die zijn gemaakt in Azure beveiligt waarschijnlijk niet. Maar als u uw virtuele machines in Azure hebt gemigreerd, vervolgens moet dat u goed Hallo VM-agent en dat de virtuele machine met de Hallo virtueel netwerk communiceren kan hebt geïnstalleerd.

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Hallo VM-Agent installeren op Hallo virtuele machine
Hello Azure VM-Agent moet worden geïnstalleerd op Hallo voor Hallo back-up extensie toowork virtuele Azure-machine. Hallo VM-Agent is al aanwezig op Hallo virtuele machine als uw virtuele machine is gemaakt vanuit hello Azure-galerie. Deze informatie wordt verstrekt voor Hallo situaties waarin u *niet* met behulp van een virtuele machine gemaakt op basis van hello Azure-galerie - bijvoorbeeld u een virtuele machine gemigreerd vanuit een on-premises datacenter. In dat geval moet Hallo VM-Agent toobe op volgorde tooprotect Hallo virtuele machine geïnstalleerd. Meer informatie over Hallo [VM-Agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux).

Als u een back-up hello Azure VM problemen ondervindt, Controleer of de Azure VM-Agent Hallo juist is geïnstalleerd op Hallo virtuele machine (Zie onderstaande tabel voor Hallo). Hallo volgende tabel bevat aanvullende informatie over Hallo VM-Agent voor Windows en Linux-machines.

| **Bewerking** | **Windows** | **Linux** |
| --- | --- | --- |
| Hallo VM-Agent installeren |Download en installeer Hallo [agent-MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). U moet Administrator-bevoegdheden toocomplete Hallo installatie. |<li> Meest recente Hallo installeren [Linux-agent](../virtual-machines/linux/agent-user-guide.md). U moet Administrator-bevoegdheden toocomplete Hallo installatie. Het is raadzaam om de installatie van agent van uw opslagplaats voor distributie. We **wordt niet aanbevolen** installeren Linux VM-agent rechtstreeks vanuit github.  |
| Hallo VM-Agent bijwerken |Bijwerken Hallo VM-Agent is net zo eenvoudig als opnieuw geïnstalleerd Hallo [binaire bestanden voor VM-Agent](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br>Zorg ervoor dat er geen back-upbewerking wordt uitgevoerd terwijl Hallo VM-agent wordt bijgewerkt. |Volg de instructies Hallo op [Linux VM-Agent bijwerken Hallo](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Het is raadzaam om de agent van uw opslagplaats distributiepunten bijwerken. We **wordt niet aanbevolen** bijwerken Linux VM-agent rechtstreeks vanuit github.<br>Zorg ervoor dat er geen back-upbewerking wordt uitgevoerd tijdens het Hallo die VM-Agent wordt bijgewerkt. |
| Hallo VM-Agent-installatie valideren |<li>Navigeer toohello *C:\WindowsAzure\Packages* map in hello Azure VM. <li>U moet Hallo WaAppAgent.exe bestand aanwezig is.<li> Met de rechtermuisknop op het Hallo-bestand, gaat u te**eigenschappen**, en selecteer vervolgens Hallo **Details** tabblad Hallo productversie veld moet 2.6.1198.718 of hoger. |N.v.t. |

### <a name="backup-extension"></a>Backup-extensie
Hallo die VM-Agent is geïnstalleerd op Hallo virtuele machine, hello Azure Backup-service wordt eenmaal Hallo Backup-extensie toohello VM-Agent geïnstalleerd. upgrades naadloos Hello Azure Backup-service en -patches Hallo Backup-extensie.

Hallo Backup-extensie is geïnstalleerd door Hallo Backup-service al dan niet Hallo VM wordt uitgevoerd. Een actieve virtuele machine biedt de grootste kans op Hallo van het ophalen van een toepassingsconsistente herstelpunt. Hello Azure Backup-service blijft echter tooback up Hallo VM, zelfs als deze is uitgeschakeld en Hallo-extensie kan niet worden geïnstalleerd. Dit wordt Offline-VM genoemd. In dit geval Hallo herstelpunt zich *crashconsistent*.

## <a name="network-connectivity"></a>Netwerkverbinding
In de volgorde toomanage Hallo VM momentopnamen Hallo Backup-extensie moet connectiviteit toohello Azure openbare IP-adressen. Zonder Hallo juiste verbinding met Internet mislukt Hallo virtuele machine HTTP-aanvragen time-out en Hallo back-up. Als uw implementatie beschikt over toegangsbeperkingen (via een netwerkbeveiligingsgroep (NSG), bijvoorbeeld), kies een van deze opties voor het ontwikkelen van een duidelijke pad voor de back-verkeer:

* [Geaccepteerde hello Azure datacenter IP-adresbereiken](http://www.microsoft.com/en-us/download/details.aspx?id=41653) -Zie Hallo-artikel voor instructies over hoe toowhitelist Hallo IP-adressen.
* Implementeer een HTTP-proxyserver voor het routeren van verkeer.

Wanneer u beslist welke optie toouse, zijn Hallo verschillen tussen beheerbaarheid, gedetailleerde controle en kosten.

| Optie | Voordelen | Nadelen |
| --- | --- | --- |
| Whitelist IP-adresbereiken |Er zijn geen extra kosten.<br><br>Gebruik voor toegang tot te openen in een NSG, Hallo <i>Set AzureNetworkSecurityRule</i> cmdlet. |Complexe toomanage als Hallo van invloed op IP-adresbereiken wijzigen gedurende een bepaalde periode.<br><br>Biedt toegang tot toohello geheel van Azure en niet alleen de opslag. |
| HTTP-proxy |Gedetailleerde controle in Hallo proxy over Hallo opslag URL's toegestaan.<br>Één punt Internet toegang tooVMs.<br>Geen onderwerp tooAzure IP-adreswijzigingen. |Extra kosten voor het uitvoeren van een virtuele machine met Hallo proxysoftware. |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a>Geaccepteerde hello Azure datacenter IP-adresbereiken
Raadpleeg Hallo toowhitelist hello Azure datacenter IP-adresbereiken [Azure-website](http://www.microsoft.com/en-us/download/details.aspx?id=41653) voor meer informatie over het Hallo-IP-adresbereiken en instructies.

### <a name="using-an-http-proxy-for-vm-backups"></a>Met behulp van een HTTP-proxy voor VM-back-ups
Wanneer een back-up van een VM, verzendt Hallo Backup-extensie op Hallo VM Hallo momentopname management opdrachten tooAzure opslag met een HTTPS-API. Hallo Backup-extensie-verkeer via Hallo HTTP-proxy te routeren omdat dit de enige onderdeel Hallo geconfigureerd voor toegang tot toohello openbare Internet.

> [!NOTE]
> Er is geen aanbeveling voor Hallo proxysoftware die moet worden gebruikt. Zorg ervoor dat u kiest een proxy die compatibel is met de onderstaande Hallo configuratiestappen.
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


*Deze stappen worden specifieke namen en waarden voor dit voorbeeld gebruiken. Gebruik Hallo namen en waarden voor uw implementatie wanneer u invoert, of knippen en plakken van gegevens in uw code.*

Nu u weet dat u verbinding met het netwerk hebt, bent u klaar tooback van uw virtuele machine. Zie [Back-up van Resource Manager geïmplementeerde VM's](backup-azure-arm-vms.md).

## <a name="questions"></a>Vragen?
Als u vragen hebt of als er een functie die u toosee opgenomen wilt, [Stuur ons feedback](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Volgende stappen
Nu u uw omgeving voor back-ups van uw virtuele machine hebt voorbereid, de volgende logische stap is toocreate een back-up. Hallo planning artikel biedt gedetailleerde informatie over back-ups van virtuele machines.

* [Back-up van virtuele machines](backup-azure-vms.md)
* [Uw VM-back-infrastructuur plannen](backup-azure-vms-introduction.md)
* [Back-ups van virtuele machine beheren](backup-azure-manage-vms.md)
