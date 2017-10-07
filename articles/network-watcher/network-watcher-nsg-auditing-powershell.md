---
title: aaaAutomate NSG controle met Azure-Watcher netwerkbeveiliging groepsweergave | Microsoft Docs
description: Deze pagina bevat instructies voor het tooconfigure controle van een Netwerkbeveiligingsgroep
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
ms.openlocfilehash: 24fc418c433fceaf55a74b7c3b0e354dc46c8729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a>Automatiseren NSG controle met Azure-Watcher netwerkbeveiliging groep weergeven

Klanten moeten vaak Hallo uitdaging Hallo beveiligingsstatus van hun infrastructuur te controleren. Deze uitdaging gaat niet anders zijn voor hun virtuele machines in Azure. Het is belangrijk toohave een vergelijkbare beveiligingsprofiel op basis van regels die Hallo Netwerkbeveiligingsgroep (NSG) worden toegepast. U kunt nu een Hallo lijst met toegepaste regels tooa VM binnen een NSG krijgen met behulp van Hallo beveiliging groep weergeven. U kunt definiëren van een gouden NSG-beveiligingsprofiel en beveiliging groepsweergave een wekelijkse uitgebracht initiëren en vergelijken Hallo uitvoer toohello gouden profiel en een rapport maken. Op deze manier kunt u identificeren met gemak alle Hallo VM's die niet toohello beveiligingsprofiel voorgeschreven voldoen.

Als u niet bekend met Netwerkbeveiligingsgroepen bent, gaat u naar [beveiligingsoverzicht van het netwerk](../virtual-network/virtual-networks-nsg.md)

## <a name="before-you-begin"></a>Voordat u begint

In dit scenario u de beveiligingsgroep van een bekende goede basis toohello vergelijken resultaten geretourneerd voor een virtuele machine weergeven.

Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher. Hallo scenario wordt ervan uitgegaan dat een resourcegroep met een geldige virtuele machine toobe gebruikt bestaat.

## <a name="scenario"></a>Scenario

Hallo scenario beschreven in dit artikel Hallo beveiliging groep weergeven voor een virtuele machine opgehaald.

U wordt in dit scenario:

- Ophalen van een bekende goede regelset
- Ophalen van een virtuele machine met de Rest-API
- Groepsweergave beveiliging voor virtuele machine ophalen
- Antwoord evalueren

## <a name="retrieve-rule-set"></a>Regelset ophalen

Hallo eerste stap in dit voorbeeld is toowork met een bestaande basislijn. Hallo volgende voorbeeld is sommige json opgehaald uit een bestaande Netwerkbeveiligingsgroep met Hallo `Get-AzureRmNetworkSecurityGroup` cmdlet die wordt gebruikt als basislijn Hallo voor dit voorbeeld.

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

## <a name="convert-rule-set-toopowershell-objects"></a>Regel set tooPowerShell objecten converteren

We zijn een json-bestand dat eerder is gemaakt met de Hallo-regels die verwachte toobe op Hallo Netwerkbeveiligingsgroep voor dit voorbeeld zijn lezen in deze stap.

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a>Ophalen van netwerk-Watcher

de volgende stap Hallo is tooretrieve Hallo netwerk-Watcher-exemplaar. Hallo `$networkWatcher` variabele is doorgegeven toohello `AzureRmNetworkWatcherSecurityGroupView` cmdlet.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a>Een virtuele machine ophalen

Een virtuele machine is vereist toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet tegen. Hallo volgende voorbeeld wordt een VM-object.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a>Groep beveiligingsweergave ophalen

de volgende stap Hallo is tooretrieve Hallo beveiliging groep weergave resultaat. Dit resultaat wordt vergeleken toohello "baseline" json die eerder is aangegeven.

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-hello-results"></a>Hallo resultaten analyseren

antwoord Hallo worden gegroepeerd per netwerkinterfaces. Hallo verschillende typen regels die zijn geretourneerd geldig zijn en de standaardinstellingen van de beveiligingsregels voor verbindingen. Hallo resultaat wordt verder opgedeeld per hoe deze wordt toegepast, op een subnet of een virtuele NIC.

Hallo vergelijkt volgende PowerShell-script Hallo resultaten van Hallo beveiliging groepsweergave tooan bestaande uitvoer van een NSG. Hallo volgende voorbeeld wordt een eenvoudig voorbeeld van hoe Hallo resultaten kunnen worden vergeleken met `Compare-Object` cmdlet.

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

Hallo volgende voorbeeld is Hallo resultaat. U ziet twee Hallo-regels die in de eerste regelset Hallo zijn zijn niet aanwezig in de Hallo vergelijking.

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

## <a name="next-steps"></a>Volgende stappen

Als de instellingen zijn gewijzigd, Zie [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack omlaag Hallo groep en beveiliging netwerkbeveiligingsregels die betrokken zijn.













