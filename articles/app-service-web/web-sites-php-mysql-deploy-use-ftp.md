---
title: een PHP-MySQL aaaCreate web-app in Azure App Service en implementeren met FTP
description: Een zelfstudie die u laat zien hoe een PHP-toocreate web-app die gegevens opslaat in de MySQL- en FTP-implementatie tooAzure.
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6d9d1de5-5868-48fd-8bad-decb4979cd65
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4d3b56a8ac63d0eba0dc0aec1b62e6d12f601bf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a><span data-ttu-id="a6fef-103">Een PHP-MySQL-webtoepassing maken in Azure App Service en implementeren met FTP</span><span class="sxs-lookup"><span data-stu-id="a6fef-103">Create a PHP-MySQL web app in Azure App Service and deploy using FTP</span></span>
<span data-ttu-id="a6fef-104">Deze zelfstudie leert u hoe u een PHP-MySQL toocreate web-app en hoe toodeploy via FTP.</span><span class="sxs-lookup"><span data-stu-id="a6fef-104">This tutorial shows you how toocreate a PHP-MySQL web app and how toodeploy it using FTP.</span></span> <span data-ttu-id="a6fef-105">Deze zelfstudie wordt ervan uitgegaan dat u hebt [PHP][install-php], [MySQL][install-mysql], een webserver en een FTP-client op uw computer geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a6fef-105">This tutorial assumes you have [PHP][install-php], [MySQL][install-mysql], a web server, and an FTP client installed on your computer.</span></span> <span data-ttu-id="a6fef-106">Hallo-instructies in deze zelfstudie kunnen worden uitgevoerd op elk besturingssysteem, met inbegrip van Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="a6fef-106">hello instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="a6fef-107">Bij voltooiing van deze handleiding hebt u een PHP/MySQL-web-app in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a6fef-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="a6fef-108">U leert:</span><span class="sxs-lookup"><span data-stu-id="a6fef-108">You will learn:</span></span>

* <span data-ttu-id="a6fef-109">Een web-app en een MySQL-database met toocreate Hallo hoe Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="a6fef-109">How toocreate a web app and a MySQL database using hello Azure Portal.</span></span> <span data-ttu-id="a6fef-110">Omdat PHP is standaard ingeschakeld in de Web-Apps, er is niets speciale vereist toorun is uw PHP-code.</span><span class="sxs-lookup"><span data-stu-id="a6fef-110">Because PHP is enabled in Web Apps by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="a6fef-111">Hoe uw toepassing tooAzure met toopublish FTP.</span><span class="sxs-lookup"><span data-stu-id="a6fef-111">How toopublish your application tooAzure using FTP.</span></span>

<span data-ttu-id="a6fef-112">Door deze zelfstudie te volgen, bouwt u een web-app voor eenvoudige registratie in PHP.</span><span class="sxs-lookup"><span data-stu-id="a6fef-112">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="a6fef-113">Hallo-toepassing wordt gehost in een Web-App.</span><span class="sxs-lookup"><span data-stu-id="a6fef-113">hello application will be hosted in a Web App.</span></span> <span data-ttu-id="a6fef-114">Een schermopname van de toepassing hello voltooid lager is dan:</span><span class="sxs-lookup"><span data-stu-id="a6fef-114">A screenshot of hello completed application is below:</span></span>

![Azure PHP-website][running-app]

> [!NOTE]
> <span data-ttu-id="a6fef-116">Als u wilt dat tooget voordat u zich aanmeldt voor een account met Azure App Service is gestart, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="a6fef-116">If you want tooget started with Azure App Service before signing up for an account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a6fef-117">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="a6fef-117">No credit cards required, no commitments.</span></span> 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a><span data-ttu-id="a6fef-118">Maken van een web-app en FTP-publicatie instellen</span><span class="sxs-lookup"><span data-stu-id="a6fef-118">Create a web app and set up FTP publishing</span></span>
<span data-ttu-id="a6fef-119">Volg deze stappen toocreate een web-app en een MySQL-database:</span><span class="sxs-lookup"><span data-stu-id="a6fef-119">Follow these steps toocreate a web app and a MySQL database:</span></span>

