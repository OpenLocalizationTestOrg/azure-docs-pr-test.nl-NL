---
title: aaaPrepare een Debian Linux VHD in Azure | Microsoft Docs
description: Meer informatie over hoe toocreate Debian 7 en 8 VHD-bestanden voor de implementatie in Azure.
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
ms.openlocfilehash: e67d126de3db146357a6509aedb5f478576768f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a><span data-ttu-id="067e9-103">Een Debian VHD voor Azure voorbereiden</span><span class="sxs-lookup"><span data-stu-id="067e9-103">Prepare a Debian VHD for Azure</span></span>
## <a name="prerequisites"></a><span data-ttu-id="067e9-104">Vereisten</span><span class="sxs-lookup"><span data-stu-id="067e9-104">Prerequisites</span></span>
<span data-ttu-id="067e9-105">Deze sectie wordt ervan uitgegaan dat u al een Debian Linux-besturingssysteem hebt geïnstalleerd vanuit een .iso-bestand dat is gedownload van Hallo [Debian website](https://www.debian.org/distrib/) tooa virtuele hardeschijf.</span><span class="sxs-lookup"><span data-stu-id="067e9-105">This section assumes that you have already installed a Debian Linux operating system from an .iso file downloaded from hello [Debian website](https://www.debian.org/distrib/) tooa virtual hard disk.</span></span> <span data-ttu-id="067e9-106">Meerdere hulpprogramma's bestaan toocreate VHD-bestanden; Hyper-V is slechts één voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="067e9-106">Multiple tools exist toocreate .vhd files; Hyper-V is only one example.</span></span> <span data-ttu-id="067e9-107">Zie voor instructies over het gebruik van Hyper-V [Hallo Hyper-V-rol installeren en configureren van een virtuele Machine](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="067e9-107">For instructions using Hyper-V, see [Install hello Hyper-V Role and Configure a Virtual Machine](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

## <a name="installation-notes"></a><span data-ttu-id="067e9-108">Opmerkingen bij de installatie</span><span class="sxs-lookup"><span data-stu-id="067e9-108">Installation notes</span></span>
* <span data-ttu-id="067e9-109">Zie ook [algemene opmerkingen bij de installatie van Linux](create-upload-generic.md#general-linux-installation-notes) voor meer tips over Linux voorbereiden voor Azure.</span><span class="sxs-lookup"><span data-stu-id="067e9-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="067e9-110">Hallo nieuwere VHDX-indeling wordt niet ondersteund in Azure.</span><span class="sxs-lookup"><span data-stu-id="067e9-110">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="067e9-111">U kunt converteren Hallo tooVHD schijfindeling met Hyper-V-beheer of Hallo **convert-vhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="067e9-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello **convert-vhd** cmdlet.</span></span>
* <span data-ttu-id="067e9-112">Bij het installeren van Hallo Linux-systeem wordt het aanbevolen dat u standaard partities in plaats van LVM (vaak Hallo standaard voor vele installaties gebruikt).</span><span class="sxs-lookup"><span data-stu-id="067e9-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="067e9-113">Dit voorkomt LVM naam conflicteert met de gekloonde virtuele machines, met name een besturingssysteemschijf ooit moet toobe gekoppeld tooanother VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="067e9-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="067e9-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mag worden gebruikt voor gegevensschijven als voorkeur.</span><span class="sxs-lookup"><span data-stu-id="067e9-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="067e9-115">Configureer een partitie van de wisseling niet op Hallo OS-schijf.</span><span class="sxs-lookup"><span data-stu-id="067e9-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="067e9-116">Hello Azure Linux-agent kan worden geconfigureerd toocreate een wisselbestand op Hallo tijdelijke schijf.</span><span class="sxs-lookup"><span data-stu-id="067e9-116">hello Azure Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="067e9-117">Meer informatie hierover vindt u in onderstaande Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="067e9-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="067e9-118">Alle VHD's Hallo moeten grootten die veelvouden van 1 MB hebben.</span><span class="sxs-lookup"><span data-stu-id="067e9-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-azure-manage-toocreate-debian-vhds"></a><span data-ttu-id="067e9-119">Azure beheren toocreate Debian VHD gebruiken</span><span class="sxs-lookup"><span data-stu-id="067e9-119">Use Azure-Manage toocreate Debian VHDs</span></span>
<span data-ttu-id="067e9-120">Er zijn extra beschikbaar voor het genereren van Debian VHD's voor Azure, zoals Hallo [azure-beheren](https://github.com/credativ/azure-manage) scripts van [credativ](http://www.credativ.com/).</span><span class="sxs-lookup"><span data-stu-id="067e9-120">There are tools available for generating Debian VHDs for Azure, such as hello [azure-manage](https://github.com/credativ/azure-manage) scripts from [credativ](http://www.credativ.com/).</span></span> <span data-ttu-id="067e9-121">Dit is de aanbevolen aanpak ten opzichte van een installatiekopie van het maken van nieuw Hallo.</span><span class="sxs-lookup"><span data-stu-id="067e9-121">This is hello recommended approach versus creating an image from scratch.</span></span> <span data-ttu-id="067e9-122">Bijvoorbeeld, toocreate een Debian 8 VHD uitgevoerd Hallo na opdrachten toodownload azure beheren (en afhankelijkheden) en Hallo azure_build_image script uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="067e9-122">For example, toocreate a Debian 8 VHD run hello following commands toodownload azure-manage (and dependencies) and run hello azure_build_image script:</span></span>

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a><span data-ttu-id="067e9-123">Handmatig een Debian VHD voorbereiden</span><span class="sxs-lookup"><span data-stu-id="067e9-123">Manually prepare a Debian VHD</span></span>
1. <span data-ttu-id="067e9-124">Selecteer Hallo virtuele machine in Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="067e9-124">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="067e9-125">Klik op **Connect** tooopen een consolevenster voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="067e9-125">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="067e9-126">Hallo-regel voor commentaar **deb cdrom** in `/etc/apt/source.list` als u Hallo VM op basis van een ISO-bestand instelt.</span><span class="sxs-lookup"><span data-stu-id="067e9-126">Comment out hello line for **deb cdrom** in `/etc/apt/source.list` if you set up hello VM against an ISO file.</span></span>
4. <span data-ttu-id="067e9-127">Hallo bewerken `/etc/default/grub` bestand en wijzig Hallo **GRUB_CMDLINE_LINUX** parameter als volgt tooinclude kernel extra parameters voor Azure.</span><span class="sxs-lookup"><span data-stu-id="067e9-127">Edit hello `/etc/default/grub` file and modify hello **GRUB_CMDLINE_LINUX** parameter as follows tooinclude additional kernel parameters for Azure.</span></span>
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. <span data-ttu-id="067e9-128">Hallo wormgaten bouwen en uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="067e9-128">Rebuild hello grub and run:</span></span>
   
        # sudo update-grub
6. <span data-ttu-id="067e9-129">Debian van Azure-opslagplaatsen too/etc/apt/sources.list voor Debian 7 of 8 toevoegen:</span><span class="sxs-lookup"><span data-stu-id="067e9-129">Add Debian's Azure repositories too/etc/apt/sources.list for either Debian 7 or 8:</span></span>
   
    <span data-ttu-id="067e9-130">**Debian 7.x 'Wheezy'**</span><span class="sxs-lookup"><span data-stu-id="067e9-130">**Debian 7.x "Wheezy"**</span></span>
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    <span data-ttu-id="067e9-131">**Debian 8.x 'Jessie'**</span><span class="sxs-lookup"><span data-stu-id="067e9-131">**Debian 8.x "Jessie"**</span></span>

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. <span data-ttu-id="067e9-132">Hello Azure Linux Agent installeren:</span><span class="sxs-lookup"><span data-stu-id="067e9-132">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. <span data-ttu-id="067e9-133">Voor Debian 7 is het vereiste toorun Hallo 3,16 gebaseerde kernel uit Hallo wheezy backports opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="067e9-133">For Debian 7, it is required toorun hello 3.16-based kernel from hello wheezy-backports repository.</span></span> <span data-ttu-id="067e9-134">Maak eerst een bestand met de naam van /etc/apt/preferences.d/linux.pref Hello inhoud na:</span><span class="sxs-lookup"><span data-stu-id="067e9-134">First create a file called /etc/apt/preferences.d/linux.pref with hello following contents:</span></span>
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    <span data-ttu-id="067e9-135">Voer 'apt sudo get-installeren linux-installatiekopie-amd64' tooinstall Hallo nieuwe kernel.</span><span class="sxs-lookup"><span data-stu-id="067e9-135">Then run "sudo apt-get install linux-image-amd64" tooinstall hello new kernel.</span></span>
3. <span data-ttu-id="067e9-136">Inrichting ervan ongedaan Hallo virtuele machine en deze voorbereiden voor het inrichten op Azure en uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="067e9-136">Deprovision hello virtual machine and prepare it for provisioning on Azure and run:</span></span>
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. <span data-ttu-id="067e9-137">Klik op **actie** -afsluiten > omlaag in de Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="067e9-137">Click **Action** -> Shut Down in Hyper-V Manager.</span></span> <span data-ttu-id="067e9-138">Uw Linux VHD is nu gereed toobe tooAzure geüpload.</span><span class="sxs-lookup"><span data-stu-id="067e9-138">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="067e9-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="067e9-139">Next steps</span></span>
<span data-ttu-id="067e9-140">U bent nu klaar toouse uw Debian virtuele harde schijf toocreate nieuwe virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="067e9-140">You're now ready toouse your Debian virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="067e9-141">Als dit Hallo eerste keer dat u Hallo .vhd-bestand tooAzure uploadt, Zie de stappen 2 en 3 in [maken en uploaden van een virtuele harde schijf waarop Linux-besturingssysteem Hallo](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="067e9-141">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

