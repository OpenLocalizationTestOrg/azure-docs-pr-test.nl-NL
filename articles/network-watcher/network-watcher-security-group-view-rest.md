---
title: de netwerkbeveiliging aaaAnalyze met Azure-netwerk-Watcher beveiliging groepsweergave - REST-API | Microsoft Docs
description: In dit artikel wordt beschreven hoe toouse PowerShell tooanalyze per virtuele machines voor beveiliging met beveiliging groep weergeven.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a2f418fe-f5d2-43ed-8dc3-df0ed2a4d4ac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 0858a64a9454816e05f06dadb9536ad0c755e90e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a><span data-ttu-id="68bbf-103">De beveiliging van uw virtuele Machine met beveiliging groep weergeven met behulp van REST-API analyseren</span><span class="sxs-lookup"><span data-stu-id="68bbf-103">Analyze your Virtual Machine security with Security Group View using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="68bbf-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="68bbf-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="68bbf-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="68bbf-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="68bbf-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="68bbf-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="68bbf-107">REST API</span><span class="sxs-lookup"><span data-stu-id="68bbf-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="68bbf-108">Groep beveiligingsweergave retourneert geconfigureerd en effectieve netwerkbeveiligingsregels die toegepast tooa virtuele machine zijn.</span><span class="sxs-lookup"><span data-stu-id="68bbf-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="68bbf-109">Deze mogelijkheid is nuttig tooaudit en onderzoeken van Netwerkbeveiligingsgroepen en regels die zijn geconfigureerd op een VM tooensure-verkeer wordt toegestaan of geweigerd correct.</span><span class="sxs-lookup"><span data-stu-id="68bbf-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="68bbf-110">In dit artikel zien we u hoe tooretrieve Hallo effectieve en toegepaste beveiligingsregels tooa virtuele machine met behulp van REST-API</span><span class="sxs-lookup"><span data-stu-id="68bbf-110">In this article, we show you how tooretrieve hello effective and applied security rules tooa virtual machine using REST API</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="68bbf-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="68bbf-111">Before you begin</span></span>

<span data-ttu-id="68bbf-112">In dit scenario kunt u Hallo Rest-API voor netwerk-Watcher tooget Hallo beveiliging groepsweergave aanroepen voor een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="68bbf-112">In this scenario, you call hello Network Watcher Rest API tooget hello security group view for a virtual machine.</span></span> <span data-ttu-id="68bbf-113">ARMclient is gebruikte toocall Hallo REST-API met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68bbf-113">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="68bbf-114">ARMClient is gevonden op chocolatey op [ARMClient op Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="68bbf-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="68bbf-115">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="68bbf-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="68bbf-116">Hallo scenario wordt ervan uitgegaan dat een resourcegroep met een geldige virtuele machine toobe gebruikt bestaat.</span><span class="sxs-lookup"><span data-stu-id="68bbf-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="68bbf-117">Scenario</span><span class="sxs-lookup"><span data-stu-id="68bbf-117">Scenario</span></span>

<span data-ttu-id="68bbf-118">Hallo scenario beschreven in dit artikel haalt Hallo effectieve en toegepaste beveiligingsregels voor een bepaalde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="68bbf-118">hello scenario covered in this article retrieves hello effective and applied security rules for a given virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="68bbf-119">Meld u aan met ARMClient</span><span class="sxs-lookup"><span data-stu-id="68bbf-119">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="68bbf-120">Een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="68bbf-120">Retrieve a virtual machine</span></span>

<span data-ttu-id="68bbf-121">Uitvoeren van script tooreturn een virtuele machineThe na Hallo, code de volgende variabelen moet:</span><span class="sxs-lookup"><span data-stu-id="68bbf-121">Run hello following script tooreturn a virtual machineThe following code needs variables:</span></span>

