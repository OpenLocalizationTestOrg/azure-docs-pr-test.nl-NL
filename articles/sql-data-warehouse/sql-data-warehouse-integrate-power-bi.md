---
title: aaaUse Power BI met SQL Data Warehouse | Microsoft Docs
description: Tips voor het gebruik van Power BI met Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: a3a347493d07af6824a561567f05894cfe3c0471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a><span data-ttu-id="96933-103">Power BI gebruiken met SQL datawarehouse</span><span class="sxs-lookup"><span data-stu-id="96933-103">Use Power BI with SQL Data Warehouse</span></span>
<span data-ttu-id="96933-104">Met de Azure SQL Database kunt SQL Data Warehouse Direct verbinding maken gebruiker tooleverage krachtige logische naar beneden duwen naast Hallo analytische functies van Power BI.</span><span class="sxs-lookup"><span data-stu-id="96933-104">As with Azure SQL Database, SQL Data Warehouse Direct Connect allows user tooleverage powerful logical pushdown alongside hello analytical capabilities of Power BI.</span></span>  <span data-ttu-id="96933-105">Met Direct Connect's query verzonden back tooyour Azure SQL Data Warehouse in realtime als u Hallo gegevens verkennen.</span><span class="sxs-lookup"><span data-stu-id="96933-105">With Direct Connect, queries are sent back tooyour Azure SQL Data Warehouse in real time as you explore hello data.</span></span>  <span data-ttu-id="96933-106">Deze, in combinatie met de schaal Hallo van SQL Data Warehouse, kunnen gebruikers toocreate dynamische rapporten in minuten op basis van terabytes aan gegevens.</span><span class="sxs-lookup"><span data-stu-id="96933-106">This, combined with hello scale of SQL Data Warehouse, enables users toocreate dynamic reports in minutes against terabytes of data.</span></span>  <span data-ttu-id="96933-107">Bovendien Hallo introductie van Hallo openen in Power BI-knop kan gebruikers toodirectly verbinding maken met Power BI tootheir SQL Data Warehouse zonder gegevens te verzamelen uit andere delen van Azure.</span><span class="sxs-lookup"><span data-stu-id="96933-107">In addition, hello introduction of hello Open in Power BI button allows users toodirectly connect Power BI tootheir SQL Data Warehouse without collecting information from other parts of Azure.</span></span>

<span data-ttu-id="96933-108">Als u Direct Connect Ga Opmerking:</span><span class="sxs-lookup"><span data-stu-id="96933-108">When using Direct Connect please note:</span></span>

* <span data-ttu-id="96933-109">Geef de volledig gekwalificeerde servernaam Hallo wanneer verbinding wordt gemaakt (Zie hieronder voor meer informatie)</span><span class="sxs-lookup"><span data-stu-id="96933-109">Specify hello fully qualified server name when connecting (see below for more details)</span></span>
* <span data-ttu-id="96933-110">Zorg ervoor dat de firewallregels voor Hallo database zijn geconfigureerd te 'toestaan toegang tooAzure services'.</span><span class="sxs-lookup"><span data-stu-id="96933-110">Ensure firewall rules for hello database are configured too"Allow access tooAzure services".</span></span>
* <span data-ttu-id="96933-111">Elke actie zoals een kolom selecteren of een filter toe te voegen rechtstreeks een query uit op Hallo-datawarehouse</span><span class="sxs-lookup"><span data-stu-id="96933-111">Every action such as selecting a column or adding a filter will  directly query hello data warehouse</span></span>
* <span data-ttu-id="96933-112">Tegels worden vernieuwd ongeveer elke 15 minuten (vernieuwen hoeft geen toobe gepland)</span><span class="sxs-lookup"><span data-stu-id="96933-112">Tiles are refreshed approximately every 15 minutes (refresh does not need toobe scheduled)</span></span>
* <span data-ttu-id="96933-113">Met Q & A is niet beschikbaar voor gegevenssets die Direct Connect</span><span class="sxs-lookup"><span data-stu-id="96933-113">Q&A is not available for Direct Connect datasets</span></span>
* <span data-ttu-id="96933-114">Wijzigingen in het schema worden niet automatisch opgepikt</span><span class="sxs-lookup"><span data-stu-id="96933-114">Schema changes are not picked up automatically</span></span>
* <span data-ttu-id="96933-115">Alle Direct verbinding maken met query's na 2 minuten</span><span class="sxs-lookup"><span data-stu-id="96933-115">All Direct Connect queries will time out after 2 minutes</span></span>

<span data-ttu-id="96933-116">Deze beperkingen en -opmerkingen kunnen wijzigen, omdat wij tooimprove Hallo ervaringen.</span><span class="sxs-lookup"><span data-stu-id="96933-116">These restrictions and notes may change as we continue tooimprove hello experiences.</span></span> <span data-ttu-id="96933-117">Hallo stappen tooconnect worden hieronder beschreven.</span><span class="sxs-lookup"><span data-stu-id="96933-117">hello steps tooconnect are detailed below.</span></span>  

