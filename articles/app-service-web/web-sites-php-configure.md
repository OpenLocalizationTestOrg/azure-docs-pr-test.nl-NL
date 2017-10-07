---
title: aaaConfigure PHP in Azure App Service Web Apps | Microsoft Docs
description: Informatie over hoe tooconfigure Hallo standaard PHP-installatie of een aangepaste PHP-installatie voor Web-Apps in Azure App Service toevoegen.
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
ms.openlocfilehash: 2e461e4a269a4ce5614f5f05560f38bc53066251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-php-in-azure-app-service-web-apps"></a><span data-ttu-id="812c4-103">PHP configureren in Azure App Service WebApps</span><span class="sxs-lookup"><span data-stu-id="812c4-103">Configure PHP in Azure App Service Web Apps</span></span>
## <a name="introduction"></a><span data-ttu-id="812c4-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="812c4-104">Introduction</span></span>
<span data-ttu-id="812c4-105">Deze handleiding leert u hoe tooconfigure ingebouwde PHP-runtime voor Web-Apps in Hallo [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), geeft u een aangepaste PHP-runtime en uitbreidingen inschakelen.</span><span class="sxs-lookup"><span data-stu-id="812c4-105">This guide will show you how tooconfigure hello built-in PHP runtime for Web Apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), provide a custom PHP runtime, and enable extensions.</span></span> <span data-ttu-id="812c4-106">App Service toouse zich aanmelden voor Hallo [gratis proefversie].</span><span class="sxs-lookup"><span data-stu-id="812c4-106">toouse App Service, sign up for hello [free trial].</span></span> <span data-ttu-id="812c4-107">tooget hello meest van deze handleiding, u moet eerst een PHP-web-app in App Service maken.</span><span class="sxs-lookup"><span data-stu-id="812c4-107">tooget hello most from this guide, you should first create a PHP web app in App Service.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-hello-built-in-php-version"></a><span data-ttu-id="812c4-108">Hoe: wijziging Hallo ingebouwde PHP-versie</span><span class="sxs-lookup"><span data-stu-id="812c4-108">How to: Change hello built-in PHP version</span></span>
<span data-ttu-id="812c4-109">Standaard is PHP 5.5 geïnstalleerd en onmiddellijk beschikbaar voor gebruik bij het maken van een App Service-web-app.</span><span class="sxs-lookup"><span data-stu-id="812c4-109">By default, PHP 5.5 is installed and immediately available for use when you create an App Service web app.</span></span> <span data-ttu-id="812c4-110">Hallo van de beste manier toosee Hallo beschikbare versie revisie, de standaardconfiguratie en hello ingeschakelde extensies is toodeploy een script dat Hallo roept [phpinfo()] functie.</span><span class="sxs-lookup"><span data-stu-id="812c4-110">hello best way toosee hello available release revision, its default configuration, and hello enabled extensions is toodeploy a script that calls hello [phpinfo()] function.</span></span>

<span data-ttu-id="812c4-111">De versies van PHP 5.6 en PHP 7.0 zijn ook beschikbaar, maar niet standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="812c4-111">PHP 5.6 and PHP 7.0 versions are also available, but not enabled by default.</span></span> <span data-ttu-id="812c4-112">tooupdate hello PHP-versie, volg een van deze methoden:</span><span class="sxs-lookup"><span data-stu-id="812c4-112">tooupdate hello PHP version, follow one of these methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="812c4-113">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="812c4-113">Azure Portal</span></span>
1. <span data-ttu-id="812c4-114">Blader tooyour web-app in Hallo [Azure Portal](https://portal.azure.com) en klik op Hallo **instellingen** knop.</span><span class="sxs-lookup"><span data-stu-id="812c4-114">Browse tooyour web app in hello [Azure Portal](https://portal.azure.com) and click on hello **Settings** button.</span></span>
   
    ![Instellingen voor Web-App][settings-button]
2. <span data-ttu-id="812c4-116">Van Hallo **instellingen** blade Selecteer **toepassingsinstellingen** en kiest u Hallo nieuwe PHP-versie.</span><span class="sxs-lookup"><span data-stu-id="812c4-116">From hello **Settings** blade select **Application Settings** and choose hello new PHP version.</span></span>
   
    ![Toepassingsinstellingen][application-settings]
3. <span data-ttu-id="812c4-118">Klik op Hallo **opslaan** knop bovenaan Hallo Hallo **Web-appinstellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="812c4-118">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Configuratie-instellingen opslaan][save-button]

