---
title: Starten van de taken uitvoeren in Azure-Cloudservices | Microsoft Docs
description: Starten van de taken helpen bij het voorbereiden van uw cloud service-omgeving voor uw app. Dit leert u hoe starten van de taken werken en hoe u ze
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
ms.openlocfilehash: 1c1b3aa86dc8211de0c07c9fb68da5685c86f551
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-and-run-startup-tasks-for-a-cloud-service"></a><span data-ttu-id="26e3a-104">Het configureren en starten van de taken voor een cloudservice uitvoeren</span><span class="sxs-lookup"><span data-stu-id="26e3a-104">How to configure and run startup tasks for a cloud service</span></span>
<span data-ttu-id="26e3a-105">Starten van de taken kunt u bewerkingen uitvoeren voordat een rol wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="26e3a-105">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="26e3a-106">Bewerkingen die u wilt uitvoeren bevatten voor het installeren van een onderdeel, registreren van COM-onderdelen, registersleutels instellen of starten van een langdurige proces.</span><span class="sxs-lookup"><span data-stu-id="26e3a-106">Operations that you might want to perform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span>

> [!NOTE]
> <span data-ttu-id="26e3a-107">Starten van de taken zijn niet van toepassing op virtuele Machines, alleen op Cloud Service-Web- en werkrollen.</span><span class="sxs-lookup"><span data-stu-id="26e3a-107">Startup tasks are not applicable to Virtual Machines, only to Cloud Service Web and Worker roles.</span></span>
> 
> 

## <a name="how-startup-tasks-work"></a><span data-ttu-id="26e3a-108">De werking van de taken starten</span><span class="sxs-lookup"><span data-stu-id="26e3a-108">How startup tasks work</span></span>
<span data-ttu-id="26e3a-109">Starten van de taken zijn acties die worden uitgevoerd voordat uw rollen beginnen en zijn gedefinieerd in de [ServiceDefinition.csdef] bestand met behulp van de [taak] element in de [opstarten] element.</span><span class="sxs-lookup"><span data-stu-id="26e3a-109">Startup tasks are actions that are taken before your roles begin and are defined in the [ServiceDefinition.csdef] file by using the [Task] element within the [Startup] element.</span></span> <span data-ttu-id="26e3a-110">Starten van de taken zijn vaak batch-bestanden, maar ze kunnen ook worden consoletoepassingen of batch-bestanden die PowerShell-scripts starten.</span><span class="sxs-lookup"><span data-stu-id="26e3a-110">Frequently startup tasks are batch files, but they can also be console applications, or batch files that start PowerShell scripts.</span></span>

<span data-ttu-id="26e3a-111">Omgevingsvariabelen informatie doorgeven in een taak starten en lokale opslag kan worden gebruikt voor het doorgeven van gegevens uit een taak starten.</span><span class="sxs-lookup"><span data-stu-id="26e3a-111">Environment variables pass information into a startup task, and local storage can be used to pass information out of a startup task.</span></span> <span data-ttu-id="26e3a-112">Bijvoorbeeld een omgevingsvariabele kan het pad opgeven naar een programma dat u wilt installeren, en bestanden kunnen worden geschreven naar de lokale opslag, die vervolgens door uw rollen later kan worden gelezen.</span><span class="sxs-lookup"><span data-stu-id="26e3a-112">For example, an environment variable can specify the path to a program you want to install, and files can be written to local storage that can then be read later by your roles.</span></span>

<span data-ttu-id="26e3a-113">Uw taak starten van de informatie en fouten kan vastleggen in de map die is opgegeven door de **TEMP** omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="26e3a-113">Your startup task can log information and errors to the directory specified by the **TEMP** environment variable.</span></span> <span data-ttu-id="26e3a-114">Tijdens het starten van de taak de **TEMP** omgevingsvariabele wordt omgezet naar de *C:\\Resources\\temp\\[guid]. [ rolename]\\RoleTemp* directory wanneer u gebruikmaakt van de cloud.</span><span class="sxs-lookup"><span data-stu-id="26e3a-114">During the startup task, the **TEMP** environment variable resolves to the *C:\\Resources\\temp\\[guid].[rolename]\\RoleTemp* directory when running on the cloud.</span></span>