- <span data-ttu-id="68bbf-122">**subscriptionId** -Hallo abonnements-id kan ook worden opgehaald met Hallo **Get-AzureRMSubscription** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="68bbf-122">**subscriptionId** - hello subscription id can also be retrieved with hello **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="68bbf-123">**resourceGroupName** - hello naam van een resourcegroep die virtuele machines bevatten.</span><span class="sxs-lookup"><span data-stu-id="68bbf-123">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="68bbf-124">Hallo informatie die nodig is Hallo **id** onder Hallo type `Microsoft.Compute/virtualMachines` in het antwoord, zoals in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="68bbf-124">hello information that is needed is hello **id** under hello type `Microsoft.Compute/virtualMachines` in response, as seen in hello following example:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft
.Network/networkInterfaces/{nicName}"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Com
pute/virtualMachines/{vmName}/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute
/virtualMachines/{vmName}",
      "name": "{vmName}"
    }
  ]
}
```

## <a name="get-security-group-view-for-virtual-machine"></a><span data-ttu-id="68bbf-125">Groepsweergave beveiliging voor virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="68bbf-125">Get security group view for virtual machine</span></span>

<span data-ttu-id="68bbf-126">Hallo volgende voorbeeld aanvragen Hallo beveiliging groepsweergave van een bepaalde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="68bbf-126">hello following example requests hello security group view of a targeted virtual machine.</span></span> <span data-ttu-id="68bbf-127">Hallo-resultaten van dit voorbeeld kunnen worden gebruikt toocompare toohello regels en beveiliging die zijn gedefinieerd door Hallo oorspronkelijke toolook configuratieafwijkingen.</span><span class="sxs-lookup"><span data-stu-id="68bbf-127">hello results from this example can be used toocompare toohello rules and security defined by hello origination toolook for configuration drift.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName

$requestBody = @"
{
    'targetResourceId': '${targetUri}'

}
"@
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/securityGroupView?api-version=2016-12-01" $requestBody -verbose
```

## <a name="view-hello-response"></a><span data-ttu-id="68bbf-128">Hallo-antwoord weergeven</span><span class="sxs-lookup"><span data-stu-id="68bbf-128">View hello response</span></span>

<span data-ttu-id="68bbf-129">Hallo volgende voorbeeld is Hallo-antwoord geretourneerd door de voorgaande opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="68bbf-129">hello following sample is hello response returned from hello preceding command.</span></span> <span data-ttu-id="68bbf-130">Hallo resultaten weergeven alle Hallo effectieve en toegepaste beveiligingsregels voor verbindingen op Hallo virtuele machine is onderverdeeld in groepen van **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, en  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="68bbf-130">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json

{
  "networkInterfaces": [
    {
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "securityRules": [
            {
              "name": "default-allow-rdp",
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
              "properties": {
                "provisioningState": "Succeeded",
                "protocol": "TCP",
                "sourcePortRange": "*",
                "destinationPortRange": "3389",
                "sourceAddressPrefix": "*",
                "destinationAddressPrefix": "*",
                "access": "Allow",
                "priority": 1000,
                "direction": "Inbound"
              }
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "name": "AllowVnetInBound",
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/",
            "properties": {
              "provisioningState": "Succeeded",
              "description": "Allow inbound traffic from all VMs in VNET",
              "protocol": "*",
              "sourcePortRange": "*",
              "destinationPortRange": "*",
              "sourceAddressPrefix": "VirtualNetwork",
              "destinationAddressPrefix": "VirtualNetwork",
              "access": "Allow",
              "priority": 65000,
              "direction": "Inbound"
            }
          },
          ...
        ],
        "effectiveSecurityRules": [
          {
            "name": "DefaultOutboundDenyAll",
            "protocol": "All",
            "sourcePortRange": "0-65535",
            "destinationPortRange": "0-65535",
            "sourceAddressPrefix": "*",
            "destinationAddressPrefix": "*",
            "access": "Deny",
            "priority": 65500,
            "direction": "Outbound"
          },
          ...
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="68bbf-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="68bbf-131">Next steps</span></span>

<span data-ttu-id="68bbf-132">Ga naar [controle Netwerkbeveiligingsgroep groepen (NSG) met de netwerk-Watcher](network-watcher-security-group-view-powershell.md) toolearn hoe tooautomate validatie van Netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="68bbf-132">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-security-group-view-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>


