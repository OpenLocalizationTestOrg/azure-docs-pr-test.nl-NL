---
title: aaaFail back virtuele VMware-machines van Azure in de klassieke portal Hallo | Microsoft Docs
description: Meer informatie over back toohello lokale site na een failover van virtuele VMware-machines en fysieke servers tooAzure mislukken.
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 7ca86e21-7a5d-45ab-8f4b-e42da90f199a
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: 80bc3ab2708a5df953c6532b353da19a4c44ac34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-toohello-on-premises-site-classic-portal"></a>Mislukken back virtuele VMware-machines en fysieke servers toohello on-premises site (klassieke portal)
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-failback-azure-to-vmware.md)
> * [Klassieke Azure Portal](site-recovery-failback-azure-to-vmware-classic.md)
> * [Klassieke Azure-Portal (verouderd)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

Dit artikel wordt beschreven hoe toofail back-Azure virtuele machines van Azure toohello lokale site. Volg de instructies in Hallo in dit artikel als u klaar toofail bent uw virtuele VMware-machines of fysieke Windows of Linux-servers back-nadat ze hebt failover van Hallo lokale site tooAzure gebruik van deze [zelfstudie](site-recovery-vmware-to-azure-classic.md).

## <a name="overview"></a>Overzicht
Dit diagram toont Hallo failback architectuur voor dit scenario.

Gebruik deze architectuur als processerver Hallo lokaal hebt en u een ExpressRoute gebruikt.

![](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)

Gebruik deze architectuur wanneer Hallo processerver in Azure en u een VPN of een ExpressRoute-verbinding hebt.

![](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)

Raadpleeg de toosee Hallo volledige lijst met poorten en Hallo failback architechture diagram toohello in onderstaande afbeelding

![](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

Dit is de werking van failback:

* Nadat u via tooAzure mislukt hebt, kunt u back-tooyour lokale site niet in een aantal fasen:
  * **Fase 1**: U hello Azure Virtual machines beveiligt, zodat deze beginnen back tooVMware VM's worden uitgevoerd in uw on-premises site repliceren. Inschakelen van beveiligingspoging Hallo VM is verplaatst naar een failback-beveiligingsgroep die automatisch is gemaakt toen u oorspronkelijk Hallo failover-beveiligingsgroep hebt gemaakt. Als u uw failover-groep tooa herstel beveiligingsplan toegevoegd vervolgens Hallo failback beveiligingsgroep is ook automatisch toegevoegd toohello plan.  Tijdens het beveiligt opgeven u hoe tooplan toofail reservekopieën.
  * **Fase 2**: nadat u uw Azure VM's zijn tooyour lokale site repliceren, u een mislukken uitvoert via toofail van Azure.
  * **Fase 3**: nadat u uw gegevens terug is mislukt, beveiligt Hallo lokale virtuele machines die u niet terug naar, zodat deze beginnen tooAzure repliceren.


  [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failback/player]

### <a name="failback-toohello-original-or-alternate-location"></a>Failback toohello oorspronkelijke of alternatieve locatie
Als de failover van een VMware VM kunt u back-toohello niet dezelfde bron VM als deze nog steeds lokale bestaat. In dit scenario alleen nog deltawijzigingen Hallo terug mislukt. Opmerking:

* Als u fysieke servers failover en failback altijd tooa is nieuwe VMware VM.
  * Let voordat u weer een fysieke computer mislukt
  * Fysieke machine die wordt beveiligd pas als een virtuele machine wanneer failover van Azure tooVMware
  * Zorg ervoor dat u minimaal één hoofddoel server samen met de Hallo nodig ESX/ESXi-hosts toowhich ontdekt u toofailback nodig.
* Als u failback is toohello oorspronkelijke VM Hallo volgende vereist:

  * Als wordt hello VM beheerd door een vCenter-server moet toegang toohello VMs datastore hebben op Hallo Master doel-ESX-host.
  * Als hello VM op een ESX-host is, maar wordt niet beheerd door de vCenter moet Hallo harde schijf van Hallo VM zich in een gegevensopslag die toegankelijk is door Hallo van MT host.
  * Als uw virtuele machine op een ESX-host en maakt geen gebruik van vCenter moet u detectie van ESX-host Hallo Hallo MT uitvoeren voordat u opnieuw beveiligen. Dit geldt als u bent terug fysieke servers te mislukken.
  * Een andere optie (als Hallo op locatie VM zich bevindt) is toodelete deze voordat u een failback. Failback wordt vervolgens maakt vervolgens een nieuwe virtuele machine op Hallo dezelfde als Hallo hoofddoel ESX-host host.
* Wanneer u failback tooan alternatieve locatie Hallo gegevens herstelde toohello worden dezelfde gegevensopslag en Hallo dezelfde ESX-host die Hallo lokale hoofddoelserver.

## <a name="prerequisites"></a>Vereisten
* U moet een VMware-omgeving in volgorde toofail back virtuele VMware-machines en fysieke servers. Mislukt back tooa fysieke server wordt niet ondersteund.
* In de volgorde toofail moet terug u hebt gemaakt een Azure-netwerk wanneer u in eerste instantie beveiliging instelt. Failback moet een VPN- of ExpressRoute-verbinding van hello Azure netwerk waarin hello Azure VM's zijn bevinden toohello lokale site.
* Desgewenst Hallo VMs toofail back tooare die worden beheerd door een vCenter-server moet u zeker dat u Hallo vereist machtigingen voor de detectie van virtuele machines op de vCenter-servers hebt toomake. [Lees meer](site-recovery-vmware-to-azure-classic.md).
* Als u momentopnamen aanwezig zijn op een virtuele machine mislukken waarvoor. U kunt momentopnamen Hallo of Hallo schijven verwijderen.
* Voordat u failback moet u een aantal onderdelen toocreate:
  * **Maken van een processerver in Azure**. Dit is een Azure VM dat u toocreate moet en tijdens de failback uitvoeren blijven. Nadat de failback is voltooid, kunt u Hallo machine verwijderen.
  * **Maken van een hoofddoelserver**: hoofddoelserver Hallo gegevens verzendt en ontvangt failback. Hallo-beheerserver is gemaakt van lokale heeft een hoofddoelserver standaard geïnstalleerd. Echter, afhankelijk van Hallo verkeersvolume mislukte back moet u mogelijk een afzonderlijke hoofddoelserver toocreate voor failback.
  * Als u een extra hoofddoelserver waarop Linux toocreate wilt, moet u tooset up Hallo Linux-VM voordat u Hallo hoofddoelserver installeert, zoals hieronder wordt beschreven.
* Configuratieserver is vereist on-premises wanneer u een failback doen. Hallo virtuele machine moet tijdens de failback bestaat in Hallo server-configuratiedatabase, mislukken welke failback niet worden voltooid. Daarom zorgen ervoor dat u regelmatig geplande back-up van uw server. In geval van een ramp, hoeft u toorestore met Hallo hetzelfde IP-adressen zodat failback zullen werken.

## <a name="set-up-hello-process-server-in-azure"></a>Instellen van de processerver Hallo in Azure
U moet tooinstall processerver in Azure zodat hello Azure Virtual machines Hallo gegevens back tooon-premises hoofddoelserver kan verzenden.

1. In de Site Recovery-portal Hallo > **configuratieservers** tooadd een nieuw processerver selecteren.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps1.png)
2. Geef een servernaam van het proces en voer een naam en het wachtwoord dat u tooconnect toohello Azure VM als beheerder. In **configuratieserver** Selecteer Hallo lokale beheerserver en geef hello Azure netwerk in welke Hallo processerver moet worden geïmplementeerd. Dit moet Hallo netwerk waarin hello Azure VM's zich bevinden. Geef een uniek IP-adres van Hallo Selecteer subnet en begint met implementeren.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps2.png)

   Een taakserver toodeploy Hallo proces wordt gestart

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps3.png)

   Na het Hallo processerver geïmplementeerd in Azure die u kunt zich aanmelden op met behulp van Hallo-referenties die u hebt opgegeven. Hallo wordt eerste keer dat u zich aanmeldt dialoogvenster Hallo proces-server uitgevoerd. Type IP-adres in Hallo Hallo on-premises beheerserver en de wachtwoordzin. Laat de standaardinstelling poort 443 Hallo. U kunt laten Hallo 9443 standaardpoort voor gegevensreplicatie tenzij u deze instelling specifiek gewijzigd bij het instellen van Hallo lokale beheerserver.

   > [!NOTE]
   > Hallo-server zijn alleen zichtbaar onder **VM-eigenschappen**. Dit is alleen zichtbaar onder Hallo **Servers** tabblad in Hallo management server toowhich die geregistreerd. Het kan duren over 10-15 minuten voor Hallo proces server tooappear.
   >
   >

