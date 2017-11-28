---
title: aaa "Azure Analysis Services zelfstudie les 8 maken perspectieven | Microsoft Docs'
description: Hierin wordt beschreven hoe toocreate perspectieven in Hallo zelfstudie Azure Analysis Services-project.
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
ms.openlocfilehash: 25391813e1969ecb22af4d6f9c1ccd8358d812fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-8-create-perspectives"></a><span data-ttu-id="8c99c-103">Les 8: Perspectieven maken</span><span class="sxs-lookup"><span data-stu-id="8c99c-103">Lesson 8: Create perspectives</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="8c99c-104">In deze les maakt u een perspectief voor internetverkopen.</span><span class="sxs-lookup"><span data-stu-id="8c99c-104">In this lesson, you create an Internet Sales perspective.</span></span> <span data-ttu-id="8c99c-105">Een perspectief definieert een subset van een model dat u kunt weergeven om gerichte, bedrijfsspecifieke of toepassingsspecifieke standpunten inzichtelijk te maken.</span><span class="sxs-lookup"><span data-stu-id="8c99c-105">A perspective defines a viewable subset of a model that provides focused, business-specific, or application-specific viewpoints.</span></span> <span data-ttu-id="8c99c-106">Wanneer een gebruiker verbinding tooa model maakt met behulp van een perspectief, zien ze alleen modelobjecten (tabellen, kolommen, metingen, hiërarchieën en KPI's) als velden die zijn gedefinieerd in dit perspectief.</span><span class="sxs-lookup"><span data-stu-id="8c99c-106">When a user connects tooa model by using a perspective, they see only those model objects (tables, columns, measures, hierarchies, and KPIs) as fields defined in that perspective.</span></span> <span data-ttu-id="8c99c-107">toolearn meer, Zie [perspectieven](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="8c99c-107">toolearn more, see [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span></span>
  
<span data-ttu-id="8c99c-108">Hallo Internet verkoop perspectief die u in deze les maakt sluit Hallo DimCustomer table-object.</span><span class="sxs-lookup"><span data-stu-id="8c99c-108">hello Internet Sales perspective you create in this lesson excludes hello DimCustomer table object.</span></span> <span data-ttu-id="8c99c-109">Wanneer u een perspectief dat bepaalde objecten van weergave uitsluit maakt, bestaat dat object nog in Hallo model.</span><span class="sxs-lookup"><span data-stu-id="8c99c-109">When you create a perspective that excludes certain objects from view, that object still exists in hello model.</span></span> <span data-ttu-id="8c99c-110">Het object wordt echter niet vermeld in de lijst met velden van de rapportageclient.</span><span class="sxs-lookup"><span data-stu-id="8c99c-110">However, it is not visible in a reporting client field list.</span></span> <span data-ttu-id="8c99c-111">Berekende kolommen en metingen die al dan niet zijn opgenomen in een perspectief, kunnen nog steeds werken met uitgesloten objectgegevens.</span><span class="sxs-lookup"><span data-stu-id="8c99c-111">Calculated columns and measures either included in a perspective or not can still calculate from object data that is excluded.</span></span>  
  
<span data-ttu-id="8c99c-112">Hallo-doel van deze les is toodescribe hoe toocreate perspectieven en vertrouwd raken met het model in tabelvorm Hallo hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="8c99c-112">hello purpose of this lesson is toodescribe how toocreate perspectives and become familiar with hello tabular model authoring tools.</span></span> <span data-ttu-id="8c99c-113">Als u later in dit model tooinclude aanvullende tabellen uitvouwt, kunt u meer perspectieven toodefine verschillende standpunten van Hallo model bijvoorbeeld inventaris en verkoop.</span><span class="sxs-lookup"><span data-stu-id="8c99c-113">If you later expand this model tooinclude additional tables, you can create additional perspectives toodefine different viewpoints of hello model, for example, Inventory and Sales.</span></span>  
  
<span data-ttu-id="8c99c-114">Geschatte tijd toocomplete deze les: **vijf minuten**</span><span class="sxs-lookup"><span data-stu-id="8c99c-114">Estimated time toocomplete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="8c99c-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8c99c-115">Prerequisites</span></span>  
<span data-ttu-id="8c99c-116">Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8c99c-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="8c99c-117">Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 7: Key Performance Indicators maken](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="8c99c-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  
  
## <a name="create-perspectives"></a><span data-ttu-id="8c99c-118">Perspectieven maken</span><span class="sxs-lookup"><span data-stu-id="8c99c-118">Create perspectives</span></span>  
  
#### <a name="toocreate-an-internet-sales-perspective"></a><span data-ttu-id="8c99c-119">toocreate een verkoop van de Internet-perspectief</span><span class="sxs-lookup"><span data-stu-id="8c99c-119">toocreate an Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="8c99c-120">Klik op Hallo **Model** menu > **perspectieven** > **maken en beheren**.</span><span class="sxs-lookup"><span data-stu-id="8c99c-120">Click hello **Model** menu > **Perspectives** > **Create and Manage**.</span></span>  
  
2.  <span data-ttu-id="8c99c-121">In Hallo **perspectieven** in het dialoogvenster, klikt u op **nieuw perspectief**.</span><span class="sxs-lookup"><span data-stu-id="8c99c-121">In hello **Perspectives** dialog box, click **New Perspective**.</span></span>  
  
3.  <span data-ttu-id="8c99c-122">Dubbelklik op Hallo **nieuw perspectief** kolomkop te klikken en vervolgens rename **Internet verkoop**.</span><span class="sxs-lookup"><span data-stu-id="8c99c-122">Double-click hello **New Perspective** column heading, and then rename **Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="8c99c-123">Selecteer alle Hallo tabellen Hallo *behalve* **DimCustomer**.</span><span class="sxs-lookup"><span data-stu-id="8c99c-123">Select hello all hello tables *except* **DimCustomer**.</span></span>  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    <span data-ttu-id="8c99c-125">In een latere les gebruikt u Hallo analyseren in Excel functie tootest dit perspectief wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8c99c-125">In a later lesson, you use hello Analyze in Excel feature tootest this perspective.</span></span> <span data-ttu-id="8c99c-126">Hallo lijst Excel PivotTable-velden bevat elke tabel behalve Hallo DimCustomer tabel.</span><span class="sxs-lookup"><span data-stu-id="8c99c-126">hello Excel PivotTable Fields List includes each table except hello DimCustomer table.</span></span>  

## <a name="whats-next"></a><span data-ttu-id="8c99c-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8c99c-127">What's next?</span></span>
<span data-ttu-id="8c99c-128">[Les 9: Hiërarchieën maken](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="8c99c-128">[Lesson 9: Create hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>
  
  
  
  
