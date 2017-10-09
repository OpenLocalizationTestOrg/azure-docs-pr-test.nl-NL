---
title: Connect Raspberry PI (C) tooAzure IoT - oplossen | Microsoft Docs
description: Het oplossen van de pagina voor Hallo frambozen Pi Node.js-ervaring
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
ms.openlocfilehash: 8f0807104550e8e53a132f7741564b33f1db17ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Problemen oplossen
## <a name="hardware-issues"></a>Hardwareproblemen
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a>Hallo-toepassing wordt uitgevoerd en maar Hallo LED knippert niet
Dit probleem is altijd gerelateerde toohardware circuit netwerkverbinding. Na de stappen tooidentify problemen hello gebruiken:

1. Controleer dat u hebt gekozen Hallo juist **GPIO** op het mededelingenbord. Hallo twee poorten moet **GPIO GND (pincode 6)** en **GPIO 04 (7 pincode)**.
2. Controleer of de polariteit Hallo van uw LED juist is. Hallo langer arm zou moeten aangeven waarom Hallo **positief**, gebruikte pincodes.
3. Gebruik Hallo **3, 3v vastmaken** en **GND pincode** op frambozen Pi 3. Hallo DC power Pi behandeld. Controleer dat Hallo LED werkt prima.

![LED specificatie](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a>Andere hardwareproblemen
Zie voor informatie over het oplossen van veelvoorkomende problemen bij frambozen Pi 3 Hallo [officiële pagina voor probleemoplossing](http://elinux.org/R-Pi_Troubleshooting).

## <a name="nodejs-package-issues"></a>Problemen met node.js-pakket
### <a name="no-response-during-gulp-tasks"></a>Geen reactie tijdens gulp taken
Als u problemen ondervindt met actieve taken gulp, kunt u toevoegen Hallo `--verbose` optie voor foutopsporing. Probeer tooterminate huidige gulp taken met behulp van Ctrl + c drukken en voer de volgende opdracht in uw foutopsporingsberichten console venster toosee Hallo. Gedetailleerde foutberichten ziet u in de console-uitvoer.

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>Problemen met detectie van apparaat
Voor hulp bij het oplossen van veelvoorkomende problemen met Hallo `devdisco` opdracht, controleert u Hallo [Leesmij](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).

### <a name="npm-issues"></a>npm problemen
Probeer tooupdate de npm-pakket met behulp van de volgende opdracht Hallo:

```bash
npm install -g npm
```

Als Hallo probleem blijft optreden, laat u hierop een toelichting op Hallo einde van dit artikel of maak een GitHub-probleem in onze [voorbeeld opslagplaats](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).

## <a name="remote-debugging"></a>Foutopsporing op afstand
### <a name="run-hello-sample-application-in-debug-mode"></a>Hallo-voorbeeldtoepassing in de foutopsporingsmodus uitvoeren
```bash
gulp run --debug
```

Wanneer foutopsporing-engine Hallo klaar is, ziet u ```Debugger listening on port 5858``` in Hallo console-uitvoer.

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a>Visual Studio Code tooconnect toohello externe apparaten configureren
1. Open Hallo **Debug** Configuratiescherm op Hallo linkerkant.
2. Klik op Hallo groen **foutopsporing starten** knop (F5). Visual Studio Code een launch.json-bestand wordt geopend.
3. Hallo launch.json updatebestand Hello inhoud te volgen. Vervang `[device hostname or IP address]` met Hallo werkelijke IP-adres of de hostnaam apparaatnaam.

> [!NOTE]
> toolearn meer informatie over Hallo Visual Studio foutopsporing Raadpleeg te[foutopsporing in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).


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

### <a name="attach-toohello-remote-application"></a>De externe toepassing toohello koppelen
Klik op Hallo groen **foutopsporing starten** (F5) knop toostart foutopsporing.

Lees [JavaScript in VS-Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn meer informatie over Hallo foutopsporing.

![Externe interactieve foutopsporing](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Problemen met Azure CLI
Hello Azure-opdrachtregelinterface (Azure CLI) is een preview-versie. oplossingen voor tooseek, kunt u Hallo [Preview installeren handleiding](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).

Als u fouten met Hallo hulpprogramma tegenkomt, het bestand een [probleem](https://github.com/Azure/azure-cli/issues) in Hallo **problemen** sectie van de GitHub-repo-Hallo.

Controleer voor hulp bij het oplossen van veelvoorkomende problemen Hallo [Leesmij](https://github.com/Azure/azure-cli/blob/master/README.rst).

## <a name="python-installation-issues"></a>Problemen met de installatie van Python
### <a name="legacy-installation-issues-macos"></a>Verouderde installatieproblemen (Mac OS)
Wanneer u pip installeert, een machtigingsfout wordt gegenereerd wanneer oudere pakketten worden geïnstalleerd met **su** machtigingen. Deze situatie doet zich voor omdat een eerdere installatie van Python met brew (Mac OS) is niet volledig verwijderd. Sommige pakketten pip van een eerdere installatie zijn gemaakt door root, waardoor Hallo machtigingsfout. Hallo oplossing tooremove die pakketten door basiscertificeringsinstantie geïnstalleerd is. Hallo toocomplete stappen te volgen met deze taak gebruiken:

1. Ga naar: /usr/local/lib/python2.7/site-packages
2. Lijst met pakketten gemaakt door hoofdmap:`ls -l | grep root`
3. Verwijderen van pakketten uit stap 2:`sudo rm -rf {package name}`
4. Installeer Python.

## <a name="azure-iot-hub-issues"></a>Problemen met Azure IoT Hub
Als u uw Azure-IoT-hub met Azure CLI met succes hebt ingericht en moet u een hulpprogramma toomanage Hallo-apparaten die verbinding maken tooyour iothub, probeer Hallo hulpprogramma's te volgen.

### <a name="device-explorer"></a>Apparaat explorer
Hallo [apparaat explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) hulpprogramma wordt uitgevoerd op uw lokale Windows-computer en verbinding maakt tooyour IoT-hub in Azure. Er wordt gecommuniceerd met de volgende Hallo [IoT-hubeindpunten](iot-hub-devguide.md):


* *Identiteiten Apparaatbeheer* tooprovision en beheren van apparaten die zijn geregistreerd met uw IoT-hub.
* *Apparaat-naar-cloud ontvangen* zodat u berichten van uw apparaat tooyour IoT-hub kunt bewaken.
* *Cloud naar apparaat verzenden* zodat u berichten tooyour apparaten van uw IoT-hub verzenden kunt.

Configureer uw IoT hub-verbindingsreeks binnen dit hulpprogramma toouse de mogelijkheden ervan.

### <a name="iothub-explorer"></a>iothub explorer
[iothub explorer](https://github.com/Azure/iothub-explorer) is een voorbeeld-hulpprogramma voor meerdere platforms CLI toomanage apparaten. U kunt Hallo hulpprogramma toomanage Hallo apparaten gebruiken in het identiteitenregister hello, apparaat-naar-cloud-berichten worden gecontroleerd en cloud-naar-apparaat-berichten verzenden.

tooinstall Hallo nieuwste (prerelease) versie van Hallo iothub explorer hulpprogramma, Hallo volgende opdracht in uw omgeving opdrachtregel uitvoeren:

```bash
npm install -g iothub-explorer@latest
```

U kunt Hallo opdracht tooget meer informatie over alle Hallo iothub explorer opdrachten en hun parameters te volgen:

```bash
iothub-explorer help
```

### <a name="azure-portal"></a>Azure Portal
Een volledige CLI-ervaring helpt u bij het maken en beheren van alle Azure-resources. U kunt ook toouse hello [Azure-portal](../azure-portal-overview.md) toohelp inrichten, beheren en fouten opsporen in uw Azure-resources.

## <a name="azure-storage-issues"></a>Azure Storage-problemen
[Microsoft Azure Opslagverkenner (preview)](http://storageexplorer.com) is een zelfstandige app van Microsoft die u toowork met Azure Storage-gegevens op Windows-, Mac OS- en Linux gebruiken kunt. Met dit hulpprogramma kunt kunt tooyour tabel u verbinding en Hallo-gegevens in het zien. U kunt dit hulpprogramma tootroubleshoot uw Azure Storage-problemen.

