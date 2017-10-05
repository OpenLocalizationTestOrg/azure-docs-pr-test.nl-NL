---
title: Dashboard, bewaken, schaal, configureren, en hybride verbindingen in BizTalk Services | Microsoft Docs
description: 'Meer informatie over de besturingselementen en bewaken op de prestaties van de klassieke portal tabbladen voor BizTalk Services: Dashboard, bewaken, schaal, configureren en hybride verbindingen. MABS, WABS'
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7a1815db-0de2-4274-8be0-198c1b077324
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 4ec88d9a681a5692b31f7e3990d1c153296b18ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="review-the-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a><span data-ttu-id="50747-104">De tabbladen Dashboard, Controleren, Schaal, Configureren en Hybride verbinding controleren</span><span class="sxs-lookup"><span data-stu-id="50747-104">Review the Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="50747-105">Nadat u uw BizTalk Service maken en implementeren van uw toepassing, kunt u enkele van de BizTalk Service-instellingen wijzigen en controleren van de toepassingsprestaties.</span><span class="sxs-lookup"><span data-stu-id="50747-105">After you create your BizTalk Service and deploy your application, you can change some of the BizTalk Service settings and monitor the application performance.</span></span> 

<span data-ttu-id="50747-106">Wanneer u de klassieke Azure portal opent, wordt u automatisch geplaatst op de **alle ITEMS** tabblad.</span><span class="sxs-lookup"><span data-stu-id="50747-106">When you open the Azure classic portal, you are automatically placed at the **ALL ITEMS** tab.</span></span> <span data-ttu-id="50747-107">Als u wilt weergeven van uw BizTalk Service, selecteer uw BizTalk Service in de **alle ITEMS** tabblad of Selecteer de **BIZTALK SERVICES** tabblad; en selecteer vervolgens de naam van uw BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="50747-107">To view your BizTalk Service, select your BizTalk Service in the **ALL ITEMS** tab or select the **BIZTALK SERVICES** tab; and then select your BizTalk Service name.</span></span>

<span data-ttu-id="50747-108">Hiermee wordt een nieuw venster geopend met de volgende tabbladen.</span><span class="sxs-lookup"><span data-stu-id="50747-108">This opens a new window with the following tabs.</span></span> <span data-ttu-id="50747-109">Dit onderwerp beschrijft deze tabbladen.</span><span class="sxs-lookup"><span data-stu-id="50747-109">This topic describes these tabs.</span></span>

## <a name="quickstart-quickstartquickstart"></a><span data-ttu-id="50747-110">Quick Start)</span><span class="sxs-lookup"><span data-stu-id="50747-110">Quickstart (</span></span>![Snelstartgids][Quickstart]<span data-ttu-id="50747-112">)</span><span class="sxs-lookup"><span data-stu-id="50747-112">)</span></span>
<span data-ttu-id="50747-113">Afhankelijk van de editie van BizTalk Services, alle vermelde opties mogelijk niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="50747-113">Depending on the BizTalk Services Edition, all options listed may not be available.</span></span> 

<table border="1">
    <tr>
        <td><span data-ttu-id="50747-114"><strong>Download de hulpprogramma 's</strong></span><span class="sxs-lookup"><span data-stu-id="50747-114"><strong>Get the tools</strong></span></span></td>
        <td><span data-ttu-id="50747-115">Download de BizTalk Services SDK voor het installeren van de Visual Studio-projectsjablonen op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="50747-115">Download the BizTalk Services SDK to install the Visual Studio project templates on your on-premises development computer.</span></span> <span data-ttu-id="50747-116">Deze sjablonen maken het <strong>BizTalk Services</strong> (brug) en de <strong>BizTalk serviceartefacten</strong> (transformatie) Visual Studio-projecten die zijn geïmplementeerd voor uw BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="50747-116">These templates create the <strong>BizTalk Services</strong> (bridge) and the <strong>BizTalk Service Artifacts</strong> (Transform) Visual Studio projects that are deployed to your BizTalk Service.</span></span>
        <br/><br/><span data-ttu-id="50747-117">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Hoe Start ik met de Azure BizTalk Services SDK </a> en <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">installeren van de Azure BizTalk Services SDK</a> vermeldt de stappen om te beginnen.</span><span class="sxs-lookup"><span data-stu-id="50747-117">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> How do I Start Using the Azure BizTalk Services SDK </a> and <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installing the Azure BizTalk Services SDK</a> lists the steps to get started.</span></span>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="50747-118"><strong>Partner overeenkomsten maken</strong></span><span class="sxs-lookup"><span data-stu-id="50747-118"><strong>Create partner agreements</strong></span></span></td>
        <td><span data-ttu-id="50747-119">Hiermee opent u de Azure BizTalk Services-Portal gehost op Azure, waarbij het toevoegen van partners en X12, AS2, maken en EDIFACT EDI-overeenkomsten.</span><span class="sxs-lookup"><span data-stu-id="50747-119">Opens the Azure BizTalk Services Portal hosted on Azure where you add partners and create X12, AS2, and EDIFACT EDI agreements.</span></span>
        <br/><br/><span data-ttu-id="50747-120">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configureren van onderdelen voor EDI-berichten op BizTalk Services Portal</a> vermeldt de stappen om te beginnen.</span><span class="sxs-lookup"><span data-stu-id="50747-120">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> lists the steps to get started.</span></span>
        </td>
    </tr>

<tr>
        <td><span data-ttu-id="50747-121"><strong>Meer informatie over BizTalk Services</strong></span><span class="sxs-lookup"><span data-stu-id="50747-121"><strong>Learn more about BizTalk Services</strong></span></span></td>
        <td><span data-ttu-id="50747-122">Ga naar de <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> voor meer informatie over Azure BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="50747-122">Go to the <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> to learn more about Azure BizTalk Services.</span></span></td>
</tr>
</table>


