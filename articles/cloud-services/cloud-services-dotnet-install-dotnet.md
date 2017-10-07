---
title: aaaInstall .NET op Azure Cloud Services-functies | Microsoft Docs
description: Dit artikel wordt beschreven hoe toomanually Hallo .NET Framework op web- en werkrollen rollen van uw cloudservice installeren
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
ms.openlocfilehash: 45f0f30221292f98c591511b091b02ebe1c1272c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-net-on-azure-cloud-services-roles"></a><span data-ttu-id="09bed-103">.NET installeren op Azure Cloud Services-functies</span><span class="sxs-lookup"><span data-stu-id="09bed-103">Install .NET on Azure Cloud Services roles</span></span>
<span data-ttu-id="09bed-104">Dit artikel wordt beschreven hoe tooinstall versies van .NET Framework die niet geleverd met Azure-Gastbesturingssysteemreleases Hallo.</span><span class="sxs-lookup"><span data-stu-id="09bed-104">This article describes how tooinstall versions of .NET Framework that don't come with hello Azure Guest OS.</span></span> <span data-ttu-id="09bed-105">U kunt .NET web- en werkrollen rollen van uw cloudservice op Hallo Gastbesturingssysteem tooconfigure gebruiken.</span><span class="sxs-lookup"><span data-stu-id="09bed-105">You can use .NET on hello Guest OS tooconfigure your cloud service web and worker roles.</span></span>

<span data-ttu-id="09bed-106">U kunt bijvoorbeeld .NET 4.6.1 installeren op Hallo Gast OS-familie 4, die niet worden geleverd met een release van .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="09bed-106">For example, you can install .NET 4.6.1 on hello Guest OS family 4, which doesn't come with any release of .NET 4.6.</span></span> <span data-ttu-id="09bed-107">(Hallo Gast OS-familie 5 maakt deel uit van .NET 4.6). Voor de meest recente informatie Hallo op Hallo Azure Gast OS releases, Zie Hallo [Azure Gast OS release nieuws](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="09bed-107">(hello Guest OS family 5 does come with .NET 4.6.) For hello latest information on hello Azure Guest OS releases, see hello [Azure Guest OS release news](cloud-services-guestos-update-matrix.md).</span></span> 

