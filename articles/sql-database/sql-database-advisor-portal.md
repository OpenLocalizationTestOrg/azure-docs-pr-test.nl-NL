---
title: Toepassen van aanbevelingen voor prestaties - Azure SQL Database | Microsoft Docs
description: "Kunt u de Azure-portal prestaties aanbevelingen die u kunnen de prestaties van uw Azure SQL Database optimaliseren zoeken of om bepaalde geïdentificeerd in de werkbelasting van uw probleem te verhelpen."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 018afaa8b08bd001e55693390e80c8e2c4f33a30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="find-and-apply-performance-recommendations"></a><span data-ttu-id="5d8b4-103">Zoeken en toepassen van aanbevelingen voor prestaties</span><span class="sxs-lookup"><span data-stu-id="5d8b4-103">Find and apply performance recommendations</span></span>

<span data-ttu-id="5d8b4-104">Kunt u de Azure-portal prestaties aanbevelingen die u kunnen de prestaties van uw Azure SQL Database optimaliseren zoeken of om bepaalde geïdentificeerd in de werkbelasting van uw probleem te verhelpen.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-104">You can use the Azure portal to find performance recommendations that can optimize performance of your Azure SQL Database or to correct some issue identified in your workload.</span></span> <span data-ttu-id="5d8b4-105">**Prestaties aanbeveling** pagina in de Azure-portal kunt u de aanbevelingen op basis van de potentiële impact vinden.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-105">**Performance recommendation** page in Azure portal enables you to find the top recommendations based on their potential impact.</span></span> 

## <a name="viewing-recommendations"></a><span data-ttu-id="5d8b4-106">Aanbevelingen weergeven</span><span class="sxs-lookup"><span data-stu-id="5d8b4-106">Viewing recommendations</span></span>

<span data-ttu-id="5d8b4-107">Als u wilt bekijken en toepassen van aanbevelingen voor prestaties, moet u de juiste [toegangsbeheer op basis van rollen](../active-directory/role-based-access-control-what-is.md) machtigingen in Azure.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-107">To view and apply performance recommendations, you need the correct [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions in Azure.</span></span> <span data-ttu-id="5d8b4-108">**Lezer**, **SQL DB Contributor** machtigingen zijn vereist voor het weergeven van aanbevelingen en **eigenaar**, **SQL DB Contributor** machtigingen zijn vereist voor uitvoeren van acties; Maak of verwijder indexen en maken van een index te annuleren.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-108">**Reader**, **SQL DB Contributor** permissions are required to view recommendations, and **Owner**, **SQL DB Contributor** permissions are required to execute any actions; create or drop indexes and cancel index creation.</span></span>

<span data-ttu-id="5d8b4-109">Gebruik de volgende stappen uit om te zoeken prestaties aanbevelingen in Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="5d8b4-109">Use the following steps to find performance recommendations on Azure portal:</span></span>

1. <span data-ttu-id="5d8b4-110">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5d8b4-110">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5d8b4-111">Ga naar **meer services** > **SQL-databases**, en selecteer uw database.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-111">Go to **More services** > **SQL databases**, and select your database.</span></span>
3. <span data-ttu-id="5d8b4-112">Navigeer naar **prestaties aanbeveling** om beschikbare aanbevelingen voor de geselecteerde database weer te geven.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-112">Navigate to **Performance recommendation** to view available recommendations for the selected database.</span></span>

<span data-ttu-id="5d8b4-113">Prestaties aanbevelingen zijn shonw in de tabel die vergelijkbaar is met wordt weergegeven op de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="5d8b4-113">Performance recommendations are shonw in the table similar to the one shown on the following figure:</span></span>

![Aanbevelingen](./media/sql-database-advisor-portal/recommendations.png)

<span data-ttu-id="5d8b4-115">Aanbevelingen worden gesorteerd op de potentiële impact op de prestaties in de volgende categorieën:</span><span class="sxs-lookup"><span data-stu-id="5d8b4-115">Recommendations are sorted by their potential impact on performance into the following categories:</span></span>

