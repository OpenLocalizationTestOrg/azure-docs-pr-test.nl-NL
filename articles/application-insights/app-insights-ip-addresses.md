---
title: IP-adressen die worden gebruikt door de Application Insights | Microsoft Docs
description: Firewall-uitzonderingen die zijn vereist voor Application Insights
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 44d989f8-bae9-40ff-bfd5-8343d3e59358
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 8/11/2017
ms.author: bwren
ms.openlocfilehash: 3bb076c63223fc1567c6b7b25c1a513bbc81ed58
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="ip-addresses-used-by-application-insights"></a><span data-ttu-id="f9df8-103">IP-adressen die worden gebruikt door Application Insights</span><span class="sxs-lookup"><span data-stu-id="f9df8-103">IP addresses used by Application Insights</span></span>
<span data-ttu-id="f9df8-104">De [Azure Application Insights](app-insights-overview.md) service gebruikt een aantal IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="f9df8-104">The [Azure Application Insights](app-insights-overview.md) service uses a number of IP addresses.</span></span> <span data-ttu-id="f9df8-105">Mogelijk moet u weten van deze adressen als de app die u bewaakt achter een firewall wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="f9df8-105">You might need to know these addresses if the app that you are monitoring is hosted behind a firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="f9df8-106">Hoewel deze adressen statisch zijn, is het mogelijk dat moeten we ze van tijd tot tijd te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f9df8-106">Although these addresses are static, it's possible that we will need to change them from time to time.</span></span>
> 
> 

## <a name="outgoing-ports"></a><span data-ttu-id="f9df8-107">Uitgaande poorten</span><span class="sxs-lookup"><span data-stu-id="f9df8-107">Outgoing ports</span></span>
<span data-ttu-id="f9df8-108">U moet een aantal uitgaande poorten openen in de firewall van uw server om toe te staan van de Application Insights-SDK en/of Status Monitor om gegevens te verzenden naar de portal:</span><span class="sxs-lookup"><span data-stu-id="f9df8-108">You need to open some outgoing ports in your server's firewall to allow the Application Insights SDK and/or Status Monitor to send data to the portal:</span></span>

| <span data-ttu-id="f9df8-109">Doel</span><span class="sxs-lookup"><span data-stu-id="f9df8-109">Purpose</span></span> | <span data-ttu-id="f9df8-110">URL</span><span class="sxs-lookup"><span data-stu-id="f9df8-110">URL</span></span> | <span data-ttu-id="f9df8-111">IP</span><span class="sxs-lookup"><span data-stu-id="f9df8-111">IP</span></span> | <span data-ttu-id="f9df8-112">Poorten</span><span class="sxs-lookup"><span data-stu-id="f9df8-112">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f9df8-113">Telemetrie</span><span class="sxs-lookup"><span data-stu-id="f9df8-113">Telemetry</span></span> |<span data-ttu-id="f9df8-114">DC.Services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="f9df8-114">dc.services.visualstudio.com</span></span><br/><span data-ttu-id="f9df8-115">DC.applicationinsights.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="f9df8-115">dc.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="f9df8-116">40.114.241.141</span><span class="sxs-lookup"><span data-stu-id="f9df8-116">40.114.241.141</span></span><br/><span data-ttu-id="f9df8-117">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="f9df8-117">104.45.136.42</span></span><br/><span data-ttu-id="f9df8-118">40.84.189.107</span><span class="sxs-lookup"><span data-stu-id="f9df8-118">40.84.189.107</span></span><br/><span data-ttu-id="f9df8-119">168.63.242.221</span><span class="sxs-lookup"><span data-stu-id="f9df8-119">168.63.242.221</span></span><br/><span data-ttu-id="f9df8-120">52.167.221.184</span><span class="sxs-lookup"><span data-stu-id="f9df8-120">52.167.221.184</span></span><br/><span data-ttu-id="f9df8-121">52.169.64.244</span><span class="sxs-lookup"><span data-stu-id="f9df8-121">52.169.64.244</span></span> |<span data-ttu-id="f9df8-122">443</span><span class="sxs-lookup"><span data-stu-id="f9df8-122">443</span></span> |
| <span data-ttu-id="f9df8-123">Metrische gegevens livestream</span><span class="sxs-lookup"><span data-stu-id="f9df8-123">Live Metrics Stream</span></span> |<span data-ttu-id="f9df8-124">RT.Services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="f9df8-124">rt.services.visualstudio.com</span></span><br/><span data-ttu-id="f9df8-125">RT.applicationinsights.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="f9df8-125">rt.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="f9df8-126">23.96.28.38</span><span class="sxs-lookup"><span data-stu-id="f9df8-126">23.96.28.38</span></span><br/><span data-ttu-id="f9df8-127">13.92.40.198</span><span class="sxs-lookup"><span data-stu-id="f9df8-127">13.92.40.198</span></span> |<span data-ttu-id="f9df8-128">443</span><span class="sxs-lookup"><span data-stu-id="f9df8-128">443</span></span> |
| <span data-ttu-id="f9df8-129">Interne telemetrie</span><span class="sxs-lookup"><span data-stu-id="f9df8-129">Internal Telemetry</span></span> |<span data-ttu-id="f9df8-130">breeze.aimon.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="f9df8-130">breeze.aimon.applicationinsights.io</span></span> |<span data-ttu-id="f9df8-131">52.161.11.71</span><span class="sxs-lookup"><span data-stu-id="f9df8-131">52.161.11.71</span></span> |<span data-ttu-id="f9df8-132">443</span><span class="sxs-lookup"><span data-stu-id="f9df8-132">443</span></span> |

