---
title: Een PHP-MySQL-webtoepassing maken in Azure App Service en implementeren met FTP
description: Een zelfstudie over het maken van een PHP-web-app die gegevens in de MySQL- en FTP-implementatie naar Azure opslaat.
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
ms.openlocfilehash: d428dffc6b810a692be0ec39a5f9cca05f5439e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a><span data-ttu-id="7ef17-103">Een PHP-MySQL-webtoepassing maken in Azure App Service en implementeren met FTP</span><span class="sxs-lookup"><span data-stu-id="7ef17-103">Create a PHP-MySQL web app in Azure App Service and deploy using FTP</span></span>
<span data-ttu-id="7ef17-104">Deze zelfstudie ziet u hoe u een PHP-MySQL web-app maken en implementeren met behulp van FTP.</span><span class="sxs-lookup"><span data-stu-id="7ef17-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it using FTP.</span></span> <span data-ttu-id="7ef17-105">Deze zelfstudie wordt ervan uitgegaan dat u hebt [PHP][install-php], [MySQL][install-mysql], een webserver en een FTP-client op uw computer geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7ef17-105">This tutorial assumes you have [PHP][install-php], [MySQL][install-mysql], a web server, and an FTP client installed on your computer.</span></span> <span data-ttu-id="7ef17-106">De instructies in deze zelfstudie kunnen worden uitgevoerd op elk besturingssysteem, met inbegrip van Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="7ef17-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="7ef17-107">Bij voltooiing van deze handleiding hebt u een PHP/MySQL-web-app in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7ef17-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="7ef17-108">U leert:</span><span class="sxs-lookup"><span data-stu-id="7ef17-108">You will learn:</span></span>

* <span data-ttu-id="7ef17-109">Het maken van een web-app en een MySQL-database met de Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="7ef17-109">How to create a web app and a MySQL database using the Azure Portal.</span></span> <span data-ttu-id="7ef17-110">Omdat PHP is standaard ingeschakeld in de Web-Apps, vereist geen speciale uw PHP-code uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="7ef17-110">Because PHP is enabled in Web Apps by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="7ef17-111">Hoe uw toepassing publiceren in Azure met FTP.</span><span class="sxs-lookup"><span data-stu-id="7ef17-111">How to publish your application to Azure using FTP.</span></span>

<span data-ttu-id="7ef17-112">Door deze zelfstudie te volgen, bouwt u een web-app voor eenvoudige registratie in PHP.</span><span class="sxs-lookup"><span data-stu-id="7ef17-112">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="7ef17-113">De toepassing zal worden gehost in een Web-App.</span><span class="sxs-lookup"><span data-stu-id="7ef17-113">The application will be hosted in a Web App.</span></span> <span data-ttu-id="7ef17-114">Een schermopname van de voltooide toepassing lager is dan:</span><span class="sxs-lookup"><span data-stu-id="7ef17-114">A screenshot of the completed application is below:</span></span>

![Azure PHP-website][running-app]

> [!NOTE]
> <span data-ttu-id="7ef17-116">Als u wilt dat aan de slag met Azure App Service voordat u zich aanmeldt voor een account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="7ef17-116">If you want to get started with Azure App Service before signing up for an account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7ef17-117">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="7ef17-117">No credit cards required, no commitments.</span></span> 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a><span data-ttu-id="7ef17-118">Maken van een web-app en FTP-publicatie instellen</span><span class="sxs-lookup"><span data-stu-id="7ef17-118">Create a web app and set up FTP publishing</span></span>
<span data-ttu-id="7ef17-119">Volg deze stappen om een web-app en een MySQL-database te maken:</span><span class="sxs-lookup"><span data-stu-id="7ef17-119">Follow these steps to create a web app and a MySQL database:</span></span>

