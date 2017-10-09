---
title: Hiermee stelt u een app op de virtuele-machineschaalset aaaDeploy
description: Extensies toodepoy een app op Azure Virtual Machine-Schaalsets gebruiken.
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
ms.openlocfilehash: 5f3988b9511d80370a8be1fc042c21fee212506e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a><span data-ttu-id="b4298-103">Implementeren van uw toepassing op virtuele-machineschaalsets</span><span class="sxs-lookup"><span data-stu-id="b4298-103">Deploy your application on virtual machine scale sets</span></span>

<span data-ttu-id="b4298-104">In dit artikel wordt beschreven hoe u zien hoe van tooinstall software op Hallo Hallo tijdschaal ingesteld is ingericht.</span><span class="sxs-lookup"><span data-stu-id="b4298-104">This article describes different ways of how tooinstall software at hello time hello scale set is provisioned.</span></span>

<span data-ttu-id="b4298-105">Gewenste tooreview hello [Scale ingesteld ontwerp overzicht](virtual-machine-scale-sets-design-overview.md) artikel worden enkele Hallo-limieten opgelegd door de virtuele-machineschaalsets beschreven.</span><span class="sxs-lookup"><span data-stu-id="b4298-105">You may want tooreview hello [Scale Set Design Overview](virtual-machine-scale-sets-design-overview.md) article, which describes some of hello limits imposed by virtual machine scale sets.</span></span>

## <a name="capture-and-reuse-an-image"></a><span data-ttu-id="b4298-106">Vastleggen en een installatiekopie van het opnieuw gebruiken</span><span class="sxs-lookup"><span data-stu-id="b4298-106">Capture and reuse an image</span></span>

<span data-ttu-id="b4298-107">U kunt een virtuele machine die in Azure tooprepare de installatiekopie van een basis voor de schaal is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b4298-107">You can use a virtual machine you have in Azure tooprepare a base-image for your scale set.</span></span> <span data-ttu-id="b4298-108">Dit proces maakt een beheerde schijf in uw opslagaccount die u kunt verwijzen naar als basisinstallatiekopie Hallo voor uw scale set.</span><span class="sxs-lookup"><span data-stu-id="b4298-108">This process creates a managed disk in your storage account, which you can reference as hello base image for your scale set.</span></span> 

<span data-ttu-id="b4298-109">Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="b4298-109">Do hello following steps:</span></span>

1. <span data-ttu-id="b4298-110">Een virtuele Machine van Azure maken</span><span class="sxs-lookup"><span data-stu-id="b4298-110">Create an Azure Virtual Machine</span></span>
   * <span data-ttu-id="b4298-111">[Linux][linux-vm-create]</span><span class="sxs-lookup"><span data-stu-id="b4298-111">[Linux][linux-vm-create]</span></span>
   * <span data-ttu-id="b4298-112">[Windows][windows-vm-create]</span><span class="sxs-lookup"><span data-stu-id="b4298-112">[Windows][windows-vm-create]</span></span>

2. <span data-ttu-id="b4298-113">Afstand verbinding met virtuele machine Hallo en Hallo system tooyour eigen smaak aanpassen.</span><span class="sxs-lookup"><span data-stu-id="b4298-113">Remote into hello virtual machine and customize hello system tooyour liking.</span></span>

   <span data-ttu-id="b4298-114">Als u wilt, kunt u nu uw toepassing kunt installeren.</span><span class="sxs-lookup"><span data-stu-id="b4298-114">If you want, you can install your application now.</span></span> <span data-ttu-id="b4298-115">Echter weet dat u nu uw toepassing installeert, mag u uw toepassing meer gecompliceerde upgraden omdat u tooremove wellicht het eerste.</span><span class="sxs-lookup"><span data-stu-id="b4298-115">However, know that by installing your application now, you may make upgrading your application more complicated because you may need tooremove it first.</span></span> <span data-ttu-id="b4298-116">In plaats daarvan kunt u deze stap tooinstall alle vereisten die uw toepassing mogelijk nodig hebt, zoals een bepaalde functie van de runtime- of -besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="b4298-116">Instead, you can use this step tooinstall any prerequisites your application may need, like a specific runtime or operating system feature.</span></span>

3. <span data-ttu-id="b4298-117">Volg 'machine vastleggen' Hallo-zelfstudie voor [Linux] [ linux-vm-capture] of [Windows][windows-vm-capture].</span><span class="sxs-lookup"><span data-stu-id="b4298-117">Follow hello "capture a machine" tutorial for either [Linux][linux-vm-capture] or [Windows][windows-vm-capture].</span></span>

