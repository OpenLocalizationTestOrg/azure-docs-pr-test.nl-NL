---
title: aaaHigh beschikbaarheid van SAP HANA op Azure Virtual Machines (VM's) | Microsoft Docs
description: Hoge beschikbaarheid van SAP HANA op Azure virtuele Machines (VM's) maken.
services: virtual-machines-linux
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: sedusch
ms.openlocfilehash: dcb9bb70594f9d97f8a888cec76300bcbe0bf1ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a>Hoge beschikbaarheid van SAP HANA op Azure virtuele Machines (VM's)

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

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

On-premises kunt u beide HANA System-replicatie gebruiken of gedeelde opslag tooestablish hoge beschikbaarheid voor SAP HANA.
Wordt alleen ondersteund HANA System Replication instellen in Azure. SAP HANA replicatie bestaat uit één hoofdknooppunt en ten minste één slave knooppunt. Wijzigingen toohello gegevens op het hoofdknooppunt Hallo zijn gerepliceerd toohello slave knooppunten synchroon of asynchroon.

Dit artikel wordt beschreven hoe toodeploy Hallo virtuele machines Hallo virtuele machines configureren, Hallo cluster framework hebt geïnstalleerd, installeren en configureren SAP HANA System Replication.
Installatie opdrachten enzovoort exemplaarnummer 03 in Hallo Voorbeeldconfiguraties en HANA systeem-ID HDB wordt gebruikt.

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
* [SAP HANA SR prestaties geoptimaliseerd Scenario] [ suse-hana-ha-guide] Hallo handleiding bevat alle vereiste gegevens tooset van SAP HANA System Replication on-premises. Deze handleiding gebruiken als basislijn.

## <a name="deploying-linux"></a>Linux implementeren

Hallo resource agent voor SAP HANA is opgenomen in SUSE Linux Enterprise Server voor SAP-toepassingen.
Hello Azure Marketplace bevat een afbeelding voor SUSE Linux Enterprise Server voor SAP-toepassingen 12 met BYOS (uw eigen abonnement Bring) waarmee u toodeploy nieuwe virtuele machines kunt.

### <a name="manual-deployment"></a>Handmatige implementatie

1. Een resourcegroep maken
1. Een virtueel netwerk maken
1. Twee Storage-Accounts maken
1. Een Beschikbaarheidsset maken  
   De maximale updatedomein instellen
1. Maak een Load Balancer (intern)  
   Selecteer VNET van de bovenstaande stap
1. Virtuele Machine 1 maken  
   https://Portal.Azure.com/#Create/SUSE-byos.SLES-for-SAP-byos12-SP1  
   SLES voor SAP toepassingen 12 SP1 (BYOS)  
   Selecteer de Storage-Account 1  
   Beschikbaarheidsset selecteren  
1. Virtuele Machine 2 maken  
   https://Portal.Azure.com/#Create/SUSE-byos.SLES-for-SAP-byos12-SP1  
   SLES voor SAP toepassingen 12 SP1 (BYOS)  
   Selecteer Opslagaccount 2   
   Beschikbaarheidsset selecteren  
1. Gegevensschijven toevoegen
1. Hallo load balancer configureren
    1. Een frontend-IP-adresgroep maken
        1. Hallo load balancer te openen, selecteer frontend-IP-adresgroep en klik op toevoegen
        1. Voer de naam Hallo van Hallo nieuwe frontend IP-adresgroep (bijvoorbeeld hana-frontend)
       1. Klik op OK
        1. Na het Hallo nieuwe frontend-IP-adresgroep is gemaakt, noteer de IP-adres
    1. Een back endpool maken
        1. Hallo load balancer te openen, selecteer back-endpools en klikt u op toevoegen
        1. Voer de naam Hallo van Hallo nieuwe back-endpool (bijvoorbeeld hana-back-end)
        1. Klik op een virtuele machine toevoegen
        1. Selecteer Hallo Beschikbaarheidsset u eerder hebt gemaakt
        1. Selecteer de virtuele machines Hallo van Hallo SAP HANA-cluster
        1. Klik op OK
    1. Een health test maken
       1. Hallo load balancer openen, selecteer statuscontroles en klikt u op toevoegen
        1. Voer de naam Hallo van Hallo nieuwe health test (bijvoorbeeld hana-hp)
        1. Selecteer TCP als protocol, poort 625**03**, houd Interval 5 en de drempelwaarde voor onjuiste status 2
        1. Klik op OK
    1. Taakverdelingsregels maken
        1. Open Hallo load balancer en taakverdelingsregels Selecteer klikt u op toevoegen
        1. Voer Hallo-naam van de nieuwe regel voor load balancer hello (bijvoorbeeld hana-lb-3**03**15)
        1. Selecteer Hallo frontend-IP-adres, back-endpool en health test u eerder hebt gemaakt (bijvoorbeeld hana-frontend)
        1. Protocol TCP houden, voert u poort 3**03**15
        1. Minuten van inactiviteit too30 verhogen
       1. **Zorg ervoor dat tooenable zwevend IP**
        1. Klik op OK
        1. Hallo bovenstaande stappen herhalen voor poort 3**03**17

### <a name="deploy-with-template"></a>Implementeren met sjabloon
Kunt u een van Hallo snel starten-sjablonen op github toodeploy alle vereiste bronnen. Hallo sjabloon implementeert Hallo virtuele machines, Hallo load balancer, beschikbaarheidsset enzovoort. Volg deze stappen toodeploy Hallo sjabloon:

1. Open Hallo [databasesjabloon] [ template-multisid-db] of Hallo [geconvergeerde sjabloon] [ template-converged] op Hallo Azure Portal maakt Hallo databasesjabloon alleen Hallo regels voor taakverdeling voor een database hello terwijl Hallo geconvergeerde sjabloon ook maakt taakverdeling regels voor een ASC's / SCS en Ebruikers (alleen voor Linux)-exemplaar. Als u van plan een SAP NetWeaver gebaseerd systeem tooinstall bent en u ook tooinstall Hallo wilt ASC's / SCS exemplaar op Hallo dezelfde machines, gebruik Hallo [geconvergeerde sjabloon][template-converged].
1. Hallo volgende parameters opgeven
    1. SAP-systeem-Id  
       Voer Hallo SAP-systeem Id Hallo gewenste tooinstall SAP-systeem. Hallo-Id wordt gebruikt als een voorvoegsel voor Hallo-resources die zijn geïmplementeerd.
    1. Stack-Type (alleen van toepassing als u Hallo geconvergeerde sjabloon gebruikt)  
       Hallo SAP NetWeaver stack-type selecteren
    1. Type besturingssysteem  
       Selecteer een van de Linux-distributies Hallo. Selecteer voor dit voorbeeld SLES 12 BYOS
    1. DB-Type  
       Selecteer HANA
    1. Grootte van het SAP  
       Hallo hoeveelheid SAP's Hallo nieuw systeem bieden. Als u niet zeker weet hoeveel SAP's Hallo systeem is vereist, vraag uw SAP-technologie Partner of System Integrator
    1. Beschikbaarheid van het systeem  
       Selecteer HA
    1. Gebruikersnaam van de beheerder en het wachtwoord van beheerder  
       Een nieuwe gebruiker gemaakt, dat de gebruikte toolog op toohello machine kunnen worden.
    1. Nieuwe of bestaande Subnet  
       Bepaalt of een nieuw virtueel netwerk en subnet moeten worden gemaakt of een bestaand subnet moet worden gebruikt. Als u al een virtueel netwerk dat is verbonden tooyour on-premises netwerk hebt, selecteert u de bestaande.
    1. Subnet-Id  
    Hallo-ID van Hallo subnet toowhich Hallo virtuele machines moet worden aangesloten. Selecteer subnet Hallo van uw VPN- of Express Route virtueel netwerk tooconnect Hallo virtuele machine tooyour on-premises netwerk. Hallo-ID meestal ziet eruit als /subscriptions/`<subscription id`> /resourceGroups/`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`>

## <a name="setting-up-linux-ha"></a>Instellen van Linux HA

Hallo volgende items worden voorafgegaan door een [A] - knooppunten van de toepasselijke tooall, [1] - alleen van toepassing toonode 1 of [2] - alleen van toepassing toonode 2.

1. [A] SLES voor SAP BYOS alleen - registreren SLES toobe kunnen toouse Hallo opslagplaatsen
1. [A] SLES voor SAP BYOS alleen - toevoegen openbare cloud module
1. [A] SLES bijwerken
    ```bash
    sudo zypper update

    ```

1. [1] ssh toegang inschakelen
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. [2] ssh toegang inschakelen
    ```bash
    sudo ssh-keygen -tdsa

    # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. [1] ssh toegang inschakelen
    ```bash
    # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. [A] HA-uitbreiding installeren
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. [A] indeling van setup-schijf
    1. LVM  
    In het algemeen wordt aangeraden toouse LVM voor volumes die bij het opslaan van gegevens en logboekbestanden. Hallo in het volgende voorbeeld wordt ervan uitgegaan dat Hallo virtuele machines vier gegevensschijven gekoppeld die gebruikt toocreate twee volumes worden moeten.
        * Fysieke volumes voor alle schijven die u toouse wilt maken.
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * Een volume-groep voor gegevensbestanden hello, één volume groep Hallo-logboekbestanden en één voor de gedeelde map Hallo van SAP HANA maken
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * Hallo logische volumes maken
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * Hallo koppelpunt mappen maken en kopieer Hallo UUID van alle logische volumes
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * Fstab-vermeldingen voor Hallo drie logische volumes maken
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    Deze regel te/etc/fstab invoegen
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * Hallo nieuwe volumes koppelen
    <pre><code>
    sudo mount -a
    </code></pre>
    1. Gewone schijven  
       Voor kleine of demo-systemen, kunt u uw bestanden HANA gegevens en logboekbestanden op één schijf plaatsen. Hallo volgende opdrachten een partitie maken op /dev/sdc en formatteert u het met xfs.
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-hello-id-of-devsdc1"></a>Schrijf Hallo-id van /dev/sdc1
    sudo/sbin/blkid sudo vi/etc/fstab-fouten
    ```

    Insert this line too/etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create hello target directory and mount hello disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. [A] setup hostnaamomzetting voor alle hosts  
    U kunt een DNS-server gebruiken of Hallo/etc/hosts op alle knooppunten wijzigen. Dit voorbeeld toont hoe toouse Hallo/etc/hosts-bestand.
   Hallo IP-adres en hostnaam in de volgende opdrachten Hallo Hallo vervangen
    ```bash
    sudo vi /etc/hosts
    ```
    Invoegen Hallo regels te/etc/hosts te volgen. Uw omgeving voor het IP-adres en hostnaam toomatch Hallo wijzigen    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. [1] Cluster installeren
    ```bash
    sudo ha-cluster-init
    
    # Do you want toocontinue anyway? [y/N] -> y
    # Network address toobind too(e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish toouse SBD? [y/N] -> N
    # Do you wish tooconfigure an administration IP? [y/N] -> N
    ```
        
1. [2] knooppunt toocluster toevoegen
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured toostart at system boot.
    # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
    # Do you want toocontinue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. [A] wijziging hacluster wachtwoord toohello hetzelfde wachtwoord
    ```bash
    sudo passwd hacluster
    
    ```

1. [A] configureren corosync toouse andere transport en nodelist toevoegen. Cluster werkt niet anders.
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

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
        ring0_addr:     < ip address of node 1 >
      }
      node {
        ring0_addr:     < ip address of node 2 > 
      } 
    }</b>
    logging {
      [...]
    </code></pre>

    Hallo corosync service opnieuw starten

    ```bash
    sudo service corosync restart
    
    ```

1. [A] HANA HA-pakketten installeren  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a>SAP HANA installeren

Ga als volgt hoofdstuk 4 Hallo [SAP HANA SR prestaties geoptimaliseerd Scenario handleiding] [ suse-hana-ha-guide] tooinstall SAP HANA System Replication.

1. [A] hdblcm vanaf HANA DVD hello uitvoeren
    * Installatie te kiezen,-1 >
    * Selecteer extra onderdelen voor installatie-1 >
    * Voer installatiepad [/ hana/gedeelde]: ENTER ->
    * Voer de naam van de lokale Host [.]: -> ENTER
    * Wilt u tooadd extra hosts toohello system? (j/n) [n]: ENTER ->
    * Voer SAP HANA systeem-ID:<SID of HANA e.g. HDB>
    * Voer exemplaarnummer [00]:   
  HANA exemplaarnummer. 03 gebruiken als u hello Azure-sjabloon gebruikt of gevolgd Hallo in bovenstaand voorbeeld
    * Selecteer Database modus / Index [1] op Enter: -> ENTER
    * Selecteer systeemgebruik / Voer Index [4]:  
  Selecteer Hallo systeem gebruik
    * Geef de locatie van gegevensvolumes [/ data/hana/HDB]: ENTER ->
    * Geef de locatie van Logboekvolumes [/ log/hana/HDB]: ENTER ->
    * Maximale geheugentoewijzing beperken? [n]: ENTER ->
    * Geef '...' Host-naam van het certificaat voor Host [...]: ENTER ->
    * Voer SAP Host Agent gebruiker (sapadm) wachtwoord:
    * SAP Host Agent gebruiker (sapadm) wachtwoord bevestigen:
    * Voer de systeembeheerder (hdbadm) wachtwoord:
    * Systeembeheerder (hdbadm) wachtwoord bevestigen:
    * Voer systeembeheerder basismap [/ usr/sap/HDB/home]: ENTER ->
    * Voer systeembeheerder aanmeldingsshell [/ bin/servicel]: ENTER ->
    * Voer systeembeheerder gebruikers-ID [1001]: -> ENTER
    * Voer-ID van gebruikersgroep (sapsys) [79]: ENTER ->
    * Geef het wachtwoord voor Database gebruiker (systeem):
    * Bevestig Database gebruikerswachtwoord (systeem):
    * Systeem opnieuw opstarten nadat de computer opnieuw is opgestart? [n]: ENTER ->
    * Wilt u toocontinue? (j/n):  
  Hallo samenvatting valideren en y toocontinue invoeren
1. [A] SAP Hostagent bijwerken  
  Hallo nieuwste SAP Hostagent archief downloaden van Hallo [SAP Softwarecenter] [ sap-swcenter] en uitvoeren hello na de opdracht tooupgrade Hallo agent. Hallo pad toohello archief toopoint toohello door u gedownloade bestand vervangen.
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path tooSAP Host Agent SAR>
    ```

1. [1] HANA replicatie maken (als root)  
    Hallo volgende opdracht worden uitgevoerd. Zorg ervoor dat tooreplace vet tekenreeksen (HANA systeem-ID HDB en exemplaar getal 03) met Hallo waarden van de SAP HANA-installatie.
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. [A] keystore-vermelding maken (als root)
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. [1] back-updatabase (als root)
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. [1] toohello sapsid gebruiker (bijvoorbeeld hdbadm) switch en maak Hallo primaire site.
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. [2] overschakelen toohello sapsid gebruiker (bijvoorbeeld hdbadm) en Hallo secundaire site maken.
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a>Cluster-Framework configureren

Hallo standaardinstellingen wijzigen

<pre>
sudo vi crm-defaults.txt
# enter hello following toocrm-defaults.txt
<code>
property $id="cib-bootstrap-options" \
  no-quorum-policy="ignore" \
  stonith-enabled="true" \
  stonith-action="reboot" \
  stonith-timeout="150s"
rsc_defaults $id="rsc-options" \
  resource-stickiness="1000" \
  migration-threshold="5000"
op_defaults $id="op-options" \
  timeout="600"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>Nu laden we Hallo toohello bestandscluster
sudo crm load update crm-defaults.txt configureren
</pre>

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

Nadat u machtigingen voor virtuele machines die Hallo Hallo bewerkt, kunt u Hallo STONITH apparaten kunt configureren in het Hallo-cluster.

<pre>
sudo vi crm-fencing.txt
# enter hello following toocrm-fencing.txt
# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>Nu laden we Hallo toohello bestandscluster
sudo crm load update crm-fencing.txt configureren
</pre>

### <a name="create-sap-hana-resources"></a>SAP HANA-resources maken

<pre>
sudo vi crm-saphanatop.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number and HANA system id
<code>
primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHanaTopology \
    operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
    op monitor interval="10" timeout="600" \
    op start interval="0" timeout="600" \
    op stop interval="0" timeout="300" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"

clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>Nu laden we Hallo toohello bestandscluster
sudo crm load update crm-saphanatop.txt configureren
</pre>

<pre>
sudo vi crm-saphana.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
<code>
primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
    operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
    op start interval="0" timeout="3600" \
    op stop interval="0" timeout="3600" \
    op promote interval="0" timeout="3600" \
    op monitor interval="60" role="Master" timeout="700" \
    op monitor interval="61" role="Slave" timeout="700" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
    DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"

ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
    target-role="Started" interleave="true"

primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
    meta target-role="Started" is-managed="true" \ 
    operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
    op monitor interval="10s" timeout="20s" \ 
    params ip="<b>10.0.0.21</b>" 
primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
    params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
    op monitor timeout=20s interval=10 depth=0 
group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
 
colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  
order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>Nu laden we Hallo toohello bestandscluster
sudo crm load update crm-saphana.txt configureren
</pre>

### <a name="test-cluster-setup"></a>Test-cluster instellen
Hallo volgende hoofdstuk wordt beschreven hoe u uw instellingen kunt testen. Elke test wordt ervan uitgegaan dat u hoofdmap en Hallo SAP HANA-master wordt uitgevoerd op Hallo virtuele machine saphanavm1.

#### <a name="fencing-test"></a>Hekwerk Test

Hallo-setup van Hallo hekwerk agent kunt u testen door de netwerkinterface Hallo op knooppunt saphanavm1 uit te schakelen.

<pre><code>
sudo ifdown eth0
</code></pre>

Hallo virtuele machine moet nu ophalen opnieuw gestart of gestopt, afhankelijk van uw clusterconfiguratie.
Als u Hallo stonith actie toooff instelt, Hallo virtuele machine wordt gestopt en Hallo bronnen gemigreerde toohello virtuele machine wordt uitgevoerd.

Zodra u Hallo virtuele machine opnieuw start, Hallo SAP HANA-resource toostart als secundaire zal mislukken als u AUTOMATED_REGISTER instellen = "false". In dit geval moet u tooconfigure Hallo HANA exemplaar als secundaire door het uitvoeren van de volgende opdracht Hallo:

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a>Een handmatige failover testen

U kunt een handmatige failover testen Hallo pacemaker heeft door service te stoppen op knooppunt saphanavm1.
<pre><code>
service pacemaker stop
</code></pre>

U kunt Hallo-service opnieuw starten na een failover Hallo. Hallo SAP HANA-bron op saphanavm1 toostart als secundaire zal mislukken als u AUTOMATED_REGISTER instellen = "false". In dit geval moet u tooconfigure Hallo HANA exemplaar als secundaire door het uitvoeren van de volgende opdracht Hallo:

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a>Een migratie testen

U kunt Hallo SAP HANA-hoofdknooppunt migreren door het uitvoeren van de volgende opdracht Hallo
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

Dit moet migreren Hallo SAP HANA-hoofdknooppunt en Hallo-groep die Hallo virtuele IP-adres toosaphanavm2 bevat.
Hallo SAP HANA-bron op saphanavm1 toostart als secundaire zal mislukken als u AUTOMATED_REGISTER instellen = "false". In dit geval moet u tooconfigure Hallo HANA exemplaar als secundaire door het uitvoeren van de volgende opdracht Hallo:

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

Hallo migratie maakt locatie beperkingen die toobe opnieuw verwijderd moeten.

<pre><code>
crm configure edited

# delete location contraints that are named like hello following contraint. You should have two contraints, one for hello SAP HANA resource and one for hello IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

U moet ook toocleanup Hallo status van Hallo secundair knooppunt resource

<pre><code>
# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a>Volgende stappen
* [Azure virtuele Machines, planning en implementatie voor SAP][planning-guide]
* [Azure virtuele Machines-implementatie voor SAP][deployment-guide]
* [Azure virtuele Machines DBMS-implementatie voor SAP][dbms-guide]
* hoe tooestablish hoge beschikbaarheid en herstel na noodgevallen van SAP HANA plannen in Azure (grote exemplaren), Zie toolearn [SAP HANA (grote exemplaren) hoge beschikbaarheid en herstel na noodgevallen op Azure](hana-overview-high-availability-disaster-recovery.md). 
