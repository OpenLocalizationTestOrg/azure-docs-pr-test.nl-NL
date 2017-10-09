---
title: aaaSet up Hallo bron en doel voor Hyper-V-replicatie tooAzure (zonder de System Center VMM) met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen tooset bron en doel-instellingen opgeven voor de replicatie van Hyper-V-machines tooAzure opslag met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d2010d85-77fd-4dea-84f3-1c960ed4c63f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 105b90e6ac053d5b842c54a36c460a26d0f5c2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-replication-tooazure"></a>Stap 8: Instellen Hallo bron en doel voor Hyper-V-replicatie tooAzure

Dit artikel wordt beschreven hoe tooconfigure bron en doel-instellingen bij het repliceren van on-premises Hyper-V virtuele machines (zonder de System Center VMM) tooAzure, met Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.

Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Hallo bronomgeving instellen

Hallo Hyper-V-site instellen, installeert hello Azure Site Recovery Provider en hello Azure Recovery Services agent op Hyper-V-hosts en Hallo site in Hallo kluis registreren.

1. In **infrastructuur voorbereiden**, klikt u op **bron**. tooadd een nieuwe Hyper-V-site als een container voor uw Hyper-V-hosts of clusters, klikt u op **+ Hyper-V-Site**.

    ![Bron instellen](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. In **maken van Hyper-V-site**, Geef een naam voor het Hallo-site. Klik vervolgens op **OK**. Selecteer Hallo site hebt gemaakt Klik op nu **+ Hyper-V Server** tooadd een toohello serversite.

    ![Bron instellen](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. In **Server toevoegen** > **servertype**, controleert u of **Hyper-V-server** wordt weergegeven.

    - Zorg ervoor dat Hallo Hyper-V-server die u wilt tooadd voldoet aan de Hallo [vereisten](#on-premises-prerequisites), en kunnen tooaccess Hallo is opgegeven URL's.
    - Download hello Azure Site Recovery Provider-installatiebestand. U voert dit bestand tooinstall Hallo Provider en Hallo Recovery Services-agent op elke Hyper-V-host.

    ![Bron instellen](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-hello-provider-and-agent"></a>Hallo Provider en agent installeren

1. Hallo Provider-installatiebestand op elke host uitvoeren u toohello Hyper-V-site toegevoegd. Als u op een Hyper-V-cluster installeert, moet u setup uitvoeren op elk clusterknooppunt. Installeren en registreren van elk clusterknooppunt Hyper-V zorgt ervoor dat virtuele machines worden beschermd, zelfs als ze via knooppunten migreren.
2. In **Microsoft Update** kunt u updates inschakelen, zodat de providerupdates volgens uw Microsoft Update-beleid worden geïnstalleerd.
3. In **installatie**, accepteer of wijzig Hallo Provider standaardlocatie voor installatie en klik op **installeren**.
4. In **Kluisinstellingen**, klikt u op **Bladeren** tooselect hello kluissleutelbestand die u hebt gedownload. Geef hello Azure Site Recovery-abonnement, Hallo kluisnaam, en Hallo Hyper-V-site toowhich Hallo Hyper-V server behoort.

    ![Serverregistratie](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. In **Proxy-instellingen**, hoe Hallo Provider waarop Hyper-V-hosts tooAzure Site Recovery verbindt via internet Hallo opgeven.

    * Als u wilt dat Hallo Provider tooconnect rechtstreeks Selecteer **tooAzure siteherstel zonder een proxy rechtstreeks verbinding gemaakt**.
    * Als uw bestaande proxy verificatie vereist, of u een aangepaste proxy toouse voor Hallo providerverbinding wilt, schakelt u **verbinding maken met Site Recovery via een proxyserver tooAzure**.
    * Als u een proxy gebruikt:
        - Hallo-adres, poort en referenties opgeven
        - Zorg ervoor dat Hallo URL's die worden beschreven in Hallo [vereisten](#prerequisites) via proxy Hallo zijn toegestaan.

    ![internet](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. Nadat de installatie is voltooid, klikt u op **registreren** tooregister Hallo-server in Hallo kluis.

    ![Installatielocatie](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. Nadat de registratie is voltooid, metagegevens van Hallo Hyper-V server worden opgehaald door Azure Site Recovery en Hallo-server wordt weergegeven in **Site Recovery-infrastructuur** > **Hyper-V-Hosts**.


## <a name="set-up-hello-target-environment"></a>Hallo doelomgeving instellen

Geef hello Azure storage-account voor replicatie en hello Azure-netwerk toowhich virtuele Azure-machines na failover verbinding maakt.

1. Klik op **infrastructuur voorbereiden** > **doel**.
2. Hallo-abonnement en resourcegroep Hallo waarin u toocreate Hallo virtuele Azure-machines na een failover wilt selecteren. Kies Hallo implementatie model wilt u toouse in Azure (klassiek of de resource management) voor Hallo virtuele machines.

3. Site Recovery controleert of u een of meer compatibele Azure-opslagaccounts en -netwerken hebt.

    - Als u geen storage-account hebt, klikt u op **en opslag** toocreate een inline-account op basis van een Resource Manager. 
    - Als u geen Azure-netwerk hebt, klikt u op **+ netwerk** toocreate een inline Resource Manager-netwerk.






## <a name="next-steps"></a>Volgende stappen

Ga te[stap 9: een replicatiebeleid instellen](hyper-v-site-walkthrough-replication.md)
