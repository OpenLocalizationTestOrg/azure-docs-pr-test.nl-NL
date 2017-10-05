---
title: 'Intel Edison (knooppunt) verbinden met Azure IoT - les 4: probleemoplossing | Microsoft Docs'
description: Pagina voor probleemoplossing voor Intel Edison Node.js-ervaring
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino probleemoplossing
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: f11c5521-8a36-44c0-baad-f5ec26ab4618
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d54dd4a13ed87152fb6c039f38a5ffe8b4470df9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a>Problemen oplossen
## <a name="hardware-issues"></a>Hardwareproblemen
Zie voor meer informatie over het oplossen van veelvoorkomende problemen op Intel Edison de [officiële pagina voor probleemoplossing](https://software.intel.com/en-us/node/637974).

## <a name="nodejs-package-issues"></a>Problemen met node.js-pakket
### <a name="no-response-during-gulp-tasks"></a>Geen reactie tijdens gulp taken
Als u met taken gulp problemen, kunt u toevoegen de `--verbose` optie voor foutopsporing. Probeer het huidige gulp taken beëindigd met behulp van `Ctrl + C`, en voer de volgende in het consolevenster opdracht om te zien foutopsporingsberichten. Gedetailleerde foutberichten ziet u in de console-uitvoer. 

```bash
gulp --verbose
```

### <a name="npm-issues"></a>NPM problemen
Voer de NPM-pakket bijwerken met de volgende opdracht:

```bash
npm install -g npm
```

Als het probleem blijft optreden, laat u hierop een toelichting aan het einde van dit artikel of maak een GitHub-probleem in onze [voorbeeld opslagplaats][sample-repository].

## <a name="remote-debugging"></a>Foutopsporing op afstand

### <a name="run-the-sample-application-in-debug-mode"></a>De voorbeeldtoepassing in de foutopsporingsmodus uitvoeren

```bash
gulp run --debug
```

Zodra de engine voor foutopsporing gereed is, moet u kunnen zien ```Debugger listening on port 5858``` van de console-uitvoer.

### <a name="configure-vs-code-to-connect-to-the-remote-device"></a>VS-Code voor het verbinding maken met het externe apparaat configureren

Open de **Debug** Configuratiescherm vanaf de linkerkant.

Klik op de groene **foutopsporing starten** knop (F5). VS Code opent een **launch.json** bestand, dat u wilt bijwerken.

Update de **launch.json** bestand met de volgende inhoud, Vervang `[device hostname or IP address]` met het daadwerkelijk apparaat IP-adres of de hostnaam.  

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

![Configuratie van extern foutopsporing](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-to-the-remote-application"></a>Koppelen aan de externe toepassing

Klik op de groene **foutopsporing starten** (F5) knop en profiteer van foutopsporing.

U kunt lezen [JavaScript in VS-Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) voor meer informatie over het foutopsporingsprogramma.

![Externe interactieve foutopsporing](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Azure CLI-problemen
De Azure-opdrachtregelinterface (Azure CLI) is een preview-versie. Zoek naar de oplossing in de [Preview installeren handleiding](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) te zoeken naar oplossingen. Probeer Azure cli naar de nieuwste versie om bij te werken opdrachten werken niet zoals verwacht.

Als u met het hulpprogramma fouten optreden, het bestand een [probleem](https://github.com/Azure/azure-cli/issues) in de **problemen** sectie van de GitHub-repo.

Voor hulp bij het oplossen van veelvoorkomende problemen, Controleer de [Leesmij](https://github.com/Azure/azure-cli/blob/master/README.rst).

Als u 'Kan een versie die voldoet aan de vereiste niet vinden' aan, voert u de volgende opdracht om te werken van pip naar de laatste versie.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Problemen met de installatie van Python
### <a name="legacy-installation-issues-macos"></a>Verouderde installatieproblemen (Mac OS)
Wanneer u installeert **pip**, een machtigingsfout wordt gegenereerd wanneer de oudere pakketten die zijn geïnstalleerd met **su** machtigingen. Deze situatie doet zich voor omdat een eerdere installatie van Python met brew (Mac OS) is niet volledig verwijderd. Sommige **pip** pakketten van een eerdere installatie zijn gemaakt door root, waardoor de machtiging fout optreedt. De oplossing is om te verwijderen die pakketten geïnstalleerd door de hoofdmap. Gebruik de volgende stappen uit om deze taak te voltooien:

1. Ga naar: /usr/local/lib/python2.7/site-packages
2. Lijst met pakketten maken door hoofdmap:`ls -l | grep root`
3. Verwijderen van pakketten uit stap 2:`sudo rm -rf {package name}`
4. Installeer Python.

## <a name="azure-iot-hub-issues"></a>Problemen met Azure IoT Hub
Als u uw Azure IoT hub met succes hebt ingericht `azure-cli`, en moet u een hulpprogramma voor het beheren van de apparaten die zijn verbonden met uw IoT-hub, probeert u de volgende hulpprogramma's:

### <a name="device-explorer"></a>Apparaat Explorer
[Apparaat Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) wordt uitgevoerd op uw lokale Windows-computer en verbinding maakt met uw IoT-hub in Azure. Er wordt gecommuniceerd met de volgende [IoT-hubeindpunten](iot-hub-devguide.md):

- _Identiteiten Apparaatbeheer_ inrichten en beheren van apparaten die zijn geregistreerd met uw IoT-hub.
- _Apparaat-naar-cloud ontvangen_ zodat u berichten van uw apparaat voor uw IoT-hub kunt bewaken.
- _Cloud naar apparaat verzenden_ zodat u berichten naar uw apparaten van uw IoT-hub verzenden kunt.

Configureer uw `IoT hub connection string` vanuit dit hulpprogramma te gebruiken van de mogelijkheden ervan.

### <a name="iot-hub-explorer"></a>IoT-hub Explorer
[IoT-hub Explorer](https://github.com/Azure/iothub-explorer) is een voorbeeld meerdere platforms CLI-hulpprogramma om apparaatclients te beheren. Het hulpprogramma kunt u de apparaten in het identiteitenregister beheren, apparaat-naar-cloud-berichten worden gecontroleerd en cloud-naar-apparaatopdrachten verzenden.

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

## <a name="azure-storage-issues"></a>Problemen met de Azure-opslag
[Microsoft Azure Opslagverkenner (preview)](http://storageexplorer.com) is een zelfstandige app van Microsoft die u gebruiken kunt voor het werken met [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) gegevens op Windows-, Mac OS- en Linux. Met dit hulpprogramma kunt u verbinding maken met uw tabel en de gegevens weergegeven in het. U kunt dit hulpprogramma om problemen met uw Azure Storage te gebruiken.

## <a name="next-steps"></a>Volgende stappen
Deze pagina bevat alleen de meest voorkomende problemen van Intel Edison kit. U kunt ook de opmerkingen onder laten problemen rapporteren voor meer informatie over.

Ga terug naar [aan de slag met Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started