## <a name="status-monitor"></a><span data-ttu-id="f9df8-133">Statuscontrole</span><span class="sxs-lookup"><span data-stu-id="f9df8-133">Status Monitor</span></span>
<span data-ttu-id="f9df8-134">Status monitorconfiguratie: alleen nodig wanneer u wijzigingen aanbrengt.</span><span class="sxs-lookup"><span data-stu-id="f9df8-134">Status Monitor Configuration - needed only when making changes.</span></span>

| <span data-ttu-id="f9df8-135">Doel</span><span class="sxs-lookup"><span data-stu-id="f9df8-135">Purpose</span></span> | <span data-ttu-id="f9df8-136">URL</span><span class="sxs-lookup"><span data-stu-id="f9df8-136">URL</span></span> | <span data-ttu-id="f9df8-137">IP</span><span class="sxs-lookup"><span data-stu-id="f9df8-137">IP</span></span> | <span data-ttu-id="f9df8-138">Poorten</span><span class="sxs-lookup"><span data-stu-id="f9df8-138">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f9df8-139">Configuratie</span><span class="sxs-lookup"><span data-stu-id="f9df8-139">Configuration</span></span> |`management.core.windows.net` | |`443` |
| <span data-ttu-id="f9df8-140">Configuratie</span><span class="sxs-lookup"><span data-stu-id="f9df8-140">Configuration</span></span> |`management.azure.com` | |`443` |
| <span data-ttu-id="f9df8-141">Configuratie</span><span class="sxs-lookup"><span data-stu-id="f9df8-141">Configuration</span></span> |`login.windows.net` | |`443` |
| <span data-ttu-id="f9df8-142">Configuratie</span><span class="sxs-lookup"><span data-stu-id="f9df8-142">Configuration</span></span> |`login.microsoftonline.com` | |`443` |
| <span data-ttu-id="f9df8-143">Configuratie</span><span class="sxs-lookup"><span data-stu-id="f9df8-143">Configuration</span></span> |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| <span data-ttu-id="f9df8-144">Configuratie</span><span class="sxs-lookup"><span data-stu-id="f9df8-144">Configuration</span></span> |`auth.gfx.ms` | |`443` |
| <span data-ttu-id="f9df8-145">Configuratie</span><span class="sxs-lookup"><span data-stu-id="f9df8-145">Configuration</span></span> |`login.live.com` | |`443` |
| <span data-ttu-id="f9df8-146">Installeren</span><span class="sxs-lookup"><span data-stu-id="f9df8-146">Installation</span></span> |`packages.nuget.org` | |`443` |