| <span data-ttu-id="5d8b4-116">Impact</span><span class="sxs-lookup"><span data-stu-id="5d8b4-116">Impact</span></span> | <span data-ttu-id="5d8b4-117">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5d8b4-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5d8b4-118">Hoog</span><span class="sxs-lookup"><span data-stu-id="5d8b4-118">High</span></span> |<span data-ttu-id="5d8b4-119">Aanbevelingen voor grote invloed moeten een van de belangrijkste prestatie-invloed.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-119">High impact recommendations should provide the most significant performance impact.</span></span> |
| <span data-ttu-id="5d8b4-120">Middelgroot</span><span class="sxs-lookup"><span data-stu-id="5d8b4-120">Medium</span></span> |<span data-ttu-id="5d8b4-121">Gemiddeld impact aanbevelingen moeten de prestaties verbeteren, maar niet aanzienlijk.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-121">Medium impact recommendations should improve performance, but not substantially.</span></span> |
| <span data-ttu-id="5d8b4-122">Laag</span><span class="sxs-lookup"><span data-stu-id="5d8b4-122">Low</span></span> |<span data-ttu-id="5d8b4-123">Lage impact aanbevelingen moeten zorgen voor betere prestaties dan zonder, maar mogelijk aanzienlijke verbeteringen niet.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-123">Low impact recommendations should provide better performance than without, but improvements might not be significant.</span></span> |


> [!NOTE]
> <span data-ttu-id="5d8b4-124">Azure SQL-Database moet activiteiten volgen die ten minste een dag om te kunnen identificeren van enkele aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-124">Azure SQL Database needs to monitor activities at least for a day in order to identify some recommendations.</span></span> <span data-ttu-id="5d8b4-125">De Azure SQL Database kunt gemakkelijker optimaliseren voor consistente querypatronen dan dit kunt doen voor willekeurige slechte bursts van activiteit.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-125">The Azure SQL Database can more easily optimize for consistent query patterns than it can for random spotty bursts of activity.</span></span> <span data-ttu-id="5d8b4-126">Als de aanbevelingen zijn niet beschikbaar is, corrently de **prestaties aanbeveling** pagina vindt u een bericht waarin wordt uitgelegd waarom.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-126">If recommendations are not corrently available, the **Performance recommendation** page provides a message explaining why.</span></span>
> 

<span data-ttu-id="5d8b4-127">U kunt ook de status van de historische bewerkingen weergeven.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-127">You can also view the status of the historical operations.</span></span> <span data-ttu-id="5d8b4-128">Selecteer een aanbeveling of de status voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-128">Select a recommendation or status to see  more details.</span></span>

<span data-ttu-id="5d8b4-129">Hier volgt een voorbeeld van een aanbeveling 'Index maken' in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-129">Here is an example of "Create index" recommendation in the Azure portal.</span></span>

