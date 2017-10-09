---
title: aaaFailback virtuele VMware-machines van Azure tooon-premises | Microsoft Docs
description: Meer informatie over back toohello lokale site na een failover van virtuele VMware-machines en fysieke servers tooAzure mislukken.
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 5a47337f-89a9-43e8-8fdc-7da373c0fb0f
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: ruturajd
ms.openlocfilehash: 258f5a55252083135b2040e5a235fa1ffbf3b9d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-toohello-on-premises-site"></a>Mislukken back virtuele VMware-machines en fysieke servers toohello on-premises site


Dit artikel wordt beschreven hoe toofailback Azure virtuele machines van Azure toohello lokale site. Volg de instructies Hallo hier wanneer u klaar bent toofail opnieuw in uw virtuele VMware-machines of fysieke servers voor Windows of Linux nadat u hebt uw gebruik van deze machines opnieuw beveiligd [verwijzing](site-recovery-how-to-reprotect.md).

>[!NOTE]
>Als u de klassieke Azure portal Hallo gebruikt, raadpleegt u tooinstructions vermeld [hier](site-recovery-failback-azure-to-vmware-classic.md) voor verbeterde VMware tooAzure architectuur en [hier](site-recovery-failback-azure-to-vmware-classic-legacy.md) voor Hallo verouderde architectuur

## <a name="overview"></a>Overzicht
Hallo-diagrammen in deze sectie geven Hallo failback architectuur voor dit scenario.

Wanneer Hallo processerver lokaal hebt en u een Azure ExpressRoute-verbinding gebruikt, gebruikt u deze architectuur:

![Architectuurdiagram voor ExpressRoute](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)

Wanneer Hallo processerver is op Azure en u hebt een VPN of een ExpressRoute-verbinding gebruiken van deze architectuur:

![Diagram voor VPN-architectuur](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)

Raadpleeg voor een volledige lijst van poorten en Hallo failback Architectuurdiagram toohello installatiekopie te volgen:

