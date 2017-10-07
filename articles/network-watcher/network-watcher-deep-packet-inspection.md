---
title: aaaPacket inspectie met Azure-netwerk-Watcher | Microsoft Docs
description: Dit artikel wordt beschreven hoe toouse netwerk-Watcher tooperform grondige inspecties van pakketten verzameld van een virtuele machine
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
ms.openlocfilehash: 4aeddcd482edc4df3d63e87b5c4b0788c540850b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a><span data-ttu-id="18eb6-103">Pakketinspecties met Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="18eb6-103">Packet inspection with Azure Network Watcher</span></span>

<span data-ttu-id="18eb6-104">Hallo pakket vastleggen functie van netwerk-Watcher gebruikt, kunt u starten en beheren van sessies mogelijk op uw Azure VM's van Hallo-portal, PowerShell, CLI en programmatisch via Hallo SDK en de REST-API.</span><span class="sxs-lookup"><span data-stu-id="18eb6-104">Using hello packet capture feature of Network Watcher, you can initiate and manage captures sessions on your Azure VMs from hello portal, PowerShell, CLI, and programmatically through hello SDK and REST API.</span></span> <span data-ttu-id="18eb6-105">Pakketopname kunt u tooaddress-scenario's waarvoor niveau pakketgegevens doordat Hallo-gegevens in een indeling die gemakkelijk kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="18eb6-105">Packet capture allows you tooaddress scenarios that require packet level data by providing hello information in a readily usable format.</span></span> <span data-ttu-id="18eb6-106">Mogelijkheden van hulpprogramma tooinspect Hallo gegevens, kunt u onderzoeken communicaties tooand van uw virtuele machines en inzicht in het netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="18eb6-106">Leveraging freely available tools tooinspect hello data, you can examine communications sent tooand from your VMs and gain insights into your network traffic.</span></span> <span data-ttu-id="18eb6-107">Sommige toepassingen voorbeeld van Pakketgegevens vastleggen zijn onder andere: onderzoeken van problemen met netwerk of de toepassing, de pogingen misbruik en inbraakdetectie netwerk te detecteren of naleving van regelgeving onderhouden.</span><span class="sxs-lookup"><span data-stu-id="18eb6-107">Some example uses of packet capture data include: investigating network or application issues, detecting network misuse and intrusion attempts, or maintaining regulatory compliance.</span></span> <span data-ttu-id="18eb6-108">In dit artikel, laten we zien hoe tooopen een pakket vastleggen bestand geleverd door netwerk-Watcher met behulp van een populaire open-source hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="18eb6-108">In this article, we show how tooopen a packet capture file provided by Network Watcher using a popular open source tool.</span></span> <span data-ttu-id="18eb6-109">We bieden ook voorbeelden ziet u hoe toocalculate latentie van de verbinding abnormaal verkeer identificeren en netwerken statistieken onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="18eb6-109">We will also provide examples showing how toocalculate a connection latency, identify abnormal traffic, and examine networking statistics.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="18eb6-110">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="18eb6-110">Before you begin</span></span>

