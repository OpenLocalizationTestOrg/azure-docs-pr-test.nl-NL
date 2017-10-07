---
title: aaaFail back virtuele VMware-machines van Azure in de klassieke verouderde portal Hallo | Microsoft Docs
description: Dit artikel wordt beschreven hoe toofail back een VMware-virtuele machine die is gerepliceerd tooAzure met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: a63524bf-990c-42ee-8554-e017e6e67e68
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 5ef66b366dcdc43f3bc171e0ed1532216cc2ab89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-from-azure-toovmware-with-azure-site-recovery-legacy"></a>Mislukken back virtuele VMware-machines en fysieke servers uit Azure tooVMware met Azure Site Recovery (verouderd)
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-failback-azure-to-vmware.md)
> * [Klassieke Azure Portal](site-recovery-failback-azure-to-vmware-classic.md)
> * [Klassieke Azure-Portal (verouderd)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

Dit artikel wordt beschreven hoe toofail back VMware virtuele machines en fysieke Windows of Linux-servers van Azure tooyour lokale site nadat u hebt gerepliceerd van uw on-premises met behulp van tooAzure site [Azure Site Recovery?](site-recovery-overview.md).

Dit artikel wordt een oude configuratie beschreven en mag niet worden gebruikt voor nieuwe kluizen.

## <a name="architecture"></a>Architectuur
Dit diagram vertegenwoordigt Hallo failover en failback scenario. Hallo blauw regels zijn Hallo-verbindingen gebruikt tijdens de failover. Hallo rode regels zijn Hallo-verbindingen gebruikt tijdens de failback. Hallo lijnen met pijlen gaan over Hallo internet.

![](./media/site-recovery-failback-azure-to-vmware/vconports.png)

## <a name="before-you-start"></a>Voordat u begint
* U moet failover uitgevoerd voor uw VMware-machines of fysieke servers en moeten ze worden uitgevoerd in Azure.
* Houd er rekening mee dat u alleen back virtuele VMware-machines en fysieke Windows of Linux-servers van Azure tooVMware virtuele machines in Hallo lokale primaire site mislukken kunt.  Als u bent niet opnieuw een fysieke computer, failover tooAzure converteren deze tooan virtuele machine van Azure en failback tooVMware converteren deze tooa VMware VM.

Hier ziet u hoe u failback ingesteld:

1. **Failback onderdelen instellen**: U moet tooset vContinuum-server on-premises en wijs deze toohello configuratieserver VM in Azure. U hebt ook een processerver instellen als een virtuele machine van Azure toosend gegevens back toohello lokale hoofddoelserver. U registreren Hallo processerver met de configuratieserver Hallo die Hallo failover worden verwerkt. U installeert een on-premises hoofddoelserver-server. Als u een Windows-hoofddoelserver nodig het stellen automatisch wanneer u vContinuum installeert. Als u Linux nodig moet u tooset het handmatig op een afzonderlijke server.
2. **Inschakelen van beveiliging en failback**: nadat u Hallo onderdelen hebt ingesteld, in de vContinuum moet u tooenable beveiliging voor failover is uitgevoerd op Azure VM's. U hebt een gereedheidscontrole op Hallo VM's uitgevoerd en een failover van Azure tooyour lokale site. Nadat de failback is voltooid beveiligt lokale machines zodat deze beginnen tooAzure repliceren.

## <a name="step-1-install-vcontinuum-on-premises"></a>Stap 1: VContinuum on-premises installeert
U moet een vContinuum-server on-premises tooinstall en wijst u toohello configuratieserver.

1. [VContinuum downloaden](http://go.microsoft.com/fwlink/?linkid=526305).
2. Download Hallo [vContinuum update](http://go.microsoft.com/fwlink/?LinkID=533813) versie.
3. Installeer de nieuwste versie van de Hallo van vContinuum. Op Hallo **Welkom** pagina op **volgende**.
    ![](./media/site-recovery-failback-azure-to-vmware/image2.png)
4. Geef op Hallo eerste pagina van wizard Hallo Hallo CX-server IP-adres en poort Hallo CX-server. Selecteer **gebruik van HTTPS**.

   ![](./media/site-recovery-failback-azure-to-vmware/image3.png)
5. Hallo configuratieserver IP-adres vinden op Hallo **Dashboard** tabblad van de configuratieserver Hallo virtuele machine in Azure.
   ![](./media/site-recovery-failback-azure-to-vmware/image4.png)
6. Openbare poort op Hallo Hallo configuratieserver HTTPS vinden **eindpunten** tabblad van de configuratieserver Hallo virtuele machine in Azure.

   ![](./media/site-recovery-failback-azure-to-vmware/image5.png)
7. Op Hallo **CS wachtwoordzin Details** pagina Hallo wachtwoordzin die u hebt genoteerd af bij de registratie van de configuratieserver Hallo opgeven. Als je het inchecken **C:\\Program Files (x86)\\InMage systemen\\persoonlijke\\connection.passphrase** op Hallo configuratieserver VM.

    ![](./media/site-recovery-failback-azure-to-vmware/image6.png)
8. In Hallo **doellocatie Selecteer** pagina opgeven waar tooinstall hello vContinuum-server en klik op **installeren**.

   ![](./media/site-recovery-failback-azure-to-vmware/image7.png)
9. Nadat de installatie is voltooid, kunt u vContinuum starten.
    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)

## <a name="step-2-install-a-process-server-in-azure"></a>Stap 2: Installeer een processerver in Azure
U moet tooinstall processerver in Azure zodat Hallo virtuele machines in Azure Hallo gegevens back tooan lokale hoofddoelserver kunnen verzenden.

1. Op Hallo **configuratieservers** pagina in Azure, selecteer tooadd nieuwe processerver.

   ![](./media/site-recovery-failback-azure-to-vmware/image9.png)
2. Geef de naam van een proces-server en een naam en het wachtwoord tooconnect toohello virtuele machine als beheerder. Selecteer Hallo configuratie server toowhich gewenste tooregister Hallo processerver. Dit Hallo moet dezelfde server u tooprotect en failover van uw virtuele machines.
3. Geef hello Azure netwerk in welke Hallo processerver moet worden geïmplementeerd. Deze moet dezelfde Hallo netwerk als Hallo configuratieserver. Geef een uniek IP-adres geselecteerd subnet en begint met implementeren.

   ![](./media/site-recovery-failback-azure-to-vmware/image10.png)
4. Een taak wordt geactiveerd toodeploy Hallo processerver.

   ![](./media/site-recovery-failback-azure-to-vmware/image11.png)
5. Nadat de processerver Hallo is geïmplementeerd in Azure kunt u zich aanmelden bij Hallo-server met behulp van Hallo-referenties die u hebt opgegeven. Hallo processerver registreren in Hallo dezelfde manier als u Hallo geregistreerd op lokale processerver.

   ![](./media/site-recovery-failback-azure-to-vmware/image12.png)

> [!NOTE]
> Hallo-servers die zijn geregistreerd tijdens de failback is niet zichtbaar onder VM-eigenschappen in Site Recovery. Ze zijn alleen zichtbaar onder Hallo **Servers** tabblad van Hallo configuratie server toowhich ze zijn geregistreerd. Duurt ongeveer 10-15 minuten totdat ze proces Hallo server op Hallo tabblad wordt weergegeven.
>
>

## <a name="step-3-install-a-master-target-server-on-premises"></a>Stap 3: Installeer een hoofddoelserver lokale
Afhankelijk van uw besturingssysteem bron voor virtuele machines, moet u een Linux tooinstall of een Windows-hoofddoelserver on-premises.

### <a name="deploy-a-windows-master-target-server"></a>Een Windows-hoofddoelserver implementeren
Een Windows-hoofddoel is al gebundeld met de vContinuum-installatie. Wanneer u Hallo vContinuum installeert, een hoofdserver ook wordt geïmplementeerd op Hallo dezelfde machine en de configuratieserver geregistreerde toohello.

1. toobegin-implementatie, maak een lege machine lokale op Hallo ESX-host waarop u wilt dat toorecover Hallo virtuele machines van Azure.
2. Zorg ervoor dat er ten minste twee schijven toohello VM gekoppeld – een wordt gebruikt voor het besturingssysteem Hallo en Hallo andere wordt gebruikt voor het bewaarstation Hallo.
3. Hallo-besturingssysteem installeren.
4. Hallo vContinuum op Hallo-server installeren. Deze installatie van de hoofddoelserver Hallo ook is voltooid.

### <a name="deploy-a-linux-master-target-server"></a>Linux-hoofddoelserver implementeren
1. toobegin-implementatie, maak een lege machine lokale op Hallo ESX-host waarop u wilt dat toorecover Hallo virtuele machines van Azure.
2. Zorg ervoor dat er ten minste twee schijven toohello VM gekoppeld – een wordt gebruikt voor het besturingssysteem Hallo en Hallo andere wordt gebruikt voor het bewaarstation Hallo.
3. Hallo Linux-besturingssysteem installeren. Linux-hoofddoel systeem Hallo moet LVM niet gebruiken voor basis- of bewaren opslagruimten. Een hoofddoelserver is Linux tooavoid LVM partities/schijven detectie standaard geconfigureerd.
4. Partities die u kunt maken:

   ![](./media/site-recovery-failback-azure-to-vmware/image13.png)
5. Hallo onderstaande stappen voor na de installatie uitvoeren voordat u de installatie van Hallo hoofddoel.

#### <a name="post-os-installation-steps"></a>Installatiestappen voor post OS
tooget hello SCSI-id's voor elke harde SCSI-schijf in een virtuele machine met Linux inschakelen Hallo parameter '-schijf. EnableUUID = TRUE ' als volgt:

1. De virtuele machine afgesloten.
2. Met de rechtermuisknop op Hallo VM in Hallo links Configuratiescherm > **instellingen bewerken**.
3. Klik op Hallo **opties** tabblad. Selecteer **Geavanceerd\>algemene** > **configuratieparameters**. Hallo **configuratieparameters** optie is alleen beschikbaar wanneer het Hallo-machine is afgesloten.

    ![](./media/site-recovery-failback-azure-to-vmware/image14.png)
4. Controleert of een rij met **schijf. EnableUUID** bestaat. Als deze te is ingesteld en**False** te ingesteld**True** (niet hoofdlettergevoelig). Als zich bevindt en tootrue instellen, klikt u op **annuleren** en testen Hallo SCSI-opdracht in het gastbesturingssysteem Hallo nadat deze opgestart. Als bestaat niet Klik **rij toevoegen**.
5. Schijf toevoegen. EnableUUID in Hallo **naam** kolom. Stel de waarde waar. Voeg niet Hallo hierboven waarden samen met dubbele aanhalingstekens.

    ![](./media/site-recovery-failback-azure-to-vmware/image15.png)

#### <a name="download-and-install-hello-additional-packages"></a>Aanvullende hello-pakketten downloaden en installeren
Opmerking: Zorg ervoor dat system Hallo verbinding heeft met internet voordat het downloaden en installeren van extra hello-pakketten.

\#YUM -y xfsprogs perl lsscsi rsync wget kexec-hulpprogramma's installeren

Met deze opdracht deze 15 pakketten uit de opslagplaats CentOS 6.6 downloadt en installeert ze:

BC-1.06.95-1.el6.x86\_64. rpm

busybox-1.15.1-20.el6.x86\_64. rpm

elfutils bibliotheken-0.158 3.2.el6.x86\_64. rpm

kexec-hulpprogramma's-2.0.0-280.el6.x86\_64. rpm

lsscsi-0.23-2.el6.x86\_64. rpm

lzo-2.03-3.1.el6\_5.1.x86\_64. rpm

Perl-5.10.1-136.el6\_6.1.x86\_64. rpm

Perl-Module-Pluggable-3.90-136.el6\_6.1.x86\_64. rpm

Perl-schil-Hiermee heft-trilling 1,04-136.el6\_6.1.x86\_64. rpm

Perl-schil-eenvoudige-3.13-136.el6\_6.1.x86\_64. rpm

Perl, bibliotheken, 5.10.1, 136.el6\_6.1.x86\_64. rpm

Perl-versie-0,77-136.el6\_6.1.x86\_64. rpm

rsync-3.0.6-12.el6.x86\_64. rpm

treffende op 1.1.0 1.el6.x86\_64. rpm

wget-1.12-5.el6\_6.1.x86\_64. rpm

Als Hallo bronmachine Reiser of XFS bestandssysteem voor Hallo basis- of -apparaat gebruikt, moeten vervolgens volgende pakketten worden gedownload en geïnstalleerd op Linux-hoofddoel voorafgaande tooprotection.

\#cd /usr/local

\#wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm>

\#wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm>

\#rpm - ivh kmod-reiserfs-0,0-1.el6.elrepo.x86\_64. rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86\_64. rpm

\#wget <http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_64.rpm>

\#rpm - ivh xfsprogs-3.1.1-16.el6.x86\_64. rpm

#### <a name="apply-custom-configuration-changes"></a>Aangepaste configuratiewijzigingen toepassen
Zorg ervoor dat u hebt voltooid, wordt de vorige sectie hello, en vervolgens als volgt te werk voordat deze wijzigingen worden toegepast:

1. Kopieer Hallo RHEL 6 64 Unified Agent binaire toohello OS een nieuw gemaakt.
2. Voer deze opdracht toountar Hallo binaire: **tar - zxvf \<bestandsnaam\>**
3. Deze opdracht toogive uitvoeringsmachtigingen: \# **type chmod 755./ApplyCustomChanges.sh**
4. Hallo-script uitvoeren:  **\# ./ApplyCustomChanges.sh**. Hallo script slechts eenmaal op Hallo server uitgevoerd. Hallo-server opnieuw opstarten nadat het Hallo-script wordt uitgevoerd.

### <a name="install-hello-linux-server"></a>Hallo Linux-server installeren
1. [Download](http://go.microsoft.com/fwlink/?LinkID=529757) Hallo-installatiebestand.
2. Kopieer Hallo bestand toohello Linux-hoofddoel virtuele machine met een hulpprogramma van de client sftp van uw keuze. Ook kunt u zich aanmeldt bij Hallo Linux hoofddoel virtuele machine en wget toodownload Hallo-installatiepakket uit de onderstaande koppeling gebruiken
3. Zich aanmeldt bij Hallo Linux hoofddoel server virtuele machine met een ssh-client van uw keuze
4. Als u bent verbonden toohello Azure netwerk waarop u uw Linux-hoofddoel-server via een VPN-verbinding geïmplementeerd en vervolgens het interne IP-adres gebruiken voor Hallo-server die u in de virtuele machine vinden kunt **Dashboard** tabblad en -poort 22 tooconnect toohello Linux master doelserver met behulp van Secure Shell.
5. Als u verbinding maakt toohello Linux hoofddoelserver via een openbare internetverbinding Hallo Linux hoofddoelserver de openbare virtuele IP-adres gebruiken (van Hallo virtuele machines **Dashboard** tabblad) en Hallo openbaar eindpunt gemaakt voor ssh toologin toohello Linux servder.
6. Hallo-bestanden extraheren uit Hallo gzipped Linux installatieprogramma tar-archief hoofddoel Server door te voeren: *' – xvzf Microsoft ASR tar\_UA\_8.2.0.0\_RHEL6 64\ '* uit Hallo directory die Hallo installer-bestand bevat.

    ![](./media/site-recovery-failback-azure-to-vmware/image16.png)
7. Als u uitgepakte Hallo installer-bestanden tooa andere directory wijzigt zijn toohello toowhich Hallo Mapinhoud van Hallo tar-archief geëxtraheerd. Vanaf dit pad worden uitgevoerd ' sudo. / install.sh '.

    ![](./media/site-recovery-failback-azure-to-vmware/image17.png)
8. Wanneer de vraag toochoose een primaire rol selecteert **2 (hoofddoel)**. Laat Hallo andere interactieve installatie-opties op hun standaardwaarden.
9. Wachten op installatie toocontinue en Hallo Host Config Interface tooappear. Hallo Host configuratieprogramma voor Hallo Linux master sarget Server is een opdrachtregelprogramma. Niet vergroten of verkleinen Hallo ssh client hulpprogramma venster. Gebruik Hallo pijl sleutels tooselect hello **Global** optie en druk op ENTER op het toetsenbord.

    ![](./media/site-recovery-failback-azure-to-vmware/image18.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image19.png)
10. In het veld Hallo **IP** Voer Hallo interne IP-adres van de configuratieserver hello (u kunt deze vinden in Hallo **Dashboard** tabblad van de configuratieserver Hallo VM) en druk op ENTER. In **poort** Voer **22** en druk op ENTER.
11. Laat **gebruik HTTPS** als **Ja**, en druk op ENTER.
12. Voer Hallo wachtwoordzin die is gegenereerd op Hallo configuratieserver. Als u een PUTTY client van een virtuele machine van Windows machine toossh toohello Linux kunt u Shift + Insert toopaste Hallo inhoud van Hallo Klembord. Hallo wachtwoordzin toohello lokale Klembord met Ctrl-C kopiëren en gebruiken van Shift + Insert toopaste deze. Druk op ENTER.
13. Hallo pijl naar rechts sleutel toonavigate tooquit en druk op ENTER. Wachten op installatie toocomplete.

    ![](./media/site-recovery-failback-azure-to-vmware/image20.png)

Als u kan voor een bepaalde reden tooregister uw Linux-server toohello configuratie hoofddoelserver kunt u doen dit door het uitvoeren van de host configuratieprogramma in /usr/local/ASR/Vx/bin/hostconfigcli (moet u eerst tooset toegang machtigingen toothis map type chmod als supergebruiker uitvoert).

#### <a name="validate-master-target-registration"></a>Hoofddoel registratie valideert
U kunt valideren die Hallo hoofddoelserver is geregistreerd toohello configuratieserver in Azure Site Recovery-kluis > **configuratieserver** > **Serverdetails**.

> [!NOTE]
> Nadat Hallo hoofddoelserver, registreren als er fouten in de configuratie die virtuele machine Hallo mogelijk is deze verwijderd uit Azure of die eindpunten niet juist zijn geconfigureerd, reden hiervoor is dat hoewel hello configuratie van het hoofddoel wordt gedetecteerd door hello Azure dndpoints wanneer Hallo hoofddoel is geïmplementeerd in Azure, dit geldt niet voor een lokale hoofddoel server on-premises. Dit geen invloed op de failback en kunt u deze fouten negeren.
>
>

## <a name="step-4-protect-hello-virtual-machines-toohello-on-premises-site"></a>Stap 4: Beveilig Hallo virtuele machines toohello lokale site
U moet tooprotect VMs toohello lokale site voordat u een failback uit.

### <a name="before-you-begin"></a>Voordat u begint
Wanneer een virtuele machine via tooAzure is mislukt, wordt een extra tijdelijke station voor een bestand met pagina toegevoegd. Dit is een extra station dat doorgaans niet vereist is door uw failover VM omdat deze mogelijk al een station dat speciaal ontworpen is voor het wisselbestand. Voordat u omgekeerde beveiliging van Hallo virtuele machines, moet u ervoor zorgen dat dit station offline is gehaald, zodat deze wordt niet beveiligd. Dit als volgt:

1. Computerbeheer openen en selecteer opslagbeheer zodat geeft het Hallo schijven online en gekoppelde toohello machine.
2. Selecteer Hallo tijdelijke schijf gekoppelde toohello machine en kies toobring offline.

### <a name="protect-hello-vms"></a>Hallo VM's beveiligen
1. Schakel in hello Azure-portal, Hallo statussen van Hallo virtuele machine tooensure die overgenomen heeft.

    ![](./media/site-recovery-failback-azure-to-vmware/image21.png)
2. VContinuum op uw computer starten.

    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)
3. Klik op **nieuwe bescherming** en Hallo bewerking systeemtype, selecteer de
4. In nieuw venster Hallo dat openen, selecteer Hallo **type besturingssysteem** > **Details ophalen** voor Hallo virtuele machines die u wilt toofail terug. In **details van de primaire server**, het identificeren en selecteer de virtuele machines die u wilt dat tooprotect Hallo. Virtuele machines worden vermeld in de hostnaam van Hallo vCenter die ze op voordat failover wordt uitgevoerd waren.
5. Wanneer u een virtuele machine tooprotect selecteert (en deze is al een failover uitgevoerd tooAzure) biedt een pop-upvenster twee vermeldingen voor Hallo virtuele machine. Dit is omdat Hallo configuratieserver twee exemplaren van Hallo virtuele machines die zijn geregistreerd tooit detecteert. U moet tooremove Hallo-vermelding voor Hallo on-premises VM zodat u kunt beveiligen Hallo juist VM. tooidentify hello Azure VM herstelmogelijkheid hier, kunt u zich aanmelden bij hello Azure VM- en ga tooC:\Program bestanden (x86) \Microsoft Azure Site Recovery\Application Data\etc. In Hallo bestand drscout.conf, geïdentificeerd Hallo host-ID. Laat in Hallo vContinuum dialoogvenster Hallo vermelding waarvoor u Hallo host-ID op Hallo VM gevonden. Alle overige items verwijderen. Hallo tooselect corrigeren VM raadpleegt u tooits IP-adres. Hallo IP-adresbereik lokale zal worden Hallo lokale VM.

   ![](./media/site-recovery-failback-azure-to-vmware/image22.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image23.png)
6. Hallo vCenter server Hallo virtuele machine te stoppen. U kunt ook Hallo VM's op de lokale verwijderen.
7. Vervolgens geeft Hallo lokale MT server toowhich gewenste tooprotect Hallo virtuele machines. toodo, toohello vCenter server toowhich u toofail terug wilt verbinden.

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
8. Selecteer Hallo hoofddoelserver op basis van Hallo host toowhich gewenste toorecover Hallo VM.

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
9. Geef Hallo replicatieoptie voor elk van Hallo virtuele machines. toodo dit moet u tooselect Hallo herstel side datastore toowhich Hallo virtuele machines worden hersteld. Hallo-tabel ziet u Hallo verschillende opties die u nodig hebt tooprovide voor elke virtuele machine.

    ![](./media/site-recovery-failback-azure-to-vmware/image25.png)

   | **Optie** | **Optie aanbevolen waarde** |
   | --- | --- |
   |  Processerver IP-adres |Selecteer de processerver Hallo geïmplementeerd in Azure |
   |  Bewaartermijn grootte in MB | |
   |  Bewaartermijn waarde |1 |
   |  Dagen/uur |Dagen |
   |  Consistentie interval |1 |
   |  Selecteer doel gegevensopslag |Hallo datastore beschikbaar op Hallo herstelsite. Hallo-gegevensarchief moet voldoende ruimte en beschikbaar toohello ESX-host waarop toorestore Hallo virtuele machine. |
10. Hallo-eigenschappen die virtuele machine Hallo na failover tooon-premises site behaalt configureren. Hallo-eigenschappen worden samengevat in de volgende tabel Hallo.

    ![](./media/site-recovery-failback-azure-to-vmware/image26.png)

    | **Eigenschap** | **Details** |
    | --- | --- |
    | Netwerkconfiguratie |Voor elke netwerkadapter gedetecteerd, te selecteren en op **wijziging** tooconfigure Hallo failback IP-adres voor Hallo virtuele machine. |
    | Hardwareconfiguratie |Hallo CPU en geheugen voor Hallo VM Hallo opgeven. Instellingen kunnen worden toegepast tooall Hallo virtuele machines die u probeert tooprotect. tooidentify Hallo juiste waarden voor Hallo CPU en geheugen, kunt u de grootte van de rol IAAS VM's toohello verwijzen en Hallo aantal kernen en het geheugen toegewezen. |
    | Weergavenaam |U kunt na failback tooon lokaal Hallo virtuele machines wijzigen zullen zien in Hallo vCenter inventaris. de standaardnaam Hallo is Hallo computerhostnaam op de virtuele machine. tooidentify hello VM-naam, kunt u toohello VM lijst in de beveiligingsgroep Hallo verwijzen. |
    | NAT-configuratie |Hieronder in detail besproken |

    ![](./media/site-recovery-failback-azure-to-vmware/image27.png)

#### <a name="configure-nat-settings"></a>NAT-instellingen configureren
1. tooenable beveiliging van Hallo virtuele machines, twee communicatiekanalen moeten toobe tot stand gebracht. eerste Hallo-kanaal is tussen Hallo virtuele machine en de processerver Hallo. Dit kanaal Hallo gegevens van Hallo VM verzamelt en verzendt deze toohello processerver welke vervolgens verzendt Hallo gegevens toohello hoofddoelserver. Als processerver Hallo en Hallo virtuele machine toobe beveiligd op Hallo zijn hetzelfde virtuele Azure-netwerk en u hoeft niet toouse NAT-instellingen. Anders NAT-instellingen opgeven. Openbaar IP-adres van de processerver Hallo Hallo weergeven in Azure.

    ![](./media/site-recovery-failback-azure-to-vmware/image28.png)
2. Hallo tweede kanaal is tussen de processerver Hallo en Hallo hoofddoelserver. Hallo optie toouse NAT of niet is afhankelijk van of u met behulp van een op basis van VPN-verbinding of communiceren via Hallo internet. Selecteer de NAt niet als u VPN, maar alleen als u een internetverbinding.

    ![](./media/site-recovery-failback-azure-to-vmware/image29.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image30.png)
3. Als u dit nog niet hebt Hallo on-premises virtuele machines als opgegeven verwijderd en als Hallo datastore u mislukken back-toostill Hallo oude VMDK bevat, moet u tooensure dat failback Hallo VM wordt gemaakt op een nieuwe locatie. toodo deze Selecteer Hallo **Geavanceerd** instellingen en geef een alternatieve map toorestore tooin **naam mapinstellingen**. Laat Hallo andere opties met de standaardinstellingen. Hallo map instellingen tooall Hallo naamservers toepassen.

    ![](./media/site-recovery-failback-azure-to-vmware/image31.png)
4. Een Gereedheidscontrole uitvoeren beveiligd dat Hallo virtuele machines gereed toobe zijn tooensure back tooon-premises.

    ![](./media/site-recovery-failback-azure-to-vmware/image32.png)
5. Wacht totdat deze toocomplete. Als deze voltooid op alle VM's is kunt u een naam voor het Hallo-beveiligingsplan. Klik vervolgens op **beveiligen** toobegin.

    ![](./media/site-recovery-failback-azure-to-vmware/image33.png)
6. U kunt de voortgang in vContinuum controleren.

    ![](./media/site-recovery-failback-azure-to-vmware/image34.png)
7. Na de stap Hallo **activeren beveiliging plannen** is voltooid, kunt u VM-beveiliging in Hallo Site Recovery-portal bewaken.

    ![](./media/site-recovery-failback-azure-to-vmware/image35.png)
8. Hier ziet u de exacte status Hallo op Hallo VM te klikken en de voortgang controleren.

    ![](./media/site-recovery-failback-azure-to-vmware/image36.png)

## <a name="prepare-hello-failback-plan"></a>Hallo failback plan voorbereiden
U kunt een failback plan met vContinuum zodat de toepassing hello mislukte back toohello lokale site op elk gewenst moment kunt voorbereiden. Deze herstelplannen zijn vergelijkbaar toohello herstelplannen in Site Recovery.

1. VContinuum Start en selecteer **plannen beheren** > **herstellen.** U kunt zien van lijst met alle Hallo plannen die gebruikt toofail via virtuele machines zijn. U kunt Hallo dezelfde toorecover plannen.

   ![](./media/site-recovery-failback-azure-to-vmware/image37.png)
2. Selecteer Hallo beveiligingsplan en alle virtuele machines die u wilt dat toorecover erin Hallo. Wanneer u elke virtuele machine kunt u meer informatie, zoals Hallo doel-ESX-server en de bronschijf VM Hallo zien. Klik op **volgende** toobegin Hallo van de Wizard herstellen en selecteer Hallo virtuele machines die u wilt dat toorecover.

    ![](./media/site-recovery-failback-azure-to-vmware/image38.png)
3. U kunt herstellen op basis van meerdere opties maar we raden u **nieuwste Tag** en selecteer **toepassen voor alle virtuele machines** tooensure die het meest recente gegevens van de virtuele machine van Hallo Hallo wordt gebruikt.
4. Voer Hallo **gereedheid controleren.** Dit wordt gecontroleerd of de juiste parameters Hallo geconfigureerde tooenable VM herstel zijn. Klik op **volgende** als alle Hallo controles geslaagd zijn. Als dat niet het Hallo-logboek te controleren en Hallo fouten op te lossen.

    ![](./media/site-recovery-failback-azure-to-vmware/image39.png)
5. In **VM-configuratie** controleren of de herstelinstellingen Hallo correct zijn ingesteld. Als u wilt, kunt u Hallo VM instellingen wijzigen.

   ![](./media/site-recovery-failback-azure-to-vmware/image40.png)
6. Bekijk Hallo lijst met virtuele machines die worden hersteld en de volgorde van een herstelpunt opgeven. Houd er rekening mee dat virtuele machines worden weergegeven met hostnaam Hallo-computer. Mogelijk moeilijk toomap Hallo computer host naam toohello virtuele machine.
   Ga toohello virtuele machines-namen Hallo toomap **Dashboard** in Azure en controle Hallo VM-hostnaam.

    ![](./media/site-recovery-failback-azure-to-vmware/image41.png)
7. Geef de naam van een abonnement en selecteer **later herstellen**. We raden aan toorecover later omdat de initiële beveiliging Hallo mogelijk niet voltooid.
8. Klik op **herstellen** toosave Hallo plan of trigger Hallo herstel als u toorecover uiterlijk en nu hebt geselecteerd. U kunt Hallo herstel status toosee controleren als Hallo plan is opgeslagen.

   ![](./media/site-recovery-failback-azure-to-vmware/image42.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image43.png)

## <a name="recover-virtual-machines"></a>Virtuele machines herstellen
Nadat Hallo plan is gemaakt, kunt u Hallo virtuele machines kunt herstellen. Voordat u dat Hallo virtuele inschakelt voltooid machines synchronisatie. Als de replicatiestatus toont OK Hallo beveiliging is voltooid en Hallo RPO drempelwaarde is voldaan. U kunt controleren of health in Hallo VM-eigenschappen.

![](./media/site-recovery-failback-azure-to-vmware/image44.png)

Uitschakelen hello Azure virtuele machines voordat u Hallo herstel starten. Dit zorgt ervoor dat er is geen split-brain en dat gebruikers alleen toegang hebben tot één exemplaar van de toepassing hello.

1. Start hello planning opgeslagen. Selecteer in de vContinuum **Monitor** Hallo plannen. Hiermee worden alle Hallo plannen die zijn uitgevoerd.

   ![](./media/site-recovery-failback-azure-to-vmware/image45.png)
2. Selecteer Hallo-plan in de **herstel** en klik op **Start**. U kunt herstel bewaken. Nadat de virtuele machines is ingeschakeld op u toothem in vCenter verbinding kunt maken.

   ![](./media/site-recovery-failback-azure-to-vmware/image46.png)

## <a name="protect-tooazure-again-after-failback"></a>TooAzure failback opnieuw beveiligen
Na voltooiing van failback zult waarschijnlijk u tooprotect Hallo virtuele machines opnieuw. Dit als volgt:

1. Controleer dat Hallo virtuele machines op de lokale werkt en of toepassingen bereikbaar zijn.
2. Hallo virtuele machines selecteren in hello Azure Site Recovery-portal en verwijder deze. Selecteer toodisable Hallo beveiliging van Hallo virtuele machines. Dit zorgt ervoor dat de Hallo virtuele machines niet meer worden beveiligd.
3. Verwijder in Azure Hallo failover van virtuele machines in Azure
4. Hallo oude virtuele machine op vSpehere verwijderen. Dit zijn Hallo virtuele machines die u eerder tooAzure failover.
5. Beveiligen in Site Recovery-portal Hallo Hallo VM's die onlangs failover. Nadat ze zijn beveiligd kunt u deze tooa herstelplan toevoegen.

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over](site-recovery-vmware-to-azure-classic.md) repliceren van virtuele VMware-machines en fysieke servers tooAzure met verbeterde Hallo-implementatie.