### <a name="azure-powershell-windows"></a><span data-ttu-id="812c4-120">Azure PowerShell (Windows)</span><span class="sxs-lookup"><span data-stu-id="812c4-120">Azure PowerShell (Windows)</span></span>
1. <span data-ttu-id="812c4-121">Open Azure PowerShell en tooyour aanmeldingsaccount:</span><span class="sxs-lookup"><span data-stu-id="812c4-121">Open Azure PowerShell, and login tooyour account:</span></span>
   
        PS C:\> Login-AzureRmAccount
2. <span data-ttu-id="812c4-122">Hallo PHP-versie voor Hallo web-app ingesteld.</span><span class="sxs-lookup"><span data-stu-id="812c4-122">Set hello PHP version for hello web app.</span></span>
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. <span data-ttu-id="812c4-123">Hallo PHP-versie is nu ingesteld.</span><span class="sxs-lookup"><span data-stu-id="812c4-123">hello PHP version is now set.</span></span> <span data-ttu-id="812c4-124">U kunt deze instellingen controleren:</span><span class="sxs-lookup"><span data-stu-id="812c4-124">You can confirm these settings:</span></span>
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a><span data-ttu-id="812c4-125">Azure-opdrachtregelinterface (Linux, Mac, Windows)</span><span class="sxs-lookup"><span data-stu-id="812c4-125">Azure Command-Line Interface (Linux, Mac, Windows)</span></span>
<span data-ttu-id="812c4-126">toouse hello Azure opdrachtregel-Interface, moet u hebben **Node.js** op uw computer geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="812c4-126">toouse hello Azure Command-Line Interface, you must have **Node.js** installed on your computer.</span></span>

1. <span data-ttu-id="812c4-127">Open de Terminal en tooyour aanmeldingsaccount.</span><span class="sxs-lookup"><span data-stu-id="812c4-127">Open Terminal, and login tooyour account.</span></span>
   
        azure login
2. <span data-ttu-id="812c4-128">Hallo PHP-versie voor Hallo web-app ingesteld.</span><span class="sxs-lookup"><span data-stu-id="812c4-128">Set hello PHP version for hello web app.</span></span>
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. <span data-ttu-id="812c4-129">Hallo PHP-versie is nu ingesteld.</span><span class="sxs-lookup"><span data-stu-id="812c4-129">hello PHP version is now set.</span></span> <span data-ttu-id="812c4-130">U kunt deze instellingen controleren:</span><span class="sxs-lookup"><span data-stu-id="812c4-130">You can confirm these settings:</span></span>
   
        azure site show {app-name}

