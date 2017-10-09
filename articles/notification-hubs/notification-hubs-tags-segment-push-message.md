---
title: aaaRouting en code-expressies
description: Dit onderwerp wordt uitgelegd Routering en code-expressies voor Azure notification hubs.
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: 0fffb3bb-8ed8-4e0f-89e8-0de24a47f644
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c2c60500f7469f1cb1a73a5cf63c221a9ad6cbb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="routing-and-tag-expressions"></a>Routering en code-expressies
## <a name="overview"></a>Overzicht
Code-expressies kunnen u bepaalde groepen van apparaten of meer specifiek registraties tootarget bij het verzenden van een push-melding via Notification Hubs.

## <a name="targeting-specific-registrations"></a>Die gericht is op specifieke registraties
Hallo alleen manier tootarget specifieke notification registraties tooassociate labels, wordt vervolgens gericht zijn op deze labels. Zoals beschreven in [registratie Management](notification-hubs-push-notification-registration-management.md), in volgorde tooreceive push meldingen is tooregister een apparaat een app verwerken op een notification hub. Zodra een registratie op een notification hub is gemaakt, kunt Hallo toepassing backend push notifications tooit verzenden.
Hallo toepassing back-end kunt Hallo registraties tootarget met een specifieke melding in de volgende manieren Hallo kiezen:

1. **Uitzenden**: alle registraties in Hallo notification hub Hallo ontvangen.
2. **Tag**: alle registraties met Hallo opgegeven tag Hallo ontvangen.
3. **Expressie labelen**: alle registraties waarvan reeks labels overeen Hallo opgegeven expressie Hallo ontvangen.

## <a name="tags"></a>Tags
Een label kunt een willekeurige tekenreeks, up too120 tekens, met alfanumerieke en Hallo volgende niet-alfanumerieke tekens: '_', ' @', '#', '. ',':', '-'. Hallo volgende voorbeeld ziet u een toepassing waaruit u de pop-upmeldingen over specifieke muziekgroepen kunt ontvangen. In dit scenario is een eenvoudige manier tooroute meldingen toolabel registraties met labels die verschillende stroken hello, zoals in de volgende afbeelding Hallo vertegenwoordigen.

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

In deze afbeelding Hallo-bericht met tags **Beatles** bereikt alleen Hallo tablet gebruikt dat geregistreerd met de Hallo code **Beatles**.

Zie voor meer informatie over het maken van rapporten voor tags [registratie Management](notification-hubs-push-notification-registration-management.md).

U kunt verzenden meldingen tootags Hallo met verzenden van meldingen methoden Hallo `Microsoft.Azure.NotificationHubs.NotificationHubClient` klasse in Hallo [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK. U kunt ook gebruik van Node.js of Hallo Push Notifications REST-API's.  Hier volgt een voorbeeld van Hallo SDK.

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




Labels hebben geen toobe vooraf is ingericht en toomultiple app-specifiek concepten kunnen verwijzen. Gebruikers van deze voorbeeldtoepassing kunnen bijvoorbeeld becommentariëren stroken en wilt tooreceive toasts, niet alleen voor opmerkingen op hun favoriete stroken hello, maar ook voor alle opmerkingen van vrienden, ongeacht het Hallo-band waarop ze zijn opmerkingen. Hallo volgende afbeelding toont een voorbeeld van dit scenario:

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

In deze afbeelding Els is geïnteresseerd in updates voor Hallo Beatles en Bob is geïnteresseerd in updates voor Hallo Wailers. Bob is ook geïnteresseerd in de Charlie opmerkingen en Charlie is geïnteresseerd in Hallo Wailers. Wanneer een melding wordt verzonden om de Charlie Opmerking bij Hallo Beatles, ontvangen zowel Alice en Bob.

U kunt meerdere problemen in de codes (bijvoorbeeld 'band_Beatles' of 'follows_Charlie') codeert, zijn tags eenvoudige tekenreeksen en niet-eigenschappen met waarden. Een registratie wordt alleen op Hallo aanwezigheid of afwezigheid van een specifieke tag gekoppeld.

Zie voor een volledige stapsgewijze zelfstudie over hoe toouse-tags voor het verzenden van toointerest groepen, [nieuws op te splitsen](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).

## <a name="using-tags-tootarget-users"></a>Met behulp van de labels tootarget gebruikers
Een andere manier toouse tags is tooidentify alle Hallo op apparaten van een bepaalde gebruiker. Registraties worden gelabeld met een tag met een gebruikersnaam, zoals in de volgende afbeelding Hallo:

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

In deze afbeelding bereikt Hallo-bericht met tags uid:Alice alle registraties met tags uid:Alice; daarom alle Els van apparaten.

## <a name="tag-expressions"></a>Code-expressies
Er zijn ook gevallen waarin een melding heeft tootarget een set met geregistreerde items die niet door een enkel label, maar door een Booleaanse expressie tags is geïdentificeerd.

U kunt een sport-toepassing die een herinnering tooeveryone in Boston over een spel tussen Hallo rood Sox en Cardinals verzendt. Als Hallo client-app wordt geregistreerd labels over interesse in teams en locatie, moet Hallo melding betreffende tooeveryone in Boston die willen Hallo rood Sox of Hallo Cardinals zijn. Dit probleem kan worden uitgedrukt Hello Boole-expressie te volgen:

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

Code-expressies kunnen bevatten alle Booleaanse operators, zoals en (& &), of (|), en niet (!). Ze kunnen ook haakjes bevatten. Code-expressies zijn beperkt too20 labels als ze alleen ORs bevatten; anders zijn ze beperkt too6 labels.

Hier volgt een voorbeeld voor het verzenden van meldingen met code-expressies met Hallo SDK.

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    String userTag = "(location_Boston && !follows_Cardinals)";    

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You want info on hello Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You want info on hello Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
