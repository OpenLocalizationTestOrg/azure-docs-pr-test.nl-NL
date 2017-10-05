---
title: Maken en uploaden van een VHD Ubuntu Linux in Azure
description: Informatie over het maken en uploaden van een Azure virtuele harde schijf (VHD) die een Ubuntu Linux-besturingssysteem bevat.
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
ms.openlocfilehash: 4496b34ff88ca1e08cc74788ae09d787d4399eaf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a><span data-ttu-id="e1377-103">Een virtuele Ubuntu-machine voor Azure voorbereiden</span><span class="sxs-lookup"><span data-stu-id="e1377-103">Prepare an Ubuntu virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a><span data-ttu-id="e1377-104">Officiële Ubuntu cloud installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="e1377-104">Official Ubuntu cloud images</span></span>
<span data-ttu-id="e1377-105">Ubuntu publiceert nu officiële Azure VHD's worden gedownload op [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="e1377-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span></span> <span data-ttu-id="e1377-106">Als u nodig hebt om uw eigen gespecialiseerde Ubuntu installatiekopie ontwikkelen voor Azure, in plaats daarvan dan de handmatige procedure hieronder gebruiken het verdient aanbeveling om te starten met deze bekende VHD's werkt en indien nodig aanpassen.</span><span class="sxs-lookup"><span data-stu-id="e1377-106">If you need to build your own specialized Ubuntu image for Azure, rather than use the manual procedure below it is recommended to start with these known working VHDs and customize as needed.</span></span> <span data-ttu-id="e1377-107">De nieuwste versies van de installatiekopie kunnen altijd worden gevonden op de volgende locaties:</span><span class="sxs-lookup"><span data-stu-id="e1377-107">The latest image releases can always be found at the following locations:</span></span>

* <span data-ttu-id="e1377-108">Ubuntu 12.04/nauwkeurig: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="e1377-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="e1377-109">Ubuntu 14.04/betrouwbare: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="e1377-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="e1377-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="e1377-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1377-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e1377-111">Prerequisites</span></span>
<span data-ttu-id="e1377-112">In dit artikel wordt ervan uitgegaan dat u al een Ubuntu Linux-besturingssysteem hebt geïnstalleerd op een virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="e1377-112">This article assumes that you have already installed an Ubuntu Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="e1377-113">Er bestaan meerdere hulpprogramma's voor het maken van de VHD-bestanden, bijvoorbeeld een virtualisatieoplossing zoals Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e1377-113">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="e1377-114">Zie voor instructies [de Hyper-V-rol installeren en configureren van een virtuele Machine](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="e1377-114">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="e1377-115">**Opmerkingen bij de installatie Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="e1377-115">**Ubuntu installation notes**</span></span>

