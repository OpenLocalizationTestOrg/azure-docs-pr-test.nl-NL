---
title: hoge beschikbaarheid virtuele Machines voor SAP NetWeaver op SUSE Linux Enterprise Server voor SAP-toepassingen aaaAzure | Microsoft Docs
description: Hoge beschikbaarheid handleiding voor SAP NetWeaver op SUSE Linux Enterprise Server voor SAP-toepassingen
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: mssedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: sedusch
ms.openlocfilehash: e944103df92d5ffec9196189f138e25972bea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a>Hoge beschikbaarheid voor SAP NetWeaver op Azure VM's op SUSE Linux Enterprise Server voor SAP-toepassingen

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

[2205917]:https://launchpad.support.sap.com/#/notes/2205917
[1944799]:https://launchpad.support.sap.com/#/notes/1944799
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

Dit artikel wordt beschreven hoe toodeploy Hallo virtuele machines Hallo virtuele machines configureren, Hallo cluster framework hebt geïnstalleerd en een maximaal beschikbare SAP NetWeaver 7,50 systeem installeren.
In Hallo voorbeeldconfiguraties, enzovoort-opdrachten voor installatie. ASC's exemplaarnummer 00, Ebruikers exemplaarnummer 02 en SAP-systeem kan NWS-ID wordt gebruikt. Hallo namen van Hallo resources (bijvoorbeeld virtuele machines, virtuele netwerken) in Hallo voorbeeld wordt ervan uitgegaan dat u hebt gebruikt dat Hallo [geconvergeerde sjabloon] [ template-converged] met SAP ID NWS toocreate Hallo systeembronnen.

Hallo eerst na de SAP-opmerkingen en documenten lezen

* SAP-notitie [1928533], die is:
  * Lijst met Azure VM-grootten die worden ondersteund voor de implementatie van Hallo van SAP-software
  * Informatie over belangrijke capaciteit voor Azure VM-grootten
  * Ondersteunde SAP-software en besturingssysteem (OS) en combinaties van de database
  * Vereiste SAP-kernel-versie voor Windows en Linux op Microsoft Azure

* SAP-notitie [2015553] bevat vereisten voor software-implementaties SAP SAP ondersteund in Azure.
* SAP-notitie [2205917] heeft aanbevolen OS-instellingen voor SUSE Linux Enterprise Server voor SAP-toepassingen
* SAP-notitie [1944799] heeft SAP HANA richtlijnen voor SUSE Linux Enterprise Server voor SAP-toepassingen
* SAP-notitie [2178632] bevat gedetailleerde informatie over alle bewaking metrische gegevens die zijn gerapporteerd voor SAP in Azure.
* SAP-notitie [2191498] Hallo vereist SAP Host Agent-versie voor Linux in Azure.
* SAP-notitie [2243692] bevat informatie over SAP licentieverlening op Linux in Azure.
* SAP-notitie [1984787] heeft algemene informatie over SUSE Linux Enterprise Server 12.
* SAP-notitie [1999351] bevat aanvullende informatie over probleemoplossing voor hello Azure verbeterde extensie Monitoring voor SAP.
* [SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) heeft alle SAP-opmerkingen voor Linux vereist.
* [Azure virtuele Machines, planning en implementatie voor SAP op Linux][planning-guide]
* [Azure virtuele Machines-implementatie voor SAP op Linux (in dit artikel)][deployment-guide]
* [Azure virtuele Machines DBMS-implementatie voor SAP op Linux][dbms-guide]
* [Scenario voor optimale SAP HANA SR prestaties][suse-hana-ha-guide]  
  Hallo handleiding bevat alle vereiste gegevens tooset van SAP HANA System Replication on-premises. Deze handleiding gebruiken als basislijn.
* [Maximaal beschikbare NFS opslag met DRBD en pacemaker heeft] [ suse-drbd-guide] Hallo handleiding bevat alle vereiste gegevens tooset van een maximaal beschikbare NFS-server. Deze handleiding gebruiken als basislijn.


## <a name="overview"></a>Overzicht

tooachieve hoge beschikbaarheid, SAP NetWeaver vereist dat een NFS-server. Hallo NFS-server is geconfigureerd in een cluster met afzonderlijke en kan worden gebruikt door meerdere SAP-systemen.

![SAP NetWeaver hoge beschikbaarheid-overzicht](./media/high-availability-guide-suse/img_001.png)

Hallo NFS-server, SAP NetWeaver ASC's, SAP NetWeaver SCS, SAP NetWeaver Ebruikers en Hallo SAP HANA-database gebruiken virtuele hostnaam en virtuele IP-adressen. In Azure is een load balancer vereist toouse een virtueel IP-adres. Hallo bevat volgende lijst Hallo configuratie van Hallo load balancer.

### <a name="nfs-server"></a>NFS-Server
* Frontend configuratie
  * IP-adres 10.0.0.4
* Back-endconfiguratie
  * Netwerkinterfaces tooprimary van alle virtuele machines die deel uitmaken van Hallo NFS cluster moeten worden verbonden
* De Testpoort
  * Poort 61000
* Loadbalancing regels
  * 2049 TCP 
  * 2049 UDP

### <a name="ascs"></a>(A) SCS
* Frontend configuratie
  * IP-adres 10.0.0.10
