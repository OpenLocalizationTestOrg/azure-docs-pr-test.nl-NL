---
title: aaaLinux VM apparaatnamen zijn gewijzigd in Azure | Microsoft Docs
description: Legt uit Hallo waarom apparaatnamen worden gewijzigd en bieden oplossing voor dit probleem.
services: virtual-machines-linux
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: 
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 4d3a5853d61edd2c8e8b85ab69e5ed3b3bc00bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a><span data-ttu-id="27615-103">Voor probleemoplossing: Apparaatnamen Linux VM zijn gewijzigd</span><span class="sxs-lookup"><span data-stu-id="27615-103">Troubleshooting: Linux VM device names are changed</span></span>

<span data-ttu-id="27615-104">Hallo artikel wordt uitgelegd waarom apparaatnamen zijn gewijzigd nadat u een Linux-virtuele machine (VM) opnieuw opstarten of opnieuw Hallo-schijven koppelen.</span><span class="sxs-lookup"><span data-stu-id="27615-104">hello article explains why device names are changed after you restart a Linux virtual machine (VM), or reattach hello disks.</span></span> <span data-ttu-id="27615-105">Ook biedt het Hallo-oplossing voor dit probleem.</span><span class="sxs-lookup"><span data-stu-id="27615-105">It also provides hello solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="27615-106">Symptoom</span><span class="sxs-lookup"><span data-stu-id="27615-106">Symptom</span></span>

<span data-ttu-id="27615-107">Hallo na de problemen bij het uitvoeren van virtuele Linux-machines in Microsoft Azure kunnen optreden.</span><span class="sxs-lookup"><span data-stu-id="27615-107">You may experience hello following problems when running Linux VMs in Microsoft Azure.</span></span>

- <span data-ttu-id="27615-108">Hallo VM mislukt tooboot na het opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="27615-108">hello VM fails tooboot after a restart.</span></span>

- <span data-ttu-id="27615-109">Als gegevensschijven worden ontkoppeld en gekoppeld, worden Hallo apparaten namen voor schijven gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="27615-109">If data disks are detached and reattached, hello devices names for disks are changed.</span></span>

- <span data-ttu-id="27615-110">Een toepassing of het script dat verwijst naar een schijf met behulp van de apparaatnaam is mislukt.</span><span class="sxs-lookup"><span data-stu-id="27615-110">An application or script that references a disk by using device name fails.</span></span> <span data-ttu-id="27615-111">U vindt dat Hallo apparaatnaam van de schijf hello wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="27615-111">You find that hello device name of hello disk is changed.</span></span>

## <a name="cause"></a><span data-ttu-id="27615-112">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="27615-112">Cause</span></span>

<span data-ttu-id="27615-113">Apparaatpaden in Linux zijn niet gegarandeerd toobe consistent via opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="27615-113">Device paths in Linux are not guaranteed toobe consistent across restarts.</span></span> <span data-ttu-id="27615-114">Apparaatnamen bestaan uit (letter) primaire en secundaire cijfers.</span><span class="sxs-lookup"><span data-stu-id="27615-114">Device names consist of major (letter) and minor numbers.</span></span>  <span data-ttu-id="27615-115">Wanneer Hallo Linux opslag apparaatstuurprogramma een nieuw apparaat detecteert, wordt er primaire en secundaire apparaat cijfers tooit toegewezen uit Hallo beschikbaar bereik.</span><span class="sxs-lookup"><span data-stu-id="27615-115">When hello Linux storage device driver detects a new device, it assigns major and minor device numbers tooit from hello available range.</span></span> <span data-ttu-id="27615-116">Wanneer een apparaat wordt verwijderd, zijn Hallo apparaat cijfers vrijgegeven toobe later opnieuw worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="27615-116">When a device is removed, hello device numbers are freed toobe reused later.</span></span>

<span data-ttu-id="27615-117">Hallo probleem doet zich voor omdat hello apparaat scannen in Linux gepland door de SCSI-subsysteem Hallo asynchroon verloopt.</span><span class="sxs-lookup"><span data-stu-id="27615-117">hello problem occurs because hello device scanning in Linux scheduled by hello SCSI subsystem happens asynchronously.</span></span> <span data-ttu-id="27615-118">Hallo laatste apparaat pad naming varieert opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="27615-118">hello final device path naming may vary across restarts.</span></span> 

## <a name="solution"></a><span data-ttu-id="27615-119">Oplossing</span><span class="sxs-lookup"><span data-stu-id="27615-119">Solution</span></span>

<span data-ttu-id="27615-120">tooresolve dit probleem op door permanente naming gebruiken.</span><span class="sxs-lookup"><span data-stu-id="27615-120">tooresolve this problem, use persistent naming.</span></span> <span data-ttu-id="27615-121">Er zijn vier methoden toopersistent naming - bestandssysteem labels, door uuid, -id en pad.</span><span class="sxs-lookup"><span data-stu-id="27615-121">There are four methods toopersistent naming - by filesystem label, by uuid, by id and by path.</span></span> <span data-ttu-id="27615-122">Aangeraden Hallo bestandssysteem label en UUID methoden voor Azure Linux VM's.</span><span class="sxs-lookup"><span data-stu-id="27615-122">We recommend hello filesystem label and UUID methods for Azure Linux VMs.</span></span> 

