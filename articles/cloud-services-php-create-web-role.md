---
title: aaaCreate Azure web- en werkrollen rollen voor PHP | Microsoft Docs
description: Een handleiding toocreating PHP web- en werkrollen rollen in een Azure-cloudservice en configureren Hallo PHP-runtime.
services: 
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9f7ccda0-bd96-4f7b-a7af-fb279a9e975b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 04a6e8c9c379cb0f854645941b6bc7d614bb91f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-php-web-and-worker-roles"></a>Hoe toocreate PHP web- en werkrollen rollen
## <a name="overview"></a>Overzicht
Deze handleiding leert u hoe toocreate PHP web- of worker rollen in een Windows-ontwikkelomgeving kiest een specifieke versie van PHP Hallo 'ingebouwde' versies die beschikbaar zijn, Hallo PHP-configuratie wijzigen uitbreidingen inschakelen en ten slotte tooAzure implementeren. Ook wordt beschreven hoe tooconfigure een web- of worker-rol toouse een PHP-runtime (met aangepaste configuratie en -extensies) die u opgeeft.

## <a name="what-are-php-web-and-worker-roles"></a>Wat zijn de PHP-web- en werkrollen functies?
Azure biedt drie compute-modellen voor het uitvoeren van toepassingen: Azure App Service, Azure virtuele Machines en Azure Cloud Services. Alle drie modellen ondersteunen PHP. Cloudservices, waaronder web-en werkrollen, biedt *platform als een service (PaaS)*. Binnen een cloudservice biedt een Webrol een speciale Internet Information Services (IIS) web server toohost van front-end webtoepassingen. Een werkrol kan asynchrone langlopende of permanente taken onafhankelijk van de gebruikersinteractie of invoer uitvoeren.

Zie voor meer informatie over deze opties [Compute hosting-opties die worden geleverd door Azure](cloud-services/cloud-services-choose-me.md).

## <a name="download-hello-azure-sdk-for-php"></a>Hello Azure SDK voor PHP downloaden
Hallo [Azure SDK voor PHP] bestaat uit verschillende onderdelen. In dit artikel wordt gebruik van deze twee: Azure PowerShell en Azure emulators Hallo. Deze twee componenten kunnen worden geïnstalleerd via Hallo Microsoft Web Platform Installer. Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

## <a name="create-a-cloud-services-project"></a>Een Cloud Services-project maken
Hallo eerste stap bij het maken van een PHP-web- of worker-rol is toocreate een Azure-Service-project. een Azure-Service-project fungeert als een logische container voor web-en werkrollen en het Hallo-project bevat [definitie (.csdef)] en [serviceconfiguratie (.cscfg)] bestanden.

toocreate een nieuw Azure-Service-project, Azure PowerShell uitvoeren als beheerder en Hallo volgende opdracht uitvoeren:

    PS C:\>New-AzureServiceProject myProject

Met deze opdracht wordt een nieuwe map maken (`myProject`) toowhich u web-en werkrollen kunt toevoegen.

## <a name="add-php-web-or-worker-roles"></a>PHP-web- of worker functies toevoegen
tooadd een PHP-rol tooa webproject uitvoeren van de volgende opdracht uit in de hoofdmap van het project Hallo Hallo:

    PS C:\myProject> Add-AzurePHPWebRole roleName

Gebruik deze opdracht voor een werkrol:

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> Hallo `roleName` parameter is optioneel. Als u dit weglaat, wordt de rolnaam Hallo automatisch gegenereerd. Hallo eerste Webrol gemaakt worden `WebRole1`, Hallo tweede worden `WebRole2`, enzovoort. Hallo eerste werkrol gemaakt worden `WorkerRole1`, Hallo tweede worden `WorkerRole2`, enzovoort.
>
>

## <a name="specify-hello-built-in-php-version"></a>Hallo ingebouwde PHP-versie opgeven
Wanneer u een PHP web- of worker tooa rolproject toevoegt, worden de configuratiebestanden van het project Hallo gewijzigd zodat PHP wordt geïnstalleerd op elke web- of worker-exemplaar van uw toepassing als deze is geïmplementeerd. toosee Hallo-versie van PHP die worden geïnstalleerd standaard Hallo volgende opdracht uitvoeren:

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

Hallo uitvoer van de bovenstaande Hallo opdracht ziet er ongeveer toowhat worden hieronder weergegeven. In dit voorbeeld Hallo `IsDefault` -vlag is ingesteld te`true` voor PHP 5.3.17, die aangeeft dat het Hallo PHP standaardversie geïnstalleerd zal zijn.

```
Runtime Version     PackageUri                      IsDefault
------- -------     ----------                      ---------
Node 0.6.17         http://nodertncu.blob.core...   False
Node 0.6.20         http://nodertncu.blob.core...   True
Node 0.8.4          http://nodertncu.blob.core...   False
IISNode 0.1.21      http://nodertncu.blob.core...   True
Cache 1.8.0         http://nodertncu.blob.core...   True
PHP 5.3.17          http://nodertncu.blob.core...   True
PHP 5.4.0           http://nodertncu.blob.core...   False
```

