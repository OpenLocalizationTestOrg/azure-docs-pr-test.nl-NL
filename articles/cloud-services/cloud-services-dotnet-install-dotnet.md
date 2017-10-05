---
title: .NET installeren op Azure Cloud Services-functies | Microsoft Docs
description: Dit artikel wordt beschreven hoe u .NET Framework handmatig installeren op web- en werkrollen rollen van uw cloudservice
services: cloud-services
documentationcenter: .net
author: thraka
manager: timlt
editor: 
ms.assetid: 8d1243dc-879c-4d1f-9ed0-eecd1f6a6653
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: adegeo
ms.openlocfilehash: a9cffa275ae6b9315b821d3160b17a997a1523f7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="install-net-on-azure-cloud-services-roles"></a><span data-ttu-id="7b147-103">.NET installeren op Azure Cloud Services-functies</span><span class="sxs-lookup"><span data-stu-id="7b147-103">Install .NET on Azure Cloud Services roles</span></span>
<span data-ttu-id="7b147-104">In dit artikel beschrijft het installeren van versies van .NET Framework die niet bij de Azure-Gastbesturingssysteemreleases worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="7b147-104">This article describes how to install versions of .NET Framework that don't come with the Azure Guest OS.</span></span> <span data-ttu-id="7b147-105">U kunt op het Gastbesturingssysteem .NET web- en werkrollen rollen van uw cloudservice te configureren.</span><span class="sxs-lookup"><span data-stu-id="7b147-105">You can use .NET on the Guest OS to configure your cloud service web and worker roles.</span></span>

<span data-ttu-id="7b147-106">U kunt bijvoorbeeld .NET 4.6.1 installeren op de Gast OS-familie 4, die niet worden geleverd met een release van .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="7b147-106">For example, you can install .NET 4.6.1 on the Guest OS family 4, which doesn't come with any release of .NET 4.6.</span></span> <span data-ttu-id="7b147-107">(De Gast OS-familie 5 maakt deel uit van .NET 4.6). Zie voor de nieuwste informatie over de Azure Gast OS-versies, de [Azure Gast OS release nieuws](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="7b147-107">(The Guest OS family 5 does come with .NET 4.6.) For the latest information on the Azure Guest OS releases, see the [Azure Guest OS release news](cloud-services-guestos-update-matrix.md).</span></span> 

