---
title: aaaReprotect van Azure tooan lokale site | Microsoft Docs
description: Na een failover van virtuele machines tooAzure kunt u een failback toobring tooon-premises back met virtuele machines starten. Meer informatie over hoe tooreprotect voordat een failback.
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: 94c86e79cba4cd3f0c5821fdd5509cca1d0e7820
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reprotect-from-azure-tooan-on-premises-site"></a>Beveiligt van Azure tooan lokale site



## <a name="overview"></a>Overzicht
Dit artikel wordt beschreven hoe tooreprotect Azure virtuele machines van Azure tooan lokale site. Volg de instructies in Hallo in dit artikel als u klaar toofail bent uw virtuele VMware-machines of fysieke Windows of Linux-servers back-nadat ze hebt failover van Hallo lokale site tooAzure (zoals beschreven in [virtuele VMware repliceren machines en fysieke servers tooAzure met Azure Site Recovery](site-recovery-failover.md)).

> [!WARNING]
> U nadat u hebt niet afkeuren [migratie voltooien](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), een resourcegroep van de virtuele machine tooanother verplaatsen of verwijderen van een virtuele machine van Azure.


Nadat de beveiligingspoging is voltooid en hello beveiligde virtuele machines worden gerepliceerd, kunt u een failback op Hallo virtuele machines toobring initiëren ze toohello on-premises-site.

Opmerkingen of vragen plaatsen aan Hallo einde van dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Bekijk voor een snel overzicht Hallo video over hoe toofail via uit Azure tooan lokale site te volgen.
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]


## <a name="prerequisites"></a>Vereisten
Wanneer u tooreprotect virtuele machines voorbereidt, nemen of rekening houden met de volgende vereiste activiteiten Hallo:

* Als een vCenter-server beheert Hallo virtuele machines die u wilt dat toofail terug naar, zorg ervoor dat u Hallo hebt [machtigingen vereist](site-recovery-vmware-to-azure-classic.md) voor de detectie van virtuele machines op de vCenter-servers.

  > [!WARNING]
  > Zo momentopnamen aanwezig op Hallo zijn on-premises master doel of Hallo virtuele machine, beveiligingspoging mislukt. Voordat u tooreprotect verdergaat, kunt u momentopnamen op het hoofddoel Hallo Hallo verwijderen. Hallo momentopnamen op Hallo virtuele machine worden automatisch samengevoegd tijdens een taak opnieuw beveiligen.

