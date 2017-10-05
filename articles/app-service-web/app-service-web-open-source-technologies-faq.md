---
title: "Open source-technologieën Veelgestelde vragen over Azure web-apps | Microsoft Docs"
description: "Vind antwoorden op veelgestelde vragen over open source-technologieën in de functie Web Apps van Azure App Service."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: d37b53242c0b231d83425a59ecbe50216216a95b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a><span data-ttu-id="125c3-103">Open source-technologieën Veelgestelde vragen voor Web-Apps in Azure</span><span class="sxs-lookup"><span data-stu-id="125c3-103">Open-source technologies FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="125c3-104">In dit artikel bevat de antwoorden op veelgestelde vragen (FAQ's) over problemen met technologieën voor open-source de [functie van Azure App Service Web Apps](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="125c3-104">This article has answers to frequently asked questions (FAQs) about issues with open-source technologies for the [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a><span data-ttu-id="125c3-105">Mijn ClearDB-database is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="125c3-105">My ClearDB database is down.</span></span> <span data-ttu-id="125c3-106">Hoe kan ik dit oplossen?</span><span class="sxs-lookup"><span data-stu-id="125c3-106">How do I resolve this?</span></span>

<span data-ttu-id="125c3-107">Problemen met database contact op met [ClearDB ondersteuning](https://www.cleardb.com/developers/help/support).</span><span class="sxs-lookup"><span data-stu-id="125c3-107">For database-related issues, contact [ClearDB support](https://www.cleardb.com/developers/help/support).</span></span> 

<span data-ttu-id="125c3-108">Zie voor antwoorden op veelgestelde vragen over ClearDB [ClearDB Veelgestelde vragen over](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="125c3-108">For answers to common questions about ClearDB, see [ClearDB FAQs](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-isnt-my-cleardb-database-listed-in-the-portal"></a><span data-ttu-id="125c3-109">Waarom wordt mijn ClearDB-database niet vermeld in de portal</span><span class="sxs-lookup"><span data-stu-id="125c3-109">Why isn't my ClearDB database listed in the portal?</span></span>

<span data-ttu-id="125c3-110">Als u maakt een ClearDB-database in de [Azure-portal](http://portal.azure.com/), de database wordt niet weergegeven in de [klassieke Azure-portal](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="125c3-110">If you create a ClearDB database in the [Azure portal](http://portal.azure.com/), the database doesn't appear in the [Azure classic portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="125c3-111">Om dit te voorkomen, kunt u de database handmatig koppelen aan de web-app.</span><span class="sxs-lookup"><span data-stu-id="125c3-111">To work around this, you can manually link your database to the web app.</span></span>

<span data-ttu-id="125c3-112">Op dezelfde manier als u maakt een ClearDB-database in de [klassieke Azure-portal](http://manage.windowsazure.com/), ziet u niet de database in de [Azure-portal](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="125c3-112">Similarly, if you create a ClearDB database in the [Azure classic portal](http://manage.windowsazure.com/),  you won't see your database in the [Azure portal](http://portal.azure.com/).</span></span> <span data-ttu-id="125c3-113">In dit geval is geen oplossing beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="125c3-113">In this case, no workaround is available.</span></span> 

<span data-ttu-id="125c3-114">Zie voor meer informatie [Veelgestelde vragen over ClearDB MySQL-databases met Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="125c3-114">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a><span data-ttu-id="125c3-115">Waarom worden mijn ClearDB-database, is niet gemigreerd tijdens de abonnementmigratie van mijn?</span><span class="sxs-lookup"><span data-stu-id="125c3-115">Why wasn't my ClearDB database migrated during my subscription migration?</span></span>

<span data-ttu-id="125c3-116">Wanneer u Resourcemigratie voor abonnementen uitvoert, zijn enkele beperkingen van toepassing.</span><span class="sxs-lookup"><span data-stu-id="125c3-116">When you perform resource migration across subscriptions, some limitations apply.</span></span> <span data-ttu-id="125c3-117">Een ClearDB MySQL-database is een service van derden en wordt tijdens de migratie van een Azure-abonnement niet gemigreerd.</span><span class="sxs-lookup"><span data-stu-id="125c3-117">A ClearDB MySQL database is a third-party service and is not migrated during an Azure subscription migration.</span></span>

<span data-ttu-id="125c3-118">Als u niet de migratie van uw MySQL-database beheert voordat u uw Azure-resources migreert, is het mogelijk dat uw ClearDB MySQL-database niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="125c3-118">If you don't manage the migration of your MySQL database before you migrate your Azure resources, your ClearDB MySQL database might be unavailable.</span></span> <span data-ttu-id="125c3-119">Om dit te voorkomen, eerst handmatig migreren uw ClearDB-database, en vervolgens migreren de Azure-abonnement voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="125c3-119">To avoid this, first, manually migrate your ClearDB database, and then migrate the Azure subscription for your web app.</span></span>

<span data-ttu-id="125c3-120">Zie voor meer informatie [Veelgestelde vragen over ClearDB MySQL-databases met Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="125c3-120">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="how-do-i-turn-on-php-logging-to-troubleshoot-php-issues"></a><span data-ttu-id="125c3-121">Hoe kan ik PHP logboekregistratie voor het oplossen van problemen voor PHP inschakelen?</span><span class="sxs-lookup"><span data-stu-id="125c3-121">How do I turn on PHP logging to troubleshoot PHP issues?</span></span>

<span data-ttu-id="125c3-122">PHP-logboekregistratie inschakelen:</span><span class="sxs-lookup"><span data-stu-id="125c3-122">To turn on PHP logging:</span></span>

1. <span data-ttu-id="125c3-123">Aanmelden bij uw [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="125c3-123">Sign in to your [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="125c3-124">Selecteer in het bovenste menu **Console voor foutopsporing** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="125c3-124">In the top menu, select **Debug Console** > **CMD**.</span></span>
3. <span data-ttu-id="125c3-125">Selecteer de **Site** map.</span><span class="sxs-lookup"><span data-stu-id="125c3-125">Select the **Site** folder.</span></span>
4. <span data-ttu-id="125c3-126">Selecteer de **wwwroot** map.</span><span class="sxs-lookup"><span data-stu-id="125c3-126">Select the **wwwroot** folder.</span></span>
5. <span data-ttu-id="125c3-127">Selecteer de  **+**  pictogram en selecteer vervolgens **nieuw bestand**.</span><span class="sxs-lookup"><span data-stu-id="125c3-127">Select the **+** icon, and then select **New File**.</span></span>
6. <span data-ttu-id="125c3-128">De bestandsnaam ingesteld op **. user.ini**.</span><span class="sxs-lookup"><span data-stu-id="125c3-128">Set the file name to **.user.ini**.</span></span>
7. <span data-ttu-id="125c3-129">Schakel het potloodpictogram naast **. user.ini**.</span><span class="sxs-lookup"><span data-stu-id="125c3-129">Select the pencil icon next to **.user.ini**.</span></span>
8. <span data-ttu-id="125c3-130">Voeg deze code in het bestand:`log_errors=on`</span><span class="sxs-lookup"><span data-stu-id="125c3-130">In the file, add this code: `log_errors=on`</span></span>
9. <span data-ttu-id="125c3-131">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="125c3-131">Select **Save**.</span></span>
10. <span data-ttu-id="125c3-132">Schakel het potloodpictogram naast **wp-config.php**.</span><span class="sxs-lookup"><span data-stu-id="125c3-132">Select the pencil icon next to **wp-config.php**.</span></span>
11. <span data-ttu-id="125c3-133">Wijzig de tekst in de volgende code:</span><span class="sxs-lookup"><span data-stu-id="125c3-133">Change the text to the following code:</span></span>
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging to /wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings to screendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors to screenini_set('display_errors', 0);
   ```
12. <span data-ttu-id="125c3-134">Start opnieuw op uw web-app in de Azure portal, in het webmenu-app.</span><span class="sxs-lookup"><span data-stu-id="125c3-134">In the Azure portal, in the web app menu, restart your web app.</span></span>

<span data-ttu-id="125c3-135">Zie voor meer informatie [inschakelen WordPress foutenlogboeken](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span><span class="sxs-lookup"><span data-stu-id="125c3-135">For more information, see [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a><span data-ttu-id="125c3-136">Hoe meld ik toepassingsfouten in Python in apps die worden gehost in App Service</span><span class="sxs-lookup"><span data-stu-id="125c3-136">How do I log Python application errors in apps that are hosted in App Service?</span></span>

<span data-ttu-id="125c3-137">Voor het vastleggen van toepassingsfouten in Python:</span><span class="sxs-lookup"><span data-stu-id="125c3-137">To capture Python application errors:</span></span>

1. <span data-ttu-id="125c3-138">Selecteer in de Azure-portal in uw web-app **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="125c3-138">In the Azure portal, in your web app, select **Settings**.</span></span>
2. <span data-ttu-id="125c3-139">Op de **instellingen** tabblad **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="125c3-139">On the **Settings** tab, select **Application settings**.</span></span>
3. <span data-ttu-id="125c3-140">Onder **appinstellingen**, voer de volgende sleutel-waardepaar:</span><span class="sxs-lookup"><span data-stu-id="125c3-140">Under **App settings**, enter the following key/value pair:</span></span>
    * <span data-ttu-id="125c3-141">Sleutel: WSGI_LOG</span><span class="sxs-lookup"><span data-stu-id="125c3-141">Key : WSGI_LOG</span></span>
    * <span data-ttu-id="125c3-142">Waarde: D:\home\site\wwwroot\logs.txt (uw keuze van bestandsnaam invoeren)</span><span class="sxs-lookup"><span data-stu-id="125c3-142">Value : D:\home\site\wwwroot\logs.txt (enter your choice of file name)</span></span>

<span data-ttu-id="125c3-143">U ziet nu de fouten in het bestand logs.txt in de wwwroot-map.</span><span class="sxs-lookup"><span data-stu-id="125c3-143">You should now see errors in the logs.txt file in the wwwroot folder.</span></span>

## <a name="how-do-i-change-the-version-of-the-nodejs-application-that-is-hosted-in-app-service"></a><span data-ttu-id="125c3-144">Hoe wijzig ik de versie van de Node.js-toepassing die wordt gehost in App Service?</span><span class="sxs-lookup"><span data-stu-id="125c3-144">How do I change the version of the Node.js application that is hosted in App Service?</span></span>

<span data-ttu-id="125c3-145">Als u wilt de versie van de Node.js-toepassing wijzigen, kunt u een van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="125c3-145">To change the version of the Node.js application, you can use one of the following options:</span></span>

*   <span data-ttu-id="125c3-146">In de Azure portal gebruiken **appinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="125c3-146">In the Azure portal, use **App settings**.</span></span>
    1. <span data-ttu-id="125c3-147">Ga naar uw web-app in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="125c3-147">In the Azure portal, go to your web app.</span></span>
    2. <span data-ttu-id="125c3-148">Op de **instellingen** blade Selecteer **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="125c3-148">On the **Settings** blade, select **Application settings**.</span></span>
    3. <span data-ttu-id="125c3-149">In **appinstellingen**, kunt u WEBSITE_NODE_DEFAULT_VERSION opnemen als de sleutel en de versie van Node.js die u wilt gebruiken als de waarde.</span><span class="sxs-lookup"><span data-stu-id="125c3-149">In **App settings**, you can include WEBSITE_NODE_DEFAULT_VERSION as the key, and the version of Node.js you want as the value.</span></span>
    4. <span data-ttu-id="125c3-150">Ga naar uw [Kudu-console](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="125c3-150">Go to your [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
    5. <span data-ttu-id="125c3-151">Als u wilt controleren de Node.js-versie, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="125c3-151">To check the Node.js version, enter the following command:</span></span>  
   ```
   node -v
   ```
*   <span data-ttu-id="125c3-152">Het bestand iisnode.yml wijzigen.</span><span class="sxs-lookup"><span data-stu-id="125c3-152">Modify the iisnode.yml file.</span></span> <span data-ttu-id="125c3-153">Het wijzigen van de Node.js-versie in het bestand iisnode.yml alleen Hiermee stelt u de runtime-omgeving waarnaar iisnode gebruikt.</span><span class="sxs-lookup"><span data-stu-id="125c3-153">Changing the Node.js version in the iisnode.yml file only sets the runtime environment that iisnode uses.</span></span> <span data-ttu-id="125c3-154">Uw cmd Kudu en andere nog steeds gebruik van de Node.js-versie die is ingesteld in **appinstellingen** in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="125c3-154">Your Kudu cmd and others still use the Node.js version that is set in **App settings** in the Azure portal.</span></span>

    <span data-ttu-id="125c3-155">De iisnode.yml als handmatig wilt instellen, door een bestand iisnode.yml in de hoofdmap van uw app te maken.</span><span class="sxs-lookup"><span data-stu-id="125c3-155">To set the iisnode.yml manually, create an iisnode.yml file in your app root folder.</span></span> <span data-ttu-id="125c3-156">In het bestand zijn onder andere de volgende regel:</span><span class="sxs-lookup"><span data-stu-id="125c3-156">In the file, include the following line:</span></span>
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   <span data-ttu-id="125c3-157">Het bestand iisnode.yml instellen met behulp van package.json tijdens de implementatie van de bron-besturingselement.</span><span class="sxs-lookup"><span data-stu-id="125c3-157">Set the iisnode.yml file by using package.json during source control deployment.</span></span>
    <span data-ttu-id="125c3-158">Het implementatieproces voor beheer van Azure bron omvat de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="125c3-158">The Azure source control deployment process involves the following steps:</span></span>
    1. <span data-ttu-id="125c3-159">Hiermee verplaatst u inhoud naar de Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="125c3-159">Moves content to the Azure web app.</span></span>
    2. <span data-ttu-id="125c3-160">Als er niet (deploy.cmd, .deployment-bestanden) in de hoofdmap van de web-app is, maakt een standaard implementatiescript.</span><span class="sxs-lookup"><span data-stu-id="125c3-160">Creates a default deployment script, if there isn’t one (deploy.cmd, .deployment files) in the web app root folder.</span></span>
    3. <span data-ttu-id="125c3-161">Wordt uitgevoerd een implementatiescript waarin deze een iisnode.yml bestand maakt als u de Node.js-versie in het bestand package.json vermeld > engine`"engines": {"node": "5.9.1","npm": "3.7.3"}`</span><span class="sxs-lookup"><span data-stu-id="125c3-161">Runs a deployment script in which it creates an iisnode.yml file if you mention the Node.js version in the package.json file > engine `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span></span>
    4. <span data-ttu-id="125c3-162">Het bestand iisnode.yml heeft de volgende regel code:</span><span class="sxs-lookup"><span data-stu-id="125c3-162">The iisnode.yml file has the following line of code:</span></span>
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-the-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a><span data-ttu-id="125c3-163">Verschijnt het bericht 'Fout bij het maken van een databaseverbinding ' in mijn WordPress-app die wordt gehost in App Service.</span><span class="sxs-lookup"><span data-stu-id="125c3-163">I see the message "Error establishing a database connection" in my WordPress app that's hosted in App Service.</span></span> <span data-ttu-id="125c3-164">Hoe kan ik dit oplossen?</span><span class="sxs-lookup"><span data-stu-id="125c3-164">How do I troubleshoot this?</span></span>

<span data-ttu-id="125c3-165">Als deze fout wordt weergegeven in de Azure WordPress-app, zodat php_errors.log en debug.log, voltooid de stappen uiteengezet in [inschakelen WordPress foutenlogboeken](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span><span class="sxs-lookup"><span data-stu-id="125c3-165">If you see this error in your Azure WordPress app, to enable php_errors.log and debug.log, complete the steps detailed in [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

<span data-ttu-id="125c3-166">De fout optreedt wanneer de logboeken zijn ingeschakeld, en controleer de logboeken om te zien als u buiten de verbindingen worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="125c3-166">When the logs are enabled, reproduce the error, and then check the logs to see if you are running out of connections:</span></span>
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded the ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

<span data-ttu-id="125c3-167">Als deze fout wordt weergegeven in uw debug.log of php_errors.log bestanden, wordt uw app overschrijdt het aantal verbindingen.</span><span class="sxs-lookup"><span data-stu-id="125c3-167">If you see this error in your debug.log or php_errors.log files, your app is exceeding the number of connections.</span></span> <span data-ttu-id="125c3-168">Als u op ClearDB host, controleert u of het aantal verbindingen die beschikbaar zijn in uw [serviceplan](https://www.cleardb.com/pricing.view).</span><span class="sxs-lookup"><span data-stu-id="125c3-168">If you’re hosting on ClearDB, verify the number of connections that are available in your [service plan](https://www.cleardb.com/pricing.view).</span></span>

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a><span data-ttu-id="125c3-169">Hoe ik fouten opsporen in een Node.js-app die wordt gehost in App Service?</span><span class="sxs-lookup"><span data-stu-id="125c3-169">How do I debug a Node.js app that's hosted in App Service?</span></span>

1.  <span data-ttu-id="125c3-170">Ga naar uw [Kudu-console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span><span class="sxs-lookup"><span data-stu-id="125c3-170">Go to your [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span></span>
2.  <span data-ttu-id="125c3-171">Ga naar de map van uw toepassing logs (D:\home\LogFiles\Application).</span><span class="sxs-lookup"><span data-stu-id="125c3-171">Go to your application logs folder (D:\home\LogFiles\Application).</span></span>
3.  <span data-ttu-id="125c3-172">Controleer in het bestand logging_errors.txt voor inhoud.</span><span class="sxs-lookup"><span data-stu-id="125c3-172">In the logging_errors.txt file, check for content.</span></span>

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a><span data-ttu-id="125c3-173">Hoe kan ik systeemeigen Python-modules in een App Service-web-app of API-app installeren?</span><span class="sxs-lookup"><span data-stu-id="125c3-173">How do I install native Python modules in an App Service web app or API app?</span></span>

<span data-ttu-id="125c3-174">Sommige pakketten mogelijk niet installeren met behulp van pip in Azure.</span><span class="sxs-lookup"><span data-stu-id="125c3-174">Some packages might not install by using pip in Azure.</span></span> <span data-ttu-id="125c3-175">Het pakket mogelijk niet beschikbaar op de Python Package Index of het is mogelijk dat een compiler vereist (een compiler is niet beschikbaar is op de computer waarop de web-app in App Service).</span><span class="sxs-lookup"><span data-stu-id="125c3-175">The package might not be available on the Python Package Index, or a compiler might be required (a compiler is not available on the computer that is running the web app in App Service).</span></span> <span data-ttu-id="125c3-176">Zie voor meer informatie over het installeren van systeemeigen modules in App Service-web-apps en API apps [installeren Python-modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span><span class="sxs-lookup"><span data-stu-id="125c3-176">For information about installing native modules in App Service web apps and API apps, see [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span></span>

## <a name="how-do-i-deploy-a-django-app-to-app-service-by-using-git-and-the-new-version-of-python"></a><span data-ttu-id="125c3-177">Hoe kan ik een Django-app in App Service implementeren met behulp van Git en de nieuwe versie van Python?</span><span class="sxs-lookup"><span data-stu-id="125c3-177">How do I deploy a Django app to App Service by using Git and the new version of Python?</span></span>

<span data-ttu-id="125c3-178">Zie voor meer informatie over het installeren van Django [implementeert een Django-app in App Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span><span class="sxs-lookup"><span data-stu-id="125c3-178">For information about installing Django, see [Deploying a Django app to App Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span></span>

## <a name="where-are-the-tomcat-log-files-located"></a><span data-ttu-id="125c3-179">Waar bevinden de Tomcat-logboekbestanden zich?</span><span class="sxs-lookup"><span data-stu-id="125c3-179">Where are the Tomcat log files located?</span></span>

<span data-ttu-id="125c3-180">Voor Azure Marketplace en aangepaste implementaties:</span><span class="sxs-lookup"><span data-stu-id="125c3-180">For Azure Marketplace and custom deployments:</span></span>

* <span data-ttu-id="125c3-181">Locatie van de map: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span><span class="sxs-lookup"><span data-stu-id="125c3-181">Folder location: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span></span>
* <span data-ttu-id="125c3-182">Bestanden die van belang:</span><span class="sxs-lookup"><span data-stu-id="125c3-182">Files of interest:</span></span>
    * <span data-ttu-id="125c3-183">catalina. *jjjj-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="125c3-183">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="125c3-184">host-manager. *jjjj-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="125c3-184">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="125c3-185">localhost. *jjjj-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="125c3-185">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="125c3-186">Manager. *jjjj-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="125c3-186">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="125c3-187">site_access_log. *jjjj-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="125c3-187">site_access_log.*yyyy-mm-dd*.log</span></span>


<span data-ttu-id="125c3-188">Voor portal **appinstellingen** implementaties:</span><span class="sxs-lookup"><span data-stu-id="125c3-188">For portal **App settings** deployments:</span></span>

* <span data-ttu-id="125c3-189">Locatie van de map: D:\home\LogFiles</span><span class="sxs-lookup"><span data-stu-id="125c3-189">Folder location: D:\home\LogFiles</span></span>
* <span data-ttu-id="125c3-190">Bestanden die van belang:</span><span class="sxs-lookup"><span data-stu-id="125c3-190">Files of interest:</span></span>
    * <span data-ttu-id="125c3-191">catalina. *jjjj-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="125c3-191">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="125c3-192">host-manager. *jjjj-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="125c3-192">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="125c3-193">localhost. *jjjj-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="125c3-193">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="125c3-194">Manager. *jjjj-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="125c3-194">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="125c3-195">site_access_log. *jjjj-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="125c3-195">site_access_log.*yyyy-mm-dd*.log</span></span>

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a><span data-ttu-id="125c3-196">Hoe kan ik JDBC-stuurprogramma verbindingsfouten oplossen?</span><span class="sxs-lookup"><span data-stu-id="125c3-196">How do I troubleshoot JDBC driver connection errors?</span></span>

<span data-ttu-id="125c3-197">U ziet het volgende bericht in uw Tomcat-Logboeken:</span><span class="sxs-lookup"><span data-stu-id="125c3-197">You might see the following message in your Tomcat logs:</span></span>

```
The web application[ROOT] registered the JDBC driver [com.mysql.jdbc.Driver] but failed to unregister it when the web application was stopped. To prevent a memory leak,the JDBC Driver has been forcibly unregistered
```

<span data-ttu-id="125c3-198">De fout oplossen:</span><span class="sxs-lookup"><span data-stu-id="125c3-198">To resolve the error:</span></span>

1. <span data-ttu-id="125c3-199">Verwijder het bestand sqljdbc*.jar van uw app/lib-map.</span><span class="sxs-lookup"><span data-stu-id="125c3-199">Remove the sqljdbc*.jar file from your app/lib folder.</span></span>
2. <span data-ttu-id="125c3-200">Als u de aangepaste Tomcat of Azure Marketplace Tomcat-webserver gebruikt, moet u dit JAR-bestand kopiëren naar de map Tomcat-lib.</span><span class="sxs-lookup"><span data-stu-id="125c3-200">If you are using the custom Tomcat or Azure Marketplace Tomcat web server, copy this .jar file to the Tomcat lib folder.</span></span>
3. <span data-ttu-id="125c3-201">Als u Java via de Azure-portal inschakelen wilt (Selecteer **Java 1.8** > **Tomcat-server**), het sqljdbc.* jar-bestand in de map die parallel aan uw app te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="125c3-201">If you are enabling Java from the Azure portal (select **Java 1.8** > **Tomcat server**), copy the sqljdbc.* jar file in the folder that's parallel to your app.</span></span> <span data-ttu-id="125c3-202">De volgende klassepad vervolgens toevoegen aan het bestand web.config:</span><span class="sxs-lookup"><span data-stu-id="125c3-202">Then, add the following classpath setting to the web.config file:</span></span>

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path to the sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-to-copy-live-log-files"></a><span data-ttu-id="125c3-203">Waarom zie ik fouten wanneer ik probeert te kopiëren live logboekbestanden?</span><span class="sxs-lookup"><span data-stu-id="125c3-203">Why do I see errors when I attempt to copy live log files?</span></span>

<span data-ttu-id="125c3-204">Als u probeert te kopiëren van live logboekbestanden voor een Java-app (bijvoorbeeld Tomcat), ziet u mogelijk deze FTP-fout:</span><span class="sxs-lookup"><span data-stu-id="125c3-204">If you try to copy live log files for a Java app (for example, Tomcat), you might see this FTP error:</span></span>

```
Error transferring file [filename] Copying files from remote side failed.
    
The process cannot access the file because it is being used by another process.
```

<span data-ttu-id="125c3-205">Het foutbericht kan afwijken, afhankelijk van de FTP-client.</span><span class="sxs-lookup"><span data-stu-id="125c3-205">The error message might vary, depending on the FTP client.</span></span>

<span data-ttu-id="125c3-206">Alle Java-apps hebben dit probleem vergrendelen.</span><span class="sxs-lookup"><span data-stu-id="125c3-206">All Java apps have this locking issue.</span></span> <span data-ttu-id="125c3-207">Alleen Kudu biedt ondersteuning voor het downloaden van dit bestand terwijl de app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="125c3-207">Only Kudu supports downloading this file while the app is running.</span></span>

<span data-ttu-id="125c3-208">De app wordt gestopt, kunt FTP-toegang tot deze bestanden.</span><span class="sxs-lookup"><span data-stu-id="125c3-208">Stopping the app allows FTP access to these files.</span></span>

<span data-ttu-id="125c3-209">Een andere oplossing is het schrijven van een webtaak waarmee volgens een planning wordt uitgevoerd en deze bestanden worden gekopieerd naar een andere map.</span><span class="sxs-lookup"><span data-stu-id="125c3-209">Another workaround is to write a WebJob that runs on a schedule and copies these files to a different directory.</span></span> <span data-ttu-id="125c3-210">Zie voor een voorbeeldproject de [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.</span><span class="sxs-lookup"><span data-stu-id="125c3-210">For a sample project, see the [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.</span></span>

## <a name="where-do-i-find-the-log-files-for-jetty"></a><span data-ttu-id="125c3-211">Waar vind ik de logboekbestanden voor Jetty</span><span class="sxs-lookup"><span data-stu-id="125c3-211">Where do I find the log files for Jetty?</span></span>

<span data-ttu-id="125c3-212">Voor de Marketplace en aangepaste implementaties is het logboekbestand in de map D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs.</span><span class="sxs-lookup"><span data-stu-id="125c3-212">For Marketplace and custom deployments, the log file is in the D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs folder.</span></span> <span data-ttu-id="125c3-213">Houd er rekening mee dat de locatie van de map afhankelijk is van de versie van de Jetty die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="125c3-213">Note that the folder location depends on the version of Jetty you are using.</span></span> <span data-ttu-id="125c3-214">Bijvoorbeeld, het pad opgegeven hier is voor Jetty 9.1.2.</span><span class="sxs-lookup"><span data-stu-id="125c3-214">For example, the path provided here is for Jetty 9.1.2.</span></span> <span data-ttu-id="125c3-215">Zoek naar jetty_*YYYY_MM_DD*. stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="125c3-215">Look for jetty_*YYYY_MM_DD*.stderrout.log.</span></span>

<span data-ttu-id="125c3-216">Voor implementaties van de portal App-instelling is het logboekbestand in D:\home\LogFiles.</span><span class="sxs-lookup"><span data-stu-id="125c3-216">For portal App Setting deployments, the log file is in D:\home\LogFiles.</span></span> <span data-ttu-id="125c3-217">Zoek naar jetty_*YYYY_MM_DD*. stderrout.log</span><span class="sxs-lookup"><span data-stu-id="125c3-217">Look for jetty_*YYYY_MM_DD*.stderrout.log</span></span>

## <a name="can-i-send-email-from-my-azure-web-app"></a><span data-ttu-id="125c3-218">Kan ik e-mail verzenden vanuit Mijn Azure-web-app</span><span class="sxs-lookup"><span data-stu-id="125c3-218">Can I send email from my Azure web app?</span></span>

<span data-ttu-id="125c3-219">App Service beschikt niet over een ingebouwde e-functie.</span><span class="sxs-lookup"><span data-stu-id="125c3-219">App Service doesn't have a built-in email feature.</span></span> <span data-ttu-id="125c3-220">Voor sommige goede alternatieven voor het verzenden van e-mail van uw app, raadpleegt u dit [bespreking van de Stack Overflow](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span><span class="sxs-lookup"><span data-stu-id="125c3-220">For some good alternatives for sending email from your app, see this [Stack Overflow discussion](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span></span>

## <a name="why-does-my-wordpress-site-redirect-to-another-url"></a><span data-ttu-id="125c3-221">Waarom mijn WordPress-site omleiden naar een andere URL?</span><span class="sxs-lookup"><span data-stu-id="125c3-221">Why does my WordPress site redirect to another URL?</span></span>

<span data-ttu-id="125c3-222">Als u onlangs naar Azure hebt gemigreerd, mogelijk WordPress omleiden naar de oude domein-URL.</span><span class="sxs-lookup"><span data-stu-id="125c3-222">If you have recently migrated to Azure, WordPress might redirect to the old domain URL.</span></span> <span data-ttu-id="125c3-223">Dit wordt veroorzaakt door een instelling in de MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="125c3-223">This is caused by a setting in the MySQL database.</span></span>

<span data-ttu-id="125c3-224">WordPress contactpersoon + is een Azure Site-uitbreiding die u gebruiken kunt om bij te werken van de omleidings-URL rechtstreeks in de database.</span><span class="sxs-lookup"><span data-stu-id="125c3-224">WordPress Buddy+ is an Azure Site Extension that you can use to update the redirection URL directly in the database.</span></span> <span data-ttu-id="125c3-225">Zie voor meer informatie over het gebruik van WordPress contactpersoon + [WordPress hulpprogramma's en MySQL migratie met WordPress contactpersoon +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="125c3-225">For more information about using WordPress Buddy+, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

<span data-ttu-id="125c3-226">U kunt ook als u liever handmatig bijwerken van de omleiding URL met behulp van SQL-query's of PHPMyAdmin, Zie [WordPress: omleiden naar foutieve URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span><span class="sxs-lookup"><span data-stu-id="125c3-226">Alternatively, if you prefer to manually update the redirection URL by using SQL queries or PHPMyAdmin, see [WordPress: Redirecting to wrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span></span>

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a><span data-ttu-id="125c3-227">Hoe kan ik mijn WordPress aanmelden wachtwoord wijzigen?</span><span class="sxs-lookup"><span data-stu-id="125c3-227">How do I change my WordPress sign-in password?</span></span>

<span data-ttu-id="125c3-228">Als u uw WordPress aanmelden wachtwoord vergeten bent, kunt u WordPress contactpersoon + bij te werken.</span><span class="sxs-lookup"><span data-stu-id="125c3-228">If you have forgotten your WordPress sign-in password, you can use WordPress Buddy+ to update it.</span></span> <span data-ttu-id="125c3-229">De WordPress contactpersoon + Azure Site-uitbreiding installeren om uw wachtwoord opnieuw instellen, en voltooi vervolgens de stappen in [WordPress hulpprogramma's en MySQL migratie met WordPress contactpersoon +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="125c3-229">To reset your password, install the WordPress Buddy+ Azure Site Extension, and then complete the steps described in [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="i-cant-sign-in-to-wordpress-how-do-i-resolve-this"></a><span data-ttu-id="125c3-230">Ik kan niet aanmelden bij WordPress.</span><span class="sxs-lookup"><span data-stu-id="125c3-230">I can't sign in to WordPress.</span></span> <span data-ttu-id="125c3-231">Hoe kan ik dit oplossen?</span><span class="sxs-lookup"><span data-stu-id="125c3-231">How do I resolve this?</span></span>

<span data-ttu-id="125c3-232">Als u WordPress vergrendeld merkt na de installatie van een invoegtoepassing onlangs, hebt u mogelijk een defecte invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="125c3-232">If you find yourself locked out of WordPress after recently installing a plugin, you might have a faulty plugin.</span></span> <span data-ttu-id="125c3-233">WordPress contactpersoon + is een Azure-Site-uitbreiding die u kunnen helpen uitschakelen invoegtoepassingen in WordPress.</span><span class="sxs-lookup"><span data-stu-id="125c3-233">WordPress Buddy+ is an Azure Site Extension that can help you disable plugins in WordPress.</span></span> <span data-ttu-id="125c3-234">Zie voor meer informatie [WordPress hulpprogramma's en MySQL migratie met WordPress contactpersoon +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="125c3-234">For more information, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="how-do-i-migrate-my-wordpress-database"></a><span data-ttu-id="125c3-235">Hoe Migreer ik mijn WordPress-database</span><span class="sxs-lookup"><span data-stu-id="125c3-235">How do I migrate my WordPress database?</span></span>

<span data-ttu-id="125c3-236">U hebt meerdere mogelijkheden voor het migreren van de MySQL-database die verbonden met uw WordPress-website:</span><span class="sxs-lookup"><span data-stu-id="125c3-236">You have multiple options for migrating the MySQL database that's connected to your WordPress website:</span></span>

* <span data-ttu-id="125c3-237">Ontwikkelaars: Gebruik de [opdrachtprompt of PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span><span class="sxs-lookup"><span data-stu-id="125c3-237">Developers: Use the [command prompt or PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span></span>
* <span data-ttu-id="125c3-238">Niet-Ontwikkelaars: [WordPress contactpersoon +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span><span class="sxs-lookup"><span data-stu-id="125c3-238">Non-developers: Use [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span></span>

## <a name="how-do-i-help-make-wordpress-more-secure"></a><span data-ttu-id="125c3-239">Hoe u helpen WordPress veiliger maken?</span><span class="sxs-lookup"><span data-stu-id="125c3-239">How do I help make WordPress more secure?</span></span>

<span data-ttu-id="125c3-240">Zie voor meer informatie over aanbevolen beveiligingsprocedures voor WordPress, [Best practices voor beveiliging van WordPress in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span><span class="sxs-lookup"><span data-stu-id="125c3-240">To learn about security best practices for WordPress, see [Best practices for WordPress security in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span></span>

## <a name="i-am-trying-to-use-phpmyadmin-and-i-see-the-message-access-denied-how-do-i-resolve-this"></a><span data-ttu-id="125c3-241">Ik wil gebruiken PHPMyAdmin en verschijnt het bericht 'Toegang geweigerd.'</span><span class="sxs-lookup"><span data-stu-id="125c3-241">I am trying to use PHPMyAdmin, and I see the message “Access denied.”</span></span> <span data-ttu-id="125c3-242">Hoe kan ik dit oplossen?</span><span class="sxs-lookup"><span data-stu-id="125c3-242">How do I resolve this?</span></span>

<span data-ttu-id="125c3-243">U kunt dit probleem kan optreden als de MySQL-in-app-functie nog niet wordt uitgevoerd in dit App Service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="125c3-243">You might experience this issue if the MySQL in-app feature isn't running yet in this App Service instance.</span></span> <span data-ttu-id="125c3-244">Probeer het probleem op te lossen voor toegang tot uw website.</span><span class="sxs-lookup"><span data-stu-id="125c3-244">To resolve the issue, try to access your website.</span></span> <span data-ttu-id="125c3-245">Hiermee start u de vereiste processen, met inbegrip van het proces van MySQL-app.</span><span class="sxs-lookup"><span data-stu-id="125c3-245">This starts the required processes, including the MySQL in-app process.</span></span> <span data-ttu-id="125c3-246">Zorg ervoor dat mysqld.exe wordt vermeld in de processen om te controleren of MySQL in-app wordt uitgevoerd, klikt u in proces Explorer.</span><span class="sxs-lookup"><span data-stu-id="125c3-246">To verify that MySQL in-app is running, in Process Explorer, ensure that mysqld.exe is listed in the processes.</span></span>

<span data-ttu-id="125c3-247">Nadat u ervoor te dat MySQL zorgen in-app wordt uitgevoerd, probeert u PHPMyAdmin gebruiken.</span><span class="sxs-lookup"><span data-stu-id="125c3-247">After you ensure that MySQL in-app is running, try to use PHPMyAdmin.</span></span>

## <a name="i-get-an-http-403-error-when-i-try-to-import-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a><span data-ttu-id="125c3-248">Ik krijg een HTTP 403-foutmelding wanneer ik probeer te importeren en exporteren van mijn MySQL-database in-app met behulp van PHPMyadmin.</span><span class="sxs-lookup"><span data-stu-id="125c3-248">I get an HTTP 403 error when I try to import or export my MySQL in-app database by using PHPMyadmin.</span></span> <span data-ttu-id="125c3-249">Hoe kan ik dit oplossen?</span><span class="sxs-lookup"><span data-stu-id="125c3-249">How do I resolve this?</span></span>

<span data-ttu-id="125c3-250">Als u een oudere versie van Chrome gebruikt, u mogelijk ondervindt een bekend probleem.</span><span class="sxs-lookup"><span data-stu-id="125c3-250">If you are using an older version of Chrome, you might be experiencing a known bug.</span></span> <span data-ttu-id="125c3-251">Upgraden naar een nieuwere versie van Chrome het probleem op te lossen.</span><span class="sxs-lookup"><span data-stu-id="125c3-251">To resolve the issue, upgrade to a newer version of Chrome.</span></span> <span data-ttu-id="125c3-252">Ook kunt u proberen met een andere browser, zoals Internet Explorer of Edge, waar het probleem niet wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="125c3-252">Also try using a different browser, like Internet Explorer or Edge, where the issue does not occur.</span></span>
