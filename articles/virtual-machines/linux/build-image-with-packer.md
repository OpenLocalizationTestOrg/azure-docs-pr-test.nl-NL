---
title: "aaaHow toocreate Linux Azure VM-installatiekopieën met verpakker | Microsoft Docs"
description: Meer informatie over hoe toouse verpakker toocreate afbeeldingen van Linux virtuele machines in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: 5990598859e73efac477884bc8de5fd5138bf6e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-linux-virtual-machine-images-in-azure"></a>Hoe installatiekopieën van toouse verpakker toocreate virtuele Linux-machine in Azure
Elke virtuele machine (VM) in Azure wordt gemaakt van een installatiekopie die Hallo Linux-distributie en versie van het besturingssysteem definieert. Voorbeelden van afbeeldingen zijn vooraf geïnstalleerde toepassingen en configuraties. Hello Azure Marketplace bevat veel installatiekopieën van het eerste en derde partij voor het meest voorkomende distributies en omgevingen met toepassingen, of kunt u uw eigen aangepaste installatiekopieën die zijn afgestemd tooyour behoeften. Dit artikel wordt uitgelegd hoe de bron-hulpprogramma voor het openen van toouse Hallo [verpakker](https://www.packer.io/) toodefine en build aangepaste installatiekopieën in Azure.


## <a name="create-azure-resource-group"></a>Azure-resourcegroep maken
Tijdens Hallo maken maakt verpakker tijdelijke Azure-resources als builds Hallo bron-VM. toocapture die VM voor gebruik als een installatiekopie van een gegevensbron, moet u een resourcegroep definiëren. Hallo wordt uitvoer van Hallo verpakker buildproces opgeslagen in deze resourcegroep.

Maak een resourcegroep maken met [az group create](/cli/azure/group#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a>Azure-referenties maken
Verpakker verifieert met Azure met behulp van een service-principal. Een Azure-service-principal is een beveiligings-id die u met apps, services en automatiseringsprogramma's zoals verpakker kunt gebruiken. U bepaalt de en definieer Hallo machtigingen als toowhat operations Hallo service-principal in Azure uitvoeren kunt.

Maken van een service principal met [az ad sp maken-voor-rbac](/cli/azure/ad/sp#create-for-rbac) en uitvoer Hallo de referenties die verpakker moet:

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

Een voorbeeld van uitvoer Hallo van Hallo voorgaande opdrachten is als volgt:

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

tooauthenticate tooAzure, moet u ook uw Azure-abonnement-ID met tooobtain [az account weergeven](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

U Hallo-uitvoer van deze twee opdrachten in de volgende stap hello gebruiken.


## <a name="define-packer-template"></a>Verpakker sjabloon definiëren
toobuild afbeeldingen, maakt u een sjabloon als een JSON-bestand. In de sjabloon hello, definieert u opbouwfuncties en buildproces provisioners die Hallo werkelijke uitvoeren. Verpakker heeft een [provisioner voor Azure](https://www.packer.io/docs/builders/azure.html) waarmee u toodefine Azure resources, zoals Hallo principal Servicereferenties in Hallo voorgaande stap hebt gemaakt.

Maak een bestand met de naam *ubuntu.json* en inhoud te plakken Hallo volgen. Geef uw eigen waarden voor Hallo volgende:

| Parameter                           | Waar tooobtain |
|-------------------------------------|----------------------------------------------------|
| *client_id*                         | Eerste regel van de uitvoer van `az ad sp` maken command - *appId* |
| *client_secret*                     | Lijn van uitvoer van de tweede `az ad sp` maken command - *wachtwoord* |
| *tenant_id*                         | Derde regel van uitvoer van `az ad sp` maken command - *tenant* |
| *subscription_id*                   | De uitvoer van `az account show` opdracht |
| *managed_image_resource_group_name* | Naam van resourcegroep die u hebt gemaakt in de eerste stap Hallo |
| *managed_image_name*                | Naam voor Hallo beheerde installatiekopie die is gemaakt |


```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Linux",
    "image_publisher": "Canonical",
    "image_offer": "UbuntuServer",
    "image_sku": "16.04-LTS",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "execute_command": "chmod +x {{ .Path }}; {{ .Vars }} sudo -E sh '{{ .Path }}'",
    "inline": [
      "apt-get update",
      "apt-get upgrade -y",
      "apt-get -y install nginx",

      "/usr/sbin/waagent -force -deprovision+user && export HISTSIZE=0 && sync"
    ],
    "inline_shebang": "/bin/sh -x",
    "type": "shell"
  }]
}
```

Deze sjabloon maakt een installatiekopie van een virtuele Ubuntu 16.04 TNS, NGINX installeert en deprovisions Hallo VM.

> [!NOTE]
> Als u deze sjabloon tooprovision gebruikersreferenties uitbreiden, aanpassen Hallo provisioner opdracht dat deprovisions hello Azure-agent tooread `-deprovision` plaats `deprovision+user`.
> Hallo `+user` vlag verwijdert alle gebruikersaccounts uit Hallo bron-VM.


## <a name="build-packer-image"></a>Verpakker installatiekopie maken
Als u nog niet geïnstalleerd op uw lokale machine verpakker hebt [Volg Hallo verpakker installatie-instructies](https://www.packer.io/docs/install/index.html).

Hallo image samenstellen door te geven van uw verpakker sjabloonbestand als volgt:

```bash
./packer build ubuntu.json
```

Een voorbeeld van uitvoer Hallo van Hallo voorgaande opdrachten is als volgt:

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> dept : Engineering
==> azure-arm:  ->> task : Image deployment
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH toobecome available...
==> azure-arm: Connected tooSSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! hello waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able toologin as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-swtxmqm7ly/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Compute Name              : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a>Virtuele machine van de afbeelding voor Azure maken
U kunt nu een virtuele machine maken van de installatiekopie met [az vm maken](/cli/azure/vm#create). Geef Hallo installatiekopie die u hebt gemaakt met de Hallo `--image` parameter. Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM* van *myPackerImage* en SSH-sleutels genereert als deze niet al bestaan:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

Het duurt enkele minuten toocreate Hallo VM. Zodra Hallo VM is gemaakt, noteer Hallo `publicIpAddress` weergegeven door hello Azure CLI. Dit adres is gebruikte tooaccess hello NGINX site via een webbrowser.

virtuele machine, open poort 80 van Hallo Internet met het web verkeer tooreach tooallow [az vm open poort](/cli/azure/vm#open-port):

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a>Virtuele machine en NGINX testen
Nu kunt u een webbrowser openen en voer `http://publicIpAddress` in de adresbalk Hallo. Geef uw eigen openbare IP-adres uit Hallo VM proces maken. Hallo standaard NGINX-pagina wordt weergegeven zoals in het volgende voorbeeld Hallo:

![Standaardsite van NGINX](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a>Volgende stappen
In dit voorbeeld gebruikt u verpakker toocreate een VM-installatiekopie met NGINX al is geïnstalleerd. U kunt deze VM-installatiekopie samen met de bestaande implementatiewerkstromen, zoals uw app tooVMs van de installatiekopie met Ansible, Chef of Puppet hello gemaakt toodeploy gebruiken.

Zie voor aanvullende voorbeeld verpakker sjablonen voor andere Linux-distributies, [deze GitHub-repo-](https://github.com/hashicorp/packer/tree/master/examples/azure).