---
title: Een Azure Resource Manager-sjabloon scale set voor het gebruik van beheerde schijven converteren | Microsoft Docs
description: Een set scale sjabloon converteren naar een beheerde schijf scale set-sjabloon.
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
ms.openlocfilehash: 2f5cb85703888c5056611d466f508547ee72e44b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="convert-a-scale-set-template-to-a-managed-disk-scale-set-template"></a><span data-ttu-id="0e137-104">Een set scale sjabloon converteren naar een beheerde schijf scale set-sjabloon</span><span class="sxs-lookup"><span data-stu-id="0e137-104">Convert a scale set template to a managed disk scale set template</span></span>

<span data-ttu-id="0e137-105">Klanten met een Resource Manager-sjabloon voor het maken van een scale-set niet met behulp van beheerde schijven mogelijk wilt wijzigen om beheerde schijf te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0e137-105">Customers with a Resource Manager template for creating a scale set not using managed disk may wish to modify it to use managed disk.</span></span> <span data-ttu-id="0e137-106">Dit artikel laat zien hoe u kunt dit doen met een voorbeeld van een pull-aanvraag van de [Azure-Snelstartsjablonen](https://github.com/Azure/azure-quickstart-templates), een opslagplaats community aangestuurde voor Resource Manager-voorbeeldsjablonen.</span><span class="sxs-lookup"><span data-stu-id="0e137-106">This article shows how to do this, using as an example a pull request from the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates), a community-driven repo for sample Resource Manager templates.</span></span> <span data-ttu-id="0e137-107">De volledige pull-aanvraag ziet u hier: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), en de belangrijke onderdelen van de diff zijn hieronder, samen met uitleg:</span><span class="sxs-lookup"><span data-stu-id="0e137-107">The full pull request can be seen here: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), and the relevant parts of the diff are below, along with explanations:</span></span>

## <a name="making-the-os-disks-managed"></a><span data-ttu-id="0e137-108">De OS-schijven beheerd maken</span><span class="sxs-lookup"><span data-stu-id="0e137-108">Making the OS disks managed</span></span>

<span data-ttu-id="0e137-109">In de onderstaande diff kunt zien we dat we verschillende variabelen die zijn gerelateerd aan de eigenschappen van de schijf en -account van de opslag hebt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="0e137-109">In the diff below, we can see that we have removed several variables related to storage account and disk properties.</span></span> <span data-ttu-id="0e137-110">Opslagaccounttype is niet meer nodig (Standard_LRS is de standaardinstelling), maar we het nog steeds kan opgeven als we willen.</span><span class="sxs-lookup"><span data-stu-id="0e137-110">Storage account type is no longer necessary (Standard_LRS is the default), but we could still specify it if we wished to.</span></span> <span data-ttu-id="0e137-111">Alleen Standard_LRS en Premium_LRS worden ondersteund met beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="0e137-111">Only Standard_LRS and Premium_LRS are supported with managed disk.</span></span> <span data-ttu-id="0e137-112">Nieuw achtervoegsel voor de storage-account, unieke tekenreeksmatrix en sa aantal werden gebruikt in de oude sjabloon voor het genereren van de namen van opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="0e137-112">New storage account suffix, unique string array, and sa count were used in the old template to generate storage account names.</span></span> <span data-ttu-id="0e137-113">Deze variabelen zijn niet meer nodig in de nieuwe sjabloon omdat beheerde schijven automatisch storage-accounts namens de klant maakt.</span><span class="sxs-lookup"><span data-stu-id="0e137-113">These variables are no longer necessary in the new template because managed disk automatically creates storage accounts on the customer's behalf.</span></span> <span data-ttu-id="0e137-114">Op dezelfde manier de naam van de vhd-container en naam besturingssysteemschijf zijn niet langer nodig omdat beheerde schijven automatisch de naam van de onderliggende opslag blob-containers en schijven.</span><span class="sxs-lookup"><span data-stu-id="0e137-114">Similarly, vhd container name and os disk name are no longer necessary because managed disk automatically names the underlying storage blob containers and disks.</span></span>

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


