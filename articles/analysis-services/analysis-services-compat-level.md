---
title: Gegevensmodel compatibiliteitsniveau in Azure Analysis Services | Microsoft Docs
description: Understanding tabelgegevens model compatibiliteitsniveau.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/16/2017
ms.author: owend
ms.openlocfilehash: b11ba54c2cdc2675ec535368e7076613a5290212
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a><span data-ttu-id="0020a-103">Het compatibiliteitsniveau voor Analysis Services-modellen in tabelvorm</span><span class="sxs-lookup"><span data-stu-id="0020a-103">Compatibility level for Analysis Services tabular models</span></span>

<span data-ttu-id="0020a-104">*Het compatibiliteitsniveau* verwijst naar de release-specifieke gedrag in de Analysis Services-engine.</span><span class="sxs-lookup"><span data-stu-id="0020a-104">*Compatibility level* refers to release-specific behaviors in the Analysis Services engine.</span></span> <span data-ttu-id="0020a-105">Wijzigingen in het compatibiliteitsniveau wordt doorgaans samenvallen met belangrijke releases van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0020a-105">Changes to the compatibility level typically coincide with major releases of SQL Server.</span></span> <span data-ttu-id="0020a-106">Deze wijzigingen zijn ook geïmplementeerd in Azure Analysis Services onderhouden pariteit tussen beide platforms.</span><span class="sxs-lookup"><span data-stu-id="0020a-106">These changes are also implemented in Azure Analysis Services to maintain parity between both platforms.</span></span> <span data-ttu-id="0020a-107">Compatibiliteit niveau wijzigingen zijn ook van invloed op functies die beschikbaar zijn in uw modellen in tabelvorm.</span><span class="sxs-lookup"><span data-stu-id="0020a-107">Compatibility level changes also affect features available in your tabular models.</span></span> <span data-ttu-id="0020a-108">Bijvoorbeeld, hebben DirectQuery en metagegevens in tabelvorm object verschillende implementaties, afhankelijk van het compatibiliteitsniveau.</span><span class="sxs-lookup"><span data-stu-id="0020a-108">For example, DirectQuery and tabular object metadata have different implementations depending on the compatibility level.</span></span> 

<span data-ttu-id="0020a-109">Azure Analysis Services biedt ondersteuning voor tabelmodellen op het niveau van de compatibiliteit 1200 en 1400.</span><span class="sxs-lookup"><span data-stu-id="0020a-109">Azure Analysis Services supports tabular models at the 1200 and 1400 compatibility levels.</span></span>

<span data-ttu-id="0020a-110">Het compatibiliteitsniveau van de meest recente is 1400.</span><span class="sxs-lookup"><span data-stu-id="0020a-110">The latest compatibility level is 1400.</span></span> <span data-ttu-id="0020a-111">Dit niveau samenvalt met SQL Server 2017 Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="0020a-111">This level coincides with SQL Server 2017 Analysis Services.</span></span> <span data-ttu-id="0020a-112">Belangrijke functies in het compatibiliteitsniveau 1400:</span><span class="sxs-lookup"><span data-stu-id="0020a-112">Major features in the 1400 compatibility level include:</span></span>

*  <span data-ttu-id="0020a-113">Nieuwe infrastructuur voor toegang tot gegevens en importeren in modellen in tabelvorm met ondersteuning voor TOM APIs en TMSL scripting.</span><span class="sxs-lookup"><span data-stu-id="0020a-113">New infrastructure for data connectivity and import into tabular models with support for TOM APIs and TMSL scripting.</span></span> <span data-ttu-id="0020a-114">Deze nieuwe functie biedt ondersteuning voor extra gegevensbronnen zoals Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="0020a-114">This new feature enables support for additional data sources such as Azure Blob storage.</span></span>
*  <span data-ttu-id="0020a-115">Gegevenstransformatie en gegevens mashup mogelijkheden met behulp van expressies gegevens ophalen en M.</span><span class="sxs-lookup"><span data-stu-id="0020a-115">Data transformation and data mashup capabilities by using Get Data and M expressions.</span></span>
*  <span data-ttu-id="0020a-116">Metingen ondersteuning voor een eigenschap detailrijen met een DAX-expressie.</span><span class="sxs-lookup"><span data-stu-id="0020a-116">Measures support a Detail Rows property with a DAX expression.</span></span> <span data-ttu-id="0020a-117">Deze eigenschap kunt clienthulpprogramma's zoals Microsoft Excel om in te zoomen naar beneden gedetailleerde gegevens van een samengevoegde lijst.</span><span class="sxs-lookup"><span data-stu-id="0020a-117">This property enables client tools like Microsoft Excel to drill down to detailed data from an aggregated report.</span></span> <span data-ttu-id="0020a-118">Bijvoorbeeld, wanneer gebruikers totale verkoop voor een regio en de maand bekijken, kunnen ze de details van de bijbehorende bekijken.</span><span class="sxs-lookup"><span data-stu-id="0020a-118">For example, when users view total sales for a region and month, they can view the associated order details.</span></span> 
*  <span data-ttu-id="0020a-119">Beveiliging op objectniveau voor tabel- en kolomnamen, naast de gegevens daarin.</span><span class="sxs-lookup"><span data-stu-id="0020a-119">Object-level security for table and column names, in addition to the data within them.</span></span>
*  <span data-ttu-id="0020a-120">Verbeterde ondersteuning voor niet-aaneengesloten hiërarchieën.</span><span class="sxs-lookup"><span data-stu-id="0020a-120">Enhanced support for ragged hierarchies.</span></span>
*  <span data-ttu-id="0020a-121">Bewaking van prestaties en verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="0020a-121">Performance and monitoring improvements.</span></span>
  
