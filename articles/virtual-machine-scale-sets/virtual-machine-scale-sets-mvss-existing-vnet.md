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
# <a name="add-reference-tooan-existing-virtual-network-in-an-azure-scale-set-template"></a><span data-ttu-id="a83f1-103">Verwijzing tooan bestaand virtueel netwerk in een Azure-scale set-sjabloon toevoegen</span><span class="sxs-lookup"><span data-stu-id="a83f1-103">Add reference tooan existing virtual network in an Azure scale set template</span></span>

<span data-ttu-id="a83f1-104">Dit artikel laat zien hoe toomodify hello [minimale levensvatbaar schaalset sjabloon](./virtual-machine-scale-sets-mvss-start.md) toodeploy in een bestaand virtueel netwerk in plaats van een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="a83f1-104">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toodeploy into an existing virtual network instead of creating a new one.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="a83f1-105">Hallo Sjabloondefinitie wijzigen</span><span class="sxs-lookup"><span data-stu-id="a83f1-105">Change hello template definition</span></span>

<span data-ttu-id="a83f1-106">Onze minimale levensvatbaar scale set sjabloon kan worden gezien [hier](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), en de sjabloon voor de implementatie van Hallo schaal instellen in een bestaand virtueel netwerk kan worden bekeken [hier](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="a83f1-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello scale set into an existing virtual network can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span></span> <span data-ttu-id="a83f1-107">Behandeld Hallo diff gebruikt toocreate deze sjabloon (`git diff minimum-viable-scale-set existing-vnet`) stuk door stuk:</span><span class="sxs-lookup"><span data-stu-id="a83f1-107">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="a83f1-108">Eerst voegen we een `subnetId` parameter.</span><span class="sxs-lookup"><span data-stu-id="a83f1-108">First, we add a `subnetId` parameter.</span></span> <span data-ttu-id="a83f1-109">Deze tekenreeks worden doorgegeven in Hallo scale set configuratie, zodat u Hallo schaalset tooidentify Hallo vooraf gemaakte subnet toodeploy virtuele machines in.</span><span class="sxs-lookup"><span data-stu-id="a83f1-109">This string will be passed into hello scale set configuration, allowing hello scale set tooidentify hello pre-created subnet toodeploy virtual machines into.</span></span> <span data-ttu-id="a83f1-110">Deze tekenreeks moet van het formulier Hallo: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span><span class="sxs-lookup"><span data-stu-id="a83f1-110">This string must be of hello form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span></span> <span data-ttu-id="a83f1-111">Bijvoorbeeld: toodeploy Hallo schaal ingesteld in een bestaand virtueel netwerk met de naam `myvnet`, subnet `mysubnet`, resourcegroep `myrg`, en het abonnement `00000000-0000-0000-0000-000000000000`, Hallo subnetId zou zijn: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span><span class="sxs-lookup"><span data-stu-id="a83f1-111">For instance, toodeploy hello scale set into an existing virtual network with name `myvnet`, subnet `mysubnet`, resource group `myrg`, and subscription `00000000-0000-0000-0000-000000000000`, hello subnetId would be: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span></span>

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

<span data-ttu-id="a83f1-112">Vervolgens we Hallo virtueel netwerk resource kunt verwijderen uit Hallo `resources` matrix, aangezien we met behulp van een bestaand virtueel netwerk en niet toodeploy een nieuwe hoeft.</span><span class="sxs-lookup"><span data-stu-id="a83f1-112">Next, we can delete hello virtual network resource from hello `resources` array, since we are using an existing virtual network and don't need toodeploy a new one.</span></span>

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

<span data-ttu-id="a83f1-113">Hallo virtueel netwerk bestaat al voordat Hallo sjabloon wordt geïmplementeerd, zodat er geen toospecify moet een component dependsOn uit Hallo schaal toohello virtueel netwerk instellen.</span><span class="sxs-lookup"><span data-stu-id="a83f1-113">hello virtual network already exists before hello template is deployed, so there is no need toospecify a dependsOn clause from hello scale set toohello virtual network.</span></span> <span data-ttu-id="a83f1-114">Dus verwijderen we deze regels:</span><span class="sxs-lookup"><span data-stu-id="a83f1-114">Thus, we delete these lines:</span></span>

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

<span data-ttu-id="a83f1-115">Ten slotte, geven we in Hallo `subnetId` parameterset door Hallo gebruiker (in plaats van `resourceId` tooget Hallo-id van een vnet in dezelfde implementatie, die welke Hallo minimale levensvatbaar schaalset sjabloon biedt Hallo).</span><span class="sxs-lookup"><span data-stu-id="a83f1-115">Finally, we pass in hello `subnetId` parameter set by hello user (instead of using `resourceId` tooget hello id of a vnet in hello same deployment, which is what hello minimum viable scale set template does).</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="a83f1-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a83f1-116">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