## <a name="hockeyapp"></a><span data-ttu-id="f9df8-147">HockeyApp</span><span class="sxs-lookup"><span data-stu-id="f9df8-147">HockeyApp</span></span>
| <span data-ttu-id="f9df8-148">Doel</span><span class="sxs-lookup"><span data-stu-id="f9df8-148">Purpose</span></span> | <span data-ttu-id="f9df8-149">URL</span><span class="sxs-lookup"><span data-stu-id="f9df8-149">URL</span></span> | <span data-ttu-id="f9df8-150">IP</span><span class="sxs-lookup"><span data-stu-id="f9df8-150">IP</span></span> | <span data-ttu-id="f9df8-151">Poorten</span><span class="sxs-lookup"><span data-stu-id="f9df8-151">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f9df8-152">Crashgegevens</span><span class="sxs-lookup"><span data-stu-id="f9df8-152">Crash data</span></span> |<span data-ttu-id="f9df8-153">gate.hockeyapp.NET</span><span class="sxs-lookup"><span data-stu-id="f9df8-153">gate.hockeyapp.net</span></span> |<span data-ttu-id="f9df8-154">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="f9df8-154">104.45.136.42</span></span> |<span data-ttu-id="f9df8-155">80, 443</span><span class="sxs-lookup"><span data-stu-id="f9df8-155">80, 443</span></span> |

## <a name="availability-tests"></a><span data-ttu-id="f9df8-156">Beschikbaarheidstests</span><span class="sxs-lookup"><span data-stu-id="f9df8-156">Availability tests</span></span>
<span data-ttu-id="f9df8-157">Dit is de lijst met adressen waaruit [webtests voor beschikbaarheid](app-insights-monitor-web-app-availability.md) worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f9df8-157">This is the list of addresses from which [availability web tests](app-insights-monitor-web-app-availability.md) are run.</span></span> <span data-ttu-id="f9df8-158">Als u wilt uitvoeren van webtests van uw app, maar de webserver beperkt is tot specifieke clients van dienst, hebt u toe dat binnenkomend verkeer op onze beschikbaarheid test-servers.</span><span class="sxs-lookup"><span data-stu-id="f9df8-158">If you want to run web tests on your app, but your web server is restricted to serving specific clients, then you will have to permit incoming traffic from our availability test servers.</span></span>

<span data-ttu-id="f9df8-159">Open de poorten 80 (http) en 443 (https) voor binnenkomend verkeer naar deze adressen (IP-adressen zijn gegroepeerd op locatie):</span><span class="sxs-lookup"><span data-stu-id="f9df8-159">Open ports 80 (http) and 443 (https) for incoming traffic from these addresses (IP addresses are grouped by location):</span></span>

```
AU : Sydney
13.70.83.252
13.75.150.96
13.75.153.9
13.75.158.185
BR : Sao Paulo
191.232.32.122
191.232.172.45
191.232.176.218
191.232.191.225
CH : Zurich
94.245.66.43
94.245.66.44
94.245.66.45
94.245.66.48
FR : Paris
94.245.72.44
94.245.72.45
94.245.72.46
94.245.72.49
94.245.72.52
94.245.72.53
HK : Hong Kong
13.75.121.122
23.99.115.153
23.99.123.38
23.102.232.186
52.175.38.49
52.175.39.103
IE : Dublin
13.74.184.101
13.74.185.160
40.69.200.198
52.164.224.46
52.169.12.203
52.169.14.11
52.169.237.149
52.178.183.105
JP : Kawaguchi
52.243.33.33
52.243.33.141
52.243.35.253
52.243.41.117
NL : Amsterdam
52.174.166.113
52.174.178.96
52.174.31.140
52.174.35.14
52.178.104.23
52.178.109.190
52.178.111.139
52.233.166.221
RU : Moscow
94.245.82.32
94.245.82.33
94.245.82.37
94.245.82.38
SE : Stockholm
94.245.78.40
94.245.78.41
94.245.78.42
94.245.78.45
SG : Singapore
52.187.29.7
52.187.179.17
52.187.76.248
52.187.43.24
52.163.57.91
52.187.30.120
US : CA-San Jose
104.45.228.236
104.45.237.251
13.64.152.110
13.64.156.54
13.64.232.251
13.64.236.105
13.91.94.59
40.118.131.182
40.83.189.192
40.83.215.122
US : FL-Miami
65.54.78.49
65.54.78.50
65.54.78.51
65.54.78.54
65.54.78.57
65.54.78.58
65.54.78.59
65.54.78.60
US : IL-Chicago
23.96.247.139
23.96.249.113
52.162.124.242
52.162.126.139
52.162.241.147
52.162.246.222
52.162.247.136
52.237.153.231
52.237.154.216
52.237.156.14
52.237.157.218
52.237.157.37
US : TX-San Antonio
104.210.145.106
13.84.176.24
13.84.49.16
13.85.11.137
13.85.26.248
13.85.69.145
52.171.136.162
52.171.141.253
52.171.57.172
52.171.58.140
US : VA-Ashburn
13.82.218.95
13.90.96.71
13.90.98.52
13.92.137.70
40.85.187.235
40.87.61.61
52.168.8.247
52.170.38.79
52.170.80.61
52.179.9.26

```  

