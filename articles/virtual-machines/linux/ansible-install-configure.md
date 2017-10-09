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
# <a name="install-and-configure-ansible-toomanage-virtual-machines-in-azure"></a>Installeren en configureren van Ansible toomanage virtuele machines in Azure
Dit artikel wordt uitgelegd hoe tooinstall Ansible en vereist Azure Python SDK-modules voor een aantal Hallo meest voorkomende Linux-distributies. U kunt installeren Ansible op andere distributies door aan te passen geïnstalleerd hello-pakketten toofit uw bepaald platform. toocreate Azure bronnen op een veilige manier u leert ook hoe toocreate en referenties voor Ansible toouse definiëren. 

Zie voor meer informatie over opties voor de installatie en stappen voor extra platforms Hallo [Ansible installatiehandleiding](https://docs.ansible.com/ansible/intro_installation.html).


## <a name="install-ansible"></a>Ansible installeren
Maak eerst een resourcegroep met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroupAnsible* in Hallo *eastus* locatie:

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

Nu een virtuele machine maken en installeer Ansible voor een Hallo distributies te volgen:

- [Ubuntu 16.04 TNS](#ubuntu1604-lts)
- [7.3 centOS](#centos-73)
- [SLES 12.2 SP2](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS
Maak een VM met [az vm create](/cli/azure/vm#create). Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour met behulp van VM Hallo `publicIpAddress` hebt genoteerd in Hallo Maakbewerking van de uitvoer van Hallo VM:

```bash
ssh azureuser@<publicIpAddress>
```

Op de virtuele machine, vereist hello-pakketten voor hello Azure Python SDK-modules en Ansible als volgt te installeren:

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

Nu verder te[maken Azure-referenties](#create-azure-credentials).


### <a name="centos-73"></a>7.3 centOS
Maak een VM met [az vm create](/cli/azure/vm#create). Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour met behulp van VM Hallo `publicIpAddress` hebt genoteerd in Hallo Maakbewerking van de uitvoer van Hallo VM:

```bash
ssh azureuser@<publicIpAddress>
```

Op de virtuele machine, vereist hello-pakketten voor hello Azure Python SDK-modules en Ansible als volgt te installeren:

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

Nu verder te[maken Azure-referenties](#create-azure-credentials).


### <a name="sles-122-sp2"></a>SLES 12.2 SP2
Maak een VM met [az vm create](/cli/azure/vm#create). Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour met behulp van VM Hallo `publicIpAddress` hebt genoteerd in Hallo Maakbewerking van de uitvoer van Hallo VM:

```bash
ssh azureuser@<publicIpAddress>
```

Op de virtuele machine, vereist hello-pakketten voor hello Azure Python SDK-modules en Ansible als volgt te installeren:

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

Nu verder te[maken Azure-referenties](#create-azure-credentials).


## <a name="create-azure-credentials"></a>Azure-referenties maken
Ansible communiceert met Azure met behulp van een gebruikersnaam en wachtwoord of een service-principal. Een Azure-service-principal is een beveiligings-id die u met apps, services en automatiseringsprogramma's zoals Ansible gebruiken kunt. U bepaalt de en definieer Hallo machtigingen als toowhat operations Hallo service-principal in Azure uitvoeren kunt. tooimprove beveiliging via gewoon een gebruikersnaam en wachtwoord voor het bieden, in dit voorbeeld wordt een basic service principal.

Maken van een service principal met [az ad sp maken-voor-rbac](/cli/azure/ad/sp#create-for-rbac) en uitvoer Hallo de referenties die Ansible moet:

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

Een voorbeeld van uitvoer Hallo van Hallo voorgaande opdrachten is als volgt:

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

tooauthenticate tooAzure, moet u ook uw Azure-abonnement-ID met tooobtain [az account weergeven](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

U Hallo-uitvoer van deze twee opdrachten in de volgende stap hello gebruiken.


## <a name="create-ansible-credentials-file"></a>Ansible referentiebestand maken
tooprovide tooAnsible referenties, u omgevingsvariabelen definiëren of maak een bestand lokale referenties. Voor meer informatie over het toodefine Ansible referenties, Zie [referenties bieden tooAzure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules). 

Voor een ontwikkelingsomgeving, maakt u een *referenties* voor Ansible bestand op de VM-host als volgt:

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

Hallo *referenties* bestand zelf Hallo abonnements-ID combineert met de Hallo-uitvoer van het maken van een service-principal. De uitvoer van de vorige Hallo [az ad sp maken-voor-rbac](/cli/azure/ad/sp#create-for-rbac) opdracht is Hallo dezelfde volgorde nodig zijn voor *client_id*, *geheim*, en *tenant* . Hallo volgende voorbeeld *referenties* bestand ziet u deze waarden die overeenkomen met de vorige uitvoer Hallo. Voer uw eigen waarden als volgt:

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a>Omgevingsvariabelen Ansible gebruiken
Als u toouse hulpprogramma's zoals Ansible Tower of Jenkins gaat, kunt u als volgt omgevingsvariabelen definiëren. Deze variabelen worden gecombineerd Hallo abonnements-ID met Hallo-uitvoer van een service-principal maken. De uitvoer van de vorige Hallo [az ad sp maken-voor-rbac](/cli/azure/ad/sp#create-for-rbac) opdracht is Hallo dezelfde volgorde nodig zijn voor *AZURE_CLIENT_ID*, *AZURE_SECRET*, en *AZURE_ TENANT*. 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a>Volgende stappen
U hebt nu Ansible en hello Azure Python SDK-modules die zijn geïnstalleerd en de referenties die zijn gedefinieerd voor Ansible toouse vereist. Meer informatie over hoe te[een virtuele machine maken met Ansible](ansible-create-vm.md). U kunt ook meer te weten hoe te[een volledige Azure-virtuele machine maken en de ondersteunende resources met Ansible](ansible-create-complete-vm.md).
