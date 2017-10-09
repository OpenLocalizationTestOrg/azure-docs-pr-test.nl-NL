---
title: aaaVisualizing Netwerkbeveiligingsgroep Azure stroom logboeken met Power BI | Microsoft Docs
description: Deze pagina wordt beschreven hoe toovisualize NSG stroom registreert met Power BI.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a><span data-ttu-id="0f263-103">Netwerkbeveiligingsgroep visualizing stroom logboeken met Power BI</span><span class="sxs-lookup"><span data-stu-id="0f263-103">Visualizing Network Security Group flow logs with Power BI</span></span>

<span data-ttu-id="0f263-104">Netwerkbeveiligingsgroep stroom logboeken toestaan tooview informatie over inkomende en uitgaande IP-verkeer op Netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="0f263-104">Network Security Group flow logs allow you tooview information about ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="0f263-105">Deze stroom logboeken weergeven uitgaande en inkomende stromen per regel op basis van een Hallo NIC Hallo stroom is van toepassing op 5-tuple informatie over het Hallo-stroom (IP bron/het doel, bron/het doel-poort Protocol) en als Hallo verkeer is toegestaan of geweigerd.</span><span class="sxs-lookup"><span data-stu-id="0f263-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="0f263-106">Het kan lastig toogain inzicht in de logboekregistratie van gegevens door te zoeken handmatig logboekbestanden Hallo stroom zijn.</span><span class="sxs-lookup"><span data-stu-id="0f263-106">It can be difficult toogain insights into flow logging data by manually searching hello log files.</span></span> <span data-ttu-id="0f263-107">In dit artikel bieden we een oplossing toovisualize uw meest recente flow logboeken en meer informatie over verkeer op uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="0f263-107">In this article, we provide a solution toovisualize your most recent flow logs and learn about traffic on your network.</span></span>

## <a name="scenario"></a><span data-ttu-id="0f263-108">Scenario</span><span class="sxs-lookup"><span data-stu-id="0f263-108">Scenario</span></span>

<span data-ttu-id="0f263-109">We verbinding Power BI desktop toohello storage-account die we voor onze gegevens NSG stromen logboekregistratie hebt geconfigureerd als sink Hallo Hallo scenario te volgen, maken.</span><span class="sxs-lookup"><span data-stu-id="0f263-109">In hello following scenario, we connect Power BI desktop toohello storage account we have configured as hello sink for our NSG Flow Logging data.</span></span> <span data-ttu-id="0f263-110">Nadat we tooour storage-account verbinding hebt gemaakt, wordt in Power BI downloadt en parseert Hallo logboeken tooprovide een visuele representatie van het Hallo-verkeer dat is vastgelegd door netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="0f263-110">After we connect tooour storage account, Power BI downloads and parses hello logs tooprovide a visual representation of hello traffic that is logged by Network Security groups.</span></span>

<span data-ttu-id="0f263-111">Met behulp van Hallo visuele elementen die zijn opgegeven in het Hallo-sjabloon die u kunt controleren:</span><span class="sxs-lookup"><span data-stu-id="0f263-111">Using hello visuals supplied in hello template you can examine:</span></span>

* <span data-ttu-id="0f263-112">Bovenste Talkers</span><span class="sxs-lookup"><span data-stu-id="0f263-112">Top Talkers</span></span>
* <span data-ttu-id="0f263-113">Tijd stromen reeksgegevens richting en regel beschikking</span><span class="sxs-lookup"><span data-stu-id="0f263-113">Time Series Flow Data by direction and rule decision</span></span>
* <span data-ttu-id="0f263-114">Stromen door Network Interface-MAC-adres</span><span class="sxs-lookup"><span data-stu-id="0f263-114">Flows by Network Interface MAC address</span></span>
* <span data-ttu-id="0f263-115">Stromen door het NSG en de regel</span><span class="sxs-lookup"><span data-stu-id="0f263-115">Flows by NSG and Rule</span></span>
* <span data-ttu-id="0f263-116">Stromen door doelpoort</span><span class="sxs-lookup"><span data-stu-id="0f263-116">Flows by Destination Port</span></span>

