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
# <a name="how-toocreate-php-web-and-worker-roles"></a><span data-ttu-id="f94bb-103">Hoe toocreate PHP web- en werkrollen rollen</span><span class="sxs-lookup"><span data-stu-id="f94bb-103">How toocreate PHP web and worker roles</span></span>
## <a name="overview"></a><span data-ttu-id="f94bb-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="f94bb-104">Overview</span></span>
<span data-ttu-id="f94bb-105">Deze handleiding leert u hoe toocreate PHP web- of worker rollen in een Windows-ontwikkelomgeving kiest een specifieke versie van PHP Hallo 'ingebouwde' versies die beschikbaar zijn, Hallo PHP-configuratie wijzigen uitbreidingen inschakelen en ten slotte tooAzure implementeren.</span><span class="sxs-lookup"><span data-stu-id="f94bb-105">This guide will show you how toocreate PHP web or worker roles in a Windows development environment, choose a specific version of PHP from hello "built-in" versions available, change hello PHP configuration, enable extensions, and finally, deploy tooAzure.</span></span> <span data-ttu-id="f94bb-106">Ook wordt beschreven hoe tooconfigure een web- of worker-rol toouse een PHP-runtime (met aangepaste configuratie en -extensies) die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="f94bb-106">It also describes how tooconfigure a web or worker role toouse a PHP runtime (with custom configuration and extensions) that you provide.</span></span>

## <a name="what-are-php-web-and-worker-roles"></a><span data-ttu-id="f94bb-107">Wat zijn de PHP-web- en werkrollen functies?</span><span class="sxs-lookup"><span data-stu-id="f94bb-107">What are PHP web and worker roles?</span></span>
<span data-ttu-id="f94bb-108">Azure biedt drie compute-modellen voor het uitvoeren van toepassingen: Azure App Service, Azure virtuele Machines en Azure Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="f94bb-108">Azure provides three compute models for running applications: Azure App Service, Azure Virtual Machines, and Azure Cloud Services.</span></span> <span data-ttu-id="f94bb-109">Alle drie modellen ondersteunen PHP.</span><span class="sxs-lookup"><span data-stu-id="f94bb-109">All three models support PHP.</span></span> <span data-ttu-id="f94bb-110">Cloudservices, waaronder web-en werkrollen, biedt *platform als een service (PaaS)*.</span><span class="sxs-lookup"><span data-stu-id="f94bb-110">Cloud Services, which includes web and worker roles, provides *platform as a service (PaaS)*.</span></span> <span data-ttu-id="f94bb-111">Binnen een cloudservice biedt een Webrol een speciale Internet Information Services (IIS) web server toohost van front-end webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="f94bb-111">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server toohost front-end web applications.</span></span> <span data-ttu-id="f94bb-112">Een werkrol kan asynchrone langlopende of permanente taken onafhankelijk van de gebruikersinteractie of invoer uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f94bb-112">A worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="f94bb-113">Zie voor meer informatie over deze opties [Compute hosting-opties die worden geleverd door Azure](cloud-services/cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="f94bb-113">For more information about these options, see [Compute hosting options provided by Azure](cloud-services/cloud-services-choose-me.md).</span></span>

