---
title: aaaTroubleshooting en bewaking van SAP HANA in Azure (grote exemplaren) | Microsoft Docs
description: Problemen oplossen en SAP HANA op een Azure (grote exemplaren) bewaken.
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1f1cd35820e227fd99af495431cd4b826aa53600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a><span data-ttu-id="b46b1-103">Hoe tootroubleshoot en monitor SAP HANA (grote exemplaren) in Azure</span><span class="sxs-lookup"><span data-stu-id="b46b1-103">How tootroubleshoot and monitor SAP HANA (large instances) on Azure</span></span>


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="b46b1-104">Bewaking in SAP HANA in Azure (grote exemplaren)</span><span class="sxs-lookup"><span data-stu-id="b46b1-104">Monitoring in SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="b46b1-105">SAP HANA in Azure (grote exemplaren) gaat niet anders andere IaaS-implementatie, moet u toomonitor wat OS Hallo en toepassing hello is doen en hoe deze Hallo resources volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b46b1-105">SAP HANA on Azure (Large Instances) is no different from any other IaaS deployment — you need toomonitor what hello OS and hello application is doing and how these consume hello following resources:</span></span>

- <span data-ttu-id="b46b1-106">CPU</span><span class="sxs-lookup"><span data-stu-id="b46b1-106">CPU</span></span>
- <span data-ttu-id="b46b1-107">Geheugen</span><span class="sxs-lookup"><span data-stu-id="b46b1-107">Memory</span></span>
- <span data-ttu-id="b46b1-108">Netwerkbandbreedte</span><span class="sxs-lookup"><span data-stu-id="b46b1-108">Network bandwidth</span></span>
- <span data-ttu-id="b46b1-109">Schijfruimte</span><span class="sxs-lookup"><span data-stu-id="b46b1-109">Disk space</span></span>

<span data-ttu-id="b46b1-110">Als u met Azure Virtual Machines, moet u toofigure uit of Hallo resource klassen hierboven genoemde voldoende of deze ophalen of leeg.</span><span class="sxs-lookup"><span data-stu-id="b46b1-110">As with Azure Virtual Machines you need toofigure out whether hello resource classes named above are sufficient, or whether these get depleted.</span></span> <span data-ttu-id="b46b1-111">Hieronder vindt u meer details op elk van de verschillende klassen Hallo:</span><span class="sxs-lookup"><span data-stu-id="b46b1-111">Here is more detail on each of hello different classes:</span></span>

<span data-ttu-id="b46b1-112">**Resource-CPU-verbruik:** Hallo verhouding die SAP gedefinieerd voor bepaalde werkbelasting tegen HANA is afgedwongen toomake ervoor dat er voldoende bronnen CPU toowork beschikbaar via het Hallo-gegevens die zijn opgeslagen in het geheugen moet zijn.</span><span class="sxs-lookup"><span data-stu-id="b46b1-112">**CPU resource consumption:** hello ratio that SAP defined for certain workload against HANA is enforced toomake sure that there should be enough CPU resources available toowork through hello data that is stored in memory.</span></span> <span data-ttu-id="b46b1-113">Niettemin, kunnen er gevallen waarbij HANA verbruikt veel CPU uitvoeren van query's vanwege toomissing indexen of vergelijkbare problemen.</span><span class="sxs-lookup"><span data-stu-id="b46b1-113">Nevertheless, there might be cases where HANA consumes a lot of CPU executing queries due toomissing indexes or similar issues.</span></span> <span data-ttu-id="b46b1-114">Dit betekent dat, moet u CPU-resourceverbruik Hallo HANA grote exemplaar eenheid, evenals de CPU-resources verbruikt door services voor specifieke HANA Hallo van controleren.</span><span class="sxs-lookup"><span data-stu-id="b46b1-114">This means you should monitor CPU resource consumption of hello HANA large instance unit as well as CPU resources consumed by hello specific HANA services.</span></span>

