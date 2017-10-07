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
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a>De beveiliging van uw virtuele Machine met beveiliging groep weergeven met behulp van Azure CLI 1.0 analyseren

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-security-group-view-powershell.md)
> - [CLI 1.0](network-watcher-security-group-view-cli-nodejs.md)
> - [CLI 2.0](network-watcher-security-group-view-cli.md)
> - [REST API](network-watcher-security-group-view-rest.md)

Groep beveiligingsweergave retourneert geconfigureerd en effectieve netwerkbeveiligingsregels die toegepast tooa virtuele machine zijn. Deze mogelijkheid is nuttig tooaudit en onderzoeken van Netwerkbeveiligingsgroepen en regels die zijn geconfigureerd op een VM tooensure-verkeer wordt toegestaan of geweigerd correct. In dit artikel zien we u hoe tooretrieve Hallo geconfigureerd en een effectieve beveiligingsmethode regels tooa virtuele machine met Azure CLI

Dit artikel wordt platformoverschrijdende Azure CLI 1.0 gebruikt die beschikbaar is voor Windows, Mac en Linux. Netwerk-Watcher gebruikt momenteel de Azure CLI 1.0 voor CLI-ondersteuning.

## <a name="before-you-begin"></a>Voordat u begint

Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.

## <a name="scenario"></a>Scenario

Hallo scenario beschreven in dit artikel worden Hallo geconfigureerd en een effectieve beveiligingsmethode regels voor een bepaalde virtuele machine opgehaald.

## <a name="get-a-vm"></a>Een virtuele machine ophalen

Een virtuele machine is vereist toorun hello `vm list` cmdlet. Hallo volgende opdracht worden virtuele machinese Hallo in een resourcegroep:

```azurecli
azure vm list -g resourceGroupName
```

Zodra u Hallo virtuele machine weet, kunt u Hallo `vm show` cmdlet tooget de resource-Id:

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a>Groep beveiligingsweergave ophalen

de volgende stap Hallo is tooretrieve Hallo beveiliging groep weergave resultaat. Toe te voegen Hallo '--json ' vlag Hallo resulteert in json wordt geformatteerd.

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-hello-results"></a>Hallo resultaten weergeven

Hallo is volgende voorbeeld een kortere respons van Hallo resultaten geretourneerd. Hallo resultaten weergeven alle Hallo effectieve en toegepaste beveiligingsregels voor verbindingen op Hallo virtuele machine is onderverdeeld in groepen van **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, en  **EffectiveSecurityRules**.

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

## <a name="next-steps"></a>Volgende stappen

Ga naar [controle Netwerkbeveiligingsgroep groepen (NSG) met de netwerk-Watcher](network-watcher-nsg-auditing-powershell.md) toolearn hoe tooautomate validatie van Netwerkbeveiligingsgroepen.

Meer informatie over Hallo beveiligingsregels voor verbindingen die toegepast tooyour netwerkbronnen in via zijn [beveiligingsoverzicht groep weergeven](network-watcher-security-group-view-overview.md)