## <a name="download-hello-azure-sdk-for-php"></a><span data-ttu-id="f94bb-114">Hello Azure SDK voor PHP downloaden</span><span class="sxs-lookup"><span data-stu-id="f94bb-114">Download hello Azure SDK for PHP</span></span>
<span data-ttu-id="f94bb-115">Hallo [Azure SDK voor PHP] bestaat uit verschillende onderdelen.</span><span class="sxs-lookup"><span data-stu-id="f94bb-115">hello [Azure SDK for PHP] consists of several components.</span></span> <span data-ttu-id="f94bb-116">In dit artikel wordt gebruik van deze twee: Azure PowerShell en Azure emulators Hallo.</span><span class="sxs-lookup"><span data-stu-id="f94bb-116">This article will use two of them: Azure PowerShell and hello Azure emulators.</span></span> <span data-ttu-id="f94bb-117">Deze twee componenten kunnen worden geïnstalleerd via Hallo Microsoft Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="f94bb-117">These two components can be installed via hello Microsoft Web Platform Installer.</span></span> <span data-ttu-id="f94bb-118">Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f94bb-118">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="create-a-cloud-services-project"></a><span data-ttu-id="f94bb-119">Een Cloud Services-project maken</span><span class="sxs-lookup"><span data-stu-id="f94bb-119">Create a Cloud Services project</span></span>
<span data-ttu-id="f94bb-120">Hallo eerste stap bij het maken van een PHP-web- of worker-rol is toocreate een Azure-Service-project.</span><span class="sxs-lookup"><span data-stu-id="f94bb-120">hello first step in creating a PHP web or worker role is toocreate an Azure Service project.</span></span> <span data-ttu-id="f94bb-121">een Azure-Service-project fungeert als een logische container voor web-en werkrollen en het Hallo-project bevat [definitie (.csdef)] en [serviceconfiguratie (.cscfg)] bestanden.</span><span class="sxs-lookup"><span data-stu-id="f94bb-121">an Azure Service project serves as a logical container for web and worker roles, and it contains hello project's [service definition (.csdef)] and [service configuration (.cscfg)] files.</span></span>

<span data-ttu-id="f94bb-122">toocreate een nieuw Azure-Service-project, Azure PowerShell uitvoeren als beheerder en Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f94bb-122">toocreate a new Azure Service project, run Azure PowerShell as an administrator, and execute hello following command:</span></span>

    PS C:\>New-AzureServiceProject myProject

<span data-ttu-id="f94bb-123">Met deze opdracht wordt een nieuwe map maken (`myProject`) toowhich u web-en werkrollen kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f94bb-123">This command will create a new directory (`myProject`) toowhich you can add web and worker roles.</span></span>

## <a name="add-php-web-or-worker-roles"></a><span data-ttu-id="f94bb-124">PHP-web- of worker functies toevoegen</span><span class="sxs-lookup"><span data-stu-id="f94bb-124">Add PHP web or worker roles</span></span>
<span data-ttu-id="f94bb-125">tooadd een PHP-rol tooa webproject uitvoeren van de volgende opdracht uit in de hoofdmap van het project Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="f94bb-125">tooadd a PHP web role tooa project, run hello following command from within hello project's root directory:</span></span>

    PS C:\myProject> Add-AzurePHPWebRole roleName

<span data-ttu-id="f94bb-126">Gebruik deze opdracht voor een werkrol:</span><span class="sxs-lookup"><span data-stu-id="f94bb-126">For a worker role, use this command:</span></span>

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> <span data-ttu-id="f94bb-127">Hallo `roleName` parameter is optioneel.</span><span class="sxs-lookup"><span data-stu-id="f94bb-127">hello `roleName` parameter is optional.</span></span> <span data-ttu-id="f94bb-128">Als u dit weglaat, wordt de rolnaam Hallo automatisch gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="f94bb-128">If it is omitted, hello role name will be automatically generated.</span></span> <span data-ttu-id="f94bb-129">Hallo eerste Webrol gemaakt worden `WebRole1`, Hallo tweede worden `WebRole2`, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="f94bb-129">hello first web role created will be `WebRole1`, hello second will be `WebRole2`, and so on.</span></span> <span data-ttu-id="f94bb-130">Hallo eerste werkrol gemaakt worden `WorkerRole1`, Hallo tweede worden `WorkerRole2`, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="f94bb-130">hello first worker role created will be `WorkerRole1`, hello second will be `WorkerRole2`, and so on.</span></span>
>
>

## <a name="specify-hello-built-in-php-version"></a><span data-ttu-id="f94bb-131">Hallo ingebouwde PHP-versie opgeven</span><span class="sxs-lookup"><span data-stu-id="f94bb-131">Specify hello built-in PHP version</span></span>
<span data-ttu-id="f94bb-132">Wanneer u een PHP web- of worker tooa rolproject toevoegt, worden de configuratiebestanden van het project Hallo gewijzigd zodat PHP wordt geïnstalleerd op elke web- of worker-exemplaar van uw toepassing als deze is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f94bb-132">When you add a PHP web or worker role tooa project, hello project's configuration files are modified so that PHP will be installed on each web or worker instance of your application when it is deployed.</span></span> <span data-ttu-id="f94bb-133">toosee Hallo-versie van PHP die worden geïnstalleerd standaard Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f94bb-133">toosee hello version of PHP that will be installed by default, run hello following command:</span></span>

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

