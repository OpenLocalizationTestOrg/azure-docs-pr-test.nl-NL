---
title: aaaData model compatibiliteitsniveau in Azure Analysis Services | Microsoft Docs
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
ms.openlocfilehash: bfaf0c60666729d1e6e0baf082c046ea9faa4e86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a><span data-ttu-id="48508-103">Het compatibiliteitsniveau voor Analysis Services-modellen in tabelvorm</span><span class="sxs-lookup"><span data-stu-id="48508-103">Compatibility level for Analysis Services tabular models</span></span>

<span data-ttu-id="48508-104">*Het compatibiliteitsniveau* toorelease-specifieke gedrag in de Analysis Services-engine Hallo verwijst.</span><span class="sxs-lookup"><span data-stu-id="48508-104">*Compatibility level* refers toorelease-specific behaviors in hello Analysis Services engine.</span></span> <span data-ttu-id="48508-105">Wijzigingen toohello compatibiliteitsniveau wordt doorgaans samenvallen met belangrijke releases van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="48508-105">Changes toohello compatibility level typically coincide with major releases of SQL Server.</span></span> <span data-ttu-id="48508-106">Deze wijzigingen zijn ook geïmplementeerd in Azure Analysis Services toomaintain pariteit tussen beide platforms.</span><span class="sxs-lookup"><span data-stu-id="48508-106">These changes are also implemented in Azure Analysis Services toomaintain parity between both platforms.</span></span> <span data-ttu-id="48508-107">Compatibiliteit niveau wijzigingen zijn ook van invloed op functies die beschikbaar zijn in uw modellen in tabelvorm.</span><span class="sxs-lookup"><span data-stu-id="48508-107">Compatibility level changes also affect features available in your tabular models.</span></span> <span data-ttu-id="48508-108">Bijvoorbeeld, hebben DirectQuery en metagegevens in tabelvorm object verschillende implementaties, afhankelijk van het compatibiliteitsniveau Hallo.</span><span class="sxs-lookup"><span data-stu-id="48508-108">For example, DirectQuery and tabular object metadata have different implementations depending on hello compatibility level.</span></span> 

<span data-ttu-id="48508-109">Azure Analysis Services biedt ondersteuning voor tabelmodellen op Hallo 1200 en 1400 compatibiliteitsniveaus.</span><span class="sxs-lookup"><span data-stu-id="48508-109">Azure Analysis Services supports tabular models at hello 1200 and 1400 compatibility levels.</span></span>

<span data-ttu-id="48508-110">de meest recente compatibiliteitsniveau Hallo is 1400.</span><span class="sxs-lookup"><span data-stu-id="48508-110">hello latest compatibility level is 1400.</span></span> <span data-ttu-id="48508-111">Dit niveau samenvalt met SQL Server 2017 Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="48508-111">This level coincides with SQL Server 2017 Analysis Services.</span></span> <span data-ttu-id="48508-112">Belangrijke functies in Hallo 1400 compatibiliteitsniveau:</span><span class="sxs-lookup"><span data-stu-id="48508-112">Major features in hello 1400 compatibility level include:</span></span>

*  <span data-ttu-id="48508-113">Nieuwe infrastructuur voor toegang tot gegevens en importeren in modellen in tabelvorm met ondersteuning voor TOM APIs en TMSL scripting.</span><span class="sxs-lookup"><span data-stu-id="48508-113">New infrastructure for data connectivity and import into tabular models with support for TOM APIs and TMSL scripting.</span></span> <span data-ttu-id="48508-114">Deze nieuwe functie biedt ondersteuning voor extra gegevensbronnen zoals Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="48508-114">This new feature enables support for additional data sources such as Azure Blob storage.</span></span>
*  <span data-ttu-id="48508-115">Gegevenstransformatie en gegevens mashup mogelijkheden met behulp van expressies gegevens ophalen en M.</span><span class="sxs-lookup"><span data-stu-id="48508-115">Data transformation and data mashup capabilities by using Get Data and M expressions.</span></span>
*  <span data-ttu-id="48508-116">Metingen ondersteuning voor een eigenschap detailrijen met een DAX-expressie.</span><span class="sxs-lookup"><span data-stu-id="48508-116">Measures support a Detail Rows property with a DAX expression.</span></span> <span data-ttu-id="48508-117">Deze eigenschap kunt clienthulpprogramma's zoals Microsoft Excel toodrill omlaag toodetailed gegevens uit een samengevoegde lijst.</span><span class="sxs-lookup"><span data-stu-id="48508-117">This property enables client tools like Microsoft Excel toodrill down toodetailed data from an aggregated report.</span></span> <span data-ttu-id="48508-118">Wanneer gebruikers totale verkoop voor een regio en de maand bekijken, kunnen ze bijvoorbeeld Hallo gekoppeld ordergegevens bekijken.</span><span class="sxs-lookup"><span data-stu-id="48508-118">For example, when users view total sales for a region and month, they can view hello associated order details.</span></span> 
*  <span data-ttu-id="48508-119">Object beveiligingsniveau voor tabel- en kolomnamen benoemt bovendien toohello gegevens daarin.</span><span class="sxs-lookup"><span data-stu-id="48508-119">Object-level security for table and column names, in addition toohello data within them.</span></span>
*  <span data-ttu-id="48508-120">Verbeterde ondersteuning voor niet-aaneengesloten hiërarchieën.</span><span class="sxs-lookup"><span data-stu-id="48508-120">Enhanced support for ragged hierarchies.</span></span>
*  <span data-ttu-id="48508-121">Bewaking van prestaties en verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="48508-121">Performance and monitoring improvements.</span></span>
  
