---
title: "aaaLoad gegevens in Azure SQL Data Warehouse – Data Factory | Microsoft Docs"
description: Deze zelfstudie gegevens laadt in Azure SQL Data Warehouse met behulp van Azure Data Factory en maakt gebruik van een SQL Server-database als Hallo-gegevensbron.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a><span data-ttu-id="70f28-103">Gegevens laden in SQL Data Warehouse met Data Factory</span><span class="sxs-lookup"><span data-stu-id="70f28-103">Load data into SQL Data Warehouse with Data Factory</span></span>

<span data-ttu-id="70f28-104">U kunt Azure Data Factory tooload gegevens in Azure SQL Data Warehouse vanaf elke Hallo [ondersteunde gegevensarchieven bron](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="70f28-104">You can use Azure Data Factory tooload data into Azure SQL Data Warehouse from any of hello [supported source data stores](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="70f28-105">U kunt bijvoorbeeld gegevens uit een Azure SQL database of een Oracle-database laden in een SQL datawarehouse met behulp van de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="70f28-105">For example, you can load data from an Azure SQL database or an Oracle database into a SQL data warehouse by using Data Factory.</span></span> <span data-ttu-id="70f28-106">Zelfstudie in dit artikel leert u hoe tooload gegevens uit een lokale SQL Server-database in een SQL datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="70f28-106">Tutorial in this article shows you how tooload data from an on-premises SQL Server database into a SQL data warehouse.</span></span>

<span data-ttu-id="70f28-107">**Tijd schatting**: in deze zelfstudie neemt ongeveer 10-15 minuten toocomplete als Hallo vereisten is voldaan.</span><span class="sxs-lookup"><span data-stu-id="70f28-107">**Time estimate**: This tutorial takes about 10-15 minutes toocomplete once hello prerequisites are met.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70f28-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="70f28-108">Prerequisites</span></span>

- <span data-ttu-id="70f28-109">U moet een **SQL Server-database** met tabellen die gegevens Hallo bevatten toobe gekopieerd toohello SQL datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="70f28-109">You need a **SQL Server database** with tables that contain hello data toobe copied over toohello SQL data warehouse.</span></span>  

- <span data-ttu-id="70f28-110">U moet een online **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="70f28-110">You need an online **SQL Data Warehouse**.</span></span> <span data-ttu-id="70f28-111">Als u nog geen datawarehouse, meer te weten hoe te[maken van een Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="70f28-111">If you do not already have a data warehouse, learn how too[Create an Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span></span>

- <span data-ttu-id="70f28-112">U moet een **Azure Storage-Account**.</span><span class="sxs-lookup"><span data-stu-id="70f28-112">You need an **Azure Storage Account**.</span></span> <span data-ttu-id="70f28-113">Als u nog geen opslagaccount, meer te weten hoe te[een opslagaccount maken](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="70f28-113">If you do not already have a storage account, learn how too[Create a storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="70f28-114">Zoek naar Hallo storage-account voor de beste prestaties en Hallo datawarehouse in Hallo dezelfde Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="70f28-114">For best performance, locate hello storage account and hello data warehouse in hello same Azure region.</span></span>

## <a name="configure-a-data-factory"></a><span data-ttu-id="70f28-115">Een gegevensfactory configureren</span><span class="sxs-lookup"><span data-stu-id="70f28-115">Configure a data factory</span></span>
1. <span data-ttu-id="70f28-116">Meld u bij toohello [Azure-portal][].</span><span class="sxs-lookup"><span data-stu-id="70f28-116">Log in toohello [Azure portal][].</span></span>
2. <span data-ttu-id="70f28-117">Zoek uw datawarehouse en klikt u op tooopen deze.</span><span class="sxs-lookup"><span data-stu-id="70f28-117">Locate your data warehouse and click tooopen it.</span></span>
3. <span data-ttu-id="70f28-118">Klik op de belangrijkste blade Hallo **gegevens laden** > **Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="70f28-118">In hello main blade, click **Load Data** > **Azure Data Factory**.</span></span>

    ![Gegevens laden wizard starten](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. <span data-ttu-id="70f28-120">Als u een gegevensfactory niet in uw Azure-abonnement hebt, ziet u een **New Data Factory** dialoogvenster in een afzonderlijke tabblad van Hallo browser.</span><span class="sxs-lookup"><span data-stu-id="70f28-120">If you do not have a data factory in your Azure subscription, you see a **New Data Factory** dialog box in a separate tab of hello browser.</span></span> <span data-ttu-id="70f28-121">Vul Hallo aangevraagde informatie en op **maken**.</span><span class="sxs-lookup"><span data-stu-id="70f28-121">Fill in hello requested information, and click **Create**.</span></span> <span data-ttu-id="70f28-122">Nadat Hallo gegevensfactory is gemaakt, Hallo **New Data Factory** dialoogvenster wordt gesloten en u ziet Hallo **Selecteer Data Factory** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="70f28-122">After hello data factory is created, hello **New Data Factory** dialog box closes, and you see hello **Select Data Factory** dialog box.</span></span>

    <span data-ttu-id="70f28-123">Als u een of meer gegevensfactory's al in hello Azure-abonnement hebt, ziet u Hallo **Selecteer Data Factory** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="70f28-123">If you have one or more data factories already in hello Azure subscription, you see hello **Select Data Factory** dialog box.</span></span> <span data-ttu-id="70f28-124">In dit dialoogvenster, u kunt selecteren van een bestaande gegevensfactory of klik op **maken nieuwe gegevensfactory** toocreate een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="70f28-124">In this dialog box, you can either select an existing data factory or click **Create new data factory** toocreate a new one.</span></span>

    ![Data Factory configureren](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. <span data-ttu-id="70f28-126">In Hallo **Selecteer Data Factory** dialoogvenster, Hallo **gegevens laden** optie is standaard geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="70f28-126">In hello **Select Data Factory** dialog box, hello **Load data** option is selected by default.</span></span> <span data-ttu-id="70f28-127">Klik op **volgende** toostart maken van een data laden van taak.</span><span class="sxs-lookup"><span data-stu-id="70f28-127">Click **Next** toostart creating a data loading task.</span></span>

## <a name="configure-hello-data-factory-properties"></a><span data-ttu-id="70f28-128">Hallo data factory-eigenschappen configureren</span><span class="sxs-lookup"><span data-stu-id="70f28-128">Configure hello data factory properties</span></span>
<span data-ttu-id="70f28-129">Nu dat u een gegevensfactory gemaakt hebt, is de volgende stap Hallo tooconfigure Hallo gegevens laden van de planning.</span><span class="sxs-lookup"><span data-stu-id="70f28-129">Now that you have created a data factory, hello next step is tooconfigure hello data loading schedule.</span></span>

1. <span data-ttu-id="70f28-130">Voor **taaknaam**, voer **DWLoadData fromSQLServer**.</span><span class="sxs-lookup"><span data-stu-id="70f28-130">For **Task name**, enter **DWLoadData-fromSQLServer**.</span></span>
2. <span data-ttu-id="70f28-131">Standaard-Hallo **eenmaal nu uitvoeren** optie, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="70f28-131">Use hello default **Run once now** option, click **Next**.</span></span>

    ![Configureer load planning](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a><span data-ttu-id="70f28-133">Hallo brongegevensarchief en gateway configureren</span><span class="sxs-lookup"><span data-stu-id="70f28-133">Configure hello source data store and gateway</span></span>
<span data-ttu-id="70f28-134">U kunt nu de Data Factory over Hallo lokale SQL Server-database van waaruit u gegevens tooload wilt.</span><span class="sxs-lookup"><span data-stu-id="70f28-134">Now you tell Data Factory about hello on-premises SQL Server database from which you want tooload data.</span></span>

1. <span data-ttu-id="70f28-135">Kies **SQL Server** uit de brongegevens Hallo ondersteund catalogus opslaan en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="70f28-135">Choose **SQL Server** from hello supported source data store catalog, and click **Next**.</span></span>

    ![SQL Server-bron kiezen](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. <span data-ttu-id="70f28-137">Een **lokale SQL Server-database. Geef Hallo** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="70f28-137">A **Specify hello on-premises SQL Server database** dialog appears.</span></span> <span data-ttu-id="70f28-138">Hallo eerst **verbindingsnaam** veld wordt automatisch ingevuld.</span><span class="sxs-lookup"><span data-stu-id="70f28-138">hello first  **Connection name** field is auto filled in.</span></span> <span data-ttu-id="70f28-139">Hallo tweede veld vraagt om de naam op Hallo van Hallo **Gateway**.</span><span class="sxs-lookup"><span data-stu-id="70f28-139">hello second field asks for hello name of hello **Gateway**.</span></span> <span data-ttu-id="70f28-140">Als u een bestaande gegevensfactory waarop al een gateway gebruikt, kunt u Hallo gateway hergebruiken door deze te selecteren in de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="70f28-140">If you are using an existing data factory that already has a gateway, you can reuse hello gateway by selecting it from hello drop-down list.</span></span> <span data-ttu-id="70f28-141">Klik op Hallo **Gateway maken** toocreate een Data Management Gateway koppelen.</span><span class="sxs-lookup"><span data-stu-id="70f28-141">Click hello **Create Gateway** link toocreate a Data Management Gateway.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="70f28-142">Als de brongegevens Hallo opslaat on-premises of in een virtuele machine van Azure IaaS een Data Management Gateway is vereist.</span><span class="sxs-lookup"><span data-stu-id="70f28-142">If hello source data store is on-premises or in an Azure IaaS virtual machine, a Data Management Gateway is required.</span></span> <span data-ttu-id="70f28-143">Een gateway heeft een 1-1-relatie met een data factory.</span><span class="sxs-lookup"><span data-stu-id="70f28-143">A gateway has a 1-1 relationship with a data factory.</span></span> <span data-ttu-id="70f28-144">Kan niet worden gebruikt uit een andere data factory, maar deze kan worden gebruikt door meerdere gegevens bij het laden van taken met in Hallo dezelfde gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="70f28-144">It cannot be used from another data factory, but it can be used by multiple data loading tasks with in hello same data factory.</span></span> <span data-ttu-id="70f28-145">Een gateway kan gebruikte tooconnect toomultiple gegevensarchieven worden bij het uitvoeren van taken laden van gegevens.</span><span class="sxs-lookup"><span data-stu-id="70f28-145">A gateway can be used tooconnect toomultiple data stores when running data loading tasks.</span></span>
    >
    > <span data-ttu-id="70f28-146">Zie voor gedetailleerde informatie over gateway-Hallo [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="70f28-146">For detailed information about hello gateway, see [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) article.</span></span>

3. <span data-ttu-id="70f28-147">Een **Gateway maken** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="70f28-147">A **Create Gateway** dialog box appears.</span></span> <span data-ttu-id="70f28-148">Voer voor de naam, **GatewayForDWLoading**, en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="70f28-148">For Name, enter **GatewayForDWLoading**, and click **Create**.</span></span>

4. <span data-ttu-id="70f28-149">Een **Gateway configureren** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="70f28-149">A **Configure Gateway** dialog box appears.</span></span> <span data-ttu-id="70f28-150">Klik op **snelle installatie op deze computer starten** tooautomatically downloaden, installeren en registreren van Data Management Gateway op de huidige computer.</span><span class="sxs-lookup"><span data-stu-id="70f28-150">Click **Launch express setup on this computer** tooautomatically download, install, and register Data Management Gateway on your current machine.</span></span> <span data-ttu-id="70f28-151">Hallo voortgang wordt weergegeven in een pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="70f28-151">hello progress is shown in a pop-up window.</span></span> <span data-ttu-id="70f28-152">Als het Hallo-computer kan geen verbinding maken toohello gegevensarchief, kunt u handmatig [download en installeer de gateway Hallo](https://www.microsoft.com/download/details.aspx?id=39717) op een computer die verbinding van toohello gegevens maken kan opslaan en gebruik vervolgens de belangrijkste tooregister Hallo.</span><span class="sxs-lookup"><span data-stu-id="70f28-152">If hello machine cannot connect toohello data store, you can manually [download and install hello gateway](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect toohello data store, and then use hello key tooregister.</span></span>
    > [!NOTE]
    > <span data-ttu-id="70f28-153">Hallo snelle installatie werkt systeemeigen met Microsoft Edge en Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="70f28-153">hello express setup works natively with Microsoft Edge and Internet Explorer.</span></span> <span data-ttu-id="70f28-154">Als u Google Chrome gebruikt, moet u eerst Hallo ClickOnce-extensie van de Chrome web store installeren.</span><span class="sxs-lookup"><span data-stu-id="70f28-154">If you are using Google Chrome, first install hello ClickOnce extension from Chrome web store.</span></span>

    ![Snelle installatie starten](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. <span data-ttu-id="70f28-156">Wachten op Hallo gateway setup toocomplete.</span><span class="sxs-lookup"><span data-stu-id="70f28-156">Wait for hello gateway setup toocomplete.</span></span> <span data-ttu-id="70f28-157">Zodra de Hallo gateway is geregistreerd en online is, Hallo pop-upvenster wordt gesloten en Hallo nieuwe gateway wordt weergegeven in het veld Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="70f28-157">Once hello gateway is successfully registered and is online, hello pop-up window closes and hello new gateway appears in hello gateway field.</span></span> <span data-ttu-id="70f28-158">Vervolgens invullen Hallo rest velden als volgt vereist, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="70f28-158">Then fill in hello rest required fields as follows, then click **Next**.</span></span>
    - <span data-ttu-id="70f28-159">**Servernaam**: naam van Hallo lokale SQL Server.</span><span class="sxs-lookup"><span data-stu-id="70f28-159">**Server name**: Name of hello on-premises SQL Server.</span></span>
    - <span data-ttu-id="70f28-160">**Databasenaam**: SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="70f28-160">**Database name**: SQL Server database.</span></span>
    - <span data-ttu-id="70f28-161">**Versleuteling van referenties**: Hallo standaard gebruiken 'door webbrowser".</span><span class="sxs-lookup"><span data-stu-id="70f28-161">**Credential encryption**: Use hello default "By web browser".</span></span>
    - <span data-ttu-id="70f28-162">**Verificatietype**: Kies Hallo type verificatie dat u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="70f28-162">**Authentication type**: Choose hello type of authentication you are using.</span></span>
    - <span data-ttu-id="70f28-163">**Gebruikersnaam** en **wachtwoord**: Hallo-gebruikersnaam en wachtwoord invoeren voor een gebruiker met machtigingen toocopy Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="70f28-163">**User name** and **password**: Enter hello user name and password for a user who has permission toocopy hello data.</span></span>

    ![Snelle installatie starten](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. <span data-ttu-id="70f28-165">de volgende stap Hallo is toochoose Hallo tabellen vanuit welke toocopy Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="70f28-165">hello next step is toochoose hello tables from which toocopy hello data.</span></span> <span data-ttu-id="70f28-166">U kunt Hallo tabellen filteren met behulp van trefwoorden.</span><span class="sxs-lookup"><span data-stu-id="70f28-166">You can filter hello tables by using keywords.</span></span> <span data-ttu-id="70f28-167">En kunt u gegevens en tabel schema Hallo in Hallo onderpaneel bekijken.</span><span class="sxs-lookup"><span data-stu-id="70f28-167">And you can preview hello data and table schema in hello bottom panel.</span></span> <span data-ttu-id="70f28-168">Nadat u hebt geselecteerd, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="70f28-168">After you finish your selection, click **Next**.</span></span>

    ![Selecteer tabellen](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a><span data-ttu-id="70f28-170">Hallo bestemming, uw SQL Data Warehouse configureren</span><span class="sxs-lookup"><span data-stu-id="70f28-170">Configure hello destination, your SQL Data Warehouse</span></span>

<span data-ttu-id="70f28-171">U kunt nu de Data Factory over informatie over het Hallo-doel.</span><span class="sxs-lookup"><span data-stu-id="70f28-171">Now you tell Data Factory about hello destination information.</span></span>

1. <span data-ttu-id="70f28-172">De verbindingsinformatie voor SQL Data Warehouse wordt automatisch ingevuld.</span><span class="sxs-lookup"><span data-stu-id="70f28-172">Your SQL Data Warehouse connection information is filled in automatically.</span></span> <span data-ttu-id="70f28-173">Hallo wachtwoord opgeven voor Hallo-gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="70f28-173">Enter hello password for hello user name.</span></span> <span data-ttu-id="70f28-174">en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="70f28-174">and click **Next**.</span></span>

    ![Doel configureren](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. <span data-ttu-id="70f28-176">Een intelligente tabeltoewijzing wordt weergegeven dat is toegewezen toodestination brontabellen op basis van tabelnamen.</span><span class="sxs-lookup"><span data-stu-id="70f28-176">An intelligent table mapping appears that maps source toodestination tables based on table names.</span></span> <span data-ttu-id="70f28-177">Als Hallo tabel niet in het Hallo-doel bestaat, standaard ADF maakt een Hello dezelfde naam (dit geldt tooSQL Server of Azure SQL Database als bron).</span><span class="sxs-lookup"><span data-stu-id="70f28-177">If hello table does not exist in hello destination, by default ADF will create one with hello same name (this applies tooSQL Server or Azure SQL Database as source).</span></span> <span data-ttu-id="70f28-178">U kunt ook toomap tooan bestaande tabel.</span><span class="sxs-lookup"><span data-stu-id="70f28-178">You can also choose toomap tooan existing table.</span></span> <span data-ttu-id="70f28-179">Controleer en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="70f28-179">Review and click **Next**.</span></span>

    ![Tabellen toewijzen](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. <span data-ttu-id="70f28-181">Bekijk Hallo schematoewijzing en zoekt u fout- of waarschuwingsberichten.</span><span class="sxs-lookup"><span data-stu-id="70f28-181">Review hello schema mapping and look for error or warning messages.</span></span> <span data-ttu-id="70f28-182">Intelligent toewijzing is gebaseerd op de kolomnaam.</span><span class="sxs-lookup"><span data-stu-id="70f28-182">Intelligent mapping is based on column name.</span></span> <span data-ttu-id="70f28-183">Als er een conversie van het type niet-ondersteunde gegevens tussen de bron- en doelserver kolom hello, ziet u een foutbericht weergegeven naast de bijbehorende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="70f28-183">If there is an unsupported data type conversion between hello source and destination column, you see an error message alongside hello corresponding table.</span></span> <span data-ttu-id="70f28-184">Als u ervoor kiest toolet Data Factory automatisch Hallo tabellen maken, typeconversie van de juiste gegevens kan gebeuren als de toofix Hallo incompatibiliteit tussen bron- en doelserver winkels nodig.</span><span class="sxs-lookup"><span data-stu-id="70f28-184">If you choose toolet Data Factory auto create hello tables, proper data type conversion may happen if needed toofix hello incompatibility between source and destination stores.</span></span>

    ![Schema toewijzen](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. <span data-ttu-id="70f28-186">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="70f28-186">Click **Next**.</span></span>

## <a name="configure-hello-performance-settings"></a><span data-ttu-id="70f28-187">Hallo prestatie-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="70f28-187">Configure hello performance settings</span></span>
<span data-ttu-id="70f28-188">In Hallo prestatieconfiguraties, configureert u een Azure storage-account gebruikt voor het Faseren van Hallo gegevens voordat deze wordt geladen in SQL Data Warehouse met behulp van sommen [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span><span class="sxs-lookup"><span data-stu-id="70f28-188">In hello Performance configurations, you configure an Azure storage account used for staging hello data before it loads into SQL Data Warehouse performantly using [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span></span> <span data-ttu-id="70f28-189">Nadat de Hallo kopie is voltooid, wordt Hallo tussentijdse gegevens in de opslag automatisch opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="70f28-189">After hello copy is done, hello interim data in storage will be cleaned up automatically.</span></span>

<span data-ttu-id="70f28-190">Selecteer een bestaand Azure Storage-account en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="70f28-190">Select an existing Azure Storage account, and click **Next**.</span></span>

![Fasering blob configureren](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a><span data-ttu-id="70f28-192">Samenvattingsinformatie controleren en implementeer de pijplijn Hallo</span><span class="sxs-lookup"><span data-stu-id="70f28-192">Review summary information and deploy hello pipeline</span></span>

<span data-ttu-id="70f28-193">Hallo-configuratie controleren en klik op **voltooien** knop toodeploy Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="70f28-193">Review hello configuration and click **Finish** button toodeploy hello pipeline.</span></span>

![Gegevensfactory implementeren](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a><span data-ttu-id="70f28-195">Monitor gegevens voortgang van het laden</span><span class="sxs-lookup"><span data-stu-id="70f28-195">Monitor data loading progress</span></span>

<span data-ttu-id="70f28-196">U kunt zien Hallo implementatie voortgang en resultaten in Hallo **implementatie** pagina.</span><span class="sxs-lookup"><span data-stu-id="70f28-196">You can see hello deployment progress and results in hello **Deployment** page.</span></span>

1. <span data-ttu-id="70f28-197">Als Hallo-implementatie is voltooid, klikt u op Hallo koppeling waarin staat dat **Klik hier toomonitor kopieerpijplijn** toomonitor gegevens te laden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="70f28-197">Once hello deployment is done, click hello link that says **Click here toomonitor copy pipeline** toomonitor data loading progress.</span></span>

    ![De pijplijn bewaken](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. <span data-ttu-id="70f28-199">Hallo nieuw gemaakte **DWLoadData fromSQLServer** gegevens laden van de pijplijn wordt automatisch geselecteerd in Hallo links **Resource Explorer**.</span><span class="sxs-lookup"><span data-stu-id="70f28-199">hello newly created **DWLoadData-fromSQLServer** data loading pipeline is auto selected from hello left-hand **Resource Explorer**.</span></span>

    ![Pijplijn voor weergeven](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. <span data-ttu-id="70f28-201">Klik in de pipeline Hallo in het midden Hallo Configuratiescherm toosee Hallo gedetailleerde status voor elke tabel die is toegewezen tooan activiteit.</span><span class="sxs-lookup"><span data-stu-id="70f28-201">Click into hello pipeline in hello middle panel toosee hello detailed status for each table that maps tooan Activity.</span></span>

    ![Activiteit van de tabel weergeven](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. <span data-ttu-id="70f28-203">Verder op in een activiteit en ziet u Hallo gegevens bij het laden van gegevens in het rechterpaneel Hallo inclusief gegevensgrootte, rijen, doorvoer, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="70f28-203">Further click into an activity and you see hello data loading details in hello right panel including data size, rows, throughput, etc.</span></span>

    ![Details van activiteit tabel weergeven](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. <span data-ttu-id="70f28-205">toolaunch deze controle weergave hoger, gaat u tooyour SQL Data Warehouse, klikt u op **gegevens laden > Azure Data Factory**, selecteer uw gegevensfactory en kiezen **bewaken bestaande taken laden**.</span><span class="sxs-lookup"><span data-stu-id="70f28-205">toolaunch this monitoring view later, go tooyour SQL Data Warehouse, click **Load Data > Azure Data Factory**, select your factory, and choose **Monitor existing loading tasks**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70f28-206">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="70f28-206">Next steps</span></span>

<span data-ttu-id="70f28-207">toomigrate uw database tooSQL datawarehouse, Zie [Migratieoverzicht](sql-data-warehouse-overview-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="70f28-207">toomigrate your database tooSQL Data Warehouse, see [Migration overview](sql-data-warehouse-overview-migrate.md).</span></span>

<span data-ttu-id="70f28-208">toolearn meer informatie over Azure Data Factory en de mogelijkheden van de verplaatsing van gegevens Zie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="70f28-208">toolearn more about Azure Data Factory and its data movement capabilities, see hello following articles:</span></span>

- [<span data-ttu-id="70f28-209">Inleiding tooAzure Data Factory</span><span class="sxs-lookup"><span data-stu-id="70f28-209">Introduction tooAzure Data Factory</span></span>](../data-factory/data-factory-introduction.md)
- [<span data-ttu-id="70f28-210">Verplaatsen van gegevens met behulp van kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="70f28-210">Move data by using Copy Activity</span></span>](../data-factory/data-factory-data-movement-activities.md)
- [<span data-ttu-id="70f28-211">Verplaatsen van gegevens tooand van Azure SQL Data Warehouse met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="70f28-211">Move data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

<span data-ttu-id="70f28-212">tooexplore uw gegevens in SQL Data Warehouse, Zie Hallo volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="70f28-212">tooexplore your data in SQL Data Warehouse, see hello following articles:</span></span>

- [<span data-ttu-id="70f28-213">Verbinding maken met tooSQL Data Warehouse met Visual Studio en SSDT</span><span class="sxs-lookup"><span data-stu-id="70f28-213">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>](sql-data-warehouse-query-visual-studio.md)
- <span data-ttu-id="70f28-214">[Visuele gegevens met Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="70f28-214">[Visual data with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span></span>

<!-- Azure references -->
[Azure Portal]: https://portal.azure.com
