---
title: Integratie van broncodebeheer automatisering met GitHub voor ondernemingen aaaAzure | Microsoft Docs
description: Hierin wordt beschreven Hallo gedetailleerde informatie over de tooconfigure integratie met GitHub Enterprise voor broncodebeheer van Automation-runbooks.
services: automation
documentationCenter: 
authors: mgoedtel
manager: jwhit
editor: 
ms.assetid: e01d817c-7d38-421c-adf5-647a4b526eb4
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: magoedte
ms.openlocfilehash: 915d36ccabb72fdee1dba663049a0b331249cd73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-github-enterprise"></a>Azure Automation-scenario - integratie van broncodebeheer automatisering met GitHub voor ondernemingen

Automation biedt momenteel ondersteuning voor integratie van broncodebeheer, waarmee u tooassociate runbooks in uw Automation-account tooa GitHub resourcebeheerbibliotheek.  Echter klanten die hebben geïmplementeerd [GitHub Enterprise](https://enterprise.github.com/home) toosupport hun DevOps practices, wilt u ook toouse het toomanage Hallo levenscyclus van runbooks die zijn ontwikkeld tooautomate zakelijke processen en servicebeheer bewerkingen.  

In dit scenario hebt u een Windows-computer in uw datacenter die is geconfigureerd als een hybride Runbook Worker met hello Azure Resource Manager-modules en Git-hulpprogramma's geïnstalleerd.  Hallo hybride worker machine heeft een kloon van de lokale Git-opslagplaats Hallo.  Hallo runbook wordt uitgevoerd op Hallo hybride worker, Hallo Git directory worden gesynchroniseerd als Hallo runbook bestandsinhoud worden geïmporteerd in Hallo Automation-account.

Dit artikel wordt beschreven hoe tooset van deze configuratie in uw Azure Automation-omgeving. Begin met het configureren van automatisering met Hallo beveiligingsreferenties runbooks vereist toosupport dit scenario en implementatie van een hybride Runbook Worker in uw gegevens centreren toorun hello runbooks en toegang tot uw onderneming GitHub-opslagplaats toosynchronize runbooks met uw Automation-account.  


## <a name="getting-hello-scenario"></a>Hallo scenario ophalen

Dit scenario bestaat uit twee PowerShell-runbooks die u rechtstreeks vanuit Hallo importeren kunt [Runbookgalerie](automation-runbook-gallery.md) in hello Azure-portal of downloaden van Hallo [PowerShell Gallery](https://www.powershellgallery.com).

### <a name="runbooks"></a>Runbooks

Runbook | Beschrijving| 
--------|------------|
Export RunAsCertificateToHybridWorker | Runbook exporteert een RunAs-certificaat van een Automation-account tooa hybride worker zodat runbooks op Hallo worker zich met Azure in volgorde tooimport runbooks in Hallo Automation-account verifiëren kunnen.| 
Synchronisatie LocalGitFolderToAutomationAccount | Runbook synchronisaties Hallo lokale Git-map op Hallo hybride machine en vervolgens importeren Hallo runbook-bestanden (*.ps1) in Hallo Automation-account.|

### <a name="credentials"></a>Referenties

Referentie | Beschrijving|
-----------|------------|
GitHRWCredential | Referentie-element maakt u toocontain Hallo gebruikersnaam en wachtwoord voor een gebruiker met machtigingen toohello hybride worker.|

## <a name="installing-and-configuring-this-scenario"></a>Dit scenario installeren en configureren

### <a name="prerequisites"></a>Vereisten

1. Hallo Sync LocalGitFolderToAutomationAccount runbook verifieert met behulp van Hallo [Azure uitvoeren als-account](automation-sec-configure-azure-runas-account.md). 

2. Een werkruimte van de Microsoft Operations Management Suite (OMS) Hello Azure Automation-oplossing ingeschakeld en geconfigureerd, is ook vereist.  Als u niet die is gekoppeld aan Hallo Automation-account gebruikt tooinstall en configureren van dit scenario hebt, is deze gemaakt en geconfigureerd voor u tijdens het uitvoeren van Hallo **nieuw OnPremiseHybridWorker.ps1** script vanaf Hallo hybride runbook worker.        

    > [!NOTE]
    > Momenteel hello volgende regio's alleen ondersteuning voor automatisering integratie met OMS - **Australië-Zuidoost**, **VS-Oost 2**, **Zuidoost-Azië**, en **West Europa**. 

3. Een computer die kan fungeren als een toegewezen hybride Runbook Worker waarin ook Hallo GitHub software en onderhouden van Hallo runbook-bestanden (*runbook*.ps1) in een bronmap op Hallo bestand system toosynchronize tussen GitHub en uw Automation-account.

### <a name="import-and-publish-hello-runbooks"></a>Importeren en Hallo runbooks publiceren

Hallo tooimport *Export RunAsCertificateToHybridWorker* en *Sync LocalGitFolderToAutomationAccount* runbooks uit Hallo Runbookgalerie uit uw Automation-account in hello Azure-portal Volg de procedures Hallo in [Runbook importeren vanuit Hallo Runbookgalerie](automation-runbook-gallery.md#to-import-a-runbook-from-the-runbook-gallery-with-the-azure-portal). Hallo runbooks publiceren nadat ze correct zijn geïmporteerd in uw Automation-account.

### <a name="deploy-and-configure-hybrid-runbook-worker"></a>Implementeren en configureren van de hybride Runbook Worker

Als u niet een hybride Runbook Worker al geïmplementeerd in uw datacenter hebt, moet u Hallo vereisten doornemen en volg Hallo geautomatiseerde installatiestappen met Hallo-procedure in [Azure Automation Hybrid Runbook Workers - automatiseren installeren en configuratie](automation-hybrid-runbook-worker.md#automated-deployment).  Wanneer u Hallo hybride worker op een computer hebt geïnstalleerd, worden uitgevoerd Hallo volgende stappen toocomplete de toosupport configuratie van dit scenario.

1. Meld u op toohello computer hosting Hallo Hybrid Runbook Worker-rol met een account met lokale beheerdersrechten en maken van een directory toohold Hallo Git runbook-bestanden.  Kloon Hallo interne Git-opslagplaats toohello directory.
2. Als u nog geen een RunAs-account gemaakt of als u een nieuw speciaal ontworpen is voor dit doel toocreate wilt, van hello Azure-portal Navigeer tooAutomation accounts, selecteer uw Automation-account en maakt een [referentieasset](automation-credentials.md) die Hallo-gebruikersnaam en wachtwoord voor een gebruiker met machtigingen toohello hybride worker bevat.  
3. Van uw Automation-account [hello runbook bewerken](automation-edit-textual-runbook.md)**Export RunAsCertificateToHybridWorker** en wijzigen van de waarde voor de variabele Hallo Hallo *$Password* met een sterke het wachtwoord.    Nadat u Hallo waarde wijzigen, klikt u op **publiceren** toohave Hallo conceptversie van Hallo runbook gepubliceerd. 
5. Hallo runbook starten **Export RunAsCertificateToHybridWorker**, en in Hallo **Runbook starten** blade onder de optie Hallo **instellingen uitvoeren** optie Hallo **Hybrid Worker** en in Hallo vervolgkeuzelijst selecteert Hallo Hybrid worker-groep u eerder hebt gemaakt voor dit scenario.  

    Hiermee exporteert u een certificaat toohello hybride worker zodat runbooks op Hallo worker kan verifiëren met Azure met behulp van Hallo uitvoeren als-verbinding in volgorde toomanage Azure-resources (met name voor dit scenario - import runbooks toohello Automation-account).

4. Van uw Automation-account selecteren Hallo Hybrid worker-groep eerder hebt gemaakt en [Geef een RunAs-account](automation-hrw-run-runbooks.md#runas-account) voor Hallo Hybrid worker-groep en kies Hallo-referentieasset u zojuist hebt of al hebt gemaakt.  Dit zorgt ervoor dat Hallo Sync runbook Git-opdrachten kunt uitvoeren. 
5. Hallo runbook starten **Sync LocalGitFolderToAutomationAccount**, bieden Hallo volgende vereiste invoerparameters en in Hallo **Runbook starten** blade onder de optie Hallo **uitvoeren instellingen** Hallo optie **Hybrid Worker** en in Hallo vervolgkeuzelijst selecteert Hallo Hybrid worker-groep u eerder hebt gemaakt voor dit scenario:
    * *ResourceGroup* - hello naam van de resourcegroep die zijn gekoppeld aan uw Automation-account
    * *AutomationAccountName* - hello naam van uw Automation-account
    * *GitPath* - Hallo lokale map of bestand op Hallo Hybrid Runbook Worker waarbij Git meest recente wijzigingen in toopull is ingesteld

    Dit wordt Hallo lokale Git-map op Hallo hybride worker computer synchroniseren en Hallo ps1-bestanden vervolgens importeren uit Hallo bron directory toohello Automation-account.

    ![Synchronisatie-LocalGitFolderToAutomationAccount Runbook starten](media/automation-scenario-source-control-integration-with-github-ent/start-runbook-synclocalgitfoldertoautoacct.png)<br>

7. Overzichtsgegevens voor Hallo runbook taak weergeven door deze te selecteren van Hallo **Runbooks** blade in uw Automation-account en selecteer vervolgens Hallo **taken** tegel.  Bevestig het met succes voltooid door het selecteren van Hallo **alle logboeken** tegel en bekeken Hallo gedetailleerd logboekstream.  

## <a name="next-steps"></a>Volgende stappen

-  tooknow meer informatie over runbooktypen, hun voordelen en beperkingen, Zie [Azure Automation-runbooktypen](automation-runbook-types.md)
-  Zie [Systeemeigen PowerShell-scriptondersteuning in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/) voor meer informatie over de functie voor PowerShelll-scriptondersteuning
