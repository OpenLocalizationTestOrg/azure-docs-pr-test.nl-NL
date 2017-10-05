---
title: Meerdere exemplaren van Azure-resources implementeren | Microsoft Docs
description: Kopieerbewerking en matrices in een Azure Resource Manager-sjabloon gebruiken om te herhalen meerdere keren bij het implementeren van resources.
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
ms.openlocfilehash: ed8e3081d2b2e07938d7cf3aa5f95f6dde81bc66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a><span data-ttu-id="04c6f-103">Implementeren van meerdere exemplaren van een resource of eigenschap in Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="04c6f-103">Deploy multiple instances of a resource or property in Azure Resource Manager templates</span></span>
<span data-ttu-id="04c6f-104">Dit onderwerp leest u hoe u in uw Azure Resource Manager-sjabloon voor het maken van meerdere exemplaren van een resource of meerdere exemplaren van een eigenschap van een resource.</span><span class="sxs-lookup"><span data-stu-id="04c6f-104">This topic shows you how to iterate in your Azure Resource Manager template to create multiple instances of a resource, or multiple instances of a property on a resource.</span></span>

<span data-ttu-id="04c6f-105">Als u Voeg logica toe aan de sjabloon waarmee u wilt kunt opgeven of een resource wordt geïmplementeerd, Zie [voorwaardelijk implementeren resource](#conditionally-deploy-resource).</span><span class="sxs-lookup"><span data-stu-id="04c6f-105">If you need to add logic to your template that enables you to specify whether a resource is deployed, see [Conditionally deploy resource](#conditionally-deploy-resource).</span></span>

## <a name="resource-iteration"></a><span data-ttu-id="04c6f-106">Resource herhaling</span><span class="sxs-lookup"><span data-stu-id="04c6f-106">Resource iteration</span></span>
<span data-ttu-id="04c6f-107">Voor het maken van meerdere exemplaren van een brontype toevoegen een `copy` element aan het brontype.</span><span class="sxs-lookup"><span data-stu-id="04c6f-107">To create multiple instances of a resource type, add a `copy` element to the resource type.</span></span> <span data-ttu-id="04c6f-108">In het element kopiëren, moet u het aantal iteraties en een naam op voor deze lus opgeven.</span><span class="sxs-lookup"><span data-stu-id="04c6f-108">In the copy element, you specify the number of iterations and a name for this loop.</span></span> <span data-ttu-id="04c6f-109">De waarde van count moet een positief geheel getal zijn en mag niet meer dan 800.</span><span class="sxs-lookup"><span data-stu-id="04c6f-109">The count value must be a positive integer and cannot exceed 800.</span></span> <span data-ttu-id="04c6f-110">Resource Manager maakt de resources parallel.</span><span class="sxs-lookup"><span data-stu-id="04c6f-110">Resource Manager creates the resources in parallel.</span></span> <span data-ttu-id="04c6f-111">De volgorde waarin ze zijn gemaakt kan daarom niet worden gegarandeerd.</span><span class="sxs-lookup"><span data-stu-id="04c6f-111">Therefore, the order in which they are created is not guaranteed.</span></span> <span data-ttu-id="04c6f-112">Zie voor informatie over het maken van resources herhaald in de reeks [seriële kopiëren](#serial-copy).</span><span class="sxs-lookup"><span data-stu-id="04c6f-112">To create iterated resources in sequence, see [Serial copy](#serial-copy).</span></span> 

<span data-ttu-id="04c6f-113">De bron voor het maken van meerdere keren wordt gebruikt in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="04c6f-113">The resource to create multiple times takes the following format:</span></span>

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

<span data-ttu-id="04c6f-114">U ziet dat de naam van elke resource bevat de `copyIndex()` functie de huidige herhaling in de lus retourneert.</span><span class="sxs-lookup"><span data-stu-id="04c6f-114">Notice that the name of each resource includes the `copyIndex()` function, which returns the current iteration in the loop.</span></span> <span data-ttu-id="04c6f-115">`copyIndex()`is gebaseerd op nul.</span><span class="sxs-lookup"><span data-stu-id="04c6f-115">`copyIndex()` is zero-based.</span></span> <span data-ttu-id="04c6f-116">Hiertoe het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="04c6f-116">So, the following example:</span></span>

```json
"name": "[concat('storage', copyIndex())]",
```

<span data-ttu-id="04c6f-117">Deze namen maakt:</span><span class="sxs-lookup"><span data-stu-id="04c6f-117">Creates these names:</span></span>

* <span data-ttu-id="04c6f-118">storage0</span><span class="sxs-lookup"><span data-stu-id="04c6f-118">storage0</span></span>
* <span data-ttu-id="04c6f-119">storage1</span><span class="sxs-lookup"><span data-stu-id="04c6f-119">storage1</span></span>
* <span data-ttu-id="04c6f-120">storage2.</span><span class="sxs-lookup"><span data-stu-id="04c6f-120">storage2.</span></span>

<span data-ttu-id="04c6f-121">Als u wilt verschuiven waarde voor de index, kunt u een waarde in de functie copyIndex() doorgeven.</span><span class="sxs-lookup"><span data-stu-id="04c6f-121">To offset the index value, you can pass a value in the copyIndex() function.</span></span> <span data-ttu-id="04c6f-122">Het aantal iteraties om uit te voeren nog steeds is opgegeven in het element kopiëren, maar de waarde van copyIndex wordt gecompenseerd door de opgegeven waarde.</span><span class="sxs-lookup"><span data-stu-id="04c6f-122">The number of iterations to perform is still specified in the copy element, but the value of copyIndex is offset by the specified value.</span></span> <span data-ttu-id="04c6f-123">Hiertoe het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="04c6f-123">So, the following example:</span></span>

```json
"name": "[concat('storage', copyIndex(1))]",
```

<span data-ttu-id="04c6f-124">Deze namen maakt:</span><span class="sxs-lookup"><span data-stu-id="04c6f-124">Creates these names:</span></span>

* <span data-ttu-id="04c6f-125">storage1</span><span class="sxs-lookup"><span data-stu-id="04c6f-125">storage1</span></span>
* <span data-ttu-id="04c6f-126">storage2</span><span class="sxs-lookup"><span data-stu-id="04c6f-126">storage2</span></span>
* <span data-ttu-id="04c6f-127">storage3</span><span class="sxs-lookup"><span data-stu-id="04c6f-127">storage3</span></span>

<span data-ttu-id="04c6f-128">De kopieerbewerking is handig bij het werken met matrices omdat u elk element in de matrix kunt doorlopen.</span><span class="sxs-lookup"><span data-stu-id="04c6f-128">The copy operation is helpful when working with arrays because you can iterate through each element in the array.</span></span> <span data-ttu-id="04c6f-129">Gebruik de `length` functie op de matrix te geven van het aantal iteraties, en `copyIndex` voor het ophalen van de huidige index in de matrix.</span><span class="sxs-lookup"><span data-stu-id="04c6f-129">Use the `length` function on the array to specify the count for iterations, and `copyIndex` to retrieve the current index in the array.</span></span> <span data-ttu-id="04c6f-130">Hiertoe het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="04c6f-130">So, the following example:</span></span>

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

<span data-ttu-id="04c6f-131">Deze namen maakt:</span><span class="sxs-lookup"><span data-stu-id="04c6f-131">Creates these names:</span></span>

* <span data-ttu-id="04c6f-132">storagecontoso</span><span class="sxs-lookup"><span data-stu-id="04c6f-132">storagecontoso</span></span>
* <span data-ttu-id="04c6f-133">storagefabrikam</span><span class="sxs-lookup"><span data-stu-id="04c6f-133">storagefabrikam</span></span>
* <span data-ttu-id="04c6f-134">storagecoho</span><span class="sxs-lookup"><span data-stu-id="04c6f-134">storagecoho</span></span>

## <a name="serial-copy"></a><span data-ttu-id="04c6f-135">Seriële kopiëren</span><span class="sxs-lookup"><span data-stu-id="04c6f-135">Serial copy</span></span>

<span data-ttu-id="04c6f-136">Wanneer u het element kopiëren gebruikt voor het maken van meerdere exemplaren van een resourcetype Resource Manager worden standaard implementeert de instanties parallel.</span><span class="sxs-lookup"><span data-stu-id="04c6f-136">When you use the copy element to create multiple instances of a resource type, Resource Manager, by default, deploys those instances in parallel.</span></span> <span data-ttu-id="04c6f-137">Daarom is het raadzaam om op te geven dat de resources in volgorde worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="04c6f-137">However, you may want to specify that the resources are deployed in sequence.</span></span> <span data-ttu-id="04c6f-138">Bijvoorbeeld bij het bijwerken van een productieomgeving, u kunt dus spreiden van de updates alleen een bepaald aantal op elk gewenst moment worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="04c6f-138">For example, when updating a production environment, you may want to stagger the updates so only a certain number are updated at any one time.</span></span>

<span data-ttu-id="04c6f-139">Resource Manager biedt de eigenschappen voor het kopiëren-element waarmee u kunt meerdere exemplaren opeenvolgend te implementeren.</span><span class="sxs-lookup"><span data-stu-id="04c6f-139">Resource Manager provides properties on the copy element that enable you to serially deploy multiple instances.</span></span> <span data-ttu-id="04c6f-140">Stel in het element kopiëren `mode` naar **seriële** en `batchSize` aan het aantal exemplaren moeten worden geïmplementeerd op een tijdstip.</span><span class="sxs-lookup"><span data-stu-id="04c6f-140">In the copy element, set `mode` to **serial** and `batchSize` to the number of instances to deploy at a time.</span></span> <span data-ttu-id="04c6f-141">Seriële modus maakt Resource Manager met een afhankelijkheid voor eerdere exemplaren in de lus, zodat dit niet één batch gestart totdat de vorige batch is voltooid.</span><span class="sxs-lookup"><span data-stu-id="04c6f-141">With serial mode, Resource Manager creates a dependency on earlier instances in the loop, so it does not start one batch until the previous batch completes.</span></span>

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

<span data-ttu-id="04c6f-142">De eigenschap mode accepteert ook **parallelle**, dit is de standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="04c6f-142">The mode property also accepts **parallel**, which is the default value.</span></span>

<span data-ttu-id="04c6f-143">Als u wilt testen seriële kopiëren zonder dat er feitelijke webbronnen, moet u de volgende sjabloon die wordt geïmplementeerd leeg geneste sjablonen gebruikt:</span><span class="sxs-lookup"><span data-stu-id="04c6f-143">To test serial copy without creating actual resources, use the following template that deploys empty nested templates:</span></span>

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

<span data-ttu-id="04c6f-144">U ziet dat de geneste implementaties in volgorde worden verwerkt in de geschiedenis van de implementatie.</span><span class="sxs-lookup"><span data-stu-id="04c6f-144">In the deployment history, notice that the nested deployments are processed in sequence.</span></span>

![seriële implementatie](./media/resource-group-create-multiple/serial-copy.png)

<span data-ttu-id="04c6f-146">Voor een meer realistische scenario is implementeert het volgende voorbeeld twee instanties op een tijdstip van een Linux-VM uit een geneste sjabloon:</span><span class="sxs-lookup"><span data-stu-id="04c6f-146">For a more realistic scenario, the following example deploys two instances at a time of a Linux VM from a nested template:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for the Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for the Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for the Public IP used to access the Virtual Machine."
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
                "description": "The Ubuntu version for the VM. This will pick a fully patched image of this given Ubuntu version."
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

## <a name="property-iteration"></a><span data-ttu-id="04c6f-147">Eigenschap herhaling</span><span class="sxs-lookup"><span data-stu-id="04c6f-147">Property iteration</span></span>

<span data-ttu-id="04c6f-148">Voor het maken van meerdere waarden voor een eigenschap van een resource, Voeg een `copy` matrix in het element eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="04c6f-148">To create multiple values for a property on a resource, add a `copy` array in the properties element.</span></span> <span data-ttu-id="04c6f-149">Deze matrix bevat objecten en elk object heeft de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="04c6f-149">This array contains objects, and each object has the following properties:</span></span>

* <span data-ttu-id="04c6f-150">naam - de naam van de eigenschap voor het maken van meerdere waarden voor</span><span class="sxs-lookup"><span data-stu-id="04c6f-150">name - the name of the property to create multiple values for</span></span>
* <span data-ttu-id="04c6f-151">aantal - het aantal waarden maken</span><span class="sxs-lookup"><span data-stu-id="04c6f-151">count - the number of values to create</span></span>
* <span data-ttu-id="04c6f-152">invoer - object dat de waarden toewijzen aan de eigenschap bevat</span><span class="sxs-lookup"><span data-stu-id="04c6f-152">input - an object that contains the values to assign to the property</span></span>  

<span data-ttu-id="04c6f-153">Het volgende voorbeeld laat zien hoe om toe te passen `copy` voor de eigenschap dataDisks op een virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="04c6f-153">The following example shows how to apply `copy` to the dataDisks property on a virtual machine:</span></span>

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

<span data-ttu-id="04c6f-154">Merk op dat wanneer u `copyIndex` binnen de herhaling van een eigenschap, moet u de naam van de herhaling opgeven.</span><span class="sxs-lookup"><span data-stu-id="04c6f-154">Notice that when using `copyIndex` inside a property iteration, you must provide the name of the iteration.</span></span> <span data-ttu-id="04c6f-155">U hebt niet de naam gebruikt in combinatie met herhaling van de resource op te geven.</span><span class="sxs-lookup"><span data-stu-id="04c6f-155">You do not have to provide the name when used with resource iteration.</span></span>

<span data-ttu-id="04c6f-156">Resource Manager breidt de `copy` matrix tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="04c6f-156">Resource Manager expands the `copy` array during deployment.</span></span> <span data-ttu-id="04c6f-157">De naam van de matrix, wordt de naam van de eigenschap.</span><span class="sxs-lookup"><span data-stu-id="04c6f-157">The name of the array becomes the name of the property.</span></span> <span data-ttu-id="04c6f-158">De invoerwaarden, worden de objecteigenschappen.</span><span class="sxs-lookup"><span data-stu-id="04c6f-158">The input values become the object properties.</span></span> <span data-ttu-id="04c6f-159">De geïmplementeerde sjabloon als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="04c6f-159">The deployed template becomes:</span></span>

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

<span data-ttu-id="04c6f-160">U kunt resource en de eigenschap iteratie samen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="04c6f-160">You can use resource and property iteration together.</span></span> <span data-ttu-id="04c6f-161">Verwijzing naar de herhaling van de eigenschap met de naam.</span><span class="sxs-lookup"><span data-stu-id="04c6f-161">Reference the property iteration by name.</span></span>

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

<span data-ttu-id="04c6f-162">U kunt alleen één exemplaar element opnemen in de eigenschappen voor elke resource.</span><span class="sxs-lookup"><span data-stu-id="04c6f-162">You can only include one copy element in the properties for each resource.</span></span> <span data-ttu-id="04c6f-163">Als u een lus herhaling voor meer dan één eigenschap, meerdere objecten definiëren die in de matrix kopiëren.</span><span class="sxs-lookup"><span data-stu-id="04c6f-163">To specify an iteration loop for more than one property, define multiple objects in the copy array.</span></span> <span data-ttu-id="04c6f-164">Elk object wordt afzonderlijk herhaald.</span><span class="sxs-lookup"><span data-stu-id="04c6f-164">Each object is iterated separately.</span></span> <span data-ttu-id="04c6f-165">Om bijvoorbeeld te maken van meerdere exemplaren van zowel de `frontendIPConfigurations` eigenschap en de `loadBalancingRules` eigenschap op een load balancer beide objecten definiëren die in een element met één exemplaar:</span><span class="sxs-lookup"><span data-stu-id="04c6f-165">For example, to create multiple instances of both the `frontendIPConfigurations` property and the `loadBalancingRules` property on a load balancer, define both objects in a single copy element:</span></span> 

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

## <a name="depend-on-resources-in-a-loop"></a><span data-ttu-id="04c6f-166">Afhankelijk zijn van bronnen in een lus</span><span class="sxs-lookup"><span data-stu-id="04c6f-166">Depend on resources in a loop</span></span>
<span data-ttu-id="04c6f-167">U opgeven dat een resource na een andere resource wordt geïmplementeerd met behulp van de `dependsOn` element.</span><span class="sxs-lookup"><span data-stu-id="04c6f-167">You specify that a resource is deployed after another resource by using the `dependsOn` element.</span></span> <span data-ttu-id="04c6f-168">Geef de naam van de lus kopie in het element dependsOn voor het implementeren van een resource die afhankelijk zijn van de verzameling van resources in een lus.</span><span class="sxs-lookup"><span data-stu-id="04c6f-168">To deploy a resource that depends on the collection of resources in a loop, provide the name of the copy loop in the dependsOn element.</span></span> <span data-ttu-id="04c6f-169">Het volgende voorbeeld laat zien hoe drie storage-accounts te implementeren voordat u de virtuele Machine implementeert.</span><span class="sxs-lookup"><span data-stu-id="04c6f-169">The following example shows how to deploy three storage accounts before deploying the Virtual Machine.</span></span> <span data-ttu-id="04c6f-170">De definitie van de volledige virtuele Machine niet wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="04c6f-170">The full Virtual Machine definition is not shown.</span></span> <span data-ttu-id="04c6f-171">U ziet dat het element kopiëren naam ingesteld op `storagecopy` en het element dependsOn voor de virtuele Machines ook is ingesteld op `storagecopy`.</span><span class="sxs-lookup"><span data-stu-id="04c6f-171">Notice that the copy element has name set to `storagecopy` and the dependsOn element for the Virtual Machines is also set to `storagecopy`.</span></span>

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

## <a name="create-multiple-instances-of-a-child-resource"></a><span data-ttu-id="04c6f-172">Meerdere exemplaren van een onderliggende resource maken</span><span class="sxs-lookup"><span data-stu-id="04c6f-172">Create multiple instances of a child resource</span></span>
<span data-ttu-id="04c6f-173">U kunt een lus kopie niet gebruiken voor een onderliggende resource.</span><span class="sxs-lookup"><span data-stu-id="04c6f-173">You cannot use a copy loop for a child resource.</span></span> <span data-ttu-id="04c6f-174">Voor het maken van meerdere exemplaren van een resource die u normaal gesproken als genest in een andere resource definiëren, moet u in plaats daarvan die resource maken als een resource op het hoogste niveau.</span><span class="sxs-lookup"><span data-stu-id="04c6f-174">To create multiple instances of a resource that you typically define as nested within another resource, you must instead create that resource as a top-level resource.</span></span> <span data-ttu-id="04c6f-175">U definieert de relatie met de bovenliggende resource via de eigenschappen van het type en de naam.</span><span class="sxs-lookup"><span data-stu-id="04c6f-175">You define the relationship with the parent resource through the type and name properties.</span></span>

<span data-ttu-id="04c6f-176">Stel bijvoorbeeld dat u doorgaans een gegevensset definiëren als een onderliggende bron binnen een gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="04c6f-176">For example, suppose you typically define a dataset as a child resource within a data factory.</span></span>

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

<span data-ttu-id="04c6f-177">Voor het maken van meerdere exemplaren van gegevenssets, verplaatst u het buiten de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="04c6f-177">To create multiple instances of data sets, move it outside of the data factory.</span></span> <span data-ttu-id="04c6f-178">De gegevensset moet zich op hetzelfde niveau als de gegevensfactory, maar nog steeds een onderliggende resource van de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="04c6f-178">The dataset must be at the same level as the data factory, but it is still a child resource of the data factory.</span></span> <span data-ttu-id="04c6f-179">U behouden de relatie tussen de gegevensset en data factory via de eigenschappen van het type en de naam.</span><span class="sxs-lookup"><span data-stu-id="04c6f-179">You preserve the relationship between data set and data factory through the type and name properties.</span></span> <span data-ttu-id="04c6f-180">Aangezien het type kan niet meer worden afgeleid van de positie in de sjabloon, moet u de volledig gekwalificeerde type in de indeling opgeven: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span><span class="sxs-lookup"><span data-stu-id="04c6f-180">Since type can no longer be inferred from its position in the template, you must provide the fully qualified type in the format: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span></span>

<span data-ttu-id="04c6f-181">Geef een naam voor de gegevensset met de naam van de bovenliggende resource voor het opzetten van een bovenliggende/onderliggende relatie met een exemplaar van de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="04c6f-181">To establish a parent/child relationship with an instance of the data factory, provide a name for the data set that includes the parent resource name.</span></span> <span data-ttu-id="04c6f-182">Gebruik de indeling: `{parent-resource-name}/{child-resource-name}`.</span><span class="sxs-lookup"><span data-stu-id="04c6f-182">Use the format: `{parent-resource-name}/{child-resource-name}`.</span></span>  

<span data-ttu-id="04c6f-183">Het volgende voorbeeld ziet u de implementatie:</span><span class="sxs-lookup"><span data-stu-id="04c6f-183">The following example shows the implementation:</span></span>

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

## <a name="conditionally-deploy-resource"></a><span data-ttu-id="04c6f-184">Voorwaardelijk resource implementeren</span><span class="sxs-lookup"><span data-stu-id="04c6f-184">Conditionally deploy resource</span></span>

<span data-ttu-id="04c6f-185">Als u wilt opgeven of een resource wordt geïmplementeerd, gebruiken de `condition` element.</span><span class="sxs-lookup"><span data-stu-id="04c6f-185">To specify whether a resource is deployed, use the `condition` element.</span></span> <span data-ttu-id="04c6f-186">De waarde voor dit element wordt omgezet in true of false.</span><span class="sxs-lookup"><span data-stu-id="04c6f-186">The value for this element resolves to true or false.</span></span> <span data-ttu-id="04c6f-187">Wanneer de waarde true is, wordt de bron wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="04c6f-187">When the value is true, the resource is deployed.</span></span> <span data-ttu-id="04c6f-188">Wanneer de waarde false is, wordt de resource wordt niet geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="04c6f-188">When the value is false, the resource is not deployed.</span></span> <span data-ttu-id="04c6f-189">Bijvoorbeeld: als u wilt opgeven of een nieuw opslagaccount wordt geïmplementeerd of een bestaand opslagaccount wordt gebruikt, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="04c6f-189">For example, to specify whether a new storage account is deployed or an existing storage account is used, use:</span></span>

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

<span data-ttu-id="04c6f-190">Zie voor een voorbeeld van het gebruik van een nieuwe of bestaande resourcegroep [nieuwe of bestaande voorwaarde sjabloon](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="04c6f-190">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="04c6f-191">Zie voor een voorbeeld van het gebruik van een wachtwoord of SSH-sleutel voor het implementeren van virtuele machine [gebruikersnaam of SSH voorwaarde sjabloon](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="04c6f-191">For an example of using a password or SSH key to deploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04c6f-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="04c6f-192">Next steps</span></span>
* <span data-ttu-id="04c6f-193">Als u wilt voor meer informatie over de secties van een sjabloon, Zie [Azure Resource Manager-sjablonen ontwerpen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="04c6f-193">If you want to learn about the sections of a template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="04c6f-194">Zie voor meer informatie over het implementeren van uw sjabloon, [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="04c6f-194">To learn how to deploy your template, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>

