---
title: aaaMicrosoft Power BI Embedded - verbindende tooa-gegevensbron
description: Power BI Embedded, toodata bronnen verbinding maken
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
ms.openlocfilehash: b1aad6e638104716d90f7e1d060eefcbc9daedbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-data-source"></a><span data-ttu-id="5988c-103">Verbinding maken met gegevensbron tooa</span><span class="sxs-lookup"><span data-stu-id="5988c-103">Connect tooa data source</span></span>
<span data-ttu-id="5988c-104">Met **Power BI Embedded**, kunt u rapporten insluiten in uw eigen app.</span><span class="sxs-lookup"><span data-stu-id="5988c-104">With **Power BI Embedded**, you can embed reports into your own app.</span></span> <span data-ttu-id="5988c-105">Wanneer u een Power BI-rapport in uw app insluiten, Hallo rapport toohello gegevens door de onderliggende verbinding **importeren** een kopie van Hallo gegevens of door **rechtstreeks verbinding maken** toohello gegevensbron via  **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="5988c-105">When you embed a Power BI report into your app, hello report connects toohello underlying data by **importing** a copy of hello data or by **connecting directly** toohello data source using **DirectQuery**.</span></span>

<span data-ttu-id="5988c-106">Hier volgen Hallo verschillen tussen het gebruik van **importeren** en **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="5988c-106">Here are hello differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="5988c-107">Importeren</span><span class="sxs-lookup"><span data-stu-id="5988c-107">Import</span></span> | <span data-ttu-id="5988c-108">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="5988c-108">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="5988c-109">Tabellen, kolommen *en gegevens* zijn geïmporteerd of gekopieerd naar de gegevensset Hallo van het rapport.</span><span class="sxs-lookup"><span data-stu-id="5988c-109">Tables, columns, *and data* are imported or copied into hello report's dataset.</span></span> <span data-ttu-id="5988c-110">toosee die opgetreden toohello onderliggende gegevens wordt gewijzigd, moet u vernieuwen of importeren, een volledige, actuele gegevensset opnieuw.</span><span class="sxs-lookup"><span data-stu-id="5988c-110">toosee changes that occurred toohello underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="5988c-111">Alleen *tabellen en kolommen* zijn geïmporteerd of gekopieerd naar de gegevensset Hallo van het rapport.</span><span class="sxs-lookup"><span data-stu-id="5988c-111">Only *tables and columns* are imported or copied into hello report's dataset.</span></span> <span data-ttu-id="5988c-112">U weergeven altijd de meest recente gegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="5988c-112">You always view hello most current data.</span></span> |

<span data-ttu-id="5988c-113">Met Power BI Embedded u DirectQuery kunt gebruiken met gegevensbronnen van de cloud, maar niet on-premises gegevensbronnen op dit moment.</span><span class="sxs-lookup"><span data-stu-id="5988c-113">With Power BI Embedded, you can use DirectQuery with cloud data sources but not on-premises data sources at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="5988c-114">Hallo wordt On-Premises Data Gateway niet ondersteund met Power BI Embedded op dit moment.</span><span class="sxs-lookup"><span data-stu-id="5988c-114">hello On-Premises Data Gateway is not supported with Power BI Embedded at this time.</span></span> <span data-ttu-id="5988c-115">Dit betekent dat u DirectQuery niet gebruiken met on-premises gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="5988c-115">This means you cannot use DirectQuery with on-premises data sources.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="5988c-116">Ondersteunde gegevensbronnen</span><span class="sxs-lookup"><span data-stu-id="5988c-116">Supported data sources</span></span>

<span data-ttu-id="5988c-117">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="5988c-117">**DirectQuery**</span></span>
* <span data-ttu-id="5988c-118">Azure SQL-database</span><span class="sxs-lookup"><span data-stu-id="5988c-118">Azure SQL database</span></span>
* <span data-ttu-id="5988c-119">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5988c-119">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="5988c-120">**Importeren**</span><span class="sxs-lookup"><span data-stu-id="5988c-120">**Import**</span></span>

<span data-ttu-id="5988c-121">U kunt importeren met alle beschikbare gegevensbronnen Hallo in Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="5988c-121">You can import using all of hello available data sources within Power BI Desktop.</span></span> <span data-ttu-id="5988c-122">U gaat **niet** kunnen toorefresh worden gegevens in Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="5988c-122">You will **not** be able toorefresh that data within Power BI Embedded.</span></span> <span data-ttu-id="5988c-123">U hebt wijzigingen tooupload tooyour PBIX-bestand tooPower BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="5988c-123">You will have tooupload changes tooyour PBIX file tooPower BI Embedded.</span></span> <span data-ttu-id="5988c-124">Dit is vanwege toono beschikbare gateway.</span><span class="sxs-lookup"><span data-stu-id="5988c-124">This is due toono available gateway.</span></span> 

## <a name="benefits-of-using-directquery"></a><span data-ttu-id="5988c-125">Voordelen van het gebruik van DirectQuery</span><span class="sxs-lookup"><span data-stu-id="5988c-125">Benefits of using DirectQuery</span></span>
<span data-ttu-id="5988c-126">Er zijn twee belangrijke voordelen bij gebruik van **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="5988c-126">There are two primary benefits when using **DirectQuery**:</span></span>

