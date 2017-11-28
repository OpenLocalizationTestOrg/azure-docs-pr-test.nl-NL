---
title: aaaVirtual machine extensies en functies voor Linux | Microsoft Docs
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
ms.openlocfilehash: e0d2ce794c76815ccc6743e8788ee5d9d931e9a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a><span data-ttu-id="10190-103">Uitbreidingen van de virtuele machine en functies voor Linux</span><span class="sxs-lookup"><span data-stu-id="10190-103">Virtual machine extensions and features for Linux</span></span>

<span data-ttu-id="10190-104">Virtuele machine van Azure-extensies zijn kleine toepassingen waarmee de configuratie en automatisering taken na de implementatie op virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="10190-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="10190-105">Als een virtuele machine vereist een software-installatie, beveiliging tegen virussen of Docker-configuratie, een VM-extensie kan bijvoorbeeld worden gebruikt toocomplete deze taken.</span><span class="sxs-lookup"><span data-stu-id="10190-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used toocomplete these tasks.</span></span> <span data-ttu-id="10190-106">Azure VM-extensies kunnen worden uitgevoerd met hello Azure CLI, Azure Resource Manager-sjablonen, PowerShell en hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="10190-106">Azure VM extensions can be run using hello Azure CLI, PowerShell, Azure Resource Manager templates, and hello Azure portal.</span></span> <span data-ttu-id="10190-107">Extensies worden gebundeld met een nieuwe implementatie van de virtuele machine of eventuele bestaande systeem uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="10190-107">Extensions can be bundled with a new virtual machine deployment, or run against any existing system.</span></span>

<span data-ttu-id="10190-108">Dit document bevat een overzicht van de VM-extensies voor vereisten voor het gebruik van Azure VM-extensies en richtlijnen over hoe toodetect, beheren en verwijderen van de VM-extensies.</span><span class="sxs-lookup"><span data-stu-id="10190-108">This document provides an overview of VM extensions, prerequisites for using Azure VM extensions, and guidance on how toodetect, manage, and remove VM extensions.</span></span> <span data-ttu-id="10190-109">Dit document vindt u algemene informatie omdat veel VM-extensies beschikbaar zijn, elk met een potentieel unieke configuratie.</span><span class="sxs-lookup"><span data-stu-id="10190-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="10190-110">Extensie-specifieke informatie vindt u in elke afzonderlijke document specifieke toohello-extensie.</span><span class="sxs-lookup"><span data-stu-id="10190-110">Extension-specific details can be found in each document specific toohello individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="10190-111">Gebruiksvoorbeelden en voorbeelden</span><span class="sxs-lookup"><span data-stu-id="10190-111">Use cases and samples</span></span>

<span data-ttu-id="10190-112">Enkele andere Azure VM-extensies beschikbaar zijn, elk met een specifieke gebruiksvoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="10190-112">Several different Azure VM extensions are available, each with a specific use case.</span></span> <span data-ttu-id="10190-113">Een aantal voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="10190-113">Some examples are:</span></span>

