---
title: aaaLearning PowerShell-werkstroom voor Azure Automation | Microsoft Docs
description: In dit artikel is bedoeld als een snelle les voor auteurs bekend bent met PowerShell toounderstand Hallo specifieke verschillen tussen PowerShell en PowerShell-werkstroom en concepten van toepassing tooAutomation runbooks.
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
ms.openlocfilehash: 362c504eb96d31b99a826b128e6a591beecaa084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a><span data-ttu-id="02508-103">Leren van de belangrijkste concepten voor Windows PowerShell-werkstroom voor Automation-runbooks</span><span class="sxs-lookup"><span data-stu-id="02508-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span></span> 
<span data-ttu-id="02508-104">Azure Automation-Runbooks worden geïmplementeerd als Windows PowerShell-werkstromen.</span><span class="sxs-lookup"><span data-stu-id="02508-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span></span>  <span data-ttu-id="02508-105">Een Windows PowerShell-werkstroom is vergelijkbaar tooa Windows PowerShell-script, maar heeft enkele belangrijke verschillen die verwarrend tooa nieuwe gebruiker worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="02508-105">A Windows PowerShell Workflow is similar tooa Windows PowerShell script but has some significant differences that can be confusing tooa new user.</span></span>  <span data-ttu-id="02508-106">In dit artikel is bedoeld toohelp schrijven van runbooks met behulp van PowerShell workflow, wordt u aangeraden dat u runbooks met behulp van PowerShell, tenzij u controlepunten moet schrijven.</span><span class="sxs-lookup"><span data-stu-id="02508-106">While this article is intended toohelp you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span></span>  <span data-ttu-id="02508-107">Er zijn verschillende syntaxisverschillen bij het ontwerpen van PowerShell Workflow-runbooks en deze verschillen vereisen iets meer werk toowrite effectieve workflows.</span><span class="sxs-lookup"><span data-stu-id="02508-107">There are several syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work toowrite effective workflows.</span></span>  

<span data-ttu-id="02508-108">Een werkstroom is een opeenvolging van geprogrammeerde, verbonden stappen waarmee langlopende taken uitvoeren of Hallo coördinatie van meerdere stappen vereisen op meerdere apparaten of beheerde knooppunten.</span><span class="sxs-lookup"><span data-stu-id="02508-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require hello coordination of multiple steps across multiple devices or managed nodes.</span></span> <span data-ttu-id="02508-109">Hallo voordelen van een werkstroom op een normaal script omvatten Hallo mogelijkheid toosimultaneously uitvoeren van een actie tegen meerdere apparaten en Hallo mogelijkheid tooautomatically herstellen van fouten.</span><span class="sxs-lookup"><span data-stu-id="02508-109">hello benefits of a workflow over a normal script include hello ability toosimultaneously perform an action against multiple devices and hello ability tooautomatically recover from failures.</span></span> <span data-ttu-id="02508-110">Een Windows PowerShell-werkstroom is een Windows PowerShell-script dat gebruikmaakt van Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="02508-110">A Windows PowerShell Workflow is a Windows PowerShell script that uses Windows Workflow Foundation.</span></span> <span data-ttu-id="02508-111">Tijdens het Hallo-werkstroom is geschreven met Windows PowerShell-syntaxis en gelanceerd door Windows PowerShell, wordt deze verwerkt door Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="02508-111">While hello workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span></span>

