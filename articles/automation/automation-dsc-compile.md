---
title: aaaCompiling configuraties in Azure Automation DSC | Microsoft Docs
description: Dit artikel wordt beschreven hoe toocompile Desired State Configuration (DSC) configuraties voor Azure Automation.
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
ms.assetid: 49f20b31-4fa5-4712-b1c7-8f4409f1aecc
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 02/07/2017
ms.author: magoedte; eslesar
ms.openlocfilehash: b195311318a2d7431c4d6b29f4b9a5f3a0a0a9a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a><span data-ttu-id="38b3d-103">Compileren van configuraties in Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="38b3d-103">Compiling configurations in Azure Automation DSC</span></span>

<span data-ttu-id="38b3d-104">U kunt configuraties Desired State Configuration (DSC) op twee manieren met Azure Automation compileren: in hello Azure-portal en met Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="38b3d-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation: in hello Azure portal, and with Windows PowerShell.</span></span> <span data-ttu-id="38b3d-105">Hallo onderstaande tabel kunt u bepalen wanneer toouse welke methode op basis van kenmerken van elk Hallo:</span><span class="sxs-lookup"><span data-stu-id="38b3d-105">hello following table will help you determine when toouse which method based on hello characteristics of each:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="38b3d-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="38b3d-106">Azure portal</span></span>

* <span data-ttu-id="38b3d-107">Eenvoudigste methode met interactieve gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="38b3d-107">Simplest method with interactive user interface</span></span>
* <span data-ttu-id="38b3d-108">Formulier tooprovide eenvoudige parameterwaarden</span><span class="sxs-lookup"><span data-stu-id="38b3d-108">Form tooprovide simple parameter values</span></span>
* <span data-ttu-id="38b3d-109">Eenvoudig bijhouden taakstatus</span><span class="sxs-lookup"><span data-stu-id="38b3d-109">Easily track job state</span></span>
* <span data-ttu-id="38b3d-110">Toegang met aanmelding bij Azure is geverifieerd</span><span class="sxs-lookup"><span data-stu-id="38b3d-110">Access authenticated with Azure logon</span></span>

### <a name="windows-powershell"></a><span data-ttu-id="38b3d-111">Windows Powershell</span><span class="sxs-lookup"><span data-stu-id="38b3d-111">Windows PowerShell</span></span>

* <span data-ttu-id="38b3d-112">Aanroepen vanuit de opdrachtregel met Windows PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="38b3d-112">Call from command line with Windows PowerShell cmdlets</span></span>
* <span data-ttu-id="38b3d-113">Kan worden opgenomen in een geautomatiseerde oplossing met meerdere stappen</span><span class="sxs-lookup"><span data-stu-id="38b3d-113">Can be included in automated solution with multiple steps</span></span>
* <span data-ttu-id="38b3d-114">Eenvoudige en complexe parameterwaarden opgeven</span><span class="sxs-lookup"><span data-stu-id="38b3d-114">Provide simple and complex parameter values</span></span>
* <span data-ttu-id="38b3d-115">Taakstatus bijhouden</span><span class="sxs-lookup"><span data-stu-id="38b3d-115">Track job state</span></span>
* <span data-ttu-id="38b3d-116">Client vereist toosupport PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="38b3d-116">Client required toosupport PowerShell cmdlets</span></span>
* <span data-ttu-id="38b3d-117">ConfigurationData doorgeven</span><span class="sxs-lookup"><span data-stu-id="38b3d-117">Pass ConfigurationData</span></span>
* <span data-ttu-id="38b3d-118">Configuraties die gebruikmaken van referenties compileren</span><span class="sxs-lookup"><span data-stu-id="38b3d-118">Compile configurations that use credentials</span></span>

<span data-ttu-id="38b3d-119">Zodra u hebt besloten een compilatie-methode, kunt u onderstaande toostart compileren respectieve procedures Hallo volgen.</span><span class="sxs-lookup"><span data-stu-id="38b3d-119">Once you have decided on a compilation method, you can follow hello respective procedures below toostart compiling.</span></span>

