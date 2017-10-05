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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a>Een PHP-MySQL-webtoepassing maken in Azure App Service en implementeren met FTP
Deze zelfstudie ziet u hoe u een PHP-MySQL web-app maken en implementeren met behulp van FTP. Deze zelfstudie wordt ervan uitgegaan dat u hebt [PHP][install-php], [MySQL][install-mysql], een webserver en een FTP-client op uw computer geïnstalleerd. De instructies in deze zelfstudie kunnen worden uitgevoerd op elk besturingssysteem, met inbegrip van Windows, Mac en Linux. Bij voltooiing van deze handleiding hebt u een PHP/MySQL-web-app in Azure wordt uitgevoerd.

U leert:

* Het maken van een web-app en een MySQL-database met de Azure-Portal. Omdat PHP is standaard ingeschakeld in de Web-Apps, vereist geen speciale uw PHP-code uit te voeren.
* Hoe uw toepassing publiceren in Azure met FTP.

Door deze zelfstudie te volgen, bouwt u een web-app voor eenvoudige registratie in PHP. De toepassing zal worden gehost in een Web-App. Een schermopname van de voltooide toepassing lager is dan:

![Azure PHP-website][running-app]

> [!NOTE]
> Als u wilt dat aan de slag met Azure App Service voordat u zich aanmeldt voor een account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen. 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a>Maken van een web-app en FTP-publicatie instellen
Volg deze stappen om een web-app en een MySQL-database te maken:

1. Meld u aan bij de [Azure-Portal][management-portal].
2. Klik op de **+ nieuw** pictogram op de bovenste links van de Azure-Portal.
   
    ![Nieuwe Azure-website maken][new-website]
3. In het type zoekopdracht **webtoepassing + MySQL** en klik op **webtoepassing + MySQL**.
   
    ![Aangepast maken een nieuwe website][custom-create]
4. Klik op **Create**. Geef een unieke app service-naam, een geldige naam voor de resourcegroep en een nieuwe service-abonnement.
   
    ![Stel de naam van resourcegroep][resource-group]
5. Geef waarden voor de nieuwe database, inclusief akkoord gaat met de juridische voorwaarden.
   
    ![Nieuwe MySQL-database maken][new-mysql-db]
6. Wanneer de web-app is gemaakt, ziet u de nieuwe app service-blade.
7. Klik op **instellingen** > **implementatiereferenties**. 
   
    ![Implementatiereferenties instellen][set-deployment-credentials]