Hallo PHP runtime versie tooany van Hallo PHP-versies die worden vermeld, kunt u instellen. Bijvoorbeeld: tooset Hallo PHP-versie (voor een rol met de naam van de Hallo `roleName`) too5.4.0, gebruik Hallo volgende opdracht:

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> Beschikbare PHP versies kunnen worden gewijzigd in toekomstige Hallo.
>
>

## <a name="customize-hello-built-in-php-runtime"></a>Hallo ingebouwde PHP-runtime aanpassen
Hebt u volledige controle over de configuratie van Hallo PHP runtime die wordt geïnstalleerd wanneer u de stappen Hallo hierboven, met inbegrip van wijziging van Hallo `php.ini` instellingen en het inschakelen van extensies.

toocustomize Hallo ingebouwde PHP-runtime, als volgt te werk:

1. Voeg een nieuwe map met de naam `php`, toohello `bin` map van uw Webrol. Voor een werkrol toevoegen hoofdmap toohello-rol.
2. In Hallo `php` map maken van een andere map met de naam `ext`. Plaats een `.dll` extensiebestanden (bijv, `php_mongo.dll`) dat u wilt dat tooenable in deze map.
3. Voeg een `php.ini` toohello bestand `php` map. Eventuele aangepaste uitbreidingen inschakelen en instellen van een PHP-richtlijnen in dit bestand. Bijvoorbeeld, als u deze wilde tooturn `display_errors` op en schakel Hallo `php_mongo.dll` extensie, Hallo inhoud van uw `php.ini` bestand zou als volgt zijn:

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> Alle instellingen die u niet expliciet in Hallo instelt `php.ini` bestand dat u wordt automatisch verstrekt tootheir standaardwaarden worden ingesteld. Houd er echter rekening mee dat u een complete kunt toevoegen `php.ini` bestand.
>
>

## <a name="use-your-own-php-runtime"></a>Uw eigen PHP-runtime gebruiken
In sommige gevallen, in plaats van een ingebouwde PHP-runtime selecteren en deze te configureren als hierboven beschreven, kunt u tooprovide uw eigen PHP-runtime. U kunt bijvoorbeeld Hallo dezelfde PHP-runtime in een web- of worker-rol die u in uw ontwikkelomgeving gebruikt. Dit maakt het eenvoudiger tooensure toepassing hello verandert niet gedrag in uw productieomgeving.

### <a name="configure-a-web-role-toouse-your-own-php-runtime"></a>Uw eigen PHP-runtime voor een rol web toouse configureren
tooconfigure een web-functie toouse een PHP-runtime die u opgeeft, als volgt te werk:

1. Een Azure-Service-project maken en toevoegen van een PHP-Webrol, zoals eerder is beschreven in dit onderwerp.
2. Maak een `php` map in Hallo `bin` map die zich in de hoofdmap van uw Webrol en voeg vervolgens uw PHP-runtime (alle binaire bestanden, configuratiebestanden, submappen, enz.) toohello `php` map.
3. (OPTIONEEL) Als uw PHP-runtime Hallo gebruikt [Microsoft-Drivers voor PHP voor SQL Server][sqlsrv drivers], moet u tooconfigure uw rol web tooinstall [SQL Server Native Client 2012] [ sql native client] wanneer deze is ingericht. toodo dit Hallo toevoegen [sqlncli.msi x64 installatieprogramma] toohello `bin` map in de hoofdmap van uw Webrol. Hallo opstartscript beschreven in de volgende stap Hallo uitgevoerd achtergrond Hallo-installatieprogramma wanneer Hallo-rol is ingericht. Als uw PHP-runtime geen Microsoft-Drivers Hallo voor PHP voor SQL Server gebruikt, kunt u volgt regel uit het Hallo-script wordt weergegeven in de volgende stap Hallo Hallo verwijderen:

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. Definieer een starten van de taak die wordt geconfigureerd [Internet Information Services (IIS)] [ iis.net] toouse uw PHP-runtime-toohandle aanvragen voor `.php` pagina's. toodo deze, open Hallo `setup_web.cmd` bestand (in Hallo `bin` -bestand van de hoofdmap van de Webrol) in een teksteditor en vervang de inhoud ervan met Hallo volgende script:

    ```cmd
    @ECHO ON
    cd "%~dp0"

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    SET PHP_FULL_PATH=%~dp0php\php-cgi.exe
    SET NEW_PATH=%PATH%;%RoleRoot%\base\x86

    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%',maxInstances='12',idleTimeout='60000',activityTimeout='3600',requestTimeout='60000',instanceMaxRequests='10000',protocol='NamedPipe',flushNamedPipe='False']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PATH',value='%NEW_PATH%']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PHP_FCGI_MAX_REQUESTS',value='10000']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/handlers /+"[name='PHP',path='*.php',verb='GET,HEAD,POST',modules='FastCgiModule',scriptProcessor='%PHP_FULL_PATH%',resourceType='Either',requireAccess='Script']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /"[fullPath='%PHP_FULL_PATH%'].queueLength:50000"
    ```
