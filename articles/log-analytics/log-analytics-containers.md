---
title: aaaContainer bewaking oplossing in Azure Log Analytics | Microsoft Docs
description: "Hallo oplossing Container bewaking in logboekanalyse helpt u bij het weergeven en beheren van uw Docker- en Windows container hosts op één locatie."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte;banders
ms.openlocfilehash: 2eed1dd81c22faef78a375fca3ebece9e5300c09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a><span data-ttu-id="5284c-103">Container bewaking oplossing in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="5284c-103">Container Monitoring solution in Log Analytics</span></span>

![Containers symbool](./media/log-analytics-containers/containers-symbol.png)

<span data-ttu-id="5284c-105">Dit artikel wordt beschreven hoe tooset up en het gebruik Container bewaking oplossing in Log Analytics, waarmee u kunt weergeven en beheren van uw Docker- en Windows hello container hosts op één locatie.</span><span class="sxs-lookup"><span data-stu-id="5284c-105">This article describes how tooset up and use hello Container Monitoring solution in Log Analytics, which helps you view and manage your Docker and Windows container hosts in a single location.</span></span> <span data-ttu-id="5284c-106">Docker is een systeem van de virtualisatie software gebruikt toocreate containers die software-implementatie tootheir IT automatiseren infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="5284c-106">Docker is a software virtualization system used toocreate containers that automate software deployment tootheir IT infrastructure.</span></span>

<span data-ttu-id="5284c-107">Hallo oplossing Hier ziet u de containers worden uitgevoerd, welke container afbeelding ze uitvoert, en waarop de containers worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5284c-107">hello solution shows which containers are running, what container image they’re running, and where containers are running.</span></span> <span data-ttu-id="5284c-108">U kunt gedetailleerde controle-informatie met opdrachten gebruikt met containers weergeven.</span><span class="sxs-lookup"><span data-stu-id="5284c-108">You can view detailed audit information showing commands used with containers.</span></span> <span data-ttu-id="5284c-109">En u containers weer te geven en gecentraliseerd logboeken zoeken zonder tooremotely weergave Docker- of Windows-hosts kunt oplossen.</span><span class="sxs-lookup"><span data-stu-id="5284c-109">And, you can troubleshoot containers by viewing and searching centralized logs without having tooremotely view Docker or Windows hosts.</span></span> <span data-ttu-id="5284c-110">U vindt de containers die mogelijk veel ruis veroorzaken en verbruiken overtollige bronnen op een host.</span><span class="sxs-lookup"><span data-stu-id="5284c-110">You can find containers that may be noisy and consuming excess resources on a host.</span></span> <span data-ttu-id="5284c-111">En u kunt gecentraliseerde CPU, geheugen, opslag en gebruiks- en netwerkgegevens voor containers weergeven.</span><span class="sxs-lookup"><span data-stu-id="5284c-111">And, you can view centralized CPU, memory, storage, and network usage and performance information for containers.</span></span> <span data-ttu-id="5284c-112">Op computers waarop Windows wordt uitgevoerd, kunt u centraliseren en vergelijken van Logboeken van Windows Server, Hyper-V en Docker-containers.</span><span class="sxs-lookup"><span data-stu-id="5284c-112">On computers running Windows, you can centralize and compare logs from Windows Server, Hyper-V, and Docker containers.</span></span> <span data-ttu-id="5284c-113">Hallo-oplossing ondersteunt Hallo container orchestrators te volgen:</span><span class="sxs-lookup"><span data-stu-id="5284c-113">hello solution supports hello following container orchestrators:</span></span>

- <span data-ttu-id="5284c-114">Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="5284c-114">Docker Swarm</span></span>
- <span data-ttu-id="5284c-115">DC/OS</span><span class="sxs-lookup"><span data-stu-id="5284c-115">DC/OS</span></span>
- <span data-ttu-id="5284c-116">Kubernetes</span><span class="sxs-lookup"><span data-stu-id="5284c-116">Kubernetes</span></span>
- <span data-ttu-id="5284c-117">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5284c-117">Service Fabric</span></span>
- <span data-ttu-id="5284c-118">Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="5284c-118">Red Hat OpenShift</span></span>


<span data-ttu-id="5284c-119">Hallo toont volgende diagram Hallo relaties tussen verschillende container hosts en -agents met OMS.</span><span class="sxs-lookup"><span data-stu-id="5284c-119">hello following diagram shows hello relationships between various container hosts and agents with OMS.</span></span>

