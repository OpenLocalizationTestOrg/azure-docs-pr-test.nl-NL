---
title: Walkthrough voor de Azure IoT-oplossing Connected Factory | Microsoft Docs
description: Een beschrijving van de vooraf geconfigureerde Azure IoT-oplossing Connected Factory en de bijbehorende architectuur.
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
ms.openlocfilehash: 517e908a744734139ed0aeee314a4f3b9eda86cc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a><span data-ttu-id="c7550-103">Walkthrough voor de vooraf geconfigureerde oplossing Connected Factory</span><span class="sxs-lookup"><span data-stu-id="c7550-103">Connected factory preconfigured solution walkthrough</span></span>

<span data-ttu-id="c7550-104">De [vooraf geconfigureerd oplossing][lnk-preconfigured-solutions] Connected Factory uit IoT Suite is een implementatie van een end-to-endoplossing waarmee:</span><span class="sxs-lookup"><span data-stu-id="c7550-104">The IoT Suite connected factory [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end industrial solution that:</span></span>

* <span data-ttu-id="c7550-105">Gesimuleerde industriële apparaten met OPC UA-servers in gesimuleerde fabrieksproductielijnen en echte OPC UA-serverapparaten kunnen worden verbonden.</span><span class="sxs-lookup"><span data-stu-id="c7550-105">Connects to both simulated industrial devices running OPC UA servers in simulated factory production lines, and real OPC UA server devices.</span></span> <span data-ttu-id="c7550-106">Zie de [veelgestelde vragen over Connected Factory](iot-suite-faq-cf.md) voor meer informatie over OPC UA.</span><span class="sxs-lookup"><span data-stu-id="c7550-106">For more information about OPC UA, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="c7550-107">Operationele KPI's en OEE van die apparaten en productielijnen kunnen worden bekeken.</span><span class="sxs-lookup"><span data-stu-id="c7550-107">Shows operational KPIs and OEE of those devices and production lines.</span></span>
* <span data-ttu-id="c7550-108">U kunt bekijken hoe cloudgebaseerde toepassingen kunnen worden gebruikt om te werken met OPC UA-serversystemen.</span><span class="sxs-lookup"><span data-stu-id="c7550-108">Demonstrates how a cloud-based application could be used to interact with OPC UA server systems.</span></span>
* <span data-ttu-id="c7550-109">U verbinding kunt maken met uw eigen OPC UA-serverapparaten.</span><span class="sxs-lookup"><span data-stu-id="c7550-109">Enables you to connect your own OPC UA server devices.</span></span>
* <span data-ttu-id="c7550-110">U kunt bladeren in de OPC UA-servergegevens en waarmee u deze kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c7550-110">Enables you to browse and modify the OPC UA server data.</span></span>
* <span data-ttu-id="c7550-111">U kunt integreren met de Azure Time Series Insights-service (TSI) om aangepaste weergaven te bekijken van de gegevens van uw OPC UA-servers.</span><span class="sxs-lookup"><span data-stu-id="c7550-111">Integrates with the Azure Time Series Insights (TSI) service to provide customized views of the data from your OPC UA servers.</span></span>

<span data-ttu-id="c7550-112">U kunt de oplossing gebruiken als uitgangspunt voor uw eigen implementatie en u kunt deze [aanpassen][lnk-customize] aan uw eigen specifieke zakelijke vereisten.</span><span class="sxs-lookup"><span data-stu-id="c7550-112">You can use the solution as a starting point for your own implementation and [customize][lnk-customize] it to meet your own specific business requirements.</span></span>

<span data-ttu-id="c7550-113">In dit artikel wordt stapsgewijs een aantal belangrijke elementen van de oplossing Connected Factory beschreven, zodat u beter begrijpt hoe deze werkt.</span><span class="sxs-lookup"><span data-stu-id="c7550-113">This article walks you through some of the key elements of the connected factory solution to enable you to understand how it works.</span></span> <span data-ttu-id="c7550-114">Deze kennis helpt u bij:</span><span class="sxs-lookup"><span data-stu-id="c7550-114">This knowledge helps you to:</span></span>

* <span data-ttu-id="c7550-115">Het oplossen van problemen met de oplossing.</span><span class="sxs-lookup"><span data-stu-id="c7550-115">Troubleshoot issues in the solution.</span></span>
* <span data-ttu-id="c7550-116">Het plannen van een aanpassing van de oplossing zodat deze voldoet aan uw eigen specifieke vereisten.</span><span class="sxs-lookup"><span data-stu-id="c7550-116">Plan how to customize to the solution to meet your own specific requirements.</span></span>
* <span data-ttu-id="c7550-117">Het ontwerpen van uw eigen IoT-oplossing die gebruikmaakt van Azure-services.</span><span class="sxs-lookup"><span data-stu-id="c7550-117">Design your own IoT solution that uses Azure services.</span></span>

<span data-ttu-id="c7550-118">Zie de [veelgestelde vragen over Connected Factory](iot-suite-faq-cf.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c7550-118">For more information, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="c7550-119">Logische architectuur</span><span class="sxs-lookup"><span data-stu-id="c7550-119">Logical architecture</span></span>

<span data-ttu-id="c7550-120">Het volgende diagram geeft een overzicht van de logische onderdelen van de vooraf geconfigureerde oplossing:</span><span class="sxs-lookup"><span data-stu-id="c7550-120">The following diagram outlines the logical components of the preconfigured solution:</span></span>

![Logische architectuur van Connected Factory][connected-factory-logical]

## <a name="communication-patterns"></a><span data-ttu-id="c7550-122">Communicatiepatronen</span><span class="sxs-lookup"><span data-stu-id="c7550-122">Communication patterns</span></span>

<span data-ttu-id="c7550-123">Voor de oplossing wordt gebruikgemaakt van de [OPC UA Pub/Sub-specificatie](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) voor het verzenden van OPC UA-telemetriegegevens naar IoT Hub in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="c7550-123">The solution uses the [OPC UA Pub/Sub specification](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) to send OPC UA telemetry data to IoT Hub in JSON format.</span></span> <span data-ttu-id="c7550-124">Voor de oplossing wordt gebruikgemaakt van de IoT Edge-module [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) voor dit doeleinde.</span><span class="sxs-lookup"><span data-stu-id="c7550-124">The solution uses the [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge module for this purpose.</span></span>

<span data-ttu-id="c7550-125">Als onderdeel van de oplossing is ook een OPC UA-client geïntegreerd in een webtoepassing, die verbinding kan maken met on-premises OPC UA-servers.</span><span class="sxs-lookup"><span data-stu-id="c7550-125">The solution also has an OPC UA client integrated into a web application that can establish connections with on-premises OPC UA servers.</span></span> <span data-ttu-id="c7550-126">De client maakt gebruik van een [omgekeerde proxy](https://wikipedia.org/wiki/Reverse_proxy) en ontvangt hulp van IoT Hub om verbinding te maken zonder dat er open poorten in de on-premises firewall nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="c7550-126">The client uses a [reverse-proxy](https://wikipedia.org/wiki/Reverse_proxy) and receives help from IoT Hub to make the connection without requiring open ports in the on-premises firewall.</span></span> <span data-ttu-id="c7550-127">Dit communicatiepatroon heet [door service ondersteunde communicatie](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span><span class="sxs-lookup"><span data-stu-id="c7550-127">This communication pattern is called [service-assisted communication](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span></span> <span data-ttu-id="c7550-128">Voor de oplossing wordt gebruikgemaakt van de IoT Edge-module [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) voor dit doeleinde.</span><span class="sxs-lookup"><span data-stu-id="c7550-128">The solution uses the [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge module for this purpose.</span></span>


## <a name="simulation"></a><span data-ttu-id="c7550-129">Simulatie</span><span class="sxs-lookup"><span data-stu-id="c7550-129">Simulation</span></span>

<span data-ttu-id="c7550-130">De gesimuleerde stations en de gesimuleerde productie-uitvoeringssystemen (MES) vormen samen een fabrieksproductielijn.</span><span class="sxs-lookup"><span data-stu-id="c7550-130">The simulated stations and the simulated manufacturing execution systems (MES) make up a factory production line.</span></span> <span data-ttu-id="c7550-131">De gesimuleerde apparaten en de OPC Publisher Module zijn gebaseerd op de [OPC UA .NET Standard][lnk-OPC-UA-NET-Standard] die is gepubliceerd door de OPC Foundation.</span><span class="sxs-lookup"><span data-stu-id="c7550-131">The simulated devices and the OPC Publisher Module are based on the [OPC UA .NET Standard][lnk-OPC-UA-NET-Standard] published by the OPC Foundation.</span></span>

<span data-ttu-id="c7550-132">OPC Proxy en OPC Publisher worden als modules geïmplementeerd op basis van [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span><span class="sxs-lookup"><span data-stu-id="c7550-132">The OPC Proxy and OPC Publisher are implemented as modules based on [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span></span> <span data-ttu-id="c7550-133">Elke gesimuleerde productielijn heeft een eigen gekoppelde gateway.</span><span class="sxs-lookup"><span data-stu-id="c7550-133">Each simulated production line has a designated gateway attached.</span></span>

<span data-ttu-id="c7550-134">Alle simulatie-onderdelen worden uitgevoerd in Docker-containers die worden gehost in een Azure Linux VM.</span><span class="sxs-lookup"><span data-stu-id="c7550-134">All simulation components run in Docker containers  hosted in an Azure Linux VM.</span></span> <span data-ttu-id="c7550-135">De simulatie wordt standaard geconfigureerd voor het uitvoeren van acht gesimuleerde productielijnen.</span><span class="sxs-lookup"><span data-stu-id="c7550-135">The simulation is configured to run eight simulated production lines by default.</span></span>

## <a name="simulated-production-line"></a><span data-ttu-id="c7550-136">Gesimuleerde productielijn</span><span class="sxs-lookup"><span data-stu-id="c7550-136">Simulated production line</span></span>

<span data-ttu-id="c7550-137">In een productielijn worden onderdelen geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="c7550-137">A production line manufactures parts.</span></span> <span data-ttu-id="c7550-138">Deze bestaat uit verschillende stations: een montagestation, een teststation en een verpakkingsstation.</span><span class="sxs-lookup"><span data-stu-id="c7550-138">It is composed of different stations: an assembly station, a test station, and a packaging station.</span></span>

<span data-ttu-id="c7550-139">De simulatie wordt uitgevoerd en werkt de gegevens bij die worden vrijgegeven via de OPC UA-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="c7550-139">The simulation runs and updates the data that is exposed through the OPC UA nodes.</span></span> <span data-ttu-id="c7550-140">Alle stations uit de gesimuleerde productielijn worden via OPC UA beheerd door de MES.</span><span class="sxs-lookup"><span data-stu-id="c7550-140">All simulated production line stations are orchestrated by the MES through OPC UA.</span></span>

## <a name="simulated-manufacturing-execution-system"></a><span data-ttu-id="c7550-141">Gesimuleerd systeem voor de productie-uitvoering</span><span class="sxs-lookup"><span data-stu-id="c7550-141">Simulated manufacturing execution system</span></span>

<span data-ttu-id="c7550-142">De MES bewaakt alle stations in de productielijn via OPC UA om wijzigingen in de stationsstatus te detecteren.</span><span class="sxs-lookup"><span data-stu-id="c7550-142">The MES monitors each station in the production line through OPC UA to detect station status changes.</span></span> <span data-ttu-id="c7550-143">Er worden OPC UA-methoden aangeroepen om de stations te bedienen en producten worden van station naar station verplaatst tot ze voltooid zijn.</span><span class="sxs-lookup"><span data-stu-id="c7550-143">It calls OPC UA methods to control the stations and passes a product from one station to the next until it is complete.</span></span>

## <a name="gateway-opc-publisher-module"></a><span data-ttu-id="c7550-144">Gateway OPC Publisher Module</span><span class="sxs-lookup"><span data-stu-id="c7550-144">Gateway OPC publisher module</span></span>

<span data-ttu-id="c7550-145">OPC Publisher Module wordt verbonden met de OPC UA-servers van de stations en wordt geabonneerd op de OPC-knooppunten die moeten worden gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="c7550-145">OPC Publisher Module connects to the station OPC UA servers and subscribes to the OPC nodes to be published.</span></span> <span data-ttu-id="c7550-146">De module converteert de knooppuntgegevens naar de JSON-indeling, versleutelt deze en verstuurt ze naar IoT Hub als OPC UA Pub/Sub-berichten.</span><span class="sxs-lookup"><span data-stu-id="c7550-146">The module converts the node data into JSON format, encrypts it, and sends it to IoT Hub as OPC UA Pub/Sub messages.</span></span>

<span data-ttu-id="c7550-147">OPC Publisher Module vereist slechts één uitgaande HTTPS-poort (443) en kan gebruikmaken van de bestaande bedrijfsinfrastructuur.</span><span class="sxs-lookup"><span data-stu-id="c7550-147">The OPC Publisher module only requires an outbound https port (443) and can work with existing enterprise infrastructure.</span></span>

## <a name="gateway-opc-proxy-module"></a><span data-ttu-id="c7550-148">Gateway OPC Proxy Module</span><span class="sxs-lookup"><span data-stu-id="c7550-148">Gateway OPC proxy module</span></span>

<span data-ttu-id="c7550-149">Gateway OPC UA Proxy stuurt binaire OPC UA-opdrachten en bedieningsberichten door en vereist slechts één uitgaande HTTPS-poort (443).</span><span class="sxs-lookup"><span data-stu-id="c7550-149">The Gateway OPC UA Proxy Module tunnels binary OPC UA command and control messages and only requires an outbound https port (443).</span></span> <span data-ttu-id="c7550-150">De module kan gebruikmaken van de bestaande bedrijfsinfrastructuur, zoals Web Proxies.</span><span class="sxs-lookup"><span data-stu-id="c7550-150">It can work with existing enterprise infrastructure, including Web Proxies.</span></span>

<span data-ttu-id="c7550-151">Er wordt gebruikgemaakt van IoT Hub-apparaatmethoden om TCP/IP-gegevens in pakketten in de toepassingslaag over te dragen. Dit zorgt voor eindpuntvertrouwen, gegevensversleuteling en integriteit dankzij SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="c7550-151">It uses IoT Hub Device methods to transfer packetized TCP/IP data at the application layer and thus ensures endpoint trust, data encryption, and integrity using SSL/TLS.</span></span>

<span data-ttu-id="c7550-152">Het binaire OPC UA-protocol dat wordt doorgegeven via de proxy zelf maakt gebruik van UA-verificatie en -versleuteling.</span><span class="sxs-lookup"><span data-stu-id="c7550-152">The OPC UA binary protocol relayed through the proxy itself uses UA authentication and encryption.</span></span>

## <a name="azure-time-series-insights"></a><span data-ttu-id="c7550-153">Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="c7550-153">Azure Time Series Insights</span></span>

<span data-ttu-id="c7550-154">De Gateway OPC Publisher Module wordt geabonneerd op OPC UA-serverknooppunten, zodat wijzigingen in de gegevenswaarden kunnen worden gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="c7550-154">The Gateway OPC Publisher Module subscribes to OPC UA server nodes to detect change in the data values.</span></span> <span data-ttu-id="c7550-155">Als er een gegevenswijziging wordt gedetecteerd in een van de knooppunten, stuurt deze module berichten naar Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c7550-155">If a data change is detected in one of the nodes, this module then sends messages to Azure IoT Hub.</span></span>

<span data-ttu-id="c7550-156">IoT Hub biedt een gebeurtenisbron aan Azure TSI.</span><span class="sxs-lookup"><span data-stu-id="c7550-156">IoT Hub provides an event source to Azure TSI.</span></span> <span data-ttu-id="c7550-157">TSI slaat gegevens gedurende 30 dagen op, op basis van de tijdstempels die aan de berichten zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="c7550-157">TSI stores data for 30 days based on timestamps attached to the messages.</span></span> <span data-ttu-id="c7550-158">Deze gegevens omvatten:</span><span class="sxs-lookup"><span data-stu-id="c7550-158">This data includes:</span></span>

* <span data-ttu-id="c7550-159">OPC UA ApplicationUri</span><span class="sxs-lookup"><span data-stu-id="c7550-159">OPC UA ApplicationUri</span></span>
* <span data-ttu-id="c7550-160">OPC UA NodeId</span><span class="sxs-lookup"><span data-stu-id="c7550-160">OPC UA NodeId</span></span>
* <span data-ttu-id="c7550-161">Waarde van het knooppunt</span><span class="sxs-lookup"><span data-stu-id="c7550-161">Value of the node</span></span>
* <span data-ttu-id="c7550-162">Tijdstempel van de bron</span><span class="sxs-lookup"><span data-stu-id="c7550-162">Source timestamp</span></span>
* <span data-ttu-id="c7550-163">OPC UA DisplayName</span><span class="sxs-lookup"><span data-stu-id="c7550-163">OPC UA DisplayName</span></span>

<span data-ttu-id="c7550-164">Momenteel kunnen klanten met TSI niet aanpassen hoe lang ze de gegevens willen bewaren.</span><span class="sxs-lookup"><span data-stu-id="c7550-164">Currently, TSI does not allow customers to customize how long they wish to keep the data for.</span></span>

<span data-ttu-id="c7550-165">TSI voert query's uit voor de knooppuntgegevens op basis van een SearchSpan (Time.From, Time.To) en sorteert ze op basis van OPC UA ApplicationUri, OPC UA NodeId of OPC UA DisplayName.</span><span class="sxs-lookup"><span data-stu-id="c7550-165">TSI queries against node data using a SearchSpan (Time.From, Time.To) and aggregates by OPC UA ApplicationUri or OPC UA NodeId or OPC UA DisplayName.</span></span>

<span data-ttu-id="c7550-166">Als u gegevens wilt ophalen voor de OEE- en KPI-meters en de tijdreeksdiagrammen, worden gegevens gesorteerd op basis van het aantal gebeurtenissen, Sum, Avg, Min en Max.</span><span class="sxs-lookup"><span data-stu-id="c7550-166">To retrieve the data for the OEE and KPI gauges, and the time series charts, data is aggregated by count of events, Sum, Avg, Min, and Max.</span></span>

<span data-ttu-id="c7550-167">De tijdreeksen worden opgebouwd op basis van een ander proces.</span><span class="sxs-lookup"><span data-stu-id="c7550-167">The time series are built using a different process.</span></span> <span data-ttu-id="c7550-168">De OEE en KPI's worden berekend op basis van stationbasisgegevens en opgedeeld op basis van de topologie (productielijnen, fabrieken, bedrijf) in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="c7550-168">OEE and KPIs are calculated from station base data and bubbled up for the topology (production lines, factories, enterprise) in the application.</span></span>

<span data-ttu-id="c7550-169">Daarnaast worden de tijdreeksen voor OEE- en KPI-topologie berekend in de app zodra er een weergegeven periode gereed is.</span><span class="sxs-lookup"><span data-stu-id="c7550-169">Additionally, time series for OEE and KPI topology is calculated in the app, whenever a displayed timespan is ready.</span></span> <span data-ttu-id="c7550-170">De dagweergave wordt bijvoorbeeld elk volledig uur bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c7550-170">For example, the day view is updated every full hour.</span></span>

<span data-ttu-id="c7550-171">De tijdreeksweergave van knooppuntgegevens is rechtstreeks uit TSI afkomstig, met een sortering op basis van de periode.</span><span class="sxs-lookup"><span data-stu-id="c7550-171">The time series view of node data comes directly from TSI using an aggregation for timespan.</span></span>

## <a name="iot-hub"></a><span data-ttu-id="c7550-172">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="c7550-172">IoT Hub</span></span>
<span data-ttu-id="c7550-173">[IoT Hub][lnk-IoT Hub] ontvangt gegevens die vanaf OPC Publisher Module worden verzonden naar de cloud, en maakt ze beschikbaar voor de Azure TSI-service.</span><span class="sxs-lookup"><span data-stu-id="c7550-173">The [IoT hub][lnk-IoT Hub] receives data sent from the OPC Publisher Module into the cloud and makes it available to the Azure TSI service.</span></span> 

<span data-ttu-id="c7550-174">De IoT Hub in de oplossing doet ook het volgende:</span><span class="sxs-lookup"><span data-stu-id="c7550-174">The IoT Hub in the solution also:</span></span>
- <span data-ttu-id="c7550-175">Een identiteitsregister beheren waarin de id's van OPC Publisher Modules en OPC Proxy Modules worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c7550-175">Maintains an identity registry that stores the IDs for all OPC Publisher Module and all OPC Proxy Modules.</span></span>
- <span data-ttu-id="c7550-176">Handelen als transportkanaal voor bidirectionele communicatie van de OPC Proxy Module.</span><span class="sxs-lookup"><span data-stu-id="c7550-176">Is used as transport channel for bidirectional communication of the OPC Proxy Module.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="c7550-177">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c7550-177">Azure Storage</span></span>
<span data-ttu-id="c7550-178">Voor de oplossing wordt gebruikgemaakt van Azure Blob Storage voor schijfopslag voor de VM en om implementatiegegevens op te slaan.</span><span class="sxs-lookup"><span data-stu-id="c7550-178">The solution uses Azure blob storage as disk storage for the VM and to store deployment data.</span></span>

## <a name="web-app"></a><span data-ttu-id="c7550-179">Web-app</span><span class="sxs-lookup"><span data-stu-id="c7550-179">Web app</span></span>
<span data-ttu-id="c7550-180">De web-app die wordt geïmplementeerd als onderdeel van de vooraf geconfigureerde oplossing, bestaat uit een ingebouwde OPC UA-client, biedt verwerking van waarschuwingen en biedt visualisatie van de telemetrie.</span><span class="sxs-lookup"><span data-stu-id="c7550-180">The web app deployed as part of the preconfigured solution comprises of an integrated OPC UA client, alerts processing and telemetry visualization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7550-181">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c7550-181">Next steps</span></span>

<span data-ttu-id="c7550-182">U kunt verder aan de slag gaan met IoT Suite door de volgende artikelen te lezen:</span><span class="sxs-lookup"><span data-stu-id="c7550-182">You can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="c7550-183">[Machtigingen op de site azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="c7550-183">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="c7550-184">Een gateway implementeren in Windows of Linux voor de vooraf geconfigureerde oplossing Connected Factory</span><span class="sxs-lookup"><span data-stu-id="c7550-184">Deploy a gateway on Windows or Linux for the connected factory preconfigured solution</span></span>](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