> [!NOTE] 
> <span data-ttu-id="812c4-131">Hallo [Azure CLI 2.0](https://github.com/Azure/azure-cli) opdrachten equivalent toohello bovenstaande zijn zijn:</span><span class="sxs-lookup"><span data-stu-id="812c4-131">hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands that are equivalent toohello above are:</span></span>
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-hello-built-in-php-configurations"></a><span data-ttu-id="812c4-132">Procedure: ingebouwde PHP-configuraties Hallo wijzigen</span><span class="sxs-lookup"><span data-stu-id="812c4-132">How to: Change hello built-in PHP configurations</span></span>
<span data-ttu-id="812c4-133">Voor een ingebouwde PHP-runtime kunt u Hallo configuratieopties door Hallo onderstaande stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="812c4-133">For any built-in PHP runtime, you can change any of hello configuration options by following hello steps below.</span></span> <span data-ttu-id="812c4-134">(Zie voor meer informatie over richtlijnen php.ini [lijst van php.ini richtlijnen].)</span><span class="sxs-lookup"><span data-stu-id="812c4-134">(For information about php.ini directives, see [List of php.ini directives].)</span></span>

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a><span data-ttu-id="812c4-135">Het wijzigen van PHP\_INI\_gebruiker, PHP\_INI\_PERDIR, PHP\_INI\_alle configuratie-instellingen</span><span class="sxs-lookup"><span data-stu-id="812c4-135">Changing PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL configuration settings</span></span>
1. <span data-ttu-id="812c4-136">Voeg een [. user.ini] bestand tooyour-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="812c4-136">Add a [.user.ini] file tooyour root directory.</span></span>
2. <span data-ttu-id="812c4-137">Toevoegen van configuratie-instellingen toohello `.user.ini` met behulp van het bestand Hallo dezelfde syntaxis die u wilt gebruiken in een `php.ini` bestand.</span><span class="sxs-lookup"><span data-stu-id="812c4-137">Add configuration settings toohello `.user.ini` file using hello same syntax you would use in a `php.ini` file.</span></span> <span data-ttu-id="812c4-138">Bijvoorbeeld, als u deze wilde tooturn hello `display_errors` instelling Stel `upload_max_filesize` too10M, instellen van uw `.user.ini` bestand zou deze tekst bevatten:</span><span class="sxs-lookup"><span data-stu-id="812c4-138">For example, if you wanted tooturn hello `display_errors` setting on and set `upload_max_filesize` setting too10M, your `.user.ini` file would contain this text:</span></span>
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on toowrite errors tood:\home\LogFiles\php_errors.log
        ; log_errors=On
3. <span data-ttu-id="812c4-139">Implementeer uw web-app.</span><span class="sxs-lookup"><span data-stu-id="812c4-139">Deploy your web app.</span></span>
4. <span data-ttu-id="812c4-140">Opnieuw opstarten Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="812c4-140">Restart hello web app.</span></span> <span data-ttu-id="812c4-141">(Opnieuw opstarten is nodig omdat Hallo frequentie met welke PHP leest `.user.ini` bestanden wordt bepaald door Hallo `user_ini.cache_ttl` instelling, die is een systeemniveau-instelling en 300 seconden (5 minuten) is standaard.</span><span class="sxs-lookup"><span data-stu-id="812c4-141">(Restarting is necessary because hello frequency with which PHP reads `.user.ini` files is governed by hello `user_ini.cache_ttl` setting, which is a system level setting and is 300 seconds (5 minutes) by default.</span></span> <span data-ttu-id="812c4-142">Opnieuw te starten Hallo web-app forceert PHP tooread Hallo nieuwe instellingen in het Hallo `.user.ini` bestand.)</span><span class="sxs-lookup"><span data-stu-id="812c4-142">Restarting hello web app forces PHP tooread hello new settings in hello `.user.ini` file.)</span></span>

<span data-ttu-id="812c4-143">Als een alternatieve toousing een `.user.ini` -bestand, kunt u Hallo [ini_set()] functie in scripts tooset configuratieopties die niet op systeemniveau richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="812c4-143">As an alternative toousing a `.user.ini` file, you can use hello [ini_set()] function in scripts tooset configuration options that are not system-level directives.</span></span>

### <a name="changing-phpinisystem-configuration-settings"></a><span data-ttu-id="812c4-144">Het wijzigen van PHP\_INI\_SYSTEM configuratie-instellingen</span><span class="sxs-lookup"><span data-stu-id="812c4-144">Changing PHP\_INI\_SYSTEM configuration settings</span></span>
1. <span data-ttu-id="812c4-145">Toevoegen van een App-instelling tooyour Web-App met Hallo sleutel `PHP_INI_SCAN_DIR` en waarde`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="812c4-145">Add an App Setting tooyour Web App with hello key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
2. <span data-ttu-id="812c4-146">Maak een `settings.ini` bestand met behulp van de Kudu-Console (http://&lt;-sitenaam&gt;. scm.azurewebsite.net) in Hallo `d:\home\site\ini` directory.</span><span class="sxs-lookup"><span data-stu-id="812c4-146">Create an `settings.ini` file using Kudu Console (http://&lt;site-name&gt;.scm.azurewebsite.net) in hello `d:\home\site\ini` directory.</span></span>
3. <span data-ttu-id="812c4-147">Toevoegen van configuratie-instellingen toohello `settings.ini` bestand met dezelfde syntaxis die u in een bestand php.ini gebruiken wilt Hallo.</span><span class="sxs-lookup"><span data-stu-id="812c4-147">Add configuration settings toohello `settings.ini` file using hello same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="812c4-148">Bijvoorbeeld, als u deze wilde toopoint hello `curl.cainfo` instelling tooa `*.crt` bestands- en wincache.maxfilesize instelling too512K, stel uw `settings.ini` bestand zou deze tekst bevatten:</span><span class="sxs-lookup"><span data-stu-id="812c4-148">For example, if you wanted toopoint hello `curl.cainfo` setting tooa `*.crt` file and set 'wincache.maxfilesize' setting too512K, your `settings.ini` file would contain this text:</span></span>
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. <span data-ttu-id="812c4-149">Start opnieuw op uw Web-App tooload Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="812c4-149">Restart your Web App tooload hello changes.</span></span>

## <a name="how-to-enable-extensions-in-hello-default-php-runtime"></a><span data-ttu-id="812c4-150">Hoe: uitbreidingen in Hallo standaard PHP-runtime inschakelen</span><span class="sxs-lookup"><span data-stu-id="812c4-150">How to: Enable extensions in hello default PHP runtime</span></span>
<span data-ttu-id="812c4-151">Zoals vermeld in de vorige sectie hello, Hallo aanbevolen manier toosee Hallo standaard PHP-versie, de standaardconfiguratie en Hallo ingeschakeld extensies toodeploy een script dat roept is [phpinfo()].</span><span class="sxs-lookup"><span data-stu-id="812c4-151">As noted in hello previous section, hello best way toosee hello default PHP version, its default configuration, and hello enabled extensions is toodeploy a script that calls [phpinfo()].</span></span> <span data-ttu-id="812c4-152">Extra extensies tooenable, stappen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="812c4-152">tooenable additional extensions, follow hello steps below:</span></span>

### <a name="configure-via-ini-settings"></a><span data-ttu-id="812c4-153">Via ini-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="812c4-153">Configure via ini settings</span></span>
1. <span data-ttu-id="812c4-154">Voeg een `ext` directory toohello `d:\home\site` directory.</span><span class="sxs-lookup"><span data-stu-id="812c4-154">Add a `ext` directory toohello `d:\home\site` directory.</span></span>
2. <span data-ttu-id="812c4-155">Plaatsen `.dll` extensiebestanden in Hallo `ext` directory (bijvoorbeeld `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="812c4-155">Put `.dll` extension files in hello `ext` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="812c4-156">Zorg ervoor dat de Hallo extensies compatibel is met de standaardversie van PHP en zijn VC9 en niet-thread-safe (nts) compatibel zijn.</span><span class="sxs-lookup"><span data-stu-id="812c4-156">Make sure that hello extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="812c4-157">Toevoegen van een App-instelling tooyour Web-App met Hallo sleutel `PHP_INI_SCAN_DIR` en waarde`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="812c4-157">Add an App Setting tooyour Web App with hello key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
4. <span data-ttu-id="812c4-158">Maak een `ini` bestanden per `d:\home\site\ini` aangeroepen `extensions.ini`.</span><span class="sxs-lookup"><span data-stu-id="812c4-158">Create an `ini` file in `d:\home\site\ini` called `extensions.ini`.</span></span>
5. <span data-ttu-id="812c4-159">Toevoegen van configuratie-instellingen toohello `extensions.ini` bestand met dezelfde syntaxis die u in een bestand php.ini gebruiken wilt Hallo.</span><span class="sxs-lookup"><span data-stu-id="812c4-159">Add configuration settings toohello `extensions.ini` file using hello same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="812c4-160">Als u deze wilde tooenable hello MongoDB en XDebug-extensies, bijvoorbeeld uw `extensions.ini` bestand zou deze tekst bevatten:</span><span class="sxs-lookup"><span data-stu-id="812c4-160">For example, if you wanted tooenable hello MongoDB and XDebug extensions, your `extensions.ini` file would contain this text:</span></span>
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. <span data-ttu-id="812c4-161">Start opnieuw op uw Web-App tooload Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="812c4-161">Restart your Web App tooload hello changes.</span></span>

### <a name="configure-via-app-setting"></a><span data-ttu-id="812c4-162">Via App-instelling configureren</span><span class="sxs-lookup"><span data-stu-id="812c4-162">Configure via App Setting</span></span>
1. <span data-ttu-id="812c4-163">Voeg een `bin` directory toohello-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="812c4-163">Add a `bin` directory toohello root directory.</span></span>
2. <span data-ttu-id="812c4-164">Plaatsen `.dll` extensiebestanden in Hallo `bin` directory (bijvoorbeeld `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="812c4-164">Put `.dll` extension files in hello `bin` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="812c4-165">Zorg ervoor dat de Hallo extensies compatibel is met de standaardversie van PHP en zijn VC9 en niet-thread-safe (nts) compatibel zijn.</span><span class="sxs-lookup"><span data-stu-id="812c4-165">Make sure that hello extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="812c4-166">Implementeer uw web-app.</span><span class="sxs-lookup"><span data-stu-id="812c4-166">Deploy your web app.</span></span>
4. <span data-ttu-id="812c4-167">Tooyour web-app in hello Azure Portal bladeren en klik op Hallo **instellingen** knop.</span><span class="sxs-lookup"><span data-stu-id="812c4-167">Browse tooyour web app in hello Azure Portal and click on hello **Settings** button.</span></span>
   
    ![Instellingen voor Web-App][settings-button]
5. <span data-ttu-id="812c4-169">Van Hallo **instellingen** blade Selecteer **toepassingsinstellingen** en schuif toohello **appinstellingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="812c4-169">From hello **Settings** blade select **Application Settings** and scroll toohello **App settings** section.</span></span>
6. <span data-ttu-id="812c4-170">In Hallo **appinstellingen** sectie, maakt u een **PHP_EXTENSIONS** sleutel.</span><span class="sxs-lookup"><span data-stu-id="812c4-170">In hello **App settings** section, create a **PHP_EXTENSIONS** key.</span></span> <span data-ttu-id="812c4-171">Hallo-waarde voor deze sleutel wordt de hoofdmap van een pad relatief toowebsite: **bin\your-ext-file**.</span><span class="sxs-lookup"><span data-stu-id="812c4-171">hello value for this key would be a path relative toowebsite root: **bin\your-ext-file**.</span></span>
   
    ![De extensie in de app-instellingen inschakelen][php-extensions]
7. <span data-ttu-id="812c4-173">Klik op Hallo **opslaan** knop bovenaan Hallo Hallo **Web-appinstellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="812c4-173">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Configuratie-instellingen opslaan][save-button]

