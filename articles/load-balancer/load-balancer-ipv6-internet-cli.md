---
title: aaaCreate een internetgerichte load balancer met IPv6 - Azure CLI | Microsoft Docs
description: Meer informatie over hoe een Internet gerichte load balancer met IPv6 in het gebruik van Azure Resource Manager toocreate hello Azure CLI
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: IPv6-, azure load balancer, dual-stack, openbare IP-adres, systeemeigen ipv6, mobiele, iot
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7ff75ac90d74a74e3d0c27672b36fbd955a086a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-hello-azure-cli"></a><span data-ttu-id="dff38-104">De load balancer met IPv6 in Azure Resource Manager hello Azure CLI met behulp van een Internetgericht maken</span><span class="sxs-lookup"><span data-stu-id="dff38-104">Create an Internet facing load balancer with IPv6 in Azure Resource Manager using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dff38-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dff38-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="dff38-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dff38-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="dff38-107">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="dff38-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="dff38-108">Azure Load Balancer is een Layer-4 (TCP, UDP) load balancer.</span><span class="sxs-lookup"><span data-stu-id="dff38-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="dff38-109">Hallo load balancer biedt hoge beschikbaarheid door het distribueren van inkomend verkeer tussen orde service-exemplaren in cloudservices of virtuele machines in een load balancer-set.</span><span class="sxs-lookup"><span data-stu-id="dff38-109">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="dff38-110">Azure Load Balancer kan deze services ook toepassen op meerdere poorten, meerdere IP-adressen of allebei.</span><span class="sxs-lookup"><span data-stu-id="dff38-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="dff38-111">Voorbeeldscenario voor implementatie</span><span class="sxs-lookup"><span data-stu-id="dff38-111">Example deployment scenario</span></span>

<span data-ttu-id="dff38-112">Hallo volgende diagram illustreert Hallo-oplossing voor taakverdeling wordt geïmplementeerd met behulp van Hallo voorbeeld van de sjabloon die in dit artikel wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="dff38-112">hello following diagram illustrates hello load balancing solution being deployed using hello example template described in this article.</span></span>

