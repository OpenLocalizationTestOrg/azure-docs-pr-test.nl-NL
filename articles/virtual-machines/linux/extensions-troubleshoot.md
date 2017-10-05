---
title: Problemen met Linux VM-extensie oplost | Microsoft Docs
description: Meer informatie over het oplossen van fouten van Azure Linux VM-extensie
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: f05d93f3-42fc-4a09-9798-d92f7929c417
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 589890de379d0b729de1f1ba9e604e0ec0496f50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a>Azure Linux VM-extensie fouten oplossen
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>De Extensiestatus van weergeven
Azure Resource Manager-sjablonen worden uitgevoerd vanaf de Azure CLI. Nadat de sjabloon die wordt uitgevoerd, kan de status van de extensie van Azure Resource Explorer of de opdrachtregel-hulpprogramma's worden weergegeven.

Hier volgt een voorbeeld:

Azure CLI:

      azure vm get-instance-view


Hier volgt een voorbeeld van uitvoer:

      Extensions:  {
      "ExtensionType": "Microsoft.Compute.CustomScriptExtension",
      "Name": "myCustomScriptExtension",
      "SubStatuses": [
        {
          "Code": "ComponentStatus/StdOut/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "    Directory: C:\\temp\\n\\n\\nMode                LastWriteTime     Length Name
              \\n----                -------------     ------ ----                              \\n-a---          9/1/2015   2:03 AM         11
              test.txt                          \\n\\n",
                      "Time": null
          },
        {
          "Code": "ComponentStatus/StdErr/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "",
          "Time": null
        }
    }
  ]

## <a name="troubleshooting-extenson-failures"></a>Voor probleemoplossing Extenson fouten:
### <a name="re-running-the-extension-on-the-vm"></a>De uitbreiding opnieuw uit te voeren op de virtuele machine
Als u scripts op de virtuele machine met behulp van de aangepaste Scriptextensie, kan het soms uitvoeren in een fout waarbij VM is gemaakt, maar het script is mislukt. Onder deze voorwaarden is de aanbevolen manier om deze fout herstellen voor het verwijderen van de extensie en voert u de sjabloon opnieuw.
Opmerking: In de toekomst deze functionaliteit zou worden uitgebreid om te verwijderen van de noodzaak voor het verwijderen van de extensie.

#### <a name="remove-the-extension-from-azure-cli"></a>Verwijder de extensie van Azure CLI
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

Waarbij 'publsher-name' komt overeen met het uitbreidingstype uit de uitvoer van 'get-exemplaar-weergave van de azure vm' en is de naam van de bron van de uitbreiding van de sjabloon

Wanneer de uitbreiding is verwijderd, is de sjabloon kan worden opnieuw uitgevoerd voor het uitvoeren van de scripts op de virtuele machine.

