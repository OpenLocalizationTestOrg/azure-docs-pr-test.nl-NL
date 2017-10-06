---
title: aaaRunbook uitvoering in Azure Automation | Microsoft Docs
description: Beschrijft de details op Hallo van hoe een runbook in Azure Automation wordt verwerkt.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d10c8ce2-2c0b-4ea7-ba3c-d20e09b2c9ca
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2017
ms.author: bwren
ms.openlocfilehash: bdb535675443353d44640bc7773de3f9dac5e42c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-execution-in-azure-automation"></a>Uitvoeren van Runbook in Azure Automation
Wanneer u een runbook in Azure Automation start, wordt een taak gemaakt. Een taak is één uitvoeringsinstantie van een runbook. Een Azure Automation worker is toegewezen toorun elke taak. Werknemers worden gedeeld door meerdere Azure-accounts, zijn taken van andere Automation-accounts geïsoleerd van elkaar. U hebt geen controle over welke worker services Hallo-aanvraag voor uw project.  Één runbook kan meerdere taken tegelijk actief hebben. Wanneer u hello lijst met runbooks in hello Azure-portal bekijkt, geeft het Hallo-status van alle taken die zijn gestart voor elk runbook. U kunt Hallo lijst met taken voor elk runbook in de volgorde tootrack Hallo status van elke weergeven. Zie voor een beschrijving van status van een andere taak Hallo [status van een taak](#job-statuses).

Hallo volgende diagram toont Hallo levenscyclus van een runbooktaak voor [grafische runbooks](automation-runbook-types.md#graphical-runbooks) en [PowerShell Workflow-runbooks](automation-runbook-types.md#powershell-workflow-runbooks).

![Status van een taak - PowerShell-werkstroom](./media/automation-runbook-execution/job-statuses.png)

Hallo volgende diagram toont Hallo levenscyclus van een runbooktaak voor [PowerShell-runbooks](automation-runbook-types.md#powershell-runbooks).

![Status van een taak - PowerShell-Script](./media/automation-runbook-execution/job-statuses-script.png)

Uw taken hebben toegang tot tooyour Azure resources door het maken van een verbinding tooyour Azure-abonnement. Ze hebben alleen toegang tooresources in uw datacenter als deze bronnen toegankelijk vanaf Hallo openbare cloud zijn.

## <a name="job-statuses"></a>Status van een taak
Hallo beschrijft volgende tabel Hallo verschillende statussen die mogelijk voor een taak zijn.

| Status | Beschrijving |
|:--- |:--- |
| Voltooid |Hallo-taak is voltooid. |
| Is mislukt |Voor [grafisch en PowerShell Workflow-runbooks](automation-runbook-types.md), Hallo runbook toocompile is mislukt.  Voor [PowerShell-Script runbooks](automation-runbook-types.md), Hallo runbook toostart is mislukt of Hallo-taak is een uitzondering opgetreden. |
| Is mislukt, wacht voor bronnen |Hallo-taak is mislukt omdat het Hallo bereikt [evenredige verdeling](#fairshare) driemaal beperken en gestart vanaf dezelfde controlepunt Hallo of van Hallo begintijd van Hallo runbook elke. |
| In de wachtrij |Hallo taak wacht bronnen op een beschikbare Automation worker toocome zodat het kan worden gestart. |
| Starting |Hallo-taak is toegewezen tooa worker en Hallo systeem zich in de Hallo proces gestart. |
| Hervatten |Hallo-systeem zich in de Hallo proces van het Hallo-taak hervatten nadat deze is onderbroken. |
| Running |Hallo-taak wordt uitgevoerd. |
| Wordt uitgevoerd, wachten op resources |Hallo taak is verwijderd omdat het Hallo bereikt [evenredige verdeling](#fairshare) limiet. Het hervatten snel uit de laatste controlepunt. |
| Stopped |Hallo-taak is gestopt door gebruiker Hallo voordat deze is voltooid. |
| Stopping |Hallo-systeem zich in de Hallo proces van het Hallo-taak wordt gestopt. |
| Onderbroken |Hallo-taak is onderbroken door de gebruiker hello, door Hallo systeem of door een opdracht in Hallo runbook. Een onderbroken taak kan opnieuw worden gestart en hervat vanaf het laatste controlepunt of vanaf Hallo vanaf van Hallo runbook als er geen controlepunten. Hallo runbook zal alleen worden onderbroken door Hallo systeem wanneer er een uitzondering optreedt. ErrorActionPreference is standaard te**doorgaan**, wat betekent dat deze taak Hallo houdt uitgevoerd op een fout opgetreden. Als deze voorkeursvariabele is ingesteld, te**stoppen**, en vervolgens het Hallo-taak wordt onderbroken op een fout opgetreden.  Van toepassing is te[grafisch en PowerShell Workflow-runbooks](automation-runbook-types.md) alleen. |
| Onderbreken |Hallo-systeem probeert toosuspend Hallo taak op verzoek van de gebruiker Hallo Hallo. Hallo runbook moet het volgende controlepunt bereiken voordat deze kan worden onderbroken. Als het laatste controlepunt al doorgegeven, is voordat deze kan worden onderbroken voltooid.  Van toepassing is te[grafisch en PowerShell Workflow-runbooks](automation-runbook-types.md) alleen. |

## <a name="viewing-job-status-from-hello-azure-portal"></a>Status van hello Azure-portal weergeven
U kunt een samengevatte status van alle runbooktaken weergeven of inzoomen op gegevens van een specifieke runbooktaak in hello Azure-portal of door integratie met Microsoft Operations Management Suite (OMS) Log Analytics werkruimte tooforward runbook taak de status van uw configureren en taak stromen.  Zie voor meer informatie over de integratie met OMS Log Analytics [taakstatus en taak streams doorsturen van Automation tooLog logboekanalyse (OMS)](automation-manage-send-joblogs-log-analytics.md).  

### <a name="automation-runbook-jobs-summary"></a>Automation-runbooktaken samenvatting
Op Hallo van uw geselecteerde Automation-account, ziet u een overzicht van alle Hallo runbooktaken voor een geselecteerde Automation-account onder **taak statistieken** tegel.<br><br> ![Statistieken voor taak tegel](./media/automation-runbook-execution/automation-account-job-status-summary.png).<br> Deze tegel wordt weergegeven voor een aantal en de grafische weergave van de taakstatus Hallo voor alle taken die worden uitgevoerd.  

Hallo te klikken op de tegel Hallo geeft **taken** blade die een overzicht van alle taken die worden uitgevoerd, met de status, taakuitvoering en begin en einde tijden bevat.<br><br> ![Blade Automation-account-uptaken](./media/automation-runbook-execution/automation-account-jobs-status-blade.png)<br><br>  U kunt filteren dat Hallo lijst met taken selecteren **Filter de taken** en filter op een specifiek runbook, taakstatus, of uit de vervolgkeuzelijst hello, Hallo datum/tijd bereik toosearch binnen.<br><br> ![Status van de taak filteren](./media/automation-runbook-execution/automation-account-jobs-filter.png)

U kunt ook overzichtsgegevens voor een specifiek runbook taak weergeven door te selecteren dat runbook in Hallo **Runbooks** blade in uw Automation-account en selecteer vervolgens Hallo **taken** tegel.  Dit geeft Hallo **taken** blade en daar kunt u klikken op Hallo taak record tooview de details en de uitvoer.<br><br> ![Blade Automation-account-uptaken](./media/automation-runbook-execution/automation-runbook-job-summary-blade.png)<br> 

### <a name="job-summary"></a>Taakoverzicht
U kunt een lijst van alle Hallo-taken die zijn gemaakt voor een bepaald runbook en de meest recente status weergeven. U kunt deze lijst filteren op de taakstatus en Hallo datumbereik voor Hallo laatste wijziging toohello taak. tooview de gedetailleerde informatie en uitvoer, klik op Hallo-naam van een taak. Hallo bevat gedetailleerde weergave van de taak Hallo Hallo waarden voor Hallo runbookparameters die zijn opgegeven toothat taak.

U kunt Hallo stappen tooview Hallo taken voor een runbook te volgen.

1. Selecteer in de Azure-portal hello, **Automation** en selecteer vervolgens Hallo-naam van een Automation-account.
2. Selecteer in het Hallo-hub **Runbooks** en klik vervolgens op Hallo **Runbooks** blade selecteert u een runbook in Hallo lijst.
3. Op de blade Hallo voor runbook Hallo geselecteerd, klikt u op Hallo **taken** tegel.
4. Klik op een van de taken in de lijst Hallo Hallo en op de blade toewijzingdetails hello runbook-taak kunt u de details en de uitvoer weergeven.

## <a name="retrieving-job-status-using-windows-powershell"></a>Taakstatus ophalen met Windows PowerShell
U kunt Hallo [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) tooretrieve Hallo taken voor een runbook en Hallo details voor een bepaalde taak gemaakt. Als u een runbook met Windows PowerShell Start [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx), en vervolgens de resulterende taak Hallo wordt. Gebruik [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx)uitvoer tooget een job-uitvoer.

Hello volgende voorbeeldopdrachten Hallo laatste taak voor een voorbeeldrunbook opgehaald en toont de status, Hallo waarden opgegeven voor de Hallo runbookparameters en de uitvoer van de taak Hallo Hallo.

    $job = (Get-AzureRmAutomationJob –AutomationAccountName "MyAutomationAccount" `
    –RunbookName "Test-Runbook" -ResourceGroupName "ResourceGroup01" | sort LastModifiedDate –desc)[0]
    $job.Status
    $job.JobParameters
    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAcct" -Id $job.JobId –Stream Output

## <a name="fair-share"></a>Evenredige verdeling
In de volgorde tooshare resources tussen alle runbooks in de cloud hello, wordt Azure Automation tijdelijk elke taak geladen nadat deze actief is geweest gedurende drie uur.  Tijdens deze periode kunnen taken voor [op basis van PowerShell-runbooks](automation-runbook-types.md#powershell-runbooks) worden gestopt en wordt niet opnieuw worden gestart.  taak status bevat Hallo **gestopt**.  Dit type runbook wordt altijd opnieuw opgestart vanaf het begin van de Hallo omdat controlepunten wordt niet ondersteund.  

[PowerShell-werkstroom runbooks](automation-runbook-types.md#powershell-workflow-runbooks) wordt hervat vanaf de laatste [controlepunt](https://docs.microsoft.com/system-center/sma/overview-powershell-workflows#bk_Checkpoints).  Na het uitvoeren van drie uur zal Hallo runbooktaak worden onderbroken door het Hallo-service en de status ervan toont **uitgevoerd, wachten op resources**.  Zodra een sandbox beschikbaar, Hallo runbook wordt automatisch opnieuw opgestart door Hallo Automation-service en wordt hervat vanaf het laatste controlepunt Hallo.  Dit is normaal gedrag van de PowerShell-werkstroom voor onderbreken/opnieuw te starten.  Als Hallo runbook opnieuw groter is dan drie uur van de runtime, Hallo-proces wordt herhaald, van toothree tijden.  Na het Hallo derde opnieuw opstarten, als Hallo runbook nog niet voltooid in drie uur en vervolgens Hallo runbooktaak is mislukt en ziet u de status van de taak Hallo **mislukt, wacht resources**.  In dit geval krijgt u de volgende uitzondering met fouten in de Hallo Hallo.

*Hallo-taak kan niet worden voortgezet omdat deze meerdere keren verwijdering uit Hallo dezelfde controlepunt. Zorg ervoor dat uw Runbook heeft geen langdurige bewerkingen zonder dat de status.*

Dit is tooprotect Hallo service runbooks uitgevoerd voor onbepaalde tijd zonder te worden voltooid, omdat deze geen toomake kunnen het volgende controlepunt toohello zonder ontladen opnieuw.

Als Hallo runbook geen controlepunten heeft of Hallo-taak niet Hallo eerste controlepunt heeft bereikt voordat het wordt ongedaan gemaakt, klikt u vervolgens opnieuw wordt gestart vanaf Hallo begin.  

Wanneer u een runbook maakt, moet u ervoor zorgen dat Hallo tijd toorun activiteiten tussen de twee controlepunten niet meer dan drie uur. Mogelijk moet u tooadd controlepunten tooyour runbook tooensure dit is geen limiet drie uur of lange onderverdelen bewerkingen uitgevoerd. Uw runbook kan bijvoorbeeld een opnieuw indexeren uitvoeren op een grote SQL-database. Als deze één bewerking niet voltooid binnen Hallo evenredige share limiet, en vervolgens Hallo taak zijn verwijderd en opnieuw gestart vanaf het begin Hallo. In dit geval moet u onderverdelen Hallo opnieuw indexeren bewerking in meerdere stappen, zoals het indexeren van één tabel tegelijk, en voeg vervolgens een controlepunt na elke bewerking zodat hello taak na de laatste bewerking toocomplete Hallo hervatten kan.

## <a name="next-steps"></a>Volgende stappen
* Zie toolearn meer informatie over Hallo verschillende methoden die gebruikt toostart een runbook in Azure Automation worden kunnen [een runbook starten in Azure Automation](automation-starting-a-runbook.md)