## <a name="data-access-api"></a><span data-ttu-id="f9df8-160">API voor gegevenstoegang</span><span class="sxs-lookup"><span data-stu-id="f9df8-160">Data access API</span></span>
| <span data-ttu-id="f9df8-161">Doel</span><span class="sxs-lookup"><span data-stu-id="f9df8-161">Purpose</span></span> | <span data-ttu-id="f9df8-162">URI</span><span class="sxs-lookup"><span data-stu-id="f9df8-162">URI</span></span> | <span data-ttu-id="f9df8-163">IP</span><span class="sxs-lookup"><span data-stu-id="f9df8-163">IP</span></span> | <span data-ttu-id="f9df8-164">Poorten</span><span class="sxs-lookup"><span data-stu-id="f9df8-164">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f9df8-165">API</span><span class="sxs-lookup"><span data-stu-id="f9df8-165">API</span></span> |<span data-ttu-id="f9df8-166">API.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="f9df8-166">api.applicationinsights.io</span></span><br/><span data-ttu-id="f9df8-167">api1.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="f9df8-167">api1.applicationinsights.io</span></span><br/><span data-ttu-id="f9df8-168">api2.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="f9df8-168">api2.applicationinsights.io</span></span><br/><span data-ttu-id="f9df8-169">api3.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="f9df8-169">api3.applicationinsights.io</span></span><br/><span data-ttu-id="f9df8-170">api4.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="f9df8-170">api4.applicationinsights.io</span></span><br/><span data-ttu-id="f9df8-171">api5.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="f9df8-171">api5.applicationinsights.io</span></span> |<span data-ttu-id="f9df8-172">13.82.26.252</span><span class="sxs-lookup"><span data-stu-id="f9df8-172">13.82.26.252</span></span><br/><span data-ttu-id="f9df8-173">40.76.213.73</span><span class="sxs-lookup"><span data-stu-id="f9df8-173">40.76.213.73</span></span> |<span data-ttu-id="f9df8-174">80,443</span><span class="sxs-lookup"><span data-stu-id="f9df8-174">80,443</span></span> |
| <span data-ttu-id="f9df8-175">API-docs</span><span class="sxs-lookup"><span data-stu-id="f9df8-175">API docs</span></span> |<span data-ttu-id="f9df8-176">dev.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="f9df8-176">dev.applicationinsights.io</span></span><br/><span data-ttu-id="f9df8-177">dev.applicationinsights.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="f9df8-177">dev.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="f9df8-178">dev.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="f9df8-178">dev.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="f9df8-179">www.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="f9df8-179">www.applicationinsights.io</span></span><br/><span data-ttu-id="f9df8-180">www.applicationinsights.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="f9df8-180">www.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="f9df8-181">www.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="f9df8-181">www.aisvc.visualstudio.com</span></span> |<span data-ttu-id="f9df8-182">13.82.24.149</span><span class="sxs-lookup"><span data-stu-id="f9df8-182">13.82.24.149</span></span><br/><span data-ttu-id="f9df8-183">40.114.82.10</span><span class="sxs-lookup"><span data-stu-id="f9df8-183">40.114.82.10</span></span> |<span data-ttu-id="f9df8-184">80,443</span><span class="sxs-lookup"><span data-stu-id="f9df8-184">80,443</span></span> |
| <span data-ttu-id="f9df8-185">Interne API</span><span class="sxs-lookup"><span data-stu-id="f9df8-185">Internal API</span></span> |<span data-ttu-id="f9df8-186">aigs.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="f9df8-186">aigs.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="f9df8-187">aigs1.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="f9df8-187">aigs1.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="f9df8-188">aigs2.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="f9df8-188">aigs2.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="f9df8-189">aigs3.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="f9df8-189">aigs3.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="f9df8-190">aigs4.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="f9df8-190">aigs4.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="f9df8-191">aigs5.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="f9df8-191">aigs5.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="f9df8-192">aigs6.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="f9df8-192">aigs6.aisvc.visualstudio.com</span></span> |<span data-ttu-id="f9df8-193">dynamische</span><span class="sxs-lookup"><span data-stu-id="f9df8-193">dynamic</span></span>|<span data-ttu-id="f9df8-194">443</span><span class="sxs-lookup"><span data-stu-id="f9df8-194">443</span></span> |

