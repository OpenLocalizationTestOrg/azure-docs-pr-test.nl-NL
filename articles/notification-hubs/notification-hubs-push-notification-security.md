---
title: aaaSecurity voor Notification Hubs
description: Dit onderwerp wordt uitgelegd security voor Azure notification hubs.
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: 6506177c-e25c-4af7-8508-a3ddca9dc07c
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f59ad4594c2c0a2e2b22ab0b6d6bad53825a4dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security"></a>Beveiliging
## <a name="overview"></a>Overzicht
Dit onderwerp beschrijft Hallo beveiligingsmodel van Azure Notification Hubs. Omdat een Service Bus-entiteit Notification Hubs, Hallo zijn geïmplementeerd dezelfde beveiligingsmodel als Service Bus. Zie voor meer informatie, Hallo [verificatie van Service Bus](https://msdn.microsoft.com/library/azure/dn155925.aspx) onderwerpen.

## <a name="shared-access-signature-security-sas"></a>Beveiliging van Shared Access Signature (SAS)
Notification Hubs implementeert een entiteitsniveau beveiligingsschema SAS (Shared Access Signature) genoemd. Dit schema kunt messaging entities toodeclare up too12 autorisatieregels in hun beschrijving verlenen van rechten op die entiteit.

Elke regel bevat een naam, de waarde van een sleutel (gedeelde geheim genoemd) en een set rechten, zoals wordt beschreven in de sectie Hallo 'Beveiligingsclaims'. Wanneer u een Notification Hub maakt, twee regels worden automatisch gemaakt: een met rechten voor luisteren (die Hallo van client-app gebruikt) en één met alle rechten (die Hallo app back-end gebruikt).

Bij het uitvoeren van beheer van de registratie van de client-apps als Hallo informatie verzonden meldingen is geen gevoelige (bijvoorbeeld weer updates), een gemeenschappelijke manier tooaccess een Notification Hub is toogive Hallo-sleutelwaarde van Hallo regel Listen alleen-lezen toegang toohello client-app en toogive Hallo-sleutelwaarde van Hallo regel volledige toegang toohello app back-end.

Het is niet raadzaam Windows Store-apps voor client-sleutelwaarde Hallo insluiten. Een manier tooavoid insluiten Hallo sleutelwaarde is toohave Hallo client-app opgehaald van Hallo back-end app bij het opstarten.

Het is belangrijk toounderstand die sleutel met luisteren toegang Hallo kunt u een client app tooregister voor elk label. Als uw app registraties toospecific labels toospecific clients (bijvoorbeeld wanneer labels vertegenwoordigen gebruikers-id's) beperken moet, moet uw app back-end Hallo registraties uitvoeren. Zie voor meer informatie registratie Management. Houd er rekening mee dat op deze manier Hallo client-app geen directe toegang tooNotification Hubs.

## <a name="security-claims"></a>Beveiligingsclaims
Vergelijkbare tooother entiteiten, Notification Hub-bewerkingen zijn toegestaan voor drie beveiligingsclaims: luisteren, te verzenden en te beheren.

| Claim | Beschrijving | Bewerkingen die zijn toegestaan |
| --- | --- | --- |
| Luisteren |Maken of bij te werken, lezen en verwijderen van één registraties |Registratie maken/bijwerken<br><br>Lezen registratie<br><br>Alle registraties voor een ingang lezen<br><br>Registratie verwijderen |
| Verzenden |Verzenden van berichten toohello notification hub |Bericht verzenden |
| Beheren |CRUDs van Notification Hubs (inclusief PNS-referenties en beveiligingssleutels bijwerken) en lezen registraties op basis van tags |Maken, bijwerken, lezen/verwijderen notification hubs<br><br>Registraties door code te lezen |

Notification Hubs accepteren claims verleend door Microsoft Azure Access Control-tokens en handtekening-tokens gegenereerd met gedeelde sleutels rechtstreeks op Hallo Notification Hub is geconfigureerd.

