---
title: 'Azure Analysis Services-zelfstudie - Les 8: Perspectieven maken| Microsoft Docs'
description: In deze les wordt beschreven hoe u perspectieven maakt in de zelfstudie over Azure Analysis Services.
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
ms.openlocfilehash: 491500909b0de0360afae45e172e85999d764fe0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-8-create-perspectives"></a><span data-ttu-id="1cf5e-103">Les 8: Perspectieven maken</span><span class="sxs-lookup"><span data-stu-id="1cf5e-103">Lesson 8: Create perspectives</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="1cf5e-104">In deze les maakt u een perspectief voor internetverkopen.</span><span class="sxs-lookup"><span data-stu-id="1cf5e-104">In this lesson, you create an Internet Sales perspective.</span></span> <span data-ttu-id="1cf5e-105">Een perspectief definieert een subset van een model dat u kunt weergeven om gerichte, bedrijfsspecifieke of toepassingsspecifieke standpunten inzichtelijk te maken.</span><span class="sxs-lookup"><span data-stu-id="1cf5e-105">A perspective defines a viewable subset of a model that provides focused, business-specific, or application-specific viewpoints.</span></span> <span data-ttu-id="1cf5e-106">Wanneer een gebruiker via een perspectief verbinding maakt met een model, worden alleen de modelobjecten (tabellen, kolommen, metingen, hiërarchieën en KPI's) weergegeven die als veld zijn gedefinieerd in dat perspectief.</span><span class="sxs-lookup"><span data-stu-id="1cf5e-106">When a user connects to a model by using a perspective, they see only those model objects (tables, columns, measures, hierarchies, and KPIs) as fields defined in that perspective.</span></span> <span data-ttu-id="1cf5e-107">Zie [Perspectieven](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1cf5e-107">To learn more, see [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span></span>
  
<span data-ttu-id="1cf5e-108">In deze les gaat u een perspectief maken (Internet Sales) waarmee het tabelobject DimCustomer wordt uitgesloten van weergave.</span><span class="sxs-lookup"><span data-stu-id="1cf5e-108">The Internet Sales perspective you create in this lesson excludes the DimCustomer table object.</span></span> <span data-ttu-id="1cf5e-109">Wanneer u een perspectief maakt waarmee bepaalde objecten worden uitgesloten voor weergave, is dit object nog steeds aanwezig in het model.</span><span class="sxs-lookup"><span data-stu-id="1cf5e-109">When you create a perspective that excludes certain objects from view, that object still exists in the model.</span></span> <span data-ttu-id="1cf5e-110">Het object wordt echter niet vermeld in de lijst met velden van de rapportageclient.</span><span class="sxs-lookup"><span data-stu-id="1cf5e-110">However, it is not visible in a reporting client field list.</span></span> <span data-ttu-id="1cf5e-111">Berekende kolommen en metingen die al dan niet zijn opgenomen in een perspectief, kunnen nog steeds werken met uitgesloten objectgegevens.</span><span class="sxs-lookup"><span data-stu-id="1cf5e-111">Calculated columns and measures either included in a perspective or not can still calculate from object data that is excluded.</span></span>  
  
<span data-ttu-id="1cf5e-112">In deze les leert u hoe u perspectieven maakt en hoe u de hulpmiddelen van het programma voor het ontwerpen van tabellaire modellen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1cf5e-112">The purpose of this lesson is to describe how to create perspectives and become familiar with the tabular model authoring tools.</span></span> <span data-ttu-id="1cf5e-113">Als u dit model later gaat uitbreiden met aanvullende tabellen, kunt u ook extra perspectieven maken om verschillende standpunten van het model te definiëren, zoals Inventory en Sales.</span><span class="sxs-lookup"><span data-stu-id="1cf5e-113">If you later expand this model to include additional tables, you can create additional perspectives to define different viewpoints of the model, for example, Inventory and Sales.</span></span>  
  
<span data-ttu-id="1cf5e-114">Geschatte tijd voor het voltooien van deze les: **5 minuten**</span><span class="sxs-lookup"><span data-stu-id="1cf5e-114">Estimated time to complete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="1cf5e-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1cf5e-115">Prerequisites</span></span>  
<span data-ttu-id="1cf5e-116">Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1cf5e-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="1cf5e-117">Voordat u de taken in deze les gaat uitvoeren, moet u de vorige les hebben voltooid: [Les 7: Key Performance Indicators maken](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="1cf5e-117">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  
  
## <a name="create-perspectives"></a><span data-ttu-id="1cf5e-118">Perspectieven maken</span><span class="sxs-lookup"><span data-stu-id="1cf5e-118">Create perspectives</span></span>  
  
#### <a name="to-create-an-internet-sales-perspective"></a><span data-ttu-id="1cf5e-119">Een perspectief Internet Sales maken:</span><span class="sxs-lookup"><span data-stu-id="1cf5e-119">To create an Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="1cf5e-120">Klik op het menu **Model** > **Perspectives** > **Create and Manage**.</span><span class="sxs-lookup"><span data-stu-id="1cf5e-120">Click the **Model** menu > **Perspectives** > **Create and Manage**.</span></span>  
  
2.  <span data-ttu-id="1cf5e-121">Klik in het dialoogvenster **Perspectives** op **New Perspective**.</span><span class="sxs-lookup"><span data-stu-id="1cf5e-121">In the **Perspectives** dialog box, click **New Perspective**.</span></span>  
  
3.  <span data-ttu-id="1cf5e-122">Dubbelklik op de kolomkop **New Perspective** en wijzig de naam van de kolom in **Internet Sales**.</span><span class="sxs-lookup"><span data-stu-id="1cf5e-122">Double-click the **New Perspective** column heading, and then rename **Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="1cf5e-123">Selecteer alle tabellen *behalve* **DimCustomer**.</span><span class="sxs-lookup"><span data-stu-id="1cf5e-123">Select the all the tables *except* **DimCustomer**.</span></span>  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    <span data-ttu-id="1cf5e-125">In een latere les gebruikt u de functie Analyseren van Excel om dit perspectief te testen.</span><span class="sxs-lookup"><span data-stu-id="1cf5e-125">In a later lesson, you use the Analyze in Excel feature to test this perspective.</span></span> <span data-ttu-id="1cf5e-126">De lijst met draaitabelvelden van Excel bevat dan alle tabellen, behalve de tabel DimCustomer.</span><span class="sxs-lookup"><span data-stu-id="1cf5e-126">The Excel PivotTable Fields List includes each table except the DimCustomer table.</span></span>  

## <a name="whats-next"></a><span data-ttu-id="1cf5e-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1cf5e-127">What's next?</span></span>
<span data-ttu-id="1cf5e-128">[Les 9: Hiërarchieën maken](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="1cf5e-128">[Lesson 9: Create hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>
  
  
  
  