## <a name="application-insights-analytics"></a><span data-ttu-id="f9df8-195">Application Insights Analytics</span><span class="sxs-lookup"><span data-stu-id="f9df8-195">Application Insights Analytics</span></span>

| <span data-ttu-id="f9df8-196">Doel</span><span class="sxs-lookup"><span data-stu-id="f9df8-196">Purpose</span></span> | <span data-ttu-id="f9df8-197">URI</span><span class="sxs-lookup"><span data-stu-id="f9df8-197">URI</span></span> | <span data-ttu-id="f9df8-198">IP</span><span class="sxs-lookup"><span data-stu-id="f9df8-198">IP</span></span> | <span data-ttu-id="f9df8-199">Poorten</span><span class="sxs-lookup"><span data-stu-id="f9df8-199">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f9df8-200">Analytics-Portal</span><span class="sxs-lookup"><span data-stu-id="f9df8-200">Analytics Portal</span></span> | <span data-ttu-id="f9df8-201">Analytics.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="f9df8-201">analytics.applicationinsights.io</span></span> | <span data-ttu-id="f9df8-202">dynamische</span><span class="sxs-lookup"><span data-stu-id="f9df8-202">dynamic</span></span> | <span data-ttu-id="f9df8-203">80,443</span><span class="sxs-lookup"><span data-stu-id="f9df8-203">80,443</span></span> |
| <span data-ttu-id="f9df8-204">CDN</span><span class="sxs-lookup"><span data-stu-id="f9df8-204">CDN</span></span> | <span data-ttu-id="f9df8-205">applicationanalytics.azureedge.NET</span><span class="sxs-lookup"><span data-stu-id="f9df8-205">applicationanalytics.azureedge.net</span></span> | <span data-ttu-id="f9df8-206">dynamische</span><span class="sxs-lookup"><span data-stu-id="f9df8-206">dynamic</span></span> | <span data-ttu-id="f9df8-207">80,443</span><span class="sxs-lookup"><span data-stu-id="f9df8-207">80,443</span></span> |
| <span data-ttu-id="f9df8-208">Media CDN</span><span class="sxs-lookup"><span data-stu-id="f9df8-208">Media CDN</span></span> | <span data-ttu-id="f9df8-209">applicationanalyticsmedia.azureedge.NET</span><span class="sxs-lookup"><span data-stu-id="f9df8-209">applicationanalyticsmedia.azureedge.net</span></span> | <span data-ttu-id="f9df8-210">dynamische</span><span class="sxs-lookup"><span data-stu-id="f9df8-210">dynamic</span></span> | <span data-ttu-id="f9df8-211">80,443</span><span class="sxs-lookup"><span data-stu-id="f9df8-211">80,443</span></span> |

<span data-ttu-id="f9df8-212">Opmerking: *. applicationinsights.io domein is eigendom van Application Insights-team.</span><span class="sxs-lookup"><span data-stu-id="f9df8-212">Note: *.applicationinsights.io domain is owned by Application Insights team.</span></span>

## <a name="application-insights-azure-portal-extension"></a><span data-ttu-id="f9df8-213">Application Insights Azure Portal-extensie</span><span class="sxs-lookup"><span data-stu-id="f9df8-213">Application Insights Azure Portal Extension</span></span>

