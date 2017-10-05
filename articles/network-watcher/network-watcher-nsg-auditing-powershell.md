---
title: NSG controle met Azure-Watcher netwerkbeveiliging groepsweergave automatiseren | Microsoft Docs
description: Deze pagina vindt u instructies voor het configureren van de controle van een Netwerkbeveiligingsgroep
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 78a01bcf-74fe-402a-9812-285f3501f877
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a91da330e677c85f16f6f4e506613576b6507d7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a><span data-ttu-id="f97ce-103">Automatiseren NSG controle met Azure-Watcher netwerkbeveiliging groep weergeven</span><span class="sxs-lookup"><span data-stu-id="f97ce-103">Automate NSG auditing with Azure Network Watcher Security group view</span></span>

<span data-ttu-id="f97ce-104">Klanten zijn vaak moeten de beveiligingsstatus van hun infrastructuur te controleren.</span><span class="sxs-lookup"><span data-stu-id="f97ce-104">Customers are often faced with the challenge of verifying the security posture of their infrastructure.</span></span> <span data-ttu-id="f97ce-105">Deze uitdaging gaat niet anders zijn voor hun virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="f97ce-105">This challenge is no different for their VMs in Azure.</span></span> <span data-ttu-id="f97ce-106">Het is belangrijk om een soortgelijke beveiligingsprofiel op basis van de Netwerkbeveiligingsgroep (NSG) regels toegepast.</span><span class="sxs-lookup"><span data-stu-id="f97ce-106">It is important to have a similar security profile based on the Network Security Group (NSG) rules applied.</span></span> <span data-ttu-id="f97ce-107">De weergave van de groep beveiliging gebruikt, krijgt u nu de lijst met regels voor een virtuele machine binnen een NSG wordt toegepast.</span><span class="sxs-lookup"><span data-stu-id="f97ce-107">Using the Security Group View, you can now get the list of rules applied to a VM within an NSG.</span></span> <span data-ttu-id="f97ce-108">U kunt definiëren van een gouden NSG-beveiligingsprofiel en beveiliging groepsweergave een wekelijkse uitgebracht initiëren en vergelijken van de uitvoer naar het gouden profiel en een rapport maken.</span><span class="sxs-lookup"><span data-stu-id="f97ce-108">You can define a golden NSG security profile and initiate Security Group View on a weekly cadence and compare the output to the golden profile and create a report.</span></span> <span data-ttu-id="f97ce-109">Op deze manier kunt u identificeren met gemak alle virtuele machines die niet met het voorgeschreven beveiligingsprofiel overeen komen.</span><span class="sxs-lookup"><span data-stu-id="f97ce-109">This way you can identify with ease all the VMs that do not conform to the prescribed security profile.</span></span>