![Diagram van de containers](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a><span data-ttu-id="5284c-121">Systeemvereisten</span><span class="sxs-lookup"><span data-stu-id="5284c-121">System requirements</span></span>

<span data-ttu-id="5284c-122">Controleer voordat u begint, Hallo details tooverify u voldoet aan de vereisten hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="5284c-122">Before starting, review hello following details tooverify you meet hello prerequisites.</span></span>

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a><span data-ttu-id="5284c-123">Container bewakingsoplossing ondersteuning voor Docker-Orchestrator en OS-platform</span><span class="sxs-lookup"><span data-stu-id="5284c-123">Container monitoring solution support for Docker Orchestrator and OS platform</span></span>
<span data-ttu-id="5284c-124">Hallo Hallo volgende overzichten van de tabel Docker orchestration en het besturingssysteem ondersteuning van container-inventaris, prestaties en logboeken met logboekanalyse bewaking.</span><span class="sxs-lookup"><span data-stu-id="5284c-124">hello following table outlines hello Docker orchestration and operating system monitoring support of container inventory, performance, and logs with Log Analytics.</span></span>   

| | <span data-ttu-id="5284c-125">ACS</span><span class="sxs-lookup"><span data-stu-id="5284c-125">ACS</span></span> | <span data-ttu-id="5284c-126">Linux</span><span class="sxs-lookup"><span data-stu-id="5284c-126">Linux</span></span> | <span data-ttu-id="5284c-127">Windows</span><span class="sxs-lookup"><span data-stu-id="5284c-127">Windows</span></span> | <span data-ttu-id="5284c-128">Container</span><span class="sxs-lookup"><span data-stu-id="5284c-128">Container</span></span><br><span data-ttu-id="5284c-129">Inventaris</span><span class="sxs-lookup"><span data-stu-id="5284c-129">Inventory</span></span> | <span data-ttu-id="5284c-130">Installatiekopie</span><span class="sxs-lookup"><span data-stu-id="5284c-130">Image</span></span><br><span data-ttu-id="5284c-131">Inventaris</span><span class="sxs-lookup"><span data-stu-id="5284c-131">Inventory</span></span> | <span data-ttu-id="5284c-132">Knooppunt</span><span class="sxs-lookup"><span data-stu-id="5284c-132">Node</span></span><br><span data-ttu-id="5284c-133">Inventaris</span><span class="sxs-lookup"><span data-stu-id="5284c-133">Inventory</span></span> | <span data-ttu-id="5284c-134">Container</span><span class="sxs-lookup"><span data-stu-id="5284c-134">Container</span></span><br><span data-ttu-id="5284c-135">Prestaties</span><span class="sxs-lookup"><span data-stu-id="5284c-135">Performance</span></span> | <span data-ttu-id="5284c-136">Container</span><span class="sxs-lookup"><span data-stu-id="5284c-136">Container</span></span><br><span data-ttu-id="5284c-137">Gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="5284c-137">Event</span></span> | <span data-ttu-id="5284c-138">Gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="5284c-138">Event</span></span><br><span data-ttu-id="5284c-139">Logboek</span><span class="sxs-lookup"><span data-stu-id="5284c-139">Log</span></span> | <span data-ttu-id="5284c-140">Container</span><span class="sxs-lookup"><span data-stu-id="5284c-140">Container</span></span><br><span data-ttu-id="5284c-141">Logboek</span><span class="sxs-lookup"><span data-stu-id="5284c-141">Log</span></span> |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| <span data-ttu-id="5284c-142">Kubernetes</span><span class="sxs-lookup"><span data-stu-id="5284c-142">Kubernetes</span></span> | <span data-ttu-id="5284c-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-143">&#8226;</span></span> | <span data-ttu-id="5284c-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-144">&#8226;</span></span> | | <span data-ttu-id="5284c-145">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-145">&#8226;</span></span> | <span data-ttu-id="5284c-146">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-146">&#8226;</span></span> | <span data-ttu-id="5284c-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-147">&#8226;</span></span> | <span data-ttu-id="5284c-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-148">&#8226;</span></span> | <span data-ttu-id="5284c-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-149">&#8226;</span></span> | <span data-ttu-id="5284c-150">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-150">&#8226;</span></span> | <span data-ttu-id="5284c-151">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-151">&#8226;</span></span> |
| <span data-ttu-id="5284c-152">Mesosphere</span><span class="sxs-lookup"><span data-stu-id="5284c-152">Mesosphere</span></span><br><span data-ttu-id="5284c-153">DC/OS</span><span class="sxs-lookup"><span data-stu-id="5284c-153">DC/OS</span></span> | <span data-ttu-id="5284c-154">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-154">&#8226;</span></span> | <span data-ttu-id="5284c-155">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-155">&#8226;</span></span> | | <span data-ttu-id="5284c-156">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-156">&#8226;</span></span> | <span data-ttu-id="5284c-157">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-157">&#8226;</span></span> | <span data-ttu-id="5284c-158">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-158">&#8226;</span></span> | <span data-ttu-id="5284c-159">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-159">&#8226;</span></span>| <span data-ttu-id="5284c-160">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-160">&#8226;</span></span> | <span data-ttu-id="5284c-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-161">&#8226;</span></span> | <span data-ttu-id="5284c-162">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-162">&#8226;</span></span> |
| <span data-ttu-id="5284c-163">Docker</span><span class="sxs-lookup"><span data-stu-id="5284c-163">Docker</span></span><br><span data-ttu-id="5284c-164">Swarm</span><span class="sxs-lookup"><span data-stu-id="5284c-164">Swarm</span></span> | <span data-ttu-id="5284c-165">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-165">&#8226;</span></span> | <span data-ttu-id="5284c-166">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-166">&#8226;</span></span> | <span data-ttu-id="5284c-167">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-167">&#8226;</span></span> | <span data-ttu-id="5284c-168">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-168">&#8226;</span></span> | <span data-ttu-id="5284c-169">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-169">&#8226;</span></span> | <span data-ttu-id="5284c-170">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-170">&#8226;</span></span> | <span data-ttu-id="5284c-171">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-171">&#8226;</span></span> | <span data-ttu-id="5284c-172">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-172">&#8226;</span></span> | | <span data-ttu-id="5284c-173">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-173">&#8226;</span></span> |
| <span data-ttu-id="5284c-174">Service</span><span class="sxs-lookup"><span data-stu-id="5284c-174">Service</span></span><br><span data-ttu-id="5284c-175">Fabric</span><span class="sxs-lookup"><span data-stu-id="5284c-175">Fabric</span></span> | | | <span data-ttu-id="5284c-176">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-176">&#8226;</span></span> | <span data-ttu-id="5284c-177">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-177">&#8226;</span></span> | <span data-ttu-id="5284c-178">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-178">&#8226;</span></span> | <span data-ttu-id="5284c-179">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-179">&#8226;</span></span> | <span data-ttu-id="5284c-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-180">&#8226;</span></span> | <span data-ttu-id="5284c-181">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-181">&#8226;</span></span> | <span data-ttu-id="5284c-182">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-182">&#8226;</span></span> | <span data-ttu-id="5284c-183">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-183">&#8226;</span></span> |
| <span data-ttu-id="5284c-184">Red Hat openen</span><span class="sxs-lookup"><span data-stu-id="5284c-184">Red Hat Open</span></span><br><span data-ttu-id="5284c-185">SHIFT</span><span class="sxs-lookup"><span data-stu-id="5284c-185">Shift</span></span> | | <span data-ttu-id="5284c-186">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-186">&#8226;</span></span> | | <span data-ttu-id="5284c-187">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-187">&#8226;</span></span> | <span data-ttu-id="5284c-188">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-188">&#8226;</span></span>| <span data-ttu-id="5284c-189">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-189">&#8226;</span></span> | <span data-ttu-id="5284c-190">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-190">&#8226;</span></span> | <span data-ttu-id="5284c-191">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-191">&#8226;</span></span> | | <span data-ttu-id="5284c-192">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-192">&#8226;</span></span> |
| <span data-ttu-id="5284c-193">Windows Server</span><span class="sxs-lookup"><span data-stu-id="5284c-193">Windows Server</span></span><br><span data-ttu-id="5284c-194">(zelfstandig)</span><span class="sxs-lookup"><span data-stu-id="5284c-194">(standalone)</span></span> | | | <span data-ttu-id="5284c-195">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-195">&#8226;</span></span> | <span data-ttu-id="5284c-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-196">&#8226;</span></span> | <span data-ttu-id="5284c-197">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-197">&#8226;</span></span> | <span data-ttu-id="5284c-198">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-198">&#8226;</span></span> | <span data-ttu-id="5284c-199">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-199">&#8226;</span></span> | <span data-ttu-id="5284c-200">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-200">&#8226;</span></span> | | <span data-ttu-id="5284c-201">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-201">&#8226;</span></span> |
| <span data-ttu-id="5284c-202">Linux-server</span><span class="sxs-lookup"><span data-stu-id="5284c-202">Linux Server</span></span><br><span data-ttu-id="5284c-203">(zelfstandig)</span><span class="sxs-lookup"><span data-stu-id="5284c-203">(standalone)</span></span> | | <span data-ttu-id="5284c-204">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-204">&#8226;</span></span> | | <span data-ttu-id="5284c-205">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-205">&#8226;</span></span> | <span data-ttu-id="5284c-206">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-206">&#8226;</span></span> | <span data-ttu-id="5284c-207">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-207">&#8226;</span></span> | <span data-ttu-id="5284c-208">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-208">&#8226;</span></span> | <span data-ttu-id="5284c-209">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-209">&#8226;</span></span> | | <span data-ttu-id="5284c-210">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5284c-210">&#8226;</span></span> |


### <a name="docker-versions-supported-on-linux"></a><span data-ttu-id="5284c-211">Docker-versies die worden ondersteund op Linux</span><span class="sxs-lookup"><span data-stu-id="5284c-211">Docker versions supported on Linux</span></span>

- <span data-ttu-id="5284c-212">Docker 1.11 too1.13</span><span class="sxs-lookup"><span data-stu-id="5284c-212">Docker 1.11 too1.13</span></span>
- <span data-ttu-id="5284c-213">Docker CE en EE v17.06</span><span class="sxs-lookup"><span data-stu-id="5284c-213">Docker CE and EE v17.06</span></span>

### <a name="x64-linux-distributions-supported-as-container-hosts"></a><span data-ttu-id="5284c-214">x64 Linux-distributies als container hosts ondersteund</span><span class="sxs-lookup"><span data-stu-id="5284c-214">x64 Linux distributions supported as container hosts</span></span>

- <span data-ttu-id="5284c-215">Ubuntu 14.04 TNS en 16.04 TNS</span><span class="sxs-lookup"><span data-stu-id="5284c-215">Ubuntu 14.04 LTS and 16.04 LTS</span></span>
- <span data-ttu-id="5284c-216">CoreOS(stable)</span><span class="sxs-lookup"><span data-stu-id="5284c-216">CoreOS(stable)</span></span>
- <span data-ttu-id="5284c-217">Amazon Linux 2016.09.0</span><span class="sxs-lookup"><span data-stu-id="5284c-217">Amazon Linux 2016.09.0</span></span>
- <span data-ttu-id="5284c-218">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="5284c-218">openSUSE 13.2</span></span>
- <span data-ttu-id="5284c-219">openSUSE 42,2 LEAP</span><span class="sxs-lookup"><span data-stu-id="5284c-219">openSUSE LEAP 42.2</span></span>
- <span data-ttu-id="5284c-220">CentOS 7.2 en 7.3</span><span class="sxs-lookup"><span data-stu-id="5284c-220">CentOS 7.2 and 7.3</span></span>
- <span data-ttu-id="5284c-221">SLES 12</span><span class="sxs-lookup"><span data-stu-id="5284c-221">SLES 12</span></span>
- <span data-ttu-id="5284c-222">RHEL 7.2 en 7.3</span><span class="sxs-lookup"><span data-stu-id="5284c-222">RHEL 7.2 and 7.3</span></span>
- <span data-ttu-id="5284c-223">Red Hat OpenShift Container Platform (OCP) 3.4 en 3.5</span><span class="sxs-lookup"><span data-stu-id="5284c-223">Red Hat OpenShift Container Platform (OCP) 3.4 and 3.5</span></span>
- <span data-ttu-id="5284c-224">ACS Mesosphere DC/OS 1.7.3 too1.8.8</span><span class="sxs-lookup"><span data-stu-id="5284c-224">ACS Mesosphere DC/OS 1.7.3 too1.8.8</span></span>
- <span data-ttu-id="5284c-225">ACS Kubernetes 1.4.5 too1.6</span><span class="sxs-lookup"><span data-stu-id="5284c-225">ACS Kubernetes 1.4.5 too1.6</span></span>
- <span data-ttu-id="5284c-226">ACS Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="5284c-226">ACS Docker Swarm</span></span>

### <a name="supported-windows-operating-system"></a><span data-ttu-id="5284c-227">Ondersteunde Windows-besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="5284c-227">Supported Windows operating system</span></span>

- <span data-ttu-id="5284c-228">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="5284c-228">Windows Server 2016</span></span>
- <span data-ttu-id="5284c-229">Speciale Windows 10-editie (Professional of Enterprise)</span><span class="sxs-lookup"><span data-stu-id="5284c-229">Windows 10 Anniversary Edition (Professional or Enterprise)</span></span>

### <a name="docker-versions-supported-on-windows"></a><span data-ttu-id="5284c-230">Docker-versies worden ondersteund in Windows</span><span class="sxs-lookup"><span data-stu-id="5284c-230">Docker versions supported on Windows</span></span>

- <span data-ttu-id="5284c-231">Docker 1.12 en 1.13</span><span class="sxs-lookup"><span data-stu-id="5284c-231">Docker 1.12 and 1.13</span></span>
- <span data-ttu-id="5284c-232">Docker 17.03.0 en hoger</span><span class="sxs-lookup"><span data-stu-id="5284c-232">Docker 17.03.0 and later</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="5284c-233">Installeren en configureren van Hallo-oplossing</span><span class="sxs-lookup"><span data-stu-id="5284c-233">Installing and configuring hello solution</span></span>
<span data-ttu-id="5284c-234">Gebruik Hallo informatie tooinstall te volgen en Hallo oplossing configureren.</span><span class="sxs-lookup"><span data-stu-id="5284c-234">Use hello following information tooinstall and configure hello solution.</span></span>

1. <span data-ttu-id="5284c-235">Hallo oplossing tooyour OMS-werkruimte Container bewaking van toevoegen [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) of met behulp van Hallo procedure beschreven in [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="5284c-235">Add hello Container Monitoring solution tooyour OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

2. <span data-ttu-id="5284c-236">Installeren en gebruiken van Docker met een OMS-agent.</span><span class="sxs-lookup"><span data-stu-id="5284c-236">Install and use Docker with an OMS agent.</span></span>  <span data-ttu-id="5284c-237">Op basis van het besturingssysteem, kunt u kiezen uit de volgende methoden Hallo:</span><span class="sxs-lookup"><span data-stu-id="5284c-237">Based on your operating system, you can choose from hello following methods:</span></span>

  * <span data-ttu-id="5284c-238">Installeren op ondersteunde Linux-besturingssystemen en Docker uitvoeren en vervolgens installeren en configureren Hallo [OMS-Agent voor Linux](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5284c-238">On supported Linux operating systems, install and run Docker and then install and configure hello [OMS Agent for Linux](log-analytics-agent-linux.md).</span></span>  
  * <span data-ttu-id="5284c-239">Op virtuele CoreOS, kunt u Hallo OMS-Agent niet uitvoeren voor Linux.</span><span class="sxs-lookup"><span data-stu-id="5284c-239">On CoreOS, you cannot run hello OMS Agent for Linux.</span></span> <span data-ttu-id="5284c-240">U kunt in plaats daarvan een beperkte versie van Hallo OMS-Agent uitvoeren voor Linux.</span><span class="sxs-lookup"><span data-stu-id="5284c-240">Instead, you run a containerized version of hello OMS Agent for Linux.</span></span> <span data-ttu-id="5284c-241">Bekijk [Linux container hosts waaronder virtuele CoreOS](#for-all-linux-container-hosts-including-coreos) of [Azure Government Linux container hosts waaronder virtuele CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) als u met containers in Azure Government Cloud werkt.</span><span class="sxs-lookup"><span data-stu-id="5284c-241">Review [Linux container hosts including CoreOS](#for-all-linux-container-hosts-including-coreos) or [Azure Government Linux container hosts including CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) if you are working with containers in Azure Government Cloud.</span></span>
  * <span data-ttu-id="5284c-242">Hallo Docker-Engine en -client installeren op Windows Server 2016 en Windows 10 en vervolgens verbinding maken met een agent toogather informatie en tooLog Analytics om dit te verzenden.</span><span class="sxs-lookup"><span data-stu-id="5284c-242">On Windows Server 2016 and Windows 10, install hello Docker Engine and client then connect an agent toogather information and send it tooLog Analytics.</span></span>  

### <a name="container-services"></a><span data-ttu-id="5284c-243">Containerservices</span><span class="sxs-lookup"><span data-stu-id="5284c-243">Container services</span></span>

- <span data-ttu-id="5284c-244">Als u een Red Hat OpenShift-omgeving hebt, raadpleegt u [configureren van een OMS-agent voor Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span><span class="sxs-lookup"><span data-stu-id="5284c-244">If you have a Red Hat OpenShift environment, review [Configure an OMS agent for Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span></span>
- <span data-ttu-id="5284c-245">Als u een Kubernetes-cluster met behulp van Azure Container Service Hallo hebt, Bekijk [bewaken van een Azure Container Service-cluster met de Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span><span class="sxs-lookup"><span data-stu-id="5284c-245">If you have a Kubernetes cluster using hello Azure Container Service, review [Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span></span>
- <span data-ttu-id="5284c-246">Als u een Azure Container Service DC/OS-cluster hebt, meer informatie op [bewaken van een Azure Container Service DC/OS-cluster met Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span><span class="sxs-lookup"><span data-stu-id="5284c-246">If you have an Azure Container Service DC/OS cluster, learn more at [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span></span>
- <span data-ttu-id="5284c-247">Als u een omgeving met de modus Docker Swarm hebt, meer informatie op [configureren van een OMS-agent voor Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span><span class="sxs-lookup"><span data-stu-id="5284c-247">If you have a Docker Swarm mode environment, learn more at [Configure an OMS agent for Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span></span>
- <span data-ttu-id="5284c-248">Als u containers met Service Fabric gebruikt, meer op [overzicht van Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5284c-248">If you use containers with Service Fabric, learn more at [Overview of Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span></span>
- <span data-ttu-id="5284c-249">Bekijk Hallo [Docker-Engine op Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) artikel voor meer informatie over het tooinstall en de Docker-Engines configureren op computers met Windows.</span><span class="sxs-lookup"><span data-stu-id="5284c-249">Review hello [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article for additional information about how tooinstall and configure your Docker Engines on computers running Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5284c-250">Docker moet worden uitgevoerd **voordat** u Hallo installeren [OMS-Agent voor Linux](log-analytics-agent-linux.md) op de container-hosts.</span><span class="sxs-lookup"><span data-stu-id="5284c-250">Docker must be running **before** you install hello [OMS Agent for Linux](log-analytics-agent-linux.md) on your container hosts.</span></span> <span data-ttu-id="5284c-251">Als u al Hallo agent hebt geïnstalleerd voordat u Docker installeert, moet u tooreinstall Hallo OMS-Agent voor Linux.</span><span class="sxs-lookup"><span data-stu-id="5284c-251">If you've already installed hello agent before installing Docker, you need tooreinstall hello OMS Agent for Linux.</span></span> <span data-ttu-id="5284c-252">Zie voor meer informatie over Docker hello [Docker-website](https://www.docker.com).</span><span class="sxs-lookup"><span data-stu-id="5284c-252">For more information about Docker, see hello [Docker website](https://www.docker.com).</span></span>


## <a name="linux-container-hosts"></a><span data-ttu-id="5284c-253">Linux-container hosts</span><span class="sxs-lookup"><span data-stu-id="5284c-253">Linux container hosts</span></span>

<span data-ttu-id="5284c-254">Nadat u Docker hebt geïnstalleerd, gebruikt u Hallo-instellingen voor de container tooconfigure hello hostagent voor gebruik met Docker te volgen.</span><span class="sxs-lookup"><span data-stu-id="5284c-254">After you've installed Docker, use hello following settings for your container host tooconfigure hello agent for use with Docker.</span></span> <span data-ttu-id="5284c-255">U moet eerst uw OMS-werkruimte-ID en sleutel, kunt u vinden in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5284c-255">First you need your OMS workspace ID and key, which you can find in hello Azure portal.</span></span> <span data-ttu-id="5284c-256">Klik in de werkruimte op **Quick Start** > **Computers** tooview uw **werkruimte-ID** en **primaire sleutel**.</span><span class="sxs-lookup"><span data-stu-id="5284c-256">In your workspace, click **Quick Start** > **Computers** tooview your **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="5284c-257">Kopieer en plak beide in uw favoriete editor.</span><span class="sxs-lookup"><span data-stu-id="5284c-257">Copy and paste both into your favorite editor.</span></span>

### <a name="for-all-linux-container-hosts-except-coreos"></a><span data-ttu-id="5284c-258">Voor alle Linux-container hosts behalve virtuele CoreOS</span><span class="sxs-lookup"><span data-stu-id="5284c-258">For all Linux container hosts except CoreOS</span></span>

- <span data-ttu-id="5284c-259">Zie voor meer informatie en stapsgewijze instructies voor hoe tooinstall OMS-Agent voor Linux Hallo [verbinding maken met uw Linux-Computers tooOperations Management Suite (OMS)](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5284c-259">For more information and steps on how tooinstall hello OMS Agent for Linux, see [Connect your Linux Computers tooOperations Management Suite (OMS)](log-analytics-agent-linux.md).</span></span>

### <a name="for-all-linux-container-hosts-including-coreos"></a><span data-ttu-id="5284c-260">Voor alle Linux-container hosts, met inbegrip van virtuele CoreOS</span><span class="sxs-lookup"><span data-stu-id="5284c-260">For all Linux container hosts including CoreOS</span></span>

<span data-ttu-id="5284c-261">Hallo OMS-container die u toomonitor wilt starten.</span><span class="sxs-lookup"><span data-stu-id="5284c-261">Start hello OMS container that you want toomonitor.</span></span> <span data-ttu-id="5284c-262">Wijzigen en gebruik Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="5284c-262">Modify and use hello following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a><span data-ttu-id="5284c-263">Voor alle Azure Government Linux container hosts, met inbegrip van virtuele CoreOS</span><span class="sxs-lookup"><span data-stu-id="5284c-263">For all Azure Government Linux container hosts including CoreOS</span></span>

<span data-ttu-id="5284c-264">Hallo OMS-container die u toomonitor wilt starten.</span><span class="sxs-lookup"><span data-stu-id="5284c-264">Start hello OMS container that you want toomonitor.</span></span> <span data-ttu-id="5284c-265">Wijzigen en gebruik Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="5284c-265">Modify and use hello following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-tooone-in-a-container"></a><span data-ttu-id="5284c-266">Overschakelen van het gebruik van een geïnstalleerde Linux-agent tooone in een container</span><span class="sxs-lookup"><span data-stu-id="5284c-266">Switching from using an installed Linux agent tooone in a container</span></span>
<span data-ttu-id="5284c-267">Als u eerder hebt gebruikt Hallo direct geïnstalleerde agent en verwijder tooinstead gebruik een agent die wordt uitgevoerd in een container, moet u eerst Hallo OMS-Agent voor Linux.</span><span class="sxs-lookup"><span data-stu-id="5284c-267">If you previously used hello directly-installed agent and want tooinstead use an agent running in a container, you must first remove hello OMS Agent for Linux.</span></span> <span data-ttu-id="5284c-268">Zie [verwijderen Hallo OMS-Agent voor Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand hoe toosuccessfully verwijderen Hallo agent.</span><span class="sxs-lookup"><span data-stu-id="5284c-268">See [Uninstalling hello OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand how toosuccessfully uninstall hello agent.</span></span>  

### <a name="configure-an-oms-agent-for-docker-swarm"></a><span data-ttu-id="5284c-269">Configureer een OMS-agent voor Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="5284c-269">Configure an OMS agent for Docker Swarm</span></span>

<span data-ttu-id="5284c-270">U kunt Hallo OMS-Agent uitvoeren als een wereldwijde service op het Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="5284c-270">You can run hello OMS Agent as a global service on Docker Swarm.</span></span> <span data-ttu-id="5284c-271">Gebruik Hallo informatie toocreate een OMS-Agent-service te volgen.</span><span class="sxs-lookup"><span data-stu-id="5284c-271">Use hello following information toocreate an OMS Agent service.</span></span> <span data-ttu-id="5284c-272">Tooinsert moet u uw OMS-werkruimte-ID en de primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="5284c-272">You need tooinsert your OMS Workspace ID and Primary Key.</span></span>

- <span data-ttu-id="5284c-273">Hallo volgende uitvoeren op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="5284c-273">Run hello following on hello master node.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a><span data-ttu-id="5284c-274">Een OMS-Agent voor Red Hat OpenShift configureren</span><span class="sxs-lookup"><span data-stu-id="5284c-274">Configure an OMS Agent for Red Hat OpenShift</span></span>
<span data-ttu-id="5284c-275">Er zijn drie manieren tooadd Hallo OMS-Agent tooRed Hat OpenShift toostart verzamelen container bewakingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="5284c-275">There are three ways tooadd hello OMS Agent tooRed Hat OpenShift toostart collecting container monitoring data.</span></span>

* <span data-ttu-id="5284c-276">[Hallo OMS-Agent voor Linux installeren](log-analytics-agent-linux.md) rechtstreeks op elk knooppunt OpenShift</span><span class="sxs-lookup"><span data-stu-id="5284c-276">[Install hello OMS Agent for Linux](log-analytics-agent-linux.md) directly on each OpenShift node</span></span>  
* <span data-ttu-id="5284c-277">[Log Analytics VM-extensie inschakelen](log-analytics-azure-vm-extension.md) op elk knooppunt OpenShift is die zich in Azure</span><span class="sxs-lookup"><span data-stu-id="5284c-277">[Enable Log Analytics VM Extension](log-analytics-azure-vm-extension.md) on each OpenShift node residing in Azure</span></span>  
* <span data-ttu-id="5284c-278">Hallo OMS-Agent installeren als een OpenShift daemon-set</span><span class="sxs-lookup"><span data-stu-id="5284c-278">Install hello OMS Agent as a OpenShift daemon-set</span></span>  

<span data-ttu-id="5284c-279">In deze sectie uitgelegd Hallo stappen vereist tooinstall Hallo OMS-Agent als een OpenShift daemon-set.</span><span class="sxs-lookup"><span data-stu-id="5284c-279">In this section we cover hello steps required tooinstall hello OMS Agent as an OpenShift daemon-set.</span></span>  

1. <span data-ttu-id="5284c-280">Meld u aan bij toohello OpenShift knooppunt en kopieer Hallo yaml hoofdbestand [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) vanuit GitHub tooyour knooppunt master en Hallo-waarde met de OMS-werkruimte-ID en met uw primaire sleutel wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5284c-280">Sign on toohello OpenShift master node and copy hello yaml file [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) from GitHub tooyour master node and modify hello value with your OMS Workspace ID and with your Primary Key.</span></span>
2. <span data-ttu-id="5284c-281">Het uitvoeren van de volgende opdrachten toocreate Hallo een project voor OMS en stel Hallo-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="5284c-281">Run hello following commands toocreate a project for OMS and set hello user account.</span></span>

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="5284c-282">toodeploy hello daemon-set, voert u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="5284c-282">toodeploy hello daemon-set, run hello following:</span></span>

    `oc create -f ocp-omsagent.yaml`

5. <span data-ttu-id="5284c-283">tooverify is geconfigureerd en naar behoren werkt, typt Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="5284c-283">tooverify it is configured and working correctly, type hello following:</span></span>

    `oc describe daemonset omsagent`  

    <span data-ttu-id="5284c-284">en Hallo uitvoer moet eruitzien als:</span><span class="sxs-lookup"><span data-stu-id="5284c-284">and hello output should resemble:</span></span>

    ```
    [ocpadmin@khm-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

<span data-ttu-id="5284c-285">Als u toouse geheimen toosecure wilt uw OMS-werkruimte-ID en de primaire sleutel bij gebruik van Hallo OMS-Agent daemon-set yaml-bestand, uitvoeren Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="5284c-285">If you want toouse secrets toosecure your OMS Workspace ID and Primary Key when using hello OMS Agent daemon-set yaml file, perform hello following steps.</span></span>

1. <span data-ttu-id="5284c-286">Meld u aan bij toohello OpenShift knooppunt en kopieer Hallo yaml hoofdbestand [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) en geheim script genereren [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="5284c-286">Sign on toohello OpenShift master node and copy hello yaml file [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) and secret generating script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) from GitHub.</span></span>  <span data-ttu-id="5284c-287">Dit script genereert Hallo geheimen yaml-bestand voor de OMS-werkruimte-ID en de primaire sleutel toosecure uw secrete informatie.</span><span class="sxs-lookup"><span data-stu-id="5284c-287">This script will generate hello secrets yaml file for OMS Workspace ID and Primary Key toosecure your secrete information.</span></span>  
2. <span data-ttu-id="5284c-288">Het uitvoeren van de volgende opdrachten toocreate Hallo een project voor OMS en stel Hallo-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="5284c-288">Run hello following commands toocreate a project for OMS and set hello user account.</span></span> <span data-ttu-id="5284c-289">script genereren Hallo-geheim vraagt om uw OMS-werkruimte-ID <WSID> en primaire sleutel <KEY> en heeft voltooid, wordt er Hallo ocp-secret.yaml logboekbestand gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5284c-289">hello secret generating script asks for your OMS Workspace ID <WSID> and Primary Key <KEY> and upon completion, it creates hello ocp-secret.yaml file.</span></span>  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="5284c-290">Hallo geheime bestand door het uitvoeren van de volgende Hallo implementeren:</span><span class="sxs-lookup"><span data-stu-id="5284c-290">Deploy hello secret file by running hello following:</span></span>

    `oc create -f ocp-secret.yaml`

5. <span data-ttu-id="5284c-291">Implementatie door het uitvoeren van Hallo volgende controleren:</span><span class="sxs-lookup"><span data-stu-id="5284c-291">Verify deployment by running hello following:</span></span>

    `oc describe secret omsagent-secret`  

    <span data-ttu-id="5284c-292">en Hallo uitvoer moet eruitzien als:</span><span class="sxs-lookup"><span data-stu-id="5284c-292">and hello  output should resemble:</span></span>  

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

6. <span data-ttu-id="5284c-293">Hallo OMS-Agent daemon-set yaml-bestand door het uitvoeren van de volgende Hallo implementeren:</span><span class="sxs-lookup"><span data-stu-id="5284c-293">Deploy hello OMS Agent daemon-set yaml file by running hello following:</span></span>

    `oc create -f ocp-ds-omsagent.yaml`  

7. <span data-ttu-id="5284c-294">Implementatie door het uitvoeren van Hallo volgende controleren:</span><span class="sxs-lookup"><span data-stu-id="5284c-294">Verify deployment by running hello following:</span></span>

    `oc describe ds oms`

    <span data-ttu-id="5284c-295">en Hallo uitvoer moet eruitzien als:</span><span class="sxs-lookup"><span data-stu-id="5284c-295">and hello output should resemble:</span></span>

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe secret omsagent-secret  
    Name:           omsagent-secret  
    Namespace:      omslogging  
    Labels:         <none>  
    Annotations:    <none>  

    Type:   Opaque  

     Data  
     ====  
     KEY:    89 bytes  
     WSID:   37 bytes  
    ```

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a><span data-ttu-id="5284c-296">Uw geheime informatie voor Docker Swarm en Kubernetes beveiligen</span><span class="sxs-lookup"><span data-stu-id="5284c-296">Secure your secret information for Docker Swarm and Kubernetes</span></span>

<span data-ttu-id="5284c-297">U kunt uw geheime OMS-werkruimte-ID en de primaire sleutels voor Docker Swarm en Kubernetes containerservices beveiligen.</span><span class="sxs-lookup"><span data-stu-id="5284c-297">You can secure your secret OMS Workspace ID and Primary Keys for Docker Swarm and Kubernetes container services.</span></span>

#### <a name="secure-secrets-for-docker-swarm"></a><span data-ttu-id="5284c-298">Beveiligen van geheimen voor Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="5284c-298">Secure secrets for Docker Swarm</span></span>

<span data-ttu-id="5284c-299">Voor Docker Swarm, zodra Hallo geheim voor werkruimte-ID en de primaire sleutel is gemaakt, kunt u uitvoeren Hallo Hallo Docker-service voor OMSagent maken.</span><span class="sxs-lookup"><span data-stu-id="5284c-299">For Docker Swarm, once hello secret for Workspace ID and Primary Key is created, you can run hello create hello Docker service for OMSagent.</span></span> <span data-ttu-id="5284c-300">Hallo informatie toocreate na uw geheime gegevens gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5284c-300">Use hello following information toocreate your secret information.</span></span>

1. <span data-ttu-id="5284c-301">Hallo volgende uitvoeren op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="5284c-301">Run hello following on hello master node.</span></span>

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. <span data-ttu-id="5284c-302">Controleer of de geheimen op de juiste wijze zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5284c-302">Verify that secrets were created properly.</span></span>

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. <span data-ttu-id="5284c-303">Voer Hallo na de opdracht toomount Hallo geheimen toohello beperkte OMS-Agent.</span><span class="sxs-lookup"><span data-stu-id="5284c-303">Run hello following command toomount hello secrets toohello containerized OMS Agent.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a><span data-ttu-id="5284c-304">Geheimen beveiligen voor Kubernetes met yaml-bestanden</span><span class="sxs-lookup"><span data-stu-id="5284c-304">Secure secrets for Kubernetes with yaml files</span></span>

<span data-ttu-id="5284c-305">Voor Kubernetes gebruikt u een script toogenerate Hallo geheimen yaml-bestand voor uw werkruimte-ID en de primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="5284c-305">For Kubernetes, you use a script toogenerate hello secrets yaml file for your Workspace ID and Primary Key.</span></span> <span data-ttu-id="5284c-306">Op Hallo [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) pagina, er zijn bestanden die u met of zonder uw geheime informatie gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="5284c-306">At hello [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) page, there are files that you can use with or without your secret information.</span></span>

- <span data-ttu-id="5284c-307">Hallo standaard OMS-Agent DaemonSet heeft geen geheime informatie (omsagent.yaml)</span><span class="sxs-lookup"><span data-stu-id="5284c-307">hello Default OMS Agent DaemonSet does not have secret information (omsagent.yaml)</span></span>
- <span data-ttu-id="5284c-308">Hallo OMS-Agent DaemonSet yaml-bestand gebruikt geheime informatie (omsagent ds secrets.yaml) met geheime generatie scripts toogenerate Hallo geheimen yaml (omsagentsecret.yaml)-bestand.</span><span class="sxs-lookup"><span data-stu-id="5284c-308">hello OMS Agent DaemonSet yaml file uses secret information (omsagent-ds-secrets.yaml) with secret generation scripts toogenerate hello secrets yaml (omsagentsecret.yaml) file.</span></span>

<span data-ttu-id="5284c-309">U kunt toocreate omsagent DaemonSets met of zonder geheimen.</span><span class="sxs-lookup"><span data-stu-id="5284c-309">You can choose toocreate omsagent DaemonSets with or without secrets.</span></span>

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a><span data-ttu-id="5284c-310">Standaard OMSagent DaemonSet yaml-bestand zonder geheimen</span><span class="sxs-lookup"><span data-stu-id="5284c-310">Default OMSagent DaemonSet yaml file without secrets</span></span>

- <span data-ttu-id="5284c-311">Vervang voor Hallo OMS-Agent DaemonSet yaml standaardbestand Hallo `<WSID>` en `<KEY>` tooyour WSID en de sleutel.</span><span class="sxs-lookup"><span data-stu-id="5284c-311">For hello default OMS Agent DaemonSet yaml file, replace hello `<WSID>` and `<KEY>` tooyour WSID and KEY.</span></span> <span data-ttu-id="5284c-312">Kopieer Hallo tooyour hoofdknooppunt-bestand en Voer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="5284c-312">Copy hello file tooyour master node and run hello following:</span></span>

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a><span data-ttu-id="5284c-313">Standaard OMSagent DaemonSet yaml-bestand met geheimen</span><span class="sxs-lookup"><span data-stu-id="5284c-313">Default OMSagent DaemonSet yaml file with secrets</span></span>

1. <span data-ttu-id="5284c-314">toouse OMS-Agent DaemonSet met behulp van geheime informatie Hallo geheimen eerst maken.</span><span class="sxs-lookup"><span data-stu-id="5284c-314">toouse OMS Agent DaemonSet using secret information, create hello secrets first.</span></span>
    1. <span data-ttu-id="5284c-315">Hallo-script en geheime sjabloonbestand kopiëren en zorg ervoor dat ze zich op Hallo dezelfde directory.</span><span class="sxs-lookup"><span data-stu-id="5284c-315">Copy hello script and secret template file and make sure they are on hello same directory.</span></span>
        - <span data-ttu-id="5284c-316">geheim script - geheim gen.sh genereren</span><span class="sxs-lookup"><span data-stu-id="5284c-316">Secret generating script - secret-gen.sh</span></span>
        - <span data-ttu-id="5284c-317">geheime sjabloon - geheim template.yaml</span><span class="sxs-lookup"><span data-stu-id="5284c-317">secret template - secret-template.yaml</span></span>
    2. <span data-ttu-id="5284c-318">Voer Hallo-script, zoals Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="5284c-318">Run hello script, like hello following example.</span></span> <span data-ttu-id="5284c-319">Hallo script vraagt om Hallo OMS-werkruimte-ID en de primaire sleutel en nadat u deze invoert, Hallo script maakt een geheime yaml-bestand zodat u deze kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5284c-319">hello script asks for hello OMS Workspace ID and Primary Key and after you enter them, hello script creates a secret yaml file so you can run it.</span></span>   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. <span data-ttu-id="5284c-320">Hallo geheimen schil maken door het uitvoeren van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="5284c-320">Create hello secrets pod by running hello following:</span></span>
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. <span data-ttu-id="5284c-321">tooverify hello volgende uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5284c-321">tooverify, run hello following:</span></span>

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        <span data-ttu-id="5284c-322">Uitvoer moet eruitzien als:</span><span class="sxs-lookup"><span data-stu-id="5284c-322">Output should resemble:</span></span>

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        <span data-ttu-id="5284c-323">Uitvoer moet eruitzien als:</span><span class="sxs-lookup"><span data-stu-id="5284c-323">Output should resemble:</span></span>

        ```
        Name:           omsagent-secret
        Namespace:      default
        Labels:         <none>
        Annotations:    <none>

        Type:   Opaque

        Data
        ====
        WSID:   36 bytes
        KEY:    88 bytes
        ```

    5. <span data-ttu-id="5284c-324">Maken van uw omsagent daemon-set door te voeren``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="5284c-324">Create your omsagent daemon-set by running ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

2. <span data-ttu-id="5284c-325">Controleer of u die Hallo die daemonset van OMS-Agent wordt uitgevoerd, vergelijkbare toohello te volgen:</span><span class="sxs-lookup"><span data-stu-id="5284c-325">Verify that hello OMS Agent DaemonSet is running, similar toohello following:</span></span>

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


<span data-ttu-id="5284c-326">Voor Kubernetes, gebruikt u een script toogenerate Hallo geheimen yaml bestand voor de werkruimte-ID en de primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="5284c-326">For Kubernetes, use a script toogenerate hello secrets yaml file for Workspace ID and Primary Key.</span></span> <span data-ttu-id="5284c-327">Gebruik Hallo volgende voorbeeldinformatie Hello [omsagent yaml bestand](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure uw geheime informatie.</span><span class="sxs-lookup"><span data-stu-id="5284c-327">Use hello following example information with hello [omsagent yaml file](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure your secret information.</span></span>

```
keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
Name:           omsagent-secret
Namespace:      default
Labels:         <none>
Annotations:    <none>

Type:   Opaque

Data
====
WSID:   36 bytes
KEY:    88 bytes
```

## <a name="windows-container-hosts"></a><span data-ttu-id="5284c-328">Windows-container hosts</span><span class="sxs-lookup"><span data-stu-id="5284c-328">Windows container hosts</span></span>

### <a name="preparation-before-installing-windows-agents"></a><span data-ttu-id="5284c-329">Voorbereiding voor de installatie van Windows-agents</span><span class="sxs-lookup"><span data-stu-id="5284c-329">Preparation before installing Windows agents</span></span>

<span data-ttu-id="5284c-330">Voordat u agents op computers met Windows installeren, moet u tooconfigure hello Docker-service.</span><span class="sxs-lookup"><span data-stu-id="5284c-330">Before you install agents on computers running Windows, you need tooconfigure hello Docker service.</span></span> <span data-ttu-id="5284c-331">Hallo-configuratie kunt Hallo Windows-agent of Hallo logboekanalyse virtuele machine extensie toouse hello Docker TCP socket zodat Hallo agents Hallo Docker-daemon op afstand toegang en toocapture gegevens voor de bewaking.</span><span class="sxs-lookup"><span data-stu-id="5284c-331">hello configuration allows hello Windows agent or hello Log Analytics virtual machine extension toouse hello Docker TCP socket so that hello agents can access hello Docker daemon remotely and toocapture data for monitoring.</span></span>

#### <a name="toostart-docker-and-verify-its-configuration"></a><span data-ttu-id="5284c-332">toostart Docker en controleer of de configuratie</span><span class="sxs-lookup"><span data-stu-id="5284c-332">toostart Docker and verify its configuration</span></span>

<span data-ttu-id="5284c-333">Er zijn tooset stappen die nodig zijn om TCP benoemde pijp voor Windows Server:</span><span class="sxs-lookup"><span data-stu-id="5284c-333">There are steps needed tooset up TCP named pipe for Windows Server:</span></span>

1. <span data-ttu-id="5284c-334">Schakel pipe TCP en named pipe in Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5284c-334">In Windows PowerShell, enable TCP pipe and named pipe.</span></span>

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. <span data-ttu-id="5284c-335">Docker configureren met Hallo-configuratiebestand voor de TCP-pipe en benoemde pijp.</span><span class="sxs-lookup"><span data-stu-id="5284c-335">Configure Docker with hello configuration file for TCP pipe and named pipe.</span></span> <span data-ttu-id="5284c-336">Hallo-configuratiebestand bevindt zich op C:\ProgramData\docker\config\daemon.json.</span><span class="sxs-lookup"><span data-stu-id="5284c-336">hello configuration file is located at C:\ProgramData\docker\config\daemon.json.</span></span>

    <span data-ttu-id="5284c-337">Hallo daemon.json bestand moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="5284c-337">In hello daemon.json file, you will need hello following:</span></span>

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

<span data-ttu-id="5284c-338">Zie voor meer informatie over Hallo Docker-daemon configuratie gebruikt met Windows Containers [Docker-Engine op Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span><span class="sxs-lookup"><span data-stu-id="5284c-338">For more information about hello Docker daemon configuration used with Windows Containers, see [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span></span>


### <a name="install-windows-agents"></a><span data-ttu-id="5284c-339">Windows-agents installeren</span><span class="sxs-lookup"><span data-stu-id="5284c-339">Install Windows agents</span></span>

<span data-ttu-id="5284c-340">tooenable Windows en de Hyper-V-container bewaking, installeert Hallo Microsoft Monitoring Agent (MMA) op Windows-computers die zijn container hosts.</span><span class="sxs-lookup"><span data-stu-id="5284c-340">tooenable Windows and Hyper-V container monitoring, install hello Microsoft Monitoring Agent (MMA) on Windows computers that are container hosts.</span></span> <span data-ttu-id="5284c-341">Voor computers waarop Windows wordt uitgevoerd in uw on-premises-omgeving, Zie [verbinding maken met Windows-computers tooLog Analytics](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="5284c-341">For computers running Windows in your on-premises environment, see [Connect Windows computers tooLog Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="5284c-342">Voor virtuele machines worden uitgevoerd in Azure, koppelt u deze tooLog Analytics Hallo met [extensie van virtuele machine](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="5284c-342">For virtual machines running in Azure, connect them tooLog Analytics using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="5284c-343">U kunt Windows-containers die zijn uitgevoerd op de Service Fabric bewaken.</span><span class="sxs-lookup"><span data-stu-id="5284c-343">You can monitor Windows containers running on Service Fabric.</span></span> <span data-ttu-id="5284c-344">Echter alleen [virtuele machines worden uitgevoerd in Azure](log-analytics-azure-vm-extension.md) en [computers met Windows in uw on-premises omgeving](log-analytics-windows-agents.md) momenteel worden ondersteund voor Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5284c-344">However, only [virtual machines running in Azure](log-analytics-azure-vm-extension.md) and [computers running Windows in your on-premises environment](log-analytics-windows-agents.md) are currently supported for Service Fabric.</span></span>

<span data-ttu-id="5284c-345">U kunt controleren dat Hallo Container bewaking oplossing correct is ingesteld voor Windows.</span><span class="sxs-lookup"><span data-stu-id="5284c-345">You can verify that hello Container Monitoring solution is set correctly for Windows.</span></span> <span data-ttu-id="5284c-346">toocheck of Hallo management pack is gedownload naar behoren zoekt *ContainerManagement.xxx*.</span><span class="sxs-lookup"><span data-stu-id="5284c-346">toocheck whether hello management pack was download properly, look for *ContainerManagement.xxx*.</span></span> <span data-ttu-id="5284c-347">Hallo-bestanden moeten zich in Hallo C:\Program Files\Microsoft Monitoring Agent\Agent\Health State\Management servicepacks map.</span><span class="sxs-lookup"><span data-stu-id="5284c-347">hello files should be in hello C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs folder.</span></span>


## <a name="solution-components"></a><span data-ttu-id="5284c-348">Oplossingsonderdelen</span><span class="sxs-lookup"><span data-stu-id="5284c-348">Solution components</span></span>

<span data-ttu-id="5284c-349">Als u van Windows-agents gebruikmaakt, vervolgens hello volgende management pack is geïnstalleerd op elke computer met een agent wanneer u deze oplossing toevoegt.</span><span class="sxs-lookup"><span data-stu-id="5284c-349">If you are using Windows agents, then hello following management pack is installed on each computer with an agent when you add this solution.</span></span> <span data-ttu-id="5284c-350">Er is geen configuratie of het onderhoud is vereist voor Hallo management pack.</span><span class="sxs-lookup"><span data-stu-id="5284c-350">No configuration or maintenance is required for hello management pack.</span></span>

- <span data-ttu-id="5284c-351">*ContainerManagement.xxx* in C:\Program Files\Microsoft Monitoring Agent\Agent\Health State\Management servicepacks zijn geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="5284c-351">*ContainerManagement.xxx* installed in C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span></span>

## <a name="container-data-collection-details"></a><span data-ttu-id="5284c-352">De verzameling Gegevensdetails container</span><span class="sxs-lookup"><span data-stu-id="5284c-352">Container data collection details</span></span>
<span data-ttu-id="5284c-353">Hallo Container bewaking oplossing verzamelt verschillende metrische gegevens en logboekbestanden prestatiegegevens van container-hosts en containers met agents die u inschakelt.</span><span class="sxs-lookup"><span data-stu-id="5284c-353">hello Container Monitoring solution collects various performance metrics and log data from container hosts and containers using agents that you enable.</span></span>

<span data-ttu-id="5284c-354">Gegevens worden elke drie minuten worden verzameld door Hallo typen van de agent te volgen.</span><span class="sxs-lookup"><span data-stu-id="5284c-354">Data is collected every three minutes by hello following agent types.</span></span>

- [<span data-ttu-id="5284c-355">OMS-Agent voor Linux</span><span class="sxs-lookup"><span data-stu-id="5284c-355">OMS Agent for Linux</span></span>](log-analytics-linux-agents.md)
- [<span data-ttu-id="5284c-356">Windows-agent</span><span class="sxs-lookup"><span data-stu-id="5284c-356">Windows agent</span></span>](log-analytics-windows-agents.md)
- [<span data-ttu-id="5284c-357">Log Analytics VM-extensie</span><span class="sxs-lookup"><span data-stu-id="5284c-357">Log Analytics VM extension</span></span>](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a><span data-ttu-id="5284c-358">Containerrecords</span><span class="sxs-lookup"><span data-stu-id="5284c-358">Container records</span></span>

<span data-ttu-id="5284c-359">Hallo ziet volgende tabel u voorbeelden van records die is verzameld door Hallo Container bewaking oplossing en Hallo-gegevenstypen die worden weergegeven in zoekresultaten logboek.</span><span class="sxs-lookup"><span data-stu-id="5284c-359">hello following table shows examples of records collected by hello Container Monitoring solution and hello data types that appear in log search results.</span></span>

| <span data-ttu-id="5284c-360">Gegevenstype</span><span class="sxs-lookup"><span data-stu-id="5284c-360">Data type</span></span> | <span data-ttu-id="5284c-361">Het gegevenstype in logboek zoeken</span><span class="sxs-lookup"><span data-stu-id="5284c-361">Data type in Log Search</span></span> | <span data-ttu-id="5284c-362">Velden</span><span class="sxs-lookup"><span data-stu-id="5284c-362">Fields</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5284c-363">Prestaties voor hosts en -containers</span><span class="sxs-lookup"><span data-stu-id="5284c-363">Performance for hosts and containers</span></span> | `Type=Perf` | <span data-ttu-id="5284c-364">Computer, ObjectName, CounterName &#40; percentage processortijd schijf leest MB, schijf schrijft MB geheugen gebruik MB netwerk ontvangen Bytes, netwerk verzenden Bytes Processor gebruik seconde, netwerk &#41; tegenwaarde, TimeGenerated, itempad, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="5284c-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span></span> |
| <span data-ttu-id="5284c-365">Inventarisatie van de container</span><span class="sxs-lookup"><span data-stu-id="5284c-365">Container inventory</span></span> | `Type=ContainerInventory` | <span data-ttu-id="5284c-366">TimeGenerated, Computer, containernaam ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, opdracht, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span><span class="sxs-lookup"><span data-stu-id="5284c-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span></span> |
| <span data-ttu-id="5284c-367">Container installatiekopie inventarisatie</span><span class="sxs-lookup"><span data-stu-id="5284c-367">Container image inventory</span></span> | `Type=ContainerImageInventory` | <span data-ttu-id="5284c-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, uitvoering is onderbroken, gestopt, is mislukt, SourceSystem, ImageID, TotalContainer</span><span class="sxs-lookup"><span data-stu-id="5284c-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span></span> |
| <span data-ttu-id="5284c-369">Container-logboek</span><span class="sxs-lookup"><span data-stu-id="5284c-369">Container log</span></span> | `Type=ContainerLog` | <span data-ttu-id="5284c-370">TimeGenerated, Computer, afbeeldings-ID, containernaam LogEntrySource, LogEntry, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="5284c-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="5284c-371">Container service-logboek</span><span class="sxs-lookup"><span data-stu-id="5284c-371">Container service log</span></span> | `Type=ContainerServiceLog`  | <span data-ttu-id="5284c-372">TimeGenerated, Computer, TimeOfCommand, Image, opdracht, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="5284c-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="5284c-373">Container knooppunt inventarisatie</span><span class="sxs-lookup"><span data-stu-id="5284c-373">Container node inventory</span></span> | `Type=ContainerNodeInventory_CL`| <span data-ttu-id="5284c-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="5284c-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span></span>|
| <span data-ttu-id="5284c-375">Kubernetes-inventarisatie</span><span class="sxs-lookup"><span data-stu-id="5284c-375">Kubernetes inventory</span></span> | `Type=KubePodInventory_CL` | <span data-ttu-id="5284c-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="5284c-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span></span> |
| <span data-ttu-id="5284c-377">Container-proces</span><span class="sxs-lookup"><span data-stu-id="5284c-377">Container process</span></span> | `Type=ContainerProcess_CL` | <span data-ttu-id="5284c-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="5284c-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span></span> |
| <span data-ttu-id="5284c-379">Kubernetes gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="5284c-379">Kubernetes events</span></span> | `Type=KubeEvents_CL` | <span data-ttu-id="5284c-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, bericht</span><span class="sxs-lookup"><span data-stu-id="5284c-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span></span> |

<span data-ttu-id="5284c-381">Labels toegevoegd te*PodLabel* gegevenstypen zijn uw eigen aangepaste etiketten.</span><span class="sxs-lookup"><span data-stu-id="5284c-381">Labels appended too*PodLabel* data types are your own custom labels.</span></span> <span data-ttu-id="5284c-382">Hallo zijn toegevoegde PodLabel labels weergegeven in de tabel Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="5284c-382">hello appended PodLabel labels shown in hello table are examples.</span></span> <span data-ttu-id="5284c-383">Dus `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` wordt verschillen in uw omgeving gegevensset en algemeen fungeren als `PodLabel_yourlabel_s`.</span><span class="sxs-lookup"><span data-stu-id="5284c-383">So, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` will differ in your environment's data set and generically resemble `PodLabel_yourlabel_s`.</span></span>


## <a name="monitor-containers"></a><span data-ttu-id="5284c-384">Monitor containers</span><span class="sxs-lookup"><span data-stu-id="5284c-384">Monitor containers</span></span>
<span data-ttu-id="5284c-385">Nadat u ingeschakeld in de OMS-portal Hallo Hallo-oplossing hebt, Hallo **Containers** tegel samenvattingsinformatie over de container-hosts en het Hallo-containers die zijn uitgevoerd in de hosts.</span><span class="sxs-lookup"><span data-stu-id="5284c-385">After you have hello solution enabled in hello OMS portal, hello **Containers** tile shows summary information about your container hosts and hello containers running in hosts.</span></span>

![Containers tegel](./media/log-analytics-containers/containers-title.png)

<span data-ttu-id="5284c-387">Hallo-tegel geeft een overzicht van hoeveel containers die u hebt in het Hallo-omgeving en of ze klaar is mislukt, uitgevoerd of gestopt.</span><span class="sxs-lookup"><span data-stu-id="5284c-387">hello tile shows an overview of how many containers you have in hello environment and whether they're failed, running, or stopped.</span></span>

### <a name="using-hello-containers-dashboard"></a><span data-ttu-id="5284c-388">Met behulp van Hallo Containers dashboard</span><span class="sxs-lookup"><span data-stu-id="5284c-388">Using hello Containers dashboard</span></span>
<span data-ttu-id="5284c-389">Klik op Hallo **Containers** tegel.</span><span class="sxs-lookup"><span data-stu-id="5284c-389">Click hello **Containers** tile.</span></span> <span data-ttu-id="5284c-390">Daar ziet u weergaven onderverdeeld op basis van:</span><span class="sxs-lookup"><span data-stu-id="5284c-390">From there you'll see views organized by:</span></span>

- <span data-ttu-id="5284c-391">**Gebeurtenissen van de container** -toont de status van de container en computers met mislukte containers.</span><span class="sxs-lookup"><span data-stu-id="5284c-391">**Container Events** - Shows container status and computers with failed containers.</span></span>
- <span data-ttu-id="5284c-392">**Logboeken van de container** -bevat een grafiek met logboekbestanden container gegenereerd over tijd en een lijst met computers met Hallo hoogste aantal logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="5284c-392">**Container Logs** - Shows a chart of container log files generated over time and a list of computers with hello highest number of log files.</span></span>
- <span data-ttu-id="5284c-393">**Kubernetes gebeurtenissen** -bevat een grafiek met Kubernetes gebeurtenissen gegenereerd over tijd en een lijst met Hallo redenen waarom gehele product Hallo gebeurtenissen gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="5284c-393">**Kubernetes Events** - Shows a chart of Kubernetes events generated over time and a list of hello reasons why pods generated hello events.</span></span> <span data-ttu-id="5284c-394">*Deze gegevensset wordt alleen gebruikt in omgevingen met Linux.*</span><span class="sxs-lookup"><span data-stu-id="5284c-394">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="5284c-395">**Kubernetes Namespace inventaris** - toont Hallo aantal naamruimten en gehele product en toont hun hiërarchie.</span><span class="sxs-lookup"><span data-stu-id="5284c-395">**Kubernetes Namespace Inventory** - Shows hello number of namespaces and pods and shows their hierarchy.</span></span> <span data-ttu-id="5284c-396">*Deze gegevensset wordt alleen gebruikt in omgevingen met Linux.*</span><span class="sxs-lookup"><span data-stu-id="5284c-396">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="5284c-397">**Container knooppunt inventaris** -Hallo aantal orchestration die worden gebruikt op de container-knooppunten/hosts bevat.</span><span class="sxs-lookup"><span data-stu-id="5284c-397">**Container Node Inventory** - Shows hello number of orchestration types used on container nodes/hosts.</span></span> <span data-ttu-id="5284c-398">Hallo computer knooppunten/hosts staan ook door Hallo aantal containers.</span><span class="sxs-lookup"><span data-stu-id="5284c-398">hello computer nodes/hosts are also listed by hello number of containers.</span></span> <span data-ttu-id="5284c-399">*Deze gegevensset wordt alleen gebruikt in omgevingen met Linux.*</span><span class="sxs-lookup"><span data-stu-id="5284c-399">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="5284c-400">**Container installatiekopieën inventaris** -toont Hallo kunt u het totale aantal container afbeeldingen die worden gebruikt en het aantal afbeeldingstypen.</span><span class="sxs-lookup"><span data-stu-id="5284c-400">**Container Images Inventory** - Shows hello total number of container images used and number of image types.</span></span> <span data-ttu-id="5284c-401">Hallo aantal afbeeldingen worden ook vermeld door Hallo afbeeldingscode.</span><span class="sxs-lookup"><span data-stu-id="5284c-401">hello number of images are also listed by hello image tag.</span></span>
- <span data-ttu-id="5284c-402">**Status van de containers** -totaal aantal container Hallo knooppunten/host-computers met actieve containers bevat.</span><span class="sxs-lookup"><span data-stu-id="5284c-402">**Containers Status** - Shows hello total number of container nodes/host computers that have running containers.</span></span> <span data-ttu-id="5284c-403">Computers worden ook vermeld door Hallo aantal hosts uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5284c-403">Computers are also listed by hello number of running hosts.</span></span>
- <span data-ttu-id="5284c-404">**Container proces** -ziet u een lijndiagram van container processen uitgevoerd gedurende een periode.</span><span class="sxs-lookup"><span data-stu-id="5284c-404">**Container Process** - Shows a line chart of container processes running over time.</span></span> <span data-ttu-id="5284c-405">Containers worden ook vermeld door te voeren opdracht/proces binnen containers.</span><span class="sxs-lookup"><span data-stu-id="5284c-405">Containers are also listed by running command/process within containers.</span></span> <span data-ttu-id="5284c-406">*Deze gegevensset wordt alleen gebruikt in omgevingen met Linux.*</span><span class="sxs-lookup"><span data-stu-id="5284c-406">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="5284c-407">**Container CPU-prestaties** -een lijndiagram Hallo gemiddelde CPU-gebruik gedurende een bepaalde periode voor computer-knooppunten/hosts bevat.</span><span class="sxs-lookup"><span data-stu-id="5284c-407">**Container CPU Performance** - Shows a line chart of hello average CPU utilization over time for computer nodes/hosts.</span></span> <span data-ttu-id="5284c-408">Een lijst met Hallo computer knooppunten/fungeert als host gebaseerd ook op gemiddelde CPU-gebruik.</span><span class="sxs-lookup"><span data-stu-id="5284c-408">Also lists hello computer nodes/hosts based on average CPU utilization.</span></span>
- <span data-ttu-id="5284c-409">**Container geheugenprestaties** -ziet u een lijndiagram geheugengebruik gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="5284c-409">**Container Memory Performance** - Shows a line chart of memory usage over time.</span></span> <span data-ttu-id="5284c-410">Een lijst met computergeheugen gebruik op basis van de exemplaarnaam.</span><span class="sxs-lookup"><span data-stu-id="5284c-410">Also lists computer memory utilization based on instance name.</span></span>
- <span data-ttu-id="5284c-411">**Prestaties van de computer** -worden lijndiagrammen van Hallo procent van de CPU-prestaties na verloop van tijd percentage geheugengebruik gedurende een bepaalde tijd, megabytes aan vrije schijfruimte voor een periode.</span><span class="sxs-lookup"><span data-stu-id="5284c-411">**Computer Performance** - Shows line charts of hello percent of CPU performance over time, percent of memory usage over time, and megabytes of free disk space over time.</span></span> <span data-ttu-id="5284c-412">U kunt op elke regel in een grafiek tooview plaatst meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5284c-412">You can hover over any line in a chart tooview more details.</span></span>


<span data-ttu-id="5284c-413">Elk onderdeel van het Hallo-dashboard is een visuele representatie van een zoekopdracht die wordt uitgevoerd op de verzamelde gegevens.</span><span class="sxs-lookup"><span data-stu-id="5284c-413">Each area of hello dashboard is a visual representation of a search that is run on collected data.</span></span>

![Containers dashboard](./media/log-analytics-containers/containers-dash01.png)

![Containers dashboard](./media/log-analytics-containers/containers-dash02.png)

<span data-ttu-id="5284c-416">In Hallo **Container Status** gebied, klikt u op Hallo bovenste gebied, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5284c-416">In hello **Container Status** area, click hello top area, as shown below.</span></span>

![Status van de containers](./media/log-analytics-containers/containers-status.png)

<span data-ttu-id="5284c-418">Logboek zoeken met de informatie over Hallo status van uw containers wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="5284c-418">Log Search opens, displaying information about hello state of your containers.</span></span>

![Meld u zoeken naar containers](./media/log-analytics-containers/containers-log-search.png)

<span data-ttu-id="5284c-420">Hier kunt u Hallo zoeken query toomodify kunt bewerken het toofind Hallo specifieke informatie u geïnteresseerd bent in.</span><span class="sxs-lookup"><span data-stu-id="5284c-420">From here, you can edit hello search query toomodify it toofind hello specific information you're interested in.</span></span> <span data-ttu-id="5284c-421">Zie voor meer informatie over logboek zoekacties [zoekopdrachten aanmelden met logboekanalyse](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="5284c-421">For more information about Log Searches, see [Log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

## <a name="troubleshoot-by-finding-a-failed-container"></a><span data-ttu-id="5284c-422">Problemen oplossen met een mislukte container te zoeken</span><span class="sxs-lookup"><span data-stu-id="5284c-422">Troubleshoot by finding a failed container</span></span>

<span data-ttu-id="5284c-423">Log Analytics markeert een container als **mislukt** als is afgesloten met een afsluitcode dan nul.</span><span class="sxs-lookup"><span data-stu-id="5284c-423">Log Analytics marks a container as **Failed** if it has exited with a non-zero exit code.</span></span> <span data-ttu-id="5284c-424">U kunt een overzicht van Hallo fouten en storingen in Hallo-omgeving in Hallo **Containers mislukt** gebied.</span><span class="sxs-lookup"><span data-stu-id="5284c-424">You can see an overview of hello errors and failures in hello environment in hello **Failed Containers** area.</span></span>

### <a name="toofind-failed-containers"></a><span data-ttu-id="5284c-425">containers toofind is mislukt</span><span class="sxs-lookup"><span data-stu-id="5284c-425">toofind failed containers</span></span>
1. <span data-ttu-id="5284c-426">Klik op Hallo **Container Status** gebied.</span><span class="sxs-lookup"><span data-stu-id="5284c-426">Click hello **Container Status** area.</span></span>  
   <span data-ttu-id="5284c-427">![status van de containers](./media/log-analytics-containers/containers-status.png)</span><span class="sxs-lookup"><span data-stu-id="5284c-427">![containers status](./media/log-analytics-containers/containers-status.png)</span></span>
2. <span data-ttu-id="5284c-428">Logboek zoeken wordt geopend en bevat Hallo status van de containers vergelijkbare toohello te volgen.</span><span class="sxs-lookup"><span data-stu-id="5284c-428">Log Search opens and displays hello state of your containers, similar toohello following.</span></span>  
   ![status van de containers](./media/log-analytics-containers/containers-log-search.png)
3. <span data-ttu-id="5284c-430">Klik vervolgens op Hallo geaggregeerd waarde van de mislukte containers tooview aanvullende informatie.</span><span class="sxs-lookup"><span data-stu-id="5284c-430">Next, click hello aggregated value of failed containers tooview additional information.</span></span> <span data-ttu-id="5284c-431">Vouw **meer** tooview Hallo installatiekopie-ID.</span><span class="sxs-lookup"><span data-stu-id="5284c-431">Expand **show more** tooview hello image ID.</span></span>  
   <span data-ttu-id="5284c-432">![mislukte containers](./media/log-analytics-containers/containers-state-failed.png)</span><span class="sxs-lookup"><span data-stu-id="5284c-432">![failed containers](./media/log-analytics-containers/containers-state-failed.png)</span></span>  
4. <span data-ttu-id="5284c-433">Typ vervolgens Hallo volgende in de zoekopdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="5284c-433">Next, type hello following in hello search query.</span></span> <span data-ttu-id="5284c-434">`Type=ContainerInventory <ImageID>`toosee details over de installatiekopie van het Hallo zoals afbeeldingsgrootte en aantal gestopt en mislukte afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="5284c-434">`Type=ContainerInventory <ImageID>` toosee details about hello image such as image size and number of stopped and failed images.</span></span>  
   <span data-ttu-id="5284c-435">![mislukte containers](./media/log-analytics-containers/containers-failed04.png)</span><span class="sxs-lookup"><span data-stu-id="5284c-435">![failed containers](./media/log-analytics-containers/containers-failed04.png)</span></span>

## <a name="search-logs-for-container-data"></a><span data-ttu-id="5284c-436">Zoeken in Logboeken voor containergegevens</span><span class="sxs-lookup"><span data-stu-id="5284c-436">Search logs for container data</span></span>
<span data-ttu-id="5284c-437">Wanneer u een specifieke fout oplossen bent, kunt u toosee waar deze in uw omgeving voordoet zich.</span><span class="sxs-lookup"><span data-stu-id="5284c-437">When you're troubleshooting a specific error, it can help toosee where it is occurring in your environment.</span></span> <span data-ttu-id="5284c-438">Hallo logboek typen volgen helpt u query's tooreturn Hallo informatie die u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="5284c-438">hello following log types will help you create queries tooreturn hello information you want.</span></span>


- <span data-ttu-id="5284c-439">**ContainerImageInventory** – Gebruik dit type wanneer u toofind informatie onderverdeeld op basis van de installatiekopie en tooview installatiekopiegegevens zoals installatiekopie-id's of grootte probeert.</span><span class="sxs-lookup"><span data-stu-id="5284c-439">**ContainerImageInventory** – Use this type when you're trying toofind information organized by image and tooview image information such as image IDs or sizes.</span></span>
- <span data-ttu-id="5284c-440">**ContainerInventory** – Gebruik dit type wanneer u informatie over de containerlocatie wilt, wat hun namen zijn en wat ze uitvoert installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="5284c-440">**ContainerInventory** – Use this type when you want information about container location, what their names are, and what images they're running.</span></span>
- <span data-ttu-id="5284c-441">**ContainerLog** – Gebruik dit type als u wilt dat specifieke foutinformatie logboek toofind en vermeldingen.</span><span class="sxs-lookup"><span data-stu-id="5284c-441">**ContainerLog** – Use this type when you want toofind specific error log information and entries.</span></span>
- <span data-ttu-id="5284c-442">**ContainerNodeInventory_CL** Gebruik dit type als u Hallo informatie over het hostknooppunt wilt/containers wonen waar.</span><span class="sxs-lookup"><span data-stu-id="5284c-442">**ContainerNodeInventory_CL**  Use this type when you want hello information about host/node where containers are residing.</span></span> <span data-ttu-id="5284c-443">Dit biedt u Docker-versie, orchestration-type, opslag en informatie over het netwerk.</span><span class="sxs-lookup"><span data-stu-id="5284c-443">It provides you Docker version, orchestration type, storage, and network information.</span></span>
- <span data-ttu-id="5284c-444">**ContainerProcess_CL** Gebruik dit type tooquickly Zie Hallo-proces binnen Hallo container wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5284c-444">**ContainerProcess_CL** Use this type tooquickly see hello process running within hello container.</span></span>
- <span data-ttu-id="5284c-445">**ContainerServiceLog** – Gebruik dit type wanneer u de audittrail controlegegevens toofind probeert voor hello Docker-daemon, zoals het starten, stoppen, verwijderen of pull-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="5284c-445">**ContainerServiceLog** – Use this type when you're trying toofind audit trail information for hello Docker daemon, such as start, stop, delete, or pull commands.</span></span>
- <span data-ttu-id="5284c-446">**KubeEvents_CL** gebruikt dit type toosee hello Kubernetes gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="5284c-446">**KubeEvents_CL**  Use this type toosee hello Kubernetes events.</span></span>
- <span data-ttu-id="5284c-447">**KubePodInventory_CL** gebruik van dit type als u toounderstand Hallo clustergegevens hiërarchie wilt.</span><span class="sxs-lookup"><span data-stu-id="5284c-447">**KubePodInventory_CL**  Use this type when you want toounderstand hello cluster hierarchy information.</span></span>


### <a name="toosearch-logs-for-container-data"></a><span data-ttu-id="5284c-448">toosearch logboeken voor containergegevens</span><span class="sxs-lookup"><span data-stu-id="5284c-448">toosearch logs for container data</span></span>
* <span data-ttu-id="5284c-449">Kies een installatiekopie die u kent onlangs is mislukt en Hallo foutenlogboeken voor het vinden.</span><span class="sxs-lookup"><span data-stu-id="5284c-449">Choose an image that you know has failed recently and find hello error logs for it.</span></span> <span data-ttu-id="5284c-450">Starten door te zoeken naar een containernaam die wordt uitgevoerd die afbeelding met een **ContainerInventory** zoeken.</span><span class="sxs-lookup"><span data-stu-id="5284c-450">Start by finding a container name that is running that image with a **ContainerInventory** search.</span></span> <span data-ttu-id="5284c-451">Bijvoorbeeld zoeken naar`Type=ContainerInventory ubuntu Failed`</span><span class="sxs-lookup"><span data-stu-id="5284c-451">For example, search for `Type=ContainerInventory ubuntu Failed`</span></span>  
    <span data-ttu-id="5284c-452">![Zoeken naar Ubuntu-containers](./media/log-analytics-containers/search-ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="5284c-452">![Search for Ubuntu containers](./media/log-analytics-containers/search-ubuntu.png)</span></span>

  <span data-ttu-id="5284c-453">naam van de container Hallo naast Hallo te**naam**, en zoek naar deze logboeken.</span><span class="sxs-lookup"><span data-stu-id="5284c-453">hello name of hello container next too**Name**, and search for those logs.</span></span> <span data-ttu-id="5284c-454">In dit voorbeeld is het `Type=ContainerLog cranky_stonebreaker`.</span><span class="sxs-lookup"><span data-stu-id="5284c-454">In this example, it is `Type=ContainerLog cranky_stonebreaker`.</span></span>

<span data-ttu-id="5284c-455">**Informatie over prestaties weergeven**</span><span class="sxs-lookup"><span data-stu-id="5284c-455">**View performance information**</span></span>

<span data-ttu-id="5284c-456">Wanneer u tooconstruct query's begint bent, kunt u toosee wat is er mogelijk eerst.</span><span class="sxs-lookup"><span data-stu-id="5284c-456">When you're beginning tooconstruct queries, it can help toosee what's possible first.</span></span> <span data-ttu-id="5284c-457">Bijvoorbeeld: toosee zoeken van alle prestatiegegevens, probeer een brede query door op te geven Hallo volgende query uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5284c-457">For example, toosee all performance data, try a broad query by typing hello following search query.</span></span>

```
Type=Perf
```

![prestaties van de containers](./media/log-analytics-containers/containers-perf01.png)

<span data-ttu-id="5284c-459">U kunt het bereik van prestatiegegevens Hallo u ziet, tooa specifieke container door Hallo naam ervan te typen toohello rechts van uw query.</span><span class="sxs-lookup"><span data-stu-id="5284c-459">You can scope hello performance data you're seeing tooa specific container by typing hello name of it toohello right of your query.</span></span>

```
Type=Perf <containerName>
```

<span data-ttu-id="5284c-460">Geeft aan Hallo lijst maatstaven voor prestaties die worden verzameld voor een afzonderlijke-container.</span><span class="sxs-lookup"><span data-stu-id="5284c-460">That shows hello list of performance metrics that are collected for an individual container.</span></span>

![prestaties van de containers](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a><span data-ttu-id="5284c-462">Voorbeeld logboek zoekquery 's</span><span class="sxs-lookup"><span data-stu-id="5284c-462">Example log search queries</span></span>
<span data-ttu-id="5284c-463">Het vaak nuttig toobuild vraagt beginnen met een voorbeeld of twee en wijzigen ze toofit op uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="5284c-463">It's often useful toobuild queries starting with an example or two and then modifying them toofit your environment.</span></span> <span data-ttu-id="5284c-464">Als uitgangspunt, kunt u experimenteren met Hallo **voorbeeldquery's** gebied toohelp u meer geavanceerde query's opbouwen.</span><span class="sxs-lookup"><span data-stu-id="5284c-464">As a starting point, you can experiment with hello **Sample Queries** area toohelp you build more advanced queries.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Containers query 's](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a><span data-ttu-id="5284c-466">Zoekopdrachten opslaan logboek</span><span class="sxs-lookup"><span data-stu-id="5284c-466">Saving log search queries</span></span>
<span data-ttu-id="5284c-467">Query's opslaan, is een standaardfunctie in logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="5284c-467">Saving queries is a standard feature in Log Analytics.</span></span> <span data-ttu-id="5284c-468">Door deze te slaan, hebt u die u hebt gevonden nuttig bij de hand hebt voor toekomstig gebruik.</span><span class="sxs-lookup"><span data-stu-id="5284c-468">By saving them, you'll have those that you've found useful handy for future use.</span></span>

<span data-ttu-id="5284c-469">Nadat u een query die nuttig maakt, deze door te klikken op Opslaan **Favorieten** bovenaan Hallo Hallo logboek zoekpagina.</span><span class="sxs-lookup"><span data-stu-id="5284c-469">After you create a query that you find useful, save it by clicking **Favorites** at hello top of hello Log Search page.</span></span> <span data-ttu-id="5284c-470">En u eenvoudig toegang dit later uit Hallo tot kunt **mijn Dashboard** pagina.</span><span class="sxs-lookup"><span data-stu-id="5284c-470">Then you can easily access it later from hello **My Dashboard** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5284c-471">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5284c-471">Next steps</span></span>
* <span data-ttu-id="5284c-472">[Zoeken in een logboek](log-analytics-log-searches.md) tooview gedetailleerde gegevensrecords container.</span><span class="sxs-lookup"><span data-stu-id="5284c-472">[Search logs](log-analytics-log-searches.md) tooview detailed container data records.</span></span>
