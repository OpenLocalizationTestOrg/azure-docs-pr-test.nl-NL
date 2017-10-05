---
title: Runbooks worden uitgevoerd op Azure Automation Hybrid Runbook Worker | Microsoft Docs
description: Dit artikel bevat informatie over het uitvoeren van runbooks op computers in uw lokale datacentrum of cloudprovider met de hybride Runbook Worker-rol.
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
ms.openlocfilehash: 993bc3ea480a329541ca4ae825189cdb5a2b4a8b
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a><span data-ttu-id="e7e01-103">Actieve runbooks in een hybride Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="e7e01-103">Running runbooks on a Hybrid Runbook Worker</span></span> 
<span data-ttu-id="e7e01-104">Er is geen verschil in de structuur van runbooks die worden uitgevoerd in Azure Automation en toepassingen die worden uitgevoerd op een hybride Runbook Worker.</span><span class="sxs-lookup"><span data-stu-id="e7e01-104">There is no difference in the structure of runbooks that run in Azure Automation and those that run on a Hybrid Runbook Worker.</span></span> <span data-ttu-id="e7e01-105">Runbooks die u met elke gebruikt waarschijnlijk aanzienlijk verschillen echter omdat runbooks die gericht is op een hybride Runbook Worker doorgaans bronnen op de lokale computer zelf of op basis van bronnen in de lokale omgeving waarop deze wordt geïmplementeerd, terwijl runbooks in beheren Azure Automation beheren meestal bronnen in de Azure-cloud.</span><span class="sxs-lookup"><span data-stu-id="e7e01-105">Runbooks that you use with each most likely differ significantly though since runbooks targeting a Hybrid Runbook Worker typically manage resources on the local computer itself or against resources in the local environment where it is deployed, while runbooks in Azure Automation typically manage resources in the Azure cloud.</span></span>

<span data-ttu-id="e7e01-106">U kunt een runbook bewerken voor hybride Runbook Worker in Azure Automation, maar misschien hebt u problemen als u probeert het runbook testen in de editor.</span><span class="sxs-lookup"><span data-stu-id="e7e01-106">You can edit a runbook for Hybrid Runbook Worker in Azure Automation, but you may have difficulties if you try to test the runbook in the editor.</span></span>  <span data-ttu-id="e7e01-107">De PowerShell-modules die toegang hebben tot de lokale bronnen kunnen niet worden geïnstalleerd in uw Azure Automation-omgeving in dat geval de test mislukt.</span><span class="sxs-lookup"><span data-stu-id="e7e01-107">The PowerShell modules that access the local resources may not be installed in your Azure Automation environment in which case, the test would fail.</span></span>  <span data-ttu-id="e7e01-108">Als u de vereiste modules installeert, klikt u vervolgens het runbook wordt uitgevoerd, maar wordt niet mogelijk is de toegang tot lokale bronnen voor een volledige test.</span><span class="sxs-lookup"><span data-stu-id="e7e01-108">If you do install the required modules, then the runbook will run, but it will not be able to access local resources for a complete test.</span></span>

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a><span data-ttu-id="e7e01-109">Een runbook wordt gestart op hybride Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="e7e01-109">Starting a runbook on Hybrid Runbook Worker</span></span>
<span data-ttu-id="e7e01-110">[Een Runbook starten in Azure Automation](automation-starting-a-runbook.md) beschrijft de verschillende methoden voor het starten van een runbook.</span><span class="sxs-lookup"><span data-stu-id="e7e01-110">[Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) describes different methods for starting a runbook.</span></span>  <span data-ttu-id="e7e01-111">Hybride Runbook Worker wordt toegevoegd een **RunOn** optie waarin u de naam van een hybride Runbook Worker-groep kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="e7e01-111">Hybrid Runbook Worker adds a **RunOn** option where you can specify the name of a Hybrid Runbook Worker Group.</span></span>  <span data-ttu-id="e7e01-112">Als u een groep opgeeft, wordt het runbook de opgehaald en uitgevoerd door de werknemers in die groep.</span><span class="sxs-lookup"><span data-stu-id="e7e01-112">If a group is specified, then the runbook is retrieved and run by of the workers in that group.</span></span>  <span data-ttu-id="e7e01-113">Als deze optie niet is opgegeven, wordt deze uitgevoerd in Azure Automation als normaal.</span><span class="sxs-lookup"><span data-stu-id="e7e01-113">If this option is not specified, then it is run in Azure Automation as normal.</span></span>