<span data-ttu-id="50747-123">U kunt in de taakbalk onder:</span><span class="sxs-lookup"><span data-stu-id="50747-123">In the task bar at the bottom, you can:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="50747-124"><strong>Beheren</strong> implementatie van uw toepassing</span><span class="sxs-lookup"><span data-stu-id="50747-124"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="50747-125">Hiermee opent u de Azure BizTalk Services-portal.</span><span class="sxs-lookup"><span data-stu-id="50747-125">Opens the Azure BizTalk Services portal.</span></span> <span data-ttu-id="50747-126">De BizTalk Services-Portal is de toegang tot EDI-configuratie, inclusief partners toevoegen en X12, AS2, maken en EDIFACT-overeenkomsten.</span><span class="sxs-lookup"><span data-stu-id="50747-126">The BizTalk Services Portal is the entrance to EDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="50747-127">Dit is hetzelfde als <strong>partner overeenkomsten maken</strong> op de <strong>Quick Start</strong> tabblad.</span><span class="sxs-lookup"><span data-stu-id="50747-127">This is the same as <strong>Create partner agreements</strong> on the <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="50747-128">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configureren van onderdelen voor EDI-berichten op BizTalk Services Portal</a> bevat meer informatie over de BizTalk Services-Portal.</span><span class="sxs-lookup"><span data-stu-id="50747-128">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on the BizTalk Services Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="50747-129"><strong>Verbindingsgegevens</strong> van de Access Control-Namespace</span><span class="sxs-lookup"><span data-stu-id="50747-129"><strong>Connection Information</strong> of the Access Control Namespace</span></span></td>
<td><span data-ttu-id="50747-130">Wanneer u de verbindingsgegevens selecteert, klikt u vervolgens de Access Control Namespace, standaard verlener en sleutel standaard weergegeven.</span><span class="sxs-lookup"><span data-stu-id="50747-130">When you select Connection Information, then the Access Control Namespace, Default Issuer, and Default Key are displayed.</span></span> <span data-ttu-id="50747-131">U kunt deze waarden kopiëren.</span><span class="sxs-lookup"><span data-stu-id="50747-131">You can copy these values.</span></span>
<br/><br/>
<span data-ttu-id="50747-132">U kunt ook de Access Control-beheerportal openen.</span><span class="sxs-lookup"><span data-stu-id="50747-132">You can also open the Access Control Portal.</span></span> <span data-ttu-id="50747-133"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Maken van een toegangsbeheer Namespace</a> bevat meer informatie over de Access Control-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="50747-133"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Create an Access control Namespace</a> provides more information on the Access Control Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="50747-134"><strong>Sleutels synchroniseren</strong> in het Opslagaccount</span><span class="sxs-lookup"><span data-stu-id="50747-134"><strong>Sync Keys</strong> in the Storage Account</span></span></td>
<td><span data-ttu-id="50747-135">Wanneer u een opslagaccount maakt, worden automatisch een primaire en secundaire sleutel gemaakt.</span><span class="sxs-lookup"><span data-stu-id="50747-135">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="50747-136">Deze versleutelingssleutels beheren toegang tot uw Storage-Account.</span><span class="sxs-lookup"><span data-stu-id="50747-136">These encryption Keys control access to your Storage Account.</span></span> <span data-ttu-id="50747-137">Uw BizTalk Service gebruikt automatisch de primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="50747-137">Your BizTalk Service automatically uses the Primary Key.</span></span> <span data-ttu-id="50747-138"><strong>Sleutels synchroniseren</strong> kunnen gebruikers schakelen tussen de primaire sleutel en de secundaire sleutel zonder te onderbreken van de BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="50747-138"><strong>Sync Keys</strong> enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="50747-139">U wilt dat de BizTalk Service met een nieuwe primaire sleutel voor het Opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="50747-139">For example, you want the BizTalk Service to use a new Primary Key for the Storage Account.</span></span> <span data-ttu-id="50747-140">Om dit te doen:</span><span class="sxs-lookup"><span data-stu-id="50747-140">To do this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="50747-141">Selecteer uw BizTalk Service en selecteer <strong>sleutels synchroniseren</strong>.</span><span class="sxs-lookup"><span data-stu-id="50747-141">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="50747-142">Selecteer de secundaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="50747-142">Select the Secondary Key.</span></span> <span data-ttu-id="50747-143">Als u dit doet, wordt de BizTalk Service wordt gestart met behulp van de secundaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="50747-143">When you do this, the BizTalk Service starts using the Secondary Key.</span></span></li>
<li><span data-ttu-id="50747-144">In de klassieke Azure portal, selecteer uw Storage-account en de primaire sleutel opnieuw genereren.</span><span class="sxs-lookup"><span data-stu-id="50747-144">In the Azure classic portal, select your Storage account and Regenerate the Primary Key.</span></span> <span data-ttu-id="50747-145">Vergeet niet uw BizTalk Service met behulp van de secundaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="50747-145">Remember, your BizTalk Service is using the Secondary Key.</span></span></li>
<li><span data-ttu-id="50747-146">Selecteer uw BizTalk Service en selecteer <strong>sleutels synchroniseren</strong>.</span><span class="sxs-lookup"><span data-stu-id="50747-146">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="50747-147">Selecteer nu de primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="50747-147">Now, select the Primary Key.</span></span> <span data-ttu-id="50747-148">Dit is de nieuwe primaire sleutel die u opnieuw gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="50747-148">This is the new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="50747-149">In de klassieke Azure portal, selecteer uw Storage-account en de secundaire sleutel opnieuw genereren.</span><span class="sxs-lookup"><span data-stu-id="50747-149">In the Azure classic portal, select your Storage account and Regenerate the Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="50747-150">Dit proces wordt 'rollover voor sleutels' genoemd.</span><span class="sxs-lookup"><span data-stu-id="50747-150">This process is called "rollover keys".</span></span> <span data-ttu-id="50747-151">Het doel is om gebruikers schakelen tussen de primaire sleutel en de secundaire sleutel zonder te onderbreken van de BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="50747-151">The purpose is to enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="50747-152"><strong>Verwijder</strong> uw toepassing</span><span class="sxs-lookup"><span data-stu-id="50747-152"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="50747-153">Wanneer u selecteert verwijderen, uw BizTalk Service en alle items die zijn geïmplementeerd, worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="50747-153">When you select Delete, your BizTalk Service and all items deployed to it are removed.</span></span></td>
</tr>
</table>


## <a name="dashboard"></a><span data-ttu-id="50747-154">Dashboard</span><span class="sxs-lookup"><span data-stu-id="50747-154">Dashboard</span></span>
<span data-ttu-id="50747-155">Afhankelijk van de editie van BizTalk Services, alle vermelde opties mogelijk niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="50747-155">Depending on the BizTalk Services Edition, all options listed may not be available.</span></span> 

<span data-ttu-id="50747-156">Wanneer u de naam van uw BizTalk Service selecteert, wordt het tabblad Dashboard wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="50747-156">When you select your BizTalk Service name, the Dashboard tab is displayed.</span></span> <span data-ttu-id="50747-157">In het Dashboard kunt u:</span><span class="sxs-lookup"><span data-stu-id="50747-157">In Dashboard, you can:</span></span>

