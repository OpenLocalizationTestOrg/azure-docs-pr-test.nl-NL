---
title: aaaCommon starten van de taken voor Cloudservices | Microsoft Docs
description: Bevat enkele voorbeelden van algemene beheertaken voor opstarten kunt u tooperform in uw cloud services-Webrol of werkrol.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: a7095dad-1ee7-4141-bc6a-ef19a6e570f1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: c80fac4079439410dfc3795e4bce0fbc07dbbfab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="common-cloud-service-startup-tasks"></a>Algemene taken voor Cloud-Service starten
Dit artikel vindt u enkele voorbeelden van algemene beheertaken voor opstarten kunt u tooperform in uw cloudservice. U kunt opstarten taken tooperform operations voordat een rol wordt gestart. Wilt u misschien tooperform bewerkingen bevatten een onderdeel te installeren, het registreren van COM-onderdelen, registersleutels instellen of starten van een langdurige proces. 

Zie [in dit artikel](cloud-services-startup-tasks.md) toounderstand de werking van starten van de taken en specifiek hoe toocreate Hallo vermeldingen die een taak starten definiëren.

> [!NOTE]
> Starten van de taken zijn niet van toepassing tooVirtual Machines, alleen tooCloud Service-Web- en werkrollen.
> 

## <a name="define-environment-variables-before-a-role-starts"></a>Omgevingsvariabelen definiëren voordat een rol wordt gestart
Als u omgevingsvariabelen die zijn gedefinieerd voor een specifieke taak moet, gebruikt u Hallo [omgeving] -element in Hallo [taak] element.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
                <Environment>
                    <Variable name="MyEnvironmentVariable" value="MyVariableValue" />
                </Environment>
            </Task>
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

Variabelen kunt ook een [geldige Azure XPath-waarde](cloud-services-role-config-xpath.md) tooreference iets over Hallo-implementatie. In plaats van Hallo `value` kenmerk, het definiëren van een [RoleInstanceValue] onderliggend element.

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a>Starten van IIS met AppCmd.exe configureren
Hallo [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) opdrachtregelprogramma mag gebruikte toomanage IIS-instellingen bij het opstarten op Azure. *AppCmd.exe* handige, opdrachtregelprogramma tooconfiguration toegangsinstellingen voor gebruik in het starten van de taken in Azure biedt. Met behulp van *AppCmd.exe*, Website-instellingen kunnen worden toegevoegd, gewijzigd of verwijderd voor toepassingen en sites.

Er zijn echter enkele dingen toowatch uit voor in het gebruik van Hallo *AppCmd.exe* als een taak starten:

* Starten van de taken kunnen meer dan één keer worden uitgevoerd tussen opnieuw wordt opgestart. Bijvoorbeeld, wanneer een rol wordt gerecycled.
* Als een *AppCmd.exe* actie meer dan één keer wordt uitgevoerd, kan er een fout gegenereerd. Bijvoorbeeld een sectie tooadd te probeert*Web.config* tweemaal genereren een fout.
* Starten van de taken mislukken als ze een afsluitcode dan nul retourneren of **errorlevel**. Bijvoorbeeld, wanneer *AppCmd.exe* wordt een fout gegenereerd.

Het is een goede gewoonte toocheck hello **errorlevel** na het aanroepen *AppCmd.exe*, dit is eenvoudig toodo als u Hallo aanroep te laten teruglopen*AppCmd.exe* met een *.cmd*  bestand. Als u een bekende detecteren **errorlevel** antwoord, u kunt deze negeren of terug doorgeven.

Hallo errorlevel geretourneerd door *AppCmd.exe* in Hallo winerror.h bestand worden vermeld en kunnen ook worden weergegeven op [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).

### <a name="example-of-managing-hello-error-level"></a>Voorbeeld van het beheer van Hallo foutniveau
In dit voorbeeld voegt een sectie compressie en de compressie-vermelding voor JSON toohello *Web.config* bestand met de foutafhandeling en logboekregistratie.

Hallo relevante secties Hallo [ServiceDefinition.csdef] bestand hier worden weergegeven, die bestaan uit het instellen van Hallo [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) te kenmerk`elevated` toogive *AppCmd.exe*  voldoende machtigingen toochange Hallo instellingen in Hallo *Web.config* bestand:

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