5. Hoofdmap van uw toepassing bestanden tooyour Webrol van toevoegen. Dit is de hoofdmap van Hallo webserver.
6. Uw toepassing te publiceren, zoals beschreven in Hallo [uw toepassing publiceren](#publish-your-application) hieronder.

> [!NOTE]
> Hallo `download.ps1` script (in Hallo `bin` map van de hoofdmap van Hallo Webrol) kan worden verwijderd nadat u Hallo stappen hierboven beschreven voor het gebruik van uw eigen PHP-runtime.
>
>

### <a name="configure-a-worker-role-toouse-your-own-php-runtime"></a>Configureren van een werknemer rol toouse uw eigen PHP-runtime
tooconfigure een werknemer rol toouse een PHP-runtime die u opgeeft, als volgt te werk:

1. Een Azure-Service-project maken en toevoegen van een PHP-werkrol zoals eerder is beschreven in dit onderwerp.
2. Maak een `php` map in de hoofdmap van Hallo worker rol, en voeg vervolgens uw PHP-runtime (alle binaire bestanden, configuratiebestanden, submappen, enz.) toohello `php` map.
3. (OPTIONEEL) Als uw PHP-runtime gebruikt [Microsoft-Drivers voor PHP voor SQL Server][sqlsrv drivers], moet u tooconfigure uw rol worker tooinstall [SQL Server Native Client 2012] [ sql native client] wanneer deze is ingericht. toodo dit Hallo toevoegen [sqlncli.msi x64 installatieprogramma] toohello-werkrol de hoofdmap. Hallo opstartscript beschreven in de volgende stap Hallo uitgevoerd achtergrond Hallo-installatieprogramma wanneer Hallo-rol is ingericht. Als uw PHP-runtime geen Microsoft-Drivers Hallo voor PHP voor SQL Server gebruikt, kunt u volgt regel uit het Hallo-script wordt weergegeven in de volgende stap Hallo Hallo verwijderen:

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. Definieer een starten van de taak die wordt toegevoegd uw `php.exe` uitvoerbare toohello-werkrol de omgevingsvariabele PATH wanneer Hallo-rol is ingericht. toodo deze, open Hallo `setup_worker.cmd` (in de hoofdmap van Hallo worker rol) bestand in een teksteditor en vervang de inhoud door Hallo script volgen:

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service toohello web root directory...
    icacls ..\ /grant "Network Service":(OI)(CI)W
    if %ERRORLEVEL% neq 0 goto error
    echo OK

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    setx Path "%PATH%;%~dp0php" /M

    if %ERRORLEVEL% neq 0 goto error

    echo SUCCESS
    exit /b 0

    :error

    echo FAILED
    exit /b -1
    ```
5. Hoofdmap van uw toepassing bestanden tooyour werkrol van toevoegen.
6. Uw toepassing te publiceren, zoals beschreven in Hallo [uw toepassing publiceren](#publish-your-application) hieronder.

## <a name="run-your-application-in-hello-compute-and-storage-emulators"></a>Uw toepassing uitvoeren in Hallo emulators berekeningen en opslag
Hello bieden Azure emulators van een lokale omgeving waarin u uw Azure-toepassing testen kunt voordat u deze toohello cloud implementeert. Er zijn een aantal verschillen tussen Hallo emulators en hello Azure-omgeving. dit beter, Zie toounderstand [hello Azure-opslagemulator gebruiken voor ontwikkeling en tests](storage/common/storage-use-emulator.md).

Opmerking PHP moeten zijn geïnstalleerd lokaal toouse hello rekenemulator. Hallo-rekenemulator gebruik uw lokale toorun voor PHP-installatie van uw toepassing.

toorun uitvoeren van uw project in Hallo-emulators Hallo volgende opdracht uit de hoofddirectory van uw project:

    PS C:\MyProject> Start-AzureEmulator

Hier ziet u uitvoer vergelijkbare toothis:

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

Ziet u uw toepassing hello emulator uitgevoerd op een webbrowser openen en bladeren door toohello lokaal adres wordt weergegeven in de uitvoer Hallo (`http://127.0.0.1:81` in bovenstaande Hallo voorbeeld van uitvoer).

toostop hello emulators, deze opdracht wordt uitgevoerd:

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a>Uw toepassing publiceren
toopublish uw toepassing, moet u toofirst importeren uw publicatie-instellingen met behulp van Hallo [importeren AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet. Vervolgens u uw toepassing publiceren kunt met behulp van Hallo [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet. Zie voor meer informatie over het ondertekenen van [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie, Hallo [PHP-ontwikkelaarscentrum](/develop/php/).

[Azure SDK voor PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[definitie (.csdef)]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[serviceconfiguratie (.cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[sqlncli.msi x64 installatieprogramma]: http://go.microsoft.com/fwlink/?LinkID=239648
