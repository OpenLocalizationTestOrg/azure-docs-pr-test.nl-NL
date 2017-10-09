---
title: aaaAbout schijven en VHD's voor Microsoft Azure Linux VM's | Microsoft Docs
description: Meer informatie over de basisprincipes van Hallo van schijven en virtuele harde schijven voor virtuele Linux-machines in Azure.
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7be8dd52-98f7-4187-9b78-55197915bc9b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 862217e4f15ff8fd2e08de71386c4f367d0c39db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-linux-vms"></a>Over schijven en VHD's voor Azure Linux VM 's
Net als een andere computer gebruik virtuele machines in Azure schijven als een plaats toostore een besturingssysteem, toepassingen en gegevens. Alle virtuele machines in Azure hebt ten minste twee schijven: een Linux-besturingssysteem en een tijdelijke schijf. Hallo besturingssysteemschijf wordt gemaakt van een installatiekopie en besturingssysteemschijf Hallo zowel Hallo installatiekopie zijn daadwerkelijk opgeslagen virtuele harde schijven (VHD's) in Azure storage-account. Virtuele machines hebben ook een of meer gegevensschijven die ook als virtuele harde schijven zijn opgeslagen. 

In dit artikel wordt bespreken Hallo verschillende manieren worden gebruikt voor Hallo schijven, en vervolgens bespreken Hallo verschillende typen schijven kunt u maken en gebruiken. In dit artikel is ook beschikbaar voor [Windows virtuele machines](../windows/about-disks-and-vhds.md).

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>Schijven die worden gebruikt door virtuele machines

Eens kijken hoe Hallo schijven door Hallo VM's worden gebruikt.

## <a name="operating-system-disk"></a>Besturingssysteemschijf
Elke virtuele machine heeft een gekoppelde besturingssysteemschijf. Het geregistreerd als een SATA harde schijf en /dev/sda heet standaard. Deze schijf heeft een maximale capaciteit van 2048 gigabyte (GB). 

## <a name="temporary-disk"></a>Tijdelijke schijf
Elke virtuele machine bevat een tijdelijke schijf. Hallo tijdelijke schijf opslag op korte termijn voor toepassingen en processen en gegevens van de beoogde tooonly opslaan zoals pagina of het swap-bestanden is. Gegevens op de tijdelijke schijf Hallo zijn mogelijk verloren gegaan tijdens een [onderhoud](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) of wanneer u [opnieuw implementeren van een virtuele machine](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Tijdens een standaard herstart Hallo VM moet Hallo-gegevens op de tijdelijke schijf Hallo handhaven.

Op Linux virtuele machines, Hallo schijf wordt meestal **/dev/sdb** en is geformatteerd en gekoppeld, te**mnt** door hello Azure Linux Agent. Hallo-grootte van de tijdelijke schijf Hallo varieert, afhankelijk van de grootte van de Hallo van Hallo virtuele machine. Zie voor meer informatie [grootten voor virtuele Linux-machines](../windows/sizes.md).

Zie voor meer informatie over hoe Azure gebruikt voor de tijdelijke schijf Hallo [begrijpen Hallo tijdelijke station op Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="data-disk"></a>Gegevensschijf
Een gegevensschijf is een VHD die is aangesloten tooa virtuele machine toostore toepassingsgegevens of andere gegevens die u nodig hebt tookeep. Gegevensschijven worden geregistreerd als SCSI-stations en zijn gelabeld met een letter die u kiest. Elke gegevensschijf heeft een maximale capaciteit van 4095 GB. Hallo grootte van Hallo virtuele machine bepaalt hoeveel gegevensschijven kunt u tooit en Hallo type opslag kunt u koppelen toohost Hallo schijven.

> [!NOTE]
> Zie voor meer informatie over virtuele machines capaciteiten [grootten voor virtuele Linux-machines](../windows/sizes.md).
> 

Azure maakt een besturingssysteemschijf wanneer u een virtuele machine van een installatiekopie maakt. Als u een afbeelding met gegevensschijven, maakt Azure ook Hallo gegevensschijven bij het maken van Hallo virtuele machine. Anders toevoegen u gegevensschijven nadat u Hallo virtuele machine hebt gemaakt.

U kunt gegevens schijven tooa virtuele machine door op elk gewenst moment toevoegen **koppelen** Hallo schijf toohello virtuele machine. U kunt een VHD die u hebt geüpload of gekopieerd tooyour storage-account of een die Azure voor u gemaakt. Koppelen van een gegevensschijf koppelt Hallo VHD-bestand aan Hallo VM, door het plaatsen van een 'lease' op Hallo VHD zodat deze kan niet worden verwijderd uit de opslag terwijl er nog steeds gekoppeld.

[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="troubleshooting"></a>Problemen oplossen
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Volgende stappen
* [Een schijf koppelen](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooadd extra opslagruimte voor uw virtuele machine.
* [Configureren van software-RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor redundantie.
* [Linux-machine vastleggen](./classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) zodat u snel extra virtuele machines kunt implementeren.

