---
title: aaaConnect Excel tooSQL Database | Microsoft Docs
description: Meer informatie over hoe tooconnect Microsoft Excel tooAzure SQL-database in de cloud Hallo. Gegevens importeren in Excel voor rapportage en gegevens verkenning.
services: sql-database
keywords: verbinding maken met excel toosql, gegevens tooexcel importeren
documentationcenter: 
author: joseidz
manager: jhubbard
editor: 
ms.assetid: 906924bc-2707-48d3-bac6-397976a0409d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: jhubbard
ms.openlocfilehash: 0048849432023145bd1009d45b6d9b64a9c7ac3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-tooan-azure-sql-database-and-create-a-report"></a><span data-ttu-id="64e76-105">Verbinding maken met Excel tooan Azure SQL database en een rapport maken</span><span class="sxs-lookup"><span data-stu-id="64e76-105">Connect Excel tooan Azure SQL database and create a report</span></span>

<span data-ttu-id="64e76-106">Verbinding maken met Excel tooa SQL database in de cloud Hallo en gegevens importeren en tabellen en grafieken op basis van waarden in Hallo-database maken.</span><span class="sxs-lookup"><span data-stu-id="64e76-106">Connect Excel tooa SQL database in hello cloud and import data and create tables and charts based on values in hello database.</span></span> <span data-ttu-id="64e76-107">In deze zelfstudie u Hallo verbinding tussen Excel en een databasetabel stelt Hallo-bestand met gegevens en Hallo verbindingsinformatie voor Excel opslaan, en maak vervolgens een draaigrafiek uit Hallo databasewaarden.</span><span class="sxs-lookup"><span data-stu-id="64e76-107">In this tutorial you will set up hello connection between Excel and a database table, save hello file that stores data and hello connection information for Excel, and then create a pivot chart from hello database values.</span></span>

<span data-ttu-id="64e76-108">Voordat u begint hebt u een SQL Database in Azure nodig.</span><span class="sxs-lookup"><span data-stu-id="64e76-108">You'll need a SQL database in Azure before you get started.</span></span> <span data-ttu-id="64e76-109">Als u niet hebt, raadpleegt u [uw eerste SQL-database maken](sql-database-get-started-portal.md) tooget een database met voorbeeldgegevens binnen enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="64e76-109">If you don't have one, see [Create your first SQL database](sql-database-get-started-portal.md) tooget a database with sample data up and running in a few minutes.</span></span> <span data-ttu-id="64e76-110">In dit artikel, zult u voorbeeldgegevens importeren in Excel van dat artikel, maar u kunt dezelfde stappen volgen met uw eigen gegevens.</span><span class="sxs-lookup"><span data-stu-id="64e76-110">In this article, you'll import sample data into Excel from that article, but you can follow similar steps with your own data.</span></span>

<span data-ttu-id="64e76-111">U hebt ook een kopie van Excel nodig.</span><span class="sxs-lookup"><span data-stu-id="64e76-111">You'll also need a copy of Excel.</span></span> <span data-ttu-id="64e76-112">Dit artikel gebruikt [Microsoft Excel 2016](https://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="64e76-112">This article uses [Microsoft Excel 2016](https://products.office.com/).</span></span>

## <a name="connect-excel-tooa-sql-database-and-create-an-odc-file"></a><span data-ttu-id="64e76-113">Verbinding maken met Excel tooa SQL database en een odc-bestand maken</span><span class="sxs-lookup"><span data-stu-id="64e76-113">Connect Excel tooa SQL database and create an odc file</span></span>
1. <span data-ttu-id="64e76-114">tooconnect Excel tooSQL database open Excel en maak een nieuwe werkmap of open een bestaande Excel-werkmap.</span><span class="sxs-lookup"><span data-stu-id="64e76-114">tooconnect Excel tooSQL database, open Excel and then create a new workbook or open an existing Excel workbook.</span></span>
2. <span data-ttu-id="64e76-115">Klik in de menubalk Hallo bovenaan Hallo Hallo pagina **gegevens**, klikt u op **van andere bronnen**, en klik vervolgens op **van SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="64e76-115">In hello menu bar at hello top of hello page click **Data**, click **From Other Sources**, and then click **From SQL Server**.</span></span>
   
   ![Selecteer gegevensbron: verbinding maken met Excel tooSQL database.](./media/sql-database-connect-excel/excel_data_source.png)
   
   <span data-ttu-id="64e76-117">Hallo Wizard Gegevensverbinding wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="64e76-117">hello Data Connection Wizard opens.</span></span>
