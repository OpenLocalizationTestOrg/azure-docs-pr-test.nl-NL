---
title: Pakketinspecties met Azure-netwerk-Watcher | Microsoft Docs
description: Dit artikel wordt beschreven hoe u met netwerk-Watcher grondige pakketinspecties verzameld van een virtuele machine uitvoeren
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b907d00-9c35-40f5-a61e-beb7b782276f
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 91c47bb8922a9be21dff72e7cf64b29b14a36e9e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a><span data-ttu-id="d438a-103">Pakketinspecties met Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="d438a-103">Packet inspection with Azure Network Watcher</span></span>

<span data-ttu-id="d438a-104">Met de functie voor het vastleggen van pakket van netwerk-Watcher, kunt u starten en beheren van sessies mogelijk op uw Azure VM's via de portal, PowerShell, CLI en programmatisch via de SDK en de REST-API.</span><span class="sxs-lookup"><span data-stu-id="d438a-104">Using the packet capture feature of Network Watcher, you can initiate and manage captures sessions on your Azure VMs from the portal, PowerShell, CLI, and programmatically through the SDK and REST API.</span></span> <span data-ttu-id="d438a-105">Pakketopname kunt u de adres-scenario's waarvoor niveau pakketgegevens doordat de gegevens in een indeling die gemakkelijk kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d438a-105">Packet capture allows you to address scenarios that require packet level data by providing the information in a readily usable format.</span></span> <span data-ttu-id="d438a-106">Mogelijkheden van gratis hulpprogramma's voor het controleren van de gegevens, kunt u onderzoeken communicatie naar en van uw virtuele machines en inzicht in het netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="d438a-106">Leveraging freely available tools to inspect the data, you can examine communications sent to and from your VMs and gain insights into your network traffic.</span></span> <span data-ttu-id="d438a-107">Sommige toepassingen voorbeeld van Pakketgegevens vastleggen zijn onder andere: onderzoeken van problemen met netwerk of de toepassing, de pogingen misbruik en inbraakdetectie netwerk te detecteren of naleving van regelgeving onderhouden.</span><span class="sxs-lookup"><span data-stu-id="d438a-107">Some example uses of packet capture data include: investigating network or application issues, detecting network misuse and intrusion attempts, or maintaining regulatory compliance.</span></span> <span data-ttu-id="d438a-108">In dit artikel, laten we zien hoe een pakket vastleggen bestand geleverd door de netwerk-Watcher te openen met behulp van een populaire open-source hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="d438a-108">In this article, we show how to open a packet capture file provided by Network Watcher using a popular open source tool.</span></span> <span data-ttu-id="d438a-109">We bieden ook voorbeelden waarin wordt getoond hoe een latentie van de verbinding berekenen, abnormaal verkeer identificeren en netwerken statistieken onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="d438a-109">We will also provide examples showing how to calculate a connection latency, identify abnormal traffic, and examine networking statistics.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d438a-110">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="d438a-110">Before you begin</span></span>

