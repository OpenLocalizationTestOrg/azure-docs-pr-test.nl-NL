---
title: Microsoft Power BI Embedded - verbinding te maken met een gegevensbron
description: Power BI Embedded, verbinding maken met gegevensbronnen
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 9f614bbc63eae788aa52132c8f0e42ad8963559a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-a-data-source"></a><span data-ttu-id="d0ac6-103">Verbinding maken met een gegevensbron</span><span class="sxs-lookup"><span data-stu-id="d0ac6-103">Connect to a data source</span></span>
<span data-ttu-id="d0ac6-104">Met **Power BI Embedded**, kunt u rapporten insluiten in uw eigen app.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-104">With **Power BI Embedded**, you can embed reports into your own app.</span></span> <span data-ttu-id="d0ac6-105">Wanneer u een Power BI-rapport in uw app insluiten, het rapport maakt verbinding met de onderliggende gegevens door **importeren** een kopie van de gegevens of door **rechtstreeks verbinding maken** naar de gegevensbron via **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-105">When you embed a Power BI report into your app, the report connects to the underlying data by **importing** a copy of the data or by **connecting directly** to the data source using **DirectQuery**.</span></span>

<span data-ttu-id="d0ac6-106">Dit zijn de verschillen tussen **Importeren** en **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-106">Here are the differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="d0ac6-107">Importeren</span><span class="sxs-lookup"><span data-stu-id="d0ac6-107">Import</span></span> | <span data-ttu-id="d0ac6-108">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="d0ac6-108">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="d0ac6-109">Tabellen, kolommen *en gegevens* zijn geïmporteerd of gekopieerd naar het rapport gegevensset.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-109">Tables, columns, *and data* are imported or copied into the report's dataset.</span></span> <span data-ttu-id="d0ac6-110">Om wijzigingen te bekijken die zijn opgetreden in de onderliggende gegevens, moet u vernieuwen of een volledige, actuele gegevensset opnieuw importeren.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-110">To see changes that occurred to the underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="d0ac6-111">Alleen *tabellen en kolommen* zijn geïmporteerd of gekopieerd naar het rapport gegevensset.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-111">Only *tables and columns* are imported or copied into the report's dataset.</span></span> <span data-ttu-id="d0ac6-112">U weergeven altijd de meest recente gegevens.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-112">You always view the most current data.</span></span> |

<span data-ttu-id="d0ac6-113">Met Power BI Embedded u DirectQuery kunt gebruiken met gegevensbronnen van de cloud, maar niet on-premises gegevensbronnen op dit moment.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-113">With Power BI Embedded, you can use DirectQuery with cloud data sources but not on-premises data sources at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="d0ac6-114">De gegevensgateway On-Premises wordt niet ondersteund met Power BI Embedded op dit moment.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-114">The On-Premises Data Gateway is not supported with Power BI Embedded at this time.</span></span> <span data-ttu-id="d0ac6-115">Dit betekent dat u DirectQuery niet gebruiken met on-premises gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-115">This means you cannot use DirectQuery with on-premises data sources.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="d0ac6-116">Ondersteunde gegevensbronnen</span><span class="sxs-lookup"><span data-stu-id="d0ac6-116">Supported data sources</span></span>

<span data-ttu-id="d0ac6-117">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="d0ac6-117">**DirectQuery**</span></span>
* <span data-ttu-id="d0ac6-118">Azure SQL-database</span><span class="sxs-lookup"><span data-stu-id="d0ac6-118">Azure SQL database</span></span>
* <span data-ttu-id="d0ac6-119">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d0ac6-119">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="d0ac6-120">**Importeren**</span><span class="sxs-lookup"><span data-stu-id="d0ac6-120">**Import**</span></span>

<span data-ttu-id="d0ac6-121">U kunt importeren met alle van de beschikbare gegevensbronnen in Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-121">You can import using all of the available data sources within Power BI Desktop.</span></span> <span data-ttu-id="d0ac6-122">U gaat **niet** kunnen vernieuwen van gegevens in Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-122">You will **not** be able to refresh that data within Power BI Embedded.</span></span> <span data-ttu-id="d0ac6-123">U moet het uploaden van wijzigingen naar uw PBIX-bestand naar Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-123">You will have to upload changes to your PBIX file to Power BI Embedded.</span></span> <span data-ttu-id="d0ac6-124">Dit komt door geen beschikbare gateway.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-124">This is due to no available gateway.</span></span> 

## <a name="benefits-of-using-directquery"></a><span data-ttu-id="d0ac6-125">Voordelen van het gebruik van DirectQuery</span><span class="sxs-lookup"><span data-stu-id="d0ac6-125">Benefits of using DirectQuery</span></span>
<span data-ttu-id="d0ac6-126">Er zijn twee belangrijke voordelen bij gebruik van **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="d0ac6-126">There are two primary benefits when using **DirectQuery**:</span></span>

