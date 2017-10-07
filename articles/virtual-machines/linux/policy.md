---
title: aaaEnforce beveiliging met beleidsregels op Linux-machines in Azure | Microsoft Docs
description: Hoe tooapply een beleid tooan Linux virtuele Machine van Azure Resource Manager
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 06778ab4-f8ff-4eed-ae10-26a276fc3faa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: singhkay
ms.openlocfilehash: 5abd0c937578aba7e72b62c65b4eef9a9737aa2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="apply-policies-toolinux-vms-with-azure-resource-manager"></a>Toepassen van beleid tooLinux VM's met Azure Resource Manager
Met behulp van beleid, kan een organisatie verschillende conventies en regels in de onderneming Hallo afdwingen. Afdwinging van Hallo gewenst gedrag kunt risico's te beperken tijdens toohello succes van Hallo organisatie bij te dragen. In dit artikel wordt beschreven hoe u Azure Resource Manager beleid toodefine Hallo gewenst gedrag kunt gebruiken voor virtuele Machines die uw organisatie.

Zie voor een toopolicies inleiding [beleid toomanage resources en toegang beheren](../../azure-resource-manager/resource-manager-policy.md).

## <a name="permitted-virtual-machines"></a>Toegestane virtuele Machines
tooensure dat virtuele machines voor uw organisatie compatibel met een toepassing zijn, kunt u besturingssystemen toegestaan Hallo beperken. In Hallo volgende voorbeeld van een beleid, zodat u alleen Ubuntu 14.04.2-LTS virtuele Machines toobe gemaakt.

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "in": [
          "Microsoft.Compute/disks",
          "Microsoft.Compute/virtualMachines",
          "Microsoft.Compute/VirtualMachineScaleSets"
        ]
      },
      {
        "not": {
          "allOf": [
            {
              "field": "Microsoft.Compute/imagePublisher",
              "in": [
                "Canonical"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "UbuntuServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "14.04.2-LTS"
              ]
            },
            {
              "field": "Microsoft.Compute/imageVersion",
              "in": [
                "latest"
              ]
            }
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

Gebruik een jokerteken toomodify Hallo voorafgaand beleid tooallow geen Ubuntu LTS afbeelding: 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

Zie voor meer informatie over Beleidsvelden [beleid aliassen](../../azure-resource-manager/resource-manager-policy.md#aliases).

## <a name="managed-disks"></a>Managed Disks

toorequire hello gebruik van beheerde schijven gebruik Hallo volgende beleid:

```json
{
  "if": {
    "anyOf": [
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/virtualMachines"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/osDisk.uri",
            "exists": true
          }
        ]
      },
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/VirtualMachineScaleSets"
          },
          {
            "anyOf": [
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osDisk.vhdContainers",
                "exists": true
              },
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl",
                "exists": true
              }
            ]
          }
        ]
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="images-for-virtual-machines"></a>Installatiekopieën voor virtuele Machines

Uit veiligheidsoverwegingen kunt u vereisen dat alleen goedgekeurde aangepaste installatiekopieën in uw omgeving zijn geïmplementeerd. U kunt Hallo resourcegroep waarin Hallo goedgekeurd afbeeldingen of specifieke goedgekeurde installatiekopieën Hallo opgeven.

Hallo volgt vereist installatiekopieën van een goedgekeurde resourcegroep:

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in": [
                    "Microsoft.Compute/virtualMachines",
                    "Microsoft.Compute/VirtualMachineScaleSets"
                ]
            },
            {
                "not": {
                    "field": "Microsoft.Compute/imageId",
                    "contains": "resourceGroups/CustomImage"
                }
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
} 
```

Hallo volgende voorbeeld worden goedgekeurd Hallo installatiekopie id's:

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a>Uitbreidingen van de virtuele Machine

U kunt tooforbid informatie over het gebruik van bepaalde soorten uitbreidingen. Bijvoorbeeld, een uitbreiding mogelijk niet compatibel met bepaalde afbeeldingen aangepaste virtuele machine. Hallo volgende voorbeeld wordt getoond hoe tooblock een bepaalde extensie. Gebruikt deze uitgever en type toodetermine welke tooblock extensie.

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Compute/virtualMachines/extensions"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/publisher",
                "equals": "Microsoft.Compute"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/type",
                "equals": "{extension-type}"

      }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```


## <a name="next-steps"></a>Volgende stappen
* Na het definiëren van een beleidsregel (zoals weergegeven in de voorgaande voorbeelden Hallo), u moet toocreate hello beleidsdefinitie en wijs deze tooa bereik. Hallo bereik mag een abonnement, resourcegroep of resource. tooassign beleid via de portal hello, Zie [gebruik Azure portal tooassign en beheren van bronbeleid](../../azure-resource-manager/resource-manager-policy-portal.md). tooassign beleid via REST API, PowerShell of Azure CLI, Zie [toewijzen en beheren van beleid via script](../../azure-resource-manager/resource-manager-policy-create-assign.md).
* Zie voor een inleiding tooresource beleidsregels, [Resource overzicht](../../azure-resource-manager/resource-manager-policy.md).
* Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](../../azure-resource-manager/resource-manager-subscription-governance.md).
