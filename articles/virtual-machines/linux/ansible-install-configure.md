---
title: aaaInstall en Ansible configureren voor gebruik met virtuele machines in Azure | Microsoft Docs
description: Meer informatie over hoe tooinstall en Ansible configureren voor het beheren van Azure-resources op Ubuntu en CentOS SLES
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/25/2017
ms.author: iainfou
ms.openlocfilehash: b33d1893909b6134a5474617c9af2d6e4f627c05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-ansible-toomanage-virtual-machines-in-azure"></a><span data-ttu-id="64bb2-103">Installeren en configureren van Ansible toomanage virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="64bb2-103">Install and configure Ansible toomanage virtual machines in Azure</span></span>
<span data-ttu-id="64bb2-104">Dit artikel wordt uitgelegd hoe tooinstall Ansible en vereist Azure Python SDK-modules voor een aantal Hallo meest voorkomende Linux-distributies.</span><span class="sxs-lookup"><span data-stu-id="64bb2-104">This article details how tooinstall Ansible and required Azure Python SDK modules for some of hello most common Linux distros.</span></span> <span data-ttu-id="64bb2-105">U kunt installeren Ansible op andere distributies door aan te passen geïnstalleerd hello-pakketten toofit uw bepaald platform.</span><span class="sxs-lookup"><span data-stu-id="64bb2-105">You can install Ansible on other distros by adjusting hello installed packages toofit your particular platform.</span></span> <span data-ttu-id="64bb2-106">toocreate Azure bronnen op een veilige manier u leert ook hoe toocreate en referenties voor Ansible toouse definiëren.</span><span class="sxs-lookup"><span data-stu-id="64bb2-106">toocreate Azure resources in a secure manner, you also learn how toocreate and define credentials for Ansible toouse.</span></span> 

