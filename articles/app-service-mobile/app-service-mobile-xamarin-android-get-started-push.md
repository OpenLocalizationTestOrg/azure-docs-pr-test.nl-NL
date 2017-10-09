---
title: aaaAdd push notifications tooyour Xamarin.Android-app | Microsoft Docs
description: Meer informatie over hoe toouse Azure App Service en Azure Notification Hubs toosend push notifications tooyour Xamarin.Android-app
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
ms.openlocfilehash: c93d1d0cae06ab15e3e3e5c4b342808b2cd49113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinandroid-app"></a><span data-ttu-id="2abc9-103">Push notifications tooyour Xamarin.Android-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="2abc9-103">Add push notifications tooyour Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="2abc9-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="2abc9-104">Overview</span></span>
<span data-ttu-id="2abc9-105">In deze zelfstudie maakt u een push notifications toohello toevoegen [Xamarin.Android snel starten](app-service-mobile-windows-store-dotnet-get-started.md) project, zodat een push-melding toohello apparaat verzonden telkens wanneer een record wordt ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="2abc9-105">In this tutorial, you add push notifications toohello [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="2abc9-106">Als u geen gebruik Hallo snel starten-serverproject gedownload, u moet Hallo push notification-uitbreidingspakket.</span><span class="sxs-lookup"><span data-stu-id="2abc9-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="2abc9-107">Zie [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2abc9-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2abc9-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2abc9-108">Prerequisites</span></span>
<span data-ttu-id="2abc9-109">Deze zelfstudie vereist de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="2abc9-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="2abc9-110">Een actief Google-account.</span><span class="sxs-lookup"><span data-stu-id="2abc9-110">An active Google account.</span></span> <span data-ttu-id="2abc9-111">U kunt zich aanmelden voor een Google-account bij [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="2abc9-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>
* <span data-ttu-id="2abc9-112">[Google Cloud Messaging-clientonderdeel](http://components.xamarin.com/view/GCMClient/).</span><span class="sxs-lookup"><span data-stu-id="2abc9-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span></span>

## <span data-ttu-id="2abc9-113"><a name="configure-hub"></a>Een Notification Hub configureren</span><span class="sxs-lookup"><span data-stu-id="2abc9-113"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="2abc9-114"><a id="register"></a>Inschakelen van Firebase Cloud-berichten</span><span class="sxs-lookup"><span data-stu-id="2abc9-114"><a id="register"></a>Enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-toosend-push-requests"></a><span data-ttu-id="2abc9-115">Azure toosend push aanvragen configureren</span><span class="sxs-lookup"><span data-stu-id="2abc9-115">Configure Azure toosend push requests</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <span data-ttu-id="2abc9-116"><a id="update-server"></a>Hallo server project toosend-pushmeldingen bijwerken</span><span class="sxs-lookup"><span data-stu-id="2abc9-116"><a id="update-server"></a>Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="2abc9-117"><a id="configure-app"></a>Hallo client-project voor pushmeldingen configureren</span><span class="sxs-lookup"><span data-stu-id="2abc9-117"><a id="configure-app"></a>Configure hello client project for push notifications</span></span>
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <span data-ttu-id="2abc9-118"><a id="add-push"></a>Push notifications code tooyour app toevoegen</span><span class="sxs-lookup"><span data-stu-id="2abc9-118"><a id="add-push"></a>Add push notifications code tooyour app</span></span>
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <span data-ttu-id="2abc9-119"><a name="test"></a>Pushmeldingen testen in uw app</span><span class="sxs-lookup"><span data-stu-id="2abc9-119"><a name="test"></a>Test push notifications in your app</span></span>
<span data-ttu-id="2abc9-120">U kunt Hallo app testen met behulp van een virtueel apparaat in Hallo-emulator.</span><span class="sxs-lookup"><span data-stu-id="2abc9-120">You can test hello app by using a virtual device in hello emulator.</span></span> <span data-ttu-id="2abc9-121">Er zijn extra configuratiestappen vereist wanneer u gebruikmaakt van een emulator.</span><span class="sxs-lookup"><span data-stu-id="2abc9-121">There are additional configuration steps required when running on an emulator.</span></span>

1. <span data-ttu-id="2abc9-122">Zorg ervoor dat u tooor foutopsporing op een virtueel apparaat met Google APIs ingesteld als doel hello implementeert, zoals hieronder wordt weergegeven in Hallo Android Virtual Device (AVD) manager.</span><span class="sxs-lookup"><span data-stu-id="2abc9-122">Make sure that you are deploying tooor debugging on a virtual device that has Google APIs set as hello target, as shown below in hello Android Virtual Device (AVD) manager.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. <span data-ttu-id="2abc9-123">Een apparaat toohello Android van Google-account toevoegen door te klikken op **Apps** > **instellingen** > **account toevoegen**, volg de aanwijzingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="2abc9-123">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. <span data-ttu-id="2abc9-124">Hallo todolist-app als voordat uitvoeren en een nieuwe taak invoegen.</span><span class="sxs-lookup"><span data-stu-id="2abc9-124">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="2abc9-125">Dit moment wordt een pictogram weergegeven in het systeemvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="2abc9-125">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="2abc9-126">U kunt Hallo melding lade tooview Hallo volledige tekst van melding Hallo openen.</span><span class="sxs-lookup"><span data-stu-id="2abc9-126">You can open hello notification drawer tooview hello full text of hello notification.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
