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
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a>Maken van een omgeving met volledige Linux virtuele machines in Azure met Ansible
Ansible kunt u tooautomate Hallo implementatie en configuratie van resources in uw omgeving. U kunt Ansible toomanage van uw virtuele machines (VM's) in Azure gebruiken, dezelfde Hallo net als elke andere bron. Dit artikel ziet u hoe toocreate een volledige Linux-omgeving en de ondersteunende resources met Ansible. U kunt ook meer te weten hoe te[maken van een basis-VM met Ansible](ansible-create-vm.md).


## <a name="prerequisites"></a>Vereisten
toomanage Azure resources met Ansible, moet u hello te volgen:

- Ansible en hello Azure Python SDK-modules die zijn geïnstalleerd op uw hostsysteem.
    - Installeer Ansible op [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), en [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)
- Azure-referenties en Ansible geconfigureerd toouse ze.
    - [Azure-referenties maken en configureren van Ansible](ansible-install-configure.md#create-azure-credentials)
- Azure CLI versie 2.0.4 of hoger. Voer `az --version` toofind Hallo versie. 
    - Als u tooupgrade moet, Zie [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). U kunt ook [Cloud Shell](/azure/cloud-shell/quickstart) vanuit de browser.


## <a name="create-virtual-network"></a>Virtueel netwerk maken
Hallo volgende sectie in een playbook Ansible maakt een virtueel netwerk met de naam *myVnet* in Hallo *10.0.0.0/16* adresruimte:

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

tooadd een subnet, Hallo volgende sectie maakt u een subnet met de naam *mySubnet* in Hallo *myVnet* virtueel netwerk:

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a>Openbare IP-adres maken
tooaccess resources tussen Hallo Internet, maken en toewijzen van een openbare IP-adres tooyour VM. Hallo volgende sectie in een playbook Ansible maakt u een openbaar IP-adres met de naam *myPublicIP*:

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a>Netwerkbeveiligingsgroep maken
Netwerkbeveiligingsgroepen transportbesturing Hallo van netwerkverkeer binnen en buiten uw virtuele machine. Hallo volgende sectie in een playbook Ansible maakt een netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup* en definieert u een regel tooallow SSH-verkeer op TCP-poort 22:

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


## <a name="create-virtual-network-interface-card"></a>Maken van de virtuele netwerkinterfacekaart
Een virtuele netwerkinterfacekaart (NIC) maakt verbinding met uw VM tooa virtueel netwerk, openbare IP-adres en de netwerkbeveiligingsgroep opgegeven. Hallo volgende sectie in een playbook Ansible maakt u een virtuele NIC met de naam *myNIC* verbonden toohello virtuele netwerkresources u hebt gemaakt:

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


## <a name="create-virtual-machine"></a>Virtuele machine maken
laatste stap Hallo toocreate is een virtuele machine en gebruik van alle Hallo bronnen die zijn gemaakt. Hallo volgende sectie in een playbook Ansible maakt u een virtuele machine met de naam *myVM* en wordt virtuele NIC met de naam Hallo *myNIC*. Voer uw eigen gegevens voor openbare sleutel in Hallo *key_data* koppelen als volgt:

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

## <a name="complete-ansible-playbook"></a>Ansible playbook voltooien
toobring alle deze secties maken samen een Ansible playbook met de naam *azure_create_complete_vm.yml* en inhoud te plakken Hallo volgen:

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

Ansible moet een groep resource toodeploy alle resources in. Maak een resourcegroep maken met [az group create](/cli/azure/vm#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:

```azurecli
az group create --name myResourceGroup --location eastus
```

toocreate hello voltooid VM-omgeving met Ansible, Hallo playbook als volgt uitvoeren:

```bash
ansible-playbook azure_create_complete_vm.yml
```

Hallo-uitvoer ziet er vergelijkbare toohello volgende voorbeeld ziet u Hallo dat VM is gemaakt:

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

## <a name="next-steps"></a>Volgende stappen
In dit voorbeeld maakt u een volledige VM-omgeving met inbegrip van virtuele netwerken bronnen Hallo vereist. Zie voor een meer rechtstreekse voorbeeld toocreate een virtuele machine in de bestaande netwerkbronnen met de standaardopties [een virtuele machine maken](ansible-create-vm.md).
