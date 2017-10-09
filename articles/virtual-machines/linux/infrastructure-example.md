---
title: Overzicht van Azure-infrastructuur aaaExample | Microsoft Docs
description: Meer informatie over Hallo belangrijke ontwerp- en implementatiestappen richtlijnen voor het implementeren van een voorbeeld van de infrastructuur in Azure.
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 281fc2c0-b533-45fa-81a3-728c0049c73d
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6b307c0112203aa83e1fada81966fc265397a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-linux-vms"></a><span data-ttu-id="5c16d-103">Voorbeeld van de Azure-infrastructuur overzicht voor virtuele Linux-machines</span><span class="sxs-lookup"><span data-stu-id="5c16d-103">Example Azure infrastructure walkthrough for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="5c16d-104">In dit artikel wordt uitgelegd opzetten van een voorbeeld van de toepassing-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="5c16d-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="5c16d-105">We beschreven ontwerpen van een infrastructuur voor een eenvoudige online winkel die alle Hallo richtlijnen en beslissingen rond naamconventies, beschikbaarheidssets, virtuele netwerken en taakverdelers samenbrengt en distribueren van uw virtuele machines (VM's).</span><span class="sxs-lookup"><span data-stu-id="5c16d-105">We detail designing an infrastructure for a simple on-line store that brings together all hello guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="5c16d-106">Voorbeeld van de werkbelasting</span><span class="sxs-lookup"><span data-stu-id="5c16d-106">Example workload</span></span>
<span data-ttu-id="5c16d-107">Adventure Works Cycles wil toobuild een online store-toepassing in Azure die bestaat uit:</span><span class="sxs-lookup"><span data-stu-id="5c16d-107">Adventure Works Cycles wants toobuild an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="5c16d-108">Twee nginx-servers uitvoeren in de weblaag van een-front-Hallo-client</span><span class="sxs-lookup"><span data-stu-id="5c16d-108">Two nginx servers running hello client front-end in a web tier</span></span>
* <span data-ttu-id="5c16d-109">Twee nginx-servers verwerken van gegevens en bestellingen in de toepassingslaag van een</span><span class="sxs-lookup"><span data-stu-id="5c16d-109">Two nginx servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="5c16d-110">Twee servers van MongoDB-onderdeel van een shard cluster voor het opslaan van productgegevens- en bestellingen in een databaselaag</span><span class="sxs-lookup"><span data-stu-id="5c16d-110">Two MongoDB servers part of a sharded cluster for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="5c16d-111">Twee Active Directory-domeincontrollers voor klantaccounts en leveranciers in een verificatie-laag</span><span class="sxs-lookup"><span data-stu-id="5c16d-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="5c16d-112">Alle Hallo-servers bevinden zich in twee subnetten:</span><span class="sxs-lookup"><span data-stu-id="5c16d-112">All hello servers are located in two subnets:</span></span>
  * <span data-ttu-id="5c16d-113">een front-end-subnet voor webservers Hallo</span><span class="sxs-lookup"><span data-stu-id="5c16d-113">a front-end subnet for hello web servers</span></span> 
  * <span data-ttu-id="5c16d-114">een back-end-subnet voor toepassingsservers hello, MongoDB-cluster en domeincontrollers</span><span class="sxs-lookup"><span data-stu-id="5c16d-114">a back-end subnet for hello application servers, MongoDB cluster, and domain controllers</span></span>

![Diagram van verschillende lagen voor de infrastructuur van de toepassing](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="5c16d-116">Binnenkomende beveiligde webverkeer moet Netwerktaakverdeling tussen Hallo webservers als klanten Hallo online winkel bladeren.</span><span class="sxs-lookup"><span data-stu-id="5c16d-116">Incoming secure web traffic must be load-balanced among hello web servers as customers browse hello on-line store.</span></span> <span data-ttu-id="5c16d-117">Volgorde Hallo vorm van HTTP-verkeer verwerken van aanvragen van Hallo web servers moeten worden verdeeld tussen Hallo toepassingsservers.</span><span class="sxs-lookup"><span data-stu-id="5c16d-117">Order processing traffic in hello form of HTTP requests from hello web servers must be load-balanced among hello application servers.</span></span> <span data-ttu-id="5c16d-118">Bovendien moet Hallo-infrastructuur zijn ontworpen voor hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="5c16d-118">Additionally, hello infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="5c16d-119">Hallo resulterende ontwerp moet gebruikmaken van:</span><span class="sxs-lookup"><span data-stu-id="5c16d-119">hello resulting design must incorporate:</span></span>

* <span data-ttu-id="5c16d-120">Een Azure-abonnement en -account</span><span class="sxs-lookup"><span data-stu-id="5c16d-120">An Azure subscription and account</span></span>
* <span data-ttu-id="5c16d-121">Één resourcegroep</span><span class="sxs-lookup"><span data-stu-id="5c16d-121">A single resource group</span></span>
* <span data-ttu-id="5c16d-122">Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="5c16d-122">Azure Managed Disks</span></span>
* <span data-ttu-id="5c16d-123">Een virtueel netwerk met twee subnetten</span><span class="sxs-lookup"><span data-stu-id="5c16d-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="5c16d-124">Beschikbaarheidssets voor Hallo virtuele machines met een vergelijkbare rol</span><span class="sxs-lookup"><span data-stu-id="5c16d-124">Availability sets for hello VMs with a similar role</span></span>
* <span data-ttu-id="5c16d-125">Virtuele machines</span><span class="sxs-lookup"><span data-stu-id="5c16d-125">Virtual machines</span></span>

<span data-ttu-id="5c16d-126">Alle bovenstaande Hallo voldoen aan deze naamgeving:</span><span class="sxs-lookup"><span data-stu-id="5c16d-126">All hello above follow these naming conventions:</span></span>

* <span data-ttu-id="5c16d-127">Adventure Works Cycles gebruikt **[IT werkbelasting]-[locatie]-[Azure resource]** als voorvoegsel</span><span class="sxs-lookup"><span data-stu-id="5c16d-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="5c16d-128">Bijvoorbeeld, "**azos**' (Azure Online Store) is de naam van de IT-werkbelasting Hallo en '**gebruiken**' (VS-Oost 2) is Hallo locatie</span><span class="sxs-lookup"><span data-stu-id="5c16d-128">For this example, "**azos**" (Azure On-line Store) is hello IT workload name and "**use**" (East US 2) is hello location</span></span>
* <span data-ttu-id="5c16d-129">Virtuele netwerken maken gebruik van AZOS-gebruik-VN**[aantal]**</span><span class="sxs-lookup"><span data-stu-id="5c16d-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="5c16d-130">Beschikbaarheidssets gebruiken azos-gebruiken-als-**[rol]**</span><span class="sxs-lookup"><span data-stu-id="5c16d-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="5c16d-131">Namen van de virtuele machine gebruiken azos-gebruiken-vm -**[vmname]**</span><span class="sxs-lookup"><span data-stu-id="5c16d-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="5c16d-132">Azure-abonnementen en accounts</span><span class="sxs-lookup"><span data-stu-id="5c16d-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="5c16d-133">Adventure Works Cycles maakt gebruik van de Enterprise-abonnement, met de naam Adventure Works Enterprise-abonnement, tooprovide facturering voor deze IT-werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="5c16d-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, tooprovide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="5c16d-134">Storage</span><span class="sxs-lookup"><span data-stu-id="5c16d-134">Storage</span></span>
<span data-ttu-id="5c16d-135">Adventure Works Cycles bepaald dat ze beheerd Azure-schijven moeten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5c16d-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="5c16d-136">Bij het maken van virtuele machines worden beide beschikbare opslag opslaglagen gebruikt:</span><span class="sxs-lookup"><span data-stu-id="5c16d-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="5c16d-137">**Standard-opslag** voor webservers hello, toepassingsservers, en domeincontrollers en hun gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="5c16d-137">**Standard storage** for hello web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="5c16d-138">**Premium-opslag** voor Hallo MongoDB shard clusterservers en hun gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="5c16d-138">**Premium storage** for hello MongoDB sharded cluster servers and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="5c16d-139">Virtueel netwerk en subnetten</span><span class="sxs-lookup"><span data-stu-id="5c16d-139">Virtual network and subnets</span></span>
<span data-ttu-id="5c16d-140">Omdat Hallo virtueel netwerk niet nodig heeft voor lopende connectiviteit toohello Adventure werk cycli on-premises netwerk, worden ze besloten op een virtueel netwerk alleen in de cloud.</span><span class="sxs-lookup"><span data-stu-id="5c16d-140">Because hello virtual network does not need ongoing connectivity toohello Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="5c16d-141">Ze een virtueel netwerk alleen in de cloud gemaakt met de Hallo-instellingen met hello Azure-portal te volgen:</span><span class="sxs-lookup"><span data-stu-id="5c16d-141">They created a cloud-only virtual network with hello following settings using hello Azure portal:</span></span>

* <span data-ttu-id="5c16d-142">Naam: AZOS gebruik VN01</span><span class="sxs-lookup"><span data-stu-id="5c16d-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="5c16d-143">Locatie: VS-Oost 2</span><span class="sxs-lookup"><span data-stu-id="5c16d-143">Location: East US 2</span></span>
* <span data-ttu-id="5c16d-144">Adresruimte virtuele netwerk: 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="5c16d-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="5c16d-145">Eerste subnet:</span><span class="sxs-lookup"><span data-stu-id="5c16d-145">First subnet:</span></span>
  * <span data-ttu-id="5c16d-146">Naam: FrontEnd</span><span class="sxs-lookup"><span data-stu-id="5c16d-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="5c16d-147">Adresruimte: 10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="5c16d-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="5c16d-148">Tweede subnet:</span><span class="sxs-lookup"><span data-stu-id="5c16d-148">Second subnet:</span></span>
  * <span data-ttu-id="5c16d-149">Naam: back-end</span><span class="sxs-lookup"><span data-stu-id="5c16d-149">Name: BackEnd</span></span>
  * <span data-ttu-id="5c16d-150">Adresruimte: 10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="5c16d-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="5c16d-151">Beschikbaarheidssets</span><span class="sxs-lookup"><span data-stu-id="5c16d-151">Availability sets</span></span>
<span data-ttu-id="5c16d-152">toomaintain hoge beschikbaarheid van alle vier lagen van de online winkel, Adventure Works Cycles genomen over de vier beschikbaarheidssets:</span><span class="sxs-lookup"><span data-stu-id="5c16d-152">toomaintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="5c16d-153">**azos gebruik als web** voor webservers Hallo</span><span class="sxs-lookup"><span data-stu-id="5c16d-153">**azos-use-as-web** for hello web servers</span></span>
* <span data-ttu-id="5c16d-154">**azos gebruik als app** voor toepassingsservers Hallo</span><span class="sxs-lookup"><span data-stu-id="5c16d-154">**azos-use-as-app** for hello application servers</span></span>
* <span data-ttu-id="5c16d-155">**azos gebruik als db** voor Hallo-servers in de shard hello MongoDB-cluster</span><span class="sxs-lookup"><span data-stu-id="5c16d-155">**azos-use-as-db** for hello servers in hello MongoDB sharded cluster</span></span>
* <span data-ttu-id="5c16d-156">**azos gebruik als dc** voor Hallo-domeincontrollers</span><span class="sxs-lookup"><span data-stu-id="5c16d-156">**azos-use-as-dc** for hello domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="5c16d-157">Virtuele machines</span><span class="sxs-lookup"><span data-stu-id="5c16d-157">Virtual machines</span></span>
<span data-ttu-id="5c16d-158">Adventure Works Cycles besloten op Hallo namen voor hun virtuele Azure-machines te volgen:</span><span class="sxs-lookup"><span data-stu-id="5c16d-158">Adventure Works Cycles decided on hello following names for their Azure VMs:</span></span>

* <span data-ttu-id="5c16d-159">**azos, gebruik, vm, web01** voor de eerste webserver Hallo</span><span class="sxs-lookup"><span data-stu-id="5c16d-159">**azos-use-vm-web01** for hello first web server</span></span>
* <span data-ttu-id="5c16d-160">**azos, gebruik, vm, web02** voor de tweede webserver Hallo</span><span class="sxs-lookup"><span data-stu-id="5c16d-160">**azos-use-vm-web02** for hello second web server</span></span>
* <span data-ttu-id="5c16d-161">**azos, gebruik, vm, app01** voor de eerste toepassingsserver Hallo</span><span class="sxs-lookup"><span data-stu-id="5c16d-161">**azos-use-vm-app01** for hello first application server</span></span>
* <span data-ttu-id="5c16d-162">**azos, gebruik, vm, app02** voor de tweede toepassingsserver Hallo</span><span class="sxs-lookup"><span data-stu-id="5c16d-162">**azos-use-vm-app02** for hello second application server</span></span>
* <span data-ttu-id="5c16d-163">**azos, gebruik, vm, db01** voor Hallo eerste MongoDB-server in het Hallo-cluster</span><span class="sxs-lookup"><span data-stu-id="5c16d-163">**azos-use-vm-db01** for hello first MongoDB server in hello cluster</span></span>
* <span data-ttu-id="5c16d-164">**azos, gebruik, vm, db02** voor Hallo tweede MongoDB-server in het Hallo-cluster</span><span class="sxs-lookup"><span data-stu-id="5c16d-164">**azos-use-vm-db02** for hello second MongoDB server in hello cluster</span></span>
* <span data-ttu-id="5c16d-165">**azos, gebruik, vm, dc01** voor de eerste domeincontroller Hallo</span><span class="sxs-lookup"><span data-stu-id="5c16d-165">**azos-use-vm-dc01** for hello first domain controller</span></span>
* <span data-ttu-id="5c16d-166">**azos, gebruik, vm, dc02** op Hallo tweede domeincontroller</span><span class="sxs-lookup"><span data-stu-id="5c16d-166">**azos-use-vm-dc02** for hello second domain controller</span></span>

<span data-ttu-id="5c16d-167">Hier wordt de resulterende configuratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="5c16d-167">Here is hello resulting configuration.</span></span>

![Laatste infrastructuur geïmplementeerd in Azure](./media/infrastructure-example/example-config.png)

<span data-ttu-id="5c16d-169">Deze configuratie omvat:</span><span class="sxs-lookup"><span data-stu-id="5c16d-169">This configuration incorporates:</span></span>

* <span data-ttu-id="5c16d-170">Een virtueel netwerk met twee subnetten (FrontEnd en BackEnd) alleen in de cloud</span><span class="sxs-lookup"><span data-stu-id="5c16d-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="5c16d-171">Azure-beheerde schijven die met behulp van standaard- en Premium-schijven</span><span class="sxs-lookup"><span data-stu-id="5c16d-171">Azure Managed Disks using both Standard and Premium disks</span></span>
* <span data-ttu-id="5c16d-172">Vier beschikbaarheidssets, één voor elke laag van de online winkel Hallo</span><span class="sxs-lookup"><span data-stu-id="5c16d-172">Four availability sets, one for each tier of hello on-line store</span></span>
* <span data-ttu-id="5c16d-173">Hallo virtuele machines voor Hallo vier lagen</span><span class="sxs-lookup"><span data-stu-id="5c16d-173">hello virtual machines for hello four tiers</span></span>
* <span data-ttu-id="5c16d-174">Een externe set met gelijke taakverdeling voor HTTPS-gebaseerde internetverkeer van Hallo Internet toohello webservers</span><span class="sxs-lookup"><span data-stu-id="5c16d-174">An external load balanced set for HTTPS-based web traffic from hello Internet toohello web servers</span></span>
* <span data-ttu-id="5c16d-175">Een interne set voor niet-versleuteld webverkeer vanaf Hallo servers toohello Webtoepassingsservers met gelijke taakverdeling</span><span class="sxs-lookup"><span data-stu-id="5c16d-175">An internal load balanced set for unencrypted web traffic from hello web servers toohello application servers</span></span>
* <span data-ttu-id="5c16d-176">Één resourcegroep</span><span class="sxs-lookup"><span data-stu-id="5c16d-176">A single resource group</span></span>
