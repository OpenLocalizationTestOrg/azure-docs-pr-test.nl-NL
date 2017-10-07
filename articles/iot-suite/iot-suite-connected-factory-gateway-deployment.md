---
title: uw Azure IoT Suite verbonden aaaDeploy factory gateway | Microsoft Docs
description: Hoe een gateway op Windows of Linux tooenable connectiviteit toohello toodeploy factory verbonden vooraf geconfigureerde oplossing.
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 72436dec60eda0de20143f362fe740b0c4412f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-gateway-on-windows-or-linux-for-hello-connected-factory-preconfigured-solution"></a>Implementeer een gateway op Windows of Linux voor Hallo verbonden factory vooraf geconfigureerde oplossing

Hallo vereist software toodeploy een gateway voor Hallo verbonden factory vooraf geconfigureerde oplossing bestaat uit twee onderdelen:

* Hallo *OPC Proxy* stelt u een verbinding tooIoT Hub. Hallo *OPC Proxy* vervolgens wachten op voor de opdracht en controle berichten van Hallo OPC-Browser die wordt uitgevoerd in de portal van de oplossing Hallo verbonden factory geïntegreerd.
* Hallo *OPC Publisher* verbindt tooexisting lokale OPC UA-servers en telemetrieberichten daarvan tooIoT Hub verzendt.

Beide onderdelen zijn open source en zijn beschikbaar als bron op GitHub, en als Docker-containers:

| GitHub | DockerHub |
| ------ | --------- |
| [OPC-uitgever][lnk-publisher-github] | [OPC-uitgever][lnk-publisher-docker] |
| [OPC-Proxy][lnk-proxy-github] | [OPC-Proxy][lnk-proxy-docker] |

Er is geen openbare IP-adres of gaten in Hallo gateway firewall zijn vereist voor beide componenten. Gebruik alleen uitgaande poorten 443 en 5671 8883 Hallo OPC-Proxy en OPC uitgever.