## <a name="set-compatibility-level"></a><span data-ttu-id="48508-122">Het compatibiliteitsniveau instellen</span><span class="sxs-lookup"><span data-stu-id="48508-122">Set compatibility level</span></span> 
 <span data-ttu-id="48508-123">Wanneer u een nieuw model in tabelvorm-project in SSDT, kunt u het compatibiliteitsniveau Hallo op Hallo **model in tabelvorm designer** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="48508-123">When creating a new tabular model project in SSDT, you can specify hello compatibility level on hello **Tabular model designer** dialog.</span></span> 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 <span data-ttu-id="48508-125">Als u Hallo selecteert **dit bericht niet meer weergeven** optie alle volgende projecten gebruiken Hallo compatibiliteitsniveau u hebt opgegeven als Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="48508-125">If you select hello **Do not show this message again** option, all subsequent projects use hello compatibility level you specified as hello default.</span></span> <span data-ttu-id="48508-126">U kunt wijzigen Hallo standaard compatibiliteitsniveau in SSDT in **extra** > **opties**.</span><span class="sxs-lookup"><span data-stu-id="48508-126">You can change hello default compatibility level in SSDT in **Tools** > **Options**.</span></span>  
  
 <span data-ttu-id="48508-127">een bestaand project model in tabelvorm in SSDT, set Hallo tooupgrade **compatibiliteitsniveau** eigenschap in Hallo model **eigenschappen** venster.</span><span class="sxs-lookup"><span data-stu-id="48508-127">tooupgrade an existing tabular model project in SSDT, set  hello **Compatibility Level** property in hello model **Properties** window.</span></span> <span data-ttu-id="48508-128">In rekening te houden, Hallo compatibiliteitsniveau upgraden is niet ongedaan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="48508-128">Keep in-mind, upgrading hello compatibility level is irreversible.</span></span>
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a><span data-ttu-id="48508-129">Controleer het compatibiliteitsniveau voor een tabellaire modeldatabase in SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="48508-129">Check compatibility level for a tabular model database in SQL Server Management Studio</span></span> 
 <span data-ttu-id="48508-130">SSMS, met de rechtermuisknop op Hallo-databasenaam > **eigenschappen** > **compatibiliteitsniveau**.</span><span class="sxs-lookup"><span data-stu-id="48508-130">In SSMS, right-click hello database name > **Properties** > **Compatibility Level**.</span></span>  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a><span data-ttu-id="48508-131">Controleer het compatibiliteitsniveau van de ondersteunde versies voor een server in SSMS</span><span class="sxs-lookup"><span data-stu-id="48508-131">Check supported compatibility level for a server in SSMS</span></span>  
 <span data-ttu-id="48508-132">SSMS, met de rechtermuisknop op Hallo-servernaam > **eigenschappen** > **compatibiliteitsniveau ondersteund**.</span><span class="sxs-lookup"><span data-stu-id="48508-132">In SSMS, right-click hello server name>  **Properties** > **Supported Compatibility Level**.</span></span>  
  
 <span data-ttu-id="48508-133">Deze eigenschap geeft Hallo hoogste compatibiliteitsniveau van een database die wordt uitgevoerd op Hallo-server (met uitzondering van de preview).</span><span class="sxs-lookup"><span data-stu-id="48508-133">This property specifies hello highest compatibility level of a database that will run on hello server (excluding preview).</span></span> <span data-ttu-id="48508-134">Hallo ondersteund compatibiliteitsniveau kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="48508-134">hello supported compatibility level cannot be changed.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="48508-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="48508-135">Next steps</span></span>
  <span data-ttu-id="48508-136">[Een model maken in Azure portal](analysis-services-create-model-portal.md) </span><span class="sxs-lookup"><span data-stu-id="48508-136">[Create a model in Azure portal](analysis-services-create-model-portal.md) </span></span>  
  [<span data-ttu-id="48508-137">Analyseservices beheren</span><span class="sxs-lookup"><span data-stu-id="48508-137">Manage Analysis Services</span></span>](analysis-services-manage.md)  