1. <span data-ttu-id="a6fef-120">Aanmelding toohello [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="a6fef-120">Login toohello [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="a6fef-121">Klik op Hallo **+ nieuw** pictogram Hallo bovenaan links van de hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="a6fef-121">Click hello **+ New** icon on hello top left of hello Azure Portal.</span></span>
   
    ![Nieuwe Azure-website maken][new-website]
3. <span data-ttu-id="a6fef-123">In het Hallo-Zoektype **webtoepassing + MySQL** en klik op **webtoepassing + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="a6fef-123">In hello search type **Web app + MySQL** and click on **Web app + MySQL**.</span></span>
   
    ![Aangepast maken een nieuwe website][custom-create]
4. <span data-ttu-id="a6fef-125">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a6fef-125">Click **Create**.</span></span> <span data-ttu-id="a6fef-126">Voer een unieke app service-naam, een geldige naam voor de resourcegroep Hallo en een nieuwe service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a6fef-126">Enter a unique app service name, a valid name for hello resource group and a new service plan.</span></span>
   
    ![Stel de naam van resourcegroep][resource-group]
5. <span data-ttu-id="a6fef-128">Voer waarden in voor de nieuwe database, inclusief ermee akkoord toohello juridische voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="a6fef-128">Enter values for your new database, including agreeing toohello legal terms.</span></span>
   
    ![Nieuwe MySQL-database maken][new-mysql-db]
6. <span data-ttu-id="a6fef-130">Als het Hallo-web-app is gemaakt, ziet u Hallo blade nieuwe app service.</span><span class="sxs-lookup"><span data-stu-id="a6fef-130">When hello web app has been created, you will see hello new app service blade.</span></span>
7. <span data-ttu-id="a6fef-131">Klik op **instellingen** > **implementatiereferenties**.</span><span class="sxs-lookup"><span data-stu-id="a6fef-131">Click on **Settings** > **Deployment credentials**.</span></span> 
   
    ![Implementatiereferenties instellen][set-deployment-credentials]
8. <span data-ttu-id="a6fef-133">tooenable FTP publiceren, moet u opgeven een gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a6fef-133">tooenable FTP publishing, you must provide a user name and password.</span></span> <span data-ttu-id="a6fef-134">Hallo-referenties op te slaan en maak een notitie van Hallo-gebruikersnaam en wachtwoord die u maakt.</span><span class="sxs-lookup"><span data-stu-id="a6fef-134">Save hello credentials and make a note of hello user name and password you create.</span></span>
   
    ![Publishing referenties maken][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="a6fef-136">Bouwen en testen van uw app lokaal</span><span class="sxs-lookup"><span data-stu-id="a6fef-136">Build and test your app locally</span></span>
<span data-ttu-id="a6fef-137">Hallo registratie van toepassing is een eenvoudige PHP-toepassing waarmee u tooregister voor een gebeurtenis aan de hand van uw naam en e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="a6fef-137">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="a6fef-138">Informatie over eerdere geregistreerde wordt weergegeven in een tabel.</span><span class="sxs-lookup"><span data-stu-id="a6fef-138">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="a6fef-139">Registratie-informatie wordt opgeslagen in een MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="a6fef-139">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="a6fef-140">Hallo app bestaat uit twee bestanden:</span><span class="sxs-lookup"><span data-stu-id="a6fef-140">hello app consists of two files:</span></span>

* <span data-ttu-id="a6fef-141">**index.php**: een formulier voor registratie en een tabel met registrant informatie wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a6fef-141">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="a6fef-142">**CreateTable.php**: Hallo MySQL tabel voor de toepassing hello wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a6fef-142">**createtable.php**: Creates hello MySQL table for hello application.</span></span> <span data-ttu-id="a6fef-143">Dit bestand wordt slechts eenmaal worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a6fef-143">This file will only be used once.</span></span>

<span data-ttu-id="a6fef-144">toobuild en lokaal uitvoeren Hallo app stappen Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="a6fef-144">toobuild and run hello app locally, follow hello steps below.</span></span> <span data-ttu-id="a6fef-145">Merk op dat u deze stappen wordt ervan uitgegaan u hebt PHP, MySQL en een webserver instellen op uw lokale computer en dat dat u hebt ingeschakeld Hallo [PDO-extensie voor MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="a6fef-145">Note that these steps assume you have PHP, MySQL, and a web server set up on your local machine, and that you have enabled hello [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="a6fef-146">Maak een MySQL-database aangeroepen `registration`.</span><span class="sxs-lookup"><span data-stu-id="a6fef-146">Create a MySQL database called `registration`.</span></span> <span data-ttu-id="a6fef-147">U kunt dit doen vanaf Hallo MySQL-opdrachtprompt met deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="a6fef-147">You can do this from hello MySQL command prompt with this command:</span></span>
   
        mysql> create database registration;
2. <span data-ttu-id="a6fef-148">Maak een map in de hoofdmap van de webserver, `registration` en maakt u twee bestanden in deze - een met de naam `createtable.php` en één aangeroepen `index.php`.</span><span class="sxs-lookup"><span data-stu-id="a6fef-148">In your web server's root directory, create a folder called `registration` and create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="a6fef-149">Open Hallo `createtable.php` in een teksteditor of IDE-bestand en voeg Hallo code hieronder.</span><span class="sxs-lookup"><span data-stu-id="a6fef-149">Open hello `createtable.php` file in a text editor or IDE and add hello code below.</span></span> <span data-ttu-id="a6fef-150">Deze code worden gebruikte toocreate hello `registration_tbl` tabel in Hallo `registration` database.</span><span class="sxs-lookup"><span data-stu-id="a6fef-150">This code will be used toocreate hello `registration_tbl` table in hello `registration` database.</span></span>
   
        <?php
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
                        id INT NOT NULL AUTO_INCREMENT, 
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
   
   > [!NOTE]
   > <span data-ttu-id="a6fef-151">U moet tooupdate Hallo waarden voor <code>$user</code> en <code>$pwd</code> met uw lokale MySQL-gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a6fef-151">You will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
4. <span data-ttu-id="a6fef-152">Open een webbrowser en te bladeren[http://localhost/registration/createtable.php][localhost-createtable].</span><span class="sxs-lookup"><span data-stu-id="a6fef-152">Open a web browser and browse too[http://localhost/registration/createtable.php][localhost-createtable].</span></span> <span data-ttu-id="a6fef-153">Hiermee maakt u Hallo `registration_tbl` tabel in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="a6fef-153">This will create hello `registration_tbl` table in hello database.</span></span>
5. <span data-ttu-id="a6fef-154">Open Hallo **index.php** in een teksteditor of IDE-bestand en voeg Hallo basic HTML en CSS-code voor Hallo pagina (Hallo PHP code wordt toegevoegd in latere stappen).</span><span class="sxs-lookup"><span data-stu-id="a6fef-154">Open hello **index.php** file in a text editor or IDE and add hello basic HTML and CSS code for hello page (hello PHP code will be added in later steps).</span></span>
   
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
6. <span data-ttu-id="a6fef-155">Binnen Hallo PHP tags toevoegen PHP-code voor het verbinden van toohello database.</span><span class="sxs-lookup"><span data-stu-id="a6fef-155">Within hello PHP tags, add PHP code for connecting toohello database.</span></span>
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > <span data-ttu-id="a6fef-156">Opnieuw, moet u tooupdate Hallo waarden voor <code>$user</code> en <code>$pwd</code> met uw lokale MySQL-gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a6fef-156">Again, you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
7. <span data-ttu-id="a6fef-157">Volgende Hallo database verbinding code, voeg code toe voor registratie-informatie in het Hallo-database invoegen.</span><span class="sxs-lookup"><span data-stu-id="a6fef-157">Following hello database connection code, add code for inserting registration information into hello database.</span></span>
   
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
8. <span data-ttu-id="a6fef-158">Na de bovenstaande Hallo code, voeg code voor het ophalen van gegevens uit het Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="a6fef-158">Finally, following hello code above, add code for retrieving data from hello database.</span></span>
   
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

<span data-ttu-id="a6fef-159">U kunt nu te bladeren[http://localhost/registration/index.php] [ localhost-index] tootest Hallo app.</span><span class="sxs-lookup"><span data-stu-id="a6fef-159">You can now browse too[http://localhost/registration/index.php][localhost-index] tootest hello app.</span></span>

## <a name="get-mysql-and-ftp-connection-information"></a><span data-ttu-id="a6fef-160">MySQL- en FTP-verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="a6fef-160">Get MySQL and FTP connection information</span></span>
<span data-ttu-id="a6fef-161">tooconnect toohello MySQL-database die wordt uitgevoerd in de Web-Apps, uw wordt moet Hallo verbindingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="a6fef-161">tooconnect toohello MySQL database that is running in Web Apps, your will need hello connection information.</span></span> <span data-ttu-id="a6fef-162">tooget verbindingsinformatie MySQL, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="a6fef-162">tooget MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="a6fef-163">Blade web-app klikt u op op Hallo resource groep koppeling van Hallo-app service:</span><span class="sxs-lookup"><span data-stu-id="a6fef-163">From hello app service web app blade click on hello resource group link:</span></span>
   
    ![Resourcegroep selecteren][select-resourcegroup]
2. <span data-ttu-id="a6fef-165">Klik op Hallo-database van de resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="a6fef-165">From your resource group, click hello database:</span></span>
   
    ![Database selecteren][select-database]
3. <span data-ttu-id="a6fef-167">Hallo database samenvatting, selecteer **instellingen** > **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="a6fef-167">From hello database summary, select **Settings** > **Properties**.</span></span>
   
    ![Eigenschappen selecteren][select-properties]
4. <span data-ttu-id="a6fef-169">Noteer Hallo waarden voor `Database`, `Host`, `User Id`, en `Password`.</span><span class="sxs-lookup"><span data-stu-id="a6fef-169">Make note of hello values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Opmerking eigenschappen][note-properties]
5. <span data-ttu-id="a6fef-171">Klik op Hallo van uw web-app **publicatieprofiel downloaden** op Hallo rechterbenedenhoek van de pagina Hallo koppeling:</span><span class="sxs-lookup"><span data-stu-id="a6fef-171">From your web app, click hello **Download publish profile** link at hello bottom right corner of hello page:</span></span>
   
    ![Publicatieprofiel downloaden][download-publish-profile]
6. <span data-ttu-id="a6fef-173">Open Hallo `.publishsettings` bestand in een XML-editor.</span><span class="sxs-lookup"><span data-stu-id="a6fef-173">Open hello `.publishsettings` file in an XML editor.</span></span> 
7. <span data-ttu-id="a6fef-174">Hallo zoeken `<publishProfile >` element met `publishMethod="FTP"` die vergelijkbaar toothis zoekt:</span><span class="sxs-lookup"><span data-stu-id="a6fef-174">Find hello `<publishProfile >` element with `publishMethod="FTP"` that looks similar toothis:</span></span>
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

<span data-ttu-id="a6fef-175">Noteer Hallo `publishUrl`, `userName`, en `userPWD` kenmerken.</span><span class="sxs-lookup"><span data-stu-id="a6fef-175">Make note of hello `publishUrl`, `userName`, and `userPWD` attributes.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="a6fef-176">Uw app publiceren</span><span class="sxs-lookup"><span data-stu-id="a6fef-176">Publish your app</span></span>
<span data-ttu-id="a6fef-177">Nadat u uw app lokaal hebt getest, kunt u deze tooyour web-app met FTP publiceren.</span><span class="sxs-lookup"><span data-stu-id="a6fef-177">After you have tested your app locally, you can publish it tooyour web app using FTP.</span></span> <span data-ttu-id="a6fef-178">Echter, moet u eerst tooupdate Hallo databaseverbindingsgegevens in Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a6fef-178">However, you first need tooupdate hello database connection information in hello application.</span></span> <span data-ttu-id="a6fef-179">Hallo databaseverbindingsgegevens u eerder hebt verkregen met (in Hallo **ophalen MySQL- en FTP-verbindingsgegevens** sectie), update Hallo volgende informatie in **beide** hello `createdatabase.php` en `index.php` bestanden met Hallo waarden nodig:</span><span class="sxs-lookup"><span data-stu-id="a6fef-179">Using hello database connection information you obtained earlier (in hello **Get MySQL and FTP connection information** section), update hello following information in **both** hello `createdatabase.php` and `index.php` files with hello appropriate values:</span></span>

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

<span data-ttu-id="a6fef-180">U bent er nu klaar toopublish uw app met FTP.</span><span class="sxs-lookup"><span data-stu-id="a6fef-180">Now you are ready toopublish your app using FTP.</span></span>

1. <span data-ttu-id="a6fef-181">Open uw FTP-client naar keuze.</span><span class="sxs-lookup"><span data-stu-id="a6fef-181">Open your FTP client of choice.</span></span>
2. <span data-ttu-id="a6fef-182">Voer Hallo *hostnaamgedeelte* van Hallo `publishUrl` kenmerk u hierboven hebt genoteerd in uw FTP-client.</span><span class="sxs-lookup"><span data-stu-id="a6fef-182">Enter hello *host name portion* from hello `publishUrl` attribute you noted above into your FTP client.</span></span>
3. <span data-ttu-id="a6fef-183">Voer Hallo `userName` en `userPWD` kenmerken die u hierboven hebt genoteerd ongewijzigd in uw FTP-client.</span><span class="sxs-lookup"><span data-stu-id="a6fef-183">Enter hello `userName` and `userPWD` attributes you noted above unchanged into your FTP client.</span></span>
4. <span data-ttu-id="a6fef-184">Een verbinding tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="a6fef-184">Establish a connection.</span></span>

<span data-ttu-id="a6fef-185">Nadat u verbinding hebt gemaakt wordt u kunnen tooupload en bestanden downloaden naar behoefte.</span><span class="sxs-lookup"><span data-stu-id="a6fef-185">After you have connected you will be able tooupload and download files as needed.</span></span> <span data-ttu-id="a6fef-186">Zorg ervoor dat u uploadt bestanden toohello hoofdmap, namelijk `/site/wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="a6fef-186">Be sure that you are uploading files toohello root directory, which is `/site/wwwroot`.</span></span>

<span data-ttu-id="a6fef-187">Na het uploaden van beide `index.php` en `createtable.php`, te bladeren**http://[site name].azurewebsites.net/createtable.php** toocreate Hallo MySQL tabel voor de toepassing hello en vervolgens te bladeren**http://[site naam ].azurewebsites.net/index.php** toobegin met Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a6fef-187">After uploading both `index.php` and `createtable.php`, browse too**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL table for hello application, then browse too**http://[site name].azurewebsites.net/index.php** toobegin using hello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6fef-188">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a6fef-188">Next steps</span></span>
<span data-ttu-id="a6fef-189">Zie voor meer informatie, Hallo [PHP-ontwikkelaarscentrum](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="a6fef-189">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-mysql]: http://dev.mysql.com/doc/refman/5.6/en/installing.html
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[localhost-createtable]: http://localhost/tasklist/createtable.php
[localhost-index]: http://localhost/tasklist/index.php
[running-app]: ./media/web-sites-php-mysql-deploy-use-ftp/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-ftp/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-ftp/create_web_mysql.png
[website-details]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/website_details.jpg
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-ftp/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-ftp/select_webapp.png
[set-deployment-credentials]: ./media/web-sites-php-mysql-deploy-use-ftp/set_credentials.png
[portal-ftp-username-password]: ./media/web-sites-php-mysql-deploy-use-ftp/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-ftp/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-ftp/create_wa.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-ftp/select_database.png
[select-resourcegroup]: ./media/web-sites-php-mysql-deploy-use-ftp/select_resourcegroup.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-ftp/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-ftp/note-properties.png

[connection-string-info]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/connection_string_info.png
[management-portal]: https://portal.azure.com
[download-publish-profile]: ./media/web-sites-php-mysql-deploy-use-ftp/download_publish_profile_3.png

