---
title: Azure Automation integreren met broncodebeheer Visual Stuido Team Services | Microsoft Docs
description: Scenario begeleidt u bij het instellen van integratie met een Azure Automation-account en de bronbeheer Visual Stuido Team Services.
services: automation
documentationcenter: 
author: eamono
manager: 
editor: 
keywords: Azure powershell, VSTS, bronbeheer, automation
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.openlocfilehash: 01f9c01c9e04e02dbb548b68cf99684ba6ddd57e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a><span data-ttu-id="fd6d6-104">Azure Automation-scenario - integratie van broncodebeheer automatisering met Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="fd6d6-104">Azure Automation scenario - Automation source control integration with Visual Studio Team Services</span></span>

<span data-ttu-id="fd6d6-105">In dit scenario hebt u een project voor Visual Studio Team Services die u gebruikt voor het beheren van Azure Automation-runbooks of DSC-configuraties onder bronbeheer.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-105">In this scenario, you have a Visual Studio Team Services project that you are using to manage Azure Automation runbooks or DSC configurations under source control.</span></span>
<span data-ttu-id="fd6d6-106">In dit artikel wordt beschreven hoe VSTS integreren met uw Azure Automation-omgeving zodat continue integratie gebeurt voor elke controle in.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-106">This article describes how to integrate VSTS with your Azure Automation environment so that continuous integration happens for each check-in.</span></span>

## <a name="getting-the-scenario"></a><span data-ttu-id="fd6d6-107">Het scenario ophalen</span><span class="sxs-lookup"><span data-stu-id="fd6d6-107">Getting the scenario</span></span>