<span data-ttu-id="26e3a-115">Starten van de taken kunnen ook worden uitgevoerd meerdere keren opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="26e3a-115">Startup tasks can also be executed several times between reboots.</span></span> <span data-ttu-id="26e3a-116">Bijvoorbeeld, het starten van de taak wordt uitgevoerd telkens wanneer die de functie wordt gerecycled en rol recyclet mogelijk opnieuw opstarten geen altijd opgenomen.</span><span class="sxs-lookup"><span data-stu-id="26e3a-116">For example, the startup task will be run each time the role recycles, and role recycles may not always include a reboot.</span></span> <span data-ttu-id="26e3a-117">Starten van de taken worden op een manier die ze meerdere keren uitvoert zonder problemen kan geschreven.</span><span class="sxs-lookup"><span data-stu-id="26e3a-117">Startup tasks should be written in a way that allows them to run several times without problems.</span></span>

<span data-ttu-id="26e3a-118">Starten van de taken moeten eindigen met een **errorlevel** (of afsluitcode) van nul voor het opstartproces te voltooien.</span><span class="sxs-lookup"><span data-stu-id="26e3a-118">Startup tasks must end with an **errorlevel** (or exit code) of zero for the startup process to complete.</span></span> <span data-ttu-id="26e3a-119">Als een taak starten met een niet-nul eindigt **errorlevel**, de rol kan niet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="26e3a-119">If a startup task ends with a non-zero **errorlevel**, the role will not start.</span></span>

## <a name="role-startup-order"></a><span data-ttu-id="26e3a-120">De opstartvolgorde rol</span><span class="sxs-lookup"><span data-stu-id="26e3a-120">Role startup order</span></span>
<span data-ttu-id="26e3a-121">Hieronder vindt u de procedure voor het opstarten van rollen in Azure:</span><span class="sxs-lookup"><span data-stu-id="26e3a-121">The following lists the role startup procedure in Azure:</span></span>

