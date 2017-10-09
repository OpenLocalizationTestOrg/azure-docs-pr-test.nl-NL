---
title: aaaGet de slag met Azure Mobile Engagement voor Windows Phone Silverlight-apps
description: Meer informatie over hoe toouse Azure Mobile Engagement met analyses en pushmeldingen voor Windows Phone Silverlight-apps.
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: aa34692f-87f7-47c6-a20c-a1972750bc25
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b39a838ab03217b2dc845cbf59d7bf8b094dac1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a>Aan de slag met Azure Mobile Engagement voor Windows Phone Silverlight-apps
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand uw app-gebruik en verzenden push notifications toosegmented gebruikers van een Windows Phone Silverlight-toepassing.
Deze zelfstudie laat zien Hallo eenvoudig broadcast-scenario met Mobile Engagement. In deze zelfstudie maakt u een lege Windows Phone Silverlight-app die basisgegevens verzamelt en pushmeldingen ontvangt via Microsoft Push Notification Service (MPNS).

> [!NOTE]
> Hallo Azure Mobile Engagement service buiten gebruik gesteld maart 2018 en is momenteel alleen beschikbaar tooexisting klanten. Zie [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/) voor meer informatie.

> [!NOTE]
> Projecten met Windows Phone 8.1 en een eerdere versie worden niet ondersteund in Visual Studio 2017.  Zie [Geschikte platforms voor Visual Studio 2017 en compatibiliteit](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs) voor meer informatie.

> [!NOTE]
> Als u ontwikkelt voor Windows Phone 8.1 (zonder Silverlight), raadpleegt u toohello [universele Windows-zelfstudie](mobile-engagement-windows-store-dotnet-get-started.md).
> 
> 

Deze zelfstudie vereist de volgende Hallo:

* Visual Studio 2013
* NuGet-pakket van [MicrosoftAzure.MobileEngagement]

> [!NOTE]
> toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started) voor meer informatie.
> 
> 

## <a id="setup-azme"></a>Mobile Engagement instellen voor uw Windows Phone-app
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end
Deze zelfstudie toont een 'basisintegratie', die wordt Hallo minimale vereiste toocollect gegevens instellen en een pushmelding verzenden. de volledige integratiedocumentatie Hallo vindt u in Hallo [Mobile Engagement Windows Phone SDK-integratie](mobile-engagement-windows-phone-sdk-overview.md)

We gaan een eenvoudige app maken met Visual Studio toodemonstrate Hallo-integratie.

### <a name="create-a-new-windows-phone-silverlight-project"></a>Een nieuw Windows Phone Silverlight-project maken
Hallo volgende stappen wordt ervan uitgegaan Hallo gebruik van Visual Studio 2015 al Hallo stappen vergelijkbaar in eerdere versies van Visual Studio zijn. 

1. Start Visual Studio en in Hallo **Start** Schakel in het scherm **nieuw Project**.
2. Selecteer in het pop-upvenster Hallo **Windows 8** -> **Windows Phone** -> **lege App (Windows Phone Silverlight)**. Vul Hallo app **naam** en **oplossingsnaam**, en klik vervolgens op **OK**.
   
    ![][1]
3. U kunt tootarget ofwel **Windows Phone 8.0** of **Windows Phone 8.1**.

U hebt nu een nieuwe Windows Phone Silverlight-app waarin we hello Azure Mobile Engagement SDK wordt integreren gemaakt.

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end
1. Hallo installeren [MicrosoftAzure.MobileEngagement] nuget-pakket in uw project.
2. Open `WMAppManifest.xml` (onder de map Hallo-eigenschappen) en zorg ervoor dat de volgende Hallo is gedeclareerd (Voeg ze als ze niet zijn) in Hallo `<Capabilities />` tag:
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. Nu Hallo verbindingsreeks die u eerder hebt gekopieerd voor uw Mobile Engagement-app te plakken en plak deze in Hallo `Resources\EngagementConfiguration.xml` bestand tussen Hallo `<connectionString>` en `</connectionString>` tags:
   
    ![][3]
4. In Hallo `App.xaml.cs` bestand:
   
    a. Hallo toevoegen `using` instructie:
   
            using Microsoft.Azure.Engagement;
   
    b. Hallo SDK in Hallo initialiseren `Application_Launching` methode:
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    c. Hallo volgende invoegen in Hallo `Application_Activated`:
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <a id="monitor"></a>Realtime-bewaking inschakelen
U moet ten minste één scherm (activiteit) toohello Mobile Engagement back-end verzenden in volgorde toostart verzenden van gegevens en ervoor te zorgen dat Hallo gebruikers actief zijn.

1. Voeg in MainPage.xaml.cs hello, Hallo `using` instructie:
   
        using Microsoft.Azure.Engagement;
2. Vervang de basisklasse Hallo van **MainPage**, die zich voor **PhoneApplicationPage**, met **EngagementPage**.
   
        class MainPage : EngagementPage 
3. In uw bestand `MainPage.xml`:
   
    a. Tooyour naamruimtedeclaraties toevoegen:
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    b. Vervang `phone:PhoneApplicationPage` in Hallo XML-tagnaam met `engagement:EngagementPage`.

## <a id="monitor"></a>App verbinden met realtime-bewaking
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen
Mobile Engagement kunt u toointeract en uw gebruikers via Pushmeldingen en in-app-berichten in de context van campagnes Hallo bereiken. Deze module heet REACH in Hallo Mobile Engagement-portal.
Hallo volgende secties stelt u uw app tooreceive ze.

### <a name="enable-your-app-tooreceive-mpns-push-notifications"></a>Uw app tooreceive MPNS-Pushmeldingen inschakelen
Toevoegen van nieuwe mogelijkheden tooyour `WMAppManifest.xml` bestand:

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-hello-reach-sdk"></a>Hallo bereiken SDK initialiseren
1. In `App.xaml.cs`, roepen `EngagementReach.Instance.Init();` in Hallo **Application_Launching** functie, meteen na de initialisatie van de agent Hallo:
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. In `App.xaml.cs`, roepen `EngagementReach.Instance.OnActivated(e);` in Hallo **Application_Activated** functie, meteen na de initialisatie van de agent Hallo:
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

U bent nu klaar. Nu controleren we of u hebt deze basisintegratie juist hebt uitgevoerd.

## <a id="send"></a>Een melding tooyour app verzenden
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

U ziet nu een melding op uw apparaat worden weergegeven als een in-app-melding indien Hallo app geopend of anders als een toast-melding zoals Hallo volgende is: 

![][6]

<!-- URLs. -->
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
