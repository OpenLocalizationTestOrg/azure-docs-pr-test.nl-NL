---
title: Installeren en configureren van Ansible voor gebruik met virtuele machines in Azure | Microsoft Docs
description: Meer informatie over het installeren en configureren van Ansible voor het beheren van Azure-resources op Ubuntu en CentOS SLES
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
ms.openlocfilehash: 52b763274437961dccfc862c8a45fbd57ea9fc4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-configure-ansible-to-manage-virtual-machines-in-azure"></a><span data-ttu-id="37a25-103">Installeren en configureren van Ansible voor het beheren van virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="37a25-103">Install and configure Ansible to manage virtual machines in Azure</span></span>
<span data-ttu-id="37a25-104">Dit artikel wordt uitgelegd hoe u Ansible en vereist Azure Python SDK-modules installeren voor enkele van de meest voorkomende Linux-distributies.</span><span class="sxs-lookup"><span data-stu-id="37a25-104">This article details how to install Ansible and required Azure Python SDK modules for some of the most common Linux distros.</span></span> <span data-ttu-id="37a25-105">U kunt Ansible installeren op andere distributies door de geïnstalleerde pakketten aanpassen aan uw bepaald platform aan te passen.</span><span class="sxs-lookup"><span data-stu-id="37a25-105">You can install Ansible on other distros by adjusting the installed packages to fit your particular platform.</span></span> <span data-ttu-id="37a25-106">Voor het maken van Azure-resources op een veilige manier, u ook informatie over het maken en definiëren van referenties voor Ansible te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="37a25-106">To create Azure resources in a secure manner, you also learn how to create and define credentials for Ansible to use.</span></span> 

