---
title: 'MyDriving Azure IoT-voorbeeld: snel aan de slag | Microsoft Docs'
description: Aan de slag met een app die is een uitgebreide demonstratie van het bouwen van een IoT-systeem met Microsoft Azure, met inbegrip van de Stream Analytics, Machine Learning en Event Hubs.
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
ms.openlocfilehash: 031b492df1f186087e7b91102cbb44f552999293
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="mydriving-iot-system-quick-start"></a>MyDriving IoT-systeem: snel starten
MyDriving is een systeem dat laat zien van het ontwerp en de implementatie van een typische [Internet der dingen](iot-suite-overview.md) (IoT)-oplossing die worden verzameld van telemetrie vanaf apparaten, verwerkt die gegevens in de cloud en machine learning voor het bieden van toepassing is een adaptieve antwoord. Demonstratie van de gegevens over uw reizen auto geregistreerd met behulp van gegevens uit uw mobiele telefoon en een netwerkadapter die u gegevens van uw auto controlesysteem verzamelt. Deze gegevens maakt gebruik van deze feedback wilt geven over uw aangedreven style in vergelijking met andere gebruikers.

Het werkelijke doel van MyDriving is weer om u bij het maken van uw eigen IoT-oplossing is gestart. Maar voordat dat we u doorgaat met de MyDriving-app--als lid van ons team van de gebruiker test. Dit biedt u een ervaring van de app en het systeem erachter als een consument voordat u de architectuur dieper. Ook vindt u naar HockeyApp, een cool manier om de alfa en beta-distributies van uw apps te beheren voor het testen van gebruikers.

## <a name="use-the-mobile-experience"></a>Gebruik de mobiele-ervaring
Als u een Android, iOS of Windows 10-apparaat hebt, kunt u de MyDriving-app gebruiken.

### <a name="android-and-windows-10-mobile-installation"></a>Android en Windows 10 Mobile-installatie
Op uw apparaat:

1. Ontwikkeling van apps toestaan:
   
   * Android: In **instellingen** > **beveiliging**, toestaan dat apps uit **onbekende bronnen**.
   * Windows 10: In **instellingen** > **Updates** > **voor ontwikkelaars**stelt **ontwikkelaarsmodus**.
