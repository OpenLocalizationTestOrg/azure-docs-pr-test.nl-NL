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
# <a name="convert-a-scale-set-template-tooa-managed-disk-scale-set-template"></a><span data-ttu-id="ad8f2-104">Een sjabloon scale set sjabloon tooa-beheerde schijven scale set converteren</span><span class="sxs-lookup"><span data-stu-id="ad8f2-104">Convert a scale set template tooa managed disk scale set template</span></span>

<span data-ttu-id="ad8f2-105">Klanten met een Resource Manager-sjabloon voor het maken van een schaal ingesteld niet met beheerde schijven kunnen toomodify desgewenst het toouse beheerd schijf.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-105">Customers with a Resource Manager template for creating a scale set not using managed disk may wish toomodify it toouse managed disk.</span></span> <span data-ttu-id="ad8f2-106">Dit artikel laat zien hoe toodo deze, met als voorbeeld een pull-aanvraag van Hallo [Azure-Snelstartsjablonen](https://github.com/Azure/azure-quickstart-templates), een opslagplaats community aangestuurde voor Resource Manager-voorbeeldsjablonen.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-106">This article shows how toodo this, using as an example a pull request from hello [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates), a community-driven repo for sample Resource Manager templates.</span></span> <span data-ttu-id="ad8f2-107">Hallo volledige pull-aanvraag ziet u hier: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), en Hallo relevante delen van Hallo diff zijn hieronder, samen met uitleg:</span><span class="sxs-lookup"><span data-stu-id="ad8f2-107">hello full pull request can be seen here: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), and hello relevant parts of hello diff are below, along with explanations:</span></span>

## <a name="making-hello-os-disks-managed"></a><span data-ttu-id="ad8f2-108">Hallo OS schijven beheerd maken</span><span class="sxs-lookup"><span data-stu-id="ad8f2-108">Making hello OS disks managed</span></span>

<span data-ttu-id="ad8f2-109">In Hallo diff hieronder ziet u dat we verschillende variabelen gerelateerde toostorage eigenschappen en het schijf hebt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-109">In hello diff below, we can see that we have removed several variables related toostorage account and disk properties.</span></span> <span data-ttu-id="ad8f2-110">Opslagaccounttype is niet meer nodig (Standard_LRS is Hallo standaard), maar we het nog steeds kan opgeven als we willen.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-110">Storage account type is no longer necessary (Standard_LRS is hello default), but we could still specify it if we wished to.</span></span> <span data-ttu-id="ad8f2-111">Alleen Standard_LRS en Premium_LRS worden ondersteund met beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-111">Only Standard_LRS and Premium_LRS are supported with managed disk.</span></span> <span data-ttu-id="ad8f2-112">Nieuw achtervoegsel voor de storage-account, unieke tekenreeksmatrix en sa aantal werden gebruikt in Hallo oude sjabloon toogenerate namen van opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-112">New storage account suffix, unique string array, and sa count were used in hello old template toogenerate storage account names.</span></span> <span data-ttu-id="ad8f2-113">Deze variabelen zijn niet meer nodig in de nieuwe sjabloon Hallo omdat beheerde schijven automatisch storage-accounts van de klant Hallo namens maakt.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-113">These variables are no longer necessary in hello new template because managed disk automatically creates storage accounts on hello customer's behalf.</span></span> <span data-ttu-id="ad8f2-114">Op dezelfde manier de naam van de vhd-container en naam besturingssysteemschijf zijn niet langer nodig omdat beheerde schijven automatisch een naam Hallo onderliggende storage-blob-containers en schijven.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-114">Similarly, vhd container name and os disk name are no longer necessary because managed disk automatically names hello underlying storage blob containers and disks.</span></span>

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


