---
title: aaaCreate een VHD en uploaden SUSE Linux in Azure
description: Informatie over toocreate en uploaden van een Azure virtuele harde schijf (VHD) waarop een SUSE Linux-besturingssysteem.
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
ms.openlocfilehash: 9185c7e67279357f00db0f43e944e96c58f0dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a><span data-ttu-id="beb06-103">Een op SLES of openSUSE gebaseerde virtuele machine voor Azure voorbereiden</span><span class="sxs-lookup"><span data-stu-id="beb06-103">Prepare a SLES or openSUSE virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="beb06-104">Vereisten</span><span class="sxs-lookup"><span data-stu-id="beb06-104">Prerequisites</span></span>
<span data-ttu-id="beb06-105">In dit artikel wordt ervan uitgegaan dat u al hebt geïnstalleerd een SUSE of openSUSE Linux-besturingssysteem tooa virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="beb06-105">This article assumes that you have already installed a SUSE or openSUSE Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="beb06-106">Meerdere hulpprogramma's bestaan toocreate VHD-bestanden, bijvoorbeeld een virtualisatieoplossing zoals Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="beb06-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="beb06-107">Zie voor instructies [Hallo Hyper-V-rol installeren en configureren van een virtuele Machine](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="beb06-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="sles--opensuse-installation-notes"></a><span data-ttu-id="beb06-108">SLES / openSUSE opmerkingen bij de installatie</span><span class="sxs-lookup"><span data-stu-id="beb06-108">SLES / openSUSE installation notes</span></span>
* <span data-ttu-id="beb06-109">Zie ook [algemene opmerkingen bij de installatie van Linux](create-upload-generic.md#general-linux-installation-notes) voor meer tips over Linux voorbereiden voor Azure.</span><span class="sxs-lookup"><span data-stu-id="beb06-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="beb06-110">Hallo VHDX-indeling wordt niet ondersteund in Azure, alleen **vaste VHD**.</span><span class="sxs-lookup"><span data-stu-id="beb06-110">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="beb06-111">U kunt converteren Hallo tooVHD schijfindeling met behulp van Hyper-V-beheer of Hallo cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="beb06-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="beb06-112">Bij het installeren van Hallo Linux-systeem wordt het aanbevolen dat u standaard partities in plaats van LVM (vaak Hallo standaard voor vele installaties gebruikt).</span><span class="sxs-lookup"><span data-stu-id="beb06-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="beb06-113">Dit voorkomt LVM naam conflicteert met de gekloonde virtuele machines, met name een besturingssysteemschijf ooit moet toobe gekoppeld tooanother VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="beb06-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="beb06-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mag worden gebruikt voor gegevensschijven als voorkeur.</span><span class="sxs-lookup"><span data-stu-id="beb06-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="beb06-115">Configureer een partitie van de wisseling niet op Hallo OS-schijf.</span><span class="sxs-lookup"><span data-stu-id="beb06-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="beb06-116">Hallo Linux-agent kan worden geconfigureerd toocreate een wisselbestand op Hallo tijdelijke schijf.</span><span class="sxs-lookup"><span data-stu-id="beb06-116">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="beb06-117">Meer informatie hierover vindt u in onderstaande Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="beb06-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="beb06-118">Alle VHD's Hallo moeten grootten die veelvouden van 1 MB hebben.</span><span class="sxs-lookup"><span data-stu-id="beb06-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-suse-studio"></a><span data-ttu-id="beb06-119">SUSE Studio gebruiken</span><span class="sxs-lookup"><span data-stu-id="beb06-119">Use SUSE Studio</span></span>
<span data-ttu-id="beb06-120">[SUSE Studio](http://www.susestudio.com) eenvoudig kunt maken en beheren van uw afbeeldingen SLES en openSUSE voor Azure en Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="beb06-120">[SUSE Studio](http://www.susestudio.com) can easily create and manage your SLES and openSUSE images for Azure and Hyper-V.</span></span> <span data-ttu-id="beb06-121">Dit is de aanbevolen aanpak voor het aanpassen van uw eigen installatiekopieën SLES en openSUSE Hallo.</span><span class="sxs-lookup"><span data-stu-id="beb06-121">This is hello recommended approach for customizing your own SLES and openSUSE images.</span></span>

<span data-ttu-id="beb06-122">Als een alternatieve toobuilding uw eigen VHD, SUSE publiceert ook BYOS (uw eigen abonnement Bring) installatiekopieën voor SLES op [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span><span class="sxs-lookup"><span data-stu-id="beb06-122">As an alternative toobuilding your own VHD, SUSE also publishes BYOS (Bring Your Own Subscription) images for SLES at [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span></span>

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a><span data-ttu-id="beb06-123">SUSE Linux Enterprise Server 11 SP4 voorbereiden</span><span class="sxs-lookup"><span data-stu-id="beb06-123">Prepare SUSE Linux Enterprise Server 11 SP4</span></span>
1. <span data-ttu-id="beb06-124">Selecteer Hallo virtuele machine in Hallo middelste deelvenster van de Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="beb06-124">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="beb06-125">Klik op **Connect** tooopen Hallo venster voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="beb06-125">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="beb06-126">Registreren van uw systeem SUSE Linux Enterprise tooallow het toodownload updates en pakketten worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="beb06-126">Register your SUSE Linux Enterprise system tooallow it toodownload updates and install packages.</span></span>
4. <span data-ttu-id="beb06-127">Hallo systeem bijwerken met de meest recente patches Hallo:</span><span class="sxs-lookup"><span data-stu-id="beb06-127">Update hello system with hello latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="beb06-128">Hello Azure Linux Agent uit Hallo SLES opslagplaats installeren:</span><span class="sxs-lookup"><span data-stu-id="beb06-128">Install hello Azure Linux Agent from hello SLES repository:</span></span>
   
        # sudo zypper install WALinuxAgent
6. <span data-ttu-id="beb06-129">Controleer als waagent te 'op' is ingesteld in chkconfig en als dat niet inschakelen voor automatisch starten:</span><span class="sxs-lookup"><span data-stu-id="beb06-129">Check if waagent is set too"on" in chkconfig, and if not, enable it for autostart:</span></span>
   
        # sudo chkconfig waagent on
7. <span data-ttu-id="beb06-130">Controleer of waagent-service wordt uitgevoerd en als dat niet starten:</span><span class="sxs-lookup"><span data-stu-id="beb06-130">Check if waagent service is running, and if not, start it:</span></span> 
   
        # sudo service waagent start
8. <span data-ttu-id="beb06-131">Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen.</span><span class="sxs-lookup"><span data-stu-id="beb06-131">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="beb06-132">dit open toodo ' / boot/grub/menu.lst ' in een teksteditor en zorg ervoor dat standaard Hallo kernel bevat Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="beb06-132">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    <span data-ttu-id="beb06-133">Hierdoor worden alle console berichten worden toohello eerste seriële poort, die Azure helpen kan ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="beb06-133">This will ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
9. <span data-ttu-id="beb06-134">Bevestig dat fstab /boot/grub/menu.lst en/etc/beide verwijzing Hallo-schijf met de UUID (door uuid) in plaats van Hallo schijf-ID (door-id).</span><span class="sxs-lookup"><span data-stu-id="beb06-134">Confirm that /boot/grub/menu.lst and /etc/fstab both reference hello disk using its UUID (by-uuid) instead of hello disk ID (by-id).</span></span> 
   
    <span data-ttu-id="beb06-135">Schijf UUID ophalen</span><span class="sxs-lookup"><span data-stu-id="beb06-135">Get disk UUID</span></span>
   
        # ls /dev/disk/by-uuid/
   
    <span data-ttu-id="beb06-136">Als /dev/disk/by-id-/boot/grub/menu.lst zowel/etc/fstab gebruikt, worden bijgewerkt met Hallo juiste door uuid waarde</span><span class="sxs-lookup"><span data-stu-id="beb06-136">If /dev/disk/by-id/ is used, update both /boot/grub/menu.lst and /etc/fstab with hello proper by-uuid value</span></span>
   
    <span data-ttu-id="beb06-137">Voordat de wijziging</span><span class="sxs-lookup"><span data-stu-id="beb06-137">Before change</span></span>
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    <span data-ttu-id="beb06-138">Na wijziging</span><span class="sxs-lookup"><span data-stu-id="beb06-138">After change</span></span>
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. <span data-ttu-id="beb06-139">Wijzig de udev regels tooavoid statische regels voor Hallo Ethernet-interface (s) te genereren.</span><span class="sxs-lookup"><span data-stu-id="beb06-139">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="beb06-140">Deze regels kunnen problemen veroorzaken bij het klonen van een virtuele machine in Microsoft Azure- of Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="beb06-140">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. <span data-ttu-id="beb06-141">Het verdient aanbeveling tooedit Hallo bestand '/ etc/sysconfig/netwerk/dhcp' en wijzigt u Hallo `DHCLIENT_SET_HOSTNAME` parameter toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="beb06-141">It is recommended tooedit hello file "/etc/sysconfig/network/dhcp" and change hello `DHCLIENT_SET_HOSTNAME` parameter toohello following:</span></span>
    
     <span data-ttu-id="beb06-142">DHCLIENT_SET_HOSTNAME = "Nee"</span><span class="sxs-lookup"><span data-stu-id="beb06-142">DHCLIENT_SET_HOSTNAME="no"</span></span>
12. <span data-ttu-id="beb06-143">In '/ etc/sudoers', uitschakelen of verwijderen Hallo volgende regels, indien aanwezig:</span><span class="sxs-lookup"><span data-stu-id="beb06-143">In "/etc/sudoers", comment out or remove hello following lines if they exist:</span></span>
    
     <span data-ttu-id="beb06-144">Standaard targetpw # om Hallo-wachtwoord van de doelgebruiker Hallo dat wil zeggen hoofdmap alle ALL=(ALL) alle vragen # waarschuwing!</span><span class="sxs-lookup"><span data-stu-id="beb06-144">Defaults targetpw   # ask for hello password of hello target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="beb06-145">Gebruik alleen deze samen met 'Standaardwaarden targetpw'!</span><span class="sxs-lookup"><span data-stu-id="beb06-145">Only use this together with 'Defaults targetpw'!</span></span>
13. <span data-ttu-id="beb06-146">Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="beb06-146">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="beb06-147">Dit is meestal Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="beb06-147">This is usually hello default.</span></span>
14. <span data-ttu-id="beb06-148">Maak geen wisselruimte op Hallo OS-schijf.</span><span class="sxs-lookup"><span data-stu-id="beb06-148">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="beb06-149">Hello Azure Linux Agent kunt wisselruimte Hallo lokale resource schijf die is aangesloten toohello VM na het inrichten op Azure automatisch configureren.</span><span class="sxs-lookup"><span data-stu-id="beb06-149">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="beb06-150">Houd er rekening mee dat lokale resource Hallo schijf is een *tijdelijke* schijfruimte en kan worden leeggemaakt wanneer Hallo VM gemaakt is.</span><span class="sxs-lookup"><span data-stu-id="beb06-150">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="beb06-151">Na de installatie van hello Azure Linux Agent (Zie de vorige stap), wijzigen Hallo-parameters in /etc/waagent.conf op de juiste wijze te volgen:</span><span class="sxs-lookup"><span data-stu-id="beb06-151">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="beb06-152">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Opmerking: deze moet u toobe toowhatever ingesteld.</span><span class="sxs-lookup"><span data-stu-id="beb06-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.</span></span>
15. <span data-ttu-id="beb06-153">Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="beb06-153">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="beb06-154">sudo waagent-force - deprovision</span><span class="sxs-lookup"><span data-stu-id="beb06-154">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="beb06-155">exporteren van HISTSIZE = 0</span><span class="sxs-lookup"><span data-stu-id="beb06-155">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="beb06-156">afmelden</span><span class="sxs-lookup"><span data-stu-id="beb06-156">logout</span></span>
16. <span data-ttu-id="beb06-157">Klik op **actie-Afsluiten > omlaag** in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="beb06-157">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="beb06-158">Uw Linux VHD is nu gereed toobe tooAzure geüpload.</span><span class="sxs-lookup"><span data-stu-id="beb06-158">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="prepare-opensuse-131"></a><span data-ttu-id="beb06-159">OpenSUSE 13,1 + voorbereiden</span><span class="sxs-lookup"><span data-stu-id="beb06-159">Prepare openSUSE 13.1+</span></span>
1. <span data-ttu-id="beb06-160">Selecteer Hallo virtuele machine in Hallo middelste deelvenster van de Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="beb06-160">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="beb06-161">Klik op **Connect** tooopen Hallo venster voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="beb06-161">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="beb06-162">Voer op Hallo-shell Hallo-opdracht '`zypper lr`'.</span><span class="sxs-lookup"><span data-stu-id="beb06-162">On hello shell, run hello command '`zypper lr`'.</span></span> <span data-ttu-id="beb06-163">Als u deze opdracht retourneert de uitvoer vergelijkbare toohello te volgen, en vervolgens het Hallo-opslagplaatsen zijn geconfigureerd zoals verwacht--zonder aanpassingen nodig zijn (opmerking die versienummers kunnen verschillen):</span><span class="sxs-lookup"><span data-stu-id="beb06-163">If this command returns output similar toohello following, then hello repositories are configured as expected--no adjustments are necessary (note that version numbers may vary):</span></span>
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    <span data-ttu-id="beb06-164">Als Hallo opdracht retourneert 'Geen opslagplaatsen gedefinieerd...' gebruikt Hallo opdrachten tooadd na deze repo's:</span><span class="sxs-lookup"><span data-stu-id="beb06-164">If hello command returns "No repositories defined..." then use hello following commands tooadd these repos:</span></span>
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    <span data-ttu-id="beb06-165">U kunt vervolgens controleren of het Hallo-opslagplaatsen zijn toegevoegd met de opdracht Hallo '`zypper lr`' opnieuw.</span><span class="sxs-lookup"><span data-stu-id="beb06-165">You can then verify hello repositories have been added by running hello command '`zypper lr`' again.</span></span> <span data-ttu-id="beb06-166">Als een van de relevante update-opslagplaatsen Hallo niet is ingeschakeld, wordt dit inschakelen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="beb06-166">In case one of hello relevant update repositories is not enabled, enable it with following command:</span></span>
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. <span data-ttu-id="beb06-167">Hallo kernel toohello meest recente versie bijwerken:</span><span class="sxs-lookup"><span data-stu-id="beb06-167">Update hello kernel toohello latest available version:</span></span>
   
        # sudo zypper up kernel-default
   
    <span data-ttu-id="beb06-168">Of tooupdate Hallo systeem met alle Hallo meest recente patches:</span><span class="sxs-lookup"><span data-stu-id="beb06-168">Or tooupdate hello system with all hello latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="beb06-169">Hello Azure Linux Agent installeren.</span><span class="sxs-lookup"><span data-stu-id="beb06-169">Install hello Azure Linux Agent.</span></span>
   
   # <a name="sudo-zypper-install-walinuxagent"></a><span data-ttu-id="beb06-170">sudo zypper installeren WALinuxAgent</span><span class="sxs-lookup"><span data-stu-id="beb06-170">sudo zypper install WALinuxAgent</span></span>
6. <span data-ttu-id="beb06-171">Hallo kernel opstarten regel in de grub tooinclude extra kernel-configuratieparameters voor Azure wijzigen.</span><span class="sxs-lookup"><span data-stu-id="beb06-171">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="beb06-172">toodo deze, open ' / boot/grub/menu.lst ' in een teksteditor en zorg ervoor dat standaard Hallo kernel bevat Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="beb06-172">toodo this, open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
     <span data-ttu-id="beb06-173">console = ttyS0 earlyprintk ttyS0 rootdelay = 300 =</span><span class="sxs-lookup"><span data-stu-id="beb06-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span></span>
   
   <span data-ttu-id="beb06-174">Hierdoor worden alle console berichten worden toohello eerste seriële poort, die Azure helpen kan ondersteuning bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="beb06-174">This will ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="beb06-175">Bovendien verwijderen Hallo volgende parameters uit Hallo kernel opstarten regel als deze bestaan:</span><span class="sxs-lookup"><span data-stu-id="beb06-175">In addition, remove hello following parameters from hello kernel boot line if they exist:</span></span>
   
     <span data-ttu-id="beb06-176">libata.atapi_enabled=0 reserve = 0x1f0, 0x8</span><span class="sxs-lookup"><span data-stu-id="beb06-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span></span>
7. <span data-ttu-id="beb06-177">Het verdient aanbeveling tooedit Hallo bestand '/ etc/sysconfig/netwerk/dhcp' en wijzigt u Hallo `DHCLIENT_SET_HOSTNAME` parameter toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="beb06-177">It is recommended tooedit hello file "/etc/sysconfig/network/dhcp" and change hello `DHCLIENT_SET_HOSTNAME` parameter toohello following:</span></span>
   
     <span data-ttu-id="beb06-178">DHCLIENT_SET_HOSTNAME = "Nee"</span><span class="sxs-lookup"><span data-stu-id="beb06-178">DHCLIENT_SET_HOSTNAME="no"</span></span>
8. <span data-ttu-id="beb06-179">**Belangrijk:** In '/ etc/sudoers', uitschakelen of verwijderen Hallo volgende regels, indien aanwezig:</span><span class="sxs-lookup"><span data-stu-id="beb06-179">**Important:** In "/etc/sudoers", comment out or remove hello following lines if they exist:</span></span>
   
     <span data-ttu-id="beb06-180">Standaard targetpw # om Hallo-wachtwoord van de doelgebruiker Hallo dat wil zeggen hoofdmap alle ALL=(ALL) alle vragen # waarschuwing!</span><span class="sxs-lookup"><span data-stu-id="beb06-180">Defaults targetpw   # ask for hello password of hello target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="beb06-181">Gebruik alleen deze samen met 'Standaardwaarden targetpw'!</span><span class="sxs-lookup"><span data-stu-id="beb06-181">Only use this together with 'Defaults targetpw'!</span></span>
9. <span data-ttu-id="beb06-182">Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="beb06-182">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="beb06-183">Dit is meestal Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="beb06-183">This is usually hello default.</span></span>
10. <span data-ttu-id="beb06-184">Maak geen wisselruimte op Hallo OS-schijf.</span><span class="sxs-lookup"><span data-stu-id="beb06-184">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="beb06-185">Hello Azure Linux Agent kunt wisselruimte Hallo lokale resource schijf die is aangesloten toohello VM na het inrichten op Azure automatisch configureren.</span><span class="sxs-lookup"><span data-stu-id="beb06-185">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="beb06-186">Houd er rekening mee dat lokale resource Hallo schijf is een *tijdelijke* schijfruimte en kan worden leeggemaakt wanneer Hallo VM gemaakt is.</span><span class="sxs-lookup"><span data-stu-id="beb06-186">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="beb06-187">Na de installatie van hello Azure Linux Agent (Zie de vorige stap), wijzigen Hallo-parameters in /etc/waagent.conf op de juiste wijze te volgen:</span><span class="sxs-lookup"><span data-stu-id="beb06-187">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="beb06-188">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Opmerking: deze moet u toobe toowhatever ingesteld.</span><span class="sxs-lookup"><span data-stu-id="beb06-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.</span></span>
11. <span data-ttu-id="beb06-189">Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="beb06-189">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="beb06-190">sudo waagent-force - deprovision</span><span class="sxs-lookup"><span data-stu-id="beb06-190">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="beb06-191">exporteren van HISTSIZE = 0</span><span class="sxs-lookup"><span data-stu-id="beb06-191">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="beb06-192">afmelden</span><span class="sxs-lookup"><span data-stu-id="beb06-192">logout</span></span>
12. <span data-ttu-id="beb06-193">Zorg ervoor dat hello die Azure Linux Agent wordt uitgevoerd bij het opstarten:</span><span class="sxs-lookup"><span data-stu-id="beb06-193">Ensure hello Azure Linux Agent runs at startup:</span></span>
    
        # sudo systemctl enable waagent.service
13. <span data-ttu-id="beb06-194">Klik op **actie-Afsluiten > omlaag** in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="beb06-194">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="beb06-195">Uw Linux VHD is nu gereed toobe tooAzure geüpload.</span><span class="sxs-lookup"><span data-stu-id="beb06-195">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="beb06-196">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="beb06-196">Next steps</span></span>
<span data-ttu-id="beb06-197">U bent nu klaar toouse uw SUSE Linux virtuele harde schijf toocreate nieuwe virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="beb06-197">You're now ready toouse your SUSE Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="beb06-198">Als dit Hallo eerste keer dat u Hallo .vhd-bestand tooAzure uploadt, Zie de stappen 2 en 3 in [maken en uploaden van een virtuele harde schijf waarop Linux-besturingssysteem Hallo](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="beb06-198">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

