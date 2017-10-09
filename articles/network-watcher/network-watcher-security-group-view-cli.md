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
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-20"></a>De beveiliging van uw virtuele Machine met beveiliging groep weergeven met behulp van Azure CLI 2.0 analyseren

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-security-group-view-powershell.md)
> - [CLI 1.0](network-watcher-security-group-view-cli-nodejs.md)
> - [CLI 2.0](network-watcher-security-group-view-cli.md)
> - [REST API](network-watcher-security-group-view-rest.md)

Groep beveiligingsweergave retourneert geconfigureerd en effectieve netwerkbeveiligingsregels die toegepast tooa virtuele machine zijn. Deze mogelijkheid is nuttig tooaudit en onderzoeken van Netwerkbeveiligingsgroepen en regels die zijn geconfigureerd op een VM tooensure-verkeer wordt toegestaan of geweigerd correct. In dit artikel zien we u hoe tooretrieve Hallo geconfigureerd en een effectieve beveiligingsmethode regels tooa virtuele machine met Azure CLI


In dit artikel gebruikt de volgende generatie CLI voor Hallo resource management-implementatiemodel, Azure CLI 2.0, die beschikbaar is voor Windows, Mac en Linux.

tooperform hello stappen in dit artikel, moet u te[hello Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI) installeren](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="before-you-begin"></a>Voordat u begint

Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.

## <a name="scenario"></a>Scenario

Hallo scenario beschreven in dit artikel worden Hallo geconfigureerd en een effectieve beveiligingsmethode regels voor een bepaalde virtuele machine opgehaald.

## <a name="get-a-vm"></a>Een virtuele machine ophalen

Een virtuele machine is vereist toorun hello `vm list` cmdlet. Hallo volgende opdracht worden Hallo virtuele machines in een resourcegroep:

```azurecli
az vm list -resource-group resourceGroupName
```

Zodra u Hallo virtuele machine weet, kunt u Hallo `vm show` cmdlet tooget de resource-Id:

```azurecli
az vm show -resource-group resourceGroupName -name virtualMachineName
```

## <a name="retrieve-security-group-view"></a>Groep beveiligingsweergave ophalen

de volgende stap Hallo is tooretrieve Hallo beveiliging groep weergave resultaat.

```azurecli
az network watcher show-security-group-view --resource-group resourceGroupName --vm vmName
```

## <a name="viewing-hello-results"></a>Hallo resultaten weergeven

Hallo is volgende voorbeeld een kortere respons van Hallo resultaten geretourneerd. Hallo resultaten weergeven alle Hallo effectieve en toegepaste beveiligingsregels voor verbindingen op Hallo virtuele machine is onderverdeeld in groepen van **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, en  **EffectiveSecurityRules**.

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

## <a name="next-steps"></a>Volgende stappen

Ga naar [controle Netwerkbeveiligingsgroep groepen (NSG) met de netwerk-Watcher](network-watcher-nsg-auditing-powershell.md) toolearn hoe tooautomate validatie van Netwerkbeveiligingsgroepen.

Meer informatie over Hallo beveiligingsregels voor verbindingen die toegepast tooyour netwerkbronnen in via zijn [beveiligingsoverzicht groep weergeven](network-watcher-security-group-view-overview.md)
