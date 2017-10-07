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
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a>Python-web- en -werkrollen met Python-tools voor Visual Studio

Dit artikel biedt een overzicht van het gebruik van Python-web- en -werkrollen met [Python Tools for Visual Studio][Python Tools for Visual Studio]. Meer informatie over hoe toouse Visual Studio toocreate en implementeren van een eenvoudige Cloud-Service die gebruikmaakt van Python.

## <a name="prerequisites"></a>Vereisten
* [Visual Studio 2013, 2015 of 2017](https://www.visualstudio.com/)
* [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)
* [Azure SDK-hulpprogramma’s voor VS 2013][Azure SDK Tools for VS 2013] of  
[Azure SDK-hulpprogramma’s voor VS 2015][Azure SDK Tools for VS 2015] of  
[Azure SDK-tools voor VS 2017][Azure SDK Tools for VS 2017]
* [Python 2.7 32-bits][Python 2.7 32-bit] of [Python 3.5 32-bits][Python 3.5 32-bit]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a>Wat zijn Python-web- en -werkrollen?
Azure biedt drie rekenmodellen voor het uitvoeren van toepassingen: [web-appsfunctie in Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms] en [Azure Cloud Services][execution model-cloud services]. Alle drie modellen ondersteunen Python. Cloud Services, die web- en werkrollen bevatten, bieden *Platform as a Service (PaaS)*. Binnen een cloudservice biedt een Webrol een speciale Internet Information Services (IIS) web server toohost front-end-web-toepassingen, terwijl een werkrol kan asynchrone, langlopende of permanente onafhankelijk van de gebruikersinteractie of invoer taken worden uitgevoerd.

Zie [Wat is een cloudservice?] voor meer informatie.

> [!NOTE]
> *Zoek toobuild een ongecompliceerde website?*
> Als uw scenario slechts een ongecompliceerde website-front-end omvat, kunt u overwegen Hallo eenvoudige functie Web Apps in Azure App Service. Als uw website groeit en uw vereisten veranderen, kunt u gemakkelijk tooa Cloudservice upgraden. Zie Hallo <a href="/develop/python/">Python Developer Center</a> voor artikelen over ontwikkeling met de functie van de Hallo Web Apps in Azure App Service.
> <br />
> 
> 

## <a name="project-creation"></a>Een project maken
In Visual Studio, kunt u **Azure Cloud Service** in Hallo **nieuw Project** dialoogvenster onder **Python**.

![Het dialoogvenster Nieuw project](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

U kunt nieuwe web- en werkrollen maken in hello Azure Cloud Service-wizard.

![Het dialoogvenster Azure Cloud Service](./media/cloud-services-python-ptvs/new-service-wizard.png)

Hallo werkrolsjabloon wordt geleverd met standaardtekst code tooconnect tooan Azure storage-account of Azure Service Bus.

![Cloudserviceoplossing](./media/cloud-services-python-ptvs/worker.png)

U kunt de web- of worker rollen tooan bestaande cloudservice op elk gewenst moment toevoegen.  U kunt de bestaande projecten tooadd kiezen in uw oplossing of nieuwe maken.

![De opdracht Rol toevoegen](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

Uw cloudservice kan rollen bevatten die zijn geïmplementeerd in verschillende talen.  U kunt bijvoorbeeld een Python-webrol hebben die is geïmplementeerd met Django, met Python of met C#-werkrollen.  U kunt eenvoudig communiceren tussen uw rollen met behulp van de Service Bus-wachtrijen of opslagwachtrijen.

## <a name="install-python-on-hello-cloud-service"></a>Python installeren op Hallo-cloudservice
> [!WARNING]
> Hallo setup-scripts die zijn geïnstalleerd met Visual Studio (op Hallo tijd die in dit artikel voor het laatst is bijgewerkt) werken niet. Deze sectie beschrijft een tijdelijke oplossing.
> 
> 

Hallo belangrijkste probleem met de installatiescripts Hallo is dat ze niet python installeert. Eerste stap definieert twee [starten van de taken](cloud-services-startup-tasks.md) in Hallo [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) bestand. de eerste taak hello (**PrepPython.ps1**) downloadt en installeert Hallo Python-runtime. de tweede taak hello (**PipInstaller.ps1**) pip tooinstall eventuele afhankelijkheden die u hebt uitgevoerd.

Hallo scripts te volgen zijn geschreven als doel Python 3.5. Als u wilt dat toouse Hallo versie 2.x van python, set Hallo **PYTHON2** variabele bestand te**op** voor Hallo twee starten van de taken en runtime-taak Hallo: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.

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

Hallo **PYTHON2** en **PYPATH** variabelen toohello worker starten van de taak moeten worden toegevoegd. Hallo **PYPATH** variabele wordt alleen gebruikt als hello **PYTHON2** variabele is ingesteld, te**op**.

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

#### <a name="sample-servicedefinitioncsdef"></a>Voorbeeld van ServiceDefinition.csdef
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



Maak vervolgens Hallo **PrepPython.ps1** en **PipInstaller.ps1** bestanden in Hallo **. / bin** map van uw rol.

#### <a name="preppythonps1"></a>PrepPython.ps1
Dit script installeert Python. Als hello **PYTHON2** omgevingsvariabele is te ingesteld**op**, en vervolgens Python 2.7 is geïnstalleerd, anders Python 3.5 is geïnstalleerd.

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

#### <a name="pipinstallerps1"></a>PipInstaller.ps1
Dit script pip-aanroepen en installeert u alle afhankelijkheden Hallo in Hallo **requirements.txt** bestand. Als hello **PYTHON2** omgevingsvariabele is te ingesteld**op**, en vervolgens Python 2.7 wordt gebruikt, anders Python 3.5 wordt gebruikt.

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

#### <a name="modify-launchworkerps1"></a>LaunchWorker.ps1 wijzigen
> [!NOTE]
> In geval van Hallo een **werkrol** project **LauncherWorker.ps1** bestand is vereist tooexecute Hallo opstarten. In een **Webrol** project, hello opstartbestand is in plaats daarvan gedefinieerd in de Projecteigenschappen Hallo.
> 
> 

Hallo **bin\LaunchWorker.ps1** toodo veel voorbereidende werk, maar niet echt werkt oorspronkelijk is gemaakt. Hallo-inhoud in dat bestand vervangen door Hallo script te volgen.

Dit script aanroept Hallo **worker.py** bestand van uw project python. Als hello **PYTHON2** omgevingsvariabele is te ingesteld**op**, en vervolgens Python 2.7 wordt gebruikt, anders Python 3.5 wordt gebruikt.

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

#### <a name="pscmd"></a>ps.cmd
Hallo Visual Studio sjablonen moeten gemaakt een **ps.cmd** bestand in Hallo **. / bin** map. Deze shell-script illustreert Hallo PowerShell bovenstaande wrapper-scripts en biedt logboekregistratie op basis van de naam Hallo van Hallo PowerShell wrapper is aangeroepen. Als dit bestand niet is gemaakt, ziet u hieronder wat het moet bevatten. 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a>Lokaal uitvoeren
Als u uw cloudserviceproject als opstartproject Hallo instelt en druk op F5 Hallo cloudservice wordt uitgevoerd in Hallo lokale Azure-emulator.

Hoewel PTVS ondersteunt werkt starten in Hallo emulator foutopsporing (bijvoorbeeld onderbrekingspunten) niet.

toodebug uw web- en werkrollen rollen, die u kunt Hallo rolproject instellen als opstartproject Hallo en fouten opsporen in dat in plaats daarvan.  U kunt ook meerdere opstartprojecten instellen.  Met de rechtermuisknop op het Hallo-oplossing en selecteer vervolgens **Opstartprojecten instellen**.

![Eigenschappen van opstartprojecten in de oplossing](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-tooazure"></a>TooAzure publiceren
toopublish, met de rechtermuisknop op het Hallo-cloudserviceproject in Hallo oplossing en selecteer vervolgens **publiceren**.

![Aanmelden voor publiceren in Microsoft Azure](./media/cloud-services-python-ptvs/publish-sign-in.png)

Volg de wizard Hallo. Schakel Extern bureaublad in, als dat nodig is. Extern bureaublad is handig als u iets toodebug.

Klik op **Publiceren** wanneer u klaar bent met het configureren van instellingen.

De voortgang wordt weergegeven in het uitvoervenster Hallo vervolgens ziet u Hallo activiteitenlogboek van Microsoft Azure-venster.

![Het venster Activiteitenlogboek van Microsoft Azure](./media/cloud-services-python-ptvs/publish-activity-log.png)

Implementatie duurt enkele minuten toocomplete, vervolgens uw web-en/of werkrollen uitgevoerd op Azure!

### <a name="investigate-logs"></a>Logboeken onderzoeken
Nadat Hallo cloud service virtuele machine opgestart wordt en geïnstalleerd Python, kunt u bekijkt hello logboeken toofind foutberichten. Deze logboeken bevinden zich in Hallo **C:\Resources\Directory\\{rol} \LogFiles** map. **PrepPython.err.txt** met ten minste één fout erin uit wanneer Hallo script toodetect probeert als Python is geïnstalleerd en **PipInstaller.err.txt** een verouderde versie van pip mogelijk klagen.

## <a name="next-steps"></a>Volgende stappen
Zie de documentatie bij PTVS Hallo voor meer gedetailleerde informatie over het werken met functies voor web- en werkrollen in Python-Tools voor Visual Studio:

* [Cloudserviceprojecten][Cloud Service Projects]

Zie voor meer informatie over het gebruik van Azure-services van uw web- en werkrollen rollen, zoals het gebruik van Azure Storage of Service Bus Hallo artikelen te volgen:

* [Blob-service][Blob Service]
* [Tabelservice][Table Service]
* [Wachtrijservice][Queue Service]
* [Service Bus-wachtrijen][Service Bus Queues]
* [Service Bus-onderwerpen][Service Bus Topics]

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
