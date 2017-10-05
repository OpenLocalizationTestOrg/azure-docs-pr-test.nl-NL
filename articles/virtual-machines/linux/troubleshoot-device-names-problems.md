---
title: Linux-VM apparaatnamen zijn gewijzigd in Azure | Microsoft Docs
description: De reden waarom uitgelegd apparaatnamen worden gewijzigd en bieden oplossing voor dit probleem.
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
ms.openlocfilehash: 789f4580901a22dc3aaae9599c7205c76f268403
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a><span data-ttu-id="9195c-103">Voor probleemoplossing: Apparaatnamen Linux VM zijn gewijzigd</span><span class="sxs-lookup"><span data-stu-id="9195c-103">Troubleshooting: Linux VM device names are changed</span></span>

<span data-ttu-id="9195c-104">Het artikel wordt uitgelegd waarom apparaatnamen zijn gewijzigd nadat u een Linux-virtuele machine (VM) opnieuw opstarten of de schijven opnieuw koppelen.</span><span class="sxs-lookup"><span data-stu-id="9195c-104">The article explains why device names are changed after you restart a Linux virtual machine (VM), or reattach the disks.</span></span> <span data-ttu-id="9195c-105">Het bevat ook de oplossing voor dit probleem.</span><span class="sxs-lookup"><span data-stu-id="9195c-105">It also provides the solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="9195c-106">Symptoom</span><span class="sxs-lookup"><span data-stu-id="9195c-106">Symptom</span></span>

<span data-ttu-id="9195c-107">U ondervinden de volgende problemen bij het uitvoeren van virtuele Linux-machines in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9195c-107">You may experience the following problems when running Linux VMs in Microsoft Azure.</span></span>

- <span data-ttu-id="9195c-108">De virtuele machine kan niet worden opgestart na het opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="9195c-108">The VM fails to boot after a restart.</span></span>

- <span data-ttu-id="9195c-109">Als gegevensschijven worden ontkoppeld en gekoppeld, worden de namen van de apparaten voor schijven gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="9195c-109">If data disks are detached and reattached, the devices names for disks are changed.</span></span>

- <span data-ttu-id="9195c-110">Een toepassing of het script dat verwijst naar een schijf met behulp van de apparaatnaam is mislukt.</span><span class="sxs-lookup"><span data-stu-id="9195c-110">An application or script that references a disk by using device name fails.</span></span> <span data-ttu-id="9195c-111">U vindt dat de naam van het apparaat van de schijf is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="9195c-111">You find that the device name of the disk is changed.</span></span>

## <a name="cause"></a><span data-ttu-id="9195c-112">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="9195c-112">Cause</span></span>

<span data-ttu-id="9195c-113">Apparaatpaden in Linux zijn niet gegarandeerd zijn consistent via opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="9195c-113">Device paths in Linux are not guaranteed to be consistent across restarts.</span></span> <span data-ttu-id="9195c-114">Apparaatnamen bestaan uit (letter) primaire en secundaire cijfers.</span><span class="sxs-lookup"><span data-stu-id="9195c-114">Device names consist of major (letter) and minor numbers.</span></span>  <span data-ttu-id="9195c-115">Als het stuurprogramma voor Linux opslag een nieuw apparaat detecteert, wijst die uit de beschikbare bereik de primaire en secundaire apparaat getallen toe aan het.</span><span class="sxs-lookup"><span data-stu-id="9195c-115">When the Linux storage device driver detects a new device, it assigns major and minor device numbers to it from the available range.</span></span> <span data-ttu-id="9195c-116">Wanneer een apparaat wordt verwijderd, worden de cijfers van het apparaat vrijgemaakt voor het later opnieuw worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9195c-116">When a device is removed, the device numbers are freed to be reused later.</span></span>

<span data-ttu-id="9195c-117">Het probleem doet zich voor omdat het apparaat scannen in Linux gepland door de SCSI-subsysteem asynchroon gebeurt.</span><span class="sxs-lookup"><span data-stu-id="9195c-117">The problem occurs because the device scanning in Linux scheduled by the SCSI subsystem happens asynchronously.</span></span> <span data-ttu-id="9195c-118">De laatste apparaat pad naamgeving varieert opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="9195c-118">The final device path naming may vary across restarts.</span></span> 

## <a name="solution"></a><span data-ttu-id="9195c-119">Oplossing</span><span class="sxs-lookup"><span data-stu-id="9195c-119">Solution</span></span>

