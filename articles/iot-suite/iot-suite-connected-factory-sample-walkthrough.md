---
title: aaaConnected factory Azure IoT Suite-oplossing overzicht | Microsoft Docs
description: Een beschrijving van de vooraf geconfigureerde Azure IoT-oplossing Hallo verbonden factory en de bijbehorende architectuur.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 7fd55c51351659401349cfde91a20fce1045b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a>Walkthrough voor de vooraf geconfigureerde oplossing Connected Factory

Hallo IoT Suite verbonden factory [vooraf geconfigureerde oplossing] [ lnk-preconfigured-solutions] is een implementatie van een industriële end-to-end-oplossing die:

* Gesimuleerde tooboth industriële apparaten uitvoeren OPC UA-servers in de regels die gesimuleerde factory productie en apparaten met echte OPC UA-server verbonden. Zie voor meer informatie over OPC UA Hallo [verbonden factory Veelgestelde vragen over](iot-suite-faq-cf.md).
* Operationele KPI's en OEE van die apparaten en productielijnen kunnen worden bekeken.
* Laat zien hoe een cloud-gebaseerde toepassing gebruikte toointeract met systemen van OPC UA-server kan worden.
* Hiermee kunt u tooconnect de apparaten van uw eigen OPC UA-server.
* Hiermee kunt u toobrowse en Hallo OPC UA-server-gegevens wijzigen.
* Integreert met hello Azure Time Series Insights (TSI) service tooprovide aangepaste weergaven van gegevens van uw servers OPC UA Hallo.

U kunt Hallo oplossing gebruiken als een beginpunt voor uw eigen implementatie en [aanpassen] [ lnk-customize] het toomeet uw eigen specifieke zakelijke vereisten.

In dit artikel worden enkele van de belangrijkste elementen van de Hallo van Hallo verbonden factory oplossing tooenable toounderstand u hoe het werkt. Deze kennis helpt u bij:

* Los problemen met het Hallo-oplossing.
* Plannen hoe toocustomize toohello oplossing toomeet uw eigen specifieke vereisten.
* Het ontwerpen van uw eigen IoT-oplossing die gebruikmaakt van Azure-services.

Zie voor meer informatie, Hallo [verbonden factory Veelgestelde vragen over](iot-suite-faq-cf.md).

## <a name="logical-architecture"></a>Logische architectuur

Hallo volgende diagram geeft een overzicht van de logische onderdelen van de Hallo van Hallo vooraf geconfigureerde oplossing:

![Logische architectuur van Connected Factory][connected-factory-logical]

## <a name="communication-patterns"></a>Communicatiepatronen

