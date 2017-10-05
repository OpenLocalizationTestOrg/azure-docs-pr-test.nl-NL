---
title: 'Azure Analysis Services-zelfstudie - Les 7: Key Performance Indicators maken | Microsoft Docs'
description: In deze les wordt beschreven hoe u Key Performance Indicator maakt in de zelfstudie over Azure Analysis Services.
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
ms.openlocfilehash: d78808421dd5acd907aa9e9000bb3b770a42c061
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-7-create-key-performance-indicators"></a><span data-ttu-id="50d9a-103">Les 7: Key Performance Indicators maken</span><span class="sxs-lookup"><span data-stu-id="50d9a-103">Lesson 7: Create Key Performance Indicators</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="50d9a-104">In deze les gaat u Key Performance Indicators (KPI's) maken.</span><span class="sxs-lookup"><span data-stu-id="50d9a-104">In this lesson, you create Key Performance Indicators (KPIs).</span></span> <span data-ttu-id="50d9a-105">KPI's worden gebruikt om de prestaties van een waarde te meten door een basislijn (*Base*), opgegeven als een meting, te vergelijken met een doelwaarde (*Target*), die ook is gedefinieerd met een meting of met een absolute waarde.</span><span class="sxs-lookup"><span data-stu-id="50d9a-105">KPIs are used to gauge performance of a value defined by a *Base* measure, against a *Target* value also defined by a measure, or by an absolute value.</span></span> <span data-ttu-id="50d9a-106">In rapportageclienttoepassingen zijn KPI's een snelle en gemakkelijke manier om een overzicht te krijgen van de succesfactoren van een onderneming of om trends te identificeren.</span><span class="sxs-lookup"><span data-stu-id="50d9a-106">In reporting client applications, KPIs can provide business professionals a quick and easy way to understand a summary of business success or to identify trends.</span></span> <span data-ttu-id="50d9a-107">Zie [KPI's](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="50d9a-107">To learn more, see [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span></span>
  
<span data-ttu-id="50d9a-108">Geschatte tijd voor het voltooien van deze les: **15 minuten**</span><span class="sxs-lookup"><span data-stu-id="50d9a-108">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="50d9a-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="50d9a-109">Prerequisites</span></span>  
<span data-ttu-id="50d9a-110">Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="50d9a-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="50d9a-111">Voordat u de taken in deze les gaat uitvoeren, moet u de vorige les hebben voltooid: [Les 6: Metingen maken](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="50d9a-111">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>   
  
## <a name="create-key-performance-indicators"></a><span data-ttu-id="50d9a-112">Key Performance Indicators maken</span><span class="sxs-lookup"><span data-stu-id="50d9a-112">Create Key Performance Indicators</span></span>  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a><span data-ttu-id="50d9a-113">Een KPI InternetCurrentQuarterSalesPerformance maken:</span><span class="sxs-lookup"><span data-stu-id="50d9a-113">To create an InternetCurrentQuarterSalesPerformance KPI</span></span>  
  
1.  <span data-ttu-id="50d9a-114">Klik in de ontwerpfunctie voor modellen op de tabel **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="50d9a-114">In the model designer, click the **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="50d9a-115">Klik in het metingenraster op een lege cel.</span><span class="sxs-lookup"><span data-stu-id="50d9a-115">In the measure grid, click an empty cell.</span></span>  
  
3.  <span data-ttu-id="50d9a-116">Typ op de formulebalk boven de tabel de volgende formule:</span><span class="sxs-lookup"><span data-stu-id="50d9a-116">In the formula bar, above the table, type the following formula:</span></span> 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    <span data-ttu-id="50d9a-117">Deze meting fungeert als de basislijn voor de KPI.</span><span class="sxs-lookup"><span data-stu-id="50d9a-117">This measure serves as the Base measure for the KPI.</span></span>  
  
4.  <span data-ttu-id="50d9a-118">Klik met de rechtermuisknop op **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span><span class="sxs-lookup"><span data-stu-id="50d9a-118">Right-click **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span></span>   
  
5.  <span data-ttu-id="50d9a-119">Ga naar **Target** in het dialoogvenster Key Performance Indicator (KPI) en selecteer **Absolute value** en typ vervolgens **1.1**.</span><span class="sxs-lookup"><span data-stu-id="50d9a-119">In the Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.1**.</span></span>  
  
