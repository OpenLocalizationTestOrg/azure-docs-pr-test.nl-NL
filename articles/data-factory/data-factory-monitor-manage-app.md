---
title: aaaMonitor en gegevenspijplijnen - Azure beheren | Microsoft Docs
description: Ontdek hoe toouse Hallo toomonitor voor bewaking en beheer-app en beheren van Azure data factory's en pijplijnen.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: 5e4ef6ec5fb8ebc9bda0be7899a39a51d58403d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-monitoring-and-management-app"></a><span data-ttu-id="169c5-103">Bewaken en beheren van Azure Data Factory-pijplijnen met Hallo-app voor bewaking en beheer</span><span class="sxs-lookup"><span data-stu-id="169c5-103">Monitor and manage Azure Data Factory pipelines by using hello Monitoring and Management app</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="169c5-104">Met behulp van Azure portal/Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="169c5-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="169c5-105">Met bewaking en beheer-app</span><span class="sxs-lookup"><span data-stu-id="169c5-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)
>
>

<span data-ttu-id="169c5-106">Dit artikel wordt beschreven hoe toouse Hallo app toomonitor voor bewaking en beheer, beheren en fouten opsporen in uw Data Factory-pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="169c5-106">This article describes how toouse hello Monitoring and Management app toomonitor, manage, and debug your Data Factory pipelines.</span></span> <span data-ttu-id="169c5-107">Het biedt ook informatie over hoe toocreate tooget melding op fouten waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="169c5-107">It also provides information on how toocreate alerts tooget notified on failures.</span></span> <span data-ttu-id="169c5-108">U kunt aan de slag met het gebruik van de toepassing hello door te kijken Hallo volgende video:</span><span class="sxs-lookup"><span data-stu-id="169c5-108">You can get started with using hello application by watching hello following video:</span></span>

> [!NOTE]
> <span data-ttu-id="169c5-109">Hallo-gebruikersinterface wordt weergegeven in Hallo video mogelijk niet precies overeenkomt met wat u ziet in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="169c5-109">hello user interface shown in hello video may not exactly match what you see in hello portal.</span></span> <span data-ttu-id="169c5-110">Het iets oudere is, maar concepten Hallo blijven hetzelfde.</span><span class="sxs-lookup"><span data-stu-id="169c5-110">It's slightly older, but concepts remain hello same.</span></span> 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-hello-monitoring-and-management-app"></a><span data-ttu-id="169c5-111">Hallo bewaking en beheer-app starten</span><span class="sxs-lookup"><span data-stu-id="169c5-111">Launch hello Monitoring and Management app</span></span>
<span data-ttu-id="169c5-112">toolaunch hello Monitor en app Management, klikt u op Hallo **Monitor & beheren** tegel op Hallo **Data Factory** blade van uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="169c5-112">toolaunch hello Monitor and Management app, click hello **Monitor & Manage** tile on hello **Data Factory** blade for your data factory.</span></span>

