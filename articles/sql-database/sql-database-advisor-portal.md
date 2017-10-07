---
title: aaaApply prestaties aanbevelingen - Azure SQL Database | Microsoft Docs
description: U kunt hello Azure portal toofind prestaties aanbevelingen die u kunnen de prestaties van uw Azure SQL Database of toocorrect optimaliseren sommige probleem dat is aangetroffen in uw workload.
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
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a><span data-ttu-id="396ce-103">Zoeken en toepassen van aanbevelingen voor prestaties</span><span class="sxs-lookup"><span data-stu-id="396ce-103">Find and apply performance recommendations</span></span>

<span data-ttu-id="396ce-104">U kunt hello Azure portal toofind prestaties aanbevelingen die u kunnen de prestaties van uw Azure SQL Database of toocorrect optimaliseren sommige probleem dat is aangetroffen in uw workload.</span><span class="sxs-lookup"><span data-stu-id="396ce-104">You can use hello Azure portal toofind performance recommendations that can optimize performance of your Azure SQL Database or toocorrect some issue identified in your workload.</span></span> <span data-ttu-id="396ce-105">**Prestaties aanbeveling** pagina in Azure-portal kunt u toofind Hallo bovenste aanbevelingen op basis van de potentiële impact.</span><span class="sxs-lookup"><span data-stu-id="396ce-105">**Performance recommendation** page in Azure portal enables you toofind hello top recommendations based on their potential impact.</span></span> 

## <a name="viewing-recommendations"></a><span data-ttu-id="396ce-106">Aanbevelingen weergeven</span><span class="sxs-lookup"><span data-stu-id="396ce-106">Viewing recommendations</span></span>

