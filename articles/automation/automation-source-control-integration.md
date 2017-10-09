---
title: aaaSource integratie van broncodebeheer in Azure Automation | Microsoft Docs
description: Integratie van broncodebeheer met GitHub in Azure Automation beschreven.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 224d7375-9887-44dd-b137-06ffe396a4b4
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 6ceee1de8065fafe85a13bbd7f585e74dbc96b47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="source-control-integration-in-azure-automation"></a>Integratie van broncodebeheer in Azure Automation
Integratie van broncodebeheer kunt u runbooks tooassociate in uw Automation-account tooa GitHub resourcebeheerbibliotheek. Broncodebeheer kunt u tooeasily samenwerken met uw team, het bijhouden van wijzigingen en terugdraaien tooearlier versies van uw runbooks. Verbinding met broncodebeheer kan bijvoorbeeld u toosync verschillende filialen in broncodebeheer tooyour ontwikkeling, testen of productie Automation-accounts, zodat u eenvoudig toopromote-code die is getest in uw productieomgeving in ontwikkeling omgeving tooyour Automation account.

Broncodebeheer kunt u code uit Azure Automation toosource besturingselement toopush of uw runbooks van bron besturingselement tooAzure Automation ophalen. Dit artikel wordt beschreven hoe tooset up bron in uw Azure Automation-omgeving beheren. We beginnen door het configureren van Azure Automation tooaccess uw GitHub-opslagplaats en doorlopen verschillende bewerkingen die kunnen worden uitgevoerd met behulp van de integratie van broncodebeheer. 

