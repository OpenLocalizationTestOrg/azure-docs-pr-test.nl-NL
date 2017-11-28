---
title: aaaCreate een Ubuntu Linux-VHD en uploaden in Azure
description: Informatie over toocreate en uploaden van een Azure virtuele harde schijf (VHD) die een Ubuntu Linux-besturingssysteem bevat.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 3e097959-84fc-4f6a-8cc8-35e087fd1542
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: cc546a487f769b32432a7e80ddcd0f6af44e201f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a><span data-ttu-id="070bb-103">Een virtuele Ubuntu-machine voor Azure voorbereiden</span><span class="sxs-lookup"><span data-stu-id="070bb-103">Prepare an Ubuntu virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a><span data-ttu-id="070bb-104">Officiële Ubuntu cloud installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="070bb-104">Official Ubuntu cloud images</span></span>
<span data-ttu-id="070bb-105">Ubuntu publiceert nu officiële Azure VHD's worden gedownload op [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="070bb-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span></span> <span data-ttu-id="070bb-106">Als u uw eigen gespecialiseerde Ubuntu-installatiekopie van toobuild nodig voor Azure, plaats gebruik Hallo handmatige procedure eronder wordt aanbevolen toostart met deze bekende werkt VHD's en indien nodig aanpassen.</span><span class="sxs-lookup"><span data-stu-id="070bb-106">If you need toobuild your own specialized Ubuntu image for Azure, rather than use hello manual procedure below it is recommended toostart with these known working VHDs and customize as needed.</span></span> <span data-ttu-id="070bb-107">Hallo laatste installatiekopie releases kunnen altijd worden gevonden op Hallo volgende locaties:</span><span class="sxs-lookup"><span data-stu-id="070bb-107">hello latest image releases can always be found at hello following locations:</span></span>

* <span data-ttu-id="070bb-108">Ubuntu 12.04/nauwkeurig: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="070bb-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="070bb-109">Ubuntu 14.04/betrouwbare: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="070bb-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="070bb-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="070bb-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="070bb-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="070bb-111">Prerequisites</span></span>
<span data-ttu-id="070bb-112">In dit artikel wordt ervan uitgegaan dat u al een Ubuntu Linux-besturingssysteem tooa virtuele harde schijf hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="070bb-112">This article assumes that you have already installed an Ubuntu Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="070bb-113">Meerdere hulpprogramma's bestaan toocreate VHD-bestanden, bijvoorbeeld een virtualisatieoplossing zoals Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="070bb-113">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="070bb-114">Zie voor instructies [Hallo Hyper-V-rol installeren en configureren van een virtuele Machine](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="070bb-114">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="070bb-115">**Opmerkingen bij de installatie Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="070bb-115">**Ubuntu installation notes**</span></span>