* Back-endconfiguratie
  * Netwerkinterfaces verbonden tooprimary van alle virtuele machines die deel van hello (A) SCS Ebruikers/cluster uitmaken moet
* De Testpoort
  * Poort 620**&lt;nr&gt;**
* Loadbalancing regels
  * 32**&lt;nr&gt;**  TCP
  * 36**&lt;nr&gt;**  TCP
  * 39**&lt;nr&gt;**  TCP
  * 81**&lt;nr&gt;**  TCP
  * 5**&lt;nr&gt;**13 TCP
  * 5**&lt;nr&gt;**14 TCP
  * 5**&lt;nr&gt;**16 TCP

### <a name="ers"></a>EBRUIKERS
* Frontend configuratie
  * IP-adres 10.0.0.11
* Back-endconfiguratie
  * Netwerkinterfaces verbonden tooprimary van alle virtuele machines die deel van hello (A) SCS Ebruikers/cluster uitmaken moet
* De Testpoort
  * Poort 621**&lt;nr&gt;**
* Loadbalancing regels
  * 33**&lt;nr&gt;**  TCP
  * 5**&lt;nr&gt;**13 TCP
  * 5**&lt;nr&gt;**14 TCP
  * 5**&lt;nr&gt;**16 TCP

### <a name="sap-hana"></a>SAP HANA
* Frontend configuratie
  * IP-adres 10.0.0.12
* Back-endconfiguratie
  * Netwerkinterfaces tooprimary van alle virtuele machines die deel uitmaken van Hallo HANA cluster moeten worden verbonden
* De Testpoort
  * Poort 625**&lt;nr&gt;**
* Loadbalancing regels
  * 3**&lt;nr&gt;**15 TCP
  * 3**&lt;nr&gt;**17 TCP

## <a name="setting-up-a-highly-available-nfs-server"></a>Een maximaal beschikbare NFS-server instellen

### <a name="deploying-linux"></a>Linux implementeren

Hello Azure Marketplace bevat een afbeelding voor SUSE Linux Enterprise Server voor SAP-toepassingen 12 waarmee u toodeploy nieuwe virtuele machines kunt.
Kunt u een van Hallo snel starten-sjablonen op github toodeploy alle vereiste bronnen. Hallo sjabloon implementeert Hallo virtuele machines, Hallo load balancer, beschikbaarheidsset enzovoort. Volg deze stappen toodeploy Hallo sjabloon:

