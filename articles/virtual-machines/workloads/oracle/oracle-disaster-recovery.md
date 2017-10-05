---
title: Overzicht van een Oracle-noodherstelscenario in uw Azure-omgeving | Microsoft Docs
description: Een noodherstelscenario voor een Oracle-Database 12c-database in uw Azure-omgeving
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/2/2017
ms.author: rclaus
ms.openlocfilehash: f17ebb2b74cd7ad872f88483ed7cdb4f239ee069
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a><span data-ttu-id="8e7bf-103">Herstel na noodgevallen voor een Oracle-Database 12c-database in een Azure-omgeving</span><span class="sxs-lookup"><span data-stu-id="8e7bf-103">Disaster recovery for an Oracle Database 12c database in an Azure environment</span></span>

## <a name="assumptions"></a><span data-ttu-id="8e7bf-104">Veronderstellingen</span><span class="sxs-lookup"><span data-stu-id="8e7bf-104">Assumptions</span></span>

- <span data-ttu-id="8e7bf-105">U hebt een goed begrip van Oracle Data Guard ontwerp en de Azure-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="8e7bf-105">You have an understanding of Oracle Data Guard design and Azure environments.</span></span>


## <a name="goals"></a><span data-ttu-id="8e7bf-106">Doelstellingen</span><span class="sxs-lookup"><span data-stu-id="8e7bf-106">Goals</span></span>
- <span data-ttu-id="8e7bf-107">Ontwerp van de topologie en de configuratie die voldoen aan de vereisten van uw disaster recovery (DR).</span><span class="sxs-lookup"><span data-stu-id="8e7bf-107">Design the topology and configuration that meet your disaster recovery (DR) requirements.</span></span>

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a><span data-ttu-id="8e7bf-108">Scenario 1: Primaire en DR-sites op Azure</span><span class="sxs-lookup"><span data-stu-id="8e7bf-108">Scenario 1: Primary and DR sites on Azure</span></span>

<span data-ttu-id="8e7bf-109">Een klant heeft een Oracle-database set up op de primaire site.</span><span class="sxs-lookup"><span data-stu-id="8e7bf-109">A customer has an Oracle database set up on the primary site.</span></span> <span data-ttu-id="8e7bf-110">Er is een DR-site in een andere regio.</span><span class="sxs-lookup"><span data-stu-id="8e7bf-110">A DR site is in a different region.</span></span> <span data-ttu-id="8e7bf-111">De klant maakt gebruik van Oracle Data Guard voor snel herstel tussen deze sites.</span><span class="sxs-lookup"><span data-stu-id="8e7bf-111">The customer uses Oracle Data Guard for quick recovery between these sites.</span></span> <span data-ttu-id="8e7bf-112">De primaire site heeft ook een secundaire database voor rapportage en andere toepassingen.</span><span class="sxs-lookup"><span data-stu-id="8e7bf-112">The primary site also has a secondary database for reporting and other uses.</span></span> 

### <a name="topology"></a><span data-ttu-id="8e7bf-113">Topologie</span><span class="sxs-lookup"><span data-stu-id="8e7bf-113">Topology</span></span>

<span data-ttu-id="8e7bf-114">Hier volgt een samenvatting van de Azure-instellingen:</span><span class="sxs-lookup"><span data-stu-id="8e7bf-114">Here is a summary of the Azure setup:</span></span>

- <span data-ttu-id="8e7bf-115">Twee sites (een primaire site en een DR-site)</span><span class="sxs-lookup"><span data-stu-id="8e7bf-115">Two sites (a primary site and a DR site)</span></span>
- <span data-ttu-id="8e7bf-116">Twee virtuele netwerken</span><span class="sxs-lookup"><span data-stu-id="8e7bf-116">Two virtual networks</span></span>
- <span data-ttu-id="8e7bf-117">Twee Oracle-databases met Data Guard (primaire en stand-by)</span><span class="sxs-lookup"><span data-stu-id="8e7bf-117">Two Oracle databases with Data Guard (primary and standby)</span></span>
- <span data-ttu-id="8e7bf-118">Twee Oracle-databases met Golden Gate of Data Guard (alleen de primaire site)</span><span class="sxs-lookup"><span data-stu-id="8e7bf-118">Two Oracle databases with Golden Gate or Data Guard (primary site only)</span></span>
- <span data-ttu-id="8e7bf-119">Twee toepassingsservices: een primaire en een op de DR-site</span><span class="sxs-lookup"><span data-stu-id="8e7bf-119">Two application services, one primary and one on the DR site</span></span>
- <span data-ttu-id="8e7bf-120">Een *beschikbaarheidsset* die wordt gebruikt voor de database en de toepassing service op de primaire site</span><span class="sxs-lookup"><span data-stu-id="8e7bf-120">An *availability set,* which is used for database and application service on the primary site</span></span>
- <span data-ttu-id="8e7bf-121">Een jumpbox op elke site die de toegang beperkt tot het particuliere netwerk en kunt alleen aanmelden door een beheerder</span><span class="sxs-lookup"><span data-stu-id="8e7bf-121">One jumpbox on each site, which restricts access to the private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="8e7bf-122">Een jumpbox, de toepassingsservice, de database en de VPN-gateway op afzonderlijke subnetten</span><span class="sxs-lookup"><span data-stu-id="8e7bf-122">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="8e7bf-123">NSG afgedwongen voor de toepassing en database subnetten</span><span class="sxs-lookup"><span data-stu-id="8e7bf-123">NSG enforced on application and database subnets</span></span>