* <span data-ttu-id="5988c-127">**DirectQuery** kunt u visualisaties op zeer grote gegevenssets bouwt, waar deze anders unfeasible toofirst importeren zijn zou alle Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="5988c-127">**DirectQuery** lets you build visualizations over very large datasets, where it otherwise would be unfeasible toofirst import all of hello data.</span></span>
* <span data-ttu-id="5988c-128">Onderliggende gegevenswijzigingen kunt vereisen een vernieuwing van gegevens, en voor sommige rapporten hello moet toodisplay actuele gegevens kunt vereisen grote hoeveelheden gegevens veroorzaken, waardoor opnieuw importeren gegevens unfeasible.</span><span class="sxs-lookup"><span data-stu-id="5988c-128">Underlying data changes can require a refresh of data, and for some reports, hello need toodisplay current data can require large data transfers, making re-importing data unfeasible.</span></span> <span data-ttu-id="5988c-129">Daarentegen **DirectQuery** rapporten altijd actuele gegevens gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5988c-129">By contrast, **DirectQuery** reports always use current data.</span></span>

## <a name="limitations-of-directquery"></a><span data-ttu-id="5988c-130">Beperkingen van DirectQuery</span><span class="sxs-lookup"><span data-stu-id="5988c-130">Limitations of DirectQuery</span></span>
   <span data-ttu-id="5988c-131">Er zijn enkele beperkingen toousing **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="5988c-131">There are a few limitations toousing **DirectQuery**:</span></span>

* <span data-ttu-id="5988c-132">Alle tabellen moeten afkomstig zijn van een individuele database.</span><span class="sxs-lookup"><span data-stu-id="5988c-132">All tables must come from a single database.</span></span>
* <span data-ttu-id="5988c-133">Als Hallo-query te complex is, treedt er een fout op.</span><span class="sxs-lookup"><span data-stu-id="5988c-133">If hello query is overly complex, an error will occur.</span></span> <span data-ttu-id="5988c-134">tooremedy hello fout moet u de Hallo query opsplitsen zodat deze minder complex is.</span><span class="sxs-lookup"><span data-stu-id="5988c-134">tooremedy hello error you must refactor hello query so it is less complex.</span></span> <span data-ttu-id="5988c-135">Als het Hallo-query moet complex zijn, moet u tooimport Hallo gegevens in plaats van **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="5988c-135">If hello query must be complex, you will need tooimport hello data instead of using **DirectQuery**.</span></span>
* <span data-ttu-id="5988c-136">Relatie voor het filteren is beperkt tooa één richting, in plaats van beide richtingen.</span><span class="sxs-lookup"><span data-stu-id="5988c-136">Relationship filtering is limited tooa single direction, rather than both directions.</span></span>
* <span data-ttu-id="5988c-137">U kunt Hallo-gegevenstype van een kolom niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5988c-137">You cannot change hello data type of a column.</span></span>
* <span data-ttu-id="5988c-138">Standaard worden de beperkingen op DAX-expressies toegestaan in metingen geplaatst.</span><span class="sxs-lookup"><span data-stu-id="5988c-138">By default, limitations are placed on DAX expressions allowed in measures.</span></span> <span data-ttu-id="5988c-139">Zie [DirectQuery en metingen](#measures).</span><span class="sxs-lookup"><span data-stu-id="5988c-139">See [DirectQuery and measures](#measures).</span></span>

<a name="measures"/>

## <a name="directquery-and-measures"></a><span data-ttu-id="5988c-140">DirectQuery en metingen</span><span class="sxs-lookup"><span data-stu-id="5988c-140">DirectQuery and measures</span></span>
<span data-ttu-id="5988c-141">tooensure query's verzonden van de onderliggende gegevensbron toohello hebben aanvaardbare prestaties, beperkingen worden opgelegd voor metingen.</span><span class="sxs-lookup"><span data-stu-id="5988c-141">tooensure queries sent toohello underlying data source have acceptable performance, limitations are imposed on measures.</span></span> <span data-ttu-id="5988c-142">Wanneer u **Power BI Desktop**, geavanceerde gebruikers kunnen kiezen toobypass deze beperking door te kiezen **bestand > Opties en instellingen > opties**.</span><span class="sxs-lookup"><span data-stu-id="5988c-142">When using **Power BI Desktop**, advanced users can choose toobypass this limitation by choosing **File > Options and settings > Options**.</span></span> <span data-ttu-id="5988c-143">In Hallo **opties** dialoogvenster kiezen **DirectQuery**, en selecteer de optie Hallo **onbeperkte metingen in DirectQuery-modus toestaan**.</span><span class="sxs-lookup"><span data-stu-id="5988c-143">In hello **Options** dialog, choose **DirectQuery**, and select hello option **Allow unrestricted measures in DirectQuery mode**.</span></span> <span data-ttu-id="5988c-144">Wanneer deze optie is geselecteerd, kan een DAX-expressie die is geldig voor een meting kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5988c-144">When that option is selected, any DAX expression that is valid for a measure can be used.</span></span> <span data-ttu-id="5988c-145">Gebruikers moeten zich op de hoogte; dat sommige expressies die uitstekend presteren wanneer Hallo gegevens worden geïmporteerd kunnen echter resulteren in zeer traag query's toohello back-end bron wanneer in **DirectQuery** modus.</span><span class="sxs-lookup"><span data-stu-id="5988c-145">Users must be aware; however, that some expressions that perform very well when hello data is imported may result in very slow queries toohello backend source when in **DirectQuery** mode.</span></span> 

## <a name="see-also"></a><span data-ttu-id="5988c-146">Zie ook</span><span class="sxs-lookup"><span data-stu-id="5988c-146">See Also</span></span>
* [<span data-ttu-id="5988c-147">Aan de slag met Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="5988c-147">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)
* [<span data-ttu-id="5988c-148">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="5988c-148">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

<span data-ttu-id="5988c-149">Nog vragen?</span><span class="sxs-lookup"><span data-stu-id="5988c-149">More questions?</span></span> [<span data-ttu-id="5988c-150">Probeer Hallo Power BI-Community</span><span class="sxs-lookup"><span data-stu-id="5988c-150">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

