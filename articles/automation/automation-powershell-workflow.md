---
title: Leren van PowerShell-werkstroom voor Azure Automation | Microsoft Docs
description: In dit artikel is bedoeld als een snelle les voor auteurs bekend zijn met PowerShell om te weten over de specifieke verschillen tussen PowerShell en PowerShell-werkstroom en concepten die van toepassing op de Automation-runbooks.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 84bf133e-5343-4e0e-8d6c-bb14304a70db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 4de812c7f863e42a6ed10c2312d61b8377e06431
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a><span data-ttu-id="67cfe-103">Leren van de belangrijkste concepten voor Windows PowerShell-werkstroom voor Automation-runbooks</span><span class="sxs-lookup"><span data-stu-id="67cfe-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span></span> 
<span data-ttu-id="67cfe-104">Azure Automation-Runbooks worden geïmplementeerd als Windows PowerShell-werkstromen.</span><span class="sxs-lookup"><span data-stu-id="67cfe-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span></span>  <span data-ttu-id="67cfe-105">Een Windows PowerShell-werkstroom is vergelijkbaar met een Windows PowerShell-script, maar heeft enkele belangrijke verschillen die kunnen verwarrend zijn naar een nieuwe gebruiker.</span><span class="sxs-lookup"><span data-stu-id="67cfe-105">A Windows PowerShell Workflow is similar to a Windows PowerShell script but has some significant differences that can be confusing to a new user.</span></span>  <span data-ttu-id="67cfe-106">Hoewel dit artikel is bedoeld om te schrijven met behulp van PowerShell-werkstroom runbooks, wordt u aangeraden dat u runbooks met behulp van PowerShell, tenzij u controlepunten moet schrijven.</span><span class="sxs-lookup"><span data-stu-id="67cfe-106">While this article is intended to help you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span></span>  <span data-ttu-id="67cfe-107">Er zijn verschillende syntaxisverschillen bij het ontwerpen van PowerShell Workflow-runbooks en deze verschillen vereisen iets meer werk effectieve werkstromen te schrijven.</span><span class="sxs-lookup"><span data-stu-id="67cfe-107">There are several syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work to write effective workflows.</span></span>  

<span data-ttu-id="67cfe-108">Een werkstroom is een opeenvolging van geprogrammeerde, verbonden stappen waarmee langlopende taken uitvoeren of de coördinatie vereisen van meerdere stappen op meerdere apparaten of beheerde knooppunten.</span><span class="sxs-lookup"><span data-stu-id="67cfe-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require the coordination of multiple steps across multiple devices or managed nodes.</span></span> <span data-ttu-id="67cfe-109">De voordelen van een werkstroom op een normaal script omvatten de mogelijkheid een actie tegen meerdere apparaten tegelijkertijd uitvoeren en de mogelijkheid om automatisch te herstellen van fouten.</span><span class="sxs-lookup"><span data-stu-id="67cfe-109">The benefits of a workflow over a normal script include the ability to simultaneously perform an action against multiple devices and the ability to automatically recover from failures.</span></span> <span data-ttu-id="67cfe-110">Een Windows PowerShell-werkstroom is een Windows PowerShell-script dat gebruikmaakt van Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="67cfe-110">A Windows PowerShell Workflow is a Windows PowerShell script that uses Windows Workflow Foundation.</span></span> <span data-ttu-id="67cfe-111">Terwijl de werkstroom is geschreven met Windows PowerShell-syntaxis en gelanceerd door Windows PowerShell, wordt deze verwerkt door Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="67cfe-111">While the workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span></span>

