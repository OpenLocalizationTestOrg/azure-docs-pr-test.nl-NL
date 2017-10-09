---
title: aaaConfigure MPIO op StorSimple Linux-host | Microsoft Docs
description: MPIO op StorSimple verbonden tooa Linux-host met CentOS 6.6 configureren
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: tysonn
ms.assetid: ca289eed-12b7-4e2e-9117-adf7e2034f2f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: alkohli
ms.openlocfilehash: d9f7e02903243494c909313fb2c33ac690764274
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a>MPIO configureren op een StorSimple-host waarop van CentOS
Dit artikel wordt uitgelegd Hallo stappen vereist tooconfigure Multipath I/O (MPIO) op uw Centos 6.6 host-server. Hallo host-server is verbonden tooyour Microsoft Azure StorSimple-apparaat voor hoge beschikbaarheid via iSCSI-initiators. Hierin wordt beschreven in detail Hallo automatische detectie van meerdere paden apparaten en specifieke instellingen Hallo alleen voor StorSimple-volumes

Deze procedure is van toepassing tooall Hallo modellen van apparaten voor StorSimple 8000-serie.

> [!NOTE]
> Deze procedure kan niet worden gebruikt voor een virtueel StorSimple-apparaat. Zie voor meer informatie hoe tooconfigure hostservers voor uw virtuele apparaat.
> 
> 

## <a name="about-multipathing"></a>Over het gebruik van meerdere paden
Hallo Multipath-functie kunt u tooconfigure meerdere i/o-paden tussen een hostserver en een opslagapparaat. Deze i/o-paden zijn fysieke SAN-verbindingen die afzonderlijke kabels, switches, netwerkinterfaces en domeincontrollers kunnen opnemen. Gebruik van meerdere paden aggregeert Hallo i/o-paden, tooconfigure een nieuw apparaat dat is gekoppeld aan alle paden Hallo geaggregeerd.

Hallo-doel van meerdere paden is tweeledig:

* **Hoge beschikbaarheid**: biedt een alternatief pad als elk element van Hallo i/o-pad (zoals een kabel, switch, netwerkinterface of domeincontroller) is mislukt.
* **Taakverdeling**: afhankelijk van de configuratie van de Hallo van uw opslagapparaat, deze prestaties kan verbeteren Hallo belasting op Hallo i/o-paden te detecteren en dynamisch herverdeling de belasting.

### <a name="about-multipathing-components"></a>Over het gebruik van meerdere paden onderdelen
Gebruik van meerdere paden in Linux bestaat uit de kernel als gebruikersruimte componenten zoals hieronder in een tabel.

* **Kernel**: Hallo hoofdonderdeel is Hallo *apparaat mapper* die wordt omgeleid i/o en failover voor paden en pad groepen ondersteunt.

* **Gebruikersruimte innemen**: dit zijn *multipath-tools* die welke toodo multipathed apparaten door multipath apparaat mapper-module Hallo beheren. Hallo-hulpprogramma's bestaan uit:
   
   * **Multipath**: geeft een lijst van en multipathed apparaten configureert.
   * **Multipathd**: daemon die multipath en monitors Hallo-paden wordt uitgevoerd.
   * **Naam van de Devmap**: biedt een zinvolle apparaatnaam tooudev voor devmaps.
   * **Kpartx**: lineaire devmaps toodevice partities toomake multipath maps partitioneerbare wordt toegewezen.
   * **Multipath.conf**: configuratiebestand voor multipath-daemon is gebruikte toooverwrite Hallo ingebouwde configuratietabel.

### <a name="about-hello-multipathconf-configuration-file"></a>Over Hallo multipath.conf-configuratiebestand
Hallo-configuratiebestand `/etc/multipath.conf` maakt veel Hallo Multipath-functies kunnen worden geconfigureerd met een gebruiker. Hallo `multipath` opdracht en Hallo kernel-daemon `multipathd` gebruik informatie gevonden in dit bestand. Hallo-bestand is geraadpleegd alleen tijdens het Hallo-configuratie van MPIO Hallo-apparaten. Zorg ervoor dat alle wijzigingen worden aangebracht voordat u Hallo uitvoert `multipath` opdracht. Als u Hallo bestand wijzigt daarna u moet toostop en multipathd voor Hallo wijzigingen tootake effect nogmaals te starten.

