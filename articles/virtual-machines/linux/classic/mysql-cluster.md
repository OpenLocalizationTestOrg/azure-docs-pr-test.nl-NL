---
title: aaaClusterize MySQL met gelijke taakverdeling sets | Microsoft Docs
description: Instellen van een taakverdeling hoge beschikbaarheid Linux MySQL-cluster met de Hallo klassieke implementatiemodel in Azure gemaakt
services: virtual-machines-linux
documentationcenter: 
author: bureado
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6c413a16-e9b5-4ffe-a8a3-ae67046bbdf3
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/14/2015
ms.author: jparrel
ms.openlocfilehash: 1829fd877c4b0ed177b23a8e3404dbb3db746561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-load-balanced-sets-tooclusterize-mysql-on-linux"></a>Sets met gelijke taakverdeling tooclusterize MySQL gebruiken op Linux
> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) en klassieke. In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Een [Resource Manager-sjabloon](https://azure.microsoft.com/documentation/templates/mysql-replication/) is beschikbaar als u een MySQL-cluster toodeploy nodig.

Dit artikel wordt verkend en ziet u Hallo verschillende benaderingen beschikbaar toodeploy maximaal beschikbare op basis van Linux services op Microsoft Azure, hoge beschikbaarheid van de MySQL-Server als een primer verkennen. Een video ter illustratie van deze benadering is beschikbaar op [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).

Er wordt een overzicht van niets wordt gedeeld, twee knooppunten, één master MySQL oplossing met hoge beschikbaarheid op basis van DRBD Corosync en pacemaker heeft. Slechts één knooppunt MySQL op een tijdstip wordt uitgevoerd. Lezen en schrijven van Hallo DRBD resource is ook beperkte tooonly één knooppunt tegelijk.

Er is niet nodig om een VIP-oplossing zoals LVS, omdat u Netwerktaakverdeling sets in Microsoft Azure tooprovide round robin-functionaliteit en eindpunt detectie, verwijderen en gecontroleerde herstelprocedure Hallo VIP. Hallo VIP is een algemeen routeerbaar IPv4-adres toegewezen door Microsoft Azure wanneer u eerst de cloudservice Hallo maken.

Er zijn andere mogelijke architecturen voor MySQL, met inbegrip van de volgende werkdag Cluster, Percona Galera en verschillende middleware oplossingen, waaronder ten minste één beschikbaar als een virtuele machine op [VM Depot](http://vmdepot.msopentech.com). Zolang deze oplossingen op unicast-vs. multicast of broadcast repliceren kunnen en Vertrouw niet op de gedeelde opslag of meerdere netwerkinterfaces, moet Hallo scenario's gemakkelijk toodeploy in Microsoft Azure.

Deze clustering architecturen kunnen tooother producten, zoals PostgreSQL en OpenLDAP op soortgelijke wijze worden uitgebreid. Bijvoorbeeld: deze procedure taakverdeling met waarbij niets wordt gedeeld met succes is getest met meerdere master OpenLDAP en kunt u deze bekijken op ons blog Channel 9.

## <a name="get-ready"></a>Voorbereiden
U moet de volgende Hallo bronnen en mogelijkheden:

  - Een Microsoft Azure-account met een geldig abonnement, kunnen toocreate ten minste twee virtuele machines (XS is gebruikt in dit voorbeeld)
  - Een netwerk en een subnet
  - Een affiniteitsgroep
  - Een beschikbaarheidsset
  - Hallo mogelijkheid toocreate VHD's in dezelfde regio bevinden als de cloudservice Hallo Hallo en koppel deze toohello virtuele Linux-machines

### <a name="tested-environment"></a>Geteste omgeving
* Ubuntu 13.10
  * DRBD
  * MySQL-Server
  * Corosync en pacemaker heeft

### <a name="affinity-group"></a>Affiniteitsgroep
Maken van een affiniteitsgroep voor Hallo oplossing met toohello klassieke Azure-portal aanmelden selecteren **instellingen**, en het maken van een affiniteitsgroep. Toegewezen bronnen maken later worden toothis affiniteitsgroep bevinden toegewezen.

### <a name="networks"></a>Netwerken
Een nieuw netwerk wordt gemaakt en een subnet binnen Hallo-netwerk wordt gemaakt. Dit voorbeeld wordt een 10.10.10.0/24-netwerk met slechts één /24 subnet binnen.

### <a name="virtual-machines"></a>Virtuele machines
Hallo eerste Ubuntu 13.10 VM wordt gemaakt met behulp van een afbeelding Endorsed Ubuntu en heet `hadb01`. Een nieuwe cloudservice wordt gemaakt bij Hallo hadb aangeroepen. Deze naam illustreert Hallo gedeeld, taakverdeling aard Hallo service hebben wanneer er meer resources worden toegevoegd. het maken van Hallo `hadb01` wordt probleemloze ingevuld met behulp van Hallo-portal. Een eindpunt voor SSH wordt automatisch gemaakt en nieuwe Hallo-netwerk is geselecteerd. U kunt nu een beschikbaarheidsset voor Hallo virtuele machines maken.

Nadat de Hallo eerste VM wordt gemaakt (technisch gezien is bij het Hallo-cloudservice is gemaakt), maakt u Hallo tweede VM `hadb02`. Tweede VM voor hello, Ubuntu 13.10 VM van Hallo galerie met behulp van de portal hello gebruiken, maar een bestaande cloudservice `hadb.cloudapp.net`, in plaats van een nieuwe maken. Hallo-netwerk en beschikbaarheid set moet automatisch worden geselecteerd. Een SSH-eindpunt wordt gemaakt, te.

Nadat beide virtuele machines zijn gemaakt, noteer Hallo SSH-poort voor `hadb01` (TCP 22) en `hadb02` (automatisch toegewezen door Azure).

### <a name="attached-storage"></a>Gekoppelde opslag
Koppelen van een nieuwe schijf tooboth VM's en 5 GB schijven in Hallo proces maken. Hallo-schijven worden in VHD-container in het gebruik van de belangrijkste besturingssysteem schijven Hallo gehost. Nadat de schijven zijn gemaakt en gekoppeld, is er geen noodzaak toorestart Linux omdat Hallo kernel Hallo nieuw apparaat ziet. Dit apparaat is meestal `/dev/sdc`. Controleer `dmesg` voor Hallo uitvoer.

Op elke virtuele machine, kunt u een partitie maken met behulp van `cfdisk` (primaire, Linux-partitie) en nieuwe partitietabel Hallo schrijven. Maak een bestandssysteem geen op deze partitie.

## <a name="set-up-hello-cluster"></a>Hallo-cluster instellen
Gebruik APT tooinstall Corosync pacemaker heeft en DRBD op beide Ubuntu VM. toodo geval met `apt-get`, voert hello volgende code:

    sudo apt-get install corosync pacemaker drbd8-utils.

Installeer geen MySQL op dit moment. Debian en Ubuntu installatiescripts een MySQL-gegevensmap op wordt geïnitialiseerd `/var/lib/mysql`, maar omdat Hallo directory wordt vervangen door een bestandssysteem DRBD, moet u later tooinstall MySQL.

Controleer of (met behulp van `/sbin/ifconfig`) dat beide VM gebruikmaakt van adressen in Hallo 10.10.10.0/24 subnet en dat ze elkaar op naam kunnen pingen. U kunt ook `ssh-keygen` en `ssh-copy-id` toomake ervoor dat beide virtuele machines kunnen communiceren via SSH zonder een wachtwoord.

### <a name="set-up-drbd"></a>DRBD instellen
Maak een DRBD resource die gebruikmaakt van onderliggende hello `/dev/sdc1` tooproduce partitie een `/dev/drbd1` resource die kan worden geformatteerd met ext3 en gebruikt in de primaire en secundaire knooppunten.

1. Open `/etc/drbd.d/r0.res` en kopiëren Hallo resourcedefinitie op beide VM:

        resource r0 {
          on `hadb01` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.4:7789;
            meta-disk internal;
          }
          on `hadb02` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.5:7789;
            meta-disk internal;
          }
        }

