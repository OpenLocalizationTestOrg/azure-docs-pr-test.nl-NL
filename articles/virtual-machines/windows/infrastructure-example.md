---
title: Overzicht van Azure-infrastructuur aaaExample | Microsoft Docs
description: Meer informatie over Hallo belangrijke ontwerp- en implementatiestappen richtlijnen voor het implementeren van een voorbeeld van de infrastructuur in Azure.
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7032b586-e4e5-4954-952f-fdfc03fc1980
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd6b6e904404bea0b5be37dfce6d60039daae636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-windows-vms"></a><span data-ttu-id="000ce-103">Voorbeeld van de Azure-infrastructuur overzicht voor het Windows-VM 's</span><span class="sxs-lookup"><span data-stu-id="000ce-103">Example Azure infrastructure walkthrough for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="000ce-104">In dit artikel wordt uitgelegd opzetten van een voorbeeld van de toepassing-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="000ce-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="000ce-105">We beschreven ontwerpen van een infrastructuur voor een eenvoudige online winkel die alle Hallo richtlijnen en beslissingen rond naamconventies, beschikbaarheidssets, virtuele netwerken en taakverdelers samenbrengt en distribueren van uw virtuele machines (VM's).</span><span class="sxs-lookup"><span data-stu-id="000ce-105">We detail designing an infrastructure for a simple on-line store that brings together all hello guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="000ce-106">Voorbeeld van de werkbelasting</span><span class="sxs-lookup"><span data-stu-id="000ce-106">Example workload</span></span>
<span data-ttu-id="000ce-107">Adventure Works Cycles wil toobuild een online store-toepassing in Azure die bestaat uit:</span><span class="sxs-lookup"><span data-stu-id="000ce-107">Adventure Works Cycles wants toobuild an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="000ce-108">Twee IIS-servers met Hallo client front-end in een weblaag</span><span class="sxs-lookup"><span data-stu-id="000ce-108">Two IIS servers running hello client front-end in a web tier</span></span>
* <span data-ttu-id="000ce-109">Twee IIS-servers verwerken van gegevens en bestellingen in de toepassingslaag van een</span><span class="sxs-lookup"><span data-stu-id="000ce-109">Two IIS servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="000ce-110">Twee exemplaren van Microsoft SQL Server met AlwaysOn availability groups (twee SQL-Servers en een meerderheid knooppunt witness) voor het opslaan van productgegevens- en bestellingen in een databaselaag</span><span class="sxs-lookup"><span data-stu-id="000ce-110">Two Microsoft SQL Server instances with AlwaysOn availability groups (two SQL Servers and a majority node witness) for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="000ce-111">Twee Active Directory-domeincontrollers voor klantaccounts en leveranciers in een verificatie-laag</span><span class="sxs-lookup"><span data-stu-id="000ce-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="000ce-112">Alle Hallo-servers bevinden zich in twee subnetten:</span><span class="sxs-lookup"><span data-stu-id="000ce-112">All hello servers are located in two subnets:</span></span>
  * <span data-ttu-id="000ce-113">een front-end-subnet voor webservers Hallo</span><span class="sxs-lookup"><span data-stu-id="000ce-113">a front-end subnet for hello web servers</span></span> 
  * <span data-ttu-id="000ce-114">een back-end-subnet voor toepassingsservers hello, SQL-cluster en domeincontrollers</span><span class="sxs-lookup"><span data-stu-id="000ce-114">a back-end subnet for hello application servers, SQL cluster, and domain controllers</span></span>

![Diagram van verschillende lagen voor de infrastructuur van de toepassing](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="000ce-116">Binnenkomende beveiligde webverkeer moet Netwerktaakverdeling tussen Hallo webservers als klanten Hallo online winkel bladeren.</span><span class="sxs-lookup"><span data-stu-id="000ce-116">Incoming secure web traffic must be load-balanced among hello web servers as customers browse hello on-line store.</span></span> <span data-ttu-id="000ce-117">Volgorde Hallo vorm van HTTP-verkeer verwerken van aanvragen van Hallo web servers moeten worden verdeeld tussen Hallo toepassingsservers.</span><span class="sxs-lookup"><span data-stu-id="000ce-117">Order processing traffic in hello form of HTTP requests from hello web servers must be balanced among hello application servers.</span></span> <span data-ttu-id="000ce-118">Bovendien moet Hallo-infrastructuur zijn ontworpen voor hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="000ce-118">Additionally, hello infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="000ce-119">Hallo resulterende ontwerp moet gebruikmaken van:</span><span class="sxs-lookup"><span data-stu-id="000ce-119">hello resulting design must incorporate:</span></span>

* <span data-ttu-id="000ce-120">Een Azure-abonnement en -account</span><span class="sxs-lookup"><span data-stu-id="000ce-120">An Azure subscription and account</span></span>
* <span data-ttu-id="000ce-121">Één resourcegroep</span><span class="sxs-lookup"><span data-stu-id="000ce-121">A single resource group</span></span>
* <span data-ttu-id="000ce-122">Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="000ce-122">Azure Managed Disks</span></span>
* <span data-ttu-id="000ce-123">Een virtueel netwerk met twee subnetten</span><span class="sxs-lookup"><span data-stu-id="000ce-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="000ce-124">Beschikbaarheidssets voor Hallo virtuele machines met een vergelijkbare rol</span><span class="sxs-lookup"><span data-stu-id="000ce-124">Availability sets for hello VMs with a similar role</span></span>
* <span data-ttu-id="000ce-125">Virtuele machines</span><span class="sxs-lookup"><span data-stu-id="000ce-125">Virtual machines</span></span>

<span data-ttu-id="000ce-126">Alle bovenstaande Hallo voldoen aan deze naamgeving:</span><span class="sxs-lookup"><span data-stu-id="000ce-126">All hello above follow these naming conventions:</span></span>

* <span data-ttu-id="000ce-127">Adventure Works Cycles gebruikt **[IT werkbelasting]-[locatie]-[Azure resource]** als voorvoegsel</span><span class="sxs-lookup"><span data-stu-id="000ce-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="000ce-128">Bijvoorbeeld, "**azos**' (Azure Online Store) is de naam van de IT-werkbelasting Hallo en '**gebruiken**' (VS-Oost 2) is Hallo locatie</span><span class="sxs-lookup"><span data-stu-id="000ce-128">For this example, "**azos**" (Azure On-line Store) is hello IT workload name and "**use**" (East US 2) is hello location</span></span>
* <span data-ttu-id="000ce-129">Virtuele netwerken maken gebruik van AZOS-gebruik-VN**[aantal]**</span><span class="sxs-lookup"><span data-stu-id="000ce-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="000ce-130">Beschikbaarheidssets gebruiken azos-gebruiken-als-**[rol]**</span><span class="sxs-lookup"><span data-stu-id="000ce-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="000ce-131">Namen van de virtuele machine gebruiken azos-gebruiken-vm -**[vmname]**</span><span class="sxs-lookup"><span data-stu-id="000ce-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="000ce-132">Azure-abonnementen en accounts</span><span class="sxs-lookup"><span data-stu-id="000ce-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="000ce-133">Adventure Works Cycles maakt gebruik van de Enterprise-abonnement, met de naam Adventure Works Enterprise-abonnement, tooprovide facturering voor deze IT-werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="000ce-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, tooprovide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="000ce-134">Storage</span><span class="sxs-lookup"><span data-stu-id="000ce-134">Storage</span></span>
<span data-ttu-id="000ce-135">Adventure Works Cycles bepaald dat ze beheerd Azure-schijven moeten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="000ce-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="000ce-136">Bij het maken van virtuele machines worden beide beschikbare opslag opslaglagen gebruikt:</span><span class="sxs-lookup"><span data-stu-id="000ce-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="000ce-137">**Standard-opslag** voor webservers hello, toepassingsservers, en domeincontrollers en hun gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="000ce-137">**Standard storage** for hello web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="000ce-138">**Premium-opslag** voor Hallo SQL Server-VM's en hun gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="000ce-138">**Premium storage** for hello SQL Server VMs and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="000ce-139">Virtueel netwerk en subnetten</span><span class="sxs-lookup"><span data-stu-id="000ce-139">Virtual network and subnets</span></span>
<span data-ttu-id="000ce-140">Omdat Hallo virtueel netwerk niet nodig heeft voor lopende connectiviteit toohello Adventure werk cycli on-premises netwerk, worden ze besloten op een virtueel netwerk alleen in de cloud.</span><span class="sxs-lookup"><span data-stu-id="000ce-140">Because hello virtual network does not need ongoing connectivity toohello Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="000ce-141">Ze een virtueel netwerk alleen in de cloud gemaakt met de Hallo-instellingen met hello Azure-portal te volgen:</span><span class="sxs-lookup"><span data-stu-id="000ce-141">They created a cloud-only virtual network with hello following settings using hello Azure portal:</span></span>

* <span data-ttu-id="000ce-142">Naam: AZOS gebruik VN01</span><span class="sxs-lookup"><span data-stu-id="000ce-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="000ce-143">Locatie: VS-Oost 2</span><span class="sxs-lookup"><span data-stu-id="000ce-143">Location: East US 2</span></span>
* <span data-ttu-id="000ce-144">Adresruimte virtuele netwerk: 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="000ce-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="000ce-145">Eerste subnet:</span><span class="sxs-lookup"><span data-stu-id="000ce-145">First subnet:</span></span>
  * <span data-ttu-id="000ce-146">Naam: FrontEnd</span><span class="sxs-lookup"><span data-stu-id="000ce-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="000ce-147">Adresruimte: 10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="000ce-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="000ce-148">Tweede subnet:</span><span class="sxs-lookup"><span data-stu-id="000ce-148">Second subnet:</span></span>
  * <span data-ttu-id="000ce-149">Naam: back-end</span><span class="sxs-lookup"><span data-stu-id="000ce-149">Name: BackEnd</span></span>
  * <span data-ttu-id="000ce-150">Adresruimte: 10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="000ce-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="000ce-151">Beschikbaarheidssets</span><span class="sxs-lookup"><span data-stu-id="000ce-151">Availability sets</span></span>
<span data-ttu-id="000ce-152">toomaintain hoge beschikbaarheid van alle vier lagen van de online winkel, Adventure Works Cycles genomen over de vier beschikbaarheidssets:</span><span class="sxs-lookup"><span data-stu-id="000ce-152">toomaintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="000ce-153">**azos gebruik als web** voor webservers Hallo</span><span class="sxs-lookup"><span data-stu-id="000ce-153">**azos-use-as-web** for hello web servers</span></span>
* <span data-ttu-id="000ce-154">**azos gebruik als app** voor toepassingsservers Hallo</span><span class="sxs-lookup"><span data-stu-id="000ce-154">**azos-use-as-app** for hello application servers</span></span>
* <span data-ttu-id="000ce-155">**azos gebruiken als sql** voor Hallo SQL-Servers</span><span class="sxs-lookup"><span data-stu-id="000ce-155">**azos-use-as-sql** for hello SQL Servers</span></span>
* <span data-ttu-id="000ce-156">**azos gebruik als dc** voor Hallo-domeincontrollers</span><span class="sxs-lookup"><span data-stu-id="000ce-156">**azos-use-as-dc** for hello domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="000ce-157">Virtuele machines</span><span class="sxs-lookup"><span data-stu-id="000ce-157">Virtual machines</span></span>
<span data-ttu-id="000ce-158">Adventure Works Cycles besloten op Hallo namen voor hun virtuele Azure-machines te volgen:</span><span class="sxs-lookup"><span data-stu-id="000ce-158">Adventure Works Cycles decided on hello following names for their Azure VMs:</span></span>

* <span data-ttu-id="000ce-159">**azos, gebruik, vm, web01** voor de eerste webserver Hallo</span><span class="sxs-lookup"><span data-stu-id="000ce-159">**azos-use-vm-web01** for hello first web server</span></span>
* <span data-ttu-id="000ce-160">**azos, gebruik, vm, web02** voor de tweede webserver Hallo</span><span class="sxs-lookup"><span data-stu-id="000ce-160">**azos-use-vm-web02** for hello second web server</span></span>
* <span data-ttu-id="000ce-161">**azos, gebruik, vm, app01** voor de eerste toepassingsserver Hallo</span><span class="sxs-lookup"><span data-stu-id="000ce-161">**azos-use-vm-app01** for hello first application server</span></span>
* <span data-ttu-id="000ce-162">**azos, gebruik, vm, app02** voor de tweede toepassingsserver Hallo</span><span class="sxs-lookup"><span data-stu-id="000ce-162">**azos-use-vm-app02** for hello second application server</span></span>
* <span data-ttu-id="000ce-163">**azos, gebruik, vm, sql01** voor Hallo eerste SQL Server-server in het Hallo-cluster</span><span class="sxs-lookup"><span data-stu-id="000ce-163">**azos-use-vm-sql01** for hello first SQL Server server in hello cluster</span></span>
* <span data-ttu-id="000ce-164">**azos, gebruik, vm, sql02** voor Hallo tweede SQL Server-server in het Hallo-cluster</span><span class="sxs-lookup"><span data-stu-id="000ce-164">**azos-use-vm-sql02** for hello second SQL Server server in hello cluster</span></span>
* <span data-ttu-id="000ce-165">**azos, gebruik, vm, dc01** voor de eerste domeincontroller Hallo</span><span class="sxs-lookup"><span data-stu-id="000ce-165">**azos-use-vm-dc01** for hello first domain controller</span></span>
* <span data-ttu-id="000ce-166">**azos, gebruik, vm, dc02** op Hallo tweede domeincontroller</span><span class="sxs-lookup"><span data-stu-id="000ce-166">**azos-use-vm-dc02** for hello second domain controller</span></span>

<span data-ttu-id="000ce-167">Hier wordt de resulterende configuratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="000ce-167">Here is hello resulting configuration.</span></span>

![Laatste infrastructuur geïmplementeerd in Azure](./media/infrastructure-example/example-config.png)

<span data-ttu-id="000ce-169">Deze configuratie omvat:</span><span class="sxs-lookup"><span data-stu-id="000ce-169">This configuration incorporates:</span></span>

* <span data-ttu-id="000ce-170">Een virtueel netwerk met twee subnetten (FrontEnd en BackEnd) alleen in de cloud</span><span class="sxs-lookup"><span data-stu-id="000ce-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="000ce-171">Azure-beheerde schijven met standaard- en Premium-schijven</span><span class="sxs-lookup"><span data-stu-id="000ce-171">Azure Managed Disks with both Standard and Premium disks</span></span>
* <span data-ttu-id="000ce-172">Vier beschikbaarheidssets, één voor elke laag van de online winkel Hallo</span><span class="sxs-lookup"><span data-stu-id="000ce-172">Four availability sets, one for each tier of hello on-line store</span></span>
* <span data-ttu-id="000ce-173">Hallo virtuele machines voor Hallo vier lagen</span><span class="sxs-lookup"><span data-stu-id="000ce-173">hello virtual machines for hello four tiers</span></span>
* <span data-ttu-id="000ce-174">Een externe set met gelijke taakverdeling voor HTTPS-gebaseerde internetverkeer van Hallo Internet toohello webservers</span><span class="sxs-lookup"><span data-stu-id="000ce-174">An external load balanced set for HTTPS-based web traffic from hello Internet toohello web servers</span></span>
* <span data-ttu-id="000ce-175">Een interne set voor niet-versleuteld webverkeer vanaf Hallo servers toohello Webtoepassingsservers met gelijke taakverdeling</span><span class="sxs-lookup"><span data-stu-id="000ce-175">An internal load balanced set for unencrypted web traffic from hello web servers toohello application servers</span></span>
* <span data-ttu-id="000ce-176">Één resourcegroep</span><span class="sxs-lookup"><span data-stu-id="000ce-176">A single resource group</span></span>