<span data-ttu-id="396ce-107">tooview en toepassen van aanbevelingen voor prestaties, u moet Hallo juist [toegangsbeheer op basis van rollen](../active-directory/role-based-access-control-what-is.md) machtigingen in Azure.</span><span class="sxs-lookup"><span data-stu-id="396ce-107">tooview and apply performance recommendations, you need hello correct [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions in Azure.</span></span> <span data-ttu-id="396ce-108">**Lezer**, **SQL DB Contributor** machtigingen zijn vereist tooview-aanbevelingen en **eigenaar**, **SQL DB Contributor** machtigingen zijn vereist tooexecute maatregelen; Maak of verwijder indexen en maken van een index te annuleren.</span><span class="sxs-lookup"><span data-stu-id="396ce-108">**Reader**, **SQL DB Contributor** permissions are required tooview recommendations, and **Owner**, **SQL DB Contributor** permissions are required tooexecute any actions; create or drop indexes and cancel index creation.</span></span>

<span data-ttu-id="396ce-109">Hallo volgende stappen toofind prestaties aanbevelingen in Azure portal gebruiken:</span><span class="sxs-lookup"><span data-stu-id="396ce-109">Use hello following steps toofind performance recommendations on Azure portal:</span></span>

1. <span data-ttu-id="396ce-110">Meld u aan toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="396ce-110">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="396ce-111">Ga te**meer services** > **SQL-databases**, en selecteer uw database.</span><span class="sxs-lookup"><span data-stu-id="396ce-111">Go too**More services** > **SQL databases**, and select your database.</span></span>
3. <span data-ttu-id="396ce-112">Navigeer te**prestaties aanbeveling** tooview beschikbaar aanbevelingen voor de geselecteerde database Hallo.</span><span class="sxs-lookup"><span data-stu-id="396ce-112">Navigate too**Performance recommendation** tooview available recommendations for hello selected database.</span></span>

<span data-ttu-id="396ce-113">Aanbevelingen voor prestaties zijn shonw Hallo vergelijkbare toohello tabel een weergegeven op de volgende afbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="396ce-113">Performance recommendations are shonw in hello table similar toohello one shown on hello following figure:</span></span>

![Aanbevelingen](./media/sql-database-advisor-portal/recommendations.png)

<span data-ttu-id="396ce-115">Aanbevelingen worden gesorteerd op de potentiële impact op de prestaties in Hallo categorieën te volgen:</span><span class="sxs-lookup"><span data-stu-id="396ce-115">Recommendations are sorted by their potential impact on performance into hello following categories:</span></span>

| <span data-ttu-id="396ce-116">Impact</span><span class="sxs-lookup"><span data-stu-id="396ce-116">Impact</span></span> | <span data-ttu-id="396ce-117">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="396ce-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="396ce-118">Hoog</span><span class="sxs-lookup"><span data-stu-id="396ce-118">High</span></span> |<span data-ttu-id="396ce-119">Aanbevelingen voor grote invloed leveren Hallo belangrijkste prestatie-invloed.</span><span class="sxs-lookup"><span data-stu-id="396ce-119">High impact recommendations should provide hello most significant performance impact.</span></span> |
| <span data-ttu-id="396ce-120">Middelgroot</span><span class="sxs-lookup"><span data-stu-id="396ce-120">Medium</span></span> |<span data-ttu-id="396ce-121">Gemiddeld impact aanbevelingen moeten de prestaties verbeteren, maar niet aanzienlijk.</span><span class="sxs-lookup"><span data-stu-id="396ce-121">Medium impact recommendations should improve performance, but not substantially.</span></span> |
| <span data-ttu-id="396ce-122">Laag</span><span class="sxs-lookup"><span data-stu-id="396ce-122">Low</span></span> |<span data-ttu-id="396ce-123">Lage impact aanbevelingen moeten zorgen voor betere prestaties dan zonder, maar mogelijk aanzienlijke verbeteringen niet.</span><span class="sxs-lookup"><span data-stu-id="396ce-123">Low impact recommendations should provide better performance than without, but improvements might not be significant.</span></span> |


> [!NOTE]
> <span data-ttu-id="396ce-124">Azure SQL Database heeft toomonitor activiteiten ten minste een dag in volgorde tooidentify enkele aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="396ce-124">Azure SQL Database needs toomonitor activities at least for a day in order tooidentify some recommendations.</span></span> <span data-ttu-id="396ce-125">Hello Azure SQL Database kunt gemakkelijker optimaliseren voor consistente querypatronen dan dit kunt doen voor willekeurige slechte bursts van activiteit.</span><span class="sxs-lookup"><span data-stu-id="396ce-125">hello Azure SQL Database can more easily optimize for consistent query patterns than it can for random spotty bursts of activity.</span></span> <span data-ttu-id="396ce-126">Als de aanbevelingen zijn niet beschikbaar corrently, Hallo **prestaties aanbeveling** pagina vindt u een bericht waarin wordt uitgelegd waarom.</span><span class="sxs-lookup"><span data-stu-id="396ce-126">If recommendations are not corrently available, hello **Performance recommendation** page provides a message explaining why.</span></span>
> 

<span data-ttu-id="396ce-127">U kunt ook de status Hallo Hallo historische bewerkingen weergeven.</span><span class="sxs-lookup"><span data-stu-id="396ce-127">You can also view hello status of hello historical operations.</span></span> <span data-ttu-id="396ce-128">Selecteer een aanbeveling of status toosee meer details.</span><span class="sxs-lookup"><span data-stu-id="396ce-128">Select a recommendation or status toosee  more details.</span></span>

<span data-ttu-id="396ce-129">Hier volgt een voorbeeld van een aanbeveling 'Index maken' in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="396ce-129">Here is an example of "Create index" recommendation in hello Azure portal.</span></span>

![Index maken](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a><span data-ttu-id="396ce-131">Toepassen van aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="396ce-131">Applying recommendations</span></span>
<span data-ttu-id="396ce-132">Azure SQL Database hebt u volledige controle over hoe aanbevelingen worden ingeschakeld met behulp van een Hallo na drie opties:</span><span class="sxs-lookup"><span data-stu-id="396ce-132">Azure SQL Database gives you full control over how recommendations are enabled using any of hello following three options:</span></span> 

* <span data-ttu-id="396ce-133">Afzonderlijke aanbevelingen één toepassing tegelijk.</span><span class="sxs-lookup"><span data-stu-id="396ce-133">Apply individual recommendations one at a time.</span></span>
* <span data-ttu-id="396ce-134">Schakel Hallo automatische afstemmen tooautomatically toepassen van aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="396ce-134">Enable hello Automatic tuning tooautomatically apply recommendations.</span></span>
* <span data-ttu-id="396ce-135">een aanbeveling tooimplement uitgevoerd handmatig Hallo aanbevolen T-SQL-script op uw database.</span><span class="sxs-lookup"><span data-stu-id="396ce-135">tooimplement a recommendation manually, run hello recommended T-SQL script against your database.</span></span>

<span data-ttu-id="396ce-136">Selecteer elke aanbeveling tooview de details en klik op **script weergeven** tooreview Hallo meer informatie over hoe Hallo aanbeveling wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="396ce-136">Select any recommendation tooview its details and then click **View script** tooreview hello exact details of how hello recommendation is created.</span></span>

<span data-ttu-id="396ce-137">Hallo-database blijft online tijdens het Hallo-aanbeveling wordt toegepast--een database met behulp van de prestaties aanbeveling of automatische afstemming nooit offline neemt.</span><span class="sxs-lookup"><span data-stu-id="396ce-137">hello database remains online while hello recommendation is applied -- using performance recommendation or automatic tuning never takes a database offline.</span></span>

### <a name="apply-an-individual-recommendation"></a><span data-ttu-id="396ce-138">Een afzonderlijke aanbeveling toepassen</span><span class="sxs-lookup"><span data-stu-id="396ce-138">Apply an individual recommendation</span></span>
<span data-ttu-id="396ce-139">U kunt bekijken en aanbevelingen een tegelijk accepteren.</span><span class="sxs-lookup"><span data-stu-id="396ce-139">You can review and accept recommendations one at a time.</span></span>

1. <span data-ttu-id="396ce-140">Op Hallo **aanbevelingen** blade, selecteert u een aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="396ce-140">On hello **Recommendations** blade, select a recommendation.</span></span>
2. <span data-ttu-id="396ce-141">Op Hallo **Details** Klik op de blade **toepassen** knop.</span><span class="sxs-lookup"><span data-stu-id="396ce-141">On hello **Details** blade click **Apply** button.</span></span>
   
    ![Aanbeveling toepassen](./media/sql-database-advisor-portal/apply.png)

<span data-ttu-id="396ce-143">Geselecteerde aanbeveling wordt toegepast op Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="396ce-143">Selected recommendation will be applied on hello database.</span></span>

### <a name="removing-recommendations-from-hello-list"></a><span data-ttu-id="396ce-144">Aanbevelingen verwijderen uit lijst Hallo</span><span class="sxs-lookup"><span data-stu-id="396ce-144">Removing recommendations from hello list</span></span>
<span data-ttu-id="396ce-145">Als uw lijst met aanbevelingen items bevat die u tooremove uit Hallo-lijst wilt, kunt u Hallo aanbeveling negeren:</span><span class="sxs-lookup"><span data-stu-id="396ce-145">If your list of recommendations contains items that you want tooremove from hello list, you can discard hello recommendation:</span></span>

1. <span data-ttu-id="396ce-146">Een aanbeveling selecteren in lijst met Hallo **aanbevelingen** tooopen Hallo details.</span><span class="sxs-lookup"><span data-stu-id="396ce-146">Select a recommendation in hello list of **Recommendations** tooopen hello details.</span></span>
2. <span data-ttu-id="396ce-147">Klik op **negeren** op Hallo **Details** blade.</span><span class="sxs-lookup"><span data-stu-id="396ce-147">Click **Discard** on hello **Details** blade.</span></span>

<span data-ttu-id="396ce-148">Indien gewenst, kunt u toevoegen verwijderde items terug toohello **aanbevelingen** lijst:</span><span class="sxs-lookup"><span data-stu-id="396ce-148">If desired, you can add discarded items back toohello **Recommendations** list:</span></span>

1. <span data-ttu-id="396ce-149">Op Hallo **aanbevelingen** Klik op de blade **weergave verwijderd**.</span><span class="sxs-lookup"><span data-stu-id="396ce-149">On hello **Recommendations** blade click **View discarded**.</span></span>
2. <span data-ttu-id="396ce-150">Selecteer een verwijderde item van Hallo lijst tooview de details ervan.</span><span class="sxs-lookup"><span data-stu-id="396ce-150">Select a discarded item from hello list tooview its details.</span></span>
3. <span data-ttu-id="396ce-151">Klik desgewenst op **ongedaan negeren** tooadd Hallo index back toohello primaire lijst met **aanbevelingen**.</span><span class="sxs-lookup"><span data-stu-id="396ce-151">Optionally, click **Undo Discard** tooadd hello index back toohello main list of **Recommendations**.</span></span>


### <a name="enable-automatic-tuning"></a><span data-ttu-id="396ce-152">Automatisch instellen inschakelen</span><span class="sxs-lookup"><span data-stu-id="396ce-152">Enable automatic tuning</span></span>
<span data-ttu-id="396ce-153">U kunt automatisch hello Azure SQL Database tooimplement aanbevelingen instellen.</span><span class="sxs-lookup"><span data-stu-id="396ce-153">You can set hello Azure SQL Database tooimplement recommendations automatically.</span></span> <span data-ttu-id="396ce-154">Aanbevelingen beschikbaar komen ze automatisch worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="396ce-154">As recommendations become available they will automatically be applied.</span></span> <span data-ttu-id="396ce-155">Als met alle aanbevelingen die worden beheerd door Hallo worden service als Hallo prestatieresultaat negatief Hallo aanbeveling is, teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="396ce-155">As with all recommendations managed by hello service if hello performance impact is negative hello recommendation will be reverted.</span></span>

1. <span data-ttu-id="396ce-156">Op Hallo **aanbevelingen** blade, klikt u op **automatiseren**:</span><span class="sxs-lookup"><span data-stu-id="396ce-156">On hello **Recommendations** blade, click **Automate**:</span></span>
   
    ![Advisor-instellingen](./media/sql-database-advisor-portal/settings.png)
2. <span data-ttu-id="396ce-158">Selecteer de acties die tooautomate:</span><span class="sxs-lookup"><span data-stu-id="396ce-158">Select actions tooautomate:</span></span>
   
    ![Aanbevolen indexen](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a><span data-ttu-id="396ce-160">Handmatig Hallo aanbevolen T-SQL-script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="396ce-160">Manually run hello recommended T-SQL script</span></span>
<span data-ttu-id="396ce-161">Selecteer elke aanbeveling en klik op **script weergeven**.</span><span class="sxs-lookup"><span data-stu-id="396ce-161">Select any recommendation and then click **View script**.</span></span> <span data-ttu-id="396ce-162">Dit script uitvoeren op uw database toomanually Hallo aanbeveling toepassen.</span><span class="sxs-lookup"><span data-stu-id="396ce-162">Run this script against your database toomanually apply hello recommendation.</span></span>

<span data-ttu-id="396ce-163">*Indexen die handmatig worden uitgevoerd wordt niet gecontroleerd en gevalideerd voor prestatie-invloed Hallo service* zodat het wordt aangeraden dat u deze indexen na het maken van tooverify controleren ze bieden betere prestaties en aan te passen of verwijder ze als nodig.</span><span class="sxs-lookup"><span data-stu-id="396ce-163">*Indexes that are manually executed are not monitored and validated for performance impact by hello service* so it is suggested that you monitor these indexes after creation tooverify they provide performance gains and adjust or delete them if necessary.</span></span> <span data-ttu-id="396ce-164">Zie voor meer informatie over het maken van indexen [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span><span class="sxs-lookup"><span data-stu-id="396ce-164">For details about creating indexes, see [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span></span>

### <a name="canceling-recommendations"></a><span data-ttu-id="396ce-165">Aanbevelingen annuleren</span><span class="sxs-lookup"><span data-stu-id="396ce-165">Canceling recommendations</span></span>
<span data-ttu-id="396ce-166">Aanbevelingen die zich in een **in behandeling**, **controleren**, of **geslaagd** status kan worden geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="396ce-166">Recommendations that are in a **Pending**, **Verifying**, or **Success** status can be canceled.</span></span> <span data-ttu-id="396ce-167">Aanbevelingen met de status van **Executing** kan niet worden geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="396ce-167">Recommendations with a status of **Executing** cannot be canceled.</span></span>

1. <span data-ttu-id="396ce-168">Selecteer een aanbeveling in Hallo **afstemmen geschiedenis** gebied tooopen hello **aanbevelingen details** blade.</span><span class="sxs-lookup"><span data-stu-id="396ce-168">Select a recommendation in hello **Tuning History** area tooopen hello **recommendations details** blade.</span></span>
2. <span data-ttu-id="396ce-169">Klik op **annuleren** tooabort Hallo proces van het toepassen van Hallo aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="396ce-169">Click **Cancel** tooabort hello process of applying hello recommendation.</span></span>

## <a name="monitoring-operations"></a><span data-ttu-id="396ce-170">Bewakingsbewerkingen</span><span class="sxs-lookup"><span data-stu-id="396ce-170">Monitoring operations</span></span>
<span data-ttu-id="396ce-171">Toepassen van een aanbeveling kan niet direct gebeuren.</span><span class="sxs-lookup"><span data-stu-id="396ce-171">Applying a recommendation might not happen instantaneously.</span></span> <span data-ttu-id="396ce-172">Hallo-portal biedt gegevens met betrekking tot het Hallo-status van de aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="396ce-172">hello portal provides details regarding hello status of recommendation.</span></span> <span data-ttu-id="396ce-173">Hallo volgen mogelijke statussen van een index worden weergegeven in:</span><span class="sxs-lookup"><span data-stu-id="396ce-173">hello following are possible states that an index can be in:</span></span>

| <span data-ttu-id="396ce-174">Status</span><span class="sxs-lookup"><span data-stu-id="396ce-174">Status</span></span> | <span data-ttu-id="396ce-175">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="396ce-175">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="396ce-176">In behandeling</span><span class="sxs-lookup"><span data-stu-id="396ce-176">Pending</span></span> |<span data-ttu-id="396ce-177">Aanbeveling opdracht is ontvangen en is gepland voor uitvoering toepassen.</span><span class="sxs-lookup"><span data-stu-id="396ce-177">Apply recommendation command has been received and is scheduled for execution.</span></span> |
| <span data-ttu-id="396ce-178">Uitvoeren</span><span class="sxs-lookup"><span data-stu-id="396ce-178">Executing</span></span> |<span data-ttu-id="396ce-179">Hallo-aanbeveling wordt toegepast.</span><span class="sxs-lookup"><span data-stu-id="396ce-179">hello recommendation is being applied.</span></span> |
| <span data-ttu-id="396ce-180">Controleren</span><span class="sxs-lookup"><span data-stu-id="396ce-180">Verifying</span></span> |<span data-ttu-id="396ce-181">Aanbeveling is toegepast en Hallo service meet Hallo voordelen.</span><span class="sxs-lookup"><span data-stu-id="396ce-181">Recommendation was successfully applied and hello service is measuring hello benefits.</span></span> |
| <span data-ttu-id="396ce-182">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="396ce-182">Success</span></span> |<span data-ttu-id="396ce-183">Aanbeveling is toegepast en voordelen zijn gemeten.</span><span class="sxs-lookup"><span data-stu-id="396ce-183">Recommendation was successfully applied and benefits have been measured.</span></span> |
| <span data-ttu-id="396ce-184">Fout</span><span class="sxs-lookup"><span data-stu-id="396ce-184">Error</span></span> |<span data-ttu-id="396ce-185">Er is een fout opgetreden tijdens het Hallo Hallo aanbeveling toe te passen.</span><span class="sxs-lookup"><span data-stu-id="396ce-185">An error occurred during hello process of applying hello recommendation.</span></span> <span data-ttu-id="396ce-186">Dit kan een tijdelijk probleem of mogelijk een tabel met schema wijzigen toohello en Hallo-script is niet meer geldig.</span><span class="sxs-lookup"><span data-stu-id="396ce-186">This can be a transient issue, or possibly a schema change toohello table and hello script is no longer valid.</span></span> |
| <span data-ttu-id="396ce-187">Herstellen van instellingen</span><span class="sxs-lookup"><span data-stu-id="396ce-187">Reverting</span></span> |<span data-ttu-id="396ce-188">Hallo aanbeveling werd toegepast, maar heeft vastgesteld dat is niet zodat en automatisch wordt omgezet.</span><span class="sxs-lookup"><span data-stu-id="396ce-188">hello recommendation was applied, but has been deemed non-performant and is being automatically reverted.</span></span> |
| <span data-ttu-id="396ce-189">Teruggedraaid</span><span class="sxs-lookup"><span data-stu-id="396ce-189">Reverted</span></span> |<span data-ttu-id="396ce-190">Hallo-aanbeveling is hersteld.</span><span class="sxs-lookup"><span data-stu-id="396ce-190">hello recommendation was reverted.</span></span> |

<span data-ttu-id="396ce-191">Klik op een in-process-aanbeveling van Hallo lijst toosee meer informatie:</span><span class="sxs-lookup"><span data-stu-id="396ce-191">Click an in-process recommendation from hello list toosee more details:</span></span>

![Aanbevolen indexen](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a><span data-ttu-id="396ce-193">Herstellen van een aanbeveling</span><span class="sxs-lookup"><span data-stu-id="396ce-193">Reverting a recommendation</span></span>
<span data-ttu-id="396ce-194">Als u Hallo prestaties aanbevelingen tooapply Hallo aanbeveling gebruikt wordt (wat betekent dat u handmatig niet Hallo T-SQL-script hebt uitgevoerd) automatisch overgeschakeld deze als het Hallo prestaties impact toobe negatieve gevonden.</span><span class="sxs-lookup"><span data-stu-id="396ce-194">If you used hello performance recommendations tooapply hello recommendation (meaning you did not manually run hello T-SQL script) it will automatically revert it if it finds hello performance impact toobe negative.</span></span> <span data-ttu-id="396ce-195">Als voor de gewenste gewoon toorevert of andere reden een aanbeveling kunt u doen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="396ce-195">If for any reason you simply want toorevert a recommendation you can do hello following:</span></span>

1. <span data-ttu-id="396ce-196">Selecteer een toegepaste aanbeveling in Hallo **afstemmen geschiedenis** gebied.</span><span class="sxs-lookup"><span data-stu-id="396ce-196">Select a successfully applied recommendation in hello **Tuning history** area.</span></span>
2. <span data-ttu-id="396ce-197">Klik op **Revert** op Hallo **gegevens over de aanbeveling** blade.</span><span class="sxs-lookup"><span data-stu-id="396ce-197">Click **Revert** on hello **recommendation details** blade.</span></span>

![Aanbevolen indexen](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a><span data-ttu-id="396ce-199">Bewaking van prestatie-invloed van de indexaanbevelingen</span><span class="sxs-lookup"><span data-stu-id="396ce-199">Monitoring performance impact of index recommendations</span></span>
<span data-ttu-id="396ce-200">Nadat de aanbevelingen zijn geïmplementeerd (momenteel index-bewerkingen en aanbevelingen voor query's alleen voorzien) kunt u **Query Insights** op Hallo aanbeveling details blade tooopen [Query Inzichten](sql-database-query-performance.md) en Zie Hallo prestatie-invloed van de meest gebruikte query's.</span><span class="sxs-lookup"><span data-stu-id="396ce-200">After recommendations are successfully implemented (currently, index operations and parameterize queries recommendations only) you can click **Query Insights** on hello recommendation details blade tooopen [Query Performance Insights](sql-database-query-performance.md) and see hello performance impact of your top queries.</span></span>

![Prestatie-invloed van monitor](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a><span data-ttu-id="396ce-202">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="396ce-202">Summary</span></span>
<span data-ttu-id="396ce-203">Azure SQL-Database bevat aanbevelingen voor het verbeteren van de prestaties van de SQL-database.</span><span class="sxs-lookup"><span data-stu-id="396ce-203">Azure SQL Database provides recommendations for improving SQL database performance.</span></span> <span data-ttu-id="396ce-204">Dankzij de T-SQL-scripts, evenals afzonderlijke en volledig-automatische, krijgt u een handig hulp bij het optimaliseren van uw database en uiteindelijk queryprestaties te verbeteren.</span><span class="sxs-lookup"><span data-stu-id="396ce-204">By providing T-SQL scripts, as well as individual and fully-automatic, you get a helpful assistance in optimizing your database and ultimately improving query performance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="396ce-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="396ce-205">Next steps</span></span>
<span data-ttu-id="396ce-206">Uw aanbevelingen controleren en doorgaan tooapply ze toorefine prestaties.</span><span class="sxs-lookup"><span data-stu-id="396ce-206">Monitor your recommendations and continue tooapply them toorefine performance.</span></span> <span data-ttu-id="396ce-207">Database-werkbelastingen zijn dynamisch en continu wijzigen.</span><span class="sxs-lookup"><span data-stu-id="396ce-207">Database workloads are dynamic and change continuously.</span></span> <span data-ttu-id="396ce-208">Azure SQL-Database wordt voortgezet toomonitor en doet aanbevelingen die potentieel prestaties van uw database kunnen verbeteren.</span><span class="sxs-lookup"><span data-stu-id="396ce-208">Azure SQL Database will continue toomonitor and provide recommendations that can potentially improve your database's performance.</span></span> 

* <span data-ttu-id="396ce-209">Zie [automatische afstemming](sql-database-automatic-tuning.md) toolearn informatie over Hallo automatische afstemming in Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="396ce-209">See [Automatic tuning](sql-database-automatic-tuning.md) toolearn more about hello automatic tuning in Azure SQL Database.</span></span>
* <span data-ttu-id="396ce-210">Zie [prestaties aanbevelingen](sql-database-advisor.md) voor een overzicht van Azure SQL Database prestaties aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="396ce-210">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="396ce-211">Zie [inzichten voor queryprestaties](sql-database-query-performance.md) toolearn over het weergeven van Hallo prestatie-invloed van de meest gebruikte query's.</span><span class="sxs-lookup"><span data-stu-id="396ce-211">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="396ce-212">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="396ce-212">Additional resources</span></span>
* [<span data-ttu-id="396ce-213">Query Store</span><span class="sxs-lookup"><span data-stu-id="396ce-213">Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx)
* [<span data-ttu-id="396ce-214">INDEX MAKEN</span><span class="sxs-lookup"><span data-stu-id="396ce-214">CREATE INDEX</span></span>](https://msdn.microsoft.com/library/ms188783.aspx)
* [<span data-ttu-id="396ce-215">Toegangsbeheer op basis van rollen</span><span class="sxs-lookup"><span data-stu-id="396ce-215">Role-based access control</span></span>](../active-directory/role-based-access-control-what-is.md)