## <a name="compiling-a-dsc-configuration-with-hello-azure-portal"></a><span data-ttu-id="38b3d-120">Compileren van een DSC-configuratie met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="38b3d-120">Compiling a DSC Configuration with hello Azure portal</span></span>

1. <span data-ttu-id="38b3d-121">Van uw Automation-account, klikt u op **DSC-configuraties**.</span><span class="sxs-lookup"><span data-stu-id="38b3d-121">From your Automation account, click **DSC Configurations**.</span></span>
2. <span data-ttu-id="38b3d-122">Klik op een tooopen configuratie van de blade.</span><span class="sxs-lookup"><span data-stu-id="38b3d-122">Click a configuration tooopen its blade.</span></span>
3. <span data-ttu-id="38b3d-123">Klik op **compileren**.</span><span class="sxs-lookup"><span data-stu-id="38b3d-123">Click **Compile**.</span></span>
4. <span data-ttu-id="38b3d-124">Als het Hallo-configuratie geen parameters heeft, worden na vragen aan gebruiker tooconfirm of u toocompile wilt deze.</span><span class="sxs-lookup"><span data-stu-id="38b3d-124">If hello configuration has no parameters, you will be prompted tooconfirm whether you want toocompile it.</span></span> <span data-ttu-id="38b3d-125">Als Hallo configuratie parameters heeft, Hallo **configuratie compileren** blade geopend zodat u parameterwaarden kan opgeven.</span><span class="sxs-lookup"><span data-stu-id="38b3d-125">If hello configuration has parameters, hello **Compile Configuration** blade will open so you can provide parameter values.</span></span> <span data-ttu-id="38b3d-126">Zie Hallo [ **fundamentele Parameters** ](#basic-parameters) sectie hieronder voor meer informatie over parameters.</span><span class="sxs-lookup"><span data-stu-id="38b3d-126">See hello [**Basic Parameters**](#basic-parameters) section below for further details on parameters.</span></span>
5. <span data-ttu-id="38b3d-127">Hallo **Compilatietaak** blade wordt geopend zodat u de status van taak Hallo-compilatie volgen kunt en hello knooppuntconfiguraties (MOF configuratiedocumenten) het veroorzaakt toobe op Hallo Azure Automation DSC-Pull-Server geplaatst.</span><span class="sxs-lookup"><span data-stu-id="38b3d-127">hello **Compilation Job** blade is opened so that you can track hello compilation job's status, and hello node configurations (MOF configuration documents) it caused toobe placed on hello Azure Automation DSC Pull Server.</span></span>

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a><span data-ttu-id="38b3d-128">Compileren van een DSC-configuratie met Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="38b3d-128">Compiling a DSC Configuration with Windows PowerShell</span></span>

<span data-ttu-id="38b3d-129">U kunt [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart compileren met Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="38b3d-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart compiling with Windows PowerShell.</span></span> <span data-ttu-id="38b3d-130">Hallo volgende voorbeeldcode wordt gestart compilatie van een DSC-configuratie aangeroepen **SampleConfig**.</span><span class="sxs-lookup"><span data-stu-id="38b3d-130">hello following sample code starts compilation of a DSC configuration called **SampleConfig**.</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

<span data-ttu-id="38b3d-131">`Start-AzureRmAutomationDscCompilationJob`retourneert een compilatie taak object waarmee u tootrack de status ervan kunt.</span><span class="sxs-lookup"><span data-stu-id="38b3d-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use tootrack its status.</span></span> <span data-ttu-id="38b3d-132">U kunt dit object compilatie met [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine Hallo status van Hallo-Compilatietaak en [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview de streams (uitvoer).</span><span class="sxs-lookup"><span data-stu-id="38b3d-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine hello status of hello compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview its streams (output).</span></span> <span data-ttu-id="38b3d-133">Hallo volgende voorbeeldcode wordt gestart compilatie van Hallo **SampleConfig** configuratie, wacht totdat deze is voltooid en wordt vervolgens de stromen.</span><span class="sxs-lookup"><span data-stu-id="38b3d-133">hello following sample code starts compilation of hello **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span></span>

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a><span data-ttu-id="38b3d-134">Basic-Parameters</span><span class="sxs-lookup"><span data-stu-id="38b3d-134">Basic Parameters</span></span>
<span data-ttu-id="38b3d-135">Parameterdeclaratie in DSC-configuraties, inclusief parametertypen en eigenschappen werkt Hallo hetzelfde als in Azure Automation-runbooks.</span><span class="sxs-lookup"><span data-stu-id="38b3d-135">Parameter declaration in DSC configurations, including parameter types and properties, works hello same as in Azure Automation runbooks.</span></span> <span data-ttu-id="38b3d-136">Zie [een runbook starten in Azure Automation](automation-starting-a-runbook.md) toolearn meer informatie over runbook-parameters.</span><span class="sxs-lookup"><span data-stu-id="38b3d-136">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) toolearn more about runbook parameters.</span></span>

<span data-ttu-id="38b3d-137">Hallo volgende voorbeeld worden twee parameters aangeroepen **FeatureName** en **IsPresent**, toodetermine Hallo waarden van eigenschappen in Hallo **ParametersExample.sample** knooppunt configuratie gegenereerd tijdens de compilatie.</span><span class="sxs-lookup"><span data-stu-id="38b3d-137">hello following example uses two parameters called **FeatureName** and **IsPresent**, toodetermine hello values of properties in hello **ParametersExample.sample** node configuration, generated during compilation.</span></span>

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]

        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = "Present"
    if($IsPresent -eq $false)
    {
        $EnsureString = "Absent"
    }

    Node "sample"
    {
        WindowsFeature ($FeatureName + "Feature")
        {
            Ensure = $EnsureString
            Name = $FeatureName
        }
    }
}
```

<span data-ttu-id="38b3d-138">U kunt compileren DSC-configuraties die gebruikmaken van eenvoudige parameters in hello Azure Automation DSC-portal of met Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="38b3d-138">You can compile DSC Configurations that use basic parameters in hello Azure Automation DSC portal, or with Azure PowerShell:</span></span>

### <a name="portal"></a><span data-ttu-id="38b3d-139">Portal</span><span class="sxs-lookup"><span data-stu-id="38b3d-139">Portal</span></span>

<span data-ttu-id="38b3d-140">In Hallo-portal, kunt u parameterwaarden opgeven wanneer u op **compileren**.</span><span class="sxs-lookup"><span data-stu-id="38b3d-140">In hello portal, you can enter parameter values after clicking **Compile**.</span></span>

![alternatieve tekst](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a><span data-ttu-id="38b3d-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="38b3d-142">PowerShell</span></span>

<span data-ttu-id="38b3d-143">PowerShell-parameters in vereist een [hashtabel](http://technet.microsoft.com/library/hh847780.aspx) Hallo-sleutel komt overeen met de parameternaam Hallo waarbij Hallo-waarde is gelijk aan Hallo parameterwaarde.</span><span class="sxs-lookup"><span data-stu-id="38b3d-143">PowerShell requires parameters in a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where hello key matches hello parameter name, and hello value equals hello parameter value.</span></span>

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

<span data-ttu-id="38b3d-144">Zie voor meer informatie over PSCredentials doorgeeft als parameters <a href="#credential-assets"> **Referentieassets** </a> hieronder.</span><span class="sxs-lookup"><span data-stu-id="38b3d-144">For information about passing PSCredentials as parameters, see <a href="#credential-assets">**Credential Assets**</a> below.</span></span>

## <a name="configurationdata"></a><span data-ttu-id="38b3d-145">ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="38b3d-145">ConfigurationData</span></span>
<span data-ttu-id="38b3d-146">**ConfigurationData** kunt u tooseparate structurele configuratie uit een specifieke configuratie van de omgeving tijdens het gebruik van PowerShell DSC.</span><span class="sxs-lookup"><span data-stu-id="38b3d-146">**ConfigurationData** allows you tooseparate structural configuration from any environment specific configuration while using PowerShell DSC.</span></span> <span data-ttu-id="38b3d-147">Zie [scheiden 'Wat' op 'Waar' in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn meer informatie over **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="38b3d-147">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn more about **ConfigurationData**.</span></span>

> [!NOTE]
> <span data-ttu-id="38b3d-148">U kunt **ConfigurationData** bij het compileren van in Azure Automation DSC met Azure PowerShell, maar niet in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="38b3d-148">You can use **ConfigurationData** when compiling in Azure Automation DSC using Azure PowerShell, but not in hello Azure portal.</span></span>

<span data-ttu-id="38b3d-149">Hallo volgende DSC-voorbeeldconfiguratie gebruikt **ConfigurationData** via Hallo **$ConfigurationData** en **$AllNodes** trefwoorden.</span><span class="sxs-lookup"><span data-stu-id="38b3d-149">hello following example DSC configuration uses **ConfigurationData** via hello **$ConfigurationData** and **$AllNodes** keywords.</span></span> <span data-ttu-id="38b3d-150">U moet ook Hallo [ **xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) voor dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="38b3d-150">You'll also need hello [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span></span>

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure   = "Present"
        }
    }
}
```