>[!IMPORTANT]
><span data-ttu-id="09bed-108">Hello Azure SDK 2.9 bevat een beperking van de .NET 4.6 op Hallo Gast OS-familie 4 of eerder is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="09bed-108">hello Azure SDK 2.9 contains a restriction on deploying .NET 4.6 on hello Guest OS family 4 or earlier.</span></span> <span data-ttu-id="09bed-109">Een oplossing voor Hallo-beperking is beschikbaar op Hallo [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span><span class="sxs-lookup"><span data-stu-id="09bed-109">A fix for hello restriction is available on hello [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span></span>

<span data-ttu-id="09bed-110">tooinstall .NET op de functies van uw web- en werkrollen, Hallo .NET web installer als onderdeel van uw cloudserviceproject opgenomen.</span><span class="sxs-lookup"><span data-stu-id="09bed-110">tooinstall .NET on your web and worker roles, include hello .NET web installer as part of your cloud service project.</span></span> <span data-ttu-id="09bed-111">Hallo-installatieprogramma starten als onderdeel van het Hallo-rol starten van de taken.</span><span class="sxs-lookup"><span data-stu-id="09bed-111">Start hello installer as part of hello role's startup tasks.</span></span> 

## <a name="add-hello-net-installer-tooyour-project"></a><span data-ttu-id="09bed-112">Hallo .NET installatieprogramma tooyour project toevoegen</span><span class="sxs-lookup"><span data-stu-id="09bed-112">Add hello .NET installer tooyour project</span></span>
<span data-ttu-id="09bed-113">toodownload hello webinstallatieprogramma voor .NET Framework, Hallo Hallo-versie die u wilt dat tooinstall kiezen:</span><span class="sxs-lookup"><span data-stu-id="09bed-113">toodownload hello web installer for hello .NET Framework, choose hello version that you want tooinstall:</span></span>

* [<span data-ttu-id="09bed-114">.NET-4.7 webinstallatie</span><span class="sxs-lookup"><span data-stu-id="09bed-114">.NET 4.7 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=825298)
* [<span data-ttu-id="09bed-115">.NET 4.6.1 web-installatieprogramma</span><span class="sxs-lookup"><span data-stu-id="09bed-115">.NET 4.6.1 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=671729)

<span data-ttu-id="09bed-116">tooadd hello installatieprogramma voor een *web* rol:</span><span class="sxs-lookup"><span data-stu-id="09bed-116">tooadd hello installer for a *web* role:</span></span>
  1. <span data-ttu-id="09bed-117">In **Solution Explorer**onder **rollen** in uw cloudserviceproject met de rechtermuisknop op uw *web* rol en selecteer **toevoegen**  >  **Nieuwe map**.</span><span class="sxs-lookup"><span data-stu-id="09bed-117">In **Solution Explorer**, under **Roles** in your cloud service project, right-click your *web* role and select **Add** > **New Folder**.</span></span> <span data-ttu-id="09bed-118">Maak een map met de naam **bin**.</span><span class="sxs-lookup"><span data-stu-id="09bed-118">Create a folder named **bin**.</span></span>
  2. <span data-ttu-id="09bed-119">Hallo bin-map met de rechtermuisknop en selecteer **toevoegen** > **bestaand Item**.</span><span class="sxs-lookup"><span data-stu-id="09bed-119">Right-click hello bin folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="09bed-120">Hallo .NET-installatieprogramma selecteren en toe te voegen toohello bin-map.</span><span class="sxs-lookup"><span data-stu-id="09bed-120">Select hello .NET installer and add it toohello bin folder.</span></span>
  
<span data-ttu-id="09bed-121">tooadd hello installatieprogramma voor een *worker* rol:</span><span class="sxs-lookup"><span data-stu-id="09bed-121">tooadd hello installer for a *worker* role:</span></span>
* <span data-ttu-id="09bed-122">Met de rechtermuisknop op uw *worker* rol en selecteer **toevoegen** > **bestaand Item**.</span><span class="sxs-lookup"><span data-stu-id="09bed-122">Right-click your *worker* role and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="09bed-123">Selecteer Hallo .NET installatieprogramma en voeg deze toohello rol.</span><span class="sxs-lookup"><span data-stu-id="09bed-123">Select hello .NET installer and add it toohello role.</span></span> 

<span data-ttu-id="09bed-124">Wanneer bestanden in deze manier toohello rol content map worden toegevoegd, zijn ze automatisch tooyour cloud servicepakket toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="09bed-124">When files are added in this way toohello role content folder, they're automatically added tooyour cloud service package.</span></span> <span data-ttu-id="09bed-125">Hallo bestanden zijn dan geïmplementeerde tooa consistente locatie op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="09bed-125">hello files are then deployed tooa consistent location on hello virtual machine.</span></span> <span data-ttu-id="09bed-126">Herhaal dit proces voor elke rol web- en werkrollen in uw cloudservice zodat alle rollen een kopie van het Hallo-installatieprogramma hebben.</span><span class="sxs-lookup"><span data-stu-id="09bed-126">Repeat this process for each web and worker role in your cloud service so that all roles have a copy of hello installer.</span></span>

> [!NOTE]
> <span data-ttu-id="09bed-127">Zelfs als uw toepassing .NET 4.6 gericht, moet u .NET 4.6.1 installeren op uw cloud service-rol.</span><span class="sxs-lookup"><span data-stu-id="09bed-127">You should install .NET 4.6.1 on your cloud service role even if your application targets .NET 4.6.</span></span> <span data-ttu-id="09bed-128">Hallo Gastbesturingssysteem bevat Hallo kennisdatabase [bijwerken 3098779](https://support.microsoft.com/kb/3098779) en [3097997 bijwerken](https://support.microsoft.com/kb/3097997).</span><span class="sxs-lookup"><span data-stu-id="09bed-128">hello Guest OS includes hello Knowledge Base [update 3098779](https://support.microsoft.com/kb/3098779) and [update 3097997](https://support.microsoft.com/kb/3097997).</span></span> <span data-ttu-id="09bed-129">Problemen kunnen optreden tijdens het uitvoeren van uw .NET-toepassingen als .NET 4.6 boven op Hallo Knowledge Base-updates is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="09bed-129">Issues can occur when you run your .NET applications if .NET 4.6 is installed on top of hello Knowledge Base updates.</span></span> <span data-ttu-id="09bed-130">Deze problemen, tooavoid installeren .NET 4.6.1 in plaats van versie 4.6.</span><span class="sxs-lookup"><span data-stu-id="09bed-130">tooavoid these issues, install .NET 4.6.1 rather than version 4.6.</span></span> <span data-ttu-id="09bed-131">Zie voor meer informatie, Hallo [Knowledge Base-artikel 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="09bed-131">For more information, see hello [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
> 
> 

![Inhoud van de rol met installer-bestanden][1]

## <a name="define-startup-tasks-for-your-roles"></a><span data-ttu-id="09bed-133">Starten van de taken voor uw rollen definiëren</span><span class="sxs-lookup"><span data-stu-id="09bed-133">Define startup tasks for your roles</span></span>
<span data-ttu-id="09bed-134">U kunt opstarten taken tooperform operations voordat een rol wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="09bed-134">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="09bed-135">Hallo .NET Framework installeren als onderdeel van de taak voor het opstarten van Hallo zorgt ervoor dat Hallo-framework is geïnstalleerd voordat een toepassingscode wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="09bed-135">Installing hello .NET Framework as part of hello startup task ensures that hello framework is installed before any application code is run.</span></span> <span data-ttu-id="09bed-136">Zie voor meer informatie over het starten van de taken, [starten van de taken uitvoeren in Azure](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="09bed-136">For more information on startup tasks, see [Run startup tasks in Azure](cloud-services-startup-tasks.md).</span></span> 

1. <span data-ttu-id="09bed-137">Toevoegen van de volgende inhoud toohello ServiceDefinition.csdef onder Hallo Hallo **WebRole** of **WorkerRole** knooppunt voor alle rollen:</span><span class="sxs-lookup"><span data-stu-id="09bed-137">Add hello following content toohello ServiceDefinition.csdef file under hello **WebRole** or **WorkerRole** node for all roles:</span></span>
   
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
   
    <span data-ttu-id="09bed-138">Hallo voorgaande configuratie Hallo console-opdracht uitvoert `install.cmd` met administrator-bevoegdheden tooinstall Hallo .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="09bed-138">hello preceding configuration runs hello console command `install.cmd` with administrator privileges tooinstall hello .NET Framework.</span></span> <span data-ttu-id="09bed-139">Hallo configuratie maakt ook een **LocalStorage** element met de naam **NETFXInstall**.</span><span class="sxs-lookup"><span data-stu-id="09bed-139">hello configuration also creates a **LocalStorage** element named **NETFXInstall**.</span></span> <span data-ttu-id="09bed-140">Hallo opstartscript stelt Hallo tijdelijke map toouse deze resource lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="09bed-140">hello startup script sets hello temp folder toouse this local storage resource.</span></span> 
    
    > [!IMPORTANT]
    > <span data-ttu-id="09bed-141">tooensure Corrigeer de installatie van Hallo framework, Hallo grootte van deze resource tooat minste 1024 MB.</span><span class="sxs-lookup"><span data-stu-id="09bed-141">tooensure correct installation of hello framework, set hello size of this resource tooat least 1,024 MB.</span></span>
    
    <span data-ttu-id="09bed-142">Zie voor meer informatie over het starten van de taken [algemene Azure Cloud Services starten van de taken](cloud-services-startup-tasks-common.md).</span><span class="sxs-lookup"><span data-stu-id="09bed-142">For more information about startup tasks, see [Common Azure Cloud Services startup tasks](cloud-services-startup-tasks-common.md).</span></span>

2. <span data-ttu-id="09bed-143">Maak een bestand met de naam **install.cmd** en voeg de volgende Hallo scriptbestand toohello installeren.</span><span class="sxs-lookup"><span data-stu-id="09bed-143">Create a file named **install.cmd** and add hello following install script toohello file.</span></span>

    <span data-ttu-id="09bed-144">Hallo-script wordt gecontroleerd of Hallo opgegeven versie van .NET Framework Hallo al is geïnstalleerd op machine Hallo door het controleren van het Hallo-register.</span><span class="sxs-lookup"><span data-stu-id="09bed-144">hello script checks whether hello specified version of hello .NET Framework is already installed on hello machine by querying hello registry.</span></span> <span data-ttu-id="09bed-145">Als Hallo .NET versie niet is geïnstalleerd, wordt Hallo .NET webinstallatie geopend.</span><span class="sxs-lookup"><span data-stu-id="09bed-145">If hello .NET version is not installed, then hello .NET web installer is opened.</span></span> <span data-ttu-id="09bed-146">toohelp los eventuele problemen, Hallo script registreert alle activiteiten toohello bestand startuptasklog-(de huidige datum en tijd) .txt die is opgeslagen in **InstallLogs** lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="09bed-146">toohelp troubleshoot any issues, hello script logs all activity toohello file startuptasklog-(current date and time).txt that is stored in **InstallLogs** local storage.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="09bed-147">Gebruik een elementaire teksteditor zoals Kladblok Windows toocreate Hallo install.cmd-bestand.</span><span class="sxs-lookup"><span data-stu-id="09bed-147">Use a basic text editor like Windows Notepad toocreate hello install.cmd file.</span></span> <span data-ttu-id="09bed-148">Als u Visual Studio toocreate een tekstbestand en Hallo extensie too.cmd verandert, kan Hallo-bestand nog steeds een UTF-8-bytevolgordemarkering bevatten.</span><span class="sxs-lookup"><span data-stu-id="09bed-148">If you use Visual Studio toocreate a text file and change hello extension too.cmd, hello file might still contain a UTF-8 byte order mark.</span></span> <span data-ttu-id="09bed-149">Dit is ingeschakeld kan een fout veroorzaken wanneer de eerste regel Hallo van Hallo-script wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="09bed-149">This mark can cause an error when hello first line of hello script is run.</span></span> <span data-ttu-id="09bed-150">tooavoid deze fout Hallo eerste regel Hallo script een een-instructie die door de verwerking van Hallo byte worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="09bed-150">tooavoid this error, make hello first line of hello script a REM statement that can be skipped by hello byte order processing.</span></span> 
    > 
    >
   
    ```cmd
    REM Set hello value of netfx tooinstall appropriate .NET Framework. 
    REM ***** tooinstall .NET 4.5.2 set hello variable netfx too"NDP452" *****
    REM ***** tooinstall .NET 4.6 set hello variable netfx too"NDP46" *****
    REM ***** tooinstall .NET 4.6.1 set hello variable netfx too"NDP461" *****
    REM ***** tooinstall .NET 4.6.2 set hello variable netfx too"NDP462" *****
    REM ***** tooinstall .NET 4.7 set hello variable netfx too"NDP47" *****
    set netfx="NDP47"

    REM ***** Set script start timestamp *****
    set timehour=%time:~0,2%
    set timestamp=%date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2%
    set "log=install.cmd started %timestamp%."

    REM ***** Exit script if running in Emulator *****
    if %ComputeEmulatorRunning%=="true" goto exit

    REM ***** Needed toocorrectly install .NET 4.6.1, otherwise you may see an out of disk space error *****
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
    echo Restarting toocomplete .NET (%netfx%) installation >> %startuptasklog%
    EXIT /B %ERRORLEVEL%

    :installed
    echo .NET (%netfx%) is installed >> %startuptasklog%

    :end
    echo install.cmd completed: %date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2% >> %startuptasklog%

    :exit
    EXIT /B 0
    ```
   
   > [!NOTE]
   > <span data-ttu-id="09bed-151">Dit script toont hoe hello Azure Gast OS tooinstall .NET 4.5.2 of versie 4.6 voor bedrijfscontinuïteit, zelfs als er geen .NET 4.5.2 is al beschikbaar op.</span><span class="sxs-lookup"><span data-stu-id="09bed-151">This script shows how tooinstall .NET 4.5.2 or version 4.6 for continuity, even though .NET 4.5.2 is already available on hello Azure Guest OS.</span></span> <span data-ttu-id="09bed-152">U moet rechtstreeks installeren .NET 4.6.1 in plaats van versie 4.6, zoals beschreven in Hallo [Knowledge Base-artikel 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="09bed-152">You should directly install .NET 4.6.1 rather than version 4.6, as described in hello [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
   > 
   > 

3. <span data-ttu-id="09bed-153">Hallo install.cmd bestand tooeach functie toevoegen met behulp van **toevoegen** > **bestaand Item** in **Solution Explorer** zoals eerder in dit onderwerp beschreven.</span><span class="sxs-lookup"><span data-stu-id="09bed-153">Add hello install.cmd file tooeach role by using **Add** > **Existing Item** in **Solution Explorer** as described earlier in this topic.</span></span> 

    <span data-ttu-id="09bed-154">Nadat deze stap voltooid is, moeten alle rollen Hallo .NET-installatiebestand en Hallo install.cmd bestand hebben.</span><span class="sxs-lookup"><span data-stu-id="09bed-154">After this step is complete, all roles should have hello .NET installer file and hello install.cmd file.</span></span>

   ![Inhoud van de rol met alle bestanden][2]

## <a name="configure-diagnostics-tootransfer-startup-logs-tooblob-storage"></a><span data-ttu-id="09bed-156">Diagnostische gegevens tootransfer opstarten logboeken tooBlob opslag configureren</span><span class="sxs-lookup"><span data-stu-id="09bed-156">Configure Diagnostics tootransfer startup logs tooBlob storage</span></span>
<span data-ttu-id="09bed-157">toosimplify het oplossen van installatieproblemen, kunt u Azure Diagnostics tootransfer alle logboekbestanden die worden gegenereerd door Hallo opstarten script of Hallo .NET installatieprogramma tooAzure Blob-opslag configureren.</span><span class="sxs-lookup"><span data-stu-id="09bed-157">toosimplify troubleshooting installation issues, you can configure Azure Diagnostics tootransfer any log files generated by hello startup script or hello .NET installer tooAzure Blob storage.</span></span> <span data-ttu-id="09bed-158">U kunt met behulp van deze benadering Hallo logboeken weergeven door logboekbestanden Hallo downloaden van Blob-opslag hoeft u geen tooremote bureaublad tot Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="09bed-158">By using this approach, you can view hello logs by downloading hello log files from Blob storage rather than having tooremote desktop into hello role.</span></span>

<span data-ttu-id="09bed-159">tooconfigure Diagnostics, Hallo diagnostics.wadcfgx bestand openen en volgen inhoud onder Hallo Hallo toevoegen **mappen** knooppunt:</span><span class="sxs-lookup"><span data-stu-id="09bed-159">tooconfigure Diagnostics, open hello diagnostics.wadcfgx file and add hello following content under hello **Directories** node:</span></span> 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

<span data-ttu-id="09bed-160">Deze XML Diagnostics tootransfer Hallo bestanden configureert in de logboekmap Hallo in Hallo **NETFXInstall** resource toohello opslagaccount voor diagnostische gegevens in Hallo **netfx-Installeer** blob-container.</span><span class="sxs-lookup"><span data-stu-id="09bed-160">This XML configures Diagnostics tootransfer hello files in hello log directory in hello **NETFXInstall** resource toohello Diagnostics storage account in hello **netfx-install** blob container.</span></span>

## <a name="deploy-your-cloud-service"></a><span data-ttu-id="09bed-161">Uw cloudservice implementeren</span><span class="sxs-lookup"><span data-stu-id="09bed-161">Deploy your cloud service</span></span>
<span data-ttu-id="09bed-162">Wanneer u uw cloudservice implementeert, installeer Hallo starten van de taken Hallo .NET Framework als deze nog niet is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="09bed-162">When you deploy your cloud service, hello startup tasks install hello .NET Framework if it's not already installed.</span></span> <span data-ttu-id="09bed-163">Uw cloud service-rollen zich in Hallo *bezet* status tijdens het Hallo-framework wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="09bed-163">Your cloud service roles are in hello *busy* state while hello framework is being installed.</span></span> <span data-ttu-id="09bed-164">Als Hallo framework-installatie opnieuw opstarten vereist, Hallo service functies mogelijk ook opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="09bed-164">If hello framework installation requires a restart, hello service roles might also restart.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="09bed-165">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="09bed-165">Additional resources</span></span>
* <span data-ttu-id="09bed-166">[Hallo .NET Framework installeren][Installing hello .NET Framework]</span><span class="sxs-lookup"><span data-stu-id="09bed-166">[Installing hello .NET Framework][Installing hello .NET Framework]</span></span>
* <span data-ttu-id="09bed-167">[Bepalen welke versies van .NET Framework zijn geïnstalleerd][How to: Determine Which .NET Framework Versions Are Installed]</span><span class="sxs-lookup"><span data-stu-id="09bed-167">[Determine which .NET Framework versions are installed][How to: Determine Which .NET Framework Versions Are Installed]</span></span>
* <span data-ttu-id="09bed-168">[Het oplossen van de installatie van .NET Framework][Troubleshooting .NET Framework Installations]</span><span class="sxs-lookup"><span data-stu-id="09bed-168">[Troubleshooting .NET Framework installations][Troubleshooting .NET Framework Installations]</span></span>

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing hello .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
