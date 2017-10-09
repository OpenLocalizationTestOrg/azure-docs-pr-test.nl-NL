---
title: aaaUse Ansible toocreate een basic Linux VM in Azure | Microsoft Docs
description: Meer informatie over hoe toouse Ansible toocreate en een eenvoudige virtuele Linux-machine in Azure beheren
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
ms.openlocfilehash: ffe278b3f846924ff9c4d026120565146f951152
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a><span data-ttu-id="20600-103">Een eenvoudige virtuele machine maken in Azure met Ansible</span><span class="sxs-lookup"><span data-stu-id="20600-103">Create a basic virtual machine in Azure with Ansible</span></span>
<span data-ttu-id="20600-104">Ansible kunt u tooautomate Hallo implementatie en configuratie van resources in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="20600-104">Ansible allows you tooautomate hello deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="20600-105">U kunt Ansible toomanage van uw virtuele machines (VM's) in Azure gebruiken, dezelfde Hallo net als elke andere bron.</span><span class="sxs-lookup"><span data-stu-id="20600-105">You can use Ansible toomanage your virtual machines (VMs) in Azure, hello same as you would any other resource.</span></span> <span data-ttu-id="20600-106">Dit artikel ziet u hoe een basis-VM met Ansible toocreate.</span><span class="sxs-lookup"><span data-stu-id="20600-106">This article shows you how toocreate a basic VM with Ansible.</span></span> <span data-ttu-id="20600-107">U kunt ook meer te weten hoe te[maakt een complete VM-omgeving met Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="20600-107">You can also learn how too[Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="20600-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="20600-108">Prerequisites</span></span>
<span data-ttu-id="20600-109">toomanage Azure resources met Ansible, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="20600-109">toomanage Azure resources with Ansible, you need hello following:</span></span>

- <span data-ttu-id="20600-110">Ansible en hello Azure Python SDK-modules die zijn geïnstalleerd op uw hostsysteem.</span><span class="sxs-lookup"><span data-stu-id="20600-110">Ansible and hello Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="20600-111">Installeer Ansible op [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), en [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span><span class="sxs-lookup"><span data-stu-id="20600-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="20600-112">Azure-referenties en Ansible geconfigureerd toouse ze.</span><span class="sxs-lookup"><span data-stu-id="20600-112">Azure credentials, and Ansible configured toouse them.</span></span>
    - [<span data-ttu-id="20600-113">Azure-referenties maken en configureren van Ansible</span><span class="sxs-lookup"><span data-stu-id="20600-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="20600-114">Azure CLI versie 2.0.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="20600-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="20600-115">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="20600-115">Run `az --version` toofind hello version.</span></span> 
    - <span data-ttu-id="20600-116">Als u tooupgrade moet, Zie [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="20600-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="20600-117">U kunt ook [Cloud Shell](/azure/cloud-shell/quickstart) vanuit de browser.</span><span class="sxs-lookup"><span data-stu-id="20600-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-supporting-azure-resources"></a><span data-ttu-id="20600-118">Ondersteuning van Azure-resources maken</span><span class="sxs-lookup"><span data-stu-id="20600-118">Create supporting Azure resources</span></span>
<span data-ttu-id="20600-119">In dit voorbeeld maken we een runbook dat een virtuele machine in een bestaande infrastructuur implementeert.</span><span class="sxs-lookup"><span data-stu-id="20600-119">In this example, we create a runbook that deploys a VM into an existing infrastructure.</span></span> <span data-ttu-id="20600-120">Maak eerst een resourcegroep met [az groep maken](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="20600-120">First, create resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="20600-121">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="20600-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="20600-122">Een virtueel netwerk maken voor uw virtuele machine met [az network vnet maken](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="20600-122">Create a virtual network for your VM with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="20600-123">Hallo volgende voorbeeld wordt een virtueel netwerk met de naam *myVnet* en een subnet met de naam *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="20600-123">hello following example creates a virtual network named *myVnet* and a subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a><span data-ttu-id="20600-124">Maken en uitvoeren van Ansible playbook</span><span class="sxs-lookup"><span data-stu-id="20600-124">Create and run Ansible playbook</span></span>
<span data-ttu-id="20600-125">Maken van een Ansible playbook met de naam **azure_create_vm.yml** en inhoud te plakken Hallo volgen.</span><span class="sxs-lookup"><span data-stu-id="20600-125">Create an Ansible playbook named **azure_create_vm.yml** and paste hello following contents.</span></span> <span data-ttu-id="20600-126">In dit voorbeeld één VM maakt en configureert u SSH-referenties.</span><span class="sxs-lookup"><span data-stu-id="20600-126">This example creates a single VM and configures SSH credentials.</span></span> <span data-ttu-id="20600-127">Voer uw eigen gegevens voor openbare sleutel in Hallo *key_data* koppelen als volgt:</span><span class="sxs-lookup"><span data-stu-id="20600-127">Enter your own public key data in hello *key_data* pair as follows:</span></span>

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

<span data-ttu-id="20600-128">toocreate hello VM met Ansible, Hallo playbook als volgt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="20600-128">toocreate hello VM with Ansible, run hello playbook as follows:</span></span>

```bash
ansible-playbook azure_create_vm.yml
```

<span data-ttu-id="20600-129">Hallo-uitvoer ziet er vergelijkbare toohello volgende voorbeeld ziet u Hallo dat VM is gemaakt:</span><span class="sxs-lookup"><span data-stu-id="20600-129">hello output looks similar toohello following example that shows hello VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a><span data-ttu-id="20600-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="20600-130">Next steps</span></span>
<span data-ttu-id="20600-131">In dit voorbeeld maakt een virtuele machine in een bestaande resourcegroep en met een virtueel netwerk al is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="20600-131">This example creates a VM in an existing resource group and with a virtual network already deployed.</span></span> <span data-ttu-id="20600-132">Voor een meer gedetailleerd voorbeeld over het toouse Ansible toocreate ondersteunende resources zoals een virtueel netwerk en de Netwerkbeveiligingsgroep regels, Zie [maakt een complete VM-omgeving met Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="20600-132">For a more detailed example on how toouse Ansible toocreate supporting resources such as a virtual network and Network Security Group rules, see [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>
