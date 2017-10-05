---
title: Algemene starten van de taken voor Cloudservices | Microsoft Docs
description: Enkele voorbeelden van algemene starten van de taken die u wilt uitvoeren in uw cloud services-web-rol of functie worker biedt.
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
ms.openlocfilehash: cee23da5b089b02bfc0ef10afd60f0f2272585b1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="common-cloud-service-startup-tasks"></a><span data-ttu-id="a92b1-103">Algemene taken voor Cloud-Service starten</span><span class="sxs-lookup"><span data-stu-id="a92b1-103">Common Cloud Service startup tasks</span></span>
<span data-ttu-id="a92b1-104">Dit artikel vindt enkele voorbeelden van algemene starten van de taken die u wilt uitvoeren in uw cloudservice.</span><span class="sxs-lookup"><span data-stu-id="a92b1-104">This article provides some examples of common startup tasks you may want to perform in your cloud service.</span></span> <span data-ttu-id="a92b1-105">Starten van de taken kunt u bewerkingen uitvoeren voordat een rol wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="a92b1-105">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="a92b1-106">Bewerkingen die u wilt uitvoeren bevatten voor het installeren van een onderdeel, registreren van COM-onderdelen, registersleutels instellen of starten van een langdurige proces.</span><span class="sxs-lookup"><span data-stu-id="a92b1-106">Operations that you might want to perform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span> 

<span data-ttu-id="a92b1-107">Zie [in dit artikel](cloud-services-startup-tasks.md) over de werking van starten van de taken en specifiek het maken van de vermeldingen die een taak starten definiëren.</span><span class="sxs-lookup"><span data-stu-id="a92b1-107">See [this article](cloud-services-startup-tasks.md) to understand how startup tasks work, and specifically how to create the entries that define a startup task.</span></span>

> [!NOTE]
> <span data-ttu-id="a92b1-108">Starten van de taken zijn niet van toepassing op virtuele Machines, alleen op Cloud Service-Web- en werkrollen.</span><span class="sxs-lookup"><span data-stu-id="a92b1-108">Startup tasks are not applicable to Virtual Machines, only to Cloud Service Web and Worker roles.</span></span>
> 

## <a name="define-environment-variables-before-a-role-starts"></a><span data-ttu-id="a92b1-109">Omgevingsvariabelen definiëren voordat een rol wordt gestart</span><span class="sxs-lookup"><span data-stu-id="a92b1-109">Define environment variables before a role starts</span></span>
<span data-ttu-id="a92b1-110">Als u omgevingsvariabelen die zijn gedefinieerd voor een specifieke taak nodig hebt, gebruikt de [omgeving] -element in de [taak] element.</span><span class="sxs-lookup"><span data-stu-id="a92b1-110">If you need environment variables defined for a specific task, use the [Environment] element inside the [Task] element.</span></span>

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

<span data-ttu-id="a92b1-111">Variabelen kunt ook een [geldige Azure XPath-waarde](cloud-services-role-config-xpath.md) om te verwijzen naar iets over de implementatie.</span><span class="sxs-lookup"><span data-stu-id="a92b1-111">Variables can also use a [valid Azure XPath value](cloud-services-role-config-xpath.md) to reference something about the deployment.</span></span> <span data-ttu-id="a92b1-112">In plaats van de `value` kenmerk, het definiëren van een [RoleInstanceValue] onderliggend element.</span><span class="sxs-lookup"><span data-stu-id="a92b1-112">Instead of using the `value` attribute, define a [RoleInstanceValue] child element.</span></span>

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a><span data-ttu-id="a92b1-113">Starten van IIS met AppCmd.exe configureren</span><span class="sxs-lookup"><span data-stu-id="a92b1-113">Configure IIS startup with AppCmd.exe</span></span>
<span data-ttu-id="a92b1-114">De [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) opdrachtregelprogramma kan worden gebruikt voor het beheren van IIS-instellingen bij het opstarten op Azure.</span><span class="sxs-lookup"><span data-stu-id="a92b1-114">The [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) command-line tool can be used to manage IIS settings at startup on Azure.</span></span> <span data-ttu-id="a92b1-115">*AppCmd.exe* handige, opdrachtregel toegang biedt tot configuratie-instellingen voor gebruik in het starten van de taken in Azure.</span><span class="sxs-lookup"><span data-stu-id="a92b1-115">*AppCmd.exe* provides convenient, command-line access to configuration settings for use in startup tasks on Azure.</span></span> <span data-ttu-id="a92b1-116">Met behulp van *AppCmd.exe*, Website-instellingen kunnen worden toegevoegd, gewijzigd of verwijderd voor toepassingen en sites.</span><span class="sxs-lookup"><span data-stu-id="a92b1-116">Using *AppCmd.exe*, Website settings can be added, modified, or removed for applications and sites.</span></span>

<span data-ttu-id="a92b1-117">Er zijn echter enkele dingen die u moet letten in het gebruik van *AppCmd.exe* als een taak starten:</span><span class="sxs-lookup"><span data-stu-id="a92b1-117">However, there are a few things to watch out for in the use of *AppCmd.exe* as a startup task:</span></span>

* <span data-ttu-id="a92b1-118">Starten van de taken kunnen meer dan één keer worden uitgevoerd tussen opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="a92b1-118">Startup tasks can be run more than once between reboots.</span></span> <span data-ttu-id="a92b1-119">Bijvoorbeeld, wanneer een rol wordt gerecycled.</span><span class="sxs-lookup"><span data-stu-id="a92b1-119">For instance, when a role recycles.</span></span>
* <span data-ttu-id="a92b1-120">Als een *AppCmd.exe* actie meer dan één keer wordt uitgevoerd, kan er een fout gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="a92b1-120">If a *AppCmd.exe* action is performed more than once, it may generate an error.</span></span> <span data-ttu-id="a92b1-121">Wilt u bijvoorbeeld een sectie toevoegen *Web.config* tweemaal genereren een fout.</span><span class="sxs-lookup"><span data-stu-id="a92b1-121">For example, attempting to add a section to *Web.config* twice could generate an error.</span></span>
* <span data-ttu-id="a92b1-122">Starten van de taken mislukken als ze een afsluitcode dan nul retourneren of **errorlevel**.</span><span class="sxs-lookup"><span data-stu-id="a92b1-122">Startup tasks fail if they return a non-zero exit code or **errorlevel**.</span></span> <span data-ttu-id="a92b1-123">Bijvoorbeeld, wanneer *AppCmd.exe* wordt een fout gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="a92b1-123">For example, when *AppCmd.exe* generates an error.</span></span>