<span data-ttu-id="d438a-111">In dit artikel gaat via een aantal vooraf geconfigureerde scenario's op een pakketopname die eerder is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d438a-111">This article goes through some pre-configured scenarios on a packet capture that was run previously.</span></span> <span data-ttu-id="d438a-112">Deze scenario's illustreren mogelijkheden die aan de hand van een pakketopname kunnen worden geopend.</span><span class="sxs-lookup"><span data-stu-id="d438a-112">These scenarios illustrate capabilities that can be accessed by reviewing a packet capture.</span></span> <span data-ttu-id="d438a-113">Dit scenario wordt gebruikgemaakt van [WireShark](https://www.wireshark.org/) de pakketopname controleren.</span><span class="sxs-lookup"><span data-stu-id="d438a-113">This scenario uses [WireShark](https://www.wireshark.org/) to inspect the packet capture.</span></span>

<span data-ttu-id="d438a-114">Dit scenario wordt ervan uitgegaan dat u al een pakketopname uitgevoerd op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d438a-114">This scenario assumes you already ran a packet capture on a virtual machine.</span></span> <span data-ttu-id="d438a-115">Voor informatie over het maken van een pakket vastleggen Bezoek [beheren pakket worden vastgelegd met de portal](network-watcher-packet-capture-manage-portal.md) of met REST in via [pakket vastgelegd beheren met de REST-API](network-watcher-packet-capture-manage-rest.md).</span><span class="sxs-lookup"><span data-stu-id="d438a-115">To learn how to create a packet capture visit [Manage packet captures with the portal](network-watcher-packet-capture-manage-portal.md) or with REST by visiting [Managing Packet Captures with REST API](network-watcher-packet-capture-manage-rest.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="d438a-116">Scenario</span><span class="sxs-lookup"><span data-stu-id="d438a-116">Scenario</span></span>

<span data-ttu-id="d438a-117">In dit scenario u:</span><span class="sxs-lookup"><span data-stu-id="d438a-117">In this scenario, you:</span></span>

* <span data-ttu-id="d438a-118">Bekijk een pakketopname</span><span class="sxs-lookup"><span data-stu-id="d438a-118">Review a packet capture</span></span>

## <a name="calculate-network-latency"></a><span data-ttu-id="d438a-119">Netwerklatentie berekenen</span><span class="sxs-lookup"><span data-stu-id="d438a-119">Calculate network latency</span></span>

<span data-ttu-id="d438a-120">In dit scenario, laten we zien hoe de initiële Round Trip Time (RTT) van een Transmission Control Protocol (TCP) conversatie plaatsvinden tussen twee eindpunten weergeven.</span><span class="sxs-lookup"><span data-stu-id="d438a-120">In this scenario, we show how to view the initial Round Trip Time (RTT) of a Transmission Control Protocol (TCP) conversation occurring between two endpoints.</span></span>

<span data-ttu-id="d438a-121">Wanneer een TCP-verbinding tot stand is gebracht, volgt u de eerste drie pakketten worden verzonden in de verbinding een patroon vaak aangeduid als de handshake drie richtingen.</span><span class="sxs-lookup"><span data-stu-id="d438a-121">When a TCP connection is established, the first three packets sent in the connection follow a pattern commonly referred to as the three-way handshake.</span></span> <span data-ttu-id="d438a-122">Door in de eerste twee pakketten worden verzonden in deze-handshake wordt een eerste verzoek van de client en een reactie van de server, kunnen we de latentie berekenen wanneer deze verbinding tot stand is gebracht.</span><span class="sxs-lookup"><span data-stu-id="d438a-122">By examining the first two packets sent in this handshake, an initial request from the client and a response from the server, we can calculate the latency when this connection was established.</span></span> <span data-ttu-id="d438a-123">Deze latentie wordt aangeduid als de Round Trip Time (RTT).</span><span class="sxs-lookup"><span data-stu-id="d438a-123">This latency is referred to as the Round Trip Time (RTT).</span></span> <span data-ttu-id="d438a-124">Raadpleeg de volgende bron voor meer informatie over het TCP-protocol en de handshake drie richtingen.</span><span class="sxs-lookup"><span data-stu-id="d438a-124">For more information on the TCP protocol and the three-way handshake refer to the following resource.</span></span> <span data-ttu-id="d438a-125">https://support.Microsoft.com/en-US/Help/172983/Explanation-of-the-three-way-handshake-via-TCP-IP</span><span class="sxs-lookup"><span data-stu-id="d438a-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span></span>

### <a name="step-1"></a><span data-ttu-id="d438a-126">Stap 1</span><span class="sxs-lookup"><span data-stu-id="d438a-126">Step 1</span></span>

<span data-ttu-id="d438a-127">WireShark starten</span><span class="sxs-lookup"><span data-stu-id="d438a-127">Launch WireShark</span></span>

### <a name="step-2"></a><span data-ttu-id="d438a-128">Stap 2</span><span class="sxs-lookup"><span data-stu-id="d438a-128">Step 2</span></span>

<span data-ttu-id="d438a-129">Load de **CAP** bestand van uw pakketopname.</span><span class="sxs-lookup"><span data-stu-id="d438a-129">Load the **.cap** file from your packet capture.</span></span> <span data-ttu-id="d438a-130">Dit bestand kan gevonden worden in de blob machine werd opgeslagen in onze lokaal op de virtuele machine, afhankelijk van hoe u geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d438a-130">This file can be found in the blob it was saved in our locally on the virtual machine, depending on how you configured it.</span></span>

### <a name="step-3"></a><span data-ttu-id="d438a-131">Stap 3</span><span class="sxs-lookup"><span data-stu-id="d438a-131">Step 3</span></span>

<span data-ttu-id="d438a-132">Om weer te geven de initiële Round Trip Time (RTT) in de TCP-gesprekken, we alleen voor het bekijken van de eerste twee pakketten die zijn betrokken bij de TCP-handshake.</span><span class="sxs-lookup"><span data-stu-id="d438a-132">To view the initial Round Trip Time (RTT) in TCP conversations, we will only be looking at the first two packets involved in the TCP handshake.</span></span> <span data-ttu-id="d438a-133">We gebruiken de eerste twee pakketten in de handshake drie richtingen die de [SYN], [SYN, ACK] pakketten.</span><span class="sxs-lookup"><span data-stu-id="d438a-133">We will be using the first two packets in the three-way handshake, which are the [SYN], [SYN, ACK] packets.</span></span> <span data-ttu-id="d438a-134">Ze zijn met de naam van de vlaggen ingesteld in de TCP-header.</span><span class="sxs-lookup"><span data-stu-id="d438a-134">They are named for flags set in the TCP header.</span></span> <span data-ttu-id="d438a-135">Het laatste pakket in de handshake, het pakket [ACK] wordt niet gebruikt in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="d438a-135">The last packet in the handshake, the [ACK] packet, will not be used in this scenario.</span></span> <span data-ttu-id="d438a-136">Het pakket [SYN] wordt verzonden door de client.</span><span class="sxs-lookup"><span data-stu-id="d438a-136">The [SYN] packet is sent by the client.</span></span> <span data-ttu-id="d438a-137">Zodra dit is ontvangen verzendt de server [ACK]-pakket als een bevestiging van ontvangst van de SYN van de client.</span><span class="sxs-lookup"><span data-stu-id="d438a-137">Once it is received the server sends the [ACK] packet as an acknowledgement of receiving the SYN from the client.</span></span> <span data-ttu-id="d438a-138">Mogelijkheden van het feit dat het antwoord van de server weinig overhead vereist, we berekent de RTT door af te trekken van de tijd de [SYN, ACK] pakket is ontvangen door de client door de tijd [SYN] pakket is verzonden door de client.</span><span class="sxs-lookup"><span data-stu-id="d438a-138">Leveraging the fact that the server’s response requires very little overhead, we calculate the RTT by subtracting the time the [SYN, ACK] packet was received by the client by the time [SYN] packet was sent by the client.</span></span>

<span data-ttu-id="d438a-139">WireShark met is deze waarde berekend voor ons.</span><span class="sxs-lookup"><span data-stu-id="d438a-139">Using WireShark this value is calculated for us.</span></span>

<span data-ttu-id="d438a-140">Om het gemakkelijker de eerste twee pakketten in de TCP-handshake drie richtingen bekijken, maken we filteren gebruiker krijgt de mogelijkheid door WireShark gebruik.</span><span class="sxs-lookup"><span data-stu-id="d438a-140">To more easily view the first two packets in the TCP three-way handshake, we will utilize the filtering capability provided by WireShark.</span></span>

<span data-ttu-id="d438a-141">Als u wilt toepassen op het filter in WireShark, vouw het Segment 'Transmission Control Protocol' van een pakket [SYN] in uw vastleggen en bekijk de vlaggen ingesteld in de TCP-header.</span><span class="sxs-lookup"><span data-stu-id="d438a-141">To apply the filter in WireShark, expand the “Transmission Control Protocol” Segment of a [SYN] packet in your capture and examine the flags set in the TCP header.</span></span>

<span data-ttu-id="d438a-142">Aangezien we willen filteren op alle [SYN] en [SYN ACK] pakketten onder vlaggen cofirm dat de Syn-bit is ingesteld op 1 en rechts Klik op de Syn-bit -> toepassen als Filter -> geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="d438a-142">Since we are looking to filter on all [SYN] and [SYN, ACK] packets, under flags cofirm that the Syn bit is set to 1, then right click on the Syn bit -> Apply as Filter -> Selected.</span></span>

![Afbeelding 7][7]

### <a name="step-4"></a><span data-ttu-id="d438a-144">Stap 4</span><span class="sxs-lookup"><span data-stu-id="d438a-144">Step 4</span></span>

<span data-ttu-id="d438a-145">Nu dat u hebt gefilterd om te zien alleen de pakketten met de [SYN] bit is ingesteld, kunt u eenvoudig conversaties die u geïnteresseerd bent in de eerste RTT weergeven.</span><span class="sxs-lookup"><span data-stu-id="d438a-145">Now that you have filtered the window to only see packets with the [SYN] bit set, you can easily select conversations you are interested in to view the initial RTT.</span></span> <span data-ttu-id="d438a-146">Een eenvoudige manier om weer te geven van de RTT in WireShark Klik op de vervolgkeuzelijst ' SEQ/ACK' analyse gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="d438a-146">A simple way to view the RTT in WireShark simply click the dropdown marked “SEQ/ACK” analysis.</span></span> <span data-ttu-id="d438a-147">Vervolgens ziet u de RTT weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d438a-147">You will then see the RTT displayed.</span></span> <span data-ttu-id="d438a-148">In dit geval is de RTT 0.0022114 seconden of 2.211 ms.</span><span class="sxs-lookup"><span data-stu-id="d438a-148">In this case, the RTT was 0.0022114 seconds, or 2.211 ms.</span></span>

![afbeelding 8][8]

## <a name="unwanted-protocols"></a><span data-ttu-id="d438a-150">Ongewenste protocollen</span><span class="sxs-lookup"><span data-stu-id="d438a-150">Unwanted protocols</span></span>

<span data-ttu-id="d438a-151">U kunt hebben veel toepassingen die worden uitgevoerd op de instantie van een virtuele machine die u hebt geïmplementeerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="d438a-151">You can have many applications running on a virtual machine instance you have deployed in Azure.</span></span> <span data-ttu-id="d438a-152">Veel van deze toepassingen communiceren via het netwerk mogelijk zonder uw expliciete toestemming.</span><span class="sxs-lookup"><span data-stu-id="d438a-152">Many of these applications communicate over the network, perhaps without your explicit permission.</span></span> <span data-ttu-id="d438a-153">Pakketopname gebruiken voor het opslaan van netwerkcommunicatie, kunt we hoe de toepassing wordt gesproken op het netwerk en zoek naar problemen onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="d438a-153">Using packet capture to store network communication, we can investigate how application are talking on the network and look for any issues.</span></span>

<span data-ttu-id="d438a-154">In dit voorbeeld we bekijken een eerdere pakketopname voor ongewenste protocollen die mogelijk aangeven onbevoegde communicatie van een toepassing die wordt uitgevoerd op uw computer uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d438a-154">In this example, we review a previous ran packet capture for unwanted protocols that may indicate unauthorized communication from an application running on your machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="d438a-155">Stap 1</span><span class="sxs-lookup"><span data-stu-id="d438a-155">Step 1</span></span>

<span data-ttu-id="d438a-156">Klik met de dezelfde opname in het voorgaande scenario **statistieken** > **Protocol hiërarchie**</span><span class="sxs-lookup"><span data-stu-id="d438a-156">Using the same capture in the previous scenario click **Statistics** > **Protocol Hierarchy**</span></span>

![Protocol hiërarchie menu][2]

<span data-ttu-id="d438a-158">Het protocol hiërarchie-venster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d438a-158">The protocol hierarchy window appears.</span></span> <span data-ttu-id="d438a-159">Deze weergave bevat een lijst van alle protocollen die werden gebruikt tijdens de opnamesessie en het aantal pakketten verzonden en ontvangen van de te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d438a-159">This view provides a list of all the protocols that were in use during the capture session and the number of packets transmitted and received using the protocols.</span></span> <span data-ttu-id="d438a-160">Deze weergave is handig voor het vinden van ongewenste netwerkverkeer op de virtuele machines of het netwerk.</span><span class="sxs-lookup"><span data-stu-id="d438a-160">This view can be useful for finding unwanted network traffic on your virtual machines or network.</span></span>

![protocol configureren geopend][3]

<span data-ttu-id="d438a-162">Zoals u in de volgende schermopname ziet, moet u er verkeer dat gebruikmaakt van het protocol BitTorrent, dat wordt gebruikt voor het delen van bestanden van de peer-to-peer is.</span><span class="sxs-lookup"><span data-stu-id="d438a-162">As you can see in the following screen capture, there was traffic using the BitTorrent protocol, which is used for peer to peer file sharing.</span></span> <span data-ttu-id="d438a-163">Als een beheerder u niet van plan bent om te zien BitTorrent verkeer op deze bepaalde virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="d438a-163">As an administrator you do not expect to see BitTorrent traffic on this particular virtual machines.</span></span> <span data-ttu-id="d438a-164">Nu u op de hoogte van dit verkeer, kunt u verwijderen de peer-to-peer-software die op deze virtuele machine is geïnstalleerd, of het verkeer met behulp van Netwerkbeveiligingsgroepen of Firewall blokkeren.</span><span class="sxs-lookup"><span data-stu-id="d438a-164">Now you aware of this traffic, you can remove the peer to peer software that installed on this virtual machine, or block the traffic using Network Security Groups or a Firewall.</span></span> <span data-ttu-id="d438a-165">U kunt bovendien ervoor kiezen pakket opnamen uitvoeren volgens een schema, zodat u kunt het gebruik van het protocol op uw virtuele machines regelmatig bekijken.</span><span class="sxs-lookup"><span data-stu-id="d438a-165">Additionally, you may elect to run packet captures on a schedule, so you can review the protocol use on your virtual machines regularly.</span></span> <span data-ttu-id="d438a-166">Voor een voorbeeld over het automatiseren van netwerktaken in azure gaat u naar [netwerkbronnen met azure automation bewaken](network-watcher-monitor-with-azure-automation.md)</span><span class="sxs-lookup"><span data-stu-id="d438a-166">For an example on how to automate network tasks in azure visit [Monitor network resources with azure automation](network-watcher-monitor-with-azure-automation.md)</span></span>

## <a name="finding-top-destinations-and-ports"></a><span data-ttu-id="d438a-167">Meest bezochte bestemmingen en poorten vinden</span><span class="sxs-lookup"><span data-stu-id="d438a-167">Finding top destinations and ports</span></span>

<span data-ttu-id="d438a-168">Informatie over de typen verkeer, de eindpunten en de poorten die via gecommuniceerd is een belangrijk bij het bewaken of het oplossen van toepassingen en bronnen in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="d438a-168">Understanding the types of traffic, the endpoints, and the ports communicated over is an important when monitoring or troubleshooting applications and resources on your network.</span></span> <span data-ttu-id="d438a-169">Met behulp van een bestand voor het vastleggen van pakket van boven, kunnen we snel leren de bovenste bestemmingen die onze VM communiceert en de poorten die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d438a-169">Utilizing a packet capture file from above, we can quickly learn the top destinations our VM is communicating with and the ports being utilized.</span></span>

### <a name="step-1"></a><span data-ttu-id="d438a-170">Stap 1</span><span class="sxs-lookup"><span data-stu-id="d438a-170">Step 1</span></span>

<span data-ttu-id="d438a-171">Klik met de dezelfde opname in het voorgaande scenario **statistieken** > **IPv4-statistieken** > **bestemmingen en poorten**</span><span class="sxs-lookup"><span data-stu-id="d438a-171">Using the same capture in the previous scenario click **Statistics** > **IPv4 Statistics** > **Destinations and Ports**</span></span>

![venster van pakket vastleggen][4]

### <a name="step-2"></a><span data-ttu-id="d438a-173">Stap 2</span><span class="sxs-lookup"><span data-stu-id="d438a-173">Step 2</span></span>

<span data-ttu-id="d438a-174">Als we door de resultaten die een regel opvalt bekijken, zijn er meerdere verbindingen via poort 111.</span><span class="sxs-lookup"><span data-stu-id="d438a-174">As we look through the results a line stands out, there were multiple connections on port 111.</span></span> <span data-ttu-id="d438a-175">De meest gebruikte poort 3389, is dit de extern bureaublad is en de resterende RPC dynamische poorten zijn.</span><span class="sxs-lookup"><span data-stu-id="d438a-175">The most used port was 3389, which is remote desktop, and the remaining are RPC dynamic ports.</span></span>

<span data-ttu-id="d438a-176">Hoewel dit verkeer betekenen er niets dat kan, is een poort die is gebruikt voor het aantal verbindingen en is onbekend bij de beheerder.</span><span class="sxs-lookup"><span data-stu-id="d438a-176">While this traffic may mean nothing, it is a port that was used for many connections and is unknown to the administrator.</span></span>

![Afbeelding 5][5]

### <a name="step-3"></a><span data-ttu-id="d438a-178">Stap 3</span><span class="sxs-lookup"><span data-stu-id="d438a-178">Step 3</span></span>

<span data-ttu-id="d438a-179">Nu dat we hebben vastgesteld dat een out-of plaats poort filteren we onze vastleggen op basis van de poort.</span><span class="sxs-lookup"><span data-stu-id="d438a-179">Now that we have determined an out of place port we can filter our capture based on the port.</span></span>

<span data-ttu-id="d438a-180">Het filter in dit scenario zou zijn:</span><span class="sxs-lookup"><span data-stu-id="d438a-180">The filter in this scenario would be:</span></span>

```
tcp.port == 111
```

<span data-ttu-id="d438a-181">We de Filtertekst uit boven in het tekstvak filter invoeren en op ENTER drukken.</span><span class="sxs-lookup"><span data-stu-id="d438a-181">We enter the filter text from above in the filter textbox and hit enter.</span></span>

![Afbeelding 6][6]

<span data-ttu-id="d438a-183">In de resultaten ziet u dat alle verkeer afkomstig is van een lokale virtuele machine op hetzelfde subnet.</span><span class="sxs-lookup"><span data-stu-id="d438a-183">From the results, we can see all the traffic is coming from a local virtual machine on the same subnet.</span></span> <span data-ttu-id="d438a-184">Als we nog steeds niet waarom dit verkeer plaatsvindt begrijpen, kunnen we de pakketten om te bepalen waarom het aan te brengen deze aanroepen op poort 111 verdere inspecteren.</span><span class="sxs-lookup"><span data-stu-id="d438a-184">If we still don’t understand why this traffic is occurring, we can further inspect the packets to determine why it is making these calls on port 111.</span></span> <span data-ttu-id="d438a-185">Met deze informatie kunnen we de juiste actie ondernemen.</span><span class="sxs-lookup"><span data-stu-id="d438a-185">With this information we can take the appropriate action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d438a-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d438a-186">Next steps</span></span>

<span data-ttu-id="d438a-187">Meer informatie over de andere diagnostische functies van netwerk-Watcher in via [bewakingsoverzicht Azure-netwerk](network-watcher-monitoring-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d438a-187">Learn about the other diagnostic features of Network Watcher by visiting [Azure network monitoring overview](network-watcher-monitoring-overview.md)</span></span>

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













