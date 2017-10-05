---
title: Azure SQL Database connectivity-architectuur | Microsoft Docs
description: Dit document wordt uitgelegd dat de Azure SQLDB connectiviteit architectuur van Azure of vanuit buiten Azure.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 8a1dd89c9e82483184ceb5d767190a5a5044265d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a><span data-ttu-id="19d39-103">Azure SQL Database Connectivity-architectuur</span><span class="sxs-lookup"><span data-stu-id="19d39-103">Azure SQL Database Connectivity Architecture</span></span> 

<span data-ttu-id="19d39-104">Dit artikel wordt uitgelegd van de Azure SQL Database connectivity-architectuur en wordt uitgelegd hoe de andere onderdelen functie voor het verkeer naar uw Azure SQL Database-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="19d39-104">This article explains the Azure SQL Database connectivity architecture and explains how the different components function to direct traffic to your instance of Azure SQL Database.</span></span> <span data-ttu-id="19d39-105">Deze Azure SQL Database connectivity onderdelen functie om netwerkverkeer te regelen met de Azure-database met clients die verbinding maken vanuit Azure en clients die verbinding maakt vanaf buiten Azure.</span><span class="sxs-lookup"><span data-stu-id="19d39-105">These Azure SQL Database connectivity components function to direct network traffic to the Azure database with clients connecting from within Azure and with clients connecting from outside of Azure.</span></span> <span data-ttu-id="19d39-106">In dit artikel biedt ook scriptvoorbeelden wijzigen hoe de verbinding plaatsvindt, evenals de overwegingen die betrekking hebben op de standaardinstellingen van de verbinding wijzigen.</span><span class="sxs-lookup"><span data-stu-id="19d39-106">This article also provides script samples to change how connectivity occurs, and the considerations related to changing the default connectivity settings.</span></span> <span data-ttu-id="19d39-107">Als er vragen na het lezen van dit artikel, neem contact op met Dhruv op dmalik@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="19d39-107">If there are any questions after reading this article, please contact Dhruv at dmalik@microsoft.com.</span></span> 

## <a name="connectivity-architecture"></a><span data-ttu-id="19d39-108">Connectiviteitsarchitectuur</span><span class="sxs-lookup"><span data-stu-id="19d39-108">Connectivity architecture</span></span>

<span data-ttu-id="19d39-109">Het volgende diagram biedt een overzicht van de Azure SQL Database connectivity-architectuur.</span><span class="sxs-lookup"><span data-stu-id="19d39-109">The following diagram provides a high-level overview of the Azure SQL Database connectivity architecture.</span></span> 

![overzicht van de architectuur](./media/sql-database-connectivity-architecture/architecture-overview.png)


<span data-ttu-id="19d39-111">De volgende stappen wordt beschreven hoe een verbinding is gemaakt met een Azure SQL database via de Azure SQL Database software load balancer (SLB) en de Azure SQL Database-gateway.</span><span class="sxs-lookup"><span data-stu-id="19d39-111">The following steps describe how a connection is established to an Azure SQL database through the Azure SQL Database software load-balancer (SLB) and the Azure SQL Database gateway.</span></span>

- <span data-ttu-id="19d39-112">Clients in Azure of buiten Azure verbinding met de SLB dat een openbare IP-adres en luistert op poort 1433.</span><span class="sxs-lookup"><span data-stu-id="19d39-112">Clients within Azure or outside of Azure connect to the SLB, which has a public IP address and listens on port 1433.</span></span>
- <span data-ttu-id="19d39-113">De SLB stuurt het verkeer naar de Azure SQL Database-gateway.</span><span class="sxs-lookup"><span data-stu-id="19d39-113">The SLB directs traffic to the Azure SQL Database gateway.</span></span>
- <span data-ttu-id="19d39-114">De gateway stuurt het verkeer naar de juiste proxy-middleware.</span><span class="sxs-lookup"><span data-stu-id="19d39-114">The gateway redirects the traffic to the correct proxy middleware.</span></span>
- <span data-ttu-id="19d39-115">De proxy-middleware leidt het verkeer naar de juiste Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="19d39-115">The proxy middleware redirects the traffic to the appropriate Azure SQL database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19d39-116">Elk van deze componenten heeft gedistribueerde denial-of-service (DDoS) beveiliging ingebouwde op het netwerk en de app-laag.</span><span class="sxs-lookup"><span data-stu-id="19d39-116">Each of these components has distributed denial of service (DDoS) protection built-in at the network and the app layer.</span></span>
>

