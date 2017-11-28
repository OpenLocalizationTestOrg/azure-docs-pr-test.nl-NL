---
title: aaaIP adressen die worden gebruikt door de Application Insights | Microsoft Docs
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
ms.openlocfilehash: 2c101b8da2ba9594fbff607f4f7551cda80c3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="ip-addresses-used-by-application-insights"></a><span data-ttu-id="d9c97-103">IP-adressen die worden gebruikt door Application Insights</span><span class="sxs-lookup"><span data-stu-id="d9c97-103">IP addresses used by Application Insights</span></span>
<span data-ttu-id="d9c97-104">Hallo [Azure Application Insights](app-insights-overview.md) service gebruikt een aantal IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="d9c97-104">hello [Azure Application Insights](app-insights-overview.md) service uses a number of IP addresses.</span></span> <span data-ttu-id="d9c97-105">Mogelijk moet u tooknow deze adressen als Hallo-app die u bewaakt achter een firewall wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="d9c97-105">You might need tooknow these addresses if hello app that you are monitoring is hosted behind a firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="d9c97-106">Hoewel deze adressen statisch zijn, is het mogelijk dat we toochange moeten van tijd tootime.</span><span class="sxs-lookup"><span data-stu-id="d9c97-106">Although these addresses are static, it's possible that we will need toochange them from time tootime.</span></span>
> 
> 

## <a name="outgoing-ports"></a><span data-ttu-id="d9c97-107">Uitgaande poorten</span><span class="sxs-lookup"><span data-stu-id="d9c97-107">Outgoing ports</span></span>
<span data-ttu-id="d9c97-108">Tooopen moet u een aantal uitgaande poorten in uw server firewall tooallow Hallo Application Insights-SDK en/of de Status Monitor toosend gegevensportal toohello:</span><span class="sxs-lookup"><span data-stu-id="d9c97-108">You need tooopen some outgoing ports in your server's firewall tooallow hello Application Insights SDK and/or Status Monitor toosend data toohello portal:</span></span>

| <span data-ttu-id="d9c97-109">Doel</span><span class="sxs-lookup"><span data-stu-id="d9c97-109">Purpose</span></span> | <span data-ttu-id="d9c97-110">URL</span><span class="sxs-lookup"><span data-stu-id="d9c97-110">URL</span></span> | <span data-ttu-id="d9c97-111">IP</span><span class="sxs-lookup"><span data-stu-id="d9c97-111">IP</span></span> | <span data-ttu-id="d9c97-112">Poorten</span><span class="sxs-lookup"><span data-stu-id="d9c97-112">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d9c97-113">Telemetrie</span><span class="sxs-lookup"><span data-stu-id="d9c97-113">Telemetry</span></span> |<span data-ttu-id="d9c97-114">DC.Services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d9c97-114">dc.services.visualstudio.com</span></span><br/><span data-ttu-id="d9c97-115">DC.applicationinsights.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="d9c97-115">dc.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="d9c97-116">40.114.241.141</span><span class="sxs-lookup"><span data-stu-id="d9c97-116">40.114.241.141</span></span><br/><span data-ttu-id="d9c97-117">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="d9c97-117">104.45.136.42</span></span><br/><span data-ttu-id="d9c97-118">40.84.189.107</span><span class="sxs-lookup"><span data-stu-id="d9c97-118">40.84.189.107</span></span><br/><span data-ttu-id="d9c97-119">168.63.242.221</span><span class="sxs-lookup"><span data-stu-id="d9c97-119">168.63.242.221</span></span><br/><span data-ttu-id="d9c97-120">52.167.221.184</span><span class="sxs-lookup"><span data-stu-id="d9c97-120">52.167.221.184</span></span><br/><span data-ttu-id="d9c97-121">52.169.64.244</span><span class="sxs-lookup"><span data-stu-id="d9c97-121">52.169.64.244</span></span> |<span data-ttu-id="d9c97-122">443</span><span class="sxs-lookup"><span data-stu-id="d9c97-122">443</span></span> |
| <span data-ttu-id="d9c97-123">Metrische gegevens livestream</span><span class="sxs-lookup"><span data-stu-id="d9c97-123">Live Metrics Stream</span></span> |<span data-ttu-id="d9c97-124">RT.Services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d9c97-124">rt.services.visualstudio.com</span></span><br/><span data-ttu-id="d9c97-125">RT.applicationinsights.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="d9c97-125">rt.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="d9c97-126">23.96.28.38</span><span class="sxs-lookup"><span data-stu-id="d9c97-126">23.96.28.38</span></span><br/><span data-ttu-id="d9c97-127">13.92.40.198</span><span class="sxs-lookup"><span data-stu-id="d9c97-127">13.92.40.198</span></span> |<span data-ttu-id="d9c97-128">443</span><span class="sxs-lookup"><span data-stu-id="d9c97-128">443</span></span> |
| <span data-ttu-id="d9c97-129">Interne telemetrie</span><span class="sxs-lookup"><span data-stu-id="d9c97-129">Internal Telemetry</span></span> |<span data-ttu-id="d9c97-130">breeze.aimon.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="d9c97-130">breeze.aimon.applicationinsights.io</span></span> |<span data-ttu-id="d9c97-131">52.161.11.71</span><span class="sxs-lookup"><span data-stu-id="d9c97-131">52.161.11.71</span></span> |<span data-ttu-id="d9c97-132">443</span><span class="sxs-lookup"><span data-stu-id="d9c97-132">443</span></span> |

