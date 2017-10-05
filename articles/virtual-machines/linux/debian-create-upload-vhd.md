---
title: Voorbereiden van een Debian Linux-VHD in Azure | Microsoft Docs
description: Informatie over het maken van Debian 7 en 8 VHD-bestanden voor implementatie in Azure.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: a6de7a7c-cc70-44e7-aed0-2ae6884d401a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 63970d162c12984d6476bf0b9fc4ab70160eccdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a><span data-ttu-id="9e7c3-103">Een Debian VHD voor Azure voorbereiden</span><span class="sxs-lookup"><span data-stu-id="9e7c3-103">Prepare a Debian VHD for Azure</span></span>
## <a name="prerequisites"></a><span data-ttu-id="9e7c3-104">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9e7c3-104">Prerequisites</span></span>
<span data-ttu-id="9e7c3-105">Deze sectie wordt ervan uitgegaan dat u al een Debian Linux-besturingssysteem hebt geïnstalleerd vanuit een .iso-bestand dat is gedownload van de [Debian website](https://www.debian.org/distrib/) op een virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-105">This section assumes that you have already installed a Debian Linux operating system from an .iso file downloaded from the [Debian website](https://www.debian.org/distrib/) to a virtual hard disk.</span></span> <span data-ttu-id="9e7c3-106">Bestaan meerdere hulpprogramma's voor het maken van de VHD-bestanden; Hyper-V is slechts één voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-106">Multiple tools exist to create .vhd files; Hyper-V is only one example.</span></span> <span data-ttu-id="9e7c3-107">Zie voor instructies over het gebruik van Hyper-V [de Hyper-V-rol installeren en configureren van een virtuele Machine](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e7c3-107">For instructions using Hyper-V, see [Install the Hyper-V Role and Configure a Virtual Machine](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

## <a name="installation-notes"></a><span data-ttu-id="9e7c3-108">Opmerkingen bij de installatie</span><span class="sxs-lookup"><span data-stu-id="9e7c3-108">Installation notes</span></span>
* <span data-ttu-id="9e7c3-109">Zie ook [algemene opmerkingen bij de installatie van Linux](create-upload-generic.md#general-linux-installation-notes) voor meer tips over Linux voorbereiden voor Azure.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="9e7c3-110">De nieuwe VHDX-indeling wordt niet ondersteund in Azure.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-110">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="9e7c3-111">U kunt de schijf converteren naar VHD-indeling met behulp van Hyper-V-beheer of de **convert-vhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-111">You can convert the disk to VHD format using Hyper-V Manager or the **convert-vhd** cmdlet.</span></span>
* <span data-ttu-id="9e7c3-112">Bij het installeren van de Linux-systeem wordt het aanbevolen dat u standaard partities in plaats van LVM (vaak de standaardinstelling voor vele installaties gebruikt).</span><span class="sxs-lookup"><span data-stu-id="9e7c3-112">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="9e7c3-113">Dit voorkomt LVM naam conflicteert met de gekloonde virtuele machines, met name als een besturingssysteemschijf ooit worden gekoppeld aan een andere virtuele machine moet voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="9e7c3-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mag worden gebruikt voor gegevensschijven als voorkeur.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="9e7c3-115">Configureer een partitie van de wisseling niet op de schijf met het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-115">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="9e7c3-116">De Azure Linux-agent kan worden geconfigureerd voor het maken van een wisselbestand op de tijdelijke schijf.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-116">The Azure Linux agent can be configured to create a swap file on the temporary resource disk.</span></span> <span data-ttu-id="9e7c3-117">Meer informatie hierover vindt u in de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-117">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="9e7c3-118">Alle van de VHD's moeten grootten die veelvouden van 1 MB hebben.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-118">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-azure-manage-to-create-debian-vhds"></a><span data-ttu-id="9e7c3-119">Gebruik Azure beheren voor het maken van Debian VHD 's</span><span class="sxs-lookup"><span data-stu-id="9e7c3-119">Use Azure-Manage to create Debian VHDs</span></span>
<span data-ttu-id="9e7c3-120">Er zijn extra beschikbaar voor het genereren van Debian VHD's voor Azure, zoals de [azure-beheren](https://github.com/credativ/azure-manage) scripts van [credativ](http://www.credativ.com/).</span><span class="sxs-lookup"><span data-stu-id="9e7c3-120">There are tools available for generating Debian VHDs for Azure, such as the [azure-manage](https://github.com/credativ/azure-manage) scripts from [credativ](http://www.credativ.com/).</span></span> <span data-ttu-id="9e7c3-121">Dit is de aanbevolen aanpak ten opzichte van een installatiekopie van het maken van nieuw.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-121">This is the recommended approach versus creating an image from scratch.</span></span> <span data-ttu-id="9e7c3-122">Bijvoorbeeld, te maken van een Debian 8 VHD Voer de volgende opdrachten voor het downloaden van azure beheren (en de afhankelijkheden) en voer het script azure_build_image:</span><span class="sxs-lookup"><span data-stu-id="9e7c3-122">For example, to create a Debian 8 VHD run the following commands to download azure-manage (and dependencies) and run the azure_build_image script:</span></span>

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a><span data-ttu-id="9e7c3-123">Handmatig een Debian VHD voorbereiden</span><span class="sxs-lookup"><span data-stu-id="9e7c3-123">Manually prepare a Debian VHD</span></span>
1. <span data-ttu-id="9e7c3-124">Selecteer de virtuele machine in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-124">In Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="9e7c3-125">Klik op **Connect** om een consolevenster voor de virtuele machine te openen.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-125">Click **Connect** to open a console window for the virtual machine.</span></span>
3. <span data-ttu-id="9e7c3-126">De regel voor commentaar **deb cdrom** in `/etc/apt/source.list` als u de virtuele machine op basis van een ISO-bestand instelt.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-126">Comment out the line for **deb cdrom** in `/etc/apt/source.list` if you set up the VM against an ISO file.</span></span>
4. <span data-ttu-id="9e7c3-127">Bewerk de `/etc/default/grub` bestand en wijzig de **GRUB_CMDLINE_LINUX** parameter de als volgt aanvullende kernel-parameters voor Azure.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-127">Edit the `/etc/default/grub` file and modify the **GRUB_CMDLINE_LINUX** parameter as follows to include additional kernel parameters for Azure.</span></span>
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. <span data-ttu-id="9e7c3-128">De grub bouwen en uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9e7c3-128">Rebuild the grub and run:</span></span>
   
        # sudo update-grub
6. <span data-ttu-id="9e7c3-129">Azure van Debian-opslagplaatsen aan /etc/apt/sources.list voor Debian 7 of 8 toevoegen:</span><span class="sxs-lookup"><span data-stu-id="9e7c3-129">Add Debian's Azure repositories to /etc/apt/sources.list for either Debian 7 or 8:</span></span>
   
    <span data-ttu-id="9e7c3-130">**Debian 7.x 'Wheezy'**</span><span class="sxs-lookup"><span data-stu-id="9e7c3-130">**Debian 7.x "Wheezy"**</span></span>
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    <span data-ttu-id="9e7c3-131">**Debian 8.x 'Jessie'**</span><span class="sxs-lookup"><span data-stu-id="9e7c3-131">**Debian 8.x "Jessie"**</span></span>

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. <span data-ttu-id="9e7c3-132">Installeer de Azure Linux Agent:</span><span class="sxs-lookup"><span data-stu-id="9e7c3-132">Install the Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. <span data-ttu-id="9e7c3-133">Voor Debian 7 is vereist voor het uitvoeren van de kernel 3,16 gebaseerde vanuit de opslagplaats wheezy backports.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-133">For Debian 7, it is required to run the 3.16-based kernel from the wheezy-backports repository.</span></span> <span data-ttu-id="9e7c3-134">Maak eerst een bestand met de naam /etc/apt/preferences.d/linux.pref met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="9e7c3-134">First create a file called /etc/apt/preferences.d/linux.pref with the following contents:</span></span>
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    <span data-ttu-id="9e7c3-135">Voer 'sudo apt get-installatie linux-installatiekopie-amd64' voor het installeren van de nieuwe kernel.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-135">Then run "sudo apt-get install linux-image-amd64" to install the new kernel.</span></span>
3. <span data-ttu-id="9e7c3-136">Inrichting ervan ongedaan maakt de virtuele machine en deze voorbereiden voor het inrichten op Azure en uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9e7c3-136">Deprovision the virtual machine and prepare it for provisioning on Azure and run:</span></span>
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. <span data-ttu-id="9e7c3-137">Klik op **actie** -afsluiten > omlaag in de Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-137">Click **Action** -> Shut Down in Hyper-V Manager.</span></span> <span data-ttu-id="9e7c3-138">Uw Linux VHD is nu gereed om te worden geüpload naar Azure.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-138">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e7c3-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9e7c3-139">Next steps</span></span>
<span data-ttu-id="9e7c3-140">U bent nu klaar voor gebruik van de Debian virtuele harde schijf maken van nieuwe virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="9e7c3-140">You're now ready to use your Debian virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="9e7c3-141">Als dit de eerste keer dat u de VHD-bestand naar Azure uploadt, Zie de stappen 2 en 3 in [maken en uploaden van een virtuele harde schijf met het Linux-besturingssysteem](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e7c3-141">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

