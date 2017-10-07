---
title: Controleer aaaVerify verkeer met Azure-netwerk-Watcher IP-flow - Azure-portal | Microsoft Docs
description: Dit artikel wordt beschreven hoe toocheck als tooor van een virtuele machine verkeer wordt toegestaan of geweigerd
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: abf639f36d32f3416dd927e66b635267b746e62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Controleer als verkeer wordt toegestaan of geweigerd tooor van een virtuele machine met het IP-stromen controleren of een onderdeel van Azure-netwerk-Watcher

> [!div class="op_single_selector"]
> - [Azure Portal](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST-API](network-watcher-check-ip-flow-verify-rest.md)


IP-stroom controleren is een functie van netwerk-Watcher waarmee u tooverify als verkeer wordt toegestaan tooor van een virtuele machine. Hallo validatie kan worden uitgevoerd voor binnenkomend of uitgaand verkeer. Dit scenario is nuttig tooget een huidige status van of een virtuele machine tooan externe bron of een andere resource praten kunt. IP-stroom controleren gebruikte tooverify is als uw regels Netwerkbeveiligingsgroep (NSG) juist zijn geconfigureerd en oplossen van stromen die worden geblokkeerd door het NSG-regels. Een andere reden voor het gebruik van IP-stroom controleren die u blokkeren wilt tooensure-verkeer wordt geblokkeerd goed door Hallo NSG.

## <a name="before-you-begin"></a>Voordat u begint

Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher of een bestaand exemplaar van netwerk-Watcher hebben. Hallo scenario wordt ervan uitgegaan dat een resourcegroep met een geldige virtuele machine toobe gebruikt bestaat.

## <a name="scenario"></a>Scenario

Dit scenario maakt gebruik van IP-stromen controleren tooverify als een virtuele machine tooanother computer via poort 443 communiceren kan. Als het Hallo-verkeer wordt geweigerd, wordt Hallo beveiligingsregel die dat verkeer wordt geweigerd. toolearn meer informatie over IP-stromen controleren, gaat u naar [overzicht van IP-stromen controleren](network-watcher-ip-flow-verify-overview.md)

### <a name="run-ip-flow-verify"></a>Voer IP-stroom controleren

Navigeer tooyour netwerk-Watcher en klik op **IP-stroom controleren**. Hallo virtuele machine en netwerkinterface die u verkeer van tooverify wilt selecteren. Voer eventueel aanvullende informatie voor het filteren en klik op **controleren**.

Nadat u op **controleren**, op basis van Hallo criteria die u hebt opgegeven Hallo-stroom is ingeschakeld. Hallo-resultaat is een **toegang is toegestaan** of **toegang is geweigerd**. Als de toegang is geweigerd Hallo Netwerkbeveiligingsgroep (NSG) en beveiligingsregel die verkeer blokkeren is opgegeven. Als Hallo DOS-verkeer verwacht gedrag is, zijn Hallo-regel is geslaagd.

> [!NOTE]
> IP-stroom controleren vereist dat de VM-resource hello wordt toegewezen.

Als u in Hallo volgende afbeelding zien kunt, is Hallo uitgaande HTTPS-verkeer toegestaan.

![IP-stroom overzicht controleren][1]

Zoals u in Hallo installatiekopie te volgen, verkeer wordt gewijzigd tooinbound en Hallo inkomende too123 poort gewijzigd. Verkeer wordt nu geweigerd, is Hallo-bericht 'Toegang geweigerd' opgegeven samen met de Hallo groep en beveiliging netwerkbeveiligingsregel die Hallo verkeer weigeren.

![IP-stroom resultaten][2]

## <a name="next-steps"></a>Volgende stappen

Zie als verkeer wordt geblokkeerd en mag geen [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack omlaag Hallo groep en beveiliging netwerkbeveiligingsregels die zijn gedefinieerd.

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













