---
title: Compileren van configuraties in Azure Automation DSC | Microsoft Docs
description: In dit artikel wordt beschreven hoe Desired State Configuration (DSC)-configuraties voor Azure Automation worden gecompileerd.
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
ms.openlocfilehash: 1aadd604e676659475f00760af3b0bdfb13a4792
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a><span data-ttu-id="33013-103">Compileren van configuraties in Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="33013-103">Compiling configurations in Azure Automation DSC</span></span>

<span data-ttu-id="33013-104">U kunt configuraties Desired State Configuration (DSC) op twee manieren met Azure Automation compileren: in de Azure-portal en met Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33013-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation: in the Azure portal, and with Windows PowerShell.</span></span> <span data-ttu-id="33013-105">De volgende tabel kunt u bepalen wanneer de methode die op basis van de kenmerken van elk gebruiken:</span><span class="sxs-lookup"><span data-stu-id="33013-105">The following table will help you determine when to use which method based on the characteristics of each:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="33013-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="33013-106">Azure portal</span></span>

* <span data-ttu-id="33013-107">Eenvoudigste methode met interactieve gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="33013-107">Simplest method with interactive user interface</span></span>
* <span data-ttu-id="33013-108">Formulier eenvoudige parameterwaarden opgeven</span><span class="sxs-lookup"><span data-stu-id="33013-108">Form to provide simple parameter values</span></span>
* <span data-ttu-id="33013-109">Eenvoudig bijhouden taakstatus</span><span class="sxs-lookup"><span data-stu-id="33013-109">Easily track job state</span></span>
* <span data-ttu-id="33013-110">Toegang met aanmelding bij Azure is geverifieerd</span><span class="sxs-lookup"><span data-stu-id="33013-110">Access authenticated with Azure logon</span></span>

### <a name="windows-powershell"></a><span data-ttu-id="33013-111">Windows Powershell</span><span class="sxs-lookup"><span data-stu-id="33013-111">Windows PowerShell</span></span>

* <span data-ttu-id="33013-112">Aanroepen vanuit de opdrachtregel met Windows PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="33013-112">Call from command line with Windows PowerShell cmdlets</span></span>
* <span data-ttu-id="33013-113">Kan worden opgenomen in een geautomatiseerde oplossing met meerdere stappen</span><span class="sxs-lookup"><span data-stu-id="33013-113">Can be included in automated solution with multiple steps</span></span>
* <span data-ttu-id="33013-114">Eenvoudige en complexe parameterwaarden opgeven</span><span class="sxs-lookup"><span data-stu-id="33013-114">Provide simple and complex parameter values</span></span>
* <span data-ttu-id="33013-115">Taakstatus bijhouden</span><span class="sxs-lookup"><span data-stu-id="33013-115">Track job state</span></span>
* <span data-ttu-id="33013-116">Client vereist ter ondersteuning van PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="33013-116">Client required to support PowerShell cmdlets</span></span>
* <span data-ttu-id="33013-117">ConfigurationData doorgeven</span><span class="sxs-lookup"><span data-stu-id="33013-117">Pass ConfigurationData</span></span>
* <span data-ttu-id="33013-118">Configuraties die gebruikmaken van referenties compileren</span><span class="sxs-lookup"><span data-stu-id="33013-118">Compile configurations that use credentials</span></span>

<span data-ttu-id="33013-119">Nadat u hebt besloten een compilatie-methode, kunt u de desbetreffende procedures hieronder om te beginnen met het compileren van volgen.</span><span class="sxs-lookup"><span data-stu-id="33013-119">Once you have decided on a compilation method, you can follow the respective procedures below to start compiling.</span></span>

## <a name="compiling-a-dsc-configuration-with-the-azure-portal"></a><span data-ttu-id="33013-120">Compileren van een DSC-configuratie met de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="33013-120">Compiling a DSC Configuration with the Azure portal</span></span>