<span data-ttu-id="fd6d6-108">Dit scenario bestaat uit twee PowerShell-runbooks die u rechtstreeks vanuit importeren kunt de [Runbookgalerie](automation-runbook-gallery.md) in de Azure-portal of downloaden van de [PowerShell Gallery](https://www.powershellgallery.com).</span><span class="sxs-lookup"><span data-stu-id="fd6d6-108">This scenario consists of two PowerShell runbooks that you can import directly from the [Runbook Gallery](automation-runbook-gallery.md) in the Azure portal or download from the [PowerShell Gallery](https://www.powershellgallery.com).</span></span>

### <a name="runbooks"></a><span data-ttu-id="fd6d6-109">Runbooks</span><span class="sxs-lookup"><span data-stu-id="fd6d6-109">Runbooks</span></span>

<span data-ttu-id="fd6d6-110">Runbook</span><span class="sxs-lookup"><span data-stu-id="fd6d6-110">Runbook</span></span> | <span data-ttu-id="fd6d6-111">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="fd6d6-111">Description</span></span>| 
--------|------------|
<span data-ttu-id="fd6d6-112">Synchronisatie-VSTS</span><span class="sxs-lookup"><span data-stu-id="fd6d6-112">Sync-VSTS</span></span> | <span data-ttu-id="fd6d6-113">Importeren runbooks of configuraties van broncodebeheer VSTS als een check-in is voltooid.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-113">Import runbooks or configurations from VSTS source control when a check-in is done.</span></span> <span data-ttu-id="fd6d6-114">Als u handmatig uitvoert, wordt de importeren en publiceren van alle runbooks of -configuraties in het Automation-account.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-114">If run manually, it will import and publish all runbooks or configurations into the Automation account.</span></span>| 
<span data-ttu-id="fd6d6-115">Synchronisatie VSTSGit</span><span class="sxs-lookup"><span data-stu-id="fd6d6-115">Sync-VSTSGit</span></span> | <span data-ttu-id="fd6d6-116">Runbooks of configuraties uit importeren VSTS onder bronbeheer Git als een check-in is voltooid.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-116">Import runbooks or configurations from VSTS under Git source control when a check-in is done.</span></span> <span data-ttu-id="fd6d6-117">Als u handmatig uitvoert, wordt de importeren en publiceren van alle runbooks of -configuraties in het Automation-account.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-117">If run manually, it will import and publish all runbooks or configurations into the Automation account.</span></span>|

### <a name="variables"></a><span data-ttu-id="fd6d6-118">Variabelen</span><span class="sxs-lookup"><span data-stu-id="fd6d6-118">Variables</span></span>

<span data-ttu-id="fd6d6-119">Variabele</span><span class="sxs-lookup"><span data-stu-id="fd6d6-119">Variable</span></span> | <span data-ttu-id="fd6d6-120">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="fd6d6-120">Description</span></span>|
-----------|------------|
<span data-ttu-id="fd6d6-121">VSToken</span><span class="sxs-lookup"><span data-stu-id="fd6d6-121">VSToken</span></span> | <span data-ttu-id="fd6d6-122">Beveiligde variabelenactivum maakt u met de VSTS persoonlijke toegangstoken.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-122">Secure variable asset you will create that contains the VSTS personal access token.</span></span> <span data-ttu-id="fd6d6-123">U kunt informatie over het maken van een VSTS persoonlijke toegangstoken op de [VSTS verificatiepagina](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview).</span><span class="sxs-lookup"><span data-stu-id="fd6d6-123">You can learn how to create a VSTS personal access token on the [VSTS authentication page](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview).</span></span> 
## <a name="installing-and-configuring-this-scenario"></a><span data-ttu-id="fd6d6-124">Dit scenario installeren en configureren</span><span class="sxs-lookup"><span data-stu-id="fd6d6-124">Installing and configuring this scenario</span></span>

<span data-ttu-id="fd6d6-125">Maak een [persoonlijke toegangstoken](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) in VSTS die u gebruiken wilt voor het synchroniseren van de runbooks of -configuraties in uw automation-account.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-125">Create a [personal access token](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) in VSTS that you will use to sync the runbooks or configurations into your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

<span data-ttu-id="fd6d6-126">Maak een [beveiligde variabele](automation-variables.md) in uw automation-account voor het opslaan van het persoonlijke toegangstoken zodat het runbook kan worden geverifieerd met VSTS en synchroniseren van de runbooks of -configuraties in het Automation-account.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-126">Create a [secure variable](automation-variables.md) in your automation account to hold the personal access token so that the runbook can authenticate to VSTS and sync the runbooks or configurations into the Automation account.</span></span> <span data-ttu-id="fd6d6-127">U kunt deze VSToken naam.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-127">You can name this VSToken.</span></span> 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

<span data-ttu-id="fd6d6-128">Importeer het runbook dat uw runbooks of -configuraties in het automation-account wordt gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-128">Import the runbook that will sync your runbooks or configurations into the automation account.</span></span> <span data-ttu-id="fd6d6-129">U kunt de [VSTS voorbeeldrunbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) of de VSTS met Git voorbeeldrunbook (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) van de PowerShellGallery.com afhankelijk van of u verbinding met broncodebeheer VSTS of VSTS gebruiken met Git en implementeren voor uw automation-account.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-129">You can use the [VSTS sample runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) or the [VSTS with Git sample runbook] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) from the PowerShellGallery.com depending on if you use VSTS source control or VSTS with Git and deploy to your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