## <a name="set-compatibility-level"></a><span data-ttu-id="0020a-122">Het compatibiliteitsniveau instellen</span><span class="sxs-lookup"><span data-stu-id="0020a-122">Set compatibility level</span></span> 
 <span data-ttu-id="0020a-123">Wanneer u een nieuw model in tabelvorm-project in SSDT, kunt u het compatibiliteitsniveau opgeven op de **model in tabelvorm designer** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0020a-123">When creating a new tabular model project in SSDT, you can specify the compatibility level on the **Tabular model designer** dialog.</span></span> 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 <span data-ttu-id="0020a-125">Als u selecteert de **dit bericht niet meer weergeven** optie, alle volgende projecten gebruik van het compatibiliteitsniveau die u hebt opgegeven als de standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="0020a-125">If you select the **Do not show this message again** option, all subsequent projects use the compatibility level you specified as the default.</span></span> <span data-ttu-id="0020a-126">U kunt het standaardniveau voor compatibiliteit in SSDT in wijzigen **extra** > **opties**.</span><span class="sxs-lookup"><span data-stu-id="0020a-126">You can change the default compatibility level in SSDT in **Tools** > **Options**.</span></span>  
  
 <span data-ttu-id="0020a-127">Om een upgrade van een bestaand project model in tabelvorm in SSDT, te stellen de **compatibiliteitsniveau** eigenschap in het model **eigenschappen** venster.</span><span class="sxs-lookup"><span data-stu-id="0020a-127">To upgrade an existing tabular model project in SSDT, set  the **Compatibility Level** property in the model **Properties** window.</span></span> <span data-ttu-id="0020a-128">Houd in gedachten, upgraden van het compatibiliteitsniveau wordt niet ongedaan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0020a-128">Keep in-mind, upgrading the compatibility level is irreversible.</span></span>
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a><span data-ttu-id="0020a-129">Controleer het compatibiliteitsniveau voor een tabellaire modeldatabase in SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="0020a-129">Check compatibility level for a tabular model database in SQL Server Management Studio</span></span> 
 <span data-ttu-id="0020a-130">SSMS, met de rechtermuisknop op de databasenaam > **eigenschappen** > **compatibiliteitsniveau**.</span><span class="sxs-lookup"><span data-stu-id="0020a-130">In SSMS, right-click the database name > **Properties** > **Compatibility Level**.</span></span>  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a><span data-ttu-id="0020a-131">Controleer het compatibiliteitsniveau van de ondersteunde versies voor een server in SSMS</span><span class="sxs-lookup"><span data-stu-id="0020a-131">Check supported compatibility level for a server in SSMS</span></span>  
 <span data-ttu-id="0020a-132">SSMS, met de rechtermuisknop op de servernaam > **eigenschappen** > **compatibiliteitsniveau ondersteund**.</span><span class="sxs-lookup"><span data-stu-id="0020a-132">In SSMS, right-click the server name>  **Properties** > **Supported Compatibility Level**.</span></span>  
  
 <span data-ttu-id="0020a-133">Deze eigenschap geeft het hoogste compatibiliteitsniveau van een database die wordt uitgevoerd op de server (met uitzondering van de preview).</span><span class="sxs-lookup"><span data-stu-id="0020a-133">This property specifies the highest compatibility level of a database that will run on the server (excluding preview).</span></span> <span data-ttu-id="0020a-134">Het compatibiliteitsniveau van de ondersteunde kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="0020a-134">The supported compatibility level cannot be changed.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="0020a-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0020a-135">Next steps</span></span>
  <span data-ttu-id="0020a-136">[Een model maken in Azure portal](analysis-services-create-model-portal.md) </span><span class="sxs-lookup"><span data-stu-id="0020a-136">[Create a model in Azure portal](analysis-services-create-model-portal.md) </span></span>  
  [<span data-ttu-id="0020a-137">Analyseservices beheren</span><span class="sxs-lookup"><span data-stu-id="0020a-137">Manage Analysis Services</span></span>](analysis-services-manage.md)  
