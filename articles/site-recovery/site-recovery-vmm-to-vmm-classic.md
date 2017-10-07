---
title: aaaReplicate Hyper-V-machines in VMM tooa secundaire site (Azure classic) | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooreplicate Hyper-V-machines in VMM clouds tooa secundaire VMM-site met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a63acba3-8fb3-4926-aa29-b1e64a765681
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: fe551e1f741579044f540ea0e50a6e36d48133ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a>Hyper-V virtuele machines in VMM-clouds tooa secundaire VMM-site repliceren
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-vmm.md)
> * [Klassieke portal](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Hello Azure Site Recovery-service draagt bij tooyour zakelijke continuïteit en (BCDR) strategie voor noodherstel door organiseren replicatie, failovers en herstel van virtuele machines en fysieke servers. Machines kunnen gerepliceerde tooAzure of tooa secundaire on-premises datacenter zijn. Lees voor een snel overzicht [Wat is Azure Site Recovery?](site-recovery-overview.md)

## <a name="overview"></a>Overzicht
Dit artikel wordt beschreven hoe tooreplicate Hyper-V virtuele machines op Hyper-V-hostservers die worden beheerd in VMM-clouds toosecondary VMM-site met Azure Site Recovery.

Hallo artikel bevat vereisten, ziet u hoe tooset van Site Recovery-kluis installeren hello Azure Site Recovery Provider op de bron en doel van de VMM-servers, Hallo-servers registreren in de kluis hello, Configureer beveiligingsinstellingen voor VMM-clouds en schakel vervolgens beveiliging voor Hyper-V-machines. Voltooien door failover toomake testen Hallo controleren of dat alles werkt zoals verwacht.

Eventuele opmerkingen of vragen plaatsen onderin Hallo van dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architecture"></a>Architectuur
Hallo afbeelding hieronder ziet u Hallo verschillende communicatiekanalen en poorten gebruikt door Azure Site Recovery voor de orchestration- en replicatie

![E2E-topologie](./media/site-recovery-vmm-to-vmm-classic/e2e-topology.png)

## <a name="before-you-start"></a>Voordat u begint
Zorg ervoor dat u deze vereisten hebt voldaan:

| **Vereisten** | **Details** |
| --- | --- |
| **Azure** |U hebt een [Microsoft Azure](https://azure.microsoft.com/)-account nodig. U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/). [Meer informatie](https://azure.microsoft.com/pricing/details/site-recovery/) over prijzen voor Site Recovery. |
| **VMM** |U moet ten minste één VMM-server.<br/><br/>Hallo VMM-server waarop ten minste System Center 2012 SP1 met Hallo meest recente cumulatieve updates.<br/><br/>Als u wilt dat tooset van de beveiliging met één VMM-server, moet u ten minste twee clouds die zijn geconfigureerd op Hallo-server.<br/><br/>Als u toodeploy beveiliging met twee VMM-servers wilt, elke server moet ten minste één cloud zijn geconfigureerd op Hallo primaire VMM-server u wilt dat tooprotect en één cloud zijn geconfigureerd op de secundaire VMM-server Hallo gewenste toouse voor beveiliging en herstel<br/><br/>Alle VMM-clouds moeten Hyper-V-mogelijkheidsprofiel voor het Hallo ingesteld hebben.<br/><br/>Hallo-broncloud die u wilt dat tooprotect moet een of meer VMM-hostgroepen bevatten. |
| **Hyper-V** |U moet een of meer Hyper-V-host-servers in Hallo primaire en secundaire VMM-hostgroepen en een of meer virtuele machines op elke Hyper-V-hostserver.<br/><br/>Hallo host- en Hyper-V-servers moeten worden uitgevoerd ten minste Windows Server 2012 met Hallo Hyper-V-rol en hebben Hallo nieuwste updates zijn geïnstalleerd.<br/><br/>Een Hyper-V-server met VM's die wilt u dat tooprotect moet zich bevinden in een VMM-cloud.<br/><br/>Als u Hyper-V in een cluster uitvoert, houd er rekening mee dat clusterbroker niet automatisch gemaakt als u een statische IP-adressen gebaseerde cluster hebt. Moet u handmatig tooconfigure hello clusterbroker. [Meer informatie](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters) in het blog van Aidan Finn. |
| **Netwerktoewijzing** |U kunt configureren netwerk toewijzing toomake ervoor dat gerepliceerde virtuele machines zijn optimaal geplaatst op secundaire Hyper-V-hostservers na een failover en dat ze tooappropriate VM-netwerken verbinding kunnen maken. Als u geen netwerktoewijzing configureert, niet replica VMs verbonden tooany netwerk na een failover.<br/><br/>tooset up netwerktoewijzing tijdens de implementatie, zorg ervoor dat Hallo virtuele machines op Hallo bron Hyper-V-hostserver verbonden tooa VMM VM-netwerk. Dit netwerk moet gekoppelde tooa logisch netwerk dat is gekoppeld aan Hallo cloud. < br /<br/>Hallo doelcloud op Hallo secundaire VMM-server die u voor herstel gebruikt moet een bijbehorende VM-netwerk is geconfigureerd en deze op zijn beurt moet gekoppelde tooa logisch netwerk dat is gekoppeld aan de doelcloud Hallo overeenkomt. |
| **Toewijzing van opslag** |Standaard dat wanneer u een virtuele machine op een Hyper-V-host-server tooa doel Hyper-V-host bronserver, repliceert gerepliceerde gegevens worden opgeslagen in de standaardlocatie Hallo die opgegeven voor Hallo doel Hyper-V-host in Hyper-V-beheer. Voor meer controle over waar de gerepliceerde gegevens worden opgeslagen, kunt u de toewijzing van opslag configureren<br/><br/> tooconfigure opslag toewijzen, u nodig hebt tooset up opslagclassificaties op Hallo bron en doel van VMM-servers voordat u begint met implementeren. |

## <a name="step-1-create-a-site-recovery-vault"></a>Stap 1: Een Site Recovery-kluis maken
1. Meld u aan toohello [beheerportal](https://portal.azure.com) van Hallo VMM-server die u wilt tooregister.
2. Vouw **Data Services** > **Recovery Services** en klik op **Site Recovery-kluis**.
3. Klik op **Nieuw maken** > **Snelle invoer**.
4. In **naam**, voer een beschrijvende naam tooidentify Hallo-kluis.
5. In **regio** Selecteer Hallo geografische regio voor Hallo kluis. toocheck ondersteunde regio's Zie geografische beschikbaarheid in [Azure Site Recovery Pricing Details](http://go.microsoft.com/fwlink/?LinkId=389880).
6. Klik op **Kluis maken**.

    ![Kluis maken](./media/site-recovery-vmm-to-vmm-classic/create-vault.png)

Controle op Hallo statusbalk die Hallo-kluis is gemaakt. Hallo-kluis wordt weergegeven als **Active** op Hallo hoofdpagina Recovery Services.

## <a name="step-2-generate-a-vault-registration-key"></a>Stap 2: Een kluisregistratiesleutel genereren
Genereer een registratiesleutel in Hallo kluis. Nadat u hello Azure Site Recovery Provider downloaden en op Hallo VMM-server installeren, gebruikt u deze sleutel tooregister Hallo VMM-server in Hallo kluis.

1. In Hallo **Recovery Services** pagina, klikt u op Hallo kluis tooopen Hallo snel starten-pagina. Snel starten kan ook worden geopend op elk gewenst moment Hallo-pictogram.

    ![Pictogram Snel starten](./media/site-recovery-vmm-to-vmm-classic/quick-start-icon.png)
2. Selecteer in de vervolgkeuzelijst Hallo **tussen twee lokale VMM sites**.
3. In **VMM-Servers voorbereiden**, klikt u op **registratiesleutelbestand genereren**. Hallo-sleutelbestand wordt automatisch gegenereerd en is geldig tot 5 dagen nadat deze gegenereerd. Als u geen toegang Azure-portal Hallo van Hallo VMM-server tot moet u toocopy deze toohello bestandsserver.

    ![Registratiesleutel](./media/site-recovery-vmm-to-vmm-classic/register-key.png)

## <a name="step-3-install-hello-azure-site-recovery-provider"></a>Stap 3: Hello Azure Site Recovery Provider installeren
1. Op Hallo **Quick Start** pagina **VMM-servers voorbereiden**, klikt u op **Microsoft Azure Site Recovery Provider is downloaden voor installatie op VMM-servers** tooobtain Hallo laatste versie van Hallo Provider-installatiebestand.
2. Voer dit bestand op Hallo bron-VMM-server.

   > [!NOTE]
   > Als VMM is geïmplementeerd in een cluster en u Hallo Provider voor Hallo eerst installeert installeren op een actief knooppunt en Hallo installatie tooregister Hallo VMM-server in de kluis Hallo voltooien. Installeer vervolgens Hallo Provider op Hallo andere knooppunten. Opmerking: als u een Hallo provider u tooupgrade op alle knooppunten nodig upgrade uitvoert omdat ze alle moeten Hallo uitgevoerd dezelfde versie van Provider.
   >
   >
3. Hallo installatieprogramma heeft een paar **vooraf vereisten controleren** en aanvragen machtiging toostop Hallo VMM service toobegin Provider setup. Hallo VMM-Service wordt opnieuw opgestart nadat setup is voltooid. Als u installeert op gevraagd een VMM-cluster, u moet toostop Hallo Cluster-rol.
4. U kunt zich in **Microsoft Update** aanmelden voor updates. Met deze instelling worden ingeschakeld Provider-updates geïnstalleerd op basis van beleid voor tooyour Microsoft Update.

    ![Microsoft-updates](./media/site-recovery-vmm-to-vmm-classic/ms-update.png)
5. Hallo-installatielocatie is ingesteld, te**<SystemDrive>\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin**. Klik op Hallo installeren knop toostart Hallo Provider installeren.

    ![InstallLocation](./media/site-recovery-vmm-to-vmm-classic/install-location.png)
6. Klik na het Hallo-Provider is geïnstalleerd op **registreren** tooregister Hallo-server in Hallo kluis.

    ![InstallComplete](./media/site-recovery-vmm-to-vmm-classic/install-complete.png)
7. In **kluisnaam**, Controleer de naam van de Hallo van Hallo kluis in welke Hallo server wordt geregistreerd. Klik op *Volgende*.

    ![Serverregistratie](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
8. In **internetverbinding** opgeven hoe Hallo Provider die wordt uitgevoerd op Hallo VMM-server maakt verbinding toohello Internet. Selecteer **verbinding maken met bestaande proxyinstellingen** toouse Hallo standaardinstellingen voor internetverbindingen op Hallo-server geconfigureerd.

    ![Instellingen voor internet](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   * Als u wilt dat toouse een aangepaste proxy u moet instellen voordat u Hallo Provider installeert. Wanneer u aangepaste proxyinstellingen configureert wordt een test toocheck Hallo proxyverbinding uitgevoerd.
   * Als u een aangepaste proxy gebruikt, of als uw standaardproxy verificatie vereist, moet u tooenter Hallo proxy-gegevens, inclusief Hallo proxy-adres en poort.
   * Volgende URL's moeten toegankelijk zijn vanuit Hallo VMM-Server en Hyper-v-hosts Hallo
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * Hallo IP-adressen die worden beschreven mogen [Azure Datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653) en het protocol HTTPS (443). Hebt u IP-adresbereiken toowhite-lijst van hello Azure-regio die u van plan toouse en die van de VS-West bent.
   * Als u een aangepaste proxy gebruikt een VMM RunAs-account (DRAProxyAccount) wordt automatisch gemaakt met Hallo opgegeven proxyreferenties. Hallo-proxyserver zodanig configureren dat dit account kan worden geverifieerd. Hallo VMM RunAs-Accountinstellingen kunnen worden gewijzigd in Hallo VMM-console. toodo deze, open Hallo **instellingen** werkruimte Vouw **beveiliging**, klikt u op **Run As-Accounts**, en wijzig vervolgens Hallo wachtwoord voor DRAProxyAccount. U moet toorestart Hallo VMM-service zodat deze instelling wordt van kracht.
9. In **registratiesleutel**, selecteer Hallo sleutel gedownload uit Azure Site Recovery uit te voeren en toohello VMM-server gekopieerd.
10. Hallo-instelling voor wachtwoordversleuteling wordt alleen gebruikt wanneer u Hyper-V-machines in VMM-clouds tooAzure repliceert. Als u tooa secundaire site repliceert wordt het niet gebruikt.
11. In **servernaam**, Geef een beschrijvende naam tooidentify Hallo VMM-server in Hallo kluis. Geef in een clusterconfiguratie Hallo VMM-clusterrolnaam op.
12. In **cloudmetagegevens synchroniseren** selecteren of u toosynchronize metagegevens voor alle clouds op Hallo VMM-server op Hallo kluis. Deze actie hoeft alleen toohappen eenmaal op elke server. Als u niet toosynchronize alle clouds wilt, kunt u laat u deze instelling uitgeschakeld en synchroniseert u elke cloud afzonderlijk in de eigenschappen van de cloud Hallo in Hallo VMM-console.
13. Klik op **volgende** toocomplete Hallo proces. Na registratie worden metagegevens van Hallo VMM-server opgehaald door Azure Site Recovery. Hallo-server wordt weergegeven in **VMM-Servers** > **Servers** in Hallo kluis.

    ![Servers](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)

### <a name="command-line-installation"></a>Installatie vanaf de opdrachtregel
Hello Azure Site Recovery Provider kan ook worden geïnstalleerd vanaf de opdrachtregel Hallo. Deze methode kan gebruikte tooinstall Hallo-provider op een Server CORE voor Windows Server 2012 R2 zijn.

1. Hallo-Provider en de registratiesleutel sleutel tooa installatiemap downloaden. Bijvoorbeeld: C:\ASR.
2. Hallo System Center Virtual Machine Manager-Service stoppen
3. Hallo Provider-installatieprogramma door deze opdrachten uitvoeren vanaf een opdrachtprompt met uit te pakken **beheerder** bevoegdheden:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Hallo-provider installeren door te voeren:

        C:\ASR> setupdr.exe /i
5. Hallo provider registreren door te voeren:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>     

Wanneer Hallo parameters zijn:

* **/ Credentials**: verplichte parameter waarmee Hallo locatie in welke Hallo registratiesleutelbestand zich bevindt  
* **/ FriendlyName**: verplichte parameter voor de naam Hallo van Hallo Hyper-V-hostserver die wordt weergegeven in hello Azure Site Recovery-portal.
* **/ EncryptionEnabled**: een optionele Parameter die u nodig hebt toouse alleen in Hallo VMM tooAzure Scenario moet u de versleuteling van uw virtuele machines in rust in Azure. Zorg ervoor dat Hallo-naam van bestand Hallo u levert, heeft een **.pfx** extensie.
* **/ proxyaddress**: een optionele parameter waarmee het adres van de proxyserver Hallo Hallo.
* **/ proxyport**: optionele parameter waarmee het Hallo-poort van de proxyserver Hallo.
* **proxyusername**: optionele parameter waarmee de proxygebruikersnaam hello (als de proxyserver verificatie is vereist).
* **/ proxypassword**: optionele parameter waarmee hello wachtwoord voor verificatie met de proxyserver hello (als de proxyserver verificatie is vereist).  

## <a name="step-4-configure-cloud-protection-settings"></a>Stap 4: Configureer cloud beveiligingsinstellingen
Nadat de VMM-servers zijn geregistreerd, kunt u cloudbeveiligingsinstellingen configureren. Als u de optie Hallo ingeschakeld **cloudgegevens synchroniseren met de kluis Hallo** wanneer u Hallo Provider hebt geïnstalleerd, zodat alle clouds op Hallo VMM server wordt weergegeven in Hallo **beveiligde Items** tabblad in Hallo kluis. Als u niet dat u kunt een specifieke cloud synchroniseren met Azure Site Recovery in Hallo **algemene** tabblad van Hallo pagina voor cloudeigenschappen in Hallo VMM-console.

![Gepubliceerde cloud](./media/site-recovery-vmm-to-vmm-classic/clouds-list.png)

1. Klik op de pagina snel starten Hallo **beveiliging instellen voor VMM-clouds**.
2. Op Hallo **VMM-Clouds** tabblad, selecteer Hallo cloud die u tooconfigure wilt en ga toohello **configuratie** tabblad.
3. In **doel**, selecteer **VMM**.
4. In **doellocatie**, selecteer Hallo lokale VMM-server die wordt beheerd Hallo cloud gewenste toouse voor herstel.
5. In **doel cloud**, Hallo doelcloud u toouse voor failover van virtuele machines in de broncloud hello wilt selecteren. Opmerking:

   * Het is raadzaam dat u selecteert een doelcloud op die voldoet aan de herstelvereisten voor Hallo virtuele machines die u gaat beveiligen.
   * Een cloud kan alleen deel uitmaken van één tooa-cloudpaar — als een primaire of een doelcloud op.
6. In **Kopieerfrequentie**, Geef op hoe vaak gegevens moeten worden gesynchroniseerd tussen de bron- en doellocaties 5he. Houd er rekening mee dat deze instelling alleen relevant is wanneer Hallo Hyper-V-host Windows Server 2012 R2 wordt uitgevoerd. Voor andere servers wordt een standaardwaarde van vijf minuten gebruikt.
7. In **extra herstelpunten**, opgeven of u toocreate extra punten. Hallo-standaardwaarde nul geeft aan dat alleen Hallo meest recente herstelpunt voor een primaire virtuele machine is opgeslagen op een replicahostserver. Houd er rekening mee dat het inschakelen van meerdere herstelpunten extra opslagruimte vereist voor Hallo momentopnamen die zijn opgeslagen in elk herstelpunt. Herstelpunten worden elk uur gemaakt zodat elk herstelpunt een uur aan gegevens bevat. Hallo waarde voor een herstelpunt dat u voor Hallo virtuele machine in VMM-console Hallo toewijst mag niet kleiner zijn dan Hallo-waarde die u toewijst in hello Azure Site Recovery-console zijn.
8. In **frequentie van toepassingsconsistente momentopnamen**, Geef op hoe vaak toocreate toepassingsconsistente momentopnamen. Hyper-V gebruikt twee soorten momentopnamen: standaardmomentopnamen waarmee een incrementele momentopname van Hallo volledige virtuele machine en een toepassingsconsistente momentopnamen waarmee een momentopname van een punt in tijd van de toepassingsgegevens Hallo in Hallo virtuele machine. Toepassingsconsistente momentopnamen gebruiken Volume Shadow Copy Service (VSS) tooensure die toepassingen zich in een consistente status wanneer Hallo momentopname wordt gemaakt. Houd er rekening mee dat als u toepassingsconsistente momentopnamen inschakelt, het invloed is op Hallo prestaties van toepassingen die worden uitgevoerd op virtuele machines die bron. Zorg ervoor dat Hallo-waarde lager dan Hallo aantal aanvullende herstelpunten dat u configureert.

    ![Configureer beveiligingsinstellingen](./media/site-recovery-vmm-to-vmm-classic/cloud-settings.png)
9. In **gegevensoverdracht compressie**, opgeven of de gerepliceerde gegevens die worden overgedragen moeten worden gecomprimeerd.
10. In **verificatie**, opgeven hoe verkeer wordt geverifieerd tussen primaire Hallo en herstel Hyper-V-hostservers. Selecteer HTTPS als u beschikt over een werkende Kerberos-omgeving die zijn geconfigureerd. Azure Site Recovery configureert automatisch certificaten voor HTTPS-verificatie. Er is geen handmatige configuratie vereist. Als u Kerberos selecteert, wordt een Kerberos-ticket voor wederzijdse verificatie van hostservers hello worden gebruikt. Standaard wordt poort 8083 en 8084 (voor certificaten) in Hallo Windows Firewall op Hallo Hyper-V-hostservers worden geopend. Houd er rekening mee dat deze instelling is alleen relevant voor Hyper-V-host-servers waarop Windows Server 2012 R2.
11. In **poort**, wijzigen Hallo-poortnummer op welke Hallo-bron en doel host computers listen voor replicatieverkeer. U zou bijvoorbeeld Hallo instelling wijzigen als u wilt dat tooapply Quality of Service (QoS) netwerk bandbreedtebeperking voor replicatieverkeer. Controleer of Hallo poort wordt niet door een andere toepassing gebruikt en dat deze geopend in Hallo firewall-instellingen is.
12. In **replicatiemethode**, opgeven hoe initiële replicatie van gegevens van tootarget bronlocaties Hallo worden verwerkt voordat normale replicatie wordt gestart:

    * **Via netwerk**: tijdrovende en bronintensieve kopiëren van gegevens via Hallo netwerk zijn. Het is raadzaam dat u deze optie gebruiken als Hallo cloud bevat virtuele machines met relatief klein virtuele harde schijven, en als Hallo primaire site is verbonden toohello secundaire site via een verbinding met een grote bandbreedte. U kunt opgeven dat Hallo kopie moet onmiddellijk starten of Selecteer een tijd. Als u replicatie netwerk gebruikt, raden wij tijdens daluren te plannen.
    * **Offline**: deze methode geeft aan dat Hallo initiële replicatie wordt uitgevoerd met behulp van externe media. Dit is handig als u wilt dat tooavoid vermindering in prestaties van het netwerk of voor geografisch externe locaties. toouse deze methode die u Hallo exportlocatie op Hallo broncloud en Hallo importeren locatie op Hallo doelcloud opgeven. Wanneer u beveiliging voor een virtuele machine inschakelt, Hallo virtuele hardeschijf is het gekopieerde toohello opgegeven locatie voor exporteren. U toohello doelsite verzenden en kopieer het toohello importeren locatie. Hallo system kopieën Hallo geïmporteerd informatie toohello gerepliceerde virtuele machines.
13. Selecteer **Replica virtuele Machine verwijderen** toospecify die Hallo replica virtuele machine moet worden verwijderd als u de beveiliging van Hallo virtuele machine door het selecteren van Hallo stopt **beveiliging voor Hallo virtuele machine verwijderen ** optie op tabblad van de virtuele Machines Hallo Hallo cloud eigenschappen. Met deze instelling is ingeschakeld, wanneer u uitschakelt beveiliging Hallo virtuele machine wordt verwijderd uit Azure Site Recovery, Hallo Site Recovery-instellingen voor Hallo virtuele machine worden verwijderd in de VMM-console Hallo en Hallo replica is verwijderd.

    ![Configureer beveiligingsinstellingen](./media/site-recovery-vmm-to-vmm-classic/cloud-settings-replica.png)

Nadat u Hallo instellingen opslaan in een taak wordt gemaakt en kan worden gecontroleerd op Hallo **taken** tabblad. Alle Hyper-V-hostservers in VMM-broncloud Hallo zullen worden geconfigureerd voor replicatie. Cloudinstellingen kunnen worden gewijzigd op Hallo **configureren** tabblad. Als u toomodify Hallo doellocatie of doelcloud wilt moet u Hallo cloud-configuratie verwijderen en Hallo cloud vervolgens opnieuw te configureren.

### <a name="prepare-for-offline-initial-replication"></a>Voorbereiden voor de offline initiële replicatie
U moet toodo hello tooprepare acties voor de offline initiële replicatie te volgen:

* Op de bronserver hello, moet u de padlocatie van een van welke Hallo exporteren van gegevens wordt gehouden. Volledig beheer voor machtigingen voor NTFS en deelmachtigingen toohello VMM-service op Hallo exportpad toewijzen. Op de doelserver hello, hebt u een locatie waarvan Hallo gegevens importeren wordt uitgevoerd. Hallo dezelfde machtigingen voor dit pad importeren toewijzen.
* Als hello importeren of exporteren pad wordt gedeeld, Administrator, Hoofdgebruikers, Print Operators of Server Operator groepslidmaatschap voor Hallo VMM-serviceaccount op de externe computer Hallo toewijzen welke Hallo gedeeld zich bevindt.
* Als u geen Run As-accounts tooadd hosts gebruikt, op Hallo importeren en exporteren paden, lezen toewijzen en schrijfmachtigingen toohello-Run As-accounts in VMM.
* Hallo importeren en exporteren van shares niet moet zich bevinden op een computer die wordt gebruikt als een Hyper-V-hostserver, omdat de loopback-configuratie wordt niet ondersteund door Hyper-V.
* In Active Directory is op elke Hyper-V-hostserver die bevat virtuele machines die u wilt dat tooprotect, inschakelen en configureren van beperkte delegering tootrust Hallo externe computers op welke Hallo importeren en exporteren paden zich bevinden, als volgt:
  1. Open op de domeincontroller hello, **Active Directory: gebruikers en Computers**.
  2. Klik in de consolestructuur Hallo **DomainName** > **Computers**.
  3. Klik met de rechtermuisknop Hallo Hyper-V-host-servernaam > **eigenschappen**.
  4. Op Hallo **delegering** tabblad klikt u op T**roest alleen overdracht toospecified-services op deze computer**.
  5. Klik op **elk verificatieprotocol voor gebruiken**.
  6. Klik op **toevoegen** > **gebruikers en Computers**.
  7. Hallo-typenaam van Hallo-computer die als host fungeert voor Hallo exportpad > **OK**. Hallo-lijst met beschikbare services, Hallo CTRL-toets ingedrukt en klik op **cifs** > **OK**. Herhaal voor Hallo naam van de computer Hallo dat pad hosts Hallo importeren. Herhaal zo nodig voor extra Hyper-V-hostservers.

## <a name="step-5-configure-network-mapping"></a>Stap 5: Netwerktoewijzing configureren
1. Klik op de pagina snel starten Hallo **netwerken toewijzen**.
2. Selecteer Hallo bron VMM-server van waaruit u wilt dat toomap netwerken en vervolgens Hallo doel VMM server toowhich Hallo netwerken worden toegewezen. Hallo-lijst van de bron en hun bijbehorende doelnetwerken weergegeven. Een lege waarde weergegeven voor de netwerken die momenteel niet worden toegewezen.
3. Selecteer een netwerk in **netwerk op de bron** > **kaart**. Hallo-service detecteert Hallo VM-netwerken op de doelserver Hallo en geeft deze weer. Klik op Hallo informatie pictogram volgende toohello bron en doel namen tooview Hallo netwerksubnetten voor elk netwerk.

    ![Netwerktoewijzing configureren](./media/site-recovery-vmm-to-vmm-classic/network-mapping1.png)
4. Selecteer een van de VM-netwerken Hallo in dialoogvenster Hallo van Hallo doel-VMM-server.

    ![Een doelnetwerk selecteren](./media/site-recovery-vmm-to-vmm-classic/network-mapping2.png)
5. Wanneer u een doelnetwerk selecteert, worden hello beveiligde clouds die Hallo Bronnetwerk weergegeven. Netwerken met beschikbare doelservers die gekoppeld aan het Hallo-clouds gebruikt voor beveiliging zijn worden ook weergegeven. Het is raadzaam dat u selecteert een doelnetwerk dat beschikbaar tooall Hallo clouds die u gebruikt voor beveiliging. Of u kunt ook gaat toohello VMM-Server en Hallo cloud eigenschappen tooadd Hallo logisch netwerk wijzigen toohello vm-netwerk dat u wilt dat toochoose overeenkomt.
6. Klik op Hallo vinkje toocomplete Hallo toewijzingsproces. Een taak begint tootrack Hallo toewijzing uitgevoerd. U kunt deze ook bekijken op Hallo **taken** tabblad.

## <a name="step-6-configure-storage-mapping"></a>Stap 6: De toewijzing van opslag configureren
Standaard dat wanneer u een virtuele machine op een Hyper-V-host-server tooa doel Hyper-V-host bronserver, repliceert gerepliceerde gegevens worden opgeslagen in de standaardlocatie Hallo die opgegeven voor Hallo doel Hyper-V-host in Hyper-V-beheer. Voor meer controle over waar de gerepliceerde gegevens worden opgeslagen, kunt u de toewijzingen van bestanden als volgt configureren:

1. Opslagclassificaties definiëren op beide Hallo-bron en doel van de VMM-servers. [Meer informatie](https://technet.microsoft.com/library/gg610685.aspx). Classificaties moet beschikbaar toohello Hyper-V-hostservers in bron en doel-clouds. Classificaties hoeft niet toohave Hallo hetzelfde type opslag. U kunt bijvoorbeeld een bron-classificatie met SMB-shares tooa doel classificatie met CSV's toewijzen.
2. Nadat de classificaties zijn geïnstalleerd, kunt u toewijzingen maken. toodo dit op Hallo **Quick Start** pagina > **opslag toewijzen**.
3. Klik op Hallo **opslag** tabblad > **opslagclassificaties toewijzen**.
4. Op Hallo **opslagclassificaties toewijzen** tabblad, selecteert u classificaties op Hallo bron en doel van de VMM-servers. Uw instellingen opslaan.

    ![Een doelnetwerk selecteren](./media/site-recovery-vmm-to-vmm-classic/storage-mapping.png)

## <a name="step-7-enable-virtual-machine-protection"></a>Stap 7: Beveiliging van virtuele machines inschakelen
Nadat de servers, clouds en netwerken correct zijn geconfigureerd, kunt u beveiliging voor virtuele machines in de cloud Hallo inschakelen.

1. Op Hallo **virtuele Machines** tabblad Hallo cloud welke Hallo virtuele machine zich bevindt, klikt u op **beveiliging inschakelen** > **virtuele machines toevoegen**.
2. Selecteer in lijst Hallo van virtuele machines in de cloud Hallo Hallo een gewenste tooprotect.

    ![Beveiliging van de virtuele machine inschakelen](./media/site-recovery-vmm-to-vmm-classic/enable-protection.png)
3. Voortgang van de bewerking beveiliging inschakelen in Hallo Hallo volgen **taken** tabblad, met inbegrip van Hallo initiële replicatie. Nadat de taak beveiliging voltooien Hallo is uitgevoerd Hallo virtuele machine gereed voor failover. Nadat de beveiliging is ingeschakeld en virtuele machines zijn gerepliceerd, moet u kunnen tooview ze in Azure.

    ![Beveiligingstaak voor virtuele machines](./media/site-recovery-vmm-to-vmm-classic/vm-jobs.png)

> [!NOTE]
> U kunt ook beveiliging voor virtuele machines in Hallo VMM-console inschakelen. Klik op **beveiliging inschakelen** op de werkbalk Hallo in Hallo **Azure Site Recovery** tabblad in de eigenschappen van de virtuele machine Hallo.
>
>

### <a name="on-board-existing-virtual-machines"></a>Ingebouwde bestaande virtuele machines
Als u een bestaande virtuele machines in VMM die worden gerepliceerd met Hyper-V Replica hebt moet u tooonboard ze voor Azure Site Recovery-beveiliging als volgt:

1. Controleer of dat u de primaire en secundaire clouds hebt. Zorg ervoor dat Hallo Hyper-V-hostserver Hallo bestaande virtuele machine bevindt zich in de primaire cloud Hallo en die Hallo Hyper-V-server die als host fungeert voor Hallo replica virtuele machine bevindt zich in Hallo secundaire cloud. Zorg ervoor dat u de beveiligingsinstellingen voor Hallo clouds hebt geconfigureerd. Hallo-instellingen moeten overeenkomen met die momenteel geconfigureerd voor Hyper-V Replica. Anders replicatie voor virtuele machines werkt mogelijk niet zoals verwacht.
2. Schakel vervolgens de beveiliging voor Hallo primaire virtuele machine. Azure Site Recovery en VMM zorgt ervoor dat hello dezelfde replicatiehost en virtuele machine wordt gedetecteerd en Azure Site Recovery wordt opnieuw gebruikt en herstellen van replicatie met Hallo-instellingen die zijn geconfigureerd tijdens de cloudconfiguratie.

## <a name="test-your-deployment"></a>Uw implementatie testen
tootest plannen voor uw implementatie kunt u een testfailover voor één virtuele machine uitvoeren of maken van een herstelplan dat bestaat uit meerdere virtuele machines en een testfailover voor Hallo uitvoeren.  Met een testfailover wordt uw failover- en herstelmechanisme in een geïsoleerd netwerk gesimuleerd.

### <a name="create-a-recovery-plan"></a>Een herstelplan maken
1. Op Hallo **herstelplannen** tabblad **herstelplan maken**.
2. Geef een naam voor het herstelplan Hallo en bron en doel-VMM-servers. Hallo-bronserver moet virtuele machines hebt die zijn ingeschakeld voor failover en herstel. Selecteer **Hyper-V** tooview alleen clouds die zijn geconfigureerd voor Hyper-V-replicatie.

    ![Herstelplan maken](./media/site-recovery-vmm-to-vmm-classic/recovery-plan1.png)
3. In **virtuele Machine selecteren**, replicatiegroepen selecteren. Alle virtuele machines die zijn gekoppeld aan de replicatiegroep hello wordt geselecteerd en toohello herstelplan toegevoegd. Deze virtuele machines worden toegevoegd standaardgroep herstel toohello: groep 1. indien nodig, kunt u meer groepen toevoegen. Let na replicatie virtuele machines in overeenstemming met Hallo volgorde van Hallo recovery planningsgroepen wordt gestart.

    ![Virtuele machines toevoegen](./media/site-recovery-vmm-to-vmm-classic/recovery-plan2.png)

Nadat een herstelplan is gemaakt, wordt deze weergegeven in de lijst op Hallo Hallo **herstelplannen** tabblad.

### <a name="run-a-test-failover"></a>Een testfailover uitvoeren
1. Op Hallo **herstelplannen** tabblad, selecteer Hallo-plan en klik op **Testfailover**.
2. Op Hallo **Testfailover bevestigen** pagina **geen**. Houd er rekening mee dat met deze optie ingeschakeld Hallo failover gerepliceerde virtuele machines niet kan verbonden tooany netwerk worden. Hierdoor wordt die Hallo mislukt van de virtuele machine dan verwacht, maar test uw netwerkomgeving replicatie niet getest. Kijken hoe te[een testfailover uitvoeren](site-recovery-failover.md) voor meer informatie over hoe de andere netwerkopties toouse.
3. Hallo test-virtuele machine wordt gemaakt op Hallo dezelfde host als Hallo-host op welke Hallo replica virtuele machine bestaat. Deze is toegevoegd toohello dezelfde cloud welke Hallo replica virtuele machine zich bevindt.

### <a name="run-a-recovery-plan"></a>Een herstelplan uitvoeren
Nadat de replicatie Hallo replica virtuele machine mogelijk geen een IP-adres dat Hallo Hallo dezelfde zijn als Hallo IP-adres van primaire virtuele machine. Virtuele machines Hallo DNS-server die ze gebruiken wordt bijgewerkt nadat ze zijn gestart. U kunt ook een script tooupdate Hallo DNS-Server tooensure een tijdige update toevoegen.

#### <a name="script-tooretrieve-hello-ip-address"></a>Script tooretrieve Hallo IP-adres
Dit voorbeeld script tooretrieve Hallo IP-adres worden uitgevoerd.

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

#### <a name="script-tooupdate-dns"></a>Script tooupdate DNS
Uitvoeren van dit voorbeeld script tooupdate DNS, opgeven Hallo IP-adres dat u hebt opgehaald Hallo-voorbeeldscript gebruiken.

        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="privacy-information-for-site-recovery"></a>Privacy-informatie voor de Site Recovery
Deze sectie bevat aanvullende informatie over privacy voor Hallo Microsoft Azure Site Recovery-service ("Service"). tooview Hallo-privacyverklaring voor Microsoft Azure-services, Zie de [Microsoft Azure privacyverklaring](http://go.microsoft.com/fwlink/?LinkId=324899)

**Functie: registratie**

* **Wat het doet**: server registreren met de service, zodat virtuele machines kunnen worden beveiligd.
* **Verzamelde gegevens**: na het Hallo-Service worden verzameld, verwerkt en certificaat beheergegevens van Hallo VMM-server die is aangewezen tooprovide noodherstel met behulp van de servicenaam Hallo van Hallo VMM-beheerserver, brengt registreren en de naam Hallo van clouds voor virtuele machines op de VMM-server.
* **Gebruik van informatie**:

  * Beheercertificaat: dit wordt gebruikt toohelp identificeren en VMM-server Hallo geregistreerd voor toegang tot toohello Service te verifiëren. Hallo Service maakt gebruik van openbare sleutel deel Hallo van Hallo certificaat toosecure een token dat alleen Hallo geregistreerd VMM-server toegang kan krijgen tot. Hallo-server moet toouse dit token toogain toohello Service toegangsfuncties.
  * Naam van de VMM-server Hallo: Hallo VMM-servernaam wordt vereist tooidentify en communiceren met Hallo juiste VMM-server op welke Hallo clouds zich bevinden.
  * Namen van de VMM-server Hallo cloud: Hallo cloud-naam is vereist wanneer Hallo Service cloud koppelen/ontkoppelen functie die hieronder worden beschreven. Wanneer u op uw cloud uit een primaire datacenter met een andere cloud in Hallo herstel Datacenter toopair beslist, wordt Hallo namen van alle Hallo clouds vanuit Hallo recovery Datacenter weergegeven.
* **Keuze**: deze informatie is een essentieel onderdeel van het registratieproces Service Hallo omdat de service u helpt en Service tooidentify Hallo VMM-server waarvoor u tooprovide Azure Site Recovery-beveiliging, evenals tooidentify Hallo wenst Hallo juiste geregistreerde VMM-server. Als u deze informatie toohello Service toosend wilt, gebruik geen deze Service. Als u uw server registreren en toounregister vervolgens later wilt, kunt u doen door Hallo VMM server-gegevens te verwijderen via de serviceportal hello (die is hello Azure-portal).

**Functie: Azure Site Recovery-beveiliging inschakelen**

* **Wat het doet**: hello Azure Site Recovery Provider is geïnstalleerd op de VMM-server Hallo Hallo-kanaal voor communicatie met de Hallo Service is. Hallo Provider is een dynamic-link library (DLL) gehost Hallo VMM. Hallo 'Datacenterherstel' functie opgehaald na het Hallo-Provider is geïnstalleerd, ingeschakeld in Hallo VMM administrator-console. Een eigenschap genaamd 'Datacenterherstel' kunt inschakelen door een nieuwe of bestaande virtuele machines in een cloud toohelp beveiligen Hallo virtuele machine. Zodra deze eigenschap is ingesteld, verzendt Hallo Provider Hallo naam en de ID van Hallo virtuele machine toohello Service. Hallo virtuele beveiliging wordt ingeschakeld door Windows Server 2012 of Windows Server 2012 R2 Hyper-V Replicatietechnologie. Hallo virtuele machinegegevens worden gerepliceerd van een Hyper-V-host tooanother (doorgaans te vinden in een datacenter van verschillende "herstelpunt').
* **Verzamelde gegevens**: Hallo Service worden verzameld, verwerkt en metagegevens voor de virtuele-machine hello, waaronder Hallo name, -ID, virtueel netwerk en Hallo-naam van de cloud Hallo verzendt waartoe deze behoort.
* **Gebruik van informatie**: Hallo Service Hallo hierboven toopopulate Hallo virtuele machine gegevens op uw Service-portal gebruikt.
* **Keuze**: dit is een essentieel onderdeel van het Hallo-service en kan niet worden uitgeschakeld. Als u niet dat deze gegevens worden toohello Service verzonden wilt, niet inschakelen voor Azure Site Recovery-beveiliging voor virtuele machines. Houd er rekening mee dat alle gegevens die zijn verzonden door Hallo Provider toohello Service worden verzonden via HTTPS.

**Functie: Het herstelplan**

* **Wat het doet**: deze functie kunt u een plan orchestration voor Hallo 'herstel' datacenter toobuild. U kunt in welke Hallo virtuele machines of een groep van virtuele machines moet worden gestart op de herstelsite Hallo Hallo-volgorde definiëren. U kunt ook een geautomatiseerde scripts toobe uitvoeren of een handmatige actie toobe genomen op Hallo moment van herstel voor elke virtuele machine opgeven. Failover (behandeld in de volgende sectie Hallo) wordt doorgaans geactiveerd op Hallo herstelplan niveau voor gecoördineerde herstel.
* **Verzamelde gegevens**: Hallo Service worden verzameld, verwerkt en metagegevens voor het herstelplan hello, met inbegrip van metagegevens van de virtuele machine en metagegevens van eventuele automatiseringsscripts en -opmerkingen bij de handmatige actie verzendt.
* **Gebruik van informatie**: Hallo metagegevens die hierboven worden beschreven is gebruikte toobuild Hallo herstelplan in uw Service-portal.
* **Keuze**: dit is een essentieel onderdeel van het Hallo-service en kan niet worden uitgeschakeld. Als u niet dat deze gegevens worden toohello Service verzonden wilt, niet samenstellen herstelplannen in deze Service.

**Functie: Netwerktoewijzing**

* **Wat het doet**: deze functie kunt u toomap netwerkgegevens van Hallo primaire data center toohello herstel Datacenter. Wanneer Hallo virtuele machines zijn hersteld op de herstelsite hello, wordt deze toewijzing helpt bij het maken van verbinding met het netwerk voor deze.
* **Verzamelde gegevens**: als onderdeel van de toewijzingsfunctie voor Hallo netwerk, Hallo Service worden verzameld, verwerkt, en verstuurt Hallo metagegevens van de logische netwerken Hallo voor elke site (primair en datacenter).
* **Gebruik van informatie**: Hallo Service maakt gebruik van Hallo metagegevens toopopulate uw Service-portal waar u hello netwerkgegevens kunt toewijzen.
* **Keuze**: dit is een essentieel onderdeel van Hallo Service en kan niet worden uitgeschakeld. Als u niet dat deze gegevens worden verzonden toohello Service wilt, hoeft u Hallo netwerk toewijzingsfunctie.

**Functie: Failover - test voor geplande, niet-geplande**

* **Wat het doet**: deze functie kunt u failover van een virtuele machine van een in VMM beheerde center tooanother VMM beheerde gegevens Datacenter. Hallo failover actie wordt geactiveerd door de gebruiker Hallo op hun serviceportal. Mogelijke oorzaken voor een failover zijn een niet-geplande gebeurtenis (bijvoorbeeld in geval van een natuurlijke disaster0; Hallo een geplande gebeurtenis (bijvoorbeeld datacenter load balancing); een testfailover (bijvoorbeeld een herstel plan try-out).

Hallo Provider op de VMM-server Hallo Hallo-gebeurtenis uit Hallo Service opgehaald gewaarschuwd en een failover-actie uitvoert op Hallo Hyper-V-host via de VMM-interfaces. Werkelijke failover van Hallo virtuele machine uit een Hyper-V-host tooanother (doorgaans uitgevoerd in een datacenter van verschillende "herstelpunt') wordt uitgevoerd door Hallo Windows Server 2012 of Windows Server 2012 R2 Hyper-V Replicatietechnologie. Nadat Hallo failover voltooid is, stuurt Hallo Provider is geïnstalleerd op de VMM-server van Hallo 'herstel' datacenter Hallo Hallo geslaagd informatie toohello Service.

* **Verzamelde gegevens**: Hallo Service Hallo hierboven informatie toopopulate Hallo status van Hallo failover actie-informatie op uw Service-portal gebruikt.
* **Gebruik van informatie**: Hallo Service gebruikt Hallo boven de gegevens als volgt:

  * Beheercertificaat: dit wordt gebruikt toohelp identificeren en VMM-server Hallo geregistreerd voor toegang tot toohello Service te verifiëren. Hallo Service maakt gebruik van openbare sleutel deel Hallo van Hallo certificaat toosecure een token dat alleen Hallo geregistreerd VMM-server toegang kan krijgen tot. Hallo-server moet toouse dit token toogain toohello Service toegangsfuncties.
  * Naam van de VMM-server Hallo: Hallo VMM-servernaam wordt vereist tooidentify en communiceren met Hallo juiste VMM-server op welke Hallo clouds zich bevinden.
  * Namen van de VMM-server Hallo cloud: Hallo cloud-naam is vereist wanneer Hallo Service cloud koppelen/ontkoppelen functie die hieronder worden beschreven. Wanneer u op uw cloud uit een primaire datacenter met een andere cloud in Hallo herstel Datacenter toopair beslist, wordt Hallo namen van alle Hallo clouds vanuit Hallo recovery Datacenter weergegeven.
* **Keuze**: dit is een essentieel onderdeel van het Hallo-service en kan niet worden uitgeschakeld. Als u niet dat deze gegevens worden verzonden toohello Service wilt, hoeft u deze Service.

## <a name="next-steps"></a>Volgende stappen
Na het uitvoeren van een test failover toocheck uw omgeving werkt zoals verwacht, [meer informatie over](site-recovery-failover.md) verschillende soorten failovers.
