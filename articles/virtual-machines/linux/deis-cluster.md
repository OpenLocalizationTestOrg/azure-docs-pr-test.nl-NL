---
title: aaaDeploy Deis een 3-node cluster | Microsoft Docs
description: Dit artikel wordt beschreven hoe toocreate een 3-knooppunt Deis cluster in Azure met een Azure Resource Manager-sjabloon
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
ms.openlocfilehash: a4c0fb8cbb849264e64b433540157c9afecd184e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a><span data-ttu-id="f8c78-103">Implementeren en configureren van een 3-node cluster in Azure Deis</span><span class="sxs-lookup"><span data-stu-id="f8c78-103">Deploy and configure a 3-node Deis cluster in Azure</span></span>
<span data-ttu-id="f8c78-104">Dit artikel begeleidt u bij het inrichten van een [Deis](http://deis.io/) cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="f8c78-104">This article walks you through provisioning a [Deis](http://deis.io/) cluster on Azure.</span></span> <span data-ttu-id="f8c78-105">Dit omvat alle Hallo stappen van Hallo benodigde certificaten toodeploying maken en schalen van een steekproef **gaat** toepassing op nieuw ingerichte Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="f8c78-105">It covers all hello steps from creating hello necessary certificates toodeploying and scaling a sample **Go** application on hello newly provisioned cluster.</span></span>

<span data-ttu-id="f8c78-106">Hallo toont volgende diagram de architectuur Hallo van systeem Hallo geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f8c78-106">hello following diagram shows hello architecture of hello deployed system.</span></span> <span data-ttu-id="f8c78-107">Een systeembeheerder beheert Hallo cluster met behulp van hulpprogramma's zoals Deis **deis** en **deisctl**.</span><span class="sxs-lookup"><span data-stu-id="f8c78-107">A system administrator manages hello cluster using Deis tools such as **deis** and **deisctl**.</span></span> <span data-ttu-id="f8c78-108">Verbindingen worden tot stand gebracht via een Azure load balancer, die Hallo verbindingen tooone van Hallo lid knooppunten op Hallo-cluster doorstuurt.</span><span class="sxs-lookup"><span data-stu-id="f8c78-108">Connections are established through an Azure load balancer, which forwards hello connections tooone of hello member nodes on hello cluster.</span></span> <span data-ttu-id="f8c78-109">Hallo clients toegang geïmplementeerde toepassingen via ook Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="f8c78-109">hello clients access deployed applications through hello load balancer as well.</span></span> <span data-ttu-id="f8c78-110">In dit geval Hallo load balancer Hallo verkeer tooa stuurt Deis router mesh, die verdere routs verkeer toocorresponding Docker containers die worden gehost op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="f8c78-110">In this case, hello load balancer forwards hello traffic tooa Deis router mesh, which further routs traffic toocorresponding Docker containers hosted on hello cluster.</span></span>

  ![Architectuurdiagram van geïmplementeerde Desis cluster](./media/deis-cluster/architecture-overview.png)

<span data-ttu-id="f8c78-112">In de volgorde toorun via Hallo stappen te volgen, hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="f8c78-112">In order toorun through hello following steps, you'll need:</span></span>

* <span data-ttu-id="f8c78-113">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f8c78-113">An active Azure subscription.</span></span> <span data-ttu-id="f8c78-114">Als u niet hebt, kunt u een gratis spoor krijgen op [azure.com](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="f8c78-114">If you don't have one, you can get a free trail on [azure.com](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="f8c78-115">Een werk of school id toouse Azure-resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="f8c78-115">A work or school id toouse Azure resource groups.</span></span> <span data-ttu-id="f8c78-116">Als u een persoonlijk account en meld u aan met een Microsoft-id hebt, moet u deze te[maken van een werk-id van uw persoonlijke](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f8c78-116">If you have a personal account and log in with a Microsoft id, you need too[create a work id from your personal one](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="f8c78-117">Een--, afhankelijk van uw client-besturingssysteem--Hallo [Azure PowerShell](/powershell/azureps-cmdlets-docs) of Hallo [Azure CLI voor Mac, Linux en Windows](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f8c78-117">Either -- depending on your client operating system -- hello [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello [Azure CLI for Mac, Linux, and Windows](../../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="f8c78-118">[OpenSSL](https://www.openssl.org/).</span><span class="sxs-lookup"><span data-stu-id="f8c78-118">[OpenSSL](https://www.openssl.org/).</span></span> <span data-ttu-id="f8c78-119">OpenSSL is gebruikte toogenerate Hallo benodigde certificaten.</span><span class="sxs-lookup"><span data-stu-id="f8c78-119">OpenSSL is used toogenerate hello necessary certificates.</span></span>
* <span data-ttu-id="f8c78-120">Een client Git zoals [Git Bash](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="f8c78-120">A Git client such as [Git Bash](https://git-scm.com/).</span></span>
* <span data-ttu-id="f8c78-121">voorbeeldtoepassing tootest hello, hebt u ook een DNS-server nodig.</span><span class="sxs-lookup"><span data-stu-id="f8c78-121">tootest hello sample application, you'll also need a DNS server.</span></span> <span data-ttu-id="f8c78-122">U kunt alle DNS-servers of services die ondersteuning bieden voor de A-records jokertekens gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f8c78-122">You can use any DNS servers or services that support wildcard A records.</span></span>
* <span data-ttu-id="f8c78-123">Een computer toorun Deis clienthulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="f8c78-123">A computer toorun Deis client tools.</span></span> <span data-ttu-id="f8c78-124">U kunt een lokale computer of een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f8c78-124">You can use either a local machine or a virtual machine.</span></span> <span data-ttu-id="f8c78-125">U kunt deze hulpprogramma's uitvoeren op bijna elke Linux-distributie, maar hello volgende instructies gebruiken Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="f8c78-125">You can run these tools on almost any Linux distribution, but hello following instructions use Ubuntu.</span></span>

## <a name="provision-hello-cluster"></a><span data-ttu-id="f8c78-126">Hallo-cluster inrichten</span><span class="sxs-lookup"><span data-stu-id="f8c78-126">Provision hello cluster</span></span>
<span data-ttu-id="f8c78-127">In deze sectie maakt u een [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) sjabloon van Hallo open-source opslagplaats [azure-snelstartsjablonen](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="f8c78-127">In this section, you'll use an [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) template from hello open source repository [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="f8c78-128">U moet eerst omlaag Hallo sjabloon kopiëren.</span><span class="sxs-lookup"><span data-stu-id="f8c78-128">First, you'll copy down hello template.</span></span> <span data-ttu-id="f8c78-129">Vervolgens maakt u een nieuwe SSH-sleutelpaar voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="f8c78-129">Then, you'll create a new SSH key pair for authentication.</span></span> <span data-ttu-id="f8c78-130">En vervolgens configureert u een nieuwe id voor u cluster.</span><span class="sxs-lookup"><span data-stu-id="f8c78-130">And then, you'll configure a new identifier for you cluster.</span></span> <span data-ttu-id="f8c78-131">En ten slotte kunt u Hallo Shell-script of Hallo PowerShell script tooprovision Hallo cluster.</span><span class="sxs-lookup"><span data-stu-id="f8c78-131">And finally, you'll use either hello Shell script or hello PowerShell script tooprovision hello cluster.</span></span>

1. <span data-ttu-id="f8c78-132">Kloon Hallo opslagplaats: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="f8c78-132">Clone hello repository: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. <span data-ttu-id="f8c78-133">Ga toohello sjabloonmap:</span><span class="sxs-lookup"><span data-stu-id="f8c78-133">Go toohello template folder:</span></span>
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. <span data-ttu-id="f8c78-134">Maak een nieuwe SSH-sleutelpaar ssh-keygen gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f8c78-134">Create a new SSH key pair using ssh-keygen:</span></span>
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. <span data-ttu-id="f8c78-135">Een certificaat met de Hallo boven de persoonlijke sleutel genereren:</span><span class="sxs-lookup"><span data-stu-id="f8c78-135">Generate a certificate using hello above private key:</span></span>
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file toobe generated]
5. <span data-ttu-id="f8c78-136">Ga te[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate een nieuw cluster-token ziet eruit als:</span><span class="sxs-lookup"><span data-stu-id="f8c78-136">Go too[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate a new cluster token, which looks something like:</span></span>
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   <span data-ttu-id="f8c78-137">Elke virtuele CoreOS-cluster moet een unieke token van deze gratis service toohave.</span><span class="sxs-lookup"><span data-stu-id="f8c78-137">Each CoreOS cluster needs toohave a unique token from this free service.</span></span> <span data-ttu-id="f8c78-138">Zie [virtuele CoreOS documentatie](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f8c78-138">Please see [CoreOS documentation](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) for more details.</span></span>
6. <span data-ttu-id="f8c78-139">Hallo wijzigen **cloud config.yaml** bestand tooreplace Hallo bestaande **detectie** token met het nieuwe token Hallo:</span><span class="sxs-lookup"><span data-stu-id="f8c78-139">Modify hello **cloud-config.yaml** file tooreplace hello existing  **discovery** token with hello new token:</span></span>
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment hello following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. <span data-ttu-id="f8c78-140">Hallo wijzigen **azuredeploy-parameters.json** bestand: u hebt gemaakt in stap 4 in een teksteditor openen Hallo-certificaat.</span><span class="sxs-lookup"><span data-stu-id="f8c78-140">Modify hello **azuredeploy-parameters.json** file: Open hello certificate you created in step 4 in a text editor.</span></span> <span data-ttu-id="f8c78-141">Kopieer alle tekst tussen `----BEGIN CERTIFICATE-----` en `-----END CERTIFICATE-----` in Hallo **sshKeyData** parameter (u moet tooremove alle newline-tekens).</span><span class="sxs-lookup"><span data-stu-id="f8c78-141">Copy all text between `----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` into hello **sshKeyData** parameter (you'll need tooremove all newline characters).</span></span>
8. <span data-ttu-id="f8c78-142">Hallo wijzigen **newStorageAccountName** parameter.</span><span class="sxs-lookup"><span data-stu-id="f8c78-142">Modify hello **newStorageAccountName** parameter.</span></span> <span data-ttu-id="f8c78-143">Dit is de opslagaccount Hallo voor VM-OS-schijven.</span><span class="sxs-lookup"><span data-stu-id="f8c78-143">This is hello storage account for VM OS disks.</span></span> <span data-ttu-id="f8c78-144">De accountnaam heeft toobe globaal uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="f8c78-144">This account name has toobe globally unique.</span></span>
9. <span data-ttu-id="f8c78-145">Hallo wijzigen **publicDomainName** parameter.</span><span class="sxs-lookup"><span data-stu-id="f8c78-145">Modify hello **publicDomainName** parameter.</span></span> <span data-ttu-id="f8c78-146">Hiermee wordt een onderdeel van Hallo DNS-naam die is gekoppeld aan Hallo load balancer openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="f8c78-146">This will become part of hello DNS name associated with hello load balancer public IP.</span></span> <span data-ttu-id="f8c78-147">Hallo laatste FQDN hebben Hallo indeling van *[waarde van deze parameter]*. *[regio]* . cloudapp.azure.com. Bijvoorbeeld, als u Hallo naam als deishbai32 opgeven en Hallo resourcegroep bevindt zich de regio VS-West geïmplementeerde toohello en vervolgens laatste Hallo FQDN tooyour load balancer worden deishbai32.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="f8c78-147">hello final FQDN will have hello format of *[value of this parameter]*.*[region]*.cloudapp.azure.com. For example, if you specify hello name as deishbai32, and hello resource group is deployed toohello West US region, then hello final FQDN tooyour load balancer will be deishbai32.westus.cloudapp.azure.com.</span></span>
10. <span data-ttu-id="f8c78-148">Hallo parameterbestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="f8c78-148">Save hello parameter file.</span></span> <span data-ttu-id="f8c78-149">En vervolgens kunt u met Azure PowerShell Hallo-cluster inrichten:</span><span class="sxs-lookup"><span data-stu-id="f8c78-149">And then you can provision hello cluster using Azure PowerShell:</span></span>
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    <span data-ttu-id="f8c78-150">of Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="f8c78-150">or Azure CLI:</span></span>
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. <span data-ttu-id="f8c78-151">Zodra de resourcegroep Hallo is geconfigureerd, ziet u alle Hallo bronnen in Hallo-groep op de klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f8c78-151">Once hello resource group is provisioned, you can see all hello resources in hello group on Azure classic portal.</span></span> <span data-ttu-id="f8c78-152">Zoals u in de volgende schermafbeelding Hallo Hallo resourcegroep bevat een virtueel netwerk met drie virtuele machines, die lid zijn van toohello dezelfde beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="f8c78-152">As shown in hello following screenshot, hello resource group contains a virtual network with three VMs, which are joined toohello same availability set.</span></span> <span data-ttu-id="f8c78-153">Hallo-groep bevat ook een load balancer met een bijbehorende openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="f8c78-153">hello group also contains a load balancer, which has an associated public IP.</span></span>
    
    ![Hallo ingericht resourcegroep in de klassieke Azure-portal](./media/deis-cluster/resource-group.png)

## <a name="install-hello-client"></a><span data-ttu-id="f8c78-155">Hallo-client installeren</span><span class="sxs-lookup"><span data-stu-id="f8c78-155">Install hello client</span></span>
<span data-ttu-id="f8c78-156">U moet **deisctl** toocontrol uw cluster Deis.</span><span class="sxs-lookup"><span data-stu-id="f8c78-156">You need **deisctl** toocontrol your Deis cluster.</span></span> <span data-ttu-id="f8c78-157">Hoewel deisctl wordt automatisch geïnstalleerd op alle clusterknooppunten van hello, is een goede gewoonte toouse deisctl op een afzonderlijke administratieve machine.</span><span class="sxs-lookup"><span data-stu-id="f8c78-157">Although deisctl is automatically installed in all hello cluster nodes, it's a good practice toouse deisctl on a separate administrative machine.</span></span> <span data-ttu-id="f8c78-158">Bovendien, omdat alle knooppunten zijn geconfigureerd met alleen persoonlijke IP-adressen, moet u toouse SSH-tunneling via Hallo load balancer met een openbare IP-adres, tooconnect toohello knooppunt machines.</span><span class="sxs-lookup"><span data-stu-id="f8c78-158">Furthermore, because all nodes are configured with only private IP addresses, you'll need toouse SSH tunneling through hello load balancer, which has a public IP, tooconnect toohello node machines.</span></span> <span data-ttu-id="f8c78-159">Hallo volgen Hallo stappen voor het instellen van deisctl op een afzonderlijke Ubuntu fysieke of virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f8c78-159">hello following are hello steps of setting up deisctl on a separate Ubuntu physical or virtual machine.</span></span>

1. <span data-ttu-id="f8c78-160">Installatie deisctl:mkdir deis</span><span class="sxs-lookup"><span data-stu-id="f8c78-160">Install deisctl:mkdir deis</span></span>
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. <span data-ttu-id="f8c78-161">De agent van uw persoonlijke sleutel toossh toevoegen:</span><span class="sxs-lookup"><span data-stu-id="f8c78-161">Add your private key toossh agent:</span></span>
   
        eval `ssh-agent -s`
        ssh-add [path toohello private key file, see step 1 in hello previous section]
3. <span data-ttu-id="f8c78-162">Deisctl configureren:</span><span class="sxs-lookup"><span data-stu-id="f8c78-162">Configure deisctl:</span></span>
   
        export DEISCTL_TUNNEL=[public ip of hello load balancer]:2223

<span data-ttu-id="f8c78-163">Hallo sjabloon definieert inkomende NAT-regels die zijn toegewezen 2223 tooinstance 1, 2224 tooinstance 2 en 2225 tooinstance 3.</span><span class="sxs-lookup"><span data-stu-id="f8c78-163">hello template defines inbound NAT rules that map 2223 tooinstance 1, 2224 tooinstance 2, and 2225 tooinstance 3.</span></span> <span data-ttu-id="f8c78-164">Dit biedt redundantie voor het gebruik Hallo deisctl hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="f8c78-164">This provides redundancy for using hello deisctl tool.</span></span> <span data-ttu-id="f8c78-165">U kunt deze regels in de klassieke Azure-portal bekijken:</span><span class="sxs-lookup"><span data-stu-id="f8c78-165">You can examine these rules on Azure classic portal:</span></span>

![NAT-regels op Hallo load balancer](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> <span data-ttu-id="f8c78-167">Hallo sjabloon ondersteunt momenteel alleen clusters 3-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="f8c78-167">Currently hello template only supports 3-node clusters.</span></span> <span data-ttu-id="f8c78-168">Dit is vanwege een beperking in Azure Resource Manager-sjabloon NAT regeldefinitie, die de syntaxis van de lus niet ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="f8c78-168">This is because of a limitation in Azure Resource Manager template NAT rule definition, which doesn’t support loop syntax.</span></span>
> 
> 

## <a name="install-and-start-hello-deis-platform"></a><span data-ttu-id="f8c78-169">Installeren en starten Hallo Deis platform</span><span class="sxs-lookup"><span data-stu-id="f8c78-169">Install and start hello Deis platform</span></span>
<span data-ttu-id="f8c78-170">Nu u kunt deisctl tooinstall gebruiken en Hallo start Deis platform:</span><span class="sxs-lookup"><span data-stu-id="f8c78-170">Now you can use deisctl tooinstall and start hello Deis platform:</span></span>

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path toohello private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> <span data-ttu-id="f8c78-171">Begin Hallo platform even duurt voordat (zo veel 10 minuten).</span><span class="sxs-lookup"><span data-stu-id="f8c78-171">Starting hello platform takes a while (as much as 10 minutes).</span></span> <span data-ttu-id="f8c78-172">Met name, kan Hallo builder-service wordt gestart lang duren.</span><span class="sxs-lookup"><span data-stu-id="f8c78-172">Especially, starting hello builder service can take a long time.</span></span> <span data-ttu-id="f8c78-173">En soms duurt een paar pogingen toosucceed: als Hallo bewerking toohang lijkt, kunt u `ctrl+c` toobreak uitvoering van het Hallo-opdracht en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="f8c78-173">And sometimes it takes a few tries toosucceed: If hello operation seems toohang, try typing `ctrl+c` toobreak execution of hello command and retry.</span></span>
> 
> 

<span data-ttu-id="f8c78-174">U kunt `deisctl list` tooverify als alle services worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="f8c78-174">You can use `deisctl list` tooverify if all services are running:</span></span>

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

<span data-ttu-id="f8c78-175">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="f8c78-175">Congratulations!</span></span> <span data-ttu-id="f8c78-176">Nu u een actieve hebt Deis clsuter op Azure!</span><span class="sxs-lookup"><span data-stu-id="f8c78-176">Now you've got a running Deis clsuter on Azure!</span></span> <span data-ttu-id="f8c78-177">Vervolgens laten we u een voorbeeld Ga toepassing toosee Hallo cluster in actie implementeert.</span><span class="sxs-lookup"><span data-stu-id="f8c78-177">Next, let's deploy a sample Go application toosee hello cluster in action.</span></span>

## <a name="deploy-and-scale-a-hello-world-application"></a><span data-ttu-id="f8c78-178">Implementeren en schalen van een toepassing Hello World</span><span class="sxs-lookup"><span data-stu-id="f8c78-178">Deploy and scale a Hello World application</span></span>
<span data-ttu-id="f8c78-179">Hallo volgende stappen laten zien hoe toodeploy "Hallo wereld" Ga toepassing toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="f8c78-179">hello following steps show how toodeploy a "Hello World" Go application toohello cluster.</span></span> <span data-ttu-id="f8c78-180">Hallo stappen zijn gebaseerd op [Deis documentatie](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span><span class="sxs-lookup"><span data-stu-id="f8c78-180">hello steps are based on [Deis documentation](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span></span>

1. <span data-ttu-id="f8c78-181">Voor Hallo routering mesh toowork goed is, moet u toohave een jokerteken A-record voor uw domein toohello openbare IP-adres van Hallo load balancer aan te wijzen.</span><span class="sxs-lookup"><span data-stu-id="f8c78-181">For hello routing mesh toowork properly, you’ll need toohave a wildcard A record for your domain pointing toohello public IP of hello load balancer.</span></span> <span data-ttu-id="f8c78-182">Hallo volgende schermafbeelding ziet Hallo A-record voor een voorbeeld-domeinregistratie op GoDaddy:</span><span class="sxs-lookup"><span data-stu-id="f8c78-182">hello following screenshot shows hello A record for a sample domain registration on GoDaddy:</span></span>
   
    ![Godaddy-A-record](./media/deis-cluster/go-daddy.png)
   
   <p />
2. <span data-ttu-id="f8c78-184">Installatie deis:</span><span class="sxs-lookup"><span data-stu-id="f8c78-184">Install deis:</span></span>
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. <span data-ttu-id="f8c78-185">Maak een nieuwe SSH-sleutel en voeg vervolgens de openbare sleutel tooGitHub hello (natuurlijk kunt u ook hergebruiken uw bestaande sleutels).</span><span class="sxs-lookup"><span data-stu-id="f8c78-185">Create a new SSH key, and then add hello public key tooGitHub (of course, you can also reuse your existing keys).</span></span> <span data-ttu-id="f8c78-186">een nieuw SSH-sleutelpaar, toocreate gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f8c78-186">toocreate a new SSH key pair, use:</span></span>
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s toouse default file names and empty passcode)
4. <span data-ttu-id="f8c78-187">Id_rsa.pub of openbare sleutel van uw keuze, tooGitHub Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f8c78-187">Add id_rsa.pub, or hello public key of your choice, tooGitHub.</span></span> <span data-ttu-id="f8c78-188">U kunt dit doen via Hallo toevoegen SSH sleutel knop in het scherm van de SSH-sleutels configuratie:</span><span class="sxs-lookup"><span data-stu-id="f8c78-188">You can do this by using hello Add SSH key button in your SSH keys configuration screen:</span></span>
   
   ![GitHub-sleutel](./media/deis-cluster/github-key.png)
   
   <p />
5. <span data-ttu-id="f8c78-190">Een nieuwe gebruiker registreren:</span><span class="sxs-lookup"><span data-stu-id="f8c78-190">Register a new user:</span></span>
   
        deis register http://deis.[your domain]
   <p />
6. <span data-ttu-id="f8c78-191">Hallo SSH-sleutel toevoegen:</span><span class="sxs-lookup"><span data-stu-id="f8c78-191">Add hello SSH key:</span></span>
   
        deis keys:add [path tooyour SSH public key]
   <p />      
7. <span data-ttu-id="f8c78-192">Een toepassing maken.</span><span class="sxs-lookup"><span data-stu-id="f8c78-192">Create an application.</span></span>
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p /><span data-ttu-id="f8c78-193">
8.Hallo git push activeren Docker installatiekopieën toobe gemaakt en geïmplementeerd, duurt enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="f8c78-193">
8. hello git push will trigger Docker images toobe built and deployed, which will take a few minutes.</span></span> <span data-ttu-id="f8c78-194">Mijn ervaring van soms vastlopen stap 10 (Pushing tooprivate-opslagplaats voor installatiekopieën).</span><span class="sxs-lookup"><span data-stu-id="f8c78-194">From my experience, occasionally, Step 10 (Pushing image tooprivate repository) may hang.</span></span> <span data-ttu-id="f8c78-195">Als dit gebeurt, kunt u Hallo-proces stoppen verwijderen Hallo toepassing gebruikt ' deis apps: vernietigen – a <application name> ` tooremove hello application and try again. You can use `deis apps:list' toofind Hallo-naam van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="f8c78-195">When this happens, you can stop hello process, remove hello application using `deis apps:destroy –a <application name>` tooremove hello application and try again. You can use `deis apps:list` toofind out hello name of your application.</span></span> <span data-ttu-id="f8c78-196">Als alles werkt, ziet u dat lijkt op de volgende Hallo aan Hallo einde van de uitvoer van de opdracht:</span><span class="sxs-lookup"><span data-stu-id="f8c78-196">If everything works out, you should see something like hello following at hello end of command outputs:</span></span>
   
        -----> Launching...
               done, lambda-underdog:v2 deployed tooDeis
               http://lambda-underdog.artitrack.com
               toolearn more, use `deis help` or visit http://deis.io
        toossh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. <span data-ttu-id="f8c78-197">Controleer of de toepassing hello werkt:</span><span class="sxs-lookup"><span data-stu-id="f8c78-197">Verify if hello application is working:</span></span>
   
        curl -S http://[your application name].[your domain]
   <span data-ttu-id="f8c78-198">U ziet het volgende:</span><span class="sxs-lookup"><span data-stu-id="f8c78-198">You should see:</span></span>
   
        Welcome tooDeis!
        See hello documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list tooget hello name of your application).
   <p />
10. <span data-ttu-id="f8c78-199">Hallo too3 toepassingsexemplaren schalen:</span><span class="sxs-lookup"><span data-stu-id="f8c78-199">Scale hello application too3 instances:</span></span>
    
        deis scale cmd=3
    <p />
11. <span data-ttu-id="f8c78-200">Desgewenst kunt u deis info tooexamine details van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="f8c78-200">Optionally, you can use deis info tooexamine details of your application.</span></span> <span data-ttu-id="f8c78-201">Hallo zijn volgende uitgangen van de implementatie van mijn toepassingen:</span><span class="sxs-lookup"><span data-stu-id="f8c78-201">hello following outputs are from my application deployment:</span></span>
    
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

## <a name="next-steps"></a><span data-ttu-id="f8c78-202">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f8c78-202">Next Steps</span></span>
<span data-ttu-id="f8c78-203">In dit artikel doorlopen u alle Hallo stappen tooprovision Deis van een nieuw cluster in Azure met een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f8c78-203">This article walked you through all hello steps tooprovision a new Deis cluster on Azure using an Azure Resource Manager template.</span></span> <span data-ttu-id="f8c78-204">Hallo sjabloon ondersteunt redundantie in tooling verbindingen, evenals taakverdeling voor geïmplementeerde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="f8c78-204">hello template supports redundancy in tooling connections as well as load balancing for deployed applications.</span></span> <span data-ttu-id="f8c78-205">Hallo sjabloon voorkomt ook met behulp van openbare IP-adressen op lid-knooppunten, bespaart kostbare openbare IP-netwerkbronnen en biedt een beter beveiligde omgeving toohost toepassingen.</span><span class="sxs-lookup"><span data-stu-id="f8c78-205">hello template also avoids using public IPs on member nodes, which saves precious public IP resources and provides a more secured environment toohost applications.</span></span> <span data-ttu-id="f8c78-206">toolearn Zie meer Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f8c78-206">toolearn more, see hello following articles:</span></span>

<span data-ttu-id="f8c78-207">[Overzicht van Azure Resource Manager][resource-group-overview]</span><span class="sxs-lookup"><span data-stu-id="f8c78-207">[Azure Resource Manager Overview][resource-group-overview]</span></span>  
<span data-ttu-id="f8c78-208">[Hoe toouse hello Azure CLI][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="f8c78-208">[How toouse hello Azure CLI][azure-command-line-tools]</span></span>  
<span data-ttu-id="f8c78-209">[Azure PowerShell gebruiken met Azure Resource Manager][powershell-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="f8c78-209">[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager]</span></span>  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
