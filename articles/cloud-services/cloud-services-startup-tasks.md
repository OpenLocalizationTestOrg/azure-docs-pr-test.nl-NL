---
title: Starten van de taken in Azure Cloud Services aaaRun | Microsoft Docs
description: Starten van de taken helpen bij het voorbereiden van uw cloud service-omgeving voor uw app. Dit leert u hoe het starten van de taken werken en hoe toomake ze
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 886939be-4b5b-49cc-9a6e-2172e3c133e9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 3391a5d7434164f59972b8e497e5c34e33409543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-and-run-startup-tasks-for-a-cloud-service"></a><span data-ttu-id="34101-104">Hoe tooconfigure en voer opstarten taken voor een cloudservice</span><span class="sxs-lookup"><span data-stu-id="34101-104">How tooconfigure and run startup tasks for a cloud service</span></span>
<span data-ttu-id="34101-105">U kunt opstarten taken tooperform operations voordat een rol wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="34101-105">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="34101-106">Wilt u misschien tooperform bewerkingen bevatten een onderdeel te installeren, het registreren van COM-onderdelen, registersleutels instellen of starten van een langdurige proces.</span><span class="sxs-lookup"><span data-stu-id="34101-106">Operations that you might want tooperform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span>

> [!NOTE]
> <span data-ttu-id="34101-107">Starten van de taken zijn niet van toepassing tooVirtual Machines, alleen tooCloud Service-Web- en werkrollen.</span><span class="sxs-lookup"><span data-stu-id="34101-107">Startup tasks are not applicable tooVirtual Machines, only tooCloud Service Web and Worker roles.</span></span>
> 
> 

## <a name="how-startup-tasks-work"></a><span data-ttu-id="34101-108">De werking van de taken starten</span><span class="sxs-lookup"><span data-stu-id="34101-108">How startup tasks work</span></span>
<span data-ttu-id="34101-109">Starten van de taken zijn acties die worden uitgevoerd voordat uw rollen beginnen en zijn gedefinieerd in Hallo [ServiceDefinition.csdef] bestand met behulp van Hallo [taak] element in Hallo [opstarten]element.</span><span class="sxs-lookup"><span data-stu-id="34101-109">Startup tasks are actions that are taken before your roles begin and are defined in hello [ServiceDefinition.csdef] file by using hello [Task] element within hello [Startup] element.</span></span> <span data-ttu-id="34101-110">Starten van de taken zijn vaak batch-bestanden, maar ze kunnen ook worden consoletoepassingen of batch-bestanden die PowerShell-scripts starten.</span><span class="sxs-lookup"><span data-stu-id="34101-110">Frequently startup tasks are batch files, but they can also be console applications, or batch files that start PowerShell scripts.</span></span>

<span data-ttu-id="34101-111">Omgevingsvariabelen informatie doorgeven in een taak starten en lokale opslag kan gegevens uit een taak starten van de gebruikte toopass.</span><span class="sxs-lookup"><span data-stu-id="34101-111">Environment variables pass information into a startup task, and local storage can be used toopass information out of a startup task.</span></span> <span data-ttu-id="34101-112">Bijvoorbeeld een omgevingsvariabele Hallo pad tooa programma kunt opgeven dat u wilt dat tooinstall en bestanden kunnen worden geschreven toolocal opslag die vervolgens door uw rollen later kan worden gelezen.</span><span class="sxs-lookup"><span data-stu-id="34101-112">For example, an environment variable can specify hello path tooa program you want tooinstall, and files can be written toolocal storage that can then be read later by your roles.</span></span>

<span data-ttu-id="34101-113">Het starten van de taak kan zich aanmelden informatie en fouten toohello map die is opgegeven door Hallo **TEMP** omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="34101-113">Your startup task can log information and errors toohello directory specified by hello **TEMP** environment variable.</span></span> <span data-ttu-id="34101-114">Hallo tijdens Hallo starten van de taak **TEMP** omgevingsvariabele wordt omgezet toohello *C:\\Resources\\temp\\[guid]. [ rolename]\\RoleTemp* directory wanneer u gebruikmaakt van Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="34101-114">During hello startup task, hello **TEMP** environment variable resolves toohello *C:\\Resources\\temp\\[guid].[rolename]\\RoleTemp* directory when running on hello cloud.</span></span>

