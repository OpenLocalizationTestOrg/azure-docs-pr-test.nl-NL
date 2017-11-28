---
title: Maken en uploaden van een VHD van Oracle Linux | Microsoft Docs
description: Informatie over het maken en uploaden van een Azure virtuele harde schijf (VHD) met een Oracle Linux-besturingssysteem.
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
ms.openlocfilehash: c631ddf3acf6df7364c03eb4691b78be0493e0d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a><span data-ttu-id="3bda6-103">Een virtuele Oracle Linux-machine voor Azure voorbereiden</span><span class="sxs-lookup"><span data-stu-id="3bda6-103">Prepare an Oracle Linux virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="3bda6-104">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3bda6-104">Prerequisites</span></span>
<span data-ttu-id="3bda6-105">In dit artikel wordt ervan uitgegaan dat u al een Oracle Linux-besturingssysteem hebt geïnstalleerd op een virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="3bda6-105">This article assumes that you have already installed an Oracle Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="3bda6-106">Er bestaan meerdere hulpprogramma's voor het maken van de VHD-bestanden, bijvoorbeeld een virtualisatieoplossing zoals Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="3bda6-106">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="3bda6-107">Zie voor instructies [de Hyper-V-rol installeren en configureren van een virtuele Machine](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="3bda6-107">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="oracle-linux-installation-notes"></a><span data-ttu-id="3bda6-108">Opmerkingen bij de installatie van de Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="3bda6-108">Oracle Linux installation notes</span></span>
* <span data-ttu-id="3bda6-109">Zie ook [algemene opmerkingen bij de installatie van Linux](create-upload-generic.md#general-linux-installation-notes) voor meer tips over Linux voorbereiden voor Azure.</span><span class="sxs-lookup"><span data-stu-id="3bda6-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="3bda6-110">Oracle van Red Hat compatibel kernel en hun UEK3 (Unbreakable Enterprise Kernel) worden beide ondersteund op Hyper-V en Azure.</span><span class="sxs-lookup"><span data-stu-id="3bda6-110">Oracle's Red Hat compatible kernel and their UEK3 (Unbreakable Enterprise Kernel) are both supported on Hyper-V and Azure.</span></span> <span data-ttu-id="3bda6-111">Voor de beste resultaten u wordt aangeraden om bij te werken naar de meest recente kernel tijdens het voorbereiden van uw Oracle Linux-VHD.</span><span class="sxs-lookup"><span data-stu-id="3bda6-111">For best results, please be sure to update to the latest kernel while preparing your Oracle Linux VHD.</span></span>
* <span data-ttu-id="3bda6-112">UEK2 van Oracle wordt niet ondersteund op Hyper-V en Azure als u beschikt niet over de vereiste stuurprogramma's.</span><span class="sxs-lookup"><span data-stu-id="3bda6-112">Oracle's UEK2 is not supported on Hyper-V and Azure as it does not include the required drivers.</span></span>
* <span data-ttu-id="3bda6-113">De VHDX-indeling wordt niet ondersteund in Azure, alleen **vaste VHD**.</span><span class="sxs-lookup"><span data-stu-id="3bda6-113">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="3bda6-114">U kunt de schijf converteren naar VHD-indeling met behulp van Hyper-V-beheer of de cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="3bda6-114">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="3bda6-115">Bij het installeren van de Linux-systeem wordt het aanbevolen dat u standaard partities in plaats van LVM (vaak de standaardinstelling voor vele installaties gebruikt).</span><span class="sxs-lookup"><span data-stu-id="3bda6-115">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="3bda6-116">Dit voorkomt LVM naam conflicteert met de gekloonde virtuele machines, met name als een besturingssysteemschijf ooit worden gekoppeld aan een andere virtuele machine moet voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="3bda6-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="3bda6-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mag worden gebruikt voor gegevensschijven als voorkeur.</span><span class="sxs-lookup"><span data-stu-id="3bda6-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="3bda6-118">NUMA wordt niet ondersteund voor grotere virtuele machine vanwege een fout in de kernel-versies van Linux onder 2.6.37.</span><span class="sxs-lookup"><span data-stu-id="3bda6-118">NUMA is not supported for larger VM sizes due to a bug in Linux kernel versions below 2.6.37.</span></span> <span data-ttu-id="3bda6-119">Dit probleem hoofdzakelijk van invloed is op distributies met behulp van de upstream Red Hat 2.6.32 kernel.</span><span class="sxs-lookup"><span data-stu-id="3bda6-119">This issue primarily impacts distributions using the upstream Red Hat 2.6.32 kernel.</span></span> <span data-ttu-id="3bda6-120">Handmatige installatie van de Azure Linux-agent (waagent) wordt automatisch NUMA uitgeschakeld in de configuratie GRUB voor de Linux-kernel.</span><span class="sxs-lookup"><span data-stu-id="3bda6-120">Manual installation of the Azure Linux agent (waagent) will automatically disable NUMA in the GRUB configuration for the Linux kernel.</span></span> <span data-ttu-id="3bda6-121">Meer informatie hierover vindt u in de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="3bda6-121">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="3bda6-122">Configureer een partitie van de wisseling niet op de schijf met het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="3bda6-122">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="3bda6-123">De Linux-agent kan worden geconfigureerd voor het maken van een wisselbestand op de tijdelijke schijf.</span><span class="sxs-lookup"><span data-stu-id="3bda6-123">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="3bda6-124">Meer informatie hierover vindt u in de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="3bda6-124">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="3bda6-125">Alle van de VHD's moeten grootten die veelvouden van 1 MB hebben.</span><span class="sxs-lookup"><span data-stu-id="3bda6-125">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>
* <span data-ttu-id="3bda6-126">Zorg ervoor dat de `Addons` opslagplaats is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3bda6-126">Make sure that the `Addons` repository is enabled.</span></span> <span data-ttu-id="3bda6-127">Bewerk het bestand `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) of `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux), en wijzigt u de regel `enabled=0` naar `enabled=1` onder **[ol6_addons]** of **[ol7_addons]** in dit bestand.</span><span class="sxs-lookup"><span data-stu-id="3bda6-127">Edit the file `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux ), and change the line `enabled=0` to `enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

## <a name="oracle-linux-64"></a><span data-ttu-id="3bda6-128">Oracle Linux 6.4 +</span><span class="sxs-lookup"><span data-stu-id="3bda6-128">Oracle Linux 6.4+</span></span>
<span data-ttu-id="3bda6-129">U moet specifieke configuratiestappen in het besturingssysteem voor de virtuele machine in Azure uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="3bda6-129">You must complete specific configuration steps in the operating system for the virtual machine to run in Azure.</span></span>

1. <span data-ttu-id="3bda6-130">Selecteer in het middelste deelvenster van de Hyper-V-beheer, de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3bda6-130">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="3bda6-131">Klik op **Connect** om het venster voor de virtuele machine te openen.</span><span class="sxs-lookup"><span data-stu-id="3bda6-131">Click **Connect** to open the window for the virtual machine.</span></span>
3. <span data-ttu-id="3bda6-132">NetworkManager verwijderen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3bda6-132">Uninstall NetworkManager by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager
   
    <span data-ttu-id="3bda6-133">**Opmerking:** als het pakket nog niet is geïnstalleerd, deze opdracht mislukt met een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3bda6-133">**Note:** If the package is not already installed, this command will fail with an error message.</span></span> <span data-ttu-id="3bda6-134">Dit is normaal.</span><span class="sxs-lookup"><span data-stu-id="3bda6-134">This is expected.</span></span>
4. <span data-ttu-id="3bda6-135">Maak een bestand met de naam **netwerk** in de `/etc/sysconfig/` map waarin zich de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="3bda6-135">Create a file named **network** in the `/etc/sysconfig/` directory that contains the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. <span data-ttu-id="3bda6-136">Maak een bestand met de naam **ifcfg eth0** in de `/etc/sysconfig/network-scripts/` map waarin zich de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="3bda6-136">Create a file named **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` directory that contains the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. <span data-ttu-id="3bda6-137">Udev-regels om te voorkomen dat statische regels voor de Ethernet-interface (s) wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3bda6-137">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="3bda6-138">Deze regels kunnen problemen veroorzaken bij het klonen van een virtuele machine in Microsoft Azure- of Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="3bda6-138">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. <span data-ttu-id="3bda6-139">Zorg ervoor dat de netwerkservice tijdens het opstarten wordt gestart met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3bda6-139">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # chkconfig network on
8. <span data-ttu-id="3bda6-140">Python-pyasn1 installeren met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3bda6-140">Install python-pyasn1 by running the following command:</span></span>
   
        # sudo yum install python-pyasn1
9. <span data-ttu-id="3bda6-141">De regel voor het opstarten van kernel in uw configuratie wormgaten aanvullende kernel-parameters voor Azure opnemen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3bda6-141">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="3bda6-142">Deze open doen ' / boot/grub/menu.lst ' in een teksteditor en zorg ervoor dat de kernel standaard de volgende parameters bevat:</span><span class="sxs-lookup"><span data-stu-id="3bda6-142">To do this open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   <span data-ttu-id="3bda6-143">Hiermee zorgt u ervoor dat alle consoleberichten worden verzonden naar de eerste seriële poort, die Azure helpen kan ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="3bda6-143">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="3bda6-144">Hiermee wordt het NUMA uitgeschakeld vanwege een fout in Oracle van Red Hat compatibel kernel.</span><span class="sxs-lookup"><span data-stu-id="3bda6-144">This will disable NUMA due to a bug in Oracle's Red Hat compatible kernel.</span></span>
   
   <span data-ttu-id="3bda6-145">Naast de bovenstaande, wordt u aangeraden te *verwijderen* de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="3bda6-145">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
   <span data-ttu-id="3bda6-146">Grafische en stil opstarten zijn niet handig in een omgeving waar we de logboeken worden verzonden naar de seriële poort.</span><span class="sxs-lookup"><span data-stu-id="3bda6-146">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>
   
   <span data-ttu-id="3bda6-147">De `crashkernel` mogelijk links geconfigureerd indien gewenst, maar dat deze parameter wordt Verklein de hoeveelheid beschikbaar geheugen in de virtuele machine 128 MB of meer, die mogelijk problemen op de VM-kleinere opmerking.</span><span class="sxs-lookup"><span data-stu-id="3bda6-147">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>
10. <span data-ttu-id="3bda6-148">Zorg ervoor dat de SSH-server is geïnstalleerd en geconfigureerd om te starten tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="3bda6-148">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="3bda6-149">Dit is doorgaans de standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="3bda6-149">This is usually the default.</span></span>
11. <span data-ttu-id="3bda6-150">Installeer de Azure Linux Agent door de volgende opdracht uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="3bda6-150">Install the Azure Linux Agent by running the following command.</span></span> <span data-ttu-id="3bda6-151">De meest recente versie is 2.0.15.</span><span class="sxs-lookup"><span data-stu-id="3bda6-151">The latest version is 2.0.15.</span></span>
    
        # sudo yum install WALinuxAgent
    
    <span data-ttu-id="3bda6-152">Houd er rekening mee dat de installatie van het pakket WALinuxAgent de NetworkManager verwijdert en NetworkManager gnome pakketten als ze zijn niet al verwijderd zoals beschreven in stap 2.</span><span class="sxs-lookup"><span data-stu-id="3bda6-152">Note that installing the WALinuxAgent package will remove the NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 2.</span></span>
12. <span data-ttu-id="3bda6-153">Maak geen wisselruimte op de schijf met het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="3bda6-153">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="3bda6-154">De Azure Linux Agent kunt wisselruimte met behulp van de lokale resource die is gekoppeld aan de virtuele machine na het inrichten op Azure automatisch configureren.</span><span class="sxs-lookup"><span data-stu-id="3bda6-154">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="3bda6-155">Let op de lokale resource-schijf is een *tijdelijke* schijfruimte en kan worden leeggemaakt wanneer de virtuele machine is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3bda6-155">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="3bda6-156">Na de installatie van de Azure Linux Agent (Zie de vorige stap), de volgende parameters in /etc/waagent.conf op de juiste wijze te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="3bda6-156">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.
13. <span data-ttu-id="3bda6-157">Voer de volgende opdrachten inrichting ervan ongedaan maakt de virtuele machine en deze voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="3bda6-157">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. <span data-ttu-id="3bda6-158">Klik op **actie-Afsluiten > omlaag** in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="3bda6-158">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="3bda6-159">Uw Linux VHD is nu gereed om te worden geüpload naar Azure.</span><span class="sxs-lookup"><span data-stu-id="3bda6-159">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

- - -
## <a name="oracle-linux-70"></a><span data-ttu-id="3bda6-160">Oracle Linux 7.0 +</span><span class="sxs-lookup"><span data-stu-id="3bda6-160">Oracle Linux 7.0+</span></span>
<span data-ttu-id="3bda6-161">**Wijzigingen in Oracle Linux 7**</span><span class="sxs-lookup"><span data-stu-id="3bda6-161">**Changes in Oracle Linux 7**</span></span>

<span data-ttu-id="3bda6-162">Een virtuele machine van de Oracle Linux 7 voorbereiden voor Azure is vergelijkbaar met Oracle Linux 6, maar er zijn echter enkele belangrijke verschillen opgemerkt:</span><span class="sxs-lookup"><span data-stu-id="3bda6-162">Preparing an Oracle Linux 7 virtual machine for Azure is very similar to Oracle Linux 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="3bda6-163">Zowel de Red Hat compatibel kernel van Oracle UEK3 worden ondersteund in Azure.</span><span class="sxs-lookup"><span data-stu-id="3bda6-163">Both the Red Hat compatible kernel and Oracle's UEK3 are supported in Azure.</span></span>  <span data-ttu-id="3bda6-164">De kernel UEK3 wordt aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="3bda6-164">The UEK3 kernel is recommended.</span></span>
* <span data-ttu-id="3bda6-165">Het pakket NetworkManager wordt niet langer strijdig met de Azure Linux-agent.</span><span class="sxs-lookup"><span data-stu-id="3bda6-165">The NetworkManager package no longer conflicts with the Azure Linux agent.</span></span> <span data-ttu-id="3bda6-166">Dit pakket wordt standaard geïnstalleerd en wordt aangeraden deze niet is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3bda6-166">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="3bda6-167">GRUB2 wordt nu gebruikt als de standaard bootloader, zodat de procedure voor het bewerken van de kernel parameters is gewijzigd (Zie hieronder).</span><span class="sxs-lookup"><span data-stu-id="3bda6-167">GRUB2 is now used as the default bootloader, so the procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="3bda6-168">XFS is nu het standaardbestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="3bda6-168">XFS is now the default file system.</span></span> <span data-ttu-id="3bda6-169">Het bestandssysteem ext4 kan nog steeds worden gebruikt, indien gewenst.</span><span class="sxs-lookup"><span data-stu-id="3bda6-169">The ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="3bda6-170">**Configuratiestappen**</span><span class="sxs-lookup"><span data-stu-id="3bda6-170">**Configuration steps**</span></span>

1. <span data-ttu-id="3bda6-171">Selecteer de virtuele machine in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="3bda6-171">In Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="3bda6-172">Klik op **Connect** om een consolevenster voor de virtuele machine te openen.</span><span class="sxs-lookup"><span data-stu-id="3bda6-172">Click **Connect** to open a console window for the virtual machine.</span></span>
3. <span data-ttu-id="3bda6-173">Maak een bestand met de naam **netwerk** in de `/etc/sysconfig/` map waarin zich de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="3bda6-173">Create a file named **network** in the `/etc/sysconfig/` directory that contains the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. <span data-ttu-id="3bda6-174">Maak een bestand met de naam **ifcfg eth0** in de `/etc/sysconfig/network-scripts/` map waarin zich de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="3bda6-174">Create a file named **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` directory that contains the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. <span data-ttu-id="3bda6-175">Udev-regels om te voorkomen dat statische regels voor de Ethernet-interface (s) wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3bda6-175">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="3bda6-176">Deze regels kunnen problemen veroorzaken bij het klonen van een virtuele machine in Microsoft Azure- of Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="3bda6-176">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. <span data-ttu-id="3bda6-177">Zorg ervoor dat de netwerkservice tijdens het opstarten wordt gestart met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3bda6-177">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # sudo chkconfig network on
7. <span data-ttu-id="3bda6-178">Installeer het pakket python pyasn1 met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3bda6-178">Install the python-pyasn1 package by running the following command:</span></span>
   
        # sudo yum install python-pyasn1
8. <span data-ttu-id="3bda6-179">Voer de volgende opdracht om te wissen van de metagegevens van de huidige yum en geen updates installeren:</span><span class="sxs-lookup"><span data-stu-id="3bda6-179">Run the following command to clear the current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all
        # sudo yum -y update
9. <span data-ttu-id="3bda6-180">De regel voor het opstarten van kernel in uw configuratie wormgaten aanvullende kernel-parameters voor Azure opnemen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3bda6-180">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="3bda6-181">Om dit te doen open '/ standaard/etc/grub' in een teksteditor en bewerk de `GRUB_CMDLINE_LINUX` parameter, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3bda6-181">To do this open "/etc/default/grub" in a text editor and edit the `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="3bda6-182">Hiermee zorgt u ervoor dat alle consoleberichten worden verzonden naar de eerste seriële poort, die Azure helpen kan ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="3bda6-182">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="3bda6-183">Deze ook schakelt u de nieuwe indicatie 7 naamconventies voor NIC's.</span><span class="sxs-lookup"><span data-stu-id="3bda6-183">It also turns off the new OEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="3bda6-184">Naast de bovenstaande, wordt u aangeraden te *verwijderen* de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="3bda6-184">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
       rhgb quiet crashkernel=auto
   
   <span data-ttu-id="3bda6-185">Grafische en stil opstarten zijn niet handig in een omgeving waar we de logboeken worden verzonden naar de seriële poort.</span><span class="sxs-lookup"><span data-stu-id="3bda6-185">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>
   
   <span data-ttu-id="3bda6-186">De `crashkernel` mogelijk links geconfigureerd indien gewenst, maar dat deze parameter wordt Verklein de hoeveelheid beschikbaar geheugen in de virtuele machine 128 MB of meer, die mogelijk problemen op de VM-kleinere opmerking.</span><span class="sxs-lookup"><span data-stu-id="3bda6-186">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>
10. <span data-ttu-id="3bda6-187">Wanneer u klaar bent editing '/ standaard/etc/grub' per hierboven, voer de volgende opdracht voor het opnieuw samenstellen van de configuratie van de grub:</span><span class="sxs-lookup"><span data-stu-id="3bda6-187">Once you are done editing "/etc/default/grub" per above, run the following command to rebuild the grub configuration:</span></span>
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. <span data-ttu-id="3bda6-188">Zorg ervoor dat de SSH-server is geïnstalleerd en geconfigureerd om te starten tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="3bda6-188">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="3bda6-189">Dit is doorgaans de standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="3bda6-189">This is usually the default.</span></span>
12. <span data-ttu-id="3bda6-190">Installeer de Azure Linux Agent met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3bda6-190">Install the Azure Linux Agent by running the following command:</span></span>
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. <span data-ttu-id="3bda6-191">Maak geen wisselruimte op de schijf met het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="3bda6-191">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="3bda6-192">De Azure Linux Agent kunt wisselruimte met behulp van de lokale resource die is gekoppeld aan de virtuele machine na het inrichten op Azure automatisch configureren.</span><span class="sxs-lookup"><span data-stu-id="3bda6-192">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="3bda6-193">Let op de lokale resource-schijf is een *tijdelijke* schijfruimte en kan worden leeggemaakt wanneer de virtuele machine is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3bda6-193">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="3bda6-194">Na de installatie van de Azure Linux Agent (Zie de vorige stap), de volgende parameters in /etc/waagent.conf op de juiste wijze te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="3bda6-194">After installing the Azure Linux Agent (see the previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.
14. <span data-ttu-id="3bda6-195">Voer de volgende opdrachten inrichting ervan ongedaan maakt de virtuele machine en deze voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="3bda6-195">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. <span data-ttu-id="3bda6-196">Klik op **actie-Afsluiten > omlaag** in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="3bda6-196">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="3bda6-197">Uw Linux VHD is nu gereed om te worden geüpload naar Azure.</span><span class="sxs-lookup"><span data-stu-id="3bda6-197">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bda6-198">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3bda6-198">Next steps</span></span>
<span data-ttu-id="3bda6-199">U bent nu klaar voor gebruik van uw VHD Oracle Linux maken van nieuwe virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="3bda6-199">You're now ready to use your Oracle Linux .vhd to create new virtual machines in Azure.</span></span> <span data-ttu-id="3bda6-200">Als dit de eerste keer dat u de VHD-bestand naar Azure uploadt, Zie de stappen 2 en 3 in [maken en uploaden van een virtuele harde schijf met het Linux-besturingssysteem](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3bda6-200">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