![Lijst van alle poorten failover failback](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

Nadat u via tooAzure mislukt hebt, kunt u back-tooyour lokale site niet in drie fasen:

* **Fase 1**: U hello Azure Virtual machines beveiligt, zodat deze beginnen back toohello virtuele VMware-machines die worden uitgevoerd op uw on-premises site repliceren.
* **Fase 2**: nadat uw Azure VM's gerepliceerde tooyour lokale site zijn, u een failover-toofail terug uitvoeren vanaf Azure.
* **Fase 3**: nadat u uw gegevens terug is mislukt, beveiligt Hallo lokale virtuele machines die u niet terug naar, zodat deze beginnen tooAzure repliceren.

### <a name="fail-back-toohello-original-location-or-an-alternate-location"></a>Mislukken van de oorspronkelijke locatie back toohello of een alternatieve locatie
Nadat u een VMware VM failover, kunt u back-toohello niet dezelfde bron VM als deze nog steeds lokale bestaat. In dit scenario alleen Hallo delta's terug mislukt.

Als de failover van fysieke servers failback is altijd tooa nieuwe VMware VM. Voordat u niet opnieuw een fysieke computer, houd er rekening mee dat:
* Een beveiligde fysieke machine wordt weer als een virtuele machine geleverd wanneer deze wordt een failover van Azure tooVMware. Een fysieke computer Windows Server 2008 R2 SP1 kan niet als deze wordt beveiligd en tooAzure, failover worden uitgevoerd voor terug. Een Windows Server 2008 R2 SP1-machine die gestart als een virtuele machine op lokale is kunnen toofail terug.
* Zorg ervoor dat u ten minste één hoofddoelserver detecteren samen met de Hallo nodig ESX/ESXi-hosts, moet u toofail terug naar.

Als u niet back toohello oorspronkelijke VM Hallo volgende is vereist:

* Als hello VM wordt beheerd door een vCenter-server, moet hello hoofddoel van ESX-host er toegang toohello VMs gegevensarchief.
* Als hello VM bevindt zich op een ESX-host, maar wordt niet beheerd door de vCenter, Hallo harde schijf van Hallo VM moet zich in een gegevensopslag die toegankelijk is voor Hallo van MT host.
* Als uw virtuele machine zich op een ESX-host en maakt geen gebruik van vCenter, moet u detectie van ESX-host Hallo Hallo MT uitvoeren voordat u opnieuw beveiligen. Dit geldt als u bent terug fysieke servers te mislukken.
* Een andere optie (als Hallo op locatie VM zich bevindt) is toodelete deze voordat u een failback. Failback maakt vervolgens een nieuwe virtuele machine op Hallo dezelfde als Hallo hoofddoel ESX-host host.

Wanneer u een alternatieve locatie back tooan failover, Hallo gegevens herstelde toohello is dezelfde gegevensopslag en Hallo dezelfde ESX-host die Hallo lokale hoofddoelserver.

## <a name="prerequisites"></a>Vereisten
* toofail back virtuele VMware-machines en fysieke servers, moet u een VMware-omgeving. Mislukt back tooa fysieke server wordt niet ondersteund.
* toofail terug, u moet hebt gemaakt een Azure-netwerk wanneer u in eerste instantie beveiliging instelt. Failback moet een VPN- of ExpressRoute-verbinding van hello Azure netwerk waarin hello Azure VM's zijn bevinden toohello lokale site.
* Als een back-Hallo virtuele machines die u wilt dat toofail tooare beheerd door een vCenter-server, zorg ervoor dat u de vereiste machtigingen voor de detectie van virtuele machines op de vCenter-servers hebben Hallo. Zie voor meer informatie [repliceren VMware virtuele machines en fysieke servers tooAzure met Azure Site Recovery](site-recovery-vmware-to-azure-classic.md).
* Als u momentopnamen aanwezig zijn op een virtuele machine, mislukt de beveiligingspoging. U kunt momentopnamen Hallo of Hallo schijven verwijderen.
* Voordat u een failback uit op, maakt u deze onderdelen:
  * **Maken van een processerver in Azure**. Dit onderdeel is een Azure VM die u maakt en blijven uitvoeren tijdens de failback. Nadat de failback is voltooid, kunt u Hallo VM verwijderen.
  * **Maken van een hoofddoelserver**: hoofddoelserver Hallo gegevens verzendt en ontvangt failback. Hallo-beheerserver die u hebt lokale gemaakt heeft een hoofddoelserver die standaard wordt geïnstalleerd. Echter, afhankelijk van Hallo verkeersvolume is mislukt-back moet u mogelijk een afzonderlijke hoofddoelserver toocreate voor failback.
  * Hallo Linux VM toocreate een extra hoofddoelserver die wordt uitgevoerd op Linux, instellen voordat u Hallo hoofddoelserver installeert, zoals verderop wordt beschreven.
* Een configuratieserver is vereist on-premises als u een failback doet. Tijdens de failback moet Hallo virtuele machine in de configuratiedatabase server Hallo bestaat. Failback kan niet worden voltooid als Hallo configuratie server-database geen VM bevat. Controleer dus regelmatig geplande back-ups van uw server te maken. In een noodgeval moet u toorestore met Hallo hetzelfde IP-adres zodat dat failback werkt.
* Instellen Hallo disk.enableUUID=true in **configuratieparameters** van Hallo master gericht op virtuele machine in VMware. Als deze rij niet bestaat, moet u deze toevoegen. Deze instelling is vereist tooprovide een consistente (UUID) universally unique identifier toohello virtuele machine schijf (VMDK)-bestand, zodat deze correct is gekoppeld.
* Houd rekening met een ' Master doelserver opslag vMotioned mag niet ' voorwaarde, wat leiden Hallo failback toofail tot kan. Hallo VM kan niet actief omdat Hallo schijven beschikbaar tooit zijn niet gemaakt.
* Een station, een station bewaren op de hoofddoelserver Hallo aangeroepen toevoegen. Een schijf toevoegen en Hallo station formatteren.

## <a name="failback-policy"></a>Beleid voor failback
tooreplicate back tooon-premises, moet u een beleid voor failback. Hallo-beleid wordt automatisch gemaakt wanneer u een vooruit-beleid maken en automatisch gekoppeld aan de configuratieserver Hallo is. Deze kan niet worden bewerkt. Hallo beleid heeft Hallo na replicatie-instellingen:

* RPO drempelwaarde = 15 minuten
* Herstel bewaarperiode = 24 uur
* App-consistente momentopname frequentie = 60 minuten

 ![Replicatie-instellingen van Hallo failback-beleid](./media/site-recovery-failback-azure-to-vmware-new/failback-policy.png)

## <a name="set-up-a-process-server-in-azure"></a>Instellen van een processerver in Azure
Installeer een processerver in Azure zodat hello Azure Virtual machines Hallo gegevens back toohello lokale hoofddoelserver kunt verzenden.

Als u uw virtuele machines als klassieke resources hebt beveiligd (dat wil zeggen, Hallo VM hersteld in Azure is voor een virtuele machine die is gemaakt met het klassieke implementatiemodel Hallo), moet u een processerver in Azure. Als u de Hallo VM's met Azure Resource Manager als Hallo implementatietype hebt hersteld, moet Hallo processerver Resource Manager als Hallo implementatietype hebben. Hallo implementatietype is geselecteerd door hello Azure virtuele netwerk die u implementeert Hallo processerver aan.

1. In **kluis** > **instellingen** > **Site Recovery-infrastructuur** (onder **beheren**) > **Configuratieservers** (onder **voor VMware en fysieke Machines**), selecteer Hallo configuratieserver.
2. Klik op **verwerken Server**.

  ![Knop Server verwerken](./media/site-recovery-failback-azure-to-vmware-classic/add-processserver.png)
3. Kies toodeploy Hallo processerver als **een failback processerver in Azure implementeren**.
4. Hallo-abonnement dat u hebt hersteld Hallo VM's te selecteren.
5. Selecteer hello Azure-netwerk dat u hebt hersteld Hallo VM's. Hallo moet processerver toobe in Hallo netwerk zodat Hallo hersteld VM's en hello processerver kan communiceren.
6. Als u hebt geselecteerd een *klassieke implementatiemodel* netwerk en Hallo processerver vervolgens installeren in het maken van een virtuele machine via hello Azure Marketplace.

 ![Hallo 'processerver toevoegen' venster](./media/site-recovery-failback-azure-to-vmware-classic/add-classic.png)

 Als u Hallo processerver maakt, betaalt u aandacht toohello volgende:
 * Hallo-naam van de installatiekopie van het Hallo is *Microsoft Azure Site Recovery proces Server V2*. Selecteer **klassieke** als Hallo-implementatiemodel.

       ![Select "Classic" as hello Process Server deployment model](./media/site-recovery-failback-azure-to-vmware-classic/templatename.png)
 * Installeer Hallo processerver volgens toohello-instructies in [repliceren VMware virtuele machines en fysieke servers tooAzure met Azure Site Recovery](site-recovery-vmware-to-azure-classic.md).
7. Als u Hallo selecteert *Resource Manager* Azure netwerk, Hallo processerver dankzij de volgende informatie Hallo implementeren:

  * Hallo-naam van resourcegroep Hallo die u toodeploy Hallo server wilt
  * Hallo-naam van Hallo-server
  * Een gebruikersnaam en wachtwoord voor het aanmelden toohello server
  * Hallo storage-account dat u toodeploy Hallo server wilt
  * Hallo-subnet en Hallo netwerkinterface die u wilt dat tooconnect tooit
   >[!NOTE]
   >Moet u uw eigen [netwerkinterface](../virtual-network/virtual-networks-multiple-nics.md) (NIC) en selecteer het terwijl u Hallo processerver implementeert.

    ![Geef informatie op in het dialoogvenster van Hallo 'processerver toevoegen'](./media/site-recovery-failback-azure-to-vmware-classic/psinputsadd.png)

8. Klik op **OK**. Deze actie wordt een taak die u een Resource Manager deployment type virtuele machine tijdens de installatie van de processerver Hallo maakt geactiveerd. tooregister hello server toohello configuratieserver, setup uitvoeren Hallo binnen VM Hallo door Hallo-instructies in [repliceren VMware virtuele machines en fysieke servers tooAzure met Azure Site Recovery](site-recovery-vmware-to-azure-classic.md). Een taak toodeploy Hallo processerver ook wordt geactiveerd.

  Hallo processerver beschikbaar zijn op Hallo **configuratieservers** > **servers die zijn gekoppeld** > **processervers** tabblad.

    ![](./media/site-recovery-failback-azure-to-vmware-new/pslistingincs.png)

    > [!NOTE]
    > Hallo processerver niet worden weergegeven onder **VM-eigenschappen**. Is alleen op Hallo **Servers** tabblad in Hallo-beheerserver die wordt het geregistreerd bij. Het kan 10 too15 minuten duren voordat Hallo processerver tooappear.


## <a name="set-up-hello-master-target-server-on-premises"></a>Hallo hoofddoel server on-premises, instellen
de hoofddoelserver Hallo ontvangt Hallo failback gegevens. Hallo-server wordt automatisch geïnstalleerd op Hallo lokale management-server, maar als u bent niet terug te veel gegevens, moet u mogelijk tooset van een extra hoofddoelserver. tooset van een model server on-premises, als doel, Hallo te volgen:

> [!NOTE]
> tooset van een hoofddoelserver op Linux, de volgende procedure toohello overslaan. Gebruik alleen CentOS 6.6 minimaal besturingssysteem als Hallo hoofddoel OS.

1. Als u de hoofddoelserver Hallo op Windows instelt, opent u Hallo snel starten-pagina van Hallo VM die u op de hoofddoelserver Hallo installeert.
2. Download het installatiebestand Hallo voor hello Azure Site Recovery Unified Setup-wizard.
3. Hallo setup uitvoeren en in **voordat u begint met**, selecteer **toevoegen van extra Servers proces tooscale uit implementatie**.
4. Wizard voltooid Hallo in Hallo dezelfde manier als wanneer u [Hallo server instellen](site-recovery-vmware-to-azure-classic.md). Op Hallo **Server configuratiedetails** pagina, Hallo IP-adres van de hoofddoelserver hello en voert u een wachtwoordzin tooaccess Hallo VM.

### <a name="set-up-a-linux-vm-as-hello-master-target-server"></a>Linux-VM instellen als de hoofddoelserver Hallo
tooset up beheerserver Hallo Hallo hoofddoelserver uitgevoerd als een Linux-VM Hallo CentOS 6.6 minimaal besturingssysteem installeren. Vervolgens Hallo SCSI-id's voor elke harde SCSI-schijf ophalen, een aantal extra pakketten installeren en een aantal aangepaste wijzigingen toepassen.

#### <a name="install-centos-66"></a>CentOS 6.6 installeren

1. Installeer minimaal besturingssysteem Hallo CentOS 6.6 op Hallo-beheerserver VM. Hallo ISO op een DVD-station te houden en Hallo opstartsysteem. Overslaan Hallo media testen. Selecteer **Amerikaans Engels** Hallo-taal selecteren **Basic opslagapparaten**, Controleer of de vaste schijf Hallo geen belangrijke gegevens, klik op **Ja**, en alle gegevens te wissen. Voer Hallo-hostnaam van de beheerserver Hallo en Hallo server-netwerkadapter selecteert.  In Hallo **System bewerken** dialoogvenster, **automatisch verbinding maken**, en voegt u een statisch IP-adres, het netwerk en DNS-instellingen. Geef een tijdzone. tooaccess Hallo-beheerserver, Voer Hallo root-wachtwoord.
2. Wanneer u wordt gevraagd welk type installatie dat u wilt, selecteert u **maken aangepaste lay-out** als Hallo-partitie. Klik op **Volgende**. Selecteer **vrije**, en klik vervolgens op **maken**. Maak  **/** , **/var/crash**, en **/home partities** met **FS Type:** **ext4**. Hallo wisselen partitie als **FS Type: wisselen**.
3. Als de bestaande apparaten zijn gevonden, wordt er een waarschuwing weergegeven. Klik op **indeling** tooformat Hallo station met de Hallo partitie-instellingen. Klik op **schrijven wijzigen toodisk** tooapply Hallo partitie wijzigingen.
4. Selecteer **installeren opstartlaadprogramma** > **volgende** tooinstall Hallo opstartlaadprogramma op Hallo hoofdmap partitie.
5. Wanneer het Hallo-installatie is voltooid, klikt u op **opnieuw opstarten**.

#### <a name="retrieve-hello-scsi-ids"></a>Hallo SCSI-id's ophalen

1. Na de installatie Hallo Hallo SCSI-id's voor elke harde SCSI-schijf in Hallo VM worden opgehaald. Hallo-beheerserver VM toodo dus afgesloten. In de VM-eigenschappen Hallo in VMware, met de rechtermuisknop op Hallo VM > **instellingen bewerken** > **opties**.
2. Selecteer **Geavanceerd** > **algemene**, en klik vervolgens op **configuratieparameters**. Deze optie is niet beschikbaar wanneer Hallo machine wordt uitgevoerd. Voor Hallo optie toobe beschikbaar is, moet u Hallo machine afgesloten.
3. Hallo volgende doen:
 * Als hello rij **schijf. EnableUUID** bestaat, zorg ervoor dat de waarde hello te is ingesteld**True** (hoofdlettergevoelig). U kunt als Hallo-waarde is al ingesteld voor tooTrue, annuleren en test Hallo SCSI-opdracht in een gastbesturingssysteem nadat deze opnieuw wordt opgestart.
 * Als hello rij **schijf. EnableUUID** niet bestaat, klikt u op **rij toevoegen**, en voeg deze toe met de Hallo **True** waarde. Gebruik geen dubbele aanhalingstekens.

#### <a name="install-additional-packages"></a>Extra pakketten installeren
Downloaden en installeren van extra pakketten.

1. Zorg ervoor dat de hoofddoelserver Hallo verbonden toohello Internet.
2. toodownload en 15 installatiepakketten van Hallo CentOS-opslagplaats, voor deze opdracht uitvoeren: `# yum install –y xfsprogs perl lsscsi rsync wget kexec-tools`.
3. Als Hallo bronmachines die u wilt beveiligen Linux wordt uitgevoerd met een Reiser of XFS bestandssysteem voor de basis- of apparaat hello, downloaden en installeren van extra pakketten als volgt:

   * \#cd /usr/local
   * \#wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm)
   * \#wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm)
   * \#reiserfs in de rpm – ivh-kmod reiserfs-0,0 1.el6.elrepo.x86_64.rpm-utils-3.6.21-1.el6.elrepo.x86_64.rpm
   * \#wget [http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm](http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm)
   * \#– ivh xfsprogs-3.1.1 rpm-16.el6.x86_64.rpm
   * \#YUM apparaat mapper MPIO (multipath pakketten voor de vereiste tooenable op de hoofddoelserver Hallo) installeren

#### <a name="apply-custom-changes"></a>Aangepaste wijzigingen toepassen
Nadat u Hallo na de installatie stappen en geïnstalleerde hello-pakketten hebt voltooid, kunt u aangepaste wijzigingen toepassen door Hallo volgende te doen:

1. Kopieer Hallo RHEL 6 64 Unified Agent binaire toohello VM. toountar hello binaire, deze opdracht uitvoeren: `tar –zxvf <file name>`.
2. toogive machtigingen, deze opdracht uitvoeren: `# chmod 755 ./ApplyCustomChanges.sh`.
3. Voer hello volgende script: `# ./ApplyCustomChanges.sh`. Slechts één keer wordt uitgevoerd. Hallo-server opnieuw opstarten nadat deze is uitgevoerd.

## <a name="run-hello-failback"></a>Hallo failback uitvoeren
### <a name="reprotect-hello-azure-vms"></a>Beveiligt hello Azure Virtual machines
1. In **kluis**in **gerepliceerde items**Hallo VM die is via is mislukt met de rechtermuisknop en selecteer vervolgens **opnieuw beveiligen**.
2. Op Hallo blade ziet u dat richting Hallo van beveiliging **Azure tooOn-premises** is al geselecteerd.
3. In **Hoofddoelserver** en **processerver**en selecteer Hallo lokale hoofddoelserver hello Azure VM processerver.
4. Selecteer Hallo gegevensarchief dat u wilt dat toorecover Hallo schijven on-premises naar. Gebruik deze optie wanneer Hallo on-premises virtuele machine is verwijderd en moet u de nieuwe schijven toocreate. Hallo-optie negeren als hello schijven al bestaan, maar u nog steeds toospecify een waarde moet.
5. Gebruik een bewaarpunten station toostop Hallo in tijd wanneer Hallo VM gerepliceerde back tooon-premises. Sommige criteria van een bewaarstation worden hier weergegeven. Zonder deze criteria Hallo station niet wordt vermeld voor Hallo hoofddoelserver.

  * Volume mag niet worden gebruikt voor andere doeleinden (doel van replicatie, enzovoort).
  * Volume mag niet zijn vergrendeld.
  * Volume mag niet het cachevolume zijn. (de installatie van de hoofddoelserver Hallo mag niet voorkomen op dat volume. Hallo processerver plus master doelvolume voor aangepaste installatie is niet in aanmerking komen voor bewaarvolume. Hier Hallo geïnstalleerd processerver plus hoofddoel volume is Hallo cachevolume van het hoofddoel Hallo.)
  * Hallo type bestandssysteem volume mag niet FAT en FAT32.
  * Hallo volumecapaciteit mag niet nul zijn.
  * Hallo standaard bewaarvolume voor Windows is R-volume.
  * Hallo standaard bewaarvolume voor Linux is /mnt/retention.

6. Hallo failback-beleid wordt automatisch geselecteerd.
7. Nadat u op **OK** toobegin beveiligingspoging, een taak begint tooreplicate Hallo VM van Azure toohello lokale site. U kunt Hallo voortgang volgen op Hallo **taken** tabblad.

Als u toorecover tooan alternatieve locatie wilt, selecteer Hallo bewaarstation en gegevensopslag die zijn geconfigureerd voor Hallo hoofddoelserver. Wanneer u geen back-toohello lokale site, Hallo virtuele VMware-machines in Hallo failback beveiligingsplan hello gebruiken hetzelfde gegevensarchief als Hallo hoofddoelserver. Als u wilt dat toorecover Hallo replica virtuele machine van Azure toohello dezelfde lokale VM, Hallo lokale VM moet al worden in Hallo dezelfde datastore als Hallo hoofddoelserver. Als er geen VM on-premises, wordt een nieuwe tijdens beveiligingspoging gemaakt.

![Selecteer 'Azure tooon lokale' in de vervolgkeuzelijst Hallo](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)

U kunt ook op een niveau van de planning recovery beveiligt. Als u een replicatiegroep hebt, kunt u alleen met behulp van een herstelplan beveiligt. Wanneer u opnieuw beveiligen met behulp van een herstelplan, moet u de vorige waarden hello gebruiken voor elke beveiligde computer.

> [!NOTE]
> Replicatiegroepen moeten worden beveiligd met de Hallo dezelfde hoofddoel. Als ze worden beschermd met de andere hoofddoelserver servers, kan niet voor deze algemene punt in tijd worden bepaald.

### <a name="run-a-failover-toohello-on-premises-site"></a>Voer een failover toohello on-premises site
Nadat u Hallo VM beveiligt, kunt u een failover van Azure tooon-premises starten.

1. Klik op pagina Hallo gerepliceerde items met de rechtermuisknop op Hallo virtuele machine en selecteer vervolgens **niet-geplande Failover**.
2. In **bevestigen Failover**, Controleer of de failoverrichting hello (van Azure) en selecteer Hallo herstelpunt dat u toouse Hallo failover (laatste Hallo of Hallo meest recente app-consistente herstelpunt wenst). Een app-consistente herstelpunt vindt plaats voordat de meest recente herstelpunt Hallo tijdstip en wordt dit ertoe leiden dat er gegevens verloren gaan.
3. Site Recovery afgesloten hello Azure VM's tijdens failover. Nadat u hebt gecontroleerd dat failback is voltooid zoals verwacht, kunt u controleren tooensure die hello Azure VM's hebt afgesloten zoals verwacht.

### <a name="reprotect-hello-on-premises-site"></a>Beveiligt Hallo lokale site
Nadat de failback is voltooid, doorvoeren Hallo virtuele machine tooensure die virtuele machines in Azure hersteld Hallo verwijderd. toodo dus met de rechtermuisknop op Hallo beveiligde item en klik vervolgens op **doorvoeren**. Deze actie wordt een taak die Hallo voormalige herstelde virtuele machines in Azure verwijdert geactiveerd.

Nadat Hallo doorvoeren is voltooid, worden uw gegevens terug op Hallo lokale site moet zijn, maar won't worden beveiligd. toostart replicerende tooAzure opnieuw Hallo te volgen:

1. In **kluis**in **instelling** > **gerepliceerde items**, selecteer Hallo-virtuele machines die zijn mislukt terug en klik vervolgens op **opnieuw beveiligen**.
2. Hallo-waarde van Hallo processerver die toobe gebruikt toosend gegevens back tooAzure moet geven.
3. Klik op **OK**.

Nadat Hallo beveiligingspoging voltooid is, Hallo VM repliceert back tooAzure en kunt u een failover uitvoeren.

### <a name="resolve-common-failback-issues"></a>Veelvoorkomende failback problemen oplossen
* Als u een alleen-lezen vCenter-gebruikersdetectie uitvoert en beveiligen van virtuele machines, het is gelukt en failover werkt. Tijdens de beveiligingspoging mislukt de failover omdat Hallo datastores kan niet worden gedetecteerd. Als een symptoom zijn, worden er geen Hallo datastores tijdens beveiligingspoging vermeld. tooresolve dit probleem, u kunt Hallo vCenter referentie bijwerken met een juiste account met machtigingen en Hallo taak opnieuw. Zie voor meer informatie [repliceren VMware virtuele machines en fysieke servers tooAzure met Azure Site Recovery](site-recovery-vmware-to-azure-classic.md)
* Wanneer u een failback uit op een Linux-VM en on-premises uitgevoerd, kunt u zien dat Hallo Network Manager-pakket is verwijderd van het Hallo-machine. Deze verwijdering gebeurt omdat Hallo netwerkbeheerder pakket wordt verwijderd wanneer Hallo VM is hersteld in Azure.
* Wanneer een virtuele machine is geconfigureerd met een statisch IP-adres en de failover wordt uitgevoerd tooAzure, wordt Hallo IP-adres verkregen via DHCP. Wanneer u een back-tooon-premises failover, blijft Hallo VM toouse DHCP tooacquire Hallo IP-adres. Handmatig toohello machine aanmelden en stel Hallo IP-adres back tooa statisch adres zo nodig.
* Als u van ESXi 5.5 gratis versie of editie free 6 vSphere-Hypervisor gebruikmaakt, failover zou slagen, maar failback niet zou slagen. tooenable failback Evaluatielicentie tooeither upgrade-programma.
* Als u de configuratieserver Hallo van Hallo processerver niet kan bereiken, Controleer de connectiviteit toohello configuratieserver door Telnet toohello configuratie servermachine op poort 443. U kunt ook proberen tooping Hallo configuratieserver van Hallo processerver machine. Processerver moet ook een heartbeat hebben wanneer het verbonden toohello configuratieserver.
* Als u toofail back tooan alternatieve vCenter probeert, zorg ervoor dat uw nieuwe vCenter wordt gedetecteerd en dat Hallo hoofddoelserver ook wordt gedetecteerd. Een typische symptoom is Hallo datastores zijn niet toegankelijk of zichtbaar in Hallo **beveiligt** in het dialoogvenster.
* Een WS2008R2SP1-machine die wordt beveiligd als een fysieke on-premises machine kan niet worden mislukt door Azure tooon-premises.

## <a name="fail-back-with-expressroute"></a>Mislukt met de ExpressRoute
U kunt niet terug via een VPN-verbinding of met behulp van een ExpressRoute-verbinding. Als u toouse een ExpressRoute-verbinding wilt, let u op Hallo volgende:

* Hallo ExpressRoute-verbinding moet worden ingesteld op Hallo Azure-netwerk dat failover tooand Hallo bronmachines waarin hello Azure Virtual machines bevinden nadat Hallo failover plaatsvindt.
* Gegevens zijn gerepliceerde tooan Azure storage-account op een openbaar eindpunt. toouse een ExpressRoute-verbinding instellen openbare peering in ExpressRoute met Hallo doel-Datacenter voor replicatie van Site Recovery.
