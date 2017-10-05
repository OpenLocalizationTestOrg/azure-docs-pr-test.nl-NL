---
title: Excel verbinden met de SQL Database | Microsoft Docs
description: Leer hoe u Microsoft Excel verbindt met Azure SQL Database in de cloud. Gegevens importeren in Excel voor rapportage en gegevens verkenning.
services: sql-database
keywords: excel verbinden met sql, gegevens importeren in excel
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
ms.openlocfilehash: 97344d7c0be38b3092a3224074d486b5bb984176
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-excel-to-an-azure-sql-database-and-create-a-report"></a><span data-ttu-id="89ff2-105">Excel verbinden met een Azure SQL database en een rapport maken</span><span class="sxs-lookup"><span data-stu-id="89ff2-105">Connect Excel to an Azure SQL database and create a report</span></span>

<span data-ttu-id="89ff2-106">Excel verbinden met een SQL-database in de cloud en gegevens importeren en tabellen en grafieken op basis van waarden in de database maken.</span><span class="sxs-lookup"><span data-stu-id="89ff2-106">Connect Excel to a SQL database in the cloud and import data and create tables and charts based on values in the database.</span></span> <span data-ttu-id="89ff2-107">In deze zelfstudie stelt u de verbinding tussen Excel en een databasetabel in, slaat u het bestand met de gegevens en de verbindingsinformatie voor Excel op en maakt u vervolgens een draaigrafiek uit de databasewaarden.</span><span class="sxs-lookup"><span data-stu-id="89ff2-107">In this tutorial you will set up the connection between Excel and a database table, save the file that stores data and the connection information for Excel, and then create a pivot chart from the database values.</span></span>

<span data-ttu-id="89ff2-108">Voordat u begint hebt u een SQL Database in Azure nodig.</span><span class="sxs-lookup"><span data-stu-id="89ff2-108">You'll need a SQL database in Azure before you get started.</span></span> <span data-ttu-id="89ff2-109">Als u deze niet hebt, raadpleegt u [Uw eerste SQL Database maken](sql-database-get-started-portal.md) om een database met voorbeeldgegevens binnen enkele minuten in te stellen.</span><span class="sxs-lookup"><span data-stu-id="89ff2-109">If you don't have one, see [Create your first SQL database](sql-database-get-started-portal.md) to get a database with sample data up and running in a few minutes.</span></span> <span data-ttu-id="89ff2-110">In dit artikel, zult u voorbeeldgegevens importeren in Excel van dat artikel, maar u kunt dezelfde stappen volgen met uw eigen gegevens.</span><span class="sxs-lookup"><span data-stu-id="89ff2-110">In this article, you'll import sample data into Excel from that article, but you can follow similar steps with your own data.</span></span>

<span data-ttu-id="89ff2-111">U hebt ook een kopie van Excel nodig.</span><span class="sxs-lookup"><span data-stu-id="89ff2-111">You'll also need a copy of Excel.</span></span> <span data-ttu-id="89ff2-112">Dit artikel gebruikt [Microsoft Excel 2016](https://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="89ff2-112">This article uses [Microsoft Excel 2016](https://products.office.com/).</span></span>

## <a name="connect-excel-to-a-sql-database-and-create-an-odc-file"></a><span data-ttu-id="89ff2-113">Excel verbinden met een SQL Database en een odc-bestand maken</span><span class="sxs-lookup"><span data-stu-id="89ff2-113">Connect Excel to a SQL database and create an odc file</span></span>
1. <span data-ttu-id="89ff2-114">Open Excel om het programme te verbinden met SQL Database, en maak een nieuwe werkmap of open een bestaande Excel-werkmap.</span><span class="sxs-lookup"><span data-stu-id="89ff2-114">To connect Excel to SQL database, open Excel and then create a new workbook or open an existing Excel workbook.</span></span>
2. <span data-ttu-id="89ff2-115">Klik in de menubalk bovenaan de pagina  op**Gegevens**, klik op **Van andere bronnen**, en klik vervolgens op **Van SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="89ff2-115">In the menu bar at the top of the page click **Data**, click **From Other Sources**, and then click **From SQL Server**.</span></span>
   
   ![Selecteer gegevensbron: Excel verbinden met SQL Database.](./media/sql-database-connect-excel/excel_data_source.png)
   
   <span data-ttu-id="89ff2-117">De wizard Gegevensverbinding wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="89ff2-117">The Data Connection Wizard opens.</span></span>