<span data-ttu-id="34101-115">Starten van de taken kunnen ook worden uitgevoerd meerdere keren opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="34101-115">Startup tasks can also be executed several times between reboots.</span></span> <span data-ttu-id="34101-116">Bijvoorbeeld Hallo starten van de taak wordt uitgevoerd telkens Hallo-rol wordt gerecycled en rol recyclet mogelijk opnieuw opstarten geen altijd opgenomen.</span><span class="sxs-lookup"><span data-stu-id="34101-116">For example, hello startup task will be run each time hello role recycles, and role recycles may not always include a reboot.</span></span> <span data-ttu-id="34101-117">Starten van de taken worden op een manier die ze toorun meerdere keren zonder problemen kan geschreven.</span><span class="sxs-lookup"><span data-stu-id="34101-117">Startup tasks should be written in a way that allows them toorun several times without problems.</span></span>

<span data-ttu-id="34101-118">Starten van de taken moeten eindigen met een **errorlevel** (of afsluitcode) van nul voor Hallo opstarten proces toocomplete.</span><span class="sxs-lookup"><span data-stu-id="34101-118">Startup tasks must end with an **errorlevel** (or exit code) of zero for hello startup process toocomplete.</span></span> <span data-ttu-id="34101-119">Als een taak starten met een niet-nul eindigt **errorlevel**, Hallo-rol kan niet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="34101-119">If a startup task ends with a non-zero **errorlevel**, hello role will not start.</span></span>

## <a name="role-startup-order"></a><span data-ttu-id="34101-120">De opstartvolgorde rol</span><span class="sxs-lookup"><span data-stu-id="34101-120">Role startup order</span></span>
<span data-ttu-id="34101-121">Hallo lijsten Hallo rol starten van de procedure in Azure te volgen:</span><span class="sxs-lookup"><span data-stu-id="34101-121">hello following lists hello role startup procedure in Azure:</span></span>