2. Deelnemen aan ons testteam beta door met registreert of aanmeldt, [HockeyApp](https://rink.hockeyapp.net). HockeyApp kunt gemakkelijk eerdere releases van uw app testen gebruikers distribueren.
   
   Als u Windows 10, gebruikt u de browser Edge.
   
   Als u een deelnemer Build 2016, aanmelden met het hetzelfde Microsoft-account e-mailbericht dat u geregistreerd voor de Conferentie via een van de Microsoft-knoppen. U bent al aangemeld met HockeyApp.
   
   ![HockeyApp aanmeldingsscherm](./media/iot-solution-get-started/image1.png)
3. Download en installeer de app vanaf deze locatie:
   
   * [Android](http://rink.io/spMyDrivingAndroid)
   * [Windows 10](http://rink.io/spMyDrivingUWP)
   
   Er zijn twee items. Installeer het certificaat in **vertrouwde personen**. Installeer de app.

*Problemen bij het starten van de app op Windows 10 Mobile?* Uw telefoon is mogelijk een update of twee achter. Zorg ervoor dat u de meest recente updates beschikt of installeren:

* [Microsoft.NET.Native.Framework.1.2.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [Microsoft.NET.Native.Runtime.1.1.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [Microsoft.VCLibs.ARM.14.00.appx](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a>iOS-installatie
Als u Build 2016 hebt gevolgd, moet u de app downloaden als lid van ons testteam op HockeyApp:

1. Op uw iOS-apparaat, moet u zich aanmelden bij [HockeyApp](https://rink.hockeyapp.net).
   Gebruik een van de Microsoft-aanmelden-knoppen en meld u aan met het hetzelfde Microsoft-account e-mailbericht dat u bij de Conferentie geregistreerd. (Gebruik niet de velden e-mailadres en wachtwoord).
   
   ![HockeyApp aanmeldingsscherm](./media/iot-solution-get-started/image1.png)
2. In het dashboard HockeyApp MyDriving Selecteer en download het.
3. De bètaversie van HockeyApp toestaan:
   
   a. Ga naar **instellingen** > **algemene** > **profielen en beheer van apparaten.**
   
   b. Vertrouwt de **bits Stadium GmbH** certificaat.

Als u hebt niet de Build 2016 letten, kunt u bouwen en implementeren van de app:

1. De code downloaden [vanuit GitHub].
2. Bouwen en implementeren met [met Xamarin].

Meer informatie in de [MyDriving handleiding](http://aka.ms/mydrivingdocs).

## <a name="get-an-obd-adapter-optional"></a>Ophalen van een OBD-adapter (optioneel)
Dit is het onderdeel dat dit een echte Internet der dingen-systeem is! Kunt u de app zonder een, maar meer plezier met de echte is, en ze niet duur.

Ingebouwde diagnostische gegevens (OBD) is de functie van uw auto die de garage gebruikt voor het optimaliseren van uw auto en onderzoeken van oneven geluiden en waarschuwing lichten. Tenzij uw auto van goede antiquity, vindt u een socket ergens in de stuurcabine, doorgaans achter een flap onder het dashboard. U kunt met de juiste connector metrische gegevens van de prestaties van de engine van ophalen en bepaalde wijzigingen aanbrengen. Een connector OBD kan goedkoop worden gekocht vanuit de gebruikelijke plaatsen. Deze verbinding maakt met behulp van de Bluetooth- of Wi-Fi met een app op uw telefoon.

In dit geval gaan we uw auto verbinding te maken met de cloud. De rechtstreekse verbinding tussen de OBD is naar uw telefoon, maar de app werkt als een relay. Telemetrie van uw auto wordt verzonden door naar de MyDriving IoT-hub, waar deze wordt verwerkt uw reizen weg aanmelden en uw aangedreven stijl te beoordelen.

Sluit een OBD-apparaat:

1. Controleer of uw auto een OBD-socket.
2. Vraag een OBD-adapter:
   
   * Als u een Android- en Windows phone, moet u een adapter OBD II Bluetooth-functionaliteit. We hebben gebruikt [BAFX producten 34t5 Bluetooth OBDII Scan Tool].
   * Als u een iOS-telefoon, moet u een Wi-Fi-functionaliteit OBD-adapter. We hebben gebruikt [onderzoekprogramma OBDLink MX Wi-Fi: OBD-Adapter/diagnose Scanner].
3. Volg de instructies die worden geleverd met uw OBD-netwerkadapter aansluiten op uw telefoon. Houd rekening met het volgende:
   
   * Een Bluetooth-adapter moet worden gekoppeld aan de telefoon op de **instellingen** pagina.
   * Een Wi-Fi-adapter moet een adres in het bereik 192.168.xxx.xxx hebben.
4. Als u verschillende auto's hebt, krijgt u een afzonderlijke adapter voor elke (maximaal drie).

Als u een adapter OBD geen hebt, wordt de app wordt nog steeds locatie en de snelheid van gegevens van de telefoon GPS-ontvanger verzonden naar de back-end en wordt u gevraagd of u wilt een OBD simuleren.

U kunt meer informatie over hoe de app gebruikmaakt van gegevens van de adapter OBD- en opties voor het maken van uw eigen apparaat OBD in sectie 2.1 'IoT-apparaten,' de [MyDriving handleiding](http://aka.ms/mydrivingdocs).

## <a name="use-the-app"></a>De app gebruiken
De app te starten. Er is een initiële Quick Start u stapsgewijs door het hoe het werkt.

### <a name="track-your-trips"></a>Uw reizen bijhouden
Tik op de knop opnemen (big rode cirkel aan de onderkant van het scherm) voor het starten van een reis en tik nogmaals op om te beëindigen.

![Afbeelding van de knop opnemen voor reis bijhouden](./media/iot-solution-get-started/image2.png)

Telkens wanneer die u een reis start als er geen OBD-apparaat, worden u gevraagd als u wilt gebruiken de simulator.

Aan het einde van een reis, tikt u op de knop stoppen, en u een samenvatting.

![Voorbeeld van een reis samenvatting](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a>Bekijk uw reizen
![Voorbeeld van een eerdere reis](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a>Uw profiel bekijken
![Voorbeeld van een groot-stijl-profiel](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a>Stuur ons uw feedback test
Omdat we MyDriving om te helpen aan de slag met uw eigen IoT-systemen gemaakt, willen we zeker graag van u over hoe goed werkt. Laat ons weten als:

* U ondervindt problemen of uitdagingen.
* Er is een extensiepunt zou om het meest geschikt is voor uw scenario.
* U vindt een efficiëntere manier voor het uitvoeren van bepaalde behoeften.
* U hebt andere suggesties voor het verbeteren van MyDriving of deze documentatie.

In de app MyDriving zelf, kunt u de ingebouwde HockeyApp feedback mechanisme: iOS en Android, net verleent op uw telefoon een schud of gebruik de **Feedback** menuopdracht. Dit wordt automatisch een schermopname koppelen zodat we weet wat u bent bespreken. En als er vervelend crashes, HockeyApp de Vertel ons meer over deze crash logboeken verzamelt. U kunt ook feedback via de [HockeyApp-portal].

U kunt ook het bestand een [probleem op GitHub], of laat een opmerking hieronder (en-us edition).

We hopen graag van u!

## <a name="next-steps"></a>Volgende stappen
* Verken de [MyDriving handleiding](http://aka.ms/mydrivingdocs) om te begrijpen hoe we hebt ontwikkeld en gebouwd van de gehele MyDriving-systeem.
* [Maken en implementeren van een systeem van uw eigen](iot-solution-build-system.md) met behulp van de Azure Resource Manager-scripts. De [MyDriving handleiding](http://aka.ms/mydrivingdocs) helpt u ook bij gebieden waar u de meeste aanpassingen maakt.

[vanuit GitHub]: https://github.com/Azure-Samples/MyDriving
[met Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[BAFX producten 34t5 Bluetooth OBDII Scan Tool]: http://www.amazon.com/gp/product/B005NLQAHS
[onderzoekprogramma OBDLink MX Wi-Fi: OBD-Adapter/diagnose Scanner]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[HockeyApp-portal]: https://rink.hockeyapp.org
[probleem op GitHub]: https://github.com/Azure-Samples/MyDriving/issues