##### <a name="usage-overview-shows-the-number-of-used-hybrid-connections"></a><span data-ttu-id="50747-158">Overzicht van gebruik: Toont het aantal gebruikte hybride verbindingen</span><span class="sxs-lookup"><span data-stu-id="50747-158">Usage Overview: Shows the number of used Hybrid Connections</span></span>
<span data-ttu-id="50747-159">Het gebruik van de gegevens worden ook weergegeven in GB.</span><span class="sxs-lookup"><span data-stu-id="50747-159">Also displays the data usage in GB.</span></span> 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a><span data-ttu-id="50747-160">Metrische grafiek: Toont een vaste lijst maatstaven voor prestaties</span><span class="sxs-lookup"><span data-stu-id="50747-160">Metric Graph: Shows a fixed list of performance metrics</span></span>
<span data-ttu-id="50747-161">Deze metrische gegevens opgeven realtime waarden met betrekking tot de status van de BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="50747-161">These metrics provide real-time values regarding the health of the BizTalk Service.</span></span> <span data-ttu-id="50747-162">U kunt ook de **relatieve** of **Absolute** waarden en het tijdsbereik **Interval** van de metrische gegevens die worden weergegeven in de grafiek.</span><span class="sxs-lookup"><span data-stu-id="50747-162">You can also choose the **Relative** or **Absolute** values and the time range **Interval** of the metrics that are displayed in the graph.</span></span> 

