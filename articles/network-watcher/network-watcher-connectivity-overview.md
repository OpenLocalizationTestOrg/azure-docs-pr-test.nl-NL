---
title: aaaIntroduction tooconnectivity controle in de Azure-netwerk-Watcher | Microsoft Docs
description: Deze pagina bevat een overzicht van netwerk-Watcher connectiviteit mogelijkheid Hallo
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 52fc4547f167cea2992a046859dc0550d136e80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooconnectivity-check-in-azure-network-watcher"></a>Inleiding tooconnectivity controle in de Azure-netwerk-Watcher

Hallo connectiviteit functie van netwerk-Watcher biedt Hallo mogelijkheid toocheck een directe TCP-verbinding van een virtuele machine tooa virtuele machine (VM), volledig gekwalificeerde domeinnaam (FQDN), URI, of IPv4-adres. Scenario's met netwerken complex zijn, worden geïmplementeerd met behulp van Netwerkbeveiligingsgroepen, firewalls, gebruiker gedefinieerde routes en resources die worden geleverd door Azure. Complexe configuraties maakt met het oplossen van verbindingsproblemen moeilijker. Netwerk-Watcher helpt Verklein Hallo en de hoeveelheid tijd toofind en verbindingsproblemen detecteren. Hallo resultaten biedt mogelijk inzicht in of een verbindingsprobleem vanwege tooa platform of een probleem met de gebruiker is. Connectiviteit kan worden gecontroleerd met [PowerShell](network-watcher-connectivity-powershell.md), [Azure CLI](network-watcher-connectivity-cli.md), en [REST-API](network-watcher-connectivity-rest.md).

> [!IMPORTANT]
> Controle van de verbinding zijn nodig voor de extensie van een virtuele machine `AzureNetworkWatcherExtension`. Ga voor het Hallo-uitbreiding installeren op een virtuele machine van Windows naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Windows](../virtual-machines/windows/extensions-nwa.md) en voor Linux-VM naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="response"></a>Antwoord

Hallo volgende tabel ziet u Hallo eigenschappen geretourneerd bij een controle van de verbinding is voltooid.

|Eigenschap  |Beschrijving  |
|---------|---------|
|ConnectionStatus     | Hallo-status van Hallo connectiviteit controleren. Mogelijke resultaten zijn **bereikbaar** en **onbereikbaar**.        |
|AvgLatencyInMs     | Gemiddelde latentie tijdens controle van Hallo-connectiviteit in milliseconden. (Alleen weergegeven als de status bereikbaar is)        |
|MinLatencyInMs     | Minimale latentie tijdens het Hallo-connectiviteit controleren in milliseconden. (Alleen weergegeven als de status bereikbaar is)        |
|MaxLatencyInMs     | Maximale duur geldt tijdens het Hallo-connectiviteit controleren in milliseconden. (Alleen weergegeven als de status bereikbaar is)        |
|ProbesSent     | Aantal tests die worden verzonden tijdens Hallo controle. De maximale waarde is 100.        |
|ProbesFailed     | Aantal tests die zijn mislukt bij het Hallo-controle. De maximale waarde is 100.        |
|Hops     | Hop door hop pad van de bron toodestination.        |
|[] Hops. Type     | Type resource. Mogelijke waarden zijn **bron**, **VirtualAppliance**, **VnetLocal**, en **Internet**.        |
|[] Hops. ID | Unieke id van het Hallo-hop.|
|[] Hops. Adres | IP-adres van Hallo-hop.|
|[] Hops. ResourceId | De ResourceID van Hallo hop als Hallo hop een Azure-resource is. Als het een internet-bron, ResourceID is **Internet**. |
|[] Hops. NextHopIds | Hallo unieke id van de volgende hop Hallo genomen.|
|[] Hops. Problemen | Een verzameling van problemen die zijn opgetreden tijdens de controle Hallo op die hop. Als er geen problemen zijn, is Hallo waarde leeg.|
|[] Hops. [] Verstrekt. Oorsprong | Op Hallo huidige hop, waar probleem is opgetreden. Mogelijke waarden zijn:<br/> **Inkomende** -probleem is op de koppeling Hallo van Hallo vorige hop toohello huidige hop<br/>**Uitgaande** -probleem is op de koppeling Hallo van Hallo huidige hop toohello volgende hop<br/>**Lokale** -probleem is op de huidige Hallo-hop.|
|[] Hops. [] Verstrekt. Ernst | Hallo ernst van Hallo probleem gedetecteerd. Mogelijke waarden zijn **fout** en **waarschuwing**. |
|[] Hops. [] Verstrekt. Type |Hallo-type van het probleem gevonden. Mogelijke waarden zijn: <br/>**CPU**<br/>**Geheugen**<br/>**GuestFirewall**<br/>**DnsResolution**<br/>**NetworkSecurityRule**<br/>**UserDefinedRoute** |
|[] Hops. [] Verstrekt. Context |Gegevens met betrekking tot Hallo probleem gevonden.|
|[] Hops. [] Verstrekt. Context [] .key |Sleutel van sleutel-waardepaar Hallo geretourneerd.|
|[] Hops. [] Verstrekt. Context [] .value |Waarde van sleutel-waardepaar Hallo geretourneerd.|

Hallo Hier volgt een voorbeeld van een probleem gevonden bij een hop.

```json
"Issues": [
    {
        "Origin": "Outbound",
        "Severity": "Error",
        "Type": "NetworkSecurityRule",
        "Context": [
            {
                "key": "RuleName",
                "value": "UserRule_Port80"
            }
        ]
    }
]
```
## <a name="fault-types"></a>Fout-typen

Hallo connectiviteit selectievakje retourneert fout typen over Hallo-verbinding. Hallo bevat volgende tabel een lijst met Hallo huidige veroorzaakt typen die zijn geretourneerd.

|Type  |Beschrijving  |
|---------|---------|
|CPU     | Hoog CPU-verbruik.       |
|Geheugen     | Hoog geheugengebruik.       |
|GuestFirewall     | Verkeer wordt geblokkeerd vanwege tooa virtuele machine firewallconfiguratie.        |
|DNSResolution     | DNS-omzetting is mislukt voor Hallo-doeladres.        |
|NetworkSecurityRule    | Verkeer wordt geblokkeerd door een regel voor het NSG (de regel is geretourneerd)        |
|UserDefinedRoute|Verkeer wordt verbroken vanwege tooa door de gebruiker gedefinieerde of systeemroute. |

### <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe tooverify connectiviteit tooa resource in via: [Controleer de verbinding met Azure-netwerk-Watcher](network-watcher-connectivity-powershell.md).

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png

