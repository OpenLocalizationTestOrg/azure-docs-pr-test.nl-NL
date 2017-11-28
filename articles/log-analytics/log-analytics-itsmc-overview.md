---
title: Service Management-Connector in OMS aaaIT | Microsoft Docs
description: Hallo IT Service Management-Connector toocentrally controleren en beheren van Hallo ITSM werkitems in OMS en eventuele problemen snel worden opgelost.
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a><span data-ttu-id="851a1-103">Centraal beheren van werkitems ITSM met IT Service Management-Connector (Preview)</span><span class="sxs-lookup"><span data-stu-id="851a1-103">Centrally manage ITSM work items using IT Service Management Connector (Preview)</span></span>

![Symbool van IT-Service Management-Connector](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="851a1-105">U kunt Hallo IT Service Management-Connector (ITSMC) in de OMS-logboekanalyse toocentrally monitor gebruiken en beheren van werkitems in uw ITSM producten/services.</span><span class="sxs-lookup"><span data-stu-id="851a1-105">You can use hello IT Service Management Connector (ITSMC) in OMS Log Analytics toocentrally monitor and manage work items across your ITSM products/services.</span></span>

<span data-ttu-id="851a1-106">Hallo IT Service Management-Connector integreert uw bestaande IT Service Management (ITSM)-producten en services met OMS-logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="851a1-106">hello IT Service Management Connector integrates your existing IT Service Management (ITSM) products and services with OMS Log Analytics.</span></span>  <span data-ttu-id="851a1-107">Hallo-oplossing heeft bidirectionele integratie met ITSM producten/services, waarbij het biedt Hallo OMS-gebruikers een optie toocreate incidenten, waarschuwingen of gebeurtenissen in ITSM oplossing.</span><span class="sxs-lookup"><span data-stu-id="851a1-107">hello solution has bidirectional integration with ITSM products/services, where it provides hello OMS users an option toocreate incidents, alerts, or events in ITSM solution.</span></span> <span data-ttu-id="851a1-108">Hallo connector ook gegevens worden geïmporteerd zoals incidenten en wijzigingsaanvragen van ITSM oplossing in OMS-logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="851a1-108">hello connector also  imports data such as incidents, and change requests from ITSM solution into OMS Log Analytics.</span></span>

<span data-ttu-id="851a1-109">U kunt met de IT-Service Management-Connector:</span><span class="sxs-lookup"><span data-stu-id="851a1-109">With IT Service Management Connector, you can:</span></span>

  - <span data-ttu-id="851a1-110">Centraal bewaken en beheren van werkitems voor ITSM producten/services in uw organisatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="851a1-110">Centrally monitor and manage work items for ITSM products/services used across your organization.</span></span>
  - <span data-ttu-id="851a1-111">Maken in ITSM ITSM werkitems (zoals waarschuwing, gebeurtenis, incident) van OMS-waarschuwingen en via de zoekfunctie.</span><span class="sxs-lookup"><span data-stu-id="851a1-111">Create ITSM work items (like alert, event, incident) in ITSM from OMS alerts and through log search.</span></span>
  - <span data-ttu-id="851a1-112">Lezen van incidenten en wijzigingsaanvragen van uw oplossing ITSM en correleren met relevante logboekgegevens in de werkruimte voor logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="851a1-112">Read incidents and change requests from your ITSM solution and correlate with relevant log data in Log Analytics workspace.</span></span>
  - <span data-ttu-id="851a1-113">Alle gebeurtenissen onverwachte of ongebruikelijke zoeken en deze op te lossen voordat eindgebruikers Hallo aanroepen en deze toohello helpdesk rapporteert.</span><span class="sxs-lookup"><span data-stu-id="851a1-113">Find any unexpected and unusual events and resolve them, even before hello end users call and report them toohello helpdesk.</span></span>
  - <span data-ttu-id="851a1-114">Werk items gegevens importeren in Log Analytics en rapporten van prestatie-indicator (KPI) maken.</span><span class="sxs-lookup"><span data-stu-id="851a1-114">Import work items data into Log Analytics and create key performance indicator (KPI) reports.</span></span>  <span data-ttu-id="851a1-115">U gebruikt deze rapporten, kunt u zien, beoordelen en reageren op een aantal belangrijke zaken zoals evaluatie van schadelijke software.</span><span class="sxs-lookup"><span data-stu-id="851a1-115">Using these reports, you can identify, assess and act on several important items such as malware assessment.</span></span>
  - <span data-ttu-id="851a1-116">Samengestelde dashboards voor meer inzicht weergeven op incidenten, wijzigingsaanvragen en betrokken systemen.</span><span class="sxs-lookup"><span data-stu-id="851a1-116">View curated dashboards for deeper insights on incidents, change requests and impacted systems.</span></span>
  - <span data-ttu-id="851a1-117">Problemen sneller door correleren met andere beheeroplossingen voor in de werkruimte voor logboekanalyse Hallo.</span><span class="sxs-lookup"><span data-stu-id="851a1-117">Troubleshoot faster by correlating with other management solutions in hello Log Analytics workspace.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="851a1-118">Vereisten</span><span class="sxs-lookup"><span data-stu-id="851a1-118">Prerequisites</span></span>

<span data-ttu-id="851a1-119">tooimport hello ITSM werkitems in OMS Log Analytics, Hallo oplossing vereist een verbinding tussen Hallo IT Service Management-Connector in Hallo OMS en Hallo IT SM product of dienst van waaruit u Hallo-werkitems importeert.</span><span class="sxs-lookup"><span data-stu-id="851a1-119">tooimport hello ITSM work items into OMS Log Analytics, hello solution requires a connection between hello IT Service Management Connector in hello OMS and hello IT SM product/service from which you import hello work items.</span></span>


## <a name="configuration"></a><span data-ttu-id="851a1-120">Configuratie</span><span class="sxs-lookup"><span data-stu-id="851a1-120">Configuration</span></span>

<span data-ttu-id="851a1-121">Add Hallo IT Service Management-Connector oplossing tooyour OMS werkruimte, met behulp van Hallo-proces dat wordt beschreven in [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="851a1-121">Add hello IT Service Management Connector solution tooyour OMS work space, using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="851a1-122">IT-Service Management-Connector tegel zoals u ziet in de galerie met Hallo oplossingen:</span><span class="sxs-lookup"><span data-stu-id="851a1-122">IT Service Management Connector tile as you see in hello Solutions gallery:</span></span>

![Connector-tegel](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

<span data-ttu-id="851a1-124">Na een geslaagde toevoeging, ziet u Hallo IT Service Management-Connector onder **OMS** > **instellingen** > **verbonden bronnen.**</span><span class="sxs-lookup"><span data-stu-id="851a1-124">After successful addition, you will see hello IT Service Management Connector under **OMS** > **Settings** > **Connected Sources.**</span></span>

![ITSMC verbonden](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> <span data-ttu-id="851a1-126">Standaard vernieuwt Hallo IT Service Management-Connector van Hallo verbinding gegevens eenmaal in elke 24 uur.</span><span class="sxs-lookup"><span data-stu-id="851a1-126">By default, hello IT Service Management Connector refreshes hello connection's data once in every 24 hours.</span></span> <span data-ttu-id="851a1-127">toorefresh uw verbinding gegevens direct voor een bewerkingen of de sjabloon die updates die u aanbrengt, klikt u op Hallo vernieuwen weergegeven knop volgende tooyour verbinding.</span><span class="sxs-lookup"><span data-stu-id="851a1-127">toorefresh your connection's data instantly for any edits or template updates that you make, click hello refresh button displayed next tooyour connection.</span></span>

 ![ITSMC vernieuwen](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a><span data-ttu-id="851a1-129">Management packs</span><span class="sxs-lookup"><span data-stu-id="851a1-129">Management packs</span></span>
<span data-ttu-id="851a1-130">Deze oplossing is niet vereist voor alle management packs.</span><span class="sxs-lookup"><span data-stu-id="851a1-130">This solution does not require any management packs.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="851a1-131">Verbonden bronnen</span><span class="sxs-lookup"><span data-stu-id="851a1-131">Connected sources</span></span>

<span data-ttu-id="851a1-132">Hallo worden volgende ITSM producten/services ondersteund door Hallo IT Service Management-Connector:</span><span class="sxs-lookup"><span data-stu-id="851a1-132">hello following ITSM products/services are supported by hello IT Service Management Connector:</span></span>

- [<span data-ttu-id="851a1-133">System Center Service Manager (SCSM)</span><span class="sxs-lookup"><span data-stu-id="851a1-133">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="851a1-134">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="851a1-134">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="851a1-135">Provance</span><span class="sxs-lookup"><span data-stu-id="851a1-135">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [<span data-ttu-id="851a1-136">Cherwell</span><span class="sxs-lookup"><span data-stu-id="851a1-136">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a><span data-ttu-id="851a1-137">Met behulp van Hallo-oplossing</span><span class="sxs-lookup"><span data-stu-id="851a1-137">Using hello solution</span></span>

<span data-ttu-id="851a1-138">Als u verbinding Hallo OMS IT Service Management-Connector hebt gemaakt met uw service ITSM, begint Hallo Log Analytics-services Hallo gegevensverzameling van Hallo verbonden ITSM producten/service.</span><span class="sxs-lookup"><span data-stu-id="851a1-138">Once you connect hello OMS IT Service Management Connector with your ITSM service, hello Log Analytics services starts gathering hello data from hello connected ITSM products/service.</span></span>

> [!NOTE]
> - <span data-ttu-id="851a1-139">Gegevens die zijn geïmporteerd door de oplossing IT Service Management-Connector wordt weergegeven in logboekanalyse als gebeurtenissen met de naam **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="851a1-139">Data imported by IT Service Management Connector solution appears in Log Analytics as events named **ServiceDesk_CL**.</span></span>
- <span data-ttu-id="851a1-140">Gebeurtenis bevat een veld met de naam **ServiceDeskWorkItemType_s**.</span><span class="sxs-lookup"><span data-stu-id="851a1-140">Event contains a field named **ServiceDeskWorkItemType_s**.</span></span> <span data-ttu-id="851a1-141">die kan duren voordat de waarde als een incident of wijzigingsaanvraag, afhankelijk van Hallo werkitem gegevens in Hallo **ServiceDesk_CL** gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="851a1-141">which can take its value as incident, or change request, depending on hello work item data contained in hello **ServiceDesk_CL** event.</span></span>

## <a name="input-data"></a><span data-ttu-id="851a1-142">Invoergegevens</span><span class="sxs-lookup"><span data-stu-id="851a1-142">Input data</span></span>
<span data-ttu-id="851a1-143">Werkitems die is geïmporteerd uit Hallo ITSM producten/services.</span><span class="sxs-lookup"><span data-stu-id="851a1-143">Work items imported from hello ITSM products/services.</span></span>

<span data-ttu-id="851a1-144">Hallo ziet hieronder u voorbeelden van gegevens die worden verzameld door Hallo IT Service Management-connector:</span><span class="sxs-lookup"><span data-stu-id="851a1-144">hello following information shows examples of data gathered by hello IT Service Management connector:</span></span>

> [!NOTE]
> <span data-ttu-id="851a1-145">Afhankelijk van Hallo type werkitem geïmporteerd in Log Analytics **ServiceDesk_CL** Hallo volgende velden bevat:</span><span class="sxs-lookup"><span data-stu-id="851a1-145">Depending on hello work item type imported into Log Analytics, **ServiceDesk_CL** contains hello following fields:</span></span>

<span data-ttu-id="851a1-146">**Werkitem:** **incidenten**</span><span class="sxs-lookup"><span data-stu-id="851a1-146">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="851a1-147">ServiceDeskWorkItemType_s = "Incident"</span><span class="sxs-lookup"><span data-stu-id="851a1-147">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="851a1-148">**Velden**</span><span class="sxs-lookup"><span data-stu-id="851a1-148">**Fields**</span></span>

- <span data-ttu-id="851a1-149">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="851a1-149">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="851a1-150">Helpdesk-service-ID</span><span class="sxs-lookup"><span data-stu-id="851a1-150">Service Desk ID</span></span>
- <span data-ttu-id="851a1-151">Status</span><span class="sxs-lookup"><span data-stu-id="851a1-151">State</span></span>
- <span data-ttu-id="851a1-152">Urgentie</span><span class="sxs-lookup"><span data-stu-id="851a1-152">Urgency</span></span>
- <span data-ttu-id="851a1-153">Impact</span><span class="sxs-lookup"><span data-stu-id="851a1-153">Impact</span></span>
- <span data-ttu-id="851a1-154">Prioriteit</span><span class="sxs-lookup"><span data-stu-id="851a1-154">Priority</span></span>
- <span data-ttu-id="851a1-155">Escalatie</span><span class="sxs-lookup"><span data-stu-id="851a1-155">Escalation</span></span>
- <span data-ttu-id="851a1-156">Gemaakt door</span><span class="sxs-lookup"><span data-stu-id="851a1-156">Created By</span></span>
- <span data-ttu-id="851a1-157">Opgelost door</span><span class="sxs-lookup"><span data-stu-id="851a1-157">Resolved By</span></span>
- <span data-ttu-id="851a1-158">Gesloten door</span><span class="sxs-lookup"><span data-stu-id="851a1-158">Closed By</span></span>
- <span data-ttu-id="851a1-159">Bron</span><span class="sxs-lookup"><span data-stu-id="851a1-159">Source</span></span>
- <span data-ttu-id="851a1-160">Toegewezen aan</span><span class="sxs-lookup"><span data-stu-id="851a1-160">Assigned To</span></span>
- <span data-ttu-id="851a1-161">Category</span><span class="sxs-lookup"><span data-stu-id="851a1-161">Category</span></span>
- <span data-ttu-id="851a1-162">Titel</span><span class="sxs-lookup"><span data-stu-id="851a1-162">Title</span></span>
- <span data-ttu-id="851a1-163">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="851a1-163">Description</span></span>
- <span data-ttu-id="851a1-164">Datum gemaakt</span><span class="sxs-lookup"><span data-stu-id="851a1-164">Created Date</span></span>
- <span data-ttu-id="851a1-165">Datum gesloten</span><span class="sxs-lookup"><span data-stu-id="851a1-165">Closed Date</span></span>
- <span data-ttu-id="851a1-166">Datum opgelost</span><span class="sxs-lookup"><span data-stu-id="851a1-166">Resolved Date</span></span>
- <span data-ttu-id="851a1-167">Datum van laatste wijziging</span><span class="sxs-lookup"><span data-stu-id="851a1-167">Last Modified Date</span></span>
- <span data-ttu-id="851a1-168">Computer</span><span class="sxs-lookup"><span data-stu-id="851a1-168">Computer</span></span>


<span data-ttu-id="851a1-169">**Werkitem:** **wijzigingsaanvragen**</span><span class="sxs-lookup"><span data-stu-id="851a1-169">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="851a1-170">ServiceDeskWorkItemType_s = "ChangeRequest"</span><span class="sxs-lookup"><span data-stu-id="851a1-170">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="851a1-171">**Velden**</span><span class="sxs-lookup"><span data-stu-id="851a1-171">**Fields**</span></span>
- <span data-ttu-id="851a1-172">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="851a1-172">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="851a1-173">Helpdesk-service-ID</span><span class="sxs-lookup"><span data-stu-id="851a1-173">Service Desk ID</span></span>
- <span data-ttu-id="851a1-174">Gemaakt door</span><span class="sxs-lookup"><span data-stu-id="851a1-174">Created By</span></span>
- <span data-ttu-id="851a1-175">Gesloten door</span><span class="sxs-lookup"><span data-stu-id="851a1-175">Closed By</span></span>
- <span data-ttu-id="851a1-176">Bron</span><span class="sxs-lookup"><span data-stu-id="851a1-176">Source</span></span>
- <span data-ttu-id="851a1-177">Toegewezen aan</span><span class="sxs-lookup"><span data-stu-id="851a1-177">Assigned To</span></span>
- <span data-ttu-id="851a1-178">Titel</span><span class="sxs-lookup"><span data-stu-id="851a1-178">Title</span></span>
- <span data-ttu-id="851a1-179">Type</span><span class="sxs-lookup"><span data-stu-id="851a1-179">Type</span></span>
- <span data-ttu-id="851a1-180">Category</span><span class="sxs-lookup"><span data-stu-id="851a1-180">Category</span></span>
- <span data-ttu-id="851a1-181">Status</span><span class="sxs-lookup"><span data-stu-id="851a1-181">State</span></span>
- <span data-ttu-id="851a1-182">Escalatie</span><span class="sxs-lookup"><span data-stu-id="851a1-182">Escalation</span></span>
- <span data-ttu-id="851a1-183">Status conflict</span><span class="sxs-lookup"><span data-stu-id="851a1-183">Conflict Status</span></span>
- <span data-ttu-id="851a1-184">Urgentie</span><span class="sxs-lookup"><span data-stu-id="851a1-184">Urgency</span></span>
- <span data-ttu-id="851a1-185">Prioriteit</span><span class="sxs-lookup"><span data-stu-id="851a1-185">Priority</span></span>
- <span data-ttu-id="851a1-186">Risico 's</span><span class="sxs-lookup"><span data-stu-id="851a1-186">Risk</span></span>
- <span data-ttu-id="851a1-187">Impact</span><span class="sxs-lookup"><span data-stu-id="851a1-187">Impact</span></span>
- <span data-ttu-id="851a1-188">Toegewezen aan</span><span class="sxs-lookup"><span data-stu-id="851a1-188">Assigned To</span></span>
- <span data-ttu-id="851a1-189">Datum gemaakt</span><span class="sxs-lookup"><span data-stu-id="851a1-189">Created Date</span></span>
- <span data-ttu-id="851a1-190">Datum gesloten</span><span class="sxs-lookup"><span data-stu-id="851a1-190">Closed Date</span></span>
- <span data-ttu-id="851a1-191">Datum van laatste wijziging</span><span class="sxs-lookup"><span data-stu-id="851a1-191">Last Modified Date</span></span>
- <span data-ttu-id="851a1-192">Gevraagde datum</span><span class="sxs-lookup"><span data-stu-id="851a1-192">Requested Date</span></span>
- <span data-ttu-id="851a1-193">Geplande begindatum</span><span class="sxs-lookup"><span data-stu-id="851a1-193">Planned Start Date</span></span>
- <span data-ttu-id="851a1-194">Geplande einddatum</span><span class="sxs-lookup"><span data-stu-id="851a1-194">Planned End Date</span></span>
- <span data-ttu-id="851a1-195">Werk de begindatum</span><span class="sxs-lookup"><span data-stu-id="851a1-195">Work Start Date</span></span>
- <span data-ttu-id="851a1-196">Werk einddatum</span><span class="sxs-lookup"><span data-stu-id="851a1-196">Work End Date</span></span>
- <span data-ttu-id="851a1-197">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="851a1-197">Description</span></span>
- <span data-ttu-id="851a1-198">Computer</span><span class="sxs-lookup"><span data-stu-id="851a1-198">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="851a1-199">Uitvoergegevens voor een incident ServiceNow</span><span class="sxs-lookup"><span data-stu-id="851a1-199">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="851a1-200">OMS-veld</span><span class="sxs-lookup"><span data-stu-id="851a1-200">OMS field</span></span> | <span data-ttu-id="851a1-201">ITSM veld</span><span class="sxs-lookup"><span data-stu-id="851a1-201">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="851a1-202">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="851a1-202">ServiceDeskId_s</span></span>| <span data-ttu-id="851a1-203">Aantal</span><span class="sxs-lookup"><span data-stu-id="851a1-203">Number</span></span> |
| <span data-ttu-id="851a1-204">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="851a1-204">IncidentState_s</span></span> | <span data-ttu-id="851a1-205">Status</span><span class="sxs-lookup"><span data-stu-id="851a1-205">State</span></span> |
| <span data-ttu-id="851a1-206">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="851a1-206">Urgency_s</span></span> |<span data-ttu-id="851a1-207">Urgentie</span><span class="sxs-lookup"><span data-stu-id="851a1-207">Urgency</span></span> |
| <span data-ttu-id="851a1-208">Impact_s</span><span class="sxs-lookup"><span data-stu-id="851a1-208">Impact_s</span></span> |<span data-ttu-id="851a1-209">Impact</span><span class="sxs-lookup"><span data-stu-id="851a1-209">Impact</span></span>|
| <span data-ttu-id="851a1-210">Priority_s</span><span class="sxs-lookup"><span data-stu-id="851a1-210">Priority_s</span></span> | <span data-ttu-id="851a1-211">Prioriteit</span><span class="sxs-lookup"><span data-stu-id="851a1-211">Priority</span></span> |
| <span data-ttu-id="851a1-212">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="851a1-212">CreatedBy_s</span></span> | <span data-ttu-id="851a1-213">Geopend door</span><span class="sxs-lookup"><span data-stu-id="851a1-213">Opened by</span></span> |
| <span data-ttu-id="851a1-214">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="851a1-214">ResolvedBy_s</span></span> | <span data-ttu-id="851a1-215">Opgelost door</span><span class="sxs-lookup"><span data-stu-id="851a1-215">Resolved by</span></span>|
| <span data-ttu-id="851a1-216">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="851a1-216">ClosedBy_s</span></span>  | <span data-ttu-id="851a1-217">Gesloten door</span><span class="sxs-lookup"><span data-stu-id="851a1-217">Closed by</span></span> |
| <span data-ttu-id="851a1-218">Source_s</span><span class="sxs-lookup"><span data-stu-id="851a1-218">Source_s</span></span>| <span data-ttu-id="851a1-219">Neem contact op met het type</span><span class="sxs-lookup"><span data-stu-id="851a1-219">Contact type</span></span> |
| <span data-ttu-id="851a1-220">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="851a1-220">AssignedTo_s</span></span> | <span data-ttu-id="851a1-221">Te worden toegewezen</span><span class="sxs-lookup"><span data-stu-id="851a1-221">Assigned too</span></span> |
| <span data-ttu-id="851a1-222">Category_s</span><span class="sxs-lookup"><span data-stu-id="851a1-222">Category_s</span></span> | <span data-ttu-id="851a1-223">Category</span><span class="sxs-lookup"><span data-stu-id="851a1-223">Category</span></span> |
| <span data-ttu-id="851a1-224">Title_s</span><span class="sxs-lookup"><span data-stu-id="851a1-224">Title_s</span></span>|  <span data-ttu-id="851a1-225">Korte beschrijving</span><span class="sxs-lookup"><span data-stu-id="851a1-225">Short description</span></span> |
| <span data-ttu-id="851a1-226">Description_s</span><span class="sxs-lookup"><span data-stu-id="851a1-226">Description_s</span></span>|  <span data-ttu-id="851a1-227">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="851a1-227">Notes</span></span> |
| <span data-ttu-id="851a1-228">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="851a1-228">CreatedDate_t</span></span>|  <span data-ttu-id="851a1-229">Geopend</span><span class="sxs-lookup"><span data-stu-id="851a1-229">Opened</span></span> |
| <span data-ttu-id="851a1-230">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="851a1-230">ClosedDate_t</span></span>| <span data-ttu-id="851a1-231">gesloten</span><span class="sxs-lookup"><span data-stu-id="851a1-231">closed</span></span>|
| <span data-ttu-id="851a1-232">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="851a1-232">ResolvedDate_t</span></span>|<span data-ttu-id="851a1-233">Opgelost</span><span class="sxs-lookup"><span data-stu-id="851a1-233">Resolved</span></span>|
| <span data-ttu-id="851a1-234">Computer</span><span class="sxs-lookup"><span data-stu-id="851a1-234">Computer</span></span>  | <span data-ttu-id="851a1-235">configuratie-item</span><span class="sxs-lookup"><span data-stu-id="851a1-235">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="851a1-236">Wijzigingsaanvraag uitvoergegevens voor een ServiceNow</span><span class="sxs-lookup"><span data-stu-id="851a1-236">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="851a1-237">OMS-veld</span><span class="sxs-lookup"><span data-stu-id="851a1-237">OMS field</span></span> | <span data-ttu-id="851a1-238">ITSM veld</span><span class="sxs-lookup"><span data-stu-id="851a1-238">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="851a1-239">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="851a1-239">ServiceDeskId_s</span></span>| <span data-ttu-id="851a1-240">Aantal</span><span class="sxs-lookup"><span data-stu-id="851a1-240">Number</span></span> |
| <span data-ttu-id="851a1-241">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="851a1-241">CreatedBy_s</span></span> | <span data-ttu-id="851a1-242">Aangevraagd door</span><span class="sxs-lookup"><span data-stu-id="851a1-242">Requested by</span></span> |
| <span data-ttu-id="851a1-243">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="851a1-243">ClosedBy_s</span></span> | <span data-ttu-id="851a1-244">Gesloten door</span><span class="sxs-lookup"><span data-stu-id="851a1-244">Closed by</span></span> |
| <span data-ttu-id="851a1-245">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="851a1-245">AssignedTo_s</span></span> | <span data-ttu-id="851a1-246">Te worden toegewezen</span><span class="sxs-lookup"><span data-stu-id="851a1-246">Assigned too</span></span> |
| <span data-ttu-id="851a1-247">Title_s</span><span class="sxs-lookup"><span data-stu-id="851a1-247">Title_s</span></span>|  <span data-ttu-id="851a1-248">Korte beschrijving</span><span class="sxs-lookup"><span data-stu-id="851a1-248">Short description</span></span> |
| <span data-ttu-id="851a1-249">Type_s</span><span class="sxs-lookup"><span data-stu-id="851a1-249">Type_s</span></span>|  <span data-ttu-id="851a1-250">Type</span><span class="sxs-lookup"><span data-stu-id="851a1-250">Type</span></span> |
| <span data-ttu-id="851a1-251">Category_s</span><span class="sxs-lookup"><span data-stu-id="851a1-251">Category_s</span></span>|  <span data-ttu-id="851a1-252">Catgory</span><span class="sxs-lookup"><span data-stu-id="851a1-252">Catgory</span></span> |
| <span data-ttu-id="851a1-253">CRState_s</span><span class="sxs-lookup"><span data-stu-id="851a1-253">CRState_s</span></span>|  <span data-ttu-id="851a1-254">Status</span><span class="sxs-lookup"><span data-stu-id="851a1-254">State</span></span>|
| <span data-ttu-id="851a1-255">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="851a1-255">Urgency_s</span></span>|  <span data-ttu-id="851a1-256">Urgentie</span><span class="sxs-lookup"><span data-stu-id="851a1-256">Urgency</span></span> |
| <span data-ttu-id="851a1-257">Priority_s</span><span class="sxs-lookup"><span data-stu-id="851a1-257">Priority_s</span></span>| <span data-ttu-id="851a1-258">Prioriteit</span><span class="sxs-lookup"><span data-stu-id="851a1-258">Priority</span></span>|
| <span data-ttu-id="851a1-259">Risk_s</span><span class="sxs-lookup"><span data-stu-id="851a1-259">Risk_s</span></span>| <span data-ttu-id="851a1-260">Risico 's</span><span class="sxs-lookup"><span data-stu-id="851a1-260">Risk</span></span>|
| <span data-ttu-id="851a1-261">Impact_s</span><span class="sxs-lookup"><span data-stu-id="851a1-261">Impact_s</span></span>| <span data-ttu-id="851a1-262">Impact</span><span class="sxs-lookup"><span data-stu-id="851a1-262">Impact</span></span>|
| <span data-ttu-id="851a1-263">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="851a1-263">RequestedDate_t</span></span>  | <span data-ttu-id="851a1-264">Aangevraagd door datum</span><span class="sxs-lookup"><span data-stu-id="851a1-264">Requested by date</span></span> |
| <span data-ttu-id="851a1-265">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="851a1-265">ClosedDate_t</span></span> | <span data-ttu-id="851a1-266">Datum gesloten</span><span class="sxs-lookup"><span data-stu-id="851a1-266">Closed date</span></span> |
| <span data-ttu-id="851a1-267">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="851a1-267">PlannedStartDate_t</span></span>  |     <span data-ttu-id="851a1-268">Geplande begindatum</span><span class="sxs-lookup"><span data-stu-id="851a1-268">Planned start date</span></span> |
| <span data-ttu-id="851a1-269">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="851a1-269">PlannedEndDate_t</span></span>  |   <span data-ttu-id="851a1-270">Geplande einddatum</span><span class="sxs-lookup"><span data-stu-id="851a1-270">Planned end date</span></span> |
| <span data-ttu-id="851a1-271">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="851a1-271">WorkStartDate_t</span></span>  | <span data-ttu-id="851a1-272">Werkelijke begindatum</span><span class="sxs-lookup"><span data-stu-id="851a1-272">Actual start date</span></span> |
| <span data-ttu-id="851a1-273">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="851a1-273">WorkEndDate_t</span></span> | <span data-ttu-id="851a1-274">Werkelijke einddatum</span><span class="sxs-lookup"><span data-stu-id="851a1-274">Actual end date</span></span>|
| <span data-ttu-id="851a1-275">Description_s</span><span class="sxs-lookup"><span data-stu-id="851a1-275">Description_s</span></span> | <span data-ttu-id="851a1-276">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="851a1-276">Description</span></span> |
| <span data-ttu-id="851a1-277">Computer</span><span class="sxs-lookup"><span data-stu-id="851a1-277">Computer</span></span>  | <span data-ttu-id="851a1-278">Configuratie-Item</span><span class="sxs-lookup"><span data-stu-id="851a1-278">Configuration Item</span></span> |

<span data-ttu-id="851a1-279">**Voorbeeld logboekanalyse scherm voor ITSM gegevens:**</span><span class="sxs-lookup"><span data-stu-id="851a1-279">**Sample Log Analytics screen for ITSM data:**</span></span>

![Log Analytics scherm](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a><span data-ttu-id="851a1-281">IT-Service Management-connector: integratie met andere OMS-oplossingen</span><span class="sxs-lookup"><span data-stu-id="851a1-281">IT Service Management connector – integration with other OMS solutions</span></span>

<span data-ttu-id="851a1-282">IT-Service Management-Connector ondersteunt momenteel integratie met Hallo Serviceoverzicht oplossing.</span><span class="sxs-lookup"><span data-stu-id="851a1-282">IT Service Management Connector, currently supports integration with hello Service Map solution.</span></span>

<span data-ttu-id="851a1-283">Serviceoverzicht detecteert automatisch Hallo toepassingsonderdelen in Windows en Linux-systemen en maps Hallo communicatie tussen services.</span><span class="sxs-lookup"><span data-stu-id="851a1-283">Service Map automatically discovers hello application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="851a1-284">Hiermee kunt u uw servers als u denkt dat ze – als onderling verbonden systemen die essentiële services leveren tooview.</span><span class="sxs-lookup"><span data-stu-id="851a1-284">It allows you tooview your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="851a1-285">Serviceoverzicht ziet u de verbindingen tussen servers, processen, en poorten voor elke architectuur TCP-verbinding waarvoor geen configuratie nodig andere dan de installatie van een agent.</span><span class="sxs-lookup"><span data-stu-id="851a1-285">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="851a1-286">Meer informatie: [Serviceoverzicht](../operations-management-suite/operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="851a1-286">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="851a1-287">U kunt met deze integratie Hallo service helpdesk items die zijn gemaakt in Hallo ITSM oplossingen zoals weergegeven in het volgende voorbeeld Hallo bekijken:</span><span class="sxs-lookup"><span data-stu-id="851a1-287">With this integration, you can view hello service desk items created in hello ITSM solutions as shown in hello following example:</span></span>

![<span data-ttu-id="851a1-288">Geïntegreerde oplossing</span><span class="sxs-lookup"><span data-stu-id="851a1-288">Integrated solution</span></span> ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a><span data-ttu-id="851a1-289">Werkitems ITSM voor OMS waarschuwingen maken</span><span class="sxs-lookup"><span data-stu-id="851a1-289">Create ITSM work items for OMS alerts</span></span>

<span data-ttu-id="851a1-290">Voor Hallo OMS waarschuwingen, kunt u gekoppelde werkitems in Hallo verbonden ITSM bronnen.</span><span class="sxs-lookup"><span data-stu-id="851a1-290">For hello OMS alerts, you can create associated work items in hello connected ITSM sources.</span></span>  <span data-ttu-id="851a1-291">toodo deze, gebruik Hallo procedure te volgen:</span><span class="sxs-lookup"><span data-stu-id="851a1-291">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="851a1-292">Van **logboek zoeken** venster een logboekgegevens zoeken query tooview uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="851a1-292">From **Log Search** window, run a log search query tooview data.</span></span> <span data-ttu-id="851a1-293">Queryresultaten zijn Hallo bron voor werkitems.</span><span class="sxs-lookup"><span data-stu-id="851a1-293">Query results are hello source for work items.</span></span>
2. <span data-ttu-id="851a1-294">In **logboek zoeken**, klikt u op **waarschuwing** tooopen hello **waarschuwingsregel toevoegen** pagina.</span><span class="sxs-lookup"><span data-stu-id="851a1-294">In **Log Search**, click **Alert** tooopen hello **Add Alert Rule** page.</span></span>

    ![Log Analytics scherm](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. <span data-ttu-id="851a1-296">Op Hallo **waarschuwingsregel toevoegen** venster Geef details op Hallo vereist voor **naam**, **ernst**, **zoekquery**, en  **Waarschuwing criteria** (Tijdsmeting venster meting).</span><span class="sxs-lookup"><span data-stu-id="851a1-296">On hello **Add Alert Rule** window, provide hello required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="851a1-297">Selecteer **Ja** voor **ITSM acties**.</span><span class="sxs-lookup"><span data-stu-id="851a1-297">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="851a1-298">Selecteer uw verbinding ITSM in Hallo **verbinding selecteren** lijst.</span><span class="sxs-lookup"><span data-stu-id="851a1-298">Select your ITSM connection from hello **Select Connection** list.</span></span>
6. <span data-ttu-id="851a1-299">Geef details op Hallo zoals vereist.</span><span class="sxs-lookup"><span data-stu-id="851a1-299">Provide hello details as required.</span></span>
7. <span data-ttu-id="851a1-300">een afzonderlijke werkitem van elke logboekvermelding van deze waarschuwing, selecteer Hallo toocreate **maken van afzonderlijke werkitems van elke logboekvermelding** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="851a1-300">toocreate a separate work item for each log entry of this alert, select hello **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="851a1-301">of</span><span class="sxs-lookup"><span data-stu-id="851a1-301">Or</span></span>

    <span data-ttu-id="851a1-302">Laat dit selectievakje niet geselecteerd toocreate slechts één werkitem voor een willekeurig aantal vermeldingen in het logboek in deze waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="851a1-302">leave this checkbox unselected toocreate only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="851a1-303">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="851a1-303">Click **Save**.</span></span>

<span data-ttu-id="851a1-304">Hallo OMS waarschuwing worden gemaakt onder **waarschuwingen**.</span><span class="sxs-lookup"><span data-stu-id="851a1-304">hello OMS alert will be created under **Alerts**.</span></span> <span data-ttu-id="851a1-305">Hallo bijbehorende ITSM-verbinding work items worden gemaakt wanneer Hallo opgegeven waarschuwing voorwaarde wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="851a1-305">hello corresponding ITSM connection's work items are created when hello specified alert's condition is met.</span></span>

## <a name="create-itsm-work-items-from-oms-logs"></a><span data-ttu-id="851a1-306">Maken van werkitems ITSM van OMS-Logboeken</span><span class="sxs-lookup"><span data-stu-id="851a1-306">Create ITSM work items from OMS logs</span></span>

<span data-ttu-id="851a1-307">U kunt werkitems in Hallo verbonden ITSM bronnen maken met behulp van OMS logboek zoeken.</span><span class="sxs-lookup"><span data-stu-id="851a1-307">You can create work items in hello connected ITSM sources by using OMS Log Search.</span></span> <span data-ttu-id="851a1-308">toodo deze, gebruik Hallo procedure te volgen:</span><span class="sxs-lookup"><span data-stu-id="851a1-308">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="851a1-309">Van **logboek zoeken**, Hallo vereist gegevens zoeken, Hallo detail selecteren en klik op **maken werkitem**.</span><span class="sxs-lookup"><span data-stu-id="851a1-309">From **Log Search**,  search hello required data, select hello detail, and click **Create work item**.</span></span>

    <span data-ttu-id="851a1-310">Hallo **maken ITSM werkitem** venster wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="851a1-310">hello **Create ITSM Work item** window appears:</span></span>

    ![Log Analytics scherm](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   <span data-ttu-id="851a1-312">Voeg Hallo volgende details:</span><span class="sxs-lookup"><span data-stu-id="851a1-312">Add hello following details:</span></span>

  - <span data-ttu-id="851a1-313">**Titel werkitem**: titel voor Hallo werkitem.</span><span class="sxs-lookup"><span data-stu-id="851a1-313">**Work item Title**: Title for hello work item.</span></span>
  - <span data-ttu-id="851a1-314">**Beschrijving van werkitem**: beschrijving voor het nieuwe werkitem Hallo.</span><span class="sxs-lookup"><span data-stu-id="851a1-314">**Work item Description**: Description for hello new work item.</span></span>
  - <span data-ttu-id="851a1-315">**Van invloed op een Computer**: naam van Hallo computer waar deze logboekgegevens is gevonden.</span><span class="sxs-lookup"><span data-stu-id="851a1-315">**Affected Computer**: Name of hello computer where this log data was found.</span></span>
  - <span data-ttu-id="851a1-316">**Selecteer verbinding**: ITSM verbinding die u toocreate dit werkitem wilt.</span><span class="sxs-lookup"><span data-stu-id="851a1-316">**Select Connection**:  ITSM connection in which you want toocreate this work item.</span></span>
  - <span data-ttu-id="851a1-317">**Werkitem**: Type werkitem.</span><span class="sxs-lookup"><span data-stu-id="851a1-317">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="851a1-318">toouse een bestaande werkitemsjabloon voor een incident voordoet, klikt u op **Ja** onder **werkitem genereren op basis van sjabloon Hallo** optie en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="851a1-318">toouse an existing work item template for an incident, click **Yes** under **Generate work item based on hello template** option and then click **Create**.</span></span>

    <span data-ttu-id="851a1-319">Of</span><span class="sxs-lookup"><span data-stu-id="851a1-319">Or,</span></span>

    <span data-ttu-id="851a1-320">Klik op **Nee** als u tooprovide uw aangepaste waarden wilt.</span><span class="sxs-lookup"><span data-stu-id="851a1-320">Click **No** if you want tooprovide your customized values.</span></span>

4. <span data-ttu-id="851a1-321">Geef de juiste waarden in Hallo Hallo **Type Contact**, **Impact**, **urgentie**, **categorie**, en **subcategorie**  tekstvakken en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="851a1-321">Provide hello appropriate values in hello **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>

<span data-ttu-id="851a1-322">Hallo werkitem wordt gemaakt in Hallo ITSM die u ook in OMS bekijken kunt.</span><span class="sxs-lookup"><span data-stu-id="851a1-322">hello work item will be created in hello ITSM, which you can also view in OMS.</span></span>

## <a name="troubleshoot-itsm-connections-in-oms"></a><span data-ttu-id="851a1-323">ITSM verbindingen in OMS oplossen</span><span class="sxs-lookup"><span data-stu-id="851a1-323">Troubleshoot ITSM connections in OMS</span></span>
1.  <span data-ttu-id="851a1-324">Als de verbinding is mislukt door de gebruikersinterface van de verbonden bron en u beschikt over Hallo **fout bij het opslaan van de verbinding** bericht wordt weergegeven, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="851a1-324">If connection fails from connected source's UI and you get hello **Error in saving connection** message, do hello following:</span></span>
 - <span data-ttu-id="851a1-325">In geval van een ServiceNow, Cherwell en Provance verbindingen, zorg ervoor dat u correct worden ingevoerd Hallo gebruikersnaam en wachtwoord en de client-ID/clientgeheim voor elk Hallo-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="851a1-325">In case of ServiceNow, Cherwell and Provance connections, ensure you correctly entered  hello username/password and  client ID/client secret  for each of hello connections.</span></span> <span data-ttu-id="851a1-326">Als Hallo fout zich blijft voordoen, controleert u of u voldoende rechten in Hallo bijbehorende ITSM product toomake Hallo verbinding hebt.</span><span class="sxs-lookup"><span data-stu-id="851a1-326">If hello error persists, check if you have sufficient privileges  in hello corresponding ITSM product toomake hello connection.</span></span>
 - <span data-ttu-id="851a1-327">In geval van een Service Manager, zorg ervoor dat Hallo Web-app is geïmplementeerd en hybride verbinding is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="851a1-327">In case of Service Manager, ensure that hello Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="851a1-328">tooverify hello verbinding is tot stand gebracht met Hallo on-premises Service Manager-computer, gaat u naar Hallo Web-app-URL zoals beschreven in de documentatie voor het maken van Hallo Hallo [hybride verbinding](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="851a1-328">tooverify hello connection is successfully established with hello on-prem Service Manager machine, visit hello  Web app URL as detailed in hello documentation for making hello [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>

2.  <span data-ttu-id="851a1-329">Als u gegevens van ServiceNow is niet ophalen van gesynchroniseerd in OMS, zorg ervoor dat Hallo ServiceNow-exemplaar niet in de slaapstand staat.</span><span class="sxs-lookup"><span data-stu-id="851a1-329">If data from ServiceNow is not getting synced in OMS, ensure that hello ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="851a1-330">Dit kan enige tijd gebeuren in Hallo ServiceNow Dev-exemplaren, als inactief.</span><span class="sxs-lookup"><span data-stu-id="851a1-330">This might sometime happen in hello ServiceNow Dev instances, when idle.</span></span> <span data-ttu-id="851a1-331">Anders, rapport Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="851a1-331">Else, report hello issue.</span></span>
3.  <span data-ttu-id="851a1-332">Als waarschuwingen van OMS ophalen gestart, maar niet ophalen van werkitems in ITSM product of configuratie-items niet van toowork gemaakt/gekoppelde items ophalen zijn of voor een algemene informatie, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="851a1-332">If Alerts are getting fired from OMS but work items are not getting created in ITSM product or configuration items are not getting created/linked toowork items or for any generic information, do hello following:</span></span>
 -  <span data-ttu-id="851a1-333">Oplossing voor IT-Service Management-Connector in OMS-portal kan worden gebruikt tooget een overzicht van verbindingen werk items computers enzovoort. Klik op het foutbericht Hallo Hallo status blade, te navigeren**logboek zoeken** en Hallo-verbinding met de Hallo fout met behulp van Hallo details in het foutbericht Hallo weergeven.</span><span class="sxs-lookup"><span data-stu-id="851a1-333">IT Service Management Connector solution in OMS portal could be used tooget a summary of connections/work items/computers etc. Click hello error message in hello status blade, navigate too**Log Search** and view hello connection that has hello error by using hello details in hello error message.</span></span>
 - <span data-ttu-id="851a1-334">u kunt rechtstreeks Hallo fouten/gerelateerde informatie weergeven in Hallo **logboek zoeken** met behulp van pagina *Type = ServiceDeskLog_CL*.</span><span class="sxs-lookup"><span data-stu-id="851a1-334">you can directly view hello errors/related information in hello **Log Search** page using *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="851a1-335">Problemen met de Web-App Service Manager-implementatie oplossen</span><span class="sxs-lookup"><span data-stu-id="851a1-335">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="851a1-336">In geval van problemen met web-app-implementatie, zorg ervoor dat u voldoende rechten hebt in Hallo abonnement toocreate/implementeren bronnen vermeld.</span><span class="sxs-lookup"><span data-stu-id="851a1-336">In case of any trouble with web app deployment, ensure you have sufficient permissions in hello subscription mentioned toocreate/deploy resources.</span></span>
2.  <span data-ttu-id="851a1-337">Als **objectverwijzing niet ingesteld tooinstance van een object** foutbericht wordt weergegeven tijdens het uitvoeren van Hallo [script](log-analytics-itsmc-service-manager-script.md) voor zorgen dat u geldige waarden onder ingevoerd **Gebruikersconfiguratie**sectie.</span><span class="sxs-lookup"><span data-stu-id="851a1-337">If **Object reference not set tooinstance of an object** error message appears while running hello [script](log-analytics-itsmc-service-manager-script.md) ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="851a1-338">Als u niet toocreate service bus relay-naamruimte, Verzeker u ervan dat Hallo vereiste resourceprovider is geregistreerd in het Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="851a1-338">If you fail toocreate service bus relay namespace, ensure that hello required resource provider is registered in hello subscription.</span></span> <span data-ttu-id="851a1-339">Als dat niet is geregistreerd, maakt u dit handmatig uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="851a1-339">If not registered, manually create it from hello Azure portal.</span></span> <span data-ttu-id="851a1-340">U kunt ook maken terwijl [Hallo hybride verbinding maken](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="851a1-340">You can also create it while [creating hello hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from hello Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="851a1-341">Contact opnemen</span><span class="sxs-lookup"><span data-stu-id="851a1-341">Contact us</span></span>

<span data-ttu-id="851a1-342">Voor query's of feedback op Hallo IT Service Management-Connector, contact met ons op [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="851a1-342">For any queries or feedback on hello IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="851a1-343">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="851a1-343">Next steps</span></span>
<span data-ttu-id="851a1-344">[ITSM producten/services tooIT Service Management-Connector toevoegen](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="851a1-344">[Add ITSM products/services tooIT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
