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
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a>Leren van de belangrijkste concepten voor Windows PowerShell-werkstroom voor Automation-runbooks 
Azure Automation-Runbooks worden geïmplementeerd als Windows PowerShell-werkstromen.  Een Windows PowerShell-werkstroom is vergelijkbaar tooa Windows PowerShell-script, maar heeft enkele belangrijke verschillen die verwarrend tooa nieuwe gebruiker worden kunnen.  In dit artikel is bedoeld toohelp schrijven van runbooks met behulp van PowerShell workflow, wordt u aangeraden dat u runbooks met behulp van PowerShell, tenzij u controlepunten moet schrijven.  Er zijn verschillende syntaxisverschillen bij het ontwerpen van PowerShell Workflow-runbooks en deze verschillen vereisen iets meer werk toowrite effectieve workflows.  

Een werkstroom is een opeenvolging van geprogrammeerde, verbonden stappen waarmee langlopende taken uitvoeren of Hallo coördinatie van meerdere stappen vereisen op meerdere apparaten of beheerde knooppunten. Hallo voordelen van een werkstroom op een normaal script omvatten Hallo mogelijkheid toosimultaneously uitvoeren van een actie tegen meerdere apparaten en Hallo mogelijkheid tooautomatically herstellen van fouten. Een Windows PowerShell-werkstroom is een Windows PowerShell-script dat gebruikmaakt van Windows Workflow Foundation. Tijdens het Hallo-werkstroom is geschreven met Windows PowerShell-syntaxis en gelanceerd door Windows PowerShell, wordt deze verwerkt door Windows Workflow Foundation.

