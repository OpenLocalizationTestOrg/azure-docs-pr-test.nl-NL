---
title: Overzicht van IPv6 voor Azure Load Balancer | Microsoft Docs
description: Understanding IPv6-ondersteuning voor Azure Load Balancer en taakverdeling virtuele machines.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: IPv6-, azure load balancer, dual-stack, openbare IP-adres, systeemeigen ipv6, mobiele, iot
ms.assetid: 6a1d583f-a305-40fd-a94b-fa42e1943bbb
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: 8cca857314ecf37ef51700fd25aef228515ecd0a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-ipv6-for-azure-load-balancer"></a><span data-ttu-id="82bea-104">Overzicht van IPv6 voor Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="82bea-104">Overview of IPv6 for Azure Load Balancer</span></span>

<span data-ttu-id="82bea-105">Internet gerichte load balancers kunnen worden geïmplementeerd met een IPv6-adres.</span><span class="sxs-lookup"><span data-stu-id="82bea-105">Internet-facing load balancers can be deployed with an IPv6 address.</span></span> <span data-ttu-id="82bea-106">Dit biedt de volgende mogelijkheden naast IPv4-verbindingen:</span><span class="sxs-lookup"><span data-stu-id="82bea-106">In addition to IPv4 connectivity, this enables the following capabilities:</span></span>

