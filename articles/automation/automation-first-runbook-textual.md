---
title: aaaMy eerste PowerShell Workflow-runbook in Azure Automation | Microsoft Docs
description: Zelfstudie die u bij Hallo maken helpt, testen en publiceren van een eenvoudig tekstrunbook met behulp van PowerShell-werkstroom.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: powershell-werkstroom, voorbeelden powershell-werkstroom, werkstroom powershell
ms.assetid: 0002d7f7-e2b5-46e3-b5eb-4596b84fd526
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/26/2017
ms.author: magoedte;bwren
ms.openlocfilehash: b5a34d363ef4865878f3f68119833367b5280f83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-powershell-workflow-runbook"></a>Mijn eerste PowerShell Workflow-runbook

> [!div class="op_single_selector"]
> * [Grafisch](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [PowerShell-werkstroom](automation-first-runbook-textual.md)
> 
> 

Deze zelfstudie wordt u begeleid Hallo maken van een [PowerShell Workflow-runbook](automation-runbook-types.md#powershell-workflow-runbooks) in Azure Automation. We beginnen met een eenvoudig runbook dat we testen en publiceren terwijl waarin wordt uitgelegd hoe tootrack status van de runbooktaak Hallo Hallo. Vervolgens wijzigt u Hallo runbook tooactually Azure-resources, in dit geval starten van een virtuele machine in Azure beheren. Ten slotte maken we Hallo runbook krachtiger door runbookparameters toe te voegen.

## <a name="prerequisites"></a>Vereisten
toocomplete in deze zelfstudie, moet u hello te volgen:

* Azure-abonnement. Als u nog geen abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of <a href="/pricing/free-account/" target="_blank">[u aanmelden voor een gratis account](https://azure.microsoft.com/free/).
* [Automation-account](automation-sec-configure-azure-runas-account.md) toohold Hallo runbook en tooAzure bronnen te verifiëren.  Dit account moet hebben machtiging toostart en stop Hallo virtuele machine.
* Een virtuele machine van Azure. We stoppen en starten deze machine, dus het mag geen productiemachine zijn.

## <a name="step-1---create-new-runbook"></a>Stap 1: nieuw runbook maken
We beginnen met het maken van een eenvoudig runbook waarmee de tekst hello *Hallo wereld*.

1. Open uw Automation-account in hello Azure-portal.  
   Hallo Automation-accountpagina vindt u een snelle weergave van Hallo resources in dit account. U hebt als het goed is al enkele assets. De meeste van deze zijn Hallo-modules die automatisch zijn opgenomen in een nieuw automatiseringsaccount. U hebt ook Hallo referentie-element dat wordt vermeld in Hallo [vereisten](#prerequisites).
2. Klik op Hallo **Runbooks** tegel tooopen Hallo lijst van runbooks.<br><br> ![Besturingselement Runbooks](media/automation-first-runbook-textual/runbooks-control-tiles.png)
3. Maak een nieuw runbook door te klikken op Hallo **een runbook toevoegen** knop en vervolgens **een nieuw runbook maken**.
4. Hallo Hallo runbooknaam geven *MyFirstRunbook-Workflow*.
5. In dit geval gaan we toocreate een [PowerShell Workflow-runbook](automation-runbook-types.md#powershell-workflow-runbooks) dus selecteer **Powershell Workflow** voor **runbooktype**.<br><br> ![Nieuw runbook](media/automation-first-runbook-textual/new-runbook-properties.png)
6. Klik op **maken** toocreate Hallo runbook en open Hallo teksteditor.

## <a name="step-2---add-code-toohello-runbook"></a>Stap 2: code toohello runbook toevoegen
U kunt de code rechtstreeks in runbook hello, of u kunt cmdlets, runbooks en assets selecteren van Hallo besturingselement bibliotheek en deze toohello runbook met eventuele gerelateerde parameters toegevoegd. Voor dit overzicht typen we rechtstreeks in Hallo runbook.

1. Ons runbook is momenteel leeg met alleen Hallo vereist *werkstroom* sleutelwoord, Hallo-naam van ons runbook en Hallo accolades die Hallo volledige werkstroom omsluiten.

   ```
   Workflow MyFirstRunbook-Workflow
   {
   }
   ```
2. Typ *Write-Output "Hallo wereld".* tussen accolades Hallo.

   ```
   Workflow MyFirstRunbook-Workflow
   {
   Write-Output "Hello World"
   }
   ```
3. Hallo runbook door te klikken op Opslaan **opslaan**.<br><br> ![Runbook opslaan](media/automation-first-runbook-textual/automation-runbook-edit-controls-save.png)

## <a name="step-3---test-hello-runbook"></a>Stap 3 - runbook-Test Hallo
Voordat we Hallo runbook toomake publiceert deze beschikbaar is in productie, willen we tootest het toomake ervoor dat deze goed werkt. Wanneer u een runbook test, voert u de **concept**versie uit en geeft u de uitvoer interactief weer.

1. Klik op **testvenster** tooopen Hallo testvenster.<br><br> ![Testvenster](media/automation-first-runbook-textual/automation-runbook-edit-controls-test.png)
2. Klik op **Start** toostart Hallo test. Dit moet Hallo alleen ingeschakelde optie zijn.
3. Een [runbooktaak](automation-runbook-execution.md) wordt gemaakt en de status ervan wordt weergegeven.  
   Hallo taakstatus wordt gestart als *in de wachtrij geplaatst* die aangeeft dat er wordt gewacht tot een runbook worker in Hallo cloud toocome beschikbaar. Verandert daarna te*starten* wanneer een werknemer claims Hallo taak, en vervolgens *met* wanneer Hallo runbook daadwerkelijk wordt uitgevoerd.  
4. Wanneer de runbooktaak Hallo is voltooid, wordt de uitvoer ervan weergegeven. In ons geval zouden we *Hallo wereld* moeten zien.<br><br> ![Hello World](media/automation-first-runbook-textual/test-output-hello-world.png)
5. Hallo Test deelvenster tooreturn toohello canvas te sluiten.

## <a name="step-4---publish-and-start-hello-runbook"></a>Stap 4: publiceer en Hallo runbook starten
Hallo runbook dat we zojuist hebben gemaakt is nog steeds in de modus concept. We moeten toopublish voordat we het in productie kunnen uitvoeren. Wanneer u een runbook publiceert, kunt u de bestaande gepubliceerde versie Hallo overschrijven met Hallo conceptversie. In ons geval nog we geen gepubliceerde versie omdat we Hallo runbook zojuist hebben gemaakt.

1. Klik op **publiceren** toopublish hello runbook en vervolgens **Ja** wanneer u wordt gevraagd.<br><br> ![Publiceren](media/automation-first-runbook-textual/automation-runbook-edit-controls-publish.png)
2. Als u links tooview hello runbook in Hallo schuift **Runbooks** deelvenster nu wordt het weergegeven een **ontwerpstatus** van **gepubliceerde**.
3. Schuif terug toohello rechts tooview Hallo deelvenster voor **MyFirstRunbook-Workflow**.  
   Hallo opties Hallo bovenaan kunnen we toostart hello runbook, toostart op een bepaald moment in toekomstige Hallo plannen of maken een [webhook](automation-webhooks.md) zodat het kan worden gestart via een HTTP-aanroep.
4. We willen dat net toostart hello runbook hiervoor klikt u op **Start** en vervolgens **Ja** wanneer u wordt gevraagd.<br><br> ![Runbook starten](media/automation-first-runbook-textual/automation-runbook-controls-start.png)
5. Een taakdeelvenster wordt geopend voor Hallo runbooktaak die we zojuist hebben gemaakt. We kunnen dit deelvenster sluiten, maar in dit geval laten we het open zodat we de voortgang van Hallo taak kunnen bekijken.
6. Hallo taakstatus wordt weergegeven **taakoverzicht** en komt overeen met de statuswaarden die we zagen wanneer we Hallo runbook getest Hallo.<br><br> ![Taakoverzicht](media/automation-first-runbook-textual/job-pane-status-blade-jobsummary.png)
7. Eenmaal Hallo runbook status bevat *voltooid*, klikt u op **uitvoer**. deelvenster Hallo-uitvoer wordt geopend en we zien onze *Hallo wereld*.<br><br> ![Taakoverzicht](media/automation-first-runbook-textual/job-pane-status-blade-outputtile.png)  
8. Deelvenster sluiten Hallo-uitvoer.
9. Klik op **alle logboeken** tooopen Hallo-deelvenster voor Streams voor de runbooktaak Hallo. Zien we alleen *Hallo wereld* in Hallo uitvoer, maar er kan weergeven andere stromen voor een runbooktaak zoals uitgebreid en fout als Hallo runbook toothem schrijft.<br><br> ![Taakoverzicht](media/automation-first-runbook-textual/job-pane-status-blade-alllogstile.png)
10. Sluit de deelvenster Streams Hallo en Hallo taak tooreturn toohello MyFirstRunbook deelvenster.
11. Klik op **taken** tooopen Hallo taken deelvenster voor dit runbook. Hiermee worden alle Hallo-taken die zijn gemaakt met dit runbook. We ziet slechts één taak vermeld aangezien we Hallo taak slechts één keer uitgevoerd.<br><br> ![Taken](media/automation-first-runbook-textual/runbook-control-job-tile.png)
12. U kunt klikken op deze taak tooopen Hallo dezelfde taakdeelvenster die we hebben bekeken toen we Hallo-runbook gestart. Hiermee kunt u toogo terug in tijd en bekijkt hello details van elke taak die is gemaakt voor een bepaald runbook.

## <a name="step-5---add-authentication-toomanage-azure-resources"></a>Stap 5: verificatie toomanage toevoegen Azure-resources
We hebben ons runbook getest en gepubliceerd, maar tot nu toe doet het nog niets nuttigs. We willen toohave het Azure-resources beheren. Het zal niet kunnen toodo Hoewel tenzij we het laten verifiëren tooin Hallo met Hallo-referenties die zijn aangeduid [vereisten](#prerequisites). We doen dat met Hallo **Add-AzureRMAccount** cmdlet.

1. Open Hallo teksteditor door te klikken op **bewerken** in deelvenster Hallo MyFirstRunbook-Workflow.<br><br> ![Runbook bewerken](media/automation-first-runbook-textual/automation-runbook-controls-edit.png)
2. We hebben Hallo **Write-Output** meer regel, dus opwekken en verwijder deze.
3. Plaats Hallo cursor op een lege regel tussen accolades Hallo.
4. Typ of kopieer en plak Hallo code die wordt afgehandeld Hallo verificatie met uw Automation Run As-account te volgen:

   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   ```
5. Klik op **testvenster** zodat we Hallo runbook kunnen testen.
6. Klik op **Start** toostart Hallo test. Nadat deze is voltooid, ontvangt u uitvoer vergelijkbare toohello te volgen, om basisinformatie uit uw account weer te geven. Dit bevestigt dat Hallo referentie geldig is.<br><br> ![Verifiëren](media/automation-first-runbook-textual/runbook-auth-output.png)

## <a name="step-6---add-code-toostart-a-virtual-machine"></a>Stap 6: code toostart een virtuele machine toevoegen
Nu dat ons runbook tooour Azure-abonnement verifieert, kunnen we resources beheren. We voegen een opdracht toostart een virtuele machine. U kunt een virtuele machine kiezen in uw Azure-abonnement en nu worden we hardcoderen deze naam in Hallo runbook.

1. Na *Add-AzureRmAccount*, type *Start-AzureRmVM-Name 'VMName' - ResourceGroupName 'NameofResourceGroup'* hello en naam van de resourcegroep van Hallo virtuele machine toostart bieden.  

   ```
   workflow MyFirstRunbook-Workflow
   {
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'ResourceGroupName'
   }
   ```
2. Hallo runbook opslaan en klik vervolgens op **testvenster** zodat deze kan worden getest.
3. Klik op **Start** toostart Hallo test. Nadat deze is voltooid, controleert u dat de virtuele machine Hallo is gestart.

## <a name="step-7---add-an-input-parameter-toohello-runbook"></a>Stap 7: een invoerparameter toohello runbook toevoegen
Ons runbook wordt momenteel gestart Hallo virtuele machine die we hebben hardgecodeerd in Hallo runbook, maar het zou nuttiger als we Hallo virtuele machine opgeven kan wanneer Hallo runbook wordt gestart. We toevoegen invoerparameters toohello runbook tooprovide nu dat de functionaliteit.

1. Voeg parameters voor *VMName* en *ResourceGroupName* toohello runbook en gebruik deze variabelen Hello **Start-AzureRmVM** cmdlet zoals in Hallo voorbeeld hieronder.

   ```
   workflow MyFirstRunbook-Workflow
   {
    Param(
     [string]$VMName,
     [string]$ResourceGroupName
    )  
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name $VMName -ResourceGroupName $ResourceGroupName
   }
   ```
2. Hallo runbook opslaan en openen van Hallo testvenster. Houd er rekening mee dat u kunt nu waarden opgeven voor Hallo twee invoervariabelen die wordt gebruikt in het Hallo-test.
3. Sluit Hallo testvenster.
4. Klik op **publiceren** toopublish Hallo nieuwe versie van Hallo runbook.
5. Stop Hallo virtuele machine die u in de vorige stap Hallo gestart.
6. Klik op **Start** toostart hello runbook. Type in Hallo **VMName** en **ResourceGroupName** voor Hallo virtuele machine die u toostart gaat.<br><br> ![Runbook starten](media/automation-first-runbook-textual/automation-pass-params.png)<br>  
7. Wanneer Hallo runbook is voltooid, controleert u dat de virtuele machine Hallo is gestart.  

## <a name="next-steps"></a>Volgende stappen
* Zie tooget gestart met grafische runbooks [Mijn eerste grafische runbook](automation-first-runbook-graphical.md)
* Zie tooget gestart met PowerShell-runbooks [Mijn eerste PowerShell-runbook](automation-first-runbook-textual-powershell.md)
* toolearn meer informatie over runbooktypen, hun voordelen en beperkingen, Zie [Azure Automation-runbooktypen](automation-runbook-types.md)
* Zie [Systeemeigen PowerShell-scriptondersteuning in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/) voor meer informatie over de functie voor PowerShelll-scriptondersteuning
