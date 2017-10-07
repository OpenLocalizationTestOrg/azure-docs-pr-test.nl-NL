---
title: aaaError verwerken in Azure Automation grafische runbooks | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooimplement-fout tijdens het verwerken van logica in Azure Automation grafische runbooks.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/26/2016
ms.author: magoedte
ms.openlocfilehash: b9ff01361d2ebd9c0174b074a7a290b1cc2fd1c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="error-handling-in-azure-automation-graphical-runbooks"></a>Foutafhandeling in grafische Azure Automation-runbooks

Een sleutel runbook ontwerp principal tooconsider met het identificeren van verschillende problemen waarmee een runbook kunt krijgen. Deze problemen kunnen geslaagde pogingen, verwachte foutstatussen en onverwachte foutvoorwaarden zijn.

Runbooks moeten foutafhandeling bevatten. toovalidate Hallo uitvoer van een activiteit of een fout opgetreden bij de grafische runbooks verwerken, kan u de activiteit van een Windows PowerShell gebruiken, voorwaardelijke logica definiëren op Hallo uitvoer koppeling van de activiteit Hallo of toepassen van een andere methode.          

Als er een fout niet wordt beëindigd, die wordt uitgevoerd met een runbook-activiteit, wordt elke activiteit die volgt vaak verwerkt ongeacht het Hallo-fout. Hallo-fout is waarschijnlijk toogenerate een uitzondering, maar de volgende activiteit Hallo heeft nog steeds toorun. Dit is Hallo manier dat PowerShell ontworpen toohandle fouten is.    

Hallo typen PowerShell fouten die zich tijdens de uitvoering voordoen kunnen wordt beëindigd of niet wordt beëindigd. Hallo verschillen tussen wordt beëindigd en niet wordt beëindigd fouten zijn als volgt:

* **Fout beëindigd**: een ernstige fout tijdens het uitvoeren van die volledig Hallo opdracht (of het uitvoeren van script) stopt. Voorbeelden zijn onder andere niet-bestaande cmdlets, syntaxisfouten waardoor een cmdlet niet kan worden uitgevoerd of andere fatale fouten.

* **Fout niet beëindigd**: een niet-ernstige fout waarmee uitvoering toocontinue ondanks Hallo-fout. Voorbeelden zijn onder andere operationele fouten, zoals niet-gevonden bestanden en machtigingsproblemen.

Azure Automation-grafische runbooks zijn verbeterd met Hallo mogelijkheid tooinclude foutafhandeling. U kunt nu van uitzonderingen niet-afsluitfouten maken en foutkoppelingen tussen activiteiten maken. Dit proces kan de runbookauteur van een toocatch fouten en gerealiseerde of onverwachte voorwaarden beheren.  

## <a name="when-toouse-error-handling"></a>Wanneer de foutafhandeling toouse

Wanneer er een kritieke fout of uitzondering genereert activiteit, is het belangrijk tooprevent Hallo volgende activiteit in uw runbook verwerking en toohandle Hallo-fout op de juiste wijze. Dit is met name cruciaal wanneer uw runbooks ondersteuning bieden voor een bedrijfsproces of servicebewerking.

Voor elke activiteit die een fout kunt produceren, toevoegen Hallo runbookauteur de koppeling van een fout die andere activiteiten wijst tooany.  Hallo doelactiviteit kunt van elk type, met inbegrip van code activiteiten, aanroepen van een cmdlet aanroepen van een ander runbook zijn enzovoort.

Bovendien kan doelactiviteit Hallo ook uitgaande koppelingen hebben. Dit kunnen gewone koppelingen zijn of foutkoppelingen. Dit betekent dat Hallo runbookauteur complexe logica voor foutafhandeling zonder tooa sorteren kunt implementeren code van de activiteit. Hallo aanbevolen procedure is een speciale foutafhandeling runbook met algemene functionaliteit toocreate, maar dit is niet verplicht. Foutafhandeling logica in een PowerShell-code-activiteit is het niet alleen optie Hallo.  