2. Hallo resource initialiseren met `drbdadm` op beide virtuele machines:

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. Op Hallo van primaire virtuele machine (`hadb01`), eigendom (primair) van Hallo DRBD resource afdwingen:

        sudo drbdadm primary --force r0

Als u hello-inhoud van proc/drbd bekijkt (`sudo cat /proc/drbd`) op beide virtuele machines, ziet u `Primary/Secondary` op `hadb01` en `Secondary/Primary` op `hadb02`, in overeenstemming met het Hallo-oplossing op dit moment. Hallo 5 GB schijfruimte is via Hallo 10.10.10.0/24 netwerk op geen kosten toocustomers gesynchroniseerd.

Nadat het Hallo-schijf wordt gesynchroniseerd, kunt u Hallo bestandssysteem maken op `hadb01`. Voor testdoeleinden, hebben we ext2 gebruikt, maar Hallo volgende code maakt een bestandssysteem ext3:

    mkfs.ext3 /dev/drbd1

### <a name="mount-hello-drbd-resource"></a>Hallo DRBD resource koppelen
U bent nu klaar toomount hello DRBD bronnen op `hadb01`. Debian en afleidingen gebruik `/var/lib/mysql` als de gegevensmap van MySQL. Omdat u MySQL nog niet hebt geïnstalleerd, Hallo-map maken en koppelen Hallo DRBD resource. tooperform deze optie worden uitgevoerd na de code op Hallo `hadb01`:

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a>MySQL instellen
U kunt nu klaar tooinstall MySQL op `hadb01`:

    sudo apt-get install mysql-server