## <a name="set-up-hello-master-target-server-on-premises"></a>Hallo hoofddoel server on-premises, instellen
de hoofddoelserver Hallo ontvangt Hallo failback gegevens. Een hoofddoelserver wordt automatisch geïnstalleerd op Hallo lokale management-server, maar als u terug grote hoeveelheden gegevens mislukken bent moet u mogelijk tooset van een extra hoofddoelserver. Dit als volgt:

> [!NOTE]
> Als u tooinstall een hoofddoelserver op Linux wilt, instructies Hallo in de volgende procedure Hallo.
>
>

1. Als u op Windows hello hoofddoelserver installeert, opent u Hallo snel starten-pagina van Hallo VM waarop u de hoofddoelserver Hallo installeert en download het installatiebestand Hallo voor hello Azure Site Recovery Unified Setup-wizard.
2. Het installatieprogramma uitvoert en in **voordat u begint met** selecteren **toevoegen van extra proces servers tooscale uit implementatie**.
3. Wizard voltooid Hallo in Hallo dezelfde manier als wanneer u [Hallo server instellen](site-recovery-vmware-to-azure-classic.md). Op Hallo **Server configuratiedetails** pagina, Hallo IP-adres van deze hoofddoelserver en een wachtwoordzin tooaccess Hallo VM opgeven.

