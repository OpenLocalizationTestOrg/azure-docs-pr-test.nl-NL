---
title: Beveiliging met beleidsregels op Windows-machines in Azure afdwingen | Microsoft Docs
description: Het toepassen van een beleid voor een Azure Resource Manager virtuele Windows-computer
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
ms.openlocfilehash: 246f5958478fd6d9afc9ba990413ab08429bd25d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="apply-policies-to-windows-vms-with-azure-resource-manager"></a><span data-ttu-id="f1a5d-103">Beleid toepassen op Windows-VM's met Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f1a5d-103">Apply policies to Windows VMs with Azure Resource Manager</span></span>
<span data-ttu-id="f1a5d-104">Een organisatie kan met behulp van beleid afdwingen verschillende conventies en regels in de hele onderneming.</span><span class="sxs-lookup"><span data-stu-id="f1a5d-104">By using policies, an organization can enforce various conventions and rules throughout the enterprise.</span></span> <span data-ttu-id="f1a5d-105">Afdwinging van het gewenste gedrag kunt risico's te beperken tijdens bijdragen aan het succes van de organisatie.</span><span class="sxs-lookup"><span data-stu-id="f1a5d-105">Enforcement of the desired behavior can help mitigate risk while contributing to the success of the organization.</span></span> <span data-ttu-id="f1a5d-106">In dit artikel wordt beschreven hoe u Azure Resource Manager-beleid kunt gebruiken voor het definiëren van het gewenste gedrag voor virtuele Machines die uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="f1a5d-106">In this article, we describe how you can use Azure Resource Manager policies to define the desired behavior for your organization’s Virtual Machines.</span></span>

