---
title: MongoDB installeren op een Linux-VM met behulp van de Azure CLI 1.0 | Microsoft Docs
description: Informatie over het installeren en configureren van MongoDB op een virtuele Linux-machine in Azure met behulp van het Resource Manager-implementatiemodel.
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
ms.openlocfilehash: c97ade0a3d95824f723aad55776de861fe49441f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-mongodb-on-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="91de1-103">Het installeren en configureren van MongoDB op een Linux-VM met behulp van de Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="91de1-103">How to install and configure MongoDB on a Linux VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="91de1-104">[MongoDB](http://www.mongodb.org) is een populaire open-source, hoogwaardige NoSQL-database.</span><span class="sxs-lookup"><span data-stu-id="91de1-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="91de1-105">In dit artikel leest u hoe installeren en configureren van MongoDB op een Linux VM in Azure met het implementatiemodel van Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="91de1-105">This article shows you how to install and configure MongoDB on a Linux VM in Azure using the Resource Manager deployment model.</span></span> <span data-ttu-id="91de1-106">Voorbeelden worden weergegeven dat detail hoe naar:</span><span class="sxs-lookup"><span data-stu-id="91de1-106">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="91de1-107">Handmatig installeren en configureren van een eenvoudige MongoDB-exemplaar</span><span class="sxs-lookup"><span data-stu-id="91de1-107">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="91de1-108">Een basic MongoDB-exemplaar met een Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="91de1-108">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="91de1-109">Een complexe MongoDB shard-cluster met de replica wordt ingesteld met een Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="91de1-109">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="91de1-110">CLI-versies om de taak uit te voeren</span><span class="sxs-lookup"><span data-stu-id="91de1-110">CLI versions to complete the task</span></span>
<span data-ttu-id="91de1-111">U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:</span><span class="sxs-lookup"><span data-stu-id="91de1-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="91de1-112">Azure CLI 1.0: onze CLI voor het klassieke implementatiemodel en het Resource Manager-implementatiemodel (dit artikel)</span><span class="sxs-lookup"><span data-stu-id="91de1-112">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="91de1-113">[Azure CLI 2.0](create-cli-complete-nodejs.md): onze CLI van de volgende generatie voor het Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="91de1-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="91de1-114">Handmatig installeren en configureren van MongoDB op een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="91de1-114">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="91de1-115">MongoDB [installatie-instructies](https://docs.mongodb.com/manual/administration/install-on-linux/) voor Linux-distributies met inbegrip van Red Hat / CentOS, SUSE, Ubuntu en Debian.</span><span class="sxs-lookup"><span data-stu-id="91de1-115">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="91de1-116">Het volgende voorbeeld wordt een *CentOS* VM die gebruikmaakt van een SSH-sleutel die is opgeslagen op *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="91de1-116">The following example creates a *CentOS* VM using an SSH key stored at *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="91de1-117">Beantwoord de aanwijzingen voor de opslagaccountnaam, DNS-naam en beheerdersreferenties:</span><span class="sxs-lookup"><span data-stu-id="91de1-117">Answer the prompts for storage account name, DNS name, and admin credentials:</span></span>

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

<span data-ttu-id="91de1-118">Aanmelden bij de virtuele machine met behulp van het openbare IP-adres weergegeven aan het einde van de vorige stap van de VM-maken:</span><span class="sxs-lookup"><span data-stu-id="91de1-118">Log on to the VM using the public IP address displayed at the end of the preceding VM creation step:</span></span>

```bash
ssh azureuser@40.78.23.145
```

<span data-ttu-id="91de1-119">Voor het toevoegen van de installatiebronnen voor MongoDB, maken een **yum** opslagplaatsbestand als volgt:</span><span class="sxs-lookup"><span data-stu-id="91de1-119">To add the installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="91de1-120">Open het bestand van de opslagplaats MongoDB om te bewerken.</span><span class="sxs-lookup"><span data-stu-id="91de1-120">Open the MongoDB repo file for editing.</span></span> <span data-ttu-id="91de1-121">Voeg de volgende regels:</span><span class="sxs-lookup"><span data-stu-id="91de1-121">Add the following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="91de1-122">Installeren met behulp van MongoDB **yum** als volgt:</span><span class="sxs-lookup"><span data-stu-id="91de1-122">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="91de1-123">SELinux wordt standaard afgedwongen voor installatiekopieën van CentOS die voorkomen dat u toegang tot MongoDB.</span><span class="sxs-lookup"><span data-stu-id="91de1-123">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="91de1-124">Beheerhulpprogramma's voor installeren en configureren van SELinux zodat MongoDB bewerkingen uitvoeren op de standaard TCP-poort 27017 als volgt.</span><span class="sxs-lookup"><span data-stu-id="91de1-124">Install policy management tools and configure SELinux to allow MongoDB to operate on its default TCP port 27017 as follows.</span></span> 

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="91de1-125">Start de MongoDB-service als volgt:</span><span class="sxs-lookup"><span data-stu-id="91de1-125">Start the MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="91de1-126">De MongoDB-installatie controleren door verbinding te maken met behulp van de lokale `mongo` client:</span><span class="sxs-lookup"><span data-stu-id="91de1-126">Verify the MongoDB installation by connecting using the local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="91de1-127">Test de MongoDB-exemplaar nu door sommige gegevens toe te voegen en vervolgens te zoeken:</span><span class="sxs-lookup"><span data-stu-id="91de1-127">Now test the MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="91de1-128">Indien gewenst, configureert u MongoDB op automatisch starten tijdens het systeem opnieuw is opgestart:</span><span class="sxs-lookup"><span data-stu-id="91de1-128">If desired, configure MongoDB to start automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="91de1-129">Basic MongoDB-exemplaar op CentOS met een sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="91de1-129">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="91de1-130">U kunt een basic MongoDB-exemplaar maken op één CentOS VM van de volgende Azure quickstart-sjabloon vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="91de1-130">You can create a basic MongoDB instance on a single CentOS VM using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="91de1-131">Deze sjabloon wordt de aangepaste scriptextensie voor Linux toe te voegen een `yum` opslagplaats naar de zojuist gemaakte CentOS VM en installeer MongoDB.</span><span class="sxs-lookup"><span data-stu-id="91de1-131">This template uses the Custom Script extension for Linux to add a `yum` repository to your newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="91de1-132">[Basic MongoDB-exemplaar op CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="91de1-132">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="91de1-133">Het volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in de `eastus` regio.</span><span class="sxs-lookup"><span data-stu-id="91de1-133">The following example creates a resource group with the name `myResourceGroup` in the `eastus` region.</span></span> <span data-ttu-id="91de1-134">Voer uw eigen waarden als volgt:</span><span class="sxs-lookup"><span data-stu-id="91de1-134">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="91de1-135">De Azure CLI keert u terug naar een prompt binnen een paar seconden van de implementatie wordt gemaakt, maar de installatie en configuratie duurt een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="91de1-135">The Azure CLI returns you to a prompt within a few seconds of creating the deployment, but the installation and configuration takes a few minutes to complete.</span></span> <span data-ttu-id="91de1-136">Controleer de status van de implementatie met de `azure group deployment show myResourceGroup`, de naam van de resourcegroep dienovereenkomstig in te voeren.</span><span class="sxs-lookup"><span data-stu-id="91de1-136">Check the status of the deployment with `azure group deployment show myResourceGroup`, entering the name of your resource group accordingly.</span></span> <span data-ttu-id="91de1-137">Wacht totdat de **ProvisioningState** toont *geslaagd* voordat u probeert te SSH naar de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="91de1-137">Wait until the **ProvisioningState** shows *Succeeded* before trying to SSH to the VM.</span></span>

<span data-ttu-id="91de1-138">Zodra de implementatie voltooid, SSH naar de virtuele machine is.</span><span class="sxs-lookup"><span data-stu-id="91de1-138">Once the deployment is complete, SSH to the VM.</span></span> <span data-ttu-id="91de1-139">Het IP-adres van uw virtuele machine met de `azure vm show` opdracht zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="91de1-139">Obtain the IP address of your VM using the `azure vm show` command as in the following example:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

<span data-ttu-id="91de1-140">Het openbare IP-adres wordt aan het einde van de uitvoer weergegeven.</span><span class="sxs-lookup"><span data-stu-id="91de1-140">Near the end of the output, the public IP address is displayed.</span></span> <span data-ttu-id="91de1-141">SSH met uw virtuele machine met het IP-adres van uw virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="91de1-141">SSH to your VM with the IP address of your VM:</span></span>

```bash
ssh azureuser@138.91.149.74
```

<span data-ttu-id="91de1-142">De MongoDB-installatie controleren door verbinding te maken met behulp van de lokale `mongo` client als volgt:</span><span class="sxs-lookup"><span data-stu-id="91de1-142">Verify the MongoDB installation by connecting using the local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="91de1-143">Test nu het exemplaar door sommige gegevens toe te voegen en te zoeken als volgt:</span><span class="sxs-lookup"><span data-stu-id="91de1-143">Now test the instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="91de1-144">Een complexe MongoDB Shard-Cluster op CentOS met een sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="91de1-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="91de1-145">U kunt een complexe MongoDB shard cluster met behulp van de volgende Azure quickstart-sjabloon vanuit GitHub maken.</span><span class="sxs-lookup"><span data-stu-id="91de1-145">You can create a complex MongoDB sharded cluster using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="91de1-146">Deze sjabloon volgt de [MongoDB shard cluster aanbevolen procedures](https://docs.mongodb.com/manual/core/sharded-cluster-components/) voor redundantie en hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="91de1-146">This template follows the [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) to provide redundancy and high availability.</span></span> <span data-ttu-id="91de1-147">De sjabloon maakt twee shards met drie knooppunten replicaset.</span><span class="sxs-lookup"><span data-stu-id="91de1-147">The template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="91de1-148">Een config server replicaset met drie knooppunten ook wordt gemaakt, plus twee **mongos** router servers om te voorzien in consistentie van toepassingen uit de shards.</span><span class="sxs-lookup"><span data-stu-id="91de1-148">One config server replica set with three nodes is also created, plus two **mongos** router servers to provide consistency to applications from across the shards.</span></span>

* <span data-ttu-id="91de1-149">[MongoDB Sharding-Cluster op CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="91de1-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="91de1-150">Dit complexe MongoDB shard-cluster moet de implementatie meer dan 20 kernen, dit is doorgaans de standaardinstelling core-telling per regio voor een abonnement.</span><span class="sxs-lookup"><span data-stu-id="91de1-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically the default core count per region for a subscription.</span></span> <span data-ttu-id="91de1-151">Open een aanvraag voor ondersteuning van Azure te verhogen van het aantal kernen.</span><span class="sxs-lookup"><span data-stu-id="91de1-151">Open an Azure support request to increase your core count.</span></span>

<span data-ttu-id="91de1-152">Het volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in de *eastus* regio.</span><span class="sxs-lookup"><span data-stu-id="91de1-152">The following example creates a resource group with the name *myResourceGroup* in the *eastus* region.</span></span> <span data-ttu-id="91de1-153">Voer uw eigen waarden als volgt:</span><span class="sxs-lookup"><span data-stu-id="91de1-153">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="91de1-154">De Azure CLI keert u terug naar een prompt binnen een paar seconden van de implementatie wordt gemaakt, maar de installatie en configuratie kunnen ruim een uur duren voltooien.</span><span class="sxs-lookup"><span data-stu-id="91de1-154">The Azure CLI returns you to a prompt within a few seconds of creating the deployment, but the installation and configuration can take over an hour to complete.</span></span> <span data-ttu-id="91de1-155">Controleer de status van de implementatie met de `azure group deployment show myResourceGroup`, de naam van de resourcegroep dienovereenkomstig aanpassen.</span><span class="sxs-lookup"><span data-stu-id="91de1-155">Check the status of the deployment with `azure group deployment show myResourceGroup`, adjusting the name of your resource group accordingly.</span></span> <span data-ttu-id="91de1-156">Wacht totdat de **ProvisioningState** toont *geslaagd* voordat u verbinding maakt met de VM's.</span><span class="sxs-lookup"><span data-stu-id="91de1-156">Wait until the **ProvisioningState** shows *Succeeded* before connecting to the VMs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="91de1-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="91de1-157">Next steps</span></span>
<span data-ttu-id="91de1-158">In deze voorbeelden verbinding u met de MongoDB-exemplaar lokaal van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="91de1-158">In these examples, you connect to the MongoDB instance locally from the VM.</span></span> <span data-ttu-id="91de1-159">Als u wilt verbinding maken met de MongoDB-exemplaar van een andere virtuele machine of een netwerk, zorg ervoor dat de juiste [Netwerkbeveiligingsgroep regels zijn gemaakt](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="91de1-159">If you want to connect to the MongoDB instance from another VM or network, ensure the appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="91de1-160">Zie voor meer informatie over het maken van sjablonen gebruiken de [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="91de1-160">For more information about creating using templates, see the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="91de1-161">De Azure Resource Manager-sjablonen gebruiken de aangepaste Scriptextensie om te downloaden en uitvoeren van scripts op uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="91de1-161">The Azure Resource Manager templates use the Custom Script Extension to download and execute scripts on your VMs.</span></span> <span data-ttu-id="91de1-162">Zie voor meer informatie [met behulp van de Azure-extensie voor aangepaste scripts met virtuele Linux-Machines](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="91de1-162">For more information, see [Using the Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

