---
title: aaaAzure Linux VM-Agent overzicht | Microsoft Docs
description: Meer informatie over hoe tooinstall en Linux-Agent (waagent) toomanage interactie van de virtuele machine met Azure-Infrastructuurcontroller configureren.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4e08c84d9205f4db7aae6fd1568ec1f15fba395c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-and-using-hello-azure-linux-agent"></a>Uitleg en het gebruik van hello Azure Linux Agent
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a>Inleiding
Hallo Microsoft Azure Linux Agent beheert (waagent) Linux en FreeBSD inrichting en VM interactie met hello Azure-Infrastructuurcontroller. Hallo functionaliteit voor Linux en FreeBSD IaaS-implementaties volgende bevat:

> [!NOTE]
> Zie hello Azure Linux agent [Leesmij](https://github.com/Azure/WALinuxAgent/blob/master/README.md) voor meer informatie.
> 
> 

* **Afbeelding inrichten**
  
  * Het maken van een gebruikersaccount
  * SSH-verificatietypen configureren
  * Implementatie van openbare SSH-sleutels en sleutelparen
  * Hallo host-naam van de instelling
  * Publishing Hallo naam toohello hostplatform DNS
  * SSH host vingerafdruk sleutel toohello rapportageplatform
  * Resource Schijfbeheer
  * Opmaak en Hallo resource schijf koppelen
  * Wisselruimte configureren
* **Netwerken**
  
  * Routes tooimprove compatibiliteit met platform DHCP-servers beheert
  * Zorgt ervoor Hallo stabiliteit van de naam voor de netwerkinterface Hallo
* **Kernel**
  
  * Hiermee configureert u virtuele NUMA (uitschakelen voor kernel < 2.6.37)
  * Hyper-V entropie voor /dev/random verbruikt
  * Hiermee configureert u de SCSI-outs voor Hallo basis-apparaat (die mogelijk externe)
* **Diagnostics**
  
  * Console omleiding toohello seriële poort
* **SCVMM-implementaties**
  
  * Detecteert en Hallo VMM-agent voor Linux bootstraps wanneer in een omgeving met System Center Virtual Machine Manager 2012 R2 wordt uitgevoerd
* **VM-extensie**
  
  * Onderdeel geschreven door Microsoft en Partners in Linux VM (IaaS) tooenable en configuratie automation invoeren
  * Implementatie van de VM-extensie verwijzing op [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)

## <a name="communication"></a>Communicatie
de informatiestroom Hallo Hallo platform toohello agent gebeurt via twee kanalen:

* Een opstarttijd gekoppeld DVD voor IaaS-implementaties. Deze DVD bevat een OVF-compatibele configuratiebestand dat alle Inrichtingsgegevens dan de werkelijke SSH keypairs Hallo bevat.
* Een TCP-eindpunt blootstellen van een REST-API gebruikt tooobtain implementatie en topologieconfiguratie.

## <a name="requirements"></a>Vereisten
Hallo volgende systemen zijn getest en staan bekend toowork Hello Azure Linux Agent:

> [!NOTE]
> Deze lijst kan afwijken van Hallo officiële lijst van ondersteunde systemen op Hallo van Microsoft Azure-Platform, zoals hier wordt beschreven: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)
> 
> 

* CoreOS
* CentOS 6.3 +
* Red Hat Enterprise Linux 6.7 +
* Debian 7.0 +
* Ubuntu 12.04 +
* openSUSE 12.3 +
* SLES 11 SP3 +
* Oracle Linux 6.4 +

Andere ondersteunde systemen:

* FreeBSD 10 + (Azure Linux Agent v2.0.10 +)

Hallo Linux-agent is afhankelijk van sommige systeempakketten in volgorde toofunction goed de:

* Python 2.6 +
* OpenSSL 1.0 +
* OpenSSH 5.3 +
* Hulpprogramma's voor FileSystem: sfdisk fdisk, mkfs, gescheiden
* Hulpprogramma's voor wachtwoord: chpasswd, sudo
* Tekst voor het verwerken van hulpprogramma's: ype, grep
* Hulpprogramma's voor netwerk: IP-route
* Kernel-ondersteuning voor het koppelen van de UDF-bestandssystemen.

