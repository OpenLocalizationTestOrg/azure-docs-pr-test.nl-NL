---
title: een PHP-MySQL aaaCreate web-app in Azure App Service en implementeren met Git
description: Een zelfstudie die u laat zien hoe toocreate een PHP web-app die gegevens in MySQL opslaat en Git-implementatie tooAzure te gebruiken.
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
ms.openlocfilehash: 9c22946777598cc973cd9dfc8d2a258bd08cc39a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a><span data-ttu-id="dc470-103">Een PHP-MySQL-webtoepassing maken in Azure App Service en implementeren met Git</span><span class="sxs-lookup"><span data-stu-id="dc470-103">Create a PHP-MySQL web app in Azure App Service and deploy using Git</span></span>
<span data-ttu-id="dc470-104">Deze zelfstudie leert u hoe u een PHP-MySQL toocreate web-app en hoe toodeploy deze te[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) met Git.</span><span class="sxs-lookup"><span data-stu-id="dc470-104">This tutorial shows you how toocreate a PHP-MySQL web app and how toodeploy it too[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) using Git.</span></span> <span data-ttu-id="dc470-105">U gaat gebruiken [PHP][install-php], MySQL opdrachtregelhulpprogramma Hallo (onderdeel van [MySQL][install-mysql]), en [Git] [ install-git] op uw computer geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="dc470-105">You will use [PHP][install-php], hello MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="dc470-106">Hallo-instructies in deze zelfstudie kunnen worden uitgevoerd op elk besturingssysteem, met inbegrip van Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="dc470-106">hello instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="dc470-107">Bij voltooiing van deze handleiding hebt u een PHP/MySQL-web-app in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="dc470-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="dc470-108">U leert:</span><span class="sxs-lookup"><span data-stu-id="dc470-108">You will learn:</span></span>

* <span data-ttu-id="dc470-109">Hoe toocreate een web-app en een MySQL-database met behulp van Hallo [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="dc470-109">How toocreate a web app and a MySQL database using hello [Azure Portal][management-portal].</span></span> <span data-ttu-id="dc470-110">Omdat PHP is ingeschakeld in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) standaard niets speciale vereist toorun is uw PHP-code.</span><span class="sxs-lookup"><span data-stu-id="dc470-110">Because PHP is enabled in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="dc470-111">Hoe toopublish en uw toepassing tooAzure met Git opnieuw te publiceren.</span><span class="sxs-lookup"><span data-stu-id="dc470-111">How toopublish and re-publish your application tooAzure using Git.</span></span>
* <span data-ttu-id="dc470-112">Hoe tooenable Hallo Composer-extensie tooautomate Composer taken op elke `git push`.</span><span class="sxs-lookup"><span data-stu-id="dc470-112">How tooenable hello Composer extension tooautomate Composer tasks at every `git push`.</span></span>

<span data-ttu-id="dc470-113">Door deze zelfstudie te volgen, bouwt u een web-app voor eenvoudige registratie in PHP.</span><span class="sxs-lookup"><span data-stu-id="dc470-113">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="dc470-114">Hallo-toepassing wordt gehost in Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="dc470-114">hello application will be hosted in Web Apps.</span></span> <span data-ttu-id="dc470-115">Een schermopname van de toepassing hello voltooid lager is dan:</span><span class="sxs-lookup"><span data-stu-id="dc470-115">A screenshot of hello completed application is below:</span></span>

![Azure PHP-website][running-app]

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="dc470-117">Hallo-ontwikkelomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="dc470-117">Set up hello development environment</span></span>
<span data-ttu-id="dc470-118">Deze zelfstudie wordt ervan uitgegaan dat u hebt [PHP][install-php], MySQL opdrachtregelhulpprogramma Hallo (onderdeel van [MySQL][install-mysql]), en [Git] [ install-git] op uw computer geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="dc470-118">This tutorial assumes you have [PHP][install-php], hello MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span>

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a><span data-ttu-id="dc470-119">Een web-app maken en Git-publicatie instellen</span><span class="sxs-lookup"><span data-stu-id="dc470-119">Create a web app and set up Git publishing</span></span>
<span data-ttu-id="dc470-120">Volg deze stappen toocreate een web-app en een MySQL-database:</span><span class="sxs-lookup"><span data-stu-id="dc470-120">Follow these steps toocreate a web app and a MySQL database:</span></span>