4. <span data-ttu-id="b4298-118">Maak een [virtuele-Machineschaalset] [ vmss-create] Hello installatiekopie URI die u in de vorige stap Hallo vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="b4298-118">Create a [Virtual Machine Scale Set][vmss-create] with hello image URI you captured in hello previous step.</span></span>

<span data-ttu-id="b4298-119">Zie voor meer informatie over schijven [schijven overzicht beheerde](../virtual-machines/windows/managed-disks-overview.md) en [gegevensschijven gekoppeld gebruik](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="b4298-119">For more information about disks, see [Managed Disks Overview](../virtual-machines/windows/managed-disks-overview.md) and [Use Attached Data Disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

## <a name="install-when-hello-scale-set-is-provisioned"></a><span data-ttu-id="b4298-120">Installeren wanneer Hallo scale set is ingericht.</span><span class="sxs-lookup"><span data-stu-id="b4298-120">Install when hello scale set is provisioned</span></span>

<span data-ttu-id="b4298-121">Uitbreidingen van de virtuele machine kunnen worden toegepast tooa virtuele-machineschaalset.</span><span class="sxs-lookup"><span data-stu-id="b4298-121">Virtual machine extensions can be applied tooa virtual machine scale set.</span></span> <span data-ttu-id="b4298-122">U kunt Hallo virtuele machines in een instellen als een hele groep schaal aanpassen met de extensie van virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b4298-122">With a virtual machine extension, you can customize hello virtual machines in a scale set as a whole group.</span></span> <span data-ttu-id="b4298-123">Zie voor meer informatie over uitbreidingen [uitbreidingen van de virtuele Machine](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b4298-123">For more information about extensions, see [Virtual Machine Extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="b4298-124">Er zijn drie belangrijkste uitbreidingen die kunt u, als afhankelijk van het besturingssysteem is op basis van Linux of op basis van Windows.</span><span class="sxs-lookup"><span data-stu-id="b4298-124">There are three main extensions you can use, depending on if your operating system is Linux-based or Windows-based.</span></span>

### <a name="windows"></a><span data-ttu-id="b4298-125">Windows</span><span class="sxs-lookup"><span data-stu-id="b4298-125">Windows</span></span>

<span data-ttu-id="b4298-126">Voor een besturingssysteem op basis van Windows gebruiken beide Hallo **aangepast Script v1.8** -extensie of Hallo **PowerShell DSC** extensie.</span><span class="sxs-lookup"><span data-stu-id="b4298-126">For a Windows-based operating system, use either hello **Custom Script v1.8** extension, or hello **PowerShell DSC** extension.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="b4298-127">Aangepast Script</span><span class="sxs-lookup"><span data-stu-id="b4298-127">Custom Script</span></span>

<span data-ttu-id="b4298-128">een script wordt uitgevoerd op elk exemplaar van de virtuele machine in de schaalset Hallo van Hallo extensie voor aangepaste scripts.</span><span class="sxs-lookup"><span data-stu-id="b4298-128">hello Custom Script extension runs a script on each virtual machine instance in hello scale set.</span></span> <span data-ttu-id="b4298-129">Een configuratiebestand of variabele geeft aan welke bestanden zijn gedownload toohello virtuele machine en vervolgens welke opdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b4298-129">A config file or variable indicates which files are downloaded toohello virtual machine, and then what command runs.</span></span> <span data-ttu-id="b4298-130">U kunt deze toorun een installatieprogramma, een script, een batchbestand en uitvoerbare bestanden bijvoorbeeld gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b4298-130">You could use this toorun an installer, a script, a batch file, any executable for example.</span></span>

<span data-ttu-id="b4298-131">PowerShell maakt gebruik van een hashtabel voor Hallo-instellingen.</span><span class="sxs-lookup"><span data-stu-id="b4298-131">PowerShell uses a hashtable for hello settings.</span></span> <span data-ttu-id="b4298-132">In dit voorbeeld configureert Hallo aangepast script extensie toorun een PowerShell-script dat door IIS wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b4298-132">This example configures hello custom script extension toorun a PowerShell script that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="b4298-133">Gebruik Hallo `-ProtectedSetting` schakelen voor alle instellingen die mogelijk gevoelige gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="b4298-133">Use hello `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

---------


<span data-ttu-id="b4298-134">Azure CLI maakt gebruik van een json-bestand voor Hallo-instellingen.</span><span class="sxs-lookup"><span data-stu-id="b4298-134">Azure CLI uses a json file for hello settings.</span></span> <span data-ttu-id="b4298-135">In dit voorbeeld configureert Hallo aangepast script extensie toorun een PowerShell-script dat door IIS wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b4298-135">This example configures hello custom script extension toorun a PowerShell script that installs IIS.</span></span> <span data-ttu-id="b4298-136">Opslaan van de volgende json-bestand als Hallo _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="b4298-136">Save hello following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

<span data-ttu-id="b4298-137">Voer deze opdracht Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b4298-137">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="b4298-138">Gebruik Hallo `--protected-settings` schakelen voor alle instellingen die mogelijk gevoelige gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="b4298-138">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="powershell-dsc"></a><span data-ttu-id="b4298-139">PowerShell DSC</span><span class="sxs-lookup"><span data-stu-id="b4298-139">PowerShell DSC</span></span>

<span data-ttu-id="b4298-140">U kunt de PowerShell DSC toocustomize Hallo scale set vm-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="b4298-140">You can use PowerShell DSC toocustomize hello scale set vm instances.</span></span> <span data-ttu-id="b4298-141">Hallo **DSC** extensie gepubliceerd door **Microsoft.Powershell** implementeert en Hallo opgegeven DSC-configuratie op elk exemplaar van de virtuele machine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b4298-141">hello **DSC** extension published by **Microsoft.Powershell** deploys and runs hello provided DSC configuration on each virtual machine instance.</span></span> <span data-ttu-id="b4298-142">Een configuratiebestand of variabele vertelt Hallo-uitbreiding waarin *.zip* pakket is, en welke _script functie_ combinatie toorun.</span><span class="sxs-lookup"><span data-stu-id="b4298-142">A config file or variable tells hello extension where *.zip* package is, and which _script-function_ combination toorun.</span></span>

<span data-ttu-id="b4298-143">PowerShell maakt gebruik van een hashtabel voor Hallo-instellingen.</span><span class="sxs-lookup"><span data-stu-id="b4298-143">PowerShell uses a hashtable for hello settings.</span></span> <span data-ttu-id="b4298-144">In dit voorbeeld implementeert een DSC-pakket dat IIS is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b4298-144">This example deploys a DSC package that installs IIS.</span></span>

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

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="b4298-145">Gebruik Hallo `-ProtectedSetting` schakelen voor alle instellingen die mogelijk gevoelige gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="b4298-145">Use hello `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

-----------

<span data-ttu-id="b4298-146">Azure CLI maakt gebruik van een json voor Hallo-instellingen.</span><span class="sxs-lookup"><span data-stu-id="b4298-146">Azure CLI uses a json for hello settings.</span></span> <span data-ttu-id="b4298-147">In dit voorbeeld implementeert een DSC-pakket dat IIS is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b4298-147">This example deploys a DSC package that installs IIS.</span></span> <span data-ttu-id="b4298-148">Opslaan van de volgende json-bestand als Hallo _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="b4298-148">Save hello following json file as _settings.json_.</span></span>

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

<span data-ttu-id="b4298-149">Voer deze opdracht Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b4298-149">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="b4298-150">Gebruik Hallo `--protected-settings` schakelen voor alle instellingen die mogelijk gevoelige gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="b4298-150">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="linux"></a><span data-ttu-id="b4298-151">Linux</span><span class="sxs-lookup"><span data-stu-id="b4298-151">Linux</span></span>

<span data-ttu-id="b4298-152">Linux kunt beide Hallo **aangepast Script v2.0** -extensie of gebruik **cloud init** tijdens het maken van.</span><span class="sxs-lookup"><span data-stu-id="b4298-152">Linux can use either hello **Custom Script v2.0** extension or use **cloud-init** during creation.</span></span>

<span data-ttu-id="b4298-153">Aangepast script is een eenvoudige uitbreiding die u downloadt bestanden toohello virtuele machine-exemplaren en een opdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b4298-153">Custom script is a simple extension that downloads files toohello virtual machine instances, and runs a command.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="b4298-154">Aangepast Script</span><span class="sxs-lookup"><span data-stu-id="b4298-154">Custom Script</span></span>

<span data-ttu-id="b4298-155">Opslaan van de volgende json-bestand als Hallo _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="b4298-155">Save hello following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

<span data-ttu-id="b4298-156">Gebruik hello Azure CLI tooadd deze extensie tooan bestaande virtuele-machineschaalset.</span><span class="sxs-lookup"><span data-stu-id="b4298-156">Use hello Azure CLI tooadd this extension tooan existing virtual machine scale set.</span></span> <span data-ttu-id="b4298-157">Elke virtuele machine in Hallo schaal instellen automatisch wordt uitgevoerd Hallo extensie.</span><span class="sxs-lookup"><span data-stu-id="b4298-157">Each virtual machine in hello scale set automatically runs hello extension.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="b4298-158">Gebruik Hallo `--protected-settings` schakelen voor alle instellingen die mogelijk gevoelige gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="b4298-158">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

#### <a name="cloud-init"></a><span data-ttu-id="b4298-159">Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="b4298-159">Cloud-Init</span></span>

<span data-ttu-id="b4298-160">Cloud-Init wordt gebruikt wanneer Hallo scale set wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b4298-160">Cloud-Init is used when hello scale set is created.</span></span> <span data-ttu-id="b4298-161">Maak eerst een lokaal bestand met de naam _cloud init.txt_ en uw tooit configuratie toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="b4298-161">First, create a local file named _cloud-init.txt_ and add your configuration tooit.</span></span> <span data-ttu-id="b4298-162">Zie bijvoorbeeld [deze basisvertalingen](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span><span class="sxs-lookup"><span data-stu-id="b4298-162">For example, see [this gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span></span>

<span data-ttu-id="b4298-163">Gebruik hello Azure CLI toocreate een schaal ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b4298-163">Use hello Azure CLI toocreate a scale set.</span></span> <span data-ttu-id="b4298-164">Hallo `--custom-data` veld accepteert Hallo-bestandsnaam van een cloud-init-script.</span><span class="sxs-lookup"><span data-stu-id="b4298-164">hello `--custom-data` field accepts hello file name of a cloud-init script.</span></span>

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

## <a name="how-do-i-manage-application-updates"></a><span data-ttu-id="b4298-165">Hoe beheer ik toepassingsupdates?</span><span class="sxs-lookup"><span data-stu-id="b4298-165">How do I manage application updates?</span></span>

<span data-ttu-id="b4298-166">Als u uw toepassing via een uitbreiding hebt geïmplementeerd, alter Hallo uitbreidingsdefinitie op een bepaalde manier.</span><span class="sxs-lookup"><span data-stu-id="b4298-166">If you deployed your application through an extension, alter hello extension definition in some way.</span></span> <span data-ttu-id="b4298-167">Deze wijziging wordt Hallo extensie toobe geïmplementeerd tooall virtuele machine-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="b4298-167">This change causes hello extension toobe redeployed tooall virtual machine instances.</span></span> <span data-ttu-id="b4298-168">Iets **moet** Azure biedt niet kunnen zien die Hallo extensie is gewijzigd over Hallo-extensie, zoals de naam van een bestand waarnaar wordt verwezen, anders worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="b4298-168">Something **must** be changed about hello extension, such as renaming a referenced file, otherwise, Azure does not see that hello extension has changed.</span></span>

<span data-ttu-id="b4298-169">Als u standaard uitbreidbaar Hallo-toepassing in uw eigen installatiekopie, gebruikt u een pijplijn geautomatiseerde implementatie updates van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b4298-169">If you baked hello application into your own operating system image, use an automated deployment pipeline for application updates.</span></span> <span data-ttu-id="b4298-170">Ontwerp uw architectuur toofacilitate snel wisselen van een gefaseerde schaal instelt in productie.</span><span class="sxs-lookup"><span data-stu-id="b4298-170">Design your architecture toofacilitate rapid swapping of a staged scale set into production.</span></span> <span data-ttu-id="b4298-171">Een goed voorbeeld van deze benadering is Hallo [Azure Spinnaker stuurprogramma werk](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span><span class="sxs-lookup"><span data-stu-id="b4298-171">A good example of this approach is hello [Azure Spinnaker driver work](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span></span>

<span data-ttu-id="b4298-172">[Verpakker](https://www.packer.io/) en [Terraform](https://www.terraform.io/) ondersteuning voor Azure Resource Manager, zodat u kunt ook uw installatiekopieën 'als de code' definiëren en ze te ontwikkelen in Azure, gebruik vervolgens Hallo VHD in de schaalset.</span><span class="sxs-lookup"><span data-stu-id="b4298-172">[Packer](https://www.packer.io/) and [Terraform](https://www.terraform.io/) support Azure Resource Manager, so you can also define your images "as code" and build them in Azure, then use hello VHD in your scale set.</span></span> <span data-ttu-id="b4298-173">Hierdoor zou dus worden echter problematisch voor installatiekopieën van marketplace, waarbij extensies/aangepaste scripts belangrijker omdat u geen bits van marketplace rechtstreeks bewerken.</span><span class="sxs-lookup"><span data-stu-id="b4298-173">However, doing so would become problematic for marketplace images, where extensions/custom scripts become more important since you don’t directly manipulate bits from marketplace.</span></span>

## <a name="what-happens-when-a-scale-set-scales-out"></a><span data-ttu-id="b4298-174">Wat gebeurt er wanneer een kan worden geschaald schaalset uit?</span><span class="sxs-lookup"><span data-stu-id="b4298-174">What happens when a scale set scales out?</span></span>
<span data-ttu-id="b4298-175">Wanneer u een of meer virtuele machines tooa scale set toevoegt, wordt de toepassing hello automatisch geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b4298-175">When you add one or more virtual machines tooa scale set, hello application is automatically installed.</span></span> <span data-ttu-id="b4298-176">Voor het voorbeeld als Hallo schaalset uitbreidingen die zijn gedefinieerd, ze worden uitgevoerd op een nieuwe virtuele machine telkens wanneer die deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b4298-176">For example if hello scale set has extensions defined, they run on a new virtual machine each time it is created.</span></span> <span data-ttu-id="b4298-177">Als Hallo scale set is gebaseerd op een aangepaste installatiekopie, is een nieuwe virtuele machine een kopie van de aangepaste broninstallatiekopie Hallo.</span><span class="sxs-lookup"><span data-stu-id="b4298-177">If hello scale set is based on a custom image, any new virtual machine is a copy of hello source custom image.</span></span> <span data-ttu-id="b4298-178">Als Hallo scale set virtuele machines container hosts zijn, mogelijk hebt u starten van de code tooload Hallo containers in een extensie voor aangepaste scripts.</span><span class="sxs-lookup"><span data-stu-id="b4298-178">If hello scale set virtual machines are container hosts, then you might have startup code tooload hello containers in a Custom Script Extension.</span></span> <span data-ttu-id="b4298-179">Of een uitbreiding van een agent die wordt geregistreerd bij de orchestrator van een cluster, zoals Azure Container Service kunt installeren.</span><span class="sxs-lookup"><span data-stu-id="b4298-179">Or, an extension might install an agent that registers with a cluster orchestrator, such as Azure Container Service.</span></span>


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a><span data-ttu-id="b4298-180">Hoe implementatie een OS-update in update domeinen?</span><span class="sxs-lookup"><span data-stu-id="b4298-180">How do you roll out an OS update across update domains?</span></span>
<span data-ttu-id="b4298-181">Stel dat u wilt dat tooupdate ingesteld terwijl de virtuele-machineschaalset Hallo uw installatiekopie van het besturingssysteem uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b4298-181">Suppose you want tooupdate your OS image while keeping hello virtual machine scale set running.</span></span> <span data-ttu-id="b4298-182">PowerShell en hello Azure CLI kunnen Hallo installatiekopieën van virtuele machines, één virtuele machine tegelijk bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b4298-182">PowerShell and hello Azure CLI can update hello virtual machine images, one virtual machine at a time.</span></span> <span data-ttu-id="b4298-183">Hallo [upgraden van een virtuele-Machineschaalset](./virtual-machine-scale-sets-upgrade-scale-set.md) artikel bevat ook verdere informatie over welke opties zijn beschikbaar tooperform een besturingssysteem bij het upgraden naar een virtuele-machineschaalset.</span><span class="sxs-lookup"><span data-stu-id="b4298-183">hello [Upgrade a Virtual Machine Scale Set](./virtual-machine-scale-sets-upgrade-scale-set.md) article also provides further information on what options are available tooperform an operating system upgrade across a virtual machine scale set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4298-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b4298-184">Next steps</span></span>

* [<span data-ttu-id="b4298-185">Gebruik PowerShell toomanage uw schaalset.</span><span class="sxs-lookup"><span data-stu-id="b4298-185">Use PowerShell toomanage your scale set.</span></span>](virtual-machine-scale-sets-windows-manage.md)
* [<span data-ttu-id="b4298-186">Maak een sjabloon van de set schaal.</span><span class="sxs-lookup"><span data-stu-id="b4298-186">Create a scale set template.</span></span>](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

