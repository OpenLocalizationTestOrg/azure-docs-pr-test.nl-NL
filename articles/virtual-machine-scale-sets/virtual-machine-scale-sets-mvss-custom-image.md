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
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a><span data-ttu-id="e36e0-103">Een aangepaste installatiekopie tooan Azure scale ingesteld sjabloon toevoegen</span><span class="sxs-lookup"><span data-stu-id="e36e0-103">Add a custom image tooan Azure scale set template</span></span>

<span data-ttu-id="e36e0-104">Dit artikel laat zien hoe toomodify hello [minimale levensvatbaar schaalset sjabloon](./virtual-machine-scale-sets-mvss-start.md) toodeploy van aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="e36e0-104">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toodeploy from custom image.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="e36e0-105">Hallo Sjabloondefinitie wijzigen</span><span class="sxs-lookup"><span data-stu-id="e36e0-105">Change hello template definition</span></span>

<span data-ttu-id="e36e0-106">Onze minimale levensvatbaar scale set sjabloon kan worden gezien [hier](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), en de sjabloon voor de implementatie van Hallo scale is ingesteld op basis van een aangepaste installatiekopie kan worden bekeken [hier](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="e36e0-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello scale set from a custom image can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span></span> <span data-ttu-id="e36e0-107">Behandeld Hallo diff gebruikt toocreate deze sjabloon (`git diff minimum-viable-scale-set custom-image`) stuk door stuk:</span><span class="sxs-lookup"><span data-stu-id="e36e0-107">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set custom-image`) piece by piece:</span></span>

### <a name="creating-a-managed-disk-image"></a><span data-ttu-id="e36e0-108">Installatiekopie van een beheerde schijf maken</span><span class="sxs-lookup"><span data-stu-id="e36e0-108">Creating a managed disk image</span></span>

<span data-ttu-id="e36e0-109">Als u al een aangepaste beheerde schijfkopie (een resource van het type `Microsoft.Compute/images`), en vervolgens kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="e36e0-109">If you already have a custom managed disk image (a resource of type `Microsoft.Compute/images`), then you can skip this section.</span></span>

<span data-ttu-id="e36e0-110">Eerst voegen we een `sourceImageVhdUri` parameter Hallo URI toohello gegeneraliseerd blob in Azure Storage dat Hallo aangepaste installatiekopie toodeploy van bevat.</span><span class="sxs-lookup"><span data-stu-id="e36e0-110">First, we add a `sourceImageVhdUri` parameter, which is hello URI toohello generalized blob in Azure Storage that contains hello custom image toodeploy from.</span></span>


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

<span data-ttu-id="e36e0-111">Vervolgens we voegt u een resource van het type `Microsoft.Compute/images`, die is Hallo beheerde schijfimage gebaseerd op Hallo gegeneraliseerd blob zich bevindt op URI `sourceImageVhdUri`.</span><span class="sxs-lookup"><span data-stu-id="e36e0-111">Next, we add a resource of type `Microsoft.Compute/images`, which is hello managed disk image based on hello generalized blob located at URI `sourceImageVhdUri`.</span></span> <span data-ttu-id="e36e0-112">Deze afbeelding moet Hallo dezelfde regio als Hallo scale set die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e36e0-112">This image must be in hello same region as hello scale set that uses it.</span></span> <span data-ttu-id="e36e0-113">In de eigenschappen van Hallo afbeelding Hallo we Hallo OS-type, Hallo-locatie van de blob Hallo opgeven (van Hallo `sourceImageVhdUri` parameter), en het type opslagaccount Hallo:</span><span class="sxs-lookup"><span data-stu-id="e36e0-113">In hello properties of hello image, we specify hello OS type, hello location of hello blob (from hello `sourceImageVhdUri` parameter), and hello storage account type:</span></span>

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

<span data-ttu-id="e36e0-114">In Hallo schaalset resource, we voegen een `dependsOn` component verwijst toohello aangepaste installatiekopie toomake ervoor Hallo afbeelding opgehaald gemaakt voordat wordt geprobeerd schaalset hello toodeploy vanuit die installatiekopie:</span><span class="sxs-lookup"><span data-stu-id="e36e0-114">In hello scale set resource, we add a `dependsOn` clause referring toohello custom image toomake sure hello image gets created before hello scale set tries toodeploy from that image:</span></span>

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

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a><span data-ttu-id="e36e0-115">Wijzigen van de schaal instellen eigenschappen toouse Hallo beheerde schijfimage</span><span class="sxs-lookup"><span data-stu-id="e36e0-115">Changing scale set properties toouse hello managed disk image</span></span>

<span data-ttu-id="e36e0-116">In Hallo `imageReference` van Hallo schaal ingesteld `storageProfile`, in plaats van geven Hallo uitgever, aanbieding, sku en versie van een besturingssysteemkopie, opgegeven Hallo `id` Hallo `Microsoft.Compute/images` resource:</span><span class="sxs-lookup"><span data-stu-id="e36e0-116">In hello `imageReference` of hello scale set `storageProfile`, instead of specifying hello publisher, offer, sku, and version of a platform image, we specify hello `id` of hello `Microsoft.Compute/images` resource:</span></span>

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

<span data-ttu-id="e36e0-117">In dit voorbeeld gebruiken we Hallo `resourceId` functie tooget Hallo bron-ID van de installatiekopie van het Hallo gemaakt in Hallo dezelfde sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e36e0-117">In this example, we use hello `resourceId` function tooget hello resource ID of hello image created in hello same template.</span></span> <span data-ttu-id="e36e0-118">Als u de beheerde schijfimage Hallo vooraf hebt gemaakt, moet u in plaats daarvan Hallo-id van die installatiekopie opgeven.</span><span class="sxs-lookup"><span data-stu-id="e36e0-118">If you have created hello managed disk image beforehand, you should provide hello id of that image instead.</span></span> <span data-ttu-id="e36e0-119">Deze id moet van het formulier Hallo: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span><span class="sxs-lookup"><span data-stu-id="e36e0-119">This id must be of hello form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e36e0-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e36e0-120">Next Steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