Voor `hadb02`, hebt u twee opties. U kunt de mysql-server, die wordt /var/lib/mysql maken, vult u deze met een nieuwe map voor gegevens, en verwijder vervolgens Hallo inhoud installeren. tooperform deze optie worden uitgevoerd na de code op Hallo `hadb02`:

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

de tweede optie Hallo is toofailover te`hadb02` en installeer vervolgens er mysql-server. Installatiescripts ziet Hallo bestaande installatie en het heeft geen invloed.

Voer hello na de code op `hadb01`:

    sudo drbdadm secondary –force r0

Voer hello na de code op `hadb02`:

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

Als u niet van plan toofailover DRBD nu bent, is de eerste optie Hallo Hoewel weliswaar minder elegante eenvoudiger. Nadat u dit instellen, kunt u beginnen aan uw MySQL-database werkt. Voer hello na de code op `hadb02` (of elk ander een van de servers Hallo actief is, op basis van tooDRBD):

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* tooroot;

> [!WARNING]
> Deze laatste instructie effectief dat verificatie is uitgeschakeld voor de hoofdgebruiker Hallo in deze tabel. Dit moet worden vervangen door uw productie-hoogwaardige instructies verlenen en is opgenomen alleen ter illustratie.

Als u wilt toomake query's van VM's voor externe hello (dit is Hallo doel van deze handleiding), moet u ook tooenable netwerken voor MySQL. Open op beide VM `/etc/mysql/my.cnf` en ga te`bind-address`. Hallo-adres wijzigen van 127.0.0.1 too0.0.0.0. Na het Hallo-bestand opslaan, geven een `sudo service mysql restart` op uw huidige primaire.

### <a name="create-hello-mysql-load-balanced-set"></a>Hallo MySQL taakverdeling set maken
Ga terug toohello portal, gaat u te`hadb01`, en kies **eindpunten**. toocreate een eindpunt, MySQL (TCP 3306) kiezen uit de vervolgkeuzelijst Hallo en selecteer **set met gelijke taakverdeling maken nieuwe load**. Naam Hallo taakverdeling eindpunt `lb-mysql`. Stel **tijd** minimale too5 seconden.

Nadat u Hallo-eindpunt maken, gaat u te`hadb02`, kies **eindpunten**, en een eindpunt te maken. Kies `lb-mysql`, en selecteer vervolgens MySQL in de vervolgkeuzelijst Hallo. U kunt ook hello Azure CLI gebruiken voor deze stap.

U hebt nu alles wat die u nodig hebt voor handmatige bewerking van Hallo-cluster.

### <a name="test-hello-load-balanced-set"></a>Hallo taakverdeling set testen
Tests kunnen worden uitgevoerd vanaf een externe computer via een MySQL-client of met behulp van bepaalde toepassingen, zoals phpMyAdmin uitgevoerd als een Azure-website. In dit geval gebruikt u het opdrachtregelprogramma van MySQL in een andere Linux:

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a>Handmatig failover wordt uitgevoerd
U kunt failovers simuleren door MySQL afgesloten, overschakelen DRBD van primaire en MySQL opnieuw te starten.

tooperform deze taak uitvoeren na de code op hadb01 Hallo:

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

Klik op hadb02:

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

Nadat u handmatig een failover, kunt u uw externe query herhalen en deze moet perfect werkt.

## <a name="set-up-corosync"></a>Corosync instellen
Corosync is Hallo onderliggende clusterinfrastructuur is vereist voor toowork pacemaker heeft. Corosync is een splitsing van Hallo-CRM-functionaliteit voor Heartbeat (en andere methoden zoals Ultramonkey), terwijl pacemaker heeft meer lijken tooHeartbeat in de functionaliteit blijft.

