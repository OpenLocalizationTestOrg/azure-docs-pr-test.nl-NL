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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a>Een PHP-MySQL-webtoepassing maken in Azure App Service en implementeren met FTP
Deze zelfstudie leert u hoe u een PHP-MySQL toocreate web-app en hoe toodeploy via FTP. Deze zelfstudie wordt ervan uitgegaan dat u hebt [PHP][install-php], [MySQL][install-mysql], een webserver en een FTP-client op uw computer geïnstalleerd. Hallo-instructies in deze zelfstudie kunnen worden uitgevoerd op elk besturingssysteem, met inbegrip van Windows, Mac en Linux. Bij voltooiing van deze handleiding hebt u een PHP/MySQL-web-app in Azure wordt uitgevoerd.

U leert:

* Een web-app en een MySQL-database met toocreate Hallo hoe Azure-Portal. Omdat PHP is standaard ingeschakeld in de Web-Apps, er is niets speciale vereist toorun is uw PHP-code.
* Hoe uw toepassing tooAzure met toopublish FTP.

Door deze zelfstudie te volgen, bouwt u een web-app voor eenvoudige registratie in PHP. Hallo-toepassing wordt gehost in een Web-App. Een schermopname van de toepassing hello voltooid lager is dan:

![Azure PHP-website][running-app]

> [!NOTE]
> Als u wilt dat tooget voordat u zich aanmeldt voor een account met Azure App Service is gestart, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen. 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a>Maken van een web-app en FTP-publicatie instellen
Volg deze stappen toocreate een web-app en een MySQL-database:

1. Aanmelding toohello [Azure Portal][management-portal].
2. Klik op Hallo **+ nieuw** pictogram Hallo bovenaan links van de hello Azure-Portal.
   
    ![Nieuwe Azure-website maken][new-website]
3. In het Hallo-Zoektype **webtoepassing + MySQL** en klik op **webtoepassing + MySQL**.
   
    ![Aangepast maken een nieuwe website][custom-create]
4. Klik op **Create**. Voer een unieke app service-naam, een geldige naam voor de resourcegroep Hallo en een nieuwe service-abonnement.
   
    ![Stel de naam van resourcegroep][resource-group]
5. Voer waarden in voor de nieuwe database, inclusief ermee akkoord toohello juridische voorwaarden.
   
    ![Nieuwe MySQL-database maken][new-mysql-db]
6. Als het Hallo-web-app is gemaakt, ziet u Hallo blade nieuwe app service.
7. Klik op **instellingen** > **implementatiereferenties**. 
   
    ![Implementatiereferenties instellen][set-deployment-credentials]