<span data-ttu-id="e7e01-114">Wanneer u een runbook in de Azure portal start, krijgt u een **uitvoeren op** optie waarin u kunt selecteren **Azure** of **Hybrid Worker**.</span><span class="sxs-lookup"><span data-stu-id="e7e01-114">When you start a runbook in the Azure portal, you are presented with a **Run on** option where you can select **Azure** or **Hybrid Worker**.</span></span>  <span data-ttu-id="e7e01-115">Als u selecteert **Hybrid Worker**, kunt u de groep uit een vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="e7e01-115">If you select **Hybrid Worker**, then you can select the group from a dropdown.</span></span>

<span data-ttu-id="e7e01-116">Gebruik de **RunOn** parameter.</span><span class="sxs-lookup"><span data-stu-id="e7e01-116">Use the **RunOn** parameter.</span></span>  <span data-ttu-id="e7e01-117">U kunt de volgende opdracht gebruiken om een runbook met de naam Test-Runbook op een Hybrid Runbook Worker-groep met de naam MyHybridGroup met Windows PowerShell te starten.</span><span class="sxs-lookup"><span data-stu-id="e7e01-117">You can use the following command to start a runbook named Test-Runbook on a Hybrid Runbook Worker Group named MyHybridGroup using Windows PowerShell.</span></span>

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> <span data-ttu-id="e7e01-118">De **RunOn** parameter is toegevoegd aan de **Start AzureAutomationRunbook** cmdlet in versie 0.9.1 van Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7e01-118">The **RunOn** parameter was added to the **Start-AzureAutomationRunbook** cmdlet in version 0.9.1 of Microsoft Azure PowerShell.</span></span>  <span data-ttu-id="e7e01-119">U moet [de nieuwste versie downloaden](https://azure.microsoft.com/downloads/) als er een eerdere versie is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e7e01-119">You should [download the latest version](https://azure.microsoft.com/downloads/) if you have an earlier one installed.</span></span>  <span data-ttu-id="e7e01-120">U hoeft alleen te installeren van deze versie op een werkstation waarop het runbook wordt gestart vanuit Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7e01-120">You only need to install this version on a workstation where you are starting the runbook from Windows PowerShell.</span></span>  <span data-ttu-id="e7e01-121">U hoeft niet te installeren op de computer van de werknemer, tenzij u van plan bent runbooks starten vanaf die computer.</span><span class="sxs-lookup"><span data-stu-id="e7e01-121">You do not need to install it on the worker computer unless you intend to start runbooks from that computer.</span></span>  <span data-ttu-id="e7e01-122">U kunt geen momenteel een runbook starten op een hybride Runbook Worker vanuit een ander runbook omdat dit de meest recente versie van Azure Powershell worden geïnstalleerd in uw Automation-account vereist.</span><span class="sxs-lookup"><span data-stu-id="e7e01-122">You cannot currently start a runbook on a Hybrid Runbook Worker from another runbook since this would require the latest version of Azure Powershell to be installed in your Automation account.</span></span>  <span data-ttu-id="e7e01-123">De nieuwste versie wordt automatisch bijgewerkt in Azure Automation en automatisch vanaf de werknemers snel.</span><span class="sxs-lookup"><span data-stu-id="e7e01-123">The latest version is automatically updated in Azure Automation and automatically pushed down to the workers soon.</span></span>
>
>

## <a name="runbook-permissions"></a><span data-ttu-id="e7e01-124">Runbook-machtigingen</span><span class="sxs-lookup"><span data-stu-id="e7e01-124">Runbook permissions</span></span>
<span data-ttu-id="e7e01-125">Runbooks die worden uitgevoerd op een hybride Runbook Worker niet dezelfde methode die doorgaans gebruikt wordt voor runbooks die worden geverifieerd voor Azure-resources, omdat ze bij het openen van bronnen buiten Azure gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e7e01-125">Runbooks running on a Hybrid Runbook Worker cannot use the same method that is typically used for runbooks authenticating to Azure resources, since they are accessing resources outside of Azure.</span></span>  <span data-ttu-id="e7e01-126">Het runbook kan ofwel de eigen verificatie tot lokale bronnen bieden of kunt u een RunAs-account om een gebruikerscontext voor alle runbooks.</span><span class="sxs-lookup"><span data-stu-id="e7e01-126">The runbook can either provide its own authentication to local resources, or you can specify a RunAs account to provide a user context for all runbooks.</span></span>

### <a name="runbook-authentication"></a><span data-ttu-id="e7e01-127">Runbook-verificatie</span><span class="sxs-lookup"><span data-stu-id="e7e01-127">Runbook authentication</span></span>
<span data-ttu-id="e7e01-128">Standaard wordt runbooks uitgevoerd in de context van het lokale systeemaccount op de lokale computer, zodat ze hun eigen verificatiegegevens aan resources die ze toegang hebben tot moeten opgeven.</span><span class="sxs-lookup"><span data-stu-id="e7e01-128">By default, runbooks will run in the context of the local System account on the on-premises computer, so they must provide their own authentication to resources that they will access.</span></span>  

<span data-ttu-id="e7e01-129">U kunt [referentie](http://msdn.microsoft.com/library/dn940015.aspx) en [certificaat](http://msdn.microsoft.com/library/dn940013.aspx) activa in uw runbook met cmdlets waarmee u referenties opgeven zodat kan worden geverifieerd voor verschillende bronnen.</span><span class="sxs-lookup"><span data-stu-id="e7e01-129">You can use [Credential](http://msdn.microsoft.com/library/dn940015.aspx) and [Certificate](http://msdn.microsoft.com/library/dn940013.aspx) assets in your runbook with cmdlets that allow you to specify credentials so you can authenticate to different resources.</span></span>  <span data-ttu-id="e7e01-130">Het volgende voorbeeld ziet u een deel van een runbook dat een computer wordt opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="e7e01-130">The following example shows a portion of a runbook that restarts a computer.</span></span>  <span data-ttu-id="e7e01-131">Deze referenties opgehaald uit een referentie-element en de naam van de computer van een variabele asset en gebruikt vervolgens deze waarden met de cmdlet Restart-Computer.</span><span class="sxs-lookup"><span data-stu-id="e7e01-131">It retrieves credentials from a credential asset and the name of the computer from a variable asset and then uses these values with the Restart-Computer cmdlet.</span></span>

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

<span data-ttu-id="e7e01-132">U kunt ook gebruikmaken van [InlineScript](automation-powershell-workflow.md#inlinescript), waarmee u blokken code uitvoeren op een andere computer met de referenties die zijn opgegeven door de [PSCredential algemene parameter](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="e7e01-132">You can also leverage [InlineScript](automation-powershell-workflow.md#inlinescript), which  allows you to run blocks of code on another computer with credentials specified by the [PSCredential common parameter](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="runas-account"></a><span data-ttu-id="e7e01-133">RunAs-account</span><span class="sxs-lookup"><span data-stu-id="e7e01-133">RunAs account</span></span>
<span data-ttu-id="e7e01-134">In plaats van runbooks bieden hun eigen verificatie van lokale bronnen, kunt u een **RunAs** account voor een Hybrid worker-groep.</span><span class="sxs-lookup"><span data-stu-id="e7e01-134">Instead of having runbooks provide their own authentication to local resources, you can specify a **RunAs** account for a Hybrid worker group.</span></span>  <span data-ttu-id="e7e01-135">U geeft een [referentieasset](automation-credentials.md) die toegang heeft tot de lokale bronnen en alle runbooks worden uitgevoerd onder deze referenties wanneer u gebruikmaakt van een hybride Runbook Worker in de groep.</span><span class="sxs-lookup"><span data-stu-id="e7e01-135">You specify a [credential asset](automation-credentials.md) that has access to local resources, and all runbooks run under these credentials when running on a Hybrid Runbook Worker in the group.</span></span>  

<span data-ttu-id="e7e01-136">De gebruikersnaam op voor de referentie moet worden gebruikt in een van de volgende indelingen:</span><span class="sxs-lookup"><span data-stu-id="e7e01-136">The user name for the credential must be in one of the following formats:</span></span>

* <span data-ttu-id="e7e01-137">domein\gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="e7e01-137">domain\username</span></span>
* username@domain
* <span data-ttu-id="e7e01-138">gebruikersnaam (voor accounts die lokaal op de lokale computer)</span><span class="sxs-lookup"><span data-stu-id="e7e01-138">username (for accounts local to the on-premises computer)</span></span>

<span data-ttu-id="e7e01-139">Gebruik de volgende procedure om op te geven van een RunAs-account voor een Hybrid worker-groep:</span><span class="sxs-lookup"><span data-stu-id="e7e01-139">Use the following procedure to specify a RunAs account for a Hybrid worker group:</span></span>

1. <span data-ttu-id="e7e01-140">Maak een [referentieasset](automation-credentials.md) met toegang tot lokale bronnen.</span><span class="sxs-lookup"><span data-stu-id="e7e01-140">Create a [credential asset](automation-credentials.md) with access to local resources.</span></span>
2. <span data-ttu-id="e7e01-141">Open het Automation-account in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e7e01-141">Open the Automation account in the Azure portal.</span></span>
3. <span data-ttu-id="e7e01-142">Selecteer de **Hybrid Worker-groepen** tegel en selecteer vervolgens de groep.</span><span class="sxs-lookup"><span data-stu-id="e7e01-142">Select the **Hybrid Worker Groups** tile, and then select the group.</span></span>
4. <span data-ttu-id="e7e01-143">Selecteer **alle instellingen** en vervolgens **hybride worker groepsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="e7e01-143">Select **All settings** and then **Hybrid worker group settings**.</span></span>
5. <span data-ttu-id="e7e01-144">Wijziging **Run As-** van **standaard** naar **aangepaste**.</span><span class="sxs-lookup"><span data-stu-id="e7e01-144">Change **Run As** from **Default** to **Custom**.</span></span>
6. <span data-ttu-id="e7e01-145">Selecteer de referentie en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e7e01-145">Select the credential and click **Save**.</span></span>

### <a name="automation-run-as-account"></a><span data-ttu-id="e7e01-146">Automation-Run As-account</span><span class="sxs-lookup"><span data-stu-id="e7e01-146">Automation Run As account</span></span>
<span data-ttu-id="e7e01-147">Als onderdeel van uw automatische proces voor het implementeren van resources in Azure, hebt u toegang tot on-premises systemen ter ondersteuning van een taak of een reeks stappen in de volgorde van de implementatie mogelijk nodig.</span><span class="sxs-lookup"><span data-stu-id="e7e01-147">As part of your automated build process for deploying resources in Azure, you may require access to on-premise systems to support a task or set of steps in your deployment sequence.</span></span>  <span data-ttu-id="e7e01-148">Ter ondersteuning van verificatie op basis van Azure met behulp van het Run As-account, moet u het Run As-account-certificaat installeren.</span><span class="sxs-lookup"><span data-stu-id="e7e01-148">To support authentication against Azure using the Run As account, you need to install the Run As account certificate.</span></span>  

<span data-ttu-id="e7e01-149">De volgende PowerShell-runbook *Export RunAsCertificateToHybridWorker*, exporteert u het Run As-certificaat van uw Azure Automation-account en downloadt en in het certificaatarchief van de lokale computer op een hybride worden geïmporteerd werknemer is verbonden met hetzelfde account.</span><span class="sxs-lookup"><span data-stu-id="e7e01-149">The following PowerShell runbook, *Export-RunAsCertificateToHybridWorker*, exports the Run As certificate from your Azure Automation account and downloads and imports it into the local machine certificate store on a Hybrid worker connected to the same account.</span></span>  <span data-ttu-id="e7e01-150">Zodra deze stap is voltooid, controleert u of dat het werkproces kan worden geverifieerd in Azure maken met het Run As-account.</span><span class="sxs-lookup"><span data-stu-id="e7e01-150">Once that step is completed, it verifies the worker can successfully authenticate to Azure using the Run As account.</span></span>

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
    Exports the Run As certificate from an Azure Automation account to a hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports the Run As certificate from an Azure Automation account to a hybrid worker in that account.
    Run this runbook in the hybrid worker where you want the certificate installed.
    This allows the use of the AzureRunAsConnection to authenticate to Azure and manage Azure resources from runbooks running in the hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set the password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get the management certificate that will be used to make calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location to store temporary certificate in the Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save the certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication to Azure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts to confirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

<span data-ttu-id="e7e01-151">Sla de *Export RunAsCertificateToHybridWorker* runbook op uw computer met een `.ps1` extensie.</span><span class="sxs-lookup"><span data-stu-id="e7e01-151">Save the *Export-RunAsCertificateToHybridWorker* runbook to your computer with a `.ps1` extension.</span></span>  <span data-ttu-id="e7e01-152">Importeren in uw Automation-account en het bewerken van het runbook, als u de waarde van de variabele `$Password` met uw eigen wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="e7e01-152">Import it into your Automation account and edit the runbook, changing the value of the variable `$Password` with your own password.</span></span>  <span data-ttu-id="e7e01-153">Publiceren en voer vervolgens het runbook die gericht is op de Hybrid Worker-groep die worden uitgevoerd en verifiëren van runbooks met het Run As-account.</span><span class="sxs-lookup"><span data-stu-id="e7e01-153">Publish and then run the runbook targeting the Hybrid Worker group that run and authenticate runbooks using the Run As account.</span></span>  <span data-ttu-id="e7e01-154">De taakstroom rapporteert de poging om het certificaat importeren in het archief van de lokale computer en volgt met meerdere regels, afhankelijk van hoeveel Automation-accounts zijn gedefinieerd in uw abonnement en als verificatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="e7e01-154">The job stream reports the attempt to import the certificate into the local machine store, and follows with multiple lines depending on how many Automation accounts are defined in your subscription and if authentication is successful.</span></span>  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a><span data-ttu-id="e7e01-155">Het oplossen van runbooks op hybride Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="e7e01-155">Troubleshooting runbooks on Hybrid Runbook Worker</span></span>
<span data-ttu-id="e7e01-156">Logboeken worden lokaal opgeslagen op elke worker hybride op C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span><span class="sxs-lookup"><span data-stu-id="e7e01-156">Logs are stored locally on each hybrid worker at C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span></span>  <span data-ttu-id="e7e01-157">Hybride worker registreert ook fouten en gebeurtenissen in het Windows-gebeurtenislogboek onder **toepassingen en Services Logs\Microsoft-SMA\Operational**.</span><span class="sxs-lookup"><span data-stu-id="e7e01-157">Hybrid worker also records errors and events in the Windows event log under **Application and Services Logs\Microsoft-SMA\Operational**.</span></span>  <span data-ttu-id="e7e01-158">Gebeurtenissen met betrekking tot runbooks die worden uitgevoerd op de worker worden geschreven naar **toepassingen en Services Logs\Microsoft-Automation\Operational**.</span><span class="sxs-lookup"><span data-stu-id="e7e01-158">Events related to runbooks executed on the worker are written to **Application and Services Logs\Microsoft-Automation\Operational**.</span></span>  <span data-ttu-id="e7e01-159">De **Microsoft SMA** logboek bevat veel meer gebeurtenissen met betrekking tot de runbooktaak die naar de werknemer en de verwerking van het runbook gepusht.</span><span class="sxs-lookup"><span data-stu-id="e7e01-159">The **Microsoft-SMA** log includes many more events related to the runbook job pushed to the worker and the processing of the runbook.</span></span>  <span data-ttu-id="e7e01-160">Terwijl de **Microsoft Automation** gebeurtenislogboek niet veel gebeurtenissen met details hulp bij het oplossen van problemen met de uitvoering van runbook, vindt u ten minste de resultaten van de runbooktaak.</span><span class="sxs-lookup"><span data-stu-id="e7e01-160">While the **Microsoft-Automation** event log does not have many events with details assisting with the troubleshooting of runbook execution, you will at least find the results of the runbook job.</span></span>  

<span data-ttu-id="e7e01-161">[Runbook uitvoer en berichten](automation-runbook-output-and-messages.md) worden verzonden naar Azure Automation van hybrid workers net als runbooktaken uitvoeren in de cloud.</span><span class="sxs-lookup"><span data-stu-id="e7e01-161">[Runbook output and messages](automation-runbook-output-and-messages.md) are sent to Azure Automation from hybrid workers just like runbook jobs run in the cloud.</span></span>  <span data-ttu-id="e7e01-162">Ook kunt u de stromen uitgebreid en voortgang van de dezelfde manier als voor andere runbooks.</span><span class="sxs-lookup"><span data-stu-id="e7e01-162">You can also enable the Verbose and Progress streams the same way you would for other runbooks.</span></span>  

<span data-ttu-id="e7e01-163">Als uw runbooks zijn niet voltooid, waardoor de taak overzicht de status van toont **onderbroken**, lees het artikel over probleemoplossing [Hybrid Runbook Worker: een runbooktaak wordt beëindigd met de status onderbroken ](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span><span class="sxs-lookup"><span data-stu-id="e7e01-163">If your runbooks are not completing successfully and the job summary shows a status of **Suspended**, please review the troubleshooting article [Hybrid Runbook Worker: A runbook job terminates with a status of Suspended](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span></span>   

## <a name="next-steps"></a><span data-ttu-id="e7e01-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e7e01-164">Next steps</span></span>
* <span data-ttu-id="e7e01-165">Zie voor meer informatie over de verschillende methoden die kunnen worden gebruikt om een runbook te starten, [een Runbook starten in Azure Automation](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="e7e01-165">To learn more about the different methods that can be used to start a runbook, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>  
* <span data-ttu-id="e7e01-166">Zie voor informatie over de verschillende procedures voor het werken met PowerShell en PowerShell Workflow-runbooks in Azure Automation met behulp van de teksteditor, [bewerken van een Runbook in Azure Automation](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="e7e01-166">To understand the different procedures for working with PowerShell and PowerShell Workflow runbooks in Azure Automation using the textual editor, see [Editing a Runbook in Azure Automation](automation-edit-textual-runbook.md)</span></span>