<span data-ttu-id="67cfe-112">Zie voor meer informatie over de onderwerpen in dit artikel [aan de slag met Windows PowerShell-werkstroom](http://technet.microsoft.com/library/jj134242.aspx).</span><span class="sxs-lookup"><span data-stu-id="67cfe-112">For complete details on the topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span></span>

## <a name="basic-structure-of-a-workflow"></a><span data-ttu-id="67cfe-113">Algemene structuur van een werkstroom</span><span class="sxs-lookup"><span data-stu-id="67cfe-113">Basic structure of a workflow</span></span>
<span data-ttu-id="67cfe-114">De eerste stap bij het converteren van een PowerShell-script naar een PowerShell-werkstroom is insluitende deze met de **werkstroom** sleutelwoord.</span><span class="sxs-lookup"><span data-stu-id="67cfe-114">The first step to converting a PowerShell script to a PowerShell workflow is enclosing it with the **Workflow** keyword.</span></span>  <span data-ttu-id="67cfe-115">Een werkstroom begint met de **werkstroom** trefwoord gevolgd door de hoofdtekst van het script tussen accolades.</span><span class="sxs-lookup"><span data-stu-id="67cfe-115">A workflow starts with the **Workflow** keyword followed by the body of the script enclosed in braces.</span></span> <span data-ttu-id="67cfe-116">De naam van de werkstroom volgt het **werkstroom** trefwoord zoals getoond in de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="67cfe-116">The name of the workflow follows the **Workflow** keyword as shown in the following syntax:</span></span>

    Workflow Test-Workflow
    {
       <Commands>
    }

<span data-ttu-id="67cfe-117">De naam van de werkstroom moet overeenkomen met de naam van het Automation-runbook.</span><span class="sxs-lookup"><span data-stu-id="67cfe-117">The name of the workflow must match the name of the Automation runbook.</span></span> <span data-ttu-id="67cfe-118">Als het runbook wordt geïmporteerd, wordt de bestandsnaam moet overeenkomen met de Werkstroomnaam en moet eindigen op *.ps1*.</span><span class="sxs-lookup"><span data-stu-id="67cfe-118">If the runbook is being imported, then the filename must match the workflow name and must end in *.ps1*.</span></span>

<span data-ttu-id="67cfe-119">U kunt parameters toevoegen aan de werkstroom met de **Param** sleutelwoord net zoals een script.</span><span class="sxs-lookup"><span data-stu-id="67cfe-119">To add parameters to the workflow, use the **Param** keyword just as you would to a script.</span></span>

## <a name="code-changes"></a><span data-ttu-id="67cfe-120">Codewijzigingen</span><span class="sxs-lookup"><span data-stu-id="67cfe-120">Code changes</span></span>
<span data-ttu-id="67cfe-121">PowerShell-werkstroom code ziet er bijna identiek aan de code van de PowerShell-script, met uitzondering van enkele belangrijke wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="67cfe-121">PowerShell workflow code looks almost identical to PowerShell script code except for a few significant changes.</span></span>  <span data-ttu-id="67cfe-122">De volgende secties worden de wijzigingen die u moet aanbrengen in een PowerShell-script voor het in een werkstroom uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="67cfe-122">The following sections describe changes that you need to make to a PowerShell script for it to run in a workflow.</span></span>

### <a name="activities"></a><span data-ttu-id="67cfe-123">Activiteiten</span><span class="sxs-lookup"><span data-stu-id="67cfe-123">Activities</span></span>
<span data-ttu-id="67cfe-124">Een activiteit is een specifieke taak in een werkstroom.</span><span class="sxs-lookup"><span data-stu-id="67cfe-124">An activity is a specific task in a workflow.</span></span> <span data-ttu-id="67cfe-125">Net zoals een script uit een of meer opdrachten bestaat, bestaat een werkstroom uit een of meer activiteiten die worden uitgevoerd in een reeks.</span><span class="sxs-lookup"><span data-stu-id="67cfe-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span></span> <span data-ttu-id="67cfe-126">Windows PowerShell-werkstroom converteert automatisch veel van de Windows PowerShell-cmdlets voor activiteiten tijdens het uitvoeren van een werkstroom.</span><span class="sxs-lookup"><span data-stu-id="67cfe-126">Windows PowerShell Workflow automatically converts many of the Windows PowerShell cmdlets to activities when it runs a workflow.</span></span> <span data-ttu-id="67cfe-127">Wanneer u een van deze cmdlets in uw runbook opgeeft, wordt de bijbehorende activiteit uitgevoerd door Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="67cfe-127">When you specify one of these cmdlets in your runbook, the corresponding activity is run by Windows Workflow Foundation.</span></span> <span data-ttu-id="67cfe-128">Voor die cmdlets zonder een bijbehorende activiteit Windows PowerShell Workflow voert automatisch de cmdlet uit binnen een [InlineScript](#inlinescript) activiteit.</span><span class="sxs-lookup"><span data-stu-id="67cfe-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs the cmdlet within an [InlineScript](#inlinescript) activity.</span></span> <span data-ttu-id="67cfe-129">Er is een set cmdlets die zijn uitgesloten en kan niet worden gebruikt in een werkstroom, tenzij u ze expliciet in een InlineScript blok opneemt.</span><span class="sxs-lookup"><span data-stu-id="67cfe-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span></span> <span data-ttu-id="67cfe-130">Zie voor meer informatie over deze begrippen [met behulp van activiteiten in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span><span class="sxs-lookup"><span data-stu-id="67cfe-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span></span>

<span data-ttu-id="67cfe-131">Werkstroomactiviteiten delen een set met algemene parameters voor het configureren van hun werking.</span><span class="sxs-lookup"><span data-stu-id="67cfe-131">Workflow activities share a set of common parameters to configure their operation.</span></span> <span data-ttu-id="67cfe-132">Zie voor meer informatie over de algemene werkstroomparameters [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="67cfe-132">For details about the workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="positional-parameters"></a><span data-ttu-id="67cfe-133">Positionele parameters</span><span class="sxs-lookup"><span data-stu-id="67cfe-133">Positional parameters</span></span>
<span data-ttu-id="67cfe-134">U kunt positieparameters niet gebruiken met activiteiten en cmdlets in een werkstroom.</span><span class="sxs-lookup"><span data-stu-id="67cfe-134">You can't use positional parameters with activities and cmdlets in a workflow.</span></span>  <span data-ttu-id="67cfe-135">Dit betekent dat is dat u de namen van parameters moet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="67cfe-135">All this means is that you must use parameter names.</span></span>

<span data-ttu-id="67cfe-136">Neem bijvoorbeeld de volgende code waarmee alle actieve services opgehaald.</span><span class="sxs-lookup"><span data-stu-id="67cfe-136">For example, consider the following code that gets all running services.</span></span>

     Get-Service | Where-Object {$_.Status -eq "Running"}

<span data-ttu-id="67cfe-137">Als u deze code in een werkstroom uitvoert probeert, ontvangt u een bericht zoals "parameterset kan niet worden omgezet met behulp van de opgegeven benoemde parameters."</span><span class="sxs-lookup"><span data-stu-id="67cfe-137">If you try to run this same code in a workflow, you receive a message like "Parameter set cannot be resolved using the specified named parameters."</span></span>  <span data-ttu-id="67cfe-138">Geef de parameternaam zoals in het volgende om dit te corrigeren.</span><span class="sxs-lookup"><span data-stu-id="67cfe-138">To correct this, provide the parameter name as in the following.</span></span>

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a><span data-ttu-id="67cfe-139">Gedeserialiseerde objecten</span><span class="sxs-lookup"><span data-stu-id="67cfe-139">Deserialized objects</span></span>
<span data-ttu-id="67cfe-140">Objecten in werkstromen worden gedeserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="67cfe-140">Objects in workflows are deserialized.</span></span>  <span data-ttu-id="67cfe-141">Dit betekent dat de eigenschappen zijn nog steeds beschikbaar, maar niet de methoden.</span><span class="sxs-lookup"><span data-stu-id="67cfe-141">This means that their properties are still available, but not their methods.</span></span>  <span data-ttu-id="67cfe-142">Neem bijvoorbeeld de volgende PowerShell-code die een service met de methode stoppen van het object van de Service wordt gestopt.</span><span class="sxs-lookup"><span data-stu-id="67cfe-142">For example, consider the following PowerShell code that stops a service using the Stop method of the Service object.</span></span>

    $Service = Get-Service -Name MyService
    $Service.Stop()

<span data-ttu-id="67cfe-143">Als u uitvoeren in een werkstroom wilt, ontvangt u een foutmelding verschijnt "de methodeaanroep wordt niet ondersteund in een Windows PowerShell-werkstroom."</span><span class="sxs-lookup"><span data-stu-id="67cfe-143">If you try to run this in a workflow, you receive an error saying "Method invocation is not supported in a Windows PowerShell Workflow."</span></span>  

<span data-ttu-id="67cfe-144">Een mogelijkheid is het inpakken van deze twee regels code in een [InlineScript](#inlinescript) blokkeren in dat geval $Service een serviceobject in het blok is.</span><span class="sxs-lookup"><span data-stu-id="67cfe-144">One option is to wrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within the block.</span></span>

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

<span data-ttu-id="67cfe-145">Een andere optie is het gebruik van een andere cmdlet die dezelfde functionaliteit als de methode uitvoert als deze beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="67cfe-145">Another option is to use another cmdlet that performs the same functionality as the method, if one is available.</span></span>  <span data-ttu-id="67cfe-146">In ons voorbeeld de cmdlet Stop-Service biedt dezelfde functionaliteit als de methode stoppen en u kunt het volgende gebruiken voor een werkstroom.</span><span class="sxs-lookup"><span data-stu-id="67cfe-146">In our sample, the Stop-Service cmdlet provides the same functionality as the Stop method, and you could use the following for a workflow.</span></span>

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a><span data-ttu-id="67cfe-147">InlineScript</span><span class="sxs-lookup"><span data-stu-id="67cfe-147">InlineScript</span></span>
<span data-ttu-id="67cfe-148">De **InlineScript** activiteit is handig wanneer u een of meer opdrachten uitvoeren als traditionele PowerShell-script in plaats van PowerShell-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="67cfe-148">The **InlineScript** activity is useful when you need to run one or more commands as traditional PowerShell script instead of PowerShell workflow.</span></span>  <span data-ttu-id="67cfe-149">Terwijl de opdrachten in een werkstroom voor verwerking naar de Windows Workflow Foundation worden verzonden, worden door Windows PowerShell-opdrachten in een InlineScript-blok verwerkt.</span><span class="sxs-lookup"><span data-stu-id="67cfe-149">While commands in a workflow are sent to Windows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span></span>

<span data-ttu-id="67cfe-150">InlineScript gebruikt van de volgende syntaxis hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="67cfe-150">InlineScript uses the following syntax shown below.</span></span>

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

<span data-ttu-id="67cfe-151">Uitvoer kunt van een InlineScript u terugkeren door de uitvoer toe te wijzen aan een variabele.</span><span class="sxs-lookup"><span data-stu-id="67cfe-151">You can return output from an InlineScript by assigning the output to a variable.</span></span> <span data-ttu-id="67cfe-152">Het volgende voorbeeld een service stopt en vervolgens de naam van de service levert.</span><span class="sxs-lookup"><span data-stu-id="67cfe-152">The following example stops a service and then outputs the service name.</span></span>

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="67cfe-153">U kunt waarden doorgeven in een InlineScript-blok, maar moet u **$Using** bereikaanpassingsfunctie.</span><span class="sxs-lookup"><span data-stu-id="67cfe-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span></span>  <span data-ttu-id="67cfe-154">Het volgende voorbeeld is identiek aan het vorige voorbeeld, behalve dat de servicenaam is opgegeven door een variabele.</span><span class="sxs-lookup"><span data-stu-id="67cfe-154">The following example is identical to the previous example except that the service name is provided by a variable.</span></span>

    Workflow Stop-MyService
    {
        $ServiceName = "MyService"

        $Output = InlineScript {
            $Service = Get-Service -Name $Using:ServiceName
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="67cfe-155">Tijdens het InlineScript-activiteiten mogelijk kritieke in bepaalde werkstromen, ze bieden geen ondersteuning voor werkstroom constructies en mag alleen worden gebruikt wanneer dat nodig is om de volgende redenen:</span><span class="sxs-lookup"><span data-stu-id="67cfe-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for the following reasons:</span></span>

* <span data-ttu-id="67cfe-156">U kunt geen gebruiken [controlepunten](#checkpoints) in een InlineScript-blok.</span><span class="sxs-lookup"><span data-stu-id="67cfe-156">You cannot use [checkpoints](#checkpoints) inside an InlineScript block.</span></span> <span data-ttu-id="67cfe-157">Als er een fout optreedt in het blok, moet het worden hervat vanaf het begin van het blok.</span><span class="sxs-lookup"><span data-stu-id="67cfe-157">If a failure occurs within the block, it must be resumed from the beginning of the block.</span></span>
* <span data-ttu-id="67cfe-158">U kunt geen gebruiken [parallelle uitvoering](#parallel-processing) binnen een InlineScriptBlock.</span><span class="sxs-lookup"><span data-stu-id="67cfe-158">You cannot use [parallel execution](#parallel-processing) inside an InlineScriptBlock.</span></span>
* <span data-ttu-id="67cfe-159">InlineScript dit beïnvloedt de schaalbaarheid van de werkstroom omdat deze de Windows PowerShell-sessie voor de hele lengte van het InlineScript-blok bevat.</span><span class="sxs-lookup"><span data-stu-id="67cfe-159">InlineScript affects scalability of the workflow since it holds the Windows PowerShell session for the entire length of the InlineScript block.</span></span>

<span data-ttu-id="67cfe-160">Zie voor meer informatie over het gebruik van InlineScript [Windows PowerShell-opdrachten in een werkstroom](http://technet.microsoft.com/library/jj574197.aspx) en [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span><span class="sxs-lookup"><span data-stu-id="67cfe-160">For more information on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span></span>

## <a name="parallel-processing"></a><span data-ttu-id="67cfe-161">Parallelle verwerking</span><span class="sxs-lookup"><span data-stu-id="67cfe-161">Parallel processing</span></span>
<span data-ttu-id="67cfe-162">Een voordeel van het Windows PowerShell-werkstromen is de mogelijkheid voor het uitvoeren van een reeks opdrachten parallel in plaats van opeenvolgend net als bij een typische script.</span><span class="sxs-lookup"><span data-stu-id="67cfe-162">One advantage of Windows PowerShell Workflows is the ability to perform a set of commands in parallel instead of sequentially as with a typical script.</span></span>

<span data-ttu-id="67cfe-163">U kunt de **parallelle** sleutelwoord voor het maken van een scriptblok is opgegeven met meerdere opdrachten die gelijktijdig worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="67cfe-163">You can use the **Parallel** keyword to create a script block with multiple commands that run concurrently.</span></span> <span data-ttu-id="67cfe-164">Dit maakt gebruik van de volgende syntaxis hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="67cfe-164">This uses the following syntax shown below.</span></span> <span data-ttu-id="67cfe-165">In dit geval starten activiteit1 en activiteit2 op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="67cfe-165">In this case, Activity1 and Activity2 starts at the same time.</span></span> <span data-ttu-id="67cfe-166">Activiteit3 start pas als zowel activiteit1 en activiteit2 zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="67cfe-166">Activity3 starts only after both Activity1 and Activity2 have completed.</span></span>

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


<span data-ttu-id="67cfe-167">Neem bijvoorbeeld het volgende PowerShell-opdrachten die meerdere bestanden naar een netwerkbestemming kopiëren.</span><span class="sxs-lookup"><span data-stu-id="67cfe-167">For example, consider the following PowerShell commands that copy multiple files to a network destination.</span></span>  <span data-ttu-id="67cfe-168">Deze opdrachten worden opeenvolgend uitgevoerd zodanig dat één bestand met het kopiëren eindigen moet voordat de volgende wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="67cfe-168">These commands are run sequentially so that one file must finish copying before the next is started.</span></span>     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

<span data-ttu-id="67cfe-169">De volgende werkstroom wordt deze opdrachten parallel uitgevoerd, zodat ze allemaal op hetzelfde moment kopiëren starten.</span><span class="sxs-lookup"><span data-stu-id="67cfe-169">The following workflow runs these same commands in parallel so that they all start copying at the same time.</span></span>  <span data-ttu-id="67cfe-170">Pas nadat ze alle zijn wordt gekopieerd het voltooiingsbericht is weergegeven.</span><span class="sxs-lookup"><span data-stu-id="67cfe-170">Only after they are all copied is the completion message displayed.</span></span>

    Workflow Copy-Files
    {
        Parallel
        {
            Copy-Item -Path "C:\LocalPath\File1.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File2.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File3.txt" -Destination "\\NetworkPath"
        }

        Write-Output "Files copied."
    }


<span data-ttu-id="67cfe-171">U kunt de **ForEach-Parallel** constructie om opdrachten proces voor elk item in een verzameling gelijktijdig te.</span><span class="sxs-lookup"><span data-stu-id="67cfe-171">You can use the **ForEach -Parallel** construct to process commands for each item in a collection concurrently.</span></span> <span data-ttu-id="67cfe-172">De items in de verzameling worden parallel verwerkt, terwijl de opdrachten in het scriptblok worden opeenvolgend uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="67cfe-172">The items in the collection are processed in parallel while the commands in the script block run sequentially.</span></span> <span data-ttu-id="67cfe-173">Dit maakt gebruik van de volgende syntaxis hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="67cfe-173">This uses the following syntax shown below.</span></span> <span data-ttu-id="67cfe-174">In dit geval starten activiteit1 op hetzelfde moment voor alle items in de verzameling.</span><span class="sxs-lookup"><span data-stu-id="67cfe-174">In this case, Activity1 starts at the same time for all items in the collection.</span></span> <span data-ttu-id="67cfe-175">Voor elk item start activiteit2 nadat activiteit1 voltooid.</span><span class="sxs-lookup"><span data-stu-id="67cfe-175">For each item, Activity2 starts after Activity1 is complete.</span></span> <span data-ttu-id="67cfe-176">Activiteit3 start pas als zowel activiteit1 en activiteit2 zijn voltooid voor alle items.</span><span class="sxs-lookup"><span data-stu-id="67cfe-176">Activity3 starts only after both Activity1 and Activity2 have completed for all items.</span></span>

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

<span data-ttu-id="67cfe-177">Het volgende voorbeeld is vergelijkbaar met het vorige voorbeeld parallel bestanden zijn gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="67cfe-177">The following example is similar to the previous example copying files in parallel.</span></span>  <span data-ttu-id="67cfe-178">In dit geval wordt een bericht weergegeven voor elk bestand nadat deze zijn gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="67cfe-178">In this case, a message is displayed for each file after it copies.</span></span>  <span data-ttu-id="67cfe-179">Pas nadat ze alle zijn volledig gekopieerd is het uiteindelijke voltooiingsbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="67cfe-179">Only after they are all completely copied is the final completion message displayed.</span></span>

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach -Parallel ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
        }

        Write-Output "All files copied."
    }

> [!NOTE]
> <span data-ttu-id="67cfe-180">We raden niet onderliggende runbooks parallel uitgevoerd, omdat dit onbetrouwbare resultaten is weergegeven.</span><span class="sxs-lookup"><span data-stu-id="67cfe-180">We do not recommend running child runbooks in parallel since this has been shown to give unreliable results.</span></span>  <span data-ttu-id="67cfe-181">De uitvoer van het onderliggende runbook soms wordt niet weergegeven en instellingen in een onderliggend runbook kunnen invloed hebben op de andere parallelle onderliggende runbooks</span><span class="sxs-lookup"><span data-stu-id="67cfe-181">The output from the child runbook sometimes does not show up, and settings in one child runbook can affect the other parallel child runbooks</span></span>
>

## <a name="checkpoints"></a><span data-ttu-id="67cfe-182">Controlepunten</span><span class="sxs-lookup"><span data-stu-id="67cfe-182">Checkpoints</span></span>
<span data-ttu-id="67cfe-183">Een *controlepunt* is een momentopname van de huidige status van de werkstroom met de huidige waarde voor variabelen en eventuele gegenereerde uitvoer naar dat punt.</span><span class="sxs-lookup"><span data-stu-id="67cfe-183">A *checkpoint* is a snapshot of the current state of the workflow that includes the current value for variables and any output generated to that point.</span></span> <span data-ttu-id="67cfe-184">Als een werkstroom in een fout eindigt of is onderbroken, wordt klikt u vervolgens de volgende keer dat deze wordt uitgevoerd gestart vanaf de laatste controlepunt in plaats van het begin van de worfklow.</span><span class="sxs-lookup"><span data-stu-id="67cfe-184">If a workflow ends in error or is suspended, then the next time it is run it will start from its last checkpoint instead of the start of the worfklow.</span></span>  <span data-ttu-id="67cfe-185">U kunt een controlepunt instellen in een werkstroom met de **Checkpoint-Workflow** activiteit.</span><span class="sxs-lookup"><span data-stu-id="67cfe-185">You can set a checkpoint in a workflow with the **Checkpoint-Workflow** activity.</span></span>

<span data-ttu-id="67cfe-186">In de volgende voorbeeldcode treedt een fout op na activiteit2 waardoor de werkstroom moet worden beëindigd.</span><span class="sxs-lookup"><span data-stu-id="67cfe-186">In the following sample code, an exception occurs after Activity2 causing the workflow to end.</span></span> <span data-ttu-id="67cfe-187">Wanneer de werkstroom opnieuw wordt uitgevoerd, wordt er door het uitvoeren van activiteit2 aangezien dit vlak nadat het laatste controlepunt instellen is gestart.</span><span class="sxs-lookup"><span data-stu-id="67cfe-187">When the workflow is run again, it starts by running Activity2 since this was just after the last checkpoint set.</span></span>

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

<span data-ttu-id="67cfe-188">U moet controlepunten in een werkstroom instellen na activiteiten die foutgevoelig uitzondering zijn en mag geen herhaalde als de werkstroom wordt hervat.</span><span class="sxs-lookup"><span data-stu-id="67cfe-188">You should set checkpoints in a workflow after activities that may be prone to exception and should not be repeated if the workflow is resumed.</span></span> <span data-ttu-id="67cfe-189">De werkstroom kan bijvoorbeeld een virtuele machine maken.</span><span class="sxs-lookup"><span data-stu-id="67cfe-189">For example, your workflow may create a virtual machine.</span></span> <span data-ttu-id="67cfe-190">U kunt een controlepunt instellen, zowel voor en na de opdrachten voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="67cfe-190">You could set a checkpoint both before and after the commands to create the virtual machine.</span></span> <span data-ttu-id="67cfe-191">Als het aanmaken mislukt, zou klikt u vervolgens de opdrachten worden herhaald als de werkstroom opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="67cfe-191">If the creation fails, then the commands would be repeated if the workflow is started again.</span></span> <span data-ttu-id="67cfe-192">Als de worfklow mislukt nadat de aanmaak slaagt, wordt klikt u vervolgens de virtuele machine niet opnieuw worden gemaakt wanneer de werkstroom wordt hervat.</span><span class="sxs-lookup"><span data-stu-id="67cfe-192">If the worfklow fails after the creation succeeds, then the virtual machine will not be created again when the workflow is resumed.</span></span>

<span data-ttu-id="67cfe-193">Het volgende voorbeeld worden meerdere bestanden gekopieerd naar een netwerklocatie en stelt een controlepunt na elk bestand.</span><span class="sxs-lookup"><span data-stu-id="67cfe-193">The following example copies multiple files to a network location and sets a checkpoint after each file.</span></span>  <span data-ttu-id="67cfe-194">Als de netwerklocatie verbroken wordt, klikt u vervolgens beëindigd de werkstroom in fout.</span><span class="sxs-lookup"><span data-stu-id="67cfe-194">If the network location is lost, then the workflow ends in error.</span></span>  <span data-ttu-id="67cfe-195">Wanneer opnieuw wordt gestart, wordt deze hervat op het laatste controlepunt, wat betekent dat alleen de bestanden die al is gekopieerd worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="67cfe-195">When it is started again, it will resume at the last checkpoint meaning that only the files that have already been copied are skipped.</span></span>

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
            Checkpoint-Workflow
        }

        Write-Output "All files copied."
    }

<span data-ttu-id="67cfe-196">Omdat de username-verwijzingen zijn niet permanent opgeslagen nadat u de [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activiteit of na het laatste controlepunt, moet u de referenties die null zijn en halen ze vervolgens opnieuw uit de store asset na instellen  **Suspend-Workflow** of controlepunt wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="67cfe-196">Because username credentials are not persisted after you call the [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after the last checkpoint, you need to set the credentials to null and then retrieve them again from the asset store after **Suspend-Workflow** or checkpoint is called.</span></span>  <span data-ttu-id="67cfe-197">Anders wordt het volgende foutbericht weergegeven: *de werkstroomtaak kan niet worden hervat, ofwel omdat persistentie gegevens kan niet worden opgeslagen volledig of opgeslagen gegevens persistentie is beschadigd. U moet de werkstroom opnieuw.*</span><span class="sxs-lookup"><span data-stu-id="67cfe-197">Otherwise, you may receive the following error message: *The workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart the workflow.*</span></span>

<span data-ttu-id="67cfe-198">De volgende dezelfde code laat zien hoe dit in uw PowerShell Workflow-runbooks te verwerken.</span><span class="sxs-lookup"><span data-stu-id="67cfe-198">The following same code demonstrates how to handle this in your PowerShell Workflow runbooks.</span></span>

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first to create the VM (code not shown)

          # Now add the VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


<span data-ttu-id="67cfe-199">Dit is niet vereist als u zich verifiëren met behulp van een Run As-account geconfigureerd met een service-principal.</span><span class="sxs-lookup"><span data-stu-id="67cfe-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span></span>  

<span data-ttu-id="67cfe-200">Zie voor meer informatie over controlepunten [controlepunten toevoegen aan een Scriptwerkstroom](http://technet.microsoft.com/library/jj574114.aspx).</span><span class="sxs-lookup"><span data-stu-id="67cfe-200">For more information about checkpoints, see [Adding Checkpoints to a Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="67cfe-201">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="67cfe-201">Next steps</span></span>
* <span data-ttu-id="67cfe-202">Zie [Mijn eerste PowerShell Workflow-runbook](automation-first-runbook-textual.md) om aan de slag te gaan met PowerShell Workflow-runbooks</span><span class="sxs-lookup"><span data-stu-id="67cfe-202">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