<span data-ttu-id="f94bb-134">Hallo uitvoer van de bovenstaande Hallo opdracht ziet er ongeveer toowhat worden hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f94bb-134">hello output from hello command above will look similar toowhat is shown below.</span></span> <span data-ttu-id="f94bb-135">In dit voorbeeld Hallo `IsDefault` -vlag is ingesteld te`true` voor PHP 5.3.17, die aangeeft dat het Hallo PHP standaardversie geïnstalleerd zal zijn.</span><span class="sxs-lookup"><span data-stu-id="f94bb-135">In this example, hello `IsDefault` flag is set too`true` for PHP 5.3.17, indicating that it will be hello default PHP version installed.</span></span>

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

<span data-ttu-id="f94bb-136">Hallo PHP runtime versie tooany van Hallo PHP-versies die worden vermeld, kunt u instellen.</span><span class="sxs-lookup"><span data-stu-id="f94bb-136">You can set hello PHP runtime version tooany of hello PHP versions that are listed.</span></span> <span data-ttu-id="f94bb-137">Bijvoorbeeld: tooset Hallo PHP-versie (voor een rol met de naam van de Hallo `roleName`) too5.4.0, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f94bb-137">For example, tooset hello PHP version (for a role with hello name `roleName`) too5.4.0, use hello following command:</span></span>

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> <span data-ttu-id="f94bb-138">Beschikbare PHP versies kunnen worden gewijzigd in toekomstige Hallo.</span><span class="sxs-lookup"><span data-stu-id="f94bb-138">Available PHP versions may change in hello future.</span></span>
>
>

## <a name="customize-hello-built-in-php-runtime"></a><span data-ttu-id="f94bb-139">Hallo ingebouwde PHP-runtime aanpassen</span><span class="sxs-lookup"><span data-stu-id="f94bb-139">Customize hello built-in PHP runtime</span></span>
<span data-ttu-id="f94bb-140">Hebt u volledige controle over de configuratie van Hallo PHP runtime die wordt geïnstalleerd wanneer u de stappen Hallo hierboven, met inbegrip van wijziging van Hallo `php.ini` instellingen en het inschakelen van extensies.</span><span class="sxs-lookup"><span data-stu-id="f94bb-140">You have complete control over hello configuration of hello PHP runtime that is installed when you follow hello steps above, including modification of `php.ini` settings and enabling of extensions.</span></span>

<span data-ttu-id="f94bb-141">toocustomize Hallo ingebouwde PHP-runtime, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="f94bb-141">toocustomize hello built-in PHP runtime, follow these steps:</span></span>

