---
title: Maak een internetgerichte load balancer met IPv6 - Azure CLI | Microsoft Docs
description: Informatie over het maken van een Internetgericht load balancer met IPv6 in Azure Resource Manager met de Azure CLI
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
ms.openlocfilehash: efb4771800c42df544c3cc37d1d164045fdcaf3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-the-azure-cli"></a><span data-ttu-id="59e92-104">Maken van een Internetgericht load balancer met IPv6 in Azure Resource Manager met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="59e92-104">Create an Internet facing load balancer with IPv6 in Azure Resource Manager using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="59e92-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="59e92-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="59e92-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="59e92-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="59e92-107">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="59e92-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="59e92-108">Azure Load Balancer is een Layer-4 (TCP, UDP) load balancer.</span><span class="sxs-lookup"><span data-stu-id="59e92-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="59e92-109">De load balancer biedt hoge beschikbaarheid bij het verdelen van inkomend verkeer over gezonde service-exemplaren in cloudservices of virtuele machines in een load balancer-set.</span><span class="sxs-lookup"><span data-stu-id="59e92-109">The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="59e92-110">Azure Load Balancer kan deze services ook toepassen op meerdere poorten, meerdere IP-adressen of allebei.</span><span class="sxs-lookup"><span data-stu-id="59e92-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="59e92-111">Voorbeeldscenario voor implementatie</span><span class="sxs-lookup"><span data-stu-id="59e92-111">Example deployment scenario</span></span>

<span data-ttu-id="59e92-112">Het volgende diagram illustreert de oplossing voor taakverdeling wordt geïmplementeerd met behulp van de voorbeeldsjabloon die in dit artikel wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="59e92-112">The following diagram illustrates the load balancing solution being deployed using the example template described in this article.</span></span>

