---
title: de netwerkbeveiliging aaaAnalyze met Azure-netwerk-Watcher beveiliging groepsweergave - Azure CLI 2.0 | Microsoft Docs
description: In dit artikel wordt beschreven hoe toouse Azure CLI 2.0 tooanalyze per virtuele machines voor beveiliging met beveiliging groep weergeven.
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
ms.openlocfilehash: 31a4cd628f54d7548f495251fd275f099e79a060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-20"></a><span data-ttu-id="aabbd-103">De beveiliging van uw virtuele Machine met beveiliging groep weergeven met behulp van Azure CLI 2.0 analyseren</span><span class="sxs-lookup"><span data-stu-id="aabbd-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="aabbd-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aabbd-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="aabbd-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="aabbd-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="aabbd-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="aabbd-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="aabbd-107">REST API</span><span class="sxs-lookup"><span data-stu-id="aabbd-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="aabbd-108">Groep beveiligingsweergave retourneert geconfigureerd en effectieve netwerkbeveiligingsregels die toegepast tooa virtuele machine zijn.</span><span class="sxs-lookup"><span data-stu-id="aabbd-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="aabbd-109">Deze mogelijkheid is nuttig tooaudit en onderzoeken van Netwerkbeveiligingsgroepen en regels die zijn geconfigureerd op een VM tooensure-verkeer wordt toegestaan of geweigerd correct.</span><span class="sxs-lookup"><span data-stu-id="aabbd-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="aabbd-110">In dit artikel zien we u hoe tooretrieve Hallo geconfigureerd en een effectieve beveiligingsmethode regels tooa virtuele machine met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="aabbd-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using Azure CLI</span></span>


<span data-ttu-id="aabbd-111">In dit artikel gebruikt de volgende generatie CLI voor Hallo resource management-implementatiemodel, Azure CLI 2.0, die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="aabbd-111">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="aabbd-112">tooperform hello stappen in dit artikel, moet u te[hello Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI) installeren](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="aabbd-112">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="aabbd-113">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="aabbd-113">Before you begin</span></span>

<span data-ttu-id="aabbd-114">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="aabbd-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="aabbd-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="aabbd-115">Scenario</span></span>

<span data-ttu-id="aabbd-116">Hallo scenario beschreven in dit artikel worden Hallo geconfigureerd en een effectieve beveiligingsmethode regels voor een bepaalde virtuele machine opgehaald.</span><span class="sxs-lookup"><span data-stu-id="aabbd-116">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="aabbd-117">Een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="aabbd-117">Get a VM</span></span>

<span data-ttu-id="aabbd-118">Een virtuele machine is vereist toorun hello `vm list` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="aabbd-118">A virtual machine is required toorun hello `vm list` cmdlet.</span></span> <span data-ttu-id="aabbd-119">Hallo volgende opdracht worden Hallo virtuele machines in een resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="aabbd-119">hello following command lists hello virtual machines in a resource group:</span></span>

```azurecli
az vm list -resource-group resourceGroupName
```

<span data-ttu-id="aabbd-120">Zodra u Hallo virtuele machine weet, kunt u Hallo `vm show` cmdlet tooget de resource-Id:</span><span class="sxs-lookup"><span data-stu-id="aabbd-120">Once you know hello virtual machine, you can use hello `vm show` cmdlet tooget its resource Id:</span></span>

```azurecli
az vm show -resource-group resourceGroupName -name virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="aabbd-121">Groep beveiligingsweergave ophalen</span><span class="sxs-lookup"><span data-stu-id="aabbd-121">Retrieve security group view</span></span>

<span data-ttu-id="aabbd-122">de volgende stap Hallo is tooretrieve Hallo beveiliging groep weergave resultaat.</span><span class="sxs-lookup"><span data-stu-id="aabbd-122">hello next step is tooretrieve hello security group view result.</span></span>

```azurecli
az network watcher show-security-group-view --resource-group resourceGroupName --vm vmName
```

## <a name="viewing-hello-results"></a><span data-ttu-id="aabbd-123">Hallo resultaten weergeven</span><span class="sxs-lookup"><span data-stu-id="aabbd-123">Viewing hello results</span></span>

<span data-ttu-id="aabbd-124">Hallo is volgende voorbeeld een kortere respons van Hallo resultaten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="aabbd-124">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="aabbd-125">Hallo resultaten weergeven alle Hallo effectieve en toegepaste beveiligingsregels voor verbindingen op Hallo virtuele machine is onderverdeeld in groepen van **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, en  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="aabbd-125">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
      "resourceGroup": "{resourceGroupName}",
      "securityRuleAssociations": {
        "defaultSecurityRules": [
          {
            "access": "Allow",
            "description": "Allow inbound traffic from all VMs in VNET",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "*",
            "direction": "Inbound",
            "etag": null,
            "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups//providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/AllowVnetInBound",
            "name": "AllowVnetInBound",
            "priority": 65000,
            "protocol": "*",
            "provisioningState": "Succeeded",
            "resourceGroup": "",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "*"
          }...
        ],
        "effectiveSecurityRules": [
          {
            "access": "Deny",
            "destinationAddressPrefix": "*",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": null,
            "expandedSourceAddressPrefix": null,
            "name": "DefaultOutboundDenyAll",
            "priority": 65500,
            "protocol": "All",
            "sourceAddressPrefix": "*",
            "sourcePortRange": "0-65535"
          },
          {
            "access": "Allow",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "expandedSourceAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "name": "DefaultRule_AllowVnetOutBound",
            "priority": 65000,
            "protocol": "All",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "0-65535"
          },...
        ],
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "resourceGroup": "{resourceGroupName}",
          "securityRules": [
            {
              "access": "Allow",
              "description": null,
              "destinationAddressPrefix": "*",
              "destinationPortRange": "3389",
              "direction": "Inbound",
              "etag": "W/\"efb606c1-2d54-475a-ab20-da3f80393577\"",
              "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "name": "default-allow-rdp",
              "priority": 1000,
              "protocol": "TCP",
              "provisioningState": "Succeeded",
              "resourceGroup": "{resourceGroupName}",
              "sourceAddressPrefix": "*",
              "sourcePortRange": "*"
            }
          ]
        },
        "subnetAssociation": null
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="aabbd-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aabbd-126">Next steps</span></span>

<span data-ttu-id="aabbd-127">Ga naar [controle Netwerkbeveiligingsgroep groepen (NSG) met de netwerk-Watcher](network-watcher-nsg-auditing-powershell.md) toolearn hoe tooautomate validatie van Netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="aabbd-127">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>

<span data-ttu-id="aabbd-128">Meer informatie over Hallo beveiligingsregels voor verbindingen die toegepast tooyour netwerkbronnen in via zijn [beveiligingsoverzicht groep weergeven](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="aabbd-128">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
