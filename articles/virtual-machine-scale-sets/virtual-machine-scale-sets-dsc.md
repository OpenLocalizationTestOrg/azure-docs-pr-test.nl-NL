---
title: aaaUsing gewenst status configuratie met virtuele-Machineschaalsets | Microsoft Docs
description: Met behulp van de virtuele-Machineschaalsets met hello Azure DSC-uitbreiding
services: virtual-machine-scale-sets
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: c8f047b5-0e6c-4ef3-8a47-f1b284d32942
ms.service: virtual-machine-scale-sets
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 04/05/2017
ms.author: zachal
ms.openlocfilehash: a35f1ca6700aa4889978032aa512882db50d6573
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-virtual-machine-scale-sets-with-hello-azure-dsc-extension"></a>Met behulp van de virtuele-Machineschaalsets met hello Azure DSC-uitbreiding
[Virtuele-Machineschaalsets](virtual-machine-scale-sets-overview.md) kan worden gebruikt met Hallo [Azure Desired State Configuration (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extensie-handler. Virtuele-machineschaalsets bieden een manier toodeploy en beheren van grote aantallen virtuele machines en in en uit in het antwoord tooload kunnen schalen. DSC is gebruikte tooconfigure Hallo VM's online komen zodat er Hallo productie software worden uitgevoerd.

## <a name="differences-between-deploying-toovirtual-machines-and-virtual-machine-scale-sets"></a>Verschillen tussen tooVirtual Machines en virtuele-Machineschaalsets implementeren
Hallo de onderliggende sjabloonstructuur voor een virtuele-machineschaalset enigszins afwijken van één VM is. Een enkele virtuele machine implementeert in het bijzonder extensies onder Hallo 'informatie' knooppunt. Er is een vermelding van het type "extensies" waar DSC toohello sjabloon is toegevoegd

```
"resources": [
          {
              "name": "Microsoft.Powershell.DSC",
              "type": "extensions",
              "location": "[resourceGroup().location]",
              "apiVersion": "2015-06-15",
              "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "tags": {
                  "displayName": "dscExtension"
              },
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": false,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "DscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }
          }
      ]
```

Een virtuele machine scale set knooppunt heeft een sectie 'Eigenschappen' Hello 'VirtualMachineProfile', 'extensionProfile'-kenmerk. DSC wordt toegevoegd onder 'extensies'

```
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": false,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
```

## <a name="behavior-for-a-virtual-machine-scale-set"></a>Gedrag voor een virtuele-Machineschaalset
Hallo-gedrag voor een virtuele-machineschaalset is identiek toohello gedrag voor één VM. Wanneer een nieuwe virtuele machine wordt gemaakt, wordt het automatisch ingericht met Hallo DSC-extensie. Als een nieuwere versie van WMF Hallo-uitbreiding vereist Hallo Hallo VM opnieuw wordt opgestart voordat afkomstig is online. Wanneer deze online is, downloadt Hallo DSC configuration .zip en deze in te richten op Hallo VM. Meer informatie vindt u in [hello Azure DSC-Extensieoverzicht](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-steps"></a>Volgende stappen
Hallo onderzoeken [Azure Resource Manager-sjabloon voor Hallo DSC-uitbreiding](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Meer informatie over hoe Hallo [referenties veilig worden verwerkt door DSC-extensie](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Zie voor meer informatie over hello Azure DSC-uitbreiding handler [inleiding toohello Azure Desired State Configuration extensie handler](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Voor meer informatie over PowerShell DSC [gaat u naar de PowerShell-documentatiecentrum hello](https://msdn.microsoft.com/powershell/dsc/overview). 

