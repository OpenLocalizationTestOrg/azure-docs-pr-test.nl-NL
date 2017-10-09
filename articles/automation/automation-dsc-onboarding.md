---
title: computers voor beheer door Azure Automation DSC aaaOnboarding | Microsoft Docs
description: Hoe toosetup machines voor beheer met Azure Automation DSC
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: ef15801fec2ffea4ba62dcba2fbe9af09268e424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a><span data-ttu-id="f2624-103">Computers voorbereiden voor beheer door Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="f2624-103">Onboarding machines for management by Azure Automation DSC</span></span>

## <a name="why-manage-machines-with-azure-automation-dsc"></a><span data-ttu-id="f2624-104">Waarom machines met een Azure Automation DSC beheren?</span><span class="sxs-lookup"><span data-stu-id="f2624-104">Why manage machines with Azure Automation DSC?</span></span>

<span data-ttu-id="f2624-105">Zoals [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is een eenvoudige maar krachtige, configuration management-service voor DSC-knooppunten (fysieke en virtuele machines) in een cloud of on-premises datacenter.</span><span class="sxs-lookup"><span data-stu-id="f2624-105">Like [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is a simple, yet powerful, configuration management service for DSC nodes (physical and virtual machines) in any cloud or on-premises datacenter.</span></span> <span data-ttu-id="f2624-106">Hiermee kunt schaalbaarheid in duizenden computers snel en eenvoudig vanuit een centrale, veilige locatie.</span><span class="sxs-lookup"><span data-stu-id="f2624-106">It enables scalability across thousands of machines quickly and easily from a central, secure location.</span></span> <span data-ttu-id="f2624-107">U kunt eenvoudig vrijgeven machines, toewijzen ze declaratieve configuraties en rapporten weergeven met elk van de computer de compatibiliteitsstatus van toohello gewenst die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f2624-107">You can easily onboard machines, assign them declarative configurations, and view reports showing each machine's compliance toohello desired state you specified.</span></span> <span data-ttu-id="f2624-108">Hello Azure Automation DSC-beheerlaag is tooDSC welke hello Azure Automation-beheerlaag is tooPowerShell scripting.</span><span class="sxs-lookup"><span data-stu-id="f2624-108">hello Azure Automation DSC management layer is tooDSC what hello Azure Automation management layer is tooPowerShell scripting.</span></span> <span data-ttu-id="f2624-109">Met andere woorden, in Hallo dezelfde manier die u helpt Azure Automation PowerShell-scripts beheren, ook helpt u bij het beheren van DSC-configuraties.</span><span class="sxs-lookup"><span data-stu-id="f2624-109">In other words, in hello same way that Azure Automation helps you manage PowerShell scripts, it also helps you manage DSC configurations.</span></span> <span data-ttu-id="f2624-110">Zie toolearn meer informatie over de voordelen van het gebruik van Azure Automation DSC Hallo [overzicht van Azure Automation DSC](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f2624-110">toolearn more about hello benefits of using Azure Automation DSC, see [Azure Automation DSC overview](automation-dsc-overview.md).</span></span>

<span data-ttu-id="f2624-111">Gebruikte toomanage diverse computers kan worden uitgevoerd met Azure Automation DSC:</span><span class="sxs-lookup"><span data-stu-id="f2624-111">Azure Automation DSC can be used toomanage a variety of machines:</span></span>

* <span data-ttu-id="f2624-112">Virtuele machines in Azure (klassiek)</span><span class="sxs-lookup"><span data-stu-id="f2624-112">Azure virtual machines (classic)</span></span>
* <span data-ttu-id="f2624-113">Virtuele machines van Azure</span><span class="sxs-lookup"><span data-stu-id="f2624-113">Azure virtual machines</span></span>
* <span data-ttu-id="f2624-114">Amazon Web Services (AWS) virtuele machines</span><span class="sxs-lookup"><span data-stu-id="f2624-114">Amazon Web Services (AWS) virtual machines</span></span>
* <span data-ttu-id="f2624-115">Fysiek virtueel Windows machines on-premises of in een cloud dan Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="f2624-115">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>
* <span data-ttu-id="f2624-116">Fysiek virtueel Linux-machines on-premises in Azure of in een cloud dan Azure</span><span class="sxs-lookup"><span data-stu-id="f2624-116">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="f2624-117">Daarnaast bent u niet klaar toomanage machineconfiguratie vanuit de cloud hello, kan Azure Automation DSC ook worden gebruikt als een eindpunt in het rapport alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="f2624-117">In addition, if you are not ready toomanage machine configuration from hello cloud, Azure Automation DSC can also be used as a report-only endpoint.</span></span> <span data-ttu-id="f2624-118">Hiermee kunt u de gewenste configuratie tooset (push) via DSC on-premises en uitgebreide rapportage details weergeven over de naleving Hallo knooppunt gewenst status in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="f2624-118">This allows you tooset (push) desired configuration through DSC on-premises and view rich reporting details on node compliance with hello desired state in Azure Automation.</span></span>

<span data-ttu-id="f2624-119">Hallo secties na een overzicht van hoe u vrijgeven elk type machine tooAzure Automation DSC kunt.</span><span class="sxs-lookup"><span data-stu-id="f2624-119">hello following sections outline how you can onboard each type of machine tooAzure Automation DSC.</span></span>

## <a name="azure-virtual-machines-classic"></a><span data-ttu-id="f2624-120">Virtuele machines in Azure (klassiek)</span><span class="sxs-lookup"><span data-stu-id="f2624-120">Azure virtual machines (classic)</span></span>

<span data-ttu-id="f2624-121">Met Azure Automation DSC kunt u eenvoudig vrijgeven virtuele machines in Azure (klassiek) voor Configuratiebeheer met hello Azure-portal of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2624-121">With Azure Automation DSC, you can easily onboard Azure virtual machines (classic) for configuration management using either hello Azure portal, or PowerShell.</span></span> <span data-ttu-id="f2624-122">Achter de schermen Hallo en zonder een beheerder met tooremote in Hallo VM registreert hello Azure VM Desired State Configuration-extensie Hallo VM bij Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="f2624-122">Under hello hood, and without an administrator having tooremote into hello VM, hello Azure VM Desired State Configuration extension registers hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="f2624-123">Aangezien hello Azure VM Desired State Configuration extensie asynchroon uitgevoerd, stappen tootrack voortgangsgegevens of het oplossen van deze beschikbaar zijn in Hallo [ **probleemoplossing voor Azure virtuele machine voorbereiden** ](#troubleshooting-azure-virtual-machine-onboarding)hieronder.</span><span class="sxs-lookup"><span data-stu-id="f2624-123">Since hello Azure VM Desired State Configuration extension runs asynchronously, steps tootrack its progress or troubleshoot it are provided in hello [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="f2624-124">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f2624-124">Azure portal</span></span>

<span data-ttu-id="f2624-125">In Hallo [Azure-portal](http://portal.azure.com/), klikt u op **Bladeren** -> **virtuele machines (klassiek)**.</span><span class="sxs-lookup"><span data-stu-id="f2624-125">In hello [Azure portal](http://portal.azure.com/), click **Browse** -> **Virtual machines (classic)**.</span></span> <span data-ttu-id="f2624-126">Selecteer de gewenste tooonboard virtuele machine van Windows hello.</span><span class="sxs-lookup"><span data-stu-id="f2624-126">Select hello Windows VM you want tooonboard.</span></span> <span data-ttu-id="f2624-127">Klik op Hallo van de virtuele machine dashboard blade **alle instellingen** -> **extensies** -> **toevoegen**  ->   **Azure Automation DSC** -> **maken**.</span><span class="sxs-lookup"><span data-stu-id="f2624-127">On hello virtual machine's dashboard blade, click **All settings** -> **Extensions** -> **Add** -> **Azure Automation DSC** -> **Create**.</span></span> <span data-ttu-id="f2624-128">Voer Hallo [PowerShell DSC Local Configuration Manager-waarden](https://msdn.microsoft.com/powershell/dsc/metaconfig4) vereist is voor uw gebruiksvoorbeeld registratiecode voor uw Automation-account en registratie-URL en eventueel een knooppunt configuratie tooassign toohello VM.</span><span class="sxs-lookup"><span data-stu-id="f2624-128">Enter hello [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, your Automation account's registration key and registration URL, and optionally a node configuration tooassign toohello VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

<span data-ttu-id="f2624-129">toofind Hallo registratie-URL's en -sleutel voor Hallo Automation-account tooonboard Hallo machine, Zie Hallo [ **registratie Secure** ](#secure-registration) hieronder.</span><span class="sxs-lookup"><span data-stu-id="f2624-129">toofind hello registration URL and key for hello Automation account tooonboard hello machine to, see hello [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="f2624-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2624-130">PowerShell</span></span>

```powershell
# log in tooboth Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in hello name of a Node Configuration in Azure Automation DSC, for this VM tooconform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use hello DSC extension tooonboard hello VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a><span data-ttu-id="f2624-131">Virtuele machines van Azure</span><span class="sxs-lookup"><span data-stu-id="f2624-131">Azure virtual machines</span></span>

<span data-ttu-id="f2624-132">Azure Automation DSC kunt u eenvoudig vrijgeven Azure virtuele machines voor Configuratiebeheer, via hello Azure-portal, Azure Resource Manager-sjablonen of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2624-132">Azure Automation DSC lets you easily onboard Azure virtual machines for configuration management, using either hello Azure portal, Azure Resource Manager templates, or PowerShell.</span></span> <span data-ttu-id="f2624-133">Achter de schermen Hallo en zonder een beheerder met tooremote in Hallo VM registreert hello Azure VM Desired State Configuration-extensie Hallo VM bij Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="f2624-133">Under hello hood, and without an administrator having tooremote into hello VM, hello Azure VM Desired State Configuration extension registers hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="f2624-134">Aangezien hello Azure VM Desired State Configuration extensie asynchroon uitgevoerd, stappen tootrack voortgangsgegevens of het oplossen van deze beschikbaar zijn in Hallo [ **probleemoplossing voor Azure virtuele machine voorbereiden** ](#troubleshooting-azure-virtual-machine-onboarding)hieronder.</span><span class="sxs-lookup"><span data-stu-id="f2624-134">Since hello Azure VM Desired State Configuration extension runs asynchronously, steps tootrack its progress or troubleshoot it are provided in hello [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="f2624-135">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f2624-135">Azure portal</span></span>

<span data-ttu-id="f2624-136">In Hallo [Azure-portal](https://portal.azure.com/), navigeer toohello Azure Automation-account waar u tooonboard virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="f2624-136">In hello [Azure portal](https://portal.azure.com/), navigate toohello Azure Automation account where you want tooonboard virtual machines.</span></span> <span data-ttu-id="f2624-137">Klik op het dashboard van Automation-account bij hello, **DSC-knooppunten** -> **toevoegen Azure VM**.</span><span class="sxs-lookup"><span data-stu-id="f2624-137">On hello Automation account dashboard, click **DSC Nodes** -> **Add Azure VM**.</span></span>

<span data-ttu-id="f2624-138">Onder **tooonboard van virtuele machines selecteren**, selecteer een of meer Azure virtual machines tooonboard.</span><span class="sxs-lookup"><span data-stu-id="f2624-138">Under **Select virtual machines tooonboard**, select one or more Azure virtual machines tooonboard.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

<span data-ttu-id="f2624-139">Onder **registratiegegevens configureren**, Voer Hallo [PowerShell DSC Local Configuration Manager-waarden](https://msdn.microsoft.com/powershell/dsc/metaconfig4) vereist zijn voor uw gebruiksvoorbeeld en eventueel een knooppunt configuratie tooassign toohello VM.</span><span class="sxs-lookup"><span data-stu-id="f2624-139">Under **Configure registration data**, enter hello [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, and optionally a node configuration tooassign toohello VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="f2624-140">Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="f2624-140">Azure Resource Manager templates</span></span>

<span data-ttu-id="f2624-141">Azure virtuele machines kunnen worden geïmplementeerd en vrijgegeven tooAzure Automation DSC via Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="f2624-141">Azure virtual machines can be deployed and onboarded tooAzure Automation DSC via Azure Resource Manager templates.</span></span> <span data-ttu-id="f2624-142">Zie [configureren van een virtuele machine via de DSC-extensie en Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) voor een van de voorbeeldsjabloon die onboards een bestaande VM-tooAzure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="f2624-142">See [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) for an example template that onboards an existing VM tooAzure Automation DSC.</span></span> <span data-ttu-id="f2624-143">toofind hello registratie sleutel en registratie-URL genomen als invoer in deze sjabloon Zie Hallo [ **registratie Secure** ](#secure-registration) hieronder.</span><span class="sxs-lookup"><span data-stu-id="f2624-143">toofind hello registration key and registration URL taken as input in this template, see hello [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="f2624-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2624-144">PowerShell</span></span>

<span data-ttu-id="f2624-145">Hallo [registreren AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet gebruikte tooonboard virtuele machines in Azure portal via PowerShell Hallo kan zijn.</span><span class="sxs-lookup"><span data-stu-id="f2624-145">hello [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet can be used tooonboard virtual machines in hello Azure portal via PowerShell.</span></span>

## <a name="amazon-web-services-aws-virtual-machines"></a><span data-ttu-id="f2624-146">Amazon Web Services (AWS) virtuele machines</span><span class="sxs-lookup"><span data-stu-id="f2624-146">Amazon Web Services (AWS) virtual machines</span></span>

<span data-ttu-id="f2624-147">U kunt eenvoudig vrijgeven Amazon Web Services virtuele machines voor Configuratiebeheer door Azure Automation DSC met Hallo AWS DSC-Toolkit.</span><span class="sxs-lookup"><span data-stu-id="f2624-147">You can easily onboard Amazon Web Services virtual machines for configuration management by Azure Automation DSC using hello AWS DSC Toolkit.</span></span> <span data-ttu-id="f2624-148">U kunt meer informatie over Hallo toolkit [hier](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span><span class="sxs-lookup"><span data-stu-id="f2624-148">You can learn more about hello toolkit [here](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span></span>

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a><span data-ttu-id="f2624-149">Fysiek virtueel Windows machines on-premises of in een cloud dan Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="f2624-149">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>

<span data-ttu-id="f2624-150">Lokale Windows-machines en Windows-machines in niet-Azure-clouds (zoals Amazon Web Services) kunnen ook worden vrijgegeven tooAzure Automation DSC zolang ze beschikken over uitgaande toegang toohello internet via een paar eenvoudige stappen:</span><span class="sxs-lookup"><span data-stu-id="f2624-150">On-premises Windows machines and Windows machines in non-Azure clouds (such as Amazon Web Services) can also be onboarded tooAzure Automation DSC, as long as they have outbound access toohello internet, via a few simple steps:</span></span>

1. <span data-ttu-id="f2624-151">Zorg ervoor dat Hallo meest recente versie van [WMF 5](http://aka.ms/wmf5latest) is geïnstalleerd op Hallo machines gewenste tooonboard tooAzure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="f2624-151">Make sure hello latest version of [WMF 5](http://aka.ms/wmf5latest) is installed on hello machines you want tooonboard tooAzure Automation DSC.</span></span>
2. <span data-ttu-id="f2624-152">Volg de aanwijzingen Hallo in sectie [ **genereren DSC metaconfigurations** ](#generating-dsc-metaconfigurations) hieronder toogenerate map met de Hallo DSC metaconfigurations nodig.</span><span class="sxs-lookup"><span data-stu-id="f2624-152">Follow hello directions in section [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) below toogenerate a folder containing hello needed DSC metaconfigurations.</span></span>
3. <span data-ttu-id="f2624-153">Hallo PowerShell DSC-metaconfiguratie toe toohello machines gewenste tooonboard extern toe te passen.</span><span class="sxs-lookup"><span data-stu-id="f2624-153">Remotely apply hello PowerShell DSC metaconfiguration toohello machines you want tooonboard.</span></span> <span data-ttu-id="f2624-154">**Hallo-machine met deze opdracht wordt uitgevoerd vanaf moet hebben Hallo meest recente versie van [WMF 5](http://aka.ms/wmf5latest) geïnstalleerd**:</span><span class="sxs-lookup"><span data-stu-id="f2624-154">**hello machine this command is run from must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed**:</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. <span data-ttu-id="f2624-155">Als u niet op afstand Hallo PowerShell DSC metaconfigurations toepassen, kopieert u Hallo metaconfigurations map uit stap 2 op elke machine tooonboard.</span><span class="sxs-lookup"><span data-stu-id="f2624-155">If you cannot apply hello PowerShell DSC metaconfigurations remotely, copy hello metaconfigurations folder from step 2 onto each machine tooonboard.</span></span> <span data-ttu-id="f2624-156">Roep vervolgens **Set DscLocalConfigurationManager** lokaal op elke machine tooonboard.</span><span class="sxs-lookup"><span data-stu-id="f2624-156">Then call **Set-DscLocalConfigurationManager** locally on each machine tooonboard.</span></span>
5. <span data-ttu-id="f2624-157">Hello Azure-portal of cmdlets, Controleer of de Hallo machines tooonboard nu weergegeven als DSC-knooppunten die zijn geregistreerd in Azure Automation-account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f2624-157">Using hello Azure portal or cmdlets, check that hello machines tooonboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a><span data-ttu-id="f2624-158">Fysiek virtueel Linux-machines on-premises in Azure of in een cloud dan Azure</span><span class="sxs-lookup"><span data-stu-id="f2624-158">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="f2624-159">Lokale Linux-machines, Linux-machines in Azure, en Linux-machines in niet-Azure-clouds kunnen ook worden vrijgegeven tooAzure Automation DSC zolang ze beschikken over uitgaande toegang toohello internet via een paar eenvoudige stappen:</span><span class="sxs-lookup"><span data-stu-id="f2624-159">On-premises Linux machines, Linux machines in Azure, and Linux machines in non-Azure clouds can also be onboarded tooAzure Automation DSC, as long as they have outbound access toohello internet, via a few simple steps:</span></span>

1. <span data-ttu-id="f2624-160">Zorg ervoor dat Hallo meest recente versie van [PowerShell Desired State Configuration voor Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is geïnstalleerd op Hallo machines gewenste tooonboard tooAzure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="f2624-160">Make sure hello latest version of [PowerShell Desired State Configuration for Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is installed on hello machines you want tooonboard tooAzure Automation DSC.</span></span>
2. <span data-ttu-id="f2624-161">Als hello [standaardinstellingen voor PowerShell DSC Local Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig4) overeenkomen met uw gebruiksvoorbeeld en gewenste tooonboard machines zoals dat zij **beide** halen uit en tooAzure Automation DSC rapporteren:</span><span class="sxs-lookup"><span data-stu-id="f2624-161">If hello [PowerShell DSC Local Configuration Manager defaults](https://msdn.microsoft.com/powershell/dsc/metaconfig4) match your use case, and you want tooonboard machines such that they **both** pull from and report tooAzure Automation DSC:</span></span>

   + <span data-ttu-id="f2624-162">Gebruik op elke Linux machine tooonboard tooAzure Automation DSC, Register.py tooonboard met behulp van PowerShell DSC Local Configuration Manager standaard Hallo:</span><span class="sxs-lookup"><span data-stu-id="f2624-162">On each Linux machine tooonboard tooAzure Automation DSC, use Register.py tooonboard using hello PowerShell DSC Local Configuration Manager defaults:</span></span>

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + <span data-ttu-id="f2624-163">toofind hello registratie sleutel en registratie-URL voor uw Automation-account, Zie Hallo [ **registratie Secure** ](#secure-registration) hieronder.</span><span class="sxs-lookup"><span data-stu-id="f2624-163">toofind hello registration key and registration URL for your Automation account, see hello [**Secure registration**](#secure-registration) section below.</span></span>

     <span data-ttu-id="f2624-164">Als hello PowerShell DSC Local Configuration Manager standaard **doen** **niet** overeenkomen met uw gebruiksvoorbeeld, of het gewenste tooonboard machines zo dat ze worden alleen tooAzure Automation DSC gerapporteerd, maar niet kunnen ophalen configuratie of het PowerShell-modules, volgt u stap 3-6.</span><span class="sxs-lookup"><span data-stu-id="f2624-164">If hello PowerShell DSC Local Configuration Manager defaults **do** **not** match your use case, or you want tooonboard machines such that they only report tooAzure Automation DSC, but do not pull configuration or PowerShell modules from it,  follow steps 3 - 6.</span></span> <span data-ttu-id="f2624-165">Ga anders verder rechtstreeks toostep 6.</span><span class="sxs-lookup"><span data-stu-id="f2624-165">Otherwise, proceed directly toostep 6.</span></span>

3. <span data-ttu-id="f2624-166">Volg de aanwijzingen Hallo in Hallo [ **genereren DSC metaconfigurations** ](#generating-dsc-metaconfigurations) sectie hieronder toogenerate map met de Hallo nodig DSC metaconfigurations.</span><span class="sxs-lookup"><span data-stu-id="f2624-166">Follow hello directions in hello [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) section below toogenerate a folder containing hello needed DSC metaconfigurations.</span></span>
4. <span data-ttu-id="f2624-167">Hallo PowerShell DSC-metaconfiguratie toe toohello machines gewenste tooonboard extern toe te passen:</span><span class="sxs-lookup"><span data-stu-id="f2624-167">Remotely apply hello PowerShell DSC metaconfiguration toohello machines you want tooonboard:</span></span>

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

<span data-ttu-id="f2624-168">Hallo-machine met deze opdracht wordt uitgevoerd vanaf moet hebben Hallo meest recente versie van [WMF 5](http://aka.ms/wmf5latest) geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f2624-168">hello machine this command is run from must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>

1. <span data-ttu-id="f2624-169">Als u geen Hallo PowerShell DSC metaconfigurations op afstand voor elke tooonboard Linux-machine toepassen kopieert u Hallo metaconfiguratie overeenkomstige toothat machine uit de map Hallo in stap 5 op Hallo Linux-machine.</span><span class="sxs-lookup"><span data-stu-id="f2624-169">If you cannot apply hello PowerShell DSC metaconfigurations remotely, for each Linux machine tooonboard, copy hello metaconfiguration corresponding toothat machine from hello folder in step 5 onto hello Linux machine.</span></span> <span data-ttu-id="f2624-170">Roep vervolgens `SetDscLocalConfigurationManager.py` lokaal op elke Linux-machine u tooonboard tooAzure Automation DSC wilt:</span><span class="sxs-lookup"><span data-stu-id="f2624-170">Then call `SetDscLocalConfigurationManager.py` locally on each Linux machine you want tooonboard tooAzure Automation DSC:</span></span>

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. <span data-ttu-id="f2624-171">Hello Azure-portal of cmdlets, Controleer of de Hallo machines tooonboard nu weergegeven als DSC-knooppunten die zijn geregistreerd in Azure Automation-account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f2624-171">Using hello Azure portal or cmdlets, check that hello machines tooonboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="generating-dsc-metaconfigurations"></a><span data-ttu-id="f2624-172">DSC-metaconfigurations genereren</span><span class="sxs-lookup"><span data-stu-id="f2624-172">Generating DSC metaconfigurations</span></span>

<span data-ttu-id="f2624-173">toogenerically vrijgeven een tooAzure Automation DSC machine een [DSC-metaconfiguratie toe](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) kan worden gegenereerd die, wanneer toegepast, vertelt Hallo DSC-agent op Hallo machine toopull uit en/of tooAzure Automation DSC rapporteren.</span><span class="sxs-lookup"><span data-stu-id="f2624-173">toogenerically onboard any machine tooAzure Automation DSC, a [DSC metaconfiguration](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) can be generated that, when applied, tells hello DSC agent on hello machine toopull from and/or report tooAzure Automation DSC.</span></span> <span data-ttu-id="f2624-174">DSC-metaconfigurations voor Azure Automation DSC kan worden gegenereerd met behulp van een PowerShell DSC-configuratie, of hello Azure Automation PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="f2624-174">DSC metaconfigurations for Azure Automation DSC can be generated using either a PowerShell DSC configuration, or hello Azure Automation PowerShell cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="f2624-175">DSC-metaconfigurations bevatten Hallo geheimen nodig tooonboard een machine tooan Automation-account voor beheer.</span><span class="sxs-lookup"><span data-stu-id="f2624-175">DSC metaconfigurations contain hello secrets needed tooonboard a machine tooan Automation account for management.</span></span> <span data-ttu-id="f2624-176">Zorg ervoor dat tooproperly beveiligen eventuele DSC-metaconfigurations die u maakt of verwijder ze na gebruik.</span><span class="sxs-lookup"><span data-stu-id="f2624-176">Make sure tooproperly protect any DSC metaconfigurations you create, or delete them after use.</span></span>

### <a name="using-a-dsc-configuration"></a><span data-ttu-id="f2624-177">Met behulp van een DSC-configuratie</span><span class="sxs-lookup"><span data-stu-id="f2624-177">Using a DSC Configuration</span></span>

1. <span data-ttu-id="f2624-178">Open Hallo PowerShell ISE als beheerder op een virtuele machine in uw lokale omgeving.</span><span class="sxs-lookup"><span data-stu-id="f2624-178">Open hello PowerShell ISE as an administrator in a machine in your local environment.</span></span> <span data-ttu-id="f2624-179">Hallo-machine moet zijn de meest recente versie Hallo van [WMF 5](http://aka.ms/wmf5latest) geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f2624-179">hello machine must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>
2. <span data-ttu-id="f2624-180">Kopieer Hallo script lokaal te volgen.</span><span class="sxs-lookup"><span data-stu-id="f2624-180">Copy hello following script locally.</span></span> <span data-ttu-id="f2624-181">Dit script bevat een PowerShell DSC-configuratie voor het maken van metaconfigurations en een opdracht tookick uit Hallo metaconfiguratie maken.</span><span class="sxs-lookup"><span data-stu-id="f2624-181">This script contains a PowerShell DSC configuration for creating metaconfigurations, and a command tookick off hello metaconfiguration creation.</span></span>

    ```powershell
    # hello DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create hello metaconfigurations
    # TODO: edit hello below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM tooonboard>', '<some other VM tooonboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set too$True toohave machines only report tooAA DSC but not pull from it
    }

    # Use PowerShell splatting toopass parameters toohello DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. <span data-ttu-id="f2624-182">Vul Hallo registratiecode en URL in voor uw Automation-account, evenals de namen van Hallo machines tooonboard Hallo.</span><span class="sxs-lookup"><span data-stu-id="f2624-182">Fill in hello registration key and URL for your Automation account, as well as hello names of hello machines tooonboard.</span></span> <span data-ttu-id="f2624-183">Alle andere parameters zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="f2624-183">All other parameters are optional.</span></span> <span data-ttu-id="f2624-184">toofind hello registratie sleutel en registratie-URL voor uw Automation-account, Zie Hallo [ **registratie Secure** ](#secure-registration) hieronder.</span><span class="sxs-lookup"><span data-stu-id="f2624-184">toofind hello registration key and registration URL for your Automation account, see hello [**Secure registration**](#secure-registration) section below.</span></span>
4. <span data-ttu-id="f2624-185">Als u Hallo machines tooreport DSC status informatie tooAzure Automation DSC wilt, maar geen pull-configuratie of het PowerShell-modules, stelt u Hallo **ReportOnly** parameter tootrue.</span><span class="sxs-lookup"><span data-stu-id="f2624-185">If you want hello machines tooreport DSC status information tooAzure Automation DSC, but not pull configuration or PowerShell modules, set hello **ReportOnly** parameter tootrue.</span></span>
5. <span data-ttu-id="f2624-186">Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f2624-186">Run hello script.</span></span> <span data-ttu-id="f2624-187">U hebt nu een map met de naam **DscMetaConfigs** die in uw werkmap Hallo PowerShell DSC metaconfigurations voor Hallo machines tooonboard (als administrator):</span><span class="sxs-lookup"><span data-stu-id="f2624-187">You should now have a folder called **DscMetaConfigs** in your working directory, containing hello PowerShell DSC metaconfigurations for hello machines tooonboard (as an administrator):</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a><span data-ttu-id="f2624-188">Met behulp van hello Azure Automation cmdlets</span><span class="sxs-lookup"><span data-stu-id="f2624-188">Using hello Azure Automation cmdlets</span></span>

<span data-ttu-id="f2624-189">Als Hallo PowerShell DSC Local Configuration Manager standaardwaarden overeenkomen met uw gebruiksvoorbeeld en u wilt dat tooonboard machines zo dat ze zowel pull van en tooAzure Automation DSC rapporteren, bieden hello Azure Automation cmdlets een vereenvoudigde methode voor het genereren van Hallo DSC metaconfigurations nodig:</span><span class="sxs-lookup"><span data-stu-id="f2624-189">If hello PowerShell DSC Local Configuration Manager defaults match your use case, and you want tooonboard machines such that they both pull from and report tooAzure Automation DSC, hello Azure Automation cmdlets provide a simplified method of generating hello DSC metaconfigurations needed:</span></span>

1. <span data-ttu-id="f2624-190">Open Hallo PowerShell-console of PowerShell ISE als beheerder op een virtuele machine in uw lokale omgeving.</span><span class="sxs-lookup"><span data-stu-id="f2624-190">Open hello PowerShell console or PowerShell ISE as an administrator in a machine in your local environment.</span></span>
2. <span data-ttu-id="f2624-191">Verbinding maken met behulp van tooAzure Resource Manager **Add-AzureRmAccount**</span><span class="sxs-lookup"><span data-stu-id="f2624-191">Connect tooAzure Resource Manager using **Add-AzureRmAccount**</span></span>
3. <span data-ttu-id="f2624-192">Hallo PowerShell DSC metaconfigurations downloaden voor Hallo-machines die u wilt dat tooonboard van Hallo Automation-account toowhich gewenste tooonboard knooppunten:</span><span class="sxs-lookup"><span data-stu-id="f2624-192">Download hello PowerShell DSC metaconfigurations for hello machines you want tooonboard from hello Automation account toowhich you want tooonboard nodes:</span></span>

    ```powershell
    # Define hello parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # hello name of hello ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # hello name of hello Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # hello names of hello computers that hello meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting toopass parameters toohello Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. <span data-ttu-id="f2624-193">U hebt nu een map met de naam ***DscMetaConfigs***, met Hallo PowerShell DSC metaconfigurations voor Hallo machines tooonboard (als administrator):</span><span class="sxs-lookup"><span data-stu-id="f2624-193">You should now have a folder called ***DscMetaConfigs***, containing hello PowerShell DSC metaconfigurations for hello machines tooonboard (as an administrator):</span></span>
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a><span data-ttu-id="f2624-194">Beveiligde registratie</span><span class="sxs-lookup"><span data-stu-id="f2624-194">Secure registration</span></span>

<span data-ttu-id="f2624-195">Machines kunnen veilig on-board tooan Azure Automation-account via Hallo WMF 5 DSC-registratie protocol, waardoor een DSC-knooppunt tooauthenticate tooa Pull-PowerShell DSC V2 of Reporting server (met inbegrip van Azure Automation DSC).</span><span class="sxs-lookup"><span data-stu-id="f2624-195">Machines can securely onboard tooan Azure Automation account through hello WMF 5 DSC registration protocol, which allows a DSC node tooauthenticate tooa PowerShell DSC V2 Pull or Reporting server (including Azure Automation DSC).</span></span> <span data-ttu-id="f2624-196">Hallo knooppunt registreert toohello server op een **registratie URL**, verificatie uitvoert met behulp van een **registratiesleutel**.</span><span class="sxs-lookup"><span data-stu-id="f2624-196">hello node registers toohello server at a **Registration URL**, authenticating using a **Registration key**.</span></span> <span data-ttu-id="f2624-197">Tijdens de registratie Hallo DSC-knooppunt en DSC-Pull/Reporting-server om te onderhandelen over een uniek certificaat voor dit knooppunt toouse voor verificatie toohello server na registratie.</span><span class="sxs-lookup"><span data-stu-id="f2624-197">During registration, hello DSC node and DSC Pull/Reporting server negotiate a unique certificate for this node toouse for authentication toohello server post-registration.</span></span> <span data-ttu-id="f2624-198">Dit proces wordt voorkomen dat de knooppunten van imitatie van een die andere, zoals wanneer een knooppunt is geknoeid en gedragen met kwaadaardige bedoelingen vrijgegeven.</span><span class="sxs-lookup"><span data-stu-id="f2624-198">This process prevents onboarded nodes from impersonating one another, such as if a node is compromised and behaving maliciously.</span></span> <span data-ttu-id="f2624-199">Na registratie Hallo registratiesleutel wordt niet gebruikt voor verificatie opnieuw en wordt verwijderd uit het Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="f2624-199">After registration, hello Registration key is not used for authentication again, and is deleted from hello node.</span></span>

<span data-ttu-id="f2624-200">U krijgt Hallo vereiste informatie voor Hallo DSC-registratie protocol van Hallo **sleutels beheren** blade in hello Azure preview-portal.</span><span class="sxs-lookup"><span data-stu-id="f2624-200">You can get hello information required for hello DSC registration protocol from hello **Manage Keys** blade in hello Azure preview portal.</span></span> <span data-ttu-id="f2624-201">Deze blade openen door te klikken op Hallo sleutelpictogram op Hallo **Essentials** deelvenster voor Hallo Automation-account.</span><span class="sxs-lookup"><span data-stu-id="f2624-201">Open this blade by clicking hello key icon on hello **Essentials** panel for hello Automation account.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* <span data-ttu-id="f2624-202">Registratie-URL is Hallo URL veld in de blade sleutels beheren Hallo.</span><span class="sxs-lookup"><span data-stu-id="f2624-202">Registration URL is hello URL field in hello Manage Keys blade.</span></span>
* <span data-ttu-id="f2624-203">Registratiecode is Hallo primaire toegangssleutel of secundaire toegangssleutel Hallo sleutels beheren blade.</span><span class="sxs-lookup"><span data-stu-id="f2624-203">Registration key is hello Primary Access Key or Secondary Access Key in hello Manage Keys blade.</span></span> <span data-ttu-id="f2624-204">De sleutel kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f2624-204">Either key can be used.</span></span>

<span data-ttu-id="f2624-205">Voor extra beveiliging Hallo toegang primaire en secundaire sleutels van een Automation-account op elk gewenst moment kunnen worden hersteld (op Hallo **sleutels beheren** blade) tooprevent toekomstige knooppunt registraties met vorige sleutels.</span><span class="sxs-lookup"><span data-stu-id="f2624-205">For added security, hello primary and secondary access keys of an Automation account can be regenerated at any time (on hello **Manage Keys** blade) tooprevent future node registrations using previous keys.</span></span>

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a><span data-ttu-id="f2624-206">Het voorbereiden van de virtuele machine van Azure oplossen</span><span class="sxs-lookup"><span data-stu-id="f2624-206">Troubleshooting Azure virtual machine onboarding</span></span>

<span data-ttu-id="f2624-207">Azure Automation DSC kunt u eenvoudig Azure Windows VM's vrijgeven voor Configuratiebeheer.</span><span class="sxs-lookup"><span data-stu-id="f2624-207">Azure Automation DSC lets you easily onboard Azure Windows VMs for configuration management.</span></span> <span data-ttu-id="f2624-208">Hallo Desired State Configuration van Azure VM-extensie is achter de schermen hello, gebruikte tooregister Hallo VM met Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="f2624-208">Under hello hood, hello Azure VM Desired State Configuration extension is used tooregister hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="f2624-209">Aangezien hello Azure VM Desired State Configuration-extensie wordt asynchroon uitgevoerd, kunnen de voortgang bijhouden en probleemoplossing van de uitvoering ervan belangrijk zijn.</span><span class="sxs-lookup"><span data-stu-id="f2624-209">Since hello Azure VM Desired State Configuration extension runs asynchronously, tracking its progress and troubleshooting its execution may be important.</span></span>

> [!NOTE]
> <span data-ttu-id="f2624-210">Een methode voor het voorbereiden op een tooAzure Windows virtuele machine in Azure Automation DSC die gebruikmaakt van hello Azure VM Desired State Configuration-extensie Hallo knooppunt tooshow up tooan uur duren kan als geregistreerd in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="f2624-210">Any method of onboarding an Azure Windows VM tooAzure Automation DSC that uses hello Azure VM Desired State Configuration extension could take up tooan hour for hello node tooshow up as registered in Azure Automation.</span></span> <span data-ttu-id="f2624-211">Dit is vanwege toohello installatie van Windows Management Framework 5.0 op Hallo VM door hello Azure VM DSC-extensie, die vereist tooonboard Hallo VM tooAzure Automation DSC is.</span><span class="sxs-lookup"><span data-stu-id="f2624-211">This is due toohello installation of Windows Management Framework 5.0 on hello VM by hello Azure VM DSC extension, which is required tooonboard hello VM tooAzure Automation DSC.</span></span>

<span data-ttu-id="f2624-212">tootroubleshoot of weergave Hallo-status van hello Azure VM Desired State Configuration extensie, hello Azure-portal navigeert toohello VM wordt vrijgegeven, vervolgens klikt u op -> **alle instellingen** -> **extensies**   ->  **DSC**.</span><span class="sxs-lookup"><span data-stu-id="f2624-212">tootroubleshoot or view hello status of hello Azure VM Desired State Configuration extension, in hello Azure portal navigate toohello VM being onboarded, then click -> **All settings** -> **Extensions** -> **DSC**.</span></span> <span data-ttu-id="f2624-213">Voor meer informatie kunt u **gedetailleerde status weergeven**.</span><span class="sxs-lookup"><span data-stu-id="f2624-213">For more details, you can click **View detailed status**.</span></span>

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a><span data-ttu-id="f2624-214">Vervaldatum van het certificaat en servernaam</span><span class="sxs-lookup"><span data-stu-id="f2624-214">Certificate expiration and reregistration</span></span>

<span data-ttu-id="f2624-215">Na de registratie van een machine als een DSC-knooppunt in Azure Automation DSC zijn er een aantal redenen waarom u tooreregister dat knooppunt in Hallo toekomstige wellicht:</span><span class="sxs-lookup"><span data-stu-id="f2624-215">After registering a machine as a DSC node in Azure Automation DSC, there are a number of reasons why you may need tooreregister that node in hello future:</span></span>

* <span data-ttu-id="f2624-216">Na de registratie wordt elk knooppunt automatisch onderhandeld over een uniek certificaat voor verificatie, die na één jaar verloopt.</span><span class="sxs-lookup"><span data-stu-id="f2624-216">After registering, each node automatically negotiates a unique certificate for authentication that expires after one year.</span></span> <span data-ttu-id="f2624-217">Hallo protocol voor PowerShell DSC-registratie kan niet op dit moment automatisch certificaten vernieuwen wanneer ze bijna zijn verlopen, zodat u tooreregister Hallo knooppunten een jaar later moet.</span><span class="sxs-lookup"><span data-stu-id="f2624-217">Currently, hello PowerShell DSC registration protocol cannot automatically renew certificates when they are nearing expiration, so you need tooreregister hello nodes after a year's time.</span></span> <span data-ttu-id="f2624-218">Voordat het opnieuw te registreren, moet u ervoor zorgen dat elk knooppunt wordt uitgevoerd op de Windows Management Framework 5.0 RTM.</span><span class="sxs-lookup"><span data-stu-id="f2624-218">Before reregistering, ensure that each node is running Windows Management Framework 5.0 RTM.</span></span> <span data-ttu-id="f2624-219">Als verificatiecertificaat van een knooppunt is verlopen en Hallo knooppunt niet is geregistreerd, Hallo knooppunt kan niet toocommunicate met Azure Automation en zal worden gemarkeerd als 'Unresponsive'.</span><span class="sxs-lookup"><span data-stu-id="f2624-219">If a node's authentication certificate expires, and hello node is not reregistered, hello node will be unable toocommunicate with Azure Automation and will be marked 'Unresponsive.'</span></span> <span data-ttu-id="f2624-220">Servernaam uitgevoerd 90 dagen of minder van certificaat de verlooptijd van Hallo of op elk gewenst moment na de verlooptijd van Hallo certificaat, resulteert in een nieuw certificaat wordt gegenereerd en gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f2624-220">Reregistration performed 90 days or less from hello certificate expiration time, or at any point after hello certificate expiration time, will result in a new certificate being generated and used.</span></span>
* <span data-ttu-id="f2624-221">toochange eventuele [PowerShell DSC Local Configuration Manager-waarden](https://msdn.microsoft.com/powershell/dsc/metaconfig4) die tijdens de initiële registratie van Hallo-knooppunt, zoals ConfigurationMode zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f2624-221">toochange any [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) that were set during initial registration of hello node, such as ConfigurationMode.</span></span> <span data-ttu-id="f2624-222">Deze waarden DSC-agent kunnen op dit moment alleen worden gewijzigd via servernaam.</span><span class="sxs-lookup"><span data-stu-id="f2624-222">Currently, these DSC agent values can only be changed through reregistration.</span></span> <span data-ttu-id="f2624-223">Hallo een uitzondering is Hallo toohello knooppunt toegewezen knooppuntconfiguratie--dit kan rechtstreeks worden gewijzigd in Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="f2624-223">hello one exception is hello Node Configuration assigned toohello node -- this can be changed in Azure Automation DSC directly.</span></span>

<span data-ttu-id="f2624-224">Servernaam kan worden uitgevoerd in Hallo dezelfde manier als u geregistreerd Hallo-knooppunt in eerste instantie met behulp van een Hallo onboarding methoden in dit document worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="f2624-224">Reregistration can be performed in hello same way you registered hello node initially, using any of hello onboarding methods described in this document.</span></span> <span data-ttu-id="f2624-225">U hoeft niet toounregister een knooppunt uit Azure Automation DSC voordat deze opnieuw te registreren.</span><span class="sxs-lookup"><span data-stu-id="f2624-225">You do not need toounregister a node from Azure Automation DSC before reregistering it.</span></span>

## <a name="related-articles"></a><span data-ttu-id="f2624-226">Verwante artikelen</span><span class="sxs-lookup"><span data-stu-id="f2624-226">Related Articles</span></span>

* [<span data-ttu-id="f2624-227">Overzicht van Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="f2624-227">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="f2624-228">Azure Automation DSC-cmdlets</span><span class="sxs-lookup"><span data-stu-id="f2624-228">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="f2624-229">Azure Automation DSC-prijzen</span><span class="sxs-lookup"><span data-stu-id="f2624-229">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)
