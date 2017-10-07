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
# <a name="add-push-notifications-tooyour-android-app"></a>Push tooyour Android-app-meldingen toevoegen
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Overzicht
In deze zelfstudie maakt u een push notifications toohello toevoegen [Android snel starten] project, zodat een push-melding toohello apparaat verzonden telkens wanneer een record wordt ingevoegd.

Als u geen gebruik Hallo gedownload serverproject snel starten, moet u push notification-uitbreidingspakket Hallo. Zie voor meer informatie [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="prerequisites"></a>Vereisten
U hebt Hallo volgende nodig:

* Een IDE, afhankelijk van de back-end van uw project:

  * [Android Studio](https://developer.android.com/sdk/index.html) als deze app een back-end voor Node.js heeft.
  * [Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) of hoger als deze app een Microsoft .NET-back-end heeft.
* Android 2.3 of hoger, Google opslagplaats revisie 27 of hoger en Google Play-Services 9.0.2 of hoger voor Firebase Cloud Messaging.
* Volledige Hallo [Android snel starten].

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a>Een project maken dat Firebase Cloud Messaging ondersteunt
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a>Een notification hub configureren
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-toosend-push-notifications"></a>Azure toosend-pushmeldingen configureren
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-hello-server-project"></a>Pushmeldingen voor Hallo serverproject inschakelen
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-tooyour-app"></a>Push notifications tooyour app toevoegen
In deze sectie kunt u uw Android-app voor client toohandle pushmeldingen bijwerken.

### <a name="verify-android-sdk-version"></a>Controleer of de Android SDK-versie
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

De volgende stap is tooinstall Google Play-services. Google Cloud Messaging heeft bepaalde minimale API-niveau vereisten voor het ontwikkelen en testen, welke Hallo **minSdkVersion** eigenschap in het manifest Hallo moet voldoen aan.

Als u met een oudere apparaat testen wilt, raadpleegt u [ingesteld van Google Play Services SDK] toodetermine hoe lage u kunt deze waarde instellen en juist instellen.

### <a name="add-google-play-services-toohello-project"></a>Google Play services toohello project toevoegen
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a>Voeg code toe
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-hello-app-against-hello-published-mobile-service"></a>Test Hallo app tegen Hallo gepubliceerd mobiele service
U kunt Hallo app testen door het koppelen van een Android-telefoon met een USB-kabel rechtstreeks of via een virtueel apparaat in Hallo-emulator.

## <a name="next-steps"></a>Volgende stappen
Nu dat u deze zelfstudie hebt voltooid, kunt u overwegen tooone Hallo volgende zelfstudies verder te gaan:

* [Verificatie tooyour Android-app toevoegen](app-service-mobile-android-get-started-users.md).
  Meer informatie over hoe tooadd verificatie toohello todolist Quick Start-project op Android met behulp van een ondersteunde id-provider.
* [Offlinesynchronisatie voor uw Android-app inschakelen](app-service-mobile-android-get-started-offline-data.md).
  Meer informatie over hoe de offline tooadd tooyour app met behulp van een back-end van Mobile Apps ondersteunen. Met het offline synchroniseren gebruikers kunnen communiceren met een mobiele app&mdash;weergeven, toevoegen of wijzigen van gegevens&mdash;zelfs wanneer er geen netwerkverbinding.

<!-- URLs -->
[Android snel starten]: app-service-mobile-android-get-started.md

[ingesteld van Google Play Services SDK]:https://developers.google.com/android/guides/setup