Hallo stappen in dit artikel ziet u hoe toodeploy een gateway met behulp van Docker van een [Windows](#windows-deployment) of [Linux](#linux-deployment). Hallo-gateway kunnen connectiviteit toohello verbonden factory vooraf geconfigureerde oplossing.

> [!NOTE]
> Hallo-gateway voor software die wordt uitgevoerd in de Docker-container Hallo [Azure IoT rand].

## <a name="windows-deployment"></a>Windows-implementatie

> [!NOTE]
> Als u een gateway-apparaat nog geen hebt, is het raadzaam om dat u een commerciële gateway koopt van een van onze partners. Bezoek Hallo [Azure IoT-apparaat catalogus] voor een lijst met gatewayapparaten die compatibel is met de Hallo factory-oplossing die is verbonden. Volg Hallo-instructies die worden geleverd met Hallo apparaat tooset up Hallo-gateway. Ook gebruiken Hallo instructies toomanually instellen op een van uw bestaande gateways te volgen.

### <a name="install-docker"></a>Docker installeren

Installeer [Docker voor Windows] op uw apparaat op basis van de Windows-gateway. Selecteer een station op uw host machine tooshare met Docker tijdens de installatie van Windows Docker. Hallo schermafbeelding ziet delen Hallo D-station op uw Windows-systeem te volgen:

![Docker installeren][img-install-docker]

Maak vervolgens een map met de naam **docker** in de hoofdmap Hallo Hallo gedeelde stations.
U kunt deze stap ook uitvoeren na de installatie van docker van Hallo **instellingen** menu.

### <a name="configure-hello-gateway"></a>Hallo-gateway configureren

1. U moet Hallo **iothubowner** verbindingsreeks van uw Azure IoT Suite verbonden factory implementatie toocomplete Hallo gateway-implementatie. In Hallo [Azure-portal], navigeer tooyour IoT-Hub in de resourcegroep Hallo gemaakt tijdens de implementatie van Hallo verbonden factory-oplossing. Klik op **gedeeld toegangsbeleid** tooaccess hello **iothubowner** verbindingsreeks:

    ![Hallo IoT Hub verbindingsreeks zoeken][img-hub-connection]

    Kopiëren Hallo **verbindingsreeks--primaire sleutel** waarde.

1. Hallo-gateway configureren voor uw IoT Hub met behulp van Hallo twee gateway modules **zodra** vanaf een opdrachtprompt met:

    `docker run -it --rm -h <ApplicationName> -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt;**  hello toogive tooyour OPC UA Publisher Hallo-indeling is **publisher.&lt; de volledig gekwalificeerde domeinnaam&gt;**. Bijvoorbeeld, als uw netwerk factory heet **myfactorynetwork.com**, Hallo **ApplicationName** waarde is **publisher.myfactorynetwork.com**.
    * **&lt;IoTHubOwnerConnectionString&gt;**  Hallo is **iothubowner** verbindingsreeks die u in de vorige stap Hallo hebt gekopieerd. Deze verbindingsreeks wordt alleen gebruikt in deze stap, u hoeft deze niet in Hallo stappen te volgen:

    U gebruikt Hallo toegewezen D:\\docker-map (Hallo `-v` argument) hoger toopersist Hallo twee X.509-certificaten die Hallo gateway-modules gebruiken.

### <a name="run-hello-gateway"></a>Hallo-gateway uitvoeren

1. Opnieuw opstarten met behulp van de volgende opdrachten Hallo Hallo-gateway:

    `docker run -it --rm -h <ApplicationName> --expose 62222 -p 62222:62222 -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/shared -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. Uit veiligheidsoverwegingen Hallo twee X.509-certificaten die zijn doorgevoerd in Hallo D:\\docker-map Hallo persoonlijke sleutel bevat. Toegangsreferenties toothis map toohello beperken (meestal **beheerders**) u toorun hello Docker-container gebruiken. Klik met de rechtermuisknop Hallo D:\\docker-map, kies **eigenschappen**, klikt u vervolgens **beveiliging**, en vervolgens **bewerken**. Geef **beheerders** volledige controle en verwijder alle andere gebruikers:

    ![Ken machtigingen tooDocker share][img-docker-share]

1. Controleer de netwerkverbinding. Voer vanaf een opdrachtprompt Hallo opdracht `ping publisher.<your fully qualified domain name>` tooping uw gateway. Als Hallo bestemming niet bereikbaar is, toevoegen Hallo IP-adres en de naam van uw gateway toohello hosts-bestand op uw gateway. Hallo hosts-bestand bevindt zich in Hallo **Windows\\System32\\stuurprogramma's\\enzovoort** map.

1. Probeer vervolgens tooconnect toohello publisher met behulp van een lokale OPC UA-client uitgevoerd op Hallo-gateway. Hallo OPC UA-eindpunt-URL is `opc.tcp://publisher.<your fully qualified domain name>:62222`. Als u een client OPC UA geen hebt, kunt u downloaden en gebruiken een [open source OPC UA client].

1. Wanneer u deze lokale tests hebt voltooid, bladeren toohello **verbinding maken met uw eigen OPC UA-Server** pagina in de portal van de oplossing Hallo verbonden factory. Voer Hallo publisher eindpunt-URL (`tcp://publisher.<your fully qualified domain name>:62222`) en klik op **Connect**. Ophalen van een certificaatwaarschuwing weergegeven en klik op **doorgaan.** Vervolgens krijgt u een fout die Hallo publisher Hallo UA webclient niet vertrouwt. tooresolve deze fout, kopie Hallo **UA webclient** certificaat van Hallo **D:\\docker\\afgewezen certificaten\\certificaten** map toohello **D:\\docker\\UA toepassingen\\certificaten** map op het Hallo-gateway. U hoeft niet toorestart van Hallo-gateway. Herhaal deze stap. U kunt nu toohello gateway verbinding vanuit de cloud Hallo en u bent klaar tooadd OPC UA servers toohello oplossing.

### <a name="add-your-opc-ua-servers"></a>Uw OPC UA-servers toevoegen

1. Blader toohello **verbinding maken met uw eigen OPC UA-Server** pagina in de portal van de oplossing Hallo verbonden factory. Volg dezelfde stappen als in de voorgaande sectie tooestablish Hallo Hallo verbonden factory-portal en Hallo OPC UA-server vertrouwen tussen Hallo. Deze stap wordt een wederzijdse vertrouwensrelatie van certificaten van Hallo Hallo verbonden factory-portal en Hallo OPC UA-server en maakt een verbinding tot stand gebracht.

1. Blader Hallo OPC UA knooppunten structuur van uw OPC UA-server, met de rechtermuisknop op Hallo OPC knooppunten en selecteer **publiceren**. Voor publicatie toowork op deze manier Hallo OPC UA-server en Hallo publisher moet op Hallo hetzelfde netwerk. Met andere woorden, als Hallo volledig gekwalificeerde domeinnaam van Hallo publisher is **publisher.mydomain.com** en vervolgens de volledig gekwalificeerde domeinnaam Hallo Hallo OPC UA-server, bijvoorbeeld zijn moet **myopcuaserver.mydomain.com**. Als de installatie anders is, kunt u handmatig knooppunten toohello publishesnodes.json bestand gevonden in Hallo toevoegen **D:\\docker** map. Hallo publishesnodes.json-bestand is automatisch gegenereerd op Hallo eerst geslaagde publiceren van een OPC-knooppunt.

1. Telemetrie loopt nu van Hallo gateway-apparaat. U kunt Hallo telemetrie weergeven in Hallo **Factory locaties** weergave van Hallo verbonden factory portal onder **New Factory**.

## <a name="linux-deployment"></a>Linux-implementatie

> [!NOTE]
> Als u een gateway-apparaat nog geen hebt, is het raadzaam om dat u een commerciële gateway koopt van een van onze partners. Bezoek Hallo [Azure IoT-apparaat catalogus] voor een lijst met gatewayapparaten die compatibel is met de Hallo factory-oplossing die is verbonden. Volg Hallo-instructies die worden geleverd met Hallo apparaat tooset up Hallo-gateway. Ook gebruiken Hallo instructies toomanually instellen op een van uw bestaande gateways te volgen.

[Installeren van Docker] op uw Linux-gatewayapparaat.

### <a name="configure-hello-gateway"></a>Hallo-gateway configureren

1. U moet Hallo **iothubowner** verbindingsreeks van uw Azure IoT Suite verbonden factory implementatie toocomplete Hallo gateway-implementatie. In Hallo [Azure-portal], navigeer tooyour IoT-Hub in de resourcegroep Hallo gemaakt tijdens de implementatie van Hallo verbonden factory-oplossing. Klik op **gedeeld toegangsbeleid** tooaccess hello **iothubowner** verbindingsreeks:

    ![Hallo IoT Hub verbindingsreeks zoeken][img-hub-connection]

    Kopiëren Hallo **verbindingsreeks--primaire sleutel** waarde.

1. Hallo-gateway configureren voor uw IoT Hub met behulp van Hallo twee gateway modules **zodra** van een shell met:

    `sudo docker run -it --rm -h <ApplicationName> -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/ -v /shared:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `sudo docker run --rm -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt;**  Hallo naam is van Hallo OPC UA Hallo toepassingsgateway in Hallo indeling maakt **publisher.&lt; de volledig gekwalificeerde domeinnaam&gt;**. Bijvoorbeeld: **publisher.microsoft.com**.
    * **&lt;IoTHubOwnerConnectionString&gt;**  Hallo is **iothubowner** verbindingsreeks die u in de vorige stap Hallo hebt gekopieerd. Deze verbindingsreeks wordt alleen gebruikt in deze stap, u hoeft deze niet in Hallo stappen te volgen:

    Gebruik van Hallo **/ gedeelde** map (Hallo `-v` argument) hoger toopersist Hallo twee X.509-certificaten die Hallo gateway-modules gebruiken.

### <a name="run-hello-gateway"></a>Hallo-gateway uitvoeren

1. Opnieuw opstarten met behulp van de volgende opdrachten Hallo Hallo-gateway:

    `sudo docker run -it -h <ApplicationName> --expose 62222 -p 62222:62222 –-rm -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v /shared:/shared -v /shared:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `sudo docker run -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. Uit veiligheidsoverwegingen Hallo twee X.509-certificaten die zijn doorgevoerd in Hallo **/ gedeelde** map Hallo persoonlijke sleutel bevat. Limiet toothis map toohello toegangsreferenties u toorun Hallo Docker-container. tooset hello machtigingen voor **hoofdmap** alleen gebruiken Hallo `chmod` opdracht in de map Hallo-shell.

1. Controleer de netwerkverbinding. Voer vanuit een shell Hallo opdracht `ping publisher.<your fully qualified domain name>` tooping uw gateway. Als Hallo bestemming niet bereikbaar is, toevoegen Hallo IP-adres en de naam van uw gateway tooyour hosts-bestand op uw gateway. Hallo hosts-bestand bevindt zich in Hallo **/enzovoort** map.

1. Probeer vervolgens tooconnect toohello publisher met behulp van een lokale OPC UA-client uitgevoerd op Hallo-gateway. Hallo OPC UA-eindpunt-URL is `opc.tcp://publisher.<your fully qualified domain name>:62222`. Als u een client OPC UA geen hebt, kunt u downloaden en gebruiken een [open source OPC UA client].

1. Wanneer u deze lokale tests hebt voltooid, bladeren toohello **verbinding maken met uw eigen OPC UA-Server** pagina in de portal van de oplossing Hallo verbonden factory. Voer Hallo publisher eindpunt-URL (`tcp://publisher.<your fully qualified domain name>:62222`) en klik op **Connect**. Ophalen van een certificaatwaarschuwing weergegeven en klik op **doorgaan.** Vervolgens krijgt u een fout die Hallo publisher Hallo UA webclient niet vertrouwt. tooresolve deze fout, kopie Hallo **UA webclient** certificaat van Hallo **/gedeeld/geweigerd certificaten/certificaten** map toohello **/shared/UA-toepassingen/certificaten** de map op Hallo-gateway. U hoeft niet toorestart van Hallo-gateway. Herhaal deze stap. U kunt nu toohello gateway verbinding vanuit de cloud Hallo en u bent klaar tooadd OPC UA servers toohello oplossing.

### <a name="add-your-opc-ua-servers"></a>Uw OPC UA-servers toevoegen

1. Blader toohello **verbinding maken met uw eigen OPC UA-Server** pagina in de portal van de oplossing Hallo verbonden factory. Volg dezelfde stappen als in de voorgaande sectie tooestablish Hallo Hallo verbonden factory-portal en Hallo OPC UA-server vertrouwen tussen Hallo. Deze stap wordt een wederzijdse vertrouwensrelatie van certificaten van Hallo Hallo verbonden factory-portal en Hallo OPC UA-server en maakt een verbinding tot stand gebracht.

1. Blader Hallo OPC UA knooppunten structuur van uw OPC UA-server, met de rechtermuisknop op Hallo OPC knooppunten en selecteer **publiceren**. Voor publicatie toowork op deze manier Hallo OPC UA-server en Hallo publisher moet op Hallo hetzelfde netwerk. Met andere woorden, als Hallo volledig gekwalificeerde domeinnaam van Hallo publisher is **publisher.mydomain.com** en vervolgens de volledig gekwalificeerde domeinnaam Hallo Hallo OPC UA-server, bijvoorbeeld zijn moet **myopcuaserver.mydomain.com**. Als de installatie anders is, kunt u handmatig knooppunten toohello publishesnodes.json bestand gevonden in Hallo toevoegen **/ gedeelde** map. Hallo publishesnodes.json wordt automatisch gegenereerd op Hallo eerst geslaagde publiceren van een OPC-knooppunt.

1. Telemetrie loopt nu van Hallo gateway-apparaat. U kunt Hallo telemetrie weergeven in Hallo **Factory locaties** weergave van Hallo verbonden factory portal onder **New Factory**.

## <a name="next-steps"></a>Volgende stappen

vooraf geconfigureerde oplossing voor toolearn meer informatie over het Hallo-architectuur van verbonden factory hello, Zie [verbonden factory oplossing walkthrough over vooraf geconfigureerde][lnk-walkthrough].

[img-install-docker]: ./media/iot-suite-connected-factory-gateway-deployment/image1.png
[img-hub-connection]: ./media/iot-suite-connected-factory-gateway-deployment/image2.png
[img-docker-share]: ./media/iot-suite-connected-factory-gateway-deployment/image3.png

[Docker voor Windows]: https://www.docker.com/docker-windows
[Azure IoT-apparaat catalogus]: https://catalog.azureiotsuite.com/?q=opc
[Azure-portal]: http://portal.azure.com/
[open source OPC UA client]: https://github.com/OPCFoundation/UA-.NETStandardLibrary/tree/master/SampleApplications/Samples/Client.Net4
[Installeren van Docker]: https://www.docker.com/community-edition#/download
[lnk-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[Azure IoT rand]: https://github.com/Azure/iot-edge

[lnk-publisher-github]: https://github.com/Azure/iot-edge-opc-publisher
[lnk-publisher-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua
[lnk-proxy-github]: https://github.com/Azure/iot-edge-opc-proxy
[lnk-proxy-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua-proxy