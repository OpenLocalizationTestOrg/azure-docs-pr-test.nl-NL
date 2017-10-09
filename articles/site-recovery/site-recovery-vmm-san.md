---
title: aaaReplicate Hyper-V-machines in VMM met SAN met behulp van Azure Site Recovery | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooreplicate Hyper-V virtuele machines tussen twee sites met Azure Site Recovery SAN-replicatie.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: eb480459-04d0-4c57-96c6-9b0829e96d65
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: cee4ff519a8e9e7f29e17e923a9533fb339634b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-in-vmm-clouds-tooa-secondary-site-with-azure-site-recovery-by-using-san"></a>Hyper-V-machines in VMM-clouds tooa secundaire site met Azure Site Recovery repliceren met behulp van SAN


Gebruik dit artikel als u wilt dat toodeploy [Azure Site Recovery](site-recovery-overview.md) toomanage replicatie van Hyper-V-machines (beheerd in System Center Virtual Machine Manager-clouds) tooa secundaire VMM-site, met behulp van Azure Site Recovery in de klassieke portal Hallo. Dit scenario is niet beschikbaar in de nieuwe Azure portal Hallo.



Na de eventuele opmerkingen aan Hallo einde van dit artikel. Vind antwoorden tootechnical vragen in Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="why-replicate-with-san-and-site-recovery"></a>Waarom repliceren met SAN- en Site Recovery?

* SAN biedt een replicatieoplossing op bedrijfsniveau, schaalbare, zodat een primaire site met Hyper-V met SAN LUN's tooa secundaire site met SAN kan worden gerepliceerd. Opslag wordt beheerd door VMM en replicatie en failover wordt beheerd met Site Recovery.
* Site Recovery heeft samengewerkt met verschillende [SAN-opslag partners](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx) tooprovide Fibre Channel en iSCSI-opslag gerepliceerd.  
* Gebruik uw bestaande SAN-infrastructuur tooprotect bedrijfskritieke apps geïmplementeerd in Hyper-V-clusters. Virtuele machines kunnen worden gerepliceerd als een groep, zodat u apps met N-aantal lagen failover mogelijk consistent.
* SAN-replicatie zorgt voor replicatieconsistentie in verschillende lagen van een toepassing met gesynchroniseerde replicatie voor de laag RTO en RPO en asynchrone uitvoering replicatie voor hoge flexibiliteit (afhankelijk van de mogelijkheden van uw opslagmatrix).  
* U kunt SAN-opslag in VMM fabric Hallo beheren en SMI-S in VMM toodiscover bestaande opslag gebruiken.  

