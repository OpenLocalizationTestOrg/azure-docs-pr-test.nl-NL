---
title: Implementeren van een app op de virtuele-machineschaalsets
description: Uitbreidingen voor depoy een app op Azure Virtual Machine-Schaalsets gebruiken.
services: virtual-machine-scale-sets
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8892199-f2e2-4b82-988a-28ca8a7fd1eb
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: fa7d9d3bef4cb326844ede76171e8c566e87116b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a><span data-ttu-id="ccac3-103">Implementeren van uw toepassing op virtuele-machineschaalsets</span><span class="sxs-lookup"><span data-stu-id="ccac3-103">Deploy your application on virtual machine scale sets</span></span>

<span data-ttu-id="ccac3-104">In dit artikel beschrijft de verschillende manieren voor het installeren van software op het moment dat de schaalaanpassingsset is ingericht.</span><span class="sxs-lookup"><span data-stu-id="ccac3-104">This article describes different ways of how to install software at the time the scale set is provisioned.</span></span>

<span data-ttu-id="ccac3-105">U wilt controleren de [Scale ingesteld ontwerp overzicht](virtual-machine-scale-sets-design-overview.md) artikel worden enkele van de grenzen die zijn opgelegd door de virtuele-machineschaalsets beschreven.</span><span class="sxs-lookup"><span data-stu-id="ccac3-105">You may want to review the [Scale Set Design Overview](virtual-machine-scale-sets-design-overview.md) article, which describes some of the limits imposed by virtual machine scale sets.</span></span>

## <a name="capture-and-reuse-an-image"></a><span data-ttu-id="ccac3-106">Vastleggen en een installatiekopie van het opnieuw gebruiken</span><span class="sxs-lookup"><span data-stu-id="ccac3-106">Capture and reuse an image</span></span>

<span data-ttu-id="ccac3-107">U kunt een virtuele machine die in Azure om de installatiekopie van een base voorbereiden voor de schaal is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ccac3-107">You can use a virtual machine you have in Azure to prepare a base-image for your scale set.</span></span> <span data-ttu-id="ccac3-108">Dit proces maakt een beheerde schijf in uw opslagaccount die u kunt verwijzen naar als de basisinstallatiekopie voor uw scale set.</span><span class="sxs-lookup"><span data-stu-id="ccac3-108">This process creates a managed disk in your storage account, which you can reference as the base image for your scale set.</span></span> 

<span data-ttu-id="ccac3-109">Voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ccac3-109">Do the following steps:</span></span>

1. <span data-ttu-id="ccac3-110">Een virtuele Machine van Azure maken</span><span class="sxs-lookup"><span data-stu-id="ccac3-110">Create an Azure Virtual Machine</span></span>
   * <span data-ttu-id="ccac3-111">[Linux][linux-vm-create]</span><span class="sxs-lookup"><span data-stu-id="ccac3-111">[Linux][linux-vm-create]</span></span>
   * <span data-ttu-id="ccac3-112">[Windows][windows-vm-create]</span><span class="sxs-lookup"><span data-stu-id="ccac3-112">[Windows][windows-vm-create]</span></span>

2. <span data-ttu-id="ccac3-113">Afstand verbinding met de virtuele machine en het systeem naar wens aanpassen.</span><span class="sxs-lookup"><span data-stu-id="ccac3-113">Remote into the virtual machine and customize the system to your liking.</span></span>

   <span data-ttu-id="ccac3-114">Als u wilt, kunt u nu uw toepassing kunt installeren.</span><span class="sxs-lookup"><span data-stu-id="ccac3-114">If you want, you can install your application now.</span></span> <span data-ttu-id="ccac3-115">Weet dat wel door uw toepassing nu te installeren, mag u uw toepassing meer gecompliceerde upgraden omdat u wellicht eerst verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ccac3-115">However, know that by installing your application now, you may make upgrading your application more complicated because you may need to remove it first.</span></span> <span data-ttu-id="ccac3-116">In plaats daarvan kunt u deze stap voor het installeren van alle vereisten die uw toepassing mogelijk nodig hebt, zoals een bepaalde functie van de runtime- of -besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="ccac3-116">Instead, you can use this step to install any prerequisites your application may need, like a specific runtime or operating system feature.</span></span>

3. <span data-ttu-id="ccac3-117">Volg de zelfstudie 'machine vastleggen' voor [Linux] [ linux-vm-capture] of [Windows][windows-vm-capture].</span><span class="sxs-lookup"><span data-stu-id="ccac3-117">Follow the "capture a machine" tutorial for either [Linux][linux-vm-capture] or [Windows][windows-vm-capture].</span></span>

