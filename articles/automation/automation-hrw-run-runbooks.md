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
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a><span data-ttu-id="b2c5d-103">Actieve runbooks in een hybride Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="b2c5d-103">Running runbooks on a Hybrid Runbook Worker</span></span> 
<span data-ttu-id="b2c5d-104">Er is geen verschil in de structuur Hallo van runbooks die worden uitgevoerd in Azure Automation en toepassingen die worden uitgevoerd op een hybride Runbook Worker.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-104">There is no difference in hello structure of runbooks that run in Azure Automation and those that run on a Hybrid Runbook Worker.</span></span> <span data-ttu-id="b2c5d-105">Runbooks die u met elke gebruikt waarschijnlijk aanzienlijk verschillen echter omdat runbooks die gericht is op een hybride Runbook Worker meestal resources op Hallo lokale computer zelf of op basis van bronnen in de lokale omgeving Hallo waarop deze wordt geïmplementeerd, terwijl runbooks beheren in Azure Automation-resources in Azure-cloud Hallo doorgaans te beheren.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-105">Runbooks that you use with each most likely differ significantly though since runbooks targeting a Hybrid Runbook Worker typically manage resources on hello local computer itself or against resources in hello local environment where it is deployed, while runbooks in Azure Automation typically manage resources in hello Azure cloud.</span></span>

<span data-ttu-id="b2c5d-106">Voor hybride Runbook Worker in Azure Automation kunt u een runbook bewerken, maar misschien hebt u problemen als u tootest hello runbook in Hallo-editor probeert.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-106">You can edit a runbook for Hybrid Runbook Worker in Azure Automation, but you may have difficulties if you try tootest hello runbook in hello editor.</span></span>  <span data-ttu-id="b2c5d-107">Hallo PowerShell-modules die toegang hebben tot Hallo lokale bronnen kunnen niet worden geïnstalleerd in uw Azure Automation-omgeving in dat geval, Hallo test mislukken.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-107">hello PowerShell modules that access hello local resources may not be installed in your Azure Automation environment in which case, hello test would fail.</span></span>  <span data-ttu-id="b2c5d-108">Als u installeert Hallo vereist modules, en vervolgens Hallo runbook wordt uitgevoerd, maar het lokale bronnen kunnen tooaccess voor een volledige test is niet mogelijk.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-108">If you do install hello required modules, then hello runbook will run, but it will not be able tooaccess local resources for a complete test.</span></span>

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a><span data-ttu-id="b2c5d-109">Een runbook wordt gestart op hybride Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="b2c5d-109">Starting a runbook on Hybrid Runbook Worker</span></span>
<span data-ttu-id="b2c5d-110">[Een Runbook starten in Azure Automation](automation-starting-a-runbook.md) beschrijft de verschillende methoden voor het starten van een runbook.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-110">[Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) describes different methods for starting a runbook.</span></span>  <span data-ttu-id="b2c5d-111">Hybride Runbook Worker wordt toegevoegd een **RunOn** optie waarin u de naam van een hybride Runbook Worker-groep Hallo kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-111">Hybrid Runbook Worker adds a **RunOn** option where you can specify hello name of a Hybrid Runbook Worker Group.</span></span>  <span data-ttu-id="b2c5d-112">Als een groep is opgegeven, klikt u vervolgens Hallo-runbook opgehaald en uitgevoerd door Hallo werknemers in die groep.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-112">If a group is specified, then hello runbook is retrieved and run by of hello workers in that group.</span></span>  <span data-ttu-id="b2c5d-113">Als deze optie niet is opgegeven, wordt deze uitgevoerd in Azure Automation als normaal.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-113">If this option is not specified, then it is run in Azure Automation as normal.</span></span>

<span data-ttu-id="b2c5d-114">Wanneer u een runbook in hello Azure-portal start, krijgt u een **uitvoeren op** optie waarin u kunt selecteren **Azure** of **Hybrid Worker**.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-114">When you start a runbook in hello Azure portal, you are presented with a **Run on** option where you can select **Azure** or **Hybrid Worker**.</span></span>  <span data-ttu-id="b2c5d-115">Als u selecteert **Hybrid Worker**, en vervolgens u Hallo groep uit een vervolgkeuzelijst selecteren kunt.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-115">If you select **Hybrid Worker**, then you can select hello group from a dropdown.</span></span>

