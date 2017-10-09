---
title: 'MyDriving Azure IoT-voorbeeld: snel aan de slag | Microsoft Docs'
description: Aan de slag met een app die is een uitgebreide demonstratie van het tooarchitect een IoT-systeem met Microsoft Azure, met inbegrip van de Stream Analytics, Machine Learning en Event Hubs.
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: f40ea71b-5721-4a6b-a886-53c2e9dffe8f
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 03/25/2016
ms.author: harikm
ms.openlocfilehash: 411b9a992deb22b915f8291d8559e2917d976b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="mydriving-iot-system-quick-start"></a>MyDriving IoT-systeem: snel starten
MyDriving is een systeem dat laat Hallo ontwerpen en implementeren van een typische zien [Internet der dingen](iot-suite-overview.md) (IoT)-oplossing die worden verzameld van telemetrie vanaf apparaten, die gegevens in de cloud Hallo verwerkt en van toepassing is machine learning tooprovide een adaptieve antwoord. Hallo-demonstratie registreert gegevens over uw reizen auto op basis van gegevens uit uw mobiele telefoon en een netwerkadapter die u gegevens van uw auto controlesysteem verzamelt. Deze gegevens tooprovide feedback wordt gebruikt op uw aangedreven stijl in vergelijking tooother gebruikers.

Hallo werkelijke doel van MyDriving is tooget die u gestart bij het maken van uw eigen IoT-oplossing. Maar vóór Hiermee kunt u beginnen met Hallo MyDriving app zelf--als lid van ons team van de gebruiker test. Dit biedt u een ervaring van Hallo-app en Hallo systeem erachter als een consument voordat u dieper Hallo-architectuur. Deze ook vindt u tooHockeyApp, een cool manier om Hallo alfa en beta distributies van uw apps tootest gebruikers te beheren.

## <a name="use-hello-mobile-experience"></a>Hallo mobiele ervaring gebruiken
U kunt Hallo MyDriving app gebruiken als u een Android, iOS of Windows 10-apparaat hebt.

### <a name="android-and-windows-10-mobile-installation"></a>Android en Windows 10 Mobile-installatie
Op uw apparaat:

1. Ontwikkeling van apps toestaan:
   
   * Android: In **instellingen** > **beveiliging**, toestaan dat apps uit **onbekende bronnen**.
   * Windows 10: In **instellingen** > **Updates** > **voor ontwikkelaars**stelt **ontwikkelaarsmodus**.