* <span data-ttu-id="e1377-116">Zie ook [algemene opmerkingen bij de installatie van Linux](create-upload-generic.md#general-linux-installation-notes) voor meer tips over Linux voorbereiden voor Azure.</span><span class="sxs-lookup"><span data-stu-id="e1377-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="e1377-117">De VHDX-indeling wordt niet ondersteund in Azure, alleen **vaste VHD**.</span><span class="sxs-lookup"><span data-stu-id="e1377-117">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="e1377-118">U kunt de schijf converteren naar VHD-indeling met behulp van Hyper-V-beheer of de cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="e1377-118">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="e1377-119">Bij het installeren van de Linux-systeem wordt het aanbevolen dat u standaard partities in plaats van LVM (vaak de standaardinstelling voor vele installaties gebruikt).</span><span class="sxs-lookup"><span data-stu-id="e1377-119">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="e1377-120">Dit voorkomt LVM naam conflicteert met de gekloonde virtuele machines, met name als een besturingssysteemschijf ooit worden gekoppeld aan een andere virtuele machine moet voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="e1377-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="e1377-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mag worden gebruikt voor gegevensschijven als voorkeur.</span><span class="sxs-lookup"><span data-stu-id="e1377-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="e1377-122">Configureer een partitie van de wisseling niet op de schijf met het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="e1377-122">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="e1377-123">De Linux-agent kan worden geconfigureerd voor het maken van een wisselbestand op de tijdelijke schijf.</span><span class="sxs-lookup"><span data-stu-id="e1377-123">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="e1377-124">Meer informatie hierover vindt u in de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="e1377-124">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="e1377-125">Alle van de VHD's moeten grootten die veelvouden van 1 MB hebben.</span><span class="sxs-lookup"><span data-stu-id="e1377-125">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="manual-steps"></a><span data-ttu-id="e1377-126">Handmatige stappen</span><span class="sxs-lookup"><span data-stu-id="e1377-126">Manual steps</span></span>
> [!NOTE]
> <span data-ttu-id="e1377-127">Voordat u uw eigen aangepaste Ubuntu-afbeelding voor Azure maken, u kunt overwegen de installatiekopieën van het vooraf samengestelde en geteste van [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="e1377-127">Before attempting to create your own custom Ubuntu image for Azure, please consider using the pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span></span>
> 
> 

1. <span data-ttu-id="e1377-128">Selecteer in het middelste deelvenster van de Hyper-V-beheer, de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e1377-128">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="e1377-129">Klik op **Connect** om het venster voor de virtuele machine te openen.</span><span class="sxs-lookup"><span data-stu-id="e1377-129">Click **Connect** to open the window for the virtual machine.</span></span>

3. <span data-ttu-id="e1377-130">Vervang de huidige opslagplaatsen in de installatiekopie van Ubuntu Azure repo's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e1377-130">Replace the current repositories in the image to use Ubuntu's Azure repos.</span></span> <span data-ttu-id="e1377-131">De stappen verschillen, afhankelijk van de Ubuntu-versie.</span><span class="sxs-lookup"><span data-stu-id="e1377-131">The steps vary slightly depending on the Ubuntu version.</span></span>
   
    <span data-ttu-id="e1377-132">Voordat u bewerkt `/etc/apt/sources.list`, wordt u aangeraden te maken van een back-up:</span><span class="sxs-lookup"><span data-stu-id="e1377-132">Before editing `/etc/apt/sources.list`, it is recommended to make a backup:</span></span>
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    <span data-ttu-id="e1377-133">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="e1377-133">Ubuntu 12.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="e1377-134">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="e1377-134">Ubuntu 14.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="e1377-135">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="e1377-135">Ubuntu 16.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. <span data-ttu-id="e1377-136">De afbeeldingen Ubuntu Azure volgt nu de *hardware stuk* kernel (HWE).</span><span class="sxs-lookup"><span data-stu-id="e1377-136">The Ubuntu Azure images are now following the *hardware enablement* (HWE) kernel.</span></span> <span data-ttu-id="e1377-137">Werk het besturingssysteem naar de meest recente kernel met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="e1377-137">Update the operating system to the latest kernel by running the following commands:</span></span>

    <span data-ttu-id="e1377-138">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="e1377-138">Ubuntu 12.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    <span data-ttu-id="e1377-139">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="e1377-139">Ubuntu 14.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    <span data-ttu-id="e1377-140">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="e1377-140">Ubuntu 16.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    <span data-ttu-id="e1377-141">**Zie ook:**</span><span class="sxs-lookup"><span data-stu-id="e1377-141">**See also:**</span></span>
    - [<span data-ttu-id="e1377-142">https://Wiki.Ubuntu.com/kernel/LTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="e1377-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [<span data-ttu-id="e1377-143">https://Wiki.Ubuntu.com/kernel/RollingLTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="e1377-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. <span data-ttu-id="e1377-144">De regel voor het opstarten van kernel voor wormgaten aanvullende kernel-parameters voor Azure opnemen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e1377-144">Modify the kernel boot line for Grub to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="e1377-145">Deze open doen `/etc/default/grub` in een teksteditor, ziet u de variabele met de naam `GRUB_CMDLINE_LINUX_DEFAULT` (of toe te voegen indien nodig) en het bewerken om op te nemen van de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="e1377-145">To do this open `/etc/default/grub` in a text editor, find the variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it to include the following parameters:</span></span>
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    <span data-ttu-id="e1377-146">Opslaan en sluiten van dit bestand en voer `sudo update-grub`.</span><span class="sxs-lookup"><span data-stu-id="e1377-146">Save and close this file, and then run `sudo update-grub`.</span></span> <span data-ttu-id="e1377-147">Dit zorgt ervoor dat alle consoleberichten worden verzonden naar de eerste seriële poort, die Azure technische ondersteuning helpen kan bij het opsporen van problemen.</span><span class="sxs-lookup"><span data-stu-id="e1377-147">This will ensure all console messages are sent to the first serial port, which can assist Azure technical support with debugging issues.</span></span>

6. <span data-ttu-id="e1377-148">Zorg ervoor dat de SSH-server is geïnstalleerd en geconfigureerd om te starten tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="e1377-148">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="e1377-149">Dit is doorgaans de standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="e1377-149">This is usually the default.</span></span>

7. <span data-ttu-id="e1377-150">Installeer de Azure Linux Agent:</span><span class="sxs-lookup"><span data-stu-id="e1377-150">Install the Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    <span data-ttu-id="e1377-151">De `walinuxagent` pakket kan verwijderen de `NetworkManager` en `NetworkManager-gnome` pakketten als ze zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e1377-151">The `walinuxagent` package may remove the `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span></span>

8. <span data-ttu-id="e1377-152">Voer de volgende opdrachten inrichting ervan ongedaan maakt de virtuele machine en deze voorbereiden voor het inrichten op Azure:</span><span class="sxs-lookup"><span data-stu-id="e1377-152">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. <span data-ttu-id="e1377-153">Klik op **actie-Afsluiten > omlaag** in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="e1377-153">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="e1377-154">Uw Linux VHD is nu gereed om te worden geüpload naar Azure.</span><span class="sxs-lookup"><span data-stu-id="e1377-154">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1377-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e1377-155">Next steps</span></span>
<span data-ttu-id="e1377-156">U bent nu klaar voor gebruik van de Ubuntu Linux virtuele harde schijf maken van nieuwe virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="e1377-156">You're now ready to use your Ubuntu Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="e1377-157">Als dit de eerste keer dat u de VHD-bestand naar Azure uploadt, Zie de stappen 2 en 3 in [maken en uploaden van een virtuele harde schijf met het Linux-besturingssysteem](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e1377-157">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="references"></a><span data-ttu-id="e1377-158">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="e1377-158">References</span></span>
<span data-ttu-id="e1377-159">Ubuntu hardware inschakelen (HWE) kernel:</span><span class="sxs-lookup"><span data-stu-id="e1377-159">Ubuntu hardware enablement (HWE) kernel:</span></span>

* [<span data-ttu-id="e1377-160">http://blog.utlemming.org/2015/01/Ubuntu-1404-Azure-images-Now-Tracking.HTML</span><span class="sxs-lookup"><span data-stu-id="e1377-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span></span>](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [<span data-ttu-id="e1377-161">http://blog.utlemming.org/2015/02/1204-Azure-cloud-images-Now-Using-Hwe.HTML</span><span class="sxs-lookup"><span data-stu-id="e1377-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span></span>](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