1. <span data-ttu-id="7ef17-120">Meld u aan bij de [Azure-Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="7ef17-120">Login to the [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="7ef17-121">Klik op de **+ nieuw** pictogram op de bovenste links van de Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="7ef17-121">Click the **+ New** icon on the top left of the Azure Portal.</span></span>
   
    ![Nieuwe Azure-website maken][new-website]
3. <span data-ttu-id="7ef17-123">In het type zoekopdracht **webtoepassing + MySQL** en klik op **webtoepassing + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="7ef17-123">In the search type **Web app + MySQL** and click on **Web app + MySQL**.</span></span>
   
    ![Aangepast maken een nieuwe website][custom-create]
4. <span data-ttu-id="7ef17-125">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7ef17-125">Click **Create**.</span></span> <span data-ttu-id="7ef17-126">Geef een unieke app service-naam, een geldige naam voor de resourcegroep en een nieuwe service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7ef17-126">Enter a unique app service name, a valid name for the resource group and a new service plan.</span></span>
   
    ![Stel de naam van resourcegroep][resource-group]
5. <span data-ttu-id="7ef17-128">Geef waarden voor de nieuwe database, inclusief akkoord gaat met de juridische voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="7ef17-128">Enter values for your new database, including agreeing to the legal terms.</span></span>
   
    ![Nieuwe MySQL-database maken][new-mysql-db]
6. <span data-ttu-id="7ef17-130">Wanneer de web-app is gemaakt, ziet u de nieuwe app service-blade.</span><span class="sxs-lookup"><span data-stu-id="7ef17-130">When the web app has been created, you will see the new app service blade.</span></span>
7. <span data-ttu-id="7ef17-131">Klik op **instellingen** > **implementatiereferenties**.</span><span class="sxs-lookup"><span data-stu-id="7ef17-131">Click on **Settings** > **Deployment credentials**.</span></span> 
   
    ![Implementatiereferenties instellen][set-deployment-credentials]
8. <span data-ttu-id="7ef17-133">Om FTP-publicatie, moet u een gebruikersnaam en wachtwoord opgeven.</span><span class="sxs-lookup"><span data-stu-id="7ef17-133">To enable FTP publishing, you must provide a user name and password.</span></span> <span data-ttu-id="7ef17-134">Sla de referenties op en noteer de gebruikersnaam en wachtwoord die u maakt.</span><span class="sxs-lookup"><span data-stu-id="7ef17-134">Save the credentials and make a note of the user name and password you create.</span></span>
   
    ![Publishing referenties maken][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="7ef17-136">Bouwen en testen van uw app lokaal</span><span class="sxs-lookup"><span data-stu-id="7ef17-136">Build and test your app locally</span></span>
<span data-ttu-id="7ef17-137">De registratie van toepassing is een eenvoudige PHP-toepassing waarmee u te registreren voor een gebeurtenis aan de hand van uw naam en e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="7ef17-137">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="7ef17-138">Informatie over eerdere geregistreerde wordt weergegeven in een tabel.</span><span class="sxs-lookup"><span data-stu-id="7ef17-138">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="7ef17-139">Registratie-informatie wordt opgeslagen in een MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="7ef17-139">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="7ef17-140">De app bestaat uit twee bestanden:</span><span class="sxs-lookup"><span data-stu-id="7ef17-140">The app consists of two files:</span></span>

* <span data-ttu-id="7ef17-141">**index.php**: een formulier voor registratie en een tabel met registrant informatie wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7ef17-141">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="7ef17-142">**CreateTable.php**: de MySQL-tabel voor de toepassing maakt.</span><span class="sxs-lookup"><span data-stu-id="7ef17-142">**createtable.php**: Creates the MySQL table for the application.</span></span> <span data-ttu-id="7ef17-143">Dit bestand wordt slechts eenmaal worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7ef17-143">This file will only be used once.</span></span>

<span data-ttu-id="7ef17-144">Voor het bouwen en de app lokaal uitvoeren, de volgende stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="7ef17-144">To build and run the app locally, follow the steps below.</span></span> <span data-ttu-id="7ef17-145">Houd er rekening mee dat deze stappen wordt ervan uitgegaan dat u hebt PHP, MySQL en een webserver instellen op uw lokale computer en die u hebt ingeschakeld de [PDO-extensie voor MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="7ef17-145">Note that these steps assume you have PHP, MySQL, and a web server set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="7ef17-146">Maak een MySQL-database aangeroepen `registration`.</span><span class="sxs-lookup"><span data-stu-id="7ef17-146">Create a MySQL database called `registration`.</span></span> <span data-ttu-id="7ef17-147">U kunt dit doen vanaf de opdrachtprompt MySQL met deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="7ef17-147">You can do this from the MySQL command prompt with this command:</span></span>
   
        mysql> create database registration;
2. <span data-ttu-id="7ef17-148">Maak een map in de hoofdmap van de webserver, `registration` en maakt u twee bestanden in deze - een met de naam `createtable.php` en één aangeroepen `index.php`.</span><span class="sxs-lookup"><span data-stu-id="7ef17-148">In your web server's root directory, create a folder called `registration` and create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="7ef17-149">Open de `createtable.php` in een teksteditor of IDE-bestand en voeg de onderstaande code.</span><span class="sxs-lookup"><span data-stu-id="7ef17-149">Open the `createtable.php` file in a text editor or IDE and add the code below.</span></span> <span data-ttu-id="7ef17-150">Deze code wordt gebruikt voor het maken van de `registration_tbl` tabel de `registration` database.</span><span class="sxs-lookup"><span data-stu-id="7ef17-150">This code will be used to create the `registration_tbl` table in the `registration` database.</span></span>
   
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
   > <span data-ttu-id="7ef17-151">U moet de waarden voor bijwerken <code>$user</code> en <code>$pwd</code> met uw lokale MySQL-gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="7ef17-151">You will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
4. <span data-ttu-id="7ef17-152">Open een webbrowser en blader naar [http://localhost/registration/createtable.php][localhost-createtable].</span><span class="sxs-lookup"><span data-stu-id="7ef17-152">Open a web browser and browse to [http://localhost/registration/createtable.php][localhost-createtable].</span></span> <span data-ttu-id="7ef17-153">Hiermee maakt u de `registration_tbl` tabel in de database.</span><span class="sxs-lookup"><span data-stu-id="7ef17-153">This will create the `registration_tbl` table in the database.</span></span>
5. <span data-ttu-id="7ef17-154">Open de **index.php** in een teksteditor of IDE-bestand en voeg de basic HTML en CSS-code voor de pagina (de PHP-code wordt toegevoegd in latere stappen).</span><span class="sxs-lookup"><span data-stu-id="7ef17-154">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span></span>
   
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
6. <span data-ttu-id="7ef17-155">Binnen de PHP-tags toevoegen PHP-code voor het verbinden met de database.</span><span class="sxs-lookup"><span data-stu-id="7ef17-155">Within the PHP tags, add PHP code for connecting to the database.</span></span>
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect to database.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > <span data-ttu-id="7ef17-156">Opnieuw, moet u de waarden voor bijwerken <code>$user</code> en <code>$pwd</code> met uw lokale MySQL-gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="7ef17-156">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
7. <span data-ttu-id="7ef17-157">Na de code van de database-verbinding, voeg code toe voor de registratiegegevens worden ingevoegd in de database.</span><span class="sxs-lookup"><span data-stu-id="7ef17-157">Following the database connection code, add code for inserting registration information into the database.</span></span>
   
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
8. <span data-ttu-id="7ef17-158">Na de code, voeg de code voor het ophalen van gegevens uit de database.</span><span class="sxs-lookup"><span data-stu-id="7ef17-158">Finally, following the code above, add code for retrieving data from the database.</span></span>
   
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

<span data-ttu-id="7ef17-159">Nu kunt u bladeren naar [http://localhost/registration/index.php] [ localhost-index] voor het testen van de app.</span><span class="sxs-lookup"><span data-stu-id="7ef17-159">You can now browse to [http://localhost/registration/index.php][localhost-index] to test the app.</span></span>

## <a name="get-mysql-and-ftp-connection-information"></a><span data-ttu-id="7ef17-160">MySQL- en FTP-verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="7ef17-160">Get MySQL and FTP connection information</span></span>
<span data-ttu-id="7ef17-161">Verbinding maken met de MySQL-database die wordt uitgevoerd in de Web-Apps, uw wordt moet de verbindingsinformatie.</span><span class="sxs-lookup"><span data-stu-id="7ef17-161">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span></span> <span data-ttu-id="7ef17-162">Als u de verbindingsgegevens MySQL, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="7ef17-162">To get MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="7ef17-163">Blade web-app klikt u op op de koppeling van de groep resource van de app service:</span><span class="sxs-lookup"><span data-stu-id="7ef17-163">From the app service web app blade click on the resource group link:</span></span>
   
    ![Resourcegroep selecteren][select-resourcegroup]
2. <span data-ttu-id="7ef17-165">Klik op de database van de resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="7ef17-165">From your resource group, click the database:</span></span>
   
    ![Database selecteren][select-database]
3. <span data-ttu-id="7ef17-167">Selecteer in de database samenvatting **instellingen** > **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="7ef17-167">From the database summary, select **Settings** > **Properties**.</span></span>
   
    ![Eigenschappen selecteren][select-properties]
4. <span data-ttu-id="7ef17-169">Noteer de waarden voor `Database`, `Host`, `User Id`, en `Password`.</span><span class="sxs-lookup"><span data-stu-id="7ef17-169">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Opmerking eigenschappen][note-properties]
5. <span data-ttu-id="7ef17-171">Klik in uw web-app op de **publicatieprofiel downloaden** koppeling in de rechterbenedenhoek van de pagina:</span><span class="sxs-lookup"><span data-stu-id="7ef17-171">From your web app, click the **Download publish profile** link at the bottom right corner of the page:</span></span>
   
    ![Publicatieprofiel downloaden][download-publish-profile]
6. <span data-ttu-id="7ef17-173">Open de `.publishsettings` bestand in een XML-editor.</span><span class="sxs-lookup"><span data-stu-id="7ef17-173">Open the `.publishsettings` file in an XML editor.</span></span> 
7. <span data-ttu-id="7ef17-174">Zoek de `<publishProfile >` element met `publishMethod="FTP"` die ziet er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="7ef17-174">Find the `<publishProfile >` element with `publishMethod="FTP"` that looks similar to this:</span></span>
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

<span data-ttu-id="7ef17-175">Noteer de `publishUrl`, `userName`, en `userPWD` kenmerken.</span><span class="sxs-lookup"><span data-stu-id="7ef17-175">Make note of the `publishUrl`, `userName`, and `userPWD` attributes.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="7ef17-176">Uw app publiceren</span><span class="sxs-lookup"><span data-stu-id="7ef17-176">Publish your app</span></span>
<span data-ttu-id="7ef17-177">Nadat u uw app lokaal hebt getest, kunt u het publiceren naar uw web-app met FTP.</span><span class="sxs-lookup"><span data-stu-id="7ef17-177">After you have tested your app locally, you can publish it to your web app using FTP.</span></span> <span data-ttu-id="7ef17-178">Echter, moet u eerst de verbindingsgegevens voor de database in de toepassing bijwerken.</span><span class="sxs-lookup"><span data-stu-id="7ef17-178">However, you first need to update the database connection information in the application.</span></span> <span data-ttu-id="7ef17-179">Met de database-verbindingsgegevens die u eerder hebt verkregen (in de **ophalen MySQL- en FTP-verbindingsgegevens** sectie), werkt u de volgende gegevens in **beide** de `createdatabase.php` en `index.php` bestanden met de juiste waarden:</span><span class="sxs-lookup"><span data-stu-id="7ef17-179">Using the database connection information you obtained earlier (in the **Get MySQL and FTP connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span></span>

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

<span data-ttu-id="7ef17-180">U bent nu klaar voor het publiceren van uw app met FTP.</span><span class="sxs-lookup"><span data-stu-id="7ef17-180">Now you are ready to publish your app using FTP.</span></span>

1. <span data-ttu-id="7ef17-181">Open uw FTP-client naar keuze.</span><span class="sxs-lookup"><span data-stu-id="7ef17-181">Open your FTP client of choice.</span></span>
2. <span data-ttu-id="7ef17-182">Voer de *hostnaamgedeelte* van de `publishUrl` kenmerk u hierboven hebt genoteerd in uw FTP-client.</span><span class="sxs-lookup"><span data-stu-id="7ef17-182">Enter the *host name portion* from the `publishUrl` attribute you noted above into your FTP client.</span></span>
3. <span data-ttu-id="7ef17-183">Voer de `userName` en `userPWD` kenmerken die u hierboven hebt genoteerd ongewijzigd in uw FTP-client.</span><span class="sxs-lookup"><span data-stu-id="7ef17-183">Enter the `userName` and `userPWD` attributes you noted above unchanged into your FTP client.</span></span>
4. <span data-ttu-id="7ef17-184">Een verbinding tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="7ef17-184">Establish a connection.</span></span>

<span data-ttu-id="7ef17-185">Nadat u verbinding hebt gemaakt kunt u zich bestanden uploaden en downloaden naar behoefte.</span><span class="sxs-lookup"><span data-stu-id="7ef17-185">After you have connected you will be able to upload and download files as needed.</span></span> <span data-ttu-id="7ef17-186">Zorg ervoor dat u uploaden van bestanden naar de hoofdmap `/site/wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="7ef17-186">Be sure that you are uploading files to the root directory, which is `/site/wwwroot`.</span></span>

<span data-ttu-id="7ef17-187">Na het uploaden van beide `index.php` en `createtable.php`, blader naar **http://[site name].azurewebsites.net/createtable.php** voor het maken van de MySQL-tabel voor de toepassing en blader vervolgens naar **http://[site name].azurewebsites.net/index.php** om te beginnen met behulp van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7ef17-187">After uploading both `index.php` and `createtable.php`, browse to **http://[site name].azurewebsites.net/createtable.php** to create the MySQL table for the application, then browse to **http://[site name].azurewebsites.net/index.php** to begin using the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ef17-188">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7ef17-188">Next steps</span></span>
<span data-ttu-id="7ef17-189">Zie voor meer informatie de [PHP-ontwikkelaarscentrum](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="7ef17-189">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

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

