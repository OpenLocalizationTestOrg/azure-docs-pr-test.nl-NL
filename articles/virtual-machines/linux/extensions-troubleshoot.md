---
title: aaaTroubleshooting Linux VM extensie fouten | Microsoft Docs
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
ms.openlocfilehash: 29a0ca34207421e0014380000a313d3c44e7e594
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a>Azure Linux VM-extensie fouten oplossen
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>De Extensiestatus van weergeven
Azure Resource Manager-sjablonen worden uitgevoerd vanaf hello Azure CLI. Zodra het Hallo-sjabloon wordt uitgevoerd, kan status van de extensie Hallo van Azure Resource Explorer of Hallo opdrachtregel-hulpprogramma's worden weergegeven.

Hier volgt een voorbeeld:

Azure CLI:

      azure vm get-instance-view


Hier volgt voorbeelduitvoer Hallo:

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
### <a name="re-running-hello-extension-on-hello-vm"></a>Hallo-uitbreiding opnieuw uit te voeren op Hallo VM
Als u scripts op Hallo VM die gebruikmaakt van de aangepaste Scriptextensie uitvoert, kunt u soms uitvoeren in een fout waarbij VM is gemaakt maar Hallo-script is mislukt. Onder deze voorwaarden Hallo aanbevolen manier toorecover van deze fout is tooremove Hallo uitbreiding en voert u Hallo sjabloon opnieuw.
Opmerking: In de toekomst wordt deze functionaliteit zou worden uitgebreide tooremove nodig voor het verwijderen van extensie Hallo Hallo.

#### <a name="remove-hello-extension-from-azure-cli"></a>Hallo-uitbreiding uit Azure CLI verwijderen
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

Waarbij 'publsher-name' komt overeen toohello extensietype van Hallo-uitvoer van 'get-exemplaar-weergave van de azure vm' en is de naam Hallo van Hallo extensie resource van Hallo-sjabloon

Zodra het Hallo-extensie is verwijderd, kan Hallo sjabloon opnieuw uitgevoerd toorun Hallo scripts op Hallo VM zijn.