## <a name="status-monitor"></a><span data-ttu-id="d9c97-133">Statuscontrole</span><span class="sxs-lookup"><span data-stu-id="d9c97-133">Status Monitor</span></span>
<span data-ttu-id="d9c97-134">Status monitorconfiguratie: alleen nodig wanneer u wijzigingen aanbrengt.</span><span class="sxs-lookup"><span data-stu-id="d9c97-134">Status Monitor Configuration - needed only when making changes.</span></span>

| <span data-ttu-id="d9c97-135">Doel</span><span class="sxs-lookup"><span data-stu-id="d9c97-135">Purpose</span></span> | <span data-ttu-id="d9c97-136">URL</span><span class="sxs-lookup"><span data-stu-id="d9c97-136">URL</span></span> | <span data-ttu-id="d9c97-137">IP</span><span class="sxs-lookup"><span data-stu-id="d9c97-137">IP</span></span> | <span data-ttu-id="d9c97-138">Poorten</span><span class="sxs-lookup"><span data-stu-id="d9c97-138">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d9c97-139">Configuratie</span><span class="sxs-lookup"><span data-stu-id="d9c97-139">Configuration</span></span> |`management.core.windows.net` | |`443` |
| <span data-ttu-id="d9c97-140">Configuratie</span><span class="sxs-lookup"><span data-stu-id="d9c97-140">Configuration</span></span> |`management.azure.com` | |`443` |
| <span data-ttu-id="d9c97-141">Configuratie</span><span class="sxs-lookup"><span data-stu-id="d9c97-141">Configuration</span></span> |`login.windows.net` | |`443` |
| <span data-ttu-id="d9c97-142">Configuratie</span><span class="sxs-lookup"><span data-stu-id="d9c97-142">Configuration</span></span> |`login.microsoftonline.com` | |`443` |
| <span data-ttu-id="d9c97-143">Configuratie</span><span class="sxs-lookup"><span data-stu-id="d9c97-143">Configuration</span></span> |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| <span data-ttu-id="d9c97-144">Configuratie</span><span class="sxs-lookup"><span data-stu-id="d9c97-144">Configuration</span></span> |`auth.gfx.ms` | |`443` |
| <span data-ttu-id="d9c97-145">Configuratie</span><span class="sxs-lookup"><span data-stu-id="d9c97-145">Configuration</span></span> |`login.live.com` | |`443` |
| <span data-ttu-id="d9c97-146">Installeren</span><span class="sxs-lookup"><span data-stu-id="d9c97-146">Installation</span></span> |`packages.nuget.org` | |`443` |

