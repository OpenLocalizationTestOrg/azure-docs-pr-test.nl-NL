---
title: runbooks in Azure Automation Hybrid Runbook Worker aaaRun | Microsoft Docs
description: Dit artikel bevat informatie over het uitvoeren van runbooks op computers in uw lokale datacentrum of cloudprovider met Hallo Hybrid Runbook Worker-rol.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/22/2017
ms.author: magoedte
ms.openlocfilehash: 51961e02603e5690edd11e577594ad2ddea489a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a>Actieve runbooks in een hybride Runbook Worker 
Er is geen verschil in de structuur Hallo van runbooks die worden uitgevoerd in Azure Automation en toepassingen die worden uitgevoerd op een hybride Runbook Worker. Runbooks die u met elke gebruikt waarschijnlijk aanzienlijk verschillen echter omdat runbooks die gericht is op een hybride Runbook Worker meestal resources op Hallo lokale computer zelf of op basis van bronnen in de lokale omgeving Hallo waarop deze wordt geïmplementeerd, terwijl runbooks beheren in Azure Automation-resources in Azure-cloud Hallo doorgaans te beheren.

Voor hybride Runbook Worker in Azure Automation kunt u een runbook bewerken, maar misschien hebt u problemen als u tootest hello runbook in Hallo-editor probeert.  Hallo PowerShell-modules die toegang hebben tot Hallo lokale bronnen kunnen niet worden geïnstalleerd in uw Azure Automation-omgeving in dat geval, Hallo test mislukken.  Als u installeert Hallo vereist modules, en vervolgens Hallo runbook wordt uitgevoerd, maar het lokale bronnen kunnen tooaccess voor een volledige test is niet mogelijk.

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a>Een runbook wordt gestart op hybride Runbook Worker
[Een Runbook starten in Azure Automation](automation-starting-a-runbook.md) beschrijft de verschillende methoden voor het starten van een runbook.  Hybride Runbook Worker wordt toegevoegd een **RunOn** optie waarin u de naam van een hybride Runbook Worker-groep Hallo kunt opgeven.  Als een groep is opgegeven, klikt u vervolgens Hallo-runbook opgehaald en uitgevoerd door Hallo werknemers in die groep.  Als deze optie niet is opgegeven, wordt deze uitgevoerd in Azure Automation als normaal.

Wanneer u een runbook in hello Azure-portal start, krijgt u een **uitvoeren op** optie waarin u kunt selecteren **Azure** of **Hybrid Worker**.  Als u selecteert **Hybrid Worker**, en vervolgens u Hallo groep uit een vervolgkeuzelijst selecteren kunt.

