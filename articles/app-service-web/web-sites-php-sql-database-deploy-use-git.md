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
# <a name="create-a-php-sql-web-app-and-deploy-to-azure-app-service-using-git"></a>Een PHP-SQL-web-app maken en implementeren in Azure App Service met Git
Deze zelfstudie ziet u het maken van een PHP-web-app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) die verbinding maakt met Azure SQL Database en implementeren met behulp van Git. Deze zelfstudie wordt ervan uitgegaan dat u hebt [PHP][install-php], [SQL Server Express][install-SQLExpress], wordt de [Microsoft-Drivers voor SQL Server voor PHP ](http://www.microsoft.com/download/en/details.aspx?id=20098), en [Git] [ install-git] op uw computer geïnstalleerd. Bij voltooiing van deze handleiding hebt u een PHP-SQL-web-app in Azure wordt uitgevoerd.

> [!NOTE]
> U kunt installeren en configureren van PHP, SQL Server Express en de Microsoft-Drivers voor SQL Server voor het gebruik van PHP de [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).
> 
> 

U leert:

* Het maken van een Azure-web-app en een SQL-Database met de [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715). Omdat PHP is standaard ingeschakeld in App Service Web Apps, vereist geen speciale uw PHP-code uit te voeren.
* Het publiceren en uw toepassing in Azure met Git opnieuw te publiceren.

Door deze zelfstudie te volgen, bouwt u een webtoepassing eenvoudig registratie in PHP. De toepassing zal worden gehost in een Azure-Website. Een schermopname van de voltooide toepassing lager is dan:

![Azure PHP-website](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a>Een Azure-web-app maken en Git-publicatie instellen
Volg deze stappen om een Azure-web-app en een SQL-Database te maken:

1. Meld u aan bij de [Azure Portal](https://portal.azure.com/).
2. Azure Marketplace openen door te klikken op de **nieuw** pictogram op de bovenste links van het dashboard, klikt u op **Alles selecteren** naast Marketplace en het selecteren van **Web en mobiel**.
3. Selecteer in de Marketplace **Web en mobiel**.
4. Klik op de **webtoepassing + SQL** pictogram.
5. Lees de beschrijving van de webtoepassing + SQL-app en selecteer **maken**.
6. Klik op elk onderdeel (**resourcegroep**, **Web-App**, **Database**, en **abonnement**) en typ of Selecteer waarden voor de vereiste velden :
   
   * Voer een URL-naam van uw keuze    
   * Referenties voor database-server configureren
   * Selecteer de regio die het dichtst bij u
     
     ![de app configureren](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. Wanneer u klaar bent met het definiëren van de web-app, klikt u op **maken**.
   
    Wanneer de web-app is gemaakt, de **meldingen** knop knippert een groene **geslaagd** en de resourcegroepblade openen om weer te geven van zowel de web-app en de SQL-database in de groep.
8. Klik op de web-app-pictogram in de resourcegroepblade om de web-app-blade te openen.
   
    ![Web-app van resourcegroep](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. In **instellingen** klikt u op **continue implementatie** > **vereiste instellingen configureren**. Selecteer **lokale Git-opslagplaats** en klik op **OK**.
   
    ![waar is de broncode](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    Als u een Git-opslagplaats voordat niet hebt ingesteld, moet u een gebruikersnaam en wachtwoord opgeven. Om dit te doen, klikt u op **instellingen** > **implementatiereferenties** in de web-app-blade.
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. In **instellingen** klikt u op **eigenschappen** om te zien van de externe Git-URL u gebruiken moet voor het implementeren van uw PHP-app hoger.

## <a name="get-sql-database-connection-information"></a>Gegevens van de SQL-Database-verbinding ophalen
Verbinding maken met de SQL-Database-exemplaar dat is gekoppeld aan uw web-app, uw wordt moet de verbindingsinformatie, die u hebt opgegeven toen u de database hebt gemaakt. Als u de verbindingsgegevens van de SQL-Database, de volgende stappen uit:

1. Klik op het pictogram van de SQL-database terug in de blade van de resourcegroep.
2. Klik op de SQL-database blade **instellingen** > **eigenschappen**, klikt u vervolgens op **databaseverbindingsreeksen tonen**. 
   
    ![Database-eigenschappen weergeven](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. Van de **PHP** sectie van het dialoogvenster wordt geopend, noteer de waarden voor `Server`, `SQL Database`, en `User Name`. U kunt deze waarden later worden gebruikt bij het publiceren van uw PHP-web-app in Azure App Service.

## <a name="build-and-test-your-application-locally"></a>De toepassing lokaal bouwen en testen
De registratie van toepassing is een eenvoudige PHP-toepassing waarmee u te registreren voor een gebeurtenis aan de hand van uw naam en e-mailadres. Informatie over eerdere geregistreerde wordt weergegeven in een tabel. Registratie-informatie wordt opgeslagen in een SQL Database-exemplaar. De toepassing bestaat uit twee bestanden (kopiëren en plakken code hieronder):

* **index.php**: een formulier voor registratie en een tabel met registrant informatie wordt weergegeven.
* **CreateTable.php**: de SQL-databasetabel voor de toepassing maakt. Dit bestand wordt slechts eenmaal worden gebruikt.

Als u wilt de toepassing lokaal uitvoert, de volgende stappen uit te voeren. Houd er rekening mee dat deze stappen wordt ervan uitgegaan dat u PHP en SQL Server Express instellen op uw lokale computer hebt en u hebt ingeschakeld de [PDO-extensie voor SQL Server][pdo-sqlsrv].

1. Maken van een SQL Server-database aangeroepen `registration`. U kunt dit doen vanuit de `sqlcmd` opdrachtprompt met de volgende opdrachten:
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. In de hoofdmap van uw toepassing maakt u twee bestanden in deze - een met de naam `createtable.php` en één aangeroepen `index.php`.
3. Open de `createtable.php` in een teksteditor of IDE-bestand en voeg de onderstaande code. Deze code wordt gebruikt voor het maken van de `registration_tbl` tabel de `registration` database.
   
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
   
    Houd er rekening mee dat moet u de waarden voor bijwerken <code>$user</code> en <code>$pwd</code> met uw lokale SQL Server-gebruikersnaam en wachtwoord.
4. Typ de volgende opdracht in een terminal in de hoofdmap van de toepassing:
   
        php -S localhost:8000
5. Open een webbrowser en blader naar **http://localhost:8000/createtable.php**. Hiermee maakt u de `registration_tbl` tabel in de database.
6. Open de **index.php** in een teksteditor of IDE-bestand en voeg de basic HTML en CSS-code voor de pagina (de PHP-code wordt toegevoegd in latere stappen).
   
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
7. Binnen de PHP-tags toevoegen PHP-code voor het verbinden met de database.
   
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
   
    Opnieuw, moet u de waarden voor bijwerken <code>$user</code> en <code>$pwd</code> met uw lokale MySQL-gebruikersnaam en wachtwoord.
8. Na de code van de database-verbinding, voeg code toe voor de registratiegegevens worden ingevoegd in de database.
   
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
9. Na de code, voeg de code voor het ophalen van gegevens uit de database.
   
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

Nu kunt u bladeren naar **http://localhost:8000/index.php** test de toepassing.

## <a name="publish-your-application"></a>Uw toepassing publiceren
Nadat u uw toepassing lokaal hebt getest, kunt u het publiceren naar App Service Web Apps met Git. Echter, moet u eerst de verbindingsgegevens voor de database in de toepassing bijwerken. Met de database-verbindingsgegevens die u eerder hebt verkregen (in de **verbindingsgegevens ophalen van de SQL-Database** sectie), werkt u de volgende gegevens in **beide** de `createdatabase.php` en `index.php` bestanden met de juiste waarden:

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> In de <code>$host</code>, de waarde van de Server moet worden voorafgegaan door <code>tcp:</code>.
> 
> 

U bent nu klaar Git-publicatie instellen en de toepassing te publiceren.

> [!NOTE]
> Dit zijn dezelfde stappen vermeld aan het einde van de **een Azure-web-app maken en Git-publicatie instellen** sectie hierboven.
> 
> 

1. Open GitBash (of een terminal als Git in uw `PATH`), wijzig de mappen in de hoofdmap van uw toepassing (de **registratie** directory), en voer de volgende opdrachten:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    U wordt gevraagd om het wachtwoord dat u eerder hebt gemaakt.
2. Blader naar **http://[web app name].azurewebsites.net/createtable.php** voor het maken van de tabel van de SQL-database voor de toepassing.
3. Blader naar **http://[web app name].azurewebsites.net/index.php** om te beginnen met behulp van de toepassing.

Nadat u uw toepassing hebt gepubliceerd, kunt u beginnen wijzigingen aanbrengen en Git gebruiken om te publiceren. 

## <a name="publish-changes-to-your-application"></a>Wijzigingen in uw toepassing publiceren
Om wijzigingen te publiceren naar de toepassing, de volgende stappen uit:

1. Wijzigingen aanbrengen in uw toepassing lokaal.
2. Open GitBash (of een terminal it Git is in uw `PATH`), wijzig de mappen in de hoofdmap van uw toepassing en voer de volgende opdrachten:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    U wordt gevraagd om het wachtwoord dat u eerder hebt gemaakt.
3. Blader naar **http://[web app name].azurewebsites.net/index.php** om uw wijzigingen te bekijken.

## <a name="whats-changed"></a>Wat is er gewijzigd
* Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

