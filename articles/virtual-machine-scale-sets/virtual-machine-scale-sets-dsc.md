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
# <a name="using-virtual-machine-scale-sets-with-hello-azure-dsc-extension"></a><span data-ttu-id="1cb84-103">Met behulp van de virtuele-Machineschaalsets met hello Azure DSC-uitbreiding</span><span class="sxs-lookup"><span data-stu-id="1cb84-103">Using Virtual Machine Scale Sets with hello Azure DSC Extension</span></span>
<span data-ttu-id="1cb84-104">[Virtuele-Machineschaalsets](virtual-machine-scale-sets-overview.md) kan worden gebruikt met Hallo [Azure Desired State Configuration (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extensie-handler.</span><span class="sxs-lookup"><span data-stu-id="1cb84-104">[Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md) can be used with hello [Azure Desired State Configuration (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extension handler.</span></span> <span data-ttu-id="1cb84-105">Virtuele-machineschaalsets bieden een manier toodeploy en beheren van grote aantallen virtuele machines en in en uit in het antwoord tooload kunnen schalen.</span><span class="sxs-lookup"><span data-stu-id="1cb84-105">Virtual machine scale sets provide a way toodeploy and manage large numbers of virtual machines, and can elastically scale in and out in response tooload.</span></span> <span data-ttu-id="1cb84-106">DSC is gebruikte tooconfigure Hallo VM's online komen zodat er Hallo productie software worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1cb84-106">DSC is used tooconfigure hello VMs as they come online so they are running hello production software.</span></span>

## <a name="differences-between-deploying-toovirtual-machines-and-virtual-machine-scale-sets"></a><span data-ttu-id="1cb84-107">Verschillen tussen tooVirtual Machines en virtuele-Machineschaalsets implementeren</span><span class="sxs-lookup"><span data-stu-id="1cb84-107">Differences between deploying tooVirtual Machines and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="1cb84-108">Hallo de onderliggende sjabloonstructuur voor een virtuele-machineschaalset enigszins afwijken van één VM is.</span><span class="sxs-lookup"><span data-stu-id="1cb84-108">hello underlying template structure for a virtual machine scale set is slightly different from a single VM.</span></span> <span data-ttu-id="1cb84-109">Een enkele virtuele machine implementeert in het bijzonder extensies onder Hallo 'informatie' knooppunt.</span><span class="sxs-lookup"><span data-stu-id="1cb84-109">Specifically, a single VM deploys extensions under hello "virtualMachines" node.</span></span> <span data-ttu-id="1cb84-110">Er is een vermelding van het type "extensies" waar DSC toohello sjabloon is toegevoegd</span><span class="sxs-lookup"><span data-stu-id="1cb84-110">There is an entry of type "extensions" where DSC is added toohello template</span></span>

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

<span data-ttu-id="1cb84-111">Een virtuele machine scale set knooppunt heeft een sectie 'Eigenschappen' Hello 'VirtualMachineProfile', 'extensionProfile'-kenmerk.</span><span class="sxs-lookup"><span data-stu-id="1cb84-111">A virtual machine scale set node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="1cb84-112">DSC wordt toegevoegd onder 'extensies'</span><span class="sxs-lookup"><span data-stu-id="1cb84-112">DSC is added under "extensions"</span></span>

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

## <a name="behavior-for-a-virtual-machine-scale-set"></a><span data-ttu-id="1cb84-113">Gedrag voor een virtuele-Machineschaalset</span><span class="sxs-lookup"><span data-stu-id="1cb84-113">Behavior for a Virtual Machine Scale Set</span></span>
<span data-ttu-id="1cb84-114">Hallo-gedrag voor een virtuele-machineschaalset is identiek toohello gedrag voor één VM.</span><span class="sxs-lookup"><span data-stu-id="1cb84-114">hello behavior for a virtual machine scale set is identical toohello behavior for a single VM.</span></span> <span data-ttu-id="1cb84-115">Wanneer een nieuwe virtuele machine wordt gemaakt, wordt het automatisch ingericht met Hallo DSC-extensie.</span><span class="sxs-lookup"><span data-stu-id="1cb84-115">When a new VM is created, it is automatically provisioned with hello DSC extension.</span></span> <span data-ttu-id="1cb84-116">Als een nieuwere versie van WMF Hallo-uitbreiding vereist Hallo Hallo VM opnieuw wordt opgestart voordat afkomstig is online.</span><span class="sxs-lookup"><span data-stu-id="1cb84-116">If a newer version of hello WMF is required by hello extension, hello VM reboots before coming online.</span></span> <span data-ttu-id="1cb84-117">Wanneer deze online is, downloadt Hallo DSC configuration .zip en deze in te richten op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="1cb84-117">Once it is online, it downloads hello DSC configuration .zip and provision it on hello VM.</span></span> <span data-ttu-id="1cb84-118">Meer informatie vindt u in [hello Azure DSC-Extensieoverzicht](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1cb84-118">More details can be found in [hello Azure DSC Extension Overview](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1cb84-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1cb84-119">Next steps</span></span>
<span data-ttu-id="1cb84-120">Hallo onderzoeken [Azure Resource Manager-sjabloon voor Hallo DSC-uitbreiding](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1cb84-120">Examine hello [Azure Resource Manager template for hello DSC extension](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="1cb84-121">Meer informatie over hoe Hallo [referenties veilig worden verwerkt door DSC-extensie](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1cb84-121">Learn how hello [DSC extension securely handles credentials](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="1cb84-122">Zie voor meer informatie over hello Azure DSC-uitbreiding handler [inleiding toohello Azure Desired State Configuration extensie handler](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1cb84-122">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="1cb84-123">Voor meer informatie over PowerShell DSC [gaat u naar de PowerShell-documentatiecentrum hello](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="1cb84-123">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

