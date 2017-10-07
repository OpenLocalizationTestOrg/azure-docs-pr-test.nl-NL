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
# <a name="configure-php-in-azure-app-service-web-apps"></a>PHP configureren in Azure App Service WebApps
## <a name="introduction"></a>Inleiding
Deze handleiding leert u hoe tooconfigure ingebouwde PHP-runtime voor Web-Apps in Hallo [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), geeft u een aangepaste PHP-runtime en uitbreidingen inschakelen. App Service toouse zich aanmelden voor Hallo [gratis proefversie]. tooget hello meest van deze handleiding, u moet eerst een PHP-web-app in App Service maken.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-hello-built-in-php-version"></a>Hoe: wijziging Hallo ingebouwde PHP-versie
Standaard is PHP 5.5 geïnstalleerd en onmiddellijk beschikbaar voor gebruik bij het maken van een App Service-web-app. Hallo van de beste manier toosee Hallo beschikbare versie revisie, de standaardconfiguratie en hello ingeschakelde extensies is toodeploy een script dat Hallo roept [phpinfo()] functie.

De versies van PHP 5.6 en PHP 7.0 zijn ook beschikbaar, maar niet standaard ingeschakeld. tooupdate hello PHP-versie, volg een van deze methoden:

### <a name="azure-portal"></a>Azure Portal
1. Blader tooyour web-app in Hallo [Azure Portal](https://portal.azure.com) en klik op Hallo **instellingen** knop.
   
    ![Instellingen voor Web-App][settings-button]
2. Van Hallo **instellingen** blade Selecteer **toepassingsinstellingen** en kiest u Hallo nieuwe PHP-versie.
   
    ![Toepassingsinstellingen][application-settings]
3. Klik op Hallo **opslaan** knop bovenaan Hallo Hallo **Web-appinstellingen** blade.
   
    ![Configuratie-instellingen opslaan][save-button]

### <a name="azure-powershell-windows"></a>Azure PowerShell (Windows)
1. Open Azure PowerShell en tooyour aanmeldingsaccount:
   
        PS C:\> Login-AzureRmAccount
2. Hallo PHP-versie voor Hallo web-app ingesteld.
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. Hallo PHP-versie is nu ingesteld. U kunt deze instellingen controleren:
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a>Azure-opdrachtregelinterface (Linux, Mac, Windows)
toouse hello Azure opdrachtregel-Interface, moet u hebben **Node.js** op uw computer geïnstalleerd.

1. Open de Terminal en tooyour aanmeldingsaccount.
   
        azure login
2. Hallo PHP-versie voor Hallo web-app ingesteld.
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. Hallo PHP-versie is nu ingesteld. U kunt deze instellingen controleren:
   
        azure site show {app-name}

> [!NOTE] 
> Hallo [Azure CLI 2.0](https://github.com/Azure/azure-cli) opdrachten equivalent toohello bovenstaande zijn zijn:
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-hello-built-in-php-configurations"></a>Procedure: ingebouwde PHP-configuraties Hallo wijzigen
Voor een ingebouwde PHP-runtime kunt u Hallo configuratieopties door Hallo onderstaande stappen te volgen. (Zie voor meer informatie over richtlijnen php.ini [lijst van php.ini richtlijnen].)

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a>Het wijzigen van PHP\_INI\_gebruiker, PHP\_INI\_PERDIR, PHP\_INI\_alle configuratie-instellingen
1. Voeg een [. user.ini] bestand tooyour-hoofdmap.
2. Toevoegen van configuratie-instellingen toohello `.user.ini` met behulp van het bestand Hallo dezelfde syntaxis die u wilt gebruiken in een `php.ini` bestand. Bijvoorbeeld, als u deze wilde tooturn hello `display_errors` instelling Stel `upload_max_filesize` too10M, instellen van uw `.user.ini` bestand zou deze tekst bevatten:
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on toowrite errors tood:\home\LogFiles\php_errors.log
        ; log_errors=On
3. Implementeer uw web-app.
4. Opnieuw opstarten Hallo web-app. (Opnieuw opstarten is nodig omdat Hallo frequentie met welke PHP leest `.user.ini` bestanden wordt bepaald door Hallo `user_ini.cache_ttl` instelling, die is een systeemniveau-instelling en 300 seconden (5 minuten) is standaard. Opnieuw te starten Hallo web-app forceert PHP tooread Hallo nieuwe instellingen in het Hallo `.user.ini` bestand.)

Als een alternatieve toousing een `.user.ini` -bestand, kunt u Hallo [ini_set()] functie in scripts tooset configuratieopties die niet op systeemniveau richtlijnen.

### <a name="changing-phpinisystem-configuration-settings"></a>Het wijzigen van PHP\_INI\_SYSTEM configuratie-instellingen
1. Toevoegen van een App-instelling tooyour Web-App met Hallo sleutel `PHP_INI_SCAN_DIR` en waarde`d:\home\site\ini`
2. Maak een `settings.ini` bestand met behulp van de Kudu-Console (http://&lt;-sitenaam&gt;. scm.azurewebsite.net) in Hallo `d:\home\site\ini` directory.
3. Toevoegen van configuratie-instellingen toohello `settings.ini` bestand met dezelfde syntaxis die u in een bestand php.ini gebruiken wilt Hallo. Bijvoorbeeld, als u deze wilde toopoint hello `curl.cainfo` instelling tooa `*.crt` bestands- en wincache.maxfilesize instelling too512K, stel uw `settings.ini` bestand zou deze tekst bevatten:
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. Start opnieuw op uw Web-App tooload Hallo wijzigingen.

## <a name="how-to-enable-extensions-in-hello-default-php-runtime"></a>Hoe: uitbreidingen in Hallo standaard PHP-runtime inschakelen
Zoals vermeld in de vorige sectie hello, Hallo aanbevolen manier toosee Hallo standaard PHP-versie, de standaardconfiguratie en Hallo ingeschakeld extensies toodeploy een script dat roept is [phpinfo()]. Extra extensies tooenable, stappen Hallo volgende:

### <a name="configure-via-ini-settings"></a>Via ini-instellingen configureren
1. Voeg een `ext` directory toohello `d:\home\site` directory.
2. Plaatsen `.dll` extensiebestanden in Hallo `ext` directory (bijvoorbeeld `php_xdebug.dll`). Zorg ervoor dat de Hallo extensies compatibel is met de standaardversie van PHP en zijn VC9 en niet-thread-safe (nts) compatibel zijn.
3. Toevoegen van een App-instelling tooyour Web-App met Hallo sleutel `PHP_INI_SCAN_DIR` en waarde`d:\home\site\ini`
4. Maak een `ini` bestanden per `d:\home\site\ini` aangeroepen `extensions.ini`.
5. Toevoegen van configuratie-instellingen toohello `extensions.ini` bestand met dezelfde syntaxis die u in een bestand php.ini gebruiken wilt Hallo. Als u deze wilde tooenable hello MongoDB en XDebug-extensies, bijvoorbeeld uw `extensions.ini` bestand zou deze tekst bevatten:
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. Start opnieuw op uw Web-App tooload Hallo wijzigingen.

### <a name="configure-via-app-setting"></a>Via App-instelling configureren
1. Voeg een `bin` directory toohello-hoofdmap.
2. Plaatsen `.dll` extensiebestanden in Hallo `bin` directory (bijvoorbeeld `php_xdebug.dll`). Zorg ervoor dat de Hallo extensies compatibel is met de standaardversie van PHP en zijn VC9 en niet-thread-safe (nts) compatibel zijn.
3. Implementeer uw web-app.
4. Tooyour web-app in hello Azure Portal bladeren en klik op Hallo **instellingen** knop.
   
    ![Instellingen voor Web-App][settings-button]
5. Van Hallo **instellingen** blade Selecteer **toepassingsinstellingen** en schuif toohello **appinstellingen** sectie.
6. In Hallo **appinstellingen** sectie, maakt u een **PHP_EXTENSIONS** sleutel. Hallo-waarde voor deze sleutel wordt de hoofdmap van een pad relatief toowebsite: **bin\your-ext-file**.
   
    ![De extensie in de app-instellingen inschakelen][php-extensions]
7. Klik op Hallo **opslaan** knop bovenaan Hallo Hallo **Web-appinstellingen** blade.
   
    ![Configuratie-instellingen opslaan][save-button]

Zend extensies worden ook ondersteund met behulp van een **PHP_ZENDEXTENSIONS** sleutel. tooenable meerdere extensies bevatten een door komma's gescheiden lijst met `.dll` bestanden voor de waarde van de instelling app Hallo.

## <a name="how-to-use-a-custom-php-runtime"></a>Procedure: een aangepaste PHP-runtime gebruiken
App Service Web Apps kunt een PHP-runtime op te geven tooexecute PHP-scripts gebruiken in plaats van Hallo standaard PHP-runtime. Hallo-runtime die u opgeeft, kan worden geconfigureerd met een `php.ini` -bestand dat u ook opgeven. een aangepaste PHP-runtime met Web-Apps toouse Hallo volgende stappen.

1. Verkrijgen van een niet-thread-safe, VC9 of VC11 compatibele versie van PHP voor Windows. Recente versies van PHP voor Windows vindt u hier: [http://windows.php.net/download/]. Oudere versies kunnen u vinden in Hallo archief hier: [http://windows.php.net/downloads/releases/archives/].
2. Hallo wijzigen `php.ini` -bestand voor de runtime. Houd er rekening mee dat alle configuratieinstellingen die systeem-niveau-only richtlijnen worden genegeerd door de Web-Apps. (Zie voor meer informatie over system-niveau-only richtlijnen [lijst van php.ini richtlijnen]).
3. Eventueel extensies tooyour PHP-runtime toevoegen en ze inschakelen in Hallo `php.ini` bestand.
4. Voeg een `bin` directory tooyour-hoofdmap en put Hallo map waarin uw PHP-runtime erin (bijvoorbeeld `bin\php`).
5. Implementeer uw web-app.
6. Tooyour web-app in hello Azure Portal bladeren en klik op Hallo **instellingen** knop.
   
    ![Instellingen voor Web-App][settings-button]
7. Van Hallo **instellingen** blade Selecteer **toepassingsinstellingen** en schuif toohello **Handlertoewijzingen** sectie. Voeg `*.php` toohello extensie veld en voeg Hallo pad toohello `php-cgi.exe` uitvoerbare. Als u uw PHP-runtime in Hallo `bin` directory in de hoofdmap van uw toepassing hello Hallo-pad moet `D:\home\site\wwwroot\bin\php\php-cgi.exe`.
   
    ![Handler in lijnhandler toewijzingen opgeven][handler-mappings]
8. Klik op Hallo **opslaan** knop bovenaan Hallo Hallo **Web-appinstellingen** blade.
   
    ![Configuratie-instellingen opslaan][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a>Hoe: Composer automatiseren met behulp van Azure
Standaard geen App Service reactie met composer.json, als u in uw PHP-project hebt. Als u [Git-implementatie](app-service-deploy-local-git.md), kunt u composer.json tijdens de verwerking inschakelen `git push` doordat Hallo Composer-extensie.

> [!NOTE]
> U kunt [stem voor uitstekende Composer ondersteuning in App Service hier](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!
> 
> 

1. In uw PHP web-app blade in Hallo [Azure-portal](https://portal.azure.com), klikt u op **extra** > **extensies**.
   
    ![Azure Portal instellingen blade tooenable Composer automatiseren met behulp van Azure](./media/web-sites-php-configure/composer-extension-settings.png)
2. Klik op **toevoegen**, klikt u vervolgens op **Composer**.
   
    ![Composer-extensie tooenable Composer automation toevoegen in Azure](./media/web-sites-php-configure/composer-extension-add.png)
3. Klik op **OK** tooaccept juridische voorwaarden. Klik op **OK** opnieuw tooadd Hallo-extensie.
   
    Hallo **extensies geïnstalleerd** blade ziet nu Hallo Composer-extensie.  
    ![Accepteer de juridische voorwaarden tooenable Composer automatiseren met behulp van Azure](./media/web-sites-php-configure/composer-extension-view.png)
4. Nu uitvoeren `git add`, `git commit`, en `git push` zoals in de vorige sectie Hallo. Nu ziet u dat Composer afhankelijkheden die zijn gedefinieerd in composer.json wordt geïnstalleerd.
   
    ![GIT-implementatie met Composer automatiseren met behulp van Azure](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie, Hallo [PHP-ontwikkelaarscentrum](/develop/php/).

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
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

