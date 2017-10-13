---
title: Aan de slag met Azure Mobile Engagement voor Unity Android-implementatie
description: Informatie over het gebruik van Azure Mobile Engagement met analyses en pushmeldingen voor implementaties van Unity-apps op iOS-apparaten.
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: d5f0ef79-be00-4cec-97a5-a0b2fdaa380e
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bf0b758159d475b4ed7eadb84227e4824e11ba86
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a>Aan de slag met Azure Mobile Engagement voor Unity Android-implementatie
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

In dit onderwerp leest u hoe u Azure Mobile Engagement gebruikt om inzicht te krijgen in het gebruik van uw apps, en om pushmeldingen te verzenden aan gesegmenteerde gebruikers van een Unity-toepassing bij implementatie op een Android-apparaat.
Deze zelfstudie maakt gebruik van de bekende Unity-zelfstudie 'Roll a Ball' als uitgangspunt. Volg de stappen in deze [zelfstudie](mobile-engagement-unity-roll-a-ball.md) voordat u doorgaat met de Mobile Engagement-integratie die we in de onderstaande zelfstudie presenteren. 

Voor deze zelfstudie hebt u het volgende nodig:

* [Unity Editor](http://unity3d.com/get-unity)
* [Mobile Engagement Unity SDK](https://aka.ms/azmeunitysdk)
* Google Android SDK

> [!NOTE]
> U hebt een actief Azure-account nodig om deze zelfstudie te voltooien. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started) voor meer informatie.
> 
> 

## <a id="setup-azme"></a>Mobile Engagement instellen voor uw Android-app
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Uw app verbinden met de back-end van Mobile Engagement
### <a name="import-the-unity-package"></a>Het Unity-pakket importeren
1. Download het [Mobile Engagement Unity-pakket](https://aka.ms/azmeunitysdk) en sla het op uw lokale computer op. 
2. Ga naar **Assets -> Import Package -> Custom Package** en selecteer het pakket dat u in de vorige stap hebt gedownload. 
   
    ![][70] 
3. Zorg dat alle bestanden zijn geselecteerd en klik op de knop **Import**. 
   
    ![][71] 
4. Wanneer het importeren is voltooid, ziet u de geïmporteerde SDK-bestanden in het project.  
   
    ![][72] 

### <a name="update-the-engagementconfiguration"></a>EngagementConfiguration bijwerken
1. Open het scriptbestand **EngagementConfiguration** in de SDK-map en werk **ANDROID\_CONNECTION\_STRING** bij met de verbindingsreeks die u eerder hebt verkregen via de Azure-portal.  
   
    ![][73]
2. Sla het bestand op. 
3. Voer **File -> Engagement -> Generate Android Manifest** uit. Dit is de invoegtoepassing die is toegevoegd door Mobile Engagement SDK. Klik erop om uw projectinstellingen automatisch bij te werken. 
   
    ![][74]

> [!IMPORTANT]
> Zorg ervoor dat u dit altijd doet wanneer u het bestand **EngagementConfiguration** bijwerkt, omdat uw wijzigingen anders niet worden doorgevoerd in de app. 
> 
> 

### <a name="configure-the-app-for-basic-tracking"></a>De app voor eenvoudig bijhouden configureren
1. Open het script **PlayerController** dat is  gekoppeld aan het object Player om het te bewerken. 
2. Voeg het volgende toe met de instructie:
   
        using Microsoft.Azure.Engagement.Unity;
3. Het volgende toevoegen aan de methode `Start()`
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-the-app"></a>De app implementeren en uitvoeren
Zorg voor dat Android SDK is geïnstalleerd op uw computer voordat u deze Unity-app op uw apparaat gaat implementeren. 

1. Sluit een Android-apparaat aan op de computer. 
2. Open **File -> Build Settings**. 
   
    ![][40]
3. Selecteer **Android** en klik vervolgens op **Switch Platform**.
   
    ![][51]
   
    ![][52]
4. Klik op **Player settings** en geef een geldige bundel-id op. 
   
    ![][53]
5. Klik tot slot op **Build And Run**.
   
    ![][54]
6. U wordt mogelijk gevraagd een mapnaam op te geven voor het opslaan van het Android-pakket. 
7. Als alles goed gaat, wordt het pakket geïmplementeerd op het aangesloten apparaat en ziet u de Unity-game op uw telefoon. 

## <a id="monitor"></a>App verbinden met realtime-bewaking
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-the-engagementconfiguration"></a>EngagementConfiguration bijwerken
1. Open het scriptbestand **EngagementConfiguration** in de SDK-map en werk **ANDROID\_GOOGLE\_NUMBER** bij met het **Google Project Number** dat u eerder hebt verkregen via de Google Cloud Developer-portal. Dit is een tekenreeks die tussen dubbele aanhalingstekens moet worden geplaatst. 
   
    ![][75]
2. Sla het bestand op. 
3. Voer **File -> Engagement -> Generate Android Manifest** uit. Dit is de invoegtoepassing die is toegevoegd door Mobile Engagement SDK. Klik erop om uw projectinstellingen automatisch bij te werken. 
   
    ![][74]

### <a name="configure-the-app-to-receive-notifications"></a>De app configureren voor het ontvangen van meldingen
1. Open het script **PlayerController** dat is  gekoppeld aan het object Player om het te bewerken. 
2. Voeg het volgende toe aan de methode `Start()`.
   
        EngagementReachAgent.Initialize();
3. Nu de app is bijgewerkt, kunt u die implementeren en uitvoeren op een apparaat aan de hand van de onderstaande instructies. 

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[40]: ./media/mobile-engagement-unity-android-get-started/40.png
[70]: ./media/mobile-engagement-unity-android-get-started/70.png
[71]: ./media/mobile-engagement-unity-android-get-started/71.png
[72]: ./media/mobile-engagement-unity-android-get-started/72.png
[73]: ./media/mobile-engagement-unity-android-get-started/73.png
[74]: ./media/mobile-engagement-unity-android-get-started/74.png
[75]: ./media/mobile-engagement-unity-android-get-started/75.png
[51]: ./media/mobile-engagement-unity-android-get-started/51.png
[52]: ./media/mobile-engagement-unity-android-get-started/52.png
[53]: ./media/mobile-engagement-unity-android-get-started/53.png
[54]: ./media/mobile-engagement-unity-android-get-started/54.png