Hallo-oplossing maakt gebruik van Hallo [OPC UA Pub subitems specificatie](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend OPC UA telemetrie gegevens tooIoT Hub in JSON-indeling. Hallo-oplossing maakt gebruik van Hallo [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge-module voor dit doel.

Hallo-oplossing heeft ook een OPC UA-client die is geïntegreerd in een webtoepassing die u kunt verbinding maken met on-premises OPC UA-servers. Hallo-client gebruikt een [reverse proxy](https://wikipedia.org/wiki/Reverse_proxy) en ontvangt van de help van IoT Hub toomake Hallo verbinding zonder geopende poorten in Hallo lokale firewall. Dit communicatiepatroon heet [door service ondersteunde communicatie](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/). Hallo-oplossing maakt gebruik van Hallo [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge-module voor dit doel.


## <a name="simulation"></a>Simulatie

Hallo gesimuleerde stations en productie-uitvoering Hallo gesimuleerde systemen (MES) van een fabriek productie-regel maken. Hallo gesimuleerde apparaten en Hallo OPC Publisher Module zijn gebaseerd op Hallo [OPC UA .NET Standard] [ lnk-OPC-UA-NET-Standard] gepubliceerd door Hallo OPC Foundation.

Hallo OPC-Proxy en OPC-Publisher zijn geïmplementeerd als modules op basis van [Azure IoT rand][lnk-Azure-IoT-Gateway]. Elke gesimuleerde productielijn heeft een eigen gekoppelde gateway.

Alle simulatie-onderdelen worden uitgevoerd in Docker-containers die worden gehost in een Azure Linux VM. Hallo simulatie is geconfigureerde toorun acht gesimuleerde productieregels standaard.

## <a name="simulated-production-line"></a>Gesimuleerde productielijn

In een productielijn worden onderdelen geproduceerd. Deze bestaat uit verschillende stations: een montagestation, een teststation en een verpakkingsstation.

Hallo simulatie wordt uitgevoerd en Hallo gegevens bijgewerkt die beschikbaar is via het Hallo OPC UA knooppunten. Alle gesimuleerde productie regel stations zijn gedirigeerd door Hallo MES via OPC UA.

## <a name="simulated-manufacturing-execution-system"></a>Gesimuleerd systeem voor de productie-uitvoering

Hallo MES bewaakt elk station op Hallo productie regel via OPC UA toodetect station statuswijzigingen. Het OPC UA methoden toocontrol Hallo stations aangeroepen en wordt vervolgens een product is geslaagd vanuit één station toohello totdat deze voltooid is.

## <a name="gateway-opc-publisher-module"></a>Gateway OPC Publisher Module

OPC Publisher Module verbindt toohello station OPC UA-servers en toohello OPC knooppunten toobe gepubliceerd op is geabonneerd. Hallo module Hallo-knooppuntgegevens converteert naar JSON-indeling, versleutelt en tooIoT Hub als OPC UA Pub subitems berichten verzendt.

Hallo OPC Publisher module alleen een uitgaande https-poort (443) vereist en kunt samenwerken met bestaande bedrijfsinfrastructuur.

## <a name="gateway-opc-proxy-module"></a>Gateway OPC Proxy Module

Hallo Gateway OPC UA Proxy Module tunnels binaire OPC UA-opdracht en controle berichten en vereist alleen een uitgaande https-poort (443). De module kan gebruikmaken van de bestaande bedrijfsinfrastructuur, zoals Web Proxies.

Deze IoT hubapparaat methoden tootransfer packetized TCP/IP-gegevens worden gebruikt op de toepassingslaag Hallo en dus garandeert eindpunt vertrouwen, gegevensversleuteling en integriteit met behulp van SSL/TLS.

Hallo OPC UA binaire protocol doorgegeven via Hallo-proxyserver van zichzelf maakt gebruik van UA-verificatie en versleuteling.

## <a name="azure-time-series-insights"></a>Azure Time Series Insights

Hallo Gateway OPC Publisher Module tooOPC UA-server knooppunten toodetect wijziging in de gegevenswaarden Hallo is geabonneerd. Als een gegevenswijziging in de in een van de knooppunten hello wordt gedetecteerd, wordt met deze module vervolgens berichten tooAzure IoT Hub verzendt.

IoT Hub biedt een gebeurtenis bron tooAzure TSI. TSI slaat gegevens voor 30 dagen op basis van tijdstempels gekoppeld toohello berichten. Deze gegevens omvatten:

* OPC UA ApplicationUri
* OPC UA NodeId
* Waarde van Hallo-knooppunt
* Tijdstempel van de bron
* OPC UA DisplayName

Op dit moment TSI staat niet toe dat klanten toocustomize hoe lang ze tookeep Hallo gegevens voor wenst.

TSI voert query's uit voor de knooppuntgegevens op basis van een SearchSpan (Time.From, Time.To) en sorteert ze op basis van OPC UA ApplicationUri, OPC UA NodeId of OPC UA DisplayName.

tooretrieve hello gegevens voor Hallo OEE en KPI meters en Hallo-tijdgrafieken reeks gegevens worden samengevoegd door het aantal gebeurtenissen, som, Gem, Min en Max.

Hallo tijdreeks zijn gebouwd met behulp van een ander proces. OEE en KPI's zijn berekend op basis van het station basisgegevens en borrelen voor Hallo-topologie (productie regels, fabrieken, enterprise) in de toepassing hello.

Tijdreeks voor OEE en KPI-topologie wordt bovendien in Hallo-app berekend wanneer een weergegeven timespan gereed is. Weergave van de dag hello wordt bijvoorbeeld elk volledige uur bijgewerkt.

Hallo time series weergave van knooppuntgegevens afkomstig zijn direct TSI met behulp van een aggregatie voor timespan.

## <a name="iot-hub"></a>IoT Hub
Hallo [IoT-hub] [ lnk-IoT Hub] ontvangt gegevens van Hallo OPC Publisher Module in de cloud Hallo verzonden en wordt het beschikbaar toohello TSI Azure-service. 

Hallo IoT-Hub in Hallo oplossing ook:
- Onderhoudt een register-id's die Hallo-id's voor alle OPC Publisher Module en alle OPC Proxy Modules opslaat.
- Wordt gebruikt als transportkanaal voor bidirectionele communicatie Hallo OPC Proxy-Module.

## <a name="azure-storage"></a>Azure Storage
Hallo-oplossing gebruikt Azure blob-opslag als schijfopslag voor Hallo VM en toostore implementatiegegevens.

## <a name="web-app"></a>Web-app
Hallo web-app is geïmplementeerd als onderdeel van Hallo vooraf geconfigureerde oplossing uit een geïntegreerde OPC UA-client bestaat, verwerking van waarschuwingen en visualisatie van telemetrie.

## <a name="next-steps"></a>Volgende stappen

U kunt blijven aan de slag met IoT Suite door te lezen Hallo artikelen te volgen:

* [Machtigingen op Hallo azureiotsuite.com site][lnk-permissions]
* [Implementeer een gateway op Windows of Linux voor Hallo verbonden factory vooraf geconfigureerde oplossing](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