1. <span data-ttu-id="33013-121">Van uw Automation-account, klikt u op **DSC-configuraties**.</span><span class="sxs-lookup"><span data-stu-id="33013-121">From your Automation account, click **DSC Configurations**.</span></span>
2. <span data-ttu-id="33013-122">Klik op een configuratie om de blade te openen.</span><span class="sxs-lookup"><span data-stu-id="33013-122">Click a configuration to open its blade.</span></span>
3. <span data-ttu-id="33013-123">Klik op **compileren**.</span><span class="sxs-lookup"><span data-stu-id="33013-123">Click **Compile**.</span></span>
4. <span data-ttu-id="33013-124">Als de configuratie geen parameters heeft, wordt u gevraagd om te bevestigen of u wilt compileren.</span><span class="sxs-lookup"><span data-stu-id="33013-124">If the configuration has no parameters, you will be prompted to confirm whether you want to compile it.</span></span> <span data-ttu-id="33013-125">Als de configuratie van de parameters, heeft de **configuratie compileren** blade geopend zodat u parameterwaarden kan opgeven.</span><span class="sxs-lookup"><span data-stu-id="33013-125">If the configuration has parameters, the **Compile Configuration** blade will open so you can provide parameter values.</span></span> <span data-ttu-id="33013-126">Zie de [ **fundamentele Parameters** ](#basic-parameters) sectie hieronder voor meer informatie over parameters.</span><span class="sxs-lookup"><span data-stu-id="33013-126">See the [**Basic Parameters**](#basic-parameters) section below for further details on parameters.</span></span>
5. <span data-ttu-id="33013-127">De **Compilatietaak** blade wordt geopend zodat u de status van de Compilatietaak en de knooppuntconfiguraties (MOF configuratiedocumenten) het veroorzaakt worden geplaatst op de Azure Automation DSC-Pull-Server kunt bijhouden.</span><span class="sxs-lookup"><span data-stu-id="33013-127">The **Compilation Job** blade is opened so that you can track the compilation job's status, and the node configurations (MOF configuration documents) it caused to be placed on the Azure Automation DSC Pull Server.</span></span>

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a><span data-ttu-id="33013-128">Compileren van een DSC-configuratie met Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="33013-128">Compiling a DSC Configuration with Windows PowerShell</span></span>

<span data-ttu-id="33013-129">U kunt [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) te compileren met Windows PowerShell starten.</span><span class="sxs-lookup"><span data-stu-id="33013-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) to start compiling with Windows PowerShell.</span></span> <span data-ttu-id="33013-130">De volgende voorbeeldcode wordt gestart compilatie van een DSC-configuratie aangeroepen **SampleConfig**.</span><span class="sxs-lookup"><span data-stu-id="33013-130">The following sample code starts compilation of a DSC configuration called **SampleConfig**.</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

<span data-ttu-id="33013-131">`Start-AzureRmAutomationDscCompilationJob`retourneert een taakobject compilatie waarmee u kunt de status ervan bijhouden.</span><span class="sxs-lookup"><span data-stu-id="33013-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use to track its status.</span></span> <span data-ttu-id="33013-132">U kunt dit object compilatie met [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) om te bepalen van de status van de Compilatietaak en [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) om weer te geven van de stromen (uitvoer).</span><span class="sxs-lookup"><span data-stu-id="33013-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) to determine the status of the compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) to view its streams (output).</span></span> <span data-ttu-id="33013-133">De volgende voorbeeldcode wordt gestart compilatie van de **SampleConfig** configuratie, wacht totdat deze is voltooid en wordt vervolgens de stromen.</span><span class="sxs-lookup"><span data-stu-id="33013-133">The following sample code starts compilation of the **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span></span>

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a><span data-ttu-id="33013-134">Basic-Parameters</span><span class="sxs-lookup"><span data-stu-id="33013-134">Basic Parameters</span></span>
<span data-ttu-id="33013-135">Parameterdeclaratie in DSC-configuraties, inclusief parametertypen en eigenschappen werkt hetzelfde als in Azure Automation-runbooks.</span><span class="sxs-lookup"><span data-stu-id="33013-135">Parameter declaration in DSC configurations, including parameter types and properties, works the same as in Azure Automation runbooks.</span></span> <span data-ttu-id="33013-136">Zie [een runbook starten in Azure Automation](automation-starting-a-runbook.md) voor meer informatie over runbook-parameters.</span><span class="sxs-lookup"><span data-stu-id="33013-136">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to learn more about runbook parameters.</span></span>

<span data-ttu-id="33013-137">Het volgende voorbeeld worden twee parameters aangeroepen **FeatureName** en **IsPresent**om te bepalen van de waarden van eigenschappen in de **ParametersExample.sample** knooppuntconfiguratie, gegenereerd tijdens de compilatie.</span><span class="sxs-lookup"><span data-stu-id="33013-137">The following example uses two parameters called **FeatureName** and **IsPresent**, to determine the values of properties in the **ParametersExample.sample** node configuration, generated during compilation.</span></span>

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

<span data-ttu-id="33013-138">U kunt compileren DSC-configuraties die gebruikmaken van eenvoudige parameters in de Azure Automation DSC-portal of met Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="33013-138">You can compile DSC Configurations that use basic parameters in the Azure Automation DSC portal, or with Azure PowerShell:</span></span>

