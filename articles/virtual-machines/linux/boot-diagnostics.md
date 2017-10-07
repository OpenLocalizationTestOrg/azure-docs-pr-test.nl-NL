---
title: aaaBoot diagnostische gegevens van Linux virtuele machines in Azure | Microsoft-document
description: Overzicht van Hallo twee foutopsporing functies voor virtuele Linux-machines in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: Deland-Han
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: delhan
ms.openlocfilehash: d355d512de09d2f1d7a2718e3db3fb99c9dd9e24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-boot-diagnostics-tootroubleshoot-linux-virtual-machines-in-azure"></a>Hoe toouse diagnostics tootroubleshoot Linux virtuele machines in Azure worden opgestart

Ondersteuning voor twee foutopsporingsfuncties is nu beschikbaar in Azure: ondersteuning voor Console-uitvoer en Schermafbeelding voor het Azure Virtual Machines Resource Manager-implementatiemodel. 

Wanneer u uw eigen installatiekopie tooAzure of zelfs opstarten een van de installatiekopieën van het platform hello te brengen, kunnen er diverse redenen waarom een virtuele Machine in een niet-opstartbare status opgehaald. Met deze functies kunt u tooeasily diagnosticeren en op uw virtuele Machines herstellen.

Voor virtuele Linux-Machines, kunt u eenvoudig hello uitvoer van uw consolelogboek van Hallo Portal bekijken:

![Azure Portal](./media/boot-diagnostics/screenshot1.png)
 
Echter voor Windows en Linux virtuele Machines kunt Azure ook u een schermopname van Hallo VM van de hypervisor Hallo toosee:

![Fout](./media/boot-diagnostics/screenshot2.png)

Beide functies worden ondersteund voor virtuele Azure-machines in alle regio's. Opmerking: de schermafbeeldingen en de uitvoer kunnen duren too10 minuten tooappear in uw opslagaccount.

## <a name="common-boot-errors"></a>Veelvoorkomende opstartfouten

- [Bestandssystemen](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [Kernel-problemen](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [FSTAB-fouten](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a>Diagnostische gegevens op een nieuwe virtuele machine inschakelen
1. Wanneer u een nieuwe virtuele Machine maakt van Hallo Preview-Portal, selecteer Hallo **Azure Resource Manager** uit Hallo deployment model vervolgkeuzelijst:
 
    ![Resource Manager](./media/boot-diagnostics/screenshot3.jpg)

2. Hallo bewaking optie tooselect Hallo storage-account waarin u tooplace wilt dat deze diagnostische bestanden configureren.
 
    ![VM maken](./media/boot-diagnostics/screenshot4.jpg)

3. Als u met een Azure Resource Manager-sjabloon implementeert, virtuele-machinebron tooyour navigeren en Hallo diagnostische profielsectie toevoegen. Houd er rekening mee toouse Hallo '2015-06-15' API-versie-header.

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. Hallo diagnostische profiel kunt u tooselect Hallo storage-account waar u tooput deze logboeken.

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

## <a name="update-an-existing-virtual-machine"></a>Een bestaande virtuele machine bijwerken

tooenable diagnostische gegevens over opstarten via de portal hello, kunt u ook een bestaande virtuele machine via de portal Hallo bijwerken. Selecteer Hallo Boot Diagnostics optie en opslaan. Opnieuw opstarten Hallo VM tootake effect.

![Bestaande VM bijwerken](./media/boot-diagnostics/screenshot5.png)