<span data-ttu-id="02508-112">Zie voor meer informatie over de onderwerpen in dit artikel Hallo [aan de slag met Windows PowerShell-werkstroom](http://technet.microsoft.com/library/jj134242.aspx).</span><span class="sxs-lookup"><span data-stu-id="02508-112">For complete details on hello topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span></span>

## <a name="basic-structure-of-a-workflow"></a><span data-ttu-id="02508-113">Algemene structuur van een werkstroom</span><span class="sxs-lookup"><span data-stu-id="02508-113">Basic structure of a workflow</span></span>
<span data-ttu-id="02508-114">Hallo eerste stap tooconverting een PowerShell-script tooa PowerShell workflow is tussen hello **werkstroom** sleutelwoord.</span><span class="sxs-lookup"><span data-stu-id="02508-114">hello first step tooconverting a PowerShell script tooa PowerShell workflow is enclosing it with hello **Workflow** keyword.</span></span>  <span data-ttu-id="02508-115">Een werkstroom begint met de Hallo **werkstroom** trefwoord gevolgd door de instantie Hallo van Hallo script tussen accolades.</span><span class="sxs-lookup"><span data-stu-id="02508-115">A workflow starts with hello **Workflow** keyword followed by hello body of hello script enclosed in braces.</span></span> <span data-ttu-id="02508-116">Hallo-naam van Hallo werkstroom volgt Hallo **werkstroom** trefwoord zoals getoond in Hallo de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="02508-116">hello name of hello workflow follows hello **Workflow** keyword as shown in hello following syntax:</span></span>

    Workflow Test-Workflow
    {
       <Commands>
    }

<span data-ttu-id="02508-117">Hallo-naam van Hallo werkstroom moet overeenkomen met de Hallo-naam van Hallo Automation-runbook.</span><span class="sxs-lookup"><span data-stu-id="02508-117">hello name of hello workflow must match hello name of hello Automation runbook.</span></span> <span data-ttu-id="02508-118">Als Hallo runbook wordt ingevoerd, wordt Hallo filename moet overeenkomen met de naam van de werkstroom Hallo en moet eindigen op *.ps1*.</span><span class="sxs-lookup"><span data-stu-id="02508-118">If hello runbook is being imported, then hello filename must match hello workflow name and must end in *.ps1*.</span></span>

<span data-ttu-id="02508-119">tooadd parameters toohello werkstroom, gebruik Hallo **Param** sleutelwoord net zoals u zou tooa script doen.</span><span class="sxs-lookup"><span data-stu-id="02508-119">tooadd parameters toohello workflow, use hello **Param** keyword just as you would tooa script.</span></span>

## <a name="code-changes"></a><span data-ttu-id="02508-120">Codewijzigingen</span><span class="sxs-lookup"><span data-stu-id="02508-120">Code changes</span></span>
<span data-ttu-id="02508-121">PowerShell-werkstroom code lijkt scriptcode van bijna identiek tooPowerShell, met uitzondering van enkele belangrijke wijzigingen aangebracht.</span><span class="sxs-lookup"><span data-stu-id="02508-121">PowerShell workflow code looks almost identical tooPowerShell script code except for a few significant changes.</span></span>  <span data-ttu-id="02508-122">Hallo volgende secties beschrijven wijzigingen moet u toomake tooa PowerShell-script voor het toorun in een werkstroom.</span><span class="sxs-lookup"><span data-stu-id="02508-122">hello following sections describe changes that you need toomake tooa PowerShell script for it toorun in a workflow.</span></span>

### <a name="activities"></a><span data-ttu-id="02508-123">Activiteiten</span><span class="sxs-lookup"><span data-stu-id="02508-123">Activities</span></span>
<span data-ttu-id="02508-124">Een activiteit is een specifieke taak in een werkstroom.</span><span class="sxs-lookup"><span data-stu-id="02508-124">An activity is a specific task in a workflow.</span></span> <span data-ttu-id="02508-125">Net zoals een script uit een of meer opdrachten bestaat, bestaat een werkstroom uit een of meer activiteiten die worden uitgevoerd in een reeks.</span><span class="sxs-lookup"><span data-stu-id="02508-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span></span> <span data-ttu-id="02508-126">Windows PowerShell-werkstroom converteert automatisch veel van Windows PowerShell-cmdlets tooactivities Hallo wanneer deze een werkstroom wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="02508-126">Windows PowerShell Workflow automatically converts many of hello Windows PowerShell cmdlets tooactivities when it runs a workflow.</span></span> <span data-ttu-id="02508-127">Wanneer u een van deze cmdlets in uw runbook opgeeft, wordt door Windows Workflow Foundation Hallo bijbehorende activiteit uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="02508-127">When you specify one of these cmdlets in your runbook, hello corresponding activity is run by Windows Workflow Foundation.</span></span> <span data-ttu-id="02508-128">Voor die cmdlets zonder een bijbehorende activiteit Windows PowerShell Workflow voert automatisch Hallo cmdlet binnen een [InlineScript](#inlinescript) activiteit.</span><span class="sxs-lookup"><span data-stu-id="02508-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs hello cmdlet within an [InlineScript](#inlinescript) activity.</span></span> <span data-ttu-id="02508-129">Er is een set cmdlets die zijn uitgesloten en kan niet worden gebruikt in een werkstroom, tenzij u ze expliciet in een InlineScript blok opneemt.</span><span class="sxs-lookup"><span data-stu-id="02508-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span></span> <span data-ttu-id="02508-130">Zie voor meer informatie over deze begrippen [met behulp van activiteiten in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span><span class="sxs-lookup"><span data-stu-id="02508-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span></span>

<span data-ttu-id="02508-131">Werkstroomactiviteiten delen een aantal gemeenschappelijke parameters tooconfigure hun werking.</span><span class="sxs-lookup"><span data-stu-id="02508-131">Workflow activities share a set of common parameters tooconfigure their operation.</span></span> <span data-ttu-id="02508-132">Zie voor meer informatie over algemene werkstroomparameters hello [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="02508-132">For details about hello workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="positional-parameters"></a><span data-ttu-id="02508-133">Positionele parameters</span><span class="sxs-lookup"><span data-stu-id="02508-133">Positional parameters</span></span>
<span data-ttu-id="02508-134">U kunt positieparameters niet gebruiken met activiteiten en cmdlets in een werkstroom.</span><span class="sxs-lookup"><span data-stu-id="02508-134">You can't use positional parameters with activities and cmdlets in a workflow.</span></span>  <span data-ttu-id="02508-135">Dit betekent dat is dat u de namen van parameters moet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02508-135">All this means is that you must use parameter names.</span></span>

<span data-ttu-id="02508-136">Denk bijvoorbeeld Hallo na de code die alle actieve services krijgt.</span><span class="sxs-lookup"><span data-stu-id="02508-136">For example, consider hello following code that gets all running services.</span></span>

     Get-Service | Where-Object {$_.Status -eq "Running"}

<span data-ttu-id="02508-137">Als u deze code in een werkstroom toorun probeert, ontvangen een bericht zoals "Parameter set kan niet worden omgezet met behulp van Hallo opgegeven benoemde parameters."</span><span class="sxs-lookup"><span data-stu-id="02508-137">If you try toorun this same code in a workflow, you receive a message like "Parameter set cannot be resolved using hello specified named parameters."</span></span>  <span data-ttu-id="02508-138">toocorrect dit Hallo parameternaam zoals in de volgende Hallo bieden.</span><span class="sxs-lookup"><span data-stu-id="02508-138">toocorrect this, provide hello parameter name as in hello following.</span></span>

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a><span data-ttu-id="02508-139">Gedeserialiseerde objecten</span><span class="sxs-lookup"><span data-stu-id="02508-139">Deserialized objects</span></span>
<span data-ttu-id="02508-140">Objecten in werkstromen worden gedeserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="02508-140">Objects in workflows are deserialized.</span></span>  <span data-ttu-id="02508-141">Dit betekent dat de eigenschappen zijn nog steeds beschikbaar, maar niet de methoden.</span><span class="sxs-lookup"><span data-stu-id="02508-141">This means that their properties are still available, but not their methods.</span></span>  <span data-ttu-id="02508-142">Denk bijvoorbeeld Hallo volgende PowerShell-code die een service met de methode voor het stoppen van Service-object Hallo Hallo stopt.</span><span class="sxs-lookup"><span data-stu-id="02508-142">For example, consider hello following PowerShell code that stops a service using hello Stop method of hello Service object.</span></span>

    $Service = Get-Service -Name MyService
    $Service.Stop()

<span data-ttu-id="02508-143">Als u toorun dit in een werkstroom probeert, ontvangt u een foutmelding verschijnt "de methodeaanroep wordt niet ondersteund in een Windows PowerShell-werkstroom."</span><span class="sxs-lookup"><span data-stu-id="02508-143">If you try toorun this in a workflow, you receive an error saying "Method invocation is not supported in a Windows PowerShell Workflow."</span></span>  

<span data-ttu-id="02508-144">Een mogelijkheid is toowrap deze twee regels code in een [InlineScript](#inlinescript) blokkeren in dat geval $Service zou een serviceobject binnen Hallo-blok zijn.</span><span class="sxs-lookup"><span data-stu-id="02508-144">One option is toowrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within hello block.</span></span>

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

<span data-ttu-id="02508-145">Een andere optie toouse is een andere cmdlet die uitvoert Hallo dezelfde functionaliteit als Hallo-methode, als deze beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="02508-145">Another option is toouse another cmdlet that performs hello same functionality as hello method, if one is available.</span></span>  <span data-ttu-id="02508-146">In ons voorbeeld Hallo Service stoppen cmdlet Hallo biedt dezelfde functionaliteit als de methode stoppen hello, en u kunt gebruiken om de volgende Hallo voor een werkstroom.</span><span class="sxs-lookup"><span data-stu-id="02508-146">In our sample, hello Stop-Service cmdlet provides hello same functionality as hello Stop method, and you could use hello following for a workflow.</span></span>

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a><span data-ttu-id="02508-147">InlineScript</span><span class="sxs-lookup"><span data-stu-id="02508-147">InlineScript</span></span>
<span data-ttu-id="02508-148">Hallo **InlineScript** activiteit is handig als u toorun een of meer opdrachten als traditionele PowerShell-script in plaats van PowerShell-werkstroom moet.</span><span class="sxs-lookup"><span data-stu-id="02508-148">hello **InlineScript** activity is useful when you need toorun one or more commands as traditional PowerShell script instead of PowerShell workflow.</span></span>  <span data-ttu-id="02508-149">Terwijl de opdrachten in een werkstroom worden tooWindows Workflow Foundation worden verzonden voor verwerking, worden door Windows PowerShell-opdrachten in een InlineScript-blok verwerkt.</span><span class="sxs-lookup"><span data-stu-id="02508-149">While commands in a workflow are sent tooWindows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span></span>

<span data-ttu-id="02508-150">InlineScript gebruikt Hallo syntaxis hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="02508-150">InlineScript uses hello following syntax shown below.</span></span>

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

<span data-ttu-id="02508-151">Uitvoer kunt van een InlineScript u terugkeren door Hallo uitvoer tooa variabele toewijzen.</span><span class="sxs-lookup"><span data-stu-id="02508-151">You can return output from an InlineScript by assigning hello output tooa variable.</span></span> <span data-ttu-id="02508-152">Hello volgende voorbeeld wordt een service wordt gestopt en vervolgens levert Hallo servicenaam.</span><span class="sxs-lookup"><span data-stu-id="02508-152">hello following example stops a service and then outputs hello service name.</span></span>

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="02508-153">U kunt waarden doorgeven in een InlineScript-blok, maar moet u **$Using** bereikaanpassingsfunctie.</span><span class="sxs-lookup"><span data-stu-id="02508-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span></span>  <span data-ttu-id="02508-154">Hallo volgende voorbeeld is het vorige voorbeeld identieke toohello, behalve dat hello servicenaam geleverd door een variabele.</span><span class="sxs-lookup"><span data-stu-id="02508-154">hello following example is identical toohello previous example except that hello service name is provided by a variable.</span></span>

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


<span data-ttu-id="02508-155">Tijdens het InlineScript-activiteiten mogelijk kritieke in bepaalde werkstromen, ze bieden geen ondersteuning voor werkstroom constructies en mag alleen worden gebruikt wanneer dat nodig is voor de volgende redenen Hallo:</span><span class="sxs-lookup"><span data-stu-id="02508-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for hello following reasons:</span></span>

* <span data-ttu-id="02508-156">U kunt geen gebruiken [controlepunten](#checkpoints) in een InlineScript-blok.</span><span class="sxs-lookup"><span data-stu-id="02508-156">You cannot use [checkpoints](#checkpoints) inside an InlineScript block.</span></span> <span data-ttu-id="02508-157">Als er een fout optreedt in Hallo blok, moet het worden hervat vanaf Hallo Hallo blok.</span><span class="sxs-lookup"><span data-stu-id="02508-157">If a failure occurs within hello block, it must be resumed from hello beginning of hello block.</span></span>
* <span data-ttu-id="02508-158">U kunt geen gebruiken [parallelle uitvoering](#parallel-processing) binnen een InlineScriptBlock.</span><span class="sxs-lookup"><span data-stu-id="02508-158">You cannot use [parallel execution](#parallel-processing) inside an InlineScriptBlock.</span></span>
* <span data-ttu-id="02508-159">InlineScript dit beïnvloedt de schaalbaarheid van de werkstroom Hallo omdat deze Windows PowerShell-sessie voor de gehele lengte van de InlineScript-blok Hallo HALLO hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="02508-159">InlineScript affects scalability of hello workflow since it holds hello Windows PowerShell session for hello entire length of hello InlineScript block.</span></span>

<span data-ttu-id="02508-160">Zie voor meer informatie over het gebruik van InlineScript [Windows PowerShell-opdrachten in een werkstroom](http://technet.microsoft.com/library/jj574197.aspx) en [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span><span class="sxs-lookup"><span data-stu-id="02508-160">For more information on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span></span>

## <a name="parallel-processing"></a><span data-ttu-id="02508-161">Parallelle verwerking</span><span class="sxs-lookup"><span data-stu-id="02508-161">Parallel processing</span></span>
<span data-ttu-id="02508-162">Een voordeel van Windows PowerShell-werkstromen is Hallo mogelijkheid tooperform een reeks opdrachten parallel in plaats van opeenvolgend zoals bij een typische script.</span><span class="sxs-lookup"><span data-stu-id="02508-162">One advantage of Windows PowerShell Workflows is hello ability tooperform a set of commands in parallel instead of sequentially as with a typical script.</span></span>

<span data-ttu-id="02508-163">U kunt Hallo **parallelle** sleutelwoord toocreate een scriptblok is opgegeven met meerdere opdrachten die gelijktijdig worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="02508-163">You can use hello **Parallel** keyword toocreate a script block with multiple commands that run concurrently.</span></span> <span data-ttu-id="02508-164">Dit maakt gebruik van Hallo syntaxis hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="02508-164">This uses hello following syntax shown below.</span></span> <span data-ttu-id="02508-165">In dit geval activiteit1 en activiteit2 begint bij Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="02508-165">In this case, Activity1 and Activity2 starts at hello same time.</span></span> <span data-ttu-id="02508-166">Activiteit3 start pas als zowel activiteit1 en activiteit2 zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="02508-166">Activity3 starts only after both Activity1 and Activity2 have completed.</span></span>

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


<span data-ttu-id="02508-167">Denk bijvoorbeeld Hallo volgende PowerShell-opdrachten die meerdere bestanden tooa netwerk doel kopiëren.</span><span class="sxs-lookup"><span data-stu-id="02508-167">For example, consider hello following PowerShell commands that copy multiple files tooa network destination.</span></span>  <span data-ttu-id="02508-168">Deze opdrachten worden opeenvolgend uitgevoerd zodanig dat één bestand met het kopiëren eindigen moet voordat naast hello wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="02508-168">These commands are run sequentially so that one file must finish copying before hello next is started.</span></span>     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

<span data-ttu-id="02508-169">Hallo volgende werkstroom wordt uitgevoerd deze dezelfde parallel opdrachten zodat deze alle beginnen met het kopiëren op Hallo van dezelfde tijd.</span><span class="sxs-lookup"><span data-stu-id="02508-169">hello following workflow runs these same commands in parallel so that they all start copying at hello same time.</span></span>  <span data-ttu-id="02508-170">Pas nadat ze alle zijn gekopieerd Hallo voltooiingsbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="02508-170">Only after they are all copied is hello completion message displayed.</span></span>

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


<span data-ttu-id="02508-171">U kunt Hallo **ForEach-Parallel** tooprocess-opdrachten voor elk item in een verzameling gelijktijdig te maken.</span><span class="sxs-lookup"><span data-stu-id="02508-171">You can use hello **ForEach -Parallel** construct tooprocess commands for each item in a collection concurrently.</span></span> <span data-ttu-id="02508-172">Hallo-items in Hallo verzameling worden parallel verwerkt tijdens het Hallo-opdrachten in Hallo-scriptblok worden opeenvolgend uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="02508-172">hello items in hello collection are processed in parallel while hello commands in hello script block run sequentially.</span></span> <span data-ttu-id="02508-173">Dit maakt gebruik van Hallo syntaxis hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="02508-173">This uses hello following syntax shown below.</span></span> <span data-ttu-id="02508-174">In dit geval activiteit1 begint bij Hallo dezelfde tijd voor alle items in de verzameling Hallo.</span><span class="sxs-lookup"><span data-stu-id="02508-174">In this case, Activity1 starts at hello same time for all items in hello collection.</span></span> <span data-ttu-id="02508-175">Voor elk item start activiteit2 nadat activiteit1 voltooid.</span><span class="sxs-lookup"><span data-stu-id="02508-175">For each item, Activity2 starts after Activity1 is complete.</span></span> <span data-ttu-id="02508-176">Activiteit3 start pas als zowel activiteit1 en activiteit2 zijn voltooid voor alle items.</span><span class="sxs-lookup"><span data-stu-id="02508-176">Activity3 starts only after both Activity1 and Activity2 have completed for all items.</span></span>

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

<span data-ttu-id="02508-177">Hallo volgende voorbeeld is vergelijkbaar toohello vorige voorbeeld parallel bestanden zijn gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="02508-177">hello following example is similar toohello previous example copying files in parallel.</span></span>  <span data-ttu-id="02508-178">In dit geval wordt een bericht weergegeven voor elk bestand nadat deze zijn gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="02508-178">In this case, a message is displayed for each file after it copies.</span></span>  <span data-ttu-id="02508-179">Alleen nadat ze alle zijn volledig gekopieerd uiteindelijke voltooiing het Hallo-bericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="02508-179">Only after they are all completely copied is hello final completion message displayed.</span></span>

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
> <span data-ttu-id="02508-180">We raden niet onderliggende runbooks parallel uitgevoerd, omdat dit is toogive onbetrouwbare resultaten weergegeven.</span><span class="sxs-lookup"><span data-stu-id="02508-180">We do not recommend running child runbooks in parallel since this has been shown toogive unreliable results.</span></span>  <span data-ttu-id="02508-181">Hallo uitvoer van Hallo onderliggend runbook soms wordt niet weergegeven en kunnen invloed hebben op de instellingen in een onderliggend runbook andere runbooks parallelle onderliggende hello</span><span class="sxs-lookup"><span data-stu-id="02508-181">hello output from hello child runbook sometimes does not show up, and settings in one child runbook can affect hello other parallel child runbooks</span></span>
>

## <a name="checkpoints"></a><span data-ttu-id="02508-182">Controlepunten</span><span class="sxs-lookup"><span data-stu-id="02508-182">Checkpoints</span></span>
<span data-ttu-id="02508-183">Een *controlepunt* is een momentopname van huidige status van de Hallo van Hallo werkstroom met de huidige waarde Hallo voor variabelen en de gegenereerde toothat punt uitvoer.</span><span class="sxs-lookup"><span data-stu-id="02508-183">A *checkpoint* is a snapshot of hello current state of hello workflow that includes hello current value for variables and any output generated toothat point.</span></span> <span data-ttu-id="02508-184">Als een werkstroom in een fout eindigt of is onderbroken, wordt vervolgens Hallo volgende keer dat deze wordt uitgevoerd dat deze gestart vanaf de laatste controlepunt in plaats van Hallo Hallo worfklow is gestart.</span><span class="sxs-lookup"><span data-stu-id="02508-184">If a workflow ends in error or is suspended, then hello next time it is run it will start from its last checkpoint instead of hello start of hello worfklow.</span></span>  <span data-ttu-id="02508-185">U kunt een controlepunt instellen in een werkstroom met Hallo **Checkpoint-Workflow** activiteit.</span><span class="sxs-lookup"><span data-stu-id="02508-185">You can set a checkpoint in a workflow with hello **Checkpoint-Workflow** activity.</span></span>

<span data-ttu-id="02508-186">In Hallo voorbeeldcode te volgen, wordt een uitzondering optreedt nadat de werkstroom tooend activiteit2 waardoor Hallo.</span><span class="sxs-lookup"><span data-stu-id="02508-186">In hello following sample code, an exception occurs after Activity2 causing hello workflow tooend.</span></span> <span data-ttu-id="02508-187">Wanneer de werkstroom Hallo opnieuw wordt uitgevoerd, wordt er door het uitvoeren van activiteit2 aangezien dit vlak nadat het laatste controlepunt Hallo ingesteld is gestart.</span><span class="sxs-lookup"><span data-stu-id="02508-187">When hello workflow is run again, it starts by running Activity2 since this was just after hello last checkpoint set.</span></span>

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

<span data-ttu-id="02508-188">U moet controlepunten in een werkstroom instellen na activiteiten die foutgevoelig tooexception mogelijk en mag geen herhaalde als Hallo werkstroom wordt hervat.</span><span class="sxs-lookup"><span data-stu-id="02508-188">You should set checkpoints in a workflow after activities that may be prone tooexception and should not be repeated if hello workflow is resumed.</span></span> <span data-ttu-id="02508-189">De werkstroom kan bijvoorbeeld een virtuele machine maken.</span><span class="sxs-lookup"><span data-stu-id="02508-189">For example, your workflow may create a virtual machine.</span></span> <span data-ttu-id="02508-190">U kunt een controlepunt instellen, zowel voor en na Hallo opdrachten toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="02508-190">You could set a checkpoint both before and after hello commands toocreate hello virtual machine.</span></span> <span data-ttu-id="02508-191">Als Hallo maken is mislukt, zou vervolgens Hallo opdrachten worden herhaald als Hallo werkstroom opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="02508-191">If hello creation fails, then hello commands would be repeated if hello workflow is started again.</span></span> <span data-ttu-id="02508-192">Als Hallo worfklow mislukt nadat Hallo aanmaak slaagt, wordt klikt u vervolgens Hallo virtuele machine niet opnieuw worden gemaakt wanneer Hallo werkstroom wordt hervat.</span><span class="sxs-lookup"><span data-stu-id="02508-192">If hello worfklow fails after hello creation succeeds, then hello virtual machine will not be created again when hello workflow is resumed.</span></span>

<span data-ttu-id="02508-193">Hallo volgt meerdere bestanden tooa netwerklocatie kopieert en stelt een controlepunt na elk bestand.</span><span class="sxs-lookup"><span data-stu-id="02508-193">hello following example copies multiple files tooa network location and sets a checkpoint after each file.</span></span>  <span data-ttu-id="02508-194">Als de netwerklocatie Hallo verloren gegaan is, vervolgens eindigt Hallo werkstroom in fout.</span><span class="sxs-lookup"><span data-stu-id="02508-194">If hello network location is lost, then hello workflow ends in error.</span></span>  <span data-ttu-id="02508-195">Wanneer opnieuw wordt gestart, wordt deze hervat op Hallo laatste controlepunt, wat betekent dat alleen Hallo-bestanden die al is gekopieerd worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="02508-195">When it is started again, it will resume at hello last checkpoint meaning that only hello files that have already been copied are skipped.</span></span>

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

<span data-ttu-id="02508-196">Omdat de referenties van de gebruikersnaam worden niet persistent na het aanroepen van Hallo [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activiteit of na de laatste controlepunt hello, u moet tooset Hallo referenties toonull en vervolgens terugzetten opnieuw uit Hallo asset store na  **Suspend-Workflow** of controlepunt wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="02508-196">Because username credentials are not persisted after you call hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after hello last checkpoint, you need tooset hello credentials toonull and then retrieve them again from hello asset store after **Suspend-Workflow** or checkpoint is called.</span></span>  <span data-ttu-id="02508-197">Anders krijgt u Hallo volgende foutbericht weergegeven: *Hallo werkstroomtaak kan niet worden hervat, ofwel omdat persistentie gegevens kan niet worden opgeslagen volledig of opgeslagen gegevens persistentie is beschadigd. U moet Hallo werkstroom opnieuw.*</span><span class="sxs-lookup"><span data-stu-id="02508-197">Otherwise, you may receive hello following error message: *hello workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart hello workflow.*</span></span>

<span data-ttu-id="02508-198">Hallo volgen dezelfde code laat zien hoe toohandle dit in uw PowerShell Workflow-runbooks.</span><span class="sxs-lookup"><span data-stu-id="02508-198">hello following same code demonstrates how toohandle this in your PowerShell Workflow runbooks.</span></span>

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first toocreate hello VM (code not shown)

          # Now add hello VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


<span data-ttu-id="02508-199">Dit is niet vereist als u zich verifiëren met behulp van een Run As-account geconfigureerd met een service-principal.</span><span class="sxs-lookup"><span data-stu-id="02508-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span></span>  

<span data-ttu-id="02508-200">Zie voor meer informatie over controlepunten [controlepunten toevoegen tooa Scriptwerkstroom](http://technet.microsoft.com/library/jj574114.aspx).</span><span class="sxs-lookup"><span data-stu-id="02508-200">For more information about checkpoints, see [Adding Checkpoints tooa Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="02508-201">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="02508-201">Next steps</span></span>
* <span data-ttu-id="02508-202">tooget gestart met PowerShell workflow-runbooks, Zie [Mijn eerste PowerShell workflow-runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="02508-202">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
