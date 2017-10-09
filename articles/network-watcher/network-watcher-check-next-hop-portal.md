---
title: de volgende hop aaaFind met Azure-netwerk-Watcher volgende Hop - Azure-portal | Microsoft Docs
description: In dit artikel wordt beschreven hoe u kunt zoeken welke Hallo type voor het volgende hop is en het IP-adres met behulp van volgende Hop hello Azure-portal
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b64a2a5275c15aa8bdb10601de4ae1504a9ab551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-hello-portal"></a>Ontdek welke Hallo volgend hoptype Hallo volgende Hop mogelijkheid gebruikt in Azure met behulp van de portal Hallo netwerk-Watcher

> [!div class="op_single_selector"]
> - [Azure Portal](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [Azure REST-API](network-watcher-check-next-hop-rest.md)

De volgende hop is een functie van netwerk-Watcher die de mogelijkheid Hallo biedt Hallo volgend hoptype en IP-adres op basis van een opgegeven virtuele machine ophalen. Deze functie is handig bij het bepalen of een virtuele machine uitgaand verkeer van een gateway, internet of virtuele netwerken tooget tooits bestemming passeert.

## <a name="before-you-begin"></a>Voordat u begint

Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher. Hallo scenario wordt ervan uitgegaan dat een resourcegroep met een geldige virtuele machine toobe gebruikt bestaat.

## <a name="scenario"></a>Scenario

Hallo scenario beschreven in dit artikel maakt gebruik van volgende hop toofind uit het volgende hoptype hello en IP-adres voor een resource. toolearn meer informatie over het volgende Hop, gaat u naar [volgende Hop overzicht](network-watcher-next-hop-overview.md).

U wordt in dit scenario:

* De volgende hop Hallo ophalen van een virtuele machine.

## <a name="get-next-hop"></a>Ophalen van de volgende Hop

### <a name="step-1"></a>Stap 1

Navigeer tooyour netwerk-Watcher-bron in hello Azure-portal.

### <a name="step-2"></a>Stap 2

Klik op **volgende hop** invullen in het navigatiedeelvenster Hallo, selecteer Hallo virtuele machine en netwerkinterface, de Hallo bron en doel-IP en klikt u op Hallo **volgende hop** knop.

> [!NOTE]
> Volgende hop is vereist dat de VM-resource Hallo toorun wordt toegewezen.

![volgende hop-overzicht][1]

### <a name="step-3"></a>Stap 3

Zodra het Hallo-taak is voltooid, worden Hallo resultaten verstrekt. Hallo IP-adres en het type apparaat Hallo volgende hop is, wordt weergegeven. Hallo volgende tabel toont Hallo beschikbare geretourneerde waarden in Hallo-portal.

**Volgend Hoptype**

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* Geen

Als een aangepaste route gebruikte tooroute is wordt dit verkeer, Hallo gebruiker opgegeven routes (UDR) ook met Hallo resultaten weergegeven.

![ophalen van de volgende hop-resultaten][2]

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe tooreview uw netwerk groep beveiligingsinstellingen programmatisch in via [NSG controleren met de netwerk-Watcher](network-watcher-nsg-auditing-powershell.md)

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














