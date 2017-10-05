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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a>Een PHP-MySQL-webtoepassing maken in Azure App Service en implementeren met Git
Deze zelfstudie ziet u hoe u een PHP-MySQL web-app maken en implementeren naar [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) met Git. U gaat gebruiken [PHP][install-php], de MySQL-opdrachtregelhulpprogramma (onderdeel van [MySQL][install-mysql]), en [Git] [ install-git] op uw computer geïnstalleerd. De instructies in deze zelfstudie kunnen worden uitgevoerd op elk besturingssysteem, met inbegrip van Windows, Mac en Linux. Bij voltooiing van deze handleiding hebt u een PHP/MySQL-web-app in Azure wordt uitgevoerd.

U leert:

* Het maken van een web-app en een MySQL-database met de [Azure Portal][management-portal]. Omdat PHP is ingeschakeld in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) standaard niets speciale is vereist voor het uitvoeren van uw PHP-code.
* Het publiceren en uw toepassing in Azure met Git opnieuw te publiceren.
* Het inschakelen van de Composer-extensie voor het automatiseren van Composer taken op elke `git push`.

Door deze zelfstudie te volgen, bouwt u een web-app voor eenvoudige registratie in PHP. De toepassing zal worden gehost in Web-Apps. Een schermopname van de voltooide toepassing lager is dan:

![Azure PHP-website][running-app]

## <a name="set-up-the-development-environment"></a>De ontwikkelomgeving instellen
Deze zelfstudie wordt ervan uitgegaan dat u hebt [PHP][install-php], de MySQL-opdrachtregelhulpprogramma (onderdeel van [MySQL][install-mysql]), en [Git] [ install-git] op uw computer geïnstalleerd.

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a>Een web-app maken en Git-publicatie instellen
Volg deze stappen om een web-app en een MySQL-database te maken:

1. Meld u aan bij de [Azure-Portal][management-portal].
2. Klik op de **nieuw** pictogram.
3. Klik op **alle Zie** naast **Marketplace**. 
4. Klik op **Web en mobiel**, klikt u vervolgens **webtoepassing + MySQL**. Klik vervolgens op **Maken**.
5. Voer een geldige naam voor de resourcegroep.
   
    ![Stel de naam van resourcegroep][resource-group]
6. Geef waarden voor uw nieuwe web-app.
   
    ![Een web-app maken][new-web-app]
7. Geef waarden voor de nieuwe database, inclusief akkoord gaat met de juridische voorwaarden.
   
    ![Nieuwe MySQL-database maken][new-mysql-db]
8. Wanneer de web-app is gemaakt, ziet u de blade van de nieuwe web-app.
9. In **instellingen** klikt u op **continue implementatie**, klikt u op *vereiste instellingen configureren*.
   
    ![Git-publicatie instellen][setup-publishing]
10. Selecteer **lokale Git-opslagplaats** voor de bron.
    
     ![Git-opslagplaats instellen][setup-repository]
11. U moet een gebruikersnaam en wachtwoord opgeven zodat Git-publicatie. Noteer de gebruikersnaam en wachtwoord die u maakt. (Als u een Git-opslagplaats voordat hebt ingesteld, wordt deze stap overgeslagen.)
    
     ![Publishing referenties maken][credentials]

## <a name="get-remote-mysql-connection-information"></a>Externe gegevens van MySQL-verbinding ophalen
Verbinding maken met de MySQL-database die wordt uitgevoerd in de Web-Apps, uw wordt moet de verbindingsinformatie. Als u de verbindingsgegevens MySQL, de volgende stappen uit:

1. Klik op de database van de resourcegroep:
   
    ![Database selecteren][select-database]
2. Uit de database **instellingen**, selecteer **eigenschappen**.
   
    ![Eigenschappen selecteren][select-properties]
3. Noteer de waarden voor `Database`, `Host`, `User Id`, en `Password`.
   
    ![Opmerking eigenschappen][note-properties]

## <a name="build-and-test-your-app-locally"></a>Bouwen en testen van uw app lokaal
Nu dat u een web-app hebt gemaakt, kunt u de toepassing lokaal ontwikkelen vervolgens implementeren nadat u hebt getest.

De registratie van toepassing is een eenvoudige PHP-toepassing waarmee u te registreren voor een gebeurtenis aan de hand van uw naam en e-mailadres. Informatie over eerdere geregistreerde wordt weergegeven in een tabel. Registratie-informatie wordt opgeslagen in een MySQL-database. De toepassing bestaat uit één bestand (kopiëren en plakken code hieronder):

* **index.php**: een formulier voor registratie en een tabel met registrant informatie wordt weergegeven.