1. <span data-ttu-id="f94bb-142">Voeg een nieuwe map met de naam `php`, toohello `bin` map van uw Webrol.</span><span class="sxs-lookup"><span data-stu-id="f94bb-142">Add a new folder, named `php`, toohello `bin` directory of your web role.</span></span> <span data-ttu-id="f94bb-143">Voor een werkrol toevoegen hoofdmap toohello-rol.</span><span class="sxs-lookup"><span data-stu-id="f94bb-143">For a worker role, add it toohello role's root directory.</span></span>
2. <span data-ttu-id="f94bb-144">In Hallo `php` map maken van een andere map met de naam `ext`.</span><span class="sxs-lookup"><span data-stu-id="f94bb-144">In hello `php` folder, create another folder called `ext`.</span></span> <span data-ttu-id="f94bb-145">Plaats een `.dll` extensiebestanden (bijv, `php_mongo.dll`) dat u wilt dat tooenable in deze map.</span><span class="sxs-lookup"><span data-stu-id="f94bb-145">Put any `.dll` extension files (e.g., `php_mongo.dll`) that you want tooenable in this folder.</span></span>
3. <span data-ttu-id="f94bb-146">Voeg een `php.ini` toohello bestand `php` map.</span><span class="sxs-lookup"><span data-stu-id="f94bb-146">Add a `php.ini` file toohello `php` folder.</span></span> <span data-ttu-id="f94bb-147">Eventuele aangepaste uitbreidingen inschakelen en instellen van een PHP-richtlijnen in dit bestand.</span><span class="sxs-lookup"><span data-stu-id="f94bb-147">Enable any custom extensions and set any PHP directives in this file.</span></span> <span data-ttu-id="f94bb-148">Bijvoorbeeld, als u deze wilde tooturn `display_errors` op en schakel Hallo `php_mongo.dll` extensie, Hallo inhoud van uw `php.ini` bestand zou als volgt zijn:</span><span class="sxs-lookup"><span data-stu-id="f94bb-148">For example, if you wanted tooturn `display_errors` on and enable hello `php_mongo.dll` extension, hello contents of your `php.ini` file would be as follows:</span></span>

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> <span data-ttu-id="f94bb-149">Alle instellingen die u niet expliciet in Hallo instelt `php.ini` bestand dat u wordt automatisch verstrekt tootheir standaardwaarden worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f94bb-149">Any settings that you don't explicitly set in hello `php.ini` file that you provide will automatically be set tootheir default values.</span></span> <span data-ttu-id="f94bb-150">Houd er echter rekening mee dat u een complete kunt toevoegen `php.ini` bestand.</span><span class="sxs-lookup"><span data-stu-id="f94bb-150">However, keep in mind that you can add a complete `php.ini` file.</span></span>
>
>

## <a name="use-your-own-php-runtime"></a><span data-ttu-id="f94bb-151">Uw eigen PHP-runtime gebruiken</span><span class="sxs-lookup"><span data-stu-id="f94bb-151">Use your own PHP runtime</span></span>
<span data-ttu-id="f94bb-152">In sommige gevallen, in plaats van een ingebouwde PHP-runtime selecteren en deze te configureren als hierboven beschreven, kunt u tooprovide uw eigen PHP-runtime.</span><span class="sxs-lookup"><span data-stu-id="f94bb-152">In some cases, instead of selecting a built-in PHP runtime and configuring it as described above, you may want tooprovide your own PHP runtime.</span></span> <span data-ttu-id="f94bb-153">U kunt bijvoorbeeld Hallo dezelfde PHP-runtime in een web- of worker-rol die u in uw ontwikkelomgeving gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f94bb-153">For example, you can use hello same PHP runtime in a web or worker role that you use in your development environment.</span></span> <span data-ttu-id="f94bb-154">Dit maakt het eenvoudiger tooensure toepassing hello verandert niet gedrag in uw productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f94bb-154">This makes it easier tooensure that hello application will not change behavior in your production environment.</span></span>