<span data-ttu-id="b46b1-115">**Geheugengebruik:** belangrijke toomonitor uit binnen HANA, evenals buiten HANA op Hallo-eenheid Is.</span><span class="sxs-lookup"><span data-stu-id="b46b1-115">**Memory consumption:** Is important toomonitor from within HANA, as well as outside of HANA on hello unit.</span></span> <span data-ttu-id="b46b1-116">Binnen HANA, controleren hoe de gegevens Hallo toegewezen geheugen in volgorde toostay binnen Hallo vereist het formaat van de richtlijnen van SAP HANA verbruikt.</span><span class="sxs-lookup"><span data-stu-id="b46b1-116">Within HANA, monitor how hello data is consuming HANA allocated memory in order toostay within hello required sizing guidelines of SAP.</span></span> <span data-ttu-id="b46b1-117">U wilt ook toomonitor geheugenverbruik op Hallo grote exemplaar niveau toomake ervoor dat aanvullende geïnstalleerde niet-HANA software niet te veel geheugen in beslag nemen, en daarom met HANA voor geheugen concurreren.</span><span class="sxs-lookup"><span data-stu-id="b46b1-117">You also want toomonitor memory consumption on hello Large Instance level toomake sure that additional installed non-HANA software does not consume too much memory, and therefore compete with HANA for memory.</span></span>

<span data-ttu-id="b46b1-118">**De netwerkbandbreedte:** hello Azure VNet gateway beperkt is in de bandbreedte van gegevens naar hello Azure VNet te verplaatsen, dus is het handig toomonitor Hallo gegevens zijn ontvangen door alle Azure VM's binnen een VNet toofigure nagaan hoe sluit u toohello grenzen van hello Azure Hallo gateway-SKU die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="b46b1-118">**Network bandwidth:** hello Azure VNet gateway is limited in bandwidth of data moving into hello Azure VNet, so it is helpful toomonitor hello data received by all hello Azure VMs within a VNet toofigure out how close you are toohello limits of hello Azure gateway SKU you selected.</span></span> <span data-ttu-id="b46b1-119">Op Hallo HANA grote exemplaar eenheid maakt deze zin toomonitor binnenkomende en uitgaande netwerkverkeer ook en tookeep bijhouden van Hallo volumes die gedurende een periode worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="b46b1-119">On hello HANA Large Instance unit, it does make sense toomonitor incoming and outgoing network traffic as well, and tookeep track of hello volumes that are handled over time.</span></span>

<span data-ttu-id="b46b1-120">**Schijfruimte:** verbruik van schijfruimte wordt meestal verhoogd gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="b46b1-120">**Disk space:** Disk space consumption usually increases over time.</span></span> <span data-ttu-id="b46b1-121">Er zijn diverse redenen hiervoor, maar de meeste van alle zijn: gegevensvolume toeneemt, neemt de uitvoering van transactielogboeken, traceringsbestanden opslaan en uitvoeren van opslag-momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="b46b1-121">There are many reasons for this, but most of all are: data volume increases, execution of transaction log backups, storing trace files, and performing storage snapshots.</span></span> <span data-ttu-id="b46b1-122">Daarom is belangrijk toomonitor schijfruimtegebruik en Hallo schijfruimte die is gekoppeld aan Hallo HANA grote exemplaar eenheid beheren.</span><span class="sxs-lookup"><span data-stu-id="b46b1-122">Therefore, it is important toomonitor disk space usage and manage hello disk space associated with hello HANA Large Instance unit.</span></span>

## <a name="monitoring-and-troubleshooting-from-hana-side"></a><span data-ttu-id="b46b1-123">Bewaking en probleemoplossing van HANA kant</span><span class="sxs-lookup"><span data-stu-id="b46b1-123">Monitoring and troubleshooting from HANA side</span></span>

<span data-ttu-id="b46b1-124">In de volgorde tooeffectively analyseren problemen gerelateerde tooSAP HANA in Azure (grote exemplaren), is het nuttig toonarrow omlaag Hallo hoofdoorzaak van een probleem.</span><span class="sxs-lookup"><span data-stu-id="b46b1-124">In order tooeffectively analyze problems related tooSAP HANA on Azure (Large Instances), it is useful toonarrow down hello root cause of a problem.</span></span> <span data-ttu-id="b46b1-125">SAP heeft een grote hoeveelheid documentatie toohelp gepubliceerd u.</span><span class="sxs-lookup"><span data-stu-id="b46b1-125">SAP has published a large amount of documentation toohelp you.</span></span>

<span data-ttu-id="b46b1-126">Toepasselijke Veelgestelde vragen over verwante tooSAP HANA prestaties vindt u in de volgende opmerkingen bij de SAP Hallo:</span><span class="sxs-lookup"><span data-stu-id="b46b1-126">Applicable FAQs related tooSAP HANA performance can be found in hello following SAP Notes:</span></span>