![Schermafbeelding van de pagina DR-topologie](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a><span data-ttu-id="8e7bf-125">Scenario 2: De primaire site on-premises en DR-site op Azure</span><span class="sxs-lookup"><span data-stu-id="8e7bf-125">Scenario 2: Primary site on-premises and DR site on Azure</span></span>

<span data-ttu-id="8e7bf-126">Een klant heeft een lokale installatie voor Oracle-database (primaire site).</span><span class="sxs-lookup"><span data-stu-id="8e7bf-126">A customer has an on-premises Oracle database setup (primary site).</span></span> <span data-ttu-id="8e7bf-127">Er is een DR-site op Azure.</span><span class="sxs-lookup"><span data-stu-id="8e7bf-127">A DR site is on Azure.</span></span> <span data-ttu-id="8e7bf-128">Oracle Data Guard wordt gebruikt voor snel herstel tussen deze sites.</span><span class="sxs-lookup"><span data-stu-id="8e7bf-128">Oracle Data Guard is used for quick recovery between these sites.</span></span> <span data-ttu-id="8e7bf-129">De primaire site heeft ook een secundaire database voor rapportage en andere toepassingen.</span><span class="sxs-lookup"><span data-stu-id="8e7bf-129">The primary site also has a secondary database for reporting and other uses.</span></span> 

<span data-ttu-id="8e7bf-130">Er zijn twee manieren om deze installatie.</span><span class="sxs-lookup"><span data-stu-id="8e7bf-130">There are two approaches for this setup.</span></span>

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-the-firewall"></a><span data-ttu-id="8e7bf-131">Methode 1: Rechtstreekse verbindingen tussen on-premises en Azure, open TCP-poorten op de firewall vereisen</span><span class="sxs-lookup"><span data-stu-id="8e7bf-131">Approach 1: Direct connections between on-premises and Azure, requiring open TCP ports on the firewall</span></span> 

<span data-ttu-id="8e7bf-132">Directe verbindingen wordt niet aanbevolen omdat ze de TCP-poorten voor de buitenwereld openbaren.</span><span class="sxs-lookup"><span data-stu-id="8e7bf-132">We don't recommend direct connections because they expose the TCP ports to the outside world.</span></span>

#### <a name="topology"></a><span data-ttu-id="8e7bf-133">Topologie</span><span class="sxs-lookup"><span data-stu-id="8e7bf-133">Topology</span></span>

<span data-ttu-id="8e7bf-134">Hier volgt een samenvatting van de installatie van de Azure:</span><span class="sxs-lookup"><span data-stu-id="8e7bf-134">Following is a summary of the Azure setup:</span></span>

- <span data-ttu-id="8e7bf-135">Een DR-site</span><span class="sxs-lookup"><span data-stu-id="8e7bf-135">One DR site</span></span> 
- <span data-ttu-id="8e7bf-136">Een virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="8e7bf-136">One virtual network</span></span>
- <span data-ttu-id="8e7bf-137">Een Oracle-database met Data Guard (actief)</span><span class="sxs-lookup"><span data-stu-id="8e7bf-137">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="8e7bf-138">De service één toepassing op de DR-site</span><span class="sxs-lookup"><span data-stu-id="8e7bf-138">One application service on the DR site</span></span>
- <span data-ttu-id="8e7bf-139">Een jumpbox, waardoor de toegang beperkt tot het particuliere netwerk en kunt alleen aanmelden door een beheerder</span><span class="sxs-lookup"><span data-stu-id="8e7bf-139">One jumpbox, which restricts access to the private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="8e7bf-140">Een jumpbox, de toepassingsservice, de database en de VPN-gateway op afzonderlijke subnetten</span><span class="sxs-lookup"><span data-stu-id="8e7bf-140">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="8e7bf-141">NSG afgedwongen voor de toepassing en database subnetten</span><span class="sxs-lookup"><span data-stu-id="8e7bf-141">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="8e7bf-142">Een NSG/beleidsregel waarmee binnenkomende TCP-poort 1521 (of een door de gebruiker gedefinieerde poort)</span><span class="sxs-lookup"><span data-stu-id="8e7bf-142">An NSG policy/rule to allow inbound TCP port 1521 (or a user-defined port)</span></span>
- <span data-ttu-id="8e7bf-143">Een NSG/beleidsregel te beperken van het IP-adres adres adressen lokale (DB of toepassing) toegang tot het virtuele netwerk</span><span class="sxs-lookup"><span data-stu-id="8e7bf-143">An NSG policy/rule to restrict only the IP address/addresses on-premises (DB or application) to access the virtual network</span></span>

![Schermafbeelding van de pagina DR-topologie](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a><span data-ttu-id="8e7bf-145">Methode 2: Site-naar-site VPN</span><span class="sxs-lookup"><span data-stu-id="8e7bf-145">Approach 2: Site-to-site VPN</span></span>
<span data-ttu-id="8e7bf-146">Site-naar-site VPN is een betere benadering.</span><span class="sxs-lookup"><span data-stu-id="8e7bf-146">Site-to-site VPN is a better approach.</span></span> <span data-ttu-id="8e7bf-147">Zie voor meer informatie over het instellen van een VPN [een virtueel netwerk maken met een Site-naar-Site VPN-verbinding met CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="8e7bf-147">For more information about setting up a VPN, see [Create a virtual network with a Site-to-Site VPN connection using CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span>

#### <a name="topology"></a><span data-ttu-id="8e7bf-148">Topologie</span><span class="sxs-lookup"><span data-stu-id="8e7bf-148">Topology</span></span>

<span data-ttu-id="8e7bf-149">Hier volgt een samenvatting van de installatie van de Azure:</span><span class="sxs-lookup"><span data-stu-id="8e7bf-149">Following is a summary of the Azure setup:</span></span>

- <span data-ttu-id="8e7bf-150">Een DR-site</span><span class="sxs-lookup"><span data-stu-id="8e7bf-150">One DR site</span></span> 
- <span data-ttu-id="8e7bf-151">Een virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="8e7bf-151">One virtual network</span></span> 
- <span data-ttu-id="8e7bf-152">Een Oracle-database met Data Guard (actief)</span><span class="sxs-lookup"><span data-stu-id="8e7bf-152">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="8e7bf-153">De service één toepassing op de DR-site</span><span class="sxs-lookup"><span data-stu-id="8e7bf-153">One application service on the DR site</span></span>
- <span data-ttu-id="8e7bf-154">Een jumpbox, waardoor de toegang beperkt tot het particuliere netwerk en kunt alleen aanmelden door een beheerder</span><span class="sxs-lookup"><span data-stu-id="8e7bf-154">One jumpbox, which restricts access to the private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="8e7bf-155">Een jumpbox, de toepassingsservice, de database en de VPN-gateway worden op afzonderlijke subnetten</span><span class="sxs-lookup"><span data-stu-id="8e7bf-155">A jumpbox, application service, database, and VPN gateway are on separate subnets</span></span>
- <span data-ttu-id="8e7bf-156">NSG afgedwongen voor de toepassing en database subnetten</span><span class="sxs-lookup"><span data-stu-id="8e7bf-156">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="8e7bf-157">Site-naar-site VPN-verbinding tussen on-premises en Azure</span><span class="sxs-lookup"><span data-stu-id="8e7bf-157">Site-to-site VPN connection between on-premises and Azure</span></span>

![Schermafbeelding van de pagina DR-topologie](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a><span data-ttu-id="8e7bf-159">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8e7bf-159">Additional reading</span></span>

- [<span data-ttu-id="8e7bf-160">Ontwerpen en implementeren van een Oracle-database in Azure</span><span class="sxs-lookup"><span data-stu-id="8e7bf-160">Design and implement an Oracle database on Azure</span></span>](oracle-design.md)
- [<span data-ttu-id="8e7bf-161">Oracle Data Guard configureren</span><span class="sxs-lookup"><span data-stu-id="8e7bf-161">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="8e7bf-162">Oracle Golden Gate configureren</span><span class="sxs-lookup"><span data-stu-id="8e7bf-162">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="8e7bf-163">Oracle back-up en herstel</span><span class="sxs-lookup"><span data-stu-id="8e7bf-163">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)


## <a name="next-steps"></a><span data-ttu-id="8e7bf-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8e7bf-164">Next steps</span></span>

- [<span data-ttu-id="8e7bf-165">Zelfstudie: Een maximaal beschikbare virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="8e7bf-165">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="8e7bf-166">VM-implementatie Azure CLI voorbeelden verkennen</span><span class="sxs-lookup"><span data-stu-id="8e7bf-166">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