<span data-ttu-id="9195c-120">U lost dit probleem, gebruik permanente naming.</span><span class="sxs-lookup"><span data-stu-id="9195c-120">To resolve this problem, use persistent naming.</span></span> <span data-ttu-id="9195c-121">Er zijn vier methoden aan de naamgeving van permanente - bestandssysteem labels, door uuid-id en naar met het pad.</span><span class="sxs-lookup"><span data-stu-id="9195c-121">There are four methods to persistent naming - by filesystem label, by uuid, by id and by path.</span></span> <span data-ttu-id="9195c-122">Het bestandssysteem label en UUID methoden u beter voor Azure Linux VM's.</span><span class="sxs-lookup"><span data-stu-id="9195c-122">We recommend the filesystem label and UUID methods for Azure Linux VMs.</span></span> 

<span data-ttu-id="9195c-123">De meeste distributies Geef ofwel de **nofail** of **nobootwait** fstab-opties.</span><span class="sxs-lookup"><span data-stu-id="9195c-123">Most distributions also provide either the **nofail** or **nobootwait** fstab options.</span></span> <span data-ttu-id="9195c-124">Deze opties kunt een systeem op te starten, zelfs als de schijf niet koppelen bij het opstarten.</span><span class="sxs-lookup"><span data-stu-id="9195c-124">These options enable a system to boot even if the disk fails to mount at startup.</span></span> <span data-ttu-id="9195c-125">Raadpleeg de distributie-documentatie voor meer informatie over deze parameters.</span><span class="sxs-lookup"><span data-stu-id="9195c-125">Check the distribution's documentation for more information about these parameters.</span></span> <span data-ttu-id="9195c-126">Zie voor meer informatie over het configureren van een Linux-VM voor het gebruik van een UUID wanneer u een gegevensschijf toevoegen [verbinding maken met de Linux-VM te koppelen van de nieuwe schijf](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="9195c-126">For more information about how to configure a Linux VM to use a UUID when you add a data disk, see [Connect to the Linux VM to mount the new disk](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> 

<span data-ttu-id="9195c-127">Wanneer de Azure Linux-agent is geïnstalleerd op een virtuele machine, Udev-regels worden gebruikt om samen te stellen van een set van symbolische koppelingen onder **/dev/disk/azure**.</span><span class="sxs-lookup"><span data-stu-id="9195c-127">When the Azure Linux agent is installed on a VM, it uses Udev rules to construct a set of symbolic links under **/dev/disk/azure**.</span></span> <span data-ttu-id="9195c-128">Deze Udev-regels kunnen worden gebruikt door toepassingen en scripts voor het identificeren van schijven zijn gekoppeld aan de virtuele machine, het type en de LUN.</span><span class="sxs-lookup"><span data-stu-id="9195c-128">These Udev rules can be used by applications and scripts to identify disks are attached to the VM, their type, and the LUN.</span></span>

## <a name="more-information"></a><span data-ttu-id="9195c-129">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="9195c-129">More information</span></span>

### <a name="identify-disk-luns"></a><span data-ttu-id="9195c-130">Schijf-LUN's identificeren</span><span class="sxs-lookup"><span data-stu-id="9195c-130">Identify disk LUNs</span></span>

<span data-ttu-id="9195c-131">Een toepassing kunt LUN's gebruiken om de gekoppelde schijven en maken van de symbolische koppelingen zoeken.</span><span class="sxs-lookup"><span data-stu-id="9195c-131">An application can use LUNs to find all the attached disks and constructing symbolic links.</span></span> <span data-ttu-id="9195c-132">De Azure Linux-agent heeft nu udev-regels die symbolische koppelingen van een LUN voor de apparaten als volgt instellen:</span><span class="sxs-lookup"><span data-stu-id="9195c-132">The Azure Linux agent now includes udev rules that set up symbolic links from a LUN to the devices, as follows:</span></span>

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
                                 

<span data-ttu-id="9195c-133">LUN-gegevens kan ook worden opgehaald van de Linux Gast met lsscsi of vergelijkbare hulpprogramma als volgt.</span><span class="sxs-lookup"><span data-stu-id="9195c-133">LUN information can also be retrieved from the Linux guest using lsscsi or similar tool as follows.</span></span>

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

<span data-ttu-id="9195c-134">Deze Gast LUN-informatie kan worden gebruikt met Azure-abonnement metagegevens voor het identificeren van de locatie in Azure-opslag van de VHD die de partitiegegevens opslaat.</span><span class="sxs-lookup"><span data-stu-id="9195c-134">This guest LUN information can be used with Azure subscription metadata to identify the location in Azure storage of the VHD which stores the partition data.</span></span> <span data-ttu-id="9195c-135">Gebruik bijvoorbeeld de cli az:</span><span class="sxs-lookup"><span data-stu-id="9195c-135">For example, use the az cli:</span></span>

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

