---
title: Een PHP-MySQL-webtoepassing maken in Azure App Service en implementeren met Git
description: Een zelfstudie over het maken van een PHP-web-app die gegevens in MySQL opslaat en Git-implementatie naar Azure gebruiken.
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
tags: mysql
ms.assetid: 7454475f-e275-4bc7-9f09-1ef07382e5da
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: aa845eb474dbd42ae2c31880690d4ced059eb448
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a><span data-ttu-id="7d57c-103">Een PHP-MySQL-webtoepassing maken in Azure App Service en implementeren met Git</span><span class="sxs-lookup"><span data-stu-id="7d57c-103">Create a PHP-MySQL web app in Azure App Service and deploy using Git</span></span>
<span data-ttu-id="7d57c-104">Deze zelfstudie ziet u hoe u een PHP-MySQL web-app maken en implementeren naar [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) met Git.</span><span class="sxs-lookup"><span data-stu-id="7d57c-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) using Git.</span></span> <span data-ttu-id="7d57c-105">U gaat gebruiken [PHP][install-php], de MySQL-opdrachtregelhulpprogramma (onderdeel van [MySQL][install-mysql]), en [Git] [ install-git] op uw computer geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7d57c-105">You will use [PHP][install-php], the MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="7d57c-106">De instructies in deze zelfstudie kunnen worden uitgevoerd op elk besturingssysteem, met inbegrip van Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="7d57c-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="7d57c-107">Bij voltooiing van deze handleiding hebt u een PHP/MySQL-web-app in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7d57c-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="7d57c-108">U leert:</span><span class="sxs-lookup"><span data-stu-id="7d57c-108">You will learn:</span></span>

* <span data-ttu-id="7d57c-109">Het maken van een web-app en een MySQL-database met de [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="7d57c-109">How to create a web app and a MySQL database using the [Azure Portal][management-portal].</span></span> <span data-ttu-id="7d57c-110">Omdat PHP is ingeschakeld in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) standaard niets speciale is vereist voor het uitvoeren van uw PHP-code.</span><span class="sxs-lookup"><span data-stu-id="7d57c-110">Because PHP is enabled in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="7d57c-111">Het publiceren en uw toepassing in Azure met Git opnieuw te publiceren.</span><span class="sxs-lookup"><span data-stu-id="7d57c-111">How to publish and re-publish your application to Azure using Git.</span></span>
* <span data-ttu-id="7d57c-112">Het inschakelen van de Composer-extensie voor het automatiseren van Composer taken op elke `git push`.</span><span class="sxs-lookup"><span data-stu-id="7d57c-112">How to enable the Composer extension to automate Composer tasks at every `git push`.</span></span>

<span data-ttu-id="7d57c-113">Door deze zelfstudie te volgen, bouwt u een web-app voor eenvoudige registratie in PHP.</span><span class="sxs-lookup"><span data-stu-id="7d57c-113">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="7d57c-114">De toepassing zal worden gehost in Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="7d57c-114">The application will be hosted in Web Apps.</span></span> <span data-ttu-id="7d57c-115">Een schermopname van de voltooide toepassing lager is dan:</span><span class="sxs-lookup"><span data-stu-id="7d57c-115">A screenshot of the completed application is below:</span></span>

![Azure PHP-website][running-app]

## <a name="set-up-the-development-environment"></a><span data-ttu-id="7d57c-117">De ontwikkelomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="7d57c-117">Set up the development environment</span></span>
<span data-ttu-id="7d57c-118">Deze zelfstudie wordt ervan uitgegaan dat u hebt [PHP][install-php], de MySQL-opdrachtregelhulpprogramma (onderdeel van [MySQL][install-mysql]), en [Git] [ install-git] op uw computer geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7d57c-118">This tutorial assumes you have [PHP][install-php], the MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span>

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a><span data-ttu-id="7d57c-119">Een web-app maken en Git-publicatie instellen</span><span class="sxs-lookup"><span data-stu-id="7d57c-119">Create a web app and set up Git publishing</span></span>
<span data-ttu-id="7d57c-120">Volg deze stappen om een web-app en een MySQL-database te maken:</span><span class="sxs-lookup"><span data-stu-id="7d57c-120">Follow these steps to create a web app and a MySQL database:</span></span>