## <a name="hockeyapp"></a><span data-ttu-id="d9c97-147">HockeyApp</span><span class="sxs-lookup"><span data-stu-id="d9c97-147">HockeyApp</span></span>
| <span data-ttu-id="d9c97-148">Doel</span><span class="sxs-lookup"><span data-stu-id="d9c97-148">Purpose</span></span> | <span data-ttu-id="d9c97-149">URL</span><span class="sxs-lookup"><span data-stu-id="d9c97-149">URL</span></span> | <span data-ttu-id="d9c97-150">IP</span><span class="sxs-lookup"><span data-stu-id="d9c97-150">IP</span></span> | <span data-ttu-id="d9c97-151">Poorten</span><span class="sxs-lookup"><span data-stu-id="d9c97-151">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d9c97-152">Crashgegevens</span><span class="sxs-lookup"><span data-stu-id="d9c97-152">Crash data</span></span> |<span data-ttu-id="d9c97-153">gate.hockeyapp.NET</span><span class="sxs-lookup"><span data-stu-id="d9c97-153">gate.hockeyapp.net</span></span> |<span data-ttu-id="d9c97-154">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="d9c97-154">104.45.136.42</span></span> |<span data-ttu-id="d9c97-155">80, 443</span><span class="sxs-lookup"><span data-stu-id="d9c97-155">80, 443</span></span> |

## <a name="availability-tests"></a><span data-ttu-id="d9c97-156">Beschikbaarheidstests</span><span class="sxs-lookup"><span data-stu-id="d9c97-156">Availability tests</span></span>
<span data-ttu-id="d9c97-157">Dit is de lijst Hallo van adressen waaruit [webtests voor beschikbaarheid](app-insights-monitor-web-app-availability.md) worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d9c97-157">This is hello list of addresses from which [availability web tests](app-insights-monitor-web-app-availability.md) are run.</span></span> <span data-ttu-id="d9c97-158">Als u webtests toorun op uw app wilt, maar uw webserver beperkte tooserving specifieke clients, hebt u toopermit binnenkomend verkeer op onze servers beschikbaarheid test.</span><span class="sxs-lookup"><span data-stu-id="d9c97-158">If you want toorun web tests on your app, but your web server is restricted tooserving specific clients, then you will have toopermit incoming traffic from our availability test servers.</span></span>

<span data-ttu-id="d9c97-159">Open de poorten 80 (http) en 443 (https) voor binnenkomend verkeer naar deze adressen (IP-adressen zijn gegroepeerd op locatie):</span><span class="sxs-lookup"><span data-stu-id="d9c97-159">Open ports 80 (http) and 443 (https) for incoming traffic from these addresses (IP addresses are grouped by location):</span></span>

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

