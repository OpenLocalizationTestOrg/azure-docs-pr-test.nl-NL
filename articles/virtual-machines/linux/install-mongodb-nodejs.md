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
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm-using-hello-azure-cli-10"></a><span data-ttu-id="a27df-103">Hoe tooinstall en MongoDB configureren op een Linux-VM met hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a27df-103">How tooinstall and configure MongoDB on a Linux VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="a27df-104">[MongoDB](http://www.mongodb.org) is een populaire open-source, hoogwaardige NoSQL-database.</span><span class="sxs-lookup"><span data-stu-id="a27df-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="a27df-105">Dit artikel ziet u hoe tooinstall en MongoDB configureren op een Linux VM in Azure met Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="a27df-105">This article shows you how tooinstall and configure MongoDB on a Linux VM in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="a27df-106">Voorbeelden worden weergegeven dat detail hoe naar:</span><span class="sxs-lookup"><span data-stu-id="a27df-106">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="a27df-107">Handmatig installeren en configureren van een eenvoudige MongoDB-exemplaar</span><span class="sxs-lookup"><span data-stu-id="a27df-107">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="a27df-108">Een basic MongoDB-exemplaar met een Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="a27df-108">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="a27df-109">Een complexe MongoDB shard-cluster met de replica wordt ingesteld met een Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="a27df-109">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="a27df-110">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="a27df-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="a27df-111">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a27df-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="a27df-112">Azure CLI 1.0 – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="a27df-112">Azure CLI 1.0 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="a27df-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="a27df-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="a27df-114">Handmatig installeren en configureren van MongoDB op een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="a27df-114">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="a27df-115">MongoDB [installatie-instructies](https://docs.mongodb.com/manual/administration/install-on-linux/) voor Linux-distributies met inbegrip van Red Hat / CentOS, SUSE, Ubuntu en Debian.</span><span class="sxs-lookup"><span data-stu-id="a27df-115">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="a27df-116">Hallo volgende voorbeeld wordt een *CentOS* VM die gebruikmaakt van een SSH-sleutel die is opgeslagen op *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="a27df-116">hello following example creates a *CentOS* VM using an SSH key stored at *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="a27df-117">Antwoord Hallo vraagt om de naam van het opslagaccount, DNS-naam en -referenties:</span><span class="sxs-lookup"><span data-stu-id="a27df-117">Answer hello prompts for storage account name, DNS name, and admin credentials:</span></span>

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

<span data-ttu-id="a27df-118">Meld u aan toohello VM Hallo openbaar IP-adres weergegeven aan einde Hallo Hallo voorafgaand aan de virtuele machine maken stap met:</span><span class="sxs-lookup"><span data-stu-id="a27df-118">Log on toohello VM using hello public IP address displayed at hello end of hello preceding VM creation step:</span></span>

```bash
ssh azureuser@40.78.23.145
```

<span data-ttu-id="a27df-119">tooadd hello installatiebronnen voor MongoDB, maak een **yum** opslagplaatsbestand als volgt:</span><span class="sxs-lookup"><span data-stu-id="a27df-119">tooadd hello installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="a27df-120">Hallo MongoDB-repo-bestand voor het bewerken van openen.</span><span class="sxs-lookup"><span data-stu-id="a27df-120">Open hello MongoDB repo file for editing.</span></span> <span data-ttu-id="a27df-121">Hallo volgende regels toevoegen:</span><span class="sxs-lookup"><span data-stu-id="a27df-121">Add hello following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="a27df-122">Installeren met behulp van MongoDB **yum** als volgt:</span><span class="sxs-lookup"><span data-stu-id="a27df-122">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="a27df-123">SELinux wordt standaard afgedwongen voor installatiekopieën van CentOS die voorkomen dat u toegang tot MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a27df-123">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="a27df-124">Beheerhulpprogramma's voor installeren en SELinux tooallow MongoDB toooperate als volgt op de standaard TCP-poort 27017 configureren.</span><span class="sxs-lookup"><span data-stu-id="a27df-124">Install policy management tools and configure SELinux tooallow MongoDB toooperate on its default TCP port 27017 as follows.</span></span> 

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="a27df-125">Start Hallo MongoDB-service als volgt:</span><span class="sxs-lookup"><span data-stu-id="a27df-125">Start hello MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="a27df-126">Hallo MongoDB installatie controleren door verbinding te maken met behulp van de lokale Hallo `mongo` client:</span><span class="sxs-lookup"><span data-stu-id="a27df-126">Verify hello MongoDB installation by connecting using hello local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="a27df-127">Hallo MongoDB-exemplaar nu testen door een aantal gegevens toe te voegen en vervolgens te zoeken:</span><span class="sxs-lookup"><span data-stu-id="a27df-127">Now test hello MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="a27df-128">Indien gewenst, MongoDB toostart automatisch configureren tijdens opstarten:</span><span class="sxs-lookup"><span data-stu-id="a27df-128">If desired, configure MongoDB toostart automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="a27df-129">Basic MongoDB-exemplaar op CentOS met een sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="a27df-129">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="a27df-130">U kunt basic MongoDB-exemplaar maken op een enkele CentOS virtuele machine met behulp van hello Azure snelstartsjabloon met de volgende uit GitHub.</span><span class="sxs-lookup"><span data-stu-id="a27df-130">You can create a basic MongoDB instance on a single CentOS VM using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="a27df-131">Deze sjabloon maakt gebruik van Hallo aangepaste scriptextensie voor Linux tooadd een `yum` tooyour opslagplaats nieuw gemaakte CentOS VM en installeer vervolgens MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a27df-131">This template uses hello Custom Script extension for Linux tooadd a `yum` repository tooyour newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="a27df-132">[Basic MongoDB-exemplaar op CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="a27df-132">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="a27df-133">Hallo volgende voorbeeld wordt een resourcegroep met de naam van de Hallo `myResourceGroup` in Hallo `eastus` regio.</span><span class="sxs-lookup"><span data-stu-id="a27df-133">hello following example creates a resource group with hello name `myResourceGroup` in hello `eastus` region.</span></span> <span data-ttu-id="a27df-134">Voer uw eigen waarden als volgt:</span><span class="sxs-lookup"><span data-stu-id="a27df-134">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="a27df-135">Hello Azure CLI retourneert u tooa prompt binnen een paar seconden voor het maken van Hallo-implementatie, maar de Hallo-installatie en configuratie duurt een paar minuten toocomplete.</span><span class="sxs-lookup"><span data-stu-id="a27df-135">hello Azure CLI returns you tooa prompt within a few seconds of creating hello deployment, but hello installation and configuration takes a few minutes toocomplete.</span></span> <span data-ttu-id="a27df-136">Controleer de status van Hallo Hallo-implementatie met `azure group deployment show myResourceGroup`, Hallo-naam van de resourcegroep dienovereenkomstig in te voeren.</span><span class="sxs-lookup"><span data-stu-id="a27df-136">Check hello status of hello deployment with `azure group deployment show myResourceGroup`, entering hello name of your resource group accordingly.</span></span> <span data-ttu-id="a27df-137">Wachten tot Hallo **ProvisioningState** toont *geslaagd* voordat de poging tooSSH toohello VM.</span><span class="sxs-lookup"><span data-stu-id="a27df-137">Wait until hello **ProvisioningState** shows *Succeeded* before trying tooSSH toohello VM.</span></span>

<span data-ttu-id="a27df-138">Als de Hallo-implementatie is voltooid, SSH toohello VM.</span><span class="sxs-lookup"><span data-stu-id="a27df-138">Once hello deployment is complete, SSH toohello VM.</span></span> <span data-ttu-id="a27df-139">Hallo IP-adres van uw virtuele machine met behulp van Hallo `azure vm show` opdracht zoals Hallo volgt in:</span><span class="sxs-lookup"><span data-stu-id="a27df-139">Obtain hello IP address of your VM using hello `azure vm show` command as in hello following example:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

<span data-ttu-id="a27df-140">In de buurt Hallo einde van Hallo-uitvoer, wordt Hallo openbaar IP-adres weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a27df-140">Near hello end of hello output, hello public IP address is displayed.</span></span> <span data-ttu-id="a27df-141">SSH tooyour VM met Hallo IP-adres van uw virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="a27df-141">SSH tooyour VM with hello IP address of your VM:</span></span>

```bash
ssh azureuser@138.91.149.74
```

<span data-ttu-id="a27df-142">Hallo MongoDB installatie controleren door verbinding te maken met behulp van de lokale Hallo `mongo` client als volgt:</span><span class="sxs-lookup"><span data-stu-id="a27df-142">Verify hello MongoDB installation by connecting using hello local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="a27df-143">Test nu Hallo exemplaar sommige gegevens toe te voegen en zoek het als volgt:</span><span class="sxs-lookup"><span data-stu-id="a27df-143">Now test hello instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="a27df-144">Een complexe MongoDB Shard-Cluster op CentOS met een sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="a27df-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="a27df-145">U kunt een complexe MongoDB shard cluster met behulp van de volgende Azure quickstart-sjabloon uit GitHub Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="a27df-145">You can create a complex MongoDB sharded cluster using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="a27df-146">Deze sjabloon volgt Hallo [MongoDB shard cluster aanbevolen procedures](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundantie en hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="a27df-146">This template follows hello [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancy and high availability.</span></span> <span data-ttu-id="a27df-147">Hallo-sjabloon maakt twee shards met drie knooppunten replicaset.</span><span class="sxs-lookup"><span data-stu-id="a27df-147">hello template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="a27df-148">Een config server replicaset met drie knooppunten ook wordt gemaakt, plus twee **mongos** router servers tooprovide consistentie tooapplications uit via Hallo shards.</span><span class="sxs-lookup"><span data-stu-id="a27df-148">One config server replica set with three nodes is also created, plus two **mongos** router servers tooprovide consistency tooapplications from across hello shards.</span></span>

* <span data-ttu-id="a27df-149">[MongoDB Sharding-Cluster op CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="a27df-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="a27df-150">Dit complexe MongoDB shard-cluster implementeren vereist meer dan 20 cores die meestal Hallo standaard core-telling per regio voor een abonnement.</span><span class="sxs-lookup"><span data-stu-id="a27df-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically hello default core count per region for a subscription.</span></span> <span data-ttu-id="a27df-151">Open een Azure ondersteuningsverzoek tooincrease core-telling.</span><span class="sxs-lookup"><span data-stu-id="a27df-151">Open an Azure support request tooincrease your core count.</span></span>

<span data-ttu-id="a27df-152">Hallo volgende voorbeeld wordt een resourcegroep met de naam van de Hallo *myResourceGroup* in Hallo *eastus* regio.</span><span class="sxs-lookup"><span data-stu-id="a27df-152">hello following example creates a resource group with hello name *myResourceGroup* in hello *eastus* region.</span></span> <span data-ttu-id="a27df-153">Voer uw eigen waarden als volgt:</span><span class="sxs-lookup"><span data-stu-id="a27df-153">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="a27df-154">Hello Azure CLI retourneert u tooa prompt binnen een paar seconden na het Hallo-implementatie wordt gemaakt, maar hello installatie en configuratie overnemen een toocomplete uur.</span><span class="sxs-lookup"><span data-stu-id="a27df-154">hello Azure CLI returns you tooa prompt within a few seconds of creating hello deployment, but hello installation and configuration can take over an hour toocomplete.</span></span> <span data-ttu-id="a27df-155">Controleer de status van Hallo Hallo-implementatie met `azure group deployment show myResourceGroup`, het Hallo-naam van de resourcegroep dienovereenkomstig aanpassen.</span><span class="sxs-lookup"><span data-stu-id="a27df-155">Check hello status of hello deployment with `azure group deployment show myResourceGroup`, adjusting hello name of your resource group accordingly.</span></span> <span data-ttu-id="a27df-156">Wachten tot Hallo **ProvisioningState** toont *geslaagd* voordat VMs toohello verbinding wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a27df-156">Wait until hello **ProvisioningState** shows *Succeeded* before connecting toohello VMs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a27df-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a27df-157">Next steps</span></span>
<span data-ttu-id="a27df-158">In deze voorbeelden u lokaal verbinding maken met toohello MongoDB-exemplaar van Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="a27df-158">In these examples, you connect toohello MongoDB instance locally from hello VM.</span></span> <span data-ttu-id="a27df-159">Als u tooconnect toohello MongoDB-exemplaar van een andere virtuele machine of een netwerk wilt, zorg ervoor dat de juiste Hallo [Netwerkbeveiligingsgroep regels zijn gemaakt](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="a27df-159">If you want tooconnect toohello MongoDB instance from another VM or network, ensure hello appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="a27df-160">Zie voor meer informatie over het maken van sjablonen Hallo [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a27df-160">For more information about creating using templates, see hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="a27df-161">Hello Azure Resource Manager-sjablonen gebruiken Hallo aangepaste Scriptextensie toodownload en scripts uitvoeren op uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="a27df-161">hello Azure Resource Manager templates use hello Custom Script Extension toodownload and execute scripts on your VMs.</span></span> <span data-ttu-id="a27df-162">Zie voor meer informatie [Using hello Azure aangepaste Scriptextensie met virtuele Linux-Machines](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="a27df-162">For more information, see [Using hello Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

