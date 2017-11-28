---
title: aaaCreate een VHD en uploaden op basis van CentOS Linux in Azure
description: Informatie over toocreate en uploaden van een Azure virtuele harde schijf (VHD) die een besturingssysteem op basis van CentOS Linux bevat.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 0e518e92-e981-43f4-b12c-9cba1064c4bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 78f36be1d36e3d44cb836c912d143f2c9a72aab5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a><span data-ttu-id="0172a-103">Een op CentOS gebaseerde virtuele Azure-machine voorbereiden</span><span class="sxs-lookup"><span data-stu-id="0172a-103">Prepare a CentOS-based virtual machine for Azure</span></span>
* [<span data-ttu-id="0172a-104">Een CentOS 6.x virtuele machine voorbereiden voor Azure</span><span class="sxs-lookup"><span data-stu-id="0172a-104">Prepare a CentOS 6.x virtual machine for Azure</span></span>](#centos-6x)
* [<span data-ttu-id="0172a-105">Een CentOS 7.0 + virtuele machine voorbereiden voor Azure</span><span class="sxs-lookup"><span data-stu-id="0172a-105">Prepare a CentOS 7.0+ virtual machine for Azure</span></span>](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="0172a-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0172a-106">Prerequisites</span></span>
<span data-ttu-id="0172a-107">In dit artikel wordt ervan uitgegaan dat u al een CentOS hebt geïnstalleerd (of vergelijkbaar afgeleide) Linux-besturingssysteem tooa virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="0172a-107">This article assumes that you have already installed a CentOS (or similar derivative) Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="0172a-108">Meerdere hulpprogramma's bestaan toocreate VHD-bestanden, bijvoorbeeld een virtualisatieoplossing zoals Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0172a-108">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="0172a-109">Zie voor instructies [Hallo Hyper-V-rol installeren en configureren van een virtuele Machine](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="0172a-109">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="0172a-110">**Opmerkingen bij de installatie van centOS**</span><span class="sxs-lookup"><span data-stu-id="0172a-110">**CentOS installation notes**</span></span>

* <span data-ttu-id="0172a-111">Zie ook [algemene opmerkingen bij de installatie van Linux](create-upload-generic.md#general-linux-installation-notes) voor meer tips over Linux voorbereiden voor Azure.</span><span class="sxs-lookup"><span data-stu-id="0172a-111">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="0172a-112">Hallo VHDX-indeling wordt niet ondersteund in Azure, alleen **vaste VHD**.</span><span class="sxs-lookup"><span data-stu-id="0172a-112">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="0172a-113">U kunt converteren Hallo tooVHD schijfindeling met behulp van Hyper-V-beheer of Hallo cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="0172a-113">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span> <span data-ttu-id="0172a-114">Als u van VirtualBox gebruikmaakt betekent dit dat selecteren **een vaste grootte** als geboden toohello standaard dynamisch toegewezen bij het Hallo-schijf maken.</span><span class="sxs-lookup"><span data-stu-id="0172a-114">If you are using VirtualBox this means selecting **Fixed size** as opposed toohello default dynamically allocated when creating hello disk.</span></span>
* <span data-ttu-id="0172a-115">Bij het installeren van Hallo Linux-systeem is *aanbevolen* dat u standaard partities in plaats van LVM (vaak Hallo standaard voor vele installaties gebruikt).</span><span class="sxs-lookup"><span data-stu-id="0172a-115">When installing hello Linux system it is *recommended* that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="0172a-116">Dit voorkomt LVM naam conflicteert met de gekloonde virtuele machines, met name een besturingssysteemschijf ooit toobe gekoppeld tooanother moet identiek zijn VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="0172a-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother identical VM for troubleshooting.</span></span> <span data-ttu-id="0172a-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mag worden gebruikt voor gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="0172a-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="0172a-118">Kernel-ondersteuning voor het koppelen van UDF-bestandssysteem is vereist.</span><span class="sxs-lookup"><span data-stu-id="0172a-118">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="0172a-119">Op de eerste keer opstarten op Azure Hallo inrichting configuratie toohello Linux VM doorgegeven via UDF-indeling media die is aangesloten toohello Gast.</span><span class="sxs-lookup"><span data-stu-id="0172a-119">At first boot on Azure hello provisioning configuration is passed toohello Linux VM via UDF-formatted media that is attached toohello guest.</span></span> <span data-ttu-id="0172a-120">Hello Azure Linux-agent moet worden kunnen toomount Hallo UDF-bestand system tooread de configuratie en Hallo VM inrichten.</span><span class="sxs-lookup"><span data-stu-id="0172a-120">hello Azure Linux agent must be able toomount hello UDF file system tooread its configuration and provision hello VM.</span></span>
* <span data-ttu-id="0172a-121">Kernel-versies van Linux onder 2.6.37 ondersteunen geen NUMA op Hyper-V met grotere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0172a-121">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="0172a-122">Dit probleem voornamelijk effecten oudere distributies Hallo stroomopwaarts met Red Hat 2.6.32 kernel, en is vastgesteld in RHEL 6.6 (kernel 2.6.32 504).</span><span class="sxs-lookup"><span data-stu-id="0172a-122">This issue primarily impacts older distributions using hello upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="0172a-123">Systemen met aangepaste kernels die ouder zijn dan 2.6.37 of op basis van RHEL kernels die ouder zijn dan 2.6.32-504 moet ingesteld Hallo opstarten parameter `numa=off` op Hallo kernel opdrachtregelprogramma in grub.conf.</span><span class="sxs-lookup"><span data-stu-id="0172a-123">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set hello boot parameter `numa=off` on hello kernel command-line in grub.conf.</span></span> <span data-ttu-id="0172a-124">Zie voor meer informatie Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="0172a-124">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="0172a-125">Configureer een partitie van de wisseling niet op Hallo OS-schijf.</span><span class="sxs-lookup"><span data-stu-id="0172a-125">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="0172a-126">Hallo Linux-agent kan worden geconfigureerd toocreate een wisselbestand op Hallo tijdelijke schijf.</span><span class="sxs-lookup"><span data-stu-id="0172a-126">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="0172a-127">Meer informatie hierover vindt u in onderstaande Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="0172a-127">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="0172a-128">Alle VHD's Hallo moeten grootten die veelvouden van 1 MB hebben.</span><span class="sxs-lookup"><span data-stu-id="0172a-128">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="centos-6x"></a><span data-ttu-id="0172a-129">CentOS 6.x</span><span class="sxs-lookup"><span data-stu-id="0172a-129">CentOS 6.x</span></span>

1. <span data-ttu-id="0172a-130">Selecteer Hallo virtuele machine in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="0172a-130">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="0172a-131">Klik op **Connect** tooopen een consolevenster voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0172a-131">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="0172a-132">In CentOS 6, kan NetworkManager hello Azure Linux agent verstoren.</span><span class="sxs-lookup"><span data-stu-id="0172a-132">In CentOS 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="0172a-133">Dit pakket verwijderen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="0172a-133">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="0172a-134">Maken of bewerken Hallo bestand `/etc/sysconfig/network` en voeg de volgende tekst hello:</span><span class="sxs-lookup"><span data-stu-id="0172a-134">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="0172a-135">Maken of bewerken Hallo bestand `/etc/sysconfig/network-scripts/ifcfg-eth0` en voeg de volgende tekst hello:</span><span class="sxs-lookup"><span data-stu-id="0172a-135">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="0172a-136">Wijzig de udev regels tooavoid statische regels voor Hallo Ethernet-interface (s) te genereren.</span><span class="sxs-lookup"><span data-stu-id="0172a-136">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="0172a-137">Deze regels kunnen problemen veroorzaken bij het klonen van een virtuele machine in Microsoft Azure- of Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="0172a-137">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="0172a-138">Zorg ervoor dat Hallo netwerkservice tijdens het opstarten wordt gestart door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="0172a-138">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on

8. <span data-ttu-id="0172a-139">Als u toouse hello OpenLogic mirrors die worden gehost in Azure-datacenters hello dat wilt, vervangt u Hallo `/etc/yum.repos.d/CentOS-Base.repo` bestand met de Hallo opslagplaatsen te volgen.</span><span class="sxs-lookup"><span data-stu-id="0172a-139">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="0172a-140">Hierdoor wordt ook toegevoegd Hallo **[openlogic]** opslagplaats met extra pakketten zoals hello Azure Linux agent:</span><span class="sxs-lookup"><span data-stu-id="0172a-140">This will also add hello **[openlogic]** repository that includes additional packages such as hello Azure Linux agent:</span></span>

        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #contrib - packages by Centos Users
        [contrib]
        name=CentOS-$releasever - Contrib
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=contrib&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/contrib/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

    >[!Note]
    <span data-ttu-id="0172a-141">Hallo rest van deze handleiding wordt wordt ervan uitgegaan dat u ten minste Hallo `[openlogic]` opslagplaats die wordt gebruikt tooinstall hello Azure Linux agent hieronder.</span><span class="sxs-lookup"><span data-stu-id="0172a-141">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>


9. <span data-ttu-id="0172a-142">Hallo regel too/etc/yum.conf volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="0172a-142">Add hello following line too/etc/yum.conf:</span></span>
    
        http_caching=packages

10. <span data-ttu-id="0172a-143">Voer Hallo opdracht tooclear Hallo huidige yum metagegevens en de updatebestanden Hallo systeem met de meest recente hello-pakketten te volgen:</span><span class="sxs-lookup"><span data-stu-id="0172a-143">Run hello following command tooclear hello current yum metadata and update hello system with hello latest packages:</span></span>
    
        # yum clean all

    <span data-ttu-id="0172a-144">Tenzij u een afbeelding voor een oudere versie van CentOS maakt, wordt het aanbevolen om alle Hallo tooupdate pakketten toohello laatste:</span><span class="sxs-lookup"><span data-stu-id="0172a-144">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="0172a-145">Mogelijk opnieuw worden opgestart na het uitvoeren van deze opdracht zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="0172a-145">A reboot may be required after running this command.</span></span>

11. <span data-ttu-id="0172a-146">(Optioneel) Hallo-stuurprogramma's voor Hallo Linux Integration Services (LIS) installeren.</span><span class="sxs-lookup"><span data-stu-id="0172a-146">(Optional) Install hello drivers for hello Linux Integration Services (LIS).</span></span>
   
    >[!IMPORTANT]
    <span data-ttu-id="0172a-147">Hallo stap is **vereist** voor CentOS 6.3 en lager en optioneel voor latere versies.</span><span class="sxs-lookup"><span data-stu-id="0172a-147">hello step is **required** for CentOS 6.3 and earlier, and optional for later releases.</span></span>

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    <span data-ttu-id="0172a-148">U kunt ook Hallo handmatige installatie-instructies volgen op Hallo [LIS downloadpagina](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall Hallo RPM naar uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0172a-148">Alternatively, you can follow hello manual installation instructions on hello [LIS download page](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello RPM onto your VM.</span></span>
 
12. <span data-ttu-id="0172a-149">Installeer de hello Azure Linux Agent en afhankelijkheden:</span><span class="sxs-lookup"><span data-stu-id="0172a-149">Install hello Azure Linux Agent and dependencies:</span></span>
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    <span data-ttu-id="0172a-150">Hallo WALinuxAgent pakket verwijdert, Hallo NetworkManager en NetworkManager gnome pakketten als ze zoals beschreven in stap 3 niet al zijn verwijderd.</span><span class="sxs-lookup"><span data-stu-id="0172a-150">hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 3.</span></span>


13. <span data-ttu-id="0172a-151">Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen.</span><span class="sxs-lookup"><span data-stu-id="0172a-151">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="0172a-152">toodo deze, open `/boot/grub/menu.lst` in een teksteditor en zorg ervoor dat standaard Hallo kernel bevat Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="0172a-152">toodo this, open `/boot/grub/menu.lst` in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="0172a-153">Hiermee zorgt u ervoor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="0172a-153">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="0172a-154">Bovendien toohello hierboven, het is raadzaam te*verwijderen* Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="0172a-154">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="0172a-155">Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort.</span><span class="sxs-lookup"><span data-stu-id="0172a-155">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="0172a-156">Hallo `crashkernel` mogelijk links geconfigureerd indien gewenst, maar dat deze parameter verminderen Hallo en de hoeveelheid beschikbaar geheugen in Hallo VM 128 MB of meer, die mogelijk problemen op Hallo kleinere VM opmerking.</span><span class="sxs-lookup"><span data-stu-id="0172a-156">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

    >[!Important]
    <span data-ttu-id="0172a-157">CentOS 6.5 en eerdere moeten ook worden ingesteld Hallo kernel parameter `numa=off`.</span><span class="sxs-lookup"><span data-stu-id="0172a-157">CentOS 6.5 and earlier must also set hello kernel parameter `numa=off`.</span></span> <span data-ttu-id="0172a-158">Red Hat Zie [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="0172a-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

14. <span data-ttu-id="0172a-159">Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="0172a-159">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="0172a-160">Dit is meestal Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="0172a-160">This is usually hello default.</span></span>

15. <span data-ttu-id="0172a-161">Maak geen wisselruimte op Hallo OS-schijf.</span><span class="sxs-lookup"><span data-stu-id="0172a-161">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="0172a-162">Hello Azure Linux Agent kunt wisselruimte Hallo lokale resource schijf die is aangesloten toohello VM na het inrichten op Azure automatisch configureren.</span><span class="sxs-lookup"><span data-stu-id="0172a-162">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="0172a-163">Houd er rekening mee dat lokale resource Hallo schijf is een *tijdelijke* schijfruimte en kan worden leeggemaakt wanneer Hallo VM gemaakt is.</span><span class="sxs-lookup"><span data-stu-id="0172a-163">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="0172a-164">Na de installatie van hello Azure Linux Agent (Zie de vorige stap), wijzigen van de volgende parameters in Hallo `/etc/waagent.conf` op de juiste wijze:</span><span class="sxs-lookup"><span data-stu-id="0172a-164">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="0172a-165">Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="0172a-165">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. <span data-ttu-id="0172a-166">Klik op **actie-Afsluiten > omlaag** in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="0172a-166">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="0172a-167">Uw Linux VHD is nu gereed toobe tooAzure geüpload.</span><span class="sxs-lookup"><span data-stu-id="0172a-167">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


- - -
## <a name="centos-70"></a><span data-ttu-id="0172a-168">CentOS 7.0 +</span><span class="sxs-lookup"><span data-stu-id="0172a-168">CentOS 7.0+</span></span>
<span data-ttu-id="0172a-169">**Wijzigingen in CentOS 7 (en vergelijkbare afgeleiden)**</span><span class="sxs-lookup"><span data-stu-id="0172a-169">**Changes in CentOS 7 (and similar derivatives)**</span></span>

<span data-ttu-id="0172a-170">Een CentOS 7 virtuele machine voorbereiden voor Azure is heel vergelijkbaar tooCentOS 6, maar er zijn echter enkele belangrijke verschillen opgemerkt:</span><span class="sxs-lookup"><span data-stu-id="0172a-170">Preparing a CentOS 7 virtual machine for Azure is very similar tooCentOS 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="0172a-171">Hallo NetworkManager van het pakket niet meer veroorzaakt een conflict met hello Azure Linux-agent.</span><span class="sxs-lookup"><span data-stu-id="0172a-171">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="0172a-172">Dit pakket wordt standaard geïnstalleerd en wordt aangeraden deze niet is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="0172a-172">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="0172a-173">GRUB2 wordt nu gebruikt als Hallo standaard bootloader, zodat het Hallo-procedure voor het bewerken van de kernel parameters is gewijzigd (Zie hieronder).</span><span class="sxs-lookup"><span data-stu-id="0172a-173">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="0172a-174">XFS is nu Hallo standaardbestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="0172a-174">XFS is now hello default file system.</span></span> <span data-ttu-id="0172a-175">Hallo ext4 bestandssysteem kan nog steeds worden gebruikt, indien gewenst.</span><span class="sxs-lookup"><span data-stu-id="0172a-175">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="0172a-176">**Configuratiestappen**</span><span class="sxs-lookup"><span data-stu-id="0172a-176">**Configuration Steps**</span></span>

1. <span data-ttu-id="0172a-177">Selecteer Hallo virtuele machine in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="0172a-177">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="0172a-178">Klik op **Connect** tooopen een consolevenster voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0172a-178">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="0172a-179">Maken of bewerken Hallo bestand `/etc/sysconfig/network` en voeg de volgende tekst hello:</span><span class="sxs-lookup"><span data-stu-id="0172a-179">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="0172a-180">Maken of bewerken Hallo bestand `/etc/sysconfig/network-scripts/ifcfg-eth0` en voeg de volgende tekst hello:</span><span class="sxs-lookup"><span data-stu-id="0172a-180">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="0172a-181">Wijzig de udev regels tooavoid statische regels voor Hallo Ethernet-interface (s) te genereren.</span><span class="sxs-lookup"><span data-stu-id="0172a-181">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="0172a-182">Deze regels kunnen problemen veroorzaken bij het klonen van een virtuele machine in Microsoft Azure- of Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="0172a-182">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. <span data-ttu-id="0172a-183">Als u toouse hello OpenLogic mirrors die worden gehost in Azure-datacenters hello dat wilt, vervangt u Hallo `/etc/yum.repos.d/CentOS-Base.repo` bestand met de Hallo opslagplaatsen te volgen.</span><span class="sxs-lookup"><span data-stu-id="0172a-183">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="0172a-184">Hierdoor wordt ook toegevoegd Hallo **[openlogic]** opslagplaats met pakketten voor hello Azure Linux agent:</span><span class="sxs-lookup"><span data-stu-id="0172a-184">This will also add hello **[openlogic]** repository that includes packages for hello Azure Linux agent:</span></span>
   
        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

    >[!Note]
    <span data-ttu-id="0172a-185">Hallo rest van deze handleiding wordt wordt ervan uitgegaan dat u ten minste Hallo `[openlogic]` opslagplaats die wordt gebruikt tooinstall hello Azure Linux agent hieronder.</span><span class="sxs-lookup"><span data-stu-id="0172a-185">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>

7. <span data-ttu-id="0172a-186">Voer Hallo opdracht tooclear Hallo huidige yum metagegevens te volgen en geen updates installeren:</span><span class="sxs-lookup"><span data-stu-id="0172a-186">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all

    <span data-ttu-id="0172a-187">Tenzij u een afbeelding voor een oudere versie van CentOS maakt, wordt het aanbevolen om alle Hallo tooupdate pakketten toohello laatste:</span><span class="sxs-lookup"><span data-stu-id="0172a-187">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="0172a-188">Een opnieuw opstarten is mogelijk vereist na het uitvoeren van deze opdracht.</span><span class="sxs-lookup"><span data-stu-id="0172a-188">A reboot maybe required after running this command.</span></span>

8. <span data-ttu-id="0172a-189">Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen.</span><span class="sxs-lookup"><span data-stu-id="0172a-189">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="0172a-190">toodo deze, open `/etc/default/grub` in een tekst-editor en bewerk Hallo `GRUB_CMDLINE_LINUX` parameter, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0172a-190">toodo this, open `/etc/default/grub` in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="0172a-191">Hiermee zorgt u ervoor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="0172a-191">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="0172a-192">Het ook uitgeschakeld Hallo nieuwe CentOS 7 naamgevingsregels voor NIC's.</span><span class="sxs-lookup"><span data-stu-id="0172a-192">It also turns off hello new CentOS 7 naming conventions for NICs.</span></span> <span data-ttu-id="0172a-193">Bovendien toohello hierboven, het is raadzaam te*verwijderen* Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="0172a-193">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="0172a-194">Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort.</span><span class="sxs-lookup"><span data-stu-id="0172a-194">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="0172a-195">Hallo `crashkernel` mogelijk links geconfigureerd indien gewenst, maar dat deze parameter verminderen Hallo en de hoeveelheid beschikbaar geheugen in Hallo VM 128 MB of meer, die mogelijk problemen op Hallo kleinere VM opmerking.</span><span class="sxs-lookup"><span data-stu-id="0172a-195">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

9. <span data-ttu-id="0172a-196">Wanneer u klaar bent bewerken `/etc/default/grub` per hierboven uitgevoerd Hallo toorebuild Hallo wormgaten configuratie te volgen:</span><span class="sxs-lookup"><span data-stu-id="0172a-196">Once you are done editing `/etc/default/grub` per above, run hello following command toorebuild hello grub configuration:</span></span>
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="0172a-197">Als de installatiekopie van het Hallo van bouwt **VMWare, VirtualBox of KVM:** Controleer Hallo Hyper-V-stuurprogramma's zijn opgenomen in Hallo initramfs:</span><span class="sxs-lookup"><span data-stu-id="0172a-197">If building hello image from **VMWare, VirtualBox or KVM:** Ensure hello Hyper-V drivers are included in hello initramfs:</span></span>
   
   <span data-ttu-id="0172a-198">Bewerken `/etc/dracut.conf`, inhoud toevoegen:</span><span class="sxs-lookup"><span data-stu-id="0172a-198">Edit `/etc/dracut.conf`, add content:</span></span>
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   <span data-ttu-id="0172a-199">Hallo initramfs bouwen:</span><span class="sxs-lookup"><span data-stu-id="0172a-199">Rebuild hello initramfs:</span></span>
   
        # sudo dracut –f -v

11. <span data-ttu-id="0172a-200">Installeer de hello Azure Linux Agent en afhankelijkheden:</span><span class="sxs-lookup"><span data-stu-id="0172a-200">Install hello Azure Linux Agent and dependencies:</span></span>

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. <span data-ttu-id="0172a-201">Maak geen wisselruimte op Hallo OS-schijf.</span><span class="sxs-lookup"><span data-stu-id="0172a-201">Do not create swap space on hello OS disk.</span></span>
   
   <span data-ttu-id="0172a-202">Hello Azure Linux Agent kunt wisselruimte Hallo lokale resource schijf die is aangesloten toohello VM na het inrichten op Azure automatisch configureren.</span><span class="sxs-lookup"><span data-stu-id="0172a-202">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="0172a-203">Houd er rekening mee dat lokale resource Hallo schijf is een *tijdelijke* schijfruimte en kan worden leeggemaakt wanneer Hallo VM gemaakt is.</span><span class="sxs-lookup"><span data-stu-id="0172a-203">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="0172a-204">Na de installatie van hello Azure Linux Agent (Zie de vorige stap), wijzigen van de volgende parameters in Hallo `/etc/waagent.conf` op de juiste wijze:</span><span class="sxs-lookup"><span data-stu-id="0172a-204">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="0172a-205">Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="0172a-205">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. <span data-ttu-id="0172a-206">Klik op **actie-Afsluiten > omlaag** in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="0172a-206">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="0172a-207">Uw Linux VHD is nu gereed toobe tooAzure geüpload.</span><span class="sxs-lookup"><span data-stu-id="0172a-207">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0172a-208">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0172a-208">Next steps</span></span>
<span data-ttu-id="0172a-209">U bent nu klaar toouse uw CentOS Linux virtuele harde schijf toocreate nieuwe virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="0172a-209">You're now ready toouse your CentOS Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="0172a-210">Als dit Hallo eerste keer dat u Hallo .vhd-bestand tooAzure uploadt, Zie de stappen 2 en 3 in [maken en uploaden van een virtuele harde schijf waarop Linux-besturingssysteem Hallo](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0172a-210">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