Gebruik Hallo **RunOn** parameter.  U kunt Hallo na de opdracht toostart een runbook met de naam Test-Runbook op een Hybrid Runbook Worker-groep met de naam MyHybridGroup met Windows PowerShell gebruiken.

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> Hallo **RunOn** parameter toohello is toegevoegd **Start AzureAutomationRunbook** cmdlet in versie 0.9.1 van Microsoft Azure PowerShell.  U moet [download de nieuwste versie Hallo](https://azure.microsoft.com/downloads/) als er een eerdere versie is geïnstalleerd.  U hoeft alleen tooinstall deze versie op een werkstation waar u Hallo runbook vanuit Windows PowerShell begint.  U hoeft geen tooinstall op Hallo worker computer tenzij u van plan toostart runbooks vanaf die computer bent.  U kunt geen momenteel een runbook op een hybride Runbook Worker vanuit een ander runbook starten omdat hiervoor Hallo meest recente versie van Azure Powershell toobe geïnstalleerd in uw Automation-account.  Hallo meest recente versie wordt automatisch bijgewerkt in Azure Automation en automatisch snel omlaag toohello werknemers is gedrukt.
>
>

## <a name="runbook-permissions"></a>Runbook-machtigingen
Runbooks die worden uitgevoerd op een hybride Runbook Worker kan geen gebruik Hallo dezelfde methode die doorgaans voor verificatie tooAzure bronnen gebruikt wordt, omdat ze bij het openen van bronnen buiten Azure runbooks.  Hallo-runbook kan ofwel de eigen verificatie bieden toolocal bronnen of kunt u een Run as-account tooprovide een gebruikerscontext voor alle runbooks.

### <a name="runbook-authentication"></a>Runbook-verificatie
Runbooks wordt standaard uitgevoerd in de context van de lokale systeemaccount op Hallo on-premises computer, Hallo Hallo zodat ze hun eigen verificatie tooresources die ze toegang tot moeten opgeven.  

U kunt [referentie](http://msdn.microsoft.com/library/dn940015.aspx) en [certificaat](http://msdn.microsoft.com/library/dn940013.aspx) activa in uw runbook met cmdlets waarmee u toospecify referenties zodat u resources toodifferent kunt verifiëren.  Hallo volgende voorbeeld ziet u een deel van een runbook dat een computer wordt opnieuw opgestart.  Deze referenties opgehaald uit een referentie asset en Hallo de naam van de computer Hallo van een variabele actief en gebruikt vervolgens deze waarden met de cmdlet Hallo Restart-Computer.

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

U kunt ook gebruikmaken van [InlineScript](automation-powershell-workflow.md#inlinescript), zodat u kunt toorun codeblokken op een andere computer met de referenties die zijn opgegeven door Hallo [PSCredential algemene parameter](http://technet.microsoft.com/library/jj129719.aspx).

### <a name="runas-account"></a>RunAs-account
In plaats van runbooks bieden hun eigen verificatie toolocal bronnen, kunt u een **RunAs** account voor een Hybrid worker-groep.  U geeft een [referentieasset](automation-credentials.md) die toegang tot toolocal bronnen heeft, en alle runbooks worden uitgevoerd onder deze referenties wanneer u gebruikmaakt van een hybride Runbook Worker in de groep Hallo.  

Hallo-gebruikersnaam voor Hallo referentie moet in een van de volgende indelingen Hallo:

* domein\gebruikersnaam
* username@domain
* gebruikersnaam (voor accounts lokale toohello lokale computer)

Gebruik hello te volgen procedure toospecify een RunAs-account voor een Hybrid worker-groep:

1. Maak een [referentieasset](automation-credentials.md) met toegang tot toolocal bronnen.
2. Hallo Automation-account openen in hello Azure-portal.
3. Selecteer Hallo **Hybrid Worker-groepen** tegel en selecteer vervolgens Hallo-groep.
4. Selecteer **alle instellingen** en vervolgens **hybride worker groepsinstellingen**.
5. Wijziging **uitvoeren als** van **standaard** te**aangepaste**.
6. Selecteer Hallo referentie en op **opslaan**.

### <a name="automation-run-as-account"></a>Automation-Run As-account
Als onderdeel van uw automatische proces voor het implementeren van resources in Azure, hebt u mogelijk nodig toegang tooon-premises systemen toosupport een taak of een reeks stappen in de volgorde van de implementatie.  toosupport verificatie op basis van Azure met behulp van Hallo Run As-account, moet u tooinstall Hallo Run As-accountcertificaat.  

Hallo volgende PowerShell-runbook *Export RunAsCertificateToHybridWorker*, Hallo uitvoeren als het certificaat exporteert van uw Azure Automation-account en downloadt en importeert u het in het certificaatarchief van de lokale machine Hallo op een Hybride worker verbonden toohello hetzelfde account.  Zodra deze stap is voltooid, controleert u of Hallo worker kan worden geverifieerd tooAzure Hallo Run As-account gebruiken.

    <#PSScriptInfo
    .VERSION 1.0
    .GUID 3a796b9a-623d-499d-86c8-c249f10a6986
    .AUTHOR Azure Automation Team
    .COMPANYNAME Microsoft
    .COPYRIGHT 
    .TAGS Azure Automation 
    .LICENSEURI 
    .PROJECTURI 
    .ICONURI 
    .EXTERNALMODULEDEPENDENCIES 
    .REQUIREDSCRIPTS 
    .EXTERNALSCRIPTDEPENDENCIES 
    .RELEASENOTES
    #>

    <#  
    .SYNOPSIS  
    Exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account.
    Run this runbook in hello hybrid worker where you want hello certificate installed.
    This allows hello use of hello AzureRunAsConnection tooauthenticate tooAzure and manage Azure resources from runbooks running in hello hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set hello password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get hello management certificate that will be used toomake calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location toostore temporary certificate in hello Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save hello certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication tooAzure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts tooconfirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

Hallo opslaan *Export RunAsCertificateToHybridWorker* runbook tooyour computer met een `.ps1` extensie.  Importeren in uw Automation-account en het bewerken van Hallo runbook wijzigen in een waarde van variabele Hallo Hallo `$Password` met uw eigen wachtwoord.  Publiceren en voer vervolgens Hallo runbook die gericht is op Hallo Hybrid Worker-groep die worden uitgevoerd en verifiëren van runbooks met Hallo Run As-account.  Hallo taak stroom rapporten Hallo poging tooimport Hallo certificaat in archief van de lokale computer Hallo en volgt met meerdere regels, afhankelijk van hoeveel Automation-accounts zijn gedefinieerd in uw abonnement en als verificatie geslaagd is.  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a>Het oplossen van runbooks op hybride Runbook Worker
Logboeken worden lokaal opgeslagen op elke worker hybride op C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.  Hybride worker registreert ook fouten en gebeurtenissen in het Windows-gebeurtenislogboek Hallo onder **toepassingen en Services Logs\Microsoft-SMA\Operational**.  Gebeurtenissen met betrekking toorunbooks op Hallo worker uitgevoerd te worden geschreven**toepassingen en Services Logs\Microsoft-Automation\Operational**.  Hallo **Microsoft SMA** logboek bevat veel meer gebeurtenissen gerelateerde toohello runbook taak pushed toohello worker en Hallo verwerking van de Hallo runbook.  Tijdens het Hallo **Microsoft Automation** gebeurtenislogboek niet veel gebeurtenissen met details te helpen bij het oplossen van de runbook-uitvoering van hello, vindt u ten minste Hallo resultaten van de runbooktaak Hallo.  

[Runbook uitvoer en berichten](automation-runbook-output-and-messages.md) tooAzure automatisering van hybrid workers net zoals runbooktaken uitvoeren in Hallo cloud worden verzonden.  U kunt ook inschakelen Hallo uitgebreid en voortgang streams Hallo dezelfde manier als voor andere runbooks.  

Als uw runbooks zijn niet voltooid en Hallo taak overzicht de status van toont **onderbroken**, Controleer artikel probleemoplossing Hallo [Hybrid Runbook Worker: een runbooktaak wordt beëindigd met de status Onderbroken](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).   

## <a name="next-steps"></a>Volgende stappen
* Zie toolearn meer informatie over Hallo verschillende methoden die gebruikt toostart een runbook worden kunnen [een Runbook starten in Azure Automation](automation-starting-a-runbook.md).  
* toounderstand hello verschillende procedures voor het werken met PowerShell en PowerShell Workflow-runbooks in Azure Automation met behulp van de teksteditor hello, Zie [bewerken van een Runbook in Azure Automation](automation-edit-textual-runbook.md)