| <span data-ttu-id="f9df8-214">Doel</span><span class="sxs-lookup"><span data-stu-id="f9df8-214">Purpose</span></span> | <span data-ttu-id="f9df8-215">URI</span><span class="sxs-lookup"><span data-stu-id="f9df8-215">URI</span></span> | <span data-ttu-id="f9df8-216">IP</span><span class="sxs-lookup"><span data-stu-id="f9df8-216">IP</span></span> | <span data-ttu-id="f9df8-217">Poorten</span><span class="sxs-lookup"><span data-stu-id="f9df8-217">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f9df8-218">Application Insights-extensie</span><span class="sxs-lookup"><span data-stu-id="f9df8-218">Application Insights Extension</span></span> | <span data-ttu-id="f9df8-219">stamp2.app.insightsportal.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="f9df8-219">stamp2.app.insightsportal.visualstudio.com</span></span> | <span data-ttu-id="f9df8-220">dynamische</span><span class="sxs-lookup"><span data-stu-id="f9df8-220">dynamic</span></span> | <span data-ttu-id="f9df8-221">80,443</span><span class="sxs-lookup"><span data-stu-id="f9df8-221">80,443</span></span> |
| <span data-ttu-id="f9df8-222">Application Insights-extensie CDN</span><span class="sxs-lookup"><span data-stu-id="f9df8-222">Application Insights Extension CDN</span></span> | <span data-ttu-id="f9df8-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="f9df8-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="f9df8-224">insightsportal prod2-asiae cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="f9df8-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="f9df8-225">insightsportal-cdn-aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="f9df8-225">insightsportal-cdn-aimon.applicationinsights.io</span></span> | <span data-ttu-id="f9df8-226">dynamische</span><span class="sxs-lookup"><span data-stu-id="f9df8-226">dynamic</span></span> | <span data-ttu-id="f9df8-227">80,443</span><span class="sxs-lookup"><span data-stu-id="f9df8-227">80,443</span></span> |

## <a name="application-insights-sdks"></a><span data-ttu-id="f9df8-228">Application Insights-SDK 's</span><span class="sxs-lookup"><span data-stu-id="f9df8-228">Application Insights SDKs</span></span>

| <span data-ttu-id="f9df8-229">Doel</span><span class="sxs-lookup"><span data-stu-id="f9df8-229">Purpose</span></span> | <span data-ttu-id="f9df8-230">URI</span><span class="sxs-lookup"><span data-stu-id="f9df8-230">URI</span></span> | <span data-ttu-id="f9df8-231">IP</span><span class="sxs-lookup"><span data-stu-id="f9df8-231">IP</span></span> | <span data-ttu-id="f9df8-232">Poorten</span><span class="sxs-lookup"><span data-stu-id="f9df8-232">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f9df8-233">Application Insights-SDK voor JS CDN</span><span class="sxs-lookup"><span data-stu-id="f9df8-233">Application Insights JS SDK CDN</span></span> | <span data-ttu-id="f9df8-234">az416426.VO.msecnd.NET</span><span class="sxs-lookup"><span data-stu-id="f9df8-234">az416426.vo.msecnd.net</span></span> | <span data-ttu-id="f9df8-235">dynamische</span><span class="sxs-lookup"><span data-stu-id="f9df8-235">dynamic</span></span> | <span data-ttu-id="f9df8-236">80,443</span><span class="sxs-lookup"><span data-stu-id="f9df8-236">80,443</span></span> |
| <span data-ttu-id="f9df8-237">Application Insights Java SDK</span><span class="sxs-lookup"><span data-stu-id="f9df8-237">Application Insights Java SDK</span></span> | <span data-ttu-id="f9df8-238">aijavasdk.BLOB.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="f9df8-238">aijavasdk.blob.core.windows.net</span></span> | <span data-ttu-id="f9df8-239">dynamische</span><span class="sxs-lookup"><span data-stu-id="f9df8-239">dynamic</span></span> | <span data-ttu-id="f9df8-240">80,443</span><span class="sxs-lookup"><span data-stu-id="f9df8-240">80,443</span></span> |

## <a name="profiler"></a><span data-ttu-id="f9df8-241">Profiler</span><span class="sxs-lookup"><span data-stu-id="f9df8-241">Profiler</span></span>