1. Open Hallo [SAP-server de sjabloon] [ template-file-server] in hello Azure-portal   
1. Hallo volgende parameters opgeven
   1. Resource-voorvoegsel  
      Voer gewenste toouse Hallo-voorvoegsel in. Hallo-waarde wordt gebruikt als een voorvoegsel voor Hallo-resources die zijn geïmplementeerd.
   2. Type besturingssysteem  
      Selecteer een van de Linux-distributies Hallo. Selecteer voor dit voorbeeld SLES 12
   3. Gebruikersnaam van de beheerder en het wachtwoord van beheerder  
      Een nieuwe gebruiker gemaakt, dat de gebruikte toolog op toohello machine kunnen worden.
   4. Subnet-Id  
      Hallo-ID van Hallo subnet toowhich Hallo virtuele machines moet worden aangesloten. Laat leeg als u toocreate een nieuw virtueel netwerk wilt of subnet Hallo van uw VPN- of Express Route virtueel netwerk tooconnect Hallo virtuele machine tooyour on-premises netwerk selecteert. Hallo-ID meestal ziet eruit als /subscriptions/**&lt;abonnements-id&gt;**/resourceGroups/**&lt;Resourcegroepnaam&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;virtuele-netwerknaam&gt;**/subnets/**&lt;subnetnaam&gt;**

### <a name="installation"></a>Installeren

Hallo volgende items, worden voorafgegaan door een **[A]** -knooppunten van de toepasselijke tooall, **[1]** -alleen van toepassing toonode 1 of **[2]** -alleen van toepassing toonode 2.

1. **[A]**  SLES bijwerken

   <pre><code>
   sudo zypper update
   </code></pre>

1. **[1]**  Ssh toegang inschakelen

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. **[2]**  Ssh toegang inschakelen

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. **[1]**  Ssh toegang inschakelen

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. **[A]**  Installeren HA-uitbreiding
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. **[A]**  Hostnamen instellen   

   U kunt een DNS-server gebruiken of Hallo/etc/hosts op alle knooppunten wijzigen. Dit voorbeeld toont hoe toouse Hallo/etc/hosts-bestand.
   Hallo IP-adres en hostnaam in de volgende opdrachten Hallo Hallo vervangen

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   Invoegen Hallo regels te/etc/hosts te volgen. Uw omgeving voor het IP-adres en hostnaam toomatch Hallo wijzigen   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. **[1]**  Cluster installeren
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. **[2]**  Knooppunt toocluster toevoegen
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. **[A]**  Wijziging hacluster wachtwoord toohello hetzelfde wachtwoord

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. **[A]**  Configureren corosync toouse andere transport en nodelist toevoegen. Cluster werkt niet anders.
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   Hallo volgende vet inhoud toohello toevoegen.
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>prod-nfs-0</b>
      ring0_addr:10.0.0.5
     }
     node {
      # IP address of <b>prod-nfs-1</b>
      ring0_addr:10.0.0.6
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   Hallo corosync service opnieuw starten

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. **[A]**  Drbd-onderdelen installeren

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. **[A]**  Maken van een partitie voor Hallo drbd apparaat

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. **[A]**  Configuraties LVM maken

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. **[A]**  Maken Hallo NFS drbd apparaat

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   Hallo-configuratie voor Hallo nieuwe drbd apparaat en afsluiten invoegen

   <pre><code>
   resource <b>NWS</b>_nfs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>prod-nfs-0</b> {
         address   <b>10.0.0.5</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
      on <b>prod-nfs-1</b> {
         address   <b>10.0.0.6</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
   }
   </code></pre>

   Hallo drbd apparaat maken en start deze

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. **[1]**  Overslaan van de initiële synchronisatie

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. **[1]**  Set Hallo primaire knooppunt

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. **[1]**  Wacht totdat het Hallo nieuwe drbd apparaten worden gesynchroniseerd

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. **[1]**  Bestandssystemen op Hallo drbd apparaten maken

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a>Cluster-Framework configureren

1. **[1]**  Hello standaardinstellingen wijzigen

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Toevoegen Hallo NFS drbd toohello cluster apparaatconfiguratie

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_nfs \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_nfs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_nfs drbd_<b>NWS</b>_nfs \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Hello NFS-server maken

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Hello NFS File System resources maken

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive fs_<b>NWS</b>_sapmnt \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/srv/nfs/<b>NWS</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# group g-<b>NWS</b>_nfs fs_<b>NWS</b>_sapmnt

   crm(live)configure# order o-<b>NWS</b>_drbd_before_nfs inf: \
     ms-drbd_<b>NWS</b>_nfs:promote g-<b>NWS</b>_nfs:start
   
   crm(live)configure# colocation col-<b>NWS</b>_nfs_on_drbd inf: \
     g-<b>NWS</b>_nfs ms-drbd_<b>NWS</b>_nfs:Master

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Hello NFS exports maken

   <pre><code>
   sudo mkdir /srv/nfs/<b>NWS</b>/sidsys
   sudo mkdir /srv/nfs/<b>NWS</b>/sapmntsid
   sudo mkdir /srv/nfs/<b>NWS</b>/trans

   sudo crm configure

   crm(live)configure# primitive exportfs_<b>NWS</b> \
     ocf:heartbeat:exportfs \
     params directory="/srv/nfs/<b>NWS</b>" \
     options="rw,no_root_squash" \
     clientspec="*" fsid=0 \
     wait_for_leasetime_on_stop=true \
     op monitor interval="30s"

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add exportfs_<b>NWS</b>

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Een virtueel IP-resource en de statuscontrole voor Hallo interne load balancer maken

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive vip_<b>NWS</b>_nfs IPaddr2 \
     params ip=<b>10.0.0.4</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_nfs anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 610<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add nc_<b>NWS</b>_nfs
   crm(live)configure# modgroup g-<b>NWS</b>_nfs add vip_<b>NWS</b>_nfs

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

### <a name="create-stonith-device"></a>STONITH apparaat maken

Hallo STONITH apparaat maakt gebruik van een Service-Principal tooauthorize tegen Microsoft Azure. Volg deze stappen toocreate een Service-Principal.

1. Ga te<https://portal.azure.com>
1. Open hello Azure Active Directory-blade  
   Ga tooProperties en schrijf Hallo Directory-id. Dit is Hallo **tenant-id**.
1. Klik op App-registraties
1. Klik op Add.
1. Voer een naam, selecteer toepassingstype 'Web-app /-API, een aanmeldings-URL (bijvoorbeeld http://localhost) en klik op maken
1. Hallo aanmeldings-URL kan niet wordt gebruikt en geldige URL
1. Selecteer de nieuwe App Hallo en sleutels op in het tabblad Hallo-instellingen
1. Voer een beschrijving voor een nieuwe sleutel, selecteer 'Verloopt nooit' en klik op Opslaan
1. Schrijf Hallo waarde. Deze wordt gebruikt als Hallo **wachtwoord** voor Hallo Service-Principal
1. Schrijf Hallo toepassings-id. Deze wordt gebruikt als gebruikersnaam Hallo (**aanmeldings-id** in de onderstaande stappen voor Hallo) Hallo Service-Principal

Hallo Service-Principal heeft geen machtigingen tooaccess uw Azure-resources standaard. Moet u toogive Hallo Service-Principal machtigingen toostart en gestopt (toewijzing ongedaan maken) alle virtuele machines van Hallo-cluster.

1. Ga toohttps://portal.azure.com
1. Open de blade van alle resources Hallo
1. Selecteer Hallo virtuele machine
1. Klik op toegangsbeheer (IAM)
1. Klik op Add.
1. Selecteer Hallo rol eigenaar
1. Voer de naam Hallo van Hallo-toepassing die u hierboven hebt gemaakt
1. Klik op OK

#### <a name="1-create-hello-stonith-devices"></a>**[1]**  Hello STONITH apparaten maken

Nadat u machtigingen voor virtuele machines die Hallo Hallo bewerkt, kunt u Hallo STONITH apparaten kunt configureren in het Hallo-cluster.

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a>**[1]**  Hello gebruik van een apparaat STONITH inschakelen

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a>(A) SCS instellen

### <a name="deploying-linux"></a>Linux implementeren

Hello Azure Marketplace bevat een afbeelding voor SUSE Linux Enterprise Server voor SAP-toepassingen 12 waarmee u toodeploy nieuwe virtuele machines kunt. Hallo marketplace-installatiekopie bevat Hallo resource-agent voor SAP NetWeaver.

Kunt u een van Hallo snel starten-sjablonen op github toodeploy alle vereiste bronnen. Hallo sjabloon implementeert Hallo virtuele machines, Hallo load balancer, beschikbaarheidsset enzovoort. Volg deze stappen toodeploy Hallo sjabloon:

1. Open Hallo [ASC's / SCS Multi SID sjabloon] [ template-multisid-xscs] of Hallo [geconvergeerde sjabloon] [ template-converged] op Hallo Azure portal Hallo ASC's / SCS sjabloon alleen Hiermee maakt Hallo load balancing regels voor Hallo SAP NetWeaver ASC's / SCS en Ebruikers (alleen voor Linux)-exemplaren dat Hallo geconvergeerde sjabloon ook Hallo-taakverdeling regels voor een database (bijvoorbeeld Microsoft SQL Server of SAP HANA maakt). Als u van plan een SAP NetWeaver gebaseerd systeem tooinstall bent en u ook tooinstall Hallo database wilt op dezelfde machines hello, gebruikt u Hallo [geconvergeerde sjabloon][template-converged].
1. Hallo volgende parameters opgeven
   1. Resource-voorvoegsel (alleen ASC's / SCS Multi SID-sjabloon)  
      Voer gewenste toouse Hallo-voorvoegsel in. Hallo-waarde wordt gebruikt als een voorvoegsel voor Hallo-resources die zijn geïmplementeerd.
   3. SAP systeem-Id (alleen geconvergeerde sjabloon)  
      Voer Hallo SAP-systeem Id Hallo gewenste tooinstall SAP-systeem. Hallo-Id wordt gebruikt als een voorvoegsel voor Hallo-resources die zijn geïmplementeerd.
   4. Stack-Type  
      Hallo SAP NetWeaver stack-type selecteren
   5. Type besturingssysteem  
      Selecteer een van de Linux-distributies Hallo. Selecteer voor dit voorbeeld SLES 12 BYOS
   6. DB-Type  
      Selecteer HANA
   7. Grootte van het SAP  
      Hallo hoeveelheid SAP's Hallo nieuw systeem biedt. Als u niet zeker weet hoeveel SAP's Hallo systeem vereist is, vraag uw SAP-technologie Partner of System Integrator
   8. Beschikbaarheid van het systeem  
      Selecteer HA
   9. Gebruikersnaam van de beheerder en het wachtwoord van beheerder  
      Een nieuwe gebruiker gemaakt, dat de gebruikte toolog op toohello machine kunnen worden.
   10. Subnet-Id  
   Hallo-ID van Hallo subnet toowhich Hallo virtuele machines moet worden aangesloten.  Laat leeg als u toocreate een nieuw virtueel netwerk wilt of Selecteer hetzelfde subnet die u gebruikt of gemaakt als onderdeel van de NFS-serverimplementatie Hallo Hallo. Hallo-ID meestal ziet eruit als /subscriptions/**&lt;abonnements-id&gt;**/resourceGroups/**&lt;Resourcegroepnaam&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;virtuele-netwerknaam&gt;**/subnets/**&lt;subnetnaam&gt;**

### <a name="installation"></a>Installeren

Hallo volgende items, worden voorafgegaan door een **[A]** -knooppunten van de toepasselijke tooall, **[1]** -alleen van toepassing toonode 1 of **[2]** -alleen van toepassing toonode 2.

1. **[A]**  SLES bijwerken

   <pre><code>
   sudo zypper update
   </code></pre>

1. **[1]**  Ssh toegang inschakelen

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. **[2]**  Ssh toegang inschakelen

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. **[1]**  Ssh toegang inschakelen

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. **[A]**  Installeren HA-uitbreiding
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. **[A]**  Update SAP resource agents  
   
   Er is een fout opgetreden in een patch voor Hallo resource agents pakket vereist toouse Hallo nieuwe configuratie, die in dit artikel wordt beschreven. U kunt controleren als Hallo patch is al geïnstalleerd met de volgende opdracht Hallo

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   Hallo-uitvoer moet er ongeveer als

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   Als Hallo grep opdracht geen Hallo IS_ERS parameter vindt, moet u tooinstall Hallo patch vermeld op [Hallo SUSE downloadpagina](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. **[A]**  Hostnamen instellen   

   U kunt een DNS-server gebruiken of Hallo/etc/hosts op alle knooppunten wijzigen. Dit voorbeeld toont hoe toouse Hallo/etc/hosts-bestand.
   Hallo IP-adres en hostnaam in de volgende opdrachten Hallo Hallo vervangen

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   Invoegen Hallo regels te/etc/hosts te volgen. Uw omgeving voor het IP-adres en hostnaam toomatch Hallo wijzigen   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. **[1]**  Cluster installeren
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. **[2]**  Knooppunt toocluster toevoegen
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. **[A]**  Wijziging hacluster wachtwoord toohello hetzelfde wachtwoord

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. **[A]**  Configureren corosync toouse andere transport en nodelist toevoegen. Cluster werkt niet anders.
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   Hallo volgende vet inhoud toohello toevoegen.
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>nws-cl-0</b>
      ring0_addr:     10.0.0.14
     }
     node {
      # IP address of <b>nws-cl-1</b>
      ring0_addr:     10.0.0.13
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   Hallo corosync service opnieuw starten

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. **[A]**  Drbd-onderdelen installeren

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. **[A]**  Maken van een partitie voor Hallo drbd apparaat

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. **[A]**  Configuraties LVM maken

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. **[A]**  Maken Hallo SCS drbd apparaat

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   Hallo-configuratie voor Hallo nieuwe drbd apparaat en afsluiten invoegen

   <pre><code>
   resource <b>NWS</b>_ascs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
   }
   </code></pre>

   Hallo drbd apparaat maken en start deze

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. **[A]**  Maken Hallo Ebruikers drbd apparaat

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   Hallo-configuratie voor Hallo nieuwe drbd apparaat en afsluiten invoegen

   <pre><code>
   resource <b>NWS</b>_ers {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
   }
   </code></pre>

   Hallo drbd apparaat maken en start deze

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. **[1]**  Overslaan van de initiële synchronisatie

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. **[1]**  Set Hallo primaire knooppunt

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. **[1]**  Wacht totdat het Hallo nieuwe drbd apparaten worden gesynchroniseerd

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:93991268 nr:0 dw:93991268 dr:93944920 al:383 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 1: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:6047920 nr:0 dw:6047920 dr:6039112 al:34 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 2: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:5142732 nr:0 dw:5142732 dr:5133924 al:30 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. **[1]**  Bestandssystemen op Hallo drbd apparaten maken

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a>Cluster-Framework configureren

**[1]**  Hello standaardinstellingen wijzigen

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a>SAP NetWeaver installatie voorbereiden

1. **[A]**  Maken Hallo gedeelde mappen

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. **[A]**  Autofs configureren
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   Maak een bestand met

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   Opnieuw opstarten autofs toomount Hallo nieuwe shares

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. **[A]**  Bestand WISSELEN configureren
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   Opnieuw Hallo Agent tooactivate Hallo wijziging

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a>SAP NetWeaver ASC's / Ebruikers installeren

1. **[1]**  Een virtueel IP-resource en de statuscontrole voor Hallo interne load balancer maken

   <pre><code>
   sudo crm node standby <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ASCS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ascs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ASCS drbd_<b>NWS</b>_ASCS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ASCS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/usr/sap/<b>NWS</b>/ASCS<b>00</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ASCS IPaddr2 \
     params ip=<b>10.0.0.10</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ASCS anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 620<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0
   
   crm(live)configure# group g-<b>NWS</b>_ASCS nc_<b>NWS</b>_ASCS vip_<b>NWS</b>_ASCS fs_<b>NWS</b>_ASCS \
      meta resource-stickiness=3000

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ASCS inf: \
     ms-drbd_<b>NWS</b>_ASCS:promote g-<b>NWS</b>_ASCS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ASCS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ASCS:Master g-<b>NWS</b>_ASCS
   
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   Zorg ervoor dat de clusterstatus Hallo ok is en dat alle resources worden gestart. Het is niet belangrijk welke bronnen van de Hallo knooppunt worden uitgevoerd.

   <pre><code>
   sudo crm_mon -r

   # Node nws-cl-1: standby
   # <b>Online: [ nws-cl-0 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      Stopped: [ nws-cl-1 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   </code></pre>

1. **[1]**  SAP NetWeaver ASC's installeren  

   SAP NetWeaver ASC's installeren als hoofdmap op Hallo van de eerste knooppunt met behulp van een virtuele hostnaam die is toegewezen toohello IP-adres van de load balancer frontend-configuratie voor Hallo ASC's Hallo bijvoorbeeld <b>nws-ASC's</b>, <b>10.0.0.10</b>en Hallo exemplaarnummer die u voor de test Hallo Hallo load balancer bijvoorbeeld gebruikt <b>00</b>.

   U kunt Hallo sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow een niet-hoofdgebruiker tooconnect toosapinst gebruiken.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. **[1]**  Een virtueel IP-resource en de statuscontrole voor Hallo interne load balancer maken

   <pre><code>
   sudo crm node standby <b>nws-cl-0</b>
   sudo crm node online <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ERS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ers" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ERS drbd_<b>NWS</b>_ERS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ERS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd1 \
     directory=/usr/sap/<b>NWS</b>/ERS<b>02</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ERS IPaddr2 \
     params ip=<b>10.0.0.11</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ERS anything \
    params binfile="/usr/bin/nc" cmdline_options="-l -k 621<b>02</b>" \
    op monitor timeout=20s interval=10 depth=0

   crm(live)configure# group g-<b>NWS</b>_ERS nc_<b>NWS</b>_ERS vip_<b>NWS</b>_ERS fs_<b>NWS</b>_ERS

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ERS inf: \
     ms-drbd_<b>NWS</b>_ERS:promote g-<b>NWS</b>_ERS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ERS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ERS:Master g-<b>NWS</b>_ERS
   
   crm(live)configure# commit
   # WARNING: Resources nc_NWS_ASCS,nc_NWS_ERS,nc_NWS_nfs violate uniqueness for parameter "binfile": "/usr/bin/nc"
   # Do you still want toocommit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   Zorg ervoor dat de clusterstatus Hallo ok is en dat alle resources worden gestart. Het is niet belangrijk welke bronnen van de Hallo knooppunt worden uitgevoerd.

   <pre><code>
   sudo crm_mon -r

   # Node <b>nws-cl-0: standby</b>
   # <b>Online: [ nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   </code></pre>

1. **[2]**  SAP NetWeaver Ebruikers installeren  

   SAP NetWeaver Ebruikers installeren als hoofdmap op Hallo van de tweede knooppunt met behulp van een virtuele hostnaam die is toegewezen toohello IP-adres van de load balancer frontend-configuratie voor Hallo Ebruikers Hallo bijvoorbeeld <b>nws ebruikers</b>, <b>10.0.0.11</b> en Hallo exemplaarnummer die u voor de test Hallo Hallo load balancer bijvoorbeeld gebruikt <b>02</b>.

   U kunt Hallo sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow een niet-hoofdgebruiker tooconnect toosapinst gebruiken.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > Gebruik SWPM SP 20 PL 05 of hoger. Lagere versies Hallo machtigingen niet correct instelt en Hallo-installatie mislukt.
   > 

1. **[1]**  Hello ASC's / SCS en Ebruikers exemplaar profielen aanpassen
 
   * ASC's / SCS-profiel

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change hello restart command tooa start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add hello keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * Ebruikers profiel

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. **[A]**  Keep-Alive configureren

   Hallo-communicatie tussen Hallo SAP NetWeaver toepassingsserver en Hallo ASC's / SCS wordt via een software load balancer doorgestuurd. Hallo load balancer wordt niet-actieve verbindingen na een configureerbare time-out verbroken. tooprevent dit u moet een parameter in Hallo SAP NetWeaver ASC's / SCS profiel tooset en Hallo Linux systeeminstellingen wijzigen. Lees [SAP-notitie 1410736] [ 1410736] voor meer informatie.
   
   Hallo ASC's / SCS profiel parameter CLR niet/encni/set_so_keepalive is al toegevoegd in de laatste stap Hallo.

   <pre><code> 
   # Change hello Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. **[A]**  Hello SAP gebruikers na de installatie van de Hallo configureren
 
   <pre><code>
   # Add sidadm toohello haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. **[1]**  Hello ASC's en Ebruikers SAP services toohello sapservice bestand toevoegen

   Hallo ASC's service vermelding toohello tweede knooppunt en de kopie Hallo Ebruikers service vermelding toohello eerste knooppunt toevoegen.

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. **[1]**  Hello SAP-clusterbronnen maken

   <pre><code>
   sudo crm configure property maintenance-mode="true"

   sudo crm configure

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ASCS<b>00</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ASCS<b>00</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b>" \
    AUTOMATIC_RECOVER=false \
    meta resource-stickiness=5000 failure-timeout=60 migration-threshold=1 priority=10

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ERS<b>02</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ERS<b>02</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>" AUTOMATIC_RECOVER=false IS_ERS=true \
    meta priority=1000

   crm(live)configure# modgroup g-<b>NWS</b>_ASCS add rsc_sap_<b>NWS</b>_ASCS<b>00</b>
   crm(live)configure# modgroup g-<b>NWS</b>_ERS add rsc_sap_<b>NWS</b>_ERS<b>02</b>

   crm(live)configure# colocation col_sap_<b>NWS</b>_no_both -5000: g-<b>NWS</b>_ERS g-<b>NWS</b>_ASCS
   crm(live)configure# location loc_sap_<b>NWS</b>_failover_to_ers rsc_sap_<b>NWS</b>_ASCS<b>00</b> rule 2000: runs_ers_<b>NWS</b> eq 1
   crm(live)configure# order ord_sap_<b>NWS</b>_first_start_ascs Optional: rsc_sap_<b>NWS</b>_ASCS<b>00</b>:start rsc_sap_<b>NWS</b>_ERS<b>02</b>:stop symmetrical=false

   crm(live)configure# commit
   crm(live)configure# exit

   sudo crm configure property maintenance-mode="false"
   sudo crm node online <b>nws-cl-0</b>
   </code></pre>

   Zorg ervoor dat de clusterstatus Hallo ok is en dat alle resources worden gestart. Het is niet belangrijk welke bronnen van de Hallo knooppunt worden uitgevoerd.

   <pre><code>
   sudo crm_mon -r

   # Online: <b>[ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   </code></pre>

### <a name="create-stonith-device"></a>STONITH apparaat maken

Hallo STONITH apparaat maakt gebruik van een Service-Principal tooauthorize tegen Microsoft Azure. Volg deze stappen toocreate een Service-Principal.

1. Ga te<https://portal.azure.com>
1. Open hello Azure Active Directory-blade  
   Ga tooProperties en schrijf Hallo Directory-id. Dit is Hallo **tenant-id**.
1. Klik op App-registraties
1. Klik op Add.
1. Voer een naam, selecteer toepassingstype 'Web-app /-API, een aanmeldings-URL (bijvoorbeeld http://localhost) en klik op maken
1. Hallo aanmeldings-URL kan niet wordt gebruikt en geldige URL
1. Selecteer de nieuwe App Hallo en sleutels op in het tabblad Hallo-instellingen
1. Voer een beschrijving voor een nieuwe sleutel, selecteer 'Verloopt nooit' en klik op Opslaan
1. Schrijf Hallo waarde. Deze wordt gebruikt als Hallo **wachtwoord** voor Hallo Service-Principal
1. Schrijf Hallo toepassings-id. Deze wordt gebruikt als gebruikersnaam Hallo (**aanmeldings-id** in de onderstaande stappen voor Hallo) Hallo Service-Principal

Hallo Service-Principal heeft geen machtigingen tooaccess uw Azure-resources standaard. Moet u toogive Hallo Service-Principal machtigingen toostart en gestopt (toewijzing ongedaan maken) alle virtuele machines van Hallo-cluster.

1. Ga toohttps://portal.azure.com
1. Open de blade van alle resources Hallo
1. Selecteer Hallo virtuele machine
1. Klik op toegangsbeheer (IAM)
1. Klik op Add.
1. Selecteer Hallo rol eigenaar
1. Voer de naam Hallo van Hallo-toepassing die u hierboven hebt gemaakt
1. Klik op OK

#### <a name="1-create-hello-stonith-devices"></a>**[1]**  Hello STONITH apparaten maken

Nadat u machtigingen voor virtuele machines die Hallo Hallo bewerkt, kunt u Hallo STONITH apparaten kunt configureren in het Hallo-cluster.

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a>**[1]**  Hello gebruik van een apparaat STONITH inschakelen

Hallo-gebruik van een apparaat STONITH inschakelen

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a>Installeren van de database

In dit voorbeeld is een SAP HANA System Replication geïnstalleerd en geconfigureerd. SAP HANA in hetzelfde cluster als Hallo SAP NetWeaver ASC's / SCS en Ebruikers Hallo uitgevoerd. U kunt ook een SAP HANA installeren op een cluster toegewezen. Zie [hoge beschikbaarheid van SAP HANA op Azure Virtual Machines (VM's)] [ sap-hana-ha] voor meer informatie.

### <a name="prepare-for-sap-hana-installation"></a>Voorbereiden voor SAP HANA-installatie

In het algemeen wordt aangeraden met LVM voor volumes die bij het opslaan van gegevens en logboekbestanden. U kunt ook toostore Hallo gegevens en logboekbestanden bestand rechtstreeks op een gewone schijf kiezen voor testdoeleinden.

1. **[A]**  LVM  
   Hallo in het volgende voorbeeld wordt ervan uitgegaan dat Hallo virtuele machines vier gegevensschijven gekoppeld die gebruikt toocreate twee volumes worden moeten.
   
   Fysieke volumes voor alle schijven die u toouse wilt maken.
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   Een volume-groep voor gegevensbestanden hello, één volume groep Hallo-logboekbestanden en één voor de gedeelde map Hallo van SAP HANA maken
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   Hallo logische volumes maken
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   Hallo koppelpunt mappen maken en kopieer Hallo UUID van alle logische volumes
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   Autofs vermeldingen voor Hallo drie logische volumes maken
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   Deze regel toosudo vi /etc/auto.direct invoegen
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   Hallo nieuwe volumes koppelen
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. **[A]**  Gewone schijven  

   Voor kleine of demo-systemen, kunt u uw bestanden HANA gegevens en logboekbestanden op één schijf plaatsen. Hallo volgende opdrachten een partitie maken op /dev/sdc en formatteert u het met xfs.
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down hello id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   Deze regel too/etc/auto.direct invoegen
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   Hallo doelmap maken en Hallo schijf koppelen.
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a>SAP HANA installeren

Hallo volgende stappen zijn gebaseerd op hoofdstuk 4 Hallo [SAP HANA SR prestaties geoptimaliseerd Scenario handleiding] [ suse-hana-ha-guide] tooinstall SAP HANA System Replication. Lees dit voordat u Hallo-installatie doorgaat.

1. **[A]**  Hdblcm vanaf HANA DVD hello uitvoeren
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. **[A]**  SAP Hostagent bijwerken

   Hallo nieuwste SAP Hostagent archief downloaden van Hallo [SAP Softwarecenter] [ sap-swcenter] en uitvoeren hello na de opdracht tooupgrade Hallo agent. Hallo pad toohello archief toopoint toohello door u gedownloade bestand vervangen.
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path tooSAP Host Agent SAR&gt;</b> 
   </code></pre>

1. **[1]**  Maken HANA-replicatie (als root)  

   Hallo volgende opdracht worden uitgevoerd. Zorg ervoor dat tooreplace vet tekenreeksen (HANA systeem-ID HDB en exemplaar getal 03) met Hallo waarden van de SAP HANA-installatie.
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. **[A]**  Keystore-vermelding (als root) maken

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. **[1]**  Backup database (als root)

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. **[1]**  Toohello HANA sapsid gebruiker wisselen en maak Hallo primaire site.

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. **[2]**  Toohello HANA sapsid gebruiker wisselen en Hallo secundaire site maken.

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. **[1]**  Clusterbronnen SAP HANA maken

   Maak eerst Hallo-topologie.
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number and HANA system id
   
   crm(live)configure# primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b>   ocf:suse:SAPHanaTopology \
     operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
     op monitor interval="10" timeout="600" \
     op start interval="0" timeout="600" \
     op stop interval="0" timeout="300" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"
    
   crm(live)configure# clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>
   
   Maak vervolgens Hallo HANA resources
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
    
   crm(live)configure# primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
     operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
     op start interval="0" timeout="3600" \
     op stop interval="0" timeout="3600" \
     op promote interval="0" timeout="3600" \
     op monitor interval="60" role="Master" timeout="700" \
     op monitor interval="61" role="Slave" timeout="700" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
     DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"
    
   crm(live)configure# ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
     target-role="Started" interleave="true"
    
   crm(live)configure# primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
     meta target-role="Started" is-managed="true" \ 
     operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
     op monitor interval="10s" timeout="20s" \ 
     params ip="<b>10.0.0.12</b>" 

   crm(live)configure# primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
     params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
     op monitor timeout=20s interval=10 depth=0 

   crm(live)configure# group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  

   crm(live)configure# order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   Zorg ervoor dat de clusterstatus Hallo ok is en dat alle resources worden gestart. Het is niet belangrijk welke bronnen van de Hallo knooppunt worden uitgevoerd.

   <pre><code>
   sudo crm_mon -r

   # <b>Online: [ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Clone Set: cln_SAPHanaTopology_HDB_HDB03 [rsc_SAPHanaTopology_HDB_HDB03]
   #      <b>Started: [ nws-cl-0 nws-cl-1 ]</b>
   #  Master/Slave Set: msl_SAPHana_HDB_HDB03 [rsc_SAPHana_HDB_HDB03]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g_ip_HDB_HDB03
   #      rsc_ip_HDB_HDB03   (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      rsc_nc_HDB_HDB03   (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   # rsc_st_azure_1  (stonith:fence_azure_arm):      <b>Started nws-cl-0</b>
   # rsc_st_azure_2  (stonith:fence_azure_arm):      <b>Started nws-cl-1</b>
   </code></pre>

1. **[1]**  Installatie Hallo SAP NetWeaver database-exemplaar

   Installatie Hallo SAP NetWeaver database-exemplaar als hoofdmap met behulp van een virtuele hostnaam die is toegewezen toohello IP-adres van de load balancer frontend-configuratie voor de database Hallo Hallo bijvoorbeeld <b>nws-db</b> en <b>10.0.0.12</b>.

   U kunt Hallo sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow een niet-hoofdgebruiker tooconnect toosapinst gebruiken.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a>SAP NetWeaver application server-installatie

Volg deze stappen tooinstall een SAP-toepassingsserver. Hallo stappen onderstaande wordt ervan uitgegaan dat u de toepassingsserver Hallo op een server die verschilt van Hallo ASC's / SCS en HANA servers installeert. Anders zijn bepaalde Hallo stappen hieronder (zoals het configureren van hostnamen) niet nodig.

1. Setup van hostnaamomzetting    
   U kunt een DNS-server gebruiken of Hallo/etc/hosts op alle knooppunten wijzigen. Dit voorbeeld toont hoe toouse Hallo/etc/hosts-bestand.
   Hallo IP-adres en hostnaam in de volgende opdrachten Hallo Hallo vervangen
   ```bash
   sudo vi /etc/hosts
   ```
   Invoegen Hallo regels te/etc/hosts te volgen. Uw omgeving voor het IP-adres en hostnaam toomatch Hallo wijzigen    
    
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of hello application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. Hallo sapmnt map maken

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. Autofs configureren
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   Maak een nieuw bestand met

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   Opnieuw opstarten autofs toomount Hallo nieuwe shares

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. Wisselbestand configureren
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   Opnieuw Hallo Agent tooactivate Hallo wijziging

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. SAP NetWeaver application server installeren

   Een primaire of extra SAP NetWeaver toepassingsserver installeren.

   U kunt Hallo sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow een niet-hoofdgebruiker tooconnect toosapinst gebruiken.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. SAP HANA secure store bijwerken

   Update Hallo SAP HANA beveiligde toopoint toohello virtuele naam van Hallo SAP HANA System replicatie-instellingen opslaan.
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a>Volgende stappen
* [Azure virtuele Machines, planning en implementatie voor SAP][planning-guide]
* [Azure virtuele Machines-implementatie voor SAP][deployment-guide]
* [Azure virtuele Machines DBMS-implementatie voor SAP][dbms-guide]
* hoe tooestablish hoge beschikbaarheid en herstel na noodgevallen van SAP HANA plannen in Azure (grote exemplaren), Zie toolearn [SAP HANA (grote exemplaren) hoge beschikbaarheid en herstel na noodgevallen op Azure](hana-overview-high-availability-disaster-recovery.md).
* hoe tooestablish hoge beschikbaarheid en herstel na noodgevallen van SAP HANA plannen op Azure Virtual machines, Zie toolearn [hoge beschikbaarheid van SAP HANA op Azure Virtual Machines (VM's)][sap-hana-ha]