3. <span data-ttu-id="89ff2-118">In het dialoogvenster **Verbinding maken met databaseserver** typt u de **servernaam** van de SQL Database die u wilt verbinden in het formulier <*servername*>**. database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="89ff2-118">In the **Connect to Database Server** dialog box, type the SQL Database **Server name** you want to connect to in the form <*servername*>**.database.windows.net**.</span></span> <span data-ttu-id="89ff2-119">Bijvoorbeeld: **adworkserver.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="89ff2-119">For example, **adworkserver.database.windows.net**.</span></span>
4. <span data-ttu-id="89ff2-120">Klik onder **aanmeldingsreferenties** op **Gebruik de volgende gebruikersnaam en wachtwoord**, typ de **gebruikersnaam** en het **wachtwoord** dat u hebt ingesteld voor de SQL Databaseserver en klik vervolgens op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="89ff2-120">Under **Log on credentials**, click **Use the following User Name and Password**, type the **User Name** and **Password** you set up for the SQL Database server when you created it, and then click **Next**.</span></span>
   
   ![Typ de servernaam en aanmeldingsreferenties in](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > <span data-ttu-id="89ff2-122">Afhankelijk van uw netwerkomgeving kunt u mogelijk geen verbinding maken of kan de verbinding verbroken worden als de server van de SQL Database geen verkeer van het IP-adres van de client toestaat.</span><span class="sxs-lookup"><span data-stu-id="89ff2-122">Depending on your network environment, you may not be able to connect or you may lose the connection if the SQL Database server doesn't allow traffic from your client IP address.</span></span> <span data-ttu-id="89ff2-123">Ga naar de [Azure-portal](https://portal.azure.com/), klik op SQL-servers, klik op uw server, klik op firewall onder instellingen en voeg uw client-IP-adres toe.</span><span class="sxs-lookup"><span data-stu-id="89ff2-123">Go to the [Azure portal](https://portal.azure.com/), click SQL servers, click your server, click firewall under settings and add your client IP address.</span></span> <span data-ttu-id="89ff2-124">Zie [Firewallinstellingen configureren](sql-database-configure-firewall-settings.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="89ff2-124">See [How to configure firewall settings](sql-database-configure-firewall-settings.md) for details.</span></span>
   > 
   > 
5. <span data-ttu-id="89ff2-125">In het dialoogvenster **Database en tabel selecteren**, selecteert u de database waarmee u wilt werken uit de lijst en klik vervolgens op de tabellen of weergaven waarmee u wilt werken (we hebben **vGetAllCategories** gekozen), en klik vervolgens op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="89ff2-125">In the **Select Database and Table** dialog, select the database you want to work with from the list, and then click the tables or views you want to work with (we chose **vGetAllCategories**), and then click **Next**.</span></span>
   
    ![Selecteer een database en tabel.](./media/sql-database-connect-excel/select-database-and-table.png)
   
    <span data-ttu-id="89ff2-127">Het dialoogvenster **Bestand opslaan en voltooien** wordt geopend. Hier geeft u informatie over het Office database connection (*.odc) bestand dat Excel gebruikt.</span><span class="sxs-lookup"><span data-stu-id="89ff2-127">The **Save Data Connection File and Finish** dialog box opens, where you provide information about the Office database connection (*.odc) file that Excel uses.</span></span> <span data-ttu-id="89ff2-128">U kunt de standaardinstellingen laten staan of uw selecties aanpassen.</span><span class="sxs-lookup"><span data-stu-id="89ff2-128">You can leave the defaults or customize your selections.</span></span>
6. <span data-ttu-id="89ff2-129">U kunt de standaardinstellingen laten staan, maar let in het bijzonder op de **bestandsnaam**.</span><span class="sxs-lookup"><span data-stu-id="89ff2-129">You can leave the defaults, but note the **File Name** in particular.</span></span> <span data-ttu-id="89ff2-130">Een **beschrijving**, een **beschrijvende naam** en **zoekwoorden** helpen u en andere gebruikers te onthouden wat u koppelt en de koppeling te vinden.</span><span class="sxs-lookup"><span data-stu-id="89ff2-130">A **Description**, a **Friendly Name**, and **Search Keywords** help you and other users remember what you're connecting to and find the connection.</span></span> <span data-ttu-id="89ff2-131">Klik op **Altijd proberen dit bestand te gebruiken om gegevens te vernieuwen** als u wilt dat verbindingsgegevens worden opgeslagen in het odc-bestand, zodat deze bijgewerkt kan worden wanneer u verbinding maakt en klik vervolgens op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="89ff2-131">Click **Always attempt to use this file to refresh data** if you want connection information stored in the odc file so it can update when you connect to it, and then click **Finish**.</span></span>
   
    ![Opslaan van een odc-bestand](./media/sql-database-connect-excel/save-odc-file.png)
   
    <span data-ttu-id="89ff2-133">Het dialoogvenster **Importeren van gegevens** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="89ff2-133">The **Import data** dialog box appears.</span></span>

## <a name="import-the-data-into-excel-and-create-a-pivot-chart"></a><span data-ttu-id="89ff2-134">Importeer de gegevens in Excel en maak een draaigrafiek.</span><span class="sxs-lookup"><span data-stu-id="89ff2-134">Import the data into Excel and create a pivot chart</span></span>
<span data-ttu-id="89ff2-135">Nu de verbinding tot stand is gebracht en het bestand met gegevens en de koppelingsinformatie is gemaakt, leest u om de gegevens te importeren.</span><span class="sxs-lookup"><span data-stu-id="89ff2-135">Now that you've established the connection and created the file with data and connection information, you're reading to import the data.</span></span>

1. <span data-ttu-id="89ff2-136">In het dialoogvenster **Gegevens importeren** , klikt u op de optie die u wilt gebruiken om uw gegevens weer te geven in het werkblad en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="89ff2-136">In the **Import Data** dialog, click the option you want for presenting your data in the worksheet and then click **OK**.</span></span> <span data-ttu-id="89ff2-137">We hebben **draaigrafiek** gekozen.</span><span class="sxs-lookup"><span data-stu-id="89ff2-137">We chose **PivotChart**.</span></span> <span data-ttu-id="89ff2-138">U kunt ook kiezen voor **Nieuw werkblad** of **Deze gegevens toevoegen aan een gegevensmodel**.</span><span class="sxs-lookup"><span data-stu-id="89ff2-138">You can also choose to create a **New worksheet** or to **Add this data to a Data Model**.</span></span> <span data-ttu-id="89ff2-139">Zie voor meer informatie over gegevensmodellen [Een gegevensmodel maken in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span><span class="sxs-lookup"><span data-stu-id="89ff2-139">For more information on Data Models, see [Create a data model in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span></span> <span data-ttu-id="89ff2-140">Klik op **eigenschappen** om informatie over het odc-bestand dat u in de vorige stap hebt gemaakt te bekijken en om opties te kiezen voor het vernieuwen van de gegevens.</span><span class="sxs-lookup"><span data-stu-id="89ff2-140">Click **Properties** to explore information about the odc file you created in the previous step and to choose options for refreshing the data.</span></span>
   
    ![De indeling kiezen voor gegevens in Excel](./media/sql-database-connect-excel/import-data.png)
   
    <span data-ttu-id="89ff2-142">Het werkblad heeft nu een lege draaitabel en grafiek.</span><span class="sxs-lookup"><span data-stu-id="89ff2-142">The worksheet now has an empty pivot table and chart.</span></span>
2. <span data-ttu-id="89ff2-143">Onder **PivotTable-velden**, selecteert u alle selectievakjes voor de velden die u wilt weergeven.</span><span class="sxs-lookup"><span data-stu-id="89ff2-143">Under **PivotTable Fields**, select all the check-boxes for the fields you want to view.</span></span>
   
    ![Databaserapport configureren.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> <span data-ttu-id="89ff2-145">Als u andere Excel-werkmappen en -werkbladen wilt verbinden met de database, klikt u op **Gegevens**, **Verbindingen** en **Toevoegen** en kiest u de koppeling die u hebt gemaakt in de lijst en klik vervolgens op **Openen**.</span><span class="sxs-lookup"><span data-stu-id="89ff2-145">If you want to connect other Excel workbooks and worksheets to the database, click **Data**, click **Connections**, click **Add**, choose the connection you created from the list, and then click **Open**.</span></span>
> <span data-ttu-id="89ff2-146">![Een verbinding openen vanuit een andere werkmap](./media/sql-database-connect-excel/open-from-another-workbook.png)</span><span class="sxs-lookup"><span data-stu-id="89ff2-146">![Open a connection from another workbook](./media/sql-database-connect-excel/open-from-another-workbook.png)</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="89ff2-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="89ff2-147">Next steps</span></span>
* <span data-ttu-id="89ff2-148">Leer hoe u [SQL Database koppelt met SQL Server Management Studio](sql-database-connect-query-ssms.md) voor geavanceerd uitvoeren van query's en analyses.</span><span class="sxs-lookup"><span data-stu-id="89ff2-148">Learn how to [Connect to SQL Database with SQL Server Management Studio](sql-database-connect-query-ssms.md) for advanced querying and analysis.</span></span>
* <span data-ttu-id="89ff2-149">Meer informatie over de voordelen van [elastische groepen](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="89ff2-149">Learn about the benefits of [elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="89ff2-150">Leer hoe u [ een webtoepassing maakt die verbinding maakt met SQL Database op de back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="89ff2-150">Learn how to [create a web application that connects to SQL Database on the back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span>