<span data-ttu-id="27615-123">De meeste distributies bieden ook beide Hallo **nofail** of **nobootwait** fstab-opties.</span><span class="sxs-lookup"><span data-stu-id="27615-123">Most distributions also provide either hello **nofail** or **nobootwait** fstab options.</span></span> <span data-ttu-id="27615-124">Deze opties inschakelen een tooboot systeem, zelfs als Hallo schijf toomount bij het opstarten is mislukt.</span><span class="sxs-lookup"><span data-stu-id="27615-124">These options enable a system tooboot even if hello disk fails toomount at startup.</span></span> <span data-ttu-id="27615-125">Raadpleeg de documentatie van het distributiepunt Hallo voor meer informatie over deze parameters.</span><span class="sxs-lookup"><span data-stu-id="27615-125">Check hello distribution's documentation for more information about these parameters.</span></span> <span data-ttu-id="27615-126">Voor meer informatie over hoe tooconfigure een Linux-VM toouse een UUID wanneer u een gegevensschijf toevoegen zien [toohello Linux VM toomount Hallo nieuwe schijf verbinding](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="27615-126">For more information about how tooconfigure a Linux VM toouse a UUID when you add a data disk, see [Connect toohello Linux VM toomount hello new disk](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> 

<span data-ttu-id="27615-127">Wanneer hello Azure Linux agent is geïnstalleerd op een virtuele machine, gebruikt het Udev regels tooconstruct een set van symbolische koppelingen onder **/dev/disk/azure**.</span><span class="sxs-lookup"><span data-stu-id="27615-127">When hello Azure Linux agent is installed on a VM, it uses Udev rules tooconstruct a set of symbolic links under **/dev/disk/azure**.</span></span> <span data-ttu-id="27615-128">Deze Udev-regels kunnen worden gebruikt door toepassingen en scripts tooidentify schijven zijn aangesloten toohello VM, het type en Hallo LUN.</span><span class="sxs-lookup"><span data-stu-id="27615-128">These Udev rules can be used by applications and scripts tooidentify disks are attached toohello VM, their type, and hello LUN.</span></span>

## <a name="more-information"></a><span data-ttu-id="27615-129">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="27615-129">More information</span></span>

### <a name="identify-disk-luns"></a><span data-ttu-id="27615-130">Schijf-LUN's identificeren</span><span class="sxs-lookup"><span data-stu-id="27615-130">Identify disk LUNs</span></span>

<span data-ttu-id="27615-131">Een toepassing kunt LUN's toofind alle Hallo gekoppelde schijven en maken symbolische koppelingen.</span><span class="sxs-lookup"><span data-stu-id="27615-131">An application can use LUNs toofind all hello attached disks and constructing symbolic links.</span></span> <span data-ttu-id="27615-132">Hello Azure Linux agent bevat nu udev-regels die symbolische koppelingen vanaf een LUN toohello apparaten, als volgt instellen:</span><span class="sxs-lookup"><span data-stu-id="27615-132">hello Azure Linux agent now includes udev rules that set up symbolic links from a LUN toohello devices, as follows:</span></span>

    $ tree /dev/disk/azure

    /dev/disk/azure
    ├── resource -> ../../sdb
    ├── resource-part1 -> ../../sdb1
    ├── root -> ../../sda
    ├── root-part1 -> ../../sda1
    └── scsi1
        ├── lun0 -> ../../../sdc
        ├── lun0-part1 -> ../../../sdc1
        ├── lun1 -> ../../../sdd
        ├── lun1-part1 -> ../../../sdd1
        ├── lun1-part2 -> ../../../sdd2
        └── lun1-part3 -> ../../../sdd3                                    
                                 

<span data-ttu-id="27615-133">LUN-gegevens kan ook worden opgehaald van Hallo Linux Gast met lsscsi of vergelijkbare hulpprogramma als volgt.</span><span class="sxs-lookup"><span data-stu-id="27615-133">LUN information can also be retrieved from hello Linux guest using lsscsi or similar tool as follows.</span></span>

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

