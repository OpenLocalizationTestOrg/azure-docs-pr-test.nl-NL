---
title: Pushmeldingen toevoegen aan uw Xamarin.Android-app | Microsoft Docs
description: Informatie over het gebruik van Azure App Service en Azure Notification Hubs pushmeldingen verzendt naar uw Xamarin.Android-app
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6f7e8517-e532-4559-9b07-874115f4c65b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: c3757d56fb1792092710740dc5ffbd64f18730cf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinandroid-app"></a><span data-ttu-id="8d8e4-103">Pushmeldingen toevoegen aan uw Xamarin.Android-app</span><span class="sxs-lookup"><span data-stu-id="8d8e4-103">Add push notifications to your Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="8d8e4-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="8d8e4-104">Overview</span></span>
<span data-ttu-id="8d8e4-105">In deze zelfstudie hebt u pushmeldingen toevoegen de [Xamarin.Android snel starten](app-service-mobile-windows-store-dotnet-get-started.md) project, zodat een pushmelding wordt verzonden naar het apparaat telkens wanneer een record wordt ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="8d8e4-105">In this tutorial, you add push notifications to the [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="8d8e4-106">Als u het gedownloade quick start-serverproject niet gebruikt, moet u het push notification-uitbreidingspakket.</span><span class="sxs-lookup"><span data-stu-id="8d8e4-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="8d8e4-107">Zie [werken met de .NET-back-endserver SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8d8e4-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d8e4-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8d8e4-108">Prerequisites</span></span>
<span data-ttu-id="8d8e4-109">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="8d8e4-109">This tutorial requires the following:</span></span>

* <span data-ttu-id="8d8e4-110">Een actief Google-account.</span><span class="sxs-lookup"><span data-stu-id="8d8e4-110">An active Google account.</span></span> <span data-ttu-id="8d8e4-111">U kunt zich aanmelden voor een Google-account bij [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="8d8e4-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>
* <span data-ttu-id="8d8e4-112">[Google Cloud Messaging-clientonderdeel](http://components.xamarin.com/view/GCMClient/).</span><span class="sxs-lookup"><span data-stu-id="8d8e4-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span></span>

## <span data-ttu-id="8d8e4-113"><a name="configure-hub"></a>Een Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="8d8e4-113"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="8d8e4-114"><a id="register"></a>Inschakelen van Firebase Cloud-berichten</span><span class="sxs-lookup"><span data-stu-id="8d8e4-114"><a id="register"></a>Enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-to-send-push-requests"></a><span data-ttu-id="8d8e4-115">Azure voor het verzenden van pushmeldingen aanvragen configureren</span><span class="sxs-lookup"><span data-stu-id="8d8e4-115">Configure Azure to send push requests</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <span data-ttu-id="8d8e4-116"><a id="update-server"></a>Bijwerken van het serverproject om pushmeldingen te verzenden</span><span class="sxs-lookup"><span data-stu-id="8d8e4-116"><a id="update-server"></a>Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="8d8e4-117"><a id="configure-app"></a>Het clientproject voor pushmeldingen configureren</span><span class="sxs-lookup"><span data-stu-id="8d8e4-117"><a id="configure-app"></a>Configure the client project for push notifications</span></span>
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <span data-ttu-id="8d8e4-118"><a id="add-push"></a>Push notifications code toevoegen aan uw app</span><span class="sxs-lookup"><span data-stu-id="8d8e4-118"><a id="add-push"></a>Add push notifications code to your app</span></span>
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <span data-ttu-id="8d8e4-119"><a name="test"></a>Pushmeldingen testen in uw app</span><span class="sxs-lookup"><span data-stu-id="8d8e4-119"><a name="test"></a>Test push notifications in your app</span></span>
<span data-ttu-id="8d8e4-120">U kunt de app testen met behulp van een virtueel apparaat in de emulator.</span><span class="sxs-lookup"><span data-stu-id="8d8e4-120">You can test the app by using a virtual device in the emulator.</span></span> <span data-ttu-id="8d8e4-121">Er zijn extra configuratiestappen vereist wanneer u gebruikmaakt van een emulator.</span><span class="sxs-lookup"><span data-stu-id="8d8e4-121">There are additional configuration steps required when running on an emulator.</span></span>

1. <span data-ttu-id="8d8e4-122">Zorg ervoor dat u implementeert voor of foutopsporing op een virtueel apparaat met Google APIs ingesteld als doel, zoals hieronder wordt weergegeven in de Android Virtual Device (AVD) manager.</span><span class="sxs-lookup"><span data-stu-id="8d8e4-122">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device (AVD) manager.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. <span data-ttu-id="8d8e4-123">Een Google-account toevoegen aan de Android-apparaat door te klikken op **Apps** > **instellingen** > **account toevoegen**, volg de instructies.</span><span class="sxs-lookup"><span data-stu-id="8d8e4-123">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. <span data-ttu-id="8d8e4-124">Voer de todolist-app als voordat en een nieuwe taak invoegen.</span><span class="sxs-lookup"><span data-stu-id="8d8e4-124">Run the todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="8d8e4-125">Dit moment wordt een pictogram weergegeven in het systeemvak.</span><span class="sxs-lookup"><span data-stu-id="8d8e4-125">This time, a notification icon is displayed in the notification area.</span></span> <span data-ttu-id="8d8e4-126">U kunt de meldingenlijst om weer te geven van de volledige tekst van de melding openen.</span><span class="sxs-lookup"><span data-stu-id="8d8e4-126">You can open the notification drawer to view the full text of the notification.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
