---
title: aaaEnforce beveiliging met beleidsregels op Windows-machines in Azure | Microsoft Docs
description: Hoe tooapply een beleid tooan Windows virtuele Machine van Azure Resource Manager
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0b71ba54-01db-43ad-9bca-8ab358ae141b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: kasing
ms.openlocfilehash: b31c8a03ecf8eed6a929f97fe4146ea14364404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="apply-policies-toowindows-vms-with-azure-resource-manager"></a><span data-ttu-id="0142c-103">Toepassen van beleid tooWindows VM's met Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0142c-103">Apply policies tooWindows VMs with Azure Resource Manager</span></span>
<span data-ttu-id="0142c-104">Met behulp van beleid, kan een organisatie verschillende conventies en regels in de onderneming Hallo afdwingen.</span><span class="sxs-lookup"><span data-stu-id="0142c-104">By using policies, an organization can enforce various conventions and rules throughout hello enterprise.</span></span> <span data-ttu-id="0142c-105">Afdwinging van Hallo gewenst gedrag kunt risico's te beperken tijdens toohello succes van Hallo organisatie bij te dragen.</span><span class="sxs-lookup"><span data-stu-id="0142c-105">Enforcement of hello desired behavior can help mitigate risk while contributing toohello success of hello organization.</span></span> <span data-ttu-id="0142c-106">In dit artikel wordt beschreven hoe u Azure Resource Manager beleid toodefine Hallo gewenst gedrag kunt gebruiken voor virtuele Machines die uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="0142c-106">In this article, we describe how you can use Azure Resource Manager policies toodefine hello desired behavior for your organization’s Virtual Machines.</span></span>