<span data-ttu-id="ad8f2-115">In Hallo diff hieronder we kunt Zie dat we Hallo bijgewerkt berekenen api-versie too2016-04-30-preview, Hallo vroegst vereist versie voor ondersteuning van beheerde schijven bij-schaalsets.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-115">In hello diff below, we can see that we updated hello compute api version too2016-04-30-preview, which is hello earliest required version for managed disk support with scale sets.</span></span> <span data-ttu-id="ad8f2-116">Houd er rekening mee dat we nog steeds niet-beheerde schijven in de nieuwe api-versie Hallo met oude syntaxis Hallo gebruiken kan indien gewenst.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-116">Note that we could still use unmanaged disks in hello new api version with hello old syntax if desired.</span></span> <span data-ttu-id="ad8f2-117">Met andere woorden, als we alleen bijwerken Hallo api-versie berekenen en niets anders niet wijzigen, Hallo sjabloon toowork als voordat moet blijven.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-117">In other words, if we only update hello compute api version and don't change anything else, hello template should continue toowork as before.</span></span>

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

<span data-ttu-id="ad8f2-118">In Hallo diff hieronder ziet u dat worden verwijderd Hallo storage account resource van een matrix van Hallo resources volledig.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-118">In hello diff below, we can see that we are removing hello storage account resource from hello resources array completely.</span></span> <span data-ttu-id="ad8f2-119">We nodig deze niet meer omdat beheerde schijven ze automatisch namens ons maakt.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-119">We no longer need them since managed disk creates them automatically on our behalf.</span></span>

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

<span data-ttu-id="ad8f2-120">Hallo diff hieronder we kunt Zie dat Hallo worden verwijderd afhankelijk component vanuit Hallo scale set toohello lus die het maken van opslagaccounts verwijst.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-120">In hello diff below, we can see that we are removing hello depends on clause referring from hello scale set toohello loop that was creating storage accounts.</span></span> <span data-ttu-id="ad8f2-121">In de oude sjabloon hello, is dit ervoor te zorgen dat Hallo storage-accounts zijn gemaakt voordat schaalset Hallo begon het maken, maar deze component niet langer nodig met beheerde schijven is.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-121">In hello old template, this was ensuring that hello storage accounts were created before hello scale set began creation, but this clause is no longer necessary with managed disk.</span></span> <span data-ttu-id="ad8f2-122">We ook Hallo vhd-containers eigenschap verwijderen en Hallo naameigenschap os-schijf als deze eigenschappen automatisch achter de schermen Hallo door beheerde schijf verwerkt worden.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-122">We also remove hello vhd containers property, and hello os disk name property as these properties are automatically handled under hello hood by managed disk.</span></span> <span data-ttu-id="ad8f2-123">Als we de volgende vragen, kunnen we toevoegen `"managedDisk": { "storageAccountType": "Premium_LRS" }` in Hallo 'osDisk' configuratie als we premium OS-schijven wilden.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-123">If we wished, we could add `"managedDisk": { "storageAccountType": "Premium_LRS" }` in hello "osDisk" configuration if we wanted premium OS disks.</span></span> <span data-ttu-id="ad8f2-124">Alleen virtuele machines met een hoofdletter of kleine van ' in hello VM sku premium-schijven kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-124">Only VMs with an uppercase or lowercase 's' in hello VM sku can use premium disks.</span></span>

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

<span data-ttu-id="ad8f2-125">Er is geen expliciete eigenschap in Hallo scale set configuratie of toouse beheerd of onbeheerd schijf.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-125">There is no explicit property in hello scale set configuration for whether toouse managed or unmanaged disk.</span></span> <span data-ttu-id="ad8f2-126">Hallo schaalset weet welke toouse op basis van Hallo-eigenschappen die in het opslagprofiel Hallo aanwezig zijn.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-126">hello scale set knows which toouse based on hello properties that are present in hello storage profile.</span></span> <span data-ttu-id="ad8f2-127">Het is dus belangrijk bij het wijzigen van Hallo sjabloon tooensure die Hallo rechts eigenschappen in het opslagprofiel Hallo van Hallo scale set zijn.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-127">Thus, it is important when modifying hello template tooensure that hello right properties are in hello storage profile of hello scale set.</span></span>


