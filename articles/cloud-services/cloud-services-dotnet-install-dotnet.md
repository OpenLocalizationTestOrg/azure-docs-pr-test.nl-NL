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
# <a name="install-net-on-azure-cloud-services-roles"></a>.NET installeren op Azure Cloud Services-functies
Dit artikel wordt beschreven hoe tooinstall versies van .NET Framework die niet geleverd met Azure-Gastbesturingssysteemreleases Hallo. U kunt .NET web- en werkrollen rollen van uw cloudservice op Hallo Gastbesturingssysteem tooconfigure gebruiken.

U kunt bijvoorbeeld .NET 4.6.1 installeren op Hallo Gast OS-familie 4, die niet worden geleverd met een release van .NET 4.6. (Hallo Gast OS-familie 5 maakt deel uit van .NET 4.6). Voor de meest recente informatie Hallo op Hallo Azure Gast OS releases, Zie Hallo [Azure Gast OS release nieuws](cloud-services-guestos-update-matrix.md). 

>[!IMPORTANT]
>Hello Azure SDK 2.9 bevat een beperking van de .NET 4.6 op Hallo Gast OS-familie 4 of eerder is geïmplementeerd. Een oplossing voor Hallo-beperking is beschikbaar op Hallo [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.

tooinstall .NET op de functies van uw web- en werkrollen, Hallo .NET web installer als onderdeel van uw cloudserviceproject opgenomen. Hallo-installatieprogramma starten als onderdeel van het Hallo-rol starten van de taken. 

## <a name="add-hello-net-installer-tooyour-project"></a>Hallo .NET installatieprogramma tooyour project toevoegen
toodownload hello webinstallatieprogramma voor .NET Framework, Hallo Hallo-versie die u wilt dat tooinstall kiezen:

* [.NET-4.7 webinstallatie](http://go.microsoft.com/fwlink/?LinkId=825298)
* [.NET 4.6.1 web-installatieprogramma](http://go.microsoft.com/fwlink/?LinkId=671729)

tooadd hello installatieprogramma voor een *web* rol:
  1. In **Solution Explorer**onder **rollen** in uw cloudserviceproject met de rechtermuisknop op uw *web* rol en selecteer **toevoegen**  >  **Nieuwe map**. Maak een map met de naam **bin**.
  2. Hallo bin-map met de rechtermuisknop en selecteer **toevoegen** > **bestaand Item**. Hallo .NET-installatieprogramma selecteren en toe te voegen toohello bin-map.
  
tooadd hello installatieprogramma voor een *worker* rol:
* Met de rechtermuisknop op uw *worker* rol en selecteer **toevoegen** > **bestaand Item**. Selecteer Hallo .NET installatieprogramma en voeg deze toohello rol. 

Wanneer bestanden in deze manier toohello rol content map worden toegevoegd, zijn ze automatisch tooyour cloud servicepakket toegevoegd. Hallo bestanden zijn dan geïmplementeerde tooa consistente locatie op Hallo virtuele machine. Herhaal dit proces voor elke rol web- en werkrollen in uw cloudservice zodat alle rollen een kopie van het Hallo-installatieprogramma hebben.

> [!NOTE]
> Zelfs als uw toepassing .NET 4.6 gericht, moet u .NET 4.6.1 installeren op uw cloud service-rol. Hallo Gastbesturingssysteem bevat Hallo kennisdatabase [bijwerken 3098779](https://support.microsoft.com/kb/3098779) en [3097997 bijwerken](https://support.microsoft.com/kb/3097997). Problemen kunnen optreden tijdens het uitvoeren van uw .NET-toepassingen als .NET 4.6 boven op Hallo Knowledge Base-updates is geïnstalleerd. Deze problemen, tooavoid installeren .NET 4.6.1 in plaats van versie 4.6. Zie voor meer informatie, Hallo [Knowledge Base-artikel 3118750](https://support.microsoft.com/kb/3118750).
> 
> 

![Inhoud van de rol met installer-bestanden][1]

## <a name="define-startup-tasks-for-your-roles"></a>Starten van de taken voor uw rollen definiëren
U kunt opstarten taken tooperform operations voordat een rol wordt gestart. Hallo .NET Framework installeren als onderdeel van de taak voor het opstarten van Hallo zorgt ervoor dat Hallo-framework is geïnstalleerd voordat een toepassingscode wordt uitgevoerd. Zie voor meer informatie over het starten van de taken, [starten van de taken uitvoeren in Azure](cloud-services-startup-tasks.md). 

1. Toevoegen van de volgende inhoud toohello ServiceDefinition.csdef onder Hallo Hallo **WebRole** of **WorkerRole** knooppunt voor alle rollen:
   
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
   
    Hallo voorgaande configuratie Hallo console-opdracht uitvoert `install.cmd` met administrator-bevoegdheden tooinstall Hallo .NET Framework. Hallo configuratie maakt ook een **LocalStorage** element met de naam **NETFXInstall**. Hallo opstartscript stelt Hallo tijdelijke map toouse deze resource lokale opslag. 
    
    > [!IMPORTANT]
    > tooensure Corrigeer de installatie van Hallo framework, Hallo grootte van deze resource tooat minste 1024 MB.
    
    Zie voor meer informatie over het starten van de taken [algemene Azure Cloud Services starten van de taken](cloud-services-startup-tasks-common.md).

2. Maak een bestand met de naam **install.cmd** en voeg de volgende Hallo scriptbestand toohello installeren.

    Hallo-script wordt gecontroleerd of Hallo opgegeven versie van .NET Framework Hallo al is geïnstalleerd op machine Hallo door het controleren van het Hallo-register. Als Hallo .NET versie niet is geïnstalleerd, wordt Hallo .NET webinstallatie geopend. toohelp los eventuele problemen, Hallo script registreert alle activiteiten toohello bestand startuptasklog-(de huidige datum en tijd) .txt die is opgeslagen in **InstallLogs** lokale opslag.

    > [!IMPORTANT]
    > Gebruik een elementaire teksteditor zoals Kladblok Windows toocreate Hallo install.cmd-bestand. Als u Visual Studio toocreate een tekstbestand en Hallo extensie too.cmd verandert, kan Hallo-bestand nog steeds een UTF-8-bytevolgordemarkering bevatten. Dit is ingeschakeld kan een fout veroorzaken wanneer de eerste regel Hallo van Hallo-script wordt uitgevoerd. tooavoid deze fout Hallo eerste regel Hallo script een een-instructie die door de verwerking van Hallo byte worden overgeslagen. 
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
   > Dit script toont hoe hello Azure Gast OS tooinstall .NET 4.5.2 of versie 4.6 voor bedrijfscontinuïteit, zelfs als er geen .NET 4.5.2 is al beschikbaar op. U moet rechtstreeks installeren .NET 4.6.1 in plaats van versie 4.6, zoals beschreven in Hallo [Knowledge Base-artikel 3118750](https://support.microsoft.com/kb/3118750).
   > 
   > 

3. Hallo install.cmd bestand tooeach functie toevoegen met behulp van **toevoegen** > **bestaand Item** in **Solution Explorer** zoals eerder in dit onderwerp beschreven. 

    Nadat deze stap voltooid is, moeten alle rollen Hallo .NET-installatiebestand en Hallo install.cmd bestand hebben.

   ![Inhoud van de rol met alle bestanden][2]

## <a name="configure-diagnostics-tootransfer-startup-logs-tooblob-storage"></a>Diagnostische gegevens tootransfer opstarten logboeken tooBlob opslag configureren
toosimplify het oplossen van installatieproblemen, kunt u Azure Diagnostics tootransfer alle logboekbestanden die worden gegenereerd door Hallo opstarten script of Hallo .NET installatieprogramma tooAzure Blob-opslag configureren. U kunt met behulp van deze benadering Hallo logboeken weergeven door logboekbestanden Hallo downloaden van Blob-opslag hoeft u geen tooremote bureaublad tot Hallo-functie.

tooconfigure Diagnostics, Hallo diagnostics.wadcfgx bestand openen en volgen inhoud onder Hallo Hallo toevoegen **mappen** knooppunt: 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

Deze XML Diagnostics tootransfer Hallo bestanden configureert in de logboekmap Hallo in Hallo **NETFXInstall** resource toohello opslagaccount voor diagnostische gegevens in Hallo **netfx-Installeer** blob-container.

## <a name="deploy-your-cloud-service"></a>Uw cloudservice implementeren
Wanneer u uw cloudservice implementeert, installeer Hallo starten van de taken Hallo .NET Framework als deze nog niet is geïnstalleerd. Uw cloud service-rollen zich in Hallo *bezet* status tijdens het Hallo-framework wordt geïnstalleerd. Als Hallo framework-installatie opnieuw opstarten vereist, Hallo service functies mogelijk ook opnieuw wordt opgestart. 

## <a name="additional-resources"></a>Aanvullende bronnen
* [Hallo .NET Framework installeren][Installing hello .NET Framework]
* [Bepalen welke versies van .NET Framework zijn geïnstalleerd][How to: Determine Which .NET Framework Versions Are Installed]
* [Het oplossen van de installatie van .NET Framework][Troubleshooting .NET Framework Installations]

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing hello .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
