---
title: Maken en uploaden van een VHD SUSE Linux in Azure
description: Informatie over het maken en uploaden van een Azure virtuele harde schijf (VHD) waarop een SUSE Linux-besturingssysteem.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 066d01a6-2a54-4718-bcd0-90fe7a5303a1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: szark
ms.openlocfilehash: c829f5d9a90b4260c6f41b2d9e511a0c6cb48f18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a><span data-ttu-id="51f2c-103">Een op SLES of openSUSE gebaseerde virtuele machine voor Azure voorbereiden</span><span class="sxs-lookup"><span data-stu-id="51f2c-103">Prepare a SLES or openSUSE virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="51f2c-104">Vereisten</span><span class="sxs-lookup"><span data-stu-id="51f2c-104">Prerequisites</span></span>
<span data-ttu-id="51f2c-105">In dit artikel wordt ervan uitgegaan dat u al hebt geïnstalleerd een SUSE of openSUSE Linux-besturingssysteem naar een virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="51f2c-105">This article assumes that you have already installed a SUSE or openSUSE Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="51f2c-106">Er bestaan meerdere hulpprogramma's voor het maken van de VHD-bestanden, bijvoorbeeld een virtualisatieoplossing zoals Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="51f2c-106">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="51f2c-107">Zie voor instructies [de Hyper-V-rol installeren en configureren van een virtuele Machine](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="51f2c-107">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="sles--opensuse-installation-notes"></a><span data-ttu-id="51f2c-108">SLES / openSUSE opmerkingen bij de installatie</span><span class="sxs-lookup"><span data-stu-id="51f2c-108">SLES / openSUSE installation notes</span></span>
* <span data-ttu-id="51f2c-109">Zie ook [algemene opmerkingen bij de installatie van Linux](create-upload-generic.md#general-linux-installation-notes) voor meer tips over Linux voorbereiden voor Azure.</span><span class="sxs-lookup"><span data-stu-id="51f2c-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="51f2c-110">De VHDX-indeling wordt niet ondersteund in Azure, alleen **vaste VHD**.</span><span class="sxs-lookup"><span data-stu-id="51f2c-110">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="51f2c-111">U kunt de schijf converteren naar VHD-indeling met behulp van Hyper-V-beheer of de cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="51f2c-111">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="51f2c-112">Bij het installeren van de Linux-systeem wordt het aanbevolen dat u standaard partities in plaats van LVM (vaak de standaardinstelling voor vele installaties gebruikt).</span><span class="sxs-lookup"><span data-stu-id="51f2c-112">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="51f2c-113">Dit voorkomt LVM naam conflicteert met de gekloonde virtuele machines, met name als een besturingssysteemschijf ooit worden gekoppeld aan een andere virtuele machine moet voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="51f2c-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="51f2c-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mag worden gebruikt voor gegevensschijven als voorkeur.</span><span class="sxs-lookup"><span data-stu-id="51f2c-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="51f2c-115">Configureer een partitie van de wisseling niet op de schijf met het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="51f2c-115">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="51f2c-116">De Linux-agent kan worden geconfigureerd voor het maken van een wisselbestand op de tijdelijke schijf.</span><span class="sxs-lookup"><span data-stu-id="51f2c-116">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="51f2c-117">Meer informatie hierover vindt u in de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="51f2c-117">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="51f2c-118">Alle van de VHD's moeten grootten die veelvouden van 1 MB hebben.</span><span class="sxs-lookup"><span data-stu-id="51f2c-118">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-suse-studio"></a><span data-ttu-id="51f2c-119">SUSE Studio gebruiken</span><span class="sxs-lookup"><span data-stu-id="51f2c-119">Use SUSE Studio</span></span>
<span data-ttu-id="51f2c-120">[SUSE Studio](http://www.susestudio.com) eenvoudig kunt maken en beheren van uw afbeeldingen SLES en openSUSE voor Azure en Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="51f2c-120">[SUSE Studio](http://www.susestudio.com) can easily create and manage your SLES and openSUSE images for Azure and Hyper-V.</span></span> <span data-ttu-id="51f2c-121">Dit is de aanbevolen aanpak voor het aanpassen van uw eigen installatiekopieën SLES en openSUSE.</span><span class="sxs-lookup"><span data-stu-id="51f2c-121">This is the recommended approach for customizing your own SLES and openSUSE images.</span></span>

<span data-ttu-id="51f2c-122">Als alternatief voor het bouwen van uw eigen VHD SUSE publiceert ook BYOS (uw eigen abonnement Bring) installatiekopieën voor SLES op [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span><span class="sxs-lookup"><span data-stu-id="51f2c-122">As an alternative to building your own VHD, SUSE also publishes BYOS (Bring Your Own Subscription) images for SLES at [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span></span>

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a><span data-ttu-id="51f2c-123">SUSE Linux Enterprise Server 11 SP4 voorbereiden</span><span class="sxs-lookup"><span data-stu-id="51f2c-123">Prepare SUSE Linux Enterprise Server 11 SP4</span></span>
1. <span data-ttu-id="51f2c-124">Selecteer in het middelste deelvenster van de Hyper-V-beheer, de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="51f2c-124">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="51f2c-125">Klik op **Connect** om het venster voor de virtuele machine te openen.</span><span class="sxs-lookup"><span data-stu-id="51f2c-125">Click **Connect** to open the window for the virtual machine.</span></span>
3. <span data-ttu-id="51f2c-126">Registreren van uw systeem SUSE Linux Enterprise zodat deze kan updates downloaden en installeren van pakketten.</span><span class="sxs-lookup"><span data-stu-id="51f2c-126">Register your SUSE Linux Enterprise system to allow it to download updates and install packages.</span></span>
4. <span data-ttu-id="51f2c-127">Het bijwerken van het systeem met de meest recente patches:</span><span class="sxs-lookup"><span data-stu-id="51f2c-127">Update the system with the latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="51f2c-128">Installeer de Azure Linux Agent uit de opslagplaats voor SLES:</span><span class="sxs-lookup"><span data-stu-id="51f2c-128">Install the Azure Linux Agent from the SLES repository:</span></span>
   
        # sudo zypper install WALinuxAgent
6. <span data-ttu-id="51f2c-129">Controleer als waagent is ingesteld op 'aan' in chkconfig en als dat niet inschakelen voor automatisch starten:</span><span class="sxs-lookup"><span data-stu-id="51f2c-129">Check if waagent is set to "on" in chkconfig, and if not, enable it for autostart:</span></span>
   
        # sudo chkconfig waagent on
7. <span data-ttu-id="51f2c-130">Controleer of waagent-service wordt uitgevoerd en als dat niet starten:</span><span class="sxs-lookup"><span data-stu-id="51f2c-130">Check if waagent service is running, and if not, start it:</span></span> 
   
        # sudo service waagent start
8. <span data-ttu-id="51f2c-131">De regel voor het opstarten van kernel in uw configuratie wormgaten aanvullende kernel-parameters voor Azure opnemen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="51f2c-131">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="51f2c-132">Deze open doen ' / boot/grub/menu.lst ' in een teksteditor en zorg ervoor dat de kernel standaard de volgende parameters bevat:</span><span class="sxs-lookup"><span data-stu-id="51f2c-132">To do this open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    <span data-ttu-id="51f2c-133">Hierdoor worden alle consoleberichten worden verzonden naar de eerste seriële poort, die Azure helpen kan ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="51f2c-133">This will ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
9. <span data-ttu-id="51f2c-134">Bevestig dat /boot/grub/menu.lst en /etc/fstab beide verwijzen naar de schijf met de UUID (door uuid) in plaats van de schijf-ID (door-id).</span><span class="sxs-lookup"><span data-stu-id="51f2c-134">Confirm that /boot/grub/menu.lst and /etc/fstab both reference the disk using its UUID (by-uuid) instead of the disk ID (by-id).</span></span> 
   
    <span data-ttu-id="51f2c-135">Schijf UUID ophalen</span><span class="sxs-lookup"><span data-stu-id="51f2c-135">Get disk UUID</span></span>
   
        # ls /dev/disk/by-uuid/
   
    <span data-ttu-id="51f2c-136">Als /dev/disk/by-id-is gebruikt, zowel /boot/grub/menu.lst als/etc/fstab bijwerken met de juiste door uuid-waarde</span><span class="sxs-lookup"><span data-stu-id="51f2c-136">If /dev/disk/by-id/ is used, update both /boot/grub/menu.lst and /etc/fstab with the proper by-uuid value</span></span>
   
    <span data-ttu-id="51f2c-137">Voordat de wijziging</span><span class="sxs-lookup"><span data-stu-id="51f2c-137">Before change</span></span>
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    <span data-ttu-id="51f2c-138">Na wijziging</span><span class="sxs-lookup"><span data-stu-id="51f2c-138">After change</span></span>
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. <span data-ttu-id="51f2c-139">Udev-regels om te voorkomen dat statische regels voor de Ethernet-interface (s) wijzigen.</span><span class="sxs-lookup"><span data-stu-id="51f2c-139">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="51f2c-140">Deze regels kunnen problemen veroorzaken bij het klonen van een virtuele machine in Microsoft Azure- of Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="51f2c-140">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. <span data-ttu-id="51f2c-141">Het wordt aanbevolen het bestand bewerken '/ etc/sysconfig/netwerk/dhcp' en wijzig de `DHCLIENT_SET_HOSTNAME` -parameter voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="51f2c-141">It is recommended to edit the file "/etc/sysconfig/network/dhcp" and change the `DHCLIENT_SET_HOSTNAME` parameter to the following:</span></span>
    
     <span data-ttu-id="51f2c-142">DHCLIENT_SET_HOSTNAME = "Nee"</span><span class="sxs-lookup"><span data-stu-id="51f2c-142">DHCLIENT_SET_HOSTNAME="no"</span></span>
12. <span data-ttu-id="51f2c-143">Uitcommentariëren '/ etc/sudoers', of verwijder de volgende regels, indien aanwezig:</span><span class="sxs-lookup"><span data-stu-id="51f2c-143">In "/etc/sudoers", comment out or remove the following lines if they exist:</span></span>
    
     <span data-ttu-id="51f2c-144">Standaard targetpw # vragen het wachtwoord van de doelgebruiker dat wil zeggen hoofdmap alle ALL=(ALL) alle # waarschuwing!</span><span class="sxs-lookup"><span data-stu-id="51f2c-144">Defaults targetpw   # ask for the password of the target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="51f2c-145">Gebruik alleen deze samen met 'Standaardwaarden targetpw'!</span><span class="sxs-lookup"><span data-stu-id="51f2c-145">Only use this together with 'Defaults targetpw'!</span></span>
13. <span data-ttu-id="51f2c-146">Zorg ervoor dat de SSH-server is geïnstalleerd en geconfigureerd om te starten tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="51f2c-146">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="51f2c-147">Dit is doorgaans de standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="51f2c-147">This is usually the default.</span></span>
14. <span data-ttu-id="51f2c-148">Maak geen wisselruimte op de schijf met het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="51f2c-148">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="51f2c-149">De Azure Linux Agent kunt wisselruimte met behulp van de lokale resource die is gekoppeld aan de virtuele machine na het inrichten op Azure automatisch configureren.</span><span class="sxs-lookup"><span data-stu-id="51f2c-149">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="51f2c-150">Let op de lokale resource-schijf is een *tijdelijke* schijfruimte en kan worden leeggemaakt wanneer de virtuele machine is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="51f2c-150">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="51f2c-151">Na de installatie van de Azure Linux Agent (Zie de vorige stap), de volgende parameters in /etc/waagent.conf op de juiste wijze te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="51f2c-151">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="51f2c-152">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Opmerking: Stel dit in op wat u ook nodig om te worden.</span><span class="sxs-lookup"><span data-stu-id="51f2c-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.</span></span>
15. <span data-ttu-id="51f2c-153">Voer de volgende opdrachten inrichting ervan ongedaan maakt de virtuele machine en deze voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="51f2c-153">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="51f2c-154">sudo waagent-force - deprovision</span><span class="sxs-lookup"><span data-stu-id="51f2c-154">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="51f2c-155">exporteren van HISTSIZE = 0</span><span class="sxs-lookup"><span data-stu-id="51f2c-155">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="51f2c-156">afmelden</span><span class="sxs-lookup"><span data-stu-id="51f2c-156">logout</span></span>
16. <span data-ttu-id="51f2c-157">Klik op **actie-Afsluiten > omlaag** in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="51f2c-157">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="51f2c-158">Uw Linux VHD is nu gereed om te worden geüpload naar Azure.</span><span class="sxs-lookup"><span data-stu-id="51f2c-158">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

- - -
## <a name="prepare-opensuse-131"></a><span data-ttu-id="51f2c-159">OpenSUSE 13,1 + voorbereiden</span><span class="sxs-lookup"><span data-stu-id="51f2c-159">Prepare openSUSE 13.1+</span></span>
1. <span data-ttu-id="51f2c-160">Selecteer in het middelste deelvenster van de Hyper-V-beheer, de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="51f2c-160">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="51f2c-161">Klik op **Connect** om het venster voor de virtuele machine te openen.</span><span class="sxs-lookup"><span data-stu-id="51f2c-161">Click **Connect** to open the window for the virtual machine.</span></span>
3. <span data-ttu-id="51f2c-162">Voer de opdracht op de shell '`zypper lr`'.</span><span class="sxs-lookup"><span data-stu-id="51f2c-162">On the shell, run the command '`zypper lr`'.</span></span> <span data-ttu-id="51f2c-163">Als u deze opdracht uitvoer lijkt op de volgende retourneert, wordt de opslagplaatsen zijn geconfigureerd zoals verwacht--zonder aanpassingen nodig zijn (Houd er rekening mee dat versienummers kan verschillen):</span><span class="sxs-lookup"><span data-stu-id="51f2c-163">If this command returns output similar to the following, then the repositories are configured as expected--no adjustments are necessary (note that version numbers may vary):</span></span>
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    <span data-ttu-id="51f2c-164">Als de opdracht 'Geen opslagplaatsen gedefinieerd...' retourneert gebruikt u de volgende opdrachten om toe te voegen deze repo's:</span><span class="sxs-lookup"><span data-stu-id="51f2c-164">If the command returns "No repositories defined..." then use the following commands to add these repos:</span></span>
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    <span data-ttu-id="51f2c-165">U kunt vervolgens controleren of de opslagplaatsen zijn toegevoegd met de opdracht '`zypper lr`' opnieuw.</span><span class="sxs-lookup"><span data-stu-id="51f2c-165">You can then verify the repositories have been added by running the command '`zypper lr`' again.</span></span> <span data-ttu-id="51f2c-166">Als een van de relevante update-opslagplaatsen niet is ingeschakeld, wordt dit inschakelen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="51f2c-166">In case one of the relevant update repositories is not enabled, enable it with following command:</span></span>
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. <span data-ttu-id="51f2c-167">De kernel bijwerken naar de meest recente versie:</span><span class="sxs-lookup"><span data-stu-id="51f2c-167">Update the kernel to the latest available version:</span></span>
   
        # sudo zypper up kernel-default
   
    <span data-ttu-id="51f2c-168">Of het systeem bijwerken met de meest recente patches:</span><span class="sxs-lookup"><span data-stu-id="51f2c-168">Or to update the system with all the latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="51f2c-169">Installeer de Azure Linux Agent.</span><span class="sxs-lookup"><span data-stu-id="51f2c-169">Install the Azure Linux Agent.</span></span>
   
   # <a name="sudo-zypper-install-walinuxagent"></a><span data-ttu-id="51f2c-170">sudo zypper installeren WALinuxAgent</span><span class="sxs-lookup"><span data-stu-id="51f2c-170">sudo zypper install WALinuxAgent</span></span>
6. <span data-ttu-id="51f2c-171">De regel voor het opstarten van kernel in uw configuratie wormgaten aanvullende kernel-parameters voor Azure opnemen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="51f2c-171">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="51f2c-172">Open hiervoor ' / boot/grub/menu.lst ' in een teksteditor en zorg ervoor dat de kernel standaard de volgende parameters bevat:</span><span class="sxs-lookup"><span data-stu-id="51f2c-172">To do this, open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span></span>
   
     <span data-ttu-id="51f2c-173">console = ttyS0 earlyprintk ttyS0 rootdelay = 300 =</span><span class="sxs-lookup"><span data-stu-id="51f2c-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span></span>
   
   <span data-ttu-id="51f2c-174">Hierdoor worden alle consoleberichten worden verzonden naar de eerste seriële poort, die Azure helpen kan ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="51f2c-174">This will ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="51f2c-175">Bovendien de volgende parameters uit de kernel boot-regel verwijderen als deze bestaan:</span><span class="sxs-lookup"><span data-stu-id="51f2c-175">In addition, remove the following parameters from the kernel boot line if they exist:</span></span>
   
     <span data-ttu-id="51f2c-176">libata.atapi_enabled=0 reserve = 0x1f0, 0x8</span><span class="sxs-lookup"><span data-stu-id="51f2c-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span></span>
7. <span data-ttu-id="51f2c-177">Het wordt aanbevolen het bestand bewerken '/ etc/sysconfig/netwerk/dhcp' en wijzig de `DHCLIENT_SET_HOSTNAME` -parameter voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="51f2c-177">It is recommended to edit the file "/etc/sysconfig/network/dhcp" and change the `DHCLIENT_SET_HOSTNAME` parameter to the following:</span></span>
   
     <span data-ttu-id="51f2c-178">DHCLIENT_SET_HOSTNAME = "Nee"</span><span class="sxs-lookup"><span data-stu-id="51f2c-178">DHCLIENT_SET_HOSTNAME="no"</span></span>
8. <span data-ttu-id="51f2c-179">**Belangrijk:** uitcommentariëren In '/ etc/sudoers', of verwijder de volgende regels, indien aanwezig:</span><span class="sxs-lookup"><span data-stu-id="51f2c-179">**Important:** In "/etc/sudoers", comment out or remove the following lines if they exist:</span></span>
   
     <span data-ttu-id="51f2c-180">Standaard targetpw # vragen het wachtwoord van de doelgebruiker dat wil zeggen hoofdmap alle ALL=(ALL) alle # waarschuwing!</span><span class="sxs-lookup"><span data-stu-id="51f2c-180">Defaults targetpw   # ask for the password of the target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="51f2c-181">Gebruik alleen deze samen met 'Standaardwaarden targetpw'!</span><span class="sxs-lookup"><span data-stu-id="51f2c-181">Only use this together with 'Defaults targetpw'!</span></span>
9. <span data-ttu-id="51f2c-182">Zorg ervoor dat de SSH-server is geïnstalleerd en geconfigureerd om te starten tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="51f2c-182">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="51f2c-183">Dit is doorgaans de standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="51f2c-183">This is usually the default.</span></span>
10. <span data-ttu-id="51f2c-184">Maak geen wisselruimte op de schijf met het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="51f2c-184">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="51f2c-185">De Azure Linux Agent kunt wisselruimte met behulp van de lokale resource die is gekoppeld aan de virtuele machine na het inrichten op Azure automatisch configureren.</span><span class="sxs-lookup"><span data-stu-id="51f2c-185">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="51f2c-186">Let op de lokale resource-schijf is een *tijdelijke* schijfruimte en kan worden leeggemaakt wanneer de virtuele machine is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="51f2c-186">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="51f2c-187">Na de installatie van de Azure Linux Agent (Zie de vorige stap), de volgende parameters in /etc/waagent.conf op de juiste wijze te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="51f2c-187">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="51f2c-188">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Opmerking: Stel dit in op wat u ook nodig om te worden.</span><span class="sxs-lookup"><span data-stu-id="51f2c-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.</span></span>
11. <span data-ttu-id="51f2c-189">Voer de volgende opdrachten inrichting ervan ongedaan maakt de virtuele machine en deze voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="51f2c-189">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="51f2c-190">sudo waagent-force - deprovision</span><span class="sxs-lookup"><span data-stu-id="51f2c-190">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="51f2c-191">exporteren van HISTSIZE = 0</span><span class="sxs-lookup"><span data-stu-id="51f2c-191">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="51f2c-192">afmelden</span><span class="sxs-lookup"><span data-stu-id="51f2c-192">logout</span></span>
12. <span data-ttu-id="51f2c-193">Zorg ervoor dat de Azure Linux Agent wordt uitgevoerd bij het opstarten:</span><span class="sxs-lookup"><span data-stu-id="51f2c-193">Ensure the Azure Linux Agent runs at startup:</span></span>
    
        # sudo systemctl enable waagent.service
13. <span data-ttu-id="51f2c-194">Klik op **actie-Afsluiten > omlaag** in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="51f2c-194">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="51f2c-195">Uw Linux VHD is nu gereed om te worden geüpload naar Azure.</span><span class="sxs-lookup"><span data-stu-id="51f2c-195">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51f2c-196">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="51f2c-196">Next steps</span></span>
<span data-ttu-id="51f2c-197">U bent nu klaar voor gebruik van de virtuele harde schijf van SUSE Linux maken van nieuwe virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="51f2c-197">You're now ready to use your SUSE Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="51f2c-198">Als dit de eerste keer dat u de VHD-bestand naar Azure uploadt, Zie de stappen 2 en 3 in [maken en uploaden van een virtuele harde schijf met het Linux-besturingssysteem](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51f2c-198">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