### <a name="portal"></a><span data-ttu-id="33013-139">Portal</span><span class="sxs-lookup"><span data-stu-id="33013-139">Portal</span></span>

<span data-ttu-id="33013-140">In de portal kunt u parameterwaarden opgeven wanneer u op **compileren**.</span><span class="sxs-lookup"><span data-stu-id="33013-140">In the portal, you can enter parameter values after clicking **Compile**.</span></span>

![alternatieve tekst](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a><span data-ttu-id="33013-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="33013-142">PowerShell</span></span>

<span data-ttu-id="33013-143">PowerShell-parameters in vereist een [hashtabel](http://technet.microsoft.com/library/hh847780.aspx) waarbij de sleutel komt overeen met de parameternaam van de en de waarde gelijk is aan de waarde van parameter.</span><span class="sxs-lookup"><span data-stu-id="33013-143">PowerShell requires parameters in a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key matches the parameter name, and the value equals the parameter value.</span></span>

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

<span data-ttu-id="33013-144">Zie voor meer informatie over PSCredentials doorgeeft als parameters <a href="#credential-assets"> **Referentieassets** </a> hieronder.</span><span class="sxs-lookup"><span data-stu-id="33013-144">For information about passing PSCredentials as parameters, see <a href="#credential-assets">**Credential Assets**</a> below.</span></span>

## <a name="configurationdata"></a><span data-ttu-id="33013-145">ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="33013-145">ConfigurationData</span></span>
<span data-ttu-id="33013-146">**ConfigurationData** kunt u afzonderlijke structurele configuratie uit een specifieke configuratie van de omgeving tijdens het gebruik van PowerShell DSC.</span><span class="sxs-lookup"><span data-stu-id="33013-146">**ConfigurationData** allows you to separate structural configuration from any environment specific configuration while using PowerShell DSC.</span></span> <span data-ttu-id="33013-147">Zie [scheiden 'Wat' op 'Waar' in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) voor meer informatie over **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="33013-147">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) to learn more about **ConfigurationData**.</span></span>

> [!NOTE]
> <span data-ttu-id="33013-148">U kunt **ConfigurationData** bij het compileren van in Azure Automation DSC met Azure PowerShell, maar niet in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="33013-148">You can use **ConfigurationData** when compiling in Azure Automation DSC using Azure PowerShell, but not in the Azure portal.</span></span>

<span data-ttu-id="33013-149">Het volgende DSC-voorbeeldconfiguratie gebruikt **ConfigurationData** via de **$ConfigurationData** en **$AllNodes** trefwoorden.</span><span class="sxs-lookup"><span data-stu-id="33013-149">The following example DSC configuration uses **ConfigurationData** via the **$ConfigurationData** and **$AllNodes** keywords.</span></span> <span data-ttu-id="33013-150">U moet ook de [ **xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) voor dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="33013-150">You'll also need the [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span></span>

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

<span data-ttu-id="33013-151">U kunt de DSC-configuratie hierboven met PowerShell compileren.</span><span class="sxs-lookup"><span data-stu-id="33013-151">You can compile the DSC configuration above with PowerShell.</span></span> <span data-ttu-id="33013-152">De onderstaande PowerShell voegt u twee knooppuntconfiguraties toe aan de Azure Automation DSC-Pull-Server: **ConfigurationDataSample.MyVM1** en **ConfigurationDataSample.MyVM3**:</span><span class="sxs-lookup"><span data-stu-id="33013-152">The below PowerShell adds two node configurations to the Azure Automation DSC Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span></span>

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

## <a name="assets"></a><span data-ttu-id="33013-153">Assets</span><span class="sxs-lookup"><span data-stu-id="33013-153">Assets</span></span>

<span data-ttu-id="33013-154">Asset-verwijzingen zijn hetzelfde als in Azure Automation DSC-configuraties en runbooks.</span><span class="sxs-lookup"><span data-stu-id="33013-154">Asset references are the same in Azure Automation DSC configurations and runbooks.</span></span> <span data-ttu-id="33013-155">Zie de volgende onderwerpen voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="33013-155">See the following for more information:</span></span>

* [<span data-ttu-id="33013-156">Certificaten</span><span class="sxs-lookup"><span data-stu-id="33013-156">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="33013-157">Verbindingen</span><span class="sxs-lookup"><span data-stu-id="33013-157">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="33013-158">Referenties</span><span class="sxs-lookup"><span data-stu-id="33013-158">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="33013-159">Variabelen</span><span class="sxs-lookup"><span data-stu-id="33013-159">Variables</span></span>](automation-variables.md)

### <a name="credential-assets"></a><span data-ttu-id="33013-160">Referentieassets</span><span class="sxs-lookup"><span data-stu-id="33013-160">Credential Assets</span></span>

<span data-ttu-id="33013-161">Terwijl in Azure Automation DSC-configuraties kunnen verwijzen naar referentieassets met **Get-AzureRmAutomationCredential**, referentieassets kunnen ook worden doorgegeven via parameters, indien gewenst.</span><span class="sxs-lookup"><span data-stu-id="33013-161">While DSC configurations in Azure Automation can reference credential assets using **Get-AzureRmAutomationCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="33013-162">Als een parameter van het duurt een configuratie voordat **PSCredential** typt, moet u de naam van een Azure Automation-referentieasset doorgeven als waarde van de parameter in plaats van een PSCredential-object.</span><span class="sxs-lookup"><span data-stu-id="33013-162">If a configuration takes a parameter of **PSCredential** type, then you need to pass the string name of an Azure Automation credential asset as that parameter’s value, rather than a PSCredential object.</span></span> <span data-ttu-id="33013-163">Achter de schermen worden wordt de Azure Automation-referentieasset met deze naam opgehaald en doorgegeven aan de configuratie.</span><span class="sxs-lookup"><span data-stu-id="33013-163">Behind the scenes, the Azure Automation credential asset with that name will be retrieved and passed to the configuration.</span></span>

<span data-ttu-id="33013-164">Referenties houden beveiligd in knooppuntconfiguraties (MOF configuratiedocumenten) is vereist voor het versleutelen van de referenties in het knooppunt configuratie MOF-bestand.</span><span class="sxs-lookup"><span data-stu-id="33013-164">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting the credentials in the node configuration MOF file.</span></span> <span data-ttu-id="33013-165">Azure Automation hierbij nog een stapje verder neemt en versleutelt het hele MOF-bestand.</span><span class="sxs-lookup"><span data-stu-id="33013-165">Azure Automation takes this one step further and encrypts the entire MOF file.</span></span> <span data-ttu-id="33013-166">Echter, momenteel u moet hoogte PowerShell DSC dat dit klopt om referenties als tekst zonder opmaak tijdens het genereren van het knooppunt configuratie MOF output omdat PowerShell DSC niet weet dat Azure Automation wordt worden versleutelen van het hele MOF-bestand na de generatie via een Compilatietaak.</span><span class="sxs-lookup"><span data-stu-id="33013-166">However, currently you must tell PowerShell DSC it is okay for credentials to be outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting the entire MOF file after its generation via a compilation job.</span></span>

<span data-ttu-id="33013-167">U kunt zien PowerShell DSC die dit voor referenties klopt output in tekst zonder opmaak in de gegenereerde knooppuntconfiguratie MOF-bestanden met [ **ConfigurationData**](#configurationdata).</span><span class="sxs-lookup"><span data-stu-id="33013-167">You can tell PowerShell DSC that it is okay for credentials to be outputted in plain text in the generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span></span> <span data-ttu-id="33013-168">U moet doorgeven `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** voor elk knooppunt-blok-naam die wordt weergegeven in de DSC-configuratie en de referenties worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="33013-168">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in the DSC configuration and uses credentials.</span></span>

<span data-ttu-id="33013-169">Het volgende voorbeeld toont een DSC-configuratie die gebruikmaakt van een Automation-referentieasset.</span><span class="sxs-lookup"><span data-stu-id="33013-169">The following example shows a DSC configuration that uses an Automation credential asset.</span></span>

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

<span data-ttu-id="33013-170">U kunt de DSC-configuratie hierboven met PowerShell compileren.</span><span class="sxs-lookup"><span data-stu-id="33013-170">You can compile the DSC configuration above with PowerShell.</span></span> <span data-ttu-id="33013-171">De onderstaande PowerShell voegt u twee knooppuntconfiguraties toe aan de Azure Automation DSC-Pull-Server: **CredentialSample.MyVM1** en **CredentialSample.MyVM2**.</span><span class="sxs-lookup"><span data-stu-id="33013-171">The below PowerShell adds two node configurations to the Azure Automation DSC Pull Server:  **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span></span>

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

## <a name="importing-node-configurations"></a><span data-ttu-id="33013-172">Knooppuntconfiguraties importeren</span><span class="sxs-lookup"><span data-stu-id="33013-172">Importing node configurations</span></span>

<span data-ttu-id="33013-173">U kunt ook knooppunt configuratons (MOF-bestanden) die u hebt gecompileerd buiten Azure importeren.</span><span class="sxs-lookup"><span data-stu-id="33013-173">You can also import node configuratons (MOFs) that you have compiled outside of Azure.</span></span> <span data-ttu-id="33013-174">Een voordeel hiervan is dat confiturations knooppunt kan worden ondertekend.</span><span class="sxs-lookup"><span data-stu-id="33013-174">One advantage of this is that node confiturations can be signed.</span></span>
<span data-ttu-id="33013-175">Een ondertekende knooppuntconfiguratie is lokaal op een beheerde knooppunt gecontroleerd door de DSC-agent, waarbij u ervoor zorgt dat de configuratie die wordt toegepast op het knooppunt van een gemachtigde bron afkomstig is.</span><span class="sxs-lookup"><span data-stu-id="33013-175">A signed node configuration is verified locally on a managed node by the DSC agent, ensuring that the configuration being applied to the node comes from an authorized source.</span></span>

> [!NOTE]
> <span data-ttu-id="33013-176">U kunt importeren gebruiken configuraties in uw Azure Automation-account is ondertekend, maar Azure Automation biedt momenteel geen ondersteuning voor het compileren van ondertekende configuraties.</span><span class="sxs-lookup"><span data-stu-id="33013-176">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span></span>

> [!NOTE]
> <span data-ttu-id="33013-177">Een configuratiebestand knooppunt mag niet groter zijn dan 1 MB te laten worden geïmporteerd in Azure Automation zijn.</span><span class="sxs-lookup"><span data-stu-id="33013-177">A node configuration file must be no larger than 1 MB to allow it to be imported into Azure Automation.</span></span>

<span data-ttu-id="33013-178">U kunt informatie over het ondertekenen van knooppuntconfiguraties op https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span><span class="sxs-lookup"><span data-stu-id="33013-178">You can learn how to sign node configurations at https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span></span>

### <a name="importing-a-node-configuration-in-the-azure-portal"></a><span data-ttu-id="33013-179">Importeren van de configuratie van een knooppunt in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="33013-179">Importing a node configuration in the Azure portal</span></span>

1. <span data-ttu-id="33013-180">Van uw Automation-account, klikt u op **DSC-knooppuntconfiguraties**.</span><span class="sxs-lookup"><span data-stu-id="33013-180">From your Automation account, click **DSC node configurations**.</span></span>

    ![DSC-knooppuntconfiguraties](./media/automation-dsc-compile/node-config.png)
2. <span data-ttu-id="33013-182">In de **DSC-knooppuntconfiguraties** blade, klikt u op **toevoegen van een NodeConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="33013-182">In the **DSC node configurations** blade, click **Add a NodeConfiguration**.</span></span>
3. <span data-ttu-id="33013-183">In de **importeren** blade, klik op het pictogram naast de **configuratiebestand knooppunt** textbox om te bladeren naar een knooppunt-configuratiebestand (MOF) op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="33013-183">In the **Import** blade, click the folder icon next to the **Node Configuration File** textbox to browse for a node configuration file (MOF) on your local computer.</span></span>

    ![Zoeken naar een lokaal bestand](./media/automation-dsc-compile/import-browse.png)
4. <span data-ttu-id="33013-185">Voer een naam in de **configuratienaam** textbox.</span><span class="sxs-lookup"><span data-stu-id="33013-185">Enter a name in the **Configuration Name** textbox.</span></span> <span data-ttu-id="33013-186">Deze naam moet overeenkomen met de naam van de configuratie van waaruit de knooppuntconfiguratie is gecompileerd.</span><span class="sxs-lookup"><span data-stu-id="33013-186">This name must match the name of the configuration from which the node configuration was compiled.</span></span>
5. <span data-ttu-id="33013-187">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="33013-187">Click **OK**.</span></span>

### <a name="importing-a-node-configuration-with-powershell"></a><span data-ttu-id="33013-188">Importeren van de configuratie van een knooppunt met PowerShell</span><span class="sxs-lookup"><span data-stu-id="33013-188">Importing a node configuration with PowerShell</span></span>

<span data-ttu-id="33013-189">U kunt de [importeren AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet voor het importeren van de knooppuntconfiguratie van een in uw automation-account.</span><span class="sxs-lookup"><span data-stu-id="33013-189">You can use the [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet to import a node configuration into your automation account.</span></span>

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