* Voordat u een failback uit op, maakt u twee extra onderdelen:

  * **Processerver**: Hallo [processerver](site-recovery-vmware-setup-azure-ps-resource-manager.md) ontvangt gegevens van Hallo beveiligde virtuele machine in Azure en verzendt gegevens toohello on-premises-site. Een traag netwerk is vereist tussen de processerver Hallo en Hallo beveiligde virtuele machine. U kunt dus een on-premises processerver hebben als u een Azure ExpressRoute-verbinding of een op basis van een Azure-processerver en een VPN.
  
  * **Hoofddoelserver**: Hallo hoofddoelserver ontvangt gegevens van failback. Hallo lokale management-server die u hebt gemaakt, heeft een hoofddoelserver standaard geïnstalleerd. Echter, afhankelijk van Hallo verkeersvolume is mislukt-back moet u mogelijk een afzonderlijke hoofddoelserver toocreate voor failback.
    * [Een virtuele Linux-machine moet een Linux-hoofddoelserver](site-recovery-how-to-install-linux-master-target.md).
    * Een virtuele Windows-computer moet een Windows-hoofddoelserver. U kunt Hallo lokale proces server en master doelmachines opnieuw gebruiken.

    Hallo hoofddoel heeft andere vereisten die worden vermeld in [algemene dingen toocheck op een hoofddoel voordat beveiligt](site-recovery-how-to-reprotect.md#common-things-to-check-after-completing-installation-of-the-master-target-server).

* Een configuratieserver is vereist on-premises wanneer u een failback uit. Tijdens de failback moet Hallo virtuele machine in de configuratiedatabase server Hallo bestaat. Anders wordt de failback is mislukt. 

> [!IMPORTANT]
> Zorg ervoor dat u rekening houden met regelmatig geplande back-ups van uw configuratieserver. Als er een ramp, terugzetten Hallo-server met dezelfde IP-adres zodat failback werkt Hallo.

* Set Hallo `disk.EnableUUID=true` instellen in de configuratieparameters Hallo van Hallo hoofddoel virtuele machine in VMware. Als deze rij niet bestaat, moet u deze toevoegen. Deze instelling is vereist tooprovide een consistente UUID toohello schijf voor virtuele machine (VMDK), zodat deze correct koppelt.

* *U kunt Storage vMotion niet gebruiken op de hoofddoelserver hello*. Hierdoor kan Hallo failback toofail. Hallo virtuele machine starten niet omdat het Hallo-schijven zijn niet beschikbaar tooit. tooprevent dit probleem op door uitsluiten Hallo hoofddoelservers uit de lijst met vMotion.

* Voeg een nieuw station toohello hoofddoelserver: een station bewaren. Voeg een nieuwe schijf en de indeling Hallo-station.


### <a name="frequently-asked-questions"></a>Veelgestelde vragen

#### <a name="why-do-i-need-a-s2s-vpn-or-an-expressroute-connection-tooreplicate-data-back-toohello-on-premises-site"></a>Waarom moet ik een S2S-VPN- of een ExpressRoute verbinding tooreplicate gegevens back toohello on-premises site?
Terwijl de replicatie van lokale tooAzure kan gebeuren via Hallo Internet of een ExpressRoute-verbinding met openbare peering, beveiligingspoging en failback moeten u een site-naar-site (S2S) VPN-tooreplicate gegevens. Geef Hallo netwerk zodat Hallo failover virtuele machines in Azure (ping) Hallo lokale configuratie-server kan bereiken. U kunt ook processerver in hello Azure-netwerk van Hallo failover virtuele machine implementeren. Dit processerver moet ook kunnen toocommunicate met Hallo lokale configuratie-server.

#### <a name="when-should-i-install-a-process-server-in-azure"></a>Wanneer moet ik een processerver in Azure installeren?


Hallo virtuele machines in Azure die u wilt dat tooreprotect verzenden replicatie gegevens tooa processerver. Instellen van uw netwerk zodat Hallo virtuele machines in Azure Hallo processerver kunnen bereiken.

U kunt een processerver in Azure implementeren of Hallo bestaande processerver die u hebt gebruikt tijdens de failover. Hallo belangrijk punt tooconsider zijn Hallo latentie toosend Hallo gegevens van Hallo virtuele machines op de processerver Azure toohello.

Als u een ExpressRoute-verbinding instellen hebt, kunt u een on-premises proces server toosend gegevens kunt gebruiken omdat Hallo latentie tussen Hallo virtuele machine en de processerver Hallo laag.

 ![Architectuurdiagram voor ExpressRoute](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)



Als u alleen een S2S-VPN hebt, is het echter raadzaam te implementeren Hallo processerver in Azure.

 ![Diagram voor VPN-architectuur](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)


Houd er rekening mee dat replicatie alleen via Hallo S2S VPN of persoonlijke peering van uw netwerk ExpressRoute Hallo gebeurt. Zorg ervoor dat er voldoende bandbreedte beschikbaar via dat netwerkkanaal is.

Zie voor meer informatie over het installeren van een op basis van een Azure-processerver [een processerver worden uitgevoerd in Azure beheren](site-recovery-vmware-setup-azure-ps-resource-manager.md).

> [!TIP]
> U wordt aangeraden met behulp van een op basis van een Azure-processerver tijdens failback. prestaties van replicaties Hallo is hoger als processerver Hallo dichter toohello repliceren van virtuele machine (Hallo failover-machine in Azure). Echter tijdens uw bewijs van het concept (POC)- of demonstratiedoeleinden, kunt u Hallo lokale processerver samen met ExpressRoute persoonlijke peering toocomplete Hello Implementatiemodel sneller.



#### <a name="what-ports-should-i-open-on-different-components-so-that-reprotection-can-work"></a>Welke poorten is het openen van op verschillende onderdelen zodat beveiligingspoging kan werken?

![Poorten voor failover en failback](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

#### <a name="which-master-target-server-should-i-use-for-reprotection"></a>Welke hoofddoelserver moet ik gebruiken voor beveiligingspoging?
Een on-premises hoofddoelserver-server zijn vereist tooreceive gegevens van de processerver Hallo en schrijf vervolgens toohello on-premises virtuele machine van VMDK. Als u Windows virtuele machines beveiligt, moet u een Windows-hoofddoelserver. U kunt hergebruiken Hallo lokale processerver en de hoofddoelserver<!-- !todo component -->. Voor virtuele Linux-machines moet u tooset van een Linux-hoofddoel extra on-premises.


Zie voor informatie over het installeren van een hoofddoelserver:

* [Hoe tooinstall Windows de hoofdsleutel van de doelserver](site-recovery-vmware-to-azure.md)
* [Hoe tooinstall Linux de hoofdsleutel van de doelserver](site-recovery-how-to-install-linux-master-target.md)


#### <a name="what-datastore-types-are-supported-on-hello-on-premises-esxi-host-during-failback"></a>Welke typen gegevensopslag op Hallo lokale ESXi host tijdens de failback worden ondersteund?

Azure Site Recovery ondersteunt mislukken back op dit moment alleen tooa virtuele machine file system (VMFS) of virtueel SAN gegevensarchief. Een NFS-gegevensopslag wordt niet ondersteund. Vanwege toothis beperking Voer Hallo datastore selectie op Hallo beveiligt scherm is leeg in geval van NFS datastores Hallo of het Hallo virtueel SAN datastore bevat maar tijdens het Hallo-taak is mislukt. Als u van plan toofail terug bent, kunt u lokale voor gegevensopslag VMFS maken en mislukken back tooit. Deze failback wordt een volledige download Hallo VMDK.

### <a name="common-things-toocheck-after-completing-installation-of-hello-master-target-server"></a>Algemene dingen toocheck na het voltooien van de installatie van de hoofddoelserver Hallo

* Als hello virtuele machine is aanwezig op lokale op Hallo vCenter-server, hello hoofddoelserver moet toegang tot toohello on-premises virtuele machine van VMDK. Toegang is de benodigde toowrite Hallo gerepliceerde gegevens toohello van schijven op virtuele machine. Zorg ervoor dat Hallo on-premises virtuele machine gegevensopslag op Hallo hoofddoel van host met lees-/ schrijftoegang is gekoppeld.

* Als Hallo virtuele machine niet aanwezig op lokale Hallo vCenter server is, moet Hallo Site Recovery-service toocreate een nieuwe virtuele machine tijdens beveiligingspoging. Deze virtuele machine wordt gemaakt op Hallo ESX-host waarop u het hoofddoel Hallo maakt. Kies Hallo ESX-host zorgvuldig, zodat Hallo failback van virtuele machine wordt gemaakt op Hallo-host die u wilt.

* *U kunt Storage vMotion niet gebruiken voor de hoofddoelserver hello*. Hierdoor kan Hallo failback toofail. Hallo virtuele machine starten niet omdat het Hallo-schijven zijn niet beschikbaar tooit.

  > [!WARNING]
  > Als een hoofddoel Storage vMotion taak na beveiligingspoging ondergaat, migreren Hallo beveiligde virtuele machines schijven die aangesloten toohello hoofddoel zijn toohello doel van Hallo vMotion taak. Als u toofail na deze, mislukt het loskoppelen van schijf Hallo omdat Hallo schijven zijn niet gevonden. Vervolgens wordt het vaste toofind Hallo schijven in uw storage-accounts. U moet toofind ze handmatig en koppelt u toohello virtuele machine. Daarna kan Hallo on-premises virtuele machine worden opgestart.

* Een bewaarperiode station tooyour bestaande Windows hoofddoelserver toevoegen. Voeg een nieuwe schijf en de indeling Hallo-station. Hallo bewaarstation is gebruikte toostop Hallo punten in de tijd wanneer Hallo virtuele machine back toohello lokale site gerepliceerd. Hier volgen enkele criteria van een bewaarstation. Zonder deze criteria Hallo station niet weergegeven Hallo hoofddoelserver.

   * Hallo-volume wordt niet gebruikt voor andere doeleinden, zoals een doel van de replicatie.

   * Hallo-volume is niet in de vergrendelingsmodus.

   * Hallo-volume is niet een cachevolume. installatie van de hoofddoelserver Hallo mag niet voorkomen op dat volume. Hallo aangepaste installatievolume voor Hallo proces server en de master-doel is niet in aanmerking komen voor een bewaarvolume. Wanneer Hallo processerver en de hoofddoelserver worden geïnstalleerd op een volume, is Hallo volume een cachevolume van het hoofddoel Hallo.

   * Hallo-bestandssysteem van Hallo volume is niet FAT of FAT32.

   * Hallo volumecapaciteit gelijk is aan nul.

   * Hallo standaard bewaarvolume voor Windows is hello R-volume.

   * Hallo standaard bewaarvolume voor Linux is /mnt/retention.

  > [!IMPORTANT]
  > Als u een bestaande proces server of configuratieserver server-machine of een schaal of een proces server-master doelmachine server moet u een nieuw station tooadd. het nieuwe station Hallo moet voldoen aan Hallo voorafgaand aan de vereisten. Als Hallo bewaarstation niet aanwezig is, wordt het niet weergegeven in Hallo selectie vervolgkeuzelijst op Hallo-portal. Nadat u een hoofddoel van station toohello lokale toevoegt, neemt het too15 minuten Hallo station tooappear in Hallo selectie op Hallo-portal. U kunt ook Hallo configuratieserver vernieuwen als Hallo station niet wordt weergegeven na 15 minuten.

* Een Linux failover virtuele machine vereist een Linux-hoofddoelserver. Een Windows failover virtuele machine vereist een Windows-hoofddoelserver.

* Installeer VMware tools op Hallo hoofddoelserver. Zonder Hallo VMware tools, kan niet Hallo datastores op Hallo hoofddoel van ESXi-host worden gedetecteerd.

* Hallo inschakelen `disk.EnableUUID=true` parameter op Hallo hoofddoel virtuele machine met behulp van Hallo vCenter eigenschappen. <!-- !todo Needs link. -->

* Hallo hoofddoel moet ten minste één VMFS datastore gekoppeld zijn. Als er geen, Hallo **Datastore** invoer op Hallo beveiligt pagina wordt niet leeg zijn en kan niet worden voortgezet.

* Hallo hoofddoelserver kan geen momentopnamen op Hallo schijven hebben. Als er momentopnamen, beveiligingspoging en failback is mislukt.

* Hallo hoofddoel kan niet een Paravirtuele SCSI-controller hebben. Hallo-controller kan alleen worden een LSI Logic-controller. Zonder een domeincontroller LSI Logic mislukt beveiligingspoging.

<!--
### Failback policy
tooreplicate back tooon-premises, you will need a failback policy. This policy get automatically created when you create a forward direction policy. Note that

1. This policy gets auto associated with hello configuration server during creation.
2. This policy is not editable.
3. hello set values of hello policy are (RPO Threshold = 15 Mins, Recovery Point Retention = 24 Hours, App Consistency Snapshot Frequency = 60 Mins)
   ![](./media/site-recovery-failback-azure-to-vmware-new/failback-policy.png)

-->

## <a name="steps-tooreprotect"></a>Stappen tooreprotect

> [!NOTE]
> Nadat een virtuele machine wordt opgestart in Azure, duurt het enige tijd voor de agent Hallo tooregister back toohello configuratieserver (omhoog too15 minuten). Gedurende deze tijd beveiligingspoging mislukt en wordt een foutbericht aangeeft dat die Hallo-agent is niet geïnstalleerd. Wacht een paar minuten en probeer het vervolgens opnieuw beveiligingspoging.



1. In **kluis** > **gerepliceerde items**Hallo virtuele machine die de storing opgetreden met de rechtermuisknop en selecteer vervolgens **opnieuw beveiligen**. U kunt ook klikken op Hallo machine en selecteer **opnieuw beveiligen** van Hallo opdrachtknoppen.
2. Hallo blade ziet die richting Hallo van beveiliging, **Azure tooOn-premises**, is al geselecteerd.
3. In **Hoofddoelserver** en **processerver**en selecteer Hallo lokale hoofddoelserver Hallo processerver.
4. Voor **Datastore**, selecteer Hallo datastore toowhich gewenste toorecover Hallo lokale schijven. Deze optie wordt gebruikt wanneer Hallo on-premises virtuele machine is verwijderd en u de nieuwe schijven toocreate moet. Deze optie wordt genegeerd als Hallo schijven is al aanwezig, maar u nog steeds toospecify een waarde moet.
5. Hallo bewaarstation kiezen.
6. Hallo failback-beleid wordt automatisch geselecteerd.
7. Klik op **OK** toobegin beveiligingspoging. Een taak begint tooreplicate Hallo virtuele machine van Azure toohello lokale site. U kunt Hallo voortgang volgen op Hallo **taken** tabblad.

Als u wilt dat toorecover tooan alternatieve locatie (wanneer Hallo on-premises virtuele machine wordt verwijderd), Hallo bewaarstation en gegevensopslag die zijn geconfigureerd voor de hoofddoelserver Hallo selecteren. Wanneer u geen back-toohello lokale site, hello VMware virtuele machines Hallo failback beveiliging plan gebruikt hetzelfde gegevensarchief als master Hallo Hallo doelserver. Een nieuwe virtuele machine wordt vervolgens gemaakt in vCenter.

Als u toorecover Hallo virtuele machine wilt op Azure tooan bestaande lokale virtuele machine, koppelpunt Hallo lokale datastores van virtuele machine met lees-/ schrijftoegang op Hallo hoofddoelserver ESXi-host.
    ![In het dialoogvenster opnieuw te beveiligen](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)

U kunt ook op Hallo niveau van een herstelplan beveiligt. Een replicatiegroep kan opnieuw worden beveiligd via een herstelplan alleen. Wanneer u met behulp van een herstelplan beveiligt, moet u tooprovide Hallo waarden voor elke beveiligde computer.

> [!NOTE]
> Gebruik Hallo dezelfde hoofddoel server tooreprotect een replicatiegroep. Als u een andere hoofddoelserver server tooreprotect een replicatiegroep gebruikt, kan geen Hallo-server een gemeenschappelijk punt in tijd leveren.

> [!NOTE]
> Hallo on-premises virtuele machine is uitgeschakeld tijdens de beveiligingspoging. Dit helpt ervoor te zorgen dat gegevens tijdens de replicatie. Zet niet op Hallo virtuele machine nadat beveiligingspoging is voltooid.

Nadat Hallo beveiligingspoging is geslaagd, voeren Hallo virtuele machine een beveiligde status.

## <a name="next-steps"></a>Volgende stappen

Nadat Hallo virtuele machine heeft een beschermd zijn ingevoerd, kunt u [initiëren van een failback](site-recovery-how-to-failback-azure-to-vmware.md#steps-to-fail-back). 

Hallo failback wordt Hallo virtuele machine in Azure en opstarten Hallo on-premises virtuele machine afgesloten. Enige uitvaltijd voor de toepassing hello verwacht. Kies een tijd voor failback wanneer Hallo toepassing uitvaltijd kan tolereren.

## <a name="common-problems"></a>Algemene problemen

* Als u een sjabloon toocreate op uw virtuele machines gebruikt, zorg ervoor dat elke virtuele machine een eigen UUID voor Hallo-schijven. Als Hallo lokale UUID is strijdig met die van het hoofddoel Hallo van virtuele machine omdat beide zijn gemaakt op basis van Hallo dezelfde sjabloon opnieuw beveiliging inschakelen is mislukt. Implementeren van een andere hoofddoelserver niet vanuit Hallo dezelfde gemaakt is sjabloon.

* Als u een alleen-lezen vCenter-gebruikersdetectie uitvoeren en virtuele machines beveiligen, beveiliging is geslaagd en failover werkt. Tijdens de beveiligingspoging mislukt de failover omdat Hallo datastores kan niet worden gedetecteerd. Een symptoom is dat Hallo datastores tijdens beveiligingspoging niet vermeld. tooresolve dit probleem kunt u Hallo vCenter referentie bijwerken met een juiste account met machtigingen voor, en het Hallo opnieuw proberen. Zie voor meer informatie [repliceren VMware virtuele machines en fysieke servers tooAzure met Azure Site Recovery](site-recovery-vmware-to-azure-classic.md).

* Wanneer u een failback uit op een virtuele Linux-machine en on-premises uitgevoerd, kunt u zien dat Hallo Network Manager-pakket is verwijderd van het Hallo-machine. Deze verwijdering gebeurt omdat Hallo netwerkbeheerder pakket wordt verwijderd wanneer Hallo virtuele machine in Azure is hersteld.

* Wanneer een virtuele Linux-machine is geconfigureerd met een statisch IP-adres en de failover wordt uitgevoerd tooAzure, wordt Hallo IP-adres verkregen van DHCP. Wanneer u een failover uitvoert tooon-premises, blijft Hallo virtuele machine toouse DHCP tooacquire Hallo IP-adres. Handmatig toohello machine aanmelden en stel Hallo IP-adres back tooa statisch adres zo nodig. De vaste IP-adres kunt opnieuw verkrijgen van een virtuele Windows-computer.

* Als u ESXi 5.5 gratis versie of editie free 6 vSphere-Hypervisor gebruikt, failover is uitgevoerd, maar failback niet is gelukt. tooenable failback Evaluatielicentie tooeither upgrade-programma.

* Als u de configuratieserver Hallo van de processerver Hallo niet kan bereiken, gebruik Telnet toocheck connectiviteit toohello configuratie-server op poort 443. U kunt ook proberen tooping Hallo configuratieserver van Hallo processerver. Processerver moet ook een heartbeat hebben wanneer het verbonden toohello configuratieserver.

* Als u toofail back tooan alternatieve vCenter probeert, ervoor zorgen dat uw nieuwe vCenter en de hoofddoelserver Hallo worden gedetecteerd. Een typische symptoom is Hallo datastores zijn niet toegankelijk of zichtbaar in Hallo **beveiligt** in het dialoogvenster.

* Een Windows Server 2008 R2 SP1-server die is beveiligd als een fysieke op lokale server kan niet worden uitgevoerd door Azure tooan lokale site.
