---
title: aaaDeploy meerdere exemplaren van Azure-resources | Microsoft Docs
description: Kopieerbewerking en matrices in een Azure Resource Manager-sjabloon tooiterate meerdere keren gebruiken bij het implementeren van resources.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 94d95810-a87b-460f-8e82-c69d462ac3ca
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/26/2017
ms.author: tomfitz
ms.openlocfilehash: a3bd42f694053317c30b639c33dc4efae41a9a9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a><span data-ttu-id="5d67b-103">Implementeren van meerdere exemplaren van een resource of eigenschap in Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="5d67b-103">Deploy multiple instances of a resource or property in Azure Resource Manager templates</span></span>
<span data-ttu-id="5d67b-104">Dit onderwerp leest u hoe tooiterate in uw Azure Resource Manager-sjabloon toocreate meerdere exemplaren van een resource of meerdere exemplaren van een eigenschap van een resource.</span><span class="sxs-lookup"><span data-stu-id="5d67b-104">This topic shows you how tooiterate in your Azure Resource Manager template toocreate multiple instances of a resource, or multiple instances of a property on a resource.</span></span>

<span data-ttu-id="5d67b-105">Als u moet tooadd logica tooyour sjabloon waarmee u toospecify of een resource wordt geïmplementeerd, Zie [voorwaardelijk implementeren resource](#conditionally-deploy-resource).</span><span class="sxs-lookup"><span data-stu-id="5d67b-105">If you need tooadd logic tooyour template that enables you toospecify whether a resource is deployed, see [Conditionally deploy resource](#conditionally-deploy-resource).</span></span>

## <a name="resource-iteration"></a><span data-ttu-id="5d67b-106">Resource herhaling</span><span class="sxs-lookup"><span data-stu-id="5d67b-106">Resource iteration</span></span>
<span data-ttu-id="5d67b-107">toocreate meerdere exemplaren van een brontype toevoegen een `copy` element toohello brontype.</span><span class="sxs-lookup"><span data-stu-id="5d67b-107">toocreate multiple instances of a resource type, add a `copy` element toohello resource type.</span></span> <span data-ttu-id="5d67b-108">Hallo aantal iteraties en een naam voor deze lus opgeven in Hallo kopie-element.</span><span class="sxs-lookup"><span data-stu-id="5d67b-108">In hello copy element, you specify hello number of iterations and a name for this loop.</span></span> <span data-ttu-id="5d67b-109">Hallo count-waarde moet een positief geheel getal zijn en mag niet meer dan 800.</span><span class="sxs-lookup"><span data-stu-id="5d67b-109">hello count value must be a positive integer and cannot exceed 800.</span></span> <span data-ttu-id="5d67b-110">Resource Manager maakt Hallo resources parallel.</span><span class="sxs-lookup"><span data-stu-id="5d67b-110">Resource Manager creates hello resources in parallel.</span></span> <span data-ttu-id="5d67b-111">Hallo volgorde waarin ze zijn gemaakt kan daarom niet worden gegarandeerd.</span><span class="sxs-lookup"><span data-stu-id="5d67b-111">Therefore, hello order in which they are created is not guaranteed.</span></span> <span data-ttu-id="5d67b-112">herhaald toocreate resources in de juiste volgorde, Zie [seriële kopiëren](#serial-copy).</span><span class="sxs-lookup"><span data-stu-id="5d67b-112">toocreate iterated resources in sequence, see [Serial copy](#serial-copy).</span></span> 

<span data-ttu-id="5d67b-113">Hallo resource toocreate wordt meerdere keren Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="5d67b-113">hello resource toocreate multiple times takes hello following format:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        }
    ],
    "outputs": {}
}
```

<span data-ttu-id="5d67b-114">U ziet dat Hallo naam van elke resource bevat Hallo `copyIndex()` functie de huidige herhaling Hallo in Hallo lus retourneert.</span><span class="sxs-lookup"><span data-stu-id="5d67b-114">Notice that hello name of each resource includes hello `copyIndex()` function, which returns hello current iteration in hello loop.</span></span> <span data-ttu-id="5d67b-115">`copyIndex()`is gebaseerd op nul.</span><span class="sxs-lookup"><span data-stu-id="5d67b-115">`copyIndex()` is zero-based.</span></span> <span data-ttu-id="5d67b-116">In dat geval Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="5d67b-116">So, hello following example:</span></span>

```json
"name": "[concat('storage', copyIndex())]",
```

<span data-ttu-id="5d67b-117">Deze namen maakt:</span><span class="sxs-lookup"><span data-stu-id="5d67b-117">Creates these names:</span></span>

* <span data-ttu-id="5d67b-118">storage0</span><span class="sxs-lookup"><span data-stu-id="5d67b-118">storage0</span></span>
* <span data-ttu-id="5d67b-119">storage1</span><span class="sxs-lookup"><span data-stu-id="5d67b-119">storage1</span></span>
* <span data-ttu-id="5d67b-120">storage2.</span><span class="sxs-lookup"><span data-stu-id="5d67b-120">storage2.</span></span>

<span data-ttu-id="5d67b-121">toooffset hello indexwaarde, kunt u een waarde in de functie copyIndex() Hallo doorgeven.</span><span class="sxs-lookup"><span data-stu-id="5d67b-121">toooffset hello index value, you can pass a value in hello copyIndex() function.</span></span> <span data-ttu-id="5d67b-122">Hallo aantal iteraties tooperform is nog steeds opgegeven in Hallo kopie element, maar Hallo-waarde van copyIndex wordt gecompenseerd door Hallo opgegeven waarde.</span><span class="sxs-lookup"><span data-stu-id="5d67b-122">hello number of iterations tooperform is still specified in hello copy element, but hello value of copyIndex is offset by hello specified value.</span></span> <span data-ttu-id="5d67b-123">In dat geval Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="5d67b-123">So, hello following example:</span></span>

```json
"name": "[concat('storage', copyIndex(1))]",
```

<span data-ttu-id="5d67b-124">Deze namen maakt:</span><span class="sxs-lookup"><span data-stu-id="5d67b-124">Creates these names:</span></span>

* <span data-ttu-id="5d67b-125">storage1</span><span class="sxs-lookup"><span data-stu-id="5d67b-125">storage1</span></span>
* <span data-ttu-id="5d67b-126">storage2</span><span class="sxs-lookup"><span data-stu-id="5d67b-126">storage2</span></span>
* <span data-ttu-id="5d67b-127">storage3</span><span class="sxs-lookup"><span data-stu-id="5d67b-127">storage3</span></span>

<span data-ttu-id="5d67b-128">Hallo kopieerbewerking is handig bij het werken met matrices omdat u elk element in de matrix Hallo kunt doorlopen.</span><span class="sxs-lookup"><span data-stu-id="5d67b-128">hello copy operation is helpful when working with arrays because you can iterate through each element in hello array.</span></span> <span data-ttu-id="5d67b-129">Gebruik Hallo `length` functie op Hallo matrix toospecify Hallo aantal voor iteraties, en `copyIndex` tooretrieve Hallo huidige index in Hallo matrix.</span><span class="sxs-lookup"><span data-stu-id="5d67b-129">Use hello `length` function on hello array toospecify hello count for iterations, and `copyIndex` tooretrieve hello current index in hello array.</span></span> <span data-ttu-id="5d67b-130">In dat geval Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="5d67b-130">So, hello following example:</span></span>

```json
"parameters": { 
  "org": { 
     "type": "array", 
     "defaultValue": [ 
         "contoso", 
         "fabrikam", 
         "coho" 
      ] 
  }
}, 
"resources": [ 
  { 
      "name": "[concat('storage', parameters('org')[copyIndex()])]", 
      "copy": { 
         "name": "storagecopy", 
         "count": "[length(parameters('org'))]" 
      }, 
      ...
  } 
]
```

<span data-ttu-id="5d67b-131">Deze namen maakt:</span><span class="sxs-lookup"><span data-stu-id="5d67b-131">Creates these names:</span></span>

* <span data-ttu-id="5d67b-132">storagecontoso</span><span class="sxs-lookup"><span data-stu-id="5d67b-132">storagecontoso</span></span>
* <span data-ttu-id="5d67b-133">storagefabrikam</span><span class="sxs-lookup"><span data-stu-id="5d67b-133">storagefabrikam</span></span>
* <span data-ttu-id="5d67b-134">storagecoho</span><span class="sxs-lookup"><span data-stu-id="5d67b-134">storagecoho</span></span>

## <a name="serial-copy"></a><span data-ttu-id="5d67b-135">Seriële kopiëren</span><span class="sxs-lookup"><span data-stu-id="5d67b-135">Serial copy</span></span>

<span data-ttu-id="5d67b-136">Wanneer u Hallo kopie element toocreate implementeert meerdere exemplaren van een resourcetype Resource Manager worden standaard de instanties parallel.</span><span class="sxs-lookup"><span data-stu-id="5d67b-136">When you use hello copy element toocreate multiple instances of a resource type, Resource Manager, by default, deploys those instances in parallel.</span></span> <span data-ttu-id="5d67b-137">U kunt echter toospecify die Hallo resources worden geïmplementeerd in de reeks.</span><span class="sxs-lookup"><span data-stu-id="5d67b-137">However, you may want toospecify that hello resources are deployed in sequence.</span></span> <span data-ttu-id="5d67b-138">Bijvoorbeeld bij het bijwerken van een productieomgeving kunt u toostagger Hallo bijgewerkt zodat alleen bepaalde op elk gewenst moment worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="5d67b-138">For example, when updating a production environment, you may want toostagger hello updates so only a certain number are updated at any one time.</span></span>

<span data-ttu-id="5d67b-139">Resource Manager biedt de eigenschappen op Hallo kopie-element waarmee u tooserially implementeren meerdere exemplaren.</span><span class="sxs-lookup"><span data-stu-id="5d67b-139">Resource Manager provides properties on hello copy element that enable you tooserially deploy multiple instances.</span></span> <span data-ttu-id="5d67b-140">Instellen in element kopiëren Hallo `mode` te**seriële** en `batchSize` toohello aantal exemplaren toodeploy tegelijk.</span><span class="sxs-lookup"><span data-stu-id="5d67b-140">In hello copy element, set `mode` too**serial** and `batchSize` toohello number of instances toodeploy at a time.</span></span> <span data-ttu-id="5d67b-141">Seriële modus maakt Resource Manager met een afhankelijkheid voor eerdere exemplaren in de lus hello, zodat dit niet één batch gestart totdat de vorige batch Hallo is voltooid.</span><span class="sxs-lookup"><span data-stu-id="5d67b-141">With serial mode, Resource Manager creates a dependency on earlier instances in hello loop, so it does not start one batch until hello previous batch completes.</span></span>

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

<span data-ttu-id="5d67b-142">Hallo eigenschap mode accepteert ook **parallelle**, namelijk Hallo-standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="5d67b-142">hello mode property also accepts **parallel**, which is hello default value.</span></span>

<span data-ttu-id="5d67b-143">tootest seriële kopiëren zonder dat er feitelijke webbronnen gebruik Hallo-sjabloon die wordt geïmplementeerd leeg geneste sjablonen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5d67b-143">tootest serial copy without creating actual resources, use hello following template that deploys empty nested templates:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "numberToDeploy": {
      "type": "int",
      "minValue": 2,
      "defaultValue": 5
    }
  },
  "resources": [
    {
      "apiVersion": "2015-01-01",
      "type": "Microsoft.Resources/deployments",
      "name": "[concat('loop-', copyIndex())]",
      "copy": {
        "name": "iterator",
        "count": "[parameters('numberToDeploy')]",
        "mode": "serial",
        "batchSize": 1
      },
      "properties": {
        "mode": "Incremental",
        "template": {
          "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {},
          "variables": {},
          "resources": [],
          "outputs": {
          }
        }
      }
    }
  ],
  "outputs": {
  }
}
```

