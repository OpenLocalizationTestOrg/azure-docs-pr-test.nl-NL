---
title: aaaAdd Pushmeldingen tooApache Cordova-App met Azure Mobile Apps | Microsoft Docs
description: Meer informatie over hoe Azure Mobile Apps-toosend toouse push-meldingen tooyour Apache Cordova-app.
services: app-service\mobile
documentationcenter: javascript
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 92c596a9-875c-4840-b0e1-69198817576f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 8e1b23d6145b446b6f01599337b677e2f2b31d7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a><span data-ttu-id="b33c4-103">Push notifications tooyour Apache Cordova-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="b33c4-103">Add push notifications tooyour Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="b33c4-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b33c4-104">Overview</span></span>
<span data-ttu-id="b33c4-105">In deze zelfstudie maakt toevoegen u push notifications toohello [Apache Cordova snel starten] project, zodat een push-melding toohello apparaat verzonden telkens wanneer een record wordt ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="b33c4-105">In this tutorial, you add push notifications toohello [Apache Cordova quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="b33c4-106">Als u geen gebruik Hallo gedownload serverproject snel starten, moet u push notification-uitbreidingspakket Hallo.</span><span class="sxs-lookup"><span data-stu-id="b33c4-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="b33c4-107">Zie voor meer informatie [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="b33c4-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

## <span data-ttu-id="b33c4-108"><a name="prerequisites"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="b33c4-108"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="b33c4-109">Deze zelfstudie bevat informatie over een Apache Cordova-toepassing die is ontwikkeld met Visual Studio 2015 die wordt uitgevoerd op Hallo Google Android-Emulator, een Android-apparaat, een Windows-apparaat en een iOS-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b33c4-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on hello Google Android Emulator, an Android device, a Windows device, and an iOS device.</span></span>

<span data-ttu-id="b33c4-110">toocomplete deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="b33c4-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="b33c4-111">Een PC met [Visual Studio Community 2015] [ 2] of hoger.</span><span class="sxs-lookup"><span data-stu-id="b33c4-111">A PC with [Visual Studio Community 2015][2] or later versions.</span></span>
* <span data-ttu-id="b33c4-112">[Visual Studio Tools voor Apache Cordova][4].</span><span class="sxs-lookup"><span data-stu-id="b33c4-112">[Visual Studio Tools for Apache Cordova][4].</span></span>
* <span data-ttu-id="b33c4-113">Een [actief Azure-account][3].</span><span class="sxs-lookup"><span data-stu-id="b33c4-113">An [active Azure account][3].</span></span>
* <span data-ttu-id="b33c4-114">Een voltooide [snel starten van Apache Cordova] [ 5] project.</span><span class="sxs-lookup"><span data-stu-id="b33c4-114">A completed [Apache Cordova quick start][5] project.</span></span>
* <span data-ttu-id="b33c4-115">(Android) Een [Google-account] [ 6] met een geverifieerde e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="b33c4-115">(Android) A [Google account][6] with a verified email address.</span></span>
* <span data-ttu-id="b33c4-116">(iOS) Een [Apple Developer Program-lidmaatschap] [ 7] en een iOS-apparaat (iOS-Simulator biedt geen ondersteuning voor pushmeldingen).</span><span class="sxs-lookup"><span data-stu-id="b33c4-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span></span>
* <span data-ttu-id="b33c4-117">(Windows) Een [Windows Store-ontwikkelaarsaccount] [ 8] en een Windows 10-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b33c4-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span></span>

## <span data-ttu-id="b33c4-118"><a name="configure-hub"></a>Een notification hub configureren</span><span class="sxs-lookup"><span data-stu-id="b33c4-118"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

<span data-ttu-id="b33c4-119">[Bekijk een video waarin de stappen in deze sectie][9]</span><span class="sxs-lookup"><span data-stu-id="b33c4-119">[Watch a video showing steps in this section][9]</span></span>

## <a name="update-hello-server-project"></a><span data-ttu-id="b33c4-120">Hallo serverproject bijwerken</span><span class="sxs-lookup"><span data-stu-id="b33c4-120">Update hello server project</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="b33c4-121"><a name="add-push-to-app"></a>Uw Cordova-app wijzigen</span><span class="sxs-lookup"><span data-stu-id="b33c4-121"><a name="add-push-to-app"></a>Modify your Cordova app</span></span>
<span data-ttu-id="b33c4-122">Zorg ervoor dat uw Apache Cordova-app-project is gereed toohandle pushmeldingen installeren Hallo Cordova push-invoegtoepassing plus de platform-specifieke pushservices.</span><span class="sxs-lookup"><span data-stu-id="b33c4-122">Ensure your Apache Cordova app project is ready toohandle push notifications by installing hello Cordova push plugin plus any platform-specific push services.</span></span>

#### <a name="update-hello-cordova-version-in-your-project"></a><span data-ttu-id="b33c4-123">Hallo Cordova-versie in uw project te werken.</span><span class="sxs-lookup"><span data-stu-id="b33c4-123">Update hello Cordova version in your project.</span></span>
<span data-ttu-id="b33c4-124">Werk de Hallo clientproject als uw project een Apache Cordova-versie die ouder zijn dan v6.1.1 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b33c4-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update hello client project.</span></span> <span data-ttu-id="b33c4-125">tooupdate hello project:</span><span class="sxs-lookup"><span data-stu-id="b33c4-125">tooupdate hello project:</span></span>

* <span data-ttu-id="b33c4-126">Met de rechtermuisknop op `config.xml` tooopen Hallo configuration designer.</span><span class="sxs-lookup"><span data-stu-id="b33c4-126">Right-click `config.xml` tooopen hello configuration designer.</span></span>
* <span data-ttu-id="b33c4-127">Selecteer Hallo Platforms tabblad.</span><span class="sxs-lookup"><span data-stu-id="b33c4-127">Select hello Platforms tab.</span></span>
* <span data-ttu-id="b33c4-128">Kies 6.1.1 in Hallo **Cordova CLI** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="b33c4-128">Choose 6.1.1 in hello **Cordova CLI** text box.</span></span>
* <span data-ttu-id="b33c4-129">Kies **bouwen**, klikt u vervolgens **Build Solution** tooupdate Hallo project.</span><span class="sxs-lookup"><span data-stu-id="b33c4-129">Choose **Build**, then **Build Solution** tooupdate hello project.</span></span>

#### <a name="install-hello-push-plugin"></a><span data-ttu-id="b33c4-130">Hallo push-invoegtoepassing installeren</span><span class="sxs-lookup"><span data-stu-id="b33c4-130">Install hello push plugin</span></span>
<span data-ttu-id="b33c4-131">Apache Cordova-toepassingen verwerken niet systeemeigen apparaat- of -mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="b33c4-131">Apache Cordova applications do not natively handle device or network capabilities.</span></span>  <span data-ttu-id="b33c4-132">Deze mogelijkheden worden geleverd door invoegtoepassingen die zijn gepubliceerd op [npm] [ 10] of op GitHub.</span><span class="sxs-lookup"><span data-stu-id="b33c4-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span></span>  <span data-ttu-id="b33c4-133">Hallo `phonegap-plugin-push` invoegtoepassing gebruikte toohandle netwerk pushmeldingen is.</span><span class="sxs-lookup"><span data-stu-id="b33c4-133">hello `phonegap-plugin-push` plugin is used toohandle network push notifications.</span></span>

<span data-ttu-id="b33c4-134">U kunt Hallo push-invoegtoepassing installeren in een van de volgende manieren:</span><span class="sxs-lookup"><span data-stu-id="b33c4-134">You can install hello push plugin in one of these ways:</span></span>

<span data-ttu-id="b33c4-135">**Hallo vanaf de opdrachtprompt:**</span><span class="sxs-lookup"><span data-stu-id="b33c4-135">**From hello command-prompt:**</span></span>

<span data-ttu-id="b33c4-136">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b33c4-136">Execute hello following command:</span></span>

    cordova plugin add phonegap-plugin-push

<span data-ttu-id="b33c4-137">**Uit vanuit Visual Studio:**</span><span class="sxs-lookup"><span data-stu-id="b33c4-137">**From within Visual Studio:**</span></span>

1. <span data-ttu-id="b33c4-138">Open in Solution Explorer Hallo `config.xml` bestand Klik **Plugins** > **aangepaste**, selecteer **Git** als de installatiebron, voer dan `https://github.com/phonegap/phonegap-plugin-push`als Hallo bron.</span><span class="sxs-lookup"><span data-stu-id="b33c4-138">In Solution Explorer, open hello `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as hello source.</span></span>

   ![][img1]

2. <span data-ttu-id="b33c4-139">Klik op Hallo pijl volgende toohello installatiebron.</span><span class="sxs-lookup"><span data-stu-id="b33c4-139">Click hello arrow next toohello installation source.</span></span>
3. <span data-ttu-id="b33c4-140">In **SENDER_ID**, hebt u al een numerieke project-ID voor Hallo Google Developer-Console-project, u kunt u deze hier toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b33c4-140">In **SENDER_ID**, if you already have a numeric project ID for hello Google Developer Console project, you can add it here.</span></span> <span data-ttu-id="b33c4-141">Anders, voer een aanduidingswaarde van de tijdelijke, zoals 777777.</span><span class="sxs-lookup"><span data-stu-id="b33c4-141">Otherwise, enter a placeholder value, like 777777.</span></span>  <span data-ttu-id="b33c4-142">Als u voor Android ontwikkelt, kunt u deze waarde in config.xml later bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b33c4-142">If you are targeting Android, you can update this value in config.xml later.</span></span>
4. <span data-ttu-id="b33c4-143">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="b33c4-143">Click **Add**.</span></span>

<span data-ttu-id="b33c4-144">Hallo push-invoegtoepassing is nu geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b33c4-144">hello push plugin is now installed.</span></span>

#### <a name="install-hello-device-plugin"></a><span data-ttu-id="b33c4-145">Hallo apparaat invoegtoepassing installeren</span><span class="sxs-lookup"><span data-stu-id="b33c4-145">Install hello device plugin</span></span>
<span data-ttu-id="b33c4-146">Volg dezelfde Hallo procedure tooinstall Hallo push-invoegtoepassing die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b33c4-146">Follow hello same procedure you used tooinstall hello push plugin.</span></span>  <span data-ttu-id="b33c4-147">Hallo apparaat invoegtoepassing uit Hallo Core plugins lijst toevoegen (Klik op **Plugins** > **Core** toofind deze).</span><span class="sxs-lookup"><span data-stu-id="b33c4-147">Add hello Device plugin from hello Core plugins list (click **Plugins** > **Core** toofind it).</span></span> <span data-ttu-id="b33c4-148">U moet de naam van deze invoegtoepassing tooobtain Hallo platform.</span><span class="sxs-lookup"><span data-stu-id="b33c4-148">You need this plugin tooobtain hello platform name.</span></span>

#### <a name="register-your-device-on-application-start-up"></a><span data-ttu-id="b33c4-149">Registreer uw apparaat op opstarten van de toepassing</span><span class="sxs-lookup"><span data-stu-id="b33c4-149">Register your device on application start-up</span></span>
<span data-ttu-id="b33c4-150">We in eerste instantie opnemen minimale code voor Android.</span><span class="sxs-lookup"><span data-stu-id="b33c4-150">Initially, we include some minimal code for Android.</span></span> <span data-ttu-id="b33c4-151">Later wijzigen Hallo app toorun op iOS- of Windows 10.</span><span class="sxs-lookup"><span data-stu-id="b33c4-151">Later, modify hello app toorun on iOS or Windows 10.</span></span>

1. <span data-ttu-id="b33c4-152">Voeg een aanroep te**registerForPushNotifications** tijdens het Hallo-retouraanroep voor Hallo aanmelding of onderin Hallo Hallo **onDeviceReady** methode:</span><span class="sxs-lookup"><span data-stu-id="b33c4-152">Add a call too**registerForPushNotifications** during hello callback for hello login process, or at hello bottom of  hello **onDeviceReady** method:</span></span>

        // Login toohello service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added tooregister for push notifications.
                registerForPushNotifications();

            }, handleError);

    <span data-ttu-id="b33c4-153">In dit voorbeeld ziet aanroepen **registerForPushNotifications** nadat verificatie is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="b33c4-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span></span>  <span data-ttu-id="b33c4-154">U kunt aanroepen `registerForPushNotifications()` zo vaak als nodig is.</span><span class="sxs-lookup"><span data-stu-id="b33c4-154">You can call `registerForPushNotifications()` as often as is required.</span></span>

2. <span data-ttu-id="b33c4-155">Toevoegen van nieuwe Hallo **registerForPushNotifications** methode als volgt:</span><span class="sxs-lookup"><span data-stu-id="b33c4-155">Add hello new **registerForPushNotifications** method as follows:</span></span>

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle hello registration event.
        pushRegistration.on('registration', function (data) {
          // Get hello native platform of hello device.
          var platform = device.platform;
          // Get hello handle returned during registration.
          var handle = data.registrationId;
          // Set hello device-specific message template.
          if (platform == 'android' || platform == 'Android') {
              // Register for GCM notifications.
              client.push.register('gcm', handle, {
                  mytemplate: { body: { data: { message: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'iOS') {
              // Register for notifications.
              client.push.register('apns', handle, {
                  mytemplate: { body: { aps: { alert: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'windows') {
              // Register for WNS notifications.
              client.push.register('wns', handle, {
                  myTemplate: {
                      body: '<toast><visual><binding template="ToastText01"><text id="1">$(messageParam)</text></binding></visual></toast>',
                      headers: { 'X-WNS-Type': 'wns/toast' } }
              });
          }
        });

        pushRegistration.on('notification', function (data, d2) {
          alert('Push Received: ' + data.message);
        });

        pushRegistration.on('error', handleError);
        }
3. <span data-ttu-id="b33c4-156">(Android) Vervang in Hallo voorafgaand aan code, `Your_Project_ID` project met Hallo numerieke ID voor uw app uit de [Google Developer-Console][18].</span><span class="sxs-lookup"><span data-stu-id="b33c4-156">(Android) In hello preceding code, replace `Your_Project_ID` with hello numeric project ID for your app from the  [Google Developer Console][18].</span></span>

## <a name="optional-configure-and-run-hello-app-on-android"></a><span data-ttu-id="b33c4-157">(Optioneel) Configureren en uitvoeren van Hallo-app voor Android</span><span class="sxs-lookup"><span data-stu-id="b33c4-157">(Optional) Configure and run hello app on Android</span></span>
<span data-ttu-id="b33c4-158">Deze sectie tooenable pushmeldingen voor Android worden voltooid.</span><span class="sxs-lookup"><span data-stu-id="b33c4-158">Complete this section tooenable push notifications for Android.</span></span>

#### <span data-ttu-id="b33c4-159"><a name="enable-gcm"></a>Inschakelen van Firebase Cloud-berichten</span><span class="sxs-lookup"><span data-stu-id="b33c4-159"><a name="enable-gcm"></a>Enable Firebase Cloud Messaging</span></span>
<span data-ttu-id="b33c4-160">Aangezien we Hallo Google Android-platform in eerste instantie ontwikkelt, moet u de Firebase Cloud Messaging inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b33c4-160">Since we are targeting hello Google Android platform initially, you must enable Firebase Cloud Messaging.</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <span data-ttu-id="b33c4-161"><a name="configure-backend"></a>Hallo mobiele App back-end toosend push-aanvragen via FCM configureren</span><span class="sxs-lookup"><span data-stu-id="b33c4-161"><a name="configure-backend"></a>Configure hello Mobile App backend toosend push requests using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a><span data-ttu-id="b33c4-162">Configureer uw Cordova-app voor Android</span><span class="sxs-lookup"><span data-stu-id="b33c4-162">Configure your Cordova app for Android</span></span>
<span data-ttu-id="b33c4-163">Open config.xml in uw Cordova-app en vervang `Your_Project_ID` project met Hallo numerieke ID voor uw app uit Hallo [Google Developer-Console][18].</span><span class="sxs-lookup"><span data-stu-id="b33c4-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with hello numeric project ID for your app from hello [Google Developer Console][18].</span></span>

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

<span data-ttu-id="b33c4-164">Index.js openen en bijwerken Hallo code toouse uw numerieke project-ID.</span><span class="sxs-lookup"><span data-stu-id="b33c4-164">Open index.js and update hello code toouse your numeric project ID.</span></span>

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <span data-ttu-id="b33c4-165"><a name="configure-device"></a>Uw Android-apparaat voor USB-foutopsporing configureren</span><span class="sxs-lookup"><span data-stu-id="b33c4-165"><a name="configure-device"></a>Configure your Android device for USB debugging</span></span>
<span data-ttu-id="b33c4-166">Voordat u uw toepassing tooyour Android-apparaat implementeren kunt, moet u tooenable USB-foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="b33c4-166">Before you can deploy your application tooyour Android Device, you need tooenable USB Debugging.</span></span>  <span data-ttu-id="b33c4-167">Voer de volgende stappen uit op uw Android-telefoon:</span><span class="sxs-lookup"><span data-stu-id="b33c4-167">Perform the following steps on your Android phone:</span></span>

1. <span data-ttu-id="b33c4-168">Ga te**instellingen** > **over telefoon**, tikt u op Hallo **Build-nummer** totdat modus voor ontwikkelaars (ongeveer zeven maal) is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b33c4-168">Go too**Settings** > **About phone**, then tap hello **Build number** until developer mode is enabled  (about seven times).</span></span>
2. <span data-ttu-id="b33c4-169">Terug in de **instellingen** > **opties voor ontwikkelaars** inschakelen **USB-foutopsporing**, sluit uw Android-telefoon tooyour ontwikkeling PC met een USB-kabel.</span><span class="sxs-lookup"><span data-stu-id="b33c4-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  tooyour development PC with a USB Cable.</span></span>

<span data-ttu-id="b33c4-170">We hebben getest dit met behulp van een Google-Nexus 5 X-apparaat met Android 6.0 (Marshmallow).</span><span class="sxs-lookup"><span data-stu-id="b33c4-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span></span>  <span data-ttu-id="b33c4-171">Hallo technieken zijn echter algemene binnen een moderne Android release.</span><span class="sxs-lookup"><span data-stu-id="b33c4-171">However, hello techniques are common across any modern Android release.</span></span>

#### <a name="install-google-play-services"></a><span data-ttu-id="b33c4-172">Installeer Google Play-Services</span><span class="sxs-lookup"><span data-stu-id="b33c4-172">Install Google Play Services</span></span>
<span data-ttu-id="b33c4-173">Hallo push-invoegtoepassing is afhankelijk van Android Google Play Services voor pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="b33c4-173">hello push plugin relies on Android Google Play Services for push notifications.</span></span>

1. <span data-ttu-id="b33c4-174">Klik in Visual Studio **extra** > **Android** > **Android SDK Manager**, vouw Hallo **extra's** map- en controle Hallo vak toomake ervoor dat elk van de volgende SDK's Hallo is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b33c4-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand hello **Extras** folder and  check hello box toomake sure that each of hello following SDKs is installed.</span></span>

   * <span data-ttu-id="b33c4-175">Android 2.3 of hoger</span><span class="sxs-lookup"><span data-stu-id="b33c4-175">Android 2.3 or higher</span></span>
   * <span data-ttu-id="b33c4-176">Google-opslagplaats revisie 27 of hoger</span><span class="sxs-lookup"><span data-stu-id="b33c4-176">Google Repository revision 27 or higher</span></span>
   * <span data-ttu-id="b33c4-177">Google Play Services 9.0.2 of hoger</span><span class="sxs-lookup"><span data-stu-id="b33c4-177">Google Play Services 9.0.2 or higher</span></span>

2. <span data-ttu-id="b33c4-178">Klik op **pakketten installeren** en wachten op Hallo installatie toocomplete.</span><span class="sxs-lookup"><span data-stu-id="b33c4-178">Click **Install Packages** and wait for hello installation toocomplete.</span></span>

<span data-ttu-id="b33c4-179">Hallo huidige vereist bibliotheken worden vermeld in Hallo [phonegap-invoegtoepassing-push-installatie documentatie][19].</span><span class="sxs-lookup"><span data-stu-id="b33c4-179">hello current required libraries are listed in hello [phonegap-plugin-push installation documentation][19].</span></span>

#### <a name="test-push-notifications-in-hello-app-on-android"></a><span data-ttu-id="b33c4-180">Pushmeldingen testen in Hallo-app voor Android</span><span class="sxs-lookup"><span data-stu-id="b33c4-180">Test push notifications in hello app on Android</span></span>
<span data-ttu-id="b33c4-181">U kunt nu pushmeldingen testen door het uitvoeren van app en invoegen items in de takentabel Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b33c4-181">You can now test push notifications by running hello app and inserting items in hello TodoItem table.</span></span> <span data-ttu-id="b33c4-182">U kunt testen van Hallo hetzelfde apparaat of van een tweede apparaat dezelfde hello, zolang u back-end.</span><span class="sxs-lookup"><span data-stu-id="b33c4-182">You can test from hello same device or from a second device, as long as you are using hello same backend.</span></span> <span data-ttu-id="b33c4-183">Test uw Cordova-app op Hallo Android-platform in een van de volgende manieren Hallo:</span><span class="sxs-lookup"><span data-stu-id="b33c4-183">Test your Cordova app on hello Android platform in one of hello following ways:</span></span>

* <span data-ttu-id="b33c4-184">**Op een fysiek apparaat:** koppelen van uw Android-apparaat tooyour ontwikkelcomputer met een USB-kabel.</span><span class="sxs-lookup"><span data-stu-id="b33c4-184">**On a physical device:** Attach your Android device tooyour development computer with a USB cable.</span></span>  <span data-ttu-id="b33c4-185">In plaats van **Google Android-Emulator**, selecteer **apparaat**.</span><span class="sxs-lookup"><span data-stu-id="b33c4-185">Instead of **Google Android Emulator**, select **Device**.</span></span> <span data-ttu-id="b33c4-186">Visual Studio Hallo toepassing toohello apparaat implementeert en vervolgens wordt de toepassing hello uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b33c4-186">Visual Studio deploys hello application toohello device and then runs hello application.</span></span>  <span data-ttu-id="b33c4-187">U kunt vervolgens met de toepassing hello op Hallo apparaat werken.</span><span class="sxs-lookup"><span data-stu-id="b33c4-187">You can then interact with hello application on hello device.</span></span>

  <span data-ttu-id="b33c4-188">De ontwikkeling-ervaring te verbeteren.</span><span class="sxs-lookup"><span data-stu-id="b33c4-188">Improve your development experience.</span></span>  <span data-ttu-id="b33c4-189">Scherm, zoals toepassingen delen [Mobizen] [ 20] kan u helpen bij het ontwikkelen van een Android-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b33c4-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span></span>  <span data-ttu-id="b33c4-190">Uw webbrowser voor Android scherm tooa projecteert Mobizen op uw PC.</span><span class="sxs-lookup"><span data-stu-id="b33c4-190">Mobizen projects your Android screen tooa web browser on your PC.</span></span>

* <span data-ttu-id="b33c4-191">**Op een Android-emulator:** er zijn extra configuratiestappen vereist wanneer u gebruikmaakt van een emulator.</span><span class="sxs-lookup"><span data-stu-id="b33c4-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span></span>

    <span data-ttu-id="b33c4-192">Zorg ervoor dat u tooa virtueel apparaat met Google APIs ingesteld als doel hello, zoals wordt weergegeven in Hallo Android Virtual Device (AVD) manager implementeert.</span><span class="sxs-lookup"><span data-stu-id="b33c4-192">Make sure you are deploying tooa virtual device that has Google APIs set as hello target, as shown in hello Android Virtual Device (AVD) manager.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    <span data-ttu-id="b33c4-193">Als u een snellere x86 toouse wilt emulator u [hello HAXM stuurprogramma installeren] [ 11] en configureer Hallo emulator toouse deze.</span><span class="sxs-lookup"><span data-stu-id="b33c4-193">If you want toouse a faster x86 emulator, you [install hello HAXM driver][11] and configure hello emulator toouse it.</span></span>

    <span data-ttu-id="b33c4-194">Een apparaat toohello Android van Google-account toevoegen door te klikken op **Apps** > **instellingen** > **account toevoegen**, volg de aanwijzingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="b33c4-194">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    <span data-ttu-id="b33c4-195">Hallo todolist-app als voordat uitvoeren en een nieuwe taak invoegen.</span><span class="sxs-lookup"><span data-stu-id="b33c4-195">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="b33c4-196">Dit moment wordt een pictogram weergegeven in het systeemvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="b33c4-196">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="b33c4-197">U kunt Hallo melding lade tooview Hallo volledige tekst van melding Hallo openen.</span><span class="sxs-lookup"><span data-stu-id="b33c4-197">You can open hello notification drawer tooview hello full text of hello notification.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a><span data-ttu-id="b33c4-198">(Optioneel) Configureren en uitvoeren op iOS</span><span class="sxs-lookup"><span data-stu-id="b33c4-198">(Optional) Configure and run on iOS</span></span>
<span data-ttu-id="b33c4-199">Deze sectie is voor het uitvoeren van Hallo Cordova-project op iOS-apparaten.</span><span class="sxs-lookup"><span data-stu-id="b33c4-199">This section is for running hello Cordova project on iOS devices.</span></span> <span data-ttu-id="b33c4-200">Als u niet met iOS-apparaten werkt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="b33c4-200">If you are not working with iOS devices, you can skip this section.</span></span>

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a><span data-ttu-id="b33c4-201">Agent installeren en uitvoeren Hallo iOS externe te ontwikkelen op een Mac- of cloud service</span><span class="sxs-lookup"><span data-stu-id="b33c4-201">Install and run hello iOS remote build agent on a Mac or cloud service</span></span>
<span data-ttu-id="b33c4-202">Voordat u een Cordova-app voor iOS met Visual Studio uitvoeren kunt, stappen doorlopen die Hallo in Hallo [iOS Setup Guide] [ 12] tooinstall en Voer Hallo externe agent te ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="b33c4-202">Before you can run a Cordova app on iOS using Visual Studio, go through hello steps in hello [iOS Setup Guide][12] tooinstall and run hello remote build agent.</span></span>

<span data-ttu-id="b33c4-203">Zorg ervoor dat u Hallo-app voor iOS kunt samenstellen.</span><span class="sxs-lookup"><span data-stu-id="b33c4-203">Make sure you can build hello app for iOS.</span></span> <span data-ttu-id="b33c4-204">Hallo zijn stappen in de handleiding voor het instellen van Hallo vereiste toobuild voor iOS vanuit Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b33c4-204">hello steps in hello setup guide are required toobuild for iOS from Visual Studio.</span></span> <span data-ttu-id="b33c4-205">Als u een Mac niet hebt, kunt u voor iOS met de Hallo externe build-agent op een service, zoals MacInCloud samenstellen.</span><span class="sxs-lookup"><span data-stu-id="b33c4-205">If you do not have a Mac, you can build for iOS using hello remote build agent on a service like MacInCloud.</span></span> <span data-ttu-id="b33c4-206">Zie voor meer informatie [uw iOS-app uitvoeren in de cloud Hallo][21].</span><span class="sxs-lookup"><span data-stu-id="b33c4-206">For more info, see [Run your iOS app in hello cloud][21].</span></span>

> [!NOTE]
> <span data-ttu-id="b33c4-207">XCode 7 of hoger is vereist toouse Hallo push-invoegtoepassing op iOS.</span><span class="sxs-lookup"><span data-stu-id="b33c4-207">XCode 7 or greater is required toouse hello push plugin on iOS.</span></span>

#### <a name="find-hello-id-toouse-as-your-app-id"></a><span data-ttu-id="b33c4-208">Hallo-ID toouse vinden als uw App-ID</span><span class="sxs-lookup"><span data-stu-id="b33c4-208">Find hello ID toouse as your App ID</span></span>
<span data-ttu-id="b33c4-209">Voordat u uw app voor pushmeldingen registreert, opent u config.xml in uw Cordova-app, Hallo zoeken `id` kenmerkwaarde in Hallo widget-element en kopiëren voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="b33c4-209">Before you register your app for push notifications, open config.xml in your Cordova app, find hello `id` attribute value in hello widget element, and copy it for later use.</span></span> <span data-ttu-id="b33c4-210">In de Hallo XML te volgen, Hallo-ID is `io.cordova.myapp7777777`.</span><span class="sxs-lookup"><span data-stu-id="b33c4-210">In hello following XML, hello ID is `io.cordova.myapp7777777`.</span></span>

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

<span data-ttu-id="b33c4-211">Deze id later gebruiken bij het maken van een App-ID op van Apple developer portal.</span><span class="sxs-lookup"><span data-stu-id="b33c4-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span></span> <span data-ttu-id="b33c4-212">Als u een andere App-ID op Hallo developer-portal maakt, moet u rekening houden met een paar extra stappen verderop in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="b33c4-212">If you create a different App ID on hello developer portal, you must take a few extra steps later in this tutorial.</span></span> <span data-ttu-id="b33c4-213">Hallo-ID in het element widget moet overeenkomen met de Hallo App-ID op Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="b33c4-213">hello ID in the widget element must match hello App ID on hello developer portal.</span></span>

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="b33c4-214">Hallo-app voor pushmeldingen op Apple developer-portal te registreren</span><span class="sxs-lookup"><span data-stu-id="b33c4-214">Register hello app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[<span data-ttu-id="b33c4-215">Bekijk een video van vergelijkbare stappen</span><span class="sxs-lookup"><span data-stu-id="b33c4-215">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="b33c4-216">Azure toosend-pushmeldingen configureren</span><span class="sxs-lookup"><span data-stu-id="b33c4-216">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a><span data-ttu-id="b33c4-217">Controleren of uw App-ID overeenkomt met uw Cordova-app</span><span class="sxs-lookup"><span data-stu-id="b33c4-217">Verify that your App ID matches your Cordova app</span></span>
<span data-ttu-id="b33c4-218">Als Hallo App-ID die u hebt gemaakt in uw ontwikkelaarsaccount Apple al overeenkomt met Hallo-ID van Hallo widget element in config.xml, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="b33c4-218">If hello App ID you created in your Apple Developer Account already matches hello ID of hello widget element in config.xml, you can skip this step.</span></span> <span data-ttu-id="b33c4-219">Als Hallo-id's niet overeenkomen, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b33c4-219">However, if hello IDs don't match, take hello following steps:</span></span>

1. <span data-ttu-id="b33c4-220">Hallo platforms map verwijderen van uw project.</span><span class="sxs-lookup"><span data-stu-id="b33c4-220">Delete hello platforms folder from your project.</span></span>
2. <span data-ttu-id="b33c4-221">Hallo plugins map verwijderen van uw project.</span><span class="sxs-lookup"><span data-stu-id="b33c4-221">Delete hello plugins folder from your project.</span></span>
3. <span data-ttu-id="b33c4-222">Hallo node_modules map verwijderen van uw project.</span><span class="sxs-lookup"><span data-stu-id="b33c4-222">Delete hello node_modules folder from your project.</span></span>
4. <span data-ttu-id="b33c4-223">Hallo-id-kenmerk van Hallo widget element in config.xml toouse Hallo App-ID die u hebt gemaakt in uw Apple Developer-Account bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b33c4-223">Update hello id attribute of hello widget element in config.xml toouse hello App ID that you created in your  Apple Developer Account.</span></span>
5. <span data-ttu-id="b33c4-224">Bouw het project opnieuw op.</span><span class="sxs-lookup"><span data-stu-id="b33c4-224">Rebuild your project.</span></span>

##### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="b33c4-225">Pushmeldingen testen in uw iOS-app</span><span class="sxs-lookup"><span data-stu-id="b33c4-225">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="b33c4-226">Controleer of in Visual Studio **iOS** is geselecteerd als het implementatiedoel Hallo en kies vervolgens **apparaat** toorun op het verbonden iOS-apparaat.</span><span class="sxs-lookup"><span data-stu-id="b33c4-226">In Visual Studio, make sure that **iOS** is selected as hello deployment target, and then choose **Device** toorun on your connected iOS device.</span></span>

    <span data-ttu-id="b33c4-227">U kunt uitvoeren op een iOS-apparaat aansluit tooyour PC met iTunes.</span><span class="sxs-lookup"><span data-stu-id="b33c4-227">You can run on an iOS device connected tooyour PC using iTunes.</span></span> <span data-ttu-id="b33c4-228">Hallo iOS-Simulator biedt geen ondersteuning voor pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="b33c4-228">hello iOS Simulator does not support push notifications.</span></span>

2. <span data-ttu-id="b33c4-229">Druk op Hallo **uitvoeren** knop of **F5** in Visual Studio toobuild Hallo-project en start Hallo-app in een iOS-apparaat en klik vervolgens op **OK** tooaccept pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="b33c4-229">Press hello **Run** button or **F5** in Visual Studio toobuild hello project and start hello app in an iOS  device, then click **OK** tooaccept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b33c4-230">Hallo app vraagt om bevestiging voor pushmeldingen tijdens Hallo voor het eerst uitvoert.</span><span class="sxs-lookup"><span data-stu-id="b33c4-230">hello app requests confirmation for push notifications during hello first run.</span></span>

3. <span data-ttu-id="b33c4-231">Typ een taak in Hallo-app, en klik op Hallo plusteken (+) pictogram.</span><span class="sxs-lookup"><span data-stu-id="b33c4-231">In hello app, type a task, and then click hello plus (+) icon.</span></span>
4. <span data-ttu-id="b33c4-232">Controleer of dat een melding wordt ontvangen en klik vervolgens op OK toodismiss Hallo melding.</span><span class="sxs-lookup"><span data-stu-id="b33c4-232">Verify that a notification is received, then click OK toodismiss hello notification.</span></span>

## <a name="optional-configure-and-run-on-windows"></a><span data-ttu-id="b33c4-233">(Optioneel) Configureren en uitvoeren in Windows</span><span class="sxs-lookup"><span data-stu-id="b33c4-233">(Optional) Configure and run on Windows</span></span>
<span data-ttu-id="b33c4-234">Deze sectie is voor het uitvoeren van Hallo Apache Cordova-app-project op Windows 10-apparaten (Hallo PhoneGap push-invoegtoepassing wordt ondersteund op Windows 10).</span><span class="sxs-lookup"><span data-stu-id="b33c4-234">This section is for running hello Apache Cordova app project on Windows 10 devices (hello PhoneGap push plugin is supported on Windows 10).</span></span> <span data-ttu-id="b33c4-235">Als u niet met Windows-apparaten werkt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="b33c4-235">If you are not working with Windows devices, you can skip this section.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a><span data-ttu-id="b33c4-236">Uw Windows-app voor pushmeldingen registreren met WNS</span><span class="sxs-lookup"><span data-stu-id="b33c4-236">Register your Windows app for push notifications with WNS</span></span>
<span data-ttu-id="b33c4-237">toouse hello Store opties in Visual Studio, selecteer een doel Windows hello oplossing Platforms lijst zoals **Windows x64** of **Windows x86** (voorkomen **Windows AnyCPU** voor pushmeldingen).</span><span class="sxs-lookup"><span data-stu-id="b33c4-237">toouse hello Store options in Visual Studio, select a Windows target from hello Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span></span>

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

<span data-ttu-id="b33c4-238">[Bekijk een video van gelijksoortige stappen][13]</span><span class="sxs-lookup"><span data-stu-id="b33c4-238">[Watch a video showing similar steps][13]</span></span>

#### <a name="configure-hello-notification-hub-for-wns"></a><span data-ttu-id="b33c4-239">Hallo notification hub configureren voor WNS</span><span class="sxs-lookup"><span data-stu-id="b33c4-239">Configure hello notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a><span data-ttu-id="b33c4-240">Uw pushmeldingen voor Cordova-app toosupport Windows configureren</span><span class="sxs-lookup"><span data-stu-id="b33c4-240">Configure your Cordova app toosupport Windows push notifications</span></span>
<span data-ttu-id="b33c4-241">Open Hallo configuration designer (met de rechtermuisknop op config.xml en selecteer **ontwerper**), selecteer Hallo **Windows** tabblad en kies **Windows 10** onder **Windows doel versie**.</span><span class="sxs-lookup"><span data-stu-id="b33c4-241">Open hello configuration designer (right-click on config.xml and select **View Designer**), select hello **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span></span>

<span data-ttu-id="b33c4-242">toosupport pushmeldingen in uw standaard (debug) bouwt, open build.json-bestand.</span><span class="sxs-lookup"><span data-stu-id="b33c4-242">toosupport push notifications in your default (debug) builds, open build.json file.</span></span> <span data-ttu-id="b33c4-243">Kopieer de "release" configuratie tooyour foutopsporing configuratie.</span><span class="sxs-lookup"><span data-stu-id="b33c4-243">Copy the "release" configuration tooyour debug configuration.</span></span>

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="b33c4-244">Nadat de update hello, moeten Hallo build.json Hallo na code bevatten:</span><span class="sxs-lookup"><span data-stu-id="b33c4-244">After hello update, hello build.json should contain hello following code:</span></span>

    "windows": {
        "release": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            },
        "debug": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="b33c4-245">Hallo-app bouwen en te controleren of er geen fouten.</span><span class="sxs-lookup"><span data-stu-id="b33c4-245">Build hello app and verify that you have no errors.</span></span> <span data-ttu-id="b33c4-246">Uw client-app moet zich nu registreren voor Hallo meldingen van de back-end van Hallo mobiele App.</span><span class="sxs-lookup"><span data-stu-id="b33c4-246">Your client app should now register for hello notifications from hello Mobile App backend.</span></span> <span data-ttu-id="b33c4-247">Herhaal deze sectie voor elke Windows-project in uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="b33c4-247">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="b33c4-248">Pushmeldingen testen in uw Windows-app</span><span class="sxs-lookup"><span data-stu-id="b33c4-248">Test push notifications in your Windows app</span></span>
<span data-ttu-id="b33c4-249">Zorg ervoor dat een Windows-platform, zoals Hallo implementatie TARGET is geselecteerd in Visual Studio **Windows x64** of **Windows x86**.</span><span class="sxs-lookup"><span data-stu-id="b33c4-249">In Visual Studio, make sure that a Windows platform is selected as hello deployment target, such as **Windows-x64** or **Windows-x86**.</span></span> <span data-ttu-id="b33c4-250">Kies toorun Hallo-app op een Windows 10-computer die als host fungeert voor Visual Studio **lokale Machine**.</span><span class="sxs-lookup"><span data-stu-id="b33c4-250">toorun hello app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span></span>

<span data-ttu-id="b33c4-251">Druk op Hallo knop toobuild Hallo project uitvoeren en Hallo-app te starten.</span><span class="sxs-lookup"><span data-stu-id="b33c4-251">Press hello Run button toobuild hello project and start hello app.</span></span>

<span data-ttu-id="b33c4-252">Typ een naam voor een nieuwe stukje in Hallo-app en klik op Hallo plusteken (+) pictogram tooadd deze.</span><span class="sxs-lookup"><span data-stu-id="b33c4-252">In hello app, type a name for a new todoitem, and then click hello plus (+) icon tooadd it.</span></span>

<span data-ttu-id="b33c4-253">Controleer of dat er een melding wordt ontvangen wanneer Hallo item wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="b33c4-253">Verify that a notification is received when hello item is added.</span></span>

## <span data-ttu-id="b33c4-254"><a name="next-steps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b33c4-254"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="b33c4-255">Meer informatie over [Notification Hubs] [ 17] toolearn over pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="b33c4-255">Read about [Notification Hubs][17] toolearn about push notifications.</span></span>
* <span data-ttu-id="b33c4-256">Als u dit nog niet hebt gedaan, gaat u verder Hallo zelfstudie door [Authentication toevoegen] [ 14] tooyour Apache Cordova-app.</span><span class="sxs-lookup"><span data-stu-id="b33c4-256">If you have not already done so, continue hello tutorial by [Adding Authentication][14] tooyour Apache Cordova app.</span></span>

<span data-ttu-id="b33c4-257">Meer informatie over hoe toouse Hallo SDK's.</span><span class="sxs-lookup"><span data-stu-id="b33c4-257">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="b33c4-258">[Apache Cordova-SDK][15]</span><span class="sxs-lookup"><span data-stu-id="b33c4-258">[Apache Cordova SDK][15]</span></span>
* <span data-ttu-id="b33c4-259">[ASP.NET-Server SDK][1]</span><span class="sxs-lookup"><span data-stu-id="b33c4-259">[ASP.NET Server SDK][1]</span></span>
* <span data-ttu-id="b33c4-260">[Server-SDK voor node.js][16]</span><span class="sxs-lookup"><span data-stu-id="b33c4-260">[Node.js Server SDK][16]</span></span>

<!-- Images -->
[img1]: ./media/app-service-mobile-cordova-get-started-push/add-push-plugin.png

<!-- URLs -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: http://www.visualstudio.com/
[3]: https://azure.microsoft.com/pricing/free-trial/
[4]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[5]: app-service-mobile-cordova-get-started.md
[6]: http://go.microsoft.com/fwlink/p/?LinkId=268302
[7]: https://developer.apple.com/programs/
[8]: https://developer.microsoft.com/en-us/store/register
[9]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-3-Create-azure-notification-hub
[10]: https://www.npmjs.com/
[11]: https://taco.visualstudio.com/en-us/docs/run-app-apache/#HAXM
[12]: http://taco.visualstudio.com/en-us/docs/ios-guide/
[13]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-6-Set-up-wns-for-push
[14]: app-service-mobile-cordova-get-started-users.md
[15]: app-service-mobile-cordova-how-to-use-client-library.md
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[17]: ../notification-hubs/notification-hubs-push-notification-overview.md
[18]: https://console.developers.google.com/home/dashboard
[19]: https://github.com/phonegap/phonegap-plugin-push/blob/master/docs/INSTALLATION.md
[20]: https://www.mobizen.com/
[21]: http://taco.visualstudio.com/en-us/docs/build_ios_cloud/