1. <span data-ttu-id="dc470-121">Aanmelding toohello [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="dc470-121">Login toohello [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="dc470-122">Klik op Hallo **nieuw** pictogram.</span><span class="sxs-lookup"><span data-stu-id="dc470-122">Click hello **New** icon.</span></span>
3. <span data-ttu-id="dc470-123">Klik op **alle Zie** volgende te**Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="dc470-123">Click **See All** next too**Marketplace**.</span></span> 
4. <span data-ttu-id="dc470-124">Klik op **Web en mobiel**, klikt u vervolgens **webtoepassing + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="dc470-124">Click **Web + Mobile**, then **Web app + MySQL**.</span></span> <span data-ttu-id="dc470-125">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="dc470-125">Then, click **Create**.</span></span>
5. <span data-ttu-id="dc470-126">Voer een geldige naam voor de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="dc470-126">Enter a valid name for your resource group.</span></span>
   
    ![Stel de naam van resourcegroep][resource-group]
6. <span data-ttu-id="dc470-128">Geef waarden voor uw nieuwe web-app.</span><span class="sxs-lookup"><span data-stu-id="dc470-128">Enter values for your new web app.</span></span>
   
    ![Een web-app maken][new-web-app]
7. <span data-ttu-id="dc470-130">Voer waarden in voor de nieuwe database, inclusief ermee akkoord toohello juridische voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="dc470-130">Enter values for your new database, including agreeing toohello legal terms.</span></span>
   
    ![Nieuwe MySQL-database maken][new-mysql-db]
8. <span data-ttu-id="dc470-132">Als het Hallo-web-app is gemaakt, ziet u Hallo nieuwe blade web-app.</span><span class="sxs-lookup"><span data-stu-id="dc470-132">When hello web app has been created, you will see hello new web app blade.</span></span>
9. <span data-ttu-id="dc470-133">In **instellingen** klikt u op **continue implementatie**, klikt u op *vereiste instellingen configureren*.</span><span class="sxs-lookup"><span data-stu-id="dc470-133">In **Settings** click on **Continuous Deployment**, then click on *Configure required settings*.</span></span>
   
    ![Git-publicatie instellen][setup-publishing]
10. <span data-ttu-id="dc470-135">Selecteer **lokale Git-opslagplaats** voor Hallo bron.</span><span class="sxs-lookup"><span data-stu-id="dc470-135">Select **Local Git Repository** for hello source.</span></span>
    
     ![Git-opslagplaats instellen][setup-repository]
11. <span data-ttu-id="dc470-137">tooenable Git publiceren, moet u opgeven een gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="dc470-137">tooenable Git publishing, you must provide a user name and password.</span></span> <span data-ttu-id="dc470-138">Maak een notitie van Hallo-gebruikersnaam en wachtwoord die u maakt.</span><span class="sxs-lookup"><span data-stu-id="dc470-138">Make a note of hello user name and password you create.</span></span> <span data-ttu-id="dc470-139">(Als u een Git-opslagplaats voordat hebt ingesteld, wordt deze stap overgeslagen.)</span><span class="sxs-lookup"><span data-stu-id="dc470-139">(If you have set up a Git repository before, this step will be skipped.)</span></span>
    
     ![Publishing referenties maken][credentials]

## <a name="get-remote-mysql-connection-information"></a><span data-ttu-id="dc470-141">Externe gegevens van MySQL-verbinding ophalen</span><span class="sxs-lookup"><span data-stu-id="dc470-141">Get remote MySQL connection information</span></span>
<span data-ttu-id="dc470-142">tooconnect toohello MySQL-database die wordt uitgevoerd in de Web-Apps, uw wordt moet Hallo verbindingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="dc470-142">tooconnect toohello MySQL database that is running in Web Apps, your will need hello connection information.</span></span> <span data-ttu-id="dc470-143">tooget verbindingsinformatie MySQL, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="dc470-143">tooget MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="dc470-144">Klik op Hallo-database van de resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="dc470-144">From your resource group, click hello database:</span></span>
   
    ![Database selecteren][select-database]
2. <span data-ttu-id="dc470-146">Uit de database Hallo **instellingen**, selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="dc470-146">From hello database **Settings**, select **Properties**.</span></span>
   
    ![Eigenschappen selecteren][select-properties]
3. <span data-ttu-id="dc470-148">Noteer Hallo waarden voor `Database`, `Host`, `User Id`, en `Password`.</span><span class="sxs-lookup"><span data-stu-id="dc470-148">Make note of hello values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Opmerking eigenschappen][note-properties]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="dc470-150">Bouwen en testen van uw app lokaal</span><span class="sxs-lookup"><span data-stu-id="dc470-150">Build and test your app locally</span></span>
<span data-ttu-id="dc470-151">Nu dat u een web-app hebt gemaakt, kunt u de toepassing lokaal ontwikkelen vervolgens implementeren nadat u hebt getest.</span><span class="sxs-lookup"><span data-stu-id="dc470-151">Now that you have created a web app, you can develop your application locally, then deploy it after testing.</span></span>

<span data-ttu-id="dc470-152">Hallo registratie van toepassing is een eenvoudige PHP-toepassing waarmee u tooregister voor een gebeurtenis aan de hand van uw naam en e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="dc470-152">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="dc470-153">Informatie over eerdere geregistreerde wordt weergegeven in een tabel.</span><span class="sxs-lookup"><span data-stu-id="dc470-153">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="dc470-154">Registratie-informatie wordt opgeslagen in een MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="dc470-154">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="dc470-155">Hallo toepassing bestaat uit één bestand (kopiëren en plakken code hieronder):</span><span class="sxs-lookup"><span data-stu-id="dc470-155">hello application consists of one file (copy/paste code available below):</span></span>

* <span data-ttu-id="dc470-156">**index.php**: een formulier voor registratie en een tabel met registrant informatie wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="dc470-156">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>

<span data-ttu-id="dc470-157">toobuild en Voer Hallo toepassing lokaal door stappen Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="dc470-157">toobuild and run hello application locally, follow hello steps below.</span></span> <span data-ttu-id="dc470-158">Houd er rekening mee dat deze stappen wordt ervan uitgegaan dat u hebt Hallo PHP en MySQL-opdrachtregelhulpprogramma (onderdeel van MySQL) instellen op uw lokale computer en dat u Hallo hebt ingeschakeld [PDO-extensie voor MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="dc470-158">Note that these steps assume you have hello PHP and MySQL Command-Line Tool (part of MySQL) set up on your local machine, and that you have enabled hello [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="dc470-159">Verbinding maken met toohello externe MySQL-server, met Hallo-waarde voor `Data Source`, `User Id`, `Password`, en `Database` die u eerder hebt opgehaald:</span><span class="sxs-lookup"><span data-stu-id="dc470-159">Connect toohello remote MySQL server, using hello value for `Data Source`, `User Id`, `Password`, and `Database` that you retrieved earlier:</span></span>
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. <span data-ttu-id="dc470-160">Hallo MySQL-opdrachtprompt wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="dc470-160">hello MySQL command prompt will appear:</span></span>
   
        mysql>
3. <span data-ttu-id="dc470-161">Plakken in de volgende Hallo `CREATE TABLE` opdracht toocreate hello `registration_tbl` tabel in de database:</span><span class="sxs-lookup"><span data-stu-id="dc470-161">Paste in hello following `CREATE TABLE` command toocreate hello `registration_tbl` table in your database:</span></span>
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. <span data-ttu-id="dc470-162">In de hoofdmap van uw map voor lokale toepassing hello maken **index.php** bestand.</span><span class="sxs-lookup"><span data-stu-id="dc470-162">In hello root of your local application folder create **index.php** file.</span></span>
5. <span data-ttu-id="dc470-163">Open Hallo **index.php** bestand in een teksteditor of IDE en toevoegen van Hallo van de volgende code en volledige Hallo noodzakelijke wijzigingen die zijn gemarkeerd met `//TODO:` opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="dc470-163">Open hello **index.php** file in a text editor or IDE and add hello following code, and complete hello necessary changes marked with `//TODO:` comments.</span></span>

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
            // DB connection info
            //TODO: Update hello values for $host, $user, $pwd, and $db
            //using hello values you retrieved earlier from hello Azure Portal.
            $host = "value of Data Source";
            $user = "value of User Id";
            $pwd = "value of Password";
            $db = "value of Database";
            // Connect toodatabase.
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

1. <span data-ttu-id="dc470-164">In een terminal Ga tooyour toepassing map en het type Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="dc470-164">In a terminal go tooyour application folder and type hello following command:</span></span>
   
       php -S localhost:8000

<span data-ttu-id="dc470-165">U kunt nu te bladeren**http://localhost: 8000 /** tootest Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="dc470-165">You can now browse too**http://localhost:8000/** tootest hello application.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="dc470-166">Uw app publiceren</span><span class="sxs-lookup"><span data-stu-id="dc470-166">Publish your app</span></span>
<span data-ttu-id="dc470-167">Nadat u uw app lokaal hebt getest, kunt u deze tooWeb Apps met Git publiceren.</span><span class="sxs-lookup"><span data-stu-id="dc470-167">After you have tested your app locally, you can publish it tooWeb Apps using Git.</span></span> <span data-ttu-id="dc470-168">U uw lokale Git-opslagplaats te initialiseren en Hallo toepassing publiceren.</span><span class="sxs-lookup"><span data-stu-id="dc470-168">You will initialize your local Git repository and publish hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="dc470-169">Dit zijn dezelfde Hallo stappen in hello Azure-Portal aan einde Hallo Hallo maken een web-app en Set up Git Publishing sectie hierboven.</span><span class="sxs-lookup"><span data-stu-id="dc470-169">These are hello same steps shown in hello Azure Portal at hello end of hello Create a web app and Set up Git Publishing section above.</span></span>
> 
> 

1. <span data-ttu-id="dc470-170">(Optioneel)  Als u hebt vergeten of de URL van de externe repostitory Git foutief worden geplaatst, navigeer toohello web app-eigenschappen op Hallo Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="dc470-170">(Optional)  If you've forgotten or misplaced your Git remote repostitory URL, navigate toohello web app properties on hello Azure Portal.</span></span>
2. <span data-ttu-id="dc470-171">Open GitBash (of een terminal als Git in uw `PATH`), mappen toohello hoofdmap van uw toepassing te wijzigen en uitvoeren van Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="dc470-171">Open GitBash (or a terminal, if Git is in your `PATH`), change directories toohello root directory of your application, and run hello following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="dc470-172">U wordt gevraagd om Hallo wachtwoord die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="dc470-172">You will be prompted for hello password you created earlier.</span></span>
   
    ![Initiële Push tooAzure via Git][git-initial-push]
3. <span data-ttu-id="dc470-174">Te bladeren**http://[site name].azurewebsites.net/index.php** toobegin met Hallo-toepassing (deze informatie wordt opgeslagen op uw dashboard account):</span><span class="sxs-lookup"><span data-stu-id="dc470-174">Browse too**http://[site name].azurewebsites.net/index.php** toobegin using hello application (this information will be stored on your account dashboard):</span></span>
   
    ![Azure PHP-website][running-app]

<span data-ttu-id="dc470-176">Nadat u uw app hebt gepubliceerd, kunt u beginnen met het maken van wijzigingen tooit en Git toopublish gebruiken ze.</span><span class="sxs-lookup"><span data-stu-id="dc470-176">After you have published your app, you can begin making changes tooit and use Git toopublish them.</span></span>

## <a name="publish-changes-tooyour-app"></a><span data-ttu-id="dc470-177">Wijzigingen tooyour app publiceren</span><span class="sxs-lookup"><span data-stu-id="dc470-177">Publish changes tooyour app</span></span>
<span data-ttu-id="dc470-178">toopublish wijzigingen tooyour app als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="dc470-178">toopublish changes tooyour app, follow these steps:</span></span>

1. <span data-ttu-id="dc470-179">Controleer de wijzigingen tooyour app lokaal.</span><span class="sxs-lookup"><span data-stu-id="dc470-179">Make changes tooyour app locally.</span></span>
2. <span data-ttu-id="dc470-180">Open GitBash (of een terminal it Git is in uw `PATH`), mappen toohello hoofdmap van uw app wijzigen en uitvoeren van Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="dc470-180">Open GitBash (or a terminal, it Git is in your `PATH`), change directories toohello root directory of your app, and run hello following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="dc470-181">U wordt gevraagd om Hallo wachtwoord die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="dc470-181">You will be prompted for hello password you created earlier.</span></span>
   
    ![TooAzure via Git pushen site wordt gewijzigd][git-change-push]
3. <span data-ttu-id="dc470-183">Te bladeren**http://[site name].azurewebsites.net/index.php** toosee uw app en eventuele wijzigingen die u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="dc470-183">Browse too**http://[site name].azurewebsites.net/index.php** toosee your app and any changes you may have made:</span></span>
   
    ![Azure PHP-website][running-app]

> [!NOTE]
> <span data-ttu-id="dc470-185">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="dc470-185">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="dc470-186">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="dc470-186">No credit cards required; no commitments.</span></span>
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-hello-composer-extension"></a><span data-ttu-id="dc470-187">Composer automation Hello Composer-extensie inschakelen</span><span class="sxs-lookup"><span data-stu-id="dc470-187">Enable Composer automation with hello Composer extension</span></span>
<span data-ttu-id="dc470-188">Standaard geen Hallo git-implementatieproces in App Service reactie met composer.json, als u in uw PHP-project hebt.</span><span class="sxs-lookup"><span data-stu-id="dc470-188">By default, hello git deployment process in App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="dc470-189">U kunt inschakelen composer.json tijdens de verwerking `git push` doordat Hallo Composer-extensie.</span><span class="sxs-lookup"><span data-stu-id="dc470-189">You can enable composer.json processing during `git push` by enabling hello Composer extension.</span></span>

1. <span data-ttu-id="dc470-190">In uw PHP web-app blade in Hallo [Azure-portal][management-portal], klikt u op **extra** > **extensies**.</span><span class="sxs-lookup"><span data-stu-id="dc470-190">In your PHP web app's blade in hello [Azure portal][management-portal], click **Tools** > **Extensions**.</span></span>
   
    ![Composer-extensie-instellingen][composer-extension-settings]
2. <span data-ttu-id="dc470-192">Klik op **toevoegen**, klikt u vervolgens op **Composer**.</span><span class="sxs-lookup"><span data-stu-id="dc470-192">Click **Add**, then click **Composer**.</span></span>
   
    ![Composer-extensie toevoegen][composer-extension-add]
3. <span data-ttu-id="dc470-194">Klik op **OK** tooaccept juridische voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="dc470-194">Click **OK** tooaccept legal terms.</span></span> <span data-ttu-id="dc470-195">Klik op **OK** opnieuw tooadd Hallo-extensie.</span><span class="sxs-lookup"><span data-stu-id="dc470-195">Click **OK** again tooadd hello extension.</span></span>
   
    <span data-ttu-id="dc470-196">Hallo **extensies geïnstalleerd** blade ziet nu Hallo Composer-extensie.</span><span class="sxs-lookup"><span data-stu-id="dc470-196">hello **Installed extensions** blade will now show hello Composer extension.</span></span>  
    <span data-ttu-id="dc470-197">![Composer-extensie weergeven][composer-extension-view]</span><span class="sxs-lookup"><span data-stu-id="dc470-197">![Composer Extension View][composer-extension-view]</span></span>
4. <span data-ttu-id="dc470-198">Nu uitvoeren `git add`, `git commit`, en `git push` zoals in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc470-198">Now, perform `git add`, `git commit`, and `git push` like in hello previous section.</span></span> <span data-ttu-id="dc470-199">Nu ziet u dat Composer afhankelijkheden die zijn gedefinieerd in composer.json wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="dc470-199">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Composer-extensie geslaagd][composer-extension-success]

## <a name="next-steps"></a><span data-ttu-id="dc470-201">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dc470-201">Next steps</span></span>
<span data-ttu-id="dc470-202">Zie voor meer informatie, Hallo [PHP-ontwikkelaarscentrum](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="dc470-202">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

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