<span data-ttu-id="f97ce-110">Als u niet bekend met Netwerkbeveiligingsgroepen bent, gaat u naar [beveiligingsoverzicht van het netwerk](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="f97ce-110">If you are unfamiliar with Network Security Groups, visit [Network Security Overview](../virtual-network/virtual-networks-nsg.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f97ce-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="f97ce-111">Before you begin</span></span>

<span data-ttu-id="f97ce-112">In dit scenario vergelijken u met een bekende goede basis voor de beveiliging groep weergaveresultaten geretourneerd voor een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f97ce-112">In this scenario, you compare a known good baseline to the security group view results returned for a virtual machine.</span></span>

<span data-ttu-id="f97ce-113">Dit scenario wordt ervan uitgegaan dat u de stappen in al hebt gevolgd [maken van een netwerk-Watcher](network-watcher-create.md) voor het maken van een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="f97ce-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="f97ce-114">Het scenario wordt ervan uitgegaan dat er een resourcegroep met een geldige virtuele machine bestaat om te worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f97ce-114">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="f97ce-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="f97ce-115">Scenario</span></span>

<span data-ttu-id="f97ce-116">Het scenario beschreven in dit artikel wordt de weergave van de groep beveiliging voor een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f97ce-116">The scenario covered in this article gets the security group view for a virtual machine.</span></span>

<span data-ttu-id="f97ce-117">U wordt in dit scenario:</span><span class="sxs-lookup"><span data-stu-id="f97ce-117">In this scenario, you will:</span></span>

- <span data-ttu-id="f97ce-118">Ophalen van een bekende goede regelset</span><span class="sxs-lookup"><span data-stu-id="f97ce-118">Retrieve a known good rule set</span></span>
- <span data-ttu-id="f97ce-119">Ophalen van een virtuele machine met de Rest-API</span><span class="sxs-lookup"><span data-stu-id="f97ce-119">Retrieve a virtual machine with Rest API</span></span>
- <span data-ttu-id="f97ce-120">Groepsweergave beveiliging voor virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="f97ce-120">Get security group view for virtual machine</span></span>
- <span data-ttu-id="f97ce-121">Antwoord evalueren</span><span class="sxs-lookup"><span data-stu-id="f97ce-121">Evaluate Response</span></span>

## <a name="retrieve-rule-set"></a><span data-ttu-id="f97ce-122">Regelset ophalen</span><span class="sxs-lookup"><span data-stu-id="f97ce-122">Retrieve rule set</span></span>

<span data-ttu-id="f97ce-123">De eerste stap in dit voorbeeld is voor gebruik met een bestaande basislijn.</span><span class="sxs-lookup"><span data-stu-id="f97ce-123">The first step in this example is to work with an existing baseline.</span></span> <span data-ttu-id="f97ce-124">Het volgende voorbeeld is sommige json opgehaald uit een bestaande Netwerkbeveiligingsgroep met behulp van de `Get-AzureRmNetworkSecurityGroup` cmdlet die wordt gebruikt als de basislijn voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f97ce-124">The following example is some json extracted from an existing Network Security Group using the `Get-AzureRmNetworkSecurityGroup` cmdlet that is used as the baseline for this example.</span></span>

```json
[
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "3389",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1000,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "default-allow-rdp",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/default-allow-rdp"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "111",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1010,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "MyRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/MyRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "112",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1020,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "My2ndRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/My2ndRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "5672",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Deny",
        "Priority":  1030,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "ThisRuleNeedsToStay",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/ThisRuleNeedsToStay"
    }
]
```

## <a name="convert-rule-set-to-powershell-objects"></a><span data-ttu-id="f97ce-125">Regelset converteren naar objecten met PowerShell</span><span class="sxs-lookup"><span data-stu-id="f97ce-125">Convert rule set to PowerShell objects</span></span>

<span data-ttu-id="f97ce-126">We zijn een json-bestand dat eerder is gemaakt met de regels die naar verwachting wordt op de Netwerkbeveiligingsgroep voor dit voorbeeld lezen in deze stap.</span><span class="sxs-lookup"><span data-stu-id="f97ce-126">In this step, we are reading a json file that was created earlier with the rules that are expected to be on the Network Security Group for this example.</span></span>

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a><span data-ttu-id="f97ce-127">Ophalen van netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="f97ce-127">Retrieve Network Watcher</span></span>

<span data-ttu-id="f97ce-128">De volgende stap is het exemplaar van de netwerk-Watcher ophalen.</span><span class="sxs-lookup"><span data-stu-id="f97ce-128">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="f97ce-129">De `$networkWatcher` variabele wordt doorgegeven aan de `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f97ce-129">The `$networkWatcher` variable is passed to the `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="f97ce-130">Een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="f97ce-130">Get a VM</span></span>

<span data-ttu-id="f97ce-131">Een virtuele machine is vereist om de `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet tegen.</span><span class="sxs-lookup"><span data-stu-id="f97ce-131">A virtual machine is required to run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="f97ce-132">Het volgende voorbeeld wordt een VM-object.</span><span class="sxs-lookup"><span data-stu-id="f97ce-132">The following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="f97ce-133">Groep beveiligingsweergave ophalen</span><span class="sxs-lookup"><span data-stu-id="f97ce-133">Retrieve security group view</span></span>

<span data-ttu-id="f97ce-134">De volgende stap is het resultaat van beveiliging groep weergave ophalen.</span><span class="sxs-lookup"><span data-stu-id="f97ce-134">The next step is to retrieve the security group view result.</span></span> <span data-ttu-id="f97ce-135">Dit resultaat wordt vergeleken met de 'basislijn' json die eerder is aangegeven.</span><span class="sxs-lookup"><span data-stu-id="f97ce-135">This result is compared to the "baseline" json that was shown earlier.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-the-results"></a><span data-ttu-id="f97ce-136">De resultaten analyseren</span><span class="sxs-lookup"><span data-stu-id="f97ce-136">Analyzing the results</span></span>

<span data-ttu-id="f97ce-137">Het antwoord worden gegroepeerd per netwerkinterfaces.</span><span class="sxs-lookup"><span data-stu-id="f97ce-137">The response is grouped by Network interfaces.</span></span> <span data-ttu-id="f97ce-138">De verschillende typen regels geretourneerd geldig zijn en de standaardinstellingen van de beveiligingsregels voor verbindingen.</span><span class="sxs-lookup"><span data-stu-id="f97ce-138">The different types of rules returned are effective and default security rules.</span></span> <span data-ttu-id="f97ce-139">Het resultaat is verder uitgesplitst hoe deze wordt toegepast, op een subnet of een virtuele NIC.</span><span class="sxs-lookup"><span data-stu-id="f97ce-139">The result is further broken down by how it is applied, either on a subnet or a virtual NIC.</span></span>

<span data-ttu-id="f97ce-140">De volgende PowerShell-script worden de resultaten van de weergave van de groep beveiliging aan een bestaande uitvoer van een NSG vergeleken.</span><span class="sxs-lookup"><span data-stu-id="f97ce-140">The following PowerShell script compares the results of the Security Group View to an existing output of an NSG.</span></span> <span data-ttu-id="f97ce-141">Het volgende voorbeeld wordt een eenvoudig voorbeeld van hoe de resultaten kunnen worden vergeleken met `Compare-Object` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f97ce-141">The following example is a simple example of how the results can be compared with `Compare-Object` cmdlet.</span></span>

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

<span data-ttu-id="f97ce-142">Het volgende voorbeeld is het resultaat.</span><span class="sxs-lookup"><span data-stu-id="f97ce-142">The following example is the result.</span></span> <span data-ttu-id="f97ce-143">U ziet twee van de regels die zijn in de eerste regel ingesteld zijn niet aanwezig in de vergelijking.</span><span class="sxs-lookup"><span data-stu-id="f97ce-143">You can see two of the rules that were in the first rule set were not present in the comparison.</span></span>

```
Name                     : My2ndRuleDoNotDelete
Description              : 
Protocol                 : *
SourcePortRange          : *
DestinationPortRange     : 112
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Allow
Priority                 : 1020
Direction                : Inbound
SideIndicator            : <=

Name                     : ThisRuleNeedsToStay
Description              : 
Protocol                 : TCP
SourcePortRange          : *
DestinationPortRange     : 5672
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Deny
Priority                 : 1030
Direction                : Inbound
SideIndicator            : <=
```

## <a name="next-steps"></a><span data-ttu-id="f97ce-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f97ce-144">Next steps</span></span>

<span data-ttu-id="f97ce-145">Als de instellingen zijn gewijzigd, Zie [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) voor het opsporen van de groep en beveiliging netwerkbeveiligingsregels die betrokken zijn.</span><span class="sxs-lookup"><span data-stu-id="f97ce-145">If settings have been changed, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are in question.</span></span>













