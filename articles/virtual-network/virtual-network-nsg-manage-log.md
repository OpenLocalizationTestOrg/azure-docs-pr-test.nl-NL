---
title: aaaMonitor bewerkingen, gebeurtenissen en prestatiemeteritems voor het nsg's | Microsoft Docs
description: Meer informatie over hoe tooenable tellers, gebeurtenissen en operationele logboekregistratie voor het nsg's
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2e699078-043f-48bd-8aa8-b011a32d98ca
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/31/2017
ms.author: jdial
ms.openlocfilehash: f16f1a0ad693028ee7aba21574b5c8ddfcd27096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-network-security-groups-nsgs"></a>Logboekanalyses voor netwerkbeveiligingsgroepen (NSG's)

Hallo diagnostische logboeken categorieën voor het nsg's te volgen, kunt u inschakelen:

* **Gebeurtenis:** bevat vermeldingen voor welke NSG regels toegepaste tooVMs en de exemplaar-rollen op basis van MAC-adres zijn. Hallo-status voor deze regels worden verzameld om de 60 seconden.
* **Regelteller:** bevat vermeldingen voor hoe vaak elke NSG regel is toegepast toodeny of verkeer toestaan.

> [!NOTE]
> Diagnostische logboeken zijn alleen beschikbaar voor het nsg's geïmplementeerd via hello Azure Resource Manager-implementatiemodel. U kunt Diagnostische logboekregistratie voor het nsg's geïmplementeerd via de klassieke implementatiemodel Hallo niet inschakelen. Voor een beter begrip van Hallo twee modellen, verwijzen naar Hallo [wat Azure-implementatiemodellen](../resource-manager-deployment-model.md) artikel.

Logboekregistratie van activiteit (voorheen bekend als audit- of operationele Logboeken) is standaard ingeschakeld voor het nsg's die zijn gemaakt via de Azure-implementatiemodel. toodetermine welke bewerkingen zijn voltooid op het nsg's in het gebeurtenissenlogboek hello, zoeken naar vermeldingen met Hallo brontypen te volgen: 

- Microsoft.ClassicNetwork/networkSecurityGroups 
- Microsoft.ClassicNetwork/networkSecurityGroups/securityRules
- Microsoft.Network/networkSecurityGroups
- Microsoft.Network/networkSecurityGroups/securityRules 

Lees Hallo [overzicht van hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) artikel toolearn meer over activiteitenlogboeken. 

## <a name="enable-diagnostic-logging"></a>Bijhouden van diagnostische gegevens inschakelen

Diagnostische logboekregistratie moet zijn ingeschakeld voor *elke* NSG gewenste toocollect gegevens voor. Hallo [overzicht van Azure diagnostische logboeken](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artikel wordt uitgelegd waar diagnostische logboeken kunnen worden verzonden. Als u een bestaande NSG geen hebt, volledige Hallo stappen voor het Hallo [maken van een netwerkbeveiligingsgroep](virtual-networks-create-nsg-arm-pportal.md) artikel toocreate een. U kunt NSG Diagnostische logboekregistratie met behulp van de volgende methoden Hallo inschakelen:

### <a name="azure-portal"></a>Azure Portal

toouse hello portal tooenable-registratie, aanmelding toohello [portal](https://portal.azure.com). Klik op **meer services**, typ *netwerkbeveiligingsgroepen*. Selecteer Hallo NSG tooenable gewenste voor logboekregistratie. Volg de instructies Hallo voor niet-rekenresources in Hallo [Schakel diagnostische logboeken in de portal Hallo](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artikel. Selecteer **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, of beide categorieën van Logboeken.

### <a name="powershell"></a>PowerShell

toouse PowerShell tooenable aan te melden, volg de instructies Hallo in Hallo [Schakel diagnostische logboeken via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artikel. Evalueert de volgende informatie voordat u een opdracht invoert uit artikel Hallo Hallo:

- U kunt bepalen Hallo waarde toouse voor Hallo `-ResourceId` parameter door te vervangen Hallo na [tekst] toepasselijke Hallo-opdracht in te voeren `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`. Hallo-ID-uitvoer van Hallo opdracht er ongeveer als volgt te*/subscriptions/ [abonnement Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.
- Als u alleen gegevens uit de categorie logboek toocollect toevoegen `-Categories [category]` toohello einde van Hallo-opdracht in Hallo artikel waar categorie is *NetworkSecurityGroupEvent* of *NetworkSecurityGroupRuleCounter*. Als u geen Hallo `-Categories` parameter gegevensverzameling is ingeschakeld voor zowel logboekbestand categorieën.

### <a name="azure-command-line-interface-cli"></a>Azure-opdrachtregelinterface (CLI)

toouse Hallo CLI tooenable logboekregistratie, volg de instructies Hallo in Hallo [Schakel diagnostische logboeken via CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artikel. Evalueert de volgende informatie voordat u een opdracht invoert uit artikel Hallo Hallo:

- U kunt bepalen Hallo waarde toouse voor Hallo `-ResourceId` parameter door te vervangen Hallo na [tekst] toepasselijke Hallo-opdracht in te voeren `azure network nsg show [resource-group-name] [nsg-name]`. Hallo-ID-uitvoer van Hallo opdracht er ongeveer als volgt te*/subscriptions/ [abonnement Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.
- Als u alleen gegevens uit de categorie logboek toocollect toevoegen `-Categories [category]` toohello einde van Hallo-opdracht in Hallo artikel waar categorie is *NetworkSecurityGroupEvent* of *NetworkSecurityGroupRuleCounter*. Als u geen Hallo `-Categories` parameter gegevensverzameling is ingeschakeld voor zowel logboekbestand categorieën.

## <a name="logged-data"></a>Logboekgegevens

Gegevens in JSON-indeling is geschreven voor beide logboeken. Hallo specifieke gegevens die zijn geschreven voor elk Logboektype wordt vermeld in Hallo uit te voeren:

### <a name="event-log"></a>Gebeurtenislogboek
Dit logboek bevat informatie over welke NSG regels worden toegepast tooVMs en cloud service rolinstanties, op basis van MAC-adres. Hallo bijvoorbeeld gegevens te volgen wordt voor elke gebeurtenis geregistreerd:

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupEvent",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION-ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupEvents",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-B791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "priority":1000,
        "type":"allow",
        "conditions":{
            "protocols":"6",
            "destinationPortRange":"3389-3389",
            "sourcePortRange":"0-65535",
            "sourceIP":"0.0.0.0/0",
            "destinationIP":"0.0.0.0/0"
            }
        }
}
```

### <a name="rule-counter-log"></a>Regel teller logboek

Dit logboek bevat informatie over de tooresources van elke regel van toepassing. Hallo volgende van de voorbeeldgegevens worden geregistreerd telkens wanneer die een regel wordt toegepast:

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupRuleCounter",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]TESTRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupCounters",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "type":"allow",
        "matchedConnections":125
        }
}
```

## <a name="view-and-analyze-logs"></a>Weergeven en analyseren van Logboeken

hoe tooview activiteit meld gegevens lezen Hallo toolearn [overzicht van hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artikel. hoe tooview diagnostische gegevens, meld lezen Hallo toolearn [overzicht van Azure diagnostische logboeken](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artikel. Als u diagnostische gegevens tooLog Analytics verzendt, kunt u Hallo [Netwerkbeveiligingsgroep Azure analytics](../log-analytics/log-analytics-azure-networking-analytics.md) oplossing voor verbeterde insights (preview). 