<span data-ttu-id="18eb6-111">In dit artikel gaat via een aantal vooraf geconfigureerde scenario's op een pakketopname die eerder is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="18eb6-111">This article goes through some pre-configured scenarios on a packet capture that was run previously.</span></span> <span data-ttu-id="18eb6-112">Deze scenario's illustreren mogelijkheden die aan de hand van een pakketopname kunnen worden geopend.</span><span class="sxs-lookup"><span data-stu-id="18eb6-112">These scenarios illustrate capabilities that can be accessed by reviewing a packet capture.</span></span> <span data-ttu-id="18eb6-113">Dit scenario wordt gebruikgemaakt van [WireShark](https://www.wireshark.org/) tooinspect hello pakketopname.</span><span class="sxs-lookup"><span data-stu-id="18eb6-113">This scenario uses [WireShark](https://www.wireshark.org/) tooinspect hello packet capture.</span></span>

<span data-ttu-id="18eb6-114">Dit scenario wordt ervan uitgegaan dat u al een pakketopname uitgevoerd op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="18eb6-114">This scenario assumes you already ran a packet capture on a virtual machine.</span></span> <span data-ttu-id="18eb6-115">hoe toocreate een pakketopname gaat u naar toolearn [beheren pakket worden vastgelegd met Hallo portal](network-watcher-packet-capture-manage-portal.md) of met REST in via [pakket vastgelegd beheren met de REST-API](network-watcher-packet-capture-manage-rest.md).</span><span class="sxs-lookup"><span data-stu-id="18eb6-115">toolearn how toocreate a packet capture visit [Manage packet captures with hello portal](network-watcher-packet-capture-manage-portal.md) or with REST by visiting [Managing Packet Captures with REST API](network-watcher-packet-capture-manage-rest.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="18eb6-116">Scenario</span><span class="sxs-lookup"><span data-stu-id="18eb6-116">Scenario</span></span>

<span data-ttu-id="18eb6-117">In dit scenario u:</span><span class="sxs-lookup"><span data-stu-id="18eb6-117">In this scenario, you:</span></span>

* <span data-ttu-id="18eb6-118">Bekijk een pakketopname</span><span class="sxs-lookup"><span data-stu-id="18eb6-118">Review a packet capture</span></span>

## <a name="calculate-network-latency"></a><span data-ttu-id="18eb6-119">Netwerklatentie berekenen</span><span class="sxs-lookup"><span data-stu-id="18eb6-119">Calculate network latency</span></span>

<span data-ttu-id="18eb6-120">In dit scenario, laten we zien hoe tooview Hallo initiële Round Trip Time RTT () van een Transmission Control Protocol (TCP) conversatie plaatsvinden tussen twee eindpunten.</span><span class="sxs-lookup"><span data-stu-id="18eb6-120">In this scenario, we show how tooview hello initial Round Trip Time (RTT) of a Transmission Control Protocol (TCP) conversation occurring between two endpoints.</span></span>

<span data-ttu-id="18eb6-121">Als er een TCP-verbinding tot stand is gebracht, voert hello eerste drie pakketten die worden verzonden in Hallo verbinding een patroon vaak aangeduid tooas Hallo drie richtingen handshake.</span><span class="sxs-lookup"><span data-stu-id="18eb6-121">When a TCP connection is established, hello first three packets sent in hello connection follow a pattern commonly referred tooas hello three-way handshake.</span></span> <span data-ttu-id="18eb6-122">Door in de eerste twee hello-pakketten dat in deze handshake, een eerste verzoek van Hallo-client en een antwoord van Hallo server verzonden, kunnen we Hallo latentie berekenen wanneer deze verbinding tot stand is gebracht.</span><span class="sxs-lookup"><span data-stu-id="18eb6-122">By examining hello first two packets sent in this handshake, an initial request from hello client and a response from hello server, we can calculate hello latency when this connection was established.</span></span> <span data-ttu-id="18eb6-123">Deze latentie is waarnaar wordt verwezen tooas Hallo Round Trip Time RTT ().</span><span class="sxs-lookup"><span data-stu-id="18eb6-123">This latency is referred tooas hello Round Trip Time (RTT).</span></span> <span data-ttu-id="18eb6-124">Raadpleeg voor meer informatie over Hallo TCP-protocol en Hallo drie richtingen handshake toohello resource te volgen.</span><span class="sxs-lookup"><span data-stu-id="18eb6-124">For more information on hello TCP protocol and hello three-way handshake refer toohello following resource.</span></span> <span data-ttu-id="18eb6-125">https://support.Microsoft.com/en-US/Help/172983/Explanation-of-the-three-way-handshake-via-TCP-IP</span><span class="sxs-lookup"><span data-stu-id="18eb6-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span></span>

### <a name="step-1"></a><span data-ttu-id="18eb6-126">Stap 1</span><span class="sxs-lookup"><span data-stu-id="18eb6-126">Step 1</span></span>

<span data-ttu-id="18eb6-127">WireShark starten</span><span class="sxs-lookup"><span data-stu-id="18eb6-127">Launch WireShark</span></span>

### <a name="step-2"></a><span data-ttu-id="18eb6-128">Stap 2</span><span class="sxs-lookup"><span data-stu-id="18eb6-128">Step 2</span></span>

<span data-ttu-id="18eb6-129">Load Hallo **CAP** bestand van uw pakketopname.</span><span class="sxs-lookup"><span data-stu-id="18eb6-129">Load hello **.cap** file from your packet capture.</span></span> <span data-ttu-id="18eb6-130">Dit bestand vindt u in Hallo blob het op onze lokaal op Hallo virtuele machine wordt opgeslagen, afhankelijk van hoe u geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="18eb6-130">This file can be found in hello blob it was saved in our locally on hello virtual machine, depending on how you configured it.</span></span>

### <a name="step-3"></a><span data-ttu-id="18eb6-131">Stap 3</span><span class="sxs-lookup"><span data-stu-id="18eb6-131">Step 3</span></span>

<span data-ttu-id="18eb6-132">tooview Hallo initiële Round Trip Time RTT () in de TCP-gesprekken, wordt alleen het bekijken van Hallo eerst twee pakketten die zijn betrokken bij Hallo TCP-handshake.</span><span class="sxs-lookup"><span data-stu-id="18eb6-132">tooview hello initial Round Trip Time (RTT) in TCP conversations, we will only be looking at hello first two packets involved in hello TCP handshake.</span></span> <span data-ttu-id="18eb6-133">We gebruiken Hallo eerst twee pakketten in drie richtingen-handshake hello, die Hallo [SYN], [SYN, ACK] pakketten.</span><span class="sxs-lookup"><span data-stu-id="18eb6-133">We will be using hello first two packets in hello three-way handshake, which are hello [SYN], [SYN, ACK] packets.</span></span> <span data-ttu-id="18eb6-134">Ze zijn met de naam van de vlaggen ingesteld in Hallo TCP-header.</span><span class="sxs-lookup"><span data-stu-id="18eb6-134">They are named for flags set in hello TCP header.</span></span> <span data-ttu-id="18eb6-135">laatste Hallo-pakket in Hallo-handshake wordt hello [ACK]-pakket wordt niet gebruikt in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="18eb6-135">hello last packet in hello handshake, hello [ACK] packet, will not be used in this scenario.</span></span> <span data-ttu-id="18eb6-136">Hallo [SYN] pakket wordt verzonden door Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="18eb6-136">hello [SYN] packet is sent by hello client.</span></span> <span data-ttu-id="18eb6-137">Zodra dit is ontvangen verzendt Hallo server hello [ACK]-pakket als een bevestiging ontvangen Hallo SYN van Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="18eb6-137">Once it is received hello server sends hello [ACK] packet as an acknowledgement of receiving hello SYN from hello client.</span></span> <span data-ttu-id="18eb6-138">Mogelijkheden van Hallo feit dat het antwoord van server Hallo weinig overhead vereist, berekenen we Hallo RTT door af te trekken Hallo tijd hello [SYN, ACK]-pakket is ontvangen door de client Hallo door hello tijd [SYN]-pakket is verzonden door de client Hallo.</span><span class="sxs-lookup"><span data-stu-id="18eb6-138">Leveraging hello fact that hello server’s response requires very little overhead, we calculate hello RTT by subtracting hello time hello [SYN, ACK] packet was received by hello client by hello time [SYN] packet was sent by hello client.</span></span>

<span data-ttu-id="18eb6-139">WireShark met is deze waarde berekend voor ons.</span><span class="sxs-lookup"><span data-stu-id="18eb6-139">Using WireShark this value is calculated for us.</span></span>

<span data-ttu-id="18eb6-140">eerste twee hello-pakketten toomore eenvoudig weergeven in drie richtingen handshake van Hallo TCP, maken we gebruik Hallo filtermogelijkheden geleverd door WireShark.</span><span class="sxs-lookup"><span data-stu-id="18eb6-140">toomore easily view hello first two packets in hello TCP three-way handshake, we will utilize hello filtering capability provided by WireShark.</span></span>

<span data-ttu-id="18eb6-141">tooapply hello filter in WireShark, vouw Hallo 'Transmission Control Protocol' Segment van een pakket [SYN] in uw vastleggen en onderzoeken Hallo-vlaggen ingesteld in Hallo TCP-header.</span><span class="sxs-lookup"><span data-stu-id="18eb6-141">tooapply hello filter in WireShark, expand hello “Transmission Control Protocol” Segment of a [SYN] packet in your capture and examine hello flags set in hello TCP header.</span></span>

<span data-ttu-id="18eb6-142">Aangezien we toofilter op alle [SYN zoekt] en [SYN ACK] pakketten onder vlaggen cofirm dat Hallo Syn bits too1 is ingesteld, wordt rechts Klik op Hallo Syn bits -> toepassen als Filter -> geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="18eb6-142">Since we are looking toofilter on all [SYN] and [SYN, ACK] packets, under flags cofirm that hello Syn bit is set too1, then right click on hello Syn bit -> Apply as Filter -> Selected.</span></span>

![Afbeelding 7][7]

### <a name="step-4"></a><span data-ttu-id="18eb6-144">Stap 4</span><span class="sxs-lookup"><span data-stu-id="18eb6-144">Step 4</span></span>

<span data-ttu-id="18eb6-145">Nu dat u hebt gefilterd Hallo venster tooonly Zie pakketten met Hallo [SYN] foutstijlbit, kunt u eenvoudig selecteren conversaties u geïnteresseerd bent in tooview Hallo initiële RTT.</span><span class="sxs-lookup"><span data-stu-id="18eb6-145">Now that you have filtered hello window tooonly see packets with hello [SYN] bit set, you can easily select conversations you are interested in tooview hello initial RTT.</span></span> <span data-ttu-id="18eb6-146">Een eenvoudige manier tooview Hallo RTT in WireShark klikt Hallo dropdown is gemarkeerd als ' SEQ/ACK' analyse.</span><span class="sxs-lookup"><span data-stu-id="18eb6-146">A simple way tooview hello RTT in WireShark simply click hello dropdown marked “SEQ/ACK” analysis.</span></span> <span data-ttu-id="18eb6-147">Vervolgens ziet u Hallo die RTT weergegeven.</span><span class="sxs-lookup"><span data-stu-id="18eb6-147">You will then see hello RTT displayed.</span></span> <span data-ttu-id="18eb6-148">In dit geval is Hallo RTT 0.0022114 seconden of 2.211 ms.</span><span class="sxs-lookup"><span data-stu-id="18eb6-148">In this case, hello RTT was 0.0022114 seconds, or 2.211 ms.</span></span>

![afbeelding 8][8]

## <a name="unwanted-protocols"></a><span data-ttu-id="18eb6-150">Ongewenste protocollen</span><span class="sxs-lookup"><span data-stu-id="18eb6-150">Unwanted protocols</span></span>

<span data-ttu-id="18eb6-151">U kunt hebben veel toepassingen die worden uitgevoerd op de instantie van een virtuele machine die u hebt geïmplementeerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="18eb6-151">You can have many applications running on a virtual machine instance you have deployed in Azure.</span></span> <span data-ttu-id="18eb6-152">Veel van deze toepassingen communiceren via Hallo-netwerk mogelijk zonder uw expliciete toestemming.</span><span class="sxs-lookup"><span data-stu-id="18eb6-152">Many of these applications communicate over hello network, perhaps without your explicit permission.</span></span> <span data-ttu-id="18eb6-153">Pakket vastleggen toostore netwerkcommunicatie gebruikt, kunt we hoe de toepassing wordt gesproken op Hallo netwerk en zoek naar problemen onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="18eb6-153">Using packet capture toostore network communication, we can investigate how application are talking on hello network and look for any issues.</span></span>

<span data-ttu-id="18eb6-154">In dit voorbeeld we bekijken een eerdere pakketopname voor ongewenste protocollen die mogelijk aangeven onbevoegde communicatie van een toepassing die wordt uitgevoerd op uw computer uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="18eb6-154">In this example, we review a previous ran packet capture for unwanted protocols that may indicate unauthorized communication from an application running on your machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="18eb6-155">Stap 1</span><span class="sxs-lookup"><span data-stu-id="18eb6-155">Step 1</span></span>

<span data-ttu-id="18eb6-156">Met behulp van dezelfde vastleggen Klik in het vorige scenario op Hallo Hallo **statistieken** > **Protocol hiërarchie**</span><span class="sxs-lookup"><span data-stu-id="18eb6-156">Using hello same capture in hello previous scenario click **Statistics** > **Protocol Hierarchy**</span></span>

![Protocol hiërarchie menu][2]

<span data-ttu-id="18eb6-158">Hallo protocol hiërarchie venster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="18eb6-158">hello protocol hierarchy window appears.</span></span> <span data-ttu-id="18eb6-159">Deze weergave bevat een lijst van alle Hallo-protocollen die werden gebruikt tijdens het Hallo opnamesessie en Hallo aantal pakketten verzonden en ontvangen met behulp van Hallo-protocollen.</span><span class="sxs-lookup"><span data-stu-id="18eb6-159">This view provides a list of all hello protocols that were in use during hello capture session and hello number of packets transmitted and received using hello protocols.</span></span> <span data-ttu-id="18eb6-160">Deze weergave is handig voor het vinden van ongewenste netwerkverkeer op de virtuele machines of het netwerk.</span><span class="sxs-lookup"><span data-stu-id="18eb6-160">This view can be useful for finding unwanted network traffic on your virtual machines or network.</span></span>

![protocol configureren geopend][3]

<span data-ttu-id="18eb6-162">Zoals u in de volgende schermopname hello ziet, moet u er verkeer dat gebruikmaakt van Hallo BitTorrent protocol, dat wordt gebruikt voor het delen van peer toopeer bestanden is.</span><span class="sxs-lookup"><span data-stu-id="18eb6-162">As you can see in hello following screen capture, there was traffic using hello BitTorrent protocol, which is used for peer toopeer file sharing.</span></span> <span data-ttu-id="18eb6-163">Als een beheerder verwacht u toosee BitTorrent verkeer niet op deze bepaalde virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="18eb6-163">As an administrator you do not expect toosee BitTorrent traffic on this particular virtual machines.</span></span> <span data-ttu-id="18eb6-164">Nu u op de hoogte van dit verkeer, kunt u Hallo peer toopeer software geïnstalleerd op deze virtuele machine of blok Hallo verkeer met behulp van Netwerkbeveiligingsgroepen of een Firewall.</span><span class="sxs-lookup"><span data-stu-id="18eb6-164">Now you aware of this traffic, you can remove hello peer toopeer software that installed on this virtual machine, or block hello traffic using Network Security Groups or a Firewall.</span></span> <span data-ttu-id="18eb6-165">U kunt bovendien toorun pakket opnamen volgens een schema ervoor kiezen zodat u kunt Hallo protocol gebruik regelmatig op uw virtuele machines bekijken.</span><span class="sxs-lookup"><span data-stu-id="18eb6-165">Additionally, you may elect toorun packet captures on a schedule, so you can review hello protocol use on your virtual machines regularly.</span></span> <span data-ttu-id="18eb6-166">Voor een voorbeeld van hoe tooautomate netwerk in azure vindt u taken [netwerkbronnen met azure automation bewaken](network-watcher-monitor-with-azure-automation.md)</span><span class="sxs-lookup"><span data-stu-id="18eb6-166">For an example on how tooautomate network tasks in azure visit [Monitor network resources with azure automation](network-watcher-monitor-with-azure-automation.md)</span></span>

## <a name="finding-top-destinations-and-ports"></a><span data-ttu-id="18eb6-167">Meest bezochte bestemmingen en poorten vinden</span><span class="sxs-lookup"><span data-stu-id="18eb6-167">Finding top destinations and ports</span></span>

<span data-ttu-id="18eb6-168">Kennis van Hallo typen verkeer, Hallo eindpunten en Hallo-poorten die via gecommuniceerd is een belangrijk bij het bewaken of het oplossen van toepassingen en bronnen in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="18eb6-168">Understanding hello types of traffic, hello endpoints, and hello ports communicated over is an important when monitoring or troubleshooting applications and resources on your network.</span></span> <span data-ttu-id="18eb6-169">Met behulp van een bestand voor het vastleggen van pakket van boven, kunnen we snel leren Hallo bovenste bestemmingen onze VM communiceert en Hallo poorten worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="18eb6-169">Utilizing a packet capture file from above, we can quickly learn hello top destinations our VM is communicating with and hello ports being utilized.</span></span>

### <a name="step-1"></a><span data-ttu-id="18eb6-170">Stap 1</span><span class="sxs-lookup"><span data-stu-id="18eb6-170">Step 1</span></span>

<span data-ttu-id="18eb6-171">Met behulp van dezelfde vastleggen Klik in het vorige scenario op Hallo Hallo **statistieken** > **IPv4-statistieken** > **bestemmingen en poorten**</span><span class="sxs-lookup"><span data-stu-id="18eb6-171">Using hello same capture in hello previous scenario click **Statistics** > **IPv4 Statistics** > **Destinations and Ports**</span></span>

![venster van pakket vastleggen][4]

### <a name="step-2"></a><span data-ttu-id="18eb6-173">Stap 2</span><span class="sxs-lookup"><span data-stu-id="18eb6-173">Step 2</span></span>

<span data-ttu-id="18eb6-174">Zoals we bekijkt hello resultaten een regel opvalt, er zijn meerdere verbindingen via poort 111.</span><span class="sxs-lookup"><span data-stu-id="18eb6-174">As we look through hello results a line stands out, there were multiple connections on port 111.</span></span> <span data-ttu-id="18eb6-175">Hallo meest gebruikte poort 3389, is dit extern bureaublad is en Hallo resterende RPC dynamische poorten zijn.</span><span class="sxs-lookup"><span data-stu-id="18eb6-175">hello most used port was 3389, which is remote desktop, and hello remaining are RPC dynamic ports.</span></span>

<span data-ttu-id="18eb6-176">Hoewel dit verkeer betekenen er niets dat kan, is een poort die is gebruikt voor het aantal verbindingen en onbekende toohello-beheerder.</span><span class="sxs-lookup"><span data-stu-id="18eb6-176">While this traffic may mean nothing, it is a port that was used for many connections and is unknown toohello administrator.</span></span>

![Afbeelding 5][5]

### <a name="step-3"></a><span data-ttu-id="18eb6-178">Stap 3</span><span class="sxs-lookup"><span data-stu-id="18eb6-178">Step 3</span></span>

<span data-ttu-id="18eb6-179">Nu dat we hebben een out-of plaats poort filteren we onze vastleggen op basis van Hallo poort bepaald.</span><span class="sxs-lookup"><span data-stu-id="18eb6-179">Now that we have determined an out of place port we can filter our capture based on hello port.</span></span>

<span data-ttu-id="18eb6-180">Hallo-filter in dit scenario zou zijn:</span><span class="sxs-lookup"><span data-stu-id="18eb6-180">hello filter in this scenario would be:</span></span>

```
tcp.port == 111
```

<span data-ttu-id="18eb6-181">We Hallo Filtertekst van boven in Hallo filter textbox invoeren en op ENTER drukken.</span><span class="sxs-lookup"><span data-stu-id="18eb6-181">We enter hello filter text from above in hello filter textbox and hit enter.</span></span>

![Afbeelding 6][6]

<span data-ttu-id="18eb6-183">Uit de resultaten hello, ziet u alle Hallo verkeer afkomstig is van een lokale virtuele machine op Hallo hetzelfde subnet.</span><span class="sxs-lookup"><span data-stu-id="18eb6-183">From hello results, we can see all hello traffic is coming from a local virtual machine on hello same subnet.</span></span> <span data-ttu-id="18eb6-184">Als we nog steeds niet waarom dit verkeer plaatsvindt begrijpen, kunnen we verder hello-pakketten toodetermine waarom het aan te deze aanroepen op poort 111 brengen inspecteren.</span><span class="sxs-lookup"><span data-stu-id="18eb6-184">If we still don’t understand why this traffic is occurring, we can further inspect hello packets toodetermine why it is making these calls on port 111.</span></span> <span data-ttu-id="18eb6-185">Met deze informatie kunnen we Hallo gepaste actie ondernemen.</span><span class="sxs-lookup"><span data-stu-id="18eb6-185">With this information we can take hello appropriate action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18eb6-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="18eb6-186">Next steps</span></span>

<span data-ttu-id="18eb6-187">Meer informatie over andere diagnostische functies van netwerk-Watcher Hallo in via [bewakingsoverzicht Azure-netwerk](network-watcher-monitoring-overview.md)</span><span class="sxs-lookup"><span data-stu-id="18eb6-187">Learn about hello other diagnostic features of Network Watcher by visiting [Azure network monitoring overview](network-watcher-monitoring-overview.md)</span></span>

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