<span data-ttu-id="0142c-107">Zie voor een toopolicies inleiding [beleid toomanage resources en toegang beheren](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="0142c-107">For an introduction toopolicies, see [Use Policy toomanage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="0142c-108">Toegestane virtuele Machines</span><span class="sxs-lookup"><span data-stu-id="0142c-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="0142c-109">tooensure dat virtuele machines voor uw organisatie compatibel met een toepassing zijn, kunt u besturingssystemen toegestaan Hallo beperken.</span><span class="sxs-lookup"><span data-stu-id="0142c-109">tooensure that virtual machines for your organization are compatible with an application, you can restrict hello permitted operating systems.</span></span> <span data-ttu-id="0142c-110">In Hallo voorbeeld van een beleid te volgen, kunt u alleen virtuele Machines van Windows Server 2012 R2 Datacenter toobe gemaakt:</span><span class="sxs-lookup"><span data-stu-id="0142c-110">In hello following policy example, you allow only Windows Server 2012 R2 Datacenter Virtual Machines toobe created:</span></span>

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
                "MicrosoftWindowsServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "WindowsServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "2012-R2-Datacenter"
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

<span data-ttu-id="0142c-111">Gebruik een jokerteken toomodify Hallo beleid tooallow voorafgaand aan de installatiekopie van een Windows Server Datacenter:</span><span class="sxs-lookup"><span data-stu-id="0142c-111">Use a wild card toomodify hello preceding policy tooallow any Windows Server Datacenter image:</span></span>

```json
{
  "field": "Microsoft.Compute/imageSku",
  "like": "*Datacenter"
}
```

<span data-ttu-id="0142c-112">Gebruik dragen toomodify Hallo beleid tooallow voorafgaand aan een Windows Server 2012 R2 Datacenter of hoger installatiekopie:</span><span class="sxs-lookup"><span data-stu-id="0142c-112">Use anyOf toomodify hello preceding policy tooallow any Windows Server 2012 R2 Datacenter or higher image:</span></span>

```json
{
  "anyOf": [
    {
      "field": "Microsoft.Compute/imageSku",
      "like": "2012-R2-Datacenter*"
    },
    {
      "field": "Microsoft.Compute/imageSku",
      "like": "2016-Datacenter*"
    }
  ]
}
```

<span data-ttu-id="0142c-113">Zie voor meer informatie over Beleidsvelden [beleid aliassen](../../azure-resource-manager/resource-manager-policy.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="0142c-113">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="0142c-114">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="0142c-114">Managed disks</span></span>

<span data-ttu-id="0142c-115">toorequire hello gebruik van beheerde schijven gebruik Hallo volgende beleid:</span><span class="sxs-lookup"><span data-stu-id="0142c-115">toorequire hello use of managed disks, use hello following policy:</span></span>

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

## <a name="images-for-virtual-machines"></a><span data-ttu-id="0142c-116">Installatiekopieën voor virtuele Machines</span><span class="sxs-lookup"><span data-stu-id="0142c-116">Images for Virtual Machines</span></span>

<span data-ttu-id="0142c-117">Uit veiligheidsoverwegingen kunt u vereisen dat alleen goedgekeurde aangepaste installatiekopieën in uw omgeving zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="0142c-117">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="0142c-118">U kunt Hallo resourcegroep waarin Hallo goedgekeurd afbeeldingen of specifieke goedgekeurde installatiekopieën Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="0142c-118">You can specify either hello resource group that contains hello approved images, or hello specific approved images.</span></span>

<span data-ttu-id="0142c-119">Hallo volgt vereist installatiekopieën van een goedgekeurde resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="0142c-119">hello following example requires images from an approved resource group:</span></span>

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

<span data-ttu-id="0142c-120">Hallo volgende voorbeeld worden goedgekeurd Hallo installatiekopie id's:</span><span class="sxs-lookup"><span data-stu-id="0142c-120">hello following example specifies hello approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="0142c-121">Uitbreidingen van de virtuele Machine</span><span class="sxs-lookup"><span data-stu-id="0142c-121">Virtual Machine extensions</span></span>

<span data-ttu-id="0142c-122">U kunt tooforbid informatie over het gebruik van bepaalde soorten uitbreidingen.</span><span class="sxs-lookup"><span data-stu-id="0142c-122">You may want tooforbid usage of certain types of extensions.</span></span> <span data-ttu-id="0142c-123">Bijvoorbeeld, een uitbreiding mogelijk niet compatibel met bepaalde afbeeldingen aangepaste virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0142c-123">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="0142c-124">Hallo volgende voorbeeld wordt getoond hoe tooblock een bepaalde extensie.</span><span class="sxs-lookup"><span data-stu-id="0142c-124">hello following example shows how tooblock a specific extension.</span></span> <span data-ttu-id="0142c-125">Gebruikt deze uitgever en type toodetermine welke tooblock extensie.</span><span class="sxs-lookup"><span data-stu-id="0142c-125">It uses publisher and type toodetermine which extension tooblock.</span></span>

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


## <a name="azure-hybrid-use-benefit"></a><span data-ttu-id="0142c-126">Azure hybride gebruik Benefit</span><span class="sxs-lookup"><span data-stu-id="0142c-126">Azure Hybrid Use Benefit</span></span>

<span data-ttu-id="0142c-127">Wanneer u een on-premises-licentie hebt, kunt u Hallo licentiekosten op uw virtuele machines kunt opslaan.</span><span class="sxs-lookup"><span data-stu-id="0142c-127">When you have an on-premise license, you can save hello license fee on your virtual machines.</span></span> <span data-ttu-id="0142c-128">Wanneer u geen Hallo-licentie hebt, moet u Hallo optie verbieden.</span><span class="sxs-lookup"><span data-stu-id="0142c-128">When you don't have hello license, you should forbid hello option.</span></span> <span data-ttu-id="0142c-129">Hallo beleid na verbiedt informatie over het gebruik van Azure hybride gebruik voordeel (AHUB):</span><span class="sxs-lookup"><span data-stu-id="0142c-129">hello following policy forbids usage of Azure Hybrid Use Benefit (AHUB):</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in":[ "Microsoft.Compute/virtualMachines","Microsoft.Compute/VirtualMachineScaleSets"]
            },
            {
                "field": "Microsoft.Compute/licenseType",
                "exists": true
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="0142c-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0142c-130">Next steps</span></span>
* <span data-ttu-id="0142c-131">Na het definiëren van een beleidsregel (zoals weergegeven in de voorgaande voorbeelden Hallo), u moet toocreate hello beleidsdefinitie en wijs deze tooa bereik.</span><span class="sxs-lookup"><span data-stu-id="0142c-131">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="0142c-132">Hallo bereik mag een abonnement, resourcegroep of resource.</span><span class="sxs-lookup"><span data-stu-id="0142c-132">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="0142c-133">tooassign beleid via de portal hello, Zie [gebruik Azure portal tooassign en beheren van bronbeleid](../../azure-resource-manager/resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0142c-133">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="0142c-134">tooassign beleid via REST API, PowerShell of Azure CLI, Zie [toewijzen en beheren van beleid via script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="0142c-134">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="0142c-135">Zie voor een inleiding tooresource beleidsregels, [Resource overzicht](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="0142c-135">For an introduction tooresource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="0142c-136">Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="0142c-136">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