## <a name="data-disks"></a><span data-ttu-id="ad8f2-128">Gegevensschijven</span><span class="sxs-lookup"><span data-stu-id="ad8f2-128">Data disks</span></span>

<span data-ttu-id="ad8f2-129">Met de bovenstaande Hallo wijzigingen schijf Hallo scale set maakt gebruik van beheerde schijven voor Hallo OS, maar wat over gegevensschijven? tooadd gegevensschijven, toevoegen Hallo 'dataDisks' eigenschap onder 'storageProfile' op hetzelfde niveau als 'osDisk' hello.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-129">With hello changes above, hello scale set uses managed disks for hello OS disk, but what about data disks? tooadd data disks, add hello "dataDisks" property under "storageProfile" at hello same level as "osDisk".</span></span> <span data-ttu-id="ad8f2-130">Hallo waarde van eigenschap Hallo is een JSON-lijst met objecten, die allemaal eigenschappen 'lun' (die uniek zijn per gegevensschijf op een virtuele machine), 'createOption' ('leeg' wordt momenteel Hallo alleen optie ondersteund), en 'diskSizeGB' (grootte van de schijf, in gigabytes Hallo Hallo; moet zijn groter dan 0 en kleiner zijn dan 1024) als in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="ad8f2-130">hello value of hello property is a JSON list of objects, each of which has properties "lun" (which must be unique per data disk on a VM), "createOption" ("empty" is currently hello only supported option), and "diskSizeGB" (hello size of hello disk in gigabytes; must be greater than 0 and less than 1024) as in hello following example:</span></span> 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

<span data-ttu-id="ad8f2-131">Als u opgeeft `n` schijven in deze matrix elke virtuele machine in Hallo scale ingesteld opgehaald `n` gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-131">If you specify `n` disks in this array, each VM in hello scale set gets `n` data disks.</span></span> <span data-ttu-id="ad8f2-132">Merk echter op dat deze gegevensschijven onbewerkte apparaten zijn.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-132">Do note, however, that these data disks are raw devices.</span></span> <span data-ttu-id="ad8f2-133">Ze zijn niet opgemaakt.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-133">They are not formatted.</span></span> <span data-ttu-id="ad8f2-134">Het is van toohello klant tooattach, paritition en indeling Hallo schijven voordat u ze gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-134">It is up toohello customer tooattach, paritition, and format hello disks before using them.</span></span> <span data-ttu-id="ad8f2-135">Er kan ook Geef eventueel `"managedDisk": { "storageAccountType": "Premium_LRS" }` in elke gegevens schijf object toospecify dat deze een gegevensschijf premium moet.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-135">Optionally, we could also specify `"managedDisk": { "storageAccountType": "Premium_LRS" }` in each data disk object toospecify that it should be a premium data disk.</span></span> <span data-ttu-id="ad8f2-136">Alleen virtuele machines met een hoofdletter of kleine van ' in hello VM sku premium-schijven kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ad8f2-136">Only VMs with an uppercase or lowercase 's' in hello VM sku can use premium disks.</span></span>

<span data-ttu-id="ad8f2-137">toolearn meer informatie over het gebruik van gegevensschijven met schaalsets, Zie [in dit artikel](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="ad8f2-137">toolearn more about using data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="ad8f2-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ad8f2-138">Next steps</span></span>
<span data-ttu-id="ad8f2-139">Bijvoorbeeld-schaalsets, met Resource Manager-sjablonen op Zoeken naar 'vmss' hello [github-repo-Azure-Snelstartsjablonen](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="ad8f2-139">For example Resource Manager templates using scale sets, search for "vmss" in hello [Azure Quickstart Templates github repo](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="ad8f2-140">Raadpleeg voor algemene informatie Hallo [belangrijkste startpagina voor schaalsets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="ad8f2-140">For general information, check out hello [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

