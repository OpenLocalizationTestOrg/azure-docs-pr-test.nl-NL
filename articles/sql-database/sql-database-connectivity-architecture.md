---
title: aaaAzure SQL Database connectivity-architectuur | Microsoft Docs
description: Dit document wordt uitgelegd hello Azure SQLDB connectiviteit-architectuur van Azure of vanuit buiten Azure.
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
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a><span data-ttu-id="265e5-103">Azure SQL Database Connectivity-architectuur</span><span class="sxs-lookup"><span data-stu-id="265e5-103">Azure SQL Database Connectivity Architecture</span></span> 

<span data-ttu-id="265e5-104">In dit artikel wordt uitgelegd hello Azure SQL Database connectivity-architectuur en wordt uitgelegd hoe de verschillende onderdelen Hallo toodirect verkeer tooyour exemplaar van Azure SQL Database werken.</span><span class="sxs-lookup"><span data-stu-id="265e5-104">This article explains hello Azure SQL Database connectivity architecture and explains how hello different components function toodirect traffic tooyour instance of Azure SQL Database.</span></span> <span data-ttu-id="265e5-105">Deze Azure SQL Database connectivity-componenten werken toodirect netwerkverkeer toohello Azure-database met clients die verbinding maken vanuit Azure en clients die verbinding maakt vanaf buiten Azure.</span><span class="sxs-lookup"><span data-stu-id="265e5-105">These Azure SQL Database connectivity components function toodirect network traffic toohello Azure database with clients connecting from within Azure and with clients connecting from outside of Azure.</span></span> <span data-ttu-id="265e5-106">In dit artikel biedt ook script voorbeelden toochange hoe connectiviteit plaatsvindt en Hallo overwegingen gerelateerd toochanging Hallo connectivity standaardinstellingen.</span><span class="sxs-lookup"><span data-stu-id="265e5-106">This article also provides script samples toochange how connectivity occurs, and hello considerations related toochanging hello default connectivity settings.</span></span> <span data-ttu-id="265e5-107">Als er vragen na het lezen van dit artikel, neem contact op met Dhruv op dmalik@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="265e5-107">If there are any questions after reading this article, please contact Dhruv at dmalik@microsoft.com.</span></span> 

## <a name="connectivity-architecture"></a><span data-ttu-id="265e5-108">Connectiviteitsarchitectuur</span><span class="sxs-lookup"><span data-stu-id="265e5-108">Connectivity architecture</span></span>

<span data-ttu-id="265e5-109">Hallo volgende diagram biedt een overzicht van hello Azure SQL Database connectivity-architectuur.</span><span class="sxs-lookup"><span data-stu-id="265e5-109">hello following diagram provides a high-level overview of hello Azure SQL Database connectivity architecture.</span></span> 

![overzicht van de architectuur](./media/sql-database-connectivity-architecture/architecture-overview.png)


<span data-ttu-id="265e5-111">Hallo volgende stappen wordt beschreven hoe een verbinding tot stand gebrachte tooan Azure SQL database via hello Azure SQL Database software load balancer (SLB) en hello Azure SQL Database-gateway is.</span><span class="sxs-lookup"><span data-stu-id="265e5-111">hello following steps describe how a connection is established tooan Azure SQL database through hello Azure SQL Database software load-balancer (SLB) and hello Azure SQL Database gateway.</span></span>

- <span data-ttu-id="265e5-112">Clients in Azure of buiten Azure verbinding toohello SLB dat een openbare IP-adres en luistert op poort 1433.</span><span class="sxs-lookup"><span data-stu-id="265e5-112">Clients within Azure or outside of Azure connect toohello SLB, which has a public IP address and listens on port 1433.</span></span>
- <span data-ttu-id="265e5-113">Hallo SLB stuurt verkeer toohello Azure SQL Database-gateway.</span><span class="sxs-lookup"><span data-stu-id="265e5-113">hello SLB directs traffic toohello Azure SQL Database gateway.</span></span>
- <span data-ttu-id="265e5-114">Hallo-gateway wordt omgeleid Hallo verkeer toohello juiste proxy middleware.</span><span class="sxs-lookup"><span data-stu-id="265e5-114">hello gateway redirects hello traffic toohello correct proxy middleware.</span></span>
- <span data-ttu-id="265e5-115">Hallo proxy middleware leidt Hallo verkeer toohello juiste Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="265e5-115">hello proxy middleware redirects hello traffic toohello appropriate Azure SQL database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="265e5-116">Elk van deze onderdelen is denial of service (DDoS) beveiliging ingebouwde op Hallo netwerk- en app-laag Hallo gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="265e5-116">Each of these components has distributed denial of service (DDoS) protection built-in at hello network and hello app layer.</span></span>
>