<span data-ttu-id="37a25-107">Zie voor meer informatie over opties voor de installatie en stappen voor extra platforms de [Ansible installatiehandleiding](https://docs.ansible.com/ansible/intro_installation.html).</span><span class="sxs-lookup"><span data-stu-id="37a25-107">For more installation options and steps for additional platforms, see the [Ansible install guide](https://docs.ansible.com/ansible/intro_installation.html).</span></span>


## <a name="install-ansible"></a><span data-ttu-id="37a25-108">Ansible installeren</span><span class="sxs-lookup"><span data-stu-id="37a25-108">Install Ansible</span></span>
<span data-ttu-id="37a25-109">Maak eerst een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="37a25-109">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="37a25-110">Het volgende voorbeeld wordt een resourcegroep met de naam *myResourceGroupAnsible* in de *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="37a25-110">The following example creates a resource group named *myResourceGroupAnsible* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

<span data-ttu-id="37a25-111">Nu een virtuele machine maken en Ansible voor een van de volgende distributies installeren:</span><span class="sxs-lookup"><span data-stu-id="37a25-111">Now create a VM and install Ansible for one of the following distros:</span></span>

- [<span data-ttu-id="37a25-112">Ubuntu 16.04 TNS</span><span class="sxs-lookup"><span data-stu-id="37a25-112">Ubuntu 16.04 LTS</span></span>](#ubuntu1604-lts)
- [<span data-ttu-id="37a25-113">7.3 centOS</span><span class="sxs-lookup"><span data-stu-id="37a25-113">CentOS 7.3</span></span>](#centos-73)
- [<span data-ttu-id="37a25-114">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="37a25-114">SLES 12.2 SP2</span></span>](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="37a25-115">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="37a25-115">Ubuntu 16.04 LTS</span></span>
<span data-ttu-id="37a25-116">Maak een VM met [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="37a25-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="37a25-117">Het volgende voorbeeld wordt een virtuele machine met de naam *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="37a25-117">The following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="37a25-118">SSH naar uw virtuele machine met de `publicIpAddress` vermeld in de uitvoer van de virtuele machine opnieuw te maken:</span><span class="sxs-lookup"><span data-stu-id="37a25-118">SSH to your VM using the `publicIpAddress` noted in the output from the VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="37a25-119">Op de virtuele machine, moet u de vereiste pakketten voor de Azure Python SDK-modules en Ansible als volgt installeren:</span><span class="sxs-lookup"><span data-stu-id="37a25-119">On your VM, install the required packages for the Azure Python SDK modules and Ansible as follows:</span></span>

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

<span data-ttu-id="37a25-120">Nu wordt verplaatst naar [maken Azure-referenties](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="37a25-120">Now move on to [Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="centos-73"></a><span data-ttu-id="37a25-121">7.3 centOS</span><span class="sxs-lookup"><span data-stu-id="37a25-121">CentOS 7.3</span></span>
<span data-ttu-id="37a25-122">Maak een VM met [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="37a25-122">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="37a25-123">Het volgende voorbeeld wordt een virtuele machine met de naam *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="37a25-123">The following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="37a25-124">SSH naar uw virtuele machine met de `publicIpAddress` vermeld in de uitvoer van de virtuele machine opnieuw te maken:</span><span class="sxs-lookup"><span data-stu-id="37a25-124">SSH to your VM using the `publicIpAddress` noted in the output from the VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="37a25-125">Op de virtuele machine, moet u de vereiste pakketten voor de Azure Python SDK-modules en Ansible als volgt installeren:</span><span class="sxs-lookup"><span data-stu-id="37a25-125">On your VM, install the required packages for the Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

<span data-ttu-id="37a25-126">Nu wordt verplaatst naar [maken Azure-referenties](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="37a25-126">Now move on to [Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="sles-122-sp2"></a><span data-ttu-id="37a25-127">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="37a25-127">SLES 12.2 SP2</span></span>
<span data-ttu-id="37a25-128">Maak een VM met [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="37a25-128">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="37a25-129">Het volgende voorbeeld wordt een virtuele machine met de naam *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="37a25-129">The following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="37a25-130">SSH naar uw virtuele machine met de `publicIpAddress` vermeld in de uitvoer van de virtuele machine opnieuw te maken:</span><span class="sxs-lookup"><span data-stu-id="37a25-130">SSH to your VM using the `publicIpAddress` noted in the output from the VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="37a25-131">Op de virtuele machine, moet u de vereiste pakketten voor de Azure Python SDK-modules en Ansible als volgt installeren:</span><span class="sxs-lookup"><span data-stu-id="37a25-131">On your VM, install the required packages for the Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

<span data-ttu-id="37a25-132">Nu wordt verplaatst naar [maken Azure-referenties](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="37a25-132">Now move on to [Create Azure credentials](#create-azure-credentials).</span></span>


## <a name="create-azure-credentials"></a><span data-ttu-id="37a25-133">Azure-referenties maken</span><span class="sxs-lookup"><span data-stu-id="37a25-133">Create Azure credentials</span></span>
<span data-ttu-id="37a25-134">Ansible communiceert met Azure met behulp van een gebruikersnaam en wachtwoord of een service-principal.</span><span class="sxs-lookup"><span data-stu-id="37a25-134">Ansible communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="37a25-135">Een Azure-service-principal is een beveiligings-id die u met apps, services en automatiseringsprogramma's zoals Ansible gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="37a25-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Ansible.</span></span> <span data-ttu-id="37a25-136">U de machtigingen over welke bewerkingen die de service-principal in Azure uitvoeren kunt te definiëren en beheren.</span><span class="sxs-lookup"><span data-stu-id="37a25-136">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span> <span data-ttu-id="37a25-137">Voor betere beveiliging via gewoon een gebruikersnaam en wachtwoord voor het bieden, in dit voorbeeld wordt een basic service principal.</span><span class="sxs-lookup"><span data-stu-id="37a25-137">To improve security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="37a25-138">Maken van een service principal met [az ad sp maken-voor-rbac](/cli/azure/ad/sp#create-for-rbac) en de uitvoer van de referenties die Ansible moet:</span><span class="sxs-lookup"><span data-stu-id="37a25-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output the credentials that Ansible needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="37a25-139">Een voorbeeld van de uitvoer van de bovenstaande opdrachten is als volgt:</span><span class="sxs-lookup"><span data-stu-id="37a25-139">An example of the output from the preceding commands is as follows:</span></span>

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

<span data-ttu-id="37a25-140">Om te verifiëren naar Azure, moet u ook uw Azure-abonnement-id met [az account weergeven](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="37a25-140">To authenticate to Azure, you also need to obtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="37a25-141">U gebruikt de uitvoer van deze twee opdrachten in de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="37a25-141">You use the output from these two commands in the next step.</span></span>


## <a name="create-ansible-credentials-file"></a><span data-ttu-id="37a25-142">Ansible referentiebestand maken</span><span class="sxs-lookup"><span data-stu-id="37a25-142">Create Ansible credentials file</span></span>
<span data-ttu-id="37a25-143">Om referenties te verstrekken aan Ansible, omgevingsvariabelen definiëren of maak een bestand lokale referenties.</span><span class="sxs-lookup"><span data-stu-id="37a25-143">To provide credentials to Ansible, you define environment variables or create a local credentials file.</span></span> <span data-ttu-id="37a25-144">Zie voor meer informatie over het definiëren van Ansible referenties [referenties bieden voor Azure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span><span class="sxs-lookup"><span data-stu-id="37a25-144">For more information about how to define Ansible credentials, see [Providing Credentials to Azure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span></span> 

<span data-ttu-id="37a25-145">Voor een ontwikkelingsomgeving, maakt u een *referenties* voor Ansible bestand op de VM-host als volgt:</span><span class="sxs-lookup"><span data-stu-id="37a25-145">For a development environment, create a *credentials* file for Ansible on your host VM as follows:</span></span>

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

<span data-ttu-id="37a25-146">De *referenties* bestand zelf combineert de abonnements-ID met de uitvoer van een service-principal maken.</span><span class="sxs-lookup"><span data-stu-id="37a25-146">The *credentials* file itself combines the subscription ID with the output of creating a service principal.</span></span> <span data-ttu-id="37a25-147">De uitvoer van de vorige [az ad sp maken-voor-rbac](/cli/azure/ad/sp#create-for-rbac) opdracht wordt dezelfde volgorde als nodig is voor *client_id*, *geheim*, en *tenant*.</span><span class="sxs-lookup"><span data-stu-id="37a25-147">Output from the previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is the same order as needed for *client_id*, *secret*, and *tenant*.</span></span> <span data-ttu-id="37a25-148">Het volgende voorbeeld *referenties* bestand deze waarden die overeenkomen met de vorige uitvoer wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="37a25-148">The following example *credentials* file shows these values matching the previous output.</span></span> <span data-ttu-id="37a25-149">Voer uw eigen waarden als volgt:</span><span class="sxs-lookup"><span data-stu-id="37a25-149">Enter your own values as follows:</span></span>

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a><span data-ttu-id="37a25-150">Omgevingsvariabelen Ansible gebruiken</span><span class="sxs-lookup"><span data-stu-id="37a25-150">Use Ansible environment variables</span></span>
<span data-ttu-id="37a25-151">Als u gebruikmaken van hulpprogramma's zoals Ansible Tower of Jenkins wilt, kunt u als volgt omgevingsvariabelen definiëren.</span><span class="sxs-lookup"><span data-stu-id="37a25-151">If you are going to use tools such as Ansible Tower or Jenkins, you can define environment variables as follows.</span></span> <span data-ttu-id="37a25-152">Deze variabelen worden de abonnements-ID gecombineerd met de uitvoer van een service-principal maken.</span><span class="sxs-lookup"><span data-stu-id="37a25-152">These variables combine the subscription ID with the output from creating a service principal.</span></span> <span data-ttu-id="37a25-153">De uitvoer van de vorige [az ad sp maken-voor-rbac](/cli/azure/ad/sp#create-for-rbac) opdracht wordt dezelfde volgorde als nodig is voor *AZURE_CLIENT_ID*, *AZURE_SECRET*, en *AZURE_TENANT* .</span><span class="sxs-lookup"><span data-stu-id="37a25-153">Output from the previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is the same order as needed for *AZURE_CLIENT_ID*, *AZURE_SECRET*, and *AZURE_TENANT*.</span></span> 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a><span data-ttu-id="37a25-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="37a25-154">Next steps</span></span>
<span data-ttu-id="37a25-155">U hebt nu Ansible en de vereiste Azure Python SDK modules geïnstalleerd en referenties die zijn gedefinieerd voor Ansible te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="37a25-155">You now have Ansible and the required Azure Python SDK modules installed, and credentials defined for Ansible to use.</span></span> <span data-ttu-id="37a25-156">Meer informatie over hoe [een virtuele machine maken met Ansible](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="37a25-156">Learn how to [create a VM with Ansible](ansible-create-vm.md).</span></span> <span data-ttu-id="37a25-157">U kunt ook meer te weten hoe [een volledige Azure-virtuele machine maken en de ondersteunende resources met Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="37a25-157">You can also learn how to [create a complete Azure VM and supporting resources with Ansible](ansible-create-complete-vm.md).</span></span>