- [<span data-ttu-id="b46b1-127">SAP-notitie #2222200: veelgestelde vragen over: SAP HANA-netwerk</span><span class="sxs-lookup"><span data-stu-id="b46b1-127">SAP Note #2222200 – FAQ: SAP HANA Network</span></span>](https://launchpad.support.sap.com/#/notes/2222200)
- [<span data-ttu-id="b46b1-128">SAP-notitie #2100040: veelgestelde vragen over: SAP HANA CPU</span><span class="sxs-lookup"><span data-stu-id="b46b1-128">SAP Note #2100040 – FAQ: SAP HANA CPU</span></span>](https://launchpad.support.sap.com/#/notes/0002100040)
- [<span data-ttu-id="b46b1-129">SAP-notitie #199997: veelgestelde vragen over: SAP HANA-geheugen</span><span class="sxs-lookup"><span data-stu-id="b46b1-129">SAP Note #199997 – FAQ: SAP HANA Memory</span></span>](https://launchpad.support.sap.com/#/notes/2177064)
- [<span data-ttu-id="b46b1-130">SAP-notitie #200000: veelgestelde vragen over: Optimalisatie van de SAP HANA-prestaties</span><span class="sxs-lookup"><span data-stu-id="b46b1-130">SAP Note #200000 – FAQ: SAP HANA Performance Optimization</span></span>](https://launchpad.support.sap.com/#/notes/2000000)
- [<span data-ttu-id="b46b1-131">SAP-notitie #199930: veelgestelde vragen over: SAP HANA i/o-analyse</span><span class="sxs-lookup"><span data-stu-id="b46b1-131">SAP Note #199930 – FAQ: SAP HANA I/O Analysis</span></span>](https://launchpad.support.sap.com/#/notes/1999930)
- [<span data-ttu-id="b46b1-132">SAP-notitie #2177064: veelgestelde vragen over: SAP HANA-Service opnieuw starten en loopt vast</span><span class="sxs-lookup"><span data-stu-id="b46b1-132">SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes</span></span>](https://launchpad.support.sap.com/#/notes/2177064)

<span data-ttu-id="b46b1-133">**SAP HANA-waarschuwingen**</span><span class="sxs-lookup"><span data-stu-id="b46b1-133">**SAP HANA Alerts**</span></span>

<span data-ttu-id="b46b1-134">Controleer Hallo huidige SAP HANA waarschuwing Logboeken als een eerste stap.</span><span class="sxs-lookup"><span data-stu-id="b46b1-134">As a first step, check hello current SAP HANA alert logs.</span></span> <span data-ttu-id="b46b1-135">Ga te in SAP HANA Studio**-beheerconsole: waarschuwingen: weergeven: alle waarschuwingen**.</span><span class="sxs-lookup"><span data-stu-id="b46b1-135">In SAP HANA Studio, go too**Administration Console: Alerts: Show: all alerts**.</span></span> <span data-ttu-id="b46b1-136">Op dit tabblad ziet alle SAP HANA-waarschuwingen voor specifieke waarden (beschikbaar fysiek geheugen, CPU-gebruik, enzovoort) die buiten Hallo ingesteld minimale en maximale drempelwaarden vallen.</span><span class="sxs-lookup"><span data-stu-id="b46b1-136">This tab will show all SAP HANA alerts for specific values (free physical memory, CPU utilization, etc.) that fall outside of hello set minimum and maximum thresholds.</span></span> <span data-ttu-id="b46b1-137">Standaard controles worden automatisch vernieuwd om de 15 minuten.</span><span class="sxs-lookup"><span data-stu-id="b46b1-137">By default, checks are auto-refreshed every 15 minutes.</span></span>

![Ga in de SAP HANA Studio tooAdministration Console: waarschuwingen: weergeven: alle waarschuwingen](./media/troubleshooting-monitoring/image1-show-alerts.png)

<span data-ttu-id="b46b1-139">**CPU**</span><span class="sxs-lookup"><span data-stu-id="b46b1-139">**CPU**</span></span>

<span data-ttu-id="b46b1-140">Voor een waarschuwing geactiveerd vanwege tooimproper drempelinstelling, is een resolutie tooreset toohello standaardwaarde of een meer redelijke drempelwaarde.</span><span class="sxs-lookup"><span data-stu-id="b46b1-140">For an alert triggered due tooimproper threshold setting, a resolution is tooreset toohello default value or a more reasonable threshold value.</span></span>

![Toohello standaardwaarde of een meer redelijke drempelwaarde opnieuw instellen](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

<span data-ttu-id="b46b1-142">Hallo waarschuwingen na kan duiden op problemen voor CPU-resources:</span><span class="sxs-lookup"><span data-stu-id="b46b1-142">hello following alerts may indicate CPU resource problems:</span></span>

- <span data-ttu-id="b46b1-143">Host-CPU-gebruik (waarschuwing 5)</span><span class="sxs-lookup"><span data-stu-id="b46b1-143">Host CPU Usage (Alert 5)</span></span>
- <span data-ttu-id="b46b1-144">Meest recente opslagpuntbewerking (waarschuwing 28)</span><span class="sxs-lookup"><span data-stu-id="b46b1-144">Most recent savepoint operation (Alert 28)</span></span>
- <span data-ttu-id="b46b1-145">Duur van het opslagpunt (waarschuwing 54)</span><span class="sxs-lookup"><span data-stu-id="b46b1-145">Savepoint duration (Alert 54)</span></span>

<span data-ttu-id="b46b1-146">Hoog CPU-verbruik ziet u op uw SAP HANA-database van een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="b46b1-146">You may notice high CPU consumption on your SAP HANA database from one of hello following:</span></span>

- <span data-ttu-id="b46b1-147">5 (Host-CPU-gebruik) van de waarschuwing wordt gegenereerd voor de huidige of eerdere CPU-gebruik</span><span class="sxs-lookup"><span data-stu-id="b46b1-147">Alert 5 (Host CPU usage) is raised for current or past CPU usage</span></span>
- <span data-ttu-id="b46b1-148">Hallo weergegeven CPU-gebruik op Hallo overzicht scherm</span><span class="sxs-lookup"><span data-stu-id="b46b1-148">hello displayed CPU usage on hello overview screen</span></span>

![CPU-gebruik op Hallo overzicht scherm weergegeven](./media/troubleshooting-monitoring/image3-cpu-usage.png)

<span data-ttu-id="b46b1-150">Hallo Load grafiek kan hoog CPU-verbruik of hoge verbruik in Hallo afgelopen weergeven:</span><span class="sxs-lookup"><span data-stu-id="b46b1-150">hello Load graph might show high CPU consumption, or high consumption in hello past:</span></span>

![Hallo Load grafiek kan hoog CPU-verbruik of hoog verbruik in Hallo afgelopen weergeven](./media/troubleshooting-monitoring/image4-load-graph.png)

<span data-ttu-id="b46b1-152">Een waarschuwing geactiveerd vanwege toohigh CPU-gebruik kan worden veroorzaakt door een aantal redenen, waaronder maar niet beperkt tot: de uitvoering van bepaalde transacties, het laden van gegevens, de verkeerd-om taken, langlopende SQL-instructies en ongeldige query-prestaties (bijvoorbeeld met BW op HANA kubussen).</span><span class="sxs-lookup"><span data-stu-id="b46b1-152">An alert triggered due toohigh CPU utilization could be caused by several reasons, including, but not limited to: execution of certain transactions, data loading, hanging of jobs, long running SQL statements, and bad query performance (for example, with BW on HANA cubes).</span></span>

<span data-ttu-id="b46b1-153">Raadpleeg toohello [SAP HANA probleemoplossing: CPU gerelateerde veroorzaakt en oplossingen](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site voor gedetailleerde stappen voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="b46b1-153">Refer toohello [SAP HANA Troubleshooting: CPU Related Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="b46b1-154">**Besturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="b46b1-154">**Operating System**</span></span>

<span data-ttu-id="b46b1-155">Een van de belangrijkste Hallo controleert voor SAP HANA op Linux is toomake ervoor dat transparante grote pagina's zijn uitgeschakeld, Zie [SAP-notitie #2131662 – transparante grote pagina's (THP) op Servers voor SAP HANA](https://launchpad.support.sap.com/#/notes/2131662).</span><span class="sxs-lookup"><span data-stu-id="b46b1-155">One of hello most important checks for SAP HANA on Linux is toomake sure that Transparent Huge Pages are disabled, see [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662).</span></span>

- <span data-ttu-id="b46b1-156">U kunt controleren als transparant grote pagina's worden ingeschakeld via Hallo Linux-opdracht te volgen: **cat /sys/kernel/mm/transparent\_hugepage/ingeschakeld**</span><span class="sxs-lookup"><span data-stu-id="b46b1-156">You can check if Transparent Huge Pages are enabled through hello following Linux command: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span></span>
- <span data-ttu-id="b46b1-157">Als _altijd_ is ingesloten door haakjes zoals hieronder, betekent dit dat de Hallo transparante grote pagina's zijn ingeschakeld: [altijd] madvise nooit; als _nooit_ is ingesloten door haakjes zoals hieronder, betekent dit dat Hallo transparant Grote pagina's zijn uitgeschakeld: altijd madvise [nooit]</span><span class="sxs-lookup"><span data-stu-id="b46b1-157">If _always_ is enclosed in brackets as below, it means that hello Transparent Huge Pages are enabled: [always] madvise never; if _never_ is enclosed in brackets as below, it means that hello Transparent Huge Pages are disabled: always madvise [never]</span></span>

<span data-ttu-id="b46b1-158">niets Hallo volgende Linux-opdracht moet worden geretourneerd: **rpm - qa | grep ulimit.**</span><span class="sxs-lookup"><span data-stu-id="b46b1-158">hello following Linux command should return nothing: **rpm -qa | grep ulimit.**</span></span> <span data-ttu-id="b46b1-159">Als het erop lijkt _ulimit_ is geïnstalleerd, verwijdert u deze onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="b46b1-159">If it appears _ulimit_ is installed, uninstall it immediately.</span></span>

<span data-ttu-id="b46b1-160">**Geheugen**</span><span class="sxs-lookup"><span data-stu-id="b46b1-160">**Memory**</span></span>

<span data-ttu-id="b46b1-161">Waarnemen dat Hallo bedrag van het geheugen toegewezen door Hallo SAP HANA-database is hoger dan verwacht.</span><span class="sxs-lookup"><span data-stu-id="b46b1-161">You may observe that hello amount of memory allocated by hello SAP HANA database is higher than expected.</span></span> <span data-ttu-id="b46b1-162">Hallo na de waarschuwingen wijzen op problemen met hoog geheugengebruik:</span><span class="sxs-lookup"><span data-stu-id="b46b1-162">hello following alerts indicate issues with high memory usage:</span></span>

- <span data-ttu-id="b46b1-163">Host fysieke geheugengebruik (waarschuwing 1)</span><span class="sxs-lookup"><span data-stu-id="b46b1-163">Host physical memory usage (Alert 1)</span></span>
- <span data-ttu-id="b46b1-164">Geheugengebruik van de naamserver (waarschuwing 12)</span><span class="sxs-lookup"><span data-stu-id="b46b1-164">Memory usage of name server (Alert 12)</span></span>
- <span data-ttu-id="b46b1-165">Totale geheugengebruik van kolom Store tabellen (waarschuwing 40)</span><span class="sxs-lookup"><span data-stu-id="b46b1-165">Total memory usage of Column Store tables (Alert 40)</span></span>
- <span data-ttu-id="b46b1-166">Geheugengebruik van services (waarschuwing 43)</span><span class="sxs-lookup"><span data-stu-id="b46b1-166">Memory usage of services (Alert 43)</span></span>
- <span data-ttu-id="b46b1-167">Geheugengebruik van de belangrijkste opslag van kolom Store tabellen (waarschuwing 45)</span><span class="sxs-lookup"><span data-stu-id="b46b1-167">Memory usage of main storage of Column Store tables (Alert 45)</span></span>
- <span data-ttu-id="b46b1-168">Runtime-dumpbestanden (waarschuwing 46)</span><span class="sxs-lookup"><span data-stu-id="b46b1-168">Runtime dump files (Alert 46)</span></span>

<span data-ttu-id="b46b1-169">Raadpleeg toohello [SAP HANA probleemoplossing: geheugenproblemen](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site voor gedetailleerde stappen voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="b46b1-169">Refer toohello [SAP HANA Troubleshooting: Memory Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="b46b1-170">**Netwerk**</span><span class="sxs-lookup"><span data-stu-id="b46b1-170">**Network**</span></span>

<span data-ttu-id="b46b1-171">Raadpleeg te[SAP-notitie #2081065 – SAP HANA-netwerk het oplossen van problemen](https://launchpad.support.sap.com/#/notes/2081065) en probleemoplossing van de stappen in deze SAP-notitie Hallo-netwerk uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="b46b1-171">Refer too[SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) and perform hello network troubleshooting steps in this SAP Note.</span></span>

1. <span data-ttu-id="b46b1-172">Analyse van round trip-tijd tussen server en client.</span><span class="sxs-lookup"><span data-stu-id="b46b1-172">Analyzing round-trip time between server and client.</span></span>
  <span data-ttu-id="b46b1-173">A.</span><span class="sxs-lookup"><span data-stu-id="b46b1-173">A.</span></span> <span data-ttu-id="b46b1-174">Hallo SQL-script uitvoeren [ _HANA\_netwerk\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="b46b1-174">Run hello SQL script [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>
  
2. <span data-ttu-id="b46b1-175">Analyseer de communicatie tussen knooppunten.</span><span class="sxs-lookup"><span data-stu-id="b46b1-175">Analyze internode communication.</span></span>
  <span data-ttu-id="b46b1-176">A.</span><span class="sxs-lookup"><span data-stu-id="b46b1-176">A.</span></span> <span data-ttu-id="b46b1-177">SQL-script uitvoeren [ _HANA\_netwerk\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="b46b1-177">Run SQL script [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>

3. <span data-ttu-id="b46b1-178">Voer de opdracht Linux **ifconfig** (Hallo uitvoer ziet als een pakketverlies optreden).</span><span class="sxs-lookup"><span data-stu-id="b46b1-178">Run Linux command **ifconfig** (hello output shows if any packet losses are occurring).</span></span>
4. <span data-ttu-id="b46b1-179">Voer de opdracht Linux **tcpdump**.</span><span class="sxs-lookup"><span data-stu-id="b46b1-179">Run Linux command **tcpdump**.</span></span>

<span data-ttu-id="b46b1-180">Gebruik tevens Hallo open-source [IPERF](https://iperf.fr/) hulpprogramma (of vergelijkbaar) toomeasure echte toepassing netwerkprestaties.</span><span class="sxs-lookup"><span data-stu-id="b46b1-180">Also, use hello open source [IPERF](https://iperf.fr/) tool (or similar) toomeasure real application network performance.</span></span>

<span data-ttu-id="b46b1-181">Raadpleeg toohello [SAP HANA probleemoplossing: prestaties toegang en verbindingsproblemen](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site voor gedetailleerde stappen voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="b46b1-181">Refer toohello [SAP HANA Troubleshooting: Networking Performance and Connectivity Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="b46b1-182">**Storage**</span><span class="sxs-lookup"><span data-stu-id="b46b1-182">**Storage**</span></span>

<span data-ttu-id="b46b1-183">Vanuit het perspectief van een eindgebruiker wordt een toepassing (of het Hallo-systeem als geheel) wordt traag uitgevoerd, reageert niet of kan zelfs toohang lijken als er problemen met i/o-prestaties zijn.</span><span class="sxs-lookup"><span data-stu-id="b46b1-183">From an end-user perspective, an application (or hello system as a whole) runs sluggishly, is unresponsive, or can even seem toohang if there are issues with I/O performance.</span></span> <span data-ttu-id="b46b1-184">In Hallo **Volumes** tabblad in SAP HANA-Studio, kunt u zien Hallo gekoppelde volumes en welke volumes worden gebruikt door elke service.</span><span class="sxs-lookup"><span data-stu-id="b46b1-184">In hello **Volumes** tab in SAP HANA Studio, you can see hello attached volumes, and what volumes are used by each service.</span></span>

![Hallo Volumes tabblad in SAP HANA Studio ziet u Hallo gekoppelde volumes en welke volumes worden gebruikt door elke service](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

<span data-ttu-id="b46b1-186">Gekoppelde volumes in de onderste gedeelte Hallo van welkomstscherm u details van ziet Hallo volumes, zoals bestanden en i/o-statistieken.</span><span class="sxs-lookup"><span data-stu-id="b46b1-186">Attached volumes in hello lower part of hello screen you can see details of hello volumes, such as files and I/O statistics.</span></span>

![Gekoppelde volumes in de onderste gedeelte Hallo van welkomstscherm u details van ziet Hallo volumes, zoals bestanden en i/o-statistieken](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

<span data-ttu-id="b46b1-188">Raadpleeg toohello [SAP HANA probleemoplossing: i/o-gerelateerde hoofdoorzaken en oplossingen](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) en [SAP HANA probleemoplossing: schijf gerelateerde hoofdoorzaken en oplossingen](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site voor gedetailleerde stappen voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="b46b1-188">Refer toohello [SAP HANA Troubleshooting: I/O Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) and [SAP HANA Troubleshooting: Disk Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="b46b1-189">**Diagnostische hulpprogramma 's**</span><span class="sxs-lookup"><span data-stu-id="b46b1-189">**Diagnostic Tools**</span></span>

<span data-ttu-id="b46b1-190">Uitvoeren van een SAP HANA-statuscontrole via HANA\_configuratie\_Minichecks.</span><span class="sxs-lookup"><span data-stu-id="b46b1-190">Perform an SAP HANA Health Check through HANA\_Configuration\_Minichecks.</span></span> <span data-ttu-id="b46b1-191">Dit hulpprogramma retourneert een potentieel kritiek technische problemen die als waarschuwingen in SAP HANA Studio al moeten zijn opgetreden.</span><span class="sxs-lookup"><span data-stu-id="b46b1-191">This tool returns potentially critical technical issues that should have already been raised as alerts in SAP HANA Studio.</span></span>

<span data-ttu-id="b46b1-192">Raadpleeg te[SAP-notitie #1969700-verzameling van de SQL-instructie voor SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) en Hallo SQL Statements.zip bestand gekoppelde toothat opmerking te downloaden.</span><span class="sxs-lookup"><span data-stu-id="b46b1-192">Refer too[SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) and download hello SQL Statements.zip file attached toothat note.</span></span> <span data-ttu-id="b46b1-193">Sla dit ZIP-bestand op Hallo van de lokale vaste schijf.</span><span class="sxs-lookup"><span data-stu-id="b46b1-193">Store this .zip file on hello local hard drive.</span></span>

<span data-ttu-id="b46b1-194">SAP HANA Studio Hallo **systeemgegevens** tabblad, met de rechtermuisknop op Hallo **naam** en selecteert u **SQL importinstructies**.</span><span class="sxs-lookup"><span data-stu-id="b46b1-194">In SAP HANA Studio, on hello **System Information** tab, right-click in hello **Name** column and select **Import SQL Statements**.</span></span>

![SAP HANA Studio op Hallo systeemgegevens tabblad met de rechtermuisknop op in de kolom naam Hallo en selecteer SQL-instructies voor importeren](./media/troubleshooting-monitoring/image7-import-statements-a.png)

<span data-ttu-id="b46b1-196">Selecteer Hallo SQL Statements.zip bestand lokaal opgeslagen en een map met de bijbehorende SQL-instructies hello wordt geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="b46b1-196">Select hello SQL Statements.zip file stored locally, and a folder with hello corresponding SQL statements will be imported.</span></span> <span data-ttu-id="b46b1-197">Op dit moment hello die veel verschillende diagnostische controles kunnen worden uitgevoerd met deze SQL-instructies.</span><span class="sxs-lookup"><span data-stu-id="b46b1-197">At this point, hello many different diagnostic checks can be run with these SQL statements.</span></span>

<span data-ttu-id="b46b1-198">Bijvoorbeeld: tootest SAP HANA System Replication bandbreedtevereisten, met de rechtermuisknop op Hallo **bandbreedte** instructie onder **replicatie: bandbreedte** en selecteer **Open** in SQL-Console.</span><span class="sxs-lookup"><span data-stu-id="b46b1-198">For example, tootest SAP HANA System Replication bandwidth requirements, right-click hello **Bandwidth** statement under **Replication: Bandwidth** and select **Open** in SQL Console.</span></span>

<span data-ttu-id="b46b1-199">Hallo volledige SQL-instructie wordt geopend zodat invoerparameters (wijziging sectie) toobe gewijzigd en vervolgens uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b46b1-199">hello complete SQL statement opens allowing input parameters (modification section) toobe changed and then executed.</span></span>

![Hallo volledige SQL-instructie wordt geopend zodat invoerparameters (wijziging sectie) toobe gewijzigd en vervolgens uitvoeren](./media/troubleshooting-monitoring/image8-import-statements-b.png)

<span data-ttu-id="b46b1-201">Een ander voorbeeld is met de rechtermuisknop op op Hallo-overzichten onder **replicatie: overzicht**.</span><span class="sxs-lookup"><span data-stu-id="b46b1-201">Another example is right-clicking on hello statements under **Replication: Overview**.</span></span> <span data-ttu-id="b46b1-202">Selecteer **Execute** in het contextmenu Hallo:</span><span class="sxs-lookup"><span data-stu-id="b46b1-202">Select **Execute** from hello context menu:</span></span>

![Een ander voorbeeld is met de rechtermuisknop op op Hallo-overzichten onder replicatie: overzicht.](./media/troubleshooting-monitoring/image9-import-statements-c.png)

<span data-ttu-id="b46b1-205">Dit resulteert in informatie die bij het oplossen van helpt:</span><span class="sxs-lookup"><span data-stu-id="b46b1-205">This results in information that helps with troubleshooting:</span></span>

![Dit leidt tot informatie die bij het oplossen van problemen helpt](./media/troubleshooting-monitoring/image10-import-statements-d.png)

<span data-ttu-id="b46b1-207">Dezelfde Hallo voor HANA\_configuratie\_Minichecks en controleer of alle _X_ merken in Hallo _C_ kolom (Kritiek).</span><span class="sxs-lookup"><span data-stu-id="b46b1-207">Do hello same for HANA\_Configuration\_Minichecks and check for any _X_ marks in hello _C_ (Critical) column.</span></span>

<span data-ttu-id="b46b1-208">Voorbeeld van uitvoer:</span><span class="sxs-lookup"><span data-stu-id="b46b1-208">Sample outputs:</span></span>

<span data-ttu-id="b46b1-209">**HANA\_configuratie\_MiniChecks\_Rev102.01 + 1** voor algemene SAP HANA-controles.</span><span class="sxs-lookup"><span data-stu-id="b46b1-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** for general SAP HANA checks.</span></span>

![HANA\_configuratie\_MiniChecks\_Rev102.01 + 1 voor algemene SAP HANA-controles](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

<span data-ttu-id="b46b1-211">**HANA\_Services\_overzicht** voor een overzicht van wat SAP HANA-services die momenteel worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b46b1-211">**HANA\_Services\_Overview** for an overview of what SAP HANA services are currently running.</span></span>

![HANA\_Services\_overzicht voor een overzicht van wat SAP HANA-services die momenteel worden uitgevoerd](./media/troubleshooting-monitoring/image12-services-overview.png)

<span data-ttu-id="b46b1-213">**HANA\_Services\_statistieken** voor SAP HANA servicegegevens (CPU, geheugen, etc.).</span><span class="sxs-lookup"><span data-stu-id="b46b1-213">**HANA\_Services\_Statistics** for SAP HANA service information (CPU, memory, etc.).</span></span>

![<span data-ttu-id="b46b1-214">HANA\_Services\_statistieken voor SAP HANA-servicegegevens</span><span class="sxs-lookup"><span data-stu-id="b46b1-214">HANA\_Services\_Statistics for SAP HANA service information</span></span> ](./media/troubleshooting-monitoring/image13-services-statistics.png)

<span data-ttu-id="b46b1-215">**HANA\_configuratie\_overzicht\_Rev110 +** voor algemene informatie over Hallo SAP HANA-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="b46b1-215">**HANA\_Configuration\_Overview\_Rev110+** for general information on hello SAP HANA instance.</span></span>

![HANA\_configuratie\_overzicht\_Rev110 + voor algemene informatie over Hallo SAP HANA-exemplaar](./media/troubleshooting-monitoring/image14-configuration-overview.png)

<span data-ttu-id="b46b1-217">**HANA\_configuratie\_Parameters\_Rev70 +** toocheck SAP HANA-parameters.</span><span class="sxs-lookup"><span data-stu-id="b46b1-217">**HANA\_Configuration\_Parameters\_Rev70+** toocheck SAP HANA parameters.</span></span>

![HANA\_configuratie\_Parameters\_Rev70 + toocheck SAP HANA parameters](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

