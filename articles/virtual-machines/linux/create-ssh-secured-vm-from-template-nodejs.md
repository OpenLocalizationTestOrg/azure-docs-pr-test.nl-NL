---
title: Maak een Linux-VM met een Azure-sjabloon met Azure CLI 1.0 | Microsoft Docs
description: Linux-VM in Azure met behulp van de Azure CLI 1.0 en een Azure Resource Manager-sjabloon maken.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 33d4aaa78fcdf3bd9e2e236606f2d3049f464a8a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-vm-using-the-azure-cli-10-an-azure-resource-manager-template"></a><span data-ttu-id="b66e3-103">Het maken van een Azure Resource Manager-sjabloon voor een Linux-VM met behulp van de Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="b66e3-103">How to create a Linux VM using the Azure CLI 1.0 an Azure Resource Manager template</span></span>
<span data-ttu-id="b66e3-104">In dit artikel laat zien hoe snel een virtuele Linux-Machine met behulp van de Azure CLI 1.0 en een Azure Resource Manager-sjabloon te implementeren.</span><span class="sxs-lookup"><span data-stu-id="b66e3-104">This article shows you how to quickly deploy a Linux Virtual Machine using the Azure CLI 1.0 and an Azure Resource Manager template.</span></span> <span data-ttu-id="b66e3-105">Het artikel schrijft het volgende als vereiste voor:</span><span class="sxs-lookup"><span data-stu-id="b66e3-105">The article requires:</span></span>

* <span data-ttu-id="b66e3-106">een Azure-account ([probeer een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/))</span><span class="sxs-lookup"><span data-stu-id="b66e3-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="b66e3-107">de [Azure CLI 1.0](../../cli-install-nodejs.md) aangemeld `azure login`.</span><span class="sxs-lookup"><span data-stu-id="b66e3-107">the [Azure CLI 1.0](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="b66e3-108">de Azure-CLI *moet in de* Azure Resource Manager-modus`azure config mode arm` staan.</span><span class="sxs-lookup"><span data-stu-id="b66e3-108">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

<span data-ttu-id="b66e3-109">U kunt een Linux-VM-sjabloon ook snel implementeren met behulp van de [Azure Portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b66e3-109">You can also quickly deploy a Linux VM template by using the [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="b66e3-110">CLI-versies om de taak uit te voeren</span><span class="sxs-lookup"><span data-stu-id="b66e3-110">CLI versions to complete the task</span></span>
<span data-ttu-id="b66e3-111">U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:</span><span class="sxs-lookup"><span data-stu-id="b66e3-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="b66e3-112">[Azure CLI 1.0](#quick-command-summary) – onze CLI voor het klassieke en resource management-implementatiemodel (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="b66e3-112">[Azure CLI 1.0](#quick-command-summary) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="b66e3-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md): onze CLI van de volgende generatie voor het Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="b66e3-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="b66e3-114">Beknopt overzicht van opdrachten</span><span class="sxs-lookup"><span data-stu-id="b66e3-114">Quick Command Summary</span></span>
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="b66e3-115">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="b66e3-115">Detailed Walkthrough</span></span>
<span data-ttu-id="b66e3-116">Met sjablonen kunt u in Azure virtuele machines maken met instellingen die u tijdens het starten wilt aanpassen, zoals gebruikersnamen en hostnamen.</span><span class="sxs-lookup"><span data-stu-id="b66e3-116">Templates allow you to create VMs on Azure with settings that you want to customize during the launch, settings like usernames and hostnames.</span></span> <span data-ttu-id="b66e3-117">Voor dit artikel starten we een Azure-sjabloon waarbij we gebruikmaken van een Ubuntu VM en een netwerkbeveiligingsgroep (NSG) waarbij poort 22 is geopend voor SSH .</span><span class="sxs-lookup"><span data-stu-id="b66e3-117">For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.</span></span>

<span data-ttu-id="b66e3-118">Azure Resource Manager-sjablonen zijn JSON-bestanden die kunnen worden gebruikt voor eenvoudige eenmalige taken, zoals het starten van een Ubuntu VM zoals in dit artikel wordt gedaan.</span><span class="sxs-lookup"><span data-stu-id="b66e3-118">Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.</span></span>  <span data-ttu-id="b66e3-119">Azure-sjablonen kunnen ook worden gebruikt om complexe Azure-configuraties te maken van volledige omgevingen, zoals een test-, ontwikkelings- of productie-implementatiestack.</span><span class="sxs-lookup"><span data-stu-id="b66e3-119">Azure Templates can also be used to construct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.</span></span>

## <a name="create-the-linux-vm"></a><span data-ttu-id="b66e3-120">De virtuele Linux-machine maken</span><span class="sxs-lookup"><span data-stu-id="b66e3-120">Create the Linux VM</span></span>
<span data-ttu-id="b66e3-121">De volgende voorbeeldcode laat zien hoe u `azure group create` aanroept om een resourcegroep te maken en op hetzelfde moment een met SSH beveiligde virtuele Linux-machine te implementeren met behulp van [deze Azure Resource Manager-sjabloon](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="b66e3-121">The following code example shows how to call `azure group create` to create a resource group and deploy an SSH-secured Linux VM at the same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span></span> <span data-ttu-id="b66e3-122">Vergeet niet om voor de implementatie namen te gebruiken die uniek zijn voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="b66e3-122">Remember that in your example you need to use names that are unique to your environment.</span></span> <span data-ttu-id="b66e3-123">In dit voorbeeld wordt *myResourceGroup* als de naam van de resourcegroep, en *myVM* als de naam van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b66e3-123">This example uses *myResourceGroup* as the resource group name, and *myVM* as the VM name.</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

<span data-ttu-id="b66e3-124">Uw uitvoer moet eruitzien als in het volgende uitvoerblok:</span><span class="sxs-lookup"><span data-stu-id="b66e3-124">The output should look like the following output block:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for the following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="b66e3-125">In dat voorbeeld werd een virtuele machine geïmplementeerd met de parameter `--template-uri`.</span><span class="sxs-lookup"><span data-stu-id="b66e3-125">That example deployed a VM using the `--template-uri` parameter.</span></span>  <span data-ttu-id="b66e3-126">U kunt ook een sjabloon downloaden of lokaal een sjabloon maken en deze sjabloon vervolgens doorgeven met behulp van de parameter `--template-file`. Hierbij neemt u het pad naar het sjabloonbestand op als argument.</span><span class="sxs-lookup"><span data-stu-id="b66e3-126">You can also download or create a template locally and pass the template using the `--template-file` parameter with a path to the template file as an argument.</span></span> <span data-ttu-id="b66e3-127">De Azure CLI vraagt u om de parameters die vereist zijn voor de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="b66e3-127">The Azure CLI prompts you for the parameters required by the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b66e3-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b66e3-128">Next steps</span></span>
<span data-ttu-id="b66e3-129">Doorzoek de [Sjablonengalerie](https://azure.microsoft.com/documentation/templates/) om te bekijken welke app-frameworks u hierna wilt gaan implementeren.</span><span class="sxs-lookup"><span data-stu-id="b66e3-129">Search the [templates gallery](https://azure.microsoft.com/documentation/templates/) to discover what app frameworks to deploy next.</span></span>