Hallo multipath.conf heeft vijf secties:

- **Niveau standaardsysteemwaarden** *(standaardwaarden)*: U kunt niveau standaardwaarden van het systeem onderdrukken.
- **Apparaten gebeurd** *(blacklist)*: U kunt opgeven dat Hallo lijst met apparaten die niet moeten worden gecontroleerd door apparaat toewijzen.
- **Uitzonderingen afgekeurde** *(blacklist_exceptions)*: U specifieke apparaten toobe behandeld als multipath-apparaten, zelfs als wordt weergegeven in zwarte lijst Hallo kunt identificeren.
- **Specifieke instellingen voor de controller opslag** *(apparaten)*: U kunt configuratie-instellingen die worden toegepast toodevices waarvoor leverancier-en productinformatie opgeven.
- **Specifieke apparaatinstellingen** *(multipaths)*: U kunt deze sectie toofine afstemmen Hallo configuratie-instellingen voor afzonderlijke LUN's.

## <a name="configure-multipathing-on-storsimple-connected-toolinux-host"></a>Gebruik van meerdere paden op StorSimple verbonden tooLinux host configureren
Een StorSimple-apparaat aansluit tooa Linux-host kan worden geconfigureerd voor hoge beschikbaarheid en taakverdeling. Bijvoorbeeld, als Hallo Linux-host heeft twee interfaces zijn verbonden toohello hello en SAN-apparaat heeft twee interfaces verbonden toohello SAN zodat deze interfaces worden op hetzelfde subnet Hallo en er zijn 4 paden beschikbaar. Echter, als elke interface gegevens op het apparaat en host interface Hallo op een ander IP-subnet (en niet-routeerbaar), vervolgens alleen 2 paden zijn beschikbaar. U kunt meerdere paden tooautomatically detecteren van alle beschikbare Hallo-paden, kiest u een taakverdelingsalgoritme voor die paden, toepassen specifieke configuratie-instellingen voor alleen-StorSimple-volumes, inschakelen en controleer of u gebruik van meerdere paden.

Hallo volgende procedure wordt beschreven waarom de tooconfigure Multipath wanneer een StorSimple-apparaat met twee netwerkinterfaces verbonden tooa host met twee netwerkinterfaces.

## <a name="prerequisites"></a>Vereisten
Deze sectie beschrijft Hallo configuratievereisten voor CentOS-server en het StorSimple-apparaat.

### <a name="on-centos-host"></a>Op de host CentOS
1. Zorg ervoor dat uw CentOS-host 2 netwerkinterfaces ingeschakeld heeft. Type:
   
    `ifconfig`
   
    Hallo volgende voorbeeld ziet u uitvoer Hallo wanneer twee netwerkinterfaces (`eth0` en `eth1`) aanwezig zijn op Hallo host.
   
        [root@centosSS ~]# ifconfig
        eth0  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:41  
          inet addr:10.126.162.65  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3341/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:36536 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6312 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:13994127 (13.3 MiB)  TX bytes:645654 (630.5 KiB)
   
        eth1  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:42  
          inet addr:10.126.162.66  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3342/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3342/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25962 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2597350 (2.4 MiB)  TX bytes:754 (754.0 b)
   
        loLink encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:12 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:720 (720.0 b)  TX bytes:720 (720.0 b)
2. Installeer *iSCSI-initiator-utils* op uw server CentOS. Volgende stappen tooinstall Hallo uitvoeren *iSCSI-initiator-utils*.
   
   1. Meld u aan als `root` in uw CentOS-host.
   2. Hallo installeren *iSCSI-initiator-utils*. Type:
      
       `yum install iscsi-initiator-utils`
   3. Na het Hallo *iSCSI-Initiator-utils* met succes is geïnstalleerd, start Hallo iSCSI-service. Type:
      
       `service iscsid start`
      
       In gevallen `iscsid` mogelijk niet daadwerkelijk start en Hallo `--force` optie zijn mogelijk vereist
   4. tooensure dat uw iSCSI-initiator is ingeschakeld tijdens het opstarten, gebruik Hallo `chkconfig` opdracht tooenable Hallo-service.
      
       `chkconfig iscsi on`
   5. tooverify dat deze goed is instellen, Hallo-opdracht uitvoeren:
      
       `chkconfig --list | grep iscsi`
      
       Hieronder ziet u een voorbeeld van de uitvoer.
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       Van Hallo hierboven voorbeeld ziet u dat uw omgeving iSCSI op opstarten op uitvoeren niveaus 2, 3, 4 en 5 wordt uitgevoerd.
3. Installeer *apparaat-mapper-multipath*. Type:
   
    `yum install device-mapper-multipath`
   
    Hallo-installatie wordt gestart. Type **Y** toocontinue wanneer u om bevestiging wordt gevraagd.

