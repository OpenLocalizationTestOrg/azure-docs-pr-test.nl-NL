---
title: Connect Intel Edison (C) tooAzure IoT - probleemoplossing | Microsoft Docs
description: Pagina voor probleemoplossing voor Intel Edison C-ervaring
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino probleemoplossing
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: fe20f2fe-490c-4910-82e1-578ed504ae86
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c4a71983e3906cfc5ce7c832cf858852b9bd744a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Problemen oplossen
## <a name="hardware-issues"></a>Hardwareproblemen
Zie voor informatie over het oplossen van veelvoorkomende problemen op Intel Edison hello [officiële pagina voor probleemoplossing](https://software.intel.com/en-us/node/637974).

## <a name="nodejs-package-issues"></a>Problemen met node.js-pakket
### <a name="no-response-during-gulp-tasks"></a>Geen reactie tijdens gulp taken
Als u problemen hebt met het actieve taken gulp, kunt u toevoegen Hallo `--verbose` optie voor foutopsporing. Probeer tooterminate huidige gulp taken met behulp van `Ctrl + C`, en vervolgens uitvoeren Hallo-opdracht in uw foutopsporingsberichten console venster toosee. Gedetailleerde foutberichten ziet u in de console-uitvoer. 

```bash
gulp --verbose
```

### <a name="npm-issues"></a>NPM problemen
Probeer tooupdate uw pakket NPM Hello volgende opdracht:

```bash
npm install -g npm
```

Als Hallo probleem blijft optreden, laat u hierop een toelichting op Hallo einde van dit artikel of maak een GitHub-probleem in onze [voorbeeld opslagplaats][sample-repository].

## <a name="azure-cli-issues"></a>Azure CLI-problemen
Hello Azure-opdrachtregelinterface (Azure CLI) is een preview-versie. Zoek naar de oplossing in Hallo [Preview installeren handleiding](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek oplossingen. Probeer tooupgrade Azure cli toolatest versie wanneer opdrachten niet werkt zoals verwacht.

Als u fouten met Hallo hulpprogramma tegenkomt, het bestand een [probleem](https://github.com/Azure/azure-cli/issues) in Hallo **problemen** sectie van de GitHub-repo-Hallo.

Voor hulp bij het oplossen van veelvoorkomende problemen, Controleer Hallo [Leesmij](https://github.com/Azure/azure-cli/blob/master/README.rst).

Als u aan 'Kan een versie die voldoet aan de vereiste Hallo niet vinden', neem opdracht uitvoeren Hallo volgende tooupgrade pip toolastest versie.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Problemen met de installatie van Python
### <a name="legacy-installation-issues-macos"></a>Verouderde installatieproblemen (Mac OS)
Wanneer u installeert **pip**, een machtigingsfout wordt gegenereerd wanneer de oudere pakketten die zijn geïnstalleerd met **su** machtigingen. Deze situatie doet zich voor omdat een eerdere installatie van Python met brew (Mac OS) is niet volledig verwijderd. Sommige **pip** pakketten van een eerdere installatie zijn gemaakt door root, waardoor Hallo machtigingsfout. Hallo oplossing tooremove die pakketten door basiscertificeringsinstantie geïnstalleerd is. Hallo toocomplete stappen te volgen met deze taak gebruiken:

1. Ga naar: /usr/local/lib/python2.7/site-packages
2. Lijst met pakketten maken door hoofdmap:`ls -l | grep root`
3. Verwijderen van pakketten uit stap 2:`sudo rm -rf {package name}`
4. Installeer Python.

## <a name="azure-iot-hub-issues"></a>Problemen met Azure IoT Hub
Als u uw Azure IoT hub met succes hebt ingericht `azure-cli`, en moet u een hulpprogramma toomanage Hallo-apparaten die verbinding maken tooyour iothub, probeer Hallo hulpprogramma's te volgen:

### <a name="device-explorer"></a>Apparaat Explorer
[Apparaat Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) wordt uitgevoerd op uw lokale Windows-computer en verbindt tooyour IoT-hub in Azure. Er wordt gecommuniceerd met de volgende Hallo [IoT-hubeindpunten](iot-hub-devguide.md):

- _Identiteiten Apparaatbeheer_ tooprovision en beheren van apparaten die zijn geregistreerd met uw IoT-hub.
- _Apparaat-naar-cloud ontvangen_ zodat u berichten van uw apparaat tooyour IoT-hub kunt bewaken.
- _Cloud naar apparaat verzenden_ zodat u berichten tooyour apparaten van uw IoT-hub verzenden kunt.

Configureer uw `IoT hub connection string` binnen dit hulpprogramma toouse de mogelijkheden ervan.

### <a name="iot-hub-explorer"></a>IoT-hub Explorer
[IoT-hub Explorer](https://github.com/Azure/iothub-explorer) is een voorbeeld-hulpprogramma voor meerdere platforms CLI toomanage-apparaatclients. U kunt Hallo hulpprogramma toomanage Hallo apparaten gebruiken in het identiteitenregister hello, apparaat-naar-cloud-berichten worden gecontroleerd en cloud-naar-apparaatopdrachten verzenden.

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

## <a name="azure-storage-issues"></a>Problemen met de Azure-opslag
[Microsoft Azure Opslagverkenner (preview)](http://storageexplorer.com) is een zelfstandige app van Microsoft waarmee u toowork met kunt [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) gegevens op Windows-, Mac OS- en Linux. Met dit hulpprogramma kunt kunt tooyour tabel u verbinding en Hallo-gegevens in het zien. U kunt dit hulpprogramma tootroubleshoot uw Azure Storage-problemen.

## <a name="next-steps"></a>Volgende stappen
Deze pagina bevat alleen de meest voorkomende problemen Hallo van Intel Edison kit. U kunt ook reacties onder tooreport problemen voor meer informatie over.

Ga terug te[aan de slag met Intel Edison (C)](iot-hub-intel-edison-kit-c-get-started.md)

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-c-edison-getting-started