3. <span data-ttu-id="64e76-118">In Hallo **tooDatabase Server verbinding** in het dialoogvenster type Hallo SQL-Database **servernaam** tooconnect tooin Hallo formulier <*servername* > **. database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="64e76-118">In hello **Connect tooDatabase Server** dialog box, type hello SQL Database **Server name** you want tooconnect tooin hello form <*servername*>**.database.windows.net**.</span></span> <span data-ttu-id="64e76-119">Bijvoorbeeld: **adworkserver.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="64e76-119">For example, **adworkserver.database.windows.net**.</span></span>
4. <span data-ttu-id="64e76-120">Onder **aanmeldingsreferenties**, klikt u op **gebruik Hallo volgende gebruikersnaam en wachtwoord**, type Hallo **gebruikersnaam** en **wachtwoord** u is ingesteld voor Hallo SQL Database-server wanneer u het hebt gemaakt en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="64e76-120">Under **Log on credentials**, click **Use hello following User Name and Password**, type hello **User Name** and **Password** you set up for hello SQL Database server when you created it, and then click **Next**.</span></span>
   
   ![Typ de servernaam en aanmeldingsreferenties in Hallo server](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > <span data-ttu-id="64e76-122">Afhankelijk van uw netwerkomgeving u mogelijk niet kunnen tooconnect of Hallo verbinding mogelijk wordt verbroken als verkeer van de IP-adres van uw client Hallo SQL Database-server niet is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="64e76-122">Depending on your network environment, you may not be able tooconnect or you may lose hello connection if hello SQL Database server doesn't allow traffic from your client IP address.</span></span> <span data-ttu-id="64e76-123">Ga toohello [Azure-portal](https://portal.azure.com/)op SQL-servers, klikt u op uw server, klikt u op firewall onder instellingen en voeg uw client-IP-adres.</span><span class="sxs-lookup"><span data-stu-id="64e76-123">Go toohello [Azure portal](https://portal.azure.com/), click SQL servers, click your server, click firewall under settings and add your client IP address.</span></span> <span data-ttu-id="64e76-124">Zie [hoe tooconfigure firewall-instellingen](sql-database-configure-firewall-settings.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="64e76-124">See [How tooconfigure firewall settings](sql-database-configure-firewall-settings.md) for details.</span></span>
   > 
   > 
5. <span data-ttu-id="64e76-125">In Hallo **Database en tabel selecteren** dialoogvenster, selecteer Hallo database u wilt toowork met uit Hallo lijst en klik vervolgens op Hallo tabellen of weergaven die u toowork met wilt (We hebben gekozen **vGetAllCategories**), en vervolgens Klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="64e76-125">In hello **Select Database and Table** dialog, select hello database you want toowork with from hello list, and then click hello tables or views you want toowork with (we chose **vGetAllCategories**), and then click **Next**.</span></span>
   
    ![Selecteer een database en tabel.](./media/sql-database-connect-excel/select-database-and-table.png)
   
    <span data-ttu-id="64e76-127">Hallo **bestand opslaan en voltooien** in het dialoogvenster wordt geopend, waarin u informatie over Hallo Office database connection (*.odc) bestand dat Excel gebruikt opgeven.</span><span class="sxs-lookup"><span data-stu-id="64e76-127">hello **Save Data Connection File and Finish** dialog box opens, where you provide information about hello Office database connection (*.odc) file that Excel uses.</span></span> <span data-ttu-id="64e76-128">U kunt Hallo standaardinstellingen laten staan of uw selecties aanpassen.</span><span class="sxs-lookup"><span data-stu-id="64e76-128">You can leave hello defaults or customize your selections.</span></span>
6. <span data-ttu-id="64e76-129">U kunt laten Hallo standaardinstellingen, maar Opmerking Hallo **bestandsnaam** in het bijzonder.</span><span class="sxs-lookup"><span data-stu-id="64e76-129">You can leave hello defaults, but note hello **File Name** in particular.</span></span> <span data-ttu-id="64e76-130">Een **beschrijving**, een **beschrijvende naam**, en **zoekwoorden** helpen u en andere gebruikers te onthouden wat u verbinding maakt tooand Hallo verbinding vinden.</span><span class="sxs-lookup"><span data-stu-id="64e76-130">A **Description**, a **Friendly Name**, and **Search Keywords** help you and other users remember what you're connecting tooand find hello connection.</span></span> <span data-ttu-id="64e76-131">Klik op **altijd proberen toouse deze bestandsgegevens toorefresh** als u wilt dat verbindingsgegevens worden opgeslagen in Hallo ODC-bestand, zodat deze bijgewerkt kan wanneer u verbinding maken met tooit en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="64e76-131">Click **Always attempt toouse this file toorefresh data** if you want connection information stored in hello odc file so it can update when you connect tooit, and then click **Finish**.</span></span>
   
    ![Opslaan van een odc-bestand](./media/sql-database-connect-excel/save-odc-file.png)
   
    <span data-ttu-id="64e76-133">Hallo **gegevens importeren** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="64e76-133">hello **Import data** dialog box appears.</span></span>

## <a name="import-hello-data-into-excel-and-create-a-pivot-chart"></a><span data-ttu-id="64e76-134">Hallo-gegevens importeren in Excel en maak een draaigrafiek.</span><span class="sxs-lookup"><span data-stu-id="64e76-134">Import hello data into Excel and create a pivot chart</span></span>
<span data-ttu-id="64e76-135">Nu dat u hebt ingesteld Hallo verbinding en gemaakte Hallo-bestand met gegevens en de verbindingsinformatie, leest u tooimport Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="64e76-135">Now that you've established hello connection and created hello file with data and connection information, you're reading tooimport hello data.</span></span>

1. <span data-ttu-id="64e76-136">In Hallo **gegevens importeren** dialoogvenster, klikt u op Hallo gewenste optie voor uw gegevens weer in Hallo werkblad en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="64e76-136">In hello **Import Data** dialog, click hello option you want for presenting your data in hello worksheet and then click **OK**.</span></span> <span data-ttu-id="64e76-137">We hebben **draaigrafiek** gekozen.</span><span class="sxs-lookup"><span data-stu-id="64e76-137">We chose **PivotChart**.</span></span> <span data-ttu-id="64e76-138">U kunt ook toocreate een **nieuw werkblad** of te**toevoegen van deze gegevens tooa gegevensmodel**.</span><span class="sxs-lookup"><span data-stu-id="64e76-138">You can also choose toocreate a **New worksheet** or too**Add this data tooa Data Model**.</span></span> <span data-ttu-id="64e76-139">Zie voor meer informatie over gegevensmodellen [Een gegevensmodel maken in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span><span class="sxs-lookup"><span data-stu-id="64e76-139">For more information on Data Models, see [Create a data model in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span></span> <span data-ttu-id="64e76-140">Klik op **eigenschappen** tooexplore meer informatie over Hallo ODC-bestand u hebt gemaakt in Hallo vorige stap en toochoose opties voor het vernieuwen van Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="64e76-140">Click **Properties** tooexplore information about hello odc file you created in hello previous step and toochoose options for refreshing hello data.</span></span>
   
    ![Hallo-indeling voor gegevens kiezen in Excel](./media/sql-database-connect-excel/import-data.png)
   
    <span data-ttu-id="64e76-142">Hallo werkblad heeft nu een lege draaitabel en grafiek.</span><span class="sxs-lookup"><span data-stu-id="64e76-142">hello worksheet now has an empty pivot table and chart.</span></span>
2. <span data-ttu-id="64e76-143">Onder **PivotTable-Fields**, schakel alle selectievakjes voor Hallo Hallo velden die u wilt tooview.</span><span class="sxs-lookup"><span data-stu-id="64e76-143">Under **PivotTable Fields**, select all hello check-boxes for hello fields you want tooview.</span></span>
   
    ![Databaserapport configureren.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> <span data-ttu-id="64e76-145">Als u wilt dat tooconnect andere Excel-werkmappen en werkbladen toohello-database, klikt u op **gegevens**, klikt u op **verbindingen**, klikt u op **toevoegen**, kies Hallo-verbinding die u hebt gemaakt in de lijst Hallo en klik vervolgens op **Open**.</span><span class="sxs-lookup"><span data-stu-id="64e76-145">If you want tooconnect other Excel workbooks and worksheets toohello database, click **Data**, click **Connections**, click **Add**, choose hello connection you created from hello list, and then click **Open**.</span></span>
> <span data-ttu-id="64e76-146">![Een verbinding openen vanuit een andere werkmap](./media/sql-database-connect-excel/open-from-another-workbook.png)</span><span class="sxs-lookup"><span data-stu-id="64e76-146">![Open a connection from another workbook](./media/sql-database-connect-excel/open-from-another-workbook.png)</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="64e76-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="64e76-147">Next steps</span></span>
* <span data-ttu-id="64e76-148">Meer informatie over hoe te[tooSQL Database met SQL Server Management Studio verbinding](sql-database-connect-query-ssms.md) voor geavanceerde query's en analyse.</span><span class="sxs-lookup"><span data-stu-id="64e76-148">Learn how too[Connect tooSQL Database with SQL Server Management Studio](sql-database-connect-query-ssms.md) for advanced querying and analysis.</span></span>
* <span data-ttu-id="64e76-149">Meer informatie over de voordelen van Hallo [elastische pools](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="64e76-149">Learn about hello benefits of [elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="64e76-150">Meer informatie over hoe te[maken van een webtoepassing die verbinding tooSQL Database op Hallo back-end maakt](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="64e76-150">Learn how too[create a web application that connects tooSQL Database on hello back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span>

