---
title: aaaHow tooinstall een Linux-hoofddoel-server voor failover van Azure tooon-premises | Microsoft Docs
description: Voordat een virtuele Linux-machine opnieuw te beveiligen, moet u een Linux-hoofddoelserver. Meer informatie over hoe tooinstall een.
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
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a>Een Linux-hoofddoel-server installeren
Nadat u uw virtuele machines failover, kunt u back-Hallo virtuele machines toohello lokale site kan mislukken. terug toofail, moet u tooreprotect Hallo virtuele machine van Azure toohello lokale site. U moet een lokale hoofddoel tooreceive Hallo verkeer van een server voor dit proces. 

Als de beveiligde virtuele machine een virtuele Windows-computer is, moet u een Windows-hoofddoel. Voor een virtuele Linux-machine moet u een Linux-hoofddoel. Lees Hallo volgende stappen uit toolearn hoe toocreate en installeer een Linux-doel master.

> [!IMPORTANT]
> Vanaf versie van de hoofddoelserver hello 9.10.0, Hallo nieuwste hoofddoelserver kan worden alleen geïnstalleerd op een server Ubuntu 16.04. Nieuwe installaties zijn niet toegestaan voor CentOS6.6 servers. U kunt echter doorgaan tooupgrade uw oude hoofdsleutel doelservers met Hallo 9.10.0 versie.

## <a name="overview"></a>Overzicht
In dit artikel bevat instructies voor hoe tooinstall een Linux-doel master.

Opmerkingen of vragen plaatsen aan Hallo einde van dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Vereisten

* toochoose hello host op welke Hallo hoofddoel van toodeploy, bepalen als Hallo failback toobe tooan bestaande on-premises virtuele machine of tooa nieuwe virtuele machine. 
    * Voor een bestaande virtuele machine hebben host van het hoofddoel Hallo Hallo toegang toohello gegevensarchieven van Hallo virtuele machine.
    * Als Hallo on-premises virtuele machine niet bestaat, wordt op dezelfde als hoofddoel Hallo host Hallo Hallo failback van virtuele machine gemaakt. U kunt een willekeurige host ESXi tooinstall Hallo hoofddoel.
* Hallo hoofddoel moet zich op een netwerk dat met de Hallo processerver en de configuratieserver Hallo communiceren kan.
* Hallo-versie van het hoofddoel Hallo moet gelijk tooor ouder is dan het Hallo-versies van Hallo processerver en de configuratieserver Hallo. Bijvoorbeeld, als Hallo-versie van de configuratieserver Hallo 9.4, kan Hallo-versie van het hoofddoel Hallo worden 9.4 of 9.3 maar niet 9.5.
* Hallo hoofddoel kan alleen worden een virtuele VMware-machine en niet op een fysieke server.

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a>Hallo hoofddoel volgens toohello sizing richtlijnen maken

Maak Hallo hoofddoel in overeenstemming met Hallo sizing richtlijnen te volgen:
- **RAM-geheugen**: 6 GB of meer
- **OS-schijfgrootte**: 100 GB of meer (tooinstall CentOS6.6)
- **Aanvullende schijfgrootte voor bewaarstation**: 1 TB
- **CPU-kernen**: 4 kernen of meer

Hallo volgende ondersteund Ubuntu kernels worden ondersteund.


|Kernel-reeks  |Ondersteuning voor maximaal te |
|---------|---------|
|4.4      |4.4.0-81-Generic         |
|4.8      |4.8.0-56-Generic         |
|4.10     |4.10.0-24-Generic        |


## <a name="deploy-hello-master-target-server"></a>De hoofddoelserver Hallo implementeren

### <a name="install-ubuntu-16042-minimal"></a>Ubuntu 16.04.2 installeren minimale

Hallo Hallo stappen tooinstall Hallo Ubuntu 16.04.2 64-bits-besturingssysteem te volgen in beslag nemen.

**Stap 1:** gaat toohello [downloadkoppeling](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) en kies de dichtstbijzijnde mirror Hallo van waarmee Ubuntu 16.04.2 minimaal 64-bits ISO downloaden.

