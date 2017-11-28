---
title: aaaUse Ansible toocreate een volledige Linux VM in Azure | Microsoft Docs
description: Meer informatie over hoe toouse Ansible toocreate en een omgeving met volledige Linux virtuele machines in Azure beheren
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
ms.openlocfilehash: 970b0427f39fc23240f9faab868196ca4f444e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a><span data-ttu-id="2024d-103">Maken van een omgeving met volledige Linux virtuele machines in Azure met Ansible</span><span class="sxs-lookup"><span data-stu-id="2024d-103">Create a complete Linux virtual machine environment in Azure with Ansible</span></span>
<span data-ttu-id="2024d-104">Ansible kunt u tooautomate Hallo implementatie en configuratie van resources in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="2024d-104">Ansible allows you tooautomate hello deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="2024d-105">U kunt Ansible toomanage van uw virtuele machines (VM's) in Azure gebruiken, dezelfde Hallo net als elke andere bron.</span><span class="sxs-lookup"><span data-stu-id="2024d-105">You can use Ansible toomanage your virtual machines (VMs) in Azure, hello same as you would any other resource.</span></span> <span data-ttu-id="2024d-106">Dit artikel ziet u hoe toocreate een volledige Linux-omgeving en de ondersteunende resources met Ansible.</span><span class="sxs-lookup"><span data-stu-id="2024d-106">This article shows you how toocreate a complete Linux environment and supporting resources with Ansible.</span></span> <span data-ttu-id="2024d-107">U kunt ook meer te weten hoe te[maken van een basis-VM met Ansible](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="2024d-107">You can also learn how too[Create a basic VM with Ansible](ansible-create-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="2024d-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2024d-108">Prerequisites</span></span>
<span data-ttu-id="2024d-109">toomanage Azure resources met Ansible, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="2024d-109">toomanage Azure resources with Ansible, you need hello following:</span></span>

- <span data-ttu-id="2024d-110">Ansible en hello Azure Python SDK-modules die zijn geïnstalleerd op uw hostsysteem.</span><span class="sxs-lookup"><span data-stu-id="2024d-110">Ansible and hello Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="2024d-111">Installeer Ansible op [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), en [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span><span class="sxs-lookup"><span data-stu-id="2024d-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="2024d-112">Azure-referenties en Ansible geconfigureerd toouse ze.</span><span class="sxs-lookup"><span data-stu-id="2024d-112">Azure credentials, and Ansible configured toouse them.</span></span>
    - [<span data-ttu-id="2024d-113">Azure-referenties maken en configureren van Ansible</span><span class="sxs-lookup"><span data-stu-id="2024d-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="2024d-114">Azure CLI versie 2.0.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="2024d-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="2024d-115">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="2024d-115">Run `az --version` toofind hello version.</span></span> 
    - <span data-ttu-id="2024d-116">Als u tooupgrade moet, Zie [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2024d-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="2024d-117">U kunt ook [Cloud Shell](/azure/cloud-shell/quickstart) vanuit de browser.</span><span class="sxs-lookup"><span data-stu-id="2024d-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-virtual-network"></a><span data-ttu-id="2024d-118">Virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="2024d-118">Create virtual network</span></span>
<span data-ttu-id="2024d-119">Hallo volgende sectie in een playbook Ansible maakt een virtueel netwerk met de naam *myVnet* in Hallo *10.0.0.0/16* adresruimte:</span><span class="sxs-lookup"><span data-stu-id="2024d-119">hello following section in an Ansible playbook creates a virtual network named *myVnet* in hello *10.0.0.0/16* address space:</span></span>

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

<span data-ttu-id="2024d-120">tooadd een subnet, Hallo volgende sectie maakt u een subnet met de naam *mySubnet* in Hallo *myVnet* virtueel netwerk:</span><span class="sxs-lookup"><span data-stu-id="2024d-120">tooadd a subnet, hello following section creates a subnet named *mySubnet* in hello *myVnet* virtual network:</span></span>

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a><span data-ttu-id="2024d-121">Openbare IP-adres maken</span><span class="sxs-lookup"><span data-stu-id="2024d-121">Create public IP address</span></span>
<span data-ttu-id="2024d-122">tooaccess resources tussen Hallo Internet, maken en toewijzen van een openbare IP-adres tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="2024d-122">tooaccess resources across hello Internet, create and assign a public IP address tooyour VM.</span></span> <span data-ttu-id="2024d-123">Hallo volgende sectie in een playbook Ansible maakt u een openbaar IP-adres met de naam *myPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="2024d-123">hello following section in an Ansible playbook creates a public IP address named *myPublicIP*:</span></span>

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a><span data-ttu-id="2024d-124">Netwerkbeveiligingsgroep maken</span><span class="sxs-lookup"><span data-stu-id="2024d-124">Create Network Security Group</span></span>
<span data-ttu-id="2024d-125">Netwerkbeveiligingsgroepen transportbesturing Hallo van netwerkverkeer binnen en buiten uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2024d-125">Network Security Groups control hello flow of network traffic in and out of your VM.</span></span> <span data-ttu-id="2024d-126">Hallo volgende sectie in een playbook Ansible maakt een netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup* en definieert u een regel tooallow SSH-verkeer op TCP-poort 22:</span><span class="sxs-lookup"><span data-stu-id="2024d-126">hello following section in an Ansible playbook creates a network security group named *myNetworkSecurityGroup* and defines a rule tooallow SSH traffic on TCP port 22:</span></span>

```yaml
- name: Create Network Security Group that allows SSH
  azure_rm_securitygroup:
    resource_group: myResourceGroup
    name: myNetworkSecurityGroup
    rules:
      - name: SSH
        protocol: TCP
        destination_port_range: 22
        access: Allow
        priority: 1001
        direction: Inbound
```


## <a name="create-virtual-network-interface-card"></a><span data-ttu-id="2024d-127">Maken van de virtuele netwerkinterfacekaart</span><span class="sxs-lookup"><span data-stu-id="2024d-127">Create virtual network interface card</span></span>
<span data-ttu-id="2024d-128">Een virtuele netwerkinterfacekaart (NIC) maakt verbinding met uw VM tooa virtueel netwerk, openbare IP-adres en de netwerkbeveiligingsgroep opgegeven.</span><span class="sxs-lookup"><span data-stu-id="2024d-128">A virtual network interface card (NIC) connects your VM tooa given virtual network, public IP address, and network security group.</span></span> <span data-ttu-id="2024d-129">Hallo volgende sectie in een playbook Ansible maakt u een virtuele NIC met de naam *myNIC* verbonden toohello virtuele netwerkresources u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="2024d-129">hello following section in an Ansible playbook creates a virtual NIC named *myNIC* connected toohello virtual networking resources you have created:</span></span>

```yaml
- name: Create virtual network inteface card
  azure_rm_networkinterface:
    resource_group: myResourceGroup
    name: myNIC
    virtual_network: myVnet
    subnet: mySubnet
    public_ip_name: myPublicIP
    security_group: myNetworkSecurityGroup
```


## <a name="create-virtual-machine"></a><span data-ttu-id="2024d-130">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="2024d-130">Create virtual machine</span></span>
<span data-ttu-id="2024d-131">laatste stap Hallo toocreate is een virtuele machine en gebruik van alle Hallo bronnen die zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2024d-131">hello final step is toocreate a VM and use all hello resources created.</span></span> <span data-ttu-id="2024d-132">Hallo volgende sectie in een playbook Ansible maakt u een virtuele machine met de naam *myVM* en wordt virtuele NIC met de naam Hallo *myNIC*.</span><span class="sxs-lookup"><span data-stu-id="2024d-132">hello following section in an Ansible playbook creates a VM named *myVM* and attaches hello virtual NIC named *myNIC*.</span></span> <span data-ttu-id="2024d-133">Voer uw eigen gegevens voor openbare sleutel in Hallo *key_data* koppelen als volgt:</span><span class="sxs-lookup"><span data-stu-id="2024d-133">Enter your own public key data in hello *key_data* pair as follows:</span></span>

```yaml
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
    network_interfaces: myNIC
    image:
      offer: CentOS
      publisher: OpenLogic
      sku: '7.3'
      version: latest
```

## <a name="complete-ansible-playbook"></a><span data-ttu-id="2024d-134">Ansible playbook voltooien</span><span class="sxs-lookup"><span data-stu-id="2024d-134">Complete Ansible playbook</span></span>
<span data-ttu-id="2024d-135">toobring alle deze secties maken samen een Ansible playbook met de naam *azure_create_complete_vm.yml* en inhoud te plakken Hallo volgen:</span><span class="sxs-lookup"><span data-stu-id="2024d-135">toobring all these sections together, create an Ansible playbook named *azure_create_complete_vm.yml* and paste hello following contents:</span></span>

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create virtual network
    azure_rm_virtualnetwork:
      resource_group: myResourceGroup
      name: myVnet
      address_prefixes: "10.0.0.0/16"
  - name: Add subnet
    azure_rm_subnet:
      resource_group: myResourceGroup
      name: mySubnet
      address_prefix: "10.0.1.0/24"
      virtual_network: myVnet
  - name: Create public IP address
    azure_rm_publicipaddress:
      resource_group: myResourceGroup
      allocation_method: Static
      name: myPublicIP
  - name: Create Network Security Group that allows SSH
    azure_rm_securitygroup:
      resource_group: myResourceGroup
      name: myNetworkSecurityGroup
      rules:
        - name: SSH
          protocol: Tcp
          destination_port_range: 22
          access: Allow
          priority: 1001
          direction: Inbound
  - name: Create virtual network inteface card
    azure_rm_networkinterface:
      resource_group: myResourceGroup
      name: myNIC
      virtual_network: myVnet
      subnet: mySubnet
      public_ip_name: myPublicIP
      security_group: myNetworkSecurityGroup
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
      network_interfaces: myNIC
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

<span data-ttu-id="2024d-136">Ansible moet een groep resource toodeploy alle resources in.</span><span class="sxs-lookup"><span data-stu-id="2024d-136">Ansible needs a resource group toodeploy all your resources into.</span></span> <span data-ttu-id="2024d-137">Maak een resourcegroep maken met [az group create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="2024d-137">Create a resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="2024d-138">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="2024d-138">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="2024d-139">toocreate hello voltooid VM-omgeving met Ansible, Hallo playbook als volgt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="2024d-139">toocreate hello complete VM environment with Ansible, run hello playbook as follows:</span></span>

```bash
ansible-playbook azure_create_complete_vm.yml
```

<span data-ttu-id="2024d-140">Hallo-uitvoer ziet er vergelijkbare toohello volgende voorbeeld ziet u Hallo dat VM is gemaakt:</span><span class="sxs-lookup"><span data-stu-id="2024d-140">hello output looks similar toohello following example that shows hello VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create virtual network] *********************************************
changed: [localhost]

TASK [Add subnet] *********************************************************
changed: [localhost]

TASK [Create public IP address] *******************************************
changed: [localhost]

TASK [Create Network Security Group that allows SSH] **********************
changed: [localhost]

TASK [Create virtual network inteface card] *******************************
changed: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=7    changed=6    unreachable=0    failed=0
```

## <a name="next-steps"></a><span data-ttu-id="2024d-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2024d-141">Next steps</span></span>
<span data-ttu-id="2024d-142">In dit voorbeeld maakt u een volledige VM-omgeving met inbegrip van virtuele netwerken bronnen Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="2024d-142">This example creates a complete VM environment including hello required virtual networking resources.</span></span> <span data-ttu-id="2024d-143">Zie voor een meer rechtstreekse voorbeeld toocreate een virtuele machine in de bestaande netwerkbronnen met de standaardopties [een virtuele machine maken](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="2024d-143">For a more direct example toocreate a VM into existing network resources with default options, see [Create a VM](ansible-create-vm.md).</span></span>
