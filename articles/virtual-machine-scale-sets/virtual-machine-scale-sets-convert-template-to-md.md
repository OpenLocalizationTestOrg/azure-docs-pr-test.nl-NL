---
title: een Azure Resource Manager-schaal aaaConvert ingesteld sjabloon toouse-beheerde schijven | Microsoft Docs
description: Een sjabloon scale set sjabloon tooa-beheerde schijven scale set converteren.
keywords: Virtuele-machineschaalsets
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: bc8c377a-8c3f-45b8-8b2d-acc2d6d0b1e8
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/18/2017
ms.author: negat
ms.openlocfilehash: 66c2217647e57ed2cfa39660c0175710ae2e63be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-scale-set-template-tooa-managed-disk-scale-set-template"></a>Een sjabloon scale set sjabloon tooa-beheerde schijven scale set converteren

Klanten met een Resource Manager-sjabloon voor het maken van een schaal ingesteld niet met beheerde schijven kunnen toomodify desgewenst het toouse beheerd schijf. Dit artikel laat zien hoe toodo deze, met als voorbeeld een pull-aanvraag van Hallo [Azure-Snelstartsjablonen](https://github.com/Azure/azure-quickstart-templates), een opslagplaats community aangestuurde voor Resource Manager-voorbeeldsjablonen. Hallo volledige pull-aanvraag ziet u hier: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), en Hallo relevante delen van Hallo diff zijn hieronder, samen met uitleg:

## <a name="making-hello-os-disks-managed"></a>Hallo OS schijven beheerd maken

In Hallo diff hieronder ziet u dat we verschillende variabelen gerelateerde toostorage eigenschappen en het schijf hebt verwijderd. Opslagaccounttype is niet meer nodig (Standard_LRS is Hallo standaard), maar we het nog steeds kan opgeven als we willen. Alleen Standard_LRS en Premium_LRS worden ondersteund met beheerde schijven. Nieuw achtervoegsel voor de storage-account, unieke tekenreeksmatrix en sa aantal werden gebruikt in Hallo oude sjabloon toogenerate namen van opslagaccounts. Deze variabelen zijn niet meer nodig in de nieuwe sjabloon Hallo omdat beheerde schijven automatisch storage-accounts van de klant Hallo namens maakt. Op dezelfde manier de naam van de vhd-container en naam besturingssysteemschijf zijn niet langer nodig omdat beheerde schijven automatisch een naam Hallo onderliggende storage-blob-containers en schijven.

```diff
   "variables": {
-    "storageAccountType": "Standard_LRS",
     "namingInfix": "[toLower(substring(concat(parameters('vmssName'), uniqueString(resourceGroup().id)), 0, 9))]",
     "longNamingInfix": "[toLower(parameters('vmssName'))]",
-    "newStorageAccountSuffix": "[concat(variables('namingInfix'), 'sa')]",
-    "uniqueStringArray": [
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '0')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '1')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '2')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '3')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '4')))]"
-    ],
-    "saCount": "[length(variables('uniqueStringArray'))]",
-    "vhdContainerName": "[concat(variables('namingInfix'), 'vhd')]",
-    "osDiskName": "[concat(variables('namingInfix'), 'osdisk')]",
     "addressPrefix": "10.0.0.0/16",
     "subnetPrefix": "10.0.0.0/24",
     "virtualNetworkName": "[concat(variables('namingInfix'), 'vnet')]",
```


In Hallo diff hieronder we kunt Zie dat we Hallo bijgewerkt berekenen api-versie too2016-04-30-preview, Hallo vroegst vereist versie voor ondersteuning van beheerde schijven bij-schaalsets. Houd er rekening mee dat we nog steeds niet-beheerde schijven in de nieuwe api-versie Hallo met oude syntaxis Hallo gebruiken kan indien gewenst. Met andere woorden, als we alleen bijwerken Hallo api-versie berekenen en niets anders niet wijzigen, Hallo sjabloon toowork als voordat moet blijven.

```diff
@@ -86,7 +74,7 @@
       "version": "latest"
     },
     "imageReference": "[variables('osType')]",
-    "computeApiVersion": "2016-03-30",
+    "computeApiVersion": "2016-04-30-preview",
     "networkApiVersion": "2016-03-30",
     "storageApiVersion": "2015-06-15"
   },
```

In Hallo diff hieronder ziet u dat worden verwijderd Hallo storage account resource van een matrix van Hallo resources volledig. We nodig deze niet meer omdat beheerde schijven ze automatisch namens ons maakt.

```diff
@@ -113,19 +101,6 @@
       }
     },
-    {
-      "type": "Microsoft.Storage/storageAccounts",
-      "name": "[concat(variables('uniqueStringArray')[copyIndex()], variables('newStorageAccountSuffix'))]",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "[variables('storageApiVersion')]",
-      "copy": {
-        "name": "storageLoop",
-        "count": "[variables('saCount')]"
-      },
-      "properties": {
-        "accountType": "[variables('storageAccountType')]"
-      }
-    },
     {
       "type": "Microsoft.Network/publicIPAddresses",
       "name": "[variables('publicIPAddressName')]",
       "location": "[resourceGroup().location]",
```

Hallo diff hieronder we kunt Zie dat Hallo worden verwijderd afhankelijk component vanuit Hallo scale set toohello lus die het maken van opslagaccounts verwijst. In de oude sjabloon hello, is dit ervoor te zorgen dat Hallo storage-accounts zijn gemaakt voordat schaalset Hallo begon het maken, maar deze component niet langer nodig met beheerde schijven is. We ook Hallo vhd-containers eigenschap verwijderen en Hallo naameigenschap os-schijf als deze eigenschappen automatisch achter de schermen Hallo door beheerde schijf verwerkt worden. Als we de volgende vragen, kunnen we toevoegen `"managedDisk": { "storageAccountType": "Premium_LRS" }` in Hallo 'osDisk' configuratie als we premium OS-schijven wilden. Alleen virtuele machines met een hoofdletter of kleine van ' in hello VM sku premium-schijven kunt gebruiken.

```diff
@@ -183,7 +158,6 @@
       "location": "[resourceGroup().location]",
       "apiVersion": "[variables('computeApiVersion')]",
       "dependsOn": [
-        "storageLoop",
         "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
         "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
       ],
@@ -200,16 +174,8 @@
         "virtualMachineProfile": {
           "storageProfile": {
             "osDisk": {
-              "vhdContainers": [
-                "[concat('https://', variables('uniqueStringArray')[0], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[1], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[2], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[3], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[4], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]"
-              ],
-              "name": "[variables('osDiskName')]",
             },
             "imageReference": "[variables('imageReference')]"
           },

```

Er is geen expliciete eigenschap in Hallo scale set configuratie of toouse beheerd of onbeheerd schijf. Hallo schaalset weet welke toouse op basis van Hallo-eigenschappen die in het opslagprofiel Hallo aanwezig zijn. Het is dus belangrijk bij het wijzigen van Hallo sjabloon tooensure die Hallo rechts eigenschappen in het opslagprofiel Hallo van Hallo scale set zijn.


## <a name="data-disks"></a>Gegevensschijven

Met de bovenstaande Hallo wijzigingen schijf Hallo scale set maakt gebruik van beheerde schijven voor Hallo OS, maar wat over gegevensschijven? tooadd gegevensschijven, toevoegen Hallo 'dataDisks' eigenschap onder 'storageProfile' op hetzelfde niveau als 'osDisk' hello. Hallo waarde van eigenschap Hallo is een JSON-lijst met objecten, die allemaal eigenschappen 'lun' (die uniek zijn per gegevensschijf op een virtuele machine), 'createOption' ('leeg' wordt momenteel Hallo alleen optie ondersteund), en 'diskSizeGB' (grootte van de schijf, in gigabytes Hallo Hallo; moet zijn groter dan 0 en kleiner zijn dan 1024) als in Hallo voorbeeld te volgen: 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

Als u opgeeft `n` schijven in deze matrix elke virtuele machine in Hallo scale ingesteld opgehaald `n` gegevensschijven. Merk echter op dat deze gegevensschijven onbewerkte apparaten zijn. Ze zijn niet opgemaakt. Het is van toohello klant tooattach, paritition en indeling Hallo schijven voordat u ze gebruikt. Er kan ook Geef eventueel `"managedDisk": { "storageAccountType": "Premium_LRS" }` in elke gegevens schijf object toospecify dat deze een gegevensschijf premium moet. Alleen virtuele machines met een hoofdletter of kleine van ' in hello VM sku premium-schijven kunt gebruiken.

toolearn meer informatie over het gebruik van gegevensschijven met schaalsets, Zie [in dit artikel](./virtual-machine-scale-sets-attached-disks.md).


## <a name="next-steps"></a>Volgende stappen
Bijvoorbeeld-schaalsets, met Resource Manager-sjablonen op Zoeken naar 'vmss' hello [github-repo-Azure-Snelstartsjablonen](https://github.com/Azure/azure-quickstart-templates).

Raadpleeg voor algemene informatie Hallo [belangrijkste startpagina voor schaalsets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).

