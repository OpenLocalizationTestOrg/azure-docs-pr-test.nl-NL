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
# <a name="understanding-and-using-hello-azure-linux-agent"></a><span data-ttu-id="6ba70-103">Uitleg en het gebruik van hello Azure Linux Agent</span><span class="sxs-lookup"><span data-stu-id="6ba70-103">Understanding and using hello Azure Linux Agent</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a><span data-ttu-id="6ba70-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="6ba70-104">Introduction</span></span>
<span data-ttu-id="6ba70-105">Hallo Microsoft Azure Linux Agent beheert (waagent) Linux en FreeBSD inrichting en VM interactie met hello Azure-Infrastructuurcontroller.</span><span class="sxs-lookup"><span data-stu-id="6ba70-105">hello Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="6ba70-106">Hallo functionaliteit voor Linux en FreeBSD IaaS-implementaties volgende bevat:</span><span class="sxs-lookup"><span data-stu-id="6ba70-106">It provides hello following functionality for Linux and FreeBSD IaaS deployments:</span></span>

> [!NOTE]
> <span data-ttu-id="6ba70-107">Zie hello Azure Linux agent [Leesmij](https://github.com/Azure/WALinuxAgent/blob/master/README.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6ba70-107">See hello Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.</span></span>
> 
> 

* <span data-ttu-id="6ba70-108">**Afbeelding inrichten**</span><span class="sxs-lookup"><span data-stu-id="6ba70-108">**Image Provisioning**</span></span>
  
  * <span data-ttu-id="6ba70-109">Het maken van een gebruikersaccount</span><span class="sxs-lookup"><span data-stu-id="6ba70-109">Creation of a user account</span></span>
  * <span data-ttu-id="6ba70-110">SSH-verificatietypen configureren</span><span class="sxs-lookup"><span data-stu-id="6ba70-110">Configuring SSH authentication types</span></span>
  * <span data-ttu-id="6ba70-111">Implementatie van openbare SSH-sleutels en sleutelparen</span><span class="sxs-lookup"><span data-stu-id="6ba70-111">Deployment of SSH public keys and key pairs</span></span>
  * <span data-ttu-id="6ba70-112">Hallo host-naam van de instelling</span><span class="sxs-lookup"><span data-stu-id="6ba70-112">Setting hello host name</span></span>
  * <span data-ttu-id="6ba70-113">Publishing Hallo naam toohello hostplatform DNS</span><span class="sxs-lookup"><span data-stu-id="6ba70-113">Publishing hello host name toohello platform DNS</span></span>
  * <span data-ttu-id="6ba70-114">SSH host vingerafdruk sleutel toohello rapportageplatform</span><span class="sxs-lookup"><span data-stu-id="6ba70-114">Reporting SSH host key fingerprint toohello platform</span></span>
  * <span data-ttu-id="6ba70-115">Resource Schijfbeheer</span><span class="sxs-lookup"><span data-stu-id="6ba70-115">Resource Disk Management</span></span>
  * <span data-ttu-id="6ba70-116">Opmaak en Hallo resource schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="6ba70-116">Formatting and mounting hello resource disk</span></span>
  * <span data-ttu-id="6ba70-117">Wisselruimte configureren</span><span class="sxs-lookup"><span data-stu-id="6ba70-117">Configuring swap space</span></span>
* <span data-ttu-id="6ba70-118">**Netwerken**</span><span class="sxs-lookup"><span data-stu-id="6ba70-118">**Networking**</span></span>
  
  * <span data-ttu-id="6ba70-119">Routes tooimprove compatibiliteit met platform DHCP-servers beheert</span><span class="sxs-lookup"><span data-stu-id="6ba70-119">Manages routes tooimprove compatibility with platform DHCP servers</span></span>
  * <span data-ttu-id="6ba70-120">Zorgt ervoor Hallo stabiliteit van de naam voor de netwerkinterface Hallo</span><span class="sxs-lookup"><span data-stu-id="6ba70-120">Ensures hello stability of hello network interface name</span></span>
* <span data-ttu-id="6ba70-121">**Kernel**</span><span class="sxs-lookup"><span data-stu-id="6ba70-121">**Kernel**</span></span>
  
  * <span data-ttu-id="6ba70-122">Hiermee configureert u virtuele NUMA (uitschakelen voor kernel < 2.6.37)</span><span class="sxs-lookup"><span data-stu-id="6ba70-122">Configures virtual NUMA (disable for kernel <2.6.37)</span></span>
  * <span data-ttu-id="6ba70-123">Hyper-V entropie voor /dev/random verbruikt</span><span class="sxs-lookup"><span data-stu-id="6ba70-123">Consumes Hyper-V entropy for /dev/random</span></span>
  * <span data-ttu-id="6ba70-124">Hiermee configureert u de SCSI-outs voor Hallo basis-apparaat (die mogelijk externe)</span><span class="sxs-lookup"><span data-stu-id="6ba70-124">Configures SCSI timeouts for hello root device (which could be remote)</span></span>
* <span data-ttu-id="6ba70-125">**Diagnostics**</span><span class="sxs-lookup"><span data-stu-id="6ba70-125">**Diagnostics**</span></span>
  
  * <span data-ttu-id="6ba70-126">Console omleiding toohello seriële poort</span><span class="sxs-lookup"><span data-stu-id="6ba70-126">Console redirection toohello serial port</span></span>
* <span data-ttu-id="6ba70-127">**SCVMM-implementaties**</span><span class="sxs-lookup"><span data-stu-id="6ba70-127">**SCVMM Deployments**</span></span>
  
  * <span data-ttu-id="6ba70-128">Detecteert en Hallo VMM-agent voor Linux bootstraps wanneer in een omgeving met System Center Virtual Machine Manager 2012 R2 wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="6ba70-128">Detects and bootstraps hello VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment</span></span>
* <span data-ttu-id="6ba70-129">**VM-extensie**</span><span class="sxs-lookup"><span data-stu-id="6ba70-129">**VM Extension**</span></span>
  
  * <span data-ttu-id="6ba70-130">Onderdeel geschreven door Microsoft en Partners in Linux VM (IaaS) tooenable en configuratie automation invoeren</span><span class="sxs-lookup"><span data-stu-id="6ba70-130">Inject component authored by Microsoft and Partners into Linux VM (IaaS) tooenable software and configuration automation</span></span>
  * <span data-ttu-id="6ba70-131">Implementatie van de VM-extensie verwijzing op [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span><span class="sxs-lookup"><span data-stu-id="6ba70-131">VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span></span>

## <a name="communication"></a><span data-ttu-id="6ba70-132">Communicatie</span><span class="sxs-lookup"><span data-stu-id="6ba70-132">Communication</span></span>
<span data-ttu-id="6ba70-133">de informatiestroom Hallo Hallo platform toohello agent gebeurt via twee kanalen:</span><span class="sxs-lookup"><span data-stu-id="6ba70-133">hello information flow from hello platform toohello agent occurs via two channels:</span></span>

* <span data-ttu-id="6ba70-134">Een opstarttijd gekoppeld DVD voor IaaS-implementaties.</span><span class="sxs-lookup"><span data-stu-id="6ba70-134">A boot-time attached DVD for IaaS deployments.</span></span> <span data-ttu-id="6ba70-135">Deze DVD bevat een OVF-compatibele configuratiebestand dat alle Inrichtingsgegevens dan de werkelijke SSH keypairs Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="6ba70-135">This DVD includes an OVF-compliant configuration file that includes all provisioning information other than hello actual SSH keypairs.</span></span>
* <span data-ttu-id="6ba70-136">Een TCP-eindpunt blootstellen van een REST-API gebruikt tooobtain implementatie en topologieconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="6ba70-136">A TCP endpoint exposing a REST API used tooobtain deployment and topology configuration.</span></span>

## <a name="requirements"></a><span data-ttu-id="6ba70-137">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6ba70-137">Requirements</span></span>
<span data-ttu-id="6ba70-138">Hallo volgende systemen zijn getest en staan bekend toowork Hello Azure Linux Agent:</span><span class="sxs-lookup"><span data-stu-id="6ba70-138">hello following systems have been tested and are known toowork with hello Azure Linux Agent:</span></span>

> [!NOTE]
> <span data-ttu-id="6ba70-139">Deze lijst kan afwijken van Hallo officiële lijst van ondersteunde systemen op Hallo van Microsoft Azure-Platform, zoals hier wordt beschreven: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span><span class="sxs-lookup"><span data-stu-id="6ba70-139">This list may differ from hello official list of supported systems on hello Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span></span>
> 
> 

* <span data-ttu-id="6ba70-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="6ba70-140">CoreOS</span></span>
* <span data-ttu-id="6ba70-141">CentOS 6.3 +</span><span class="sxs-lookup"><span data-stu-id="6ba70-141">CentOS 6.3+</span></span>
* <span data-ttu-id="6ba70-142">Red Hat Enterprise Linux 6.7 +</span><span class="sxs-lookup"><span data-stu-id="6ba70-142">Red Hat Enterprise Linux 6.7+</span></span>
* <span data-ttu-id="6ba70-143">Debian 7.0 +</span><span class="sxs-lookup"><span data-stu-id="6ba70-143">Debian 7.0+</span></span>
* <span data-ttu-id="6ba70-144">Ubuntu 12.04 +</span><span class="sxs-lookup"><span data-stu-id="6ba70-144">Ubuntu 12.04+</span></span>
* <span data-ttu-id="6ba70-145">openSUSE 12.3 +</span><span class="sxs-lookup"><span data-stu-id="6ba70-145">openSUSE 12.3+</span></span>
* <span data-ttu-id="6ba70-146">SLES 11 SP3 +</span><span class="sxs-lookup"><span data-stu-id="6ba70-146">SLES 11 SP3+</span></span>
* <span data-ttu-id="6ba70-147">Oracle Linux 6.4 +</span><span class="sxs-lookup"><span data-stu-id="6ba70-147">Oracle Linux 6.4+</span></span>

<span data-ttu-id="6ba70-148">Andere ondersteunde systemen:</span><span class="sxs-lookup"><span data-stu-id="6ba70-148">Other Supported Systems:</span></span>

* <span data-ttu-id="6ba70-149">FreeBSD 10 + (Azure Linux Agent v2.0.10 +)</span><span class="sxs-lookup"><span data-stu-id="6ba70-149">FreeBSD 10+ (Azure Linux Agent v2.0.10+)</span></span>

<span data-ttu-id="6ba70-150">Hallo Linux-agent is afhankelijk van sommige systeempakketten in volgorde toofunction goed de:</span><span class="sxs-lookup"><span data-stu-id="6ba70-150">hello Linux agent depends on some system packages in order toofunction properly:</span></span>

* <span data-ttu-id="6ba70-151">Python 2.6 +</span><span class="sxs-lookup"><span data-stu-id="6ba70-151">Python 2.6+</span></span>
* <span data-ttu-id="6ba70-152">OpenSSL 1.0 +</span><span class="sxs-lookup"><span data-stu-id="6ba70-152">OpenSSL 1.0+</span></span>
* <span data-ttu-id="6ba70-153">OpenSSH 5.3 +</span><span class="sxs-lookup"><span data-stu-id="6ba70-153">OpenSSH 5.3+</span></span>
* <span data-ttu-id="6ba70-154">Hulpprogramma's voor FileSystem: sfdisk fdisk, mkfs, gescheiden</span><span class="sxs-lookup"><span data-stu-id="6ba70-154">Filesystem utilities: sfdisk, fdisk, mkfs, parted</span></span>
* <span data-ttu-id="6ba70-155">Hulpprogramma's voor wachtwoord: chpasswd, sudo</span><span class="sxs-lookup"><span data-stu-id="6ba70-155">Password tools: chpasswd, sudo</span></span>
* <span data-ttu-id="6ba70-156">Tekst voor het verwerken van hulpprogramma's: ype, grep</span><span class="sxs-lookup"><span data-stu-id="6ba70-156">Text processing tools: sed, grep</span></span>
* <span data-ttu-id="6ba70-157">Hulpprogramma's voor netwerk: IP-route</span><span class="sxs-lookup"><span data-stu-id="6ba70-157">Network tools: ip-route</span></span>
* <span data-ttu-id="6ba70-158">Kernel-ondersteuning voor het koppelen van de UDF-bestandssystemen.</span><span class="sxs-lookup"><span data-stu-id="6ba70-158">Kernel support for mounting UDF filesystems.</span></span>

## <a name="installation"></a><span data-ttu-id="6ba70-159">Installeren</span><span class="sxs-lookup"><span data-stu-id="6ba70-159">Installation</span></span>
<span data-ttu-id="6ba70-160">Installatie met een RPM of een pakket DEB vanuit uw distributiepunt pakket opslagplaats is Hallo voorkeurs-methode voor het installeren en upgraden hello Azure Linux Agent.</span><span class="sxs-lookup"><span data-stu-id="6ba70-160">Installation using an RPM or a DEB package from your distribution's package repository is hello preferred method of installing and upgrading hello Azure Linux Agent.</span></span> <span data-ttu-id="6ba70-161">Alle Hallo [goedgekeurd door providers van distributie](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) hello Azure Linux agentpakket integreren in hun installatiekopieën en -opslagplaatsen.</span><span class="sxs-lookup"><span data-stu-id="6ba70-161">All hello [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate hello Azure Linux agent package into their images and repositories.</span></span>

<span data-ttu-id="6ba70-162">Raadpleeg de documentatie in Hallo toohello [Azure Linux Agent opslagplaats op GitHub](https://github.com/Azure/WALinuxAgent) voor geavanceerde installatie-opties, zoals het installeren van de bron- of toocustom locaties of voorvoegsels.</span><span class="sxs-lookup"><span data-stu-id="6ba70-162">Refer toohello documentation in hello [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or toocustom locations or prefixes.</span></span>

## <a name="command-line-options"></a><span data-ttu-id="6ba70-163">Opdrachtregelopties</span><span class="sxs-lookup"><span data-stu-id="6ba70-163">Command Line Options</span></span>
### <a name="flags"></a><span data-ttu-id="6ba70-164">Vlaggen</span><span class="sxs-lookup"><span data-stu-id="6ba70-164">Flags</span></span>
* <span data-ttu-id="6ba70-165">uitgebreide: uitgebreidheid van de opgegeven opdracht verhogen</span><span class="sxs-lookup"><span data-stu-id="6ba70-165">verbose: Increase verbosity of specified command</span></span>
* <span data-ttu-id="6ba70-166">afdwingen: interactieve bevestiging voor bepaalde opdrachten overslaan</span><span class="sxs-lookup"><span data-stu-id="6ba70-166">force: Skip interactive confirmation for some commands</span></span>

### <a name="commands"></a><span data-ttu-id="6ba70-167">Opdrachten</span><span class="sxs-lookup"><span data-stu-id="6ba70-167">Commands</span></span>
* <span data-ttu-id="6ba70-168">Help: geeft een lijst van ondersteunde Hallo opdrachten en vlaggen.</span><span class="sxs-lookup"><span data-stu-id="6ba70-168">help: Lists hello supported commands and flags.</span></span>
* <span data-ttu-id="6ba70-169">identiteitsgegevens: tooclean Hallo systeem probeert, waardoor het geschikt is om opnieuw in te richten.</span><span class="sxs-lookup"><span data-stu-id="6ba70-169">deprovision: Attempt tooclean hello system and make it suitable for re-provisioning.</span></span> <span data-ttu-id="6ba70-170">Deze bewerking Hallo volgende verwijderd:</span><span class="sxs-lookup"><span data-stu-id="6ba70-170">This operation deleted hello following:</span></span>
  
  * <span data-ttu-id="6ba70-171">Alle SSH host-sleutels (als Provisioning.RegenerateSshHostKeyPair 'y' in het configuratiebestand Hallo)</span><span class="sxs-lookup"><span data-stu-id="6ba70-171">All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="6ba70-172">Configuratie van de naamserver in /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="6ba70-172">Nameserver configuration in /etc/resolv.conf</span></span>
  * <span data-ttu-id="6ba70-173">Basis voor het wachtwoord van/etc/shadow (als Provisioning.DeleteRootPassword 'y' in het configuratiebestand Hallo)</span><span class="sxs-lookup"><span data-stu-id="6ba70-173">Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="6ba70-174">In de cache leases voor DHCP-client</span><span class="sxs-lookup"><span data-stu-id="6ba70-174">Cached DHCP client leases</span></span>
  * <span data-ttu-id="6ba70-175">Opnieuw instellen van hosten naam toolocalhost.localdomain</span><span class="sxs-lookup"><span data-stu-id="6ba70-175">Resets host name toolocalhost.localdomain</span></span>

> [!WARNING]
> <span data-ttu-id="6ba70-176">Opheffen van inrichting wordt niet gegarandeerd die installatiekopie Hallo gewist van alle gevoelige informatie en kan deze geschikt is voor het opnieuw distribueren.</span><span class="sxs-lookup"><span data-stu-id="6ba70-176">Deprovisioning does not guarantee that hello image is cleared of all sensitive information and suitable for redistribution.</span></span>
> 
> 

* <span data-ttu-id="6ba70-177">identiteitsgegevens + gebruiker: alles onder - deprovision (boven) wordt uitgevoerd en ook verwijdert Hallo laatste ingerichte gebruikersaccount (verkregen uit /var/lib/waagent) en gegevens die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="6ba70-177">deprovision+user: Performs everything under -deprovision (above) and also deletes hello last provisioned user account (obtained from /var/lib/waagent) and associated data.</span></span> <span data-ttu-id="6ba70-178">Deze parameter is bij het inrichten van een afbeelding die eerder is ingericht op Azure zodat kan worden vastgelegd en hergebruikt ongedaan.</span><span class="sxs-lookup"><span data-stu-id="6ba70-178">This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.</span></span>
* <span data-ttu-id="6ba70-179">versie: geeft Hallo versie van waagent</span><span class="sxs-lookup"><span data-stu-id="6ba70-179">version: Displays hello version of waagent</span></span>
* <span data-ttu-id="6ba70-180">serialconsole: Hiermee configureert u GRUB toomark ttyS0 (eerste seriële poort Hallo) als Hallo boot-console.</span><span class="sxs-lookup"><span data-stu-id="6ba70-180">serialconsole: Configures GRUB toomark ttyS0 (hello first serial port) as hello boot console.</span></span> <span data-ttu-id="6ba70-181">Dit zorgt ervoor dat de kernel wanneer logboeken zijn verzonden toothe seriële poort en beschikbaar gesteld voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="6ba70-181">This ensures that kernel bootup logs are sent toothe serial port and made available for debugging.</span></span>
* <span data-ttu-id="6ba70-182">daemon: waagent uitgevoerd als een daemon toomanage interactie met het Hallo-platform.</span><span class="sxs-lookup"><span data-stu-id="6ba70-182">daemon: Run waagent as a daemon toomanage interaction with hello platform.</span></span> <span data-ttu-id="6ba70-183">Dit argument is opgegeven toowaagent in Hallo waagent init-script.</span><span class="sxs-lookup"><span data-stu-id="6ba70-183">This argument is specified toowaagent in hello waagent init script.</span></span>
* <span data-ttu-id="6ba70-184">Start: waagent als een achtergrondproces uitvoeren</span><span class="sxs-lookup"><span data-stu-id="6ba70-184">start: Run waagent as a background process</span></span>

## <a name="configuration"></a><span data-ttu-id="6ba70-185">Configuratie</span><span class="sxs-lookup"><span data-stu-id="6ba70-185">Configuration</span></span>
<span data-ttu-id="6ba70-186">Een configuratiebestand (/ etc/waagent.conf) besturingselementen Hallo acties van waagent.</span><span class="sxs-lookup"><span data-stu-id="6ba70-186">A configuration file (/etc/waagent.conf) controls hello actions of waagent.</span></span> <span data-ttu-id="6ba70-187">Een voorbeeldconfiguratiebestand wordt hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="6ba70-187">A sample configuration file is shown below:</span></span>

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

<span data-ttu-id="6ba70-188">Hallo die verschillende configuratieopties hieronder in detail worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="6ba70-188">hello various configuration options are described in detail below.</span></span> <span data-ttu-id="6ba70-189">Configuratie-opties zijn van de drie typen; Booleaanse waarde, String of Integer.</span><span class="sxs-lookup"><span data-stu-id="6ba70-189">Configuration options are of three types; Boolean, String or Integer.</span></span> <span data-ttu-id="6ba70-190">Hallo Booleaanse configuratieopties kunnen worden opgegeven als "y" of "n".</span><span class="sxs-lookup"><span data-stu-id="6ba70-190">hello Boolean configuration options can be specified as "y" or "n".</span></span> <span data-ttu-id="6ba70-191">Hallo speciale sleutelwoord 'None' kunnen worden gebruikt voor bepaalde tekenreeks type configuratie-items als gedetailleerde hieronder.</span><span class="sxs-lookup"><span data-stu-id="6ba70-191">hello special keyword "None" may be used for some string type configuration entries as detailed below.</span></span>

<span data-ttu-id="6ba70-192">**Provisioning.Enabled:**</span><span class="sxs-lookup"><span data-stu-id="6ba70-192">**Provisioning.Enabled:**</span></span>  
<span data-ttu-id="6ba70-193">Type: Booleaanse</span><span class="sxs-lookup"><span data-stu-id="6ba70-193">Type: Boolean</span></span>  
<span data-ttu-id="6ba70-194">Standaard: y</span><span class="sxs-lookup"><span data-stu-id="6ba70-194">Default: y</span></span>

<span data-ttu-id="6ba70-195">Dit kunt Hallo gebruiker tooenable of Hallo functionaliteit in Hallo agent inrichten uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="6ba70-195">This allows hello user tooenable or disable hello provisioning functionality in hello agent.</span></span> <span data-ttu-id="6ba70-196">Geldige waarden zijn "y" of "n".</span><span class="sxs-lookup"><span data-stu-id="6ba70-196">Valid values are "y" or "n".</span></span> <span data-ttu-id="6ba70-197">Als inrichting is uitgeschakeld, SSH-host en de gebruiker sleutels in de installatiekopie van het Hallo behouden blijven en alle opgegeven in hello Azure inrichting API configuratie wordt genegeerd.</span><span class="sxs-lookup"><span data-stu-id="6ba70-197">If provisioning is disabled, SSH host and user keys in hello image are preserved and any configuration specified in hello Azure provisioning API is ignored.</span></span>

> [!NOTE]
> <span data-ttu-id="6ba70-198">Hallo `Provisioning.Enabled` standaardparameters te "n" Ubuntu Cloud afbeeldingen die cloud init voor het inrichten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6ba70-198">hello `Provisioning.Enabled` parameter defaults too"n" on Ubuntu Cloud Images that use cloud-init for provisioning.</span></span>
> 
> 

<span data-ttu-id="6ba70-199">**Provisioning.DeleteRootPassword:**</span><span class="sxs-lookup"><span data-stu-id="6ba70-199">**Provisioning.DeleteRootPassword:**</span></span>  
<span data-ttu-id="6ba70-200">Type: Booleaanse</span><span class="sxs-lookup"><span data-stu-id="6ba70-200">Type: Boolean</span></span>  
<span data-ttu-id="6ba70-201">Standaard: n</span><span class="sxs-lookup"><span data-stu-id="6ba70-201">Default: n</span></span>

<span data-ttu-id="6ba70-202">Hallo inrichtingsproces als set, Hallo hoofdwachtwoord in Hallo bestand/etc/shadow tijdens is gewist.</span><span class="sxs-lookup"><span data-stu-id="6ba70-202">If set, hello root password in hello /etc/shadow file is erased during hello provisioning process.</span></span>

<span data-ttu-id="6ba70-203">**Provisioning.RegenerateSshHostKeyPair:**</span><span class="sxs-lookup"><span data-stu-id="6ba70-203">**Provisioning.RegenerateSshHostKeyPair:**</span></span>  
<span data-ttu-id="6ba70-204">Type: Booleaanse</span><span class="sxs-lookup"><span data-stu-id="6ba70-204">Type: Boolean</span></span>  
<span data-ttu-id="6ba70-205">Standaard: y</span><span class="sxs-lookup"><span data-stu-id="6ba70-205">Default: y</span></span>

<span data-ttu-id="6ba70-206">Als de set, alle SSH host sleutelparen (ecdsa, dsa en rsa) worden tijdens het inrichtingsproces van/etc/ssh/Hallo verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6ba70-206">If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during hello provisioning process from /etc/ssh/.</span></span> <span data-ttu-id="6ba70-207">En een enkele nieuwe sleutelpaar gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="6ba70-207">And a single fresh key pair is generated.</span></span>

<span data-ttu-id="6ba70-208">Hallo coderingstype voor de nieuwe sleutelpaar Hallo kan worden geconfigureerd door Hallo Provisioning.SshHostKeyPairType vermelding.</span><span class="sxs-lookup"><span data-stu-id="6ba70-208">hello encryption type for hello fresh key pair is configurable by hello Provisioning.SshHostKeyPairType entry.</span></span> <span data-ttu-id="6ba70-209">Houd er rekening mee dat sommige distributies opnieuw SSH-sleutelparen voor eventuele ontbrekende versleutelingstypen gemaakt worden wanneer Hallo SSH-daemon opnieuw wordt gestart (bijvoorbeeld, na het opnieuw opstarten).</span><span class="sxs-lookup"><span data-stu-id="6ba70-209">Please note that some distributions will re-create SSH key pairs for any missing encryption types when hello SSH daemon is restarted (for example, upon a reboot).</span></span>

<span data-ttu-id="6ba70-210">**Provisioning.SshHostKeyPairType:**</span><span class="sxs-lookup"><span data-stu-id="6ba70-210">**Provisioning.SshHostKeyPairType:**</span></span>  
<span data-ttu-id="6ba70-211">Type: String</span><span class="sxs-lookup"><span data-stu-id="6ba70-211">Type: String</span></span>  
<span data-ttu-id="6ba70-212">Standaard: rsa</span><span class="sxs-lookup"><span data-stu-id="6ba70-212">Default: rsa</span></span>

<span data-ttu-id="6ba70-213">Dit kan tooan versleutelingstype algoritme die wordt ondersteund door Hallo SSH-daemon op Hallo virtuele machine worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6ba70-213">This can be set tooan encryption algorithm type that is supported by hello SSH daemon on hello virtual machine.</span></span> <span data-ttu-id="6ba70-214">Hallo gewoonlijk ondersteund waarden zijn 'rsa', 'dsa' en 'ecdsa'.</span><span class="sxs-lookup"><span data-stu-id="6ba70-214">hello typically supported values are "rsa", "dsa" and "ecdsa".</span></span> <span data-ttu-id="6ba70-215">Houd er rekening mee 'putty.exe' in Windows biedt geen ondersteuning voor 'ecdsa'.</span><span class="sxs-lookup"><span data-stu-id="6ba70-215">Note that "putty.exe" on Windows does not support "ecdsa".</span></span> <span data-ttu-id="6ba70-216">Dus als u van plan toouse putty.exe op Windows tooconnect tooa Linux-implementatie bent, gebruik 'rsa' of 'dsa'.</span><span class="sxs-lookup"><span data-stu-id="6ba70-216">So, if you intend toouse putty.exe on Windows tooconnect tooa Linux deployment, please use "rsa" or "dsa".</span></span>

<span data-ttu-id="6ba70-217">**Provisioning.MonitorHostName:**</span><span class="sxs-lookup"><span data-stu-id="6ba70-217">**Provisioning.MonitorHostName:**</span></span>  
<span data-ttu-id="6ba70-218">Type: Booleaanse</span><span class="sxs-lookup"><span data-stu-id="6ba70-218">Type: Boolean</span></span>  
<span data-ttu-id="6ba70-219">Standaard: y</span><span class="sxs-lookup"><span data-stu-id="6ba70-219">Default: y</span></span>

<span data-ttu-id="6ba70-220">Als is ingesteld, waagent wordt bewaken Hallo virtuele Linux-machine voor wijzigingen van de hostnaam (zoals die wordt geretourneerd door de opdracht 'hostname' hello) en automatisch Hallo netwerkconfiguratie in Hallo installatiekopie tooreflect Hallo wijzigen bijwerken.</span><span class="sxs-lookup"><span data-stu-id="6ba70-220">If set, waagent will monitor hello Linux virtual machine for hostname changes (as returned by hello "hostname" command) and automatically update hello networking configuration in hello image tooreflect hello change.</span></span> <span data-ttu-id="6ba70-221">Wijzig in volgorde toopush Hallo naam toohello DNS-servers, netwerken opnieuw in Hallo virtuele machine wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="6ba70-221">In order toopush hello name change toohello DNS servers, networking will be restarted in hello virtual machine.</span></span> <span data-ttu-id="6ba70-222">Dit resulteert in het kort verlies van verbinding met Internet.</span><span class="sxs-lookup"><span data-stu-id="6ba70-222">This will result in brief loss of Internet connectivity.</span></span>

<span data-ttu-id="6ba70-223">**Provisioning.DecodeCustomData**</span><span class="sxs-lookup"><span data-stu-id="6ba70-223">**Provisioning.DecodeCustomData**</span></span>  
<span data-ttu-id="6ba70-224">Type: Booleaanse</span><span class="sxs-lookup"><span data-stu-id="6ba70-224">Type: Boolean</span></span>  
<span data-ttu-id="6ba70-225">Standaard: n</span><span class="sxs-lookup"><span data-stu-id="6ba70-225">Default: n</span></span>

<span data-ttu-id="6ba70-226">Als is ingesteld, waagent wordt decoderen CustomData van Base64.</span><span class="sxs-lookup"><span data-stu-id="6ba70-226">If set, waagent will decode CustomData from Base64.</span></span>

<span data-ttu-id="6ba70-227">**Provisioning.ExecuteCustomData**</span><span class="sxs-lookup"><span data-stu-id="6ba70-227">**Provisioning.ExecuteCustomData**</span></span>  
<span data-ttu-id="6ba70-228">Type: Booleaanse</span><span class="sxs-lookup"><span data-stu-id="6ba70-228">Type: Boolean</span></span>  
<span data-ttu-id="6ba70-229">Standaard: n</span><span class="sxs-lookup"><span data-stu-id="6ba70-229">Default: n</span></span>

<span data-ttu-id="6ba70-230">Als de ingesteld, worden waagent CustomData na het inrichten uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6ba70-230">If set, waagent will execute CustomData after provisioning.</span></span>

<span data-ttu-id="6ba70-231">**Provisioning.PasswordCryptId**</span><span class="sxs-lookup"><span data-stu-id="6ba70-231">**Provisioning.PasswordCryptId**</span></span>  
<span data-ttu-id="6ba70-232">Type: tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6ba70-232">Type:String</span></span>  
<span data-ttu-id="6ba70-233">Standaard: 6</span><span class="sxs-lookup"><span data-stu-id="6ba70-233">Default:6</span></span>

<span data-ttu-id="6ba70-234">Door crypt gebruikt bij het genereren van wachtwoord-hash-algoritme.</span><span class="sxs-lookup"><span data-stu-id="6ba70-234">Algorithm used by crypt when generating password hash.</span></span>  
 <span data-ttu-id="6ba70-235">1 - MD5</span><span class="sxs-lookup"><span data-stu-id="6ba70-235">1 - MD5</span></span>  
 <span data-ttu-id="6ba70-236">2a - Blowfish</span><span class="sxs-lookup"><span data-stu-id="6ba70-236">2a - Blowfish</span></span>  
 <span data-ttu-id="6ba70-237">5 - SHA-256</span><span class="sxs-lookup"><span data-stu-id="6ba70-237">5 - SHA-256</span></span>  
 <span data-ttu-id="6ba70-238">6 - SHA-512</span><span class="sxs-lookup"><span data-stu-id="6ba70-238">6 - SHA-512</span></span>  

<span data-ttu-id="6ba70-239">**Provisioning.PasswordCryptSaltLength**</span><span class="sxs-lookup"><span data-stu-id="6ba70-239">**Provisioning.PasswordCryptSaltLength**</span></span>  
<span data-ttu-id="6ba70-240">Type: tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6ba70-240">Type:String</span></span>  
<span data-ttu-id="6ba70-241">Standaard: 10</span><span class="sxs-lookup"><span data-stu-id="6ba70-241">Default:10</span></span>

<span data-ttu-id="6ba70-242">Lengte van willekeurige salt gebruikt bij het genereren van wachtwoord-hash.</span><span class="sxs-lookup"><span data-stu-id="6ba70-242">Length of random salt used when generating password hash.</span></span>

<span data-ttu-id="6ba70-243">**ResourceDisk.Format:**</span><span class="sxs-lookup"><span data-stu-id="6ba70-243">**ResourceDisk.Format:**</span></span>  
<span data-ttu-id="6ba70-244">Type: Booleaanse</span><span class="sxs-lookup"><span data-stu-id="6ba70-244">Type: Boolean</span></span>  
<span data-ttu-id="6ba70-245">Standaard: y</span><span class="sxs-lookup"><span data-stu-id="6ba70-245">Default: y</span></span>

<span data-ttu-id="6ba70-246">Als is ingesteld, Hallo resource schijf geleverd door Hallo platform wordt geformatteerd en gekoppeld door waagent als Hallo bestandssysteem type aangevraagd door de gebruiker in 'ResourceDisk.Filesystem' hello iets anders dan 'ntfs'.</span><span class="sxs-lookup"><span data-stu-id="6ba70-246">If set, hello resource disk provided by hello platform will be formatted and mounted by waagent if hello filesystem type requested by hello user in "ResourceDisk.Filesystem" is anything other than "ntfs".</span></span> <span data-ttu-id="6ba70-247">Een enkele partitie van het type Linux (83) wordt beschikbaar gesteld op Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="6ba70-247">A single partition of type Linux (83) will be made available on hello disk.</span></span> <span data-ttu-id="6ba70-248">Houd er rekening mee dat deze partitie niet geformatteerd als met succes worden gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="6ba70-248">Note that this partition will not be formatted if it can be successfully mounted.</span></span>

<span data-ttu-id="6ba70-249">**ResourceDisk.Filesystem:**</span><span class="sxs-lookup"><span data-stu-id="6ba70-249">**ResourceDisk.Filesystem:**</span></span>  
<span data-ttu-id="6ba70-250">Type: String</span><span class="sxs-lookup"><span data-stu-id="6ba70-250">Type: String</span></span>  
<span data-ttu-id="6ba70-251">Standaard: ext4</span><span class="sxs-lookup"><span data-stu-id="6ba70-251">Default: ext4</span></span>

<span data-ttu-id="6ba70-252">Hiermee geeft u Hallo filesystem-type voor Hallo resource schijf.</span><span class="sxs-lookup"><span data-stu-id="6ba70-252">This specifies hello filesystem type for hello resource disk.</span></span> <span data-ttu-id="6ba70-253">Ondersteunde waarden verschillen per Linux-distributie.</span><span class="sxs-lookup"><span data-stu-id="6ba70-253">Supported values vary by Linux distribution.</span></span> <span data-ttu-id="6ba70-254">Als het Hallo-tekenreeks is de X-en vervolgens mkfs. X moet aanwezig zijn op Hallo Linux installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="6ba70-254">If hello string is X, then mkfs.X should be present on hello Linux image.</span></span> <span data-ttu-id="6ba70-255">SLES 11 afbeeldingen moeten doorgaans 'ext3' gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6ba70-255">SLES 11 images should typically use 'ext3'.</span></span> <span data-ttu-id="6ba70-256">Installatiekopieën van FreeBSD moeten 'ufs2' hier gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6ba70-256">FreeBSD images should use 'ufs2' here.</span></span>

<span data-ttu-id="6ba70-257">**ResourceDisk.MountPoint:**</span><span class="sxs-lookup"><span data-stu-id="6ba70-257">**ResourceDisk.MountPoint:**</span></span>  
<span data-ttu-id="6ba70-258">Type: String</span><span class="sxs-lookup"><span data-stu-id="6ba70-258">Type: String</span></span>  
<span data-ttu-id="6ba70-259">Standaardwaarde: / mnt/resourcegroep</span><span class="sxs-lookup"><span data-stu-id="6ba70-259">Default: /mnt/resource</span></span> 

<span data-ttu-id="6ba70-260">Hiermee geeft u Hallo pad waarmee Hallo resource schijf is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="6ba70-260">This specifies hello path at which hello resource disk is mounted.</span></span> <span data-ttu-id="6ba70-261">Houd er rekening mee dat Hallo resource-schijf is een *tijdelijke* schijfruimte en kan worden leeggemaakt wanneer Hallo VM gemaakt is.</span><span class="sxs-lookup"><span data-stu-id="6ba70-261">Note that hello resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span>

<span data-ttu-id="6ba70-262">**ResourceDisk.MountOptions**</span><span class="sxs-lookup"><span data-stu-id="6ba70-262">**ResourceDisk.MountOptions**</span></span>  
<span data-ttu-id="6ba70-263">Type: String</span><span class="sxs-lookup"><span data-stu-id="6ba70-263">Type: String</span></span>  
<span data-ttu-id="6ba70-264">Standaard: geen</span><span class="sxs-lookup"><span data-stu-id="6ba70-264">Default: None</span></span>

<span data-ttu-id="6ba70-265">Hiermee geeft u een schijf koppelen toobe doorgegeven toohello mount -o opdracht Opties.</span><span class="sxs-lookup"><span data-stu-id="6ba70-265">Specifies disk mount options toobe passed toohello mount -o command.</span></span> <span data-ttu-id="6ba70-266">Dit is een door komma's gescheiden lijst met waarden, bijvoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="6ba70-266">This is a comma separated list of values, ex.</span></span> <span data-ttu-id="6ba70-267">'nodev, nosuid'.</span><span class="sxs-lookup"><span data-stu-id="6ba70-267">'nodev,nosuid'.</span></span> <span data-ttu-id="6ba70-268">Zie mount(8) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6ba70-268">See mount(8) for details.</span></span>

<span data-ttu-id="6ba70-269">**ResourceDisk.EnableSwap:**</span><span class="sxs-lookup"><span data-stu-id="6ba70-269">**ResourceDisk.EnableSwap:**</span></span>  
<span data-ttu-id="6ba70-270">Type: Booleaanse</span><span class="sxs-lookup"><span data-stu-id="6ba70-270">Type: Boolean</span></span>  
<span data-ttu-id="6ba70-271">Standaard: n</span><span class="sxs-lookup"><span data-stu-id="6ba70-271">Default: n</span></span>

<span data-ttu-id="6ba70-272">Als is ingesteld, een wisselbestand (/ swapfile) op Hallo resource schijf wordt gemaakt en toegevoegd toohello system wisselruimte.</span><span class="sxs-lookup"><span data-stu-id="6ba70-272">If set, a swap file (/swapfile) is created on hello resource disk and added toohello system swap space.</span></span>

<span data-ttu-id="6ba70-273">**ResourceDisk.SwapSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="6ba70-273">**ResourceDisk.SwapSizeMB:**</span></span>  
<span data-ttu-id="6ba70-274">Type: geheel getal</span><span class="sxs-lookup"><span data-stu-id="6ba70-274">Type: Integer</span></span>  
<span data-ttu-id="6ba70-275">Standaard: 0</span><span class="sxs-lookup"><span data-stu-id="6ba70-275">Default: 0</span></span>

<span data-ttu-id="6ba70-276">Hallo grootte van het wisselbestand Hallo in megabytes.</span><span class="sxs-lookup"><span data-stu-id="6ba70-276">hello size of hello swap file in megabytes.</span></span>

<span data-ttu-id="6ba70-277">**Logs.Verbose:**</span><span class="sxs-lookup"><span data-stu-id="6ba70-277">**Logs.Verbose:**</span></span>  
<span data-ttu-id="6ba70-278">Type: Booleaanse</span><span class="sxs-lookup"><span data-stu-id="6ba70-278">Type: Boolean</span></span>  
<span data-ttu-id="6ba70-279">Standaard: n</span><span class="sxs-lookup"><span data-stu-id="6ba70-279">Default: n</span></span>

<span data-ttu-id="6ba70-280">Als de set, logboek uitgebreidheid wordt versterkt.</span><span class="sxs-lookup"><span data-stu-id="6ba70-280">If set, log verbosity is boosted.</span></span> <span data-ttu-id="6ba70-281">Waagent too/var/log/waagent.log registreert en maakt gebruik van Hallo logrotate functionaliteit toorotate systeemlogboeken.</span><span class="sxs-lookup"><span data-stu-id="6ba70-281">Waagent logs too/var/log/waagent.log and leverages hello system logrotate functionality toorotate logs.</span></span>

<span data-ttu-id="6ba70-282">**OS. EnableRDMA**</span><span class="sxs-lookup"><span data-stu-id="6ba70-282">**OS.EnableRDMA**</span></span>  
<span data-ttu-id="6ba70-283">Type: Booleaanse</span><span class="sxs-lookup"><span data-stu-id="6ba70-283">Type: Boolean</span></span>  
<span data-ttu-id="6ba70-284">Standaard: n</span><span class="sxs-lookup"><span data-stu-id="6ba70-284">Default: n</span></span>

<span data-ttu-id="6ba70-285">Als is ingesteld, Hallo agent tooinstall proberen en vervolgens een RDMA-kernel-stuurprogramma die overeenkomt met Hallo-versie van de Hallo firmware op Hallo onderliggende hardware laden.</span><span class="sxs-lookup"><span data-stu-id="6ba70-285">If set, hello agent will attempt tooinstall and then load an RDMA kernel driver that matches hello version of hello firmware on hello underlying hardware.</span></span>

<span data-ttu-id="6ba70-286">**OS. RootDeviceScsiTimeout:**</span><span class="sxs-lookup"><span data-stu-id="6ba70-286">**OS.RootDeviceScsiTimeout:**</span></span>  
<span data-ttu-id="6ba70-287">Type: geheel getal</span><span class="sxs-lookup"><span data-stu-id="6ba70-287">Type: Integer</span></span>  
<span data-ttu-id="6ba70-288">Standaard: 300</span><span class="sxs-lookup"><span data-stu-id="6ba70-288">Default: 300</span></span>

<span data-ttu-id="6ba70-289">Hiermee configureert u Hallo SCSI time-out in seconden op Hallo OS-schijf- en stations.</span><span class="sxs-lookup"><span data-stu-id="6ba70-289">This configures hello SCSI timeout in seconds on hello OS disk and data drives.</span></span> <span data-ttu-id="6ba70-290">Als dat niet is ingesteld, Hallo system standaardwaarden worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6ba70-290">If not set, hello system defaults are used.</span></span>

<span data-ttu-id="6ba70-291">**OS. OpensslPath:**</span><span class="sxs-lookup"><span data-stu-id="6ba70-291">**OS.OpensslPath:**</span></span>  
<span data-ttu-id="6ba70-292">Type: String</span><span class="sxs-lookup"><span data-stu-id="6ba70-292">Type: String</span></span>  
<span data-ttu-id="6ba70-293">Standaard: geen</span><span class="sxs-lookup"><span data-stu-id="6ba70-293">Default: None</span></span>

<span data-ttu-id="6ba70-294">Dit kan zijn gebruikte toospecify een alternatief pad voor Hallo openssl binaire toouse voor cryptografische bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="6ba70-294">This can be used toospecify an alternate path for hello openssl binary toouse for cryptographic operations.</span></span>

<span data-ttu-id="6ba70-295">**HttpProxy.Host, HttpProxy.Port**</span><span class="sxs-lookup"><span data-stu-id="6ba70-295">**HttpProxy.Host, HttpProxy.Port**</span></span>  
<span data-ttu-id="6ba70-296">Type: String</span><span class="sxs-lookup"><span data-stu-id="6ba70-296">Type: String</span></span>  
<span data-ttu-id="6ba70-297">Standaard: geen</span><span class="sxs-lookup"><span data-stu-id="6ba70-297">Default: None</span></span>

<span data-ttu-id="6ba70-298">Als is ingesteld, Hallo agent gebruikt deze proxy server tooaccess Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="6ba70-298">If set, hello agent will use this proxy server tooaccess hello internet.</span></span> 

## <a name="ubuntu-cloud-images"></a><span data-ttu-id="6ba70-299">Ubuntu Cloud installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="6ba70-299">Ubuntu Cloud Images</span></span>
<span data-ttu-id="6ba70-300">Opmerking die gebruikmaken van installatiekopieën van de Cloud Ubuntu [cloud init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform veel configuratietaken die anders zou worden beheerd door hello Azure Linux Agent.</span><span class="sxs-lookup"><span data-stu-id="6ba70-300">Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform many configuration tasks that would otherwise be managed by hello Azure Linux Agent.</span></span>  <span data-ttu-id="6ba70-301">Houd er rekening mee Hallo volgende verschillen:</span><span class="sxs-lookup"><span data-stu-id="6ba70-301">Please note hello following differences:</span></span>

* <span data-ttu-id="6ba70-302">**Provisioning.Enabled** standaardwaarden te "n" Ubuntu Cloud afbeeldingen die gebruikmaken van cloud-init tooperform taken wordt ingericht.</span><span class="sxs-lookup"><span data-stu-id="6ba70-302">**Provisioning.Enabled** defaults too"n" on Ubuntu Cloud Images that use cloud-init tooperform provisioning tasks.</span></span>
* <span data-ttu-id="6ba70-303">Hallo na configuratieparameters hebben geen effect op Ubuntu Cloud installatiekopieën die cloud init toomanage Hallo resource schijf en de wisselruimte ruimte gebruiken:</span><span class="sxs-lookup"><span data-stu-id="6ba70-303">hello following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init toomanage hello resource disk and swap space:</span></span>
  
  * <span data-ttu-id="6ba70-304">**ResourceDisk.Format**</span><span class="sxs-lookup"><span data-stu-id="6ba70-304">**ResourceDisk.Format**</span></span>
  * <span data-ttu-id="6ba70-305">**ResourceDisk.Filesystem**</span><span class="sxs-lookup"><span data-stu-id="6ba70-305">**ResourceDisk.Filesystem**</span></span>
  * <span data-ttu-id="6ba70-306">**ResourceDisk.MountPoint**</span><span class="sxs-lookup"><span data-stu-id="6ba70-306">**ResourceDisk.MountPoint**</span></span>
  * <span data-ttu-id="6ba70-307">**ResourceDisk.EnableSwap**</span><span class="sxs-lookup"><span data-stu-id="6ba70-307">**ResourceDisk.EnableSwap**</span></span>
  * <span data-ttu-id="6ba70-308">**ResourceDisk.SwapSizeMB**</span><span class="sxs-lookup"><span data-stu-id="6ba70-308">**ResourceDisk.SwapSizeMB**</span></span>
* <span data-ttu-id="6ba70-309">Zie Hallo resources tooconfigure Hallo resource schijf koppelpunt te volgen en wisselruimte op Ubuntu Cloud installatiekopieën tijdens het inrichten:</span><span class="sxs-lookup"><span data-stu-id="6ba70-309">Please see hello following resources tooconfigure hello resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:</span></span>
  
  * [<span data-ttu-id="6ba70-310">Ubuntu-Wiki: Swap-partities configureren</span><span class="sxs-lookup"><span data-stu-id="6ba70-310">Ubuntu Wiki: Configure Swap Partitions</span></span>](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [<span data-ttu-id="6ba70-311">Injecteren van aangepaste gegevens in Azure een virtuele Machine</span><span class="sxs-lookup"><span data-stu-id="6ba70-311">Injecting Custom Data into an Azure Virtual Machine</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

