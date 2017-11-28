---
title: patronen in aaaVisualize het netwerkverkeer met Azure-netwerk-Watcher en open-source hulpprogramma's | Microsoft Docs
description: Deze pagina wordt beschreven hoe toouse netwerk-Watcher pakket vastleggen met Capanalysis toovisualize verkeer patronen tooand van uw virtuele machines.
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
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a><span data-ttu-id="7902e-103">Visualiseren netwerkverkeer patronen tooand van uw virtuele machines met open-source hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="7902e-103">Visualize network traffic patterns tooand from your VMs using open source tools</span></span>

<span data-ttu-id="7902e-104">Pakket opnamen bevatten gegevens van het netwerk waarmee u tooperform netwerk forensisch en grondige inspecties van pakketten.</span><span class="sxs-lookup"><span data-stu-id="7902e-104">Packet captures contain network data that allow you tooperform network forensics and deep packet inspection.</span></span> <span data-ttu-id="7902e-105">Er zijn veel wordt geopend, source hulpprogramma's kunt u tooanalyze pakket opnamen toogain inzicht te krijgen over uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="7902e-105">There are many opens source tools you can use tooanalyze packet captures toogain insights about your network.</span></span> <span data-ttu-id="7902e-106">Een van deze programma is CapAnalysis, een visualisatie pakket open-source hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="7902e-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span></span> <span data-ttu-id="7902e-107">Pakket vastleggen gegevens te visualiseren is een waardevolle manier tooquickly afgeleid insights op patronen en afwijkingen in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="7902e-107">Visualizing packet capture data is a valuable way tooquickly derive insights on patterns and anomalies within your network.</span></span> <span data-ttu-id="7902e-108">Visualisaties bieden ook een manier om dergelijke insights te delen op een manier eenvoudig worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7902e-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span></span>

<span data-ttu-id="7902e-109">Azure netwerk-Watcher biedt dat u de mogelijkheid toocapture deze waardevolle gegevens doordat u tooperform pakket vastgelegd Hallo in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="7902e-109">Azure’s Network Watcher provides you hello ability toocapture this valuable data by allowing you tooperform packet captures on your network.</span></span> <span data-ttu-id="7902e-110">We bieden een overzicht van hoe toovisualize en beter inzicht in het pakket worden vastgelegd met behulp van CapAnalysis met netwerk-Watcher in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="7902e-110">In this article, we provide a walkthrough of how toovisualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="7902e-111">Scenario</span><span class="sxs-lookup"><span data-stu-id="7902e-111">Scenario</span></span>

<span data-ttu-id="7902e-112">Hebt u een eenvoudige webtoepassing geïmplementeerd op een virtuele machine in Azure wilt toouse open-source hulpprogramma's voor toovisualize de netwerk-verkeer tooquickly stroom patronen en eventuele mogelijke afwijkingen identificeren.</span><span class="sxs-lookup"><span data-stu-id="7902e-112">You have a simple web application deployed on a VM in Azure want toouse open source tools toovisualize its network traffic tooquickly identify flow patterns and any possible anomalies.</span></span> <span data-ttu-id="7902e-113">U kunt met de netwerk-Watcher verkrijgen van een pakketopname van uw netwerkomgeving en bewaar deze rechtstreeks van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="7902e-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span></span> <span data-ttu-id="7902e-114">CapAnalysis kunt opnemen pakketopname van Hallo rechtstreeks van Hallo storage-blob en visualiseren van de inhoud ervan.</span><span class="sxs-lookup"><span data-stu-id="7902e-114">CapAnalysis can then ingest hello packet capture directly from hello storage blob and visualize its contents.</span></span>

![scenario][1]

## <a name="steps"></a><span data-ttu-id="7902e-116">Stappen</span><span class="sxs-lookup"><span data-stu-id="7902e-116">Steps</span></span>

### <a name="install-capanalysis"></a><span data-ttu-id="7902e-117">CapAnalysis installeren</span><span class="sxs-lookup"><span data-stu-id="7902e-117">Install CapAnalysis</span></span>

