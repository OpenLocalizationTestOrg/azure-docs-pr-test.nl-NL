---
title: aaaRun een MariaDB (MySQL)-cluster in Azure | Microsoft Docs
description: Maken van een MariaDB + Galera MySQL-cluster op virtuele machines in Azure
services: virtual-machines-linux
documentationcenter: 
author: sabbour
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d0d21937-7aac-4222-8255-2fdc4f2ea65b
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/15/2015
ms.author: asabbour
ms.openlocfilehash: f9a4d6c45d76478a8a3526b407c7bbe6aeb40423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="mariadb-mysql-cluster-azure-tutorial"></a>MariaDB (MySQL)-cluster: zelfstudie voor Azure
> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) en klassieke. In dit artikel bevat informatie over Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties hello Azure Resource Manager-model gebruiken.

> [!NOTE]
> MariaDB Enterprise-cluster is nu beschikbaar in hello Azure Marketplace. nieuwe aanbieding Hallo implementeren automatisch een MariaDB Galera-cluster op Azure Resource Manager. Moet u de nieuwe aanbieding Hallo van [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).
>
>

Dit artikel ziet u hoe een meerdere Master toocreate [Galera](http://galeracluster.com/products/) cluster [MariaDBs](https://mariadb.org/en/about/) (een robuuste, schaalbare en betrouwbare onverwachte ter vervanging van MySQL) toowork in een maximaal beschikbare omgeving op Azure virtuele machines.

## <a name="architecture-overview"></a>Overzicht van de architectuur
Dit artikel wordt beschreven hoe toocomplete Hallo volgende stappen:

- Maak een cluster met drie knooppunten.
- Afzonderlijke Hallo gegevensschijven van Hallo OS-schijf.
- Hallo gegevensschijven in de instelling RAID-0/striped tooincrease IOP's maken.
- Gebruik Azure Load Balancer toobalance Hallo load voor Hallo drie knooppunten.
- herhaalde toominimize werken, een VM-installatiekopie waarin MariaDB + Galera maken en deze gebruiken toocreate Hallo andere cluster virtuele machines.

![Systeemarchitectuur](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> In dit onderwerp maakt gebruik van Hallo [Azure CLI](../../../cli-install-nodejs.md) hulpprogramma's, dus zorg ervoor dat toodownload ze en verbindt u ze tooyour Azure-abonnement volgens toohello instructies. Als u een verwijzing toohello opdrachten die beschikbaar zijn in hello Azure CLI moet, Zie Hallo [Azure CLI-opdrachten](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2). U moet ook te[maken van een SSH-sleutel voor verificatie] en noteer Hallo .pem bestandslocatie.
>
>

## <a name="create-hello-template"></a>Hallo-sjabloon maken
### <a name="infrastructure"></a>Infrastructuur
1. Maken van een affiniteitsgroep toohold Hallo resources samen.

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. Een virtueel netwerk maken.

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. Alle onze schijven voor een toohost storage-account maken. U mag niet meer dan 40 intensief gebruikte schijven te plaatsen op Hallo dezelfde opslag account tooavoid roept Hallo 20.000 IOPS opslaglimiet-account. In dit geval je ruim onder deze limiet, zodat u alles wat u wilt opslaan op Hallo dezelfde voor de eenvoud account.

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. Hallo-naam van de installatiekopie van de virtuele machine Hallo CentOS 7 vinden.

        azure vm image list | findstr CentOS
   Hallo-uitvoer is ongeveer `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.

   Deze naam in de volgende stap Hallo gebruiken.
5. Hallo VM-sjabloon maken en vervang /path/to/key.pem door Hallo pad op waar u Hallo gegenereerd .pem SSH-sleutel hebt opgeslagen.

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. Koppel vier 500 GB aan gegevens schijven toohello VM voor gebruik in Hallo RAID-configuratie.

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. SSH toosign gebruiken in toohello sjabloon voor virtuele machine die u hebt gemaakt op mariadbhatemplate.cloudapp.net:22 en verbinding maken met behulp van uw persoonlijke sleutel.

### <a name="software"></a>Software
1. Hallo-hoofdmap ophalen.

        sudo su

2. Ondersteuning voor RAID installeren:

    a. Mdadm installeren.

              yum install mdadm

    b. Hallo RAID 0/stripe-configuratie maken met een bestandssysteem EXT4.

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    c. Hallo punt Koppelmap maken.

              mkdir /mnt/data
    d. Hallo UUID van Hallo nieuw gemaakte RAID apparaat worden opgehaald.

              blkid | grep /dev/md0
    e. /Etc/fstab bewerken.

              vi /etc/fstab
    f. Voeg Hallo apparaat tooenable automatisch koppelen op opnieuw opstarten, Hallo UUID vervangen door een Hallo-waarde opgehaald uit de vorige Hallo **blkid** opdracht.

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    g. Koppel Hallo nieuwe partitie.

              mount /mnt/data

3. MariaDB installeren.

    a. Hallo MariaDB.repo bestand maken.

                vi /etc/yum.repos.d/MariaDB.repo

    b. Vul Hallo-repo-bestand met Hallo volgende inhoud:

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    c. tooavoid conflicten, verwijder de bestaande postfix en mariadb-bibliotheken.

           yum remove postfix mariadb-libs-*
    d. Installeer MariaDB met Galera.

           yum install MariaDB-Galera-server MariaDB-client galera

4. Hallo MySQL directory toohello RAID blok gegevensapparaat verplaatsen.

    a. Hallo huidige MySQL map kopiëren naar de nieuwe locatie en Hallo oude map verwijderen.

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    b. Stel machtigingen voor de nieuwe map Hallo dienovereenkomstig.

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    c. Maak een symlink die Hallo oude toohello nieuwe maplocatie op Hallo RAID-partitie verwijst.

           ln -s /mnt/data/mysql /var/lib/mysql

5. Omdat [SELinux verstoort Hallo clusterbewerkingen](http://galeracluster.com/documentation-webpages/configuration.html#selinux), toodisable nodig is voor de huidige sessie Hallo. Bewerken `/etc/selinux/config` toodisable voor latere opnieuw wordt opgestart.

            setenforce 0

            then editing `/etc/selinux/config` tooset `SELINUX=permissive`
6. Valideren van MySQL wordt uitgevoerd.

   a. MySQL wordt gestart.

           service mysql start
   b. Hallo MySQL installatie Secure Hallo root-wachtwoord instellen, verwijder anonieme gebruikers toodisable externe hoofdmap aanmelding en Hallo testdatabase verwijderen.

           mysql_secure_installation
   c. Maak een gebruiker op Hallo database voor bewerkingen voor een cluster, en desgewenst voor uw toepassingen.

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* too'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   d. MySQL stoppen.

            service mysql stop
7. Maak een configuratie-tijdelijke aanduiding.

   a. Hallo MySQL configuratie toocreate een tijdelijke aanduiding voor Hallo clusterinstellingen bewerken. Hallo niet vervangen  **`<Variables>`**  of verwijder de opmerking nu. Dat gebeurt nadat u een virtuele machine met deze sjabloon maken.

            vi /etc/my.cnf.d/server.cnf
   b. Hallo bewerken  **[galera]**  sectie en maak deze.

   c. Hallo bewerken **[mariadb]** sectie.

           wsrep_provider=/usr/lib64/galera/libgalera_smm.so
           binlog_format=ROW
           wsrep_sst_method=rsync
           bind-address=0.0.0.0 # When set too0.0.0.0, hello server listens tooremote connections
           default_storage_engine=InnoDB
           innodb_autoinc_lock_mode=2

           wsrep_sst_auth=cluster:p@ssw0rd # CHANGE: Username and password you created for hello SST cluster MySQL user
           #wsrep_cluster_name='mariadbcluster' # CHANGE: Uncomment and set your desired cluster name
           #wsrep_cluster_address="gcomm://mariadb1,mariadb2,mariadb3" # CHANGE: Uncomment and Add all your servers
           #wsrep_node_address='<ServerIP>' # CHANGE: Uncomment and set IP address of this server
           #wsrep_node_name='<NodeName>' # CHANGE: Uncomment and set hello node name of this server
8. Vereiste poorten op Hallo firewall openen met behulp van FirewallD op CentOS 7.

   * MySQL:`firewall-cmd --zone=public --add-port=3306/tcp --permanent`
   * GALERA:`firewall-cmd --zone=public --add-port=4567/tcp --permanent`
   * GALERA IST:`firewall-cmd --zone=public --add-port=4568/tcp --permanent`
   * RSYNC:`firewall-cmd --zone=public --add-port=4444/tcp --permanent`
   * Opnieuw laden Hallo firewall:`firewall-cmd --reload`

9. Hallo-systeem voor prestaties optimaliseren. Zie voor meer informatie [prestaties afstemmen strategie](optimize-mysql.md).

   a. Hallo MySQL-configuratiebestand opnieuw bewerken.

            vi /etc/my.cnf.d/server.cnf
   b. Hallo bewerken **[mariadb]** sectie en toevoeg-Hallo volgende inhoud:

   > [!NOTE]
   > We raden aan dat innodb\_buffer\_pool_size 70 procent van het geheugen van de VM is. In dit voorbeeld is deze ingesteld op 2,45 GB voor de Hallo middelgrote virtuele machine van Azure met 3.5 GB aan RAM-geheugen.
   >
   >

           innodb_buffer_pool_size = 2508M # hello buffer pool contains buffered data and hello index. This is usually set too70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give hello server more time toorecycle idled connections
           innodb_file_per_table = 1 # Speed up hello table space transmission and optimize hello debris management performance
           innodb_log_buffer_size = 128M # hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit
           innodb_flush_log_at_trx_commit = 2 # hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. MySQL stoppen, MySQL-service worden uitgevoerd op opstarten tooavoid Hallo cluster verstoren bij het toevoegen van een knooppunt uitschakelen en inrichting ervan ongedaan Hallo-machine.

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. Hallo VM via de portal Hallo vastleggen. (Momenteel [#1268 in hello Azure CLI-hulpprogramma's uitgeven](https://github.com/Azure/azure-xplat-cli/issues/1268) beschrijft Hallo feit afbeeldingen die zijn vastgelegd door hello Azure CLI-hulpprogramma's worden niet vastgelegd gegevensschijven Hallo gekoppeld.)

    a. Sluit de machine Hallo via Hallo-portal.

    b. Klik op **vastleggen** en geeft u de procesnaam Hallo als **mariadb-galera-image**. Geef een beschrijving op en controleer 'Ik hebben waagent uitvoeren'.
      
      ![Hallo-machine vastleggen](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-hello-cluster"></a>Hallo-cluster maken
Maak drie virtuele machines met Hallo sjabloon die u hebt gemaakt, en vervolgens configureren en Hallo cluster starten.

1. Maak Hallo eerste CentOS 7 VM van Hallo mariadb galera image installatiekopie hebt gemaakt, bieden Hallo volgende informatie:

 - Virtuele-netwerknaam: mariadbvnet
 - Subnet: mariadb
 - Grootte van de computer: gemiddeld
 - Cloudservicenaam: mariadbha (of welke naam u wilt dat toegankelijk is via mariadbha.cloudapp.net toobe)
 - Computernaam: mariadb1
 - Gebruikersnaam: azureuser
 - SSH-toegang: ingeschakeld
 - Hallo SSH-certificaat .pem-bestand doorgeeft en /path/to/key.pem vervangen door een Hallo pad op waar u Hallo opgeslagen gegenereerd .pem SSH-sleutel.

   > [!NOTE]
   > Hallo volgende opdrachten verdeeld zijn over meerdere regels voor de duidelijkheid, maar u moet elk als één regel invoeren.
   >
   >
        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 22
        --vm-name mariadb1
        mariadbha mariadb-galera-image azureuser
2. Twee meer virtuele machines door deze te verbinden toohello mariadbha cloudservice maken. Hallo dezelfde cloudservice Hallo VM-naam wijzigen en Hallo SSH-poort tooa unieke poort niet conflicteert met andere virtuele machines in.

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 23
        --vm-name mariadb2
        --connect mariadbha mariadb-galera-image azureuser
  Voor MariaDB3:

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 24
        --vm-name mariadb3
        --connect mariadbha mariadb-galera-image azureuser
3. U moet tooget Hallo interne IP-adres van elk van de Hallo drie virtuele machines voor de volgende stap Hallo:

    ![IP-adres ophalen](./media/mariadb-mysql-cluster/IP.png)
4. Gebruik van SSH toosign in toohello drie virtuele machines en Hallo-configuratiebestand op elk van deze bewerken.

        sudo vi /etc/my.cnf.d/server.cnf

    Verwijder de opmerking  **`wsrep_cluster_name`**  en  **`wsrep_cluster_address`**  door het verwijderen van Hallo  **#**  aan begin van regel Hallo Hallo.
    Verder vervangen  **`<ServerIP>`**  in  **`wsrep_node_address`**  en  **`<NodeName>`**  in  **`wsrep_node_name`**  Hello De VM-IP-adres een naam, respectievelijk, en verwijder deze regels ook de opmerkingen.
5. Hallo cluster starten op MariaDB1 en laat deze uitgevoerd bij het opstarten.

        sudo service mysql bootstrap
        chkconfig mysql on
6. Start MySQL op MariaDB2 en MariaDB3 en laat het uitgevoerd bij het opstarten.

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-hello-cluster"></a>Load balance Hallo cluster
Wanneer u Hallo geclusterde virtuele machines hebt gemaakt, kunt u ze in een beschikbaarheidsset clusteravset tooensure dat ze op verschillende domeinen met fouten en update domeinen zijn geplaatst en dat Azure nooit onderhoud op alle computers in één keer biedt aangeroepen toegevoegd. Deze configuratie voldoet Hallo toobe ondersteund door hello Azure service level agreement (SLA).

Nu gebruikmaken van Azure Load Balancer toobalance aanvragen tussen Hallo drie knooppunten.

Hallo opdrachten op uw computer te volgen met behulp van Azure CLI Hallo worden uitgevoerd.

Hallo parameters opdrachtstructuur is:`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

Hallo CLI stelt Hallo load balancer-test interval too15 seconden, dat mogelijk iets te lang. Dit wijzigen in de portal Hallo onder **eindpunten** voor alle virtuele machines Hallo.

![Eindpunt bewerken](./media/mariadb-mysql-cluster/Endpoint.PNG)

Selecteer **Reconfigure Hallo Load-Balanced ingesteld**.

![Configureer opnieuw Hallo load-Set met gelijke taakverdeling](./media/mariadb-mysql-cluster/Endpoint2.PNG)

Wijziging **Probe Interval** too5 seconden en sla de wijzigingen.

![Interval voor wijzigen van test](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-hello-cluster"></a>Hallo cluster valideren
Hallo harde werk wordt uitgevoerd. Hallo-cluster moet nu toegankelijk zijn op `mariadbha.cloudapp.net:3306`, die Hallo load balancer treffers en route-aanvragen tussen drie virtuele machines Hallo soepel en efficiënt.

Uw favoriete MySQL client tooconnect gebruiken of verbinding maakt vanaf een Hallo VMs tooverify dat dit cluster werkt.

     mysql -u cluster -h mariadbha.cloudapp.net -p

Vervolgens maakt u een database en deze vullen met gegevens.

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

Hallo-database die u hebt gemaakt, retourneert Hallo volgende tabel:

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Volgende stappen
In dit artikel wordt gemaakt van een drie-knooppunt MariaDB + Galera maximaal beschikbare cluster in Azure virtuele machines actief CentOS 7. Hallo VM's zijn taakverdeling met Azure Load Balancer.

U kunt toolook op [een andere manier toocluster MySQL op Linux](mysql-cluster.md) en manieren te[optimaliseren en test de prestaties van MySQL op Azure Linux VM's](optimize-mysql.md).

<!--Anchors-->
[Architecture overview]:#architecture-overview
[Creating hello template]:#creating-the-template
[Creating hello cluster]:#creating-the-cluster
[Load balancing hello cluster]:#load-balancing-the-cluster
[Validating hello cluster]:#validating-the-cluster
[Next steps]:#next-steps

<!--Image references-->

<!--Link references-->
[Galera]:http://galeracluster.com/products/
[MariaDBs]:https://mariadb.org/en/about/
[maken van een SSH-sleutel voor verificatie]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/
[issue #1268 in hello Azure CLI]:https://github.com/Azure/azure-xplat-cli/issues/1268