<span data-ttu-id="fd6d6-130">U kunt nu [publiceren](automation-creating-importing-runbook.md#publishing-a-runbook) dit runbook zodat u kunt een webhook maken.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-130">You can now [publish](automation-creating-importing-runbook.md#publishing-a-runbook) this runbook so you can create a webhook.</span></span> 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

<span data-ttu-id="fd6d6-131">Maak een [webhook](automation-webhooks.md) voor deze runbook-synchronisatie VSTS en vul de parameters zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-131">Create a [webhook](automation-webhooks.md) for this Sync-VSTS runbook and fill in the parameters as shown below.</span></span> <span data-ttu-id="fd6d6-132">Zorg ervoor dat u de webhook-url kopiëren als u deze nodig voor een service haakje in VSTS.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-132">Make sure you copy the webhook url as you will need it for a service hook in VSTS.</span></span> <span data-ttu-id="fd6d6-133">De VSAccessTokenVariableName is de naam (VSToken) van de beveiligde variabele die u eerder hebt gemaakt voor het persoonlijke toegangstoken houdt.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-133">The VSAccessTokenVariableName is the name (VSToken) of the secure variable that you created earlier to hold the personal access token.</span></span> 

<span data-ttu-id="fd6d6-134">Integratie met VSTS (Sync-VSTS.ps1), gaat de volgende parameters.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-134">Integrating with VSTS (Sync-VSTS.ps1) will take the following parameters.</span></span>
### <a name="sync-vsts-parameters"></a><span data-ttu-id="fd6d6-135">Synchronisatie-VSTS Parameters</span><span class="sxs-lookup"><span data-stu-id="fd6d6-135">Sync-VSTS Parameters</span></span>

<span data-ttu-id="fd6d6-136">Parameter</span><span class="sxs-lookup"><span data-stu-id="fd6d6-136">Parameter</span></span> | <span data-ttu-id="fd6d6-137">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="fd6d6-137">Description</span></span>| 
--------|------------|
<span data-ttu-id="fd6d6-138">WebhookData</span><span class="sxs-lookup"><span data-stu-id="fd6d6-138">WebhookData</span></span> | <span data-ttu-id="fd6d6-139">Hiermee wordt het inchecken-informatie verzonden van de service VSTS hook bevatten.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-139">This will contain the checkin information sent from the VSTS service hook.</span></span> <span data-ttu-id="fd6d6-140">U moet deze parameter leeg laten.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-140">You should leave this parameter blank.</span></span>| 
<span data-ttu-id="fd6d6-141">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fd6d6-141">ResourceGroup</span></span> | <span data-ttu-id="fd6d6-142">Dit is de naam van de resourcegroep die het automation-account in.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-142">This is the name of the resource group that the automation account is in.</span></span>|
<span data-ttu-id="fd6d6-143">AutomationAccountName</span><span class="sxs-lookup"><span data-stu-id="fd6d6-143">AutomationAccountName</span></span> | <span data-ttu-id="fd6d6-144">De naam van het automation-account met VSTS moeten worden gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-144">The name of the automation account that will sync with VSTS.</span></span>|
<span data-ttu-id="fd6d6-145">VSFolder</span><span class="sxs-lookup"><span data-stu-id="fd6d6-145">VSFolder</span></span> | <span data-ttu-id="fd6d6-146">De naam van de map in VSTS waar de runbooks en configuraties bestaan.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-146">The name of the folder in VSTS where the runbooks and configurations exist.</span></span>|
<span data-ttu-id="fd6d6-147">VSAccount</span><span class="sxs-lookup"><span data-stu-id="fd6d6-147">VSAccount</span></span> | <span data-ttu-id="fd6d6-148">De naam van de Visual Studio Team Services-account.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-148">The name of the Visual Studio Team Services account.</span></span>| 
<span data-ttu-id="fd6d6-149">VSAccessTokenVariableName</span><span class="sxs-lookup"><span data-stu-id="fd6d6-149">VSAccessTokenVariableName</span></span> | <span data-ttu-id="fd6d6-150">De naam van de beveiligde variabele (VSToken) die het VSTS persoonlijke toegangstoken bevat.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-150">The name of the secure variable (VSToken) that holds the VSTS personal access token.</span></span>| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

<span data-ttu-id="fd6d6-151">Als u van VSTS met GIT (Sync-VSTSGit.ps1 gebruikmaakt) wordt uitgevoerd, de volgende parameters.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-151">If you are using VSTS with GIT (Sync-VSTSGit.ps1) it will take the following parameters.</span></span>

<span data-ttu-id="fd6d6-152">Parameter</span><span class="sxs-lookup"><span data-stu-id="fd6d6-152">Parameter</span></span> | <span data-ttu-id="fd6d6-153">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="fd6d6-153">Description</span></span>|
--------|------------|
<span data-ttu-id="fd6d6-154">WebhookData</span><span class="sxs-lookup"><span data-stu-id="fd6d6-154">WebhookData</span></span> | <span data-ttu-id="fd6d6-155">Hiermee wordt het inchecken-informatie verzonden van de service VSTS hook bevatten.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-155">This will contain the checkin information sent from the VSTS service hook.</span></span> <span data-ttu-id="fd6d6-156">U moet deze parameter leeg laten.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-156">You should leave this parameter blank.</span></span>| <span data-ttu-id="fd6d6-157">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fd6d6-157">ResourceGroup</span></span> | <span data-ttu-id="fd6d6-158">Deze de naam van de resourcegroep die het automation-account in.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-158">This the name of the resource group that the automation account is in.</span></span>|
<span data-ttu-id="fd6d6-159">AutomationAccountName</span><span class="sxs-lookup"><span data-stu-id="fd6d6-159">AutomationAccountName</span></span> | <span data-ttu-id="fd6d6-160">De naam van het automation-account met VSTS moeten worden gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-160">The name of the automation account that will sync with VSTS.</span></span>|
<span data-ttu-id="fd6d6-161">VSAccount</span><span class="sxs-lookup"><span data-stu-id="fd6d6-161">VSAccount</span></span> | <span data-ttu-id="fd6d6-162">De naam van de Visual Studio Team Services-account.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-162">The name of the Visual Studio Team Services account.</span></span>|
<span data-ttu-id="fd6d6-163">VSProject</span><span class="sxs-lookup"><span data-stu-id="fd6d6-163">VSProject</span></span> | <span data-ttu-id="fd6d6-164">De naam van het project in VSTS waar de runbooks en configuraties bestaan.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-164">The name of the project in VSTS where the runbooks and configurations exist.</span></span>|
<span data-ttu-id="fd6d6-165">GitRepo</span><span class="sxs-lookup"><span data-stu-id="fd6d6-165">GitRepo</span></span> | <span data-ttu-id="fd6d6-166">De naam van de Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-166">The name of the Git repository.</span></span>|
<span data-ttu-id="fd6d6-167">GitBranch</span><span class="sxs-lookup"><span data-stu-id="fd6d6-167">GitBranch</span></span> | <span data-ttu-id="fd6d6-168">De naam van de vertakking in VSTS Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-168">The name of the branch in VSTS Git repository.</span></span>|
<span data-ttu-id="fd6d6-169">Map</span><span class="sxs-lookup"><span data-stu-id="fd6d6-169">Folder</span></span> | <span data-ttu-id="fd6d6-170">De naam van de map in VSTS Git vertakking.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-170">The name of the folder in VSTS Git branch.</span></span>|
<span data-ttu-id="fd6d6-171">VSAccessTokenVariableName</span><span class="sxs-lookup"><span data-stu-id="fd6d6-171">VSAccessTokenVariableName</span></span> | <span data-ttu-id="fd6d6-172">De naam van de beveiligde variabele (VSToken) die het VSTS persoonlijke toegangstoken bevat.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-172">The name of the secure variable (VSToken) that holds the VSTS personal access token.</span></span>|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

<span data-ttu-id="fd6d6-173">Maak een haakje service in VSTS voor controle-modules naar de map die deze webhook bij code controle wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-173">Create a service hook in VSTS for check-ins to the folder that triggers this webhook on code check-in.</span></span> <span data-ttu-id="fd6d6-174">Selecteer Web Hiermee als de service om te integreren met wanneer u een nieuw abonnement maakt.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-174">Select Web Hooks as the service to integrate with when you create a new subscription.</span></span> <span data-ttu-id="fd6d6-175">Voor meer informatie over service hooks op [VSTS Service Hooks documentatie](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).</span><span class="sxs-lookup"><span data-stu-id="fd6d6-175">You can learn more about service hooks on [VSTS Service Hooks documentation](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).</span></span>
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

<span data-ttu-id="fd6d6-176">Nu moet u kunnen alle controle-modules van uw runbooks en de configuraties in VSTS doen en moet deze automatisch synchroniseren 'd in uw automation-account.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-176">You should now be able to do all check-ins of your runbooks and configurations into VSTS and have these automatically sync’d into your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

<span data-ttu-id="fd6d6-177">Als u dit runbook handmatig uitvoert zonder wordt geactiveerd door VSTS, kunt u de parameter webhookdata leeg laten en doet een volledige synchronisatie van de map VSTS die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-177">If you run this runbook manually without being triggered by VSTS, you can leave the webhookdata parameter empty and it will do a full sync from the VSTS folder specified.</span></span>

<span data-ttu-id="fd6d6-178">Als u wilt verwijderen van het scenario, verwijdert u de service hook uit VSTS, verwijdert u het runbook en de variabele VSToken.</span><span class="sxs-lookup"><span data-stu-id="fd6d6-178">If you wish to uninstall the scenario, remove the service hook from VSTS, delete the runbook, and the VSToken variable.</span></span>
