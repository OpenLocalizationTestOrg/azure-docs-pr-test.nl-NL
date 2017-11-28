---
title: Redgate gebruiken om gegevens in uw Azure datawarehouse te laden | Microsoft Docs
description: Leer hoe u Data Platform Studio van Redgate kunt gebruiken voor datawarehousingscenario's.
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
ms.openlocfilehash: a38b237d5bfc0450c1ca79b53a5784dbb9bf8602
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a><span data-ttu-id="9a458-103">Gegevens laden met behulp van Data Platform Studio van Redgate</span><span class="sxs-lookup"><span data-stu-id="9a458-103">Load data with Redgate Data Platform Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9a458-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="9a458-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)
> * [<span data-ttu-id="9a458-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="9a458-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [<span data-ttu-id="9a458-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="9a458-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)
> * [<span data-ttu-id="9a458-107">BCP</span><span class="sxs-lookup"><span data-stu-id="9a458-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="9a458-108">In deze zelfstudie ziet u hoe u [DPS van Redgate](http://www.red-gate.com/products/azure-development/data-platform-studio/) (Data Platform Studio) kunt gebruiken om gegevens te verplaatsen van een on-premises SQL-server naar Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9a458-108">This tutorial shows you how to use [Redgate's Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) to move data from an on-premises SQL Server to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="9a458-109">Met DPS worden de meest geschikte compatibiliteitscorrecties en optimalisaties toegepast. Daarom is het de snelste manier om aan de slag te gaan met SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9a458-109">Data Platform Studio applies the most appropriate compatibility fixes and optimizations, so it's the quickest way to get started with SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="9a458-110">[Redgate](http://www.red-gate.com) is al lange tijd een Microsoft-partner en levert verschillende SQL Server-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="9a458-110">[Redgate](http://www.red-gate.com) is a long-time Microsoft partner that delivers various SQL Server tools.</span></span> <span data-ttu-id="9a458-111">Deze functie in DPS is gratis beschikbaar voor commercieel en niet-commercieel gebruik.</span><span class="sxs-lookup"><span data-stu-id="9a458-111">This feature in Data Platform Studio has been made available freely for both commercial and non-commercial use.</span></span>
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="9a458-112">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="9a458-112">Before you begin</span></span>
### <a name="create-or-identify-resources"></a><span data-ttu-id="9a458-113">Resources maken of identificeren</span><span class="sxs-lookup"><span data-stu-id="9a458-113">Create or identify resources</span></span>
<span data-ttu-id="9a458-114">Voordat u met deze zelfstudie begint, moet u beschikken over:</span><span class="sxs-lookup"><span data-stu-id="9a458-114">Before starting this tutorial, you need to have:</span></span>

* <span data-ttu-id="9a458-115">**Een on-premises SQL Server-database**: de gegevens die u wilt importeren naar SQL Data Warehouse, moeten afkomstig zijn van een on-premises SQL-server (versie 2008R2 of hoger).</span><span class="sxs-lookup"><span data-stu-id="9a458-115">**on-premises SQL Server Database**: The data you want to import to SQL Data Warehouse needs to come from an on-premises SQL Server (version 2008R2 or above).</span></span> <span data-ttu-id="9a458-116">Met DPS kunnen gegevens niet rechtstreeks worden geïmporteerd uit een Azure SQL-database of uit tekstbestanden.</span><span class="sxs-lookup"><span data-stu-id="9a458-116">Data Platform Studio cannot import data directly from an Azure SQL Database or from text files.</span></span>
* <span data-ttu-id="9a458-117">**Azure-opslagaccount**: met DPS worden de gegevens klaargezet in de Azure Blob-opslag voordat ze in SQL Data Warehouse worden geladen.</span><span class="sxs-lookup"><span data-stu-id="9a458-117">**Azure Storage Account**: Data Platform Studio stages the data in Azure Blob Storage before loading it into SQL Data Warehouse.</span></span> <span data-ttu-id="9a458-118">Het opslagaccount moet het standaardimplementatiemodel Resource Manager gebruiken in plaats van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="9a458-118">The storage account must be using the “Resource Manager” deployment model (the default) rather than the “Classic” deployment model.</span></span> <span data-ttu-id="9a458-119">Als u geen opslagaccount hebt, leert u hoe u er een kunt maken.</span><span class="sxs-lookup"><span data-stu-id="9a458-119">If you don't have a storage account, learn how to Create a storage account.</span></span> 
* <span data-ttu-id="9a458-120">**SQL Data Warehouse**: in deze zelfstudie wordt getoond hoe gegevens worden verplaatst van een on-premises SQL-server naar SQL Data Warehouse. U hebt daarom een onlinedatawarehouse nodig.</span><span class="sxs-lookup"><span data-stu-id="9a458-120">**SQL Data Warehouse**: This tutorial moves the data from on-premises SQL Server to SQL Data Warehouse, so you need to have a data warehouse online.</span></span> <span data-ttu-id="9a458-121">Als u nog geen datawarehouse hebt, leert u hoe u er een moet inrichten om een SQL-datawarehouse te maken.</span><span class="sxs-lookup"><span data-stu-id="9a458-121">If you do not already have a data warehouse, learn how to Create an Azure SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="9a458-122">Als het opslagaccount en het datawarehouse in dezelfde regio worden gemaakt, verbeteren de prestaties.</span><span class="sxs-lookup"><span data-stu-id="9a458-122">Performance is improved if the storage account and the data warehouse are created in the same region.</span></span>
> 
> 

## <a name="step-1-sign-in-to-data-platform-studio-with-your-azure-account"></a><span data-ttu-id="9a458-123">Stap 1: Aanmelden bij DPS met uw Azure-account</span><span class="sxs-lookup"><span data-stu-id="9a458-123">Step 1: Sign in to Data Platform Studio with your Azure account</span></span>
<span data-ttu-id="9a458-124">Open de webbrowser en navigeer naar de website van [Data Platform Studio](https://www.dataplatformstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="9a458-124">Open your web browser and navigate to the [Data Platform Studio](https://www.dataplatformstudio.com/) website.</span></span> <span data-ttu-id="9a458-125">Meld u aan met hetzelfde Azure-account dat u hebt gebruikt om het opslagaccount en het datawarehouse te maken.</span><span class="sxs-lookup"><span data-stu-id="9a458-125">Sign in with the same Azure account that you used to create the storage account and data warehouse.</span></span> <span data-ttu-id="9a458-126">Als uw e-mailadres is gekoppeld aan een werk- of schoolaccount en aan een Microsoft-account, kiest u het account waarmee u toegang hebt tot uw resources.</span><span class="sxs-lookup"><span data-stu-id="9a458-126">If your email address is associated with both a work or school account and a Microsoft account, be sure to choose the account that has access to your resources.</span></span>

> [!NOTE]
> <span data-ttu-id="9a458-127">Als dit de eerste keer is dat u DPS gebruikt, wordt u gevraagd om de toepassing toestemming te geven om de Azure-resources te beheren.</span><span class="sxs-lookup"><span data-stu-id="9a458-127">If this is your first time using Data Platform Studio, you are asked to grant the application permission to manage your Azure resources.</span></span>
> 
> 

## <a name="step-2-start-the-import-wizard"></a><span data-ttu-id="9a458-128">Stap 2: Wizard Importeren starten</span><span class="sxs-lookup"><span data-stu-id="9a458-128">Step 2: Start the Import Wizard</span></span>
<span data-ttu-id="9a458-129">Selecteer in het hoofdvenster van DPS de koppeling Importeren naar Azure SQL Data Warehouse om de wizard Importeren te starten.</span><span class="sxs-lookup"><span data-stu-id="9a458-129">From the DPS main screen, select the Import to Azure SQL Data Warehouse link to start the import wizard.</span></span>

![][1]

## <a name="step-3-install-the-data-platform-studio-gateway"></a><span data-ttu-id="9a458-130">Stap 3: DPS-gateway installeren</span><span class="sxs-lookup"><span data-stu-id="9a458-130">Step 3: Install the Data Platform Studio Gateway</span></span>
<span data-ttu-id="9a458-131">Als u verbinding wilt maken met uw on-premises SQL Server-database, moet u de DPS-gateway installeren.</span><span class="sxs-lookup"><span data-stu-id="9a458-131">To connect to your on-premises SQL Server database, you need to install the DPS Gateway.</span></span> <span data-ttu-id="9a458-132">De gateway is een clientagent voor toegang tot de on-premises omgeving, waarmee gegevens worden uitgepakt en geüpload naar uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="9a458-132">The gateway is a client agent that provides access to your on-premises environment, extracts the data, and uploads it to your storage account.</span></span> <span data-ttu-id="9a458-133">De gegevens worden niet verwerkt op de servers van Redgate.</span><span class="sxs-lookup"><span data-stu-id="9a458-133">Your data never passes through Redgate’s servers.</span></span> <span data-ttu-id="9a458-134">De gateway installeren:</span><span class="sxs-lookup"><span data-stu-id="9a458-134">To install the Gateway:</span></span>

1. <span data-ttu-id="9a458-135">Klik op de koppeling **Gateway maken**</span><span class="sxs-lookup"><span data-stu-id="9a458-135">Click the **Create Gateway** link</span></span>
2. <span data-ttu-id="9a458-136">Download en installeer de gateway met behulp van het geleverde installatieprogramma</span><span class="sxs-lookup"><span data-stu-id="9a458-136">Download and install the Gateway using the provided installer</span></span>

![][2]

> [!NOTE]
> <span data-ttu-id="9a458-137">De gateway kan worden geïnstalleerd op elke computer met netwerktoegang tot de SQL Server-brondatabase.</span><span class="sxs-lookup"><span data-stu-id="9a458-137">The Gateway can be installed on any machine with network access to the source SQL Server database.</span></span> <span data-ttu-id="9a458-138">De gateway heeft toegang tot de SQL Server-database via Windows-verificatie met de referenties van de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="9a458-138">It accesses the SQL Server database using Windows authentication with the credentials of the current user.</span></span>
> 
> 

<span data-ttu-id="9a458-139">Zodra de gateway is geïnstalleerd, wordt de status ervan gewijzigd naar Verbonden en kunt u Volgende selecteren.</span><span class="sxs-lookup"><span data-stu-id="9a458-139">Once installed, the Gateway status changes to Connected and you can select Next.</span></span>

## <a name="step-4-identify-the-source-database"></a><span data-ttu-id="9a458-140">Stap 4: De brondatabase identificeren</span><span class="sxs-lookup"><span data-stu-id="9a458-140">Step 4: Identify the source database</span></span>
<span data-ttu-id="9a458-141">Voer in het tekstvak *Servernaam invoeren* de naam in van de server die de database host, en selecteer **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9a458-141">In the *Enter Server Name* textbox, enter the name of the server that hosts your database and select **Next**.</span></span> <span data-ttu-id="9a458-142">Selecteer vervolgens in de vervolgkeuzelijst de database waaruit u gegevens wilt importeren.</span><span class="sxs-lookup"><span data-stu-id="9a458-142">Then, from the drop-down menu, select the database you want to import data from.</span></span>

![][3]

<span data-ttu-id="9a458-143">De geselecteerde database wordt met DPS gecontroleerd op tabellen die kunnen worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="9a458-143">DPS inspects the selected database for tables to import.</span></span> <span data-ttu-id="9a458-144">Met DPS worden standaard alle tabellen in de database geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="9a458-144">By default, DPS imports all the tables in the database.</span></span> <span data-ttu-id="9a458-145">U kunt tabellen selecteren of de selectie van tabellen opheffen door de koppeling Alle tabellen uit te vouwen.</span><span class="sxs-lookup"><span data-stu-id="9a458-145">You can select or deselect tables by expanding the All Tables link.</span></span> <span data-ttu-id="9a458-146">Selecteer de knop Volgende om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="9a458-146">Select the Next button to move forward.</span></span>

## <a name="step-5-choose-a-storage-account-to-stage-the-data"></a><span data-ttu-id="9a458-147">Stap 5: Een opslagaccount kiezen om de gegevens in klaar te zetten</span><span class="sxs-lookup"><span data-stu-id="9a458-147">Step 5: Choose a storage account to stage the data</span></span>
<span data-ttu-id="9a458-148">DPS vraagt u om een locatie om de gegevens in klaar te zetten.</span><span class="sxs-lookup"><span data-stu-id="9a458-148">DPS prompts you for a location to stage the data.</span></span> <span data-ttu-id="9a458-149">Kies een bestaand opslagaccount in uw abonnement en selecteer **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9a458-149">Choose an existing storage account from your subscription and select **Next**.</span></span>

> [!NOTE]
> <span data-ttu-id="9a458-150">Met DPS wordt een nieuwe blobcontainer gemaakt in het gekozen opslagaccount. Voor elke import wordt een afzonderlijke map gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9a458-150">DPS will create a new blob container in the chosen storage account and use a distinct folder for each import.</span></span>
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a><span data-ttu-id="9a458-151">Stap 6: Een datawarehouse selecteren</span><span class="sxs-lookup"><span data-stu-id="9a458-151">Step 6: Select a data warehouse</span></span>
<span data-ttu-id="9a458-152">Vervolgens selecteert u [Azure SQL-datawarehouse](http://aka.ms/sqldw) om de gegevens in te importeren.</span><span class="sxs-lookup"><span data-stu-id="9a458-152">Next, you select an online [Azure SQL Data Warehouse](http://aka.ms/sqldw) database to import the data into.</span></span> <span data-ttu-id="9a458-153">Nadat u de database hebt geselecteerd, moet u de referenties invoeren om verbinding te maken met de database. Selecteer vervolgens **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9a458-153">Once you've selected your database, you need to enter the credentials to connect to the database and select **Next**.</span></span>

![][5]

> [!NOTE]
> <span data-ttu-id="9a458-154">De doelgegevenstabellen worden samengevoegd in het datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="9a458-154">DPS merges the source data tables into the data warehouse.</span></span> <span data-ttu-id="9a458-155">U wordt gewaarschuwd als de tabelnaam vereist dat bestaande tabellen in het datawarehouse worden overschreven.</span><span class="sxs-lookup"><span data-stu-id="9a458-155">DPS warns you if the table name requires it to overwrite existing tables in the data warehouse.</span></span> <span data-ttu-id="9a458-156">U kunt ervoor kiezen om bestaande objecten in het datawarehouse te verwijderen. Dit doet u door te tikken op Alle bestaande objecten verwijderen voor het importeren.</span><span class="sxs-lookup"><span data-stu-id="9a458-156">You may optionally delete any existing objects in the data warehouse by ticking Delete all existing objects before import.</span></span>
> 
> 

## <a name="step-7-import-the-data"></a><span data-ttu-id="9a458-157">Stap 7: De gegevens importeren</span><span class="sxs-lookup"><span data-stu-id="9a458-157">Step 7: Import the data</span></span>
<span data-ttu-id="9a458-158">In DPS wordt bevestigd dat u de gegevens wilt importeren.</span><span class="sxs-lookup"><span data-stu-id="9a458-158">DPS confirms that you would like to import the data.</span></span> <span data-ttu-id="9a458-159">Klik op de knop Importeren starten om te beginnen met het importeren van gegevens.</span><span class="sxs-lookup"><span data-stu-id="9a458-159">Simply click the Start import button to begin the data import.</span></span>

![][6]

<span data-ttu-id="9a458-160">Er wordt een visualisatie weergegeven waarin de voortgang van het uitpakken en uploaden van de gegevens van de on-premises SQL-server wordt weergegeven, evenals de voortgang van het importeren in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9a458-160">DPS displays a visualization that shows the progress of extracting and uploading the data from the on-premises SQL Server and the progress of the import into SQL Data Warehouse.</span></span>

![][7]

<span data-ttu-id="9a458-161">Als het importeren is voltooid, wordt er in DPS een overzicht weergegeven van de gegevensimport en een wijzigingsrapport van de compatibiliteitsoplossingen die zijn uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9a458-161">Once the import is complete, DPS displays a summary of the data import and a change report of the compatibility fixes that have been performed.</span></span>

![][8]

## <a name="next-steps"></a><span data-ttu-id="9a458-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9a458-162">Next steps</span></span>
<span data-ttu-id="9a458-163">Als u de gegevens in SQL Data Warehouse wilt verkennen, begint u met het bekijken van:</span><span class="sxs-lookup"><span data-stu-id="9a458-163">To explore your data within SQL Data Warehouse, start by viewing:</span></span>

* <span data-ttu-id="9a458-164">[Query’s uitvoeren bij Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span><span class="sxs-lookup"><span data-stu-id="9a458-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span></span>
* <span data-ttu-id="9a458-165">[Gegevens visualiseren met Power BI][Visualize data with Power BI]</span><span class="sxs-lookup"><span data-stu-id="9a458-165">[Visualize data with Power BI][Visualize data with Power BI]</span></span>

<span data-ttu-id="9a458-166">Voor meer informatie over Data Platform Studio van Redgate:</span><span class="sxs-lookup"><span data-stu-id="9a458-166">To learn more about Redgate’s Data Platform Studio:</span></span>

* [<span data-ttu-id="9a458-167">Ga naar de DPS-startpagina</span><span class="sxs-lookup"><span data-stu-id="9a458-167">Visit the DPS homepage</span></span>](http://www.dataplatformstudio.com/)
* [<span data-ttu-id="9a458-168">Bekijk een demonstratie van DPS op Channel 9</span><span class="sxs-lookup"><span data-stu-id="9a458-168">Watch a demo of DPS on Channel9</span></span>](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

<span data-ttu-id="9a458-169">Zie voor een overzicht van andere manieren om te migreren en uw gegevens in SQL Data Warehouse te laden:</span><span class="sxs-lookup"><span data-stu-id="9a458-169">For an overview of other ways to migrate and load your data in SQL Data Warehouse see:</span></span>

* <span data-ttu-id="9a458-170">[Uw oplossing migreren naar SQL Data Warehouse][Migrate your solution to SQL Data Warehouse]</span><span class="sxs-lookup"><span data-stu-id="9a458-170">[Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse]</span></span>
* <span data-ttu-id="9a458-171">[Load data into Azure SQL Data Warehouse](sql-data-warehouse-overview-load.md) (Gegevens laden in Azure SQL Data Warehouse)</span><span class="sxs-lookup"><span data-stu-id="9a458-171">[Load data into Azure SQL Data Warehouse](sql-data-warehouse-overview-load.md)</span></span>

<span data-ttu-id="9a458-172">Zie het [Overzicht van SQL Data Warehouse voor ontwikkelaars](sql-data-warehouse-overview-develop.md) voor meer tips voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="9a458-172">For more development tips, see the [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span></span>

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
[Migrate your solution to SQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