> [!NOTE]
> Biedt ondersteuning voor broncodebeheer ophalen en opslaan [PowerShell Workflow-runbooks](automation-runbook-types.md#powershell-workflow-runbooks) , evenals [PowerShell-runbooks](automation-runbook-types.md#powershell-runbooks). [Grafische runbooks](automation-runbook-types.md#graphical-runbooks) worden nog niet ondersteund.<br><br>
> 
> 

Er zijn twee eenvoudige stappen vereist tooconfigure broncodebeheer voor uw Automation-account, en slechts één als er al een GitHub-account. Ze zijn:

## <a name="step-1--create-a-github-repository"></a>Stap 1: Maak een GitHub-opslagplaats
Als u al een GitHub-account en een locatie die u wilt toolink tooAzure Automation, en vervolgens aanmelding tooyour bestaande account en beginnen bij stap 2 hieronder. Ga anders te[GitHub](https://github.com/), zich aanmelden voor een nieuw account en [maken van een nieuwe opslagplaats](https://help.github.com/articles/create-a-repo/).

## <a name="step-2--set-up-source-control-in-azure-automation"></a>Stap 2: broncodebeheer in Azure Automation instellen
1. Hallo Automation-Account blade in hello Azure-portal klikt u op **broncodebeheer instellen.** 
   
    ![Resourcebeheer instellen](media/automation-source-control-integration/automation_01_SetUpSourceControl.png)
2. Hallo **broncodebeheer** blade wordt geopend, waar u de gegevens van uw GitHub-account kunt configureren. Hieronder volgt Hallo lijst met parameters tooconfigure:  
   
   | **Parameter** | **Beschrijving** |
   |:--- |:--- |
   | Bron kiezen |Selecteer Hallo bron. Op dit moment alleen **GitHub** wordt ondersteund. |
   | Autorisatie |Klik op Hallo **autoriseren** knop toogrant Azure Automation toegang tooyour GitHub-opslagplaats. Als u al aangemeld tooyour GitHub-account in een ander venster, Hallo worden de referenties van het account gebruikt. Wanneer de autorisatie is geslaagd, Hallo blade uw GitHub-gebruikersnaam onder weergegeven **autorisatie eigenschap**. |
   | Kies de opslagplaats |Selecteer een GitHub-opslagplaats in Hallo lijst met beschikbare opslagplaatsen. |
   | Vertakking kiezen |Selecteer een vertakking uit Hallo lijst met beschikbare vertakkingen. Alleen Hallo **master** vertakking wordt weergegeven als u eventuele vertakkingen dat nog niet hebt gemaakt. |
   | Pad naar de Runbookmap |Hallo runbook mappad geeft Hallo pad in Hallo GitHub-opslagplaats van waaruit u wilt dat toopush of ophalen van uw code. Dit moet worden ingevoerd in de indeling Hallo **/mapnaam/submapnaam**. Alleen runbooks in het pad naar Hallo de runbookmap worden gesynchroniseerde tooyour Automation-account. Runbooks in submappen van Hallo runbook mappad hello wordt **niet** worden gesynchroniseerd. Gebruik  **/**  toosync alle runbooks onder Hallo opslagplaats Hallo. |
3. Bijvoorbeeld, als er een opslagplaats met de naam **PowerShellScripts** die een map met de naam bevat **RootFolder**, die een map met de naam bevat **submap**. Elke mapniveau, kunt u Hallo tekenreeksen toosync volgende gebruiken:
   
   1. toosync runbooks uit **opslagplaats**, pad naar de runbookmap is*/*
   2. toosync runbooks uit **RootFolder**, pad naar de runbookmap is */RootFolder*
   3. toosync runbooks uit **submap**, pad naar de runbookmap is */RootFolder/submap*.
4. Nadat u Hallo parameters hebt geconfigureerd, worden weergegeven op Hallo **blade broncodebeheer instellen.**  
   
    ![Blade configureren](media/automation-source-control-integration/automation_02_SourceControlConfigure.png)
5. Wanneer u op OK klikt, worden de integratie van broncodebeheer is nu geconfigureerd voor uw Automation-account en moet worden bijgewerkt met uw GitHub-gegevens. U kunt nu klikken op de tooview van dit onderdeel al uw broncodebeheer Taakgeschiedenis synchroniseren.  
   
    ![Waarden van de opslagplaats](media/automation-source-control-integration/automation_03_RepoValues.png)
6. Na het instellen van broncodebeheer, wordt hello volgende Automation-resources gemaakt in uw Automation-account:  
   Twee [variabele assets](automation-variables.md) worden gemaakt.  
   
   * Hallo variabele **Microsoft.Azure.Automation.SourceControl.Connection** Hallo waarden van Hallo-verbindingsreeks bevat, zoals hieronder wordt weergegeven.  
     
     | **Parameter** | **Waarde** |
     |:--- |:--- |
     | Naam |Microsoft.Azure.Automation.SourceControl.Connection |
     | Type |Tekenreeks |
     | Waarde |{{'Vertakking':\<*de naam van uw vertakking*>, 'RunbookFolderPath':\<*pad naar de Runbookmap*>, 'ProviderType':\<*heeft de waarde 1 voor GitHub*>, 'Opslagplaats':\<*naam van uw opslagplaats*>, 'Gebruikersnaam':\<*uw GitHub-gebruikersnaam*>} |

    * Hallo variabele **Microsoft.Azure.Automation.SourceControl.OAuthToken**, Hallo veilig versleutelde waarde van uw OAuthToken bevat.  

    |**Parameter**            |**Waarde** |
    |:---|:---|
    | Naam  | Microsoft.Azure.Automation.SourceControl.OAuthToken |
    | Type | Unknown(Encrypted) |
    | Waarde | <*Versleutelde OAuthToken*> |  

    ![Variabelen](media/automation-source-control-integration/automation_04_Variables.png)  

    * **Automation-bronbeheer** wordt toegevoegd als een geautoriseerde toepassing tooyour GitHub-account. tooview hello toepassing: Ga vanuit uw startpagina GitHub tooyour **profiel** > **instellingen** > **toepassingen**. Deze toepassing kunnen Azure Automation toosync uw GitHub-opslagplaats tooan Automation-account.  

    ![GIT-toepassing](media/automation-source-control-integration/automation_05_GitApplication.png)


## <a name="using-source-control-in-automation"></a>Met behulp van broncodebeheer in Automation
### <a name="check-in-a-runbook-from-azure-automation-toosource-control"></a>Controleer in een runbook uit Azure Automation toosource besturingselement
Controleer in de Runbook kunt u toopush Hallo wijzigingen zijn aangebracht tooa runbook in Azure Automation in uw resourcebeheerbibliotheek. Hieronder staat een runbook Hallo stappen toocheck in:

1. Van uw Automation-Account [maken van nieuwe tekstueel runbook](automation-first-runbook-textual.md), of [bewerken van een bestaande, tekstgegevens runbook](automation-edit-textual-runbook.md). Dit runbook is een PowerShell-werkstroom of een PowerShell-script runbook.  
2. Nadat u uw runbook hebt bewerkt, opslaan en klik op **inchecken** van Hallo **bewerken** blade.  
   
    ![Knop inchecken](media/automation-source-control-integration/automation_06_CheckinButton.png)

     > [!NOTE] 
     > Inchecken van Azure Automation, Hallo-code die momenteel aanwezig is in uw bronbeheer wordt overschreven. Hallo Git equivalente opdrachtregel aanwijzingen toocheck-in is **git toevoegen + git-doorvoer + git push**  

1. Wanneer u klikt op **inchecken**, u wordt gevraagd met een bevestigingsbericht wordt weergegeven, klikt u op Ja toocontinue.  
   
    ![Inchecken bericht](media/automation-source-control-integration/automation_07_CheckinMessage.png)
2. Inchecken begint Hallo bron besturingselement runbook: **Sync MicrosoftAzureAutomationAccountToGitHubV1**. Dit runbook tooGitHub verbindt en pushes wijzigingen uit Azure Automation tooyour opslagplaats. tooview Hallo inchecken Taakgeschiedenis, gaat u terug toohello **integratie van broncodebeheer** tabblad en klik op tooopen Hallo opslagplaats synchronisatie blade. Deze blade bevat alle uw resourcebeheertaken.  Hallo functie u wilt tooview en klik op details voor tooview Hallo selecteren.  
   
    ![Inchecken Runbook](media/automation-source-control-integration/automation_08_CheckinRunbook.png)
   
   > [!NOTE]
   > Bron besturingselement runbooks zijn speciale Automation-runbooks die u kunt weergeven of bewerken. Terwijl ze niet in de lijst met runbook weergegeven worden, ziet u synchronisatietaken in de takenlijst met weergegeven.
   > 
   > 
3. Hallo-naam van Hallo gewijzigd runbook wordt verzonden als een invoerparameter toohello inchecken runbook. U kunt [Hallo Taakdetails weergeven](automation-runbook-execution.md#viewing-job-status-from-the-azure-portal) door het uitbreiden van runbook in **opslagplaats synchronisatie** blade.  
   
    ![Inchecken invoer](media/automation-source-control-integration/automation_09_CheckinInput.png)
4. Uw GitHub-opslagplaats vernieuwen wanneer de taak Hallo tooview Hallo wijzigingen is voltooid.  Er moet een doorvoeren in de opslagplaats met een commit-bericht: **bijgewerkt *Runbooknaam* in Azure Automation.**  

### <a name="sync-runbooks-from-source-control-tooazure-automation"></a>Synchronisatie runbooks uit bron besturingselement tooAzure Automation
Hallo sync knop op Hallo opslagplaats synchronisatie blade kunt u toopull alle Hallo runbooks in Hallo pad naar de runbookmap van uw opslagplaats tooyour Automation-account. Hallo kan dezelfde opslagplaats worden gesynchroniseerd toomore dan één Automation-account. Hieronder staat een runbook Hallo stappen toosync:

1. Open in Hallo Automation-account waarmee u verbinding met broncodebeheer instellen, Hallo **bron besturingselement integratie/opslagplaats synchronisatie blade** en klik op **Sync** en vervolgens wordt u gevraagd met een bevestiging bericht wordt weergegeven, klikt u op **Ja** toocontinue.  
   
    ![Knop synchronisatie](media/automation-source-control-integration/automation_10_SyncButtonwithMessage.png)
2. Synchronisatie Hallo runbook wordt gestart: **Sync MicrosoftAzureAutomationAccountFromGitHubV1**. Dit runbook tooGitHub verbindt en haalt Hallo wijzigingen van uw opslagplaats tooAzure Automation. U ziet een nieuwe taak op Hallo **opslagplaats synchronisatie** blade voor deze actie. tooview details over Hallo-sync-taak klikt u op de blade toewijzingdetails tooopen Hallo-taak.  
   
    ![Runbook synchroniseren](media/automation-source-control-integration/automation_11_SyncRunbook.png)

    > [!NOTE] 
    > Een synchroniseren vanuit resourcebeheer overschrijft de conceptversie Hallo van Hallo runbooks die momenteel aanwezig zijn in uw Automation-account voor **alle** besturingselement voor runbooks die momenteel in de gegevensbron. Hallo Git equivalente opdrachtregel instructie toosync is **git, pull**


## <a name="troubleshooting-source-control-problems"></a>Het oplossen van problemen van bron-besturingselement
Als er fouten optreden met een in- of sync-taak, taakstatus Hallo moet worden onderbroken en vindt u meer informatie over Hallo fout in de blade taak Hallo.  Hallo **alle logboeken** deel ziet u alle PowerShell-stromen gekoppeld aan deze taak Hallo. Zodoende kunt dat u met Hallo details toohelp u los eventuele problemen met het in- of de synchronisatie nodig. Dit wordt ook beschreven u Hallo volgorde van de acties die zijn opgetreden tijdens het synchroniseren of controleren in een runbook.  

![Afbeelding van AllLogs](media/automation-source-control-integration/automation_13_AllLogs.png)

## <a name="disconnecting-source-control"></a>Verbinding met broncodebeheer verbreken
toodisconnect uit uw GitHub-account Hallo opslagplaats synchronisatie blade open en klik op **Disconnect**. Wanneer u verbinding met broncodebeheer verbreken, runbooks die eerder zijn gesynchroniseerd blijven bestaan in uw Automation-account maar Hallo opslagplaats synchronisatie blade wordt niet ingeschakeld.  

  ![Knop verbinding verbreken](media/automation-source-control-integration/automation_12_Disconnect.png)

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over de integratie van broncodebeheer Hallo resources te volgen:  

* [Azure Automation: Integratie van broncodebeheer in Azure Automation](https://azure.microsoft.com/blog/azure-automation-source-control-13/)  
* [Stem voor uw favoriete bronbeheersysteem](https://www.surveymonkey.com/r/?sm=2dVjdcrCPFdT0dFFI8nUdQ%3d%3d)  
* [Azure Automation: Integratie van broncodebeheer Runbook met behulp van Visual Studio Team Services](https://azure.microsoft.com/blog/azure-automation-integrating-runbook-source-control-using-visual-studio-online/)  