Houd een Ubuntu 16.04.2 minimaal 64-bits ISO Hallo DVD-station en start Hallo systeem.

**Stap 2:** Selecteer **Engels** als uw voorkeurstaal en selecteer vervolgens **Enter**.

![Een taal selecteren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

**Stap 3:** Selecteer **Ubuntu Server installeren**, en selecteer vervolgens **Enter**.

![Selecteer installeren Ubuntu Server](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

**Stap 4:** Selecteer **Engels** als uw voorkeurstaal en selecteer vervolgens **Enter**.

![Engels als uw voorkeurstaal selecteren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

**Stap 5:** Selecteer optie van Hallo Hallo **tijdzone** optielijst en selecteer vervolgens **Enter**.

![Selecteer de juiste tijdzone Hallo](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

**Stap 6:** Selecteer **Nee** (hello standaardoptie), en selecteer vervolgens **Enter**.


![Hallo toetsenbord configureren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

**Stap 7:** Selecteer **Engels (V.S.)** als Hallo land van oorsprong voor Hallo toetsenbord en selecteert u vervolgens **Enter**.

![VS als Hallo land van oorsprong selecteren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

**Stap 8:** Selecteer **Engels (V.S.)** als Hallo toetsenbordindeling en selecteer vervolgens **Enter**.

![Selecteer Amerikaans Engels als Hallo toetsenbordindeling](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

**Stap 9:** Voer Hallo-hostnaam voor uw server in Hallo **hostnaam** vak en selecteer vervolgens **doorgaan**.

![Voer Hallo-hostnaam voor de server](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

**Stap 10:** toocreate een gebruikersaccount, voer de naam van de gebruiker Hallo en selecteer vervolgens **doorgaan**.

![Een gebruikersaccount maken](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

**Stap 11:** Hallo wachtwoord invoeren voor het nieuwe gebruikersaccount Hallo en selecteer vervolgens **doorgaan**.

![Hallo wachtwoord invoeren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

**Stap 12:** Bevestig het wachtwoord voor de nieuwe gebruiker Hallo Hallo en selecteer vervolgens **doorgaan**.

![Hallo wachtwoorden bevestigen](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

**Stap 13:** Selecteer **Nee** (hello standaardoptie), en selecteer vervolgens **Enter**.

![Gebruikers en wachtwoorden instellen](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

**Step 14:** als Hallo tijdzone die wordt weergegeven correct is, selecteert u **Ja** (hello standaardoptie), en selecteer vervolgens **Enter**.

tooreconfigure uw tijdzone, selecteer **Nee**.

![Hallo klok configureren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

**Stap 15:** Hallo opties voor de methode partitioneren, selecteer **begeleide - volledige schijf gebruiken**, en selecteer vervolgens **Enter**.

![Selecteer optie methode partitioneren Hallo](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

**Stap 16:** Selecteer Hallo geschikte schijf van Hallo **Selecteer schijf toopartition** opties en selecteer vervolgens **Enter**.


![Hallo schijf selecteren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

**Stap 17:** Selecteer **Ja** toowrite Hallo wijzigingen toodisk en selecteer vervolgens **Enter**.

![Hallo wijzigingen toodisk schrijven](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

**Stap 18:** Hallo standaardoptie selecteert, selecteert u **doorgaan**, en selecteer vervolgens **Enter**.

![Selecteer de standaardoptie Hallo](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

**Stap 19:** Selecteer de relevante optie Hallo voor het beheren van upgrades op uw systeem, en selecteer vervolgens **Enter**.

![Selecteer hoe toomanage wordt bijgewerkt](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> Omdat hello Azure Site Recovery hoofddoelserver een specifieke versie van Hallo Ubuntu vereist, moet u op tooensure die Hallo kernel upgrades zijn uitgeschakeld voor Hallo virtuele machine. Als ze zijn ingeschakeld, veroorzaken eventuele upgrades voor reguliere Hallo hoofddoel server toomalfunction. Zorg ervoor dat u selecteert Hallo **geen automatische updates** optie.


**Stap 20:** standaardopties selecteren. Als u openSSH wilt voor SSH-verbinding maken, selecteert u Hallo **OpenSSH server** optie en selecteer vervolgens **doorgaan**.

![Selecteer de software](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

**Stap 21:** Selecteer **Ja**, en selecteer vervolgens **Enter**.

![Doelsessie Hallo WORMGATEN opstartlaadprogramma](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

**Stap 22:** Selecteer Hallo juiste apparaatstuurprogramma voor Hallo boot loader installatie (bij voorkeur **/dev/sda**), en selecteer vervolgens **Enter**.

![Selecteer een apparaat voor opstarten laadprogramma installeren](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

**Stap 23:** Selecteer **doorgaan**, en selecteer vervolgens **Enter** toofinish Hallo-installatie.

![Hallo-installatie voltooien](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

Nadat het Hallo-installatie is voltooid, meld u aan toohello VM met de nieuwe gebruikersgegevens Hallo. (Raadpleeg te**stap 10** voor meer informatie.)

Hallo-stappen die worden beschreven in de volgende screenshot tooset Hallo hoofdmap Hallo gebruikerswachtwoord ondernemen. Meld u vervolgens aan als hoofdgebruiker.

![Hallo hoofdmap gebruiker-wachtwoord instellen](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a>Hallo-machine voor configuratie als een hoofddoelserver voorbereiden
Hallo-machine voor de configuratie vervolgens voorbereiden als een hoofddoelserver.

tooget Hallo-ID voor elke harde SCSI-schijf in een virtuele machine met Linux inschakelen Hallo **schijf. EnableUUID = TRUE** parameter.

tooenable deze parameter, nemen Hallo volgende stappen:

1. De virtuele machine afgesloten.

2. Met de rechtermuisknop op het Hallo-vermelding voor Hallo virtuele machine in het linkerdeelvenster Hallo en selecteer vervolgens **instellingen bewerken**.

3. Selecteer Hallo **opties** tabblad.

4. Selecteer in het linkerdeelvenster Hallo **Geavanceerd** > **algemene**, en selecteer vervolgens Hallo **configuratieparameters** knop op Hallo rechtsonder deel uit van welkomstscherm.

    ![Tabblad Opties](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    Hallo **configuratieparameters** optie is niet beschikbaar wanneer Hallo machine wordt uitgevoerd. toomake op dit tabblad actief, Hallo virtuele machine afgesloten.

5. Zie of een rij met **schijf. EnableUUID** bestaat al.

    - Als Hallo waarde bestaat en is ingesteld te**False**, Hallo waarde te wijzigen**True**. (Hallo waarden zijn niet hoofdlettergevoelig).

    - Als Hallo waarde bestaat en is ingesteld te**True**, selecteer **annuleren**.

    - Als het Hallo-waarde niet bestaat, selecteert u **rij toevoegen**.

    - In de kolom naam Hallo toevoegen **schijf. EnableUUID**, en stel Hallo waarde te**TRUE**.

    ![Controleren of schijf. Er bestaat al een EnableUUID](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a>Kernel-upgrades uitschakelen

Azure Site Recovery-hoofddoelserver vereist een specifieke versie van Hallo Ubuntu, zorg ervoor dat de Hallo kernel upgrades voor Hallo virtuele machine zijn uitgeschakeld.

Als upgrades van de kernel zijn ingeschakeld, veroorzaken eventuele upgrades voor reguliere Hallo hoofddoel server toomalfunction.

#### <a name="download-and-install-additional-packages"></a>Extra pakketten downloaden en installeren

> [!NOTE]
> Zorg ervoor dat u Internet connectiviteit toodownload en extra pakketten installeren. Als u geen verbinding met Internet, moet u toomanually deze RPM-pakketten zoeken en te installeren.

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a>Hallo-installatieprogramma niet ophalen voor setup

Als uw hoofddoel verbinding met Internet heeft, kunt u Hallo stappen toodownload Hallo installatieprogramma te volgen. U kunt anders Hallo installatieprogramma kopiëren vanuit de processerver Hallo en u deze vervolgens installeren.

#### <a name="download-hello-master-target-installation-packages"></a>Hallo hoofddoel installatiepakketten downloaden

[Hallo nieuwste Linux hoofddoel installatie bits downloaden](https://aka.ms/latestlinuxmobsvc).

toodownload deze via Linux, type:

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

Zorg ervoor dat u downloaden en uitpakken van Hallo installer in de basismap. Als u te pakken**/usr/Local**, mislukt de installatie van de Hallo.


#### <a name="access-hello-installer-from-hello-process-server"></a>Toegang Hallo installatieprogramma van de processerver Hallo

1. Op de processerver hello, gaat u te**C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.

2. Hallo vereist installer-bestand kopiëren vanuit de processerver Hallo en sla het bestand als **latestlinuxmobsvc.tar.gz** in de basismap.


### <a name="apply-custom-configuration-changes"></a>Aangepaste configuratiewijzigingen toepassen

aangepaste configuratiewijzigingen tooapply gebruik Hallo stappen te volgen:


1. Hallo na de opdracht toountar Hallo binair worden uitgevoerd.
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Schermopname van Hallo opdracht toorun](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. Voer Hallo opdracht toogive machtiging te volgen.
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. Hallo opdrachtscript toorun Hallo volgende worden uitgevoerd.
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> Hallo script slechts eenmaal op Hallo server uitgevoerd. Hallo server afsluiten. Start opnieuw op Hallo server nadat u een schijf toevoegen zoals beschreven in de volgende sectie Hallo.

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a>Een bewaarperiode schijf toohello Linux hoofddoel virtuele machine toevoegen

Volgende stappen toocreate een bewaarschijf Hallo gebruiken:

1. Een nieuwe schijf van 1 TB toohello Linux hoofddoel virtuele machine koppelen en vervolgens Hallo machine starten.

2. Gebruik Hallo **multipath -lle** opdracht toolearn Hallo multipath-ID van de bewaarschijf Hallo.

    ```
    multipath -ll
    ```
    ![Hallo multipath-ID van de bewaarschijf Hallo](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. Hallo station formatteren, en maak vervolgens een bestandssysteem op Hallo nieuwe schijf.

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Een bestandssysteem maken op Hallo station](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. Nadat u het bestandssysteem Hallo hebt gemaakt, kunt u Hallo bewaren schijf koppelen.
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Hallo-bewaarschijf koppelen](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. Hallo maken **fstab** vermelding toomount hello bewaarstation telkens wanneer Hallo-systeem wordt gestart.
    ```
    vi /etc/fstab
    ```
    Selecteer **invoegen** toobegin Hallo-bestand te bewerken. Maak een nieuwe regel en voeg vervolgens de volgende tekst hello. Hallo schijf multipath-ID op basis van Hallo gemarkeerd multipath-ID van de vorige opdracht Hallo bewerken.

     **/dev/mapper/ <Retention disks multipath id> /mnt/bewaren ext4 rw 0 0**

    Selecteer **Esc**, en typ vervolgens **: wq** (schrijven en afsluiten) tooclose Hallo-editorvenster.

### <a name="install-hello-master-target"></a>Hallo hoofddoel installeren

> [!IMPORTANT]
> Hallo-versie van de hoofddoelserver Hallo moet gelijk tooor ouder is dan het Hallo-versies van Hallo processerver en de configuratieserver Hallo. Als dit probleem niet wordt voldaan, beveiligt is geslaagd, maar mislukt de replicatie.


> [!NOTE]
> Voordat u Hallo hoofddoelserver installeert, controleert u dat Hallo **/etc/hosts** -bestand op Hallo virtuele machine bevat items die zijn toegewezen Hallo lokale hostnaam toohello IP-adressen die gekoppeld aan alle netwerkadapters zijn.

1. Kopieer Hallo wachtwoordzin van **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** op Hallo configuratieserver. Sla het als **passphrase.txt** in Hallo Hallo dezelfde lokale map door te voeren opdracht op te volgen:

    ```
    echo <passphrase> >passphrase.txt
    ```
    Voorbeeld: 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. Houd er rekening mee Hallo configuratieserver IP-adres. U moet deze in de volgende stap Hallo.

3. Hallo na de opdracht tooinstall hello hoofddoelserver worden uitgevoerd en Hallo-server registreren met de configuratieserver Hallo.

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    Voorbeeld: 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    Wacht totdat het Hallo-script is voltooid. Als het hoofddoel Hallo is geregistreerd, hoofddoel Hallo wordt weergegeven op Hallo **Site Recovery-infrastructuur** pagina van het Hallo-portal.


#### <a name="install-hello-master-target-by-using-interactive-installation"></a>Hallo hoofddoel installeren met behulp van interactieve installatie

1. Hallo na de opdracht tooinstall hello hoofddoelserver worden uitgevoerd. Voor de rol van de agent hello, kies **hoofddoel**.

    ```
    ./install
    ```

2. Kies Hallo standaardlocatie voor installatie en selecteer vervolgens **Enter** toocontinue.

    ![Een standaardlocatie voor installatie van het hoofddoel kiezen](./media/site-recovery-how-to-install-linux-master-target/image17.png)

Nadat het Hallo-installatie is voltooid, kunt u de Hallo configuratieserver registreren via de opdrachtregel Hallo.

1. Houd er rekening mee Hallo IP-adres van de configuratieserver Hallo. U moet deze in de volgende stap Hallo.

2. Hallo na de opdracht tooinstall hello hoofddoelserver worden uitgevoerd en Hallo-server registreren met de configuratieserver Hallo.

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    Voorbeeld: 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   Wacht totdat het Hallo-script is voltooid. Als het hoofddoel hello geregistreerd met succes is wordt, hoofddoel Hallo wordt vermeld op Hallo **Site Recovery-infrastructuur** pagina van het Hallo-portal.


### <a name="upgrade-hello-master-target"></a>Hallo hoofddoel upgraden

Hallo-installatieprogramma wordt uitgevoerd. Er wordt automatisch gedetecteerd dat die Hallo-agent is geïnstalleerd op het hoofddoel Hallo. tooupgrade, selecteer **Y**.  Nadat het Hallo-setup is voltooid, controleert u Hallo-versie van het hoofddoel Hallo geïnstalleerd met behulp van de volgende opdracht Hallo.

    ```
    cat /usr/local/.vx_version
    ```

U kunt zien die Hallo **versie** veld kunt Hallo versienummer van het hoofddoel Hallo.

### <a name="install-vmware-tools-on-hello-master-target-server"></a>VMware-hulpprogramma's installeren op de hoofddoelserver Hallo

U moet tooinstall VMware tools op het hoofddoel Hallo zodat het Hallo-gegevensarchieven kan detecteren. Als Hallo-hulpprogramma's zijn niet geïnstalleerd, is niet in de gegevensarchieven Hallo beveiligt welkomstscherm vermeld. Na installatie van Hallo VMware tools moet u toorestart.

## <a name="next-steps"></a>Volgende stappen
Nadat het Hallo-installatie en registratie van het hoofddoel Hallo heeft finsihed, ziet u Hallo hoofddoel worden weergegeven op Hallo **hoofddoel** in sectie **Site Recovery-infrastructuur**, onder Hallo overzicht van configuratie-server.

U kunt nu doorgaan met [beveiligingspoging](site-recovery-how-to-reprotect.md), gevolgd door de failback.

## <a name="common-issues"></a>Algemene problemen

* Zorg ervoor dat u inschakelt Storage vMotion op eventuele management-onderdelen, zoals een hoofddoel. Als hoofddoel Hallo na een geslaagde beveiligt verplaatst, kan de schijven van de virtuele machine hello (VMDKs) kunnen niet worden losgekoppeld. In dit geval failback is mislukt.

* Hallo hoofddoel mag geen eventuele momentopnamen op Hallo virtuele machine. Als momentopnamen bevat, mislukt de failback.

* Hallo-netwerkinterface tijdens het opstarten is uitgeschakeld vanwege toosome aangepaste NIC configuraties op sommige klanten, en Hallo hoofddoel agent kan niet worden geïnitialiseerd. Zorg ervoor dat Hallo volgende eigenschappen correct zijn ingesteld. Controleer deze eigenschappen in Hallo Ethernet-kaart van het bestand /etc/sysconfig/network-scripts/ifcfg-eth *.
    * BOOTPROTO = dhcp
    * ONBOOT = yes
