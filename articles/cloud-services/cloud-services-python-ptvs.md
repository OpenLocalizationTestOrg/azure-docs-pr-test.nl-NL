---
title: aaaGet gestart met Python en Azure Cloud Services | Microsoft Docs
description: Overzicht van het gebruik van Python-Tools voor Visual Studio toocreate Azure cloudservices, met inbegrip van webrollen en werkrollen.
services: cloud-services
documentationcenter: python
author: thraka
manager: timlt
editor: 
ms.assetid: 5489405d-6fa9-4b11-a161-609103cbdc18
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: f5fd85e754839f146abe912351c59dc4a148c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a><span data-ttu-id="e0709-103">Python-web- en -werkrollen met Python-tools voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e0709-103">Python web and worker roles with Python Tools for Visual Studio</span></span>

<span data-ttu-id="e0709-104">Dit artikel biedt een overzicht van het gebruik van Python-web- en -werkrollen met [Python Tools for Visual Studio][Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="e0709-104">This article provides an overview of using Python web and worker roles using [Python Tools for Visual Studio][Python Tools for Visual Studio].</span></span> <span data-ttu-id="e0709-105">Meer informatie over hoe toouse Visual Studio toocreate en implementeren van een eenvoudige Cloud-Service die gebruikmaakt van Python.</span><span class="sxs-lookup"><span data-stu-id="e0709-105">Learn how toouse Visual Studio toocreate and deploy a basic Cloud Service that uses Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0709-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e0709-106">Prerequisites</span></span>
* [<span data-ttu-id="e0709-107">Visual Studio 2013, 2015 of 2017</span><span class="sxs-lookup"><span data-stu-id="e0709-107">Visual Studio 2013, 2015, or 2017</span></span>](https://www.visualstudio.com/)
* <span data-ttu-id="e0709-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span><span class="sxs-lookup"><span data-stu-id="e0709-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span></span>
* <span data-ttu-id="e0709-109">[Azure SDK-hulpprogramma’s voor VS 2013][Azure SDK Tools for VS 2013] of</span><span class="sxs-lookup"><span data-stu-id="e0709-109">[Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] or</span></span>  
<span data-ttu-id="e0709-110">[Azure SDK-hulpprogramma’s voor VS 2015][Azure SDK Tools for VS 2015] of</span><span class="sxs-lookup"><span data-stu-id="e0709-110">[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] or</span></span>  
<span data-ttu-id="e0709-111">[Azure SDK-tools voor VS 2017][Azure SDK Tools for VS 2017]</span><span class="sxs-lookup"><span data-stu-id="e0709-111">[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]</span></span>
* <span data-ttu-id="e0709-112">[Python 2.7 32-bits][Python 2.7 32-bit] of [Python 3.5 32-bits][Python 3.5 32-bit]</span><span class="sxs-lookup"><span data-stu-id="e0709-112">[Python 2.7 32-bit][Python 2.7 32-bit] or [Python 3.5 32-bit][Python 3.5 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a><span data-ttu-id="e0709-113">Wat zijn Python-web- en -werkrollen?</span><span class="sxs-lookup"><span data-stu-id="e0709-113">What are Python web and worker roles?</span></span>
<span data-ttu-id="e0709-114">Azure biedt drie rekenmodellen voor het uitvoeren van toepassingen: [web-appsfunctie in Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms] en [Azure Cloud Services][execution model-cloud services].</span><span class="sxs-lookup"><span data-stu-id="e0709-114">Azure provides three compute models for running applications: [Web Apps feature in Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms], and [Azure Cloud Services][execution model-cloud services].</span></span> <span data-ttu-id="e0709-115">Alle drie modellen ondersteunen Python.</span><span class="sxs-lookup"><span data-stu-id="e0709-115">All three models support Python.</span></span> <span data-ttu-id="e0709-116">Cloud Services, die web- en werkrollen bevatten, bieden *Platform as a Service (PaaS)*.</span><span class="sxs-lookup"><span data-stu-id="e0709-116">Cloud Services, which include web and worker roles, provide *Platform as a Service (PaaS)*.</span></span> <span data-ttu-id="e0709-117">Binnen een cloudservice biedt een Webrol een speciale Internet Information Services (IIS) web server toohost front-end-web-toepassingen, terwijl een werkrol kan asynchrone, langlopende of permanente onafhankelijk van de gebruikersinteractie of invoer taken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e0709-117">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server toohost front end web applications, while a worker role can run asynchronous, long-running, or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="e0709-118">Zie [Wat is een cloudservice?] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e0709-118">For more information, see [What is a Cloud Service?].</span></span>

> [!NOTE]
> <span data-ttu-id="e0709-119">*Zoek toobuild een ongecompliceerde website?*</span><span class="sxs-lookup"><span data-stu-id="e0709-119">*Looking toobuild a simple website?*</span></span>
> <span data-ttu-id="e0709-120">Als uw scenario slechts een ongecompliceerde website-front-end omvat, kunt u overwegen Hallo eenvoudige functie Web Apps in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="e0709-120">If your scenario involves just a simple website front end, consider using hello lightweight Web Apps feature in Azure App Service.</span></span> <span data-ttu-id="e0709-121">Als uw website groeit en uw vereisten veranderen, kunt u gemakkelijk tooa Cloudservice upgraden.</span><span class="sxs-lookup"><span data-stu-id="e0709-121">You can easily upgrade tooa Cloud Service as your website grows and your requirements change.</span></span> <span data-ttu-id="e0709-122">Zie Hallo <a href="/develop/python/">Python Developer Center</a> voor artikelen over ontwikkeling met de functie van de Hallo Web Apps in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="e0709-122">See hello <a href="/develop/python/">Python Developer Center</a> for articles that cover development of hello Web Apps feature in Azure App Service.</span></span>
> <br />
> 
> 

## <a name="project-creation"></a><span data-ttu-id="e0709-123">Een project maken</span><span class="sxs-lookup"><span data-stu-id="e0709-123">Project creation</span></span>
<span data-ttu-id="e0709-124">In Visual Studio, kunt u **Azure Cloud Service** in Hallo **nieuw Project** dialoogvenster onder **Python**.</span><span class="sxs-lookup"><span data-stu-id="e0709-124">In Visual Studio, you can select **Azure Cloud Service** in hello **New Project** dialog box, under **Python**.</span></span>

![Het dialoogvenster Nieuw project](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

<span data-ttu-id="e0709-126">U kunt nieuwe web- en werkrollen maken in hello Azure Cloud Service-wizard.</span><span class="sxs-lookup"><span data-stu-id="e0709-126">In hello Azure Cloud Service wizard, you can create new web and worker roles.</span></span>

![Het dialoogvenster Azure Cloud Service](./media/cloud-services-python-ptvs/new-service-wizard.png)

<span data-ttu-id="e0709-128">Hallo werkrolsjabloon wordt geleverd met standaardtekst code tooconnect tooan Azure storage-account of Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="e0709-128">hello worker role template comes with boilerplate code tooconnect tooan Azure storage account or Azure Service Bus.</span></span>

![Cloudserviceoplossing](./media/cloud-services-python-ptvs/worker.png)

<span data-ttu-id="e0709-130">U kunt de web- of worker rollen tooan bestaande cloudservice op elk gewenst moment toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e0709-130">You can add web or worker roles tooan existing cloud service at any time.</span></span>  <span data-ttu-id="e0709-131">U kunt de bestaande projecten tooadd kiezen in uw oplossing of nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="e0709-131">You can choose tooadd existing projects in your solution, or create new ones.</span></span>

![De opdracht Rol toevoegen](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

<span data-ttu-id="e0709-133">Uw cloudservice kan rollen bevatten die zijn geïmplementeerd in verschillende talen.</span><span class="sxs-lookup"><span data-stu-id="e0709-133">Your cloud service can contain roles implemented in different languages.</span></span>  <span data-ttu-id="e0709-134">U kunt bijvoorbeeld een Python-webrol hebben die is geïmplementeerd met Django, met Python of met C#-werkrollen.</span><span class="sxs-lookup"><span data-stu-id="e0709-134">For example, you can have a Python web role implemented using Django, with Python, or with C# worker roles.</span></span>  <span data-ttu-id="e0709-135">U kunt eenvoudig communiceren tussen uw rollen met behulp van de Service Bus-wachtrijen of opslagwachtrijen.</span><span class="sxs-lookup"><span data-stu-id="e0709-135">You can easily communicate between your roles using Service Bus queues or storage queues.</span></span>

## <a name="install-python-on-hello-cloud-service"></a><span data-ttu-id="e0709-136">Python installeren op Hallo-cloudservice</span><span class="sxs-lookup"><span data-stu-id="e0709-136">Install Python on hello cloud service</span></span>
> [!WARNING]
> <span data-ttu-id="e0709-137">Hallo setup-scripts die zijn geïnstalleerd met Visual Studio (op Hallo tijd die in dit artikel voor het laatst is bijgewerkt) werken niet.</span><span class="sxs-lookup"><span data-stu-id="e0709-137">hello setup scripts that are installed with Visual Studio (at hello time this article was last updated) do not work.</span></span> <span data-ttu-id="e0709-138">Deze sectie beschrijft een tijdelijke oplossing.</span><span class="sxs-lookup"><span data-stu-id="e0709-138">This section describes a workaround.</span></span>
> 
> 

<span data-ttu-id="e0709-139">Hallo belangrijkste probleem met de installatiescripts Hallo is dat ze niet python installeert.</span><span class="sxs-lookup"><span data-stu-id="e0709-139">hello main problem with hello setup scripts is that they do not install python.</span></span> <span data-ttu-id="e0709-140">Eerste stap definieert twee [starten van de taken](cloud-services-startup-tasks.md) in Hallo [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) bestand.</span><span class="sxs-lookup"><span data-stu-id="e0709-140">First, define two [startup tasks](cloud-services-startup-tasks.md) in hello [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) file.</span></span> <span data-ttu-id="e0709-141">de eerste taak hello (**PrepPython.ps1**) downloadt en installeert Hallo Python-runtime.</span><span class="sxs-lookup"><span data-stu-id="e0709-141">hello first task (**PrepPython.ps1**) downloads and installs hello Python runtime.</span></span> <span data-ttu-id="e0709-142">de tweede taak hello (**PipInstaller.ps1**) pip tooinstall eventuele afhankelijkheden die u hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e0709-142">hello second task (**PipInstaller.ps1**) runs pip tooinstall any dependencies you may have.</span></span>

<span data-ttu-id="e0709-143">Hallo scripts te volgen zijn geschreven als doel Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="e0709-143">hello following scripts were written targeting Python 3.5.</span></span> <span data-ttu-id="e0709-144">Als u wilt dat toouse Hallo versie 2.x van python, set Hallo **PYTHON2** variabele bestand te**op** voor Hallo twee starten van de taken en runtime-taak Hallo: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span><span class="sxs-lookup"><span data-stu-id="e0709-144">If you want toouse hello version 2.x of python, set hello **PYTHON2** variable file too**on** for hello two startup tasks and hello runtime task: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span></span>

```xml
<Startup>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>
  </Task>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>

  </Task>

</Startup>
```

<span data-ttu-id="e0709-145">Hallo **PYTHON2** en **PYPATH** variabelen toohello worker starten van de taak moeten worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e0709-145">hello **PYTHON2** and **PYPATH** variables must be added toohello worker startup task.</span></span> <span data-ttu-id="e0709-146">Hallo **PYPATH** variabele wordt alleen gebruikt als hello **PYTHON2** variabele is ingesteld, te**op**.</span><span class="sxs-lookup"><span data-stu-id="e0709-146">hello **PYPATH** variable is only used if hello **PYTHON2** variable is set too**on**.</span></span>

```xml
<Runtime>
  <Environment>
    <Variable name="EMULATED">
      <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
    </Variable>
    <Variable name="PYTHON2" value="off" />
    <Variable name="PYPATH" value="%SystemDrive%\Python27" />
  </Environment>
  <EntryPoint>
    <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
  </EntryPoint>
</Runtime>
```

#### <a name="sample-servicedefinitioncsdef"></a><span data-ttu-id="e0709-147">Voorbeeld van ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="e0709-147">Sample ServiceDefinition.csdef</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="AzureCloudServicePython" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
      <Setting name="Python2" />
    </ConfigurationSettings>
    <Startup>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="EMULATED">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
        </Variable>
        <Variable name="PYTHON2" value="off" />
        <Variable name="PYPATH" value="%SystemDrive%\Python27" />
      </Environment>
      <EntryPoint>
        <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
      </EntryPoint>
    </Runtime>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
  </WorkerRole>
</ServiceDefinition>
```



<span data-ttu-id="e0709-148">Maak vervolgens Hallo **PrepPython.ps1** en **PipInstaller.ps1** bestanden in Hallo **. / bin** map van uw rol.</span><span class="sxs-lookup"><span data-stu-id="e0709-148">Next, create hello **PrepPython.ps1** and **PipInstaller.ps1** files in hello **./bin** folder of your role.</span></span>

#### <a name="preppythonps1"></a><span data-ttu-id="e0709-149">PrepPython.ps1</span><span class="sxs-lookup"><span data-stu-id="e0709-149">PrepPython.ps1</span></span>
<span data-ttu-id="e0709-150">Dit script installeert Python.</span><span class="sxs-lookup"><span data-stu-id="e0709-150">This script installs python.</span></span> <span data-ttu-id="e0709-151">Als hello **PYTHON2** omgevingsvariabele is te ingesteld**op**, en vervolgens Python 2.7 is geïnstalleerd, anders Python 3.5 is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e0709-151">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is installed, otherwise Python 3.5 is installed.</span></span>

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if python is installed...$nl"
    if ($is_python2) {
        & "${env:SystemDrive}\Python27\python.exe"  -V | Out-Null
    }
    else {
        py -V | Out-Null
    }

    if (-not $?) {

        $url = "https://www.python.org/ftp/python/3.5.2/python-3.5.2-amd64.exe"
        $outFile = "${env:TEMP}\python-3.5.2-amd64.exe"

        if ($is_python2) {
            $url = "https://www.python.org/ftp/python/2.7.12/python-2.7.12.amd64.msi"
            $outFile = "${env:TEMP}\python-2.7.12.amd64.msi"
        }

        Write-Output "Not found, downloading $url too$outFile$nl"
        Invoke-WebRequest $url -OutFile $outFile
        Write-Output "Installing$nl"

        if ($is_python2) {
            Start-Process msiexec.exe -ArgumentList "/q", "/i", "$outFile", "ALLUSERS=1" -Wait
        }
        else {
            Start-Process "$outFile" -ArgumentList "/quiet", "InstallAllUsers=1" -Wait
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Already installed"
    }
}
```

#### <a name="pipinstallerps1"></a><span data-ttu-id="e0709-152">PipInstaller.ps1</span><span class="sxs-lookup"><span data-stu-id="e0709-152">PipInstaller.ps1</span></span>
<span data-ttu-id="e0709-153">Dit script pip-aanroepen en installeert u alle afhankelijkheden Hallo in Hallo **requirements.txt** bestand.</span><span class="sxs-lookup"><span data-stu-id="e0709-153">This script calls up pip and installs all of hello dependencies in hello **requirements.txt** file.</span></span> <span data-ttu-id="e0709-154">Als hello **PYTHON2** omgevingsvariabele is te ingesteld**op**, en vervolgens Python 2.7 wordt gebruikt, anders Python 3.5 wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e0709-154">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if requirements.txt exists$nl"
    if (Test-Path ..\requirements.txt) {
        Write-Output "Found. Processing pip$nl"

        if ($is_python2) {
            & "${env:SystemDrive}\Python27\python.exe" -m pip install -r ..\requirements.txt
        }
        else {
            py -m pip install -r ..\requirements.txt
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Not found$nl"
    }
}
```

#### <a name="modify-launchworkerps1"></a><span data-ttu-id="e0709-155">LaunchWorker.ps1 wijzigen</span><span class="sxs-lookup"><span data-stu-id="e0709-155">Modify LaunchWorker.ps1</span></span>
> [!NOTE]
> <span data-ttu-id="e0709-156">In geval van Hallo een **werkrol** project **LauncherWorker.ps1** bestand is vereist tooexecute Hallo opstarten.</span><span class="sxs-lookup"><span data-stu-id="e0709-156">In hello case of a **worker role** project, **LauncherWorker.ps1** file is required tooexecute hello startup file.</span></span> <span data-ttu-id="e0709-157">In een **Webrol** project, hello opstartbestand is in plaats daarvan gedefinieerd in de Projecteigenschappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="e0709-157">In a **web role** project, hello startup file is instead defined in hello project properties.</span></span>
> 
> 

<span data-ttu-id="e0709-158">Hallo **bin\LaunchWorker.ps1** toodo veel voorbereidende werk, maar niet echt werkt oorspronkelijk is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e0709-158">hello **bin\LaunchWorker.ps1** was originally created toodo a lot of prep work but it doesn't really work.</span></span> <span data-ttu-id="e0709-159">Hallo-inhoud in dat bestand vervangen door Hallo script te volgen.</span><span class="sxs-lookup"><span data-stu-id="e0709-159">Replace hello contents in that file with hello following script.</span></span>

<span data-ttu-id="e0709-160">Dit script aanroept Hallo **worker.py** bestand van uw project python.</span><span class="sxs-lookup"><span data-stu-id="e0709-160">This script calls hello **worker.py** file from your python project.</span></span> <span data-ttu-id="e0709-161">Als hello **PYTHON2** omgevingsvariabele is te ingesteld**op**, en vervolgens Python 2.7 wordt gebruikt, anders Python 3.5 wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e0709-161">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated)
{
    Write-Output "Running worker.py$nl"

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
else
{
    Write-Output "Running (EMULATED) worker.py$nl"

    # Customize tooyour local dev environment

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
```

#### <a name="pscmd"></a><span data-ttu-id="e0709-162">ps.cmd</span><span class="sxs-lookup"><span data-stu-id="e0709-162">ps.cmd</span></span>
<span data-ttu-id="e0709-163">Hallo Visual Studio sjablonen moeten gemaakt een **ps.cmd** bestand in Hallo **. / bin** map.</span><span class="sxs-lookup"><span data-stu-id="e0709-163">hello Visual Studio templates should have created a **ps.cmd** file in hello **./bin** folder.</span></span> <span data-ttu-id="e0709-164">Deze shell-script illustreert Hallo PowerShell bovenstaande wrapper-scripts en biedt logboekregistratie op basis van de naam Hallo van Hallo PowerShell wrapper is aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e0709-164">This shell script calls out hello PowerShell wrapper scripts above and provides logging based on hello name of hello PowerShell wrapper called.</span></span> <span data-ttu-id="e0709-165">Als dit bestand niet is gemaakt, ziet u hieronder wat het moet bevatten.</span><span class="sxs-lookup"><span data-stu-id="e0709-165">If this file wasn't created, here is what should be in it.</span></span> 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a><span data-ttu-id="e0709-166">Lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e0709-166">Run locally</span></span>
<span data-ttu-id="e0709-167">Als u uw cloudserviceproject als opstartproject Hallo instelt en druk op F5 Hallo cloudservice wordt uitgevoerd in Hallo lokale Azure-emulator.</span><span class="sxs-lookup"><span data-stu-id="e0709-167">If you set your cloud service project as hello startup project and press F5, hello cloud service runs in hello local Azure emulator.</span></span>

<span data-ttu-id="e0709-168">Hoewel PTVS ondersteunt werkt starten in Hallo emulator foutopsporing (bijvoorbeeld onderbrekingspunten) niet.</span><span class="sxs-lookup"><span data-stu-id="e0709-168">Although PTVS supports launching in hello emulator, debugging (for example, breakpoints) does not work.</span></span>

<span data-ttu-id="e0709-169">toodebug uw web- en werkrollen rollen, die u kunt Hallo rolproject instellen als opstartproject Hallo en fouten opsporen in dat in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="e0709-169">toodebug your web and worker roles, you can set hello role project as hello startup project and debug that instead.</span></span>  <span data-ttu-id="e0709-170">U kunt ook meerdere opstartprojecten instellen.</span><span class="sxs-lookup"><span data-stu-id="e0709-170">You can also set multiple startup projects.</span></span>  <span data-ttu-id="e0709-171">Met de rechtermuisknop op het Hallo-oplossing en selecteer vervolgens **Opstartprojecten instellen**.</span><span class="sxs-lookup"><span data-stu-id="e0709-171">Right-click hello solution and then select **Set StartUp Projects**.</span></span>

![Eigenschappen van opstartprojecten in de oplossing](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-tooazure"></a><span data-ttu-id="e0709-173">TooAzure publiceren</span><span class="sxs-lookup"><span data-stu-id="e0709-173">Publish tooAzure</span></span>
<span data-ttu-id="e0709-174">toopublish, met de rechtermuisknop op het Hallo-cloudserviceproject in Hallo oplossing en selecteer vervolgens **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="e0709-174">toopublish, right-click hello cloud service project in hello solution and then select **Publish**.</span></span>

![Aanmelden voor publiceren in Microsoft Azure](./media/cloud-services-python-ptvs/publish-sign-in.png)

<span data-ttu-id="e0709-176">Volg de wizard Hallo.</span><span class="sxs-lookup"><span data-stu-id="e0709-176">Follow hello wizard.</span></span> <span data-ttu-id="e0709-177">Schakel Extern bureaublad in, als dat nodig is.</span><span class="sxs-lookup"><span data-stu-id="e0709-177">If you need to, enable remote desktop.</span></span> <span data-ttu-id="e0709-178">Extern bureaublad is handig als u iets toodebug.</span><span class="sxs-lookup"><span data-stu-id="e0709-178">Remote desktop is helpful when you need toodebug something.</span></span>

<span data-ttu-id="e0709-179">Klik op **Publiceren** wanneer u klaar bent met het configureren van instellingen.</span><span class="sxs-lookup"><span data-stu-id="e0709-179">When you are done configuring settings, click **Publish**.</span></span>

<span data-ttu-id="e0709-180">De voortgang wordt weergegeven in het uitvoervenster Hallo vervolgens ziet u Hallo activiteitenlogboek van Microsoft Azure-venster.</span><span class="sxs-lookup"><span data-stu-id="e0709-180">Some progress appears in hello output window, then you'll see hello Microsoft Azure Activity Log window.</span></span>

![Het venster Activiteitenlogboek van Microsoft Azure](./media/cloud-services-python-ptvs/publish-activity-log.png)

<span data-ttu-id="e0709-182">Implementatie duurt enkele minuten toocomplete, vervolgens uw web-en/of werkrollen uitgevoerd op Azure!</span><span class="sxs-lookup"><span data-stu-id="e0709-182">Deployment takes several minutes toocomplete, then your web and/or worker roles run on Azure!</span></span>

### <a name="investigate-logs"></a><span data-ttu-id="e0709-183">Logboeken onderzoeken</span><span class="sxs-lookup"><span data-stu-id="e0709-183">Investigate logs</span></span>
<span data-ttu-id="e0709-184">Nadat Hallo cloud service virtuele machine opgestart wordt en geïnstalleerd Python, kunt u bekijkt hello logboeken toofind foutberichten.</span><span class="sxs-lookup"><span data-stu-id="e0709-184">After hello cloud service virtual machine starts up and installs Python, you can look at hello logs toofind any failure messages.</span></span> <span data-ttu-id="e0709-185">Deze logboeken bevinden zich in Hallo **C:\Resources\Directory\\{rol} \LogFiles** map.</span><span class="sxs-lookup"><span data-stu-id="e0709-185">These logs are located in hello **C:\Resources\Directory\\{role}\LogFiles** folder.</span></span> <span data-ttu-id="e0709-186">**PrepPython.err.txt** met ten minste één fout erin uit wanneer Hallo script toodetect probeert als Python is geïnstalleerd en **PipInstaller.err.txt** een verouderde versie van pip mogelijk klagen.</span><span class="sxs-lookup"><span data-stu-id="e0709-186">**PrepPython.err.txt** has at least one error in it from when hello script tries toodetect if Python is installed and **PipInstaller.err.txt** may complain about an outdated version of pip.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0709-187">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e0709-187">Next steps</span></span>
<span data-ttu-id="e0709-188">Zie de documentatie bij PTVS Hallo voor meer gedetailleerde informatie over het werken met functies voor web- en werkrollen in Python-Tools voor Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="e0709-188">For more detailed information about working with web and worker roles in Python Tools for Visual Studio, see hello PTVS documentation:</span></span>

* <span data-ttu-id="e0709-189">[Cloudserviceprojecten][Cloud Service Projects]</span><span class="sxs-lookup"><span data-stu-id="e0709-189">[Cloud Service Projects][Cloud Service Projects]</span></span>

<span data-ttu-id="e0709-190">Zie voor meer informatie over het gebruik van Azure-services van uw web- en werkrollen rollen, zoals het gebruik van Azure Storage of Service Bus Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e0709-190">For more details about using Azure services from your web and worker roles, such as using Azure Storage or Service Bus, see hello following articles:</span></span>

* <span data-ttu-id="e0709-191">[Blob-service][Blob Service]</span><span class="sxs-lookup"><span data-stu-id="e0709-191">[Blob Service][Blob Service]</span></span>
* <span data-ttu-id="e0709-192">[Tabelservice][Table Service]</span><span class="sxs-lookup"><span data-stu-id="e0709-192">[Table Service][Table Service]</span></span>
* <span data-ttu-id="e0709-193">[Wachtrijservice][Queue Service]</span><span class="sxs-lookup"><span data-stu-id="e0709-193">[Queue Service][Queue Service]</span></span>
* <span data-ttu-id="e0709-194">[Service Bus-wachtrijen][Service Bus Queues]</span><span class="sxs-lookup"><span data-stu-id="e0709-194">[Service Bus Queues][Service Bus Queues]</span></span>
* <span data-ttu-id="e0709-195">[Service Bus-onderwerpen][Service Bus Topics]</span><span class="sxs-lookup"><span data-stu-id="e0709-195">[Service Bus Topics][Service Bus Topics]</span></span>

<!--Link references-->

[Wat is een cloudservice?]: cloud-services-choose-me.md
[execution model-web sites]: ../app-service-web/app-service-web-overview.md
[execution model-vms]:../virtual-machines/windows/overview.md
[execution model-cloud services]: cloud-services-choose-me.md
[Python Developer Center]: /develop/python/

[Blob Service]:../storage/blobs/storage-python-how-to-use-blob-storage.md
[Queue Service]: ../storage/queues/storage-python-how-to-use-queue-storage.md
[Table Service]:../cosmos-db/table-storage-how-to-use-python.md
[Service Bus Queues]: ../service-bus-messaging/service-bus-python-how-to-use-queues.md
[Service Bus Topics]: ../service-bus-messaging/service-bus-python-how-to-use-topics-subscriptions.md


<!--External Link references-->

[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs
[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure SDK Tools for VS 2013]: http://go.microsoft.com/fwlink/?LinkId=746482
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=746481
[Azure SDK Tools for VS 2017]: http://go.microsoft.com/fwlink/?LinkId=746483
[Python 2.7 32-bit]: https://www.python.org/downloads/
[Python 3.5 32-bit]: https://www.python.org/downloads/
