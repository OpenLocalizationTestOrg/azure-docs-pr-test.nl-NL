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
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a>Een PHP-SQL-web-app maken en implementeren van tooAzure App Service met Git
Deze zelfstudie laat zien hoe een PHP-toocreate web-app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) tooAzure SQL-Database die is verbonden en hoe toodeploy met Git. Deze zelfstudie wordt ervan uitgegaan dat u hebt [PHP][install-php], [SQL Server Express][install-SQLExpress], Hallo [Microsoft-Drivers voor SQL Server voor PHP ](http://www.microsoft.com/download/en/details.aspx?id=20098), en [Git] [ install-git] op uw computer geïnstalleerd. Bij voltooiing van deze handleiding hebt u een PHP-SQL-web-app in Azure wordt uitgevoerd.

> [!NOTE]
> U kunt installeren en PHP, SQL Server Express en Microsoft-Drivers Hallo voor SQL Server configureren voor PHP met Hallo [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).
> 
> 

U leert:

* Hoe toocreate een Azure web-app en een SQL-Database met behulp van Hallo [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715). Omdat PHP is standaard ingeschakeld in App Service Web Apps, er is niets speciale vereist toorun is uw PHP-code.
* Hoe toopublish en uw toepassing tooAzure met Git opnieuw te publiceren.

Door deze zelfstudie te volgen, bouwt u een webtoepassing eenvoudig registratie in PHP. Hallo-toepassing wordt gehost in een Azure-Website. Een schermopname van de toepassing hello voltooid lager is dan:

![Azure PHP-website](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a>Een Azure-web-app maken en Git-publicatie instellen
Volg deze stappen toocreate een Azure-web-app en een SQL-Database:

1. Meld u bij toohello [Azure Portal](https://portal.azure.com/).
2. Open hello Azure Marketplace door te klikken op Hallo **nieuw** pictogram Hallo bovenaan links van Hallo dashboard, klikt u op **Alles selecteren** volgende tooMarketplace en het selecteren van **Web en mobiel**.
3. Selecteer in de Hallo Marketplace, **Web en mobiel**.
4. Klik op Hallo **webtoepassing + SQL** pictogram.
5. Na het lezen van Hallo beschrijving van het Hallo-webtoepassing + SQL-app, selecteer **maken**.
6. Klik op elk onderdeel (**resourcegroep**, **Web-App**, **Database**, en **abonnement**) en typ of Selecteer waarden voor Hallo vereist velden:
   
   * Voer een URL-naam van uw keuze    
   * Referenties voor database-server configureren
   * Hallo regio dichtstbijzijnde tooyou selecteren
     
     ![de app configureren](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. Wanneer u klaar bent met definiëren Hallo web-app, klikt u op **maken**.
   
    Wanneer het Hallo-web-app is gemaakt, Hallo **meldingen** knop knippert een groene **geslaagd** en resource groep blade open tooshow beide Hallo web app en Hallo SQL-database in de groep Hallo Hallo.
8. Klik op Hallo van web-app-pictogram op de blade Hallo resource groep blade tooopen Hallo van web-app.
   
    ![Web-app van resourcegroep](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. In **instellingen** klikt u op **continue implementatie** > **vereiste instellingen configureren**. Selecteer **lokale Git-opslagplaats** en klik op **OK**.
   
    ![waar is de broncode](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    Als u een Git-opslagplaats voordat niet hebt ingesteld, moet u een gebruikersnaam en wachtwoord opgeven. toodo, klikt u op **instellingen** > **implementatiereferenties** op Hallo van web-app-blade.
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. In **instellingen** klikt u op **eigenschappen** toosee Hallo Git externe URL u toouse toodeploy uw PHP-app later nodig.

## <a name="get-sql-database-connection-information"></a>Gegevens van de SQL-Database-verbinding ophalen
tooconnect toohello SQL Database-exemplaar dat is gekoppeld tooyour web-app, uw wordt moet Hallo verbindingsgegevens die u hebt opgegeven toen u het Hallo-database gemaakt. tooget hello verbindingsinformatie voor SQL-Database, als volgt te werk:

1. Terug in de blade Hallo resourcegroep bevindt, klikt u op het pictogram Hallo SQL database.
2. Klik op de blade Hallo SQL database **instellingen** > **eigenschappen**, klikt u vervolgens op **databaseverbindingsreeksen tonen**. 
   
    ![Database-eigenschappen weergeven](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. Van Hallo **PHP** sectie van de resulterende dialoogvenster hello, noteer Hallo waarden voor `Server`, `SQL Database`, en `User Name`. U gebruikt deze waarden later wanneer publiceren van uw app tooAzure voor PHP web-App Service.

## <a name="build-and-test-your-application-locally"></a>De toepassing lokaal bouwen en testen
Hallo registratie van toepassing is een eenvoudige PHP-toepassing waarmee u tooregister voor een gebeurtenis aan de hand van uw naam en e-mailadres. Informatie over eerdere geregistreerde wordt weergegeven in een tabel. Registratie-informatie wordt opgeslagen in een SQL Database-exemplaar. Hallo toepassing bestaat uit twee bestanden (kopiëren en plakken code hieronder):

* **index.php**: een formulier voor registratie en een tabel met registrant informatie wordt weergegeven.
* **CreateTable.php**: Hallo SQL-databasetabel voor Hallo toepassing maakt. Dit bestand wordt slechts eenmaal worden gebruikt.

toorun hello toepassing lokaal door Hallo volgende stappen. Merk op dat u deze stappen wordt ervan uitgegaan dat u PHP en SQL Server Express instellen op uw lokale computer en dat u hebt ingeschakeld Hallo [PDO-extensie voor SQL Server][pdo-sqlsrv].

1. Maken van een SQL Server-database aangeroepen `registration`. U kunt dit doen vanuit Hallo `sqlcmd` opdrachtprompt met de volgende opdrachten:
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. In de hoofdmap van uw toepassing maakt u twee bestanden in deze - een met de naam `createtable.php` en één aangeroepen `index.php`.
3. Open Hallo `createtable.php` in een teksteditor of IDE-bestand en voeg Hallo code hieronder. Deze code worden gebruikte toocreate hello `registration_tbl` tabel in Hallo `registration` database.
   
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
   
    Houd er rekening mee dat u moet tooupdate Hallo waarden voor <code>$user</code> en <code>$pwd</code> met uw lokale SQL Server-gebruikersnaam en wachtwoord.
4. In een terminal in de hoofdmap Hallo Hallo toepassing type Hallo volgende opdracht:
   
        php -S localhost:8000
5. Open een webbrowser en te bladeren**http://localhost:8000/createtable.php**. Hiermee maakt u Hallo `registration_tbl` tabel in Hallo-database.
6. Open Hallo **index.php** in een teksteditor of IDE-bestand en voeg Hallo basic HTML en CSS-code voor Hallo pagina (Hallo PHP code wordt toegevoegd in latere stappen).
   
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
7. Binnen Hallo PHP tags toevoegen PHP-code voor het verbinden van toohello database.
   
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
   
    Opnieuw, moet u tooupdate Hallo waarden voor <code>$user</code> en <code>$pwd</code> met uw lokale MySQL-gebruikersnaam en wachtwoord.
8. Volgende Hallo database verbinding code, voeg code toe voor registratie-informatie in het Hallo-database invoegen.
   
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
9. Na de bovenstaande Hallo code, voeg code voor het ophalen van gegevens uit het Hallo-database.
   
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

U kunt nu te bladeren**http://localhost:8000/index.php** tootest Hallo-toepassing.

## <a name="publish-your-application"></a>Uw toepassing publiceren
Nadat u uw toepassing lokaal hebt getest, kunt u deze tooApp Service Web Apps met Git publiceren. Echter, moet u eerst tooupdate Hallo databaseverbindingsgegevens in Hallo-toepassing. Hallo databaseverbindingsgegevens u eerder hebt verkregen met (in Hallo **verbindingsgegevens ophalen van de SQL-Database** sectie), update Hallo volgende informatie in **beide** hello `createdatabase.php` en `index.php` bestanden met Hallo waarden nodig:

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> In Hallo <code>$host</code>, Hallo-waarde van de Server moet worden voorafgegaan door <code>tcp:</code>.
> 
> 

Nu u bent klaar tooset van Git-publicatie en Hallo toepassing publiceren.

> [!NOTE]
> Dit zijn dezelfde stappen vermeld achter Hallo HALLO hallo **een Azure-web-app maken en Git-publicatie instellen** sectie hierboven.
> 
> 

1. Open GitBash (of een terminal als Git in uw `PATH`), mappen toohello hoofdmap van uw toepassing wijzigen (Hallo **registratie** directory), en Voer Hallo de volgende opdrachten:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    U wordt gevraagd om Hallo wachtwoord die u eerder hebt gemaakt.
2. Te bladeren**http://[web app name].azurewebsites.net/createtable.php** toocreate Hallo SQL-databasetabel voor Hallo-toepassing.
3. Te bladeren**http://[web app name].azurewebsites.net/index.php** toobegin met Hallo-toepassing.

Nadat u uw toepassing hebt gepubliceerd, kunt u beginnen met het maken van wijzigingen tooit en Git toopublish gebruiken ze. 

## <a name="publish-changes-tooyour-application"></a>Wijzigingen tooyour toepassing publiceren
toopublish tooapplication, verandert als volgt te werk:

1. Breng wijzigingen tooyour toepassing lokaal.
2. Open GitBash (of een terminal it Git is in uw `PATH`), mappen toohello hoofdmap van uw toepassing te wijzigen en uitvoeren van Hallo volgende opdrachten:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    U wordt gevraagd om Hallo wachtwoord die u eerder hebt gemaakt.
3. Te bladeren**http://[web app name].azurewebsites.net/index.php** toosee uw wijzigingen.

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

