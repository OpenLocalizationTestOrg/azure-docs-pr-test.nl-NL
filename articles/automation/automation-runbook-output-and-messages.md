---
title: aaaRunbook uitvoer en berichten in Azure Automation | Microsoft Docs
description: Beschrijving van hoe de uitvoer van toocreate en ophalen en de fout van berichten van runbooks in Azure Automation.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 13a414f5-0e2c-4be2-9558-a3e3ec84b6b2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: magoedte;bwren
ms.openlocfilehash: c1505fa889473766bfa47e43aaed2449d60ad851
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-output-and-messages-in-azure-automation"></a>Runbookuitvoer en -berichten in Azure Automation
De meeste Azure Automation-runbooks hebben een vorm van uitvoer, zoals een fout bericht toohello gebruiker of een complex object dat bedoeld toobe gebruikt door een andere werkstroom. Windows PowerShell biedt [meerdere streams](http://blogs.technet.com/heyscriptingguy/archive/2014/03/30/understanding-streams-redirection-and-write-host-in-powershell.aspx) toosend uitvoer van een script of een werkstroom. Azure Automation anders werkt met elk van deze stromen en u moet volgen aanbevolen procedures voor het toouse elke tijdens het maken van een runbook.

Hallo volgende tabel bevat een korte beschrijving van elke Hallo stromen en hun gedrag in hello Azure-beheerportal bij het uitvoeren van een gepubliceerd runbook en wanneer [testen van een runbook](automation-testing-runbook.md). In de volgende secties vindt u meer informatie over elke stroom.

| Stroom | Beschrijving | Gepubliceerd | Test |
|:--- |:--- |:--- |:--- |
| Uitvoer |Objecten die zijn bedoeld toobe verbruikt door andere runbooks. |Toohello Taakgeschiedenis geschreven. |In het deelvenster Testuitvoer Hallo weergegeven. |
| Waarschuwing |Waarschuwingsbericht bedoeld voor Hallo-gebruiker. |Toohello Taakgeschiedenis geschreven. |In het deelvenster Testuitvoer Hallo weergegeven. |
| Fout |Foutbericht bedoeld voor Hallo-gebruiker. In tegenstelling tot een uitzondering blijft Hallo runbook standaard na een foutbericht weergegeven. |Toohello Taakgeschiedenis geschreven. |In het deelvenster Testuitvoer Hallo weergegeven. |
| Uitgebreide |Berichten algemene of foutopsporing informatie opgeeft. |Alleen toojob geschiedenis geschreven als uitgebreide logboekregistratie is ingeschakeld voor Hallo runbook. |In het deelvenster van de uitvoer van de Test Hallo weergegeven alleen als $VerbosePreference tooContinue in Hallo runbook is ingesteld. |
| Voortgang |Records automatisch gegenereerd voor en na elke activiteit in Hallo runbook. Hallo runbook moet niet proberen toocreate eigen voortgangsrecords omdat deze zijn bedoeld voor een interactieve gebruiker. |Alleen toojob geschiedenis geschreven als voortgangslogboekregistratie is ingeschakeld voor Hallo runbook. |Niet weergegeven in het deelvenster Testuitvoer Hallo. |
| Fouten opsporen |Berichten die zijn bedoeld voor een interactieve gebruiker. Mag niet worden gebruikt in runbooks. |Geschiedenis van toojob niet geschreven. |Niet tooTest deelvenster Testuitvoer geschreven. |

## <a name="output-stream"></a>Uitvoerstroom
Hallo-uitvoerstroom is bedoeld voor de uitvoer van objecten die zijn gemaakt door een script of een werkstroom wanneer deze correct wordt uitgevoerd. In Azure Automation wordt deze stroom voornamelijk gebruikt voor objecten die zijn bedoeld toobe verbruikt door [bovenliggende runbooks die Hallo huidige runbook aanroepen](automation-child-runbooks.md). Wanneer u [een runbook inline aanroept](automation-child-runbooks.md#invoking-a-child-runbook-using-inline-execution) vanuit een runbook bovenliggende gegevens worden geretourneerd van Hallo uitvoer stroom toohello bovenliggende. U moet Hallo uitvoer stroom toocommunicate algemene informatie terug toohello gebruiker alleen gebruiken als u weet Hallo runbook wordt nooit aangeroepen door een ander runbook. Als een best practice, echter, moet u doorgaans gebruiken Hallo [uitgebreide stroom](#Verbose) toocommunicate algemene informatie toohello gebruiker.

U kunt schrijven gegevens toohello uitvoer stream met [Write-Output](http://technet.microsoft.com/library/hh849921.aspx) of door het Hallo-object in een eigen regel in Hallo runbook plaatsen.

    #hello following lines both write an object toohello output stream.
    Write-Output –InputObject $object
    $object

### <a name="output-from-a-function"></a>Uitvoer van een functie
Wanneer u toohello uitvoerstroom in een functie die is opgenomen in uw runbook schrijven, Hallo uitvoer back toohello runbook doorgegeven. Als Hallo runbook die uitvoer tooa variabele toewijst, wordt deze niet toohello uitvoerstroom geschreven. Schrijven tooany andere stromen vanuit Hallo functie schrijft toohello bijbehorende stroom voor Hallo runbook.

Overweeg het volgende voorbeeldrunbook Hallo.

    Workflow Test-Runbook
    {
        Write-Verbose "Verbose outside of function" -Verbose
        Write-Output "Output outside of function"
        $functionOutput = Test-Function
        $functionOutput

    Function Test-Function
     {
        Write-Verbose "Verbose inside of function" -Verbose
        Write-Output "Output inside of function"
      }
    }


de uitvoerstroom Hallo voor Hallo runbooktaak zou zijn:

    Output inside of function
    Output outside of function

uitgebreide stroom voor de runbooktaak Hallo Hallo zou zijn:

    Verbose outside of function
    Verbose inside of function

Wanneer u Hallo runbook hebt gepubliceerd en voordat u deze starten, moet u ook uitgebreide logboekregistratie in Hallo runbookinstellingen in de volgorde tooget Hallo uitgebreide Stroomuitvoer inschakelen.

### <a name="declaring-output-data-type"></a>Declarerende uitvoer-gegevenstype
Een werkstroom kunt opgeven Hallo-gegevenstype van de uitvoer met Hallo [OutputType kenmerk](http://technet.microsoft.com/library/hh847785.aspx). Dit kenmerk heeft geen effect tijdens runtime, maar het biedt een indicatie toohello runbookauteur tijdens het ontwerpen van uitvoer van runbook Hallo Hallo verwacht. Wanneer Hallo toolset voor runbooks tooevolve blijft, wordt het belang Hallo belang van uitvoergegevenstypen in de ontwerpfase verhoogd. Als gevolg hiervan is een best practices tooinclude deze verklaring in runbooks die u maakt.

Hier volgt een lijst van voorbeeld van uitvoer typen:

* System.String
* System.Int32
* System.Collections.Hashtable
* Microsoft.Azure.Commands.Compute.Models.PSVirtualMachine

Hallo volgende voorbeeldrunbook voert een tekenreeksobject en bevat een declaratie van het uitvoertype. Als uw runbook een matrix van een bepaald type, moet u nog steeds Hallo type als matrix van het type Hallo tegengestelde tooan opgeven.

    Workflow Test-Runbook
    {
       [OutputType([string])]

       $output = "This is some string output."
       Write-Output $output
    }

toodeclare uitvoer typt in Grapical of grafische PowerShell Workflow-runbooks, kunt u Hallo **invoer en uitvoer** menuoptie en typt u de naam van de Hallo Hallo type uitvoer.  Het is raadzaam u Hallo volledig .NET-klasse naam toomake gebruiken deze gemakkelijk kan worden geïdentificeerd als ernaar wordt verwezen vanuit een bovenliggend runbook.  Dit beschrijft alle Hallo-eigenschappen van de gegevensbus van die klasse toohello in Hallo runbook en biedt een grote flexibiliteit bij gebruik van deze voor voorwaardelijke logica, logboekregistratie en het verwijzen naar als waarden voor andere activiteiten in Hallo runbook.<br> ![Runbook-invoer en uitvoer-optie](media/automation-runbook-output-and-messages/runbook-menu-input-and-output-option.png)

In de Hallo voorbeeld te volgen, hebben we twee grafische runbooks toodemonstrate deze functie.  Als we Hallo modulaire runbook ontwerpmodel toepast, hebben we een runbook dat als Hallo fungeert *verificatie runbooksjabloon* het beheren van verificatie met behulp van Azure Hallo Run As-account.  Ons runbook tweede, die normaal Hallo core logica tooautomate een bepaald scenario kunt uitvoeren, in dit geval gaat tooexecute hello *verificatie runbooksjabloon* en weer te geven Hallo resultaten tooyour **Test** deelvenster Uitvoer.  Onder normale omstandigheden hebben we dit runbook iets op basis van een resource van Hallo uitvoer van Hallo onderliggend runbook te doen.    

Hier volgt de basislogica Hallo Hallo **AuthenticateTo Azure** runbook.<br> ![Voorbeeld van de Runbook-sjabloon verifiëren](media/automation-runbook-output-and-messages/runbook-authentication-template.png).  

Het uitvoertype Hallo omvat *Microsoft.Azure.Commands.Profile.Models.PSAzureContext*, die wordt geretourneerd profieleigenschappen Hallo-verificatie.<br> ![Voorbeeld van uitvoer van de Runbook-Type](media/automation-runbook-output-and-messages/runbook-input-and-output-add-blade.png) 

Dit runbook is eenvoudig doorsturen, maar er is een configuratie-item toocall hier af.  de laatste activiteit Hallo Hallo voert **Write-Output** cmdlet- en schrijfbewerkingen profiel gegevens tooa $_ variabele met een PowerShell-expressie voor Hallo Hallo **Inputobject** parameter, die vereist voor die is cmdlet.  

Voor het tweede runbook Hallo in dit voorbeeld, met de naam *Test ChildOutputType*, we gewoon twee activiteiten hebben.<br> ![Voorbeeld van de onderliggende uitvoer Type Runbook](media/automation-runbook-output-and-messages/runbook-display-authentication-results-example.png) 

de eerste activiteit Hallo Hallo roept **AuthenticateTo Azure** runbook en Hallo tweede activiteit wordt uitgevoerd Hallo **Write-Verbose** cmdlet Hello **gegevensbron** van  **Uitvoer van activiteit** en Hallo-waarde voor **pad naar veld** is **Context.Subscription.SubscriptionName**, die is opgeven van Hallo context uitvoer van Hallo  **AuthenticateTo Azure** runbook.<br> ![Write-Verbose cmdlet Parameter-gegevensbron](media/automation-runbook-output-and-messages/runbook-write-verbose-parameters-config.png)    

de resulterende uitvoer Hallo is Hallo-naam van het Hallo-abonnement.<br> ![Test ChildOutputType Runbookresultaten](media/automation-runbook-output-and-messages/runbook-test-childoutputtype-results.png)

Een opmerking over de werking van Hallo Hallo Type uitvoer-besturingselement.  Wanneer u een waarde in Hallo uitvoertype veld op Hallo invoer en uitvoer eigenschappenblade typt, hebben tooclick buiten Hallo besturingselement nadat u, in volgorde voor de vermelding toobe herkend door het Hallo-besturingselement.  

## <a name="message-streams"></a>Berichtstromen
In tegenstelling tot Hallo uitvoerstroom zijn berichtstromen beoogde toocommunicate informatie toohello gebruiker. Er zijn meerdere berichtstromen voor verschillende soorten informatie en elk wordt anders afgehandeld door Azure Automation.

### <a name="warning-and-error-streams"></a>Waarschuwings- en foutstromen
Hallo waarschuwings- en foutstromen zijn bedoeld toolog problemen die in een runbook optreden. Ze worden toohello Taakgeschiedenis geschreven wanneer een runbook wordt uitgevoerd en zijn opgenomen in het deelvenster Testuitvoer Hallo in hello Azure-beheerportal wanneer een runbook wordt getest. Standaard blijft Hallo runbook uitvoering na een waarschuwing of fout. U kunt opgeven dat runbook Hallo op een waarschuwing of fout moet worden onderbroken door een [voorkeursvariabele](#PreferenceVariables) in Hallo runbook voordat het Hallo-bericht. Bijvoorbeeld, toocause een runbook toosuspend op een fout als een uitzondering ingesteld **$ErrorActionPreference** tooStop.

Een waarschuwing of fout bericht maken met Hallo [Write-Warning](https://technet.microsoft.com/library/hh849931.aspx) of [Write-Error](http://technet.microsoft.com/library/hh849962.aspx) cmdlet. Activiteiten mogen ook toothese stromen schrijven.

    #hello following lines create a warning message and then an error message that will suspend hello runbook.

    $ErrorActionPreference = "Stop"
    Write-Warning –Message "This is a warning message."
    Write-Error –Message "This is an error message that will stop hello runbook because of hello preference variable."

### <a name="verbose-stream"></a>Uitgebreide stroom
Hallo uitgebreide berichtenstroom is bedoeld voor algemene informatie over de runbookwerking Hallo. Sinds Hallo [foutopsporingsstroom](#Debug) is niet beschikbaar in een runbook uitgebreide berichten moeten worden gebruikt voor gegevens voor foutopsporing. Standaard worden uitgebreide berichten uit gepubliceerde runbooks niet opgeslagen in de taakgeschiedenis Hallo. uitgebreide berichten toostore, configureren gepubliceerde runbooks tooLog uitgebreide Records op tabblad voor het configureren van Hallo runbook in Azure Management Portal Hallo Hallo. In de meeste gevallen moet u de standaardinstelling Hallo van logboekregistratie van uitgebreide records voor een runbook uit prestatieoverwegingen niet behouden. Schakel deze optie alleen tootroubleshoot of fouten opsporen in een runbook.

Wanneer [testen van een runbook](automation-testing-runbook.md), uitgebreide berichten worden niet weergegeven als Hallo runbook geconfigureerde toolog uitgebreide records. uitgebreide berichten tijdens toodisplay [testen van een runbook](automation-testing-runbook.md), moet u de variabele tooContinue hello $VerbosePreference instellen. Met deze variabele is ingesteld, wordt uitgebreide berichten weergegeven in het deelvenster Testuitvoer van hello Azure-portal Hallo.

Een uitgebreide bericht maken met Hallo [Write-Verbose](http://technet.microsoft.com/library/hh849951.aspx) cmdlet.

    #hello following line creates a verbose message.

    Write-Verbose –Message "This is a verbose message."

### <a name="debug-stream"></a>Foutopsporingsstroom
Hallo foutopsporingsstroom is bedoeld voor gebruik met een interactieve gebruiker en mag niet worden gebruikt in runbooks.

## <a name="progress-records"></a>Voortgangsrecords
Als u configureert de voortgang van een runbook toolog registreert (op Hallo configureren tabblad van Hallo runbook in hello Azure-portal), wordt een record wordt toohello Taakgeschiedenis worden geschreven voordat en nadat elke activiteit is uitgevoerd. In de meeste gevallen moet u de standaardinstelling Hallo van logboekregistratie van voortgangsrecords voor een runbook niet in de volgorde toomaximize prestaties behouden. Schakel deze optie alleen tootroubleshoot of fouten opsporen in een runbook. Bij het testen van een runbook worden voortgangsberichten niet weergegeven als Hallo runbook geconfigureerde toolog voortgangsrecords.

Hallo [Write-Progress](http://technet.microsoft.com/library/hh849902.aspx) cmdlet is niet geldig in een runbook, omdat deze is bedoeld voor gebruik met een interactieve gebruiker.

## <a name="preference-variables"></a>Voorkeursvariabelen
Maakt gebruik van Windows PowerShell [voorkeursvariabelen](http://technet.microsoft.com/library/hh847796.aspx) toodetermine hoe toorespond toodata verzonden toodifferent uitvoerstromen. U kunt deze variabelen instellen in een runbook toocontrol hoe zal reageren toodata verzonden naar verschillende stromen.

Hallo bevat volgende tabel Hallo-voorkeursvariabelen die kunnen worden gebruikt in runbooks met hun geldige en standaardwaarden. Houd er rekening mee dat deze tabel alleen Hallo-waarden die geldig in een runbook zijn bevat. Er zijn aanvullende waarden geldig voor Hallo voorkeursvariabelen bij gebruik in Windows PowerShell buiten Azure Automation.

| Variabele | Standaardwaarde | Geldige waarden |
|:--- |:--- |:--- |
| WarningPreference |Doorgaan |Stoppen<br>Doorgaan<br>SilentlyContinue |
| ErrorActionPreference |Doorgaan |Stoppen<br>Doorgaan<br>SilentlyContinue |
| VerbosePreference |SilentlyContinue |Stoppen<br>Doorgaan<br>SilentlyContinue |

Hallo volgende tabel geeft een lijst Hallo-gedrag voor Hallo voorkeursvariabelewaarden die geldig in runbooks zijn.

| Waarde | Gedrag |
|:--- |:--- |
| Doorgaan |Registreert het Hallo-bericht en blijft Hallo runbook uitvoeren. |
| SilentlyContinue |Blijft Hallo runbook uitvoeren zonder de logboekregistratie van het Hallo-bericht. Dit heeft Hallo effect van het Hallo-bericht wordt genegeerd. |
| Stoppen |Registreert het Hallo-bericht en Hallo runbook wordt onderbroken. |

## <a name="retrieving-runbook-output-and-messages"></a>Runbookuitvoer en -berichten ophalen
### <a name="azure-portal"></a>Azure Portal
U kunt Hallo details van een runbooktaak weergeven in hello Azure-portal op Hallo taken tabblad van een runbook. Hallo samenvatting van de taak Hallo Hallo invoerparameters en Hallo weergegeven [uitvoerstroom](#Output) in aanvullende toogeneral informatie over Hallo taak en eventuele uitzonderingen als ze zich heeft voorgedaan. Hallo geschiedenis bevat berichten van Hallo [uitvoerstroom](#Output) en [waarschuwings- en Foutstromen](#WarningError) in toevoeging toohello [uitgebreide stroom](#Verbose) en [uitgevoerd Records](#Progress) als Hallo runbook geconfigureerd toolog uitgebreide records en voortgangsrecords is.

### <a name="windows-powershell"></a>Windows Powershell
In Windows PowerShell, kunt u uitvoer en berichten ophalen vanuit een runbook met behulp van Hallo [Get-AzureAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) cmdlet. Deze cmdlet vereist Hallo Hallo taak-ID en heeft een parameter genaamd stroom waarin u welke stroom tooreturn opgeeft. U kunt tooreturn alle stromen voor Hallo taak opgeven.

Hallo volgende voorbeeld start een voorbeeldrunbook en vervolgens wacht op het toocomplete. Zodra de voltooid, wordt de uitvoerstroom van Hallo taak verzameld.

    $job = Start-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook"

    $doLoop = $true
    While ($doLoop) {
       $job = Get-AzureRmAutomationJob -ResourceGroupName "ResourceGroup01" `
       –AutomationAccountName "MyAutomationAccount" -Id $job.JobId
       $status = $job.Status
       $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped")
    }

    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" -Id $job.JobId –Stream Output

### <a name="graphical-authoring"></a>Grafisch ontwerpen
Extra logboekregistratie is voor grafische runbooks beschikbaar zijn in de vorm Hallo activiteitenniveau tracering.  Er zijn twee niveaus van tracering: Basic en gedetailleerde.  In Basic tracering ziet u Hallo starten en eindtijd van elke activiteit in Hallo runbook plus informatie tooany activiteit nieuwe pogingen, zoals het aantal pogingen en de begintijd van activiteit Hallo gerelateerd.  In de gedetailleerde tracering krijgt u Basic tracering plus invoer- en uitvoergegevens voor elke activiteit.  Houd er rekening mee dat momenteel Hallo trace records worden geschreven met uitgebreide stroom hello, zodat u uitgebreide logboekregistratie wanneer u tracering inschakelt moet inschakelen.  Voor grafische runbooks met tracering ingeschakeld hoeft niet toolog voortgangsrecords, omdat Hallo Basic tracering fungeert Hallo hetzelfde doel en meer informatieve.

![Grafisch ontwerpen taak Streams weergeven](media/automation-runbook-output-and-messages/job-streams-view-blade.png)

U ziet van Hallo bovenstaande schermafbeelding dat wanneer u uitgebreide logboekregistratie en tracering voor grafische runbooks inschakelt, veel meer informatie beschikbaar is in Hallo productie die taak Streams weergeven.  Deze extra informatie kan essentieel zijn voor het oplossen van productieproblemen met een runbook, en daarom moet u alleen deze inschakelen voor dit doel en niet als over het algemeen.    
Hallo Trace records kunnen worden met name talrijke.  U tracering ophalen twee toofour records per activiteit, afhankelijk van of u de basisindeling of gedetailleerde tracering hebt geconfigureerd met grafisch runbook.  Tenzij u deze informatie tootrack Hallo voortgang van een runbook voor het oplossen van problemen moet, kunt u tookeep die tracering is uitgeschakeld.

**tooenable activiteitenniveau tracering, Hallo stappen uitvoeren.**

1. Open uw Automation-account in Azure Portal hello.
2. Klik op Hallo **Runbooks** tegel tooopen Hallo lijst van runbooks.
3. Klik op Hallo Runbooks blade tooselect grafisch runbook uit de lijst met runbooks.
4. Op Hallo blade van de instellingen voor runbook Hallo geselecteerd, klikt u op **logboekregistratie en tracering**.
5. Hallo logboekregistratie en tracering blade onder uitgebreide records in het logboek, klik op **op** tooenable uitgebreide logboekregistratie en tracering van udner activiteitenniveau Hallo traceerniveau ook wijzigen**Basic** of **gedetailleerd**  op basis van Hallo tracering die u nodig hebt.<br>
   
   ![Grafisch ontwerpen logboekregistratie en tracering Blade](media/automation-runbook-output-and-messages/logging-and-tracing-settings-blade.png)

### <a name="microsoft-operations-management-suite-oms-log-analytics"></a>Microsoft Operations Management Suite (OMS) Log Analytics
Automatisering kan de runbook-taak status en taak streams tooyour Microsoft Operations Management Suite (OMS) werkruimte voor logboekanalyse verzenden.  U kunt met Log Analytics,

* Inzicht verkrijgen in uw Automation-taken 
* Trigger een e-mailadres of de waarschuwing op basis van de status van de taak runbook (bijvoorbeeld mislukte of onderbroken) 
* Geavanceerde query's in uw taak stromen schrijven 
* Taken correleren via Automation-accounts 
* De taakgeschiedenis visualiseren gedurende een periode    

Zie voor meer informatie over hoe tooconfigure integratie met logboekanalyse toocollect, afstemmen en taakgegevens ondernemen [taakstatus en taak streams doorsturen van Automation tooLog logboekanalyse (OMS)](automation-manage-send-joblogs-log-analytics.md).

## <a name="next-steps"></a>Volgende stappen
* meer over de uitvoering van runbook, hoe toomonitor runbooktaken en andere technische details, Zie toolearn [een runbooktaak bijhouden](automation-runbook-execution.md)
* hoe toodesign en gebruik onderliggende runbooks zien toounderstand [onderliggende runbooks in Azure Automation](automation-child-runbooks.md)

