---
title: aaaEditing tekstuele runbooks in Azure Automation
description: Dit artikel bevat verschillende procedures voor het werken met PowerShell en PowerShell Workflow-runbooks in Azure Automation met behulp van Hallo teksteditor.
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 6f5b48fb-6f30-4e99-9e14-9061b5554b08
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 3fd87d457838f300ca6c94bc345e82c679a0e011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="editing-textual-runbooks-in-azure-automation"></a>Tekstuele runbooks in Azure Automation bewerken
Hallo teksteditor in Azure Automation kan worden gebruikt tooedit [PowerShell-runbooks](automation-runbook-types.md#powershell-runbooks) en [PowerShell Workflow-runbooks](automation-runbook-types.md#powershell-workflow-runbooks). Dit heeft Hallo typische functies van andere code-editors, zoals intellisense en kleurcodering met extra functies voor speciale tooassist u bij het openen van bronnen algemene toorunbooks.  In dit artikel biedt gedetailleerde stappen voor het uitvoeren van verschillende functies met deze editor.

Hallo teksteditor bevat een functie tooinsert code voor activiteiten, assets en onderliggende runbooks in een runbook. U kunt in plaats van te typen in Hallo code zelf selecteren uit een lijst met beschikbare bronnen en hebt de juiste code Hallo Hallo runbook ingevoegd.

Elk runbook in Azure Automation heeft twee versies, ontwerp- en gepubliceerd. U bewerkt de conceptversie Hallo van Hallo runbook en publiceert deze zodat deze kan worden uitgevoerd. Hallo gepubliceerde versie kan niet worden bewerkt. Zie [een runbook publiceren](automation-creating-importing-runbook.md#publishing-a-runbook) voor meer informatie.

toowork met [grafische Runbooks](automation-runbook-types.md#graphical-runbooks), Zie [grafisch ontwerpen in Azure Automation](automation-graphical-authoring-intro.md).

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>tooedit een runbook met hello Azure-portal
Hallo te volgen procedure tooopen een runbook bewerken in de teksteditor hello gebruiken.

1. In hello Azure-portal, selecteer uw automation-account.
2. Klik op Hallo **Runbooks** tegel tooopen Hallo lijst van runbooks.
3. Klik op de naam van de Hallo van Hallo runbook u wilt dat tooedit en klik vervolgens op Hallo **bewerken** knop.
4. Hallo vereist bewerken uitvoeren.
5. Klik op **opslaan** wanneer de bewerkingen zijn voltooid.
6. Klik op **publiceren** als u wilt dat de meest recente conceptversie Hallo van Hallo runbook toobe gepubliceerd.

### <a name="tooinsert-a-cmdlet-into-a-runbook"></a>tooinsert een cmdlet in een runbook
1. Hallo Canvas van teksteditor hello, zet Hallo cursor in waar u tooplace Hallo cmdlet.
2. Vouw Hallo **Cmdlets** knooppunt in het besturingselement bibliotheek Hallo.
3. Hallo-module met Hallo-cmdlet u toouse wilt uitbreiden.
4. Klik met de rechtermuisknop op Hallo cmdlet tooinsert en selecteer **toocanvas toevoegen**.  Als Hallo cmdlet meer dan één parameter is ingesteld heeft, wordt de standaardset Hallo worden toegevoegd.  U kunt ook uitbreiden Hallo cmdlet tooselect een andere parameter ingesteld.
5. Hallo-code voor Hallo cmdlet wordt ingevoegd met de volledige lijst van parameters.
6. Kies een passende waarde in plaats van Hallo gegevenstype omgeven door accolades <> voor alle vereiste parameters.  U hoeft geen parameters worden verwijderd.

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>tooinsert code voor een onderliggend runbook in een runbook
1. Hallo Canvas van teksteditor hello, zet Hallo cursor in waar u tooplace Hallo code voor Hallo [onderliggend runbook](automation-child-runbooks.md).
2. Vouw Hallo **Runbooks** knooppunt in het besturingselement bibliotheek Hallo.
3. Klik met de rechtermuisknop op Hallo runbook tooinsert en selecteer **toocanvas toevoegen**.
4. Hallo-code voor Hallo onderliggend runbook wordt ingevoegd met een tijdelijke aanduidingen voor elke runbook-parameters.
5. Vervang de tijdelijke aanduidingen Hallo met de juiste waarden voor elke parameter.

### <a name="tooinsert-an-asset-into-a-runbook"></a>tooinsert activa in een runbook
1. Hallo Canvas van teksteditor hello, zet Hallo cursor in waar u tooplace Hallo code voor Hallo onderliggend runbook.
2. Vouw Hallo **activa** knooppunt in het besturingselement bibliotheek Hallo.
3. Hallo-knooppunt voor Hallo type asset die u wilt uitbreiden.
4. Hallo asset tooinsert Klik met de rechtermuisknop en selecteer **toocanvas toevoegen**.  Voor [variabele assets](automation-variables.md), selecteert u **toevoegen 'Variabele ophalen' toocanvas** of **toevoegen '-variabele instellen' toocanvas** , afhankelijk van of u wilt dat tooget of Hallo-variabele instellen.
5. Hallo-code voor Hallo asset is ingevoegd in Hallo runbook.

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>tooedit een runbook met hello Azure-portal
Hallo te volgen procedure tooopen een runbook bewerken in de teksteditor hello gebruiken.

1. Selecteer in de Azure-portal hello, **Automation** en klik vervolgens op Hallo-naam van een automation-account.
2. Selecteer Hallo **Runbooks** tabblad.
3. Klik op de naam van de Hallo van Hallo runbook u wilt dat tooedit en selecteer vervolgens Hallo **auteur** tabblad.
4. Klik op Hallo **bewerken** knop Hallo onder welkomstscherm aan.
5. Hallo vereist bewerken uitvoeren.
6. Klik op **opslaan** wanneer de bewerkingen zijn voltooid.
7. Klik op **publiceren** als u wilt dat de meest recente conceptversie Hallo van Hallo runbook toobe gepubliceerd.

### <a name="tooinsert-an-activity-into-a-runbook"></a>een activiteit in een Runbook tooinsert
1. Hallo Canvas van teksteditor hello, zet Hallo cursor in waar u tooplace Hallo activiteit.
2. Aan de onderkant van de Hallo van Hallo scherm, klikt u op **invoegen** en vervolgens **activiteit**.
3. In Hallo **integratiemodule** kolom, selecteer Hallo-module die Hallo activiteit bevat.
4. In Hallo **activiteit** deelvenster, selecteert u een activiteit.
5. In Hallo **beschrijving** kolom Opmerking Hallo beschrijving van Hallo-activiteit. Desgewenst kunt u gedetailleerde weergave toolaunch help voor de activiteit in de browser Hallo Hallo.
6. Klik op de pijl-rechts Hallo.  Als Hallo activiteit parameters bevat, worden ze ter informatie weergegeven.
7. Klik op de knop controleren Hallo.  Code toorun Hallo activiteit zal worden ingevoegd in Hallo runbook.
8. Als Hallo activiteit parameters vereist, typt u een geschikte waarde in plaats van Hallo gegevenstype omgeven door accolades <>.

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>tooinsert code voor een onderliggend runbook in een runbook
1. Hallo Canvas van teksteditor hello, zet Hallo cursor in waar u tooplace hello [onderliggend runbook](automation-child-runbooks.md).
2. Aan de onderkant van de Hallo van Hallo scherm, klikt u op **invoegen** en vervolgens **Runbook**.
3. Hallo runbook tooinsert van Hallo middelste kolom en klik op de pijl-rechts Hallo.
4. Als Hallo runbook parameters heeft, kunt u ze wordt weergegeven voor uw gegevens.
5. Klik op de knop controleren Hallo.  Code toorun Hallo geselecteerd runbook zal worden ingevoegd in de huidige runbook Hallo.
6. Als Hallo runbook parameters vereist, typt u een geschikte waarde in plaats van Hallo gegevenstype omgeven door accolades <>.

### <a name="tooinsert-an-asset-into-a-runbook"></a>tooinsert activa in een runbook
1. Hallo Canvas van teksteditor hello, zet Hallo cursor in waar u tooplace Hallo activiteit tooretrieve Hallo asset.
2. Aan de onderkant van de Hallo van Hallo scherm, klikt u op **invoegen** en vervolgens **instelling**.
3. In Hallo **Instellingsactie** kolom, selecteer Hallo-actie die u wilt.
4. Selecteer in de beschikbare activa Hallo in Hallo middelste kolom.
5. Klik op de knop controleren Hallo.  Code tooget of set Hallo asset zal worden ingevoegd in Hallo runbook.

## <a name="tooedit-an-azure-automation-runbook-using-windows-powershell"></a>tooedit een Azure Automation-runbook met Windows PowerShell
tooedit een runbook met Windows PowerShell kunt u gebruik Hallo-editor van uw keuze en tooa .ps1-bestand opslaan. Kunt u Hallo [Get-AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/getazurerunbookdefinition) cmdlet tooretrieve Hallo inhoud van Hallo runbook en vervolgens [Set AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/setazurerunbookdefinition) cmdlet tooreplace Hallo bestaande conceptrunbook Hello gewijzigd een.

### <a name="tooretrieve-hello-contents-of-a-runbook-using-windows-powershell"></a>tooRetrieve Hallo inhoud van een Runbook met Windows PowerShell
Hallo volgende voorbeeldopdrachten laten zien hoe tooretrieve Hallo script voor een runbook en sla het tooa-scriptbestand. In dit voorbeeld wordt de conceptversie Hallo opgehaald. Het is ook mogelijk tooretrieve Hallo gepubliceerde versie van Hallo runbook Hoewel deze versie kan niet worden gewijzigd.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    $runbookDefinition = Get-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Slot Draft
    $runbookContent = $runbookDefinition.Content

    Out-File -InputObject $runbookContent -FilePath $scriptPath

### <a name="toochange-hello-contents-of-a-runbook-using-windows-powershell"></a>tooChange Hallo inhoud van een Runbook met Windows PowerShell
Hallo volgende voorbeeldopdrachten laten zien hoe tooreplace bestaande inhoud van een runbook met inhoud van een scriptbestand Hallo Hallo. Opmerking dat is dit Hallo dezelfde procedure als in voorbeeld [tooimport een runbook uit een scriptbestand met Windows PowerShell](automation-creating-importing-runbook.md).

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    Set-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Path $scriptPath -Overwrite
    Publish-AzureAutomationRunbook –AutomationAccountName $automationAccountName –Name $runbookName

## <a name="related-articles"></a>Verwante artikelen:
* [Maken of importeren van een runbook in Azure Automation](automation-creating-importing-runbook.md)
* [Learning PowerShell workflow](automation-powershell-workflow.md)
* [Grafisch ontwerpen in Azure Automation](automation-graphical-authoring-intro.md)
* [Certificaten](automation-certificates.md)
* [Verbindingen](automation-connections.md)
* [Referenties](automation-credentials.md)
* [Schema's](automation-schedules.md)
* [Variabelen](automation-variables.md)
