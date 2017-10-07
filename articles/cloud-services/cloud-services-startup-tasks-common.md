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
# <a name="common-cloud-service-startup-tasks"></a><span data-ttu-id="70112-103">Algemene taken voor Cloud-Service starten</span><span class="sxs-lookup"><span data-stu-id="70112-103">Common Cloud Service startup tasks</span></span>
<span data-ttu-id="70112-104">Dit artikel vindt u enkele voorbeelden van algemene beheertaken voor opstarten kunt u tooperform in uw cloudservice.</span><span class="sxs-lookup"><span data-stu-id="70112-104">This article provides some examples of common startup tasks you may want tooperform in your cloud service.</span></span> <span data-ttu-id="70112-105">U kunt opstarten taken tooperform operations voordat een rol wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="70112-105">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="70112-106">Wilt u misschien tooperform bewerkingen bevatten een onderdeel te installeren, het registreren van COM-onderdelen, registersleutels instellen of starten van een langdurige proces.</span><span class="sxs-lookup"><span data-stu-id="70112-106">Operations that you might want tooperform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span> 

<span data-ttu-id="70112-107">Zie [in dit artikel](cloud-services-startup-tasks.md) toounderstand de werking van starten van de taken en specifiek hoe toocreate Hallo vermeldingen die een taak starten definiëren.</span><span class="sxs-lookup"><span data-stu-id="70112-107">See [this article](cloud-services-startup-tasks.md) toounderstand how startup tasks work, and specifically how toocreate hello entries that define a startup task.</span></span>

> [!NOTE]
> <span data-ttu-id="70112-108">Starten van de taken zijn niet van toepassing tooVirtual Machines, alleen tooCloud Service-Web- en werkrollen.</span><span class="sxs-lookup"><span data-stu-id="70112-108">Startup tasks are not applicable tooVirtual Machines, only tooCloud Service Web and Worker roles.</span></span>
> 

## <a name="define-environment-variables-before-a-role-starts"></a><span data-ttu-id="70112-109">Omgevingsvariabelen definiëren voordat een rol wordt gestart</span><span class="sxs-lookup"><span data-stu-id="70112-109">Define environment variables before a role starts</span></span>
<span data-ttu-id="70112-110">Als u omgevingsvariabelen die zijn gedefinieerd voor een specifieke taak moet, gebruikt u Hallo [omgeving] -element in Hallo [taak] element.</span><span class="sxs-lookup"><span data-stu-id="70112-110">If you need environment variables defined for a specific task, use hello [Environment] element inside hello [Task] element.</span></span>

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

<span data-ttu-id="70112-111">Variabelen kunt ook een [geldige Azure XPath-waarde](cloud-services-role-config-xpath.md) tooreference iets over Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="70112-111">Variables can also use a [valid Azure XPath value](cloud-services-role-config-xpath.md) tooreference something about hello deployment.</span></span> <span data-ttu-id="70112-112">In plaats van Hallo `value` kenmerk, het definiëren van een [RoleInstanceValue] onderliggend element.</span><span class="sxs-lookup"><span data-stu-id="70112-112">Instead of using hello `value` attribute, define a [RoleInstanceValue] child element.</span></span>

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a><span data-ttu-id="70112-113">Starten van IIS met AppCmd.exe configureren</span><span class="sxs-lookup"><span data-stu-id="70112-113">Configure IIS startup with AppCmd.exe</span></span>
<span data-ttu-id="70112-114">Hallo [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) opdrachtregelprogramma mag gebruikte toomanage IIS-instellingen bij het opstarten op Azure.</span><span class="sxs-lookup"><span data-stu-id="70112-114">hello [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) command-line tool can be used toomanage IIS settings at startup on Azure.</span></span> <span data-ttu-id="70112-115">*AppCmd.exe* handige, opdrachtregelprogramma tooconfiguration toegangsinstellingen voor gebruik in het starten van de taken in Azure biedt.</span><span class="sxs-lookup"><span data-stu-id="70112-115">*AppCmd.exe* provides convenient, command-line access tooconfiguration settings for use in startup tasks on Azure.</span></span> <span data-ttu-id="70112-116">Met behulp van *AppCmd.exe*, Website-instellingen kunnen worden toegevoegd, gewijzigd of verwijderd voor toepassingen en sites.</span><span class="sxs-lookup"><span data-stu-id="70112-116">Using *AppCmd.exe*, Website settings can be added, modified, or removed for applications and sites.</span></span>

<span data-ttu-id="70112-117">Er zijn echter enkele dingen toowatch uit voor in het gebruik van Hallo *AppCmd.exe* als een taak starten:</span><span class="sxs-lookup"><span data-stu-id="70112-117">However, there are a few things toowatch out for in hello use of *AppCmd.exe* as a startup task:</span></span>

* <span data-ttu-id="70112-118">Starten van de taken kunnen meer dan één keer worden uitgevoerd tussen opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="70112-118">Startup tasks can be run more than once between reboots.</span></span> <span data-ttu-id="70112-119">Bijvoorbeeld, wanneer een rol wordt gerecycled.</span><span class="sxs-lookup"><span data-stu-id="70112-119">For instance, when a role recycles.</span></span>
* <span data-ttu-id="70112-120">Als een *AppCmd.exe* actie meer dan één keer wordt uitgevoerd, kan er een fout gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="70112-120">If a *AppCmd.exe* action is performed more than once, it may generate an error.</span></span> <span data-ttu-id="70112-121">Bijvoorbeeld een sectie tooadd te probeert*Web.config* tweemaal genereren een fout.</span><span class="sxs-lookup"><span data-stu-id="70112-121">For example, attempting tooadd a section too*Web.config* twice could generate an error.</span></span>
* <span data-ttu-id="70112-122">Starten van de taken mislukken als ze een afsluitcode dan nul retourneren of **errorlevel**.</span><span class="sxs-lookup"><span data-stu-id="70112-122">Startup tasks fail if they return a non-zero exit code or **errorlevel**.</span></span> <span data-ttu-id="70112-123">Bijvoorbeeld, wanneer *AppCmd.exe* wordt een fout gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="70112-123">For example, when *AppCmd.exe* generates an error.</span></span>

