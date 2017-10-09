---
title: aaaUse Redgate tooload gegevens tooyour Azure datawarehouse | Microsoft Docs
description: Meer informatie over hoe de toouse Redgate gegevens Platform Studio voor datawarehousescenario's.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 6082390c07c8ffa73ebd8ab272ace00ba8bb1897
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a><span data-ttu-id="fb518-103">Gegevens laden met behulp van Data Platform Studio van Redgate</span><span class="sxs-lookup"><span data-stu-id="fb518-103">Load data with Redgate Data Platform Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb518-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="fb518-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)
> * [<span data-ttu-id="fb518-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="fb518-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [<span data-ttu-id="fb518-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="fb518-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)
> * [<span data-ttu-id="fb518-107">BCP</span><span class="sxs-lookup"><span data-stu-id="fb518-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="fb518-108">Deze zelfstudie leert u hoe toouse [Redgate van gegevens Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DP's) toomove gegevens uit een lokale SQL Server tooAzure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fb518-108">This tutorial shows you how toouse [Redgate's Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) toomove data from an on-premises SQL Server tooAzure SQL Data Warehouse.</span></span> <span data-ttu-id="fb518-109">Gegevens Platform Studio past u het meest geschikte compatibiliteit oplossingen Hallo en optimalisatie, dus het snelst Hallo manier tooget gestart met SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fb518-109">Data Platform Studio applies hello most appropriate compatibility fixes and optimizations, so it's hello quickest way tooget started with SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="fb518-110">[Redgate](http://www.red-gate.com) is al lange tijd een Microsoft-partner en levert verschillende SQL Server-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="fb518-110">[Redgate](http://www.red-gate.com) is a long-time Microsoft partner that delivers various SQL Server tools.</span></span> <span data-ttu-id="fb518-111">Deze functie in DPS is gratis beschikbaar voor commercieel en niet-commercieel gebruik.</span><span class="sxs-lookup"><span data-stu-id="fb518-111">This feature in Data Platform Studio has been made available freely for both commercial and non-commercial use.</span></span>
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="fb518-112">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="fb518-112">Before you begin</span></span>
### <a name="create-or-identify-resources"></a><span data-ttu-id="fb518-113">Resources maken of identificeren</span><span class="sxs-lookup"><span data-stu-id="fb518-113">Create or identify resources</span></span>
<span data-ttu-id="fb518-114">Voordat u deze zelfstudie begint, moet u toohave:</span><span class="sxs-lookup"><span data-stu-id="fb518-114">Before starting this tutorial, you need toohave:</span></span>

* <span data-ttu-id="fb518-115">**lokale SQL Server-Database**: gegevens die u wilt tooimport tooSQL Data Warehouse toocome van een lokale SQL Server moet Hallo (versie 2008 R2 of hoger).</span><span class="sxs-lookup"><span data-stu-id="fb518-115">**on-premises SQL Server Database**: hello data you want tooimport tooSQL Data Warehouse needs toocome from an on-premises SQL Server (version 2008R2 or above).</span></span> <span data-ttu-id="fb518-116">Met DPS kunnen gegevens niet rechtstreeks worden geïmporteerd uit een Azure SQL-database of uit tekstbestanden.</span><span class="sxs-lookup"><span data-stu-id="fb518-116">Data Platform Studio cannot import data directly from an Azure SQL Database or from text files.</span></span>
* <span data-ttu-id="fb518-117">**Azure Storage-Account**: Data Platform Studio bereidt Hallo-gegevens in Azure Blob Storage voordat deze worden geladen in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fb518-117">**Azure Storage Account**: Data Platform Studio stages hello data in Azure Blob Storage before loading it into SQL Data Warehouse.</span></span> <span data-ttu-id="fb518-118">Hallo storage-account moet gebruikmaken van Hallo ' Resource Manager '-implementatiemodel (standaard Hallo) in plaats van 'Klassiek' Hallo-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="fb518-118">hello storage account must be using hello “Resource Manager” deployment model (hello default) rather than hello “Classic” deployment model.</span></span> <span data-ttu-id="fb518-119">Als u geen storage-account hebt, Ontdek hoe tooCreate een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="fb518-119">If you don't have a storage account, learn how tooCreate a storage account.</span></span> 
* <span data-ttu-id="fb518-120">**SQL Data Warehouse**: in deze zelfstudie Hallo gegevens verplaatst van de lokale SQL Server tooSQL datawarehouse, zodat u toohave moet een datawarehouse online.</span><span class="sxs-lookup"><span data-stu-id="fb518-120">**SQL Data Warehouse**: This tutorial moves hello data from on-premises SQL Server tooSQL Data Warehouse, so you need toohave a data warehouse online.</span></span> <span data-ttu-id="fb518-121">Als u nog geen datawarehouse, Ontdek hoe tooCreate een Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fb518-121">If you do not already have a data warehouse, learn how tooCreate an Azure SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="fb518-122">De prestaties worden verbeterd als Hallo storage-account en Hallo datawarehouse worden gemaakt in Hallo dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="fb518-122">Performance is improved if hello storage account and hello data warehouse are created in hello same region.</span></span>
> 
> 

## <a name="step-1-sign-in-toodata-platform-studio-with-your-azure-account"></a><span data-ttu-id="fb518-123">Stap 1: Registreren in tooData Platform Studio met uw Azure-account</span><span class="sxs-lookup"><span data-stu-id="fb518-123">Step 1: Sign in tooData Platform Studio with your Azure account</span></span>
<span data-ttu-id="fb518-124">Open uw webbrowser en navigeer toohello [gegevens Platform Studio](https://www.dataplatformstudio.com/) website.</span><span class="sxs-lookup"><span data-stu-id="fb518-124">Open your web browser and navigate toohello [Data Platform Studio](https://www.dataplatformstudio.com/) website.</span></span> <span data-ttu-id="fb518-125">Aanmelden met Hallo dezelfde Azure-account die u gebruikte toocreate Hallo storage-account en het datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="fb518-125">Sign in with hello same Azure account that you used toocreate hello storage account and data warehouse.</span></span> <span data-ttu-id="fb518-126">Als uw e-mailadres gekoppeld aan een werk of schoolaccount en een Microsoft-account worden ervoor toochoose Hallo-account dat toegang tooyour bronnen heeft is.</span><span class="sxs-lookup"><span data-stu-id="fb518-126">If your email address is associated with both a work or school account and a Microsoft account, be sure toochoose hello account that has access tooyour resources.</span></span>

> [!NOTE]
> <span data-ttu-id="fb518-127">Als dit de eerste keer met gegevens Platform Studio, wordt u gevraagd toogrant Hallo toepassing machtiging toomanage uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="fb518-127">If this is your first time using Data Platform Studio, you are asked toogrant hello application permission toomanage your Azure resources.</span></span>
> 
> 

## <a name="step-2-start-hello-import-wizard"></a><span data-ttu-id="fb518-128">Stap 2: Start Hallo Wizard importeren</span><span class="sxs-lookup"><span data-stu-id="fb518-128">Step 2: Start hello Import Wizard</span></span>
<span data-ttu-id="fb518-129">Selecteer in de Hallo DP's hoofdvenster Hallo tooAzure SQL Data Warehouse koppeling toostart Hallo importeren wizard importeren.</span><span class="sxs-lookup"><span data-stu-id="fb518-129">From hello DPS main screen, select hello Import tooAzure SQL Data Warehouse link toostart hello import wizard.</span></span>

![][1]

## <a name="step-3-install-hello-data-platform-studio-gateway"></a><span data-ttu-id="fb518-130">Stap 3: Hallo gegevensgateway Platform Studio installeren</span><span class="sxs-lookup"><span data-stu-id="fb518-130">Step 3: Install hello Data Platform Studio Gateway</span></span>
<span data-ttu-id="fb518-131">tooconnect tooyour lokale SQL Server-database, moet u tooinstall Hallo DP's Gateway.</span><span class="sxs-lookup"><span data-stu-id="fb518-131">tooconnect tooyour on-premises SQL Server database, you need tooinstall hello DPS Gateway.</span></span> <span data-ttu-id="fb518-132">Hallo-gateway is een clientagent waarmee toegang tooyour lokale omgeving haalt gegevens op Hallo en geüpload tooyour storage-account.</span><span class="sxs-lookup"><span data-stu-id="fb518-132">hello gateway is a client agent that provides access tooyour on-premises environment, extracts hello data, and uploads it tooyour storage account.</span></span> <span data-ttu-id="fb518-133">De gegevens worden niet verwerkt op de servers van Redgate.</span><span class="sxs-lookup"><span data-stu-id="fb518-133">Your data never passes through Redgate’s servers.</span></span> <span data-ttu-id="fb518-134">tooinstall hello Gateway:</span><span class="sxs-lookup"><span data-stu-id="fb518-134">tooinstall hello Gateway:</span></span>

1. <span data-ttu-id="fb518-135">Klik op Hallo **Gateway maken** koppeling</span><span class="sxs-lookup"><span data-stu-id="fb518-135">Click hello **Create Gateway** link</span></span>
2. <span data-ttu-id="fb518-136">Downloaden en installeren Hallo Gateway met Hallo opgegeven installatieprogramma</span><span class="sxs-lookup"><span data-stu-id="fb518-136">Download and install hello Gateway using hello provided installer</span></span>

![][2]

> [!NOTE]
> <span data-ttu-id="fb518-137">Hallo Gateway kan worden geïnstalleerd op een machine met het netwerk toegang toohello bron SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="fb518-137">hello Gateway can be installed on any machine with network access toohello source SQL Server database.</span></span> <span data-ttu-id="fb518-138">Deze toegang heeft tot Hallo SQL Server-database met behulp van Windows-verificatie met referenties van de huidige gebruiker Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="fb518-138">It accesses hello SQL Server database using Windows authentication with hello credentials of hello current user.</span></span>
> 
> 

<span data-ttu-id="fb518-139">Na de installatie configureert Hallo Gateway status wijzigingen tooConnected en kunt u de volgende selecteren.</span><span class="sxs-lookup"><span data-stu-id="fb518-139">Once installed, hello Gateway status changes tooConnected and you can select Next.</span></span>

## <a name="step-4-identify-hello-source-database"></a><span data-ttu-id="fb518-140">Stap 4: De brondatabase Hallo identificeren</span><span class="sxs-lookup"><span data-stu-id="fb518-140">Step 4: Identify hello source database</span></span>
<span data-ttu-id="fb518-141">In Hallo *servernaam Voer* textbox, voer de naam Hallo van Hallo-server die als host fungeert voor uw database en selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="fb518-141">In hello *Enter Server Name* textbox, enter hello name of hello server that hosts your database and select **Next**.</span></span> <span data-ttu-id="fb518-142">Selecteer vervolgens uit de vervolgkeuzelijst hello, tooimport gegevens van gewenste Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="fb518-142">Then, from hello drop-down menu, select hello database you want tooimport data from.</span></span>

![][3]

<span data-ttu-id="fb518-143">DP's inspecteert de geselecteerde database Hallo voor tabellen tooimport.</span><span class="sxs-lookup"><span data-stu-id="fb518-143">DPS inspects hello selected database for tables tooimport.</span></span> <span data-ttu-id="fb518-144">Standaard wordt DP's alle Hallo tabellen in Hallo database geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="fb518-144">By default, DPS imports all hello tables in hello database.</span></span> <span data-ttu-id="fb518-145">U kunt selecteren of selectie opheffen tabellen door het uitbreiden van alle tabellen koppelen Hallo.</span><span class="sxs-lookup"><span data-stu-id="fb518-145">You can select or deselect tables by expanding hello All Tables link.</span></span> <span data-ttu-id="fb518-146">Selecteer Hallo volgende knop toomove doorsturen.</span><span class="sxs-lookup"><span data-stu-id="fb518-146">Select hello Next button toomove forward.</span></span>

## <a name="step-5-choose-a-storage-account-toostage-hello-data"></a><span data-ttu-id="fb518-147">Stap 5: Kies een storage account toostage Hallo-gegevens</span><span class="sxs-lookup"><span data-stu-id="fb518-147">Step 5: Choose a storage account toostage hello data</span></span>
<span data-ttu-id="fb518-148">DP's wordt u gevraagd een locatie toostage Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="fb518-148">DPS prompts you for a location toostage hello data.</span></span> <span data-ttu-id="fb518-149">Kies een bestaand opslagaccount in uw abonnement en selecteer **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="fb518-149">Choose an existing storage account from your subscription and select **Next**.</span></span>

> [!NOTE]
> <span data-ttu-id="fb518-150">DP's maakt een nieuwe blob-container in Hallo gekozen storage-account en een unieke map gebruiken voor elke importeren.</span><span class="sxs-lookup"><span data-stu-id="fb518-150">DPS will create a new blob container in hello chosen storage account and use a distinct folder for each import.</span></span>
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a><span data-ttu-id="fb518-151">Stap 6: Een datawarehouse selecteren</span><span class="sxs-lookup"><span data-stu-id="fb518-151">Step 6: Select a data warehouse</span></span>
<span data-ttu-id="fb518-152">Vervolgens selecteert u een online [Azure SQL Data Warehouse](http://aka.ms/sqldw) tooimport Hallo gegevens in de database.</span><span class="sxs-lookup"><span data-stu-id="fb518-152">Next, you select an online [Azure SQL Data Warehouse](http://aka.ms/sqldw) database tooimport hello data into.</span></span> <span data-ttu-id="fb518-153">Wanneer u de database hebt geselecteerd, moet u tooenter Hallo referenties tooconnect toohello database en selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="fb518-153">Once you've selected your database, you need tooenter hello credentials tooconnect toohello database and select **Next**.</span></span>

![][5]

> [!NOTE]
> <span data-ttu-id="fb518-154">DP's samengevoegd Hallo bron gegevenstabellen met Hallo-datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="fb518-154">DPS merges hello source data tables into hello data warehouse.</span></span> <span data-ttu-id="fb518-155">DP's waarschuwt u als Hallo tabelnaam dit vereist is voor de bestaande tabellen toooverwrite in Hallo datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="fb518-155">DPS warns you if hello table name requires it toooverwrite existing tables in hello data warehouse.</span></span> <span data-ttu-id="fb518-156">U kunt desgewenst verwijderen eventuele bestaande objecten in Hallo datawarehouse door te tikken verwijderen alle bestaande objecten voor de import.</span><span class="sxs-lookup"><span data-stu-id="fb518-156">You may optionally delete any existing objects in hello data warehouse by ticking Delete all existing objects before import.</span></span>
> 
> 

## <a name="step-7-import-hello-data"></a><span data-ttu-id="fb518-157">Stap 7: Hallo gegevens importeren</span><span class="sxs-lookup"><span data-stu-id="fb518-157">Step 7: Import hello data</span></span>
<span data-ttu-id="fb518-158">DP's wordt bevestigd dat u tooimport Hallo gegevens wilt.</span><span class="sxs-lookup"><span data-stu-id="fb518-158">DPS confirms that you would like tooimport hello data.</span></span> <span data-ttu-id="fb518-159">Klik op Hallo Start knop toobegin Hallo gegevens importeren.</span><span class="sxs-lookup"><span data-stu-id="fb518-159">Simply click hello Start import button toobegin hello data import.</span></span>

![][6]

<span data-ttu-id="fb518-160">DP's wordt weergegeven een visualisatie die Hallo voortgang geeft van het uitpakken en het uploaden van gegevens van Hallo van Hallo lokale SQL Server en Hallo voortgang van Hallo importeren in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fb518-160">DPS displays a visualization that shows hello progress of extracting and uploading hello data from hello on-premises SQL Server and hello progress of hello import into SQL Data Warehouse.</span></span>

![][7]

<span data-ttu-id="fb518-161">Zodra de Hallo importeren is voltooid, geeft een samenvatting van Hallo gegevens importeren en een rapport wijzigen van Hallo compatibiliteit met oplossingen die zijn uitgevoerd DP's weer.</span><span class="sxs-lookup"><span data-stu-id="fb518-161">Once hello import is complete, DPS displays a summary of hello data import and a change report of hello compatibility fixes that have been performed.</span></span>

![][8]

## <a name="next-steps"></a><span data-ttu-id="fb518-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fb518-162">Next steps</span></span>
<span data-ttu-id="fb518-163">tooexplore uw gegevens in SQL Data Warehouse opstarten weer te geven:</span><span class="sxs-lookup"><span data-stu-id="fb518-163">tooexplore your data within SQL Data Warehouse, start by viewing:</span></span>

* <span data-ttu-id="fb518-164">[Query’s uitvoeren bij Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span><span class="sxs-lookup"><span data-stu-id="fb518-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span></span>
* <span data-ttu-id="fb518-165">[Gegevens visualiseren met Power BI][Visualize data with Power BI]</span><span class="sxs-lookup"><span data-stu-id="fb518-165">[Visualize data with Power BI][Visualize data with Power BI]</span></span>

<span data-ttu-id="fb518-166">meer informatie over de Redgate gegevens Platform Studio toolearn:</span><span class="sxs-lookup"><span data-stu-id="fb518-166">toolearn more about Redgate’s Data Platform Studio:</span></span>

* [<span data-ttu-id="fb518-167">Ga naar de startpagina van Hallo DP 's</span><span class="sxs-lookup"><span data-stu-id="fb518-167">Visit hello DPS homepage</span></span>](http://www.dataplatformstudio.com/)
* [<span data-ttu-id="fb518-168">Bekijk een demonstratie van DPS op Channel 9</span><span class="sxs-lookup"><span data-stu-id="fb518-168">Watch a demo of DPS on Channel9</span></span>](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

<span data-ttu-id="fb518-169">Zie voor een overzicht van andere manieren toomigrate en load uw gegevens in SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="fb518-169">For an overview of other ways toomigrate and load your data in SQL Data Warehouse see:</span></span>

* <span data-ttu-id="fb518-170">[Uw oplossing tooSQL Data Warehouse migreren][Migrate your solution tooSQL Data Warehouse]</span><span class="sxs-lookup"><span data-stu-id="fb518-170">[Migrate your solution tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse]</span></span>
* <span data-ttu-id="fb518-171">[Load data into Azure SQL Data Warehouse](sql-data-warehouse-overview-load.md) (Gegevens laden in Azure SQL Data Warehouse)</span><span class="sxs-lookup"><span data-stu-id="fb518-171">[Load data into Azure SQL Data Warehouse](sql-data-warehouse-overview-load.md)</span></span>

<span data-ttu-id="fb518-172">Zie voor meer tips voor het ontwikkeling Hallo [overzicht van SQL Data Warehouse voor ontwikkelaars](sql-data-warehouse-overview-develop.md).</span><span class="sxs-lookup"><span data-stu-id="fb518-172">For more development tips, see hello [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution tooSQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