Bijvoorbeeld: overweeg een runbook dat toostart probeert een virtuele machine en een toepassing installeert op deze. Als hello virtuele machine niet correct wordt gestart, worden twee acties uitgevoerd:

1. Er wordt een melding over dit probleem verzonden.
2. Er wordt een ander runbook gestart dat in plaats hiervan automatisch een nieuwe VM inricht.

Een oplossing toohave is een fout-koppeling die verwijst tooan activiteit ingangen stap 1. Bijvoorbeeld, u verbinding kan maken van Hallo **Write-Warning** cmdlet tooan activiteit voor stap 2, zoals Hallo **Start AzureRmAutomationRunbook** cmdlet.

U kan ook dit gedrag voor gebruik in runbooks met veel generalize door de gegevens van deze twee activiteiten in een afzonderlijk foutbericht verwerking runbook en de volgende Hallo richtlijnen eerder voorgesteld. Voordat u dit runbook foutafhandeling, kan u een aangepast bericht van Hallo-gegevens in de oorspronkelijke runbook Hallo maken en vervolgens doorgeven als een parameter toohello foutafhandeling runbook.

## <a name="how-toouse-error-handling"></a>Hoe toouse foutafhandeling

Elke activiteit heeft een configuratie-instellingen waarmee van uitzonderingen niet-afsluitfouten worden gemaakt. Deze instelling is standaard uitgeschakeld. Het is raadzaam dat u deze instelling inschakelt op een activiteit waarvoor toohandle fouten.  

Als u deze configuratie inschakelt, worden u zodat zeker zowel wordt beëindigd als niet wordt beëindigd fouten in de Hallo activiteit worden behandeld als fouten niet wordt beëindigd en kunnen worden verwerkt met de koppeling van een fout.  

Nadat u deze instelling configureert, moet u een activiteit die verantwoordelijk is voor Hallo fout maken. Als een activiteit een fout produceert, vervolgens Hallo uitgaande fout koppelingen worden gevolgd en Hallo reguliere koppelingen zijn niet, zelfs als Hallo activiteit ook reguliere uitvoer produceert.<br><br> ![Voorbeeld van foutkoppeling voor Automation-runbook](media/automation-runbook-graphical-error-handling/error-link-example.png)

Een runbook haalt in Hallo voorbeeld te volgen, een variabele die Hallo computernaam van een virtuele machine bevat. Wordt geprobeerd toostart Hallo virtuele machine met de volgende activiteit Hallo.<br><br> ![Voorbeeld van foutafhandeling in Automation-runbook](media/automation-runbook-graphical-error-handling/runbook-example-error-handling.png)<br><br>      

Hallo **Get-AutomationVariable** activiteit en **Start-AzureRmVm** geconfigureerde tooconvert uitzonderingen tooerrors zijn.  Als er zijn problemen bij het gebruik van Hallo variabele of begin Hallo VM en fouten gegenereerd.<br><br> ![Activiteitsinstellingen voor foutafhandeling in Automation-runbook](media/automation-runbook-graphical-error-handling/activity-blade-convertexception-option.png)

Fout koppelingen stromen van deze activiteiten van één tooa **fout management** activiteit (een code-activiteit). Deze activiteit is geconfigureerd met een eenvoudige PowerShell-expressie die gebruikmaakt van Hallo *Throw* sleutelwoord toostop verwerking, samen met *$Error.Exception.Message* tooget Hallo-bericht met een beschrijving van Hallo huidige uitzondering.<br><br> ![Codevoorbeeld voor foutafhandeling in Automation-runbook](media/automation-runbook-graphical-error-handling/runbook-example-error-handling-code.png)


## <a name="next-steps"></a>Volgende stappen

* Zie toolearn meer informatie over koppelingen en koppelingstypen in de grafische runbooks [grafisch ontwerpen in Azure Automation](automation-graphical-authoring-intro.md#links-and-workflow).

* meer over de uitvoering van runbook, hoe toomonitor runbooktaken en andere technische details, Zie toolearn [bijhouden van een runbooktaak](automation-runbook-execution.md).
