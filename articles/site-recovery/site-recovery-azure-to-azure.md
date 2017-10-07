---
title: 'Virtuele Azure-machines repliceren tussen Azure-regio''s voor herstel na noodgevallen moet: Azure tooAzure | Microsoft Docs'
description: Geeft een overzicht van Hallo stappen u moet tooreplicate Azure VM's tussen Azure-regio's (Azure Azure) met hello Azure Site Recovery-service voor herstel nodig zijn na noodgevallen.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a>Virtuele Azure-machines repliceren tussen regio's met Azure Site Recovery

>[!NOTE]
>
> Azure Site Recovery-replicatie voor virtuele Azure-machines (VM's) is momenteel in preview.

Dit artikel wordt beschreven hoe tooreplicate Azure VM's tussen Azure-regio's met behulp van Hallo [siteherstel](site-recovery-overview.md) service in hello Azure-portal.

Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="disaster-recovery-in-azure"></a>Herstel na noodgevallen in Azure

Ingebouwde Azure-infrastructuur functies en mogelijkheden die bijdragen tooa robuuste en robuuste beschikbaarheidsstrategie voor werkbelastingen die worden uitgevoerd op Azure Virtual machines. Er zijn echter diverse redenen waarom u nodig tooplan voor herstel na noodgevallen tussen Azure-regio's zelf hebt:

- U moet toomeet naleving richtlijnen voor specifieke toepassingen en werkbelastingen waarvoor een zakelijke continuïteit en noodherstelplan (BCDR).
- U wilt Hallo mogelijkheid tooprotect en het herstellen van Azure VM's op basis van uw zakelijke beslissingen te nemen en niet alleen op basis van ingebouwde functionaliteit voor Azure.
- U moet tootest failovers en herstel in overeenstemming met uw behoeften bedrijven en naleving zonder impact op de productie.
- U moet toofail via toohello herstel regio in geval van een noodgeval Hallo en de oorspronkelijke bron regio back toohello naadloos mislukken.

Site Recovery gebruiken voor de virtuele machine van Azure naar Azure replicatie toohelp bent u al deze taken.


## <a name="why-use-site-recovery"></a>Waarom u Site Recovery moet gebruiken      

Site Recovery biedt een eenvoudige manier tooreplicate Azure VM's tussen regio's:

- **Automatische implementatie**. In tegenstelling tot een actief / actief-replicatiemodel hoeft niet voor een dure en complexe infrastructuur in Hallo secundaire regio. Wanneer u replicatie inschakelt, maakt Site Recovery automatisch Hallo vereist resources in Hallo doelregio, op basis van regio broninstellingen.
- **Regio's beheren**. Met Site Recovery kunt u vanaf een willekeurige regio tooany regio binnen een continent repliceren. Vergelijk deze met leestoegang geografisch redundante opslag, dat asynchroon tussen Standaard repliceert [regio's gekoppeld](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) alleen. Geografisch redundante opslag met leestoegang biedt alleen-lezentoegang toohello gegevens in Hallo doelregio.
- **Automatische replicatie**. Site Recovery biedt geautomatiseerde continue replicatie. Failover en failback kunnen worden geactiveerd met een enkele klik.
- **RTO en RPO**. Site Recovery wordt gebruikgemaakt van hello Azure netwerkinfrastructuur die verbinding regio's tookeep maakt RTO en zeer lage RPO.
- **Testen van**. U kunt herstel na noodgevallen zoomt uitvoeren met op aanvraag testfailovers, wanneer nodig, zonder de productie-workloads of lopende replicatie te beïnvloeden.
- **De herstelplannen**. U kunt herstel plannen tooorchestrate failover en failback van de gehele toepassing hello uitgevoerd op meerdere virtuele machines. Hallo-functie voor herstel plan heeft uitgebreide klas integratie met Azure automation-runbooks.


## <a name="deployment-summary"></a>Implementatieoverzicht

Hier volgt een samenvatting van wat u moet toodo tooset van de replicatie van virtuele machines tussen Azure-regio's:

1. Maak een Recovery Services-kluis. Hallo-kluis bevat configuratie-instellingen en stuurt replicatie.
2. Replicatie inschakelen voor hello Azure VM's.
3. Een test failover-toomake of alles werkt zoals verwacht worden uitgevoerd.

>[!IMPORTANT]
>
> U kunt controleren Hallo [ondersteuningsmatrix voor replicatie van de virtuele machine van Azure](./site-recovery-support-matrix-azure-to-azure.md).

>[!IMPORTANT]
>
> Zie voor informatie over hoe tooconfigure Hallo uitgaande netwerkverbinding voor Azure Virtual Machines voor replicatie van Site Recovery vereist Hallo [leidraad voor netwerken](./site-recovery-azure-to-azure-networking-guidance.md).

### <a name="before-you-start"></a>Voordat u begint

