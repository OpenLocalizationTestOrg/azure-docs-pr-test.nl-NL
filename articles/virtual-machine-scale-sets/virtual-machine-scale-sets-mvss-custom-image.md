---
title: Verwijst naar een aangepaste installatiekopie in een Azure-scale set-sjabloon | Microsoft Docs
description: Meer informatie over hoe tooadd een aangepaste installatiekopie tooan bestaande Azure virtuele-Machineschaalset sjabloon
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
ms.date: 5/10/2017
ms.author: negat
ms.openlocfilehash: 6a17d989e44d241b460238c0106350c3ef038e56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a>Een aangepaste installatiekopie tooan Azure scale ingesteld sjabloon toevoegen

Dit artikel laat zien hoe toomodify hello [minimale levensvatbaar schaalset sjabloon](./virtual-machine-scale-sets-mvss-start.md) toodeploy van aangepaste installatiekopie.

## <a name="change-hello-template-definition"></a>Hallo Sjabloondefinitie wijzigen

Onze minimale levensvatbaar scale set sjabloon kan worden gezien [hier](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), en de sjabloon voor de implementatie van Hallo scale is ingesteld op basis van een aangepaste installatiekopie kan worden bekeken [hier](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json). Behandeld Hallo diff gebruikt toocreate deze sjabloon (`git diff minimum-viable-scale-set custom-image`) stuk door stuk:

### <a name="creating-a-managed-disk-image"></a>Installatiekopie van een beheerde schijf maken

Als u al een aangepaste beheerde schijfkopie (een resource van het type `Microsoft.Compute/images`), en vervolgens kunt u deze sectie overslaan.

Eerst voegen we een `sourceImageVhdUri` parameter Hallo URI toohello gegeneraliseerd blob in Azure Storage dat Hallo aangepaste installatiekopie toodeploy van bevat.


```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "sourceImageVhdUri": {
+      "type": "string",
+      "metadata": {
+        "description": "hello source of hello generalized blob containing hello custom image"
+      }
     }
   },
   "variables": {},
```

Vervolgens we voegt u een resource van het type `Microsoft.Compute/images`, die is Hallo beheerde schijfimage gebaseerd op Hallo gegeneraliseerd blob zich bevindt op URI `sourceImageVhdUri`. Deze afbeelding moet Hallo dezelfde regio als Hallo scale set die wordt gebruikt. In de eigenschappen van Hallo afbeelding Hallo we Hallo OS-type, Hallo-locatie van de blob Hallo opgeven (van Hallo `sourceImageVhdUri` parameter), en het type opslagaccount Hallo:

```diff
   "resources": [
     {
+      "type": "Microsoft.Compute/images",
+      "apiVersion": "2016-04-30-preview",
+      "name": "myCustomImage",
+      "location": "[resourceGroup().location]",
+      "properties": {
+        "storageProfile": {
+          "osDisk": {
+            "osType": "Linux",
+            "osState": "Generalized",
+            "blobUri": "[parameters('sourceImageVhdUri')]",
+            "storageAccountType": "Standard_LRS"
+          }
+        }
+      }
+    },
+    {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "location": "[resourceGroup().location]",

```

In Hallo schaalset resource, we voegen een `dependsOn` component verwijst toohello aangepaste installatiekopie toomake ervoor Hallo afbeelding opgehaald gemaakt voordat wordt geprobeerd schaalset hello toodeploy vanuit die installatiekopie:

```diff
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
       "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
+        "Microsoft.Network/virtualNetworks/myVnet",
+        "Microsoft.Compute/images/myCustomImage"
       ],
       "sku": {
         "name": "Standard_A1",

```

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a>Wijzigen van de schaal instellen eigenschappen toouse Hallo beheerde schijfimage

In Hallo `imageReference` van Hallo schaal ingesteld `storageProfile`, in plaats van geven Hallo uitgever, aanbieding, sku en versie van een besturingssysteemkopie, opgegeven Hallo `id` Hallo `Microsoft.Compute/images` resource:

```diff
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
-              "publisher": "Canonical",
-              "offer": "UbuntuServer",
-              "sku": "16.04-LTS",
-              "version": "latest"
+              "id": "[resourceId('Microsoft.Compute/images', 'myCustomImage')]"
             }
           },
           "osProfile": {
```

In dit voorbeeld gebruiken we Hallo `resourceId` functie tooget Hallo bron-ID van de installatiekopie van het Hallo gemaakt in Hallo dezelfde sjabloon. Als u de beheerde schijfimage Hallo vooraf hebt gemaakt, moet u in plaats daarvan Hallo-id van die installatiekopie opgeven. Deze id moet van het formulier Hallo: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.


## <a name="next-steps"></a>Volgende stappen

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
