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
# <a name="routing-and-tag-expressions"></a><span data-ttu-id="e81e6-103">Routering en code-expressies</span><span class="sxs-lookup"><span data-stu-id="e81e6-103">Routing and tag expressions</span></span>
## <a name="overview"></a><span data-ttu-id="e81e6-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="e81e6-104">Overview</span></span>
<span data-ttu-id="e81e6-105">Code-expressies kunnen u bepaalde groepen van apparaten of meer specifiek registraties tootarget bij het verzenden van een push-melding via Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="e81e6-105">Tag expressions enable you tootarget specific sets of devices, or more specifically registrations, when sending a push notification through Notification Hubs.</span></span>

## <a name="targeting-specific-registrations"></a><span data-ttu-id="e81e6-106">Die gericht is op specifieke registraties</span><span class="sxs-lookup"><span data-stu-id="e81e6-106">Targeting specific registrations</span></span>
<span data-ttu-id="e81e6-107">Hallo alleen manier tootarget specifieke notification registraties tooassociate labels, wordt vervolgens gericht zijn op deze labels.</span><span class="sxs-lookup"><span data-stu-id="e81e6-107">hello only way tootarget specific notification registrations is tooassociate tags with them, then target those tags.</span></span> <span data-ttu-id="e81e6-108">Zoals beschreven in [registratie Management](notification-hubs-push-notification-registration-management.md), in volgorde tooreceive push meldingen is tooregister een apparaat een app verwerken op een notification hub.</span><span class="sxs-lookup"><span data-stu-id="e81e6-108">As discussed in [Registration Management](notification-hubs-push-notification-registration-management.md), in order tooreceive push notifications an app has tooregister a device handle on a notification hub.</span></span> <span data-ttu-id="e81e6-109">Zodra een registratie op een notification hub is gemaakt, kunt Hallo toepassing backend push notifications tooit verzenden.</span><span class="sxs-lookup"><span data-stu-id="e81e6-109">Once a registration is created on a notification hub, hello application backend can send push notifications tooit.</span></span>
<span data-ttu-id="e81e6-110">Hallo toepassing back-end kunt Hallo registraties tootarget met een specifieke melding in de volgende manieren Hallo kiezen:</span><span class="sxs-lookup"><span data-stu-id="e81e6-110">hello application backend can choose hello registrations tootarget with a specific notification in hello following ways:</span></span>

1. <span data-ttu-id="e81e6-111">**Uitzenden**: alle registraties in Hallo notification hub Hallo ontvangen.</span><span class="sxs-lookup"><span data-stu-id="e81e6-111">**Broadcast**: all registrations in hello notification hub receive hello notification.</span></span>
2. <span data-ttu-id="e81e6-112">**Tag**: alle registraties met Hallo opgegeven tag Hallo ontvangen.</span><span class="sxs-lookup"><span data-stu-id="e81e6-112">**Tag**: all registrations that contain hello specified tag receive hello notification.</span></span>
3. <span data-ttu-id="e81e6-113">**Expressie labelen**: alle registraties waarvan reeks labels overeen Hallo opgegeven expressie Hallo ontvangen.</span><span class="sxs-lookup"><span data-stu-id="e81e6-113">**Tag expression**: all registrations whose set of tags match hello specified expression receive hello notification.</span></span>

## <a name="tags"></a><span data-ttu-id="e81e6-114">Tags</span><span class="sxs-lookup"><span data-stu-id="e81e6-114">Tags</span></span>
<span data-ttu-id="e81e6-115">Een label kunt een willekeurige tekenreeks, up too120 tekens, met alfanumerieke en Hallo volgende niet-alfanumerieke tekens: '_', ' @', '#', '. ',':', '-'.</span><span class="sxs-lookup"><span data-stu-id="e81e6-115">A tag can be any string, up too120 characters, containing alphanumeric and hello following non-alphanumeric characters: ‘_’, ‘@’, ‘#’, ‘.’, ‘:’, ‘-’.</span></span> <span data-ttu-id="e81e6-116">Hallo volgende voorbeeld ziet u een toepassing waaruit u de pop-upmeldingen over specifieke muziekgroepen kunt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="e81e6-116">hello following example shows an application from which you can receive toast notifications about specific music groups.</span></span> <span data-ttu-id="e81e6-117">In dit scenario is een eenvoudige manier tooroute meldingen toolabel registraties met labels die verschillende stroken hello, zoals in de volgende afbeelding Hallo vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="e81e6-117">In this scenario, a simple way tooroute notifications is toolabel registrations with tags that represent hello different bands, as in hello following picture.</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