<span data-ttu-id="0f263-117">Hallo sjabloon kan worden bewerkt zodat u kunt deze nieuwe gegevens tooadd, visuele elementen, wijzigen of bewerken van query's toosuit uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="0f263-117">hello template provided is editable so you can modify it tooadd new data, visuals, or edit queries toosuit your needs.</span></span>

## <a name="setup"></a><span data-ttu-id="0f263-118">Instellen</span><span class="sxs-lookup"><span data-stu-id="0f263-118">Setup</span></span>

<span data-ttu-id="0f263-119">Voordat u begint, kunt u Network Security groep stromen-logboekregistratie is ingeschakeld op een of meer Netwerkbeveiligingsgroepen in uw account moet hebben.</span><span class="sxs-lookup"><span data-stu-id="0f263-119">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="0f263-120">Voor instructies over het inschakelen van netwerkbeveiliging stromen Logboeken, raadpleeg dan toohello volgende artikel: [inleiding tooflow logboekregistratie voor Netwerkbeveiligingsgroepen](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0f263-120">For instructions on enabling Network Security flow logs, refer toohello following article: [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="0f263-121">U moet ook Hallo Power BI Desktop client is geïnstalleerd op uw computer en genoeg ruimte vrij op uw machine toodownload en de belasting Hallo logboekgegevens die in uw storage-account voorkomt hebben.</span><span class="sxs-lookup"><span data-stu-id="0f263-121">You must also have hello Power BI Desktop client installed on your machine, and enough free space on your machine toodownload and load hello log data that exists in your storage account.</span></span>

![Visio-diagram][1]

### <a name="steps"></a><span data-ttu-id="0f263-123">Stappen</span><span class="sxs-lookup"><span data-stu-id="0f263-123">Steps</span></span>

1. <span data-ttu-id="0f263-124">De download- en open Hallo volgende van Power BI-sjabloon in Power BI Desktop toepassing hello [netwerk-Watcher Power BI-stroom logboeken sjabloon](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span><span class="sxs-lookup"><span data-stu-id="0f263-124">Download and open hello following Power BI template in hello Power BI Desktop Application [Network Watcher PowerBI flow logs template](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span></span>
1. <span data-ttu-id="0f263-125">Voer de queryparameters Hallo vereist</span><span class="sxs-lookup"><span data-stu-id="0f263-125">Enter hello required Query parameters</span></span>
    1. <span data-ttu-id="0f263-126">**StorageAccountName** – geeft toohello naam van Hallo storage-account met Hallo NSG stroom logboeken die u wilt tooload en visualiseren.</span><span class="sxs-lookup"><span data-stu-id="0f263-126">**StorageAccountName** – Specifies toohello name of hello storage account containing hello NSG flow logs that you would like tooload and visualize.</span></span>
    1. <span data-ttu-id="0f263-127">**NumberOfLogFiles** – Hiermee geeft u het aantal logboekbestanden dat u wilt toodownload en in Power BI visualiseren Hallo.</span><span class="sxs-lookup"><span data-stu-id="0f263-127">**NumberOfLogFiles** – Specifies hello number of log files that you would like toodownload and visualize in Power BI.</span></span> <span data-ttu-id="0f263-128">Bijvoorbeeld, als 50 is opgegeven, Hallo 50 meest recente logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="0f263-128">For example, if 50 is specified, hello 50 latest log files.</span></span> <span data-ttu-id="0f263-129">FF hebben we 2 nsg's ingeschakeld en geconfigureerd toosend NSG stroom logboeken toothis account vervolgens hello afgelopen 25 uur aan logbestanden kunnen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0f263-129">Ff we have 2 NSGs enabled and configured toosend NSG flow logs toothis account, then hello past 25 hours of logs can be viewed.</span></span>

    ![Power BI main][2]

1. <span data-ttu-id="0f263-131">Voer Hallo toegangssleutel voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="0f263-131">Enter hello Access Key for your storage account.</span></span> <span data-ttu-id="0f263-132">U kunt geldig toegangstoetsen vinden door te navigeren tooyour storage-account in hello Azure portal en selecteert **toegangstoetsen** in Hallo-instellingen.</span><span class="sxs-lookup"><span data-stu-id="0f263-132">You can find valid access keys by navigating tooyour storage account in hello Azure portal and selecting **Access Keys** from hello Settings menu.</span></span> <span data-ttu-id="0f263-133">Klik op **Connect** past u wijzigingen toe.</span><span class="sxs-lookup"><span data-stu-id="0f263-133">Click **Connect** then apply changes.</span></span>

    ![Toegangstoetsen][3]

    ![toegangssleutel 2][4]

4.  <span data-ttu-id="0f263-136">Uw logboeken worden gedownload en geparseerd en kunt u nu gebruikmaken van vooraf gemaakte visuele elementen Hallo.</span><span class="sxs-lookup"><span data-stu-id="0f263-136">Your logs are download and parsed and you can now utilize hello pre-created visuals.</span></span>

## <a name="understanding-hello-visuals"></a><span data-ttu-id="0f263-137">Understanding Hallo visuele elementen</span><span class="sxs-lookup"><span data-stu-id="0f263-137">Understanding hello visuals</span></span>

<span data-ttu-id="0f263-138">Opgegeven in Hallo sjabloon zijn een set van visuele elementen waarmee logisch Hallo NSG stromen logboekgegevens.</span><span class="sxs-lookup"><span data-stu-id="0f263-138">Provided in hello template are a set of visuals that help make sense of hello NSG Flow Log data.</span></span> <span data-ttu-id="0f263-139">Hallo volgende afbeeldingen ziet u een voorbeeld van welke dashboard Hallo eruit wanneer gevuld met gegevens.</span><span class="sxs-lookup"><span data-stu-id="0f263-139">hello following images show a sample of what hello dashboard looks like when populated with data.</span></span> <span data-ttu-id="0f263-140">Hieronder wordt elke visual met meer details onderzoeken</span><span class="sxs-lookup"><span data-stu-id="0f263-140">Below we examine each visual in greater detail</span></span> 

![Power BI][5]
 
<span data-ttu-id="0f263-142">Hallo boven Talkers visual toont Hallo IP-adressen die zijn geïnitieerd Hallo meeste verbindingen via Hallo opgegeven periode.</span><span class="sxs-lookup"><span data-stu-id="0f263-142">hello Top Talkers visual shows hello IPs that have initiated hello most connections over hello period specified.</span></span> <span data-ttu-id="0f263-143">Hallo-grootte van de vakken Hallo komt overeen toohello relatieve aantal verbindingen.</span><span class="sxs-lookup"><span data-stu-id="0f263-143">hello size of hello boxes corresponds toohello relative number of connections.</span></span> 

![toptalkers][6]

<span data-ttu-id="0f263-145">Hallo weergeven volgende time series-grafieken Hallo aantal overdrachten Hallo periode.</span><span class="sxs-lookup"><span data-stu-id="0f263-145">hello following time series graphs show hello number of flows over hello period.</span></span> <span data-ttu-id="0f263-146">Hallo bovenste grafiek wordt gesegmenteerd op Hallo stroomrichting en lagere hello wordt gesegmenteerd op Hallo beslissingen (toestaan of weigeren).</span><span class="sxs-lookup"><span data-stu-id="0f263-146">hello upper graph is segmented by hello flow direction, and hello lower is segmented by hello decision made (allow or deny).</span></span> <span data-ttu-id="0f263-147">Met dit visuele element, kunt u onderzoeken van uw verkeer trends na verloop van tijd en eventuele abnormale pieken herkennen of daling van verkeer of verkeer segmentering.</span><span class="sxs-lookup"><span data-stu-id="0f263-147">With this visual, you can examine your traffic trends over time, and spot any abnormal spikes or decline in traffic or traffic segmentation.</span></span>

![flowsoverperiod][7]

<span data-ttu-id="0f263-149">Hallo volgende grafieken wordt aangegeven Hallo stromen per netwerkinterface met Hallo bovenste gesegmenteerd op stroomrichting en Hallo lagere gesegmenteerd op beslissingen.</span><span class="sxs-lookup"><span data-stu-id="0f263-149">hello following graphs show hello flows per Network interface, with hello upper segmented by flow direction and hello lower segmented by decision made.</span></span> <span data-ttu-id="0f263-150">Met deze informatie krijgt u inzicht in welke van uw virtuele machines gecommuniceerd meeste relatieve tooothers hello, en als verkeer tooa specifieke virtuele machine wordt toegestaan of geweigerd.</span><span class="sxs-lookup"><span data-stu-id="0f263-150">With this information, you can gain insights into which of your VMs communicated hello most relative tooothers, and if traffic tooa specific VM is being allowed or denied.</span></span>

![flowspernic][8]

<span data-ttu-id="0f263-152">Hallo na ring wheel-grafiek kunt een uitsplitsing van stromen door doelpoort.</span><span class="sxs-lookup"><span data-stu-id="0f263-152">hello following donut wheel chart shows a breakdown of Flows by Destination Port.</span></span> <span data-ttu-id="0f263-153">Met deze informatie vindt u Hallo meest gebruikte doelpoorten gebruikt binnen Hallo opgegeven periode.</span><span class="sxs-lookup"><span data-stu-id="0f263-153">With this information, you can view hello most commonly used destination ports used within hello specified period.</span></span>

![Ring][9]

<span data-ttu-id="0f263-155">Hallo ziet volgende staafdiagram Hallo stroom door het NSG en de regel.</span><span class="sxs-lookup"><span data-stu-id="0f263-155">hello following bar chart shows hello Flow by NSG and Rule.</span></span> <span data-ttu-id="0f263-156">Met deze informatie ziet u nsg's die verantwoordelijk is voor Hallo Hallo meeste verkeer en Hallo uitsplitsing van verkeer op een NSG door regel.</span><span class="sxs-lookup"><span data-stu-id="0f263-156">With this information, you can see hello NSGs responsible for hello most traffic, and hello breakdown of traffic on an NSG by rule.</span></span>

![barchart][10]
 
<span data-ttu-id="0f263-158">Hallo volgende informatief grafieken weergave-informatie over Nsg Hallo aanwezig is in Logboeken hello, Hallo aantal overdrachten vastgelegd via hello, en -datum Hallo van Hallo vroegste logboek vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="0f263-158">hello following informational charts display information about hello NSGs present in hello logs, hello number of Flows captured over hello period, and hello date of hello earliest log captured.</span></span> <span data-ttu-id="0f263-159">Deze informatie kunt u een idee van welke nsg's worden vastgelegd en Hallo datumbereik van stromen.</span><span class="sxs-lookup"><span data-stu-id="0f263-159">This information gives you an idea of what NSGs are being logged and hello date range of flows.</span></span>

![infochart1][11]

![infochart2][12]

<span data-ttu-id="0f263-162">Deze sjabloon bevat Hallo volgende slicers tooallow u tooview enige Hallo gegevens u meest geïnteresseerd bent in.</span><span class="sxs-lookup"><span data-stu-id="0f263-162">This template includes hello following slicers tooallow you tooview only hello data you are most interested in.</span></span> <span data-ttu-id="0f263-163">U kunt filteren op uw resourcegroepen, nsg's en regels.</span><span class="sxs-lookup"><span data-stu-id="0f263-163">You can filter on your resource groups, NSGs, and rules.</span></span> <span data-ttu-id="0f263-164">U kunt ook filteren op 5-tuple informatie, besluit en Hallo tijd Hallo-logboek is geschreven.</span><span class="sxs-lookup"><span data-stu-id="0f263-164">You can also filter on 5-tuple information, decision, and hello time hello log was written.</span></span>

![slicers][13]

## <a name="conclusion"></a><span data-ttu-id="0f263-166">Conclusie</span><span class="sxs-lookup"><span data-stu-id="0f263-166">Conclusion</span></span>

<span data-ttu-id="0f263-167">We bleek in dit scenario dat via het netwerk beveiliging groep overgebracht logboeken die worden geleverd door Power BI en netwerk-Watcher we kunnen toovisualize en Hallo-verkeer begrijpen.</span><span class="sxs-lookup"><span data-stu-id="0f263-167">We showed in this scenario that by using Network Security Group Flow logs provided by Network Watcher and Power BI, we are able toovisualize and understand hello traffic.</span></span> <span data-ttu-id="0f263-168">Met behulp van de sjabloon Hallo opgegeven Power BI Hallo logboeken rechtstreeks uit storage downloadt en verwerkt deze lokaal.</span><span class="sxs-lookup"><span data-stu-id="0f263-168">Using hello provided template, Power BI downloads hello logs directly from storage and processes them locally.</span></span> <span data-ttu-id="0f263-169">Gebruikte tijd tooload Hallo sjabloon varieert al naar gelang het aantal bestanden die zijn aangevraagd Hallo en totale grootte van bestanden worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="0f263-169">Time taken tooload hello template varies depending on hello number of files requested and total size of files downloaded.</span></span>

<span data-ttu-id="0f263-170">U kunt gratis toocustomize deze sjabloon voor uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="0f263-170">Feel free toocustomize this template for your needs.</span></span> <span data-ttu-id="0f263-171">Er zijn veel verschillende manieren u Power BI kunt gebruiken met het netwerk groep stromen beveiligingslogboeken.</span><span class="sxs-lookup"><span data-stu-id="0f263-171">There are many numerous ways that you can use Power BI with Network Security Group Flow Logs.</span></span> 

## <a name="notes"></a><span data-ttu-id="0f263-172">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="0f263-172">Notes</span></span>

* <span data-ttu-id="0f263-173">Logboeken standaard worden opgeslagen in`https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span><span class="sxs-lookup"><span data-stu-id="0f263-173">Logs by default are stored in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span></span>

    * <span data-ttu-id="0f263-174">Als andere gegevens in een andere directory bestaat deze query's toopull Hallo en proces Hallo gegevens moeten worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="0f263-174">If other data exists in another directory they hello queries toopull and process hello data must be modified.</span></span>

* <span data-ttu-id="0f263-175">Hallo opgegeven sjabloon wordt niet aanbevolen voor gebruik met meer dan 1 GB van Logboeken.</span><span class="sxs-lookup"><span data-stu-id="0f263-175">hello provided template is not recommended for use with more than 1 GB of logs.</span></span>

* <span data-ttu-id="0f263-176">Als u een grote hoeveelheid Logboeken hebt, raden wij onderzoeken van een oplossing met behulp van een ander gegevensarchief zoals Data Lake of SQL server.</span><span class="sxs-lookup"><span data-stu-id="0f263-176">If you have a large amount of logs, we recommend that you investigate a solution using another data store like Data Lake or SQL server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f263-177">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0f263-177">Next Steps</span></span>

<span data-ttu-id="0f263-178">Meer informatie over hoe toovisualize uw NSG-flow registreert Hello Elastick Stack in via [visualiseren netwerkverkeer patronen tooand van uw virtuele machines met open-source hulpprogramma's](network-watcher-using-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="0f263-178">Learn how toovisualize your NSG flow logs with hello Elastick Stack by visiting [Visualize network traffic patterns tooand from your VMs using open source tools](network-watcher-using-open-source-tools.md)</span></span>

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