* Uw Azure gebruikersaccount moet toohave bepaalde [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replicatie van een virtuele machine van Azure.
* Uw Azure-abonnement moet zijn ingeschakeld toocreate virtuele machines in Hallo target-locatie die u toouse als Hallo disaster recovery regio wilt. Neem contact op met ondersteuning tooenable Hallo vereist quota.

## <a name="create-a-recovery-services-vault"></a>Een Recovery Services-kluis maken

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> U wordt aangeraden dat u Hallo Recovery Services-kluis maken in Hallo-locatie waar u uw virtuele machines tooreplicate. Bijvoorbeeld, als uw target-locatie wordt centraal ons hello, Hallo kluis in maken **VS-midden**.

## <a name="enable-replication"></a>Replicatie inschakelen

In **Recovery Services-kluizen**, klikt u op de kluisnaam Hallo. Klik in het Hallo-kluis op Hallo **+ repliceren** knop.

### <a name="step-1-configure-hello-source"></a>Step 1. Hallo bron configureren
1. In **bron**, selecteer **Azure - PREVIEW**.
2. In **bronlocatie**, selecteer Hallo bron Azure-regio waarin uw virtuele machines worden uitgevoerd.
3. Selecteer Hallo implementatiemodel van uw virtuele machines: **Resource Manager** of **klassieke**.
4. Selecteer Hallo **resourcegroep** voor Resource Manager virtuele machines of **cloudservice** voor klassieke virtuele machines.

    ![Hallo bron configureren](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a>Stap 2. Selecteer de virtuele machines

* Selecteer Hallo VMs u tooreplicate wilt en klik vervolgens op **OK**.

    ![Selecteer de virtuele machines](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a>Stap 3. Instellingen configureren

1. toooverride hello standaard instellingen als doel en geef instellingen op Hallo van uw keuze, klikt u op **aanpassen**. Zie voor meer informatie [doelresources aanpassen](site-recovery-replicate-azure-to-azure.md##customize-target-resources).

    ![Instellingen configureren](./media/site-recovery-azure-to-azure/settings.png)


2. Standaard maakt Site Recovery een replicatiebeleid die ervoor zorgt dat toepassingsconsistente momentopnamen elke 4 uur handhaaft herstelpunten gedurende 24 uur. toocreate beleid met verschillende instellingen, klikt u op **aanpassen** volgende te**replicatiebeleid**.

    ![Beleid aanpassen](./media/site-recovery-azure-to-azure/customize-policy.png)

3. toostart inrichting Hallo doelresources, klikt u op **doelresources maken**. Inrichting duurt een minuut. Sluit de blade Hallo niet tijdens het inrichten of u toostart dan nodig.

4. replicatie tootrigger Hallo VM geselecteerd, klikt u op **replicatie inschakelen**.

5. U kunt de voortgang van Hallo volgen **beveiliging inschakelen** taak **instellingen** > **taken** > **Site Recovery-taken**.

6. In **instellingen** > **gerepliceerde Items**, kunt u weergeven Hallo status van virtuele machines en Hallo initiële replicatie uitgevoerd. Klik op Hallo VM toodrill omlaag in de instellingen ervan.

## <a name="run-a-test-failover"></a>Een testfailover uitvoeren

Nadat u alles instellen, voert u een test failover toomake, controleren of dat alles werkt zoals verwacht:

1. toofail via één computer in **instellingen** > **gerepliceerde Items**, klikt u op Hallo VM **+ Testfailover** pictogram.

2. plan toofail via een herstelbewerking **instellingen** > **herstelplannen**, klik met de rechtermuisknop Hallo plan **Testfailover**. een herstelplan toocreate [Volg deze instructies](site-recovery-create-recovery-plans.md). 

3. In **Testfailover**, selecteer Hallo doel virtuele Azure-netwerk toowhich virtuele Azure-machines worden verbonden nadat er een Hallo failover plaatsvindt.

4. toostart Hallo failover, klikt u op **OK**. tootrack voortgang, klikt u op Hallo VM tooopen eigenschappen ervan. U kunt ook op Hallo **Testfailover** taak in de kluisnaam Hallo > **instellingen** > **taken** > **Site Recovery-taken**.

5. Na het Hallo failover is voltooid, Hallo replica machine van Azure in hello Azure-portal weergegeven > **virtuele Machines**. Zorg ervoor dat Hallo VM is de juiste grootte hello, of deze is verbonden met het juiste netwerk toohello en dat deze wordt uitgevoerd.

6. toodelete hello virtuele machines die zijn gemaakt tijdens de testfailover hello, klikt u op **testfailover opschonen** op Hallo gerepliceerd item of Hallo herstelplan. In **notities**, vastleggen en opslaan van eventuele opmerkingen die zijn gekoppeld aan de testfailover Hallo. 

[Meer informatie](site-recovery-test-failover-to-azure.md) over testfailovers.


## <a name="next-steps"></a>Volgende stappen

Na het Hallo-implementatie te testen:

- [Meer informatie](site-recovery-failover.md) over verschillende soorten failovers en hoe toorun ze.
- Meer informatie over [met herstelplannen](site-recovery-create-recovery-plans.md) tooreduce RTO.