![Bewaking van de tegel op Hallo Data Factory-startpagina](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

<span data-ttu-id="169c5-114">U ziet Hallo bewaking en beheer app in een apart venster geopend.</span><span class="sxs-lookup"><span data-stu-id="169c5-114">You should see hello Monitoring and Management app open in a separate window.</span></span>  

![App voor controle en beheer](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> <span data-ttu-id="169c5-116">Als u ziet dat Hallo webbrowser is vastgelopen bij 'Autoriseren...', schakelt u Hallo **blokkeren van cookies van derden en sitegegevens** selectievakje-- of houd deze is geselecteerd, maakt u een uitzondering voor **login.microsoftonline.com** , en probeer het vervolgens opnieuw tooopen Hallo app.</span><span class="sxs-lookup"><span data-stu-id="169c5-116">If you see that hello web browser is stuck at "Authorizing...", clear hello **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try tooopen hello app again.</span></span>


<span data-ttu-id="169c5-117">In Hallo Activiteitsvensters lijst in het middelste deelvenster hello ziet u een venster van de activiteit voor elke uitvoering van een activiteit.</span><span class="sxs-lookup"><span data-stu-id="169c5-117">In hello Activity Windows list in hello middle pane, you see an activity window for each run of an activity.</span></span> <span data-ttu-id="169c5-118">Als u Hallo activiteit gepland toorun elk uur gedurende vijf uur hebt, ziet u bijvoorbeeld vijf activiteit windows die zijn gekoppeld aan vijf gegevenssegmenten.</span><span class="sxs-lookup"><span data-stu-id="169c5-118">For example, if you have hello activity scheduled toorun hourly for five hours, you see five activity windows associated with five data slices.</span></span> <span data-ttu-id="169c5-119">Als er geen activiteit windows in de lijst Hallo Hallo onderin, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="169c5-119">If you don't see activity windows in hello list at hello bottom, do hello following:</span></span>
 
- <span data-ttu-id="169c5-120">Update Hallo **begintijd** en **eindtijd** filters op Hallo bovenste toomatch Hallo start en eindtijd van de pijplijn en klik op Hallo **toepassen** knop.</span><span class="sxs-lookup"><span data-stu-id="169c5-120">Update hello **start time** and **end time** filters at hello top toomatch hello start and end times of your pipeline, and then click hello **Apply** button.</span></span>  
- <span data-ttu-id="169c5-121">lijst van de activiteit Windows Hello wordt niet automatisch vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="169c5-121">hello Activity Windows list is not automatically refreshed.</span></span> <span data-ttu-id="169c5-122">Klik op Hallo **vernieuwen** op de werkbalk in Hallo Hallo **Activiteitsvensters** lijst.</span><span class="sxs-lookup"><span data-stu-id="169c5-122">Click hello **Refresh** button on hello toolbar in hello **Activity Windows** list.</span></span>  

<span data-ttu-id="169c5-123">Als u geen deze stappen met een tootest Data Factory-toepassing, zelfstudie Hallo: [gegevens kopiëren van Blob Storage tooSQL-Database met de Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="169c5-123">If you don't have a Data Factory application tootest these steps with, do hello tutorial: [copy data from Blob Storage tooSQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="understand-hello-monitoring-and-management-app"></a><span data-ttu-id="169c5-124">Hallo-app voor bewaking en beheer begrijpen</span><span class="sxs-lookup"><span data-stu-id="169c5-124">Understand hello Monitoring and Management app</span></span>
<span data-ttu-id="169c5-125">Er zijn drie tabbladen aan de linkerkant Hallo: **Resource Explorer**, **weergaven**, en **waarschuwingen**.</span><span class="sxs-lookup"><span data-stu-id="169c5-125">There are three tabs on hello left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span></span> <span data-ttu-id="169c5-126">het eerste tabblad hello (**Resource Explorer**) is standaard geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="169c5-126">hello first tab (**Resource Explorer**) is selected by default.</span></span>

### <a name="resource-explorer"></a><span data-ttu-id="169c5-127">Resource Explorer</span><span class="sxs-lookup"><span data-stu-id="169c5-127">Resource Explorer</span></span>
<span data-ttu-id="169c5-128">U ziet Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="169c5-128">You see hello following:</span></span>

* <span data-ttu-id="169c5-129">Hallo Resource Explorer **structuurweergave** in het linkerdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="169c5-129">hello Resource Explorer **tree view** in hello left pane.</span></span>
* <span data-ttu-id="169c5-130">Hallo **diagramweergave** Hallo boven in het middelste deelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="169c5-130">hello **Diagram View** at hello top in hello middle pane.</span></span>
* <span data-ttu-id="169c5-131">Hallo **Activiteitsvensters** lijst Hallo onderaan in het middelste deelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="169c5-131">hello **Activity Windows** list at hello bottom in hello middle pane.</span></span>
* <span data-ttu-id="169c5-132">Hallo **eigenschappen**, **activiteit venster Explorer**, en **Script** tabbladen in het rechterdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="169c5-132">hello **Properties**, **Activity Window Explorer**, and **Script** tabs in hello right pane.</span></span>

<span data-ttu-id="169c5-133">In Resource Explorer ziet u alle resources (pijplijnen, gegevenssets, gekoppelde services) in de gegevensfactory Hallo in een boomstructuur.</span><span class="sxs-lookup"><span data-stu-id="169c5-133">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in hello data factory in a tree view.</span></span> <span data-ttu-id="169c5-134">Wanneer u een object selecteren in Resource Explorer:</span><span class="sxs-lookup"><span data-stu-id="169c5-134">When you select an object in Resource Explorer:</span></span>

* <span data-ttu-id="169c5-135">Hallo gekoppelde Data Factory-entiteit op Hallo diagramweergave is gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="169c5-135">hello associated Data Factory entity is highlighted in hello Diagram View.</span></span>
* <span data-ttu-id="169c5-136">[Activiteit windows gekoppeld](data-factory-scheduling-and-execution.md) zijn gemarkeerd in de lijst met Hallo activiteit Windows hello onderaan.</span><span class="sxs-lookup"><span data-stu-id="169c5-136">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in hello Activity Windows list at hello bottom.</span></span>  
* <span data-ttu-id="169c5-137">Hallo-eigenschappen van het geselecteerde object Hallo worden weergegeven in het venster Eigenschappen Hallo in het rechterdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="169c5-137">hello properties of hello selected object are shown in hello Properties window in hello right pane.</span></span>
* <span data-ttu-id="169c5-138">Hallo JSON-definitie van het geselecteerde object hello wordt weergegeven, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="169c5-138">hello JSON definition of hello selected object is shown, if applicable.</span></span> <span data-ttu-id="169c5-139">Bijvoorbeeld: een gekoppelde service, een dataset of een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="169c5-139">For example: a linked service, a dataset, or a pipeline.</span></span>

![Resource Explorer](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

<span data-ttu-id="169c5-141">Zie Hallo [planning en uitvoering](data-factory-scheduling-and-execution.md) artikel voor meer conceptuele informatie over windows activiteit.</span><span class="sxs-lookup"><span data-stu-id="169c5-141">See hello [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span></span>

### <a name="diagram-view"></a><span data-ttu-id="169c5-142">Diagramweergave</span><span class="sxs-lookup"><span data-stu-id="169c5-142">Diagram View</span></span>
<span data-ttu-id="169c5-143">Hallo diagramweergave van een data factory biedt één van glas toomonitor en beheren van een gegevensfactory en de activa.</span><span class="sxs-lookup"><span data-stu-id="169c5-143">hello Diagram View of a data factory provides a single pane of glass toomonitor and manage a data factory and its assets.</span></span> <span data-ttu-id="169c5-144">Wanneer u een Data Factory-entiteit (gegevensset/pipeline) in de diagramweergave Hallo selecteert:</span><span class="sxs-lookup"><span data-stu-id="169c5-144">When you select a Data Factory entity (dataset/pipeline) in hello Diagram View:</span></span>

* <span data-ttu-id="169c5-145">Hallo data factory-entiteit wordt geselecteerd in de structuurweergave Hallo.</span><span class="sxs-lookup"><span data-stu-id="169c5-145">hello data factory entity is selected in hello tree view.</span></span>
* <span data-ttu-id="169c5-146">Hallo gekoppelde windows zijn gemarkeerd in de lijst van de activiteit Windows hello activiteit.</span><span class="sxs-lookup"><span data-stu-id="169c5-146">hello associated activity windows are highlighted in hello Activity Windows list.</span></span>
* <span data-ttu-id="169c5-147">Hallo-eigenschappen van het geselecteerde object Hallo worden weergegeven in het venster Eigenschappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="169c5-147">hello properties of hello selected object are shown in hello Properties window.</span></span>

<span data-ttu-id="169c5-148">Wanneer Hallo pijplijn (niet in een onderbroken status) is ingeschakeld, wordt deze met een groene lijn weergegeven:</span><span class="sxs-lookup"><span data-stu-id="169c5-148">When hello pipeline is enabled (not in a paused state), it's shown with a green line:</span></span>

![Pijplijn uitgevoerd](./media/data-factory-monitor-manage-app/PipelineRunning.png)

<span data-ttu-id="169c5-150">U kunt onderbreken, hervatten of een pipeline is beëindigd door te selecteren in de diagramweergave Hallo en Hallo knoppen op de opdrachtbalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="169c5-150">You can pause, resume, or terminate a pipeline by selecting it in hello diagram view and using hello buttons on hello command bar.</span></span>

![Onderbreken/hervatten op de opdrachtbalk Hallo](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
<span data-ttu-id="169c5-152">Er zijn drie opdrachtbalkknoppen voor Hallo pijplijn in Hallo diagramweergave.</span><span class="sxs-lookup"><span data-stu-id="169c5-152">There are three command bar buttons for hello pipeline in hello Diagram View.</span></span> <span data-ttu-id="169c5-153">U kunt Hallo tweede knop toopause Hallo pijplijn gebruiken.</span><span class="sxs-lookup"><span data-stu-id="169c5-153">You can use hello second button toopause hello pipeline.</span></span> <span data-ttu-id="169c5-154">Onderbreken Hallo activiteiten momenteel wordt uitgevoerd niet beëindigen en kan ze doorgaan toocompletion.</span><span class="sxs-lookup"><span data-stu-id="169c5-154">Pausing doesn't terminate hello currently running activities and lets them proceed toocompletion.</span></span> <span data-ttu-id="169c5-155">Hallo derde knop pauzeert Hallo pijplijn en beëindigt de bestaande activiteiten in uitvoering.</span><span class="sxs-lookup"><span data-stu-id="169c5-155">hello third button pauses hello pipeline and terminates its existing executing activities.</span></span> <span data-ttu-id="169c5-156">de eerste knop Hallo hervatten Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="169c5-156">hello first button resumes hello pipeline.</span></span> <span data-ttu-id="169c5-157">Wanneer uw pijplijn wordt onderbroken, verandert de kleur van de Hallo van Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="169c5-157">When your pipeline is paused, hello color of hello pipeline changes.</span></span> <span data-ttu-id="169c5-158">Bijvoorbeeld ziet een onderbroken pijplijn er in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="169c5-158">For example, a paused pipeline looks like in hello following image:</span></span> 

![Pijplijn onderbroken](./media/data-factory-monitor-manage-app/PipelinePaused.png)

<span data-ttu-id="169c5-160">Meervoudige selectie twee of meer pijplijnen kunt u met behulp van Hallo Ctrl-toets.</span><span class="sxs-lookup"><span data-stu-id="169c5-160">You can multi-select two or more pipelines by using hello Ctrl key.</span></span> <span data-ttu-id="169c5-161">U kunt Hallo opdracht balk knoppen toopause/hervatten meerdere pijplijnen tegelijk.</span><span class="sxs-lookup"><span data-stu-id="169c5-161">You can use hello command bar buttons toopause/resume multiple pipelines at a time.</span></span>

<span data-ttu-id="169c5-162">U kunt ook met de rechtermuisknop op een pijplijn en selecteer opties toosuspend, hervatten of een pipeline is beëindigd.</span><span class="sxs-lookup"><span data-stu-id="169c5-162">You can also right-click a pipeline and select options toosuspend, resume, or terminate a pipeline.</span></span> 

![Contextmenu voor de pijplijn](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

<span data-ttu-id="169c5-164">Klik op Hallo **pijplijn openen** toosee alle Hallo activiteiten in de pijplijn Hallo optie.</span><span class="sxs-lookup"><span data-stu-id="169c5-164">Click hello **Open pipeline** option toosee all hello activities in hello pipeline.</span></span> 

![Menu Pijplijn openen](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

<span data-ttu-id="169c5-166">In de weergave van de pijplijn Hallo geopend ziet u alle activiteiten in Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="169c5-166">In hello opened pipeline view, you see all activities in hello pipeline.</span></span> <span data-ttu-id="169c5-167">In dit voorbeeld is er slechts één activiteit: Kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="169c5-167">In this example, there is only one activity: Copy Activity.</span></span> 

![Geopende pijplijn](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

<span data-ttu-id="169c5-169">back-toogo toohello vorige weergave, klikt u op Hallo data factory-naam in Hallo breadcrumb menu Hallo boven.</span><span class="sxs-lookup"><span data-stu-id="169c5-169">toogo back toohello previous view, click hello data factory name in hello breadcrumb menu at hello top.</span></span>

<span data-ttu-id="169c5-170">Pijplijnweergave hello, wanneer u een uitvoergegevensset of wanneer u de muisaanwijzer over uitvoergegevensset hello, selecteert ziet u in Hallo Windows van de activiteit pop-upvenster voor deze gegevensset.</span><span class="sxs-lookup"><span data-stu-id="169c5-170">In hello pipeline view, when you select an output dataset or when you move your mouse over hello output dataset, you see hello Activity Windows pop-up window for that dataset.</span></span>

![Activiteit Windows pop-upvenster](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

<span data-ttu-id="169c5-172">U kunt een activiteit venster toosee details klikken voor het in Hallo **eigenschappen** venster in het rechterdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="169c5-172">You can click an activity window toosee details for it in hello **Properties** window in hello right pane.</span></span>

![Eigenschappen van het venster activiteit](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

<span data-ttu-id="169c5-174">In het rechterdeelvenster Hallo overschakelen toohello **activiteit venster Explorer** toosee tabblad meer informatie.</span><span class="sxs-lookup"><span data-stu-id="169c5-174">In hello right pane, switch toohello **Activity Window Explorer** tab toosee more details.</span></span>

![Activiteit venster Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

<span data-ttu-id="169c5-176">U ziet ook **opgelost variabelen** voor elke poging uitvoeren voor een activiteit in Hallo **pogingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="169c5-176">You also see **resolved variables** for each run attempt for an activity in hello **Attempts** section.</span></span>

![Opgelost variabelen](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

<span data-ttu-id="169c5-178">Overschakelen van toohello **Script** toosee Hallo JSON-script-definitie voor het geselecteerde object Hallo tabblad.</span><span class="sxs-lookup"><span data-stu-id="169c5-178">Switch toohello **Script** tab toosee hello JSON script definition for hello selected object.</span></span>   

![Tabblad script](./media/data-factory-monitor-manage-app/ScriptTab.png)

<span data-ttu-id="169c5-180">Hier ziet u activiteitsvensters op drie locaties:</span><span class="sxs-lookup"><span data-stu-id="169c5-180">You can see activity windows in three places:</span></span>

* <span data-ttu-id="169c5-181">Hallo activiteit Windows pop-upvenster in Hallo diagramweergave (middelste deelvenster).</span><span class="sxs-lookup"><span data-stu-id="169c5-181">hello Activity Windows pop-up in hello Diagram View (middle pane).</span></span>
* <span data-ttu-id="169c5-182">Hallo activiteit venster Explorer in het rechterdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="169c5-182">hello Activity Window Explorer in hello right pane.</span></span>
* <span data-ttu-id="169c5-183">lijst met Hallo activiteit Windows in Hallo onderste deelvenster.</span><span class="sxs-lookup"><span data-stu-id="169c5-183">hello Activity Windows list in hello bottom pane.</span></span>

<span data-ttu-id="169c5-184">U kunt bladeren toohello vorige week in Hallo Windows van de activiteit pop-upvenster en activiteit venster Explorer en Hallo volgende week met behulp van Hallo pijlen naar rechts en.</span><span class="sxs-lookup"><span data-stu-id="169c5-184">In hello Activity Windows pop-up and Activity Window Explorer, you can scroll toohello previous week and hello next week by using hello left and right arrows.</span></span>

![Activiteit Explorer-venster horizontaal pijlen](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

<span data-ttu-id="169c5-186">Aan de onderkant van de Hallo Hallo diagramweergave, ziet u deze knoppen: inzoomen, uitzoomen, zoomen tooFit, zoomen 100%, indeling vergrendelen.</span><span class="sxs-lookup"><span data-stu-id="169c5-186">At hello bottom of hello Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom tooFit, Zoom 100%, Lock layout.</span></span> <span data-ttu-id="169c5-187">Hallo **indeling vergrendelen** knop voorkomt u dat u per ongeluk tabellen en pijplijnen verplaatsen in Hallo diagramweergave.</span><span class="sxs-lookup"><span data-stu-id="169c5-187">hello **Lock layout** button prevents you from accidentally moving tables and pipelines in hello Diagram View.</span></span> <span data-ttu-id="169c5-188">Deze is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="169c5-188">It's on by default.</span></span> <span data-ttu-id="169c5-189">U kunt deze uitschakelen en entiteiten navigeren in Hallo-diagram.</span><span class="sxs-lookup"><span data-stu-id="169c5-189">You can turn it off and move entities around in hello diagram.</span></span> <span data-ttu-id="169c5-190">Wanneer u deze uitschakelen, gebruikt u Hallo laatste knop tooautomatically positie tabellen en pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="169c5-190">When you turn it off, you can use hello last button tooautomatically position tables and pipelines.</span></span> <span data-ttu-id="169c5-191">U kunt ook in- of uitzoomen met Hallo muiswiel.</span><span class="sxs-lookup"><span data-stu-id="169c5-191">You can also zoom in or out by using hello mouse wheel.</span></span>

![Diagram van weergave zoomopdrachten](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a><span data-ttu-id="169c5-193">Lijst met Windows</span><span class="sxs-lookup"><span data-stu-id="169c5-193">Activity Windows list</span></span>
<span data-ttu-id="169c5-194">Hallo Activiteitsvensters lijst onderaan Hallo Hallo middelste deelvenster geeft alle activiteitsvensters voor Hallo gegevensset die u hebt geselecteerd in Hallo Resource Explorer of Hallo diagramweergave.</span><span class="sxs-lookup"><span data-stu-id="169c5-194">hello Activity Windows list at hello bottom of hello middle pane displays all activity windows for hello dataset that you selected in hello Resource Explorer or hello Diagram View.</span></span> <span data-ttu-id="169c5-195">Hallo-lijst is standaard in aflopende volgorde, wat betekent dat u de meest recente activiteitvenster boven Hallo Hallo ziet.</span><span class="sxs-lookup"><span data-stu-id="169c5-195">By default, hello list is in descending order, which means that you see hello latest activity window at hello top.</span></span>

![Lijst met Windows](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

<span data-ttu-id="169c5-197">Deze lijst vernieuwd niet automatisch zodat dit gebruik de knop Hallo vernieuwen op Hallo werkbalk toomanually vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="169c5-197">This list doesn't refresh automatically, so use hello refresh button on hello toolbar toomanually refresh it.</span></span>  

<span data-ttu-id="169c5-198">Activiteit windows kunnen worden gebruikt in een Hallo volgende statussen:</span><span class="sxs-lookup"><span data-stu-id="169c5-198">Activity windows can be in one of hello following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="169c5-199">Status</span><span class="sxs-lookup"><span data-stu-id="169c5-199">Status</span></span></th><th align="left"><span data-ttu-id="169c5-200">Substatus</span><span class="sxs-lookup"><span data-stu-id="169c5-200">Substatus</span></span></th><th align="left"><span data-ttu-id="169c5-201">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="169c5-201">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="169c5-202">Wachten</span><span class="sxs-lookup"><span data-stu-id="169c5-202">Waiting</span></span></td><td><span data-ttu-id="169c5-203">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="169c5-203">ScheduleTime</span></span></td><td><span data-ttu-id="169c5-204">Hallo-tijd is niet geleverd voor Hallo activiteit venster toorun.</span><span class="sxs-lookup"><span data-stu-id="169c5-204">hello time hasn't come for hello activity window toorun.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="169c5-205">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="169c5-205">DatasetDependencies</span></span></td><td><span data-ttu-id="169c5-206">Hallo upstream-afhankelijkheden zijn niet gereed.</span><span class="sxs-lookup"><span data-stu-id="169c5-206">hello upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="169c5-207">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="169c5-207">ComputeResources</span></span></td><td><span data-ttu-id="169c5-208">Hallo rekenresources zijn niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="169c5-208">hello compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="169c5-209">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="169c5-209">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="169c5-210">Alle Hallo-activiteitsinstanties zijn bezig met andere windows activiteit.</span><span class="sxs-lookup"><span data-stu-id="169c5-210">All hello activity instances are busy running other activity windows.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="169c5-211">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="169c5-211">ActivityResume</span></span></td><td><span data-ttu-id="169c5-212">Hallo-activiteit is onderbroken en Hallo activiteit windows kan niet worden uitgevoerd totdat deze hervat.</span><span class="sxs-lookup"><span data-stu-id="169c5-212">hello activity is paused and can't run hello activity windows until it's resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="169c5-213">Probeer het opnieuw</span><span class="sxs-lookup"><span data-stu-id="169c5-213">Retry</span></span></td><td><span data-ttu-id="169c5-214">Er wordt opnieuw geprobeerd Hallo activiteit is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="169c5-214">hello activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="169c5-215">Validatie</span><span class="sxs-lookup"><span data-stu-id="169c5-215">Validation</span></span></td><td><span data-ttu-id="169c5-216">Validatie is nog niet gestart.</span><span class="sxs-lookup"><span data-stu-id="169c5-216">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="169c5-217">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="169c5-217">ValidationRetry</span></span></td><td><span data-ttu-id="169c5-218">Validatie is wachten toobe opnieuw geprobeerd.</span><span class="sxs-lookup"><span data-stu-id="169c5-218">Validation is waiting toobe retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="169c5-219">InProgress</span><span class="sxs-lookup"><span data-stu-id="169c5-219">InProgress</span></span></td><td><span data-ttu-id="169c5-220">Valideren</span><span class="sxs-lookup"><span data-stu-id="169c5-220">Validating</span></span></td><td><span data-ttu-id="169c5-221">Validatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="169c5-221">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="169c5-222">venster van de activiteit Hello wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="169c5-222">hello activity window is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="169c5-223">Is mislukt</span><span class="sxs-lookup"><span data-stu-id="169c5-223">Failed</span></span></td><td><span data-ttu-id="169c5-224">Time-out</span><span class="sxs-lookup"><span data-stu-id="169c5-224">TimedOut</span></span></td><td><span data-ttu-id="169c5-225">Hallo activiteit uitvoeren duurde langer dan is toegestaan door Hallo-activiteit.</span><span class="sxs-lookup"><span data-stu-id="169c5-225">hello activity execution took longer than what is allowed by hello activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="169c5-226">Geannuleerd</span><span class="sxs-lookup"><span data-stu-id="169c5-226">Canceled</span></span></td><td><span data-ttu-id="169c5-227">venster van de activiteit Hallo is geannuleerd door in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="169c5-227">hello activity window was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="169c5-228">Validatie</span><span class="sxs-lookup"><span data-stu-id="169c5-228">Validation</span></span></td><td><span data-ttu-id="169c5-229">Validatie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="169c5-229">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="169c5-230">venster van de activiteit Hallo mislukt toobe gegenereerd of gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="169c5-230">hello activity window failed toobe generated or validated.</span></span></td>
</tr>
<td><span data-ttu-id="169c5-231">Gereed</span><span class="sxs-lookup"><span data-stu-id="169c5-231">Ready</span></span></td><td>-</td><td><span data-ttu-id="169c5-232">venster van de activiteit Hallo is gereed voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="169c5-232">hello activity window is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="169c5-233">Overgeslagen</span><span class="sxs-lookup"><span data-stu-id="169c5-233">Skipped</span></span></td><td>-</td><td><span data-ttu-id="169c5-234">venster Hallo-activiteit is niet verwerkt.</span><span class="sxs-lookup"><span data-stu-id="169c5-234">hello activity window wasn't processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="169c5-235">Geen</span><span class="sxs-lookup"><span data-stu-id="169c5-235">None</span></span></td><td>-</td><td><span data-ttu-id="169c5-236">Het venster van een activiteit tooexist gebruikt met een andere status, maar is opnieuw ingesteld.</span><span class="sxs-lookup"><span data-stu-id="169c5-236">An activity window used tooexist with a different status, but has been reset.</span></span></td>
</tr>
</table>


<span data-ttu-id="169c5-237">Wanneer u klikt op een venster van de activiteit in de lijst hello, ziet u meer informatie over het in Hallo **activiteit Windows Verkenner** of Hallo **eigenschappen** -venster op de juiste Hallo.</span><span class="sxs-lookup"><span data-stu-id="169c5-237">When you click an activity window in hello list, you see details about it in hello **Activity Windows Explorer** or hello **Properties** window on hello right.</span></span>

![Activiteit venster Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a><span data-ttu-id="169c5-239">Activiteit windows vernieuwen</span><span class="sxs-lookup"><span data-stu-id="169c5-239">Refresh activity windows</span></span>
<span data-ttu-id="169c5-240">Hallo details worden niet automatisch vernieuwd, dus Hallo de knop Vernieuwen (Hallo tweede knop) op de opdrachtbalk lijst met toomanually vernieuwen Hallo activiteit windows hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="169c5-240">hello details aren't automatically refreshed, so use hello refresh button (hello second button) on hello command bar toomanually refresh hello activity windows list.</span></span>  

### <a name="properties-window"></a><span data-ttu-id="169c5-241">Eigenschappenvenster</span><span class="sxs-lookup"><span data-stu-id="169c5-241">Properties window</span></span>
<span data-ttu-id="169c5-242">het venster Eigenschappen Hello wordt Hallo meest rechtse deelvenster van Hallo-app voor bewaking en beheer.</span><span class="sxs-lookup"><span data-stu-id="169c5-242">hello Properties window is in hello right-most pane of hello Monitoring and Management app.</span></span>

![Eigenschappenvenster](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

<span data-ttu-id="169c5-244">Eigenschappen voor Hallo-item dat u hebt geselecteerd in Hallo Resource Explorer (structuurweergave), wordt de diagramweergave of activiteit Windows-lijst.</span><span class="sxs-lookup"><span data-stu-id="169c5-244">It displays properties for hello item that you selected in hello Resource Explorer (tree view), Diagram View, or Activity Windows list.</span></span>

### <a name="activity-window-explorer"></a><span data-ttu-id="169c5-245">Activiteit venster Explorer</span><span class="sxs-lookup"><span data-stu-id="169c5-245">Activity Window Explorer</span></span>
<span data-ttu-id="169c5-246">Hallo **activiteit venster Explorer** venster is in Hallo meest rechtse deelvenster van Hallo-app voor bewaking en beheer.</span><span class="sxs-lookup"><span data-stu-id="169c5-246">hello **Activity Window Explorer** window is in hello right-most pane of hello Monitoring and Management app.</span></span> <span data-ttu-id="169c5-247">Meer informatie over het venster van de Hallo-activiteit die u hebt geselecteerd in Hallo Windows van de activiteit pop-upvenster of lijst van de activiteit Windows hello wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="169c5-247">It displays details about hello activity window that you selected in hello Activity Windows pop-up window or hello Activity Windows list.</span></span>

![Activiteit venster Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

<span data-ttu-id="169c5-249">U kunt venster van de activiteit tooanother schakelen door erop te klikken in de weergave van de kalender Hallo Hallo boven.</span><span class="sxs-lookup"><span data-stu-id="169c5-249">You can switch tooanother activity window by clicking it in hello calendar view at hello top.</span></span> <span data-ttu-id="169c5-250">U kunt ook gebruik Hallo pijl-links/rechts pijltjesknoppen op Hallo bovenste toosee activiteit windows hello vorige week of Hallo volgende week.</span><span class="sxs-lookup"><span data-stu-id="169c5-250">You can also use hello left arrow/right arrow buttons at hello top toosee activity windows from hello previous week or hello next week.</span></span>

<span data-ttu-id="169c5-251">U kunt werkbalkknoppen hello gebruiken in Hallo onderste deelvenster toorerun Hallo activiteitvenster of Hallo details in het deelvenster Hallo vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="169c5-251">You can use hello toolbar buttons in hello bottom pane toorerun hello activity window or refresh hello details in hello pane.</span></span>

### <a name="script"></a><span data-ttu-id="169c5-252">Script</span><span class="sxs-lookup"><span data-stu-id="169c5-252">Script</span></span>
<span data-ttu-id="169c5-253">U kunt Hallo **Script** tabblad tooview Hallo JSON-definitie Hallo Data Factory-entiteit (gekoppelde service, gegevensset of pijplijn) geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="169c5-253">You can use hello **Script** tab tooview hello JSON definition of hello selected Data Factory entity (linked service, dataset, or pipeline).</span></span>

![Tabblad script](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a><span data-ttu-id="169c5-255">Systeemweergaven gebruiken</span><span class="sxs-lookup"><span data-stu-id="169c5-255">Use system views</span></span>
<span data-ttu-id="169c5-256">Hallo bewaking en beheer-app bevat vooraf samengestelde systeemweergaven (**recente activiteit windows**, **activiteitsvensters is mislukt**, **windows activiteit In uitvoering**) die kunt u tooview recente/mislukt/in uitvoering activiteitsvensters van uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="169c5-256">hello Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you tooview recent/failed/in-progress activity windows for your data factory.</span></span>

<span data-ttu-id="169c5-257">Overschakelen van toohello **weergaven** tabblad aan de linkerkant Hallo door erop te klikken.</span><span class="sxs-lookup"><span data-stu-id="169c5-257">Switch toohello **Monitoring Views** tab on hello left by clicking it.</span></span>

![Weergaven tabblad bewaking](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

<span data-ttu-id="169c5-259">Er zijn momenteel drie systeemweergaven die worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="169c5-259">Currently, there are three system views that are supported.</span></span> <span data-ttu-id="169c5-260">Selecteer een optie toosee recente activiteit windows, windows mislukte activiteit of activiteit in uitvoering windows in de lijst met activiteit Windows hello (onderaan Hallo Hallo middelste deelvenster).</span><span class="sxs-lookup"><span data-stu-id="169c5-260">Select an option toosee recent activity windows, failed activity windows, or in-progress activity windows in hello Activity Windows list (at hello bottom of hello middle pane).</span></span>

<span data-ttu-id="169c5-261">Wanneer u selecteert Hallo **recente activiteit windows** optie, ziet u alle recente activiteit windows in aflopende volgorde Hallo **tijd laatste poging**.</span><span class="sxs-lookup"><span data-stu-id="169c5-261">When you select hello **Recent activity windows** option, you see all recent activity windows in descending order of hello **last attempt time**.</span></span>

<span data-ttu-id="169c5-262">U kunt Hallo **activiteitsvensters is mislukt** activiteitsvensters toosee is mislukt in Hallo lijst bekijken.</span><span class="sxs-lookup"><span data-stu-id="169c5-262">You can use hello **Failed activity windows** view toosee all failed activity windows in hello list.</span></span> <span data-ttu-id="169c5-263">Selecteer een mislukte activiteit-venster in Hallo toosee details weergeven over het in Hallo **eigenschappen** venster of Hallo **activiteit venster Explorer**.</span><span class="sxs-lookup"><span data-stu-id="169c5-263">Select a failed activity window in hello list toosee details about it in hello **Properties** window or hello **Activity Window Explorer**.</span></span> <span data-ttu-id="169c5-264">U kunt ook alle logboeken voor een mislukte activiteitvenster downloaden.</span><span class="sxs-lookup"><span data-stu-id="169c5-264">You can also download any logs for a failed activity window.</span></span>

## <a name="sort-and-filter-activity-windows"></a><span data-ttu-id="169c5-265">Activiteitsvensters sorteren en filteren</span><span class="sxs-lookup"><span data-stu-id="169c5-265">Sort and filter activity windows</span></span>
<span data-ttu-id="169c5-266">Wijziging Hallo **begintijd** en **eindtijd** instellingen in de opdrachtbalk toofilter activiteit windows hello.</span><span class="sxs-lookup"><span data-stu-id="169c5-266">Change hello **start time** and **end time** settings in hello command bar toofilter activity windows.</span></span> <span data-ttu-id="169c5-267">Nadat u Hallo begintijd en eindtijd wijzigt, klikt u op Hallo knop volgende toohello end toorefresh hello Activiteitsvensters lijst time.</span><span class="sxs-lookup"><span data-stu-id="169c5-267">After you change hello start time and end time, click hello button next toohello end time toorefresh hello Activity Windows list.</span></span>

![Begin- en eindtijden](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> <span data-ttu-id="169c5-269">Alle tijden zijn momenteel in UTC-notatie in Hallo-app voor bewaking en beheer.</span><span class="sxs-lookup"><span data-stu-id="169c5-269">Currently, all times are in UTC format in hello Monitoring and Management app.</span></span>
>
>

<span data-ttu-id="169c5-270">In Hallo **Activiteitsvensters lijst**, klikt u op Hallo-naam van een kolom (bijvoorbeeld: Status).</span><span class="sxs-lookup"><span data-stu-id="169c5-270">In hello **Activity Windows list**, click hello name of a column (for example: Status).</span></span>

![Menu kolom activiteit Windows-lijst](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

<span data-ttu-id="169c5-272">U kunt doen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="169c5-272">You can do hello following:</span></span>

* <span data-ttu-id="169c5-273">Sorteren in oplopende volgorde.</span><span class="sxs-lookup"><span data-stu-id="169c5-273">Sort in ascending order.</span></span>
* <span data-ttu-id="169c5-274">Sorteren in aflopende volgorde.</span><span class="sxs-lookup"><span data-stu-id="169c5-274">Sort in descending order.</span></span>
* <span data-ttu-id="169c5-275">Filteren op een of meer waarden (Ready, Waiting, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="169c5-275">Filter by one or more values (Ready, Waiting, and so on).</span></span>

<span data-ttu-id="169c5-276">Wanneer u een filter voor een kolom opgeven, ziet u de knop filteren Hallo voor die kolom, waarmee wordt aangegeven dat de Hallo-waarden in kolom Hallo gefilterde waarden zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="169c5-276">When you specify a filter on a column, you see hello filter button enabled for that column, which indicates that hello values in hello column are filtered values.</span></span>

![Filteren op een kolom van een lijst van de activiteit Windows hello](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

<span data-ttu-id="169c5-278">U kunt dezelfde pop-upvenster tooclear filters Hallo.</span><span class="sxs-lookup"><span data-stu-id="169c5-278">You can use hello same pop-up window tooclear filters.</span></span> <span data-ttu-id="169c5-279">tooclear alle filters voor lijst van de activiteit Windows hello, klik op Hallo filter wissen op de opdrachtbalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="169c5-279">tooclear all filters for hello Activity Windows list, click hello clear filter button on hello command bar.</span></span>

![Alle filters voor een lijst van de activiteit Windows hello wissen](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a><span data-ttu-id="169c5-281">Batch-acties uitvoeren</span><span class="sxs-lookup"><span data-stu-id="169c5-281">Perform batch actions</span></span>
### <a name="rerun-selected-activity-windows"></a><span data-ttu-id="169c5-282">Geselecteerde activiteit windows opnieuw uitvoeren</span><span class="sxs-lookup"><span data-stu-id="169c5-282">Rerun selected activity windows</span></span>
<span data-ttu-id="169c5-283">Selecteer een activiteitvenster, klikt u op Hallo pijl-omlaag voor Hallo eerste knop en selecteer **opnieuw uitvoeren** / **opnieuw uitvoeren met upstream in pijplijn**.</span><span class="sxs-lookup"><span data-stu-id="169c5-283">Select an activity window, click hello down arrow for hello first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span></span> <span data-ttu-id="169c5-284">Wanneer u Hallo selecteert **opnieuw uitvoeren met upstream in pijplijn** optie, evenals alle upstream-activiteit-vensters opnieuw worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="169c5-284">When you select hello **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span></span>
    <span data-ttu-id="169c5-285">![Voer een venster van de activiteit](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span><span class="sxs-lookup"><span data-stu-id="169c5-285">![Rerun an activity window](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span></span>

<span data-ttu-id="169c5-286">Kunt u ook meerdere activiteitsvensters selecteren in lijst Hallo en ze opnieuw uitvoeren op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="169c5-286">You can also select multiple activity windows in hello list and rerun them at hello same time.</span></span> <span data-ttu-id="169c5-287">Kunt u toofilter activiteitsvensters op basis van status hello (bijvoorbeeld: **mislukt**)-- en voert u na het corrigeren van Hallo probleem waardoor Hallo activiteit windows toofail activiteitsvensters Hallo is mislukt.</span><span class="sxs-lookup"><span data-stu-id="169c5-287">You might want toofilter activity windows based on hello status (for example: **Failed**)--and then rerun hello failed activity windows after correcting hello issue that causes hello activity windows toofail.</span></span> <span data-ttu-id="169c5-288">Zie de volgende sectie voor meer informatie over het filteren van activiteit windows in de lijst Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="169c5-288">See hello following section for details about filtering activity windows in hello list.</span></span>  

### <a name="pauseresume-multiple-pipelines"></a><span data-ttu-id="169c5-289">Meerdere pijplijnen onderbreken/hervatten</span><span class="sxs-lookup"><span data-stu-id="169c5-289">Pause/resume multiple pipelines</span></span>
<span data-ttu-id="169c5-290">U kunt multiselect twee of meer pijplijnen met Hallo Ctrl-toets.</span><span class="sxs-lookup"><span data-stu-id="169c5-290">You can multiselect two or more pipelines by using hello Ctrl key.</span></span> <span data-ttu-id="169c5-291">U kunt Hallo opdrachtbalkknoppen (die zijn gemarkeerd in rood Hallo rechthoek op Hallo volgende afbeelding) toopause/hervatten ze.</span><span class="sxs-lookup"><span data-stu-id="169c5-291">You can use hello command bar buttons (which are highlighted in hello red rectangle in hello following image) toopause/resume them.</span></span>

![Onderbreken/hervatten op de opdrachtbalk Hallo](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a><span data-ttu-id="169c5-293">Waarschuwingen maken</span><span class="sxs-lookup"><span data-stu-id="169c5-293">Create alerts</span></span>
<span data-ttu-id="169c5-294">Hallo **waarschuwingen** pagina kunt u bij het maken van een waarschuwing en de bestaande waarschuwingen weergeven/bewerken/verwijderen.</span><span class="sxs-lookup"><span data-stu-id="169c5-294">hello **Alerts** page lets you create an alert and view/edit/delete existing alerts.</span></span> <span data-ttu-id="169c5-295">U kunt ook inschakelen/uitschakelen een waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="169c5-295">You can also disable/enable an alert.</span></span> <span data-ttu-id="169c5-296">toosee Hallo pagina waarschuwingen, klikt u op Hallo **waarschuwingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="169c5-296">toosee hello Alerts page, click hello **Alerts** tab.</span></span>

![Tabblad waarschuwingen](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="toocreate-an-alert"></a><span data-ttu-id="169c5-298">toocreate een waarschuwing</span><span class="sxs-lookup"><span data-stu-id="169c5-298">toocreate an alert</span></span>
1. <span data-ttu-id="169c5-299">Klik op **waarschuwing toevoegen** tooadd een waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="169c5-299">Click **Add Alert** tooadd an alert.</span></span> <span data-ttu-id="169c5-300">U ziet Hallo **Details** pagina.</span><span class="sxs-lookup"><span data-stu-id="169c5-300">You see hello **Details** page.</span></span>

    ![Waarschuwingen - pagina met Details maken](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. <span data-ttu-id="169c5-302">Geef Hallo **naam** en **beschrijving** voor Hallo waarschuwing en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="169c5-302">Specify hello **Name** and **Description** for hello alert, and click **Next**.</span></span> <span data-ttu-id="169c5-303">U ziet Hallo **Filters** pagina.</span><span class="sxs-lookup"><span data-stu-id="169c5-303">You should see hello **Filters** page.</span></span>

    ![Waarschuwingen - pagina Filters maken](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. <span data-ttu-id="169c5-305">Selecteer Hallo **gebeurtenis**, **status**, en **substatus** (optioneel) dat u wilt dat toocreate Data Factory-service voor een waarschuwing en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="169c5-305">Select hello **event**, **status**, and **substatus** (optional) that you want toocreate a Data Factory service alert for, and click **Next**.</span></span> <span data-ttu-id="169c5-306">U ziet Hallo **ontvangers** pagina.</span><span class="sxs-lookup"><span data-stu-id="169c5-306">You should see hello **Recipients** page.</span></span>

    ![Waarschuwingen - ontvangers pagina maken](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. <span data-ttu-id="169c5-308">Selecteer Hallo **e-abonnementsbeheerders** optie en/of geef een **extra beheerders-e**, en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="169c5-308">Select hello **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**.</span></span> <span data-ttu-id="169c5-309">U ziet de waarschuwing in de lijst Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="169c5-309">You should see hello alert in hello list.</span></span>

    ![Lijst met waarschuwingen](./media/data-factory-monitor-manage-app/AlertsList.png)

<span data-ttu-id="169c5-311">Gebruik de knoppen met de Hallo die gekoppeld aan Hallo waarschuwing tooedit/delete/inschakelen/uitschakelen een waarschuwing zijn in de lijst met Hallo-meldingen.</span><span class="sxs-lookup"><span data-stu-id="169c5-311">In hello Alerts list, use hello buttons that are associated with hello alert tooedit/delete/disable/enable an alert.</span></span>

### <a name="eventstatussubstatus"></a><span data-ttu-id="169c5-312">Status-gebeurtenis/substatus</span><span class="sxs-lookup"><span data-stu-id="169c5-312">Event/status/substatus</span></span>
<span data-ttu-id="169c5-313">Hallo bevat volgende tabel Hallo lijst met beschikbare gebeurtenissen en status (en substatus).</span><span class="sxs-lookup"><span data-stu-id="169c5-313">hello following table provides hello list of available events and statuses (and substatuses).</span></span>

| <span data-ttu-id="169c5-314">De naam van gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="169c5-314">Event name</span></span> | <span data-ttu-id="169c5-315">Status</span><span class="sxs-lookup"><span data-stu-id="169c5-315">Status</span></span> | <span data-ttu-id="169c5-316">Substatus</span><span class="sxs-lookup"><span data-stu-id="169c5-316">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="169c5-317">Activiteit die wordt uitgevoerd gestart</span><span class="sxs-lookup"><span data-stu-id="169c5-317">Activity Run Started</span></span> |<span data-ttu-id="169c5-318">Gestart</span><span class="sxs-lookup"><span data-stu-id="169c5-318">Started</span></span> |<span data-ttu-id="169c5-319">Starting</span><span class="sxs-lookup"><span data-stu-id="169c5-319">Starting</span></span> |
| <span data-ttu-id="169c5-320">Activiteit die wordt uitgevoerd is voltooid</span><span class="sxs-lookup"><span data-stu-id="169c5-320">Activity Run Finished</span></span> |<span data-ttu-id="169c5-321">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="169c5-321">Succeeded</span></span> |<span data-ttu-id="169c5-322">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="169c5-322">Succeeded</span></span> |
| <span data-ttu-id="169c5-323">Activiteit die wordt uitgevoerd is voltooid</span><span class="sxs-lookup"><span data-stu-id="169c5-323">Activity Run Finished</span></span> |<span data-ttu-id="169c5-324">Is mislukt</span><span class="sxs-lookup"><span data-stu-id="169c5-324">Failed</span></span> |<span data-ttu-id="169c5-325">Fout in de Resource-toewijzing</span><span class="sxs-lookup"><span data-stu-id="169c5-325">Failed Resource Allocation</span></span><br/><br/><span data-ttu-id="169c5-326">Mislukte uitvoering</span><span class="sxs-lookup"><span data-stu-id="169c5-326">Failed Execution</span></span><br/><br/><span data-ttu-id="169c5-327">Time-out</span><span class="sxs-lookup"><span data-stu-id="169c5-327">Timed Out</span></span><br/><br/><span data-ttu-id="169c5-328">De validatie is mislukt</span><span class="sxs-lookup"><span data-stu-id="169c5-328">Failed Validation</span></span><br/><br/><span data-ttu-id="169c5-329">Afgebroken</span><span class="sxs-lookup"><span data-stu-id="169c5-329">Abandoned</span></span> |
| <span data-ttu-id="169c5-330">On-Demand HDI-Cluster maken gestart</span><span class="sxs-lookup"><span data-stu-id="169c5-330">On-Demand HDI Cluster Create Started</span></span> |<span data-ttu-id="169c5-331">Gestart</span><span class="sxs-lookup"><span data-stu-id="169c5-331">Started</span></span> |-|
| <span data-ttu-id="169c5-332">On-Demand HDI-Cluster is gemaakt</span><span class="sxs-lookup"><span data-stu-id="169c5-332">On-Demand HDI Cluster Created Successfully</span></span> |<span data-ttu-id="169c5-333">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="169c5-333">Succeeded</span></span> |-|
| <span data-ttu-id="169c5-334">On-Demand-HDI-Cluster is verwijderd</span><span class="sxs-lookup"><span data-stu-id="169c5-334">On-Demand HDI Cluster Deleted</span></span> |<span data-ttu-id="169c5-335">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="169c5-335">Succeeded</span></span> |-|

### <a name="tooedit-delete-or-disable-an-alert"></a><span data-ttu-id="169c5-336">tooedit, verwijderen of uitschakelen van een waarschuwing</span><span class="sxs-lookup"><span data-stu-id="169c5-336">tooedit, delete, or disable an alert</span></span>

<span data-ttu-id="169c5-337">Gebruik hello tooedit knoppen (rood gemarkeerd), verwijderen of uitschakelen van een waarschuwing te volgen.</span><span class="sxs-lookup"><span data-stu-id="169c5-337">Use hello following buttons (highlighted in red) tooedit, delete, or disable an alert.</span></span>

![Waarschuwingen knoppen](./media/data-factory-monitor-manage-app/AlertButtons.png)
