---
title: een PHP-SQL aaaCreate web-app en tooAzure App Service implementeren met Git
description: Een zelfstudie die u laat zien hoe een PHP-toocreate web-app die gegevens in Azure SQL Database opslaat en Git-implementatie tooAzure App Service te gebruiken.
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
ms.openlocfilehash: aaacb2fe0787bbcdafa72871912e8d08792be29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a><span data-ttu-id="948b6-103">Een PHP-SQL-web-app maken en implementeren van tooAzure App Service met Git</span><span class="sxs-lookup"><span data-stu-id="948b6-103">Create a PHP-SQL web app and deploy tooAzure App Service using Git</span></span>
<span data-ttu-id="948b6-104">Deze zelfstudie laat zien hoe een PHP-toocreate web-app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) tooAzure SQL-Database die is verbonden en hoe toodeploy met Git.</span><span class="sxs-lookup"><span data-stu-id="948b6-104">This tutorial shows you how toocreate a PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) that connects tooAzure SQL Database and how toodeploy it using Git.</span></span> <span data-ttu-id="948b6-105">Deze zelfstudie wordt ervan uitgegaan dat u hebt [PHP][install-php], [SQL Server Express][install-SQLExpress], Hallo [Microsoft-Drivers voor SQL Server voor PHP ](http://www.microsoft.com/download/en/details.aspx?id=20098), en [Git] [ install-git] op uw computer geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="948b6-105">This tutorial assumes you have [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [Microsoft Drivers for SQL Server for PHP](http://www.microsoft.com/download/en/details.aspx?id=20098), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="948b6-106">Bij voltooiing van deze handleiding hebt u een PHP-SQL-web-app in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="948b6-106">Upon completing this guide, you will have a PHP-SQL web app running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="948b6-107">U kunt installeren en PHP, SQL Server Express en Microsoft-Drivers Hallo voor SQL Server configureren voor PHP met Hallo [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="948b6-107">You can install and configure PHP, SQL Server Express, and hello Microsoft Drivers for SQL Server for PHP using hello [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> 
> 

<span data-ttu-id="948b6-108">U leert:</span><span class="sxs-lookup"><span data-stu-id="948b6-108">You will learn:</span></span>

* <span data-ttu-id="948b6-109">Hoe toocreate een Azure web-app en een SQL-Database met behulp van Hallo [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="948b6-109">How toocreate an Azure web app and a SQL Database using hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="948b6-110">Omdat PHP is standaard ingeschakeld in App Service Web Apps, er is niets speciale vereist toorun is uw PHP-code.</span><span class="sxs-lookup"><span data-stu-id="948b6-110">Because PHP is enabled in App Service Web Apps by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="948b6-111">Hoe toopublish en uw toepassing tooAzure met Git opnieuw te publiceren.</span><span class="sxs-lookup"><span data-stu-id="948b6-111">How toopublish and re-publish your application tooAzure using Git.</span></span>

<span data-ttu-id="948b6-112">Door deze zelfstudie te volgen, bouwt u een webtoepassing eenvoudig registratie in PHP.</span><span class="sxs-lookup"><span data-stu-id="948b6-112">By following this tutorial, you will build a simple registration web application in PHP.</span></span> <span data-ttu-id="948b6-113">Hallo-toepassing wordt gehost in een Azure-Website.</span><span class="sxs-lookup"><span data-stu-id="948b6-113">hello application will be hosted in an Azure Website.</span></span> <span data-ttu-id="948b6-114">Een schermopname van de toepassing hello voltooid lager is dan:</span><span class="sxs-lookup"><span data-stu-id="948b6-114">A screenshot of hello completed application is below:</span></span>

![Azure PHP-website](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="948b6-116">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="948b6-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="948b6-117">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="948b6-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a><span data-ttu-id="948b6-118">Een Azure-web-app maken en Git-publicatie instellen</span><span class="sxs-lookup"><span data-stu-id="948b6-118">Create an Azure web app and set up Git publishing</span></span>
<span data-ttu-id="948b6-119">Volg deze stappen toocreate een Azure-web-app en een SQL-Database:</span><span class="sxs-lookup"><span data-stu-id="948b6-119">Follow these steps toocreate an Azure web app and a SQL Database:</span></span>

1. <span data-ttu-id="948b6-120">Meld u bij toohello [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="948b6-120">Log in toohello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="948b6-121">Open hello Azure Marketplace door te klikken op Hallo **nieuw** pictogram Hallo bovenaan links van Hallo dashboard, klikt u op **Alles selecteren** volgende tooMarketplace en het selecteren van **Web en mobiel**.</span><span class="sxs-lookup"><span data-stu-id="948b6-121">Open hello Azure Marketplace by clicking hello **New** icon on hello top left of hello dashboard, click on **Select All** next tooMarketplace and selecting **Web + Mobile**.</span></span>
3. <span data-ttu-id="948b6-122">Selecteer in de Hallo Marketplace, **Web en mobiel**.</span><span class="sxs-lookup"><span data-stu-id="948b6-122">In hello Marketplace, select **Web + Mobile**.</span></span>
4. <span data-ttu-id="948b6-123">Klik op Hallo **webtoepassing + SQL** pictogram.</span><span class="sxs-lookup"><span data-stu-id="948b6-123">Click hello **Web app + SQL** icon.</span></span>
5. <span data-ttu-id="948b6-124">Na het lezen van Hallo beschrijving van het Hallo-webtoepassing + SQL-app, selecteer **maken**.</span><span class="sxs-lookup"><span data-stu-id="948b6-124">After reading hello description of hello Web app + SQL app, select **Create**.</span></span>
6. <span data-ttu-id="948b6-125">Klik op elk onderdeel (**resourcegroep**, **Web-App**, **Database**, en **abonnement**) en typ of Selecteer waarden voor Hallo vereist velden:</span><span class="sxs-lookup"><span data-stu-id="948b6-125">Click on each part (**Resource Group**, **Web App**, **Database**, and **Subscription**) and enter or select values for hello required fields:</span></span>
   
   * <span data-ttu-id="948b6-126">Voer een URL-naam van uw keuze</span><span class="sxs-lookup"><span data-stu-id="948b6-126">Enter a URL name of your choice</span></span>    
   * <span data-ttu-id="948b6-127">Referenties voor database-server configureren</span><span class="sxs-lookup"><span data-stu-id="948b6-127">Configure database server credentials</span></span>
   * <span data-ttu-id="948b6-128">Hallo regio dichtstbijzijnde tooyou selecteren</span><span class="sxs-lookup"><span data-stu-id="948b6-128">Select hello region closest tooyou</span></span>
     
     ![de app configureren](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. <span data-ttu-id="948b6-130">Wanneer u klaar bent met definiëren Hallo web-app, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="948b6-130">When finished defining hello web app, click **Create**.</span></span>
   
    <span data-ttu-id="948b6-131">Wanneer het Hallo-web-app is gemaakt, Hallo **meldingen** knop knippert een groene **geslaagd** en resource groep blade open tooshow beide Hallo web app en Hallo SQL-database in de groep Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="948b6-131">When hello web app has been created, hello **Notifications** button will flash a green **SUCCESS** and hello resource group blade open tooshow both hello web app and hello SQL database in hello group.</span></span>
8. <span data-ttu-id="948b6-132">Klik op Hallo van web-app-pictogram op de blade Hallo resource groep blade tooopen Hallo van web-app.</span><span class="sxs-lookup"><span data-stu-id="948b6-132">Click hello web app's icon in hello resource group blade tooopen hello web app's blade.</span></span>
   
    ![Web-app van resourcegroep](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. <span data-ttu-id="948b6-134">In **instellingen** klikt u op **continue implementatie** > **vereiste instellingen configureren**.</span><span class="sxs-lookup"><span data-stu-id="948b6-134">In **Settings** click **Continuous deployment** > **Configure required settings**.</span></span> <span data-ttu-id="948b6-135">Selecteer **lokale Git-opslagplaats** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="948b6-135">Select **Local Git Repository** and click **OK**.</span></span>
   
    ![waar is de broncode](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    <span data-ttu-id="948b6-137">Als u een Git-opslagplaats voordat niet hebt ingesteld, moet u een gebruikersnaam en wachtwoord opgeven.</span><span class="sxs-lookup"><span data-stu-id="948b6-137">If you have not set up a Git repository before, you must provide a user name and password.</span></span> <span data-ttu-id="948b6-138">toodo, klikt u op **instellingen** > **implementatiereferenties** op Hallo van web-app-blade.</span><span class="sxs-lookup"><span data-stu-id="948b6-138">toodo this, click **Settings** > **Deployment credentials** in hello web app's blade.</span></span>
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. <span data-ttu-id="948b6-139">In **instellingen** klikt u op **eigenschappen** toosee Hallo Git externe URL u toouse toodeploy uw PHP-app later nodig.</span><span class="sxs-lookup"><span data-stu-id="948b6-139">In **Settings** click on **Properties** toosee hello Git remote URL you need toouse toodeploy your PHP app later.</span></span>

## <a name="get-sql-database-connection-information"></a><span data-ttu-id="948b6-140">Gegevens van de SQL-Database-verbinding ophalen</span><span class="sxs-lookup"><span data-stu-id="948b6-140">Get SQL Database connection information</span></span>
<span data-ttu-id="948b6-141">tooconnect toohello SQL Database-exemplaar dat is gekoppeld tooyour web-app, uw wordt moet Hallo verbindingsgegevens die u hebt opgegeven toen u het Hallo-database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="948b6-141">tooconnect toohello SQL Database instance that is linked tooyour web app, your will need hello connection information, which you specified when you created hello database.</span></span> <span data-ttu-id="948b6-142">tooget hello verbindingsinformatie voor SQL-Database, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="948b6-142">tooget hello SQL Database connection information, follow these steps:</span></span>

1. <span data-ttu-id="948b6-143">Terug in de blade Hallo resourcegroep bevindt, klikt u op het pictogram Hallo SQL database.</span><span class="sxs-lookup"><span data-stu-id="948b6-143">Back in hello resource group's blade, click hello SQL database's icon.</span></span>
2. <span data-ttu-id="948b6-144">Klik op de blade Hallo SQL database **instellingen** > **eigenschappen**, klikt u vervolgens op **databaseverbindingsreeksen tonen**.</span><span class="sxs-lookup"><span data-stu-id="948b6-144">In hello SQL database's blade, click **Settings** > **Properties**, then click **Show database connection strings**.</span></span> 
   
    ![Database-eigenschappen weergeven](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. <span data-ttu-id="948b6-146">Van Hallo **PHP** sectie van de resulterende dialoogvenster hello, noteer Hallo waarden voor `Server`, `SQL Database`, en `User Name`.</span><span class="sxs-lookup"><span data-stu-id="948b6-146">From hello **PHP** section of hello resulting dialog, make note of hello values for `Server`, `SQL Database`, and `User Name`.</span></span> <span data-ttu-id="948b6-147">U gebruikt deze waarden later wanneer publiceren van uw app tooAzure voor PHP web-App Service.</span><span class="sxs-lookup"><span data-stu-id="948b6-147">You will use these values later when publishing your PHP web app tooAzure App Service.</span></span>

## <a name="build-and-test-your-application-locally"></a><span data-ttu-id="948b6-148">De toepassing lokaal bouwen en testen</span><span class="sxs-lookup"><span data-stu-id="948b6-148">Build and test your application locally</span></span>
<span data-ttu-id="948b6-149">Hallo registratie van toepassing is een eenvoudige PHP-toepassing waarmee u tooregister voor een gebeurtenis aan de hand van uw naam en e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="948b6-149">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="948b6-150">Informatie over eerdere geregistreerde wordt weergegeven in een tabel.</span><span class="sxs-lookup"><span data-stu-id="948b6-150">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="948b6-151">Registratie-informatie wordt opgeslagen in een SQL Database-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="948b6-151">Registration information is stored in a SQL Database instance.</span></span> <span data-ttu-id="948b6-152">Hallo toepassing bestaat uit twee bestanden (kopiëren en plakken code hieronder):</span><span class="sxs-lookup"><span data-stu-id="948b6-152">hello application consists of two files (copy/paste code available below):</span></span>

* <span data-ttu-id="948b6-153">**index.php**: een formulier voor registratie en een tabel met registrant informatie wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="948b6-153">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="948b6-154">**CreateTable.php**: Hallo SQL-databasetabel voor Hallo toepassing maakt.</span><span class="sxs-lookup"><span data-stu-id="948b6-154">**createtable.php**: Creates hello SQL Database table for hello application.</span></span> <span data-ttu-id="948b6-155">Dit bestand wordt slechts eenmaal worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="948b6-155">This file will only be used once.</span></span>

<span data-ttu-id="948b6-156">toorun hello toepassing lokaal door Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="948b6-156">toorun hello application locally, follow hello steps below.</span></span> <span data-ttu-id="948b6-157">Merk op dat u deze stappen wordt ervan uitgegaan dat u PHP en SQL Server Express instellen op uw lokale computer en dat u hebt ingeschakeld Hallo [PDO-extensie voor SQL Server][pdo-sqlsrv].</span><span class="sxs-lookup"><span data-stu-id="948b6-157">Note that these steps assume you have PHP and SQL Server Express set up on your local machine, and that you have enabled hello [PDO extension for SQL Server][pdo-sqlsrv].</span></span>

1. <span data-ttu-id="948b6-158">Maken van een SQL Server-database aangeroepen `registration`.</span><span class="sxs-lookup"><span data-stu-id="948b6-158">Create a SQL Server database called `registration`.</span></span> <span data-ttu-id="948b6-159">U kunt dit doen vanuit Hallo `sqlcmd` opdrachtprompt met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="948b6-159">You can do this from hello `sqlcmd` command prompt with these commands:</span></span>
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. <span data-ttu-id="948b6-160">In de hoofdmap van uw toepassing maakt u twee bestanden in deze - een met de naam `createtable.php` en één aangeroepen `index.php`.</span><span class="sxs-lookup"><span data-stu-id="948b6-160">In your application root directory, create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="948b6-161">Open Hallo `createtable.php` in een teksteditor of IDE-bestand en voeg Hallo code hieronder.</span><span class="sxs-lookup"><span data-stu-id="948b6-161">Open hello `createtable.php` file in a text editor or IDE and add hello code below.</span></span> <span data-ttu-id="948b6-162">Deze code worden gebruikte toocreate hello `registration_tbl` tabel in Hallo `registration` database.</span><span class="sxs-lookup"><span data-stu-id="948b6-162">This code will be used toocreate hello `registration_tbl` table in hello `registration` database.</span></span>
   
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
   
    <span data-ttu-id="948b6-163">Houd er rekening mee dat u moet tooupdate Hallo waarden voor <code>$user</code> en <code>$pwd</code> met uw lokale SQL Server-gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="948b6-163">Note that you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local SQL Server user name and password.</span></span>
4. <span data-ttu-id="948b6-164">In een terminal in de hoofdmap Hallo Hallo toepassing type Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="948b6-164">In a terminal at hello root directory of hello application type hello following command:</span></span>
   
        php -S localhost:8000
5. <span data-ttu-id="948b6-165">Open een webbrowser en te bladeren**http://localhost:8000/createtable.php**.</span><span class="sxs-lookup"><span data-stu-id="948b6-165">Open a web browser and browse too**http://localhost:8000/createtable.php**.</span></span> <span data-ttu-id="948b6-166">Hiermee maakt u Hallo `registration_tbl` tabel in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="948b6-166">This will create hello `registration_tbl` table in hello database.</span></span>
6. <span data-ttu-id="948b6-167">Open Hallo **index.php** in een teksteditor of IDE-bestand en voeg Hallo basic HTML en CSS-code voor Hallo pagina (Hallo PHP code wordt toegevoegd in latere stappen).</span><span class="sxs-lookup"><span data-stu-id="948b6-167">Open hello **index.php** file in a text editor or IDE and add hello basic HTML and CSS code for hello page (hello PHP code will be added in later steps).</span></span>
   
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
        <p>Fill in your name and email address, then click <strong>Submit</strong> tooregister.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
7. <span data-ttu-id="948b6-168">Binnen Hallo PHP tags toevoegen PHP-code voor het verbinden van toohello database.</span><span class="sxs-lookup"><span data-stu-id="948b6-168">Within hello PHP tags, add PHP code for connecting toohello database.</span></span>
   
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
    <span data-ttu-id="948b6-169">Opnieuw, moet u tooupdate Hallo waarden voor <code>$user</code> en <code>$pwd</code> met uw lokale MySQL-gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="948b6-169">Again, you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
8. <span data-ttu-id="948b6-170">Volgende Hallo database verbinding code, voeg code toe voor registratie-informatie in het Hallo-database invoegen.</span><span class="sxs-lookup"><span data-stu-id="948b6-170">Following hello database connection code, add code for inserting registration information into hello database.</span></span>
   
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
9. <span data-ttu-id="948b6-171">Na de bovenstaande Hallo code, voeg code voor het ophalen van gegevens uit het Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="948b6-171">Finally, following hello code above, add code for retrieving data from hello database.</span></span>
   
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

<span data-ttu-id="948b6-172">U kunt nu te bladeren**http://localhost:8000/index.php** tootest Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="948b6-172">You can now browse too**http://localhost:8000/index.php** tootest hello application.</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="948b6-173">Uw toepassing publiceren</span><span class="sxs-lookup"><span data-stu-id="948b6-173">Publish your application</span></span>
<span data-ttu-id="948b6-174">Nadat u uw toepassing lokaal hebt getest, kunt u deze tooApp Service Web Apps met Git publiceren.</span><span class="sxs-lookup"><span data-stu-id="948b6-174">After you have tested your application locally, you can publish it tooApp Service Web Apps using Git.</span></span> <span data-ttu-id="948b6-175">Echter, moet u eerst tooupdate Hallo databaseverbindingsgegevens in Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="948b6-175">However, you first need tooupdate hello database connection information in hello application.</span></span> <span data-ttu-id="948b6-176">Hallo databaseverbindingsgegevens u eerder hebt verkregen met (in Hallo **verbindingsgegevens ophalen van de SQL-Database** sectie), update Hallo volgende informatie in **beide** hello `createdatabase.php` en `index.php` bestanden met Hallo waarden nodig:</span><span class="sxs-lookup"><span data-stu-id="948b6-176">Using hello database connection information you obtained earlier (in hello **Get SQL Database connection information** section), update hello following information in **both** hello `createdatabase.php` and `index.php` files with hello appropriate values:</span></span>

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> <span data-ttu-id="948b6-177">In Hallo <code>$host</code>, Hallo-waarde van de Server moet worden voorafgegaan door <code>tcp:</code>.</span><span class="sxs-lookup"><span data-stu-id="948b6-177">In hello <code>$host</code>, hello value of Server must be prepended with <code>tcp:</code>.</span></span>
> 
> 

<span data-ttu-id="948b6-178">Nu u bent klaar tooset van Git-publicatie en Hallo toepassing publiceren.</span><span class="sxs-lookup"><span data-stu-id="948b6-178">Now, you are ready tooset up Git publishing and publish hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="948b6-179">Dit zijn dezelfde stappen vermeld achter Hallo HALLO hallo **een Azure-web-app maken en Git-publicatie instellen** sectie hierboven.</span><span class="sxs-lookup"><span data-stu-id="948b6-179">These are hello same steps noted at hello end of hello **Create an Azure web app and set up Git publishing** section above.</span></span>
> 
> 

1. <span data-ttu-id="948b6-180">Open GitBash (of een terminal als Git in uw `PATH`), mappen toohello hoofdmap van uw toepassing wijzigen (Hallo **registratie** directory), en Voer Hallo de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="948b6-180">Open GitBash (or a terminal, if Git is in your `PATH`), change directories toohello root directory of your application (hello **registration** directory), and run hello following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="948b6-181">U wordt gevraagd om Hallo wachtwoord die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="948b6-181">You will be prompted for hello password you created earlier.</span></span>
2. <span data-ttu-id="948b6-182">Te bladeren**http://[web app name].azurewebsites.net/createtable.php** toocreate Hallo SQL-databasetabel voor Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="948b6-182">Browse too**http://[web app name].azurewebsites.net/createtable.php** toocreate hello SQL database table for hello application.</span></span>
3. <span data-ttu-id="948b6-183">Te bladeren**http://[web app name].azurewebsites.net/index.php** toobegin met Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="948b6-183">Browse too**http://[web app name].azurewebsites.net/index.php** toobegin using hello application.</span></span>

<span data-ttu-id="948b6-184">Nadat u uw toepassing hebt gepubliceerd, kunt u beginnen met het maken van wijzigingen tooit en Git toopublish gebruiken ze.</span><span class="sxs-lookup"><span data-stu-id="948b6-184">After you have published your application, you can begin making changes tooit and use Git toopublish them.</span></span> 

## <a name="publish-changes-tooyour-application"></a><span data-ttu-id="948b6-185">Wijzigingen tooyour toepassing publiceren</span><span class="sxs-lookup"><span data-stu-id="948b6-185">Publish changes tooyour application</span></span>
<span data-ttu-id="948b6-186">toopublish tooapplication, verandert als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="948b6-186">toopublish changes tooapplication, follow these steps:</span></span>

1. <span data-ttu-id="948b6-187">Breng wijzigingen tooyour toepassing lokaal.</span><span class="sxs-lookup"><span data-stu-id="948b6-187">Make changes tooyour application locally.</span></span>
2. <span data-ttu-id="948b6-188">Open GitBash (of een terminal it Git is in uw `PATH`), mappen toohello hoofdmap van uw toepassing te wijzigen en uitvoeren van Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="948b6-188">Open GitBash (or a terminal, it Git is in your `PATH`), change directories toohello root directory of your application, and run hello following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="948b6-189">U wordt gevraagd om Hallo wachtwoord die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="948b6-189">You will be prompted for hello password you created earlier.</span></span>
3. <span data-ttu-id="948b6-190">Te bladeren**http://[web app name].azurewebsites.net/index.php** toosee uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="948b6-190">Browse too**http://[web app name].azurewebsites.net/index.php** toosee your changes.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="948b6-191">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="948b6-191">What's changed</span></span>
* <span data-ttu-id="948b6-192">Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="948b6-192">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