## <a name="connectivity-from-within-azure"></a><span data-ttu-id="265e5-117">Verbinding tussen in Azure</span><span class="sxs-lookup"><span data-stu-id="265e5-117">Connectivity from within Azure</span></span>

<span data-ttu-id="265e5-118">Als u verbinding vanaf in Azure maakt, uw verbindingen hebben een beleid van **omleiden** standaard.</span><span class="sxs-lookup"><span data-stu-id="265e5-118">If you are connecting from within Azure, your connections have a connection policy of **Redirect** by default.</span></span> <span data-ttu-id="265e5-119">Een beleid van **omleiden** betekent dat verbindingen nadat Hallo TCP-sessie tot stand gebrachte toohello Azure SQL-database is, Hallo clientsessie vervolgens omgeleid toohello proxy middleware met een wijziging toohello bestemming virtuele IP-adres uit die van hello Azure SQL Database gateway toothat van Hallo proxy middleware.</span><span class="sxs-lookup"><span data-stu-id="265e5-119">A policy of **Redirect** means that connections after hello TCP session is established toohello Azure SQL database, hello client session is then redirected toohello proxy middleware with a change toohello destination virtual IP from that of hello Azure SQL Database gateway toothat of hello proxy middleware.</span></span> <span data-ttu-id="265e5-120">Daarna alle latere pakketten stromen rechtstreeks via Hallo proxy middleware, omzeilen hello Azure SQL Database-gateway.</span><span class="sxs-lookup"><span data-stu-id="265e5-120">Thereafter, all subsequent packets flow directly via hello proxy middleware, bypassing hello Azure SQL Database gateway.</span></span> <span data-ttu-id="265e5-121">Hallo volgende diagram illustreert dit netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="265e5-121">hello following diagram illustrates this traffic flow.</span></span>

