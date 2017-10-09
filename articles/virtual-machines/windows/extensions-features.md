---
title: aaaVirtual machine extensies en functies voor Windows in Azure | Microsoft Docs
description: Meer informatie over welke extensies beschikbaar zijn voor virtuele machines in Azure, gegroepeerd op wat ze bieden of verbeteren.
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 999d63ee-890e-432e-9391-25b3fc6cde28
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/06/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 61ccfd696b38e9be1026d836d5796c2346fd650f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a><span data-ttu-id="e53ac-103">Virtuele machine-extensies en functies voor Windows</span><span class="sxs-lookup"><span data-stu-id="e53ac-103">Virtual machine extensions and features for Windows</span></span>

<span data-ttu-id="e53ac-104">Virtuele machine van Azure-extensies zijn kleine toepassingen waarmee de configuratie en automatisering taken na de implementatie op virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="e53ac-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="e53ac-105">Als een virtuele machine vereist een software-installatie, beveiliging tegen virussen of Docker-configuratie, een VM-extensie kan bijvoorbeeld worden gebruikt toocomplete deze taken.</span><span class="sxs-lookup"><span data-stu-id="e53ac-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used toocomplete these tasks.</span></span> <span data-ttu-id="e53ac-106">Azure VM-extensies kunnen worden uitgevoerd met behulp van hello Azure CLI, Azure Resource Manager-sjablonen, PowerShell en hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e53ac-106">Azure VM extensions can be run by using hello Azure CLI, PowerShell, Azure Resource Manager templates, and hello Azure portal.</span></span> <span data-ttu-id="e53ac-107">Uitbreidingen worden gebundeld met een nieuwe implementatie van de virtuele machine of eventuele bestaande systeem uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e53ac-107">Extensions can be bundled with a new virtual machine deployment or run against any existing system.</span></span>

<span data-ttu-id="e53ac-108">Dit document bevat een overzicht van de virtuele machine-extensies vereisten voor het gebruik van uitbreidingen van de virtuele machine en richtlijnen over hoe toodetect, beheren en uitbreidingen van de virtuele machine verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e53ac-108">This document provides an overview of virtual machine extensions, prerequisites for using virtual machine extensions, and guidance on how toodetect, manage, and remove virtual machine extensions.</span></span> <span data-ttu-id="e53ac-109">Dit document vindt u algemene informatie omdat veel VM-extensies beschikbaar zijn, elk met een potentieel unieke configuratie.</span><span class="sxs-lookup"><span data-stu-id="e53ac-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="e53ac-110">Extensie-specifieke informatie vindt u in elke afzonderlijke document specifieke toohello-extensie.</span><span class="sxs-lookup"><span data-stu-id="e53ac-110">Extension-specific details can be found in each document specific toohello individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="e53ac-111">Gebruiksvoorbeelden en voorbeelden</span><span class="sxs-lookup"><span data-stu-id="e53ac-111">Use cases and samples</span></span>

<span data-ttu-id="e53ac-112">Er zijn veel verschillende Azure VM-extensies beschikbaar, elk met een specifieke aanvraag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e53ac-112">There are many different Azure VM extensions available, each with a specific use case.</span></span> <span data-ttu-id="e53ac-113">Er zijn enkele gebruiksvoorbeelden:</span><span class="sxs-lookup"><span data-stu-id="e53ac-113">Some example use cases are:</span></span>

