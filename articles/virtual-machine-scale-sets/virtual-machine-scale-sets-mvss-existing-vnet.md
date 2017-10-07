---
title: Verwijst naar een bestaand virtueel netwerk in een Azure-scale set-sjabloon | Microsoft Docs
description: Meer informatie over hoe tooadd een virtueel netwerk tooan bestaande Azure virtuele-Machineschaalset sjabloon
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: negat
ms.openlocfilehash: c3034b577e17abc4643dc26d7c38ad643fa26322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-reference-tooan-existing-virtual-network-in-an-azure-scale-set-template"></a>Verwijzing tooan bestaand virtueel netwerk in een Azure-scale set-sjabloon toevoegen

Dit artikel laat zien hoe toomodify hello [minimale levensvatbaar schaalset sjabloon](./virtual-machine-scale-sets-mvss-start.md) toodeploy in een bestaand virtueel netwerk in plaats van een nieuwe maken.

## <a name="change-hello-template-definition"></a>Hallo Sjabloondefinitie wijzigen

Onze minimale levensvatbaar scale set sjabloon kan worden gezien [hier](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), en de sjabloon voor de implementatie van Hallo schaal instellen in een bestaand virtueel netwerk kan worden bekeken [hier](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json). Behandeld Hallo diff gebruikt toocreate deze sjabloon (`git diff minimum-viable-scale-set existing-vnet`) stuk door stuk:

Eerst voegen we een `subnetId` parameter. Deze tekenreeks worden doorgegeven in Hallo scale set configuratie, zodat u Hallo schaalset tooidentify Hallo vooraf gemaakte subnet toodeploy virtuele machines in. Deze tekenreeks moet van het formulier Hallo: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`. Bijvoorbeeld: toodeploy Hallo schaal ingesteld in een bestaand virtueel netwerk met de naam `myvnet`, subnet `mysubnet`, resourcegroep `myrg`, en het abonnement `00000000-0000-0000-0000-000000000000`, Hallo subnetId zou zijn: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "subnetId": {
+      "type": "string"
     }
   },
```

Vervolgens we Hallo virtueel netwerk resource kunt verwijderen uit Hallo `resources` matrix, aangezien we met behulp van een bestaand virtueel netwerk en niet toodeploy een nieuwe hoeft.

```diff
   "variables": {},
   "resources": [
-    {
-      "type": "Microsoft.Network/virtualNetworks",
-      "name": "myVnet",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "2016-12-01",
-      "properties": {
-        "addressSpace": {
-          "addressPrefixes": [
-            "10.0.0.0/16"
-          ]
-        },
-        "subnets": [
-          {
-            "name": "mySubnet",
-            "properties": {
-              "addressPrefix": "10.0.0.0/16"
-            }
-          }
-        ]
-      }
-    },
```

Hallo virtueel netwerk bestaat al voordat Hallo sjabloon wordt geïmplementeerd, zodat er geen toospecify moet een component dependsOn uit Hallo schaal toohello virtueel netwerk instellen. Dus verwijderen we deze regels:

```diff
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
-      "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
-      ],
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
```

Ten slotte, geven we in Hallo `subnetId` parameterset door Hallo gebruiker (in plaats van `resourceId` tooget Hallo-id van een vnet in dezelfde implementatie, die welke Hallo minimale levensvatbaar schaalset sjabloon biedt Hallo).

```diff
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
-                          "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
+                          "id": "[parameters('subnetId')]"
                         }
                       }
                     }
```




## <a name="next-steps"></a>Volgende stappen

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
