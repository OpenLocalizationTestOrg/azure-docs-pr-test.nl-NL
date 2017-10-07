---
title: aaaIntroduction tooIP stroom controleren in de Azure-netwerk-Watcher | Microsoft Docs
description: Deze pagina bevat een overzicht van Hallo netwerk-Watcher-IP-stroom mogelijkheid controleren
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b648a4816a7ffdc6ca54462944b574e2395e8298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooip-flow-verify-in-azure-network-watcher"></a>Inleiding tooIP stroom controleren in de Azure-netwerk-Watcher

IP-stroom Controleer controles of als een pakket wordt toegestaan of geweigerd tooor van een virtuele machine op basis van 5-tuple informatie. Deze informatie bestaat uit de richting, protocol, lokaal IP-, externe IP-, lokale poort en externe poort. Als hello-pakket is geweigerd door een beveiligingsgroep, wordt Hallo-naam van Hallo-regel die geweigerd hello-pakket geretourneerd. Terwijl de IP-bron- of doelserver kan worden gekozen, deze functie kan beheerders die Analyseer snel problemen met de netwerkverbinding van of toohello internet en van of toohello on-premises omgeving.

IP-stroom controleren is bedoeld voor een netwerkinterface van een virtuele machine. Netwerkverkeer is geverifieerd op basis van Hallo geconfigureerd instellingen tooor van netwerkinterface. Deze functie is handig bij de bevestiging als toegangsroutes en uitgaande verkeer tooor van een virtuele machine wordt geblokkeerd door een regel in een Netwerkbeveiligingsgroep.

Een exemplaar van netwerk-Watcher behoeften toobe gemaakt in alle regio's dat u van plan toorun IP-stroom bent controleren. Netwerk-Watcher is een regionale service en kan alleen worden uitgevoerd op resources in Hallo dezelfde regio. Dit heeft geen invloed op Hallo resultaten van IP-stroom controleren als Hallo route gekoppeld Hallo die NIC nog steeds worden geretourneerd.

![1][1]

## <a name="next-steps"></a>Volgende stappen

Ga naar de volgende artikel toolearn als een pakket wordt toegestaan of geweigerd voor een specifieke virtuele machine via de portal Hallo Hallo. [Controleer of verkeer is toegestaan op een virtuele machine met het IP-stromen controleren met behulp van de portal Hallo](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