<span data-ttu-id="a92b1-124">Het is raadzaam om te controleren de **errorlevel** na het aanroepen *AppCmd.exe*, dit is eenvoudig te doen als u de aanroep van inpakt *AppCmd.exe* met een *.cmd* bestand.</span><span class="sxs-lookup"><span data-stu-id="a92b1-124">It is a good practice to check the **errorlevel** after calling *AppCmd.exe*, which is easy to do if you wrap the call to *AppCmd.exe* with a *.cmd* file.</span></span> <span data-ttu-id="a92b1-125">Als u een bekende detecteren **errorlevel** antwoord, u kunt deze negeren of terug doorgeven.</span><span class="sxs-lookup"><span data-stu-id="a92b1-125">If you detect a known **errorlevel** response, you can ignore it, or pass it back.</span></span>

<span data-ttu-id="a92b1-126">De waarde voor errorlevel geretourneerd door *AppCmd.exe* worden weergegeven in het bestand winerror.h en kunnen ook worden weergegeven op [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span><span class="sxs-lookup"><span data-stu-id="a92b1-126">The errorlevel returned by *AppCmd.exe* are listed in the winerror.h file, and can also be seen on [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span></span>

### <a name="example-of-managing-the-error-level"></a><span data-ttu-id="a92b1-127">Voorbeeld van het beheer van het foutniveau van de</span><span class="sxs-lookup"><span data-stu-id="a92b1-127">Example of managing the error level</span></span>
<span data-ttu-id="a92b1-128">In dit voorbeeld voegt u een sectie compressie en een compressie-vermelding voor JSON voor de *Web.config* bestand met de foutafhandeling en logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="a92b1-128">This example adds a compression section and a compression entry for JSON to the *Web.config* file, with error handling and logging.</span></span>

<span data-ttu-id="a92b1-129">De relevante secties van de [ServiceDefinition.csdef] bestand hier worden weergegeven, zoals instelling de [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) kenmerk `elevated` geven *AppCmd.exe* voldoende machtigingen om te wijzigen van de instellingen in de *Web.config* bestand:</span><span class="sxs-lookup"><span data-stu-id="a92b1-129">The relevant sections of the [ServiceDefinition.csdef] file are shown here, which include setting the [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) attribute to `elevated` to give *AppCmd.exe* sufficient permissions to change the settings in the *Web.config* file:</span></span>

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

<span data-ttu-id="a92b1-130">De *Startup.cmd* batch-bestand gebruikt *AppCmd.exe* toevoegen van een sectie compressie en een compressie-vermelding voor JSON naar de *Web.config* bestand.</span><span class="sxs-lookup"><span data-stu-id="a92b1-130">The *Startup.cmd* batch file uses *AppCmd.exe* to add a compression section and a compression entry for JSON to the *Web.config* file.</span></span> <span data-ttu-id="a92b1-131">De verwachte **errorlevel** van 183 is ingesteld op nul met behulp van de CONTROLEER. EXE-opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="a92b1-131">The expected **errorlevel** of 183 is set to zero using the VERIFY.EXE command-line program.</span></span> <span data-ttu-id="a92b1-132">Onverwachte errorlevels zijn StartupErrorLog.txt aangemeld.</span><span class="sxs-lookup"><span data-stu-id="a92b1-132">Unexpected errorlevels are logged to StartupErrorLog.txt.</span></span>

```cmd
REM   *** Add a compression section to the Web.config file. ***
%windir%\system32\inetsrv\appcmd set config /section:urlCompression /doDynamicCompression:True /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1

REM   ERRORLEVEL 183 occurs when trying to add a section that already exists. This error is expected if this
REM   batch file were executed twice. This can occur and must be accounted for in a Azure startup
REM   task. To handle this situation, set the ERRORLEVEL to zero by using the Verify command. The Verify
REM   command will safely set the ERRORLEVEL to zero.
IF %ERRORLEVEL% EQU 183 DO VERIFY > NUL

REM   If the ERRORLEVEL is not zero at this point, some other error occurred.
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding a compression section to the Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Add compression for json. ***
%windir%\system32\inetsrv\appcmd set config  -section:system.webServer/httpCompression /+"dynamicTypes.[mimeType='application/json; charset=utf-8',enabled='True']" /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1
IF %ERRORLEVEL% EQU 183 VERIFY > NUL
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding the JSON compression type to the Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Exit batch file. ***
EXIT /b 0

REM   *** Log error and exit ***
:ErrorExit
REM   Report the date, time, and ERRORLEVEL of the error.
DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
ECHO An error occurred during startup. ERRORLEVEL = %ERRORLEVEL% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT %ERRORLEVEL%
```

## <a name="add-firewall-rules"></a><span data-ttu-id="a92b1-133">Firewallregels toevoegen</span><span class="sxs-lookup"><span data-stu-id="a92b1-133">Add firewall rules</span></span>
<span data-ttu-id="a92b1-134">In Azure zijn er effectief twee firewalls.</span><span class="sxs-lookup"><span data-stu-id="a92b1-134">In Azure, there are effectively two firewalls.</span></span> <span data-ttu-id="a92b1-135">De eerste firewall bepaalt verbindingen tussen de virtuele machine en de buitenwereld.</span><span class="sxs-lookup"><span data-stu-id="a92b1-135">The first firewall controls connections between the virtual machine and the outside world.</span></span> <span data-ttu-id="a92b1-136">Deze firewall wordt bepaald door de [eindpunten] -element in de [ServiceDefinition.csdef] bestand.</span><span class="sxs-lookup"><span data-stu-id="a92b1-136">This firewall is controlled by the [EndPoints] element in the [ServiceDefinition.csdef] file.</span></span>

<span data-ttu-id="a92b1-137">De tweede firewall bepaalt verbindingen tussen de virtuele machine en de processen op dat de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="a92b1-137">The second firewall controls connections between the virtual machine and the processes within that virtual machine.</span></span> <span data-ttu-id="a92b1-138">Deze firewall kan worden beheerd door de `netsh advfirewall firewall` opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="a92b1-138">This firewall can be controlled by the `netsh advfirewall firewall` command-line tool.</span></span>

<span data-ttu-id="a92b1-139">Azure maakt firewallregels voor de processen binnen uw rollen gestart.</span><span class="sxs-lookup"><span data-stu-id="a92b1-139">Azure creates firewall rules for the processes started within your roles.</span></span> <span data-ttu-id="a92b1-140">Bijvoorbeeld, wanneer u een service of programma start, maakt Azure automatisch de benodigde firewallregels om toe te staan of de service te communiceren met Internet.</span><span class="sxs-lookup"><span data-stu-id="a92b1-140">For example, when you start a service or program, Azure automatically creates the necessary firewall rules to allow that service to communicate with the Internet.</span></span> <span data-ttu-id="a92b1-141">Als u een service die wordt gestart door een proces buiten uw rol (zoals een COM +-service of een Windows-taak plannen) maakt, moet u handmatig een firewallregel voor toegang tot deze service te maken.</span><span class="sxs-lookup"><span data-stu-id="a92b1-141">However, if you create a service that is started by a process outside your role (like a COM+ service or a Windows Scheduled Task), you need to manually create a firewall rule to allow access to that service.</span></span> <span data-ttu-id="a92b1-142">Deze firewall-regels kunnen worden gemaakt met behulp van een taak starten.</span><span class="sxs-lookup"><span data-stu-id="a92b1-142">These firewall rules can be created by using a startup task.</span></span>

<span data-ttu-id="a92b1-143">Een starten van de taak die wordt gemaakt van een firewallregel moet hebben een [executionContext][taak] van **verhoogde**.</span><span class="sxs-lookup"><span data-stu-id="a92b1-143">A startup task that creates a firewall rule must have an [executionContext][Task] of **elevated**.</span></span> <span data-ttu-id="a92b1-144">Voeg de volgende opstarttaak naar de [ServiceDefinition.csdef] bestand.</span><span class="sxs-lookup"><span data-stu-id="a92b1-144">Add the following startup task to the [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="a92b1-145">Als u wilt de firewallregel toevoegen, moet u de juiste `netsh advfirewall firewall` opdrachten in het batchbestand opstarten.</span><span class="sxs-lookup"><span data-stu-id="a92b1-145">To add the firewall rule, you must use the appropriate `netsh advfirewall firewall` commands in your startup batch file.</span></span> <span data-ttu-id="a92b1-146">In dit voorbeeld vereist de taak starten van de beveiliging en versleuteling voor TCP-poort 80.</span><span class="sxs-lookup"><span data-stu-id="a92b1-146">In this example, the startup task requires security and encryption for TCP port 80.</span></span>

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a><span data-ttu-id="a92b1-147">Een specifiek IP-adres blokkeren</span><span class="sxs-lookup"><span data-stu-id="a92b1-147">Block a specific IP address</span></span>
<span data-ttu-id="a92b1-148">U kunt de toegang van een Azure-web-rol op een reeks opgegeven IP-adressen beperken door het wijzigen van de IIS **web.config** bestand.</span><span class="sxs-lookup"><span data-stu-id="a92b1-148">You can restrict an Azure web role access to a set of specified IP addresses by modifying your IIS **web.config** file.</span></span> <span data-ttu-id="a92b1-149">U moet ook een opdrachtbestand waarmee wordt ontgrendeld gebruiken de **ipSecurity** sectie van de **ApplicationHost.config** bestand.</span><span class="sxs-lookup"><span data-stu-id="a92b1-149">You also need to use a command file which unlocks the **ipSecurity** section of the **ApplicationHost.config** file.</span></span>

<span data-ttu-id="a92b1-150">Voor het ontgrendelen van de **ipSecurity** sectie van de **ApplicationHost.config** bestand, een opdrachtbestand maken dat wordt uitgevoerd op de rol is gestart.</span><span class="sxs-lookup"><span data-stu-id="a92b1-150">To do unlock the **ipSecurity** section of the **ApplicationHost.config** file, create a command file that runs at role start.</span></span> <span data-ttu-id="a92b1-151">Maak een map op het hoofdniveau van de Webrol aangeroepen **opstarten** en maak in deze map een batchbestand aangeroepen **startup.cmd**.</span><span class="sxs-lookup"><span data-stu-id="a92b1-151">Create a folder at the root level of your web role called **startup** and, within this folder, create a batch file called **startup.cmd**.</span></span> <span data-ttu-id="a92b1-152">Dit bestand toevoegen aan uw Visual Studio-project en de eigenschappen instellen op **kopie altijd** om ervoor te zorgen dat is opgenomen in het pakket.</span><span class="sxs-lookup"><span data-stu-id="a92b1-152">Add this file to your Visual Studio project and set the properties to **Copy Always** to ensure that it is included in your package.</span></span>

<span data-ttu-id="a92b1-153">Voeg de volgende opstarttaak naar de [ServiceDefinition.csdef] bestand.</span><span class="sxs-lookup"><span data-stu-id="a92b1-153">Add the following startup task to the [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="a92b1-154">Deze opdracht kunt toevoegen de **startup.cmd** bestand:</span><span class="sxs-lookup"><span data-stu-id="a92b1-154">Add this command to the **startup.cmd** file:</span></span>

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

<span data-ttu-id="a92b1-155">Met deze taak wordt de **startup.cmd** batchbestand worden uitgevoerd telkens als de Webrol is geïnitialiseerd, zorgt u ervoor dat de vereiste **ipSecurity** sectie is opgeheven.</span><span class="sxs-lookup"><span data-stu-id="a92b1-155">This task causes the **startup.cmd** batch file to be run every time the web role is initialized, ensuring that the required **ipSecurity** section is unlocked.</span></span>

<span data-ttu-id="a92b1-156">Wijzig tot slot de [system.webServer sectie](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) uw Webrol **web.config** bestand toevoegen van een lijst met IP-adressen die toegang, zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a92b1-156">Finally, modify the [system.webServer section](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) your web role’s **web.config** file to add a list of IP addresses that are granted access, as shown in the following example:</span></span>

<span data-ttu-id="a92b1-157">De configuratie van dit voorbeeld **kunt** alle IP-adressen voor toegang tot de server met uitzondering van de twee gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="a92b1-157">This sample config **allows** all IPs to access the server except the two defined</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are granted access-->
    <ipSecurity>
        <!--The following IP addresses are denied access-->
        <add allowed="false" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="false" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

<span data-ttu-id="a92b1-158">De configuratie van dit voorbeeld **weigert** alle IP-adressen van de toegang tot de server, met uitzondering van de twee gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="a92b1-158">This sample config **denies** all IPs from accessing the server except for the two defined.</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are denied access-->
    <ipSecurity allowUnlisted="false">
        <!--The following IP addresses are granted access-->
        <add allowed="true" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="true" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

## <a name="create-a-powershell-startup-task"></a><span data-ttu-id="a92b1-159">Een PowerShell starten van de taak maken</span><span class="sxs-lookup"><span data-stu-id="a92b1-159">Create a PowerShell startup task</span></span>
<span data-ttu-id="a92b1-160">Windows PowerShell-scripts, kunnen niet worden aangeroepen rechtstreeks vanuit de [ServiceDefinition.csdef] bestand, maar ze kunnen worden aangeroepen vanuit een batchbestand opstarten.</span><span class="sxs-lookup"><span data-stu-id="a92b1-160">Windows PowerShell scripts cannot be called directly from the [ServiceDefinition.csdef] file, but they can be invoked from within a startup batch file.</span></span>

<span data-ttu-id="a92b1-161">Niet-ondertekende scripts niet wordt uitgevoerd in PowerShell (standaard).</span><span class="sxs-lookup"><span data-stu-id="a92b1-161">PowerShell (by default) does not run unsigned scripts.</span></span> <span data-ttu-id="a92b1-162">Tenzij u uw script ondertekent, moet u PowerShell als u wilt uitvoeren van niet-ondertekende scripts configureren.</span><span class="sxs-lookup"><span data-stu-id="a92b1-162">Unless you sign your script, you need to configure PowerShell to run unsigned scripts.</span></span> <span data-ttu-id="a92b1-163">Niet-ondertekende scripts uitvoeren de **ExecutionPolicy** moet worden ingesteld op **onbeperkt**.</span><span class="sxs-lookup"><span data-stu-id="a92b1-163">To run unsigned scripts, the **ExecutionPolicy** must be set to **Unrestricted**.</span></span> <span data-ttu-id="a92b1-164">De **ExecutionPolicy** instelt dat u gebruik is op basis van de versie van Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a92b1-164">The **ExecutionPolicy** setting that you use is based on the version of Windows PowerShell.</span></span>

```cmd
REM   Run an unsigned PowerShell script and log the output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

<span data-ttu-id="a92b1-165">Als u een Gastbesturingssysteem dat wordt uitgevoerd, PowerShell 2.0 of 1.0 die u kunt afdwingen dat versie 2 om uit te voeren, en als niet beschikbaar is, wordt versie 1 gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a92b1-165">If you're using a Guest OS that is runs PowerShell 2.0 or 1.0 you can force version 2 to run, and if unavailable, use version 1.</span></span>

```cmd
REM   Attempt to set the execution policy by using PowerShell version 2.0 syntax.
PowerShell -Version 2.0 -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If PowerShell version 2.0 isn't available. Set the execution policy by using the PowerShell
IF %ERRORLEVEL% EQU -393216 (
   PowerShell -Command "Set-ExecutionPolicy Unrestricted" >> "%TEMP%\StartupLog.txt" 2>&1
   PowerShell .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1
)

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

## <a name="create-files-in-local-storage-from-a-startup-task"></a><span data-ttu-id="a92b1-166">Maken van bestanden in lokale opslag van een taak starten</span><span class="sxs-lookup"><span data-stu-id="a92b1-166">Create files in local storage from a startup task</span></span>
<span data-ttu-id="a92b1-167">U kunt een resource voor lokale opslag gebruiken voor het opslaan van bestanden die zijn gemaakt met het starten van de taak die later worden geopend door uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="a92b1-167">You can use a local storage resource to store files created by your startup task that is accessed later by your application.</span></span>

<span data-ttu-id="a92b1-168">Toevoegen voor het maken van de bron van de lokale opslag, een [LocalResources] sectie aan de [ServiceDefinition.csdef] -bestand en voeg vervolgens de [LocalStorage] onderliggend element.</span><span class="sxs-lookup"><span data-stu-id="a92b1-168">To create the local storage resource, add a [LocalResources] section to the [ServiceDefinition.csdef] file and then add the [LocalStorage] child element.</span></span> <span data-ttu-id="a92b1-169">Geeft de bron van de lokale opslag een unieke naam en de juiste grootte voor het starten van de taak.</span><span class="sxs-lookup"><span data-stu-id="a92b1-169">Give the local storage resource a unique name and an appropriate size for your startup task.</span></span>

<span data-ttu-id="a92b1-170">Als u een resource voor lokale opslag in uw taak starten, moet u een omgevingsvariabele om te verwijzen naar de lokale resource opslaglocatie maken.</span><span class="sxs-lookup"><span data-stu-id="a92b1-170">To use a local storage resource in your startup task, you need to create an environment variable to reference the local storage resource location.</span></span> <span data-ttu-id="a92b1-171">Vervolgens kunnen de taak starten en de toepassing bestanden lezen en schrijven naar de bron van de lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="a92b1-171">Then the startup task and the application are able to read and write files to the local storage resource.</span></span>

<span data-ttu-id="a92b1-172">De relevante secties van de **ServiceDefinition.csdef** bestand worden hier weergegeven:</span><span class="sxs-lookup"><span data-stu-id="a92b1-172">The relevant sections of the **ServiceDefinition.csdef** file are shown here:</span></span>

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

<span data-ttu-id="a92b1-173">Als u bijvoorbeeld dit **Startup.cmd** batch-bestand gebruikt de **PathToStartupStorage** omgevingsvariabele voor het maken van het bestand **MyTest.txt** op de locatie van lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="a92b1-173">As an example, this **Startup.cmd** batch file uses the **PathToStartupStorage** environment variable to create the file **MyTest.txt** on the local storage location.</span></span>

```cmd
REM   Create a simple text file.

ECHO This text will go into the MyTest.txt file which will be in the    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed to by the PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO The contents of the PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit the batch file with ERRORLEVEL 0.

EXIT /b 0
```

<span data-ttu-id="a92b1-174">U kunt lokale opslagmap openen vanaf de Azure SDK met behulp van de [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) methode.</span><span class="sxs-lookup"><span data-stu-id="a92b1-174">You can access local storage folder from the Azure SDK by using the [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-the-emulator-or-cloud"></a><span data-ttu-id="a92b1-175">Uitgevoerd in de emulator of de cloud</span><span class="sxs-lookup"><span data-stu-id="a92b1-175">Run in the emulator or cloud</span></span>
<span data-ttu-id="a92b1-176">U kunt uw opstarttaak verschillende stappen uitvoeren wanneer deze wordt uitgevoerd in de cloud in vergelijking met wanneer het zich in de rekenemulator hebben.</span><span class="sxs-lookup"><span data-stu-id="a92b1-176">You can have your startup task perform different steps when it is operating in the cloud compared to when it is in the compute emulator.</span></span> <span data-ttu-id="a92b1-177">U wilt bijvoorbeeld een nieuw exemplaar van uw SQL-gegevens gebruiken alleen bij het uitvoeren in de emulator.</span><span class="sxs-lookup"><span data-stu-id="a92b1-177">For example, you may want to use a fresh copy of your SQL data only when running in the emulator.</span></span> <span data-ttu-id="a92b1-178">Of u kunt doen prestatieoptimalisatie voor de cloud die u niet hoeft te doen wanneer uitgevoerd in de emulator.</span><span class="sxs-lookup"><span data-stu-id="a92b1-178">Or you may want to do some performance optimizations for the cloud that you don't need to do when running in the emulator.</span></span>

<span data-ttu-id="a92b1-179">Dit kunnen verschillende acties uitvoeren op de rekenemulator en de cloud kunt u doen met het maken van een omgevingsvariabele in de [ServiceDefinition.csdef] bestand.</span><span class="sxs-lookup"><span data-stu-id="a92b1-179">This ability to perform different actions on the compute emulator and the cloud can be accomplished by creating an environment variable in the [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="a92b1-180">U test die omgevingsvariabele voor een waarde in uw taak starten.</span><span class="sxs-lookup"><span data-stu-id="a92b1-180">You then test that environment variable for a value in your startup task.</span></span>

<span data-ttu-id="a92b1-181">Voor het maken van de omgevingsvariabele toevoegen de [variabele]/[RoleInstanceValue] element en het maken van een XPath-waarde van `/RoleEnvironment/Deployment/@emulated`.</span><span class="sxs-lookup"><span data-stu-id="a92b1-181">To create the environment variable, add the [Variable]/[RoleInstanceValue] element and create an XPath value of `/RoleEnvironment/Deployment/@emulated`.</span></span> <span data-ttu-id="a92b1-182">De waarde van de **% ComputeEmulatorRunning %** omgevingsvariabele is `true` wanneer u gebruikmaakt van de rekenemulator en `false` wanneer u gebruikmaakt van de cloud.</span><span class="sxs-lookup"><span data-stu-id="a92b1-182">The value of the **%ComputeEmulatorRunning%** environment variable is `true` when running on the compute emulator, and `false` when running on the cloud.</span></span>

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

<span data-ttu-id="a92b1-183">Controleer de taak kan nu de **% ComputeEmulatorRunning %** omgevingsvariabele andere acties uit te voeren op basis van de vraag of de rol wordt uitgevoerd in de cloud of de emulator.</span><span class="sxs-lookup"><span data-stu-id="a92b1-183">The task can now check the **%ComputeEmulatorRunning%** environment variable to perform different actions based on whether the role is running in the cloud or the emulator.</span></span> <span data-ttu-id="a92b1-184">Hier volgt een cmd-shell-script waarmee wordt gecontroleerd of deze omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="a92b1-184">Here is a .cmd shell script that checks for that environment variable.</span></span>

```cmd
REM   Check if this task is running on the compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on the compute emulator. Perform tasks that must be run only in the compute emulator.
) ELSE (
    REM   This task is running on the cloud. Perform tasks that must be run only in the cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a><span data-ttu-id="a92b1-185">Detecteren of de taak al is uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="a92b1-185">Detect that your task has already run</span></span>
<span data-ttu-id="a92b1-186">De rol kan niet opnieuw starten van de taken opnieuw uit te voeren waardoor start recyclen.</span><span class="sxs-lookup"><span data-stu-id="a92b1-186">The role may recycle without a reboot causing your startup tasks to run again.</span></span> <span data-ttu-id="a92b1-187">Er is geen vlag die aangeeft dat een taak al is uitgevoerd op de host VM.</span><span class="sxs-lookup"><span data-stu-id="a92b1-187">There is no flag to indicate that a task has already run on the hosting VM.</span></span> <span data-ttu-id="a92b1-188">Mogelijk hebt u een aantal taken waarbij het maakt niet uit dat ze meerdere keren worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a92b1-188">You may have some tasks where it doesn't matter that they run multiple times.</span></span> <span data-ttu-id="a92b1-189">U kunt echter uitvoeren in een situatie waarin u wilt voorkomen dat een taak meerdere keren wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a92b1-189">However, you may run into a situation where you need to prevent a task from running more than once.</span></span>

<span data-ttu-id="a92b1-190">De eenvoudigste manier om te detecteren of er al een taak is uitgevoerd, is voor het maken van een bestand in de **% TEMP %** map wanneer de taak geslaagd is en zoeken naar deze aan het begin van de taak.</span><span class="sxs-lookup"><span data-stu-id="a92b1-190">The simplest way to detect that a task has already run is to create a file in the **%TEMP%** folder when the task is successful and look for it at the start of the task.</span></span> <span data-ttu-id="a92b1-191">Hier volgt een voorbeeld cmd shell-script dat die voor u uitvoert.</span><span class="sxs-lookup"><span data-stu-id="a92b1-191">Here is a sample cmd shell script that does that for you.</span></span>

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
  REM   The application installed without error. Create a file to indicate that the task
  REM   does not need to be run again.

  ECHO This line will create a file to indicate that Application 1 installed correctly. > "%RoleRoot%\Task1_Success.txt"

) ELSE (
  REM   An error occurred. Log the error and exit with the error code.

  DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
  TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
  ECHO  An error occurred running task 1. Errorlevel = %ERRORLEVEL%. >> "%TEMP%\StartupLog.txt" 2>&1

  EXIT %ERRORLEVEL%
)

:Finish

REM   Exit normally.
EXIT /B 0
```

## <a name="task-best-practices"></a><span data-ttu-id="a92b1-192">Aanbevolen procedures van taak</span><span class="sxs-lookup"><span data-stu-id="a92b1-192">Task best practices</span></span>
<span data-ttu-id="a92b1-193">Hier volgen enkele aanbevolen procedures die u volgen moet wanneer de taak voor uw web- of worker-rol configureert.</span><span class="sxs-lookup"><span data-stu-id="a92b1-193">Here are some best practices you should follow when configuring task for your web or worker role.</span></span>

### <a name="always-log-startup-activities"></a><span data-ttu-id="a92b1-194">Meld u altijd starten van activiteiten</span><span class="sxs-lookup"><span data-stu-id="a92b1-194">Always log startup activities</span></span>
<span data-ttu-id="a92b1-195">Visual Studio biedt geen een foutopsporingsprogramma stap batchbestanden, dus is het raadzaam om zo veel mogelijk gegevens ophalen over de werking van de batch-bestanden mogelijk wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a92b1-195">Visual Studio does not provide a debugger to step through batch files, so it's good to get as much data on the operation of batch files as possible.</span></span> <span data-ttu-id="a92b1-196">Logboekregistratie van de uitvoer van de batch-bestanden, beide **stdout** en **stderr**, krijgt u belangrijke informatie bij het opsporen en oplossen van batch-bestanden.</span><span class="sxs-lookup"><span data-stu-id="a92b1-196">Logging the output of batch files, both **stdout** and **stderr**, can give you important information when trying to debug and fix batch files.</span></span> <span data-ttu-id="a92b1-197">Aan te melden beide **stdout** en **stderr** naar de StartupLog.txt bestand in de map waarnaar wordt verwezen door de **% TEMP %** omgevingsvariabele, Voeg tekst toe `>>  "%TEMP%\\StartupLog.txt" 2>&1` aan het einde van specifieke regels die u wilt registreren.</span><span class="sxs-lookup"><span data-stu-id="a92b1-197">To log both **stdout** and **stderr** to the StartupLog.txt file in the directory pointed to by the **%TEMP%** environment variable, add the text `>>  "%TEMP%\\StartupLog.txt" 2>&1` to the end of specific lines you want to log.</span></span> <span data-ttu-id="a92b1-198">Bijvoorbeeld, om het uitvoeren van setup.exe in de **% PathToApp1Install** directory:</span><span class="sxs-lookup"><span data-stu-id="a92b1-198">For example, to execute setup.exe in the **%PathToApp1Install%** directory:</span></span>

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

<span data-ttu-id="a92b1-199">Als u wilt uw XML-vereenvoudigen, kunt u een wrapper *cmd* bestand die alle uw opstarten aanroept taken samen met de logboekregistratie en zorgt ervoor dat elke onderliggende-taak deelt de dezelfde omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="a92b1-199">To simplify your xml, you can create a wrapper *cmd* file that calls all of your startup tasks along with logging and ensures each child-task shares the same environment variables.</span></span>

<span data-ttu-id="a92b1-200">Wellicht vindt u het vervelend dat moet worden gebruikt `>> "%TEMP%\StartupLog.txt" 2>&1` aan het einde van elke taak starten.</span><span class="sxs-lookup"><span data-stu-id="a92b1-200">You may find it annoying though to use `>> "%TEMP%\StartupLog.txt" 2>&1` on the end of each startup task.</span></span> <span data-ttu-id="a92b1-201">U kunt de taak logboekregistratie afdwingen door het maken van een wrapper die verantwoordelijk is voor logboekregistratie voor u.</span><span class="sxs-lookup"><span data-stu-id="a92b1-201">You can enforce task logging by creating a wrapper that handles logging for you.</span></span> <span data-ttu-id="a92b1-202">Deze wrapper roept het echte batchbestand dat u wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a92b1-202">This wrapper calls the real batch file you want to run.</span></span> <span data-ttu-id="a92b1-203">Elke uitvoer van het doelbestand voor de batch wordt omgeleid naar de *Startuplog.txt* bestand.</span><span class="sxs-lookup"><span data-stu-id="a92b1-203">Any output from the target batch file will be redirected to the *Startuplog.txt* file.</span></span>

<span data-ttu-id="a92b1-204">Het volgende voorbeeld laat zien hoe alle uitvoer omleiden van een starten van de batch-bestand.</span><span class="sxs-lookup"><span data-stu-id="a92b1-204">The following example shows how to redirect all output from a startup batch file.</span></span> <span data-ttu-id="a92b1-205">In dit voorbeeld wordt het ServerDefinition.csdef maakt een taak gestart die aanroept *logwrap.cmd*.</span><span class="sxs-lookup"><span data-stu-id="a92b1-205">In this example, the ServerDefinition.csdef file creates a startup task that calls *logwrap.cmd*.</span></span> <span data-ttu-id="a92b1-206">*logwrap.cmd* aanroepen *Startup2.cmd*, alle uitvoer naar omleiden **% TEMP %\\StartupLog.txt**.</span><span class="sxs-lookup"><span data-stu-id="a92b1-206">*logwrap.cmd* calls *Startup2.cmd*, redirecting all output to **%TEMP%\\StartupLog.txt**.</span></span>

<span data-ttu-id="a92b1-207">ServiceDefinition.cmd:</span><span class="sxs-lookup"><span data-stu-id="a92b1-207">ServiceDefinition.cmd:</span></span>

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

<span data-ttu-id="a92b1-208">**logwrap.cmd:**</span><span class="sxs-lookup"><span data-stu-id="a92b1-208">**logwrap.cmd:**</span></span>

```cmd
@ECHO OFF

REM   logwrap.cmd calls passed in batch file, redirecting all output to the StartupLog.txt log file.

ECHO [%date% %time%] == START logwrap.cmd ============================================== >> "%TEMP%\StartupLog.txt" 2>&1
ECHO [%date% %time%] Running %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Call the child command batch file, redirecting all output to the StartupLog.txt log file.
START /B /WAIT %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Log the completion of child command.
ECHO [%date% %time%] Done >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (

   REM   No errors occurred. Exit logwrap.cmd normally.
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B 0

) ELSE (

   REM   Log the error.
   ECHO [%date% %time%] An error occurred. The ERRORLEVEL = %ERRORLEVEL%.  >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B %ERRORLEVEL%

)
```

<span data-ttu-id="a92b1-209">**Startup2.cmd:**</span><span class="sxs-lookup"><span data-stu-id="a92b1-209">**Startup2.cmd:**</span></span>

```cmd
@ECHO OFF

REM   This is the batch file where the startup steps should be performed. Because of the
REM   way Startup2.cmd was called, all commands and their outputs will be stored in the
REM   StartupLog.txt file in the directory pointed to by the TEMP environment variable.

REM   If an error occurs, the following command will pass the ERRORLEVEL back to the
REM   calling batch file.

ECHO [%date% %time%] Some log information about this task
ECHO [%date% %time%] Some more log information about this task

EXIT %ERRORLEVEL%
```

<span data-ttu-id="a92b1-210">Voorbeeld van uitvoer in de **StartupLog.txt** bestand:</span><span class="sxs-lookup"><span data-stu-id="a92b1-210">Sample output in the **StartupLog.txt** file:</span></span>

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> <span data-ttu-id="a92b1-211">De **StartupLog.txt** bestand bevindt zich in de *C:\Resources\temp\\{rol-id} \RoleTemp* map.</span><span class="sxs-lookup"><span data-stu-id="a92b1-211">The **StartupLog.txt** file is located in the *C:\Resources\temp\\{role identifier}\RoleTemp* folder.</span></span>
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a><span data-ttu-id="a92b1-212">Set executionContext op de juiste wijze voor opstarttaken</span><span class="sxs-lookup"><span data-stu-id="a92b1-212">Set executionContext appropriately for startup tasks</span></span>
<span data-ttu-id="a92b1-213">Bevoegdheden voor het starten van de taak op de juiste wijze ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a92b1-213">Set privileges appropriately for the startup task.</span></span> <span data-ttu-id="a92b1-214">Soms moeten taken starten met verhoogde bevoegdheden uitvoeren, ondanks dat de rol wordt uitgevoerd met normale bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="a92b1-214">Sometimes startup tasks must run with elevated privileges even though the role runs with normal privileges.</span></span>

<span data-ttu-id="a92b1-215">De [executionContext][taak] kenmerk Hiermee stelt u de bevoegdheden van de taak starten.</span><span class="sxs-lookup"><span data-stu-id="a92b1-215">The [executionContext][Task] attribute sets the privilege level of the startup task.</span></span> <span data-ttu-id="a92b1-216">Met behulp van `executionContext="limited"` betekent dat het starten van de taak heeft dezelfde toegangsrechten als de rol.</span><span class="sxs-lookup"><span data-stu-id="a92b1-216">Using `executionContext="limited"` means the startup task has the same privilege level as the role.</span></span> <span data-ttu-id="a92b1-217">Met behulp van `executionContext="elevated"` betekent dat de taak starten van de administrator-bevoegdheden heeft, waardoor de opstarttaak beheerderstaken uitvoeren zonder dat de administrator-bevoegdheden voor uw rol.</span><span class="sxs-lookup"><span data-stu-id="a92b1-217">Using `executionContext="elevated"` means the startup task has administrator privileges, which allows the startup task to perform administrator tasks without giving administrator privileges to your role.</span></span>

<span data-ttu-id="a92b1-218">Een voorbeeld van een taak gestart die zijn verhoogde bevoegdheden vereist is een taak gestart die gebruikmaakt van **AppCmd.exe** om IIS te configureren.</span><span class="sxs-lookup"><span data-stu-id="a92b1-218">An example of a startup task that requires elevated privileges is a startup task that uses **AppCmd.exe** to configure IIS.</span></span> <span data-ttu-id="a92b1-219">**AppCmd.exe** vereist `executionContext="elevated"`.</span><span class="sxs-lookup"><span data-stu-id="a92b1-219">**AppCmd.exe** requires `executionContext="elevated"`.</span></span>

### <a name="use-the-appropriate-tasktype"></a><span data-ttu-id="a92b1-220">Gebruik de juiste taskType</span><span class="sxs-lookup"><span data-stu-id="a92b1-220">Use the appropriate taskType</span></span>
<span data-ttu-id="a92b1-221">De [taskType][taak] kenmerk bepaalt de manier waarop het starten van de taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a92b1-221">The [taskType][Task] attribute determines the way the startup task is executed.</span></span> <span data-ttu-id="a92b1-222">Er zijn drie waarden: **eenvoudige**, **achtergrond**, en **voorgrond**.</span><span class="sxs-lookup"><span data-stu-id="a92b1-222">There are three values: **simple**, **background**, and **foreground**.</span></span> <span data-ttu-id="a92b1-223">De taken en achtergrond asynchroon worden gestart en vervolgens de eenvoudige taken synchroon uitgevoerd één tegelijk.</span><span class="sxs-lookup"><span data-stu-id="a92b1-223">The background and foreground tasks are started asynchronously, and then the simple tasks are executed synchronously one at a time.</span></span>

<span data-ttu-id="a92b1-224">Met **eenvoudige** starten van de taken, kunt u de volgorde waarin de taken worden uitgevoerd door de volgorde waarin de taken worden weergegeven in het bestand ServiceDefinition.csdef instellen.</span><span class="sxs-lookup"><span data-stu-id="a92b1-224">With **simple** startup tasks, you can set the order in which the tasks run by the order in which the tasks are listed in the ServiceDefinition.csdef file.</span></span> <span data-ttu-id="a92b1-225">Als een **eenvoudige** taak eindigt met een afsluitcode dan nul en vervolgens de procedure opstarten stopt en de rol wordt niet gestart.</span><span class="sxs-lookup"><span data-stu-id="a92b1-225">If a **simple** task ends with a non-zero exit code, then the startup procedure stops and the role does not start.</span></span>

<span data-ttu-id="a92b1-226">Het verschil tussen **achtergrond** starten van de taken en **voorgrond** starten van de taken is dat **voorgrond** taken houden de functie die wordt uitgevoerd totdat de  **voorgrond** taak is geëindigd.</span><span class="sxs-lookup"><span data-stu-id="a92b1-226">The difference between **background** startup tasks and **foreground** startup tasks is that **foreground** tasks keep the role running until the **foreground** task ends.</span></span> <span data-ttu-id="a92b1-227">Dit betekent ook dat wanneer de **voorgrond** taak vastloopt of crasht, de functie niet gerecycled totdat de **voorgrond** taak wordt geforceerd gesloten.</span><span class="sxs-lookup"><span data-stu-id="a92b1-227">This also means that if the **foreground** task hangs or crashes, the role will not recycle until the **foreground** task is forced closed.</span></span> <span data-ttu-id="a92b1-228">Om deze reden **achtergrond** taken worden aanbevolen voor het starten van de asynchrone taken alleen u deze functie van moet de **voorgrond** taak.</span><span class="sxs-lookup"><span data-stu-id="a92b1-228">For this reason, **background** tasks are recommended for asynchronous startup tasks unless you need that feature of the **foreground** task.</span></span>

### <a name="end-batch-files-with-exit-b-0"></a><span data-ttu-id="a92b1-229">Einde batch-bestanden met de AFSLUITCODE /B 0</span><span class="sxs-lookup"><span data-stu-id="a92b1-229">End batch files with EXIT /B 0</span></span>
<span data-ttu-id="a92b1-230">De rol wordt alleen gestart als de **errorlevel** van elk van uw eenvoudige starten van de taak is aan nul.</span><span class="sxs-lookup"><span data-stu-id="a92b1-230">The role will only start if the **errorlevel** from each of your simple startup task is zero.</span></span> <span data-ttu-id="a92b1-231">Niet alle programma's instellen de **errorlevel** (afsluitcode) correct, dus het batchbestand moet eindigen met een `EXIT /B 0` als alles goed is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a92b1-231">Not all programs set the **errorlevel** (exit code) correctly, so the batch file should end with an `EXIT /B 0` if everything ran correctly.</span></span>

<span data-ttu-id="a92b1-232">Een ontbrekende `EXIT /B 0` aan het einde van een starten van de batch-bestand is een veelvoorkomende oorzaak van de functies die niet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="a92b1-232">A missing `EXIT /B 0` at the end of a startup batch file is a common cause of roles that do not start.</span></span>

> [!NOTE]
> <span data-ttu-id="a92b1-233">Ik opgevallen dat geneste batch bestanden soms vastlopen wanneer u de `/B` parameter.</span><span class="sxs-lookup"><span data-stu-id="a92b1-233">I've noticed that nested batch files sometimes hang when using the `/B` parameter.</span></span> <span data-ttu-id="a92b1-234">U kunt om ervoor te zorgen dat dit probleem blijft hangen niet gebeurt als een ander batchbestand het huidige batchbestand roept, zoals als u de [logboek wrapper](#always-log-startup-activities).</span><span class="sxs-lookup"><span data-stu-id="a92b1-234">You may want to make sure that this hang problem does not happen if another batch file calls your current batch file, like if you use the [log wrapper](#always-log-startup-activities).</span></span> <span data-ttu-id="a92b1-235">U kunt weglaten de `/B` parameter in dit geval.</span><span class="sxs-lookup"><span data-stu-id="a92b1-235">You can omit the `/B` parameter in this case.</span></span>
> 
> 

### <a name="expect-startup-tasks-to-run-more-than-once"></a><span data-ttu-id="a92b1-236">Starten van de taken uitvoeren meer dan één keer verwacht</span><span class="sxs-lookup"><span data-stu-id="a92b1-236">Expect startup tasks to run more than once</span></span>
<span data-ttu-id="a92b1-237">Niet alle rol recyclet zijn opnieuw worden opgestart, maar alle rol recyclet omvatten alle starten van de taken uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a92b1-237">Not all role recycles include a reboot, but all role recycles include running all startup tasks.</span></span> <span data-ttu-id="a92b1-238">Dit betekent dat starten van de taken kunnen moet worden meerdere keren opnieuw wordt gestart zonder problemen uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a92b1-238">This means that startup tasks must be able to run multiple times between reboots without any problems.</span></span> <span data-ttu-id="a92b1-239">Dit wordt besproken de [voorgaande sectie](#detect-that-your-task-has-already-run).</span><span class="sxs-lookup"><span data-stu-id="a92b1-239">This is discussed in the [preceding section](#detect-that-your-task-has-already-run).</span></span>

### <a name="use-local-storage-to-store-files-that-must-be-accessed-in-the-role"></a><span data-ttu-id="a92b1-240">Lokale opslag gebruiken voor het opslaan van bestanden die moeten worden geopend in de rol</span><span class="sxs-lookup"><span data-stu-id="a92b1-240">Use local storage to store files that must be accessed in the role</span></span>
<span data-ttu-id="a92b1-241">Als u wilt kopiëren of een bestand maken tijdens het starten van de taak die vervolgens toegankelijk is voor uw rol, moet dit bestand in de lokale opslag worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="a92b1-241">If you want to copy or create a file during your startup task that is then accessible to your role, then that file must be placed in local storage.</span></span> <span data-ttu-id="a92b1-242">Zie de [voorgaande sectie](#create-files-in-local-storage-from-a-startup-task).</span><span class="sxs-lookup"><span data-stu-id="a92b1-242">See the [preceding section](#create-files-in-local-storage-from-a-startup-task).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a92b1-243">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a92b1-243">Next steps</span></span>
<span data-ttu-id="a92b1-244">Bekijk de cloud [service model- en -pakket](cloud-services-model-and-package.md)</span><span class="sxs-lookup"><span data-stu-id="a92b1-244">Review the cloud [service model and package](cloud-services-model-and-package.md)</span></span>

<span data-ttu-id="a92b1-245">Meer informatie over het [taken](cloud-services-startup-tasks.md) werken.</span><span class="sxs-lookup"><span data-stu-id="a92b1-245">Learn more about how [Tasks](cloud-services-startup-tasks.md) work.</span></span>

<span data-ttu-id="a92b1-246">[Maken en implementeren van](cloud-services-how-to-create-deploy-portal.md) uw cloud-pakket.</span><span class="sxs-lookup"><span data-stu-id="a92b1-246">[Create and deploy](cloud-services-how-to-create-deploy-portal.md) your cloud service package.</span></span>

<span data-ttu-id="a92b1-247">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span><span class="sxs-lookup"><span data-stu-id="a92b1-247">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span></span>
<span data-ttu-id="a92b1-248">[taak]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span><span class="sxs-lookup"><span data-stu-id="a92b1-248">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span></span>
[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
<span data-ttu-id="a92b1-249">[omgeving]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span><span class="sxs-lookup"><span data-stu-id="a92b1-249">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span></span>
<span data-ttu-id="a92b1-250">[variabele]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span><span class="sxs-lookup"><span data-stu-id="a92b1-250">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span></span>
<span data-ttu-id="a92b1-251">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="a92b1-251">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
<span data-ttu-id="a92b1-252">[Eindpunten]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints</span><span class="sxs-lookup"><span data-stu-id="a92b1-252">[Endpoints]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints</span></span>
<span data-ttu-id="a92b1-253">[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage</span><span class="sxs-lookup"><span data-stu-id="a92b1-253">[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage</span></span>
<span data-ttu-id="a92b1-254">[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources</span><span class="sxs-lookup"><span data-stu-id="a92b1-254">[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources</span></span>
<span data-ttu-id="a92b1-255">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="a92b1-255">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
