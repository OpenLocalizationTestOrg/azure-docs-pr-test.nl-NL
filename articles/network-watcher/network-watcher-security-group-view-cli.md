---
title: Netwerkbeveiliging met Azure-netwerk-Watcher beveiliging groepsweergave - Azure CLI 2.0 analyseren | Microsoft Docs
description: In dit artikel wordt beschreven hoe Azure CLI 2.0 gebruiken voor het analyseren van de beveiliging van een virtuele machines met beveiliging groep weergeven.
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
ms.openlocfilehash: 1756e14819e3b7c79361c193413a1fcd7f24a4e6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-20"></a><span data-ttu-id="49238-103">De beveiliging van uw virtuele Machine met beveiliging groep weergeven met behulp van Azure CLI 2.0 analyseren</span><span class="sxs-lookup"><span data-stu-id="49238-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="49238-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="49238-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="49238-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="49238-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="49238-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="49238-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="49238-107">REST API</span><span class="sxs-lookup"><span data-stu-id="49238-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="49238-108">Groep beveiligingsweergave retourneert geconfigureerd en effectieve netwerkbeveiligingsregels die worden toegepast op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="49238-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="49238-109">Deze mogelijkheid is handig om te controleren en onderzoeken van Netwerkbeveiligingsgroepen en -regels die zijn geconfigureerd op een virtuele machine om ervoor te zorgen verkeer wordt toegestaan of geweigerd correct.</span><span class="sxs-lookup"><span data-stu-id="49238-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="49238-110">In dit artikel wordt beschreven hoe u voor het ophalen van de geconfigureerde en doeltreffende beveiligingsregels voor verbindingen met een virtuele machine met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="49238-110">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using Azure CLI</span></span>


<span data-ttu-id="49238-111">Dit artikel wordt de volgende generatie CLI gebruikt voor de resource management-implementatiemodel, Azure CLI 2.0, die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="49238-111">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="49238-112">Als u wilt de stappen in dit artikel uitvoert, moet u [installeren van de Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="49238-112">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="49238-113">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="49238-113">Before you begin</span></span>

<span data-ttu-id="49238-114">Dit scenario wordt ervan uitgegaan dat u de stappen in al hebt gevolgd [maken van een netwerk-Watcher](network-watcher-create.md) voor het maken van een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="49238-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="49238-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="49238-115">Scenario</span></span>

<span data-ttu-id="49238-116">Het scenario beschreven in dit artikel worden de geconfigureerde en doeltreffende beveiligingsregels voor een bepaalde virtuele machine opgehaald.</span><span class="sxs-lookup"><span data-stu-id="49238-116">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="49238-117">Een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="49238-117">Get a VM</span></span>

<span data-ttu-id="49238-118">Een virtuele machine is vereist om de `vm list` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="49238-118">A virtual machine is required to run the `vm list` cmdlet.</span></span> <span data-ttu-id="49238-119">De volgende opdracht worden de virtuele machines in een resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="49238-119">The following command lists the virtual machines in a resource group:</span></span>

```azurecli
az vm list -resource-group resourceGroupName
```

<span data-ttu-id="49238-120">Zodra u weet dat de virtuele machine, kunt u de `vm show` cmdlet ophalen van de resource-Id:</span><span class="sxs-lookup"><span data-stu-id="49238-120">Once you know the virtual machine, you can use the `vm show` cmdlet to get its resource Id:</span></span>

```azurecli
az vm show -resource-group resourceGroupName -name virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="49238-121">Groep beveiligingsweergave ophalen</span><span class="sxs-lookup"><span data-stu-id="49238-121">Retrieve security group view</span></span>

<span data-ttu-id="49238-122">De volgende stap is het resultaat van beveiliging groep weergave ophalen.</span><span class="sxs-lookup"><span data-stu-id="49238-122">The next step is to retrieve the security group view result.</span></span>

```azurecli
az network watcher show-security-group-view --resource-group resourceGroupName --vm vmName
```

## <a name="viewing-the-results"></a><span data-ttu-id="49238-123">De resultaten weergeven</span><span class="sxs-lookup"><span data-stu-id="49238-123">Viewing the results</span></span>

<span data-ttu-id="49238-124">Het volgende voorbeeld wordt een kortere antwoord van de resultaten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="49238-124">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="49238-125">De resultaten weergeven alle beveiligingsregels voor de effectieve en toegepaste op de virtuele machine onderverdeeld in groepen van **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, en **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="49238-125">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="49238-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="49238-126">Next steps</span></span>

<span data-ttu-id="49238-127">Ga naar [controle Netwerkbeveiligingsgroep groepen (NSG) met de netwerk-Watcher](network-watcher-nsg-auditing-powershell.md) voor informatie over het automatiseren van validatie van Netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="49238-127">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>

<span data-ttu-id="49238-128">Meer informatie over de beveiligingsregels voor verbindingen die worden toegepast op uw netwerkbronnen in via [beveiligingsoverzicht groep weergeven](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="49238-128">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