![Index maken](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a><span data-ttu-id="5d8b4-131">Toepassen van aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="5d8b4-131">Applying recommendations</span></span>
<span data-ttu-id="5d8b4-132">Azure SQL Database hebt u volledige controle over hoe aanbevelingen worden ingeschakeld met een van de volgende drie opties:</span><span class="sxs-lookup"><span data-stu-id="5d8b4-132">Azure SQL Database gives you full control over how recommendations are enabled using any of the following three options:</span></span> 

* <span data-ttu-id="5d8b4-133">Afzonderlijke aanbevelingen één toepassing tegelijk.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-133">Apply individual recommendations one at a time.</span></span>
* <span data-ttu-id="5d8b4-134">Schakel de automatische afstemming voor automatisch toepassen van aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-134">Enable the Automatic tuning to automatically apply recommendations.</span></span>
* <span data-ttu-id="5d8b4-135">Een aanbeveling als handmatig wilt implementeren, de aanbevolen T-SQL-script worden uitgevoerd op basis van uw database.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-135">To implement a recommendation manually, run the recommended T-SQL script against your database.</span></span>

<span data-ttu-id="5d8b4-136">Selecteer elke aanbeveling om de details weergeven en klik vervolgens op **script weergeven** om te controleren van de exacte details van hoe de aanbeveling wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-136">Select any recommendation to view its details and then click **View script** to review the exact details of how the recommendation is created.</span></span>

<span data-ttu-id="5d8b4-137">De database blijft online terwijl de aanbeveling wordt toegepast--met prestaties aanbeveling of automatische afstemming een database nooit offline neemt.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-137">The database remains online while the recommendation is applied -- using performance recommendation or automatic tuning never takes a database offline.</span></span>

### <a name="apply-an-individual-recommendation"></a><span data-ttu-id="5d8b4-138">Een afzonderlijke aanbeveling toepassen</span><span class="sxs-lookup"><span data-stu-id="5d8b4-138">Apply an individual recommendation</span></span>
<span data-ttu-id="5d8b4-139">U kunt bekijken en aanbevelingen een tegelijk accepteren.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-139">You can review and accept recommendations one at a time.</span></span>

1. <span data-ttu-id="5d8b4-140">Op de **aanbevelingen** blade, selecteert u een aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-140">On the **Recommendations** blade, select a recommendation.</span></span>
2. <span data-ttu-id="5d8b4-141">Op de **Details** Klik op de blade **toepassen** knop.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-141">On the **Details** blade click **Apply** button.</span></span>
   
    ![Aanbeveling toepassen](./media/sql-database-advisor-portal/apply.png)

<span data-ttu-id="5d8b4-143">Geselecteerde aanbeveling wordt toegepast op de database.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-143">Selected recommendation will be applied on the database.</span></span>

### <a name="removing-recommendations-from-the-list"></a><span data-ttu-id="5d8b4-144">Aanbevelingen verwijderen uit de lijst</span><span class="sxs-lookup"><span data-stu-id="5d8b4-144">Removing recommendations from the list</span></span>
<span data-ttu-id="5d8b4-145">Als uw lijst met aanbevelingen items die u wilt verwijderen uit de lijst bevat, kunt u de aanbeveling negeren:</span><span class="sxs-lookup"><span data-stu-id="5d8b4-145">If your list of recommendations contains items that you want to remove from the list, you can discard the recommendation:</span></span>

1. <span data-ttu-id="5d8b4-146">Selecteer een aanbeveling in de lijst met **aanbevelingen** de details te openen.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-146">Select a recommendation in the list of **Recommendations** to open the details.</span></span>
2. <span data-ttu-id="5d8b4-147">Klik op **negeren** op de **Details** blade.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-147">Click **Discard** on the **Details** blade.</span></span>

<span data-ttu-id="5d8b4-148">Indien gewenst, kunt u toevoegen verwijderde items terug naar de **aanbevelingen** lijst:</span><span class="sxs-lookup"><span data-stu-id="5d8b4-148">If desired, you can add discarded items back to the **Recommendations** list:</span></span>

1. <span data-ttu-id="5d8b4-149">Op de **aanbevelingen** Klik op de blade **weergave verwijderd**.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-149">On the **Recommendations** blade click **View discarded**.</span></span>
2. <span data-ttu-id="5d8b4-150">Selecteer een verwijderde item uit de lijst om de details ervan weer te geven.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-150">Select a discarded item from the list to view its details.</span></span>
3. <span data-ttu-id="5d8b4-151">Klik desgewenst op **ongedaan negeren** om toe te voegen van de index terug naar de belangrijkste lijst van **aanbevelingen**.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-151">Optionally, click **Undo Discard** to add the index back to the main list of **Recommendations**.</span></span>


### <a name="enable-automatic-tuning"></a><span data-ttu-id="5d8b4-152">Automatisch instellen inschakelen</span><span class="sxs-lookup"><span data-stu-id="5d8b4-152">Enable automatic tuning</span></span>
<span data-ttu-id="5d8b4-153">U kunt de Azure SQL Database voor het implementeren van aanbevelingen automatisch instellen.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-153">You can set the Azure SQL Database to implement recommendations automatically.</span></span> <span data-ttu-id="5d8b4-154">Aanbevelingen beschikbaar komen ze automatisch worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-154">As recommendations become available they will automatically be applied.</span></span> <span data-ttu-id="5d8b4-155">Als met alle aanbevelingen die worden beheerd door de service als het prestatieresultaat negatief is worden de aanbeveling, teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-155">As with all recommendations managed by the service if the performance impact is negative the recommendation will be reverted.</span></span>

1. <span data-ttu-id="5d8b4-156">Op de **aanbevelingen** blade, klikt u op **automatiseren**:</span><span class="sxs-lookup"><span data-stu-id="5d8b4-156">On the **Recommendations** blade, click **Automate**:</span></span>
   
    ![Advisor-instellingen](./media/sql-database-advisor-portal/settings.png)
2. <span data-ttu-id="5d8b4-158">Selecteer de acties die voor het automatiseren van:</span><span class="sxs-lookup"><span data-stu-id="5d8b4-158">Select actions to automate:</span></span>
   
    ![Aanbevolen indexen](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-the-recommended-t-sql-script"></a><span data-ttu-id="5d8b4-160">Voer handmatig het aanbevolen T-SQL-script</span><span class="sxs-lookup"><span data-stu-id="5d8b4-160">Manually run the recommended T-SQL script</span></span>
<span data-ttu-id="5d8b4-161">Selecteer elke aanbeveling en klik op **script weergeven**.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-161">Select any recommendation and then click **View script**.</span></span> <span data-ttu-id="5d8b4-162">Dit script wordt uitgevoerd in de database naar de aanbeveling handmatig toe te passen.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-162">Run this script against your database to manually apply the recommendation.</span></span>

<span data-ttu-id="5d8b4-163">*Indexen die handmatig worden uitgevoerd wordt niet gecontroleerd en gevalideerd voor invloed op de prestaties door de service* zodat het wordt aangeraden deze indexen te bewaken na herstart maken om te controleren of ze bieden betere prestaties en aanpassen of verwijder ze indien nodig.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-163">*Indexes that are manually executed are not monitored and validated for performance impact by the service* so it is suggested that you monitor these indexes after creation to verify they provide performance gains and adjust or delete them if necessary.</span></span> <span data-ttu-id="5d8b4-164">Zie voor meer informatie over het maken van indexen [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span><span class="sxs-lookup"><span data-stu-id="5d8b4-164">For details about creating indexes, see [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span></span>

### <a name="canceling-recommendations"></a><span data-ttu-id="5d8b4-165">Aanbevelingen annuleren</span><span class="sxs-lookup"><span data-stu-id="5d8b4-165">Canceling recommendations</span></span>
<span data-ttu-id="5d8b4-166">Aanbevelingen die zich in een **in behandeling**, **controleren**, of **geslaagd** status kan worden geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-166">Recommendations that are in a **Pending**, **Verifying**, or **Success** status can be canceled.</span></span> <span data-ttu-id="5d8b4-167">Aanbevelingen met de status van **Executing** kan niet worden geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-167">Recommendations with a status of **Executing** cannot be canceled.</span></span>

1. <span data-ttu-id="5d8b4-168">Selecteer een aanbeveling in de **afstemmen geschiedenis** gebied openen de **aanbevelingen details** blade.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-168">Select a recommendation in the **Tuning History** area to open the **recommendations details** blade.</span></span>
2. <span data-ttu-id="5d8b4-169">Klik op **annuleren** om af te breken van het proces van het toepassen van de aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-169">Click **Cancel** to abort the process of applying the recommendation.</span></span>

## <a name="monitoring-operations"></a><span data-ttu-id="5d8b4-170">Bewakingsbewerkingen</span><span class="sxs-lookup"><span data-stu-id="5d8b4-170">Monitoring operations</span></span>
<span data-ttu-id="5d8b4-171">Toepassen van een aanbeveling kan niet direct gebeuren.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-171">Applying a recommendation might not happen instantaneously.</span></span> <span data-ttu-id="5d8b4-172">De portal biedt informatie over de status van een aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-172">The portal provides details regarding the status of recommendation.</span></span> <span data-ttu-id="5d8b4-173">Hier volgen de mogelijke statussen van een index worden weergegeven in:</span><span class="sxs-lookup"><span data-stu-id="5d8b4-173">The following are possible states that an index can be in:</span></span>

| <span data-ttu-id="5d8b4-174">Status</span><span class="sxs-lookup"><span data-stu-id="5d8b4-174">Status</span></span> | <span data-ttu-id="5d8b4-175">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5d8b4-175">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5d8b4-176">In behandeling</span><span class="sxs-lookup"><span data-stu-id="5d8b4-176">Pending</span></span> |<span data-ttu-id="5d8b4-177">Aanbeveling opdracht is ontvangen en is gepland voor uitvoering toepassen.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-177">Apply recommendation command has been received and is scheduled for execution.</span></span> |
| <span data-ttu-id="5d8b4-178">Uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5d8b4-178">Executing</span></span> |<span data-ttu-id="5d8b4-179">De aanbeveling wordt toegepast.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-179">The recommendation is being applied.</span></span> |
| <span data-ttu-id="5d8b4-180">Controleren</span><span class="sxs-lookup"><span data-stu-id="5d8b4-180">Verifying</span></span> |<span data-ttu-id="5d8b4-181">Aanbeveling is toegepast en de service is de voordelen te meten.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-181">Recommendation was successfully applied and the service is measuring the benefits.</span></span> |
| <span data-ttu-id="5d8b4-182">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="5d8b4-182">Success</span></span> |<span data-ttu-id="5d8b4-183">Aanbeveling is toegepast en voordelen zijn gemeten.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-183">Recommendation was successfully applied and benefits have been measured.</span></span> |
| <span data-ttu-id="5d8b4-184">Fout</span><span class="sxs-lookup"><span data-stu-id="5d8b4-184">Error</span></span> |<span data-ttu-id="5d8b4-185">Er is een fout opgetreden tijdens het toepassen van de aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-185">An error occurred during the process of applying the recommendation.</span></span> <span data-ttu-id="5d8b4-186">Dit is een tijdelijk probleem of mogelijk een schema wijzigen in de tabel en het script is niet meer geldig.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-186">This can be a transient issue, or possibly a schema change to the table and the script is no longer valid.</span></span> |
| <span data-ttu-id="5d8b4-187">Herstellen van instellingen</span><span class="sxs-lookup"><span data-stu-id="5d8b4-187">Reverting</span></span> |<span data-ttu-id="5d8b4-188">De aanbeveling is toegepast, maar heeft vastgesteld dat is niet zodat en automatisch wordt omgezet.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-188">The recommendation was applied, but has been deemed non-performant and is being automatically reverted.</span></span> |
| <span data-ttu-id="5d8b4-189">Teruggedraaid</span><span class="sxs-lookup"><span data-stu-id="5d8b4-189">Reverted</span></span> |<span data-ttu-id="5d8b4-190">De aanbeveling is hersteld.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-190">The recommendation was reverted.</span></span> |

<span data-ttu-id="5d8b4-191">Klik op een aanbeveling in proces uit de lijst voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="5d8b4-191">Click an in-process recommendation from the list to see more details:</span></span>

![Aanbevolen indexen](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a><span data-ttu-id="5d8b4-193">Herstellen van een aanbeveling</span><span class="sxs-lookup"><span data-stu-id="5d8b4-193">Reverting a recommendation</span></span>
<span data-ttu-id="5d8b4-194">Als u de prestaties van aanbevelingen om toe te passen de aanbeveling gebruikt wordt (wat betekent dat u de T-SQL-script handmatig niet hebt uitgevoerd) automatisch overgeschakeld deze als het wordt het prestatieresultaat negatief gevonden.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-194">If you used the performance recommendations to apply the recommendation (meaning you did not manually run the T-SQL script) it will automatically revert it if it finds the performance impact to be negative.</span></span> <span data-ttu-id="5d8b4-195">Als voor een bepaalde reden u gewoon wilt terugkeren naar een aanbeveling kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="5d8b4-195">If for any reason you simply want to revert a recommendation you can do the following:</span></span>

1. <span data-ttu-id="5d8b4-196">Selecteer een toegepaste aanbeveling in de **afstemmen geschiedenis** gebied.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-196">Select a successfully applied recommendation in the **Tuning history** area.</span></span>
2. <span data-ttu-id="5d8b4-197">Klik op **Revert** op de **gegevens over de aanbeveling** blade.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-197">Click **Revert** on the **recommendation details** blade.</span></span>

![Aanbevolen indexen](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a><span data-ttu-id="5d8b4-199">Bewaking van prestatie-invloed van de indexaanbevelingen</span><span class="sxs-lookup"><span data-stu-id="5d8b4-199">Monitoring performance impact of index recommendations</span></span>
<span data-ttu-id="5d8b4-200">Nadat de aanbevelingen zijn geïmplementeerd (momenteel index-bewerkingen en aanbevelingen voor query's alleen voorzien) kunt u **Query Insights** op de blade aanbeveling details openen [Query Inzichten](sql-database-query-performance.md) en de impact van de prestaties van uw meest gebruikte query's.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-200">After recommendations are successfully implemented (currently, index operations and parameterize queries recommendations only) you can click **Query Insights** on the recommendation details blade to open [Query Performance Insights](sql-database-query-performance.md) and see the performance impact of your top queries.</span></span>

![Prestatie-invloed van monitor](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a><span data-ttu-id="5d8b4-202">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="5d8b4-202">Summary</span></span>
<span data-ttu-id="5d8b4-203">Azure SQL-Database bevat aanbevelingen voor het verbeteren van de prestaties van de SQL-database.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-203">Azure SQL Database provides recommendations for improving SQL database performance.</span></span> <span data-ttu-id="5d8b4-204">Dankzij de T-SQL-scripts, evenals afzonderlijke en volledig-automatische, krijgt u een handig hulp bij het optimaliseren van uw database en uiteindelijk queryprestaties te verbeteren.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-204">By providing T-SQL scripts, as well as individual and fully-automatic, you get a helpful assistance in optimizing your database and ultimately improving query performance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d8b4-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5d8b4-205">Next steps</span></span>
<span data-ttu-id="5d8b4-206">Bewaken van uw aanbevelingen en blijven toepassen om de prestaties te verfijnen.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-206">Monitor your recommendations and continue to apply them to refine performance.</span></span> <span data-ttu-id="5d8b4-207">Database-werkbelastingen zijn dynamisch en continu wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-207">Database workloads are dynamic and change continuously.</span></span> <span data-ttu-id="5d8b4-208">Azure SQL Database blijven bewaken en doet aanbevelingen die potentieel prestaties van uw database kunnen verbeteren.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-208">Azure SQL Database will continue to monitor and provide recommendations that can potentially improve your database's performance.</span></span> 

* <span data-ttu-id="5d8b4-209">Zie [automatische afstemming](sql-database-automatic-tuning.md) voor meer informatie over automatische afstemming in Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-209">See [Automatic tuning](sql-database-automatic-tuning.md) to learn more about the automatic tuning in Azure SQL Database.</span></span>
* <span data-ttu-id="5d8b4-210">Zie [prestaties aanbevelingen](sql-database-advisor.md) voor een overzicht van Azure SQL Database prestaties aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-210">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="5d8b4-211">Zie [inzichten voor queryprestaties](sql-database-query-performance.md) voor meer informatie over het weergeven van de prestatie-invloed van de meest gebruikte query's.</span><span class="sxs-lookup"><span data-stu-id="5d8b4-211">See [Query Performance Insights](sql-database-query-performance.md) to learn about viewing the performance impact of your top queries.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5d8b4-212">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="5d8b4-212">Additional resources</span></span>
* [<span data-ttu-id="5d8b4-213">Query Store</span><span class="sxs-lookup"><span data-stu-id="5d8b4-213">Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx)
* [<span data-ttu-id="5d8b4-214">INDEX MAKEN</span><span class="sxs-lookup"><span data-stu-id="5d8b4-214">CREATE INDEX</span></span>](https://msdn.microsoft.com/library/ms188783.aspx)
* [<span data-ttu-id="5d8b4-215">Toegangsbeheer op basis van rollen</span><span class="sxs-lookup"><span data-stu-id="5d8b4-215">Role-based access control</span></span>](../active-directory/role-based-access-control-what-is.md)