1. <span data-ttu-id="26e3a-122">Het exemplaar is gemarkeerd als **starten** en ontvangt geen verkeer.</span><span class="sxs-lookup"><span data-stu-id="26e3a-122">The instance is marked as **Starting** and does not receive traffic.</span></span>
2. <span data-ttu-id="26e3a-123">Alle starten van de taken worden uitgevoerd volgens hun **taskType** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="26e3a-123">All startup tasks are executed according to their **taskType** attribute.</span></span>
   
   * <span data-ttu-id="26e3a-124">De **eenvoudige** taken worden uitgevoerd, synchroon, één voor één.</span><span class="sxs-lookup"><span data-stu-id="26e3a-124">The **simple** tasks are executed synchronously, one at a time.</span></span>
   * <span data-ttu-id="26e3a-125">De **achtergrond** en **voorgrond** taken voor de taak starten asynchroon, parallel worden gestart.</span><span class="sxs-lookup"><span data-stu-id="26e3a-125">The **background** and **foreground** tasks are started asynchronously, parallel to the startup task.</span></span>  
     
     > [!WARNING]
     > <span data-ttu-id="26e3a-126">IIS mogelijk niet volledig geconfigureerd tijdens de fase van de taak starten in het opstartproces zodat rolspecifieke gegevens mogelijk niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="26e3a-126">IIS may not be fully configured during the startup task stage in the startup process, so role-specific data may not be available.</span></span> <span data-ttu-id="26e3a-127">Starten van de taken waarvoor rolspecifieke gegevens moeten gebruiken [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span><span class="sxs-lookup"><span data-stu-id="26e3a-127">Startup tasks that require role-specific data should use [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span></span>
     > 
     > 
3. <span data-ttu-id="26e3a-128">Het hostproces van de rol is gestart en de site is gemaakt in IIS.</span><span class="sxs-lookup"><span data-stu-id="26e3a-128">The role host process is started and the site is created in IIS.</span></span>
4. <span data-ttu-id="26e3a-129">De [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) methode wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="26e3a-129">The [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method is called.</span></span>
5. <span data-ttu-id="26e3a-130">Het exemplaar is gemarkeerd als **gereed** en verkeer wordt doorgestuurd naar het exemplaar.</span><span class="sxs-lookup"><span data-stu-id="26e3a-130">The instance is marked as **Ready** and traffic is routed to the instance.</span></span>
6. <span data-ttu-id="26e3a-131">De [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="26e3a-131">The [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method is called.</span></span>

## <a name="example-of-a-startup-task"></a><span data-ttu-id="26e3a-132">Voorbeeld van een taak starten</span><span class="sxs-lookup"><span data-stu-id="26e3a-132">Example of a startup task</span></span>
<span data-ttu-id="26e3a-133">Starten van de taken zijn gedefinieerd in de [ServiceDefinition.csdef] bestand in de **taak** element.</span><span class="sxs-lookup"><span data-stu-id="26e3a-133">Startup tasks are defined in the [ServiceDefinition.csdef] file, in the **Task** element.</span></span> <span data-ttu-id="26e3a-134">De **commandLine** kenmerk geeft de naam en parameters van de batch-bestand of console startopdracht, de **executionContext** kenmerk geeft u de bevoegdheden van de taak starten en de **taskType** kenmerk geeft aan hoe de taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="26e3a-134">The **commandLine** attribute specifies the name and parameters of the startup batch file or console command, the **executionContext** attribute specifies the privilege level of the startup task, and the **taskType** attribute specifies how the task will be executed.</span></span>

<span data-ttu-id="26e3a-135">In dit voorbeeld wordt een omgevingsvariabele **MyVersionNumber**, is gemaakt voor het starten van de taak en wordt ingesteld op de waarde '**1.0.0.0**'.</span><span class="sxs-lookup"><span data-stu-id="26e3a-135">In this example, an environment variable, **MyVersionNumber**, is created for the startup task and set to the value "**1.0.0.0**".</span></span>

<span data-ttu-id="26e3a-136">**ServiceDefinition.csdef**:</span><span class="sxs-lookup"><span data-stu-id="26e3a-136">**ServiceDefinition.csdef**:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

<span data-ttu-id="26e3a-137">In het volgende voorbeeld wordt de **Startup.cmd** batchbestand schrijft de regel 'de huidige versie is 1.0.0.0' naar het bestand StartupLog.txt in de map die is opgegeven door de omgevingsvariabele TEMP.</span><span class="sxs-lookup"><span data-stu-id="26e3a-137">In the following example, the **Startup.cmd** batch file writes the line "The current version is 1.0.0.0" to the StartupLog.txt file in the directory specified by the TEMP environment variable.</span></span> <span data-ttu-id="26e3a-138">De `EXIT /B 0` regel zorgt ervoor dat de opstarttaak met eindigt een **errorlevel** gelijk is aan nul.</span><span class="sxs-lookup"><span data-stu-id="26e3a-138">The `EXIT /B 0` line ensures that the startup task ends with an **errorlevel** of zero.</span></span>

```cmd
ECHO The current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> <span data-ttu-id="26e3a-139">In Visual Studio de **naar uitvoermap kopiëren** eigenschap voor het starten van de batch-bestand moet worden ingesteld op **kopie altijd** om ervoor te zorgen dat uw batchbestand opstarten goed aan uw project op Azure (wordtgeïmplementeerd**approot\\bin** voor Web-rollen en **approot** voor werkrollen).</span><span class="sxs-lookup"><span data-stu-id="26e3a-139">In Visual Studio, the **Copy to Output Directory** property for your startup batch file should be set to **Copy Always** to be sure that your startup batch file is properly deployed to your project on Azure (**approot\\bin** for Web roles, and **approot** for worker roles).</span></span>
> 
> 

## <a name="description-of-task-attributes"></a><span data-ttu-id="26e3a-140">Beschrijving van de kenmerken van de taak</span><span class="sxs-lookup"><span data-stu-id="26e3a-140">Description of task attributes</span></span>
<span data-ttu-id="26e3a-141">De volgende beschrijft de kenmerken van de **taak** -element in de [ServiceDefinition.csdef] bestand:</span><span class="sxs-lookup"><span data-stu-id="26e3a-141">The following describes the attributes of the **Task** element in the [ServiceDefinition.csdef] file:</span></span>

<span data-ttu-id="26e3a-142">**commandLine** -Hiermee wordt de opdrachtregel voor de taak starten:</span><span class="sxs-lookup"><span data-stu-id="26e3a-142">**commandLine** - Specifies the command line for the startup task:</span></span>

* <span data-ttu-id="26e3a-143">De opdracht met optionele opdrachtregelparameters, het starten van de taak wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="26e3a-143">The command, with optional command line parameters, which begins the startup task.</span></span>
* <span data-ttu-id="26e3a-144">Dit is vaak de bestandsnaam van een batchbestand .cmd of .bat.</span><span class="sxs-lookup"><span data-stu-id="26e3a-144">Frequently this is the filename of a .cmd or .bat batch file.</span></span>
* <span data-ttu-id="26e3a-145">De taak is ten opzichte van de AppRoot\\Bin-map voor de implementatie.</span><span class="sxs-lookup"><span data-stu-id="26e3a-145">The task is relative to the AppRoot\\Bin folder for the deployment.</span></span> <span data-ttu-id="26e3a-146">Omgevingsvariabelen worden niet aangevuld bij het bepalen van het pad en de bestandsnaam van de taak.</span><span class="sxs-lookup"><span data-stu-id="26e3a-146">Environment variables are not expanded in determining the path and file of the task.</span></span> <span data-ttu-id="26e3a-147">Als uitbreiding van de omgeving vereist is, kunt u een kleine CMD-script waarmee het starten van de taak wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="26e3a-147">If environment expansion is required, you can create a small .cmd script that calls your startup task.</span></span>
* <span data-ttu-id="26e3a-148">Kan dit een consoletoepassing of een batchbestand dat begint een [PowerShell-script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span><span class="sxs-lookup"><span data-stu-id="26e3a-148">Can be a console application or a batch file that starts a [PowerShell script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span></span>

<span data-ttu-id="26e3a-149">**executionContext** -Hiermee geeft u op het niveau van bevoegdheden voor het starten van de taak.</span><span class="sxs-lookup"><span data-stu-id="26e3a-149">**executionContext** - Specifies the privilege level for the startup task.</span></span> <span data-ttu-id="26e3a-150">Het niveau van bevoegdheden kan worden beperkt of met verhoogde bevoegdheden:</span><span class="sxs-lookup"><span data-stu-id="26e3a-150">The privilege level can be limited or elevated:</span></span>

* <span data-ttu-id="26e3a-151">**beperkt**</span><span class="sxs-lookup"><span data-stu-id="26e3a-151">**limited**</span></span>  
  <span data-ttu-id="26e3a-152">Het starten van de taak wordt uitgevoerd met dezelfde bevoegdheden als de rol.</span><span class="sxs-lookup"><span data-stu-id="26e3a-152">The startup task runs with the same privileges as the role.</span></span> <span data-ttu-id="26e3a-153">Wanneer de **executionContext** kenmerk voor de [Runtime] element is ook **beperkt**, en vervolgens de gebruiker heeft bevoegdheden die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="26e3a-153">When the **executionContext** attribute for the [Runtime] element is also **limited**, then user privileges are used.</span></span>
* <span data-ttu-id="26e3a-154">**verhoogde**</span><span class="sxs-lookup"><span data-stu-id="26e3a-154">**elevated**</span></span>  
  <span data-ttu-id="26e3a-155">Het starten van de taak wordt uitgevoerd met administrator-bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="26e3a-155">The startup task runs with administrator privileges.</span></span> <span data-ttu-id="26e3a-156">Dit kan taken starten van de programma's installeren, IIS-configuratie wijzigen, voert u wijzigingen in het register en andere taken van de administrator-niveau zonder te verhogen van de bevoegdheden van de rol zelf.</span><span class="sxs-lookup"><span data-stu-id="26e3a-156">This allows startup tasks to install programs, make IIS configuration changes, perform registry changes, and other administrator level tasks, without increasing the privilege level of the role itself.</span></span>  

> [!NOTE]
> <span data-ttu-id="26e3a-157">De bevoegdheden van een taak starten hoeft niet dezelfde zijn als de rol zelf.</span><span class="sxs-lookup"><span data-stu-id="26e3a-157">The privilege level of a startup task does not need to be the same as the role itself.</span></span>
> 
> 

<span data-ttu-id="26e3a-158">**taskType** -geeft aan hoe een starten van de taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="26e3a-158">**taskType** - Specifies the way a startup task is executed.</span></span>

* <span data-ttu-id="26e3a-159">**eenvoudige**</span><span class="sxs-lookup"><span data-stu-id="26e3a-159">**simple**</span></span>  
  <span data-ttu-id="26e3a-160">Taken worden uitgevoerd, synchroon, één voor één, in de volgorde die is opgegeven in de [ServiceDefinition.csdef] bestand.</span><span class="sxs-lookup"><span data-stu-id="26e3a-160">Tasks are executed synchronously, one at a time, in the order specified in the [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="26e3a-161">Wanneer een **eenvoudige** opstarttaak eindigt met een **errorlevel** is aan nul, de volgende **eenvoudige** starten van de taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="26e3a-161">When one **simple** startup task ends with an **errorlevel** of zero, the next **simple** startup task is executed.</span></span> <span data-ttu-id="26e3a-162">Als er niet meer **eenvoudige** starten van de taken worden uitgevoerd, en vervolgens de rol zelf wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="26e3a-162">If there are no more **simple** startup tasks to execute, then the role itself will be started.</span></span>   
  
  > [!NOTE]
  > <span data-ttu-id="26e3a-163">Als de **eenvoudige** taak eindigt met een niet-nul **errorlevel**, het exemplaar wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="26e3a-163">If the **simple** task ends with a non-zero **errorlevel**, the instance will be blocked.</span></span> <span data-ttu-id="26e3a-164">Daaropvolgende **eenvoudige** starten van de taken en de rol zelf, kunnen niet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="26e3a-164">Subsequent **simple** startup tasks, and the role itself, will not start.</span></span>
  > 
  > 
  
    <span data-ttu-id="26e3a-165">Om ervoor te zorgen dat uw batchbestand met eindigt een **errorlevel** is aan nul, geef dan de opdracht `EXIT /B 0` aan het einde van uw batch-bestand.</span><span class="sxs-lookup"><span data-stu-id="26e3a-165">To ensure that your batch file ends with an **errorlevel** of zero, execute the command `EXIT /B 0` at the end of your batch file process.</span></span>
* <span data-ttu-id="26e3a-166">**achtergrond**</span><span class="sxs-lookup"><span data-stu-id="26e3a-166">**background**</span></span>  
  <span data-ttu-id="26e3a-167">Taken worden in combinatie met het starten van de rol van asynchroon uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="26e3a-167">Tasks are executed asynchronously, in parallel with the startup of the role.</span></span>
* <span data-ttu-id="26e3a-168">**voorgrond**</span><span class="sxs-lookup"><span data-stu-id="26e3a-168">**foreground**</span></span>  
  <span data-ttu-id="26e3a-169">Taken worden in combinatie met het starten van de rol van asynchroon uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="26e3a-169">Tasks are executed asynchronously, in parallel with the startup of the role.</span></span> <span data-ttu-id="26e3a-170">Het belangrijkste verschil tussen een **voorgrond** en een **achtergrond** taak is dat een **voorgrond** taak voorkomt u dat de rol van recycling of afgesloten totdat de taak is beëindigd.</span><span class="sxs-lookup"><span data-stu-id="26e3a-170">The key difference between a **foreground** and a **background** task is that a **foreground** task prevents the role from recycling or shutting down until the task has ended.</span></span> <span data-ttu-id="26e3a-171">De **achtergrond** taken beschikt niet over deze beperking.</span><span class="sxs-lookup"><span data-stu-id="26e3a-171">The **background** tasks do not have this restriction.</span></span>

## <a name="environment-variables"></a><span data-ttu-id="26e3a-172">Omgevingsvariabelen</span><span class="sxs-lookup"><span data-stu-id="26e3a-172">Environment variables</span></span>
<span data-ttu-id="26e3a-173">Omgevingsvariabelen zijn een manier om informatie doorgeven aan een taak starten.</span><span class="sxs-lookup"><span data-stu-id="26e3a-173">Environment variables are a way to pass information to a startup task.</span></span> <span data-ttu-id="26e3a-174">Bijvoorbeeld, kunt u het pad naar een blob met een programma te installeren, of poortnummers die door uw rol wordt gebruikt of instellingen voor de functies van de taak starten van de plaatsen.</span><span class="sxs-lookup"><span data-stu-id="26e3a-174">For example, you can put the path to a blob that contains a program to install, or port numbers that your role will use, or settings to control features of your startup task.</span></span>

<span data-ttu-id="26e3a-175">Er zijn twee soorten van omgevingsvariabelen voor starten van de taken. statische omgevingsvariabelen en omgevingsvariabelen op basis van de leden van de [ RoleEnvironment] klasse.</span><span class="sxs-lookup"><span data-stu-id="26e3a-175">There are two kinds of environment variables for startup tasks; static environment variables and environment variables based on members of the [RoleEnvironment] class.</span></span> <span data-ttu-id="26e3a-176">Beide zijn de [omgeving] sectie van de [ServiceDefinition.csdef] bestands- en beide gebruik de [variabele] element en **naam** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="26e3a-176">Both are in the [Environment] section of the [ServiceDefinition.csdef] file, and both use the [Variable] element and **name** attribute.</span></span>

<span data-ttu-id="26e3a-177">Maakt gebruik van statische omgevingsvariabelen de **waarde** kenmerk van de [variabele] element.</span><span class="sxs-lookup"><span data-stu-id="26e3a-177">Static environment variables uses the **value** attribute of the [Variable] element.</span></span> <span data-ttu-id="26e3a-178">Het bovenstaande voorbeeld maakt de omgevingsvariabele **MyVersionNumber** die een vaste waarde heeft van '**1.0.0.0**'.</span><span class="sxs-lookup"><span data-stu-id="26e3a-178">The example above creates the environment variable **MyVersionNumber** which has a static value of "**1.0.0.0**".</span></span> <span data-ttu-id="26e3a-179">Een ander voorbeeld is voor het maken een **StagingOrProduction** omgevingsvariabele die u handmatig op waarden van instellen kunt '**fasering**"of"**productie**' uit te voeren starten van de verschillende acties op basis van de waarde van de **StagingOrProduction** omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="26e3a-179">Another example would be to create a **StagingOrProduction** environment variable which you can manually set to values of "**staging**" or "**production**" to perform different startup actions based on the value of the **StagingOrProduction** environment variable.</span></span>

<span data-ttu-id="26e3a-180">Gebruik geen omgevingsvariabelen op basis van de leden van de klasse RoleEnvironment de **waarde** kenmerk van de [variabele] element.</span><span class="sxs-lookup"><span data-stu-id="26e3a-180">Environment variables based on members of the RoleEnvironment class do not use the **value** attribute of the [Variable] element.</span></span> <span data-ttu-id="26e3a-181">In plaats daarvan de [RoleInstanceValue] onderliggend element met de juiste **XPath** kenmerkwaarde, worden gebruikt om het maken van een omgevingsvariabele op basis van een specifiek lid van de [ RoleEnvironment] klasse.</span><span class="sxs-lookup"><span data-stu-id="26e3a-181">Instead, the [RoleInstanceValue] child element, with the appropriate **XPath** attribute value, are used to create an environment variable based on a specific member of the [RoleEnvironment] class.</span></span> <span data-ttu-id="26e3a-182">Waarden voor de **XPath** kenmerk voor toegang tot verschillende [ RoleEnvironment] waarden kunt u vinden [hier](cloud-services-role-config-xpath.md).</span><span class="sxs-lookup"><span data-stu-id="26e3a-182">Values for the **XPath** attribute to access various [RoleEnvironment] values can be found [here](cloud-services-role-config-xpath.md).</span></span>

<span data-ttu-id="26e3a-183">Om bijvoorbeeld te maken van een omgevingsvariabele die is '**true**' wanneer het exemplaar wordt uitgevoerd in de rekenemulator en '**false**' wanneer in de cloud wordt uitgevoerd, gebruikt u de volgende [variabele] en [RoleInstanceValue] elementen:</span><span class="sxs-lookup"><span data-stu-id="26e3a-183">For example, to create an environment variable that is "**true**" when the instance is running in the compute emulator, and "**false**" when running in the cloud, use the following [Variable] and [RoleInstanceValue] elements:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create the environment variable that informs the startup task whether it is running
                in the Compute Emulator or in the cloud. "%ComputeEmulatorRunning%"=="true" when
                running in the Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in the cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a><span data-ttu-id="26e3a-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="26e3a-184">Next steps</span></span>
<span data-ttu-id="26e3a-185">Meer informatie over het uitvoeren van sommige [algemene beheertaken voor opstarten](cloud-services-startup-tasks-common.md) met de Cloudservice.</span><span class="sxs-lookup"><span data-stu-id="26e3a-185">Learn how to perform some [common startup tasks](cloud-services-startup-tasks-common.md) with your Cloud Service.</span></span>

<span data-ttu-id="26e3a-186">[Pakket](cloud-services-model-and-package.md) uw Cloudservice.</span><span class="sxs-lookup"><span data-stu-id="26e3a-186">[Package](cloud-services-model-and-package.md) your Cloud Service.</span></span>  

<span data-ttu-id="26e3a-187">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span><span class="sxs-lookup"><span data-stu-id="26e3a-187">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span></span>
<span data-ttu-id="26e3a-188">[taak]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span><span class="sxs-lookup"><span data-stu-id="26e3a-188">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span></span>
<span data-ttu-id="26e3a-189">[opstarten]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup</span><span class="sxs-lookup"><span data-stu-id="26e3a-189">[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup</span></span>
<span data-ttu-id="26e3a-190">[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime</span><span class="sxs-lookup"><span data-stu-id="26e3a-190">[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime</span></span>
<span data-ttu-id="26e3a-191">[omgeving]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span><span class="sxs-lookup"><span data-stu-id="26e3a-191">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span></span>
<span data-ttu-id="26e3a-192">[variabele]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span><span class="sxs-lookup"><span data-stu-id="26e3a-192">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span></span>
<span data-ttu-id="26e3a-193">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="26e3a-193">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
<span data-ttu-id="26e3a-194">[ RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx</span><span class="sxs-lookup"><span data-stu-id="26e3a-194">[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx</span></span>