### <a name="configure-a-web-role-toouse-your-own-php-runtime"></a><span data-ttu-id="f94bb-155">Uw eigen PHP-runtime voor een rol web toouse configureren</span><span class="sxs-lookup"><span data-stu-id="f94bb-155">Configure a web role toouse your own PHP runtime</span></span>
<span data-ttu-id="f94bb-156">tooconfigure een web-functie toouse een PHP-runtime die u opgeeft, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="f94bb-156">tooconfigure a web role toouse a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="f94bb-157">Een Azure-Service-project maken en toevoegen van een PHP-Webrol, zoals eerder is beschreven in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="f94bb-157">Create an Azure Service project and add a PHP web role as described previously in this topic.</span></span>
2. <span data-ttu-id="f94bb-158">Maak een `php` map in Hallo `bin` map die zich in de hoofdmap van uw Webrol en voeg vervolgens uw PHP-runtime (alle binaire bestanden, configuratiebestanden, submappen, enz.) toohello `php` map.</span><span class="sxs-lookup"><span data-stu-id="f94bb-158">Create a `php` folder in hello `bin` folder that is in your web role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) toohello `php` folder.</span></span>
3. <span data-ttu-id="f94bb-159">(OPTIONEEL) Als uw PHP-runtime Hallo gebruikt [Microsoft-Drivers voor PHP voor SQL Server][sqlsrv drivers], moet u tooconfigure uw rol web tooinstall [SQL Server Native Client 2012] [ sql native client] wanneer deze is ingericht.</span><span class="sxs-lookup"><span data-stu-id="f94bb-159">(OPTIONAL) If your PHP runtime uses hello [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need tooconfigure your web role tooinstall [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="f94bb-160">toodo dit Hallo toevoegen [sqlncli.msi x64 installatieprogramma] toohello `bin` map in de hoofdmap van uw Webrol.</span><span class="sxs-lookup"><span data-stu-id="f94bb-160">toodo this, add hello [sqlncli.msi x64 installer] toohello `bin` folder in your web role's root directory.</span></span> <span data-ttu-id="f94bb-161">Hallo opstartscript beschreven in de volgende stap Hallo uitgevoerd achtergrond Hallo-installatieprogramma wanneer Hallo-rol is ingericht.</span><span class="sxs-lookup"><span data-stu-id="f94bb-161">hello startup script described in hello next step will silently run hello installer when hello role is provisioned.</span></span> <span data-ttu-id="f94bb-162">Als uw PHP-runtime geen Microsoft-Drivers Hallo voor PHP voor SQL Server gebruikt, kunt u volgt regel uit het Hallo-script wordt weergegeven in de volgende stap Hallo Hallo verwijderen:</span><span class="sxs-lookup"><span data-stu-id="f94bb-162">If your PHP runtime does not use hello Microsoft Drivers for PHP for SQL Server, you can remove hello following line from hello script shown in hello next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="f94bb-163">Definieer een starten van de taak die wordt geconfigureerd [Internet Information Services (IIS)] [ iis.net] toouse uw PHP-runtime-toohandle aanvragen voor `.php` pagina's.</span><span class="sxs-lookup"><span data-stu-id="f94bb-163">Define a startup task that configures [Internet Information Services (IIS)][iis.net] toouse your PHP runtime toohandle requests for `.php` pages.</span></span> <span data-ttu-id="f94bb-164">toodo deze, open Hallo `setup_web.cmd` bestand (in Hallo `bin` -bestand van de hoofdmap van de Webrol) in een teksteditor en vervang de inhoud ervan met Hallo volgende script:</span><span class="sxs-lookup"><span data-stu-id="f94bb-164">toodo this, open hello `setup_web.cmd` file (in hello `bin` file of your web role's root directory) in a text editor and replace its contents with hello following script:</span></span>

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
5. <span data-ttu-id="f94bb-165">Hoofdmap van uw toepassing bestanden tooyour Webrol van toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f94bb-165">Add your application files tooyour web role's root directory.</span></span> <span data-ttu-id="f94bb-166">Dit is de hoofdmap van Hallo webserver.</span><span class="sxs-lookup"><span data-stu-id="f94bb-166">This will be hello web server's root directory.</span></span>
6. <span data-ttu-id="f94bb-167">Uw toepassing te publiceren, zoals beschreven in Hallo [uw toepassing publiceren](#publish-your-application) hieronder.</span><span class="sxs-lookup"><span data-stu-id="f94bb-167">Publish your application as described in hello [Publish your application](#publish-your-application) section below.</span></span>

> [!NOTE]
> <span data-ttu-id="f94bb-168">Hallo `download.ps1` script (in Hallo `bin` map van de hoofdmap van Hallo Webrol) kan worden verwijderd nadat u Hallo stappen hierboven beschreven voor het gebruik van uw eigen PHP-runtime.</span><span class="sxs-lookup"><span data-stu-id="f94bb-168">hello `download.ps1` script (in hello `bin` folder of hello web role's root directory) can be deleted after you follow hello steps described above for using your own PHP runtime.</span></span>
>
>

### <a name="configure-a-worker-role-toouse-your-own-php-runtime"></a><span data-ttu-id="f94bb-169">Configureren van een werknemer rol toouse uw eigen PHP-runtime</span><span class="sxs-lookup"><span data-stu-id="f94bb-169">Configure a worker role toouse your own PHP runtime</span></span>
<span data-ttu-id="f94bb-170">tooconfigure een werknemer rol toouse een PHP-runtime die u opgeeft, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="f94bb-170">tooconfigure a worker role toouse a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="f94bb-171">Een Azure-Service-project maken en toevoegen van een PHP-werkrol zoals eerder is beschreven in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="f94bb-171">Create an Azure Service project and add a PHP worker role as described previously in this topic.</span></span>
2. <span data-ttu-id="f94bb-172">Maak een `php` map in de hoofdmap van Hallo worker rol, en voeg vervolgens uw PHP-runtime (alle binaire bestanden, configuratiebestanden, submappen, enz.) toohello `php` map.</span><span class="sxs-lookup"><span data-stu-id="f94bb-172">Create a `php` folder in hello worker role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) toohello `php` folder.</span></span>
3. <span data-ttu-id="f94bb-173">(OPTIONEEL) Als uw PHP-runtime gebruikt [Microsoft-Drivers voor PHP voor SQL Server][sqlsrv drivers], moet u tooconfigure uw rol worker tooinstall [SQL Server Native Client 2012] [ sql native client] wanneer deze is ingericht.</span><span class="sxs-lookup"><span data-stu-id="f94bb-173">(OPTIONAL) If your PHP runtime uses [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need tooconfigure your worker role tooinstall [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="f94bb-174">toodo dit Hallo toevoegen [sqlncli.msi x64 installatieprogramma] toohello-werkrol de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="f94bb-174">toodo this, add hello [sqlncli.msi x64 installer] toohello worker role's root directory.</span></span> <span data-ttu-id="f94bb-175">Hallo opstartscript beschreven in de volgende stap Hallo uitgevoerd achtergrond Hallo-installatieprogramma wanneer Hallo-rol is ingericht.</span><span class="sxs-lookup"><span data-stu-id="f94bb-175">hello startup script described in hello next step will silently run hello installer when hello role is provisioned.</span></span> <span data-ttu-id="f94bb-176">Als uw PHP-runtime geen Microsoft-Drivers Hallo voor PHP voor SQL Server gebruikt, kunt u volgt regel uit het Hallo-script wordt weergegeven in de volgende stap Hallo Hallo verwijderen:</span><span class="sxs-lookup"><span data-stu-id="f94bb-176">If your PHP runtime does not use hello Microsoft Drivers for PHP for SQL Server, you can remove hello following line from hello script shown in hello next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="f94bb-177">Definieer een starten van de taak die wordt toegevoegd uw `php.exe` uitvoerbare toohello-werkrol de omgevingsvariabele PATH wanneer Hallo-rol is ingericht.</span><span class="sxs-lookup"><span data-stu-id="f94bb-177">Define a startup task that adds your `php.exe` executable toohello worker role's PATH environment variable when hello role is provisioned.</span></span> <span data-ttu-id="f94bb-178">toodo deze, open Hallo `setup_worker.cmd` (in de hoofdmap van Hallo worker rol) bestand in een teksteditor en vervang de inhoud door Hallo script volgen:</span><span class="sxs-lookup"><span data-stu-id="f94bb-178">toodo this, open hello `setup_worker.cmd` file (in hello worker role's root directory) in a text editor and replace its contents with hello following script:</span></span>

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
5. <span data-ttu-id="f94bb-179">Hoofdmap van uw toepassing bestanden tooyour werkrol van toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f94bb-179">Add your application files tooyour worker role's root directory.</span></span>
6. <span data-ttu-id="f94bb-180">Uw toepassing te publiceren, zoals beschreven in Hallo [uw toepassing publiceren](#publish-your-application) hieronder.</span><span class="sxs-lookup"><span data-stu-id="f94bb-180">Publish your application as described in hello [Publish your application](#publish-your-application) section below.</span></span>

## <a name="run-your-application-in-hello-compute-and-storage-emulators"></a><span data-ttu-id="f94bb-181">Uw toepassing uitvoeren in Hallo emulators berekeningen en opslag</span><span class="sxs-lookup"><span data-stu-id="f94bb-181">Run your application in hello compute and storage emulators</span></span>
<span data-ttu-id="f94bb-182">Hello bieden Azure emulators van een lokale omgeving waarin u uw Azure-toepassing testen kunt voordat u deze toohello cloud implementeert.</span><span class="sxs-lookup"><span data-stu-id="f94bb-182">hello Azure emulators provide a local environment in which you can test your Azure application before you deploy it toohello cloud.</span></span> <span data-ttu-id="f94bb-183">Er zijn een aantal verschillen tussen Hallo emulators en hello Azure-omgeving.</span><span class="sxs-lookup"><span data-stu-id="f94bb-183">There are some differences between hello emulators and hello Azure environment.</span></span> <span data-ttu-id="f94bb-184">dit beter, Zie toounderstand [hello Azure-opslagemulator gebruiken voor ontwikkeling en tests](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="f94bb-184">toounderstand this better, see [Use hello Azure storage emulator for development and testing](storage/common/storage-use-emulator.md).</span></span>

<span data-ttu-id="f94bb-185">Opmerking PHP moeten zijn geïnstalleerd lokaal toouse hello rekenemulator.</span><span class="sxs-lookup"><span data-stu-id="f94bb-185">Note that you must have PHP installed locally toouse hello compute emulator.</span></span> <span data-ttu-id="f94bb-186">Hallo-rekenemulator gebruik uw lokale toorun voor PHP-installatie van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="f94bb-186">hello compute emulator will use your local PHP installation toorun your application.</span></span>

<span data-ttu-id="f94bb-187">toorun uitvoeren van uw project in Hallo-emulators Hallo volgende opdracht uit de hoofddirectory van uw project:</span><span class="sxs-lookup"><span data-stu-id="f94bb-187">toorun your project in hello emulators, execute hello following command from your project's root directory:</span></span>

    PS C:\MyProject> Start-AzureEmulator

<span data-ttu-id="f94bb-188">Hier ziet u uitvoer vergelijkbare toothis:</span><span class="sxs-lookup"><span data-stu-id="f94bb-188">You will see output similar toothis:</span></span>

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

<span data-ttu-id="f94bb-189">Ziet u uw toepassing hello emulator uitgevoerd op een webbrowser openen en bladeren door toohello lokaal adres wordt weergegeven in de uitvoer Hallo (`http://127.0.0.1:81` in bovenstaande Hallo voorbeeld van uitvoer).</span><span class="sxs-lookup"><span data-stu-id="f94bb-189">You can see your application running in hello emulator by opening a web browser and browsing toohello local address shown in hello output (`http://127.0.0.1:81` in hello example output above).</span></span>

<span data-ttu-id="f94bb-190">toostop hello emulators, deze opdracht wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="f94bb-190">toostop hello emulators, execute this command:</span></span>

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a><span data-ttu-id="f94bb-191">Uw toepassing publiceren</span><span class="sxs-lookup"><span data-stu-id="f94bb-191">Publish your application</span></span>
<span data-ttu-id="f94bb-192">toopublish uw toepassing, moet u toofirst importeren uw publicatie-instellingen met behulp van Hallo [importeren AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f94bb-192">toopublish your application, you need toofirst import your publish settings by using hello [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span></span> <span data-ttu-id="f94bb-193">Vervolgens u uw toepassing publiceren kunt met behulp van Hallo [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f94bb-193">Then you can publish your application by using hello [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span></span> <span data-ttu-id="f94bb-194">Zie voor meer informatie over het ondertekenen van [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f94bb-194">For information about signing in, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f94bb-195">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f94bb-195">Next steps</span></span>
<span data-ttu-id="f94bb-196">Zie voor meer informatie, Hallo [PHP-ontwikkelaarscentrum](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="f94bb-196">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

[Azure SDK voor PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[definitie (.csdef)]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[serviceconfiguratie (.cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[sqlncli.msi x64 installatieprogramma]: http://go.microsoft.com/fwlink/?LinkID=239648