8. Om FTP-publicatie, moet u een gebruikersnaam en wachtwoord opgeven. Sla de referenties op en noteer de gebruikersnaam en wachtwoord die u maakt.
   
    ![Publishing referenties maken][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a>Bouwen en testen van uw app lokaal
De registratie van toepassing is een eenvoudige PHP-toepassing waarmee u te registreren voor een gebeurtenis aan de hand van uw naam en e-mailadres. Informatie over eerdere geregistreerde wordt weergegeven in een tabel. Registratie-informatie wordt opgeslagen in een MySQL-database. De app bestaat uit twee bestanden:

* **index.php**: een formulier voor registratie en een tabel met registrant informatie wordt weergegeven.
* **CreateTable.php**: de MySQL-tabel voor de toepassing maakt. Dit bestand wordt slechts eenmaal worden gebruikt.

Voor het bouwen en de app lokaal uitvoeren, de volgende stappen uit te voeren. Houd er rekening mee dat deze stappen wordt ervan uitgegaan dat u hebt PHP, MySQL en een webserver instellen op uw lokale computer en die u hebt ingeschakeld de [PDO-extensie voor MySQL][pdo-mysql].

1. Maak een MySQL-database aangeroepen `registration`. U kunt dit doen vanaf de opdrachtprompt MySQL met deze opdracht:
   
        mysql> create database registration;
2. Maak een map in de hoofdmap van de webserver, `registration` en maakt u twee bestanden in deze - een met de naam `createtable.php` en één aangeroepen `index.php`.
3. Open de `createtable.php` in een teksteditor of IDE-bestand en voeg de onderstaande code. Deze code wordt gebruikt voor het maken van de `registration_tbl` tabel de `registration` database.
   
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
   > U moet de waarden voor bijwerken <code>$user</code> en <code>$pwd</code> met uw lokale MySQL-gebruikersnaam en wachtwoord.
   > 
   > 
4. Open een webbrowser en blader naar [http://localhost/registration/createtable.php][localhost-createtable]. Hiermee maakt u de `registration_tbl` tabel in de database.
5. Open de **index.php** in een teksteditor of IDE-bestand en voeg de basic HTML en CSS-code voor de pagina (de PHP-code wordt toegevoegd in latere stappen).
   
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
6. Binnen de PHP-tags toevoegen PHP-code voor het verbinden met de database.
   
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
   > Opnieuw, moet u de waarden voor bijwerken <code>$user</code> en <code>$pwd</code> met uw lokale MySQL-gebruikersnaam en wachtwoord.
   > 
   > 
7. Na de code van de database-verbinding, voeg code toe voor de registratiegegevens worden ingevoegd in de database.
   
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
8. Na de code, voeg de code voor het ophalen van gegevens uit de database.
   
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

Nu kunt u bladeren naar [http://localhost/registration/index.php] [ localhost-index] voor het testen van de app.

## <a name="get-mysql-and-ftp-connection-information"></a>MySQL- en FTP-verbindingsgegevens ophalen
Verbinding maken met de MySQL-database die wordt uitgevoerd in de Web-Apps, uw wordt moet de verbindingsinformatie. Als u de verbindingsgegevens MySQL, de volgende stappen uit:

1. Blade web-app klikt u op op de koppeling van de groep resource van de app service:
   
    ![Resourcegroep selecteren][select-resourcegroup]
2. Klik op de database van de resourcegroep:
   
    ![Database selecteren][select-database]
3. Selecteer in de database samenvatting **instellingen** > **eigenschappen**.
   
    ![Eigenschappen selecteren][select-properties]
4. Noteer de waarden voor `Database`, `Host`, `User Id`, en `Password`.
   
    ![Opmerking eigenschappen][note-properties]
5. Klik in uw web-app op de **publicatieprofiel downloaden** koppeling in de rechterbenedenhoek van de pagina:
   
    ![Publicatieprofiel downloaden][download-publish-profile]
6. Open de `.publishsettings` bestand in een XML-editor. 
7. Zoek de `<publishProfile >` element met `publishMethod="FTP"` die ziet er ongeveer als volgt uit:
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

Noteer de `publishUrl`, `userName`, en `userPWD` kenmerken.

## <a name="publish-your-app"></a>Uw app publiceren
Nadat u uw app lokaal hebt getest, kunt u het publiceren naar uw web-app met FTP. Echter, moet u eerst de verbindingsgegevens voor de database in de toepassing bijwerken. Met de database-verbindingsgegevens die u eerder hebt verkregen (in de **ophalen MySQL- en FTP-verbindingsgegevens** sectie), werkt u de volgende gegevens in **beide** de `createdatabase.php` en `index.php` bestanden met de juiste waarden:

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

U bent nu klaar voor het publiceren van uw app met FTP.

1. Open uw FTP-client naar keuze.
2. Voer de *hostnaamgedeelte* van de `publishUrl` kenmerk u hierboven hebt genoteerd in uw FTP-client.
3. Voer de `userName` en `userPWD` kenmerken die u hierboven hebt genoteerd ongewijzigd in uw FTP-client.
4. Een verbinding tot stand brengen.

Nadat u verbinding hebt gemaakt kunt u zich bestanden uploaden en downloaden naar behoefte. Zorg ervoor dat u uploaden van bestanden naar de hoofdmap `/site/wwwroot`.

Na het uploaden van beide `index.php` en `createtable.php`, blader naar **http://[site name].azurewebsites.net/createtable.php** voor het maken van de MySQL-tabel voor de toepassing en blader vervolgens naar **http://[site name].azurewebsites.net/index.php** om te beginnen met behulp van de toepassing.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie de [PHP-ontwikkelaarscentrum](/develop/php/).

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