* <span data-ttu-id="d0ac6-127">**DirectQuery** kunt u bouwen visualisaties alle gegevens via zeer grote gegevenssets, waar deze anders unfeasible eerste importeren zijn zou.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-127">**DirectQuery** lets you build visualizations over very large datasets, where it otherwise would be unfeasible to first import all of the data.</span></span>
* <span data-ttu-id="d0ac6-128">Voor sommige rapporten de noodzaak om weer te geven gegevens van de huidige overdrachten van grote hoeveelheden gegevens, waardoor opnieuw importeren gegevens unfeasible kunt vereisen en onderliggende gegevenswijzigingen vereist een vernieuwing van gegevens.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-128">Underlying data changes can require a refresh of data, and for some reports, the need to display current data can require large data transfers, making re-importing data unfeasible.</span></span> <span data-ttu-id="d0ac6-129">Daarentegen **DirectQuery** rapporten altijd actuele gegevens gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-129">By contrast, **DirectQuery** reports always use current data.</span></span>

## <a name="limitations-of-directquery"></a><span data-ttu-id="d0ac6-130">Beperkingen van DirectQuery</span><span class="sxs-lookup"><span data-stu-id="d0ac6-130">Limitations of DirectQuery</span></span>
   <span data-ttu-id="d0ac6-131">Er zijn enkele beperkingen voor het gebruik van **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="d0ac6-131">There are a few limitations to using **DirectQuery**:</span></span>

* <span data-ttu-id="d0ac6-132">Alle tabellen moeten afkomstig zijn van een individuele database.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-132">All tables must come from a single database.</span></span>
* <span data-ttu-id="d0ac6-133">Als de query te complex is is, treedt er een fout op.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-133">If the query is overly complex, an error will occur.</span></span> <span data-ttu-id="d0ac6-134">Als u wilt de fout te verhelpen moet u de query opsplitsen zodat deze minder complex is.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-134">To remedy the error you must refactor the query so it is less complex.</span></span> <span data-ttu-id="d0ac6-135">Als de query complex zijn moet, moet u de gegevens in plaats van te importeren **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-135">If the query must be complex, you will need to import the data instead of using **DirectQuery**.</span></span>
* <span data-ttu-id="d0ac6-136">Relatie voor het filteren is beperkt tot één richting, in plaats van beide richtingen.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-136">Relationship filtering is limited to a single direction, rather than both directions.</span></span>
* <span data-ttu-id="d0ac6-137">U kunt het gegevenstype van een kolom niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-137">You cannot change the data type of a column.</span></span>
* <span data-ttu-id="d0ac6-138">Standaard worden de beperkingen op DAX-expressies toegestaan in metingen geplaatst.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-138">By default, limitations are placed on DAX expressions allowed in measures.</span></span> <span data-ttu-id="d0ac6-139">Zie [DirectQuery en metingen](#measures).</span><span class="sxs-lookup"><span data-stu-id="d0ac6-139">See [DirectQuery and measures](#measures).</span></span>

<a name="measures"/>

## <a name="directquery-and-measures"></a><span data-ttu-id="d0ac6-140">DirectQuery en metingen</span><span class="sxs-lookup"><span data-stu-id="d0ac6-140">DirectQuery and measures</span></span>
<span data-ttu-id="d0ac6-141">Query's verzonden naar de onderliggende gegevensbron hebben aanvaardbare prestaties, zodat worden beperkingen opgelegd voor metingen.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-141">To ensure queries sent to the underlying data source have acceptable performance, limitations are imposed on measures.</span></span> <span data-ttu-id="d0ac6-142">Wanneer u **Power BI Desktop**, geavanceerde gebruikers kunnen kiezen deze beperking omzeilen door te kiezen **bestand > Opties en instellingen > opties**.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-142">When using **Power BI Desktop**, advanced users can choose to bypass this limitation by choosing **File > Options and settings > Options**.</span></span> <span data-ttu-id="d0ac6-143">In de **opties** dialoogvenster kiezen **DirectQuery**, en selecteer de optie **onbeperkte metingen in DirectQuery-modus toestaan**.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-143">In the **Options** dialog, choose **DirectQuery**, and select the option **Allow unrestricted measures in DirectQuery mode**.</span></span> <span data-ttu-id="d0ac6-144">Wanneer deze optie is geselecteerd, kan een DAX-expressie die is geldig voor een meting kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-144">When that option is selected, any DAX expression that is valid for a measure can be used.</span></span> <span data-ttu-id="d0ac6-145">Gebruikers moeten zich op de hoogte; echter dat aantal expressies die zeer goed worden uitgevoerd wanneer de gegevens zijn geïmporteerd leiden zeer traag tot kunnen vragen naar de back-end bron wanneer in **DirectQuery** modus.</span><span class="sxs-lookup"><span data-stu-id="d0ac6-145">Users must be aware; however, that some expressions that perform very well when the data is imported may result in very slow queries to the backend source when in **DirectQuery** mode.</span></span> 

## <a name="see-also"></a><span data-ttu-id="d0ac6-146">Zie ook</span><span class="sxs-lookup"><span data-stu-id="d0ac6-146">See Also</span></span>
* [<span data-ttu-id="d0ac6-147">Aan de slag met Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="d0ac6-147">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)
* [<span data-ttu-id="d0ac6-148">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="d0ac6-148">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

<span data-ttu-id="d0ac6-149">Nog vragen?</span><span class="sxs-lookup"><span data-stu-id="d0ac6-149">More questions?</span></span> [<span data-ttu-id="d0ac6-150">Probeer de Power BI-community</span><span class="sxs-lookup"><span data-stu-id="d0ac6-150">Try the Power BI Community</span></span>](http://community.powerbi.com/)