Voor het bouwen en de toepassing lokaal uitvoeren, de volgende stappen uit te voeren. Houd er rekening mee dat deze stappen wordt ervan uitgegaan u hebt de PHP en de MySQL-opdrachtregelhulpprogramma (onderdeel van MySQL dat) instellen op uw lokale computer en die u hebt ingeschakeld de [PDO-extensie voor MySQL][pdo-mysql].

1. Verbinding maken met de externe MySQL-server, met de waarde voor `Data Source`, `User Id`, `Password`, en `Database` die u eerder hebt opgehaald:
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. De MySQL-opdrachtprompt wordt weergegeven:
   
        mysql>
3. Plakken in de volgende `CREATE TABLE` opdracht maken de `registration_tbl` tabel in de database:
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. Maak in de hoofdmap van uw lokale map application **index.php** bestand.
5. Open de **index.php** bestand in een teksteditor of IDE en voeg de volgende code en voer de benodigde wijzigingen gemarkeerd met `//TODO:` opmerkingen.

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

1. Ga naar de map van uw toepassing in een terminal en typ de volgende opdracht:
   
       php -S localhost:8000

Nu kunt u bladeren naar **http://localhost: 8000 /** test de toepassing.

## <a name="publish-your-app"></a>Uw app publiceren
Nadat u uw app lokaal hebt getest, kunt u het publiceren op Web-Apps met Git. U uw lokale Git-opslagplaats te initialiseren en publiceer de toepassing.

> [!NOTE]
> Dit zijn dezelfde stappen in de Azure-Portal aan het einde van het maken van een web-app en een Set up Git Publishing sectie hierboven.
> 
> 

1. (Optioneel)  Als u hebt vergeten of de URL van de externe repostitory Git foutief worden geplaatst, gaat u naar de eigenschappen van het web-app in de Azure Portal.
2. Open GitBash (of een terminal als Git in uw `PATH`), wijzig de mappen in de hoofdmap van uw toepassing en voer de volgende opdrachten:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    U wordt gevraagd om het wachtwoord dat u eerder hebt gemaakt.
   
    ![Initiële Push naar Azure via Git][git-initial-push]
3. Blader naar **http://[site name].azurewebsites.net/index.php** om te beginnen met behulp van de toepassing (deze informatie wordt opgeslagen op uw dashboard account):
   
    ![Azure PHP-website][running-app]

Nadat u uw app hebt gepubliceerd, kunt u beginnen wijzigingen aanbrengen en Git gebruiken om te publiceren.

## <a name="publish-changes-to-your-app"></a>Wijzigingen aan uw app publiceren
Als u wilt publiceren wijzigingen aan uw app, de volgende stappen uit:

1. Wijzigingen aanbrengen in uw app lokaal.
2. Open GitBash (of een terminal it Git is in uw `PATH`), wijzig de mappen in de hoofdmap van uw app en voer de volgende opdrachten:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    U wordt gevraagd om het wachtwoord dat u eerder hebt gemaakt.
   
    ![Sitewijzigingen pushen naar Azure via Git][git-change-push]
3. Blader naar **http://[site name].azurewebsites.net/index.php** om te zien van uw app en eventuele wijzigingen die u hebt gemaakt:
   
    ![Azure PHP-website][running-app]

> [!NOTE]
> Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-the-composer-extension"></a>Composer automatiseren met de Composer-extensie
Standaard biedt geen de git-implementatieproces in App Service niets doen met composer.json, als u in uw PHP-project hebt. U kunt inschakelen composer.json tijdens de verwerking `git push` doordat de Composer-extensie.

1. In uw PHP web-app blade in de [Azure-portal][management-portal], klikt u op **extra** > **extensies**.
   
    ![Composer-extensie-instellingen][composer-extension-settings]
2. Klik op **toevoegen**, klikt u vervolgens op **Composer**.
   
    ![Composer-extensie toevoegen][composer-extension-add]
3. Klik op **OK** juridische voorwaarden accepteren. Klik op **OK** om opnieuw toe te voegen van de extensie.
   
    De **extensies geïnstalleerd** blade ziet nu de Composer-extensie.  
    ![Composer-extensie weergeven][composer-extension-view]
4. Nu uitvoeren `git add`, `git commit`, en `git push` zoals in de vorige sectie. Nu ziet u dat Composer afhankelijkheden die zijn gedefinieerd in composer.json wordt geïnstalleerd.
   
    ![Composer-extensie geslaagd][composer-extension-success]

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie de [PHP-ontwikkelaarscentrum](/develop/php/).

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
