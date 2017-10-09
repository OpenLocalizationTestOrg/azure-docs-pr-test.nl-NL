---
title: aaaHow toosend gepland meldingen | Microsoft Docs
description: In dit onderwerp wordt beschreven hoe gepland meldingen met Azure Notification Hubs.
services: notification-hubs
documentationcenter: .net
keywords: pushmeldingen, push-melding pushmeldingen plannen
author: ysxu
manager: erikre
editor: 
ms.assetid: 6b718c75-75dd-4c99-aee3-db1288235c1a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 9b3ba715dad6f5d824a615e83f2863b0db47b533
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-send-scheduled-notifications"></a>Procedure: Een geplande meldingen verzenden
## <a name="overview"></a>Overzicht
Als u een scenario waarin u wilt toosend een melding op een bepaald moment in Hallo toekomstige, maar hebben geen een eenvoudige manier toowake van uw back-end-code toosend Hallo melding hebt. Standard-laag Notification Hubs ondersteunt een functie waarmee u meldingen tooschedule too7 dagen in toekomstige Hallo.

Gebruiken bij het verzenden van een melding gewoon Hallo [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) zoals weergegeven in het volgende voorbeeld Hallo-klasse in Hallo Notification Hubs SDK:

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

U kunt ook een eerder geplande melding met behulp van de notificationId annuleren:

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

Er zijn geen limieten op Hallo aantal geplande meldingen die u kunt verzenden.

