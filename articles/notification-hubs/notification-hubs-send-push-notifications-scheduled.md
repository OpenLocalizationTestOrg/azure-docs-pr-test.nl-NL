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
# <a name="how-to-send-scheduled-notifications"></a><span data-ttu-id="aa8d2-104">Procedure: Een geplande meldingen verzenden</span><span class="sxs-lookup"><span data-stu-id="aa8d2-104">How To: Send scheduled notifications</span></span>
## <a name="overview"></a><span data-ttu-id="aa8d2-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="aa8d2-105">Overview</span></span>
<span data-ttu-id="aa8d2-106">Als u een scenario waarin u wilt toosend een melding op een bepaald moment in Hallo toekomstige, maar hebben geen een eenvoudige manier toowake van uw back-end-code toosend Hallo melding hebt.</span><span class="sxs-lookup"><span data-stu-id="aa8d2-106">If you have a scenario in which you want toosend a notification at some point in hello future, but do not have an easy way toowake up your back-end code toosend hello notification.</span></span> <span data-ttu-id="aa8d2-107">Standard-laag Notification Hubs ondersteunt een functie waarmee u meldingen tooschedule too7 dagen in toekomstige Hallo.</span><span class="sxs-lookup"><span data-stu-id="aa8d2-107">Standard tier Notification Hubs supports a feature that enables you tooschedule notifications up too7 days in hello future.</span></span>

<span data-ttu-id="aa8d2-108">Gebruiken bij het verzenden van een melding gewoon Hallo [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) zoals weergegeven in het volgende voorbeeld Hallo-klasse in Hallo Notification Hubs SDK:</span><span class="sxs-lookup"><span data-stu-id="aa8d2-108">When sending a notification, simply use hello [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) class in hello Notification Hubs SDK as shown in hello following example:</span></span>

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

<span data-ttu-id="aa8d2-109">U kunt ook een eerder geplande melding met behulp van de notificationId annuleren:</span><span class="sxs-lookup"><span data-stu-id="aa8d2-109">Also, you can cancel a previously scheduled notification using its notificationId:</span></span>

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

<span data-ttu-id="aa8d2-110">Er zijn geen limieten op Hallo aantal geplande meldingen die u kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="aa8d2-110">There are no limits on hello number of scheduled notifications you can send.</span></span>

