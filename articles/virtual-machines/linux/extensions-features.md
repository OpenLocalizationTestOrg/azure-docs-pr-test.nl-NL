---
title: Uitbreidingen van de virtuele machine en functies voor Linux | Microsoft Docs
description: Meer informatie over welke extensies beschikbaar zijn voor virtuele machines in Azure, gegroepeerd op wat ze bieden of verbeteren.
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 52f5d0ec-8f75-49e7-9e15-88d46b420e63
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 8a5b39351f665c51ae7d83f755329e54ff3cf786
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a><span data-ttu-id="c6c30-103">Uitbreidingen van de virtuele machine en functies voor Linux</span><span class="sxs-lookup"><span data-stu-id="c6c30-103">Virtual machine extensions and features for Linux</span></span>

<span data-ttu-id="c6c30-104">Virtuele machine van Azure-extensies zijn kleine toepassingen waarmee de configuratie en automatisering taken na de implementatie op virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="c6c30-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="c6c30-105">Als een virtuele machine vereist een software-installatie, beveiliging tegen virussen of Docker-configuratie, kan er bijvoorbeeld een VM-extensie worden gebruikt om deze taken te voltooien.</span><span class="sxs-lookup"><span data-stu-id="c6c30-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used to complete these tasks.</span></span> <span data-ttu-id="c6c30-106">Azure VM-extensies kunnen worden uitgevoerd met behulp van de Azure CLI, PowerShell, Azure resourcemanager-sjablonen en de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c6c30-106">Azure VM extensions can be run using the Azure CLI, PowerShell, Azure Resource Manager templates, and the Azure portal.</span></span> <span data-ttu-id="c6c30-107">Extensies worden gebundeld met een nieuwe implementatie van de virtuele machine of eventuele bestaande systeem uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c6c30-107">Extensions can be bundled with a new virtual machine deployment, or run against any existing system.</span></span>

<span data-ttu-id="c6c30-108">Dit document bevat een overzicht van de VM-extensies voor vereisten voor het gebruik van Azure VM-extensies en instructies voor het detecteren, beheren en verwijderen van de VM-extensies.</span><span class="sxs-lookup"><span data-stu-id="c6c30-108">This document provides an overview of VM extensions, prerequisites for using Azure VM extensions, and guidance on how to detect, manage, and remove VM extensions.</span></span> <span data-ttu-id="c6c30-109">Dit document vindt u algemene informatie omdat veel VM-extensies beschikbaar zijn, elk met een potentieel unieke configuratie.</span><span class="sxs-lookup"><span data-stu-id="c6c30-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="c6c30-110">Extensie-specifieke informatie vindt u in elk document specifiek is voor de afzonderlijke extensie.</span><span class="sxs-lookup"><span data-stu-id="c6c30-110">Extension-specific details can be found in each document specific to the individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="c6c30-111">Gebruiksvoorbeelden en voorbeelden</span><span class="sxs-lookup"><span data-stu-id="c6c30-111">Use cases and samples</span></span>

<span data-ttu-id="c6c30-112">Enkele andere Azure VM-extensies beschikbaar zijn, elk met een specifieke gebruiksvoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c6c30-112">Several different Azure VM extensions are available, each with a specific use case.</span></span> <span data-ttu-id="c6c30-113">Een aantal voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="c6c30-113">Some examples are:</span></span>