<span data-ttu-id="7902e-118">tooinstall CapAnalysis op een virtuele machine, raadpleegt u de officiële instructies toohello hier https://www.capanalysis.net/ca/how-to-install-capanalysis.</span><span class="sxs-lookup"><span data-stu-id="7902e-118">tooinstall CapAnalysis on a virtual machine, you can refer toohello official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span></span>
<span data-ttu-id="7902e-119">In volgorde extern toegang tot CapAnalysis, moeten we tooopen poort 9877 op de virtuele machine door een nieuwe beveiligingsregel voor binnenkomende toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="7902e-119">In order access CapAnalysis remotely, we need tooopen port 9877 on your VM by adding a new inbound security rule.</span></span> <span data-ttu-id="7902e-120">Voor meer informatie over het maken van regels in Netwerkbeveiligingsgroepen, Raadpleeg te[regels maken in een bestaande NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span><span class="sxs-lookup"><span data-stu-id="7902e-120">For more about creating rules in Network Security Groups, refer too[Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span></span> <span data-ttu-id="7902e-121">Zodra het Hallo-regel is toegevoegd, moet u kunnen tooaccess CapAnalysis uit`http://<PublicIP>:9877`</span><span class="sxs-lookup"><span data-stu-id="7902e-121">Once hello rule has been successfully added, you should be able tooaccess CapAnalysis from `http://<PublicIP>:9877`</span></span>

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a><span data-ttu-id="7902e-122">Azure-netwerk-Watcher toostart een pakket vastleggen sessie gebruiken</span><span class="sxs-lookup"><span data-stu-id="7902e-122">Use Azure Network Watcher toostart a packet capture session</span></span>

<span data-ttu-id="7902e-123">Netwerk-Watcher kunt u toocapture pakketten tootrack binnenkomend en uitgaand verkeer een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7902e-123">Network Watcher allows you toocapture packets tootrack traffic in and out of a virtual machine.</span></span> <span data-ttu-id="7902e-124">U kunt verwijzen toohello instructies op de [beheren pakket worden vastgelegd met de netwerk-Watcher](network-watcher-packet-capture-manage-portal.md) toostart een pakket vastleggen sessie.</span><span class="sxs-lookup"><span data-stu-id="7902e-124">You can refer toohello instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) toostart a packet capture session.</span></span> <span data-ttu-id="7902e-125">Deze pakketopname kan worden opgeslagen in een opslag-blob toobe toegankelijk is voor CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="7902e-125">This packet capture can be stored in a storage blob toobe accessed by CapAnalysis.</span></span>

### <a name="upload-a-packet-capture-toocapanalysis"></a><span data-ttu-id="7902e-126">Uploaden van een pakket vastleggen tooCapAnalysis</span><span class="sxs-lookup"><span data-stu-id="7902e-126">Upload a packet capture tooCapAnalysis</span></span>
<span data-ttu-id="7902e-127">U kunt rechtstreeks uploaden een pakketopname die door de netwerk-watcher Hallo 'Importeren van URL' tabblad en het geven van een koppeling toohello storage-blob waar Hallo pakketopname wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7902e-127">You can directly upload a packet capture taken by network watcher using hello “Import from URL” tab and providing a link toohello storage blob where hello packet capture is stored.</span></span>

<span data-ttu-id="7902e-128">Wanneer een koppeling tooCapAnalysis biedt, zorg ervoor dat tooappend een SAS-token toohello storage blob-URL.</span><span class="sxs-lookup"><span data-stu-id="7902e-128">When providing a link tooCapAnalysis, make sure tooappend a SAS token toohello storage blob URL.</span></span>  <span data-ttu-id="7902e-129">toodo, tooShared toegangshandtekening van het opslagaccount Hallo navigeren, Hallo toegestane machtigingen toewijzen en druk op Hallo SAS genereren knop toocreate een token.</span><span class="sxs-lookup"><span data-stu-id="7902e-129">toodo this, navigate tooShared access signature from hello storage account, designate hello allowed permissions, and press hello Generate SAS button toocreate a token.</span></span> <span data-ttu-id="7902e-130">Vervolgens kunt u deze SAS-token toohello pakket vastleggen opslag blob-URL toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7902e-130">You can then append this SAS token toohello packet capture storage blob URL.</span></span>

<span data-ttu-id="7902e-131">Hallo resulterende URL ziet er ongeveer als volgt: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span><span class="sxs-lookup"><span data-stu-id="7902e-131">hello resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span></span>


### <a name="analyzing-packet-captures"></a><span data-ttu-id="7902e-132">Analyseren van pakket worden vastgelegd</span><span class="sxs-lookup"><span data-stu-id="7902e-132">Analyzing packet captures</span></span>

<span data-ttu-id="7902e-133">CapAnalysis biedt verschillende opties toovisualize uw pakketopname, elke verstrekken analyse vanuit een ander perspectief.</span><span class="sxs-lookup"><span data-stu-id="7902e-133">CapAnalysis offers various options toovisualize your packet capture, each providing analysis from a different perspective.</span></span> <span data-ttu-id="7902e-134">U kunt met deze visual samenvattingen inzicht in uw netwerkverkeer trends en snel een ongewone activiteit te herkennen.</span><span class="sxs-lookup"><span data-stu-id="7902e-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span></span> <span data-ttu-id="7902e-135">Enkele van deze functies worden weergegeven in Hallo volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="7902e-135">A few of these features are shown in hello following list:</span></span>

1. <span data-ttu-id="7902e-136">Stroom tabellen</span><span class="sxs-lookup"><span data-stu-id="7902e-136">Flow Tables</span></span>

    <span data-ttu-id="7902e-137">Deze tabel geeft u lijst met stromen in pakketgegevens Hallo Hallo, Hallo tijdstempel Hallo stromen gekoppeld en Hallo van verschillende protocollen die zijn gekoppeld aan het Hallo-stroom, evenals de IP-bron- en doelserver.</span><span class="sxs-lookup"><span data-stu-id="7902e-137">This table gives you hello list of flows in hello packet data, hello time stamp associated with hello flows and hello various protocols associated with hello flow, as well as source and destination IP.</span></span>

    ![capanalysis stroom pagina][5]

1. <span data-ttu-id="7902e-139">Overzicht van Protocol</span><span class="sxs-lookup"><span data-stu-id="7902e-139">Protocol Overview</span></span>

    <span data-ttu-id="7902e-140">Dit deelvenster kunt u tooquickly Zie Hallo distributie van netwerkverkeer via Hallo verschillende protocollen en -locaties.</span><span class="sxs-lookup"><span data-stu-id="7902e-140">This pane allows you tooquickly see hello distribution of network traffic over hello various protocols and geographies.</span></span>

    ![overzicht van capanalysis protocol][6]

1. <span data-ttu-id="7902e-142">statistieken</span><span class="sxs-lookup"><span data-stu-id="7902e-142">Statistics</span></span>

    <span data-ttu-id="7902e-143">Dit deelvenster kunt u tooview netwerkverkeer statistics – bytes verzonden en ontvangen van de bron en doel-IP-adressen, stromen voor elk van de Hallo bron en doel-IP-adressen,-protocol gebruikt voor verschillende stromen en Hallo duur van stromen.</span><span class="sxs-lookup"><span data-stu-id="7902e-143">This pane allows you tooview network traffic statistics – bytes sent and received from source and destination IPs, flows for each of hello source and destination IPs, protocol used for various flows, and hello duration of flows.</span></span>

    ![capanalysis statistieken][7]

1. <span data-ttu-id="7902e-145">geomap</span><span class="sxs-lookup"><span data-stu-id="7902e-145">Geomap</span></span>

    <span data-ttu-id="7902e-146">Dit deelvenster biedt u een overzichtsweergave van het netwerkverkeer met kleuren toohello hoeveelheid verkeer vanuit elk land schalen.</span><span class="sxs-lookup"><span data-stu-id="7902e-146">This pane provides you with a map view of your network traffic, with colors scaling toohello volume of traffic from each country.</span></span> <span data-ttu-id="7902e-147">U kunt gemarkeerde landen tooview extra stroom statistieken zoals Hallo deel van de gegevens worden verzonden en ontvangen van IP-adressen in dat land selecteren.</span><span class="sxs-lookup"><span data-stu-id="7902e-147">You can select highlighted countries tooview additional flow statistics such as hello proportion of data sent and received from IPs in that country.</span></span>

    ![geomap][8]

1. <span data-ttu-id="7902e-149">Filters</span><span class="sxs-lookup"><span data-stu-id="7902e-149">Filters</span></span>

    <span data-ttu-id="7902e-150">CapAnalysis biedt een set met filters voor snelle analyse van specifieke pakketten.</span><span class="sxs-lookup"><span data-stu-id="7902e-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span></span> <span data-ttu-id="7902e-151">U kunt bijvoorbeeld toofilter Hallo gegevens door protocol toogain specifieke insights op deze subset van verkeer.</span><span class="sxs-lookup"><span data-stu-id="7902e-151">For example, you can choose toofilter hello data by protocol toogain specific insights on that subset of traffic.</span></span>

    ![filters][11]

    <span data-ttu-id="7902e-153">Ga naar [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn meer over de mogelijkheden van alle CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="7902e-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn more about all CapAnalysis' capabilities.</span></span>

## <a name="conclusion"></a><span data-ttu-id="7902e-154">Conclusie</span><span class="sxs-lookup"><span data-stu-id="7902e-154">Conclusion</span></span>

<span data-ttu-id="7902e-155">Netwerk-Watcher pakket vastleggen functie kunt u toocapture Hallo gegevens nodig tooperform netwerk forensische en het netwerkverkeer beter te begrijpen.</span><span class="sxs-lookup"><span data-stu-id="7902e-155">Network Watcher’s packet capture feature allows you toocapture hello data necessary tooperform network forensics and better understand your network traffic.</span></span> <span data-ttu-id="7902e-156">In dit scenario wordt beschreven hoe pakket schermopnamen van netwerk-Watcher eenvoudig worden geïntegreerd met open-source hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="7902e-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span></span> <span data-ttu-id="7902e-157">U kunt met open-source hulpprogramma's zoals CapAnalysis toovisualize pakketten worden vastgelegd, grondige pakketinspecties uitvoeren en snel trends te identificeren binnen het netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="7902e-157">By using open source tools such as CapAnalysis toovisualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7902e-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7902e-158">Next steps</span></span>

<span data-ttu-id="7902e-159">toolearn meer informatie over het NSG-logboeken stroom, gaat u naar [stroom NSG-Logboeken](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7902e-159">toolearn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span></span>

<span data-ttu-id="7902e-160">Meer informatie over hoe toovisualize uw NSG-flow registreert met Power BI in via [visualiseren NSG loopt logboeken met Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="7902e-160">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>
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
