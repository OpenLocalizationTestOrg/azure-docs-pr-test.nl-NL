---
title: "Azure Analysis Services-zelfstudie - Les 9: Hiërarchieën maken | Microsoft Docs"
description: 
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: d628dc621335acf231342a6d9186079de16e85f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-9-create-hierarchies"></a><span data-ttu-id="3cba0-102">Les 9: Hiërarchieën maken</span><span class="sxs-lookup"><span data-stu-id="3cba0-102">Lesson 9: Create hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="3cba0-103">In deze les gaat u hiërarchieën maken.</span><span class="sxs-lookup"><span data-stu-id="3cba0-103">In this lesson, you create hierarchies.</span></span> <span data-ttu-id="3cba0-104">Hiërarchieën zijn groepen van kolommen die op niveaus zijn gerangschikt. Zo kan een hiërarchie Geografie onderliggende niveaus bevatten voor land, provincie en stad.</span><span class="sxs-lookup"><span data-stu-id="3cba0-104">Hierarchies are groups of columns arranged in levels; for example, a Geography hierarchy might have sublevels for Country, State, County, and City.</span></span> <span data-ttu-id="3cba0-105">Hiërarchieën kunnen los van andere kolommen worden weergegeven in een clienttoepassing voor rapportagedoeleinden. Hierdoor is het makkelijker voor gebruikers om door een hiërarchie te navigeren of deze op te nemen in een rapport.</span><span class="sxs-lookup"><span data-stu-id="3cba0-105">Hierarchies can appear separate from other columns in a reporting client application field list, making them easier for client users to navigate and include in a report.</span></span> <span data-ttu-id="3cba0-106">Zie [Hiërarchieën](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3cba0-106">To learn more, see [Hierarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span></span>
  
<span data-ttu-id="3cba0-107">U maakt hiërarchieën met de *diagramweergave* van de ontwerpfunctie voor modellen.</span><span class="sxs-lookup"><span data-stu-id="3cba0-107">To create hierarchies, use the model designer in *Diagram View*.</span></span> <span data-ttu-id="3cba0-108">De gegevensweergave is niet geschikt voor het maken en beheren van hiërarchieën.</span><span class="sxs-lookup"><span data-stu-id="3cba0-108">Creating and managing hierarchies is not supported in Data View.</span></span>  
  
<span data-ttu-id="3cba0-109">Geschatte tijd voor het voltooien van deze les: **20 minuten**</span><span class="sxs-lookup"><span data-stu-id="3cba0-109">Estimated time to complete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="3cba0-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3cba0-110">Prerequisites</span></span>  
<span data-ttu-id="3cba0-111">Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3cba0-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="3cba0-112">Voordat u de taken in deze les gaat uitvoeren, moet u de vorige les hebben voltooid: [Les 8: Perspectieven maken](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="3cba0-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>  
  
## <a name="create-hierarchies"></a><span data-ttu-id="3cba0-113">Hiërarchieën maken</span><span class="sxs-lookup"><span data-stu-id="3cba0-113">Create hierarchies</span></span>  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a><span data-ttu-id="3cba0-114">Een hiërarchie Category maken in de tabel DimProduct:</span><span class="sxs-lookup"><span data-stu-id="3cba0-114">To create a Category hierarchy in the DimProduct table</span></span>  
  
1.  <span data-ttu-id="3cba0-115">Klik in de ontwerpfunctie voor modellen (in de diagramweergave) met de rechtermuisknop op de tabel **DimProduct** > **Create Hierarchy**.</span><span class="sxs-lookup"><span data-stu-id="3cba0-115">In the model designer (diagram view), right-click the **DimProduct** table > **Create Hierarchy**.</span></span> <span data-ttu-id="3cba0-116">Er wordt onderaan het tabelvenster een nieuwe hiërarchie weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3cba0-116">A new hierarchy appears at the bottom of the table window.</span></span> <span data-ttu-id="3cba0-117">Wijzig de naam van de hiërarchie in **Category**.</span><span class="sxs-lookup"><span data-stu-id="3cba0-117">Rename the hierarchy **Category**.</span></span>  
  
2.  <span data-ttu-id="3cba0-118">Sleep de kolom **ProductCategoryName** naar de nieuwe hiërarchie **Category**.</span><span class="sxs-lookup"><span data-stu-id="3cba0-118">Click and drag the **ProductCategoryName** column to the new **Category** hierarchy.</span></span>  
  
3.  <span data-ttu-id="3cba0-119">Klik in de hiërarchie **Category** met de rechtermuisknop op **ProductCategoryName** > **Rename** en typ vervolgens **Category**.</span><span class="sxs-lookup"><span data-stu-id="3cba0-119">In the **Category** hierarchy, right-click the **ProductCategoryName** > **Rename**, and then type **Category**.</span></span>  
  
    > [!NOTE]  
    > <span data-ttu-id="3cba0-120">Als u de naam van een kolom wijzigt in een hiërarchie, wordt de naam van die kolom niet gewijzigd in de onderliggende tabel.</span><span class="sxs-lookup"><span data-stu-id="3cba0-120">Renaming a column in a hierarchy does not rename that column in the table.</span></span> <span data-ttu-id="3cba0-121">Een kolom in een hiërarchie is alleen maar een weergave van de kolom in de tabel.</span><span class="sxs-lookup"><span data-stu-id="3cba0-121">A column in a hierarchy is just a representation of the column in the table.</span></span>  
  
4.  <span data-ttu-id="3cba0-122">Sleep de kolom **ProductSubcategoryName** naar de hiërarchie **Category**.</span><span class="sxs-lookup"><span data-stu-id="3cba0-122">Click and drag the **ProductSubcategoryName** column to the **Category** hierarchy.</span></span> <span data-ttu-id="3cba0-123">Wijzig de naam in **Subcategory**.</span><span class="sxs-lookup"><span data-stu-id="3cba0-123">Rename it **Subcategory**.</span></span> 
  
5.  <span data-ttu-id="3cba0-124">Klik met de rechtermuisknop op de kolom **ModelName** > **Add to hierarchy** en selecteer vervolgens **Category**.</span><span class="sxs-lookup"><span data-stu-id="3cba0-124">Right-click the **ModelName** column > **Add to hierarchy**, and then select **Category**.</span></span> <span data-ttu-id="3cba0-125">Wijzig de naam in **Model**.</span><span class="sxs-lookup"><span data-stu-id="3cba0-125">Rename it **Model**.</span></span>

6.  <span data-ttu-id="3cba0-126">Voeg als laatste **EnglishProductName** toe aan de hiërarchie.</span><span class="sxs-lookup"><span data-stu-id="3cba0-126">Finally, add **EnglishProductName** to the Category hierarchy.</span></span> <span data-ttu-id="3cba0-127">Wijzig de naam in **Product**.</span><span class="sxs-lookup"><span data-stu-id="3cba0-127">Rename it **Product**.</span></span>  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a><span data-ttu-id="3cba0-129">Hiërarchieën maken in de tabel DimDate:</span><span class="sxs-lookup"><span data-stu-id="3cba0-129">To create hierarchies in the DimDate table</span></span>  
  
1.  <span data-ttu-id="3cba0-130">Maak in de tabel **DimDate** een hiërarchie met de naam **Calendar**.</span><span class="sxs-lookup"><span data-stu-id="3cba0-130">In the **DimDate** table, create a hierarchy named **Calendar**.</span></span>  
  
3.  <span data-ttu-id="3cba0-131">Voeg de volgende kolommen in deze volgorde toe:</span><span class="sxs-lookup"><span data-stu-id="3cba0-131">Add the following columns in-order:</span></span>

    *  <span data-ttu-id="3cba0-132">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="3cba0-132">CalendarYear</span></span>
    *  <span data-ttu-id="3cba0-133">CalendarSemester</span><span class="sxs-lookup"><span data-stu-id="3cba0-133">CalendarSemester</span></span>
    *  <span data-ttu-id="3cba0-134">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="3cba0-134">CalendarQuarter</span></span>
    *  <span data-ttu-id="3cba0-135">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="3cba0-135">MonthCalendar</span></span>
    *  <span data-ttu-id="3cba0-136">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="3cba0-136">DayNumberOfMonth</span></span>
    
4.  <span data-ttu-id="3cba0-137">Maak in de tabel **DimDate** een hiërarchie met de naam **Fiscal**.</span><span class="sxs-lookup"><span data-stu-id="3cba0-137">In the **DimDate** table, create a **Fiscal** hierarchy.</span></span> <span data-ttu-id="3cba0-138">Voeg de volgende kolommen in deze volgorde toe:</span><span class="sxs-lookup"><span data-stu-id="3cba0-138">Include the following columns in-order:</span></span>  
  
    *  <span data-ttu-id="3cba0-139">FiscalYear</span><span class="sxs-lookup"><span data-stu-id="3cba0-139">FiscalYear</span></span>
    *  <span data-ttu-id="3cba0-140">FiscalSemester</span><span class="sxs-lookup"><span data-stu-id="3cba0-140">FiscalSemester</span></span>
    *  <span data-ttu-id="3cba0-141">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="3cba0-141">FiscalQuarter</span></span>
    *  <span data-ttu-id="3cba0-142">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="3cba0-142">MonthCalendar</span></span>
    *  <span data-ttu-id="3cba0-143">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="3cba0-143">DayNumberOfMonth</span></span>
  
5.  <span data-ttu-id="3cba0-144">Maak ten slotte in de tabel **DimDate** een hiërarchie **ProductionCalendar**.</span><span class="sxs-lookup"><span data-stu-id="3cba0-144">Finally, in the **DimDate** table, create a **ProductionCalendar** hierarchy.</span></span> <span data-ttu-id="3cba0-145">Voeg de volgende kolommen in deze volgorde toe:</span><span class="sxs-lookup"><span data-stu-id="3cba0-145">Include the following columns in-order:</span></span>  
    *  <span data-ttu-id="3cba0-146">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="3cba0-146">CalendarYear</span></span>
    *  <span data-ttu-id="3cba0-147">WeekNumberOfYear</span><span class="sxs-lookup"><span data-stu-id="3cba0-147">WeekNumberOfYear</span></span>
    *  <span data-ttu-id="3cba0-148">DayNumberOfWeek</span><span class="sxs-lookup"><span data-stu-id="3cba0-148">DayNumberOfWeek</span></span>
  
 ## <a name="whats-next"></a><span data-ttu-id="3cba0-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3cba0-149">What's next?</span></span>
<span data-ttu-id="3cba0-150">[Les 10: Partities maken](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="3cba0-150">[Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span> 
  
  