### <a name="discover-filesystem-uuids-by-using-blkid"></a><span data-ttu-id="9195c-136">Bestandssysteem UUID's detecteren met behulp van blkid</span><span class="sxs-lookup"><span data-stu-id="9195c-136">Discover filesystem UUIDs by using blkid</span></span>

<span data-ttu-id="9195c-137">Een script of toepassing kan de uitvoer van blkid of vergelijkbare bronnen met informatie lezen en opstelt symbolische koppelingen in **/dev** voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="9195c-137">A script or application can read the output of blkid, or similar sources of information, and construct symbolic links in **/dev** for use.</span></span> <span data-ttu-id="9195c-138">De uitvoer bevat de UUID's van alle schijven die zijn gekoppeld aan de virtuele machine en de apparaat-bestand waarop ze gekoppeld zijn:</span><span class="sxs-lookup"><span data-stu-id="9195c-138">The output will show the UUIDs of all disks attached to the VM and the device file to which they are associated:</span></span>

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

<span data-ttu-id="9195c-139">De waagent udev-regels maken een reeks symbolische koppelingen onder **/dev/disk/azure**:</span><span class="sxs-lookup"><span data-stu-id="9195c-139">The waagent udev rules construct a set of symbolic links under **/dev/disk/azure**:</span></span>


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


<span data-ttu-id="9195c-140">De toepassing kan deze informatie gebruiken het opstartapparaat schijf en de resource (tijdelijke)-schijf te identificeren.</span><span class="sxs-lookup"><span data-stu-id="9195c-140">The application can use this information identify the boot disk device and the resource (ephemeral) disk.</span></span> <span data-ttu-id="9195c-141">In Azure, toepassingen moeten verwijzen naar **/dev/disk/azure/root-part1** of **/dev/disk/azure-resource-part1** voor het detecteren van deze partities.</span><span class="sxs-lookup"><span data-stu-id="9195c-141">In Azure, applications should refer to **/dev/disk/azure/root-part1** or **/dev/disk/azure-resource-part1** to discover these partitions.</span></span>

<span data-ttu-id="9195c-142">Als er extra partities in de lijst blkid, wordt deze op een gegevensschijf staan.</span><span class="sxs-lookup"><span data-stu-id="9195c-142">If there are additional partitions from the blkid list, they reside on a data disk.</span></span> <span data-ttu-id="9195c-143">Toepassingen kunnen de UUID voor deze partities onderhouden en een pad zoals gebruiken de onderstaande voor het detecteren van de naam van het apparaat tijdens runtime:</span><span class="sxs-lookup"><span data-stu-id="9195c-143">Applications can maintain the UUID for these partitions and use a path like the below to discover the device name at runtime:</span></span>

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-the-latest-azure-storage-rules"></a><span data-ttu-id="9195c-144">De nieuwste Azure-opslag-regels ophalen</span><span class="sxs-lookup"><span data-stu-id="9195c-144">Get the latest Azure storage rules</span></span>

<span data-ttu-id="9195c-145">Voer de volgende opdrachten aan de nieuwste Azure-opslag-regels:</span><span class="sxs-lookup"><span data-stu-id="9195c-145">To the latest Azure storage rules, run th following commands:</span></span>

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


<span data-ttu-id="9195c-146">Raadpleeg voor meer informatie de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="9195c-146">For more information, see the following articles:</span></span>

- [<span data-ttu-id="9195c-147">Ubuntu: Met behulp van UUID</span><span class="sxs-lookup"><span data-stu-id="9195c-147">Ubuntu: Using UUID</span></span>](https://help.ubuntu.com/community/UsingUUID)

- [<span data-ttu-id="9195c-148">Red Hat: Permanente Naming</span><span class="sxs-lookup"><span data-stu-id="9195c-148">Red Hat: Persistent Naming</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)

- [<span data-ttu-id="9195c-149">Linux: Wat UUID's voor u kunnen doen</span><span class="sxs-lookup"><span data-stu-id="9195c-149">Linux: What UUIDs can do for you</span></span>](https://www.linux.com/news/what-uuids-can-do-you)

- [<span data-ttu-id="9195c-150">Udev: Inleiding tot beheer van apparaten In moderne Linux-systeem</span><span class="sxs-lookup"><span data-stu-id="9195c-150">Udev: Introduction to Device Management In Modern Linux System</span></span>](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

