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
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a>Een eenvoudige virtuele machine maken in Azure met Ansible
Ansible kunt u tooautomate Hallo implementatie en configuratie van resources in uw omgeving. U kunt Ansible toomanage van uw virtuele machines (VM's) in Azure gebruiken, dezelfde Hallo net als elke andere bron. Dit artikel ziet u hoe een basis-VM met Ansible toocreate. U kunt ook meer te weten hoe te[maakt een complete VM-omgeving met Ansible](ansible-create-complete-vm.md).


## <a name="prerequisites"></a>Vereisten
toomanage Azure resources met Ansible, moet u hello te volgen:

- Ansible en hello Azure Python SDK-modules die zijn geïnstalleerd op uw hostsysteem.
    - Installeer Ansible op [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), en [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)
- Azure-referenties en Ansible geconfigureerd toouse ze.
    - [Azure-referenties maken en configureren van Ansible](ansible-install-configure.md#create-azure-credentials)
- Azure CLI versie 2.0.4 of hoger. Voer `az --version` toofind Hallo versie. 
    - Als u tooupgrade moet, Zie [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). U kunt ook [Cloud Shell](/azure/cloud-shell/quickstart) vanuit de browser.


## <a name="create-supporting-azure-resources"></a>Ondersteuning van Azure-resources maken
In dit voorbeeld maken we een runbook dat een virtuele machine in een bestaande infrastructuur implementeert. Maak eerst een resourcegroep met [az groep maken](/cli/azure/vm#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:

```azurecli
az group create --name myResourceGroup --location eastus
```

Een virtueel netwerk maken voor uw virtuele machine met [az network vnet maken](/cli/azure/network/vnet#create). Hallo volgende voorbeeld wordt een virtueel netwerk met de naam *myVnet* en een subnet met de naam *mySubnet*:

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a>Maken en uitvoeren van Ansible playbook
Maken van een Ansible playbook met de naam **azure_create_vm.yml** en inhoud te plakken Hallo volgen. In dit voorbeeld één VM maakt en configureert u SSH-referenties. Voer uw eigen gegevens voor openbare sleutel in Hallo *key_data* koppelen als volgt:

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

toocreate hello VM met Ansible, Hallo playbook als volgt uitvoeren:

```bash
ansible-playbook azure_create_vm.yml
```

Hallo-uitvoer ziet er vergelijkbare toohello volgende voorbeeld ziet u Hallo dat VM is gemaakt:

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a>Volgende stappen
In dit voorbeeld maakt een virtuele machine in een bestaande resourcegroep en met een virtueel netwerk al is geïmplementeerd. Voor een meer gedetailleerd voorbeeld over het toouse Ansible toocreate ondersteunende resources zoals een virtueel netwerk en de Netwerkbeveiligingsgroep regels, Zie [maakt een complete VM-omgeving met Ansible](ansible-create-complete-vm.md).