![Load balancer-scenario](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

<span data-ttu-id="59e92-114">In dit scenario maakt u de volgende Azure-resources:</span><span class="sxs-lookup"><span data-stu-id="59e92-114">In this scenario you will create the following Azure resources:</span></span>

* <span data-ttu-id="59e92-115">twee virtuele machines (VM's)</span><span class="sxs-lookup"><span data-stu-id="59e92-115">two virtual machines (VMs)</span></span>
* <span data-ttu-id="59e92-116">de virtuele netwerkinterface voor elke virtuele machine met zowel IPv4 als IPv6-adressen die zijn toegewezen</span><span class="sxs-lookup"><span data-stu-id="59e92-116">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>
* <span data-ttu-id="59e92-117">een internetgerichte Load Balancer met een IPv4 en IPv6-openbare IP-adres</span><span class="sxs-lookup"><span data-stu-id="59e92-117">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="59e92-118">een Beschikbaarheidsset aan die bevat de twee virtuele machines</span><span class="sxs-lookup"><span data-stu-id="59e92-118">an Availability Set to that contains the two VMs</span></span>
* <span data-ttu-id="59e92-119">twee taakverdelingsregels het openbare VIP's worden toegewezen aan de persoonlijke eindpunten</span><span class="sxs-lookup"><span data-stu-id="59e92-119">two load balancing rules to map the public VIPs to the private endpoints</span></span>

## <a name="deploying-the-solution-using-the-azure-cli"></a><span data-ttu-id="59e92-120">De oplossing implementeren met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="59e92-120">Deploying the solution using the Azure CLI</span></span>

<span data-ttu-id="59e92-121">De volgende stappen laten zien hoe u Azure Resource Manager gebruikt om een internetgerichte load balancer te maken met behulp van CLI.</span><span class="sxs-lookup"><span data-stu-id="59e92-121">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="59e92-122">Met Azure Resource Manager wordt elke resource afzonderlijk gemaakt en geconfigureerd, en vervolgens samengevoegd om een resource te maken.</span><span class="sxs-lookup"><span data-stu-id="59e92-122">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a resource.</span></span>

<span data-ttu-id="59e92-123">Voor het implementeren van een load balancer maken en configureren van de volgende objecten:</span><span class="sxs-lookup"><span data-stu-id="59e92-123">To deploy a load balancer, you create and configure the following objects:</span></span>

* <span data-ttu-id="59e92-124">Front-end-IP-configuratie: bevat openbare IP-adressen voor inkomend netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="59e92-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="59e92-125">Back-endadresgroep: bevat netwerkinterfaces (NIC's) waardoor de virtuele machines netwerkverkeer kunnen ontvangen van de load balancer.</span><span class="sxs-lookup"><span data-stu-id="59e92-125">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="59e92-126">Regels voor taakverdeling: bevat regels die een openbare poort op de load balancer toewijzen aan een poort in de back-endadresgroep.</span><span class="sxs-lookup"><span data-stu-id="59e92-126">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="59e92-127">NAT-regels voor binnenkomende verbindingen: bevat regels die een openbare poort op de load balancer toewijzen aan een poort voor een specifieke virtuele machine in de back-endadresgroep.</span><span class="sxs-lookup"><span data-stu-id="59e92-127">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="59e92-128">Tests: bevat statustests die worden gebruikt om de beschikbaarheid van exemplaren van virtuele machines in de back-endadresgroep te controleren.</span><span class="sxs-lookup"><span data-stu-id="59e92-128">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="59e92-129">Zie [Azure Resource Manager-ondersteuning voor load balancer](load-balancer-arm.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="59e92-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-your-cli-environment-to-use-azure-resource-manager"></a><span data-ttu-id="59e92-130">Uw omgeving CLI instellen voor gebruik van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="59e92-130">Set up your CLI environment to use Azure Resource Manager</span></span>

<span data-ttu-id="59e92-131">In dit voorbeeld wordt de CLI-hulpprogramma's uitgevoerd in een PowerShell-opdrachtvenster.</span><span class="sxs-lookup"><span data-stu-id="59e92-131">For this example, we are running the CLI tools in a PowerShell command window.</span></span> <span data-ttu-id="59e92-132">We de Azure PowerShell-cmdlets niet gebruiken, maar we scriptmogelijkheden van PowerShell gebruiken voor het verbeteren van de leesbaarheid en opnieuw kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="59e92-132">We are not using the Azure PowerShell cmdlets but we use PowerShell's scripting capabilities to improve readability and reuse.</span></span>

1. <span data-ttu-id="59e92-133">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [De Azure CLI installeren en configureren](../cli-install-nodejs.md) en volgt u de instructies tot het punt waar u uw Azure-account en -abonnement moet selecteren.</span><span class="sxs-lookup"><span data-stu-id="59e92-133">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="59e92-134">Voer de **azure config mode** opdracht overschakelen naar de modus Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="59e92-134">Run the **azure config mode** command to switch to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="59e92-135">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="59e92-135">Expected output:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="59e92-136">Aanmelden bij Azure en een lijst met abonnementen ophalen.</span><span class="sxs-lookup"><span data-stu-id="59e92-136">Sign in to Azure and get a list of subscriptions.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="59e92-137">Voer uw Azure-referenties wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="59e92-137">Enter your Azure credentials when prompted.</span></span>

    ```azurecli
    azure account list
    ```

    <span data-ttu-id="59e92-138">Kies het abonnement dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="59e92-138">Pick the subscription you want to use.</span></span> <span data-ttu-id="59e92-139">Noteer de abonnements-Id voor de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="59e92-139">Make note of the subscription Id for the next step.</span></span>

4. <span data-ttu-id="59e92-140">Variabelen voor gebruik met de CLI-opdrachten PowerShell instellen.</span><span class="sxs-lookup"><span data-stu-id="59e92-140">Set up PowerShell variables for use with the CLI commands.</span></span>

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

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a><span data-ttu-id="59e92-141">Een resourcegroep, een load balancer, een virtueel netwerk en subnetten maken</span><span class="sxs-lookup"><span data-stu-id="59e92-141">Create a resource group, a load balancer, a virtual network, and subnets</span></span>

1. <span data-ttu-id="59e92-142">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="59e92-142">Create a resource group</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="59e92-143">Een load balancer maken</span><span class="sxs-lookup"><span data-stu-id="59e92-143">Create a load balancer</span></span>

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. <span data-ttu-id="59e92-144">Maak een virtueel netwerk (VNet).</span><span class="sxs-lookup"><span data-stu-id="59e92-144">Create a virtual network (VNet).</span></span>

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    <span data-ttu-id="59e92-145">Maak twee subnetten in dit VNet.</span><span class="sxs-lookup"><span data-stu-id="59e92-145">Create two subnets in this VNet.</span></span>

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-the-front-end-pool"></a><span data-ttu-id="59e92-146">Openbare IP-adressen voor de front-pool maken</span><span class="sxs-lookup"><span data-stu-id="59e92-146">Create public IP addresses for the front-end pool</span></span>

1. <span data-ttu-id="59e92-147">De PowerShell-variabelen instellen</span><span class="sxs-lookup"><span data-stu-id="59e92-147">Set up the PowerShell variables</span></span>

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. <span data-ttu-id="59e92-148">Maak een openbaar IP-adres van de front-end-IP-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="59e92-148">Create a public IP address the front-end IP pool.</span></span>

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="59e92-149">De load balancer gebruikt het domeinlabel van het openbare IP als FQDN.</span><span class="sxs-lookup"><span data-stu-id="59e92-149">The load balancer uses the domain label of the public IP as its FQDN.</span></span> <span data-ttu-id="59e92-150">Dit een wijziging van de klassieke implementatie dat gebruikmaakt van de cloudservice naam als de load balancer FQDN-naam.</span><span class="sxs-lookup"><span data-stu-id="59e92-150">This a change from classic deployment, which uses the cloud service name as the load balancer FQDN.</span></span>
    > <span data-ttu-id="59e92-151">In dit voorbeeld wordt de FQDN-naam is *contoso09152016.southcentralus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="59e92-151">In this example, the FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span></span>

## <a name="create-front-end-and-back-end-pools"></a><span data-ttu-id="59e92-152">Front-end en back-end-adresgroepen maken</span><span class="sxs-lookup"><span data-stu-id="59e92-152">Create front-end and back-end pools</span></span>

<span data-ttu-id="59e92-153">In dit voorbeeld maakt de front-end-IP-adresgroep die het inkomende netwerkverkeer op de load balancer ontvangt en de back-end-IP-adresgroep waar de front-groep het netwerkverkeer van taakverdeling verzendt.</span><span class="sxs-lookup"><span data-stu-id="59e92-153">This example creates the front-end IP pool that receives the incoming network traffic on the load balancer and the back-end IP pool where the front-end pool sends the load balanced network traffic.</span></span>

1. <span data-ttu-id="59e92-154">De PowerShell-variabelen instellen</span><span class="sxs-lookup"><span data-stu-id="59e92-154">Set up the PowerShell variables</span></span>

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. <span data-ttu-id="59e92-155">Maak een front-end-IP-adresgroep door het openbare IP dat u in de vorige stap hebt gemaakt en de load balancer te koppelen.</span><span class="sxs-lookup"><span data-stu-id="59e92-155">Create a front-end IP pool associating the public IP created in the previous step and the load balancer.</span></span>

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-the-probe-nat-rules-and-lb-rules"></a><span data-ttu-id="59e92-156">De test, NAT-regels en LB regels maken</span><span class="sxs-lookup"><span data-stu-id="59e92-156">Create the probe, NAT rules, and LB rules</span></span>

<span data-ttu-id="59e92-157">In dit voorbeeld worden de volgende items gemaakt:</span><span class="sxs-lookup"><span data-stu-id="59e92-157">This example creates the following items:</span></span>

* <span data-ttu-id="59e92-158">een regel test om te controleren op connectiviteit met TCP-poort 80</span><span class="sxs-lookup"><span data-stu-id="59e92-158">a probe rule to check for connectivity to TCP port 80</span></span>
* <span data-ttu-id="59e92-159">een NAT-regel voor het omzetten van alle binnenkomend verkeer op poort 3389 voor poort 3389 voor RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="59e92-159">a NAT rule to translate all incoming traffic on port 3389 to port 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="59e92-160">een NAT-regel voor het omzetten van alle binnenkomend verkeer op poort 3391 tot poort 3389 voor RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="59e92-160">a NAT rule to translate all incoming traffic on port 3391 to port 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="59e92-161">een load balancer-regel om al het verkeer dat binnenkomt op poort 80, gelijk te verdelen naar poort 80 op de adressen in de back-endgroep.</span><span class="sxs-lookup"><span data-stu-id="59e92-161">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>

<span data-ttu-id="59e92-162"><sup>1</sup> NAT-regels worden gekoppeld aan een specifiek exemplaar van een virtuele machine achter de load balancer.</span><span class="sxs-lookup"><span data-stu-id="59e92-162"><sup>1</sup> NAT rules are associated to a specific virtual machine instance behind the load balancer.</span></span> <span data-ttu-id="59e92-163">Het netwerkverkeer dat binnenkomt op poort 3389 is verzonden naar de specifieke virtuele machine en de poort die is gekoppeld aan de NAT-regel.</span><span class="sxs-lookup"><span data-stu-id="59e92-163">The network traffic arriving on port 3389 is sent to the specific virtual machine and port associated with the NAT rule.</span></span> <span data-ttu-id="59e92-164">U moet een protocol (UDP of TCP) voor een NAT-regel opgeven.</span><span class="sxs-lookup"><span data-stu-id="59e92-164">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="59e92-165">Beide protocollen kunnen niet worden toegewezen aan dezelfde poort.</span><span class="sxs-lookup"><span data-stu-id="59e92-165">Both protocols can't be assigned to the same port.</span></span>

1. <span data-ttu-id="59e92-166">De PowerShell-variabelen instellen</span><span class="sxs-lookup"><span data-stu-id="59e92-166">Set up the PowerShell variables</span></span>

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. <span data-ttu-id="59e92-167">Maken van de test</span><span class="sxs-lookup"><span data-stu-id="59e92-167">Create the probe</span></span>

    <span data-ttu-id="59e92-168">Het volgende voorbeeld wordt elke 15 seconden gemaakt TCP voor een test waarmee wordt gecontroleerd of de verbinding met de back-end TCP-poort 80.</span><span class="sxs-lookup"><span data-stu-id="59e92-168">The following example creates a TCP probe that checks for connectivity to back-end TCP port 80 every 15 seconds.</span></span> <span data-ttu-id="59e92-169">Het markeert u de back-end-bron niet beschikbaar na twee achtereenvolgende mislukte pogingen.</span><span class="sxs-lookup"><span data-stu-id="59e92-169">It will mark the back-end resource unavailable after two consecutive failures.</span></span>

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. <span data-ttu-id="59e92-170">Binnenkomende NAT-regels waarmee de RDP-verbindingen met de back-end-bronnen maken</span><span class="sxs-lookup"><span data-stu-id="59e92-170">Create inbound NAT rules that allow RDP connections to the back-end resources</span></span>

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. <span data-ttu-id="59e92-171">Regels die verkeer naar andere back-end-poorten verzenden, afhankelijk van welke front-end heeft de aanvraag ontvangen voor een load balancer maken</span><span class="sxs-lookup"><span data-stu-id="59e92-171">Create a load balancer rules that send traffic to different back-end ports depending on which front end received the request</span></span>

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. <span data-ttu-id="59e92-172">Controleer uw instellingen</span><span class="sxs-lookup"><span data-stu-id="59e92-172">Check your settings</span></span>

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    <span data-ttu-id="59e92-173">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="59e92-173">Expected output:</span></span>

        info:    Executing command network lb show
        info:    Looking up the load balancer "myIPv4IPv6Lb"
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

## <a name="create-nics"></a><span data-ttu-id="59e92-174">NIC's maken</span><span class="sxs-lookup"><span data-stu-id="59e92-174">Create NICs</span></span>

<span data-ttu-id="59e92-175">NIC's maken en deze koppelt aan de NAT-regels, load balancer-regels en -tests.</span><span class="sxs-lookup"><span data-stu-id="59e92-175">Create NICs and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="59e92-176">De PowerShell-variabelen instellen</span><span class="sxs-lookup"><span data-stu-id="59e92-176">Set up the PowerShell variables</span></span>

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

2. <span data-ttu-id="59e92-177">Maken van een NIC voor elke back-end en een IPv6-configuratie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="59e92-177">Create a NIC for each back-end and add an IPv6 configuration.</span></span>

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-the-back-end-vm-resources-and-attach-each-nic"></a><span data-ttu-id="59e92-178">Maken van de back-end-VM-netwerkbronnen en elke NIC koppelen</span><span class="sxs-lookup"><span data-stu-id="59e92-178">Create the back-end VM resources and attach each NIC</span></span>

<span data-ttu-id="59e92-179">Voor het maken van virtuele machines, moet u een opslagaccount hebben.</span><span class="sxs-lookup"><span data-stu-id="59e92-179">To create VMs, you must have a storage account.</span></span> <span data-ttu-id="59e92-180">De virtuele machines moeten lid zijn van een beschikbaarheidsset voor load balancing.</span><span class="sxs-lookup"><span data-stu-id="59e92-180">For load balancing, the VMs need to be members of an availability set.</span></span> <span data-ttu-id="59e92-181">Zie voor meer informatie over het maken van virtuele machines [maken van een virtuele machine in Azure met behulp van PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="59e92-181">For more information about creating VMs, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="59e92-182">De PowerShell-variabelen instellen</span><span class="sxs-lookup"><span data-stu-id="59e92-182">Set up the PowerShell variables</span></span>

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
    > <span data-ttu-id="59e92-183">Dit voorbeeld wordt de gebruikersnaam en het wachtwoord voor de virtuele machines in ongecodeerde tekst.</span><span class="sxs-lookup"><span data-stu-id="59e92-183">This example uses the username and password for the VMs in clear text.</span></span> <span data-ttu-id="59e92-184">Juiste Wees voorzichtig bij het gebruik van referenties in de wissen.</span><span class="sxs-lookup"><span data-stu-id="59e92-184">Appropriate care must be taken when using credentials in the clear.</span></span> <span data-ttu-id="59e92-185">Zie voor een veiligere methode afhandelen van referenties in PowerShell de [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="59e92-185">For a more secure method of handling credentials in PowerShell, see the [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

2. <span data-ttu-id="59e92-186">De set met storage-account en beschikbaarheid maken</span><span class="sxs-lookup"><span data-stu-id="59e92-186">Create the storage account and availability set</span></span>

    <span data-ttu-id="59e92-187">U mag een bestaand opslagaccount gebruiken bij het maken van de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="59e92-187">You may use an existing storage account when you create the VMs.</span></span> <span data-ttu-id="59e92-188">De volgende opdracht maakt een nieuw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="59e92-188">The following command creates a new storage account.</span></span>

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    <span data-ttu-id="59e92-189">Maak vervolgens de beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="59e92-189">Next, create the availability set.</span></span>

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. <span data-ttu-id="59e92-190">De virtuele machines maken met de gekoppelde NIC 's</span><span class="sxs-lookup"><span data-stu-id="59e92-190">Create the virtual machines with the associated NICs</span></span>

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a><span data-ttu-id="59e92-191">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="59e92-191">Next steps</span></span>

[<span data-ttu-id="59e92-192">Aan de slag met het configureren van een interne load balancer</span><span class="sxs-lookup"><span data-stu-id="59e92-192">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="59e92-193">Een distributiemodus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="59e92-193">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="59e92-194">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="59e92-194">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