<span data-ttu-id="27615-134">Deze Gast LUN-informatie kan worden gebruikt met Azure-abonnement metagegevens tooidentify Hallo locatie in Azure-opslag Hallo VHD die Hallo partitiegegevens opslaat.</span><span class="sxs-lookup"><span data-stu-id="27615-134">This guest LUN information can be used with Azure subscription metadata tooidentify hello location in Azure storage of hello VHD which stores hello partition data.</span></span> <span data-ttu-id="27615-135">Gebruik bijvoorbeeld Hallo az cli:</span><span class="sxs-lookup"><span data-stu-id="27615-135">For example, use hello az cli:</span></span>

    $ az vm show --resource-group testVM --name testVM | jq -r .storageProfile.dataDisks                                        
    [                                                                                                                                                                  
    {                                                                                                                                                                  
    "caching": "None",                                                                                                                                              
      "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 1023,                                                                                                                                             
      "image": null,                                                                                                                                                   
    "lun": 0,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-114353",                                                                                                                    
    "vhd": {                                                                                                                                                          
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-114353.vhd"                                                       
    }                                                                                                                                                              
    },                                                                                                                                                                
    {                                                                                                                                                                   
    "caching": "None",                                                                                                                                               
    "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 512,                                                                                                                                              
    "image": null,                                                                                                                                                   
    "lun": 1,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-121516",                                                                                                                    
    "vhd": {                                                                                                                                                           
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-121516.vhd"                                                       
      }                                                                                                                                                             
      }                                                                                                                                                             
    ]

### <a name="discover-filesystem-uuids-by-using-blkid"></a><span data-ttu-id="27615-136">Bestandssysteem UUID's detecteren met behulp van blkid</span><span class="sxs-lookup"><span data-stu-id="27615-136">Discover filesystem UUIDs by using blkid</span></span>

<span data-ttu-id="27615-137">Een script of toepassing kan lezen Hallo-uitvoer van blkid of vergelijkbare bronnen met informatie en opstelt symbolische koppelingen in **/dev** voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="27615-137">A script or application can read hello output of blkid, or similar sources of information, and construct symbolic links in **/dev** for use.</span></span> <span data-ttu-id="27615-138">Hallo-uitvoer wordt weergegeven Hallo UUID's van alle schijven die zijn gekoppeld toohello VM en Hallo apparaat bestand toowhich zijn gekoppeld:</span><span class="sxs-lookup"><span data-stu-id="27615-138">hello output will show hello UUIDs of all disks attached toohello VM and hello device file toowhich they are associated:</span></span>

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

<span data-ttu-id="27615-139">Hallo waagent udev regels maken een reeks symbolische koppelingen onder **/dev/disk/azure**:</span><span class="sxs-lookup"><span data-stu-id="27615-139">hello waagent udev rules construct a set of symbolic links under **/dev/disk/azure**:</span></span>


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


<span data-ttu-id="27615-140">Hallo-toepassing kan deze informatie gebruiken Hallo schijf opstartapparaat en Hallo resource (tijdelijke) schijf identificeren.</span><span class="sxs-lookup"><span data-stu-id="27615-140">hello application can use this information identify hello boot disk device and hello resource (ephemeral) disk.</span></span> <span data-ttu-id="27615-141">In Azure, toepassingen te raadplegen**/dev/disk/azure/root-part1** of **/dev/disk/azure-resource-part1** toodiscover deze partities.</span><span class="sxs-lookup"><span data-stu-id="27615-141">In Azure, applications should refer too**/dev/disk/azure/root-part1** or **/dev/disk/azure-resource-part1** toodiscover these partitions.</span></span>

<span data-ttu-id="27615-142">Als er aanvullende partities uit Hallo blkid lijst, wordt deze op een gegevensschijf staan.</span><span class="sxs-lookup"><span data-stu-id="27615-142">If there are additional partitions from hello blkid list, they reside on a data disk.</span></span> <span data-ttu-id="27615-143">Toepassingen kunnen onderhouden Hallo UUID voor deze partities en een pad zoals Hallo hieronder toodiscover Hallo apparaatnaam in runtime te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="27615-143">Applications can maintain hello UUID for these partitions and use a path like hello below toodiscover hello device name at runtime:</span></span>

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a><span data-ttu-id="27615-144">Hallo nieuwste Azure-opslag-regels ophalen</span><span class="sxs-lookup"><span data-stu-id="27615-144">Get hello latest Azure storage rules</span></span>

<span data-ttu-id="27615-145">meest recente Azure storage-regels toohello, voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="27615-145">toohello latest Azure storage rules, run th following commands:</span></span>

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


<span data-ttu-id="27615-146">Zie voor meer informatie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="27615-146">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="27615-147">Ubuntu: Met behulp van UUID</span><span class="sxs-lookup"><span data-stu-id="27615-147">Ubuntu: Using UUID</span></span>](https://help.ubuntu.com/community/UsingUUID)

- [<span data-ttu-id="27615-148">Red Hat: Permanente Naming</span><span class="sxs-lookup"><span data-stu-id="27615-148">Red Hat: Persistent Naming</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)

- [<span data-ttu-id="27615-149">Linux: Wat UUID's voor u kunnen doen</span><span class="sxs-lookup"><span data-stu-id="27615-149">Linux: What UUIDs can do for you</span></span>](https://www.linux.com/news/what-uuids-can-do-you)

- [<span data-ttu-id="27615-150">Udev: Inleiding tooDevice In moderne Linux beheersysteem</span><span class="sxs-lookup"><span data-stu-id="27615-150">Udev: Introduction tooDevice Management In Modern Linux System</span></span>](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