### <a name="set-up-a-linux-vm-as-hello-master-target-server"></a>Linux-VM instellen als de hoofddoelserver Hallo
tooset up beheerserver Hallo Hallo hoofddoelserver uitgevoerd als een Linux VM moet u tooinstall Hallo Cent) S 6.6 minimaal-besturingssysteem, Hallo SCSI-id's voor elke harde SCSI-schijf ophalen, een aantal extra pakketten installeren en een aantal aangepaste wijzigingen toepassen.

#### <a name="install-centos-66"></a>CentOS 6.6 installeren
1. Installeer minimaal besturingssysteem Hallo CentOS 6.6 op Hallo-beheerserver VM. Houd Hallo ISO in een DVD-station en opstarten Hallo-systeem. Overslaan Hallo testen, selecteer Amerikaans Engels op Hallo taal, selecteer **Basic opslagapparaten**, Controleer of de vaste schijf Hallo niet er belangrijke gegevens op en klikt u op **Ja**, geen gegevens verwijderen. Voer Hallo-hostnaam van de beheerserver Hallo en Hallo server-netwerkadapter selecteert.  In Hallo **System bewerken** dialoogvenster Selecteer ** automatisch verbinding maken ** en een statisch IP-adres, het netwerk en DNS-instellingen toe te voegen. Geef een tijdzone en een wachtwoord tooaccess hello hoofdbeheerserver.
2. Wanneer u wordt gevraagd Hallo type installatie dat u wilt selecteren dat **maken aangepaste lay-out** als Hallo-partitie. Nadat u op **volgende** Selecteer **vrije** en klik op maken. Maak  **/** , **/var/crash** en **/home partities** met **FS Type:** **ext4**. Maken van Hallo wisselen partion als **FS Type: wisselen**.
3. Als bestaande apparaten zijn gevonden dat wordt een waarschuwing weergegeven. Klik op **indeling** tooformat Hallo station met de Hallo partitie-instellingen. Klik op **schrijven wijzigen toodisk** tooapply Hallo partitie wijzigingen.
4. Selecteer **installeren opstartlaadprogramma** > **volgende** tooinstall Hallo opstartlaadprogramma op Hallo hoofdmap partitie.
5. Wanneer de installatie voltooid is klikt u op **opnieuw opstarten**.

#### <a name="retrieve-hello-scsi-ids"></a>Hallo SCSI-id's ophalen
1. Hallo SCSI-id's voor elke harde SCSI-schijf in Hallo VM na de installatie worden opgehaald. toodo dit Hallo managementserver afsluiten VM, Hallo VM eigenschappen in VMware met de rechtermuisknop op Hallo VM vermelding > **instellingen bewerken** > **opties**.
2. Selecteer **Geavanceerd** > **algemene** en klik op **configuratieparameters**. Deze optie niet de-active wanneer Hallo machine wordt uitgevoerd. toomake it active Hallo machine moet worden afgesloten.
3. Als hello rij **schijf. EnableUUID** bestaat controleren Hallo-waarde is ingesteld, te**True** (hoofdlettergevoelig). U kunt als deze al annuleren en test Hallo SCSI-opdracht in een gastbesturingssysteem nadat deze opnieuw wordt opgestart.
4. Als het Hallo-rij niet bestaande Klik **rij toevoegen** – en voeg deze toe met de Hallo **True** waarde. Gebruik geen dubbele aanhalingstekens.

