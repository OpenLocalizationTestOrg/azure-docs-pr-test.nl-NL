---
title: aaaAzure IoT Suite verbonden factory Veelgestelde vragen | Microsoft Docs
description: Veelgestelde vragen voor verbonden IoT Suite-factory
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 4ae9beb0daf1b0578850cd652eaca7635b0d039d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite-connected-factory-preconfigured-solution"></a>Veelgestelde vragen voor verbonden factory IoT Suite vooraf geconfigureerde oplossing

Zie ook, algemene Hallo [Veelgestelde vragen over](iot-suite-faq.md) voor IoT Suite.

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solution"></a>Waar vind ik broncode Hallo voor Hallo vooraf geconfigureerde oplossing

Hallo broncode is opgeslagen in Hallo GitHub-opslagplaats te volgen:

* [Verbonden factory vooraf geconfigureerde oplossing](https://github.com/Azure/azure-iot-connected-factory)

### <a name="what-is-opc-ua"></a>Wat is OPC UA?

OPC Unified architectuur (UA), uitgebracht in 2008, is een standaard platformonafhankelijk, servicegerichte interoperabiliteit. OPC UA wordt gebruikt door verschillende industriële systemen en apparaten zoals bedrijfstak pc's, plc's en sensoren. OPC UA integreert Hallo-functionaliteit van Hallo OPC klassieke specificaties in één uitbreidbaar framework met ingebouwde beveiliging. Er is een standaard die wordt aangedreven door Hallo OPC Foundation. Hallo [OPC Foundation](http://opcfoundation.org/) is een organisatie zonder met meer dan 440 leden. Hallo-doel van de organisatie Hallo is toouse OPC specificaties toofacilitate meerdere leveranciers, meerdere platforms, veilige en betrouwbare interoperabiliteit via:

* Infrastructuur
* Specificaties
* Technologie
* Processen

### <a name="why-did-microsoft-choose-opc-ua-for-hello-connected-factory-preconfigured-solution"></a>Waarom Microsoft kiezen dat OPC UA voor Hallo verbonden factory vooraf geconfigureerde oplossing?

Microsoft heeft ervoor gekozen OPC UA omdat het een open, op niet-bedrijfseigen platform onafhankelijke bedrijfstak herkend en beproefde standaard. Het is een vereiste voor Industrie 4.0 (RAMI4.0) reference architecture oplossingen interoperabiliteit tussen een uitgebreide reeks productieprocessen en apparatuur. Microsoft ziet vraag van onze klanten toobuild Industrie 4.0-oplossingen. Ondersteuning voor OPC UA helpt lagere Hallo blokkade voor klanten tooachieve hun doelstellingen en onmiddellijk waarde toothem biedt.

### <a name="how-do-i-add-a-public-ip-address-toohello-simulation-vm"></a>Hoe kan ik een openbare IP-adres toohello-simulatie VM toevoegen

U hebt twee opties tooadd Hallo IP-adres:

* Gebruik de PowerShell-script Hallo `Simulation/Factory/Add-SimulationPublicIp.ps1` in Hallo [opslagplaats](https://github.com/Azure/azure-iot-connected-factory). Als een parameter doorgeven in de implementatienaam van uw. Gebruik voor een lokale implementatie `<your username>ConnFactoryLocal`. Hallo IP-adres van VM Hallo Hallo script wordt afgedrukt.

* Zoek in hello Azure-portal, de resourcegroep Hallo van uw implementatie. Met uitzondering van een lokale implementatie is Hallo-resourcegroep Hallo-naam die u hebt opgegeven als oplossing of de implementatienaam van de. Voor een lokale implementatie met behulp van Hallo build script, Hallo-naam van de resourcegroep Hallo is `<your username>ConnFactoryLocal`. Voeg nu een nieuwe **openbaar IP-adres** resource toohello resourcegroep.

> [!NOTE]
> Zorg ervoor dat u de meest recente patches Hallo installeren door Hallo instructies te volgen op Hallo in beide gevallen [Ubuntu website](https://wiki.ubuntu.com/Security/Upgrades). Hallo-installatie van toodate voor behouden zolang uw VM toegankelijk via een openbaar IP-adres is.

### <a name="how-do-i-remove-hello-public-ip-address-toohello-simulation-vm"></a>Hoe verwijder ik Hallo openbare IP-adres toohello simulatie VM

U hebt twee opties tooremove Hallo IP-adres:

* Gebruik PowerShell-script Hallo Simulation/Factory/Remove-SimulationPublicIp.ps1 Hallo [opslagplaats](https://github.com/Azure/azure-iot-connected-factory). Als een parameter doorgeven in de implementatienaam van uw. Gebruik voor een lokale implementatie `<your username>ConnFactoryLocal`. Hallo IP-adres van VM Hallo Hallo script wordt afgedrukt.

* Zoek in hello Azure-portal, de resourcegroep Hallo van uw implementatie. Met uitzondering van een lokale implementatie is Hallo-resourcegroep Hallo-naam die u hebt opgegeven als oplossing of de implementatienaam van de. Voor een lokale implementatie met behulp van Hallo build script, Hallo-naam van de resourcegroep Hallo is `<your username>ConnFactoryLocal`. Nu verwijderen Hallo **openbaar IP-adres** resource uit de resourcegroep Hallo.

### <a name="how-do-i-sign-in-toohello-simulation-vm"></a>Hoe meld ik in toohello simulatie VM?

Aanmelden toohello simulatie VM wordt alleen ondersteund als u uw oplossing met behulp van PowerShell-script Hallo hebt geïmplementeerd `build.ps1` in Hallo [opslagplaats](https://github.com/Azure/azure-iot-connected-factory).

Als u de oplossing Hallo van www.azureiotsuite.com hebt geïmplementeerd, kunt u toohello VM kan niet aanmelden. Je aanmelden niet, omdat Hallo wachtwoord willekeurig gegenereerd en kunt u deze niet herstellen.

1. Voeg een openbaar IP-adres toohello VM. Zie [hoe voeg ik een openbare IP-adres toohello-simulatie VM?](#how-do-i-remove-the-public-ip-address-to-the-simulation-vm)
1. Maken van een SSH-sessie tooyour VM Hallo IP-adres van Hallo VM.
1. Hallo gebruikersnaam toouse is: `docker`.
1. Hallo wachtwoord toouse, is afhankelijk van Hallo-versie die u toodeploy gebruikt:
    * Voor oplossingen die zijn geïmplementeerd met behulp van Hallo build.ps1 script vóór 1 juni 2017, is het Hallo-wachtwoord: `Passw0rd`.
    * Voor oplossingen die zijn geïmplementeerd met behulp van Hallo build.ps1 script na 1 juni 2017, vindt u Hallo wachtwoord in Hallo `<name of your deployment>.config.user` bestand. Hallo-wachtwoord wordt opgeslagen in Hallo **VmAdminPassword** instelling. Hallo wachtwoord willekeurig gegenereerd tijdens de implementatie tenzij u opgeeft met behulp van Hallo `build.ps1` parameter script`-VmAdminPassword`

### <a name="how-do-i-stop-and-start-all-docker-processes-in-hello-simulation-vm"></a>Hoe ik stoppen en starten van alle docker-processen in Hallo simulatie VM?

1. Meld u aan toohello simulatie VM. Zie [hoe meld ik me toohello simulatie VM?](#how-do-i-sign-in-to-the-simulation-vm)
1. welke containers zijn actief, toocheck uitvoeren: `docker ps`.
1. toostop alle simulatie containers uitvoeren: `./stopsimulation`.
1. toostart alle simulatie containers:
    * Exporteren van een shell-variabele met de naam van de Hallo **IOTHUB_CONNECTIONSTRING**. Gebruik Hallo-waarde van Hallo **IotHubOwnerConnectionString** instellen in Hallo `<name of your deployment>.config.user` bestand. Bijvoorbeeld:

        ```
        export IOTHUB_CONNECTIONSTRING="HostName={yourdeployment}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={your key}"
        ```

    * Voer `./startsimulation` uit.

### <a name="how-do-i-update-hello-simulation-in-hello-vm"></a>Hoe kan ik de simulatie Hallo in Hallo VM bijwerken?

Als u wijzigingen toohello simulatie aangebracht hebt, kunt u de PowerShell-script Hallo `build.ps1` in Hallo [opslagplaats](https://github.com/Azure/azure-iot-connected-factory) met Hallo `updatedimulation` opdracht. Dit script alle Hallo simulatie onderdelen bouwt, stopt de simulatie Hallo in Hallo VM, uploadt, installeert en start deze.

### <a name="how-do-i-find-out-hello-connection-string-of-hello-iot-hub-used-by-my-solution"></a>Hoe vind ik Hallo verbindingsreeks van Hallo IoT-hub die wordt gebruikt door Mijn-oplossing?

Als u uw oplossing Hello geïmplementeerd `build.ps1` script in Hallo [opslagplaats](https://github.com/Azure/azure-iot-connected-factory), Hallo-verbindingsreeks is Hallo-waarde van **IotHubOwnerConnectionString** in Hallo `<name of your deployment>.config.user` bestand.

U vindt ook Hallo verbindingsreeks met hello Azure-portal. Zoek in Hallo IoT Hub-resource in de resourcegroep Hallo van uw implementatie, Hallo verbindingstekenreeksinstellingen.

### <a name="which-iot-hub-devices-does-hello-connected-factory-simulation-use"></a>Welke apparaten IoT Hub verbonden factory simulatie gebruik Hallo?

Hallo simulatie zichzelf registreert Hallo volgende apparaten:

* proxy.Beijing.corp.contoso
* proxy.capetown.corp.contoso
* proxy.Mumbai.corp.contoso
* proxy.munich0.corp.contoso
* proxy.Rio.corp.contoso
* proxy.Seattle.corp.contoso
* Publisher.Beijing.corp.contoso
* Publisher.capetown.corp.contoso
* Publisher.Mumbai.corp.contoso
* Publisher.munich0.corp.contoso
* Publisher.Rio.corp.contoso
* Publisher.Seattle.corp.contoso

Met behulp van Hallo [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) of [iothub explorer](https://github.com/azure/iothub-explorer) hulpprogramma, u kunt controleren welke apparaten zijn geregistreerd met uw oplossing gebruikmaakt van Hallo iothub. toouse deze hulpprogramma's, moet u de verbindingsreeks Hallo in uw implementatie voor Hallo IoT-hub.

### <a name="how-can-i-get-log-data-from-hello-simulation-components"></a>Hoe krijg ik logboekgegevens uit Hallo simulatie onderdelen

Alle onderdelen in de simulatie Hallo logboekgegevens in toolog bestanden. Deze bestanden vindt u in Hallo VM in de map Hallo `home/docker/Logs`. tooretrieve hello zich aanmeldt, kunt u de PowerShell-script Hallo `Simulation/Factory/Get-SimulationLogs.ps1` in Hallo [opslagplaats](https://github.com/Azure/azure-iot-connected-factory).

Dit script moet toosign in toohello VM. Mogelijk moet u referenties tooprovide voor Hallo aanmelden. Zie [hoe meld ik me toohello simulatie VM?](#how-do-i-sign-in-to-the-simulation-vm) toofind Hallo referenties.

Hallo script toevoegen of eruit verwijderen een openbare IP-adres toohello VM, als deze nog niet over een en wordt deze verwijderd. Hallo script plaatst alle logboekbestanden in een archief en downloadt Hallo archief tooyour ontwikkelwerkstation.

U kunt ook toohello VM via SSH aanmelden en controleren van logboekbestanden Hallo tijdens runtime.

### <a name="how-can-i-check-if-hello-simulation-is-sending-data-toohello-cloud"></a>Hoe kan ik controleren als Hallo simulatie van gegevens toohello cloud verzenden?

Hello [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) of Hallo [iothub explorer](https://github.com/azure/iothub-explorer) hulpprogramma, kunt u Hallo gegevens verzonden tooIoT Hub van bepaalde apparaten controleren. toouse deze hulpprogramma's, moet u tooknow Hallo-verbindingsreeks in uw implementatie voor Hallo IoT-hub. Zie [hoe vind ik uit de verbindingsreeks Hallo van Hallo IoT-hub die wordt gebruikt door Mijn oplossing?](#how-do-i-find-out-the-connection-string-of-the-iot-hub-used-by-my-solution)

Hallo gegevens die worden verzonden door een van de Hallo publisher apparaten controleren:

* Publisher.Beijing.corp.contoso
* Publisher.capetown.corp.contoso
* Publisher.Mumbai.corp.contoso
* Publisher.munich0.corp.contoso
* Publisher.Rio.corp.contoso
* Publisher.Seattle.corp.contoso

Als er geen gegevens verzonden tooIoT Hub, klik is er een probleem met de Hallo simulatie. Als een eerste stap van de analyse moet u de logboekbestanden Hallo Hallo simulatie onderdelen analyseren. Zie [hoe krijg ik logboekgegevens van Hallo simulatie onderdelen?](#how-can-i-get-log-data-from-the-simulation-components) Vervolgens probeert toostop en Hallo simulatie starten en als er nog geen gegevens die worden verzonden, werkt u Hallo simulatie volledig. Zie [hoe bijwerken Hallo simulatie in Hallo VM?](#how-do-i-update-the-simulation-in-the-vm)

### <a name="next-steps"></a>Volgende stappen

U kunt ook verkennen van Hallo andere functies en mogelijkheden van Hallo vooraf geconfigureerde IoT Suite-oplossingen:

* [Overzicht van voorspeld onderhoud vooraf geconfigureerde oplossing](iot-suite-predictive-overview.md)
* [Overzicht van de verbonden factory vooraf geconfigureerde oplossing](iot-suite-connected-factory-overview.md)
* [Beveiliging van de IoT van Hallo gemalen](securing-iot-ground-up.md)