## <a name="data-access-api"></a><span data-ttu-id="d9c97-160">API voor gegevenstoegang</span><span class="sxs-lookup"><span data-stu-id="d9c97-160">Data access API</span></span>
| <span data-ttu-id="d9c97-161">Doel</span><span class="sxs-lookup"><span data-stu-id="d9c97-161">Purpose</span></span> | <span data-ttu-id="d9c97-162">URI</span><span class="sxs-lookup"><span data-stu-id="d9c97-162">URI</span></span> | <span data-ttu-id="d9c97-163">IP</span><span class="sxs-lookup"><span data-stu-id="d9c97-163">IP</span></span> | <span data-ttu-id="d9c97-164">Poorten</span><span class="sxs-lookup"><span data-stu-id="d9c97-164">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d9c97-165">API</span><span class="sxs-lookup"><span data-stu-id="d9c97-165">API</span></span> |<span data-ttu-id="d9c97-166">API.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="d9c97-166">api.applicationinsights.io</span></span><br/><span data-ttu-id="d9c97-167">api1.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="d9c97-167">api1.applicationinsights.io</span></span><br/><span data-ttu-id="d9c97-168">api2.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="d9c97-168">api2.applicationinsights.io</span></span><br/><span data-ttu-id="d9c97-169">api3.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="d9c97-169">api3.applicationinsights.io</span></span><br/><span data-ttu-id="d9c97-170">api4.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="d9c97-170">api4.applicationinsights.io</span></span><br/><span data-ttu-id="d9c97-171">api5.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="d9c97-171">api5.applicationinsights.io</span></span> |<span data-ttu-id="d9c97-172">13.82.26.252</span><span class="sxs-lookup"><span data-stu-id="d9c97-172">13.82.26.252</span></span><br/><span data-ttu-id="d9c97-173">40.76.213.73</span><span class="sxs-lookup"><span data-stu-id="d9c97-173">40.76.213.73</span></span> |<span data-ttu-id="d9c97-174">80,443</span><span class="sxs-lookup"><span data-stu-id="d9c97-174">80,443</span></span> |
| <span data-ttu-id="d9c97-175">API-docs</span><span class="sxs-lookup"><span data-stu-id="d9c97-175">API docs</span></span> |<span data-ttu-id="d9c97-176">dev.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="d9c97-176">dev.applicationinsights.io</span></span><br/><span data-ttu-id="d9c97-177">dev.applicationinsights.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="d9c97-177">dev.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="d9c97-178">dev.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d9c97-178">dev.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d9c97-179">www.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="d9c97-179">www.applicationinsights.io</span></span><br/><span data-ttu-id="d9c97-180">www.applicationinsights.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="d9c97-180">www.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="d9c97-181">www.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d9c97-181">www.aisvc.visualstudio.com</span></span> |<span data-ttu-id="d9c97-182">13.82.24.149</span><span class="sxs-lookup"><span data-stu-id="d9c97-182">13.82.24.149</span></span><br/><span data-ttu-id="d9c97-183">40.114.82.10</span><span class="sxs-lookup"><span data-stu-id="d9c97-183">40.114.82.10</span></span> |<span data-ttu-id="d9c97-184">80,443</span><span class="sxs-lookup"><span data-stu-id="d9c97-184">80,443</span></span> |
| <span data-ttu-id="d9c97-185">Interne API</span><span class="sxs-lookup"><span data-stu-id="d9c97-185">Internal API</span></span> |<span data-ttu-id="d9c97-186">aigs.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d9c97-186">aigs.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d9c97-187">aigs1.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d9c97-187">aigs1.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d9c97-188">aigs2.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d9c97-188">aigs2.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d9c97-189">aigs3.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d9c97-189">aigs3.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d9c97-190">aigs4.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d9c97-190">aigs4.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d9c97-191">aigs5.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d9c97-191">aigs5.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d9c97-192">aigs6.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d9c97-192">aigs6.aisvc.visualstudio.com</span></span> |<span data-ttu-id="d9c97-193">dynamische</span><span class="sxs-lookup"><span data-stu-id="d9c97-193">dynamic</span></span>|<span data-ttu-id="d9c97-194">443</span><span class="sxs-lookup"><span data-stu-id="d9c97-194">443</span></span> |

## <a name="application-insights-analytics"></a><span data-ttu-id="d9c97-195">Application Insights Analytics</span><span class="sxs-lookup"><span data-stu-id="d9c97-195">Application Insights Analytics</span></span>