## <a name="installation"></a>Installeren
Installatie met een RPM of een pakket DEB vanuit uw distributiepunt pakket opslagplaats is Hallo voorkeurs-methode voor het installeren en upgraden hello Azure Linux Agent. Alle Hallo [goedgekeurd door providers van distributie](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) hello Azure Linux agentpakket integreren in hun installatiekopieën en -opslagplaatsen.

Raadpleeg de documentatie in Hallo toohello [Azure Linux Agent opslagplaats op GitHub](https://github.com/Azure/WALinuxAgent) voor geavanceerde installatie-opties, zoals het installeren van de bron- of toocustom locaties of voorvoegsels.

## <a name="command-line-options"></a>Opdrachtregelopties
### <a name="flags"></a>Vlaggen
* uitgebreide: uitgebreidheid van de opgegeven opdracht verhogen
* afdwingen: interactieve bevestiging voor bepaalde opdrachten overslaan

### <a name="commands"></a>Opdrachten
* Help: geeft een lijst van ondersteunde Hallo opdrachten en vlaggen.
* identiteitsgegevens: tooclean Hallo systeem probeert, waardoor het geschikt is om opnieuw in te richten. Deze bewerking Hallo volgende verwijderd:
  
  * Alle SSH host-sleutels (als Provisioning.RegenerateSshHostKeyPair 'y' in het configuratiebestand Hallo)
  * Configuratie van de naamserver in /etc/resolv.conf
  * Basis voor het wachtwoord van/etc/shadow (als Provisioning.DeleteRootPassword 'y' in het configuratiebestand Hallo)
  * In de cache leases voor DHCP-client
  * Opnieuw instellen van hosten naam toolocalhost.localdomain

> [!WARNING]
> Opheffen van inrichting wordt niet gegarandeerd die installatiekopie Hallo gewist van alle gevoelige informatie en kan deze geschikt is voor het opnieuw distribueren.
> 
> 

* identiteitsgegevens + gebruiker: alles onder - deprovision (boven) wordt uitgevoerd en ook verwijdert Hallo laatste ingerichte gebruikersaccount (verkregen uit /var/lib/waagent) en gegevens die zijn gekoppeld. Deze parameter is bij het inrichten van een afbeelding die eerder is ingericht op Azure zodat kan worden vastgelegd en hergebruikt ongedaan.
* versie: geeft Hallo versie van waagent
* serialconsole: Hiermee configureert u GRUB toomark ttyS0 (eerste seriële poort Hallo) als Hallo boot-console. Dit zorgt ervoor dat de kernel wanneer logboeken zijn verzonden toothe seriële poort en beschikbaar gesteld voor foutopsporing.
* daemon: waagent uitgevoerd als een daemon toomanage interactie met het Hallo-platform. Dit argument is opgegeven toowaagent in Hallo waagent init-script.
* Start: waagent als een achtergrondproces uitvoeren

## <a name="configuration"></a>Configuratie
Een configuratiebestand (/ etc/waagent.conf) besturingselementen Hallo acties van waagent. Een voorbeeldconfiguratiebestand wordt hieronder weergegeven:

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

Hallo die verschillende configuratieopties hieronder in detail worden beschreven. Configuratie-opties zijn van de drie typen; Booleaanse waarde, String of Integer. Hallo Booleaanse configuratieopties kunnen worden opgegeven als "y" of "n". Hallo speciale sleutelwoord 'None' kunnen worden gebruikt voor bepaalde tekenreeks type configuratie-items als gedetailleerde hieronder.

**Provisioning.Enabled:**  
Type: Booleaanse  
Standaard: y

Dit kunt Hallo gebruiker tooenable of Hallo functionaliteit in Hallo agent inrichten uitschakelen. Geldige waarden zijn "y" of "n". Als inrichting is uitgeschakeld, SSH-host en de gebruiker sleutels in de installatiekopie van het Hallo behouden blijven en alle opgegeven in hello Azure inrichting API configuratie wordt genegeerd.

> [!NOTE]
> Hallo `Provisioning.Enabled` standaardparameters te "n" Ubuntu Cloud afbeeldingen die cloud init voor het inrichten gebruiken.
> 
> 

**Provisioning.DeleteRootPassword:**  
Type: Booleaanse  
Standaard: n

Hallo inrichtingsproces als set, Hallo hoofdwachtwoord in Hallo bestand/etc/shadow tijdens is gewist.

**Provisioning.RegenerateSshHostKeyPair:**  
Type: Booleaanse  
Standaard: y

Als de set, alle SSH host sleutelparen (ecdsa, dsa en rsa) worden tijdens het inrichtingsproces van/etc/ssh/Hallo verwijderd. En een enkele nieuwe sleutelpaar gegenereerd.

Hallo coderingstype voor de nieuwe sleutelpaar Hallo kan worden geconfigureerd door Hallo Provisioning.SshHostKeyPairType vermelding. Houd er rekening mee dat sommige distributies opnieuw SSH-sleutelparen voor eventuele ontbrekende versleutelingstypen gemaakt worden wanneer Hallo SSH-daemon opnieuw wordt gestart (bijvoorbeeld, na het opnieuw opstarten).

**Provisioning.SshHostKeyPairType:**  
Type: String  
Standaard: rsa

Dit kan tooan versleutelingstype algoritme die wordt ondersteund door Hallo SSH-daemon op Hallo virtuele machine worden ingesteld. Hallo gewoonlijk ondersteund waarden zijn 'rsa', 'dsa' en 'ecdsa'. Houd er rekening mee 'putty.exe' in Windows biedt geen ondersteuning voor 'ecdsa'. Dus als u van plan toouse putty.exe op Windows tooconnect tooa Linux-implementatie bent, gebruik 'rsa' of 'dsa'.

**Provisioning.MonitorHostName:**  
Type: Booleaanse  
Standaard: y

Als is ingesteld, waagent wordt bewaken Hallo virtuele Linux-machine voor wijzigingen van de hostnaam (zoals die wordt geretourneerd door de opdracht 'hostname' hello) en automatisch Hallo netwerkconfiguratie in Hallo installatiekopie tooreflect Hallo wijzigen bijwerken. Wijzig in volgorde toopush Hallo naam toohello DNS-servers, netwerken opnieuw in Hallo virtuele machine wordt gestart. Dit resulteert in het kort verlies van verbinding met Internet.

**Provisioning.DecodeCustomData**  
Type: Booleaanse  
Standaard: n

Als is ingesteld, waagent wordt decoderen CustomData van Base64.

**Provisioning.ExecuteCustomData**  
Type: Booleaanse  
Standaard: n

Als de ingesteld, worden waagent CustomData na het inrichten uitgevoerd.

**Provisioning.PasswordCryptId**  
Type: tekenreeks  
Standaard: 6

Door crypt gebruikt bij het genereren van wachtwoord-hash-algoritme.  
 1 - MD5  
 2a - Blowfish  
 5 - SHA-256  
 6 - SHA-512  

**Provisioning.PasswordCryptSaltLength**  
Type: tekenreeks  
Standaard: 10

Lengte van willekeurige salt gebruikt bij het genereren van wachtwoord-hash.

**ResourceDisk.Format:**  
Type: Booleaanse  
Standaard: y

Als is ingesteld, Hallo resource schijf geleverd door Hallo platform wordt geformatteerd en gekoppeld door waagent als Hallo bestandssysteem type aangevraagd door de gebruiker in 'ResourceDisk.Filesystem' hello iets anders dan 'ntfs'. Een enkele partitie van het type Linux (83) wordt beschikbaar gesteld op Hallo schijf. Houd er rekening mee dat deze partitie niet geformatteerd als met succes worden gekoppeld.

**ResourceDisk.Filesystem:**  
Type: String  
Standaard: ext4

Hiermee geeft u Hallo filesystem-type voor Hallo resource schijf. Ondersteunde waarden verschillen per Linux-distributie. Als het Hallo-tekenreeks is de X-en vervolgens mkfs. X moet aanwezig zijn op Hallo Linux installatiekopie. SLES 11 afbeeldingen moeten doorgaans 'ext3' gebruiken. Installatiekopieën van FreeBSD moeten 'ufs2' hier gebruiken.

**ResourceDisk.MountPoint:**  
Type: String  
Standaardwaarde: / mnt/resourcegroep 

Hiermee geeft u Hallo pad waarmee Hallo resource schijf is gekoppeld. Houd er rekening mee dat Hallo resource-schijf is een *tijdelijke* schijfruimte en kan worden leeggemaakt wanneer Hallo VM gemaakt is.

**ResourceDisk.MountOptions**  
Type: String  
Standaard: geen

Hiermee geeft u een schijf koppelen toobe doorgegeven toohello mount -o opdracht Opties. Dit is een door komma's gescheiden lijst met waarden, bijvoorbeeld. 'nodev, nosuid'. Zie mount(8) voor meer informatie.

**ResourceDisk.EnableSwap:**  
Type: Booleaanse  
Standaard: n

Als is ingesteld, een wisselbestand (/ swapfile) op Hallo resource schijf wordt gemaakt en toegevoegd toohello system wisselruimte.

**ResourceDisk.SwapSizeMB:**  
Type: geheel getal  
Standaard: 0

Hallo grootte van het wisselbestand Hallo in megabytes.

**Logs.Verbose:**  
Type: Booleaanse  
Standaard: n

Als de set, logboek uitgebreidheid wordt versterkt. Waagent too/var/log/waagent.log registreert en maakt gebruik van Hallo logrotate functionaliteit toorotate systeemlogboeken.

**OS. EnableRDMA**  
Type: Booleaanse  
Standaard: n

Als is ingesteld, Hallo agent tooinstall proberen en vervolgens een RDMA-kernel-stuurprogramma die overeenkomt met Hallo-versie van de Hallo firmware op Hallo onderliggende hardware laden.

**OS. RootDeviceScsiTimeout:**  
Type: geheel getal  
Standaard: 300

Hiermee configureert u Hallo SCSI time-out in seconden op Hallo OS-schijf- en stations. Als dat niet is ingesteld, Hallo system standaardwaarden worden gebruikt.

**OS. OpensslPath:**  
Type: String  
Standaard: geen

Dit kan zijn gebruikte toospecify een alternatief pad voor Hallo openssl binaire toouse voor cryptografische bewerkingen.

**HttpProxy.Host, HttpProxy.Port**  
Type: String  
Standaard: geen

Als is ingesteld, Hallo agent gebruikt deze proxy server tooaccess Hallo internet. 

## <a name="ubuntu-cloud-images"></a>Ubuntu Cloud installatiekopieën
Opmerking die gebruikmaken van installatiekopieën van de Cloud Ubuntu [cloud init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform veel configuratietaken die anders zou worden beheerd door hello Azure Linux Agent.  Houd er rekening mee Hallo volgende verschillen:

* **Provisioning.Enabled** standaardwaarden te "n" Ubuntu Cloud afbeeldingen die gebruikmaken van cloud-init tooperform taken wordt ingericht.
* Hallo na configuratieparameters hebben geen effect op Ubuntu Cloud installatiekopieën die cloud init toomanage Hallo resource schijf en de wisselruimte ruimte gebruiken:
  
  * **ResourceDisk.Format**
  * **ResourceDisk.Filesystem**
  * **ResourceDisk.MountPoint**
  * **ResourceDisk.EnableSwap**
  * **ResourceDisk.SwapSizeMB**
* Zie Hallo resources tooconfigure Hallo resource schijf koppelpunt te volgen en wisselruimte op Ubuntu Cloud installatiekopieën tijdens het inrichten:
  
  * [Ubuntu-Wiki: Swap-partities configureren](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [Injecteren van aangepaste gegevens in Azure een virtuele Machine](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