* <span data-ttu-id="82bea-107">Oorspronkelijke end-to-end IPv6-connectiviteit tussen het openbare Internet-clients en Azure Virtual Machines (VM's) via de load balancer.</span><span class="sxs-lookup"><span data-stu-id="82bea-107">Native end-to-end IPv6 connectivity between public Internet clients and Azure Virtual Machines (VMs) through the load balancer.</span></span>
* <span data-ttu-id="82bea-108">Systeemeigen end-to-end IPv6 uitgaande connectiviteit tussen virtuele machines en openbare clients voor Internet IPv6 is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="82bea-108">Native end-to-end IPv6 outbound connectivity between VMs and public Internet IPv6-enabled clients.</span></span>

<span data-ttu-id="82bea-109">De volgende afbeelding ziet u de IPv6-functionaliteit voor Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="82bea-109">The following picture illustrates the IPv6 functionality for Azure Load Balancer.</span></span>

![Azure Load Balancer met IPv6](./media/load-balancer-ipv6-overview/load-balancer-ipv6.png)

<span data-ttu-id="82bea-111">Zodra geïmplementeerd, kan een client IPv4 of IPv6-functionaliteit Internet communiceren met de openbare IPv4- of IPv6-adressen (of hostnamen) van de Azure Internet gerichte Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="82bea-111">Once deployed, an IPv4 or IPv6-enabled Internet client can communicate with the public IPv4 or IPv6 addresses (or hostnames) of the Azure Internet-facing Load Balancer.</span></span> <span data-ttu-id="82bea-112">De load balancer stuurt de IPv6-pakketten naar de persoonlijke IPv6-adressen van de virtuele machines met network address translation (NAT).</span><span class="sxs-lookup"><span data-stu-id="82bea-112">The load balancer routes the IPv6 packets to the private IPv6 addresses of the VMs using network address translation (NAT).</span></span> <span data-ttu-id="82bea-113">De IPv6-Internet-client communiceren niet rechtstreeks met het IPv6-adres van de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="82bea-113">The IPv6 Internet client cannot communicate directly with the IPv6 address of the VMs.</span></span>

## <a name="features"></a><span data-ttu-id="82bea-114">Functies</span><span class="sxs-lookup"><span data-stu-id="82bea-114">Features</span></span>

<span data-ttu-id="82bea-115">Systeemeigen IPv6-ondersteuning voor virtuele machines die zijn geïmplementeerd via Azure Resource Manager biedt:</span><span class="sxs-lookup"><span data-stu-id="82bea-115">Native IPv6 support for VMs deployed via Azure Resource Manager provides:</span></span>

1. <span data-ttu-id="82bea-116">Taakverdeling IPv6-services voor IPv6-clients op Internet</span><span class="sxs-lookup"><span data-stu-id="82bea-116">Load-balanced IPv6 services for IPv6 clients on the Internet</span></span>
2. <span data-ttu-id="82bea-117">Systeemeigen IPv6- en IPv4-eindpunten op virtuele machines ('dual gestapelde')</span><span class="sxs-lookup"><span data-stu-id="82bea-117">Native IPv6 and IPv4 endpoints on VMs ("dual stacked")</span></span>
3. <span data-ttu-id="82bea-118">Binnenkomende en uitgaande geïnitieerde systeemeigen IPv6-verbindingen</span><span class="sxs-lookup"><span data-stu-id="82bea-118">Inbound and outbound-initiated native IPv6 connections</span></span>
4. <span data-ttu-id="82bea-119">Ondersteunde protocollen zoals TCP, UDP- en HTTP (S) inschakelen een volledige reeks architecturen service</span><span class="sxs-lookup"><span data-stu-id="82bea-119">Supported protocols such as TCP, UDP, and HTTP(S) enable a full range of service architectures</span></span>

## <a name="benefits"></a><span data-ttu-id="82bea-120">Voordelen</span><span class="sxs-lookup"><span data-stu-id="82bea-120">Benefits</span></span>

<span data-ttu-id="82bea-121">Deze functionaliteit kunnen de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="82bea-121">This functionality enables the following key benefits:</span></span>

* <span data-ttu-id="82bea-122">Voldoen aan wettelijke voorschriften vereisen dat de nieuwe toepassingen toegankelijk voor clients met alleen IPv6 zijn</span><span class="sxs-lookup"><span data-stu-id="82bea-122">Meet government regulations requiring that new applications be accessible to IPv6-only clients</span></span>
* <span data-ttu-id="82bea-123">Schakel mobiele en Internet der dingen (IOT)-ontwikkelaars kunnen dual gestapelde (IPv4 + IPv6) Azure Virtual Machines gebruiken voor het oplossen van de groeiende mobile & IOT markten</span><span class="sxs-lookup"><span data-stu-id="82bea-123">Enable mobile and Internet of things (IOT) developers to use dual-stacked (IPv4+IPv6) Azure Virtual Machines to address the growing mobile & IOT markets</span></span>

## <a name="details-and-limitations"></a><span data-ttu-id="82bea-124">Meer informatie en beperkingen</span><span class="sxs-lookup"><span data-stu-id="82bea-124">Details and limitations</span></span>

<span data-ttu-id="82bea-125">Details</span><span class="sxs-lookup"><span data-stu-id="82bea-125">Details</span></span>

* <span data-ttu-id="82bea-126">De Azure DNS-service bevat zowel IPv4 A en AAAA IPv6-records van naam en reageert met beide records voor de load balancer.</span><span class="sxs-lookup"><span data-stu-id="82bea-126">The Azure DNS service contains both IPv4 A and IPv6 AAAA name records and responds with both records for the load balancer.</span></span> <span data-ttu-id="82bea-127">De client kiezen welk adres (IPv4 of IPv6) om te communiceren met.</span><span class="sxs-lookup"><span data-stu-id="82bea-127">The client chooses which address (IPv4 or IPv6) to communicate with.</span></span>
* <span data-ttu-id="82bea-128">Wanneer een virtuele machine een verbinding met een openbaar Internet IPv6 verbonden apparaat initieert, is IPv6-adres van de VM-bron netwerkadres vertaald (NAT) naar het openbare IPv6-adres van de load balancer.</span><span class="sxs-lookup"><span data-stu-id="82bea-128">When a VM initiates a connection to a public Internet IPv6-connected device, the VM's source IPv6 address is network address translated (NAT) to the public IPv6 address of the load balancer.</span></span>
* <span data-ttu-id="82bea-129">Virtuele machines met Linux-besturingssysteem moeten worden geconfigureerd voor het ontvangen van een IPv6-IP-adres via DHCP.</span><span class="sxs-lookup"><span data-stu-id="82bea-129">VMs running the Linux operating system must be configured to receive an IPv6 IP address via DHCP.</span></span> <span data-ttu-id="82bea-130">Veel van de Linux-afbeeldingen in de galerie van Azure zijn al geconfigureerd voor ondersteuning voor IPv6 zonder aanpassing.</span><span class="sxs-lookup"><span data-stu-id="82bea-130">Many of the Linux images in the Azure Gallery are already configured to support IPv6 without modification.</span></span> <span data-ttu-id="82bea-131">Zie voor meer informatie [DHCPv6 configureren voor virtuele Linux-machines](load-balancer-ipv6-for-linux.md)</span><span class="sxs-lookup"><span data-stu-id="82bea-131">For more information, see [Configuring DHCPv6 for Linux VMs](load-balancer-ipv6-for-linux.md)</span></span>
* <span data-ttu-id="82bea-132">Als u kiest voor het gebruik van een health test met de load balancer, een IPv4-test maken en deze gebruiken met de IPv4- als IPv6-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="82bea-132">If you choose to use a health probe with your load balancer, create an IPv4 probe and use it with both the IPv4 and IPv6 endpoints.</span></span> <span data-ttu-id="82bea-133">Als de service op de virtuele machine uitgeschakeld wordt, worden zowel de IPv4- als IPv6-eindpunten buiten rotatie genomen.</span><span class="sxs-lookup"><span data-stu-id="82bea-133">If the service on your VM goes down, both the IPv4 and IPv6 endpoints are taken out of rotation.</span></span>

<span data-ttu-id="82bea-134">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="82bea-134">Limitations</span></span>

* <span data-ttu-id="82bea-135">U kunt geen regels voor taakverdeling IPv6 toevoegen in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="82bea-135">You cannot add IPv6 load balancing rules in the Azure portal.</span></span> <span data-ttu-id="82bea-136">De regels kunnen alleen worden gemaakt via de sjabloon, CLI, PowerShell.</span><span class="sxs-lookup"><span data-stu-id="82bea-136">The rules can only be created through the template, CLI, PowerShell.</span></span>
* <span data-ttu-id="82bea-137">U kunt geen upgrade van bestaande virtuele machines voor het gebruik van IPv6-adressen.</span><span class="sxs-lookup"><span data-stu-id="82bea-137">You may not upgrade existing VMs to use IPv6 addresses.</span></span> <span data-ttu-id="82bea-138">U kunt nieuwe virtuele machines moet implementeren.</span><span class="sxs-lookup"><span data-stu-id="82bea-138">You must deploy new VMs.</span></span>
* <span data-ttu-id="82bea-139">Één IPv6-adres kan worden toegewezen aan één netwerkinterface in elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="82bea-139">A single IPv6 address can be assigned to a single network interface in each VM.</span></span>
* <span data-ttu-id="82bea-140">De openbare IPv6-adressen kunnen niet worden toegewezen aan een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="82bea-140">The public IPv6 addresses cannot be assigned to a VM.</span></span> <span data-ttu-id="82bea-141">Ze kunnen alleen worden toegewezen aan een load balancer.</span><span class="sxs-lookup"><span data-stu-id="82bea-141">They can only be assigned to a load balancer.</span></span>
* <span data-ttu-id="82bea-142">U kunt de reverse DNS-lookup niet configureren voor uw openbare IPv6-adressen.</span><span class="sxs-lookup"><span data-stu-id="82bea-142">You cannot configure the reverse DNS lookup for your public IPv6 addresses.</span></span>
* <span data-ttu-id="82bea-143">De virtuele machines met het IPv6-adressen kunnen niet lid zijn van een Azure Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="82bea-143">The VMs with the IPv6 addresses cannot be members of an Azure Cloud Service.</span></span> <span data-ttu-id="82bea-144">Ze kunnen worden verbonden met een Azure-netwerk (VNet) en communiceren met elkaar via hun IPv4-adressen.</span><span class="sxs-lookup"><span data-stu-id="82bea-144">They can be connected to an Azure Virtual Network (VNet) and communicate with each other over their IPv4 addresses.</span></span>
* <span data-ttu-id="82bea-145">Persoonlijke IPv6-adressen kunnen worden geïmplementeerd op afzonderlijke virtuele machines in een resourcegroep, maar kunnen niet worden geïmplementeerd in een resourcegroep via-Schaalsets.</span><span class="sxs-lookup"><span data-stu-id="82bea-145">Private IPv6 addresses can be deployed on individual VMs in a resource group but cannot be deployed into a resource group via Scale Sets.</span></span>
* <span data-ttu-id="82bea-146">Virtuele machines in Azure kunnen geen verbinding maken via IPv6 op andere virtuele machines, andere Azure-services of on-premises apparaten.</span><span class="sxs-lookup"><span data-stu-id="82bea-146">Azure VMs cannot connect over IPv6 to other VMs, other Azure services, or on-premises devices.</span></span> <span data-ttu-id="82bea-147">Ze kunnen alleen de Azure load balancer communiceren via IPv6.</span><span class="sxs-lookup"><span data-stu-id="82bea-147">They can only communicate with the Azure load balancer over IPv6.</span></span> <span data-ttu-id="82bea-148">Ze kunnen echter communiceren met deze andere resources met behulp van IPv4.</span><span class="sxs-lookup"><span data-stu-id="82bea-148">However, they can communicate with these other resources using IPv4.</span></span>
* <span data-ttu-id="82bea-149">Beveiliging van de Netwerkbeveiligingsgroep (NSG) voor IPv4 wordt ondersteund in implementaties van dual stack (IPv4 + IPv6).</span><span class="sxs-lookup"><span data-stu-id="82bea-149">Network Security Group (NSG) protection for IPv4 is supported in dual-stack (IPv4+IPv6) deployments.</span></span> <span data-ttu-id="82bea-150">Nsg's niet van toepassing op de IPv6-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="82bea-150">NSGs do not apply to the IPv6 endpoints.</span></span>
* <span data-ttu-id="82bea-151">Het IPv6-eindpunt op de virtuele machine is niet rechtstreeks blootgesteld aan internet.</span><span class="sxs-lookup"><span data-stu-id="82bea-151">The IPv6 endpoint on the VM is not exposed directly to the internet.</span></span> <span data-ttu-id="82bea-152">Het is achter een load balancer.</span><span class="sxs-lookup"><span data-stu-id="82bea-152">It is behind a load balancer.</span></span> <span data-ttu-id="82bea-153">Alleen de poorten die zijn opgegeven in de load balancer-regels zijn toegankelijk via IPv6.</span><span class="sxs-lookup"><span data-stu-id="82bea-153">Only the ports specified in the load balancer rules are accessible over IPv6.</span></span>
* <span data-ttu-id="82bea-154">Wijzigen van de parameter IdleTimeout voor IPv6 **momenteel niet ondersteund**.</span><span class="sxs-lookup"><span data-stu-id="82bea-154">Changing the IdleTimeout parameter for IPv6 is **currently not supported**.</span></span> <span data-ttu-id="82bea-155">De standaardwaarde is vier minuten.</span><span class="sxs-lookup"><span data-stu-id="82bea-155">The default is four minutes.</span></span>
* <span data-ttu-id="82bea-156">Wijzigen van de parameter loadDistributionMethod voor IPv6 **momenteel niet ondersteund**.</span><span class="sxs-lookup"><span data-stu-id="82bea-156">Changing the loadDistributionMethod parameter for IPv6 is **currently not supported**.</span></span>
* <span data-ttu-id="82bea-157">Gereserveerd IP-IPv6-adressen (waarbij IPAllocationMethod = statisch) zijn **momenteel niet ondersteund**.</span><span class="sxs-lookup"><span data-stu-id="82bea-157">Reserved IPv6 IPs (where IPAllocationMethod = static) are **currently not supported**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82bea-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="82bea-158">Next steps</span></span>

<span data-ttu-id="82bea-159">Informatie over het implementeren van een load balancer met IPv6.</span><span class="sxs-lookup"><span data-stu-id="82bea-159">Learn how to deploy a load balancer with IPv6.</span></span>

* [<span data-ttu-id="82bea-160">Beschikbaarheid van IPv6 per regio</span><span class="sxs-lookup"><span data-stu-id="82bea-160">Availability of IPv6 by region</span></span>](https://go.microsoft.com/fwlink/?linkid=828357)
* [<span data-ttu-id="82bea-161">Een load balancer met IPv6 met een sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="82bea-161">Deploy a load balancer with IPv6 using a template</span></span>](load-balancer-ipv6-internet-template.md)
* [<span data-ttu-id="82bea-162">Implementeren van een load balancer met IPv6 met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="82bea-162">Deploy a load balancer with IPv6 using Azure PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
* [<span data-ttu-id="82bea-163">Implementeren van een load balancer met IPv6 met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="82bea-163">Deploy a load balancer with IPv6 using Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