Opmerking:
- Replicatie van site-naar-site met SAN is niet beschikbaar in hello Azure-portal. De optie is alleen beschikbaar in de klassieke portal Hallo. Nieuwe kluizen kunnen niet worden gemaakt in de klassieke portal Hallo. Bestaande kluizen kunnen worden beheerd.
- Replicatie van SAN tooAzure wordt niet ondersteund.
- Gedeelde vhdx-bestanden kan niet worden gerepliceerd of logische eenheden (LUN's) die rechtstreeks zijn verbonden tooVMs via iSCSI of Fibre Channel. Gastclusters kunnen worden gerepliceerd.


## <a name="architecture"></a>Architectuur

![SAN-architectuur](./media/site-recovery-vmm-san/architecture.png)

- **Azure**: instellen van een Site Recovery-kluis in hello Azure-portal.
- **SAN-opslag**: SAN-opslag in Hallo VMM fabric wordt beheerd. U Hallo opslagprovider toevoegen, opslagcategorieën aanmaken en instellen van de opslaggroepen.
- **VMM en Hyper-V**: We raden aan een VMM-server op elke site. Instellen van VMM-privéclouds en Hyper-V-clusters in die clouds plaatsen. Tijdens de implementatie hello Azure Site Recovery Provider is geïnstalleerd op elke VMM-server en Hallo-server is geregistreerd in kluis Hallo. Hallo Provider communiceert met de Hallo Site Recovery service toomanage replicatie, failover en failback.
- **Replicatie**: nadat u opslag in VMM installeren en configureren van replicatie in Site Recovery, replicatie tussen Hallo primaire en secundaire SAN-opslag. Er zijn geen replicatiegegevens verzonden tooSite herstel.
- **Failover**: inschakelen-failover in Hallo Site Recovery-portal. Er is geen gegevens verloren gaan tijdens de failover omdat replicatie synchroon is.
- **Failback**: toofail achter, inschakelen van omgekeerde replicatie tootransfer deltawijzigingen van Hallo secundaire site toohello primaire site. Als omgekeerde replicatie voltooid is, kunt u een geplande failover uitvoeren vanaf de secundaire tooprimary. Deze geplande failover Hallo replica VMs stopt op de secundaire site Hallo en ze op de primaire site Hallo gestart.


## <a name="before-you-start"></a>Voordat u begint


**Vereisten** | **Details**
--- | ---
**Azure** |U hebt een [Microsoft Azure](https://azure.microsoft.com/)-account nodig. U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/). [Meer informatie](https://azure.microsoft.com/pricing/details/site-recovery/) over prijzen voor Site Recovery. Een Azure Site Recovery-kluis tooconfigure maken en beheren van replicatie en failover.
**VMM** | U kunt gebruiken één VMM-server en andere clouds repliceren, maar we raden aan één VMM in Hallo primaire site en één in Hallo secundaire site. VMM kan worden geïmplementeerd als een fysieke of virtuele zelfstandige server of als een cluster. <br/><br/>Hallo VMM-server moet worden uitgevoerd op System Center 2012 R2 of hoger met Hallo meest recente cumulatieve updates.<br/><br/> U moet ten minste één cloud zijn geconfigureerd op Hallo primaire VMM-server u wilt dat tooprotect en één cloud zijn geconfigureerd op de secundaire VMM-server Hallo gewenste toouse voor failover.<br/><br/> Hallo-broncloud moet een of meer VMM-hostgroepen bevatten.<br/><br/> Alle VMM-clouds moeten Hallo Hyper-V Capaciteitsprofiel ingesteld hebben.<br/><br/> Zie voor meer informatie over het instellen van VMM-clouds [implementeren van een privécloud VM](https://technet.microsoft.com/en-us/system-center-docs/vmm/scenario/cloud-overview).
**Hyper-V** | U moet een of meer Hyper-V-clusters in primaire en secundaire VMM-clouds.<br/><br/> Hallo bron Hyper-V-cluster moet een of meer virtuele machines bevatten.<br/><br/> Hallo VMM-hostgroepen in de primaire en secundaire sites Hallo moeten ten minste één van de Hyper-V-clusters Hallo bevatten.<br/><br/>Hallo host- en Hyper-V-servers moet worden uitgevoerd op Windows Server 2012 of hoger met Hallo Hyper-V-rol en Hallo meest recente updates zijn geïnstalleerd.<br/><br/> Als u Hyper-V in een cluster uitvoert en een statische IP-adressen gebaseerde cluster hebt, zijn de clusterbroker niet automatisch gemaakt. U moet deze handmatig configureren. Zie voor meer informatie [hostclusters voor Hyper-V replica voorbereiden](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters).
**SAN-opslag** | U kunt guest geclusterde virtuele machines met iSCSI of channel-opslag of met behulp van gedeelde virtuele harde schijven (vhdx) repliceren.<br/><br/> U moet twee SAN-matrices: een in Hallo primaire site en één in Hallo secundaire site.<br/><br/> Een netwerkinfrastructuur moet worden ingesteld tussen Hallo matrices. Peering en replicatie moeten worden geconfigureerd. Replicatie-licenties moeten worden ingesteld in overeenstemming met de opslagvereisten matrix Hallo.<br/><br/>Stel netwerken tussen Hallo Hyper-V-hostservers en Hallo opslagmatrix zodat hosts met opslag-LUN's communiceren kunnen met behulp van iSCSI of Fibre Channel.<br/><br/> Controleer [ondersteunde opslagmatrices](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx).<br/><br/> SMI-S-providers van fabrikanten van opslag-matrix moeten worden geïnstalleerd en Hallo SAN-matrices moeten worden beheerd door Hallo-provider. Hallo Provider volgens toomanufacturer instructies instellen.<br/><br/>Zorg ervoor dat Hallo-matrix SMI-S-provider zich op een server die Hallo VMM server toegankelijk via Hallo-netwerk met een IP-adres of FQDN-naam.<br/><br/> Elke SAN-matrix moet een of meer beschikbare opslaggroepen hebben.<br/><br/> Hallo primaire VMM-server Hallo primaire matrix moet beheren en secundaire VMM-server Hallo Hallo secundaire matrix moet beheren.
**Netwerktoewijzing** | Stel netwerktoewijzing zodat gerepliceerde virtuele machines optimaal op secundaire Hyper-V-hostservers zijn geplaatst na een failover en dat ze zijn verbonden tooappropriate VM-netwerken. Als u geen netwerktoewijzing configureert, niet replica VMs verbonden tooany netwerk na een failover.<br/><br/> Zorg ervoor dat VMM netwerken correct zijn geconfigureerd zodat u netwerktoewijzing tijdens de implementatie van Site Recovery kunt instellen. In VMM moet Hallo VM's op de bronhost Hyper-V Hallo verbonden tooa VMM VM-netwerk. Dit netwerk moet gekoppelde tooa logisch netwerk dat is gekoppeld aan Hallo cloud.<br/><br/> Hallo doelcloud moet een bijbehorende VM-netwerk hebt en deze gekoppelde tooa bijbehorende logisch netwerk dat is gekoppeld aan Hallo doelcloud op zijn beurt moet worden.<br/><br/>.

## <a name="step-1-prepare-hello-vmm-infrastructure"></a>Stap 1: Hallo VMM infrastructuur voorbereiden
tooprepare uw VMM-infrastructuur, moet u:

1. Controleer of de VMM-clouds.
2. Integreren en classificeren van SAN-opslag in VMM.
3. LUN's maken en toewijzen van opslag.
4. Replicatiegroepen maken.
5. Stel VM-netwerken.

### <a name="verify-vmm-clouds"></a>Controleer of de VMM-clouds

Zorg ervoor dat de VMM-clouds correct zijn ingesteld voordat u begint met implementatie van Site Recovery.

### <a name="integrate-and-classify-san-storage-in-hello-vmm-fabric"></a>Integreren en SAN-opslag in VMM fabric Hallo classificeren

1. Hallo VMM-console, ga te**Fabric** > **opslag** > **Resources toevoegen** > **opslagapparaten**.
2. In Hallo **opslagapparaten toevoegen** wizard selecteert u **Selecteer een type opslagprovider** en selecteer **SAN- en NAS-apparaten gedetecteerd en beheerd door een SMI-S-provider**.

    ![Type provider](./media/site-recovery-vmm-san/provider-type.png)

3. Op Hallo **Protocol opgeven en het adres van de SMI-S-opslagprovider Hallo** pagina **SMI-S CIMXML** en Hallo-instellingen voor verbinding toohello provider opgeven.
4. In **Provider IP-adres of FQDN-naam** en **TCP/IP-poort**, Hallo-instellingen voor verbinding toohello provider opgeven. U kunt alleen een SSL-verbinding voor de SMI-S CIMXML gebruiken.

    ![Provider verbinding maken](./media/site-recovery-vmm-san/connect-settings.png)
5. In **Run as-account**, VMM uitvoeren als-account die u kunt toegang krijgen tot Hallo-provider of maak een account opgeven.
6. Op Hallo **informatie verzamelen** pagina VMM probeert automatisch importeren en toodiscover Hallo informatie over opslagapparaten. detectie van tooretry, klikt u op **Provider scannen**. Als het detectieproces Hallo slaagt, gedetecteerd Hallo opslagmatrices, opslaggroepen, de fabrikant, model en capaciteit op Hallo pagina worden weergegeven.

    ![Opslag detecteren](./media/site-recovery-vmm-san/discover.png)
7. In **storage pools tooplace onder beheer selecteren en toewijzen van een classificatie**, selecteer de opslaggroepen Hallo VMM beheerd en ze een classificatie toewijzen. LUN-gegevens worden geïmporteerd vanaf Hallo opslaggroepen. Maken van LUN's die zijn gebaseerd op Hallo toepassingen moet u tooprotect, hun capaciteitsvereisten en uw vereisten voor wat tooreplicate samen nodig heeft.

    ![Opslag classificeren](./media/site-recovery-vmm-san/classify.png)

### <a name="create-luns-and-allocate-storage"></a>LUN's maken en toewijzen van opslag

Maken van LUN's die zijn gebaseerd op Hallo toepassingen moet u tooprotect capaciteitsvereisten en uw vereisten voor wat tooreplicate samen nodig heeft.

1. Nadat het Hallo-opslag in VMM fabric hello wordt weergegeven, kunt u [inrichten van LUN's](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-storage-host-groups#create-a-lun-in-vmm).

     > [!NOTE]
     > Geen VHD's voor VM die zijn ingeschakeld voor replicatie tooLUNs Hallo niet toevoegen. Als deze LUN's niet in een replicatiegroep voor de Site Recovery, won't ze worden gedetecteerd door Site Recovery.
     >

2. Toegewezen opslag capaciteit toohello Hyper-V-hostcluster zodat VMM virtuele machine toohello ingericht gegevensopslag kunt implementeren:

   * Voordat u toohello opslagcluster toewijzen, moet u tooallocate deze toohello VMM-hostgroep op welke Hallo cluster zich bevindt. Zie voor meer informatie [hoe tooallocate opslag logische eenheden tooa hostgroep in VMM](https://technet.microsoft.com/library/gg610686.aspx) en [hoe tooallocate opslaggroepen tooa hostgroep in VMM](https://technet.microsoft.com/library/gg610635.aspx).
   * Opslagcluster capaciteit toohello toewijzen, zoals beschreven in [hoe tooconfigure opslag op een host met Hyper-V-cluster in VMM](https://technet.microsoft.com/library/gg610692.aspx).

    ![Type provider](./media/site-recovery-vmm-san/provider-type.png)
3. In **Protocol opgeven en het adres van de SMI-S-opslagprovider Hallo**, selecteer **SMI-S CIMXML**. Hallo-instellingen opgeven voor het verbinden van toohello provider. Alleen voor de SMI-S CIMXML kunt u een SSL-verbinding.

    ![Provider verbinding maken](./media/site-recovery-vmm-san/connect-settings.png)
4. In **Run as-account**, VMM uitvoeren als-account die u kunt toegang krijgen tot Hallo-provider of maak een account opgeven.
5. In **informatie verzamelen**, VMM probeert automatisch importeren en toodiscover Hallo informatie over opslagapparaten. Als u tooretry nodig hebt, klikt u op **Provider scannen**. Als het detectieproces Hallo is geslaagd, Hallo opslagmatrices, worden opslaggroepen, de fabrikant, model en capaciteit weergegeven op de pagina Hallo.

    ![Opslag detecteren](./media/site-recovery-vmm-san/discover.png)
7. In **storage pools tooplace onder beheer selecteren en toewijzen van een classificatie**, selecteer de opslaggroepen Hallo dat VMM wordt beheren en hieraan een classificatie. LUN-gegevens worden geïmporteerd vanaf Hallo opslaggroepen.

    ![Opslag classificeren](./media/site-recovery-vmm-san/classify.png)


### <a name="create-replication-groups"></a>Replicatiegroepen maken

Een replicatiegroep met alle Hallo-LUN's die tooreplicate samen moet maken.

1. Open in de VMM-console Hallo Hallo **replicatiegroepen** tabblad Eigenschappen van de matrix Hallo opslag en klik vervolgens op **nieuw**.
2. Hallo replicatiegroep maken.

    ![Groep voor SAN-replicatie](./media/site-recovery-vmm-san/rep-group.png)

### <a name="set-up-networks"></a>Stel netwerken

Als u de netwerktoewijzing tooconfigure wilt, Hallo te volgen:

1. Site Recovery netwerktoewijzing zien.
2. Bereid VM-netwerken in VMM voor:

   * [Stel logische netwerken in](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-logical-networks).
   * [Stel VM-netwerken in](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-vm-networks).


## <a name="step-2-create-a-vault"></a>Stap 2: Een kluis maken

1. Meld u aan toohello [Azure-portal](https://portal.azure.com) van Hallo VMM-server die u wilt tooregister in Hallo kluis.
2. Vouw **Data Services** > **Recovery Services**, en klik vervolgens op **Site Recovery-kluis**.
3. Klik op **Nieuw maken** > **Snelle invoer**.
4. In **naam**, voer een beschrijvende naam tooidentify Hallo-kluis.
5. In **regio**, selecteer de geografische regio voor de kluis Hallo Hallo. toocheck ondersteunde regio's, Zie [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Klik op **Kluis maken**.

    ![Nieuwe kluis](./media/site-recovery-vmm-san/create-vault.png)

Selectievakje Hallo status balk tooconfirm die Hallo kluis is gemaakt. Hallo-kluis wordt weergegeven als **Active** op Hallo belangrijkste **Recovery Services** pagina.

### <a name="register-hello-vmm-servers"></a>Hallo VMM-servers registreren

1. Open Hallo **Quick Start** pagina uit Hallo **Recovery Services** pagina. Snel starten kan ook op elk gewenst moment worden geopend door te kiezen Hallo-pictogram.

    ![Pictogram Snel starten](./media/site-recovery-vmm-san/quick-start-icon.png)
2. Selecteer in de vervolgkeuzelijst hello, **tussen Hyper-V lokale site met behulp van replicatie van de matrix**.

    ![Registratiesleutel](./media/site-recovery-vmm-san/select-san.png)
3. In **VMM-servers voorbereiden**, download de nieuwste versie Hallo van hello Azure Site Recovery Provider-installatiebestand.
4. Voer dit bestand op Hallo bron-VMM-server. Als VMM in een cluster is geïmplementeerd en u Hallo Provider voor Hallo eerst installeert, Hallo Provider installeren op een actief knooppunt- en eindtijd Hallo installatie tooregister Hallo VMM-server in Hallo kluis. Installeer vervolgens Hallo Provider op Hallo andere knooppunten. Als u een Hallo Provider upgrade uitvoert, moet u tooupgrade op alle knooppunten zodat ze dezelfde versie van Provider hebt Hallo.
5. Hallo-installatieprogramma controleert de vereisten en aanvragen machtiging toostop Hallo VMM service toobegin Provider setup. Hallo-service wordt opnieuw opgestart nadat setup is voltooid. Op een VMM-cluster, moet u na vragen aan gebruiker toostop Hallo Cluster-rol.
6. In **Microsoft Update**, kunt u zich aanmelden voor updates en updates van de Provider worden geïnstalleerd op basis van beleid voor tooyour Microsoft Update.

    ![Microsoft-updates](./media/site-recovery-vmm-san/ms-update.png)

7. Hallo-installatielocatie voor Provider Hallo is standaard <SystemDrive>\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin. Klik op **installeren** toobegin.

    ![Installatielocatie](./media/site-recovery-vmm-san/install-location.png)

8. Nadat het Hallo-Provider is geïnstalleerd, klikt u op **registreren** tooregister Hallo VMM-server in Hallo kluis.

    ![De installatie is voltooid](./media/site-recovery-vmm-san/install-complete.png)

9. In **internetverbinding**, opgeven hoe door Hallo Provider toohello Internet verbinding maakt. Selecteer **standaardsysteemproxyinstellingen gebruiken** als u wilt dat toouse Hallo standaardinstellingen voor internetverbindingen op Hallo-server.

    ![Instellingen voor internet](./media/site-recovery-vmm-san/proxy-details.png)

   * Desgewenst kunt u een aangepaste proxy toouse instellen voordat u Hallo Provider installeert. Wanneer u aangepaste proxyinstellingen configureert, wordt een test uitgevoerd toocheck Hallo proxyverbinding.
   * Als u een aangepaste proxy gebruikt, of als uw standaardproxy verificatie vereist, moet u Hallo proxy-gegevens, inclusief Hallo-adres en poort.
   * Hallo vereist dat URL 's moet toegankelijk zijn vanaf Hallo VMM-server.
   * Als u een aangepaste proxy gebruikt, VMM uitvoeren als-account (DRAProxyAccount) automatisch is gemaakt met behulp van Hallo opgegeven proxyreferenties. Hallo-proxyserver zodanig configureren dat dit account kan worden geverifieerd. U kunt Hallo Run As-accountinstellingen in de VMM-console Hallo wijzigen (**instellingen** > **beveiliging** > **Run As-Accounts**  >  **DRAProxyAccount**). U moet de VMM-service voor Hallo wijziging tootake effect Hallo opnieuw.
10. In **registratiesleutel**, selecteer Hallo-sleutel die u hebt gedownload van Hallo portal en gekopieerde toohello VMM-server.
11. In **kluisnaam**, Controleer de naam van de Hallo van Hallo kluis in welke Hallo server wordt geregistreerd.

    ![Serverregistratie](./media/site-recovery-vmm-san/vault-creds.png)
12. Hallo-instelling voor wachtwoordversleuteling wordt alleen gebruikt voor VMM tooAzure replicatie. U kunt deze negeren.

    ![Serverregistratie](./media/site-recovery-vmm-san/encrypt.png)
13. In **servernaam**, Geef een beschrijvende naam tooidentify Hallo VMM-server in Hallo kluis. Geef in een clusterconfiguratie Hallo VMM-clusterrolnaam op.
14. In **initiële synchronisatie van metagegevens van cloud**, selecteer of u toosynchronize metagegevens wilt maken voor alle clouds op Hallo VMM-server. Deze actie hoeft alleen toohappen eenmaal op elke server. Als u niet toosynchronize alle clouds wilt, kunt u laat u deze instelling uitgeschakeld en synchroniseert u elke cloud afzonderlijk in de eigenschappen van de cloud Hallo in Hallo VMM-console.

    ![Serverregistratie](./media/site-recovery-vmm-san/friendly-name.png)

15. Klik op **volgende** toocomplete Hallo proces. Na registratie worden metagegevens van Hallo VMM-server opgehaald door Azure Site Recovery. Hallo-server wordt weergegeven in **Servers** > **VMM-Servers** in Hallo kluis.

### <a name="command-line-installation"></a>Installatie vanaf de opdrachtregel

Hello Azure Site Recovery Provider kan ook worden geïnstalleerd met behulp van Hallo opdrachtregel te volgen. Deze methode kan gebruikte tooinstall Hallo-provider op Server Core voor Windows Server 2012 R2 zijn.

1. Hallo-Provider en de registratiesleutel sleutel tooa installatiemap downloaden. Bijvoorbeeld: C:\ASR.
2. Hallo VMM-service niet stoppen.
3. Pak het Provider-installatieprogramma Hallo. Deze opdrachten uitvoeren als beheerder:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Hallo Provider installeren:

        C:\ASR> setupdr.exe /i
5. Hallo Provider registreren:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>         

Parameters:

* **/ Credentials**: vereiste parameter voor de locatie van Hallo welke Hallo registratiesleutelbestand zich bevindt.  
* **/ FriendlyName**: vereiste parameter voor de naam van de Hallo van Hallo Hyper-V-hostserver die wordt weergegeven in hello Azure Site Recovery-portal.
* **/ EncryptionEnabled**: een optionele parameter alleen gebruikt wanneer van VMM tooAzure te repliceren.
* **/ proxyaddress**: een optionele parameter waarmee het adres van de proxyserver Hallo Hallo.
* **/ proxyport**: optionele parameter waarmee het Hallo-poort van de proxyserver Hallo.
* **proxyusername**: optionele parameter waarmee de proxygebruikersnaam hello (indien Hallo proxy verificatie is vereist).
* **/ proxypassword**: optionele parameter waarmee het Hallo-wachtwoord voor verificatie met de proxyserver hello (indien Hallo proxy verificatie is vereist).

## <a name="step-3-map-storage-arrays-and-pools"></a>Stap 3: Opslagmatrices en groepen toewijzen

Primaire en secundaire matrices toospecify welke secundaire opslaggroep replicatiegegevens van de primaire groep Hallo ontvangt worden toegewezen. Opslag toewijzen voordat u replicatie configureert omdat Hallo toewijzingsinformatie wordt gebruikt wanneer u de beveiliging voor replicatiegroepen inschakelen.

Voordat u begint, controleert u of VMM-clouds worden weergegeven in de kluis Hallo. Clouds worden gedetecteerd bij het synchroniseren van alle clouds tijdens de installatie van de Provider of wanneer u een specifieke cloud in VMM-console Hallo synchroniseert.

1. Klik op **Resources** > **serveropslag** > **kaart bron- en Doelmatrices**.
    ![Serverregistratie](./media/site-recovery-vmm-san/storage-map.png)

2. Hallo opslagmatrices op de primaire site Hallo selecteren en deze matrices toostorage op de secundaire site Hallo toewijzen. In **opslaggroepen**, selecteert u een bron en doel storage pool toomap.

    ![Serverregistratie](./media/site-recovery-vmm-san/storage-map-pool.png)

## <a name="step-4-configure-replication-settings"></a>Stap 4: Replicatie-instellingen configureren

Nadat de VMM-servers zijn geregistreerd, kunt u cloudbeveiligingsinstellingen configureren.

1. Op Hallo **Quick Start** pagina, klikt u op **beveiliging instellen voor VMM-clouds**.
2. Op Hallo **beveiligde Items** tabblad, selecteer Hallo cloud **configuratie**.
3. In **doel**, selecteer **VMM**.
4. In **doellocatie**, selecteer Hallo VMM-server die wordt beheerd Hallo cloud gewenste toouse voor herstel.
5. In **doel cloud**, selecteer Hallo doelcloud gewenste toouse voor VM-failover.
   * Het is raadzaam dat u selecteert een doelcloud op die voldoet aan de herstelvereisten voor Hallo virtuele machines die u beveiligt.
   * Een cloud kan alleen tooa één cloudpaar--als een primaire of een doelcloud behoren.
6. Site Recovery controleert of dat wolken hebben toegang tot tooSAN opslag en de opslag van die Hallo matrices worden toegewezen.
7. Als controle is geslaagd, in **replicatietype**, selecteer **SAN**.

Nadat u Hallo instellingen opslaat, wordt er een taak gemaakt die kan worden gecontroleerd op Hallo **taken** tabblad. Instellingen kunnen worden gewijzigd op Hallo **configureren** tabblad. Als u toomodify Hallo doellocatie of doelcloud wilt, moet u Hallo cloudconfiguratie verwijderen en vervolgens opnieuw configureren Hallo cloud.

## <a name="step-5-enable-network-mapping"></a>Stap 5: Netwerktoewijzing inschakelen

1. Op Hallo **Quick Start** pagina, klikt u op **netwerken toewijzen**.
2. Hallo bron-VMM-server selecteren en selecteer vervolgens Hallo doel VMM server toowhich Hallo netwerken worden toegewezen. Hallo-lijst van de bron en hun bijbehorende doelnetwerken weergegeven. Een lege waarde weergegeven voor de netwerken die niet zijn toegewezen. Klik op Hallo informatie pictogram volgende toohello bron en doel namen tooview Hallo netwerksubnetten voor elk netwerk.
3. Selecteer een netwerk in **netwerk op de bron**, en klik vervolgens op **kaart**. Hallo-service detecteert Hallo VM-netwerken op de doelserver Hallo en geeft deze weer.

    ![SAN-architectuur](./media/site-recovery-vmm-san/network-map1.png)
4. Selecteer een van de VM-netwerken Hallo in Hallo doel-VMM-server.

    ![SAN-architectuur](./media/site-recovery-vmm-san/network-map2.png)

5. Wanneer u een doelnetwerk selecteert, worden hello beveiligde clouds die Hallo Bronnetwerk weergegeven. Netwerken met beschikbare doelservers worden ook weergegeven. Het is raadzaam dat u selecteert een doelnetwerk dat beschikbaar tooall Hallo clouds die u gebruikt voor replicatie.
6. Klik op Hallo vinkje toocomplete Hallo toewijzingsproces. Een taak gestart die uitgevoerd wordt bijgehouden. U kunt deze ook bekijken op Hallo **taken** tabblad.

## <a name="step-6-enable-replication-for-replication-groups"></a>Stap 6: Replicatie inschakelen voor replicatiegroepen

Voordat u beveiliging voor virtuele machines inschakelen kunt, moet u replicatie tooenable voor replicatie van opslaggroepen.

1. Op Hallo **eigenschappen** pagina van de primaire cloud Hallo in Hallo Site Recovery-portal, open Hallo **virtuele Machines** tabblad en klik op **replicatiegroep toevoegen**.
2. Selecteer een of meer VMM replicatiegroepen die zijn gekoppeld aan cloud hello, Controleer of de bron en doel matrices Hallo en replicatiefrequentie Hallo opgeven.

Site Recovery, VMM en Hallo SMI-S-providers inrichten Hallo doel site opslag-LUN's en storage-replicatie inschakelen. Hallo replicatiegroep al is gerepliceerd, Site Recovery hergebruikt de bestaande replicatierelatie Hallo als updates Hallo informatie.

## <a name="step-7-enable-protection-for-virtual-machines"></a>Stap 7: Beveiliging voor virtuele machines inschakelen


Wanneer een opslaggroep wordt gerepliceerd, schakel de beveiliging voor virtuele machines in de VMM-console Hallo met een van de volgende methoden Hallo:

* **Nieuwe virtuele machine**: wanneer u een virtuele machine maakt, u replicatie inschakelt en Hallo VM koppelen aan een replicatiegroep Hallo.
  Met deze optie gebruikt VMM intelligente plaatsing toooptimally plaats Hallo VM-opslag op Hallo LUN's van de replicatiegroep Hallo. Site Recovery Hallo maken van een schaduwkopie VM op de secundaire site Hallo ingedeeld en capaciteit toegewezen zodat replica-VM kunnen worden gestart na een failover.
* **Bestaande virtuele machine**: als een virtuele machine in VMM al is geïmplementeerd, kunt u replicatie inschakelt en uitvoeren van een opslaggroep migratie tooa replicatie. Na voltooiing, VMM en de Site Recovery detecteren Hallo van nieuwe virtuele machine en start u deze beheren in Site Recovery. Een schaduw VM wordt gemaakt op de secundaire site Hallo en capaciteit is toegewezen, zodat die Hallo replica virtuele machine kan worden gestart na een failover.

![Beveiliging inschakelen](./media/site-recovery-vmm-san/enable-protect.png)

Nadat de virtuele machines zijn ingeschakeld voor replicatie, worden ze in Hallo Site Recovery-console weergegeven. U kunt zien VM-eigenschappen, status volgen en bijhouden van failover-replicatiegroepen die meerdere virtuele machines bevatten. In SAN-replicatie moeten alle virtuele machines die zijn gekoppeld aan een replicatiegroep failover samen. Dit is omdat failover op Hallo opslaglaag eerst plaatsvindt. Het is belangrijk toogroup uw replicatie goed groepen en alleen gekoppelde virtuele machines tegelijk te plaatsen.

> [!NOTE]
> Nadat u replicatie voor een virtuele machine hebt ingeschakeld, niet de VHD's tooLUNs toevoegen tenzij ze zich in een replicatiegroep voor de Site Recovery bevinden. Virtuele harde schijven wordt alleen door Site Recovery worden gedetecteerd als ze zich in een replicatiegroep voor de Site Recovery bevinden.
>
>

U kunt de voortgang, met inbegrip van de initiële replicatie Hallo op Hallo volgen **taken** tabblad. Nadat de taak beveiliging voltooien hello wordt uitgevoerd, is Hallo virtuele machine gereed voor failover.

![Beveiligingstaak voor virtuele machines](./media/site-recovery-vmm-san/job-props.png)

## <a name="step-8-test-hello-deployment"></a>Stap 8: Hallo-implementatie testen

Test uw implementatie toomake ervoor dat virtuele machines mislukken dan verwacht. toodo hiervan kan een herstelplan maken en een testfailover uitvoeren.

1. Op Hallo **herstelplannen** tabblad **herstelplan maken**.
2. Geef een naam voor het herstelplan Hallo en selecteer de bron en doel-VMM-servers. Hallo-bronserver, moet virtuele machines die zijn ingeschakeld voor failover en herstel hebben. Selecteer **SAN** tooview alleen clouds die zijn geconfigureerd voor SAN-replicatie.

    ![Herstelplan maken](./media/site-recovery-vmm-san/r-plan.png)

3. In **virtuele Machines selecteren**, replicatiegroepen selecteren. Alle virtuele machines die zijn gekoppeld aan de groep Hallo toohello herstelplan toegevoegd. Deze virtuele machines worden toegevoegd toohello herstel standaardgroep (groep 1). U kunt meer groepen toevoegen, indien nodig. Na de replicatie, worden virtuele machines genummerd volgens toohello volgorde van Hallo recovery planningsgroepen.

    ![Selecteer de virtuele machines](./media/site-recovery-vmm-san/r-plan-vm.png)
4. Nadat het herstelplan Hallo is gemaakt, wordt weergegeven in de lijst Hallo op Hallo **herstelplannen** tabblad. Hallo-abonnement selecteren en kies **Testfailover**.
5. Op Hallo **Testfailover bevestigen** pagina **geen**. Met deze optie is ingeschakeld, niet Hallo failover replica VMs tooany verbonden netwerk. Hiermee test u die Hallo VMs failover zoals verwacht, maar het Hallo-netwerkomgeving niet testen. Zie voor meer informatie over andere netwerkopties [siteherstel failover](site-recovery-failover.md).

    ![Selecteer testnetwerk](./media/site-recovery-vmm-san/test-fail1.png)

6. Hallo test-VM wordt gemaakt op Hallo dezelfde host als Hallo-host op welke replica Hallo VM zich bevindt. Deze is niet toohello cloud welke Hallo replica-VM zich bevindt toegevoegd.
2. Hallo replica-VM heeft na de replicatie, een ander IP-adres dan Hallo primaire virtuele machine. Als u adressen van DHCP uitgeeft, wordt deze automatisch worden bijgewerkt. Als u geen DHCP en u hello wilt wordt dezelfde adressen, moet u een aantal scripts toorun.
3. Voer dit script tooretrieve Hallo IP-adres:

       $vm = Get-SCVirtualMachine -Name <VM_NAME>
       $na = $vm[0].VirtualNetworkAdapters>
       $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
       $ip.address  

4. In dit voorbeeld script tooupdate DNS worden uitgevoerd. Geef Hallo IP-adres dat u hebt opgehaald.

       [string]$Zone,
       [string]$name,
       [string]$IP
       )
       $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
       $newrecord = $record.clone()
       $newrecord.RecordData[0].IPv4Address  =  $IP
       Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord


## <a name="next-steps"></a>Volgende stappen

Nadat u hebt een test failover toocheck dat uw omgeving werkt zoals verwacht uitgevoerd, Zie [siteherstel failover](site-recovery-failover.md) toolearn over verschillende soorten failovers.