7.  <span data-ttu-id="50d9a-120">Typ **1** in het veld met de schuifregelaar voor lage waarden (links) en **1.07** in het veld met de schuifregelaar voor hoge waarden (rechts).</span><span class="sxs-lookup"><span data-stu-id="50d9a-120">In the left (low) slider field, type **1**, and then in the right (high) slider field, type **1.07**.</span></span>  
  
8.  <span data-ttu-id="50d9a-121">Selecteer bij **Select icon style** de reeks met een ruit (rood), driehoek (geel) en cirkel (groen).</span><span class="sxs-lookup"><span data-stu-id="50d9a-121">In **Select Icon Style**, select the diamond (red), triangle (yellow), circle (green) icon type.</span></span>
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > <span data-ttu-id="50d9a-123">U kunt desgewenst een beschrijving weergeven door **Descriptions** uit te vouwen onder de beschikbare pictogramreeksen.</span><span class="sxs-lookup"><span data-stu-id="50d9a-123">Notice the expandable **Descriptions** label below the available icon styles.</span></span> <span data-ttu-id="50d9a-124">Gebruik beschrijvingen voor de verschillende onderdelen van de KPI, zodat ze makkelijker herkenbaar zijn in clienttoepassingen.</span><span class="sxs-lookup"><span data-stu-id="50d9a-124">Use descriptions for the various KPI elements to make them more identifiable in client applications.</span></span>  
  
9. <span data-ttu-id="50d9a-125">Klik op **OK** om de KPI te voltooien.</span><span class="sxs-lookup"><span data-stu-id="50d9a-125">Click **OK** to complete the KPI.</span></span>  
  
    <span data-ttu-id="50d9a-126">In het metingenraster ziet u nu een pictogram naast de meting **InternetCurrentQuarterSalesPerformance**.</span><span class="sxs-lookup"><span data-stu-id="50d9a-126">In the measure grid, notice the icon next to the **InternetCurrentQuarterSalesPerformance** measure.</span></span> <span data-ttu-id="50d9a-127">Dit pictogram geeft aan dat deze meting fungeert als een basislijn voor een KPI.</span><span class="sxs-lookup"><span data-stu-id="50d9a-127">This icon indicates that this measure serves as a Base value for a KPI.</span></span>  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a><span data-ttu-id="50d9a-128">Een KPI InternetCurrentQuarterMarginPerformance maken:</span><span class="sxs-lookup"><span data-stu-id="50d9a-128">To create an InternetCurrentQuarterMarginPerformance KPI</span></span>  
  
1.  <span data-ttu-id="50d9a-129">Klik in metingenraster voor de tabel **FactInternetSales** op een lege cel.</span><span class="sxs-lookup"><span data-stu-id="50d9a-129">In the measure grid for the **FactInternetSales** table, click an empty cell.</span></span>  
  
2.  <span data-ttu-id="50d9a-130">Typ op de formulebalk boven de tabel de volgende formule:</span><span class="sxs-lookup"><span data-stu-id="50d9a-130">In the formula bar, above the table, type the following formula:</span></span>  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  <span data-ttu-id="50d9a-131">Klik met de rechtermuisknop op **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span><span class="sxs-lookup"><span data-stu-id="50d9a-131">Right-click **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span></span>  
  
4.  <span data-ttu-id="50d9a-132">Ga naar **Target** in het dialoogvenster Key Performance Indicator (KPI) en selecteer **Absolute value** en typ vervolgens **1.25**.</span><span class="sxs-lookup"><span data-stu-id="50d9a-132">In the Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.25**.</span></span>   
  
5.  <span data-ttu-id="50d9a-133">Sleep de schuifregelaar voor lage waarden (links) totdat **0.8** wordt weergegeven en sleep vervolgens de schuifregelaar voor hoge waarden (rechts) totdat **1.03** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="50d9a-133">In the left (low) slider field, slide until the field displays **0.8**, and then slide the right (high) slider field, until the field displays **1.03**.</span></span>  
  
6.  <span data-ttu-id="50d9a-134">Selecteer bij **Select icon style** de reeks met een ruit (rood), driehoek (geel) en cirkel (groen), en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="50d9a-134">In **Select Icon Style**, select the diamond (red), triangle (yellow), circle (green) icon type, and then click **OK**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="50d9a-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="50d9a-135">What's next?</span></span>
<span data-ttu-id="50d9a-136">[Les 8: Perspectieven maken](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="50d9a-136">[Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>
  
  