<span data-ttu-id="64bb2-107">Zie voor meer informatie over opties voor de installatie en stappen voor extra platforms Hallo [Ansible installatiehandleiding](https://docs.ansible.com/ansible/intro_installation.html).</span><span class="sxs-lookup"><span data-stu-id="64bb2-107">For more installation options and steps for additional platforms, see hello [Ansible install guide](https://docs.ansible.com/ansible/intro_installation.html).</span></span>


## <a name="install-ansible"></a><span data-ttu-id="64bb2-108">Ansible installeren</span><span class="sxs-lookup"><span data-stu-id="64bb2-108">Install Ansible</span></span>
<span data-ttu-id="64bb2-109">Maak eerst een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="64bb2-109">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="64bb2-110">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupAnsible* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="64bb2-110">hello following example creates a resource group named *myResourceGroupAnsible* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

<span data-ttu-id="64bb2-111">Nu een virtuele machine maken en installeer Ansible voor een Hallo distributies te volgen:</span><span class="sxs-lookup"><span data-stu-id="64bb2-111">Now create a VM and install Ansible for one of hello following distros:</span></span>

- [<span data-ttu-id="64bb2-112">Ubuntu 16.04 TNS</span><span class="sxs-lookup"><span data-stu-id="64bb2-112">Ubuntu 16.04 LTS</span></span>](#ubuntu1604-lts)
- [<span data-ttu-id="64bb2-113">7.3 centOS</span><span class="sxs-lookup"><span data-stu-id="64bb2-113">CentOS 7.3</span></span>](#centos-73)
- [<span data-ttu-id="64bb2-114">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="64bb2-114">SLES 12.2 SP2</span></span>](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="64bb2-115">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="64bb2-115">Ubuntu 16.04 LTS</span></span>
<span data-ttu-id="64bb2-116">Maak een VM met [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="64bb2-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="64bb2-117">Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="64bb2-117">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="64bb2-118">SSH tooyour met behulp van VM Hallo `publicIpAddress` hebt genoteerd in Hallo Maakbewerking van de uitvoer van Hallo VM:</span><span class="sxs-lookup"><span data-stu-id="64bb2-118">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="64bb2-119">Op de virtuele machine, vereist hello-pakketten voor hello Azure Python SDK-modules en Ansible als volgt te installeren:</span><span class="sxs-lookup"><span data-stu-id="64bb2-119">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev python-pip

## Install Azure SDKs via pip
pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via apt
sudo apt-get install -y software-properties-common
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt-get update && sudo apt-get install -y ansible
```

<span data-ttu-id="64bb2-120">Nu verder te[maken Azure-referenties](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="64bb2-120">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="centos-73"></a><span data-ttu-id="64bb2-121">7.3 centOS</span><span class="sxs-lookup"><span data-stu-id="64bb2-121">CentOS 7.3</span></span>
<span data-ttu-id="64bb2-122">Maak een VM met [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="64bb2-122">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="64bb2-123">Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="64bb2-123">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="64bb2-124">SSH tooyour met behulp van VM Hallo `publicIpAddress` hebt genoteerd in Hallo Maakbewerking van de uitvoer van Hallo VM:</span><span class="sxs-lookup"><span data-stu-id="64bb2-124">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="64bb2-125">Op de virtuele machine, vereist hello-pakketten voor hello Azure Python SDK-modules en Ansible als volgt te installeren:</span><span class="sxs-lookup"><span data-stu-id="64bb2-125">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

<span data-ttu-id="64bb2-126">Nu verder te[maken Azure-referenties](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="64bb2-126">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="sles-122-sp2"></a><span data-ttu-id="64bb2-127">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="64bb2-127">SLES 12.2 SP2</span></span>
<span data-ttu-id="64bb2-128">Maak een VM met [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="64bb2-128">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="64bb2-129">Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="64bb2-129">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="64bb2-130">SSH tooyour met behulp van VM Hallo `publicIpAddress` hebt genoteerd in Hallo Maakbewerking van de uitvoer van Hallo VM:</span><span class="sxs-lookup"><span data-stu-id="64bb2-130">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="64bb2-131">Op de virtuele machine, vereist hello-pakketten voor hello Azure Python SDK-modules en Ansible als volgt te installeren:</span><span class="sxs-lookup"><span data-stu-id="64bb2-131">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

<span data-ttu-id="64bb2-132">Nu verder te[maken Azure-referenties](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="64bb2-132">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


## <a name="create-azure-credentials"></a><span data-ttu-id="64bb2-133">Azure-referenties maken</span><span class="sxs-lookup"><span data-stu-id="64bb2-133">Create Azure credentials</span></span>
<span data-ttu-id="64bb2-134">Ansible communiceert met Azure met behulp van een gebruikersnaam en wachtwoord of een service-principal.</span><span class="sxs-lookup"><span data-stu-id="64bb2-134">Ansible communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="64bb2-135">Een Azure-service-principal is een beveiligings-id die u met apps, services en automatiseringsprogramma's zoals Ansible gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="64bb2-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Ansible.</span></span> <span data-ttu-id="64bb2-136">U bepaalt de en definieer Hallo machtigingen als toowhat operations Hallo service-principal in Azure uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="64bb2-136">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span> <span data-ttu-id="64bb2-137">tooimprove beveiliging via gewoon een gebruikersnaam en wachtwoord voor het bieden, in dit voorbeeld wordt een basic service principal.</span><span class="sxs-lookup"><span data-stu-id="64bb2-137">tooimprove security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="64bb2-138">Maken van een service principal met [az ad sp maken-voor-rbac](/cli/azure/ad/sp#create-for-rbac) en uitvoer Hallo de referenties die Ansible moet:</span><span class="sxs-lookup"><span data-stu-id="64bb2-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that Ansible needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="64bb2-139">Een voorbeeld van uitvoer Hallo van Hallo voorgaande opdrachten is als volgt:</span><span class="sxs-lookup"><span data-stu-id="64bb2-139">An example of hello output from hello preceding commands is as follows:</span></span>

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

<span data-ttu-id="64bb2-140">tooauthenticate tooAzure, moet u ook uw Azure-abonnement-ID met tooobtain [az account weergeven](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="64bb2-140">tooauthenticate tooAzure, you also need tooobtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="64bb2-141">U Hallo-uitvoer van deze twee opdrachten in de volgende stap hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="64bb2-141">You use hello output from these two commands in hello next step.</span></span>


## <a name="create-ansible-credentials-file"></a><span data-ttu-id="64bb2-142">Ansible referentiebestand maken</span><span class="sxs-lookup"><span data-stu-id="64bb2-142">Create Ansible credentials file</span></span>
<span data-ttu-id="64bb2-143">tooprovide tooAnsible referenties, u omgevingsvariabelen definiëren of maak een bestand lokale referenties.</span><span class="sxs-lookup"><span data-stu-id="64bb2-143">tooprovide credentials tooAnsible, you define environment variables or create a local credentials file.</span></span> <span data-ttu-id="64bb2-144">Voor meer informatie over het toodefine Ansible referenties, Zie [referenties bieden tooAzure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span><span class="sxs-lookup"><span data-stu-id="64bb2-144">For more information about how toodefine Ansible credentials, see [Providing Credentials tooAzure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span></span> 

<span data-ttu-id="64bb2-145">Voor een ontwikkelingsomgeving, maakt u een *referenties* voor Ansible bestand op de VM-host als volgt:</span><span class="sxs-lookup"><span data-stu-id="64bb2-145">For a development environment, create a *credentials* file for Ansible on your host VM as follows:</span></span>

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

<span data-ttu-id="64bb2-146">Hallo *referenties* bestand zelf Hallo abonnements-ID combineert met de Hallo-uitvoer van het maken van een service-principal.</span><span class="sxs-lookup"><span data-stu-id="64bb2-146">hello *credentials* file itself combines hello subscription ID with hello output of creating a service principal.</span></span> <span data-ttu-id="64bb2-147">De uitvoer van de vorige Hallo [az ad sp maken-voor-rbac](/cli/azure/ad/sp#create-for-rbac) opdracht is Hallo dezelfde volgorde nodig zijn voor *client_id*, *geheim*, en *tenant* .</span><span class="sxs-lookup"><span data-stu-id="64bb2-147">Output from hello previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is hello same order as needed for *client_id*, *secret*, and *tenant*.</span></span> <span data-ttu-id="64bb2-148">Hallo volgende voorbeeld *referenties* bestand ziet u deze waarden die overeenkomen met de vorige uitvoer Hallo.</span><span class="sxs-lookup"><span data-stu-id="64bb2-148">hello following example *credentials* file shows these values matching hello previous output.</span></span> <span data-ttu-id="64bb2-149">Voer uw eigen waarden als volgt:</span><span class="sxs-lookup"><span data-stu-id="64bb2-149">Enter your own values as follows:</span></span>

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a><span data-ttu-id="64bb2-150">Omgevingsvariabelen Ansible gebruiken</span><span class="sxs-lookup"><span data-stu-id="64bb2-150">Use Ansible environment variables</span></span>
<span data-ttu-id="64bb2-151">Als u toouse hulpprogramma's zoals Ansible Tower of Jenkins gaat, kunt u als volgt omgevingsvariabelen definiëren.</span><span class="sxs-lookup"><span data-stu-id="64bb2-151">If you are going toouse tools such as Ansible Tower or Jenkins, you can define environment variables as follows.</span></span> <span data-ttu-id="64bb2-152">Deze variabelen worden gecombineerd Hallo abonnements-ID met Hallo-uitvoer van een service-principal maken.</span><span class="sxs-lookup"><span data-stu-id="64bb2-152">These variables combine hello subscription ID with hello output from creating a service principal.</span></span> <span data-ttu-id="64bb2-153">De uitvoer van de vorige Hallo [az ad sp maken-voor-rbac](/cli/azure/ad/sp#create-for-rbac) opdracht is Hallo dezelfde volgorde nodig zijn voor *AZURE_CLIENT_ID*, *AZURE_SECRET*, en *AZURE_ TENANT*.</span><span class="sxs-lookup"><span data-stu-id="64bb2-153">Output from hello previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is hello same order as needed for *AZURE_CLIENT_ID*, *AZURE_SECRET*, and *AZURE_TENANT*.</span></span> 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a><span data-ttu-id="64bb2-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="64bb2-154">Next steps</span></span>
<span data-ttu-id="64bb2-155">U hebt nu Ansible en hello Azure Python SDK-modules die zijn geïnstalleerd en de referenties die zijn gedefinieerd voor Ansible toouse vereist.</span><span class="sxs-lookup"><span data-stu-id="64bb2-155">You now have Ansible and hello required Azure Python SDK modules installed, and credentials defined for Ansible toouse.</span></span> <span data-ttu-id="64bb2-156">Meer informatie over hoe te[een virtuele machine maken met Ansible](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="64bb2-156">Learn how too[create a VM with Ansible](ansible-create-vm.md).</span></span> <span data-ttu-id="64bb2-157">U kunt ook meer te weten hoe te[een volledige Azure-virtuele machine maken en de ondersteunende resources met Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="64bb2-157">You can also learn how too[create a complete Azure VM and supporting resources with Ansible](ansible-create-complete-vm.md).</span></span>
