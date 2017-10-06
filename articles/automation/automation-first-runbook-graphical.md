---
title: aaaMy eerste grafische runbook in Azure Automation | Microsoft Docs
description: Zelfstudie die u bij Hallo maken helpt, testen en publiceren van een eenvoudig grafisch runbook.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: runbook, runbook-sjabloon, runbook-automatisering, azure-runbook
ms.assetid: dcb88f19-ed2b-4372-9724-6625cd287c8a
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/17/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 964cf8bae75ca597959bfc39b2b07c22bbc9acb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-graphical-runbook"></a>Mijn eerste grafische runbook

> [!div class="op_single_selector"]
> * [Grafisch](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [PowerShell-werkstroom](automation-first-runbook-textual.md)
> 
> 

Deze zelfstudie wordt u begeleid Hallo maken van een [grafisch runbook](automation-runbook-types.md#graphical-runbooks) in Azure Automation.  We beginnen met een eenvoudig runbook dat test en terwijl we uitleggen hoe tootrack status van de runbooktaak Hallo Hallo publiceert.  Vervolgens wijzigt u Hallo runbook tooactually Azure-resources, in dit geval starten van een virtuele machine in Azure beheren.  We vervolgens voltooien Hallo zelfstudie door het maken van Hallo runbook krachtiger door runbookparameters en voorwaardelijke koppelingen toe te voegen.

## <a name="prerequisites"></a>Vereisten
toocomplete in deze zelfstudie, moet u hello te volgen.

* Azure-abonnement.  Als u nog geen abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of <a href="/pricing/free-account/" target="_blank">[u aanmelden voor een gratis account](https://azure.microsoft.com/free/).
* [Azure Automation-account](automation-sec-configure-azure-runas-account.md) toohold Hallo runbook en tooAzure bronnen te verifiëren.  Dit account moet hebben machtiging toostart en stop Hallo virtuele machine.
* Een virtuele machine van Azure.  We stoppen en starten deze machine, dus het mag geen productiemachine zijn.

## <a name="step-1---create-runbook"></a>Stap 1: runbook maken
We beginnen met het maken van een eenvoudig runbook waarmee de tekst hello *Hallo wereld*.

1. Open uw Automation-account in hello Azure-portal.  
   Hallo Automation-accountpagina vindt u een snelle weergave van Hallo resources in dit account.  U zou al enkele assets moeten hebben.  De meeste van deze zijn Hallo-modules die automatisch zijn opgenomen in een nieuw automatiseringsaccount.  U hebt ook Hallo referentie-element dat wordt vermeld in Hallo [vereisten](#prerequisites).
2. Klik op Hallo **Runbooks** tegel tooopen Hallo lijst van runbooks.<br> ![Besturingselement Runbooks](media/automation-first-runbook-graphical/runbooks-resources-tile.png)
3. Maak een nieuw runbook door te klikken op Hallo **een runbook toevoegen** knop en vervolgens **een nieuw runbook maken**.
4. Hallo Hallo runbooknaam geven *MyFirstRunbook-Graphical*.
5. In dit geval gaan we toocreate een [grafisch runbook](automation-graphical-authoring-intro.md) dus selecteer **grafisch** voor **runbooktype**.<br> ![Nieuw runbook](media/automation-first-runbook-graphical/create-new-runbook.png)<br>
6. Klik op **maken** toocreate runbook en de grafische editor open Hallo Hallo.

## <a name="step-2---add-activities-toohello-runbook"></a>Stap 2: activiteiten toohello runbook toevoegen
het besturingselement bibliotheek aan de linkerkant van de editor Hallo HALLO hallo kunt u tooselect activiteiten tooadd tooyour runbook.  We zullen tooadd een **Write-Output** cmdlet toooutput tekst uit Hallo runbook.

1. Klik in het besturingselement bibliotheek hello, in Hallo Zoektekstvak en typ **Write-Output**.  Hallo zoekresultaten worden eronder weergegeven. <br> ![Microsoft.PowerShell.Utility](media/automation-first-runbook-graphical/search-powershell-cmdlet-writeoutput.png)
2. Schuif naar beneden toohello Hallo lijst onderaan.  U kunt ofwel met de rechtermuisknop op **Write-Output** en selecteer **toocanvas toevoegen** of klik op Hallo ellips volgende toohello cmdlet en selecteer vervolgens **toocanvas toevoegen**.
3. Klik op Hallo **Write-Output** activiteit op Hallo canvas.  Hiermee opent u Hallo besturingselementblade configuratie, zodat u tooconfigure Hallo activiteit.
4. Hallo **Label** standaard toohello-naam van cmdlet hello, maar we toosomething meer beschrijvende kunt wijzigen. Ook wijzigen*Schrijf Hallo wereld toooutput*.
5. Klik op **Parameters** tooprovide waarden voor Hallo-cmdlet-parameters.  
   Sommige cmdlets hebben meerdere parametersets, en u moet tooselect welke u één toouse. In dit geval **Write-Output** heeft slechts één parameterset, dus u niet tooselect een hoeft. <br> ![Write-Output-eigenschappen](media/automation-first-runbook-graphical/write-output-properties-b.png)
6. Selecteer Hallo **InputObject** parameter.  Dit is Hallo parameter waarin we Hallo tekst toosend toohello-uitvoerstroom opgeven.
7. In Hallo **gegevensbron** vervolgkeuzelijst **PowerShell-expressie**.  Hallo **gegevensbron** dropdown staan verschillende bronnen toopopulate een parameterwaarde te gebruiken.  
   U kunt uitvoer van deze bronnen gebruiken, zoals een andere activiteit, een Automation-asset of een PowerShell-expressie.  In dit geval wordt alleen willen we toooutput Hallo tekst *Hallo wereld*. We kunnen een PowerShell-expressie gebruiken en een tekenreeks opgeven.
8. In Hallo **expressie** in het vak *"Hallo wereld"* en klik vervolgens op **OK** tweemaal tooreturn toohello canvas.<br> ![PowerShell-expressie](media/automation-first-runbook-graphical/expression-hello-world.png)
9. Hallo runbook door te klikken op Opslaan **opslaan**.<br> ![Runbook opslaan](media/automation-first-runbook-graphical/runbook-toolbar-save-revised20165.png)

## <a name="step-3---test-hello-runbook"></a>Stap 3 - runbook-Test Hallo
Voordat we Hallo runbook toomake publiceert deze beschikbaar is in productie, willen we tootest het toomake ervoor dat deze goed werkt.  Wanneer u een runbook test, voert u de **concept**versie uit en geeft u de uitvoer interactief weer.

1. Klik op **testvenster** blade tooopen Hallo-Test.<br> ![Testvenster](media/automation-first-runbook-graphical/runbook-toolbar-test-revised20165.png)
2. Klik op **Start** toostart Hallo test.  Dit moet Hallo alleen ingeschakelde optie zijn.
3. Een [runbooktaak](automation-runbook-execution.md) wordt gemaakt en de status ervan in Hallo deelvenster worden weergegeven.  
   Hallo taakstatus wordt gestart als *in de wachtrij geplaatst* die aangeeft dat er wordt gewacht tot een runbook worker in Hallo cloud toobecome beschikbaar.  Vervolgens verplaatst te*starten* wanneer een werknemer claims Hallo taak, en vervolgens *met* wanneer Hallo runbook daadwerkelijk wordt uitgevoerd.  
4. Wanneer de runbooktaak Hallo is voltooid, wordt de uitvoer ervan weergegeven. In ons geval zouden we *Hallo wereld* moeten zien.<br> ![Hello World](media/automation-first-runbook-graphical/runbook-test-results.png)
5. Hallo Test blade tooreturn toohello canvas te sluiten.

## <a name="step-4---publish-and-start-hello-runbook"></a>Stap 4: publiceer en Hallo runbook starten
Hallo runbook dat we hebben gemaakt is nog steeds in de modus concept. We moeten toopublish voordat we het in productie kunnen uitvoeren.  Wanneer u een runbook publiceert, kunt u de bestaande gepubliceerde versie Hallo overschrijven met Hallo conceptversie.  In ons geval nog we geen gepubliceerde versie omdat we Hallo runbook zojuist hebben gemaakt.

1. Klik op **publiceren** toopublish hello runbook en vervolgens **Ja** wanneer u wordt gevraagd.<br> ![Publiceren](media/automation-first-runbook-graphical/runbook-toolbar-publish-revised20166.png)
2. Als u links tooview hello runbook in Hallo schuift **Runbooks** blade toont een **ontwerpstatus** van **gepubliceerde**.
3. Schuif terug toohello rechts tooview Hallo blade voor **MyFirstRunbook**.  
   Hallo opties Hallo bovenaan kunnen we toostart hello runbook, toostart op een bepaald moment in toekomstige Hallo plannen of maken een [webhook](automation-webhooks.md) zodat het kan worden gestart via een HTTP-aanroep.
4. We willen dat net toostart hello runbook hiervoor klikt u op **Start** en vervolgens **Ja** wanneer u wordt gevraagd.<br> ![Runbook starten](media/automation-first-runbook-graphical/runbook-controls-start-revised20165.png)
5. Een taakblade wordt geopend voor Hallo runbooktaak die we hebben gemaakt.  We kunnen deze blade sluiten, maar in dit geval we open laten zodat we de voortgang van Hallo taak kunnen bekijken.
6. Hallo taakstatus wordt weergegeven **taakoverzicht** en komt overeen met de statuswaarden die we zagen wanneer we Hallo runbook getest Hallo.<br> ![Taakoverzicht](media/automation-first-runbook-graphical/runbook-job-summary.png)
7. Eenmaal Hallo runbook status bevat *voltooid*, klikt u op **uitvoer**. Hallo **uitvoer** blade wordt geopend en we zien onze *Hallo wereld* in Hallo deelvenster.<br> ![Taakoverzicht](media/automation-first-runbook-graphical/runbook-job-output.png)  
8. Blade sluiten Hallo-uitvoer.
9. Klik op **alle logboeken** tooopen Hallo Streams blade voor de runbooktaak Hallo.  Zien we alleen *Hallo wereld* in Hallo uitvoer, maar er kan weergeven andere stromen voor een runbooktaak zoals uitgebreid en fout als Hallo runbook toothem schrijft.<br> ![Taakoverzicht](media/automation-first-runbook-graphical/runbook-job-AllLogs.png)
10. Sluit de blade alle logboeken Hallo en Hallo taak blade tooreturn toohello blade MyFirstRunbook.
11. Klik op **taken** tooopen Hallo taken blade voor dit runbook.  Hiermee worden alle Hallo taken die zijn gemaakt met dit runbook. We ziet slechts één taak vermeld aangezien we Hallo taak slechts één keer uitgevoerd.<br> ![Taken](media/automation-first-runbook-graphical/runbook-control-jobs.png)
12. U kunt deze taak klikken tooopen Hallo hetzelfde taakvenster die we hebben bekeken toen we Hallo-runbook gestart.  Hiermee kunt u toogo terug in tijd en bekijkt hello details van elke taak die is gemaakt voor een bepaald runbook.

## <a name="step-5---create-variable-assets"></a>Stap 5: variabele assets maken
We hebben ons runbook getest en gepubliceerd, maar tot nu toe doet het nog niets nuttigs. We willen toohave het Azure-resources beheren.  Voordat we Hallo runbook tooauthenticate configureert, we een variabele toohold Hallo abonnements-ID maken en verwijzen we hiernaar nadat we Hallo activiteit tooauthenticate in stap 6 hieronder instellen.  Met inbegrip van de context van een verwijzing toohello abonnement kunt u tooeasily werk tussen meerdere abonnementen.  Voordat u doorgaat, uw abonnements-ID van Hallo optie uitschakelen Hallo navigatiedeelvenster abonnementen te kopiëren.  

1. Klik in de blade Automation-Accounts Hallo op Hallo **activa** tegel en Hallo **activa** blade wordt geopend.
2. Klik in de blade Assets Hallo op Hallo **variabelen** tegel.
3. Klik op de blade variabelen Hallo **toevoegen van een variabele**.<br>![Automation-variabele](media/automation-first-runbook-graphical/create-new-subscriptionid-variable.png)
4. In Hallo blade nieuwe variabele, in Hallo **naam** Voer **AzureSubscriptionId** en in Hallo **waarde** vak uw abonnement-id invoeren.  Houd *tekenreeks* voor Hallo **Type** en de standaardwaarde Hallo voor **versleuteling**.  
5. Klik op **maken** toocreate Hallo variabele.  

## <a name="step-6---add-authentication-toomanage-azure-resources"></a>Stap 6: verificatie toomanage toevoegen Azure-resources
Nu dat we een variabele toohold onze abonnements-ID hebt, kunnen we ons runbook tooauthenticate configureren met Hallo Run As-referenties die bedoeld tooin hello zijn [vereisten](#prerequisites).  We doen dat door toe te voegen hello Azure uitvoeren als-verbinding **Asset** en **Add-AzureRMAccount** cmdlet toohello canvas.  

1. Open Hallo grafische editor door te klikken op **bewerken** op de blade MyFirstRunbook Hallo.<br> ![Runbook bewerken](media/automation-first-runbook-graphical/runbook-controls-edit-revised20165.png)
2. We hebben Hallo **Schrijf Hallo wereld toooutput** voordoet, dus met de rechtermuisknop en selecteer **verwijderen**.
3. Vouw in het besturingselement bibliotheek hello, **verbindingen** en voeg **AzureRunAsConnection** toohello canvas selecteert **toocanvas toevoegen**.
4. Selecteer op papier Hallo **AzureRunAsConnection** en typ in het besturingselementvenster configuratie hello, **uitvoeren als-verbinding ophalen** in Hallo **Label** textbox.  Dit is Hallo-verbinding
5. Typ in het besturingselement bibliotheek hello, **Add-AzureRmAccount** in het Zoektekstvak Hallo.
6. Add **Add-AzureRmAccount** toohello canvas.<br> ![Add-AzureRMAccount](media/automation-first-runbook-graphical/search-powershell-cmdlet-addazurermaccount.png)
7. Beweeg de muisaanwijzer over **uitvoeren als-verbinding ophalen** totdat een cirkel wordt weergegeven onder Hallo van Hallo vorm. Klik op Hallo cirkel en sleep de pijl Hallo te**Add-AzureRmAccount**.  Hallo pijl die u hebt gemaakt is een *koppeling*.  Hallo runbook start met **uitvoeren als-verbinding ophalen** en voer vervolgens **Add-AzureRmAccount**.<br> ![Koppeling tussen activiteiten maken](media/automation-first-runbook-graphical/runbook-link-auth-activities.png)
8. Selecteer op papier Hallo **Add-AzureRmAccount** en bepalen in Hallo configuratie deelvenster type **aanmelding tooAzure** in Hallo **Label** textbox.
9. Klik op **Parameters** en Hallo Parameterconfiguratie van activiteit blade wordt weergegeven.
10. **Add-AzureRmAccount** bevat meerdere parametersets, dus we er tooselect een moeten voordat we parameterwaarden kunnen opgeven.  Klik op **parameterset** en selecteer vervolgens Hallo **ServicePrincipalCertificatewithSubscriptionId** parameterset.
11. Zodra u de parameterset Hallo selecteert, worden in de blade Parameterconfiguratie van activiteit Hallo Hallo parameters weergegeven.  Klik op **APPLICATIONID**.<br> ![Parameters voor Azure RM-account toevoegen](media/automation-first-runbook-graphical/add-azurermaccount-params.png)
12. Selecteer in de blade parameterwaarde de Hallo **uitvoer van activiteit** voor Hallo **gegevensbron** en selecteer **uitvoeren als-verbinding ophalen** in de lijst Hallo in Hallo **veld pad** textbox type **ApplicationId**, en klik vervolgens op **OK**.  We geven Hallo-naam van Hallo-eigenschap voor pad naar het veld van Hallo omdat Hallo activiteit een object met meerdere eigenschappen levert.
13. Klik op **CERTIFICATETHUMBPRINT**, en selecteer in de blade parameterwaarde de Hallo **uitvoer van activiteit** voor Hallo **gegevensbron**.  Selecteer **uitvoeren als-verbinding ophalen** in de lijst Hallo in Hallo **pad naar veld** textbox type **CertificateThumbprint**, en klik vervolgens op **OK**.
14. Klik op **SERVICEPRINCIPAL**, en selecteer in de blade parameterwaarde de Hallo **ConstantValue** voor Hallo **gegevensbron**, klikt u op Hallo optie **True**, en klik vervolgens op **OK**.
15. Klik op **TENANTID**, en selecteer in de blade parameterwaarde de Hallo **uitvoer van activiteit** voor Hallo **gegevensbron**.  Selecteer **uitvoeren als-verbinding ophalen** in de lijst Hallo in Hallo **pad naar veld** textbox type **TenantId**, en klik vervolgens op **OK** twee keer.  
16. Typ in het besturingselement bibliotheek hello, **Set-AzureRmContext** in het Zoektekstvak Hallo.
17. Voeg **Set-AzureRmContext** toohello canvas.
18. Selecteer op papier Hallo **Set-AzureRmContext** en bepalen in Hallo configuratie deelvenster type **abonnements-Id opgeven** in Hallo **Label** textbox.
19. Klik op **Parameters** en Hallo Parameterconfiguratie van activiteit blade wordt weergegeven.
20. **Set-AzureRmContext** bevat meerdere parametersets, dus we er tooselect een moeten voordat we parameterwaarden kunnen opgeven.  Klik op **parameterset** en selecteer vervolgens Hallo **SubscriptionId** parameterset.  
21. Zodra u de parameterset Hallo selecteert, worden in de blade Parameterconfiguratie van activiteit Hallo Hallo parameters weergegeven.  Klik op **SubscriptionID**.
22. Selecteer in de blade parameterwaarde de Hallo **Variabelenactivum** voor Hallo **gegevensbron** en selecteer **AzureSubscriptionId** van Hallo lijst en klik vervolgens op **OK**  twee keer.   
23. Beweeg de muisaanwijzer over **aanmelding tooAzure** totdat een cirkel wordt weergegeven onder Hallo van Hallo vorm. Klik op Hallo cirkel en sleep de pijl Hallo te**abonnements-Id opgeven**.

Uw runbook moet eruitzien als Hallo op dit moment volgen: <br>![Configuratie runbookverificatie](media/automation-first-runbook-graphical/runbook-auth-config.png)

## <a name="step-7---add-activity-toostart-a-virtual-machine"></a>Stap 7: activiteit toostart een virtuele machine toevoegen
Hier we voegen een **Start-AzureRmVM** activiteit toostart een virtuele machine.  U kunt een virtuele machine kiezen in uw Azure-abonnement en voor nu hardcode u die naam in Hallo-cmdlet.

1. Typ in het besturingselement bibliotheek hello, **Start-AzureRm** in het Zoektekstvak Hallo.
2. Voeg **Start-AzureRmVM** toohello canvas Klik en sleep het onder **abonnements-Id opgeven**.
3. Beweeg de muisaanwijzer over **abonnements-Id opgeven** totdat een cirkel wordt weergegeven onder Hallo van Hallo vorm.  Klik op Hallo cirkel en sleep de pijl Hallo te**Start-AzureRmVM**.
4. Selecteer **Start-AzureRmVM**.  Klik op **Parameters** en vervolgens **parameterset** tooview hello wordt ingesteld voor **Start-AzureRmVM**.  Selecteer Hallo **ResourceGroupNameParameterSetName** parameterset. Naast **ResourceGroupName** en **Name** staan uitroeptekens.  Hiermee wordt aangegeven dat dit vereiste parameters zijn.  Voor beide parameters worden tekenreekswaarden verwacht.
5. Selecteer **Name**.  Selecteer **PowerShell-expressie** voor Hallo **gegevensbron** en typt u de naam van de Hallo van Hallo virtuele machine tussen dubbele aanhalingstekens die we met dit runbook beginnen.  Klik op **OK**.<br>![Start-AzureRmVM Naam Parameter Waarde](media/automation-first-runbook-graphical/runbook-startvm-nameparameter.png)
6. Selecteer **ResourceGroupName**. Gebruik **PowerShell-expressie** voor Hallo **gegevensbron** en typt u de naam van de Hallo van Hallo resourcegroep tussen dubbele aanhalingstekens.  Klik op **OK**.<br> ![Start-AzureRmVM-parameters](media/automation-first-runbook-graphical/startazurermvm-params.png)
7. Klik op testvenster zodat we Hallo runbook kunnen testen.
8. Klik op **Start** toostart Hallo test.  Nadat deze is voltooid, controleert u dat de virtuele machine Hallo is gestart.

Uw runbook moet eruitzien als Hallo op dit moment volgen: <br>![Configuratie runbookverificatie](media/automation-first-runbook-graphical/runbook-startvm.png)

## <a name="step-8---add-additional-input-parameters-toohello-runbook"></a>Stap 8: aanvullende invoerparameters toohello runbook toevoegen
Ons runbook momenteel Hallo virtuele machine wordt gestart in Hallo resourcegroep die we hebben opgegeven in Hallo **Start-AzureRmVM** cmdlet.  Ons runbook zou nuttiger zijn als we beide opgeven konden wanneer Hallo runbook wordt gestart.  We nu invoerparameters toohello runbook tooprovide die functionaliteit toevoegen.

1. Open Hallo grafische editor door te klikken op **bewerken** op Hallo **MyFirstRunbook** deelvenster.
2. Klik op **invoer en uitvoer** en vervolgens **invoer toevoegen** tooopen hello Runbookinvoerparameter deelvenster.<br> ![Invoer en uitvoer van runbook](media/automation-first-runbook-graphical/runbook-toolbar-InputandOutput-revised20165.png)
3. Geef *VMName* voor Hallo **naam**.  Houd *tekenreeks* voor Hallo **Type**, maar wijzigen **verplichte** te*Ja*.  Klik op **OK**.
4. Maak een tweede verplichte invoerparameter aangeroepen *ResourceGroupName* en klik vervolgens op **OK** tooclose hello **invoer en uitvoer** deelvenster.<br> ![Invoerparameters voor runbook](media/automation-first-runbook-graphical/start-azurermvm-params-outputs.png)
5. Selecteer Hallo **Start-AzureRmVM** activiteit en klik vervolgens op **Parameters**.
6. Wijziging Hallo **gegevensbron** voor **naam** te**runbookinvoer** en selecteer vervolgens **VMName**.<br>
7. Wijziging Hallo **gegevensbron** voor **ResourceGroupName** te**runbookinvoer** en selecteer vervolgens **ResourceGroupName**.<br> ![Start-AzureVM-parameters](media/automation-first-runbook-graphical/start-azurermvm-params-runbookinput.png)
8. Hallo runbook opslaan en openen van Hallo testvenster.  Houd er rekening mee dat u kunt nu waarden opgeven voor Hallo twee invoervariabelen die u in de test Hallo gebruiken.
9. Sluit Hallo testvenster.
10. Klik op **publiceren** toopublish Hallo nieuwe versie van Hallo runbook.
11. Stop Hallo virtuele machine die u in de vorige stap Hallo gestart.
12. Klik op **Start** toostart hello runbook.  Type in Hallo **VMName** en **ResourceGroupName** voor Hallo virtuele machine die u toostart gaat.<br> ![Runbook starten](media/automation-first-runbook-graphical/runbook-start-inputparams.png)
13. Wanneer Hallo runbook is voltooid, controleert u dat de virtuele machine Hallo is gestart.

## <a name="step-9---create-a-conditional-link"></a>Stap 9: een voorwaardelijke koppeling maken
We wijzigen Hallo runbook nu zodat deze alleen toostart Hallo virtuele machine probeert als deze nog niet is gestart.  U dit doen door het toevoegen van een **Get-AzureRmVM** cmdlet toohello runbook dat Hallo-exemplaarniveaustatus van Hallo virtuele machine opgehaald. Toevoegen van een PowerShell Workflow-codemodule genaamd **Get Status** code met een fragment van PowerShell toodetermine als de status van de virtuele machine hello uitgevoerd of gestopt wordt.  Een voorwaardelijke koppeling van Hallo **Get Status** module kan alleen worden uitgevoerd **Start-AzureRmVM** als de huidige actieve status hello wordt gestopt.  Ten slotte uitvoer we van een bericht tooinform die u als Hallo VM is gestart of niet gebruik Hallo Write-Output van de PowerShell-cmdlet.

1. Open **MyFirstRunbook** in Hallo grafische editor.
2. Hallo-koppeling verwijderen tussen **abonnements-Id opgeven** en **Start-AzureRmVM** door erop te klikken en vervolgens op Hallo *verwijderen* sleutel.
3. Typ in het besturingselement bibliotheek hello, **Get-AzureRm** in het Zoektekstvak Hallo.
4. Voeg **Get-AzureRmVM** toohello canvas.
5. Selecteer **Get-AzureRmVM** en vervolgens **parameterset** tooview hello wordt ingesteld voor **Get-AzureRmVM**.  Selecteer Hallo **GetVirtualMachineInResourceGroupNameParamSet** parameterset.  Naast **ResourceGroupName** en **Name** staan uitroeptekens.  Hiermee wordt aangegeven dat dit vereiste parameters zijn.  Voor beide parameters worden tekenreekswaarden verwacht.
6. Selecteer onder **Gegevensbron** voor **Name** de optie **Runbookinvoer** en selecteer vervolgens **VMName**.  Klik op **OK**.
7. Selecteer onder **Gegevensbron** voor **ResourceGroupName** de optie **Runbookinvoer** en selecteer vervolgens **ResourceGroupName**.  Klik op **OK**.
8. Selecteer onder **Gegevensbron** voor **Status** de optie **Constante waarde** en klik vervolgens op **Waar**.  Klik op **OK**.  
9. Maak een koppeling van **abonnements-Id opgeven** te**Get-AzureRmVM**.
10. Vouw in het besturingselement bibliotheek Hallo **Runbookbesturing** en voeg **Code** toohello canvas.  
11. Maak een koppeling van **Get-AzureRmVM** te**Code**.  
12. Klik op **Code** en wijzig in het deelvenster configuratie Hallo label te**Get Status**.
13. Selecteer **Code** parameter en Hallo **Code-Editor** blade wordt weergegeven.  
14. Plak in Hallo code-editor Hallo codefragment te volgen:
    
     ```
     $StatusesJson = $ActivityOutput['Get-AzureRmVM'].StatusesText
     $Statuses = ConvertFrom-Json $StatusesJson
     $StatusOut =""
     foreach ($Status in $Statuses){
     if($Status.Code -eq "Powerstate/running"){$StatusOut = "running"}
     elseif ($Status.Code -eq "Powerstate/deallocated") {$StatusOut = "stopped"}
     }
     $StatusOut
     ```
15. Maak een koppeling van **Get Status** te**Start-AzureRmVM**.<br> ![Runbook met codemodule](media/automation-first-runbook-graphical/runbook-startvm-get-status.png)  
16. Selecteer Hallo koppeling en wijzig in het deelvenster configuratie Hallo **voorwaarde toepassen** te**Ja**.   Opmerking Hallo koppeling wordt onderbroken tooa-lijn waarmee wordt aangegeven dat Hallo doelactiviteit alleen wordt uitgevoerd als Hallo voorwaarde tootrue is opgelost.  
17. Voor Hallo **expressie van voorwaarde**, type *$ActivityOutput ['Get Status'] - eq "Stopped"*.  **Start-AzureRmVM** nu alleen worden uitgevoerd als Hallo virtuele machine is gestopt.
18. Vouw in het besturingselement bibliotheek hello, **Cmdlets** en vervolgens **Microsoft.PowerShell.Utility**.
19. Voeg **Write-Output** tweemaal toohello canvas.<br> ![Runbook met Write-Output](media/automation-first-runbook-graphical/runbook-startazurermvm-complete.png)
20. Op Hallo eerste **Write-Output** beheren, klikt u op **Parameters** en wijzig Hallo **Label** waarde te*VM gestart melden*.
21. Voor **InputObject**, wijzigen **gegevensbron** te**PowerShell-expressie** en typt u Hallo expressie *"$VMName successfully started."* .
22. Op Hallo tweede **Write-Output** beheren, klikt u op **Parameters** en wijzig Hallo **Label** waarde te*starten VM mislukt melden*
23. Voor **InputObject**, wijzigen **gegevensbron** te**PowerShell-expressie** en typt u Hallo expressie *"$VMName could not start."* .
24. Maak een koppeling van **Start-AzureRmVM** te**VM gestart melden** en **starten VM mislukt melden**.
25. Hallo-koppeling te selecteren**VM gestart melden** en wijzig **voorwaarde toepassen** te**True**.
26. Voor Hallo **expressie van voorwaarde**, type *$ActivityOutput ['Start-AzureRmVM']. IsSuccessStatusCode - eq $true*.  Deze Write-Output beheren nu alleen worden uitgevoerd als Hallo virtuele machine is gestart.
27. Hallo-koppeling te selecteren**starten VM mislukt melden** en wijzig **voorwaarde toepassen** te**True**.
28. Voor Hallo **expressie van voorwaarde**, type *$ActivityOutput ['Start-AzureRmVM']. IsSuccessStatusCode - ne $true*.  Deze Write-Output beheren wordt alleen uitgevoerd als Hallo virtuele machine niet is gestart.
29. Hallo runbook opslaan en openen van Hallo testvenster.
30. Hallo runbook start met Hallo virtuele machine is gestopt en moet worden gestart.

## <a name="next-steps"></a>Volgende stappen
* Zie toolearn meer informatie over grafisch ontwerpen [grafisch ontwerpen in Azure Automation](automation-graphical-authoring-intro.md)
* Zie tooget gestart met PowerShell-runbooks [Mijn eerste PowerShell-runbook](automation-first-runbook-textual-powershell.md)
* tooget gestart met PowerShell workflow-runbooks, Zie [Mijn eerste PowerShell workflow-runbook](automation-first-runbook-textual.md)

