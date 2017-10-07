---
title: aaaCheck connectiviteit met de Azure-netwerk-Watcher - Azure-portal | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe toouse connectiviteit contact op met de netwerk-Watcher met hello Azure-portal
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
ms.openlocfilehash: ef6ecccd688f06f70003a5b59771c15bcbe8f3e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a>Controleer de verbinding met de netwerk-Watcher van Azure met behulp van hello Azure-portal

> [!div class="op_single_selector"]
> - [Portal](network-watcher-connectivity-portal.md)
> - [PowerShell](network-watcher-connectivity-powershell.md)
> - [CLI 2.0](network-watcher-connectivity-cli.md)
> - [Azure REST-API](network-watcher-connectivity-rest.md)

Meer informatie over hoe toouse connectiviteit tooverify als een directe TCP-verbinding van een virtuele machine tooa opgegeven eindpunt kan worden vastgesteld.

## <a name="before-you-begin"></a>Voordat u begint

In dit artikel wordt ervan uitgegaan dat er Hallo resources te volgen:

* Een exemplaar van netwerk-Watcher in Hallo regio die u wilt toocheck connectiviteit.

* Virtuele machines toocheck connectiviteit met.

> [!IMPORTANT]
> Controle van de verbinding zijn nodig voor de extensie van een virtuele machine `AzureNetworkWatcherExtension`. Ga voor het Hallo-uitbreiding installeren op een virtuele machine van Windows naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Windows](../virtual-machines/windows/extensions-nwa.md) en voor Linux-VM naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="check-connectivity-tooa-virtual-machine"></a>Controleer de connectiviteit tooa virtuele machine

In dit voorbeeld controleert connectiviteit tooa bestemde virtuele machine via poort 80.

Navigeer tooyour netwerk-Watcher en klik op **connectiviteit selectievakje (Preview)**. Selecteer Hallo virtuele machine vanaf toocheck verbinding. In Hallo **bestemming** sectie kiezen **Selecteer een virtuele machine** en kies Hallo juiste virtuele machine en poort tootest.

Nadat u op **controleren**, Hallo connectiviteit tussen Hallo virtuele machines op de opgegeven poort voor Hallo worden gecontroleerd. In voorbeeld Hallo Hallo bestemming VM is niet bereikbaar, een overzicht van hops worden weergegeven.

![Resultaten van de verbinding voor een virtuele machine][1]

## <a name="check-remote-endpoint-connectivity"></a>Controleer de verbindingen van het externe eindpunt

toocheck hello connectiviteit en latentie tooa externe eindpunt, kies Hallo **handmatig opgeven** keuzerondje in Hallo **bestemming** sectie, invoer Hallo-url en Hallo-poort en klik op **controleren** .  Dit wordt gebruikt voor externe eindpunten zoals websites en -opslag-eindpunten.

![Resultaten van de verbinding voor een website][2]

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe tooautomate pakket worden vastgelegd met waarschuwingen van de virtuele machine door [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)

Als bepaalde verkeer is toegestaan in of buiten uw virtuele machine in via vinden [controleren IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