<span data-ttu-id="f1a5d-107">Zie voor een inleiding tot beleidsregels, [beleid gebruiken voor het beheren van resources en toegangsbeheer](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="f1a5d-107">For an introduction to policies, see [Use Policy to manage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="f1a5d-108">Toegestane virtuele Machines</span><span class="sxs-lookup"><span data-stu-id="f1a5d-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="f1a5d-109">Om ervoor te zorgen dat virtuele machines voor uw organisatie compatibel met een toepassing zijn, kunt u de toegestane besturingssystemen beperken.</span><span class="sxs-lookup"><span data-stu-id="f1a5d-109">To ensure that virtual machines for your organization are compatible with an application, you can restrict the permitted operating systems.</span></span> <span data-ttu-id="f1a5d-110">U kunt alleen Windows Server 2012 R2 Datacenter virtuele Machines worden gemaakt in het volgende voorbeeld voor het beleid:</span><span class="sxs-lookup"><span data-stu-id="f1a5d-110">In the following policy example, you allow only Windows Server 2012 R2 Datacenter Virtual Machines to be created:</span></span>

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

<span data-ttu-id="f1a5d-111">Gebruik een jokerteken voor het wijzigen van het vorige beleid voor het toestaan van een installatiekopie van Windows Server Datacenter:</span><span class="sxs-lookup"><span data-stu-id="f1a5d-111">Use a wild card to modify the preceding policy to allow any Windows Server Datacenter image:</span></span>

```json
{
  "field": "Microsoft.Compute/imageSku",
  "like": "*Datacenter"
}
```

<span data-ttu-id="f1a5d-112">Gebruik dragen om het voorgaande beleid aanpassen om een Windows Server 2012 R2 Datacenter of hoger installatiekopie toe te staan:</span><span class="sxs-lookup"><span data-stu-id="f1a5d-112">Use anyOf to modify the preceding policy to allow any Windows Server 2012 R2 Datacenter or higher image:</span></span>

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

<span data-ttu-id="f1a5d-113">Zie voor meer informatie over Beleidsvelden [beleid aliassen](../../azure-resource-manager/resource-manager-policy.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="f1a5d-113">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="f1a5d-114">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="f1a5d-114">Managed disks</span></span>

<span data-ttu-id="f1a5d-115">Als u wilt het gebruik van beheerde schijven, gebruikt u het volgende beleid:</span><span class="sxs-lookup"><span data-stu-id="f1a5d-115">To require the use of managed disks, use the following policy:</span></span>

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

## <a name="images-for-virtual-machines"></a><span data-ttu-id="f1a5d-116">Installatiekopieën voor virtuele Machines</span><span class="sxs-lookup"><span data-stu-id="f1a5d-116">Images for Virtual Machines</span></span>

<span data-ttu-id="f1a5d-117">Uit veiligheidsoverwegingen kunt u vereisen dat alleen goedgekeurde aangepaste installatiekopieën in uw omgeving zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f1a5d-117">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="f1a5d-118">Kunt u ofwel de resourcegroep die de goedgekeurde installatiekopieën bevat, of de specifieke goedgekeurd installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="f1a5d-118">You can specify either the resource group that contains the approved images, or the specific approved images.</span></span>

<span data-ttu-id="f1a5d-119">Het volgende voorbeeld is vereist voor installatiekopieën van een goedgekeurde resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="f1a5d-119">The following example requires images from an approved resource group:</span></span>

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

<span data-ttu-id="f1a5d-120">Het volgende voorbeeld wordt de goedgekeurde installatiekopie-id's:</span><span class="sxs-lookup"><span data-stu-id="f1a5d-120">The following example specifies the approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="f1a5d-121">Uitbreidingen van de virtuele Machine</span><span class="sxs-lookup"><span data-stu-id="f1a5d-121">Virtual Machine extensions</span></span>

<span data-ttu-id="f1a5d-122">U kunt informatie over het gebruik van bepaalde soorten extensies verbieden.</span><span class="sxs-lookup"><span data-stu-id="f1a5d-122">You may want to forbid usage of certain types of extensions.</span></span> <span data-ttu-id="f1a5d-123">Bijvoorbeeld, een uitbreiding mogelijk niet compatibel met bepaalde afbeeldingen aangepaste virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f1a5d-123">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="f1a5d-124">Het volgende voorbeeld laat zien hoe een bepaalde extensie blokkeren.</span><span class="sxs-lookup"><span data-stu-id="f1a5d-124">The following example shows how to block a specific extension.</span></span> <span data-ttu-id="f1a5d-125">Uitgever en type worden gebruikt om te bepalen welke extensie te blokkeren.</span><span class="sxs-lookup"><span data-stu-id="f1a5d-125">It uses publisher and type to determine which extension to block.</span></span>

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


## <a name="azure-hybrid-use-benefit"></a><span data-ttu-id="f1a5d-126">Azure hybride gebruik Benefit</span><span class="sxs-lookup"><span data-stu-id="f1a5d-126">Azure Hybrid Use Benefit</span></span>

<span data-ttu-id="f1a5d-127">Wanneer u een on-premises-licentie hebt, kunt u de licentiekosten op uw virtuele machines kunt opslaan.</span><span class="sxs-lookup"><span data-stu-id="f1a5d-127">When you have an on-premise license, you can save the license fee on your virtual machines.</span></span> <span data-ttu-id="f1a5d-128">Wanneer u de licentie niet hebt, moet u de optie verbieden.</span><span class="sxs-lookup"><span data-stu-id="f1a5d-128">When you don't have the license, you should forbid the option.</span></span> <span data-ttu-id="f1a5d-129">Het volgende beleid verbiedt informatie over het gebruik van Azure hybride gebruik voordeel (AHUB):</span><span class="sxs-lookup"><span data-stu-id="f1a5d-129">The following policy forbids usage of Azure Hybrid Use Benefit (AHUB):</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f1a5d-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f1a5d-130">Next steps</span></span>
* <span data-ttu-id="f1a5d-131">Na het definiëren van een beleidsregel (zoals weergegeven in de voorgaande voorbeelden), moet u de beleidsdefinitie maken en toewijzen aan een bereik.</span><span class="sxs-lookup"><span data-stu-id="f1a5d-131">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="f1a5d-132">Het bereik mag een abonnement, resourcegroep of resource.</span><span class="sxs-lookup"><span data-stu-id="f1a5d-132">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="f1a5d-133">Als u wilt toewijzen beleid via de portal, Zie [gebruik Azure-portal toewijzen en beheren van bronbeleid](../../azure-resource-manager/resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f1a5d-133">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="f1a5d-134">Als u wilt toewijzen beleid via REST API, PowerShell of Azure CLI, Zie [toewijzen en beheren van beleid via script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="f1a5d-134">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="f1a5d-135">Zie voor een inleiding tot bronbeleid, [Resource overzicht](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="f1a5d-135">For an introduction to resource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="f1a5d-136">Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="f1a5d-136">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