#### <a name="install-additional-packages"></a>Extra pakketten installeren
U moet toodownload en een aantal extra pakketten installeren.

1. Zorg ervoor dat de hoofddoelserver Hallo verbonden toohello internet.
2. Voer deze opdracht toodownload en 15 pakketten installeren vanuit Hallo CentOS opslagplaats: **# yum – y xfsprogs perl lsscsi rsync wget kexec-hulpprogramma's installeren**.
3. Als u wilt beveiligen van Hallo bronmachines worden uitgevoerd Linux dat Reiser XFS bestandssysteem voor Hallo hoofdmap of opstarten van apparaat, moet u downloaden en installeren van extra pakketten als volgt:

   * # <a name="cd-usrlocal"></a>cd /usr/local
   * # <a name="wget-httpelrepoorglinuxelrepoel6x8664rpmskmod-reiserfs-00-1el6elrepox8664rpmhttpelrepoorglinuxelrepoel6x8664rpmskmod-reiserfs-00-1el6elrepox8664rpm"></a>wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm)
   * # <a name="wget-httpelrepoorglinuxelrepoel6x8664rpmsreiserfs-utils-3621-1el6elrepox8664rpmhttpelrepoorglinuxelrepoel6x8664rpmsreiserfs-utils-3621-1el6elrepox8664rpm"></a>wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm)
   * # <a name="rpm-ivh-kmod-reiserfs-00-1el6elrepox8664rpm-reiserfs-utils-3621-1el6elrepox8664rpm"></a>reiserfs in de rpm – ivh-kmod reiserfs-0,0 1.el6.elrepo.x86_64.rpm-utils-3.6.21-1.el6.elrepo.x86_64.rpm
   * # <a name="wget-httpmirrorcentosorgcentos66osx8664packagesxfsprogs-311-16el6x8665rpmhttpmirrorcentosorgcentos66osx8664packagesxfsprogs-311-16el6x8665rpm"></a>wget [http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm](http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm)
   * # <a name="rpm-ivh-xfsprogs-311-16el6x8664rpm"></a>– ivh xfsprogs-3.1.1 rpm-16.el6.x86_64.rpm

#### <a name="apply-custom-changes"></a>Aangepaste wijzigingen toepassen
Voer Hallo tooapply aangepaste wijzigingen te volgen nadat u volledige Hallo na de installatie stappen en geïnstalleerde hello-pakketten hebt:

1. Kopieer Hallo RHEL 6 64 Unified Agent binaire toohello VM. Voer deze opdracht toountar Hallo binaire: **– zxvf tar<file name>**
2. Deze opdracht toogive uitvoeringsmachtigingen: **# type chmod 755./ApplyCustomChanges.sh**
3. Hallo-script uitvoeren: **#./ApplyCustomChanges.sh**. U moet slechts eenmaal Hallo-script uitvoeren. Hallo-server opnieuw opstarten nadat Hallo script wordt uitgevoerd.

## <a name="run-hello-failback"></a>Hallo failback uitvoeren
### <a name="reprotect-hello-azure-vms"></a>Beveiligt hello Azure Virtual machines
1. In de Site Recovery-portal Hallo > **Machines** tabblad select Hallo VM die storing opgetreden en klik op **opnieuw beveiligen**.
2. In **Hoofddoelserver** en **processerver** Hallo lokale hoofddoelserver en hello Azure VM processerver selecteren.
3. U hebt geconfigureerd voor het verbinden van toohello VM Hallo-account selecteren.
4. Hallo failback versie van de beveiligingsgroep Hallo selecteren. Bijvoorbeeld als Hallo VM is beveiligd in PG1, dan moet u tooselect PG1_Failback.
5. Als u toorecover tooan alternatieve locatie wilt, schakelt u Hallo bewaarstation en geconfigureerd voor de hoofddoelserver Hallo-gegevensarchief. Als u een back-toohello lokale site Hallo virtuele VMware-machines in Hallo failback beveiligingsplan failback Hallo gebruikt hetzelfde gegevensarchief als Hallo hoofddoelserver. Als u wilt dat toorecover Hallo replica virtuele machine van Azure toohello dezelfde lokale VM vervolgens Hallo lokale VM moet al worden in Hallo hetzelfde gegevensarchief als Hallo master doelserver. Als er geen VM on-premises wordt een nieuw gemaakt tijdens de beveiligingspoging.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/failback1.png)
6. Nadat u op **OK** toobegin waarvoor een taak begint tooreplicate Hallo VM van Azure toohello lokale site. U kunt Hallo voortgang volgen op Hallo **taken** tabblad.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/failback2.png)