| <span data-ttu-id="d9c97-196">Doel</span><span class="sxs-lookup"><span data-stu-id="d9c97-196">Purpose</span></span> | <span data-ttu-id="d9c97-197">URI</span><span class="sxs-lookup"><span data-stu-id="d9c97-197">URI</span></span> | <span data-ttu-id="d9c97-198">IP</span><span class="sxs-lookup"><span data-stu-id="d9c97-198">IP</span></span> | <span data-ttu-id="d9c97-199">Poorten</span><span class="sxs-lookup"><span data-stu-id="d9c97-199">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d9c97-200">Analytics-Portal</span><span class="sxs-lookup"><span data-stu-id="d9c97-200">Analytics Portal</span></span> | <span data-ttu-id="d9c97-201">Analytics.applicationinsights.IO</span><span class="sxs-lookup"><span data-stu-id="d9c97-201">analytics.applicationinsights.io</span></span> | <span data-ttu-id="d9c97-202">dynamische</span><span class="sxs-lookup"><span data-stu-id="d9c97-202">dynamic</span></span> | <span data-ttu-id="d9c97-203">80,443</span><span class="sxs-lookup"><span data-stu-id="d9c97-203">80,443</span></span> |
| <span data-ttu-id="d9c97-204">CDN</span><span class="sxs-lookup"><span data-stu-id="d9c97-204">CDN</span></span> | <span data-ttu-id="d9c97-205">applicationanalytics.azureedge.NET</span><span class="sxs-lookup"><span data-stu-id="d9c97-205">applicationanalytics.azureedge.net</span></span> | <span data-ttu-id="d9c97-206">dynamische</span><span class="sxs-lookup"><span data-stu-id="d9c97-206">dynamic</span></span> | <span data-ttu-id="d9c97-207">80,443</span><span class="sxs-lookup"><span data-stu-id="d9c97-207">80,443</span></span> |
| <span data-ttu-id="d9c97-208">Media CDN</span><span class="sxs-lookup"><span data-stu-id="d9c97-208">Media CDN</span></span> | <span data-ttu-id="d9c97-209">applicationanalyticsmedia.azureedge.NET</span><span class="sxs-lookup"><span data-stu-id="d9c97-209">applicationanalyticsmedia.azureedge.net</span></span> | <span data-ttu-id="d9c97-210">dynamische</span><span class="sxs-lookup"><span data-stu-id="d9c97-210">dynamic</span></span> | <span data-ttu-id="d9c97-211">80,443</span><span class="sxs-lookup"><span data-stu-id="d9c97-211">80,443</span></span> |

<span data-ttu-id="d9c97-212">Opmerking: *. applicationinsights.io domein is eigendom van Application Insights-team.</span><span class="sxs-lookup"><span data-stu-id="d9c97-212">Note: *.applicationinsights.io domain is owned by Application Insights team.</span></span>

## <a name="application-insights-azure-portal-extension"></a><span data-ttu-id="d9c97-213">Application Insights Azure Portal-extensie</span><span class="sxs-lookup"><span data-stu-id="d9c97-213">Application Insights Azure Portal Extension</span></span>

| <span data-ttu-id="d9c97-214">Doel</span><span class="sxs-lookup"><span data-stu-id="d9c97-214">Purpose</span></span> | <span data-ttu-id="d9c97-215">URI</span><span class="sxs-lookup"><span data-stu-id="d9c97-215">URI</span></span> | <span data-ttu-id="d9c97-216">IP</span><span class="sxs-lookup"><span data-stu-id="d9c97-216">IP</span></span> | <span data-ttu-id="d9c97-217">Poorten</span><span class="sxs-lookup"><span data-stu-id="d9c97-217">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d9c97-218">Application Insights-extensie</span><span class="sxs-lookup"><span data-stu-id="d9c97-218">Application Insights Extension</span></span> | <span data-ttu-id="d9c97-219">stamp2.app.insightsportal.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d9c97-219">stamp2.app.insightsportal.visualstudio.com</span></span> | <span data-ttu-id="d9c97-220">dynamische</span><span class="sxs-lookup"><span data-stu-id="d9c97-220">dynamic</span></span> | <span data-ttu-id="d9c97-221">80,443</span><span class="sxs-lookup"><span data-stu-id="d9c97-221">80,443</span></span> |
| <span data-ttu-id="d9c97-222">Application Insights-extensie CDN</span><span class="sxs-lookup"><span data-stu-id="d9c97-222">Application Insights Extension CDN</span></span> | <span data-ttu-id="d9c97-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d9c97-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d9c97-224">insightsportal prod2-asiae cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d9c97-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d9c97-225">insightsportal-cdn-aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d9c97-225">insightsportal-cdn-aimon.applicationinsights.io</span></span> | <span data-ttu-id="d9c97-226">dynamische</span><span class="sxs-lookup"><span data-stu-id="d9c97-226">dynamic</span></span> | <span data-ttu-id="d9c97-227">80,443</span><span class="sxs-lookup"><span data-stu-id="d9c97-227">80,443</span></span> |

