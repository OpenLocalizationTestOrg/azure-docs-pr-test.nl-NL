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
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a><span data-ttu-id="f9333-103">Hoe tooinstall en MongoDB configureren op een Linux-VM</span><span class="sxs-lookup"><span data-stu-id="f9333-103">How tooinstall and configure MongoDB on a Linux VM</span></span>
<span data-ttu-id="f9333-104">[MongoDB](http://www.mongodb.org) is een populaire open-source, hoogwaardige NoSQL-database.</span><span class="sxs-lookup"><span data-stu-id="f9333-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="f9333-105">Dit artikel ziet u hoe tooinstall en MongoDB configureren op een Linux-VM met hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="f9333-105">This article shows you how tooinstall and configure MongoDB on a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="f9333-106">U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](install-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f9333-106">You can also perform these steps with hello [Azure CLI 1.0](install-mongodb-nodejs.md).</span></span> <span data-ttu-id="f9333-107">Voorbeelden worden weergegeven dat detail hoe naar:</span><span class="sxs-lookup"><span data-stu-id="f9333-107">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="f9333-108">Handmatig installeren en configureren van een eenvoudige MongoDB-exemplaar</span><span class="sxs-lookup"><span data-stu-id="f9333-108">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="f9333-109">Een basic MongoDB-exemplaar met een Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="f9333-109">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="f9333-110">Een complexe MongoDB shard-cluster met de replica wordt ingesteld met een Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="f9333-110">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="f9333-111">Handmatig installeren en configureren van MongoDB op een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="f9333-111">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="f9333-112">MongoDB [installatie-instructies](https://docs.mongodb.com/manual/administration/install-on-linux/) voor Linux-distributies met inbegrip van Red Hat / CentOS, SUSE, Ubuntu en Debian.</span><span class="sxs-lookup"><span data-stu-id="f9333-112">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="f9333-113">Hallo volgende voorbeeld wordt een *CentOS* VM.</span><span class="sxs-lookup"><span data-stu-id="f9333-113">hello following example creates a *CentOS* VM.</span></span> <span data-ttu-id="f9333-114">toocreate deze omgeving moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="f9333-114">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="f9333-115">Maak een resourcegroep maken met [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f9333-115">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f9333-116">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="f9333-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="f9333-117">Maak een VM met [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="f9333-117">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="f9333-118">Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM* aan een gebruiker met de naam *azureuser* met behulp van SSH-verificatie voor openbare sleutel</span><span class="sxs-lookup"><span data-stu-id="f9333-118">hello following example creates a VM named *myVM* with a user named *azureuser* using SSH public key authentication</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="f9333-119">SSH toohello VM die gebruikmaakt van uw eigen gebruikersnaam en het Hallo `publicIpAddress` die worden vermeld in de uitvoer van de vorige stap Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="f9333-119">SSH toohello VM using your own username and hello `publicIpAddress` listed in hello output from hello previous step:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="f9333-120">tooadd hello installatiebronnen voor MongoDB, maak een **yum** opslagplaatsbestand als volgt:</span><span class="sxs-lookup"><span data-stu-id="f9333-120">tooadd hello installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="f9333-121">Hallo MongoDB-repo-bestand voor het bewerken van openen.</span><span class="sxs-lookup"><span data-stu-id="f9333-121">Open hello MongoDB repo file for editing.</span></span> <span data-ttu-id="f9333-122">Hallo volgende regels toevoegen:</span><span class="sxs-lookup"><span data-stu-id="f9333-122">Add hello following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="f9333-123">Installeren met behulp van MongoDB **yum** als volgt:</span><span class="sxs-lookup"><span data-stu-id="f9333-123">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="f9333-124">SELinux wordt standaard afgedwongen voor installatiekopieën van CentOS die voorkomen dat u toegang tot MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f9333-124">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="f9333-125">Beheerhulpprogramma's voor installeren en SELinux tooallow MongoDB toooperate op de standaard TCP-poort 27017 als volgt configureren:</span><span class="sxs-lookup"><span data-stu-id="f9333-125">Install policy management tools and configure SELinux tooallow MongoDB toooperate on its default TCP port 27017 as follows:</span></span>

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="f9333-126">Start Hallo MongoDB-service als volgt:</span><span class="sxs-lookup"><span data-stu-id="f9333-126">Start hello MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="f9333-127">Hallo MongoDB installatie controleren door verbinding te maken met behulp van de lokale Hallo `mongo` client:</span><span class="sxs-lookup"><span data-stu-id="f9333-127">Verify hello MongoDB installation by connecting using hello local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="f9333-128">Hallo MongoDB-exemplaar nu testen door een aantal gegevens toe te voegen en vervolgens te zoeken:</span><span class="sxs-lookup"><span data-stu-id="f9333-128">Now test hello MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="f9333-129">Indien gewenst, MongoDB toostart automatisch configureren tijdens opstarten:</span><span class="sxs-lookup"><span data-stu-id="f9333-129">If desired, configure MongoDB toostart automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="f9333-130">Basic MongoDB-exemplaar op CentOS met een sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="f9333-130">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="f9333-131">U kunt basic MongoDB-exemplaar maken op een enkele CentOS virtuele machine met behulp van hello Azure snelstartsjabloon met de volgende uit GitHub.</span><span class="sxs-lookup"><span data-stu-id="f9333-131">You can create a basic MongoDB instance on a single CentOS VM using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="f9333-132">Deze sjabloon maakt gebruik van Hallo aangepaste scriptextensie voor Linux tooadd een **yum** tooyour opslagplaats nieuw gemaakte CentOS VM en installeer vervolgens MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f9333-132">This template uses hello Custom Script extension for Linux tooadd a **yum** repository tooyour newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="f9333-133">[Basic MongoDB-exemplaar op CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="f9333-133">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="f9333-134">toocreate deze omgeving moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="f9333-134">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="f9333-135">Maak eerst een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f9333-135">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f9333-136">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="f9333-136">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="f9333-137">Vervolgens implementeert u Hallo MongoDB-sjabloon met [az implementatie maken](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="f9333-137">Next, deploy hello MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="f9333-138">Definieer uw eigen resource namen en waar nodig zoals als voor groottes *newStorageAccountName*, *virtualNetworkName*, en *vmSize*:</span><span class="sxs-lookup"><span data-stu-id="f9333-138">Define your own resource names and sizes where needed such as for *newStorageAccountName*, *virtualNetworkName*, and *vmSize*:</span></span>

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

<span data-ttu-id="f9333-139">Meld u aan toohello VM Hallo openbare DNS-adres van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f9333-139">Log on toohello VM using hello public DNS address of your VM.</span></span> <span data-ttu-id="f9333-140">U kunt de openbare DNS-serveradres Hallo met weergeven [az vm weergeven](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="f9333-140">You can view hello public DNS address with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

<span data-ttu-id="f9333-141">SSH tooyour VM die gebruikmaakt van uw eigen gebruikersnaam en een openbare DNS-adres:</span><span class="sxs-lookup"><span data-stu-id="f9333-141">SSH tooyour VM using your own username and public DNS address:</span></span>

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="f9333-142">Hallo MongoDB installatie controleren door verbinding te maken met behulp van de lokale Hallo `mongo` client als volgt:</span><span class="sxs-lookup"><span data-stu-id="f9333-142">Verify hello MongoDB installation by connecting using hello local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="f9333-143">Test nu Hallo exemplaar sommige gegevens toe te voegen en zoek het als volgt:</span><span class="sxs-lookup"><span data-stu-id="f9333-143">Now test hello instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="f9333-144">Een complexe MongoDB Shard-Cluster op CentOS met een sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="f9333-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="f9333-145">U kunt een complexe MongoDB shard cluster met behulp van de volgende Azure quickstart-sjabloon uit GitHub Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="f9333-145">You can create a complex MongoDB sharded cluster using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="f9333-146">Deze sjabloon volgt Hallo [MongoDB shard cluster aanbevolen procedures](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundantie en hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="f9333-146">This template follows hello [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancy and high availability.</span></span> <span data-ttu-id="f9333-147">Hallo-sjabloon maakt twee shards met drie knooppunten replicaset.</span><span class="sxs-lookup"><span data-stu-id="f9333-147">hello template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="f9333-148">Een config server replicaset met drie knooppunten ook wordt gemaakt, plus twee **mongos** router servers tooprovide consistentie tooapplications uit via Hallo shards.</span><span class="sxs-lookup"><span data-stu-id="f9333-148">One config server replica set with three nodes is also created, plus two **mongos** router servers tooprovide consistency tooapplications from across hello shards.</span></span>

* <span data-ttu-id="f9333-149">[MongoDB Sharding-Cluster op CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="f9333-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="f9333-150">Dit complexe MongoDB shard-cluster implementeren vereist meer dan 20 cores die meestal Hallo standaard core-telling per regio voor een abonnement.</span><span class="sxs-lookup"><span data-stu-id="f9333-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically hello default core count per region for a subscription.</span></span> <span data-ttu-id="f9333-151">Open een Azure ondersteuningsverzoek tooincrease core-telling.</span><span class="sxs-lookup"><span data-stu-id="f9333-151">Open an Azure support request tooincrease your core count.</span></span>

<span data-ttu-id="f9333-152">toocreate deze omgeving moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="f9333-152">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="f9333-153">Maak eerst een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f9333-153">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f9333-154">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="f9333-154">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="f9333-155">Vervolgens implementeert u Hallo MongoDB-sjabloon met [az implementatie maken](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="f9333-155">Next, deploy hello MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="f9333-156">Definieer uw eigen resource namen en waar nodig zoals als voor groottes *mongoAdminUsername*, *sizeOfDataDiskInGB*, en *configNodeVmSize*:</span><span class="sxs-lookup"><span data-stu-id="f9333-156">Define your own resource names and sizes where needed such as for *mongoAdminUsername*, *sizeOfDataDiskInGB*, and *configNodeVmSize*:</span></span>

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

<span data-ttu-id="f9333-157">Deze implementatie kan ruim een uur toodeploy duren en alle Hallo VM-instanties configureren.</span><span class="sxs-lookup"><span data-stu-id="f9333-157">This deployment can take over an hour toodeploy and configure all hello VM instances.</span></span> <span data-ttu-id="f9333-158">Hallo `--no-wait` markering achter Hallo Hallo voorafgaand aan de opdracht tooreturn besturingselement toohello-opdrachtprompt wanneer Hallo sjabloonimplementatie is geaccepteerd door hello Azure-platform wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f9333-158">hello `--no-wait` flag is used at hello end of hello preceding command tooreturn control toohello command prompt once hello template deployment has been accepted by hello Azure platform.</span></span> <span data-ttu-id="f9333-159">Vervolgens kunt u de implementatiestatus Hallo met bekijken [az groep implementatie weergeven](/cli/azure/group/deployment#show).</span><span class="sxs-lookup"><span data-stu-id="f9333-159">You can then view hello deployment status with [az group deployment show](/cli/azure/group/deployment#show).</span></span> <span data-ttu-id="f9333-160">Hallo volgende voorbeeld weergaven Hallo status voor Hallo *myMongoDBCluster* -implementatie in Hallo *myResourceGroup* resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="f9333-160">hello following example views hello status for hello *myMongoDBCluster* deployment in hello *myResourceGroup* resource group:</span></span>

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a><span data-ttu-id="f9333-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f9333-161">Next steps</span></span>
<span data-ttu-id="f9333-162">In deze voorbeelden u lokaal verbinding maken met toohello MongoDB-exemplaar van Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="f9333-162">In these examples, you connect toohello MongoDB instance locally from hello VM.</span></span> <span data-ttu-id="f9333-163">Als u tooconnect toohello MongoDB-exemplaar van een andere virtuele machine of een netwerk wilt, zorg ervoor dat de juiste Hallo [Netwerkbeveiligingsgroep regels zijn gemaakt](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="f9333-163">If you want tooconnect toohello MongoDB instance from another VM or network, ensure hello appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="f9333-164">Deze voorbeelden implementeren Hallo core MongoDB-omgeving voor ontwikkelingsdoeleinden.</span><span class="sxs-lookup"><span data-stu-id="f9333-164">These examples deploy hello core MongoDB environment for development purposes.</span></span> <span data-ttu-id="f9333-165">Toepassing hello vereist beveiliging configuratieopties voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="f9333-165">Apply hello required security configuration options for your environment.</span></span> <span data-ttu-id="f9333-166">Zie voor meer informatie, Hallo [MongoDB beveiliging docs](https://docs.mongodb.com/manual/security/).</span><span class="sxs-lookup"><span data-stu-id="f9333-166">For more information, see hello [MongoDB security docs](https://docs.mongodb.com/manual/security/).</span></span>

<span data-ttu-id="f9333-167">Zie voor meer informatie over het maken van sjablonen Hallo [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9333-167">For more information about creating using templates, see hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="f9333-168">Hello Azure Resource Manager-sjablonen gebruiken Hallo aangepaste Scriptextensie toodownload en scripts uitvoeren op uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="f9333-168">hello Azure Resource Manager templates use hello Custom Script Extension toodownload and execute scripts on your VMs.</span></span> <span data-ttu-id="f9333-169">Zie voor meer informatie [Using hello Azure aangepaste Scriptextensie met virtuele Linux-Machines](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="f9333-169">For more information, see [Using hello Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

