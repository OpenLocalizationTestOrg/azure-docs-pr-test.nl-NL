---
title: aaaGet de slag met Azure Mobile Engagement voor Web-Apps | Microsoft Docs
description: Meer informatie over hoe toouse Azure Mobile Engagement met analyses en pushmeldingen voor Web-Apps.
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04afe53a-4caf-4c80-bd75-20cc630cd75c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: hero-article
ms.date: 06/01/2016
ms.author: piyushjo
ms.openlocfilehash: a84c96cac13bf3b85e72aef55da5c91693e1766c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a>Aan de slag met Azure Mobile Engagement voor web-apps
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand gebruik van uw Web-App.

> [!NOTE]
> Hallo Azure Mobile Engagement service buiten gebruik gesteld maart 2018 en is momenteel alleen beschikbaar tooexisting klanten. Zie [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/) voor meer informatie.

Deze zelfstudie vereist de volgende Hallo:

* Visual Studio 2015 of een andere editor van uw keuze
* [Web SDK](http://aka.ms/P7b453)

Deze Web-SDK is Preview-versie en alleen Analytics Hallo momenteel ondersteunt en biedt geen ondersteuning voor pushmeldingen verzenden browser of in-app nog. 

> [!NOTE]
> toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started) voor meer informatie.
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a>Mobile Engagement instellen voor uw web-app
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end
Deze zelfstudie toont een 'basisintegratie,' Hallo minimale set die vereist toocollect gegevens.

We gaan een eenvoudige web-app maken met Visual Studio-integratie voor toodemonstrate hello, maar u Hallo met een webtoepassing die ook buiten Visual Studio gemaakt stappen kunt. 

### <a name="create-a-new-web-app"></a>Een nieuwe web-app maken
Hallo volgende stappen wordt ervan uitgegaan Hallo gebruik van Visual Studio 2015 al Hallo stappen vergelijkbaar in eerdere versies van Visual Studio zijn. 

1. Start Visual Studio en in Hallo **Start** Schakel in het scherm **nieuw Project**.
2. Selecteer in het pop-upvenster Hallo **Web** -> **ASP.Net-webtoepassing**. Vul Hallo app **naam**, **locatie** en **oplossingsnaam**, en klik vervolgens op **OK**.
3. In Hallo **Selecteer een sjabloon** pop-up Selecteer **leeg** onder **ASP.Net 4.5 sjablonen** en klik op **OK**. 

U hebt nu een nieuwe lege Web-App-project waarin hello Azure Mobile Engagement Web SDK is geïntegreerd gemaakt.

### <a name="connect-your-app-toomobile-engagement-backend"></a>Verbinding maken met uw app tooMobile Engagement back-end
1. Maak een nieuwe map **javascript** in uw oplossing en Hallo Web SDK JS bestand toevoegen **azure engagement.js** in de App. 
2. Voeg een nieuw bestand genaamd **main.js** in deze map javascript Hello code te volgen. Zorg ervoor dat tooupdate Hallo-verbindingsreeks. Dit `azureEngagement` -object worden gebruikte tooaccess Web SDK-methoden. 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Visual Studio met js-bestanden][1]

## <a name="enable-real-time-monitoring"></a>Realtime-bewaking inschakelen
U moet ten minste één activiteit toohello Mobile Engagement back-end verzenden in volgorde toostart verzenden van gegevens en ervoor te zorgen dat Hallo gebruikers actief zijn. Een activiteit in de context Hallo van een web-app is een webpagina. 

1. Maak een nieuwe pagina aangeroepen **home.html** in uw oplossing en als Hallo vanaf pagina voor uw web-app. 
2. Hallo twee JavaScript die we eerder in deze pagina hebt toegevoegd door toe te voegen Hallo volgende binnen Hallo hoofdtekst tag bevatten. 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. Hallo hoofdtekst tag toocall EngagementAgent van bijwerken `startActivity` methode
   
        <body onload="engagement.agent.startActivity('Home')">
4. Zo ziet uw **home.html**-pagina eruit
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a>App verbinden met realtime-bewaking
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a>Analyse uitbreiden
Hier zijn alle Hallo methoden beschikbaar met Web-SDK die u voor analyses kunt gebruiken:

1. Activiteiten/webpagina's:
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. Gebeurtenissen
   
        engagement.agent.sendEvent(name, extras);
3. Fouten
   
        engagement.agent.sendError(name, extras);
4. Taken
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

