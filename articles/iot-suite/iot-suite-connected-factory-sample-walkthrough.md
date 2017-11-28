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
# <a name="connected-factory-preconfigured-solution-walkthrough"></a><span data-ttu-id="d42f7-103">Walkthrough voor de vooraf geconfigureerde oplossing Connected Factory</span><span class="sxs-lookup"><span data-stu-id="d42f7-103">Connected factory preconfigured solution walkthrough</span></span>

<span data-ttu-id="d42f7-104">Hallo IoT Suite verbonden factory [vooraf geconfigureerde oplossing] [ lnk-preconfigured-solutions] is een implementatie van een industriële end-to-end-oplossing die:</span><span class="sxs-lookup"><span data-stu-id="d42f7-104">hello IoT Suite connected factory [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end industrial solution that:</span></span>

* <span data-ttu-id="d42f7-105">Gesimuleerde tooboth industriële apparaten uitvoeren OPC UA-servers in de regels die gesimuleerde factory productie en apparaten met echte OPC UA-server verbonden.</span><span class="sxs-lookup"><span data-stu-id="d42f7-105">Connects tooboth simulated industrial devices running OPC UA servers in simulated factory production lines, and real OPC UA server devices.</span></span> <span data-ttu-id="d42f7-106">Zie voor meer informatie over OPC UA Hallo [verbonden factory Veelgestelde vragen over](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="d42f7-106">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="d42f7-107">Operationele KPI's en OEE van die apparaten en productielijnen kunnen worden bekeken.</span><span class="sxs-lookup"><span data-stu-id="d42f7-107">Shows operational KPIs and OEE of those devices and production lines.</span></span>
* <span data-ttu-id="d42f7-108">Laat zien hoe een cloud-gebaseerde toepassing gebruikte toointeract met systemen van OPC UA-server kan worden.</span><span class="sxs-lookup"><span data-stu-id="d42f7-108">Demonstrates how a cloud-based application could be used toointeract with OPC UA server systems.</span></span>
* <span data-ttu-id="d42f7-109">Hiermee kunt u tooconnect de apparaten van uw eigen OPC UA-server.</span><span class="sxs-lookup"><span data-stu-id="d42f7-109">Enables you tooconnect your own OPC UA server devices.</span></span>
* <span data-ttu-id="d42f7-110">Hiermee kunt u toobrowse en Hallo OPC UA-server-gegevens wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d42f7-110">Enables you toobrowse and modify hello OPC UA server data.</span></span>
* <span data-ttu-id="d42f7-111">Integreert met hello Azure Time Series Insights (TSI) service tooprovide aangepaste weergaven van gegevens van uw servers OPC UA Hallo.</span><span class="sxs-lookup"><span data-stu-id="d42f7-111">Integrates with hello Azure Time Series Insights (TSI) service tooprovide customized views of hello data from your OPC UA servers.</span></span>

<span data-ttu-id="d42f7-112">U kunt Hallo oplossing gebruiken als een beginpunt voor uw eigen implementatie en [aanpassen] [ lnk-customize] het toomeet uw eigen specifieke zakelijke vereisten.</span><span class="sxs-lookup"><span data-stu-id="d42f7-112">You can use hello solution as a starting point for your own implementation and [customize][lnk-customize] it toomeet your own specific business requirements.</span></span>

<span data-ttu-id="d42f7-113">In dit artikel worden enkele van de belangrijkste elementen van de Hallo van Hallo verbonden factory oplossing tooenable toounderstand u hoe het werkt.</span><span class="sxs-lookup"><span data-stu-id="d42f7-113">This article walks you through some of hello key elements of hello connected factory solution tooenable you toounderstand how it works.</span></span> <span data-ttu-id="d42f7-114">Deze kennis helpt u bij:</span><span class="sxs-lookup"><span data-stu-id="d42f7-114">This knowledge helps you to:</span></span>

* <span data-ttu-id="d42f7-115">Los problemen met het Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="d42f7-115">Troubleshoot issues in hello solution.</span></span>
* <span data-ttu-id="d42f7-116">Plannen hoe toocustomize toohello oplossing toomeet uw eigen specifieke vereisten.</span><span class="sxs-lookup"><span data-stu-id="d42f7-116">Plan how toocustomize toohello solution toomeet your own specific requirements.</span></span>
* <span data-ttu-id="d42f7-117">Het ontwerpen van uw eigen IoT-oplossing die gebruikmaakt van Azure-services.</span><span class="sxs-lookup"><span data-stu-id="d42f7-117">Design your own IoT solution that uses Azure services.</span></span>

<span data-ttu-id="d42f7-118">Zie voor meer informatie, Hallo [verbonden factory Veelgestelde vragen over](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="d42f7-118">For more information, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="d42f7-119">Logische architectuur</span><span class="sxs-lookup"><span data-stu-id="d42f7-119">Logical architecture</span></span>

<span data-ttu-id="d42f7-120">Hallo volgende diagram geeft een overzicht van de logische onderdelen van de Hallo van Hallo vooraf geconfigureerde oplossing:</span><span class="sxs-lookup"><span data-stu-id="d42f7-120">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![Logische architectuur van Connected Factory][connected-factory-logical]

## <a name="communication-patterns"></a><span data-ttu-id="d42f7-122">Communicatiepatronen</span><span class="sxs-lookup"><span data-stu-id="d42f7-122">Communication patterns</span></span>

<span data-ttu-id="d42f7-123">Hallo-oplossing maakt gebruik van Hallo [OPC UA Pub subitems specificatie](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend OPC UA telemetrie gegevens tooIoT Hub in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="d42f7-123">hello solution uses hello [OPC UA Pub/Sub specification](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend OPC UA telemetry data tooIoT Hub in JSON format.</span></span> <span data-ttu-id="d42f7-124">Hallo-oplossing maakt gebruik van Hallo [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge-module voor dit doel.</span><span class="sxs-lookup"><span data-stu-id="d42f7-124">hello solution uses hello [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge module for this purpose.</span></span>

<span data-ttu-id="d42f7-125">Hallo-oplossing heeft ook een OPC UA-client die is geïntegreerd in een webtoepassing die u kunt verbinding maken met on-premises OPC UA-servers.</span><span class="sxs-lookup"><span data-stu-id="d42f7-125">hello solution also has an OPC UA client integrated into a web application that can establish connections with on-premises OPC UA servers.</span></span> <span data-ttu-id="d42f7-126">Hallo-client gebruikt een [reverse proxy](https://wikipedia.org/wiki/Reverse_proxy) en ontvangt van de help van IoT Hub toomake Hallo verbinding zonder geopende poorten in Hallo lokale firewall.</span><span class="sxs-lookup"><span data-stu-id="d42f7-126">hello client uses a [reverse-proxy](https://wikipedia.org/wiki/Reverse_proxy) and receives help from IoT Hub toomake hello connection without requiring open ports in hello on-premises firewall.</span></span> <span data-ttu-id="d42f7-127">Dit communicatiepatroon heet [door service ondersteunde communicatie](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span><span class="sxs-lookup"><span data-stu-id="d42f7-127">This communication pattern is called [service-assisted communication](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span></span> <span data-ttu-id="d42f7-128">Hallo-oplossing maakt gebruik van Hallo [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge-module voor dit doel.</span><span class="sxs-lookup"><span data-stu-id="d42f7-128">hello solution uses hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge module for this purpose.</span></span>


## <a name="simulation"></a><span data-ttu-id="d42f7-129">Simulatie</span><span class="sxs-lookup"><span data-stu-id="d42f7-129">Simulation</span></span>

<span data-ttu-id="d42f7-130">Hallo gesimuleerde stations en productie-uitvoering Hallo gesimuleerde systemen (MES) van een fabriek productie-regel maken.</span><span class="sxs-lookup"><span data-stu-id="d42f7-130">hello simulated stations and hello simulated manufacturing execution systems (MES) make up a factory production line.</span></span> <span data-ttu-id="d42f7-131">Hallo gesimuleerde apparaten en Hallo OPC Publisher Module zijn gebaseerd op Hallo [OPC UA .NET Standard] [ lnk-OPC-UA-NET-Standard] gepubliceerd door Hallo OPC Foundation.</span><span class="sxs-lookup"><span data-stu-id="d42f7-131">hello simulated devices and hello OPC Publisher Module are based on hello [OPC UA .NET Standard][lnk-OPC-UA-NET-Standard] published by hello OPC Foundation.</span></span>

<span data-ttu-id="d42f7-132">Hallo OPC-Proxy en OPC-Publisher zijn geïmplementeerd als modules op basis van [Azure IoT rand][lnk-Azure-IoT-Gateway].</span><span class="sxs-lookup"><span data-stu-id="d42f7-132">hello OPC Proxy and OPC Publisher are implemented as modules based on [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span></span> <span data-ttu-id="d42f7-133">Elke gesimuleerde productielijn heeft een eigen gekoppelde gateway.</span><span class="sxs-lookup"><span data-stu-id="d42f7-133">Each simulated production line has a designated gateway attached.</span></span>

<span data-ttu-id="d42f7-134">Alle simulatie-onderdelen worden uitgevoerd in Docker-containers die worden gehost in een Azure Linux VM.</span><span class="sxs-lookup"><span data-stu-id="d42f7-134">All simulation components run in Docker containers  hosted in an Azure Linux VM.</span></span> <span data-ttu-id="d42f7-135">Hallo simulatie is geconfigureerde toorun acht gesimuleerde productieregels standaard.</span><span class="sxs-lookup"><span data-stu-id="d42f7-135">hello simulation is configured toorun eight simulated production lines by default.</span></span>

## <a name="simulated-production-line"></a><span data-ttu-id="d42f7-136">Gesimuleerde productielijn</span><span class="sxs-lookup"><span data-stu-id="d42f7-136">Simulated production line</span></span>

<span data-ttu-id="d42f7-137">In een productielijn worden onderdelen geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="d42f7-137">A production line manufactures parts.</span></span> <span data-ttu-id="d42f7-138">Deze bestaat uit verschillende stations: een montagestation, een teststation en een verpakkingsstation.</span><span class="sxs-lookup"><span data-stu-id="d42f7-138">It is composed of different stations: an assembly station, a test station, and a packaging station.</span></span>

<span data-ttu-id="d42f7-139">Hallo simulatie wordt uitgevoerd en Hallo gegevens bijgewerkt die beschikbaar is via het Hallo OPC UA knooppunten.</span><span class="sxs-lookup"><span data-stu-id="d42f7-139">hello simulation runs and updates hello data that is exposed through hello OPC UA nodes.</span></span> <span data-ttu-id="d42f7-140">Alle gesimuleerde productie regel stations zijn gedirigeerd door Hallo MES via OPC UA.</span><span class="sxs-lookup"><span data-stu-id="d42f7-140">All simulated production line stations are orchestrated by hello MES through OPC UA.</span></span>

## <a name="simulated-manufacturing-execution-system"></a><span data-ttu-id="d42f7-141">Gesimuleerd systeem voor de productie-uitvoering</span><span class="sxs-lookup"><span data-stu-id="d42f7-141">Simulated manufacturing execution system</span></span>

<span data-ttu-id="d42f7-142">Hallo MES bewaakt elk station op Hallo productie regel via OPC UA toodetect station statuswijzigingen.</span><span class="sxs-lookup"><span data-stu-id="d42f7-142">hello MES monitors each station in hello production line through OPC UA toodetect station status changes.</span></span> <span data-ttu-id="d42f7-143">Het OPC UA methoden toocontrol Hallo stations aangeroepen en wordt vervolgens een product is geslaagd vanuit één station toohello totdat deze voltooid is.</span><span class="sxs-lookup"><span data-stu-id="d42f7-143">It calls OPC UA methods toocontrol hello stations and passes a product from one station toohello next until it is complete.</span></span>

## <a name="gateway-opc-publisher-module"></a><span data-ttu-id="d42f7-144">Gateway OPC Publisher Module</span><span class="sxs-lookup"><span data-stu-id="d42f7-144">Gateway OPC publisher module</span></span>

<span data-ttu-id="d42f7-145">OPC Publisher Module verbindt toohello station OPC UA-servers en toohello OPC knooppunten toobe gepubliceerd op is geabonneerd.</span><span class="sxs-lookup"><span data-stu-id="d42f7-145">OPC Publisher Module connects toohello station OPC UA servers and subscribes toohello OPC nodes toobe published.</span></span> <span data-ttu-id="d42f7-146">Hallo module Hallo-knooppuntgegevens converteert naar JSON-indeling, versleutelt en tooIoT Hub als OPC UA Pub subitems berichten verzendt.</span><span class="sxs-lookup"><span data-stu-id="d42f7-146">hello module converts hello node data into JSON format, encrypts it, and sends it tooIoT Hub as OPC UA Pub/Sub messages.</span></span>

<span data-ttu-id="d42f7-147">Hallo OPC Publisher module alleen een uitgaande https-poort (443) vereist en kunt samenwerken met bestaande bedrijfsinfrastructuur.</span><span class="sxs-lookup"><span data-stu-id="d42f7-147">hello OPC Publisher module only requires an outbound https port (443) and can work with existing enterprise infrastructure.</span></span>

## <a name="gateway-opc-proxy-module"></a><span data-ttu-id="d42f7-148">Gateway OPC Proxy Module</span><span class="sxs-lookup"><span data-stu-id="d42f7-148">Gateway OPC proxy module</span></span>

<span data-ttu-id="d42f7-149">Hallo Gateway OPC UA Proxy Module tunnels binaire OPC UA-opdracht en controle berichten en vereist alleen een uitgaande https-poort (443).</span><span class="sxs-lookup"><span data-stu-id="d42f7-149">hello Gateway OPC UA Proxy Module tunnels binary OPC UA command and control messages and only requires an outbound https port (443).</span></span> <span data-ttu-id="d42f7-150">De module kan gebruikmaken van de bestaande bedrijfsinfrastructuur, zoals Web Proxies.</span><span class="sxs-lookup"><span data-stu-id="d42f7-150">It can work with existing enterprise infrastructure, including Web Proxies.</span></span>

<span data-ttu-id="d42f7-151">Deze IoT hubapparaat methoden tootransfer packetized TCP/IP-gegevens worden gebruikt op de toepassingslaag Hallo en dus garandeert eindpunt vertrouwen, gegevensversleuteling en integriteit met behulp van SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="d42f7-151">It uses IoT Hub Device methods tootransfer packetized TCP/IP data at hello application layer and thus ensures endpoint trust, data encryption, and integrity using SSL/TLS.</span></span>

<span data-ttu-id="d42f7-152">Hallo OPC UA binaire protocol doorgegeven via Hallo-proxyserver van zichzelf maakt gebruik van UA-verificatie en versleuteling.</span><span class="sxs-lookup"><span data-stu-id="d42f7-152">hello OPC UA binary protocol relayed through hello proxy itself uses UA authentication and encryption.</span></span>

## <a name="azure-time-series-insights"></a><span data-ttu-id="d42f7-153">Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="d42f7-153">Azure Time Series Insights</span></span>

<span data-ttu-id="d42f7-154">Hallo Gateway OPC Publisher Module tooOPC UA-server knooppunten toodetect wijziging in de gegevenswaarden Hallo is geabonneerd.</span><span class="sxs-lookup"><span data-stu-id="d42f7-154">hello Gateway OPC Publisher Module subscribes tooOPC UA server nodes toodetect change in hello data values.</span></span> <span data-ttu-id="d42f7-155">Als een gegevenswijziging in de in een van de knooppunten hello wordt gedetecteerd, wordt met deze module vervolgens berichten tooAzure IoT Hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="d42f7-155">If a data change is detected in one of hello nodes, this module then sends messages tooAzure IoT Hub.</span></span>

<span data-ttu-id="d42f7-156">IoT Hub biedt een gebeurtenis bron tooAzure TSI.</span><span class="sxs-lookup"><span data-stu-id="d42f7-156">IoT Hub provides an event source tooAzure TSI.</span></span> <span data-ttu-id="d42f7-157">TSI slaat gegevens voor 30 dagen op basis van tijdstempels gekoppeld toohello berichten.</span><span class="sxs-lookup"><span data-stu-id="d42f7-157">TSI stores data for 30 days based on timestamps attached toohello messages.</span></span> <span data-ttu-id="d42f7-158">Deze gegevens omvatten:</span><span class="sxs-lookup"><span data-stu-id="d42f7-158">This data includes:</span></span>

* <span data-ttu-id="d42f7-159">OPC UA ApplicationUri</span><span class="sxs-lookup"><span data-stu-id="d42f7-159">OPC UA ApplicationUri</span></span>
* <span data-ttu-id="d42f7-160">OPC UA NodeId</span><span class="sxs-lookup"><span data-stu-id="d42f7-160">OPC UA NodeId</span></span>
* <span data-ttu-id="d42f7-161">Waarde van Hallo-knooppunt</span><span class="sxs-lookup"><span data-stu-id="d42f7-161">Value of hello node</span></span>
* <span data-ttu-id="d42f7-162">Tijdstempel van de bron</span><span class="sxs-lookup"><span data-stu-id="d42f7-162">Source timestamp</span></span>
* <span data-ttu-id="d42f7-163">OPC UA DisplayName</span><span class="sxs-lookup"><span data-stu-id="d42f7-163">OPC UA DisplayName</span></span>

<span data-ttu-id="d42f7-164">Op dit moment TSI staat niet toe dat klanten toocustomize hoe lang ze tookeep Hallo gegevens voor wenst.</span><span class="sxs-lookup"><span data-stu-id="d42f7-164">Currently, TSI does not allow customers toocustomize how long they wish tookeep hello data for.</span></span>

<span data-ttu-id="d42f7-165">TSI voert query's uit voor de knooppuntgegevens op basis van een SearchSpan (Time.From, Time.To) en sorteert ze op basis van OPC UA ApplicationUri, OPC UA NodeId of OPC UA DisplayName.</span><span class="sxs-lookup"><span data-stu-id="d42f7-165">TSI queries against node data using a SearchSpan (Time.From, Time.To) and aggregates by OPC UA ApplicationUri or OPC UA NodeId or OPC UA DisplayName.</span></span>

<span data-ttu-id="d42f7-166">tooretrieve hello gegevens voor Hallo OEE en KPI meters en Hallo-tijdgrafieken reeks gegevens worden samengevoegd door het aantal gebeurtenissen, som, Gem, Min en Max.</span><span class="sxs-lookup"><span data-stu-id="d42f7-166">tooretrieve hello data for hello OEE and KPI gauges, and hello time series charts, data is aggregated by count of events, Sum, Avg, Min, and Max.</span></span>

<span data-ttu-id="d42f7-167">Hallo tijdreeks zijn gebouwd met behulp van een ander proces.</span><span class="sxs-lookup"><span data-stu-id="d42f7-167">hello time series are built using a different process.</span></span> <span data-ttu-id="d42f7-168">OEE en KPI's zijn berekend op basis van het station basisgegevens en borrelen voor Hallo-topologie (productie regels, fabrieken, enterprise) in de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="d42f7-168">OEE and KPIs are calculated from station base data and bubbled up for hello topology (production lines, factories, enterprise) in hello application.</span></span>

<span data-ttu-id="d42f7-169">Tijdreeks voor OEE en KPI-topologie wordt bovendien in Hallo-app berekend wanneer een weergegeven timespan gereed is.</span><span class="sxs-lookup"><span data-stu-id="d42f7-169">Additionally, time series for OEE and KPI topology is calculated in hello app, whenever a displayed timespan is ready.</span></span> <span data-ttu-id="d42f7-170">Weergave van de dag hello wordt bijvoorbeeld elk volledige uur bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="d42f7-170">For example, hello day view is updated every full hour.</span></span>

<span data-ttu-id="d42f7-171">Hallo time series weergave van knooppuntgegevens afkomstig zijn direct TSI met behulp van een aggregatie voor timespan.</span><span class="sxs-lookup"><span data-stu-id="d42f7-171">hello time series view of node data comes directly from TSI using an aggregation for timespan.</span></span>

## <a name="iot-hub"></a><span data-ttu-id="d42f7-172">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="d42f7-172">IoT Hub</span></span>
<span data-ttu-id="d42f7-173">Hallo [IoT-hub] [ lnk-IoT Hub] ontvangt gegevens van Hallo OPC Publisher Module in de cloud Hallo verzonden en wordt het beschikbaar toohello TSI Azure-service.</span><span class="sxs-lookup"><span data-stu-id="d42f7-173">hello [IoT hub][lnk-IoT Hub] receives data sent from hello OPC Publisher Module into hello cloud and makes it available toohello Azure TSI service.</span></span> 

<span data-ttu-id="d42f7-174">Hallo IoT-Hub in Hallo oplossing ook:</span><span class="sxs-lookup"><span data-stu-id="d42f7-174">hello IoT Hub in hello solution also:</span></span>
- <span data-ttu-id="d42f7-175">Onderhoudt een register-id's die Hallo-id's voor alle OPC Publisher Module en alle OPC Proxy Modules opslaat.</span><span class="sxs-lookup"><span data-stu-id="d42f7-175">Maintains an identity registry that stores hello IDs for all OPC Publisher Module and all OPC Proxy Modules.</span></span>
- <span data-ttu-id="d42f7-176">Wordt gebruikt als transportkanaal voor bidirectionele communicatie Hallo OPC Proxy-Module.</span><span class="sxs-lookup"><span data-stu-id="d42f7-176">Is used as transport channel for bidirectional communication of hello OPC Proxy Module.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="d42f7-177">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d42f7-177">Azure Storage</span></span>
<span data-ttu-id="d42f7-178">Hallo-oplossing gebruikt Azure blob-opslag als schijfopslag voor Hallo VM en toostore implementatiegegevens.</span><span class="sxs-lookup"><span data-stu-id="d42f7-178">hello solution uses Azure blob storage as disk storage for hello VM and toostore deployment data.</span></span>

## <a name="web-app"></a><span data-ttu-id="d42f7-179">Web-app</span><span class="sxs-lookup"><span data-stu-id="d42f7-179">Web app</span></span>
<span data-ttu-id="d42f7-180">Hallo web-app is geïmplementeerd als onderdeel van Hallo vooraf geconfigureerde oplossing uit een geïntegreerde OPC UA-client bestaat, verwerking van waarschuwingen en visualisatie van telemetrie.</span><span class="sxs-lookup"><span data-stu-id="d42f7-180">hello web app deployed as part of hello preconfigured solution comprises of an integrated OPC UA client, alerts processing and telemetry visualization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d42f7-181">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d42f7-181">Next steps</span></span>

<span data-ttu-id="d42f7-182">U kunt blijven aan de slag met IoT Suite door te lezen Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d42f7-182">You can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="d42f7-183">[Machtigingen op Hallo azureiotsuite.com site][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="d42f7-183">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="d42f7-184">Implementeer een gateway op Windows of Linux voor Hallo verbonden factory vooraf geconfigureerde oplossing</span><span class="sxs-lookup"><span data-stu-id="d42f7-184">Deploy a gateway on Windows or Linux for hello connected factory preconfigured solution</span></span>](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