![overzicht van de architectuur](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a><span data-ttu-id="265e5-123">Connectiviteit van buiten Azure</span><span class="sxs-lookup"><span data-stu-id="265e5-123">Connectivity from outside of Azure</span></span>

<span data-ttu-id="265e5-124">Als u verbinding vanaf buiten Azure maakt, uw verbindingen hebben een beleid van **Proxy** standaard.</span><span class="sxs-lookup"><span data-stu-id="265e5-124">If you are connecting from outside Azure, your connections have a connection policy of **Proxy** by default.</span></span> <span data-ttu-id="265e5-125">Een beleid van **Proxy** betekent dat dat Hallo TCP-sessie tot stand is gebracht via hello Azure SQL Database-gateway en alle latere pakketten via stromen Hallo gateway.</span><span class="sxs-lookup"><span data-stu-id="265e5-125">A policy of **Proxy** means that hello TCP session is established via hello Azure SQL Database gateway and all subsequent packets flow via hello gateway.</span></span> <span data-ttu-id="265e5-126">Hallo volgende diagram illustreert dit netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="265e5-126">hello following diagram illustrates this traffic flow.</span></span>

![overzicht van de architectuur](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a><span data-ttu-id="265e5-128">IP-adressen van Azure SQL Database-gateway</span><span class="sxs-lookup"><span data-stu-id="265e5-128">Azure SQL Database gateway IP addresses</span></span>

<span data-ttu-id="265e5-129">tooconnect tooan Azure SQL-database van lokale bronnen, moet u tooallow uitgaand verkeer toohello Azure SQL Database netwerkgateway voor uw Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="265e5-129">tooconnect tooan Azure SQL database from on-premises resources, you need tooallow outbound network traffic toohello Azure SQL Database gateway for your Azure region.</span></span> <span data-ttu-id="265e5-130">Uw verbindingen gaat alleen via Hallo gateway om verbinding te maken in de Proxy-modus, die de standaardeigenschap hello om verbinding te maken van lokale bronnen.</span><span class="sxs-lookup"><span data-stu-id="265e5-130">Your connections only go via hello gateway when connecting in Proxy mode, which is hello default when connecting from on-premises resources.</span></span>

<span data-ttu-id="265e5-131">Hallo volgende Tabellijsten Hallo primaire en secundaire IP-adressen van hello Azure SQL Database-gateway voor alle regio's van gegevens.</span><span class="sxs-lookup"><span data-stu-id="265e5-131">hello following table lists hello primary and secondary IPs of hello Azure SQL Database gateway for all data regions.</span></span> <span data-ttu-id="265e5-132">Er zijn twee IP-adressen voor bepaalde gebieden.</span><span class="sxs-lookup"><span data-stu-id="265e5-132">For some regions, there are two IP addresses.</span></span> <span data-ttu-id="265e5-133">In deze regio's, Hallo primaire IP-adres is het huidige IP-adres Hallo van Hallo gateway en Hallo tweede IP-adres is een failover-IP-adres.</span><span class="sxs-lookup"><span data-stu-id="265e5-133">In these regions, hello primary IP address is hello current IP address of hello gateway and hello second IP address is a failover IP address.</span></span> <span data-ttu-id="265e5-134">Hallo failover-adres is Hallo adres toowhich kunnen we uw server tookeep Hallo servicebeschikbaarheid hoge verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="265e5-134">hello failover address is hello address toowhich we might move your server tookeep hello service availability high.</span></span> <span data-ttu-id="265e5-135">Voor deze regio's, is het raadzaam dat u uitgaande tooboth Hallo IP-adressen toestaat.</span><span class="sxs-lookup"><span data-stu-id="265e5-135">For these regions, we recommend that you allow outbound tooboth hello IP addresses.</span></span> <span data-ttu-id="265e5-136">Hallo tweede IP-adres is het eigendom van Microsoft en luistert niet op alle services totdat deze is geactiveerd door Azure SQL Database tooaccept verbindingen.</span><span class="sxs-lookup"><span data-stu-id="265e5-136">hello second IP address is owned by Microsoft and does not listen in on any services until it is activated by Azure SQL Database tooaccept connections.</span></span>

| <span data-ttu-id="265e5-137">Naam regio</span><span class="sxs-lookup"><span data-stu-id="265e5-137">Region Name</span></span> | <span data-ttu-id="265e5-138">Primaire IP-adres</span><span class="sxs-lookup"><span data-stu-id="265e5-138">Primary IP address</span></span> | <span data-ttu-id="265e5-139">Secundaire IP-adres</span><span class="sxs-lookup"><span data-stu-id="265e5-139">Secondary IP address</span></span> |
| --- | --- |--- |
| <span data-ttu-id="265e5-140">Australië - oost</span><span class="sxs-lookup"><span data-stu-id="265e5-140">Australia East</span></span> | <span data-ttu-id="265e5-141">191.238.66.109</span><span class="sxs-lookup"><span data-stu-id="265e5-141">191.238.66.109</span></span> | <span data-ttu-id="265e5-142">13.75.149.87</span><span class="sxs-lookup"><span data-stu-id="265e5-142">13.75.149.87</span></span> |
| <span data-ttu-id="265e5-143">Australië - zuidoost</span><span class="sxs-lookup"><span data-stu-id="265e5-143">Australia South East</span></span> | <span data-ttu-id="265e5-144">191.239.192.109</span><span class="sxs-lookup"><span data-stu-id="265e5-144">191.239.192.109</span></span> | <span data-ttu-id="265e5-145">13.73.109.251</span><span class="sxs-lookup"><span data-stu-id="265e5-145">13.73.109.251</span></span> |
| <span data-ttu-id="265e5-146">Brazilië - zuid</span><span class="sxs-lookup"><span data-stu-id="265e5-146">Brazil South</span></span> | <span data-ttu-id="265e5-147">104.41.11.5</span><span class="sxs-lookup"><span data-stu-id="265e5-147">104.41.11.5</span></span> | |    
| <span data-ttu-id="265e5-148">Canada - midden</span><span class="sxs-lookup"><span data-stu-id="265e5-148">Canada Central</span></span> | <span data-ttu-id="265e5-149">40.85.224.249</span><span class="sxs-lookup"><span data-stu-id="265e5-149">40.85.224.249</span></span> | |    
| <span data-ttu-id="265e5-150">Canada - oost</span><span class="sxs-lookup"><span data-stu-id="265e5-150">Canada East</span></span> | <span data-ttu-id="265e5-151">40.86.226.166</span><span class="sxs-lookup"><span data-stu-id="265e5-151">40.86.226.166</span></span> | |
| <span data-ttu-id="265e5-152">VS - midden</span><span class="sxs-lookup"><span data-stu-id="265e5-152">Central US</span></span> | <span data-ttu-id="265e5-153">23.99.160.139</span><span class="sxs-lookup"><span data-stu-id="265e5-153">23.99.160.139</span></span> | <span data-ttu-id="265e5-154">13.67.215.62</span><span class="sxs-lookup"><span data-stu-id="265e5-154">13.67.215.62</span></span> |
| <span data-ttu-id="265e5-155">Oost-Azië</span><span class="sxs-lookup"><span data-stu-id="265e5-155">East Asia</span></span> | <span data-ttu-id="265e5-156">191.234.2.139</span><span class="sxs-lookup"><span data-stu-id="265e5-156">191.234.2.139</span></span> | <span data-ttu-id="265e5-157">52.175.33.150</span><span class="sxs-lookup"><span data-stu-id="265e5-157">52.175.33.150</span></span> |
| <span data-ttu-id="265e5-158">VS-Oost 1</span><span class="sxs-lookup"><span data-stu-id="265e5-158">East US 1</span></span> | <span data-ttu-id="265e5-159">191.238.6.43</span><span class="sxs-lookup"><span data-stu-id="265e5-159">191.238.6.43</span></span> | <span data-ttu-id="265e5-160">40.121.158.30</span><span class="sxs-lookup"><span data-stu-id="265e5-160">40.121.158.30</span></span> |
| <span data-ttu-id="265e5-161">VS - oost 2</span><span class="sxs-lookup"><span data-stu-id="265e5-161">East US 2</span></span> | <span data-ttu-id="265e5-162">191.239.224.107</span><span class="sxs-lookup"><span data-stu-id="265e5-162">191.239.224.107</span></span> | <span data-ttu-id="265e5-163">40.79.84.180</span><span class="sxs-lookup"><span data-stu-id="265e5-163">40.79.84.180</span></span> |
| <span data-ttu-id="265e5-164">India - midden</span><span class="sxs-lookup"><span data-stu-id="265e5-164">India Central</span></span> | <span data-ttu-id="265e5-165">104.211.96.159</span><span class="sxs-lookup"><span data-stu-id="265e5-165">104.211.96.159</span></span>  | |   
| <span data-ttu-id="265e5-166">India - zuid</span><span class="sxs-lookup"><span data-stu-id="265e5-166">India South</span></span> | <span data-ttu-id="265e5-167">104.211.224.146</span><span class="sxs-lookup"><span data-stu-id="265e5-167">104.211.224.146</span></span>  | |
| <span data-ttu-id="265e5-168">India - west</span><span class="sxs-lookup"><span data-stu-id="265e5-168">India West</span></span> | <span data-ttu-id="265e5-169">104.211.160.80</span><span class="sxs-lookup"><span data-stu-id="265e5-169">104.211.160.80</span></span> | |
| <span data-ttu-id="265e5-170">Japan - oost</span><span class="sxs-lookup"><span data-stu-id="265e5-170">Japan East</span></span> | <span data-ttu-id="265e5-171">191.237.240.43</span><span class="sxs-lookup"><span data-stu-id="265e5-171">191.237.240.43</span></span> | <span data-ttu-id="265e5-172">13.78.61.196</span><span class="sxs-lookup"><span data-stu-id="265e5-172">13.78.61.196</span></span> |
| <span data-ttu-id="265e5-173">Japan - west</span><span class="sxs-lookup"><span data-stu-id="265e5-173">Japan West</span></span> | <span data-ttu-id="265e5-174">191.238.68.11</span><span class="sxs-lookup"><span data-stu-id="265e5-174">191.238.68.11</span></span> | <span data-ttu-id="265e5-175">104.214.148.156</span><span class="sxs-lookup"><span data-stu-id="265e5-175">104.214.148.156</span></span> |
| <span data-ttu-id="265e5-176">Korea - centraal</span><span class="sxs-lookup"><span data-stu-id="265e5-176">Korea Central</span></span> | <span data-ttu-id="265e5-177">52.231.32.42</span><span class="sxs-lookup"><span data-stu-id="265e5-177">52.231.32.42</span></span> | |
| <span data-ttu-id="265e5-178">Korea - zuid</span><span class="sxs-lookup"><span data-stu-id="265e5-178">Korea South</span></span> | <span data-ttu-id="265e5-179">52.231.200.86</span><span class="sxs-lookup"><span data-stu-id="265e5-179">52.231.200.86</span></span> |  |
| <span data-ttu-id="265e5-180">Noord-centraal VS</span><span class="sxs-lookup"><span data-stu-id="265e5-180">North Central US</span></span> | <span data-ttu-id="265e5-181">23.98.55.75</span><span class="sxs-lookup"><span data-stu-id="265e5-181">23.98.55.75</span></span> | <span data-ttu-id="265e5-182">23.96.178.199</span><span class="sxs-lookup"><span data-stu-id="265e5-182">23.96.178.199</span></span> |
| <span data-ttu-id="265e5-183">Noord-Europa</span><span class="sxs-lookup"><span data-stu-id="265e5-183">North Europe</span></span> | <span data-ttu-id="265e5-184">191.235.193.75</span><span class="sxs-lookup"><span data-stu-id="265e5-184">191.235.193.75</span></span> | <span data-ttu-id="265e5-185">40.113.93.91</span><span class="sxs-lookup"><span data-stu-id="265e5-185">40.113.93.91</span></span> |
| <span data-ttu-id="265e5-186">Zuid-centraal VS</span><span class="sxs-lookup"><span data-stu-id="265e5-186">South Central US</span></span> | <span data-ttu-id="265e5-187">23.98.162.75</span><span class="sxs-lookup"><span data-stu-id="265e5-187">23.98.162.75</span></span> | <span data-ttu-id="265e5-188">13.66.62.124</span><span class="sxs-lookup"><span data-stu-id="265e5-188">13.66.62.124</span></span> |
| <span data-ttu-id="265e5-189">Zuidoost-Azië</span><span class="sxs-lookup"><span data-stu-id="265e5-189">South East Asia</span></span> | <span data-ttu-id="265e5-190">23.100.117.95</span><span class="sxs-lookup"><span data-stu-id="265e5-190">23.100.117.95</span></span> | <span data-ttu-id="265e5-191">104.43.15.0</span><span class="sxs-lookup"><span data-stu-id="265e5-191">104.43.15.0</span></span> |
| <span data-ttu-id="265e5-192">VK, noord</span><span class="sxs-lookup"><span data-stu-id="265e5-192">UK North</span></span> | <span data-ttu-id="265e5-193">13.87.97.210</span><span class="sxs-lookup"><span data-stu-id="265e5-193">13.87.97.210</span></span> | |
| <span data-ttu-id="265e5-194">VK Zuid 1</span><span class="sxs-lookup"><span data-stu-id="265e5-194">UK South 1</span></span> | <span data-ttu-id="265e5-195">51.140.184.11</span><span class="sxs-lookup"><span data-stu-id="265e5-195">51.140.184.11</span></span> | |    
| <span data-ttu-id="265e5-196">VK, zuid 2</span><span class="sxs-lookup"><span data-stu-id="265e5-196">UK South 2</span></span> | <span data-ttu-id="265e5-197">13.87.34.7</span><span class="sxs-lookup"><span data-stu-id="265e5-197">13.87.34.7</span></span> | |
| <span data-ttu-id="265e5-198">Verenigd Koninkrijk West</span><span class="sxs-lookup"><span data-stu-id="265e5-198">UK West</span></span> | <span data-ttu-id="265e5-199">51.141.8.11</span><span class="sxs-lookup"><span data-stu-id="265e5-199">51.141.8.11</span></span>  | |
| <span data-ttu-id="265e5-200">West-centraal VS</span><span class="sxs-lookup"><span data-stu-id="265e5-200">West Central US</span></span> | <span data-ttu-id="265e5-201">13.78.145.25</span><span class="sxs-lookup"><span data-stu-id="265e5-201">13.78.145.25</span></span> | |
| <span data-ttu-id="265e5-202">West-Europa</span><span class="sxs-lookup"><span data-stu-id="265e5-202">West Europe</span></span> | <span data-ttu-id="265e5-203">191.237.232.75</span><span class="sxs-lookup"><span data-stu-id="265e5-203">191.237.232.75</span></span> | <span data-ttu-id="265e5-204">40.68.37.158</span><span class="sxs-lookup"><span data-stu-id="265e5-204">40.68.37.158</span></span> |
| <span data-ttu-id="265e5-205">VS-West 1</span><span class="sxs-lookup"><span data-stu-id="265e5-205">West US 1</span></span> | <span data-ttu-id="265e5-206">23.99.34.75</span><span class="sxs-lookup"><span data-stu-id="265e5-206">23.99.34.75</span></span> | <span data-ttu-id="265e5-207">104.42.238.205</span><span class="sxs-lookup"><span data-stu-id="265e5-207">104.42.238.205</span></span> |
| <span data-ttu-id="265e5-208">VS - west 2</span><span class="sxs-lookup"><span data-stu-id="265e5-208">West US 2</span></span> | <span data-ttu-id="265e5-209">13.66.226.202</span><span class="sxs-lookup"><span data-stu-id="265e5-209">13.66.226.202</span></span>  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a><span data-ttu-id="265e5-210">Azure SQL Database verbindingsbeleid wijzigen</span><span class="sxs-lookup"><span data-stu-id="265e5-210">Change Azure SQL Database connection policy</span></span>

<span data-ttu-id="265e5-211">toochange hello verbindingsbeleid Azure SQL Database voor een Azure SQL Database-server, gebruik Hallo [REST-API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="265e5-211">toochange hello Azure SQL Database connection policy for an Azure SQL Database server, use hello [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span> 

- <span data-ttu-id="265e5-212">Als uw verbindingsbeleid voor de is ingesteld, te**Proxy**, alle netwerkapparaten stroom van pakketten via hello Azure SQL Database-gateway.</span><span class="sxs-lookup"><span data-stu-id="265e5-212">If your connection policy is set too**Proxy**, all network packets flow via hello Azure SQL Database gateway.</span></span> <span data-ttu-id="265e5-213">Voor deze instelling moet u tooallow uitgaande tooonly hello Azure SQL Database gateway IP.</span><span class="sxs-lookup"><span data-stu-id="265e5-213">For this setting, you need tooallow outbound tooonly hello Azure SQL Database gateway IP.</span></span> <span data-ttu-id="265e5-214">Met behulp van een instelling van **Proxy** heeft latentie van meer dan een instelling van **omleiden**.</span><span class="sxs-lookup"><span data-stu-id="265e5-214">Using a setting of **Proxy** has more latency than a setting of **Redirect**.</span></span> 
- <span data-ttu-id="265e5-215">Als uw verbindingsbeleid voor de tot stand **omleiden**, alle netwerkpakketten stromen rechtstreeks toohello middleware proxy.</span><span class="sxs-lookup"><span data-stu-id="265e5-215">If your connection policy is setting **Redirect**, all network packets flow directly toohello middleware proxy.</span></span> <span data-ttu-id="265e5-216">Voor deze instelling moet u tooallow uitgaande toomultiple IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="265e5-216">For this setting, you need tooallow outbound toomultiple IPs.</span></span> 

## <a name="script-toochange-connection-settings"></a><span data-ttu-id="265e5-217">Script toochange verbindingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="265e5-217">Script toochange connection settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="265e5-218">Dit script vereist Hallo [Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="265e5-218">This script requires hello [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>
>

<span data-ttu-id="265e5-219">Hallo volgende PowerShell-script toont hoe toochange verbindingsbeleid Hallo.</span><span class="sxs-lookup"><span data-stu-id="265e5-219">hello following PowerShell script shows how toochange hello connection policy.</span></span>

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

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a><span data-ttu-id="265e5-220">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="265e5-220">Next steps</span></span>

- <span data-ttu-id="265e5-221">Zie voor informatie over hoe toochange Hallo verbindingsbeleid Azure SQL Database voor een Azure SQL Database-server, [REST-API met behulp van maken of Update Server verbindingsbeleid Hallo](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="265e5-221">For information on how toochange hello Azure SQL Database connection policy for an Azure SQL Database server, see [Create or Update Server Connection Policy using hello REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span>
- <span data-ttu-id="265e5-222">Zie voor informatie over de werking van Azure SQL Database-verbinding voor clients die gebruikmaken van ADO.NET 4.5 of hoger, [poorten buiten 1433 ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="265e5-222">For information about Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version, see [Ports beyond 1433 for ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>
- <span data-ttu-id="265e5-223">Zie voor informatie over algemene toepassing ontwikkeling overzicht, [SQL Database ontwikkelen-overzicht](sql-database-develop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="265e5-223">For general application development overview information, see [SQL Database Application Development Overview](sql-database-develop-overview.md).</span></span>