## <a name="connectivity-from-within-azure"></a><span data-ttu-id="19d39-117">Verbinding tussen in Azure</span><span class="sxs-lookup"><span data-stu-id="19d39-117">Connectivity from within Azure</span></span>

<span data-ttu-id="19d39-118">Als u verbinding vanaf in Azure maakt, uw verbindingen hebben een beleid van **omleiden** standaard.</span><span class="sxs-lookup"><span data-stu-id="19d39-118">If you are connecting from within Azure, your connections have a connection policy of **Redirect** by default.</span></span> <span data-ttu-id="19d39-119">Een beleid van **omleiden** betekent dat verbindingen nadat de TCP-sessie tot stand is gebracht met de Azure SQL database, de clientsessie wordt vervolgens omgeleid naar de proxy-middleware met een wijziging in het virtuele IP-adres voor doel van die van de Azure SQL Database-gateway met die van de proxy-middleware.</span><span class="sxs-lookup"><span data-stu-id="19d39-119">A policy of **Redirect** means that connections after the TCP session is established to the Azure SQL database, the client session is then redirected to the proxy middleware with a change to the destination virtual IP from that of the Azure SQL Database gateway to that of the proxy middleware.</span></span> <span data-ttu-id="19d39-120">Daarna alle latere pakketten stromen rechtstreeks via de proxy-middleware voor het omzeilen van de Azure SQL Database-gateway.</span><span class="sxs-lookup"><span data-stu-id="19d39-120">Thereafter, all subsequent packets flow directly via the proxy middleware, bypassing the Azure SQL Database gateway.</span></span> <span data-ttu-id="19d39-121">Het volgende diagram illustreert dit netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="19d39-121">The following diagram illustrates this traffic flow.</span></span>