Hallo *Startup.cmd* batch-bestand gebruikt *AppCmd.exe* tooadd een sectie compressie en de compressie-vermelding voor JSON toohello *Web.config* bestand. Hallo verwacht **errorlevel** van 183 toozero Hallo controleren met is ingesteld. EXE-opdrachtregelprogramma. Onverwachte errorlevels zijn geregistreerde tooStartupErrorLog.txt.

```cmd
REM   *** Add a compression section toohello Web.config file. ***
%windir%\system32\inetsrv\appcmd set config /section:urlCompression /doDynamicCompression:True /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1

REM   ERRORLEVEL 183 occurs when trying tooadd a section that already exists. This error is expected if this
REM   batch file were executed twice. This can occur and must be accounted for in a Azure startup
REM   task. toohandle this situation, set hello ERRORLEVEL toozero by using hello Verify command. hello Verify
REM   command will safely set hello ERRORLEVEL toozero.
IF %ERRORLEVEL% EQU 183 DO VERIFY > NUL

REM   If hello ERRORLEVEL is not zero at this point, some other error occurred.
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding a compression section toohello Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Add compression for json. ***
%windir%\system32\inetsrv\appcmd set config  -section:system.webServer/httpCompression /+"dynamicTypes.[mimeType='application/json; charset=utf-8',enabled='True']" /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1
IF %ERRORLEVEL% EQU 183 VERIFY > NUL
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding hello JSON compression type toohello Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Exit batch file. ***
EXIT /b 0

REM   *** Log error and exit ***
:ErrorExit
REM   Report hello date, time, and ERRORLEVEL of hello error.
DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
ECHO An error occurred during startup. ERRORLEVEL = %ERRORLEVEL% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT %ERRORLEVEL%
```

## <a name="add-firewall-rules"></a>Firewallregels toevoegen
In Azure zijn er effectief twee firewalls. de eerste firewall Hallo bepaalt verbindingen tussen Hallo virtuele machine en Hallo buiten world. Deze firewall wordt beheerd door Hallo [eindpunten] -element in Hallo [ServiceDefinition.csdef] bestand.

de tweede firewall Hallo bepaalt verbindingen tussen Hallo virtuele machine en Hallo processen binnen dat de virtuele machine. Deze firewall kan worden beheerd door Hallo `netsh advfirewall firewall` opdrachtregelprogramma.

Azure maakt firewallregels voor Hallo processen binnen uw rollen gestart. Bijvoorbeeld, wanneer u een service of programma start, maakt Azure automatisch Hallo nodig firewall-regels tooallow die service toocommunicate Hello Internet. Als u een service die wordt gestart door een proces buiten uw rol (zoals een COM +-service of een Windows-taak plannen) maakt, moet u echter toomanually maken van een firewall regel tooallow access toothat service. Deze firewall-regels kunnen worden gemaakt met behulp van een taak starten.

Een starten van de taak die wordt gemaakt van een firewallregel moet hebben een [executionContext][taak] van **verhoogde**. Starten van de taak toohello na Hallo toevoegen [ServiceDefinition.csdef] bestand.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="AddFirewallRules.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

tooadd hello firewallregel, moet u relevante Hallo `netsh advfirewall firewall` opdrachten in het batchbestand opstarten. In dit voorbeeld vereist Hallo starten van de taak beveiliging en versleuteling voor TCP-poort 80.

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a>Een specifiek IP-adres blokkeren
U kunt een Azure-web-rol toegang tooa set opgegeven IP-adressen beperken door het wijzigen van de IIS **web.config** bestand. U moet ook een opdrachtbestand waarmee wordt ontgrendeld Hallo toouse **ipSecurity** sectie Hallo **ApplicationHost.config** bestand.

toodo ontgrendelen Hallo **ipSecurity** sectie Hallo **ApplicationHost.config** bestand, een opdrachtbestand maken dat wordt uitgevoerd op de rol is gestart. Maak een map op Hallo hoogste niveau van de Webrol aangeroepen **opstarten** en maak in deze map een batchbestand aangeroepen **startup.cmd**. Dit bestand tooyour Visual Studio-project toevoegen en stel de Hallo te**kopie altijd** tooensure dat is opgenomen in het pakket.