* <span data-ttu-id="070bb-116">Zie ook [algemene opmerkingen bij de installatie van Linux](create-upload-generic.md#general-linux-installation-notes) voor meer tips over Linux voorbereiden voor Azure.</span><span class="sxs-lookup"><span data-stu-id="070bb-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="070bb-117">Hallo VHDX-indeling wordt niet ondersteund in Azure, alleen **vaste VHD**.</span><span class="sxs-lookup"><span data-stu-id="070bb-117">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="070bb-118">U kunt converteren Hallo tooVHD schijfindeling met behulp van Hyper-V-beheer of Hallo cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="070bb-118">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="070bb-119">Bij het installeren van Hallo Linux-systeem wordt het aanbevolen dat u standaard partities in plaats van LVM (vaak Hallo standaard voor vele installaties gebruikt).</span><span class="sxs-lookup"><span data-stu-id="070bb-119">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="070bb-120">Dit voorkomt LVM naam conflicteert met de gekloonde virtuele machines, met name een besturingssysteemschijf ooit moet toobe gekoppeld tooanother VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="070bb-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="070bb-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mag worden gebruikt voor gegevensschijven als voorkeur.</span><span class="sxs-lookup"><span data-stu-id="070bb-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="070bb-122">Configureer een partitie van de wisseling niet op Hallo OS-schijf.</span><span class="sxs-lookup"><span data-stu-id="070bb-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="070bb-123">Hallo Linux-agent kan worden geconfigureerd toocreate een wisselbestand op Hallo tijdelijke schijf.</span><span class="sxs-lookup"><span data-stu-id="070bb-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="070bb-124">Meer informatie hierover vindt u in onderstaande Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="070bb-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="070bb-125">Alle VHD's Hallo moeten grootten die veelvouden van 1 MB hebben.</span><span class="sxs-lookup"><span data-stu-id="070bb-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="manual-steps"></a><span data-ttu-id="070bb-126">Handmatige stappen</span><span class="sxs-lookup"><span data-stu-id="070bb-126">Manual steps</span></span>
> [!NOTE]
> <span data-ttu-id="070bb-127">Voordat u probeert toocreate uw eigen aangepaste installatiekopie Ubuntu voor Azure, overweeg Hallo met vooraf gemaakte en installatiekopieën van getest [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="070bb-127">Before attempting toocreate your own custom Ubuntu image for Azure, please consider using hello pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span></span>
> 
> 

1. <span data-ttu-id="070bb-128">Selecteer Hallo virtuele machine in Hallo middelste deelvenster van de Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="070bb-128">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="070bb-129">Klik op **Connect** tooopen Hallo venster voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="070bb-129">Click **Connect** tooopen hello window for hello virtual machine.</span></span>

3. <span data-ttu-id="070bb-130">Huidige Hallo-opslagplaatsen in Hallo installatiekopie toouse Ubuntu van Azure repo's vervangen.</span><span class="sxs-lookup"><span data-stu-id="070bb-130">Replace hello current repositories in hello image toouse Ubuntu's Azure repos.</span></span> <span data-ttu-id="070bb-131">Hallo stappen verschillen, afhankelijk van Hallo Ubuntu-versie.</span><span class="sxs-lookup"><span data-stu-id="070bb-131">hello steps vary slightly depending on hello Ubuntu version.</span></span>
   
    <span data-ttu-id="070bb-132">Voordat u bewerkt `/etc/apt/sources.list`, het is aanbevolen toomake een back-up:</span><span class="sxs-lookup"><span data-stu-id="070bb-132">Before editing `/etc/apt/sources.list`, it is recommended toomake a backup:</span></span>
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    <span data-ttu-id="070bb-133">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="070bb-133">Ubuntu 12.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="070bb-134">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="070bb-134">Ubuntu 14.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="070bb-135">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="070bb-135">Ubuntu 16.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. <span data-ttu-id="070bb-136">Hallo Ubuntu Azure installatiekopieën volgt nu Hallo *hardware stuk* kernel (HWE).</span><span class="sxs-lookup"><span data-stu-id="070bb-136">hello Ubuntu Azure images are now following hello *hardware enablement* (HWE) kernel.</span></span> <span data-ttu-id="070bb-137">Hallo besturingssysteem toohello nieuwste kernel bijwerken door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="070bb-137">Update hello operating system toohello latest kernel by running hello following commands:</span></span>

    <span data-ttu-id="070bb-138">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="070bb-138">Ubuntu 12.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    <span data-ttu-id="070bb-139">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="070bb-139">Ubuntu 14.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    <span data-ttu-id="070bb-140">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="070bb-140">Ubuntu 16.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    <span data-ttu-id="070bb-141">**Zie ook:**</span><span class="sxs-lookup"><span data-stu-id="070bb-141">**See also:**</span></span>
    - [<span data-ttu-id="070bb-142">https://Wiki.Ubuntu.com/kernel/LTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="070bb-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [<span data-ttu-id="070bb-143">https://Wiki.Ubuntu.com/kernel/RollingLTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="070bb-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. <span data-ttu-id="070bb-144">Hallo kernel opstarten regel voor wormgaten tooinclude kernel extra parameters voor Azure wijzigen.</span><span class="sxs-lookup"><span data-stu-id="070bb-144">Modify hello kernel boot line for Grub tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="070bb-145">dit open toodo `/etc/default/grub` vinden in een teksteditor Hallo variabele met de naam `GRUB_CMDLINE_LINUX_DEFAULT` (of toe te voegen indien nodig) en bewerk het tooinclude Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="070bb-145">toodo this open `/etc/default/grub` in a text editor, find hello variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it tooinclude hello following parameters:</span></span>
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    <span data-ttu-id="070bb-146">Opslaan en sluiten van dit bestand en voer `sudo update-grub`.</span><span class="sxs-lookup"><span data-stu-id="070bb-146">Save and close this file, and then run `sudo update-grub`.</span></span> <span data-ttu-id="070bb-147">Dit zorgt ervoor dat alle consoleberichten toohello eerste seriële poort, die Azure technische ondersteuning helpen kan bij het opsporen van problemen worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="070bb-147">This will ensure all console messages are sent toohello first serial port, which can assist Azure technical support with debugging issues.</span></span>

6. <span data-ttu-id="070bb-148">Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="070bb-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="070bb-149">Dit is meestal Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="070bb-149">This is usually hello default.</span></span>

7. <span data-ttu-id="070bb-150">Hello Azure Linux Agent installeren:</span><span class="sxs-lookup"><span data-stu-id="070bb-150">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    <span data-ttu-id="070bb-151">Hallo `walinuxagent` pakket kan verwijderen Hallo `NetworkManager` en `NetworkManager-gnome` pakketten als ze zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="070bb-151">hello `walinuxagent` package may remove hello `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span></span>

8. <span data-ttu-id="070bb-152">Voer Hallo opdrachten toodeprovision Hallo virtuele machine te volgen en voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="070bb-152">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. <span data-ttu-id="070bb-153">Klik op **actie-Afsluiten > omlaag** in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="070bb-153">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="070bb-154">Uw Linux VHD is nu gereed toobe tooAzure geüpload.</span><span class="sxs-lookup"><span data-stu-id="070bb-154">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="070bb-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="070bb-155">Next steps</span></span>
<span data-ttu-id="070bb-156">U bent nu klaar toouse uw Ubuntu Linux virtuele harde schijf toocreate nieuwe virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="070bb-156">You're now ready toouse your Ubuntu Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="070bb-157">Als dit Hallo eerste keer dat u Hallo .vhd-bestand tooAzure uploadt, Zie de stappen 2 en 3 in [maken en uploaden van een virtuele harde schijf waarop Linux-besturingssysteem Hallo](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="070bb-157">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="references"></a><span data-ttu-id="070bb-158">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="070bb-158">References</span></span>
<span data-ttu-id="070bb-159">Ubuntu hardware inschakelen (HWE) kernel:</span><span class="sxs-lookup"><span data-stu-id="070bb-159">Ubuntu hardware enablement (HWE) kernel:</span></span>

* [<span data-ttu-id="070bb-160">http://blog.utlemming.org/2015/01/Ubuntu-1404-Azure-images-Now-Tracking.HTML</span><span class="sxs-lookup"><span data-stu-id="070bb-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span></span>](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [<span data-ttu-id="070bb-161">http://blog.utlemming.org/2015/02/1204-Azure-cloud-images-Now-Using-Hwe.HTML</span><span class="sxs-lookup"><span data-stu-id="070bb-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span></span>](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

