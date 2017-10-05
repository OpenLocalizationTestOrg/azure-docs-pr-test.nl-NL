---
title: Patronen in het netwerkverkeer met Azure-netwerk-Watcher en open-source hulpprogramma's visualiseren | Microsoft Docs
description: Deze pagina beschrijft het gebruik van netwerk-Watcher pakketopname met Capanalysis voor het visualiseren van patronen in het netwerkverkeer naar en van uw virtuele machines.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: e27bb694d0cbcf1ff7c9d8ca4682a79c8b5c5cb1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-network-traffic-patterns-to-and-from-your-vms-using-open-source-tools"></a><span data-ttu-id="ad170-103">Visualiseren patronen in het netwerkverkeer naar en van uw virtuele machines met open-source hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="ad170-103">Visualize network traffic patterns to and from your VMs using open source tools</span></span>

<span data-ttu-id="ad170-104">Pakket opnamen bevatten gegevens van het netwerk waarmee u kunt het netwerk forensische en grondige pakketinspecties uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ad170-104">Packet captures contain network data that allow you to perform network forensics and deep packet inspection.</span></span> <span data-ttu-id="ad170-105">Er zijn veel wordt geopend, source hulpprogramma's die u gebruiken kunt voor het analyseren van opnamen van pakket voor het verkrijgen van inzicht in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="ad170-105">There are many opens source tools you can use to analyze packet captures to gain insights about your network.</span></span> <span data-ttu-id="ad170-106">Een van deze programma is CapAnalysis, een visualisatie pakket open-source hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="ad170-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span></span> <span data-ttu-id="ad170-107">Pakket vastleggen gegevens te visualiseren is een waardevolle manier voor het afleiden van snel inzicht op patronen en afwijkingen in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="ad170-107">Visualizing packet capture data is a valuable way to quickly derive insights on patterns and anomalies within your network.</span></span> <span data-ttu-id="ad170-108">Visualisaties bieden ook een manier om dergelijke insights te delen op een manier eenvoudig worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ad170-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span></span>

<span data-ttu-id="ad170-109">Azure netwerk-Watcher biedt u de mogelijkheid voor het vastleggen van deze waardevolle gegevens doordat u voor het pakket opnamen uitvoeren op uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="ad170-109">Azure’s Network Watcher provides you the ability to capture this valuable data by allowing you to perform packet captures on your network.</span></span> <span data-ttu-id="ad170-110">In dit artikel bieden we een overzicht van het visualiseren en Verkrijg inzicht in het pakket worden vastgelegd met behulp van CapAnalysis met netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="ad170-110">In this article, we provide a walkthrough of how to visualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="ad170-111">Scenario</span><span class="sxs-lookup"><span data-stu-id="ad170-111">Scenario</span></span>

<span data-ttu-id="ad170-112">U hebt een eenvoudige webtoepassing geïmplementeerd op een virtuele machine in Azure wilt gebruiken van open-source hulpprogramma's voor het visualiseren van het netwerkverkeer om snel te identificeren stroom patronen en eventuele mogelijke afwijkingen.</span><span class="sxs-lookup"><span data-stu-id="ad170-112">You have a simple web application deployed on a VM in Azure want to use open source tools to visualize its network traffic to quickly identify flow patterns and any possible anomalies.</span></span> <span data-ttu-id="ad170-113">U kunt met de netwerk-Watcher verkrijgen van een pakketopname van uw netwerkomgeving en bewaar deze rechtstreeks van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ad170-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span></span> <span data-ttu-id="ad170-114">CapAnalysis kunnen vervolgens de pakketopname rechtstreeks van de storage-blob voor opnemen en visualiseren van de inhoud ervan.</span><span class="sxs-lookup"><span data-stu-id="ad170-114">CapAnalysis can then ingest the packet capture directly from the storage blob and visualize its contents.</span></span>

![scenario][1]

## <a name="steps"></a><span data-ttu-id="ad170-116">Stappen</span><span class="sxs-lookup"><span data-stu-id="ad170-116">Steps</span></span>

### <a name="install-capanalysis"></a><span data-ttu-id="ad170-117">CapAnalysis installeren</span><span class="sxs-lookup"><span data-stu-id="ad170-117">Install CapAnalysis</span></span>

