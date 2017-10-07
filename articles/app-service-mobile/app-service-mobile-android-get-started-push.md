---
title: aaaAdd push notifications tooyour Android-app voor Mobile Apps | Microsoft Docs
description: Meer informatie over hoe toouse Mobile Apps toosend push-meldingen tooyour Android-app.
services: app-service\mobile
documentationcenter: android
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 9058ed6d-e871-4179-86af-0092d0ca09d3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: dcfb8463b395904b4bd0bf9bde2f71f259894066
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-android-app"></a><span data-ttu-id="a86c6-103">Push tooyour Android-app-meldingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="a86c6-103">Add push notifications tooyour Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="a86c6-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="a86c6-104">Overview</span></span>
<span data-ttu-id="a86c6-105">In deze zelfstudie maakt u een push notifications toohello toevoegen [Android snel starten] project, zodat een push-melding toohello apparaat verzonden telkens wanneer een record wordt ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="a86c6-105">In this tutorial, you add push notifications toohello [Android quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="a86c6-106">Als u geen gebruik Hallo gedownload serverproject snel starten, moet u push notification-uitbreidingspakket Hallo.</span><span class="sxs-lookup"><span data-stu-id="a86c6-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="a86c6-107">Zie voor meer informatie [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="a86c6-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a86c6-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a86c6-108">Prerequisites</span></span>
<span data-ttu-id="a86c6-109">U hebt Hallo volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="a86c6-109">You need hello following:</span></span>

* <span data-ttu-id="a86c6-110">Een IDE, afhankelijk van de back-end van uw project:</span><span class="sxs-lookup"><span data-stu-id="a86c6-110">An IDE, depending on your project's back end:</span></span>

  * <span data-ttu-id="a86c6-111">[Android Studio](https://developer.android.com/sdk/index.html) als deze app een back-end voor Node.js heeft.</span><span class="sxs-lookup"><span data-stu-id="a86c6-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span></span>
  * <span data-ttu-id="a86c6-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) of hoger als deze app een Microsoft .NET-back-end heeft.</span><span class="sxs-lookup"><span data-stu-id="a86c6-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span></span>
* <span data-ttu-id="a86c6-113">Android 2.3 of hoger, Google opslagplaats revisie 27 of hoger en Google Play-Services 9.0.2 of hoger voor Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="a86c6-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="a86c6-114">Volledige Hallo [Android snel starten].</span><span class="sxs-lookup"><span data-stu-id="a86c6-114">Complete hello [Android quick start].</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="a86c6-115">Een project maken dat Firebase Cloud Messaging ondersteunt</span><span class="sxs-lookup"><span data-stu-id="a86c6-115">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a><span data-ttu-id="a86c6-116">Een notification hub configureren</span><span class="sxs-lookup"><span data-stu-id="a86c6-116">Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="a86c6-117">Azure toosend-pushmeldingen configureren</span><span class="sxs-lookup"><span data-stu-id="a86c6-117">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-hello-server-project"></a><span data-ttu-id="a86c6-118">Pushmeldingen voor Hallo serverproject inschakelen</span><span class="sxs-lookup"><span data-stu-id="a86c6-118">Enable push notifications for hello server project</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-tooyour-app"></a><span data-ttu-id="a86c6-119">Push notifications tooyour app toevoegen</span><span class="sxs-lookup"><span data-stu-id="a86c6-119">Add push notifications tooyour app</span></span>
<span data-ttu-id="a86c6-120">In deze sectie kunt u uw Android-app voor client toohandle pushmeldingen bijwerken.</span><span class="sxs-lookup"><span data-stu-id="a86c6-120">In this section, you update your client Android app toohandle push notifications.</span></span>

### <a name="verify-android-sdk-version"></a><span data-ttu-id="a86c6-121">Controleer of de Android SDK-versie</span><span class="sxs-lookup"><span data-stu-id="a86c6-121">Verify Android SDK version</span></span>
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

<span data-ttu-id="a86c6-122">De volgende stap is tooinstall Google Play-services.</span><span class="sxs-lookup"><span data-stu-id="a86c6-122">Your next step is tooinstall Google Play services.</span></span> <span data-ttu-id="a86c6-123">Google Cloud Messaging heeft bepaalde minimale API-niveau vereisten voor het ontwikkelen en testen, welke Hallo **minSdkVersion** eigenschap in het manifest Hallo moet voldoen aan.</span><span class="sxs-lookup"><span data-stu-id="a86c6-123">Google Cloud Messaging has some minimum API level requirements for development and testing, which hello **minSdkVersion** property in hello manifest must conform to.</span></span>

<span data-ttu-id="a86c6-124">Als u met een oudere apparaat testen wilt, raadpleegt u [ingesteld van Google Play Services SDK] toodetermine hoe lage u kunt deze waarde instellen en juist instellen.</span><span class="sxs-lookup"><span data-stu-id="a86c6-124">If you are testing with an older device, consult [Set Up Google Play Services SDK] toodetermine how low you can set this value, and set it appropriately.</span></span>

### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="a86c6-125">Google Play services toohello project toevoegen</span><span class="sxs-lookup"><span data-stu-id="a86c6-125">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a><span data-ttu-id="a86c6-126">Voeg code toe</span><span class="sxs-lookup"><span data-stu-id="a86c6-126">Add code</span></span>
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-hello-app-against-hello-published-mobile-service"></a><span data-ttu-id="a86c6-127">Test Hallo app tegen Hallo gepubliceerd mobiele service</span><span class="sxs-lookup"><span data-stu-id="a86c6-127">Test hello app against hello published mobile service</span></span>
<span data-ttu-id="a86c6-128">U kunt Hallo app testen door het koppelen van een Android-telefoon met een USB-kabel rechtstreeks of via een virtueel apparaat in Hallo-emulator.</span><span class="sxs-lookup"><span data-stu-id="a86c6-128">You can test hello app by directly attaching an Android phone with a USB cable, or by using a virtual device in hello emulator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a86c6-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a86c6-129">Next steps</span></span>
<span data-ttu-id="a86c6-130">Nu dat u deze zelfstudie hebt voltooid, kunt u overwegen tooone Hallo volgende zelfstudies verder te gaan:</span><span class="sxs-lookup"><span data-stu-id="a86c6-130">Now that you completed this tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="a86c6-131">[Verificatie tooyour Android-app toevoegen](app-service-mobile-android-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="a86c6-131">[Add authentication tooyour Android app](app-service-mobile-android-get-started-users.md).</span></span>
  <span data-ttu-id="a86c6-132">Meer informatie over hoe tooadd verificatie toohello todolist Quick Start-project op Android met behulp van een ondersteunde id-provider.</span><span class="sxs-lookup"><span data-stu-id="a86c6-132">Learn how tooadd authentication toohello todolist quickstart project on Android using a supported identity provider.</span></span>
* <span data-ttu-id="a86c6-133">[Offlinesynchronisatie voor uw Android-app inschakelen](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="a86c6-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="a86c6-134">Meer informatie over hoe de offline tooadd tooyour app met behulp van een back-end van Mobile Apps ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="a86c6-134">Learn how tooadd offline support tooyour app by using a Mobile Apps back end.</span></span> <span data-ttu-id="a86c6-135">Met het offline synchroniseren gebruikers kunnen communiceren met een mobiele app&mdash;weergeven, toevoegen of wijzigen van gegevens&mdash;zelfs wanneer er geen netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="a86c6-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs -->
[Android snel starten]: app-service-mobile-android-get-started.md

[ingesteld van Google Play Services SDK]:https://developers.google.com/android/guides/setup