1. <span data-ttu-id="34101-122">Hallo-exemplaar is gemarkeerd als **starten** en ontvangt geen verkeer.</span><span class="sxs-lookup"><span data-stu-id="34101-122">hello instance is marked as **Starting** and does not receive traffic.</span></span>
2. <span data-ttu-id="34101-123">Alle starten van de taken worden uitgevoerd op basis van tootheir **taskType** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="34101-123">All startup tasks are executed according tootheir **taskType** attribute.</span></span>
   
   * <span data-ttu-id="34101-124">Hallo **eenvoudige** taken worden uitgevoerd, synchroon, één voor één.</span><span class="sxs-lookup"><span data-stu-id="34101-124">hello **simple** tasks are executed synchronously, one at a time.</span></span>
   * <span data-ttu-id="34101-125">Hallo **achtergrond** en **voorgrond** taken zijn gestart asynchroon, parallelle toohello starten van de taak.</span><span class="sxs-lookup"><span data-stu-id="34101-125">hello **background** and **foreground** tasks are started asynchronously, parallel toohello startup task.</span></span>  
     
     > [!WARNING]
     > <span data-ttu-id="34101-126">IIS mogelijk niet volledig geconfigureerd tijdens het Hallo starten van de taak in het opstartproces hello, zodat rolspecifieke gegevens mogelijk niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="34101-126">IIS may not be fully configured during hello startup task stage in hello startup process, so role-specific data may not be available.</span></span> <span data-ttu-id="34101-127">Starten van de taken waarvoor rolspecifieke gegevens moeten gebruiken [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span><span class="sxs-lookup"><span data-stu-id="34101-127">Startup tasks that require role-specific data should use [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span></span>
     > 
     > 
3. <span data-ttu-id="34101-128">hostproces Hallo-rol is gestart en Hallo site is gemaakt in IIS.</span><span class="sxs-lookup"><span data-stu-id="34101-128">hello role host process is started and hello site is created in IIS.</span></span>
4. <span data-ttu-id="34101-129">Hallo [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) methode wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="34101-129">hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method is called.</span></span>
5. <span data-ttu-id="34101-130">Hallo-exemplaar is gemarkeerd als **gereed** en verkeer wordt gerouteerd toohello exemplaar.</span><span class="sxs-lookup"><span data-stu-id="34101-130">hello instance is marked as **Ready** and traffic is routed toohello instance.</span></span>
6. <span data-ttu-id="34101-131">Hallo [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="34101-131">hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method is called.</span></span>

## <a name="example-of-a-startup-task"></a><span data-ttu-id="34101-132">Voorbeeld van een taak starten</span><span class="sxs-lookup"><span data-stu-id="34101-132">Example of a startup task</span></span>
<span data-ttu-id="34101-133">Starten van de taken zijn gedefinieerd in Hallo [ServiceDefinition.csdef] bestand in Hallo **taak** element.</span><span class="sxs-lookup"><span data-stu-id="34101-133">Startup tasks are defined in hello [ServiceDefinition.csdef] file, in hello **Task** element.</span></span> <span data-ttu-id="34101-134">Hallo **commandLine** kenmerk geeft Hallo naam en parameters van Hallo starten van de batch-bestand of console opdracht hello **executionContext** kenmerk geeft machtigingsniveau Hallo Hallo opstarten taak en Hallo **taskType** kenmerk geeft aan hoe Hallo-taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="34101-134">hello **commandLine** attribute specifies hello name and parameters of hello startup batch file or console command, hello **executionContext** attribute specifies hello privilege level of hello startup task, and hello **taskType** attribute specifies how hello task will be executed.</span></span>

<span data-ttu-id="34101-135">In dit voorbeeld wordt een omgevingsvariabele **MyVersionNumber**, is gemaakt voor Hallo starten van de taak en stel toohello waarde '**1.0.0.0**'.</span><span class="sxs-lookup"><span data-stu-id="34101-135">In this example, an environment variable, **MyVersionNumber**, is created for hello startup task and set toohello value "**1.0.0.0**".</span></span>

<span data-ttu-id="34101-136">**ServiceDefinition.csdef**:</span><span class="sxs-lookup"><span data-stu-id="34101-136">**ServiceDefinition.csdef**:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

<span data-ttu-id="34101-137">Hallo in Hallo voorbeeld te volgen, **Startup.cmd** batchbestand schrijft Hallo regel 'hello huidige versie is 1.0.0.0' toohello StartupLog.txt bestand in de opgegeven door de omgevingsvariabele TEMP Hallo Hallo-map.</span><span class="sxs-lookup"><span data-stu-id="34101-137">In hello following example, hello **Startup.cmd** batch file writes hello line "hello current version is 1.0.0.0" toohello StartupLog.txt file in hello directory specified by hello TEMP environment variable.</span></span> <span data-ttu-id="34101-138">Hallo `EXIT /B 0` regel zorgt ervoor dat opstarttaak Hallo eindigt met een **errorlevel** gelijk is aan nul.</span><span class="sxs-lookup"><span data-stu-id="34101-138">hello `EXIT /B 0` line ensures that hello startup task ends with an **errorlevel** of zero.</span></span>

```cmd
ECHO hello current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> <span data-ttu-id="34101-139">In Visual Studio Hallo **tooOutput Directory kopiëren** eigenschap voor het starten van de batch-bestand te moet worden ingesteld**kopie altijd** toobe of het starten van de batch-bestand is juist geïmplementeerd tooyour project op Azure (**approot\\bin** voor Web-rollen en **approot** voor werkrollen).</span><span class="sxs-lookup"><span data-stu-id="34101-139">In Visual Studio, hello **Copy tooOutput Directory** property for your startup batch file should be set too**Copy Always** toobe sure that your startup batch file is properly deployed tooyour project on Azure (**approot\\bin** for Web roles, and **approot** for worker roles).</span></span>
> 
> 

## <a name="description-of-task-attributes"></a><span data-ttu-id="34101-140">Beschrijving van de kenmerken van de taak</span><span class="sxs-lookup"><span data-stu-id="34101-140">Description of task attributes</span></span>
<span data-ttu-id="34101-141">Hallo hieronder wordt beschreven Hallo kenmerken van Hallo **taak** -element in Hallo [ServiceDefinition.csdef] bestand:</span><span class="sxs-lookup"><span data-stu-id="34101-141">hello following describes hello attributes of hello **Task** element in hello [ServiceDefinition.csdef] file:</span></span>

<span data-ttu-id="34101-142">**commandLine** -Hiermee geeft u de opdrachtregel Hallo voor Hallo starten van de taak:</span><span class="sxs-lookup"><span data-stu-id="34101-142">**commandLine** - Specifies hello command line for hello startup task:</span></span>

* <span data-ttu-id="34101-143">Hallo opdracht met optionele opdrachtregelparameters Hallo starten van de taak wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="34101-143">hello command, with optional command line parameters, which begins hello startup task.</span></span>
* <span data-ttu-id="34101-144">Dit is vaak Hallo-bestandsnaam van een batchbestand .cmd of .bat.</span><span class="sxs-lookup"><span data-stu-id="34101-144">Frequently this is hello filename of a .cmd or .bat batch file.</span></span>
* <span data-ttu-id="34101-145">Hallo-taak is relatief toohello AppRoot\\Bin-map voor Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="34101-145">hello task is relative toohello AppRoot\\Bin folder for hello deployment.</span></span> <span data-ttu-id="34101-146">Omgevingsvariabelen zijn niet bij het bepalen van Hallo pad en de bestandsnaam van de taak Hallo uitgevouwen.</span><span class="sxs-lookup"><span data-stu-id="34101-146">Environment variables are not expanded in determining hello path and file of hello task.</span></span> <span data-ttu-id="34101-147">Als uitbreiding van de omgeving vereist is, kunt u een kleine CMD-script waarmee het starten van de taak wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="34101-147">If environment expansion is required, you can create a small .cmd script that calls your startup task.</span></span>
* <span data-ttu-id="34101-148">Kan dit een consoletoepassing of een batchbestand dat begint een [PowerShell-script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span><span class="sxs-lookup"><span data-stu-id="34101-148">Can be a console application or a batch file that starts a [PowerShell script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span></span>

<span data-ttu-id="34101-149">**executionContext** -Hiermee geeft u op Hallo machtigingsniveau voor Hallo starten van de taak.</span><span class="sxs-lookup"><span data-stu-id="34101-149">**executionContext** - Specifies hello privilege level for hello startup task.</span></span> <span data-ttu-id="34101-150">Hallo machtigingsniveau kan worden beperkt of met verhoogde bevoegdheden:</span><span class="sxs-lookup"><span data-stu-id="34101-150">hello privilege level can be limited or elevated:</span></span>

* <span data-ttu-id="34101-151">**beperkt**</span><span class="sxs-lookup"><span data-stu-id="34101-151">**limited**</span></span>  
  <span data-ttu-id="34101-152">Hallo starten van de taak wordt uitgevoerd met dezelfde als Hallo rol toegangsrechten Hallo.</span><span class="sxs-lookup"><span data-stu-id="34101-152">hello startup task runs with hello same privileges as hello role.</span></span> <span data-ttu-id="34101-153">Wanneer Hallo **executionContext** kenmerk voor Hallo [Runtime] element is ook **beperkt**, en vervolgens de gebruiker heeft bevoegdheden die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34101-153">When hello **executionContext** attribute for hello [Runtime] element is also **limited**, then user privileges are used.</span></span>
* <span data-ttu-id="34101-154">**verhoogde**</span><span class="sxs-lookup"><span data-stu-id="34101-154">**elevated**</span></span>  
  <span data-ttu-id="34101-155">Hallo starten van de taak wordt uitgevoerd met administrator-bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="34101-155">hello startup task runs with administrator privileges.</span></span> <span data-ttu-id="34101-156">Zo kunnen opstarttaken tooinstall programma, IIS-configuratiewijzigingen aanbrengen, wijzigingen in het register en andere taken van de administrator-niveau uitvoeren zonder te verhogen machtigingsniveau Hallo van Hallo rol zelf.</span><span class="sxs-lookup"><span data-stu-id="34101-156">This allows startup tasks tooinstall programs, make IIS configuration changes, perform registry changes, and other administrator level tasks, without increasing hello privilege level of hello role itself.</span></span>  

> [!NOTE]
> <span data-ttu-id="34101-157">Hallo machtigingsniveau van een taak starten hoeft niet toobe Hallo dezelfde als Hallo rol zelf.</span><span class="sxs-lookup"><span data-stu-id="34101-157">hello privilege level of a startup task does not need toobe hello same as hello role itself.</span></span>
> 
> 

<span data-ttu-id="34101-158">**taskType** -Hiermee geeft u op Hallo manier een starten van de taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="34101-158">**taskType** - Specifies hello way a startup task is executed.</span></span>

* <span data-ttu-id="34101-159">**eenvoudige**</span><span class="sxs-lookup"><span data-stu-id="34101-159">**simple**</span></span>  
  <span data-ttu-id="34101-160">Taken worden uitgevoerd synchroon, één voor één, in volgorde van Hallo opgegeven in Hallo [ServiceDefinition.csdef] bestand.</span><span class="sxs-lookup"><span data-stu-id="34101-160">Tasks are executed synchronously, one at a time, in hello order specified in hello [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="34101-161">Wanneer een **eenvoudige** opstarttaak eindigt met een **errorlevel** is aan nul, Hallo naast **eenvoudige** starten van de taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="34101-161">When one **simple** startup task ends with an **errorlevel** of zero, hello next **simple** startup task is executed.</span></span> <span data-ttu-id="34101-162">Als er niet meer **eenvoudige** opstarten tooexecute, taken en vervolgens het Hallo-rol zelf wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="34101-162">If there are no more **simple** startup tasks tooexecute, then hello role itself will be started.</span></span>   
  
  > [!NOTE]
  > <span data-ttu-id="34101-163">Als hello **eenvoudige** taak eindigt met een niet-nul **errorlevel**, Hallo-exemplaar wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="34101-163">If hello **simple** task ends with a non-zero **errorlevel**, hello instance will be blocked.</span></span> <span data-ttu-id="34101-164">Daaropvolgende **eenvoudige** starten van de taken en Hallo rol zelf, kunnen niet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="34101-164">Subsequent **simple** startup tasks, and hello role itself, will not start.</span></span>
  > 
  > 
  
    <span data-ttu-id="34101-165">tooensure dat uw batchbestand met eindigt een **errorlevel** is aan nul, Hallo-opdracht uitvoeren `EXIT /B 0` aan Hallo einde van uw batch-bestand.</span><span class="sxs-lookup"><span data-stu-id="34101-165">tooensure that your batch file ends with an **errorlevel** of zero, execute hello command `EXIT /B 0` at hello end of your batch file process.</span></span>
* <span data-ttu-id="34101-166">**achtergrond**</span><span class="sxs-lookup"><span data-stu-id="34101-166">**background**</span></span>  
  <span data-ttu-id="34101-167">Taken worden asynchroon uitgevoerd parallel met Hallo opstarten van Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="34101-167">Tasks are executed asynchronously, in parallel with hello startup of hello role.</span></span>
* <span data-ttu-id="34101-168">**voorgrond**</span><span class="sxs-lookup"><span data-stu-id="34101-168">**foreground**</span></span>  
  <span data-ttu-id="34101-169">Taken worden asynchroon uitgevoerd parallel met Hallo opstarten van Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="34101-169">Tasks are executed asynchronously, in parallel with hello startup of hello role.</span></span> <span data-ttu-id="34101-170">Hallo belangrijkste verschil tussen een **voorgrond** en een **achtergrond** taak is dat een **voorgrond** taak voorkomt dat Hallo-functie uit de recycling of totdat het Hallo-taak is afgesloten beëindigd.</span><span class="sxs-lookup"><span data-stu-id="34101-170">hello key difference between a **foreground** and a **background** task is that a **foreground** task prevents hello role from recycling or shutting down until hello task has ended.</span></span> <span data-ttu-id="34101-171">Hallo **achtergrond** taken beschikt niet over deze beperking.</span><span class="sxs-lookup"><span data-stu-id="34101-171">hello **background** tasks do not have this restriction.</span></span>

## <a name="environment-variables"></a><span data-ttu-id="34101-172">Omgevingsvariabelen</span><span class="sxs-lookup"><span data-stu-id="34101-172">Environment variables</span></span>
<span data-ttu-id="34101-173">Omgevingsvariabelen zijn een manier toopass informatie tooa starten van de taak.</span><span class="sxs-lookup"><span data-stu-id="34101-173">Environment variables are a way toopass information tooa startup task.</span></span> <span data-ttu-id="34101-174">U kunt bijvoorbeeld Hallo pad tooa blob met een tooinstall programma of poortnummers die door uw rol wordt gebruikt of instellingen toocontrol functies van uw opstarttaak plaatsen.</span><span class="sxs-lookup"><span data-stu-id="34101-174">For example, you can put hello path tooa blob that contains a program tooinstall, or port numbers that your role will use, or settings toocontrol features of your startup task.</span></span>

<span data-ttu-id="34101-175">Er zijn twee soorten van omgevingsvariabelen voor starten van de taken. statische omgevingsvariabelen en omgevingsvariabelen op basis van de leden van Hallo [ RoleEnvironment] klasse.</span><span class="sxs-lookup"><span data-stu-id="34101-175">There are two kinds of environment variables for startup tasks; static environment variables and environment variables based on members of hello [RoleEnvironment] class.</span></span> <span data-ttu-id="34101-176">Beide zijn in Hallo [omgeving] sectie Hallo [ServiceDefinition.csdef] bestands- en beide Hallo gebruik [variabele] element en **naam** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="34101-176">Both are in hello [Environment] section of hello [ServiceDefinition.csdef] file, and both use hello [Variable] element and **name** attribute.</span></span>

<span data-ttu-id="34101-177">Statische omgeving variabelen gebruikt Hallo **waarde** kenmerk Hallo [variabele] element.</span><span class="sxs-lookup"><span data-stu-id="34101-177">Static environment variables uses hello **value** attribute of hello [Variable] element.</span></span> <span data-ttu-id="34101-178">Hallo in bovenstaand voorbeeld maakt de omgevingsvariabele Hallo **MyVersionNumber** die een vaste waarde heeft van '**1.0.0.0**'.</span><span class="sxs-lookup"><span data-stu-id="34101-178">hello example above creates hello environment variable **MyVersionNumber** which has a static value of "**1.0.0.0**".</span></span> <span data-ttu-id="34101-179">Een ander voorbeeld is toocreate een **StagingOrProduction** omgevingsvariabele die u handmatig toovalues van instellen kunt '**fasering**"of"**productie**' tooperform starten van de verschillende acties die zijn gebaseerd op Hallo-waarde van Hallo **StagingOrProduction** omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="34101-179">Another example would be toocreate a **StagingOrProduction** environment variable which you can manually set toovalues of "**staging**" or "**production**" tooperform different startup actions based on hello value of hello **StagingOrProduction** environment variable.</span></span>

<span data-ttu-id="34101-180">Omgevingsvariabelen op basis van de leden van Hallo RoleEnvironment klasse gebruik geen Hallo **waarde** kenmerk Hallo [variabele] element.</span><span class="sxs-lookup"><span data-stu-id="34101-180">Environment variables based on members of hello RoleEnvironment class do not use hello **value** attribute of hello [Variable] element.</span></span> <span data-ttu-id="34101-181">In plaats daarvan Hallo [RoleInstanceValue] onderliggend element met de juiste Hallo **XPath** kenmerkwaarde, gebruikte toocreate zijn een omgevingsvariabele op basis van een specifiek lid van Hallo [ RoleEnvironment] klasse.</span><span class="sxs-lookup"><span data-stu-id="34101-181">Instead, hello [RoleInstanceValue] child element, with hello appropriate **XPath** attribute value, are used toocreate an environment variable based on a specific member of hello [RoleEnvironment] class.</span></span> <span data-ttu-id="34101-182">Waarden voor Hallo **XPath** tooaccess kenmerk verschillende [ RoleEnvironment] waarden kunt u vinden [hier](cloud-services-role-config-xpath.md).</span><span class="sxs-lookup"><span data-stu-id="34101-182">Values for hello **XPath** attribute tooaccess various [RoleEnvironment] values can be found [here](cloud-services-role-config-xpath.md).</span></span>

<span data-ttu-id="34101-183">Toocreate bijvoorbeeld een omgevingsvariabele die is '**true**' wanneer Hallo-exemplaar wordt uitgevoerd in de rekenemulator hello, en "**false**' wanneer uitgevoerd in de cloud hello, gebruikt u de volgende Hallo [variabele] en [RoleInstanceValue] elementen:</span><span class="sxs-lookup"><span data-stu-id="34101-183">For example, toocreate an environment variable that is "**true**" when hello instance is running in hello compute emulator, and "**false**" when running in hello cloud, use hello following [Variable] and [RoleInstanceValue] elements:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create hello environment variable that informs hello startup task whether it is running
                in hello Compute Emulator or in hello cloud. "%ComputeEmulatorRunning%"=="true" when
                running in hello Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in hello cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a><span data-ttu-id="34101-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="34101-184">Next steps</span></span>
<span data-ttu-id="34101-185">Meer informatie over hoe tooperform sommige [algemene beheertaken voor opstarten](cloud-services-startup-tasks-common.md) met de Cloudservice.</span><span class="sxs-lookup"><span data-stu-id="34101-185">Learn how tooperform some [common startup tasks](cloud-services-startup-tasks-common.md) with your Cloud Service.</span></span>

<span data-ttu-id="34101-186">[Pakket](cloud-services-model-and-package.md) uw Cloudservice.</span><span class="sxs-lookup"><span data-stu-id="34101-186">[Package](cloud-services-model-and-package.md) your Cloud Service.</span></span>  

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[taak]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[opstarten]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[omgeving]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[variabele]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[ RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