## <a name="using-hello-open-in-power-bi-button"></a><span data-ttu-id="96933-118">Met behulp van 'Openen in Power BI' Hallo-knop</span><span class="sxs-lookup"><span data-stu-id="96933-118">Using hello ‘Open in Power BI’ button</span></span>
<span data-ttu-id="96933-119">Hallo gemakkelijkste manier toomove tussen uw SQL Data Warehouse en Power BI is met hello openen in Power BI-knop.</span><span class="sxs-lookup"><span data-stu-id="96933-119">hello easiest way toomove between your SQL Data Warehouse and Power BI is with hello Open in Power BI button.</span></span> <span data-ttu-id="96933-120">Deze knop kunt u tooseamlessly beginnen met het maken van nieuwe dashboards in Power BI.</span><span class="sxs-lookup"><span data-stu-id="96933-120">This button allows you tooseamlessly begin creating new dashboards in Power BI.</span></span>  

1. <span data-ttu-id="96933-121">tooget gestart Navigeer tooyour SQL Data Warehouse-exemplaar in Hallo klassieke Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="96933-121">tooget started navigate tooyour SQL Data Warehouse instance in hello Azure Classic Portal.</span></span>
2. <span data-ttu-id="96933-122">Klik op 'Openen in Power BI' Hallo-knop.</span><span class="sxs-lookup"><span data-stu-id="96933-122">Click hello 'Open in Power BI' button.</span></span>
3. <span data-ttu-id="96933-123">Als we niet kunnen toosign u rechtstreeks, of als u een Power BI-account niet hebt, moet u toosign in.</span><span class="sxs-lookup"><span data-stu-id="96933-123">If we are not able toosign you in directly, or if you do not have a Power BI account, you will need toosign-in.</span></span>  
4. <span data-ttu-id="96933-124">U wordt omgeleid toohello SQL Data Warehouse verbindingspagina met de Hallo gegevens van uw SQL Data Warehouse vooraf worden ingevuld.</span><span class="sxs-lookup"><span data-stu-id="96933-124">You will be directed toohello SQL Data Warehouse connection page, with hello information from your SQL Data Warehouse pre-populated.</span></span>
5. <span data-ttu-id="96933-125">Na het invoeren van uw referenties kunt u zich volledig verbonden tooyour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="96933-125">After entering your credentials you will be fully connected tooyour SQL Data Warehouse.</span></span>

## <a name="connecting-through-hello-power-bi-portal"></a><span data-ttu-id="96933-126">Verbinding maken via Hallo Power BI-portal</span><span class="sxs-lookup"><span data-stu-id="96933-126">Connecting through hello Power BI portal</span></span>
<span data-ttu-id="96933-127">In toevoeging toousing Hallo openen in Power BI-knop, kunnen gebruikers ook tootheir SQL Data Warehouse communiceren via Hallo Power BI-Portal.</span><span class="sxs-lookup"><span data-stu-id="96933-127">In addition toousing hello Open in Power BI button, users can also connect tootheir SQL Data Warehouse through hello Power BI Portal.</span></span>

1. <span data-ttu-id="96933-128">Klik op gegevens ophalen Hallo Hallo navigatiedeelvenster onderaan in.</span><span class="sxs-lookup"><span data-stu-id="96933-128">Click 'Get Data' at hello bottom of hello navigation pane.</span></span>
2. <span data-ttu-id="96933-129">Selecteer 'Databases'.</span><span class="sxs-lookup"><span data-stu-id="96933-129">Select 'Databases'.</span></span>
3. <span data-ttu-id="96933-130">Selecteer één keer op Hallo Databases pagina 'Azure SQL Data Warehouse' en klik op 'Connect'.</span><span class="sxs-lookup"><span data-stu-id="96933-130">Once on hello Databases page, select 'Azure SQL Data Warehouse' and then click 'Connect'.</span></span>
4. <span data-ttu-id="96933-131">Voer de noodzakelijke verbindingsgegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="96933-131">Enter hello necessary connection information.</span></span>  <span data-ttu-id="96933-132">De servernaam en databasenaam vindt u in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="96933-132">Your server name and database name can be found in hello Azure Portal.</span></span>
5. <span data-ttu-id="96933-133">U wordt omgeleid terug hoofdpagina toohello van Power BI en nadat de verbinding wordt gemaakt van een nieuwe vermelding onder 'Gegevenssets' wordt weergegeven met de naam van uw exemplaar Hallo.</span><span class="sxs-lookup"><span data-stu-id="96933-133">You will be directed back toohello main page of Power BI and after your connection is made a new entry under 'Datasets' will appear with hello name of your instance.</span></span>  
6. <span data-ttu-id="96933-134">U kunt klikken op de nieuwe gegevensset tooexplore Hallo alle Hallo tabellen en weergaven in de database.</span><span class="sxs-lookup"><span data-stu-id="96933-134">You can click on hello new dataset tooexplore all of hello tables and views in your database.</span></span> <span data-ttu-id="96933-135">Als u een kolom selecteert, stuurt query back toohello bron, het visuele element dynamisch te maken.</span><span class="sxs-lookup"><span data-stu-id="96933-135">Selecting a column will send a query back toohello source, dynamically creating your visual.</span></span> <span data-ttu-id="96933-136">Deze visuele elementen kunnen worden opgeslagen in een nieuw rapport en vastgemaakt terug tooyour dashboard.</span><span class="sxs-lookup"><span data-stu-id="96933-136">These visuals can be saved in a new report and pinned back tooyour dashboard.</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
