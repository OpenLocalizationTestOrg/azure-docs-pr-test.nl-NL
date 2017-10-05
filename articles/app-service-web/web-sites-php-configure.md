---
title: PHP configureren in Azure App Service WebApps | Microsoft Docs
description: Informatie over het configureren van de standaard PHP-installatie of het toevoegen van een aangepaste PHP-installatie voor Web-Apps in Azure App Service.
services: app-service
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 95c4072b-8570-496b-9c48-ee21a223fb60
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 624dd416f37aacdb3d2f6e59afdc2efe646e610b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-php-in-azure-app-service-web-apps"></a><span data-ttu-id="81611-103">PHP configureren in Azure App Service WebApps</span><span class="sxs-lookup"><span data-stu-id="81611-103">Configure PHP in Azure App Service Web Apps</span></span>
## <a name="introduction"></a><span data-ttu-id="81611-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="81611-104">Introduction</span></span>
<span data-ttu-id="81611-105">Deze handleiding wordt beschreven hoe u voor het configureren van de ingebouwde PHP-runtime voor Web-Apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), geeft u een aangepaste PHP-runtime en uitbreidingen inschakelen.</span><span class="sxs-lookup"><span data-stu-id="81611-105">This guide will show you how to configure the built-in PHP runtime for Web Apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), provide a custom PHP runtime, and enable extensions.</span></span> <span data-ttu-id="81611-106">Voor het gebruik van App Service moet zich aanmelden voor de [gratis proefversie].</span><span class="sxs-lookup"><span data-stu-id="81611-106">To use App Service, sign up for the [free trial].</span></span> <span data-ttu-id="81611-107">Als u optimaal van deze handleiding, moet u eerst een PHP-web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="81611-107">To get the most from this guide, you should first create a PHP web app in App Service.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-the-built-in-php-version"></a><span data-ttu-id="81611-108">Procedure: ingebouwde PHP-versie wijzigen</span><span class="sxs-lookup"><span data-stu-id="81611-108">How to: Change the built-in PHP version</span></span>
<span data-ttu-id="81611-109">Standaard is PHP 5.5 geïnstalleerd en onmiddellijk beschikbaar voor gebruik bij het maken van een App Service-web-app.</span><span class="sxs-lookup"><span data-stu-id="81611-109">By default, PHP 5.5 is installed and immediately available for use when you create an App Service web app.</span></span> <span data-ttu-id="81611-110">De beste manier om de beschikbare versie revisie, de standaardconfiguratie en de ingeschakelde extensies is voor het implementeren van een script dat roept de [phpinfo()] functie.</span><span class="sxs-lookup"><span data-stu-id="81611-110">The best way to see the available release revision, its default configuration, and the enabled extensions is to deploy a script that calls the [phpinfo()] function.</span></span>

