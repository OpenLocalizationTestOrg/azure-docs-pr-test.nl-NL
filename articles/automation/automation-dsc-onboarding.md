---
title: Computers voorbereiden voor beheer door Azure Automation DSC | Microsoft Docs
description: Het instellen van computers voor beheer met Azure Automation DSC
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
ms.openlocfilehash: cc9b1ea19b4e17374d47e12f970cb333a8051559
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a><span data-ttu-id="ad5a5-103">Computers voorbereiden voor beheer door Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="ad5a5-103">Onboarding machines for management by Azure Automation DSC</span></span>

## <a name="why-manage-machines-with-azure-automation-dsc"></a><span data-ttu-id="ad5a5-104">Waarom machines met een Azure Automation DSC beheren?</span><span class="sxs-lookup"><span data-stu-id="ad5a5-104">Why manage machines with Azure Automation DSC?</span></span>

<span data-ttu-id="ad5a5-105">Zoals [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is een eenvoudige maar krachtige, configuration management-service voor DSC-knooppunten (fysieke en virtuele machines) in een cloud of on-premises datacenter.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-105">Like [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is a simple, yet powerful, configuration management service for DSC nodes (physical and virtual machines) in any cloud or on-premises datacenter.</span></span> <span data-ttu-id="ad5a5-106">Hiermee kunt schaalbaarheid in duizenden computers snel en eenvoudig vanuit een centrale, veilige locatie.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-106">It enables scalability across thousands of machines quickly and easily from a central, secure location.</span></span> <span data-ttu-id="ad5a5-107">U kunt eenvoudig vrijgeven machines, toewijzen ze declaratieve configuraties en rapporten weergeven met elk van de computer de naleving van de gewenste status die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-107">You can easily onboard machines, assign them declarative configurations, and view reports showing each machine's compliance to the desired state you specified.</span></span> <span data-ttu-id="ad5a5-108">De Azure Automation DSC-beheerlaag is DSC wat het Azure Automation-beheerlaag is PowerShell-scripts.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-108">The Azure Automation DSC management layer is to DSC what the Azure Automation management layer is to PowerShell scripting.</span></span> <span data-ttu-id="ad5a5-109">Met andere woorden, op dezelfde manier die Azure Automation kunt u PowerShell-scripts beheren, kunt ook u de DSC-configuraties te beheren.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-109">In other words, in the same way that Azure Automation helps you manage PowerShell scripts, it also helps you manage DSC configurations.</span></span> <span data-ttu-id="ad5a5-110">Zie voor meer informatie over de voordelen van het gebruik van Azure Automation DSC, [overzicht van Azure Automation DSC](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ad5a5-110">To learn more about the benefits of using Azure Automation DSC, see [Azure Automation DSC overview](automation-dsc-overview.md).</span></span>

<span data-ttu-id="ad5a5-111">Azure Automation DSC kunnen worden gebruikt voor het beheren van tal van machines:</span><span class="sxs-lookup"><span data-stu-id="ad5a5-111">Azure Automation DSC can be used to manage a variety of machines:</span></span>

* <span data-ttu-id="ad5a5-112">Virtuele machines in Azure (klassiek)</span><span class="sxs-lookup"><span data-stu-id="ad5a5-112">Azure virtual machines (classic)</span></span>
* <span data-ttu-id="ad5a5-113">Virtuele machines van Azure</span><span class="sxs-lookup"><span data-stu-id="ad5a5-113">Azure virtual machines</span></span>
* <span data-ttu-id="ad5a5-114">Amazon Web Services (AWS) virtuele machines</span><span class="sxs-lookup"><span data-stu-id="ad5a5-114">Amazon Web Services (AWS) virtual machines</span></span>
* <span data-ttu-id="ad5a5-115">Fysiek virtueel Windows machines on-premises of in een cloud dan Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="ad5a5-115">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>
* <span data-ttu-id="ad5a5-116">Fysiek virtueel Linux-machines on-premises in Azure of in een cloud dan Azure</span><span class="sxs-lookup"><span data-stu-id="ad5a5-116">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="ad5a5-117">Bovendien, als u niet klaar voor het beheren van machineconfiguratie vanuit de cloud, kan Azure Automation DSC ook worden gebruikt als een eindpunt in het rapport alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-117">In addition, if you are not ready to manage machine configuration from the cloud, Azure Automation DSC can also be used as a report-only endpoint.</span></span> <span data-ttu-id="ad5a5-118">Hiermee kunt u de gewenste configuratie (push) via DSC on-premises instellen en uitgebreide rapportage details weergeven over de naleving van knooppunt met de gewenste status in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-118">This allows you to set (push) desired configuration through DSC on-premises and view rich reporting details on node compliance with the desired state in Azure Automation.</span></span>

<span data-ttu-id="ad5a5-119">De volgende secties worden hoe kunt u vrijgeven elk type van de machine aan Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-119">The following sections outline how you can onboard each type of machine to Azure Automation DSC.</span></span>

## <a name="azure-virtual-machines-classic"></a><span data-ttu-id="ad5a5-120">Virtuele machines in Azure (klassiek)</span><span class="sxs-lookup"><span data-stu-id="ad5a5-120">Azure virtual machines (classic)</span></span>

<span data-ttu-id="ad5a5-121">Met Azure Automation DSC kunt u eenvoudig vrijgeven virtuele machines in Azure (klassiek) voor het beheer van de configuratie met de Azure-portal of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-121">With Azure Automation DSC, you can easily onboard Azure virtual machines (classic) for configuration management using either the Azure portal, or PowerShell.</span></span> <span data-ttu-id="ad5a5-122">Achter de schermen en zonder een beheerder op afstand verbinding met de virtuele machine met de extensie Azure VM Desired State Configuration de virtuele machine geregistreerd bij Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-122">Under the hood, and without an administrator having to remote into the VM, the Azure VM Desired State Configuration extension registers the VM with Azure Automation DSC.</span></span> <span data-ttu-id="ad5a5-123">Omdat de extensie Azure VM Desired State Configuration asynchroon wordt uitgevoerd, stappen voor het bijhouden van de voortgang of het oplossen van dit probleem vindt u in de [ **probleemoplossing voor Azure virtuele machine voorbereiden** ](#troubleshooting-azure-virtual-machine-onboarding) hieronder.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-123">Since the Azure VM Desired State Configuration extension runs asynchronously, steps to track its progress or troubleshoot it are provided in the [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="ad5a5-124">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ad5a5-124">Azure portal</span></span>

<span data-ttu-id="ad5a5-125">In de [Azure-portal](http://portal.azure.com/), klikt u op **Bladeren** -> **virtuele machines (klassiek)**.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-125">In the [Azure portal](http://portal.azure.com/), click **Browse** -> **Virtual machines (classic)**.</span></span> <span data-ttu-id="ad5a5-126">Selecteer de Windows virtuele machine die u vrijgeven wilt.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-126">Select the Windows VM you want to onboard.</span></span> <span data-ttu-id="ad5a5-127">Klik op de virtuele machine dashboard blade **alle instellingen** -> **extensies** -> **toevoegen** -> **Azure Automation DSC** -> **maken**.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-127">On the virtual machine's dashboard blade, click **All settings** -> **Extensions** -> **Add** -> **Azure Automation DSC** -> **Create**.</span></span> <span data-ttu-id="ad5a5-128">Voer de [PowerShell DSC Local Configuration Manager-waarden](https://msdn.microsoft.com/powershell/dsc/metaconfig4) vereist is voor uw gebruiksvoorbeeld registratiecode voor uw Automation-account en registratie-URL en eventueel een knooppuntconfiguratie toewijzen aan de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-128">Enter the [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, your Automation account's registration key and registration URL, and optionally a node configuration to assign to the VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

<span data-ttu-id="ad5a5-129">De URL van de registratie van zoeken en sleutel voor het Automation-account om vrij te geven van de machine, Zie de [ **registratie Secure** ](#secure-registration) hieronder.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-129">To find the registration URL and key for the Automation account to onboard the machine to, see the [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="ad5a5-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad5a5-130">PowerShell</span></span>

```powershell
# log in to both Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in the name of a Node Configuration in Azure Automation DSC, for this VM to conform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use the DSC extension to onboard the VM for management with Azure Automation DSC
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

## <a name="azure-virtual-machines"></a><span data-ttu-id="ad5a5-131">Virtuele machines van Azure</span><span class="sxs-lookup"><span data-stu-id="ad5a5-131">Azure virtual machines</span></span>

<span data-ttu-id="ad5a5-132">Azure Automation DSC kunt u eenvoudig vrijgeven Azure virtuele machines voor Configuratiebeheer, via de Azure-portal, Azure Resource Manager-sjablonen of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-132">Azure Automation DSC lets you easily onboard Azure virtual machines for configuration management, using either the Azure portal, Azure Resource Manager templates, or PowerShell.</span></span> <span data-ttu-id="ad5a5-133">Achter de schermen en zonder een beheerder op afstand verbinding met de virtuele machine met de extensie Azure VM Desired State Configuration de virtuele machine geregistreerd bij Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-133">Under the hood, and without an administrator having to remote into the VM, the Azure VM Desired State Configuration extension registers the VM with Azure Automation DSC.</span></span> <span data-ttu-id="ad5a5-134">Omdat de extensie Azure VM Desired State Configuration asynchroon wordt uitgevoerd, stappen voor het bijhouden van de voortgang of het oplossen van dit probleem vindt u in de [ **probleemoplossing voor Azure virtuele machine voorbereiden** ](#troubleshooting-azure-virtual-machine-onboarding) hieronder.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-134">Since the Azure VM Desired State Configuration extension runs asynchronously, steps to track its progress or troubleshoot it are provided in the [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="ad5a5-135">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ad5a5-135">Azure portal</span></span>

<span data-ttu-id="ad5a5-136">In de [Azure-portal](https://portal.azure.com/), navigeer naar de Azure Automation-account waarin u vrijgeven virtuele machines wilt.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-136">In the [Azure portal](https://portal.azure.com/), navigate to the Azure Automation account where you want to onboard virtual machines.</span></span> <span data-ttu-id="ad5a5-137">Klik op het dashboard van Automation-account, **DSC-knooppunten** -> **toevoegen Azure VM**.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-137">On the Automation account dashboard, click **DSC Nodes** -> **Add Azure VM**.</span></span>

<span data-ttu-id="ad5a5-138">Onder **selecteert u virtuele machines om vrij te geven**, selecteer een of meer Azure virtual machines vrijgeven.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-138">Under **Select virtual machines to onboard**, select one or more Azure virtual machines to onboard.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

<span data-ttu-id="ad5a5-139">Onder **registratiegegevens configureren**, voer de [PowerShell DSC Local Configuration Manager-waarden](https://msdn.microsoft.com/powershell/dsc/metaconfig4) vereist is voor uw gebruiksvoorbeeld, en desgewenst een knooppuntconfiguratie toewijzen aan de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-139">Under **Configure registration data**, enter the [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, and optionally a node configuration to assign to the VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="ad5a5-140">Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="ad5a5-140">Azure Resource Manager templates</span></span>

<span data-ttu-id="ad5a5-141">Azure virtuele machines kunnen worden geïmplementeerd en vrijgegeven voor Azure Automation DSC via Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-141">Azure virtual machines can be deployed and onboarded to Azure Automation DSC via Azure Resource Manager templates.</span></span> <span data-ttu-id="ad5a5-142">Zie [configureren van een virtuele machine via de DSC-extensie en Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) voor een van de voorbeeldsjabloon die onboards een bestaande VM aan Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-142">See [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) for an example template that onboards an existing VM to Azure Automation DSC.</span></span> <span data-ttu-id="ad5a5-143">Zoeken naar de registratiecode en registratie-URL genomen als invoer in deze sjabloon, Zie de [ **registratie Secure** ](#secure-registration) hieronder.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-143">To find the registration key and registration URL taken as input in this template, see the [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="ad5a5-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad5a5-144">PowerShell</span></span>

<span data-ttu-id="ad5a5-145">De [registreren AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet kan worden gebruikt voor het vrijgeven van virtuele machines in de Azure portal via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-145">The [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet can be used to onboard virtual machines in the Azure portal via PowerShell.</span></span>

## <a name="amazon-web-services-aws-virtual-machines"></a><span data-ttu-id="ad5a5-146">Amazon Web Services (AWS) virtuele machines</span><span class="sxs-lookup"><span data-stu-id="ad5a5-146">Amazon Web Services (AWS) virtual machines</span></span>

<span data-ttu-id="ad5a5-147">U kunt eenvoudig vrijgeven Amazon Web Services virtuele machines voor Configuratiebeheer door Azure Automation DSC met behulp van de AWS DSC-Toolkit.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-147">You can easily onboard Amazon Web Services virtual machines for configuration management by Azure Automation DSC using the AWS DSC Toolkit.</span></span> <span data-ttu-id="ad5a5-148">U kunt meer informatie over de toolkit [hier](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span><span class="sxs-lookup"><span data-stu-id="ad5a5-148">You can learn more about the toolkit [here](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span></span>

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a><span data-ttu-id="ad5a5-149">Fysiek virtueel Windows machines on-premises of in een cloud dan Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="ad5a5-149">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>

<span data-ttu-id="ad5a5-150">Lokale Windows-machines en Windows-machines in niet-Azure-clouds (zoals Amazon Web Services) kunnen ook worden vrijgegeven aan Azure Automation DSC zolang ze beschikken over uitgaande toegang tot internet, via een paar eenvoudige stappen:</span><span class="sxs-lookup"><span data-stu-id="ad5a5-150">On-premises Windows machines and Windows machines in non-Azure clouds (such as Amazon Web Services) can also be onboarded to Azure Automation DSC, as long as they have outbound access to the internet, via a few simple steps:</span></span>

1. <span data-ttu-id="ad5a5-151">Zorg ervoor dat de nieuwste versie van [WMF 5](http://aka.ms/wmf5latest) is geïnstalleerd op de computers die u voorbereiden voor Azure Automation DSC wilt.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-151">Make sure the latest version of [WMF 5](http://aka.ms/wmf5latest) is installed on the machines you want to onboard to Azure Automation DSC.</span></span>
2. <span data-ttu-id="ad5a5-152">Volg de aanwijzingen in de sectie [ **genereren DSC metaconfigurations** ](#generating-dsc-metaconfigurations) hieronder voor het genereren van een map met de benodigde DSC-metaconfigurations.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-152">Follow the directions in section [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) below to generate a folder containing the needed DSC metaconfigurations.</span></span>
3. <span data-ttu-id="ad5a5-153">Van toepassing op afstand de PowerShell DSC-metaconfiguratie toe op de machines die u vrijgeven wilt.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-153">Remotely apply the PowerShell DSC metaconfiguration to the machines you want to onboard.</span></span> <span data-ttu-id="ad5a5-154">**De machine met deze opdracht wordt uitgevoerd vanaf moet hebben tot de nieuwste versie van [WMF 5](http://aka.ms/wmf5latest) geïnstalleerd**:</span><span class="sxs-lookup"><span data-stu-id="ad5a5-154">**The machine this command is run from must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed**:</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. <span data-ttu-id="ad5a5-155">Als u de PowerShell DSC-metaconfigurations op afstand niet toepassen, kopieert u de map metaconfigurations uit stap 2 op elke machine om vrij te geven.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-155">If you cannot apply the PowerShell DSC metaconfigurations remotely, copy the metaconfigurations folder from step 2 onto each machine to onboard.</span></span> <span data-ttu-id="ad5a5-156">Roep vervolgens **Set DscLocalConfigurationManager** lokaal op elke machine om vrij te geven.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-156">Then call **Set-DscLocalConfigurationManager** locally on each machine to onboard.</span></span>
5. <span data-ttu-id="ad5a5-157">Met behulp van de Azure-portal of cmdlets, Controleer of de machines om vrij te geven nu worden weergegeven als DSC-knooppunten die zijn geregistreerd in Azure Automation-account.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-157">Using the Azure portal or cmdlets, check that the machines to onboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a><span data-ttu-id="ad5a5-158">Fysiek virtueel Linux-machines on-premises in Azure of in een cloud dan Azure</span><span class="sxs-lookup"><span data-stu-id="ad5a5-158">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="ad5a5-159">Lokale Linux-machines, Linux-machines in Azure en Linux-machines in niet-Azure-clouds kunnen ook worden vrijgegeven aan Azure Automation DSC zolang ze beschikken over uitgaande toegang tot internet, via een paar eenvoudige stappen:</span><span class="sxs-lookup"><span data-stu-id="ad5a5-159">On-premises Linux machines, Linux machines in Azure, and Linux machines in non-Azure clouds can also be onboarded to Azure Automation DSC, as long as they have outbound access to the internet, via a few simple steps:</span></span>

1. <span data-ttu-id="ad5a5-160">Zorg ervoor dat de nieuwste versie van [PowerShell Desired State Configuration voor Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is geïnstalleerd op de computers die u voorbereiden voor Azure Automation DSC wilt.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-160">Make sure the latest version of [PowerShell Desired State Configuration for Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is installed on the machines you want to onboard to Azure Automation DSC.</span></span>
2. <span data-ttu-id="ad5a5-161">Als de [PowerShell DSC Local Configuration Manager standaardwaarden](https://msdn.microsoft.com/powershell/dsc/metaconfig4) overeenkomen met uw gebruiksvoorbeeld en u wilt vrijgeven machines zoals dat zij **beide** halen uit en te rapporteren aan Azure Automation DSC:</span><span class="sxs-lookup"><span data-stu-id="ad5a5-161">If the [PowerShell DSC Local Configuration Manager defaults](https://msdn.microsoft.com/powershell/dsc/metaconfig4) match your use case, and you want to onboard machines such that they **both** pull from and report to Azure Automation DSC:</span></span>

   + <span data-ttu-id="ad5a5-162">Gebruik op elke Linux-machine voor Onboarding van Azure Automation DSC, Register.py om vrij te geven met de standaardinstellingen voor PowerShell DSC Local Configuration Manager:</span><span class="sxs-lookup"><span data-stu-id="ad5a5-162">On each Linux machine to onboard to Azure Automation DSC, use Register.py to onboard using the PowerShell DSC Local Configuration Manager defaults:</span></span>

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + <span data-ttu-id="ad5a5-163">De registratiesleutel en de registratie-URL voor uw Automation-account, Zie de [ **registratie Secure** ](#secure-registration) hieronder.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-163">To find the registration key and registration URL for your Automation account, see the [**Secure registration**](#secure-registration) section below.</span></span>

     <span data-ttu-id="ad5a5-164">Als de standaardwaarden van de PowerShell DSC Local Configuration Manager **doen** **niet** overeen uw gebruiksvoorbeeld, of u voorbereiden wilt, zodat ze alleen aan Azure Automation DSC rapporteren machines maar geen pull-configuratie of het PowerShell-modules doen vanuit het, volgt u stap 3-6.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-164">If the PowerShell DSC Local Configuration Manager defaults **do** **not** match your use case, or you want to onboard machines such that they only report to Azure Automation DSC, but do not pull configuration or PowerShell modules from it,  follow steps 3 - 6.</span></span> <span data-ttu-id="ad5a5-165">Ga anders verder met stap 6 rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-165">Otherwise, proceed directly to step 6.</span></span>

3. <span data-ttu-id="ad5a5-166">Volg de aanwijzingen in de [ **genereren DSC metaconfigurations** ](#generating-dsc-metaconfigurations) hieronder voor het genereren van een map met de benodigde DSC-metaconfigurations.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-166">Follow the directions in the [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) section below to generate a folder containing the needed DSC metaconfigurations.</span></span>
4. <span data-ttu-id="ad5a5-167">Van toepassing op afstand de PowerShell DSC-metaconfiguratie toe op de machines die u vrijgeven wilt:</span><span class="sxs-lookup"><span data-stu-id="ad5a5-167">Remotely apply the PowerShell DSC metaconfiguration to the machines you want to onboard:</span></span>

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine to onboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

<span data-ttu-id="ad5a5-168">De machine met deze opdracht wordt uitgevoerd vanaf moet hebben tot de nieuwste versie van [WMF 5](http://aka.ms/wmf5latest) geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-168">The machine this command is run from must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>

1. <span data-ttu-id="ad5a5-169">Als u de PowerShell DSC-metaconfigurations op afstand niet voor elke Linux-machine om vrij te geven toepassen, kopieert u de metaconfiguratie toe die overeenkomt met die machine uit de map die u in stap 5 naar de Linux-machine.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-169">If you cannot apply the PowerShell DSC metaconfigurations remotely, for each Linux machine to onboard, copy the metaconfiguration corresponding to that machine from the folder in step 5 onto the Linux machine.</span></span> <span data-ttu-id="ad5a5-170">Roep vervolgens `SetDscLocalConfigurationManager.py` lokaal op elke Linux-machine u wilt voorbereiden voor Azure Automation DSC:</span><span class="sxs-lookup"><span data-stu-id="ad5a5-170">Then call `SetDscLocalConfigurationManager.py` locally on each Linux machine you want to onboard to Azure Automation DSC:</span></span>

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path to metaconfiguration file>`

2. <span data-ttu-id="ad5a5-171">Met behulp van de Azure-portal of cmdlets, Controleer of de machines om vrij te geven nu worden weergegeven als DSC-knooppunten die zijn geregistreerd in Azure Automation-account.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-171">Using the Azure portal or cmdlets, check that the machines to onboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="generating-dsc-metaconfigurations"></a><span data-ttu-id="ad5a5-172">DSC-metaconfigurations genereren</span><span class="sxs-lookup"><span data-stu-id="ad5a5-172">Generating DSC metaconfigurations</span></span>

<span data-ttu-id="ad5a5-173">Om vrij te algemeen geven een aan Azure Automation DSC machine een [DSC-metaconfiguratie toe](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) kan worden gegenereerd dat, wanneer toegepast, wordt uitgelegd van de DSC-agent op de machine op te halen uit en/of rapporteren aan Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-173">To generically onboard any machine to Azure Automation DSC, a [DSC metaconfiguration](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) can be generated that, when applied, tells the DSC agent on the machine to pull from and/or report to Azure Automation DSC.</span></span> <span data-ttu-id="ad5a5-174">DSC-metaconfigurations voor Azure Automation DSC kan worden gegenereerd met behulp van een PowerShell DSC-configuratie of de Azure Automation PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-174">DSC metaconfigurations for Azure Automation DSC can be generated using either a PowerShell DSC configuration, or the Azure Automation PowerShell cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="ad5a5-175">DSC-metaconfigurations bevatten de geheimen die nodig zijn om vrij te geven een machine naar een Automation-account voor beheer.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-175">DSC metaconfigurations contain the secrets needed to onboard a machine to an Automation account for management.</span></span> <span data-ttu-id="ad5a5-176">Zorg ervoor dat u goed beveiligen eventuele DSC-metaconfigurations die u maakt of verwijder ze na gebruik.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-176">Make sure to properly protect any DSC metaconfigurations you create, or delete them after use.</span></span>

### <a name="using-a-dsc-configuration"></a><span data-ttu-id="ad5a5-177">Met behulp van een DSC-configuratie</span><span class="sxs-lookup"><span data-stu-id="ad5a5-177">Using a DSC Configuration</span></span>

1. <span data-ttu-id="ad5a5-178">Open de PowerShell ISE als beheerder op een virtuele machine in uw lokale omgeving.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-178">Open the PowerShell ISE as an administrator in a machine in your local environment.</span></span> <span data-ttu-id="ad5a5-179">De machine moet hebben tot de nieuwste versie van [WMF 5](http://aka.ms/wmf5latest) geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-179">The machine must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>
2. <span data-ttu-id="ad5a5-180">Kopieer het volgende script lokaal.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-180">Copy the following script locally.</span></span> <span data-ttu-id="ad5a5-181">Dit script bevat een PowerShell DSC-configuratie voor het maken van metaconfigurations en een opdracht voor het maken van de metaconfiguratie starten.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-181">This script contains a PowerShell DSC configuration for creating metaconfigurations, and a command to kick off the metaconfiguration creation.</span></span>

    ```powershell
    # The DSC configuration that will generate metaconfigurations
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

    # Create the metaconfigurations
    # TODO: edit the below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM to onboard>', '<some other VM to onboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set to $True to have machines only report to AA DSC but not pull from it
    }

    # Use PowerShell splatting to pass parameters to the DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. <span data-ttu-id="ad5a5-182">Vul de registratiecode en de URL in voor uw Automation-account, evenals de namen van de machines om vrij te geven.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-182">Fill in the registration key and URL for your Automation account, as well as the names of the machines to onboard.</span></span> <span data-ttu-id="ad5a5-183">Alle andere parameters zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-183">All other parameters are optional.</span></span> <span data-ttu-id="ad5a5-184">De registratiesleutel en de registratie-URL voor uw Automation-account, Zie de [ **registratie Secure** ](#secure-registration) hieronder.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-184">To find the registration key and registration URL for your Automation account, see the [**Secure registration**](#secure-registration) section below.</span></span>
4. <span data-ttu-id="ad5a5-185">Als u wilt dat de machines DSC-statusinformatie rapporteren aan Azure Automation DSC, maar geen pull-configuratie of PowerShell-modules, stelt u de **ReportOnly** parameter in op true.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-185">If you want the machines to report DSC status information to Azure Automation DSC, but not pull configuration or PowerShell modules, set the **ReportOnly** parameter to true.</span></span>
5. <span data-ttu-id="ad5a5-186">Voer het script.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-186">Run the script.</span></span> <span data-ttu-id="ad5a5-187">U hebt nu een map met de naam **DscMetaConfigs** die in uw werkmap, bevat de PowerShell DSC-metaconfigurations voor de machines voorbereiden (als administrator):</span><span class="sxs-lookup"><span data-stu-id="ad5a5-187">You should now have a folder called **DscMetaConfigs** in your working directory, containing the PowerShell DSC metaconfigurations for the machines to onboard (as an administrator):</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-the-azure-automation-cmdlets"></a><span data-ttu-id="ad5a5-188">Azure Automation-cmdlets gebruiken</span><span class="sxs-lookup"><span data-stu-id="ad5a5-188">Using the Azure Automation cmdlets</span></span>

<span data-ttu-id="ad5a5-189">Als de PowerShell DSC Local Configuration Manager-standaardwaarden overeenkomen met uw gebruiksvoorbeeld en u vrijgeven machines wilt zo dat ze zowel pull van en aan Azure Automation DSC rapporteren, bieden de cmdlets van Azure Automation een vereenvoudigde methode voor het genereren van de DSC-metaconfigurations nodig:</span><span class="sxs-lookup"><span data-stu-id="ad5a5-189">If the PowerShell DSC Local Configuration Manager defaults match your use case, and you want to onboard machines such that they both pull from and report to Azure Automation DSC, the Azure Automation cmdlets provide a simplified method of generating the DSC metaconfigurations needed:</span></span>

1. <span data-ttu-id="ad5a5-190">Open de PowerShell-console of PowerShell ISE als beheerder op een virtuele machine in uw lokale omgeving.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-190">Open the PowerShell console or PowerShell ISE as an administrator in a machine in your local environment.</span></span>
2. <span data-ttu-id="ad5a5-191">Verbinding maken met behulp van Azure Resource Manager **Add-AzureRmAccount**</span><span class="sxs-lookup"><span data-stu-id="ad5a5-191">Connect to Azure Resource Manager using **Add-AzureRmAccount**</span></span>
3. <span data-ttu-id="ad5a5-192">De PowerShell DSC-metaconfigurations voor de machines die u wilt downloaden om vrij te geven van het Automation-account die u vrijgeven knooppunten wilt:</span><span class="sxs-lookup"><span data-stu-id="ad5a5-192">Download the PowerShell DSC metaconfigurations for the machines you want to onboard from the Automation account to which you want to onboard nodes:</span></span>

    ```powershell
    # Define the parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # The name of the ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # The name of the Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # The names of the computers that the meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting to pass parameters to the Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. <span data-ttu-id="ad5a5-193">U hebt nu een map met de naam ***DscMetaConfigs***, met de PowerShell DSC-metaconfigurations voor de machines voorbereiden (als administrator):</span><span class="sxs-lookup"><span data-stu-id="ad5a5-193">You should now have a folder called ***DscMetaConfigs***, containing the PowerShell DSC metaconfigurations for the machines to onboard (as an administrator):</span></span>
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a><span data-ttu-id="ad5a5-194">Beveiligde registratie</span><span class="sxs-lookup"><span data-stu-id="ad5a5-194">Secure registration</span></span>

<span data-ttu-id="ad5a5-195">Machines kunnen veilig vrijgeven aan een Azure Automation-account via het protocol WMF 5 DSC-registratie, waardoor een DSC-knooppunt om een Pull-PowerShell DSC V2 of Reporting server (met inbegrip van Azure Automation DSC) te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-195">Machines can securely onboard to an Azure Automation account through the WMF 5 DSC registration protocol, which allows a DSC node to authenticate to a PowerShell DSC V2 Pull or Reporting server (including Azure Automation DSC).</span></span> <span data-ttu-id="ad5a5-196">Het knooppunt wordt geregistreerd met de server op een **registratie URL**, verificatie uitvoert met behulp van een **registratiesleutel**.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-196">The node registers to the server at a **Registration URL**, authenticating using a **Registration key**.</span></span> <span data-ttu-id="ad5a5-197">Tijdens de registratie, de DSC-knooppunt en DSC-Pull/Reporting-server om te onderhandelen over een uniek certificaat voor dit knooppunt wilt gebruiken voor verificatie op de na serverregistratie.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-197">During registration, the DSC node and DSC Pull/Reporting server negotiate a unique certificate for this node to use for authentication to the server post-registration.</span></span> <span data-ttu-id="ad5a5-198">Dit proces wordt voorkomen dat de knooppunten van imitatie van een die andere, zoals wanneer een knooppunt is geknoeid en gedragen met kwaadaardige bedoelingen vrijgegeven.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-198">This process prevents onboarded nodes from impersonating one another, such as if a node is compromised and behaving maliciously.</span></span> <span data-ttu-id="ad5a5-199">Na de registratie, de registratiesleutel wordt niet gebruikt voor verificatie opnieuw en wordt verwijderd uit het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-199">After registration, the Registration key is not used for authentication again, and is deleted from the node.</span></span>

<span data-ttu-id="ad5a5-200">U kunt de vereiste informatie voor het protocol van de DSC-registratie van de **sleutels beheren** blade in de Azure preview portal.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-200">You can get the information required for the DSC registration protocol from the **Manage Keys** blade in the Azure preview portal.</span></span> <span data-ttu-id="ad5a5-201">Deze blade openen door te klikken op het sleutelpictogram op de **Essentials** Configuratiescherm voor het Automation-account.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-201">Open this blade by clicking the key icon on the **Essentials** panel for the Automation account.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* <span data-ttu-id="ad5a5-202">Registratie-URL is het veld URL in de blade sleutels beheren.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-202">Registration URL is the URL field in the Manage Keys blade.</span></span>
* <span data-ttu-id="ad5a5-203">Registratiecode is de primaire toegangssleutel of de secundaire toegangssleutel op de blade sleutels beheren.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-203">Registration key is the Primary Access Key or Secondary Access Key in the Manage Keys blade.</span></span> <span data-ttu-id="ad5a5-204">De sleutel kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-204">Either key can be used.</span></span>

<span data-ttu-id="ad5a5-205">Voor extra beveiliging, de primaire en secundaire toegangssleutel van een Automation-account op elk gewenst moment kunnen worden hersteld (op het **sleutels beheren** blade) om te voorkomen dat toekomstige knooppunt registraties met vorige sleutels.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-205">For added security, the primary and secondary access keys of an Automation account can be regenerated at any time (on the **Manage Keys** blade) to prevent future node registrations using previous keys.</span></span>

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a><span data-ttu-id="ad5a5-206">Het voorbereiden van de virtuele machine van Azure oplossen</span><span class="sxs-lookup"><span data-stu-id="ad5a5-206">Troubleshooting Azure virtual machine onboarding</span></span>

<span data-ttu-id="ad5a5-207">Azure Automation DSC kunt u eenvoudig Azure Windows VM's vrijgeven voor Configuratiebeheer.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-207">Azure Automation DSC lets you easily onboard Azure Windows VMs for configuration management.</span></span> <span data-ttu-id="ad5a5-208">De extensie Azure VM Desired State Configuration wordt achter de schermen gebruikt voor het registreren van de virtuele machine met Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-208">Under the hood, the Azure VM Desired State Configuration extension is used to register the VM with Azure Automation DSC.</span></span> <span data-ttu-id="ad5a5-209">Omdat de extensie Azure VM Desired State Configuration asynchroon wordt uitgevoerd, kunnen de voortgang bijhouden en probleemoplossing van de uitvoering ervan belangrijk zijn.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-209">Since the Azure VM Desired State Configuration extension runs asynchronously, tracking its progress and troubleshooting its execution may be important.</span></span>

> [!NOTE]
> <span data-ttu-id="ad5a5-210">Een voorbereiden op een Windows Azure VM aan Azure Automation DSC die gebruikmaakt van de extensie Azure VM Desired State Configuration-methode kan een uur duren voor het knooppunt om maximaal geregistreerd in Azure Automation weer te geven.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-210">Any method of onboarding an Azure Windows VM to Azure Automation DSC that uses the Azure VM Desired State Configuration extension could take up to an hour for the node to show up as registered in Azure Automation.</span></span> <span data-ttu-id="ad5a5-211">Dit wordt veroorzaakt door de installatie van Windows Management Framework 5.0 op de virtuele machine voor de Azure VM DSC-uitbreiding vereist om vrij te geven is de VM naar Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-211">This is due to the installation of Windows Management Framework 5.0 on the VM by the Azure VM DSC extension, which is required to onboard the VM to Azure Automation DSC.</span></span>

<span data-ttu-id="ad5a5-212">Voor probleemoplossing of weer de status van de Azure VM Desired State Configuration-uitbreiding in de Azure portal gaat u naar de virtuele machine wordt vrijgegeven en vervolgens klik -> **alle instellingen** -> **extensies** -> **DSC**.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-212">To troubleshoot or view the status of the Azure VM Desired State Configuration extension, in the Azure portal navigate to the VM being onboarded, then click -> **All settings** -> **Extensions** -> **DSC**.</span></span> <span data-ttu-id="ad5a5-213">Voor meer informatie kunt u **gedetailleerde status weergeven**.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-213">For more details, you can click **View detailed status**.</span></span>

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a><span data-ttu-id="ad5a5-214">Vervaldatum van het certificaat en servernaam</span><span class="sxs-lookup"><span data-stu-id="ad5a5-214">Certificate expiration and reregistration</span></span>

<span data-ttu-id="ad5a5-215">Na de registratie van een machine als een DSC-knooppunt in Azure Automation DSC zijn er een aantal redenen waarom u wellicht dat knooppunt in de toekomst opnieuw registreren:</span><span class="sxs-lookup"><span data-stu-id="ad5a5-215">After registering a machine as a DSC node in Azure Automation DSC, there are a number of reasons why you may need to reregister that node in the future:</span></span>

* <span data-ttu-id="ad5a5-216">Na de registratie wordt elk knooppunt automatisch onderhandeld over een uniek certificaat voor verificatie, die na één jaar verloopt.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-216">After registering, each node automatically negotiates a unique certificate for authentication that expires after one year.</span></span> <span data-ttu-id="ad5a5-217">Het protocol PowerShell DSC-registratie kan niet op dit moment automatisch certificaten vernieuwen wanneer ze bijna zijn verlopen, dus moet u de knooppunten van een jaar later opnieuw te registreren.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-217">Currently, the PowerShell DSC registration protocol cannot automatically renew certificates when they are nearing expiration, so you need to reregister the nodes after a year's time.</span></span> <span data-ttu-id="ad5a5-218">Voordat het opnieuw te registreren, moet u ervoor zorgen dat elk knooppunt wordt uitgevoerd op de Windows Management Framework 5.0 RTM.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-218">Before reregistering, ensure that each node is running Windows Management Framework 5.0 RTM.</span></span> <span data-ttu-id="ad5a5-219">Als het verificatiecertificaat van een knooppunt is verlopen en het knooppunt niet is geregistreerd, het knooppunt kan niet communiceren met Azure Automation en zal worden gemarkeerd als 'Unresponsive'.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-219">If a node's authentication certificate expires, and the node is not reregistered, the node will be unable to communicate with Azure Automation and will be marked 'Unresponsive.'</span></span> <span data-ttu-id="ad5a5-220">Servernaam uitgevoerd 90 dagen of minder van de verlooptijd van het certificaat, of op elk gewenst moment na de verlooptijd certificaat resulteert in een nieuw certificaat wordt gegenereerd en gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-220">Reregistration performed 90 days or less from the certificate expiration time, or at any point after the certificate expiration time, will result in a new certificate being generated and used.</span></span>
* <span data-ttu-id="ad5a5-221">Niet te wijzigen [PowerShell DSC Local Configuration Manager-waarden](https://msdn.microsoft.com/powershell/dsc/metaconfig4) die tijdens de initiële registratie van het knooppunt, zoals ConfigurationMode zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-221">To change any [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) that were set during initial registration of the node, such as ConfigurationMode.</span></span> <span data-ttu-id="ad5a5-222">Deze waarden DSC-agent kunnen op dit moment alleen worden gewijzigd via servernaam.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-222">Currently, these DSC agent values can only be changed through reregistration.</span></span> <span data-ttu-id="ad5a5-223">De enige uitzondering hierop is de toegewezen aan het knooppunt knooppuntconfiguratie--dit kan rechtstreeks worden gewijzigd in Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-223">The one exception is the Node Configuration assigned to the node -- this can be changed in Azure Automation DSC directly.</span></span>

<span data-ttu-id="ad5a5-224">Servernaam kan worden uitgevoerd op dezelfde manier als die u geregistreerd het knooppunt in eerste instantie met een van de voorbereiding-methoden die in dit document worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-224">Reregistration can be performed in the same way you registered the node initially, using any of the onboarding methods described in this document.</span></span> <span data-ttu-id="ad5a5-225">U hoeft niet de registratie van een knooppunt uit Azure Automation DSC voordat deze opnieuw te registreren.</span><span class="sxs-lookup"><span data-stu-id="ad5a5-225">You do not need to unregister a node from Azure Automation DSC before reregistering it.</span></span>

## <a name="related-articles"></a><span data-ttu-id="ad5a5-226">Verwante artikelen</span><span class="sxs-lookup"><span data-stu-id="ad5a5-226">Related Articles</span></span>

* [<span data-ttu-id="ad5a5-227">Overzicht van Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="ad5a5-227">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="ad5a5-228">Azure Automation DSC-cmdlets</span><span class="sxs-lookup"><span data-stu-id="ad5a5-228">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="ad5a5-229">Azure Automation DSC-prijzen</span><span class="sxs-lookup"><span data-stu-id="ad5a5-229">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)