<span data-ttu-id="0e137-115">In de onderstaande diff kunt zien we dat we de berekening die is bijgewerkt naar 2016-04-30-preview, die de eerste vereiste versie voor ondersteuning van beheerde schijven bij schaalsets api-versie.</span><span class="sxs-lookup"><span data-stu-id="0e137-115">In the diff below, we can see that we updated the compute api version to 2016-04-30-preview, which is the earliest required version for managed disk support with scale sets.</span></span> <span data-ttu-id="0e137-116">Houd er rekening mee dat we nog steeds niet-beheerde schijven in de nieuwe api-versie met de syntaxis van de oude gebruiken kan indien gewenst.</span><span class="sxs-lookup"><span data-stu-id="0e137-116">Note that we could still use unmanaged disks in the new api version with the old syntax if desired.</span></span> <span data-ttu-id="0e137-117">Met andere woorden, als we alleen de compute-update api-versie en niets anders niet wijzigen, de sjabloon moet blijven werken als voorheen.</span><span class="sxs-lookup"><span data-stu-id="0e137-117">In other words, if we only update the compute api version and don't change anything else, the template should continue to work as before.</span></span>

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

<span data-ttu-id="0e137-118">In de onderstaande diff kunt zien we dat we de opslagbronnen account van de matrix resources volledig verwijdert.</span><span class="sxs-lookup"><span data-stu-id="0e137-118">In the diff below, we can see that we are removing the storage account resource from the resources array completely.</span></span> <span data-ttu-id="0e137-119">We nodig deze niet meer omdat beheerde schijven ze automatisch namens ons maakt.</span><span class="sxs-lookup"><span data-stu-id="0e137-119">We no longer need them since managed disk creates them automatically on our behalf.</span></span>

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

<span data-ttu-id="0e137-120">In de onderstaande diff we zien we verwijdert het afhankelijk is van een component van de schaal is ingesteld op de lus die het maken van opslagaccounts verwijst.</span><span class="sxs-lookup"><span data-stu-id="0e137-120">In the diff below, we can see that we are removing the depends on clause referring from the scale set to the loop that was creating storage accounts.</span></span> <span data-ttu-id="0e137-121">In de oude sjabloon is dit ervoor te zorgen dat de storage-accounts zijn gemaakt voordat de schaalaanpassingsset begon het maken, maar deze component niet langer met beheerde schijf nodig is.</span><span class="sxs-lookup"><span data-stu-id="0e137-121">In the old template, this was ensuring that the storage accounts were created before the scale set began creation, but this clause is no longer necessary with managed disk.</span></span> <span data-ttu-id="0e137-122">We ook de eigenschap vhd-containers en verwijderen de naameigenschap van de os-schijf als deze eigenschappen automatisch achter de schermen worden verwerkt door beheerde schijf.</span><span class="sxs-lookup"><span data-stu-id="0e137-122">We also remove the vhd containers property, and the os disk name property as these properties are automatically handled under the hood by managed disk.</span></span> <span data-ttu-id="0e137-123">Als we de volgende vragen, kunnen we toevoegen `"managedDisk": { "storageAccountType": "Premium_LRS" }` in de configuratie 'osDisk' als we premium OS-schijven wilden.</span><span class="sxs-lookup"><span data-stu-id="0e137-123">If we wished, we could add `"managedDisk": { "storageAccountType": "Premium_LRS" }` in the "osDisk" configuration if we wanted premium OS disks.</span></span> <span data-ttu-id="0e137-124">Alleen virtuele machines met een hoofdletter of kleine van ' in de virtuele machine sku premium-schijven kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0e137-124">Only VMs with an uppercase or lowercase 's' in the VM sku can use premium disks.</span></span>

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

<span data-ttu-id="0e137-125">Er is geen expliciete eigenschap in de configuratie van de set scale voor of moet worden beheerd of onbeheerd schijf gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0e137-125">There is no explicit property in the scale set configuration for whether to use managed or unmanaged disk.</span></span> <span data-ttu-id="0e137-126">De schaalaanpassingsset kent die wordt gebruikt op basis van de eigenschappen die aanwezig in het opslagprofiel voor zijn.</span><span class="sxs-lookup"><span data-stu-id="0e137-126">The scale set knows which to use based on the properties that are present in the storage profile.</span></span> <span data-ttu-id="0e137-127">Het is dus belangrijk bij het wijzigen van de sjabloon om ervoor te zorgen dat de juiste eigenschappen in het opslagprofiel van de schaal is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="0e137-127">Thus, it is important when modifying the template to ensure that the right properties are in the storage profile of the scale set.</span></span>


