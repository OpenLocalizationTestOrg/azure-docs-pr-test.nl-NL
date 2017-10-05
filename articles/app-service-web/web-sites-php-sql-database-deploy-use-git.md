---
title: Een PHP-SQL-web-app maken en implementeren in Azure App Service met Git
description: Een zelfstudie over het maken van een PHP-web-app die gegevens in Azure SQL Database opslaat en Git in Azure App Service-implementatie gebruiken.
services: app-service\web, sql-database
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6b090bf6-31d8-4b74-81eb-050ef95929ca
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 0baa3eced3824fec0907ca937c594f127a2bdf8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-sql-web-app-and-deploy-to-azure-app-service-using-git"></a><span data-ttu-id="658c2-103">Een PHP-SQL-web-app maken en implementeren in Azure App Service met Git</span><span class="sxs-lookup"><span data-stu-id="658c2-103">Create a PHP-SQL web app and deploy to Azure App Service using Git</span></span>
<span data-ttu-id="658c2-104">Deze zelfstudie ziet u het maken van een PHP-web-app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) die verbinding maakt met Azure SQL Database en implementeren met behulp van Git.</span><span class="sxs-lookup"><span data-stu-id="658c2-104">This tutorial shows you how to create a PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) that connects to Azure SQL Database and how to deploy it using Git.</span></span> <span data-ttu-id="658c2-105">Deze zelfstudie wordt ervan uitgegaan dat u hebt [PHP][install-php], [SQL Server Express][install-SQLExpress], wordt de [Microsoft-Drivers voor SQL Server voor PHP ](http://www.microsoft.com/download/en/details.aspx?id=20098), en [Git] [ install-git] op uw computer geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="658c2-105">This tutorial assumes you have [PHP][install-php], [SQL Server Express][install-SQLExpress], the [Microsoft Drivers for SQL Server for PHP](http://www.microsoft.com/download/en/details.aspx?id=20098), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="658c2-106">Bij voltooiing van deze handleiding hebt u een PHP-SQL-web-app in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="658c2-106">Upon completing this guide, you will have a PHP-SQL web app running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="658c2-107">U kunt installeren en configureren van PHP, SQL Server Express en de Microsoft-Drivers voor SQL Server voor het gebruik van PHP de [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="658c2-107">You can install and configure PHP, SQL Server Express, and the Microsoft Drivers for SQL Server for PHP using the [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> 
> 

<span data-ttu-id="658c2-108">U leert:</span><span class="sxs-lookup"><span data-stu-id="658c2-108">You will learn:</span></span>

* <span data-ttu-id="658c2-109">Het maken van een Azure-web-app en een SQL-Database met de [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="658c2-109">How to create an Azure web app and a SQL Database using the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="658c2-110">Omdat PHP is standaard ingeschakeld in App Service Web Apps, vereist geen speciale uw PHP-code uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="658c2-110">Because PHP is enabled in App Service Web Apps by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="658c2-111">Het publiceren en uw toepassing in Azure met Git opnieuw te publiceren.</span><span class="sxs-lookup"><span data-stu-id="658c2-111">How to publish and re-publish your application to Azure using Git.</span></span>

<span data-ttu-id="658c2-112">Door deze zelfstudie te volgen, bouwt u een webtoepassing eenvoudig registratie in PHP.</span><span class="sxs-lookup"><span data-stu-id="658c2-112">By following this tutorial, you will build a simple registration web application in PHP.</span></span> <span data-ttu-id="658c2-113">De toepassing zal worden gehost in een Azure-Website.</span><span class="sxs-lookup"><span data-stu-id="658c2-113">The application will be hosted in an Azure Website.</span></span> <span data-ttu-id="658c2-114">Een schermopname van de voltooide toepassing lager is dan:</span><span class="sxs-lookup"><span data-stu-id="658c2-114">A screenshot of the completed application is below:</span></span>

![Azure PHP-website](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="658c2-116">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="658c2-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="658c2-117">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="658c2-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a><span data-ttu-id="658c2-118">Een Azure-web-app maken en Git-publicatie instellen</span><span class="sxs-lookup"><span data-stu-id="658c2-118">Create an Azure web app and set up Git publishing</span></span>
<span data-ttu-id="658c2-119">Volg deze stappen om een Azure-web-app en een SQL-Database te maken:</span><span class="sxs-lookup"><span data-stu-id="658c2-119">Follow these steps to create an Azure web app and a SQL Database:</span></span>

1. <span data-ttu-id="658c2-120">Meld u aan bij de [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="658c2-120">Log in to the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="658c2-121">Azure Marketplace openen door te klikken op de **nieuw** pictogram op de bovenste links van het dashboard, klikt u op **Alles selecteren** naast Marketplace en het selecteren van **Web en mobiel**.</span><span class="sxs-lookup"><span data-stu-id="658c2-121">Open the Azure Marketplace by clicking the **New** icon on the top left of the dashboard, click on **Select All** next to Marketplace and selecting **Web + Mobile**.</span></span>
3. <span data-ttu-id="658c2-122">Selecteer in de Marketplace **Web en mobiel**.</span><span class="sxs-lookup"><span data-stu-id="658c2-122">In the Marketplace, select **Web + Mobile**.</span></span>
4. <span data-ttu-id="658c2-123">Klik op de **webtoepassing + SQL** pictogram.</span><span class="sxs-lookup"><span data-stu-id="658c2-123">Click the **Web app + SQL** icon.</span></span>
5. <span data-ttu-id="658c2-124">Lees de beschrijving van de webtoepassing + SQL-app en selecteer **maken**.</span><span class="sxs-lookup"><span data-stu-id="658c2-124">After reading the description of the Web app + SQL app, select **Create**.</span></span>
6. <span data-ttu-id="658c2-125">Klik op elk onderdeel (**resourcegroep**, **Web-App**, **Database**, en **abonnement**) en typ of Selecteer waarden voor de vereiste velden :</span><span class="sxs-lookup"><span data-stu-id="658c2-125">Click on each part (**Resource Group**, **Web App**, **Database**, and **Subscription**) and enter or select values for the required fields:</span></span>
   
   * <span data-ttu-id="658c2-126">Voer een URL-naam van uw keuze</span><span class="sxs-lookup"><span data-stu-id="658c2-126">Enter a URL name of your choice</span></span>    
   * <span data-ttu-id="658c2-127">Referenties voor database-server configureren</span><span class="sxs-lookup"><span data-stu-id="658c2-127">Configure database server credentials</span></span>
   * <span data-ttu-id="658c2-128">Selecteer de regio die het dichtst bij u</span><span class="sxs-lookup"><span data-stu-id="658c2-128">Select the region closest to you</span></span>
     
     ![de app configureren](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. <span data-ttu-id="658c2-130">Wanneer u klaar bent met het definiëren van de web-app, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="658c2-130">When finished defining the web app, click **Create**.</span></span>
   
    <span data-ttu-id="658c2-131">Wanneer de web-app is gemaakt, de **meldingen** knop knippert een groene **geslaagd** en de resourcegroepblade openen om weer te geven van zowel de web-app en de SQL-database in de groep.</span><span class="sxs-lookup"><span data-stu-id="658c2-131">When the web app has been created, the **Notifications** button will flash a green **SUCCESS** and the resource group blade open to show both the web app and the SQL database in the group.</span></span>
8. <span data-ttu-id="658c2-132">Klik op de web-app-pictogram in de resourcegroepblade om de web-app-blade te openen.</span><span class="sxs-lookup"><span data-stu-id="658c2-132">Click the web app's icon in the resource group blade to open the web app's blade.</span></span>
   
    ![Web-app van resourcegroep](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. <span data-ttu-id="658c2-134">In **instellingen** klikt u op **continue implementatie** > **vereiste instellingen configureren**.</span><span class="sxs-lookup"><span data-stu-id="658c2-134">In **Settings** click **Continuous deployment** > **Configure required settings**.</span></span> <span data-ttu-id="658c2-135">Selecteer **lokale Git-opslagplaats** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="658c2-135">Select **Local Git Repository** and click **OK**.</span></span>
   
    ![waar is de broncode](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    <span data-ttu-id="658c2-137">Als u een Git-opslagplaats voordat niet hebt ingesteld, moet u een gebruikersnaam en wachtwoord opgeven.</span><span class="sxs-lookup"><span data-stu-id="658c2-137">If you have not set up a Git repository before, you must provide a user name and password.</span></span> <span data-ttu-id="658c2-138">Om dit te doen, klikt u op **instellingen** > **implementatiereferenties** in de web-app-blade.</span><span class="sxs-lookup"><span data-stu-id="658c2-138">To do this, click **Settings** > **Deployment credentials** in the web app's blade.</span></span>
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. <span data-ttu-id="658c2-139">In **instellingen** klikt u op **eigenschappen** om te zien van de externe Git-URL u gebruiken moet voor het implementeren van uw PHP-app hoger.</span><span class="sxs-lookup"><span data-stu-id="658c2-139">In **Settings** click on **Properties** to see the Git remote URL you need to use to deploy your PHP app later.</span></span>

## <a name="get-sql-database-connection-information"></a><span data-ttu-id="658c2-140">Gegevens van de SQL-Database-verbinding ophalen</span><span class="sxs-lookup"><span data-stu-id="658c2-140">Get SQL Database connection information</span></span>
<span data-ttu-id="658c2-141">Verbinding maken met de SQL-Database-exemplaar dat is gekoppeld aan uw web-app, uw wordt moet de verbindingsinformatie, die u hebt opgegeven toen u de database hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="658c2-141">To connect to the SQL Database instance that is linked to your web app, your will need the connection information, which you specified when you created the database.</span></span> <span data-ttu-id="658c2-142">Als u de verbindingsgegevens van de SQL-Database, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="658c2-142">To get the SQL Database connection information, follow these steps:</span></span>

1. <span data-ttu-id="658c2-143">Klik op het pictogram van de SQL-database terug in de blade van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="658c2-143">Back in the resource group's blade, click the SQL database's icon.</span></span>
2. <span data-ttu-id="658c2-144">Klik op de SQL-database blade **instellingen** > **eigenschappen**, klikt u vervolgens op **databaseverbindingsreeksen tonen**.</span><span class="sxs-lookup"><span data-stu-id="658c2-144">In the SQL database's blade, click **Settings** > **Properties**, then click **Show database connection strings**.</span></span> 
   
    ![Database-eigenschappen weergeven](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. <span data-ttu-id="658c2-146">Van de **PHP** sectie van het dialoogvenster wordt geopend, noteer de waarden voor `Server`, `SQL Database`, en `User Name`.</span><span class="sxs-lookup"><span data-stu-id="658c2-146">From the **PHP** section of the resulting dialog, make note of the values for `Server`, `SQL Database`, and `User Name`.</span></span> <span data-ttu-id="658c2-147">U kunt deze waarden later worden gebruikt bij het publiceren van uw PHP-web-app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="658c2-147">You will use these values later when publishing your PHP web app to Azure App Service.</span></span>

## <a name="build-and-test-your-application-locally"></a><span data-ttu-id="658c2-148">De toepassing lokaal bouwen en testen</span><span class="sxs-lookup"><span data-stu-id="658c2-148">Build and test your application locally</span></span>
<span data-ttu-id="658c2-149">De registratie van toepassing is een eenvoudige PHP-toepassing waarmee u te registreren voor een gebeurtenis aan de hand van uw naam en e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="658c2-149">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="658c2-150">Informatie over eerdere geregistreerde wordt weergegeven in een tabel.</span><span class="sxs-lookup"><span data-stu-id="658c2-150">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="658c2-151">Registratie-informatie wordt opgeslagen in een SQL Database-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="658c2-151">Registration information is stored in a SQL Database instance.</span></span> <span data-ttu-id="658c2-152">De toepassing bestaat uit twee bestanden (kopiëren en plakken code hieronder):</span><span class="sxs-lookup"><span data-stu-id="658c2-152">The application consists of two files (copy/paste code available below):</span></span>

* <span data-ttu-id="658c2-153">**index.php**: een formulier voor registratie en een tabel met registrant informatie wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="658c2-153">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="658c2-154">**CreateTable.php**: de SQL-databasetabel voor de toepassing maakt.</span><span class="sxs-lookup"><span data-stu-id="658c2-154">**createtable.php**: Creates the SQL Database table for the application.</span></span> <span data-ttu-id="658c2-155">Dit bestand wordt slechts eenmaal worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="658c2-155">This file will only be used once.</span></span>

<span data-ttu-id="658c2-156">Als u wilt de toepassing lokaal uitvoert, de volgende stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="658c2-156">To run the application locally, follow the steps below.</span></span> <span data-ttu-id="658c2-157">Houd er rekening mee dat deze stappen wordt ervan uitgegaan dat u PHP en SQL Server Express instellen op uw lokale computer hebt en u hebt ingeschakeld de [PDO-extensie voor SQL Server][pdo-sqlsrv].</span><span class="sxs-lookup"><span data-stu-id="658c2-157">Note that these steps assume you have PHP and SQL Server Express set up on your local machine, and that you have enabled the [PDO extension for SQL Server][pdo-sqlsrv].</span></span>

1. <span data-ttu-id="658c2-158">Maken van een SQL Server-database aangeroepen `registration`.</span><span class="sxs-lookup"><span data-stu-id="658c2-158">Create a SQL Server database called `registration`.</span></span> <span data-ttu-id="658c2-159">U kunt dit doen vanuit de `sqlcmd` opdrachtprompt met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="658c2-159">You can do this from the `sqlcmd` command prompt with these commands:</span></span>
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. <span data-ttu-id="658c2-160">In de hoofdmap van uw toepassing maakt u twee bestanden in deze - een met de naam `createtable.php` en één aangeroepen `index.php`.</span><span class="sxs-lookup"><span data-stu-id="658c2-160">In your application root directory, create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="658c2-161">Open de `createtable.php` in een teksteditor of IDE-bestand en voeg de onderstaande code.</span><span class="sxs-lookup"><span data-stu-id="658c2-161">Open the `createtable.php` file in a text editor or IDE and add the code below.</span></span> <span data-ttu-id="658c2-162">Deze code wordt gebruikt voor het maken van de `registration_tbl` tabel de `registration` database.</span><span class="sxs-lookup"><span data-stu-id="658c2-162">This code will be used to create the `registration_tbl` table in the `registration` database.</span></span>
   
        <?php
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
            id INT NOT NULL IDENTITY(1,1) 
            PRIMARY KEY(id),
            name VARCHAR(30),
            email VARCHAR(30),
            date DATE)";
            $conn->query($sql);
        }
        catch(Exception $e){
            die(print_r($e));
        }
        echo "<h3>Table created.</h3>";
        ?>
   
    <span data-ttu-id="658c2-163">Houd er rekening mee dat moet u de waarden voor bijwerken <code>$user</code> en <code>$pwd</code> met uw lokale SQL Server-gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="658c2-163">Note that you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local SQL Server user name and password.</span></span>
4. <span data-ttu-id="658c2-164">Typ de volgende opdracht in een terminal in de hoofdmap van de toepassing:</span><span class="sxs-lookup"><span data-stu-id="658c2-164">In a terminal at the root directory of the application type the following command:</span></span>
   
        php -S localhost:8000
5. <span data-ttu-id="658c2-165">Open een webbrowser en blader naar **http://localhost:8000/createtable.php**.</span><span class="sxs-lookup"><span data-stu-id="658c2-165">Open a web browser and browse to **http://localhost:8000/createtable.php**.</span></span> <span data-ttu-id="658c2-166">Hiermee maakt u de `registration_tbl` tabel in de database.</span><span class="sxs-lookup"><span data-stu-id="658c2-166">This will create the `registration_tbl` table in the database.</span></span>
6. <span data-ttu-id="658c2-167">Open de **index.php** in een teksteditor of IDE-bestand en voeg de basic HTML en CSS-code voor de pagina (de PHP-code wordt toegevoegd in latere stappen).</span><span class="sxs-lookup"><span data-stu-id="658c2-167">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span></span>
   
        <html>
        <head>
        <Title>Registration Form</Title>
        <style type="text/css">
            body { background-color: #fff; border-top: solid 10px #000;
                color: #333; font-size: .85em; margin: 20; padding: 20;
                font-family: "Segoe UI", Verdana, Helvetica, Sans-Serif;
            }
            h1, h2, h3,{ color: #000; margin-bottom: 0; padding-bottom: 0; }
            h1 { font-size: 2em; }
            h2 { font-size: 1.75em; }
            h3 { font-size: 1.2em; }
            table { margin-top: 0.75em; }
            th { font-size: 1.2em; text-align: left; border: none; padding-left: 0; }
            td { padding: 0.25em 2em 0.25em 0em; border: 0 none; }
        </style>
        </head>
        <body>
        <h1>Register here!</h1>
        <p>Fill in your name and email address, then click <strong>Submit</strong> to register.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
7. <span data-ttu-id="658c2-168">Binnen de PHP-tags toevoegen PHP-code voor het verbinden met de database.</span><span class="sxs-lookup"><span data-stu-id="658c2-168">Within the PHP tags, add PHP code for connecting to the database.</span></span>
   
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect to database.
        try {
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
    <span data-ttu-id="658c2-169">Opnieuw, moet u de waarden voor bijwerken <code>$user</code> en <code>$pwd</code> met uw lokale MySQL-gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="658c2-169">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
8. <span data-ttu-id="658c2-170">Na de code van de database-verbinding, voeg code toe voor de registratiegegevens worden ingevoegd in de database.</span><span class="sxs-lookup"><span data-stu-id="658c2-170">Following the database connection code, add code for inserting registration information into the database.</span></span>
   
        if(!empty($_POST)) {
        try {
            $name = $_POST['name'];
            $email = $_POST['email'];
            $date = date("Y-m-d");
            // Insert data
            $sql_insert = "INSERT INTO registration_tbl (name, email, date) 
                           VALUES (?,?,?)";
            $stmt = $conn->prepare($sql_insert);
            $stmt->bindValue(1, $name);
            $stmt->bindValue(2, $email);
            $stmt->bindValue(3, $date);
            $stmt->execute();
        }
        catch(Exception $e) {
            die(var_dump($e));
        }
        echo "<h3>Your're registered!</h3>";
        }
9. <span data-ttu-id="658c2-171">Na de code, voeg de code voor het ophalen van gegevens uit de database.</span><span class="sxs-lookup"><span data-stu-id="658c2-171">Finally, following the code above, add code for retrieving data from the database.</span></span>
   
        $sql_select = "SELECT * FROM registration_tbl";
        $stmt = $conn->query($sql_select);
        $registrants = $stmt->fetchAll(); 
        if(count($registrants) > 0) {
            echo "<h2>People who are registered:</h2>";
            echo "<table>";
            echo "<tr><th>Name</th>";
            echo "<th>Email</th>";
            echo "<th>Date</th></tr>";
            foreach($registrants as $registrant) {
                echo "<tr><td>".$registrant['name']."</td>";
                echo "<td>".$registrant['email']."</td>";
                echo "<td>".$registrant['date']."</td></tr>";
            }
             echo "</table>";
        } else {
            echo "<h3>No one is currently registered.</h3>";
        }

<span data-ttu-id="658c2-172">Nu kunt u bladeren naar **http://localhost:8000/index.php** test de toepassing.</span><span class="sxs-lookup"><span data-stu-id="658c2-172">You can now browse to **http://localhost:8000/index.php** to test the application.</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="658c2-173">Uw toepassing publiceren</span><span class="sxs-lookup"><span data-stu-id="658c2-173">Publish your application</span></span>
<span data-ttu-id="658c2-174">Nadat u uw toepassing lokaal hebt getest, kunt u het publiceren naar App Service Web Apps met Git.</span><span class="sxs-lookup"><span data-stu-id="658c2-174">After you have tested your application locally, you can publish it to App Service Web Apps using Git.</span></span> <span data-ttu-id="658c2-175">Echter, moet u eerst de verbindingsgegevens voor de database in de toepassing bijwerken.</span><span class="sxs-lookup"><span data-stu-id="658c2-175">However, you first need to update the database connection information in the application.</span></span> <span data-ttu-id="658c2-176">Met de database-verbindingsgegevens die u eerder hebt verkregen (in de **verbindingsgegevens ophalen van de SQL-Database** sectie), werkt u de volgende gegevens in **beide** de `createdatabase.php` en `index.php` bestanden met de juiste waarden:</span><span class="sxs-lookup"><span data-stu-id="658c2-176">Using the database connection information you obtained earlier (in the **Get SQL Database connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span></span>

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> <span data-ttu-id="658c2-177">In de <code>$host</code>, de waarde van de Server moet worden voorafgegaan door <code>tcp:</code>.</span><span class="sxs-lookup"><span data-stu-id="658c2-177">In the <code>$host</code>, the value of Server must be prepended with <code>tcp:</code>.</span></span>
> 
> 

<span data-ttu-id="658c2-178">U bent nu klaar Git-publicatie instellen en de toepassing te publiceren.</span><span class="sxs-lookup"><span data-stu-id="658c2-178">Now, you are ready to set up Git publishing and publish the application.</span></span>

> [!NOTE]
> <span data-ttu-id="658c2-179">Dit zijn dezelfde stappen vermeld aan het einde van de **een Azure-web-app maken en Git-publicatie instellen** sectie hierboven.</span><span class="sxs-lookup"><span data-stu-id="658c2-179">These are the same steps noted at the end of the **Create an Azure web app and set up Git publishing** section above.</span></span>
> 
> 

1. <span data-ttu-id="658c2-180">Open GitBash (of een terminal als Git in uw `PATH`), wijzig de mappen in de hoofdmap van uw toepassing (de **registratie** directory), en voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="658c2-180">Open GitBash (or a terminal, if Git is in your `PATH`), change directories to the root directory of your application (the **registration** directory), and run the following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="658c2-181">U wordt gevraagd om het wachtwoord dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="658c2-181">You will be prompted for the password you created earlier.</span></span>
2. <span data-ttu-id="658c2-182">Blader naar **http://[web app name].azurewebsites.net/createtable.php** voor het maken van de tabel van de SQL-database voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="658c2-182">Browse to **http://[web app name].azurewebsites.net/createtable.php** to create the SQL database table for the application.</span></span>
3. <span data-ttu-id="658c2-183">Blader naar **http://[web app name].azurewebsites.net/index.php** om te beginnen met behulp van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="658c2-183">Browse to **http://[web app name].azurewebsites.net/index.php** to begin using the application.</span></span>

<span data-ttu-id="658c2-184">Nadat u uw toepassing hebt gepubliceerd, kunt u beginnen wijzigingen aanbrengen en Git gebruiken om te publiceren.</span><span class="sxs-lookup"><span data-stu-id="658c2-184">After you have published your application, you can begin making changes to it and use Git to publish them.</span></span> 

## <a name="publish-changes-to-your-application"></a><span data-ttu-id="658c2-185">Wijzigingen in uw toepassing publiceren</span><span class="sxs-lookup"><span data-stu-id="658c2-185">Publish changes to your application</span></span>
<span data-ttu-id="658c2-186">Om wijzigingen te publiceren naar de toepassing, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="658c2-186">To publish changes to application, follow these steps:</span></span>

1. <span data-ttu-id="658c2-187">Wijzigingen aanbrengen in uw toepassing lokaal.</span><span class="sxs-lookup"><span data-stu-id="658c2-187">Make changes to your application locally.</span></span>
2. <span data-ttu-id="658c2-188">Open GitBash (of een terminal it Git is in uw `PATH`), wijzig de mappen in de hoofdmap van uw toepassing en voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="658c2-188">Open GitBash (or a terminal, it Git is in your `PATH`), change directories to the root directory of your application, and run the following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="658c2-189">U wordt gevraagd om het wachtwoord dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="658c2-189">You will be prompted for the password you created earlier.</span></span>
3. <span data-ttu-id="658c2-190">Blader naar **http://[web app name].azurewebsites.net/index.php** om uw wijzigingen te bekijken.</span><span class="sxs-lookup"><span data-stu-id="658c2-190">Browse to **http://[web app name].azurewebsites.net/index.php** to see your changes.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="658c2-191">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="658c2-191">What's changed</span></span>
* <span data-ttu-id="658c2-192">Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="658c2-192">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