Starten van de taak toohello na Hallo toevoegen [ServiceDefinition.csdef] bestand.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WebRole name="WebRole1">
        ...
        <Startup>
            <Task commandLine="startup.cmd" executionContext="elevated" />
        </Startup>
    </WebRole>
</ServiceDefinition>
```

Toevoegen van deze opdracht toohello **startup.cmd** bestand:

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

Met deze taak wordt Hallo **startup.cmd** batch-bestand toobe uitgevoerd telkens als de Webrol Hallo is geïnitialiseerd, waarbij u ervoor zorgt dat Hallo vereist **ipSecurity** sectie is opgeheven.

Wijzig tot slot Hallo [system.webServer sectie](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) uw Webrol **web.config** bestand tooadd een lijst met IP-adressen die toegang, zoals wordt weergegeven in Hallo voorbeeld te volgen:

De configuratie van dit voorbeeld **kunt** alle IP-adressen tooaccess Hallo server behalve Hallo twee gedefinieerd

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are granted access-->
    <ipSecurity>
        <!--hello following IP addresses are denied access-->
        <add allowed="false" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="false" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

De configuratie van dit voorbeeld **weigert** alle IP-adressen van toegang tot de server hello, met uitzondering van Hallo twee gedefinieerd.

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are denied access-->
    <ipSecurity allowUnlisted="false">
        <!--hello following IP addresses are granted access-->
        <add allowed="true" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="true" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

## <a name="create-a-powershell-startup-task"></a>Een PowerShell starten van de taak maken
Windows PowerShell-scripts, kunnen niet worden aangeroepen rechtstreeks vanuit Hallo [ServiceDefinition.csdef] bestand, maar ze kunnen worden aangeroepen vanuit een batchbestand opstarten.

Niet-ondertekende scripts niet wordt uitgevoerd in PowerShell (standaard). Tenzij u uw script ondertekent, moet u tooconfigure PowerShell toorun niet-ondertekende scripts. toorun niet-ondertekende scripts, hello **ExecutionPolicy** te moet worden ingesteld**onbeperkt**. Hallo **ExecutionPolicy** instelt dat u gebruik is gebaseerd op Hallo-versie van Windows PowerShell.

```cmd
REM   Run an unsigned PowerShell script and log hello output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

Als u een Gastbesturingssysteem dat wordt uitgevoerd, PowerShell 2.0 of 1.0 u versie 2 toorun kunt afdwingen, en als niet beschikbaar is, wordt versie 1 gebruiken.

```cmd
REM   Attempt tooset hello execution policy by using PowerShell version 2.0 syntax.
PowerShell -Version 2.0 -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If PowerShell version 2.0 isn't available. Set hello execution policy by using hello PowerShell
IF %ERRORLEVEL% EQU -393216 (
   PowerShell -Command "Set-ExecutionPolicy Unrestricted" >> "%TEMP%\StartupLog.txt" 2>&1
   PowerShell .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1
)

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="create-files-in-local-storage-from-a-startup-task"></a>Maken van bestanden in lokale opslag van een taak starten
U kunt een lokale opslag resource toostore gebruiken bestanden die zijn gemaakt met het starten van de taak die later worden geopend door uw toepassing.

toocreate Hallo resource voor lokale opslag, het toevoegen van een [LocalResources] sectie toohello [ServiceDefinition.csdef] -bestand en voeg vervolgens Hallo [LocalStorage] onderliggend element. Geeft een unieke naam en de juiste grootte Hallo lokale opslagresource voor het starten van de taak.

een bron van de lokale opslag in uw opstarttaak toouse, moet u toocreate een Resourcelocatie omgeving variabele tooreference Hallo lokale opslag. Vervolgens Hallo opstarttaak Hallo toepassing zijn en kunnen tooread en bestanden toohello lokale opslagbron schrijven.

Hallo relevante secties Hallo **ServiceDefinition.csdef** bestand worden hier weergegeven:

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">
    ...

    <LocalResources>
      <LocalStorage name="StartupLocalStorage" sizeInMB="5"/>
    </LocalResources>

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="PathToStartupStorage">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
  </WorkerRole>
</ServiceDefinition>
```

Als u bijvoorbeeld dit **Startup.cmd** gebruikt Hallo batchbestand **PathToStartupStorage** omgeving variabele toocreate Hallo bestand **MyTest.txt** op Hallo lokale opslag locatie.