![overzicht van de architectuur](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a><span data-ttu-id="19d39-123">Connectiviteit van buiten Azure</span><span class="sxs-lookup"><span data-stu-id="19d39-123">Connectivity from outside of Azure</span></span>

<span data-ttu-id="19d39-124">Als u verbinding vanaf buiten Azure maakt, uw verbindingen hebben een beleid van **Proxy** standaard.</span><span class="sxs-lookup"><span data-stu-id="19d39-124">If you are connecting from outside Azure, your connections have a connection policy of **Proxy** by default.</span></span> <span data-ttu-id="19d39-125">Een beleid van **Proxy** betekent dat de TCP-sessie tot stand is gebracht via de Azure SQL Database-gateway en alle latere pakketten stromen via de gateway.</span><span class="sxs-lookup"><span data-stu-id="19d39-125">A policy of **Proxy** means that the TCP session is established via the Azure SQL Database gateway and all subsequent packets flow via the gateway.</span></span> <span data-ttu-id="19d39-126">Het volgende diagram illustreert dit netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="19d39-126">The following diagram illustrates this traffic flow.</span></span>

![overzicht van de architectuur](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a><span data-ttu-id="19d39-128">IP-adressen van Azure SQL Database-gateway</span><span class="sxs-lookup"><span data-stu-id="19d39-128">Azure SQL Database gateway IP addresses</span></span>

<span data-ttu-id="19d39-129">Voor verbinding met een Azure SQL database van de lokale bronnen, moet u uitgaand netwerkverkeer naar de Azure SQL Database-gateway voor uw Azure-regio toestaan.</span><span class="sxs-lookup"><span data-stu-id="19d39-129">To connect to an Azure SQL database from on-premises resources, you need to allow outbound network traffic to the Azure SQL Database gateway for your Azure region.</span></span> <span data-ttu-id="19d39-130">Uw verbindingen gaat alleen via de gateway om verbinding te maken in de Proxy-modus de standaardinstelling is bij het verbinden van lokale bronnen.</span><span class="sxs-lookup"><span data-stu-id="19d39-130">Your connections only go via the gateway when connecting in Proxy mode, which is the default when connecting from on-premises resources.</span></span>

<span data-ttu-id="19d39-131">De volgende tabel bevat de primaire en secundaire IP-adressen van de Azure SQL Database-gateway voor alle regio's van gegevens.</span><span class="sxs-lookup"><span data-stu-id="19d39-131">The following table lists the primary and secondary IPs of the Azure SQL Database gateway for all data regions.</span></span> <span data-ttu-id="19d39-132">Er zijn twee IP-adressen voor bepaalde gebieden.</span><span class="sxs-lookup"><span data-stu-id="19d39-132">For some regions, there are two IP addresses.</span></span> <span data-ttu-id="19d39-133">In deze regio's, de primaire IP-adres is het huidige IP-adres van de gateway en het tweede IP-adres is een failover-IP-adres.</span><span class="sxs-lookup"><span data-stu-id="19d39-133">In these regions, the primary IP address is the current IP address of the gateway and the second IP address is a failover IP address.</span></span> <span data-ttu-id="19d39-134">De failover-adres is het adres waarop we uw server te houden van hoge beschikbaarheid van de service mogelijk verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="19d39-134">The failover address is the address to which we might move your server to keep the service availability high.</span></span> <span data-ttu-id="19d39-135">Voor deze regio's, is het raadzaam dat u uitgaand verkeer naar de IP-adressen toestaan.</span><span class="sxs-lookup"><span data-stu-id="19d39-135">For these regions, we recommend that you allow outbound to both the IP addresses.</span></span> <span data-ttu-id="19d39-136">Het tweede IP-adres is het eigendom van Microsoft en luistert niet op alle services totdat deze is geactiveerd door Azure SQL Database om verbindingen te accepteren.</span><span class="sxs-lookup"><span data-stu-id="19d39-136">The second IP address is owned by Microsoft and does not listen in on any services until it is activated by Azure SQL Database to accept connections.</span></span>

| <span data-ttu-id="19d39-137">Naam regio</span><span class="sxs-lookup"><span data-stu-id="19d39-137">Region Name</span></span> | <span data-ttu-id="19d39-138">Primaire IP-adres</span><span class="sxs-lookup"><span data-stu-id="19d39-138">Primary IP address</span></span> | <span data-ttu-id="19d39-139">Secundaire IP-adres</span><span class="sxs-lookup"><span data-stu-id="19d39-139">Secondary IP address</span></span> |
| --- | --- |--- |
| <span data-ttu-id="19d39-140">Australië - oost</span><span class="sxs-lookup"><span data-stu-id="19d39-140">Australia East</span></span> | <span data-ttu-id="19d39-141">191.238.66.109</span><span class="sxs-lookup"><span data-stu-id="19d39-141">191.238.66.109</span></span> | <span data-ttu-id="19d39-142">13.75.149.87</span><span class="sxs-lookup"><span data-stu-id="19d39-142">13.75.149.87</span></span> |
| <span data-ttu-id="19d39-143">Australië - zuidoost</span><span class="sxs-lookup"><span data-stu-id="19d39-143">Australia South East</span></span> | <span data-ttu-id="19d39-144">191.239.192.109</span><span class="sxs-lookup"><span data-stu-id="19d39-144">191.239.192.109</span></span> | <span data-ttu-id="19d39-145">13.73.109.251</span><span class="sxs-lookup"><span data-stu-id="19d39-145">13.73.109.251</span></span> |
| <span data-ttu-id="19d39-146">Brazilië - zuid</span><span class="sxs-lookup"><span data-stu-id="19d39-146">Brazil South</span></span> | <span data-ttu-id="19d39-147">104.41.11.5</span><span class="sxs-lookup"><span data-stu-id="19d39-147">104.41.11.5</span></span> | |    
| <span data-ttu-id="19d39-148">Canada - midden</span><span class="sxs-lookup"><span data-stu-id="19d39-148">Canada Central</span></span> | <span data-ttu-id="19d39-149">40.85.224.249</span><span class="sxs-lookup"><span data-stu-id="19d39-149">40.85.224.249</span></span> | |    
| <span data-ttu-id="19d39-150">Canada - oost</span><span class="sxs-lookup"><span data-stu-id="19d39-150">Canada East</span></span> | <span data-ttu-id="19d39-151">40.86.226.166</span><span class="sxs-lookup"><span data-stu-id="19d39-151">40.86.226.166</span></span> | |
| <span data-ttu-id="19d39-152">VS - midden</span><span class="sxs-lookup"><span data-stu-id="19d39-152">Central US</span></span> | <span data-ttu-id="19d39-153">23.99.160.139</span><span class="sxs-lookup"><span data-stu-id="19d39-153">23.99.160.139</span></span> | <span data-ttu-id="19d39-154">13.67.215.62</span><span class="sxs-lookup"><span data-stu-id="19d39-154">13.67.215.62</span></span> |
| <span data-ttu-id="19d39-155">Oost-Azië</span><span class="sxs-lookup"><span data-stu-id="19d39-155">East Asia</span></span> | <span data-ttu-id="19d39-156">191.234.2.139</span><span class="sxs-lookup"><span data-stu-id="19d39-156">191.234.2.139</span></span> | <span data-ttu-id="19d39-157">52.175.33.150</span><span class="sxs-lookup"><span data-stu-id="19d39-157">52.175.33.150</span></span> |
| <span data-ttu-id="19d39-158">VS-Oost 1</span><span class="sxs-lookup"><span data-stu-id="19d39-158">East US 1</span></span> | <span data-ttu-id="19d39-159">191.238.6.43</span><span class="sxs-lookup"><span data-stu-id="19d39-159">191.238.6.43</span></span> | <span data-ttu-id="19d39-160">40.121.158.30</span><span class="sxs-lookup"><span data-stu-id="19d39-160">40.121.158.30</span></span> |
| <span data-ttu-id="19d39-161">VS - oost 2</span><span class="sxs-lookup"><span data-stu-id="19d39-161">East US 2</span></span> | <span data-ttu-id="19d39-162">191.239.224.107</span><span class="sxs-lookup"><span data-stu-id="19d39-162">191.239.224.107</span></span> | <span data-ttu-id="19d39-163">40.79.84.180</span><span class="sxs-lookup"><span data-stu-id="19d39-163">40.79.84.180</span></span> |
| <span data-ttu-id="19d39-164">India - midden</span><span class="sxs-lookup"><span data-stu-id="19d39-164">India Central</span></span> | <span data-ttu-id="19d39-165">104.211.96.159</span><span class="sxs-lookup"><span data-stu-id="19d39-165">104.211.96.159</span></span>  | |   
| <span data-ttu-id="19d39-166">India - zuid</span><span class="sxs-lookup"><span data-stu-id="19d39-166">India South</span></span> | <span data-ttu-id="19d39-167">104.211.224.146</span><span class="sxs-lookup"><span data-stu-id="19d39-167">104.211.224.146</span></span>  | |
| <span data-ttu-id="19d39-168">India - west</span><span class="sxs-lookup"><span data-stu-id="19d39-168">India West</span></span> | <span data-ttu-id="19d39-169">104.211.160.80</span><span class="sxs-lookup"><span data-stu-id="19d39-169">104.211.160.80</span></span> | |
| <span data-ttu-id="19d39-170">Japan - oost</span><span class="sxs-lookup"><span data-stu-id="19d39-170">Japan East</span></span> | <span data-ttu-id="19d39-171">191.237.240.43</span><span class="sxs-lookup"><span data-stu-id="19d39-171">191.237.240.43</span></span> | <span data-ttu-id="19d39-172">13.78.61.196</span><span class="sxs-lookup"><span data-stu-id="19d39-172">13.78.61.196</span></span> |
| <span data-ttu-id="19d39-173">Japan - west</span><span class="sxs-lookup"><span data-stu-id="19d39-173">Japan West</span></span> | <span data-ttu-id="19d39-174">191.238.68.11</span><span class="sxs-lookup"><span data-stu-id="19d39-174">191.238.68.11</span></span> | <span data-ttu-id="19d39-175">104.214.148.156</span><span class="sxs-lookup"><span data-stu-id="19d39-175">104.214.148.156</span></span> |
| <span data-ttu-id="19d39-176">Korea - centraal</span><span class="sxs-lookup"><span data-stu-id="19d39-176">Korea Central</span></span> | <span data-ttu-id="19d39-177">52.231.32.42</span><span class="sxs-lookup"><span data-stu-id="19d39-177">52.231.32.42</span></span> | |
| <span data-ttu-id="19d39-178">Korea - zuid</span><span class="sxs-lookup"><span data-stu-id="19d39-178">Korea South</span></span> | <span data-ttu-id="19d39-179">52.231.200.86</span><span class="sxs-lookup"><span data-stu-id="19d39-179">52.231.200.86</span></span> |  |
| <span data-ttu-id="19d39-180">Noord-centraal VS</span><span class="sxs-lookup"><span data-stu-id="19d39-180">North Central US</span></span> | <span data-ttu-id="19d39-181">23.98.55.75</span><span class="sxs-lookup"><span data-stu-id="19d39-181">23.98.55.75</span></span> | <span data-ttu-id="19d39-182">23.96.178.199</span><span class="sxs-lookup"><span data-stu-id="19d39-182">23.96.178.199</span></span> |
| <span data-ttu-id="19d39-183">Noord-Europa</span><span class="sxs-lookup"><span data-stu-id="19d39-183">North Europe</span></span> | <span data-ttu-id="19d39-184">191.235.193.75</span><span class="sxs-lookup"><span data-stu-id="19d39-184">191.235.193.75</span></span> | <span data-ttu-id="19d39-185">40.113.93.91</span><span class="sxs-lookup"><span data-stu-id="19d39-185">40.113.93.91</span></span> |
| <span data-ttu-id="19d39-186">Zuid-centraal VS</span><span class="sxs-lookup"><span data-stu-id="19d39-186">South Central US</span></span> | <span data-ttu-id="19d39-187">23.98.162.75</span><span class="sxs-lookup"><span data-stu-id="19d39-187">23.98.162.75</span></span> | <span data-ttu-id="19d39-188">13.66.62.124</span><span class="sxs-lookup"><span data-stu-id="19d39-188">13.66.62.124</span></span> |
| <span data-ttu-id="19d39-189">Zuidoost-Azië</span><span class="sxs-lookup"><span data-stu-id="19d39-189">South East Asia</span></span> | <span data-ttu-id="19d39-190">23.100.117.95</span><span class="sxs-lookup"><span data-stu-id="19d39-190">23.100.117.95</span></span> | <span data-ttu-id="19d39-191">104.43.15.0</span><span class="sxs-lookup"><span data-stu-id="19d39-191">104.43.15.0</span></span> |
| <span data-ttu-id="19d39-192">VK, noord</span><span class="sxs-lookup"><span data-stu-id="19d39-192">UK North</span></span> | <span data-ttu-id="19d39-193">13.87.97.210</span><span class="sxs-lookup"><span data-stu-id="19d39-193">13.87.97.210</span></span> | |
| <span data-ttu-id="19d39-194">VK Zuid 1</span><span class="sxs-lookup"><span data-stu-id="19d39-194">UK South 1</span></span> | <span data-ttu-id="19d39-195">51.140.184.11</span><span class="sxs-lookup"><span data-stu-id="19d39-195">51.140.184.11</span></span> | |    
| <span data-ttu-id="19d39-196">VK, zuid 2</span><span class="sxs-lookup"><span data-stu-id="19d39-196">UK South 2</span></span> | <span data-ttu-id="19d39-197">13.87.34.7</span><span class="sxs-lookup"><span data-stu-id="19d39-197">13.87.34.7</span></span> | |
| <span data-ttu-id="19d39-198">Verenigd Koninkrijk West</span><span class="sxs-lookup"><span data-stu-id="19d39-198">UK West</span></span> | <span data-ttu-id="19d39-199">51.141.8.11</span><span class="sxs-lookup"><span data-stu-id="19d39-199">51.141.8.11</span></span>  | |
| <span data-ttu-id="19d39-200">West-centraal VS</span><span class="sxs-lookup"><span data-stu-id="19d39-200">West Central US</span></span> | <span data-ttu-id="19d39-201">13.78.145.25</span><span class="sxs-lookup"><span data-stu-id="19d39-201">13.78.145.25</span></span> | |
| <span data-ttu-id="19d39-202">West-Europa</span><span class="sxs-lookup"><span data-stu-id="19d39-202">West Europe</span></span> | <span data-ttu-id="19d39-203">191.237.232.75</span><span class="sxs-lookup"><span data-stu-id="19d39-203">191.237.232.75</span></span> | <span data-ttu-id="19d39-204">40.68.37.158</span><span class="sxs-lookup"><span data-stu-id="19d39-204">40.68.37.158</span></span> |
| <span data-ttu-id="19d39-205">VS-West 1</span><span class="sxs-lookup"><span data-stu-id="19d39-205">West US 1</span></span> | <span data-ttu-id="19d39-206">23.99.34.75</span><span class="sxs-lookup"><span data-stu-id="19d39-206">23.99.34.75</span></span> | <span data-ttu-id="19d39-207">104.42.238.205</span><span class="sxs-lookup"><span data-stu-id="19d39-207">104.42.238.205</span></span> |
| <span data-ttu-id="19d39-208">VS - west 2</span><span class="sxs-lookup"><span data-stu-id="19d39-208">West US 2</span></span> | <span data-ttu-id="19d39-209">13.66.226.202</span><span class="sxs-lookup"><span data-stu-id="19d39-209">13.66.226.202</span></span>  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a><span data-ttu-id="19d39-210">Azure SQL Database verbindingsbeleid wijzigen</span><span class="sxs-lookup"><span data-stu-id="19d39-210">Change Azure SQL Database connection policy</span></span>

<span data-ttu-id="19d39-211">Om te wijzigen van het beleid van de Azure SQL Database-verbinding voor een Azure SQL Database-server, gebruiken de [REST-API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="19d39-211">To change the Azure SQL Database connection policy for an Azure SQL Database server, use the [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span> 

- <span data-ttu-id="19d39-212">Als uw verbindingsbeleid voor de is ingesteld op **Proxy**, alle netwerkapparaten stroom van pakketten via de Azure SQL Database-gateway.</span><span class="sxs-lookup"><span data-stu-id="19d39-212">If your connection policy is set to **Proxy**, all network packets flow via the Azure SQL Database gateway.</span></span> <span data-ttu-id="19d39-213">Voor deze instelling moet u uitgaand verkeer op alleen de Azure SQL Database gateway IP toestaan.</span><span class="sxs-lookup"><span data-stu-id="19d39-213">For this setting, you need to allow outbound to only the Azure SQL Database gateway IP.</span></span> <span data-ttu-id="19d39-214">Met behulp van een instelling van **Proxy** heeft latentie van meer dan een instelling van **omleiden**.</span><span class="sxs-lookup"><span data-stu-id="19d39-214">Using a setting of **Proxy** has more latency than a setting of **Redirect**.</span></span> 
- <span data-ttu-id="19d39-215">Als uw verbindingsbeleid voor de tot stand **omleiden**, alle pakketten stroom rechtstreeks naar de proxy middleware netwerkapparaten.</span><span class="sxs-lookup"><span data-stu-id="19d39-215">If your connection policy is setting **Redirect**, all network packets flow directly to the middleware proxy.</span></span> <span data-ttu-id="19d39-216">Voor deze instelling moet u uitgaand verkeer naar meerdere IP-adressen toestaan.</span><span class="sxs-lookup"><span data-stu-id="19d39-216">For this setting, you need to allow outbound to multiple IPs.</span></span> 

## <a name="script-to-change-connection-settings"></a><span data-ttu-id="19d39-217">Script verbindingsinstellingen wijzigen</span><span class="sxs-lookup"><span data-stu-id="19d39-217">Script to change connection settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19d39-218">Dit script vereist de [Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="19d39-218">This script requires the [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>
>

<span data-ttu-id="19d39-219">De volgende PowerShell-script laat zien hoe het verbindingsbeleid wijzigen.</span><span class="sxs-lookup"><span data-stu-id="19d39-219">The following PowerShell script shows how to change the connection policy.</span></span>

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting the current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting the property to ‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a><span data-ttu-id="19d39-220">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="19d39-220">Next steps</span></span>

- <span data-ttu-id="19d39-221">Zie voor meer informatie over het wijzigen van het beleid van de Azure SQL Database-verbinding voor een Azure SQL Database-server [maken of bijwerken Server verbindingsbeleid met de REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="19d39-221">For information on how to change the Azure SQL Database connection policy for an Azure SQL Database server, see [Create or Update Server Connection Policy using the REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span>
- <span data-ttu-id="19d39-222">Zie voor informatie over de werking van Azure SQL Database-verbinding voor clients die gebruikmaken van ADO.NET 4.5 of hoger, [poorten buiten 1433 ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="19d39-222">For information about Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version, see [Ports beyond 1433 for ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>
- <span data-ttu-id="19d39-223">Zie voor informatie over algemene toepassing ontwikkeling overzicht, [SQL Database ontwikkelen-overzicht](sql-database-develop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="19d39-223">For general application development overview information, see [SQL Database Application Development Overview](sql-database-develop-overview.md).</span></span>
