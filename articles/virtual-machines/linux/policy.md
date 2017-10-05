---
title: Beveiliging met beleidsregels op Linux-machines in Azure afdwingen | Microsoft Docs
description: Het toepassen van een beleid voor een Azure Resource Manager virtuele Linux-Machine
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 06778ab4-f8ff-4eed-ae10-26a276fc3faa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: singhkay
ms.openlocfilehash: 58eaab4fa03afc1e6a5e38bef691cce62a921ea9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="apply-policies-to-linux-vms-with-azure-resource-manager"></a><span data-ttu-id="ae267-103">Beleid toepassen op Linux VM's met Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ae267-103">Apply policies to Linux VMs with Azure Resource Manager</span></span>
<span data-ttu-id="ae267-104">Een organisatie kan met behulp van beleid afdwingen verschillende conventies en regels in de hele onderneming.</span><span class="sxs-lookup"><span data-stu-id="ae267-104">By using policies, an organization can enforce various conventions and rules throughout the enterprise.</span></span> <span data-ttu-id="ae267-105">Afdwinging van het gewenste gedrag kunt risico's te beperken tijdens bijdragen aan het succes van de organisatie.</span><span class="sxs-lookup"><span data-stu-id="ae267-105">Enforcement of the desired behavior can help mitigate risk while contributing to the success of the organization.</span></span> <span data-ttu-id="ae267-106">In dit artikel wordt beschreven hoe u Azure Resource Manager-beleid kunt gebruiken voor het definiëren van het gewenste gedrag voor virtuele Machines die uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="ae267-106">In this article, we describe how you can use Azure Resource Manager policies to define the desired behavior for your organization's Virtual Machines.</span></span>

<span data-ttu-id="ae267-107">Zie voor een inleiding tot beleidsregels, [beleid gebruiken voor het beheren van resources en toegangsbeheer](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ae267-107">For an introduction to policies, see [Use Policy to manage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="ae267-108">Toegestane virtuele Machines</span><span class="sxs-lookup"><span data-stu-id="ae267-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="ae267-109">Om ervoor te zorgen dat virtuele machines voor uw organisatie compatibel met een toepassing zijn, kunt u de toegestane besturingssystemen beperken.</span><span class="sxs-lookup"><span data-stu-id="ae267-109">To ensure that virtual machines for your organization are compatible with an application, you can restrict the permitted operating systems.</span></span> <span data-ttu-id="ae267-110">In het volgende voorbeeld voor het beleid kunt u alleen Ubuntu 14.04.2-LTS virtuele Machines worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ae267-110">In the following policy example, you allow only Ubuntu 14.04.2-LTS Virtual Machines to be created.</span></span>

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
                "Canonical"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "UbuntuServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "14.04.2-LTS"
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

<span data-ttu-id="ae267-111">Een jokerteken gebruiken voor het wijzigen van het vorige beleid zodat geen Ubuntu LTS afbeelding:</span><span class="sxs-lookup"><span data-stu-id="ae267-111">Use a wild card to modify the preceding policy to allow any Ubuntu LTS image:</span></span> 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

<span data-ttu-id="ae267-112">Zie voor meer informatie over Beleidsvelden [beleid aliassen](../../azure-resource-manager/resource-manager-policy.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="ae267-112">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="ae267-113">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="ae267-113">Managed disks</span></span>

<span data-ttu-id="ae267-114">Als u wilt het gebruik van beheerde schijven, gebruikt u het volgende beleid:</span><span class="sxs-lookup"><span data-stu-id="ae267-114">To require the use of managed disks, use the following policy:</span></span>

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

## <a name="images-for-virtual-machines"></a><span data-ttu-id="ae267-115">Installatiekopieën voor virtuele Machines</span><span class="sxs-lookup"><span data-stu-id="ae267-115">Images for Virtual Machines</span></span>

<span data-ttu-id="ae267-116">Uit veiligheidsoverwegingen kunt u vereisen dat alleen goedgekeurde aangepaste installatiekopieën in uw omgeving zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="ae267-116">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="ae267-117">Kunt u ofwel de resourcegroep die de goedgekeurde installatiekopieën bevat, of de specifieke goedgekeurd installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="ae267-117">You can specify either the resource group that contains the approved images, or the specific approved images.</span></span>

<span data-ttu-id="ae267-118">Het volgende voorbeeld is vereist voor installatiekopieën van een goedgekeurde resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="ae267-118">The following example requires images from an approved resource group:</span></span>

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

<span data-ttu-id="ae267-119">Het volgende voorbeeld wordt de goedgekeurde installatiekopie-id's:</span><span class="sxs-lookup"><span data-stu-id="ae267-119">The following example specifies the approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="ae267-120">Uitbreidingen van de virtuele Machine</span><span class="sxs-lookup"><span data-stu-id="ae267-120">Virtual Machine extensions</span></span>

<span data-ttu-id="ae267-121">U kunt informatie over het gebruik van bepaalde soorten extensies verbieden.</span><span class="sxs-lookup"><span data-stu-id="ae267-121">You may want to forbid usage of certain types of extensions.</span></span> <span data-ttu-id="ae267-122">Bijvoorbeeld, een uitbreiding mogelijk niet compatibel met bepaalde afbeeldingen aangepaste virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ae267-122">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="ae267-123">Het volgende voorbeeld laat zien hoe een bepaalde extensie blokkeren.</span><span class="sxs-lookup"><span data-stu-id="ae267-123">The following example shows how to block a specific extension.</span></span> <span data-ttu-id="ae267-124">Uitgever en type worden gebruikt om te bepalen welke extensie te blokkeren.</span><span class="sxs-lookup"><span data-stu-id="ae267-124">It uses publisher and type to determine which extension to block.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="ae267-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ae267-125">Next steps</span></span>
* <span data-ttu-id="ae267-126">Na het definiëren van een beleidsregel (zoals weergegeven in de voorgaande voorbeelden), moet u de beleidsdefinitie maken en toewijzen aan een bereik.</span><span class="sxs-lookup"><span data-stu-id="ae267-126">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="ae267-127">Het bereik mag een abonnement, resourcegroep of resource.</span><span class="sxs-lookup"><span data-stu-id="ae267-127">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="ae267-128">Als u wilt toewijzen beleid via de portal, Zie [gebruik Azure-portal toewijzen en beheren van bronbeleid](../../azure-resource-manager/resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ae267-128">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="ae267-129">Als u wilt toewijzen beleid via REST API, PowerShell of Azure CLI, Zie [toewijzen en beheren van beleid via script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="ae267-129">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="ae267-130">Zie voor een inleiding tot bronbeleid, [Resource overzicht](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ae267-130">For an introduction to resource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="ae267-131">Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="ae267-131">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
