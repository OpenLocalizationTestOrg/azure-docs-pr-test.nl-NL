---
title: MySQL-prestaties op Linux aaaOptimize | Microsoft Docs
description: Meer informatie over hoe toooptimize MySQL uitgevoerd op Azure een virtuele machine (VM) waarop Linux wordt uitgevoerd.
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0c1c7fc5-a528-4d84-b65d-2df225f2233f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: ningk
ms.openlocfilehash: 9e6458723233721e06f30b9de33635d403eefcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a>MySQL-optimaliseren op Azure Linux VM 's
Er zijn talloze factoren die van invloed op prestaties MySQL in Azure, zowel in de selectie van de virtuele hardware en softwareconfiguratie. Dit artikel is gericht op optimaliseren prestaties door middel van opslag-, systeem- en databaseconfiguraties.

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) en klassieke. In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Zie voor meer informatie over Linux-VM-optimalisatie met Resource Manager-model Hallo [optimaliseren van uw Linux-VM op Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="utilize-raid-on-an-azure-virtual-machine"></a>Gebruikmaken van RAID op een virtuele machine van Azure
Opslag is Hallo van groot belang dat betrekking heeft op de prestaties van de database in cloudomgevingen. Enkele schijf vergeleken tooa RAID kan sneller toegang via Gelijktijdigheidsfout bieden. Zie voor meer informatie [standaard RAID-niveaus](http://en.wikipedia.org/wiki/Standard_RAID_levels).   

-I/o-schijfdoorvoer en i/o-reactietijd in Azure kunnen worden verbeterd via RAID. Onze tests lab ziet u dat-i/o-schijfdoorvoer kan worden verdubbeld en i/o-reactietijd kan worden verkleind door helft gemiddeld wanneer verdubbeld Hallo aantal RAID-schijven (van toofour twee, vier tooeight, enzovoort). Zie [bijlage A](#AppendixA) voor meer informatie.  

Bovendien toodisk i/o, MySQL prestaties worden verbeterd als u Hallo RAID-niveau verhogen.  Zie [bijlage B](#AppendixB) voor meer informatie.  

U kunt ook tooconsider Hallo chunkgrootte. In het algemeen als u een grotere chunkgrootte hebt, krijgt u lagere overhead, met name voor grote schrijfbewerkingen. Wanneer de chunkgrootte hello te groot is, kan deze extra overhead die voorkomen dat u profiteert van RAID toevoegen. de huidige standaardgrootte Hallo is 512 KB bewezen wordt toobe optimaal is voor de meest algemene productieomgevingen. Zie [bijlage C](#AppendixC) voor meer informatie.   

Er gelden beperkingen op hoeveel schijven die u voor andere virtuele machine-typen kunt toevoegen. Deze limieten zijn aangegeven in [grootten voor virtuele machine en cloud-service voor Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx). U moet vier bijgesloten gegevens schijven toofollow Hallo RAID voorbeeld in dit artikel, hoewel u tooset van RAID met minder schijven kunt kiezen.  

In dit artikel wordt ervan uitgegaan dat u al een virtuele Linux-machine hebt gemaakt en hebben MYSQL geïnstalleerd en geconfigureerd. Zie voor meer informatie over aan de slag, hoe tooinstall MySQL in Azure.  

### <a name="set-up-raid-on-azure"></a>Instellen van RAID op Azure
Hallo volgende stappen laten zien hoe toocreate RAID op Azure met behulp van hello Azure-portal. U kunt ook RAID instellen met behulp van Windows PowerShell-scripts.
In dit voorbeeld configureert we RAID 0 met vier schijven.  

#### <a name="add-a-data-disk-tooyour-virtual-machine"></a>Een data schijf tooyour virtuele machine toevoegen
In hello Azure-portal, gaat u toohello dashboard en selecteer Hallo virtuele machine toowhich gewenste tooadd een gegevensschijf. In dit voorbeeld is Hallo virtuele machine mysqlnode1.  

<!--![Virtual machines][1]-->

Klik op **schijven** en klik vervolgens op **nieuwe koppelen**.

![Virtuele machines toevoegen schijf](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

Maak een nieuwe schijf van 500 GB. Zorg ervoor dat **Host Cache voorkeur** te is ingesteld,**geen**.  Wanneer u klaar bent, klikt u op **OK**.

![Lege schijf koppelen](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


Hiermee wordt een lege schijf in uw virtuele machine toegevoegd. Herhaal deze stap drie keer zodat er vier gegevensschijven voor RAID.  

U kunt zien Hallo toegevoegd stations in Hallo virtuele machine door te kijken Hallo kernel berichtenlogboek. Bijvoorbeeld: toosee op Ubuntu, gebruik Hallo volgende opdracht:  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-hello-additional-disks"></a>RAID Hello extra schijven maken
Hallo volgende stappen wordt beschreven hoe te[configureren van software-RAID op Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

> [!NOTE]
> Als u van Hallo XFS bestandssysteem gebruikmaakt, uitvoeren Hallo stappen te volgen nadat u RAID hebt gemaakt.
>
>

tooinstall XFS op Debian, Ubuntu of Linux-munt gebruik Hallo volgende opdracht:  

    apt-get -y install xfsprogs  

tooinstall XFS op Fedora, CentOS of RHEL, gebruik Hallo volgende opdracht:  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a>Een nieuw opslagpad instellen
Gebruik Hallo opdracht tooset van een nieuw opslagpad te volgen:  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-hello-original-data-toohello-new-storage-path"></a>Hallo oorspronkelijke toohello nieuwe opslag gegevenspad kopiëren
Hallo opdracht toocopy toohello nieuwe opslag gegevenspad volgende gebruiken:  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-hello-data-disk"></a>(Lezen en schrijven) zodat MySQL toegang heeft tot wijzigingsmachtiging Hallo gegevensschijf
Hallo volgende opdracht toomodify machtigingen gebruiken:  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-hello-disk-io-scheduling-algorithm"></a>Hallo schijf-i/o algoritme planning aanpassen
Linux implementeert vier typen i/o algoritmen plannen:  

* Nooperation-algoritme (Er is geen bewerking)
* Deadline-algoritme (Deadline)
* Volledig evenredige Queuing-algoritme (CFQ)
* Periode budget-algoritme (Anticipatory)  

U kunt verschillende i/o-planners onder verschillende scenario's toooptimize prestaties selecteren. In een omgeving met volledig willekeurige toegang is er een belangrijk verschil tussen Hallo CFQ en Deadline algoritmen voor prestaties. Het is raadzaam dat u Hallo MySQL-database omgeving tooDeadline voor stabiliteit ingesteld. Als er een groot aantal opeenvolgende i/o, mogelijk CFQ schijf-i/o-prestaties verminderen.   

Voor de SSD- en andere apparatuur bereiken Nooperation of Deadline betere prestaties dan Hallo standaard scheduler.   

Eerdere toohello kernel 2.5, Hallo standaard i/o planning algoritme is een Deadline. Beginnen met Hallo kernel 2.6.18, werd CFQ Hallo i/o-planning standaardalgoritme.  U kunt deze instelling tijdens het opstarten van de kernel opgeven of deze instelling dynamisch te wijzigen wanneer Hallo-systeem wordt uitgevoerd.  

Hallo volgende voorbeeld laat zien hoe Hallo scheduler toohello Nooperation standaardalgoritme in Hallo Debian distributie familie toocheck en set.  

### <a name="view-hello-current-io-scheduler"></a>Weergave Hallo huidige i/o-planner
tooview hello scheduler Hallo volgende opdracht uitvoeren:  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

Ziet u uitvoer, waarmee wordt aangegeven van de huidige Taakplanner hello te volgen:  

    noop [deadline] cfq


### <a name="change-hello-current-device-devsda-of-hello-io-scheduling-algorithm"></a>Wijzigen in een huidige Hallo-apparaat (/ dev/sda) van planning Hallo i/o-algoritme
Voer Hallo opdrachten toochange Hallo huidige apparaat te volgen:  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> Instellen van dit voor /dev/sda zichzelf is niet handig. Deze moet worden ingesteld op alle gegevensschijven waar Hallo-database zich bevindt.  
>
>

U ziet Hallo volgende uitvoer, die aangeeft dat grub.cfg met succes is opnieuw opgebouwd en die standaard Hallo scheduler is bijgewerkte tooNOOP:  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

Voor Hallo Red Hat distributie familie, moet u alleen Hallo volgende opdracht:

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a>Bewerkingen van de systeeminstellingen-bestand configureren
Een aanbevolen procedure is toodisable hello *atime* functie voor logboekregistratie op Hallo-bestandssysteem. Atime is hello bestandstijd van laatste. Wanneer een bestand wordt geopend, Hallo Hallo system bestandsrecords tijdstempel in Hallo logboek. Deze informatie wordt echter zelden gebruikt. U kunt deze uitschakelen als u niet nodig hebt, waarmee algehele schijftijd toegang wordt beperkt.  

toodisable atime aan te melden, u moet toomodify Hallo bestand system configuratie bestand /etc/ bevinden fstab en Hallo toevoegen **noatime** optie.  

Bijvoorbeeld, bewerk Hallo vim /etc/fstab bestand, toe te voegen Hallo noatime, zoals wordt weergegeven in Hallo voorbeeld te volgen:  

    # CLOUD_IMG: This file was created/modified by hello Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add hello “noatime” option below toodisable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

Vervolgens opnieuw koppelen Hallo bestandssysteem Hello volgende opdracht:  

    mount -o remount /RAID0

Test Hallo gewijzigd resultaat. Wanneer u het testbestand Hallo wijzigt, wordt Hallo tijd niet bijgewerkt. Hallo volgen voorbeelden kunt u zien welke Hallo code ziet er vóór en na wijziging.

Voor:        

![Code voordat toegang werd gewijzigd][5]

Na:

![Code na wijziging toegang][6]

## <a name="increase-hello-maximum-number-of-system-handles-for-high-concurrency"></a>Maximum aantal ingangen voor hoge gelijktijdigheid system Hallo vergroten
MySQL is een database hoge gelijktijdigheid van taken. Hallo standaardaantal gelijktijdige ingangen is 1024 voor Linux, die niet altijd voldoende. Volgende stappen tooincrease Hallo maximum aantal gelijktijdige ingangen van Hallo system toosupport hoge gelijktijdigheid van MySQL hello gebruiken.

### <a name="modify-hello-limitsconf-file"></a>Hallo limits.conf bestand wijzigen
tooincrease hello maximum aantal gelijktijdige ingangen toegestaan, Hallo volgende vier regels in Hallo /etc/security/limits.conf bestand toevoegen. Houd er rekening mee dat 65536 Hallo maximumaantal die Hallo-systeem kan ondersteunen.   

    * voorlopig nofile 65536
    * vaste nofile 65536
    * voorlopig nproc 65536
    * vaste nproc 65536

### <a name="update-hello-system-for-hello-new-limits"></a>Hallo-systeem voor nieuwe Hallo-beperkingen bijwerken
tooupdate hello systeem, Hallo volgende opdrachten uitvoeren:  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-hello-limits-are-updated-at-boot-time"></a>Zorg ervoor dat de Hallo limieten tijdens het opstarten zijn bijgewerkt
Starten van de opdrachten in Hallo /etc/rc.local bestand volgen zodat deze van tijdens het opstarten kracht wordt Hallo geplaatst.  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a>Optimalisatie van MySQL-database
tooconfigure MySQL in Azure, kunt u dezelfde prestaties afstemmen strategie u op een on-premises machine gebruiken Hallo.  

Hallo belangrijkste i/o-optimalisatie regels zijn:   

* Hallo-cachegrootte verhogen.
* I/o-reactietijd verminderen.  

toooptimize MySQL-serverinstellingen, kunt u Hallo my.cnf bestand Hallo standaardconfiguratiebestand voor server en clientcomputers bijwerken.  

Hallo zijn volgende configuratie-items Hallo belangrijkste factoren die van invloed op prestaties MySQL:  

* **innodb_buffer_pool_size**: Hallo buffergroep buffer opgeslagen gegevens en Hallo index bevat. Dit wordt meestal ingesteld too70 procent van het fysieke geheugen.
* **innodb_log_file_size**: dit Hallo opnieuw logboekgrootte is. U opnieuw logboeken tooensure dat schrijfbewerkingen snelle, betrouwbare en hersteld na een crash zijn. Deze wordt too512 MB, zodat u voldoende ruimte voor het registreren van schrijfbewerkingen ingesteld.
* **max_connections**: soms toepassingen niet sluiten verbindingen goed. Een hogere waarde geeft Hallo server meer tijd toorecycle inactief sinds verbindingen. Hallo kunt u het maximum aantal verbindingen is 10.000, maar Hallo aanbevolen maximaal 5.000 is.
* **Innodb_file_per_table**: deze instelling Hiermee schakelt u of de mogelijkheid Hallo van InnoDB toostore tabellen in afzonderlijke bestanden. Schakel Hallo optie tooensure dat verschillende geavanceerde beheerbewerkingen efficiënt kunnen worden toegepast. Uit oogpunt van prestaties kan het versnellen Hallo tabel ruimte verzending en Hallo opgeruimd management prestaties te optimaliseren. Hallo aanbevolen instelling voor deze optie is ingeschakeld.</br></br>
Hallo standaardinstelling is ingeschakeld, van MySQL 5.6, dus er is geen actie vereist. Voor eerdere versies is de standaardinstelling Hallo uitgeschakeld. Hallo-instelling moet worden gewijzigd voordat gegevens worden geladen, omdat alleen de zojuist gemaakte tabellen worden getroffen.
* **innodb_flush_log_at_trx_commit**: Hallo standaardwaarde is 1, hello bereik too0 stelt ~ 2. Hallo-standaardwaarde is de meest geschikte optie Hallo zelfstandig MySQL-database. Hallo-instelling van 2 schakelt Hallo meeste gegevensintegriteit en geschikt is voor het model in de MySQL-Cluster. Hallo-instelling van 0 kan verlies van gegevens die invloed kan zijn op de betrouwbaarheid (in sommige gevallen met betere prestaties) en is geschikt voor Slave in MySQL-Cluster.
* **Innodb_log_buffer_size**: Hallo logboekbuffer kan transacties toorun zonder tooflush Hallo logboek toodisk voordat Hallo transacties doorvoeren. Als er grote binaire object of tekstveld, Hallo cache snel worden gebruikt en regelmatig schijf-i/o wordt geactiveerd. Het is beter Hallo buffergrootte verhogen als Innodb_log_waits status variabele niet is 0.
* **query_cache_size**: de beste optie Hallo is toodisable op Hallo begin. Query_cache_size too0 (dit is de standaardinstelling Hallo in MySQL 5.6) en andere toospeed methoden om query's gebruikt.  

Zie [bijlage D](#AppendixD) voor een vergelijking van de prestaties voor en na Hallo optimalisatie.

## <a name="turn-on-hello-mysql-slow-query-log-for-analyzing-hello-performance-bottleneck"></a>Hallo MySQL trage querylogboek voor het analyseren van het prestatieknelpunt Hallo inschakelen
Hallo MySQL trage querylogboek kunt u trage Hallo-query's voor MySQL identificeren. Nadat de Hallo MySQL trage query-logboek is ingeschakeld, kunt u MySQL hulpmiddelen zoals **mysqldumpslow** tooidentify hello prestatieknelpunt.  

Standaard, is dit niet ingeschakeld. Hallo trage querylogboek inschakelen mogelijk enkele CPU-resources in beslag nemen. Het is raadzaam dat u dit tijdelijk inschakelt voor het oplossen van knelpunten. tooturn op Hallo trage querylogboek:

1. Hallo my.cnf bestand wijzigen door Hallo na toohello regels toe te voegen:

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. Hallo MySQL-server opnieuw opstarten.

        service  mysql  restart

3. Controleer of instelling Hallo effect duurt via Hallo **weergeven** opdracht.

![Trage query log ON][7]   

![Resultaten van trage-query-logboek][8]

In dit voorbeeld ziet u dat deze functie van de query wordt vertraagd Hallo is ingeschakeld. Vervolgens kunt u Hallo **mysqldumpslow** hulpprogramma toodetermine prestatieknelpunten en optimaliseren, zoals het toevoegen van indexen.

## <a name="appendices"></a>Bijlagen
Hallo hieronder vindt u voorbeeld test prestatiegegevens in een testomgeving gerichte geproduceerd. Ze bieden algemene achtergrond op Hallo prestaties gegevens trend met verschillende prestaties afstemmen benaderingen. Hallo resultaten kunnen variëren en onder verschillende versies van omgeving of product.

### <a name="AppendixA"></a>Bijlage A  
**Prestaties (IOPS) van de schijf met verschillende RAID-niveaus**

![Schijf IOP's met verschillende RAID-niveaus][9]

**Test-opdrachten**  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> Hallo werkbelasting van deze test maakt gebruik van 64 threads, probeert tooreach Hallo bovengrens van RAID.
>
>

### <a name="AppendixB"></a>Bijlage B  
**Vergelijking van MySQL-prestaties (doorvoer) met verschillende RAID-niveaus**   
(XFS bestandssysteem)

![Vergelijking van MySQL-prestaties met verschillende RAID-niveaus][10]  
![Vergelijking van MySQL-prestaties met verschillende RAID-niveaus][11]

**Test-opdrachten**

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

**Vergelijking van MySQL-prestaties (OLTP) met verschillende RAID-niveaus**  
![Vergelijking van MySQL-prestaties (OLTP) met verschillende RAID-niveaus][12]

**Test-opdrachten**

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <a name="AppendixC"></a>Bijlage C   
**Vergelijking van de schijf prestaties (IOPS) voor verschillende chunk grootten**  
(XFS bestandssysteem)

![][13]

**Test-opdrachten**  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

Hallo bestandsgrootten waarmee deze test zijn respectievelijk 30 GB en 1 GB, met RAID 0 (4 schijven) XFS bestandssysteem.

### <a name="AppendixD"></a>Bijlage D  
**Vergelijking van MySQL prestaties (doorvoer) voor en na optimalisatie**  
(XFS File System)

![Vergelijking van MySQL prestaties (doorvoer) voor en na optimalisatie][14]

**Test-opdrachten**

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

**Hallo-configuratie-instelling voor standaard- en optimalisatie is als volgt:**

| Parameters | Standaard | Optimalisatie |
| --- | --- | --- |
| **innodb_buffer_pool_size** |Geen |7 GB |
| **innodb_log_file_size** |5 MB |512 MB |
| **max_connections** |100 |5000 |
| **innodb_file_per_table** |0 |1 |
| **innodb_flush_log_at_trx_commit** |1 |2 |
| **innodb_log_buffer_size** |8 MB |128 MB |
| **query_cache_size** |16 MB |0 |

Voor meer gedetailleerde [optimalisatie configuratieparameters](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), Raadpleeg toohello [MySQL officiële instructies](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).  

  **Testomgeving**  

| Hardware | Details |
| --- | --- |
| CPU |AMD Opteron (TM) Processor 4171 hij / 4 kernen |
| Geheugen |14 GB |
| Schijf |10 GB/schijf |
| OS |Ubuntu 14.04.1 TNS |

[1]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-01.png
[2]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-02.png
[3]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-03.png
[4]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-04.png
[5]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-05.png
[6]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-06.png
[7]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-07.png
[8]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-08.png
[9]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-09.png
[10]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-10.png
[11]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-11.png
[12]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-12.png
[13]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-13.png
[14]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-14.png