### <a name="on-storsimple-device"></a>Op het StorSimple-apparaat
Uw StorSimple-apparaat moet hebben:

* Minimaal twee interfaces zijn ingeschakeld voor iSCSI. tooverify dat twee interfaces zijn ingeschakeld voor iSCSI op uw StorSimple-apparaat, voert u stappen te volgen in de klassieke Azure-portal voor uw StorSimple-apparaat Hallo Hallo:
  
  1. Meld u aan bij de klassieke portal Hallo voor uw StorSimple-apparaat.
  2. Selecteer uw StorSimple Manager-service, klikt u op **apparaten** en kies Hallo specifieke StorSimple-apparaat. Klik op **configureren** en controleer of Hallo netwerkinterface-instellingen. Een schermafbeelding met twee netwerkinterfaces zijn ingeschakeld voor iSCSI-worden hieronder weergegeven. Hier DATA 2 en DATA 3, beide 10 GbE interfaces zijn ingeschakeld voor iSCSI.
     
      ![Configuratie van MPIO StorsSimple DATA 2](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![MPIO StorSimple gegevens 3 Config](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      In Hallo **configureren** pagina
     
     1. Zorg ervoor dat beide netwerkinterfaces iSCSI-functionaliteit. Hallo **iSCSI ingeschakeld** veld te moet worden ingesteld**Ja**.
     2. Zorg ervoor dat de netwerkinterfaces Hallo Hallo hebben dezelfde snelheid beide moet 1 GbE- of 10 GbE.
     3. Houd er rekening mee Hallo IPv4-adressen van Hallo ingeschakeld voor iSCSI-interfaces en opslaan voor toekomstig gebruik op Hallo host.
* Hallo iSCSI-interfaces op uw StorSimple-apparaat moet bereikbaar is vanaf Hallo CentOS-server.
      tooverify, moet u tooprovide Hallo IP-adressen van uw StorSimple-ingeschakeld voor iSCSI-netwerkinterfaces op de hostserver. Hallo opdrachten die worden gebruikt en de bijbehorende uitvoer met DATA2 Hallo (10.126.162.25) en DATA3 (10.126.162.26) worden hieronder weergegeven:
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a>Hardwareconfiguratie
Het is raadzaam dat u verbinding Hallo twee iSCSI-netwerkinterfaces op afzonderlijke paden voor de redundantie maakt. Hallo afbeelding hieronder ziet u de aanbevolen hardwareconfiguratie Hallo voor hoge beschikbaarheid en taakverdeling gebruik van meerdere paden voor uw CentOS-server en het StorSimple-apparaat.

![MPIO-hardwareconfiguratie voor StorSimple tooLinux host](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

Zoals u in de voorgaande afbeelding Hallo:

* Uw StorSimple-apparaat zich in een actief / passief-configuratie met twee domeincontrollers.
* Twee SAN-switches zijn verbonden tooyour apparaatcontrollers.
* Twee iSCSI-initiators zijn ingeschakeld op uw StorSimple-apparaat.
* Twee netwerkinterfaces zijn ingeschakeld op uw host CentOS.

Hallo hierboven configuratie resulteert 4 afzonderlijke paden tussen uw apparaat en het Hallo-host als Hallo host- en interfaces routeerbaar zijn.

> [!IMPORTANT]
> * Het is raadzaam dat u niet door elkaar 1 GbE- en 10 GbE-netwerkinterfaces voor gebruik van meerdere paden. Wanneer u twee netwerkinterfaces, moeten beide interfaces Hallo Hallo identiek type zijn.
> * Op uw StorSimple-apparaat DATA0, bestand1, DATA4 en DATA5 zijn 1 GbE-interfaces DATA2 en DATA3 10 GbE-netwerkinterfaces zijn. |
> 
> 

## <a name="configuration-steps"></a>Configuratiestappen
Hallo configuratiestappen voor gebruik van meerdere paden hebben betrekking op Hallo beschikbare paden voor automatische detectie, geven Hallo-taakverdeling algoritme toouse, gebruik van meerdere paden inschakelen en ten slotte Hallo-configuratie controleren configureren. Elk van deze stappen wordt uitgebreid beschreven in Hallo uit te voeren.

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a>Stap 1: Configureer meerdere paden voor automatische detectie
Hallo multipath-ondersteunde apparaten kunnen automatisch worden gedetecteerd en geconfigureerd.

1. Initialiseren `/etc/multipath.conf` bestand. Type:
   
     `mpathconf --enable`
   
    Hallo bovenstaande opdracht maakt een `sample/etc/multipath.conf` bestand.
2. Multipath-service starten. Type:
   
    `service multipathd start`
   
    Hier ziet u Hallo volgende uitvoer:
   
    `Starting multipathd daemon:`
3. Automatische detectie van multipaths inschakelen. Type:
   
    `mpathconf --find_multipaths y`
   
    Dit wijzigt Hallo standaardwaarden gedeelte van uw `multipath.conf` zoals hieronder wordt weergegeven:
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a>Stap 2: Configureer meerdere paden voor StorSimple-volumes
Standaard worden alle apparaten zwart zijn vermeld in Hallo multipath.conf bestand en zal worden overgeslagen. U moet toocreate blacklist uitzonderingen tooallow gebruik van meerdere paden voor volumes van StorSimple-apparaten.

1. Hallo bewerken `/etc/mulitpath.conf` bestand. Type:
   
    `vi /etc/multipath.conf`
2. Hallo blacklist_exceptions sectie in Hallo multipath.conf bestand vinden. Uw StorSimple-apparaat moet toobe vermeld als een zwarte lijst uitzondering in deze sectie. U kunt opmerkingen bij de relevante regels in dit bestand toomodify het hieronder (Gebruik alleen Hallo specifieke model van Hallo apparaat dat u gebruikt):
   
        blacklist_exceptions {
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8100*"
            }
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8600*"
            }
           }

### <a name="step-3-configure-round-robin-multipathing"></a>Stap 3: Gebruik van meerdere paden round robin configureren
Deze load balancing-algoritme maakt gebruik van alle Hallo beschikbaar multipaths toohello actieve controller taakverdeling, round-robin toewijst.

1. Hallo bewerken `/etc/multipath.conf` bestand. Type:
   
    `vi /etc/multipath.conf`
2. Onder Hallo `defaults` sectie, set Hallo `path_grouping_policy` te`multibus`. Hallo `path_grouping_policy` Hallo standaard pad groepering beleid tooapply toounspecified multipaths bevat. Hallo standaardwaarden sectie eruit zoals hieronder wordt weergegeven.
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> meest voorkomende waarden van Hallo `path_grouping_policy` omvatten:
> 
> * failover = 1 pad per groep prioriteit
> * multibus = alle geldige paden in de groep 1 prioriteit
> 
> 

### <a name="step-4-enable-multipathing"></a>Stap 4: Enable meerdere paden
1. Opnieuw opstarten Hallo `multipathd` daemon. Type:
   
    `service multipathd restart`
2. Hallo-uitvoer zijn zoals hieronder wordt weergegeven:
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a>Stap 5: Controleren of gebruik van meerdere paden
1. Eerst voor zorgen dat dat iSCSI-verbinding tot stand is gebracht met Hallo StorSimple-apparaat als volgt:
   
   a. Detecteren van uw StorSimple-apparaat. Type:
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on hello device>:<iSCSI port on StorSimple device>
    ```
    
    Hallo uitvoer wanneer IP-adres voor DATA0 10.126.162.25 en poort 3260 wordt geopend op Hallo StorSimple-apparaat voor uitgaande iSCSI-verkeer is zoals hieronder wordt weergegeven:
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    Kopiëren Hallo IQN van uw StorSimple-apparaat `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, van Hallo voorafgaand aan de uitvoer.

   b. Verbinding maken met doel IQN toohello-apparaat. Hallo StorSimple-apparaat is hier Hallo iSCSI-doel. Type:

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    Hallo volgende voorbeeld ziet u uitvoer met een doel IQN van `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`. Hallo-uitvoer geeft aan dat u verbinding hebt gemaakt toohello twee ingeschakeld voor iSCSI-netwerkinterfaces op uw apparaat.

    ```
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    Als u slechts één host-interface en twee paden Hier ziet, moet u tooenable beide Hallo-interfaces op de host voor iSCSI. U kunt volgen Hallo [gedetailleerde instructies in de documentatie van Linux](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).

2. Een volume is blootgestelde toohello CentOS server uit Hallo StorSimple-apparaat. Zie voor meer informatie [stap 6: een volume maken](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via Hallo klassieke Azure-portal op uw StorSimple-apparaat.

3. Controleer of de beschikbare paden Hallo. Type:

      ```
      multipath –l
      ```

      Hallo volgende voorbeeld ziet u de uitvoer Hallo voor twee netwerkinterfaces op de netwerkinterface van StorSimple-apparaat verbonden tooa één host met twee beschikbare paden.

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        hello following example shows hello output for two network interfaces on a StorSimple device connected tootwo host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After hello paths are configured, refer toohello specific instructions on your host operating system (Centos 6.6) toomount and format this volume.

## <a name="troubleshoot-multipathing"></a>Problemen met meerdere paden
Deze sectie bevat enkele nuttige tips als u problemen ondervindt tijdens het gebruik van meerdere paden configureren uitvoert.

Q. Zie ik niet Hallo wijzigingen in `multipath.conf` bestand die van kracht.

A. Als u toohello wijzigingen hebt aangebracht `multipath.conf` -bestand, moet u toorestart Hallo Multipath-service. Type Hallo volgende opdracht:

    service multipathd restart

Q. Ik heb twee netwerkinterfaces op Hallo StorSimple-apparaat en twee netwerkinterfaces op de host Hallo ingeschakeld. Wanneer ik de lijst beschikbare paden hello, zie ik slechts twee paden. Toosee vier beschikbare paden wordt verwacht.

A. Zorg ervoor dat Hallo twee paden op Hallo hetzelfde subnet en routeerbaar. Als de netwerkinterfaces Hallo zich op verschillende VLAN's en niet routeerbaar te maken, u slechts twee paden ziet. Eenzijdige tooverify dit is toomake ervoor dat u beide interfaces Hallo host van een netwerkinterface op Hallo StorSimple-apparaat kan bereiken. U moet te[contact op met Microsoft Support](storsimple-contact-microsoft-support.md) zoals deze verificatie kan alleen worden uitgevoerd via een ondersteuningssessie voor.

Q. Wanneer ik de lijst beschikbare paden, zie ik niet geen uitvoer.

A. Normaal gesproken een probleem met de Hallo Multipath-daemon niet ziet multipathed paden voorgesteld en is waarschijnlijk dat hier probleem veroorzaakt door Hallo `multipath.conf` bestand.

Het is ook waard controleren dat u daadwerkelijk een aantal schijven zien kunt nadat u hebt aangesloten toohello doel, omdat er geen reactie van Hallo multipath aanbiedingen kan ook betekenen er geen schijven.

* Gebruik Hallo opdracht toorescan Hallo SCSI-bus te volgen:
  
    `$ rescan-scsi-bus.sh `(onderdeel van het pakket sg3_utils)
* Type Hallo volgende opdrachten:
  
    `$ dmesg | grep sd*`
     
     of
  
    `$ fdisk –l`
  
    Deze wordt details van onlangs toegevoegde schijven geretourneerd.
* toodetermine of het om een schijf StorSimple gebruiken Hallo volgende opdrachten:
  
    `cat /sys/block/<DISK>/device/model`
  
    Hiermee wordt een tekenreeks, die bepaalt of het een StorSimple-schijf is geretourneerd.

Een minder waarschijnlijk maar mogelijke oorzaak kan ook worden de verlopen iscsid pid. Hallo opdracht toolog volgende uitschakelen uit Hallo iSCSI-sessies gebruiken:

    iscsiadm -m node --logout -p <Target_IP>

Herhaal deze opdracht voor alle Hallo verbonden netwerkinterfaces op Hallo iSCSI target, dit uw StorSimple-apparaat is. Nadat u afgemeld bij alle Hallo iSCSI-sessies bent, gebruikt u Hallo iSCSI-doel IQN tooreestablish Hallo iSCSI-sessie. Type Hallo volgende opdracht:

    iscsiadm -m node --login -T <TARGET_IQN>


Q. Ik wil niet zeker weet of het apparaat wilt plaatsen is.

A. tooverify of uw apparaat wilt plaatsen, is gebruik Hallo voor probleemoplossing interactief opdracht te volgen:

    multipathd –k
    multipathd> show devices
    available block devices:
    ram0 devnode blacklisted, unmonitored
    ram1 devnode blacklisted, unmonitored
    ram2 devnode blacklisted, unmonitored
    ram3 devnode blacklisted, unmonitored
    ram4 devnode blacklisted, unmonitored
    ram5 devnode blacklisted, unmonitored
    ram6 devnode blacklisted, unmonitored
    ram7 devnode blacklisted, unmonitored
    ram8 devnode blacklisted, unmonitored
    ram9 devnode blacklisted, unmonitored
    ram10 devnode blacklisted, unmonitored
    ram11 devnode blacklisted, unmonitored
    ram12 devnode blacklisted, unmonitored
    ram13 devnode blacklisted, unmonitored
    ram14 devnode blacklisted, unmonitored
    ram15 devnode blacklisted, unmonitored
    loop0 devnode blacklisted, unmonitored
    loop1 devnode blacklisted, unmonitored
    loop2 devnode blacklisted, unmonitored
    loop3 devnode blacklisted, unmonitored
    loop4 devnode blacklisted, unmonitored
    loop5 devnode blacklisted, unmonitored
    loop6 devnode blacklisted, unmonitored
    loop7 devnode blacklisted, unmonitored
    sr0 devnode blacklisted, unmonitored
    sda devnode whitelisted, monitored
    dm-0 devnode blacklisted, unmonitored
    dm-1 devnode blacklisted, unmonitored
    dm-2 devnode blacklisted, unmonitored
    sdb devnode whitelisted, monitored
    sdc devnode whitelisted, monitored
    dm-3 devnode blacklisted, unmonitored


Voor meer informatie gaat te[probleemoplossing interactief opdracht voor het gebruik van meerdere paden gebruiken](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).

## <a name="list-of-useful-commands"></a>Lijst met opdrachten nuttig
| Type | Opdracht | Beschrijving |
| --- | --- | --- |
| **iSCSI** |`service iscsid start` |ISCSI-service starten |
| &nbsp; |`service iscsid stop` |ISCSI-service stoppen |
| &nbsp; |`service iscsid restart` |ISCSI-service opnieuw starten |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |Detecteren van beschikbare doelen op Hallo opgegeven adres |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |Meld u bij toohello iSCSI-doel |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |Meld u af van Hallo iSCSI-doel |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |Naam van de iSCSI-initiator afdrukken |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |Controleer de status van de Hallo van Hallo iSCSI-sessie en het volume dat is gedetecteerd op Hallo host |
| &nbsp; |`iscsi –m session` |Bevat alle Hallo iSCSI-sessies tot stand gebracht tussen het Hallo-host en Hallo StorSimple-apparaat |
|  | | |
| **Gebruik van meerdere paden** |`service multipathd start` |Multipath-daemon starten |
| &nbsp; |`service multipathd stop` |Multipath-daemon stoppen |
| &nbsp; |`service multipathd restart` |Multipath-daemon starten |
| &nbsp; |`chkconfig multipathd on` </br> OF </br> `mpathconf –with_chkconfig y` |Schakel multipath-daemon toostart tijdens het opstarten |
| &nbsp; |`multipathd –k` |Hallo interactieve console voor probleemoplossing starten |
| &nbsp; |`multipath –l` |Lijst met meerdere paden verbindingen en apparaten |
| &nbsp; |`mpathconf --enable` |Maken van een voorbeeldbestand mulitpath.conf in`/etc/mulitpath.conf` |
|  | | |

## <a name="next-steps"></a>Volgende stappen
Als u de MPIO op Linux-host configureert, moet u ook toorefer toohello CentoS 6.6 documenten te volgen:

* [Instellen van MPIO op CentOS](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [Linux Training handleiding](http://linux-training.be/files/books/LinuxAdm.pdf)