<span data-ttu-id="5d67b-144">In Hallo implementatiegeschiedenis, merk op dat geneste implementaties Hallo verwerkt in de reeks.</span><span class="sxs-lookup"><span data-stu-id="5d67b-144">In hello deployment history, notice that hello nested deployments are processed in sequence.</span></span>

![seriële implementatie](./media/resource-group-create-multiple/serial-copy.png)

<span data-ttu-id="5d67b-146">Voor een meer realistische scenario implementeert Hallo voorbeeld van de volgende twee instanties op een tijdstip van een Linux-VM uit een geneste sjabloon:</span><span class="sxs-lookup"><span data-stu-id="5d67b-146">For a more realistic scenario, hello following example deploys two instances at a time of a Linux VM from a nested template:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for hello Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for hello Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for hello Public IP used tooaccess hello Virtual Machine."
            }
        },
        "ubuntuOSVersion": {
            "type": "string",
            "defaultValue": "16.04.0-LTS",
            "allowedValues": [
                "12.04.5-LTS",
                "14.04.5-LTS",
                "15.10",
                "16.04.0-LTS"
            ],
            "metadata": {
                "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version."
            }
        }
    },
    "variables": {
        "templatelink": "https://raw.githubusercontent.com/rjmax/Build2017/master/Act1.TemplateEnhancements/Chapter03.LinuxVM.json"
    },
    "resources": [
        {
            "apiVersion": "2015-01-01",
            "name": "[concat('nestedDeployment',copyIndex())]",
            "type": "Microsoft.Resources/deployments",
            "copy": {
                "name": "myCopySet",
                "count": 4,
                "mode": "serial",
                "batchSize": 2
            },
            "properties": {
                "mode": "Incremental",
                "templateLink": {
                    "uri": "[variables('templatelink')]",
                    "contentVersion": "1.0.0.0"
                },
                "parameters": {
                    "adminUsername": {
                        "value": "[parameters('adminUsername')]"
                    },
                    "adminPassword": {
                        "value": "[parameters('adminPassword')]"
                    },
                    "dnsLabelPrefix": {
                        "value": "[parameters('dnsLabelPrefix')]"
                    },
                    "ubuntuOSVersion": {
                        "value": "[parameters('ubuntuOSVersion')]"
                    },
                    "index":{
                        "value": "[copyIndex()]"
                    }
                }
            }
        }
    ]
}
```

## <a name="property-iteration"></a><span data-ttu-id="5d67b-147">Eigenschap herhaling</span><span class="sxs-lookup"><span data-stu-id="5d67b-147">Property iteration</span></span>

<span data-ttu-id="5d67b-148">toocreate meerdere waarden voor een eigenschap van een resource toevoegen een `copy` matrix in Hallo eigenschappen element.</span><span class="sxs-lookup"><span data-stu-id="5d67b-148">toocreate multiple values for a property on a resource, add a `copy` array in hello properties element.</span></span> <span data-ttu-id="5d67b-149">Deze matrix bevat objecten en elk object heeft Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="5d67b-149">This array contains objects, and each object has hello following properties:</span></span>

* <span data-ttu-id="5d67b-150">naam - Hallo van Hallo eigenschap toocreate meerdere waarden voor</span><span class="sxs-lookup"><span data-stu-id="5d67b-150">name - hello name of hello property toocreate multiple values for</span></span>
* <span data-ttu-id="5d67b-151">het aantal waarden toocreate Hallo - tellen</span><span class="sxs-lookup"><span data-stu-id="5d67b-151">count - hello number of values toocreate</span></span>
* <span data-ttu-id="5d67b-152">invoer - object dat Hallo waarden tooassign toohello-eigenschap bevat</span><span class="sxs-lookup"><span data-stu-id="5d67b-152">input - an object that contains hello values tooassign toohello property</span></span>  

<span data-ttu-id="5d67b-153">Hallo volgende voorbeeld wordt getoond hoe tooapply `copy` toohello dataDisks-eigenschap op een virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="5d67b-153">hello following example shows how tooapply `copy` toohello dataDisks property on a virtual machine:</span></span>

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "copy": [{
          "name": "dataDisks",
          "count": 3,
          "input": {
              "lun": "[copyIndex('dataDisks')]",
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

<span data-ttu-id="5d67b-154">Merk op dat wanneer u `copyIndex` binnen een iteratie eigenschap u Hallo-naam van Hallo herhaling moet opgeven.</span><span class="sxs-lookup"><span data-stu-id="5d67b-154">Notice that when using `copyIndex` inside a property iteration, you must provide hello name of hello iteration.</span></span> <span data-ttu-id="5d67b-155">U hoeft geen tooprovide Hallo naam gebruikt in combinatie met resource herhaling.</span><span class="sxs-lookup"><span data-stu-id="5d67b-155">You do not have tooprovide hello name when used with resource iteration.</span></span>

<span data-ttu-id="5d67b-156">Resource Manager worden uitgevouwen Hallo `copy` matrix tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="5d67b-156">Resource Manager expands hello `copy` array during deployment.</span></span> <span data-ttu-id="5d67b-157">Hallo-naam van de matrix hello wordt Hallo-naam van Hallo-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="5d67b-157">hello name of hello array becomes hello name of hello property.</span></span> <span data-ttu-id="5d67b-158">Hallo invoerwaarden worden Hallo objecteigenschappen.</span><span class="sxs-lookup"><span data-stu-id="5d67b-158">hello input values become hello object properties.</span></span> <span data-ttu-id="5d67b-159">Hallo geïmplementeerd sjabloon als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="5d67b-159">hello deployed template becomes:</span></span>

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "dataDisks": [
          {
              "lun": 0,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 1,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 2,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

<span data-ttu-id="5d67b-160">U kunt resource en de eigenschap iteratie samen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5d67b-160">You can use resource and property iteration together.</span></span> <span data-ttu-id="5d67b-161">Verwijzing Hallo herhaling eigenschap met de naam.</span><span class="sxs-lookup"><span data-stu-id="5d67b-161">Reference hello property iteration by name.</span></span>

```json
{
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[concat(parameters('vnetname'), copyIndex())]",
    "apiVersion": "2016-06-01",
    "copy":{
        "count": 2,
        "name": "vnetloop"
    },
    "location": "[resourceGroup().location]",
    "properties": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "copy": [
            {
                "name": "subnets",
                "count": 2,
                "input": {
                    "name": "[concat('subnet-', copyIndex('subnets'))]",
                    "properties": {
                        "addressPrefix": "[variables('subnetAddressPrefix')[copyIndex('subnets')]]"
                    }
                }
            }
        ]
    }
}
```

<span data-ttu-id="5d67b-162">U kunt alleen één exemplaar element opnemen in Hallo-eigenschappen voor elke resource.</span><span class="sxs-lookup"><span data-stu-id="5d67b-162">You can only include one copy element in hello properties for each resource.</span></span> <span data-ttu-id="5d67b-163">meerdere objecten toospecify een lus herhaling voor meer dan één eigenschap definiëren in Hallo kopie matrix.</span><span class="sxs-lookup"><span data-stu-id="5d67b-163">toospecify an iteration loop for more than one property, define multiple objects in hello copy array.</span></span> <span data-ttu-id="5d67b-164">Elk object wordt afzonderlijk herhaald.</span><span class="sxs-lookup"><span data-stu-id="5d67b-164">Each object is iterated separately.</span></span> <span data-ttu-id="5d67b-165">Bijvoorbeeld: toocreate meerdere exemplaren van beide Hallo `frontendIPConfigurations` eigenschap en Hallo `loadBalancingRules` eigenschap op een load balancer beide objecten definiëren die in een element met één exemplaar:</span><span class="sxs-lookup"><span data-stu-id="5d67b-165">For example, toocreate multiple instances of both hello `frontendIPConfigurations` property and hello `loadBalancingRules` property on a load balancer, define both objects in a single copy element:</span></span> 

```json
{
    "name": "[variables('loadBalancerName')]",
    "type": "Microsoft.Network/loadBalancers",
    "properties": {
        "copy": [
          {
              "name": "frontendIPConfigurations",
              "count": 2,
              "input": {
                  "name": "[concat('loadBalancerFrontEnd', copyIndex('frontendIPConfigurations', 1))]",
                  "properties": {
                      "publicIPAddress": {
                          "id": "[variables(concat('publicIPAddressID', copyIndex('frontendIPConfigurations', 1)))]"
                      }
                  }
              }
          },
          {
              "name": "loadBalancingRules",
              "count": 2,
              "input": {
                  "name": "[concat('LBRuleForVIP', copyIndex('loadBalancingRules', 1))]",
                  "properties": {
                      "frontendIPConfiguration": {
                          "id": "[variables(concat('frontEndIPConfigID', copyIndex('loadBalancingRules', 1)))]"
                      },
                      "backendAddressPool": {
                          "id": "[variables('lbBackendPoolID')]"
                      },
                      "protocol": "tcp",
                      "frontendPort": "[variables(concat('frontEndPort' copyIndex('loadBalancingRules', 1))]",
                      "backendPort": "[variables(concat('backEndPort' copyIndex('loadBalancingRules', 1))]",
                      "probe": {
                          "id": "[variables('lbProbeID')]"
                      }
                  }
              }
          }
        ],
        ...
    }
}
```

## <a name="depend-on-resources-in-a-loop"></a><span data-ttu-id="5d67b-166">Afhankelijk zijn van bronnen in een lus</span><span class="sxs-lookup"><span data-stu-id="5d67b-166">Depend on resources in a loop</span></span>
<span data-ttu-id="5d67b-167">U opgeven dat een resource na een andere resource wordt geïmplementeerd met behulp van Hallo `dependsOn` element.</span><span class="sxs-lookup"><span data-stu-id="5d67b-167">You specify that a resource is deployed after another resource by using hello `dependsOn` element.</span></span> <span data-ttu-id="5d67b-168">een resource die afhankelijk zijn van de verzameling van resources in een lus Hallo toodeploy Hallo naam opgeven van Hallo kopie lus in Hallo dependsOn element.</span><span class="sxs-lookup"><span data-stu-id="5d67b-168">toodeploy a resource that depends on hello collection of resources in a loop, provide hello name of hello copy loop in hello dependsOn element.</span></span> <span data-ttu-id="5d67b-169">Hallo volgende voorbeeld ziet u hoe toodeploy drie storage-accounts voordat u implementeert Hallo voor virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="5d67b-169">hello following example shows how toodeploy three storage accounts before deploying hello Virtual Machine.</span></span> <span data-ttu-id="5d67b-170">Hallo volledige virtuele Machine definitie wordt niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5d67b-170">hello full Virtual Machine definition is not shown.</span></span> <span data-ttu-id="5d67b-171">U ziet dat Hallo kopie-element heeft naam ingesteld te`storagecopy` en ook Hallo dependsOn element voor Hallo virtuele Machines is ingesteld op een te`storagecopy`.</span><span class="sxs-lookup"><span data-stu-id="5d67b-171">Notice that hello copy element has name set too`storagecopy` and hello dependsOn element for hello Virtual Machines is also set too`storagecopy`.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        },
        {
            "apiVersion": "2015-06-15", 
            "type": "Microsoft.Compute/virtualMachines", 
            "name": "[concat('VM', uniqueString(resourceGroup().id))]",  
            "dependsOn": ["storagecopy"],
            ...
        }
    ],
    "outputs": {}
}
```

