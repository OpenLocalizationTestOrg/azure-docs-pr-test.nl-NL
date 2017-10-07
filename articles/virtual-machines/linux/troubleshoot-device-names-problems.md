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
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a>Voor probleemoplossing: Apparaatnamen Linux VM zijn gewijzigd

Hallo artikel wordt uitgelegd waarom apparaatnamen zijn gewijzigd nadat u een Linux-virtuele machine (VM) opnieuw opstarten of opnieuw Hallo-schijven koppelen. Ook biedt het Hallo-oplossing voor dit probleem.

## <a name="symptom"></a>Symptoom

Hallo na de problemen bij het uitvoeren van virtuele Linux-machines in Microsoft Azure kunnen optreden.

- Hallo VM mislukt tooboot na het opnieuw opstarten.

- Als gegevensschijven worden ontkoppeld en gekoppeld, worden Hallo apparaten namen voor schijven gewijzigd.

- Een toepassing of het script dat verwijst naar een schijf met behulp van de apparaatnaam is mislukt. U vindt dat Hallo apparaatnaam van de schijf hello wordt gewijzigd.

## <a name="cause"></a>Oorzaak

Apparaatpaden in Linux zijn niet gegarandeerd toobe consistent via opnieuw wordt opgestart. Apparaatnamen bestaan uit (letter) primaire en secundaire cijfers.  Wanneer Hallo Linux opslag apparaatstuurprogramma een nieuw apparaat detecteert, wordt er primaire en secundaire apparaat cijfers tooit toegewezen uit Hallo beschikbaar bereik. Wanneer een apparaat wordt verwijderd, zijn Hallo apparaat cijfers vrijgegeven toobe later opnieuw worden gebruikt.

Hallo probleem doet zich voor omdat hello apparaat scannen in Linux gepland door de SCSI-subsysteem Hallo asynchroon verloopt. Hallo laatste apparaat pad naming varieert opnieuw wordt opgestart. 

## <a name="solution"></a>Oplossing

tooresolve dit probleem op door permanente naming gebruiken. Er zijn vier methoden toopersistent naming - bestandssysteem labels, door uuid, -id en pad. Aangeraden Hallo bestandssysteem label en UUID methoden voor Azure Linux VM's. 

De meeste distributies bieden ook beide Hallo **nofail** of **nobootwait** fstab-opties. Deze opties inschakelen een tooboot systeem, zelfs als Hallo schijf toomount bij het opstarten is mislukt. Raadpleeg de documentatie van het distributiepunt Hallo voor meer informatie over deze parameters. Voor meer informatie over hoe tooconfigure een Linux-VM toouse een UUID wanneer u een gegevensschijf toevoegen zien [toohello Linux VM toomount Hallo nieuwe schijf verbinding](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk). 

Wanneer hello Azure Linux agent is geïnstalleerd op een virtuele machine, gebruikt het Udev regels tooconstruct een set van symbolische koppelingen onder **/dev/disk/azure**. Deze Udev-regels kunnen worden gebruikt door toepassingen en scripts tooidentify schijven zijn aangesloten toohello VM, het type en Hallo LUN.

## <a name="more-information"></a>Meer informatie

### <a name="identify-disk-luns"></a>Schijf-LUN's identificeren

Een toepassing kunt LUN's toofind alle Hallo gekoppelde schijven en maken symbolische koppelingen. Hello Azure Linux agent bevat nu udev-regels die symbolische koppelingen vanaf een LUN toohello apparaten, als volgt instellen:

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
                                 

LUN-gegevens kan ook worden opgehaald van Hallo Linux Gast met lsscsi of vergelijkbare hulpprogramma als volgt.

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

Deze Gast LUN-informatie kan worden gebruikt met Azure-abonnement metagegevens tooidentify Hallo locatie in Azure-opslag Hallo VHD die Hallo partitiegegevens opslaat. Gebruik bijvoorbeeld Hallo az cli:

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

### <a name="discover-filesystem-uuids-by-using-blkid"></a>Bestandssysteem UUID's detecteren met behulp van blkid

Een script of toepassing kan lezen Hallo-uitvoer van blkid of vergelijkbare bronnen met informatie en opstelt symbolische koppelingen in **/dev** voor gebruik. Hallo-uitvoer wordt weergegeven Hallo UUID's van alle schijven die zijn gekoppeld toohello VM en Hallo apparaat bestand toowhich zijn gekoppeld:

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

Hallo waagent udev regels maken een reeks symbolische koppelingen onder **/dev/disk/azure**:


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


Hallo-toepassing kan deze informatie gebruiken Hallo schijf opstartapparaat en Hallo resource (tijdelijke) schijf identificeren. In Azure, toepassingen te raadplegen**/dev/disk/azure/root-part1** of **/dev/disk/azure-resource-part1** toodiscover deze partities.

Als er aanvullende partities uit Hallo blkid lijst, wordt deze op een gegevensschijf staan. Toepassingen kunnen onderhouden Hallo UUID voor deze partities en een pad zoals Hallo hieronder toodiscover Hallo apparaatnaam in runtime te gebruiken:

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a>Hallo nieuwste Azure-opslag-regels ophalen

meest recente Azure storage-regels toohello, voer de volgende opdrachten:

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


Zie voor meer informatie Hallo artikelen te volgen:

- [Ubuntu: Met behulp van UUID](https://help.ubuntu.com/community/UsingUUID)

- [Red Hat: Permanente Naming](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)

- [Linux: Wat UUID's voor u kunnen doen](https://www.linux.com/news/what-uuids-can-do-you)

- [Udev: Inleiding tooDevice In moderne Linux beheersysteem](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