| <span data-ttu-id="f9df8-242">Doel</span><span class="sxs-lookup"><span data-stu-id="f9df8-242">Purpose</span></span> | <span data-ttu-id="f9df8-243">URI</span><span class="sxs-lookup"><span data-stu-id="f9df8-243">URI</span></span> | <span data-ttu-id="f9df8-244">IP</span><span class="sxs-lookup"><span data-stu-id="f9df8-244">IP</span></span> | <span data-ttu-id="f9df8-245">Poorten</span><span class="sxs-lookup"><span data-stu-id="f9df8-245">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f9df8-246">Agent</span><span class="sxs-lookup"><span data-stu-id="f9df8-246">Agent</span></span> | <span data-ttu-id="f9df8-247">Agent.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="f9df8-247">agent.azureserviceprofiler.net</span></span><br/><span data-ttu-id="f9df8-248">*. agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="f9df8-248">*.agent.azureserviceprofiler.net</span></span> | <span data-ttu-id="f9df8-249">dynamische</span><span class="sxs-lookup"><span data-stu-id="f9df8-249">dynamic</span></span> | <span data-ttu-id="f9df8-250">443</span><span class="sxs-lookup"><span data-stu-id="f9df8-250">443</span></span>
| <span data-ttu-id="f9df8-251">Portal</span><span class="sxs-lookup"><span data-stu-id="f9df8-251">Portal</span></span> | <span data-ttu-id="f9df8-252">gateway.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="f9df8-252">gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="f9df8-253">dynamische</span><span class="sxs-lookup"><span data-stu-id="f9df8-253">dynamic</span></span> | <span data-ttu-id="f9df8-254">443</span><span class="sxs-lookup"><span data-stu-id="f9df8-254">443</span></span>
| <span data-ttu-id="f9df8-255">Storage</span><span class="sxs-lookup"><span data-stu-id="f9df8-255">Storage</span></span> | <span data-ttu-id="f9df8-256">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="f9df8-256">*.core.windows.net</span></span> | <span data-ttu-id="f9df8-257">dynamische</span><span class="sxs-lookup"><span data-stu-id="f9df8-257">dynamic</span></span> | <span data-ttu-id="f9df8-258">443</span><span class="sxs-lookup"><span data-stu-id="f9df8-258">443</span></span>

## <a name="snapshot-debugger"></a><span data-ttu-id="f9df8-259">Snapshot Debugger</span><span class="sxs-lookup"><span data-stu-id="f9df8-259">Snapshot Debugger</span></span>

| <span data-ttu-id="f9df8-260">Doel</span><span class="sxs-lookup"><span data-stu-id="f9df8-260">Purpose</span></span> | <span data-ttu-id="f9df8-261">URI</span><span class="sxs-lookup"><span data-stu-id="f9df8-261">URI</span></span> | <span data-ttu-id="f9df8-262">IP</span><span class="sxs-lookup"><span data-stu-id="f9df8-262">IP</span></span> | <span data-ttu-id="f9df8-263">Poorten</span><span class="sxs-lookup"><span data-stu-id="f9df8-263">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f9df8-264">Agent</span><span class="sxs-lookup"><span data-stu-id="f9df8-264">Agent</span></span> | <span data-ttu-id="f9df8-265">ppe.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="f9df8-265">ppe.azureserviceprofiler.net</span></span><br/><span data-ttu-id="f9df8-266">*. ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="f9df8-266">*.ppe.azureserviceprofiler.net</span></span> | <span data-ttu-id="f9df8-267">dynamische</span><span class="sxs-lookup"><span data-stu-id="f9df8-267">dynamic</span></span> | <span data-ttu-id="f9df8-268">443</span><span class="sxs-lookup"><span data-stu-id="f9df8-268">443</span></span>
| <span data-ttu-id="f9df8-269">Portal</span><span class="sxs-lookup"><span data-stu-id="f9df8-269">Portal</span></span> | <span data-ttu-id="f9df8-270">ppe.gateway.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="f9df8-270">ppe.gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="f9df8-271">dynamische</span><span class="sxs-lookup"><span data-stu-id="f9df8-271">dynamic</span></span> | <span data-ttu-id="f9df8-272">443</span><span class="sxs-lookup"><span data-stu-id="f9df8-272">443</span></span>
| <span data-ttu-id="f9df8-273">Storage</span><span class="sxs-lookup"><span data-stu-id="f9df8-273">Storage</span></span> | <span data-ttu-id="f9df8-274">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="f9df8-274">*.core.windows.net</span></span> | <span data-ttu-id="f9df8-275">dynamische</span><span class="sxs-lookup"><span data-stu-id="f9df8-275">dynamic</span></span> | <span data-ttu-id="f9df8-276">443</span><span class="sxs-lookup"><span data-stu-id="f9df8-276">443</span></span>
