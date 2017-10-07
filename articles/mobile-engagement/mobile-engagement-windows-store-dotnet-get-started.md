---
title: aaaGet gestart met Windows universele Apps in Azure Mobile Engagement
description: Meer informatie over hoe toouse Azure Mobile Engagement met analyses en pushmeldingen voor universele Windows-Apps.
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a>Aan de slag met Azure Mobile Engagement voor universele Windows-apps
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand uw app-gebruik en verzenden push notifications toosegmented gebruikers van een universele Windows-toepassing.
Deze zelfstudie laat zien Hallo eenvoudig broadcast-scenario met Mobile Engagement. In deze zelfstudie maakt u een lege universele Windows-app die basisgegevens verzamelt en pushmeldingen ontvangt via Windows Notification Service (WNS).

> [!NOTE]
> Hallo Azure Mobile Engagement service buiten gebruik gesteld maart 2018 en is momenteel alleen beschikbaar tooexisting klanten. Zie [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/) voor meer informatie.

## <a name="prerequisites"></a>Vereisten
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a>Mobile Engagement instellen voor uw universele Windows-app
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end
Deze zelfstudie toont een 'basisintegratie', die wordt Hallo minimale vereiste toocollect gegevens instellen en een pushmelding verzenden. de volledige integratiedocumentatie Hallo vindt u in Hallo [Mobile Engagement universele Windows SDK-integratie](mobile-engagement-windows-store-sdk-overview.md).

U kunt een eenvoudige app maken met Visual Studio toodemonstrate Hallo-integratie.

### <a name="create-a-windows-universal-app-project"></a>Een nieuw project voor een universele Windows-app maken
Hallo volgende stappen wordt ervan uitgegaan Hallo gebruik van Visual Studio 2015 al Hallo stappen vergelijkbaar in eerdere versies van Visual Studio zijn.

1. Start Visual Studio en in Hallo **Start** Schakel in het scherm **nieuw Project**.
2. Selecteer in het pop-upvenster Hallo **Windows** -> **Universal** -> **lege App (universeel Windows)**. Vul Hallo app **naam** en **oplossingsnaam**, en klik vervolgens op **OK**.

    ![][1]

U hebt nu een universele Windows-App-project waarin u naast hello Azure Mobile Engagement SDK integreren gemaakt.

### <a name="connect-your-app-toomobile-engagement-backend"></a>Verbinding maken met uw app tooMobile Engagement back-end
1. Hallo installeren [MicrosoftAzure.MobileEngagement] Nuget-pakket in uw project. Als u voor zowel Windows als Windows Phone ontwikkelt, moet u toodo dit voor beide projecten. Voor Windows 8.x en Windows Phone 8.1, Hallo hetzelfde Nuget-pakket plaatsen Hallo juiste platform-specifieke binaire bestanden in elk project.
2. Open **Package.appxmanifest** en zorg ervoor dat Hallo volgende mogelijkheid is toegevoegd:

        Internet (Client)

    ![][2]
3. Nu Hallo verbindingsreeks die u eerder hebt gekopieerd voor uw Mobile Engagement-App kopiëren en plakken in Hallo `Resources\EngagementConfiguration.xml` bestand tussen Hallo `<connectionString>` en `</connectionString>` tags:

    ![][3]

    > [!TIP]
    > Als u een app maakt voor zowel Windows als Windows Phone, moet u nog steeds twee Mobile Engagement-toepassingen maken, een voor elk ondersteund platform. Met twee apps zorgt ervoor dat u juist segmentering van Hallo doelgroep maken kunt en op de juiste wijze gerichte meldingen voor elk platform kunt verzenden.

    > [!IMPORTANT]
    > NuGet kopiëren hello SDK-bronnen in uw Windows 10 UWP-toepassing niet automatisch. U hebt toodo het Hallo-stappen die worden weergegeven wanneer u Hallo Nuget-pakket is geïnstalleerd (Leesmij) handmatig te volgen.  

1. In Hallo `App.xaml.cs` bestand:

    a. Hallo toevoegen `using` instructie:

            using Microsoft.Azure.Engagement;

    b. Toevoegen van een methode die wordt geïnitialiseerd Hallo Engagement:

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    c. Hallo SDK in Hallo initialiseren **OnLaunched** methode:

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    c. Hallo volgende invoegen in Hallo **OnActivated** methode en het Hallo-methode toevoegen als deze nog niet aanwezig is:

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <a id="monitor"></a>Realtime-bewaking inschakelen
toostart verzenden van gegevens en ervoor te zorgen dat Hallo gebruikers actief zijn, moet u ten minste één scherm (activiteit) toohello Mobile Engagement back-end verzenden.

