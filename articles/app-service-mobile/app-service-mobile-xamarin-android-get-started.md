---
title: aaaGet gestart met Azure Mobile Apps voor Xamarin.Android-apps
description: Volg deze zelfstudie tooget de slag met Azure Mobile Apps voor Xamarin.android-ontwikkeling
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 81649dd3-544f-40ff-b9b7-60c66d683e60
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 38710660d9328fe3c068efca972f76aa8b6e049b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinandroid-app"></a>Een Xamarin.Android-app maken
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Overzicht
Deze zelfstudie laat zien hoe een cloud-gebaseerde back-end tooadd tooa Xamarin.Android-app service. Zie [What are Mobile Apps](app-service-mobile-value-prop.md) (Wat zijn Mobile Apps?) voor meer informatie.

Een schermafbeelding van de app Hallo voltooid lager is dan:

![][0]

Het voltooien van deze zelfstudie is een vereiste voor alle andere Mobile Apps-zelfstudies voor Xamarin.Android-apps.

## <a name="prerequisites"></a>Vereisten
toocomplete in deze zelfstudie, moet u Hallo volgende vereisten:

* Een actief Azure-account. Als u geen account hebt, zich aanmeldt voor een proefversie van Azure en krijg too10 gratis mobiele Apps. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.
* Visual Studio met Xamarin. Zie [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Installeren en instellen voor Visual Studio en Xamarin) voor instructies.

## <a name="create-an-azure-mobile-app-backend"></a>Een back-end voor mobiele apps van Azure maken
Volg deze stappen toocreate een back-end voor de mobiele App.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

U hebt nu een back-end voor mobiele apps van Azure ingericht, die kan worden gebruikt door uw mobiele-clienttoepassingen. Vervolgens een serverproject downloaden voor een eenvoudige 'todo list' back-end en deze tooAzure publiceren.

## <a name="configure-hello-server-project"></a>Hallo serverproject configureren
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinandroid-app"></a>Hallo Xamarin.Android-app downloaden en uitvoeren
1. Onder **uw Xamarin.Android-project downloaden en uitvoeren**, klikt u op Hallo **downloaden** knop.

      Hallo project gecomprimeerde bestand tooyour lokale computer opslaan en maak een notitie van de opslaglocatie.
2. Druk op Hallo **F5** toobuild Hallo project sleutel en het Hallo-app te starten.
3. Typ in het Hallo-app zinvolle tekst, zoals *voltooid Hallo zelfstudie* en klik vervolgens op Hallo **toevoegen** knop.

    ![][10]

    De gegevens van Hallo-aanvraag is opgenomen in de takentabel Hallo. Items die zijn opgeslagen in de tabel Hallo zijn geretourneerd door de back-end van Hallo mobiele app en de gegevens worden weergegeven in de lijst Hallo.

   > [!NOTE]
   > U kunt Hallo-code die toegang heeft tot uw back-end voor mobiele app tooquery bekijken en gegevens vindt u in C#-bestand ToDoActivity.cs Hallo invoegen.
   >
   >

## <a name="next-steps"></a>Volgende stappen
* [Offline synchronisatie tooyour app toevoegen](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [Verificatie tooyour app toevoegen](app-service-mobile-xamarin-android-get-started-users.md)
* [Push notifications tooyour Xamarin.Android-app toevoegen](app-service-mobile-xamarin-android-get-started-push.md)
* [Hoe toouse Hallo-client voor mobiele Apps van Azure beheerd](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
