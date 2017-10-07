---
title: aaaIntroduction tootopology in Azure-netwerk-Watcher | Microsoft Docs
description: Deze pagina bevat een overzicht van Hallo netwerk-Watcher-topologie-mogelijkheden
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e753a435-38e0-482b-846b-121cb547555c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7fa1c5518e4a25a5db999d898a9ee19fd0121db7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tootopology-in-azure-network-watcher"></a>Inleiding tootopology in Azure-netwerk-Watcher

Topologie retourneert een grafiek van netwerkbronnen in een virtueel netwerk. Hallo-grafiek wordt Hallo koppeling tussen Hallo resources toorepresent Hallo end tooend verbinding met het netwerk.

![overzicht van de topologie][1]

In de portal Hallo retourneert topologie Hallo resourceobjecten op een per per virtueel netwerk. Hallo relaties zijn afgebeeld met lijnen tussen Hallo resources bronnen buiten Hallo netwerk-Watcher regio, zelfs als in Hallo bron de groep niet worden weergegeven. Hallo bronnen geretourneerd in de portal weergave Hallo zijn een subset van Hallo netwerkonderdelen die diagram worden weergegeven aan. toosee hello volledige lijst met netwerkresources kunt u [PowerShell](network-watcher-topology-powershell.md) of [REST](network-watcher-topology-rest.md)

> [!NOTE]
> Een exemplaar van netwerk-Watcher is vereist in elke regio waarin u wilt dat toorun topologie op.

Resources Hallo verbinding tussen hen worden geretourneerd worden gemodelleerd onder twee-relaties.

- **Containment** -voorbeeld: virtueel netwerk bevat een Subnet met een NIC
- **Gekoppeld** -voorbeeld: een NIC is gekoppeld aan een virtuele machine

### <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe toouse PowerShell tooretrieve Hallo topologie bekijken op [netwerk-Watcher-topologie met PowerShell](network-watcher-topology-powershell.md)

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
