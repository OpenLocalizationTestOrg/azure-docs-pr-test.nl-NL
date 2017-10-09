---
title: aaaSet up Hallo bron en doel voor tooAzure in een Hyper-V-replicatie (met System Center VMM) met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen tooset bron en doel-instellingen opgeven voor de replicatie van Hyper-V-machines in VMM-clouds tooAzure opslag met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5edb6d87-25a5-40fe-b6f1-ddf7b55a6b31
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/25/2017
ms.author: raynew
ms.openlocfilehash: 3f8c5386cb64527c775aef636980bac098ee9905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-with-vmm-replication-tooazure"></a>Stap 8: Instellen Hallo bron en doel voor Hyper-V (met VMM) replicatie tooAzure

Na [maken van een kluis](vmm-to-azure-walkthrough-create-vault.md) en opgeven wat u wilt tooreplicate, gebruikt u dit artikel tooconfigure bron en doel instellingen bij het repliceren van on-premises Hyper-V virtuele machines in System Center Virtual Machine Manager (VMM) Clouds tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.

Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Hallo bronomgeving instellen

S1. Klik op **Infrastructuur voorbereiden** > **Bron**.

    ![Set up source](./media/vmm-to-azure-walkthrough-source-target/set-source1.png)

2. In **bron voorbereiden**, klikt u op **+ VMM** tooadd een VMM-server.

    ![Bron instellen](./media/vmm-to-azure-walkthrough-source-target/set-source2.png)