<span data-ttu-id="50747-163">Voor een beschrijving van deze maatstaven voor prestaties, gaat u naar [beschikbare metrische gegevens](#Metrics) in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="50747-163">For a description of these performance metrics, go to [Available Metrics](#Metrics) in this topic.</span></span>

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a><span data-ttu-id="50747-164">Snelle weergave: Geeft een lijst van uw BizTalk Service-eigenschappen</span><span class="sxs-lookup"><span data-stu-id="50747-164">Quick Glance: Lists your BizTalk Service properties</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="50747-165"><strong>Database bijhouden referenties bijwerken</strong></span><span class="sxs-lookup"><span data-stu-id="50747-165"><strong>Update Tracking Database credentials</strong></span></span></td>
<td><span data-ttu-id="50747-166">De gebruikersnaam en wachtwoord gebruikt voor aanmelding bij de Database voor het bijhouden van wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="50747-166">Changes the user name and password used to log into the Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-167"><strong>SSL-certificaat bijwerken</strong></span><span class="sxs-lookup"><span data-stu-id="50747-167"><strong>Update SSL Certificate</strong></span></span></td>
<td><span data-ttu-id="50747-168">Kan de BizTalk Service voor het gebruik van een ander SSL-certificaat bijwerken.</span><span class="sxs-lookup"><span data-stu-id="50747-168">Can update the BizTalk Service to use a different SSL certificate.</span></span> <span data-ttu-id="50747-169">Een zelfondertekend SSL-certificaat wordt automatisch gemaakt wanneer u <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">de BizTalk Service maakt</a>.</span><span class="sxs-lookup"><span data-stu-id="50747-169">A self-signed SSL certificate is automatically created when you <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">create the BizTalk Service</a>.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-170"><strong>Certificaat downloaden</strong></span><span class="sxs-lookup"><span data-stu-id="50747-170"><strong>Download Certificate</strong></span></span></td>
<td><span data-ttu-id="50747-171">U kunt het SSL-certificaat gebruikt door uw BizTalk Service naar een lokale computer downloaden.</span><span class="sxs-lookup"><span data-stu-id="50747-171">You can download the SSL certificate used by your BizTalk Service to a local machine.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-172"><strong>Status</strong></span><span class="sxs-lookup"><span data-stu-id="50747-172"><strong>Status</strong></span></span></td>
<td><span data-ttu-id="50747-173">Geeft de huidige status van uw BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="50747-173">Displays the current status of your BizTalk Service.</span></span> <span data-ttu-id="50747-174">Zie <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Statusgrafiek Service</a>.</span><span class="sxs-lookup"><span data-stu-id="50747-174">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Service state chart</a>.</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="50747-175"><strong>Service-URL</strong></span><span class="sxs-lookup"><span data-stu-id="50747-175"><strong>Service URL</strong></span></span></td>
<td><span data-ttu-id="50747-176">De URL voor uw BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="50747-176">The URL for your BizTalk Service.</span></span> <span data-ttu-id="50747-177">Dit is hetzelfde als de <strong>domein-URL</strong> ingevoerd bij het maken van uw BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="50747-177">This is the same as the <strong>Domain URL</strong> entered when your BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-178"><strong>Adres van de openbare virtuele IP (VIP)</strong></span><span class="sxs-lookup"><span data-stu-id="50747-178"><strong>Public Virtual IP (VIP) Address</strong></span></span></td>
<td><span data-ttu-id="50747-179">Het IP-adres wordt toegewezen aan uw BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="50747-179">The IP address assigned to your BizTalk Service.</span></span> <span data-ttu-id="50747-180">Het wordt gebruikt voor alle invoereindpunten en het bronadres voor uitgaand verkeer.</span><span class="sxs-lookup"><span data-stu-id="50747-180">It is used for all input endpoints and is the source address for outbound traffic.</span></span> <span data-ttu-id="50747-181">Dit IP-adres behoort tot uw BizTalk Service wanneer deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="50747-181">This IP address belongs to your BizTalk Service as long as it is created.</span></span> <span data-ttu-id="50747-182">Als u de BizTalk Service verwijdert, wordt het IP-adres toegewezen aan een andere BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="50747-182">If you delete the BizTalk Service, the IP address is assigned to another BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-183"><strong>ACS-Namespace</strong></span><span class="sxs-lookup"><span data-stu-id="50747-183"><strong>ACS Namespace</strong></span></span></td>
<td><span data-ttu-id="50747-184">Verifieert met de BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="50747-184">Authenticates with the BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-185"><strong>Editie</strong></span><span class="sxs-lookup"><span data-stu-id="50747-185"><strong>Edition</strong></span></span></td>
<td><span data-ttu-id="50747-186">Een lijst met de editie ingevoerd bij het maken van de BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="50747-186">Lists the Edition entered when the BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-187"><strong>Locatie</strong></span><span class="sxs-lookup"><span data-stu-id="50747-187"><strong>Location</strong></span></span></td>
<td><span data-ttu-id="50747-188">Geeft de geografische regio die als host fungeert voor uw BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="50747-188">Displays the geographic region that hosts your BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-189"><strong>Gemaakt</strong></span><span class="sxs-lookup"><span data-stu-id="50747-189"><strong>Created</strong></span></span></td>
<td><span data-ttu-id="50747-190">Geeft de datum en tijd waarop die de BizTalk Service is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="50747-190">Displays the date and time the BizTalk Service was created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-191"><strong>Traceringsdatabase</strong></span><span class="sxs-lookup"><span data-stu-id="50747-191"><strong>Tracking Database</strong></span></span></td>
<td><span data-ttu-id="50747-192">De naam van het Azure SQL Database die de Traceringstabellen gebruikt door uw BizTalk Service worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="50747-192">The Azure SQL Database name that stores the tracking tables used by your BizTalk Service.</span></span> 
<br/><br/><span data-ttu-id="50747-193">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Vereisten wat</a> biedt details over de Database bijhouden.</span><span class="sxs-lookup"><span data-stu-id="50747-193">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on the Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-194"><strong>Opslag voor bewaken/archiveren</strong></span><span class="sxs-lookup"><span data-stu-id="50747-194"><strong>Monitoring/Archiving Storage</strong></span></span></td>
<td><span data-ttu-id="50747-195">De naam van de Azure Storage-account waarmee de uitvoer van de bewaking van uw BizTalk Service worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="50747-195">The Azure Storage account name that stores the monitoring output of your BizTalk Service.</span></span>
<br/><br/><span data-ttu-id="50747-196">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Vereisten wat</a> biedt details over de Storage-account.</span><span class="sxs-lookup"><span data-stu-id="50747-196">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on the Storage account.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-197"><strong>De naam van abonnement</strong></span><span class="sxs-lookup"><span data-stu-id="50747-197"><strong>Subscription Name</strong></span></span></td>
<td><span data-ttu-id="50747-198">Het abonnement dat als host fungeert voor uw BizTalk Service bevat.</span><span class="sxs-lookup"><span data-stu-id="50747-198">Lists the subscription that hosts your BizTalk Service.</span></span> <span data-ttu-id="50747-199">Het abonnement bepaalt toegang tot de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="50747-199">The subscription governs access to the Azure classic portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-200"><strong>Abonnements-ID</strong></span><span class="sxs-lookup"><span data-stu-id="50747-200"><strong>Subscription ID</strong></span></span></td>
<td><span data-ttu-id="50747-201">Wanneer een abonnement is gemaakt, wordt er automatisch een abonnements-ID gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="50747-201">When a subscription is created, a subscription ID is automatically generated.</span></span> <span data-ttu-id="50747-202">Wanneer u de REST-API's, moet u mogelijk opgeven de abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="50747-202">When using REST APIs, you may need to enter the Subscription ID.</span></span></td>
</tr>
</table>

<span data-ttu-id="50747-203">[BizTalk Services: Inrichten met behulp van Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) vermeldt de stappen voor het maken van een BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="50747-203">[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) lists the steps to create a BizTalk Service.</span></span>

##### <a name="manage-connection-information-sync-keys-and-delete-in-the-task-bar"></a><span data-ttu-id="50747-204">Beheren van de verbindingsinformatie, de sleutels synchroniseren, en verwijder in de taakbalk:</span><span class="sxs-lookup"><span data-stu-id="50747-204">Manage, Connection Information, Sync Keys, and Delete in the task bar:</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="50747-205"><strong>Beheren</strong> implementatie van uw toepassing</span><span class="sxs-lookup"><span data-stu-id="50747-205"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="50747-206">Hiermee opent u de Azure BizTalk Services-Portal.</span><span class="sxs-lookup"><span data-stu-id="50747-206">Opens the Azure BizTalk Services Portal.</span></span> <span data-ttu-id="50747-207">De BizTalk Services-Portal is de toegang tot EDI-configuratie, inclusief partners toevoegen en X12, AS2, maken en EDIFACT-overeenkomsten.</span><span class="sxs-lookup"><span data-stu-id="50747-207">The BizTalk Services Portal is the entrance to EDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="50747-208">Dit is hetzelfde als <strong>partner overeenkomsten maken</strong> op de <strong>Quick Start</strong> tabblad.</span><span class="sxs-lookup"><span data-stu-id="50747-208">This is the same as <strong>Create partner agreements</strong> on the <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="50747-209">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configureren van onderdelen voor EDI-berichten op BizTalk Services Portal</a> bevat meer informatie over de BizTalk Services-Portal.</span><span class="sxs-lookup"><span data-stu-id="50747-209">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on the BizTalk Services Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-210"><strong>Verbindingsgegevens</strong> van de Access Control-Namespace</span><span class="sxs-lookup"><span data-stu-id="50747-210"><strong>Connection Information</strong> of the Access Control Namespace</span></span></td>
<td><span data-ttu-id="50747-211">Geeft de Access Control Namespace, standaard verlener en standaard sleutelwaarden; die kunnen worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="50747-211">Displays the Access Control Namespace, Default Issuer, and Default Key values; which can be copied.</span></span>
<br/><br/>
<span data-ttu-id="50747-212">U kunt ook de Access Control-beheerportal openen.</span><span class="sxs-lookup"><span data-stu-id="50747-212">You can also open the Access Control Portal.</span></span> <span data-ttu-id="50747-213">Deze Access Control-beheerportal is hetzelfde als wanneer u de optie Active Directory in het navigatiedeelvenster links.</span><span class="sxs-lookup"><span data-stu-id="50747-213">This Access Control Portal is the same as using the Active Directory option in the left navigation pane.</span></span>
<br/><br/><span data-ttu-id="50747-214">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Het beheren van uw ACS-Namespace</a> bevat meer informatie over de Access Control-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="50747-214">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Managing Your ACS Namespace</a> provides more information on the Access Control Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-215"><strong>Sleutels synchroniseren</strong> in het Opslagaccount</span><span class="sxs-lookup"><span data-stu-id="50747-215"><strong>Sync Keys</strong> in the Storage Account</span></span></td>
<td><span data-ttu-id="50747-216">Wanneer u een opslagaccount maakt, worden automatisch een primaire en secundaire sleutel gemaakt.</span><span class="sxs-lookup"><span data-stu-id="50747-216">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="50747-217">Deze versleutelingssleutels beheren toegang tot uw Storage-Account.</span><span class="sxs-lookup"><span data-stu-id="50747-217">These encryption Keys control access to your Storage Account.</span></span> <span data-ttu-id="50747-218">Uw BizTalk Service gebruikt automatisch de primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="50747-218">Your BizTalk Service automatically uses the Primary Key.</span></span> <span data-ttu-id="50747-219"><strong>Sleutels synchroniseren</strong> kunnen gebruikers schakelen tussen de primaire sleutel en de secundaire sleutel zonder te onderbreken van de BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="50747-219"><strong>Sync Keys</strong> enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="50747-220">U wilt dat de BizTalk Service met een nieuwe primaire sleutel voor het Opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="50747-220">For example, you want the BizTalk Service to use a new Primary Key for the Storage Account.</span></span> <span data-ttu-id="50747-221">Om dit te doen:</span><span class="sxs-lookup"><span data-stu-id="50747-221">To do this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="50747-222">Selecteer uw BizTalk Service en selecteer <strong>sleutels synchroniseren</strong>.</span><span class="sxs-lookup"><span data-stu-id="50747-222">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="50747-223">Selecteer de secundaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="50747-223">Select the Secondary Key.</span></span> <span data-ttu-id="50747-224">Als u dit doet, wordt de BizTalk Service wordt gestart met behulp van de secundaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="50747-224">When you do this, the BizTalk Service starts using the Secondary Key.</span></span></li>
<li><span data-ttu-id="50747-225">In de klassieke Azure portal, selecteer uw Storage-account en de primaire sleutel opnieuw genereren.</span><span class="sxs-lookup"><span data-stu-id="50747-225">In the Azure classic portal, select your Storage account and Regenerate the Primary Key.</span></span> <span data-ttu-id="50747-226">Vergeet niet uw BizTalk Service met behulp van de secundaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="50747-226">Remember, your BizTalk Service is using the Secondary Key.</span></span></li>
<li><span data-ttu-id="50747-227">Selecteer uw BizTalk Service en selecteer <strong>sleutels synchroniseren</strong>.</span><span class="sxs-lookup"><span data-stu-id="50747-227">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="50747-228">Selecteer nu de primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="50747-228">Now, select the Primary Key.</span></span> <span data-ttu-id="50747-229">Dit is de nieuwe primaire sleutel die u opnieuw gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="50747-229">This is the new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="50747-230">In de klassieke Azure portal, selecteer uw Storage-account en de secundaire sleutel opnieuw genereren.</span><span class="sxs-lookup"><span data-stu-id="50747-230">In the Azure classic portal, select your Storage account and Regenerate the Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="50747-231">Dit proces wordt 'rollover voor sleutels' genoemd.</span><span class="sxs-lookup"><span data-stu-id="50747-231">This process is called "rollover keys".</span></span> <span data-ttu-id="50747-232">Het doel is om gebruikers schakelen tussen de primaire sleutel en de secundaire sleutel zonder te onderbreken van de BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="50747-232">The purpose is to enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="50747-233"><strong>Verwijder</strong> uw toepassing</span><span class="sxs-lookup"><span data-stu-id="50747-233"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="50747-234">Uw BizTalk Service en alle items die zijn geïmplementeerd, worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="50747-234">Your BizTalk Service and all items deployed to it are removed.</span></span></td>
</tr>
</table>


## <a name="monitor"></a><span data-ttu-id="50747-235">Bewaken</span><span class="sxs-lookup"><span data-stu-id="50747-235">Monitor</span></span>
<span data-ttu-id="50747-236">Niet van toepassing op de editie Free.</span><span class="sxs-lookup"><span data-stu-id="50747-236">Does not apply to the Free Edition.</span></span>

<span data-ttu-id="50747-237">Wanneer u de naam van uw BizTalk Service selecteert, wordt het tabblad Monitor beschikbaar en wordt het volgende weergegeven:</span><span class="sxs-lookup"><span data-stu-id="50747-237">When you select your BizTalk Service name, the Monitor tab is available and displays the following:</span></span>

##### <a name="metric-graph-displays-the-selected-performance-metrics"></a><span data-ttu-id="50747-238">Metrische grafiek: Geeft de geselecteerde prestatiewaarden</span><span class="sxs-lookup"><span data-stu-id="50747-238">Metric Graph: Displays the selected performance metrics</span></span>
<span data-ttu-id="50747-239">Deze metrische gegevens opgeven realtime waarden met betrekking tot de status van de BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="50747-239">These metrics provide real-time values regarding the health of the BizTalk Service.</span></span> <span data-ttu-id="50747-240">U kiezen welke maatstaven voor prestaties worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="50747-240">You choose which performance metrics are displayed.</span></span> <span data-ttu-id="50747-241">Maximaal zes maatstaven voor prestaties kan tegelijkertijd worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="50747-241">A maximum of six performance metrics can be displayed simultaneously.</span></span> 

<span data-ttu-id="50747-242">U kunt ook de **relatieve** of **Absolute** waarden en het tijdsbereik **Interval** van de metrische gegevens die worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="50747-242">You can also choose the **Relative** or **Absolute** values and the time range **Interval** of the metrics that are displayed.</span></span> 

##### <a name="to-remove-or-display-metrics-in-the-graph"></a><span data-ttu-id="50747-243">Om te verwijderen of metrische gegevens weergeven in de grafiek:</span><span class="sxs-lookup"><span data-stu-id="50747-243">To remove or display metrics in the graph:</span></span>
1. <span data-ttu-id="50747-244">Selecteer de **Monitor** tabblad.</span><span class="sxs-lookup"><span data-stu-id="50747-244">Select the **Monitor** tab.</span></span>
2. <span data-ttu-id="50747-245">Selecteer **toevoegen metrische gegevens** in de taakbalk:</span><span class="sxs-lookup"><span data-stu-id="50747-245">Select **Add Metrics** in the task bar:</span></span>  
   <span data-ttu-id="50747-246">![Selecteer de metrische gegevens toevoegen][AddMetrics]</span><span class="sxs-lookup"><span data-stu-id="50747-246">![Select Add Metrics][AddMetrics]</span></span>
3. <span data-ttu-id="50747-247">Controleer de maatstaven voor prestaties die u wilt weergeven.</span><span class="sxs-lookup"><span data-stu-id="50747-247">Check the performance metrics you want to display.</span></span>
4. <span data-ttu-id="50747-248">Selecteer het vinkje om terug te keren naar de **Monitor** tabblad.</span><span class="sxs-lookup"><span data-stu-id="50747-248">Select the checkmark to return to the **Monitor** tab.</span></span>
5. <span data-ttu-id="50747-249">Selecteer de cirkel naast de metrische gegevens om weer te geven die metrische waarde in de grafiek.</span><span class="sxs-lookup"><span data-stu-id="50747-249">Select the circle next to the metric to display that metric's value in the graph.</span></span>  
   
    <span data-ttu-id="50747-250">Bijvoorbeeld, de **CPU-gebruik** metriek is niet beschikbaar; de uitvoer wordt niet weergegeven in de grafiek:</span><span class="sxs-lookup"><span data-stu-id="50747-250">For example, the **CPU Usage** metric is grayed out; its output is not displayed in the graph:</span></span>  
   <span data-ttu-id="50747-251">![CPU-gebruik metriek is niet beschikbaar][GrayedMetric]</span><span class="sxs-lookup"><span data-stu-id="50747-251">![CPU Usage metric is grayed out][GrayedMetric]</span></span>  
   
    <span data-ttu-id="50747-252">Selecteer de grijs uit cirkel om in te schakelen de **CPU-gebruik** metrische gegevens om de uitvoer ervan weergegeven in de grafiek weer te geven:</span><span class="sxs-lookup"><span data-stu-id="50747-252">Select the grayed out circle to enable the **CPU Usage** metric to display its output in the graph:</span></span>  
   <span data-ttu-id="50747-253">![CPU-gebruik metrische gegevens is ingeschakeld][EnabledMetric]</span><span class="sxs-lookup"><span data-stu-id="50747-253">![CPU Usage metric is enabled][EnabledMetric]</span></span>
6. <span data-ttu-id="50747-254">Als een waarde van de grafiek weergeven en de lijst, selecteert u **metriek verwijderen** in de taakbalk.</span><span class="sxs-lookup"><span data-stu-id="50747-254">To remove a metric from the display graph and the list, select **Delete Metric** in the task bar.</span></span> <span data-ttu-id="50747-255">Als u wilt de metrische gegevens weer toe te voegen aan de lijst, selecteert u **toevoegen metrische gegevens** in de taakbalk de metrische gegevens controleren en selecteer het vinkje om terug te keren naar de **Monitor** tabblad.</span><span class="sxs-lookup"><span data-stu-id="50747-255">To add the metric back to the list, select **Add Metrics** in the task bar, check the metric, and select the checkmark to return to the **Monitor** tab.</span></span> <span data-ttu-id="50747-256">Selecteer de grijs uit cirkel om in te schakelen, de metriek.</span><span class="sxs-lookup"><span data-stu-id="50747-256">Select the grayed out circle to enable the metric.</span></span>

## <span data-ttu-id="50747-257"><a name="Metrics"></a>Beschikbare metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="50747-257"><a name="Metrics"></a>Available Metrics</span></span>
<span data-ttu-id="50747-258">De volgende prestatiemeteritems/maatstaven voor prestaties zijn beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="50747-258">The following performance counters/metrics are available:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="50747-259"><strong>RountdTrip latentie</strong></span><span class="sxs-lookup"><span data-stu-id="50747-259"><strong>RountdTrip Latency</strong></span></span></td>
<td><span data-ttu-id="50747-260">Geeft de gemiddelde tijd in milliseconden (ms) voor het verwerken van een bericht van de tijd die het bericht wordt ontvangen totdat het bericht volledig is verwerkt door de BizTalk Service weer over alle bruggen.</span><span class="sxs-lookup"><span data-stu-id="50747-260">Displays the average time taken in milliseconds (ms) to process a message from the time the message is received until the message is fully processed by the BizTalk Service across all bridges.</span></span> <span data-ttu-id="50747-261">Alleen de verwerkte berichten worden meegeteld.</span><span class="sxs-lookup"><span data-stu-id="50747-261">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="50747-262">Wanneer de volgende gebeurtenissen plaatsvinden, wordt een tijdstempel gemaakt:</span><span class="sxs-lookup"><span data-stu-id="50747-262">When the following events occur, a timestamp is created:</span></span>
<ul>
<li><span data-ttu-id="50747-263">Bericht krijgt de gateway</span><span class="sxs-lookup"><span data-stu-id="50747-263">Message enters the gateway</span></span></li>
<li><span data-ttu-id="50747-264">Bericht wordt doorgestuurd naar de bestemming</span><span class="sxs-lookup"><span data-stu-id="50747-264">Message is routed to the destination</span></span></li>
<li><span data-ttu-id="50747-265">Bestemming reactie wordt ontvangen</span><span class="sxs-lookup"><span data-stu-id="50747-265">Destination response is received</span></span></li>
<li><span data-ttu-id="50747-266">Bestemming bevestiging antwoord verzonden naar de gateway</span><span class="sxs-lookup"><span data-stu-id="50747-266">Destination acknowledgement response sent to the gateway</span></span></li>
</ul>
<br/>
<span data-ttu-id="50747-267">Met deze metriek wordt het resultaat van de volgende berekening:</span><span class="sxs-lookup"><span data-stu-id="50747-267">This metric shows the result of the following calculation:</span></span>
<br/><br/>
<span data-ttu-id="50747-268">[Bestemming bevestiging antwoord verzonden naar de gateway] - [bericht krijgt de gateway]</span><span class="sxs-lookup"><span data-stu-id="50747-268">[Destination acknowledgement response sent to the gateway] - [Message enters the gateway]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-269"><strong>Fouten bij de bron</strong></span><span class="sxs-lookup"><span data-stu-id="50747-269"><strong>Failures At Source</strong></span></span></td>
<td><span data-ttu-id="50747-270">Geeft het totaal aantal berichten die niet door de BizTalk Service bij het ophalen van berichten van de bron-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="50747-270">Displays the total number of messages that failed by the BizTalk Service when pulling messages from the source endpoints.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-271"><strong>CPU-gebruik</strong></span><span class="sxs-lookup"><span data-stu-id="50747-271"><strong>CPU Usage</strong></span></span></td>
<td><span data-ttu-id="50747-272">Geeft het gemiddelde percentage processortijd van alle rolinstanties.</span><span class="sxs-lookup"><span data-stu-id="50747-272">Lists the average %Processor Time of all role instances.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-273"><strong>Latentie verwerken</strong></span><span class="sxs-lookup"><span data-stu-id="50747-273"><strong>Processing Latency</strong></span></span></td>
<td><span data-ttu-id="50747-274">Geeft de gemiddelde tijd In milliseconden (ms) in een bericht te verwerken door de BizTalk Service weer over alle bruggen, met uitzondering van de tijd doorgebracht in bestemmingen.</span><span class="sxs-lookup"><span data-stu-id="50747-274">Displays the average time taken In milliseconds (ms) to process a message by the BizTalk Service across all bridges, excluding the time spent in destinations.</span></span> <span data-ttu-id="50747-275">Alleen de verwerkte berichten worden meegeteld.</span><span class="sxs-lookup"><span data-stu-id="50747-275">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="50747-276">Wanneer elk van de volgende gebeurtenissen plaatsvinden, wordt er een tijdstempel gemaakt:</span><span class="sxs-lookup"><span data-stu-id="50747-276">When each of the following events occur, a timestamp is created:</span></span>

<ul>
<li><span data-ttu-id="50747-277">Bericht krijgt de gateway</span><span class="sxs-lookup"><span data-stu-id="50747-277">Message enters the gateway</span></span></li>
<li><span data-ttu-id="50747-278">Bericht wordt doorgestuurd naar de bestemming</span><span class="sxs-lookup"><span data-stu-id="50747-278">Message is routed to the destination</span></span></li>
<li><span data-ttu-id="50747-279">Bestemming reactie wordt ontvangen</span><span class="sxs-lookup"><span data-stu-id="50747-279">Destination response is received</span></span></li>
<li><span data-ttu-id="50747-280">Bestemming bevestiging antwoord verzonden naar de gateway</span><span class="sxs-lookup"><span data-stu-id="50747-280">Destination acknowledgement response sent to the gateway</span></span></li>
</ul>
<br/><span data-ttu-id="50747-281">Met deze metriek wordt het resultaat van de volgende berekening:</span><span class="sxs-lookup"><span data-stu-id="50747-281">This metric shows the result of the following calculation:</span></span><br/><br/>
<span data-ttu-id="50747-282">[Bestemming bevestiging antwoord verzonden naar de gateway] - [bericht krijgt de gateway] - [bestemming reactie wordt ontvangen] + [bericht wordt doorgestuurd naar de bestemming]</span><span class="sxs-lookup"><span data-stu-id="50747-282">[Destination acknowledgement response sent to the gateway] - [Message enters the gateway] - [Destination response is received] + [Message is routed to the destination]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-283"><strong>Fouten In het proces</strong></span><span class="sxs-lookup"><span data-stu-id="50747-283"><strong>Failures In Process</strong></span></span></td>
<td><span data-ttu-id="50747-284">Geeft het totaal aantal berichten die zijn mislukt bij de verwerking door de BizTalk Service via de bruggen binnen een periode.</span><span class="sxs-lookup"><span data-stu-id="50747-284">Displays the total number of messages that failed during processing by the BizTalk Service across all the bridges within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-285"><strong>Berichten die worden verzonden</strong></span><span class="sxs-lookup"><span data-stu-id="50747-285"><strong>Messages Sent</strong></span></span></td>
<td><span data-ttu-id="50747-286">Geeft het totaal aantal berichten is verzonden door de BizTalk Service via alle bruggen binnen een periode.</span><span class="sxs-lookup"><span data-stu-id="50747-286">Displays the total number of messages sent by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="50747-287">Met deze metriek wordt verhoogd wanneer er een bericht verzonden vanuit een pijplijn de route-bestemming heeft bereikt.</span><span class="sxs-lookup"><span data-stu-id="50747-287">This metric is incremented when a message sent from a pipeline reaches the route destination.</span></span> <span data-ttu-id="50747-288">Met deze metriek geeft niet aan een bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="50747-288">This metric does not indicate that a message is successfully processed.</span></span><br/><br/>
<span data-ttu-id="50747-289">In een Request-Reply-scenario worden de metriek wordt verhoogd als de bestemming route een ontvangstbevestiging teruggestuurd naar de pijplijn wordt.</span><span class="sxs-lookup"><span data-stu-id="50747-289">In a Request-Reply scenario, the metric is incremented when the route destination sends a receipt acknowledgement back to the pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-290"><strong>Berichten ontvangen</strong></span><span class="sxs-lookup"><span data-stu-id="50747-290"><strong>Messages Received</strong></span></span></td>
<td><span data-ttu-id="50747-291">Geeft het totaal aantal berichten is ontvangen door de BizTalk Service via alle bruggen binnen een periode.</span><span class="sxs-lookup"><span data-stu-id="50747-291">Displays the total number of messages received by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="50747-292">Met deze metriek wordt verhoogd wanneer een nieuw bericht wordt ontvangen door de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="50747-292">This metric is incremented when a new message is received by the pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-293"><strong>Berichten In proces</strong></span><span class="sxs-lookup"><span data-stu-id="50747-293"><strong>Messages In Process</strong></span></span></td>
<td><span data-ttu-id="50747-294">Geeft het totaal aantal berichten wordt verwerkt door de BizTalk Service binnen een periode.</span><span class="sxs-lookup"><span data-stu-id="50747-294">Displays the total number of messages currently being processed by the BizTalk Service within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="50747-295"><strong>Berichten die zijn verwerkt</strong></span><span class="sxs-lookup"><span data-stu-id="50747-295"><strong>Messages Processed</strong></span></span></td>
<td><span data-ttu-id="50747-296">Geeft het totale aantal berichten dat is verwerkt door de BizTalk Service via alle bruggen binnen een periode.</span><span class="sxs-lookup"><span data-stu-id="50747-296">Displays the total number of messages successfully processed by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="50747-297">Met deze metriek wordt verhoogd wanneer er een bericht wordt ontvangen door de pijplijn en is doorgestuurd naar de bestemming.</span><span class="sxs-lookup"><span data-stu-id="50747-297">This metric is incremented when a message is successfully received by the pipeline and successfully routed to the destination.</span></span></td>
</tr>
</table>


## <a name="scale"></a><span data-ttu-id="50747-298">Schalen</span><span class="sxs-lookup"><span data-stu-id="50747-298">Scale</span></span>
<span data-ttu-id="50747-299">U kunt toevoegen of verwijderen van het aantal eenheden dat door uw BizTalk Service gebruikt in het tabblad schaal.</span><span class="sxs-lookup"><span data-stu-id="50747-299">In the Scale tab, you can add or subtract the number of units used by your BizTalk Service.</span></span> <span data-ttu-id="50747-300">Er is standaard één eenheid worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="50747-300">By default, there is one Unit configured.</span></span> <span data-ttu-id="50747-301">Extra eenheden kunnen worden toegevoegd aan het schalen van uw BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="50747-301">Additional Units can be added to scale your BizTalk Service.</span></span> <span data-ttu-id="50747-302">Als u de schaal verhoogt, bent u doorvoer te verbeteren.</span><span class="sxs-lookup"><span data-stu-id="50747-302">When you increase the scale, you are increasing throughput.</span></span> <span data-ttu-id="50747-303">De hoeveelheid resources verhoogt ook, inclusief geïmplementeerde bruggen, overeenkomsten, LOB-verbindingen en verwerkingskracht.</span><span class="sxs-lookup"><span data-stu-id="50747-303">The amount of resources also increases, including deployed bridges, agreements, LOB connections, and processing power.</span></span> <span data-ttu-id="50747-304">Bijvoorbeeld, verhoogt u de schaal van 1 eenheid tot 2 eenheden.</span><span class="sxs-lookup"><span data-stu-id="50747-304">For example, you increase the scale from 1 Unit to 2 Units.</span></span> <span data-ttu-id="50747-305">In dit geval kunt u dubbele het aantal bruggen implementeren, dubbelklik de overeenkomsten, dubbelklik de LOB-verbindingen en dubbelklik de verwerkingskracht.</span><span class="sxs-lookup"><span data-stu-id="50747-305">In this situation, you can deploy double the number of bridges, double the agreements, double the LOB connections, and double the processing power.</span></span>

<span data-ttu-id="50747-306">Sommige edities van BizTalk bieden geen een optie voor schaal.</span><span class="sxs-lookup"><span data-stu-id="50747-306">Some BizTalk editions do not offer a scale option.</span></span> <span data-ttu-id="50747-307">In dit geval is één eenheid toegestaan.</span><span class="sxs-lookup"><span data-stu-id="50747-307">In this situation, one Unit is permitted.</span></span> <span data-ttu-id="50747-308">Om te bepalen hoeveel eenheden uw editie kan worden geschaald, verwijzen naar [BizTalk Services: grafiek van edities](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="50747-308">To determine how many units your edition can be scaled, refer to [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>

<span data-ttu-id="50747-309">Het aantal eenheden verhogen mogelijk van invloed prijzen.</span><span class="sxs-lookup"><span data-stu-id="50747-309">Increasing the number of units may impact pricing.</span></span> <span data-ttu-id="50747-310">Als u de eenheden verhogen, selecteer **opslaan** wordt een bericht weergegeven dat aangeeft of facturering wordt beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="50747-310">If you increase the Units, selecting **Save** displays a message that tells you if billing is impacted.</span></span> <span data-ttu-id="50747-311">U wordt dan kiezen om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="50747-311">You then choose to continue.</span></span> <span data-ttu-id="50747-312">Wanneer u het aantal eenheden, de BizTalk Service status is gewijzigd van actief in Updating verhogen.</span><span class="sxs-lookup"><span data-stu-id="50747-312">When you increase the number of Units, the BizTalk Service status changes from Active to Updating.</span></span> <span data-ttu-id="50747-313">Uw BizTalk Service blijft uitvoeren in de status bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="50747-313">In the Updating state, your BizTalk Service continues to run.</span></span>

<span data-ttu-id="50747-314">[BizTalk Services: Grafiek van edities](biztalk-editions-feature-chart.md) definieert een 'eenheid'.</span><span class="sxs-lookup"><span data-stu-id="50747-314">[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) defines a "Unit".</span></span>

## <a name="configure"></a><span data-ttu-id="50747-315">Configureren</span><span class="sxs-lookup"><span data-stu-id="50747-315">Configure</span></span>
<span data-ttu-id="50747-316">Geldt niet voor hybride verbindingen.</span><span class="sxs-lookup"><span data-stu-id="50747-316">Does not apply to Hybrid Connections.</span></span>

<span data-ttu-id="50747-317">De back-Status wordt ingesteld op None of automatisch.</span><span class="sxs-lookup"><span data-stu-id="50747-317">Sets the Backup Status to None or Automatic.</span></span> <span data-ttu-id="50747-318">Als op None is ingesteld, worden geen back-ups automatisch gemaakt.</span><span class="sxs-lookup"><span data-stu-id="50747-318">When set to None, no backups are automatically created.</span></span> <span data-ttu-id="50747-319">Als de waarde op automatisch, configureert u de back-uplocatie, de frequentie van de back-up, en hoe lang de back-bestanden moeten worden behouden.</span><span class="sxs-lookup"><span data-stu-id="50747-319">When set to Automatic, you configure the backup location, the frequency of the backup, and how long to keep the backup files.</span></span> 

<span data-ttu-id="50747-320">[BizTalk Services: Back-up en herstel](biztalk-backup-restore.md) bevat de details.</span><span class="sxs-lookup"><span data-stu-id="50747-320">[BizTalk Services: Backup and Restore](biztalk-backup-restore.md) provides the details.</span></span> 

## <span data-ttu-id="50747-321"><a name="HybridConnections"></a>Hybride verbindingen</span><span class="sxs-lookup"><span data-stu-id="50747-321"><a name="HybridConnections"></a>Hybrid Connections</span></span>
<span data-ttu-id="50747-322">Hybride verbinding wordt een Azure-toepassing, zoals Web-Apps of mobiele Apps in Azure App Service met een on-premises resource die gebruikmaakt van een statische TCP-poort, zoals SQL Server, MySQL, HTTP-Web-API's en de meeste aangepaste webservices.</span><span class="sxs-lookup"><span data-stu-id="50747-322">Hybrid Connections connect an Azure application, like Web Apps or Mobile Apps in Azure App Service, to an on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="50747-323">Hybride verbindingen worden beheerd in BizTalk Services in de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="50747-323">Hybrid Connections are managed in  BizTalk Services in the Azure classic portal.</span></span>

<span data-ttu-id="50747-324">Zie voor informatie over het maken van hybride verbindingen in Azure App Service [toegang tot on-premises resources met behulp van hybride verbindingen in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="50747-324">To create Hybrid Connections in Azure App Service, see [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

<span data-ttu-id="50747-325">Als u wilt maken of beheren van hybride verbindingen in de Azure BizTalk Services, Zie [hybride verbindingen](integration-hybrid-connection-overview.md).</span><span class="sxs-lookup"><span data-stu-id="50747-325">To create or manage Hybrid Connections in Azure BizTalk Services, see [Hybrid Connections](integration-hybrid-connection-overview.md).</span></span>

## <a name="next"></a><span data-ttu-id="50747-326">Volgende</span><span class="sxs-lookup"><span data-stu-id="50747-326">Next</span></span>
<span data-ttu-id="50747-327">Nu dat u bekend met de verschillende tabbladen bent, kunt u meer informatie over de functies van Azure BizTalk Services:</span><span class="sxs-lookup"><span data-stu-id="50747-327">Now that you're familiar with the different tabs, you can learn more about the Azure BizTalk Services features:</span></span>

* [<span data-ttu-id="50747-328">BizTalk Services: beperking</span><span class="sxs-lookup"><span data-stu-id="50747-328">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)  
* [<span data-ttu-id="50747-329">BizTalk Services: naam en sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="50747-329">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)  
* [<span data-ttu-id="50747-330">BizTalk Services: back-ups maken en herstellen</span><span class="sxs-lookup"><span data-stu-id="50747-330">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)

## <a name="see-also"></a><span data-ttu-id="50747-331">Zie ook</span><span class="sxs-lookup"><span data-stu-id="50747-331">See Also</span></span>
* [<span data-ttu-id="50747-332">Hybride verbindingen</span><span class="sxs-lookup"><span data-stu-id="50747-332">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)  
* [<span data-ttu-id="50747-333">BizTalk Services: Developer, Basic, Standard en Premium-edities grafiek</span><span class="sxs-lookup"><span data-stu-id="50747-333">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
* [<span data-ttu-id="50747-334">BizTalk Services: Inrichten met behulp van Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="50747-334">BizTalk Services: Provisioning Using Azure classic portal</span></span>](biztalk-provision-services.md)  
* [<span data-ttu-id="50747-335">BizTalk Services: Grafiek van de status van de BizTalk-Service</span><span class="sxs-lookup"><span data-stu-id="50747-335">BizTalk Services: BizTalk Service State Chart</span></span>](biztalk-service-state-chart.md)  
* [<span data-ttu-id="50747-336">De Azure BizTalk Services SDK gaan gebruiken</span><span class="sxs-lookup"><span data-stu-id="50747-336">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

