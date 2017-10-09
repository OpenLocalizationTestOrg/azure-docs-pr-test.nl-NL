---
title: aaaCreate en een Oracle Linux VHD uploaden | Microsoft Docs
description: Informatie over toocreate en uploaden van een Azure virtuele harde schijf (VHD) met een Oracle Linux-besturingssysteem.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: dd96f771-26eb-4391-9a89-8c8b6d691822
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: szark
ms.openlocfilehash: be9cf284d7f5e7122a106506a343e53e9f1ac56e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a><span data-ttu-id="a5e1f-103">Een virtuele Oracle Linux-machine voor Azure voorbereiden</span><span class="sxs-lookup"><span data-stu-id="a5e1f-103">Prepare an Oracle Linux virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="a5e1f-104">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a5e1f-104">Prerequisites</span></span>
<span data-ttu-id="a5e1f-105">In dit artikel wordt ervan uitgegaan dat u al een Oracle Linux-besturingssysteem tooa virtuele harde schijf hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-105">This article assumes that you have already installed an Oracle Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="a5e1f-106">Meerdere hulpprogramma's bestaan toocreate VHD-bestanden, bijvoorbeeld een virtualisatieoplossing zoals Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="a5e1f-107">Zie voor instructies [Hallo Hyper-V-rol installeren en configureren van een virtuele Machine](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5e1f-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="oracle-linux-installation-notes"></a><span data-ttu-id="a5e1f-108">Opmerkingen bij de installatie van de Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="a5e1f-108">Oracle Linux installation notes</span></span>
* <span data-ttu-id="a5e1f-109">Zie ook [algemene opmerkingen bij de installatie van Linux](create-upload-generic.md#general-linux-installation-notes) voor meer tips over Linux voorbereiden voor Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="a5e1f-110">Oracle van Red Hat compatibel kernel en hun UEK3 (Unbreakable Enterprise Kernel) worden beide ondersteund op Hyper-V en Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-110">Oracle's Red Hat compatible kernel and their UEK3 (Unbreakable Enterprise Kernel) are both supported on Hyper-V and Azure.</span></span> <span data-ttu-id="a5e1f-111">Zorg ervoor dat tooupdate toohello nieuwste kernel tijdens het voorbereiden van uw Oracle Linux VHD voor de beste resultaten.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-111">For best results, please be sure tooupdate toohello latest kernel while preparing your Oracle Linux VHD.</span></span>
* <span data-ttu-id="a5e1f-112">UEK2 van Oracle wordt niet ondersteund op Hyper-V en Azure zoals geen stuurprogramma's Hallo vereist bevat.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-112">Oracle's UEK2 is not supported on Hyper-V and Azure as it does not include hello required drivers.</span></span>
* <span data-ttu-id="a5e1f-113">Hallo VHDX-indeling wordt niet ondersteund in Azure, alleen **vaste VHD**.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-113">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="a5e1f-114">U kunt converteren Hallo tooVHD schijfindeling met behulp van Hyper-V-beheer of Hallo cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-114">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="a5e1f-115">Bij het installeren van Hallo Linux-systeem wordt het aanbevolen dat u standaard partities in plaats van LVM (vaak Hallo standaard voor vele installaties gebruikt).</span><span class="sxs-lookup"><span data-stu-id="a5e1f-115">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="a5e1f-116">Dit voorkomt LVM naam conflicteert met de gekloonde virtuele machines, met name een besturingssysteemschijf ooit moet toobe gekoppeld tooanother VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="a5e1f-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mag worden gebruikt voor gegevensschijven als voorkeur.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="a5e1f-118">NUMA wordt niet ondersteund voor grotere VM-groottes vanwege tooa fout in de kernel-versies van Linux onder 2.6.37.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-118">NUMA is not supported for larger VM sizes due tooa bug in Linux kernel versions below 2.6.37.</span></span> <span data-ttu-id="a5e1f-119">Dit probleem voornamelijk effecten distributies met Hallo upstream Red Hat 2.6.32 kernel.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-119">This issue primarily impacts distributions using hello upstream Red Hat 2.6.32 kernel.</span></span> <span data-ttu-id="a5e1f-120">Handmatige installatie van hello Azure Linux-agent (waagent) wordt automatisch NUMA uitgeschakeld in Hallo WORMGATEN configuratie voor Hallo Linux kernel.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-120">Manual installation of hello Azure Linux agent (waagent) will automatically disable NUMA in hello GRUB configuration for hello Linux kernel.</span></span> <span data-ttu-id="a5e1f-121">Meer informatie hierover vindt u in onderstaande Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-121">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="a5e1f-122">Configureer een partitie van de wisseling niet op Hallo OS-schijf.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="a5e1f-123">Hallo Linux-agent kan worden geconfigureerd toocreate een wisselbestand op Hallo tijdelijke schijf.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="a5e1f-124">Meer informatie hierover vindt u in onderstaande Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="a5e1f-125">Alle VHD's Hallo moeten grootten die veelvouden van 1 MB hebben.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>
* <span data-ttu-id="a5e1f-126">Zorg ervoor dat Hallo `Addons` opslagplaats is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-126">Make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="a5e1f-127">Hallo-bestand bewerken `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) of `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux), en wijzig Hallo regel `enabled=0` te`enabled=1` onder **[ol6_addons]** of **[ol7_addons]** in deze het bestand.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-127">Edit hello file `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux ), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

## <a name="oracle-linux-64"></a><span data-ttu-id="a5e1f-128">Oracle Linux 6.4 +</span><span class="sxs-lookup"><span data-stu-id="a5e1f-128">Oracle Linux 6.4+</span></span>
<span data-ttu-id="a5e1f-129">U moet de specifieke configuratiestappen in Hallo besturingssysteem Hallo virtuele machine toorun in Azure voltooien.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-129">You must complete specific configuration steps in hello operating system for hello virtual machine toorun in Azure.</span></span>

1. <span data-ttu-id="a5e1f-130">Selecteer Hallo virtuele machine in Hallo middelste deelvenster van de Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-130">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="a5e1f-131">Klik op **Connect** tooopen Hallo venster voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-131">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="a5e1f-132">NetworkManager verwijderen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-132">Uninstall NetworkManager by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager
   
    <span data-ttu-id="a5e1f-133">**Opmerking:** als Hallo pakket nog niet is geïnstalleerd, deze opdracht mislukt met een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-133">**Note:** If hello package is not already installed, this command will fail with an error message.</span></span> <span data-ttu-id="a5e1f-134">Dit is normaal.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-134">This is expected.</span></span>
4. <span data-ttu-id="a5e1f-135">Maak een bestand met de naam **netwerk** in Hallo `/etc/sysconfig/` map waarin zich de volgende tekst hello:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-135">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. <span data-ttu-id="a5e1f-136">Maak een bestand met de naam **ifcfg eth0** in Hallo `/etc/sysconfig/network-scripts/` map waarin zich de volgende tekst hello:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-136">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. <span data-ttu-id="a5e1f-137">Wijzig de udev regels tooavoid statische regels voor Hallo Ethernet-interface (s) te genereren.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-137">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="a5e1f-138">Deze regels kunnen problemen veroorzaken bij het klonen van een virtuele machine in Microsoft Azure- of Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-138">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. <span data-ttu-id="a5e1f-139">Zorg ervoor dat Hallo netwerkservice tijdens het opstarten wordt gestart door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-139">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # chkconfig network on
8. <span data-ttu-id="a5e1f-140">Python-pyasn1 door het uitvoeren van de volgende opdracht Hallo installeren:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-140">Install python-pyasn1 by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
9. <span data-ttu-id="a5e1f-141">Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-141">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="a5e1f-142">dit open toodo ' / boot/grub/menu.lst ' in een teksteditor en zorg ervoor dat standaard Hallo kernel bevat Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-142">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   <span data-ttu-id="a5e1f-143">Hiermee zorgt u ervoor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-143">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="a5e1f-144">Hiermee wordt het NUMA uitgeschakeld vanwege tooa fout in Oracle van Red Hat compatibel kernel.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-144">This will disable NUMA due tooa bug in Oracle's Red Hat compatible kernel.</span></span>
   
   <span data-ttu-id="a5e1f-145">Bovendien toohello hierboven, het is raadzaam te*verwijderen* Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-145">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
   <span data-ttu-id="a5e1f-146">Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-146">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="a5e1f-147">Hallo `crashkernel` mogelijk links geconfigureerd indien gewenst, maar dat deze parameter verminderen Hallo en de hoeveelheid beschikbaar geheugen in Hallo VM 128 MB of meer, die mogelijk problemen op Hallo kleinere VM opmerking.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-147">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="a5e1f-148">Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="a5e1f-149">Dit is meestal Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-149">This is usually hello default.</span></span>
11. <span data-ttu-id="a5e1f-150">Hello Azure Linux Agent installeren door het uitvoeren van de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-150">Install hello Azure Linux Agent by running hello following command.</span></span> <span data-ttu-id="a5e1f-151">Hallo meest recente versie is 2.0.15.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-151">hello latest version is 2.0.15.</span></span>
    
        # sudo yum install WALinuxAgent
    
    <span data-ttu-id="a5e1f-152">Houd er rekening mee dat installeren Hallo WALinuxAgent pakket Hallo NetworkManager wordt verwijderd en NetworkManager gnome pakketten als ze zijn niet al verwijderd zoals beschreven in stap 2.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-152">Note that installing hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 2.</span></span>
12. <span data-ttu-id="a5e1f-153">Maak geen wisselruimte op Hallo OS-schijf.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-153">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="a5e1f-154">Hello Azure Linux Agent kunt wisselruimte Hallo lokale resource schijf die is aangesloten toohello VM na het inrichten op Azure automatisch configureren.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-154">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="a5e1f-155">Houd er rekening mee dat lokale resource Hallo schijf is een *tijdelijke* schijfruimte en kan worden leeggemaakt wanneer Hallo VM gemaakt is.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-155">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="a5e1f-156">Na de installatie van hello Azure Linux Agent (Zie de vorige stap), wijzigen Hallo-parameters in /etc/waagent.conf op de juiste wijze te volgen:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-156">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
13. <span data-ttu-id="a5e1f-157">Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-157">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. <span data-ttu-id="a5e1f-158">Klik op **actie-Afsluiten > omlaag** in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-158">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="a5e1f-159">Uw Linux VHD is nu gereed toobe tooAzure geüpload.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-159">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="oracle-linux-70"></a><span data-ttu-id="a5e1f-160">Oracle Linux 7.0 +</span><span class="sxs-lookup"><span data-stu-id="a5e1f-160">Oracle Linux 7.0+</span></span>
<span data-ttu-id="a5e1f-161">**Wijzigingen in Oracle Linux 7**</span><span class="sxs-lookup"><span data-stu-id="a5e1f-161">**Changes in Oracle Linux 7**</span></span>

<span data-ttu-id="a5e1f-162">Een virtuele machine van de Oracle Linux 7 voorbereiden voor Azure is heel vergelijkbaar tooOracle Linux 6, maar er zijn echter enkele belangrijke verschillen opgemerkt:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-162">Preparing an Oracle Linux 7 virtual machine for Azure is very similar tooOracle Linux 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="a5e1f-163">Hallo Red Hat compatibel kernel zowel van Oracle UEK3 worden ondersteund in Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-163">Both hello Red Hat compatible kernel and Oracle's UEK3 are supported in Azure.</span></span>  <span data-ttu-id="a5e1f-164">Hallo UEK3 kernel wordt aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-164">hello UEK3 kernel is recommended.</span></span>
* <span data-ttu-id="a5e1f-165">Hallo NetworkManager van het pakket niet meer veroorzaakt een conflict met hello Azure Linux-agent.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-165">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="a5e1f-166">Dit pakket wordt standaard geïnstalleerd en wordt aangeraden deze niet is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-166">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="a5e1f-167">GRUB2 wordt nu gebruikt als Hallo standaard bootloader, zodat het Hallo-procedure voor het bewerken van de kernel parameters is gewijzigd (Zie hieronder).</span><span class="sxs-lookup"><span data-stu-id="a5e1f-167">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="a5e1f-168">XFS is nu Hallo standaardbestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-168">XFS is now hello default file system.</span></span> <span data-ttu-id="a5e1f-169">Hallo ext4 bestandssysteem kan nog steeds worden gebruikt, indien gewenst.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-169">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="a5e1f-170">**Configuratiestappen**</span><span class="sxs-lookup"><span data-stu-id="a5e1f-170">**Configuration steps**</span></span>

1. <span data-ttu-id="a5e1f-171">Selecteer Hallo virtuele machine in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-171">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="a5e1f-172">Klik op **Connect** tooopen een consolevenster voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-172">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="a5e1f-173">Maak een bestand met de naam **netwerk** in Hallo `/etc/sysconfig/` map waarin zich de volgende tekst hello:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-173">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. <span data-ttu-id="a5e1f-174">Maak een bestand met de naam **ifcfg eth0** in Hallo `/etc/sysconfig/network-scripts/` map waarin zich de volgende tekst hello:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-174">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. <span data-ttu-id="a5e1f-175">Wijzig de udev regels tooavoid statische regels voor Hallo Ethernet-interface (s) te genereren.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-175">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="a5e1f-176">Deze regels kunnen problemen veroorzaken bij het klonen van een virtuele machine in Microsoft Azure- of Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-176">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. <span data-ttu-id="a5e1f-177">Zorg ervoor dat Hallo netwerkservice tijdens het opstarten wordt gestart door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-177">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on
7. <span data-ttu-id="a5e1f-178">Hallo python pyasn1 pakket installeren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-178">Install hello python-pyasn1 package by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
8. <span data-ttu-id="a5e1f-179">Voer Hallo opdracht tooclear Hallo huidige yum metagegevens te volgen en geen updates installeren:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-179">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all
        # sudo yum -y update
9. <span data-ttu-id="a5e1f-180">Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-180">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="a5e1f-181">toodo dat openen '/ standaard/etc/grub' in een tekst-editor en bewerk Hallo `GRUB_CMDLINE_LINUX` parameter, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-181">toodo this open "/etc/default/grub" in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="a5e1f-182">Hiermee zorgt u ervoor dat alle consoleberichten toohello eerste seriële poort, die Azure helpen kan worden verzonden ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-182">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="a5e1f-183">Het ook uitgeschakeld Hallo nieuwe indicatie 7 naamgevingsregels voor NIC's.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-183">It also turns off hello new OEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="a5e1f-184">Bovendien toohello hierboven, het is raadzaam te*verwijderen* Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-184">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
       rhgb quiet crashkernel=auto
   
   <span data-ttu-id="a5e1f-185">Grafische en stil opstarten zijn niet handig in een omgeving waar we alle Hallo logboeken toobe verzonden toohello seriële poort.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-185">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="a5e1f-186">Hallo `crashkernel` mogelijk links geconfigureerd indien gewenst, maar dat deze parameter verminderen Hallo en de hoeveelheid beschikbaar geheugen in Hallo VM 128 MB of meer, die mogelijk problemen op Hallo kleinere VM opmerking.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-186">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="a5e1f-187">Wanneer u klaar bent editing '/ standaard/etc/grub' uitgevoerd per hierboven Hallo toorebuild Hallo wormgaten configuratie te volgen:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-187">Once you are done editing "/etc/default/grub" per above, run hello following command toorebuild hello grub configuration:</span></span>
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. <span data-ttu-id="a5e1f-188">Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-188">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="a5e1f-189">Dit is meestal Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-189">This is usually hello default.</span></span>
12. <span data-ttu-id="a5e1f-190">Hello Azure Linux Agent installeren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-190">Install hello Azure Linux Agent by running hello following command:</span></span>
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. <span data-ttu-id="a5e1f-191">Maak geen wisselruimte op Hallo OS-schijf.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-191">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="a5e1f-192">Hello Azure Linux Agent kunt wisselruimte Hallo lokale resource schijf die is aangesloten toohello VM na het inrichten op Azure automatisch configureren.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-192">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="a5e1f-193">Houd er rekening mee dat lokale resource Hallo schijf is een *tijdelijke* schijfruimte en kan worden leeggemaakt wanneer Hallo VM gemaakt is.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-193">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="a5e1f-194">Na de installatie van hello Azure Linux Agent (Zie de vorige stap Hallo), wijzigen Hallo-parameters in /etc/waagent.conf op de juiste wijze te volgen:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-194">After installing hello Azure Linux Agent (see hello previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. <span data-ttu-id="a5e1f-195">Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="a5e1f-195">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. <span data-ttu-id="a5e1f-196">Klik op **actie-Afsluiten > omlaag** in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-196">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="a5e1f-197">Uw Linux VHD is nu gereed toobe tooAzure geüpload.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-197">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5e1f-198">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a5e1f-198">Next steps</span></span>
<span data-ttu-id="a5e1f-199">U bent nu klaar toouse uw Oracle Linux .vhd toocreate nieuwe virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e1f-199">You're now ready toouse your Oracle Linux .vhd toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="a5e1f-200">Als dit Hallo eerste keer dat u Hallo .vhd-bestand tooAzure uploadt, Zie de stappen 2 en 3 in [maken en uploaden van een virtuele harde schijf waarop Linux-besturingssysteem Hallo](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a5e1f-200">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

