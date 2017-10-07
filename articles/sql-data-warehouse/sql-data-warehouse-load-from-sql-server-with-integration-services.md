---
title: aaaLoad gegevens uit SQL Server in Azure SQL Data Warehouse (SSIS) | Microsoft Docs
description: Ziet u hoe toocreate SQL Server Integration Services (SSIS) toomove pakketgegevens uit een scala aan gegevensbronnen tooSQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e2c252e9-0828-47c2-a808-e3bea46c134a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/30/2017
ms.author: cakarst;douglasl;barbkess
ms.openlocfilehash: bb28a08807a5b07832b85f2f074c2acf912c1dc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a><span data-ttu-id="a58de-103">Laden van gegevens uit SQL Server in Azure SQL Data Warehouse (SSIS)</span><span class="sxs-lookup"><span data-stu-id="a58de-103">Load data from SQL Server into Azure SQL Data Warehouse (SSIS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a58de-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="a58de-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="a58de-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="a58de-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="a58de-106">bcp</span><span class="sxs-lookup"><span data-stu-id="a58de-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="a58de-107">SQL Server Integration Services (SSIS) tooload pakketgegevens van SQL Server maken in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a58de-107">Create a SQL Server Integration Services (SSIS) package tooload data from SQL Server into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="a58de-108">U kunt eventueel herstructureren, transformeren en opschonen Hallo gegevens als het Hallo SSIS-gegevensstroom passeert.</span><span class="sxs-lookup"><span data-stu-id="a58de-108">You can optionally restructure, transform, and cleanse hello data as it passes through hello SSIS data flow.</span></span>

<span data-ttu-id="a58de-109">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="a58de-109">In this tutorial, you will:</span></span>

* <span data-ttu-id="a58de-110">Maak een nieuwe Integration Services-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a58de-110">Create a new Integration Services project in Visual Studio.</span></span>
* <span data-ttu-id="a58de-111">Verbinding maken met toodata bronnen, met inbegrip van SQL Server (als een bron) en SQL Data Warehouse (als doel).</span><span class="sxs-lookup"><span data-stu-id="a58de-111">Connect toodata sources, including SQL Server (as a source) and SQL Data Warehouse (as a destination).</span></span>
* <span data-ttu-id="a58de-112">Ontwerp een SSIS-pakket dat gegevens worden geladen van bron Hallo in Hallo bestemming.</span><span class="sxs-lookup"><span data-stu-id="a58de-112">Design an SSIS package that loads data from hello source into hello destination.</span></span>
* <span data-ttu-id="a58de-113">Hallo SSIS tooload Hallo Pakketgegevens worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a58de-113">Run hello SSIS package tooload hello data.</span></span>

<span data-ttu-id="a58de-114">Deze zelfstudie gebruikt SQL Server als Hallo-gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="a58de-114">This tutorial uses SQL Server as hello data source.</span></span> <span data-ttu-id="a58de-115">SQL Server kan on-premises of in Azure een virtuele machine worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a58de-115">SQL Server could be running on premises or in an Azure virtual machine.</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="a58de-116">Basisconcepten</span><span class="sxs-lookup"><span data-stu-id="a58de-116">Basic concepts</span></span>
<span data-ttu-id="a58de-117">Hallo-pakket is Hallo werkeenheid in SSIS.</span><span class="sxs-lookup"><span data-stu-id="a58de-117">hello package is hello unit of work in SSIS.</span></span> <span data-ttu-id="a58de-118">Verwante pakketten worden gegroepeerd in projecten.</span><span class="sxs-lookup"><span data-stu-id="a58de-118">Related packages are grouped in projects.</span></span> <span data-ttu-id="a58de-119">U maken projecten en ontwerp pakketten in Visual Studio met SQL Server Data Tools.</span><span class="sxs-lookup"><span data-stu-id="a58de-119">You create projects and design packages in Visual Studio with SQL Server Data Tools.</span></span> <span data-ttu-id="a58de-120">Hallo-ontwerp proces is een visual proces waarin u slepen en neerzetten van onderdelen van Hallo werkset toohello ontwerpoppervlak ze verbinding maken en hun eigenschappen instellen.</span><span class="sxs-lookup"><span data-stu-id="a58de-120">hello design process is a visual process in which you drag and drop components from hello Toolbox toohello design surface, connect them, and set their properties.</span></span> <span data-ttu-id="a58de-121">Nadat u het pakket, kunt u eventueel implementeren tooSQL Server voor uitgebreide beheer, bewaking en beveiliging.</span><span class="sxs-lookup"><span data-stu-id="a58de-121">After you finish your package, you can optionally deploy it tooSQL Server for comprehensive management, monitoring, and security.</span></span>

## <a name="options-for-loading-data-with-ssis"></a><span data-ttu-id="a58de-122">Opties voor het laden van gegevens met SSIS</span><span class="sxs-lookup"><span data-stu-id="a58de-122">Options for loading data with SSIS</span></span>
<span data-ttu-id="a58de-123">SQL Server Integration Services (SSIS) is een flexibele set hulpprogramma's waarmee een groot aantal opties voor verbinding met en gegevens in SQL Data Warehouse te laden.</span><span class="sxs-lookup"><span data-stu-id="a58de-123">SQL Server Integration Services (SSIS) is a flexible set of tools that provides a variety of options for connecting to, and loading data into, SQL Data Warehouse.</span></span>

1. <span data-ttu-id="a58de-124">Gebruik een ADO NET bestemming tooconnect tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a58de-124">Use an ADO NET Destination tooconnect tooSQL Data Warehouse.</span></span> <span data-ttu-id="a58de-125">Deze zelfstudie wordt een ADO NET doel omdat het minste aantal configuratieopties Hallo heeft.</span><span class="sxs-lookup"><span data-stu-id="a58de-125">This tutorial uses an ADO NET Destination because it has hello fewest configuration options.</span></span>
2. <span data-ttu-id="a58de-126">Gebruik een OLE DB-bestemming tooconnect tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a58de-126">Use an OLE DB Destination tooconnect tooSQL Data Warehouse.</span></span> <span data-ttu-id="a58de-127">Deze optie kan enigszins betere prestaties dan Hallo ADO NET bestemming bieden.</span><span class="sxs-lookup"><span data-stu-id="a58de-127">This option may provide slightly better performance than hello ADO NET Destination.</span></span>
3. <span data-ttu-id="a58de-128">Hello Azure Blob uploaden taak toostage Hallo gegevens in Azure Blob Storage gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a58de-128">Use hello Azure Blob Upload Task toostage hello data in Azure Blob Storage.</span></span> <span data-ttu-id="a58de-129">Gebruik vervolgens Hallo SQL uitvoeren van SSIS taak toolaunch een Polybase-script dat Hallo gegevens in SQL Data Warehouse laadt.</span><span class="sxs-lookup"><span data-stu-id="a58de-129">Then use hello SSIS Execute SQL task toolaunch a Polybase script that loads hello data into SQL Data Warehouse.</span></span> <span data-ttu-id="a58de-130">Deze optie biedt de beste prestaties Hallo van Hallo drie opties die hier worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="a58de-130">This option provides hello best performance of hello three options listed here.</span></span> <span data-ttu-id="a58de-131">tooget hello Azure Blob uploaden taak downloaden Hallo [Microsoft SQL Server 2016 Integration Services Feature Pack voor Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure].</span><span class="sxs-lookup"><span data-stu-id="a58de-131">tooget hello Azure Blob Upload task, download hello [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure].</span></span> <span data-ttu-id="a58de-132">toolearn meer informatie over Polybase, Zie [PolyBase-handleiding][PolyBase Guide].</span><span class="sxs-lookup"><span data-stu-id="a58de-132">toolearn more about Polybase, see [PolyBase Guide][PolyBase Guide].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="a58de-133">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="a58de-133">Before you start</span></span>
<span data-ttu-id="a58de-134">toostep voor deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="a58de-134">toostep through this tutorial, you need:</span></span>

1. <span data-ttu-id="a58de-135">**SQL Server integratieservices (SSIS)**.</span><span class="sxs-lookup"><span data-stu-id="a58de-135">**SQL Server Integration Services (SSIS)**.</span></span> <span data-ttu-id="a58de-136">SSIS is een onderdeel van SQL Server en een evaluatieversie of een gelicentieerde versie van SQL Server vereist.</span><span class="sxs-lookup"><span data-stu-id="a58de-136">SSIS is a component of SQL Server and requires an evaluation version or a licensed version of SQL Server.</span></span> <span data-ttu-id="a58de-137">Zie voor een evaluatieversie van SQL Server 2016 Preview tooget [SQL Server-evaluaties][SQL Server Evaluations].</span><span class="sxs-lookup"><span data-stu-id="a58de-137">tooget an evaluation version of SQL Server 2016 Preview, see [SQL Server Evaluations][SQL Server Evaluations].</span></span>
2. <span data-ttu-id="a58de-138">**Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="a58de-138">**Visual Studio**.</span></span> <span data-ttu-id="a58de-139">tooget Hallo gratis Visual Studio Community Edition, Zie [Visual Studio Community][Visual Studio Community].</span><span class="sxs-lookup"><span data-stu-id="a58de-139">tooget hello free Visual Studio Community Edition, see [Visual Studio Community][Visual Studio Community].</span></span>
3. <span data-ttu-id="a58de-140">**SQL Server Data Tools voor Visual Studio (SSDT)**.</span><span class="sxs-lookup"><span data-stu-id="a58de-140">**SQL Server Data Tools for Visual Studio (SSDT)**.</span></span> <span data-ttu-id="a58de-141">tooget SQL Server Data Tools voor Visual Studio, Zie [Download SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].</span><span class="sxs-lookup"><span data-stu-id="a58de-141">tooget SQL Server Data Tools for Visual Studio, see [Download SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].</span></span>
4. <span data-ttu-id="a58de-142">**Voorbeeldgegevens**.</span><span class="sxs-lookup"><span data-stu-id="a58de-142">**Sample data**.</span></span> <span data-ttu-id="a58de-143">Deze zelfstudie wordt opgeslagen in SQL Server in de AdventureWorks voorbeelddatabase Hallo het Hallo bron gegevens toobe geladen in SQL Data Warehouse voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="a58de-143">This tutorial uses sample data stored in SQL Server in hello AdventureWorks sample database as hello source data toobe loaded into SQL Data Warehouse.</span></span> <span data-ttu-id="a58de-144">Zie tooget Hallo AdventureWorks-voorbeelddatabase [AdventureWorks 2014 voorbeeld Databases][AdventureWorks 2014 Sample Databases].</span><span class="sxs-lookup"><span data-stu-id="a58de-144">tooget hello AdventureWorks sample database, see [AdventureWorks 2014 Sample Databases][AdventureWorks 2014 Sample Databases].</span></span>
5. <span data-ttu-id="a58de-145">**Een SQL Data Warehouse-database en machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="a58de-145">**A SQL Data Warehouse database and permissions**.</span></span> <span data-ttu-id="a58de-146">Deze zelfstudie verbindt tooa SQL Data Warehouse-exemplaar en gegevens worden geladen in de App.</span><span class="sxs-lookup"><span data-stu-id="a58de-146">This tutorial connects tooa SQL Data Warehouse instance and loads data into it.</span></span> <span data-ttu-id="a58de-147">U hebt een tabel en tooload data toohave machtigingen toocreate.</span><span class="sxs-lookup"><span data-stu-id="a58de-147">You have toohave permissions toocreate a table and tooload data.</span></span>
6. <span data-ttu-id="a58de-148">**Een firewallregel**.</span><span class="sxs-lookup"><span data-stu-id="a58de-148">**A firewall rule**.</span></span> <span data-ttu-id="a58de-149">U hebt toocreate een firewallregel op SQL Data Warehouse met Hallo IP-adres van uw lokale computer voordat u gegevens toohello SQL Data Warehouse kunt uploaden.</span><span class="sxs-lookup"><span data-stu-id="a58de-149">You have toocreate a firewall rule on SQL Data Warehouse with hello IP address of your local computer before you can upload data toohello SQL Data Warehouse.</span></span>

## <a name="step-1-create-a-new-integration-services-project"></a><span data-ttu-id="a58de-150">Stap 1: Maak een nieuw project voor de Integration Services</span><span class="sxs-lookup"><span data-stu-id="a58de-150">Step 1: Create a new Integration Services project</span></span>
1. <span data-ttu-id="a58de-151">Visual Studio starten.</span><span class="sxs-lookup"><span data-stu-id="a58de-151">Launch Visual Studio.</span></span>
2. <span data-ttu-id="a58de-152">Op Hallo **bestand** selecteert u **nieuw | Project**.</span><span class="sxs-lookup"><span data-stu-id="a58de-152">On hello **File** menu, select **New | Project**.</span></span>
3. <span data-ttu-id="a58de-153">Navigeer toohello **geïnstalleerde | Sjablonen | Business Intelligence | Integratieservices** projecttypen.</span><span class="sxs-lookup"><span data-stu-id="a58de-153">Navigate toohello **Installed | Templates | Business Intelligence | Integration Services** project types.</span></span>
4. <span data-ttu-id="a58de-154">Selecteer **Integration Services-Project**.</span><span class="sxs-lookup"><span data-stu-id="a58de-154">Select **Integration Services Project**.</span></span> <span data-ttu-id="a58de-155">Waarden opgeven voor **naam** en **locatie**, en selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="a58de-155">Provide values for **Name** and **Location**, and then select **OK**.</span></span>

<span data-ttu-id="a58de-156">Visual Studio wordt geopend en wordt een nieuw project voor de Integration Services (SSIS) gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a58de-156">Visual Studio opens and creates a new Integration Services (SSIS) project.</span></span> <span data-ttu-id="a58de-157">Visual Studio wordt geopend Hallo ontwerpfunctie voor Hallo één nieuwe SSIS-pakket (Package.dtsx) in Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="a58de-157">Then Visual Studio opens hello designer for hello single new SSIS package (Package.dtsx) in hello project.</span></span> <span data-ttu-id="a58de-158">U ziet Hallo schermgebieden te volgen:</span><span class="sxs-lookup"><span data-stu-id="a58de-158">You see hello following screen areas:</span></span>

* <span data-ttu-id="a58de-159">Aan de linkerkant Hallo Hallo **werkset** van SSIS-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="a58de-159">On hello left, hello **Toolbox** of SSIS components.</span></span>
* <span data-ttu-id="a58de-160">Hallo ontwerpoppervlak met meerdere tabbladen in het Hallo-midden.</span><span class="sxs-lookup"><span data-stu-id="a58de-160">In hello middle, hello design surface, with multiple tabs.</span></span> <span data-ttu-id="a58de-161">Doorgaans gebruikt u ten minste Hallo **controlestroom** en Hallo **gegevensstroom** tabbladen.</span><span class="sxs-lookup"><span data-stu-id="a58de-161">You typically use at least hello **Control Flow** and hello **Data Flow** tabs.</span></span>
* <span data-ttu-id="a58de-162">Op de juiste hello, Hallo **Solution Explorer** en Hallo **eigenschappen** deelvensters.</span><span class="sxs-lookup"><span data-stu-id="a58de-162">On hello right, hello **Solution Explorer** and hello **Properties** panes.</span></span>
  
    ![][01]

## <a name="step-2-create-hello-basic-data-flow"></a><span data-ttu-id="a58de-163">Stap 2: Basic Hallo-gegevensstroom maken</span><span class="sxs-lookup"><span data-stu-id="a58de-163">Step 2: Create hello basic data flow</span></span>
1. <span data-ttu-id="a58de-164">Sleep een taak gegevens stromen van Hallo werkset toohello midden van het ontwerpoppervlak hello (op Hallo **controlestroom** tabblad).</span><span class="sxs-lookup"><span data-stu-id="a58de-164">Drag a Data Flow Task from hello Toolbox toohello center of hello design surface (on hello **Control Flow** tab).</span></span>
   
    ![][02]
2. <span data-ttu-id="a58de-165">Dubbelklik op Hallo gegevens stromen tooswitch toohello gegevensstroom tabblad taak.</span><span class="sxs-lookup"><span data-stu-id="a58de-165">Double-click hello Data Flow Task tooswitch toohello Data Flow tab.</span></span>
3. <span data-ttu-id="a58de-166">Hallo lijst van de andere bronnen in Hallo werkset, Sleep een ADO.NET bron toohello-ontwerpoppervlak.</span><span class="sxs-lookup"><span data-stu-id="a58de-166">From hello Other Sources list in hello Toolbox, drag an ADO.NET Source toohello design surface.</span></span> <span data-ttu-id="a58de-167">Met de Hallo bron-adapter is nog steeds is geselecteerd, ook de naam ervan wijzigen**SQL Server-bron** in Hallo **eigenschappen** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="a58de-167">With hello source adapter still selected, change its name too**SQL Server source** in hello **Properties** pane.</span></span>
4. <span data-ttu-id="a58de-168">Sleep een ADO.NET bestemming toohello ontwerpoppervlak onder Hallo ADO.NET-bron van Hallo andere bestemmingen lijst in Hallo werkset.</span><span class="sxs-lookup"><span data-stu-id="a58de-168">From hello Other Destinations list in hello Toolbox, drag an ADO.NET Destination toohello design surface under hello ADO.NET Source.</span></span> <span data-ttu-id="a58de-169">Met de Hallo-doeladapter nog steeds is geselecteerd, ook de naam ervan wijzigen**SQL DW bestemming** in Hallo **eigenschappen** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="a58de-169">With hello destination adapter still selected, change its name too**SQL DW destination** in hello **Properties** pane.</span></span>
   
    ![][09]

## <a name="step-3-configure-hello-source-adapter"></a><span data-ttu-id="a58de-170">Stap 3: Configureer Hallo bron adapter</span><span class="sxs-lookup"><span data-stu-id="a58de-170">Step 3: Configure hello source adapter</span></span>
1. <span data-ttu-id="a58de-171">Dubbelklik op Hallo bron adapter tooopen hello **ADO.NET bron Editor**.</span><span class="sxs-lookup"><span data-stu-id="a58de-171">Double-click hello source adapter tooopen hello **ADO.NET Source Editor**.</span></span>
   
    ![][03]
2. <span data-ttu-id="a58de-172">Op Hallo **Verbindingsbeheer** tabblad Hallo **ADO.NET bron Editor**, klikt u op Hallo **nieuw** knop volgende toohello **ADO.NET Verbindingsbeheer**lijst tooopen hello **ADO.NET Verbindingsbeheer configureren** dialoogvenster en te maken van de verbindingsinstellingen voor Hallo SQL Server-database waarin gegevens voor deze zelfstudie worden geladen.</span><span class="sxs-lookup"><span data-stu-id="a58de-172">On hello **Connection Manager** tab of hello **ADO.NET Source Editor**, click hello **New** button next toohello **ADO.NET connection manager** list tooopen hello **Configure ADO.NET Connection Manager** dialog box and create connection settings for hello SQL Server database from which this tutorial loads data.</span></span>
   
    ![][04]
3. <span data-ttu-id="a58de-173">In Hallo **ADO.NET Verbindingsbeheer configureren** dialoogvenster vak, klikt u op Hallo **nieuw** knop tooopen hello **Verbindingsbeheer** dialoogvenster vak en maak een nieuwe verbinding.</span><span class="sxs-lookup"><span data-stu-id="a58de-173">In hello **Configure ADO.NET Connection Manager** dialog box, click hello **New** button tooopen hello **Connection Manager** dialog box and create a new data connection.</span></span>
   
    ![][05]
4. <span data-ttu-id="a58de-174">In Hallo **Verbindingsbeheer** dialoogvenster vak, de volgende dingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="a58de-174">In hello **Connection Manager** dialog box, do hello following things.</span></span>
   
   1. <span data-ttu-id="a58de-175">Voor **Provider**, selecteer Hallo SqlClient-gegevensprovider.</span><span class="sxs-lookup"><span data-stu-id="a58de-175">For **Provider**, select hello SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="a58de-176">Voor **servernaam**, Voer Hallo SQL Server-naam.</span><span class="sxs-lookup"><span data-stu-id="a58de-176">For **Server name**, enter hello SQL Server name.</span></span>
   3. <span data-ttu-id="a58de-177">In Hallo **toohello server aanmelden** sectie Selecteer of typ de verificatiegegevens.</span><span class="sxs-lookup"><span data-stu-id="a58de-177">In hello **Log on toohello server** section, select or enter authentication information.</span></span>
   4. <span data-ttu-id="a58de-178">In Hallo **Connect tooa database** sectie, selecteert u Hallo AdventureWorks-voorbeelddatabase.</span><span class="sxs-lookup"><span data-stu-id="a58de-178">In hello **Connect tooa database** section, select hello AdventureWorks sample database.</span></span>
   5. <span data-ttu-id="a58de-179">Klik op **verbinding testen**.</span><span class="sxs-lookup"><span data-stu-id="a58de-179">Click **Test Connection**.</span></span>
      
       ![][06]
   6. <span data-ttu-id="a58de-180">Klik in het dialoogvenster Hallo Hallo resultaten van de verbindingstest Hallo rapporten, **OK** tooreturn toohello **Verbindingsbeheer** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a58de-180">In hello dialog box that reports hello results of hello connection test, click **OK** tooreturn toohello **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="a58de-181">In Hallo **Connection Manager** in het dialoogvenster, klikt u op **OK** tooreturn toohello **ADO.NET Verbindingsbeheer configureren** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a58de-181">In hello **Connection Manager** dialog box, click **OK** tooreturn toohello **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="a58de-182">In Hallo **ADO.NET Verbindingsbeheer configureren** in het dialoogvenster, klikt u op **OK** tooreturn toohello **ADO.NET gegevensbron bewerken**.</span><span class="sxs-lookup"><span data-stu-id="a58de-182">In hello **Configure ADO.NET Connection Manager** dialog box, click **OK** tooreturn toohello **ADO.NET Source Editor**.</span></span>
6. <span data-ttu-id="a58de-183">In Hallo **ADO.NET bron Editor**, in Hallo **naam van Hallo tabel of weergave Hallo** lijst, selecteer Hallo **Sales.SalesOrderDetail** tabel.</span><span class="sxs-lookup"><span data-stu-id="a58de-183">In hello **ADO.NET Source Editor**, in hello **Name of hello table or hello view** list, select hello **Sales.SalesOrderDetail** table.</span></span>
   
    ![][07]
7. <span data-ttu-id="a58de-184">Klik op **Preview** toosee eerste 200 rijen met gegevens in de brontabel Hallo in Hallo Hallo **Preview queryresultaten** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a58de-184">Click **Preview** toosee hello first 200 rows of data in hello source table in hello **Preview Query Results** dialog box.</span></span>
   
    ![][08]
8. <span data-ttu-id="a58de-185">In Hallo **Preview queryresultaten** in het dialoogvenster klikt u op **sluiten** tooreturn toohello **ADO.NET bron Editor**.</span><span class="sxs-lookup"><span data-stu-id="a58de-185">In hello **Preview Query Results** dialog box, click **Close** tooreturn toohello **ADO.NET Source Editor**.</span></span>
9. <span data-ttu-id="a58de-186">In Hallo **ADO.NET bron Editor**, klikt u op **OK** toofinish configureren Hallo-gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="a58de-186">In hello **ADO.NET Source Editor**, click **OK** toofinish configuring hello data source.</span></span>

## <a name="step-4-connect-hello-source-adapter-toohello-destination-adapter"></a><span data-ttu-id="a58de-187">Stap 4: Verbinding maken met de Hallo bron adapter toohello-doeladapter</span><span class="sxs-lookup"><span data-stu-id="a58de-187">Step 4: Connect hello source adapter toohello destination adapter</span></span>
1. <span data-ttu-id="a58de-188">Selecteer de bron-adapter Hallo op Hallo ontwerpoppervlak.</span><span class="sxs-lookup"><span data-stu-id="a58de-188">Select hello source adapter on hello design surface.</span></span>
2. <span data-ttu-id="a58de-189">Selecteer Hallo blauwe pijl die uitgebreider is dan uit de bron-adapter Hallo en sleep deze toohello bestemming editor totdat deze wordt uitgelijnd naar de juiste plaats.</span><span class="sxs-lookup"><span data-stu-id="a58de-189">Select hello blue arrow that extends from hello source adapter and drag it toohello destination editor until it snaps into place.</span></span>
   
    ![][10]
   
    <span data-ttu-id="a58de-190">Een aantal andere onderdelen van Hallo SSIS-werkset Between Hallo bron en Hallo bestemming toorestructure, transformatie gebruiken in een typische SSIS-pakketten en gegevens verwijderen als het Hallo SSIS-gegevensstroom passeert.</span><span class="sxs-lookup"><span data-stu-id="a58de-190">In a typical SSIS package, you use a number of other components from hello SSIS Toolbox in between hello source and hello destination toorestructure, transform, and cleanse your data as it passes through hello SSIS data flow.</span></span> <span data-ttu-id="a58de-191">tookeep in dit voorbeeld zo eenvoudig mogelijk we verbinden Hallo bron rechtstreeks toohello doel.</span><span class="sxs-lookup"><span data-stu-id="a58de-191">tookeep this example as simple as possible, we’re connecting hello source directly toohello destination.</span></span>

## <a name="step-5-configure-hello-destination-adapter"></a><span data-ttu-id="a58de-192">Stap 5: Hallo-doeladapter configureren</span><span class="sxs-lookup"><span data-stu-id="a58de-192">Step 5: Configure hello destination adapter</span></span>
1. <span data-ttu-id="a58de-193">Dubbelklik op Hallo bestemming adapter tooopen hello **ADO.NET bestemming Editor**.</span><span class="sxs-lookup"><span data-stu-id="a58de-193">Double-click hello destination adapter tooopen hello **ADO.NET Destination Editor**.</span></span>
   
    ![][11]
2. <span data-ttu-id="a58de-194">Op Hallo **Verbindingsbeheer** tabblad Hallo **ADO.NET bestemming Editor**, klikt u op Hallo **nieuw** knop volgende toohello **Verbindingsbeheer**lijst tooopen hello **ADO.NET Verbindingsbeheer configureren** dialoogvenster en te maken van de verbindingsinstellingen voor hello Azure SQL Data Warehouse-database waarin gegevens voor deze zelfstudie worden geladen.</span><span class="sxs-lookup"><span data-stu-id="a58de-194">On hello **Connection Manager** tab of hello **ADO.NET Destination Editor**, click hello **New** button next toohello **Connection manager** list tooopen hello **Configure ADO.NET Connection Manager** dialog box and create connection settings for hello Azure SQL Data Warehouse database into which this tutorial loads data.</span></span>
3. <span data-ttu-id="a58de-195">In Hallo **ADO.NET Verbindingsbeheer configureren** dialoogvenster vak, klikt u op Hallo **nieuw** knop tooopen hello **Verbindingsbeheer** dialoogvenster vak en maak een nieuwe verbinding.</span><span class="sxs-lookup"><span data-stu-id="a58de-195">In hello **Configure ADO.NET Connection Manager** dialog box, click hello **New** button tooopen hello **Connection Manager** dialog box and create a new data connection.</span></span>
4. <span data-ttu-id="a58de-196">In Hallo **Verbindingsbeheer** dialoogvenster vak, de volgende dingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="a58de-196">In hello **Connection Manager** dialog box, do hello following things.</span></span>
   1. <span data-ttu-id="a58de-197">Voor **Provider**, selecteer Hallo SqlClient-gegevensprovider.</span><span class="sxs-lookup"><span data-stu-id="a58de-197">For **Provider**, select hello SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="a58de-198">Voor **servernaam**, Hallo SQL Data Warehouse naam invoeren.</span><span class="sxs-lookup"><span data-stu-id="a58de-198">For **Server name**, enter hello SQL Data Warehouse name.</span></span>
   3. <span data-ttu-id="a58de-199">In Hallo **toohello server aanmelden** sectie **Gebruik SQL Server-verificatie** en voer de verificatiegegevens.</span><span class="sxs-lookup"><span data-stu-id="a58de-199">In hello **Log on toohello server** section, select **Use SQL Server authentication** and enter authentication information.</span></span>
   4. <span data-ttu-id="a58de-200">In Hallo **Connect tooa database** sectie, selecteer een bestaande SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="a58de-200">In hello **Connect tooa database** section, select an existing SQL Data Warehouse database.</span></span>
   5. <span data-ttu-id="a58de-201">Klik op **verbinding testen**.</span><span class="sxs-lookup"><span data-stu-id="a58de-201">Click **Test Connection**.</span></span>
   6. <span data-ttu-id="a58de-202">Klik in het dialoogvenster Hallo Hallo resultaten van de verbindingstest Hallo rapporten, **OK** tooreturn toohello **Verbindingsbeheer** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a58de-202">In hello dialog box that reports hello results of hello connection test, click **OK** tooreturn toohello **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="a58de-203">In Hallo **Connection Manager** in het dialoogvenster, klikt u op **OK** tooreturn toohello **ADO.NET Verbindingsbeheer configureren** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a58de-203">In hello **Connection Manager** dialog box, click **OK** tooreturn toohello **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="a58de-204">In Hallo **ADO.NET Verbindingsbeheer configureren** in het dialoogvenster, klikt u op **OK** tooreturn toohello **ADO.NET bestemming Editor**.</span><span class="sxs-lookup"><span data-stu-id="a58de-204">In hello **Configure ADO.NET Connection Manager** dialog box, click **OK** tooreturn toohello **ADO.NET Destination Editor**.</span></span>
6. <span data-ttu-id="a58de-205">In Hallo **ADO.NET bestemming Editor**, klikt u op **nieuw** volgende toohello **gebruik van een tabel of weergave** lijst tooopen hello **Create Table** in het dialoogvenster een nieuwe bestemming tabel met een kolomlijst die overeenkomt met de brontabel Hallo toocreate.</span><span class="sxs-lookup"><span data-stu-id="a58de-205">In hello **ADO.NET Destination Editor**, click **New** next toohello **Use a table or view** list tooopen hello **Create Table** dialog box toocreate a new destination table with a column list that matches hello source table.</span></span>
   
    ![][12a]
7. <span data-ttu-id="a58de-206">In Hallo **Create Table** dialoogvenster vak, de volgende dingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="a58de-206">In hello **Create Table** dialog box, do hello following things.</span></span>
   
   1. <span data-ttu-id="a58de-207">Hallo-naam van de doeltabel Hallo ook wijzigen**verkooporderdetail**.</span><span class="sxs-lookup"><span data-stu-id="a58de-207">Change hello name of hello destination table too**SalesOrderDetail**.</span></span>
   2. <span data-ttu-id="a58de-208">Hallo verwijderen **rowguid** kolom.</span><span class="sxs-lookup"><span data-stu-id="a58de-208">Remove hello **rowguid** column.</span></span> <span data-ttu-id="a58de-209">Hallo **uniqueidentifier** gegevenstype wordt niet ondersteund in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a58de-209">hello **uniqueidentifier** data type is not supported in SQL Data Warehouse.</span></span>
   3. <span data-ttu-id="a58de-210">Wijzig het gegevenstype Hallo Hallo **LineTotal** kolom te**geld**.</span><span class="sxs-lookup"><span data-stu-id="a58de-210">Change hello data type of hello **LineTotal** column too**money**.</span></span> <span data-ttu-id="a58de-211">Hallo **decimale** gegevenstype wordt niet ondersteund in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a58de-211">hello **decimal** data type is not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="a58de-212">Zie voor informatie over de ondersteunde gegevenstypen [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].</span><span class="sxs-lookup"><span data-stu-id="a58de-212">For info about supported data types, see [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].</span></span>
      
       ![][12b]
   4. <span data-ttu-id="a58de-213">Klik op **OK** toocreate Hallo tabel en keer terug toohello **ADO.NET bestemming Editor**.</span><span class="sxs-lookup"><span data-stu-id="a58de-213">Click **OK** toocreate hello table and return toohello **ADO.NET Destination Editor**.</span></span>
8. <span data-ttu-id="a58de-214">In Hallo **ADO.NET bestemming Editor**, selecteer Hallo **toewijzingen** tabblad toosee toocolumns in Hallo doel hoe kolommen in bron Hallo zijn toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a58de-214">In hello **ADO.NET Destination Editor**, select hello **Mappings** tab toosee how columns in hello source are mapped toocolumns in hello destination.</span></span>
   
    ![][13]
9. <span data-ttu-id="a58de-215">Klik op **OK** toofinish configureren Hallo-gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="a58de-215">Click **OK** toofinish configuring hello data source.</span></span>

## <a name="step-6-run-hello-package-tooload-hello-data"></a><span data-ttu-id="a58de-216">Stap 6: Tooload Hallo-Hallo pakketgegevens uitvoeren</span><span class="sxs-lookup"><span data-stu-id="a58de-216">Step 6: Run hello package tooload hello data</span></span>
<span data-ttu-id="a58de-217">Voer Hallo-pakket door te klikken op Hallo **Start** knop op Hallo werkbalk of door een hello te selecteren **uitvoeren** opties op Hallo **Debug** menu.</span><span class="sxs-lookup"><span data-stu-id="a58de-217">Run hello package by clicking hello **Start** button on hello toolbar or by selecting one of hello **Run** options on hello **Debug** menu.</span></span>

<span data-ttu-id="a58de-218">Als het pakket Hallo begint toorun, ziet u gele draaiende wheels tooindicate activiteit, evenals het aantal rijen verwerkt tot nu toe Hallo.</span><span class="sxs-lookup"><span data-stu-id="a58de-218">As hello package begins toorun, you see yellow spinning wheels tooindicate activity as well as hello number of rows processed so far.</span></span>

![][14]

<span data-ttu-id="a58de-219">Wanneer het Hallo-pakket is voltooid, u groen vinkje tooindicate geslaagd Zie evenals Hallo totale aantal rijen met gegevens die worden geladen vanuit Hallo bron toohello doel.</span><span class="sxs-lookup"><span data-stu-id="a58de-219">When hello package has finished running, you see green check marks tooindicate success as well as hello total number of rows of data loaded from hello source toohello destination.</span></span>

![][15]

<span data-ttu-id="a58de-220">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="a58de-220">Congratulations!</span></span> <span data-ttu-id="a58de-221">U hebt de gegevens van SQL Server Integration Services tooload is gebruikt in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a58de-221">You’ve successfully used SQL Server Integration Services tooload data into Azure SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a58de-222">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a58de-222">Next steps</span></span>
* <span data-ttu-id="a58de-223">Meer informatie over Hallo SSIS-gegevensstroom.</span><span class="sxs-lookup"><span data-stu-id="a58de-223">Learn more about hello SSIS data flow.</span></span> <span data-ttu-id="a58de-224">Begin hier: [gegevensstroom][Data Flow].</span><span class="sxs-lookup"><span data-stu-id="a58de-224">Start here: [Data Flow][Data Flow].</span></span>
* <span data-ttu-id="a58de-225">Meer informatie over hoe toodebug en uw recht pakketten in de ontwerpomgeving Hallo oplossen.</span><span class="sxs-lookup"><span data-stu-id="a58de-225">Learn how toodebug and troubleshoot your packages right in hello design environment.</span></span> <span data-ttu-id="a58de-226">Begin hier: [hulpprogramma's voor het oplossen van problemen voor de ontwikkeling van pakket][Troubleshooting Tools for Package Development].</span><span class="sxs-lookup"><span data-stu-id="a58de-226">Start here: [Troubleshooting Tools for Package Development][Troubleshooting Tools for Package Development].</span></span>
* <span data-ttu-id="a58de-227">Meer informatie over hoe toodeploy uw SSIS-projecten en pakketten tooIntegration Services-Server of tooanother opslaglocatie.</span><span class="sxs-lookup"><span data-stu-id="a58de-227">Learn how toodeploy your SSIS projects and packages tooIntegration Services Server or tooanother storage location.</span></span> <span data-ttu-id="a58de-228">Begin hier: [van implementatieprojecten en pakketten][Deployment of Projects and Packages].</span><span class="sxs-lookup"><span data-stu-id="a58de-228">Start here: [Deployment of Projects and Packages][Deployment of Projects and Packages].</span></span>

<!-- Image references -->
[01]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-designer-01.png
[02]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-data-flow-task-02.png
[03]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-03.png
[04]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-manager-04.png
[05]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-05.png
[06]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/test-connection-06.png
[07]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-07.png
[08]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/preview-data-08.png
[09]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/source-destination-09.png
[10]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/connect-source-destination-10.png
[11]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-destination-11.png
[12a]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-before-12a.png
[12b]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-after-12b.png
[13]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/column-mapping-13.png
[14]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-running-14.png
[15]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: https://msdn.microsoft.com/library/mt143171.aspx
[Download SQL Server Data Tools (SSDT)]: https://msdn.microsoft.com/library/mt204009.aspx
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: https://msdn.microsoft.com/library/mt203953.aspx
[Data Flow]: https://msdn.microsoft.com/library/ms140080.aspx
[Troubleshooting Tools for Package Development]: https://msdn.microsoft.com/library/ms137625.aspx
[Deployment of Projects and Packages]: https://msdn.microsoft.com/library/hh213290.aspx

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://msftdbprodsamples.codeplex.com/releases/view/125550