## <a name="create-multiple-instances-of-a-child-resource"></a><span data-ttu-id="5d67b-172">Meerdere exemplaren van een onderliggende resource maken</span><span class="sxs-lookup"><span data-stu-id="5d67b-172">Create multiple instances of a child resource</span></span>
<span data-ttu-id="5d67b-173">U kunt een lus kopie niet gebruiken voor een onderliggende resource.</span><span class="sxs-lookup"><span data-stu-id="5d67b-173">You cannot use a copy loop for a child resource.</span></span> <span data-ttu-id="5d67b-174">toocreate meerdere exemplaren van een resource die u doorgaans als definiëren in een andere resource genest, moet u in plaats daarvan maken die resource als een resource op het hoogste niveau.</span><span class="sxs-lookup"><span data-stu-id="5d67b-174">toocreate multiple instances of a resource that you typically define as nested within another resource, you must instead create that resource as a top-level resource.</span></span> <span data-ttu-id="5d67b-175">U definiëren Hallo relatie met de Hallo bovenliggende resource via Hallo type en de naam eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="5d67b-175">You define hello relationship with hello parent resource through hello type and name properties.</span></span>

<span data-ttu-id="5d67b-176">Stel bijvoorbeeld dat u doorgaans een gegevensset definiëren als een onderliggende bron binnen een gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="5d67b-176">For example, suppose you typically define a dataset as a child resource within a data factory.</span></span>

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
    "resources": [
    {
        "type": "datasets",
        "name": "exampleDataSet",
        "dependsOn": [
            "exampleDataFactory"
        ],
        ...
    }
}]
```

<span data-ttu-id="5d67b-177">toocreate meerdere exemplaren van gegevenssets, verplaatst u het buiten Hallo data factory.</span><span class="sxs-lookup"><span data-stu-id="5d67b-177">toocreate multiple instances of data sets, move it outside of hello data factory.</span></span> <span data-ttu-id="5d67b-178">Hallo gegevensset moet zich op hetzelfde niveau als Hallo gegevensfactory hello, maar nog steeds een onderliggende resource van Hallo-gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="5d67b-178">hello dataset must be at hello same level as hello data factory, but it is still a child resource of hello data factory.</span></span> <span data-ttu-id="5d67b-179">U behouden Hallo relatie tussen de gegevensset en data factory via de eigenschappen voor het type en de naam van Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d67b-179">You preserve hello relationship between data set and data factory through hello type and name properties.</span></span> <span data-ttu-id="5d67b-180">Aangezien het type kan niet meer worden afgeleid van de positie in de sjabloon hello, moet u Hallo volledig gekwalificeerd type Hallo indeling opgeven: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span><span class="sxs-lookup"><span data-stu-id="5d67b-180">Since type can no longer be inferred from its position in hello template, you must provide hello fully qualified type in hello format: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span></span>

<span data-ttu-id="5d67b-181">tooestablish een bovenliggende/onderliggende relatie met een exemplaar van de gegevensfactory hello, Geef een naam voor de gegevensset Hallo met Hallo bovenliggende resourcenaam.</span><span class="sxs-lookup"><span data-stu-id="5d67b-181">tooestablish a parent/child relationship with an instance of hello data factory, provide a name for hello data set that includes hello parent resource name.</span></span> <span data-ttu-id="5d67b-182">Gebruik de indeling Hallo: `{parent-resource-name}/{child-resource-name}`.</span><span class="sxs-lookup"><span data-stu-id="5d67b-182">Use hello format: `{parent-resource-name}/{child-resource-name}`.</span></span>  

<span data-ttu-id="5d67b-183">Hallo toont volgende voorbeeld Hallo implementatie:</span><span class="sxs-lookup"><span data-stu-id="5d67b-183">hello following example shows hello implementation:</span></span>

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
},
{
    "type": "Microsoft.DataFactory/datafactories/datasets",
    "name": "[concat('exampleDataFactory', '/', 'exampleDataSet', copyIndex())]",
    "dependsOn": [
        "exampleDataFactory"
    ],
    "copy": { 
        "name": "datasetcopy", 
        "count": "3" 
    } 
    ...
}]
```

