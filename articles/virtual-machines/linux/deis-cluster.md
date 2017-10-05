---
title: Implementeren van een 3-node cluster Deis | Microsoft Docs
description: In dit artikel wordt beschreven hoe u een 3-node cluster in Azure met een Azure Resource Manager-sjabloon Deis
services: virtual-machines-linux
documentationcenter: 
author: HaishiBai
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9a0c3dd7562dfb5ce54c2ebfd4665109f59cd8fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a><span data-ttu-id="a4fe1-103">Implementeren en configureren van een 3-node cluster in Azure Deis</span><span class="sxs-lookup"><span data-stu-id="a4fe1-103">Deploy and configure a 3-node Deis cluster in Azure</span></span>
<span data-ttu-id="a4fe1-104">Dit artikel begeleidt u bij het inrichten van een [Deis](http://deis.io/) cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-104">This article walks you through provisioning a [Deis](http://deis.io/) cluster on Azure.</span></span> <span data-ttu-id="a4fe1-105">Dit omvat alle stappen van het maken van de benodigde certificaten te implementeren en schalen van een steekproef **gaat** toepassing op het nieuw ingerichte cluster.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-105">It covers all the steps from creating the necessary certificates to deploying and scaling a sample **Go** application on the newly provisioned cluster.</span></span>

<span data-ttu-id="a4fe1-106">Het volgende diagram toont de architectuur van het geïmplementeerde systeem.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-106">The following diagram shows the architecture of the deployed system.</span></span> <span data-ttu-id="a4fe1-107">Een systeembeheerder beheert het cluster met behulp van hulpprogramma's zoals Deis **deis** en **deisctl**.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-107">A system administrator manages the cluster using Deis tools such as **deis** and **deisctl**.</span></span> <span data-ttu-id="a4fe1-108">Verbindingen worden tot stand gebracht via een Azure load balancer, die de verbindingen naar een van de lid-knooppunten op het cluster doorstuurt.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-108">Connections are established through an Azure load balancer, which forwards the connections to one of the member nodes on the cluster.</span></span> <span data-ttu-id="a4fe1-109">De toegang van clients geïmplementeerde toepassingen via de load balancer.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-109">The clients access deployed applications through the load balancer as well.</span></span> <span data-ttu-id="a4fe1-110">In dit geval wordt de load balancer stuurt het verkeer naar een Deis router mesh, die verdere routs verkeer naar de bijbehorende Docker-containers die worden gehost op het cluster.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-110">In this case, the load balancer forwards the traffic to a Deis router mesh, which further routs traffic to corresponding Docker containers hosted on the cluster.</span></span>

  ![Architectuurdiagram van geïmplementeerde Desis cluster](./media/deis-cluster/architecture-overview.png)

<span data-ttu-id="a4fe1-112">De volgende stappen uitvoeren, hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-112">In order to run through the following steps, you'll need:</span></span>

* <span data-ttu-id="a4fe1-113">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-113">An active Azure subscription.</span></span> <span data-ttu-id="a4fe1-114">Als u niet hebt, kunt u een gratis spoor krijgen op [azure.com](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="a4fe1-114">If you don't have one, you can get a free trail on [azure.com](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="a4fe1-115">Een werk- of schoolaccount-id te gebruiken van Azure-resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-115">A work or school id to use Azure resource groups.</span></span> <span data-ttu-id="a4fe1-116">Als u een persoonlijk account en meld u aan met een Microsoft-id hebt, moet u [maken van een werk-id van uw persoonlijke](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a4fe1-116">If you have a personal account and log in with a Microsoft id, you need to [create a work id from your personal one](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="a4fe1-117">Een--afhankelijk van uw clientbesturingssysteem--de [Azure PowerShell](/powershell/azureps-cmdlets-docs) of de [Azure CLI voor Mac, Linux en Windows](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a4fe1-117">Either -- depending on your client operating system -- the [Azure PowerShell](/powershell/azureps-cmdlets-docs) or the [Azure CLI for Mac, Linux, and Windows](../../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="a4fe1-118">[OpenSSL](https://www.openssl.org/).</span><span class="sxs-lookup"><span data-stu-id="a4fe1-118">[OpenSSL](https://www.openssl.org/).</span></span> <span data-ttu-id="a4fe1-119">OpenSSL wordt gebruikt voor het genereren van de benodigde certificaten.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-119">OpenSSL is used to generate the necessary certificates.</span></span>
* <span data-ttu-id="a4fe1-120">Een client Git zoals [Git Bash](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="a4fe1-120">A Git client such as [Git Bash](https://git-scm.com/).</span></span>
* <span data-ttu-id="a4fe1-121">Als u wilt testen van de voorbeeldtoepassing, hebt u ook een DNS-server nodig.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-121">To test the sample application, you'll also need a DNS server.</span></span> <span data-ttu-id="a4fe1-122">U kunt alle DNS-servers of services die ondersteuning bieden voor de A-records jokertekens gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-122">You can use any DNS servers or services that support wildcard A records.</span></span>
* <span data-ttu-id="a4fe1-123">Een computer om uit te voeren Deis clienthulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-123">A computer to run Deis client tools.</span></span> <span data-ttu-id="a4fe1-124">U kunt een lokale computer of een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-124">You can use either a local machine or a virtual machine.</span></span> <span data-ttu-id="a4fe1-125">U kunt deze hulpprogramma's uitvoeren op bijna elke Linux-distributie, maar de volgende instructies Ubuntu gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-125">You can run these tools on almost any Linux distribution, but the following instructions use Ubuntu.</span></span>

## <a name="provision-the-cluster"></a><span data-ttu-id="a4fe1-126">Het cluster inrichten</span><span class="sxs-lookup"><span data-stu-id="a4fe1-126">Provision the cluster</span></span>
<span data-ttu-id="a4fe1-127">In deze sectie maakt u een [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) sjabloon uit de opslagplaats voor open-source [azure-snelstartsjablonen](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="a4fe1-127">In this section, you'll use an [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) template from the open source repository [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="a4fe1-128">U moet eerst kopiëren omlaag in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-128">First, you'll copy down the template.</span></span> <span data-ttu-id="a4fe1-129">Vervolgens maakt u een nieuwe SSH-sleutelpaar voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-129">Then, you'll create a new SSH key pair for authentication.</span></span> <span data-ttu-id="a4fe1-130">En vervolgens configureert u een nieuwe id voor u cluster.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-130">And then, you'll configure a new identifier for you cluster.</span></span> <span data-ttu-id="a4fe1-131">En ten slotte wordt vervolgens gebruikt u de Shell-script of het PowerShell-script voor het inrichten van het cluster.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-131">And finally, you'll use either the Shell script or the PowerShell script to provision the cluster.</span></span>

1. <span data-ttu-id="a4fe1-132">Kloon de opslagplaats: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="a4fe1-132">Clone the repository: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. <span data-ttu-id="a4fe1-133">Ga naar de sjabloonmap:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-133">Go to the template folder:</span></span>
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. <span data-ttu-id="a4fe1-134">Maak een nieuwe SSH-sleutelpaar ssh-keygen gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-134">Create a new SSH key pair using ssh-keygen:</span></span>
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. <span data-ttu-id="a4fe1-135">Een certificaat met de bovenstaande persoonlijke sleutel genereren:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-135">Generate a certificate using the above private key:</span></span>
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file to be generated]
5. <span data-ttu-id="a4fe1-136">Ga naar [https://discovery.etcd.io/new](https://discovery.etcd.io/new) voor het genereren van een nieuw cluster token ziet eruit als:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-136">Go to [https://discovery.etcd.io/new](https://discovery.etcd.io/new) to generate a new cluster token, which looks something like:</span></span>
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   <span data-ttu-id="a4fe1-137">Elke virtuele CoreOS-cluster moet een unieke token van deze gratis service hebben.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-137">Each CoreOS cluster needs to have a unique token from this free service.</span></span> <span data-ttu-id="a4fe1-138">Zie [virtuele CoreOS documentatie](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-138">Please see [CoreOS documentation](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) for more details.</span></span>
6. <span data-ttu-id="a4fe1-139">Wijzig de **cloud config.yaml** bestand vervangt de bestaande **detectie** token met het nieuwe token:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-139">Modify the **cloud-config.yaml** file to replace the existing  **discovery** token with the new token:</span></span>
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment the following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. <span data-ttu-id="a4fe1-140">Wijzig de **azuredeploy-parameters.json** bestand: het certificaat dat u hebt gemaakt in stap 4 in een teksteditor openen.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-140">Modify the **azuredeploy-parameters.json** file: Open the certificate you created in step 4 in a text editor.</span></span> <span data-ttu-id="a4fe1-141">Kopieer alle tekst tussen `----BEGIN CERTIFICATE-----` en `-----END CERTIFICATE-----` in de **sshKeyData** parameter (moet u alle newline-tekens te verwijderen).</span><span class="sxs-lookup"><span data-stu-id="a4fe1-141">Copy all text between `----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` into the **sshKeyData** parameter (you'll need to remove all newline characters).</span></span>
8. <span data-ttu-id="a4fe1-142">Wijzig de **newStorageAccountName** parameter.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-142">Modify the **newStorageAccountName** parameter.</span></span> <span data-ttu-id="a4fe1-143">Dit is het opslagaccount voor VM-OS-schijven.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-143">This is the storage account for VM OS disks.</span></span> <span data-ttu-id="a4fe1-144">De accountnaam moet globaal uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-144">This account name has to be globally unique.</span></span>
9. <span data-ttu-id="a4fe1-145">Wijzig de **publicDomainName** parameter.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-145">Modify the **publicDomainName** parameter.</span></span> <span data-ttu-id="a4fe1-146">Dit wordt een onderdeel van de DNS-naam die is gekoppeld aan de load balancer openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-146">This will become part of the DNS name associated with the load balancer public IP.</span></span> <span data-ttu-id="a4fe1-147">De laatste FQDN hebben de indeling van *[waarde van deze parameter]*. *[regio]* . cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-147">The final FQDN will have the format of *[value of this parameter]*.*[region]*.cloudapp.azure.com.</span></span> <span data-ttu-id="a4fe1-148">Bijvoorbeeld, als u de naam als deishbai32 opgeven en de resourcegroep wordt geïmplementeerd voor de regio VS-West, klikt u vervolgens de uiteindelijke FQDN-naam voor de load balancer worden deishbai32.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-148">For example, if you specify the name as deishbai32, and the resource group is deployed to the West US region, then the final FQDN to your load balancer will be deishbai32.westus.cloudapp.azure.com.</span></span>
10. <span data-ttu-id="a4fe1-149">Sla het parameterbestand.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-149">Save the parameter file.</span></span> <span data-ttu-id="a4fe1-150">En vervolgens inrichten van het cluster met Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-150">And then you can provision the cluster using Azure PowerShell:</span></span>
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    <span data-ttu-id="a4fe1-151">of Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-151">or Azure CLI:</span></span>
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. <span data-ttu-id="a4fe1-152">Zodra de resourcegroep is geconfigureerd, ziet u alle resources in de groep naar de klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-152">Once the resource group is provisioned, you can see all the resources in the group on Azure classic portal.</span></span> <span data-ttu-id="a4fe1-153">Zoals u in de volgende schermafbeelding ziet, bevat de resourcegroep een virtueel netwerk met drie virtuele machines die zijn gekoppeld aan dezelfde beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-153">As shown in the following screenshot, the resource group contains a virtual network with three VMs, which are joined to the same availability set.</span></span> <span data-ttu-id="a4fe1-154">De groep bevat ook een load balancer met een bijbehorende openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-154">The group also contains a load balancer, which has an associated public IP.</span></span>
    
    ![De ingerichte resourcegroep in de klassieke Azure-portal](./media/deis-cluster/resource-group.png)

## <a name="install-the-client"></a><span data-ttu-id="a4fe1-156">De client installeren</span><span class="sxs-lookup"><span data-stu-id="a4fe1-156">Install the client</span></span>
<span data-ttu-id="a4fe1-157">U moet **deisctl** om te bepalen uw cluster Deis.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-157">You need **deisctl** to control your Deis cluster.</span></span> <span data-ttu-id="a4fe1-158">Hoewel deisctl automatisch op alle clusterknooppunten is geïnstalleerd, is het raadzaam deisctl gebruiken op een afzonderlijke administratieve machine.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-158">Although deisctl is automatically installed in all the cluster nodes, it's a good practice to use deisctl on a separate administrative machine.</span></span> <span data-ttu-id="a4fe1-159">Bovendien, omdat alle knooppunten zijn geconfigureerd met alleen persoonlijke IP-adressen, moet u SSH-tunneling via de load balancer met een openbare IP-adres om verbinding met de knooppunt-machines te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-159">Furthermore, because all nodes are configured with only private IP addresses, you'll need to use SSH tunneling through the load balancer, which has a public IP, to connect to the node machines.</span></span> <span data-ttu-id="a4fe1-160">Hier volgen de stappen voor het instellen van deisctl op een afzonderlijke Ubuntu fysieke of virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-160">The following are the steps of setting up deisctl on a separate Ubuntu physical or virtual machine.</span></span>

1. <span data-ttu-id="a4fe1-161">Installatie deisctl:mkdir deis</span><span class="sxs-lookup"><span data-stu-id="a4fe1-161">Install deisctl:mkdir deis</span></span>
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. <span data-ttu-id="a4fe1-162">Uw persoonlijke sleutel voor ssh-agent toevoegen:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-162">Add your private key to ssh agent:</span></span>
   
        eval `ssh-agent -s`
        ssh-add [path to the private key file, see step 1 in the previous section]
3. <span data-ttu-id="a4fe1-163">Deisctl configureren:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-163">Configure deisctl:</span></span>
   
        export DEISCTL_TUNNEL=[public ip of the load balancer]:2223

<span data-ttu-id="a4fe1-164">De sjabloon definieert inkomende NAT-regels die zijn toegewezen 2223 waarvan u een exemplaar van 1, 2224 met exemplaar 2 en 2225 met 3-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-164">The template defines inbound NAT rules that map 2223 to instance 1, 2224 to instance 2, and 2225 to instance 3.</span></span> <span data-ttu-id="a4fe1-165">Dit biedt redundantie voor het gebruik van het hulpprogramma deisctl.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-165">This provides redundancy for using the deisctl tool.</span></span> <span data-ttu-id="a4fe1-166">U kunt deze regels in de klassieke Azure-portal bekijken:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-166">You can examine these rules on Azure classic portal:</span></span>

![NAT-regels op de load balancer](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> <span data-ttu-id="a4fe1-168">De sjabloon ondersteunt momenteel alleen clusters 3-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-168">Currently the template only supports 3-node clusters.</span></span> <span data-ttu-id="a4fe1-169">Dit is vanwege een beperking in Azure Resource Manager-sjabloon NAT regeldefinitie, die de syntaxis van de lus niet ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-169">This is because of a limitation in Azure Resource Manager template NAT rule definition, which doesn’t support loop syntax.</span></span>
> 
> 

## <a name="install-and-start-the-deis-platform"></a><span data-ttu-id="a4fe1-170">Installeer en start de Deis platform</span><span class="sxs-lookup"><span data-stu-id="a4fe1-170">Install and start the Deis platform</span></span>
<span data-ttu-id="a4fe1-171">Nu kunt u deisctl installeren en start de Deis platform:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-171">Now you can use deisctl to install and start the Deis platform:</span></span>

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path to the private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> <span data-ttu-id="a4fe1-172">Starten van het platform even duurt voordat (zo veel 10 minuten).</span><span class="sxs-lookup"><span data-stu-id="a4fe1-172">Starting the platform takes a while (as much as 10 minutes).</span></span> <span data-ttu-id="a4fe1-173">Met name, kan starten van de opbouwfunctie voor service erg lang duren.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-173">Especially, starting the builder service can take a long time.</span></span> <span data-ttu-id="a4fe1-174">En soms duurt een paar probeert te slagen: als de bewerking lijkt vastlopen, kunt u `ctrl+c` opsplitsen uitvoeren van de opdracht en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-174">And sometimes it takes a few tries to succeed: If the operation seems to hang, try typing `ctrl+c` to break execution of the command and retry.</span></span>
> 
> 

<span data-ttu-id="a4fe1-175">U kunt `deisctl list` om te controleren of alle services worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-175">You can use `deisctl list` to verify if all services are running:</span></span>

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

<span data-ttu-id="a4fe1-176">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-176">Congratulations!</span></span> <span data-ttu-id="a4fe1-177">Nu u een actieve hebt Deis clsuter op Azure!</span><span class="sxs-lookup"><span data-stu-id="a4fe1-177">Now you've got a running Deis clsuter on Azure!</span></span> <span data-ttu-id="a4fe1-178">Vervolgens laten we implementeert u een toepassing Ga om te zien van het cluster in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-178">Next, let's deploy a sample Go application to see the cluster in action.</span></span>

## <a name="deploy-and-scale-a-hello-world-application"></a><span data-ttu-id="a4fe1-179">Implementeren en schalen van een toepassing Hello World</span><span class="sxs-lookup"><span data-stu-id="a4fe1-179">Deploy and scale a Hello World application</span></span>
<span data-ttu-id="a4fe1-180">De volgende stappen ziet u het implementeren van een 'Hallo wereld' gaat de toepassing aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-180">The following steps show how to deploy a "Hello World" Go application to the cluster.</span></span> <span data-ttu-id="a4fe1-181">De stappen zijn gebaseerd op [Deis documentatie](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span><span class="sxs-lookup"><span data-stu-id="a4fe1-181">The steps are based on [Deis documentation](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span></span>

1. <span data-ttu-id="a4fe1-182">Voor de routering mesh goed te laten werken, moet u een jokerteken A-record voor uw domein die verwijst naar het openbare IP-adres van de load balancer hebben.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-182">For the routing mesh to work properly, you’ll need to have a wildcard A record for your domain pointing to the public IP of the load balancer.</span></span> <span data-ttu-id="a4fe1-183">De volgende schermafbeelding ziet u de A-record voor een voorbeeld-domeinregistratie op GoDaddy:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-183">The following screenshot shows the A record for a sample domain registration on GoDaddy:</span></span>
   
    ![Godaddy-A-record](./media/deis-cluster/go-daddy.png)
   
   <p />
2. <span data-ttu-id="a4fe1-185">Installatie deis:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-185">Install deis:</span></span>
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. <span data-ttu-id="a4fe1-186">Maak een nieuwe SSH-sleutel en voeg vervolgens de openbare sleutel met GitHub (natuurlijk kunt u ook hergebruiken uw bestaande sleutels).</span><span class="sxs-lookup"><span data-stu-id="a4fe1-186">Create a new SSH key, and then add the public key to GitHub (of course, you can also reuse your existing keys).</span></span> <span data-ttu-id="a4fe1-187">Voor het maken van een nieuw sleutelpaar van de SSH-sleutel gebruikt:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-187">To create a new SSH key pair, use:</span></span>
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s to use default file names and empty passcode)
4. <span data-ttu-id="a4fe1-188">Id_rsa.pub of de openbare sleutel van uw keuze toevoegen met GitHub.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-188">Add id_rsa.pub, or the public key of your choice, to GitHub.</span></span> <span data-ttu-id="a4fe1-189">U kunt dit doen met behulp van de sleutel toevoegen SSH-knop in het scherm van de SSH-sleutels configuratie:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-189">You can do this by using the Add SSH key button in your SSH keys configuration screen:</span></span>
   
   ![GitHub-sleutel](./media/deis-cluster/github-key.png)
   
   <p />
5. <span data-ttu-id="a4fe1-191">Een nieuwe gebruiker registreren:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-191">Register a new user:</span></span>
   
        deis register http://deis.[your domain]
   <p />
6. <span data-ttu-id="a4fe1-192">De SSH-sleutel toevoegen:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-192">Add the SSH key:</span></span>
   
        deis keys:add [path to your SSH public key]
   <p />      
7. <span data-ttu-id="a4fe1-193">Een toepassing maken.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-193">Create an application.</span></span>
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p /><span data-ttu-id="a4fe1-194">
8.De git push activeren Docker-installatiekopieën worden gemaakt en geïmplementeerd, duurt enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-194">
8. The git push will trigger Docker images to be built and deployed, which will take a few minutes.</span></span> <span data-ttu-id="a4fe1-195">Mijn ervaring van soms vastlopen stap 10 (Pushing installatiekopie naar de opslagplaats voor persoonlijke).</span><span class="sxs-lookup"><span data-stu-id="a4fe1-195">From my experience, occasionally, Step 10 (Pushing image to private repository) may hang.</span></span> <span data-ttu-id="a4fe1-196">Als dit gebeurt, kunt u het proces beëindigen, verwijdert u de toepassing met behulp van ' deis apps: vernietigen – a <application name> ` to remove the application and try again. You can use `deis apps:list' om erachter te komen met de naam van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-196">When this happens, you can stop the process, remove the application using `deis apps:destroy –a <application name>` to remove the application and try again. You can use `deis apps:list` to find out the name of your application.</span></span> <span data-ttu-id="a4fe1-197">Als alles werkt, moet er ongeveer als volgt aan het einde van de uitvoer van de opdracht:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-197">If everything works out, you should see something like the following at the end of command outputs:</span></span>
   
        -----> Launching...
               done, lambda-underdog:v2 deployed to Deis
               http://lambda-underdog.artitrack.com
               To learn more, use `deis help` or visit http://deis.io
        To ssh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. <span data-ttu-id="a4fe1-198">Controleer of de toepassing werkt:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-198">Verify if the application is working:</span></span>
   
        curl -S http://[your application name].[your domain]
   <span data-ttu-id="a4fe1-199">U ziet het volgende:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-199">You should see:</span></span>
   
        Welcome to Deis!
        See the documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list to get the name of your application).
   <p />
10. <span data-ttu-id="a4fe1-200">Schaal de toepassing naar 3 exemplaren:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-200">Scale the application to 3 instances:</span></span>
    
        deis scale cmd=3
    <p />
11. <span data-ttu-id="a4fe1-201">Desgewenst kunt u deis info om te controleren van de details van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-201">Optionally, you can use deis info to examine details of your application.</span></span> <span data-ttu-id="a4fe1-202">De volgende uitvoer zijn van de implementatie van mijn toepassingen:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-202">The following outputs are from my application deployment:</span></span>
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a><span data-ttu-id="a4fe1-203">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a4fe1-203">Next Steps</span></span>
<span data-ttu-id="a4fe1-204">In dit artikel gelopen u stapsgewijs door de procedure voor het inrichten van een nieuw cluster in Azure met een Azure Resource Manager-sjabloon Deis.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-204">This article walked you through all the steps to provision a new Deis cluster on Azure using an Azure Resource Manager template.</span></span> <span data-ttu-id="a4fe1-205">De sjabloon ondersteunt redundantie in tooling verbindingen, evenals taakverdeling voor geïmplementeerde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-205">The template supports redundancy in tooling connections as well as load balancing for deployed applications.</span></span> <span data-ttu-id="a4fe1-206">De sjabloon ook voorkomt met behulp van openbare IP-adressen op lid-knooppunten, bespaart kostbare openbare IP-netwerkbronnen en biedt een beter beveiligde omgeving host voor toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a4fe1-206">The template also avoids using public IPs on member nodes, which saves precious public IP resources and provides a more secured environment to host applications.</span></span> <span data-ttu-id="a4fe1-207">Zie voor meer informatie de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="a4fe1-207">To learn more, see the following articles:</span></span>

<span data-ttu-id="a4fe1-208">[Overzicht van Azure Resource Manager][resource-group-overview]</span><span class="sxs-lookup"><span data-stu-id="a4fe1-208">[Azure Resource Manager Overview][resource-group-overview]</span></span>  
<span data-ttu-id="a4fe1-209">[Het gebruik van de Azure CLI][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="a4fe1-209">[How to use the Azure CLI][azure-command-line-tools]</span></span>  
<span data-ttu-id="a4fe1-210">[Azure PowerShell gebruiken met Azure Resource Manager][powershell-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="a4fe1-210">[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager]</span></span>  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
