---
title: aaaGet gestart met Azure Mobile Engagement voor Unity iOS-implementatie
description: Meer informatie over hoe toouse Azure Mobile Engagement met analyses en Pushmeldingen voor Unity-apps tooiOS apparaten implementeren.
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7ddfbac3-8d13-4ebe-b061-c865f357297f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f4247b0a9240cbe2bf1a6618388919d3554c07fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a>Aan de slag met Azure Mobile Engagement voor Unity iOS-implementatie
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Dit onderwerp leest u hoe toouse Azure Mobile Engagement toounderstand gebruik van uw Apps en hoe toosend push-meldingen toosegmented gebruikers van een Unity-toepassing bij het implementeren van tooan iOS-apparaat.
Deze zelfstudie maakt gebruik van Hallo klassieke Unity draaien een zelfstudie bDe volledige als Hallo beginpunt. U moet Hallo stappen in deze [zelfstudie](mobile-engagement-unity-roll-a-ball.md) voordat u doorgaat met de Hallo Mobile Engagement-integratie die we in Hallo onderstaande zelfstudie presenteren. 

Deze zelfstudie vereist de volgende Hallo:

* [Unity Editor](http://unity3d.com/get-unity)
* [Mobile Engagement Unity SDK](https://aka.ms/azmeunitysdk)
* XCode Editor

> [!NOTE]
> toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started) voor meer informatie.
> 
> 

## <a id="setup-azme"></a>Mobile Engagement instellen voor uw iOS-app
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
1. Open Hallo **EngagementConfiguration** scriptbestand uit het SDK-map en werk Hallo Hallo **IOS\_verbinding\_tekenreeks** met Hallo-verbindingsreeks die u eerder hebt verkregen. van hello Azure-portal.  
   
    ![][73]
2. Hallo-bestand opslaan. 

### <a name="configure-hello-app-for-basic-tracking"></a>Hallo-app voor eenvoudig bijhouden configureren
1. Open Hallo **PlayerController** script gekoppeld toohello Player object bewerken. 
2. Voeg de volgende Hallo met de instructie:
   
        using Microsoft.Azure.Engagement.Unity;
3. Hallo na toohello toevoegen `Start()` methode
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>Implementeren en het Hallo-app uitvoeren
1. Verbinding maken met een iOS-apparaat tooyour machine. 
2. Open **File -> Build Settings**. 
   
    ![][40]
3. Selecteer **iOS** en klik vervolgens op **Switch Platform**.
   
    ![][41]
   
    ![][42]
4. Klik op **Player settings** en geef een geldige bundel-id op. 
   
    ![][53]
5. Klik tot slot op **Build And Run**.
   
    ![][54]
6. Hebt u mogelijk gevraagd tooprovide een map naam toostore Hallo iOS-pakket. 
   
    ![][43]
7. Als alles goed gaat, Hallo project gecompileerd en u moet openen in uw XCode-toepassing. 
8. Zorg ervoor dat Hallo **bundel-id** in Hallo project juist is.  
   
    ![][75]
9. Nu Hallo app uitvoeren in XCode, zodat het Hallo-pakket geïmplementeerde tooyour aangesloten apparaat en ziet u de Unity-game op uw telefoon! 

## <a id="monitor"></a>App verbinden met realtime-bewaking
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Pushmeldingen en in-app-berichten inschakelen
Mobile Engagement kunt u toointeract met uw gebruikers- en bereiken met pushmeldingen en in-app-berichten in Hallo context van campagnes. Deze module heet REACH in Hallo Mobile Engagement-portal.
U hoeft toodo extra configuratie in uw app-meldingen tooreceive en is al ingesteld voor het.

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[40]: ./media/mobile-engagement-unity-ios-get-started/40.png
[41]: ./media/mobile-engagement-unity-ios-get-started/41.png
[42]: ./media/mobile-engagement-unity-ios-get-started/42.png
[43]: ./media/mobile-engagement-unity-ios-get-started/43.png
[53]: ./media/mobile-engagement-unity-ios-get-started/53.png
[54]: ./media/mobile-engagement-unity-ios-get-started/54.png
[70]: ./media/mobile-engagement-unity-ios-get-started/70.png
[71]: ./media/mobile-engagement-unity-ios-get-started/71.png
[72]: ./media/mobile-engagement-unity-ios-get-started/72.png
[73]: ./media/mobile-engagement-unity-ios-get-started/73.png
[74]: ./media/mobile-engagement-unity-ios-get-started/74.png
[75]: ./media/mobile-engagement-unity-ios-get-started/75.png
