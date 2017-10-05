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
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a>Voor probleemoplossing: Apparaatnamen Linux VM zijn gewijzigd

Het artikel wordt uitgelegd waarom apparaatnamen zijn gewijzigd nadat u een Linux-virtuele machine (VM) opnieuw opstarten of de schijven opnieuw koppelen. Het bevat ook de oplossing voor dit probleem.

## <a name="symptom"></a>Symptoom

U ondervinden de volgende problemen bij het uitvoeren van virtuele Linux-machines in Microsoft Azure.

- De virtuele machine kan niet worden opgestart na het opnieuw opstarten.

- Als gegevensschijven worden ontkoppeld en gekoppeld, worden de namen van de apparaten voor schijven gewijzigd.

- Een toepassing of het script dat verwijst naar een schijf met behulp van de apparaatnaam is mislukt. U vindt dat de naam van het apparaat van de schijf is gewijzigd.

## <a name="cause"></a>Oorzaak

Apparaatpaden in Linux zijn niet gegarandeerd zijn consistent via opnieuw wordt opgestart. Apparaatnamen bestaan uit (letter) primaire en secundaire cijfers.  Als het stuurprogramma voor Linux opslag een nieuw apparaat detecteert, wijst die uit de beschikbare bereik de primaire en secundaire apparaat getallen toe aan het. Wanneer een apparaat wordt verwijderd, worden de cijfers van het apparaat vrijgemaakt voor het later opnieuw worden gebruikt.

Het probleem doet zich voor omdat het apparaat scannen in Linux gepland door de SCSI-subsysteem asynchroon gebeurt. De laatste apparaat pad naamgeving varieert opnieuw wordt opgestart. 

## <a name="solution"></a>Oplossing

U lost dit probleem, gebruik permanente naming. Er zijn vier methoden aan de naamgeving van permanente - bestandssysteem labels, door uuid-id en naar met het pad. Het bestandssysteem label en UUID methoden u beter voor Azure Linux VM's. 

De meeste distributies Geef ofwel de **nofail** of **nobootwait** fstab-opties. Deze opties kunt een systeem op te starten, zelfs als de schijf niet koppelen bij het opstarten. Raadpleeg de distributie-documentatie voor meer informatie over deze parameters. Zie voor meer informatie over het configureren van een Linux-VM voor het gebruik van een UUID wanneer u een gegevensschijf toevoegen [verbinding maken met de Linux-VM te koppelen van de nieuwe schijf](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk). 

Wanneer de Azure Linux-agent is geïnstalleerd op een virtuele machine, Udev-regels worden gebruikt om samen te stellen van een set van symbolische koppelingen onder **/dev/disk/azure**. Deze Udev-regels kunnen worden gebruikt door toepassingen en scripts voor het identificeren van schijven zijn gekoppeld aan de virtuele machine, het type en de LUN.

## <a name="more-information"></a>Meer informatie

### <a name="identify-disk-luns"></a>Schijf-LUN's identificeren

Een toepassing kunt LUN's gebruiken om de gekoppelde schijven en maken van de symbolische koppelingen zoeken. De Azure Linux-agent heeft nu udev-regels die symbolische koppelingen van een LUN voor de apparaten als volgt instellen:

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
                                 

LUN-gegevens kan ook worden opgehaald van de Linux Gast met lsscsi of vergelijkbare hulpprogramma als volgt.

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

Deze Gast LUN-informatie kan worden gebruikt met Azure-abonnement metagegevens voor het identificeren van de locatie in Azure-opslag van de VHD die de partitiegegevens opslaat. Gebruik bijvoorbeeld de cli az:

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

Een script of toepassing kan de uitvoer van blkid of vergelijkbare bronnen met informatie lezen en opstelt symbolische koppelingen in **/dev** voor gebruik. De uitvoer bevat de UUID's van alle schijven die zijn gekoppeld aan de virtuele machine en de apparaat-bestand waarop ze gekoppeld zijn:

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

De waagent udev-regels maken een reeks symbolische koppelingen onder **/dev/disk/azure**:


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


De toepassing kan deze informatie gebruiken het opstartapparaat schijf en de resource (tijdelijke)-schijf te identificeren. In Azure, toepassingen moeten verwijzen naar **/dev/disk/azure/root-part1** of **/dev/disk/azure-resource-part1** voor het detecteren van deze partities.

Als er extra partities in de lijst blkid, wordt deze op een gegevensschijf staan. Toepassingen kunnen de UUID voor deze partities onderhouden en een pad zoals gebruiken de onderstaande voor het detecteren van de naam van het apparaat tijdens runtime:

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-the-latest-azure-storage-rules"></a>De nieuwste Azure-opslag-regels ophalen

Voer de volgende opdrachten aan de nieuwste Azure-opslag-regels:

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


Raadpleeg voor meer informatie de volgende artikelen:

- [Ubuntu: Met behulp van UUID](https://help.ubuntu.com/community/UsingUUID)

- [Red Hat: Permanente Naming](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)

- [Linux: Wat UUID's voor u kunnen doen](https://www.linux.com/news/what-uuids-can-do-you)

- [Udev: Inleiding tot beheer van apparaten In moderne Linux-systeem](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

