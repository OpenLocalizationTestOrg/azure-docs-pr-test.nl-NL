---
title: Verbinding maken met Raspberry Pi (C) naar Azure IoT - oplossen | Microsoft Docs
description: Pagina voor de frambozen Pi Node.js-ervaring voor probleemoplossing
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT-problemen, internet der dingen problemen
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 22cf50dc-8206-42a2-a1fc-f75fa85135fa
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f9058068972ddbb674d3cd159948835dc88c4451
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a>Problemen oplossen
## <a name="hardware-issues"></a>Hardwareproblemen
### <a name="the-application-runs-well-but-the-led-is-not-blinking"></a>De toepassing goed wordt uitgevoerd, maar niet de LED knippert
Dit probleem is altijd gerelateerd aan hardware circuit connectiviteit. Gebruik de volgende stappen om problemen te identificeren:

1. Controleer dat u hebt ervoor de juiste gekozen **GPIO** op het mededelingenbord. De twee poorten moet **GPIO GND (pincode 6)** en **GPIO 04 (7 pincode)**.
2. Controleer of de polariteit van uw LED juist is. De langer arm zou moeten aangeven waarom de **positief**, gebruikte pincodes.
3. Gebruik de **3, 3v vastmaken** en **GND pincode** op frambozen Pi 3. De DC-macht Pi behandeld. Controleer of de LED prima werkt.

