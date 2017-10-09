---
title: aaaAzure Mobile Engagement demo-app | Microsoft Docs
description: Hier wordt beschreven waar toodownload, hoe demo app toouse en Hallo voordelen van het gebruik van Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: f624d5aa-254b-4ad0-96a3-f00e6c3a2c97
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2016
ms.author: piyushjo
ms.openlocfilehash: 9ff0df0d21e1bad6aff573db49304a55593df1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-demo-app"></a>Azure Mobile Engagement demo-app
We een Azure Mobile Engagement-demo-app voor hebt gepubliceerd **iOS**, **Android**, en **Windows** platforms toohelp u nuttige informatiebronnen toofind en meer informatie over mobiele Engagement.

Hallo app helpt u bij:

* Gemakkelijk nuttige koppelingen tooMobile Engagement bronnen zoals video's, documentatie, ondersteuningsforum hello, vinden en waar toogo tooraise functie aanvragen.
* Ervaring voorbeeld meldingen die worden ondersteund door de Mobile Engagement tooget ideeën voor uw eigen mobiele toepassingen.
* Gebruik een verwijzing implementatie toostudy hoe tooimplement Mobile Engagement in uw eigen app. U leert:
  
  * Analytische gegevens verzamelen.
  * Implementeer ingewikkelde melding van typen zoals *volledig scherm verspreide* of *pop-*.
  * Enquêtes en polls geïmplementeerd.
  * Gegevens en push achtergrond push-scenario's implementeren.   

## <a name="app-installation"></a>App-installatie
Deze app is beschikbaar in de volgende app-winkels Hallo:

* **Universele Windows-demo-app**:
  
  * Hallo-app op Hallo downloaden [Windows-App store](https://www.microsoft.com/en-us/store/apps/azure-mobile-engagement/9nblggh4qmh2).
  * Hallo-app is ontwikkeld als een Windows 10 Universal-app. Hallo broncode is beschikbaar op [GitHub](https://github.com/Azure/azure-mobile-engagement-app-windows).
* **iOS app demo**:
  
  * Hallo-app op Hallo downloaden [Apple store](https://itunes.apple.com/us/app/azure%20mobile%20engagement/id1105090090).
  * Hallo app is iOS Swift ontwikkeld. Hallo broncode is beschikbaar op [GitHub](https://github.com/Azure/azure-mobile-engagement-app-ios).
* **Android demo-app**:
  
  * Hallo-app op Hallo downloaden [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.azure.engagement).
  * Hallo broncode is beschikbaar op [GitHub](https://github.com/Azure/azure-mobile-engagement-app-android).

![Universele Windows-demo-app][1]

![iOS app demo][2]
![Android demo-app][3]

## <a name="usage"></a>Gebruik
U kunt deze app in de volgende manieren hello gebruiken:

**Hallo-app op uw apparaat downloaden van Hallo toepassing store koppelingen (eerder):**

> [!IMPORTANT]
> U hoeft niet een Azure-account of tooconnect Hallo app tooa back-end nodig. Hallo-app werkt onafhankelijk van elkaar.
> 
> 

* Nadat u Hallo-app op uw apparaat hebt, kunt u Hallo koppelingen in Hallo menu aan de linkerkant toofind Hallo nuttige informatiebronnen over de Mobile Engagement doorlopen.
* Hallo toegevoegd [van service RSS-feed](https://aka.ms/azmerssfeed) in deze toepassing zodat u altijd over de meest recente productupdates Hallo zijn bijgewerkt.
* U kunt ook gaan via Hallo voorbeeld scenario's tooexperience Hallo meldingstype van meldingen die worden ondersteund door de Mobile Engagement voor elk platform. Deze meldingen kunnen worden ervaren lokaal--dat wil zeggen, u kunt klikken op knoppen Hallo op Hallo schermen tooshow u Hallo meldingen-ervaring identiek toosending Hallo meldingen van Hallo Mobile Engagement-platform is.

![App-menu voor Windows][4]

![App-menu voor iOS][5]
![App-menu voor Android][6]

**Hallo broncode downloaden van Hallo GitHub koppelingen (eerder):**

* Nadat u de broncode Hallo hebt gedownload, opent u het in Hallo respectieve ontwikkelomgeving--XCode voor iOS, Android Studio voor Android- en Visual Studio voor Windows.
* U moet vervolgens volgen onze [basisstappen voor SDK-integratie](mobile-engagement-windows-store-dotnet-get-started.md) zodat u kunt tooconnect eigenaar van deze app tooits Mobile Engagement back-end-exemplaar.
  * U moet tooconfigure een verbindingsreeks in Hallo-app.
  * U moet ook tooconfigure Hallo push notification-platform voor uw app.
* U zult zien dat Hallo app zelf is uitgerust met Mobile Engagement. Dus als u Hallo app opent na de back-end toohello verbinding maken, moet u kunnen toosee Hallo gebruikerssessie, activiteiten, gebeurtenissen en enzovoort op Hallo **Monitor** tabblad.
* U zult ook kunnen toosend meldingen toothis app van uw eigen exemplaar van de Mobile Engagement, in plaats van lokale meldingen.
  
  * Hier u uw apparaat kunt toevoegen als een testapparaat met behulp van Hallo **Get Hallo apparaat-ID** menu-item in het Hallo-app. Dit biedt u een apparaat-ID die u vervolgens als een testapparaat met uw exemplaar van de back-end-platform registreren.
    
    ![Apparaat-ID in Windows][7]
    
    ![Apparaat-ID op iOS][8]
    ![op Android-apparaat-ID][9]

## <a name="key-features-of-hello-demo-app"></a>Belangrijke functies van Hallo demo-app
* Zoals eerder gezegd met deze app hebt u alle Hallo belangrijke bronnen voor Mobile Engagement in uw hand. U kunt koppelingen Hallo op Hallo linkermenu doorlopen.
* U kunt ervaren out-van-app-meldingen voor elk platform. Deze meldingen kunnen worden geleverd als **alleen melding**, waar te klikken op Hallo melding gewoon creëert een systeemeigen scherm van de toepassing hello (met behulp van **grondige koppelen**)-- of als een **Web aankondiging**, waar u kunt leveren extra HTML-inhoud van Mobile Engagement back-end Hallo toobe weergegeven als Hallo melding wordt geklikt.
  
    ![Out-van-app-meldingen][29]
* Op iOS hebt u tooclose Hallo app toosee Hallo out van de toepassing of het systeem pushmeldingen. U kunt zoeken op Hallo implementatie hier voor het toevoegen van **bewerkingsknoppen**, zoals die zijn toegevoegd toothis out-van-app-melding voor Hallo *Feedback* en *Share* (zodat Hallo-gebruiker kan actie-rechts vanaf Hallo melding zelf uitvoeren).
  
    ![Out-van-app-meldingen op iOS][11] ![Out-van-app-melding worden weergegeven op iOS][14]
* Op Android-, Hallo-opties die worden ondersteund met meerdere regels tekst toevoegt (**Big tekst**) of een installatiekopie van een melding (**grote afbeelding**) toohello melding, samen met de Hallo **bewerkingsknoppen** (als ondersteund door iOS).
  
    ![Out-van-app-meldingen op Android][12] ![Out-van-app-melding worden weergegeven op Android][15]
* Op Windows 10 ziet u hoe Hallo meldingen Hallo PC eruitzien. Deze melding wordt ook weergegeven in Windows 10 Hallo **Meldingencentrum**. Er is geen ondersteuning voor het toevoegen van **bewerkingsknoppen** op Hallo moment Hallo Windows SDK.
  
    ![Out-van-app-meldingen op Windows][10] ![Out van de toepassing worden weergegeven op Windows][13]
* U kunt ervaren standaard 'in-app' meldingen voor elk platform. Dit is een ervaring in twee stappen waarbij een **melding** venster als eerste wordt weergegeven. Wanneer u erop klikt, wordt geopend om een volledig scherm **aankondiging**, zoals weergegeven in de volgende schermafbeelding Hallo. Hallo-inhoud van deze aankondiging afkomstig van uw Mobile Engagement back-end-exemplaar. Hallo SDK heeft Hallo sjablonen voor meldingen en aankondigingen. U kunt ze gemakkelijk aanpassen zoals weergegeven in deze demo-app met Hallo toevoeging van onze logo en kleuren.  
  
    ![In-app-meldingen op Windows][16]
  
    ![In-app-meldingen op iOS][17]  ![In-app-meldingen op Android][18]
  
    **iOS**, **Android**
* U kunt ook Hallo **categorie** functie van Mobile Engagement toocustomize deze ervaring standaard. In Hallo demo-app, hebben we twee algemene ervaring manieren toochange Hallo Hallo meldingen gedemonstreerd. Houd er rekening mee dat Hallo categorie-functie is nog niet ondersteund in Hallo Windows SDK.
  
    **Volledig scherm verspreide:**
  
    ![In het app-melding - verspreide categorie][30]
  
    ![Verspreide categorie op iOS][21]     ![Verspreide categorie voor Android][22]
  
    **Pop-upbericht:**
  
    ![In het app-melding - pop-categorie][31]
  
    ![Pop-upbericht op iOS][19]    ![Pop-upbericht op Android][20]

**iOS**, **Android**

* Mobile Engagement biedt ook ondersteuning voor een speciaal type melding in de app aangeroepen **Polls**. Hiermee kunt u toosend snelle enquêtes tooyour gesegmenteerde app-gebruikers. U kunt vragen en opties voor elke vraag zoals in de volgende schermafbeelding Hallo toevoegen. Dit wordt vervolgens als een gebruiker in het app-melding toohello app worden weergegeven.   
  
    ![Poll-meldingen][32]
  
    ![Overzicht van Windows][26]
  
    ![Enquête op iOS][27]   ![Onderzoek op Android][28]

**iOS**, **Android**

* Mobile Engagement biedt ook ondersteuning voor verzenden van achtergrond **gegevens Push** meldingen. U kunt met deze meldingen gegevens verzenden van uw service (zoals Hallo JSON-gegevens in het volgende voorbeeld Hallo), die u kunt verwerken in uw app en een bepaalde actie ondernemen. Een voorbeeld is hoe we wijzigt Hallo prijs van een artikel selectief via pushmeldingen gegevens.
  
    ![Gegevens-push-melding][33]
  
    ![Gegevens-push-melding in Windows][23]
  
    ![Gegevens van pushmeldingen in iOS][24]  ![Gegevens-push-melding op Android][25]

**iOS**, **Android**

> [!NOTE]
> U kunt gedetailleerde stapsgewijze instructies voor een van deze meldingen weergeven door te klikken op **Klik hier voor instructies over het toosend deze meldingen van Mobile Engagement-platform** op een melding voorbeeldscherm.
> 
> 

[1]: ./media/mobile-engagement-demo-apps/home-windows.png
[2]: ./media/mobile-engagement-demo-apps/home-ios.png
[3]: ./media/mobile-engagement-demo-apps/home-android.png
[4]: ./media/mobile-engagement-demo-apps/menu-windows.png
[5]: ./media/mobile-engagement-demo-apps/menu-ios.png
[6]: ./media/mobile-engagement-demo-apps/menu-android.png
[7]: ./media/mobile-engagement-demo-apps/device-id-windows.png
[8]: ./media/mobile-engagement-demo-apps/device-id-ios.png
[9]: ./media/mobile-engagement-demo-apps/device-id-android.png
[10]: ./media/mobile-engagement-demo-apps/out-of-app-windows.png
[11]: ./media/mobile-engagement-demo-apps/out-of-app-ios.png
[12]: ./media/mobile-engagement-demo-apps/out-of-app-android.png
[13]: ./media/mobile-engagement-demo-apps/out-of-app-display-windows.png
[14]: ./media/mobile-engagement-demo-apps/out-of-app-display-ios.png
[15]: ./media/mobile-engagement-demo-apps/out-of-app-display-android.png
[16]: ./media/mobile-engagement-demo-apps/in-app-windows.png
[17]: ./media/mobile-engagement-demo-apps/in-app-ios.png
[18]: ./media/mobile-engagement-demo-apps/in-app-android.png
[19]: ./media/mobile-engagement-demo-apps/pop-up-ios.png
[20]: ./media/mobile-engagement-demo-apps/pop-up-android.png
[21]: ./media/mobile-engagement-demo-apps/interstitial-ios.png
[22]: ./media/mobile-engagement-demo-apps/interstitial-android.png
[23]: ./media/mobile-engagement-demo-apps/data-push-windows.png
[24]: ./media/mobile-engagement-demo-apps/data-push-ios.png
[25]: ./media/mobile-engagement-demo-apps/data-push-android.png
[26]: ./media/mobile-engagement-demo-apps/survey-windows.png
[27]: ./media/mobile-engagement-demo-apps/survey-ios.png
[28]: ./media/mobile-engagement-demo-apps/survey-android.png
[29]: ./media/mobile-engagement-demo-apps/out-of-app.png
[30]: ./media/mobile-engagement-demo-apps/in-app-interstitial.png
[31]: ./media/mobile-engagement-demo-apps/in-app-pop-up.png
[32]: ./media/mobile-engagement-demo-apps/notification-poll.png
[33]: ./media/mobile-engagement-demo-apps/notification-data-push.png