8. tooenable FTP publiceren, moet u opgeven een gebruikersnaam en wachtwoord. Hallo-referenties op te slaan en maak een notitie van Hallo-gebruikersnaam en wachtwoord die u maakt.
   
    ![Publishing referenties maken][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a>Bouwen en testen van uw app lokaal
Hallo registratie van toepassing is een eenvoudige PHP-toepassing waarmee u tooregister voor een gebeurtenis aan de hand van uw naam en e-mailadres. Informatie over eerdere geregistreerde wordt weergegeven in een tabel. Registratie-informatie wordt opgeslagen in een MySQL-database. Hallo app bestaat uit twee bestanden:

* **index.php**: een formulier voor registratie en een tabel met registrant informatie wordt weergegeven.
* **CreateTable.php**: Hallo MySQL tabel voor de toepassing hello wordt gemaakt. Dit bestand wordt slechts eenmaal worden gebruikt.

toobuild en lokaal uitvoeren Hallo app stappen Hallo volgende. Merk op dat u deze stappen wordt ervan uitgegaan u hebt PHP, MySQL en een webserver instellen op uw lokale computer en dat dat u hebt ingeschakeld Hallo [PDO-extensie voor MySQL][pdo-mysql].

1. Maak een MySQL-database aangeroepen `registration`. U kunt dit doen vanaf Hallo MySQL-opdrachtprompt met deze opdracht:
   
        mysql> create database registration;
2. Maak een map in de hoofdmap van de webserver, `registration` en maakt u twee bestanden in deze - een met de naam `createtable.php` en één aangeroepen `index.php`.
3. Open Hallo `createtable.php` in een teksteditor of IDE-bestand en voeg Hallo code hieronder. Deze code worden gebruikte toocreate hello `registration_tbl` tabel in Hallo `registration` database.
   
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
   > U moet tooupdate Hallo waarden voor <code>$user</code> en <code>$pwd</code> met uw lokale MySQL-gebruikersnaam en wachtwoord.
   > 
   > 
4. Open een webbrowser en te bladeren[http://localhost/registration/createtable.php][localhost-createtable]. Hiermee maakt u Hallo `registration_tbl` tabel in Hallo-database.
5. Open Hallo **index.php** in een teksteditor of IDE-bestand en voeg Hallo basic HTML en CSS-code voor Hallo pagina (Hallo PHP code wordt toegevoegd in latere stappen).
   
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
6. Binnen Hallo PHP tags toevoegen PHP-code voor het verbinden van toohello database.
   
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
   > Opnieuw, moet u tooupdate Hallo waarden voor <code>$user</code> en <code>$pwd</code> met uw lokale MySQL-gebruikersnaam en wachtwoord.
   > 
   > 
7. Volgende Hallo database verbinding code, voeg code toe voor registratie-informatie in het Hallo-database invoegen.
   
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
8. Na de bovenstaande Hallo code, voeg code voor het ophalen van gegevens uit het Hallo-database.
   
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

U kunt nu te bladeren[http://localhost/registration/index.php] [ localhost-index] tootest Hallo app.

## <a name="get-mysql-and-ftp-connection-information"></a>MySQL- en FTP-verbindingsgegevens ophalen
tooconnect toohello MySQL-database die wordt uitgevoerd in de Web-Apps, uw wordt moet Hallo verbindingsgegevens. tooget verbindingsinformatie MySQL, als volgt te werk:

1. Blade web-app klikt u op op Hallo resource groep koppeling van Hallo-app service:
   
    ![Resourcegroep selecteren][select-resourcegroup]
2. Klik op Hallo-database van de resourcegroep:
   
    ![Database selecteren][select-database]
3. Hallo database samenvatting, selecteer **instellingen** > **eigenschappen**.
   
    ![Eigenschappen selecteren][select-properties]
4. Noteer Hallo waarden voor `Database`, `Host`, `User Id`, en `Password`.
   
    ![Opmerking eigenschappen][note-properties]
5. Klik op Hallo van uw web-app **publicatieprofiel downloaden** op Hallo rechterbenedenhoek van de pagina Hallo koppeling:
   
    ![Publicatieprofiel downloaden][download-publish-profile]
6. Open Hallo `.publishsettings` bestand in een XML-editor. 
7. Hallo zoeken `<publishProfile >` element met `publishMethod="FTP"` die vergelijkbaar toothis zoekt:
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

Noteer Hallo `publishUrl`, `userName`, en `userPWD` kenmerken.

## <a name="publish-your-app"></a>Uw app publiceren
Nadat u uw app lokaal hebt getest, kunt u deze tooyour web-app met FTP publiceren. Echter, moet u eerst tooupdate Hallo databaseverbindingsgegevens in Hallo-toepassing. Hallo databaseverbindingsgegevens u eerder hebt verkregen met (in Hallo **ophalen MySQL- en FTP-verbindingsgegevens** sectie), update Hallo volgende informatie in **beide** hello `createdatabase.php` en `index.php` bestanden met Hallo waarden nodig:

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

U bent er nu klaar toopublish uw app met FTP.

1. Open uw FTP-client naar keuze.
2. Voer Hallo *hostnaamgedeelte* van Hallo `publishUrl` kenmerk u hierboven hebt genoteerd in uw FTP-client.
3. Voer Hallo `userName` en `userPWD` kenmerken die u hierboven hebt genoteerd ongewijzigd in uw FTP-client.
4. Een verbinding tot stand brengen.

Nadat u verbinding hebt gemaakt wordt u kunnen tooupload en bestanden downloaden naar behoefte. Zorg ervoor dat u uploadt bestanden toohello hoofdmap, namelijk `/site/wwwroot`.

Na het uploaden van beide `index.php` en `createtable.php`, te bladeren**http://[site name].azurewebsites.net/createtable.php** toocreate Hallo MySQL tabel voor de toepassing hello en vervolgens te bladeren**http://[site naam ].azurewebsites.net/index.php** toobegin met Hallo-toepassing.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie, Hallo [PHP-ontwikkelaarscentrum](/develop/php/).

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