2. Deelnemen aan ons testteam beta door met registreert of aanmeldt, [HockeyApp](https://rink.hockeyapp.net). HockeyApp maakt het eenvoudig toodistribute prereleases van uw app tootest-gebruikers.
   
   Als u Windows 10, gebruikt u Hallo Edge-browser.
   
   Als u een deelnemer Build 2016, meld u aan met Hallo hetzelfde Microsoft-account e-mailbericht dat u voor Hallo conferentie, met behulp van een Microsoft-knoppen Hallo geregistreerd. U bent al aangemeld met HockeyApp.
   
   ![HockeyApp aanmeldingsscherm](./media/iot-solution-get-started/image1.png)
3. Download en installeer Hallo app vanaf hier:
   
   * [Android](http://rink.io/spMyDrivingAndroid)
   * [Windows 10](http://rink.io/spMyDrivingUWP)
   
   Er zijn twee items. Installeren van certificaat in Hallo **vertrouwde personen**. Hallo-app installeren.

*Hallo-app starten op Windows 10 Mobile problemen?* Uw telefoon is mogelijk een update of twee achter. Zorg ervoor dat u de nieuwste updates Hallo heeft of installeert:

* [Microsoft.NET.Native.Framework.1.2.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [Microsoft.NET.Native.Runtime.1.1.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [Microsoft.VCLibs.ARM.14.00.appx](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a>iOS-installatie
Als u Build 2016 hebt gevolgd, moet u Hallo-app downloaden als lid van ons testteam op HockeyApp:

1. Op uw iOS-apparaat, meld u aan te[HockeyApp](https://rink.hockeyapp.net).
   Gebruik een van de Microsoft-aanmelden-knoppen Hallo en meld u aan met dezelfde e-mail van de Microsoft-account dat u bij Hallo conferentie geregistreerd Hallo. (Gebruik niet Hallo e-mailadres en wachtwoord velden).
   
   ![HockeyApp aanmeldingsscherm](./media/iot-solution-get-started/image1.png)
2. In Hallo HockeyApp dashboard MyDriving Selecteer en download het.
3. Autoriseren hello bètaversie van HockeyApp:
   
   a. Ga te**instellingen** > **algemene** > **profielen en beheer van apparaten.**
   
   b. Hallo vertrouwen **bits Stadium GmbH** certificaat.

Als u niet de Build 2016 aandacht, kunt u app bouwen en implementeren Hallo zelf:

1. Hallo code downloaden [vanuit GitHub].
2. Bouwen en implementeren met [met Xamarin].

Meer informatie vinden in Hallo [MyDriving handleiding](http://aka.ms/mydrivingdocs).

## <a name="get-an-obd-adapter-optional"></a>Ophalen van een OBD-adapter (optioneel)
Dit is Hallo onderdeel waarmee dit een echte Internet der dingen-systeem! Hallo app zonder, kunt u maar meer plezier met Hallo echt een ding is, en ze niet duur.

Ingebouwde diagnostische gegevens (OBD) is de functie Hallo auto die Hallo garage gebruikt tootune van uw auto en onderzoeken van oneven geluiden en waarschuwing lichten. Tenzij uw auto van goede antiquity, vindt u een socket ergens in Hallo stuurcabine, doorgaans achter een flap onder Hallo-dashboard. U kunt met de juiste connector hello, metrische gegevens van Hallo motorprestaties ophalen en bepaalde wijzigingen aanbrengen. Een OBD-connector kan worden gekocht goedkoop Hallo gangbare locaties. Deze verbinding maakt met behulp van de Bluetooth- of Wi-Fi tooan-app op uw telefoon.

In dit geval gaan we tooconnect uw auto toohello cloud. Hallo rechtstreekse verbinding tussen Hallo OBD tooyour telefoonnummer is, maar onze app werkt als een relay. Telemetrie van uw auto wordt verzonden, rechte toohello MyDriving IoT hub, waar deze zich toolog verwerkt uw reizen weg en uw aangedreven stijl te beoordelen.

een apparaat OBD-tooconnect:

1. Controleer of uw auto een OBD-socket.
2. Vraag een OBD-adapter:
   
   * Als u een Android- en Windows phone, moet u een adapter OBD II Bluetooth-functionaliteit. We hebben gebruikt [BAFX producten 34t5 Bluetooth OBDII Scan Tool].
   * Als u een iOS-telefoon, moet u een Wi-Fi-functionaliteit OBD-adapter. We hebben gebruikt [onderzoekprogramma OBDLink MX Wi-Fi: OBD-Adapter/diagnose Scanner].
3. Volg Hallo-instructies die worden geleverd met uw OBD-adapter tooconnect het tooyour telefoon. Houd er rekening mee Hallo volgende:
   
   * Een Bluetooth-adapter moet worden gekoppeld aan het Hallo-telefoon, op Hallo **instellingen** pagina.
   * Een Wi-Fi-adapter moet een adres Hallo bereik 192.168.xxx.xxx hebben.
4. Als u verschillende auto's hebt, krijgt u een afzonderlijke adapter voor elke (maximaal drie).

Als u geen een OBD-adapter, stuurt Hallo app nog steeds locatie en gegevens van de snelheid van van Hallo telefoon GPS ontvanger toohello terug wordt gevraagd of u een OBD toosimulate wilt beëindigen.

U vindt hier meer over hoe Hallo app gebruikmaakt van gegevens uit de Hallo OBD-adapter en opties voor het maken van uw eigen apparaat OBD in sectie 2.1 'IoT-apparaten,' in hello [MyDriving handleiding](http://aka.ms/mydrivingdocs).

## <a name="use-hello-app"></a>Hallo-app gebruiken
Hallo-app te starten. Er is een initiële Quick Start-toowalk u stapsgewijs hoe het werkt.

### <a name="track-your-trips"></a>Uw reizen bijhouden
Tik op Hallo record knop (big rode cirkel onderaan Hallo welkomstscherm) toostart reis en tik nogmaals op tooend.

![Afbeelding van knop voor Hallo-record voor reis bijhouden](./media/iot-solution-get-started/image2.png)

Telkens wanneer die u een reis start als er geen OBD-apparaat, u gevraagd als u wilt dat toouse Hallo simulator.

Hallo na een reis Tik Hallo stop-knop, en u een samenvatting worden opgehaald.

![Voorbeeld van een reis samenvatting](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a>Bekijk uw reizen
![Voorbeeld van een eerdere reis](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a>Uw profiel bekijken
![Voorbeeld van een groot-stijl-profiel](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a>Stuur ons uw feedback test
Omdat we MyDriving toohelp aan de slag met uw eigen IoT-systemen gemaakt, willen we zeker toohear van u over hoe goed werkt. Laat ons weten als:

* U ondervindt problemen of uitdagingen.
* Er is een extensiepunt waaruit zou geschikte tooyour scenario.
* U vindt een efficiëntere manier tooaccomplish bepaalde behoeften.
* U hebt andere suggesties voor het verbeteren van MyDriving of deze documentatie.

Binnen Hallo MyDriving app zelf, kunt u Hallo ingebouwde HockeyApp feedback mechanisme: iOS en Android, net verleent op uw telefoon een schud of gebruik Hallo **Feedback** menuopdracht. Dit wordt automatisch een schermopname koppelen zodat we weet wat u bent bespreken. En als er vervelend crashes, HockeyApp verzamelt Hallo crash logboeken tootell ons informatie hierover. U kunt ook feedback via Hallo [HockeyApp-portal].

U kunt ook het bestand een [probleem op GitHub], of laat een opmerking hieronder (en-us edition).

We hopen toohearing van u!

## <a name="next-steps"></a>Volgende stappen
* Hallo verkennen [MyDriving handleiding](http://aka.ms/mydrivingdocs) toounderstand hoe we hebt ontwikkeld en gebouwd Hallo gehele MyDriving-systeem.
* [Maken en implementeren van een systeem van uw eigen](iot-solution-build-system.md) met behulp van de Azure Resource Manager-scripts. Hallo [MyDriving handleiding](http://aka.ms/mydrivingdocs) helpt u ook bij gebieden waarin u Hallo meeste aanpassingen zult.

[vanuit GitHub]: https://github.com/Azure-Samples/MyDriving
[met Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[BAFX producten 34t5 Bluetooth OBDII Scan Tool]: http://www.amazon.com/gp/product/B005NLQAHS
[onderzoekprogramma OBDLink MX Wi-Fi: OBD-Adapter/diagnose Scanner]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[HockeyApp-portal]: https://rink.hockeyapp.org
[probleem op GitHub]: https://github.com/Azure-Samples/MyDriving/issues
