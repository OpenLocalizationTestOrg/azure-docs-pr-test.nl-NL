---
title: Ansible gebruiken voor het maken van een basis Linux VM in Azure | Microsoft Docs
description: Informatie over het gebruik van Ansible maken en beheren van een eenvoudige virtuele Linux-machine in Azure
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
ms.openlocfilehash: 526f3522334450564500c4ba0e401a683cae55f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a><span data-ttu-id="87741-103">Een eenvoudige virtuele machine maken in Azure met Ansible</span><span class="sxs-lookup"><span data-stu-id="87741-103">Create a basic virtual machine in Azure with Ansible</span></span>
<span data-ttu-id="87741-104">Ansible kunt u de implementatie en configuratie van resources in uw omgeving automatiseren.</span><span class="sxs-lookup"><span data-stu-id="87741-104">Ansible allows you to automate the deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="87741-105">U kunt Ansible gebruiken voor het beheren van uw virtuele machines (VM's) in Azure, net als elke andere bron dezelfde.</span><span class="sxs-lookup"><span data-stu-id="87741-105">You can use Ansible to manage your virtual machines (VMs) in Azure, the same as you would any other resource.</span></span> <span data-ttu-id="87741-106">In dit artikel leest u hoe een basis-VM met Ansible maken.</span><span class="sxs-lookup"><span data-stu-id="87741-106">This article shows you how to create a basic VM with Ansible.</span></span> <span data-ttu-id="87741-107">U kunt ook meer te weten hoe [maakt een complete VM-omgeving met Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="87741-107">You can also learn how to [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="87741-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="87741-108">Prerequisites</span></span>
<span data-ttu-id="87741-109">Voor het beheren van Azure-resources met Ansible, moet u het volgende:</span><span class="sxs-lookup"><span data-stu-id="87741-109">To manage Azure resources with Ansible, you need the following:</span></span>

- <span data-ttu-id="87741-110">Ansible en de Azure Python SDK-modules die op uw hostsysteem zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="87741-110">Ansible and the Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="87741-111">Installeer Ansible op [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), en [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span><span class="sxs-lookup"><span data-stu-id="87741-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="87741-112">Azure-referenties en Ansible geconfigureerd ze gebruiken.</span><span class="sxs-lookup"><span data-stu-id="87741-112">Azure credentials, and Ansible configured to use them.</span></span>
    - [<span data-ttu-id="87741-113">Azure-referenties maken en configureren van Ansible</span><span class="sxs-lookup"><span data-stu-id="87741-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="87741-114">Azure CLI versie 2.0.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="87741-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="87741-115">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="87741-115">Run `az --version` to find the version.</span></span> 
    - <span data-ttu-id="87741-116">Als u Azure CLI 2.0 wilt upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="87741-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="87741-117">U kunt ook [Cloud Shell](/azure/cloud-shell/quickstart) vanuit de browser.</span><span class="sxs-lookup"><span data-stu-id="87741-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-supporting-azure-resources"></a><span data-ttu-id="87741-118">Ondersteuning van Azure-resources maken</span><span class="sxs-lookup"><span data-stu-id="87741-118">Create supporting Azure resources</span></span>
<span data-ttu-id="87741-119">In dit voorbeeld maken we een runbook dat een virtuele machine in een bestaande infrastructuur implementeert.</span><span class="sxs-lookup"><span data-stu-id="87741-119">In this example, we create a runbook that deploys a VM into an existing infrastructure.</span></span> <span data-ttu-id="87741-120">Maak eerst een resourcegroep met [az groep maken](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="87741-120">First, create resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="87741-121">Het volgende voorbeeld wordt een resourcegroep met de naam *myResourceGroup* in de *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="87741-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="87741-122">Een virtueel netwerk maken voor uw virtuele machine met [az network vnet maken](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="87741-122">Create a virtual network for your VM with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="87741-123">Het volgende voorbeeld wordt een virtueel netwerk met de naam *myVnet* en een subnet met de naam *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="87741-123">The following example creates a virtual network named *myVnet* and a subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a><span data-ttu-id="87741-124">Maken en uitvoeren van Ansible playbook</span><span class="sxs-lookup"><span data-stu-id="87741-124">Create and run Ansible playbook</span></span>
<span data-ttu-id="87741-125">Maken van een Ansible playbook met de naam **azure_create_vm.yml** en plak de volgende inhoud.</span><span class="sxs-lookup"><span data-stu-id="87741-125">Create an Ansible playbook named **azure_create_vm.yml** and paste the following contents.</span></span> <span data-ttu-id="87741-126">In dit voorbeeld één VM maakt en configureert u SSH-referenties.</span><span class="sxs-lookup"><span data-stu-id="87741-126">This example creates a single VM and configures SSH credentials.</span></span> <span data-ttu-id="87741-127">Voer uw eigen gegevens voor openbare sleutel in de *key_data* koppelen als volgt:</span><span class="sxs-lookup"><span data-stu-id="87741-127">Enter your own public key data in the *key_data* pair as follows:</span></span>

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create VM
    azure_rm_virtualmachine:
      resource_group: myResourceGroup
      name: myVM
      vm_size: Standard_DS1_v2
      admin_username: azureuser
      ssh_password_enabled: false
      ssh_public_keys: 
        - path: /home/azureuser/.ssh/authorized_keys
          key_data: "ssh-rsa AAAAB3Nz{snip}hwhqT9h"
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

<span data-ttu-id="87741-128">Als de virtuele machine maken met Ansible, voert u de playbook als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="87741-128">To create the VM with Ansible, run the playbook as follows:</span></span>

```bash
ansible-playbook azure_create_vm.yml
```

<span data-ttu-id="87741-129">De uitvoer lijkt op het volgende voorbeeld ziet u dat de virtuele machine is gemaakt:</span><span class="sxs-lookup"><span data-stu-id="87741-129">The output looks similar to the following example that shows the VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a><span data-ttu-id="87741-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="87741-130">Next steps</span></span>
<span data-ttu-id="87741-131">In dit voorbeeld maakt een virtuele machine in een bestaande resourcegroep en met een virtueel netwerk al is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="87741-131">This example creates a VM in an existing resource group and with a virtual network already deployed.</span></span> <span data-ttu-id="87741-132">Zie voor een uitgebreider voorbeeld over het gebruik van Ansible ondersteunende resources zoals een virtueel netwerk en de Netwerkbeveiligingsgroep regels maken [maakt een complete VM-omgeving met Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="87741-132">For a more detailed example on how to use Ansible to create supporting resources such as a virtual network and Network Security Group rules, see [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>