## <a name="data-disks"></a><span data-ttu-id="0e137-128">Gegevensschijven</span><span class="sxs-lookup"><span data-stu-id="0e137-128">Data disks</span></span>

<span data-ttu-id="0e137-129">Met de bovenstaande wijzigingen schijf scale set maakt gebruik van beheerde schijven voor het besturingssysteem, maar wat over gegevensschijven?</span><span class="sxs-lookup"><span data-stu-id="0e137-129">With the changes above, the scale set uses managed disks for the OS disk, but what about data disks?</span></span> <span data-ttu-id="0e137-130">Om toe te voegen gegevensschijven, de eigenschap 'dataDisks' onder 'storageProfile' op hetzelfde niveau als 'osDisk' niet toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0e137-130">To add data disks, add the "dataDisks" property under "storageProfile" at the same level as "osDisk".</span></span> <span data-ttu-id="0e137-131">De waarde van de eigenschap is een JSON-lijst met objecten, die allemaal eigenschappen 'lun' (die uniek zijn per gegevensschijf op een virtuele machine), 'createOption' ('leeg' is momenteel de enige ondersteunde optie), en "diskSizeGB" (de grootte van de schijf, in gigabytes; moet groter dan 0 en kleiner zijn dan 1024) zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0e137-131">The value of the property is a JSON list of objects, each of which has properties "lun" (which must be unique per data disk on a VM), "createOption" ("empty" is currently the only supported option), and "diskSizeGB" (the size of the disk in gigabytes; must be greater than 0 and less than 1024) as in the following example:</span></span> 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

<span data-ttu-id="0e137-132">Als u opgeeft `n` schijven in deze matrix elke virtuele machine in de schaal ingesteld opgehaald `n` gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="0e137-132">If you specify `n` disks in this array, each VM in the scale set gets `n` data disks.</span></span> <span data-ttu-id="0e137-133">Merk echter op dat deze gegevensschijven onbewerkte apparaten zijn.</span><span class="sxs-lookup"><span data-stu-id="0e137-133">Do note, however, that these data disks are raw devices.</span></span> <span data-ttu-id="0e137-134">Ze zijn niet opgemaakt.</span><span class="sxs-lookup"><span data-stu-id="0e137-134">They are not formatted.</span></span> <span data-ttu-id="0e137-135">Het is tot de klant te koppelen, paritition, en de schijven formatteren voordat u ze gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0e137-135">It is up to the customer to attach, paritition, and format the disks before using them.</span></span> <span data-ttu-id="0e137-136">Er kan ook Geef eventueel `"managedDisk": { "storageAccountType": "Premium_LRS" }` in elke schijf gegevensobject om op te geven dat deze een gegevensschijf premium moet.</span><span class="sxs-lookup"><span data-stu-id="0e137-136">Optionally, we could also specify `"managedDisk": { "storageAccountType": "Premium_LRS" }` in each data disk object to specify that it should be a premium data disk.</span></span> <span data-ttu-id="0e137-137">Alleen virtuele machines met een hoofdletter of kleine van ' in de virtuele machine sku premium-schijven kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0e137-137">Only VMs with an uppercase or lowercase 's' in the VM sku can use premium disks.</span></span>

<span data-ttu-id="0e137-138">Zie voor meer informatie over het gebruik van gegevensschijven met schaalsets, [in dit artikel](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="0e137-138">To learn more about using data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="0e137-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0e137-139">Next steps</span></span>
<span data-ttu-id="0e137-140">Bijvoorbeeld-schaalsets, met Resource Manager-sjablonen zoeken 'vmss' in de [github-repo-Azure-Snelstartsjablonen](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="0e137-140">For example Resource Manager templates using scale sets, search for "vmss" in the [Azure Quickstart Templates github repo](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="0e137-141">Bekijk voor algemene informatie, de [belangrijkste startpagina voor schaalsets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="0e137-141">For general information, check out the [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

