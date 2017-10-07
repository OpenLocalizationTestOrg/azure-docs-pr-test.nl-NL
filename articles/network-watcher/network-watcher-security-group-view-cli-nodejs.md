---
title: de netwerkbeveiliging aaaAnalyze met Azure-netwerk-Watcher beveiliging groepsweergave - Azure CLI 1.0 | Microsoft Docs
description: In dit artikel wordt beschreven hoe toouse Azure CLI 1.0 tooanalyze per virtuele machines voor beveiliging met beveiliging groep weergeven.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a986ff4f-7e0c-4994-95e1-4ac824986500
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 96383a734b94d215d5b0f3d47339e46940d700b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a><span data-ttu-id="513ba-103">De beveiliging van uw virtuele Machine met beveiliging groep weergeven met behulp van Azure CLI 1.0 analyseren</span><span class="sxs-lookup"><span data-stu-id="513ba-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="513ba-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="513ba-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="513ba-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="513ba-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="513ba-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="513ba-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="513ba-107">REST API</span><span class="sxs-lookup"><span data-stu-id="513ba-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="513ba-108">Groep beveiligingsweergave retourneert geconfigureerd en effectieve netwerkbeveiligingsregels die toegepast tooa virtuele machine zijn.</span><span class="sxs-lookup"><span data-stu-id="513ba-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="513ba-109">Deze mogelijkheid is nuttig tooaudit en onderzoeken van Netwerkbeveiligingsgroepen en regels die zijn geconfigureerd op een VM tooensure-verkeer wordt toegestaan of geweigerd correct.</span><span class="sxs-lookup"><span data-stu-id="513ba-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="513ba-110">In dit artikel zien we u hoe tooretrieve Hallo geconfigureerd en een effectieve beveiligingsmethode regels tooa virtuele machine met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="513ba-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using Azure CLI</span></span>

<span data-ttu-id="513ba-111">Dit artikel wordt platformoverschrijdende Azure CLI 1.0 gebruikt die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="513ba-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="513ba-112">Netwerk-Watcher gebruikt momenteel de Azure CLI 1.0 voor CLI-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="513ba-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="513ba-113">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="513ba-113">Before you begin</span></span>

<span data-ttu-id="513ba-114">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="513ba-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="513ba-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="513ba-115">Scenario</span></span>

<span data-ttu-id="513ba-116">Hallo scenario beschreven in dit artikel worden Hallo geconfigureerd en een effectieve beveiligingsmethode regels voor een bepaalde virtuele machine opgehaald.</span><span class="sxs-lookup"><span data-stu-id="513ba-116">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="513ba-117">Een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="513ba-117">Get a VM</span></span>

<span data-ttu-id="513ba-118">Een virtuele machine is vereist toorun hello `vm list` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="513ba-118">A virtual machine is required toorun hello `vm list` cmdlet.</span></span> <span data-ttu-id="513ba-119">Hallo volgende opdracht worden virtuele machinese Hallo in een resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="513ba-119">hello following command lists hello virtual machinese in a resource group:</span></span>

```azurecli
azure vm list -g resourceGroupName
```

<span data-ttu-id="513ba-120">Zodra u Hallo virtuele machine weet, kunt u Hallo `vm show` cmdlet tooget de resource-Id:</span><span class="sxs-lookup"><span data-stu-id="513ba-120">Once you know hello virtual machine, you can use hello `vm show` cmdlet tooget its resource Id:</span></span>

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="513ba-121">Groep beveiligingsweergave ophalen</span><span class="sxs-lookup"><span data-stu-id="513ba-121">Retrieve security group view</span></span>

<span data-ttu-id="513ba-122">de volgende stap Hallo is tooretrieve Hallo beveiliging groep weergave resultaat.</span><span class="sxs-lookup"><span data-stu-id="513ba-122">hello next step is tooretrieve hello security group view result.</span></span> <span data-ttu-id="513ba-123">Toe te voegen Hallo '--json ' vlag Hallo resulteert in json wordt geformatteerd.</span><span class="sxs-lookup"><span data-stu-id="513ba-123">Adding hello "--json" flag will format hello results in json.</span></span>

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-hello-results"></a><span data-ttu-id="513ba-124">Hallo resultaten weergeven</span><span class="sxs-lookup"><span data-stu-id="513ba-124">Viewing hello results</span></span>

<span data-ttu-id="513ba-125">Hallo is volgende voorbeeld een kortere respons van Hallo resultaten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="513ba-125">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="513ba-126">Hallo resultaten weergeven alle Hallo effectieve en toegepaste beveiligingsregels voor verbindingen op Hallo virtuele machine is onderverdeeld in groepen van **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, en  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="513ba-126">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testnic",
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testvm",
          "securityRules": [
            {
              "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/test-nsg/securityRules/default-allow-rdp",
              "protocol": "TCP",
              "sourcePortRange": "*",
              "destinationPortRange": "3389",
              "sourceAddressPrefix": "*",
              "destinationAddressPrefix": "*",
              "access": "Allow",
              "priority": 1000,
              "direction": "Inbound",
              "provisioningState": "Succeeded",
              "name": "default-allow-rdp",
              "etag": "W/\"00000000-0000-0000-0000-000000000000\""
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/networkSecurityGroups//defaultSecurityRules/",
            "description": "Allow inbound traffic from all VMs in VNET",
            "protocol": "*",
            "sourcePortRange": "*",
            "destinationPortRange": "*",
            "sourceAddressPrefix": "VirtualNetwork",
            "destinationAddressPrefix": "VirtualNetwork",
            "access": "Allow",
            "priority": 65000,
            "direction": "Inbound",
            "provisioningState": "Succeeded",
            "name": "AllowVnetInBound"
          }
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="513ba-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="513ba-127">Next steps</span></span>

<span data-ttu-id="513ba-128">Ga naar [controle Netwerkbeveiligingsgroep groepen (NSG) met de netwerk-Watcher](network-watcher-nsg-auditing-powershell.md) toolearn hoe tooautomate validatie van Netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="513ba-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>

<span data-ttu-id="513ba-129">Meer informatie over Hallo beveiligingsregels voor verbindingen die toegepast tooyour netwerkbronnen in via zijn [beveiligingsoverzicht groep weergeven](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="513ba-129">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