4. <span data-ttu-id="ccac3-118">Maak een [virtuele-Machineschaalset] [ vmss-create] met de installatiekopie van URI die u hebt vastgelegd in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="ccac3-118">Create a [Virtual Machine Scale Set][vmss-create] with the image URI you captured in the previous step.</span></span>

<span data-ttu-id="ccac3-119">Zie voor meer informatie over schijven [schijven overzicht beheerde](../virtual-machines/windows/managed-disks-overview.md) en [gegevensschijven gekoppeld gebruik](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="ccac3-119">For more information about disks, see [Managed Disks Overview](../virtual-machines/windows/managed-disks-overview.md) and [Use Attached Data Disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

## <a name="install-when-the-scale-set-is-provisioned"></a><span data-ttu-id="ccac3-120">Wanneer de schaalaanpassingsset is ingericht installeren</span><span class="sxs-lookup"><span data-stu-id="ccac3-120">Install when the scale set is provisioned</span></span>

<span data-ttu-id="ccac3-121">Uitbreidingen van de virtuele machine kunnen worden toegepast op een virtuele-machineschaalset.</span><span class="sxs-lookup"><span data-stu-id="ccac3-121">Virtual machine extensions can be applied to a virtual machine scale set.</span></span> <span data-ttu-id="ccac3-122">U kunt de virtuele machines in een schaal ingesteld als een hele groep aanpassen met de extensie van virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ccac3-122">With a virtual machine extension, you can customize the virtual machines in a scale set as a whole group.</span></span> <span data-ttu-id="ccac3-123">Zie voor meer informatie over uitbreidingen [uitbreidingen van de virtuele Machine](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ccac3-123">For more information about extensions, see [Virtual Machine Extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="ccac3-124">Er zijn drie belangrijkste uitbreidingen die kunt u, als afhankelijk van het besturingssysteem is op basis van Linux of op basis van Windows.</span><span class="sxs-lookup"><span data-stu-id="ccac3-124">There are three main extensions you can use, depending on if your operating system is Linux-based or Windows-based.</span></span>

### <a name="windows"></a><span data-ttu-id="ccac3-125">Windows</span><span class="sxs-lookup"><span data-stu-id="ccac3-125">Windows</span></span>

<span data-ttu-id="ccac3-126">Voor een besturingssysteem op basis van Windows, gebruiken de **aangepast Script v1.8** extensie, of de **PowerShell DSC** extensie.</span><span class="sxs-lookup"><span data-stu-id="ccac3-126">For a Windows-based operating system, use either the **Custom Script v1.8** extension, or the **PowerShell DSC** extension.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="ccac3-127">Aangepast Script</span><span class="sxs-lookup"><span data-stu-id="ccac3-127">Custom Script</span></span>

<span data-ttu-id="ccac3-128">De aangepaste scriptextensie wordt een script uitgevoerd op elk exemplaar van de virtuele machine in de schaalset.</span><span class="sxs-lookup"><span data-stu-id="ccac3-128">The Custom Script extension runs a script on each virtual machine instance in the scale set.</span></span> <span data-ttu-id="ccac3-129">Een configuratiebestand of variabele geeft aan welke bestanden zijn gedownload naar de virtuele machine en vervolgens welke opdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ccac3-129">A config file or variable indicates which files are downloaded to the virtual machine, and then what command runs.</span></span> <span data-ttu-id="ccac3-130">U kunt dit bijvoorbeeld een installatieprogramma, een script, een batch-bestand, uitvoerbare bestanden uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ccac3-130">You could use this to run an installer, a script, a batch file, any executable for example.</span></span>

<span data-ttu-id="ccac3-131">Een hashtabel PowerShell gebruikt om de instellingen.</span><span class="sxs-lookup"><span data-stu-id="ccac3-131">PowerShell uses a hashtable for the settings.</span></span> <span data-ttu-id="ccac3-132">In dit voorbeeld configureert u de extensie voor aangepaste scripts voor het uitvoeren van een PowerShell-script waarop IIS wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ccac3-132">This example configures the custom script extension to run a PowerShell script that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add the extension to the config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send the new config to Azure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="ccac3-133">Gebruik de `-ProtectedSetting` overschakelen voor alle instellingen die mogelijk gevoelige gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="ccac3-133">Use the `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

---------


<span data-ttu-id="ccac3-134">Azure CLI maakt gebruik van een json-bestand voor de instellingen.</span><span class="sxs-lookup"><span data-stu-id="ccac3-134">Azure CLI uses a json file for the settings.</span></span> <span data-ttu-id="ccac3-135">In dit voorbeeld configureert u de extensie voor aangepaste scripts voor het uitvoeren van een PowerShell-script waarop IIS wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ccac3-135">This example configures the custom script extension to run a PowerShell script that installs IIS.</span></span> <span data-ttu-id="ccac3-136">Sla het volgende json-bestand als _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="ccac3-136">Save the following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

<span data-ttu-id="ccac3-137">Voer deze opdracht Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ccac3-137">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="ccac3-138">Gebruik de `--protected-settings` overschakelen voor alle instellingen die mogelijk gevoelige gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="ccac3-138">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="powershell-dsc"></a><span data-ttu-id="ccac3-139">PowerShell DSC</span><span class="sxs-lookup"><span data-stu-id="ccac3-139">PowerShell DSC</span></span>

<span data-ttu-id="ccac3-140">U kunt de PowerShell DSC gebruiken om aan te passen scale set vm-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="ccac3-140">You can use PowerShell DSC to customize the scale set vm instances.</span></span> <span data-ttu-id="ccac3-141">De **DSC** extensie gepubliceerd door **Microsoft.Powershell** implementeert en de opgegeven DSC-configuratie op elk exemplaar van de virtuele machine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ccac3-141">The **DSC** extension published by **Microsoft.Powershell** deploys and runs the provided DSC configuration on each virtual machine instance.</span></span> <span data-ttu-id="ccac3-142">Een configuratiebestand of variabele vertelt u de extensie waar *.zip* pakket is, en welke _script functie_ combinatie om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="ccac3-142">A config file or variable tells the extension where *.zip* package is, and which _script-function_ combination to run.</span></span>

<span data-ttu-id="ccac3-143">Een hashtabel PowerShell gebruikt om de instellingen.</span><span class="sxs-lookup"><span data-stu-id="ccac3-143">PowerShell uses a hashtable for the settings.</span></span> <span data-ttu-id="ccac3-144">In dit voorbeeld implementeert een DSC-pakket dat IIS is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ccac3-144">This example deploys a DSC package that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$dscConfig = @{
  "wmfVersion" = "latest";
  "configuration" = @{
    "url" = "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip";
    "script" = "configure-http.ps1";
    "function" = "WebsiteTest";
  };
}

# Add the extension to the config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send the new config to Azure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="ccac3-145">Gebruik de `-ProtectedSetting` overschakelen voor alle instellingen die mogelijk gevoelige gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="ccac3-145">Use the `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

-----------

<span data-ttu-id="ccac3-146">Azure CLI maakt gebruik van een json voor de instellingen.</span><span class="sxs-lookup"><span data-stu-id="ccac3-146">Azure CLI uses a json for the settings.</span></span> <span data-ttu-id="ccac3-147">In dit voorbeeld implementeert een DSC-pakket dat IIS is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ccac3-147">This example deploys a DSC package that installs IIS.</span></span> <span data-ttu-id="ccac3-148">Sla het volgende json-bestand als _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="ccac3-148">Save the following json file as _settings.json_.</span></span>

```json
{
  "wmfVersion": "latest",
  "configuration": {
    "url": "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip",
    "script": "configure-http.ps1",
    "function": "WebsiteTest"
  }
}
```

<span data-ttu-id="ccac3-149">Voer deze opdracht Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ccac3-149">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="ccac3-150">Gebruik de `--protected-settings` overschakelen voor alle instellingen die mogelijk gevoelige gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="ccac3-150">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="linux"></a><span data-ttu-id="ccac3-151">Linux</span><span class="sxs-lookup"><span data-stu-id="ccac3-151">Linux</span></span>

<span data-ttu-id="ccac3-152">Linux kunt beide gebruiken de **aangepast Script v2.0** -extensie of gebruik **cloud init** tijdens het maken van.</span><span class="sxs-lookup"><span data-stu-id="ccac3-152">Linux can use either the **Custom Script v2.0** extension or use **cloud-init** during creation.</span></span>

<span data-ttu-id="ccac3-153">Aangepast script is een eenvoudige uitbreiding die u downloadt bestanden naar de virtuele machine-exemplaren en een opdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ccac3-153">Custom script is a simple extension that downloads files to the virtual machine instances, and runs a command.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="ccac3-154">Aangepast Script</span><span class="sxs-lookup"><span data-stu-id="ccac3-154">Custom Script</span></span>

<span data-ttu-id="ccac3-155">Sla het volgende json-bestand als _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="ccac3-155">Save the following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

<span data-ttu-id="ccac3-156">De Azure CLI gebruiken deze extensie toevoegen aan een bestaande virtuele-machineschaalset.</span><span class="sxs-lookup"><span data-stu-id="ccac3-156">Use the Azure CLI to add this extension to an existing virtual machine scale set.</span></span> <span data-ttu-id="ccac3-157">Elke virtuele machine in de schaal automatisch ingesteld wordt uitgevoerd voor de uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="ccac3-157">Each virtual machine in the scale set automatically runs the extension.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="ccac3-158">Gebruik de `--protected-settings` overschakelen voor alle instellingen die mogelijk gevoelige gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="ccac3-158">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

#### <a name="cloud-init"></a><span data-ttu-id="ccac3-159">Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="ccac3-159">Cloud-Init</span></span>

<span data-ttu-id="ccac3-160">Cloud-Init wordt gebruikt wanneer de schaalset gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ccac3-160">Cloud-Init is used when the scale set is created.</span></span> <span data-ttu-id="ccac3-161">Maak eerst een lokaal bestand met de naam _cloud init.txt_ en voeg uw configuratie toe.</span><span class="sxs-lookup"><span data-stu-id="ccac3-161">First, create a local file named _cloud-init.txt_ and add your configuration to it.</span></span> <span data-ttu-id="ccac3-162">Zie bijvoorbeeld [deze basisvertalingen](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span><span class="sxs-lookup"><span data-stu-id="ccac3-162">For example, see [this gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span></span>

<span data-ttu-id="ccac3-163">De Azure CLI gebruiken voor het maken van een schaalset.</span><span class="sxs-lookup"><span data-stu-id="ccac3-163">Use the Azure CLI to create a scale set.</span></span> <span data-ttu-id="ccac3-164">De `--custom-data` veld accepteert de bestandsnaam van een cloud-init-script.</span><span class="sxs-lookup"><span data-stu-id="ccac3-164">The `--custom-data` field accepts the file name of a cloud-init script.</span></span>

```azurecli
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

## <a name="how-do-i-manage-application-updates"></a><span data-ttu-id="ccac3-165">Hoe beheer ik toepassingsupdates?</span><span class="sxs-lookup"><span data-stu-id="ccac3-165">How do I manage application updates?</span></span>

<span data-ttu-id="ccac3-166">Als u uw toepassing via een uitbreiding hebt geïmplementeerd, wijzigt u de definitie van de extensie in een bepaalde manier.</span><span class="sxs-lookup"><span data-stu-id="ccac3-166">If you deployed your application through an extension, alter the extension definition in some way.</span></span> <span data-ttu-id="ccac3-167">Deze wijziging zorgt ervoor dat de extensie moet worden geïmplementeerd op alle exemplaren van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ccac3-167">This change causes the extension to be redeployed to all virtual machine instances.</span></span> <span data-ttu-id="ccac3-168">Iets **moet** Azure biedt niet kunnen zien dat de extensie is gewijzigd over de extensie in, zoals de naam van een bestand waarnaar wordt verwezen, anders worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="ccac3-168">Something **must** be changed about the extension, such as renaming a referenced file, otherwise, Azure does not see that the extension has changed.</span></span>

<span data-ttu-id="ccac3-169">Als u standaard de toepassing in uw eigen installatiekopie uitbreidbaar, gebruikt u een pijplijn geautomatiseerde implementatie updates van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="ccac3-169">If you baked the application into your own operating system image, use an automated deployment pipeline for application updates.</span></span> <span data-ttu-id="ccac3-170">Ontwerp uw architectuur ter bevordering van de snelle wisselen van een gefaseerde schaal instelt in productie.</span><span class="sxs-lookup"><span data-stu-id="ccac3-170">Design your architecture to facilitate rapid swapping of a staged scale set into production.</span></span> <span data-ttu-id="ccac3-171">Een goed voorbeeld van deze benadering is de [Azure Spinnaker stuurprogramma werk](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span><span class="sxs-lookup"><span data-stu-id="ccac3-171">A good example of this approach is the [Azure Spinnaker driver work](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span></span>

<span data-ttu-id="ccac3-172">[Verpakker](https://www.packer.io/) en [Terraform](https://www.terraform.io/) ondersteuning voor Azure Resource Manager, zodat u kunt ook uw installatiekopieën 'als de code' definiëren en ze te ontwikkelen in Azure, gebruik vervolgens de VHD in de schaalset.</span><span class="sxs-lookup"><span data-stu-id="ccac3-172">[Packer](https://www.packer.io/) and [Terraform](https://www.terraform.io/) support Azure Resource Manager, so you can also define your images "as code" and build them in Azure, then use the VHD in your scale set.</span></span> <span data-ttu-id="ccac3-173">Hierdoor zou dus worden echter problematisch voor installatiekopieën van marketplace, waarbij extensies/aangepaste scripts belangrijker omdat u geen bits van marketplace rechtstreeks bewerken.</span><span class="sxs-lookup"><span data-stu-id="ccac3-173">However, doing so would become problematic for marketplace images, where extensions/custom scripts become more important since you don’t directly manipulate bits from marketplace.</span></span>

## <a name="what-happens-when-a-scale-set-scales-out"></a><span data-ttu-id="ccac3-174">Wat gebeurt er wanneer een kan worden geschaald schaalset uit?</span><span class="sxs-lookup"><span data-stu-id="ccac3-174">What happens when a scale set scales out?</span></span>
<span data-ttu-id="ccac3-175">Wanneer u een of meer virtuele machines aan een schaalset toevoegt, wordt de toepassing wordt automatisch geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ccac3-175">When you add one or more virtual machines to a scale set, the application is automatically installed.</span></span> <span data-ttu-id="ccac3-176">Voor het voorbeeld als de schaal ingesteld uitbreidingen die zijn gedefinieerd, ze worden uitgevoerd op een nieuwe virtuele machine telkens wanneer die deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ccac3-176">For example if the scale set has extensions defined, they run on a new virtual machine each time it is created.</span></span> <span data-ttu-id="ccac3-177">Als de scale-set is gebaseerd op een aangepaste installatiekopie, is een nieuwe virtuele machine een kopie van de aangepaste installatiekopie van de bron.</span><span class="sxs-lookup"><span data-stu-id="ccac3-177">If the scale set is based on a custom image, any new virtual machine is a copy of the source custom image.</span></span> <span data-ttu-id="ccac3-178">Als de scale set virtuele machines container hosts zijn, hebt u mogelijk starten van de code voor het laden van de containers in een extensie voor aangepaste scripts.</span><span class="sxs-lookup"><span data-stu-id="ccac3-178">If the scale set virtual machines are container hosts, then you might have startup code to load the containers in a Custom Script Extension.</span></span> <span data-ttu-id="ccac3-179">Of een uitbreiding van een agent die wordt geregistreerd bij de orchestrator van een cluster, zoals Azure Container Service kunt installeren.</span><span class="sxs-lookup"><span data-stu-id="ccac3-179">Or, an extension might install an agent that registers with a cluster orchestrator, such as Azure Container Service.</span></span>


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a><span data-ttu-id="ccac3-180">Hoe implementatie een OS-update in update domeinen?</span><span class="sxs-lookup"><span data-stu-id="ccac3-180">How do you roll out an OS update across update domains?</span></span>
<span data-ttu-id="ccac3-181">Stel dat u wilt uw installatiekopie van het besturingssysteem bijwerken terwijl de virtuele-machineschaalset ingesteld uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ccac3-181">Suppose you want to update your OS image while keeping the virtual machine scale set running.</span></span> <span data-ttu-id="ccac3-182">PowerShell en Azure CLI kunt installatiekopieën van virtuele machines, één virtuele machine tegelijk bijwerken.</span><span class="sxs-lookup"><span data-stu-id="ccac3-182">PowerShell and the Azure CLI can update the virtual machine images, one virtual machine at a time.</span></span> <span data-ttu-id="ccac3-183">De [upgraden van een virtuele-Machineschaalset](./virtual-machine-scale-sets-upgrade-scale-set.md) artikel bevat ook verdere informatie over welke opties beschikbaar zijn voor een upgrade uitvoert op een virtuele-machineschaalset.</span><span class="sxs-lookup"><span data-stu-id="ccac3-183">The [Upgrade a Virtual Machine Scale Set](./virtual-machine-scale-sets-upgrade-scale-set.md) article also provides further information on what options are available to perform an operating system upgrade across a virtual machine scale set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccac3-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ccac3-184">Next steps</span></span>

* [<span data-ttu-id="ccac3-185">Gebruik PowerShell voor het beheren van uw scale ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ccac3-185">Use PowerShell to manage your scale set.</span></span>](virtual-machine-scale-sets-windows-manage.md)
* [<span data-ttu-id="ccac3-186">Maak een sjabloon van de set schaal.</span><span class="sxs-lookup"><span data-stu-id="ccac3-186">Create a scale set template.</span></span>](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

