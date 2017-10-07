---
title: aaaInstall MongoDB op een Linux-VM met hello Azure CLI | Microsoft Docs
description: Meer informatie over hoe tooinstall en MongoDB configureren op een Linux virtuele machine iusing hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 97a4d9913f0eeaf7b8bf15d7fc81befe538cdc8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a>Hoe tooinstall en MongoDB configureren op een Linux-VM
[MongoDB](http://www.mongodb.org) is een populaire open-source, hoogwaardige NoSQL-database. Dit artikel ziet u hoe tooinstall en MongoDB configureren op een Linux-VM met hello Azure CLI 2.0. U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](install-mongodb-nodejs.md). Voorbeelden worden weergegeven dat detail hoe naar:

* [Handmatig installeren en configureren van een eenvoudige MongoDB-exemplaar](#manually-install-and-configure-mongodb-on-a-vm)
* [Een basic MongoDB-exemplaar met een Resource Manager-sjabloon maken](#create-basic-mongodb-instance-on-centos-using-a-template)
* [Een complexe MongoDB shard-cluster met de replica wordt ingesteld met een Resource Manager-sjabloon maken](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>Handmatig installeren en configureren van MongoDB op een virtuele machine
MongoDB [installatie-instructies](https://docs.mongodb.com/manual/administration/install-on-linux/) voor Linux-distributies met inbegrip van Red Hat / CentOS, SUSE, Ubuntu en Debian. Hallo volgende voorbeeld wordt een *CentOS* VM. toocreate deze omgeving moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).

Maak een resourcegroep maken met [az group create](/cli/azure/group#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:

```azurecli
az group create --name myResourceGroup --location eastus
```

Maak een VM met [az vm create](/cli/azure/vm#create). Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM* aan een gebruiker met de naam *azureuser* met behulp van SSH-verificatie voor openbare sleutel

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH toohello VM die gebruikmaakt van uw eigen gebruikersnaam en het Hallo `publicIpAddress` die worden vermeld in de uitvoer van de vorige stap Hallo Hallo:

```bash
ssh azureuser@<publicIpAddress>
```

tooadd hello installatiebronnen voor MongoDB, maak een **yum** opslagplaatsbestand als volgt:

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

Hallo MongoDB-repo-bestand voor het bewerken van openen. Hallo volgende regels toevoegen:

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

Installeren met behulp van MongoDB **yum** als volgt:

```bash
sudo yum install -y mongodb-org
```

SELinux wordt standaard afgedwongen voor installatiekopieën van CentOS die voorkomen dat u toegang tot MongoDB. Beheerhulpprogramma's voor installeren en SELinux tooallow MongoDB toooperate op de standaard TCP-poort 27017 als volgt configureren:

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

Start Hallo MongoDB-service als volgt:

```bash
sudo service mongod start
```

Hallo MongoDB installatie controleren door verbinding te maken met behulp van de lokale Hallo `mongo` client:

```bash
mongo
```

Hallo MongoDB-exemplaar nu testen door een aantal gegevens toe te voegen en vervolgens te zoeken:

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

Indien gewenst, MongoDB toostart automatisch configureren tijdens opstarten:

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a>Basic MongoDB-exemplaar op CentOS met een sjabloon maken
U kunt basic MongoDB-exemplaar maken op een enkele CentOS virtuele machine met behulp van hello Azure snelstartsjabloon met de volgende uit GitHub. Deze sjabloon maakt gebruik van Hallo aangepaste scriptextensie voor Linux tooadd een **yum** tooyour opslagplaats nieuw gemaakte CentOS VM en installeer vervolgens MongoDB.

* [Basic MongoDB-exemplaar op CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json

toocreate deze omgeving moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login). Maak eerst een resourcegroep met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:

```azurecli
az group create --name myResourceGroup --location eastus
```

Vervolgens implementeert u Hallo MongoDB-sjabloon met [az implementatie maken](/cli/azure/group/deployment#create). Definieer uw eigen resource namen en waar nodig zoals als voor groottes *newStorageAccountName*, *virtualNetworkName*, en *vmSize*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"},
    "virtualNetworkName": {"value": "myVnet"},
    "vmSize": {"value": "Standard_DS2_v2"},
    "vmName": {"value": "myVM"},
    "publicIPAddressName": {"value": "myPublicIP"},
    "nicName": {"value": "myNic"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

Meld u aan toohello VM Hallo openbare DNS-adres van uw virtuele machine. U kunt de openbare DNS-serveradres Hallo met weergeven [az vm weergeven](/cli/azure/vm#show):

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

SSH tooyour VM die gebruikmaakt van uw eigen gebruikersnaam en een openbare DNS-adres:

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

Hallo MongoDB installatie controleren door verbinding te maken met behulp van de lokale Hallo `mongo` client als volgt:

```bash
mongo
```

Test nu Hallo exemplaar sommige gegevens toe te voegen en zoek het als volgt:

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a>Een complexe MongoDB Shard-Cluster op CentOS met een sjabloon maken
U kunt een complexe MongoDB shard cluster met behulp van de volgende Azure quickstart-sjabloon uit GitHub Hallo maken. Deze sjabloon volgt Hallo [MongoDB shard cluster aanbevolen procedures](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundantie en hoge beschikbaarheid. Hallo-sjabloon maakt twee shards met drie knooppunten replicaset. Een config server replicaset met drie knooppunten ook wordt gemaakt, plus twee **mongos** router servers tooprovide consistentie tooapplications uit via Hallo shards.

* [MongoDB Sharding-Cluster op CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json

> [!WARNING]
> Dit complexe MongoDB shard-cluster implementeren vereist meer dan 20 cores die meestal Hallo standaard core-telling per regio voor een abonnement. Open een Azure ondersteuningsverzoek tooincrease core-telling.

toocreate deze omgeving moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login). Maak eerst een resourcegroep met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:

```azurecli
az group create --name myResourceGroup --location eastus
```

Vervolgens implementeert u Hallo MongoDB-sjabloon met [az implementatie maken](/cli/azure/group/deployment#create). Definieer uw eigen resource namen en waar nodig zoals als voor groottes *mongoAdminUsername*, *sizeOfDataDiskInGB*, en *configNodeVmSize*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "mongoAdminUsername": {"value": "mongoadmin"},
    "mongoAdminPassword": {"value": "P@ssw0rd!"},
    "dnsNamePrefix": {"value": "mypublicdns"},
    "environment": {"value": "AzureCloud"},
    "numDataDisks": {"value": "4"},
    "sizeOfDataDiskInGB": {"value": 20},
    "centOsVersion": {"value": "7.0"},
    "routerNodeVmSize": {"value": "Standard_DS3_v2"},
    "configNodeVmSize": {"value": "Standard_DS3_v2"},
    "replicaNodeVmSize": {"value": "Standard_DS3_v2"},
    "zabbixServerIPAddress": {"value": "Null"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json \
  --name myMongoDBCluster \
  --no-wait
```

Deze implementatie kan ruim een uur toodeploy duren en alle Hallo VM-instanties configureren. Hallo `--no-wait` markering achter Hallo Hallo voorafgaand aan de opdracht tooreturn besturingselement toohello-opdrachtprompt wanneer Hallo sjabloonimplementatie is geaccepteerd door hello Azure-platform wordt gebruikt. Vervolgens kunt u de implementatiestatus Hallo met bekijken [az groep implementatie weergeven](/cli/azure/group/deployment#show). Hallo volgende voorbeeld weergaven Hallo status voor Hallo *myMongoDBCluster* -implementatie in Hallo *myResourceGroup* resourcegroep:

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a>Volgende stappen
In deze voorbeelden u lokaal verbinding maken met toohello MongoDB-exemplaar van Hallo VM. Als u tooconnect toohello MongoDB-exemplaar van een andere virtuele machine of een netwerk wilt, zorg ervoor dat de juiste Hallo [Netwerkbeveiligingsgroep regels zijn gemaakt](nsg-quickstart.md).

Deze voorbeelden implementeren Hallo core MongoDB-omgeving voor ontwikkelingsdoeleinden. Toepassing hello vereist beveiliging configuratieopties voor uw omgeving. Zie voor meer informatie, Hallo [MongoDB beveiliging docs](https://docs.mongodb.com/manual/security/).

Zie voor meer informatie over het maken van sjablonen Hallo [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

Hello Azure Resource Manager-sjablonen gebruiken Hallo aangepaste Scriptextensie toodownload en scripts uitvoeren op uw virtuele machines. Zie voor meer informatie [Using hello Azure aangepaste Scriptextensie met virtuele Linux-Machines](extensions-customscript.md).