<span data-ttu-id="38b3d-151">U kunt compileren Hallo DSC-configuratie hierboven met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="38b3d-151">You can compile hello DSC configuration above with PowerShell.</span></span> <span data-ttu-id="38b3d-152">Hallo onderstaande PowerShell voegt twee knooppunt configuraties toohello Azure Automation DSC-Pull-Server: **ConfigurationDataSample.MyVM1** en **ConfigurationDataSample.MyVM3**:</span><span class="sxs-lookup"><span data-stu-id="38b3d-152">hello below PowerShell adds two node configurations toohello Azure Automation DSC Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "MyVM1"
            Role = "WebServer"
        },
        @{
            NodeName = "MyVM2"
            Role = "SQLServer"
        },
        @{
            NodeName = "MyVM3"
            Role = "WebServer"
        }
    )

    NonNodeData = @{
        SomeMessage = "I love Azure Automation DSC!"
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ConfigurationDataSample" -ConfigurationData $ConfigData
```

## <a name="assets"></a><span data-ttu-id="38b3d-153">Assets</span><span class="sxs-lookup"><span data-stu-id="38b3d-153">Assets</span></span>

<span data-ttu-id="38b3d-154">Asset-verwijzingen zijn hetzelfde in Azure Automation DSC-configuraties en runbooks Hallo.</span><span class="sxs-lookup"><span data-stu-id="38b3d-154">Asset references are hello same in Azure Automation DSC configurations and runbooks.</span></span> <span data-ttu-id="38b3d-155">Zie de volgende Hallo voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="38b3d-155">See hello following for more information:</span></span>

* [<span data-ttu-id="38b3d-156">Certificaten</span><span class="sxs-lookup"><span data-stu-id="38b3d-156">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="38b3d-157">Verbindingen</span><span class="sxs-lookup"><span data-stu-id="38b3d-157">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="38b3d-158">Referenties</span><span class="sxs-lookup"><span data-stu-id="38b3d-158">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="38b3d-159">Variabelen</span><span class="sxs-lookup"><span data-stu-id="38b3d-159">Variables</span></span>](automation-variables.md)

### <a name="credential-assets"></a><span data-ttu-id="38b3d-160">Referentieassets</span><span class="sxs-lookup"><span data-stu-id="38b3d-160">Credential Assets</span></span>

<span data-ttu-id="38b3d-161">Terwijl in Azure Automation DSC-configuraties kunnen verwijzen naar referentieassets met **Get-AzureRmAutomationCredential**, referentieassets kunnen ook worden doorgegeven via parameters, indien gewenst.</span><span class="sxs-lookup"><span data-stu-id="38b3d-161">While DSC configurations in Azure Automation can reference credential assets using **Get-AzureRmAutomationCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="38b3d-162">Als een parameter van het duurt een configuratie voordat **PSCredential** typt, moet u toopass Hallo-naam van een Azure Automation-referentieasset als waarde van de parameter in plaats van een PSCredential-object.</span><span class="sxs-lookup"><span data-stu-id="38b3d-162">If a configuration takes a parameter of **PSCredential** type, then you need toopass hello string name of an Azure Automation credential asset as that parameter’s value, rather than a PSCredential object.</span></span> <span data-ttu-id="38b3d-163">Achter de schermen hello, wordt hello Azure Automation-referentieasset met die naam opgehaald en doorgegeven toohello configuratie.</span><span class="sxs-lookup"><span data-stu-id="38b3d-163">Behind hello scenes, hello Azure Automation credential asset with that name will be retrieved and passed toohello configuration.</span></span>

<span data-ttu-id="38b3d-164">Referenties houden vereist beveiligd in knooppuntconfiguraties (MOF configuratiedocumenten) versleutelen Hallo-referenties in Hallo knooppunt configuratie MOF-bestand.</span><span class="sxs-lookup"><span data-stu-id="38b3d-164">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting hello credentials in hello node configuration MOF file.</span></span> <span data-ttu-id="38b3d-165">Azure Automation wordt hierbij nog een stapje verder en versleutelt Hallo volledige MOF-bestand.</span><span class="sxs-lookup"><span data-stu-id="38b3d-165">Azure Automation takes this one step further and encrypts hello entire MOF file.</span></span> <span data-ttu-id="38b3d-166">Echter, momenteel u moet de hoogte PowerShell DSC dit klopt voor referenties toobe output als tekst zonder opmaak tijdens het genereren van het knooppunt configuratie MOF omdat PowerShell DSC niet weet dat Azure Automation Hallo volledige MOF-bestand na wordt versleutelen de het genereren via een Compilatietaak.</span><span class="sxs-lookup"><span data-stu-id="38b3d-166">However, currently you must tell PowerShell DSC it is okay for credentials toobe outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting hello entire MOF file after its generation via a compilation job.</span></span>

<span data-ttu-id="38b3d-167">U kunt PowerShell DSC zien of dit voor referenties toobe output in tekst zonder opmaak in Hallo gegenereerd knooppuntconfiguratie MOF-bestanden klopt met [ **ConfigurationData**](#configurationdata).</span><span class="sxs-lookup"><span data-stu-id="38b3d-167">You can tell PowerShell DSC that it is okay for credentials toobe outputted in plain text in hello generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span></span> <span data-ttu-id="38b3d-168">U moet doorgeven `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** voor elk knooppunt-blok-naam die wordt weergegeven in Hallo DSC-configuratie en de referenties worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="38b3d-168">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in hello DSC configuration and uses credentials.</span></span>

<span data-ttu-id="38b3d-169">Hallo volgende voorbeeld ziet u een DSC-configuratie die gebruikmaakt van een Automation-referentieasset.</span><span class="sxs-lookup"><span data-stu-id="38b3d-169">hello following example shows a DSC configuration that uses an Automation credential asset.</span></span>

```powershell
Configuration CredentialSample
{
    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -AutomationAccountName "AutomationAcct" -Name "SomeCredentialAsset"

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $Cred
        }
    }
}
```

<span data-ttu-id="38b3d-170">U kunt compileren Hallo DSC-configuratie hierboven met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="38b3d-170">You can compile hello DSC configuration above with PowerShell.</span></span> <span data-ttu-id="38b3d-171">Hallo onderstaande PowerShell voegt twee knooppunt configuraties toohello Azure Automation DSC-Pull-Server: **CredentialSample.MyVM1** en **CredentialSample.MyVM2**.</span><span class="sxs-lookup"><span data-stu-id="38b3d-171">hello below PowerShell adds two node configurations toohello Azure Automation DSC Pull Server:  **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "*"
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = "MyVM1"
        },
        @{
            NodeName = "MyVM2"
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "CredentialSample" -ConfigurationData $ConfigData
```

## <a name="importing-node-configurations"></a><span data-ttu-id="38b3d-172">Knooppuntconfiguraties importeren</span><span class="sxs-lookup"><span data-stu-id="38b3d-172">Importing node configurations</span></span>

<span data-ttu-id="38b3d-173">U kunt ook knooppunt configuratons (MOF-bestanden) die u hebt gecompileerd buiten Azure importeren.</span><span class="sxs-lookup"><span data-stu-id="38b3d-173">You can also import node configuratons (MOFs) that you have compiled outside of Azure.</span></span> <span data-ttu-id="38b3d-174">Een voordeel hiervan is dat confiturations knooppunt kan worden ondertekend.</span><span class="sxs-lookup"><span data-stu-id="38b3d-174">One advantage of this is that node confiturations can be signed.</span></span>
<span data-ttu-id="38b3d-175">Een ondertekende knooppuntconfiguratie is lokaal op een beheerde knooppunt gecontroleerd door Hallo DSC-agent, waarbij u ervoor zorgt dat Hallo toegepaste toohello knooppunt wordt de configuratie van een gemachtigde bron afkomstig is.</span><span class="sxs-lookup"><span data-stu-id="38b3d-175">A signed node configuration is verified locally on a managed node by hello DSC agent, ensuring that hello configuration being applied toohello node comes from an authorized source.</span></span>

> [!NOTE]
> <span data-ttu-id="38b3d-176">U kunt importeren gebruiken configuraties in uw Azure Automation-account is ondertekend, maar Azure Automation biedt momenteel geen ondersteuning voor het compileren van ondertekende configuraties.</span><span class="sxs-lookup"><span data-stu-id="38b3d-176">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span></span>

> [!NOTE]
> <span data-ttu-id="38b3d-177">Een configuratiebestand knooppunt is mag niet groter zijn dan 1 MB tooallow het toobe geïmporteerd in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="38b3d-177">A node configuration file must be no larger than 1 MB tooallow it toobe imported into Azure Automation.</span></span>

<span data-ttu-id="38b3d-178">U leert hoe toosign knooppuntconfiguraties op https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span><span class="sxs-lookup"><span data-stu-id="38b3d-178">You can learn how toosign node configurations at https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span></span>

### <a name="importing-a-node-configuration-in-hello-azure-portal"></a><span data-ttu-id="38b3d-179">Importeren van de knooppuntconfiguratie van een in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="38b3d-179">Importing a node configuration in hello Azure portal</span></span>

1. <span data-ttu-id="38b3d-180">Van uw Automation-account, klikt u op **DSC-knooppuntconfiguraties**.</span><span class="sxs-lookup"><span data-stu-id="38b3d-180">From your Automation account, click **DSC node configurations**.</span></span>

    ![DSC-knooppuntconfiguraties](./media/automation-dsc-compile/node-config.png)
2. <span data-ttu-id="38b3d-182">In Hallo **DSC-knooppuntconfiguraties** blade, klikt u op **toevoegen van een NodeConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="38b3d-182">In hello **DSC node configurations** blade, click **Add a NodeConfiguration**.</span></span>
3. <span data-ttu-id="38b3d-183">In Hallo **importeren** blade, klikt u op Hallo map pictogram volgende toohello **configuratiebestand knooppunt** textbox toobrowse voor een knooppunt-configuratiebestand (MOF) op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="38b3d-183">In hello **Import** blade, click hello folder icon next toohello **Node Configuration File** textbox toobrowse for a node configuration file (MOF) on your local computer.</span></span>

    ![Zoeken naar een lokaal bestand](./media/automation-dsc-compile/import-browse.png)
4. <span data-ttu-id="38b3d-185">Voer een naam in Hallo **configuratienaam** textbox.</span><span class="sxs-lookup"><span data-stu-id="38b3d-185">Enter a name in hello **Configuration Name** textbox.</span></span> <span data-ttu-id="38b3d-186">Deze naam moet overeenkomen met de naam van de Hallo van Hallo-configuratie waaruit Hallo knooppuntconfiguratie is gecompileerd.</span><span class="sxs-lookup"><span data-stu-id="38b3d-186">This name must match hello name of hello configuration from which hello node configuration was compiled.</span></span>
5. <span data-ttu-id="38b3d-187">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="38b3d-187">Click **OK**.</span></span>

### <a name="importing-a-node-configuration-with-powershell"></a><span data-ttu-id="38b3d-188">Importeren van de configuratie van een knooppunt met PowerShell</span><span class="sxs-lookup"><span data-stu-id="38b3d-188">Importing a node configuration with PowerShell</span></span>

<span data-ttu-id="38b3d-189">U kunt Hallo [importeren AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport een knooppuntconfiguratie in uw automation-account.</span><span class="sxs-lookup"><span data-stu-id="38b3d-189">You can use hello [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport a node configuration into your automation account.</span></span>

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