<span data-ttu-id="b2c5d-116">Gebruik Hallo **RunOn** parameter.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-116">Use hello **RunOn** parameter.</span></span>  <span data-ttu-id="b2c5d-117">U kunt Hallo na de opdracht toostart een runbook met de naam Test-Runbook op een Hybrid Runbook Worker-groep met de naam MyHybridGroup met Windows PowerShell gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-117">You can use hello following command toostart a runbook named Test-Runbook on a Hybrid Runbook Worker Group named MyHybridGroup using Windows PowerShell.</span></span>

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> <span data-ttu-id="b2c5d-118">Hallo **RunOn** parameter toohello is toegevoegd **Start AzureAutomationRunbook** cmdlet in versie 0.9.1 van Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-118">hello **RunOn** parameter was added toohello **Start-AzureAutomationRunbook** cmdlet in version 0.9.1 of Microsoft Azure PowerShell.</span></span>  <span data-ttu-id="b2c5d-119">U moet [download de nieuwste versie Hallo](https://azure.microsoft.com/downloads/) als er een eerdere versie is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-119">You should [download hello latest version](https://azure.microsoft.com/downloads/) if you have an earlier one installed.</span></span>  <span data-ttu-id="b2c5d-120">U hoeft alleen tooinstall deze versie op een werkstation waar u Hallo runbook vanuit Windows PowerShell begint.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-120">You only need tooinstall this version on a workstation where you are starting hello runbook from Windows PowerShell.</span></span>  <span data-ttu-id="b2c5d-121">U hoeft geen tooinstall op Hallo worker computer tenzij u van plan toostart runbooks vanaf die computer bent.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-121">You do not need tooinstall it on hello worker computer unless you intend toostart runbooks from that computer.</span></span>  <span data-ttu-id="b2c5d-122">U kunt geen momenteel een runbook op een hybride Runbook Worker vanuit een ander runbook starten omdat hiervoor Hallo meest recente versie van Azure Powershell toobe geïnstalleerd in uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-122">You cannot currently start a runbook on a Hybrid Runbook Worker from another runbook since this would require hello latest version of Azure Powershell toobe installed in your Automation account.</span></span>  <span data-ttu-id="b2c5d-123">Hallo meest recente versie wordt automatisch bijgewerkt in Azure Automation en automatisch snel omlaag toohello werknemers is gedrukt.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-123">hello latest version is automatically updated in Azure Automation and automatically pushed down toohello workers soon.</span></span>
>
>

## <a name="runbook-permissions"></a><span data-ttu-id="b2c5d-124">Runbook-machtigingen</span><span class="sxs-lookup"><span data-stu-id="b2c5d-124">Runbook permissions</span></span>
<span data-ttu-id="b2c5d-125">Runbooks die worden uitgevoerd op een hybride Runbook Worker kan geen gebruik Hallo dezelfde methode die doorgaans voor verificatie tooAzure bronnen gebruikt wordt, omdat ze bij het openen van bronnen buiten Azure runbooks.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-125">Runbooks running on a Hybrid Runbook Worker cannot use hello same method that is typically used for runbooks authenticating tooAzure resources, since they are accessing resources outside of Azure.</span></span>  <span data-ttu-id="b2c5d-126">Hallo-runbook kan ofwel de eigen verificatie bieden toolocal bronnen of kunt u een Run as-account tooprovide een gebruikerscontext voor alle runbooks.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-126">hello runbook can either provide its own authentication toolocal resources, or you can specify a RunAs account tooprovide a user context for all runbooks.</span></span>

### <a name="runbook-authentication"></a><span data-ttu-id="b2c5d-127">Runbook-verificatie</span><span class="sxs-lookup"><span data-stu-id="b2c5d-127">Runbook authentication</span></span>
<span data-ttu-id="b2c5d-128">Runbooks wordt standaard uitgevoerd in de context van de lokale systeemaccount op Hallo on-premises computer, Hallo Hallo zodat ze hun eigen verificatie tooresources die ze toegang tot moeten opgeven.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-128">By default, runbooks will run in hello context of hello local System account on hello on-premises computer, so they must provide their own authentication tooresources that they will access.</span></span>  

<span data-ttu-id="b2c5d-129">U kunt [referentie](http://msdn.microsoft.com/library/dn940015.aspx) en [certificaat](http://msdn.microsoft.com/library/dn940013.aspx) activa in uw runbook met cmdlets waarmee u toospecify referenties zodat u resources toodifferent kunt verifiëren.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-129">You can use [Credential](http://msdn.microsoft.com/library/dn940015.aspx) and [Certificate](http://msdn.microsoft.com/library/dn940013.aspx) assets in your runbook with cmdlets that allow you toospecify credentials so you can authenticate toodifferent resources.</span></span>  <span data-ttu-id="b2c5d-130">Hallo volgende voorbeeld ziet u een deel van een runbook dat een computer wordt opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-130">hello following example shows a portion of a runbook that restarts a computer.</span></span>  <span data-ttu-id="b2c5d-131">Deze referenties opgehaald uit een referentie asset en Hallo de naam van de computer Hallo van een variabele actief en gebruikt vervolgens deze waarden met de cmdlet Hallo Restart-Computer.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-131">It retrieves credentials from a credential asset and hello name of hello computer from a variable asset and then uses these values with hello Restart-Computer cmdlet.</span></span>

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

<span data-ttu-id="b2c5d-132">U kunt ook gebruikmaken van [InlineScript](automation-powershell-workflow.md#inlinescript), zodat u kunt toorun codeblokken op een andere computer met de referenties die zijn opgegeven door Hallo [PSCredential algemene parameter](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2c5d-132">You can also leverage [InlineScript](automation-powershell-workflow.md#inlinescript), which  allows you toorun blocks of code on another computer with credentials specified by hello [PSCredential common parameter](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="runas-account"></a><span data-ttu-id="b2c5d-133">RunAs-account</span><span class="sxs-lookup"><span data-stu-id="b2c5d-133">RunAs account</span></span>
<span data-ttu-id="b2c5d-134">In plaats van runbooks bieden hun eigen verificatie toolocal bronnen, kunt u een **RunAs** account voor een Hybrid worker-groep.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-134">Instead of having runbooks provide their own authentication toolocal resources, you can specify a **RunAs** account for a Hybrid worker group.</span></span>  <span data-ttu-id="b2c5d-135">U geeft een [referentieasset](automation-credentials.md) die toegang tot toolocal bronnen heeft, en alle runbooks worden uitgevoerd onder deze referenties wanneer u gebruikmaakt van een hybride Runbook Worker in de groep Hallo.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-135">You specify a [credential asset](automation-credentials.md) that has access toolocal resources, and all runbooks run under these credentials when running on a Hybrid Runbook Worker in hello group.</span></span>  

<span data-ttu-id="b2c5d-136">Hallo-gebruikersnaam voor Hallo referentie moet in een van de volgende indelingen Hallo:</span><span class="sxs-lookup"><span data-stu-id="b2c5d-136">hello user name for hello credential must be in one of hello following formats:</span></span>

* <span data-ttu-id="b2c5d-137">domein\gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="b2c5d-137">domain\username</span></span>
* username@domain
* <span data-ttu-id="b2c5d-138">gebruikersnaam (voor accounts lokale toohello lokale computer)</span><span class="sxs-lookup"><span data-stu-id="b2c5d-138">username (for accounts local toohello on-premises computer)</span></span>

<span data-ttu-id="b2c5d-139">Gebruik hello te volgen procedure toospecify een RunAs-account voor een Hybrid worker-groep:</span><span class="sxs-lookup"><span data-stu-id="b2c5d-139">Use hello following procedure toospecify a RunAs account for a Hybrid worker group:</span></span>

1. <span data-ttu-id="b2c5d-140">Maak een [referentieasset](automation-credentials.md) met toegang tot toolocal bronnen.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-140">Create a [credential asset](automation-credentials.md) with access toolocal resources.</span></span>
2. <span data-ttu-id="b2c5d-141">Hallo Automation-account openen in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-141">Open hello Automation account in hello Azure portal.</span></span>
3. <span data-ttu-id="b2c5d-142">Selecteer Hallo **Hybrid Worker-groepen** tegel en selecteer vervolgens Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-142">Select hello **Hybrid Worker Groups** tile, and then select hello group.</span></span>
4. <span data-ttu-id="b2c5d-143">Selecteer **alle instellingen** en vervolgens **hybride worker groepsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-143">Select **All settings** and then **Hybrid worker group settings**.</span></span>
5. <span data-ttu-id="b2c5d-144">Wijziging **uitvoeren als** van **standaard** te**aangepaste**.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-144">Change **Run As** from **Default** too**Custom**.</span></span>
6. <span data-ttu-id="b2c5d-145">Selecteer Hallo referentie en op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-145">Select hello credential and click **Save**.</span></span>

### <a name="automation-run-as-account"></a><span data-ttu-id="b2c5d-146">Automation-Run As-account</span><span class="sxs-lookup"><span data-stu-id="b2c5d-146">Automation Run As account</span></span>
<span data-ttu-id="b2c5d-147">Als onderdeel van uw automatische proces voor het implementeren van resources in Azure, hebt u mogelijk nodig toegang tooon-premises systemen toosupport een taak of een reeks stappen in de volgorde van de implementatie.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-147">As part of your automated build process for deploying resources in Azure, you may require access tooon-premise systems toosupport a task or set of steps in your deployment sequence.</span></span>  <span data-ttu-id="b2c5d-148">toosupport verificatie op basis van Azure met behulp van Hallo Run As-account, moet u tooinstall Hallo Run As-accountcertificaat.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-148">toosupport authentication against Azure using hello Run As account, you need tooinstall hello Run As account certificate.</span></span>  

<span data-ttu-id="b2c5d-149">Hallo volgende PowerShell-runbook *Export RunAsCertificateToHybridWorker*, Hallo uitvoeren als het certificaat exporteert van uw Azure Automation-account en downloadt en importeert u het in het certificaatarchief van de lokale machine Hallo op een Hybride worker verbonden toohello hetzelfde account.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-149">hello following PowerShell runbook, *Export-RunAsCertificateToHybridWorker*, exports hello Run As certificate from your Azure Automation account and downloads and imports it into hello local machine certificate store on a Hybrid worker connected toohello same account.</span></span>  <span data-ttu-id="b2c5d-150">Zodra deze stap is voltooid, controleert u of Hallo worker kan worden geverifieerd tooAzure Hallo Run As-account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-150">Once that step is completed, it verifies hello worker can successfully authenticate tooAzure using hello Run As account.</span></span>

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

<span data-ttu-id="b2c5d-151">Hallo opslaan *Export RunAsCertificateToHybridWorker* runbook tooyour computer met een `.ps1` extensie.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-151">Save hello *Export-RunAsCertificateToHybridWorker* runbook tooyour computer with a `.ps1` extension.</span></span>  <span data-ttu-id="b2c5d-152">Importeren in uw Automation-account en het bewerken van Hallo runbook wijzigen in een waarde van variabele Hallo Hallo `$Password` met uw eigen wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-152">Import it into your Automation account and edit hello runbook, changing hello value of hello variable `$Password` with your own password.</span></span>  <span data-ttu-id="b2c5d-153">Publiceren en voer vervolgens Hallo runbook die gericht is op Hallo Hybrid Worker-groep die worden uitgevoerd en verifiëren van runbooks met Hallo Run As-account.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-153">Publish and then run hello runbook targeting hello Hybrid Worker group that run and authenticate runbooks using hello Run As account.</span></span>  <span data-ttu-id="b2c5d-154">Hallo taak stroom rapporten Hallo poging tooimport Hallo certificaat in archief van de lokale computer Hallo en volgt met meerdere regels, afhankelijk van hoeveel Automation-accounts zijn gedefinieerd in uw abonnement en als verificatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-154">hello job stream reports hello attempt tooimport hello certificate into hello local machine store, and follows with multiple lines depending on how many Automation accounts are defined in your subscription and if authentication is successful.</span></span>  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a><span data-ttu-id="b2c5d-155">Het oplossen van runbooks op hybride Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="b2c5d-155">Troubleshooting runbooks on Hybrid Runbook Worker</span></span>
<span data-ttu-id="b2c5d-156">Logboeken worden lokaal opgeslagen op elke worker hybride op C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-156">Logs are stored locally on each hybrid worker at C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span></span>  <span data-ttu-id="b2c5d-157">Hybride worker registreert ook fouten en gebeurtenissen in het Windows-gebeurtenislogboek Hallo onder **toepassingen en Services Logs\Microsoft-SMA\Operational**.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-157">Hybrid worker also records errors and events in hello Windows event log under **Application and Services Logs\Microsoft-SMA\Operational**.</span></span>  <span data-ttu-id="b2c5d-158">Gebeurtenissen met betrekking toorunbooks op Hallo worker uitgevoerd te worden geschreven**toepassingen en Services Logs\Microsoft-Automation\Operational**.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-158">Events related toorunbooks executed on hello worker are written too**Application and Services Logs\Microsoft-Automation\Operational**.</span></span>  <span data-ttu-id="b2c5d-159">Hallo **Microsoft SMA** logboek bevat veel meer gebeurtenissen gerelateerde toohello runbook taak pushed toohello worker en Hallo verwerking van de Hallo runbook.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-159">hello **Microsoft-SMA** log includes many more events related toohello runbook job pushed toohello worker and hello processing of hello runbook.</span></span>  <span data-ttu-id="b2c5d-160">Tijdens het Hallo **Microsoft Automation** gebeurtenislogboek niet veel gebeurtenissen met details te helpen bij het oplossen van de runbook-uitvoering van hello, vindt u ten minste Hallo resultaten van de runbooktaak Hallo.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-160">While hello **Microsoft-Automation** event log does not have many events with details assisting with hello troubleshooting of runbook execution, you will at least find hello results of hello runbook job.</span></span>  

<span data-ttu-id="b2c5d-161">[Runbook uitvoer en berichten](automation-runbook-output-and-messages.md) tooAzure automatisering van hybrid workers net zoals runbooktaken uitvoeren in Hallo cloud worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-161">[Runbook output and messages](automation-runbook-output-and-messages.md) are sent tooAzure Automation from hybrid workers just like runbook jobs run in hello cloud.</span></span>  <span data-ttu-id="b2c5d-162">U kunt ook inschakelen Hallo uitgebreid en voortgang streams Hallo dezelfde manier als voor andere runbooks.</span><span class="sxs-lookup"><span data-stu-id="b2c5d-162">You can also enable hello Verbose and Progress streams hello same way you would for other runbooks.</span></span>  

<span data-ttu-id="b2c5d-163">Als uw runbooks zijn niet voltooid en Hallo taak overzicht de status van toont **onderbroken**, Controleer artikel probleemoplossing Hallo [Hybrid Runbook Worker: een runbooktaak wordt beëindigd met de status Onderbroken](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span><span class="sxs-lookup"><span data-stu-id="b2c5d-163">If your runbooks are not completing successfully and hello job summary shows a status of **Suspended**, please review hello troubleshooting article [Hybrid Runbook Worker: A runbook job terminates with a status of Suspended](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span></span>   

## <a name="next-steps"></a><span data-ttu-id="b2c5d-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b2c5d-164">Next steps</span></span>
* <span data-ttu-id="b2c5d-165">Zie toolearn meer informatie over Hallo verschillende methoden die gebruikt toostart een runbook worden kunnen [een Runbook starten in Azure Automation](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="b2c5d-165">toolearn more about hello different methods that can be used toostart a runbook, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>  
* <span data-ttu-id="b2c5d-166">toounderstand hello verschillende procedures voor het werken met PowerShell en PowerShell Workflow-runbooks in Azure Automation met behulp van de teksteditor hello, Zie [bewerken van een Runbook in Azure Automation](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="b2c5d-166">toounderstand hello different procedures for working with PowerShell and PowerShell Workflow runbooks in Azure Automation using hello textual editor, see [Editing a Runbook in Azure Automation](automation-edit-textual-runbook.md)</span></span>
