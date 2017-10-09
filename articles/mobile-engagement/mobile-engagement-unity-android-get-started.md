---
title: aaaGet gestart met Azure Mobile Engagement voor Unity Android-implementatie
description: Meer informatie over hoe toouse Azure Mobile Engagement met analyses en Pushmeldingen voor Unity-apps tooiOS apparaten implementeren.
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
ms.openlocfilehash: c4d34691daeb7544b11c2d6895b2474af0f902b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a>Aan de slag met Azure Mobile Engagement voor Unity Android-implementatie
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand gebruik van uw Apps en hoe toosend push-meldingen toosegmented gebruikers van een Unity-toepassing bij het implementeren van tooan Android-apparaat.
Deze zelfstudie maakt gebruik van Hallo klassieke Unity draaien een zelfstudie bDe volledige als Hallo beginpunt. U moet Hallo stappen in deze [zelfstudie](mobile-engagement-unity-roll-a-ball.md) voordat u doorgaat met de Hallo Mobile Engagement-integratie die we in Hallo onderstaande zelfstudie presenteren. 

Deze zelfstudie vereist de volgende Hallo:

* [Unity Editor](http://unity3d.com/get-unity)
* [Mobile Engagement Unity SDK](https://aka.ms/azmeunitysdk)
* Google Android SDK

> [!NOTE]
> toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started) voor meer informatie.
> 
> 

## <a id="setup-azme"></a>Mobile Engagement instellen voor uw Android-app
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Verbinding maken met uw app toohello Mobile Engagement-back-end
### <a name="import-hello-unity-package"></a>Hallo Unity-pakket importeren
1. Hallo downloaden [Mobile Engagement Unity-pakket](https://aka.ms/azmeunitysdk) en sla het tooyour lokale computer. 
2. Ga te**Assets -> Import Package -> Custom Package** en u hebt gedownload in Hallo hierboven stap Selecteer Hallo-pakket. 
   
    ![][70] 
3. Zorg dat alle bestanden zijn geselecteerd en klik op de knop **Import**. 
   
    ![][71] 
4. Nadat het importeren is voltooid, ziet u Hallo geïmporteerd SDK-bestanden in uw project.  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a>Hallo EngagementConfiguration bijwerken
1. Open Hallo **EngagementConfiguration** scriptbestand uit het SDK-map en werk Hallo Hallo **ANDROID\_verbinding\_tekenreeks** met Hallo-verbindingsreeks die u hebt verkregen oudere versies van hello Azure-portal.  
   
    ![][73]
2. Hallo-bestand opslaan 
3. Voer **File -> Engagement -> Generate Android Manifest** uit. Dit is toegevoegd door Mobile Engagement SDK Hallo Hallo-invoegtoepassing en erop te klikken, wordt uw projectinstellingen automatisch bijgewerkt. 
   
    ![][74]

> [!IMPORTANT]
> Hiervan ervoor tooexecute telkens wanneer u Hallo bijwerken **EngagementConfiguration** bestand anders uw wijzigingen niet worden doorgevoerd in Hallo-app. 
> 
> 

### <a name="configure-hello-app-for-basic-tracking"></a>Hallo-app voor eenvoudig bijhouden configureren
1. Open Hallo **PlayerController** script gekoppeld toohello Player object bewerken. 
2. Voeg de volgende Hallo met de instructie:
   
        using Microsoft.Azure.Engagement.Unity;
3. Hallo na toohello toevoegen `Start()` methode
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>Implementeren en het Hallo-app uitvoeren
Zorg ervoor dat er Android SDK is geïnstalleerd op uw computer voordat u dit apparaat Unity-app tooyour probeert toodeploy. 

1. Verbinding maken met een Android-apparaat tooyour-machine. 
2. Open **File -> Build Settings**. 
   
    ![][40]
3. Selecteer **Android** en klik vervolgens op **Switch Platform**.
   
    ![][51]
   
    ![][52]
4. Klik op **Player settings** en geef een geldige bundel-id op. 
   
    ![][53]
5. Klik tot slot op **Build And Run**.
   
    ![][54]
6. Hebt u mogelijk gevraagd tooprovide een map naam toostore hello Android-pakket. 
7. Als alles goed, gaat wordt Hallo pakket geïmplementeerde tooyour verbonden ziet apparaat en u de Unity-game op uw telefoon! 

## <a id="monitor"></a>App verbinden met realtime-bewaking
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-hello-engagementconfiguration"></a>Hallo EngagementConfiguration bijwerken
1. Open Hallo **EngagementConfiguration** scriptbestand uit het SDK-map en werk Hallo Hallo **ANDROID\_GOOGLE\_getal** Hello **Google Project Aantal** u eerder hebt verkregen via Hallo Google Cloud Developer portal. Dit is een tekenreeks waarde dus zorg ervoor dat tooenclose deze tussen dubbele aanhalingstekens. 
   
    ![][75]
2. Hallo-bestand opslaan. 
3. Voer **File -> Engagement -> Generate Android Manifest** uit. Dit is toegevoegd door Mobile Engagement SDK Hallo Hallo-invoegtoepassing en erop te klikken, wordt uw projectinstellingen automatisch bijgewerkt. 
   
    ![][74]

### <a name="configure-hello-app-tooreceive-notifications"></a>Hallo app tooreceive meldingen configureren
1. Open Hallo **PlayerController** script gekoppeld toohello Player object bewerken. 
2. Hallo na toohello toevoegen `Start()` methode
   
        EngagementReachAgent.Initialize();
3. Nu dat hello app is bijgewerkt, implementeren en uitvoeren van Hallo-app op een apparaat per Hallo onderstaande instructies. 

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
