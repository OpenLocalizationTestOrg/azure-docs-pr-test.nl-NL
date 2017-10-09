---
title: SensorTag apparaat & Azure IoT Gateway - probleemoplossing | Microsoft Docs
description: Pagina voor probleemoplossing voor Intel NUC gateway
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT-problemen, internet der dingen problemen
ROBOTS: NOINDEX
ms.assetid: 5f742c38-0e33-465a-9a0d-1e41e8d17187
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ed6812c60412afb615012e3d694051d009b149a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Problemen oplossen

## <a name="hardware-issues"></a>Hardwareproblemen

### <a name="ti-sensortag-cannot-be-connected"></a>TI SensorTag kan niet worden verbonden.

verbindingsproblemen tootroubleshoot SensorTag, gebruik Hallo [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).

### <a name="have-an-issue-with-intel-nuc"></a>Een probleem met de Intel NUC

opstartproblemen tootroubleshoot, te verwijzen[problemen met het niet opstarten op Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).

problemen met de besturingssystemen van tootroubleshoot te verwijzen[problemen met het besturingssysteem op Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).

tootroubleshoot andere problemen te verwijzen[knipperen Codes en een piepgeluid laat horen Codes voor Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).

## <a name="nodejs-package-issues"></a>Problemen met node.js-pakket

### <a name="no-response-during-gulp-tasks"></a>Geen reactie tijdens gulp taken

Als u problemen ondervindt met actieve taken gulp, kunt u toevoegen Hallo `--verbose` optie voor foutopsporing. Probeer tooterminate huidige gulp taken met behulp van `Ctrl + C`, en vervolgens uitvoeren Hallo-opdracht in uw foutopsporingsberichten console venster toosee. Gedetailleerde foutberichten ziet u in de console-uitvoer.

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>Problemen met detectie van apparaat

Voor hulp bij het oplossen van veelvoorkomende problemen met Hallo `discover-sensortag` opdracht, controleert u Hallo [wiki-pagina](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).

### <a name="npm-issues"></a>npm problemen

Probeer tooupdate de npm-pakket door het uitvoeren van de volgende opdracht Hallo:

```bash
npm install -g npm
```

Als Hallo probleem blijft optreden, laat u hierop een toelichting op Hallo einde van dit artikel of maak een GitHub-probleem in onze [voorbeeld opslagplaats](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).

## <a name="remote-debugging"></a>Foutopsporing op afstand
> Onderstaande instructies zijn bedoeld voor het opsporen van node.js-scripts die worden gebruikt in deze zelfstudie.
### <a name="run-hello-sample-application-in-debug-mode"></a>Hallo-voorbeeldtoepassing in de foutopsporingsmodus uitvoeren

Hallo-voorbeeldtoepassing in de foutopsporingsmodus uitvoeren door te voeren van Hallo volgende opdracht:

```bash
gulp run --debug
```

Wanneer foutopsporing-engine Hallo klaar is, ziet u `Debugger listening on port 5858` in Hallo console-uitvoer.

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a>Visual Studio Code tooconnect toohello externe apparaten configureren

1. Open Hallo **Debug** Configuratiescherm op Hallo linkerkant.
2. Klik op Hallo groen **foutopsporing starten** knop (F5). Hiermee opent u Visual Studio Code een `launch.json` bestand.
3. Update Hallo `launch.json` bestand met de Hallo inhoud te volgen. Vervang `[device hostname or IP address]` met Hallo werkelijke IP-adres of de hostnaam apparaatnaam.

   ``` json
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
            "remoteRoot": "~/ble_sample"
        }
     ]
   }
   ```

