---
title: aaaLearn over bandbreedtebeperking in BizTalk Services | Microsoft Docs
description: Meer informatie over bandbreedtebeperking drempelwaarden en de resulterende gedrag van de runtime voor BizTalk Services. Bandbreedtebeperking is gebaseerd op het gebruik van geheugen en het aantal berichten. MABS, WABS
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: f6663cf2-cda4-4bac-855e-27d2ad5c4fa4
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 46c8806c3a1f4eeb793f721f849771e0ec155197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-throttling"></a>BizTalk Services: beperking

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Azure BizTalk Services implementeert service bandbreedtebeperking op basis van twee voorwaarden: geheugen gebruiks- en Hallo aantal gelijktijdige berichten verwerken. In dit onderwerp bevat Hallo beperking drempelwaarden en beschrijft van Hallo runtimegedrag wanneer er een voorwaarde bandbreedteregeling optreedt.

## <a name="throttling-thresholds"></a>Beperking van de drempelwaarden
Hallo volgende Tabellijsten Hallo bandbreedteregeling bron- en drempelwaarden:

|  | Beschrijving | Lage drempelwaarde | Hoge drempelwaarde |
| --- | --- | --- | --- |
| Geheugen |% van totale systeem geheugen beschikbaar/PageFileBytes. <p><p>Totaal aantal beschikbare PageFileBytes is ongeveer 2 maal Hallo RAM-geheugen van Hallo-systeem. |60% |70% |
| Berichtverwerking |Aantal berichten tegelijkertijd verwerken |40 * aantal kernen |100 * aantal kernen |

Wanneer u een hoge drempelwaarde wordt bereikt, wordt in Azure BizTalk Services toothrottle gestart. Beperking stopt wanneer Hallo lage drempelwaarde is bereikt. Bijvoorbeeld, is uw service met behulp van 65% systeemgeheugen. Hallo service komt niet in deze situatie vertraging. Uw service wordt gestart met behulp van het systeemgeheugen 70%. In dit geval Hallo service bandbreedte en toothrottle wordt vervolgd totdat Hallo service 60% (lage drempelwaarde) het systeemgeheugen gebruikt.

Azure BizTalk Services houdt Hallo beperking status (normale status versus beperkte status) en Hallo duur beperking.

## <a name="runtime-behavior"></a>Runtime-gedrag
Wanneer u Azure BizTalk Services in een bandbreedteregeling staat, wordt Hallo volgende gebeurt:

* Beperking is per rolexemplaar. Bijvoorbeeld:<br/>
  RoleInstanceA is beperking. RoleInstanceB is geen beperking. In deze situatie verwerkt berichten in RoleInstanceB zoals verwacht. Berichten in RoleInstanceA worden verwijderd en mislukt met de volgende fout Hallo:<br/><br/>
  **Server is bezet. Probeer het opnieuw.**<br/><br/>
* Een pull-bronnen geen pollen of downloaden van een bericht. Bijvoorbeeld:<br/>
  Een pijplijn haalt berichten uit een externe FTP-bron. Hallo rolinstantie doen Hallo pull opgehaald in een status bandbreedteregeling. In dit geval stopt Hallo pijplijn aanvullende berichten downloaden totdat de rolinstantie Hallo niet meer beperking.
* Een antwoord wordt verzonden toohello client Hallo-client kan het Hallo-bericht verzenden.
* U moet wachten tot het Hallo-beperking is opgelost. In het bijzonder moet u wachten tot Hallo lage drempelwaarde is bereikt.

## <a name="important-notes"></a>Belangrijke opmerkingen
* Beperking kan niet worden uitgeschakeld.
* Drempelwaarden beperking kan niet worden gewijzigd.
* Beperking, is de hele systeem geïmplementeerd.
* Hello Azure SQL Database-Server heeft ook ingebouwde beperking.

## <a name="additional-azure-biztalk-services-topics"></a>Aanvullende onderwerpen voor Azure BizTalk Services
* [Hello Azure BizTalk Services SDK installeren](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [Zelfstudies: Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [Hoe gaan gebruiken Azure BizTalk Services SDK Hallo](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>Zie ook
* [BizTalk Services: Developer, Basic, Standard en Premium-edities grafiek](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [BizTalk Services: Inrichten met behulp van Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [BizTalk Services: statusgrafiek voor de inrichting](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [BizTalk Services: de tabbladen Dashboard, Bewaken en Schalen](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [BizTalk Services: back-ups maken en herstellen](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [BizTalk Services: naam en sleutel van verlener](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