<span data-ttu-id="812c4-175">Zend extensies worden ook ondersteund met behulp van een **PHP_ZENDEXTENSIONS** sleutel.</span><span class="sxs-lookup"><span data-stu-id="812c4-175">Zend extensions are also supported by using a **PHP_ZENDEXTENSIONS** key.</span></span> <span data-ttu-id="812c4-176">tooenable meerdere extensies bevatten een door komma's gescheiden lijst met `.dll` bestanden voor de waarde van de instelling app Hallo.</span><span class="sxs-lookup"><span data-stu-id="812c4-176">tooenable multiple extensions, include a comma-separated list of `.dll` files for hello app setting value.</span></span>

## <a name="how-to-use-a-custom-php-runtime"></a><span data-ttu-id="812c4-177">Procedure: een aangepaste PHP-runtime gebruiken</span><span class="sxs-lookup"><span data-stu-id="812c4-177">How to: Use a custom PHP runtime</span></span>
<span data-ttu-id="812c4-178">App Service Web Apps kunt een PHP-runtime op te geven tooexecute PHP-scripts gebruiken in plaats van Hallo standaard PHP-runtime.</span><span class="sxs-lookup"><span data-stu-id="812c4-178">Instead of hello default PHP runtime, App Service Web Apps can use a PHP runtime that you provide tooexecute PHP scripts.</span></span> <span data-ttu-id="812c4-179">Hallo-runtime die u opgeeft, kan worden geconfigureerd met een `php.ini` -bestand dat u ook opgeven.</span><span class="sxs-lookup"><span data-stu-id="812c4-179">hello runtime that you provide can be configured by a `php.ini` file that you also provide.</span></span> <span data-ttu-id="812c4-180">een aangepaste PHP-runtime met Web-Apps toouse Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="812c4-180">toouse a custom PHP runtime with Web Apps, follow hello steps below.</span></span>