![Configuratie van extern foutopsporing](./media/iot-hub-gateway-kit-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>De externe toepassing toohello koppelen

Klik op Hallo groen **foutopsporing starten** (F5) knop toostart foutopsporing.

Lees [JavaScript in VS-Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn meer informatie over Hallo foutopsporing.

![Voorbeeld van foutopsporing uitschakelen](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a>Problemen met Azure CLI

Hello Azure-opdrachtregelinterface (Azure CLI) is een preview-versie. oplossingen voor tooseek, kunt u Hallo [Preview installeren handleiding](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).

Als u fouten met Hallo hulpprogramma tegenkomt, het bestand een [probleem](https://github.com/Azure/azure-cli/issues) in Hallo **problemen** sectie van de GitHub-repo-Hallo.

Controleer voor hulp bij het oplossen van veelvoorkomende problemen Hallo [Leesmij](https://github.com/Azure/azure-cli/blob/master/README.rst).

Als u aan 'Kan een versie die voldoet aan de vereiste Hallo niet vinden', neem opdracht uitvoeren Hallo volgende tooupgrade pip toolastest versie.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Problemen met de installatie van Python

### <a name="legacy-installation-issues-macos"></a>Verouderde installatieproblemen (Mac OS)

Wanneer u pip installeert, een machtigingsfout wordt gegenereerd wanneer oudere pakketten worden geïnstalleerd met **su** machtigingen. Deze situatie doet zich voor omdat een eerdere installatie van Python met brew (Mac OS) is niet volledig verwijderd. Sommige pakketten pip van een eerdere installatie zijn gemaakt door root, waardoor Hallo machtigingsfout. Hallo oplossing tooremove die pakketten door basiscertificeringsinstantie geïnstalleerd is. Hallo toocomplete stappen te volgen met deze taak gebruiken:

1. Te gaan`/usr/local/lib/python2.7/site-packages`
2. Lijst met pakketten gemaakt door hoofdmap:`ls -l | grep root`
3. Verwijderen van pakketten uit stap 2:`sudo rm -rf {package name}`
4. Installeer Python.

## <a name="azure-iot-hub-issues"></a>Problemen met Azure IoT Hub

Als u uw Azure-IoT-hub Hello Azure CLI met succes hebt ingericht en moet u een hulpprogramma toomanage Hallo-apparaten die verbinding maken tooyour iothub, probeer Hallo hulpprogramma's te volgen.

### <a name="device-explorer"></a>Apparaat Explorer

[Apparaat Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) wordt uitgevoerd op uw lokale Windows-computer en verbindt tooyour IoT-hub in Azure. Er wordt gecommuniceerd met de volgende Hallo [IoT-hubeindpunten](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):

- Apparaat identity management tooprovision en beheren van apparaten die zijn geregistreerd met uw IoT-hub.
- Apparaat-naar-cloud ontvangen u berichten van uw apparaat tooyour IoT-hub kunt bewaken.
- Cloud naar apparaat verzenden zodat u berichten tooyour apparaten van uw IoT-hub verzenden kunt.

Configureer uw IoT hub-verbindingsreeks binnen dit hulpprogramma toouse de mogelijkheden ervan.

### <a name="iothub-explorer"></a>iothub explorer

[iothub explorer](https://github.com/Azure/iothub-explorer) is een voorbeeld-hulpprogramma voor meerdere platforms CLI toomanage-apparaatclients. U kunt Hallo hulpprogramma toomanage Hallo apparaten gebruiken in het identiteitenregister hello, apparaat-naar-cloud-berichten worden gecontroleerd en cloud-naar-apparaatopdrachten verzenden.

tooinstall hello nieuwste (prerelease) versie van Hallo iothub explorer hulpprogramma, Hallo volgende opdracht uitvoeren:

```bash
npm install -g iothub-explorer@latest
```

meer informatie over alle tooget Hallo iothub explorer opdrachten en de bijbehorende parameters, Hallo volgende opdracht uitvoeren:

```bash
iothub-explorer help
```

### <a name="hello-azure-portal"></a>Hello Azure-portal

Een volledige CLI-ervaring helpt u bij het maken en beheren van alle Azure-resources. U kunt ook toouse hello [Azure-portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp inrichten, beheren en fouten opsporen in uw Azure-resources.

## <a name="azure-storage-issues"></a>Azure Storage-problemen

[Microsoft Azure Opslagverkenner (preview)](http://storageexplorer.com/) is een zelfstandige app van Microsoft die u toowork met Azure Storage-gegevens op Windows-, Mac OS- en Linux gebruiken kunt. Met dit hulpprogramma kunt kunt tooyour tabel u verbinding en Hallo-gegevens in het zien. U kunt dit hulpprogramma tootroubleshoot uw Azure Storage-problemen.
