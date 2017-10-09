---
title: aaaInstall MongoDB op een Linux-VM met behulp van Azure CLI 1.0 Hallo | Microsoft Docs
description: Meer informatie over hoe tooinstall en MongoDB configureren op een virtuele Linux-machine in Azure met behulp van Hallo Resource Manager-implementatiemodel.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 4ce21a2c63da7d00a4422e0a6766e2103e7f12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm-using-hello-azure-cli-10"></a>Hoe tooinstall en MongoDB configureren op een Linux-VM met hello Azure CLI 1.0
[MongoDB](http://www.mongodb.org) is een populaire open-source, hoogwaardige NoSQL-database. Dit artikel ziet u hoe tooinstall en MongoDB configureren op een Linux VM in Azure met Hallo Resource Manager-implementatiemodel. Voorbeelden worden weergegeven dat detail hoe naar:

* [Handmatig installeren en configureren van een eenvoudige MongoDB-exemplaar](#manually-install-and-configure-mongodb-on-a-vm)
* [Een basic MongoDB-exemplaar met een Resource Manager-sjabloon maken](#create-basic-mongodb-instance-on-centos-using-a-template)
* [Een complexe MongoDB shard-cluster met de replica wordt ingesteld met een Resource Manager-sjabloon maken](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- Azure CLI 1.0 – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](create-cli-complete-nodejs.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>Handmatig installeren en configureren van MongoDB op een virtuele machine
MongoDB [installatie-instructies](https://docs.mongodb.com/manual/administration/install-on-linux/) voor Linux-distributies met inbegrip van Red Hat / CentOS, SUSE, Ubuntu en Debian. Hallo volgende voorbeeld wordt een *CentOS* VM die gebruikmaakt van een SSH-sleutel die is opgeslagen op *~/.ssh/id_rsa.pub*. Antwoord Hallo vraagt om de naam van het opslagaccount, DNS-naam en -referenties:

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

Meld u aan toohello VM Hallo openbaar IP-adres weergegeven aan einde Hallo Hallo voorafgaand aan de virtuele machine maken stap met:

```bash
ssh azureuser@40.78.23.145
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

SELinux wordt standaard afgedwongen voor installatiekopieën van CentOS die voorkomen dat u toegang tot MongoDB. Beheerhulpprogramma's voor installeren en SELinux tooallow MongoDB toooperate als volgt op de standaard TCP-poort 27017 configureren. 

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
U kunt basic MongoDB-exemplaar maken op een enkele CentOS virtuele machine met behulp van hello Azure snelstartsjabloon met de volgende uit GitHub. Deze sjabloon maakt gebruik van Hallo aangepaste scriptextensie voor Linux tooadd een `yum` tooyour opslagplaats nieuw gemaakte CentOS VM en installeer vervolgens MongoDB.

* [Basic MongoDB-exemplaar op CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json

Hallo volgende voorbeeld wordt een resourcegroep met de naam van de Hallo `myResourceGroup` in Hallo `eastus` regio. Voer uw eigen waarden als volgt:

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> Hello Azure CLI retourneert u tooa prompt binnen een paar seconden voor het maken van Hallo-implementatie, maar de Hallo-installatie en configuratie duurt een paar minuten toocomplete. Controleer de status van Hallo Hallo-implementatie met `azure group deployment show myResourceGroup`, Hallo-naam van de resourcegroep dienovereenkomstig in te voeren. Wachten tot Hallo **ProvisioningState** toont *geslaagd* voordat de poging tooSSH toohello VM.

Als de Hallo-implementatie is voltooid, SSH toohello VM. Hallo IP-adres van uw virtuele machine met behulp van Hallo `azure vm show` opdracht zoals Hallo volgt in:

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

In de buurt Hallo einde van Hallo-uitvoer, wordt Hallo openbaar IP-adres weergegeven. SSH tooyour VM met Hallo IP-adres van uw virtuele machine:

```bash
ssh azureuser@138.91.149.74
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

Hallo volgende voorbeeld wordt een resourcegroep met de naam van de Hallo *myResourceGroup* in Hallo *eastus* regio. Voer uw eigen waarden als volgt:

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> Hello Azure CLI retourneert u tooa prompt binnen een paar seconden na het Hallo-implementatie wordt gemaakt, maar hello installatie en configuratie overnemen een toocomplete uur. Controleer de status van Hallo Hallo-implementatie met `azure group deployment show myResourceGroup`, het Hallo-naam van de resourcegroep dienovereenkomstig aanpassen. Wachten tot Hallo **ProvisioningState** toont *geslaagd* voordat VMs toohello verbinding wordt gemaakt.


## <a name="next-steps"></a>Volgende stappen
In deze voorbeelden u lokaal verbinding maken met toohello MongoDB-exemplaar van Hallo VM. Als u tooconnect toohello MongoDB-exemplaar van een andere virtuele machine of een netwerk wilt, zorg ervoor dat de juiste Hallo [Netwerkbeveiligingsgroep regels zijn gemaakt](nsg-quickstart.md).

Zie voor meer informatie over het maken van sjablonen Hallo [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

Hello Azure Resource Manager-sjablonen gebruiken Hallo aangepaste Scriptextensie toodownload en scripts uitvoeren op uw virtuele machines. Zie voor meer informatie [Using hello Azure aangepaste Scriptextensie met virtuele Linux-Machines](extensions-customscript.md).