>[!IMPORTANT]
><span data-ttu-id="7b147-108">De Azure SDK 2.9 bevat een beperking van de .NET 4.6 op de Gast OS-familie 4 of eerder is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="7b147-108">The Azure SDK 2.9 contains a restriction on deploying .NET 4.6 on the Guest OS family 4 or earlier.</span></span> <span data-ttu-id="7b147-109">Er is een oplossing voor de beperking die beschikbaar is op de [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span><span class="sxs-lookup"><span data-stu-id="7b147-109">A fix for the restriction is available on the [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span></span>

<span data-ttu-id="7b147-110">Om .NET te installeren op uw web- en werkrollen rollen, omvatten het webinstallatieprogramma voor .NET als onderdeel van uw cloudserviceproject.</span><span class="sxs-lookup"><span data-stu-id="7b147-110">To install .NET on your web and worker roles, include the .NET web installer as part of your cloud service project.</span></span> <span data-ttu-id="7b147-111">Het installatieprogramma starten als onderdeel van de rol starten van de taken.</span><span class="sxs-lookup"><span data-stu-id="7b147-111">Start the installer as part of the role's startup tasks.</span></span> 

## <a name="add-the-net-installer-to-your-project"></a><span data-ttu-id="7b147-112">Het installatieprogramma voor .NET aan uw project toevoegen</span><span class="sxs-lookup"><span data-stu-id="7b147-112">Add the .NET installer to your project</span></span>
<span data-ttu-id="7b147-113">Voor het downloaden van het webinstallatieprogramma voor .NET Framework, kiest u de versie die u wilt installeren:</span><span class="sxs-lookup"><span data-stu-id="7b147-113">To download the web installer for the .NET Framework, choose the version that you want to install:</span></span>

* [<span data-ttu-id="7b147-114">.NET-4.7 webinstallatie</span><span class="sxs-lookup"><span data-stu-id="7b147-114">.NET 4.7 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=825298)
* [<span data-ttu-id="7b147-115">.NET 4.6.1 web-installatieprogramma</span><span class="sxs-lookup"><span data-stu-id="7b147-115">.NET 4.6.1 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=671729)

<span data-ttu-id="7b147-116">Toevoegen van het installatieprogramma voor een *web* rol:</span><span class="sxs-lookup"><span data-stu-id="7b147-116">To add the installer for a *web* role:</span></span>
  1. <span data-ttu-id="7b147-117">In **Solution Explorer**onder **rollen** in uw cloudserviceproject met de rechtermuisknop op uw *web* rol en selecteer **toevoegen**  >  **Nieuwe map**.</span><span class="sxs-lookup"><span data-stu-id="7b147-117">In **Solution Explorer**, under **Roles** in your cloud service project, right-click your *web* role and select **Add** > **New Folder**.</span></span> <span data-ttu-id="7b147-118">Maak een map met de naam **bin**.</span><span class="sxs-lookup"><span data-stu-id="7b147-118">Create a folder named **bin**.</span></span>
  2. <span data-ttu-id="7b147-119">Met de rechtermuisknop op de bin-map en selecteer **toevoegen** > **bestaand Item**.</span><span class="sxs-lookup"><span data-stu-id="7b147-119">Right-click the bin folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="7b147-120">Het .NET-installatieprogramma selecteren en toe te voegen aan de bin-map.</span><span class="sxs-lookup"><span data-stu-id="7b147-120">Select the .NET installer and add it to the bin folder.</span></span>
  
<span data-ttu-id="7b147-121">Toevoegen van het installatieprogramma voor een *worker* rol:</span><span class="sxs-lookup"><span data-stu-id="7b147-121">To add the installer for a *worker* role:</span></span>
* <span data-ttu-id="7b147-122">Met de rechtermuisknop op uw *worker* rol en selecteer **toevoegen** > **bestaand Item**.</span><span class="sxs-lookup"><span data-stu-id="7b147-122">Right-click your *worker* role and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="7b147-123">Het .NET-installatieprogramma selecteren en toe te voegen aan de rol.</span><span class="sxs-lookup"><span data-stu-id="7b147-123">Select the .NET installer and add it to the role.</span></span> 

<span data-ttu-id="7b147-124">Wanneer bestanden worden toegevoegd op deze manier naar de inhoudsmap van de rol, zijn ze automatisch toegevoegd aan uw cloud-pakket.</span><span class="sxs-lookup"><span data-stu-id="7b147-124">When files are added in this way to the role content folder, they're automatically added to your cloud service package.</span></span> <span data-ttu-id="7b147-125">De bestanden zijn geïmplementeerd op een consistente locatie op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7b147-125">The files are then deployed to a consistent location on the virtual machine.</span></span> <span data-ttu-id="7b147-126">Herhaal dit proces voor elke rol web- en werkrollen in uw cloudservice zodat alle rollen een kopie van het installatieprogramma hebben.</span><span class="sxs-lookup"><span data-stu-id="7b147-126">Repeat this process for each web and worker role in your cloud service so that all roles have a copy of the installer.</span></span>

> [!NOTE]
> <span data-ttu-id="7b147-127">Zelfs als uw toepassing .NET 4.6 gericht, moet u .NET 4.6.1 installeren op uw cloud service-rol.</span><span class="sxs-lookup"><span data-stu-id="7b147-127">You should install .NET 4.6.1 on your cloud service role even if your application targets .NET 4.6.</span></span> <span data-ttu-id="7b147-128">Het Gastbesturingssysteem bevat de Knowledge Base [bijwerken 3098779](https://support.microsoft.com/kb/3098779) en [3097997 bijwerken](https://support.microsoft.com/kb/3097997).</span><span class="sxs-lookup"><span data-stu-id="7b147-128">The Guest OS includes the Knowledge Base [update 3098779](https://support.microsoft.com/kb/3098779) and [update 3097997](https://support.microsoft.com/kb/3097997).</span></span> <span data-ttu-id="7b147-129">Problemen kunnen optreden tijdens het uitvoeren van uw .NET-toepassingen als .NET 4.6 is geïnstalleerd op de Knowledge Base-updates.</span><span class="sxs-lookup"><span data-stu-id="7b147-129">Issues can occur when you run your .NET applications if .NET 4.6 is installed on top of the Knowledge Base updates.</span></span> <span data-ttu-id="7b147-130">Om te voorkomen dat deze problemen, installeert u .NET 4.6.1 in plaats van versie 4.6.</span><span class="sxs-lookup"><span data-stu-id="7b147-130">To avoid these issues, install .NET 4.6.1 rather than version 4.6.</span></span> <span data-ttu-id="7b147-131">Zie voor meer informatie de [Knowledge Base-artikel 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="7b147-131">For more information, see the [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
> 
> 

![Inhoud van de rol met installer-bestanden][1]

## <a name="define-startup-tasks-for-your-roles"></a><span data-ttu-id="7b147-133">Starten van de taken voor uw rollen definiëren</span><span class="sxs-lookup"><span data-stu-id="7b147-133">Define startup tasks for your roles</span></span>
<span data-ttu-id="7b147-134">Starten van de taken kunt u bewerkingen uitvoeren voordat een rol wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="7b147-134">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="7b147-135">Installatie van .NET Framework als onderdeel van de opstarttaak zorgt ervoor dat het framework is geïnstalleerd voordat een toepassingscode wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7b147-135">Installing the .NET Framework as part of the startup task ensures that the framework is installed before any application code is run.</span></span> <span data-ttu-id="7b147-136">Zie voor meer informatie over het starten van de taken, [starten van de taken uitvoeren in Azure](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="7b147-136">For more information on startup tasks, see [Run startup tasks in Azure](cloud-services-startup-tasks.md).</span></span> 

1. <span data-ttu-id="7b147-137">De volgende inhoud toevoegen aan het bestand ServiceDefinition.csdef onder de **WebRole** of **WorkerRole** knooppunt voor alle rollen:</span><span class="sxs-lookup"><span data-stu-id="7b147-137">Add the following content to the ServiceDefinition.csdef file under the **WebRole** or **WorkerRole** node for all roles:</span></span>
   
    ```xml
    <LocalResources>
      <LocalStorage name="NETFXInstall" sizeInMB="1024" cleanOnRoleRecycle="false" />
    </LocalResources>    
    <Startup>
      <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
        <Environment>
          <Variable name="PathToNETFXInstall">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='NETFXInstall']/@path" />
          </Variable>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
    ```
   
    <span data-ttu-id="7b147-138">De console-opdracht wordt uitgevoerd in de configuratie van de voorgaande `install.cmd` met administrator-bevoegdheden voor het installeren van .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="7b147-138">The preceding configuration runs the console command `install.cmd` with administrator privileges to install the .NET Framework.</span></span> <span data-ttu-id="7b147-139">De configuratie maakt ook een **LocalStorage** element met de naam **NETFXInstall**.</span><span class="sxs-lookup"><span data-stu-id="7b147-139">The configuration also creates a **LocalStorage** element named **NETFXInstall**.</span></span> <span data-ttu-id="7b147-140">Het opstartscript Hiermee stelt u de map temp deze bron lokale opslag gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7b147-140">The startup script sets the temp folder to use this local storage resource.</span></span> 
    
    > [!IMPORTANT]
    > <span data-ttu-id="7b147-141">Als u wilt correcte installatie van het framework, stelt u de grootte van deze resource op ten minste 1024 MB.</span><span class="sxs-lookup"><span data-stu-id="7b147-141">To ensure correct installation of the framework, set the size of this resource to at least 1,024 MB.</span></span>
    
    <span data-ttu-id="7b147-142">Zie voor meer informatie over het starten van de taken [algemene Azure Cloud Services starten van de taken](cloud-services-startup-tasks-common.md).</span><span class="sxs-lookup"><span data-stu-id="7b147-142">For more information about startup tasks, see [Common Azure Cloud Services startup tasks](cloud-services-startup-tasks-common.md).</span></span>

2. <span data-ttu-id="7b147-143">Maak een bestand met de naam **install.cmd** en voeg het volgende script naar het bestand installeren.</span><span class="sxs-lookup"><span data-stu-id="7b147-143">Create a file named **install.cmd** and add the following install script to the file.</span></span>

    <span data-ttu-id="7b147-144">Het script wordt gecontroleerd of de opgegeven versie van .NET Framework is al geïnstalleerd op de computer door het opvragen van het register.</span><span class="sxs-lookup"><span data-stu-id="7b147-144">The script checks whether the specified version of the .NET Framework is already installed on the machine by querying the registry.</span></span> <span data-ttu-id="7b147-145">Als u de .NET-versie niet is geïnstalleerd, wordt het installatieprogramma van .NET web geopend.</span><span class="sxs-lookup"><span data-stu-id="7b147-145">If the .NET version is not installed, then the .NET web installer is opened.</span></span> <span data-ttu-id="7b147-146">Voor het oplossen van problemen, registreert het script alle activiteiten in het bestand startuptasklog-(de huidige datum en tijd) .txt die is opgeslagen in **InstallLogs** lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="7b147-146">To help troubleshoot any issues, the script logs all activity to the file startuptasklog-(current date and time).txt that is stored in **InstallLogs** local storage.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="7b147-147">Gebruik een elementaire teksteditor zoals Kladblok Windows het install.cmd-bestand te maken.</span><span class="sxs-lookup"><span data-stu-id="7b147-147">Use a basic text editor like Windows Notepad to create the install.cmd file.</span></span> <span data-ttu-id="7b147-148">Als u Visual Studio gebruikt voor het maken van een tekstbestand en wijzigt u de extensie in .cmd, kan het bestand nog steeds een UTF-8-bytevolgordemarkering bevatten.</span><span class="sxs-lookup"><span data-stu-id="7b147-148">If you use Visual Studio to create a text file and change the extension to .cmd, the file might still contain a UTF-8 byte order mark.</span></span> <span data-ttu-id="7b147-149">Deze is ingeschakeld, kan een fout veroorzaken wanneer de eerste regel van het script wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7b147-149">This mark can cause an error when the first line of the script is run.</span></span> <span data-ttu-id="7b147-150">Om te voorkomen dat deze fout, moet u de eerste regel van het script een een-instructie die door de verwerking van de volgorde byte worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7b147-150">To avoid this error, make the first line of the script a REM statement that can be skipped by the byte order processing.</span></span> 
    > 
    >
   
    ```cmd
    REM Set the value of netfx to install appropriate .NET Framework. 
    REM ***** To install .NET 4.5.2 set the variable netfx to "NDP452" *****
    REM ***** To install .NET 4.6 set the variable netfx to "NDP46" *****
    REM ***** To install .NET 4.6.1 set the variable netfx to "NDP461" *****
    REM ***** To install .NET 4.6.2 set the variable netfx to "NDP462" *****
    REM ***** To install .NET 4.7 set the variable netfx to "NDP47" *****
    set netfx="NDP47"

    REM ***** Set script start timestamp *****
    set timehour=%time:~0,2%
    set timestamp=%date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2%
    set "log=install.cmd started %timestamp%."

    REM ***** Exit script if running in Emulator *****
    if %ComputeEmulatorRunning%=="true" goto exit

    REM ***** Needed to correctly install .NET 4.6.1, otherwise you may see an out of disk space error *****
    set TMP=%PathToNETFXInstall%
    set TEMP=%PathToNETFXInstall%

    REM ***** Setup .NET filenames and registry keys *****
    if %netfx%=="NDP47" goto NDP47
    if %netfx%=="NDP462" goto NDP462
    if %netfx%=="NDP461" goto NDP461
    if %netfx%=="NDP46" goto NDP46
        set "netfxinstallfile=NDP452-KB2901954-Web.exe"
        set netfxregkey="0x5cbf5"
        goto logtimestamp

    :NDP46
    set "netfxinstallfile=NDP46-KB3045560-Web.exe"
    set netfxregkey="0x6004f"
    goto logtimestamp

    :NDP461
    set "netfxinstallfile=NDP461-KB3102438-Web.exe"
    set netfxregkey="0x6040e"
    goto logtimestamp

    :NDP462
    set "netfxinstallfile=NDP462-KB3151802-Web.exe"
    set netfxregkey="0x60632"

    :NDP47
    set "netfxinstallfile=NDP47-KB3186500-Web.exe"
    set netfxregkey="0x707FE"

    :logtimestamp
    REM ***** Setup LogFile with timestamp *****
    md "%PathToNETFXInstall%\log"
    set startuptasklog="%PathToNETFXInstall%log\startuptasklog-%timestamp%.txt"
    set netfxinstallerlog="%PathToNETFXInstall%log\NetFXInstallerLog-%timestamp%"
    echo %log% >> %startuptasklog%
    echo Logfile generated at: %startuptasklog% >> %startuptasklog%
    echo TMP set to: %TMP% >> %startuptasklog%
    echo TEMP set to: %TEMP% >> %startuptasklog%

    REM ***** Check if .NET is installed *****
    echo Checking if .NET (%netfx%) is installed >> %startuptasklog%
    set /A netfxregkeydecimal=%netfxregkey%
    set foundkey=0
    FOR /F "usebackq skip=2 tokens=1,2*" %%A in (`reg query "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full" /v Release 2^>nul`) do @set /A foundkey=%%C
    echo Minimum required key: %netfxregkeydecimal% -- found key: %foundkey% >> %startuptasklog%
    if %foundkey% GEQ %netfxregkeydecimal% goto installed

    REM ***** Installing .NET *****
    echo Installing .NET with commandline: start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog%  /chainingpackage "CloudService Startup Task" >> %startuptasklog%
    start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog% /chainingpackage "CloudService Startup Task" >> %startuptasklog% 2>>&1
    if %ERRORLEVEL%== 0 goto installed
        echo .NET installer exited with code %ERRORLEVEL% >> %startuptasklog%    
        if %ERRORLEVEL%== 3010 goto restart
        if %ERRORLEVEL%== 1641 goto restart
        echo .NET (%netfx%) install failed with Error Code %ERRORLEVEL%. Further logs can be found in %netfxinstallerlog% >> %startuptasklog%

    :restart
    echo Restarting to complete .NET (%netfx%) installation >> %startuptasklog%
    EXIT /B %ERRORLEVEL%

    :installed
    echo .NET (%netfx%) is installed >> %startuptasklog%

    :end
    echo install.cmd completed: %date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2% >> %startuptasklog%

    :exit
    EXIT /B 0
    ```
   
   > [!NOTE]
   > <span data-ttu-id="7b147-151">Dit script toont hoe u installeert .NET 4.5.2 of versie 4.6 voor bedrijfscontinuïteit, ondanks dat .NET 4.5.2 al beschikbaar op de Azure-Gastbesturingssysteemreleases is.</span><span class="sxs-lookup"><span data-stu-id="7b147-151">This script shows how to install .NET 4.5.2 or version 4.6 for continuity, even though .NET 4.5.2 is already available on the Azure Guest OS.</span></span> <span data-ttu-id="7b147-152">U moet rechtstreeks installeren .NET 4.6.1 in plaats van versie 4.6, zoals beschreven in de [Knowledge Base-artikel 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="7b147-152">You should directly install .NET 4.6.1 rather than version 4.6, as described in the [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
   > 
   > 

3. <span data-ttu-id="7b147-153">Het bestand install.cmd toevoegen aan elke rol met behulp van **toevoegen** > **bestaand Item** in **Solution Explorer** zoals eerder in dit onderwerp beschreven.</span><span class="sxs-lookup"><span data-stu-id="7b147-153">Add the install.cmd file to each role by using **Add** > **Existing Item** in **Solution Explorer** as described earlier in this topic.</span></span> 

    <span data-ttu-id="7b147-154">Nadat deze stap voltooid is, moeten alle rollen van het .NET-installatiebestand en het bestand install.cmd hebben.</span><span class="sxs-lookup"><span data-stu-id="7b147-154">After this step is complete, all roles should have the .NET installer file and the install.cmd file.</span></span>

   ![Inhoud van de rol met alle bestanden][2]

## <a name="configure-diagnostics-to-transfer-startup-logs-to-blob-storage"></a><span data-ttu-id="7b147-156">Diagnostische functies voor het starten van de logboeken over te dragen naar Blob-opslag configureren</span><span class="sxs-lookup"><span data-stu-id="7b147-156">Configure Diagnostics to transfer startup logs to Blob storage</span></span>
<span data-ttu-id="7b147-157">Als u wilt de het oplossen van installatieproblemen vereenvoudigen, kunt u Azure Diagnostics om over te dragen van alle logboekbestanden zijn gegenereerd door het opstartscript of het installatieprogramma .NET naar Azure Blob-opslag kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="7b147-157">To simplify troubleshooting installation issues, you can configure Azure Diagnostics to transfer any log files generated by the startup script or the .NET installer to Azure Blob storage.</span></span> <span data-ttu-id="7b147-158">Met deze benadering kunt u de logboeken bekijken door het downloaden van de logboekbestanden van Blob-opslag in plaats van dat extern bureaublad in de rol.</span><span class="sxs-lookup"><span data-stu-id="7b147-158">By using this approach, you can view the logs by downloading the log files from Blob storage rather than having to remote desktop into the role.</span></span>

<span data-ttu-id="7b147-159">Diagnostische gegevens configureren, opent u het bestand diagnostics.wadcfgx en voegt u de volgende inhoud onder de **mappen** knooppunt:</span><span class="sxs-lookup"><span data-stu-id="7b147-159">To configure Diagnostics, open the diagnostics.wadcfgx file and add the following content under the **Directories** node:</span></span> 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

<span data-ttu-id="7b147-160">Deze XML configureert u diagnostische gegevens om over te dragen van de bestanden in de logboekmap in de **NETFXInstall** resource toe aan het opslagaccount voor diagnostische gegevens in de **netfx-Installeer** blob-container.</span><span class="sxs-lookup"><span data-stu-id="7b147-160">This XML configures Diagnostics to transfer the files in the log directory in the **NETFXInstall** resource to the Diagnostics storage account in the **netfx-install** blob container.</span></span>

## <a name="deploy-your-cloud-service"></a><span data-ttu-id="7b147-161">Uw cloudservice implementeren</span><span class="sxs-lookup"><span data-stu-id="7b147-161">Deploy your cloud service</span></span>
<span data-ttu-id="7b147-162">Wanneer u uw cloudservice implementeert, installeer de taken starten van de .NET Framework als deze nog niet is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7b147-162">When you deploy your cloud service, the startup tasks install the .NET Framework if it's not already installed.</span></span> <span data-ttu-id="7b147-163">Uw cloud service-rollen zich in de *bezet* status terwijl het framework wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7b147-163">Your cloud service roles are in the *busy* state while the framework is being installed.</span></span> <span data-ttu-id="7b147-164">Als de framework-installatie opnieuw opstarten vereist, de functies van de service mogelijk ook opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="7b147-164">If the framework installation requires a restart, the service roles might also restart.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7b147-165">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="7b147-165">Additional resources</span></span>
* <span data-ttu-id="7b147-166">[Installatie van .NET Framework][Installing the .NET Framework]</span><span class="sxs-lookup"><span data-stu-id="7b147-166">[Installing the .NET Framework][Installing the .NET Framework]</span></span>
* <span data-ttu-id="7b147-167">[Bepalen welke versies van .NET Framework zijn geïnstalleerd][How to: Determine Which .NET Framework Versions Are Installed]</span><span class="sxs-lookup"><span data-stu-id="7b147-167">[Determine which .NET Framework versions are installed][How to: Determine Which .NET Framework Versions Are Installed]</span></span>
* <span data-ttu-id="7b147-168">[Het oplossen van de installatie van .NET Framework][Troubleshooting .NET Framework Installations]</span><span class="sxs-lookup"><span data-stu-id="7b147-168">[Troubleshooting .NET Framework installations][Troubleshooting .NET Framework Installations]</span></span>

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing the .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