## <a name="application-insights-sdks"></a><span data-ttu-id="d9c97-228">Application Insights-SDK 's</span><span class="sxs-lookup"><span data-stu-id="d9c97-228">Application Insights SDKs</span></span>

| <span data-ttu-id="d9c97-229">Doel</span><span class="sxs-lookup"><span data-stu-id="d9c97-229">Purpose</span></span> | <span data-ttu-id="d9c97-230">URI</span><span class="sxs-lookup"><span data-stu-id="d9c97-230">URI</span></span> | <span data-ttu-id="d9c97-231">IP</span><span class="sxs-lookup"><span data-stu-id="d9c97-231">IP</span></span> | <span data-ttu-id="d9c97-232">Poorten</span><span class="sxs-lookup"><span data-stu-id="d9c97-232">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d9c97-233">Application Insights-SDK voor JS CDN</span><span class="sxs-lookup"><span data-stu-id="d9c97-233">Application Insights JS SDK CDN</span></span> | <span data-ttu-id="d9c97-234">az416426.VO.msecnd.NET</span><span class="sxs-lookup"><span data-stu-id="d9c97-234">az416426.vo.msecnd.net</span></span> | <span data-ttu-id="d9c97-235">dynamische</span><span class="sxs-lookup"><span data-stu-id="d9c97-235">dynamic</span></span> | <span data-ttu-id="d9c97-236">80,443</span><span class="sxs-lookup"><span data-stu-id="d9c97-236">80,443</span></span> |
| <span data-ttu-id="d9c97-237">Application Insights Java SDK</span><span class="sxs-lookup"><span data-stu-id="d9c97-237">Application Insights Java SDK</span></span> | <span data-ttu-id="d9c97-238">aijavasdk.BLOB.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="d9c97-238">aijavasdk.blob.core.windows.net</span></span> | <span data-ttu-id="d9c97-239">dynamische</span><span class="sxs-lookup"><span data-stu-id="d9c97-239">dynamic</span></span> | <span data-ttu-id="d9c97-240">80,443</span><span class="sxs-lookup"><span data-stu-id="d9c97-240">80,443</span></span> |

## <a name="profiler"></a><span data-ttu-id="d9c97-241">Profiler</span><span class="sxs-lookup"><span data-stu-id="d9c97-241">Profiler</span></span>

