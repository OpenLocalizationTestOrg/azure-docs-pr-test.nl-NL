---
title: de netwerkbeveiliging aaaAnalyze met Azure-netwerk-Watcher beveiliging groepsweergave - PowerShell | Microsoft Docs
description: In dit artikel wordt beschreven hoe toouse PowerShell tooanalyze per virtuele machines voor beveiliging met beveiliging groep weergeven.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04e76b49-6a1b-4d0f-9a9b-51cf2f4df5a2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5e1990d97899bd8585025ec13dd556ab2e034c3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a><span data-ttu-id="62523-103">De beveiliging van uw virtuele Machine met beveiliging groep weergeven met behulp van PowerShell analyseren</span><span class="sxs-lookup"><span data-stu-id="62523-103">Analyze your Virtual Machine security with Security Group View using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="62523-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="62523-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="62523-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="62523-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="62523-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="62523-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="62523-107">REST API</span><span class="sxs-lookup"><span data-stu-id="62523-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="62523-108">Groep beveiligingsweergave retourneert geconfigureerd en effectieve netwerkbeveiligingsregels die toegepast tooa virtuele machine zijn.</span><span class="sxs-lookup"><span data-stu-id="62523-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="62523-109">Deze mogelijkheid is nuttig tooaudit en onderzoeken van Netwerkbeveiligingsgroepen en regels die zijn geconfigureerd op een VM tooensure-verkeer wordt toegestaan of geweigerd correct.</span><span class="sxs-lookup"><span data-stu-id="62523-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="62523-110">In dit artikel zien we u hoe tooretrieve Hallo geconfigureerd en een effectieve beveiligingsmethode regels tooa virtuele machine met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="62523-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using PowerShell</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="62523-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="62523-111">Before you begin</span></span>

<span data-ttu-id="62523-112">In dit scenario voert u Hallo `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet tooretrieve Hallo beveiligingsgegevens-regel.</span><span class="sxs-lookup"><span data-stu-id="62523-112">In this scenario, you run hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet tooretrieve hello security rule information.</span></span>

<span data-ttu-id="62523-113">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="62523-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="62523-114">Scenario</span><span class="sxs-lookup"><span data-stu-id="62523-114">Scenario</span></span>

<span data-ttu-id="62523-115">Hallo scenario beschreven in dit artikel worden Hallo geconfigureerd en een effectieve beveiligingsmethode regels voor een bepaalde virtuele machine opgehaald.</span><span class="sxs-lookup"><span data-stu-id="62523-115">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="62523-116">Ophalen van netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="62523-116">Retrieve Network Watcher</span></span>

<span data-ttu-id="62523-117">de eerste stap Hallo is tooretrieve Hallo netwerk-Watcher-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="62523-117">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="62523-118">Deze variabele wordt doorgegeven toohello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="62523-118">This variable is passed toohello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a><span data-ttu-id="62523-119">Een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="62523-119">Get a VM</span></span>

<span data-ttu-id="62523-120">Een virtuele machine is vereist toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet tegen.</span><span class="sxs-lookup"><span data-stu-id="62523-120">A virtual machine is required toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="62523-121">Hallo volgende voorbeeld wordt een VM-object.</span><span class="sxs-lookup"><span data-stu-id="62523-121">hello following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="62523-122">Groep beveiligingsweergave ophalen</span><span class="sxs-lookup"><span data-stu-id="62523-122">Retrieve security group view</span></span>

<span data-ttu-id="62523-123">de volgende stap Hallo is tooretrieve Hallo beveiliging groep weergave resultaat.</span><span class="sxs-lookup"><span data-stu-id="62523-123">hello next step is tooretrieve hello security group view result.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-hello-results"></a><span data-ttu-id="62523-124">Hallo resultaten weergeven</span><span class="sxs-lookup"><span data-stu-id="62523-124">Viewing hello results</span></span>

<span data-ttu-id="62523-125">Hallo is volgende voorbeeld een kortere respons van Hallo resultaten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="62523-125">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="62523-126">Hallo resultaten weergeven alle Hallo effectieve en toegepaste beveiligingsregels voor verbindingen op Hallo virtuele machine is onderverdeeld in groepen van **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, en  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="62523-126">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```
NetworkInterfaces : [
                      {
                        "NetworkInterfaceSecurityRules": [
                          {
                            "Name": "default-allow-rdp",
                            "Etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
                            "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/securityRules/default-allow-rdp",
                            "Protocol": "TCP",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "3389",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "Access": "Allow",
                            "Priority": 1000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "DefaultSecurityRules": [
                          {
                            "Name": "AllowVnetInBound",
                            "Id": "/subscriptions00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/defaultSecurityRules/",
                            "Description": "Allow inbound traffic from all VMs in VNET",
                            "Protocol": "*",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "*",
                            "SourceAddressPrefix": "VirtualNetwork",
                            "DestinationAddressPrefix": "VirtualNetwork",
                            "Access": "Allow",
                            "Priority": 65000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "EffectiveSecurityRules": [
                          {
                            "Name": "DefaultOutboundDenyAll",
                            "Protocol": "All",
                            "SourcePortRange": "0-65535",
                            "DestinationPortRange": "0-65535",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "ExpandedSourceAddressPrefix": [],
                            "ExpandedDestinationAddressPrefix": [],
                            "Access": "Deny",
                            "Priority": 65500,
                            "Direction": "Outbound"
                          },
                          ...
                        ]
                      }
                    ]
```

## <a name="next-steps"></a><span data-ttu-id="62523-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="62523-127">Next steps</span></span>

<span data-ttu-id="62523-128">Ga naar [controle Netwerkbeveiligingsgroep groepen (NSG) met de netwerk-Watcher](network-watcher-nsg-auditing-powershell.md) toolearn hoe tooautomate validatie van Netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="62523-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>


