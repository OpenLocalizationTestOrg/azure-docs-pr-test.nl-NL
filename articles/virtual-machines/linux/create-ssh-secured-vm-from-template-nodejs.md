---
title: een Linux-VM met een Azure-sjabloon met Azure CLI 1.0 aaaCreate | Microsoft Docs
description: Maak een Linux-VM op Azure met behulp van hello Azure CLI 1.0- en een Azure Resource Manager-sjabloon.
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
ms.openlocfilehash: b694cc8247a8431b7ef4b24cc7dc2b4cdb9660ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a><span data-ttu-id="01dac-103">Hoe toocreate een Linux-VM met behulp van Azure CLI 1.0 een Azure Resource Manager-sjabloon Hallo</span><span class="sxs-lookup"><span data-stu-id="01dac-103">How toocreate a Linux VM using hello Azure CLI 1.0 an Azure Resource Manager template</span></span>
<span data-ttu-id="01dac-104">Dit artikel laat zien hoe tooquickly implementeren voor een virtuele Linux-Machine met behulp van hello Azure CLI 1.0 en een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="01dac-104">This article shows you how tooquickly deploy a Linux Virtual Machine using hello Azure CLI 1.0 and an Azure Resource Manager template.</span></span> <span data-ttu-id="01dac-105">Hallo artikel is vereist:</span><span class="sxs-lookup"><span data-stu-id="01dac-105">hello article requires:</span></span>

* <span data-ttu-id="01dac-106">een Azure-account ([probeer een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/))</span><span class="sxs-lookup"><span data-stu-id="01dac-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="01dac-107">Hallo [Azure CLI 1.0](../../cli-install-nodejs.md) aangemeld `azure login`.</span><span class="sxs-lookup"><span data-stu-id="01dac-107">hello [Azure CLI 1.0](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="01dac-108">Hello Azure CLI *moet* modus Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="01dac-108">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

<span data-ttu-id="01dac-109">U kunt ook snel een Linux-VM-sjabloon implementeren met behulp van Hallo [Azure-portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="01dac-109">You can also quickly deploy a Linux VM template by using hello [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="01dac-110">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="01dac-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="01dac-111">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="01dac-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="01dac-112">[Azure CLI 1.0](#quick-command-summary) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="01dac-112">[Azure CLI 1.0](#quick-command-summary) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="01dac-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="01dac-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="01dac-114">Beknopt overzicht van opdrachten</span><span class="sxs-lookup"><span data-stu-id="01dac-114">Quick Command Summary</span></span>
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="01dac-115">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="01dac-115">Detailed Walkthrough</span></span>
<span data-ttu-id="01dac-116">Sjablonen kunt u toocreate virtuele machines in Azure met instellingen die u wilt de toocustomize tijdens Hallo starten, instellingen, zoals gebruikersnamen en hostnamen.</span><span class="sxs-lookup"><span data-stu-id="01dac-116">Templates allow you toocreate VMs on Azure with settings that you want toocustomize during hello launch, settings like usernames and hostnames.</span></span> <span data-ttu-id="01dac-117">Voor dit artikel starten we een Azure-sjabloon waarbij we gebruikmaken van een Ubuntu VM en een netwerkbeveiligingsgroep (NSG) waarbij poort 22 is geopend voor SSH .</span><span class="sxs-lookup"><span data-stu-id="01dac-117">For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.</span></span>

<span data-ttu-id="01dac-118">Azure Resource Manager-sjablonen zijn JSON-bestanden die kunnen worden gebruikt voor eenvoudige eenmalige taken, zoals het starten van een Ubuntu VM zoals in dit artikel wordt gedaan.</span><span class="sxs-lookup"><span data-stu-id="01dac-118">Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.</span></span>  <span data-ttu-id="01dac-119">Azure-sjablonen kunnen ook worden gebruikt tooconstruct complexe Azure configuraties voor de volledige omgeving een stack testen, ontwikkeling of productie-implementatie.</span><span class="sxs-lookup"><span data-stu-id="01dac-119">Azure Templates can also be used tooconstruct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.</span></span>

## <a name="create-hello-linux-vm"></a><span data-ttu-id="01dac-120">Hallo Linux VM maken</span><span class="sxs-lookup"><span data-stu-id="01dac-120">Create hello Linux VM</span></span>
<span data-ttu-id="01dac-121">Hallo van de volgende code voorbeeld ziet u hoe toocall `azure group create` toocreate een bron groeperen en een Linux-VM SSH beveiligde op Hallo implementeren met behulp van dezelfde tijd [deze Azure Resource Manager-sjabloon](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="01dac-121">hello following code example shows how toocall `azure group create` toocreate a resource group and deploy an SSH-secured Linux VM at hello same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span></span> <span data-ttu-id="01dac-122">Vergeet niet dat in uw voorbeeld moet u toouse namen die unieke tooyour omgeving.</span><span class="sxs-lookup"><span data-stu-id="01dac-122">Remember that in your example you need toouse names that are unique tooyour environment.</span></span> <span data-ttu-id="01dac-123">In dit voorbeeld wordt *myResourceGroup* als naam resourcegroep hello, en *myVM* als Hallo VM-naam.</span><span class="sxs-lookup"><span data-stu-id="01dac-123">This example uses *myResourceGroup* as hello resource group name, and *myVM* as hello VM name.</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

<span data-ttu-id="01dac-124">Hallo-uitvoer moet eruitzien als Hallo uitvoerblok te volgen:</span><span class="sxs-lookup"><span data-stu-id="01dac-124">hello output should look like hello following output block:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for hello following parameters
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

<span data-ttu-id="01dac-125">In dat geval een VM die gebruikmaakt van Hallo geïmplementeerd `--template-uri` parameter.</span><span class="sxs-lookup"><span data-stu-id="01dac-125">That example deployed a VM using hello `--template-uri` parameter.</span></span>  <span data-ttu-id="01dac-126">U kunt ook downloaden of lokaal een sjabloon maken en doorgeven met Hallo Hallo-sjabloon `--template-file` parameter met een pad toohello sjabloonbestand als argument.</span><span class="sxs-lookup"><span data-stu-id="01dac-126">You can also download or create a template locally and pass hello template using hello `--template-file` parameter with a path toohello template file as an argument.</span></span> <span data-ttu-id="01dac-127">Hello Azure CLI vraagt u om de vereiste door Hallo sjabloon Hallo-parameters.</span><span class="sxs-lookup"><span data-stu-id="01dac-127">hello Azure CLI prompts you for hello parameters required by hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01dac-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="01dac-128">Next steps</span></span>
<span data-ttu-id="01dac-129">Zoeken Hallo [sjablonengalerie](https://azure.microsoft.com/documentation/templates/) toodiscover welke app-frameworks toodeploy volgende.</span><span class="sxs-lookup"><span data-stu-id="01dac-129">Search hello [templates gallery](https://azure.microsoft.com/documentation/templates/) toodiscover what app frameworks toodeploy next.</span></span>