| <span data-ttu-id="d9c97-242">Doel</span><span class="sxs-lookup"><span data-stu-id="d9c97-242">Purpose</span></span> | <span data-ttu-id="d9c97-243">URI</span><span class="sxs-lookup"><span data-stu-id="d9c97-243">URI</span></span> | <span data-ttu-id="d9c97-244">IP</span><span class="sxs-lookup"><span data-stu-id="d9c97-244">IP</span></span> | <span data-ttu-id="d9c97-245">Poorten</span><span class="sxs-lookup"><span data-stu-id="d9c97-245">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d9c97-246">Agent</span><span class="sxs-lookup"><span data-stu-id="d9c97-246">Agent</span></span> | <span data-ttu-id="d9c97-247">Agent.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="d9c97-247">agent.azureserviceprofiler.net</span></span><br/><span data-ttu-id="d9c97-248">*. agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="d9c97-248">*.agent.azureserviceprofiler.net</span></span> | <span data-ttu-id="d9c97-249">dynamische</span><span class="sxs-lookup"><span data-stu-id="d9c97-249">dynamic</span></span> | <span data-ttu-id="d9c97-250">443</span><span class="sxs-lookup"><span data-stu-id="d9c97-250">443</span></span>
| <span data-ttu-id="d9c97-251">Portal</span><span class="sxs-lookup"><span data-stu-id="d9c97-251">Portal</span></span> | <span data-ttu-id="d9c97-252">gateway.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="d9c97-252">gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="d9c97-253">dynamische</span><span class="sxs-lookup"><span data-stu-id="d9c97-253">dynamic</span></span> | <span data-ttu-id="d9c97-254">443</span><span class="sxs-lookup"><span data-stu-id="d9c97-254">443</span></span>
| <span data-ttu-id="d9c97-255">Storage</span><span class="sxs-lookup"><span data-stu-id="d9c97-255">Storage</span></span> | <span data-ttu-id="d9c97-256">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="d9c97-256">*.core.windows.net</span></span> | <span data-ttu-id="d9c97-257">dynamische</span><span class="sxs-lookup"><span data-stu-id="d9c97-257">dynamic</span></span> | <span data-ttu-id="d9c97-258">443</span><span class="sxs-lookup"><span data-stu-id="d9c97-258">443</span></span>

## <a name="snapshot-debugger"></a><span data-ttu-id="d9c97-259">Snapshot Debugger</span><span class="sxs-lookup"><span data-stu-id="d9c97-259">Snapshot Debugger</span></span>

| <span data-ttu-id="d9c97-260">Doel</span><span class="sxs-lookup"><span data-stu-id="d9c97-260">Purpose</span></span> | <span data-ttu-id="d9c97-261">URI</span><span class="sxs-lookup"><span data-stu-id="d9c97-261">URI</span></span> | <span data-ttu-id="d9c97-262">IP</span><span class="sxs-lookup"><span data-stu-id="d9c97-262">IP</span></span> | <span data-ttu-id="d9c97-263">Poorten</span><span class="sxs-lookup"><span data-stu-id="d9c97-263">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d9c97-264">Agent</span><span class="sxs-lookup"><span data-stu-id="d9c97-264">Agent</span></span> | <span data-ttu-id="d9c97-265">ppe.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="d9c97-265">ppe.azureserviceprofiler.net</span></span><br/><span data-ttu-id="d9c97-266">*. ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="d9c97-266">*.ppe.azureserviceprofiler.net</span></span> | <span data-ttu-id="d9c97-267">dynamische</span><span class="sxs-lookup"><span data-stu-id="d9c97-267">dynamic</span></span> | <span data-ttu-id="d9c97-268">443</span><span class="sxs-lookup"><span data-stu-id="d9c97-268">443</span></span>
| <span data-ttu-id="d9c97-269">Portal</span><span class="sxs-lookup"><span data-stu-id="d9c97-269">Portal</span></span> | <span data-ttu-id="d9c97-270">ppe.gateway.azureserviceprofiler.NET</span><span class="sxs-lookup"><span data-stu-id="d9c97-270">ppe.gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="d9c97-271">dynamische</span><span class="sxs-lookup"><span data-stu-id="d9c97-271">dynamic</span></span> | <span data-ttu-id="d9c97-272">443</span><span class="sxs-lookup"><span data-stu-id="d9c97-272">443</span></span>
| <span data-ttu-id="d9c97-273">Storage</span><span class="sxs-lookup"><span data-stu-id="d9c97-273">Storage</span></span> | <span data-ttu-id="d9c97-274">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="d9c97-274">*.core.windows.net</span></span> | <span data-ttu-id="d9c97-275">dynamische</span><span class="sxs-lookup"><span data-stu-id="d9c97-275">dynamic</span></span> | <span data-ttu-id="d9c97-276">443</span><span class="sxs-lookup"><span data-stu-id="d9c97-276">443</span></span>