## <a name="conditionally-deploy-resource"></a><span data-ttu-id="5d67b-184">Voorwaardelijk resource implementeren</span><span class="sxs-lookup"><span data-stu-id="5d67b-184">Conditionally deploy resource</span></span>

<span data-ttu-id="5d67b-185">toospecify of een resource wordt geïmplementeerd, gebruiken Hallo `condition` element.</span><span class="sxs-lookup"><span data-stu-id="5d67b-185">toospecify whether a resource is deployed, use hello `condition` element.</span></span> <span data-ttu-id="5d67b-186">Hallo-waarde voor dit element wordt omgezet tootrue of ONWAAR.</span><span class="sxs-lookup"><span data-stu-id="5d67b-186">hello value for this element resolves tootrue or false.</span></span> <span data-ttu-id="5d67b-187">Wanneer het Hallo-waarde true is, wordt Hallo resource geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="5d67b-187">When hello value is true, hello resource is deployed.</span></span> <span data-ttu-id="5d67b-188">Wanneer het Hallo-waarde is ingesteld op false, worden Hallo resource wordt niet geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="5d67b-188">When hello value is false, hello resource is not deployed.</span></span> <span data-ttu-id="5d67b-189">Bijvoorbeeld: toospecify of een nieuw opslagaccount wordt geïmplementeerd of een bestaand opslagaccount wordt gebruikt, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5d67b-189">For example, toospecify whether a new storage account is deployed or an existing storage account is used, use:</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="5d67b-190">Zie voor een voorbeeld van het gebruik van een nieuwe of bestaande resourcegroep [nieuwe of bestaande voorwaarde sjabloon](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="5d67b-190">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="5d67b-191">Zie voor een voorbeeld van het gebruik van een wachtwoord of SSH-sleutel toodeploy virtuele machine [gebruikersnaam of SSH voorwaarde sjabloon](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="5d67b-191">For an example of using a password or SSH key toodeploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d67b-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5d67b-192">Next steps</span></span>
* <span data-ttu-id="5d67b-193">Als u toolearn Hallo secties van een sjabloon wilt, Zie [Azure Resource Manager-sjablonen ontwerpen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5d67b-193">If you want toolearn about hello sections of a template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="5d67b-194">toolearn hoe toodeploy uw sjabloon Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="5d67b-194">toolearn how toodeploy your template, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>