1. In Hallo **MainPage.xaml.cs**, voeg de volgende Hallo `using` instructie:

    met behulp van Microsoft.Azure.Engagement.Overlay;
2. Wijzigen van de basisklasse Hallo van **MainPage** van **pagina** te**EngagementPageOverlay**:

        class MainPage : EngagementPageOverlay
3. In Hallo `MainPage.xaml` bestand:

    a. Tooyour naamruimtedeclaraties toevoegen:

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    b. Vervang Hallo **pagina** in Hallo XML-tagnaam met **engagement: EngagementPageOverlay**

> [!IMPORTANT]
> Als uw pagina Hallo overschrijft `OnNavigatedTo` methode ervoor toocall worden `base.OnNavigatedTo(e)`. Hallo-activiteit is anders niet gerapporteerd `EngagementPage` aanroepen `StartActivity` binnen de `OnNavigatedTo` methode). Dit is vooral belangrijk in een Windows Phone-project waarbij de standaardsjabloon Hallo heeft een `OnNavigatedTo` methode.
>
> Voor **Windows 10 Universal-apps**, gebruik Hallo methode aanbevolen in Hallo ' aanbevolen methode: uw pagina klassen van de overbelasting ' sectie van [geavanceerde Reporting Hello Windows universele Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md) , in plaats van Hallo een hierboven vermeld.

## <a id="monitor"></a>App verbinden met realtime-bewaking
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen
Mobile Engagement kunt u toointeract en uw gebruikers met pushmeldingen en in-app-berichten in de context van campagnes Hallo bereiken. Deze module heet REACH in Hallo Mobile Engagement-portal.
Hallo volgende secties stelt u uw app tooreceive ze.

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a>Uw app tooreceive WNS-Pushmeldingen inschakelen
1. In Hallo `Package.appxmanifest` bestand in Hallo **toepassing** tabblad onder **meldingen**stelt **Toast capable:** te**Ja**

    ![][5]

### <a name="initialize-hello-reach-sdk"></a>Hallo bereiken SDK initialiseren
In `App.xaml.cs`, roepen **EngagementReach.Instance.Init(e);** in Hallo **InitEngagement** functie meteen na de initialisatie van de agent Hallo:

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

U bent klaar toosend een toast-melding. Vervolgens controleren we of u deze basisintegratie juist hebt uitgevoerd.

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a>Verleen toegang tooMobile Engagement toosend meldingen
1. Open het [ontwikkelaarscentrum voor Windows Store] in uw webbrowser, meld u aan, en maak indien nodig een account.
2. Klik op **Dashboard** op Hallo rechterbovenhoek hoek en klik vervolgens op **maakt een nieuwe app** Hallo linker deelvenster menu.

    ![][9]
3. Maak uw app door de naam ervan te reserveren.

    ![][10]
4. Zodra het Hallo-app is gemaakt, te navigeren**Services -> Push notifications** in het linkermenu Hallo.

    ![][11]
5. Push sectie meldingen in hello, klikt u op Hallo **Live Services site** koppeling.

    ![][12]
6. U navigeren gedeelte toohello Push credentials. Zorg ervoor dat u in Hallo **Appinstellingen** sectie en kopieer uw **pakket-SID** en **clientgeheim**

    ![][13]
7. Navigeer toohello **instellingen** van uw Mobile Engagement-portal en klikt u op Hallo **Native Pushbericht** sectie aan de linkerkant Hallo. Klik vervolgens op Hallo **bewerken** knop tooenter uw **pakket beveiligings-id (SID)** en uw **geheime sleutel** zoals wordt weergegeven:

    ![][6]
8. Controleer ten slotte dat u uw app in Visual Studio hebt gekoppeld aan deze app gemaakt in Hallo appstore. Klik in Visual Studio op **Associate App with Store** (App koppelen aan Store).

    ![][7]

## <a id="send"></a>Een melding tooyour app verzenden
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

Als het Hallo-app wordt uitgevoerd, ziet u een melding in de app. anders als Hallo app is gesloten, ziet u een pop-upmelding.
Als u een melding in de app, maar geen toast-melding ziet en u Hallo app in de foutopsporingsmodus in Visual Studio uitvoert, probeer **Lifecycle events -> Suspend** in Hallo werkbalk tooensure die Hallo-app is onderbroken. Als u de knop Start Hallo tijdens het opsporen van Hallo-toepassing in Visual Studio hebt geklikt, klikt u vervolgens het niet altijd onderbroken en terwijl u Hallo melding als in de app ziet, deze niet wordt weergegeven als een toast-melding.  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592
[ontwikkelaarscentrum voor Windows Store]: https://dev.windows.com
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
