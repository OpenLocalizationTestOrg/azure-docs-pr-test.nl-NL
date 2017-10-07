---
title: aaaGet de slag met Azure App Service Mobile Apps voor Xamarin.iOS-apps | Microsoft Docs
description: Volg deze zelfstudie tooget slag kunt met Mobile Apps voor Xamarin.iOS-ontwikkeling.
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: syntaxc4
ms.openlocfilehash: 524c5ac4d8a29d7cb858f74132aad5d6e2201d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinios-app"></a>Een Xamarin.iOS-app maken
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Overzicht
Deze zelfstudie leert u hoe tooadd back-end van een cloud-gebaseerde mobiele tooa Xamarin.iOS-app service met behulp van een back-end voor mobiele Apps van Azure.  U maakt zowel een nieuwe back-end voor mobiele apps als een eenvoudige Xamarin.iOS-app voor *takenlijsten* die app-gegevens opslaat in Azure.

Voltooien van deze zelfstudie is een vereiste voor alle andere Xamarin.iOS-zelfstudies over het gebruik van de functie Mobile Apps Hallo in Azure App Service.

## <a name="prerequisites"></a>Vereisten
toocomplete in deze zelfstudie, moet u Hallo volgende vereisten:

* Een actief Azure-account. Als u geen account hebt, zich aanmelden voor een proefversie van Azure en krijg too10 gratis mobiele apps die u ook na de proefperiode kunt blijven gebruiken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.
* Visual Studio met Xamarin. Zie [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Installeren en instellen voor Visual Studio en Xamarin) voor instructies.
* Een Mac met Xcode v7.0 of hoger en waarop Xamarin Studio Community is geïnstalleerd. Zie [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Installeren en instellen voor Visual Studio en Xamarin) en [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (Instructies voor installatie, configuratie en verificatie voor Mac-gebruikers) (MSDN).

## <a name="create-an-azure-mobile-app-backend"></a>Een back-end voor mobiele apps van Azure maken
Volg deze stappen toocreate een back-end voor de mobiele App.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a>Hallo serverproject configureren
U hebt nu een back-end voor mobiele apps van Azure ingericht, die kan worden gebruikt door uw mobiele-clienttoepassingen. Vervolgens een serverproject downloaden voor een eenvoudige 'todo list' back-end en deze tooAzure publiceren.

Volg stappen tooconfigure Hallo server project toouse na Hallo beide Hallo Node.js- of .NET-back-end.

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a>Hallo Xamarin.iOS-app downloaden en uitvoeren
1. Open Hallo [Azure-portal] in een browservenster.
2. Klik op de blade met Hallo-instellingen voor uw mobiele App, **aan de slag** > **Xamarin.iOS**. Klik in stap 3 op **Een nieuwe app maken** als deze optie nog niet is geselecteerd.  Klik vervolgens op Hallo **downloaden** knop.

      Een clienttoepassing die verbinding tooyour mobiele back-end maakt wordt gedownload. Hallo gecomprimeerde projectbestand op uw lokale computer opslaan en maak een notitie van de opslaglocatie.
3. Pak Hallo-project dat u hebt gedownload en open het in Xamarin Studio (of Visual Studio).

    ![][9]

    ![][8]
4. Druk op Hallo F5 sleutel toobuild Hallo project en Hallo-app te starten in Hallo iPhone-emulator.
5. Typ in het Hallo-app zinvolle tekst, zoals *xamarin leren kennen*, en klik vervolgens op Hallo  **+**  knop.

    ![][10]

    De gegevens van Hallo-aanvraag is opgenomen in de takentabel Hallo. Items die zijn opgeslagen in de tabel Hallo zijn geretourneerd door de back-end van Hallo mobiele app en de gegevens worden weergegeven in de lijst Hallo.

> [!NOTE]
> U kunt Hallo-code die toegang heeft tot uw back-end voor mobiele app tooquery bekijken en gegevens invoegen in Hallo QSTodoService.cs C#-bestand.
>
>

## <a name="next-steps"></a>Volgende stappen
* [Offline synchronisatie tooyour app toevoegen](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [Verificatie tooyour app toevoegen](app-service-mobile-xamarin-ios-get-started-users.md)
* [Push notifications tooyour Xamarin.Android-app toevoegen](app-service-mobile-xamarin-ios-get-started-push.md)
* [Hoe toouse Hallo-client voor mobiele Apps van Azure beheerd](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
[Azure-portal]: https://portal.azure.com/
