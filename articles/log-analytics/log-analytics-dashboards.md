---
title: een aangepast dashboard in Azure-logboekanalyse aaaCreate | Microsoft Docs
description: "Deze handleiding helpt u begrijpen hoe logboekanalyse dashboards Visualiseer al uw zoekopdrachten opgeslagen logboek, zodat u één lens tooview uw omgeving."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 73fcf131a91c743d473f37d5a40d52eaf78a7ba3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a><span data-ttu-id="46831-103">Maken van een aangepast dashboard voor gebruik in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="46831-103">Create a custom dashboard for use in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="46831-104">Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), en u geen nieuwe dashboards maken of bewerken van bestaande dashboards.</span><span class="sxs-lookup"><span data-stu-id="46831-104">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you cannot create new dashboards or edit existing dashboards.</span></span> 

<span data-ttu-id="46831-105">Deze handleiding helpt u begrijpen hoe logboekanalyse dashboards Visualiseer al uw zoekopdrachten opgeslagen logboek, zodat u één lens tooview uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="46831-105">This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens tooview your environment.</span></span>

![Voorbeeld van Dashboard](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

<span data-ttu-id="46831-107">Alle Hallo aangepaste dashboards die u in Hallo OMS-portal maakt zijn ook beschikbaar in Hallo OMS mobiele App.</span><span class="sxs-lookup"><span data-stu-id="46831-107">All hello custom dashboards that you create in hello OMS portal are also available in hello OMS Mobile App.</span></span> <span data-ttu-id="46831-108">Zie de volgende pagina's voor meer informatie over apps Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="46831-108">See hello following pages for more information about hello apps.</span></span>

* [<span data-ttu-id="46831-109">Mobiele app van Microsoft Store Hallo OMS</span><span class="sxs-lookup"><span data-stu-id="46831-109">OMS mobile app from hello Microsoft Store</span></span>](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [<span data-ttu-id="46831-110">Mobiele app van Apple iTunes OMS</span><span class="sxs-lookup"><span data-stu-id="46831-110">OMS mobile app from Apple iTunes</span></span>](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![mobiele dashboard](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a><span data-ttu-id="46831-112">Hoe maak ik mijn dashboard</span><span class="sxs-lookup"><span data-stu-id="46831-112">How do I create my dashboard?</span></span>
<span data-ttu-id="46831-113">toobegin, Ga toohello OMS-overzichtspagina.</span><span class="sxs-lookup"><span data-stu-id="46831-113">toobegin, go toohello OMS Overview page.</span></span> <span data-ttu-id="46831-114">Ziet u Hallo **mijn Dashboard** tegel op Hallo links.</span><span class="sxs-lookup"><span data-stu-id="46831-114">You'll see hello **My Dashboard** tile on hello left.</span></span> <span data-ttu-id="46831-115">Klik op het toodrill omlaag in uw dashboard.</span><span class="sxs-lookup"><span data-stu-id="46831-115">Click it toodrill down into your dashboard.</span></span>

![Overzicht](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a><span data-ttu-id="46831-117">Toevoegen van een tegel</span><span class="sxs-lookup"><span data-stu-id="46831-117">Adding a tile</span></span>
<span data-ttu-id="46831-118">Dashboards, worden de tegels aangedreven door uw zoekopdrachten opgeslagen logboek.</span><span class="sxs-lookup"><span data-stu-id="46831-118">In dashboards, tiles are powered by your saved log searches.</span></span> <span data-ttu-id="46831-119">OMS wordt geleverd met veel en-klare opgeslagen logboek zoekopdrachten, zodat u meteen kunt beginnen.</span><span class="sxs-lookup"><span data-stu-id="46831-119">OMS comes with many pre-made saved log searches, so you can begin right away.</span></span> <span data-ttu-id="46831-120">Gebruik Hallo volgende stappen overzicht hoe toobegin.</span><span class="sxs-lookup"><span data-stu-id="46831-120">Use hello following steps that outline how toobegin.</span></span>

<span data-ttu-id="46831-121">In deze dashboardweergave Hallo, klikt u op **aanpassen** tooenter modus aanpassen.</span><span class="sxs-lookup"><span data-stu-id="46831-121">In hello My Dashboard view, simply click **Customize** tooenter customize mode.</span></span>

![Afbeeldingen](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 <span data-ttu-id="46831-123">Hallo-Configuratiescherm dat wordt geopend aan de rechterkant Hallo van Hallo pagina geeft alle uw werkruimte opgeslagen logboek zoekopdrachten.</span><span class="sxs-lookup"><span data-stu-id="46831-123">hello panel that opens on hello right side of hello page shows all of your workspace's saved log searches.</span></span> <span data-ttu-id="46831-124">een opgeslagen logboek zoeken als een tegel toovisualize Beweeg de muisaanwijzer over een opgeslagen zoekopdracht en klik vervolgens op Hallo **plus** symbool.</span><span class="sxs-lookup"><span data-stu-id="46831-124">toovisualize a saved log search as a tile,  hover over a saved search and then click hello **plus** symbol.</span></span>

![1 tegels toevoegen](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

<span data-ttu-id="46831-126">Wanneer u klikt op Hallo **plus** een symbool, een nieuwe tegel wordt weergegeven in Hallo mijn dashboardweergave.</span><span class="sxs-lookup"><span data-stu-id="46831-126">When you click hello **plus** symbol, a new tile appears in hello My Dashboard view.</span></span>

![2 tegels toevoegen](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a><span data-ttu-id="46831-128">Een tegel bewerken</span><span class="sxs-lookup"><span data-stu-id="46831-128">Edit a tile</span></span>
<span data-ttu-id="46831-129">In deze dashboardweergave Hallo, klikt u op **aanpassen** tooenter modus aanpassen.</span><span class="sxs-lookup"><span data-stu-id="46831-129">In hello My Dashboard view, simply click  **Customize** tooenter customize mode.</span></span> <span data-ttu-id="46831-130">Klik op de gewenste tooedit tegel Hallo.</span><span class="sxs-lookup"><span data-stu-id="46831-130">Click hello tile you want tooedit.</span></span> <span data-ttu-id="46831-131">Hallo rechterpaneel tooedit wijzigingen, en biedt een aantal opties:</span><span class="sxs-lookup"><span data-stu-id="46831-131">hello right panel changes tooedit, and gives a selection of options:</span></span>

![Tegel bewerken](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Tegel bewerken](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a><span data-ttu-id="46831-134">Tegel visualisaties</span><span class="sxs-lookup"><span data-stu-id="46831-134">Tile visualizations</span></span>
<span data-ttu-id="46831-135">Er zijn drie soorten tegel visualisaties toochoose uit:</span><span class="sxs-lookup"><span data-stu-id="46831-135">There are three kinds of tile visualizations toochoose from:</span></span>

| <span data-ttu-id="46831-136">grafiektype</span><span class="sxs-lookup"><span data-stu-id="46831-136">chart type</span></span> | <span data-ttu-id="46831-137">wat het programma doet</span><span class="sxs-lookup"><span data-stu-id="46831-137">what it does</span></span> |
| --- | --- |
| ![Staafdiagram](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |<span data-ttu-id="46831-139">Geeft een tijdlijn met uw opgeslagen logboek zoekresultaten weer als een staafdiagram of een lijst met resultaten in een veld afhankelijk van als uw zoekopdracht logboek resultaten door een veld of niet aggregeert.</span><span class="sxs-lookup"><span data-stu-id="46831-139">Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not.</span></span> |
| ![Metrische gegevens](./media/log-analytics-dashboards/oms-dashboards-metric.png) |<span data-ttu-id="46831-141">Worden uw totale logboek zoeken resultaat treffers weergegeven als een getal in een tegel.</span><span class="sxs-lookup"><span data-stu-id="46831-141">Displays your total log search result hits as a number in a tile.</span></span> <span data-ttu-id="46831-142">Metrische tegels kunnen u tooset een drempel die Hallo-tegel wordt gemarkeerd als Hallo drempelwaarde is bereikt.</span><span class="sxs-lookup"><span data-stu-id="46831-142">Metric tiles allow you tooset a threshold that will highlight hello tile when hello threshold is reached.</span></span> |
| ![regel](./media/log-analytics-dashboards/oms-dashboards-line.png) |<span data-ttu-id="46831-144">Hiermee geeft u een tijdlijn van uw opgeslagen logboek resultaat gevonden in de zoekopdracht met waarden weer als een lijndiagram.</span><span class="sxs-lookup"><span data-stu-id="46831-144">Displays a timeline of your saved log search result hits with values as a line chart.</span></span> |

### <a name="threshold"></a><span data-ttu-id="46831-145">Drempelwaarde</span><span class="sxs-lookup"><span data-stu-id="46831-145">Threshold</span></span>
<span data-ttu-id="46831-146">U kunt een drempelwaarde maken op een tegel Hallo metrische visualisatie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="46831-146">You can create a threshold on a tile using hello Metric visualization.</span></span> <span data-ttu-id="46831-147">Selecteer op de toocreate een drempelwaarde op Hallo tegel.</span><span class="sxs-lookup"><span data-stu-id="46831-147">Select on toocreate a threshold value on hello tile.</span></span> <span data-ttu-id="46831-148">Kies of toohighlight Hallo tegel wanneer Hallo waarde boven of onder de drempelwaarde voor Hallo gekozen, stel Hallo drempelwaarde hieronder.</span><span class="sxs-lookup"><span data-stu-id="46831-148">Choose whether toohighlight hello tile when hello value is over or under hello chosen threshold, then set hello threshold value below.</span></span>

## <a name="organizing-hello-dashboard"></a><span data-ttu-id="46831-149">Hallo dashboard ordenen</span><span class="sxs-lookup"><span data-stu-id="46831-149">Organizing hello dashboard</span></span>
<span data-ttu-id="46831-150">tooorganize uw dashboard toohello mijn dashboardweergave te navigeren en klik op **aanpassen** tooenter modus aanpassen.</span><span class="sxs-lookup"><span data-stu-id="46831-150">tooorganize your dashboard, navigate toohello My Dashboard view and click **Customize** tooenter customize mode.</span></span> <span data-ttu-id="46831-151">Klik en sleep Hallo tegel u toomove wilt en u wilt dat uw tegel toobe toowhere verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="46831-151">Click and drag hello tile you want toomove, and move it toowhere you want your tile toobe.</span></span>

![Uw Dashboard ordenen](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a><span data-ttu-id="46831-153">Een tegel verwijderen</span><span class="sxs-lookup"><span data-stu-id="46831-153">Remove a tile</span></span>
<span data-ttu-id="46831-154">een tegel tooremove toohello mijn dashboardweergave te navigeren en klik op **aanpassen** tooenter modus aanpassen.</span><span class="sxs-lookup"><span data-stu-id="46831-154">tooremove a tile, navigate toohello My Dashboard view and click **Customize** tooenter customize mode.</span></span> <span data-ttu-id="46831-155">Selecteer Hallo tegel u wilt tooremove en selecteer in het rechterdeelvenster Hallo **verwijderen tegel**.</span><span class="sxs-lookup"><span data-stu-id="46831-155">Select hello tile you want tooremove, then on hello right panel select **Remove Tile**.</span></span>

![Een tegel verwijderen](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a><span data-ttu-id="46831-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="46831-157">Next steps</span></span>
* <span data-ttu-id="46831-158">Maak [waarschuwingen](log-analytics-alerts.md) in tooremediate problemen en Log Analytics toogenerate meldingen.</span><span class="sxs-lookup"><span data-stu-id="46831-158">Create [alerts](log-analytics-alerts.md) in Log Analytics toogenerate notifications and tooremediate problems.</span></span>