![Load balancer-scenario](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

<span data-ttu-id="dff38-114">In dit scenario maakt u hello Azure-resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="dff38-114">In this scenario you will create hello following Azure resources:</span></span>

* <span data-ttu-id="dff38-115">twee virtuele machines (VM's)</span><span class="sxs-lookup"><span data-stu-id="dff38-115">two virtual machines (VMs)</span></span>
* <span data-ttu-id="dff38-116">de virtuele netwerkinterface voor elke virtuele machine met zowel IPv4 als IPv6-adressen die zijn toegewezen</span><span class="sxs-lookup"><span data-stu-id="dff38-116">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>
* <span data-ttu-id="dff38-117">een internetgerichte Load Balancer met een IPv4 en IPv6-openbare IP-adres</span><span class="sxs-lookup"><span data-stu-id="dff38-117">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="dff38-118">een Beschikbaarheidsset toothat bevat Hallo twee virtuele machines</span><span class="sxs-lookup"><span data-stu-id="dff38-118">an Availability Set toothat contains hello two VMs</span></span>
* <span data-ttu-id="dff38-119">twee laden taakverdeling regels toomap Hallo openbare VIP's toohello persoonlijke eindpunten</span><span class="sxs-lookup"><span data-stu-id="dff38-119">two load balancing rules toomap hello public VIPs toohello private endpoints</span></span>

## <a name="deploying-hello-solution-using-hello-azure-cli"></a><span data-ttu-id="dff38-120">Hallo-oplossing met behulp van Azure CLI Hallo implementeren</span><span class="sxs-lookup"><span data-stu-id="dff38-120">Deploying hello solution using hello Azure CLI</span></span>

<span data-ttu-id="dff38-121">Hallo stappen laten zien hoe toocreate een internetverbinding netwerktaakverdeler met Azure Resource Manager met CLI.</span><span class="sxs-lookup"><span data-stu-id="dff38-121">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="dff38-122">Met Azure Resource Manager elke bron wordt gemaakt en afzonderlijk geconfigureerd en vervolgens samengesteld toocreate een resource.</span><span class="sxs-lookup"><span data-stu-id="dff38-122">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a resource.</span></span>

<span data-ttu-id="dff38-123">een load balancer toodeploy, u maken en configureren van Hallo objecten te volgen:</span><span class="sxs-lookup"><span data-stu-id="dff38-123">toodeploy a load balancer, you create and configure hello following objects:</span></span>

* <span data-ttu-id="dff38-124">Front-end-IP-configuratie: bevat openbare IP-adressen voor inkomend netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="dff38-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="dff38-125">Back-end-adresgroep - bevat netwerkinterfaces (NIC's) voor virtuele machines tooreceive-netwerkverkeer Hallo van Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="dff38-125">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="dff38-126">Taakverdeling regels - bevat regels voor toewijzing van een openbare poort op Hallo load balancer tooport in Hallo back-end-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="dff38-126">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="dff38-127">Binnenkomende NAT-regels: regels voor toewijzing van een openbare poort op Hallo load balancer tooa poort voor een specifieke virtuele machine in het back-end-adresgroep Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="dff38-127">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="dff38-128">Tests - beschikbaarheid van health-tests gebruikt toocheck van exemplaren van virtuele machines in het back-end-adresgroep Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="dff38-128">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="dff38-129">Zie [Azure Resource Manager-ondersteuning voor load balancer](load-balancer-arm.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="dff38-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-your-cli-environment-toouse-azure-resource-manager"></a><span data-ttu-id="dff38-130">Instellen van uw CLI omgeving toouse Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dff38-130">Set up your CLI environment toouse Azure Resource Manager</span></span>

<span data-ttu-id="dff38-131">In dit voorbeeld wordt Hallo CLI-hulpprogramma's uitgevoerd in een PowerShell-opdrachtvenster.</span><span class="sxs-lookup"><span data-stu-id="dff38-131">For this example, we are running hello CLI tools in a PowerShell command window.</span></span> <span data-ttu-id="dff38-132">We hello Azure PowerShell-cmdlets niet gebruiken, maar we gebruiken de scripting mogelijkheden tooimprove leesbaarheid en opnieuw gebruiken van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dff38-132">We are not using hello Azure PowerShell cmdlets but we use PowerShell's scripting capabilities tooimprove readability and reuse.</span></span>

1. <span data-ttu-id="dff38-133">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.</span><span class="sxs-lookup"><span data-stu-id="dff38-133">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="dff38-134">Voer Hallo **azure config mode** opdracht tooswitch tooResource Manager-modus.</span><span class="sxs-lookup"><span data-stu-id="dff38-134">Run hello **azure config mode** command tooswitch tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="dff38-135">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="dff38-135">Expected output:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="dff38-136">Meld u aan tooAzure en een lijst met abonnementen ophalen.</span><span class="sxs-lookup"><span data-stu-id="dff38-136">Sign in tooAzure and get a list of subscriptions.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="dff38-137">Voer uw Azure-referenties wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="dff38-137">Enter your Azure credentials when prompted.</span></span>

    ```azurecli
    azure account list
    ```

    <span data-ttu-id="dff38-138">Kies Hallo abonnement die u wilt dat toouse.</span><span class="sxs-lookup"><span data-stu-id="dff38-138">Pick hello subscription you want toouse.</span></span> <span data-ttu-id="dff38-139">Noteer Hallo abonnements-Id voor de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="dff38-139">Make note of hello subscription Id for hello next step.</span></span>

4. <span data-ttu-id="dff38-140">Variabelen voor gebruik met CLI-opdrachten Hallo PowerShell instellen.</span><span class="sxs-lookup"><span data-stu-id="dff38-140">Set up PowerShell variables for use with hello CLI commands.</span></span>

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a><span data-ttu-id="dff38-141">Een resourcegroep, een load balancer, een virtueel netwerk en subnetten maken</span><span class="sxs-lookup"><span data-stu-id="dff38-141">Create a resource group, a load balancer, a virtual network, and subnets</span></span>

1. <span data-ttu-id="dff38-142">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="dff38-142">Create a resource group</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="dff38-143">Een load balancer maken</span><span class="sxs-lookup"><span data-stu-id="dff38-143">Create a load balancer</span></span>

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. <span data-ttu-id="dff38-144">Maak een virtueel netwerk (VNet).</span><span class="sxs-lookup"><span data-stu-id="dff38-144">Create a virtual network (VNet).</span></span>

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    <span data-ttu-id="dff38-145">Maak twee subnetten in dit VNet.</span><span class="sxs-lookup"><span data-stu-id="dff38-145">Create two subnets in this VNet.</span></span>

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-hello-front-end-pool"></a><span data-ttu-id="dff38-146">Openbare IP-adressen voor Hallo front-pool maken</span><span class="sxs-lookup"><span data-stu-id="dff38-146">Create public IP addresses for hello front-end pool</span></span>

1. <span data-ttu-id="dff38-147">Hallo PowerShell variabelen instellen</span><span class="sxs-lookup"><span data-stu-id="dff38-147">Set up hello PowerShell variables</span></span>

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. <span data-ttu-id="dff38-148">Maak een openbare IP-Hallo front-end-IP-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="dff38-148">Create a public IP address hello front-end IP pool.</span></span>

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="dff38-149">Hallo load balancer gebruikmaakt van Hallo domeinlabel van Hallo openbare IP-adres als de FQDN.</span><span class="sxs-lookup"><span data-stu-id="dff38-149">hello load balancer uses hello domain label of hello public IP as its FQDN.</span></span> <span data-ttu-id="dff38-150">Deze een wijziging van de klassieke implementatie dat gebruikmaakt van Hallo cloudservicenaam zoals Hallo load balancer FQDN-naam.</span><span class="sxs-lookup"><span data-stu-id="dff38-150">This a change from classic deployment, which uses hello cloud service name as hello load balancer FQDN.</span></span>
    > <span data-ttu-id="dff38-151">In dit voorbeeld Hallo FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="dff38-151">In this example, hello FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span></span>

## <a name="create-front-end-and-back-end-pools"></a><span data-ttu-id="dff38-152">Front-end en back-end-adresgroepen maken</span><span class="sxs-lookup"><span data-stu-id="dff38-152">Create front-end and back-end pools</span></span>

<span data-ttu-id="dff38-153">In dit voorbeeld maakt het front-end-IP-groep hello, die Hallo binnenkomend netwerkverkeer op Hallo load balancer ontvangt en Hallo backend-IP-groep waar front-pool Hallo Hallo taakverdeling netwerkverkeer verzendt.</span><span class="sxs-lookup"><span data-stu-id="dff38-153">This example creates hello front-end IP pool that receives hello incoming network traffic on hello load balancer and hello back-end IP pool where hello front-end pool sends hello load balanced network traffic.</span></span>

1. <span data-ttu-id="dff38-154">Hallo PowerShell variabelen instellen</span><span class="sxs-lookup"><span data-stu-id="dff38-154">Set up hello PowerShell variables</span></span>

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. <span data-ttu-id="dff38-155">Maak een front-end-IP-adresgroep Hallo openbare IP-adres gemaakt in de vorige stap Hallo en Hallo load balancer koppelen.</span><span class="sxs-lookup"><span data-stu-id="dff38-155">Create a front-end IP pool associating hello public IP created in hello previous step and hello load balancer.</span></span>

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-hello-probe-nat-rules-and-lb-rules"></a><span data-ttu-id="dff38-156">Hallo test, NAT-regels en LB regels maken</span><span class="sxs-lookup"><span data-stu-id="dff38-156">Create hello probe, NAT rules, and LB rules</span></span>

<span data-ttu-id="dff38-157">In dit voorbeeld maakt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="dff38-157">This example creates hello following items:</span></span>

* <span data-ttu-id="dff38-158">een test regel toocheck voor connectiviteit tooTCP poort 80</span><span class="sxs-lookup"><span data-stu-id="dff38-158">a probe rule toocheck for connectivity tooTCP port 80</span></span>
* <span data-ttu-id="dff38-159">een NAT-regel tootranslate alle binnenkomend verkeer op poort 3389 tooport 3389 voor RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="dff38-159">a NAT rule tootranslate all incoming traffic on port 3389 tooport 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="dff38-160">een NAT-regel tootranslate alle binnenkomend verkeer op poort 3391 tooport 3389 voor RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="dff38-160">a NAT rule tootranslate all incoming traffic on port 3391 tooport 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="dff38-161">een load balancer-regel toobalance alle binnenkomend verkeer op poort 80 tooport 80 op Hallo adressen in Hallo back-end-pool.</span><span class="sxs-lookup"><span data-stu-id="dff38-161">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>

<span data-ttu-id="dff38-162"><sup>1</sup> NAT-regels zijn gekoppeld tooa specifieke virtuele machine exemplaar achter Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="dff38-162"><sup>1</sup> NAT rules are associated tooa specific virtual machine instance behind hello load balancer.</span></span> <span data-ttu-id="dff38-163">Hallo-netwerkverkeer dat binnenkomt op poort 3389 verzonden toohello specifieke virtuele machine en de poort die is gekoppeld aan Hallo NAT-regel.</span><span class="sxs-lookup"><span data-stu-id="dff38-163">hello network traffic arriving on port 3389 is sent toohello specific virtual machine and port associated with hello NAT rule.</span></span> <span data-ttu-id="dff38-164">U moet een protocol (UDP of TCP) voor een NAT-regel opgeven.</span><span class="sxs-lookup"><span data-stu-id="dff38-164">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="dff38-165">Beide protocollen kunnen niet worden toegewezen toohello dezelfde poort.</span><span class="sxs-lookup"><span data-stu-id="dff38-165">Both protocols can't be assigned toohello same port.</span></span>

1. <span data-ttu-id="dff38-166">Hallo PowerShell variabelen instellen</span><span class="sxs-lookup"><span data-stu-id="dff38-166">Set up hello PowerShell variables</span></span>

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. <span data-ttu-id="dff38-167">Hallo-test maken</span><span class="sxs-lookup"><span data-stu-id="dff38-167">Create hello probe</span></span>

    <span data-ttu-id="dff38-168">Hallo wordt volgende voorbeeld een TCP-test waarmee wordt gecontroleerd of voor connectiviteit tooback-end TCP-poort 80 elke 15 seconden.</span><span class="sxs-lookup"><span data-stu-id="dff38-168">hello following example creates a TCP probe that checks for connectivity tooback-end TCP port 80 every 15 seconds.</span></span> <span data-ttu-id="dff38-169">Het markeert Hallo back-end-bron niet beschikbaar na twee achtereenvolgende mislukte pogingen.</span><span class="sxs-lookup"><span data-stu-id="dff38-169">It will mark hello back-end resource unavailable after two consecutive failures.</span></span>

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. <span data-ttu-id="dff38-170">Binnenkomende NAT-regels waarmee de RDP-verbindingen toohello back-end resources maken</span><span class="sxs-lookup"><span data-stu-id="dff38-170">Create inbound NAT rules that allow RDP connections toohello back-end resources</span></span>

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. <span data-ttu-id="dff38-171">Regels die verkeer toodifferent back-end-poorten, afhankelijk van welke front-end ontvangen Hallo-aanvraag verzenden voor een load balancer maken</span><span class="sxs-lookup"><span data-stu-id="dff38-171">Create a load balancer rules that send traffic toodifferent back-end ports depending on which front end received hello request</span></span>

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. <span data-ttu-id="dff38-172">Controleer uw instellingen</span><span class="sxs-lookup"><span data-stu-id="dff38-172">Check your settings</span></span>

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    <span data-ttu-id="dff38-173">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="dff38-173">Expected output:</span></span>

        info:    Executing command network lb show
        info:    Looking up hello load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a><span data-ttu-id="dff38-174">NIC's maken</span><span class="sxs-lookup"><span data-stu-id="dff38-174">Create NICs</span></span>

<span data-ttu-id="dff38-175">NIC's maken en deze koppelt tooNAT regels, load balancer-regels en -tests.</span><span class="sxs-lookup"><span data-stu-id="dff38-175">Create NICs and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="dff38-176">Hallo PowerShell variabelen instellen</span><span class="sxs-lookup"><span data-stu-id="dff38-176">Set up hello PowerShell variables</span></span>

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. <span data-ttu-id="dff38-177">Maken van een NIC voor elke back-end en een IPv6-configuratie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="dff38-177">Create a NIC for each back-end and add an IPv6 configuration.</span></span>

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-hello-back-end-vm-resources-and-attach-each-nic"></a><span data-ttu-id="dff38-178">Hallo back-end VM resources maken en koppelen van elke NIC</span><span class="sxs-lookup"><span data-stu-id="dff38-178">Create hello back-end VM resources and attach each NIC</span></span>

<span data-ttu-id="dff38-179">toocreate virtuele machines, moet u een opslagaccount hebben.</span><span class="sxs-lookup"><span data-stu-id="dff38-179">toocreate VMs, you must have a storage account.</span></span> <span data-ttu-id="dff38-180">Load balancing, moeten Hallo VMs toobe leden van een beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="dff38-180">For load balancing, hello VMs need toobe members of an availability set.</span></span> <span data-ttu-id="dff38-181">Zie voor meer informatie over het maken van virtuele machines [maken van een virtuele machine in Azure met behulp van PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="dff38-181">For more information about creating VMs, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="dff38-182">Hallo PowerShell variabelen instellen</span><span class="sxs-lookup"><span data-stu-id="dff38-182">Set up hello PowerShell variables</span></span>

    ```powershell
    $storageAccountName = "ps08092016v6sa0"
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $disk1Name = "WindowsVMosDisk1"
    $disk2Name = "WindowsVMosDisk2"
    $osDisk1Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk1Name.vhd"
    $osDisk2Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk2Name.vhd"
    $imageurn "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > <span data-ttu-id="dff38-183">Dit voorbeeld wordt Hallo gebruikersnaam en wachtwoord voor virtuele machines Hallo in ongecodeerde tekst.</span><span class="sxs-lookup"><span data-stu-id="dff38-183">This example uses hello username and password for hello VMs in clear text.</span></span> <span data-ttu-id="dff38-184">Juiste Wees voorzichtig bij het gebruik van referenties in Hallo wissen.</span><span class="sxs-lookup"><span data-stu-id="dff38-184">Appropriate care must be taken when using credentials in hello clear.</span></span> <span data-ttu-id="dff38-185">Zie voor een veiligere methode afhandelen van referenties in PowerShell Hallo [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dff38-185">For a more secure method of handling credentials in PowerShell, see hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

2. <span data-ttu-id="dff38-186">Hallo storage-account en beschikbaarheid set maken</span><span class="sxs-lookup"><span data-stu-id="dff38-186">Create hello storage account and availability set</span></span>

    <span data-ttu-id="dff38-187">U mag een bestaand opslagaccount gebruiken bij het maken van Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="dff38-187">You may use an existing storage account when you create hello VMs.</span></span> <span data-ttu-id="dff38-188">Hallo volgende opdracht maakt een nieuw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="dff38-188">hello following command creates a new storage account.</span></span>

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    <span data-ttu-id="dff38-189">Maak vervolgens Hallo beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="dff38-189">Next, create hello availability set.</span></span>

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. <span data-ttu-id="dff38-190">Hallo virtuele machines maken met de Hallo gekoppeld NIC 's</span><span class="sxs-lookup"><span data-stu-id="dff38-190">Create hello virtual machines with hello associated NICs</span></span>

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a><span data-ttu-id="dff38-191">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dff38-191">Next steps</span></span>

[<span data-ttu-id="dff38-192">Aan de slag met het configureren van een interne load balancer</span><span class="sxs-lookup"><span data-stu-id="dff38-192">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="dff38-193">Een distributiemodus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="dff38-193">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="dff38-194">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="dff38-194">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
