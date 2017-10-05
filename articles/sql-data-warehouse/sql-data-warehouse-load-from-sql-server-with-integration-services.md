---
title: Laden van gegevens uit SQL Server in Azure SQL Data Warehouse (SSIS) | Microsoft Docs
description: Laat zien hoe u een pakket met SQL Server Integration Services (SSIS) om gegevens te verplaatsen van een groot aantal gegevensbronnen in SQL Data Warehouse maken.
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
ms.openlocfilehash: 6c9cebdd715b6997d0633bc725a3945ba9e0c357
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a><span data-ttu-id="27b19-103">Laden van gegevens uit SQL Server in Azure SQL Data Warehouse (SSIS)</span><span class="sxs-lookup"><span data-stu-id="27b19-103">Load data from SQL Server into Azure SQL Data Warehouse (SSIS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="27b19-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="27b19-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="27b19-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="27b19-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="27b19-106">bcp</span><span class="sxs-lookup"><span data-stu-id="27b19-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="27b19-107">Maak een pakket met SQL Server Integration Services (SSIS) om gegevens uit SQL Server laden in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="27b19-107">Create a SQL Server Integration Services (SSIS) package to load data from SQL Server into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="27b19-108">U kunt eventueel herstructureren, transformeren en opschonen van de gegevens als deze de SSIS-gegevensstroom passeert.</span><span class="sxs-lookup"><span data-stu-id="27b19-108">You can optionally restructure, transform, and cleanse the data as it passes through the SSIS data flow.</span></span>

<span data-ttu-id="27b19-109">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="27b19-109">In this tutorial, you will:</span></span>

* <span data-ttu-id="27b19-110">Maak een nieuwe Integration Services-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="27b19-110">Create a new Integration Services project in Visual Studio.</span></span>
* <span data-ttu-id="27b19-111">Verbinding maken met gegevensbronnen, met inbegrip van SQL Server (als een bron) en SQL Data Warehouse (als doel).</span><span class="sxs-lookup"><span data-stu-id="27b19-111">Connect to data sources, including SQL Server (as a source) and SQL Data Warehouse (as a destination).</span></span>
* <span data-ttu-id="27b19-112">Ontwerp een SSIS-pakket dat gegevens worden geladen van de bron naar doel.</span><span class="sxs-lookup"><span data-stu-id="27b19-112">Design an SSIS package that loads data from the source into the destination.</span></span>
* <span data-ttu-id="27b19-113">Voer de SSIS-pakket om de gegevens te laden.</span><span class="sxs-lookup"><span data-stu-id="27b19-113">Run the SSIS package to load the data.</span></span>

<span data-ttu-id="27b19-114">Deze zelfstudie gebruikt SQL Server als de gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="27b19-114">This tutorial uses SQL Server as the data source.</span></span> <span data-ttu-id="27b19-115">SQL Server kan on-premises of in Azure een virtuele machine worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="27b19-115">SQL Server could be running on premises or in an Azure virtual machine.</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="27b19-116">Basisconcepten</span><span class="sxs-lookup"><span data-stu-id="27b19-116">Basic concepts</span></span>
<span data-ttu-id="27b19-117">Het pakket is de werkeenheid in SSIS.</span><span class="sxs-lookup"><span data-stu-id="27b19-117">The package is the unit of work in SSIS.</span></span> <span data-ttu-id="27b19-118">Verwante pakketten worden gegroepeerd in projecten.</span><span class="sxs-lookup"><span data-stu-id="27b19-118">Related packages are grouped in projects.</span></span> <span data-ttu-id="27b19-119">U maken projecten en ontwerp pakketten in Visual Studio met SQL Server Data Tools.</span><span class="sxs-lookup"><span data-stu-id="27b19-119">You create projects and design packages in Visual Studio with SQL Server Data Tools.</span></span> <span data-ttu-id="27b19-120">Het ontwerpproces is een visual proces waarin u slepen en neerzetten van onderdelen uit de werkset naar het ontwerpoppervlak, koppelt u deze en hun eigenschappen instellen.</span><span class="sxs-lookup"><span data-stu-id="27b19-120">The design process is a visual process in which you drag and drop components from the Toolbox to the design surface, connect them, and set their properties.</span></span> <span data-ttu-id="27b19-121">Nadat u het pakket, kunt u eventueel deze implementeren op SQL Server voor uitgebreide beheer, bewaking en beveiliging.</span><span class="sxs-lookup"><span data-stu-id="27b19-121">After you finish your package, you can optionally deploy it to SQL Server for comprehensive management, monitoring, and security.</span></span>

## <a name="options-for-loading-data-with-ssis"></a><span data-ttu-id="27b19-122">Opties voor het laden van gegevens met SSIS</span><span class="sxs-lookup"><span data-stu-id="27b19-122">Options for loading data with SSIS</span></span>
<span data-ttu-id="27b19-123">SQL Server Integration Services (SSIS) is een flexibele set hulpprogramma's waarmee een groot aantal opties voor verbinding met en gegevens in SQL Data Warehouse te laden.</span><span class="sxs-lookup"><span data-stu-id="27b19-123">SQL Server Integration Services (SSIS) is a flexible set of tools that provides a variety of options for connecting to, and loading data into, SQL Data Warehouse.</span></span>

1. <span data-ttu-id="27b19-124">Gebruik een ADO NET doel verbinding maken met SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="27b19-124">Use an ADO NET Destination to connect to SQL Data Warehouse.</span></span> <span data-ttu-id="27b19-125">Deze zelfstudie wordt een ADO NET doel omdat deze het minste aantal configuratieopties.</span><span class="sxs-lookup"><span data-stu-id="27b19-125">This tutorial uses an ADO NET Destination because it has the fewest configuration options.</span></span>
2. <span data-ttu-id="27b19-126">Gebruik een OLE DB-doel verbinding maken met SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="27b19-126">Use an OLE DB Destination to connect to SQL Data Warehouse.</span></span> <span data-ttu-id="27b19-127">Deze optie kan enigszins betere prestaties dan het doel van ADO NET bieden.</span><span class="sxs-lookup"><span data-stu-id="27b19-127">This option may provide slightly better performance than the ADO NET Destination.</span></span>
3. <span data-ttu-id="27b19-128">Gebruik de Azure-taak voor het uploaden van Blob om voor te bereiden van de gegevens in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="27b19-128">Use the Azure Blob Upload Task to stage the data in Azure Blob Storage.</span></span> <span data-ttu-id="27b19-129">Gebruik vervolgens de SQL uitvoeren van SSIS-taak starten van een Polybase-script dat de gegevens worden geladen in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="27b19-129">Then use the SSIS Execute SQL task to launch a Polybase script that loads the data into SQL Data Warehouse.</span></span> <span data-ttu-id="27b19-130">Deze optie biedt de beste prestaties van de drie opties die hier worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="27b19-130">This option provides the best performance of the three options listed here.</span></span> <span data-ttu-id="27b19-131">Als u de taak Azure Blob uploaden, downloaden de [Microsoft SQL Server 2016 Integration Services Feature Pack voor Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure].</span><span class="sxs-lookup"><span data-stu-id="27b19-131">To get the Azure Blob Upload task, download the [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure].</span></span> <span data-ttu-id="27b19-132">Zie voor meer informatie over Polybase, [PolyBase-handleiding][PolyBase Guide].</span><span class="sxs-lookup"><span data-stu-id="27b19-132">To learn more about Polybase, see [PolyBase Guide][PolyBase Guide].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="27b19-133">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="27b19-133">Before you start</span></span>
<span data-ttu-id="27b19-134">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="27b19-134">To step through this tutorial, you need:</span></span>

1. <span data-ttu-id="27b19-135">**SQL Server integratieservices (SSIS)**.</span><span class="sxs-lookup"><span data-stu-id="27b19-135">**SQL Server Integration Services (SSIS)**.</span></span> <span data-ttu-id="27b19-136">SSIS is een onderdeel van SQL Server en een evaluatieversie of een gelicentieerde versie van SQL Server vereist.</span><span class="sxs-lookup"><span data-stu-id="27b19-136">SSIS is a component of SQL Server and requires an evaluation version or a licensed version of SQL Server.</span></span> <span data-ttu-id="27b19-137">Als u een evaluatieversie van SQL Server 2016 Preview, Zie [SQL Server-evaluaties][SQL Server Evaluations].</span><span class="sxs-lookup"><span data-stu-id="27b19-137">To get an evaluation version of SQL Server 2016 Preview, see [SQL Server Evaluations][SQL Server Evaluations].</span></span>
2. <span data-ttu-id="27b19-138">**Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="27b19-138">**Visual Studio**.</span></span> <span data-ttu-id="27b19-139">Als u de gratis Visual Studio Community Edition, Zie [Visual Studio Community][Visual Studio Community].</span><span class="sxs-lookup"><span data-stu-id="27b19-139">To get the free Visual Studio Community Edition, see [Visual Studio Community][Visual Studio Community].</span></span>
3. <span data-ttu-id="27b19-140">**SQL Server Data Tools voor Visual Studio (SSDT)**.</span><span class="sxs-lookup"><span data-stu-id="27b19-140">**SQL Server Data Tools for Visual Studio (SSDT)**.</span></span> <span data-ttu-id="27b19-141">Als u SQL Server Data Tools voor Visual Studio, Zie [Download SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].</span><span class="sxs-lookup"><span data-stu-id="27b19-141">To get SQL Server Data Tools for Visual Studio, see [Download SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].</span></span>
4. <span data-ttu-id="27b19-142">**Voorbeeldgegevens**.</span><span class="sxs-lookup"><span data-stu-id="27b19-142">**Sample data**.</span></span> <span data-ttu-id="27b19-143">Deze zelfstudie wordt opgeslagen in SQL Server in de AdventureWorks voorbeelddatabase als de brongegevens voorbeeldgegevens worden geladen in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="27b19-143">This tutorial uses sample data stored in SQL Server in the AdventureWorks sample database as the source data to be loaded into SQL Data Warehouse.</span></span> <span data-ttu-id="27b19-144">Als u de AdventureWorks voorbeelddatabase, Zie [AdventureWorks 2014 voorbeeld Databases][AdventureWorks 2014 Sample Databases].</span><span class="sxs-lookup"><span data-stu-id="27b19-144">To get the AdventureWorks sample database, see [AdventureWorks 2014 Sample Databases][AdventureWorks 2014 Sample Databases].</span></span>
5. <span data-ttu-id="27b19-145">**Een SQL Data Warehouse-database en machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="27b19-145">**A SQL Data Warehouse database and permissions**.</span></span> <span data-ttu-id="27b19-146">Deze zelfstudie maakt verbinding met een exemplaar van SQL Data Warehouse en gegevens worden geladen in de App.</span><span class="sxs-lookup"><span data-stu-id="27b19-146">This tutorial connects to a SQL Data Warehouse instance and loads data into it.</span></span> <span data-ttu-id="27b19-147">U moet gemachtigd zijn om een tabel te maken en om gegevens te laden.</span><span class="sxs-lookup"><span data-stu-id="27b19-147">You have to have permissions to create a table and to load data.</span></span>
6. <span data-ttu-id="27b19-148">**Een firewallregel**.</span><span class="sxs-lookup"><span data-stu-id="27b19-148">**A firewall rule**.</span></span> <span data-ttu-id="27b19-149">U moet een firewallregel maken in SQL Data Warehouse met het IP-adres van uw lokale computer, voordat u gegevens naar de SQL Data Warehouse uploaden kunt.</span><span class="sxs-lookup"><span data-stu-id="27b19-149">You have to create a firewall rule on SQL Data Warehouse with the IP address of your local computer before you can upload data to the SQL Data Warehouse.</span></span>

## <a name="step-1-create-a-new-integration-services-project"></a><span data-ttu-id="27b19-150">Stap 1: Maak een nieuw project voor de Integration Services</span><span class="sxs-lookup"><span data-stu-id="27b19-150">Step 1: Create a new Integration Services project</span></span>
1. <span data-ttu-id="27b19-151">Visual Studio starten.</span><span class="sxs-lookup"><span data-stu-id="27b19-151">Launch Visual Studio.</span></span>
2. <span data-ttu-id="27b19-152">Op de **bestand** selecteert u **nieuw | Project**.</span><span class="sxs-lookup"><span data-stu-id="27b19-152">On the **File** menu, select **New | Project**.</span></span>
3. <span data-ttu-id="27b19-153">Navigeer naar de **geïnstalleerd | Sjablonen | Business Intelligence | Integratieservices** projecttypen.</span><span class="sxs-lookup"><span data-stu-id="27b19-153">Navigate to the **Installed | Templates | Business Intelligence | Integration Services** project types.</span></span>
4. <span data-ttu-id="27b19-154">Selecteer **Integration Services-Project**.</span><span class="sxs-lookup"><span data-stu-id="27b19-154">Select **Integration Services Project**.</span></span> <span data-ttu-id="27b19-155">Waarden opgeven voor **naam** en **locatie**, en selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="27b19-155">Provide values for **Name** and **Location**, and then select **OK**.</span></span>

<span data-ttu-id="27b19-156">Visual Studio wordt geopend en wordt een nieuw project voor de Integration Services (SSIS) gemaakt.</span><span class="sxs-lookup"><span data-stu-id="27b19-156">Visual Studio opens and creates a new Integration Services (SSIS) project.</span></span> <span data-ttu-id="27b19-157">Visual Studio wordt geopend de ontwerpfunctie voor het één nieuwe SSIS-pakket (Package.dtsx) in het project.</span><span class="sxs-lookup"><span data-stu-id="27b19-157">Then Visual Studio opens the designer for the single new SSIS package (Package.dtsx) in the project.</span></span> <span data-ttu-id="27b19-158">U ziet het volgende schermgebieden:</span><span class="sxs-lookup"><span data-stu-id="27b19-158">You see the following screen areas:</span></span>

* <span data-ttu-id="27b19-159">Aan de linkerkant de **werkset** van SSIS-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="27b19-159">On the left, the **Toolbox** of SSIS components.</span></span>
* <span data-ttu-id="27b19-160">In het midden het ontwerpoppervlak met meerdere tabbladen.</span><span class="sxs-lookup"><span data-stu-id="27b19-160">In the middle, the design surface, with multiple tabs.</span></span> <span data-ttu-id="27b19-161">Doorgaans gebruikt u ten minste de **controlestroom** en de **gegevensstroom** tabbladen.</span><span class="sxs-lookup"><span data-stu-id="27b19-161">You typically use at least the **Control Flow** and the **Data Flow** tabs.</span></span>
* <span data-ttu-id="27b19-162">Aan de rechterkant de **Solution Explorer** en de **eigenschappen** deelvensters.</span><span class="sxs-lookup"><span data-stu-id="27b19-162">On the right, the **Solution Explorer** and the **Properties** panes.</span></span>
  
    ![][01]

## <a name="step-2-create-the-basic-data-flow"></a><span data-ttu-id="27b19-163">Stap 2: De stroom basisgegevens maken</span><span class="sxs-lookup"><span data-stu-id="27b19-163">Step 2: Create the basic data flow</span></span>
1. <span data-ttu-id="27b19-164">Sleep een taak gegevens stromen vanuit de werkset naar het midden van het ontwerpoppervlak dat (op het **controlestroom** tabblad).</span><span class="sxs-lookup"><span data-stu-id="27b19-164">Drag a Data Flow Task from the Toolbox to the center of the design surface (on the **Control Flow** tab).</span></span>
   
    ![][02]
2. <span data-ttu-id="27b19-165">Dubbelklik op de taak gegevens stromen overschakelen naar het tabblad gegevens stromen.</span><span class="sxs-lookup"><span data-stu-id="27b19-165">Double-click the Data Flow Task to switch to the Data Flow tab.</span></span>
3. <span data-ttu-id="27b19-166">In de lijst van andere bronnen in de werkset, sleept u een ADO.NET-gegevensbron naar het ontwerpoppervlak.</span><span class="sxs-lookup"><span data-stu-id="27b19-166">From the Other Sources list in the Toolbox, drag an ADO.NET Source to the design surface.</span></span> <span data-ttu-id="27b19-167">De naam ervan te wijzigen met de bron-adapter nog steeds is geselecteerd, **SQL Server-bron** in de **eigenschappen** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="27b19-167">With the source adapter still selected, change its name to **SQL Server source** in the **Properties** pane.</span></span>
4. <span data-ttu-id="27b19-168">Sleep een ADO.NET-doel naar het ontwerpoppervlak onder de ADO.NET-bron in de lijst andere bestemmingen in de werkset.</span><span class="sxs-lookup"><span data-stu-id="27b19-168">From the Other Destinations list in the Toolbox, drag an ADO.NET Destination to the design surface under the ADO.NET Source.</span></span> <span data-ttu-id="27b19-169">De naam ervan te wijzigen met de doeladapter nog steeds is geselecteerd, **SQL DW bestemming** in de **eigenschappen** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="27b19-169">With the destination adapter still selected, change its name to **SQL DW destination** in the **Properties** pane.</span></span>
   
    ![][09]

## <a name="step-3-configure-the-source-adapter"></a><span data-ttu-id="27b19-170">Stap 3: Configureer de bron-adapter</span><span class="sxs-lookup"><span data-stu-id="27b19-170">Step 3: Configure the source adapter</span></span>
1. <span data-ttu-id="27b19-171">Dubbelklik op de adapter bron te openen de **ADO.NET bron Editor**.</span><span class="sxs-lookup"><span data-stu-id="27b19-171">Double-click the source adapter to open the **ADO.NET Source Editor**.</span></span>
   
    ![][03]
2. <span data-ttu-id="27b19-172">Op de **Verbindingsbeheer** tabblad van de **ADO.NET bron Editor**, klikt u op de **nieuw** naast de **ADO.NET Verbindingsbeheer** lijst openen van de **ADO.NET Verbindingsbeheer configureren** dialoogvenster en te maken van de verbindingsinstellingen voor de SQL Server-database waarin gegevens voor deze zelfstudie worden geladen.</span><span class="sxs-lookup"><span data-stu-id="27b19-172">On the **Connection Manager** tab of the **ADO.NET Source Editor**, click the **New** button next to the **ADO.NET connection manager** list to open the **Configure ADO.NET Connection Manager** dialog box and create connection settings for the SQL Server database from which this tutorial loads data.</span></span>
   
    ![][04]
3. <span data-ttu-id="27b19-173">In de **ADO.NET Verbindingsbeheer configureren** in het dialoogvenster klikt u op de **nieuw** te openen de **Verbindingsbeheer** dialoogvenster vak en maak een nieuwe verbinding.</span><span class="sxs-lookup"><span data-stu-id="27b19-173">In the **Configure ADO.NET Connection Manager** dialog box, click the **New** button to open the **Connection Manager** dialog box and create a new data connection.</span></span>
   
    ![][05]
4. <span data-ttu-id="27b19-174">In de **Verbindingsbeheer** dialoogvenster vak, het volgende doen.</span><span class="sxs-lookup"><span data-stu-id="27b19-174">In the **Connection Manager** dialog box, do the following things.</span></span>
   
   1. <span data-ttu-id="27b19-175">Voor **Provider**, selecteer de SqlClient-gegevensprovider.</span><span class="sxs-lookup"><span data-stu-id="27b19-175">For **Provider**, select the SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="27b19-176">Voor **servernaam**, voer de naam van de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="27b19-176">For **Server name**, enter the SQL Server name.</span></span>
   3. <span data-ttu-id="27b19-177">In de **Meld u aan bij de server** sectie Selecteer of typ de verificatiegegevens.</span><span class="sxs-lookup"><span data-stu-id="27b19-177">In the **Log on to the server** section, select or enter authentication information.</span></span>
   4. <span data-ttu-id="27b19-178">In de **verbinding maken met een database** sectie, selecteert u de AdventureWorks voorbeelddatabase.</span><span class="sxs-lookup"><span data-stu-id="27b19-178">In the **Connect to a database** section, select the AdventureWorks sample database.</span></span>
   5. <span data-ttu-id="27b19-179">Klik op **verbinding testen**.</span><span class="sxs-lookup"><span data-stu-id="27b19-179">Click **Test Connection**.</span></span>
      
       ![][06]
   6. <span data-ttu-id="27b19-180">Klik in het dialoogvenster die de resultaten van de verbindingstest rapporteert op **OK** om terug te keren naar de **Verbindingsbeheer** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="27b19-180">In the dialog box that reports the results of the connection test, click **OK** to return to the **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="27b19-181">In de **Verbindingsbeheer** in het dialoogvenster klikt u op **OK** om terug te keren naar de **ADO.NET Verbindingsbeheer configureren** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="27b19-181">In the **Connection Manager** dialog box, click **OK** to return to the **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="27b19-182">In de **ADO.NET Verbindingsbeheer configureren** in het dialoogvenster klikt u op **OK** om terug te keren naar de **ADO.NET bron Editor**.</span><span class="sxs-lookup"><span data-stu-id="27b19-182">In the **Configure ADO.NET Connection Manager** dialog box, click **OK** to return to the **ADO.NET Source Editor**.</span></span>
6. <span data-ttu-id="27b19-183">In de **ADO.NET bron Editor**, in de **naam van de tabel of de weergave** lijst, selecteert de **Sales.SalesOrderDetail** tabel.</span><span class="sxs-lookup"><span data-stu-id="27b19-183">In the **ADO.NET Source Editor**, in the **Name of the table or the view** list, select the **Sales.SalesOrderDetail** table.</span></span>
   
    ![][07]
7. <span data-ttu-id="27b19-184">Klik op **Preview** om te zien van de eerste 200 rijen van de gegevens in de brontabel in de **Preview queryresultaten** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="27b19-184">Click **Preview** to see the first 200 rows of data in the source table in the **Preview Query Results** dialog box.</span></span>
   
    ![][08]
8. <span data-ttu-id="27b19-185">In de **Preview queryresultaten** in het dialoogvenster klikt u op **sluiten** om terug te keren naar de **ADO.NET bron Editor**.</span><span class="sxs-lookup"><span data-stu-id="27b19-185">In the **Preview Query Results** dialog box, click **Close** to return to the **ADO.NET Source Editor**.</span></span>
9. <span data-ttu-id="27b19-186">In de **ADO.NET bron Editor**, klikt u op **OK** voltooid met het configureren van de gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="27b19-186">In the **ADO.NET Source Editor**, click **OK** to finish configuring the data source.</span></span>

## <a name="step-4-connect-the-source-adapter-to-the-destination-adapter"></a><span data-ttu-id="27b19-187">Stap 4: Verbind de netwerkadapter van de bron met de doeladapter</span><span class="sxs-lookup"><span data-stu-id="27b19-187">Step 4: Connect the source adapter to the destination adapter</span></span>
1. <span data-ttu-id="27b19-188">Selecteer de bron-adapter op het ontwerpoppervlak.</span><span class="sxs-lookup"><span data-stu-id="27b19-188">Select the source adapter on the design surface.</span></span>
2. <span data-ttu-id="27b19-189">Selecteer de blauwe pijl die van de bron-adapter loopt en sleep deze naar de doel-editor totdat deze wordt uitgelijnd naar de juiste plaats.</span><span class="sxs-lookup"><span data-stu-id="27b19-189">Select the blue arrow that extends from the source adapter and drag it to the destination editor until it snaps into place.</span></span>
   
    ![][10]
   
    <span data-ttu-id="27b19-190">In een typische SSIS-pakket gebruikt u een aantal andere onderdelen uit de werkset SSIS tussen de bron en bestemming herstructureren, transformeren en gegevens te verwijderen als deze de SSIS-gegevensstroom passeert.</span><span class="sxs-lookup"><span data-stu-id="27b19-190">In a typical SSIS package, you use a number of other components from the SSIS Toolbox in between the source and the destination to restructure, transform, and cleanse your data as it passes through the SSIS data flow.</span></span> <span data-ttu-id="27b19-191">Als u wilt behouden in dit voorbeeld zo eenvoudig mogelijk, verbinding we de bron rechtstreeks naar de bestemming.</span><span class="sxs-lookup"><span data-stu-id="27b19-191">To keep this example as simple as possible, we’re connecting the source directly to the destination.</span></span>

## <a name="step-5-configure-the-destination-adapter"></a><span data-ttu-id="27b19-192">Stap 5: Configureer de doeladapter</span><span class="sxs-lookup"><span data-stu-id="27b19-192">Step 5: Configure the destination adapter</span></span>
1. <span data-ttu-id="27b19-193">Dubbelklik op de doeladapter te openen de **ADO.NET bestemming Editor**.</span><span class="sxs-lookup"><span data-stu-id="27b19-193">Double-click the destination adapter to open the **ADO.NET Destination Editor**.</span></span>
   
    ![][11]
2. <span data-ttu-id="27b19-194">Op de **Verbindingsbeheer** tabblad van de **ADO.NET bestemming Editor**, klikt u op de **nieuw** naast de **Verbindingsbeheer** lijst Open de **ADO.NET Verbindingsbeheer configureren** dialoogvenster en te maken van de verbindingsinstellingen voor de Azure SQL Data Warehouse-database waarin gegevens voor deze zelfstudie worden geladen.</span><span class="sxs-lookup"><span data-stu-id="27b19-194">On the **Connection Manager** tab of the **ADO.NET Destination Editor**, click the **New** button next to the **Connection manager** list to open the **Configure ADO.NET Connection Manager** dialog box and create connection settings for the Azure SQL Data Warehouse database into which this tutorial loads data.</span></span>
3. <span data-ttu-id="27b19-195">In de **ADO.NET Verbindingsbeheer configureren** in het dialoogvenster klikt u op de **nieuw** te openen de **Verbindingsbeheer** dialoogvenster vak en maak een nieuwe verbinding.</span><span class="sxs-lookup"><span data-stu-id="27b19-195">In the **Configure ADO.NET Connection Manager** dialog box, click the **New** button to open the **Connection Manager** dialog box and create a new data connection.</span></span>
4. <span data-ttu-id="27b19-196">In de **Verbindingsbeheer** dialoogvenster vak, het volgende doen.</span><span class="sxs-lookup"><span data-stu-id="27b19-196">In the **Connection Manager** dialog box, do the following things.</span></span>
   1. <span data-ttu-id="27b19-197">Voor **Provider**, selecteer de SqlClient-gegevensprovider.</span><span class="sxs-lookup"><span data-stu-id="27b19-197">For **Provider**, select the SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="27b19-198">Voor **servernaam**, voer de naam van de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="27b19-198">For **Server name**, enter the SQL Data Warehouse name.</span></span>
   3. <span data-ttu-id="27b19-199">In de **Meld u aan bij de server** sectie **Gebruik SQL Server-verificatie** en voer de verificatiegegevens.</span><span class="sxs-lookup"><span data-stu-id="27b19-199">In the **Log on to the server** section, select **Use SQL Server authentication** and enter authentication information.</span></span>
   4. <span data-ttu-id="27b19-200">In de **verbinding maken met een database** sectie, selecteer een bestaande SQL Data Warehouse-database.</span><span class="sxs-lookup"><span data-stu-id="27b19-200">In the **Connect to a database** section, select an existing SQL Data Warehouse database.</span></span>
   5. <span data-ttu-id="27b19-201">Klik op **verbinding testen**.</span><span class="sxs-lookup"><span data-stu-id="27b19-201">Click **Test Connection**.</span></span>
   6. <span data-ttu-id="27b19-202">Klik in het dialoogvenster die de resultaten van de verbindingstest rapporteert op **OK** om terug te keren naar de **Verbindingsbeheer** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="27b19-202">In the dialog box that reports the results of the connection test, click **OK** to return to the **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="27b19-203">In de **Verbindingsbeheer** in het dialoogvenster klikt u op **OK** om terug te keren naar de **ADO.NET Verbindingsbeheer configureren** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="27b19-203">In the **Connection Manager** dialog box, click **OK** to return to the **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="27b19-204">In de **ADO.NET Verbindingsbeheer configureren** in het dialoogvenster klikt u op **OK** om terug te keren naar de **ADO.NET bestemming Editor**.</span><span class="sxs-lookup"><span data-stu-id="27b19-204">In the **Configure ADO.NET Connection Manager** dialog box, click **OK** to return to the **ADO.NET Destination Editor**.</span></span>
6. <span data-ttu-id="27b19-205">In de **ADO.NET bestemming Editor**, klikt u op **nieuw** naast de **gebruik van een tabel of weergave** lijst openen de **Create Table** in het dialoogvenster voor het maken een nieuwe doeltabel met een kolomlijst die overeenkomt met de brontabel.</span><span class="sxs-lookup"><span data-stu-id="27b19-205">In the **ADO.NET Destination Editor**, click **New** next to the **Use a table or view** list to open the **Create Table** dialog box to create a new destination table with a column list that matches the source table.</span></span>
   
    ![][12a]
7. <span data-ttu-id="27b19-206">In de **Create Table** dialoogvenster vak, het volgende doen.</span><span class="sxs-lookup"><span data-stu-id="27b19-206">In the **Create Table** dialog box, do the following things.</span></span>
   
   1. <span data-ttu-id="27b19-207">Wijzig de naam van de doeltabel voor **verkooporderdetail**.</span><span class="sxs-lookup"><span data-stu-id="27b19-207">Change the name of the destination table to **SalesOrderDetail**.</span></span>
   2. <span data-ttu-id="27b19-208">Verwijder de **rowguid** kolom.</span><span class="sxs-lookup"><span data-stu-id="27b19-208">Remove the **rowguid** column.</span></span> <span data-ttu-id="27b19-209">De **uniqueidentifier** gegevenstype wordt niet ondersteund in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="27b19-209">The **uniqueidentifier** data type is not supported in SQL Data Warehouse.</span></span>
   3. <span data-ttu-id="27b19-210">Wijzig het gegevenstype van de **LineTotal** kolom **geld**.</span><span class="sxs-lookup"><span data-stu-id="27b19-210">Change the data type of the **LineTotal** column to **money**.</span></span> <span data-ttu-id="27b19-211">De **decimale** gegevenstype wordt niet ondersteund in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="27b19-211">The **decimal** data type is not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="27b19-212">Zie voor informatie over de ondersteunde gegevenstypen [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].</span><span class="sxs-lookup"><span data-stu-id="27b19-212">For info about supported data types, see [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].</span></span>
      
       ![][12b]
   4. <span data-ttu-id="27b19-213">Klik op **OK** voor het maken van de tabel en Ga terug naar de **ADO.NET bestemming Editor**.</span><span class="sxs-lookup"><span data-stu-id="27b19-213">Click **OK** to create the table and return to the **ADO.NET Destination Editor**.</span></span>
8. <span data-ttu-id="27b19-214">In de **ADO.NET bestemming Editor**, selecteer de **toewijzingen** tabblad om te zien hoe de kolommen in de bron zijn toegewezen aan kolommen in de bestemming.</span><span class="sxs-lookup"><span data-stu-id="27b19-214">In the **ADO.NET Destination Editor**, select the **Mappings** tab to see how columns in the source are mapped to columns in the destination.</span></span>
   
    ![][13]
9. <span data-ttu-id="27b19-215">Klik op **OK** voltooid met het configureren van de gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="27b19-215">Click **OK** to finish configuring the data source.</span></span>

## <a name="step-6-run-the-package-to-load-the-data"></a><span data-ttu-id="27b19-216">Stap 6: Het pakket om de gegevens te laden uitvoeren</span><span class="sxs-lookup"><span data-stu-id="27b19-216">Step 6: Run the package to load the data</span></span>
<span data-ttu-id="27b19-217">Het pakket uitvoeren door te klikken op de **Start** knop op de werkbalk of door het selecteren van een van de **uitvoeren** opties op de **Debug** menu.</span><span class="sxs-lookup"><span data-stu-id="27b19-217">Run the package by clicking the **Start** button on the toolbar or by selecting one of the **Run** options on the **Debug** menu.</span></span>

<span data-ttu-id="27b19-218">Als het pakket gestart wordt, ziet u gele draaiende wheels om aan te geven van de activiteit, evenals het aantal rijen verwerkt tot nu toe.</span><span class="sxs-lookup"><span data-stu-id="27b19-218">As the package begins to run, you see yellow spinning wheels to indicate activity as well as the number of rows processed so far.</span></span>

![][14]

<span data-ttu-id="27b19-219">Wanneer het pakket is voltooid, ziet u groen vinkje om aan te geven, zowel geslaagd als het totale aantal rijen met gegevens die worden geladen vanuit de bron naar de bestemming.</span><span class="sxs-lookup"><span data-stu-id="27b19-219">When the package has finished running, you see green check marks to indicate success as well as the total number of rows of data loaded from the source to the destination.</span></span>

![][15]

<span data-ttu-id="27b19-220">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="27b19-220">Congratulations!</span></span> <span data-ttu-id="27b19-221">U hebt de SQL Server Integration Services is gebruikt om gegevens te laden in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="27b19-221">You’ve successfully used SQL Server Integration Services to load data into Azure SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27b19-222">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="27b19-222">Next steps</span></span>
* <span data-ttu-id="27b19-223">Meer informatie over de SSIS-gegevensstroom.</span><span class="sxs-lookup"><span data-stu-id="27b19-223">Learn more about the SSIS data flow.</span></span> <span data-ttu-id="27b19-224">Begin hier: [gegevensstroom][Data Flow].</span><span class="sxs-lookup"><span data-stu-id="27b19-224">Start here: [Data Flow][Data Flow].</span></span>
* <span data-ttu-id="27b19-225">Informatie over het opsporen en oplossen van uw recht pakketten in de ontwerpomgeving.</span><span class="sxs-lookup"><span data-stu-id="27b19-225">Learn how to debug and troubleshoot your packages right in the design environment.</span></span> <span data-ttu-id="27b19-226">Begin hier: [hulpprogramma's voor het oplossen van problemen voor de ontwikkeling van pakket][Troubleshooting Tools for Package Development].</span><span class="sxs-lookup"><span data-stu-id="27b19-226">Start here: [Troubleshooting Tools for Package Development][Troubleshooting Tools for Package Development].</span></span>
* <span data-ttu-id="27b19-227">Informatie over het implementeren van SSIS-projecten en pakketten op Integration Services-Server of naar een andere opslaglocatie.</span><span class="sxs-lookup"><span data-stu-id="27b19-227">Learn how to deploy your SSIS projects and packages to Integration Services Server or to another storage location.</span></span> <span data-ttu-id="27b19-228">Begin hier: [van implementatieprojecten en pakketten][Deployment of Projects and Packages].</span><span class="sxs-lookup"><span data-stu-id="27b19-228">Start here: [Deployment of Projects and Packages][Deployment of Projects and Packages].</span></span>

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