- <span data-ttu-id="10190-114">Status van PowerShell gewenste configuraties tooa virtuele machine met behulp van Hallo DSC-extensie voor Linux toepassen.</span><span class="sxs-lookup"><span data-stu-id="10190-114">Apply PowerShell Desired State configurations tooa virtual machine using hello DSC extension for Linux.</span></span> <span data-ttu-id="10190-115">Zie voor meer informatie [Azure gewenst State configuration-uitbreiding](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span><span class="sxs-lookup"><span data-stu-id="10190-115">For more information, see [Azure Desired State configuration extension](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span></span>
- <span data-ttu-id="10190-116">Bewaking van een virtuele machine met Microsoft Monitoring Agent VM-extensie Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="10190-116">Configure monitoring of a virtual machine with hello Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="10190-117">Zie voor meer informatie [hoe toomonitor een Linux-VM](tutorial-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="10190-117">For more information, see [How toomonitor a Linux VM](tutorial-monitoring.md).</span></span>
- <span data-ttu-id="10190-118">Bewaking van uw Azure-infrastructuur met Hallo Datadog-uitbreiding configureren.</span><span class="sxs-lookup"><span data-stu-id="10190-118">Configure monitoring of your Azure infrastructure with hello Datadog extension.</span></span> <span data-ttu-id="10190-119">Zie voor meer informatie, Hallo [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="10190-119">For more information, see hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="10190-120">Configureer een Docker-host op een virtuele machine van Azure met behulp van Hallo Docker VM-extensie.</span><span class="sxs-lookup"><span data-stu-id="10190-120">Configure a Docker host on an Azure virtual machine using hello Docker VM extension.</span></span> <span data-ttu-id="10190-121">Zie voor meer informatie [Docker VM-extensie](dockerextension.md).</span><span class="sxs-lookup"><span data-stu-id="10190-121">For more information, see [Docker VM extension](dockerextension.md).</span></span>

<span data-ttu-id="10190-122">Bovendien tooprocess-specifieke uitbreidingen, een extensie voor aangepaste scripts is beschikbaar voor Windows- en Linux virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="10190-122">In addition tooprocess-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="10190-123">Hallo-extensie voor aangepaste scripts voor Linux kunt eventuele Bash script toobe uitvoeren op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="10190-123">hello Custom Script extension for Linux allows any Bash script toobe run on a virtual machine.</span></span> <span data-ttu-id="10190-124">Aangepaste scripts zijn handig voor het ontwerpen van Azure-implementaties die moeten worden geconfigureerd afgezien van wat systeemeigen Azure tooling kan bieden.</span><span class="sxs-lookup"><span data-stu-id="10190-124">Custom scripts are useful for designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="10190-125">Zie voor meer informatie [Linux VM aangepaste scriptextensie](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="10190-125">For more information, see [Linux VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="10190-126">Vereisten</span><span class="sxs-lookup"><span data-stu-id="10190-126">Prerequisites</span></span>

<span data-ttu-id="10190-127">De extensie van elke virtuele machine mogelijk een eigen set vereisten.</span><span class="sxs-lookup"><span data-stu-id="10190-127">Each virtual machine extension might have its own set of prerequisites.</span></span> <span data-ttu-id="10190-128">Hallo Docker VM-extensie heeft bijvoorbeeld een vereiste van een ondersteunde Linux-distributie.</span><span class="sxs-lookup"><span data-stu-id="10190-128">For instance, hello Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="10190-129">Vereisten van afzonderlijke uitbreidingen zijn aangegeven in het Hallo-extensie-specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="10190-129">Requirements of individual extensions are detailed in hello extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="10190-130">Azure VM-agent</span><span class="sxs-lookup"><span data-stu-id="10190-130">Azure VM agent</span></span>

<span data-ttu-id="10190-131">Hello Azure VM-agent beheert interactie tussen een virtuele machine van Azure en hello Azure-infrastructuurcontroller.</span><span class="sxs-lookup"><span data-stu-id="10190-131">hello Azure VM agent manages interactions between an Azure virtual machine and hello Azure fabric controller.</span></span> <span data-ttu-id="10190-132">Hallo VM-agent is verantwoordelijk voor veel functionele aspecten van het implementeren en beheren van virtuele machines in Azure, waaronder het uitvoeren van de VM-extensies.</span><span class="sxs-lookup"><span data-stu-id="10190-132">hello VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="10190-133">Hello Azure VM-agent is geïnstalleerd op Azure Marketplace-installatiekopieën en kan handmatig worden geïnstalleerd op ondersteunde besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="10190-133">hello Azure VM agent is preinstalled on Azure Marketplace images and can be installed manually on supported operating systems.</span></span>

<span data-ttu-id="10190-134">Zie voor informatie over ondersteunde besturingssystemen en installatie-instructies, [virtuele machine van Azure-agent](../windows/classic/agents-and-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="10190-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](../windows/classic/agents-and-extensions.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="10190-135">VM-extensies detecteren</span><span class="sxs-lookup"><span data-stu-id="10190-135">Discover VM extensions</span></span>

<span data-ttu-id="10190-136">Veel andere VM-extensies zijn beschikbaar voor gebruik met virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="10190-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="10190-137">toosee een volledige lijst Hallo de volgende opdracht met hello Azure CLI, Hallo Voorbeeldlocatie vervangen door een Hallo-locatie van uw keuze uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="10190-137">toosee a complete list, run hello following command with hello Azure CLI, replacing hello example location with hello location of your choice.</span></span>

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a><span data-ttu-id="10190-138">VM-extensies worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="10190-138">Run VM extensions</span></span>

<span data-ttu-id="10190-139">Uitbreidingen van de virtuele machine van Azure kunnen worden uitgevoerd op de bestaande virtuele machines, die handig zijn als u de verbinding op een reeds geïmplementeerde virtuele machine herstellen of toomake configuratiewijzigingen nodig.</span><span class="sxs-lookup"><span data-stu-id="10190-139">Azure virtual machine extensions can be run on existing virtual machines, which are useful when you need toomake configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="10190-140">VM-extensies kunnen ook worden gebundeld met implementaties van Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="10190-140">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="10190-141">Via uitbreidingen met Resource Manager-sjablonen kunnen virtuele machines in Azure worden geïmplementeerd en geconfigureerd zonder tussenkomst van de na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="10190-141">By using extensions with Resource Manager templates, Azure virtual machines can be deployed and configured without post-deployment intervention.</span></span>

<span data-ttu-id="10190-142">Hallo volgende methoden kan worden gebruikt toorun een uitbreiding op basis van een bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="10190-142">hello following methods can be used toorun an extension against an existing virtual machine.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="10190-143">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="10190-143">Azure CLI</span></span>

<span data-ttu-id="10190-144">Uitbreidingen van de virtuele machine van Azure kunnen worden uitgevoerd op basis van een bestaande virtuele machine met behulp van Hallo `az vm extension set` opdracht.</span><span class="sxs-lookup"><span data-stu-id="10190-144">Azure virtual machine extensions can be run against an existing virtual machine by using hello `az vm extension set` command.</span></span> <span data-ttu-id="10190-145">In dit voorbeeld voert Hallo-extensie voor aangepaste scripts op basis van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="10190-145">This example runs hello custom script extension against a virtual machine.</span></span>

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

<span data-ttu-id="10190-146">Hallo script produceert uitvoer vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="10190-146">hello script produces output similar toohello following text:</span></span>

```azurecli
info:    Executing command vm extension set
+ Looking up hello VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a><span data-ttu-id="10190-147">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="10190-147">Azure portal</span></span>

<span data-ttu-id="10190-148">VM-extensies mag toegepaste tooan bestaande virtuele machine via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="10190-148">VM extensions can be applied tooan existing virtual machine through hello Azure portal.</span></span> <span data-ttu-id="10190-149">toodo hello virtuele machine, dus selecteer kiezen **extensies**, en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="10190-149">toodo so, select hello virtual machine, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="10190-150">Hallo-extensie gewenste uit Hallo lijst met beschikbare uitbreidingen en Hallo-instructies in de wizard Hallo selecteren.</span><span class="sxs-lookup"><span data-stu-id="10190-150">Select hello extension you want from hello list of available extensions and follow hello instructions in hello wizard.</span></span>

<span data-ttu-id="10190-151">Hallo toont volgende afbeelding Hallo-installatie van Hallo Linux aangepaste scriptextensie van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="10190-151">hello following image shows hello installation of hello Linux Custom Script extension from hello Azure portal.</span></span>

![Extensie voor aangepaste scripts installeren](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="10190-153">Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="10190-153">Azure Resource Manager templates</span></span>

<span data-ttu-id="10190-154">VM-extensies kunnen toegevoegde tooan Azure Resource Manager-sjabloon en uitgevoerd met de implementatie van de sjabloon Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="10190-154">VM extensions can be added tooan Azure Resource Manager template and executed with hello deployment of hello template.</span></span> <span data-ttu-id="10190-155">Wanneer u een uitbreiding met een sjabloon implementeert, kunt u volledig geconfigureerde Azure-implementaties.</span><span class="sxs-lookup"><span data-stu-id="10190-155">When you deploy an extension with a template, you can create fully configured Azure deployments.</span></span> <span data-ttu-id="10190-156">Bijvoorbeeld: hello die volgende JSON is genomen van de Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="10190-156">For example, hello following JSON is taken from a Resource Manager template.</span></span> <span data-ttu-id="10190-157">Hallo sjabloon implementeert een set van netwerktaakverdeling virtuele machines en een Azure SQL database, en installeert een toepassing .NET Core op elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="10190-157">hello template deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="10190-158">Hallo VM-extensie zorgt voor Hallo software-installatie.</span><span class="sxs-lookup"><span data-stu-id="10190-158">hello VM extension takes care of hello software installation.</span></span>

<span data-ttu-id="10190-159">Zie voor meer informatie, Hallo volledige [Resource Manager-sjabloon](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="10190-159">For more information, see hello full [Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

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

<span data-ttu-id="10190-160">Zie voor meer informatie [Azure Resource Manager-sjablonen samenstellen](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span><span class="sxs-lookup"><span data-stu-id="10190-160">For more information, see [Authoring Azure Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="10190-161">Beveiligde gegevens van de VM-extensie</span><span class="sxs-lookup"><span data-stu-id="10190-161">Secure VM extension data</span></span>

<span data-ttu-id="10190-162">Wanneer u een VM-extensie uitvoert, kan het benodigde tooinclude gevoelige informatie zoals referenties, namen van opslagaccounts en toegang tot de opslagaccountsleutels zijn.</span><span class="sxs-lookup"><span data-stu-id="10190-162">When you're running a VM extension, it may be necessary tooinclude sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="10190-163">Veel VM-extensies bevatten een beveiligde configuratie die gegevens versleutelt en ontsleutelt deze alleen in de virtuele doelmachine Hallo.</span><span class="sxs-lookup"><span data-stu-id="10190-163">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside hello target virtual machine.</span></span> <span data-ttu-id="10190-164">Elke uitbreiding heeft een specifieke beveiligde configuratieschema en elk wordt beschreven in de uitbreiding specifieke documentatie bij.</span><span class="sxs-lookup"><span data-stu-id="10190-164">Each extension has a specific protected configuration schema, and each is detailed in extension-specific documentation.</span></span>

<span data-ttu-id="10190-165">Hallo volgende voorbeeld ziet u een exemplaar van de aangepaste scriptextensie Hallo voor Linux.</span><span class="sxs-lookup"><span data-stu-id="10190-165">hello following example shows an instance of hello Custom Script extension for Linux.</span></span> <span data-ttu-id="10190-166">U ziet dat tooexecute Hallo-opdracht bevat een set referenties.</span><span class="sxs-lookup"><span data-stu-id="10190-166">Notice that hello command tooexecute includes a set of credentials.</span></span> <span data-ttu-id="10190-167">In dit voorbeeld Hallo opdracht tooexecute niet versleuteld.</span><span class="sxs-lookup"><span data-stu-id="10190-167">In this example, hello command tooexecute will not be encrypted.</span></span>


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

<span data-ttu-id="10190-168">Zwevend Hallo **opdracht tooexecute** eigenschap toohello **beveiligd** configuratie beveiligt Hallo uitvoering tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="10190-168">Moving hello **command tooexecute** property toohello **protected** configuration secures hello execution string.</span></span>

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

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="10190-169">VM-extensies oplossen</span><span class="sxs-lookup"><span data-stu-id="10190-169">Troubleshoot VM extensions</span></span>

<span data-ttu-id="10190-170">Elk VM-extensie wellicht stappen specifieke toohello extensie probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="10190-170">Each VM extension may have troubleshooting steps specific toohello extension.</span></span> <span data-ttu-id="10190-171">Bijvoorbeeld, wanneer u Hallo aangepaste scriptextensie, script uitvoering details zijn te vinden lokaal op Hallo virtuele machine waarop Hallo-extensie is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="10190-171">For example, when you're using hello Custom Script extension, script execution details can be found locally on hello virtual machine on which hello extension was run.</span></span> <span data-ttu-id="10190-172">Probleemoplossing-extensie-specifieke worden beschreven in de documentatie van de extensie-specifieke.</span><span class="sxs-lookup"><span data-stu-id="10190-172">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="10190-173">Hallo volgende stappen voor probleemoplossing toepassing tooall-extensies voor virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="10190-173">hello following troubleshooting steps apply tooall virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="10190-174">Status van de extensie weergeven</span><span class="sxs-lookup"><span data-stu-id="10190-174">View extension status</span></span>

<span data-ttu-id="10190-175">Nadat u de extensie van een virtuele machine is uitgevoerd voor een virtuele machine, gebruik Hallo status van de Azure CLI opdracht tooreturn-extensie te volgen.</span><span class="sxs-lookup"><span data-stu-id="10190-175">After a virtual machine extension has been run against a virtual machine, use hello following Azure CLI command tooreturn extension status.</span></span> <span data-ttu-id="10190-176">Parameternamen voorbeeld vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="10190-176">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="10190-177">Hallo-uitvoer ziet er Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="10190-177">hello output looks like hello following text:</span></span>

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

<span data-ttu-id="10190-178">Status van extensie-uitvoering kan worden gevonden in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="10190-178">Extension execution status can also be found in hello Azure portal.</span></span> <span data-ttu-id="10190-179">tooview hello status van een extensie, selecteer Hallo virtuele machine kiezen **extensies**, en selecteer de gewenste extensie Hallo.</span><span class="sxs-lookup"><span data-stu-id="10190-179">tooview hello status of an extension, select hello virtual machine, choose **Extensions**, and select hello desired extension.</span></span>

### <a name="rerun-a-vm-extension"></a><span data-ttu-id="10190-180">Voer een VM-extensie</span><span class="sxs-lookup"><span data-stu-id="10190-180">Rerun a VM extension</span></span>

<span data-ttu-id="10190-181">Mogelijk zijn er gevallen waarin de extensie van een virtuele machine toobe moet opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="10190-181">There may be cases in which a virtual machine extension needs toobe rerun.</span></span> <span data-ttu-id="10190-182">U kunt een uitbreiding opnieuw uitvoeren te verwijderen en vervolgens opnieuw uit te voeren Hallo-extensie met een methode van de uitvoering van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="10190-182">You can rerun an extension by removing it, and then rerunning hello extension with an execution method of your choice.</span></span> <span data-ttu-id="10190-183">tooremove een uitbreiding Hallo volgende opdracht met hello Azure CLI uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="10190-183">tooremove an extension, run hello following command with hello Azure CLI.</span></span> <span data-ttu-id="10190-184">Parameternamen voorbeeld vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="10190-184">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

<span data-ttu-id="10190-185">U kunt een uitbreiding verwijderen met behulp van Hallo stappen te volgen in hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="10190-185">You can remove an extension by using hello following steps in hello Azure portal:</span></span>

1. <span data-ttu-id="10190-186">Selecteer een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="10190-186">Select a virtual machine.</span></span>
2. <span data-ttu-id="10190-187">Kies **extensies**.</span><span class="sxs-lookup"><span data-stu-id="10190-187">Choose **Extensions**.</span></span>
3. <span data-ttu-id="10190-188">Selecteer Hallo gewenste extensie.</span><span class="sxs-lookup"><span data-stu-id="10190-188">Select hello desired extension.</span></span>
4. <span data-ttu-id="10190-189">Kies **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="10190-189">Choose **Uninstall**.</span></span>

## <a name="common-vm-extension-reference"></a><span data-ttu-id="10190-190">Algemene referentie voor VM-extensie</span><span class="sxs-lookup"><span data-stu-id="10190-190">Common VM extension reference</span></span>
| <span data-ttu-id="10190-191">Naam van de uitbreiding</span><span class="sxs-lookup"><span data-stu-id="10190-191">Extension name</span></span> | <span data-ttu-id="10190-192">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="10190-192">Description</span></span> | <span data-ttu-id="10190-193">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="10190-193">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="10190-194">Extensie voor aangepaste scripts voor Linux</span><span class="sxs-lookup"><span data-stu-id="10190-194">Custom Script extension for Linux</span></span> |<span data-ttu-id="10190-195">Scripts uitvoeren op een virtuele machine van Azure</span><span class="sxs-lookup"><span data-stu-id="10190-195">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="10190-196">Extensie voor aangepaste scripts voor Linux</span><span class="sxs-lookup"><span data-stu-id="10190-196">Custom Script extension for Linux</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="10190-197">Docker-uitbreiding</span><span class="sxs-lookup"><span data-stu-id="10190-197">Docker extension</span></span> |<span data-ttu-id="10190-198">Hallo Docker-daemon toosupport externe Docker opdrachten installeren.</span><span class="sxs-lookup"><span data-stu-id="10190-198">Install hello Docker daemon toosupport remote Docker commands.</span></span> |[<span data-ttu-id="10190-199">Docker-VM-extensie</span><span class="sxs-lookup"><span data-stu-id="10190-199">Docker VM extension</span></span>](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="10190-200">VM-extensie voor toegang</span><span class="sxs-lookup"><span data-stu-id="10190-200">VM Access extension</span></span> |<span data-ttu-id="10190-201">Toegang tooan Azure virtuele machine herstellen</span><span class="sxs-lookup"><span data-stu-id="10190-201">Regain access tooan Azure virtual machine</span></span> |[<span data-ttu-id="10190-202">VM-extensie voor toegang</span><span class="sxs-lookup"><span data-stu-id="10190-202">VM Access extension</span></span>](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| <span data-ttu-id="10190-203">Azure extensie voor diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="10190-203">Azure Diagnostics extension</span></span> |<span data-ttu-id="10190-204">Azure Diagnostics beheren</span><span class="sxs-lookup"><span data-stu-id="10190-204">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="10190-205">Azure extensie voor diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="10190-205">Azure Diagnostics extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="10190-206">De extensie Azure VM-toegang</span><span class="sxs-lookup"><span data-stu-id="10190-206">Azure VM Access extension</span></span> |<span data-ttu-id="10190-207">Gebruikers en referenties beheren</span><span class="sxs-lookup"><span data-stu-id="10190-207">Manage users and credentials</span></span> |[<span data-ttu-id="10190-208">Uitbreiding van de VM-toegang voor Linux</span><span class="sxs-lookup"><span data-stu-id="10190-208">VM Access extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
