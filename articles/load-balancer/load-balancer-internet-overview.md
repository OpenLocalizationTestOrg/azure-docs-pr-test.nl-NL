---
title: overzicht van de load balancer gerichte aaaInternet | Microsoft Docs
description: Overzicht voor Internet gerichte load balancer en de bijbehorende functies. Hoe werkt een load balancer voor virtuele machines en cloudservices met Azure.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 529b37aa-a45c-41d1-8877-fee8cc1fa375
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3514f945d69ec576ed256cdd01069491e3e43936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="internet-facing-load-balancer-overview"></a>Internet gerichte load balancer-overzicht

Azure load balancer wijst Hallo openbare IP-adres en poort nummer van binnenkomende verkeer toohello persoonlijke IP-adres en poort van Hallo virtuele machine en omgekeerd voor Hallo antwoord verkeer van Hallo virtuele machine. Regels voor taakverdeling kunnen u specifieke typen toodistribute van verkeer tussen meerdere virtuele machines of services. Bijvoorbeeld, kunt u Hallo belasting van de aanvraag webverkeer spreiden meerdere webservers of web-rollen.

Voor een cloudservice die exemplaren van webrollen of werkrollen bevat, kunt u een openbaar eindpunt in hello (.csdef) servicedefinitiebestand definiëren.

Hallo *servicedefinition.csdef* bestand bevat de eindpuntconfiguratie Hallo en wanneer er meerdere rolexemplaren voor een implementatie van web- of worker-rol, Hallo load balancer worden ingesteld voor het. Hallo manier tooadd exemplaren tooyour cloudimplementatie verandert Hallo-exemplaren op Hallo serviceconfiguratiebestand (.csfg).

Hallo volgende afbeelding ziet u een eindpunt met gelijke taakverdeling voor internetverkeer die wordt gedeeld door drie virtuele machines voor Hallo openbare en persoonlijke TCP-poort 80. Deze drie virtuele machines zijn in een set met gelijke taakverdeling.

![openbare load balancer-voorbeeld](./media/load-balancer-internet-overview/IC727496.png)

Afbeelding 1 - eindpunt voor internetverkeer Netwerktaakverdeling

Wanneer Internet-clients webpagina-aanvragen toohello openbaar IP-adres van de cloudservice Hallo op TCP-poort 80 verzenden, distribueert hello Azure Load Balancer Hallo aanvragen tussen Hallo drie virtuele machines in Hallo taakverdeling set. Zie voor meer informatie over load balancer algoritmen Hallo [overzichtspagina van load balancer](load-balancer-overview.md#load-balancer-features).

Azure Load Balancer distribueert standaard netwerkverkeer wordt evenredig verdeeld over meerdere exemplaren van de virtuele machine. U kunt ook de affiniteit van de sessie configureren voor meer informatie Zie [load balancer-distributie modus](load-balancer-distribution-mode.md).

## <a name="next-steps"></a>Volgende stappen

Meer informatie over [interne load balancer](load-balancer-internal-overview.md) toobetter begrijpen welke load balancer is beter geschikt zijn voor uw implementatie van de cloud.

U kunt ook [maken van de load balancer van een Internetgericht](load-balancer-get-started-internet-arm-ps.md) en configureren van welk type [distributie modus](load-balancer-distribution-mode.md) voor een specifieke load balancer-netwerk het gedrag van verkeer.

Als uw toepassing tookeep verbindingen voor servers achter een load balancer actief is moet, kunt u meer begrip over [inactieve TCP-time-outinstellingen voor een load balancer](load-balancer-tcp-idle-timeout.md). Dit helpt toolearn over niet-actieve Verbindingsgedrag wanneer u van Azure Load Balancer gebruikmaakt.