- <span data-ttu-id="e53ac-114">Virtuele machine met PowerShell gewenst status configuraties tooa toepassen door middel van Hallo DSC-uitbreiding voor Windows.</span><span class="sxs-lookup"><span data-stu-id="e53ac-114">Apply PowerShell Desired State configurations tooa virtual machine by using hello DSC extension for Windows.</span></span> <span data-ttu-id="e53ac-115">Zie voor meer informatie [Azure gewenst State configuration-uitbreiding](extensions-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e53ac-115">For more information, see [Azure Desired State configuration extension](extensions-dsc-overview.md).</span></span>
- <span data-ttu-id="e53ac-116">Virtuele machine met behulp van Microsoft Monitoring Agent VM-extensie Hallo controle configureren</span><span class="sxs-lookup"><span data-stu-id="e53ac-116">Configure virtual machine monitoring by using hello Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="e53ac-117">Zie voor meer informatie [verbinding maken met Azure virtuele machines tooLog Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="e53ac-117">For more information, see [Connect Azure virtual machines tooLog Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="e53ac-118">Bewaking van uw Azure-infrastructuur met Hallo Datadog-uitbreiding configureren.</span><span class="sxs-lookup"><span data-stu-id="e53ac-118">Configure monitoring of your Azure infrastructure with hello Datadog extension.</span></span> <span data-ttu-id="e53ac-119">Zie voor meer informatie, Hallo [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="e53ac-119">For more information, see hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="e53ac-120">Een virtuele machine van Azure met behulp van Chef configureren.</span><span class="sxs-lookup"><span data-stu-id="e53ac-120">Configure an Azure virtual machine by using Chef.</span></span> <span data-ttu-id="e53ac-121">Zie voor meer informatie [Azure automatisering van de implementatie van de virtuele machine met Chef](chef-automation.md).</span><span class="sxs-lookup"><span data-stu-id="e53ac-121">For more information, see [Automating Azure virtual machine deployment with Chef](chef-automation.md).</span></span>

<span data-ttu-id="e53ac-122">Bovendien tooprocess-specifieke uitbreidingen, een extensie voor aangepaste scripts is beschikbaar voor Windows- en Linux virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="e53ac-122">In addition tooprocess-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="e53ac-123">Hallo-extensie voor aangepaste scripts voor Windows kunt een PowerShell-script toobe uitvoeren op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e53ac-123">hello Custom Script extension for Windows allows any PowerShell script toobe run on a virtual machine.</span></span> <span data-ttu-id="e53ac-124">Dit is handig bij het ontwerpen van Azure-implementaties die moeten worden geconfigureerd afgezien van wat systeemeigen Azure tooling kan bieden.</span><span class="sxs-lookup"><span data-stu-id="e53ac-124">This is useful when you're designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="e53ac-125">Zie voor meer informatie [Windows VM aangepaste scriptextensie](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="e53ac-125">For more information, see [Windows VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e53ac-126">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e53ac-126">Prerequisites</span></span>

<span data-ttu-id="e53ac-127">De extensie van elke virtuele machine mogelijk een eigen set vereisten.</span><span class="sxs-lookup"><span data-stu-id="e53ac-127">Each virtual machine extension may have its own set of prerequisites.</span></span> <span data-ttu-id="e53ac-128">Hallo Docker VM-extensie heeft bijvoorbeeld een vereiste van een ondersteunde Linux-distributie.</span><span class="sxs-lookup"><span data-stu-id="e53ac-128">For instance, hello Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="e53ac-129">Vereisten van afzonderlijke uitbreidingen zijn aangegeven in het Hallo-extensie-specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="e53ac-129">Requirements of individual extensions are detailed in hello extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="e53ac-130">Azure VM-agent</span><span class="sxs-lookup"><span data-stu-id="e53ac-130">Azure VM agent</span></span>
<span data-ttu-id="e53ac-131">Hello Azure VM-agent beheert interactie tussen een virtuele machine van Azure en hello Azure-infrastructuurcontroller.</span><span class="sxs-lookup"><span data-stu-id="e53ac-131">hello Azure VM agent manages interaction between an Azure virtual machine and hello Azure fabric controller.</span></span> <span data-ttu-id="e53ac-132">Hallo VM-agent is verantwoordelijk voor veel functionele aspecten van het implementeren en beheren van virtuele machines in Azure, waaronder het uitvoeren van de VM-extensies.</span><span class="sxs-lookup"><span data-stu-id="e53ac-132">hello VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="e53ac-133">Hello Azure VM-agent is geïnstalleerd op Azure Marketplace-installatiekopieën en kan worden geïnstalleerd op ondersteunde besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="e53ac-133">hello Azure VM agent is preinstalled on Azure Marketplace images and can be installed on supported operating systems.</span></span>

<span data-ttu-id="e53ac-134">Zie voor informatie over ondersteunde besturingssystemen en installatie-instructies, [virtuele machine van Azure-agent](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="e53ac-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](agent-user-guide.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="e53ac-135">VM-extensies detecteren</span><span class="sxs-lookup"><span data-stu-id="e53ac-135">Discover VM extensions</span></span>
<span data-ttu-id="e53ac-136">Veel andere VM-extensies zijn beschikbaar voor gebruik met virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="e53ac-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="e53ac-137">toosee een volledige lijst Hallo volgende opdracht met hello Azure Resource Manager PowerShell-module worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e53ac-137">toosee a complete list, run hello following command with hello Azure Resource Manager PowerShell module.</span></span> <span data-ttu-id="e53ac-138">Zorg ervoor dat toospecify Hallo gewenste locatie wanneer u deze opdracht uitvoert.</span><span class="sxs-lookup"><span data-stu-id="e53ac-138">Make sure toospecify hello desired location when you're running this command.</span></span>

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a><span data-ttu-id="e53ac-139">VM-extensies worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="e53ac-139">Run VM extensions</span></span>

<span data-ttu-id="e53ac-140">Uitbreidingen van de virtuele machine van Azure kunnen worden uitgevoerd op een bestaande virtuele machines die is handig als u de verbinding op een reeds geïmplementeerde virtuele machine herstellen of toomake configuratiewijzigingen nodig.</span><span class="sxs-lookup"><span data-stu-id="e53ac-140">Azure virtual machine extensions can be run on existing virtual machines, which is useful when you need toomake configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="e53ac-141">VM-extensies kunnen ook worden gebundeld met implementaties van Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e53ac-141">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="e53ac-142">Via uitbreidingen met Resource Manager-sjablonen kunt u virtuele machines in Azure toobe geïmplementeerd en geconfigureerd zonder dat tussenkomst van de na de implementatie Hallo inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e53ac-142">By using extensions with Resource Manager templates, you can enable Azure virtual machines toobe deployed and configured without hello need for post-deployment intervention.</span></span>

<span data-ttu-id="e53ac-143">Hallo volgende methoden kan worden gebruikt toorun een uitbreiding op basis van een bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e53ac-143">hello following methods can be used toorun an extension against an existing virtual machine.</span></span>

### <a name="powershell"></a><span data-ttu-id="e53ac-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e53ac-144">PowerShell</span></span>

<span data-ttu-id="e53ac-145">Er bestaan verschillende PowerShell-opdrachten voor het uitvoeren van afzonderlijke uitbreidingen.</span><span class="sxs-lookup"><span data-stu-id="e53ac-145">Several PowerShell commands exist for running individual extensions.</span></span> <span data-ttu-id="e53ac-146">toosee een lijst Hallo volgende PowerShell-opdrachten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e53ac-146">toosee a list, run hello following PowerShell commands.</span></span>

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

<span data-ttu-id="e53ac-147">Dit biedt soortgelijke toohello-volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e53ac-147">This provides output similar toohello following:</span></span>

```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Set-AzureRmVMAccessExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMADDomainExtension                     2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMAEMExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBackupExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBginfoExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMChefExtension                         2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMCustomScriptExtension                 2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiagnosticsExtension                  2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiskEncryptionExtension               2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDscExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMExtension                             2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMSqlServerExtension                    2.2.0      AzureRM.Compute
```

<span data-ttu-id="e53ac-148">Hallo volgende voorbeeld wordt Hallo aangepast Script extensie toodownload een script van een GitHub-opslagplaats op Hallo doel-virtuele machine en vervolgens Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e53ac-148">hello following example uses hello Custom Script extension toodownload a script from a GitHub repository onto hello target virtual machine and then run hello script.</span></span> <span data-ttu-id="e53ac-149">Zie voor meer informatie over Hallo extensie voor aangepaste scripts [extensieoverzicht aangepast Script](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="e53ac-149">For more information on hello Custom Script extension, see [Custom Script extension overview](extensions-customscript.md).</span></span>

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

<span data-ttu-id="e53ac-150">In dit voorbeeld is Hallo uitbreiding voor toegang tot VM gebruikte tooreset Hallo beheerderswachtwoord van een virtuele machine van Windows.</span><span class="sxs-lookup"><span data-stu-id="e53ac-150">In this example, hello VM Access extension is used tooreset hello administrative password of a Windows virtual machine.</span></span> <span data-ttu-id="e53ac-151">Zie voor meer informatie over Hallo uitbreiding voor toegang tot VM [opnieuw instellen van extern bureaublad-service in een Windows-VM](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="e53ac-151">For more information on hello VM Access extension, see [Reset Remote Desktop service in a Windows VM](reset-rdp.md).</span></span>

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

<span data-ttu-id="e53ac-152">Hallo `Set-AzureRmVMExtension` opdracht gebruikte toostart elke VM-extensie kan zijn.</span><span class="sxs-lookup"><span data-stu-id="e53ac-152">hello `Set-AzureRmVMExtension` command can be used toostart any VM extension.</span></span> <span data-ttu-id="e53ac-153">Zie voor meer informatie, Hallo [Set AzureRmVMExtension verwijzing](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span><span class="sxs-lookup"><span data-stu-id="e53ac-153">For more information, see hello [Set-AzureRmVMExtension reference](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span></span>


### <a name="azure-portal"></a><span data-ttu-id="e53ac-154">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e53ac-154">Azure portal</span></span>

<span data-ttu-id="e53ac-155">Een VM-extensie kan worden toegepast tooan bestaande virtuele machine via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e53ac-155">A VM extension can be applied tooan existing virtual machine through hello Azure portal.</span></span> <span data-ttu-id="e53ac-156">toodo dus Hallo virtuele machine selecteert u toouse wilt, kiest u **extensies**, en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e53ac-156">toodo so, select hello virtual machine you want toouse, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="e53ac-157">Dit biedt een lijst met beschikbare uitbreidingen.</span><span class="sxs-lookup"><span data-stu-id="e53ac-157">This provides a list of available extensions.</span></span> <span data-ttu-id="e53ac-158">Selecteer Hallo een u wilt en volg de stappen Hallo in Hallo-wizard.</span><span class="sxs-lookup"><span data-stu-id="e53ac-158">Select hello one you want and follow hello steps in hello wizard.</span></span>

<span data-ttu-id="e53ac-159">Hallo toont volgende afbeelding Hallo-installatie van Hallo Microsoft Antimalware-extensie van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e53ac-159">hello following image shows hello installation of hello Microsoft Antimalware extension from hello Azure portal.</span></span>

![Antimalware-uitbreiding installeren](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="e53ac-161">Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="e53ac-161">Azure Resource Manager templates</span></span>

<span data-ttu-id="e53ac-162">VM-extensies kunnen toegevoegde tooan Azure Resource Manager-sjabloon en uitgevoerd met de implementatie van de sjabloon Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="e53ac-162">VM extensions can be added tooan Azure Resource Manager template and executed with hello deployment of hello template.</span></span> <span data-ttu-id="e53ac-163">Uitbreidingen met een sjabloon implementeren is handig voor het volledig geconfigureerde Azure-implementaties maken.</span><span class="sxs-lookup"><span data-stu-id="e53ac-163">Deploying extensions with a template is useful for creating fully configured Azure deployments.</span></span> <span data-ttu-id="e53ac-164">Bijvoorbeeld: hello die volgende JSON is genomen van de Resource Manager-sjabloon die u implementeert een set van netwerktaakverdeling virtuele machines en een Azure SQL database en installeert een toepassing .NET Core op elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e53ac-164">For example, hello following JSON is taken from a Resource Manager template that deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="e53ac-165">Hallo VM-extensie zorgt voor Hallo software-installatie.</span><span class="sxs-lookup"><span data-stu-id="e53ac-165">hello VM extension takes care of hello software installation.</span></span>

<span data-ttu-id="e53ac-166">Zie voor meer informatie, Hallo [volledige Resource Manager-sjabloon](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="e53ac-166">For more information, see hello [full Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

<span data-ttu-id="e53ac-167">Zie voor meer informatie [Azure Resource Manager-sjablonen samenstellen met Windows VM-extensies](template-description.md#extensions).</span><span class="sxs-lookup"><span data-stu-id="e53ac-167">For more information, see [Authoring Azure Resource Manager templates with Windows VM extensions](template-description.md#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="e53ac-168">Beveiligde gegevens van de VM-extensie</span><span class="sxs-lookup"><span data-stu-id="e53ac-168">Secure VM extension data</span></span>

<span data-ttu-id="e53ac-169">Wanneer u een VM-extensie uitvoert, kan het benodigde tooinclude gevoelige informatie zoals referenties, namen van opslagaccounts en toegang tot de opslagaccountsleutels zijn.</span><span class="sxs-lookup"><span data-stu-id="e53ac-169">When you're running a VM extension, it may be necessary tooinclude sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="e53ac-170">Veel VM-extensies bevatten een beveiligde configuratie die gegevens versleutelt en ontsleutelt deze alleen in de virtuele doelmachine Hallo.</span><span class="sxs-lookup"><span data-stu-id="e53ac-170">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside hello target virtual machine.</span></span> <span data-ttu-id="e53ac-171">Elke uitbreiding heeft een specifieke beveiligde configuratieschema die worden uiteengezet in de documentatie van de extensie-specifieke.</span><span class="sxs-lookup"><span data-stu-id="e53ac-171">Each extension has a specific protected configuration schema that will be detailed in extension-specific documentation.</span></span>

<span data-ttu-id="e53ac-172">Hallo volgende voorbeeld ziet u een exemplaar van Hallo extensie voor aangepaste scripts voor Windows.</span><span class="sxs-lookup"><span data-stu-id="e53ac-172">hello following example shows an instance of hello Custom Script extension for Windows.</span></span> <span data-ttu-id="e53ac-173">U ziet dat tooexecute Hallo-opdracht bevat een set referenties.</span><span class="sxs-lookup"><span data-stu-id="e53ac-173">Notice that hello command tooexecute includes a set of credentials.</span></span> <span data-ttu-id="e53ac-174">In dit voorbeeld Hallo opdracht tooexecute niet versleuteld.</span><span class="sxs-lookup"><span data-stu-id="e53ac-174">In this example, hello command tooexecute will not be encrypted.</span></span>


```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ],
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

<span data-ttu-id="e53ac-175">Hallo uitvoering tekenreeks beveiligen door Hallo verplaatsen **opdracht tooexecute** eigenschap toohello **beveiligd** configuratie.</span><span class="sxs-lookup"><span data-stu-id="e53ac-175">Secure hello execution string by moving hello **command tooexecute** property toohello **protected** configuration.</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="e53ac-176">VM-extensies oplossen</span><span class="sxs-lookup"><span data-stu-id="e53ac-176">Troubleshoot VM extensions</span></span>

<span data-ttu-id="e53ac-177">Elk VM-extensie wellicht specifieke stappen voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="e53ac-177">Each VM extension may have specific troubleshooting steps.</span></span> <span data-ttu-id="e53ac-178">Bijvoorbeeld, wanneer u Hallo aangepaste scriptextensie, script uitvoering details zijn te vinden lokaal op Hallo virtuele machine waarop Hallo-extensie is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e53ac-178">For instance, when you're using hello Custom Script extension, script execution details can be found locally on hello virtual machine on which hello extension was run.</span></span> <span data-ttu-id="e53ac-179">Probleemoplossing-extensie-specifieke worden beschreven in de documentatie van de extensie-specifieke.</span><span class="sxs-lookup"><span data-stu-id="e53ac-179">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="e53ac-180">Hallo volgende stappen voor probleemoplossing toepassing tooall-extensies voor virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e53ac-180">hello following troubleshooting steps apply tooall virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="e53ac-181">Status van de extensie weergeven</span><span class="sxs-lookup"><span data-stu-id="e53ac-181">View extension status</span></span>

<span data-ttu-id="e53ac-182">Nadat de extensie van een virtuele machine is uitgevoerd voor een virtuele machine, gebruikt u Hallo status van de PowerShell-opdracht tooreturn-extensie te volgen.</span><span class="sxs-lookup"><span data-stu-id="e53ac-182">After a virtual machine extension has been run against a virtual machine, use hello following PowerShell command tooreturn extension status.</span></span> <span data-ttu-id="e53ac-183">Parameternamen voorbeeld vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="e53ac-183">Replace example parameter names with your own values.</span></span> <span data-ttu-id="e53ac-184">Hallo `Name` parameter toohello extensie opgegeven tijdens het uitvoeren van Hallo-naam heeft.</span><span class="sxs-lookup"><span data-stu-id="e53ac-184">hello `Name` parameter takes hello name given toohello extension at execution time.</span></span>

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="e53ac-185">Hallo-uitvoer ziet er Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="e53ac-185">hello output looks like hello following:</span></span>

```json
ResourceGroupName       : myResourceGroup
VMName                  : myVM
Name                    : myExtensionName
Location                : westus
Etag                    : null
Publisher               : Microsoft.Azure.Extensions
ExtensionType           : DockerExtension
TypeHandlerVersion      : 1.0
Id                      : /subscriptions/mySubscriptionIS/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM/extensions/myExtensionName
PublicSettings          :
ProtectedSettings       :
ProvisioningState       : Succeeded
Statuses                :
SubStatuses             :
AutoUpgradeMinorVersion : False
ForceUpdateTag          :
```

<span data-ttu-id="e53ac-186">Status van extensie-uitvoering kan worden gevonden in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e53ac-186">Extension execution status can also be found in hello Azure portal.</span></span> <span data-ttu-id="e53ac-187">tooview hello status van een extensie, selecteer Hallo virtuele machine kiezen **extensies**, en selecteer de gewenste extensie Hallo.</span><span class="sxs-lookup"><span data-stu-id="e53ac-187">tooview hello status of an extension, select hello virtual machine, choose **Extensions**, and select hello desired extension.</span></span>

### <a name="rerun-vm-extensions"></a><span data-ttu-id="e53ac-188">VM-extensies opnieuw uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e53ac-188">Rerun VM extensions</span></span>

<span data-ttu-id="e53ac-189">Mogelijk zijn er gevallen waarin de extensie van een virtuele machine toobe moet opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="e53ac-189">There may be cases in which a virtual machine extension needs toobe rerun.</span></span> <span data-ttu-id="e53ac-190">U kunt dit doen door Hallo extensie verwijderen en vervolgens opnieuw uit te voeren Hallo-extensie met een methode van de uitvoering van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="e53ac-190">You can do this by removing hello extension and then rerunning hello extension with an execution method of your choice.</span></span> <span data-ttu-id="e53ac-191">tooremove een uitbreiding Hallo volgende opdracht met hello Azure PowerShell-module worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e53ac-191">tooremove an extension, run hello following command with hello Azure PowerShell module.</span></span> <span data-ttu-id="e53ac-192">Parameternamen voorbeeld vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="e53ac-192">Replace example parameter names with your own values.</span></span>

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="e53ac-193">Een uitbreiding kan ook worden verwijderd via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e53ac-193">An extension can also be removed using hello Azure portal.</span></span> <span data-ttu-id="e53ac-194">toodo zodat:</span><span class="sxs-lookup"><span data-stu-id="e53ac-194">toodo so:</span></span>

1. <span data-ttu-id="e53ac-195">Selecteer een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e53ac-195">Select a virtual machine.</span></span>
2. <span data-ttu-id="e53ac-196">Selecteer **extensies**.</span><span class="sxs-lookup"><span data-stu-id="e53ac-196">Select **Extensions**.</span></span>
3. <span data-ttu-id="e53ac-197">Kies Hallo gewenste extensie.</span><span class="sxs-lookup"><span data-stu-id="e53ac-197">Choose hello desired extension.</span></span>
4. <span data-ttu-id="e53ac-198">Selecteer **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="e53ac-198">Select **Uninstall**.</span></span>

## <a name="common-vm-extensions-reference"></a><span data-ttu-id="e53ac-199">Algemene referentie voor VM-extensies</span><span class="sxs-lookup"><span data-stu-id="e53ac-199">Common VM extensions reference</span></span>
| <span data-ttu-id="e53ac-200">Naam van de uitbreiding</span><span class="sxs-lookup"><span data-stu-id="e53ac-200">Extension name</span></span> | <span data-ttu-id="e53ac-201">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e53ac-201">Description</span></span> | <span data-ttu-id="e53ac-202">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="e53ac-202">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e53ac-203">Extensie voor aangepaste scripts voor Windows</span><span class="sxs-lookup"><span data-stu-id="e53ac-203">Custom Script Extension for Windows</span></span> |<span data-ttu-id="e53ac-204">Scripts uitvoeren op een virtuele machine van Azure</span><span class="sxs-lookup"><span data-stu-id="e53ac-204">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="e53ac-205">Extensie voor aangepaste scripts voor Windows</span><span class="sxs-lookup"><span data-stu-id="e53ac-205">Custom Script Extension for Windows</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="e53ac-206">DSC-extensie voor Windows</span><span class="sxs-lookup"><span data-stu-id="e53ac-206">DSC Extension for Windows</span></span> |<span data-ttu-id="e53ac-207">PowerShell DSC (Desired State Configuration)-extensie</span><span class="sxs-lookup"><span data-stu-id="e53ac-207">PowerShell DSC (Desired State Configuration) Extension</span></span> |[<span data-ttu-id="e53ac-208">DSC-extensie voor Windows</span><span class="sxs-lookup"><span data-stu-id="e53ac-208">DSC Extension for Windows</span></span>](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="e53ac-209">Azure Diagnostics-extensie</span><span class="sxs-lookup"><span data-stu-id="e53ac-209">Azure Diagnostics Extension</span></span> |<span data-ttu-id="e53ac-210">Azure Diagnostics beheren</span><span class="sxs-lookup"><span data-stu-id="e53ac-210">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="e53ac-211">Azure Diagnostics-extensie</span><span class="sxs-lookup"><span data-stu-id="e53ac-211">Azure Diagnostics Extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="e53ac-212">Uitbreiding van de toegang tot Azure VM</span><span class="sxs-lookup"><span data-stu-id="e53ac-212">Azure VM Access Extension</span></span> |<span data-ttu-id="e53ac-213">Gebruikers en referenties beheren</span><span class="sxs-lookup"><span data-stu-id="e53ac-213">Manage users and credentials</span></span> |[<span data-ttu-id="e53ac-214">Uitbreiding van de VM-toegang voor Linux</span><span class="sxs-lookup"><span data-stu-id="e53ac-214">VM Access Extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