<span data-ttu-id="e81e6-118">In deze afbeelding Hallo-bericht met tags **Beatles** bereikt alleen Hallo tablet gebruikt dat geregistreerd met de Hallo code **Beatles**.</span><span class="sxs-lookup"><span data-stu-id="e81e6-118">In this picture, hello message tagged **Beatles** reaches only hello tablet that registered with hello tag **Beatles**.</span></span>

<span data-ttu-id="e81e6-119">Zie voor meer informatie over het maken van rapporten voor tags [registratie Management](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="e81e6-119">For more information about creating registrations for tags, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

<span data-ttu-id="e81e6-120">U kunt verzenden meldingen tootags Hallo met verzenden van meldingen methoden Hallo `Microsoft.Azure.NotificationHubs.NotificationHubClient` klasse in Hallo [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span><span class="sxs-lookup"><span data-stu-id="e81e6-120">You can send notifications tootags using hello send notifications methods of hello `Microsoft.Azure.NotificationHubs.NotificationHubClient` class in hello [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span></span> <span data-ttu-id="e81e6-121">U kunt ook gebruik van Node.js of Hallo Push Notifications REST-API's.</span><span class="sxs-lookup"><span data-stu-id="e81e6-121">You can also use Node.js, or hello Push Notifications REST APIs.</span></span>  <span data-ttu-id="e81e6-122">Hier volgt een voorbeeld van Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="e81e6-122">Here's an example using hello SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




<span data-ttu-id="e81e6-123">Labels hebben geen toobe vooraf is ingericht en toomultiple app-specifiek concepten kunnen verwijzen.</span><span class="sxs-lookup"><span data-stu-id="e81e6-123">Tags do not have toobe pre-provisioned and can refer toomultiple app-specific concepts.</span></span> <span data-ttu-id="e81e6-124">Gebruikers van deze voorbeeldtoepassing kunnen bijvoorbeeld becommentariëren stroken en wilt tooreceive toasts, niet alleen voor opmerkingen op hun favoriete stroken hello, maar ook voor alle opmerkingen van vrienden, ongeacht het Hallo-band waarop ze zijn opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="e81e6-124">For example, users of this example application can comment on bands and want tooreceive toasts, not only for hello comments on their favorite bands, but also for all comments from their friends, regardless of hello band on which they are commenting.</span></span> <span data-ttu-id="e81e6-125">Hallo volgende afbeelding toont een voorbeeld van dit scenario:</span><span class="sxs-lookup"><span data-stu-id="e81e6-125">hello following picture shows an example of this scenario:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

<span data-ttu-id="e81e6-126">In deze afbeelding Els is geïnteresseerd in updates voor Hallo Beatles en Bob is geïnteresseerd in updates voor Hallo Wailers.</span><span class="sxs-lookup"><span data-stu-id="e81e6-126">In this picture, Alice is interested in updates for hello Beatles, and Bob is interested in updates for hello Wailers.</span></span> <span data-ttu-id="e81e6-127">Bob is ook geïnteresseerd in de Charlie opmerkingen en Charlie is geïnteresseerd in Hallo Wailers.</span><span class="sxs-lookup"><span data-stu-id="e81e6-127">Bob is also interested in Charlie’s comments, and Charlie is in interested in hello Wailers.</span></span> <span data-ttu-id="e81e6-128">Wanneer een melding wordt verzonden om de Charlie Opmerking bij Hallo Beatles, ontvangen zowel Alice en Bob.</span><span class="sxs-lookup"><span data-stu-id="e81e6-128">When a notification is sent for Charlie’s comment on hello Beatles, both Alice and Bob receive it.</span></span>

<span data-ttu-id="e81e6-129">U kunt meerdere problemen in de codes (bijvoorbeeld 'band_Beatles' of 'follows_Charlie') codeert, zijn tags eenvoudige tekenreeksen en niet-eigenschappen met waarden.</span><span class="sxs-lookup"><span data-stu-id="e81e6-129">While you can encode multiple concerns in tags (for example, “band_Beatles” or “follows_Charlie”), tags are simple strings and not properties with values.</span></span> <span data-ttu-id="e81e6-130">Een registratie wordt alleen op Hallo aanwezigheid of afwezigheid van een specifieke tag gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="e81e6-130">A registration is matched only on hello presence or absence of a specific tag.</span></span>

<span data-ttu-id="e81e6-131">Zie voor een volledige stapsgewijze zelfstudie over hoe toouse-tags voor het verzenden van toointerest groepen, [nieuws op te splitsen](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span><span class="sxs-lookup"><span data-stu-id="e81e6-131">For a full step-by-step tutorial on how toouse tags for sending toointerest groups, see [Breaking News](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span></span>

## <a name="using-tags-tootarget-users"></a><span data-ttu-id="e81e6-132">Met behulp van de labels tootarget gebruikers</span><span class="sxs-lookup"><span data-stu-id="e81e6-132">Using tags tootarget users</span></span>
<span data-ttu-id="e81e6-133">Een andere manier toouse tags is tooidentify alle Hallo op apparaten van een bepaalde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e81e6-133">Another way toouse tags is tooidentify all hello devices of a particular user.</span></span> <span data-ttu-id="e81e6-134">Registraties worden gelabeld met een tag met een gebruikersnaam, zoals in de volgende afbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="e81e6-134">Registrations can be tagged with a tag that contains a user id, as in hello following picture:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

<span data-ttu-id="e81e6-135">In deze afbeelding bereikt Hallo-bericht met tags uid:Alice alle registraties met tags uid:Alice; daarom alle Els van apparaten.</span><span class="sxs-lookup"><span data-stu-id="e81e6-135">In this picture, hello message tagged uid:Alice reaches all registrations tagged uid:Alice; hence, all of Alice’s devices.</span></span>

## <a name="tag-expressions"></a><span data-ttu-id="e81e6-136">Code-expressies</span><span class="sxs-lookup"><span data-stu-id="e81e6-136">Tag expressions</span></span>
<span data-ttu-id="e81e6-137">Er zijn ook gevallen waarin een melding heeft tootarget een set met geregistreerde items die niet door een enkel label, maar door een Booleaanse expressie tags is geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="e81e6-137">There are cases in which a notification has tootarget a set of registrations that is identified not by a single tag, but by a Boolean expression on tags.</span></span>

<span data-ttu-id="e81e6-138">U kunt een sport-toepassing die een herinnering tooeveryone in Boston over een spel tussen Hallo rood Sox en Cardinals verzendt.</span><span class="sxs-lookup"><span data-stu-id="e81e6-138">Consider a sports application that sends a reminder tooeveryone in Boston about a game between hello Red Sox and Cardinals.</span></span> <span data-ttu-id="e81e6-139">Als Hallo client-app wordt geregistreerd labels over interesse in teams en locatie, moet Hallo melding betreffende tooeveryone in Boston die willen Hallo rood Sox of Hallo Cardinals zijn.</span><span class="sxs-lookup"><span data-stu-id="e81e6-139">If hello client app registers tags about interest in teams and location, then hello notification should be targeted tooeveryone in Boston who is interested in either hello Red Sox or hello Cardinals.</span></span> <span data-ttu-id="e81e6-140">Dit probleem kan worden uitgedrukt Hello Boole-expressie te volgen:</span><span class="sxs-lookup"><span data-stu-id="e81e6-140">This condition can be expressed with hello following Boolean expression:</span></span>

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

<span data-ttu-id="e81e6-141">Code-expressies kunnen bevatten alle Booleaanse operators, zoals en (& &), of (|), en niet (!).</span><span class="sxs-lookup"><span data-stu-id="e81e6-141">Tag expressions can contain all Boolean operators, such as AND (&&), OR (||), and NOT (!).</span></span> <span data-ttu-id="e81e6-142">Ze kunnen ook haakjes bevatten.</span><span class="sxs-lookup"><span data-stu-id="e81e6-142">They can also contain parentheses.</span></span> <span data-ttu-id="e81e6-143">Code-expressies zijn beperkt too20 labels als ze alleen ORs bevatten; anders zijn ze beperkt too6 labels.</span><span class="sxs-lookup"><span data-stu-id="e81e6-143">Tag expressions are limited too20 tags if they contain only ORs; otherwise they are limited too6 tags.</span></span>

<span data-ttu-id="e81e6-144">Hier volgt een voorbeeld voor het verzenden van meldingen met code-expressies met Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="e81e6-144">Here's an example for sending notifications with tag expressions using hello SDK.</span></span>

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