### <a name="run-a-failover-toohello-on-premises-site"></a>Voer een failover toohello on-premises site
Na het beveiligingspoging Hallo VM verplaatste toohello failback versie van de beveiligingsgroep en toohello herstelplan die u voor Hallo failover tooAzure, gebruikt indien aanwezig, wordt automatisch toegevoegd.

1. In Hallo **herstelplannen** pagina Selecteer Hallo-herstelplan met Hallo failback groep en klik op **Failover** > **niet-geplande Failover**.
2. In **bevestigen Failover** controleren Hallo failoverrichting (tooAzure) en selecteer Hallo herstelpunt gewenste toouse voor Hallo failover (laatste). Als u ingeschakeld **Multi-VM** wanneer u replicatie eigenschappen geconfigureerd kunt u de meest recente app toohello of crashconsistent herstelpunt herstellen. Klik op Hallo vinkje toostart Hallo failover.
3. Tijdens de failover van Site Recovery hello Azure Virtual machines afgesloten. Nadat u hebt gecontroleerd dat failback is voltooid zoals verwacht u kunt kunt u controleren dat hello die Azure VM's hebt afgesloten zoals verwacht.

### <a name="reprotect-hello--on-premises-site"></a>Beveiligt Hallo lokale site
Nadat de failback is voltooid wordt uw gegevens worden terug op Hallo on-premises-site, maar won't worden beveiligd. de replicerende tooAzure toostart opnieuw Hallo te volgen:

1. In de Site Recovery-portal Hallo > **Machines** Selecteer Hallo-virtuele machines die zijn mislukt terug en klik op tabblad **opnieuw beveiligen**.
2. Nadat u hebt gecontroleerd dat tooAzure replicatie werkt zoals verwacht, in Azure kunt u verwijderen hello Azure Virtual machines (momenteel niet uitgevoerd) die zijn niet terug.

### <a name="common-issues-in-failback"></a>Veelvoorkomende problemen in de failback
1. Als u virtuele machines beveiligt en alleen-lezen vCenter gebruikersdetectie uitvoert, het is gelukt en failover werkt. Bij Hallo beveiligt, zal mislukken omdat Hallo datastores kan niet worden gedetecteerd. Als een symptoom worden er geen Hallo datastores weergegeven tijdens het opnieuw te beveiligen. tooresolve, kunt u Hallo vCenter referentie bijwerken met de juiste account met machtigingen en Hallo taak opnieuw. [Meer informatie](site-recovery-vmware-to-azure-classic.md)
2. Wanneer u een Linux-VM failback en voer het on-premises, ziet u dat Hallo Network Manager-pakket wordt verwijderd van het Hallo-machine. Dit is omdat wanneer Hallo VM is hersteld in Azure, Hallo netwerkbeheerder pakket wordt verwijderd.
3. Wanneer een virtuele machine is geconfigureerd met statische IP-adres en de failover wordt uitgevoerd tooAzure, wordt Hallo IP-adres verkregen via DHCP. Wanneer u een back-tooOn-premises failover, blijft Hallo VM toouse DHCP tooacquire Hallo IP-adres. U moet toomanually aanmelding naar Hallo-machine en set Hallo IP-adres, indien nodig een back-tooStatic adres maken.
4. Als u van ESXi 5.5 gratis versie of editie free 6 vSphere-Hypervisor gebruikmaakt, failover zou slagen, maar failback niet slaagt. U gaat ned tooupgrade tooeither Evaluatielicentie tooenable failback.

## <a name="failing-back-with-expressroute"></a>Beschadigde back met ExpressRoute
U kunt niet terug via een VPN-verbinding of Azure ExpressRoute. Als u wilt dat toouse ExpressRoute Opmerking Hallo volgende:

* ExpressRoute moet worden ingesteld op Hallo virtuele Azure-netwerk toowhich bron machines mislukken via en in die virtuele Azure-machines zich bevinden nadat Hallo failover plaatsvindt.
* Gegevens zijn gerepliceerde tooan Azure storage-account op een openbaar eindpunt. U moet een openbare peering in ExpressRoute met Hallo doel-Datacenter voor Site Recovery replicatie toouse ExpressRoute instellen.