1. <span data-ttu-id="7d57c-121">Meld u aan bij de [Azure-Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="7d57c-121">Login to the [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="7d57c-122">Klik op de **nieuw** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7d57c-122">Click the **New** icon.</span></span>
3. <span data-ttu-id="7d57c-123">Klik op **alle Zie** naast **Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="7d57c-123">Click **See All** next to **Marketplace**.</span></span> 
4. <span data-ttu-id="7d57c-124">Klik op **Web en mobiel**, klikt u vervolgens **webtoepassing + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="7d57c-124">Click **Web + Mobile**, then **Web app + MySQL**.</span></span> <span data-ttu-id="7d57c-125">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="7d57c-125">Then, click **Create**.</span></span>
5. <span data-ttu-id="7d57c-126">Voer een geldige naam voor de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="7d57c-126">Enter a valid name for your resource group.</span></span>
   
    ![Stel de naam van resourcegroep][resource-group]
6. <span data-ttu-id="7d57c-128">Geef waarden voor uw nieuwe web-app.</span><span class="sxs-lookup"><span data-stu-id="7d57c-128">Enter values for your new web app.</span></span>
   
    ![Een web-app maken][new-web-app]
7. <span data-ttu-id="7d57c-130">Geef waarden voor de nieuwe database, inclusief akkoord gaat met de juridische voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="7d57c-130">Enter values for your new database, including agreeing to the legal terms.</span></span>
   
    ![Nieuwe MySQL-database maken][new-mysql-db]
8. <span data-ttu-id="7d57c-132">Wanneer de web-app is gemaakt, ziet u de blade van de nieuwe web-app.</span><span class="sxs-lookup"><span data-stu-id="7d57c-132">When the web app has been created, you will see the new web app blade.</span></span>
9. <span data-ttu-id="7d57c-133">In **instellingen** klikt u op **continue implementatie**, klikt u op *vereiste instellingen configureren*.</span><span class="sxs-lookup"><span data-stu-id="7d57c-133">In **Settings** click on **Continuous Deployment**, then click on *Configure required settings*.</span></span>
   
    ![Git-publicatie instellen][setup-publishing]
10. <span data-ttu-id="7d57c-135">Selecteer **lokale Git-opslagplaats** voor de bron.</span><span class="sxs-lookup"><span data-stu-id="7d57c-135">Select **Local Git Repository** for the source.</span></span>
    
     ![Git-opslagplaats instellen][setup-repository]
11. <span data-ttu-id="7d57c-137">U moet een gebruikersnaam en wachtwoord opgeven zodat Git-publicatie.</span><span class="sxs-lookup"><span data-stu-id="7d57c-137">To enable Git publishing, you must provide a user name and password.</span></span> <span data-ttu-id="7d57c-138">Noteer de gebruikersnaam en wachtwoord die u maakt.</span><span class="sxs-lookup"><span data-stu-id="7d57c-138">Make a note of the user name and password you create.</span></span> <span data-ttu-id="7d57c-139">(Als u een Git-opslagplaats voordat hebt ingesteld, wordt deze stap overgeslagen.)</span><span class="sxs-lookup"><span data-stu-id="7d57c-139">(If you have set up a Git repository before, this step will be skipped.)</span></span>
    
     ![Publishing referenties maken][credentials]

## <a name="get-remote-mysql-connection-information"></a><span data-ttu-id="7d57c-141">Externe gegevens van MySQL-verbinding ophalen</span><span class="sxs-lookup"><span data-stu-id="7d57c-141">Get remote MySQL connection information</span></span>
<span data-ttu-id="7d57c-142">Verbinding maken met de MySQL-database die wordt uitgevoerd in de Web-Apps, uw wordt moet de verbindingsinformatie.</span><span class="sxs-lookup"><span data-stu-id="7d57c-142">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span></span> <span data-ttu-id="7d57c-143">Als u de verbindingsgegevens MySQL, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="7d57c-143">To get MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="7d57c-144">Klik op de database van de resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="7d57c-144">From your resource group, click the database:</span></span>
   
    ![Database selecteren][select-database]
2. <span data-ttu-id="7d57c-146">Uit de database **instellingen**, selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="7d57c-146">From the database **Settings**, select **Properties**.</span></span>
   
    ![Eigenschappen selecteren][select-properties]
3. <span data-ttu-id="7d57c-148">Noteer de waarden voor `Database`, `Host`, `User Id`, en `Password`.</span><span class="sxs-lookup"><span data-stu-id="7d57c-148">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Opmerking eigenschappen][note-properties]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="7d57c-150">Bouwen en testen van uw app lokaal</span><span class="sxs-lookup"><span data-stu-id="7d57c-150">Build and test your app locally</span></span>
<span data-ttu-id="7d57c-151">Nu dat u een web-app hebt gemaakt, kunt u de toepassing lokaal ontwikkelen vervolgens implementeren nadat u hebt getest.</span><span class="sxs-lookup"><span data-stu-id="7d57c-151">Now that you have created a web app, you can develop your application locally, then deploy it after testing.</span></span>

<span data-ttu-id="7d57c-152">De registratie van toepassing is een eenvoudige PHP-toepassing waarmee u te registreren voor een gebeurtenis aan de hand van uw naam en e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="7d57c-152">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="7d57c-153">Informatie over eerdere geregistreerde wordt weergegeven in een tabel.</span><span class="sxs-lookup"><span data-stu-id="7d57c-153">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="7d57c-154">Registratie-informatie wordt opgeslagen in een MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="7d57c-154">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="7d57c-155">De toepassing bestaat uit één bestand (kopiëren en plakken code hieronder):</span><span class="sxs-lookup"><span data-stu-id="7d57c-155">The application consists of one file (copy/paste code available below):</span></span>

* <span data-ttu-id="7d57c-156">**index.php**: een formulier voor registratie en een tabel met registrant informatie wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7d57c-156">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>

<span data-ttu-id="7d57c-157">Voor het bouwen en de toepassing lokaal uitvoeren, de volgende stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="7d57c-157">To build and run the application locally, follow the steps below.</span></span> <span data-ttu-id="7d57c-158">Houd er rekening mee dat deze stappen wordt ervan uitgegaan u hebt de PHP en de MySQL-opdrachtregelhulpprogramma (onderdeel van MySQL dat) instellen op uw lokale computer en die u hebt ingeschakeld de [PDO-extensie voor MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="7d57c-158">Note that these steps assume you have the PHP and MySQL Command-Line Tool (part of MySQL) set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="7d57c-159">Verbinding maken met de externe MySQL-server, met de waarde voor `Data Source`, `User Id`, `Password`, en `Database` die u eerder hebt opgehaald:</span><span class="sxs-lookup"><span data-stu-id="7d57c-159">Connect to the remote MySQL server, using the value for `Data Source`, `User Id`, `Password`, and `Database` that you retrieved earlier:</span></span>
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. <span data-ttu-id="7d57c-160">De MySQL-opdrachtprompt wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7d57c-160">The MySQL command prompt will appear:</span></span>
   
        mysql>
3. <span data-ttu-id="7d57c-161">Plakken in de volgende `CREATE TABLE` opdracht maken de `registration_tbl` tabel in de database:</span><span class="sxs-lookup"><span data-stu-id="7d57c-161">Paste in the following `CREATE TABLE` command to create the `registration_tbl` table in your database:</span></span>
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. <span data-ttu-id="7d57c-162">Maak in de hoofdmap van uw lokale map application **index.php** bestand.</span><span class="sxs-lookup"><span data-stu-id="7d57c-162">In the root of your local application folder create **index.php** file.</span></span>
5. <span data-ttu-id="7d57c-163">Open de **index.php** bestand in een teksteditor of IDE en voeg de volgende code en voer de benodigde wijzigingen gemarkeerd met `//TODO:` opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="7d57c-163">Open the **index.php** file in a text editor or IDE and add the following code, and complete the necessary changes marked with `//TODO:` comments.</span></span>

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
            // DB connection info
            //TODO: Update the values for $host, $user, $pwd, and $db
            //using the values you retrieved earlier from the Azure Portal.
            $host = "value of Data Source";
            $user = "value of User Id";
            $pwd = "value of Password";
            $db = "value of Database";
            // Connect to database.
            try {
                $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
                $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            }
            catch(Exception $e){
                die(var_dump($e));
            }
            // Insert registration info
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
            // Retrieve data
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
        ?>
        </body>
        </html>

1. <span data-ttu-id="7d57c-164">Ga naar de map van uw toepassing in een terminal en typ de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7d57c-164">In a terminal go to your application folder and type the following command:</span></span>
   
       php -S localhost:8000

<span data-ttu-id="7d57c-165">Nu kunt u bladeren naar **http://localhost: 8000 /** test de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7d57c-165">You can now browse to **http://localhost:8000/** to test the application.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="7d57c-166">Uw app publiceren</span><span class="sxs-lookup"><span data-stu-id="7d57c-166">Publish your app</span></span>
<span data-ttu-id="7d57c-167">Nadat u uw app lokaal hebt getest, kunt u het publiceren op Web-Apps met Git.</span><span class="sxs-lookup"><span data-stu-id="7d57c-167">After you have tested your app locally, you can publish it to Web Apps using Git.</span></span> <span data-ttu-id="7d57c-168">U uw lokale Git-opslagplaats te initialiseren en publiceer de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7d57c-168">You will initialize your local Git repository and publish the application.</span></span>

> [!NOTE]
> <span data-ttu-id="7d57c-169">Dit zijn dezelfde stappen in de Azure-Portal aan het einde van het maken van een web-app en een Set up Git Publishing sectie hierboven.</span><span class="sxs-lookup"><span data-stu-id="7d57c-169">These are the same steps shown in the Azure Portal at the end of the Create a web app and Set up Git Publishing section above.</span></span>
> 
> 

1. <span data-ttu-id="7d57c-170">(Optioneel)  Als u hebt vergeten of de URL van de externe repostitory Git foutief worden geplaatst, gaat u naar de eigenschappen van het web-app in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7d57c-170">(Optional)  If you've forgotten or misplaced your Git remote repostitory URL, navigate to the web app properties on the Azure Portal.</span></span>
2. <span data-ttu-id="7d57c-171">Open GitBash (of een terminal als Git in uw `PATH`), wijzig de mappen in de hoofdmap van uw toepassing en voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="7d57c-171">Open GitBash (or a terminal, if Git is in your `PATH`), change directories to the root directory of your application, and run the following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="7d57c-172">U wordt gevraagd om het wachtwoord dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7d57c-172">You will be prompted for the password you created earlier.</span></span>
   
    ![Initiële Push naar Azure via Git][git-initial-push]
3. <span data-ttu-id="7d57c-174">Blader naar **http://[site name].azurewebsites.net/index.php** om te beginnen met behulp van de toepassing (deze informatie wordt opgeslagen op uw dashboard account):</span><span class="sxs-lookup"><span data-stu-id="7d57c-174">Browse to **http://[site name].azurewebsites.net/index.php** to begin using the application (this information will be stored on your account dashboard):</span></span>
   
    ![Azure PHP-website][running-app]

<span data-ttu-id="7d57c-176">Nadat u uw app hebt gepubliceerd, kunt u beginnen wijzigingen aanbrengen en Git gebruiken om te publiceren.</span><span class="sxs-lookup"><span data-stu-id="7d57c-176">After you have published your app, you can begin making changes to it and use Git to publish them.</span></span>

## <a name="publish-changes-to-your-app"></a><span data-ttu-id="7d57c-177">Wijzigingen aan uw app publiceren</span><span class="sxs-lookup"><span data-stu-id="7d57c-177">Publish changes to your app</span></span>
<span data-ttu-id="7d57c-178">Als u wilt publiceren wijzigingen aan uw app, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="7d57c-178">To publish changes to your app, follow these steps:</span></span>

1. <span data-ttu-id="7d57c-179">Wijzigingen aanbrengen in uw app lokaal.</span><span class="sxs-lookup"><span data-stu-id="7d57c-179">Make changes to your app locally.</span></span>
2. <span data-ttu-id="7d57c-180">Open GitBash (of een terminal it Git is in uw `PATH`), wijzig de mappen in de hoofdmap van uw app en voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="7d57c-180">Open GitBash (or a terminal, it Git is in your `PATH`), change directories to the root directory of your app, and run the following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="7d57c-181">U wordt gevraagd om het wachtwoord dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7d57c-181">You will be prompted for the password you created earlier.</span></span>
   
    ![Sitewijzigingen pushen naar Azure via Git][git-change-push]
3. <span data-ttu-id="7d57c-183">Blader naar **http://[site name].azurewebsites.net/index.php** om te zien van uw app en eventuele wijzigingen die u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="7d57c-183">Browse to **http://[site name].azurewebsites.net/index.php** to see your app and any changes you may have made:</span></span>
   
    ![Azure PHP-website][running-app]

> [!NOTE]
> <span data-ttu-id="7d57c-185">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="7d57c-185">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7d57c-186">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="7d57c-186">No credit cards required; no commitments.</span></span>
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-the-composer-extension"></a><span data-ttu-id="7d57c-187">Composer automatiseren met de Composer-extensie</span><span class="sxs-lookup"><span data-stu-id="7d57c-187">Enable Composer automation with the Composer extension</span></span>
<span data-ttu-id="7d57c-188">Standaard biedt geen de git-implementatieproces in App Service niets doen met composer.json, als u in uw PHP-project hebt.</span><span class="sxs-lookup"><span data-stu-id="7d57c-188">By default, the git deployment process in App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="7d57c-189">U kunt inschakelen composer.json tijdens de verwerking `git push` doordat de Composer-extensie.</span><span class="sxs-lookup"><span data-stu-id="7d57c-189">You can enable composer.json processing during `git push` by enabling the Composer extension.</span></span>

1. <span data-ttu-id="7d57c-190">In uw PHP web-app blade in de [Azure-portal][management-portal], klikt u op **extra** > **extensies**.</span><span class="sxs-lookup"><span data-stu-id="7d57c-190">In your PHP web app's blade in the [Azure portal][management-portal], click **Tools** > **Extensions**.</span></span>
   
    ![Composer-extensie-instellingen][composer-extension-settings]
2. <span data-ttu-id="7d57c-192">Klik op **toevoegen**, klikt u vervolgens op **Composer**.</span><span class="sxs-lookup"><span data-stu-id="7d57c-192">Click **Add**, then click **Composer**.</span></span>
   
    ![Composer-extensie toevoegen][composer-extension-add]
3. <span data-ttu-id="7d57c-194">Klik op **OK** juridische voorwaarden accepteren.</span><span class="sxs-lookup"><span data-stu-id="7d57c-194">Click **OK** to accept legal terms.</span></span> <span data-ttu-id="7d57c-195">Klik op **OK** om opnieuw toe te voegen van de extensie.</span><span class="sxs-lookup"><span data-stu-id="7d57c-195">Click **OK** again to add the extension.</span></span>
   
    <span data-ttu-id="7d57c-196">De **extensies geïnstalleerd** blade ziet nu de Composer-extensie.</span><span class="sxs-lookup"><span data-stu-id="7d57c-196">The **Installed extensions** blade will now show the Composer extension.</span></span>  
    <span data-ttu-id="7d57c-197">![Composer-extensie weergeven][composer-extension-view]</span><span class="sxs-lookup"><span data-stu-id="7d57c-197">![Composer Extension View][composer-extension-view]</span></span>
4. <span data-ttu-id="7d57c-198">Nu uitvoeren `git add`, `git commit`, en `git push` zoals in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="7d57c-198">Now, perform `git add`, `git commit`, and `git push` like in the previous section.</span></span> <span data-ttu-id="7d57c-199">Nu ziet u dat Composer afhankelijkheden die zijn gedefinieerd in composer.json wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7d57c-199">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Composer-extensie geslaagd][composer-extension-success]

## <a name="next-steps"></a><span data-ttu-id="7d57c-201">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7d57c-201">Next steps</span></span>
<span data-ttu-id="7d57c-202">Zie voor meer informatie de [PHP-ontwikkelaarscentrum](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="7d57c-202">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

<!-- URL List -->

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[install-mysql]: http://dev.mysql.com/downloads/mysql/
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[management-portal]: https://portal.azure.com
[sql-database-editions]: http://msdn.microsoft.com/library/windowsazure/ee621788.aspx

<!-- IMG List -->

[running-app]: ./media/web-sites-php-mysql-deploy-use-git/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-git/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-git/create_web_mysql.png
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-git/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-git/select_webapp.png
[setup-git-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_git_publishing.png
[credentials]: ./media/web-sites-php-mysql-deploy-use-git/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-git/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-git/create_wa.png
[setup-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_deploy.png
[setup-repository]: ./media/web-sites-php-mysql-deploy-use-git/select_local_git.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-git/select_database.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-git/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-git/note-properties.png

[git-instructions]: ./media/web-sites-php-mysql-deploy-use-git/git-instructions.png
[git-change-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-change-push.png
[git-initial-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-initial-push.png

[composer-extension-settings]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-settings.png
[composer-extension-add]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-add.png
[composer-extension-view]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-view.png
[composer-extension-success]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-success.png