```cmd
REM   Create a simple text file.

ECHO This text will go into hello MyTest.txt file which will be in hello    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed tooby hello PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO hello contents of hello PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit hello batch file with ERRORLEVEL 0.

EXIT /b 0
```

U kunt lokale opslagmap openen vanaf hello Azure SDK met behulp van Hallo [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) methode.

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-hello-emulator-or-cloud"></a>In het Hallo-emulator of cloud worden uitgevoerd
U kunt uw verschillende stappen uitvoeren wanneer deze wordt uitgevoerd in de Hallo cloud vergeleken toowhen zich in de rekenemulator hello opstarttaak hebben. U kunt bijvoorbeeld, toouse een nieuw exemplaar van uw SQL-gegevens alleen bij uitvoering in Hallo-emulator. Of u wilt dat toodo prestatieoptimalisatie voor Hallo cloud hoeft u niet toodo bij uitvoering in Hallo-emulator.

Deze mogelijkheid tooperform verschillende acties op Hallo rekenemulator en Hallo cloud kan worden uitgevoerd door het maken van een omgevingsvariabele in Hallo [ServiceDefinition.csdef] bestand. U test die omgevingsvariabele voor een waarde in uw taak starten.

Hallo omgevingsvariabele toocreate Hallo toevoegen [variabele]/[RoleInstanceValue] element en het maken van een XPath-waarde van `/RoleEnvironment/Deployment/@emulated`. waarde van Hallo Hallo **% ComputeEmulatorRunning %** omgevingsvariabele is `true` bij uitvoering op Hallo-rekenemulator en `false` bij uitvoering op Hallo cloud.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">

    ...

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>

  </WorkerRole>
