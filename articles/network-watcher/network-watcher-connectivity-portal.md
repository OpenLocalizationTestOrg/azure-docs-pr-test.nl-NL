---
title: Controleer de verbinding met Azure-netwerk-Watcher - Azure-portal | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe u verbinding met de netwerk-Watcher met de Azure portal gebruiken
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
ms.date: 08/03/2017
ms.author: gwallace
ms.openlocfilehash: 84774d0f40e06a819ca6de6cf0be68e17ba474e4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-the-azure-portal"></a>Controleer de verbinding met de netwerk-Watcher van Azure met Azure portal

> [!div class="op_single_selector"]
> - [Portal](network-watcher-connectivity-portal.md)
> - [PowerShell](network-watcher-connectivity-powershell.md)
> - [CLI 2.0](network-watcher-connectivity-cli.md)
> - [Azure REST-API](network-watcher-connectivity-rest.md)

Informatie over het gebruik van verbinding om te controleren als direct TCP-verbinding van een virtuele machine naar een opgegeven eindpunt kan worden gemaakt.

## <a name="before-you-begin"></a>Voordat u begint

In dit artikel wordt ervan uitgegaan dat u hebt de volgende bronnen:

* Een exemplaar van netwerk-Watcher in de regio die u wilt controleren, connectiviteit.

* Virtuele machines connectiviteit met controleren.

> [!IMPORTANT]
> Controle van de verbinding zijn nodig voor de extensie van een virtuele machine `AzureNetworkWatcherExtension`. Voor het installeren van de extensie op een Windows-virtuele machine gaat u naar [extensie voor het virtuele machine voor Windows Azure-netwerk-Watcher Agent](../virtual-machines/windows/extensions-nwa.md) en voor Linux-VM naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="check-connectivity-to-a-virtual-machine"></a>Controleer de verbinding met een virtuele machine

In dit voorbeeld controleert de verbinding met een doel-virtuele machine via poort 80.

Navigeer naar uw netwerk-Watcher en klikt u op **connectiviteit selectievakje (Preview)**. Selecteer de virtuele machine, Controleer de verbinding tussen. In de **bestemming** sectie kiezen **Selecteer een virtuele machine** en kies de juiste virtuele machine en poort om te testen.

Nadat u op **controleren**, de verbinding tussen de virtuele machines op de opgegeven poort worden gecontroleerd. De doel-virtuele machine is niet bereikbaar, een overzicht van hops weergegeven in het voorbeeld.

![Resultaten van de verbinding voor een virtuele machine][1]

## <a name="check-remote-endpoint-connectivity"></a>Controleer de verbindingen van het externe eindpunt

Als u wilt controleren de connectiviteit en de latentie van een extern eindpunt, kies de **handmatig opgeven** keuzerondje in de **bestemming** sectie, voert u de url en de poort en klik op **controleren**.  Dit wordt gebruikt voor externe eindpunten zoals websites en -opslag-eindpunten.

![Resultaten van de verbinding voor een website][2]

## <a name="next-steps"></a>Volgende stappen

Meer informatie over het automatiseren van pakket opnamen met waarschuwingen van de virtuele machine met weer te geven [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)

Als bepaalde verkeer is toegestaan in of buiten uw virtuele machine in via vinden [controleren IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