<span data-ttu-id="70112-124">Het is een goede gewoonte toocheck hello **errorlevel** na het aanroepen *AppCmd.exe*, dit is eenvoudig toodo als u Hallo aanroep te laten teruglopen*AppCmd.exe* met een *.cmd*  bestand.</span><span class="sxs-lookup"><span data-stu-id="70112-124">It is a good practice toocheck hello **errorlevel** after calling *AppCmd.exe*, which is easy toodo if you wrap hello call too*AppCmd.exe* with a *.cmd* file.</span></span> <span data-ttu-id="70112-125">Als u een bekende detecteren **errorlevel** antwoord, u kunt deze negeren of terug doorgeven.</span><span class="sxs-lookup"><span data-stu-id="70112-125">If you detect a known **errorlevel** response, you can ignore it, or pass it back.</span></span>

<span data-ttu-id="70112-126">Hallo errorlevel geretourneerd door *AppCmd.exe* in Hallo winerror.h bestand worden vermeld en kunnen ook worden weergegeven op [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span><span class="sxs-lookup"><span data-stu-id="70112-126">hello errorlevel returned by *AppCmd.exe* are listed in hello winerror.h file, and can also be seen on [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span></span>

### <a name="example-of-managing-hello-error-level"></a><span data-ttu-id="70112-127">Voorbeeld van het beheer van Hallo foutniveau</span><span class="sxs-lookup"><span data-stu-id="70112-127">Example of managing hello error level</span></span>
<span data-ttu-id="70112-128">In dit voorbeeld voegt een sectie compressie en de compressie-vermelding voor JSON toohello *Web.config* bestand met de foutafhandeling en logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="70112-128">This example adds a compression section and a compression entry for JSON toohello *Web.config* file, with error handling and logging.</span></span>

<span data-ttu-id="70112-129">Hallo relevante secties Hallo [ServiceDefinition.csdef] bestand hier worden weergegeven, die bestaan uit het instellen van Hallo [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) te kenmerk`elevated` toogive *AppCmd.exe*  voldoende machtigingen toochange Hallo instellingen in Hallo *Web.config* bestand:</span><span class="sxs-lookup"><span data-stu-id="70112-129">hello relevant sections of hello [ServiceDefinition.csdef] file are shown here, which include setting hello [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) attribute too`elevated` toogive *AppCmd.exe* sufficient permissions toochange hello settings in hello *Web.config* file:</span></span>

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

<span data-ttu-id="70112-130">Hallo *Startup.cmd* batch-bestand gebruikt *AppCmd.exe* tooadd een sectie compressie en de compressie-vermelding voor JSON toohello *Web.config* bestand.</span><span class="sxs-lookup"><span data-stu-id="70112-130">hello *Startup.cmd* batch file uses *AppCmd.exe* tooadd a compression section and a compression entry for JSON toohello *Web.config* file.</span></span> <span data-ttu-id="70112-131">Hallo verwacht **errorlevel** van 183 toozero Hallo controleren met is ingesteld. EXE-opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="70112-131">hello expected **errorlevel** of 183 is set toozero using hello VERIFY.EXE command-line program.</span></span> <span data-ttu-id="70112-132">Onverwachte errorlevels zijn geregistreerde tooStartupErrorLog.txt.</span><span class="sxs-lookup"><span data-stu-id="70112-132">Unexpected errorlevels are logged tooStartupErrorLog.txt.</span></span>

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

## <a name="add-firewall-rules"></a><span data-ttu-id="70112-133">Firewallregels toevoegen</span><span class="sxs-lookup"><span data-stu-id="70112-133">Add firewall rules</span></span>
<span data-ttu-id="70112-134">In Azure zijn er effectief twee firewalls.</span><span class="sxs-lookup"><span data-stu-id="70112-134">In Azure, there are effectively two firewalls.</span></span> <span data-ttu-id="70112-135">de eerste firewall Hallo bepaalt verbindingen tussen Hallo virtuele machine en Hallo buiten world.</span><span class="sxs-lookup"><span data-stu-id="70112-135">hello first firewall controls connections between hello virtual machine and hello outside world.</span></span> <span data-ttu-id="70112-136">Deze firewall wordt beheerd door Hallo [eindpunten] -element in Hallo [ServiceDefinition.csdef] bestand.</span><span class="sxs-lookup"><span data-stu-id="70112-136">This firewall is controlled by hello [EndPoints] element in hello [ServiceDefinition.csdef] file.</span></span>

<span data-ttu-id="70112-137">de tweede firewall Hallo bepaalt verbindingen tussen Hallo virtuele machine en Hallo processen binnen dat de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="70112-137">hello second firewall controls connections between hello virtual machine and hello processes within that virtual machine.</span></span> <span data-ttu-id="70112-138">Deze firewall kan worden beheerd door Hallo `netsh advfirewall firewall` opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="70112-138">This firewall can be controlled by hello `netsh advfirewall firewall` command-line tool.</span></span>

<span data-ttu-id="70112-139">Azure maakt firewallregels voor Hallo processen binnen uw rollen gestart.</span><span class="sxs-lookup"><span data-stu-id="70112-139">Azure creates firewall rules for hello processes started within your roles.</span></span> <span data-ttu-id="70112-140">Bijvoorbeeld, wanneer u een service of programma start, maakt Azure automatisch Hallo nodig firewall-regels tooallow die service toocommunicate Hello Internet.</span><span class="sxs-lookup"><span data-stu-id="70112-140">For example, when you start a service or program, Azure automatically creates hello necessary firewall rules tooallow that service toocommunicate with hello Internet.</span></span> <span data-ttu-id="70112-141">Als u een service die wordt gestart door een proces buiten uw rol (zoals een COM +-service of een Windows-taak plannen) maakt, moet u echter toomanually maken van een firewall regel tooallow access toothat service.</span><span class="sxs-lookup"><span data-stu-id="70112-141">However, if you create a service that is started by a process outside your role (like a COM+ service or a Windows Scheduled Task), you need toomanually create a firewall rule tooallow access toothat service.</span></span> <span data-ttu-id="70112-142">Deze firewall-regels kunnen worden gemaakt met behulp van een taak starten.</span><span class="sxs-lookup"><span data-stu-id="70112-142">These firewall rules can be created by using a startup task.</span></span>

<span data-ttu-id="70112-143">Een starten van de taak die wordt gemaakt van een firewallregel moet hebben een [executionContext][taak] van **verhoogde**.</span><span class="sxs-lookup"><span data-stu-id="70112-143">A startup task that creates a firewall rule must have an [executionContext][Task] of **elevated**.</span></span> <span data-ttu-id="70112-144">Starten van de taak toohello na Hallo toevoegen [ServiceDefinition.csdef] bestand.</span><span class="sxs-lookup"><span data-stu-id="70112-144">Add hello following startup task toohello [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="70112-145">tooadd hello firewallregel, moet u relevante Hallo `netsh advfirewall firewall` opdrachten in het batchbestand opstarten.</span><span class="sxs-lookup"><span data-stu-id="70112-145">tooadd hello firewall rule, you must use hello appropriate `netsh advfirewall firewall` commands in your startup batch file.</span></span> <span data-ttu-id="70112-146">In dit voorbeeld vereist Hallo starten van de taak beveiliging en versleuteling voor TCP-poort 80.</span><span class="sxs-lookup"><span data-stu-id="70112-146">In this example, hello startup task requires security and encryption for TCP port 80.</span></span>

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a><span data-ttu-id="70112-147">Een specifiek IP-adres blokkeren</span><span class="sxs-lookup"><span data-stu-id="70112-147">Block a specific IP address</span></span>
<span data-ttu-id="70112-148">U kunt een Azure-web-rol toegang tooa set opgegeven IP-adressen beperken door het wijzigen van de IIS **web.config** bestand.</span><span class="sxs-lookup"><span data-stu-id="70112-148">You can restrict an Azure web role access tooa set of specified IP addresses by modifying your IIS **web.config** file.</span></span> <span data-ttu-id="70112-149">U moet ook een opdrachtbestand waarmee wordt ontgrendeld Hallo toouse **ipSecurity** sectie Hallo **ApplicationHost.config** bestand.</span><span class="sxs-lookup"><span data-stu-id="70112-149">You also need toouse a command file which unlocks hello **ipSecurity** section of hello **ApplicationHost.config** file.</span></span>

<span data-ttu-id="70112-150">toodo ontgrendelen Hallo **ipSecurity** sectie Hallo **ApplicationHost.config** bestand, een opdrachtbestand maken dat wordt uitgevoerd op de rol is gestart.</span><span class="sxs-lookup"><span data-stu-id="70112-150">toodo unlock hello **ipSecurity** section of hello **ApplicationHost.config** file, create a command file that runs at role start.</span></span> <span data-ttu-id="70112-151">Maak een map op Hallo hoogste niveau van de Webrol aangeroepen **opstarten** en maak in deze map een batchbestand aangeroepen **startup.cmd**.</span><span class="sxs-lookup"><span data-stu-id="70112-151">Create a folder at hello root level of your web role called **startup** and, within this folder, create a batch file called **startup.cmd**.</span></span> <span data-ttu-id="70112-152">Dit bestand tooyour Visual Studio-project toevoegen en stel de Hallo te**kopie altijd** tooensure dat is opgenomen in het pakket.</span><span class="sxs-lookup"><span data-stu-id="70112-152">Add this file tooyour Visual Studio project and set hello properties too**Copy Always** tooensure that it is included in your package.</span></span>

<span data-ttu-id="70112-153">Starten van de taak toohello na Hallo toevoegen [ServiceDefinition.csdef] bestand.</span><span class="sxs-lookup"><span data-stu-id="70112-153">Add hello following startup task toohello [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="70112-154">Toevoegen van deze opdracht toohello **startup.cmd** bestand:</span><span class="sxs-lookup"><span data-stu-id="70112-154">Add this command toohello **startup.cmd** file:</span></span>

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

<span data-ttu-id="70112-155">Met deze taak wordt Hallo **startup.cmd** batch-bestand toobe uitgevoerd telkens als de Webrol Hallo is geïnitialiseerd, waarbij u ervoor zorgt dat Hallo vereist **ipSecurity** sectie is opgeheven.</span><span class="sxs-lookup"><span data-stu-id="70112-155">This task causes hello **startup.cmd** batch file toobe run every time hello web role is initialized, ensuring that hello required **ipSecurity** section is unlocked.</span></span>

<span data-ttu-id="70112-156">Wijzig tot slot Hallo [system.webServer sectie](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) uw Webrol **web.config** bestand tooadd een lijst met IP-adressen die toegang, zoals wordt weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="70112-156">Finally, modify hello [system.webServer section](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) your web role’s **web.config** file tooadd a list of IP addresses that are granted access, as shown in hello following example:</span></span>

<span data-ttu-id="70112-157">De configuratie van dit voorbeeld **kunt** alle IP-adressen tooaccess Hallo server behalve Hallo twee gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="70112-157">This sample config **allows** all IPs tooaccess hello server except hello two defined</span></span>

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

<span data-ttu-id="70112-158">De configuratie van dit voorbeeld **weigert** alle IP-adressen van toegang tot de server hello, met uitzondering van Hallo twee gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="70112-158">This sample config **denies** all IPs from accessing hello server except for hello two defined.</span></span>

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

## <a name="create-a-powershell-startup-task"></a><span data-ttu-id="70112-159">Een PowerShell starten van de taak maken</span><span class="sxs-lookup"><span data-stu-id="70112-159">Create a PowerShell startup task</span></span>
<span data-ttu-id="70112-160">Windows PowerShell-scripts, kunnen niet worden aangeroepen rechtstreeks vanuit Hallo [ServiceDefinition.csdef] bestand, maar ze kunnen worden aangeroepen vanuit een batchbestand opstarten.</span><span class="sxs-lookup"><span data-stu-id="70112-160">Windows PowerShell scripts cannot be called directly from hello [ServiceDefinition.csdef] file, but they can be invoked from within a startup batch file.</span></span>

<span data-ttu-id="70112-161">Niet-ondertekende scripts niet wordt uitgevoerd in PowerShell (standaard).</span><span class="sxs-lookup"><span data-stu-id="70112-161">PowerShell (by default) does not run unsigned scripts.</span></span> <span data-ttu-id="70112-162">Tenzij u uw script ondertekent, moet u tooconfigure PowerShell toorun niet-ondertekende scripts.</span><span class="sxs-lookup"><span data-stu-id="70112-162">Unless you sign your script, you need tooconfigure PowerShell toorun unsigned scripts.</span></span> <span data-ttu-id="70112-163">toorun niet-ondertekende scripts, hello **ExecutionPolicy** te moet worden ingesteld**onbeperkt**.</span><span class="sxs-lookup"><span data-stu-id="70112-163">toorun unsigned scripts, hello **ExecutionPolicy** must be set too**Unrestricted**.</span></span> <span data-ttu-id="70112-164">Hallo **ExecutionPolicy** instelt dat u gebruik is gebaseerd op Hallo-versie van Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="70112-164">hello **ExecutionPolicy** setting that you use is based on hello version of Windows PowerShell.</span></span>

```cmd
REM   Run an unsigned PowerShell script and log hello output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

<span data-ttu-id="70112-165">Als u een Gastbesturingssysteem dat wordt uitgevoerd, PowerShell 2.0 of 1.0 u versie 2 toorun kunt afdwingen, en als niet beschikbaar is, wordt versie 1 gebruiken.</span><span class="sxs-lookup"><span data-stu-id="70112-165">If you're using a Guest OS that is runs PowerShell 2.0 or 1.0 you can force version 2 toorun, and if unavailable, use version 1.</span></span>

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

## <a name="create-files-in-local-storage-from-a-startup-task"></a><span data-ttu-id="70112-166">Maken van bestanden in lokale opslag van een taak starten</span><span class="sxs-lookup"><span data-stu-id="70112-166">Create files in local storage from a startup task</span></span>
<span data-ttu-id="70112-167">U kunt een lokale opslag resource toostore gebruiken bestanden die zijn gemaakt met het starten van de taak die later worden geopend door uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="70112-167">You can use a local storage resource toostore files created by your startup task that is accessed later by your application.</span></span>

<span data-ttu-id="70112-168">toocreate Hallo resource voor lokale opslag, het toevoegen van een [LocalResources] sectie toohello [ServiceDefinition.csdef] -bestand en voeg vervolgens Hallo [LocalStorage] onderliggend element.</span><span class="sxs-lookup"><span data-stu-id="70112-168">toocreate hello local storage resource, add a [LocalResources] section toohello [ServiceDefinition.csdef] file and then add hello [LocalStorage] child element.</span></span> <span data-ttu-id="70112-169">Geeft een unieke naam en de juiste grootte Hallo lokale opslagresource voor het starten van de taak.</span><span class="sxs-lookup"><span data-stu-id="70112-169">Give hello local storage resource a unique name and an appropriate size for your startup task.</span></span>

<span data-ttu-id="70112-170">een bron van de lokale opslag in uw opstarttaak toouse, moet u toocreate een Resourcelocatie omgeving variabele tooreference Hallo lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="70112-170">toouse a local storage resource in your startup task, you need toocreate an environment variable tooreference hello local storage resource location.</span></span> <span data-ttu-id="70112-171">Vervolgens Hallo opstarttaak Hallo toepassing zijn en kunnen tooread en bestanden toohello lokale opslagbron schrijven.</span><span class="sxs-lookup"><span data-stu-id="70112-171">Then hello startup task and hello application are able tooread and write files toohello local storage resource.</span></span>

<span data-ttu-id="70112-172">Hallo relevante secties Hallo **ServiceDefinition.csdef** bestand worden hier weergegeven:</span><span class="sxs-lookup"><span data-stu-id="70112-172">hello relevant sections of hello **ServiceDefinition.csdef** file are shown here:</span></span>

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

<span data-ttu-id="70112-173">Als u bijvoorbeeld dit **Startup.cmd** gebruikt Hallo batchbestand **PathToStartupStorage** omgeving variabele toocreate Hallo bestand **MyTest.txt** op Hallo lokale opslag locatie.</span><span class="sxs-lookup"><span data-stu-id="70112-173">As an example, this **Startup.cmd** batch file uses hello **PathToStartupStorage** environment variable toocreate hello file **MyTest.txt** on hello local storage location.</span></span>

```cmd
REM   Create a simple text file.

ECHO This text will go into hello MyTest.txt file which will be in hello    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed tooby hello PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO hello contents of hello PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit hello batch file with ERRORLEVEL 0.

EXIT /b 0
```

<span data-ttu-id="70112-174">U kunt lokale opslagmap openen vanaf hello Azure SDK met behulp van Hallo [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) methode.</span><span class="sxs-lookup"><span data-stu-id="70112-174">You can access local storage folder from hello Azure SDK by using hello [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-hello-emulator-or-cloud"></a><span data-ttu-id="70112-175">In het Hallo-emulator of cloud worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="70112-175">Run in hello emulator or cloud</span></span>
<span data-ttu-id="70112-176">U kunt uw verschillende stappen uitvoeren wanneer deze wordt uitgevoerd in de Hallo cloud vergeleken toowhen zich in de rekenemulator hello opstarttaak hebben.</span><span class="sxs-lookup"><span data-stu-id="70112-176">You can have your startup task perform different steps when it is operating in hello cloud compared toowhen it is in hello compute emulator.</span></span> <span data-ttu-id="70112-177">U kunt bijvoorbeeld, toouse een nieuw exemplaar van uw SQL-gegevens alleen bij uitvoering in Hallo-emulator.</span><span class="sxs-lookup"><span data-stu-id="70112-177">For example, you may want toouse a fresh copy of your SQL data only when running in hello emulator.</span></span> <span data-ttu-id="70112-178">Of u wilt dat toodo prestatieoptimalisatie voor Hallo cloud hoeft u niet toodo bij uitvoering in Hallo-emulator.</span><span class="sxs-lookup"><span data-stu-id="70112-178">Or you may want toodo some performance optimizations for hello cloud that you don't need toodo when running in hello emulator.</span></span>

<span data-ttu-id="70112-179">Deze mogelijkheid tooperform verschillende acties op Hallo rekenemulator en Hallo cloud kan worden uitgevoerd door het maken van een omgevingsvariabele in Hallo [ServiceDefinition.csdef] bestand.</span><span class="sxs-lookup"><span data-stu-id="70112-179">This ability tooperform different actions on hello compute emulator and hello cloud can be accomplished by creating an environment variable in hello [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="70112-180">U test die omgevingsvariabele voor een waarde in uw taak starten.</span><span class="sxs-lookup"><span data-stu-id="70112-180">You then test that environment variable for a value in your startup task.</span></span>

<span data-ttu-id="70112-181">Hallo omgevingsvariabele toocreate Hallo toevoegen [variabele]/[RoleInstanceValue] element en het maken van een XPath-waarde van `/RoleEnvironment/Deployment/@emulated`.</span><span class="sxs-lookup"><span data-stu-id="70112-181">toocreate hello environment variable, add hello [Variable]/[RoleInstanceValue] element and create an XPath value of `/RoleEnvironment/Deployment/@emulated`.</span></span> <span data-ttu-id="70112-182">waarde van Hallo Hallo **% ComputeEmulatorRunning %** omgevingsvariabele is `true` bij uitvoering op Hallo-rekenemulator en `false` bij uitvoering op Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="70112-182">hello value of hello **%ComputeEmulatorRunning%** environment variable is `true` when running on hello compute emulator, and `false` when running on hello cloud.</span></span>

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

<span data-ttu-id="70112-183">Hallo taak controleren nu Hallo **% ComputeEmulatorRunning %** omgeving variabele tooperform verschillende acties op basis van of Hallo-functie wordt uitgevoerd in Hallo cloud of Hallo emulator.</span><span class="sxs-lookup"><span data-stu-id="70112-183">hello task can now check hello **%ComputeEmulatorRunning%** environment variable tooperform different actions based on whether hello role is running in hello cloud or hello emulator.</span></span> <span data-ttu-id="70112-184">Hier volgt een cmd-shell-script waarmee wordt gecontroleerd of deze omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="70112-184">Here is a .cmd shell script that checks for that environment variable.</span></span>

```cmd
REM   Check if this task is running on hello compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on hello compute emulator. Perform tasks that must be run only in hello compute emulator.
) ELSE (
    REM   This task is running on hello cloud. Perform tasks that must be run only in hello cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a><span data-ttu-id="70112-185">Detecteren of de taak al is uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="70112-185">Detect that your task has already run</span></span>
<span data-ttu-id="70112-186">Hallo-rol kan recycle zonder waardoor uw taken starten toorun opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="70112-186">hello role may recycle without a reboot causing your startup tasks toorun again.</span></span> <span data-ttu-id="70112-187">Er is geen vlag tooindicate die een taak is al uitgevoerd op Hallo hosten van virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="70112-187">There is no flag tooindicate that a task has already run on hello hosting VM.</span></span> <span data-ttu-id="70112-188">Mogelijk hebt u een aantal taken waarbij het maakt niet uit dat ze meerdere keren worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="70112-188">You may have some tasks where it doesn't matter that they run multiple times.</span></span> <span data-ttu-id="70112-189">Echter, u kunt uitvoeren in een situatie waarin u tooprevent moet een taak meer dan één keer worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="70112-189">However, you may run into a situation where you need tooprevent a task from running more than once.</span></span>

<span data-ttu-id="70112-190">het eenvoudigste manier toodetect Hello, die een taak heeft al een bestand in Hallo toocreate is **% TEMP %** map wanneer het Hallo-taak is voltooid en bekijk voor Hallo starten van Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="70112-190">hello simplest way toodetect that a task has already run is toocreate a file in hello **%TEMP%** folder when hello task is successful and look for it at hello start of hello task.</span></span> <span data-ttu-id="70112-191">Hier volgt een voorbeeld cmd shell-script dat die voor u uitvoert.</span><span class="sxs-lookup"><span data-stu-id="70112-191">Here is a sample cmd shell script that does that for you.</span></span>

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

## <a name="task-best-practices"></a><span data-ttu-id="70112-192">Aanbevolen procedures van taak</span><span class="sxs-lookup"><span data-stu-id="70112-192">Task best practices</span></span>
<span data-ttu-id="70112-193">Hier volgen enkele aanbevolen procedures die u volgen moet wanneer de taak voor uw web- of worker-rol configureert.</span><span class="sxs-lookup"><span data-stu-id="70112-193">Here are some best practices you should follow when configuring task for your web or worker role.</span></span>

### <a name="always-log-startup-activities"></a><span data-ttu-id="70112-194">Meld u altijd starten van activiteiten</span><span class="sxs-lookup"><span data-stu-id="70112-194">Always log startup activities</span></span>
<span data-ttu-id="70112-195">Visual Studio biedt geen een foutopsporingsprogramma toostep via batchbestanden, dus is het goed tooget zo veel mogelijk gegevens over Hallo werking van batch-bestanden mogelijk.</span><span class="sxs-lookup"><span data-stu-id="70112-195">Visual Studio does not provide a debugger toostep through batch files, so it's good tooget as much data on hello operation of batch files as possible.</span></span> <span data-ttu-id="70112-196">Hallo-uitvoer van de batch-bestanden logboekregistratie beide **stdout** en **stderr**, kunt u belangrijke informatie geven bij het toodebug en los van de batch-bestanden.</span><span class="sxs-lookup"><span data-stu-id="70112-196">Logging hello output of batch files, both **stdout** and **stderr**, can give you important information when trying toodebug and fix batch files.</span></span> <span data-ttu-id="70112-197">beide toolog **stdout** en **stderr** toohello StartupLog.txt bestand in Hallo directory verwijzen tooby hello **% TEMP %** omgevingsvariabele tekst hello toevoegen`>>  "%TEMP%\\StartupLog.txt" 2>&1`toohello einde van de specifieke regels u wilt dat toolog.</span><span class="sxs-lookup"><span data-stu-id="70112-197">toolog both **stdout** and **stderr** toohello StartupLog.txt file in hello directory pointed tooby hello **%TEMP%** environment variable, add hello text `>>  "%TEMP%\\StartupLog.txt" 2>&1` toohello end of specific lines you want toolog.</span></span> <span data-ttu-id="70112-198">Bijvoorbeeld: tooexecute setup.exe in Hallo **% PathToApp1Install** directory:</span><span class="sxs-lookup"><span data-stu-id="70112-198">For example, tooexecute setup.exe in hello **%PathToApp1Install%** directory:</span></span>

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

<span data-ttu-id="70112-199">toosimplify uw XML-gegevens, kunt u een wrapper *cmd* bestand die alle uw opstarten aanroept taken samen met de logboekregistratie en zorgt ervoor dat elke onderliggende taak shares Hallo dezelfde omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="70112-199">toosimplify your xml, you can create a wrapper *cmd* file that calls all of your startup tasks along with logging and ensures each child-task shares hello same environment variables.</span></span>

<span data-ttu-id="70112-200">Soms is het echter toouse irritante `>> "%TEMP%\StartupLog.txt" 2>&1` op Hallo einde van elke taak starten.</span><span class="sxs-lookup"><span data-stu-id="70112-200">You may find it annoying though toouse `>> "%TEMP%\StartupLog.txt" 2>&1` on hello end of each startup task.</span></span> <span data-ttu-id="70112-201">U kunt de taak logboekregistratie afdwingen door het maken van een wrapper die verantwoordelijk is voor logboekregistratie voor u.</span><span class="sxs-lookup"><span data-stu-id="70112-201">You can enforce task logging by creating a wrapper that handles logging for you.</span></span> <span data-ttu-id="70112-202">Deze wrapper roept echte batchbestand Hallo gewenste toorun.</span><span class="sxs-lookup"><span data-stu-id="70112-202">This wrapper calls hello real batch file you want toorun.</span></span> <span data-ttu-id="70112-203">Elke uitvoer van de doel-batchbestand Hallo worden omgeleid toohello *Startuplog.txt* bestand.</span><span class="sxs-lookup"><span data-stu-id="70112-203">Any output from hello target batch file will be redirected toohello *Startuplog.txt* file.</span></span>

<span data-ttu-id="70112-204">Hallo volgende voorbeeld ziet u hoe u alle tooredirect de uitvoer van een starten van de batch-bestand.</span><span class="sxs-lookup"><span data-stu-id="70112-204">hello following example shows how tooredirect all output from a startup batch file.</span></span> <span data-ttu-id="70112-205">In dit voorbeeld Hallo ServerDefinition.csdef maakt een taak gestart die aanroept *logwrap.cmd*.</span><span class="sxs-lookup"><span data-stu-id="70112-205">In this example, hello ServerDefinition.csdef file creates a startup task that calls *logwrap.cmd*.</span></span> <span data-ttu-id="70112-206">*logwrap.cmd* aanroepen *Startup2.cmd*, alle uitvoer te leiden**% TEMP %\\StartupLog.txt**.</span><span class="sxs-lookup"><span data-stu-id="70112-206">*logwrap.cmd* calls *Startup2.cmd*, redirecting all output too**%TEMP%\\StartupLog.txt**.</span></span>

<span data-ttu-id="70112-207">ServiceDefinition.cmd:</span><span class="sxs-lookup"><span data-stu-id="70112-207">ServiceDefinition.cmd:</span></span>

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

<span data-ttu-id="70112-208">**logwrap.cmd:**</span><span class="sxs-lookup"><span data-stu-id="70112-208">**logwrap.cmd:**</span></span>

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

<span data-ttu-id="70112-209">**Startup2.cmd:**</span><span class="sxs-lookup"><span data-stu-id="70112-209">**Startup2.cmd:**</span></span>

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

<span data-ttu-id="70112-210">Voorbeeld van uitvoer in Hallo **StartupLog.txt** bestand:</span><span class="sxs-lookup"><span data-stu-id="70112-210">Sample output in hello **StartupLog.txt** file:</span></span>

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> <span data-ttu-id="70112-211">Hallo **StartupLog.txt** bestand bevindt zich in Hallo *C:\Resources\temp\\{rol-id} \RoleTemp* map.</span><span class="sxs-lookup"><span data-stu-id="70112-211">hello **StartupLog.txt** file is located in hello *C:\Resources\temp\\{role identifier}\RoleTemp* folder.</span></span>
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a><span data-ttu-id="70112-212">Set executionContext op de juiste wijze voor opstarttaken</span><span class="sxs-lookup"><span data-stu-id="70112-212">Set executionContext appropriately for startup tasks</span></span>
<span data-ttu-id="70112-213">Stel bevoegdheden op de juiste wijze voor Hallo starten van de taak.</span><span class="sxs-lookup"><span data-stu-id="70112-213">Set privileges appropriately for hello startup task.</span></span> <span data-ttu-id="70112-214">Soms moeten starten van de taken uitvoeren met verhoogde bevoegdheden Hoewel Hallo-rol wordt uitgevoerd met normale bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="70112-214">Sometimes startup tasks must run with elevated privileges even though hello role runs with normal privileges.</span></span>

<span data-ttu-id="70112-215">Hallo [executionContext][taak] kenmerk machtigingsniveau Hallo van Hallo starten van de taak wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="70112-215">hello [executionContext][Task] attribute sets hello privilege level of hello startup task.</span></span> <span data-ttu-id="70112-216">Met behulp van `executionContext="limited"` betekent Hallo starten van de taak heeft Hallo hetzelfde niveau van bevoegdheden als Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="70112-216">Using `executionContext="limited"` means hello startup task has hello same privilege level as hello role.</span></span> <span data-ttu-id="70112-217">Met behulp van `executionContext="elevated"` betekent Hallo opstarttaak administrator-bevoegdheden heeft, kunnen de Hallo opstarten taak tooperform beheerderstaken zonder administrator-bevoegdheden tooyour rol toekennen.</span><span class="sxs-lookup"><span data-stu-id="70112-217">Using `executionContext="elevated"` means hello startup task has administrator privileges, which allows hello startup task tooperform administrator tasks without giving administrator privileges tooyour role.</span></span>

<span data-ttu-id="70112-218">Een voorbeeld van een taak gestart die zijn verhoogde bevoegdheden vereist is een taak gestart die gebruikmaakt van **AppCmd.exe** tooconfigure IIS.</span><span class="sxs-lookup"><span data-stu-id="70112-218">An example of a startup task that requires elevated privileges is a startup task that uses **AppCmd.exe** tooconfigure IIS.</span></span> <span data-ttu-id="70112-219">**AppCmd.exe** vereist `executionContext="elevated"`.</span><span class="sxs-lookup"><span data-stu-id="70112-219">**AppCmd.exe** requires `executionContext="elevated"`.</span></span>

### <a name="use-hello-appropriate-tasktype"></a><span data-ttu-id="70112-220">Gebruik de juiste taskType Hallo</span><span class="sxs-lookup"><span data-stu-id="70112-220">Use hello appropriate taskType</span></span>
<span data-ttu-id="70112-221">Hallo [taskType][taak] kenmerk bepaalt Hallo manier Hallo starten van de taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="70112-221">hello [taskType][Task] attribute determines hello way hello startup task is executed.</span></span> <span data-ttu-id="70112-222">Er zijn drie waarden: **eenvoudige**, **achtergrond**, en **voorgrond**.</span><span class="sxs-lookup"><span data-stu-id="70112-222">There are three values: **simple**, **background**, and **foreground**.</span></span> <span data-ttu-id="70112-223">Hallo en achtergrond taken zijn gestart asynchroon en vervolgens Hallo eenvoudige taken synchroon uitgevoerd één tegelijk.</span><span class="sxs-lookup"><span data-stu-id="70112-223">hello background and foreground tasks are started asynchronously, and then hello simple tasks are executed synchronously one at a time.</span></span>

<span data-ttu-id="70112-224">Met **eenvoudige** starten van de taken, kunt u Hallo in welke volgorde Hallo taken uitgevoerd door Hallo volgorde welke Hallo taken worden opgenomen in Hallo ServiceDefinition.csdef bestand instellen.</span><span class="sxs-lookup"><span data-stu-id="70112-224">With **simple** startup tasks, you can set hello order in which hello tasks run by hello order in which hello tasks are listed in hello ServiceDefinition.csdef file.</span></span> <span data-ttu-id="70112-225">Als een **eenvoudige** taak eindigt met een niet-nul afsluitcode en vervolgens opstarten procedure stopt Hallo en Hallo-rol niet gestart.</span><span class="sxs-lookup"><span data-stu-id="70112-225">If a **simple** task ends with a non-zero exit code, then hello startup procedure stops and hello role does not start.</span></span>

<span data-ttu-id="70112-226">verschil tussen Hallo **achtergrond** starten van de taken en **voorgrond** starten van de taken is dat **voorgrond** taken houden Hallo rol uitgevoerd totdat Hallo  **voorgrond** taak is geëindigd.</span><span class="sxs-lookup"><span data-stu-id="70112-226">hello difference between **background** startup tasks and **foreground** startup tasks is that **foreground** tasks keep hello role running until hello **foreground** task ends.</span></span> <span data-ttu-id="70112-227">Dit betekent ook dat als hello **voorgrond** taak vastloopt of crasht, Hallo-rol niet gerecycled tot Hallo **voorgrond** taak wordt geforceerd gesloten.</span><span class="sxs-lookup"><span data-stu-id="70112-227">This also means that if hello **foreground** task hangs or crashes, hello role will not recycle until hello **foreground** task is forced closed.</span></span> <span data-ttu-id="70112-228">Om deze reden **achtergrond** taken worden aanbevolen voor het starten van de asynchrone taken alleen u deze functie Hallo moet **voorgrond** taak.</span><span class="sxs-lookup"><span data-stu-id="70112-228">For this reason, **background** tasks are recommended for asynchronous startup tasks unless you need that feature of hello **foreground** task.</span></span>

### <a name="end-batch-files-with-exit-b-0"></a><span data-ttu-id="70112-229">Einde batch-bestanden met de AFSLUITCODE /B 0</span><span class="sxs-lookup"><span data-stu-id="70112-229">End batch files with EXIT /B 0</span></span>
<span data-ttu-id="70112-230">Hallo rol wordt alleen gestart als hello **errorlevel** van elk van uw eenvoudige starten van de taak is aan nul.</span><span class="sxs-lookup"><span data-stu-id="70112-230">hello role will only start if hello **errorlevel** from each of your simple startup task is zero.</span></span> <span data-ttu-id="70112-231">Niet alle programma's ingesteld Hallo **errorlevel** (afsluitcode) correct, dus Hallo batch-bestand moet eindigen met een `EXIT /B 0` als alles goed is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="70112-231">Not all programs set hello **errorlevel** (exit code) correctly, so hello batch file should end with an `EXIT /B 0` if everything ran correctly.</span></span>

<span data-ttu-id="70112-232">Een ontbrekende `EXIT /B 0` Hallo einde van een starten van de batch-bestand is een veelvoorkomende oorzaak van de functies die niet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="70112-232">A missing `EXIT /B 0` at hello end of a startup batch file is a common cause of roles that do not start.</span></span>

> [!NOTE]
> <span data-ttu-id="70112-233">Ik opgevallen dat geneste batch bestanden soms vastlopen wanneer u Hallo `/B` parameter.</span><span class="sxs-lookup"><span data-stu-id="70112-233">I've noticed that nested batch files sometimes hang when using hello `/B` parameter.</span></span> <span data-ttu-id="70112-234">Desgewenst kunt u ervoor dat dit probleem blijft hangen niet gebeurt als een ander batchbestand het huidige batchbestand roept, zoals als u Hallo toomake [logboek wrapper](#always-log-startup-activities).</span><span class="sxs-lookup"><span data-stu-id="70112-234">You may want toomake sure that this hang problem does not happen if another batch file calls your current batch file, like if you use hello [log wrapper](#always-log-startup-activities).</span></span> <span data-ttu-id="70112-235">U kunt Hallo weglaten `/B` parameter in dit geval.</span><span class="sxs-lookup"><span data-stu-id="70112-235">You can omit hello `/B` parameter in this case.</span></span>
> 
> 

### <a name="expect-startup-tasks-toorun-more-than-once"></a><span data-ttu-id="70112-236">Starten van de taken toorun meer dan één keer verwacht</span><span class="sxs-lookup"><span data-stu-id="70112-236">Expect startup tasks toorun more than once</span></span>
<span data-ttu-id="70112-237">Niet alle rol recyclet zijn opnieuw worden opgestart, maar alle rol recyclet omvatten alle starten van de taken uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="70112-237">Not all role recycles include a reboot, but all role recycles include running all startup tasks.</span></span> <span data-ttu-id="70112-238">Dit betekent dat starten van de taken kunnen toorun meerdere keren tussen opnieuw wordt opgestart zonder problemen moeten zijn.</span><span class="sxs-lookup"><span data-stu-id="70112-238">This means that startup tasks must be able toorun multiple times between reboots without any problems.</span></span> <span data-ttu-id="70112-239">Dit wordt besproken in Hallo [voorgaande sectie](#detect-that-your-task-has-already-run).</span><span class="sxs-lookup"><span data-stu-id="70112-239">This is discussed in hello [preceding section](#detect-that-your-task-has-already-run).</span></span>

### <a name="use-local-storage-toostore-files-that-must-be-accessed-in-hello-role"></a><span data-ttu-id="70112-240">Lokale opslag toostore bestanden die moeten worden geopend in de rol hello gebruiken</span><span class="sxs-lookup"><span data-stu-id="70112-240">Use local storage toostore files that must be accessed in hello role</span></span>
<span data-ttu-id="70112-241">Als u wilt dat toocopy of maak een bestand tijdens het starten van de taak die vervolgens toegankelijk tooyour rol, wordt dat bestand moet worden geplaatst in de lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="70112-241">If you want toocopy or create a file during your startup task that is then accessible tooyour role, then that file must be placed in local storage.</span></span> <span data-ttu-id="70112-242">Zie Hallo [voorgaande sectie](#create-files-in-local-storage-from-a-startup-task).</span><span class="sxs-lookup"><span data-stu-id="70112-242">See hello [preceding section](#create-files-in-local-storage-from-a-startup-task).</span></span>

## <a name="next-steps"></a><span data-ttu-id="70112-243">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="70112-243">Next steps</span></span>
<span data-ttu-id="70112-244">Bekijk Hallo cloud [service model- en -pakket](cloud-services-model-and-package.md)</span><span class="sxs-lookup"><span data-stu-id="70112-244">Review hello cloud [service model and package](cloud-services-model-and-package.md)</span></span>

<span data-ttu-id="70112-245">Meer informatie over het [taken](cloud-services-startup-tasks.md) werken.</span><span class="sxs-lookup"><span data-stu-id="70112-245">Learn more about how [Tasks](cloud-services-startup-tasks.md) work.</span></span>

<span data-ttu-id="70112-246">[Maken en implementeren van](cloud-services-how-to-create-deploy-portal.md) uw cloud-pakket.</span><span class="sxs-lookup"><span data-stu-id="70112-246">[Create and deploy](cloud-services-how-to-create-deploy-portal.md) your cloud service package.</span></span>

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
