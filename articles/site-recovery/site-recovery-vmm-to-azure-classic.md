---
title: aaaReplicate Hyper-V virtuele machines in VMM-clouds tooAzure | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooreplicate Hyper-V virtuele machines op Hyper-V-hosts zich in System Center VMM-clouds tooAzure.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 9d526a1f-0d8e-46ec-83eb-7ea762271db5
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: 136f68585534c17b615ecc4e82c0133bf813503f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure"></a>Hyper-V virtuele machines in VMM-clouds tooAzure repliceren
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-azure.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [Klassieke portal](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - Klassiek](site-recovery-deploy-with-powershell.md)
>
>

Hello Azure Site Recovery-service draagt bij tooyour zakelijke continuïteit en (BCDR) strategie voor noodherstel door organiseren replicatie, failovers en herstel van virtuele machines en fysieke servers. Machines kunnen gerepliceerde tooAzure of tooa secundaire on-premises datacenter zijn. Lees voor een snel overzicht [Wat is Azure Site Recovery?](site-recovery-overview.md)

## <a name="overview"></a>Overzicht
Dit artikel wordt beschreven hoe toodeploy siteherstel tooreplicate Hyper-V virtuele machines op Hyper-V-hostservers die zich in de VMM-privéclouds tooAzure bevinden.

Hallo artikel bevat vereisten voor Hallo scenario en ziet u hoe tooset van Site Recovery-kluis downloaden hello Azure Site Recovery Provider is geïnstalleerd op VMM-bronserver met Hallo Hallo-server registreren in de kluis Hallo, Azure storage-account toevoegen, Hallo installeren Azure Recovery Services-agent op Hyper-V-hostservers Configureer beveiligingsinstellingen voor VMM-clouds die wordt toegepast tooall beveiligde virtuele machines, en schakel vervolgens de beveiliging voor deze virtuele machines. Voltooien door failover toomake testen Hallo controleren of dat alles werkt zoals verwacht.

Eventuele opmerkingen of vragen plaatsen onderin Hallo van dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architecture"></a>Architectuur
![Architectuur](./media/site-recovery-vmm-to-azure-classic/topology.png)

* Hello Azure Site Recovery Provider is geïnstalleerd op Hallo VMM tijdens de implementatie van Site Recovery en Hallo VMM-server is geregistreerd in Hallo Site Recovery-kluis. Hallo Provider communiceert met Site Recovery toohandle replicatie-indeling.
* Hello Azure Recovery Services-agent is geïnstalleerd op de Hyper-V-hostservers tijdens de implementatie van Site Recovery. Gegevensopslag replicatie tooAzure verwerkt.

## <a name="azure-prerequisites"></a>Vereisten voor Azure
In Azure hebt u het volgende nodig.

