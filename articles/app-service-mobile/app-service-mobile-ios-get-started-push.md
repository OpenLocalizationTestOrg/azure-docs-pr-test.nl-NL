---
title: aaaAdd Pushmeldingen tooiOS App met Azure Mobile Apps
description: Meer informatie over hoe Azure Mobile Apps-toosend toouse push-meldingen tooyour iOS-app.
services: app-service\mobile
documentationcenter: ios
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: fa503833-d23e-4925-8d93-341bb3fbab7d
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/10/2016
ms.author: glenga
ms.openlocfilehash: 11588c56bc8987a71257dbad4fcdebf1b3209b1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-ios-app"></a><span data-ttu-id="557c5-103">IOS-Pushmeldingen tooyour App toevoegen</span><span class="sxs-lookup"><span data-stu-id="557c5-103">Add Push Notifications tooyour iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="557c5-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="557c5-104">Overview</span></span>
<span data-ttu-id="557c5-105">In deze zelfstudie maakt u een push notifications toohello toevoegen [iOS snel starten] project, zodat een push-melding toohello apparaat verzonden telkens wanneer een record wordt ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="557c5-105">In this tutorial, you add push notifications toohello [iOS quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="557c5-106">Als u geen gebruik Hallo snel starten-serverproject gedownload, u moet Hallo push notification-uitbreidingspakket.</span><span class="sxs-lookup"><span data-stu-id="557c5-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="557c5-107">Zie [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="557c5-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

<span data-ttu-id="557c5-108">Hallo [iOS-simulator biedt geen ondersteuning voor pushmeldingen](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="557c5-108">hello [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span> <span data-ttu-id="557c5-109">U moet een fysiek iOS-apparaat en een [Apple Developer Program-lidmaatschap](https://developer.apple.com/programs/ios/).</span><span class="sxs-lookup"><span data-stu-id="557c5-109">You need a physical iOS device and an [Apple Developer Program membership](https://developer.apple.com/programs/ios/).</span></span>

## <span data-ttu-id="557c5-110"><a name="configure-hub"></a>Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="557c5-110"><a name="configure-hub"></a>Configure Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="557c5-111"><a id="register"></a>App voor pushmeldingen registreren</span><span class="sxs-lookup"><span data-stu-id="557c5-111"><a id="register"></a>Register app for push notifications</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="557c5-112">Azure toosend-pushmeldingen configureren</span><span class="sxs-lookup"><span data-stu-id="557c5-112">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <span data-ttu-id="557c5-113"><a id="update-server"></a>Back-end toosend pushmeldingen bijwerken</span><span class="sxs-lookup"><span data-stu-id="557c5-113"><a id="update-server"></a>Update backend toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <span data-ttu-id="557c5-114"><a id="add-push"></a>Push notifications tooapp toevoegen</span><span class="sxs-lookup"><span data-stu-id="557c5-114"><a id="add-push"></a>Add push notifications tooapp</span></span>
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <span data-ttu-id="557c5-115"><a id="test"></a>Pushmeldingen testen</span><span class="sxs-lookup"><span data-stu-id="557c5-115"><a id="test"></a>Test push notifications</span></span>
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <span data-ttu-id="557c5-116"><a id="more"></a>Meer</span><span class="sxs-lookup"><span data-stu-id="557c5-116"><a id="more"></a>More</span></span>
* <span data-ttu-id="557c5-117">Sjablonen bieden u de flexibiliteit toosend platformoverschrijdende pushes en gelokaliseerde pushes.</span><span class="sxs-lookup"><span data-stu-id="557c5-117">Templates give you flexibility toosend cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="557c5-118">[Hoe tooUse iOS-clientbibliotheek voor Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) laat u zien hoe tooregister sjablonen.</span><span class="sxs-lookup"><span data-stu-id="557c5-118">[How tooUse iOS Client Library for Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) shows you how tooregister templates.</span></span>

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
[iOS snel starten]: app-service-mobile-ios-get-started.md