3. In **Server toevoegen**, controleert u of **System Center VMM-server** wordt weergegeven in **servertype** en die Hallo VMM-server voldoet aan Hallo [vereisten en -URL vereisten voor](#prerequisites).
4. Download hello Azure Site Recovery Provider-installatiebestand.
5. Download de registratiesleutel Hallo. U hebt deze nodig wanneer u de installatie uitvoert. Hallo-sleutel is vijf dagen na het genereren ervan geldig.

    ![Bron instellen](./media/vmm-to-azure-walkthrough-source-target/set-source3.png)

## <a name="install-hello-provider-on-hello-vmm-server"></a>Hallo Provider installeren op Hallo VMM-server

1. Hallo Provider-installatiebestand op Hallo VMM-server wordt uitgevoerd.
2. In **Microsoft Update** kunt u updates inschakelen, zodat de providerupdates volgens uw Microsoft Update-beleid worden geïnstalleerd.
3. In **installatie**, accepteer of wijzig Hallo Provider standaardlocatie voor installatie en klik op **installeren**.

    ![Installatielocatie](./media/vmm-to-azure-walkthrough-source-target/provider2.png)
4. Wanneer de installatie is voltooid, klikt u op **registreren** tooregister Hallo VMM-server in Hallo kluis.
5. In Hallo **Kluisinstellingen** pagina, klikt u op **Bladeren** kluissleutelbestand hello tooselect. Hello Azure Site Recovery-abonnement en de kluisnaam Hallo opgeven.

    ![Serverregistratie](./media/vmm-to-azure-walkthrough-source-target/provider10.png)
6. In **internetverbinding**, hoe Hallo Provider die wordt uitgevoerd op Hallo VMM-server de tooSite herstel verbinding maken via internet Hallo opgeven.

   * Als u rechtstreeks Hallo Provider tooconnect wilt, schakelt **tooAzure siteherstel zonder een proxy rechtstreeks verbinding gemaakt**.
   * Als uw bestaande proxy verificatie vereist, of u een aangepaste proxy toouse wilt, schakelt u **verbinding maken met Site Recovery via een proxyserver tooAzure**.
   * Als u een aangepaste proxy gebruikt, geef Hallo-adres, poort en referenties.
   * Als u een proxy gebruikt, u moet hebben al toegestaan Hallo URL's die worden beschreven [vereisten](#on-premises-prerequisites).
   * Als u een aangepaste proxy gebruikt, een VMM RunAs-account (DRAProxyAccount) wordt automatisch gemaakt met Hallo opgegeven proxyreferenties. Hallo-proxyserver zodanig configureren dat dit account kan worden geverifieerd. Hallo VMM RunAs-Accountinstellingen kunnen worden gewijzigd in Hallo VMM-console. In **instellingen**, vouw **beveiliging** > **Run As-Accounts**, en wijzig vervolgens Hallo wachtwoord voor DRAProxyAccount. U moet toorestart Hallo VMM-service zodat deze instelling wordt van kracht.

     ![internet](./media/vmm-to-azure-walkthrough-source-target/provider13.png)
7. Accepteer of wijzig de locatie Hallo van een SSL-certificaat dat automatisch gegenereerd voor gegevensversleuteling. Dit certificaat wordt gebruikt als u gegevensversleuteling voor een cloud die wordt beveiligd door Azure in hello Azure Site Recovery-portal inschakelt. Bewaar dit certificaat op een veilige plaats. Wanneer u een failover-tooAzure uitvoert moet u deze toodecrypt, als gegevensversleuteling is ingeschakeld.
8. In **servernaam**, Geef een beschrijvende naam tooidentify Hallo VMM-server in Hallo kluis. Geef in een clusterconfiguratie Hallo VMM-clusterrolnaam op.
9. Schakel **cloudmetagegevens synchroniseren**, als u wilt dat toosynchronize metagegevens voor alle clouds op Hallo VMM-server op Hallo kluis. Deze actie hoeft alleen toohappen eenmaal op elke server. Als u niet toosynchronize alle clouds wilt, kunt u laat u deze instelling uitgeschakeld en synchroniseert u elke cloud afzonderlijk in de eigenschappen van de cloud Hallo in Hallo VMM-console. Klik op **registreren** toocomplete Hallo proces.

    ![Serverregistratie](./media/vmm-to-azure-walkthrough-source-target/provider16.png)
10. De registratie begint. Nadat de registratie is voltooid, Hallo-server wordt weergegeven in **Site Recovery-infrastructuur** > **VMM-Servers**.


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a>Hello Azure Recovery Services-agent installeren op Hyper-V-hosts

1. Nadat u Hallo Provider hebt ingesteld, moet u toodownload Hallo-installatiebestand voor hello Azure Recovery Services agent. Voer setup uit op elke Hyper-V-server in Hallo VMM-cloud.

    ![Hyper-V-sites](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent1.png)
2. Klik in **Controle van vereisten** op **Volgende**. Ontbrekende vereiste onderdelen worden automatisch geïnstalleerd.

    ![Vereisten voor de Recovery Services-agent](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent2.png)
3. In **installatie-instellingen**Accepteer of wijzig de installatielocatie Hallo en Hallo cachelocatie. U kunt Hallo-cache configureren op een station met ten minste 5 GB aan opslagruimte maar we raden een cachestation met 600 GB of meer aan vrije ruimte. Klik vervolgens op **Installeren**.
4. Nadat de installatie is voltooid, klikt u op **sluiten** toofinish.

    ![MARS-agent registreren](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent3.png)

### <a name="command-line-installation"></a>Installatie vanaf de opdrachtregel
U kunt Hallo Microsoft Azure Recovery Services Agent installeren vanaf de opdrachtregel met behulp van de volgende opdracht Hallo:

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a>Internet proxy toegang tooSite herstel van Hyper-V-hosts instellen

Hallo Recovery Services agent waarop Hyper-V-hosts moet internet toegang tooAzure voor VM-replicatie. Als u toegang hebt tot Hallo internet via een proxy instellen als volgt:

1. Open Hallo Microsoft Azure Backup MMC-module op Hallo Hyper-V-host. Een snelkoppeling naar Microsoft Azure Backup is standaard beschikbaar zijn op Hallo bureaublad of in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Klik in het Hallo-module op **eigenschappen wijzigen**.
3. Op Hallo **proxyconfiguratie** tabblad, proxyservergegevens opgeven.

    ![MARS-agent registreren](./media/vmm-to-azure-walkthrough-source-target/mars-proxy.png)
4. Controleer die agent Hallo Hallo URL's die worden beschreven in Hallo kan bereiken [vereisten](#on-premises-prerequisites).

## <a name="set-up-hello-target-environment"></a>Hallo doelomgeving instellen
Geef hello Azure storage-account toobe gebruikt voor replicatie en hello Azure-netwerk toowhich virtuele Azure-machines na failover verbinding maakt.

1. Klik op **infrastructuur voorbereiden** > **doel**en selecteer Hallo abonnement Hallo resourcegroep waar u toocreate Hallo failover van virtuele machines. Hallo-implementatiemodel dat u toouse in Azure (klassiek of de resource management) voor Hallo failover van virtuele machines wilt kiezen.

    ![Storage](./media/vmm-to-azure-walkthrough-source-target/enablerep3.png)

2. Site Recovery controleert of u een of meer compatibele Azure-opslagaccounts en -netwerken hebt.

    ![Storage](./media/vmm-to-azure-walkthrough-source-target/compatible-storage.png)

3. Als u een opslagaccount dat nog niet hebt gemaakt, en toocreate een gewenste met Resource Manager, klikt u op **+ opslagaccount** toodo dat inline.  Op Hallo **storage-account maken** blade een naam, type, abonnement en locatie opgeven. Hallo-account moet zich op Hallo dezelfde locatie als Hallo Recovery Services-kluis.

   ![Storage](./media/vmm-to-azure-walkthrough-source-target/gs-createstorage.png)


   * Als u een opslagaccount met behulp van het klassieke model Hallo toocreate wilt, doet u dat in hello Azure-portal. [Meer informatie](../storage/common/storage-create-storage-account.md)
   * Als u een premium storage-account voor gerepliceerde gegevens, instellen van een extra standard-opslagaccount, toostore replicatielogboeken die de doorlopende wijzigingen tooon-premises gegevens vastleggen.
5. Als u een Azure-netwerk dat nog niet hebt gemaakt, en toocreate een gewenste met Resource Manager, klikt u op **+ netwerk** toodo dat inline. Op Hallo **virtueel netwerk maken** blade een netwerknaam, adresbereik subnetgegevens, abonnement en locatie opgeven. Hallo-netwerk moet zich in Hallo dezelfde locatie als Hallo Recovery Services-kluis.

   ![Netwerk](./media/vmm-to-azure-walkthrough-source-target/gs-createnetwork.png)

   Als u een netwerk met het klassieke model Hallo toocreate wilt, doet u dat in hello Azure-portal. [Meer informatie](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).





## <a name="next-steps"></a>Volgende stappen

Ga te[stap 9: netwerktoewijzing configureren](vmm-to-azure-walkthrough-network-mapping.md)
