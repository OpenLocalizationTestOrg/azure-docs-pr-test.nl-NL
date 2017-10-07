---
title: aaaTroubleshooting Windows VM-extensie fouten | Microsoft Docs
description: Meer informatie over het oplossen van fouten voor virtuele machine van Windows Azure-extensie
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: 878ab9b6-c3e6-40be-82d4-d77fecd5030f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: d24544743d9e0cb1a68ec9ab7718716f918054f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a>Virtuele machine van Windows Azure-extensie fouten oplossen
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>De Extensiestatus van weergeven
Azure Resource Manager-sjablonen kunnen in Azure PowerShell worden uitgevoerd. Zodra het Hallo-sjabloon wordt uitgevoerd, kan status van de extensie Hallo van Azure Resource Explorer of Hallo opdrachtregel-hulpprogramma's worden weergegeven.

Hier volgt een voorbeeld:

Azure PowerShell:

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

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

## <a name="troubleshooting-extension-failures"></a>Het extensie-fouten oplossen
### <a name="re-running-hello-extension-on-hello-vm"></a>Hallo-uitbreiding opnieuw uit te voeren op Hallo VM
Als u scripts op Hallo VM die gebruikmaakt van de aangepaste Scriptextensie uitvoert, kunt u soms uitvoeren in een fout waarbij VM is gemaakt maar Hallo-script is mislukt. Onder deze voorwaarden Hallo aanbevolen manier toorecover van deze fout is tooremove Hallo uitbreiding en voert u Hallo sjabloon opnieuw.
Opmerking: In de toekomst wordt deze functionaliteit zou worden uitgebreide tooremove nodig voor het verwijderen van extensie Hallo Hallo.

#### <a name="remove-hello-extension-from-azure-powershell"></a>Hallo-uitbreiding uit Azure PowerShell verwijderen
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

Zodra het Hallo-extensie is verwijderd, kan Hallo sjabloon opnieuw uitgevoerd toorun Hallo scripts op Hallo VM zijn.

