---
title: "aaaOpen bron technologieën Veelgestelde vragen over Azure web-apps | Microsoft Docs"
description: "Toofrequently van antwoorden op veelgestelde vragen over open source-technologieën in functie van Hallo-Web-Apps van Azure App Service worden opgehaald."
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
ms.openlocfilehash: 35cff4f322859d25972747cf55aa7c4316381a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a><span data-ttu-id="b28d6-103">Open source-technologieën Veelgestelde vragen voor Web-Apps in Azure</span><span class="sxs-lookup"><span data-stu-id="b28d6-103">Open-source technologies FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="b28d6-104">Dit artikel bevat antwoorden toofrequently Veelgestelde vragen (FAQ's) over problemen met open source-technologieën voor Hallo [functie van Azure App Service Web Apps](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="b28d6-104">This article has answers toofrequently asked questions (FAQs) about issues with open-source technologies for hello [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a><span data-ttu-id="b28d6-105">Mijn ClearDB-database is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="b28d6-105">My ClearDB database is down.</span></span> <span data-ttu-id="b28d6-106">Hoe kan ik dit oplossen?</span><span class="sxs-lookup"><span data-stu-id="b28d6-106">How do I resolve this?</span></span>

<span data-ttu-id="b28d6-107">Problemen met database contact op met [ClearDB ondersteuning](https://www.cleardb.com/developers/help/support).</span><span class="sxs-lookup"><span data-stu-id="b28d6-107">For database-related issues, contact [ClearDB support](https://www.cleardb.com/developers/help/support).</span></span> 

<span data-ttu-id="b28d6-108">Bekijk voor antwoorden toocommon vragen over ClearDB [ClearDB Veelgestelde vragen over](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="b28d6-108">For answers toocommon questions about ClearDB, see [ClearDB FAQs](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-isnt-my-cleardb-database-listed-in-hello-portal"></a><span data-ttu-id="b28d6-109">Waarom wordt mijn ClearDB-database niet vermeld in Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="b28d6-109">Why isn't my ClearDB database listed in hello portal?</span></span>

<span data-ttu-id="b28d6-110">Als u een ClearDB-database in Hallo maken [Azure-portal](http://portal.azure.com/), Hallo-database wordt niet weergegeven in Hallo [klassieke Azure-portal](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="b28d6-110">If you create a ClearDB database in hello [Azure portal](http://portal.azure.com/), hello database doesn't appear in hello [Azure classic portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="b28d6-111">toowork voorkomen, kunt u handmatig uw database toohello web-app koppelen.</span><span class="sxs-lookup"><span data-stu-id="b28d6-111">toowork around this, you can manually link your database toohello web app.</span></span>

<span data-ttu-id="b28d6-112">Op dezelfde manier als u een ClearDB-database in Hallo maken [klassieke Azure-portal](http://manage.windowsazure.com/), ziet u niet de database in Hallo [Azure-portal](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b28d6-112">Similarly, if you create a ClearDB database in hello [Azure classic portal](http://manage.windowsazure.com/),  you won't see your database in hello [Azure portal](http://portal.azure.com/).</span></span> <span data-ttu-id="b28d6-113">In dit geval is geen oplossing beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="b28d6-113">In this case, no workaround is available.</span></span> 

<span data-ttu-id="b28d6-114">Zie voor meer informatie [Veelgestelde vragen over ClearDB MySQL-databases met Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="b28d6-114">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a><span data-ttu-id="b28d6-115">Waarom worden mijn ClearDB-database, is niet gemigreerd tijdens de abonnementmigratie van mijn?</span><span class="sxs-lookup"><span data-stu-id="b28d6-115">Why wasn't my ClearDB database migrated during my subscription migration?</span></span>

<span data-ttu-id="b28d6-116">Wanneer u Resourcemigratie voor abonnementen uitvoert, zijn enkele beperkingen van toepassing.</span><span class="sxs-lookup"><span data-stu-id="b28d6-116">When you perform resource migration across subscriptions, some limitations apply.</span></span> <span data-ttu-id="b28d6-117">Een ClearDB MySQL-database is een service van derden en wordt tijdens de migratie van een Azure-abonnement niet gemigreerd.</span><span class="sxs-lookup"><span data-stu-id="b28d6-117">A ClearDB MySQL database is a third-party service and is not migrated during an Azure subscription migration.</span></span>

<span data-ttu-id="b28d6-118">Als u geen Hallo migratie van uw MySQL-database beheren voordat u uw Azure-resources migreert, is het mogelijk dat uw ClearDB MySQL-database niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="b28d6-118">If you don't manage hello migration of your MySQL database before you migrate your Azure resources, your ClearDB MySQL database might be unavailable.</span></span> <span data-ttu-id="b28d6-119">tooavoid dit eerst handmatig migreren uw ClearDB-database en vervolgens migreren hello Azure-abonnement voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="b28d6-119">tooavoid this, first, manually migrate your ClearDB database, and then migrate hello Azure subscription for your web app.</span></span>

<span data-ttu-id="b28d6-120">Zie voor meer informatie [Veelgestelde vragen over ClearDB MySQL-databases met Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="b28d6-120">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="how-do-i-turn-on-php-logging-tootroubleshoot-php-issues"></a><span data-ttu-id="b28d6-121">Hoe kan ik PHP tootroubleshoot PHP problemen logboekregistratie inschakelen?</span><span class="sxs-lookup"><span data-stu-id="b28d6-121">How do I turn on PHP logging tootroubleshoot PHP issues?</span></span>

<span data-ttu-id="b28d6-122">tooturn PHP logboekregistratie:</span><span class="sxs-lookup"><span data-stu-id="b28d6-122">tooturn on PHP logging:</span></span>

1. <span data-ttu-id="b28d6-123">Meld u aan tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="b28d6-123">Sign in tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="b28d6-124">Selecteer in het bovenste menu Hallo **Console voor foutopsporing** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="b28d6-124">In hello top menu, select **Debug Console** > **CMD**.</span></span>
3. <span data-ttu-id="b28d6-125">Selecteer Hallo **Site** map.</span><span class="sxs-lookup"><span data-stu-id="b28d6-125">Select hello **Site** folder.</span></span>
4. <span data-ttu-id="b28d6-126">Selecteer Hallo **wwwroot** map.</span><span class="sxs-lookup"><span data-stu-id="b28d6-126">Select hello **wwwroot** folder.</span></span>
5. <span data-ttu-id="b28d6-127">Selecteer Hallo  **+**  pictogram en selecteer vervolgens **nieuw bestand**.</span><span class="sxs-lookup"><span data-stu-id="b28d6-127">Select hello **+** icon, and then select **New File**.</span></span>
6. <span data-ttu-id="b28d6-128">Hallo-bestandsnaam te ingesteld**. user.ini**.</span><span class="sxs-lookup"><span data-stu-id="b28d6-128">Set hello file name too**.user.ini**.</span></span>
7. <span data-ttu-id="b28d6-129">Selecteer Hallo potloodpictogram naast te**. user.ini**.</span><span class="sxs-lookup"><span data-stu-id="b28d6-129">Select hello pencil icon next too**.user.ini**.</span></span>
8. <span data-ttu-id="b28d6-130">Voeg deze code in Hallo-bestand:`log_errors=on`</span><span class="sxs-lookup"><span data-stu-id="b28d6-130">In hello file, add this code: `log_errors=on`</span></span>
9. <span data-ttu-id="b28d6-131">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b28d6-131">Select **Save**.</span></span>
10. <span data-ttu-id="b28d6-132">Selecteer Hallo potloodpictogram naast te**wp-config.php**.</span><span class="sxs-lookup"><span data-stu-id="b28d6-132">Select hello pencil icon next too**wp-config.php**.</span></span>
11. <span data-ttu-id="b28d6-133">Hallo tekst toohello na code wijzigen:</span><span class="sxs-lookup"><span data-stu-id="b28d6-133">Change hello text toohello following code:</span></span>
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging too/wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings tooscreendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors tooscreenini_set('display_errors', 0);
   ```
12. <span data-ttu-id="b28d6-134">Start opnieuw op uw web-app in hello Azure-portal in Hallo web app-menu.</span><span class="sxs-lookup"><span data-stu-id="b28d6-134">In hello Azure portal, in hello web app menu, restart your web app.</span></span>

<span data-ttu-id="b28d6-135">Zie voor meer informatie [inschakelen WordPress foutenlogboeken](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span><span class="sxs-lookup"><span data-stu-id="b28d6-135">For more information, see [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a><span data-ttu-id="b28d6-136">Hoe meld ik toepassingsfouten in Python in apps die worden gehost in App Service</span><span class="sxs-lookup"><span data-stu-id="b28d6-136">How do I log Python application errors in apps that are hosted in App Service?</span></span>

<span data-ttu-id="b28d6-137">toepassingsfouten in Python toocapture:</span><span class="sxs-lookup"><span data-stu-id="b28d6-137">toocapture Python application errors:</span></span>

1. <span data-ttu-id="b28d6-138">Selecteer in de Azure-portal in uw web-app Hallo **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="b28d6-138">In hello Azure portal, in your web app, select **Settings**.</span></span>
2. <span data-ttu-id="b28d6-139">Op Hallo **instellingen** tabblad **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="b28d6-139">On hello **Settings** tab, select **Application settings**.</span></span>
3. <span data-ttu-id="b28d6-140">Onder **appinstellingen**, Voer Hallo sleutel-waardepaar te volgen:</span><span class="sxs-lookup"><span data-stu-id="b28d6-140">Under **App settings**, enter hello following key/value pair:</span></span>
    * <span data-ttu-id="b28d6-141">Sleutel: WSGI_LOG</span><span class="sxs-lookup"><span data-stu-id="b28d6-141">Key : WSGI_LOG</span></span>
    * <span data-ttu-id="b28d6-142">Waarde: D:\home\site\wwwroot\logs.txt (uw keuze van bestandsnaam invoeren)</span><span class="sxs-lookup"><span data-stu-id="b28d6-142">Value : D:\home\site\wwwroot\logs.txt (enter your choice of file name)</span></span>

<span data-ttu-id="b28d6-143">U ziet nu de fouten in Hallo logs.txt bestand in de map wwwroot Hallo.</span><span class="sxs-lookup"><span data-stu-id="b28d6-143">You should now see errors in hello logs.txt file in hello wwwroot folder.</span></span>

## <a name="how-do-i-change-hello-version-of-hello-nodejs-application-that-is-hosted-in-app-service"></a><span data-ttu-id="b28d6-144">Hoe wijzig ik Hallo-versie van Hallo Node.js-toepassing die wordt gehost in App Service?</span><span class="sxs-lookup"><span data-stu-id="b28d6-144">How do I change hello version of hello Node.js application that is hosted in App Service?</span></span>

<span data-ttu-id="b28d6-145">toochange Hallo-versie van Node.js-toepassing hello, kunt u een Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="b28d6-145">toochange hello version of hello Node.js application, you can use one of hello following options:</span></span>

*   <span data-ttu-id="b28d6-146">Gebruik in hello Azure-portal, **appinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="b28d6-146">In hello Azure portal, use **App settings**.</span></span>
    1. <span data-ttu-id="b28d6-147">Ga in de Azure-portal hello, tooyour web-app.</span><span class="sxs-lookup"><span data-stu-id="b28d6-147">In hello Azure portal, go tooyour web app.</span></span>
    2. <span data-ttu-id="b28d6-148">Op Hallo **instellingen** blade Selecteer **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="b28d6-148">On hello **Settings** blade, select **Application settings**.</span></span>
    3. <span data-ttu-id="b28d6-149">In **appinstellingen**, kunt u WEBSITE_NODE_DEFAULT_VERSION als Hallo sleutel opnemen en hello versie van Node.js u wilt gebruiken als Hallo-waarde.</span><span class="sxs-lookup"><span data-stu-id="b28d6-149">In **App settings**, you can include WEBSITE_NODE_DEFAULT_VERSION as hello key, and hello version of Node.js you want as hello value.</span></span>
    4. <span data-ttu-id="b28d6-150">Ga tooyour [Kudu-console](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="b28d6-150">Go tooyour [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
    5. <span data-ttu-id="b28d6-151">toocheck Hallo Node.js-versie, Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="b28d6-151">toocheck hello Node.js version, enter hello following command:</span></span>  
   ```
   node -v
   ```
*   <span data-ttu-id="b28d6-152">Hallo iisnode.yml bestand te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b28d6-152">Modify hello iisnode.yml file.</span></span> <span data-ttu-id="b28d6-153">Veranderende Hallo Node.js-versie in Hallo iisnode.yml bestand alleen ingesteld Hallo runtime-omgeving waarnaar iisnode gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b28d6-153">Changing hello Node.js version in hello iisnode.yml file only sets hello runtime environment that iisnode uses.</span></span> <span data-ttu-id="b28d6-154">Uw cmd Kudu en anderen die nog steeds gebruiken Hallo Node.js-versie die is ingesteld in **appinstellingen** in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b28d6-154">Your Kudu cmd and others still use hello Node.js version that is set in **App settings** in hello Azure portal.</span></span>

    <span data-ttu-id="b28d6-155">een bestand iisnode.yml tooset hello iisnode.yml handmatig maken in de hoofdmap van uw app.</span><span class="sxs-lookup"><span data-stu-id="b28d6-155">tooset hello iisnode.yml manually, create an iisnode.yml file in your app root folder.</span></span> <span data-ttu-id="b28d6-156">In het bestand hello, zijn onder andere Hallo volgt regel:</span><span class="sxs-lookup"><span data-stu-id="b28d6-156">In hello file, include hello following line:</span></span>
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   <span data-ttu-id="b28d6-157">Hallo iisnode.yml bestand worden ingesteld met behulp van package.json tijdens de implementatie van de bron-besturingselement.</span><span class="sxs-lookup"><span data-stu-id="b28d6-157">Set hello iisnode.yml file by using package.json during source control deployment.</span></span>
    <span data-ttu-id="b28d6-158">Hello Azure bron besturingselement implementatieproces omvat Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b28d6-158">hello Azure source control deployment process involves hello following steps:</span></span>
    1. <span data-ttu-id="b28d6-159">Hiermee verplaatst u inhoud toohello Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="b28d6-159">Moves content toohello Azure web app.</span></span>
    2. <span data-ttu-id="b28d6-160">Als er niet (deploy.cmd, .deployment-bestanden) in de hoofdmap van Hallo web app is, maakt een standaard implementatiescript.</span><span class="sxs-lookup"><span data-stu-id="b28d6-160">Creates a default deployment script, if there isn’t one (deploy.cmd, .deployment files) in hello web app root folder.</span></span>
    3. <span data-ttu-id="b28d6-161">Wordt uitgevoerd een implementatiescript waarin deze een iisnode.yml bestand maakt als u vermeld Hallo Node.js-versie in Hallo package.json-bestand > engine`"engines": {"node": "5.9.1","npm": "3.7.3"}`</span><span class="sxs-lookup"><span data-stu-id="b28d6-161">Runs a deployment script in which it creates an iisnode.yml file if you mention hello Node.js version in hello package.json file > engine `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span></span>
    4. <span data-ttu-id="b28d6-162">Hallo iisnode.yml bestand heeft de volgende coderegel Hallo:</span><span class="sxs-lookup"><span data-stu-id="b28d6-162">hello iisnode.yml file has hello following line of code:</span></span>
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-hello-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a><span data-ttu-id="b28d6-163">Ik zie Hallo-bericht 'Fout bij het maken van een databaseverbinding ' in mijn WordPress-app die wordt gehost in App Service.</span><span class="sxs-lookup"><span data-stu-id="b28d6-163">I see hello message "Error establishing a database connection" in my WordPress app that's hosted in App Service.</span></span> <span data-ttu-id="b28d6-164">Hoe kan ik dit oplossen?</span><span class="sxs-lookup"><span data-stu-id="b28d6-164">How do I troubleshoot this?</span></span>

<span data-ttu-id="b28d6-165">Als u deze fout in uw Azure WordPress-app, tooenable php_errors.log en debug.log ziet, volledige Hallo stappen uiteengezet in [inschakelen WordPress foutenlogboeken](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span><span class="sxs-lookup"><span data-stu-id="b28d6-165">If you see this error in your Azure WordPress app, tooenable php_errors.log and debug.log, complete hello steps detailed in [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

<span data-ttu-id="b28d6-166">Wanneer Hallo logboeken zijn ingeschakeld, Hallo-fout optreedt en controleer vervolgens Hallo logboeken toosee als u werkt met buiten-verbindingen:</span><span class="sxs-lookup"><span data-stu-id="b28d6-166">When hello logs are enabled, reproduce hello error, and then check hello logs toosee if you are running out of connections:</span></span>
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded hello ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

<span data-ttu-id="b28d6-167">Als deze fout wordt weergegeven in uw debug.log of php_errors.log bestanden, wordt uw app Hallo aantal verbindingen overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="b28d6-167">If you see this error in your debug.log or php_errors.log files, your app is exceeding hello number of connections.</span></span> <span data-ttu-id="b28d6-168">Als u op ClearDB host, controleert u of Hallo aantal verbindingen die beschikbaar zijn in uw [serviceplan](https://www.cleardb.com/pricing.view).</span><span class="sxs-lookup"><span data-stu-id="b28d6-168">If you’re hosting on ClearDB, verify hello number of connections that are available in your [service plan](https://www.cleardb.com/pricing.view).</span></span>

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a><span data-ttu-id="b28d6-169">Hoe ik fouten opsporen in een Node.js-app die wordt gehost in App Service?</span><span class="sxs-lookup"><span data-stu-id="b28d6-169">How do I debug a Node.js app that's hosted in App Service?</span></span>

1.  <span data-ttu-id="b28d6-170">Ga tooyour [Kudu-console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span><span class="sxs-lookup"><span data-stu-id="b28d6-170">Go tooyour [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span></span>
2.  <span data-ttu-id="b28d6-171">Ga tooyour logboeken toepassingsmap (D:\home\LogFiles\Application).</span><span class="sxs-lookup"><span data-stu-id="b28d6-171">Go tooyour application logs folder (D:\home\LogFiles\Application).</span></span>
3.  <span data-ttu-id="b28d6-172">Controleer in Hallo logging_errors.txt bestand, voor inhoud.</span><span class="sxs-lookup"><span data-stu-id="b28d6-172">In hello logging_errors.txt file, check for content.</span></span>

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a><span data-ttu-id="b28d6-173">Hoe kan ik systeemeigen Python-modules in een App Service-web-app of API-app installeren?</span><span class="sxs-lookup"><span data-stu-id="b28d6-173">How do I install native Python modules in an App Service web app or API app?</span></span>

<span data-ttu-id="b28d6-174">Sommige pakketten mogelijk niet installeren met behulp van pip in Azure.</span><span class="sxs-lookup"><span data-stu-id="b28d6-174">Some packages might not install by using pip in Azure.</span></span> <span data-ttu-id="b28d6-175">Hallo-pakket mogelijk niet beschikbaar op Hallo Python Package Index of het is mogelijk dat een compiler vereist (een compiler is niet beschikbaar is op Hallo-computer met Hallo web-app in App Service).</span><span class="sxs-lookup"><span data-stu-id="b28d6-175">hello package might not be available on hello Python Package Index, or a compiler might be required (a compiler is not available on hello computer that is running hello web app in App Service).</span></span> <span data-ttu-id="b28d6-176">Zie voor meer informatie over het installeren van systeemeigen modules in App Service-web-apps en API apps [installeren Python-modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span><span class="sxs-lookup"><span data-stu-id="b28d6-176">For information about installing native modules in App Service web apps and API apps, see [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span></span>

## <a name="how-do-i-deploy-a-django-app-tooapp-service-by-using-git-and-hello-new-version-of-python"></a><span data-ttu-id="b28d6-177">Hoe implementeer ik het tooApp in een Django-app Service met behulp van Git en Hallo nieuwe versie van Python</span><span class="sxs-lookup"><span data-stu-id="b28d6-177">How do I deploy a Django app tooApp Service by using Git and hello new version of Python?</span></span>

<span data-ttu-id="b28d6-178">Zie voor meer informatie over het installeren van Django [implementeren van een Django-app tooApp Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span><span class="sxs-lookup"><span data-stu-id="b28d6-178">For information about installing Django, see [Deploying a Django app tooApp Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span></span>

## <a name="where-are-hello-tomcat-log-files-located"></a><span data-ttu-id="b28d6-179">Waar zijn Hallo Tomcat-logboekbestanden bevinden?</span><span class="sxs-lookup"><span data-stu-id="b28d6-179">Where are hello Tomcat log files located?</span></span>

<span data-ttu-id="b28d6-180">Voor Azure Marketplace en aangepaste implementaties:</span><span class="sxs-lookup"><span data-stu-id="b28d6-180">For Azure Marketplace and custom deployments:</span></span>

* <span data-ttu-id="b28d6-181">Locatie van de map: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span><span class="sxs-lookup"><span data-stu-id="b28d6-181">Folder location: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span></span>
* <span data-ttu-id="b28d6-182">Bestanden die van belang:</span><span class="sxs-lookup"><span data-stu-id="b28d6-182">Files of interest:</span></span>
    * <span data-ttu-id="b28d6-183">catalina. *jjjj-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="b28d6-183">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="b28d6-184">host-manager. *jjjj-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="b28d6-184">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="b28d6-185">localhost. *jjjj-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="b28d6-185">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="b28d6-186">Manager. *jjjj-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="b28d6-186">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="b28d6-187">site_access_log. *jjjj-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="b28d6-187">site_access_log.*yyyy-mm-dd*.log</span></span>


<span data-ttu-id="b28d6-188">Voor portal **appinstellingen** implementaties:</span><span class="sxs-lookup"><span data-stu-id="b28d6-188">For portal **App settings** deployments:</span></span>

* <span data-ttu-id="b28d6-189">Locatie van de map: D:\home\LogFiles</span><span class="sxs-lookup"><span data-stu-id="b28d6-189">Folder location: D:\home\LogFiles</span></span>
* <span data-ttu-id="b28d6-190">Bestanden die van belang:</span><span class="sxs-lookup"><span data-stu-id="b28d6-190">Files of interest:</span></span>
    * <span data-ttu-id="b28d6-191">catalina. *jjjj-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="b28d6-191">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="b28d6-192">host-manager. *jjjj-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="b28d6-192">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="b28d6-193">localhost. *jjjj-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="b28d6-193">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="b28d6-194">Manager. *jjjj-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="b28d6-194">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="b28d6-195">site_access_log. *jjjj-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="b28d6-195">site_access_log.*yyyy-mm-dd*.log</span></span>

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a><span data-ttu-id="b28d6-196">Hoe kan ik JDBC-stuurprogramma verbindingsfouten oplossen?</span><span class="sxs-lookup"><span data-stu-id="b28d6-196">How do I troubleshoot JDBC driver connection errors?</span></span>

<span data-ttu-id="b28d6-197">U ziet Hallo-bericht in uw Tomcat-logboeken te volgen:</span><span class="sxs-lookup"><span data-stu-id="b28d6-197">You might see hello following message in your Tomcat logs:</span></span>

```
hello web application[ROOT] registered hello JDBC driver [com.mysql.jdbc.Driver] but failed toounregister it when hello web application was stopped. tooprevent a memory leak,hello JDBC Driver has been forcibly unregistered
```

<span data-ttu-id="b28d6-198">tooresolve Hallo-fout:</span><span class="sxs-lookup"><span data-stu-id="b28d6-198">tooresolve hello error:</span></span>

1. <span data-ttu-id="b28d6-199">Hallo sqljdbc*.jar bestand uit de map van uw app/lib verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b28d6-199">Remove hello sqljdbc*.jar file from your app/lib folder.</span></span>
2. <span data-ttu-id="b28d6-200">Als u van Hallo aangepaste Tomcat of Azure Marketplace Tomcat webserver gebruikmaakt, moet u deze JAR-bestand toohello Tomcat lib map kopiëren.</span><span class="sxs-lookup"><span data-stu-id="b28d6-200">If you are using hello custom Tomcat or Azure Marketplace Tomcat web server, copy this .jar file toohello Tomcat lib folder.</span></span>
3. <span data-ttu-id="b28d6-201">Als u Java van inschakelt hello Azure-portal (Selecteer **Java 1.8** > **Tomcat-server**), Hallo sqljdbc.* jar-bestand in map Hallo die parallel tooyour app kopiëren.</span><span class="sxs-lookup"><span data-stu-id="b28d6-201">If you are enabling Java from hello Azure portal (select **Java 1.8** > **Tomcat server**), copy hello sqljdbc.* jar file in hello folder that's parallel tooyour app.</span></span> <span data-ttu-id="b28d6-202">Vervolgens voegt u Hallo classpath instelling toohello web.config-bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="b28d6-202">Then, add hello following classpath setting toohello web.config file:</span></span>

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path toohello sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-toocopy-live-log-files"></a><span data-ttu-id="b28d6-203">Waarom zie ik fouten wanneer ik de live logboekbestanden toocopy proberen?</span><span class="sxs-lookup"><span data-stu-id="b28d6-203">Why do I see errors when I attempt toocopy live log files?</span></span>

<span data-ttu-id="b28d6-204">Als u probeert toocopy live logboekbestanden voor een Java-app (bijvoorbeeld Tomcat), ziet u mogelijk deze FTP-fout:</span><span class="sxs-lookup"><span data-stu-id="b28d6-204">If you try toocopy live log files for a Java app (for example, Tomcat), you might see this FTP error:</span></span>

```
Error transferring file [filename] Copying files from remote side failed.
    
hello process cannot access hello file because it is being used by another process.
```

<span data-ttu-id="b28d6-205">Fout bij het Hallo-bericht kan variëren, afhankelijk van Hallo FTP-client.</span><span class="sxs-lookup"><span data-stu-id="b28d6-205">hello error message might vary, depending on hello FTP client.</span></span>

<span data-ttu-id="b28d6-206">Alle Java-apps hebben dit probleem vergrendelen.</span><span class="sxs-lookup"><span data-stu-id="b28d6-206">All Java apps have this locking issue.</span></span> <span data-ttu-id="b28d6-207">Alleen Kudu biedt ondersteuning voor het downloaden van dit bestand tijdens het Hallo-app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b28d6-207">Only Kudu supports downloading this file while hello app is running.</span></span>

<span data-ttu-id="b28d6-208">Stoppen Hallo app toestaat toothese bestanden FTP-toegang.</span><span class="sxs-lookup"><span data-stu-id="b28d6-208">Stopping hello app allows FTP access toothese files.</span></span>

<span data-ttu-id="b28d6-209">Er is een fout opgetreden in een andere oplossing toowrite een webtaak die volgens een planning wordt uitgevoerd en deze bestanden tooa andere map kopieert.</span><span class="sxs-lookup"><span data-stu-id="b28d6-209">Another workaround is toowrite a WebJob that runs on a schedule and copies these files tooa different directory.</span></span> <span data-ttu-id="b28d6-210">Zie voor een voorbeeldproject Hallo [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.</span><span class="sxs-lookup"><span data-stu-id="b28d6-210">For a sample project, see hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.</span></span>

## <a name="where-do-i-find-hello-log-files-for-jetty"></a><span data-ttu-id="b28d6-211">Waar vind ik Hallo-logboekbestanden voor Jetty</span><span class="sxs-lookup"><span data-stu-id="b28d6-211">Where do I find hello log files for Jetty?</span></span>

<span data-ttu-id="b28d6-212">Voor Marketplace- en aangepaste implementaties is het logboekbestand Hallo Hallo D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs map.</span><span class="sxs-lookup"><span data-stu-id="b28d6-212">For Marketplace and custom deployments, hello log file is in hello D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs folder.</span></span> <span data-ttu-id="b28d6-213">Houd er rekening mee dat Hallo maplocatie afhankelijk is van Hallo-versie van de Jetty die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b28d6-213">Note that hello folder location depends on hello version of Jetty you are using.</span></span> <span data-ttu-id="b28d6-214">Hallo-pad opgegeven bijvoorbeeld hier is voor Jetty 9.1.2.</span><span class="sxs-lookup"><span data-stu-id="b28d6-214">For example, hello path provided here is for Jetty 9.1.2.</span></span> <span data-ttu-id="b28d6-215">Zoek naar jetty_*YYYY_MM_DD*. stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="b28d6-215">Look for jetty_*YYYY_MM_DD*.stderrout.log.</span></span>

<span data-ttu-id="b28d6-216">Voor implementaties van de portal App-instelling is Hallo logboekbestand in D:\home\LogFiles.</span><span class="sxs-lookup"><span data-stu-id="b28d6-216">For portal App Setting deployments, hello log file is in D:\home\LogFiles.</span></span> <span data-ttu-id="b28d6-217">Zoek naar jetty_*YYYY_MM_DD*. stderrout.log</span><span class="sxs-lookup"><span data-stu-id="b28d6-217">Look for jetty_*YYYY_MM_DD*.stderrout.log</span></span>

## <a name="can-i-send-email-from-my-azure-web-app"></a><span data-ttu-id="b28d6-218">Kan ik e-mail verzenden vanuit Mijn Azure-web-app</span><span class="sxs-lookup"><span data-stu-id="b28d6-218">Can I send email from my Azure web app?</span></span>

<span data-ttu-id="b28d6-219">App Service beschikt niet over een ingebouwde e-functie.</span><span class="sxs-lookup"><span data-stu-id="b28d6-219">App Service doesn't have a built-in email feature.</span></span> <span data-ttu-id="b28d6-220">Voor sommige goede alternatieven voor het verzenden van e-mail van uw app, raadpleegt u dit [bespreking van de Stack Overflow](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span><span class="sxs-lookup"><span data-stu-id="b28d6-220">For some good alternatives for sending email from your app, see this [Stack Overflow discussion](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span></span>

## <a name="why-does-my-wordpress-site-redirect-tooanother-url"></a><span data-ttu-id="b28d6-221">Waarom mijn WordPress-site Omleidings-URL tooanother?</span><span class="sxs-lookup"><span data-stu-id="b28d6-221">Why does my WordPress site redirect tooanother URL?</span></span>

<span data-ttu-id="b28d6-222">Als u onlangs tooAzure hebt gemigreerd, mogelijk WordPress toohello oude domein-URL omleiden.</span><span class="sxs-lookup"><span data-stu-id="b28d6-222">If you have recently migrated tooAzure, WordPress might redirect toohello old domain URL.</span></span> <span data-ttu-id="b28d6-223">Dit wordt veroorzaakt door een instelling in Hallo MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="b28d6-223">This is caused by a setting in hello MySQL database.</span></span>

<span data-ttu-id="b28d6-224">WordPress contactpersoon + is een Azure Site-uitbreiding die u rechtstreeks in de database Hallo tooupdate Hallo Omleidings-URL kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b28d6-224">WordPress Buddy+ is an Azure Site Extension that you can use tooupdate hello redirection URL directly in hello database.</span></span> <span data-ttu-id="b28d6-225">Zie voor meer informatie over het gebruik van WordPress contactpersoon + [WordPress hulpprogramma's en MySQL migratie met WordPress contactpersoon +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="b28d6-225">For more information about using WordPress Buddy+, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

<span data-ttu-id="b28d6-226">U kunt ook als u liever toomanually update Hallo Omleidings-URL met behulp van SQL-query's of PHPMyAdmin, Zie [WordPress: toowrong URL omleiden](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span><span class="sxs-lookup"><span data-stu-id="b28d6-226">Alternatively, if you prefer toomanually update hello redirection URL by using SQL queries or PHPMyAdmin, see [WordPress: Redirecting toowrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span></span>

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a><span data-ttu-id="b28d6-227">Hoe kan ik mijn WordPress aanmelden wachtwoord wijzigen?</span><span class="sxs-lookup"><span data-stu-id="b28d6-227">How do I change my WordPress sign-in password?</span></span>

<span data-ttu-id="b28d6-228">Als u uw WordPress aanmelden wachtwoord vergeten bent, kunt u WordPress contactpersoon + tooupdate deze.</span><span class="sxs-lookup"><span data-stu-id="b28d6-228">If you have forgotten your WordPress sign-in password, you can use WordPress Buddy+ tooupdate it.</span></span> <span data-ttu-id="b28d6-229">uw wachtwoord, installatie Hallo WordPress contactpersoon + Azure Site-uitbreiding en vervolgens voltooit Hallo stappen wordt beschreven in tooreset [WordPress hulpprogramma's en MySQL migratie met WordPress contactpersoon +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="b28d6-229">tooreset your password, install hello WordPress Buddy+ Azure Site Extension, and then complete hello steps described in [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="i-cant-sign-in-toowordpress-how-do-i-resolve-this"></a><span data-ttu-id="b28d6-230">Ik kan niet tooWordPress aanmelden.</span><span class="sxs-lookup"><span data-stu-id="b28d6-230">I can't sign in tooWordPress.</span></span> <span data-ttu-id="b28d6-231">Hoe kan ik dit oplossen?</span><span class="sxs-lookup"><span data-stu-id="b28d6-231">How do I resolve this?</span></span>

<span data-ttu-id="b28d6-232">Als u WordPress vergrendeld merkt na de installatie van een invoegtoepassing onlangs, hebt u mogelijk een defecte invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="b28d6-232">If you find yourself locked out of WordPress after recently installing a plugin, you might have a faulty plugin.</span></span> <span data-ttu-id="b28d6-233">WordPress contactpersoon + is een Azure-Site-uitbreiding die u kunnen helpen uitschakelen invoegtoepassingen in WordPress.</span><span class="sxs-lookup"><span data-stu-id="b28d6-233">WordPress Buddy+ is an Azure Site Extension that can help you disable plugins in WordPress.</span></span> <span data-ttu-id="b28d6-234">Zie voor meer informatie [WordPress hulpprogramma's en MySQL migratie met WordPress contactpersoon +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="b28d6-234">For more information, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="how-do-i-migrate-my-wordpress-database"></a><span data-ttu-id="b28d6-235">Hoe Migreer ik mijn WordPress-database</span><span class="sxs-lookup"><span data-stu-id="b28d6-235">How do I migrate my WordPress database?</span></span>

<span data-ttu-id="b28d6-236">U hebt meerdere mogelijkheden voor migratie Hallo MySQL-database die is verbonden tooyour WordPress-website:</span><span class="sxs-lookup"><span data-stu-id="b28d6-236">You have multiple options for migrating hello MySQL database that's connected tooyour WordPress website:</span></span>

* <span data-ttu-id="b28d6-237">Ontwikkelaars: Gebruik Hallo [opdrachtprompt of PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span><span class="sxs-lookup"><span data-stu-id="b28d6-237">Developers: Use hello [command prompt or PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span></span>
* <span data-ttu-id="b28d6-238">Niet-Ontwikkelaars: [WordPress contactpersoon +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span><span class="sxs-lookup"><span data-stu-id="b28d6-238">Non-developers: Use [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span></span>

## <a name="how-do-i-help-make-wordpress-more-secure"></a><span data-ttu-id="b28d6-239">Hoe u helpen WordPress veiliger maken?</span><span class="sxs-lookup"><span data-stu-id="b28d6-239">How do I help make WordPress more secure?</span></span>

<span data-ttu-id="b28d6-240">toolearn over aanbevolen beveiligingsprocedures voor WordPress, Zie [Best practices voor beveiliging van WordPress in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span><span class="sxs-lookup"><span data-stu-id="b28d6-240">toolearn about security best practices for WordPress, see [Best practices for WordPress security in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span></span>

## <a name="i-am-trying-toouse-phpmyadmin-and-i-see-hello-message-access-denied-how-do-i-resolve-this"></a><span data-ttu-id="b28d6-241">Ik probeer toouse PHPMyAdmin en Zie Hallo-bericht 'Toegang geweigerd'.</span><span class="sxs-lookup"><span data-stu-id="b28d6-241">I am trying toouse PHPMyAdmin, and I see hello message “Access denied.”</span></span> <span data-ttu-id="b28d6-242">Hoe kan ik dit oplossen?</span><span class="sxs-lookup"><span data-stu-id="b28d6-242">How do I resolve this?</span></span>

<span data-ttu-id="b28d6-243">U kunt dit probleem kan optreden als Hallo MySQL in-app-functie nog niet wordt uitgevoerd in dit App Service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="b28d6-243">You might experience this issue if hello MySQL in-app feature isn't running yet in this App Service instance.</span></span> <span data-ttu-id="b28d6-244">tooresolve Hallo probleem, probeer tooaccess uw website.</span><span class="sxs-lookup"><span data-stu-id="b28d6-244">tooresolve hello issue, try tooaccess your website.</span></span> <span data-ttu-id="b28d6-245">Hallo vereist processen, inclusief Hallo MySQL in-app-proces wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="b28d6-245">This starts hello required processes, including hello MySQL in-app process.</span></span> <span data-ttu-id="b28d6-246">MySQL-app wordt uitgevoerd, klikt u in proces Explorer ervoor te zorgen dat mysqld.exe tooverify wordt vermeld in het Hallo-processen.</span><span class="sxs-lookup"><span data-stu-id="b28d6-246">tooverify that MySQL in-app is running, in Process Explorer, ensure that mysqld.exe is listed in hello processes.</span></span>

<span data-ttu-id="b28d6-247">Nadat u ervoor te zorgen dat MySQL in-app wordt uitgevoerd, probeert u toouse PHPMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="b28d6-247">After you ensure that MySQL in-app is running, try toouse PHPMyAdmin.</span></span>

## <a name="i-get-an-http-403-error-when-i-try-tooimport-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a><span data-ttu-id="b28d6-248">Er verschijnt een HTTP 403-fout als ik probeer tooimport of mijn MySQL-database in-app met behulp van PHPMyadmin exporteren.</span><span class="sxs-lookup"><span data-stu-id="b28d6-248">I get an HTTP 403 error when I try tooimport or export my MySQL in-app database by using PHPMyadmin.</span></span> <span data-ttu-id="b28d6-249">Hoe kan ik dit oplossen?</span><span class="sxs-lookup"><span data-stu-id="b28d6-249">How do I resolve this?</span></span>

<span data-ttu-id="b28d6-250">Als u een oudere versie van Chrome gebruikt, u mogelijk ondervindt een bekend probleem.</span><span class="sxs-lookup"><span data-stu-id="b28d6-250">If you are using an older version of Chrome, you might be experiencing a known bug.</span></span> <span data-ttu-id="b28d6-251">tooresolve hello probleem upgrade tooa nieuwere versie van Chrome.</span><span class="sxs-lookup"><span data-stu-id="b28d6-251">tooresolve hello issue, upgrade tooa newer version of Chrome.</span></span> <span data-ttu-id="b28d6-252">Ook kunt u proberen met een andere browser, zoals Internet Explorer of Edge, waarbij Hallo niet gebeurt.</span><span class="sxs-lookup"><span data-stu-id="b28d6-252">Also try using a different browser, like Internet Explorer or Edge, where hello issue does not occur.</span></span>
