---
title: aaaIoT DevKit toocloud - verbinding maken met IoT DevKit AZ3166 tooAzure IoT Hub | Microsoft Docs
description: Meer informatie over hoe toosetup en toosend gegevens toohello Azure-cloudplatform van IoT DevKit AZ3166 tooAzure IoT Hub voor deze verbinding in deze zelfstudie.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: xshi
ms.openlocfilehash: fd36abaed1fd9f73028b84312bca9e900fb9c004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-iot-devkit-az3166-tooazure-iot-hub-in-hello-cloud"></a>Verbinding maken met IoT DevKit AZ3166 tooAzure IoT-Hub in de cloud Hallo

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Hallo [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) kan worden gebruikt toodevelop en prototype Internet der dingen (IoT) oplossingen gebruik van Microsoft Azure-services. Het bevat een compatibel mededelingenbord Arduino met uitgebreide randapparatuur en sensoren, een open source mededelingenbord pakket en een groeiende [projecten catalogus](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).

## <a name="what-you-do"></a>Wat u doet
Verbinding maken met [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT hub maken, de temperatuur en vochtigheid gegevens verzamelen Hallo van sensoren en Hallo gegevens tooIoT hub te verzenden.

Heb je nog een DevKit? Ophalen van een nieuwe [hier](https://aka.ms/iot-devkit-purchase).

## <a name="what-you-learn"></a>Wat u leert

* Hoe tooconnect IoT DevKit tooWireless toegang wijst u en uw ontwikkelingsomgeving voorbereiden.
* Hoe toocreate een IoT-hub en een apparaat registreren voor MXChip IoT DevKit.
* Hoe toocollect sensorgegevens door het uitvoeren van een voorbeeld van toepassing op MXChip IoT DevKit.
* Hoe Hallo toosend sensor gegevens tooyour IoT-hub.

## <a name="what-you-need"></a>Wat u nodig hebt

* Een MXChip IoT DevKit moederbord met een micro USB-kabel. [Nu downloaden](https://aka.ms/iot-devkit-purchase)
* Een computer met Windows 10- of Mac OS 10.10 +
* Een actief Azure-abonnement
  * Activeren van een [gratis 30-daagse evaluatieversie Microsoft Azure-account](https://azureinfo.microsoft.com/us-freetrial.html)

## <a name="prepare-your-hardware"></a>Bereid uw hardware

Hallo hardware tooyour computer aansluiten.

### <a name="hardware-you-need"></a>U moet hardware

* DevKit mededelingenbord
* Micro USB-kabel

![ophalen van-slag-hardware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-tooyour-computer"></a>Verbind DevKit tooyour computer

1. Verbinding maken met USB-end tooyour PC
2. Verbinding maken met Micro USB end toohello DevKit
3. Hallo groen LED volgende toopower bevestigt verbinding

![ophalen van-slag-verbinding](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a>Wi-Fi configureren

IoT-projecten zijn afhankelijk van verbinding met Internet. Gebruik Hallo instructies tooconfigure hello DevKit tooconnect tooWiFi te volgen.

### <a name="enter-ap-mode"></a>Azië modus

Houd B, en vervolgens push en release Hallo herstelknop vervolgens release knop B. Uw DevKit opgeven voor het configureren van Wi-Fi AP-modus. welkomstscherm worden weergegeven Hallo Service ingesteld Identifier(SSID) Hallo DevKit evenals Hallo portal IP-adres:

![ophalen van-slag-Wi-Fi-Azië](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-toodevkit-ap"></a>Verbinding maken met tooDevKit Azië

Nu een andere Wi-Fi ingeschakeld apparaat (PC of mobiele telefoon) tooconnect toohello DevKit SSID (gemarkeerd in de bovenstaande Hallo) gebruiken, Hallo wachtwoord leeg laten.

![ophalen van-slag-ssid](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a>Wi-Fi voor DevKit configureren

Open Hallo IP-adres weergegeven op het Hallo DevKit scherm op uw PC of mobiele telefoon browser Hallo Wi-Fi-netwerk Hallo DevKit tooconnect te gewenste selecteren, en typ Hallo wachtwoord. Klik op **Connect** toocomplete:

![ophalen van-slag-Wi-Fi-portal](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

Zodra het Hallo-verbinding is geslaagd, wordt in een paar seconden Hallo DevKit opnieuw. Als de is voltooid, ziet u Hallo Wi-Fi-naam en IP-adres op het welkomstscherm:

![ophalen van-slag-Wi-Fi-ip](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
Hallo IP-adres weergegeven in Hallo photo mogelijk niet overeen met de Hallo werkelijke IP toegewezen en weergegeven op het welkomstscherm DevKit. Dit is normaal als Wi-Fi maakt gebruik van DHCP-toodynamically IP-adressen toewijzen.

Nadat Wi-Fi is geconfigureerd, worden uw referenties persistent op Hallo-apparaat voor die verbinding, zelfs als losgekoppeld. Bijvoorbeeld, als u Hallo DevKit geconfigureerd voor Wi-Fi thuis en vervolgens Hallo DevKit toohello office duurde, moet u tooreconfigure AP-modus (vanaf stap **Voer Azië modus**) tooconnect hello DevKit tooyour office Wi-Fi. 

## <a name="start-using-devkit"></a>Aan de slag met DevKit

Hallo standaard app uitgevoerd op DevKit wordt Hallo meest recente versie van de firmware Hallo controleren en sommige diagnose sensorgegevens weergeven voor u.

### <a name="upgrade-toohello-latest-firmware"></a>De meest recente firmware toohello bijwerken

U wordt gevraagd op het welkomstscherm die zowel huidige en de meest recente firmwareversie Hallo als er een upgrade nodig. Ga als volgt [firmware bijwerken](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) tooupgrade helpen deze.

![ophalen van-slag-firmware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
Dit is een eenmalige moeite, wanneer u begint met het ontwikkelen van op Hallo DevKit en uw app te uploaden, moet u de meest recente firmware Hallo worden geleverd met uw app.

### <a name="test-various-sensors"></a>Verschillende sensoren testen

Druk op de knop B tootest sensoren, blijven indrukken en loslaten Hallo B knop toocycle via elke sensor.

![ophalen van-slag-sensoren](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a>Ontwikkelingsomgeving voorbereiden

Nu gaat u tijd tooset van Hallo ontwikkelomgeving: hulpprogramma's en pakketten voor u toobuild bedwelmen IoT-toepassingen. U kunt Windows of Mac OS-versie op basis van het besturingssysteem tooyour.


### <a name="windows"></a>Windows

We raden u toouse Hallo installatie pakket tooprepare Hallo-ontwikkelomgeving. Als u problemen ondervindt, kunt u Hallo [handmatige stappen](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget doen.

#### <a name="download-latest-package"></a>Meest recente pakket te downloaden

Hallo `.zip` bestand downloaden bevat alle benodigde hulpprogramma's en pakketten die zijn vereist voor de ontwikkeling van DevKit.

> [!div class="button"]
[Downloaden](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> Hallo `.zip` bestand bevat Hallo volgende hulpprogramma's en pakketten. Als u al een aantal onderdelen geïnstalleerd hebt, Hallo script detecteert en ze overslaan.
> * Node.js en Yarn: Runtime voor het installatiescript Hallo en geautomatiseerde taken
> * [Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -platformoverschrijdende opdrachtregel ervaring voor het beheren van Azure-resources, Hallo MSI afhankelijke Python en pip bevat.
> * [Visual Studio Code](https://code.visualstudio.com/): Lightweight code-editor voor DevKit-ontwikkeling
> * [Visual Studio Code-uitbreiding voor Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): Arduino kunt ontwikkelen in VS-Code
> * [Arduino IDE](https://www.arduino.cc/en/Main/Software): Hallo-extensie voor Arduino is afhankelijk van dit hulpprogramma
> * DevKit mededelingenbord pakket: Hulpprogramma ketens, bibliotheken en projecten voor Hallo DevKit
> * ST koppeling hulpprogramma: Essentiële hulpprogramma's en stuurprogramma 's

#### <a name="run-installation-script"></a>Voer het script voor installatie

Zoek in Windows Verkenner, Hallo `.zip` en pak deze uit, Ga naar `install.cmd`, klik met de rechtermuisknop en selecteer **'Als administrator uitvoeren'** toostart.

![ophalen van-slag-run-admin](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

Tijdens de installatie ziet u Hallo voortgang van elk hulpprogramma of het pakket.

![ophalen van-slag-installatie](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-tooinstall-drivers"></a>Stuurprogramma's tooinstall bevestigen

Hallo VS-Code voor de extensie Arduino afhankelijk van Hallo Arduino IDE. Als dit Hallo eerst die u Hallo Arduino IDE installeert, kunt u zich na vragen aan gebruiker tooinstall relevante stuurprogramma's:

![ophalen van-slag-stuurprogramma](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

Het duurt ongeveer 10 minuten toofinish installatie, afhankelijk van uw Internet-snelheid. Zodra het Hallo-installatie is voltooid, ziet u Visual Studio Code en Arduino IDE snelkoppelingen op het bureaublad.

> [!NOTE] 
Van tijd tot tijd, wanneer u Code tegenover start, wordt u gevraagd met een fout die Arduino IDE of verwante mededelingenbord pakket niet vinden. toosolve deze sluiten VS-Code Arduino IDE eenmaal starten en VS-Code moet Arduino IDE pad correct vinden.


### <a name="macos-preview"></a>Mac OS (Preview)

Volg deze stappen tooprepare-ontwikkelomgeving op Mac OS.

#### <a name="install-azure-cli-20"></a>Azure CLI 2.0 installeren

Ga als volgt Hallo [officiële handleiding](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall Azure CLI 2.0:

Azure CLI 2.0 installeren met een `curl` opdracht:

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

En start de opdrachtshell voor wijzigingen tootake effect:

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a>Arduino IDE installeren

Hallo Visual Studio Code Arduino-extensie is afhankelijk van Hallo Arduino IDE. Download en installeer Hallo [Arduino IDE voor Mac OS](https://www.arduino.cc/en/Main/Software).

#### <a name="install-visual-studio-code"></a>Visual Studio Code installeren

Download en installeer [Visual Studio Code voor Mac OS](https://code.visualstudio.com/). Dit is de primaire ontwikkelprogramma Hallo voor het bouwen van DevKit IoT-toepassingen.

####  <a name="download-latest-package"></a>Meest recente pakket te downloaden

1. Installeer Node.js. U kunt de Pakketbeheer populaire Mac OS [Homebrew](https://brew.sh/) of [vooraf gemaakte installatieprogramma](https://nodejs.org/en/download/) tooinstall deze.

2. Download `.zip` -bestand met taak-scripts die zijn vereist voor de ontwikkeling van DevKit in VS-Code.

   > [!div class="button"]
   [Downloaden](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   Zoek Hallo `.zip` en pak het bestand. Start vervolgens **Terminal** app en Voer Hallo opdrachten tooconfigure te volgen:

   Verplaats de uitgepakte map tooyour Mac OS gebruikersmap:
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   Installeer `npm` pakketten:
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a>VS-Code-uitbreiding voor Arduino installeren

Visual Studio Code kunt u tooinstall Marketplace extensies rechtstreeks in Hallo hulpprogramma, klikt u op Hallo extensies pictogram in Hallo linkermenu deelvenster en zoek vervolgens `Arduino` tooinstall:

![installatie-extensies](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a>DevKit mededelingenbord pakket installeren

U moet tooadd hello DevKit mededelingenbord met Hallo mededelingenbord Manager in Visual Studio Code.

1. Gebruik `Cmd+Shift+P` tooinvoke palet en het type opdracht **Arduino** vervolgens zoeken en te selecteren **Arduino: mededelingenbord Manager**.

2. Klik op **extra URL's** op Hallo rechtsonder.
   ![installatie van extra URL](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)

3. In Hallo `settings.json` bestand, een regel toegevoegd aan de onderkant Hallo van `USER SETTINGS` deelvenster en op te slaan.
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![installatie-instellingen-json](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. Nu zoeken in Hallo mededelingenbord Manager 'az3166' en installeer de meest recente versie Hallo.
   ![installatie az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)

U hebt nu alle benodigde Hallo-hulpprogramma's en pakketten die zijn geïnstalleerd voor Mac OS.


## <a name="open-project-folder"></a>Open projectmap

### <a name="launch-vs-code"></a>VS Code starten

Zorg ervoor dat uw DevKit niet is verbonden. VS Code eerst start en Hallo DevKit tooyour computer verbinden. VS-Code wordt automatisch vinden en pop-up van een introductiepagina:

![Mini solution vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
Van tijd tot tijd, wanneer u Code tegenover start, wordt u gevraagd met fout die Arduino IDE of verwante mededelingenbord pakket niet vinden. toosolve deze sluiten VS-Code Arduino IDE opnieuw starten en VS-Code moet Arduino IDE pad correct vinden.

### <a name="open-arduino-examples-folder"></a>Voorbeelden van Arduino-map openen

Switch te**'Arduino voorbeelden'** tabblad, te navigeren`Examples for MXCHIP AZ3166 > AzureIoT` en klik op `GetStarted`.

![Mini solution-voorbeelden](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

Als u per ongeluk tooclose Hallo deelvenster tooreload ervan gebruik `Ctrl+Shift+P` (Mac OS: `Cmd+Shift+P`) tooinvoke palet en het type opdracht **Arduino** toofind en selecteer **Arduino: voorbeelden**.

## <a name="provision-azure-services"></a>Azure-services inrichten

Voer in Hallo oplossingsvenster uw taak via `Ctrl+P` (Mac OS: `Cmd+P`) door 'cloud inrichten van de taak' in te voeren:

VS Code terminal dat een interactieve opdrachtregel leidt u door de inrichting Hallo vereist in hello Azure-services:

![Mini-solution-cloud-inrichten](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a>Maken en uploaden Arduino schema

### <a name="install-required-library"></a>Installeren van vereiste bibliotheek

1. Druk op `F1` of `Ctrl+Shift+P` (Mac OS: `Cmd+Shift+P`) tooinvoke palet en het type opdracht **Arduino** vervolgens zoeken en te selecteren **Arduino: Library Manager**.

2. Zoeken naar `ArduinoJson` bibliotheek en klik op **installeren**

### <a name="build-and-upload-hello-device-code"></a>Maken en uploaden Hallo apparaatcode

Gebruik `Ctrl+P` (Mac OS: `Cmd+P`) toorun 'taak apparaat-upload'. Hallo terminal vraagt tooenter configuratiemodus. knop A toodo dus houd vervolgens push en release Hallo knop herstellen. welkomstscherm weergegeven 'Configuration'. Dit is tooset Hallo-verbindingsreeks die wordt opgehaald uit de stap 'taak cloud-provision'.

Vervolgens wordt gestart wordt gecontroleerd en Hallo Arduino schema uploaden:

![Mini-solution-apparaat-upload](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

Hallo DevKit wordt opnieuw opgestart en start Hallo code wordt uitgevoerd.

## <a name="test-hello-project"></a>Hallo testproject

Klik op Hallo power plug-pictogram op Hallo statusbalk tooopen Hallo seriële Monitor in VS-Code.

Hallo-voorbeeldtoepassing wordt correct uitgevoerd wanneer er Hallo resultaten te volgen:

* Hallo Hallo seriële Monitor geeft dezelfde informatie als Hallo inhoud in Hallo schermafbeelding hieronder.
* Hallo LED MXChip IoT DevKit knippert.

![Uiteindelijke uitvoer in VS-Code](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a>Problemen en feedback

U vindt [Veelgestelde vragen over](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) als u problemen ondervindt of toous van Hallo kanalen onderstaande bereiken.

## <a name="next-steps"></a>Volgende stappen

De verbinding van een MXChip IoT DevKit tooyour IoT-Hub gemaakt en verzonden hello vastgelegd sensor gegevens tooyour IoT-hub.

toocontinue aan de slag met IoT Hub en tooexplore raadpleegt u andere IoT-scenario's:

- [Berichten op cloudapparaten beheren met iothub-explorer](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [IoT Hub berichten tooAzure gegevensopslag opslaan](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [Gebruik Power BI toovisualize realtime-sensorgegevens uit Azure IoT Hub](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [Gebruik Azure Web Apps toovisualize realtime-sensorgegevens uit Azure IoT Hub](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [Weer voor de prognose met Hallo sensorgegevens uit uw IoT-hub in Azure Machine Learning](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [Apparaatbeheer met iothub-explorer](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [Externe bewaking en meldingen met Logic Apps](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)