<span data-ttu-id="ad170-118">Als u wilt installeren CapAnalysis op een virtuele machine, kunt u hier de officiële instructies https://www.capanalysis.net/ca/how-to-install-capanalysis verwijzen.</span><span class="sxs-lookup"><span data-stu-id="ad170-118">To install CapAnalysis on a virtual machine, you can refer to the official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span></span>
<span data-ttu-id="ad170-119">In volgorde extern toegang tot CapAnalysis, moeten we open poort 9877 op de virtuele machine door een nieuwe beveiligingsregel voor binnenkomende toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="ad170-119">In order access CapAnalysis remotely, we need to open port 9877 on your VM by adding a new inbound security rule.</span></span> <span data-ttu-id="ad170-120">Raadpleeg voor meer informatie over het maken van regels in Netwerkbeveiligingsgroepen [regels maken in een bestaande NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span><span class="sxs-lookup"><span data-stu-id="ad170-120">For more about creating rules in Network Security Groups, refer to [Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span></span> <span data-ttu-id="ad170-121">Wanneer de regel is toegevoegd, moet u kunnen toegang krijgen tot CapAnalysis van`http://<PublicIP>:9877`</span><span class="sxs-lookup"><span data-stu-id="ad170-121">Once the rule has been successfully added, you should be able to access CapAnalysis from `http://<PublicIP>:9877`</span></span>

### <a name="use-azure-network-watcher-to-start-a-packet-capture-session"></a><span data-ttu-id="ad170-122">Gebruik Azure netwerk-Watcher pakket vastleggen sessie starten</span><span class="sxs-lookup"><span data-stu-id="ad170-122">Use Azure Network Watcher to start a packet capture session</span></span>

<span data-ttu-id="ad170-123">Netwerk-Watcher kunt u pakketten om bij te houden van verkeer van en naar een virtuele machine vastleggen.</span><span class="sxs-lookup"><span data-stu-id="ad170-123">Network Watcher allows you to capture packets to track traffic in and out of a virtual machine.</span></span> <span data-ttu-id="ad170-124">U kunt verwijzen naar de instructies op de [beheren pakket worden vastgelegd met de netwerk-Watcher](network-watcher-packet-capture-manage-portal.md) pakket vastleggen sessie starten.</span><span class="sxs-lookup"><span data-stu-id="ad170-124">You can refer to the instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) to start a packet capture session.</span></span> <span data-ttu-id="ad170-125">Deze pakketopname kan worden opgeslagen in een blob storage toegankelijk door CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="ad170-125">This packet capture can be stored in a storage blob to be accessed by CapAnalysis.</span></span>

### <a name="upload-a-packet-capture-to-capanalysis"></a><span data-ttu-id="ad170-126">Een pakketopname uploaden naar CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="ad170-126">Upload a packet capture to CapAnalysis</span></span>
<span data-ttu-id="ad170-127">U kunt rechtstreeks uploaden een pakketopname die door de netwerk-watcher via het tabblad 'Importeren van URL' en het geven van een koppeling naar de blob storage waar het vastleggen van het pakket wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ad170-127">You can directly upload a packet capture taken by network watcher using the “Import from URL” tab and providing a link to the storage blob where the packet capture is stored.</span></span>

<span data-ttu-id="ad170-128">Wanneer een koppeling biedt naar CapAnalysis, zorg er dan voor dat een SAS-token toevoegen aan de URL van de opslag-blob.</span><span class="sxs-lookup"><span data-stu-id="ad170-128">When providing a link to CapAnalysis, make sure to append a SAS token to the storage blob URL.</span></span>  <span data-ttu-id="ad170-129">Hiervoor gaat u naar de gedeelde-toegangshandtekening van het opslagaccount, de toegestane machtigingen aanwijzen en druk op de knop SAS genereren voor het maken van een token.</span><span class="sxs-lookup"><span data-stu-id="ad170-129">To do this, navigate to Shared access signature from the storage account, designate the allowed permissions, and press the Generate SAS button to create a token.</span></span> <span data-ttu-id="ad170-130">Vervolgens kunt u deze SAS-token toevoegen aan de URL van de pakket vastleggen opslag-blob.</span><span class="sxs-lookup"><span data-stu-id="ad170-130">You can then append this SAS token to the packet capture storage blob URL.</span></span>

<span data-ttu-id="ad170-131">De resulterende URL ziet er ongeveer als volgt: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span><span class="sxs-lookup"><span data-stu-id="ad170-131">The resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span></span>


### <a name="analyzing-packet-captures"></a><span data-ttu-id="ad170-132">Analyseren van pakket worden vastgelegd</span><span class="sxs-lookup"><span data-stu-id="ad170-132">Analyzing packet captures</span></span>

<span data-ttu-id="ad170-133">CapAnalysis biedt verschillende opties voor het visualiseren van uw pakketopname, elke verstrekken analyse vanuit een ander perspectief.</span><span class="sxs-lookup"><span data-stu-id="ad170-133">CapAnalysis offers various options to visualize your packet capture, each providing analysis from a different perspective.</span></span> <span data-ttu-id="ad170-134">U kunt met deze visual samenvattingen inzicht in uw netwerkverkeer trends en snel een ongewone activiteit te herkennen.</span><span class="sxs-lookup"><span data-stu-id="ad170-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span></span> <span data-ttu-id="ad170-135">Enkele van deze functies worden weergegeven in de volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="ad170-135">A few of these features are shown in the following list:</span></span>

1. <span data-ttu-id="ad170-136">Stroom tabellen</span><span class="sxs-lookup"><span data-stu-id="ad170-136">Flow Tables</span></span>

    <span data-ttu-id="ad170-137">Deze tabel geeft de lijst met stromen in de pakketgegevens, de tijdstempel die is gekoppeld aan de stromen en de verschillende protocollen die zijn gekoppeld aan de stroom, evenals de bron en doel-IP.</span><span class="sxs-lookup"><span data-stu-id="ad170-137">This table gives you the list of flows in the packet data, the time stamp associated with the flows and the various protocols associated with the flow, as well as source and destination IP.</span></span>

    ![capanalysis stroom pagina][5]

1. <span data-ttu-id="ad170-139">Overzicht van Protocol</span><span class="sxs-lookup"><span data-stu-id="ad170-139">Protocol Overview</span></span>

    <span data-ttu-id="ad170-140">Dit deelvenster kunt u snel zien wat de distributie van netwerkverkeer via de verschillende protocollen en -locaties.</span><span class="sxs-lookup"><span data-stu-id="ad170-140">This pane allows you to quickly see the distribution of network traffic over the various protocols and geographies.</span></span>

    ![overzicht van capanalysis protocol][6]

1. <span data-ttu-id="ad170-142">statistieken</span><span class="sxs-lookup"><span data-stu-id="ad170-142">Statistics</span></span>

    <span data-ttu-id="ad170-143">Dit deelvenster kunt u weergeven netwerkverkeer statistics – bytes verzonden en ontvangen van de bron en doel-IP-adressen, stromen voor elk van de bron en doel-IP-adressen,-protocol gebruikt voor verschillende stromen en de duur van stromen.</span><span class="sxs-lookup"><span data-stu-id="ad170-143">This pane allows you to view network traffic statistics – bytes sent and received from source and destination IPs, flows for each of the source and destination IPs, protocol used for various flows, and the duration of flows.</span></span>

    ![capanalysis statistieken][7]

1. <span data-ttu-id="ad170-145">geomap</span><span class="sxs-lookup"><span data-stu-id="ad170-145">Geomap</span></span>

    <span data-ttu-id="ad170-146">Dit deelvenster bevat een overzichtsweergave van het netwerkverkeer met kleuren schalen van het volume van verkeer vanuit elk land.</span><span class="sxs-lookup"><span data-stu-id="ad170-146">This pane provides you with a map view of your network traffic, with colors scaling to the volume of traffic from each country.</span></span> <span data-ttu-id="ad170-147">Gemarkeerde landen extra stroom statistieken zoals het deel van de gegevens worden verzonden en ontvangen van IP-adressen in dat land weergeven, kunt u selecteren.</span><span class="sxs-lookup"><span data-stu-id="ad170-147">You can select highlighted countries to view additional flow statistics such as the proportion of data sent and received from IPs in that country.</span></span>

    ![geomap][8]

1. <span data-ttu-id="ad170-149">Filters</span><span class="sxs-lookup"><span data-stu-id="ad170-149">Filters</span></span>

    <span data-ttu-id="ad170-150">CapAnalysis biedt een set met filters voor snelle analyse van specifieke pakketten.</span><span class="sxs-lookup"><span data-stu-id="ad170-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span></span> <span data-ttu-id="ad170-151">U kunt bijvoorbeeld de gegevens filteren per protocol om specifieke inzicht in deze subset van verkeer te krijgen.</span><span class="sxs-lookup"><span data-stu-id="ad170-151">For example, you can choose to filter the data by protocol to gain specific insights on that subset of traffic.</span></span>

    ![filters][11]

    <span data-ttu-id="ad170-153">Ga naar [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) voor meer informatie over alle CapAnalysis mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="ad170-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) to learn more about all CapAnalysis' capabilities.</span></span>

## <a name="conclusion"></a><span data-ttu-id="ad170-154">Conclusie</span><span class="sxs-lookup"><span data-stu-id="ad170-154">Conclusion</span></span>

<span data-ttu-id="ad170-155">Netwerk-Watcher pakket vastleggen functie kunt u voor het vastleggen van de gegevens die nodig zijn om netwerk forensische uitvoeren en het netwerkverkeer beter te begrijpen.</span><span class="sxs-lookup"><span data-stu-id="ad170-155">Network Watcher’s packet capture feature allows you to capture the data necessary to perform network forensics and better understand your network traffic.</span></span> <span data-ttu-id="ad170-156">In dit scenario wordt beschreven hoe pakket schermopnamen van netwerk-Watcher eenvoudig worden geïntegreerd met open-source hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="ad170-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span></span> <span data-ttu-id="ad170-157">U kunt met open-source hulpprogramma's zoals CapAnalysis pakketten opnamen visualiseren, grondige pakketinspecties uitvoeren en snel trends te identificeren binnen het netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="ad170-157">By using open source tools such as CapAnalysis to visualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad170-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ad170-158">Next steps</span></span>

<span data-ttu-id="ad170-159">Ga voor meer informatie over het NSG stroom logboeken naar [stroom NSG-Logboeken](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ad170-159">To learn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span></span>

<span data-ttu-id="ad170-160">Meer informatie over het visualiseren van uw NSG stroom logboeken met Power BI in via [visualiseren NSG loopt logboeken met Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="ad170-160">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
