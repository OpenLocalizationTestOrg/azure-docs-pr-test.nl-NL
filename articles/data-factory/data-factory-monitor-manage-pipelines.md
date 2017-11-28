---
title: aaaMonitor en pijplijnen beheren met behulp van hello Azure-portal en PowerShell | Microsoft Docs
description: Ontdek hoe toouse hello Azure portal en Azure PowerShell toomonitor en beheren van hello Azure data factory's en pijplijnen die u hebt gemaakt.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: a8d3c7943e79450895ff754f06a37fdad1cbef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-azure-portal-and-powershell"></a><span data-ttu-id="8eed5-103">Bewaken en beheren van Azure Data Factory-pijplijnen met behulp van hello Azure-portal en PowerShell</span><span class="sxs-lookup"><span data-stu-id="8eed5-103">Monitor and manage Azure Data Factory pipelines by using hello Azure portal and PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8eed5-104">Met behulp van Azure portal/Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8eed5-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="8eed5-105">Met bewaking en beheer-app</span><span class="sxs-lookup"><span data-stu-id="8eed5-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> <span data-ttu-id="8eed5-106">Hallo-toepassing voor bewaking en beheer biedt een betere ondersteuning voor bewaking en het beheren van uw gegevenspijplijnen en het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="8eed5-106">hello monitoring & management application provides a better support for monitoring and managing your data pipelines, and troubleshooting any issues.</span></span> <span data-ttu-id="8eed5-107">Zie voor meer informatie over het gebruik van de toepassing hello [bewaken en beheren van Data Factory-pijplijnen met Hallo-app voor bewaking en beheer](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="8eed5-107">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 


<span data-ttu-id="8eed5-108">Dit artikel wordt beschreven hoe u toomonitor, beheren en fouten opsporen in uw pijplijnen met behulp van Azure-portal en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8eed5-108">This article describes how toomonitor, manage, and debug your pipelines by using Azure portal and PowerShell.</span></span> <span data-ttu-id="8eed5-109">Hallo artikel biedt ook informatie over hoe toocreate waarschuwingen en u geïnformeerd over fouten.</span><span class="sxs-lookup"><span data-stu-id="8eed5-109">hello article also provides information on how toocreate alerts and get notified about failures.</span></span>

## <a name="understand-pipelines-and-activity-states"></a><span data-ttu-id="8eed5-110">Pijplijnen en activiteiten statussen begrijpen</span><span class="sxs-lookup"><span data-stu-id="8eed5-110">Understand pipelines and activity states</span></span>
<span data-ttu-id="8eed5-111">U kunt met behulp van hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="8eed5-111">By using hello Azure portal, you can:</span></span>

* <span data-ttu-id="8eed5-112">Uw data factory als een diagram weergeven.</span><span class="sxs-lookup"><span data-stu-id="8eed5-112">View your data factory as a diagram.</span></span>
* <span data-ttu-id="8eed5-113">Activiteiten in een pijplijn weergeven.</span><span class="sxs-lookup"><span data-stu-id="8eed5-113">View activities in a pipeline.</span></span>
* <span data-ttu-id="8eed5-114">Invoer- en uitvoergegevenssets weergeven.</span><span class="sxs-lookup"><span data-stu-id="8eed5-114">View input and output datasets.</span></span>

<span data-ttu-id="8eed5-115">Deze sectie beschrijft ook hoe een segment gegevensset overgangen vanuit één status tooanother status.</span><span class="sxs-lookup"><span data-stu-id="8eed5-115">This section also describes how a dataset slice transitions from one state tooanother state.</span></span>   