1. <span data-ttu-id="812c4-181">Verkrijgen van een niet-thread-safe, VC9 of VC11 compatibele versie van PHP voor Windows.</span><span class="sxs-lookup"><span data-stu-id="812c4-181">Obtain a non-thread-safe, VC9 or VC11 compatible version of PHP for Windows.</span></span> <span data-ttu-id="812c4-182">Recente versies van PHP voor Windows vindt u hier: [http://windows.php.net/download/].</span><span class="sxs-lookup"><span data-stu-id="812c4-182">Recent releases of PHP for Windows can be found here: [http://windows.php.net/download/].</span></span> <span data-ttu-id="812c4-183">Oudere versies kunnen u vinden in Hallo archief hier: [http://windows.php.net/downloads/releases/archives/].</span><span class="sxs-lookup"><span data-stu-id="812c4-183">Older releases can be found in hello archive here: [http://windows.php.net/downloads/releases/archives/].</span></span>
2. <span data-ttu-id="812c4-184">Hallo wijzigen `php.ini` -bestand voor de runtime.</span><span class="sxs-lookup"><span data-stu-id="812c4-184">Modify hello `php.ini` file for your runtime.</span></span> <span data-ttu-id="812c4-185">Houd er rekening mee dat alle configuratieinstellingen die systeem-niveau-only richtlijnen worden genegeerd door de Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="812c4-185">Note that any configuration settings that are system-level-only directives will be ignored by Web Apps.</span></span> <span data-ttu-id="812c4-186">(Zie voor meer informatie over system-niveau-only richtlijnen [lijst van php.ini richtlijnen]).</span><span class="sxs-lookup"><span data-stu-id="812c4-186">(For information about system-level-only directives, see [List of php.ini directives]).</span></span>
3. <span data-ttu-id="812c4-187">Eventueel extensies tooyour PHP-runtime toevoegen en ze inschakelen in Hallo `php.ini` bestand.</span><span class="sxs-lookup"><span data-stu-id="812c4-187">Optionally, add extensions tooyour PHP runtime and enable them in hello `php.ini` file.</span></span>
4. <span data-ttu-id="812c4-188">Voeg een `bin` directory tooyour-hoofdmap en put Hallo map waarin uw PHP-runtime erin (bijvoorbeeld `bin\php`).</span><span class="sxs-lookup"><span data-stu-id="812c4-188">Add a `bin` directory tooyour root directory, and put hello directory that contains your PHP runtime in it (for example, `bin\php`).</span></span>
5. <span data-ttu-id="812c4-189">Implementeer uw web-app.</span><span class="sxs-lookup"><span data-stu-id="812c4-189">Deploy your web app.</span></span>
6. <span data-ttu-id="812c4-190">Tooyour web-app in hello Azure Portal bladeren en klik op Hallo **instellingen** knop.</span><span class="sxs-lookup"><span data-stu-id="812c4-190">Browse tooyour web app in hello Azure Portal and click on hello **Settings** button.</span></span>
   
    ![Instellingen voor Web-App][settings-button]
7. <span data-ttu-id="812c4-192">Van Hallo **instellingen** blade Selecteer **toepassingsinstellingen** en schuif toohello **Handlertoewijzingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="812c4-192">From hello **Settings** blade select **Application Settings** and scroll toohello **Handler mappings** section.</span></span> <span data-ttu-id="812c4-193">Voeg `*.php` toohello extensie veld en voeg Hallo pad toohello `php-cgi.exe` uitvoerbare.</span><span class="sxs-lookup"><span data-stu-id="812c4-193">Add `*.php` toohello Extension field and add hello path toohello `php-cgi.exe` executable.</span></span> <span data-ttu-id="812c4-194">Als u uw PHP-runtime in Hallo `bin` directory in de hoofdmap van uw toepassing hello Hallo-pad moet `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span><span class="sxs-lookup"><span data-stu-id="812c4-194">If you put your PHP runtime in hello `bin` directory in hello root of you application, hello path will be `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span></span>
   
    ![Handler in lijnhandler toewijzingen opgeven][handler-mappings]
8. <span data-ttu-id="812c4-196">Klik op Hallo **opslaan** knop bovenaan Hallo Hallo **Web-appinstellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="812c4-196">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Configuratie-instellingen opslaan][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a><span data-ttu-id="812c4-198">Hoe: Composer automatiseren met behulp van Azure</span><span class="sxs-lookup"><span data-stu-id="812c4-198">How to: Enable Composer automation in Azure</span></span>
<span data-ttu-id="812c4-199">Standaard geen App Service reactie met composer.json, als u in uw PHP-project hebt.</span><span class="sxs-lookup"><span data-stu-id="812c4-199">By default, App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="812c4-200">Als u [Git-implementatie](app-service-deploy-local-git.md), kunt u composer.json tijdens de verwerking inschakelen `git push` doordat Hallo Composer-extensie.</span><span class="sxs-lookup"><span data-stu-id="812c4-200">If you use [Git deployment](app-service-deploy-local-git.md), you can enable composer.json processing during `git push` by enabling hello Composer extension.</span></span>

> [!NOTE]
> <span data-ttu-id="812c4-201">U kunt [stem voor uitstekende Composer ondersteuning in App Service hier](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span><span class="sxs-lookup"><span data-stu-id="812c4-201">You can [vote for first-class Composer support in App Service here](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span></span>
> 
> 

1. <span data-ttu-id="812c4-202">In uw PHP web-app blade in Hallo [Azure-portal](https://portal.azure.com), klikt u op **extra** > **extensies**.</span><span class="sxs-lookup"><span data-stu-id="812c4-202">In your PHP web app's blade in hello [Azure portal](https://portal.azure.com), click **Tools** > **Extensions**.</span></span>
   
    ![Azure Portal instellingen blade tooenable Composer automatiseren met behulp van Azure](./media/web-sites-php-configure/composer-extension-settings.png)
2. <span data-ttu-id="812c4-204">Klik op **toevoegen**, klikt u vervolgens op **Composer**.</span><span class="sxs-lookup"><span data-stu-id="812c4-204">Click **Add**, then click **Composer**.</span></span>
   
    ![Composer-extensie tooenable Composer automation toevoegen in Azure](./media/web-sites-php-configure/composer-extension-add.png)
3. <span data-ttu-id="812c4-206">Klik op **OK** tooaccept juridische voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="812c4-206">Click **OK** tooaccept legal terms.</span></span> <span data-ttu-id="812c4-207">Klik op **OK** opnieuw tooadd Hallo-extensie.</span><span class="sxs-lookup"><span data-stu-id="812c4-207">Click **OK** again tooadd hello extension.</span></span>
   
    <span data-ttu-id="812c4-208">Hallo **extensies geïnstalleerd** blade ziet nu Hallo Composer-extensie.</span><span class="sxs-lookup"><span data-stu-id="812c4-208">hello **Installed extensions** blade will now show hello Composer extension.</span></span>  
    <span data-ttu-id="812c4-209">![Accepteer de juridische voorwaarden tooenable Composer automatiseren met behulp van Azure](./media/web-sites-php-configure/composer-extension-view.png)</span><span class="sxs-lookup"><span data-stu-id="812c4-209">![Accept legal terms tooenable Composer automation in Azure](./media/web-sites-php-configure/composer-extension-view.png)</span></span>
4. <span data-ttu-id="812c4-210">Nu uitvoeren `git add`, `git commit`, en `git push` zoals in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="812c4-210">Now, perform `git add`, `git commit`, and `git push` like in hello previous section.</span></span> <span data-ttu-id="812c4-211">Nu ziet u dat Composer afhankelijkheden die zijn gedefinieerd in composer.json wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="812c4-211">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![GIT-implementatie met Composer automatiseren met behulp van Azure](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a><span data-ttu-id="812c4-213">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="812c4-213">Next steps</span></span>
<span data-ttu-id="812c4-214">Zie voor meer informatie, Hallo [PHP-ontwikkelaarscentrum](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="812c4-214">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

> [!NOTE]
> <span data-ttu-id="812c4-215">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="812c4-215">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="812c4-216">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="812c4-216">No credit cards required; no commitments.</span></span>
> 
> 

[gratis proefversie]: https://www.windowsazure.com/pricing/free-trial/
[phpinfo()]: http://php.net/manual/en/function.phpinfo.php
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
[lijst van php.ini richtlijnen]: http://www.php.net/manual/en/ini.list.php
[. user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php
[ini_set()]: http://www.php.net/manual/en/function.ini-set.php
[application-settings]: ./media/web-sites-php-configure/application-settings.png
[settings-button]: ./media/web-sites-php-configure/settings-button.png
[save-button]: ./media/web-sites-php-configure/save-button.png
[php-extensions]: ./media/web-sites-php-configure/php-extensions.png
[handler-mappings]: ./media/web-sites-php-configure/handler-mappings.png
[http://windows.php.net/download/]: http://windows.php.net/download/
[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/
[SETPHPVERCLI]: ./media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: ./media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: ./media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: ./media/web-sites-php-configure/ShowPHPVersion-PS.png

