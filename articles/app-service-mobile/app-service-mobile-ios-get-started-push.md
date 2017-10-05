---
title: Pushmeldingen toevoegen aan iOS-App met Azure Mobile Apps
description: Informatie over hoe u pushmeldingen verzendt naar uw iOS-app met Azure Mobile Apps.
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
ms.openlocfilehash: 08a8c35b89386bd0dbe7bba406a6985a5a0d7eb8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-ios-app"></a><span data-ttu-id="150ba-103">Pushmeldingen toevoegen aan uw iOS-App</span><span class="sxs-lookup"><span data-stu-id="150ba-103">Add Push Notifications to your iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="150ba-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="150ba-104">Overview</span></span>
<span data-ttu-id="150ba-105">In deze zelfstudie hebt u pushmeldingen toevoegen de [iOS snel starten] project, zodat een pushmelding wordt verzonden naar het apparaat telkens wanneer een record wordt ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="150ba-105">In this tutorial, you add push notifications to the [iOS quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="150ba-106">Als u het gedownloade quick start-serverproject niet gebruikt, moet u het push notification-uitbreidingspakket.</span><span class="sxs-lookup"><span data-stu-id="150ba-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="150ba-107">Zie [werken met de .NET-back-endserver SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="150ba-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

<span data-ttu-id="150ba-108">De [iOS-simulator biedt geen ondersteuning voor pushmeldingen](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="150ba-108">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span> <span data-ttu-id="150ba-109">U moet een fysiek iOS-apparaat en een [Apple Developer Program-lidmaatschap](https://developer.apple.com/programs/ios/).</span><span class="sxs-lookup"><span data-stu-id="150ba-109">You need a physical iOS device and an [Apple Developer Program membership](https://developer.apple.com/programs/ios/).</span></span>

## <span data-ttu-id="150ba-110"><a name="configure-hub"></a>Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="150ba-110"><a name="configure-hub"></a>Configure Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="150ba-111"><a id="register"></a>App voor pushmeldingen registreren</span><span class="sxs-lookup"><span data-stu-id="150ba-111"><a id="register"></a>Register app for push notifications</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="150ba-112">Configureren van Azure om pushmeldingen te verzenden</span><span class="sxs-lookup"><span data-stu-id="150ba-112">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <span data-ttu-id="150ba-113"><a id="update-server"></a>Bijwerken van de back-end om pushmeldingen te verzenden</span><span class="sxs-lookup"><span data-stu-id="150ba-113"><a id="update-server"></a>Update backend to send push notifications</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <span data-ttu-id="150ba-114"><a id="add-push"></a>Pushmeldingen toevoegen aan de app</span><span class="sxs-lookup"><span data-stu-id="150ba-114"><a id="add-push"></a>Add push notifications to app</span></span>
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <span data-ttu-id="150ba-115"><a id="test"></a>Pushmeldingen testen</span><span class="sxs-lookup"><span data-stu-id="150ba-115"><a id="test"></a>Test push notifications</span></span>
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <span data-ttu-id="150ba-116"><a id="more"></a>Meer</span><span class="sxs-lookup"><span data-stu-id="150ba-116"><a id="more"></a>More</span></span>
* <span data-ttu-id="150ba-117">Sjablonen bieden u de flexibiliteit om platformoverschrijdende pushes en gelokaliseerde pushes te verzenden.</span><span class="sxs-lookup"><span data-stu-id="150ba-117">Templates give you flexibility to send cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="150ba-118">[Hoe gebruik iOS-clientbibliotheek voor Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) ziet u hoe u sjablonen registreren.</span><span class="sxs-lookup"><span data-stu-id="150ba-118">[How to Use iOS Client Library for Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) shows you how to register templates.</span></span>

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
<span data-ttu-id="150ba-119">[iOS snel starten]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="150ba-119">[iOS quick start]: app-service-mobile-ios-get-started.md</span></span>