<span data-ttu-id="81611-111">De versies van PHP 5.6 en PHP 7.0 zijn ook beschikbaar, maar niet standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="81611-111">PHP 5.6 and PHP 7.0 versions are also available, but not enabled by default.</span></span> <span data-ttu-id="81611-112">Voer een van deze methoden voor het bijwerken van de PHP-versie:</span><span class="sxs-lookup"><span data-stu-id="81611-112">To update the PHP version, follow one of these methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="81611-113">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="81611-113">Azure Portal</span></span>
1. <span data-ttu-id="81611-114">Blader naar uw web-app in de [Azure Portal](https://portal.azure.com) en klik op de **instellingen** knop.</span><span class="sxs-lookup"><span data-stu-id="81611-114">Browse to your web app in the [Azure Portal](https://portal.azure.com) and click on the **Settings** button.</span></span>
   
    ![Instellingen voor Web-App][settings-button]
2. <span data-ttu-id="81611-116">Van de **instellingen** blade Selecteer **toepassingsinstellingen** en kiest u de nieuwe versie van PHP.</span><span class="sxs-lookup"><span data-stu-id="81611-116">From the **Settings** blade select **Application Settings** and choose the new PHP version.</span></span>
   
    ![Toepassingsinstellingen][application-settings]
3. <span data-ttu-id="81611-118">Klik op de **opslaan** knop aan de bovenkant van de **Web-appinstellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="81611-118">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![Configuratie-instellingen opslaan][save-button]

### <a name="azure-powershell-windows"></a><span data-ttu-id="81611-120">Azure PowerShell (Windows)</span><span class="sxs-lookup"><span data-stu-id="81611-120">Azure PowerShell (Windows)</span></span>
1. <span data-ttu-id="81611-121">Open Azure PowerShell en meld u aan bij uw account:</span><span class="sxs-lookup"><span data-stu-id="81611-121">Open Azure PowerShell, and login to your account:</span></span>
   
        PS C:\> Login-AzureRmAccount
2. <span data-ttu-id="81611-122">Stel de PHP-versie voor de web-app.</span><span class="sxs-lookup"><span data-stu-id="81611-122">Set the PHP version for the web app.</span></span>
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. <span data-ttu-id="81611-123">De PHP-versie is nu ingesteld.</span><span class="sxs-lookup"><span data-stu-id="81611-123">The PHP version is now set.</span></span> <span data-ttu-id="81611-124">U kunt deze instellingen controleren:</span><span class="sxs-lookup"><span data-stu-id="81611-124">You can confirm these settings:</span></span>
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a><span data-ttu-id="81611-125">Azure-opdrachtregelinterface (Linux, Mac, Windows)</span><span class="sxs-lookup"><span data-stu-id="81611-125">Azure Command-Line Interface (Linux, Mac, Windows)</span></span>
<span data-ttu-id="81611-126">U moet hebben voor het gebruik van de Azure-opdrachtregelinterface **Node.js** op uw computer geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="81611-126">To use the Azure Command-Line Interface, you must have **Node.js** installed on your computer.</span></span>

1. <span data-ttu-id="81611-127">Open Terminal en meld u aan bij uw account.</span><span class="sxs-lookup"><span data-stu-id="81611-127">Open Terminal, and login to your account.</span></span>
   
        azure login
2. <span data-ttu-id="81611-128">Stel de PHP-versie voor de web-app.</span><span class="sxs-lookup"><span data-stu-id="81611-128">Set the PHP version for the web app.</span></span>
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. <span data-ttu-id="81611-129">De PHP-versie is nu ingesteld.</span><span class="sxs-lookup"><span data-stu-id="81611-129">The PHP version is now set.</span></span> <span data-ttu-id="81611-130">U kunt deze instellingen controleren:</span><span class="sxs-lookup"><span data-stu-id="81611-130">You can confirm these settings:</span></span>
   
        azure site show {app-name}

> [!NOTE] 
> <span data-ttu-id="81611-131">De [Azure CLI 2.0](https://github.com/Azure/azure-cli) opdrachten die equivalent aan de bovenstaande zijn zijn:</span><span class="sxs-lookup"><span data-stu-id="81611-131">The [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands that are equivalent to the above are:</span></span>
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-the-built-in-php-configurations"></a><span data-ttu-id="81611-132">Procedure: de ingebouwde PHP-configuraties wijzigen</span><span class="sxs-lookup"><span data-stu-id="81611-132">How to: Change the built-in PHP configurations</span></span>
<span data-ttu-id="81611-133">Voor een ingebouwde PHP-runtime kunt u een van de configuratieopties wijzigen door de onderstaande stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="81611-133">For any built-in PHP runtime, you can change any of the configuration options by following the steps below.</span></span> <span data-ttu-id="81611-134">(Zie voor meer informatie over richtlijnen php.ini [lijst van php.ini richtlijnen].)</span><span class="sxs-lookup"><span data-stu-id="81611-134">(For information about php.ini directives, see [List of php.ini directives].)</span></span>

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a><span data-ttu-id="81611-135">Het wijzigen van PHP\_INI\_gebruiker, PHP\_INI\_PERDIR, PHP\_INI\_alle configuratie-instellingen</span><span class="sxs-lookup"><span data-stu-id="81611-135">Changing PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL configuration settings</span></span>
1. <span data-ttu-id="81611-136">Voeg een [. user.ini] bestand naar de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="81611-136">Add a [.user.ini] file to your root directory.</span></span>
2. <span data-ttu-id="81611-137">Configuratieinstellingen toevoegen aan de `.user.ini` bestand met dezelfde syntaxis als u wilt gebruiken in een `php.ini` bestand.</span><span class="sxs-lookup"><span data-stu-id="81611-137">Add configuration settings to the `.user.ini` file using the same syntax you would use in a `php.ini` file.</span></span> <span data-ttu-id="81611-138">Bijvoorbeeld, als u wilt inschakelen de `display_errors` instelling Stel `upload_max_filesize` instelt op 10M, uw `.user.ini` bestand zou deze tekst bevatten:</span><span class="sxs-lookup"><span data-stu-id="81611-138">For example, if you wanted to turn the `display_errors` setting on and set `upload_max_filesize` setting to 10M, your `.user.ini` file would contain this text:</span></span>
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on to write errors to d:\home\LogFiles\php_errors.log
        ; log_errors=On
3. <span data-ttu-id="81611-139">Implementeer uw web-app.</span><span class="sxs-lookup"><span data-stu-id="81611-139">Deploy your web app.</span></span>
4. <span data-ttu-id="81611-140">Start opnieuw op de web-app.</span><span class="sxs-lookup"><span data-stu-id="81611-140">Restart the web app.</span></span> <span data-ttu-id="81611-141">(Opnieuw opstarten is nodig omdat de frequentie welke PHP leest `.user.ini` bestanden wordt bepaald door de `user_ini.cache_ttl` instelling, die is een systeemniveau-instelling en 300 seconden (5 minuten) is standaard.</span><span class="sxs-lookup"><span data-stu-id="81611-141">(Restarting is necessary because the frequency with which PHP reads `.user.ini` files is governed by the `user_ini.cache_ttl` setting, which is a system level setting and is 300 seconds (5 minutes) by default.</span></span> <span data-ttu-id="81611-142">Opnieuw starten van de web-app forceert PHP lezen van de nieuwe instellingen in de `.user.ini` bestand.)</span><span class="sxs-lookup"><span data-stu-id="81611-142">Restarting the web app forces PHP to read the new settings in the `.user.ini` file.)</span></span>

<span data-ttu-id="81611-143">Als alternatief voor het gebruik van een `.user.ini` -bestand, kunt u de [ini_set()] functie in scripts in te stellen van de configuratieopties die niet op systeemniveau richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="81611-143">As an alternative to using a `.user.ini` file, you can use the [ini_set()] function in scripts to set configuration options that are not system-level directives.</span></span>

### <a name="changing-phpinisystem-configuration-settings"></a><span data-ttu-id="81611-144">Het wijzigen van PHP\_INI\_SYSTEM configuratie-instellingen</span><span class="sxs-lookup"><span data-stu-id="81611-144">Changing PHP\_INI\_SYSTEM configuration settings</span></span>
1. <span data-ttu-id="81611-145">Een App-instelling toevoegen aan uw Web-App met de sleutel `PHP_INI_SCAN_DIR` en waarde`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="81611-145">Add an App Setting to your Web App with the key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
2. <span data-ttu-id="81611-146">Maak een `settings.ini` bestand met behulp van de Kudu-Console (http://&lt;-sitenaam&gt;. scm.azurewebsite.net) in de `d:\home\site\ini` directory.</span><span class="sxs-lookup"><span data-stu-id="81611-146">Create an `settings.ini` file using Kudu Console (http://&lt;site-name&gt;.scm.azurewebsite.net) in the `d:\home\site\ini` directory.</span></span>
3. <span data-ttu-id="81611-147">Configuratieinstellingen toevoegen aan de `settings.ini` bestand met dezelfde syntaxis als u wilt gebruiken in een bestand php.ini.</span><span class="sxs-lookup"><span data-stu-id="81611-147">Add configuration settings to the `settings.ini` file using the same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="81611-148">Bijvoorbeeld, als u deze wilde wijst de `curl.cainfo` instellen voor een `*.crt` bestands- en instellen 'wincache.maxfilesize' tot 512 kB uw `settings.ini` bestand zou deze tekst bevatten:</span><span class="sxs-lookup"><span data-stu-id="81611-148">For example, if you wanted to point the `curl.cainfo` setting to a `*.crt` file and set 'wincache.maxfilesize' setting to 512K, your `settings.ini` file would contain this text:</span></span>
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. <span data-ttu-id="81611-149">Uw Web-App voor het laden van de wijzigingen opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="81611-149">Restart your Web App to load the changes.</span></span>

## <a name="how-to-enable-extensions-in-the-default-php-runtime"></a><span data-ttu-id="81611-150">Hoe: uitbreidingen in de standaard PHP-runtime inschakelen</span><span class="sxs-lookup"><span data-stu-id="81611-150">How to: Enable extensions in the default PHP runtime</span></span>
<span data-ttu-id="81611-151">Zoals beschreven in de vorige sectie, de beste manier om de standaard PHP-versie, de standaardconfiguratie en de extensies ingeschakeld is voor het implementeren van een script dat roept [phpinfo()].</span><span class="sxs-lookup"><span data-stu-id="81611-151">As noted in the previous section, the best way to see the default PHP version, its default configuration, and the enabled extensions is to deploy a script that calls [phpinfo()].</span></span> <span data-ttu-id="81611-152">Volg de onderstaande stappen zodat de aanvullende extensies:</span><span class="sxs-lookup"><span data-stu-id="81611-152">To enable additional extensions, follow the steps below:</span></span>

### <a name="configure-via-ini-settings"></a><span data-ttu-id="81611-153">Via ini-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="81611-153">Configure via ini settings</span></span>
1. <span data-ttu-id="81611-154">Voeg een `ext` map naar de `d:\home\site` directory.</span><span class="sxs-lookup"><span data-stu-id="81611-154">Add a `ext` directory to the `d:\home\site` directory.</span></span>
2. <span data-ttu-id="81611-155">Plaatsen `.dll` extensie bestanden in de `ext` directory (bijvoorbeeld `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="81611-155">Put `.dll` extension files in the `ext` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="81611-156">Zorg ervoor dat de extensies compatibel is met de standaardversie van PHP en zijn VC9 en niet-thread-safe (nts) compatibel zijn.</span><span class="sxs-lookup"><span data-stu-id="81611-156">Make sure that the extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="81611-157">Een App-instelling toevoegen aan uw Web-App met de sleutel `PHP_INI_SCAN_DIR` en waarde`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="81611-157">Add an App Setting to your Web App with the key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
4. <span data-ttu-id="81611-158">Maak een `ini` bestanden per `d:\home\site\ini` aangeroepen `extensions.ini`.</span><span class="sxs-lookup"><span data-stu-id="81611-158">Create an `ini` file in `d:\home\site\ini` called `extensions.ini`.</span></span>
5. <span data-ttu-id="81611-159">Configuratieinstellingen toevoegen aan de `extensions.ini` bestand met dezelfde syntaxis als u wilt gebruiken in een bestand php.ini.</span><span class="sxs-lookup"><span data-stu-id="81611-159">Add configuration settings to the `extensions.ini` file using the same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="81611-160">Bijvoorbeeld, als u wilt inschakelen van de extensies MongoDB en XDebug uw `extensions.ini` bestand zou deze tekst bevatten:</span><span class="sxs-lookup"><span data-stu-id="81611-160">For example, if you wanted to enable the MongoDB and XDebug extensions, your `extensions.ini` file would contain this text:</span></span>
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. <span data-ttu-id="81611-161">Uw Web-App voor het laden van de wijzigingen opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="81611-161">Restart your Web App to load the changes.</span></span>

### <a name="configure-via-app-setting"></a><span data-ttu-id="81611-162">Via App-instelling configureren</span><span class="sxs-lookup"><span data-stu-id="81611-162">Configure via App Setting</span></span>
1. <span data-ttu-id="81611-163">Voeg een `bin` map naar de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="81611-163">Add a `bin` directory to the root directory.</span></span>
2. <span data-ttu-id="81611-164">Plaatsen `.dll` extensie bestanden in de `bin` directory (bijvoorbeeld `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="81611-164">Put `.dll` extension files in the `bin` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="81611-165">Zorg ervoor dat de extensies compatibel is met de standaardversie van PHP en zijn VC9 en niet-thread-safe (nts) compatibel zijn.</span><span class="sxs-lookup"><span data-stu-id="81611-165">Make sure that the extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="81611-166">Implementeer uw web-app.</span><span class="sxs-lookup"><span data-stu-id="81611-166">Deploy your web app.</span></span>
4. <span data-ttu-id="81611-167">Blader naar uw web-app in de Azure Portal en klik op de **instellingen** knop.</span><span class="sxs-lookup"><span data-stu-id="81611-167">Browse to your web app in the Azure Portal and click on the **Settings** button.</span></span>
   
    ![Instellingen voor Web-App][settings-button]
5. <span data-ttu-id="81611-169">Van de **instellingen** blade Selecteer **toepassingsinstellingen** en schuif naar de **appinstellingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="81611-169">From the **Settings** blade select **Application Settings** and scroll to the **App settings** section.</span></span>
6. <span data-ttu-id="81611-170">In de **appinstellingen** sectie, maakt u een **PHP_EXTENSIONS** sleutel.</span><span class="sxs-lookup"><span data-stu-id="81611-170">In the **App settings** section, create a **PHP_EXTENSIONS** key.</span></span> <span data-ttu-id="81611-171">De waarde voor deze sleutel wordt een pad relatief ten opzichte van hoofdmap website: **bin\your-ext-file**.</span><span class="sxs-lookup"><span data-stu-id="81611-171">The value for this key would be a path relative to website root: **bin\your-ext-file**.</span></span>
   
    ![De extensie in de app-instellingen inschakelen][php-extensions]
7. <span data-ttu-id="81611-173">Klik op de **opslaan** knop aan de bovenkant van de **Web-appinstellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="81611-173">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![Configuratie-instellingen opslaan][save-button]

<span data-ttu-id="81611-175">Zend extensies worden ook ondersteund met behulp van een **PHP_ZENDEXTENSIONS** sleutel.</span><span class="sxs-lookup"><span data-stu-id="81611-175">Zend extensions are also supported by using a **PHP_ZENDEXTENSIONS** key.</span></span> <span data-ttu-id="81611-176">Zodat meerdere extensies bevatten een door komma's gescheiden lijst met `.dll` bestanden voor de waarde van de app-instelling.</span><span class="sxs-lookup"><span data-stu-id="81611-176">To enable multiple extensions, include a comma-separated list of `.dll` files for the app setting value.</span></span>

## <a name="how-to-use-a-custom-php-runtime"></a><span data-ttu-id="81611-177">Procedure: een aangepaste PHP-runtime gebruiken</span><span class="sxs-lookup"><span data-stu-id="81611-177">How to: Use a custom PHP runtime</span></span>
<span data-ttu-id="81611-178">App Service Web Apps kunt een PHP-runtime die u opgeeft voor het uitvoeren van PHP-scripts gebruiken in plaats van de standaard PHP-runtime.</span><span class="sxs-lookup"><span data-stu-id="81611-178">Instead of the default PHP runtime, App Service Web Apps can use a PHP runtime that you provide to execute PHP scripts.</span></span> <span data-ttu-id="81611-179">De runtime die u opgeeft, kan worden geconfigureerd met een `php.ini` -bestand dat u ook opgeven.</span><span class="sxs-lookup"><span data-stu-id="81611-179">The runtime that you provide can be configured by a `php.ini` file that you also provide.</span></span> <span data-ttu-id="81611-180">Voor het gebruik van een aangepaste PHP-runtime met Web-Apps, de volgende stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="81611-180">To use a custom PHP runtime with Web Apps, follow the steps below.</span></span>

1. <span data-ttu-id="81611-181">Verkrijgen van een niet-thread-safe, VC9 of VC11 compatibele versie van PHP voor Windows.</span><span class="sxs-lookup"><span data-stu-id="81611-181">Obtain a non-thread-safe, VC9 or VC11 compatible version of PHP for Windows.</span></span> <span data-ttu-id="81611-182">Recente versies van PHP voor Windows vindt u hier: [http://windows.php.net/download/].</span><span class="sxs-lookup"><span data-stu-id="81611-182">Recent releases of PHP for Windows can be found here: [http://windows.php.net/download/].</span></span> <span data-ttu-id="81611-183">Oudere versies vindt u in het archief hier: [http://windows.php.net/downloads/releases/archives/].</span><span class="sxs-lookup"><span data-stu-id="81611-183">Older releases can be found in the archive here: [http://windows.php.net/downloads/releases/archives/].</span></span>
2. <span data-ttu-id="81611-184">Wijzig de `php.ini` -bestand voor de runtime.</span><span class="sxs-lookup"><span data-stu-id="81611-184">Modify the `php.ini` file for your runtime.</span></span> <span data-ttu-id="81611-185">Houd er rekening mee dat alle configuratieinstellingen die systeem-niveau-only richtlijnen worden genegeerd door de Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="81611-185">Note that any configuration settings that are system-level-only directives will be ignored by Web Apps.</span></span> <span data-ttu-id="81611-186">(Zie voor meer informatie over system-niveau-only richtlijnen [lijst van php.ini richtlijnen]).</span><span class="sxs-lookup"><span data-stu-id="81611-186">(For information about system-level-only directives, see [List of php.ini directives]).</span></span>
3. <span data-ttu-id="81611-187">Eventueel extensies toevoegen aan uw PHP-runtime en inschakelen in de `php.ini` bestand.</span><span class="sxs-lookup"><span data-stu-id="81611-187">Optionally, add extensions to your PHP runtime and enable them in the `php.ini` file.</span></span>
4. <span data-ttu-id="81611-188">Voeg een `bin` tot uw hoofdmap en de opslag van de map waarin uw PHP-runtime in deze map (bijvoorbeeld `bin\php`).</span><span class="sxs-lookup"><span data-stu-id="81611-188">Add a `bin` directory to your root directory, and put the directory that contains your PHP runtime in it (for example, `bin\php`).</span></span>
5. <span data-ttu-id="81611-189">Implementeer uw web-app.</span><span class="sxs-lookup"><span data-stu-id="81611-189">Deploy your web app.</span></span>
6. <span data-ttu-id="81611-190">Blader naar uw web-app in de Azure Portal en klik op de **instellingen** knop.</span><span class="sxs-lookup"><span data-stu-id="81611-190">Browse to your web app in the Azure Portal and click on the **Settings** button.</span></span>
   
    ![Instellingen voor Web-App][settings-button]
7. <span data-ttu-id="81611-192">Van de **instellingen** blade Selecteer **toepassingsinstellingen** en schuif naar de **Handlertoewijzingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="81611-192">From the **Settings** blade select **Application Settings** and scroll to the **Handler mappings** section.</span></span> <span data-ttu-id="81611-193">Voeg `*.php` veld naar de extensie en voeg het pad naar de `php-cgi.exe` uitvoerbare.</span><span class="sxs-lookup"><span data-stu-id="81611-193">Add `*.php` to the Extension field and add the path to the `php-cgi.exe` executable.</span></span> <span data-ttu-id="81611-194">Als u uw PHP-runtime in de `bin` directory in de hoofdmap van uw toepassing, het pad moet `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span><span class="sxs-lookup"><span data-stu-id="81611-194">If you put your PHP runtime in the `bin` directory in the root of you application, the path will be `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span></span>
   
    ![Handler in lijnhandler toewijzingen opgeven][handler-mappings]
8. <span data-ttu-id="81611-196">Klik op de **opslaan** knop aan de bovenkant van de **Web-appinstellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="81611-196">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![Configuratie-instellingen opslaan][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a><span data-ttu-id="81611-198">Hoe: Composer automatiseren met behulp van Azure</span><span class="sxs-lookup"><span data-stu-id="81611-198">How to: Enable Composer automation in Azure</span></span>
<span data-ttu-id="81611-199">Standaard geen App Service reactie met composer.json, als u in uw PHP-project hebt.</span><span class="sxs-lookup"><span data-stu-id="81611-199">By default, App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="81611-200">Als u [Git-implementatie](app-service-deploy-local-git.md), kunt u composer.json tijdens de verwerking inschakelen `git push` doordat de Composer-extensie.</span><span class="sxs-lookup"><span data-stu-id="81611-200">If you use [Git deployment](app-service-deploy-local-git.md), you can enable composer.json processing during `git push` by enabling the Composer extension.</span></span>

> [!NOTE]
> <span data-ttu-id="81611-201">U kunt [stem voor uitstekende Composer ondersteuning in App Service hier](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span><span class="sxs-lookup"><span data-stu-id="81611-201">You can [vote for first-class Composer support in App Service here](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span></span>
> 
> 

1. <span data-ttu-id="81611-202">In uw PHP web-app blade in de [Azure-portal](https://portal.azure.com), klikt u op **extra** > **extensies**.</span><span class="sxs-lookup"><span data-stu-id="81611-202">In your PHP web app's blade in the [Azure portal](https://portal.azure.com), click **Tools** > **Extensions**.</span></span>
   
    ![Azure Portal instellingenblade Composer automatiseren met behulp van Azure inschakelen](./media/web-sites-php-configure/composer-extension-settings.png)
2. <span data-ttu-id="81611-204">Klik op **toevoegen**, klikt u vervolgens op **Composer**.</span><span class="sxs-lookup"><span data-stu-id="81611-204">Click **Add**, then click **Composer**.</span></span>
   
    ![Als u wilt Composer automatiseren met behulp van Azure Composer-extensie toevoegen](./media/web-sites-php-configure/composer-extension-add.png)
3. <span data-ttu-id="81611-206">Klik op **OK** juridische voorwaarden accepteren.</span><span class="sxs-lookup"><span data-stu-id="81611-206">Click **OK** to accept legal terms.</span></span> <span data-ttu-id="81611-207">Klik op **OK** om opnieuw toe te voegen van de extensie.</span><span class="sxs-lookup"><span data-stu-id="81611-207">Click **OK** again to add the extension.</span></span>
   
    <span data-ttu-id="81611-208">De **extensies geïnstalleerd** blade ziet nu de Composer-extensie.</span><span class="sxs-lookup"><span data-stu-id="81611-208">The **Installed extensions** blade will now show the Composer extension.</span></span>  
    <span data-ttu-id="81611-209">![Accepteer de juridische voorwaarden om in te schakelen Composer automatiseren met behulp van Azure](./media/web-sites-php-configure/composer-extension-view.png)</span><span class="sxs-lookup"><span data-stu-id="81611-209">![Accept legal terms to enable Composer automation in Azure](./media/web-sites-php-configure/composer-extension-view.png)</span></span>
4. <span data-ttu-id="81611-210">Nu uitvoeren `git add`, `git commit`, en `git push` zoals in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="81611-210">Now, perform `git add`, `git commit`, and `git push` like in the previous section.</span></span> <span data-ttu-id="81611-211">Nu ziet u dat Composer afhankelijkheden die zijn gedefinieerd in composer.json wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="81611-211">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![GIT-implementatie met Composer automatiseren met behulp van Azure](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a><span data-ttu-id="81611-213">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="81611-213">Next steps</span></span>
<span data-ttu-id="81611-214">Zie voor meer informatie de [PHP-ontwikkelaarscentrum](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="81611-214">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

> [!NOTE]
> <span data-ttu-id="81611-215">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="81611-215">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="81611-216">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="81611-216">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="81611-217">[gratis proefversie]: https://www.windowsazure.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="81611-217">[free trial]: https://www.windowsazure.com/pricing/free-trial/</span></span>
<span data-ttu-id="81611-218">[phpinfo()]: http://php.net/manual/en/function.phpinfo.php</span><span class="sxs-lookup"><span data-stu-id="81611-218">[phpinfo()]: http://php.net/manual/en/function.phpinfo.php</span></span>
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
<span data-ttu-id="81611-219">[lijst van php.ini richtlijnen]: http://www.php.net/manual/en/ini.list.php</span><span class="sxs-lookup"><span data-stu-id="81611-219">[List of php.ini directives]: http://www.php.net/manual/en/ini.list.php</span></span>
<span data-ttu-id="81611-220">[. user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php</span><span class="sxs-lookup"><span data-stu-id="81611-220">[.user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php</span></span>
<span data-ttu-id="81611-221">[ini_set()]: http://www.php.net/manual/en/function.ini-set.php</span><span class="sxs-lookup"><span data-stu-id="81611-221">[ini_set()]: http://www.php.net/manual/en/function.ini-set.php</span></span>
[application-settings]: ./media/web-sites-php-configure/application-settings.png
[settings-button]: ./media/web-sites-php-configure/settings-button.png
[save-button]: ./media/web-sites-php-configure/save-button.png
[php-extensions]: ./media/web-sites-php-configure/php-extensions.png
[handler-mappings]: ./media/web-sites-php-configure/handler-mappings.png
<span data-ttu-id="81611-222">[http://windows.php.net/download/]: http://windows.php.net/download/</span><span class="sxs-lookup"><span data-stu-id="81611-222">[http://windows.php.net/download/]: http://windows.php.net/download/</span></span>
<span data-ttu-id="81611-223">[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/</span><span class="sxs-lookup"><span data-stu-id="81611-223">[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/</span></span>
[SETPHPVERCLI]: ./media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: ./media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: ./media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: ./media/web-sites-php-configure/ShowPHPVersion-PS.png

