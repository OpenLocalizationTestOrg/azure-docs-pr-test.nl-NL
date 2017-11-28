---
title: Verbinding maken met Database tooAzure voor MySQL van MySQL Workbench | Microsoft Docs
description: Deze snelstartgids biedt Hallo stappen toouse MySQL Workbench tooconnect en query gegevens uit Azure-Database voor MySQL.
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: c64fcb9bb99ba06aa3a95eec420d5d5ef4a31d14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-tooconnect-and-query-data"></a><span data-ttu-id="81344-103">Azure MySQL-Database: gebruik MySQL Workbench tooconnect en query-gegevens</span><span class="sxs-lookup"><span data-stu-id="81344-103">Azure Database for MySQL: Use MySQL Workbench tooconnect and query data</span></span>
<span data-ttu-id="81344-104">Deze snelstartgids demonstreert hoe tooconnect tooan Azure Database voor het gebruik van MySQL Hallo toepassing MySQL-Workbench.</span><span class="sxs-lookup"><span data-stu-id="81344-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using hello MySQL Workbench application.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="81344-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="81344-105">Prerequisites</span></span>
<span data-ttu-id="81344-106">Deze snelstartgids Hallo bronnen die zijn gemaakt in een van deze handleidingen als uitgangspunt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="81344-106">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="81344-107">Een Azure-database voor een MySQL-server maken met behulp van Azure Portal</span><span class="sxs-lookup"><span data-stu-id="81344-107">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="81344-108">Een Azure-database voor een MySQL-server maken met behulp van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="81344-108">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a><span data-ttu-id="81344-109">MySQL-Workbench installeren</span><span class="sxs-lookup"><span data-stu-id="81344-109">Install MySQL Workbench</span></span>
<span data-ttu-id="81344-110">Download en installeer MySQL Workbench op uw computer uit [Hallo MySQL website](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="81344-110">Download and install MySQL Workbench on your computer from [hello MySQL website](https://dev.mysql.com/downloads/workbench/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="81344-111">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="81344-111">Get connection information</span></span>
<span data-ttu-id="81344-112">Hallo verbinding informatie die nodig is tooconnect toohello Azure Database voor MySQL niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="81344-112">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="81344-113">U moet Hallo van server volledig gekwalificeerde servernaam en aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="81344-113">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="81344-114">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="81344-114">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="81344-115">Hallo links menu in Azure-portal en klik op **alle resources** en zoek naar Hallo-server die u hebt gemaakt, zoals **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="81344-115">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>

3. <span data-ttu-id="81344-116">Klik op Hallo servernaam.</span><span class="sxs-lookup"><span data-stu-id="81344-116">Click hello server name.</span></span>

4. <span data-ttu-id="81344-117">Selecteer Hallo-server **eigenschappen** pagina.</span><span class="sxs-lookup"><span data-stu-id="81344-117">Select hello server's **Properties** page.</span></span> <span data-ttu-id="81344-118">Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**.</span><span class="sxs-lookup"><span data-stu-id="81344-118">Make a note of hello **Server name** and **Server admin login name**.</span></span>

 ![Azure servernaam MySQL-Database](./media/connect-workbench/1-server-properties-name-login.png)
 
5. <span data-ttu-id="81344-120">Als u uw aanmeldingsgegevens server bent vergeten, gaat u toohello **overzicht** pagina tooview Hallo Server admin-aanmeldingsnaam en, indien nodig, opnieuw ingesteld wachtwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="81344-120">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-toohello-server-using-mysql-workbench"></a><span data-ttu-id="81344-121">Verbinding maken met behulp van MySQL Workbench toohello-server</span><span class="sxs-lookup"><span data-stu-id="81344-121">Connect toohello server using MySQL Workbench</span></span> 
<span data-ttu-id="81344-122">tooAzure tooconnect MySQL-server met Hallo GUI-hulpprogramma MySQL Workbench:</span><span class="sxs-lookup"><span data-stu-id="81344-122">tooconnect tooAzure MySQL server using hello GUI tool MySQL Workbench:</span></span>

1.  <span data-ttu-id="81344-123">Hallo MySQL Workbench van toepassing op uw computer starten.</span><span class="sxs-lookup"><span data-stu-id="81344-123">Launch hello MySQL Workbench application on your computer.</span></span> 

2.  <span data-ttu-id="81344-124">In **Setup nieuwe verbinding** dialoogvenster en voer de volgende informatie op Hallo Hallo **Parameters** tabblad:</span><span class="sxs-lookup"><span data-stu-id="81344-124">In **Setup New Connection** dialog box, enter hello following information on hello **Parameters** tab:</span></span>

    ![nieuwe verbinding instellen](./media/connect-workbench/2-setup-new-connection.png)

    | <span data-ttu-id="81344-126">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="81344-126">**Setting**</span></span> | <span data-ttu-id="81344-127">**Voorgestelde waarde**</span><span class="sxs-lookup"><span data-stu-id="81344-127">**Suggested value**</span></span> | <span data-ttu-id="81344-128">**Beschrijving van veld**</span><span class="sxs-lookup"><span data-stu-id="81344-128">**Field description**</span></span> |
    |---|---|---|
    |   <span data-ttu-id="81344-129">Verbindingsnaam</span><span class="sxs-lookup"><span data-stu-id="81344-129">Connection Name</span></span> | <span data-ttu-id="81344-130">Demo-verbinding</span><span class="sxs-lookup"><span data-stu-id="81344-130">Demo Connection</span></span> | <span data-ttu-id="81344-131">Geef een label op voor deze verbinding.</span><span class="sxs-lookup"><span data-stu-id="81344-131">Specify a label for this connection.</span></span> |
    | <span data-ttu-id="81344-132">Verbindingsmethode</span><span class="sxs-lookup"><span data-stu-id="81344-132">Connection Method</span></span> | <span data-ttu-id="81344-133">Standard (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="81344-133">Standard (TCP/IP)</span></span> | <span data-ttu-id="81344-134">Standard (TCP/IP) is voldoende.</span><span class="sxs-lookup"><span data-stu-id="81344-134">Standard (TCP/IP) is sufficient.</span></span> |
    | <span data-ttu-id="81344-135">Hostnaam</span><span class="sxs-lookup"><span data-stu-id="81344-135">Hostname</span></span> | <span data-ttu-id="81344-136">*servernaam*</span><span class="sxs-lookup"><span data-stu-id="81344-136">*server name*</span></span> | <span data-ttu-id="81344-137">Hallo-server de naam van waarde dat werd gebruikt toen u eerder hebt gemaakt hello Azure Database voor MySQL opgeven.</span><span class="sxs-lookup"><span data-stu-id="81344-137">Specify hello server name value that was used when you created hello Azure Database for MySQL earlier.</span></span> <span data-ttu-id="81344-138">De server in ons voorbeeld is myserver4demo.mysql.database.azure.com. Gebruik Hallo volledig gekwalificeerde domeinnaam (\*. mysql.database.azure.com) zoals weergegeven in Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="81344-138">Our example server shown is myserver4demo.mysql.database.azure.com. Use hello fully qualified domain name (\*.mysql.database.azure.com) as shown in hello example.</span></span> <span data-ttu-id="81344-139">Stappen Hallo in Hallo vorige sectie tooget Hallo verbindingsgegevens als u niet meer de servernaam van uw weet.</span><span class="sxs-lookup"><span data-stu-id="81344-139">Follow hello steps in hello previous section tooget hello connection information if you do not remember your server name.</span></span>  |
    | <span data-ttu-id="81344-140">Poort</span><span class="sxs-lookup"><span data-stu-id="81344-140">Port</span></span> | <span data-ttu-id="81344-141">3306</span><span class="sxs-lookup"><span data-stu-id="81344-141">3306</span></span> | <span data-ttu-id="81344-142">Gebruik altijd poort 3306 bij het verbinden van tooAzure Database voor MySQL.</span><span class="sxs-lookup"><span data-stu-id="81344-142">Always use port 3306 when connecting tooAzure Database for MySQL.</span></span> |
    | <span data-ttu-id="81344-143">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="81344-143">Username</span></span> |  <span data-ttu-id="81344-144">*aanmeldnaam van serverbeheerder*</span><span class="sxs-lookup"><span data-stu-id="81344-144">*server admin login name*</span></span> | <span data-ttu-id="81344-145">Typ Hallo server admin aanmelding gebruikersnaam opgegeven toen u eerder hebt gemaakt hello Azure Database voor MySQL.</span><span class="sxs-lookup"><span data-stu-id="81344-145">Type in hello server admin login username supplied when you created hello Azure Database for MySQL earlier.</span></span> <span data-ttu-id="81344-146">De gebruikersnaam in ons voorbeeld is myadmin@myserver4demo.</span><span class="sxs-lookup"><span data-stu-id="81344-146">Our example username is myadmin@myserver4demo.</span></span> <span data-ttu-id="81344-147">Stappen Hallo in Hallo vorige sectie tooget Hallo verbindingsgegevens als u niet meer Hallo gebruikersnaam weet.</span><span class="sxs-lookup"><span data-stu-id="81344-147">Follow hello steps in hello previous section tooget hello connection information if you do not remember hello username.</span></span> <span data-ttu-id="81344-148">Hallo-indeling is  *username@servername* .</span><span class="sxs-lookup"><span data-stu-id="81344-148">hello format is *username@servername*.</span></span>
    | <span data-ttu-id="81344-149">Wachtwoord</span><span class="sxs-lookup"><span data-stu-id="81344-149">Password</span></span> | <span data-ttu-id="81344-150">Uw wachtwoord</span><span class="sxs-lookup"><span data-stu-id="81344-150">your password</span></span> | <span data-ttu-id="81344-151">Klik op **Store in kluis...**  knop toosave Hallo wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="81344-151">Click **Store in Vault...** button toosave hello password.</span></span> |

3.   <span data-ttu-id="81344-152">Klik op **testverbinding** tootest als alle parameters juist zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="81344-152">Click **Test Connection** tootest if all parameters are correctly configured.</span></span> 

4.   <span data-ttu-id="81344-153">Klik op **OK** toosave Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="81344-153">Click **OK** toosave hello connection.</span></span> 

5.   <span data-ttu-id="81344-154">In de aanbieding Hallo van **MySQL verbindingen**, klik op Hallo bijbehorende tooyour tegelserver en wachten op Hallo verbinding toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="81344-154">In hello listing of **MySQL Connections**, click hello tile corresponding tooyour server and wait for hello connection toobe established.</span></span>

6.   <span data-ttu-id="81344-155">Een nieuwe SQL-tabblad is geopend met een lege editor u uw query's typt.</span><span class="sxs-lookup"><span data-stu-id="81344-155">A new SQL tab opens with a blank editor where you can type your queries.</span></span>

    > [!NOTE]
    > <span data-ttu-id="81344-156">Standaard is de beveiliging van de SSL-verbinding vereist en afgedwongen voor uw Azure-Database voor de MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="81344-156">By default, SSL connection security is required and enforced on your Azure Database for MySQL server.</span></span> <span data-ttu-id="81344-157">Geen aanvullende configuratie met SSL-certificaten is doorgaans vereist voor MySQL Workbench tooconnect tooyour server.</span><span class="sxs-lookup"><span data-stu-id="81344-157">Typically no additional configuration with SSL certificates is required for MySQL Workbench tooconnect tooyour server.</span></span> <span data-ttu-id="81344-158">Zie voor meer informatie over SSL [configureren van SSL-verbindingen in uw toepassing toosecurely tooAzure Database connect voor MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="81344-158">For more information on SSL, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span>  <span data-ttu-id="81344-159">Als u toodisable SSL moet, gaat u naar hello Azure-portal en klik Hallo verbinding beveiliging pagina toodisable Hallo afdwingen SSL verbinding in-of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="81344-159">If you need toodisable SSL, visit hello Azure portal and click hello Connection security page toodisable hello Enforce SSL connection toggle button.</span></span>

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a><span data-ttu-id="81344-160">Een tabel maken, gegevens invoegen, gegevens lezen, bijwerken van gegevens en gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="81344-160">Create a table, insert data, read data, update data, delete data</span></span>
1. <span data-ttu-id="81344-161">Kopieer en plak de voorbeeldcode SQL Hallo in een lege SQL tabblad tooillustrate voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="81344-161">Copy and paste hello sample SQL code into a blank SQL tab tooillustrate some sample data.</span></span>

    <span data-ttu-id="81344-162">Deze code maakt een lege database met de naam quickstartdb en maakt vervolgens een tabel met de naam inventory.</span><span class="sxs-lookup"><span data-stu-id="81344-162">This code creates an empty database named quickstartdb, and then creates a sample table named inventory.</span></span> <span data-ttu-id="81344-163">Hiermee voegt een aantal rijen en vervolgens Hallo rijen leest.</span><span class="sxs-lookup"><span data-stu-id="81344-163">It inserts some rows, then reads hello rows.</span></span> <span data-ttu-id="81344-164">Hallo-gegevens met een update-instructie wordt gewijzigd en leesbewerkingen Hallo rijen opnieuw.</span><span class="sxs-lookup"><span data-stu-id="81344-164">It changes hello data with an update statement, and reads hello rows again.</span></span> <span data-ttu-id="81344-165">Ten slotte deze een rij verwijdert en opnieuw Hallo rijen leest.</span><span class="sxs-lookup"><span data-stu-id="81344-165">Finally it deletes a row, and reads hello rows again.</span></span>
    
    ```sql
    -- Create a database
    -- DROP DATABASE IF EXISTS quickstartdb;
    CREATE DATABASE quickstartdb;
    USE quickstartdb;
    
    -- Create a table and insert rows
    DROP TABLE IF EXISTS inventory;
    CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
    INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
    INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
    INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    
    -- Read
    SELECT * FROM inventory;
    
    -- Update
    UPDATE inventory SET quantity = 200 WHERE id = 1;
    SELECT * FROM inventory;
    
    -- Delete
    DELETE FROM inventory WHERE id = 2;
    SELECT * FROM inventory;
    ```

    <span data-ttu-id="81344-166">Hallo Schermafbeelding toont een voorbeeld van Hallo SQL-code in de uitvoer van SQL Workbench en Hallo nadat deze is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="81344-166">hello screenshot shows an example of hello SQL code in SQL Workbench and hello output after it has been run.</span></span>
    
    ![MySQL-Workbench SQL tabblad toorun voorbeeldcode SQL](media/connect-workbench/3-workbench-sql-tab.png)

2. <span data-ttu-id="81344-168">toorun hello voorbeeld SQL-Code, klikt u op het pictogram op de werkbalk Hallo Hallo lichter Hallo **SQL-bestand** tabblad.</span><span class="sxs-lookup"><span data-stu-id="81344-168">toorun hello sample SQL Code, click hello lightening bolt icon in hello toolbar of hello **SQL File** tab.</span></span>
3. <span data-ttu-id="81344-169">Let op drie tabbladen resulteert in een Hallo Hallo **resultaat raster** sectie in het midden Hallo van Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="81344-169">Notice hello three tabbed results in hello **Result Grid** section in hello middle of hello page.</span></span> 
4. <span data-ttu-id="81344-170">Kennisgeving Hallo **uitvoer** lijst onderaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="81344-170">Notice hello **Output** list at hello bottom of hello page.</span></span> <span data-ttu-id="81344-171">Hallo-status van elke opdracht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="81344-171">hello status of each command is shown.</span></span> 

<span data-ttu-id="81344-172">Nu u verbinding hebt tooAzure Database gemaakt voor gebruik van MySQL Workbench MySQL en gegevens met behulp van de SQL-taal Hallo hebt opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="81344-172">Now, you have connected tooAzure Database for MySQL using MySQL Workbench, and have queried data using hello SQL language.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81344-173">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="81344-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="81344-174">Een database migreren met behulp van Exporteren en importeren</span><span class="sxs-lookup"><span data-stu-id="81344-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