</ServiceDefinition>
```

Hallo taak controleren nu Hallo **% ComputeEmulatorRunning %** omgeving variabele tooperform verschillende acties op basis van of Hallo-functie wordt uitgevoerd in Hallo cloud of Hallo emulator. Hier volgt een cmd-shell-script waarmee wordt gecontroleerd of deze omgevingsvariabele.

```cmd
REM   Check if this task is running on hello compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on hello compute emulator. Perform tasks that must be run only in hello compute emulator.
) ELSE (
    REM   This task is running on hello cloud. Perform tasks that must be run only in hello cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a>Detecteren of de taak al is uitgevoerd
Hallo-rol kan recycle zonder waardoor uw taken starten toorun opnieuw opgestart. Er is geen vlag tooindicate die een taak is al uitgevoerd op Hallo hosten van virtuele machine. Mogelijk hebt u een aantal taken waarbij het maakt niet uit dat ze meerdere keren worden uitgevoerd. Echter, u kunt uitvoeren in een situatie waarin u tooprevent moet een taak meer dan één keer worden uitgevoerd.

het eenvoudigste manier toodetect Hello, die een taak heeft al een bestand in Hallo toocreate is **% TEMP %** map wanneer het Hallo-taak is voltooid en bekijk voor Hallo starten van Hallo-taak. Hier volgt een voorbeeld cmd shell-script dat die voor u uitvoert.

```cmd
REM   If Task1_Success.txt exists, then Application 1 is already installed.
IF EXIST "%RoleRoot%\Task1_Success.txt" (
  ECHO Application 1 is already installed. Exiting. >> "%TEMP%\StartupLog.txt" 2>&1
  GOTO Finish
)

REM   Run your real exe task
ECHO Running XYZ >> "%TEMP%\StartupLog.txt" 2>&1
"%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (
  REM   hello application installed without error. Create a file tooindicate that hello task
  REM   does not need toobe run again.

  ECHO This line will create a file tooindicate that Application 1 installed correctly. > "%RoleRoot%\Task1_Success.txt"

) ELSE (
  REM   An error occurred. Log hello error and exit with hello error code.

  DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
  TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
  ECHO  An error occurred running task 1. Errorlevel = %ERRORLEVEL%. >> "%TEMP%\StartupLog.txt" 2>&1

  EXIT %ERRORLEVEL%
)

:Finish

REM   Exit normally.
EXIT /B 0
```

## <a name="task-best-practices"></a>Aanbevolen procedures van taak
Hier volgen enkele aanbevolen procedures die u volgen moet wanneer de taak voor uw web- of worker-rol configureert.

### <a name="always-log-startup-activities"></a>Meld u altijd starten van activiteiten
Visual Studio biedt geen een foutopsporingsprogramma toostep via batchbestanden, dus is het goed tooget zo veel mogelijk gegevens over Hallo werking van batch-bestanden mogelijk. Hallo-uitvoer van de batch-bestanden logboekregistratie beide **stdout** en **stderr**, kunt u belangrijke informatie geven bij het toodebug en los van de batch-bestanden. beide toolog **stdout** en **stderr** toohello StartupLog.txt bestand in Hallo directory verwijzen tooby hello **% TEMP %** omgevingsvariabele tekst hello toevoegen`>>  "%TEMP%\\StartupLog.txt" 2>&1`toohello einde van de specifieke regels u wilt dat toolog. Bijvoorbeeld: tooexecute setup.exe in Hallo **% PathToApp1Install** directory:

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

toosimplify uw XML-gegevens, kunt u een wrapper *cmd* bestand die alle uw opstarten aanroept taken samen met de logboekregistratie en zorgt ervoor dat elke onderliggende taak shares Hallo dezelfde omgevingsvariabelen.

Soms is het echter toouse irritante `>> "%TEMP%\StartupLog.txt" 2>&1` op Hallo einde van elke taak starten. U kunt de taak logboekregistratie afdwingen door het maken van een wrapper die verantwoordelijk is voor logboekregistratie voor u. Deze wrapper roept echte batchbestand Hallo gewenste toorun. Elke uitvoer van de doel-batchbestand Hallo worden omgeleid toohello *Startuplog.txt* bestand.

Hallo volgende voorbeeld ziet u hoe u alle tooredirect de uitvoer van een starten van de batch-bestand. In dit voorbeeld Hallo ServerDefinition.csdef maakt een taak gestart die aanroept *logwrap.cmd*. *logwrap.cmd* aanroepen *Startup2.cmd*, alle uitvoer te leiden**% TEMP %\\StartupLog.txt**.

ServiceDefinition.cmd:

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

**logwrap.cmd:**

```cmd
@ECHO OFF

REM   logwrap.cmd calls passed in batch file, redirecting all output toohello StartupLog.txt log file.

ECHO [%date% %time%] == START logwrap.cmd ============================================== >> "%TEMP%\StartupLog.txt" 2>&1
ECHO [%date% %time%] Running %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Call hello child command batch file, redirecting all output toohello StartupLog.txt log file.
START /B /WAIT %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Log hello completion of child command.
ECHO [%date% %time%] Done >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (

   REM   No errors occurred. Exit logwrap.cmd normally.
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B 0

) ELSE (

   REM   Log hello error.
   ECHO [%date% %time%] An error occurred. hello ERRORLEVEL = %ERRORLEVEL%.  >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B %ERRORLEVEL%

)
```

**Startup2.cmd:**

```cmd
@ECHO OFF

REM   This is hello batch file where hello startup steps should be performed. Because of the
REM   way Startup2.cmd was called, all commands and their outputs will be stored in the
REM   StartupLog.txt file in hello directory pointed tooby hello TEMP environment variable.

REM   If an error occurs, hello following command will pass hello ERRORLEVEL back toothe
REM   calling batch file.

ECHO [%date% %time%] Some log information about this task
ECHO [%date% %time%] Some more log information about this task

EXIT %ERRORLEVEL%
```

Voorbeeld van uitvoer in Hallo **StartupLog.txt** bestand:

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> Hallo **StartupLog.txt** bestand bevindt zich in Hallo *C:\Resources\temp\\{rol-id} \RoleTemp* map.
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a>Set executionContext op de juiste wijze voor opstarttaken
Stel bevoegdheden op de juiste wijze voor Hallo starten van de taak. Soms moeten starten van de taken uitvoeren met verhoogde bevoegdheden Hoewel Hallo-rol wordt uitgevoerd met normale bevoegdheden.

Hallo [executionContext][taak] kenmerk machtigingsniveau Hallo van Hallo starten van de taak wordt ingesteld. Met behulp van `executionContext="limited"` betekent Hallo starten van de taak heeft Hallo hetzelfde niveau van bevoegdheden als Hallo-rol. Met behulp van `executionContext="elevated"` betekent Hallo opstarttaak administrator-bevoegdheden heeft, kunnen de Hallo opstarten taak tooperform beheerderstaken zonder administrator-bevoegdheden tooyour rol toekennen.

Een voorbeeld van een taak gestart die zijn verhoogde bevoegdheden vereist is een taak gestart die gebruikmaakt van **AppCmd.exe** tooconfigure IIS. **AppCmd.exe** vereist `executionContext="elevated"`.

### <a name="use-hello-appropriate-tasktype"></a>Gebruik de juiste taskType Hallo
Hallo [taskType][taak] kenmerk bepaalt Hallo manier Hallo starten van de taak wordt uitgevoerd. Er zijn drie waarden: **eenvoudige**, **achtergrond**, en **voorgrond**. Hallo en achtergrond taken zijn gestart asynchroon en vervolgens Hallo eenvoudige taken synchroon uitgevoerd één tegelijk.

Met **eenvoudige** starten van de taken, kunt u Hallo in welke volgorde Hallo taken uitgevoerd door Hallo volgorde welke Hallo taken worden opgenomen in Hallo ServiceDefinition.csdef bestand instellen. Als een **eenvoudige** taak eindigt met een niet-nul afsluitcode en vervolgens opstarten procedure stopt Hallo en Hallo-rol niet gestart.

verschil tussen Hallo **achtergrond** starten van de taken en **voorgrond** starten van de taken is dat **voorgrond** taken houden Hallo rol uitgevoerd totdat Hallo  **voorgrond** taak is geëindigd. Dit betekent ook dat als hello **voorgrond** taak vastloopt of crasht, Hallo-rol niet gerecycled tot Hallo **voorgrond** taak wordt geforceerd gesloten. Om deze reden **achtergrond** taken worden aanbevolen voor het starten van de asynchrone taken alleen u deze functie Hallo moet **voorgrond** taak.

### <a name="end-batch-files-with-exit-b-0"></a>Einde batch-bestanden met de AFSLUITCODE /B 0
Hallo rol wordt alleen gestart als hello **errorlevel** van elk van uw eenvoudige starten van de taak is aan nul. Niet alle programma's ingesteld Hallo **errorlevel** (afsluitcode) correct, dus Hallo batch-bestand moet eindigen met een `EXIT /B 0` als alles goed is uitgevoerd.

Een ontbrekende `EXIT /B 0` Hallo einde van een starten van de batch-bestand is een veelvoorkomende oorzaak van de functies die niet worden gestart.

> [!NOTE]
> Ik opgevallen dat geneste batch bestanden soms vastlopen wanneer u Hallo `/B` parameter. Desgewenst kunt u ervoor dat dit probleem blijft hangen niet gebeurt als een ander batchbestand het huidige batchbestand roept, zoals als u Hallo toomake [logboek wrapper](#always-log-startup-activities). U kunt Hallo weglaten `/B` parameter in dit geval.
> 
> 

### <a name="expect-startup-tasks-toorun-more-than-once"></a>Starten van de taken toorun meer dan één keer verwacht
Niet alle rol recyclet zijn opnieuw worden opgestart, maar alle rol recyclet omvatten alle starten van de taken uitgevoerd. Dit betekent dat starten van de taken kunnen toorun meerdere keren tussen opnieuw wordt opgestart zonder problemen moeten zijn. Dit wordt besproken in Hallo [voorgaande sectie](#detect-that-your-task-has-already-run).

### <a name="use-local-storage-toostore-files-that-must-be-accessed-in-hello-role"></a>Lokale opslag toostore bestanden die moeten worden geopend in de rol hello gebruiken
Als u wilt dat toocopy of maak een bestand tijdens het starten van de taak die vervolgens toegankelijk tooyour rol, wordt dat bestand moet worden geplaatst in de lokale opslag. Zie Hallo [voorgaande sectie](#create-files-in-local-storage-from-a-startup-task).

## <a name="next-steps"></a>Volgende stappen
Bekijk Hallo cloud [service model- en -pakket](cloud-services-model-and-package.md)

Meer informatie over het [taken](cloud-services-startup-tasks.md) werken.

[Maken en implementeren van](cloud-services-how-to-create-deploy-portal.md) uw cloud-pakket.

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[taak]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[omgeving]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[variabele]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
[Eindpunten]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints
[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage
[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