- <span data-ttu-id="c6c30-114">Status van PowerShell gewenste configuraties toepassen op een virtuele machine met behulp van de DSC-uitbreiding voor Linux.</span><span class="sxs-lookup"><span data-stu-id="c6c30-114">Apply PowerShell Desired State configurations to a virtual machine using the DSC extension for Linux.</span></span> <span data-ttu-id="c6c30-115">Zie voor meer informatie [Azure gewenst State configuration-uitbreiding](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span><span class="sxs-lookup"><span data-stu-id="c6c30-115">For more information, see [Azure Desired State configuration extension](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span></span>
- <span data-ttu-id="c6c30-116">Bewaking van een virtuele machine met de Microsoft Monitoring Agent VM-extensie te configureren.</span><span class="sxs-lookup"><span data-stu-id="c6c30-116">Configure monitoring of a virtual machine with the Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="c6c30-117">Zie voor meer informatie [het bewaken van Linux-VM](tutorial-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="c6c30-117">For more information, see [How to monitor a Linux VM](tutorial-monitoring.md).</span></span>
- <span data-ttu-id="c6c30-118">Bewaking van uw Azure-infrastructuur met de extensie Datadog configureren.</span><span class="sxs-lookup"><span data-stu-id="c6c30-118">Configure monitoring of your Azure infrastructure with the Datadog extension.</span></span> <span data-ttu-id="c6c30-119">Zie voor meer informatie de [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="c6c30-119">For more information, see the [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="c6c30-120">Configureer een Docker-host op een virtuele machine van Azure met behulp van de Docker-VM-extensie.</span><span class="sxs-lookup"><span data-stu-id="c6c30-120">Configure a Docker host on an Azure virtual machine using the Docker VM extension.</span></span> <span data-ttu-id="c6c30-121">Zie voor meer informatie [Docker VM-extensie](dockerextension.md).</span><span class="sxs-lookup"><span data-stu-id="c6c30-121">For more information, see [Docker VM extension](dockerextension.md).</span></span>

<span data-ttu-id="c6c30-122">Een aangepast Script-uitbreiding is naast processpecifieke uitbreidingen beschikbaar voor Windows- en Linux virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="c6c30-122">In addition to process-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="c6c30-123">De aangepaste scriptextensie voor Linux kunt u een Bash-script worden uitgevoerd op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c6c30-123">The Custom Script extension for Linux allows any Bash script to be run on a virtual machine.</span></span> <span data-ttu-id="c6c30-124">Aangepaste scripts zijn handig voor het ontwerpen van Azure-implementaties die moeten worden geconfigureerd afgezien van wat systeemeigen Azure tooling kan bieden.</span><span class="sxs-lookup"><span data-stu-id="c6c30-124">Custom scripts are useful for designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="c6c30-125">Zie voor meer informatie [Linux VM aangepaste scriptextensie](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="c6c30-125">For more information, see [Linux VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="c6c30-126">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c6c30-126">Prerequisites</span></span>

<span data-ttu-id="c6c30-127">De extensie van elke virtuele machine mogelijk een eigen set vereisten.</span><span class="sxs-lookup"><span data-stu-id="c6c30-127">Each virtual machine extension might have its own set of prerequisites.</span></span> <span data-ttu-id="c6c30-128">De Docker-VM-extensie heeft bijvoorbeeld een vereiste van een ondersteunde Linux-distributie.</span><span class="sxs-lookup"><span data-stu-id="c6c30-128">For instance, the Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="c6c30-129">Vereisten van afzonderlijke uitbreidingen worden beschreven in de documentatie van extensie-specifieke.</span><span class="sxs-lookup"><span data-stu-id="c6c30-129">Requirements of individual extensions are detailed in the extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="c6c30-130">Azure VM-agent</span><span class="sxs-lookup"><span data-stu-id="c6c30-130">Azure VM agent</span></span>

<span data-ttu-id="c6c30-131">De Azure VM-agent beheert interactie tussen Azure een virtuele machine en de domeincontroller van de Azure-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="c6c30-131">The Azure VM agent manages interactions between an Azure virtual machine and the Azure fabric controller.</span></span> <span data-ttu-id="c6c30-132">De VM-agent is verantwoordelijk voor veel functionele aspecten van het implementeren en beheren van virtuele machines in Azure, waaronder het uitvoeren van de VM-extensies.</span><span class="sxs-lookup"><span data-stu-id="c6c30-132">The VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="c6c30-133">De Azure VM-agent is geïnstalleerd op Azure Marketplace-installatiekopieën en kan handmatig worden geïnstalleerd op ondersteunde besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="c6c30-133">The Azure VM agent is preinstalled on Azure Marketplace images and can be installed manually on supported operating systems.</span></span>

<span data-ttu-id="c6c30-134">Zie voor informatie over ondersteunde besturingssystemen en installatie-instructies, [virtuele machine van Azure-agent](../windows/classic/agents-and-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="c6c30-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](../windows/classic/agents-and-extensions.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="c6c30-135">VM-extensies detecteren</span><span class="sxs-lookup"><span data-stu-id="c6c30-135">Discover VM extensions</span></span>

<span data-ttu-id="c6c30-136">Veel andere VM-extensies zijn beschikbaar voor gebruik met virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="c6c30-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="c6c30-137">Voer de volgende opdracht met de Azure CLI, de Voorbeeldlocatie vervangen door de locatie van uw keuze voor een volledig overzicht.</span><span class="sxs-lookup"><span data-stu-id="c6c30-137">To see a complete list, run the following command with the Azure CLI, replacing the example location with the location of your choice.</span></span>

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a><span data-ttu-id="c6c30-138">VM-extensies worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="c6c30-138">Run VM extensions</span></span>

<span data-ttu-id="c6c30-139">Uitbreidingen van de virtuele machine van Azure kunnen op bestaande virtuele machines, die vooral nuttig zijn wanneer u configuratiewijzigingen aanbrengen of herstel de verbinding op een reeds geïmplementeerde virtuele machine moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c6c30-139">Azure virtual machine extensions can be run on existing virtual machines, which are useful when you need to make configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="c6c30-140">VM-extensies kunnen ook worden gebundeld met implementaties van Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="c6c30-140">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="c6c30-141">Via uitbreidingen met Resource Manager-sjablonen kunnen virtuele machines in Azure worden geïmplementeerd en geconfigureerd zonder tussenkomst van de na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="c6c30-141">By using extensions with Resource Manager templates, Azure virtual machines can be deployed and configured without post-deployment intervention.</span></span>

<span data-ttu-id="c6c30-142">De volgende manieren kunnen worden gebruikt voor het uitvoeren van een uitbreiding op een bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c6c30-142">The following methods can be used to run an extension against an existing virtual machine.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="c6c30-143">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c6c30-143">Azure CLI</span></span>

<span data-ttu-id="c6c30-144">Uitbreidingen van de virtuele machine van Azure kunnen worden uitgevoerd op basis van een bestaande virtuele machine met behulp van de `az vm extension set` opdracht.</span><span class="sxs-lookup"><span data-stu-id="c6c30-144">Azure virtual machine extensions can be run against an existing virtual machine by using the `az vm extension set` command.</span></span> <span data-ttu-id="c6c30-145">In dit voorbeeld wordt de extensie voor aangepaste scripts uitgevoerd op basis van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c6c30-145">This example runs the custom script extension against a virtual machine.</span></span>

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

<span data-ttu-id="c6c30-146">Het script wordt de uitvoer is vergelijkbaar met de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="c6c30-146">The script produces output similar to the following text:</span></span>

```azurecli
info:    Executing command vm extension set
+ Looking up the VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a><span data-ttu-id="c6c30-147">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c6c30-147">Azure portal</span></span>

<span data-ttu-id="c6c30-148">VM-extensies kunnen worden toegepast op een bestaande virtuele machine via de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c6c30-148">VM extensions can be applied to an existing virtual machine through the Azure portal.</span></span> <span data-ttu-id="c6c30-149">Selecteer de virtuele machine om dit te doen, kiest u **extensies**, en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c6c30-149">To do so, select the virtual machine, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="c6c30-150">Selecteer de uitbreiding die u wilt dat in de lijst met beschikbare uitbreidingen en volg de instructies in de wizard.</span><span class="sxs-lookup"><span data-stu-id="c6c30-150">Select the extension you want from the list of available extensions and follow the instructions in the wizard.</span></span>

<span data-ttu-id="c6c30-151">De volgende afbeelding ziet u de installatie van de extensie Linux aangepast Script van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c6c30-151">The following image shows the installation of the Linux Custom Script extension from the Azure portal.</span></span>

![Extensie voor aangepaste scripts installeren](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="c6c30-153">Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="c6c30-153">Azure Resource Manager templates</span></span>

<span data-ttu-id="c6c30-154">VM-extensies worden toegevoegd aan een Azure Resource Manager-sjabloon en uitgevoerd met de implementatie van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="c6c30-154">VM extensions can be added to an Azure Resource Manager template and executed with the deployment of the template.</span></span> <span data-ttu-id="c6c30-155">Wanneer u een uitbreiding met een sjabloon implementeert, kunt u volledig geconfigureerde Azure-implementaties.</span><span class="sxs-lookup"><span data-stu-id="c6c30-155">When you deploy an extension with a template, you can create fully configured Azure deployments.</span></span> <span data-ttu-id="c6c30-156">Bijvoorbeeld is de volgende JSON afkomstig van een Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="c6c30-156">For example, the following JSON is taken from a Resource Manager template.</span></span> <span data-ttu-id="c6c30-157">De sjabloon implementeert een set van netwerktaakverdeling virtuele machines en een Azure SQL database, en installeert een toepassing .NET Core op elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c6c30-157">The template deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="c6c30-158">De VM-extensie zorgt voor de software-installatie.</span><span class="sxs-lookup"><span data-stu-id="c6c30-158">The VM extension takes care of the software installation.</span></span>

<span data-ttu-id="c6c30-159">Voor meer informatie raadpleegt u de volledige [Resource Manager-sjabloon](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="c6c30-159">For more information, see the full [Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
    }
}
```

<span data-ttu-id="c6c30-160">Zie voor meer informatie [Azure Resource Manager-sjablonen samenstellen](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span><span class="sxs-lookup"><span data-stu-id="c6c30-160">For more information, see [Authoring Azure Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="c6c30-161">Beveiligde gegevens van de VM-extensie</span><span class="sxs-lookup"><span data-stu-id="c6c30-161">Secure VM extension data</span></span>

<span data-ttu-id="c6c30-162">Wanneer u een VM-extensie uitvoert, is het mogelijk met gevoelige informatie zoals referenties, namen van opslagaccounts en toegangssleutels voor opslag-account nodig.</span><span class="sxs-lookup"><span data-stu-id="c6c30-162">When you're running a VM extension, it may be necessary to include sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="c6c30-163">Veel VM-extensies bevatten een beveiligde configuratie die gegevens versleutelt en ontsleutelt deze alleen in de doel-virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c6c30-163">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside the target virtual machine.</span></span> <span data-ttu-id="c6c30-164">Elke uitbreiding heeft een specifieke beveiligde configuratieschema en elk wordt beschreven in de uitbreiding specifieke documentatie bij.</span><span class="sxs-lookup"><span data-stu-id="c6c30-164">Each extension has a specific protected configuration schema, and each is detailed in extension-specific documentation.</span></span>

<span data-ttu-id="c6c30-165">Het volgende voorbeeld ziet een exemplaar van de aangepaste scriptextensie voor Linux.</span><span class="sxs-lookup"><span data-stu-id="c6c30-165">The following example shows an instance of the Custom Script extension for Linux.</span></span> <span data-ttu-id="c6c30-166">U ziet dat de opdracht voor het uitvoeren van een set referenties bevat.</span><span class="sxs-lookup"><span data-stu-id="c6c30-166">Notice that the command to execute includes a set of credentials.</span></span> <span data-ttu-id="c6c30-167">In dit voorbeeld de opdracht wordt uitgevoerd niet versleuteld.</span><span class="sxs-lookup"><span data-stu-id="c6c30-167">In this example, the command to execute will not be encrypted.</span></span>


```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ],
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

<span data-ttu-id="c6c30-168">Het verplaatsen van de **opdracht wordt uitgevoerd** eigenschap in op de **beveiligd** configuratie beveiligt de tekenreeks kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c6c30-168">Moving the **command to execute** property to the **protected** configuration secures the execution string.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="c6c30-169">VM-extensies oplossen</span><span class="sxs-lookup"><span data-stu-id="c6c30-169">Troubleshoot VM extensions</span></span>

<span data-ttu-id="c6c30-170">Elk VM-extensie mogelijk naar de extensie specifieke stappen voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="c6c30-170">Each VM extension may have troubleshooting steps specific to the extension.</span></span> <span data-ttu-id="c6c30-171">Bijvoorbeeld, wanneer u de extensie voor aangepaste scripts, script uitvoering details zijn te vinden lokaal op de virtuele machine waarop de uitbreiding is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c6c30-171">For example, when you're using the Custom Script extension, script execution details can be found locally on the virtual machine on which the extension was run.</span></span> <span data-ttu-id="c6c30-172">Probleemoplossing-extensie-specifieke worden beschreven in de documentatie van de extensie-specifieke.</span><span class="sxs-lookup"><span data-stu-id="c6c30-172">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="c6c30-173">De volgende stappen van toepassing op alle uitbreidingen van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c6c30-173">The following troubleshooting steps apply to all virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="c6c30-174">Status van de extensie weergeven</span><span class="sxs-lookup"><span data-stu-id="c6c30-174">View extension status</span></span>

<span data-ttu-id="c6c30-175">Extensie nadat een virtuele machine is uitgevoerd voor een virtuele machine, gebruikt u de volgende opdracht in de Azure CLI om te retourneren van de status van extensie.</span><span class="sxs-lookup"><span data-stu-id="c6c30-175">After a virtual machine extension has been run against a virtual machine, use the following Azure CLI command to return extension status.</span></span> <span data-ttu-id="c6c30-176">Parameternamen voorbeeld vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="c6c30-176">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="c6c30-177">De uitvoer ziet er de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="c6c30-177">The output looks like the following text:</span></span>

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

<span data-ttu-id="c6c30-178">Status van extensie-uitvoering kan worden gevonden in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c6c30-178">Extension execution status can also be found in the Azure portal.</span></span> <span data-ttu-id="c6c30-179">Selecteer de virtuele machine om de status van een uitbreiding, weergeven, kiest u **extensies**, en selecteer de gewenste extensie.</span><span class="sxs-lookup"><span data-stu-id="c6c30-179">To view the status of an extension, select the virtual machine, choose **Extensions**, and select the desired extension.</span></span>

### <a name="rerun-a-vm-extension"></a><span data-ttu-id="c6c30-180">Voer een VM-extensie</span><span class="sxs-lookup"><span data-stu-id="c6c30-180">Rerun a VM extension</span></span>

<span data-ttu-id="c6c30-181">Mogelijk zijn er gevallen waarin de extensie van een virtuele machine moet opnieuw worden gestart.</span><span class="sxs-lookup"><span data-stu-id="c6c30-181">There may be cases in which a virtual machine extension needs to be rerun.</span></span> <span data-ttu-id="c6c30-182">U kunt een uitbreiding opnieuw uitvoeren te verwijderen en vervolgens opnieuw uit te voeren de uitbreiding met een methode van de uitvoering van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="c6c30-182">You can rerun an extension by removing it, and then rerunning the extension with an execution method of your choice.</span></span> <span data-ttu-id="c6c30-183">Voer de volgende opdracht met de Azure CLI voor het verwijderen van extensie.</span><span class="sxs-lookup"><span data-stu-id="c6c30-183">To remove an extension, run the following command with the Azure CLI.</span></span> <span data-ttu-id="c6c30-184">Parameternamen voorbeeld vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="c6c30-184">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

<span data-ttu-id="c6c30-185">U kunt een uitbreiding verwijderen met behulp van de volgende stappen uit in de Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="c6c30-185">You can remove an extension by using the following steps in the Azure portal:</span></span>

1. <span data-ttu-id="c6c30-186">Selecteer een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c6c30-186">Select a virtual machine.</span></span>
2. <span data-ttu-id="c6c30-187">Kies **extensies**.</span><span class="sxs-lookup"><span data-stu-id="c6c30-187">Choose **Extensions**.</span></span>
3. <span data-ttu-id="c6c30-188">Selecteer de gewenste extensie.</span><span class="sxs-lookup"><span data-stu-id="c6c30-188">Select the desired extension.</span></span>
4. <span data-ttu-id="c6c30-189">Kies **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="c6c30-189">Choose **Uninstall**.</span></span>

## <a name="common-vm-extension-reference"></a><span data-ttu-id="c6c30-190">Algemene referentie voor VM-extensie</span><span class="sxs-lookup"><span data-stu-id="c6c30-190">Common VM extension reference</span></span>
| <span data-ttu-id="c6c30-191">Naam van de uitbreiding</span><span class="sxs-lookup"><span data-stu-id="c6c30-191">Extension name</span></span> | <span data-ttu-id="c6c30-192">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c6c30-192">Description</span></span> | <span data-ttu-id="c6c30-193">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="c6c30-193">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6c30-194">Extensie voor aangepaste scripts voor Linux</span><span class="sxs-lookup"><span data-stu-id="c6c30-194">Custom Script extension for Linux</span></span> |<span data-ttu-id="c6c30-195">Scripts uitvoeren op een virtuele machine van Azure</span><span class="sxs-lookup"><span data-stu-id="c6c30-195">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="c6c30-196">Extensie voor aangepaste scripts voor Linux</span><span class="sxs-lookup"><span data-stu-id="c6c30-196">Custom Script extension for Linux</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="c6c30-197">Docker-uitbreiding</span><span class="sxs-lookup"><span data-stu-id="c6c30-197">Docker extension</span></span> |<span data-ttu-id="c6c30-198">Installeer de Docker-daemon ter ondersteuning van externe Docker-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="c6c30-198">Install the Docker daemon to support remote Docker commands.</span></span> |[<span data-ttu-id="c6c30-199">Docker-VM-extensie</span><span class="sxs-lookup"><span data-stu-id="c6c30-199">Docker VM extension</span></span>](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="c6c30-200">VM-extensie voor toegang</span><span class="sxs-lookup"><span data-stu-id="c6c30-200">VM Access extension</span></span> |<span data-ttu-id="c6c30-201">Weer toegang tot een virtuele machine van Azure</span><span class="sxs-lookup"><span data-stu-id="c6c30-201">Regain access to an Azure virtual machine</span></span> |[<span data-ttu-id="c6c30-202">VM-extensie voor toegang</span><span class="sxs-lookup"><span data-stu-id="c6c30-202">VM Access extension</span></span>](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| <span data-ttu-id="c6c30-203">Azure extensie voor diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="c6c30-203">Azure Diagnostics extension</span></span> |<span data-ttu-id="c6c30-204">Azure Diagnostics beheren</span><span class="sxs-lookup"><span data-stu-id="c6c30-204">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="c6c30-205">Azure extensie voor diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="c6c30-205">Azure Diagnostics extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="c6c30-206">De extensie Azure VM-toegang</span><span class="sxs-lookup"><span data-stu-id="c6c30-206">Azure VM Access extension</span></span> |<span data-ttu-id="c6c30-207">Gebruikers en referenties beheren</span><span class="sxs-lookup"><span data-stu-id="c6c30-207">Manage users and credentials</span></span> |[<span data-ttu-id="c6c30-208">Uitbreiding van de VM-toegang voor Linux</span><span class="sxs-lookup"><span data-stu-id="c6c30-208">VM Access extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