| **Vereiste** | **Details** |
| --- | --- |
| **Azure-account** |U hebt een [Microsoft Azure](https://azure.microsoft.com/)-account nodig. U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/). [Meer informatie](https://azure.microsoft.com/pricing/details/site-recovery/) over prijzen voor Site Recovery. |
| **Azure Storage** |U moet een Azure storage-account toostore gerepliceerde gegevens. Gerepliceerde gegevens worden opgeslagen in Azure Storage en Azure VM's worden bij een failover ingezet. <br/><br/>U hebt een [standaard geografisch redundant opslagaccount](../storage/common/storage-redundancy.md#geo-redundant-storage) nodig. Hallo-account moet zich in dezelfde regio bevinden als de Site Recovery-service Hallo Hallo en worden gekoppeld aan hetzelfde abonnement Hallo. Houd er rekening mee dat replicatie toopremium storage-accounts wordt momenteel niet ondersteund en mag niet worden gebruikt.<br/><br/>[Meer informatie](../storage/common/storage-introduction.md) over Azure-opslag. |
| **Azure-netwerk** |U moet een Azure-netwerk waarmee virtuele Azure-machines verbinding maken toowhen failover plaatsvindt. Hello Azure virtuele netwerk moet zich in Hallo dezelfde regio bevinden als Hallo Site Recovery-kluis. |

## <a name="on-premises-prerequisites"></a>Vereisten voor on-premises
Dit is wat u on-premises nodig hebt.

| **Vereiste** | **Details** |
| --- | --- |
| **VMM** |U moet ten minste één VMM-server hebben die als fysieke of virtuele zelfstandige server of als virtueel cluster is geïmplementeerd. <br/><br/>Hallo VMM-server moet System Center 2012 R2 met Hallo meest recente cumulatieve updates worden uitgevoerd.<br/><br/>U moet ten minste één cloud zijn geconfigureerd op Hallo VMM-server.<br/><br/>Hallo-broncloud die u wilt dat tooprotect moet een of meer VMM-hostgroepen bevatten.<br/><br/>Meer informatie over het instellen van VMM-clouds in [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx) (Overzicht: privéclouds maken met System Center 2012 SP1 VMM) in het blog van Keith Mayer. |
| **Hyper-V** |U moet een of meer Hyper-V-hostservers of -clusters in Hallo VMM-cloud. Hallo-hostserver moet hebben en een of meer virtuele machines. <br/><br/>Hallo Hyper-V-server moet worden uitgevoerd op ten minste **Windows Server 2012 R2** met Hallo Hyper-V-rol of **Microsoft Hyper-V Server 2012 R2** en hebben Hallo nieuwste updates zijn geïnstalleerd.<br/><br/>Een Hyper-V-server met VM's die wilt u dat tooprotect moet zich bevinden in een VMM-cloud.<br/><br/>Als u Hyper-V in een cluster uitvoert, wordt die clusterbroker niet automatisch gemaakt als u een cluster op basis van een statisch IP-adres hebt. U moet tooconfigure hello clusterbroker handmatig. [Meer informatie](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters) in het blog van Aidan Finn. |
| **Beveiligde machines** | Virtuele machines die u wilt dat tooprotect moeten voldoen aan [Azure-vereisten](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). |

## <a name="network-mapping-prerequisites"></a>Vereisten voor netwerktoewijzing
Als u virtuele machines in Azure koppelingen van Netwerktoewijzingen tussen VM-netwerken op Hallo bron-VMM-server beveiligen en gericht op Azure-netwerken tooenable Hallo volgende:

* Alle machines met failover op Hallo dezelfde netwerk verbinding kan maken van andere, ongeacht welk herstelplan ze tooeach.
* Als een netwerkgateway is ingesteld op Hallo Azure-doelnetwerk, kunnen virtuele machines verbinding tooother on-premises virtuele machines maken.
* Als u niet configureert netwerk alleen virtuele machines met failover in Hallo dezelfde toewijzing herstelplan kunnen tooconnect tooeach andere worden na failover tooAzure.

Als u wilt dat de netwerktoewijzing toodeploy moet u de volgende Hallo:

* Hallo virtuele machines die u wilt dat tooprotect op Hallo bron-VMM-server moet zijn verbonden tooa VM-netwerk. Dit netwerk moet gekoppelde tooa logisch netwerk dat is gekoppeld aan Hallo cloud.
* Een Azure-netwerk toowhich gerepliceerde virtuele machines verbinding kunnen maken na een failover. U selecteert dit netwerk op Hallo moment van failover. Hallo-netwerk moet zich in Hallo dezelfde regio bevinden als uw Azure Site Recovery-abonnement.


Het voorbereiden van netwerken in VMM:

   * [Stel logische netwerken in](https://technet.microsoft.com/library/jj721568.aspx).
   * [Stel VM-netwerken in](https://technet.microsoft.com/library/jj721575.aspx).


## <a name="step-1-create-a-site-recovery-vault"></a>Stap 1: Een Site Recovery-kluis maken
1. Meld u aan toohello [beheerportal](https://portal.azure.com) van Hallo VMM-server die u wilt tooregister.
2. Klik op **Data Services** > **Recovery Services** > **Site Recovery-kluis**.
3. Klik op **Nieuw maken** > **Snelle invoer**.
4. In **naam**, voer een beschrijvende naam tooidentify Hallo-kluis.
5. In **regio**, selecteer de geografische regio voor de kluis Hallo Hallo. toocheck ondersteunde regio's Zie geografische beschikbaarheid in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Klik op **Kluis maken**.

    ![Nieuwe kluis](./media/site-recovery-vmm-to-azure-classic/create-vault.png)

Selectievakje Hallo status balk tooconfirm die Hallo kluis is gemaakt. Hallo-kluis wordt weergegeven als **Active** op Hallo hoofdpagina Recovery Services.

## <a name="step-2-generate-a-vault-registration-key"></a>Stap 2: Een kluisregistratiesleutel genereren
Genereer een registratiesleutel in Hallo kluis. Nadat u hello Azure Site Recovery Provider downloaden en op Hallo VMM-server installeren, gebruikt u deze sleutel tooregister Hallo VMM-server in Hallo kluis.

1. In Hallo **Recovery Services** pagina, klikt u op Hallo kluis tooopen Hallo snel starten-pagina. Snel starten kan ook worden geopend op elk gewenst moment Hallo-pictogram.

    ![Pictogram Snel starten](./media/site-recovery-vmm-to-azure-classic/qs-icon.png)
2. Selecteer in de vervolgkeuzelijst Hallo **tussen een lokale VMM-site en Microsoft Azure**.
3. Klik in **VMM-servers voorbereiden** op het **Registratiesleutel genereren**-bestand. Hallo-sleutelbestand wordt automatisch gegenereerd en is geldig tot 5 dagen nadat deze gegenereerd. Als u geen toegang Azure-portal Hallo van Hallo VMM-server tot moet u toocopy deze toohello bestandsserver.

    ![Registratiesleutel](./media/site-recovery-vmm-to-azure-classic/register-key.png)

## <a name="step-3-install-hello-azure-site-recovery-provider"></a>Stap 3: Hello Azure Site Recovery Provider installeren
1. In **Quick Start** > **VMM-servers voorbereiden**, klikt u op **Microsoft Azure Site Recovery Provider is downloaden voor installatie op VMM-servers** tooobtain Hallo meest recente versie van Hallo Provider-installatiebestand.
2. Voer dit bestand op Hallo bron-VMM-server.

   > [!NOTE]
   > Als VMM is geïmplementeerd in een cluster en u Hallo Provider voor Hallo eerst installeert installeren op een actief knooppunt en Hallo installatie tooregister Hallo VMM-server in de kluis Hallo voltooien. Installeer vervolgens Hallo Provider op Hallo andere knooppunten. Opmerking: als u een Hallo provider moet u tooupgrade op alle knooppunten upgrade uitvoert omdat ze alle moeten Hallo uitgevoerd dezelfde versie van Provider.
   >
   >
3. Hallo installatieprogramma controleert of en vraagt toestemming toostop Hallo VMM service toobegin installatie van de Provider. Hallo VMM-Service wordt opnieuw opgestart nadat setup is voltooid. Als u installeert op gevraagd een VMM-cluster, u moet toostop Hallo Cluster-rol.
4. U kunt zich in **Microsoft Update** aanmelden voor updates. Met deze instelling worden ingeschakeld Provider-updates geïnstalleerd op basis van beleid voor tooyour Microsoft Update.

    ![Microsoft-updates](./media/site-recovery-vmm-to-azure-classic/updates.png)
5. installatielocatie voor Provider is ingesteld, te Hallo Hallo**<SystemDrive>\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin**. Klik op **Install**.

   ![InstallLocation](./media/site-recovery-vmm-to-azure-classic/install-location.png)
6. Klik na het Hallo-Provider is geïnstalleerd op **registreren** tooregister Hallo-server in Hallo kluis.

    ![InstallComplete](./media/site-recovery-vmm-to-azure-classic/install-complete.png)
7. In **kluisnaam**, Controleer de naam van de Hallo van Hallo kluis in welke Hallo server wordt geregistreerd. Klik op *Volgende*.

    ![Serverregistratie](./media/site-recovery-vmm-to-azure-classic/vaultcred.PNG)
8. In **internetverbinding** opgeven hoe Hallo Provider die wordt uitgevoerd op Hallo VMM-server maakt verbinding toohello Internet. Selecteer **verbinding maken met bestaande proxyinstellingen** toouse Hallo standaardinstellingen voor internetverbindingen op Hallo-server geconfigureerd.

    ![Instellingen voor internet](./media/site-recovery-vmm-to-azure-classic/proxydetails.PNG)

   * Als u wilt dat toouse een aangepaste proxy u moet instellen voordat u Hallo Provider installeert. Wanneer u aangepaste proxyinstellingen configureert wordt een test toocheck Hallo proxyverbinding uitgevoerd.
   * Als u een aangepaste proxy gebruikt, of als uw standaardproxy verificatie vereist moet u tooenter Hallo proxy-gegevens, inclusief Hallo proxy-adres en poort.
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
13. Klik op **volgende** toocomplete Hallo proces. Na registratie worden metagegevens van Hallo VMM-server opgehaald door Azure Site Recovery. Hallo-server wordt weergegeven op Hallo **VMM-Servers** tabblad op Hallo **Servers** pagina in Hallo kluis.

    ![Laatste pagina](./media/site-recovery-vmm-to-azure-classic/provider13.PNG)

Na registratie worden metagegevens van Hallo VMM-server opgehaald door Azure Site Recovery. Hallo-server wordt weergegeven op Hallo **VMM-Servers** tabblad op Hallo **Servers** pagina in Hallo kluis.

### <a name="command-line-installation"></a>Installatie vanaf de opdrachtregel
Hello Azure Site Recovery Provider kan ook worden geïnstalleerd met behulp van de opdrachtregel na Hallo. Deze methode kan gebruikte tooinstall Hallo-provider op een Server Core voor Windows Server 2012 R2 zijn.

1. Hallo-Provider en de registratiesleutel sleutel tooa installatiemap downloaden. Bijvoorbeeld: C:\ASR.
2. Hallo System Center Virtual Machine Manager-service niet stoppen
3. Pak Hallo Provider-installatieprogramma met de volgende opdrachten vanaf een opdrachtprompt met verhoogde bevoegdheid:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Hallo-provider als volgt installeren:

        C:\ASR> setupdr.exe /i
5. Registreer Hallo Provider als volgt:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>       

Gebruik daarbij de volgende parameters:

* **/ Credentials** : verplichte parameter waarmee Hallo locatie in welke Hallo registratiesleutelbestand zich bevindt  
* **/ FriendlyName** : verplichte parameter voor de naam Hallo van Hallo Hyper-V-hostserver die wordt weergegeven in hello Azure Site Recovery-portal.
* **/ EncryptionEnabled** : een optionele parameter toospecify als u wilt dat tooencryption uw virtuele machines in Azure (versleuteling bij rust). Hallo-bestandsnaam mag hebben een **.pfx** extensie.
* **/ proxyaddress** : een optionele parameter waarmee het adres van de proxyserver Hallo Hallo.
* **/ proxyport** : optionele parameter waarmee het Hallo-poort van de proxyserver Hallo.
* **proxyusername** : optionele parameter waarmee de proxygebruikersnaam Hallo.
* **/ proxypassword** : optionele parameter waarmee het proxywachtwoord Hallo.  

## <a name="step-4-create-an-azure-storage-account"></a>Stap 4: Een Azure Storage-account maken
1. Als u geen Azure storage-account klikt u op **toevoegen van een Azure Storage-Account** toocreate een account.
2. Maak een account waarvoor geo-replicatie is ingeschakeld. Moet in dezelfde regio bevinden als hello Azure Site Recovery-service hello, en worden gekoppeld aan Hallo hetzelfde abonnement.

    ![Storage-account](./media/site-recovery-vmm-to-azure-classic/storage.png)

> [!NOTE]
> [Migratie van opslagaccounts](../azure-resource-manager/resource-group-move-resources.md) via resource groepen binnen hetzelfde abonnement Hallo of voor abonnementen wordt niet ondersteund voor storage-accounts gebruikt voor de implementatie van Site Recovery.
>
>

## <a name="step-5-install-hello-azure-recovery-services-agent"></a>Stap 5: Hello Azure Recovery Services-Agent installeren
Hello Azure Recovery Services-agent installeren op elke Hyper-V-hostserver in Hallo VMM-cloud.

1. Klik op **Quick Start** > **Azure Site Recovery Services Agent downloaden en installeren op hosts** tooobtain Hallo meest recente versie van Hallo agent-installatiebestand.

    ![Recovery Services-agent installeren](./media/site-recovery-vmm-to-azure-classic/install-agent.png)
2. Hallo-installatiebestand op elke Hyper-V-hostserver uitvoeren.
3. Op Hallo **controle van vereisten** pagina op **volgende**. Ontbrekende vereiste onderdelen worden automatisch geïnstalleerd.

    ![Vereisten voor de Recovery Services-agent](./media/site-recovery-vmm-to-azure-classic/agent-prereqs.png)
4. Op Hallo **installatie-instellingen** pagina, opgeven waar u tooinstall Hallo agent en selecteer Hallo cachelocatie waar back-upmetagegevens moeten worden geïnstalleerd. Klik vervolgens op **Installeren**.
5. Nadat de installatie is voltooid, klikt u op **sluiten** toocomplete Hallo-wizard.

    ![MARS-agent registreren](./media/site-recovery-vmm-to-azure-classic/agent-register.png)

### <a name="command-line-installation"></a>Installatie vanaf de opdrachtregel
U kunt ook Hallo Microsoft Azure Recovery Services-Agent installeren vanaf Hallo-opdrachtregel met de volgende opdracht:

    marsagentinstaller.exe /q /nu

## <a name="step-6-configure-cloud-protection-settings"></a>Stap 6: Cloudbeveiligingsinstellingen configureren
Nadat het Hallo-VMM-server is geregistreerd, kunt u cloudbeveiligingsinstellingen configureren. Hallo-optie is ingeschakeld **cloudgegevens synchroniseren met de kluis Hallo** wanneer u Hallo Provider hebt geïnstalleerd, zodat alle clouds op Hallo VMM server wordt weergegeven in Hallo <b>beveiligde Items</b> tabblad in Hallo kluis.

![Gepubliceerde cloud](./media/site-recovery-vmm-to-azure-classic/clouds-list.png)

1. Klik op de pagina snel starten Hallo **beveiliging instellen voor VMM-clouds**.
2. Op Hallo **beveiligde Items** tabblad, klikt u op Hallo cloud gewenste tooconfigure en ga toohello **configuratie** tabblad.
3. Selecteer in **Doel** de optie **Azure**.
4. In **Opslagaccount** Selecteer hello Azure-opslagaccount u voor replicatie gebruikt.
5. Stel **opgeslagen gegevens versleutelen** te**uit**. Deze instelling geeft aan dat de gegevens moeten worden versleuteld tijdens de replicatie tussen Hallo on-premises site en Azure.
6. In **Kopieerfrequentie** laat de standaardinstelling Hallo. Met deze waarde wordt bepaald hoe vaak gegevens moeten worden gesynchroniseerd tussen de bron- en doellocatie.
7. In **herstelpunten bewaren voor**, laat de standaardinstelling Hallo. Met een standaardwaarde nul wordt alleen Hallo meest recente herstelpunt voor een primaire virtuele machine opgeslagen op een replicahostserver.
8. In **frequentie van toepassingsconsistente momentopnamen**, laat de standaardinstelling Hallo. Deze waarde geeft aan hoe vaak toocreate momentopnamen. Momentopnamen gebruiken Volume Shadow Copy Service (VSS) tooensure die toepassingen zich in een consistente status wanneer Hallo momentopname wordt gemaakt.  Als u een waarde instelt, zorg er dan voor dat kleiner is dan het aantal aanvullende herstelpunten dat u configureert Hallo.
9. In **replicatie begintijd**, opgeven waarop de initiële replicatie van gegevens tooAzure wordt gestart. Hallo tijdzone op Hallo Hyper-V-hostserver wordt gebruikt. Het is raadzaam dat u plant dat de initiële replicatie Hallo tijdens de daluren.

    ![Replicatie-instellingen voor cloud](./media/site-recovery-vmm-to-azure-classic/cloud-settings.png)

Nadat u Hallo instellingen opslaan in een taak wordt gemaakt en kan worden gecontroleerd op Hallo **taken** tabblad. Alle Hyper-V-hostservers in VMM-broncloud Hallo zullen worden geconfigureerd voor replicatie.

Nadat ze zijn opgeslagen, cloudinstellingen kunnen worden gewijzigd op Hallo **configureren** tabblad toomodify Hallo locatie of doel doelopslagaccount past u moet de configuratie van de cloud Hallo tooremove en Hallo cloud vervolgens opnieuw te configureren. Houd er rekening mee dat als u wijzigt Hallo storage account Hallo wijzigen alleen voor virtuele machines die zijn ingeschakeld voor beveiliging toegepast wordt nadat Hallo storage-account is gewijzigd. Bestaande virtuele machines worden niet gemigreerd toohello nieuw opslagaccount.

## <a name="step-7-configure-network-mapping"></a>Stap 7: Netwerktoewijzing configureren
Voordat u begint met de netwerktoewijzing controleert u of virtuele machines op de bronserver VMM Hallo verbonden tooa VM-netwerk. Maak ook een of meer virtuele Azure-netwerken. Houd er rekening mee dat meerdere VM-netwerken kunnen bestaan uit toegewezen tooa één Azure-netwerk.

1. Klik op de pagina snel starten Hallo **netwerken toewijzen**.
2. Op Hallo **netwerken** tabblad, in **bronlocatie**, selecteer Hallo bron-VMM-server. Selecteer in **Doellocatie** de optie Azure.
3. In **bron** netwerken die een lijst met VM-netwerken die zijn gekoppeld aan de VMM-server Hallo worden weergegeven. In **doel** netwerken hello Azure netwerken die zijn gekoppeld aan het Hallo-abonnement worden weergegeven.
4. Selecteer Hallo bron-VM-netwerk en klik op **kaart**.
5. Op Hallo **een doelnetwerk selecteren** pagina, selecteer Hallo doelnetwerk in Azure gewenste toouse.
6. Klik op Hallo vinkje toocomplete Hallo toewijzingsproces.

    ![Replicatie-instellingen voor cloud](./media/site-recovery-vmm-to-azure-classic/map-networks.png)

Nadat u Hallo instellingen opslaan een taak begint tootrack Hallo toewijzing uitgevoerd en deze kan worden gecontroleerd op het tabblad Hallo-taken. Alle bestaande gerepliceerde virtuele machines die overeenkomen met toohello bron-VM-netwerk worden verbonden toohello gericht op Azure-netwerken. Nieuwe virtuele machines die verbonden toohello bron-VM-netwerk zijn is verbonden toohello toegewezen Azure-netwerk na de replicatie. Als u een bestaande toewijzing met een nieuw netwerk wijzigt, worden gerepliceerde virtuele machines verbonden met de nieuwe instellingen Hallo.

Houd er rekening mee dat als Hallo doelnetwerk meerdere subnetten heeft en een van deze subnetten Hallo heeft dezelfde naam als het subnet waarop Hallo bron virtual machine zich bevindt, wordt Hallo replica virtuele machine na een failover worden verbonden toothat Doelsubnet. Als er geen Doelsubnet met een overeenkomende naam, wordt de Hallo virtuele machine verbonden toohello eerste subnet in het Hallo-netwerk zijn.

> [!NOTE]
> [Migratie van netwerken](../azure-resource-manager/resource-group-move-resources.md) via resource groepen binnen hetzelfde abonnement Hallo of voor abonnementen wordt niet ondersteund voor netwerken gebruikt voor de implementatie van Site Recovery.
>
>

## <a name="step-8-enable-protection-for-virtual-machines"></a>Stap 8: Beveiliging voor virtuele machines inschakelen
Nadat de servers, clouds en netwerken correct zijn geconfigureerd, kunt u beveiliging voor virtuele machines in de cloud Hallo inschakelen. Let op Hallo volgende:

* Virtuele machines moeten voldoen aan [Azure-vereisten](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
* tooenable beveiliging Hallo-besturingssysteem en de schijfeigenschappen besturingssysteem moeten worden ingesteld voor Hallo virtuele machine. Wanneer u een virtuele machine in VMM met een virtuele machine-sjabloon maakt, kunt u Hallo-eigenschap instellen. U kunt deze eigenschappen voor de bestaande virtuele machines ook instellen op Hallo **algemene** en **hardwareconfiguratie** tabbladen van de eigenschappen van de virtuele machine Hallo. Als u deze eigenschappen niet ingesteld in VMM, moet u kunnen tooconfigure ze in hello Azure Site Recovery-portal.

    ![Virtuele machine maken](./media/site-recovery-vmm-to-azure-classic/enable-new.png)

    ![Eigenschappen van de virtuele machine wijzigen](./media/site-recovery-vmm-to-azure-classic/enable-existing.png)

1. tooenable beveiliging, op Hallo **virtuele Machines** tabblad Hallo cloud welke Hallo virtuele machine zich bevindt, klikt u op **beveiliging inschakelen** > **virtuele machinestoevoegen**.
2. Selecteer in lijst Hallo van virtuele machines in de cloud Hallo Hallo een gewenste tooprotect.

    ![Beveiliging van de virtuele machine inschakelen](./media/site-recovery-vmm-to-azure-classic/select-vm.png)

    Voortgang van Hallo volgen **beveiliging inschakelen** actie in Hallo **taken** tabblad, met inbegrip van Hallo initiële replicatie. Na het Hallo **beveiliging voltooien** taak wordt uitgevoerd Hallo virtuele machine is gereed voor failover. Nadat de beveiliging is ingeschakeld en virtuele machines zijn gerepliceerd, moet u kunnen tooview ze in Azure.

    ![Beveiligingstaak voor virtuele machines](./media/site-recovery-vmm-to-azure-classic/vm-jobs.png)

1. Controleer de eigenschappen van de virtuele machine Hallo en wijzig zo nodig.

    ![Virtuele machines controleren](./media/site-recovery-vmm-to-azure-classic/vm-properties.png)
2. Op Hallo **configureren** tabblad van de eigenschappen van de virtuele machine Hallo volgende netwerkeigenschappen kan worden gewijzigd.

* **Het aantal netwerkadapters op de virtuele doelmachine Hallo** -Hallo aantal netwerkadapters wordt bepaald door het Hallo-grootte die u voor de virtuele doelmachine Hallo opgeeft. Controleer [specificaties van de grootte van de virtuele machine](../virtual-machines/linux/sizes.md) voor het aantal adapters die worden ondersteund door de grootte van de virtuele machine Hallo Hallo. Wanneer u Hallo grootte voor een virtuele machine wijzigen en het Hallo-instellingen opslaan, wijzigen Hallo aantal netwerkadapters Hallo wanneer u Hallo opent **configureren** pagina. Hallo aantal netwerkadapters van de virtuele doelmachines is Hallo minimum aantal netwerkadapters op de bron virtuele machine en Hallo maximum aantal netwerkadapters wordt ondersteund door de grootte Hallo van Hallo gekozen virtuele machine, als volgt:

  * Als het aantal netwerkadapters op de bronmachine Hallo Hallo kleiner dan of gelijk aantal adapters toohello toegestaan voor de doelgrootte machine Hallo vervolgens Hallo doel hetzelfde aantal adapters als bron Hallo Hallo.
  * Als het aantal adapters voor de virtuele bronmachine Hallo HALLO hallo maximum overschrijden voor Hallo doelgrootte, wordt maximaal Hallo doel wordt gebruikt.
  * Als een bronmachine twee netwerkadapters heeft en de grootte van Hallo doelmachine vier ondersteunt, wordt Hallo doelmachine twee adapters hebben. Als Hallo-bronmachine twee adapters heeft, maar hello ondersteunde doelgrootte biedt alleen ondersteuning voor een hebben Hallo doelmachine slechts één adapter.     
* **Netwerk van de virtuele doelmachine Hallo** -Hallo netwerk toowhich Hallo virtuele machine verbinding maakt toois bepaald door de netwerktoewijzing van Hallo-netwerk van de virtuele bronmachine. Als de virtuele bronmachine Hallo zijn meer dan één netwerkadapter en de brontabel netwerken toegewezen toodifferent doelnetwerken, dan u toochoose tussen een van de doelnetwerken Hallo moet.
* **Subnet van elke netwerkadapter** : voor elke netwerkadapter Hallo subnet toowhich Hallo failover van virtuele machine kunt u verbinding maakt.
* **Doel-IP-adres** - als Hallo-netwerkadapter van de virtuele bronmachine geconfigureerde toouse een statische IP-adressen kunt u Hallo IP-adres opgeven voor de virtuele doelmachine Hallo is. Gebruik deze functie Hallo IP-adres van een virtuele bronmachine te behouden na een failover. Als geen IP-adres is opgegeven, kunnen een beschikbaar IP-adres wordt toohello netwerkadapter gegeven op Hallo moment van failover. Als de IP-doeladres hello wordt opgegeven, maar wordt al gebruikt door een andere virtuele machine in Azure wordt uitgevoerd, mislukt de failover.  

    ![Netwerkeigenschappen wijzigen](./media/site-recovery-vmm-to-azure-classic/multi-nic.png)

> [!NOTE]
> Virtuele Linux-machines met een statisch IP-adres worden niet ondersteund.
>
>

## <a name="test-hello-deployment"></a>Hallo-implementatie testen
tootest plannen voor uw implementatie kunt u een testfailover voor één virtuele machine uitvoeren of maken van een herstelplan dat bestaat uit meerdere virtuele machines en een testfailover voor Hallo uitvoeren.  

Met een testfailover wordt uw failover- en herstelmechanisme in een geïsoleerd netwerk gesimuleerd. Opmerking:

* Als u tooconnect toohello virtuele machine in Azure met extern bureaublad na een failover Hallo wilt, moet u verbinding met extern bureaublad inschakelen op Hallo virtuele machine voordat u Hallo testfailover uitvoeren.
* Na een failover moet u een openbaar IP-adres tooconnect-toohello virtuele Azure-machine via Extern bureaublad gebruiken. Als u toodo dit wilt, zorg ervoor dat u geen domeinbeleid hebt geïmplementeerd die verhinderen dat u verbinding maakt tooa virtuele machine via een openbaar adres.

> [!NOTE]
> tooget hello optimale prestaties wanneer u een failover tooAzure, zorg ervoor dat u hebt geïnstalleerd hello Azure Hallo VM-agent. Dit zorgt ervoor dat u sneller kunt opstarten en dat problemen sneller worden opgelost. Hallo downloaden [Linux-agent](https://github.com/Azure/WALinuxAgent), of Hallo [Windows-agent](http://go.microsoft.com/fwlink/?LinkID=394789).
>
>

### <a name="create-a-recovery-plan"></a>Een herstelplan maken
1. Op Hallo **herstelplannen** tabblad, het toevoegen van een nieuw plan. Geef een naam **VMM** in **gegevensbrontype**, en Hallo bron VMM-beheerserver in **bron**. Hallo doel worden Azure.

    ![Herstelplan maken](./media/site-recovery-vmm-to-azure-classic/recovery-plan1.png)
2. In Hallo **virtuele Machines selecteren** pagina, selecteer virtuele machines tooadd toohello herstelplan. Deze virtuele machines worden toegevoegd standaardgroep herstel toohello: groep 1. Er zijn maximaal 100 virtuele machines in één herstelplan getest.

* Als u wilt dat de eigenschappen van de virtuele machine Hallo tooverify voordat u deze toohello plan toevoegt, klikt u op Hallo virtuele machine op de eigenschappenpagina Hallo van Hallo cloud waarin deze zich bevindt. U kunt ook de eigenschappen van de virtuele machine Hallo configureren in Hallo VMM-console.
* Alle Hallo virtuele machines die worden weergegeven zijn ingeschakeld voor beveiliging. Hallo-lijst bevat zowel virtuele machines die zijn ingeschakeld voor beveiliging en initiële replicatie is voltooid, en die zijn ingeschakeld voor beveiliging met initiële replicatie in behandeling. Alleen voor virtuele machines waarvoor de eerste replicatie is voltooid, kan een failover als onderdeel van een herstelplan worden uitgevoerd.

    ![Herstelplan maken](./media/site-recovery-vmm-to-azure-classic/select-rp.png)

Nadat een herstelplan is gemaakt wordt weergegeven in Hallo **herstelplannen** tabblad. U kunt ook toevoegen [Azure automation-runbooks](site-recovery-runbook-automation.md) toohello plan tooautomate herstelacties tijdens failover.

### <a name="run-a-test-failover"></a>Een testfailover uitvoeren
Er zijn twee manieren toorun een test failover tooAzure.

* **Testfailover zonder een Azure-netwerk**: dit type testfailover wordt gecontroleerd dat de virtuele machine Hallo voordoet correct in Azure. Hallo virtuele machine niet verbonden tooany Azure-netwerk na een failover.
* **Testfailover met een Azure-netwerk**: dit type failover controleert of de volledige replicatieomgeving Hallo maximaal zoals verwacht wordt geleverd en die failover Hallo virtuele machines worden verbonden toohello opgegeven doelnetwerk in Azure. Voor het verwerken van een subnet voor de testfailover wordt Hallo subnet van de virtuele testmachine Hallo worden doorberekend af op basis van het subnet van de virtuele replicamachine Hallo Hallo. Dit is de verschillende tooregular replicatie wanneer Hallo subnet van een replica virtuele machine is gebaseerd op het subnet van de virtuele bronmachine Hallo Hallo.

Als u een testfailover toorun voor een virtuele machine ingeschakeld voor beveiliging tooAzure zonder op te geven van een Azure-doelnetwerk wilt hoeft u niet tooprepare alles. toorun een testfailover met een doel-Azure-netwerk u een nieuw Azure-netwerk dat is geïsoleerd toocreate van uw Azure productienetwerk (standaardwerking moet wanneer u een nieuw netwerk in Azure maakt). Kijken hoe te[een testfailover uitvoeren](site-recovery-failover.md) voor meer informatie.

U moet ook tooset Hallo infrastructuur voor Hallo gerepliceerde virtuele machine toowork zoals verwacht. Bijvoorbeeld, een virtuele machine met de domeincontroller en DNS-gerepliceerde tooAzure met Azure Site Recovery kan worden en kunnen worden gemaakt in Hallo testnetwerk met Testfailover. Zie [Testfailover-overwegingen voor Active Directory](site-recovery-active-directory.md#test-failover-considerations) voor meer informatie.

een testfailover toorun Hallo te volgen:

1. Op Hallo **herstelplannen** tabblad, selecteer Hallo-plan en klik op **Testfailover**.
2. Op Hallo **Testfailover bevestigen** pagina **geen** of een specifieke Azure-netwerk.  Houd er rekening mee dat als u geen Hallo testfailover wordt selecteert Controleer of de virtuele machine Hallo gerepliceerd correct tooAzure maar configuratie van het replicatienetwerk niet gecontroleerd.

    ![Geen netwerk](./media/site-recovery-vmm-to-azure-classic/test-no-network.png)
3. Als gegevensversleuteling is ingeschakeld voor Hallo-cloud in **versleutelingssleutel** Selecteer Hallo-certificaat dat is uitgegeven tijdens de installatie van Provider Hallo op Hallo VMM-server bij het inschakelen van Hallo optie tooenable gegevensversleuteling voor een cloud .
4. Op Hallo **taken** tabblad kunt u failover voortgang bijhouden. U moet ook kunnen toosee Hallo virtuele machine testreplica in hello Azure-portal. Als u van uw on-premises netwerk tooaccess virtuele machines alles hebt ingesteld, kunt u een extern bureaublad verbinding toohello virtuele machine starten.
5. Wanneer failover Hallo Hallo bereikt **testen voltooien** fase, klikt u op **volledige Test** toofinish deze. U kunt inzoomen van toohello **taak** tootrack failover voortgang en status en tooperform tabblad acties die nodig zijn.
6. Na een failover ziet u Hallo testreplica van virtuele machine in hello Azure-portal. Als u van uw on-premises netwerk tooaccess virtuele machines alles hebt ingesteld, kunt u een extern bureaublad verbinding toohello virtuele machine starten. Hallo te volgen:

   1. Controleren of Hallo virtuele machines worden gestart.
   2. Als u tooconnect toohello virtuele machine in Azure met extern bureaublad na een failover Hallo wilt, moet u verbinding met extern bureaublad inschakelen op Hallo virtuele machine voordat u Hallo testfailover uitvoeren. U moet ook tooadd een RDP-eindpunt op Hallo virtuele machine. U kunt gebruikmaken van een [Azure Automation-Runbooks](site-recovery-runbook-automation.md) toodo die.
   3. Na een failover als u een openbaar IP-adres tooconnect toohello virtuele machine in Azure met behulp van extern bureaublad gebruikt, zorg ervoor dat u geen domeinbeleid hebt geïmplementeerd die verhinderen dat u verbinding maakt tooa virtuele machine via een openbaar adres.
7. Voer Hallo te volgen nadat Hallo testen voltooid is:

   * Klik op **Hallo testfailover is voltooid**. Hallo opschonen omgeving tooautomatically power testen uit en verwijdert u Hallo test-virtuele machines.
   * Klik op **notities** toorecord en eventuele opmerkingen die zijn gekoppeld aan de testfailover Hallo op te slaan.


## <a name="next-steps"></a>Volgende stappen
Meer informatie over [herstelplannen maken](site-recovery-create-recovery-plans.md) en [failover](site-recovery-failover.md).