![LED specificatie](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a>Andere hardwareproblemen
Zie voor meer informatie over het oplossen van veelvoorkomende problemen bij frambozen Pi 3 de [officiële pagina voor probleemoplossing](http://elinux.org/R-Pi_Troubleshooting).

## <a name="nodejs-package-issues"></a>Problemen met node.js-pakket
### <a name="no-response-during-gulp-tasks"></a>Geen reactie tijdens gulp taken
Als u problemen ondervindt met actieve taken gulp, kunt u toevoegen de `--verbose` optie voor foutopsporing. Huidige gulp taken beëindigd met behulp van Ctrl + C, en voer de volgende opdracht in het consolevenster om te zien foutopsporingsberichten. Gedetailleerde foutberichten ziet u in de console-uitvoer.

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>Problemen met detectie van apparaat
Voor hulp bij het oplossen van veelvoorkomende problemen met de `devdisco` opdracht, Controleer de [Leesmij](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).

### <a name="npm-issues"></a>npm problemen
Voer uw npm pakket bijwerken met behulp van de volgende opdracht:

```bash
npm install -g npm
```

Als het probleem blijft optreden, laat u hierop een toelichting aan het einde van dit artikel of maak een GitHub-probleem in onze [voorbeeld opslagplaats](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).

## <a name="remote-debugging"></a>Foutopsporing op afstand
### <a name="run-the-sample-application-in-debug-mode"></a>De voorbeeldtoepassing in de foutopsporingsmodus uitvoeren
```bash
gulp run --debug
```

Wanneer de engine voor foutopsporing klaar is, ziet u ```Debugger listening on port 5858``` in de console-uitvoer.

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a>Visual Studio Code verbinding maken met het externe apparaat configureren
1. Open de **Debug** deelvenster aan de linkerkant.
2. Klik op de groene **foutopsporing starten** knop (F5). Visual Studio Code een launch.json-bestand wordt geopend.
3. Het bestand launch.json bijwerken met de volgende inhoud. Vervang `[device hostname or IP address]` met de werkelijke IP-adres of de hostnaam apparaatnaam.

> [!NOTE]
> Voor meer informatie over de foutopsporing Visual Studio, Raadpleeg [foutopsporing in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).


```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "[device hostname or IP address]",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": null
        }
    ]
}
```

![Configuratie van extern foutopsporing](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-to-the-remote-application"></a>Koppelen aan de externe toepassing
Klik op de groene **foutopsporing starten** (F5) knop foutopsporing te starten.

Lees [JavaScript in VS-Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) voor meer informatie over het foutopsporingsprogramma.

![Externe interactieve foutopsporing](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Problemen met Azure CLI
De Azure-opdrachtregelinterface (Azure CLI) is een preview-versie. Als u wilt zoeken naar oplossingen, kunt u de [Preview installeren handleiding](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).

Als u met het hulpprogramma fouten optreden, het bestand een [probleem](https://github.com/Azure/azure-cli/issues) in de **problemen** sectie van de GitHub-repo.

Als u hulp nodig hebt bij het oplossen van veelvoorkomende problemen, Controleer de [Leesmij](https://github.com/Azure/azure-cli/blob/master/README.rst).

## <a name="python-installation-issues"></a>Problemen met de installatie van Python
### <a name="legacy-installation-issues-macos"></a>Verouderde installatieproblemen (Mac OS)
Wanneer u pip installeert, een machtigingsfout wordt gegenereerd wanneer oudere pakketten worden geïnstalleerd met **su** machtigingen. Deze situatie doet zich voor omdat een eerdere installatie van Python met brew (Mac OS) is niet volledig verwijderd. Sommige pakketten pip van een eerdere installatie zijn gemaakt door root, waardoor de machtiging fout optreedt. De oplossing is om te verwijderen die pakketten geïnstalleerd door de hoofdmap. Gebruik de volgende stappen uit om deze taak te voltooien:

1. Ga naar: /usr/local/lib/python2.7/site-packages
2. Lijst met pakketten gemaakt door hoofdmap:`ls -l | grep root`
3. Verwijderen van pakketten uit stap 2:`sudo rm -rf {package name}`
4. Installeer Python.

## <a name="azure-iot-hub-issues"></a>Problemen met Azure IoT Hub
Als u uw Azure-IoT-hub met Azure CLI met succes hebt ingericht en u een hulpprogramma moet voor het beheren van de apparaten die zijn verbonden met uw IoT-hub, kunt u de volgende hulpprogramma's.

### <a name="device-explorer"></a>Apparaat explorer
De [apparaat explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) hulpprogramma wordt uitgevoerd op uw lokale Windows-computer en verbinding maakt met uw IoT-hub in Azure. Er wordt gecommuniceerd met de volgende [IoT-hubeindpunten](iot-hub-devguide.md):


* *Identiteiten Apparaatbeheer* inrichten en beheren van apparaten die zijn geregistreerd met uw IoT-hub.
* *Apparaat-naar-cloud ontvangen* zodat u berichten van uw apparaat voor uw IoT-hub kunt bewaken.
* *Cloud naar apparaat verzenden* zodat u berichten naar uw apparaten van uw IoT-hub verzenden kunt.

Configureer uw IoT hub-verbindingsreeks vanuit dit hulpprogramma te gebruiken van de mogelijkheden ervan.

### <a name="iothub-explorer"></a>iothub explorer
[iothub explorer](https://github.com/Azure/iothub-explorer) is een voorbeeld meerdere platforms CLI-hulpprogramma om apparaten te beheren. Het hulpprogramma kunt u de apparaten in het identiteitenregister beheren, apparaat-naar-cloud-berichten worden gecontroleerd en cloud-naar-apparaat-berichten verzenden.

Voer de volgende opdracht in uw omgeving opdrachtregelprogramma voor het installeren van de meest recente (voorlopige) versie van het hulpprogramma iothub explorer:

```bash
npm install -g iothub-explorer@latest
```

De volgende opdracht kunt u extra hulp vragen over alle iothub explorer-opdrachten en de bijbehorende parameters:

```bash
iothub-explorer help
```

### <a name="azure-portal"></a>Azure Portal
Een volledige CLI-ervaring helpt u bij het maken en beheren van alle Azure-resources. U kunt ook gebruik van de [Azure-portal](../azure-portal-overview.md) kunt inrichten, beheren en fouten opsporen in uw Azure-resources.

## <a name="azure-storage-issues"></a>Azure Storage-problemen
[Microsoft Azure Opslagverkenner (preview)](http://storageexplorer.com) is een zelfstandige app van Microsoft die u gebruiken kunt voor het werken met Azure Storage-gegevens op Windows-, Mac OS- en Linux. Met dit hulpprogramma kunt u verbinding maken met uw tabel en de gegevens weergegeven in het. U kunt dit hulpprogramma om problemen met uw Azure Storage te gebruiken.