### <a name="navigate-tooyour-data-factory"></a><span data-ttu-id="8eed5-116">Navigeer tooyour data factory</span><span class="sxs-lookup"><span data-stu-id="8eed5-116">Navigate tooyour data factory</span></span>
1. <span data-ttu-id="8eed5-117">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8eed5-117">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8eed5-118">Klik op **gegevensfactory** in Hallo-menu op Hallo links.</span><span class="sxs-lookup"><span data-stu-id="8eed5-118">Click **Data factories** on hello menu on hello left.</span></span> <span data-ttu-id="8eed5-119">Als u deze niet ziet, klikt u op **meer services >**, en klik vervolgens op **gegevensfactory** onder Hallo **INTELLIGENCE en analyse** categorie.</span><span class="sxs-lookup"><span data-stu-id="8eed5-119">If you don't see it, click **More services >**, and then click **Data factories** under hello **INTELLIGENCE + ANALYTICS** category.</span></span>

   ![Door alle Bladeren > gegevensfactory's](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. <span data-ttu-id="8eed5-121">Op Hallo **gegevensfactory** blade, selecteer Hallo gegevensfactory die u geïnteresseerd bent in.</span><span class="sxs-lookup"><span data-stu-id="8eed5-121">On hello **Data factories** blade, select hello data factory that you're interested in.</span></span>

    ![Selecteer gegevensfactory](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   <span data-ttu-id="8eed5-123">U ziet de startpagina Hallo voor Hallo data factory.</span><span class="sxs-lookup"><span data-stu-id="8eed5-123">You should see hello home page for hello data factory.</span></span>

   ![Blade gegevensfactory](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a><span data-ttu-id="8eed5-125">Diagramweergave van uw data factory</span><span class="sxs-lookup"><span data-stu-id="8eed5-125">Diagram view of your data factory</span></span>
<span data-ttu-id="8eed5-126">Hallo **Diagram** weergave van een gegevensfactory biedt één van glas toomonitor en Hallo gegevensfactory en bijbehorende assets beheren.</span><span class="sxs-lookup"><span data-stu-id="8eed5-126">hello **Diagram** view of a data factory provides a single pane of glass toomonitor and manage hello data factory and its assets.</span></span> <span data-ttu-id="8eed5-127">Hallo toosee **Diagram** van uw gegevensfactory weergeven, klikt u op **Diagram** op de startpagina Hallo voor Hallo data factory.</span><span class="sxs-lookup"><span data-stu-id="8eed5-127">toosee hello **Diagram** view of your data factory, click **Diagram** on hello home page for hello data factory.</span></span>

![Diagramweergave](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

<span data-ttu-id="8eed5-129">U kunt inzoomen, uitzoomen, zoomen toofit, zoomen too100%, Hallo indeling vergrendelen van Hallo diagram en automatische positie gebruiken voor pijplijnen en gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="8eed5-129">You can zoom in, zoom out, zoom toofit, zoom too100%, lock hello layout of hello diagram, and automatically position pipelines and datasets.</span></span> <span data-ttu-id="8eed5-130">U ziet ook Hallo afkomst gegevens (dat wil zeggen items upstream- en downstreamitems van geselecteerde items weergeven).</span><span class="sxs-lookup"><span data-stu-id="8eed5-130">You can also see hello data lineage information (that is, show upstream and downstream items of selected items).</span></span>

### <a name="activities-inside-a-pipeline"></a><span data-ttu-id="8eed5-131">Activiteiten binnen een pijplijn</span><span class="sxs-lookup"><span data-stu-id="8eed5-131">Activities inside a pipeline</span></span>
1. <span data-ttu-id="8eed5-132">Met de rechtermuisknop op het Hallo-pijplijn en klik vervolgens op **pijplijn openen** toosee alle activiteiten in Hallo pipeline, samen met invoer- en uitvoergegevenssets voor Hallo activiteiten.</span><span class="sxs-lookup"><span data-stu-id="8eed5-132">Right-click hello pipeline, and then click **Open pipeline** toosee all activities in hello pipeline, along with input and output datasets for hello activities.</span></span> <span data-ttu-id="8eed5-133">Deze functie is handig als uw pijplijn meer dan één activiteit bevat en toounderstand Hallo operationele afkomst van één pijplijn gewenste.</span><span class="sxs-lookup"><span data-stu-id="8eed5-133">This feature is useful when your pipeline includes more than one activity and you want toounderstand hello operational lineage of a single pipeline.</span></span>

    ![Menu Pijplijn openen](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. <span data-ttu-id="8eed5-135">In de Hallo voorbeeld te volgen, ziet u een kopieeractiviteit in Hallo-pijplijn met een invoer en uitvoer.</span><span class="sxs-lookup"><span data-stu-id="8eed5-135">In hello following example, you see a copy activity in hello pipeline with an input and an output.</span></span> 

    ![Activiteiten binnen een pijplijn](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. <span data-ttu-id="8eed5-137">U kunt back toohello startpagina van de gegevensfactory Hallo navigeren door te klikken op Hallo **gegevensfactory** koppeling in Hallo breadcrumb op Hallo linkerbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="8eed5-137">You can navigate back toohello home page of hello data factory by clicking hello **Data factory** link in hello breadcrumb at hello top-left corner.</span></span>

    ![Navigeer terug toodata factory](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-hello-state-of-each-activity-inside-a-pipeline"></a><span data-ttu-id="8eed5-139">Hallo-status van elke activiteit in een pijplijn weergeven</span><span class="sxs-lookup"><span data-stu-id="8eed5-139">View hello state of each activity inside a pipeline</span></span>
<span data-ttu-id="8eed5-140">U kunt Hallo huidige status van een activiteit weergeven door Hallo status van Hallo gegevenssets die worden geproduceerd door Hallo activiteit weer te geven.</span><span class="sxs-lookup"><span data-stu-id="8eed5-140">You can view hello current state of an activity by viewing hello status of any of hello datasets that are produced by hello activity.</span></span>

<span data-ttu-id="8eed5-141">Door te dubbelklikken op Hallo **OutputBlobTable** in Hallo **Diagram**, ziet u alle Hallo-segmenten die worden geproduceerd door andere activiteiten bij uitvoering binnen een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="8eed5-141">By double-clicking hello **OutputBlobTable** in hello **Diagram**, you can see all hello slices that are produced by different activity runs inside a pipeline.</span></span> <span data-ttu-id="8eed5-142">U kunt zien of Hallo kopieeractiviteit is uitgevoerd voor Hallo afgelopen acht uur en geproduceerd Hallo segmenten in Hallo **gereed** status.</span><span class="sxs-lookup"><span data-stu-id="8eed5-142">You can see that hello copy activity ran successfully for hello last eight hours and produced hello slices in hello **Ready** state.</span></span>  

![Status van het Hallo-pipeline](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

<span data-ttu-id="8eed5-144">Hallo gegevensset segmenten in de gegevensfactory Hallo kunnen een van volgende statussen Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="8eed5-144">hello dataset slices in hello data factory can have one of hello following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="8eed5-145">Status</span><span class="sxs-lookup"><span data-stu-id="8eed5-145">State</span></span></th><th align="left"><span data-ttu-id="8eed5-146">Subtoestand</span><span class="sxs-lookup"><span data-stu-id="8eed5-146">Substate</span></span></th><th align="left"><span data-ttu-id="8eed5-147">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8eed5-147">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="8eed5-148">Wachten</span><span class="sxs-lookup"><span data-stu-id="8eed5-148">Waiting</span></span></td><td><span data-ttu-id="8eed5-149">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="8eed5-149">ScheduleTime</span></span></td><td><span data-ttu-id="8eed5-150">Hallo-tijd is niet geleverd voor Hallo segment toorun.</span><span class="sxs-lookup"><span data-stu-id="8eed5-150">hello time hasn't come for hello slice toorun.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8eed5-151">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="8eed5-151">DatasetDependencies</span></span></td><td><span data-ttu-id="8eed5-152">Hallo upstream-afhankelijkheden zijn niet gereed.</span><span class="sxs-lookup"><span data-stu-id="8eed5-152">hello upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8eed5-153">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="8eed5-153">ComputeResources</span></span></td><td><span data-ttu-id="8eed5-154">Hallo rekenresources zijn niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="8eed5-154">hello compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8eed5-155">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="8eed5-155">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="8eed5-156">Alle Hallo activiteitsinstanties zijn bezig met het uitvoeren van andere segmenten.</span><span class="sxs-lookup"><span data-stu-id="8eed5-156">All hello activity instances are busy running other slices.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8eed5-157">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="8eed5-157">ActivityResume</span></span></td><td><span data-ttu-id="8eed5-158">Hallo-activiteit is onderbroken en Hallo segmenten kan niet worden uitgevoerd totdat het Hallo-activiteit is hervat.</span><span class="sxs-lookup"><span data-stu-id="8eed5-158">hello activity is paused and can't run hello slices until hello activity is resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8eed5-159">Probeer het opnieuw</span><span class="sxs-lookup"><span data-stu-id="8eed5-159">Retry</span></span></td><td><span data-ttu-id="8eed5-160">Er wordt opnieuw geprobeerd activiteit is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8eed5-160">Activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8eed5-161">Validatie</span><span class="sxs-lookup"><span data-stu-id="8eed5-161">Validation</span></span></td><td><span data-ttu-id="8eed5-162">Validatie is nog niet gestart.</span><span class="sxs-lookup"><span data-stu-id="8eed5-162">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8eed5-163">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="8eed5-163">ValidationRetry</span></span></td><td><span data-ttu-id="8eed5-164">Validatie is wachten toobe opnieuw geprobeerd.</span><span class="sxs-lookup"><span data-stu-id="8eed5-164">Validation is waiting toobe retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="8eed5-165">InProgress</span><span class="sxs-lookup"><span data-stu-id="8eed5-165">InProgress</span></span></td><td><span data-ttu-id="8eed5-166">Valideren</span><span class="sxs-lookup"><span data-stu-id="8eed5-166">Validating</span></span></td><td><span data-ttu-id="8eed5-167">Validatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8eed5-167">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="8eed5-168">Hallo-segment wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="8eed5-168">hello slice is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="8eed5-169">Is mislukt</span><span class="sxs-lookup"><span data-stu-id="8eed5-169">Failed</span></span></td><td><span data-ttu-id="8eed5-170">Time-out</span><span class="sxs-lookup"><span data-stu-id="8eed5-170">TimedOut</span></span></td><td><span data-ttu-id="8eed5-171">Hallo activiteit uitvoeren duurde langer dan is toegestaan door Hallo-activiteit.</span><span class="sxs-lookup"><span data-stu-id="8eed5-171">hello activity execution took longer than what is allowed by hello activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8eed5-172">Geannuleerd</span><span class="sxs-lookup"><span data-stu-id="8eed5-172">Canceled</span></span></td><td><span data-ttu-id="8eed5-173">Hallo-segment is geannuleerd door in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="8eed5-173">hello slice was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8eed5-174">Validatie</span><span class="sxs-lookup"><span data-stu-id="8eed5-174">Validation</span></span></td><td><span data-ttu-id="8eed5-175">Validatie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="8eed5-175">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="8eed5-176">Hallo-segment is mislukt toobe gegenereerd en/of gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="8eed5-176">hello slice failed toobe generated and/or validated.</span></span></td>
</tr>
<td><span data-ttu-id="8eed5-177">Gereed</span><span class="sxs-lookup"><span data-stu-id="8eed5-177">Ready</span></span></td><td>-</td><td><span data-ttu-id="8eed5-178">Hallo-segment is gereed voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="8eed5-178">hello slice is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8eed5-179">Overgeslagen</span><span class="sxs-lookup"><span data-stu-id="8eed5-179">Skipped</span></span></td><td><span data-ttu-id="8eed5-180">Geen</span><span class="sxs-lookup"><span data-stu-id="8eed5-180">None</span></span></td><td><span data-ttu-id="8eed5-181">Hallo-segment wordt niet verwerkt.</span><span class="sxs-lookup"><span data-stu-id="8eed5-181">hello slice isn't being processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8eed5-182">Geen</span><span class="sxs-lookup"><span data-stu-id="8eed5-182">None</span></span></td><td>-</td><td><span data-ttu-id="8eed5-183">Een segment tooexist gebruikt met een andere status, maar is teruggezet.</span><span class="sxs-lookup"><span data-stu-id="8eed5-183">A slice used tooexist with a different status, but it has been reset.</span></span></td>
</tr>
</table>



<span data-ttu-id="8eed5-184">U kunt Hallo details over een segment weergeven door te klikken op een vermelding segment op Hallo **segmenten onlangs bijgewerkt** blade.</span><span class="sxs-lookup"><span data-stu-id="8eed5-184">You can view hello details about a slice by clicking a slice entry on hello **Recently Updated Slices** blade.</span></span>

![Details van het segment](./media/data-factory-monitor-manage-pipelines/slice-details.png)

<span data-ttu-id="8eed5-186">Als het Hallo-segment is meerdere keren uitgevoerd, ziet u meerdere rijen in Hallo **activiteit wordt uitgevoerd** lijst.</span><span class="sxs-lookup"><span data-stu-id="8eed5-186">If hello slice has been executed multiple times, you see multiple rows in hello **Activity runs** list.</span></span> <span data-ttu-id="8eed5-187">U kunt details zien over een activiteit die wordt uitgevoerd door te klikken op Hallo uitvoeren vermelding in Hallo **activiteit wordt uitgevoerd** lijst.</span><span class="sxs-lookup"><span data-stu-id="8eed5-187">You can view details about an activity run by clicking hello run entry in hello **Activity runs** list.</span></span> <span data-ttu-id="8eed5-188">Hallo-lijst bevat alle Hallo-logboekbestanden, samen met een foutbericht als er een.</span><span class="sxs-lookup"><span data-stu-id="8eed5-188">hello list shows all hello log files, along with an error message if there is one.</span></span> <span data-ttu-id="8eed5-189">Deze functie is handig logboeken voor tooview en foutopsporing zonder tooleave uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="8eed5-189">This feature is useful tooview and debug logs without having tooleave your data factory.</span></span>

![Details uitvoering van activiteit](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

<span data-ttu-id="8eed5-191">Als Hallo segment niet in Hallo **gereed** staat, kunt u zien Hallo upstreamsegmenten die niet gereed zijn en blokkeren het huidige segment uitgevoerd Hallo Hallo **upstreamsegmenten die niet gereed** lijst.</span><span class="sxs-lookup"><span data-stu-id="8eed5-191">If hello slice isn't in hello **Ready** state, you can see hello upstream slices that aren't ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span> <span data-ttu-id="8eed5-192">Deze functie is handig als uw segment **wachten** status en u wilt dat toounderstand Hallo upstream-afhankelijkheden die Hallo segment wacht op.</span><span class="sxs-lookup"><span data-stu-id="8eed5-192">This feature is useful when your slice is in **Waiting** state and you want toounderstand hello upstream dependencies that hello slice is waiting on.</span></span>

![Upstreamsegmenten die niet gereed zijn](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a><span data-ttu-id="8eed5-194">DataSet staat diagram</span><span class="sxs-lookup"><span data-stu-id="8eed5-194">Dataset state diagram</span></span>
<span data-ttu-id="8eed5-195">Nadat u een gegevensfactory implementeert en Hallo pijplijnen een ongeldige actieve periode hebben, segmenten Hallo gegevensset overgang van een status tooanother.</span><span class="sxs-lookup"><span data-stu-id="8eed5-195">After you deploy a data factory and hello pipelines have a valid active period, hello dataset slices transition from one state tooanother.</span></span> <span data-ttu-id="8eed5-196">Op dit moment volgt Hallo segment status Hallo status-diagram te volgen:</span><span class="sxs-lookup"><span data-stu-id="8eed5-196">Currently, hello slice status follows hello following state diagram:</span></span>

![Diagram van status](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

<span data-ttu-id="8eed5-198">Hallo gegevensset status overgang stroom in gegevensfactory is de volgende Hallo: wachten-In-voortgang/In uitvoering (Validating) > -> gereed/mislukt.</span><span class="sxs-lookup"><span data-stu-id="8eed5-198">hello dataset state transition flow in data factory is hello following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span></span>

<span data-ttu-id="8eed5-199">Hallo-segment wordt gestart in een **wachten** staat, wacht voorwaarden toobe voldaan voordat deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8eed5-199">hello slice starts in a **Waiting** state, waiting for preconditions toobe met before it executes.</span></span> <span data-ttu-id="8eed5-200">Vervolgens Hallo activiteit wordt uitgevoerd en probeert het Hallo-segment een **In uitvoering** status.</span><span class="sxs-lookup"><span data-stu-id="8eed5-200">Then, hello activity starts executing, and hello slice goes into an **In-Progress** state.</span></span> <span data-ttu-id="8eed5-201">Hallo activiteit is uitgevoerd, kan slagen of mislukken.</span><span class="sxs-lookup"><span data-stu-id="8eed5-201">hello activity execution might succeed or fail.</span></span> <span data-ttu-id="8eed5-202">Hallo-segment is gemarkeerd als **gereed** of **mislukt**, op basis van Hallo resultaat van het Hallo-uitvoering.</span><span class="sxs-lookup"><span data-stu-id="8eed5-202">hello slice is marked as **Ready** or **Failed**, based on hello result of hello execution.</span></span>

<span data-ttu-id="8eed5-203">Kunt u herstellen Hallo segment toogo door Hallo **gereed** of **mislukt** status toohello **wachten** status.</span><span class="sxs-lookup"><span data-stu-id="8eed5-203">You can reset hello slice toogo back from hello **Ready** or **Failed** state toohello **Waiting** state.</span></span> <span data-ttu-id="8eed5-204">U kunt ook Hallo segment de status te markeren**overslaan**, waardoor Hallo-activiteit uit uitgevoerd en geen Hallo segment worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="8eed5-204">You can also mark hello slice state too**Skip**, which prevents hello activity from executing and not processing hello slice.</span></span>

## <a name="pause-and-resume-pipelines"></a><span data-ttu-id="8eed5-205">Onderbreken en hervatten pijplijnen</span><span class="sxs-lookup"><span data-stu-id="8eed5-205">Pause and resume pipelines</span></span>
<span data-ttu-id="8eed5-206">U kunt uw pijplijnen beheren met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8eed5-206">You can manage your pipelines by using Azure PowerShell.</span></span> <span data-ttu-id="8eed5-207">U kunt bijvoorbeeld onderbreken en hervatten van pijplijnen door het uitvoeren van Azure PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="8eed5-207">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span></span> 

> [!NOTE] 
> <span data-ttu-id="8eed5-208">Hallo diagramweergave biedt geen ondersteuning voor het onderbreken en hervatten pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="8eed5-208">hello diagram view does not support pausing and resuming pipelines.</span></span> <span data-ttu-id="8eed5-209">Als u toouse een gebruikersinterface wilt, gebruikt u Hallo controleren en beheren van toepassing.</span><span class="sxs-lookup"><span data-stu-id="8eed5-209">If you want toouse an user interface, use hello monitoring and managing application.</span></span> <span data-ttu-id="8eed5-210">Zie voor meer informatie over het gebruik van de toepassing hello [bewaken en beheren van Data Factory-pijplijnen met Hallo-app voor bewaking en beheer](data-factory-monitor-manage-app.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="8eed5-210">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

<span data-ttu-id="8eed5-211">U kunt onderbreken/uitstellen pijplijnen met behulp van Hallo **onderbreken AzureRmDataFactoryPipeline** PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8eed5-211">You can pause/suspend pipelines by using hello **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span></span> <span data-ttu-id="8eed5-212">Deze cmdlet is handig als u niet dat toorun uw pijplijnen wilt totdat een probleem is opgelost.</span><span class="sxs-lookup"><span data-stu-id="8eed5-212">This cmdlet is useful when you don’t want toorun your pipelines until an issue is fixed.</span></span> 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="8eed5-213">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8eed5-213">For example:</span></span>

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

<span data-ttu-id="8eed5-214">Nadat het Hallo-probleem is opgelost met Hallo pipeline, kunt u Hallo onderbroken pijplijn hervatten door Hallo volgende PowerShell-opdracht uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="8eed5-214">After hello issue has been fixed with hello pipeline, you can resume hello suspended pipeline by running hello following PowerShell command:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="8eed5-215">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8eed5-215">For example:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a><span data-ttu-id="8eed5-216">Fouten opsporen in pijplijnen</span><span class="sxs-lookup"><span data-stu-id="8eed5-216">Debug pipelines</span></span>
<span data-ttu-id="8eed5-217">Azure Data Factory biedt uitgebreide mogelijkheden voor u toodebug en pijplijnen oplossen met behulp van hello Azure-portal en Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8eed5-217">Azure Data Factory provides rich capabilities for you toodebug and troubleshoot pipelines by using hello Azure portal and Azure PowerShell.</span></span>

> <span data-ttu-id="8eed5-218">[! Houd er rekening mee} is veel eenvoudiger tootroubleshot fouten bij het gebruik Hallo bewaking App en beheer.</span><span class="sxs-lookup"><span data-stu-id="8eed5-218">[!NOTE} It is much easier tootroubleshot errors using hello Monitoring & Management App.</span></span> <span data-ttu-id="8eed5-219">Zie voor meer informatie over het gebruik van de toepassing hello [bewaken en beheren van Data Factory-pijplijnen met Hallo-app voor bewaking en beheer](data-factory-monitor-manage-app.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="8eed5-219">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

### <a name="find-errors-in-a-pipeline"></a><span data-ttu-id="8eed5-220">Fouten gevonden in een pijplijn</span><span class="sxs-lookup"><span data-stu-id="8eed5-220">Find errors in a pipeline</span></span>
<span data-ttu-id="8eed5-221">Als Hallo activiteit die wordt uitgevoerd in een pijplijn is mislukt, is het Hallo-gegevensset die wordt geproduceerd door Hallo pijplijn in een foutstatus vanwege fout Hallo.</span><span class="sxs-lookup"><span data-stu-id="8eed5-221">If hello activity run fails in a pipeline, hello dataset that is produced by hello pipeline is in an error state because of hello failure.</span></span> <span data-ttu-id="8eed5-222">U kunt fouten opsporen en oplossen van fouten in Azure Data Factory met behulp van de volgende methoden Hallo.</span><span class="sxs-lookup"><span data-stu-id="8eed5-222">You can debug and troubleshoot errors in Azure Data Factory by using hello following methods.</span></span>

#### <a name="use-hello-azure-portal-toodebug-an-error"></a><span data-ttu-id="8eed5-223">Gebruik hello Azure portal toodebug een fout opgetreden</span><span class="sxs-lookup"><span data-stu-id="8eed5-223">Use hello Azure portal toodebug an error</span></span>
1. <span data-ttu-id="8eed5-224">Op Hallo **tabel** blade, klikt u op Hallo probleem segment dat Hallo is **Status** instellen te**mislukt**.</span><span class="sxs-lookup"><span data-stu-id="8eed5-224">On hello **Table** blade, click hello problem slice that has hello **Status** set too**Failed**.</span></span>

   ![Blade tabel met probleem segment](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. <span data-ttu-id="8eed5-226">Op Hallo **gegevenssegment** blade, klikt u op Hallo activiteit die wordt uitgevoerd die niet zijn geslaagd.</span><span class="sxs-lookup"><span data-stu-id="8eed5-226">On hello **Data slice** blade, click hello activity run that failed.</span></span>

   ![Gegevenssegment met een fout](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. <span data-ttu-id="8eed5-228">Op Hallo **details uitvoering van activiteit** blade kunt u Hallo-bestanden die gekoppeld aan Hallo HDInsight verwerking zijn downloaden.</span><span class="sxs-lookup"><span data-stu-id="8eed5-228">On hello **Activity run details** blade, you can download hello files that are associated with hello HDInsight processing.</span></span> <span data-ttu-id="8eed5-229">Klik op **downloaden** voor Status/stderr toodownload Hallo foutenlogboekbestand met informatie over het Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="8eed5-229">Click **Download** for Status/stderr toodownload hello error log file that contains details about hello error.</span></span>

   ![Activiteit blade toewijzingdetails uitvoeren met de fout](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-toodebug-an-error"></a><span data-ttu-id="8eed5-231">Gebruik PowerShell toodebug een fout opgetreden</span><span class="sxs-lookup"><span data-stu-id="8eed5-231">Use PowerShell toodebug an error</span></span>
1. <span data-ttu-id="8eed5-232">Start **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="8eed5-232">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="8eed5-233">Voer Hallo **Get-AzureRmDataFactorySlice** opdracht toosee Hallo segmenten en hun status.</span><span class="sxs-lookup"><span data-stu-id="8eed5-233">Run hello **Get-AzureRmDataFactorySlice** command toosee hello slices and their statuses.</span></span> <span data-ttu-id="8eed5-234">U ziet een segment met Hallo status **mislukt**.</span><span class="sxs-lookup"><span data-stu-id="8eed5-234">You should see a slice with hello status of **Failed**.</span></span>        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   <span data-ttu-id="8eed5-235">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8eed5-235">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   <span data-ttu-id="8eed5-236">Vervang **StartDateTime** met begintijd van de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="8eed5-236">Replace **StartDateTime** with start time of your pipeline.</span></span> 
3. <span data-ttu-id="8eed5-237">Voer nu Hallo **Get-AzureRmDataFactoryRun** cmdlet tooget gegevens over Hallo activiteit uitvoeren voor Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="8eed5-237">Now, run hello **Get-AzureRmDataFactoryRun** cmdlet tooget details about hello activity run for hello slice.</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    <span data-ttu-id="8eed5-238">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8eed5-238">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    <span data-ttu-id="8eed5-239">Hallo-waarde van StartDateTime is Hallo begintijd voor Hallo fout/probleem segment dat u hebt genoteerd uit de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="8eed5-239">hello value of StartDateTime is hello start time for hello error/problem slice that you noted from hello previous step.</span></span> <span data-ttu-id="8eed5-240">datum / tijd-Hallo moet tussen dubbele aanhalingstekens worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="8eed5-240">hello date-time should be enclosed in double quotes.</span></span>
4. <span data-ttu-id="8eed5-241">Hier ziet u uitvoer met meer informatie over Hallo-fout die is vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="8eed5-241">You should see output with details about hello error that is similar toohello following:</span></span>

    ```   
    Id                      : 841b77c9-d56c-48d1-99a3-8c16c3e77d39
    ResourceGroupName       : ADF
    DataFactoryName         : LogProcessingFactory3
    DatasetName               : EnrichedGameEventsTable
    ProcessingStartTime     : 10/10/2014 3:04:52 AM
    ProcessingEndTime       : 10/10/2014 3:06:49 AM
    PercentComplete         : 0
    DataSliceStart          : 5/5/2014 12:00:00 AM
    DataSliceEnd            : 5/6/2014 12:00:00 AM
    Status                  : FailedExecution
    Timestamp               : 10/10/2014 3:04:52 AM
    RetryAttempt            : 0
    Properties              : {}
    ErrorMessage            : Pig script failed with exit code '5'. See wasb://        adfjobs@spestore.blob.core.windows.net/PigQuery
                                    Jobs/841b77c9-d56c-48d1-99a3-
                8c16c3e77d39/10_10_2014_03_04_53_277/Status/stderr' for
                more details.
    ActivityName            : PigEnrichLogs
    PipelineName            : EnrichGameLogsPipeline
    Type                    :
    ```
5. <span data-ttu-id="8eed5-242">Hallo kan worden uitgevoerd **opslaan AzureRmDataFactoryLog** cmdlet uit met de id-waarde in Hallo uitvoer zien en Hallo logboekbestanden downloaden met behulp van Hallo Hallo **- DownloadLogsoption** voor Hallo-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8eed5-242">You can run hello **Save-AzureRmDataFactoryLog** cmdlet with hello Id value that you see from hello output, and download hello log files by using hello **-DownloadLogsoption** for hello cmdlet.</span></span>

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a><span data-ttu-id="8eed5-243">Fouten in een pijplijn opnieuw uitvoeren</span><span class="sxs-lookup"><span data-stu-id="8eed5-243">Rerun failures in a pipeline</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8eed5-244">Is het eenvoudiger tootroubleshoot fouten en voer mislukte segmenten met behulp van Hallo voor bewaking en beheer-App.</span><span class="sxs-lookup"><span data-stu-id="8eed5-244">It's easier tootroubleshoot errors and rerun failed slices by using hello Monitoring & Management App.</span></span> <span data-ttu-id="8eed5-245">Zie voor meer informatie over het gebruik van de toepassing hello [bewaken en beheren van Data Factory-pijplijnen met Hallo-app voor bewaking en beheer](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="8eed5-245">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 

### <a name="use-hello-azure-portal"></a><span data-ttu-id="8eed5-246">Gebruik hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="8eed5-246">Use hello Azure portal</span></span>
<span data-ttu-id="8eed5-247">Nadat u problemen oplossen en het opsporen van fouten in een pijplijn, kunt u fouten opnieuw uitvoeren door te navigeren toohello fout segment en te klikken op Hallo **uitvoeren** knop op de opdrachtbalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="8eed5-247">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating toohello error slice and clicking hello **Run** button on hello command bar.</span></span>

![Een mislukte segment opnieuw uitvoeren](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

<span data-ttu-id="8eed5-249">In geval Hallo segment heeft validatie is mislukt vanwege een fout van beleid (bijvoorbeeld als gegevens niet beschikbaar is), kunt u Hallo fout corrigeren en validatie opnieuw uit door te klikken op Hallo **valideren** knop op de opdrachtbalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="8eed5-249">In case hello slice has failed validation because of a policy failure (for example, if data isn't available), you can fix hello failure and validate again by clicking hello **Validate** button on hello command bar.</span></span>

![Corrigeer de fouten en valideren](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a><span data-ttu-id="8eed5-251">Azure PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="8eed5-251">Use Azure PowerShell</span></span>
<span data-ttu-id="8eed5-252">U kunt fouten opnieuw uitvoeren met behulp van Hallo **Set-AzureRmDataFactorySliceStatus** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8eed5-252">You can rerun failures by using hello **Set-AzureRmDataFactorySliceStatus** cmdlet.</span></span> <span data-ttu-id="8eed5-253">Zie Hallo [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) onderwerp voor de syntaxis en andere details over Hallo-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8eed5-253">See hello [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) topic for syntax and other details about hello cmdlet.</span></span>

<span data-ttu-id="8eed5-254">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="8eed5-254">**Example:**</span></span>

<span data-ttu-id="8eed5-255">Hallo volgende voorbeeld wordt ingesteld Hallo status van alle segmenten voor Hallo tabel 'DAWikiAggregatedData' too'Waiting' in hello Azure-gegevensfactory 'WikiADF'.</span><span class="sxs-lookup"><span data-stu-id="8eed5-255">hello following example sets hello status of all slices for hello table 'DAWikiAggregatedData' too'Waiting' in hello Azure data factory 'WikiADF'.</span></span>

<span data-ttu-id="8eed5-256">Hallo 'UpdateType' too'UpstreamInPipeline is ingesteld, wat betekent dat de status van elk segment voor Hallo tabel en alle Hallo afhankelijke (upstream) tabellen too'Waiting zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8eed5-256">hello 'UpdateType' is set too'UpstreamInPipeline', which means that statuses of each slice for hello table and all hello dependent (upstream) tables are set too'Waiting'.</span></span> <span data-ttu-id="8eed5-257">Hallo is andere mogelijke waarde voor deze parameter 'Afzonderlijk'.</span><span class="sxs-lookup"><span data-stu-id="8eed5-257">hello other possible value for this parameter is 'Individual'.</span></span>

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a><span data-ttu-id="8eed5-258">Waarschuwingen maken</span><span class="sxs-lookup"><span data-stu-id="8eed5-258">Create alerts</span></span>
<span data-ttu-id="8eed5-259">Azure logboeken gebruikersgebeurtenissen als een Azure-resource (bijvoorbeeld een gegevensfactory) wordt gemaakt, bijgewerkt of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8eed5-259">Azure logs user events when an Azure resource (for example, a data factory) is created, updated, or deleted.</span></span> <span data-ttu-id="8eed5-260">U kunt waarschuwingen maken van deze gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="8eed5-260">You can create alerts on these events.</span></span> <span data-ttu-id="8eed5-261">U kunt gebruiken Gegevensfactory toocapture verschillende metrische gegevens en waarschuwingen maken op de metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="8eed5-261">You can use Data Factory toocapture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="8eed5-262">U wordt aangeraden dat u gebeurtenissen voor realtime-controle en metrische gegevens worden gebruikt voor historische doeleinden.</span><span class="sxs-lookup"><span data-stu-id="8eed5-262">We recommend that you use events for real-time monitoring and use metrics for historical purposes.</span></span>

### <a name="alerts-on-events"></a><span data-ttu-id="8eed5-263">Waarschuwingen over gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="8eed5-263">Alerts on events</span></span>
<span data-ttu-id="8eed5-264">Gebeurtenissen van Azure bieden handig inzicht in wat in uw Azure-resources gebeurt er.</span><span class="sxs-lookup"><span data-stu-id="8eed5-264">Azure events provide useful insights into what is happening in your Azure resources.</span></span> <span data-ttu-id="8eed5-265">Wanneer u van Azure Data Factory gebruikmaakt, gebeurtenissen worden gegenereerd wanneer:</span><span class="sxs-lookup"><span data-stu-id="8eed5-265">When you're using Azure Data Factory, events are generated when:</span></span>

* <span data-ttu-id="8eed5-266">Een gegevensfactory is gemaakt, bijgewerkt of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8eed5-266">A data factory is created, updated, or deleted.</span></span>
* <span data-ttu-id="8eed5-267">Verwerken van gegevens (als 'wordt uitgevoerd') is gestart of voltooid.</span><span class="sxs-lookup"><span data-stu-id="8eed5-267">Data processing (as "runs") has started or completed.</span></span>
* <span data-ttu-id="8eed5-268">Een HDInsight-cluster op aanvraag wordt gemaakt of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8eed5-268">An on-demand HDInsight cluster is created or removed.</span></span>

<span data-ttu-id="8eed5-269">U kunt waarschuwingen van deze gebruikersgebeurtenissen maken en configureren toosend e-mailmeldingen toohello beheerder en coadministrators van Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8eed5-269">You can create alerts on these user events and configure them toosend email notifications toohello administrator and coadministrators of hello subscription.</span></span> <span data-ttu-id="8eed5-270">Bovendien kunt u aanvullende e-mailadressen van de gebruikers hoeven tooreceive e-mailmeldingen Hallo voorwaarden wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="8eed5-270">In addition, you can specify additional email addresses of users who need tooreceive email notifications when hello conditions are met.</span></span> <span data-ttu-id="8eed5-271">Deze functie is handig als u tooget melding op fouten wilt en niet dat de monitor toocontinuously uw gegevensfactory wilt.</span><span class="sxs-lookup"><span data-stu-id="8eed5-271">This feature is useful when you want tooget notified on failures and don’t want toocontinuously monitor your data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="8eed5-272">Op dit moment weergeven niet Hallo portal waarschuwingen op gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="8eed5-272">Currently, hello portal doesn't show alerts on events.</span></span> <span data-ttu-id="8eed5-273">Gebruik Hallo [app voor bewaking en beheer](data-factory-monitor-manage-app.md) toosee alle waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="8eed5-273">Use hello [Monitoring and Management app](data-factory-monitor-manage-app.md) toosee all alerts.</span></span>


#### <a name="specify-an-alert-definition"></a><span data-ttu-id="8eed5-274">Geef een definitie van een waarschuwing</span><span class="sxs-lookup"><span data-stu-id="8eed5-274">Specify an alert definition</span></span>
<span data-ttu-id="8eed5-275">de definitie van een waarschuwing toospecify, u een JSON-bestand met een beschrijving van Hallo-bewerkingen die u wilt dat een melding op toobe maken.</span><span class="sxs-lookup"><span data-stu-id="8eed5-275">toospecify an alert definition, you create a JSON file that describes hello operations that you want toobe alerted on.</span></span> <span data-ttu-id="8eed5-276">In Hallo volgt, verzendt Hallo waarschuwing een e-mailmelding voor Hallo RunFinished bewerking.</span><span class="sxs-lookup"><span data-stu-id="8eed5-276">In hello following example, hello alert sends an email notification for hello RunFinished operation.</span></span> <span data-ttu-id="8eed5-277">specifieke toobe, een e-mailmelding wordt verzonden wanneer een uitvoering in de gegevensfactory Hallo is voltooid en Hallo uitvoeren is mislukt (Status = FailedExecution).</span><span class="sxs-lookup"><span data-stu-id="8eed5-277">toobe specific, an email notification is sent when a run in hello data factory has completed and hello run has failed (Status = FailedExecution).</span></span>

```JSON
{
    "contentVersion": "1.0.0.0",
     "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters": {},
    "resources":
    [
        {
            "name": "ADFAlertsSlice",
            "type": "microsoft.insights/alertrules",
            "apiVersion": "2014-04-01",
            "location": "East US",
            "properties":
            {
                "name": "ADFAlertsSlice",
                "description": "One or more of hello data slices for hello Azure Data Factory has failed processing.",
                "isEnabled": true,
                "condition":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ManagementEventRuleCondition",
                    "dataSource":
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleManagementEventDataSource",
                        "operationName": "RunFinished",
                        "status": "Failed",
                        "subStatus": "FailedExecution"   
                    }
                },
                "action":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails": [ "<your alias>@contoso.com" ]
                }
            }
        }
    ]
}
```

<span data-ttu-id="8eed5-278">U kunt verwijderen **subStatus** van Hallo JSON-definitie als u niet toobe gewaarschuwd op een specifieke fout wilt.</span><span class="sxs-lookup"><span data-stu-id="8eed5-278">You can remove **subStatus** from hello JSON definition if you don’t want toobe alerted on a specific failure.</span></span>

<span data-ttu-id="8eed5-279">In dit voorbeeld wordt een Hallo-waarschuwing voor alle data Factory in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="8eed5-279">This example sets up hello alert for all data factories in your subscription.</span></span> <span data-ttu-id="8eed5-280">Als u wilt dat Hallo waarschuwing toobe instellen voor een bepaalde data factory, kunt u data factory **resourceUri** in Hallo **dataSource**:</span><span class="sxs-lookup"><span data-stu-id="8eed5-280">If you want hello alert toobe set up for a particular data factory, you can specify data factory **resourceUri** in hello **dataSource**:</span></span>

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

<span data-ttu-id="8eed5-281">Hallo bevat volgende tabel Hallo-lijst van beschikbare bewerkingen en statussen (en substatus).</span><span class="sxs-lookup"><span data-stu-id="8eed5-281">hello following table provides hello list of available operations and statuses (and substatuses).</span></span>

| <span data-ttu-id="8eed5-282">De naam van bewerking</span><span class="sxs-lookup"><span data-stu-id="8eed5-282">Operation name</span></span> | <span data-ttu-id="8eed5-283">Status</span><span class="sxs-lookup"><span data-stu-id="8eed5-283">Status</span></span> | <span data-ttu-id="8eed5-284">Substatus</span><span class="sxs-lookup"><span data-stu-id="8eed5-284">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8eed5-285">RunStarted</span><span class="sxs-lookup"><span data-stu-id="8eed5-285">RunStarted</span></span> |<span data-ttu-id="8eed5-286">Gestart</span><span class="sxs-lookup"><span data-stu-id="8eed5-286">Started</span></span> |<span data-ttu-id="8eed5-287">Starting</span><span class="sxs-lookup"><span data-stu-id="8eed5-287">Starting</span></span> |
| <span data-ttu-id="8eed5-288">RunFinished</span><span class="sxs-lookup"><span data-stu-id="8eed5-288">RunFinished</span></span> |<span data-ttu-id="8eed5-289">Kan niet / is voltooid</span><span class="sxs-lookup"><span data-stu-id="8eed5-289">Failed / Succeeded</span></span> |<span data-ttu-id="8eed5-290">FailedResourceAllocation</span><span class="sxs-lookup"><span data-stu-id="8eed5-290">FailedResourceAllocation</span></span><br/><br/><span data-ttu-id="8eed5-291">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="8eed5-291">Succeeded</span></span><br/><br/><span data-ttu-id="8eed5-292">FailedExecution</span><span class="sxs-lookup"><span data-stu-id="8eed5-292">FailedExecution</span></span><br/><br/><span data-ttu-id="8eed5-293">Time-out</span><span class="sxs-lookup"><span data-stu-id="8eed5-293">TimedOut</span></span><br/><br/><span data-ttu-id="8eed5-294">< geannuleerd</span><span class="sxs-lookup"><span data-stu-id="8eed5-294"><Canceled</span></span><br/><br/><span data-ttu-id="8eed5-295">FailedValidation</span><span class="sxs-lookup"><span data-stu-id="8eed5-295">FailedValidation</span></span><br/><br/><span data-ttu-id="8eed5-296">Afgebroken</span><span class="sxs-lookup"><span data-stu-id="8eed5-296">Abandoned</span></span> |
| <span data-ttu-id="8eed5-297">OnDemandClusterCreateStarted</span><span class="sxs-lookup"><span data-stu-id="8eed5-297">OnDemandClusterCreateStarted</span></span> |<span data-ttu-id="8eed5-298">Gestart</span><span class="sxs-lookup"><span data-stu-id="8eed5-298">Started</span></span> | |
| <span data-ttu-id="8eed5-299">OnDemandClusterCreateSuccessful</span><span class="sxs-lookup"><span data-stu-id="8eed5-299">OnDemandClusterCreateSuccessful</span></span> |<span data-ttu-id="8eed5-300">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="8eed5-300">Succeeded</span></span> | |
| <span data-ttu-id="8eed5-301">OnDemandClusterDeleted</span><span class="sxs-lookup"><span data-stu-id="8eed5-301">OnDemandClusterDeleted</span></span> |<span data-ttu-id="8eed5-302">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="8eed5-302">Succeeded</span></span> | |

<span data-ttu-id="8eed5-303">Zie [waarschuwingsregel maken](https://msdn.microsoft.com/library/azure/dn510366.aspx) voor meer informatie over Hallo JSON-elementen die worden gebruikt in het Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="8eed5-303">See [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) for details about hello JSON elements that are used in hello example.</span></span>

#### <a name="deploy-hello-alert"></a><span data-ttu-id="8eed5-304">Hallo waarschuwing implementeren</span><span class="sxs-lookup"><span data-stu-id="8eed5-304">Deploy hello alert</span></span>
<span data-ttu-id="8eed5-305">toodeploy hello waarschuwing, gebruik hello Azure PowerShell-cmdlet **New-AzureRmResourceGroupDeployment**, zoals weergegeven in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="8eed5-305">toodeploy hello alert, use hello Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

<span data-ttu-id="8eed5-306">Nadat de resource Hallo implementatie is voltooid, ziet u Hallo volgende berichten:</span><span class="sxs-lookup"><span data-stu-id="8eed5-306">After hello resource group deployment has finished successfully, you see hello following messages:</span></span>

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - hello StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts tooremove this parameter.
VERBOSE: 7:00:49 PM - Create template deployment 'ADFAlertFailedSlice'.
VERBOSE: 7:00:57 PM - Resource microsoft.insights/alertrules 'ADFAlertsSlice' provisioning status is succeeded

DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

> [!NOTE]
> <span data-ttu-id="8eed5-307">U kunt Hallo [waarschuwingsregel maken](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST-API toocreate een waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="8eed5-307">You can use hello [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API toocreate an alert rule.</span></span> <span data-ttu-id="8eed5-308">Hallo JSON-nettolading is vergelijkbaar toohello JSON-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="8eed5-308">hello JSON payload is similar toohello JSON example.</span></span>  


#### <a name="retrieve-hello-list-of-azure-resource-group-deployments"></a><span data-ttu-id="8eed5-309">Hallo-lijst met Azure resourcegroepimplementaties ophalen</span><span class="sxs-lookup"><span data-stu-id="8eed5-309">Retrieve hello list of Azure resource group deployments</span></span>
<span data-ttu-id="8eed5-310">tooretrieve hello lijst met Azure resourcegroepimplementaties geïmplementeerd, gebruikt u de cmdlet Hallo **Get-AzureRmResourceGroupDeployment**, zoals weergegeven in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="8eed5-310">tooretrieve hello list of deployed Azure resource group deployments, use hello cmdlet **Get-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
Get-AzureRmResourceGroupDeployment -ResourceGroupName adf
```

```
DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

#### <a name="troubleshoot-user-events"></a><span data-ttu-id="8eed5-311">Oplossen van gebruikersgebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="8eed5-311">Troubleshoot user events</span></span>
1. <span data-ttu-id="8eed5-312">U kunt zien dat alle Hallo-gebeurtenissen die worden gegenereerd wanneer u op Hallo **metrische gegevens en bewerkingen** tegel.</span><span class="sxs-lookup"><span data-stu-id="8eed5-312">You can see all hello events that are generated after clicking hello **Metrics and operations** tile.</span></span>

    ![Tegel metrische gegevens en bewerkingen](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. <span data-ttu-id="8eed5-314">Klik op Hallo **gebeurtenissen** tegel toosee Hallo gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="8eed5-314">Click hello **Events** tile toosee hello events.</span></span>

    ![Tegel gebeurtenissen](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. <span data-ttu-id="8eed5-316">Op Hallo **gebeurtenissen** blade ziet u informatie over gebeurtenissen en gefilterde gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="8eed5-316">On hello **Events** blade, you can see details about events, filtered events, and so on.</span></span>

    ![Blade gebeurtenissen](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. <span data-ttu-id="8eed5-318">Klik op een **bewerking** in de lijst met bewerkingen Hallo dat een fout veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="8eed5-318">Click an **Operation** in hello operations list that causes an error.</span></span>

    ![Een bewerking selecteren](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. <span data-ttu-id="8eed5-320">Klik op een **fout** toosee Gebeurtenisdetails over Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="8eed5-320">Click an **Error** event toosee details about hello error.</span></span>

    ![Fout van gebeurtenis](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

<span data-ttu-id="8eed5-322">Zie [inzicht van Azure-cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) ophalen of verwijderen van waarschuwingen voor PowerShell-cmdlets waarmee u tooadd kunt.</span><span class="sxs-lookup"><span data-stu-id="8eed5-322">See [Azure Insight cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) for PowerShell cmdlets that you can use tooadd, get, or remove alerts.</span></span> <span data-ttu-id="8eed5-323">Hier volgen enkele voorbeelden van het gebruik van Hallo **Get-AlertRule** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8eed5-323">Here are a few examples of using hello **Get-AlertRule** cmdlet:</span></span>

```powershell
get-alertrule -res $resourceGroup -n ADFAlertsSlice -det
```

```
Properties :
Action      : Microsoft.Azure.Management.Insights.Models.RuleEmailAction
Condition   :
DataSource :
EventName             :
Category              :
Level                 :
OperationName         : RunFinished
ResourceGroupName     :
ResourceProviderName  :
ResourceId            :
Status                : Failed
SubStatus             : FailedExecution
Claims                : Microsoft.Azure.Management.Insights.Models.RuleManagementEventClaimsDataSource
Condition      :
Description : One or more of hello data slices for hello Azure Data Factory has failed processing.
Status      : Enabled
Name:       : ADFAlertsSlice
Tags       :
$type          : Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/ADFAlertsSlice
Location   : West US
Name       : ADFAlertsSlice
```

```powershell
Get-AlertRule -res $resourceGroup
```
```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0

Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest3
Location   : West US
Name       : FailedExecutionRunsWest3
```

```powershell
Get-AlertRule -res $resourceGroup -Name FailedExecutionRunsWest0
```

```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0
```

<span data-ttu-id="8eed5-324">Hallo na de get-help opdrachten toosee details en voorbeelden voor Hallo Get AlertRule cmdlet wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8eed5-324">Run hello following get-help commands toosee details and examples for hello Get-AlertRule cmdlet.</span></span>

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


<span data-ttu-id="8eed5-325">Als er Hallo genereren van waarschuwingen gebeurtenissen op Hallo portalblade, maar u geen e-mailmeldingen ontvangen, controleert u of Hallo e-mailadres dat is opgegeven tooreceive e-mailberichten van externe afzenders is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8eed5-325">If you see hello alert generation events on hello portal blade but you don't receive email notifications, check whether hello email address that is specified is set tooreceive emails from external senders.</span></span> <span data-ttu-id="8eed5-326">Hallo e-mailwaarschuwingen is mogelijk geblokkeerd door uw e-mailinstellingen.</span><span class="sxs-lookup"><span data-stu-id="8eed5-326">hello alert emails might have been blocked by your email settings.</span></span>

### <a name="alerts-on-metrics"></a><span data-ttu-id="8eed5-327">Waarschuwingen op metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="8eed5-327">Alerts on metrics</span></span>
<span data-ttu-id="8eed5-328">U kunt verschillende metrische gegevens vastleggen en waarschuwingen maken op de metrische gegevens in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8eed5-328">In Data Factory, you can capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="8eed5-329">U kunt bewaken en waarschuwingen maken op Hallo metrische gegevens voor Hallo segmenten in de gegevensfactory te volgen:</span><span class="sxs-lookup"><span data-stu-id="8eed5-329">You can monitor and create alerts on hello following metrics for hello slices in your data factory:</span></span>

* <span data-ttu-id="8eed5-330">**Mislukte wordt uitgevoerd**</span><span class="sxs-lookup"><span data-stu-id="8eed5-330">**Failed Runs**</span></span>
* <span data-ttu-id="8eed5-331">**Geslaagde wordt uitgevoerd**</span><span class="sxs-lookup"><span data-stu-id="8eed5-331">**Successful Runs**</span></span>

<span data-ttu-id="8eed5-332">Deze metrische gegevens zijn nuttig en helpt u een overzicht van de algemene mislukte en geslaagde wordt uitgevoerd in de gegevensfactory hello tooget.</span><span class="sxs-lookup"><span data-stu-id="8eed5-332">These metrics are useful and help you tooget an overview of overall failed and successful runs in hello data factory.</span></span> <span data-ttu-id="8eed5-333">Metrische gegevens zijn verzonden, elke keer dat er wordt een segment uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8eed5-333">Metrics are emitted every time there is a slice run.</span></span> <span data-ttu-id="8eed5-334">Aan het begin van de Hallo van Hallo uur, wordt deze metrische gegevens worden geaggregeerd en gepusht tooyour storage-account.</span><span class="sxs-lookup"><span data-stu-id="8eed5-334">At hello beginning of hello hour, these metrics are aggregated and pushed tooyour storage account.</span></span> <span data-ttu-id="8eed5-335">metrische gegevens voor tooenable, instellen van een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="8eed5-335">tooenable metrics, set up a storage account.</span></span>

#### <a name="enable-metrics"></a><span data-ttu-id="8eed5-336">Metrische gegevens inschakelen</span><span class="sxs-lookup"><span data-stu-id="8eed5-336">Enable metrics</span></span>
<span data-ttu-id="8eed5-337">tooenable metrische gegevens en klik op volgende Hallo van Hallo **Data Factory** blade:</span><span class="sxs-lookup"><span data-stu-id="8eed5-337">tooenable metrics, click hello following from hello **Data Factory** blade:</span></span>

<span data-ttu-id="8eed5-338">**Bewaking** > **metriek** > **diagnostische instellingen** > **diagnostische gegevens**</span><span class="sxs-lookup"><span data-stu-id="8eed5-338">**Monitoring** > **Metric** > **Diagnostic settings** > **Diagnostics**</span></span>

![Diagnostische gegevens koppelen](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

<span data-ttu-id="8eed5-340">Op Hallo **Diagnostics** blade, klikt u op **op**, selecteer Hallo storage-account en klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8eed5-340">On hello **Diagnostics** blade, click **On**, select hello storage account, and click **Save**.</span></span>

![Blade diagnostische gegevens](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

<span data-ttu-id="8eed5-342">Het Hallo metrische gegevens toobe zichtbaar zijn op Hallo tooone uur kan duren **bewaking** blade omdat metrische gegevens aggregatie per uur gebeurt.</span><span class="sxs-lookup"><span data-stu-id="8eed5-342">It might take up tooone hour for hello metrics toobe visible on hello **Monitoring** blade because metrics aggregation happens hourly.</span></span>

### <a name="set-up-an-alert-on-metrics"></a><span data-ttu-id="8eed5-343">Instellen van een waarschuwing op metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="8eed5-343">Set up an alert on metrics</span></span>
<span data-ttu-id="8eed5-344">Klik op Hallo **Data Factory metrische gegevens** tegel:</span><span class="sxs-lookup"><span data-stu-id="8eed5-344">Click hello **Data Factory metrics** tile:</span></span>

![Data factory metrische gegevens tegel](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

<span data-ttu-id="8eed5-346">Op Hallo **metriek** blade, klikt u op **+ waarschuwing toevoegen** op Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="8eed5-346">On hello **Metric** blade, click **+ Add alert** on hello toolbar.</span></span>
<span data-ttu-id="8eed5-347">![Metrische blade gegevensfactory > Waarschuwing toevoegen](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span><span class="sxs-lookup"><span data-stu-id="8eed5-347">![Data factory metric blade > Add alert](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span></span>

<span data-ttu-id="8eed5-348">Op Hallo **een waarschuwingsregel toevoegen** pagina Hallo van de volgende stappen uit en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8eed5-348">On hello **Add an alert rule** page, do hello following steps, and click **OK**.</span></span>

* <span data-ttu-id="8eed5-349">Voer een naam voor de waarschuwing hello (voorbeeld: 'is mislukt van de waarschuwing').</span><span class="sxs-lookup"><span data-stu-id="8eed5-349">Enter a name for hello alert (example: "failed alert").</span></span>
* <span data-ttu-id="8eed5-350">Voer een beschrijving van waarschuwing hello (voorbeeld: 'een e-mailbericht verzenden wanneer een fout optreedt').</span><span class="sxs-lookup"><span data-stu-id="8eed5-350">Enter a description for hello alert (example: "send an email when a failure occurs").</span></span>
* <span data-ttu-id="8eed5-351">Selecteer een waarde (vs "Wordt uitgevoerd is mislukt". 'Geslaagd wordt uitgevoerd').</span><span class="sxs-lookup"><span data-stu-id="8eed5-351">Select a metric ("Failed Runs" vs. "Successful Runs").</span></span>
* <span data-ttu-id="8eed5-352">Geef een voorwaarde en de drempelwaarde.</span><span class="sxs-lookup"><span data-stu-id="8eed5-352">Specify a condition and a threshold value.</span></span>   
* <span data-ttu-id="8eed5-353">Hallo periode opgeven.</span><span class="sxs-lookup"><span data-stu-id="8eed5-353">Specify hello period of time.</span></span>
* <span data-ttu-id="8eed5-354">Geef op of een e-mailbericht moet worden verzonden tooowners, bijdragers en lezers.</span><span class="sxs-lookup"><span data-stu-id="8eed5-354">Specify whether an email should be sent tooowners, contributors, and readers.</span></span>

![Metrische blade gegevensfactory > waarschuwingsregel toevoegen](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

<span data-ttu-id="8eed5-356">Nadat Hallo waarschuwingsregel is toegevoegd, Hallo blade wordt gesloten en er nieuwe waarschuwing Hallo op Hallo **metriek** blade.</span><span class="sxs-lookup"><span data-stu-id="8eed5-356">After hello alert rule is added successfully, hello blade closes and you see hello new alert on hello **Metric** blade.</span></span>

![Metrische blade gegevensfactory > nieuwe waarschuwing toegevoegd](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

<span data-ttu-id="8eed5-358">U ziet ook het aantal waarschuwingen in Hallo Hallo **waarschuwing regels** tegel.</span><span class="sxs-lookup"><span data-stu-id="8eed5-358">You should also see hello number of alerts in hello **Alert rules** tile.</span></span> <span data-ttu-id="8eed5-359">Klik op Hallo **waarschuwing regels** tegel.</span><span class="sxs-lookup"><span data-stu-id="8eed5-359">Click hello **Alert rules** tile.</span></span>

![Metrische blade gegevensfactory - regels voor waarschuwingen](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

<span data-ttu-id="8eed5-361">Op Hallo **regels waarschuwingen** blade ziet u een bestaande waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="8eed5-361">On hello **Alerts rules** blade, you see any existing alerts.</span></span> <span data-ttu-id="8eed5-362">tooadd een waarschuwing, klikt u op **waarschuwing toevoegen** op Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="8eed5-362">tooadd an alert, click **Add alert** on hello toolbar.</span></span>

![Regels voor waarschuwingen-blade](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a><span data-ttu-id="8eed5-364">Meldingen van waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="8eed5-364">Alert notifications</span></span>
<span data-ttu-id="8eed5-365">Nadat de waarschuwingsregel Hallo overeenkomt met Hallo voorwaarde, krijgt u een e-mailbericht met de tekst hello waarschuwing is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="8eed5-365">After hello alert rule matches hello condition, you should get an email that says hello alert is activated.</span></span> <span data-ttu-id="8eed5-366">Nadat de Hallo probleem is opgelost en Hallo meldingsvoorwaarde meer komt niet overeen, krijgt u een e-mailbericht met de tekst hello waarschuwing is opgelost.</span><span class="sxs-lookup"><span data-stu-id="8eed5-366">After hello issue is resolved and hello alert condition doesn’t match anymore, you get an email that says hello alert is resolved.</span></span>

<span data-ttu-id="8eed5-367">Dit gedrag is anders dan gebeurtenissen waarbij een melding wordt verzonden op elke fout die een waarschuwingsregel in aanmerking komt voor.</span><span class="sxs-lookup"><span data-stu-id="8eed5-367">This behavior is different than events where a notification is sent on every failure that an alert rule qualifies for.</span></span>

### <a name="deploy-alerts-by-using-powershell"></a><span data-ttu-id="8eed5-368">Waarschuwingen implementeren met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="8eed5-368">Deploy alerts by using PowerShell</span></span>
<span data-ttu-id="8eed5-369">U kunt waarschuwingen kunt implementeren voor metrische gegevens Hallo dezelfde manier voor gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="8eed5-369">You can deploy alerts for metrics hello same way that you do for events.</span></span>

<span data-ttu-id="8eed5-370">**Definitie van waarschuwing**</span><span class="sxs-lookup"><span data-stu-id="8eed5-370">**Alert definition**</span></span>

```JSON
{
    "contentVersion" : "1.0.0.0",
    "$schema" : "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters" : {},
    "resources" : [
    {
            "name" : "FailedRunsGreaterThan5",
            "type" : "microsoft.insights/alertrules",
            "apiVersion" : "2014-04-01",
            "location" : "East US",
            "properties" : {
                "name" : "FailedRunsGreaterThan5",
                "description" : "Failed Runs greater than 5",
                "isEnabled" : true,
                "condition" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource" : {
                        "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
                        "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName
>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>",
                        "metricName" : "FailedRuns"
                    },
                    "threshold" : 5.0,
                    "windowSize" : "PT3H",
                    "timeAggregation" : "Total"
                },
                "action" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails" : ["abhinav.gpt@live.com"]
                }
            }
        }
    ]
}
```

<span data-ttu-id="8eed5-371">Vervang *subscriptionId*, *resourceGroupName*, en *dataFactoryName* in Hallo voorbeeld met de juiste waarden.</span><span class="sxs-lookup"><span data-stu-id="8eed5-371">Replace *subscriptionId*, *resourceGroupName*, and *dataFactoryName* in hello sample with appropriate values.</span></span>

<span data-ttu-id="8eed5-372">*metricName* ondersteunt momenteel twee waarden:</span><span class="sxs-lookup"><span data-stu-id="8eed5-372">*metricName* currently supports two values:</span></span>

* <span data-ttu-id="8eed5-373">FailedRuns</span><span class="sxs-lookup"><span data-stu-id="8eed5-373">FailedRuns</span></span>
* <span data-ttu-id="8eed5-374">SuccessfulRuns</span><span class="sxs-lookup"><span data-stu-id="8eed5-374">SuccessfulRuns</span></span>

<span data-ttu-id="8eed5-375">**Hallo waarschuwing implementeren**</span><span class="sxs-lookup"><span data-stu-id="8eed5-375">**Deploy hello alert**</span></span>

<span data-ttu-id="8eed5-376">toodeploy hello waarschuwing, gebruik hello Azure PowerShell-cmdlet **New-AzureRmResourceGroupDeployment**, zoals weergegeven in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="8eed5-376">toodeploy hello alert, use hello Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

<span data-ttu-id="8eed5-377">Ziet het volgende bericht na een geslaagde implementatie:</span><span class="sxs-lookup"><span data-stu-id="8eed5-377">You should see following message after a successful deployment:</span></span>

```
VERBOSE: 12:52:47 PM - Template is valid.
VERBOSE: 12:52:48 PM - Create template deployment 'FailedRunsGreaterThan5'.
VERBOSE: 12:52:55 PM - Resource microsoft.insights/alertrules 'FailedRunsGreaterThan5' provisioning status is succeeded


DeploymentName    : FailedRunsGreaterThan5
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 7/27/2015 7:52:56 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           
```

<span data-ttu-id="8eed5-378">U kunt ook Hallo **toevoegen AlertRule** cmdlet toodeploy een waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="8eed5-378">You can also use hello **Add-AlertRule** cmdlet toodeploy an alert rule.</span></span> <span data-ttu-id="8eed5-379">Zie Hallo [toevoegen AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) onderwerp voor meer informatie en voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="8eed5-379">See hello [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) topic for details and examples.</span></span>  

## <a name="move-a-data-factory-tooa-different-resource-group-or-subscription"></a><span data-ttu-id="8eed5-380">Een data factory tooa andere resourcegroep of abonnement verplaatsen</span><span class="sxs-lookup"><span data-stu-id="8eed5-380">Move a data factory tooa different resource group or subscription</span></span>
<span data-ttu-id="8eed5-381">U kunt een data factory tooa andere resourcegroep of een ander abonnement verplaatsen met behulp van Hallo **verplaatsen** opdracht balk knop op de startpagina Hallo van uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="8eed5-381">You can move a data factory tooa different resource group or a different subscription by using hello **Move** command bar button on hello home page of your data factory.</span></span>

![Verplaatsen van de gegevensfactory](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

<span data-ttu-id="8eed5-383">U kunt ook alle gerelateerde resources (zoals waarschuwingen die gekoppeld aan de gegevensfactory Hallo zijn), samen met de Hallo gegevensfactory verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="8eed5-383">You can also move any related resources (such as alerts that are associated with hello data factory), along with hello data factory.</span></span>

![Dialoogvenster resources verplaatsen](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