Zie voor meer informatie over de onderwerpen in dit artikel Hallo [aan de slag met Windows PowerShell-werkstroom](http://technet.microsoft.com/library/jj134242.aspx).

## <a name="basic-structure-of-a-workflow"></a>Algemene structuur van een werkstroom
Hallo eerste stap tooconverting een PowerShell-script tooa PowerShell workflow is tussen hello **werkstroom** sleutelwoord.  Een werkstroom begint met de Hallo **werkstroom** trefwoord gevolgd door de instantie Hallo van Hallo script tussen accolades. Hallo-naam van Hallo werkstroom volgt Hallo **werkstroom** trefwoord zoals getoond in Hallo de volgende syntaxis:

    Workflow Test-Workflow
    {
       <Commands>
    }

Hallo-naam van Hallo werkstroom moet overeenkomen met de Hallo-naam van Hallo Automation-runbook. Als Hallo runbook wordt ingevoerd, wordt Hallo filename moet overeenkomen met de naam van de werkstroom Hallo en moet eindigen op *.ps1*.

tooadd parameters toohello werkstroom, gebruik Hallo **Param** sleutelwoord net zoals u zou tooa script doen.

## <a name="code-changes"></a>Codewijzigingen
PowerShell-werkstroom code lijkt scriptcode van bijna identiek tooPowerShell, met uitzondering van enkele belangrijke wijzigingen aangebracht.  Hallo volgende secties beschrijven wijzigingen moet u toomake tooa PowerShell-script voor het toorun in een werkstroom.

### <a name="activities"></a>Activiteiten
Een activiteit is een specifieke taak in een werkstroom. Net zoals een script uit een of meer opdrachten bestaat, bestaat een werkstroom uit een of meer activiteiten die worden uitgevoerd in een reeks. Windows PowerShell-werkstroom converteert automatisch veel van Windows PowerShell-cmdlets tooactivities Hallo wanneer deze een werkstroom wordt uitgevoerd. Wanneer u een van deze cmdlets in uw runbook opgeeft, wordt door Windows Workflow Foundation Hallo bijbehorende activiteit uitgevoerd. Voor die cmdlets zonder een bijbehorende activiteit Windows PowerShell Workflow voert automatisch Hallo cmdlet binnen een [InlineScript](#inlinescript) activiteit. Er is een set cmdlets die zijn uitgesloten en kan niet worden gebruikt in een werkstroom, tenzij u ze expliciet in een InlineScript blok opneemt. Zie voor meer informatie over deze begrippen [met behulp van activiteiten in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).

Werkstroomactiviteiten delen een aantal gemeenschappelijke parameters tooconfigure hun werking. Zie voor meer informatie over algemene werkstroomparameters hello [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).

### <a name="positional-parameters"></a>Positionele parameters
U kunt positieparameters niet gebruiken met activiteiten en cmdlets in een werkstroom.  Dit betekent dat is dat u de namen van parameters moet gebruiken.

Denk bijvoorbeeld Hallo na de code die alle actieve services krijgt.

     Get-Service | Where-Object {$_.Status -eq "Running"}

Als u deze code in een werkstroom toorun probeert, ontvangen een bericht zoals "Parameter set kan niet worden omgezet met behulp van Hallo opgegeven benoemde parameters."  toocorrect dit Hallo parameternaam zoals in de volgende Hallo bieden.

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a>Gedeserialiseerde objecten
Objecten in werkstromen worden gedeserialiseerd.  Dit betekent dat de eigenschappen zijn nog steeds beschikbaar, maar niet de methoden.  Denk bijvoorbeeld Hallo volgende PowerShell-code die een service met de methode voor het stoppen van Service-object Hallo Hallo stopt.

    $Service = Get-Service -Name MyService
    $Service.Stop()

Als u toorun dit in een werkstroom probeert, ontvangt u een foutmelding verschijnt "de methodeaanroep wordt niet ondersteund in een Windows PowerShell-werkstroom."  

Een mogelijkheid is toowrap deze twee regels code in een [InlineScript](#inlinescript) blokkeren in dat geval $Service zou een serviceobject binnen Hallo-blok zijn.

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

Een andere optie toouse is een andere cmdlet die uitvoert Hallo dezelfde functionaliteit als Hallo-methode, als deze beschikbaar is.  In ons voorbeeld Hallo Service stoppen cmdlet Hallo biedt dezelfde functionaliteit als de methode stoppen hello, en u kunt gebruiken om de volgende Hallo voor een werkstroom.

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a>InlineScript
Hallo **InlineScript** activiteit is handig als u toorun een of meer opdrachten als traditionele PowerShell-script in plaats van PowerShell-werkstroom moet.  Terwijl de opdrachten in een werkstroom worden tooWindows Workflow Foundation worden verzonden voor verwerking, worden door Windows PowerShell-opdrachten in een InlineScript-blok verwerkt.

InlineScript gebruikt Hallo syntaxis hieronder weergegeven.

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

Uitvoer kunt van een InlineScript u terugkeren door Hallo uitvoer tooa variabele toewijzen. Hello volgende voorbeeld wordt een service wordt gestopt en vervolgens levert Hallo servicenaam.

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


U kunt waarden doorgeven in een InlineScript-blok, maar moet u **$Using** bereikaanpassingsfunctie.  Hallo volgende voorbeeld is het vorige voorbeeld identieke toohello, behalve dat hello servicenaam geleverd door een variabele.

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


Tijdens het InlineScript-activiteiten mogelijk kritieke in bepaalde werkstromen, ze bieden geen ondersteuning voor werkstroom constructies en mag alleen worden gebruikt wanneer dat nodig is voor de volgende redenen Hallo:

* U kunt geen gebruiken [controlepunten](#checkpoints) in een InlineScript-blok. Als er een fout optreedt in Hallo blok, moet het worden hervat vanaf Hallo Hallo blok.
* U kunt geen gebruiken [parallelle uitvoering](#parallel-processing) binnen een InlineScriptBlock.
* InlineScript dit beïnvloedt de schaalbaarheid van de werkstroom Hallo omdat deze Windows PowerShell-sessie voor de gehele lengte van de InlineScript-blok Hallo HALLO hallo bevat.

Zie voor meer informatie over het gebruik van InlineScript [Windows PowerShell-opdrachten in een werkstroom](http://technet.microsoft.com/library/jj574197.aspx) en [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).

## <a name="parallel-processing"></a>Parallelle verwerking
Een voordeel van Windows PowerShell-werkstromen is Hallo mogelijkheid tooperform een reeks opdrachten parallel in plaats van opeenvolgend zoals bij een typische script.

U kunt Hallo **parallelle** sleutelwoord toocreate een scriptblok is opgegeven met meerdere opdrachten die gelijktijdig worden uitgevoerd. Dit maakt gebruik van Hallo syntaxis hieronder weergegeven. In dit geval activiteit1 en activiteit2 begint bij Hallo hetzelfde moment. Activiteit3 start pas als zowel activiteit1 en activiteit2 zijn voltooid.

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


Denk bijvoorbeeld Hallo volgende PowerShell-opdrachten die meerdere bestanden tooa netwerk doel kopiëren.  Deze opdrachten worden opeenvolgend uitgevoerd zodanig dat één bestand met het kopiëren eindigen moet voordat naast hello wordt gestart.     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

Hallo volgende werkstroom wordt uitgevoerd deze dezelfde parallel opdrachten zodat deze alle beginnen met het kopiëren op Hallo van dezelfde tijd.  Pas nadat ze alle zijn gekopieerd Hallo voltooiingsbericht weergegeven.

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


U kunt Hallo **ForEach-Parallel** tooprocess-opdrachten voor elk item in een verzameling gelijktijdig te maken. Hallo-items in Hallo verzameling worden parallel verwerkt tijdens het Hallo-opdrachten in Hallo-scriptblok worden opeenvolgend uitgevoerd. Dit maakt gebruik van Hallo syntaxis hieronder weergegeven. In dit geval activiteit1 begint bij Hallo dezelfde tijd voor alle items in de verzameling Hallo. Voor elk item start activiteit2 nadat activiteit1 voltooid. Activiteit3 start pas als zowel activiteit1 en activiteit2 zijn voltooid voor alle items.

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

Hallo volgende voorbeeld is vergelijkbaar toohello vorige voorbeeld parallel bestanden zijn gekopieerd.  In dit geval wordt een bericht weergegeven voor elk bestand nadat deze zijn gekopieerd.  Alleen nadat ze alle zijn volledig gekopieerd uiteindelijke voltooiing het Hallo-bericht weergegeven.

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
> We raden niet onderliggende runbooks parallel uitgevoerd, omdat dit is toogive onbetrouwbare resultaten weergegeven.  Hallo uitvoer van Hallo onderliggend runbook soms wordt niet weergegeven en kunnen invloed hebben op de instellingen in een onderliggend runbook andere runbooks parallelle onderliggende hello
>

## <a name="checkpoints"></a>Controlepunten
Een *controlepunt* is een momentopname van huidige status van de Hallo van Hallo werkstroom met de huidige waarde Hallo voor variabelen en de gegenereerde toothat punt uitvoer. Als een werkstroom in een fout eindigt of is onderbroken, wordt vervolgens Hallo volgende keer dat deze wordt uitgevoerd dat deze gestart vanaf de laatste controlepunt in plaats van Hallo Hallo worfklow is gestart.  U kunt een controlepunt instellen in een werkstroom met Hallo **Checkpoint-Workflow** activiteit.

In Hallo voorbeeldcode te volgen, wordt een uitzondering optreedt nadat de werkstroom tooend activiteit2 waardoor Hallo. Wanneer de werkstroom Hallo opnieuw wordt uitgevoerd, wordt er door het uitvoeren van activiteit2 aangezien dit vlak nadat het laatste controlepunt Hallo ingesteld is gestart.

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

U moet controlepunten in een werkstroom instellen na activiteiten die foutgevoelig tooexception mogelijk en mag geen herhaalde als Hallo werkstroom wordt hervat. De werkstroom kan bijvoorbeeld een virtuele machine maken. U kunt een controlepunt instellen, zowel voor en na Hallo opdrachten toocreate Hallo virtuele machine. Als Hallo maken is mislukt, zou vervolgens Hallo opdrachten worden herhaald als Hallo werkstroom opnieuw wordt gestart. Als Hallo worfklow mislukt nadat Hallo aanmaak slaagt, wordt klikt u vervolgens Hallo virtuele machine niet opnieuw worden gemaakt wanneer Hallo werkstroom wordt hervat.

Hallo volgt meerdere bestanden tooa netwerklocatie kopieert en stelt een controlepunt na elk bestand.  Als de netwerklocatie Hallo verloren gegaan is, vervolgens eindigt Hallo werkstroom in fout.  Wanneer opnieuw wordt gestart, wordt deze hervat op Hallo laatste controlepunt, wat betekent dat alleen Hallo-bestanden die al is gekopieerd worden overgeslagen.

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

Omdat de referenties van de gebruikersnaam worden niet persistent na het aanroepen van Hallo [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activiteit of na de laatste controlepunt hello, u moet tooset Hallo referenties toonull en vervolgens terugzetten opnieuw uit Hallo asset store na  **Suspend-Workflow** of controlepunt wordt aangeroepen.  Anders krijgt u Hallo volgende foutbericht weergegeven: *Hallo werkstroomtaak kan niet worden hervat, ofwel omdat persistentie gegevens kan niet worden opgeslagen volledig of opgeslagen gegevens persistentie is beschadigd. U moet Hallo werkstroom opnieuw.*

Hallo volgen dezelfde code laat zien hoe toohandle dit in uw PowerShell Workflow-runbooks.

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


Dit is niet vereist als u zich verifiëren met behulp van een Run As-account geconfigureerd met een service-principal.  

Zie voor meer informatie over controlepunten [controlepunten toevoegen tooa Scriptwerkstroom](http://technet.microsoft.com/library/jj574114.aspx).

## <a name="next-steps"></a>Volgende stappen
* tooget gestart met PowerShell workflow-runbooks, Zie [Mijn eerste PowerShell workflow-runbook](automation-first-runbook-textual.md)