Hallo belangrijkste beperking voor Corosync in Azure is dat Corosync multicast via broadcast boven unicast-communicatie verkiest, maar Microsoft Azure-netwerken alleen unicast ondersteunt.

Gelukkig heeft Corosync een werkende unicast-modus. Hallo alleen echte beperking is omdat alle knooppunten niet onderling communiceren zijn, u toodefine Hallo knooppunten in uw configuratiebestanden moet, met inbegrip van de IP-adressen. We Hallo Corosync voorbeeldbestanden kunnen gebruiken voor Unicast en wijzig adres, knooppunt lijsten en logboekregistratie-mappen binden (Ubuntu gebruikt `/var/log/corosync` terwijl Hallo voorbeeld gebruik bestanden `/var/log/cluster`), en hulpprogramma's voor quorum inschakelen.

> [!NOTE]
> Gebruik de volgende Hallo `transport: udpu` richtlijn en Hallo handmatig IP-adressen voor beide knooppunten worden gedefinieerd.

Voer hello na de code op `/etc/corosync/corosync.conf` voor beide knooppunten:

    totem {
      version: 2
      crypto_cipher: none
      crypto_hash: none
      interface {
        ringnumber: 0
        bindnetaddr: 10.10.10.0
        mcastport: 5405
        ttl: 1
      }
      transport: udpu
    }

    logging {
      fileline: off
      to_logfile: yes
      to_syslog: yes
      logfile: /var/log/corosync/corosync.log
      debug: off
      timestamp: on
      logger_subsys {
        subsys: QUORUM
        debug: off
        }
      }

    nodelist {
      node {
        ring0_addr: 10.10.10.4
        nodeid: 1
      }

      node {
        ring0_addr: 10.10.10.5
        nodeid: 2
      }
    }

    quorum {
      provider: corosync_votequorum
    }

Kopieer dit configuratiebestand op beide virtuele machines en Corosync in beide knooppunten te starten:

    sudo service start corosync

Hallo-cluster moet worden gemaakt in de huidige ring Hallo kort na het Hallo-service wordt gestart, en quorum moet worden gevormd. We kunnen deze functionaliteit controleren aan de hand van Logboeken of door te voeren Hallo code te volgen:

    sudo corosync-quorumtool –l

Hier ziet u uitvoer vergelijkbare toohello installatiekopie te volgen:

![voorbeelduitvoer van corosync quorumtool - l](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a>Pacemaker heeft instellen
Pacemaker heeft gebruikt Hallo cluster toomonitor voor resources, definiëren wanneer de primaire omlaag gaan en deze resources toosecondaries overschakelen. Resources kunnen worden gedefinieerd van een reeks beschikbaar scripts of van LSB (init-achtige)-scripts, onder andere opties.

We willen pacemaker heeft te 'eigen' hello DRBD resource Hallo koppelpunt en Hallo MySQL-service. Als pacemaker heeft en uitschakelen DRBD inschakelen kunt, koppelen en ontkoppelen, en vervolgens starten en stoppen MySQL in Hallo juiste volgorde wanneer er een probleem gebeurt Hello primaire, setup is voltooid.

Wanneer u pacemaker heeft voor het eerst installeert, worden uw configuratie eenvoudige genoeg is, bijvoorbeeld:

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. Controleer de configuratie van Hallo door het uitvoeren van `sudo crm configure show`.
2. Maak een bestand (zoals `/tmp/cluster.conf`) Hello resources te volgen:

        primitive drbd_mysql ocf:linbit:drbd \
              params drbd_resource="r0" \
              op monitor interval="29s" role="Master" \
              op monitor interval="31s" role="Slave"

        ms ms_drbd_mysql drbd_mysql \
              meta master-max="1" master-node-max="1" \
                clone-max="2" clone-node-max="1" \
                notify="true"

        primitive fs_mysql ocf:heartbeat:Filesystem \
              params device="/dev/drbd/by-res/r0" \
              directory="/var/lib/mysql" fstype="ext3"

        primitive mysqld lsb:mysql

        group mysql fs_mysql mysqld

        colocation mysql_on_drbd \
               inf: mysql ms_drbd_mysql:Master

        order mysql_after_drbd \
               inf: ms_drbd_mysql:promote mysql:start

        property stonith-enabled=false

        property no-quorum-policy=ignore

3. Hallo-bestand in Hallo configuratie laden. U hoeft alleen toodo dit in één knooppunt.

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. Zorg ervoor dat pacemaker heeft tijdens het opstarten in beide knooppunten begint:

        sudo update-rc.d pacemaker defaults

5. Met behulp van `sudo crm_mon –L`, controleert u of een van uw knooppunten Hallo master voor Hallo-cluster is geworden en alle Hallo resources wordt uitgevoerd. U kunt koppelen en ps toocheck Hallo resources met gebruiken.

Hallo volgende schermafbeelding ziet `crm_mon` met één knooppunt gestopt (afsluiten door te selecteren Ctrl + C):

![crm_mon knooppunt gestopt](./media/mysql-cluster/image002.png)

Deze schermafbeelding ziet u knooppunten, één master en een lager niveau bevindende:

![crm_mon operationele master/slave](./media/mysql-cluster/image003.png)

## <a name="testing"></a>Testen
U bent klaar voor de simulatie van een automatische failover. Er zijn van twee manieren toodo dit: zachte en harde.

Hallo zachte manier gebruikt van het cluster Hallo afsluiten functie: ``crm_standby -U `uname -n` -v on``. Als u deze op Hallo master gebruiken, neemt Hallo slave op. Houd er rekening mee tooset deze back-toooff. Als u dit niet doet, ziet crm_mon één knooppunt op stand-by.

Hallo vaste manier wordt afgesloten omlaag Hallo Hallo primaire virtuele machine (hadb01) via de portal Hallo of door te wijzigen (uitvoeringsniveau) op Hallo VM (dat wil zeggen, stoppen, afsluiten). Hierdoor kunnen Corosync en pacemaker heeft door-signalering gaat omlaag dat Hallo-model. U kunt dit testen (dit is nuttig voor onderhoudsvensters), maar u kunt ook Hallo scenario afdwingen door bevriezing Hallo VM.

## <a name="stonith"></a>STONITH
Het moet mogelijk tooissue VM afsluiten via hello Azure CLI in plaats van een script STONITH die een fysiek apparaat bepaalt. U kunt `/usr/lib/stonith/plugins/external/ssh` als een basis- en inschakelen STONITH in Hallo clusterconfiguratie. Azure CLI globaal moet worden geïnstalleerd en Hallo publish settings-profiel moet worden geladen voor de gebruiker Hallo-cluster.

Voorbeeldcode voor Hallo resource is beschikbaar op [GitHub](https://github.com/bureado/aztonith). Hallo clusterconfiguratie wijzigen door toe te voegen hello te volgen`sudo crm configure`:

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> Hallo-script uitvoeren niet omhoog/omlaag controles. Hallo oorspronkelijke SSH resource 15 ping cheques had, maar hersteltijd voor een Azure-virtuele machine mogelijk meer variabele.

## <a name="limitations"></a>Beperkingen
Hallo volgen beperkingen toepassen:

* Hallo linbit DRBD resource script waarmee DRBD worden beheerd als een resource in pacemaker heeft gebruikt `drbdadm down` bij het afsluiten van een knooppunt, zelfs als er Hallo knooppunt net op stand-by. Dit is niet ideaal omdat Hallo slave zal niet worden synchroniseren Hallo DRBD resource terwijl Hallo master schrijfbewerkingen opgehaald. Als Hallo master niet vriendelijk mislukt, kan Hallo slave de systeemstatus van een oudere bestand overnemen. Er zijn twee mogelijke manieren om dit op te lossen:
  * Afdwingen van een `drbdadm up r0` op alle clusterknooppunten via een lokale (niet-clusterized) watchdog
  * Hallo linbit DRBD script bewerken en ervoor te zorgen dat `down` niet wordt aangeroepen in`/usr/lib/ocf/resource.d/linbit/drbd`
* Hallo load balancer moet ten minste vijf seconden toorespond, zodat toepassingen clusterbewust is en minder gevoelig voor time-out. Andere architecturen, zoals in-app-wachtrijen en query middlewares, kunnen ook helpen.
* MySQL afstemmen nodig tooensure die beheerbare tempo geschreven en caches leeggemaakte toodisk zo vaak als mogelijke toominimize geheugen gegevensverlies.
* Prestaties zijn afhankelijk in VM schrijven onderling verbinding maken in de virtuele switch hello, omdat dit Hallo mechanisme dat wordt gebruikt door DRBD tooreplicate Hallo apparaat.
